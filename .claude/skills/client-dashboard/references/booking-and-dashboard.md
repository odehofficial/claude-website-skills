# Booking Flow and Owner Dashboard

*Last reviewed: August 2026. Check package names against current Supabase docs before installing — their Next.js auth library has been renamed once already.*

```bash
npm install @supabase/supabase-js @supabase/ssr
```

---

# Step 12 — Build the booking system

## How slots work

Do not build a free-text time picker. Generate **fixed slots** from the business's opening hours and the service duration — 9:00, 9:30, 10:00 — and let the visitor pick one.

This is not a shortcut. It makes double-booking preventable with a single database rule, it matches how receptionists actually think, and it removes an entire category of bug. For a local business every customer shares one timezone, which removes the other hard part.

Hide any slot that is already booked, and any slot in the past.

## The API route

Every booking goes through the server. The browser never talks to the database.

```ts
// app/api/bookings/route.ts
import { NextResponse } from 'next/server'
import { createClient } from '@supabase/supabase-js'
import { Resend } from 'resend'

// Service role key — server-side only. Never import this file into a client component.
const supabase = createClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,
  process.env.SUPABASE_SERVICE_ROLE_KEY!,
)
const resend = new Resend(process.env.RESEND_API_KEY)

export async function POST(req: Request) {
  try {
    const { name, phone, email, serviceId, startsAt, notes, company } =
      await req.json()

    // Honeypot: humans never fill this in.
    if (company) return NextResponse.json({ ok: true })

    if (!name?.trim() || !phone?.trim() || !startsAt) {
      return NextResponse.json(
        { error: 'Please fill in your name, phone number, and a time.' },
        { status: 400 },
      )
    }

    // Refuse bookings in the past, whatever the browser claims.
    if (new Date(startsAt) < new Date()) {
      return NextResponse.json(
        { error: 'That time has already passed. Please pick another.' },
        { status: 400 },
      )
    }

    const { error } = await supabase.from('bookings').insert({
      service_id: serviceId,
      customer_name: name,
      customer_phone: phone,
      customer_email: email || null,
      starts_at: startsAt,
      notes: notes || null,
    })

    // 23505 = the unique index rejected it: someone took this slot first.
    if (error?.code === '23505') {
      return NextResponse.json(
        { error: 'Sorry, that time was just taken. Please choose another.' },
        { status: 409 },
      )
    }
    if (error) throw error

    // Tell the business. Do not let an email failure lose the booking.
    try {
      await resend.emails.send({
        from: process.env.CONTACT_FROM_EMAIL!,
        to: process.env.CONTACT_TO_EMAIL!,
        subject: `New booking — ${name}`,
        text: `${name}\n${phone}\n${email || 'no email'}\n${startsAt}\n\n${notes || ''}`,
      })
      if (email) {
        await resend.emails.send({
          from: process.env.CONTACT_FROM_EMAIL!,
          to: email,
          subject: 'Your appointment is confirmed',
          text: `Hi ${name}, your appointment is confirmed for ${startsAt}.`,
        })
      }
    } catch (mailErr) {
      console.error('Booking saved but email failed:', mailErr)
    }

    return NextResponse.json({ ok: true })
  } catch (err) {
    console.error('Booking failed:', err)
    return NextResponse.json(
      { error: 'Something went wrong. Please call us instead.' },
      { status: 500 },
    )
  }
}
```

**Two details worth teaching:**

The `23505` check is what makes double-booking impossible. Checking "is this slot free?" before inserting is not enough — two people can pass that check in the same instant. The database rule is the only reliable guard.

The email is wrapped in its own `try`. A booking that saved but whose email failed is still a booking. Losing it because of a mail problem would be much worse.

## The form

Same four states as the contact form: idle, submitting, success, error. On error, show the phone number.

Required: real `<label>` elements, `type="tel"`, a visible privacy line explaining what is collected, and slots as large tap targets — at least 44px, since a lot of these bookings happen one-handed on a phone.

---

# Step 13 — Build the owner's dashboard

## Protect the route

Everything under `/dashboard` requires a login. Enforce it in middleware, not in the page — a check inside a component can be bypassed.

```ts
// middleware.ts
import { createServerClient } from '@supabase/ssr'
import { NextResponse, type NextRequest } from 'next/server'

export async function middleware(req: NextRequest) {
  const res = NextResponse.next()
  const supabase = createServerClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!,
    {
      cookies: {
        getAll: () => req.cookies.getAll(),
        setAll: (list) =>
          list.forEach(({ name, value, options }) =>
            res.cookies.set(name, value, options),
          ),
      },
    },
  )

  const { data: { user } } = await supabase.auth.getUser()
  if (!user) return NextResponse.redirect(new URL('/login', req.url))
  return res
}

export const config = { matcher: ['/dashboard/:path*'] }
```

Dashboard pages read through the **anon key with the owner's session**, not the service role key. Row level security then does its job: a signed-in user sees the bookings, a stranger sees nothing.

## What the dashboard contains

Build for someone opening it on a phone behind a reception desk, first thing in the morning.

**Today** — the default view, and the only one that matters most days. Each appointment shows time, customer name, phone as a tap-to-call link, service, and notes. Sorted by time. Today's date visible.

**Upcoming** — the next 7 or 30 days.

**Actions on each booking** — Cancel, Reschedule (pick a new slot), Mark as completed, Mark as no-show. Cancel must ask for confirmation; a mis-tap should not silently delete someone's appointment.

**Enquiries** — contact form messages, newest first, with a read/unread marker so nothing is missed.

**Services** — edit names, durations, prices, and switch a service off without deleting it. This is the part that lets the owner change things without calling the student, which is most of what they are paying for.

## Design notes

Do not decorate this. It is a working tool used in a hurry, often one-handed. Large text, high contrast, obvious buttons, no dense tables. A receptionist glancing at a phone must read the next appointment in under a second.

Cancelling should mark `status = 'cancelled'`, never delete the row. The slot frees up automatically because of the partial unique index, and the history stays intact for the owner.

---

## Before going live

- [ ] The leak test passes, and the test page is deleted
- [ ] The service role key appears in no client component
- [ ] All four environment variables are in Vercel, and the site was redeployed after adding them
- [ ] A real booking made on the live site appears in the dashboard
- [ ] Cancelling frees the slot for someone else
- [ ] Two bookings cannot take the same slot — try it in two browser windows
- [ ] The owner can log in and change their password
- [ ] A privacy notice on the booking form says what is collected and why
- [ ] The phone number is visible on the booking page
- [ ] Fake seed data is removed
