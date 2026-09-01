---
name: nvme-egpu-design
description: >
  Frontend design system extracted from the M.2 NVMe eGPU guide page. It uses a dark‑mode aesthetic with a deep navy background, purple accent colors, Inter and JetBrains Mono fonts, card‑based layout, radial‑gradient hero atmosphere, and a responsive 2‑/3‑column grid.
---

# NVMe‑eGPU Design System — Design Skill

## Concept & Aesthetic Direction
The page presents a **technical guide** styled as a modern, dark‑theme documentation site. It fuses **minimalist technical documentation** aesthetics with **high‑contrast accent accents** (purple‑orange‑teal) and **card‑based UI** reminiscent of design‑system dashboards. It is **not** a colorful marketing site; it stays within a limited palette and low‑radius UI, suitable for technical content where readability and data tables dominate.

---

## Typography
```css
/* Font imports */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500&display=swap');
```
| Role | Font‑family | Weight | Size | Line‑height | Letter‑spacing | Text‑transform |
|------|-------------|--------|------|-------------|----------------|----------------|
| Body / UI | var(--font‑sans) = "Inter", system-ui, -apple-system, sans-serif | 400 (default) | 1rem (base) – varies per component | 1.6 (body) | normal | none |
| Monospace code | var(--font‑mono) = "JetBrains Mono", monospace | 400 / 500 | 13px (code‑block, .step‑num) | 1.8 (code‑block) | normal | none |
| Hero title | var(--font‑sans) (Inter) | 800 | `clamp(2.2rem,5vw,3.8rem)` | 1.1 | normal | none |
| Hero badge | var(--font‑sans) | 600 | 12px | normal | 1px (uppercase) | uppercase |
| Tab buttons | var(--font‑sans) | 500 | 13px | normal | normal | none |
| Section headers (h2) | var(--font‑sans) | 700 | 1.5rem | normal | normal | none |
| Card titles (h3) | var(--font‑sans) | 600 | 1.05rem | normal | normal | none |
| Tags & badges | var(--font‑sans) | 500 | 11px | normal | normal | uppercase |
| Prices | var(--font‑sans) | 700 | 1.4rem | normal | normal | none |
| Step numbers | var(--font‑mono) | 700 | 13px | normal | normal | none |
```

---

## Color System
```css
:root {
  --bg: #0a0a0f;               /* page background */
  --surface: #111118;          /* card background */
  --surface-2: #181820;        /* secondary surface (tables, code blocks) */
  --surface-3: #1e1e28;        /* hover surface / borders */
  --border: rgba(255,255,255,0.06);
  --border-hover: rgba(255,255,255,0.12);
  --text: #e8e8ec;             /* primary text */
  --text-secondary: #9a9aa8;   /* secondary text */
  --text-muted: #6b6b7a;       /* muted / notes */
  --accent: #7c5cff;           /* main purple accent */
  --accent-soft: rgba(124,92,255,0.12);
  --accent-2: #ff6b9d;        /* pink accent */
  --accent-3: #00d4aa;         /* teal accent */
  --accent-4: #ffb347;        /* orange accent */
  --accent-5: #5cadff;        /* light‑blue accent */
  --danger: #ff4757;          /* error / danger */
  --success: #00d4aa;         /* success (same as accent‑3) */
  --warning: #ffb347;        /* warning (same as accent‑4) */
  --info: #5cadff;            /* info (same as accent‑5) */
  --radius: 14px;             /* default border‑radius */
  --radius-sm: 8px;
  --radius-xs: 6px;
  --shadow: 0 8px 32px rgba(0,0,0,0.4);
  --font-sans: 'Inter', system-ui, -apple-system, sans-serif;
  --font-mono: 'JetBrains Mono', monospace;
  --transition: 0.2s cubic-bezier(0.4,0,0.2,1);
}
```
### Semantic groups
- **Backgrounds** – `--bg`, `--surface`, `--surface-2`, `--surface-3`
- **Text** – `--text`, `--text-secondary`, `--text-muted`
- **Accents** – `--accent` (primary), `--accent-2` … `--accent-5`
- **State colors** – `--danger`, `--success`, `--warning`, `--info`
- **Borders** – `--border`, `--border-hover`
- **Radii & shadows** – `--radius*`, `--shadow`

---

## Background & Atmosphere
```css
body {
  background: var(--bg);
  color: var(--text);
  font-family: var(--font-sans);
}

