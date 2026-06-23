---
name: frontend-design
description: >
  Deep navy-slate editorial dark UI with electric teal accent, dual-axis variable-font
  typography (Fraunces serif + Geist sans + JetBrains Mono), and a scanline/ambient-glow
  atmosphere. Structural idioms: three-column masthead/footer, asymmetric 1.3fr/1fr hero
  grid, ruled meta strip, diff-colored tabbed sections, and accordion Q&A panels with
  left-border tier accents. Supports a full light/dark theme toggle via data-theme
  attribute. Use for technical prep guides, AI platform dashboards, internal knowledge
  bases, and document-dense single-page applications where editorial precision and
  production-grade feel are required.
---

# VGA Dark-Navy Editorial Prep UI — Design System Skill

## Concept & Aesthetic Direction

This system fuses **editorial print design** (grid-based layout, ruled rules, large
display serif, eyebrow labels, colophon credits) with **engineering terminal aesthetics**
(monospaced metadata, teal glow accents, code tokens, scanline overlays). The result
reads as a high-quality internal field manual or technical publication — not a
consumer app.

**What this is:**
- A dark-first, deeply layered document-style UI with cinematic atmosphere
- Informational density without clutter, achieved via typographic hierarchy
- Tier/category color coding (teal = easy/pass, blue = intermediate, violet = hard,
  amber = other, coral = JD/priority)
- Every interactive surface responds with glow, left-border accent, or background shift

**What this is NOT:**
- Rounded-corner card-grid consumer UI
- Dashboard with heavy chart emphasis
- Marketing landing page with gradients and hero images
- Any UI with more than 4px border-radius anywhere

**Appropriate use contexts:** Interview prep guides, AI platform control panels,
technical knowledge bases, engineering documentation portals, developer-facing SaaS.

---

## Typography

