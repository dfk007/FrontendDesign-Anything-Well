---
name: frontend-design
description: >
  Warm neutral-paper "operating system" design language for strategy decks, profile/portfolio
  audits, and structured advisory reports rendered as a single scrollable web page. Off-white
  paper background, near-black ink text, a bright lime-green primary accent plus a soft
  pastel supporting palette (blue, peach, lavender, yellow), rounded 20px cards on a 12-column
  grid, and Space Grotesk display type paired with DM Sans body text. Feels like a hybrid of a
  Notion doc, a pitch deck, and a dashboard — structured, confident, editorial, never dark-mode,
  never glassy or neon. Use for consulting/audit reports, personal-brand or resume strategy
  pages, roadmap/plan pages, and any "here is the diagnosis, here is the plan" one-page site.
---

# Paper OS — Design System Skill

## Concept & Aesthetic Direction

Paper OS reads as a **calm, editorial strategy document that behaves like a product UI**. It
fuses three traditions:

1. **Swiss/editorial print** — big confident display headlines, generous whitespace, a strict
   12-column grid, numbered section labels ("01 / Read the signal").
2. **Notion-style soft dashboard** — rounded 20px cards, pastel tag chips, big bold metric
   numbers, soft ambient drop shadows instead of borders-only separation.
3. **Startup pitch-deck** — one loud accent color (lime) used sparingly but decisively, a dark
   "hero visual" card that inverts the palette to create a single high-contrast focal point per
   page.

**What it is NOT:**
- Not dark mode. The canvas is always warm off-white paper; only isolated card surfaces (like
  the hero visual or a highlighted quote card) invert to near-black.
- Not neon/cyberpunk — the lime accent is a flat matte swatch, never glowing, never with
  text-shadow or box-shadow bloom.
- Not glassmorphic — no blur, no translucent frosted panels. The one exception is the nav pill
  which uses a subtle `#ffffff80` (50% white) fill over the paper, not a blur.
- Not heavy-bordered brutalism — borders are hairline (1px) and mostly used as horizontal
  section dividers, not as the primary structural device (shadows + radius do that job).

**When appropriate:** internal or client-facing strategy reports, audits, personal brand /
portfolio repositioning pages, execution roadmaps, "diagnosis → plan" documents, anything that
needs to feel like a confident, structured recommendation rather than raw data or marketing hype.

---

## Typography

### Import (verbatim)

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Space+Grotesk:wght@500;600;700&display=swap" rel="stylesheet">
```

### Font roles

| Font | Weights loaded | Used for |
|---|---|---|
| **DM Sans** | 400, 500, 600, 700 | Body text, paragraphs, nav links, muted captions, tag chips, small metric suffix labels |
| **Space Grotesk** | 500, 600, 700 | All headings (`h1`, `h2`, `h3`), the brand/logo wordmark, all big numeric "metric" figures |

Base body rule:
```css
body{
  margin:0;
  background:var(--paper);
  color:var(--ink);
  font:15px/1.55 'DM Sans', system-ui, sans-serif;
}
h1,h2,h3,p{ margin:0; }
h1,h2,h3,.brand,.metric{ font-family:'Space Grotesk', sans-serif; }
```

### Exact per-role values

**Brand / logo wordmark** (`.brand`)
```css
font-weight:700; letter-spacing:-.04em; font-size:19px;
```

**Eyebrow label** (small caps label above every section heading — the numbered-section idiom)
```css
.eyebrow{
  font-size:12px;
  letter-spacing:.14em;
  text-transform:uppercase;
  color:var(--green);
  font-weight:700;
  margin-bottom:18px;
}
```

**Hero H1** (the single largest headline on the page, used once)
```css
.hero h1{
  font-size:clamp(40px,6vw,78px);
  letter-spacing:-.075em;
  line-height:.98;
  max-width:750px;
}
```
Mobile override (≤860px): `font-size:clamp(42px,13vw,68px)`.

Inline emphasis inside the hero H1 uses a highlighter-marker span, not italics or color alone:
```css
.hero h1 em{
  font-style:normal;
  background:var(--lime);
  padding:0 .12em;
  border-radius:8px;
}
```

**Hero lede paragraph**
```css
.hero-lede{
  font-size:19px;
  color:var(--muted);
  max-width:630px;
  margin:24px 0;
}
```
Mobile: `font-size:17px`.

**Section heading** (`h2`, repeats once per section)
```css
.section h2{ font-size:30px; letter-spacing:-.05em; }
```

**Section intro paragraph** (sits beside/under the `h2`)
```css
.section-intro{ color:var(--muted); max-width:590px; }
```

**Card heading** (`h3` inside `.card`)
```css
.card h3{ font-size:18px; margin-bottom:8px; letter-spacing:-.03em; }
```
Large "quote card" variant bumps this up ad hoc via inline style to `font-size:29px;
line-height:1.15` or `font-size:26px` for a primary headline card — treat 18px as the
default and scale up only for a single hero-quote card per page.

**Metric figure** (big bold numbers — the signature device of this system)
```css
.metric{
  font-size:42px;
  line-height:1;
  font-weight:700;
  letter-spacing:-.07em;
}
.metric small{
  font:600 14px 'DM Sans';
  letter-spacing:0;
  color:var(--muted);
}
```
Mobile: `font-size:38px`. The `<small>` suffix (e.g. `/hr`, `%`, `ms p99`) always resets to
DM Sans at 14px/600 — never inherits the Space Grotesk display font.

**Flag label** (all-caps micro-label at the top of a card, like a category tag)
```css
.flag{
  font-size:12px;
  color:#a25540;
  font-weight:700;
  text-transform:uppercase;
  letter-spacing:.1em;
}
```
Note: `.flag` uses a distinct rust/terracotta color (`#a25540`), separate from `.eyebrow`'s
green — `.eyebrow` marks section-level labels, `.flag` marks card-level labels. Keep this
distinction; don't collapse them into one color.

