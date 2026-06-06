# SKILL: Frontend Design — Editorial Craft System
> Derived from `opencode-session-summation-all.html` · Daud's house style

---

## 1. Design Identity

This design system follows an **editorial print aesthetic** — the visual language of a premium field manual, newspaper, or technical journal rendered in the browser. It is not a "tech startup" look. It is not "dark mode SaaS". It is ink on paper, brought to life with purposeful motion and precise typographic structure.

**Core character:**
- Warm parchment/paper backgrounds with genuine texture and noise grain
- A strict tri-family type system (serif display · sans body · monospace utility)
- Ruled lines, double borders, and grid dividers as the primary structural device
- Rust red as the single dominant accent; forest green and mustard as supporting secondaries
- Zero border-radius on cards and containers — hard rectangular cuts only
- Shadow offset boxes (the "lifted paper" card effect) instead of blurred drop shadows
- A persistent light/dark mode toggle with smooth `transition: background 0.4s ease`

---

## 2. Typography System

Use **exactly three font families**. Never substitute or expand this list without strong justification.

| Role | Font | Usage |
|---|---|---|
| Display / Headings | `Fraunces` (variable: opsz, SOFT, WONK) | Hero titles, panel numbers, pull quotes, large numerals |
| Body / UI | `Geist` (variable: wght 300–900) | Body text, paragraphs, navigation, general UI |
| Monospace / Labels | `JetBrains Mono` (variable: wght, ital) | Metadata, labels, code, table headers, masthead, sub-labels |

**Google Fonts import (always include all three):**
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght,SOFT,WONK@9..144,300..900,0..100,0..1&family=Geist:wght@300..900&family=JetBrains+Mono:ital,wght@0,300..700;1,300..700&display=swap" rel="stylesheet">
```

### Fraunces variable axis usage

| Context | `font-variation-settings` | Weight | Style |
|---|---|---|---|
| Hero H1 (large) | `"opsz" 144, "SOFT" 0, "WONK" 0` | 360 | normal |
| Hero H1 italic em | `"opsz" 144, "SOFT" 100, "WONK" 1` | 300 | italic |
| Panel number | `"opsz" 144` | 300 | italic |
| Section title | `"opsz" 144, "SOFT" 100, "WONK" 1` (em) | 380 | mixed |
| Content H2 | `"opsz" 72` | 400 | normal |
| Content H2 em | `"opsz" 72, "SOFT" 100, "WONK" 1` | — | italic |
| Pull quote / lede | `"opsz" 36, "SOFT" 30` | 380 | italic |
| Meta big number | `"opsz" 72` | 400 | — |
| Stat large number | `"opsz" 144` | 300 | italic |

**Rule:** Italic `em` inside headings always uses rust colour + soft/wonky variation axes. This is the single most recognisable typographic fingerprint of this system.

### Type scale

```css
/* Hero */
font-size: clamp(3.5rem, 8vw, 6.5rem);  line-height: 0.88;  letter-spacing: -0.04em;

/* Panel number */
font-size: clamp(5rem, 12vw, 9rem);     line-height: 0.8;

/* Panel title */
font-size: clamp(2rem, 5vw, 3.5rem);   line-height: 0.95;  letter-spacing: -0.025em;

/* Content H2 */
font-size: 1.85rem;                     line-height: 1.1;   letter-spacing: -0.015em;

/* Body */
font-size: 1rem (default);             line-height: 1.55;