### Import URL (verbatim)
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght,SOFT,WONK@9..144,300..900,0..100,0..1&family=Geist:wght@300..900&family=JetBrains+Mono:ital,wght@0,300..700;1,300..700&display=swap" rel="stylesheet">
```

### Font 1: Fraunces (Variable Serif)
**Role:** Hero display headings, section titles, lede/pull-quote blocks, meta big
numbers, section description subtitles.

**Axis values by context:**

| Context | `font-variation-settings` | `font-weight` | `font-size` | `line-height` | `letter-spacing` |
|---|---|---|---|---|---|
| Hero H1 upright | `"opsz" 144, "SOFT" 0, "WONK" 0` | 300 | `clamp(3rem, 7.2vw, 5.8rem)` | 0.9 | -0.04em |
| Hero H1 italic (teal em) | `"opsz" 144, "SOFT" 80, "WONK" 1` | 300 | (inherits h1) | 0.9 | -0.04em |
| Section title | `"opsz" 72` | 360 | 1.9rem | — | -0.015em |
| Lede / pull-quote | `"opsz" 36, "SOFT" 20` | 360 | 1.08rem | 1.6 | — |
| Section description | `"opsz" 36` | 400 italic | 0.88rem | — | — |
| Meta big number | `"opsz" 72` | 400 italic | 1.9rem | 1 | — |

**Critical:** Fraunces SOFT and WONK axes must be explicitly set per context.
SOFT=80/WONK=1 on italic `em` elements creates the organic ink-brush italic effect
that distinguishes hero text. SOFT=0/WONK=0 on upright keeps it geometric.

### Font 2: Geist (Variable Sans)
**Role:** Body text (default `font-family` on `body`), question text in Q&A items,
meta cell values (regular size), general prose in answer content.

| Context | `font-weight` | `font-size` | `line-height` |
|---|---|---|---|
| Body default | 400 (inherited) | 1rem | 1.55 |
| Q&A question text `.q-text` | 600 | 0.93rem | 1.45 |
| Meta cell `.val` (normal) | 400 | 0.85rem | — |

### Font 3: JetBrains Mono (Variable Monospace)
**Role:** ALL metadata labels, masthead, footer, nav tabs, eyebrow labels,
section labels, theme toggle button, search input, inline code chips, colophon,
question numbers, search icon.

**Decision rule:** Any element that is a label, tag, count, metadata annotation,
navigation control, or code token uses JetBrains Mono. Never use Geist or Fraunces
for these roles.

| Context | `font-size` | `font-weight` | `letter-spacing` | `text-transform` |
|---|---|---|---|---|
| Masthead left/right | 0.68rem | 400 | 0.1em | uppercase |
| Masthead center | 0.78rem | 700 | 0.2em | uppercase |
| Eyebrow (`.eyebrow`) | 0.66rem | 400 | 0.18em | uppercase |
| Section label | 0.65rem | 400 | 0.2em | uppercase |
| Nav tab | 0.69rem | 700 | 0.1em | uppercase |
| Meta cell label | 0.62rem | 400 | 0.18em | uppercase |
| Q number `.q-num` | 0.68rem | 500 | — | — |
| Q arrow `.q-arrow` | 0.65rem | — | — | — |
| Inline `code` | 0.77rem | 400 | — | — |
| Tip/star chip | 0.66rem | 400 | — | — |
| Footer rule | 0.68rem | 400 | 0.12em | uppercase |
| Colophon | 0.62rem | 400 | 0.18em | uppercase |
| Theme toggle | 1rem | — | — | — |
| Search input | 0.82rem | 400 | — | — |

---

## Color System

### Dark Theme `:root` (default)
```css
:root {
  /* Backgrounds — layered depth */
  --paper:        #0b0f18;   /* deepest background, body base */
  --paper-2:      #111827;   /* Q&A question row bg, search input bg */
  --paper-3:      #1a2236;   /* Q&A question hover bg */
  --tile:         #131c2e;   /* (available for card/tile surfaces) */

  /* Text hierarchy */
  --ink:          #e8edf5;   /* primary text, headings, strong elements */
  --ink-2:        #c2cfe0;   /* secondary text, body default, answer content */
  --muted:        #5e7394;   /* metadata, labels, placeholder, q-numbers */

  /* Structural borders */
  --rule:         #1e2e44;   /* standard divider, Q&A borders, grid lines */
  --rule-soft:    #162033;   /* subtle dividers */

  /* Atmosphere */
  --grid-line:    rgba(100,160,255,0.04); /* body background grid */

  /* Primary accent — electric teal */
  --teal:         #00c8a0;   /* primary accent: borders, glows, active states */
  --teal-soft:    #00a880;   /* hover/pressed teal variant */

  /* Secondary accents */
  --blue:         #3b82f6;   /* intermediate difficulty */
  --amber:        #f59e0b;   /* other/behavioral tier, star chip, medium-priority JD */
  --violet:       #8b5cf6;   /* hard difficulty */
  --coral:        #f87171;   /* JD section color, high-priority JD border */

  /* Semantic aliases — difficulty tiers */
  --easy:         #00c8a0;   /* = --teal */
  --intermediate: #3b82f6;   /* = --blue */
  --hard:         #8b5cf6;   /* = --violet */
  --other:        #f59e0b;   /* = --amber */
  --jd-col:       #f87171;   /* = --coral */

  /* Tab active aliases (parallel naming) */
  --accent-1:     #00c8a0;
  --accent-2:     #3b82f6;
  --accent-3:     #f59e0b;
  --accent-4:     #8b5cf6;
  --accent-5:     #f87171;

  /* Code block */
  --code-bg:      #050910;   /* inline code background — near-black */
  --code-text:    #a8d8b8;   /* inline code text — muted sage green */
}
```

### Light Theme Override `[data-theme="light"]`
```css
[data-theme="light"] {
  --paper:        #f4f6fb;
  --paper-2:      #e9edf6;
  --paper-3:      #dee4f0;
  --tile:         #edf0f8;
  --ink:          #0d1424;
  --ink-2:        #1e2d42;
  --muted:        #5a6e8a;
  --rule:         #c8d4e8;
  --rule-soft:    #d8e2f0;
  --grid-line:    rgba(30,60,120,0.05);
  --teal:         #00957a;
  --teal-soft:    #007d66;
  --blue:         #1d4ed8;
  --amber:        #b45309;
  --violet:       #6d28d9;
  --coral:        #dc2626;
  --accent-1:     #00957a;
  --accent-2:     #1d4ed8;
  --accent-3:     #b45309;
  --accent-4:     #6d28d9;
  --accent-5:     #dc2626;
  --code-bg:      #0d1424;   /* code bg stays dark in light mode */
  --code-text:    #a8d8b8;   /* code text unchanged */
  --easy:         #00957a;
  --intermediate: #1d4ed8;
  --hard:         #6d28d9;
  --other:        #b45309;
  --jd-col:       #dc2626;
}
```

### Color Usage Rules
- **Teal** is the single primary accent. All interactive focus rings, active borders,
  CTAs, glow effects, and nav active indicators use `--teal`.
- **Coral/JD** is reserved for urgency/job-description priority markers only.
- **Amber** is secondary emphasis — star badges, medium-priority, behavioral tier.
- **Violet** signals maximum complexity/difficulty.
- **Muted** is the metadata ink — never use for primary content.
- **Code blocks always stay dark** regardless of theme (dark `--code-bg` in both modes).

---

## Background & Atmosphere

### Body — Grid Background
```css
body {
  background: var(--paper);
  background-image:
    linear-gradient(var(--grid-line) 1px, transparent 1px),
    linear-gradient(90deg, var(--grid-line) 1px, transparent 1px);
  background-size: 44px 44px;
  color: var(--ink-2);
  font-family: 'Geist', sans-serif;
  font-size: 1rem;
  line-height: 1.55;
  overflow-x: hidden;
  transition: background 0.4s ease, color 0.4s ease;
}
```

Grid: 44×44px crosshatch using `--grid-line` (rgba near-zero opacity). The grid is
purely atmospheric — it must not interrupt reading.

### body::before — Scanline Overlay
```css
body::before {
  content: "";
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 1;
  opacity: 0.22;
  background: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 2px,
    rgba(0,200,160,0.015) 2px,
    rgba(0,200,160,0.015) 4px
  );
}
```
Light theme override: `[data-theme="light"] body::before { opacity: 0.06; }`

Scanlines are 4px repeating bands — 2px transparent + 2px teal at 0.015 opacity.
The 0.22 global opacity makes this barely perceptible but present.

### body::after — Ambient Glow Corner
```css
body::after {
  content: "";
  position: fixed;
  top: -200px;
  right: -200px;
  width: 600px;
  height: 600px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(0,200,160,0.07) 0%, transparent 70%);
  pointer-events: none;
  z-index: 0;
}
```
Light theme override:
`[data-theme="light"] body::after { background: radial-gradient(circle, rgba(0,149,122,0.06) 0%, transparent 70%); }`

### Z-Index Stacking
```
z-index: 0  → body::after (ambient glow — behind everything)
z-index: 1  → body::before (scanline — sits above content in fixed layer)
z-index: 2  → .page-wrapper (all content)
z-index: 100 → .theme-toggle (fixed UI control above all)
```

---

## Layout

### Page Wrapper
```css
.page-wrapper {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1.5rem 1.5rem 4rem;
  position: relative;
  z-index: 2;
}
```

### Masthead (Three-Column)
```css
.masthead {
  border-top: 1px solid var(--teal);    /* teal top rule — opening brand accent */
  border-bottom: 1px solid var(--rule);
  padding: 1rem 0 0.9rem;
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.68rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--muted);
}
.masthead .left  { text-align: left; }
.masthead .center {
  text-align: center;
  font-weight: 700;
  color: var(--teal);
  font-size: 0.78rem;
  letter-spacing: 0.2em;
  text-shadow: 0 0 8px rgba(0,200,160,0.5);
}
.masthead .right { text-align: right; }
```
The teal `border-top` is the single most distinctive structural mark: it signals the
start of branded content and is echoed by the footer's `border-top`.

### Hero (Asymmetric Two-Column)
```css
.hero {
  padding: 3.5rem 0 2.5rem;
  border-bottom: 1px solid var(--rule);
  display: grid;
  grid-template-columns: 1.3fr 1fr;
  gap: 3rem;
  align-items: end;
}
```
Column ratio is intentionally **not** 50/50 — the 1.3fr left column gives the
display headline more room than the lede. Never use equal columns for this layout.

### Meta Bar (Horizontal Stats Strip)
```css
.meta-bar {
  display: flex;
  flex-wrap: wrap;
  border-top: 1px solid var(--rule);
  border-bottom: 1px solid var(--rule);
  margin-top: 0;
}
.meta-cell {
  flex: 1;
  min-width: 130px;
  padding: 1rem 1.2rem;
  border-right: 1px solid var(--rule);
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.7rem;
  letter-spacing: 0.05em;
}
.meta-cell:last-child { border-right: none; }
```

### Footer (Three-Column Mirror of Masthead)
```css
.footer-rule {
  border-top: 1px solid var(--teal);
  margin-top: 5rem;
  padding-top: 1.2rem;
  padding-bottom: 1.2rem;
  border-bottom: 1px solid var(--rule);
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.68rem;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--muted);
}
.footer-rule .center {
  color: var(--teal);
  font-weight: 700;
  text-align: center;
  text-shadow: 0 0 8px rgba(0,200,160,0.4);
}
.footer-rule .left  { text-align: left; }
.footer-rule .right { text-align: right; }
```

---

## Component: Theme Toggle Button

```css
.theme-toggle {
  position: fixed; top: 1rem; right: 1rem; z-index: 100;
  background: var(--paper-2);
  color: var(--teal);
  border: 1.5px solid var(--teal);
  width: 44px; height: 44px;
  border-radius: 4px;
  font-family: 'JetBrains Mono', monospace;
  font-size: 1rem;
  box-shadow: 0 0 12px rgba(0,200,160,0.2);
  transition: all 0.25s ease;
  cursor: pointer;
}
.theme-toggle:hover {
  background: var(--teal);
  color: var(--paper);
  box-shadow: 0 0 20px rgba(0,200,160,0.4);
}
```
**HTML:** `<button class="theme-toggle" onclick="toggleTheme()" aria-label="Toggle theme">◑</button>`

Symbol: `◑` (Unicode half-circle — references light/dark duality).

---

## Component: Hero Headline

```css
.hero h1 {
  font-family: 'Fraunces', serif;
  font-variation-settings: "opsz" 144, "SOFT" 0, "WONK" 0;
  font-weight: 300;
  font-size: clamp(3rem, 7.2vw, 5.8rem);
  line-height: 0.9;
  letter-spacing: -0.04em;
  color: var(--ink);
}
/* Italic accent span */
.hero h1 em {
  font-style: italic;
  font-variation-settings: "opsz" 144, "SOFT" 80, "WONK" 1;
  font-weight: 300;
  color: var(--teal);
  text-shadow: 0 0 24px rgba(0,200,160,0.35);
}
/* Context label above H1 */
.hero h1 .co-name {
  display: block;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.72rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--muted);
  font-style: normal;
  font-variation-settings: normal;
  margin-bottom: 1.2rem;
}
```

**HTML structure:**
```html
<h1>
  <span class="co-name">// COMPANY · Context Line</span>
  Primary <em>Italic Accent</em><br>Secondary <em>Word</em>
