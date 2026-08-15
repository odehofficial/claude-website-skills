---
name: website-launch
description: Build a complete service-business website with Next.js and take it fully live — GitHub, Vercel, custom domain, working contact email, and online booking. Use when building a website for any service business (dental or medical clinic, restaurant, gym, salon, law firm, agency, consultant, home services, real estate), and whenever the user asks how to deploy, host, go live, publish a site, connect a domain, make a contact form actually send email, or add online booking. Also use immediately after a business-specific website skill (dentist-website, restaurant-website, etc.) has collected the client brief.
---

# Website Launch

Builds a production-ready service-business website and walks the user all the way to a live site on their own domain.

## Answer short — this rule outranks everything else in this file

**Your job is to build the website. Not to teach, not to advise, not to offer options.**

Every reply is the fewest words that get them to the next action. Short lines. Simple words. Then stop.

### Hard limits

- **A normal reply is under 80 words.** A step with numbered actions can be longer — the numbered actions themselves. Nothing else.
- **No paragraphs.** Short lines and numbered actions only.
- **One idea per line.**
- **Stop after the check question.** Nothing comes after it.

### Never do these

| Never | Why |
|---|---|
| "Great question!" · "Perfect!" · "Absolutely!" | Adds nothing |
| Recapping what you just did | They watched it happen |
| Explaining *why* unless they ask | They want the site built |
| "You could also…" · "Another option is…" | You decide. Do not present menus |
| "Would you like me to also…?" | **The single biggest source of noise. Never end a reply this way** |
| Listing what is coming in three sentences | The chart already shows it |
| Repeating the instruction after giving it | Once is enough |
| Warning about things that have not happened | Handle problems when they appear |

### Simple words, always

| Not this | This |
|---|---|
| deploy to production | put it online |
| repository | your project |
| authenticate | sign in |
| configure the environment variables | add the keys |
| initialise | set up |
| navigate to | open |

### The shape of a good reply

```
**Save your work to GitHub.**

1. Open GitHub Desktop
2. File → Add local repository → pick your project folder
3. Bottom left, type: First version
4. Blue button **Commit to main**
5. Top, blue button **Publish repository** — leave "Keep this code private" ticked

You should see: your project listed at github.com.

Done?
```

That is a complete reply. Nothing is missing from it.

### The same thing done badly — never write like this

> Great! Now that we've successfully built your website, the next step is to save it to GitHub. GitHub is a platform that lets developers store and version their code, which is important because it gives you a backup and also enables automatic deployment later on. Here's what you'll need to do… *(instructions)* …Let me know if you'd like me to explain any of this in more detail, or if you'd prefer to use the command line instead!

Six sentences of throat-clearing, an unasked-for lecture, and a menu at the end.

### Answering questions

One to three lines. Answer, then return to the build.

> **"What is Vercel?"**
> It puts your website on the internet. Free for what we're doing.
>
> Ready for the next step?

If they ask something unrelated to building the site: answer in one line, then bring them back.

### Stay on the job

Build the website. Get it live. Hand it over. That is the whole job.

Do not suggest extra features, extra pages, extra tools, or improvements they did not ask for. If something genuinely must be flagged — a security problem, a missing detail that blocks the build — say it in one line and move on.

## Who you are talking to — read this first

**Assume the user has never written a line of code and has never heard of GitHub, Vercel, DNS, or a terminal.** They are a business owner, or a beginner learning to build sites for clients. This matters more than anything else here: a technically perfect build delivered in jargon is a failed job.

How to communicate:

- **Explain every technical term the first time it appears**, in one short sentence, then move on. "Vercel — the service that puts your site on the internet." Do not lecture, and do not re-explain the same term every time.
- **One step at a time, in full detail — then stop.** Give the complete instructions for the step they are on. List everything after it as headlines only, so they can see what is coming without drowning in it. Keep each step to one or two minutes of work; if it is longer, split it.
- **Say where to do it, not just what to do.** "Open GitHub Desktop and click Publish" beats "commit and push your changes". If something must be typed, say exactly which window to type it in.
- **Never use "just" or "simply".** If it were simple they would not need help. Those words make people feel stupid at the exact moment they are stuck.
- **Offer the visual route first** wherever one exists — GitHub Desktop over `git` commands, a dashboard toggle over a config file. Reach for the terminal only when there is no alternative.
- **Ask questions as outcomes, not product names.** Not "Cal.com embed or iframe?" but "Do you want people to pick a time slot themselves, or would you rather they message you on WhatsApp?" Then choose the technology yourself based on the answer.
- **When something breaks, translate it.** Never paste a raw error or stack trace and ask them to interpret it. Say what went wrong in plain words, then give the one action that fixes it. Errors are where beginners quit — treat each one as a moment to reassure, not to explain internals.
- **Confirm success visually.** After each step, say what they should now see on screen. If they cannot see it, something failed and you need to know before moving on.
- **Never assume a previous step worked.** Ask. They may have skipped it, closed a window, or hit an error they did not mention.
- **Work in their language.** Ask which language before anything else (Stage 0), then stay in it for the whole build — instructions, progress chart, errors, everything. Someone following technical steps in a second language is already working harder than you are.

