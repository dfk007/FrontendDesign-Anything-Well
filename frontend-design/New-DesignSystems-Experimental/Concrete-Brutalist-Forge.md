---
name: concrete-brutalist-forge
description: >
  Raw neo-brutalist design system for developer tools, AI sandboxes, and
  data-dense internal platforms. Cream/black/ink palette with a single
  electric-lime forge accent, oversized condensed display type, thick 3-4px
  structural borders, zero shadows, zero gradients, zero rounded corners.
  Font stack: Space Grotesk (display/UI), IBM Plex Mono (data/labels).
  Signature: exposed grid seams, flip-on-hover buttons, heavy rule dividers,
  and a "forged ribbon" thick progress bar. Use for CLI-adjacent web apps,
  internal admin tools, dev consoles, and infra dashboards that should feel
  industrial, structural, and unapologetically raw rather than polished.
---

# Concrete Brutalist Forge — Design System Skill

## Concept & Aesthetic Direction

This system fuses 1960s brutalist architecture (poured concrete, exposed
structure, no ornament) with contemporary neo-brutalism (thick borders,
flat color, deliberate visual weight) and industrial workshop signage
(stencil-adjacent condensed type, hazard-stripe accenting used sparingly).

The feel is **built, not decorated**. Every border is structural — it exists
because two regions meet, not because it looks nice. Color is almost
entirely absent except for one forge-lime accent that reads as "live" or
"active," like a pilot light. There is no blur, no drop shadow, no
gradient, no glassmorphism anywhere in this system.

**Use for**: developer dashboards, AI experiment/eval consoles, infra
admin panels, CLI-adjacent web tools, internal build/deploy status boards,
data explorers.

**Do not use for**: consumer marketing sites, e-commerce, onboarding flows,
anything that needs to feel warm or inviting on first contact.

---

## Typography

**Google Fonts import (verified, free):**
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300..700&family=IBM+Plex+Mono:ital,wght@0,400;0,500;0,600;0,700;1,400&display=swap" rel="stylesheet">
```

### Space Grotesk — Display & UI
Used for all headings, buttons, and interactive labels that are not pure
metadata. Its slightly geometric, slightly irregular letterforms read as
"constructed" rather than corporate.

| Role | Size | Weight | Line-height | Letter-spacing |
|---|---|---|---|---|
| Hero display | `clamp(2.75rem, 7vw, 5.25rem)` | 700 | 0.94 | `-0.03em` |
| Hero sub-line | `1.35rem` | 500 | 1.3 | `-0.01em` |
| Section title | `1.7rem` | 700 | 1.1 | `-0.015em` |
| Card title | `1.05rem` | 600 | 1.3 | normal |
| Body / prose | `0.95rem` | 400 | 1.6 | normal |
| Button label | `0.85rem` | 600 | 1 | `0.02em` |

No italics anywhere in this system. Emphasis is carried by weight jump
(400→700) or by the accent color, never by slanting text.

### IBM Plex Mono — Data & Labels
Used for every number, every metadata label, every tab, every table cell,
every code fragment, every index/ID.

| Role | Size | Weight | Letter-spacing | Transform |
|---|---|---|---|---|
| Eyebrow / section tag | `0.7rem` | 600 | `0.14em` | uppercase |
| Nav / tab label | `0.78rem` | 500 | `0.06em` | uppercase |
| Data cell / table value | `0.85rem` | 400 | normal | none |
| Big stat number | `2.4rem` | 700 | `-0.02em` | none |
| Code block | `0.82rem` | 400 | normal | none |
| Index badge (row numbers) | `0.72rem` | 600 | `0.04em` | none |

**Decision rule**: if it's a proper noun, sentence, or explanatory prose →
Space Grotesk. If it's a number, code, status, ID, or label → IBM Plex
Mono. There is no third font and no exception.

---

## Color System

```css
:root {
  /* Structural surfaces */
  --ink:        #0A0A0A;   /* near-black, primary dark surface */
  --paper:      #F7F4EC;   /* warm off-white/cream, primary light surface */
  --surface:    #141414;   /* card/panel surface on dark */
  --surface-2:  #1F1F1F;   /* elevated/hover surface on dark */

  /* Text */
  --text-hi:    #F7F4EC;   /* primary text on dark */
  --text-lo:    #A8A29A;   /* secondary/muted text on dark */
  --text-on-paper: #0A0A0A;

  /* Structural lines — always thick, always solid, never blurred */
  --line:       #3A3A3A;   /* standard border on dark */
  --line-hi:    #F7F4EC;   /* high-contrast border (rare, emphasis only) */

  /* The one accent — forge lime */
  --forge:      #C6FF00;
  --forge-dim:  rgba(198, 255, 0, 0.10);   /* fill for active/selected state */
  --forge-line: rgba(198, 255, 0, 0.35);   /* subtle grid tint */

  /* Status (used sparingly, same weight as forge, never combined with it) */
  --status-warn: #FF8A00;
  --status-bad:  #FF3B3B;
  --status-good: var(--forge);
}