</h1>
```

The `.co-name` pattern is a monospace comment-style label (`// prefix`) placed above
the display headline — it provides context without competing with the headline scale.

---

## Component: Lede / Pull-Quote Block

```css
.lede {
  border-left: 2px solid var(--teal);
  padding-left: 1.4rem;
  font-family: 'Fraunces', serif;
  font-variation-settings: "opsz" 36, "SOFT" 20;
  font-weight: 360;
  font-size: 1.08rem;
  line-height: 1.6;
  color: var(--ink-2);
}
.lede .eyebrow {
  display: block;
  font-family: 'JetBrains Mono', monospace;
  font-style: normal;
  font-size: 0.66rem;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--teal);
  margin-bottom: 0.7rem;
}
.lede em { font-style: italic; color: var(--muted); }
```

**HTML structure:**
```html
<div class="lede">
  <span class="eyebrow">// descriptor · count · topics</span>
  Body text of the pull quote block. <em>Italic muted aside.</em>
</div>
```

The 2px teal left border is the visual anchor. The eyebrow must use JetBrains Mono
with `//` prefix convention.

---

## Component: Meta Cell (Stat Block)

```css
/* Labels */
.meta-cell .label {
  text-transform: uppercase;
  color: var(--muted);
  font-size: 0.62rem;
  letter-spacing: 0.18em;
  display: block;
  margin-bottom: 0.4rem;
  font-family: 'JetBrains Mono', monospace;
}
/* Standard value */
.meta-cell .val {
  font-family: 'Geist', sans-serif;
  font-size: 0.85rem;
  color: var(--ink-2);
}
/* Large numeric value */
.meta-cell .val.big {
  font-family: 'Fraunces', serif;
  font-variation-settings: "opsz" 72;
  font-size: 1.9rem;
  font-weight: 400;
  color: var(--teal);
  font-style: italic;
  line-height: 1;
  display: block;
  text-shadow: 0 0 16px rgba(0,200,160,0.3);
}
```