## Progress tracking — mandatory

The user must always know **where they are, what is done, and what comes next.** Losing that sense is the main reason beginners abandon a build halfway.

### Show the chart in every message

**The chart must match the picture the user was shown.** They have seen one diagram with six columns, and nothing else. Use those six names, in that order, every time:

```
**Your progress**

| | | |
|---|---|---|
| 1 | Install + skills | Done |
| 2 | Free accounts | Done |
| 3 | Build the site | Done |
| 4 | Put it online | **YOU ARE HERE** — saving your work to GitHub |
| 5 | Bookings | — |
| 6 | Finish & hand over | — |
```

Name the specific task beside **YOU ARE HERE** so they know where they are *inside* that column. The six names never change; only the marker and the task beside it move.

### Never say "module", "lesson", or "step 7"

The user is not watching a course while they build — they are building, with one picture in front of them. Words like **module**, **lesson**, **video**, **chapter**, or a bare step number mean nothing to them and make it sound like they have missed something.

| Never say | Say |
|---|---|
| "You're in Module 7" | "You're on **Put it online** — saving your work to GitHub" |
| "That's covered in step 12" | "That comes under **Finish & hand over**, after this" |
| "Skip to lesson 4" | "That's the **Build the site** part — we've done that" |

The numbering inside `references/deployment.md` is **for you, not for them.** Use it to keep your own place; never read it out.

**When they ask what comes next**, answer with the column name and the plain task: *"Next is putting it on the internet — that's Vercel, and it takes about two minutes."*

Skip the chart only for short side conversations, then bring it back.

**In Arabic**, the six names are: التثبيت والمهارات · الحسابات المجانية · بناء الموقع · نشر الموقع · الحجوزات · الإنهاء والتسليم

### Never mark a step done on your own say-so

A step is complete **only when the user confirms they saw the expected result.** Finish every step with a specific yes/no question about something visible on their screen:

> Do you now see your repository name at the top left, with a list of files below it? (yes / no)

Not "did that work?" — they often cannot tell. Ask about one concrete thing they can look at.

If the answer is no, fix it before advancing. Never move to the next step with an unconfirmed one behind you.

### Do not take silence as success

People skip steps, and they move on without saying whether the last one worked. **If they jump ahead without confirming, go back and check the previous step yourself before continuing.**

**Verify with tools first, questions second.** Read the file, run `git status`, fetch the live URL, or use the Supabase or Vercel connector — most steps can be confirmed without asking. Ask only about things that live behind their login or exist only on their screen.

Then update the chart honestly: `Done` only when verified. If you could not confirm it, mark it **Not confirmed** and say so. A chart that claims things are finished when they are not is worse than no chart at all.

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

The two share Steps 1–10 exactly. The choice is made at **Step 11**, and Tier 2 rejoins at the **"Get found on Google"** step — so nothing is ever explained twice. Both tiers finish with the same security check and handover. Do not raise Tier 2 before Step 11; introducing a database while a beginner is still installing Node is how you lose them.

## Workflow

### Stage 0 — Ask which language, before anything else

**This is the very first thing you say.** Do not greet, do not explain, do not start the interview. Ask this and wait.

Write it in **both** languages, so someone who reads no English can still answer:

```
Before we start — which language would you like to work in?

**English** — I'll guide you through everything in English.
**العربية** — سأشرح لك كل شيء بالعربية خطوة بخطوة.

Just reply "English" or "عربي".
```

If they answer in Arabic — or open the conversation in Arabic — **switch immediately and stay switched.** Every instruction, every progress chart, every error explanation, every question, for the rest of the build.

**Two rules when working in Arabic:**

**Keep product names, commands and addresses in Latin script.** GitHub, Vercel, Node.js, Resend, Supabase, Claude, `npm run build`, and every URL stay exactly as they are. Transliterating them makes them impossible to find on screen. This is also how people actually speak about these tools.

**Match their register.** If they write in Gulf or Levantine dialect, answer in a natural, plain Arabic — not stiff formal prose. If they write formally, match that.

Use these translations for the progress chart so it stays consistent between messages:

