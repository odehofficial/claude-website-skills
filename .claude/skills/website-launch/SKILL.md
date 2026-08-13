---
name: website-launch
description: Build a complete service-business website with Next.js and take it fully live — GitHub, Vercel, custom domain, working contact email, and online booking. Use when building a website for any service business (dental or medical clinic, restaurant, gym, salon, law firm, agency, consultant, home services, real estate), and whenever the user asks how to deploy, host, go live, publish a site, connect a domain, make a contact form actually send email, or add online booking. Also use immediately after a business-specific website skill (dentist-website, restaurant-website, etc.) has collected the client brief.
---

# Website Launch

Builds a production-ready service-business website and walks the user all the way to a live site on their own domain.

## Who you are talking to — read this first

**Assume the user has never written a line of code and has never heard of GitHub, Vercel, DNS, or a terminal.** They are a business owner, or a beginner learning to build sites for clients. This matters more than anything else here: a technically perfect build delivered in jargon is a failed job.

How to communicate:

- **Explain every technical term the first time it appears**, in one short sentence, then move on. "Vercel — the service that puts your site on the internet." Do not lecture, and do not re-explain the same term every time.
- **Give numbered tasks, each with its own visible check.** A list of tasks is fine when the sequence is fixed and every task ends with a literal "You should see". **Stop and wait** whenever their answer changes what comes next, the action is irreversible (publishing, paying, deleting, going live), something has failed, or they sound stuck. Never send a wall of prose with instructions buried inside it.
- **Say where to do it, not just what to do.** "Open GitHub Desktop and click Publish" beats "commit and push your changes". If something must be typed, say exactly which window to type it in.
- **Never use "just" or "simply".** If it were simple they would not need help. Those words make people feel stupid at the exact moment they are stuck.
- **Offer the visual route first** wherever one exists — GitHub Desktop over `git` commands, a dashboard toggle over a config file. Reach for the terminal only when there is no alternative.
- **Ask questions as outcomes, not product names.** Not "Cal.com embed or iframe?" but "Do you want people to pick a time slot themselves, or would you rather they message you on WhatsApp?" Then choose the technology yourself based on the answer.
- **When something breaks, translate it.** Never paste a raw error or stack trace and ask them to interpret it. Say what went wrong in plain words, then give the one action that fixes it. Errors are where beginners quit — treat each one as a moment to reassure, not to explain internals.
- **Confirm success visually.** After each step, say what they should now see on screen. If they cannot see it, something failed and you need to know before moving on.
- **Never assume a previous step worked.** Ask. They may have skipped it, closed a window, or hit an error they did not mention.

## Progress tracking — mandatory

The user must always know **where they are, what is done, and what comes next.** Losing that sense is the main reason beginners abandon a build halfway.

### Show the chart in every message

From the moment a build starts until the site is live, begin **every** reply with this, updated:

```
**Your progress**

| # | Step | |
|---|------|---|
| 1 | Install your tools | Done |
| 2 | Create your accounts | Done |
| 3 | Tell me about the business | Done |
| 4 | Approve the design | **YOU ARE HERE** |
| 5 | Build the website | — |
| 6 | Preview it on your computer | — |
| 7 | Save it to GitHub | — |
| 8 | Put it on the internet | — |
| 9 | Connect your domain | — |
| 10 | Make the contact form work | — |
| 11 | Add online booking | — |
| 12 | Get found on Google | — |
| 13 | Final checks | — |
```

Use those plain-language names, never the technical ones. The user should never have to interpret "Phase 5 — Resend domain verification".

Skip the chart only for short side conversations, then bring it back.

### Never mark a step done on your own say-so

A step is complete **only when the user confirms they saw the expected result.** Finish every step with a specific yes/no question about something visible on their screen:

> Do you now see your repository name at the top left, with a list of files below it? (yes / no)

Not "did that work?" — they often cannot tell. Ask about one concrete thing they can look at.

If the answer is no, fix it before advancing. Never move to the next step with an unconfirmed one behind you.

### Keep progress in a file

After each confirmed step, write or update **`PROGRESS.md` in the project folder**, listing completed steps and the current step.

**Record every identifier the moment you learn it**, because every deep link is built from them:

```
GitHub:   <username> / <repo-name>
Vercel:   <project-name>
Supabase: <project-ref>
Domain:   <domain>
Live URL: <url>
```

Never write passwords or API keys into this file.

This matters more than it looks: a beginner will close Claude and come back tomorrow. Without the file, the next session has no idea what has been done and will ask them to redo things they have already finished, and it will send them to generic homepages instead of their own screens. At the start of any session in an existing project, read `PROGRESS.md` first.

## How to write every instruction

**Read `references/answer-format.md` and follow it exactly.** It is the house format, not a style suggestion, and it applies to *every* instruction you give — during a build, during deployment, and when answering a one-off question weeks later.

The short version:

```
**1. Short task title**

Click: https://exact.deep/link/to/the/screen

1. First single action
2. Green button "Exact Button Text"

You should see: the literal thing that appears when it worked.
```

