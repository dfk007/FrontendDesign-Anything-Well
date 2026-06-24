# SKILL: Frontend Design — CyberPunk Terminal System
> Derived from `example-html-CyberPunk.html` · Daud's house style (dark variant)

---

## 1. Design Identity

This design system follows a **hacker terminal / cyberpunk aesthetic** — the visual language of a live command-line environment rendered as a rich, animated web document. It is the polar opposite of the editorial print system. Everything is dark, electric, and alive. The page breathes with pulsing glows, a scrolling grid background, and scan-line animations. It is a document that feels like a running process.

**Core character:**
- Near-black void backgrounds with a faint animated green grid that scrolls vertically
- A strict dual-family type system: `Orbitron` (display, uppercase, futuristic) + `Fira Code` (body, monospace, terminal)
- Neon colour triad: electric green, cyan, and magenta — each carrying a semantic role
- Glowing `box-shadow` and `text-shadow` are the primary depth mechanism (not drop shadows, not blur-only — actual glow bloom)
- `border-radius: 6–8px` on cards and terminal blocks — slightly rounded, not hard-cut
- A scanning chromatic gradient stripe animates across every card top (`borderScan`)
- Sticky header with `box-shadow` glow, animated entrance via `slideDown`
- No light/dark toggle — this system is **permanently dark**; a dark mode is its only mode

---

## 2. Typography System

Use **exactly two font families**. Both are monospace-adjacent. There is no serif option in this system.

| Role | Font | Usage |
|---|---|---|
| Display / Headings | `Orbitron` (wght 400, 700, 900) | H1 page title, card H2, section labels |
| Body / Terminal / UI | `Fira Code` (wght 300, 400, 500, 700) | All body text, code, tabs, badges, captions, everything else |

**Google Fonts import (always include both):**
```html
<link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;500;700&family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet">
```

### Font role assignments

```css
body         { font-family: 'Fira Code', monospace; }         /* global default */
h1           { font-family: 'Orbitron', sans-serif; }         /* page hero */
.card h2     { font-family: 'Orbitron', sans-serif; }         /* card section title */
.tab-button  { font-family: 'Fira Code', monospace; }         /* navigation */
.terminal    { font-family: 'Fira Code', monospace; }         /* code/terminal */
.badge       { font-family: 'Fira Code', monospace; }         /* status badges */
```

### Type scale

```css
/* Page H1 (Orbitron) */
font-size: 2.8rem;     font-weight: 900;    letter-spacing: 4px;    text-transform: uppercase;

/* Card H2 (Orbitron) */
font-size: 1.8rem;     font-weight: 700;    letter-spacing: 2px;    text-transform: uppercase;

/* Card H3 (Fira Code) */
font-size: 1.3rem;     font-weight: 700;

/* Body / card p, li (Fira Code) */
font-size: 1rem;       line-height: 1.8;

/* Tab button (Fira Code) */
font-size: 0.9rem;     font-weight: 500;    letter-spacing: 1px;    text-transform: uppercase;

/* Terminal pre (Fira Code) */
font-size: 0.9rem;     line-height: 1.7;

/* Subtitle / meta (Fira Code) */
font-size: 0.95rem;    letter-spacing: 2px;

/* Badge (Fira Code) */
font-size: 0.75rem;    font-weight: 700;    letter-spacing: 1px;    text-transform: uppercase;

/* Inline code (Fira Code) */
font-size: 0.9em;
```

**Rule:** `Orbitron` is reserved exclusively for titles. Everything interactive and informational stays in `Fira Code`. Never mix them at the same heading level.

---

## 3. Colour System

This system has **no CSS variable theming toggle**. All variables are declared once on `:root`. There is no `[data-theme="dark"]` counterpart — dark is the only mode.