**Muted / secondary text** (used everywhere for de-emphasized copy)
```css
.muted{ color:var(--muted); }
```

**Caption** (small text under the hero visual)
```css
.caption{ font-size:13px; color:#aeb5ab; margin-top:18px; }
```
This is a lighter tint used only inside the dark `.hero-visual` card — do not use it on the
paper background (insufficient contrast by design; it's meant to read as a quiet caption over
dark).

### Decision logic

- Use **Space Grotesk** for anything that is a number, a heading, or the brand mark — anything
  meant to be scanned first.
- Use **DM Sans** for anything meant to be read — body copy, muted captions, nav, tags, the
  metric's unit suffix.
- Never mix: a `.metric` block's suffix (`<small>`) is the one deliberate exception where DM
  Sans nests inside a Space Grotesk parent, and it must explicitly reset `font` to do so.

---

## Color System

### Full token block

```css
:root{
  --ink:#20211f;      /* primary text, dark card backgrounds, dark button fill */
  --muted:#6f746e;     /* secondary/tertiary text */
  --paper:#f4f4ef;     /* page background */
  --card:#fff;         /* card surface background */
  --line:#dedfd7;      /* hairline borders / dividers */
  --lime:#d9f27c;      /* primary accent — highlights, primary tag, hero visual accent circle */
  --blue:#c9e9f5;      /* pastel accent 2 — secondary stack layer, infra-flavored tags */
  --peach:#ffd8c8;     /* pastel accent 3 — tertiary stack layer, action-flavored tags */
  --lav:#e4d8f8;       /* pastel accent 4 — quaternary stack layer */
  --yellow:#ffe59a;    /* pastel accent 5 — callout/highlight card background */
  --green:#3f7a5a;     /* eyebrow labels, positive/"good" state accents, arrow icons */
  --shadow:0 12px 34px #20211f0d;  /* ambient card shadow — ink at 5% opacity, soft & wide */
  --r:20px;            /* card border-radius */
}
```

No theme-switching mechanism exists in this system — it is single-theme (light/paper) only.
There is no `[data-theme]` attribute, no `prefers-color-scheme` handling, and no JS toggle. If
a dark mode is required for a derived application, treat that as new design work, not a
variable swap — this system's identity depends on the warm paper canvas.

### Semantic groupings

