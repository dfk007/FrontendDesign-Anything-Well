---
name: frontend-design
description: >
  Editorial-Technical Dark UI — a production-grade design system combining editorial
  typographic refinement with technical/terminal aesthetics. Use when the user wants
  to build any web application, dashboard, document viewer, report, prep tool, or
  single-page app with this distinctive "field manual" look: deep navy backgrounds,
  electric teal accent, Fraunces + Geist + JetBrains Mono font stack, grid-line
  texture, scanline overlay, collapsible accordion panels, and a light/dark theme toggle.
---

# Editorial-Technical Dark UI — Design System Skill

## Concept & Aesthetic Direction

This design language fuses **editorial print design** (magazine mastheads, Fraunces variable serif, tight tracked letterspacing, ruled dividers) with **technical terminal culture** (JetBrains Mono everywhere for metadata, teal glow, code chips, monochromatic scan-lines). The result feels like a high-quality printed field manual that runs in a terminal.

**Core feel**: Serious, precise, trustworthy. Not flashy — *authoritative*. Every element earns its place. Negative space is a feature, not an omission.

**When to use**: Dashboards, knowledge bases, interview prep tools, documentation sites, reference guides, data-heavy reports, developer portals, internal tooling UIs.

---

## Typography

Three-font system. Never deviate from this stack.

### 1. Fraunces (Display / Serif)
- **Source**: Google Fonts — `family=Fraunces:opsz,wght,SOFT,WONK@9..144,300..900,0..100,0..1`
- **Role**: Hero headings, section titles, lede/pull-quote text, large numeric callouts
- **Key variation axes**:
  - Hero H1: `font-variation-settings: "opsz" 144, "SOFT" 0, "WONK" 0;` weight 300 — ultra-refined, optical large
  - Hero italic accent: `font-variation-settings: "opsz" 144, "SOFT" 80, "WONK" 1;` — soft, slightly quirky
  - Section titles / lede: `font-variation-settings: "opsz" 72;` weight 360
  - Italic descriptors: `font-variation-settings: "opsz" 36, "SOFT" 20;`
- **Sizing**: H1 `clamp(3rem, 7.2vw, 5.8rem)`, section titles `1.9rem`, lede `1.08rem`
- **Line height**: H1 `0.9` (tight), body text `1.6–1.72`
- **Letter spacing**: H1 `-0.04em`, section titles `-0.015em`

### 2. Geist (Body / Sans-serif)
- **Source**: Google Fonts — `family=Geist:wght@300..900`
- **Role**: Body copy, question text, answer prose, general paragraph content
- **Sizing**: Base `1rem`, question text `0.93rem`, answer body `0.9rem`
- **Weight**: 600 for question titles, 400 for body prose
- **Line height**: `1.55` base, `1.72` in answer panels

### 3. JetBrains Mono (Monospace / Metadata)
- **Source**: Google Fonts — `family=JetBrains+Mono:ital,wght@0,300..700;1,300..700`
- **Role**: ALL metadata labels, tab buttons, question numbers, mastheads, footers, search inputs, code chips, eyebrows, colophons, theme toggle
- **Sizing**: `0.62rem`–`0.82rem` for labels; never larger than body text except for code blocks
- **Letter spacing**: `0.1em`–`0.3em` (always tracked wide)
- **Transform**: `uppercase` everywhere it appears as a label