[data-theme="light"] {
  --ink:        #F7F4EC;
  --paper:      #0A0A0A;   /* inverted: "light" theme still has a dark page,
                               only the card surfaces flip to cream — this
                               system is intentionally low on true "light mode"
                               softness; see note below */
  --surface:    #EFEBE0;
  --surface-2:  #E3DECE;
  --text-hi:    #0A0A0A;
  --text-lo:    #5C574C;
  --line:       #C9C3B4;
  --line-hi:    #0A0A0A;
  --forge:      #7A9900;   /* darkened for AA contrast on cream */
  --forge-dim:  rgba(122, 153, 0, 0.10);
  --forge-line: rgba(122, 153, 0, 0.30);
}
```

**Note on theming**: this system is designed dark-first. The light theme
swaps card/panel backgrounds to cream but the outer page shell stays dark
— true "light mode" would dilute the brutalist weight, so light theme here
means "cream panels on ink," not "ink text on white." If a fully light
page is required, invert `--ink` and `--paper` roles directly and darken
`--forge` further for contrast.

**Color rules**:
- Only ONE accent color is visible at a time — `--forge`. Status colors
  exist for error/warning states only and never appear alongside forge in
  the same component.
- Never use `--forge` as a large fill. It is for borders, text, thin rules,
  and small indicator shapes only. Large lime fills read as a warning
  label, not a design accent.
- `--forge-dim` is the only acceptable use of forge as a background — for
  the selected/active state of rows, tabs, and buttons.

---

## Background & Atmosphere

No blur. No radial glow. No noise texture. Atmosphere here comes entirely
from a visible **construction grid** — thin lines that suggest a drafting
table or blueprint, always exactly aligned to the layout grid so they read
as structural rather than decorative.

```css
body {
  background: var(--ink);
  background-image:
    linear-gradient(var(--forge-line) 1px, transparent 1px),
    linear-gradient(90deg, var(--forge-line) 1px, transparent 1px);
  background-size: 64px 64px;
  background-position: -1px -1px;
}
```

There is no `body::before` scanline and no `body::after` glow in this
system — that softness contradicts the brutalist premise. The only
permitted atmospheric effect is the grid above, and it must stay under
`rgba(198,255,0,0.35)` at 1px width so it never competes with content.

**Z-index**: grid is a `background-image` on `body`, not a layered
pseudo-element, so there is no stacking to manage — content sits at the
default stacking context throughout.

---

## Layout

```css
.page-wrapper {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 2rem 5rem;
}
```

### Topbar (not a masthead — a structural header bar)
```css
.topbar {
  border-bottom: 4px solid var(--line-hi);
  padding: 1.4rem 0;
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: center;
  gap: 2rem;
}
.topbar .mark {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 700;
  font-size: 1.1rem;
  letter-spacing: -0.02em;
}
.topbar .mark::before {
  content: '■';
  color: var(--forge);
  margin-right: 0.5rem;
  font-size: 0.7em;
}
.topbar nav {
  display: flex;
  gap: 1.8rem;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 0.78rem;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  justify-self: center;
}
```

### Hero — left-aligned, massive, thick left rule
```css
.hero {
  padding: 4rem 0 3rem;
  border-bottom: 4px solid var(--line);
  display: grid;
  grid-template-columns: 4px 1fr;
  gap: 2rem;
}
.hero .rule { background: var(--forge); }
.hero h1 {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 700;
  font-size: clamp(2.75rem, 7vw, 5.25rem);
  line-height: 0.94;
  letter-spacing: -0.03em;
}
.hero .sub {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 500;
  font-size: 1.35rem;
  color: var(--text-lo);
  margin-top: 1rem;
  max-width: 46ch;
}
```

### Structural grid (12-col, gutters visible via border, not gap alone)
```css
.grid-12 {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  border-top: 3px solid var(--line);
  border-left: 3px solid var(--line);
}
.grid-12 > * {
  border-right: 3px solid var(--line);
  border-bottom: 3px solid var(--line);
  padding: 1.5rem;
}
```
This "shared border" grid is the system's core layout idiom — cells never
have their own independent border-radius or shadow; they are simply
compartments in a poured slab.

---

## Components

### Thick-Border Card
```css
.card {
  background: var(--surface);
  border: 3px solid var(--line);
  border-radius: 0;
  padding: 1.75rem;
  transition: border-color 0.12s linear;
}
.card:hover { border-color: var(--forge); }
.card .card-eyebrow {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 0.7rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--forge);
  margin-bottom: 0.6rem;
}
```

### Flip-on-Hover Button (signature interactive idiom)
```css
.btn {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 600;
  font-size: 0.85rem;
  letter-spacing: 0.02em;
  padding: 0.9rem 1.6rem;
  background: transparent;
  color: var(--text-hi);
  border: 3px solid var(--line-hi);
  border-radius: 0;
  cursor: pointer;
  transition: background 0.1s linear, color 0.1s linear, border-color 0.1s linear;
}
.btn:hover {
  background: var(--forge);
  color: var(--ink);
  border-color: var(--forge);
}
.btn.primary {
  background: var(--forge);
  color: var(--ink);
  border-color: var(--forge);
}
.btn.primary:hover {
  background: transparent;
  color: var(--forge);
}
```
No easing curves, no `ease-in-out` — transitions use `linear` at 100–120ms
to feel mechanical/instant rather than soft.

### Forged Ribbon (progress / status bar)
```css
.ribbon {
  height: 8px;
  background: var(--surface-2);
  border: 2px solid var(--line);
  position: relative;
}
.ribbon .fill {
  height: 100%;
  background: var(--forge);
  /* width set inline via JS/style, e.g. width: 62% */
}
```

### Data Row (table-like list item)
```css
.data-row {
  display: grid;
  grid-template-columns: 48px 1fr auto;
  align-items: center;
  gap: 1rem;
  padding: 0.9rem 0;
  border-bottom: 2px solid var(--line);
  font-family: 'IBM Plex Mono', monospace;
  font-size: 0.85rem;
}
.data-row .idx { color: var(--forge); font-weight: 600; }
.data-row:hover { background: var(--surface-2); }
```

### Accordion (thick top border activates)
```css
.accordion-item {
  border: 3px solid var(--line);
  border-top-width: 3px;
  margin-top: -3px; /* collapse shared borders */
}
.accordion-item.open { border-top: 3px solid var(--forge); }
.accordion-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.1rem 1.4rem;
  cursor: pointer;
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 600;
}
.accordion-body {
  display: none;
  padding: 0 1.4rem 1.4rem;
  font-size: 0.9rem;
  color: var(--text-lo);
  border-top: 2px solid var(--line);
}
.accordion-item.open .accordion-body { display: block; }
```

### Status Badge
```css
.badge {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 0.7rem;
  font-weight: 600;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  padding: 0.3rem 0.7rem;
  border: 2px solid currentColor;
  border-radius: 0;
}
.badge.good { color: var(--forge); }
.badge.warn { color: var(--status-warn); }
.badge.bad  { color: var(--status-bad); }
```

---

## Animation & Motion

Motion in this system is **mechanical, not soft** — short linear
transitions, no eases, no fades-with-blur, no springy overshoot.

```css
* { transition-timing-function: linear; }