/* Mono labels */
font-size: 0.65–0.72rem;               letter-spacing: 0.08–0.2em;  text-transform: uppercase;
```

---

## 3. Colour System

Always declare both light and dark themes via `[data-theme]` on `<html>`. Never hardcode hex values in component styles — reference CSS variables exclusively.

```css
:root {
  /* Backgrounds (warm parchment) */
  --paper:        #f0e7d2;   /* page background */
  --paper-2:      #e7dcc1;   /* card / sidebar / table header */
  --paper-3:      #ddcfac;   /* card hover state */
  --tile:         #ece1c2;   /* subtle tiled surfaces */

  /* Ink (warm near-black) */
  --ink:          #1a140e;   /* primary text, borders, active bg */
  --ink-2:        #3a2f23;   /* secondary text, body copy */
  --muted:        #7a6852;   /* labels, captions, disabled states */

  /* Rules / borders */
  --rule:         #b8a47a;   /* standard border */
  --rule-soft:    #d4c196;   /* light dividers, grid lines */
  --grid-line:    rgba(26, 20, 14, 0.06);  /* background grid */

  /* Accents */
  --rust:         #b8331a;   /* PRIMARY accent: CTAs, em tags, markers, answers */
  --rust-soft:    #e85d3a;   /* code highlights, hover rust */
  --mustard:      #b48020;   /* SECONDARY accent: warnings, answer labels */
  --forest:       #1f4a36;   /* TERTIARY accent: info cards, answer backgrounds */
  --moss:         #5a7048;   /* supporting green */

  /* Named accent series (tab markers, pattern lists) */
  --accent-1:     #b8331a;   /* rust */
  --accent-2:     #1f4a36;   /* forest */
  --accent-3:     #b48020;   /* mustard */
  --accent-4:     #3b2a4a;   /* deep violet */
  --accent-5:     #2c4858;   /* slate blue */

  /* Code blocks */
  --code-bg:      #2a1f12;   /* dark brown, not pure black */
  --code-text:    #f0e7d2;   /* paper colour on dark */
}

[data-theme="dark"] {
  --paper:        #14110b;
  --paper-2:      #1c1810;
  --paper-3:      #25201a;
  --tile:         #1c1810;
  --ink:          #f0e7d2;
  --ink-2:        #d4c5a8;
  --muted:        #9a8a72;
  --rule:         #4a3f2d;
  --rule-soft:    #3a3022;
  --grid-line:    rgba(240, 231, 210, 0.05);
  --rust:         #e85d3a;
  --rust-soft:    #ff7a52;
  --mustard:      #d9a04a;
  --forest:       #6ba888;
  --moss:         #8aa878;
  --accent-1:     #e85d3a;
  --accent-2:     #6ba888;
  --accent-3:     #d9a04a;
  --accent-4:     #9a7ab8;
  --accent-5:     #6ba8c8;
  --code-bg:      #0a0805;
  --code-text:    #d4c5a8;
}
```

**Accent usage rules:**
- `--rust` = interactive, danger, emphasis, primary CTA, `em` text in headings
- `--mustard` = secondary label, answer keys, warning callout borders
- `--forest` = success state, info callout background, answer block background
- `--accent-4/5` = tab markers only; never use as text colour in body copy

---

## 4. Background Texture

Two layers always compose the page background:

### Layer 1 — Blueprint grid
```css
body {
  background: var(--paper);
  background-image:
    linear-gradient(var(--grid-line) 1px, transparent 1px),
    linear-gradient(90deg, var(--grid-line) 1px, transparent 1px);
  background-size: 40px 40px;
}
```

### Layer 2 — Noise/grain overlay (fixed pseudo-element)
```css
body::before {
  content: "";
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 1;
  opacity: 0.35;  /* 0.18 in dark mode */
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='2' stitchTiles='stitch'/%3E%3CfeColorMatrix values='0 0 0 0 0.1 0 0 0 0 0.08 0 0 0 0 0.05 0 0 0 0.4 0'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
}
[data-theme="dark"] body::before { opacity: 0.18; }
```

All content sits above this at `z-index: 2` or higher.

---

## 5. Layout Architecture

### Page wrapper
```css
.page-wrapper {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1.5rem 1.5rem 4rem;
  position: relative;
  z-index: 2;
}
```

### Masthead (newspaper-style header bar)
Three-column grid: `left · center · right`. Always `JetBrains Mono`, `0.7rem`, uppercase, `letter-spacing: 0.08–0.2em`. The center cell carries the publication title in heavy weight; flanking cells carry metadata (volume, date, edition).

```css
.masthead {
  border-top: 4px double var(--ink);    /* double rule = editorial hallmark */
  border-bottom: 1px solid var(--ink);
  padding: 1.25rem 0 1rem;
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: end;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.7rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}
```

### Hero section
Asymmetric two-column grid. Left column (1.2fr) holds the display headline; right column (1fr) holds a lede/tagline with left rust border. Bottom border `1px solid var(--ink)`.

```css
.hero {
  padding: 3rem 0 2rem;
  border-bottom: 1px solid var(--ink);
  display: grid;
  grid-template-columns: 1.2fr 1fr;
  gap: 2.5rem;
  align-items: end;
}
.lede {
  border-left: 3px solid var(--rust);
  padding-left: 1.25rem;
  font-style: italic;
  font-family: 'Fraunces', serif;
}
```

### Meta bar (stat strip)
Flexbox row of equal cells, each with an uppercase mono label above and a value below. Large values use Fraunces display. Cells divide with `border-right: 1px solid var(--rule-soft)`.

```css
.meta-bar {
  display: flex;
  flex-wrap: wrap;
  border-top: 1px solid var(--ink);
  border-bottom: 1px solid var(--ink);
}
.meta-cell {
  flex: 1;
  min-width: 140px;
  padding: 0.85rem 1rem;
  border-right: 1px solid var(--rule-soft);
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.72rem;
  letter-spacing: 0.05em;
}
.meta-cell .label { text-transform: uppercase; color: var(--muted); font-size: 0.65rem; }
.meta-cell .val.big {
  font-family: 'Fraunces', serif;
  font-size: 1.6rem;
  font-weight: 400;
  color: var(--rust);
}
```

### Content layout (sidebar + main)
```css
.layout {
  display: grid;
  grid-template-columns: 200px 1fr;
  gap: 2.5rem;
}
.sidebar {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.72rem;
  text-transform: uppercase;
  position: sticky;
  top: 1.5rem;
  align-self: start;
  color: var(--muted);
}
```

---

## 6. Component Library

### 6.1 Cards

All cards are **zero border-radius**. The signature feature is a **shadow-offset pseudo-element** that creates a "lifted paper" effect.

```css
.card {
  background: var(--paper-2);
  border: 1px solid var(--rule);
  border-radius: 0;
  padding: 1.25rem 1.4rem;
  position: relative;
  transition: all 0.3s ease;
}
.card::before {
  content: "";
  position: absolute;
  top: 6px; left: 6px; right: -6px; bottom: -6px;
  border: 1px solid var(--rule);
  z-index: -1;
  transition: all 0.3s ease;
}
.card:hover { background: var(--paper-3); border-color: var(--ink); }
.card:hover::before { top: 4px; left: 4px; right: -4px; bottom: -4px; }