```css
:root {
  /* Neon primaries */
  --neon-green:    #00ff41;   /* PRIMARY — default text, borders, list markers, prompts, glow source */
  --neon-cyan:     #00d9ff;   /* SECONDARY — H1 title, card H2, hover states, arrows, info alerts */
  --neon-pink:     #ff00ff;   /* TERTIARY — advanced/optional badges, dashed borders, special nodes */

  /* Dark backgrounds */
  --dark-bg:       #0a0e1a;   /* page background (deepest usable dark, not pure black) */
  --darker-bg:     #050810;   /* gradient endpoint, header background, card gradient end */
  --terminal-bg:   #0d1117;   /* card body bg, tab button bg, terminal-like surfaces */

  /* Glow border */
  --border-glow:   rgba(0, 255, 65, 0.3);   /* default glowing border colour */

  /* Text */
  --text-dim:      #8b949e;   /* body text, list items, table cells, secondary copy */

  /* Status colours */
  --warning-red:   #ff4757;   /* danger alerts, required badges, evil-twin borders */
  --success-green: #2ed573;   /* output text in terminals, success alerts */
}
```

### Semantic colour assignment

| Element | Colour |
|---|---|
| Page H1 | `--neon-cyan` with 3-layer glow |
| Card H2 | `--neon-cyan` |
| Card H3 | `--neon-green` |
| Body text / `p`, `li` | `--text-dim` |
| `strong` inside cards | `--neon-green` |
| Terminal `pre` text | `--neon-green` |
| Terminal `.prompt` | `--neon-cyan` (bold) |
| Terminal `.comment` | `#6a737d` (italic, darker than dim) |
| Terminal `.output` | `--success-green` |
| Terminal `.warning` | `--warning-red` |
| Alert warning border + label | `--warning-red` |
| Alert info border + label | `--neon-cyan` |
| Alert success border + label | `--success-green` |
| Tab active state | `--neon-green` border + green gradient bg |
| Tab hover state | `--neon-cyan` border + cyan glow shadow |
| Badge required | `--warning-red` |
| Badge optional | `--neon-cyan` |
| Badge advanced | `--neon-pink` |
| Table headers | `--neon-cyan` on green→cyan gradient bg |
| Footer links | `--neon-cyan` → `--neon-green` on hover |
| Scrollbar thumb | `--neon-green` with glow |
| Inline `code` bg | `rgba(0, 255, 65, 0.1)` — faint green wash |

---

## 4. Background

One animated layer composes the entire page background.

### Scrolling green grid (mandatory)

```css
body {
  background: var(--dark-bg);
  overflow-x: hidden;
}

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

The opacity of the grid lines is deliberately very low (`0.03`) — it should be felt, not seen. It creates a sense of dimensional depth without competing with content.

---

## 5. Layout Architecture

### Global container

```css
.container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 2rem;
}
```

Maximum width is wider than typical (1400px) to feel like a terminal filling the screen, not a narrow document.

### Sticky header

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

@keyframes slideDown {
  from { transform: translateY(-100%); opacity: 0; }
  to   { transform: translateY(0); opacity: 1; }
}
```

The header always slides in on page load — this is non-negotiable. The `border-bottom: 2px solid --neon-green` is the green horizon line that anchors all content below.

### Subtitle pattern

```css
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

Subtitles always highlight a key noun with `--neon-green` inside a `<span>`.

### Footer

```css
footer {
  text-align: center;
  padding: 3rem 2rem;
  margin-top: 4rem;
  border-top: 2px solid var(--border-glow);
  color: var(--text-dim);
  font-size: 0.9rem;
}
footer a { color: var(--neon-cyan); text-decoration: none; transition: color 0.3s ease; }
footer a:hover { color: var(--neon-green); text-shadow: 0 0 10px var(--neon-green); }
```

---

## 6. Component Library

### 6.1 Cards

Cards are the primary content container. They use a `linear-gradient` background, a green glow border, a dark drop shadow, and a **chromatic scanning stripe** that animates across the top edge on every card perpetually.

```css
.card {
  background: linear-gradient(135deg, var(--terminal-bg) 0%, var(--darker-bg) 100%);
  border: 1px solid var(--border-glow);
  border-radius: 8px;
  padding: 2rem;
  margin: 2rem 0;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
  position: relative;
  overflow: hidden;   /* critical — clips the scanning stripe */
}

/* Chromatic stripe — animates left-to-right on every card indefinitely */
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

.card h2 {
  font-family: 'Orbitron', sans-serif;
  color: var(--neon-cyan);
  font-size: 1.8rem;
  margin-bottom: 1rem;
  text-transform: uppercase;
  letter-spacing: 2px;
}

