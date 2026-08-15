---
name: client-dashboard
description: Add a custom booking system and a private client dashboard to a service-business website using Supabase — the business owner logs in to see, cancel, and reschedule appointments, and read enquiries. Use when the user wants their client to manage bookings themselves, wants a login area, an admin panel, a booking system they own rather than a third-party link, or asks for a database, Supabase, user accounts, or a members area on a site built with the website-launch skill.
---

# Client Dashboard (Tier 2)

Upgrades a brochure site into a system the business owner logs into and runs. Replaces the third-party booking link with a booking system they own.

**This is the paid upgrade.** A brochure site is a one-off fee. A site where the owner logs in every morning to see the day's appointments is worth more and justifies a monthly maintenance fee. Say so when the user is pricing work.

## When this applies — and when it does not

**Use it when** the business takes appointments and the owner wants to manage them on their own site, needs enquiries kept in one place rather than scattered across an inbox, or wants staff to have logins.

**Do not use it when** a brochure site would serve the client fine. Most small businesses are genuinely well served by Tier 1. Selling a database to a barber with a paper diary is how students get refund requests. Ask what the owner does today before recommending this.

## Where this sits in the build

This skill is entered from **Step 11 of `website-launch/references/deployment.md`**, at the point where booking is chosen. Everything before Step 11 is identical for every student. Everything after rejoins the same path.

**Do not restart the progress chart, and do not renumber it.** The user has seen one picture with six columns. Keep those six, and show the extra work *inside* column 5:

```
**Your progress**

| | | |
|---|---|---|
| 1 | Install + skills | Done |
| 2 | Free accounts | Done |
| 3 | Build the site | Done |
| 4 | Put it online | Done |
| 5 | Bookings | **YOU ARE HERE** — setting up the database |
| 6 | Finish & hand over | — |
```

Move the note beside **YOU ARE HERE** as you go: *setting up the database* → *building the booking system* → *building the dashboard* → *testing that data is private*.

**Never say "module", "lesson", or a bare step number** — see `website-launch/SKILL.md` for why. The user is building, not watching a course.

Every rule from `website-launch` still applies here. In particular, **write every instruction in the house format from `website-launch/references/answer-format.md`** — deep links carrying the user's own Supabase project ref, buttons named exactly with their colour, both keyboard shortcuts, exact SQL to paste in code format, and a literal `You should see:` closing every task.

## Stack addition

Supabase — the database, and the login system. Nothing else changes. Cal.com is **not** used on this tier; the booking system replaces it.

Be honest with the user about the one thing they give up: Cal.com sends automatic reminder emails and syncs to Google Calendar out of the box. Here, reminders are something we build. Confirmation emails are straightforward via Resend, which the site already uses. Scheduled reminders need a cron job and are a later addition — do not promise them in week one.

For a **local** business this trade is easy, because every customer is in the same timezone. That removes the hardest part of scheduling. If the client serves customers across countries, say so plainly and reconsider Tier 1.

## Architecture — read before writing code

**All writes go through Next.js API routes, never from the browser to Supabase directly.**

The site already sends the contact form through an API route, so this is the same pattern the student has seen — one idea, reused. It also means the powerful Supabase key stays on the server and never reaches a visitor's browser.

```
Visitor books      → /api/bookings  → Supabase   (server-side key)
Owner views/edits  → logs in        → Supabase   (their own session + RLS)
```

Row Level Security stays switched on for every table regardless. It is the safety net beneath the API routes, not an alternative to them.

## Workflow

1. **Confirm the business actually needs it.** Ask what the owner uses today.
2. **Set up Supabase** — `references/supabase-setup.md`, click by click.
3. **Create the tables and security rules** — same file.
4. **Prove the security works** — the test in that file. Do not skip it, and do not accept "it looks fine".
5. **Build the booking flow** — `references/booking-and-dashboard.md`.
6. **Build the dashboard** — same file.
7. **Deploy and test on the live site**, not locally.
8. Rejoin the walkthrough at the **"Get found on Google"** step, then finish with the security check and handover as normal.

**The security check matters more on this tier.** A Tier 2 site holds a real database of customer names, phone numbers, and appointment reasons. Run `website-launch/references/security-check.md` in full — including re-running the leak test — before handing anything over.

## Hard rules

- **Never launch with Row Level Security disabled.** Not "for now", not "we'll fix it after". A bookings table without it is every customer's name, phone number, and appointment reason readable by anyone who views the page source.
- **The service role key never goes in browser code.** It belongs in `.env.local` and Vercel environment variables, used only inside API routes. If it appears in any file under a `"use client"` directive, stop and fix it.
- **Run the leak test before going live**, and show the user the result.
- **Never invent appointment data.** Seed data must be obviously fake and removed before launch.
- **This is personal data.** Names, phone numbers, and appointment reasons for a clinic are health-adjacent information. Tell the user their client may have legal duties around storing it, and that the privacy notice on the site must say what is collected and why.
- **Always keep a phone number visible** on the booking page. A booking system the visitor cannot use must never be a dead end.

## References

- `references/supabase-setup.md` — account, project, tables, security rules, and the leak test
- `references/booking-and-dashboard.md` — the booking flow and the owner's admin area