| Group | Variables | Usage rule |
|---|---|---|
| **Canvas** | `--paper` | Body background only |
| **Surface** | `--card` | Card backgrounds, pill background base |
| **Text hierarchy** | `--ink` (primary), `--muted` (secondary) | Never use pure black or pure gray — always these two warm-tinted values |
| **Structure** | `--line` | 1px borders on cards, topbar bottom border, section top border, divider rules |
| **Primary accent** | `--lime` | The ONE loud color: em-highlight in H1, `.tag.ai`, accent circle in hero visual, `.stack .s1` (first/most-important stack layer) |
| **Pastel support set** | `--blue`, `--peach`, `--lav` | Used in strict sequence for ordered/layered lists (see `.stack`), and for `.tag.infra` (blue) / `.tag.action` (peach). `--lav` has no tag class in the source but is reserved as the 4th sequential pastel |
| **Callout** | `--yellow` | Reserved for exactly one "non-negotiables"-style highlighted full-width card per page — not for routine cards |
| **Positive/system accent** | `--green` | Eyebrow label color, `.arrow` icon color, `.state.good` is a *tint background* (`#edf7dc`, hand-picked, not a `--green` derivative) |
| **Rust/warning label** | `#a25540` (not tokenized) | `.flag` label color only |

### Color usage rules

1. **Lime is scarce.** It appears as: one em-highlight per hero H1, one tag variant, one hero
   visual accent shape, and the first (top) item in any ranked/stacked list. It never becomes a
   full section background or a text color for body copy.
2. **Pastels are sequential, not arbitrary.** When showing an ordered list of 3–4 items of
   decreasing emphasis (see `.stack`), assign colors in this fixed order: lime → blue → peach →
   lavender. This order is itself a signal of rank/priority.
3. **Ink inverts sparingly.** Only one card per page (the hero visual, or an equivalent
   "primary quote" card) inverts to `background:var(--ink); color:#fff`. Everything else stays
   on the light paper/card surfaces. Overusing dark cards destroys the device's impact.
4. **Yellow is a stop sign.** Use the `--yellow` background only for a single "read this
   carefully" callout block per page (rules, non-negotiables, warnings) — never for routine
   content cards.
5. **Shadows carry the elevation, not borders.** Cards use both a 1px `--line` border AND the
   `--shadow` ambient shadow together — the shadow is what makes them feel "soft" rather than
   flat-outlined.

---

## Background & Atmosphere

This system has **no atmospheric pseudo-elements** — no grid overlays, no noise textures, no
ambient glows on the body, no `body::before`/`body::after` layers. The paper background is a
completely flat `var(--paper)` fill.

The one atmospheric device in the whole system lives inside `.hero-visual`, not on the body:

```css
.hero-visual{
  background:var(--ink);
  border-radius:28px;
  padding:26px;
  color:#fff;
  box-shadow:var(--shadow);
  position:relative;
  overflow:hidden;
}
.hero-visual:after{
  content:'';
  position:absolute;
  width:220px;
  height:220px;
  border-radius:50%;
  right:-80px;
  top:-80px;
  background:var(--lime);
  opacity:.85;
}
```

This is a single oversized lime circle, bled off the top-right corner of the dark hero card, at
85% opacity, sitting behind the card's content (`z-index` implicit — content wrapped in
`position:relative; z-index:1` sits above it). Treat this as the system's one permitted
"ambient accent" move, and reserve it for exactly one card per page — do not scatter decorative
circles throughout.

**Z-index layering inside `.hero-visual`:**
1. `.hero-visual` itself (`position:relative`)
2. `:after` lime circle — no explicit z-index, painted per DOM order (before content, so it
   sits behind since content gets `z-index:1`)
3. `.visual-label`, `.stack`, `.caption` — all explicitly `position:relative; z-index:1`

---

## Layout

### Page wrapper

```css
.shell{
  max-width:1280px;
  margin:auto;
  padding:0 28px;
}
```
Mobile (≤860px): `padding:0 18px`.

Every top-level section reuses `.shell` as its inner container — the outer `<section>` /
`<header>` / `<footer>` spans full width for the border-top divider, and `.shell` centers the
content within it.

### Topbar

