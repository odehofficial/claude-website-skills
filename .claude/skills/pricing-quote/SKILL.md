---
name: pricing-quote
description: Turn a client's website needs into a priced quote and a one-page proposal, using the Website Pricing Guide. Use when the user asks what to charge, how to price a website, how much a client should pay, wants a quote or proposal, or uploads a pricing guide and describes a client. Also use when they ask about monthly maintenance pricing or a payment schedule.
---

# Pricing Quote

Turns "here is what my client needs" into a number, a breakdown, and a proposal they can send today.

**Everything in `website-launch/SKILL.md` about tone applies here** — short lines, plain words, no lecturing. Ask, calculate, hand over the quote.

## STOP — ask before calculating

**Reply 1:**

```
Before we start — which language would you like to work in?

**English** — I'll guide you through everything in English.
**العربية** — سأشرح لك كل شيء بالعربية خطوة بخطوة.

Just reply "English" or "عربي".
```

**Reply 2 onward:** the questions below, one at a time.

## Which guide to use

- **If the user uploaded or pasted a pricing guide, use theirs.** Their base prices, multipliers, and add-ons override the ones in `references/pricing-model.md`. Read it fully before asking anything.
- **If not**, use `references/pricing-model.md`.

Same calculation either way.

## The questions

Ask them **one at a time**. Skip any the user already answered.

1. **Which country is the client in?**
2. **What kind of business?** — clinic, law, real estate, salon, gym, restaurant, home services, consultant, online shop, or something else
3. **Which package fits?** — describe the three in one line each so they can choose:
   - **Starter** — brochure site with a contact form
   - **Business** — plus booking, a page per service, Google profile
   - **Premium** — plus the owner's dashboard, two languages
4. **Any extras?** — go through the add-on list, yes/no each: second language · dashboard on a Business site · you write the text · photography · extra pages · blog · menu entry (restaurants) · logo · rush
5. **Monthly plan?** — Care-Basic or Care-Plus (describe both in one line)
6. **What is the currency they pay in?** — for the final rounding

Then calculate.

## The calculation — always in this order

```
1. Package base price
2. × industry adjustment           (clinic 1.25, law 1.30, real estate 1.20 …)
3. × country multiplier             (UAE 2.2, Saudi 2.0, Jordan 1.0 …)
4. + each add-on × country multiplier
5. Round to a clean number in the client's currency
6. Monthly = Care base × country multiplier, rounded
7. Deposit = 50% of the build price
```

**Show the working.** Every line. The user needs to be able to defend the number when the client asks.

## The output — exactly this shape

```
**Quote — [business type], [city]**

Package         [Business]                              $900
Industry        [dental, +25%]                          × 1.25
Country         [Saudi Arabia]                          × 2.0
                                                        ────────
Build                                                   $2,250
+ [Second language]   $250 × 2.0                        $500
                                                        ────────
**Total build                        $2,750  →  SAR 10,500**

**Monthly (Care-Plus)   $75 × 2.0    →  SAR 550 / month**

**Payment**
Deposit to start:   SAR 5,250  (50%)
On handover:        SAR 5,250  (50%)  + first month SAR 550

Want the one-page proposal?
```

Then stop.

## The proposal — if they say yes

Fill the template in `references/proposal-template.md` with their answers. Client's name, their numbers, their currency, their language. Nothing generic left in it.

## Rules

- **Never quote hourly.** If asked, say why in one line — a faster build would mean less money — and give the package price instead.
- **Never invent a country multiplier.** If the country is not in the guide, ask the user which listed country it is most like, and say you are using that as a stand-in.
- **Never discount the middle package.** If the client says too expensive, the answer is the Starter package, not a cheaper Business.
- **The three packages are always presented together** in the proposal — even when the user has already picked one. Anchoring is the point.
- **Round.** SAR 10,500, not SAR 10,312. AED 7,500, not AED 7,346.
- **Say plainly that the numbers are opening positions** the first time you quote for a user, then not again.
- **Cash markets** — Lebanon, Syria, Iraq — quote in USD and note deposit-in-hand.

## References

- `references/pricing-model.md` — the default guide: packages, add-ons, monthly plans, country multipliers, industry adjustments, payment terms
- `references/proposal-template.md` — the one-page proposal to fill in