**HTML structure:**
```html
<div class="meta-cell">
  <span class="label">Category Label</span>
  <span class="val big">42</span>
</div>
<div class="meta-cell">
  <span class="label">Text Value</span>
  <span class="val">Some · Separated · Text</span>
</div>
```

Large numbers use Fraunces italic at `"opsz" 72` with teal glow — this is the
primary data-viz element in the system (no charts needed for counts).

---

## Component: Search Bar

```css
.search-bar {
  margin: 2rem 0 0;
  position: relative;
}
.search-bar input {
  width: 100%;
  background: var(--paper-2);
  border: 1px solid var(--rule);
  border-left: 2px solid var(--teal);      /* teal left accent — signature pattern */
  color: var(--ink-2);
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.82rem;
  padding: 0.9rem 1rem 0.9rem 2.8rem;
  outline: none;
  transition: border-color 0.2s, box-shadow 0.2s;
}
.search-bar input:focus {
  border-color: var(--teal);
  box-shadow: 0 0 0 3px rgba(0,200,160,0.1);
}
.search-bar input::placeholder { color: var(--muted); }
.search-icon {
  position: absolute;
  left: 14px;
  top: 50%;
  transform: translateY(-50%);
  color: var(--teal);
  font-size: 1rem;
  font-family: 'JetBrains Mono', monospace;
}
```

**HTML:**
```html
<div class="search-bar">
  <span class="search-icon">⌕</span>
  <input type="text" id="searchInput" placeholder="Search…" oninput="filterQuestions()">
</div>
```

Icon: `⌕` (Unicode search glass). The 2px teal left border is the resting state
accent — inputs in this system never use a full teal border at rest, only on focus.

---

## Component: Navigation Tabs

```css
.nav-bar {
  display: flex;
  gap: 2px;
  margin: 2rem 0 0;
  border-bottom: 1px solid var(--rule);
  flex-wrap: wrap;
}
.tab-btn {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.69rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  padding: 0.8rem 1.3rem;
  background: transparent;
  border: none;
  border-bottom: 2px solid transparent;
  cursor: pointer;
  color: var(--muted);
  transition: all 0.2s;
  margin-bottom: -1px;        /* overlap nav-bar border-bottom */
}
.tab-btn:hover { color: var(--ink); }

/* Active states — per tier color */
.tab-btn.active-easy         { color: var(--easy);         border-bottom-color: var(--easy); }
.tab-btn.active-intermediate { color: var(--intermediate); border-bottom-color: var(--intermediate); }
.tab-btn.active-hard         { color: var(--hard);         border-bottom-color: var(--hard); }
.tab-btn.active-other        { color: var(--other);        border-bottom-color: var(--other); }
.tab-btn.active-jd           { color: var(--jd-col);       border-bottom-color: var(--jd-col); }
```

The `margin-bottom: -1px` trick makes the active tab's 2px bottom border visually
replace the nav-bar's 1px rule — achieving the underline tab pattern without a gap.

---

## Component: Section Header

```css
.section { display: none; padding-top: 2.5rem; }
.section.active { display: block; }

.section-header { margin-bottom: 2rem; }

/* Ruled eyebrow label with extending line */
.section-label {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  margin-bottom: 0.5rem;
  display: flex;
  align-items: center;
  gap: 0.8rem;
}
.section-label::after {
  content: '';
  flex: 1;
  height: 1px;
  background: var(--rule);
}

/* Section colors override label color per tier */
.easy         .section-label { color: var(--easy); }
.intermediate .section-label { color: var(--intermediate); }
.hard         .section-label { color: var(--hard); }
.other        .section-label { color: var(--other); }
.jd           .section-label { color: var(--jd-col); }

.section-title {
  font-family: 'Fraunces', serif;
  font-variation-settings: "opsz" 72;
  font-size: 1.9rem;
  font-weight: 360;
  color: var(--ink);
  letter-spacing: -0.015em;
}
.section-desc {
  font-size: 0.88rem;
  color: var(--muted);
  margin-top: 0.35rem;
  font-style: italic;
  font-family: 'Fraunces', serif;
  font-variation-settings: "opsz" 36;
}
```

The `::after` extending ruled line is a signature pattern — the label text anchors
the left, the rule extends to fill the remaining width.

---

## Component: Accordion Q&A Items

