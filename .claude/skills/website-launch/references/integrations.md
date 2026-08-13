# Integrations

Working code for the two integrations every service site needs. *Last reviewed: August 2026 — verify SDK option names against the installed package version before shipping.*

---

## Contact form → email (Resend)

```bash
npm install resend
```

### Environment variables

`.env.local` (never committed — confirm it is in `.gitignore`):

```
RESEND_API_KEY=re_xxxxxxxxxxxx
CONTACT_TO_EMAIL=clinic@example.com
CONTACT_FROM_EMAIL=website@yourdomain.com
```

`CONTACT_FROM_EMAIL` must be on a domain verified in Resend, or delivery fails. The same three variables must also be added in the Vercel dashboard, followed by a redeploy.

### Route handler — `app/api/contact/route.ts`

```ts
import { NextResponse } from 'next/server'
import { Resend } from 'resend'

const resend = new Resend(process.env.RESEND_API_KEY)

export async function POST(req: Request) {
  try {
    const { name, phone, email, service, message } = await req.json()

    // Never trust the client. Validate server-side too.
    if (!name?.trim() || !phone?.trim()) {
      return NextResponse.json(
        { error: 'Name and phone are required.' },
        { status: 400 },
      )
    }

    await resend.emails.send({
      from: process.env.CONTACT_FROM_EMAIL!,
      to: process.env.CONTACT_TO_EMAIL!,
      replyTo: email || undefined, // older resend SDKs name this `reply_to`
      subject: `New enquiry from ${name}`,
      text: [
        `Name:    ${name}`,
        `Phone:   ${phone}`,
        `Email:   ${email || '—'}`,
        `Service: ${service || '—'}`,
        '',
        message || '(no message)',
      ].join('\n'),
    })

    return NextResponse.json({ ok: true })
  } catch (err) {
    console.error('Contact form failed:', err)
    // Never leak internal error details to the browser.
    return NextResponse.json(
      { error: 'Could not send. Please call us instead.' },
      { status: 500 },
    )
  }
}
```

`replyTo` lets the business hit Reply and answer the customer directly. The option is named `replyTo` in recent SDK versions and `reply_to` in older ones — check which is installed.

### Client form requirements

The form must handle four states, not two. Most beginner forms only handle "idle" and break the moment anything goes wrong:

- **idle** — normal
- **submitting** — button disabled, spinner visible, so nobody double-submits
- **success** — clear confirmation that stays on screen
- **error** — the failure message **plus a phone number**, so a broken form never costs the business a customer

Also required: real `<label>` elements, `type="tel"` on phone fields and `type="email"` on email (mobile keyboards adapt), `autoComplete` attributes, and a visible privacy note if any health or personal detail is collected.

### Spam protection

Public forms attract bots. The lightest effective defence is a honeypot — a field hidden from humans that bots fill in anyway:

```tsx
<input
  type="text"
  name="company"
  tabIndex={-1}
  autoComplete="off"
  aria-hidden="true"
  style={{ position: 'absolute', left: '-9999px' }}
/>
```

Reject the submission server-side if that field has any value. No CAPTCHA, no friction for real users. If spam persists, add Cloudflare Turnstile.

---

## Booking (Cal.com)

### Option A — link out (most robust)

```tsx
<a
  href="https://cal.com/your-handle/consultation"
  target="_blank"
  rel="noopener noreferrer"
  className="btn-primary"
>
  Book an appointment
</a>
```

Nothing to break, works everywhere. The tradeoff is that the visitor leaves the site.

### Option B — embed (keeps visitors on the site)

```bash
npm install @calcom/embed-react
```

```tsx
'use client'
import Cal from '@calcom/embed-react'

export function BookingEmbed() {
  return (
    <Cal
      calLink="your-handle/consultation"
      style={{ width: '100%', height: '100%', minHeight: 600 }}
      config={{ layout: 'month_view' }}
    />
  )
}
```

Must be a client component. Give it a real `minHeight` or it can collapse on mobile.

**Always keep a phone number next to the booking widget.** Third-party embeds fail — blocked by privacy extensions, slow networks, ad blockers. An older visitor who cannot make the widget work should never be stranded.

### Option C — WhatsApp (strongest in many markets)

```tsx
<a href="https://wa.me/9715XXXXXXXX?text=Hi,%20I'd%20like%20to%20book%20an%20appointment">
  Book on WhatsApp
</a>
```

Number in full international format, no `+`, no spaces. In much of the Middle East, South Asia, and Latin America this converts better than any booking widget, because it is where people already are. Do not assume a Western booking flow is the right default — ask what the local market uses.

---

## Analytics

```bash
npm install @vercel/analytics
```

```tsx
// app/layout.tsx
import { Analytics } from '@vercel/analytics/react'

// inside <body>
<Analytics />
```

No cookie banner required, since it sets no cookies — a genuine advantage over Google Analytics for a small site with EU visitors.