/* Variants */
.card.warn    { background: rgba(184, 51, 26, 0.08); border-color: var(--rust); }
.card.info    { background: rgba(31, 74, 54, 0.08);  border-color: var(--forest); }
.card.mustard { background: rgba(180, 128, 32, 0.10); border-color: var(--mustard); }
.card.deep    { background: var(--code-bg); color: var(--code-text); border-color: var(--ink); }
```

### 6.2 Question / Content blocks

```css
.qbox {
  border: 1.5px solid var(--ink);
  background: var(--paper);
  padding: 1.25rem 1.4rem;
  position: relative;
}
/* Floating label badge */
.qbox .qno {
  position: absolute;
  top: -14px; left: 20px;
  background: var(--ink);
  color: var(--paper);
  padding: 0.2rem 0.7rem;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.7rem;
  font-weight: 700;
  letter-spacing: 0.15em;
  text-transform: uppercase;
}
/* Answer block */
.qbox .answer {
  background: var(--forest);
  color: var(--paper);
  border-left: 4px solid var(--mustard);
  padding: 0.9rem 1.1rem;
  font-family: 'JetBrains Mono', monospace;
}
.qbox .answer b { color: var(--mustard); }
```

### 6.3 Steps (numbered process)

```css
.step {
  display: grid;
  grid-template-columns: 32px 1fr;
  gap: 0.8rem;
  margin-bottom: 0.7rem;
}
.step .n {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.75rem;
  font-weight: 700;
  color: var(--rust);
  background: var(--paper-2);
  border: 1px solid var(--rule);
  width: 32px; height: 32px;
  display: flex; align-items: center; justify-content: center;
}
```

### 6.4 Inline formula / code token

```css
.formula {
  font-family: 'JetBrains Mono', monospace;
  background: var(--paper-2);
  padding: 0.15rem 0.5rem;
  color: var(--rust);
  border: 1px solid var(--rule);
  font-size: 0.9em;
}
```

### 6.5 Code blocks

```css
pre, .code {
  font-family: 'JetBrains Mono', monospace;
  background: var(--code-bg);
  color: var(--code-text);
  padding: 1rem 1.25rem;
  border-left: 3px solid var(--rust-soft);
  overflow-x: auto;
  font-size: 0.82rem;
  line-height: 1.7;
}
pre .key { color: var(--rust-soft); }  /* keyword highlight */
pre .v   { color: var(--mustard); }    /* value highlight */
```

### 6.6 Tables

```css
table { width: 100%; border-collapse: collapse; font-size: 0.88rem; }
th, td { text-align: left; padding: 0.7rem 0.8rem; border-bottom: 1px solid var(--rule-soft); }
th {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.68rem;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--muted);
  border-bottom: 1.5px solid var(--ink);  /* heavier bottom rule for header */
  background: var(--paper-2);
}
tr:last-child td { border-bottom: none; }
```

### 6.7 Pull quote

```css
.pull-quote {
  border-left: 3px solid var(--rust);
  padding: 0.3rem 0 0.3rem 1.5rem;
  margin: 1.5rem 0;
  font-family: 'Fraunces', serif;
  font-variation-settings: "opsz" 36, "SOFT" 50;
  font-style: italic;
  font-size: 1.15rem;
}
```

### 6.8 Checklist

```css
.checklist { list-style: none; margin-left: 0; }
.checklist li {
  padding: 0.5rem 0 0.5rem 1.8rem;
  position: relative;
  border-bottom: 1px dotted var(--rule);
}
.checklist li::before {
  content: "✕";
  position: absolute; left: 0; top: 0.5rem;
  color: var(--rust);
  font-family: 'JetBrains Mono', monospace;
  font-weight: 700;
}
```

### 6.9 Pattern list (accent-cycled left borders)

```css
.pattern-list { list-style: none; margin-left: 0; }
.pattern-list li {
  padding: 0.65rem 0.9rem;
  margin-bottom: 0.5rem;
  background: var(--paper-2);
  border-left: 3px solid var(--rust);
}
.pattern-list li:nth-child(2) { border-left-color: var(--forest); }
.pattern-list li:nth-child(3) { border-left-color: var(--mustard); }
.pattern-list li:nth-child(4) { border-left-color: var(--accent-4); }
.pattern-list li:nth-child(5) { border-left-color: var(--accent-5); }
.pattern-list li:nth-child(6) { border-left-color: var(--accent-1); }
```

### 6.10 Stat row

```css
.stat-row { display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); border: 1px solid var(--ink); }
.stat { padding: 1rem 1.2rem; border-right: 1px solid var(--rule-soft); }
.stat .n { font-family: 'Fraunces', serif; font-size: 2.2rem; color: var(--rust); font-style: italic; font-weight: 300; }
.stat .l { font-family: 'JetBrains Mono', monospace; font-size: 0.65rem; text-transform: uppercase; letter-spacing: 0.12em; color: var(--muted); }
```

### 6.11 Dimension / feature grid

```css
.dimension-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); border: 1px solid var(--ink); }
.dim { padding: 1rem 1.1rem; border-right: 1px solid var(--rule-soft); border-bottom: 1px solid var(--rule-soft); }
.dim .ltr { font-family: 'Fraunces', serif; font-size: 2.5rem; font-style: italic; color: var(--rust); font-weight: 300; }
```

### 6.12 Sidebar stamp

Rotated, bordered, uppercase text — a postmark-style decorative element.

```css
.stamp {
  padding: 0.8rem;
  border: 2px solid var(--rust);
  color: var(--rust);
  text-align: center;
  transform: rotate(-3deg);
  font-family: 'JetBrains Mono', monospace;
  font-weight: 700;
  font-size: 0.65rem;
  letter-spacing: 0.15em;
}
```

### 6.13 Sigil (inline label badge)

```css
.sigil {
  display: inline-block;
  font-family: 'JetBrains Mono', monospace;
  background: var(--ink);
  color: var(--paper);
  padding: 0.1rem 0.4rem;
  font-size: 0.78em;
  letter-spacing: 0.05em;
}
```

### 6.14 Theme toggle button

Fixed position, circular, offset box-shadow, hover shifts to rust background.

```css
.theme-toggle {
  position: fixed; top: 1rem; right: 1rem; z-index: 100;
  background: var(--paper); color: var(--ink);
  border: 1.5px solid var(--ink);
  width: 44px; height: 44px; border-radius: 50%;
  font-family: 'JetBrains Mono', monospace;
  box-shadow: 2px 2px 0 var(--ink);
  transition: all 0.3s ease;
  cursor: pointer;
}
.theme-toggle:hover { transform: translate(-1px, -1px); box-shadow: 3px 3px 0 var(--ink); background: var(--rust); color: var(--paper); }
.theme-toggle:active { transform: translate(1px, 1px); box-shadow: 1px 1px 0 var(--ink); }
```

---

## 7. Navigation: Tab System

Tabs are rendered as full-width grid buttons, not pills or underline tabs.

```css
.toc { border-top: 1px solid var(--ink); border-bottom: 4px double var(--ink); }
.toc-list { display: grid; grid-template-columns: repeat(5, 1fr); list-style: none; }
.toc-btn {
  width: 100%; background: transparent; border: none;
  padding: 1.25rem 0.75rem 1rem;
  text-align: left; cursor: pointer; color: var(--muted);
  transition: all 0.3s ease; position: relative;
}
.toc-btn:hover { background: var(--paper-2); color: var(--ink); }
.toc-btn.active { background: var(--ink); color: var(--paper); }