@keyframes slam-in {
  from { opacity: 0; transform: translateY(6px); }
  to   { opacity: 1; transform: translateY(0); }
}
.block { animation: slam-in 0.18s linear forwards; }
.block:nth-child(2) { animation-delay: 0.04s; }
.block:nth-child(3) { animation-delay: 0.08s; }
.block:nth-child(4) { animation-delay: 0.12s; }
```

Standard transition durations: **100–180ms, always `linear`**. No
component in this system should ever use `ease`, `ease-in-out`, or any
duration above 200ms.

---

## Responsive Breakpoints

```css
@media (max-width: 860px) {
  .hero { grid-template-columns: 3px 1fr; gap: 1.25rem; }
  .grid-12 { grid-template-columns: repeat(4, 1fr); }
  .topbar { grid-template-columns: 1fr auto; }
  .topbar nav { display: none; } /* replace with a mono "MENU" toggle */
  .card { padding: 1.25rem; }
}
```

## Print

```css
@media print {
  body { background: #fff; }
  .accordion-body { display: block !important; }
  .btn, .topbar nav { display: none; }
}
```

---

## Design Rules — Do & Don't

### Do
- Use `border: 3px solid` or `4px solid` as the only method of separating
  regions — never `box-shadow`, never `border-radius`.
- Keep `--forge` to borders, text, thin fills (`--forge-dim`), and small
  marks (`■`, ribbon fills). Never a large background fill.
- Use `linear` transitions at 100–180ms everywhere.
- Let borders touch/collapse between adjacent components (shared-border
  grid idiom) rather than adding gaps.
- Use IBM Plex Mono uppercase for every label, tab, and metadata string.

### Don't
- Never use `border-radius` above `0px` anywhere in this system.
- Never use `box-shadow`, `filter: blur()`, or `backdrop-filter`.
- Never use a gradient of any kind, including on hover states.
- Never combine `--forge` with `--status-warn` or `--status-bad` in the
  same component — pick one signal color per element.
- Never use `ease` or `ease-in-out` — motion must feel instant/mechanical.
- Never italicize text; use weight jumps for emphasis instead.

---

## Composing a New Application in This System

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>APP NAME — Concrete Brutalist Forge</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300..700&family=IBM+Plex+Mono:ital,wght@0,400;0,500;0,600;0,700;1,400&display=swap" rel="stylesheet">
  <style>
    /* 1. Tokens (dark + light) */
    /* 2. Reset + body grid background */
    /* 3. .page-wrapper */
    /* 4. .topbar */
    /* 5. .hero */
    /* 6. .grid-12 structural layout */
    /* 7. .card, .btn, .ribbon, .data-row, .accordion-item, .badge */
    /* 8. Motion (slam-in keyframe) */
    /* 9. Responsive + print */
  </style>
</head>
<body>
  <div class="page-wrapper">
    <div class="topbar block">
      <span class="mark">APP NAME</span>
      <nav><a href="#">Overview</a><a href="#">Data</a><a href="#">Logs</a></nav>
      <button class="btn">Deploy</button>
    </div>
    <section class="hero block">
      <div class="rule"></div>
      <div>
        <h1>Build Systems<br>That Hold Weight.</h1>
        <p class="sub">Infrastructure tooling with zero decoration and total clarity.</p>
      </div>
    </section>
    <div class="grid-12 block">
      <!-- structural content cells -->
    </div>
  </div>
  <script>
    /* accordion toggle, tab switching, ribbon width updates */
  </script>
</body>
</html>
```

### Adapting other components
- **Forms**: inputs use the same `border: 3px solid var(--line)`, focus
  state swaps border to `--forge`, no glow/shadow on focus — just the
  color change.
- **Tables**: use `.data-row` pattern repeated; header row gets
  `border-bottom: 4px solid var(--line-hi)` instead of 2px.
- **Modals**: no backdrop blur — use a flat `rgba(10,10,10,0.85)` scrim
  and a modal panel with `border: 4px solid var(--line-hi)`.
- **Charts**: bars/lines in `--forge`, gridlines in `--line` at low
  opacity, axis labels in IBM Plex Mono `0.72rem`.