```css
.qa-list { display: flex; flex-direction: column; gap: 0; }

/* Item container */
.qa-item {
  border: 1px solid var(--rule);
  border-top: none;
  overflow: hidden;
  transition: border-color 0.2s;
  animation: panelIn 0.28s ease both;
}
.qa-item:first-child { border-top: 1px solid var(--rule); }
.qa-item:hover { border-color: var(--muted); }

/* Left-border accent on hover per tier */
.qa-item.easy:hover         { border-left: 2px solid var(--easy); }
.qa-item.intermediate:hover { border-left: 2px solid var(--intermediate); }
.qa-item.hard:hover         { border-left: 2px solid var(--hard); }
.qa-item.other:hover        { border-left: 2px solid var(--other); }

/* Question row (clickable header) */
.qa-question {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  padding: 1.1rem 1.4rem;
  cursor: pointer;
  background: var(--paper-2);
  transition: background 0.15s;
  user-select: none;
}
.qa-question:hover { background: var(--paper-3); }

/* Question number */
.q-num {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.68rem;
  font-weight: 500;
  min-width: 28px;
  padding-top: 2px;
  color: var(--muted);
}
/* Question text */
.q-text {
  flex: 1;
  font-family: 'Geist', sans-serif;
  font-size: 0.93rem;
  font-weight: 600;
  color: var(--ink);
  line-height: 1.45;
}
/* Expand arrow */
.q-arrow {
  font-size: 0.65rem;
  color: var(--muted);
  padding-top: 4px;
  transition: transform 0.25s;
  min-width: 16px;
}
.qa-item.open .q-arrow { transform: rotate(180deg); }

/* Answer panel */
.qa-answer {
  display: none;
  padding: 0 1.4rem 1.4rem 3.6rem;
  background: var(--paper);
  border-top: 1px solid var(--rule);
}
.qa-item.open .qa-answer { display: block; }

/* Answer body text */
.answer-content {
  padding-top: 1.2rem;
  font-size: 0.9rem;
  line-height: 1.72;
  color: var(--ink-2);
}
.answer-content p          { margin-bottom: 0.85rem; }
.answer-content p:last-child { margin-bottom: 0; }
.answer-content strong     { color: var(--ink); font-weight: 600; }
.answer-content em         { font-style: italic; color: var(--muted); }
.answer-content code {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.77rem;
  background: var(--code-bg);
  border: 1px solid var(--rule);
  padding: 1px 6px;
  color: var(--teal);
}
.answer-content ul         { margin-top: 0.6rem; padding-left: 1.5rem; }
.answer-content li         { margin-bottom: 0.4rem; }
```

**Accordion behavior:** Single-open (opening a new item closes any currently open
item within the same list). Arrow rotates 180° on open.

**HTML structure:**
```html
<div class="qa-list">
  <div class="qa-item easy" onclick="toggleItem(this)">
    <div class="qa-question">
      <span class="q-num">01</span>
      <span class="q-text">Question text here</span>
      <span class="q-arrow">▼</span>
    </div>
    <div class="qa-answer">
      <div class="answer-content">
        <p>Answer paragraph.</p>
        <p>Another paragraph with <strong>emphasis</strong> and <code>code token</code>.</p>
      </div>
    </div>
  </div>
</div>
```

---

## Component: Chips / Badges

### Tip Chip (teal — interview/usage tips)
```css
.tip-chip {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.66rem;
  padding: 3px 10px;
  margin-top: 0.9rem;
  border: 1px solid var(--teal);
  color: var(--teal);
  background: rgba(0,200,160,0.05);
  /* border-radius: 0 — sharp corners, NO rounding */
}
```
**HTML:** `<div class="tip-chip">✓ Tip text · constraint · action</div>`

### Star Chip (amber — STAR method / priority)
```css
.star-chip {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.66rem;
  padding: 3px 10px;
  margin-top: 0.9rem;
  margin-left: 6px;
  border: 1px solid var(--amber);
  color: var(--amber);
  background: rgba(245,158,11,0.05);
}
```
**HTML:** `<div class="star-chip">★ STAR: Situation · Task · Action</div>`

### JD Priority Borders (job-description items only)
```css
.qa-item.job-description.high-priority   { border-left: 3px solid var(--jd-col); }
.qa-item.job-description.medium-priority { border-left: 3px solid var(--amber); }
.qa-item.job-description.low-priority    { border-left: 3px solid var(--teal); }
```

---

## Component: Colophon

```css
.colophon {
  text-align: center;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.62rem;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--muted);
  margin-top: 1.2rem;
}
```
**HTML:** `<p class="colophon">Set in Fraunces · Geist · JetBrains Mono · Deep Navy · 2026</p>`

The colophon is a mandatory closing element — it credits the typographic system,
mirrors editorial book design, and closes the document cleanly.

---

## Animations & Motion

### `@keyframes rise` — Page-load entrance for major blocks
```css
@keyframes rise {
  to { opacity: 1; transform: translateY(0); }
}
.block {
  opacity: 0;
  transform: translateY(15px);
  animation: rise 0.55s forwards;
}
/* Staggered delays per child order */
.block:nth-child(2) { animation-delay: 0.08s; }
.block:nth-child(3) { animation-delay: 0.16s; }
.block:nth-child(4) { animation-delay: 0.24s; }
.block:nth-child(5) { animation-delay: 0.32s; }
.block:nth-child(6) { animation-delay: 0.40s; }
.block:nth-child(7) { animation-delay: 0.48s; }
```
Apply `.block` class to: masthead, hero, meta-bar, search-bar, nav-bar, and the
colophon. Each block rises 15px upward from its start position and fades in.
Stagger increment: 0.08s per child.