/* Chapter number */
.toc-btn .num { font-family: 'JetBrains Mono', monospace; font-size: 0.7rem; font-weight: 700; letter-spacing: 0.15em; }
.toc-btn .num::before { content: "— "; }
.toc-btn .num::after  { content: " —"; }

/* Tab title */
.toc-btn .title { font-family: 'Fraunces', serif; font-size: 1.1rem; line-height: 1.1; }

/* Animated left-border accent marker (unique colour per tab) */
.toc-btn .marker {
  position: absolute; left: 0; top: 0;
  width: 4px; height: 100%;
  transform: scaleY(0); transform-origin: top;
  transition: transform 0.4s cubic-bezier(0.65, 0, 0.35, 1);
}
.toc-btn.active .marker { transform: scaleY(1); }
.toc-btn:nth-child(1) .marker { background: var(--accent-1); }
.toc-btn:nth-child(2) .marker { background: var(--accent-2); }
/* ... continue for each tab */
```

**JavaScript tab switching pattern:**

```javascript
function showTab(id) {
  buttons.forEach(b => b.classList.toggle('active', b.dataset.tab === id));
  panels.forEach(p => p.classList.toggle('active', p.id === 'panel-' + id));
  // Re-trigger stagger animation on new panel's blocks
  const active = document.getElementById('panel-' + id);
  if (active) {
    active.querySelectorAll('.block').forEach((b, i) => {
      b.style.animation = 'none';
      b.offsetHeight; // force reflow
      b.style.animation = '';
      b.style.animationDelay = (i * 0.08) + 's';
    });
    window.scrollTo({ top: document.querySelector('.toc').offsetTop - 20, behavior: 'smooth' });
  }
}
```

---

## 8. Animation Patterns

### Content block stagger (rise-in on load and tab switch)

```css
.block {
  opacity: 0;
  transform: translateY(15px);
  animation: rise 0.6s forwards;
}
.block:nth-child(1) { animation-delay: 0.05s; }
.block:nth-child(2) { animation-delay: 0.15s; }
.block:nth-child(3) { animation-delay: 0.25s; }
/* +0.10s per child up to ~7 */

