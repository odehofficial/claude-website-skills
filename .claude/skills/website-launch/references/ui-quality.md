# UI Quality — Faults to Prevent

**Check every one of these before showing a build to the user.** They are the flaws that make an otherwise good site look amateur, and they are the ones a client notices immediately even when they cannot name what is wrong.

---

## 1. Chopped containers

**The fault:** a box whose contents look sliced — a thin strip missing along an edge, or a head cut off at the top of a photo.

There are two different causes and they need different fixes. Work out which one you are looking at.

### Cause A — the image is cropped badly

A container with a fixed height or a short aspect ratio crops whatever does not fit. With `object-fit: cover` and the default centre position, a portrait gets cut across the forehead.

```css
.card-image {
  width: 100%;
  aspect-ratio: 4 / 3;      /* tall enough for the subject */
  object-fit: cover;
  object-position: center top;  /* keep faces in frame */
  display: block;
}
```

**Rules:**
- If the image contains a **face**, use `object-position: center top` — never let a crop cut a head.
- If it contains a **product**, keep the whole product visible. Use `object-fit: contain` with a background colour rather than cropping it.
- Never use an aspect ratio shorter than `16 / 9` for images with people in them.
- Ask what the images will actually be before choosing a ratio. Portrait photos in a wide card will always crop badly.

### Cause B — a geometric sliver

A one-pixel line of background bleeding through a rounded corner, or square corners poking out of a rounded box.

```css
.card {
  border-radius: 16px;
  overflow: hidden;      /* clips the child to the rounded shape */
  isolation: isolate;    /* stops paint bleeding at the corners */
}
.card img {
  display: block;        /* not inline — see below */
  width: 100%;
}
```

**The four usual culprits:**

1. **`display: inline` on the image.** This is the most common one by far. An `<img>` is inline by default, which leaves a few pixels of gap under it for the text baseline — it reads as a chopped bottom edge. `display: block` fixes it.
2. **No `overflow: hidden` on the rounded parent.** The child's square corners sit outside the curve.
3. **A hover `transform: scale()` on a child inside a rounded parent.** Some browsers leak a hairline at the corners during the animation. `isolation: isolate` on the parent fixes it.
4. **Fractional pixel heights** from percentage heights or flex maths. A container 200.5px tall against a 200px child leaves half a pixel of background. Use `aspect-ratio` and `object-fit: cover` rather than fixed heights.

---

## 2. The container's curve must match the image's curve

**The fault:** a card with soft rounded corners containing an image with different corners. The two curves fight, and the gap between them changes width around the corner. It looks wrong even to someone who cannot say why.

**The rule — inner radius = outer radius − padding.**

| Card radius | Padding | Image radius |
|---|---|---|
| 16px | 0 | 16px (or `overflow: hidden` on the card) |
| 16px | 8px | 8px |
| 24px | 12px | 12px |
| 12px | 12px | 0 — a square image is correct here |

```css
/* Padded card */
.card   { border-radius: 24px; padding: 12px; }
.card img { border-radius: 12px; display: block; }

/* Flush card — image touches the edges */
.card   { border-radius: 24px; overflow: hidden; isolation: isolate; }
.card img { border-radius: 0; display: block; }   /* the parent does the clipping */
```

Tailwind: `rounded-3xl p-3` on the card pairs with `rounded-xl` on the image. Never `rounded-3xl` on both when the card has padding — the inner curve will look too round.

**Apply the same rule to everything nested**, not only images: buttons inside cards, inputs inside panels, avatars inside tiles.

---

## 3. Counters and number fields must never cover what is behind them

**The fault:** the up/down arrows on a number field sitting on top of the currency symbol, a unit label, or the number itself.

**Never absolutely position a control over the contents of a field.** Reserve space for it with padding.

### Turn off the browser's own spinners

They cannot be styled, they are tiny, and they overlap content:

```css
input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
input[type="number"] {
  -moz-appearance: textfield;
  appearance: textfield;
}
```

### Then build your own, with room reserved

```css
.qty {
  position: relative;
}
.qty input {
  width: 100%;
  padding-left: 2.25rem;   /* room for the $ */
  padding-right: 3rem;     /* room for the buttons — never let them overlap */
}
.qty .prefix {
  position: absolute; left: .75rem; top: 50%; transform: translateY(-50%);
  pointer-events: none;    /* clicking it still focuses the field */
}
.qty .step {
  position: absolute; right: .25rem;
  width: 2.5rem; height: 2.5rem;   /* 40px+, tappable */
}
```

**Checklist for any counter, stepper, or number field:**

- [ ] Native spinners switched off
- [ ] Padding reserves space for every control — nothing overlaps the value, a currency symbol, or a unit
- [ ] Buttons at least 40×40px, ideally 44×44
- [ ] Buttons use the site's own colours, radius, and border — not browser defaults
- [ ] Visible focus ring, and the field works with a keyboard
- [ ] It stops at sensible limits, and cannot go negative where that makes no sense

---

## 4. Nothing on the page uses default browser styling

**The fault:** a beautifully styled site with one grey system dropdown, a blue default focus outline, or spinner arrows from 2004. One unstyled control makes the whole page look unfinished.

Style, or replace, every one of these to match the design tokens:

- `<select>` dropdowns — including the arrow
- Checkboxes and radios
- Date and time pickers
- Number spinners (see above)
- File upload buttons
- Focus rings — **restyle, never remove.** `outline: none` with nothing in its place makes the site unusable by keyboard
- Scrollbars inside custom panels
- Text selection colour, on strongly branded sites

**The test:** screenshot any form and ask whether every element looks like it belongs to the same site. If one element looks like it came from the operating system, it did.

---

## 5. Before showing any build to the user

- [ ] No image has a face or product cut off by its crop
- [ ] Every `<img>` is `display: block`
- [ ] Every rounded container with a flush child has `overflow: hidden`
- [ ] Inner radius equals outer radius minus padding, everywhere
- [ ] No control overlaps text, symbols, or images behind it
- [ ] No default browser controls anywhere
- [ ] Focus rings visible and styled
- [ ] Checked at 375px wide, not only on a desktop screen
- [ ] No element sits within 16px of the screen edge on mobile
- [ ] Nothing shifts position as images finish loading

**If the user says something "looks wrong" but cannot explain it, ask for a screenshot.** It is nearly always one of the faults above, and one image settles it faster than five questions.