**Font import block** (always include all three):
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght,SOFT,WONK@9..144,300..900,0..100,0..1&family=Geist:wght@300..900&family=JetBrains+Mono:ital,wght@0,300..700;1,300..700&display=swap" rel="stylesheet">
```

---

## Color System

Full dual-theme via `data-theme` attribute on `<html>`. CSS variables drive everything — never hardcode colors.

### Dark Theme (default) — Deep Navy-Slate

```css
:root {
  /* Backgrounds — layered depth */
  --paper:        #0b0f18;   /* page background — near-black navy */
  --paper-2:      #111827;   /* card/panel background */
  --paper-3:      #1a2236;   /* hover state background */
  --tile:         #131c2e;   /* subtle tile/chip background */

  /* Text */
  --ink:          #e8edf5;   /* primary text — cool off-white */
  --ink-2:        #c2cfe0;   /* secondary text — slightly muted blue-white */
  --muted:        #5e7394;   /* muted labels, placeholders, dividers */

  /* Borders */
  --rule:         #1e2e44;   /* standard divider lines */
  --rule-soft:    #162033;   /* very subtle dividers */
  --grid-line:    rgba(100,160,255,0.04); /* blueprint grid texture */

  /* Accent palette */
  --teal:         #00c8a0;   /* PRIMARY accent — electric teal (glows) */
  --teal-soft:    #00a880;   /* teal hover/pressed state */
  --blue:         #3b82f6;   /* secondary accent */
  --amber:        #f59e0b;   /* warning / medium priority */
  --violet:       #8b5cf6;   /* hard / complex */
  --coral:        #f87171;   /* danger / high priority */

  /* Semantic aliases for difficulty/priority tiers */
  --easy:         #00c8a0;   /* tier 1 */
  --intermediate: #3b82f6;   /* tier 2 */
  --hard:         #8b5cf6;   /* tier 3 */
  --other:        #f59e0b;   /* tier 4 / miscellaneous */
  --jd-col:       #f87171;   /* special tab / critical items */

  /* Code blocks */
  --code-bg:      #050910;   /* darker than page for code contrast */
  --code-text:    #a8d8b8;   /* soft green — readable, not harsh */
}
```

### Light Theme Override

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
  --easy:         #00957a;
  --intermediate: #1d4ed8;
  --hard:         #6d28d9;
  --other:        #b45309;
  --jd-col:       #dc2626;
  --code-bg:      #0d1424;   /* code bg stays dark in light mode */
  --code-text:    #a8d8b8;
}
```

**Color rules**:
- Teal is the single dominant accent. It must glow: always pair with `text-shadow: 0 0 Xpx rgba(0,200,160,Y)` or `box-shadow` when used on interactive elements.
- Never use more than 2 accent colors in the same visual region.
- Amber = medium warning. Coral = danger/critical. Violet = complex/hard.
- Background depth: `--paper` → `--paper-2` → `--paper-3` (deeper = more interactive/elevated).

---

## Background & Atmosphere

### Blueprint Grid Texture
Applied to `body` background — subtle coordinate-paper feel:

```css
body {
  background: var(--paper);
  background-image:
    linear-gradient(var(--grid-line) 1px, transparent 1px),
    linear-gradient(90deg, var(--grid-line) 1px, transparent 1px);
  background-size: 44px 44px;
}
```

### Scanline Overlay
Fixed `::before` pseudo-element on body — CRT/terminal texture at very low opacity:

```css
body::before {
  content: "";
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 1;
  opacity: 0.22;  /* reduce to 0.06 for light theme */
  background: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 2px,
    rgba(0,200,160,0.015) 2px,
    rgba(0,200,160,0.015) 4px
  );
}
```

### Ambient Teal Glow
Fixed `::after` pseudo-element — radial gradient corner light source, top-right:

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

### Z-index Layering
- `z-index: 0` — ambient glow (behind everything)
- `z-index: 1` — scanline overlay (above content but non-interactive)
- `z-index: 2` — page wrapper / all actual content
- `z-index: 100` — fixed UI controls (theme toggle)

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

### Masthead (3-Column Header Bar)
Top-of-page newspaper-style masthead with ruled borders:

```css
.masthead {
  border-top: 1px solid var(--teal);    /* teal top rule — signature detail */
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
.masthead .center {
  font-weight: 700;
  color: var(--teal);
  font-size: 0.78rem;
  letter-spacing: 0.2em;
  text-shadow: 0 0 8px rgba(0,200,160,0.5);
}
```

Usage: Left = context/role label, Center = document title (teal, glowing), Right = date/edition.

### Hero Section
Asymmetric 2-column grid (1.3fr / 1fr), content aligned to bottom:

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

Left column: giant Fraunces headline. Right column: `lede` block with left teal border.

