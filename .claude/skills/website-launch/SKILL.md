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
- **One step at a time, then stop and wait.** Never send five instructions in one message. Give one action, say what they should see when it works, and wait for confirmation before continuing.
- **Say where to do it, not just what to do.** "Open GitHub Desktop and click Publish" beats "commit and push your changes". If something must be typed, say exactly which window to type it in.
- **Never use "just" or "simply".** If it were simple they would not need help. Those words make people feel stupid at the exact moment they are stuck.
- **Offer the visual route first** wherever one exists — GitHub Desktop over `git` commands, a dashboard toggle over a config file. Reach for the terminal only when there is no alternative.
- **Ask questions as outcomes, not product names.** Not "Cal.com embed or iframe?" but "Do you want people to pick a time slot themselves, or would you rather they message you on WhatsApp?" Then choose the technology yourself based on the answer.
- **When something breaks, translate it.** Never paste a raw error or stack trace and ask them to interpret it. Say what went wrong in plain words, then give the one action that fixes it. Errors are where beginners quit — treat each one as a moment to reassure, not to explain internals.
- **Confirm success visually.** After each step, say what they should now see on screen. If they cannot see it, something failed and you need to know before moving on.
- **Never assume a previous step worked.** Ask. They may have skipped it, closed a window, or hit an error they did not mention.

## What this skill owns vs. what business skills own

| This skill | Business skills (`dentist-website`, etc.) |
|---|---|
| Stack decisions, build workflow | Intake questions for that industry |
| Deployment roadmap | Page structure and sections |
| Email + booking integration | Industry compliance rules |
| Pre-launch checks, client handover | Conversion priorities |

If the user names a business type that has its own skill, **invoke that skill first** to get the brief, then return here to build and launch. If no matching skill exists, run the generic intake in Step 1 yourself.

## Fixed stack — do not substitute

Next.js (App Router, TypeScript) · Tailwind CSS · deployed on Vercel · email via Resend · booking via Cal.com.

This is deliberately fixed so one roadmap always applies. Change it only if the user explicitly asks; if they do, tell them the deployment steps will differ from what the roadmap describes.

## Workflow

### Step 1 — Intake

Ask before assuming. Use `AskUserQuestion` wherever the options are discrete (booking approach, logo status, photo source).

Do not start building until you have: business name · city/country · real contact details · service list · logo status · photo source · booking approach · domain status · language(s).

If a business skill supplied a brief, confirm the gaps rather than re-asking everything.

### Step 2 — Design system (required, before any page code)

Invoke the `ui-ux-pro-max` skill and generate the design system with `--persist` so tokens are written into the project.

Show the user the recommended style, palette, and font pairing. **Wait for approval.** Do not write page code against a palette they have not seen — reworking tokens after ten components exist is expensive.

### Step 3 — Prerequisites

Check `node --version` and `git --version`. Node 18+ is required. If either is missing, stop and get it installed first — see `references/deployment.md` Phase 0.

### Step 4 — Build

Scaffold with `create-next-app`, wire the persisted design tokens into Tailwind config and CSS variables, then build the pages the business skill specified.

Non-negotiable quality bar on every build:
- Mobile-first. Test the narrow viewport before the wide one.
- Every interactive target at least 44×44px.
- Contrast at least 4.5:1 for body text.
- Real `<label>` elements on form fields — never placeholder-as-label.
- Every image has meaningful `alt` text.
- Forms show a loading state, a success state, and a failure state with a fallback phone number.
- Page titles, meta descriptions, and Open Graph tags on every route.

### Step 5 — Verify locally

Run the production build and fix every error before deploying. A site that runs in dev but fails `next build` will fail on Vercel too.

### Step 6 — Go live

Follow `references/deployment.md` phase by phase. **Walk one phase at a time and confirm it worked before moving on.** Dumping all ten phases at once is how students get lost. Each phase has a verification step — actually run it.

### Step 7 — Handover

If the site is for a client, produce the handover document from Phase 9.

## Hard rules

- **Never invent business facts.** Opening hours, credentials, license numbers, prices, years in business, patient/customer counts — if the user has not given it to you, use a clearly marked placeholder like `[[CLINIC HOURS — CONFIRM]]` and list every placeholder at the end so nothing ships unfilled.
- **Never write fake testimonials or reviews.** Inventing a named person praising a real business is a genuine legal problem, not just a style issue. Build the testimonial component, leave it empty, and tell the user to supply real ones.
- **Never claim something is live until the user confirms the URL loads.** You cannot see their browser. Ask.
- **Secrets never get committed.** API keys go in `.env.local`, which must be in `.gitignore`. Set the real values in the Vercel dashboard.
- **Placeholder images must look like placeholders** so they cannot be mistaken for finished work.

## References

- `references/deployment.md` — the full go-live roadmap, Phase 0 to Phase 9
- `references/integrations.md` — working code for the contact form, Resend, and Cal.com booking