```css
.topbar{
  height:72px;
  border-bottom:1px solid var(--line);
  display:flex;
  align-items:center;
  justify-content:space-between;
}
.brand span{
  display:inline-block; width:12px; height:12px;
  border-radius:50%; background:var(--green); margin-right:8px;
}
.topnav{ display:flex; gap:8px; align-items:center; }
.topnav a{
  color:var(--muted); text-decoration:none;
  padding:8px 12px; border-radius:9px;
}
.topnav a:hover{ background:#e9eae3; color:var(--ink); }
.pill{
  border:1px solid var(--line); border-radius:99px;
  padding:8px 13px; font-size:12px; color:var(--muted);
  background:#ffffff80;
}
```
Mobile: `.topbar` becomes `height:auto; min-height:68px; gap:12px`; `.topnav` becomes
horizontally scrollable (`overflow-x:auto; white-space:nowrap`) and nav `<a>` links are hidden
(`display:none`), leaving only the `.pill` status badge visible.

### Hero (asymmetric two-column)

```css
.hero{
  padding:64px 0 54px;
  display:grid;
  grid-template-columns:1.15fr .85fr;
  gap:56px;
  align-items:center;
}
```
This 1.15fr / .85fr ratio (roughly 58/42) is deliberate — text column slightly wider than the
visual column. Mobile collapses to `grid-template-columns:1fr; gap:30px; padding:46px 0 38px`.

Hero actions row:
```css
.hero-actions{ display:flex; gap:10px; flex-wrap:wrap; }
.btn{
  border:0; padding:12px 17px; border-radius:10px;
  text-decoration:none; font-weight:700; cursor:pointer;
  font-family:inherit;
}
.btn-dark{ background:var(--ink); color:#fff; }
.btn-light{ background:var(--card); border:1px solid var(--line); color:var(--ink); }
```

### Section structure (repeats per `<section class="section">`)

```css
.section{ padding:44px 0; border-top:1px solid var(--line); }
.section-head{
  display:flex; justify-content:space-between;
  align-items:end; gap:20px; margin-bottom:22px;
}
```
Mobile: `.section{ padding:34px 0; }`, `.section-head{ display:block; }` (stacks instead of
justify-between), with `.section-intro{ margin-top:10px; }` to restore spacing once stacked.

Every section follows this exact anatomy: `.eyebrow` (numbered label) → `h2` (headline) on the
left of `.section-head`, `.section-intro` paragraph on the right — then a `.grid` of `.card`
elements below.

### 12-column card grid

```css
.grid{ display:grid; grid-template-columns:repeat(12,1fr); gap:16px; }
.card{
  background:var(--card); border:1px solid var(--line);
  border-radius:var(--r); padding:22px; box-shadow:var(--shadow);
}
.span-3{ grid-column:span 3; }
.span-4{ grid-column:span 4; }
.span-5{ grid-column:span 5; }
.span-6{ grid-column:span 6; }
.span-7{ grid-column:span 7; }
.span-8{ grid-column:span 8; }
.span-12{ grid-column:span 12; }
```
Mobile: grid collapses to single column and **every** span utility is forced to full width —
`.grid{ grid-template-columns:1fr; } .grid>*{ grid-column:span 1 !important; }`.

Nesting: a `.span-12` card can itself contain a nested `.grid` (see the "Technical outcomes"
and "Non-negotiables" cards in the source) — always with `margin-top:12–14px` on the nested
grid to separate it from the card's heading.

### Border-as-structure pattern

The only structural (non-card) borders in the system are horizontal 1px `--line` rules used as
section separators (`.section{ border-top:... }`, `.topbar{ border-bottom:... }`) and as
manual divider rules inside cards (`<div style="height:1px;background:var(--line);
margin:20px 0"></div>`) to split a card into labeled zones without introducing a second nested
card.

---

## Components

### Metric Card

The core content unit — an oversized number with a flag label above and a muted description
below.

```css
.card .flag{ /* label */ }
.card .metric{ /* big number, optionally with <small> unit */ }
.card p.muted{ /* one-line explanation */ }
```

```html
<div class="card span-3">
  <div class="flag">Recommended rate</div>
  <div class="metric">$75–100<small>/hr</small></div>
  <p class="muted">Above volume-fix work, below proof-heavy premium.</p>
</div>
```

States: none — this is a static display card, no hover/interactive state in the source.

### Tag / Chip

```css
.tag{
  display:inline-block; font-size:12px;
  padding:6px 9px; border-radius:7px;
  background:#eef0e8; margin:4px 3px 0 0;
}
.tag.ai{ background:var(--lime); }
.tag.infra{ background:var(--blue); }
.tag.action{ background:var(--peach); }
```
Default (untyped) tag uses a neutral sage-tinted gray (`#eef0e8`), not a palette pastel — this
is the "generic/other" bucket. Always assign a semantic class (`ai` / `infra` / `action`) when
the tag represents a scored category; leave it bare only for filler/context tags.

