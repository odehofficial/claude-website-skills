# Performance, SEO, and AI Search

**These are build requirements, not a later optimisation pass.** A site that needs "speeding up" afterwards was built wrong. Apply all of this while writing the pages.

Three things are deeply linked and handled together here: **how fast the site loads**, **whether Google ranks it**, and **whether AI assistants recommend it**. Speed feeds ranking; structured facts feed both ranking and AI answers.

---

# Part 1 — Speed

## Targets — aim past "good", not at it

| Measure | Google calls this good | **Build to this** |
|---|---|---|
| LCP (largest thing appears) | under 2.5s | **under 1.8s** |
| CLS (layout jumping) | under 0.1 | **under 0.05** |
| INP (tap responsiveness) | under 200ms | **under 150ms** |
| Lighthouse Performance, **mobile** | — | **95+** |
| First-load JavaScript | — | **under 150KB** |

Test on **mobile with throttling**, never desktop on office wifi. Desktop scores flatter and mislead.

## 1.1 Images — where these sites are won or lost

Client photos are the number one cause of a slow site. A phone photo is often 4–8MB; it has no business being served at that size.

**Always `next/image`. Never a bare `<img>` for content images.**

```tsx
import Image from 'next/image'

// The hero — the one image that decides your LCP score
<Image
  src="/clinic-reception.jpg"
  alt="The reception area at Smile Dental"
  width={1600}
  height={900}
  priority                    // ONLY on the hero. Never anywhere else.
  sizes="100vw"
  className="w-full h-auto"
/>

// Everything below the fold
<Image
  src="/team-sarah.jpg"
  alt="Dr Sarah Ahmed, lead dentist"
  width={600}
  height={800}
  sizes="(max-width: 768px) 100vw, 33vw"
  className="w-full h-auto"
/>
```

**Rules:**

- **`priority` goes on exactly one image per page** — the largest one visible without scrolling. Putting it on several makes the page slower, not faster.
- **Always give `width` and `height`** (or `fill` inside an `aspect-ratio` container). This reserves the space and is what keeps CLS at zero.
- **Always set `sizes`.** Without it the browser downloads a desktop-sized image onto a phone.
- **Resize source files before they enter the project.** Nothing above **2000px** on the long edge, nothing above **300KB**. Do this for the user — do not commit a 6MB photo and rely on the framework.
- Next.js serves AVIF and WebP automatically. Do not hand-convert.
- **Never a background-image in CSS for a meaningful photo.** It cannot be optimised, prioritised, or given alt text.

## 1.2 Fonts

```tsx
import { Inter } from 'next/font/google'

const inter = Inter({
  subsets: ['latin'],
  display: 'swap',
  variable: '--font-sans',
})
```

- **`next/font` only.** Never a `<link>` to Google Fonts — that is a render-blocking request to another server.
- **Two families maximum.** Each one is another download.
- `display: 'swap'` so text is readable immediately.
- Only the subsets actually used. For Arabic see `multilingual.md`.

## 1.3 Third-party embeds — the biggest hidden cost

A Cal.com embed or a Google Map can pull in **more JavaScript than the entire rest of the site**, and it loads before the visitor has shown any interest in it.

**Never load an embed on page load. Show a lightweight placeholder and load the real thing on click.**

### Map facade