@keyframes rise {
  to { opacity: 1; transform: translateY(0); }
}
```

### Panel entrance

```css
.panel { animation: panelIn 0.5s cubic-bezier(0.2, 0.7, 0.2, 1); }
@keyframes panelIn {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}
```

### Tab marker animation

`transform: scaleY(0→1)` with `cubic-bezier(0.65, 0, 0.35, 1)` — a smooth deceleration from the top of the tab edge.

### Theme transition

```css
body { transition: background 0.4s ease, color 0.4s ease; }
```

### Theme toggle JavaScript

```javascript
function toggleTheme() {
  const html = document.documentElement;
  const next = html.getAttribute('data-theme') === 'dark' ? 'light' : 'dark';
  html.setAttribute('data-theme', next);
  localStorage.setItem('theme', next);
}
// On load: restore saved preference
(function() {
  const saved = localStorage.getItem('theme') || 'light';
  document.documentElement.setAttribute('data-theme', saved);
})();
```

---

## 9. Heading Hierarchy

Every heading level has a defined font, weight, and `em` colour rule.

| Level | Font | Size | Weight | Em colour |
|---|---|---|---|---|
| `h1` (hero) | Fraunces | clamp(3.5rem, 8vw, 6.5rem) | 360 | `--rust` italic with SOFT/WONK |
| `.panel-title` | Fraunces | clamp(2rem, 5vw, 3.5rem) | 380 | `--rust` italic |
| `h2` in blocks | Fraunces opsz:72 | 1.85rem | 400 | `--rust` italic |
| `h3` in blocks | JetBrains Mono | 0.72rem | 700 | `--rust` (text colour, not em) |
| `h4` in blocks | Fraunces opsz:36 | 1.1rem | 500 | `--ink-2`, italic, no em rule |

**Critical rule:** `em` inside `h1`, `h2`, `.panel-title` is **always rust italic** with high SOFT+WONK variation axes. This is the typographic signature — never override it.

---

## 10. Structural Dividers

```css
/* Double-rule divider (section breaks) */
hr.divider { border: none; border-top: 4px double var(--ink); margin: 3rem 0; }

