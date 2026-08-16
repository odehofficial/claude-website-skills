---
name: dentist-website
description: Build a website for a dental or orthodontic clinic — collects the clinic brief, applies dental-industry conversion and compliance rules, then hands off to the website-launch skill to build and go live. Use when the user wants a website for a dentist, dental clinic, dental practice, orthodontist, oral surgeon, implant centre, or cosmetic dentistry brand. Also use for a general medical or aesthetic clinic site, adapting the service list.
---

# Dental Clinic Website

Collects the brief for a dental clinic, then hands off to `website-launch` for the build and deployment.

## STOP — questions first, always

**Your first reply is not code and not a plan. It is this, verbatim:**

```
Before we start — which language would you like to work in?

**English** — I'll guide you through everything in English.
**العربية** — سأشرح لك كل شيء بالعربية خطوة بخطوة.

Just reply "English" or "عربي".
```

**Your second reply starts the interview below — one question at a time.** Nothing gets built until every required question is answered and the design has been approved. This holds even if the user gave detail up front or said "just build it" — confirm the essentials in one short message; never skip straight to code.

## How to run this

1. Interview the user with the questions below — use `AskUserQuestion` for the discrete choices.
2. Confirm the brief back to them in a short summary.
3. Invoke `website-launch` and follow its workflow from Step 2 (design system) onward.

Do not build anything from this skill directly. This skill decides *what* the site says; `website-launch` decides *how* it is built and shipped.

## Intake questions

**Ask these first — the build cannot start without them:**

1. Clinic name, city, and country
2. Language(s) — if Arabic, the whole layout must be RTL, not a translated LTR site
3. Which services (see list below)
4. Phone, WhatsApp number, email, and full address
5. Opening hours, including weekends
6. Logo — do they have one, should I design a wordmark, or text-only for now?
7. Photos — real clinic photos, stock, or marked placeholders?
8. Booking — Cal.com embed, a form that emails the clinic, WhatsApp, or phone only?
9. Pricing — published, "from $X", or request-a-quote?
10. Domain — already owned, or do they need to buy one?

**Ask these if they matter in the market:**

11. Insurance providers accepted
12. Lead dentist's name, qualifications, and license/registration number
13. Years established, and roughly how many patients treated
14. Anything that genuinely differentiates them — same-day crowns, sedation for anxious patients, evening hours, a language they speak that competitors do not

## Services menu

General dentistry & cleanings · Cosmetic (veneers, whitening, bonding) · Orthodontics (braces, clear aligners) · Implants · Root canal · Crowns & bridges · Pediatric dentistry · Gum treatment · Emergency / same-day care

## What actually converts for a dental clinic

Patients are not comparing feature lists. They are managing **fear, cost uncertainty, and trust**. Design against those three, in this order:

1. **Fear.** A large share of adults delay dental care because they are afraid. Address it directly — gentle language, a "nervous patients" section, sedation options if offered. This single section outperforms most other content on a dental site.
2. **Cost uncertainty.** "Request a quote" loses people. Even a "from $X" range or a clear statement that consultations are free reduces the drop-off sharply.
3. **Trust.** Real photos of the actual clinic and the actual team beat stock photography by a wide margin. A visitor wants to see the room they will sit in and the face of the person treating them. Push hard for real photos.
4. **Friction.** Booking must be reachable in one tap from anywhere on the site. Sticky mobile bar with Call and Book. Most dental traffic is mobile, and a large portion is someone in pain looking for help right now — which is why emergency contact must be immediately visible, not buried on a contact page.

## Page structure

**Home** — hero with booking CTA above the fold · trust bar (years, credentials, patients treated) · services grid · nervous patients / pain-free approach · meet the team · before & after · testimonials · insurance logos · location, hours & map · FAQ · closing CTA · sticky mobile Call + Book bar

**Other pages** — Services overview plus one page per major service · About & team · Before/after gallery · Pricing & insurance · Contact + map · Booking · FAQ · Blog (optional)

Per-service pages are where the SEO actually lives. "Dental implants [city]" is the search that brings high-value patients, and it needs its own page to rank — not an anchor link on a combined services page.

## Medical compliance — enforce these

These are not stylistic preferences. Getting them wrong creates real regulatory and legal exposure, and rules vary by country — tell the user to confirm against their local dental council or health authority.

- **No guaranteed outcomes.** Never "painless", "perfect results", or "guaranteed". Use qualified language: "we focus on comfort", "designed to minimise discomfort".
- **Before/after photos need documented patient consent**, and in several jurisdictions are restricted or banned outright in advertising. Ask; do not assume. Use placeholders until the user confirms.
- **No invented testimonials.** Build the component, leave it empty, list it as pending real content.
- **No invented statistics or credentials.** If "15 years experience" was not stated by the user, it does not go on the site.
- **Display license/registration number** in the footer where the jurisdiction requires it.
- **Any form collecting health information needs a visible privacy notice** stating what is collected and why. Keep symptom detail out of forms entirely where possible — "what do you need help with?" as a service dropdown is safer than a free-text medical history.
- **Accessibility above the normal bar.** Older patients are a core segment. Base font 17–18px rather than 16, strong contrast, large tap targets, and no critical information conveyed by colour alone.

## Design direction

Clean and clinical but **warm** — never cold. The failure mode for dental sites is sterile all-blue-and-white that reinforces exactly the clinical anxiety you are trying to reduce.

When running `ui-ux-pro-max`, pass the product type as a health/wellness service rather than generic corporate, so the recommendation leans toward calm and trustworthy rather than aggressive SaaS conversion patterns.

Avoid: stock photos of disembodied teeth or extreme close-ups of open mouths. They repel the exact anxious visitor you most need to convert. Faces, smiles, and real people work better.