**Hero H1 pattern**:
```html
<h1>
  <span class="co-name">// COMPANY · Category · Subtitle</span>
  Primary Title &<br>Secondary <em>Keyword</em>
</h1>
```
- `.co-name`: JetBrains Mono, `0.72rem`, `letter-spacing: 0.3em`, `uppercase`, `--muted`
- `em` inside h1: teal color, SOFT/WONK variation axes, `text-shadow: 0 0 24px rgba(0,200,160,0.35)`

**Lede / Pull Quote**:
```css
.lede {
  border-left: 2px solid var(--teal);
  padding-left: 1.4rem;
  font-family: 'Fraunces', serif;
  font-variation-settings: "opsz" 36, "SOFT" 20;
  font-weight: 360;
  font-size: 1.08rem;
  line-height: 1.6;
}
.lede .eyebrow {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.66rem;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--teal);
  margin-bottom: 0.7rem;
  display: block;
}
```

### Meta Bar (Stats Strip)
Horizontal strip of key-value pairs, each in its own cell with ruled dividers:

```css
.meta-bar {
  display: flex;
  flex-wrap: wrap;
  border-top: 1px solid var(--rule);
  border-bottom: 1px solid var(--rule);
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
.meta-cell .label {
  text-transform: uppercase;
  color: var(--muted);
  font-size: 0.62rem;
  letter-spacing: 0.18em;
  display: block;
  margin-bottom: 0.4rem;
}
.meta-cell .val.big {
  font-family: 'Fraunces', serif;
  font-variation-settings: "opsz" 72;
  font-size: 1.9rem;
  font-weight: 400;
  color: var(--teal);
  font-style: italic;
  line-height: 1;
  text-shadow: 0 0 16px rgba(0,200,160,0.3);
}
```

Use `.val.big` for the single most important metric (e.g., total question count, score, percentage).

---

## Navigation — Tab Bar

Horizontal tab strip at the bottom of the search bar, border-bottom ruled. Each tab activates with a color-matched bottom border:

```css
.nav-bar {
  display: flex;
  gap: 2px;
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
  margin-bottom: -1px;  /* overlap the nav-bar border */
}
.tab-btn:hover { color: var(--ink); }
/* Active states — one per tier */
.tab-btn.active-easy         { color: var(--easy);         border-bottom-color: var(--easy); }
.tab-btn.active-intermediate { color: var(--intermediate); border-bottom-color: var(--intermediate); }
.tab-btn.active-hard         { color: var(--hard);         border-bottom-color: var(--hard); }
.tab-btn.active-other        { color: var(--other);        border-bottom-color: var(--other); }
.tab-btn.active-jd           { color: var(--jd-col);       border-bottom-color: var(--jd-col); }
```

Tab switching via JS: hide/show `.section` blocks, toggle active class on button. Sections: `display: none` default, `display: block` when `.active`.

---

## Search Bar

Full-width, monospace input with teal left border accent:

```css
.search-bar { margin: 2rem 0 0; position: relative; }
.search-bar input {
  width: 100%;
  background: var(--paper-2);
  border: 1px solid var(--rule);
  border-left: 2px solid var(--teal);
  color: var(--ink-2);
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.82rem;
  padding: 0.9rem 1rem 0.9rem 2.8rem;
  outline: none;
  border-radius: 0;  /* NO border radius — sharp corners throughout */
  transition: border-color 0.2s, box-shadow 0.2s;
}
.search-bar input:focus {
  border-color: var(--teal);
  box-shadow: 0 0 0 3px rgba(0,200,160,0.1);
}
.search-bar input::placeholder { color: var(--muted); }
/* Icon positioned inside input */
.search-icon {
  position: absolute;
  left: 14px;
  top: 50%;
  transform: translateY(-50%);
  color: var(--teal);
  font-family: 'JetBrains Mono', monospace;
}
```

**Important**: Zero border-radius everywhere. This design uses sharp rectangular corners as a deliberate aesthetic choice.

---

## Section Headers

Each content section has a labeled header with a ruled line extending to the right:

```css
.section-label {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
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

Section label color matches its tier accent: `.easy .section-label { color: var(--easy); }` etc.

---

## Accordion / Q&A Panels

The core interactive component. Collapsible rows stacked flush with shared borders (no gap):

```css
.qa-list { display: flex; flex-direction: column; gap: 0; }
.qa-item {
  border: 1px solid var(--rule);
  border-top: none;
  overflow: hidden;
  transition: border-color 0.2s;
}
.qa-item:first-child { border-top: 1px solid var(--rule); }
.qa-item:hover { border-color: var(--muted); }

/* Left-border color accent on hover by tier */
.qa-item.easy:hover        { border-left: 2px solid var(--easy); }
.qa-item.intermediate:hover { border-left: 2px solid var(--intermediate); }
.qa-item.hard:hover        { border-left: 2px solid var(--hard); }
.qa-item.other:hover       { border-left: 2px solid var(--other); }

/* Question row */
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

/* Question number badge */
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
}
.qa-item.open .q-arrow { transform: rotate(180deg); }

/* Answer panel — hidden by default */
.qa-answer {
  display: none;
  padding: 0 1.4rem 1.4rem 3.6rem;  /* indent matches q-num + gap */
  background: var(--paper);
  border-top: 1px solid var(--rule);
}
.qa-item.open .qa-answer { display: block; }

/* Answer body */
.answer-content {
  padding-top: 1.2rem;
  font-size: 0.9rem;
  line-height: 1.72;
  color: var(--ink-2);
}
.answer-content strong { color: var(--ink); font-weight: 600; }
.answer-content em { font-style: italic; color: var(--muted); }
.answer-content code {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.77rem;
  background: var(--code-bg);
  border: 1px solid var(--rule);
  padding: 1px 6px;
  color: var(--teal);
  border-radius: 0;  /* sharp corners */
}
```

**Priority border variants** (for items with pre-set urgency):
```css
.qa-item.high-priority   { border-left: 3px solid var(--coral); }
.qa-item.medium-priority { border-left: 3px solid var(--amber); }
.qa-item.low-priority    { border-left: 3px solid var(--teal); }
```

**Accordion JS** (single-open pattern):
```javascript
function toggleItem(el) {
  const wasOpen = el.classList.contains('open');
  el.parentElement.querySelectorAll('.qa-item.open').forEach(i => i.classList.remove('open'));
  if (!wasOpen) el.classList.add('open');
}
```

---

## Chip / Badge Components

Small inline label components — always sharp corners, always monospace:

```css
/* Teal tip chip */
.tip-chip {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.66rem;
  padding: 3px 10px;
  border: 1px solid var(--teal);
  color: var(--teal);
  background: rgba(0,200,160,0.05);
}