/* Footer rule (3-col) */
.footer-rule {
  border-top: 1px solid var(--ink);
  padding-top: 1rem;
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.7rem;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--muted);
}
.footer-rule .center { color: var(--rust); font-weight: 700; }
```

Use Unicode ornaments freely in masthead and footer: `◆ · ▌ · — · ◐`

---

## 11. List Styles

```css
ul, ol { margin-left: 1.4rem; margin-bottom: 1rem; }
ul li, ol li { margin-bottom: 0.35rem; color: var(--ink-2); }
/* Ordered list markers use rust mono */
ol li::marker { color: var(--rust); font-family: 'JetBrains Mono', monospace; font-weight: 700; }
```

---

## 12. Responsive Breakpoints

```css
@media (max-width: 900px) {
  .hero       { grid-template-columns: 1fr; gap: 1.5rem; }
  .layout     { grid-template-columns: 1fr; }
  .sidebar    { position: static; margin-bottom: 1.5rem; }
  .toc-list   { grid-template-columns: repeat(2, 1fr); }
  .masthead   { grid-template-columns: 1fr; text-align: center; gap: 0.3rem; }
  .meta-cell  { border-bottom: 1px solid var(--rule-soft); }
}
```

---

## 13. Design Rules — Do and Don't

### ✅ Always do
- Use `clamp()` for all display-size typography
- Use `border: 1px solid var(--ink)` (not `--rule`) for primary structural borders
- Use `4px double var(--ink)` for top masthead and TOC bottom — the double rule is a non-negotiable editorial marker
- Provide `data-theme="light"` on `<html>` as the default and dark as override
- Keep all component backgrounds on `--paper-2` (one step darker than page), never pure white
- Use `box-shadow: 2px 2px 0 var(--ink)` (hard offset, no blur) for interactive elevated elements
- Include the grain pseudo-element on `body::before`
- Apply `scroll-behavior: smooth` and `overflow-x: hidden` on `html` / `body`
- Use `position: sticky; top: 1.5rem; align-self: start` for sidebar context columns

### ❌ Never do
- Never use `border-radius` on cards, tables, code blocks, or structural containers
- Never use `box-shadow` with blur radius for cards — only the hard offset `::before` pseudo approach
- Never use `Inter`, `Roboto`, `Arial`, `system-ui` as primary fonts
- Never hardcode hex colours in component CSS — always `var(--token)`
- Never use purple gradients, glassmorphism, or frosted blur (`backdrop-filter`) — this aesthetic is ink and paper, not glass
- Never centre-align body text
- Never use `font-weight: 900` in Fraunces for display — `300–380` is the editorial weight range
- Never omit the `font-variation-settings` for Fraunces — the axes are load-bearing

---

## 14. HTML Document Shell

```html
<!DOCTYPE html>
<html lang="en" data-theme="light">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght,SOFT,WONK@9..144,300..900,0..100,0..1&family=Geist:wght@300..900&family=JetBrains+Mono:ital,wght@0,300..700;1,300..700&display=swap" rel="stylesheet">
  <style>
    /* 1. CSS variables (light + dark) */
    /* 2. Reset */
    /* 3. Body + grid background + grain pseudo */
    /* 4. Layout: masthead, hero, meta-bar, tabs, panels */
    /* 5. Components */
    /* 6. Animations */
    /* 7. Responsive */
  </style>