### Positioning Stack (staggered indent list)

The signature "layered pastel blocks" idiom used inside the dark hero visual.

```css
.stack{ position:relative; z-index:1; margin:28px 0 6px; display:grid; gap:9px; }
.stack div{ padding:15px; border-radius:12px; font-weight:700; }
.stack .s1{ background:var(--lime); color:var(--ink); margin-left:0; }
.stack .s2{ background:var(--blue); color:var(--ink); margin-left:28px; }
.stack .s3{ background:var(--peach); color:var(--ink); margin-left:56px; }
.stack .s4{ background:var(--lav); color:var(--ink); margin-left:84px; }
```
Mobile: indents compress — `s2: margin-left:16px`, `s3: 32px`, `s4: 48px` (from 28/56/84px).

Each successive item indents further right and steps to the next pastel in the fixed sequence
(lime → blue → peach → lav). Text inside each block is always `var(--ink)` regardless of the
block's background (all pastels are light enough for dark text). Use for "ranked layers of a
stack/pipeline/priority list," 3–4 items max — more than 4 has no defined color beyond `--lav`.

### Before/After Comparison Block

```css
.before-after{
  display:grid; grid-template-columns:1fr 40px 1fr;
  gap:12px; align-items:stretch;
}
.state{ padding:16px; border-radius:14px; background:#f3f3ee; }
.state.good{ background:#edf7dc; }
.state strong{ display:block; font-family:'Space Grotesk'; margin-bottom:5px; }
.arrow{
  display:flex; align-items:center; justify-content:center;
  font-size:24px; color:var(--green);
}
```
Mobile: `.before-after{ grid-template-columns:1fr; }`, `.arrow{ transform:rotate(90deg);
height:20px; }` (arrow rotates to point downward when stacked).

```html
<div class="before-after">
  <div class="state">
    <strong>Today · friction</strong>
    <span class="muted">description of the current/bad state</span>
  </div>
  <div class="arrow">→</div>
  <div class="state good">
    <strong>Target · clear signal</strong>
    <span class="muted">description of the target/good state</span>
  </div>
</div>
```
`.state` (default) = neutral gray-green tint for "before." `.state.good` = pale lime-green
tint for "after." Never swap these — good/target state is always the `.good` variant.

### Inverted Quote / Headline Card

A single full-bleed dark card used once per page to state the core thesis or positioning
statement in oversized type.

```html
<div class="card span-7" style="background:var(--ink);color:#fff">
  <div class="flag" style="color:var(--lime)">One-liner for messages</div>
  <h3 style="font-size:29px;line-height:1.15;margin-top:18px">"..."</h3>
  <p style="color:#b7beb3;margin-top:18px">Supporting line.</p>
</div>
```
Note the `.flag` label recolors to `--lime` (not its default rust) when placed on a dark card
— flag color always adapts to maintain contrast against its immediate background, rust on
paper/white, lime on ink.

### Callout / Non-Negotiables Card

```html
<div class="card span-12" style="background:var(--yellow)">
  <h3>Non-negotiables</h3>
  <div class="grid" style="margin-top:12px">
    <p class="span-4"><strong>Do:</strong> ...</p>
    <p class="span-4"><strong>Don't:</strong> ...</p>
    <p class="span-4"><strong>Fallback:</strong> ...</p>
  </div>
</div>
```
Full-width, flat `--yellow` fill, no border override (keeps the default `--line` border and
`--shadow`), nested 3-column grid for parallel Do/Don't/Fallback copy.

### Navigation Link (hover state)

```css
.topnav a{ color:var(--muted); text-decoration:none; padding:8px 12px; border-radius:9px; }
.topnav a:hover{ background:#e9eae3; color:var(--ink); }
```
Simple background-fill hover, no underline, no transition timing defined in source (instant
snap) — acceptable to add `transition:background .15s ease` when porting, as a safe
enhancement, not a deviation.

### Buttons