```tsx
'use client'
import { useState } from 'react'

export function MapFacade({ query }: { query: string }) {
  const [loaded, setLoaded] = useState(false)

  if (!loaded) {
    return (
      <button
        onClick={() => setLoaded(true)}
        className="relative w-full aspect-[16/9] rounded-2xl overflow-hidden bg-muted"
        aria-label="Load the map"
      >
        <img
          src="/map-preview.jpg"     // a static screenshot, under 100KB
          alt=""
          className="w-full h-full object-cover"
        />
        <span className="absolute inset-0 grid place-items-center">
          <span className="rounded-full bg-white px-5 py-3 font-medium shadow-lg">
            Show map
          </span>
        </span>
      </button>
    )
  }

  return (
    <iframe
      src={`https://www.google.com/maps?q=${encodeURIComponent(query)}&output=embed`}
      className="w-full aspect-[16/9] rounded-2xl border-0"
      loading="lazy"
      title="Location map"
    />
  )
}
```

Always put the **address as real text** next to the map, plus a "Get directions" link. Most people want the address, not the map — and text costs nothing.

### Booking facade

Same pattern for Cal.com: a styled **"Book an appointment"** button that mounts the embed on click. The visitor who never books never pays for it.

### Analytics

```tsx
import { Analytics } from '@vercel/analytics/react'   // no cookie banner, tiny
```

If the client insists on Google Tag Manager, load it with `next/script` and `strategy="lazyOnload"`, and tell them plainly what it costs in speed.

## 1.4 JavaScript

- **Server Components by default.** Add `"use client"` only to the smallest component that genuinely needs interactivity — a form, an accordion, a slider. Never to a whole page.
- **No component library for one button.** These sites need very little JavaScript.
- **No carousel library.** A CSS scroll-snap row does the same job for nothing.
- Check what you shipped: `npm run build` prints First Load JS per route. Anything over **150KB** needs justifying.

## 1.5 Nothing may move as the page loads

Layout shift is the most irritating failure on a phone and the easiest to prevent.

- Every image has dimensions or an `aspect-ratio` box
- Every embed sits in a container with a reserved height
- Banners and cookie notices never push content down — overlay them
- Fonts use `swap` with a matched fallback so text does not jump when the webfont arrives

## 1.6 Render statically

These pages do not change per visitor. Let them be generated once at build time — no `cache: 'no-store'`, no unnecessary `dynamic = 'force-dynamic'`. Static pages are served from the edge and are close to instant.

## 1.7 Verify — do this, do not assume

```bash
npm run build          # read the First Load JS column
```

Then on the **live** URL:

1. **https://pagespeed.web.dev** — enter the address, read the **Mobile** tab.
2. Anything under 95 on Performance: read the "Opportunities" list and fix the top item first. It is almost always an image.

Show the user the score. It is a number they can put in front of a client.

---

# Part 2 — Being found on Google

## 2.1 Every page

- One `<h1>`, and it says what the page is about
- A unique `<title>` under ~60 characters
- A unique meta description around 150 characters that reads like a sentence, not keywords
- A canonical URL
- An Open Graph image so shared links show a preview
- Real semantic HTML — `<header>`, `<nav>`, `<main>`, `<footer>`, proper heading order

## 2.2 One page per service — this is where local ranking comes from

"Dental implants Dubai" is the search that brings a high-value patient. It cannot rank against a combined services page with an anchor link. Each significant service gets its own page with real content: what it is, who it suits, what happens, roughly what it costs, and a booking call to action.

The business skills already specify this. Build it that way.

## 2.3 Site plumbing

`app/sitemap.ts` and `app/robots.ts` — Next.js generates both. Submit the sitemap in Search Console (Step 12 of the walkthrough).

## 2.4 Consistency of the basics

The business name, address and phone number must be **byte-identical** on the site, in the structured data, and on the Google Business Profile. Inconsistency between them is one of the most common reasons a local business ranks poorly.

---

# Part 3 — Structured data — the bridge to AI answers

This is the highest-leverage thing on this page. Structured data states the facts about the business in a form that both search engines and AI assistants read directly, rather than guessing from prose.

**Every site gets `LocalBusiness`.** Use the most specific type that fits: `Dentist`, `Restaurant`, `HealthAndBeautyBusiness`, `LegalService`, `ExerciseGym`, `RealEstateAgent`, `HomeAndConstructionBusiness`.

```tsx
// app/layout.tsx
const businessSchema = {
  '@context': 'https://schema.org',
  '@type': 'Dentist',
  '@id': 'https://smiledental.ae/#business',
  name: 'Smile Dental Clinic',
  url: 'https://smiledental.ae',
  telephone: '+971-4-555-0100',
  email: 'hello@smiledental.ae',
  image: 'https://smiledental.ae/clinic.jpg',
  priceRange: '$$',
  address: {
    '@type': 'PostalAddress',
    streetAddress: 'Unit 4, Jumeirah Road',
    addressLocality: 'Dubai',
    addressCountry: 'AE',
  },
  geo: { '@type': 'GeoCoordinates', latitude: 25.2048, longitude: 55.2708 },
  openingHoursSpecification: [
    {
      '@type': 'OpeningHoursSpecification',
      dayOfWeek: ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Saturday'],
      opens: '09:00',
      closes: '19:00',
    },
  ],
  sameAs: ['https://www.instagram.com/smiledental'],
}

<script
  type="application/ld+json"
  dangerouslySetInnerHTML={{ __html: JSON.stringify(businessSchema) }}
/>
```

**Also add:**

| Schema | Where | Why |
|---|---|---|
| `Service` | each service page | lets the service itself be understood and quoted |
| `FAQPage` | the FAQ section | **the single most quoted format in AI answers** |
| `BreadcrumbList` | every inner page | structure |
| `WebSite` | layout | site-level identity |

**Never include `aggregateRating` unless the reviews are real and verifiable.** Fake review markup is a manual-penalty offence and is exactly the kind of shortcut this course does not take.

**Verify** at `https://search.google.com/test/rich-results` before handover.

