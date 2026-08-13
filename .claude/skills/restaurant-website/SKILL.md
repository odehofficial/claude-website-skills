---
name: restaurant-website
description: Build a website for a restaurant, cafe, bakery, coffee shop, bar, food truck, or catering business — collects the brief, applies hospitality conversion rules, then hands off to the website-launch skill to build and go live. Use when the user wants a website for any food or drink business, or mentions menus, reservations, table booking, opening hours, or delivery links.
---

# Restaurant Website

Collects the brief for a food or drink business, then hands off to `website-launch` for the build and deployment.

## How to run this

1. Interview the user with the questions below — use `AskUserQuestion` for the discrete choices.
2. Confirm the brief back in a short summary.
3. Invoke `website-launch` and follow its workflow from Step 2 (design system) onward.

## Intake questions

**Required before building:**

1. Restaurant name, city, country, and full address
2. Cuisine and format — fine dining, casual, cafe, takeaway, food truck, bakery
3. Language(s) — if Arabic, full RTL layout
4. The menu itself, or a link to it
5. Opening hours per day, including kitchen close time if different
6. Phone, WhatsApp, email, and social handles
7. Reservations — accepting them? Via what: a booking platform, phone, WhatsApp, or walk-in only?
8. Delivery — which platforms (Talabat, Deliveroo, Uber Eats, own delivery)?
9. Photos — real food photography, or placeholders? (see warning below)
10. Domain — owned or needs buying?

**Ask if relevant:**

11. Alcohol served — affects imagery, tone, and legal notices in some markets
12. Private events, catering, or large group bookings
13. Parking, outdoor seating, shisha, live music, family section
14. Dietary range — vegan, vegetarian, gluten-free, halal

## What actually converts for a restaurant

Visitors arrive with one of three intents, and almost nothing else matters:

1. **"What's on the menu and what does it cost?"** The menu is the single most-visited page on virtually every restaurant site. It should be one tap from anywhere.
2. **"Are you open right now, and where are you?"** Hours and address must be visible without scrolling on mobile.
3. **"Can I book / order?"** One tap.

Everything else — the chef's story, the interior design philosophy — is secondary. Build for those three first.

### The menu must be real HTML, never a PDF

This is the most common and most damaging mistake on restaurant websites. A PDF menu:

- Is nearly unreadable on a phone, where most of your traffic is
- Cannot be indexed properly by Google, so dish names never rank in search
- Is invisible to screen readers
- Forces a download before anyone can see a price

Build the menu as structured HTML with proper headings and prices. If the client insists on a PDF, offer it as an *extra* download beside the HTML version, never instead of it.

### Photography carries this category

Food photography converts better than any copy you can write, and bad photos actively repel. If the client has no good photos, say so plainly and recommend a photographer before launch — this is one of the few cases where a site should wait. Generic stock images of unrelated food are worse than no images, because visitors recognise them as fake.

### Google Business Profile beats the website for discovery

Most people find a restaurant through Maps, not organic search. The site's job is to convert someone already looking. Step 12 of the deployment walkthrough covers this; for restaurants, treat it as mandatory rather than optional, and make sure hours and phone number match the site exactly.

## Page structure

**Home** — hero with strong food imagery and Menu + Book CTAs · quick info bar (open now, address, phone) · signature dishes · menu preview linking to the full menu · about/story · gallery · reviews · location with map and directions link · hours · closing CTA · sticky mobile bar with Call, Menu, Directions

**Other pages** — Full menu (by category) · Reservations · About · Gallery · Contact & directions · Private events / catering (if offered) · Delivery links

## Industry rules

- **Allergen information** is legally required in many jurisdictions. Include allergen labelling or at minimum a clear "please inform staff of allergies" notice. Tell the user to confirm local requirements.
- **Prices go stale.** Warn the client that menu prices on the site must be updated when they change, and consider a "prices subject to change" line.
- **Never invent dishes, prices, or reviews.** Use the real menu or a clearly marked placeholder.
- **Hours must be exact**, including Ramadan or seasonal variations where relevant, and must match Google Business Profile.
- Alcohol imagery and promotion is restricted in some markets — ask before featuring it.

## Design direction

Let the food lead. Large imagery, restrained typography, minimal chrome competing for attention.

Match the price point: a fine dining restaurant and a burger joint need genuinely different type, spacing, and colour temperature. Ask where they sit before choosing a style — an elegant serif on a casual takeaway reads as pretentious, and a playful sans on fine dining reads as cheap.

When running `ui-ux-pro-max`, pass the format and price point, not just "restaurant".
