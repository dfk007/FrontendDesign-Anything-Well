---
name: deepfield-design-system
description: >
  DEEPFIELD — a cinematic dark-mode design system for single-file HTML visual
  guides, explainers, and technical storytelling pages. Use whenever the user
  asks for an HTML page to present diagrams, images, concepts, or a multi-part
  visual narrative and wants a world-class, lively, dark, immersive design
  "like the MCP atlas". Produces a self-contained index.html with embedded
  CSS/JS: aurora stage, film grain, cursor glow, a scroll-progress "spine"
  with a traveling packet, scanner-style image frames, staggered reveals,
  3D tilt, and a lightbox. Works over file:// with zero dependencies except
  Google Fonts (graceful system fallbacks).
---

# DEEPFIELD — Frontend Design System

A design language for **visual field guides**: pages whose job is to make a
technical system *felt*, not just read. The signature metaphor: **the page is
a wire, and scrolling is a signal traveling through it.**

Reference implementation: `Why-MCP-Exists/index.html` (the MCP atlas).

---

## 1. Core philosophy (non-negotiable)

1. **Dark is the stage, light is the actor.** Background stays near-black.
   Color appears only as: accent glows, the traveling packet, bracket corners,
   and one gradient headline per page.
2. **One metaphor per page.** Pick a single spatial metaphor (wire/spine,
   orbit, pipeline, stack) and let every component serve it. DEEPFIELD's
   default is *the spine* — a vertical progress wire with a packet that
   travels as you scroll and docks at each chapter.
3. **Minimal text, maximal clarity.** Per section you are allowed: one kicker
   label, one headline, one sentence, a few mono chips. If a paragraph exceeds
   ~20 words, cut it. The visuals explain; the words orient.
4. **Everything moves with intent.** Motion always communicates state
   (reveal = entering focus, packet = progress, pulse = activity). No
   decorative bounce. All motion disabled under `prefers-reduced-motion`.
5. **Single file, zero build.** One `.html` file, embedded `<style>` and
   `<script>`, relative image paths. Must work when double-clicked from disk.

---

## 2. Design tokens

Always define as CSS custom properties on `:root`. Never hardcode.

```css
:root{
  /* surfaces */
  --bg:            #060609;   /* page background — near black, blue-violet cast */
  --bg-2:          #0b0b12;   /* raised surface */
  /* ink */
  --ink:           #e8e6f0;   /* primary text */
  --ink-dim:       #8f8ca3;   /* secondary text */
  --ink-faint:     #55536a;   /* tertiary / hints */
  /* accents */
  --violet:        #8b5cf6;   /* primary accent — structure, protocol */
  --violet-soft:   #a78bfa;   /* headline accent variant */
  --signal:        #34d399;   /* "alive" accent — packets, success, brackets */
  --amber:         #fbbf24;   /* tertiary accent — contrast concept */
  --rose:          #fb7185;   /* destructive / close */
  /* lines & frames */
  --line:          rgba(139, 92, 246, .14);
  --frame:         rgba(255,255,255,.07);
  --radius:        18px;
  /* type */
  --font-display:  "Space Grotesk", "Segoe UI", system-ui, sans-serif;
  --font-mono:     "JetBrains Mono", "SF Mono", Consolas, monospace;
}
```

**Accent semantics** — keep meaning consistent across pages:
`--violet` = the system/structure · `--signal` (green) = flow, life, data in
motion · `--amber` = an alternative/contrast path · `--rose` = exit/danger.

**Re-theming:** keep `--bg`, inks, and `--signal` fixed (they ARE the
Deepfield identity); you may swap `--violet` for another hue (e.g. cyan
`#22d3ee`, orange `#fb923c`) to fit a topic, and `--amber` accordingly.

### Typography rules
- Display: **Space Grotesk** 600–700, tight tracking (`letter-spacing:-.03em`),
  hero at `clamp(64px, 14vw, 190px)`, chapter headlines `clamp(34px, 5.4vw, 72px)`.
- Mono: **JetBrains Mono** for ALL labels, kickers, chips, nav, hints — always
  uppercase with wide tracking (`.2em`–`.5em`), sizes 10–12px.
- Body sentences: display font at weight 300, `var(--ink-dim)`, ~1.6 line-height.
- Load via Google Fonts `<link>`; system fallbacks keep the page decent offline.

---

## 3. The ambient stage (always 3 layers, fixed, `pointer-events:none`)

Every DEEPFIELD page sits on the same three-layer atmosphere:

1. **Aurora** — 2–3 huge `border-radius:50%` divs, `filter:blur(110px)`,
   `opacity:.22–.35`, deep desaturated radial gradients (e.g. `#4c1d95`,
   `#065f46`, `#7c2d12`), each drifting on a 30–50s `ease-in-out infinite
   alternate` keyframe. Orbs live at the page edges and bleed inward.
2. **Grain** — a full-viewport div with an inline SVG `feTurbulence`
   noise data-URI at `opacity:.05`, jittered with an 8s `steps(10)` keyframe.
   This kills banding and adds filmic texture.
3. **Cursor glow** — a ~520px `radial-gradient` disc (`mix-blend-mode:screen`,
   violet at ~9% alpha) that follows the pointer with lerp smoothing
   (`pos += (target-pos) * .08` in `requestAnimationFrame`).

Grain data-URI (reuse verbatim):

```css
.grain{
  position:fixed; inset:-50%; z-index:1; pointer-events:none;
  background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='240' height='240'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.5'/%3E%3C/svg%3E");
  opacity:.05; animation: grain 8s steps(10) infinite;
}
```

---

## 4. Signature components

### 4.1 The Spine (scroll progress, reimagined)
A fixed 2px vertical line near the left edge (`left:clamp(18px,4vw,56px)`),
filled via `transform:scaleY(var(--p))` with a violet→signal gradient. A 14px
`--signal` dot with layered `box-shadow` glow sits at `top:calc(var(--p)*100%)`.
One small **dock** dot per chapter is positioned at each chapter's vertical
center; docks turn violet + glow when their chapter is in the middle band of
the viewport. JS updates `--p` on scroll: `p = scrollY / (scrollHeight - innerHeight)`.

### 4.2 The Frame (how ALL images/diagrams are presented)
Images never sit bare. Wrap each in a `.frame`:

- translucent gradient fill + 1px `--frame` border, `--radius` corners,
  inner padding so the image reads as "behind glass"
- **corner brackets**: four 22×22px `--signal` L-brackets at opacity .65 via
  `::before/::after` on the frame and an inner `<span class="br">`; on hover
  they grow to 30px and full opacity
- a floating `.tag` label (mono, uppercase, signal color, pill, half-overlapping
  the top edge) naming what's inside the frame
- hover: border turns violet-ish, deep violet+signal box-shadow glow
- `.zoomhint` pill ("click to expand") fades in bottom-right on hover
- cursor: `zoom-in`

```html
<figure class="frame reveal d2" data-cap="01 · short caption">
  <span class="tag">label</span>
  <img src="img/…png" alt="…" loading="lazy">
  <span class="br"></span>
  <span class="zoomhint">click to expand</span>
</figure>
```

### 4.3 Nodes & wires (mini flow diagrams, pure CSS)
Pill "nodes" (mono 11px, `--frame` border, pill radius) connected by 2px
"wires" — a violet gradient line with a glowing 6–7px signal dot animating
left→right on a ~2s `linear infinite` loop (stagger delays across wires).
Use in the hero to preview the page's mental model, and in the finale to
recap the full chain. Highlight the central node with a signal-colored
border + inner glow.

### 4.4 Chips
Tiny mono pills (`11px`, `--ink-dim`, `--frame` border) listing key terms,
metrics, or API names. Hover: text turns signal, border tints signal. Use
3–5 per chapter, never more.

### 4.5 Header
Fixed, `mix-blend-mode:difference` (so it works over any content), brand in
mono caps left (`name<b>·</b>tag` with the middot in signal green), chapter
anchor links right in tiny mono (`01 why · 02 shape …`). Active link turns
signal via an IntersectionObserver with `rootMargin:'-40% 0px -40% 0px'`.
Hide the nav under 640px.

### 4.6 Lightbox
Fixed overlay, `rgba(4,4,8,.9)` + `backdrop-filter:blur(14px)`. Image scales
from `.94` on open. Round prev/next ghost buttons at the edges, mono
"esc ✕" top-right, mono caption bottom-center. Supports `←` `→` `Esc` keys;
clicking image or backdrop closes. Lock body scroll while open.

---

## 5. Page structure (the canonical skeleton)