/* Amber star chip */
.star-chip {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.66rem;
  padding: 3px 10px;
  border: 1px solid var(--amber);
  color: var(--amber);
  background: rgba(245,158,11,0.05);
}
```

Pattern: `border: 1px solid var(--ACCENT)` + `color: var(--ACCENT)` + `background: rgba(R,G,B,0.05)` — works for any accent color.

---

## Theme Toggle Button

Fixed position, top-right corner, square:

```css
.theme-toggle {
  position: fixed;
  top: 1rem;
  right: 1rem;
  z-index: 100;
  background: var(--paper-2);
  color: var(--teal);
  border: 1.5px solid var(--teal);
  width: 44px;
  height: 44px;
  border-radius: 4px;  /* slight rounding only here — exception to the sharp-corners rule */
  font-family: 'JetBrains Mono', monospace;
  font-size: 1rem;
  box-shadow: 0 0 12px rgba(0,200,160,0.2);
  cursor: pointer;
  transition: all 0.25s ease;
}
.theme-toggle:hover {
  background: var(--teal);
  color: var(--paper);
  box-shadow: 0 0 20px rgba(0,200,160,0.4);
}
```

Toggle icon: `◑` (half-filled circle). JS:
```javascript
function toggleTheme() {
  const html = document.documentElement;
  const next = html.getAttribute('data-theme') === 'dark' ? 'light' : 'dark';
  html.setAttribute('data-theme', next);
  localStorage.setItem('theme', next);
}
// On load — restore saved preference
(function() {
  const saved = localStorage.getItem('theme') || 'dark';
  document.documentElement.setAttribute('data-theme', saved);
})();
```

---

## Footer

Three-column ruled footer, mirroring masthead layout:

```css
.footer-rule {
  border-top: 1px solid var(--teal);    /* teal top rule — matches masthead */
  border-bottom: 1px solid var(--rule);
  margin-top: 5rem;
  padding: 1.2rem 0;
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
/* Colophon — below footer */
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

Colophon pattern: `Set in [Font 1] · [Font 2] · [Font 3] · [Year]`

---

## Animations

### Page Load — Staggered Rise
Every major block fades up on load:

```css
@keyframes rise {
  to { opacity: 1; transform: translateY(0); }
}
.block {
  opacity: 0;
  transform: translateY(15px);
  animation: rise 0.55s forwards;
}
.block:nth-child(2) { animation-delay: 0.08s; }
.block:nth-child(3) { animation-delay: 0.16s; }
.block:nth-child(4) { animation-delay: 0.24s; }
.block:nth-child(5) { animation-delay: 0.32s; }
.block:nth-child(6) { animation-delay: 0.40s; }
.block:nth-child(7) { animation-delay: 0.48s; }
```

### Panel Reveal
Accordion items animate in when their section becomes active:

```css
@keyframes panelIn {
  from { opacity: 0; transform: translateY(14px); }
  to   { opacity: 1; transform: translateY(0); }
}
.qa-item { animation: panelIn 0.28s ease both; }
```

### Transitions
- Color/background changes: `transition: 0.15s–0.25s ease`
- Theme switch: `transition: background 0.4s ease, color 0.4s ease` on `body`
- Arrow rotation: `transition: transform 0.25s`
- Interactive element glows: `transition: box-shadow 0.25s`

---

## Responsive Breakpoints

### Mobile (≤ 860px)

```css
@media (max-width: 860px) {
  .hero { grid-template-columns: 1fr; gap: 2rem; }
  .masthead { grid-template-columns: 1fr; text-align: center; gap: 0.35rem; }
  .masthead .right, .masthead .left { text-align: center; }
  .meta-bar { flex-direction: column; }
  .meta-cell { border-right: none; border-bottom: 1px solid var(--rule); }
  .qa-answer { padding-left: 1.4rem; }  /* remove indentation on mobile */
  .nav-bar { gap: 1px; }
  .tab-btn { padding: 0.65rem 0.9rem; font-size: 0.62rem; }
  .footer-rule { grid-template-columns: 1fr; text-align: center; gap: 0.5rem; }
}
```

### Print

```css
@media print {
  body { background: #fff !important; color: #000 !important; }
  body::before, body::after { display: none; }
  .qa-answer { display: block !important; }  /* expand all panels */
  .q-arrow, .theme-toggle, .nav-bar { display: none; }
  .block { opacity: 1; transform: none; animation: none; }
  .section { display: block !important; }
}
```

---

## Design Rules — Do & Don't

### DO
- Use `var(--teal)` as the single most prominent accent. When in doubt, it's teal.
- Add `text-shadow: 0 0 Xpx rgba(0,200,160,Y)` to any teal text that is a focal point.
- Use JetBrains Mono for every label, number, tag, badge, or metadata element.
- Use Fraunces for every heading, pull quote, or large number — exploit its variable axes.
- Use Geist for all body prose and interactive question text.
- Keep border-radius at `0` or `4px` maximum. This is a rectilinear system.
- Layer backgrounds: `--paper` → `--paper-2` → `--paper-3` for increasing interactivity depth.
- Use ruled lines (`1px solid var(--rule)`) generously — they are structural, not decorative.
- Make the teal top border on the masthead and footer the visual signature of the document.
- Use `clamp()` for all headline font sizes.
- Indent answer content to align with question text (not with the number badge).

### DON'T
- Don't use purple gradients, rounded cards, or drop shadows (box-shadow for glow only).
- Don't use Inter, Roboto, or system-ui. Always load the three-font stack.
- Don't use border-radius > 4px anywhere.
- Don't add decorative icons from icon libraries — use Unicode symbols (◆, ◈, ◑, ▼, ✅) set in JetBrains Mono.
- Don't use colored backgrounds on cards — depth is conveyed by border + background layering, not fills.
- Don't use uppercase on body prose — uppercase is strictly for labels, badges, and navigation.
- Don't animate layout properties (no width/height transitions).
- Don't use more than two accent colors in any single component.

---

## Composing a New Application in This System

### Page Structure Template

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>APP NAME · Section · Subtitle</title>
  <!-- Font stack: always all three -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght,SOFT,WONK@9..144,300..900,0..100,0..1&family=Geist:wght@300..900&family=JetBrains+Mono:ital,wght@0,300..700;1,300..700&display=swap" rel="stylesheet">
  <style>
    /* 1. CSS variable tokens (dark + light themes) */
    /* 2. Reset + body with grid texture + scanlines + ambient glow */
    /* 3. Page wrapper */
    /* 4. Masthead */
    /* 5. Hero */
    /* 6. Meta bar */
    /* 7. Search bar (if needed) */
    /* 8. Navigation tabs (if needed) */
    /* 9. Section headers */
    /* 10. Content components (accordions, tables, cards) */
    /* 11. Chips / badges */
    /* 12. Footer + colophon */
    /* 13. Animations (rise, panelIn) */
    /* 14. Responsive breakpoints */
    /* 15. Print styles */
  </style>
</head>
<body>
  <button class="theme-toggle" onclick="toggleTheme()" aria-label="Toggle theme">◑</button>
  <div class="page-wrapper">
    <!-- MASTHEAD -->
    <div class="masthead block">
      <span class="left">Context · Subtitle</span>
      <span class="center">◆ APP TITLE · CATEGORY · YEAR ◆</span>
      <span class="right">Date · Edition</span>
    </div>
    <!-- HERO -->
    <section class="hero block">
      <h1>
        <span class="co-name">// Context line in mono</span>
        Main Title &<br>Secondary <em>Accent</em>
      </h1>
      <div class="lede">
        <span class="eyebrow">// Descriptor line</span>
        Lead paragraph describing the tool or content.
      </div>
    </section>
    <!-- META BAR -->
    <div class="meta-bar block">
      <div class="meta-cell">
        <span class="label">Metric Label</span>
        <span class="val big">42</span>
      </div>
      <!-- more cells -->
    </div>
    <!-- CONTENT -->
    <!-- ... tabs, sections, accordions, etc. -->
    <!-- FOOTER -->
    <div class="footer-rule block">
      <span class="left">◈ App Name · Category</span>
      <span class="center">End of Document</span>
      <span class="right">Built for [Name] · [Year]</span>
    </div>
    <p class="colophon block">Set in Fraunces · Geist · JetBrains Mono · [Year]</p>
  </div>
  <script>
    /* Theme toggle + localStorage restore */
    /* Tab switching (if needed) */
    /* Accordion toggle (if needed) */
    /* Search/filter (if needed) */
  </script>
</body>
</html>
```

### Adapting Content Components
- **Data tables**: Use `border: 1px solid var(--rule)` cells, JetBrains Mono for column headers (uppercase, tracked), Geist for cell data. Teal for primary value column.
- **Progress bars / meters**: `background: var(--rule)` track, `background: var(--teal)` fill, `box-shadow: 0 0 8px rgba(0,200,160,0.3)` on fill.
- **Buttons**: `background: transparent`, `border: 1.5px solid var(--teal)`, `color: var(--teal)`, JetBrains Mono uppercase. On hover: invert (fill teal, text becomes `--paper`).
- **Forms / inputs**: Same as search bar — `border-left: 2px solid var(--teal)`, focus glow `0 0 0 3px rgba(0,200,160,0.1)`.
- **Code blocks**: `background: var(--code-bg)`, `color: var(--code-text)`, `border: 1px solid var(--rule)`, JetBrains Mono, `font-size: 0.82rem`.
- **Badges / status pills**: Chip pattern — `border: 1px solid var(--ACCENT)`, `color: var(--ACCENT)`, `background: rgba(R,G,B,0.05)`, JetBrains Mono, `0.66rem`, sharp corners.
