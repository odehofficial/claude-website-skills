---
name: gym-website
description: Build a website for a gym, fitness studio, personal trainer, CrossFit box, yoga or pilates studio, or martial arts academy — collects the brief, applies fitness-industry conversion rules, then hands off to the website-launch skill to build and go live. Use when the user wants a website for any fitness or training business, or mentions memberships, class schedules, personal training, or free trials.
---

# Gym & Fitness Website

Collects the brief for a fitness business, then hands off to `website-launch` for the build and deployment.

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
2. Confirm the brief back in a short summary.
3. Invoke `website-launch` and follow its workflow from Step 2 (design system) onward.

## Intake questions

**Required before building:**

1. Business name, city, country, full address
2. Type — commercial gym, boutique studio, CrossFit, yoga/pilates, martial arts, personal training
3. Language(s) — if Arabic, full RTL layout
4. Membership tiers and prices (see pricing note below)
5. Class types and the weekly schedule
6. Trainers — names, specialisms, certifications
7. Opening hours, including staffed vs. 24-hour access
8. Phone, WhatsApp, email, social handles
9. Lead offer — free trial, day pass, first class free, intro week? (this is the primary CTA)
10. Sign-up — online, in person, or enquiry form?
11. Domain — owned or needs buying?

**Ask if relevant:**

12. Women-only hours or sections — significant in many markets
13. Facilities: parking, showers, sauna, creche, pool
14. Contract terms — minimum commitment, freeze policy, cancellation
15. Corporate memberships

## What actually converts for a gym

The decision is emotional and the barrier is intimidation. Nobody joins a gym because of the equipment list.

1. **The trial offer is the whole site.** Almost nobody buys a membership from a website cold. They come in for a free trial or day pass and convert in person. Make the trial the single dominant CTA everywhere; treat membership sign-up as secondary.
2. **Publish prices.** Hidden pricing is standard in this industry and it costs conversions. Visitors assume hidden means expensive and leave. If the client refuses to publish, push for a starting-from figure.
3. **Beat intimidation.** The largest untapped segment is beginners who feel they are not fit enough to join. Show real members of varied ages and body types, not models. A "new to the gym?" section converts a group competitors ignore entirely.
4. **The schedule must be current.** A stale class timetable is the fastest way to lose trust. If the client cannot commit to updating it, embed a live schedule from their booking system instead of hard-coding it.

## Page structure

**Home** — hero with the trial offer as the primary CTA · what's included · class types · schedule preview · meet the trainers · membership pricing · real member results and testimonials · facilities gallery · location, hours, parking · FAQ covering contracts and cancellation · closing trial CTA · sticky mobile bar with the trial CTA

**Other pages** — Classes (with descriptions and difficulty) · Timetable · Membership & pricing · Trainers · Personal training · About · Contact · Free trial sign-up

## Industry rules

- **No health or medical claims.** Never guarantee weight loss, results in a timeframe, or any health outcome. "Members often see…" is not a fix — avoid the claim entirely.
- **Before/after transformation photos** need written consent from the member and must not imply typical results. Include a disclaimer if used.
- **A health screening notice** (PAR-Q or local equivalent) belongs in the sign-up flow — tell the user to confirm local requirements.
- **Contract terms must be clear and honest.** Minimum term, notice period, and cancellation policy stated plainly. Hidden terms generate chargebacks and complaints, and in some jurisdictions unclear cancellation terms are unenforceable.
- **Never invent member testimonials or results.**

## Design direction

High energy, but match the format. A CrossFit box and a prenatal yoga studio are opposite ends of the spectrum and should not share a design language — ask which they are before choosing.

Common failure: aggressive dark-and-neon design that appeals to existing gym enthusiasts and alienates the beginners who represent most of the growth. Unless the client is explicitly targeting serious lifters, aim more welcoming than intense.

Real photos of the actual space and actual members outperform stock fitness imagery by a wide margin. Stock photos of models with visible abs signal "this place is not for you" to exactly the person you are trying to convert.