.hero::before {
  content: '';
  position: absolute;
  top: -200px;
  left: 50%;
  transform: translateX(-50%);
  width: 800px;
  height: 800px;
  background: radial-gradient(circle, rgba(124,92,255,0.08) 0%, transparent 70%);
  pointer-events: none;
  z-index: 0;
}

.hero-badge {
  background: var(--accent-soft);
  border: 1px solid rgba(124,92,255,0.2);
  color: var(--accent);
}
```
**Z‑index layering**
- `body` → base
- `.hero` (relative) → layer 0
- `.hero::before` → `z-index:0`
- `.hero-badge` & content → `z-index:1`
- `.tabs` sticky → `z-index:100`
- `.card` hover → `box-shadow` with `var(--shadow)`

---

## Layout Architecture
```css
.app {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 24px;
}

.hero {
  padding: 80px 0 48px;
  text-align: center;
  overflow: hidden;
}

.tabs {
  position: sticky;
  top: 0;
  z-index: 100;
  background: linear-gradient(180deg, var(--bg) 60%, rgba(10,10,15,0.95));
  padding: 16px 0 8px;
  border-bottom: 1px solid var(--border);
}

.grid-2 {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px,1fr));
  gap: 20px;
}

.grid-3 {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px,1fr));
  gap: 20px;
}
```
- **Responsive breakpoint**: `@media (max-width:768px)` (see later).
- **Structural regions**: `.hero`, `.tabs`, `.section`, `.card`, `.table-wrap`, `.performance-chart`, `.footer`.

---

## Component Inventory
### Hero
- `.hero` container with large top padding.
- `.hero::before` radial‑gradient atmosphere.
- `.hero-badge` inline‑flex badge.
- `h1` with clamp‑sized font, gradient text via `background-clip: text`.
- `p` subtitle.
- `.hero-meta` flex list of icons.
### Tabs
- `.tabs` sticky bar, `.tabs-inner` flex scrollable list.
- `.tab-btn` button, `active` state adds background `var(--surface-2)`, accent colour, and underline via `::after`.
- JS `switchTab(index)` toggles `.active` classes.
### Card
- Base `.card` with surface background, border, radius, transition.
- Hover adds `box-shadow` and accent left border via variant classes `.card-accent`, `.card-accent-2` … `.card-accent-5` (different accent colours).
- Elements inside: `h3` with dot, `p`, `ul/li`, `.tag`, `.price`.
### Badge
- `.badge` utility, colour variants `.badge-success`, `.badge-warning`, etc. Uses `background: rgba(...,0.12)`.
- Text colour matches the state variable (`--success`, `--danger`, …).
### Code Block
- `.code-block` with monospaced font, background `var(--surface-2)`, border, radius `var(--radius-sm)`.
### Step / Timeline
- `.step` container, `.step-num` circular badge with accent‑soft background and accent border.
### Connector Diagram
- `.connector-diagram` flex, `.connector-box` with label & name, `.arrow` coloured with `var(--accent)`.
### Tables
- `.table-wrap` gives rounded border and overflow.
- `table` full‑width, `thead` surface‑2 background, `th` accent text, `td` border lines.
### Performance Chart
- Grid of `.perf-card` with surface background, centered stats.
### Footer
- Simple centered text with top border.

---

## Micro‑details & Signature Patterns
- **Border radius**: default `14px`, smaller `8px`/`6px` for components.
- **Left‑border accent** on cards (`border-left:3px solid var(--accent‑X)`).
- **Dot indicator** in card titles (`.dot` with background colour matching accent). 
- **Selection highlight** via `::selection` using `var(--accent‑soft)`.
- **Icon colour** – SVGs inherit `color: var(--accent)` for hero meta icons.
- **Rounded badge** shapes (`border-radius:100px`).
- **Hover underline** on active tab (`.tab-btn.active::after`).
- **Hover border colour change** (`--border-hover`).
- **Radial‑gradient hero overlay** with low opacity.

---

## Animation & Motion
```css
@keyframes fadeIn {
  from { opacity:0; transform:translateY(12px); }
  to   { opacity:1; transform:translateY(0); }
}