.card h3    { color: var(--neon-green); font-size: 1.3rem; margin: 1.5rem 0 1rem; font-weight: 700; }
.card p, .card li  { color: var(--text-dim); margin-bottom: 0.8rem; line-height: 1.8; }
.card strong { color: var(--neon-green); font-weight: 700; }
```

**`overflow: hidden` on `.card` is mandatory** — without it, the borderScan stripe bleeds outside the card bounds.

### 6.2 Terminal Block

The terminal is a first-class element. It simulates a real terminal window with a `●●●` chrome bar above it, inset and outset neon green glow, and coloured spans for interactive semantic highlighting.

```css
.terminal {
  background: #000;                      /* true black — distinguishable from --darker-bg */
  border: 2px solid var(--neon-green);
  border-radius: 6px;
  padding: 1.5rem;
  margin: 1.5rem 0;
  font-family: 'Fira Code', monospace;
  font-size: 0.9rem;
  overflow-x: auto;
  box-shadow:
    0 0 20px rgba(0, 255, 65, 0.2),       /* outer glow */
    inset 0 0 30px rgba(0, 255, 65, 0.05); /* inner phosphor ambient */
  position: relative;
}

/* macOS-style traffic-light dots — purely decorative chrome */
.terminal::before {
  content: '● ● ●';
  position: absolute;
  top: -25px; left: 10px;
  color: var(--text-dim);
  font-size: 1.2rem;
  letter-spacing: 8px;
}