### `@keyframes panelIn` — Q&A item entrance
```css
@keyframes panelIn {
  from { opacity: 0; transform: translateY(14px); }
  to   { opacity: 1; transform: translateY(0); }
}
.qa-item { animation: panelIn 0.28s ease both; }
```
Applied to every `.qa-item` — triggers on section display, creating a cascade effect
as items render.

### Transitions per component
| Component | Property | Duration | Easing |
|---|---|---|---|
| `body` | `background`, `color` | 0.4s | ease |
| `.theme-toggle` | all | 0.25s | ease |
| `.qa-item` | `border-color` | 0.2s | — |
| `.qa-question` | `background` | 0.15s | — |
| `.q-arrow` | `transform` | 0.25s | — |
| `.tab-btn` | all | 0.2s | — |
| `.search-bar input` | `border-color`, `box-shadow` | 0.2s | — |

---

## Responsive Breakpoints

### `@media (max-width: 860px)`
```css
@media (max-width: 860px) {
  .hero               { grid-template-columns: 1fr; gap: 2rem; }
  .masthead           { grid-template-columns: 1fr; text-align: center; gap: 0.35rem; }
  .masthead .right,
  .masthead .left     { text-align: center; }
  .meta-bar           { flex-direction: column; }
  .meta-cell          { border-right: none; border-bottom: 1px solid var(--rule); }
  .qa-answer          { padding-left: 1.4rem; }
  .nav-bar            { gap: 1px; }
  .tab-btn            { padding: 0.65rem 0.9rem; font-size: 0.62rem; }
  .footer-rule        { grid-template-columns: 1fr; text-align: center; gap: 0.5rem; }
  .footer-rule .right,
  .footer-rule .left  { text-align: center; }
}
```

Hero collapses to single column. Masthead and footer collapse to stacked centered
columns. Meta cells stack vertically with bottom borders replacing right borders.
Tab font shrinks slightly; answer padding reduces to match body margin.

---

## Print Styles

```css
@media print {
  body             { background: #fff !important; color: #000 !important; }
  body::before,
  body::after      { display: none; }
  .qa-answer       { display: block !important; }  /* expand all answers */
  .q-arrow         { display: none; }
  .theme-toggle    { display: none; }
  .block           { opacity: 1; transform: none; animation: none; }
  .nav-bar         { display: none; }
  .section         { display: block !important; }  /* show all sections */
}
```

---

## JavaScript Behaviors

### Theme Toggle
```javascript
function toggleTheme() {
  const html = document.documentElement;
  const next = html.getAttribute('data-theme') === 'dark' ? 'light' : 'dark';
  html.setAttribute('data-theme', next);
  localStorage.setItem('theme', next);
}
// Init from localStorage on page load
(function() {
  const saved = localStorage.getItem('theme') || 'dark';
  document.documentElement.setAttribute('data-theme', saved);
})();
```
- **Mechanism:** Toggles `data-theme` attribute on `<html>` element
- **Persistence:** `localStorage` key `'theme'`
- **Default:** `'dark'`
- **HTML default:** `<html lang="en" data-theme="dark">`

### Tab Switching
```javascript
function showTab(id, btn) {
  document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
  document.querySelectorAll('.tab-btn').forEach(b => {
    b.classList.remove('active-easy','active-intermediate','active-hard','active-other','active-jd');
  });
  document.getElementById('sec-' + id).classList.add('active');
  btn.classList.add('active-' + id);
  const q = document.getElementById('searchInput').value;
  if (q) filterQuestions();
}
```
- **Section IDs:** `sec-easy`, `sec-intermediate`, `sec-hard`, `sec-other`, `sec-jd`
- **Active class pattern:** `active-{id}` on the button (drives tier-colored underline)
- **Search persistence:** If search input has content, re-runs filter on tab switch

### Q&A Accordion (Single-Open)
```javascript
function toggleItem(el) {
  const wasOpen = el.classList.contains('open');
  el.parentElement.querySelectorAll('.qa-item.open').forEach(i => i.classList.remove('open'));
  if (!wasOpen) el.classList.add('open');
}
```
Single-open within each `.qa-list`. Clicking an open item closes it (toggle).

### Cross-Section Search/Filter
```javascript
function filterQuestions() {
  const q = document.getElementById('searchInput').value.toLowerCase().trim();
  const allItems = document.querySelectorAll('.qa-item');
  if (!q) { allItems.forEach(item => item.style.display = ''); return; }
  const sections = ['easy','intermediate','hard','other','jd'];
  sections.forEach(sec => {
    const secEl = document.getElementById('sec-' + sec);
    let hasHit = false;
    secEl.querySelectorAll('.qa-item').forEach(item => {
      const text = item.textContent.toLowerCase();
      if (text.includes(q)) { item.style.display = ''; hasHit = true; }
      else { item.style.display = 'none'; }
    });
    if (hasHit) secEl.classList.add('active');
  });
  sections.forEach(sec => {
    const secEl = document.getElementById('sec-' + sec);
    const hasVisible = [...secEl.querySelectorAll('.qa-item')].some(i => i.style.display !== 'none');
    if (!hasVisible) secEl.classList.remove('active');
    else secEl.classList.add('active');
  });
}
```
- **Scope:** All `.qa-item` elements across all sections
- **Matching:** `textContent.toLowerCase().includes(query)` (full-text match)
- **Section visibility:** Sections with matching items become active; empty sections hide

---

## Unicode Symbols Used