```css
.btn{ border:0; padding:12px 17px; border-radius:10px; text-decoration:none; font-weight:700; cursor:pointer; font-family:inherit; }
.btn-dark{ background:var(--ink); color:#fff; }
.btn-light{ background:var(--card); border:1px solid var(--line); color:var(--ink); }
```
No hover/active states defined in source — when porting, keep changes subtle (e.g. slight
opacity or background-darken on `.btn-dark:hover`), never scale/transform, to stay consistent
with the system's restrained interaction language.

---

## Animation & Motion

The system defines **no `@keyframes`** and **no `transition` rules** on any component. The
only motion-related CSS is:

```css
html{ scroll-behavior:smooth; }
```

and a reduced-motion safeguard:
```css
@media(prefers-reduced-motion:reduce){
  *{ scroll-behavior:auto !important; transition:none !important; }
}
```

**Rule for derived work:** this system is intentionally static/instant. If you add hover
transitions (e.g. on `.topnav a` or `.btn`), keep them fast and subtle (120–180ms ease,
background/opacity only — never transform/scale, never box-shadow bloom) and always preserve
the `prefers-reduced-motion` override.

---

## Responsive Breakpoints

Single breakpoint at **860px** (mobile-first override applied above it via `max-width:860px`).
Full consolidated override block:

```css
@media(max-width:860px){
  .shell{ padding:0 18px; }
  .topbar{ height:auto; min-height:68px; gap:12px; }
  .topnav{ overflow-x:auto; white-space:nowrap; }
  .topnav a{ display:none; }
  .topnav .pill{ margin-left:0; }
  .hero{ grid-template-columns:1fr; gap:30px; padding:46px 0 38px; }
  .hero h1{ font-size:clamp(42px,13vw,68px); }
  .hero-lede{ font-size:17px; }
  .grid{ grid-template-columns:1fr; }
  .grid>*{ grid-column:span 1 !important; }
  .before-after{ grid-template-columns:1fr; }
  .arrow{ transform:rotate(90deg); height:20px; }
  .section{ padding:34px 0; }
  .section-head{ display:block; }
  .section-intro{ margin-top:10px; }
  .hero-visual{ padding:22px; }
  .stack .s2{ margin-left:16px; }
  .stack .s3{ margin-left:32px; }
  .stack .s4{ margin-left:48px; }
  .card{ padding:19px; }
  .metric{ font-size:38px; }
}

@media(prefers-reduced-motion:reduce){
  *{ scroll-behavior:auto !important; transition:none !important; }
}
```

No tablet-specific intermediate breakpoint exists — the layout jumps directly from the 12-col
desktop grid to a fully single-column mobile stack at 860px. When porting to a new app, insert
an intermediate breakpoint (e.g. 1024px, dropping `span-*` to a 2-column max) only if your
content density genuinely needs it — the source system does not use one.

---

## Print Styles

None defined in the source. No `@media print` block exists.

---

## JavaScript Behavior

**None.** The page is pure CSS/HTML — no `<script>` tags, no theme toggle, no tab switching,
no accordion, no search/filter, no localStorage usage. The only "interactivity" is native
anchor-link navigation (`<a href="#section-id">`) combined with `scroll-behavior:smooth`.

If a derived application needs interactivity (tabs, accordions, filters), implement it without
changing any visual token above — add `.is-active` / `.is-open` style state classes that reuse
existing tokens (e.g., an active tab could adopt the `.tag.ai` lime treatment) rather than
inventing new colors.

---

## Design Rules — Do & Don't

**Do:**
- Keep the canvas `var(--paper)` at all times; only individual cards may invert to ink.
- Use exactly one numbered `.eyebrow` label per section, in the green `#3f7a5a`, uppercase,
  `.14em` letter-spacing.
- Use `.metric` + `<small>` for every standalone statistic — never render a stat as plain body
  text.
- Reserve `--lime` for: one hero em-highlight, the `.tag.ai` chip, the hero-visual accent
  circle, and the first item of any `.stack`.
- Follow the fixed pastel sequence lime → blue → peach → lav for any ranked/staggered list.
- Pair every `.card` with both its 1px `--line` border AND `--shadow` — never drop one and keep
  the other.
- Keep border-radius consistently at `--r` (20px) for cards, 28px for the hero visual, 99px for
  pill/badge shapes, 50% for dot/circle accents. No sharp (0px) corners anywhere in this system.
- Limit dark-inverted (`background:var(--ink)`) cards to one per page section, maximum two per
  full page.
