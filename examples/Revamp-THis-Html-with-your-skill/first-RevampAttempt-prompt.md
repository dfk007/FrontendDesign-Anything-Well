Using this pasted Skill.md frontend-design skill :
---Frontend-Design Skill.md Starts here---
# SKILL: Frontend Design — Editorial Craft System

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
---Frontend-Design Skill.md Ends here---


Your TASK: Update following  html of a Webpage with the Frontend-Design Skill.md pasted above, and give me its full updated html code with new design: 


---HTML page whose design to starts here---
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>DevOps → AI DevOps Engineer Roadmap</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #070b12;
    --surface: #0d1420;
    --border: #1a2540;
    --accent: #00e5ff;
    --accent2: #7b61ff;
    --accent3: #39ff9a;
    --warn: #ff6b35;
    --text: #d8e3f0;
    --muted: #5a7090;
    --font-head: 'Syne', sans-serif;
    --font-mono: 'DM Mono', monospace;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-mono);
    font-size: 13px;
    line-height: 1.7;
    overflow-x: hidden;
  }

  /* BACKGROUND GRID */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(0,229,255,0.025) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,229,255,0.025) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
  }

  .wrap {
    max-width: 1080px;
    margin: 0 auto;
    padding: 0 24px 80px;
    position: relative;
    z-index: 1;
  }

  /* ─── HEADER ─────────────────────────────────────────── */
  header {
    padding: 64px 0 48px;
    border-bottom: 1px solid var(--border);
    margin-bottom: 56px;
    position: relative;
  }

  .eyebrow {
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 0.18em;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 16px;
    opacity: 0;
    animation: fadeUp 0.5s 0.1s forwards;
  }

  h1 {
    font-family: var(--font-head);
    font-size: clamp(32px, 5vw, 58px);
    font-weight: 800;
    line-height: 1.05;
    letter-spacing: -0.02em;
    color: #fff;
    opacity: 0;
    animation: fadeUp 0.5s 0.2s forwards;
  }

  h1 span.hl {
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .subtitle {
    margin-top: 20px;
    max-width: 620px;
    color: var(--muted);
    font-size: 13px;
    opacity: 0;
    animation: fadeUp 0.5s 0.3s forwards;
  }

  .meta-pills {
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
    margin-top: 28px;
    opacity: 0;
    animation: fadeUp 0.5s 0.4s forwards;
  }

  .pill {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 5px 14px;
    border-radius: 2px;
    font-size: 11px;
    letter-spacing: 0.08em;
    border: 1px solid;
  }
  .pill.cyan  { border-color: var(--accent);  color: var(--accent); }
  .pill.purple{ border-color: var(--accent2); color: var(--accent2);}
  .pill.green { border-color: var(--accent3); color: var(--accent3);}
  .pill.orange{ border-color: var(--warn);    color: var(--warn);   }

  /* ─── PROGRESS BAR ───────────────────────────────────── */
  .progress-bar {
    display: flex;
    gap: 3px;
    margin-bottom: 52px;
    opacity: 0;
    animation: fadeUp 0.5s 0.5s forwards;
  }

  .progress-bar .seg {
    height: 3px;
    flex: 1;
    border-radius: 2px;
    background: var(--border);
    transition: background 0.3s;
    cursor: pointer;
  }

  .progress-bar .seg.active { background: var(--accent); }
  .progress-bar .seg:hover { background: var(--accent2); }

  /* ─── SECTION TITLE ──────────────────────────────────── */
  .section-title {
    font-family: var(--font-head);
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 28px;
    padding-bottom: 10px;
    border-bottom: 1px solid var(--border);
  }

  /* ─── STEP CARD ──────────────────────────────────────── */
  .steps { display: flex; flex-direction: column; gap: 2px; }

  .step {
    background: var(--surface);
    border: 1px solid var(--border);
    border-left: 3px solid var(--border);
    padding: 28px 32px;
    cursor: pointer;
    transition: border-color 0.2s, background 0.2s, transform 0.15s;
    opacity: 0;
    position: relative;
    overflow: hidden;
  }

  .step::after {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background: linear-gradient(135deg, transparent 70%, rgba(0,229,255,0.03));
    pointer-events: none;
  }

  .step:hover {
    border-left-color: var(--accent);
    background: #0f1928;
    transform: translateX(4px);
  }

  .step.open {
    border-left-color: var(--accent);
    background: #0f1928;
  }

  .step-header {
    display: flex;
    align-items: center;
    gap: 18px;
  }

  .step-num {
    font-family: var(--font-head);
    font-size: 28px;
    font-weight: 800;
    color: var(--border);
    min-width: 42px;
    line-height: 1;
    transition: color 0.2s;
  }

  .step:hover .step-num,
  .step.open .step-num { color: var(--accent); }

  .step-meta { flex: 1; }

  .step-tag {
    font-size: 10px;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    margin-bottom: 4px;
    font-family: var(--font-mono);
  }

  .step-name {
    font-family: var(--font-head);
    font-size: 18px;
    font-weight: 700;
    color: #fff;
    letter-spacing: -0.01em;
    line-height: 1.2;
  }

  .step-chevron {
    font-size: 18px;
    color: var(--muted);
    transition: transform 0.25s, color 0.2s;
  }

  .step.open .step-chevron { transform: rotate(90deg); color: var(--accent); }

  .step-body {
    display: none;
    padding-top: 24px;
    margin-top: 24px;
    border-top: 1px solid var(--border);
    grid-template-columns: 1fr 1fr;
    gap: 20px;
  }

  .step.open .step-body { display: grid; }

  /* responsive */
  @media(max-width: 640px) {
    .step-body { grid-template-columns: 1fr; }
  }

  .col-label {
    font-size: 10px;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 10px;
    font-family: var(--font-mono);
  }

  .step-desc {
    color: #8fa8c8;
    font-size: 13px;
    line-height: 1.75;
    grid-column: 1 / -1;
    margin-bottom: 4px;
  }

  /* tools list */
  .tools { display: flex; flex-wrap: wrap; gap: 7px; }

  .tool {
    display: inline-block;
    padding: 3px 10px;
    background: rgba(0,229,255,0.07);
    border: 1px solid rgba(0,229,255,0.15);
    border-radius: 2px;
    font-size: 11px;
    color: var(--accent);
    font-family: var(--font-mono);
    transition: background 0.15s;
  }

  .tool:hover { background: rgba(0,229,255,0.14); }
  .tool.purple { background: rgba(123,97,255,0.08); border-color: rgba(123,97,255,0.2); color: var(--accent2); }
  .tool.green  { background: rgba(57,255,154,0.07); border-color: rgba(57,255,154,0.18); color: var(--accent3); }
  .tool.orange { background: rgba(255,107,53,0.07); border-color: rgba(255,107,53,0.18); color: var(--warn); }

  /* snippet block */
  .snippet {
    background: #070b12;
    border: 1px solid var(--border);
    border-radius: 2px;
    padding: 14px 16px;
    font-size: 11.5px;
    font-family: var(--font-mono);
    color: #8cb4d4;
    overflow-x: auto;
    white-space: pre;
    line-height: 1.6;
    grid-column: 1 / -1;
    position: relative;
  }

  .snippet .kw  { color: var(--accent); }
  .snippet .cm  { color: var(--muted); font-style: italic; }
  .snippet .str { color: var(--accent3); }
  .snippet .fn  { color: var(--accent2); }
  .snippet .snip-label {
    position: absolute;
    top: 8px; right: 12px;
    font-size: 10px;
    color: var(--muted);
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }

  /* outcome chips */
  .outcomes { display: flex; flex-wrap: wrap; gap: 8px; }

  .outcome {
    display: inline-flex;
    align-items: center;
    gap: 5px;
    padding: 4px 12px;
    background: rgba(57,255,154,0.06);
    border: 1px solid rgba(57,255,154,0.15);
    border-radius: 2px;
    font-size: 11px;
    color: var(--accent3);
  }

  .outcome::before { content: '✓'; }

  /* timeline indicator */
  .timeline-badge {
    display: inline-flex;
    align-items: center;
    gap: 5px;
    padding: 3px 10px;
    background: rgba(123,97,255,0.1);
    border: 1px solid rgba(123,97,255,0.2);
    border-radius: 2px;
    font-size: 11px;
    color: var(--accent2);
    font-family: var(--font-mono);
    margin-bottom: 12px;
  }

  /* ─── PHASE DIVIDER ──────────────────────────────────── */
  .phase-divider {
    display: flex;
    align-items: center;
    gap: 14px;
    margin: 40px 0 8px;
    opacity: 0;
    animation: fadeUp 0.4s forwards;
  }

  .phase-label {
    font-family: var(--font-head);
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    white-space: nowrap;
    padding: 4px 14px;
    border-radius: 2px;
  }

  .phase-line { flex: 1; height: 1px; background: var(--border); }

  .phase-label.p1 { color: var(--accent);  background: rgba(0,229,255,0.07);  border: 1px solid rgba(0,229,255,0.15); }
  .phase-label.p2 { color: var(--accent2); background: rgba(123,97,255,0.07); border: 1px solid rgba(123,97,255,0.15); }
  .phase-label.p3 { color: var(--accent3); background: rgba(57,255,154,0.07); border: 1px solid rgba(57,255,154,0.15); }

  /* ─── FOOTER ─────────────────────────────────────────── */
  footer {
    margin-top: 72px;
    padding-top: 32px;
    border-top: 1px solid var(--border);
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 12px;
    color: var(--muted);
    font-size: 11px;
  }

  footer a { color: var(--accent); text-decoration: none; }
  footer a:hover { text-decoration: underline; }

  /* ─── ANIMATIONS ─────────────────────────────────────── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(16px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .step:nth-child(1)  { animation: fadeUp 0.4s 0.55s forwards; }
  .step:nth-child(2)  { animation: fadeUp 0.4s 0.62s forwards; }
  .step:nth-child(3)  { animation: fadeUp 0.4s 0.69s forwards; }
  .step:nth-child(4)  { animation: fadeUp 0.4s 0.76s forwards; }
  .step:nth-child(5)  { animation: fadeUp 0.4s 0.83s forwards; }
  .step:nth-child(6)  { animation: fadeUp 0.4s 0.90s forwards; }
  .step:nth-child(7)  { animation: fadeUp 0.4s 0.97s forwards; }

  .phase-divider:nth-child(1)  { animation-delay: 0.50s; }
  .phase-divider:nth-child(2)  { animation-delay: 0.72s; }
  .phase-divider:nth-child(3)  { animation-delay: 0.90s; }

  /* ─── PRINT ───────────────────────────────────────────── */
  @media print {
    body { background: #fff; color: #000; }
    .step-body { display: grid !important; }
    .step-chevron { display: none; }
  }
</style>
</head>
<body>
<div class="wrap">

  <!-- HEADER -->
  <header>
    <p class="eyebrow">// Career Transition Guide · 2025–2026</p>
    <h1>DevOps <span class="hl">→ AI DevOps</span><br>Engineer Roadmap</h1>
    <p class="subtitle">
      A practitioner-grade 7-step path for DevOps engineers integrating AI into production workflows —
      covering prompt engineering, local inference, cloud APIs, autonomous agents, workflow automation,
      AIOps, and continuous learning.
    </p>
    <div class="meta-pills">
      <span class="pill cyan">7 Core Steps</span>
      <span class="pill purple">3 Phases</span>
      <span class="pill green">~6–12 months</span>
      <span class="pill orange">No ML degree required</span>
    </div>
  </header>

  <!-- PROGRESS BAR (decorative) -->
  <div class="progress-bar" id="progressBar">
    <div class="seg active"></div>
    <div class="seg active"></div>
    <div class="seg active"></div>
    <div class="seg"></div>
    <div class="seg"></div>
    <div class="seg"></div>
    <div class="seg"></div>
  </div>

  <p class="section-title">// Roadmap Steps — Click to expand</p>

  <!-- ═══ PHASE 1 ═══ -->
  <div class="phase-divider">
    <span class="phase-label p1">Phase 01 · AI Foundations</span>
    <div class="phase-line"></div>
  </div>

  <div class="steps" id="steps">

    <!-- STEP 1 -->
    <div class="step" onclick="toggle(this, 0)">
      <div class="step-header">
        <span class="step-num">01</span>
        <div class="step-meta">
          <div class="step-tag" style="color:var(--accent)">Foundation</div>
          <div class="step-name">Prompt Engineering</div>
        </div>
        <span class="step-chevron">›</span>
      </div>
      <div class="step-body">
        <p class="step-desc">
          Before touching any framework, master how to talk to models. Zero-shot, one-shot, and n-shot prompting are
          the most underrated DevOps productivity multipliers. A well-crafted prompt replaces hours of scripting.
          Learn chain-of-thought, role prompting, and structured output (JSON mode) to get deterministic results
          from stochastic systems — critical before you pipe LLM output into real pipelines.
        </p>

        <div>
          <p class="col-label">Core concepts</p>
          <div class="tools">
            <span class="tool">Zero-shot prompting</span>
            <span class="tool">Few-shot / n-shot</span>
            <span class="tool">Chain-of-Thought</span>
            <span class="tool">Role prompting</span>
            <span class="tool">JSON mode / structured output</span>
            <span class="tool">System vs user prompt</span>
            <span class="tool">Temperature &amp; top-p tuning</span>
          </div>
        </div>

        <div>
          <p class="col-label">Tools</p>
          <div class="tools">
            <span class="tool purple">Claude / ChatGPT</span>
            <span class="tool purple">OpenAI Playground</span>
            <span class="tool purple">LangSmith (trace)</span>
            <span class="tool purple">PromptLayer</span>
          </div>
        </div>

        <div class="snippet"><span class="snip-label">bash · curl example</span><span class="kw">curl</span> https://api.openai.com/v1/chat/completions \
  -H <span class="str">"Authorization: Bearer $OPENAI_API_KEY"</span> \
  -H <span class="str">"Content-Type: application/json"</span> \
  -d <span class="str">'{
    "model": "gpt-4o-mini",
    "messages": [
      {"role":"system","content":"You are a senior DevOps engineer. Reply only in valid JSON."},
      {"role":"user","content":"Generate a Dockerfile for a FastAPI app. Output keys: base_image, workdir, cmd."}
    ],
    "response_format": {"type":"json_object"},
    "temperature": 0.1
  }'</span></div>

        <div>
          <p class="col-label">Outcomes</p>
          <div class="outcomes">
            <span class="outcome">Consistent, parseable LLM output</span>
            <span class="outcome">Prompt templates for Dockerfile / K8s manifest generation</span>
            <span class="outcome">Reduced hallucination via structured output</span>
          </div>
        </div>
      </div>
    </div>

    <!-- STEP 2 -->
    <div class="step" onclick="toggle(this, 1)">
      <div class="step-header">
        <span class="step-num">02</span>
        <div class="step-meta">
          <div class="step-tag" style="color:var(--accent)">Foundation</div>
          <div class="step-name">Local Model Execution</div>
        </div>
        <span class="step-chevron">›</span>
      </div>
      <div class="step-body">
        <p class="step-desc">
          Run models on your own hardware — zero API costs, full privacy, no rate limits. Ollama gives you
          an OpenAI-compatible local server in one command. Hugging Face + transformers handles custom fine-tuned
          models. This is your sandbox before committing to cloud APIs, and the foundation for air-gapped
          production deployments. Quantized models (GGUF, AWQ) let mid-range hardware (8–32GB RAM) run
          7B–13B models at acceptable throughput.
        </p>

        <div>
          <p class="col-label">Stack</p>
          <div class="tools">
            <span class="tool">Ollama</span>
            <span class="tool">Hugging Face Transformers</span>
            <span class="tool">llama.cpp</span>
            <span class="tool">GGUF quantization</span>
            <span class="tool">vLLM (GPU serving)</span>
            <span class="tool">Open WebUI</span>
          </div>
        </div>

        <div>
          <p class="col-label">Models to start with</p>
          <div class="tools">
            <span class="tool purple">llama3.2:3b (CPU-friendly)</span>
            <span class="tool purple">qwen2.5-coder:7b (code)</span>
            <span class="tool purple">mistral:7b (general)</span>
            <span class="tool purple">nomic-embed-text (RAG)</span>
          </div>
        </div>

        <div class="snippet"><span class="snip-label">docker-compose · ollama</span><span class="kw">services</span>:
  <span class="fn">ollama</span>:
    image: <span class="str">ollama/ollama:latest</span>
    ports: [<span class="str">"11434:11434"</span>]
    volumes: [<span class="str">"ollama_data:/root/.ollama"</span>]
    deploy:
      resources.reservations.devices:
        - capabilities: [gpu]   <span class="cm"># remove if CPU-only</span>

  <span class="fn">open-webui</span>:
    image: <span class="str">ghcr.io/open-webui/open-webui:latest</span>
    ports: [<span class="str">"3000:8080"</span>]
    environment:
      OLLAMA_BASE_URL: <span class="str">http://ollama:11434</span>
    depends_on: [ollama]

<span class="kw">volumes</span>: { ollama_data: }</div>

        <div>
          <p class="col-label">Outcomes</p>
          <div class="outcomes">
            <span class="outcome">$0 inference cost dev environment</span>
            <span class="outcome">OpenAI-compatible local endpoint</span>
            <span class="outcome">Model hot-swap without code changes</span>
          </div>
        </div>
      </div>
    </div>

    <!-- STEP 3 -->
    <div class="step" onclick="toggle(this, 2)">
      <div class="step-header">
        <span class="step-num">03</span>
        <div class="step-meta">
          <div class="step-tag" style="color:var(--accent)">Foundation</div>
          <div class="step-name">Cloud Model Integration via APIs</div>
        </div>
        <span class="step-chevron">›</span>
      </div>
      <div class="step-body">
        <p class="step-desc">
          When local hardware isn't enough — scale, latency, or multimodal capability — wire proprietary models
          into your Python and shell scripts via APIs. The goal: automate real DevOps tasks such as Dockerfile
          generation, incident triage write-ups, and runbook drafts. Use async Python clients for non-blocking
          calls in pipelines. AWS Bedrock and GCP Vertex AI let you stay inside your existing cloud billing and
          IAM without managing API keys directly.
        </p>

        <div>
          <p class="col-label">Providers</p>
          <div class="tools">
            <span class="tool">OpenAI API / Azure OpenAI</span>
            <span class="tool">Anthropic Claude API</span>
            <span class="tool">AWS Bedrock</span>
            <span class="tool">GCP Vertex AI</span>
            <span class="tool">Groq (low-latency)</span>
          </div>
        </div>

        <div>
          <p class="col-label">Python libs</p>
          <div class="tools">
            <span class="tool purple">openai</span>
            <span class="tool purple">anthropic</span>
            <span class="tool purple">boto3 (Bedrock)</span>
            <span class="tool purple">google-cloud-aiplatform</span>
            <span class="tool purple">httpx (async)</span>
          </div>
        </div>

        <div class="snippet"><span class="snip-label">python · async dockerfile generator</span><span class="kw">import</span> asyncio, json
<span class="kw">from</span> openai <span class="kw">import</span> <span class="fn">AsyncOpenAI</span>

client = <span class="fn">AsyncOpenAI</span>()  <span class="cm"># reads OPENAI_API_KEY from env</span>

<span class="kw">async def</span> <span class="fn">gen_dockerfile</span>(app_desc: str) -> dict:
    resp = <span class="kw">await</span> client.chat.completions.<span class="fn">create</span>(
        model=<span class="str">"gpt-4o-mini"</span>,
        messages=[
            {<span class="str">"role"</span>:<span class="str">"system"</span>, <span class="str">"content"</span>:<span class="str">"Output valid JSON only."</span>},
            {<span class="str">"role"</span>:<span class="str">"user"</span>,   <span class="str">"content"</span>: f<span class="str">"Dockerfile for: {app_desc}"</span>}
        ],
        response_format={<span class="str">"type"</span>:<span class="str">"json_object"</span>},
        temperature=0.1,
    )
    <span class="kw">return</span> json.<span class="fn">loads</span>(resp.choices[0].message.content)

asyncio.<span class="fn">run</span>(<span class="fn">gen_dockerfile</span>(<span class="str">"FastAPI + uvicorn, Python 3.12"</span>))</div>

        <div>
          <p class="col-label">Outcomes</p>
          <div class="outcomes">
            <span class="outcome">Automated Dockerfile / manifest generation</span>
            <span class="outcome">AI-assisted incident summary in runbooks</span>
            <span class="outcome">Cost-aware model routing (local ↔ cloud)</span>
          </div>
        </div>
      </div>
    </div>

    <!-- ═══ PHASE 2 ═══ -->
    <div class="phase-divider" style="animation-delay:0.76s">
      <span class="phase-label p2">Phase 02 · Automation &amp; Agents</span>
      <div class="phase-line"></div>
    </div>

    <!-- STEP 4 -->
    <div class="step" onclick="toggle(this, 3)">
      <div class="step-header">
        <span class="step-num">04</span>
        <div class="step-meta">
          <div class="step-tag" style="color:var(--accent2)">Automation</div>
          <div class="step-name">AI Agents</div>
        </div>
        <span class="step-chevron">›</span>
      </div>
      <div class="step-body">
        <p class="step-desc">
          Agents go beyond single API calls — they plan, use tools, and self-correct over multiple steps.
          For DevOps: a pod-failure agent that reads kubectl describe, queries Prometheus, checks recent
          deployments, and outputs a structured incident report is a real 2-hour time saver per on-call shift.
          LangGraph gives you state-machine-level control over agent flow. MCP (Model Context Protocol) is
          the emerging standard for wiring AI directly to your infra tooling without custom glue code.
        </p>

        <div>
          <p class="col-label">Frameworks</p>
          <div class="tools">
            <span class="tool">LangGraph</span>
            <span class="tool">LangChain</span>
            <span class="tool">CrewAI</span>
            <span class="tool">AutoGen</span>
            <span class="tool">MCP (Model Context Protocol)</span>
          </div>
        </div>

        <div>
          <p class="col-label">Agent use-cases for DevOps</p>
          <div class="tools">
            <span class="tool purple">K8s pod failure diagnosis</span>
            <span class="tool purple">Auto-generated PR descriptions</span>
            <span class="tool purple">Terraform plan reviewer</span>
            <span class="tool purple">Log anomaly triage</span>
            <span class="tool purple">CVE impact analysis</span>
          </div>
        </div>

        <div class="snippet"><span class="snip-label">python · k8s agent tool (LangGraph)</span><span class="kw">from</span> langchain_core.tools <span class="kw">import</span> tool
<span class="kw">import</span> subprocess, json

<span class="fn">@tool</span>
<span class="kw">def</span> <span class="fn">kubectl_describe</span>(pod_name: str, namespace: str = <span class="str">"default"</span>) -> str:
    <span class="str">"""Describe a Kubernetes pod to diagnose failures."""</span>
    result = subprocess.<span class="fn">run</span>(
        [<span class="str">"kubectl"</span>, <span class="str">"describe"</span>, <span class="str">"pod"</span>, pod_name, <span class="str">"-n"</span>, namespace],
        capture_output=True, text=True
    )
    <span class="kw">return</span> result.stdout[-4000:]  <span class="cm"># last 4k chars fit in context</span>

<span class="fn">@tool</span>
<span class="kw">def</span> <span class="fn">get_recent_events</span>(namespace: str = <span class="str">"default"</span>) -> str:
    <span class="str">"""Get recent K8s events for a namespace."""</span>
    result = subprocess.<span class="fn">run</span>(
        [<span class="str">"kubectl"</span>, <span class="str">"get"</span>, <span class="str">"events"</span>, <span class="str">"-n"</span>, namespace, <span class="str">"--sort-by=.lastTimestamp"</span>],
        capture_output=True, text=True
    )
    <span class="kw">return</span> result.stdout

tools = [kubectl_describe, get_recent_events]
<span class="cm"># bind to LangGraph ReAct agent + Claude/GPT backbone</span></div>

        <div>
          <p class="col-label">Outcomes</p>
          <div class="outcomes">
            <span class="outcome">Autonomous incident analysis agent</span>
            <span class="outcome">MCP server connected to kubectl + Prometheus</span>
            <span class="outcome">Reduced mean time to diagnose (MTTD)</span>
          </div>
        </div>
      </div>
    </div>

    <!-- STEP 5 -->
    <div class="step" onclick="toggle(this, 4)">
      <div class="step-header">
        <span class="step-num">05</span>
        <div class="step-meta">
          <div class="step-tag" style="color:var(--accent2)">Automation</div>
          <div class="step-name">Workflow Automation</div>
        </div>
        <span class="step-chevron">›</span>
      </div>
      <div class="step-body">
        <p class="step-desc">
          Embed AI into your CI/CD pipelines and event-driven workflows without reinventing glue code.
          n8n gives you a self-hostable, visual workflow builder with native LLM nodes — wire GitHub webhooks,
          Slack alerts, and LLM calls in minutes. In pipelines, use AI for security policy checking (SAST
          summary), auto-tagging releases, and generating human-readable changelogs from commit diffs.
          The key discipline: treat AI as a pipeline step with clear input/output contracts and fallback behavior.
        </p>

        <div>
          <p class="col-label">Platforms</p>
          <div class="tools">
            <span class="tool">n8n (self-hosted)</span>
            <span class="tool">GitHub Actions + AI step</span>
            <span class="tool">GitLab CI AI jobs</span>
            <span class="tool">Zapier / Make (SaaS)</span>
          </div>
        </div>

        <div>
          <p class="col-label">Pipeline AI use-cases</p>
          <div class="tools">
            <span class="tool purple">SAST finding summarizer</span>
            <span class="tool purple">Changelog generator</span>
            <span class="tool purple">PR diff reviewer</span>
            <span class="tool purple">Helm chart linter + explainer</span>
            <span class="tool purple">Slack incident notifier</span>
          </div>
        </div>

        <div class="snippet"><span class="snip-label">github actions · AI changelog step</span>- <span class="kw">name</span>: Generate AI changelog
  <span class="kw">env</span>:
    OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
  <span class="kw">run</span>: |
    DIFF=$(git log --oneline ${{ github.event.before }}..HEAD)
    RESPONSE=$(curl -s https://api.openai.com/v1/chat/completions \
      -H "Authorization: Bearer $OPENAI_API_KEY" \
      -H "Content-Type: application/json" \
      -d "{\"model\":\"gpt-4o-mini\",\"messages\":[
            {\"role\":\"system\",\"content\":\"Summarize git commits as a user-facing changelog. Be concise.\"},
            {\"role\":\"user\",\"content\":\"$DIFF\"}
          ],\"temperature\":0.2}")
    echo "$RESPONSE" | jq -r '.choices[0].message.content' >> CHANGELOG.md
    git add CHANGELOG.md && git commit -m "chore: AI changelog [skip ci]"</div>

        <div>
          <p class="col-label">Outcomes</p>
          <div class="outcomes">
            <span class="outcome">AI-aware CI/CD pipeline</span>
            <span class="outcome">Auto-generated changelogs &amp; PR summaries</span>
            <span class="outcome">n8n workflow for on-call alert triage</span>
          </div>
        </div>
      </div>
    </div>

    <!-- ═══ PHASE 3 ═══ -->
    <div class="phase-divider" style="animation-delay:0.90s">
      <span class="phase-label p3">Phase 03 · Intelligence &amp; Growth</span>
      <div class="phase-line"></div>
    </div>

    <!-- STEP 6 -->
    <div class="step" onclick="toggle(this, 5)">
      <div class="step-header">
        <span class="step-num">06</span>
        <div class="step-meta">
          <div class="step-tag" style="color:var(--accent3)">Intelligence</div>
          <div class="step-name">AIOps — AI-Driven Observability</div>
        </div>
        <span class="step-chevron">›</span>
      </div>
      <div class="step-body">
        <p class="step-desc">
          Threshold-based alerts are the floor, not the ceiling. AIOps layers ML-based anomaly detection
          over your Prometheus metrics and log streams to catch patterns no human writes a static rule for:
          gradual memory drift, correlated cross-service latency, and silent error rate upticks below alert
          thresholds. Tools like Grafana's built-in ML forecasting, Dynatrace Davis AI, and open-source
          Prophet-based alerting on Prometheus data put predictive ops within reach without a data science team.
        </p>

        <div>
          <p class="col-label">AIOps stack</p>
          <div class="tools">
            <span class="tool">Grafana (ML forecasting)</span>
            <span class="tool">Prometheus + Alertmanager</span>
            <span class="tool">OpenTelemetry</span>
            <span class="tool">Elastic / OpenSearch ML</span>
            <span class="tool">Prophet (time-series)</span>
            <span class="tool">Dynatrace Davis</span>
            <span class="tool">Coroot (self-hosted)</span>
          </div>
        </div>

        <div>
          <p class="col-label">Key capabilities to implement</p>
          <div class="tools">
            <span class="tool green">Anomaly detection on Prometheus metrics</span>
            <span class="tool green">Log clustering (reduce alert noise)</span>
            <span class="tool green">Predictive autoscaling</span>
            <span class="tool green">LLM-powered alert enrichment</span>
            <span class="tool green">Root cause correlation</span>
          </div>
        </div>

        <div class="snippet"><span class="snip-label">python · prophet anomaly on prom metrics</span><span class="kw">from</span> prophet <span class="kw">import</span> <span class="fn">Prophet</span>
<span class="kw">import</span> pandas <span class="kw">as</span> pd, requests

<span class="cm"># Pull metric from Prometheus HTTP API</span>
<span class="kw">def</span> <span class="fn">fetch_metric</span>(query: str, step=<span class="str">"5m"</span>, hours=24) -> pd.DataFrame:
    url = <span class="str">"http://prometheus:9090/api/v1/query_range"</span>
    r = requests.<span class="fn">get</span>(url, params={
        <span class="str">"query"</span>: query, <span class="str">"step"</span>: step,
        <span class="str">"start"</span>: <span class="str">"now-24h"</span>, <span class="str">"end"</span>: <span class="str">"now"</span>
    })
    vals = r.json()[<span class="str">"data"</span>][<span class="str">"result"</span>][0][<span class="str">"values"</span>]
    df = pd.<span class="fn">DataFrame</span>(vals, columns=[<span class="str">"ds"</span>, <span class="str">"y"</span>])
    df[<span class="str">"ds"</span>] = pd.to_datetime(df[<span class="str">"ds"</span>], unit=<span class="str">"s"</span>)
    df[<span class="str">"y"</span>] = df[<span class="str">"y"</span>].<span class="fn">astype</span>(float)
    <span class="kw">return</span> df

df = <span class="fn">fetch_metric</span>(<span class="str">'rate(http_requests_total[5m])'</span>)
m  = <span class="fn">Prophet</span>(interval_width=0.95)
m.<span class="fn">fit</span>(df)
forecast = m.<span class="fn">predict</span>(m.<span class="fn">make_future_dataframe</span>(periods=12, freq=<span class="str">"5min"</span>))
<span class="cm"># flag rows where yhat_lower > actual → anomaly</span></div>

        <div>
          <p class="col-label">Outcomes</p>
          <div class="outcomes">
            <span class="outcome">Anomaly alerts before user impact</span>
            <span class="outcome">30–50% alert noise reduction via log clustering</span>
            <span class="outcome">LLM-enriched PagerDuty/Slack notifications</span>
          </div>
        </div>
      </div>
    </div>

    <!-- STEP 7 -->
    <div class="step" onclick="toggle(this, 6)">
      <div class="step-header">
        <span class="step-num">07</span>
        <div class="step-meta">
          <div class="step-tag" style="color:var(--accent3)">Growth</div>
          <div class="step-name">Continuous Learning &amp; Future-Proofing</div>
        </div>
        <span class="step-chevron">›</span>
      </div>
      <div class="step-body">
        <p class="step-desc">
          The AI tooling landscape has a 3-month half-life. Engineers who treat learning as a daily
          15–30 minute discipline — not a course they take once — compound significantly over those who binge
          then stall. Focus on the layer above your current role: if you do K8s well, learn LLMOps and
          model serving. If you do RAG, learn evaluation frameworks. Build in public: write one technical
          post per month, contribute to one open-source AI infra project per quarter. Certifications
          signal credibility; hands-on projects signal capability.
        </p>

        <div>
          <p class="col-label">Learning channels (15–30 min/day)</p>
          <div class="tools">
            <span class="tool">Anthropic / OpenAI release notes</span>
            <span class="tool">TLDR Newsletter (AI/DevOps)</span>
            <span class="tool">Hacker News — AI track</span>
            <span class="tool">LangChain blog</span>
            <span class="tool">Grafana Labs blog</span>
            <span class="tool">KodeKloud AI labs</span>
          </div>
        </div>

        <div>
          <p class="col-label">Certifications to consider</p>
          <div class="tools">
            <span class="tool green">CKA / CKAD (Kubernetes)</span>
            <span class="tool green">AWS ML Specialty</span>
            <span class="tool green">GCP Professional ML Engineer</span>
            <span class="tool green">DeepLearning.AI MLOps Specialization</span>
          </div>
        </div>

        <div>
          <p class="col-label">Emerging areas to track (2026)</p>
          <div class="tools">
            <span class="tool orange">MCP ecosystem</span>
            <span class="tool orange">AI gateway / LLM proxies (LiteLLM)</span>
            <span class="tool orange">Evals &amp; observability (LangSmith, Arize)</span>
            <span class="tool orange">Model fine-tuning on infra data (LoRA)</span>
            <span class="tool orange">AI-native IaC (Pulumi AI, Terraform AI)</span>
            <span class="tool orange">Green DevOps / AI energy efficiency</span>
          </div>
        </div>

        <div>
          <div class="timeline-badge">▸ Suggested daily habit</div>
          <div class="snippet"><span class="snip-label">fish shell · daily learning script</span><span class="cm"># ~/.config/fish/functions/ailearn.fish</span>
<span class="kw">function</span> <span class="fn">ailearn</span>
    echo <span class="str">"── Today's AI DevOps learning ──"</span>
    <span class="cm"># Open HN AI digest in browser</span>
    open <span class="str">"https://news.ycombinator.com/news?q=llm+devops"</span>
    <span class="cm"># Pull latest anthropic / openai changelog</span>
    curl -s <span class="str">"https://docs.anthropic.com/rss.xml"</span> | grep -m3 <span class="str">"&lt;title&gt;"</span>
    echo <span class="str">"15 min timer started — focus on one concept."</span>
<span class="kw">end</span></div>
        </div>

        <div>
          <p class="col-label">Outcomes</p>
          <div class="outcomes">
            <span class="outcome">Consistent skill compounding</span>
            <span class="outcome">Public portfolio of AI infra projects</span>
            <span class="outcome">Recognized as AI-forward DevOps engineer</span>
          </div>
        </div>
      </div>
    </div>

  </div><!-- /steps -->

  <!-- FOOTER -->
  <footer>
    <span>AI DevOps Roadmap · Based on practitioner research &amp; <em>DevOps to AI Engineer</em> framework · 2025–2026</span>
    <span>Built for engineers, by engineers · <a href="https://roadmap.sh/devops" target="_blank">roadmap.sh/devops ↗</a></span>
  </footer>

</div><!-- /wrap -->

<script>
  const segs = document.querySelectorAll('.progress-bar .seg');

  function toggle(el, idx) {
    const isOpen = el.classList.contains('open');
    // close all
    document.querySelectorAll('.step').forEach(s => s.classList.remove('open'));
    if (!isOpen) el.classList.add('open');
    // update progress
    segs.forEach((s, i) => {
      s.classList.toggle('active', i <= idx);
    });
  }

  // open first step by default
  const firstStep = document.querySelector('.step');
  if (firstStep) {
    firstStep.classList.add('open');
  }
</script>
</body>
</html>








---HTML page whose design to update ends here---