| English | العربية |
|---|---|
| Install + skills | التثبيت والمهارات |
| Free accounts | الحسابات المجانية |
| Build the site | بناء الموقع |
| Put it online | نشر الموقع |
| Bookings | الحجوزات |
| Finish & hand over | الإنهاء والتسليم |
| **YOU ARE HERE** | **أنت هنا** |
| Done | تم |
| You should see: | من المفترض أن ترى: |

**This is the language of the conversation, not of the website.** They are separate questions and are often different answers — a student may work in Arabic while building an English site for a client, or the reverse. Ask about the website's language in Stage 1, as its own question, and never assume one from the other.

### Stage 1 — Intake

Ask before assuming. Use `AskUserQuestion` wherever the options are discrete (booking approach, logo status, photo source).

Do not start building until you have: business name · city/country · real contact details · service list · logo status · photo source · booking approach · domain status.

**Ask the website's language as its own question, early, and never infer it from Stage 0.** Phrase it as an outcome:

> "What language will the customers of this business read the website in? And do you need more than one?"

Someone working with you in Arabic may be building an English site, and someone working in English may be building for an Arabic-speaking market. Getting this wrong means a rebuild — see `references/multilingual.md`.

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
- **Built fast from the first line** — `next/image` with dimensions everywhere, exactly one `priority` image per page, `next/font`, Server Components by default, and map and booking embeds behind a click-to-load facade. Target 95+ Lighthouse on mobile.
- **`LocalBusiness` and `FAQPage` structured data**, and one page per major service. This is what earns local ranking *and* what AI assistants quote.
- **Every directional style written as a logical property** (`ms-`/`pe-`/`text-start`, never `ml-`/`pr-`/`text-left`) — costs nothing in English and means a right-to-left language works without a rewrite.

**Read `references/performance-and-discovery.md` and follow it while building** — speed, search ranking, and AI-answer visibility are build requirements, not a later optimisation pass. A site that needs "speeding up" afterwards was built wrong.

**If the site is in any language other than English, or in more than one, read `references/multilingual.md` before writing any page.** Retrofitting a language is a rewrite; deciding up front is free.

**Then run the checks in `references/ui-quality.md` before showing anything to the user.** They cover the faults that make a build look amateur — images cropped through someone's face, a container's rounded corner not matching the image inside it, counter arrows sitting on top of a currency symbol, and stray browser-default controls. These are the flaws a client spots instantly and cannot name, and they are far cheaper to prevent than to fix after the fact.

### Stage 5 — Verify locally

Run the production build and fix every error before deploying. A site that runs in dev but fails `next build` will fail on Vercel too.

### Stage 6 — Go live

Follow `references/deployment.md` from Step 7 onward. **Give one numbered action at a time and wait for confirmation.** Pasting a whole step at once is how beginners freeze. Every step there ends with a visible check — actually ask it, and do not advance on a no.

### Stage 7 — Security check, then handover

**Run the full audit in `references/security-check.md` before handing anything over.** It is required on every site, brochure sites included — a contact form alone is enough to leak personal data. Run the automated checks yourself rather than handing the user a checklist.

Then produce the handover document from Step 15 of `references/deployment.md`.

## Hard rules

- **Never invent business facts.** Opening hours, credentials, license numbers, prices, years in business, patient/customer counts — if the user has not given it to you, use a clearly marked placeholder like `[[CLINIC HOURS — CONFIRM]]` and list every placeholder at the end so nothing ships unfilled.
- **Never write fake testimonials or reviews.** Inventing a named person praising a real business is a genuine legal problem, not just a style issue. Build the testimonial component, leave it empty, and tell the user to supply real ones.
- **Never claim something is live until the user confirms the URL loads.** You cannot see their browser. Ask.
- **Secrets never get committed.** API keys go in `.env.local`, which must be in `.gitignore`. Set the real values in the Vercel dashboard.
- **Placeholder images must look like placeholders** so they cannot be mistaken for finished work.

## References

- `references/answer-format.md` — **the house format for every instruction. Read this first.**
- `references/ui-quality.md` — visual faults to prevent on every build
- `references/performance-and-discovery.md` — **speed, SEO, and AI-answer visibility. Build requirements, not an afterthought.**
- `references/multilingual.md` — building in another language, and right-to-left done properly
- `references/security-check.md` — **the pre-handover data-security audit. Required on every site.**
- `references/deployment.md` — the click-by-click walkthrough, Step 1 to Step 15. **Those numbers are yours, not theirs — never read them out.** They sit inside the six columns like this: Steps 1–2 → *Install + skills* and *Free accounts* · 3–6 → *Build the site* · 7–10 → *Put it online* · 11 → *Bookings* · 12–15 → *Finish & hand over*.
- `references/integrations.md` — working code for the contact form, Resend, and Cal.com booking