- Limit `--yellow` callout cards to one per page.
- Use `.flag` (rust `#a25540`) for card-level micro-labels on light cards; recolor to `--lime`
  when the flag sits on a dark/ink card.

**Don't:**
- Don't introduce a dark-mode/theme-switch — this system has no theming layer; it is single-
  theme by design.
- Don't add glow, blur, or neon treatments to `--lime` — it is always a flat matte swatch.
- Don't use `--lime` as a large background fill (a whole card or section) — it's an accent, not
  a surface color.
- Don't add box-shadow bloom, transform/scale hovers, or long transitions — motion in this
  system is restrained to none-or-subtle, and `scroll-behavior:smooth` plus a
  `prefers-reduced-motion` guard is the only motion contract that must always be preserved.
- Don't mix border-radius scales — don't introduce 4px "sharp" cards alongside 20px cards.
- Don't let `.metric`'s `<small>` suffix inherit Space Grotesk — always explicit `font:600 14px
  'DM Sans'`.
- Don't collapse `.eyebrow` and `.flag` into the same color — green marks section-level,
  rust/lime marks card-level.
- Don't add a second intermediate breakpoint unless content density demands it; the source
  jumps straight from full desktop grid to single-column mobile at 860px.

---

## Composing a New Application in This System

### Page scaffold

```html
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>{{PAGE_TITLE}}</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Space+Grotesk:wght@500;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --ink:#20211f; --muted:#6f746e; --paper:#f4f4ef; --card:#fff; --line:#dedfd7;
  --lime:#d9f27c; --blue:#c9e9f5; --peach:#ffd8c8; --lav:#e4d8f8; --yellow:#ffe59a;
  --green:#3f7a5a; --shadow:0 12px 34px #20211f0d; --r:20px;
}
*{ box-sizing:border-box; }
html{ scroll-behavior:smooth; }
body{ margin:0; background:var(--paper); color:var(--ink); font:15px/1.55 'DM Sans',system-ui,sans-serif; }
h1,h2,h3,p{ margin:0; }
h1,h2,h3,.brand,.metric{ font-family:'Space Grotesk',sans-serif; }
.shell{ max-width:1280px; margin:auto; padding:0 28px; }
.topbar{ height:72px; border-bottom:1px solid var(--line); display:flex; align-items:center; justify-content:space-between; }
.brand{ font-weight:700; letter-spacing:-.04em; font-size:19px; }
.brand span{ display:inline-block; width:12px; height:12px; border-radius:50%; background:var(--green); margin-right:8px; }
.topnav{ display:flex; gap:8px; align-items:center; }
.topnav a{ color:var(--muted); text-decoration:none; padding:8px 12px; border-radius:9px; }
.topnav a:hover{ background:#e9eae3; color:var(--ink); }
.pill{ border:1px solid var(--line); border-radius:99px; padding:8px 13px; font-size:12px; color:var(--muted); background:#ffffff80; }
.eyebrow{ font-size:12px; letter-spacing:.14em; text-transform:uppercase; color:var(--green); font-weight:700; margin-bottom:18px; }
.section{ padding:44px 0; border-top:1px solid var(--line); }
.section-head{ display:flex; justify-content:space-between; align-items:end; gap:20px; margin-bottom:22px; }
.section h2{ font-size:30px; letter-spacing:-.05em; }
.section-intro{ color:var(--muted); max-width:590px; }
.grid{ display:grid; grid-template-columns:repeat(12,1fr); gap:16px; }
.card{ background:var(--card); border:1px solid var(--line); border-radius:var(--r); padding:22px; box-shadow:var(--shadow); }
.span-3{ grid-column:span 3; } .span-4{ grid-column:span 4; } .span-5{ grid-column:span 5; }
.span-6{ grid-column:span 6; } .span-7{ grid-column:span 7; } .span-8{ grid-column:span 8; } .span-12{ grid-column:span 12; }
.card h3{ font-size:18px; margin-bottom:8px; letter-spacing:-.03em; }
.muted{ color:var(--muted); }
.metric{ font-size:42px; line-height:1; font-weight:700; letter-spacing:-.07em; }
.metric small{ font:600 14px 'DM Sans'; letter-spacing:0; color:var(--muted); }
.tag{ display:inline-block; font-size:12px; padding:6px 9px; border-radius:7px; background:#eef0e8; margin:4px 3px 0 0; }
.tag.ai{ background:var(--lime); } .tag.infra{ background:var(--blue); } .tag.action{ background:var(--peach); }
.flag{ font-size:12px; color:#a25540; font-weight:700; text-transform:uppercase; letter-spacing:.1em; }
.before-after{ display:grid; grid-template-columns:1fr 40px 1fr; gap:12px; align-items:stretch; }
.state{ padding:16px; border-radius:14px; background:#f3f3ee; }
.state.good{ background:#edf7dc; }
.state strong{ display:block; font-family:'Space Grotesk'; margin-bottom:5px; }
.arrow{ display:flex; align-items:center; justify-content:center; font-size:24px; color:var(--green); }
.btn{ border:0; padding:12px 17px; border-radius:10px; text-decoration:none; font-weight:700; cursor:pointer; font-family:inherit; }
.btn-dark{ background:var(--ink); color:#fff; }
.btn-light{ background:var(--card); border:1px solid var(--line); color:var(--ink); }
@media(max-width:860px){
  .shell{ padding:0 18px; }
  .topbar{ height:auto; min-height:68px; gap:12px; }
  .topnav{ overflow-x:auto; white-space:nowrap; }
  .topnav a{ display:none; }
  .grid{ grid-template-columns:1fr; }
  .grid>*{ grid-column:span 1 !important; }
  .before-after{ grid-template-columns:1fr; }
  .arrow{ transform:rotate(90deg); height:20px; }
  .section{ padding:34px 0; }
  .section-head{ display:block; }
  .section-intro{ margin-top:10px; }
  .card{ padding:19px; }
  .metric{ font-size:38px; }
}
@media(prefers-reduced-motion:reduce){
  *{ scroll-behavior:auto !important; transition:none !important; }
}
</style>
</head>
<body>
<div class="shell">
  <header class="topbar">
    <div class="brand"><span></span>{{BRAND_NAME}}</div>
    <nav class="topnav">
      <a href="#section-1">{{NAV_1}}</a>
      <a href="#section-2">{{NAV_2}}</a>
      <div class="pill">{{STATUS_PILL_TEXT}}</div>
    </nav>
  </header>

  <main>
    <section class="section" id="section-1">
      <div class="section-head">
        <div>
          <div class="eyebrow">{{SECTION_NUMBER}} / {{SECTION_LABEL}}</div>
          <h2>{{SECTION_HEADLINE}}</h2>
        </div>
        <p class="section-intro">{{SECTION_INTRO_COPY}}</p>
      </div>
      <div class="grid">
        <!-- cards go here -->
      </div>
    </section>
  </main>

  <footer class="section" style="padding-bottom:60px">
    <p class="muted">{{FOOTER_COLOPHON_TEXT}}</p>
  </footer>
</div>
</body>
</html>
```

