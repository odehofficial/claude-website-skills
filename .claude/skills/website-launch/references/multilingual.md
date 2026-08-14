# Building in Any Language

**Ask about language before anything is built.** Retrofitting a second language into a finished site means touching every component. Deciding up front costs nothing.

The intake question — in outcomes, not jargon:

> "What language will your customers read this in? And do you need more than one?"

Then build accordingly. A site that is Arabic-only is simpler than a bilingual site, and both are simpler than an afterthought.

---

# Part 1 — One language, not English

If the client wants an Arabic-only site, **build it in Arabic**. Do not build in English and translate at the end — every layout decision is different in a right-to-left language, and converting late produces a site that feels translated.

Set the document correctly at the root:

```tsx
// app/layout.tsx
<html lang="ar" dir="rtl">
```

Everything in Part 3 (right-to-left) applies.

---

# Part 2 — Two or more languages

## 2.1 Structure

Use locale-prefixed paths — clean, cacheable, and understood by every search engine:

```
smiledental.ae/          → default language
smiledental.ae/ar/       → Arabic
```

`next-intl` is the usual choice with the App Router. Keep translations in flat JSON per locale, and **load only the active locale's messages** — shipping every language to every visitor is a real and avoidable performance cost.

## 2.2 Tell search engines about each version

```tsx
export const metadata = {
  alternates: {
    canonical: 'https://smiledental.ae/services/implants',
    languages: {
      'en': 'https://smiledental.ae/services/implants',
      'ar': 'https://smiledental.ae/ar/services/implants',
      'x-default': 'https://smiledental.ae/services/implants',
    },
  },
}
```

Every page needs this, in every language. Without it the two versions compete with each other instead of reinforcing each other.

## 2.3 Set `lang` and `dir` per locale

```tsx
export default function Layout({ children, params: { locale } }) {
  const dir = locale === 'ar' ? 'rtl' : 'ltr'
  return (
    <html lang={locale} dir={dir}>
      <body>{children}</body>
    </html>
  )
}
```

`lang` matters for screen readers and search engines; `dir` is what makes the whole layout flip.

## 2.4 The language switcher

- Label each option **in its own language** — "العربية", not "Arabic"
- Link to the **same page** in the other language, never dump the user on the homepage
- Keep it visible in the header, not buried in the footer
- Never auto-redirect based on browser language — it strands people and confuses crawlers

---

# Part 3 — Right-to-left, done properly

Arabic, Hebrew, Urdu and Farsi read right to left. This is the part most sites get wrong.

## 3.1 Use logical properties — never a mirrored stylesheet

Write CSS that describes **start and end**, not left and right. Then `dir="rtl"` flips the entire layout with no duplicated styles.

| Never write | Write this |
|---|---|
| `margin-left` | `margin-inline-start` |
| `padding-right` | `padding-inline-end` |
| `text-align: left` | `text-align: start` |
| `left: 0` | `inset-inline-start: 0` |
| `border-left` | `border-inline-start` |

**In Tailwind, use the logical utilities:**

| Never | Use |
|---|---|
| `ml-4` | `ms-4` |
| `pr-6` | `pe-6` |
| `text-left` | `text-start` |
| `left-0` | `start-0` |
| `rounded-l-lg` | `rounded-s-lg` |

Build every component this way from the first line, in every language. It costs nothing in a left-to-right site and means the right-to-left version simply works.

## 3.2 What must flip, and what must not

**Flip:** layout, text alignment, navigation order, sidebars, breadcrumbs, progress indicators, directional arrows ("next" now points left).

**Do NOT flip:**

- **Logos and brand marks** — a mirrored logo is a broken logo
- **Phone numbers** — `+971 4 555 0100` reads left to right in any language
- **Latin brand names** — "Smile Dental" stays as written
- **Clock icons, play buttons, and other real-world symbols** — a clock does not run backwards in Arabic
- **Photographs**

Wrap Latin text and numbers inside Arabic paragraphs so they render correctly:

```html
<span dir="ltr">+971 4 555 0100</span>
```

## 3.3 Arabic typography — it is not Latin with different glyphs

- **Use a real Arabic font.** `IBM Plex Sans Arabic`, `Noto Sans Arabic`, or `Cairo`. A Latin font with fallback glyphs looks amateur to a native reader and is the fastest way to lose credibility.
- **More line height.** Arabic script needs roughly `1.7–1.9`, against `1.5` for Latin. Cramped Arabic is genuinely hard to read.
- **Avoid ultra-light weights.** Thin Arabic strokes disappear on screen. Regular and above.
- **Subset the font** and load it with `next/font` like any other — an unsubsetted Arabic font is a large download.
- **Numerals:** decide with the client between Western (`123`) and Eastern Arabic (`١٢٣`). Most Gulf businesses use Western for phone numbers and prices. Ask; do not assume.
- **Text runs longer or shorter after translation.** Buttons and headings that fit in one language may wrap in another. Check every layout in both.

## 3.4 Check the whole site in both directions

Before handover, walk every page in every language on a phone. Look for: text hitting the wrong edge, icons pointing the wrong way, cramped Arabic line spacing, and buttons whose labels have overflowed.

---

# Part 4 — Translation quality

**Never ship machine translation as final on a client's site.** It reads as foreign to a native speaker, and for a clinic or a law firm it damages exactly the trust the site exists to build.

Say this plainly to the user:

> "I can produce the translation, but a native speaker should read it before this goes live — especially the service names and anything legal or medical. Getting a phrase subtly wrong in the language your customers actually speak costs more than it saves."

What matters most to get right: service names, calls to action, any medical or legal wording, and the business's own description of itself.

---

# Part 5 — Speed and search in every language

**The other language is not a second-class version.** Everything in `performance-and-discovery.md` applies to each locale.

- **Structured data per locale** — the `LocalBusiness` block on the Arabic pages carries the Arabic business name and description, with the same address and phone
- **Every locale in the sitemap**, each with its `hreflang` alternates
- **Unique title and meta description per page per language** — not translated word for word, but written for how people search in that language. The Arabic phrase people actually type is often not a direct translation of the English one.
- **An FAQ in each language**, with the questions phrased the way people ask them in that language. This is what makes the site quotable by AI assistants in that language.
- **Only the active locale's messages ship** to the browser
- **Run PageSpeed Insights on both** — the Arabic pages must hit the same 95+ mobile score
- **The Google Business Profile** should carry the business name and description in the local language too

---

# Pre-handover checks

- [ ] `lang` and `dir` correct on every locale
- [ ] `hreflang` alternates on every page, including `x-default`
- [ ] Language switcher links to the same page, labelled in its own language
- [ ] No `ml-`/`pr-`/`text-left`-style directional utilities anywhere — logical properties only
- [ ] Logo, phone numbers and Latin brand names not mirrored
- [ ] A real Arabic font, line-height 1.7+, no ultra-light weights
- [ ] Every page walked in both directions on a phone
- [ ] Translation reviewed by a native speaker, or flagged to the client as pending
- [ ] Structured data, titles and descriptions written per language
- [ ] PageSpeed Insights 95+ mobile on **both** language versions