| Symbol | Context |
|---|---|
| `◈` | Masthead/footer center decoration (diamond with dot) |
| `◑` | Theme toggle button (half-filled circle) |
| `▼` | Q&A expand arrow (rotates 180° when open) |
| `⌕` | Search icon (loupe/magnifier) |
| `✓` | Tip chip prefix |
| `★` | Star chip / STAR method prefix |
| `//` | co-name prefix and eyebrow label prefix (text, not Unicode) |
| `·` | Separator in metadata strings (middle dot) |

---

## Design Rules — Do & Don't

### DO
- **Always** place `border-top: 1px solid var(--teal)` on the masthead — this teal
  top rule is the most important brand mark in the system.
- **Always** echo the masthead's teal top border on the footer (`border-top: 1px solid var(--teal)`).
- **Always** use `border-radius: 0` or `border-radius: 4px` maximum. The theme toggle
  button at 4px is the only rounded element. Everything else is sharp.
- **Always** apply the `.block` animation class to major structural sections for
  staggered page-load entrance.
- **Always** prefix eyebrow labels and co-name lines with `//` in the text content.
- **Always** use JetBrains Mono for any label, metadata, badge, chip, or control.
- **Always** apply `text-shadow: 0 0 Xpx rgba(0,200,160,Y)` to teal text that is
  bold or displayed at heading scale (masthead center, footer center, meta big numbers,
  hero italic em).
- **Always** use the 1.3fr/1fr asymmetric column ratio for the hero split. Never 50/50.
- **Always** include the `::after` extending rule on `.section-label` (the horizontal
  line that fills remaining width after the label text).
- **Always** include a colophon at the bottom crediting the font stack.
- **Always** use `clamp(3rem, 7.2vw, 5.8rem)` for the hero H1 — fluid scaling is
  required, fixed px values are wrong.
- **Always** set `font-variation-settings` explicitly on every Fraunces usage —
  the browser defaults are not this system's defaults.

### DON'T
- **Never** use `border-radius` > 4px anywhere.
- **Never** use Geist for labels, badges, tabs, or metadata — those are JetBrains
  Mono only.
- **Never** use Fraunces for navigation, tabs, or code-adjacent text.
- **Never** apply teal glow (`text-shadow`) to body text — only to bold/display
  elements and the masthead/footer center.
- **Never** use equal columns in the hero grid.
- **Never** omit the `font-variation-settings` on Fraunces (no bare `font-family:
  'Fraunces', serif` without axis values).
- **Never** use `box-shadow` with colored spread for general cards — only the theme
  toggle and search focus use glow shadows in this system.
- **Never** put rounded pill badges — chips are always sharp-cornered rectangles.
- **Never** use a colored background for body text sections — answer panels use
  `var(--paper)` (darkest), question rows use `var(--paper-2)`, hover uses
  `var(--paper-3)`. The depth order must be preserved.
- **Never** omit `pointer-events: none` on `body::before` and `body::after` — the
  atmospheric layers must never intercept clicks.
- **Never** use a navbar with visible background fill — tabs are transparent with only
  a bottom-border active indicator.

---

## Composing a New Application in This System

### Full Page Scaffold

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>APP · Section — Application Name</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght,SOFT,WONK@9..144,300..900,0..100,0..1&family=Geist:wght@300..900&family=JetBrains+Mono:ital,wght@0,300..700;1,300..700&display=swap" rel="stylesheet">
<style>
  /* === PASTE FULL :root AND [data-theme="light"] BLOCKS HERE === */
  /* === PASTE ALL COMPONENT CSS HERE === */
  /* === PASTE @keyframes rise AND panelIn HERE === */
  /* === PASTE RESPONSIVE AND PRINT MEDIA QUERIES HERE === */
</style>
</head>
<body>

<!-- FIXED THEME TOGGLE -->
<button class="theme-toggle" onclick="toggleTheme()" aria-label="Toggle theme">◑</button>

<div class="page-wrapper">

  <!-- MASTHEAD -->
  <div class="masthead block">
    <span class="left">Context · Location · Type</span>
    <span class="center">◈ APP NAME · DESCRIPTOR · YEAR ◈</span>
    <span class="right">Month YEAR · Edition</span>
  </div>

  <!-- HERO -->
  <section class="hero block">
    <h1>
      <span class="co-name">// Organization · Context</span>
      Primary <em>Heading</em><br>Secondary <em>Word</em>
    </h1>
    <div class="lede">
      <span class="eyebrow">// descriptor · count · key topics</span>
      Lede paragraph text. Production-grade context sentence. Key technical anchors.
    </div>
  </section>

  <!-- META BAR -->
  <div class="meta-bar block">
    <div class="meta-cell">
      <span class="label">Metric Label</span>
      <span class="val big">42</span>
    </div>
    <div class="meta-cell">
      <span class="label">Text Stat</span>
      <span class="val">Value · Sub-value</span>
    </div>
    <!-- repeat meta-cell as needed -->
  </div>

  <!-- SEARCH (if filterable content) -->
  <div class="search-bar block">
    <span class="search-icon">⌕</span>
    <input type="text" id="searchInput" placeholder="Search…" oninput="filterQuestions()">
  </div>

  <!-- NAV TABS -->
  <div class="nav-bar block">
    <button class="tab-btn active-easy" onclick="showTab('tab1', this)">Tab One · 1–20</button>
    <button class="tab-btn" onclick="showTab('tab2', this)">Tab Two · 21–40</button>
    <button class="tab-btn" onclick="showTab('tab3', this)">Tab Three</button>
  </div>

  <!-- SECTION 1 -->
  <div class="section easy active" id="sec-tab1">
    <div class="section-header">
      <div class="section-label">Tier 1 · Items 01–20</div>
      <div class="section-title">Section Heading</div>
      <div class="section-desc">Brief italic description of this section's purpose.</div>
    </div>
    <div class="qa-list" id="list-tab1">
      <div class="qa-item easy" onclick="toggleItem(this)">
        <div class="qa-question">
          <span class="q-num">01</span>
          <span class="q-text">Question or item title</span>
          <span class="q-arrow">▼</span>
        </div>
        <div class="qa-answer">
          <div class="answer-content">
            <p>Answer content. Use <strong>bold</strong> for key terms, <code>code</code> for tokens.</p>
            <div class="tip-chip">✓ Tip or constraint</div>
            <div class="star-chip">★ STAR / priority note</div>
          </div>
        </div>
      </div>
      <!-- repeat qa-item -->
    </div>
  </div>

  <!-- SECTION 2 -->
  <div class="section intermediate" id="sec-tab2">
    <!-- same structure, class="section intermediate" -->
  </div>

  <!-- FOOTER -->
  <div class="footer-rule block">
    <span class="left">App Name · Context</span>
    <span class="center">End of Document</span>
    <span class="right">Built by Name · Year</span>
  </div>
  <p class="colophon block">Set in Fraunces · Geist · JetBrains Mono · Deep Navy · 2026</p>