---

# Part 4 — Showing up in AI answers

When someone asks an AI assistant *"best dental clinic in Dubai"*, the answer is assembled from what the model can retrieve and quote. You cannot buy a place there, and **nobody can guarantee it** — but almost everything that helps is under your control.

## 4.1 Let the AI crawlers in — a decision, not a default

To be quoted, the site must be readable by the crawlers that feed AI answers. Many sites block them without realising.

**Ask the client explicitly**, because there is a real trade-off: allowing these crawlers means the content may also be used for training.

```ts
// app/robots.ts
export default function robots() {
  return {
    rules: [
      { userAgent: '*', allow: '/' },
      { userAgent: 'GPTBot', allow: '/' },          // ChatGPT
      { userAgent: 'OAI-SearchBot', allow: '/' },   // ChatGPT search
      { userAgent: 'ClaudeBot', allow: '/' },       // Claude
      { userAgent: 'PerplexityBot', allow: '/' },
      { userAgent: 'Google-Extended', allow: '/' }, // Gemini
    ],
    sitemap: 'https://smiledental.ae/sitemap.xml',
  }
}
```

For a local business wanting to be recommended, allowing them is almost always right. Say so, but let the client decide.

## 4.2 Write answers, not brochure copy

AI assistants quote **specific, self-contained, factual statements**. Marketing prose gives them nothing to lift.

| Gives an AI nothing | Gets quoted |
|---|---|
| "We offer world-class implant solutions tailored to you." | "A single dental implant at Smile Dental costs from AED 4,500 and takes two visits over about three months." |
| "Conveniently located in the heart of Dubai." | "Smile Dental is on Jumeirah Road, Dubai, with free parking, open 9am–7pm Saturday to Thursday." |

Every important fact — price, duration, location, hours, who it suits — should appear as a **plain, complete sentence** somewhere on the page. Not only in an icon, a table cell, or an image.

## 4.3 A real FAQ section on every site

This is the highest-return single addition. Write questions the way a person actually asks them, and answer each in **two or three complete sentences that stand on their own** without the surrounding page.

> **How much does a dental implant cost in Dubai?**
> At Smile Dental, a single implant starts from AED 4,500, including the crown. The full process takes two visits over roughly three months.

Mark it up as `FAQPage`. That combination — natural question, self-contained factual answer, structured markup — is what gets lifted into an AI response.

## 4.4 `llms.txt`

An emerging convention: a plain-text summary of the site at `/llms.txt` for AI systems.

```
# Smile Dental Clinic
> Dental clinic on Jumeirah Road, Dubai. General, cosmetic and implant
> dentistry. Open Saturday to Thursday, 9am to 7pm. +971 4 555 0100.

## Services
- [Dental implants](https://smiledental.ae/services/implants): from AED 4,500
- [Teeth whitening](https://smiledental.ae/services/whitening): from AED 900

## Contact
- Phone: +971 4 555 0100
- Address: Unit 4, Jumeirah Road, Dubai
```

**Be honest about it:** this is not an established standard and no assistant is obliged to read it. It costs ten minutes and may help. Do not sell it to a client as a guarantee.

## 4.5 What actually moves the needle most

For **local** questions, AI answers lean heavily on the same signals as local search. In rough order of impact:

1. **A complete, verified Google Business Profile** — often outweighs everything on the website
2. **Real reviews**, in volume, answered by the business
3. **The same name, address and phone number everywhere** — site, schema, Business Profile, directories
4. **Structured data** stating the facts plainly
5. **A quotable FAQ**
6. **Being crawlable** by the AI bots

Numbers 1 and 2 live off the website. Tell the client that plainly at handover — it is the honest advice, and it is what actually works.

---

# Pre-handover checks

- [ ] PageSpeed Insights **mobile** ≥ 95 on the live URL
- [ ] LCP under 1.8s, CLS under 0.05
- [ ] First Load JS under 150KB
- [ ] Exactly one `priority` image per page
- [ ] No source image over 300KB in the repo
- [ ] Map and booking embeds load on click, not on page load
- [ ] Every page has a unique title and meta description
- [ ] One page per major service
- [ ] `LocalBusiness` schema passes the Rich Results test
- [ ] `FAQPage` schema present and valid
- [ ] No `aggregateRating` unless the reviews are real
- [ ] Name, address and phone identical everywhere
- [ ] AI crawler decision made **with the client** and reflected in `robots.ts`
- [ ] Sitemap submitted in Search Console
