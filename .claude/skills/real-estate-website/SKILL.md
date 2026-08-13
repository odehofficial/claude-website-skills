---
name: real-estate-website
description: Build a website for a real estate agency, property broker, individual agent, or property developer — collects the brief, applies property-industry conversion and listing-accuracy rules, then hands off to the website-launch skill to build and go live. Use when the user wants a website for any property business, or mentions listings, property search, valuations, or agent profiles.
---

# Real Estate Website

Collects the brief for a property business, then hands off to `website-launch` for the build and deployment.

**Read the listings section before promising anything.** How listings get onto the site is the single biggest decision in this category and it determines the entire build.

## How to run this

1. Interview the user with the questions below — use `AskUserQuestion` for the discrete choices.
2. Confirm the brief back in a short summary.
3. Invoke `website-launch` and follow its workflow from Step 2 (design system) onward.

## Intake questions

**Required before building:**

1. Agency or agent name, city, country, office address
2. Type — sales, rentals, commercial, off-plan/developer, property management
3. Language(s) — if Arabic, full RTL layout
4. **How listings will be managed** — see the section below, ask this early
5. Roughly how many active listings
6. Agents — names, photos, specialisms, contact details
7. Phone, WhatsApp, email
8. Licence or registration number (usually legally required)
9. Domain — owned or needs buying?

**Ask if relevant:**

10. Areas or neighbourhoods they specialise in
11. Whether they want a valuation request tool as a lead magnet
12. Portal integrations they already use (Bayut, Property Finder, Rightmove, Zillow)
13. Landlord services, property management, mortgage referrals

## The listings decision — settle this first

Listings change constantly. A site with stale or sold properties destroys credibility faster than anything else in this category. There are three honest options, and the client must pick one:

**A. Hard-coded listings.** Simplest to build. Only viable for a very small, slow-moving portfolio, and someone must edit code to update it. For most agencies this fails within weeks — be explicit about that rather than letting them discover it.

**B. A CMS the client can edit.** Listings live in something like Sanity or Payload, and staff add properties through an admin panel with no developer involvement. This is the right answer for most agencies and adds meaningful scope beyond a standard build — say so when quoting.

**C. Feed from an existing portal or CRM.** If they already manage listings in a CRM or portal, syncing from it is the only approach that stays accurate long-term. Feasibility depends entirely on whether that system offers an API or export — verify before promising it.

**Do not build option A while implying it behaves like option B.** Tell the user plainly which one they are getting and what maintaining it requires.

## What actually converts for a real estate site

1. **Search and filter that actually works.** Location, price range, bedrooms, and property type at minimum. Buyers filter immediately; a site that makes them scroll a flat list loses them.
2. **Photography decides everything.** Listings with poor photos do not get enquiries regardless of the property. Push for professional photography and floor plans.
3. **Enquiry on every listing** — a form plus a WhatsApp button, right beside the property, not on a separate contact page.
4. **The valuation lead magnet.** "What is my property worth?" is the highest-intent action a seller takes online and it generates the most valuable leads in this business. If they take listings, build it.
5. **Area guides win the long-tail SEO.** "Living in [neighbourhood]" content brings buyers earlier in their search than listing pages do, and competitors rarely bother.

## Page structure

**Home** — hero with property search · featured listings · services (buy, sell, rent, manage) · area guides · why this agency · meet the team · valuation CTA · contact

**Other pages** — Listings with filters · Individual property pages (gallery, floor plan, map, features, enquiry form, agent contact) · Area guides · Agent profiles · Valuation request · About · Contact · Sell/list with us

## Industry rules

- **Listing accuracy is a legal matter**, not a quality issue. Misrepresenting size, price, condition, or features exposes the agency to real liability. Never generate, embellish, or infer property details — use only what the client supplies.
- **Sold and let properties must be marked or removed promptly.** Bait listings that stay up to harvest enquiries are prohibited in many jurisdictions.
- **Fair housing / anti-discrimination rules** (US and elsewhere) restrict language about who a property suits. Describe the property, never the ideal occupant — no "perfect for young professionals", no references to family status, religion, or nationality.
- **Display the agency licence or registration number** where required, and the agent's individual registration where that applies.
- **Price display rules vary** — some markets require currency, fees, and commission disclosure. Confirm locally.
- **Never invent listings, prices, or testimonials.** Placeholder properties must be obviously fictional so they cannot be mistaken for real inventory.

## Design direction

Let the properties dominate. Large imagery, clean grids, minimal decoration. The site is a frame around the photography.

Match the market tier honestly. Luxury property needs restraint, whitespace, and elegant serif type; a high-volume rental agency needs density, speed, and obvious filtering. Applying luxury design to a budget rental portfolio makes it look slow and pretentious; the reverse makes premium property look cheap.

Performance matters more here than in most categories, because listing pages carry many large images. Insist on proper image optimisation and lazy loading — a slow gallery loses the enquiry.