</div><!-- /page-wrapper -->

<script>
  function toggleTheme() {
    const html = document.documentElement;
    const next = html.getAttribute('data-theme') === 'dark' ? 'light' : 'dark';
    html.setAttribute('data-theme', next);
    localStorage.setItem('theme', next);
  }
  (function() {
    const saved = localStorage.getItem('theme') || 'dark';
    document.documentElement.setAttribute('data-theme', saved);
  })();

  function showTab(id, btn) {
    document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
    document.querySelectorAll('.tab-btn').forEach(b => {
      b.classList.remove('active-easy','active-intermediate','active-hard','active-other','active-jd');
    });
    document.getElementById('sec-' + id).classList.add('active');
    btn.classList.add('active-' + id);
    const q = document.getElementById('searchInput').value;
    if (q) filterQuestions();
  }

  function toggleItem(el) {
    const wasOpen = el.classList.contains('open');
    el.parentElement.querySelectorAll('.qa-item.open').forEach(i => i.classList.remove('open'));
    if (!wasOpen) el.classList.add('open');
  }

  function filterQuestions() {
    const q = document.getElementById('searchInput').value.toLowerCase().trim();
    const allItems = document.querySelectorAll('.qa-item');
    if (!q) { allItems.forEach(item => item.style.display = ''); return; }
    const sections = ['tab1','tab2','tab3']; // update with your section IDs
    sections.forEach(sec => {
      const secEl = document.getElementById('sec-' + sec);
      let hasHit = false;
      secEl.querySelectorAll('.qa-item').forEach(item => {
        const text = item.textContent.toLowerCase();
        if (text.includes(q)) { item.style.display = ''; hasHit = true; }
        else { item.style.display = 'none'; }
      });
      if (hasHit) secEl.classList.add('active');
    });
    sections.forEach(sec => {
      const secEl = document.getElementById('sec-' + sec);
      const hasVisible = [...secEl.querySelectorAll('.qa-item')].some(i => i.style.display !== 'none');
      if (!hasVisible) secEl.classList.remove('active');
      else secEl.classList.add('active');
    });
  }
</script>
</body>
</html>
```

### Adapting Components for Other Content Types

**Data table:** Use `.meta-bar` layout with more cells, or build a `<table>` with
`font-family: 'JetBrains Mono'`, `border: 1px solid var(--rule)`, `background:
var(--paper-2)` on `<thead>`, and `color: var(--muted)` for column headers.

**Buttons (CTA):** Use the theme-toggle pattern — `background: var(--paper-2)`,
`border: 1.5px solid var(--teal)`, `color: var(--teal)`, hover inverts to
`background: var(--teal)`, `color: var(--paper)`, glow on hover.

**Form inputs:** Follow search-bar pattern — `border-left: 2px solid var(--teal)` at
rest, full `border-color: var(--teal)` and `box-shadow: 0 0 0 3px rgba(0,200,160,0.1)`
on focus, `font-family: 'JetBrains Mono'`.

**Progress/status bar:** Use a `<div>` with `height: 2px`, `background: var(--rule)`,
inner `<div>` with `background: var(--teal)` and `box-shadow: 0 0 8px rgba(0,200,160,0.4)`.

**Code block (multi-line):** `background: var(--code-bg)`, `border: 1px solid
var(--rule)`, `font-family: 'JetBrains Mono'`, `font-size: 0.82rem`, `color:
var(--code-text)` (`#a8d8b8`), `padding: 1rem 1.2rem`, border-radius: 0.

**Badges/tags (non-chip):** `display: inline-block`, `font-family: 'JetBrains Mono'`,
`font-size: 0.62rem`, `letter-spacing: 0.12em`, `text-transform: uppercase`,
`padding: 2px 8px`, `border: 1px solid [tier-color]`, `color: [tier-color]`,
`background: rgba([tier-rgb], 0.05)`, border-radius: 0.

**Section dividers:** `border-top: 1px solid var(--rule)` with a `.section-label`
pattern (JetBrains Mono uppercase + `::after` extending line).

**Notification/alert:** Same as `.tip-chip` but full-width — `display: flex`,
`padding: 0.75rem 1rem`, left border 2px solid tier color, `background: rgba(tier, 0.05)`.