</head>
<body>
  <button class="theme-toggle" onclick="toggleTheme()" aria-label="Toggle theme">◐</button>
  <div class="page-wrapper">
    <!-- masthead -->
    <!-- hero -->
    <!-- meta-bar -->
    <!-- tab nav -->
    <!-- panel sections -->
    <!-- footer rule -->
  </div>
  <script>
    /* theme toggle + localStorage */
    /* tab system */
  </script>
</body>
</html>
```

---

## 15. React/JSX Adaptation Notes

When implementing this system in React:

1. **CSS variables** — define in a global `styles/tokens.css` imported at root; add `data-theme` attribute via `document.documentElement.setAttribute` in a `useEffect` on a `ThemeProvider`.
2. **Fraunces variation axes** — pass via inline `style` prop: `style={{ fontVariationSettings: '"opsz" 144, "SOFT" 100, "WONK" 1' }}` or in a CSS class.
3. **Tab system** — maintain `activeTab` in `useState`; trigger block re-animation via a `key` prop change on the panel, causing React to remount and restart CSS animations.
4. **Body grain overlay** — apply via a fixed `<div className="grain-overlay" />` rendered once in the layout root; avoid `body::before` pseudo-elements in CSS Modules.
5. **`clamp()` values** — safe to use directly in Tailwind via arbitrary values: `text-[clamp(3.5rem,8vw,6.5rem)]`.

---

---

## ADDENDUM — Additional Tips from System Frontend Design Skill

> The following section contains supplemental design guidance from the base `frontend-design` skill. It is additional and secondary; the primary source of truth for this design system is Sections 1–15 above.

```
ADDENDUM: General Frontend Design Principles (from system skill)

## Design Thinking Before Coding
Before writing any markup, commit to a BOLD aesthetic direction:
- Purpose: What problem does this interface solve? Who uses it?
- Tone: Pick an extreme — brutally minimal, maximalist chaos, retro-futuristic,
  organic/natural, luxury/refined, playful/toy-like, editorial/magazine (THIS FILE),
  brutalist/raw, art deco/geometric, soft/pastel, industrial/utilitarian, etc.
- Constraints: Technical requirements (framework, performance, accessibility).
- Differentiation: What makes this UNFORGETTABLE?

CRITICAL: Choose a clear conceptual direction and execute it with precision.
Bold maximalism and refined minimalism both work — the key is intentionality.

## Typography
- Choose fonts that are beautiful, unique, and interesting.
- Avoid generic fonts like Arial and Inter.
- Pair a distinctive display font with a refined body font.
- Unexpected, characterful font choices elevate aesthetics.

## Color & Theme
- Commit to a cohesive aesthetic using CSS variables.
- Dominant colors with sharp accents outperform timid, evenly-distributed palettes.
- NEVER converge on common choices (Space Grotesk, purple-on-white, etc.)

## Motion
- Prioritize CSS-only animations for HTML artifacts.
- Use Motion library for React when available.
- One well-orchestrated page load with staggered reveals creates more delight
  than scattered micro-interactions.
- Use scroll-triggering and hover states that surprise.

## Spatial Composition
- Unexpected layouts. Asymmetry. Overlap.
- Grid-breaking elements.
- Generous negative space OR controlled density — pick one.

## Backgrounds & Visual Details
- Create atmosphere and depth rather than defaulting to solid colors.
- Apply: gradient meshes, noise textures, geometric patterns, layered
  transparencies, dramatic shadows, decorative borders, grain overlays.
- Contextual effects that match the overall aesthetic.

## Anti-patterns to NEVER use
- Overused font families: Inter, Roboto, Arial, system-ui as primary
- Clichéd color schemes: purple gradients on white backgrounds
- Predictable layouts and cookie-cutter component patterns
- Glassmorphism / frosted blur when it doesn't fit the aesthetic
- Generic "AI slop" aesthetics — every design should be context-specific

## Implementation
- Match complexity to vision: maximalist designs need elaborate code;
  minimalist designs need restraint, precision, careful spacing.
- Production-grade and functional, not just visually striking.
- Visually cohesive with a clear aesthetic point-of-view.
- Meticulously refined in every detail.
```
