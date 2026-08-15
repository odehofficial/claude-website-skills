# Copying a Design from a Video or Another Site

The user will hand you a screen recording, a video of a site they like, design token files, or another site's code — and say "make mine like this."

**The goal is one build, not three iterations.** The known failure mode: capturing the steady state of an animation and missing its opening move. It happens when a video is treated as a mood board instead of a timeline. Everything below exists to prevent it.

---

# Part 1 — You cannot watch a video. Extract frames.

MP4/MOV/WebM cannot be read directly. Turn the video into frames, then read the frames as images.

**Check for ffmpeg first; install it yourself if missing** (winget on Windows, brew on Mac — do not send the user to a website):

```bash
ffmpeg -version
```

**Get the duration:**

```bash
ffprobe -v error -show_entries format=duration -of default=noprint_wrappers=1:nokey=1 video.mp4
```

**Extract in two passes. One pass is how animations get missed.**

```bash
# Pass 1 — overview: ~12 frames spread across the whole video
ffmpeg -i video.mp4 -vf fps=12/DURATION overview-%02d.png

# Pass 2 — the entrance, dense: first 3 seconds at 8 fps
ffmpeg -i video.mp4 -t 3 -vf fps=8 entrance-%02d.png
```

**Entrances live in the first one to three seconds.** At overview sampling they fall between frames and vanish. Pass 2 is not optional.

If pass 1 shows a transition mid-video (scroll, section change, hover state), extract a dense pass around that moment too.

---

# Part 2 — Read it as a timeline, not a picture

Answer these in order, from the frames:

1. **Frame zero.** Where is every element before anything moves? Offscreen? Gathered at the bottom? Already in place? *This is the question that was missed in the real failure — the products started below the frame and rose up, and the build had them sitting in place from the start.*
2. **The entrance.** What travels, from where, to where? What order? What overlaps?
3. **The settle.** How does movement end — abrupt stop, or a long gentle landing?
4. **The loop.** What keeps moving forever after everything arrives?
5. **Interactions.** Any hover, scroll, or click behaviour shown?

**Fill a motion table for every moving element:**

| Element | Starts at | Ends at | Path | Duration | Delay | Rotation/scale |
|---|---|---|---|---|---|---|

**Get timing from frame math.** At 8 fps each frame is 125 ms. Count frames from first movement to rest: 12 frames ≈ 1.5 s. Stagger = frames between one element starting and the next.

**Get easing from spacing.** Big jumps between early frames, small ones near the end = fast start, slow landing. Even spacing = linear.

---

# Part 3 — Say what you saw, then build in the same reply

Before the code, state the timeline in a few short lines:

> What the video does:
> 1. Products start gathered low, mostly below the frame
> 2. They rise and spread outward to scattered positions, staggered
> 3. Then a slow endless drift takes over
>
> Building that now, with your products.

Do not wait for approval — build in the same reply. The spec is there so a miss is visible **immediately**, not after three rounds. Ask first only if something is genuinely ambiguous.

---

# Part 4 — Implementation rules

- **Entrance and loop go on separate nested wrappers.** Two animations on one element's transform cancel each other. Entrance on the outer element, endless drift on the inner — they compose.
- **CSS animations only.** No animation library for a hero. The 95+ speed score survives CSS; it rarely survives a 3D engine.
- **`prefers-reduced-motion`: no entrance, no drift** — elements simply at rest.
- **RTL:** horizontal offsets mirror. Verify the motion in both directions if the site is bilingual.
- **Verify by measurement when you cannot watch it live:** scrub each animation's timeline — confirm start positions match the spec, everything ends at `transform: none`, nothing collides at rest, and nothing causes horizontal scroll. At mobile width too.

---

# Part 5 — Tailor it. Never clone it.

Take from the reference: **layout, motion, spacing rhythm, type scale, the feel.**

Replace with the user's: **products, photos, colours, fonts, and every word of text.**

Never carry over the source site's photos, logos, copy, or brand name. Recreating a look is normal practice; shipping someone else's assets is not.

**If the reference's palette conflicts with the client's brand** — e.g. a strictly monochrome reference for a brand with colours — ask one question: *"Keep your brand colours inside this layout, or adopt the reference's palette fully?"* Then build. Do not silently pick.

Fonts in reference files are often commercial. If the user does not own them, use the substitutes the reference lists, or the closest free face — say which you used in one line.

---

# Part 6 — When they hand you files as well

| Given | Worth |
|---|---|
| A design doc / DESIGN.md with tokens | **The master.** Usually contains everything the other files do |
| tokens as .css / .json exports | Same data as drop-in code. Use them, expect nothing new |
| Another site's actual code | Read for structure and technique; re-express in this project's tokens — never paste |
| **The video** | **The only source of motion.** Files describe the still design; the video is why it feels alive |

Best possible input = one design doc + one video. If the user asks what to provide, say that.