.tab-panel { display:none; animation:fadeIn .35s ease; }
.tab-panel.active { display:block; }

.card, .tab-btn { transition: var(--transition); }
```
- Fade‑in for tab panels.
- All interactive elements use the same cubic‑bezier transition.

---

## Responsive Breakpoints
```css
@media (max-width: 768px) {
  .hero { padding:48px 0 32px; }
  .tabs { padding:12px 0 4px; }
  .grid-2, .grid-3 { grid-template-columns:1fr; }
  .connector-diagram { flex-direction:column; }
  .compatibility-matrix .row { flex-direction:column; align-items:flex-start; gap:6px; }
  .compatibility-matrix .row .status { margin-left:0; }
}
```
Only one breakpoint (tablet/mobile). Adjusts paddings, collapses grids to single column, stacks compatibility rows.

---

## Print Styles
No explicit `@media print` rules – the page will print using the default styles.

---

## JavaScript Behavior
```js
function switchTab(index) {
  document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('tab-' + index).classList.add('active');
  document.querySelectorAll('.tab-btn')[index].classList.add('active');
}
// initial activation
document.querySelectorAll('.tab-btn')[0].classList.add('active');
document.getElementById('tab-0').classList.add('active');
```
- Handles tab navigation, toggles `active` classes on panels and buttons.
- No additional dynamic behaviour.

---

## Design Rules — Do & Don't
**Do**
- Use the defined `--` variables for any colour, radius, or transition.
- Keep the dark background (`--bg`) and surface hierarchy.
- Apply the left‑border accent pattern for card‑type components.
- Respect the mobile breakpoint at 768 px – collapse grids to a single column.
- Use the hero radial‑gradient overlay for atmospheric depth.
- Keep all typography within the Inter/JetBrains Mono families.

**Don't**
- Change the accent palette (purple‑pink‑teal‑orange‑light‑blue) – it defines the brand.
- Increase border‑radius beyond `var(--radius)` – the design is deliberately sharp.
- Remove the `::selection` highlight – it provides visual feedback.
- Add extra media queries; the single breakpoint must stay consistent.

---

## Composing a New Application in This System
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1.0">
  <title>My NVMe‑eGPU App</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
  <style>
    /* Insert the full :root block and all component CSS from the original file here */
  </style>
</head>
<body>
  <div class="app">
    <!-- Hero -->
    <header class="hero">
      <div class="hero-badge">Your Badge</div>
      <h1>Title</h1>
      <p>Subtitle text.</p>
      <div class="hero-meta"><span>Meta 1</span><span>Meta 2</span></div>
    </header>

    <!-- Tabs -->
    <nav class="tabs">
      <div class="tabs-inner">
        <button class="tab-btn" onclick="switchTab(0)">Tab 0</button>
        <button class="tab-btn" onclick="switchTab(1)">Tab 1</button>
        <!-- more buttons as needed -->
      </div>
    </nav>

    <div class="tab-content">
      <div class="tab-panel" id="tab-0">Content for Tab 0</div>
      <div class="tab-panel" id="tab-1">Content for Tab 1</div>
      <!-- additional panels -->
    </div>
  </div>
  <script>
    // copy the switchTab function from the original page
  </script>
</body>
</html>
```
Replace the comment `/* Insert … */` with the exact CSS from the original `index.html` (the whole `<style>` block). All component markup follows the same class naming conventions, so you can copy any of the existing card, table, step, or performance‑card structures and simply replace the text/content.

---

## Checklist
- [x] All `:root` custom properties captured.
- [x] Font imports and families listed.
- [x] Hero, tabs, cards, badges, code blocks, steps, connector diagram, tables, performance chart extracted.
- [x] Micro‑details (radius, left‑border accents, dot colours) documented.
- [x] Animation (`fadeIn`) and transition values recorded.
- [x] Responsive breakpoint (`max-width:768px`) saved.
- [x] JavaScript tab‑switch behaviour included.
- [x] No references to the original file remain.

---

*Generated by the Frontend‑Design‑Extractor skill.*