### Adapting other UI elements not present in the source

- **Data table:** wrap in a `.card`, use `--line` for row dividers (1px, bottom-border only),
  header row in `.flag`-style uppercase rust or `.eyebrow`-style green, body cells in default
  15px DM Sans, numeric columns right-aligned using `.metric` styling only if the number is the
  single most important figure in that row (don't apply `.metric` to routine data-table cells).
- **Form inputs:** background `var(--card)`, border `1px solid var(--line)`, radius `10px`
  (matches `.btn`), focus state: swap border to `var(--ink)` (2px) — do not use `--lime` as a
  focus ring color, it's reserved as a background/highlight fill, not an outline color.
- **Badges/status pills:** reuse `.pill` for neutral status, or `.tag` + a semantic class for
  categorized status (map "success" → sits closest to `.tag.ai`'s lime, "info" → `.tag.infra`
  blue, "warning" → `.tag.action` peach, "danger" → introduce a new class using `#a25540` rust
  at ~15% tint background, since no red/danger token exists in the source palette).
- **Progress meters:** track background `#eef0e8` (same as default `.tag`), fill `var(--lime)`,
  radius `99px` (pill), height `8–10px` — no defined pattern in source, this is a safe
  extrapolation consistent with existing tokens.
- **Code blocks:** not present in source; if needed, use `var(--ink)` background, `#fff` text,
  a monospace font (source has none loaded — add JetBrains Mono or similar only for this
  purpose), radius `12px` to match `.stack div`, padding `15–22px`.
