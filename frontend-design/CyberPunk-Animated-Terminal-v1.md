# SKILL: Frontend Design — Cyberpunk Terminal System
---

## 1. Design Identity

This design system follows a **cyberpunk hacker terminal aesthetic** — the visual language of a futuristic network operations center, digital security dashboard, or sci-fi terminal interface rendered in the browser. It is not "corporate SaaS." It is not "minimalist white." It is glowing neon on void-black, where every pixel feels like it's alive with data and every element pulses with electric energy.

**Core character:**
- Deep void-black backgrounds (#0a0e1a) with subtle animated grid overlays
- A dual-family type system (futuristic display · monospace utility)
- Neon green (#00ff41) as the primary data colour; neon cyan (#00d9ff) for headings; neon magenta (#ff00ff) for accent/warning states
- Glowing borders, box-shadows, and text-shadows as the primary structural device — everything emits light
- Animated scan-line borders on cards (rainbow gradient sweep)
- Terminal-style code blocks with pulsing cursor aesthetic and dot-decorated headers
- A persistent dark-only mode — light theme is fundamentally incompatible with this system

---

## 2. Typography System

Use **exactly two font families**. Never substitute or expand this list without strong justification.

| Role | Font | Usage |
|---|---|---|
| Display / Headings | `Orbitron` (wght 400, 700, 900) | Hero titles, section headings, panel numbers, all-caps markers |
| Body / Code / UI | `Fira Code` (wght 300, 400, 500, 700) | Body text, code blocks, navigation, labels, terminal output, everything else |

**Google Fonts import (always include both):**
```html
<link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;500;700&family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet">
```

### Orbitron usage rules

| Context | Weight | Style | Size |
|---|---|---|---|
| Hero H1 | 900 | uppercase | 2.8rem, letter-spacing 4px |
| Card H2 | 700 | uppercase | 1.8rem, letter-spacing 2px |
| Tab number / phase label | 700 | uppercase | 0.9–1.4rem |
| Small accent heading | 400 | uppercase | 0.75–1rem |

**Rule:** `Orbitron` is reserved for headings and structural markers exclusively. All body copy, labels, code, and UI text use `Fira Code`. This split creates the signature "command console with futuristic headers" look.

### Type scale

```css
/* Hero H1 */
font-family: 'Orbitron', sans-serif;
font-size: 2.8rem; font-weight: 900; text-transform: uppercase;
letter-spacing: 4px; line-height: 1.1;

/* Card H2 */
font-family: 'Orbitron', sans-serif;
font-size: 1.8rem; font-weight: 700; text-transform: uppercase;
letter-spacing: 2px; line-height: 1.2;

/* Body */
font-family: 'Fira Code', monospace;
font-size: 0.95rem; line-height: 1.7;

/* Subtitle / dim text */
font-family: 'Fira Code', monospace;
font-size: 0.9rem; letter-spacing: 1–2px; color: var(--text-dim);

/* Mono labels / badges */
font-family: 'Fira Code', monospace;
font-size: 0.65–0.75rem; letter-spacing: 1px; text-transform: uppercase;

/* Key cap */
font-family: 'Fira Code', monospace;
font-size: 0.9em; font-weight: 700;
```

---

## 3. Colour System

This is a **dark-only** system. There is no light theme. The aesthetic is fundamentally predicated on light-on-dark contrast — glowing elements against void space.

```css
:root {
  /* Core neons */
  --neon-green:       #00ff41;
  --neon-cyan:        #00d9ff;
  --neon-pink:        #ff00ff;

  /* Backgrounds (deep void blacks) */
  --dark-bg:          #0a0e1a;
  --darker-bg:        #050810;
  --terminal-bg:      #0d1117;

  /* Borders and rules */
  --border-glow:      rgba(0, 255, 65, 0.3);

  /* Text levels */
  --text-bright:      #ffffff;
  --text-dim:         #8b949e;

  /* Semantic accents */
  --warning-red:      #ff4757;
  --success-green:    #2ed573;
}
```

**Colour usage rules:**
- `--neon-green` = primary data colour, body text (on dark), terminal output text, active states, list markers, code highlights, strong text
- `--neon-cyan` = heading colour, h1 glow, prompt markers (`> `), info alert accent, tab hover glow, link colour
- `--neon-pink` = advanced/optional badge, secondary attack paths, dashed-border optional phases, accent border on advanced elements
- `--warning-red` = danger, required badges, warning alerts, failure states
- `--success-green` = success messages, verified states, positive output
- `--text-dim` = secondary body copy, subtitle text, list body text, table data cells
- `--dark-bg` / `--darker-bg` / `--terminal-bg` = layered background depths (darkest for page, mid for terminal, lightest for cards/panels)

---

## 4. Background Texture

Two layers always compose the page background:

### Layer 1 — Animated grid
```css
body::before {
  content: '';
  position: fixed;
  top: 0; left: 0;
  width: 100%; height: 100%;
  background-image:
    linear-gradient(rgba(0, 255, 65, 0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0, 255, 65, 0.03) 1px, transparent 1px);
  background-size: 50px 50px;
  animation: gridScroll 20s linear infinite;
  pointer-events: none;
  z-index: -1;
}

@keyframes gridScroll {
  0%   { transform: translateY(0); }
  100% { transform: translateY(50px); }
}
```

No noise/grain layer — the animated grid IS the texture. The slow vertical scroll creates the "data flowing through the net" feeling that defines cyberpunk atmosphere.

---

## 5. Layout Architecture

### Container
```css
.container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 2rem;
}
```

### Header (sticky command bar)
The header is a fixed, sticky banner at the top with a bottom neon border and box-shadow glow.

```css
header {
  background: linear-gradient(135deg, var(--darker-bg) 0%, var(--terminal-bg) 100%);
  border-bottom: 2px solid var(--neon-green);
  box-shadow: 0 4px 20px rgba(0, 255, 65, 0.2);
  padding: 2rem;
  text-align: center;
  position: sticky;
  top: 0;
  z-index: 100;
  animation: slideDown 0.6s ease-out;
}
```

### Tab Navigation
Horizontal row of tab buttons with a bottom border glow. Active tab gets a glowing green border and gradient background.

```css
.tab-nav {
  display: flex;
  gap: 0.5rem;
  margin: 2rem 0;
  border-bottom: 2px solid var(--border-glow);
  overflow-x: auto;
}

.tab-button {
  background: var(--terminal-bg);
  color: var(--text-dim);
  border: 1px solid transparent;
  padding: 1rem 1.5rem;
  cursor: pointer;
  font-family: 'Fira Code', monospace;
  font-size: 0.9rem;
  font-weight: 500;
  transition: all 0.3s ease;
  position: relative;
  white-space: nowrap;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.tab-button::before {
  content: '> ';
  color: var(--neon-green);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.tab-button:hover {
  color: var(--neon-cyan);
  border-color: var(--neon-cyan);
  box-shadow: 0 0 15px rgba(0, 217, 255, 0.3);
}

.tab-button.active {
  background: linear-gradient(135deg, rgba(0, 255, 65, 0.1) 0%, rgba(0, 217, 255, 0.1) 100%);
  color: var(--neon-green);
  border-color: var(--neon-green);
  box-shadow: 0 0 20px var(--border-glow);
}

.tab-button.active::before {
  opacity: 1;
}
```

**Critical rule:** The `> ` prefix before active tab text is a signature marker — it appears on `:active` and `:hover` states, always in `--neon-green`, always with `opacity: 0 → 1` transition.

---

## 6. Component Library

### 6.1 Cards

Cards use a gradient dark background with a glowing border. The signature feature is the **animated scan-line border** — a `::before` pseudo-element with a rainbow gradient that sweeps across the top.

```css
.card {
  background: linear-gradient(135deg, var(--terminal-bg) 0%, var(--darker-bg) 100%);
  border: 1px solid var(--border-glow);
  border-radius: 8px;
  padding: 2rem;
  margin: 2rem 0;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
  position: relative;
  overflow: hidden;
}

.card::before {
  content: '';
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 3px;
  background: linear-gradient(90deg, var(--neon-green), var(--neon-cyan), var(--neon-pink));
  animation: borderScan 3s linear infinite;
}

@keyframes borderScan {
  0%   { transform: translateX(-100%); }
  100% { transform: translateX(100%); }
}
```

**Card heading rules:**
- `h2` inside `.card` → `Orbitron`, `--neon-cyan`, 1.8rem, uppercase, letter-spacing 2px
- `h3` inside `.card` → `Fira Code`, `--neon-green`, 1.3rem, weight 700
- `p` and `li` inside `.card` → `--text-dim`, line-height 1.8
- `strong` inside `.card` → `--neon-green`, weight 700

### 6.2 Terminal / Code blocks

The terminal block is the second most recognisable element. Pure black background with neon green border and dual box-shadow (outer glow + inner glow).

```css
.terminal {
  background: #000;
  border: 2px solid var(--neon-green);
  border-radius: 6px;
  padding: 1.5rem;
  margin: 1.5rem 0;
  font-family: 'Fira Code', monospace;
  font-size: 0.9rem;
  overflow-x: auto;
  box-shadow:
    0 0 20px rgba(0, 255, 65, 0.2),
    inset 0 0 30px rgba(0, 255, 65, 0.05);
  position: relative;
}

.terminal::before {
  content: '● ● ●';
  position: absolute;
  top: -25px; left: 10px;
  color: var(--text-dim);
  font-size: 1.2rem;
  letter-spacing: 8px;
}

.terminal pre {
  margin: 0;
  color: var(--neon-green);
  white-space: pre-wrap;
  word-wrap: break-word;
}
```

**Terminal text classes:**
```css
.terminal .prompt  { color: var(--neon-cyan); font-weight: 700; }
.terminal .comment  { color: #6a737d; font-style: italic; }
.terminal .output   { color: var(--success-green); }
.terminal .warning  { color: var(--warning-red); }
```

### 6.3 Steps (numbered process)

Circular neon gradient step numbers, horizontally laid out with content.

```css
.step {
  display: flex;
  gap: 1.5rem;
  margin: 2rem 0;
  align-items: flex-start;
}

.step-number {
  background: linear-gradient(135deg, var(--neon-green), var(--neon-cyan));
  color: var(--dark-bg);
  font-weight: 900;
  font-size: 1.5rem;
  width: 50px; height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  flex-shrink: 0;
  box-shadow: 0 0 20px rgba(0, 255, 65, 0.5);
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50%      { transform: scale(1.05); }
}

.step-content { flex: 1; }
```

### 6.4 Alert boxes

Three semantic variants — warning (red), info (cyan), success (green). Always left-border-accented with translucent background.

```css
.alert {
  border-left: 4px solid;
  padding: 1rem 1.5rem;
  margin: 1.5rem 0;
  border-radius: 4px;
  background: rgba(0, 0, 0, 0.5);
}

.alert-warning {
  border-color: var(--warning-red);
  background: rgba(255, 71, 87, 0.1);
}
.alert-warning strong { color: var(--warning-red); }

.alert-info {
  border-color: var(--neon-cyan);
  background: rgba(0, 217, 255, 0.1);
}
.alert-info strong { color: var(--neon-cyan); }

.alert-success {
  border-color: var(--success-green);
  background: rgba(46, 213, 115, 0.1);
}
.alert-success strong { color: var(--success-green); }
```

### 6.5 Badges

Small, rounded pill badges with uppercase text and colour-coded borders.

```css
.badge {
  display: inline-block;
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-right: 0.5rem;
}

.badge-required {
  background: rgba(255, 71, 87, 0.2);
  color: var(--warning-red);
  border: 1px solid var(--warning-red);
}

.badge-optional {
  background: rgba(0, 217, 255, 0.2);
  color: var(--neon-cyan);
  border: 1px solid var(--neon-cyan);
}

.badge-advanced {
  background: rgba(255, 0, 255, 0.2);
  color: var(--neon-pink);
  border: 1px solid var(--neon-pink);
}
```

### 6.6 Tables

Dark-themed tables with gradient header row and subtle green border glow.

```css
table {
  width: 100%;
  border-collapse: collapse;
  margin: 1.5rem 0;
}

table th {
  background: linear-gradient(135deg, rgba(0, 255, 65, 0.2), rgba(0, 217, 255, 0.2));
  color: var(--neon-cyan);
  padding: 1rem;
  text-align: left;
  font-weight: 700;
  border: 1px solid var(--border-glow);
}

table td {
  padding: 1rem;
  border: 1px solid var(--border-glow);
  color: var(--text-dim);
}

table tr:hover {
  background: rgba(0, 255, 65, 0.05);
}
```

### 6.7 Illustration containers

For SVG diagrams and flowcharts — dark bordered containers that frame technical illustrations.

```css
.illustration {
  background: rgba(0, 0, 0, 0.6);
  border: 1px solid var(--border-glow);
  border-radius: 8px;
  padding: 2rem;
  margin: 2rem 0;
  text-align: center;
}

.illustration svg {
  max-width: 100%;
  height: auto;
}
```

**SVG illustration rules:** Use `var()` colour references in CSS context; inside SVGs, use the same hex values: `#0d1117` for boxes, `#00ff41` for green strokes/text, `#00d9ff` for cyan strokes/text, `#ff00ff` for pink dashed strokes, `#8b949e` for dim text, `#0a0e1a` for SVG backgrounds.

### 6.8 Inline code / formula tokens

```css
code {
  background: rgba(0, 255, 65, 0.1);
  color: var(--neon-green);
  padding: 0.2rem 0.5rem;
  border-radius: 3px;
  font-family: 'Fira Code', monospace;
  font-size: 0.9em;
}
```

### 6.9 Key cap (keyboard shortcut display)

```css
.key {
  display: inline-block;
  background: var(--terminal-bg);
  border: 2px solid var(--neon-green);
  padding: 0.2rem 0.6rem;
  border-radius: 4px;
  font-family: 'Fira Code', monospace;
  font-weight: 700;
  color: var(--neon-green);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
}
```

### 6.10 Lists

```css
ul, ol {
  margin-left: 2rem;
  margin-bottom: 1rem;
}

li { margin-bottom: 0.5rem; }
li::marker { color: var(--neon-green); }
```

---

## 7. Animation Patterns

### Header entrance (slide down)
```css
@keyframes slideDown {
  from { transform: translateY(-100%); opacity: 0; }
  to   { transform: translateY(0); opacity: 1; }
}
```

### H1 glow pulse
```css
@keyframes glow {
  from { text-shadow: 0 0 10px var(--neon-cyan), 0 0 20px var(--neon-cyan); }
  to   { text-shadow: 0 0 20px var(--neon-cyan), 0 0 40px var(--neon-cyan), 0 0 60px rgba(0, 217, 255, 0.8); }
}
```

### Generic fade-in (for sections, tabs, cards)
```css
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}
```

### Tab content entrance
```css
@keyframes fadeInContent {
  from { opacity: 0; transform: translateX(-20px); }
  to   { opacity: 1; transform: translateX(0); }
}
```

### Card scan-line sweep
```css
@keyframes borderScan {
  0%   { transform: translateX(-100%); }
  100% { transform: translateX(100%); }
}
```

### Step number pulse
```css
@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50%      { transform: scale(1.05); }
}
```

### Background grid scroll
```css
@keyframes gridScroll {
  0%   { transform: translateY(0); }
  100% { transform: translateY(50px); }
}
```

---

## 8. Scrollbar Styling

Neon-styled scrollbars are part of the immersive experience.

```css
::-webkit-scrollbar { width: 12px; height: 12px; }
::-webkit-scrollbar-track { background: var(--darker-bg); }
::-webkit-scrollbar-thumb {
  background: var(--neon-green);
  border-radius: 6px;
  box-shadow: 0 0 10px var(--neon-green);
}
::-webkit-scrollbar-thumb:hover { background: var(--neon-cyan); }
```

---

## 9. Footer

```css
footer {
  text-align: center;
  padding: 3rem 2rem;
  margin-top: 4rem;
  border-top: 2px solid var(--border-glow);
  color: var(--text-dim);
  font-size: 0.9rem;
}

footer a {
  color: var(--neon-cyan);
  text-decoration: none;
  transition: color 0.3s ease;
}

footer a:hover {
  color: var(--neon-green);
  text-shadow: 0 0 10px var(--neon-green);
}
```

---

## 10. Divider / Subtitle

```css
/* Subtitle beneath hero heading with green accent span */
.subtitle {
  color: var(--text-dim);
  font-size: 0.95rem;
  letter-spacing: 2px;
}
.subtitle span {
  color: var(--neon-green);
  font-weight: 700;
}
```

---

## 11. Heading Hierarchy

Every heading level has a defined font, weight, and glow rule.

| Level | Font | Size | Weight | Colour / Effect |
|---|---|---|---|---|
| `h1` (hero) | Orbitron | 2.8rem | 900 | `--neon-cyan` with animated glow text-shadow |
| `.card h2` | Orbitron | 1.8rem | 700 | `--neon-cyan`, uppercase |
| `.card h3` | Fira Code | 1.3rem | 700 | `--neon-green` |

**Critical rule:** `h1` always has animated `text-shadow` glow via the `glow` keyframe animation. This pulsing cyan glow is the header's signature — never remove it.

---

## 12. Responsive Breakpoints

```css
@media (max-width: 768px) {
  h1 { font-size: 2rem; }
  .tab-nav { flex-wrap: wrap; }
  .step { flex-direction: column; }
  .card { padding: 1.5rem; }
}
```

---

## 13. Design Rules — Do and Don't

### ✅ Always do
- Use animated `text-shadow` glow on hero `h1` elements
- Use `box-shadow` with colour-matched rgba for all glow effects (neon green, cyan, pink)
- Use the animated grid overlay on `body::before`
- Use `Orbitron` exclusively for headings and structural markers
- Use `border-radius: 8px` on cards and `6px` on terminals (slight rounding is cyberpunk, not editorial)
- Use the `> ` prefix marker on active/hovered tabs
- Use `border-radius: 50%` on step numbers and `20px` on badges
- Use the scan-line `::before` pseudo-element with `linear-gradient(90deg, green, cyan, pink)` on cards
- Use the `● ● ●` terminal header decoration
- Apply `transition: all 0.3s ease` on interactive elements
- Use gradient backgrounds (`linear-gradient(135deg, ...)`) on cards and headers

### ❌ Never do
- Never use a light background — this system is dark-only
- Never remove the animated grid from `body::before`
- Never use `Orbitron` for body text or long paragraphs
- Never use `Fira Code` for hero/display headings
- Never hardcode hex colours in component CSS — always `var(--token)`
- Never use blurred `box-shadow` without a colour-matched glow (no generic grey shadows)
- Never use `border-radius: 0` on cards (unlike editorial style — slight rounding is correct here)
- Never add a light/dark theme toggle — dark-only is intentional
- Never use serif fonts or warm/paper colours
- Never remove the scan-line animation from card pseudo-elements
- Never use `backdrop-filter: blur()` or glassmorphism — this aesthetic is illuminated screen, not frosted glass

---

## 14. HTML Document Shell

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
  <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;500;700&family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet">
  <style>
    /* 1. CSS variables (dark-only) */
    /* 2. Reset */
    /* 3. Body + animated grid background */
    /* 4. Keyframes (gridScroll, glow, slideDown, fadeIn, borderScan, pulse) */
    /* 5. Layout: header, container, tab-nav */
    /* 6. Components: card, terminal, alert, badge, table, illustration, step, key, code */
    /* 7. Scrollbar styling */
    /* 8. Responsive */
  </style>
</head>
<body>
  <header>
    <h1>Page Title</h1>
    <p class="subtitle">Subtitle with <span>Accent</span></p>
  </header>

  <div class="container">
    <!-- alert banner (optional) -->
    <!-- tab navigation -->
    <!-- tab content panels with cards, terminals, steps, illustrations -->
  </div>

  <footer>
    <p>Footer text</p>
  </footer>

  <script>
    /* tab switching logic */
    const tabButtons = document.querySelectorAll('.tab-button');
    const tabContents = document.querySelectorAll('.tab-content');
    tabButtons.forEach(button => {
      button.addEventListener('click', () => {
        const targetTab = button.getAttribute('data-tab');
        tabButtons.forEach(btn => btn.classList.remove('active'));
        tabContents.forEach(content => content.classList.remove('active'));
        button.classList.add('active');
        document.getElementById(targetTab).classList.add('active');
      });
    });
  </script>
</body>
</html>
```

---

## 15. React/JSX Adaptation Notes

When implementing this system in React:

1. **CSS variables** — define in a global `styles/tokens.css` imported at root; no theme toggle needed (dark-only).
2. **Keyframe animations** — define in global CSS; assign via `className` or `animationName` in style objects.
3. **Tab system** — maintain `activeTab` in `useState`; toggle `.active` class on buttons and panels.
4. **Card scan-line `::before`** — use a real `<div className="card-scan" />` as first child inside card components since CSS Modules may not support `::before` pseudo-elements cleanly.
5. **Terminal `● ● ●` decoration** — render as a real `<span className="terminal-dots">● ● ●</span>` positioned absolutely above the terminal block.
6. **Animated grid** — render as a fixed `<div className="grid-overlay" />` behind all content; apply `pointer-events: none`.
7. **`Orbitron`** — import via the Google Fonts `<link>` in `index.html` or via `@import` in global CSS.

---

---

## ADDENDUM — General Frontend Design Principles (from system skill)

> The following section contains supplemental design guidance from the base `frontend-design` skill. It is additional and secondary; the primary source of truth for this design system is Sections 1–15 above.

```
ADDENDUM: General Frontend Design Principles (from system skill)

## Design Thinking Before Coding
Before writing any markup, commit to a BOLD aesthetic direction:
- Purpose: What problem does this interface solve? Who uses it?
- Tone: Pick an extreme — brutally minimal, maximalist chaos, retro-futuristic,
  organic/natural, luxury/refined, playful/toy-like, editorial/magazine,
  brutalist/raw, art deco/geometric, soft/pastel, industrial/utilitarian, etc.
  THIS FILE = cyberpunk neon terminal
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
