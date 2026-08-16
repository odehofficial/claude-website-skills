---
name: ecommerce-website
description: Build a small online store with Stripe Checkout for a business selling a limited product range — collects the brief, applies e-commerce conversion and consumer-law rules, then hands off to the website-launch skill to build and go live. Use when the user wants to sell products online, mentions a shop, cart, checkout, or payments. Read the scope warning first — larger catalogues belong on Shopify, not a custom build.
---

# E-commerce Website

Collects the brief for a small online store, then hands off to `website-launch` for the build and deployment.

## Scope warning — read before agreeing to build

A custom store is the wrong choice for most clients, and being honest about that early saves everyone a painful project.

**A custom Next.js + Stripe build fits when:** the catalogue is small (roughly under 30 products), variants are simple, inventory does not need tight tracking, and the client wants full design control.

**Use Shopify instead when any of these are true:** a large or growing catalogue, complex variants, real inventory management, multiple sales channels, a non-technical client who needs to manage products daily, or subscriptions and complex tax and shipping rules.

Rebuilding Shopify's back office in a custom project is a large, expensive, and mostly invisible amount of work. If the client needs it, say so plainly and recommend Shopify — a well-configured Shopify store will serve them better than a hand-built one, and the student keeps the relationship by being honest about it.

If they proceed with a custom build, be explicit that **product management means editing code or adding a CMS**, and that inventory will not track itself.

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

1. Confirm the scope decision above.
2. Interview with the questions below.
3. Confirm the brief back in a short summary.
4. Invoke `website-launch` and follow its workflow from Step 2 (design system) onward.

## Intake questions

**Required before building:**

1. Business name, country, and where they ship to
2. What they sell, and roughly how many products
3. Do products have variants (size, colour) and do they need stock tracking?
4. Language(s) and currency — if Arabic, full RTL layout
5. Price points
6. **Payment** — Stripe is the default; confirm it is available in their country, as it is not everywhere
7. Shipping — flat rate, by weight, by zone, or free over a threshold?
8. Returns and refunds policy — required, not optional
9. Product photography — do they have it?
10. Business contact details and registered address
11. Domain — owned or needs buying?

**Ask if relevant:**

12. Discount codes or promotions
13. Local delivery or pickup
14. Cash on delivery — still dominant in several markets and Stripe does not cover it
15. Whether they need customer accounts, or guest checkout is enough

## What actually converts

1. **Photography is the product online.** The customer cannot touch it. Multiple angles, scale reference, and detail shots. This is the highest-leverage investment in the entire build.
2. **Guest checkout.** Forcing account creation is one of the largest measured causes of cart abandonment. Offer accounts; never require them.
3. **Total cost, early.** Unexpected shipping cost at the final step is the single biggest reason carts are abandoned. Show shipping cost or a free-shipping threshold on the product page, not at checkout.
4. **Trust signals at the payment step.** Returns policy, secure payment indication, and real contact details visible near the buy button. A store with no phone number and no address feels like a scam.
5. **Fewest possible checkout steps.** Every field removed lifts completion. Stripe Checkout handles this well — prefer it over a hand-built payment form, which also removes most of your compliance burden.
6. **Mobile checkout must be flawless.** Most traffic, and the place where hand-built stores break most often. Test a real purchase on a real phone before launch.

## Page structure

**Home** — hero · featured products · categories · trust bar (shipping, returns, secure payment) · social proof · newsletter signup

**Other pages** — Product listing with filters · Product detail (gallery, description, variants, price, shipping info, add to cart) · Cart · Checkout (Stripe) · Order confirmation · About · Contact · Shipping policy · Returns and refunds · Terms · Privacy policy

## Legal requirements — these are not optional

Consumer protection law applies to online sales in essentially every jurisdiction. Confirm specifics locally, but expect to need all of the following:

- **Business identity** — legal trading name, registered address, and contact details, genuinely reachable
- **Full price transparency** including tax and shipping before the customer commits
- **A returns and refunds policy.** Many jurisdictions grant a statutory cooling-off period for online purchases regardless of what the policy says — the policy cannot remove rights the law grants
- **Terms and conditions** covering the sale
- **A privacy policy** covering customer data, mandatory under GDPR and equivalent regimes
- **Cookie consent** if any non-essential tracking is used
- **Order confirmation email** with a full order summary

**Never handle raw card details.** Use Stripe Checkout or Stripe Elements so card data never touches the site — this is what keeps the client out of PCI compliance scope. A hand-built card form is both a security risk and a compliance liability.

**Never invent reviews**, and never display fake urgency ("3 people viewing", fake countdowns). Both are actively illegal in a growing number of jurisdictions, not merely distasteful.

**Never invent product details, dimensions, materials, or origin.** Inaccurate product descriptions are directly actionable under consumer law.

## Design direction

Products first, chrome last. Clean grids, large imagery, restrained interface.

Match the price point: premium goods need whitespace, restraint, and elegant type; value retailers need density, visible discounts, and urgency. The mismatch is obvious to customers and costs sales.

Performance is revenue here more than in any other category — every additional second of load time measurably reduces completed purchases. Insist on optimised images, lazy loading, and a fast checkout path.