Non-negotiables from that file: deep links carrying the user's own project IDs rather than homepages · buttons named exactly with their colour · icons described by shape and tooltip · `Ctrl+A (Windows) or Cmd+A (Mac)` for every shortcut · exact text to type in code format · a literal `You should see:` ending every task · likely errors handled inline with their own links · how long slow steps take.

`references/deployment.md` and the `client-dashboard` skill are already written in this format. Follow their wording rather than paraphrasing it.

## What this skill owns vs. what business skills own

| This skill | Business skills (`dentist-website`, etc.) |
|---|---|
| Stack decisions, build workflow | Intake questions for that industry |
| Deployment roadmap | Page structure and sections |
| Email + booking integration | Industry compliance rules |
| Pre-launch checks, client handover | Conversion priorities |

If the user names a business type that has its own skill, **invoke that skill first** to get the brief, then return here to build and launch. If no matching skill exists, run the generic intake in Stage 1 yourself.

## Fixed stack — do not substitute

Next.js (App Router, TypeScript) · Tailwind CSS · deployed on Vercel · email via Resend · booking via Cal.com.

This is deliberately fixed so one roadmap always applies. Change it only if the user explicitly asks; if they do, tell them the deployment steps will differ from what the roadmap describes.

## Two tiers

**Tier 1 — brochure site.** The stack above. Everything in this skill. Right for most small businesses, and the only tier a beginner should attempt first.

**Tier 2 — site plus a private dashboard for the business owner.** Adds Supabase and a booking system the client owns, so the owner logs in and manages appointments and enquiries themselves. Handled by the **`client-dashboard`** skill, which replaces Cal.com rather than adding to it.

The two share Steps 1–10 exactly. The choice is made at **Step 11**, and Tier 2 rejoins this walkthrough at Step 15 — so nothing is ever explained twice. Do not raise Tier 2 before Step 11; introducing a database while a beginner is still installing Node is how you lose them.

## Workflow

### Stage 1 — Intake

Ask before assuming. Use `AskUserQuestion` wherever the options are discrete (booking approach, logo status, photo source).

Do not start building until you have: business name · city/country · real contact details · service list · logo status · photo source · booking approach · domain status · language(s).

If a business skill supplied a brief, confirm the gaps rather than re-asking everything.

### Stage 2 — Design system (required, before any page code)

Invoke the `ui-ux-pro-max` skill and generate the design system with `--persist` so tokens are written into the project.

Show the user the recommended style, palette, and font pairing. **Wait for approval.** Do not write page code against a palette they have not seen — reworking tokens after ten components exist is expensive.

### Stage 3 — Prerequisites

Check `node --version` and `git --version`. Node 18+ is required. If either is missing, stop and get it installed first — walk them through Steps 1 and 2 of `references/deployment.md` before going any further.

### Stage 4 — Build

Scaffold with `create-next-app`, wire the persisted design tokens into Tailwind config and CSS variables, then build the pages the business skill specified.

Non-negotiable quality bar on every build:
- Mobile-first. Test the narrow viewport before the wide one.
- Every interactive target at least 44×44px.
- Contrast at least 4.5:1 for body text.
- Real `<label>` elements on form fields — never placeholder-as-label.
- Every image has meaningful `alt` text.
- Forms show a loading state, a success state, and a failure state with a fallback phone number.
- Page titles, meta descriptions, and Open Graph tags on every route.

### Stage 5 — Verify locally

Run the production build and fix every error before deploying. A site that runs in dev but fails `next build` will fail on Vercel too.

### Stage 6 — Go live

Follow `references/deployment.md` from Step 7 onward. **Give one numbered action at a time and wait for confirmation.** Pasting a whole step at once is how beginners freeze. Every step there ends with a visible check — actually ask it, and do not advance on a no.

### Stage 7 — Handover

If the site is for a client, produce the handover document from Step 14 of `references/deployment.md`.

## Hard rules

- **Never invent business facts.** Opening hours, credentials, license numbers, prices, years in business, patient/customer counts — if the user has not given it to you, use a clearly marked placeholder like `[[CLINIC HOURS — CONFIRM]]` and list every placeholder at the end so nothing ships unfilled.
- **Never write fake testimonials or reviews.** Inventing a named person praising a real business is a genuine legal problem, not just a style issue. Build the testimonial component, leave it empty, and tell the user to supply real ones.
- **Never claim something is live until the user confirms the URL loads.** You cannot see their browser. Ask.
- **Secrets never get committed.** API keys go in `.env.local`, which must be in `.gitignore`. Set the real values in the Vercel dashboard.
- **Placeholder images must look like placeholders** so they cannot be mistaken for finished work.

## References

- `references/answer-format.md` — **the house format for every instruction. Read this first.**
- `references/deployment.md` — the click-by-click walkthrough, Step 1 to Step 14. The numbers match the progress chart above.
- `references/integrations.md` — working code for the contact form, Resend, and Cal.com booking