```
<stage>        aurora + grain + cursor glow          (fixed, z 0–2)
<spine>        progress wire + packet + docks        (fixed, z 5)
<header>       brand + chapter nav                   (fixed, z 10, blend diff)
<hero>         100svh — kicker / giant gradient H1 / one-sentence sub /
               nodes-and-wires preview / animated scroll cue
<main>
  <chapter>    min-height:100svh, alternating 2-col grid:
               text column = kicker "chapter NN — name", H2 with accent spans,
               one-sentence paragraph, chips
               media column = .frame with the visual
</main>
<finale>       ~90svh, centered — one-line thesis, full nodes-and-wires
               recap strip with "heat pulse" cycling a highlight across nodes,
               tiny mono footer
<lightbox>     overlay
```

**Grid:** `grid-template-columns: minmax(300px,5fr) 7fr`; `.flip` chapters
swap columns. Below 1024px collapse to single column; keep generous left
padding so content never touches the spine.

**Hero H1** is the page's one typographic spectacle: `background:
linear-gradient(115deg,#fff 20%, var(--violet-soft) 55%, var(--signal) 90%)`
with `background-clip:text`. Chapter H2s are plain ink with 1–3 accented
words (`.accent` = signal, `.accent-v` = violet-soft, `.accent-a` = amber).

---

## 6. Motion system

| Effect | Spec |
|---|---|
| Reveal on scroll | `.reveal{opacity:0; translateY(48px)}` → `.in` via IntersectionObserver (threshold .18), `.9s cubic-bezier(.2,.8,.2,1)`, stagger `.d1/.d2/.d3` at 120ms steps |
| Hero entrance | `rise` keyframe, 1s, elements staggered 100–150ms, all `both` fill |
| 3D tilt | on pointermove over `.frame`: `perspective(1100px) rotateY(x*5deg) rotateX(-y*5deg)`, rAF-throttled; spring back on leave with a 600ms transition |
| Scroll cue | mono label + 44px gradient line doing a `drip` scaleY loop, 1.8s |
| Packet travel | 2s `linear infinite`, fade in/out at wire ends, stagger delays |
| Heat pulse (finale) | `setInterval` 900ms cycling a `.hot` class across recap nodes |
| Easing | entrances `cubic-bezier(.2,.8,.2,1)`; loops `linear` or `ease-in-out` |
| Reduced motion | one media query zeroing all animation/transition durations |

---

## 7. Copywriting rules

- Kicker format: `chapter NN — the <noun>` (lowercase, mono).
- Headlines are claims, not labels: "Nine hand-built bridges, or one shared
  protocol." not "Why MCP Exists".
- One sentence per chapter, ≤ 20 words, ending with a period.
- Chips carry the jargon (API names, numbers, formulas) so prose stays clean.
- Footer format: `project · name — built for <user>`.

---

## 8. Recipe — building a new DEEPFIELD page

1. Create a folder; copy visuals into `img/` with numbered, kebab-case names.
2. Single `index.html`: tokens → stage → spine → header → hero → chapters
   (one per visual, alternating flip) → finale → lightbox → script.
3. Write the 5-part copy per chapter (kicker/headline/sentence/chips) BEFORE
   styling; enforce the word budget.
4. Number chapters in the header nav and spine docks to match section count.
5. Keep all JS vanilla: one lerp loop (glow), one scroll handler (spine),
   three observers (reveal, nav-active), tilt, lightbox, heat pulse.
6. Verify: open via a local `python3 -m http.server` and screenshot the hero,
   a mid chapter, and the finale. Check reveal states triggered, packet
   visible, brackets crisp, no horizontal overflow.
7. Stop the server when done — the file must also work from `file://`.

## 9. Don'ts

- No cards-in-cards, no visible boxes around text — text floats on the stage.
- No more than 3 accent colors per page + rose for close/destructive only.
- No carousels, no tabs, no modals other than the lightbox.
- No heavy frameworks, no icon fonts, no emoji in UI chrome.
- No walls of text; if explanation is needed, it becomes a new chapter
  with a visual, not a paragraph.
- No white frames around images — always the dark "glass + brackets" frame.

## 10. Definition of done (quality bar)

- [ ] Single self-contained HTML file, images in `img/`, works from `file://`
- [ ] All three stage layers present (aurora / grain / glow)
- [ ] Spine packet travels and docks light up per chapter
- [ ] Every image in a bracketed frame with tag, tilt, and lightbox
- [ ] Word budget honored (kicker + headline + ≤20-word sentence + chips)
- [ ] Lightbox keyboard nav works; body scroll locks
- [ ] `prefers-reduced-motion` respected
- [ ] No console errors; no horizontal scrollbar at 360px–1920px
