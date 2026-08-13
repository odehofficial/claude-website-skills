# Go-Live Roadmap

*Last reviewed: August 2026. Vercel, Resend, Cal.com and domain registrars redesign their dashboards regularly. This guide describes **what to achieve and where to look**, not exact click paths, so it stays usable. If a screen does not match, look for the same concept under a renamed menu.*

Walk the user through **one phase at a time**. Confirm each verification step before moving on.

---

## Phase 0 — Accounts and tooling

**Install locally:**
- **Node.js** (version 18 or newer) — required to build anything. Verify: `node --version`
- **Git** — required to push code. Verify: `git --version`

**Free accounts to create** (all have workable free tiers for a small business site):
- **GitHub** — stores the code
- **Vercel** — hosts the site. Sign up *with GitHub* so the two are already connected
- **Resend** — sends contact form email
- **Cal.com** — handles booking (skip if using WhatsApp or phone only)

**Costs money:** the domain, roughly $10–15/year at Namecheap, Cloudflare, or Porkbun. Everything else on this list has a free tier that comfortably covers a small service business. Check current limits on each provider's pricing page rather than trusting a number in a course — they change.

> Verify: `node --version` and `git --version` both print a version.

---

## Phase 1 — Build and review locally

```bash
npm run dev
```

Open the local URL. Review on a narrow window first, then desktop.

```bash
npm run build
```

This must pass with zero errors. A dev server tolerates mistakes that a production build rejects — and Vercel runs the production build.

> Verify: `npm run build` completes successfully.

---

## Phase 2 — Push to GitHub

Confirm secrets are ignored before the first commit:

```bash
cat .gitignore
```

`.env.local` and `node_modules` must be listed. If `.env.local` is missing from it, add it now — a committed API key is public the moment you push, and deleting it later does not remove it from git history.

```bash
git init
git add .
git commit -m "Initial site build"
```

Create an empty repo on GitHub (no README, no .gitignore — the project already has them), then:

```bash
git remote add origin https://github.com/USERNAME/REPO.git
git branch -M main
git push -u origin main
```

> Verify: refresh the GitHub repo page and see the files. Confirm `.env.local` is **not** among them.

---

## Phase 3 — Deploy to Vercel

In Vercel, add a new project and import the GitHub repo. Vercel detects Next.js automatically — the default build settings are correct, so change nothing.

Deploy. You get a live `something.vercel.app` URL in a minute or two.

From now on **every push to `main` redeploys automatically**. This is the part students find surprising and it is worth pointing out: there is no "upload" step ever again.

If the build fails here but passed locally, the cause is almost always a missing environment variable or a case-sensitive import path — Vercel builds on Linux, where `Header.tsx` and `header.tsx` are different files, while Windows and macOS treat them as the same.

> Verify: open the `.vercel.app` URL on a phone. The site loads.

---

## Phase 4 — Custom domain

Buy the domain at any registrar. Namecheap, Cloudflare, and Porkbun are all fine; avoid registrars that bundle expensive "privacy" add-ons.

In the Vercel project, add the domain under the project's Domains settings. Vercel then shows the exact DNS records to create.

**Use the records Vercel shows you.** Do not copy IP addresses from a tutorial, including this one — they change, and a stale A record means a dead site.

Add those records at the registrar's DNS panel. Propagation is usually minutes, occasionally up to 48 hours. HTTPS is issued automatically once DNS resolves; no certificate to buy or configure.

Add both `example.com` and `www.example.com`, and let Vercel redirect one to the other so the site has a single canonical address.

> Verify: `https://yourdomain.com` loads with a padlock in the address bar.

---

## Phase 5 — Contact form email (Resend)

Code for this is in `references/integrations.md`.

1. In Resend, add and verify the sending domain. Verification means adding DNS records at the registrar, same place as Phase 4. Resend provides a test sender for development, but sending *from your own domain* to arbitrary recipients requires this verification — plan for it rather than discovering it at launch.
2. Create an API key.
3. Put it in `.env.local` for local development.
4. Add the same variables in the Vercel project's Environment Variables settings.
5. **Redeploy.** Environment variables are read at build time; adding one does not affect the already-built site until it rebuilds. This trips up nearly everyone.

Email deliverability note worth teaching: mail sent from a brand-new domain often lands in spam for the first few weeks. Domain verification (SPF and DKIM records) is what fixes this. Tell the client to check spam initially.

> Verify: submit the form on the **live** site and confirm the email arrives. Testing only on localhost proves nothing about production.

---

## Phase 6 — Booking (Cal.com)

Skip if the business chose WhatsApp or phone only.

1. Create the Cal.com account and set the real availability — working hours, days off, buffer between appointments, and how far ahead people may book.
2. Create an event type per service if durations differ. A cleaning and an implant consultation are not the same length.
3. Turn on confirmation and reminder emails. Reminders are the single biggest lever on no-shows.
4. Embed it using the snippet Cal.com generates, or link out to the booking page. Embedding keeps people on the site; linking is more robust. Either is defensible.

> Verify: make a real test booking end to end. Confirm it appears in the calendar and that the confirmation email arrives.

---

## Phase 7 — SEO and analytics

- Every page has a unique `<title>` and meta description
- An Open Graph image, so shared links show a preview instead of a bare URL
- `sitemap.xml` and `robots.txt` — Next.js generates both from `app/sitemap.ts` and `app/robots.ts`
- Vercel Analytics — one toggle in the dashboard, no cookie banner needed
- Google Search Console — verify the domain and submit the sitemap
- **Google Business Profile** — for a local business this outranks almost everything else on the list. A clinic gets far more traffic from Maps than from organic search. Do not skip it.
- Local business structured data (JSON-LD) with the real address, hours, and phone

> Verify: search `site:yourdomain.com` in Google after a few days and see pages indexed.

---

## Phase 8 — Pre-launch checklist

Run through this on the live domain, not localhost:

- [ ] Every nav link goes somewhere real; no dead links
- [ ] Contact form delivers, and the success message is clear
- [ ] Phone numbers are tap-to-call on mobile (`tel:` links)
- [ ] WhatsApp link opens the right number, if used
- [ ] Map shows the correct location
- [ ] Opening hours match reality
- [ ] Booking flow completes
- [ ] Site works on a real phone, not just a resized browser window
- [ ] Lighthouse: Performance and Accessibility both 90+ (Chrome DevTools)
- [ ] A custom 404 page exists
- [ ] Favicon set
- [ ] No `[[PLACEHOLDER]]` text anywhere — search the codebase for it
- [ ] No fake testimonials, fake statistics, or invented credentials
- [ ] Privacy notice present on any form collecting personal data

---

## Phase 9 — Client handover

If the site was built for a client, deliver a short document containing:

**Accounts and ownership** — which accounts exist, and who owns them. Best practice: the *client* owns the domain and Vercel account, and the builder is added as a collaborator. When the domain sits in the builder's personal account, the eventual separation is painful for both sides.

**Credentials** — via a password manager share, not email or WhatsApp.

**How to change content** — plain-language instructions for the things they will actually want to change: hours, prices, photos, a new service.

**Recurring costs** — the domain renewal date, and any paid tier. Domains that lapse because nobody knew who was paying are a common and avoidable disaster.

**What to do if something breaks** — who to contact, and whether ongoing support is included. Put this in writing before it comes up.

**Suggest an ongoing arrangement.** Content updates, monitoring, and small changes are a legitimate recurring service and the reason a build becomes a client relationship rather than a one-off.
