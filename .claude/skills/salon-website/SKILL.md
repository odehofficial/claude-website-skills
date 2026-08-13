---
name: salon-website
description: Build a website for a hair salon, barbershop, beauty salon, nail bar, spa, massage centre, or aesthetics clinic — collects the brief, applies beauty-industry conversion rules, then hands off to the website-launch skill to build and go live. Use when the user wants a website for any beauty, grooming, or wellness business, or mentions stylists, treatments, appointments, or a service price list.
---

# Salon & Spa Website

Collects the brief for a beauty, grooming, or wellness business, then hands off to `website-launch` for the build and deployment.

## How to run this

1. Interview the user with the questions below — use `AskUserQuestion` for the discrete choices.
2. Confirm the brief back in a short summary.
3. Invoke `website-launch` and follow its workflow from Step 2 (design system) onward.

## Intake questions

**Required before building:**

1. Business name, city, country, full address
2. Type — hair salon, barbershop, beauty salon, nail bar, spa, massage, aesthetics clinic
3. Language(s) — if Arabic, full RTL layout
4. Full service list **with prices** (see pricing note below)
5. Team — names, specialisms, and whether clients book a specific person
6. Opening hours, including late nights and weekends
7. Phone, WhatsApp, email, Instagram handle
8. Booking — Cal.com, an industry system (Fresha, Booksy, Treatwell), WhatsApp, or phone?
9. Photos — real work portfolio, or placeholders?
10. Domain — owned or needs buying?

**Ask if relevant:**

11. Women-only, men-only, or mixed — critical in many markets and must be unmistakable on the site
12. Home service or mobile appointments
13. Bridal and event packages — often the highest-value bookings
14. Products retailed
15. Loyalty scheme or memberships

## What actually converts for a salon

1. **Prices, visibly.** This is the number one thing visitors look for and the number one thing salons hide. "Prices on request" loses bookings to the competitor who published theirs. Push hard for at least a from-price on every service.
2. **The portfolio is the product.** Nobody books a haircut based on written descriptions. Real photos of real work done by this team decide it. If the client has an active Instagram, that *is* their portfolio — embed or link it prominently rather than building a gallery that will go stale.
3. **Booking must be immediate.** This category has the highest expectation of instant online booking of any on this list. A contact form that says "we'll get back to you" loses to a competitor with a live calendar. If they only take phone bookings, make tap-to-call enormous.
4. **Individual stylists matter.** Clients follow specific people, not salons. Stylist profiles with their own portfolios and direct booking links convert well and reduce the risk of losing a client if a stylist leaves.
5. **Mobile is overwhelming.** Traffic here skews more mobile than almost any other category, often browsed on Instagram. Design the phone layout first and treat desktop as secondary.

## Page structure

**Home** — hero with strong visual work and a Book CTA · services with prices · portfolio/Instagram feed · meet the team · why choose us · reviews · location, hours, parking · booking CTA · sticky mobile bar with Book and Call

**Other pages** — Full service menu with prices · Team and individual portfolios · Gallery · Bridal/packages (if offered) · About · Contact · Booking

## Industry rules

- **Aesthetic and cosmetic treatments** (injectables, laser, chemical peels, microblading) are regulated as medical procedures in many jurisdictions. If offered, apply the same discipline as the `dentist-website` skill: no guaranteed outcomes, practitioner qualifications displayed, consent required for before/after imagery, and confirmation against local health authority rules.
- **No guaranteed results** on any treatment — hair, skin, or body.
- **Before/after photos need client consent.** Always ask; never assume Instagram posts carry consent for website use.
- **Never invent reviews or before/after images.**
- **Patch test and allergy notices** where relevant (colour, lash extensions, chemical treatments).
- **Cancellation and deposit policy** stated clearly if they charge for no-shows — otherwise it is unenforceable and generates disputes.
- Gendered service pricing is restricted in some jurisdictions; price by service and duration rather than by gender where that applies.

## Design direction

Visual-led and aspirational. Large imagery, generous whitespace, elegant type. The site should feel like the experience of visiting.

Match the segment precisely — a traditional barbershop and a luxury day spa need opposite treatments. Barbershops go bold, dark, and masculine with heavier type; spas go soft, muted, and airy. A mismatch here reads as inauthentic faster than in almost any other category, because customers are choosing partly on aesthetic taste.

Real work photography is non-negotiable. Stock beauty imagery is instantly recognisable and undermines the exact credibility the portfolio is supposed to build.