.terminal pre    { margin: 0; color: var(--neon-green); white-space: pre-wrap; word-wrap: break-word; }
.terminal .prompt  { color: var(--neon-cyan); font-weight: 700; }
.terminal .comment { color: #6a737d; font-style: italic; }
.terminal .output  { color: var(--success-green); }
.terminal .warning { color: var(--warning-red); }
```

**Span class usage in terminal `<pre>` blocks:**

```html
<pre>
<span class="prompt">user@host ~$</span> command --flag value
<span class="comment"># This is a comment</span>
<span class="output">Success: operation complete</span>
<span class="warning">Error: permission denied</span>
</pre>
```

### 6.3 Steps (numbered process)

Steps use a **circular gradient badge** with a pulsing glow animation for the number, and a flex layout for number + content side-by-side.

```css
.step {
  display: flex;
  gap: 1.5rem;
  margin: 2rem 0;
  align-items: flex-start;
}

.step-number {
  background: linear-gradient(135deg, var(--neon-green), var(--neon-cyan));
  color: var(--dark-bg);         /* dark text on bright gradient */
  font-weight: 900;
  font-size: 1.5rem;
  width: 50px; height: 50px;
  display: flex; align-items: center; justify-content: center;
  border-radius: 50%;
  flex-shrink: 0;
  box-shadow: 0 0 20px rgba(0, 255, 65, 0.5);
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50%       { transform: scale(1.05); }
}

.step-content { flex: 1; }
```

The step badge is one of the strongest brand elements — the green→cyan gradient circle with a constant slow pulse. Never replace this with a square or plain number.

### 6.4 Alert boxes

Alerts always use a **left border** as the primary colour signal, a dark semi-transparent background tinted with the alert colour, and a bold `<strong>` label in the accent colour.

```css
.alert {
  border-left: 4px solid;
  padding: 1rem 1.5rem;
  margin: 1.5rem 0;
  border-radius: 4px;
  background: rgba(0, 0, 0, 0.5);
}

/* Warning (red) */
.alert-warning { border-color: var(--warning-red); background: rgba(255, 71, 87, 0.1); }
.alert-warning strong { color: var(--warning-red); }

/* Info (cyan) */
.alert-info { border-color: var(--neon-cyan); background: rgba(0, 217, 255, 0.1); }
.alert-info strong { color: var(--neon-cyan); }

/* Success (green) */
.alert-success { border-color: var(--success-green); background: rgba(46, 213, 115, 0.1); }
.alert-success strong { color: var(--success-green); }
```

**Pattern for alert content:**
```html
<div class="alert alert-warning">
  <strong>⚠️ WARNING LABEL:</strong> Body text in --text-dim continues here.
</div>
```

The emoji prefix before the strong label is standard — `⚠️`, `ℹ️`, `✅` for warning/info/success respectively.

### 6.5 Badges

Inline pill-shaped status tags. Always uppercase, always Fira Code, always with a matching border + tinted background.

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

.badge-required { background: rgba(255, 71, 87, 0.2); color: var(--warning-red);  border: 1px solid var(--warning-red); }
.badge-optional { background: rgba(0, 217, 255, 0.2); color: var(--neon-cyan);   border: 1px solid var(--neon-cyan); }
.badge-advanced { background: rgba(255, 0, 255, 0.2); color: var(--neon-pink);   border: 1px solid var(--neon-pink); }
```

### 6.6 Tables

Tables use a gradient header row (green→cyan gradient, low opacity), and a hover row highlight in faint green. All borders reference `--border-glow`.

```css
table { width: 100%; border-collapse: collapse; margin: 1.5rem 0; }

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

table tr:hover { background: rgba(0, 255, 65, 0.05); }
```

### 6.7 Inline code token

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

### 6.8 Keyboard key token

For keyboard shortcut notation or literal key display:

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

### 6.9 Illustration container

For SVG diagrams and inline graphics:

```css
.illustration {
  background: rgba(0, 0, 0, 0.6);
  border: 1px solid var(--border-glow);
  border-radius: 8px;
  padding: 2rem;
  margin: 2rem 0;
  text-align: center;
}
.illustration svg { max-width: 100%; height: auto; }
```

**SVG style convention inside illustrations:**
- Background rect: `fill="#0a0e1a"` (matches `--dark-bg`)
- Required phase boxes: `fill="#0d1117"` stroke `#00ff41` solid `stroke-width="2"`
- Optional phase boxes: dashed `stroke-dasharray="5,5"` in `--neon-pink` or `--warning-red`
- Text labels: `font-family="Fira Code"` fill `#00ff41` (labels) or `#8b949e` (subtitles)
- Arrows: `fill="#00d9ff"` cyan `<polygon>` arrowheads
- Optional arrows: dashed stroke in `--neon-pink`

### 6.10 Custom scrollbar (WebKit)

```css
::-webkit-scrollbar           { width: 12px; height: 12px; }
::-webkit-scrollbar-track     { background: var(--darker-bg); }
::-webkit-scrollbar-thumb     { background: var(--neon-green); border-radius: 6px; box-shadow: 0 0 10px var(--neon-green); }
::-webkit-scrollbar-thumb:hover { background: var(--neon-cyan); }
```

This makes the scrollbar part of the aesthetic, not an afterthought.

---

## 7. Navigation: Tab System

Tabs are a flex row of terminal-style buttons with a green glow border on the bottom. They do not use a grid — they overflow-scroll horizontally on mobile.

```css
.tab-nav {
  display: flex;
  gap: 0.5rem;
  margin: 2rem 0;
  border-bottom: 2px solid var(--border-glow);
  overflow-x: auto;
  animation: fadeIn 0.8s ease-out 0.2s both;
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

/* Terminal prompt prefix — appears only on hover and active */
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

.tab-button.active::before { opacity: 1; }

/* Panel entrance */
.tab-content { display: none; animation: fadeInContent 0.5s ease-out; }
.tab-content.active { display: block; }

@keyframes fadeInContent {
  from { opacity: 0; transform: translateX(-20px); }
  to   { opacity: 1; transform: translateX(0); }
}
```

**The `> ` prefix pseudo-element** is the tab system's primary brand detail — it is invisible until hover/active, then snaps on. Do not remove or replace it with another symbol.

**JavaScript tab switching:**

```javascript
const tabButtons  = document.querySelectorAll('.tab-button');
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
```

Note: unlike the editorial system, this tab switcher does **not** restore scroll position or re-trigger staggered block animations. `fadeInContent` re-fires naturally because `display: none` → `display: block` forces CSS animation restart.

---

## 8. Animation Patterns

### H1 neon glow pulse (`glow`) — breathing title effect

```css
@keyframes glow {
  from { text-shadow: 0 0 10px var(--neon-cyan), 0 0 20px var(--neon-cyan); }
  to   { text-shadow: 0 0 20px var(--neon-cyan), 0 0 40px var(--neon-cyan), 0 0 60px rgba(0, 217, 255, 0.8); }
}

h1 {
  color: var(--neon-cyan);
  text-shadow: 0 0 10px var(--neon-cyan), 0 0 20px var(--neon-cyan), 0 0 40px rgba(0, 217, 255, 0.5);
  animation: glow 2s ease-in-out infinite alternate;
}
```

### Header entrance (`slideDown`)

```css
@keyframes slideDown {
  from { transform: translateY(-100%); opacity: 0; }
  to   { transform: translateY(0); opacity: 1; }
}
header { animation: slideDown 0.6s ease-out; }
```

### Tab nav entrance (`fadeIn`)

```css
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}
.tab-nav { animation: fadeIn 0.8s ease-out 0.2s both; }
```

### Tab content slide-in (`fadeInContent`)

```css
@keyframes fadeInContent {
  from { opacity: 0; transform: translateX(-20px); }
  to   { opacity: 1; transform: translateX(0); }
}
```

Content slides in from the left — this gives the impression of navigating deeper into a file system or a terminal session history.

### Card border chromatic scan (`borderScan`)

```css
@keyframes borderScan {
  0%   { transform: translateX(-100%); }
  100% { transform: translateX(100%); }
}
.card::before { animation: borderScan 3s linear infinite; }
```

### Step number pulse (`pulse`)

```css
@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50%       { transform: scale(1.05); }
}
.step-number { animation: pulse 2s ease-in-out infinite; }
```

### Grid background scroll (`gridScroll`)

```css
@keyframes gridScroll {
  0%   { transform: translateY(0); }
  100% { transform: translateY(50px); }
}
body::before { animation: gridScroll 20s linear infinite; }
```

### Glitch effect (optional, for emphasis elements)

```css
@keyframes glitch {
  0%, 100% { transform: translate(0); }
  33%       { transform: translate(-2px, 2px); }
  66%       { transform: translate(2px, -2px); }
}
/* Apply sparingly: .glitch-target { animation: glitch 0.3s ease-in-out; } */
```

---

## 9. Heading Hierarchy

| Level | Font | Size | Weight | Colour |
|---|---|---|---|---|
| `h1` (page) | Orbitron | 2.8rem | 900 | `--neon-cyan` with 3-layer glow |
| `.card h2` | Orbitron | 1.8rem | 700 | `--neon-cyan` |
| `.card h3` | Fira Code | 1.3rem | 700 | `--neon-green` |
| Section label / subtitle | Fira Code | 0.95rem | 400 | `--text-dim` with `span > --neon-green` |

**Rules:**
- `h1` always uses the `glow` animation — a static Orbitron h1 is wrong
- `h2` inside cards is always `--neon-cyan`, never `--neon-green` — this differentiates section titles from body emphasis
- `h3` inside cards is always `--neon-green` — it is the same colour as `strong`, forming a consistency layer
- No `h4` exists in this system — use `h3` or a `strong` label inside a terminal/alert

---

## 10. Lists

```css
ul, ol { margin-left: 2rem; margin-bottom: 1rem; }
li { margin-bottom: 0.5rem; }
li::marker { color: var(--neon-green); }
```

List marker colour is always `--neon-green`. No custom unicode markers or pseudo-elements needed — the browser default `::marker` coloured green is sufficient and correct.

---

## 11. Responsive Breakpoints

```css
@media (max-width: 768px) {
  h1 { font-size: 2rem; }

  .tab-nav {
    flex-wrap: wrap;    /* allow tabs to wrap on small screens */
  }

  .step {
    flex-direction: column;   /* stack number above content */
  }

  .card {
    padding: 1.5rem;
  }
}
```

Mobile handling is intentionally minimal — this is a dense, technical UI built for desktop. On mobile it degrades gracefully to stacked layout and wrapped tabs.

---

## 12. Design Rules — Do and Don't

### ✅ Always do
- Use `text-shadow` with multiple radius layers for all neon glow text (minimum 2 layers: sharp inner + diffuse outer)
- Use `box-shadow` with `rgba(0, 255, 65, 0.2–0.5)` for all interactive elevated surfaces (terminals, step badges, tabs)
- Apply `overflow: hidden` to every `.card` — the `borderScan` stripe will leak otherwise
- Keep the `body::before` grid layer at `opacity` via `rgba(0, 255, 65, 0.03)` — extremely subtle
- Use `border-radius: 6–8px` consistently on cards and terminals; `4px` on alerts and tables
- Always include the `● ● ●` pseudo-element on `.terminal::before` as decorative chrome
- Use the `> ` pseudo-element `::before` on `.tab-button` — it is the tab system's identity marker
- Apply `animation: glow 2s ease-in-out infinite alternate` to every page `h1`
- Keep `--text-dim: #8b949e` as the body copy colour — never use `--neon-green` for paragraphs or it loses signal value
- Scrollbar styling is mandatory — use the neon green thumb with glow

### ❌ Never do
- Never use a light background or light theme — this system has no paper/parchment mode
- Never use `font-family: serif` — there is no serif in this system
- Never use `--neon-green` as an H2 card title colour — that role belongs to `--neon-cyan`
- Never remove the `borderScan` animation from cards — a static card breaks the living-terminal feel
- Never use `border-radius > 10px` — overly rounded corners kill the hard-edged terminal character
- Never use gradient text (CSS `background-clip: text`) on body copy — only on the circular step number badge
- Never use purple as a general accent — `--neon-pink` is reserved strictly for advanced/optional elements
- Never omit the `0.2s` delay on `.tab-nav`'s `fadeIn` animation — the staggered entrance after the header is intentional pacing
- Never use `box-shadow` with blur alone (no spread, no colour) — glow requires colour-matched rgba shadows
- Never hardcode hex values in component styles — always reference `var(--token)`

---

## 13. HTML Document Shell

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
  <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;500;700&family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet">
  <style>
    /* 1. CSS variables (:root only — no dark mode toggle) */
    /* 2. Reset (*, margin/padding/box-sizing) */
    /* 3. body: font, bg, color, line-height, overflow-x */
    /* 4. body::before: animated grid */
    /* 5. Keyframes: gridScroll, glitch, glow, slideDown, fadeIn,
                     fadeInContent, borderScan, pulse */
    /* 6. header: sticky, gradient bg, green bottom border, slideDown */
    /* 7. h1: Orbitron, neon-cyan, text-shadow glow, glow animation */
    /* 8. .container */
    /* 9. .tab-nav + .tab-button + .tab-content */
    /* 10. .card + .card::before (borderScan) */
    /* 11. .terminal + span classes */
    /* 12. .step + .step-number + .step-content */
    /* 13. .alert variants */
    /* 14. .badge variants */
    /* 15. table */
    /* 16. .illustration */
    /* 17. code + .key */
    /* 18. ul/ol/li */
    /* 19. footer */
    /* 20. ::-webkit-scrollbar */
    /* 21. @media (max-width: 768px) */
  </style>
</head>
<body>
  <header>
    <h1>Page Title</h1>
    <p class="subtitle">Subtitle text for <span>highlighted term</span></p>
  </header>

  <div class="container">
    <!-- Optional top-level alert -->
    <div class="alert alert-warning">
      <strong>⚠️ NOTICE LABEL:</strong> Alert body text here.
    </div>

    <!-- Tab navigation -->
    <nav class="tab-nav">
      <button class="tab-button active" data-tab="tab1">Tab One</button>
      <button class="tab-button" data-tab="tab2">Tab Two</button>
    </nav>

    <!-- Tab panels -->
    <div class="tab-content active" id="tab1">
      <div class="card">
        <h2>Section Title</h2>
        <h3>Subsection</h3>
        <p>Body text in <strong>highlighted keyword</strong> and <code>inline code</code> form.</p>
        <div class="terminal">
          <pre><span class="prompt">user@host ~$</span> command
<span class="output">Expected output here</span></pre>
        </div>
      </div>
    </div>

    <div class="tab-content" id="tab2">
      <!-- content -->
    </div>
  </div>

  <footer>
    <p>Footer tagline. <a href="#">Link text</a></p>
  </footer>

  <script>
    const tabButtons  = document.querySelectorAll('.tab-button');
    const tabContents = document.querySelectorAll('.tab-content');
    tabButtons.forEach(btn => {
      btn.addEventListener('click', () => {
        const t = btn.getAttribute('data-tab');
        tabButtons.forEach(b => b.classList.remove('active'));
        tabContents.forEach(c => c.classList.remove('active'));
        btn.classList.add('active');
        document.getElementById(t).classList.add('active');
      });
    });
  </script>
</body>
</html>
```

---

## 14. React/JSX Adaptation Notes

When implementing this system in React:

1. **CSS variables** — declare in `src/styles/cyberpunk-tokens.css`, import globally at root; no `data-theme` attribute switching needed since there is only one theme.
2. **`body::before` grid** — render as a fixed `<div className="cyber-grid" />` in the root layout component; style with `position: fixed; inset: 0; z-index: -1; pointer-events: none`.
3. **`borderScan` on cards** — implement via `::before` in CSS Modules or a Tailwind arbitrary `before:` class; ensure `overflow-hidden` is on the card wrapper.
4. **Tab system** — `useState<string>` for `activeTab`; conditionally apply `className="tab-button active"` and mount panel content. To re-trigger `fadeInContent`, use a `key={activeTab}` prop on the panel wrapper to force remount.
5. **Animations** — define all `@keyframes` in a global CSS file, not CSS Modules, so they are available across components without duplication.
6. **`text-shadow` glow** — pass via inline `style` prop for dynamic colours: `style={{ textShadow: '0 0 10px #00d9ff, 0 0 20px #00d9ff' }}`, or define static Tailwind arbitrary utilities in `tailwind.config.js`.
7. **Step number** — implement as a styled `<div>` with `className="step-number"`; the `pulse` animation is defined globally and applies automatically.
8. **Scrollbar** — must be in a global CSS file (`src/index.css` or `src/globals.css`); CSS Modules scope prevents `::-webkit-scrollbar` from applying correctly.

---

---

## ADDENDUM — Additional Tips from System Frontend Design Skill

> The following section contains supplemental design guidance from the base `frontend-design` skill. It is additional and secondary; the primary source of truth for this design system is Sections 1–14 above.

```
ADDENDUM: General Frontend Design Principles (from system skill)

## Design Thinking Before Coding
Before writing any markup, commit to a BOLD aesthetic direction:
- Purpose: What problem does this interface solve? Who uses it?
- Tone: This system has committed to: cyberpunk/terminal/hacker. Execute with
  total precision. Every deviation — a rounded card, a serif font, a pastel
  colour, a light background — breaks the immersion immediately.
- Differentiation: The LIVE quality (pulsing glows, scanning stripes, scrolling
  grid) is what makes this system unforgettable. Static implementations of this
  palette look flat. Animation is structural, not decorative.

## Color
- Neon colours only work at full saturation against near-black backgrounds.
  On any background lighter than #1a1a2e these colours become garish and
  unreadable. Do not try to adapt this palette to a light theme.
- The green→cyan→pink triadic relationship is load-bearing. Green = system/ok,
  Cyan = title/interactive, Pink = advanced/optional/danger-adjacent. Swapping
  roles destroys semantic clarity.

## Motion
- In this system, animation IS identity. The grid scroll, borderScan, and glow
  pulse together create the "live terminal" feeling. Strip any one of them and
  the aesthetic degrades toward generic dark mode.
- All animations should loop infinitely where possible. This is not a "subtle
  micro-interaction" system — it is a fully animated environment.

## Typography discipline
- Orbitron at small sizes (below 1.4rem) becomes unreadable due to its geometric
  construction. Never use Orbitron for body copy, labels, or captions.
- Fira Code is the workhorse — it is readable at 0.75rem and carries the
  "terminal authenticity" even for non-code text.

## Backgrounds and depth
- Three dark levels (--darker-bg, --dark-bg, --terminal-bg) create the
  z-axis of the UI. Page bg → card bg → terminal bg: each step is one shade
  lighter (but all still very dark). This stacking reads as physical depth.
- The grid background must remain at near-zero opacity. Increasing it to even
  0.08 makes the grid dominant and the content unreadable.

## Anti-patterns to NEVER use in this system
- Light or white backgrounds anywhere
- Sans-serif non-monospace fonts (Inter, Roboto, DM Sans)
- Soft pastel accents (mint green, baby blue, lavender)
- Glassmorphism / frosted blur — incompatible with terminal aesthetic
- Flat single-colour borders without glow (always pair with box-shadow rgba)
- Centred body text paragraphs
- Border-radius above 10px on any structural container
```
