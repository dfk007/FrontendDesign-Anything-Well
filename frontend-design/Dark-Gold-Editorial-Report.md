---
name: frontend-design
description: >
  Dark-masthead editorial report system fusing financial journalism aesthetics with technical
  documentation precision. Primary accent is warm gold (#c8922a) on an ink-dark navy masthead
  (#0d1117), over a warm off-white parchment body (#f7f6f2). Font stack: DM Serif Display
  (display headings, numbers), DM Mono (all metadata, labels, badges, nav, footer, code),
  Space Grotesk (all body prose and UI text). Signature patterns: gold eyebrow labels in
  DM Mono ALL-CAPS above serif headings; horizontal ruled section dividers with numbered
  index; full-bleed dark-ink "inversion" panels breaking the light body; horizontal ruled
  scanlines on the masthead via repeating-gradient; a gold "verdict strip" banner anchored
  to the bottom of the masthead; sticky monospace navigation tabs with gold underline hover;
  3px top-border color-coded role cards; a vertical timeline with gold/teal phase dots;
  inline progress bars with DM Mono range labels; and a two-tone colophon footer.
  Use this system for editorial reports, career guides, technical roadmaps, research
  documents, dashboards, and any long-form single-page application that needs to project
  authority and analytical depth.
---

# Dark-Gold Editorial Report — Design System Skill

## Concept & Aesthetic Direction

This system fuses three design traditions:
1. **Financial/editorial print** — The Economist, Bloomberg Businessweek section headers, ruled dividers, numbered sections, gold accent hierarchy
2. **Technical documentation** — monospace metadata everywhere, inline code styling, data tables with dark headers, tier badges
3. **Dark-mode masthead journalism** — full-bleed dark ink header with scanline texture, gold verdict banner, parchment-warm body contrast

**What it is NOT:**
- Not a dashboard with heavy chrome or sidebar nav
- Not a dark-mode-everywhere design (only the masthead and one "inversion" section are dark)
- Not a gradient/glow aesthetic — all fills are flat
- Not Inter or Roboto — every non-prose element uses DM Mono; the serif is DM Serif Display only for display-scale text

**When to use:** Reports, career guides, technical roadmaps, research briefings, competitive analyses, interview prep guides, single-page annual reports, and any document where content authority is paramount.

---

## Typography

### Font Import

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Mono:wght@400;500&family=Space+Grotesk:wght@300;400;500;600&display=swap" rel="stylesheet">
```

### Font 1 — DM Serif Display

**Role:** Display headlines, section titles, large stat numbers  
**Used when:** H1, H2 section titles, `.signal-num` large metric numbers — any moment of editorial authority

| Context | font-size | font-weight | line-height | font-style | color |
|---|---|---|---|---|---|
| Masthead H1 | `clamp(2.4rem, 5vw, 3.8rem)` | 400 | 1.1 | normal | `#f0ebe3` |
| Masthead H1 `em` | (inherited) | 400 | 1.1 | **italic** | `var(--accent-gold)` |
| Section titles `.section-title` | `1.7rem` | 400 | (default) | normal | `var(--ink)` |
| Section titles in dark panel | `1.7rem` | 400 | (default) | normal | `#f0ebe3` |
| Stat numbers `.signal-num` | `2.2rem` | 400 | 1 | normal | `var(--accent-teal)` / `.red` / `.gold` / `.blue` variants |

**No variable font axes** — DM Serif Display is not a variable font. Uses standard weight 400 italic/non-italic only.

### Font 2 — DM Mono

**Role:** All metadata, all labels, all badges, all navigation, all footer text, all inline code, all eyebrow labels, all table headers, all numbered section prefixes, all salary range values, all phase labels on timeline, all status indicators

**Used when:** Every piece of UI chrome, meta-information, system text — any text that is NOT prose body and NOT a display headline

| Context | font-size | font-weight | letter-spacing | text-transform | color |
|---|---|---|---|---|---|
| Eyebrow `.eyebrow` | 11px | 400 | 0.18em | uppercase | `var(--accent-gold)` |
| Meta labels `.meta-label` | 10px | 400 | 0.12em | uppercase | `#665f50` |
| Meta values `.meta-value` | 13px | 500 | — | — | `#c8bfb0` |
| Verdict strip label | 11px | 500 | 0.1em | uppercase | `#2a1a00` |
| Section number `.section-number` | 11px | 400 | 0.1em | — | `var(--accent-gold)` |
| Table `th` | 11px | 500 | 0.08em | uppercase | `#f0ebe3` |
| Priority badges `.priority-badge` | 11px | 600 | 0.04em | — | varies by badge |
| `.already-badge` | 10px | 600 | 0.04em | — | `var(--accent-teal)` |
| Role fit tag `.role-fit-tag` | 10px | 400 | 0.1em | uppercase | `var(--ink-muted)` |
| Best-fit banner `.best-fit-banner` | 10px | 700 | 0.1em | uppercase | `#2a1a00` |
| Role salary `.role-salary` | 12px | 500 | — | — | `var(--accent-teal)` |
| `.tag` (tech chips) | 11px | 400 | — | — | `var(--ink-dim)` |
| Phase label `.phase-label` | 10px | 400 | 0.1em | uppercase | `var(--accent-gold)` |
| Nav tabs `.nav-tab` | 11px | 400 | 0.07em | uppercase | `var(--ink-muted)` |
| Callout label `.callout-label` | 10px | 600 | 0.1em | uppercase | `#7a4f0a` |
| Signal item number `.si-num` | 11px | 400 | — | — | `var(--ink-muted)` |
| Footer `.doc-footer p` | 11px | 400 | 0.05em | — | `var(--ink-muted)` |
| Salary role note | 11px | 400 | — | — | `#665f50` |
| Salary range labels `.salary-nums span` | 11px | 400 | — | — | `#a09880` |
| Salary range hi value `.hi` | 11px | 600 | — | — | `var(--accent-gold)` |
| `.salary-tag` (table cell) | 12px | 500 | — | — | `var(--accent-teal)` |
| `.skill-sub` | 12px | 400 | — | — | `var(--ink-muted)` |
| Inline `code` | 12px | 400 | — | — | `var(--accent-blue)` |
| `.proof-exists` | 11px | 600 | — | — | `var(--accent-teal)` |
| `.proof-todo` | 11px | 600 | — | — | `var(--accent-gold)` |

### Font 3 — Space Grotesk

**Role:** All body prose, UI card text, descriptive paragraphs, checklist items, split-card list items

**Used when:** Any sentence-length text that a human reads for content, not for UI orientation

| Context | font-size | font-weight | line-height | color |
|---|---|---|---|---|
| `body` default | 15px | 400 | 1.65 | `var(--ink)` |
| Masthead subtitle `.masthead-sub` | 15px | 400 | 1.7 | `#a09880` |
| Verdict strip `strong` | 13px | (bold) | — | `#2a1a00` |
| Split card list items | 13.5px | 400 | — | `var(--ink-dim)` |
| Table `td` body | 13.5px | 400 | — | `var(--ink-dim)` |
| `.skill-name` | (table size) | 600 | — | `var(--ink)` |
| Role card `h3` | 15px | 600 | 1.3 | `var(--ink)` |
| Role card `p` | 13px | 400 | 1.55 | `var(--ink-dim)` |
| Phase title `.phase-title` | 15px | 600 | — | `var(--ink)` |
| Phase body `.phase-body` | 13.5px | 400 | 1.65 | `var(--ink-dim)` |
| Checklist items | 13px | 400 | — | `var(--ink-dim)` |
| Proof card `h4` | 13px | 600 | — | `var(--ink)` |
| Proof card `p` | 12px | 400 | 1.5 | `var(--ink-muted)` |
| Signal item text | 13.5px | 400 | — | `var(--ink-dim)` |
| Callout `p` | 13.5px | 400 | 1.6 | `#4a2c00` |
| Salary role name | 13px | 600 | — | `#e8e0d4` |

---

## Color System

### Full CSS Custom Properties

```css
:root {
  /* ── Ink hierarchy ── */
  --ink: #0d1117;          /* Primary text, darkest */
  --ink-2: #1e2530;        /* Dark panel backgrounds (salary section, table thead) */
  --ink-dim: #4a5568;      /* Secondary text, card body */
  --ink-muted: #718096;    /* Tertiary text, placeholders, muted metadata */

  /* ── Backgrounds ── */
  --bg: #f7f6f2;           /* Warm off-white parchment — page body */
  --bg-card: #ffffff;      /* Pure white — card surfaces */
  --bg-dark: #0d1117;      /* Masthead background */

  /* ── Accent palette ── */
  --accent-gold: #c8922a;        /* Primary brand accent — gold */
  --accent-gold-light: #f5e6c8;  /* Gold tint — callout backgrounds, badge fills */
  --accent-teal: #0d7a5f;        /* Secondary accent — positive, "exists", salaries */
  --accent-teal-light: #d1f0e8;  /* Teal tint — "already have" badge background */
  --accent-red: #c0392b;         /* Warning/threat accent */
  --accent-red-light: #fdecea;   /* Red tint — critical badge background */
  --accent-blue: #1a5fa8;        /* Informational accent — medium priority, inline code */
  --accent-blue-light: #dbeafe;  /* Blue tint — medium badge background */
  --accent-purple: #6b46c1;      /* Agent/AI category accent — role card top bar */
  --accent-purple-light: #ede9fe;/* Purple tint — available for purple badges */

  /* ── Borders ── */
  --border: #e2ddd6;       /* Default border — warm greige */
  --border-strong: #c8c0b4;/* Stronger border — timeline line, checkbox outlines */

  /* ── Shorthand ── */
  --rule: 1px solid var(--border);
}
```

### Semantic Color Mapping

**Backgrounds (light to dark):**
- `--bg` (`#f7f6f2`) — page body, warm parchment
- `--bg-card` (`#ffffff`) — card surfaces, table rows
- `#faf9f7` — alternate table row tint (even rows)
- `--ink-2` (`#1e2530`) — dark panel inversion sections
- `--bg-dark` / `--ink` (`#0d1117`) — masthead

**Text hierarchy:**
- `--ink` — primary headings and emphasized text
- `--ink-dim` — secondary body text, descriptions
- `--ink-muted` — tertiary, placeholders, less-important labels
- `#f0ebe3` — text on dark (masthead headings, table headers)
- `#a09880` — muted text on dark (masthead subtitle)
- `#665f50` — very muted on dark (meta labels, salary role notes)
- `#c8bfb0` — medium on dark (meta values)
- `#e8e0d4` — slightly warm white on dark (salary role names)

**Accent usage rules:**
- Gold (`--accent-gold`) → progress, achievement, featured, "active" states, section numbers, eyebrow labels, phase labels, verdict strip, best-fit banners
- Teal (`--accent-teal`) → positive/existing, salary figures, teal role cards, "opp" split cards, `.proof-exists`, `.salary-tag`
- Red (`--accent-red`) → threats, critical priority, `.threat` split cards, `.p-critical` badges
- Blue (`--accent-blue`) → medium priority, informational, inline code color
- Purple (`--accent-purple`) → agent/AI category top bar accent only

**Badge fill + text pairings (exact):**
- `.p-critical`: bg `--accent-red-light` (#fdecea), text `--accent-red` (#c0392b)
- `.p-high`: bg `--accent-gold-light` (#f5e6c8), text `#7a4f0a`
- `.p-medium`: bg `--accent-blue-light` (#dbeafe), text `--accent-blue` (#1a5fa8)
- `.p-nice`: bg `#f0f0f0`, text `#555`
- `.already-badge`: bg `--accent-teal-light` (#d1f0e8), text `--accent-teal` (#0d7a5f)
- `.best-fit-banner`: bg `--accent-gold` (#c8922a), text `#2a1a00`

---

## Background & Atmosphere

### Body

```css
body {
  background: var(--bg);  /* #f7f6f2 — warm parchment, no texture */
  color: var(--ink);
}
```

The body has no pseudo-element decoration. Texture and atmosphere are confined to the masthead.

### Masthead Scanline Texture

The masthead has a subtle repeating horizontal rule texture via `::before`:

```css
.masthead {
  background: var(--bg-dark);  /* #0d1117 */
  position: relative;
  overflow: hidden;
}
.masthead::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0; bottom: 0;
  background: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 39px,
    rgba(255, 255, 255, 0.03) 39px,
    rgba(255, 255, 255, 0.03) 40px
  );
  pointer-events: none;
  /* No z-index — sits above bg-dark, below content (position: relative on inner) */
}
```

**Effect:** Ultra-subtle horizontal scanlines at 40px intervals. Each line is 1px wide at 3% white opacity. Visible only on close inspection — creates depth without gradient.

### Sticky Nav Background

```css
.sticky-nav {
  background: rgba(247, 246, 242, 0.95);  /* body bg at 95% opacity */
  backdrop-filter: blur(4px);
}
```

Semi-transparent frosted glass on scroll, using body color so it blends when at top.

### Dark Inversion Panel (`.salary-section`)

Full-bleed dark panel breaking the light body:

```css
.salary-section {
  background: var(--ink-2);  /* #1e2530 */
  margin: 0 -2rem;           /* bleeds beyond .page container horizontally */
  padding: 2.5rem 2rem;
  color: #f0ebe3;
}
```

Used once per page to add rhythm and contrast. The negative horizontal margin trick bleeds it full-width while the page content is constrained.

---

## Layout Architecture

### Page Container

```css
.page {
  max-width: 900px;
  margin: 0 auto;
  padding: 0 2rem 4rem;
}
```

### Masthead Container

```css
.masthead-inner {
  max-width: 900px;
  margin: 0 auto;
  padding: 0 2rem;
  position: relative;  /* above ::before scanline layer */
}
```

### Sticky Navigation

```css
.sticky-nav {
  position: sticky;
  top: 0;
  z-index: 100;
  background: rgba(247, 246, 242, 0.95);
  backdrop-filter: blur(4px);
  border-bottom: var(--rule);
  padding: 0 2rem;
}
.nav-inner {
  max-width: 900px;
  margin: 0 auto;
  display: flex;
  gap: 0;
  overflow-x: auto;
  scrollbar-width: none;
}
.nav-inner::-webkit-scrollbar { display: none; }
```

### Section Header Pattern

Every section uses this two-element flex header with a ruled bottom:

```css
.section-header {
  display: flex;
  align-items: baseline;
  gap: 1rem;
  padding: 3rem 0 1.2rem;
  border-bottom: var(--rule);
  margin-bottom: 1.5rem;
}
```

**Left element:** `.section-number` — DM Mono 11px gold, e.g. "01"  
**Right element:** `.section-title` — DM Serif Display 1.7rem, `var(--ink)`

In dark panels (`.salary-section`), override:
```css
.salary-section .section-title { color: #f0ebe3; }
.salary-section .section-number { color: var(--accent-gold); }
.salary-section .section-header { border-bottom-color: rgba(255,255,255,0.1); }
```

### Masthead Layout

```
┌─────────────────────────────────────────────────────┐
│ .masthead (full-width, bg: #0d1117, pt: 3.5rem)     │
│   ├── .eyebrow (DM Mono 11px gold, mb: 1.2rem)      │
│   ├── h1 (DM Serif Display clamp, max-w: 700px)     │
│   ├── .masthead-sub (Space Grotesk 15px, max-w: 560px) │
│   ├── .masthead-meta (flex, gap: 2rem, pt: 1.5rem,  │
│   │     border-top: 1px rgba(255,255,255,0.08))      │
│   │     └── .meta-item × N (column flex, gap: 2px)  │
│   │           ├── .meta-label (DM Mono 10px)         │
│   │           └── .meta-value (13px)                 │
│   └── .verdict-strip (gold bg, -2rem margin, 0.9rem pad) │
└─────────────────────────────────────────────────────┘
```

---

## Component: Navigation Tabs

```css
.nav-tab {
  font-family: 'DM Mono', monospace;
  font-size: 11px;
  letter-spacing: 0.07em;
  text-transform: uppercase;
  color: var(--ink-muted);
  text-decoration: none;
  padding: 0.8rem 1.1rem;
  border-bottom: 2px solid transparent;
  white-space: nowrap;
  transition: color 0.15s, border-color 0.15s;
}
.nav-tab:hover {
  color: var(--ink);
  border-bottom-color: var(--accent-gold);
}
```

**HTML:**
```html
<nav class="sticky-nav">
  <div class="nav-inner">
    <a class="nav-tab" href="#section-id">Label</a>
  </div>
</nav>
```

**Behavior:** No active state in CSS — uses scroll anchor links. Hover reveals gold 2px underline and darkens text.

---

## Component: Masthead Verdict Strip

Full-width gold banner anchored to the bottom of the masthead. The `margin: 0 -2rem` technique bleeds it beyond the `.masthead-inner` container to match the masthead edge.

```css
.verdict-strip {
  background: var(--accent-gold);
  margin: 0 -2rem;
  padding: 0.9rem 2rem;
  display: flex;
  align-items: center;
  gap: 1rem;
  flex-wrap: wrap;
}
.verdict-strip span {
  font-family: 'DM Mono', monospace;
  font-size: 11px;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #2a1a00;
  font-weight: 500;
}
.verdict-strip strong {
  color: #2a1a00;
  font-size: 13px;
}
```

**HTML:**
```html
<div class="verdict-strip">
  <span>Label:</span>
  <strong>The verdict text in Space Grotesk 13px bold.</strong>
</div>
```

---

## Component: Signal / Metric Grid

Mosaic of stat cells separated by 1px `--border` gaps. Border-radius applied to outer container only; cells have no individual radius.

```css
.signal-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
  gap: 1px;
  background: var(--border);   /* gap color trick — grid bg shows as borders */
  border: var(--rule);
  border-radius: 8px;
  overflow: hidden;
  margin-bottom: 2rem;
}
.signal-cell {
  background: var(--bg-card);
  padding: 1.2rem 1.4rem;
}
.signal-num {
  font-family: 'DM Serif Display', serif;
  font-size: 2.2rem;
  color: var(--accent-teal);
  line-height: 1;
  margin-bottom: 4px;
}
.signal-num.red  { color: var(--accent-red); }
.signal-num.gold { color: var(--accent-gold); }
.signal-num.blue { color: var(--accent-blue); }
.signal-label {
  font-size: 12px;
  color: var(--ink-muted);
  line-height: 1.4;
}
```

**HTML:**
```html
<div class="signal-grid">
  <div class="signal-cell">
    <div class="signal-num">+85%</div>
    <div class="signal-label">Description of metric in 12px muted prose</div>
  </div>
  <div class="signal-cell">
    <div class="signal-num red">−25%</div>
    <div class="signal-label">Negative metric label</div>
  </div>
</div>
```

**Key technique:** `gap: 1px; background: var(--border)` on the grid container creates hairline separator lines between cells without individual cell borders.

---

## Component: Split Comparison Cards

Two-column layout with semantic top-border accents and custom list markers.

```css
.split-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  margin-bottom: 2rem;
}
.split-card {
  border-radius: 8px;
  border: var(--rule);
  background: var(--bg-card);
  padding: 1.4rem;
}
.split-card.threat { border-top: 3px solid var(--accent-red); }
.split-card.opp    { border-top: 3px solid var(--accent-teal); }
.split-card h3 {
  font-size: 13px;
  font-weight: 600;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  margin-bottom: 0.9rem;
}
.split-card.threat h3 { color: var(--accent-red); }
.split-card.opp h3    { color: var(--accent-teal); }
.split-card ul { list-style: none; }
.split-card ul li {
  font-size: 13.5px;
  color: var(--ink-dim);
  padding: 5px 0;
  border-bottom: 1px solid var(--bg);
  display: flex;
  gap: 8px;
  align-items: flex-start;
}
.split-card ul li::before {
  content: '→';
  color: var(--ink-muted);
  flex-shrink: 0;
  font-size: 12px;
  margin-top: 2px;
}
.split-card.threat ul li::before { content: '✕'; color: var(--accent-red); }
.split-card.opp    ul li::before { content: '✓'; color: var(--accent-teal); }
```

**Responsive:**
```css
@media (max-width: 600px) {
  .split-grid { grid-template-columns: 1fr; }
}
```

**Icon symbols used:** `→` (default), `✕` (threat), `✓` (opportunity)

---

## Component: Data Table with Dark Header

```css
.tier-table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 2rem;
  font-size: 13.5px;
}
.tier-table th {
  text-align: left;
  padding: 10px 14px;
  background: var(--ink-2);      /* #1e2530 */
  color: #f0ebe3;
  font-size: 11px;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  font-weight: 500;
  font-family: 'DM Mono', monospace;
}
.tier-table th:first-child { border-radius: 6px 0 0 0; }
.tier-table th:last-child  { border-radius: 0 6px 0 0; }
.tier-table td {
  padding: 11px 14px;
  border-bottom: 1px solid var(--border);
  vertical-align: top;
  color: var(--ink-dim);
}
.tier-table tr:last-child td { border-bottom: none; }
.tier-table tr:nth-child(even) td { background: #faf9f7; }
.tier-table .skill-name {
  font-weight: 600;
  color: var(--ink);
  display: flex;
  flex-direction: column;
  gap: 2px;
}
.tier-table .skill-sub {
  font-size: 12px;
  font-weight: 400;
  color: var(--ink-muted);
  font-family: 'DM Mono', monospace;
}
```

**HTML structure for a skill-name cell:**
```html
<td>
  <div class="skill-name">
    Main Skill Name <span class="already-badge">HAVE</span>
    <div class="skill-sub">sub-tool · sub-tool · sub-tool</div>
  </div>
</td>
```

---

## Component: Priority / Status Badges

All badges share the same base class, with modifier classes for semantic variants:

```css
.priority-badge {
  display: inline-block;
  padding: 2px 9px;
  border-radius: 20px;         /* pill shape */
  font-size: 11px;
  font-weight: 600;
  font-family: 'DM Mono', monospace;
  letter-spacing: 0.04em;
}
.p-critical { background: #fdecea; color: #c0392b; }
.p-high     { background: #f5e6c8; color: #7a4f0a; }
.p-medium   { background: #dbeafe; color: #1a5fa8; }
.p-nice     { background: #f0f0f0; color: #555555; }

/* Inline status badge (appears inside table cells, after skill names) */
.already-badge {
  display: inline-block;
  background: #d1f0e8;
  color: #0d7a5f;
  font-size: 10px;
  font-weight: 600;
  padding: 1px 7px;
  border-radius: 20px;
  letter-spacing: 0.04em;
  font-family: 'DM Mono', monospace;
  vertical-align: middle;
  margin-left: 4px;
}
```

---

## Component: Tech Chip Tags

Small monospace tags used in role cards and anywhere to list technology keywords:

```css
.tag {
  background: var(--bg);           /* #f7f6f2 */
  border: 1px solid var(--border); /* #e2ddd6 */
  color: var(--ink-dim);
  font-size: 11px;
  padding: 2px 8px;
  border-radius: 4px;              /* small, NOT pill */
  font-family: 'DM Mono', monospace;
}
.role-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
  margin-top: 0.6rem;
}
```

**Note:** Tags use `border-radius: 4px` (small square-ish). Badges use `border-radius: 20px` (pill). Never swap these.

---

## Component: Role Cards

Cards with a 3px colored top-border accent per category, optional gold featured border, and optional best-fit banner:

```css
.role-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1rem;
  margin-bottom: 2rem;
}
.role-card {
  background: var(--bg-card);
  border: var(--rule);
  border-radius: 10px;
  padding: 1.4rem;
  position: relative;
  overflow: hidden;
}
.role-card.featured {
  border-color: var(--accent-gold);
  border-width: 2px;
}
/* Top color stripe via ::before */
.role-card::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 3px;
}
/* Category color mapping */
.role-card.r-platform::before { background: var(--accent-teal);   }
.role-card.r-llm::before      { background: var(--accent-gold);   }
.role-card.r-agent::before    { background: var(--accent-purple); }
.role-card.r-infra::before    { background: var(--accent-blue);   }
.role-card.r-forward::before  { background: var(--accent-red);    }

.role-fit-tag {
  font-family: 'DM Mono', monospace;
  font-size: 10px;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--ink-muted);
  margin-bottom: 0.5rem;
}
.role-card h3 {
  font-size: 15px;
  font-weight: 600;
  color: var(--ink);
  margin-bottom: 0.5rem;
  line-height: 1.3;
}
.role-card .role-salary {
  font-family: 'DM Mono', monospace;
  font-size: 12px;
  color: var(--accent-teal);
  margin-bottom: 0.8rem;
  font-weight: 500;
}
.role-card p {
  font-size: 13px;
  color: var(--ink-dim);
  line-height: 1.55;
  margin-bottom: 0.8rem;
}
.best-fit-banner {
  background: var(--accent-gold);
  color: #2a1a00;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  padding: 3px 10px;
  border-radius: 20px;
  display: inline-block;
  margin-bottom: 8px;
  font-family: 'DM Mono', monospace;
}
```

**HTML:**
```html
<div class="role-card r-platform featured">
  <div class="best-fit-banner">★ Best Fit — Immediate</div>
  <div class="role-fit-tag">Platform · Infrastructure</div>
  <h3>Role Title</h3>
  <div class="role-salary">Remote US/EU: $120K–$180K</div>
  <p>Description in Space Grotesk 13px.</p>
  <div class="role-tags">
    <span class="tag">tech1</span>
    <span class="tag">tech2</span>
  </div>
</div>
```

---

## Component: Callout Box

Left-border accent callout on gold background:

```css
.callout {
  border-left: 3px solid var(--accent-gold);
  background: var(--accent-gold-light);  /* #f5e6c8 */
  padding: 1rem 1.2rem;
  border-radius: 0 6px 6px 0;           /* flat left, rounded right */
  margin-bottom: 1.5rem;
}
.callout-label {
  font-family: 'DM Mono', monospace;
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: #7a4f0a;
  font-weight: 600;
  margin-bottom: 5px;
}
.callout p {
  font-size: 13.5px;
  color: #4a2c00;
  line-height: 1.6;
}
```

**Note:** `border-radius: 0 6px 6px 0` is deliberate — the flat left side aligns with the left border accent, which would look wrong with rounded corners.

---

## Component: Vertical Timeline

A vertical ruled timeline with absolute-positioned numbered dots:

```css
.timeline {
  position: relative;
  margin-bottom: 2rem;
}
.timeline::before {
  content: '';
  position: absolute;
  left: 28px;
  top: 0; bottom: 0;
  width: 1px;
  background: var(--border-strong);  /* #c8c0b4 */
}
.timeline-phase {
  position: relative;
  padding-left: 70px;
  margin-bottom: 2rem;
}
.phase-dot {
  position: absolute;
  left: 18px;
  top: 4px;
  width: 20px; height: 20px;
  border-radius: 50%;
  background: var(--bg-card);
  border: 2px solid var(--border-strong);
  display: flex; align-items: center; justify-content: center;
  font-size: 9px;
  font-weight: 700;
  font-family: 'DM Mono', monospace;
  color: var(--ink-muted);
}
.phase-dot.active {
  border-color: var(--accent-gold);
  background: var(--accent-gold);
  color: #ffffff;
}
.phase-dot.future {
  border-color: var(--accent-teal);
  /* background remains var(--bg-card) — hollow */
}
.phase-label {
  font-family: 'DM Mono', monospace;
  font-size: 10px;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--accent-gold);
  margin-bottom: 4px;
}
.phase-title {
  font-size: 15px;
  font-weight: 600;
  color: var(--ink);
  margin-bottom: 0.6rem;
}
.phase-body {
  font-size: 13.5px;
  color: var(--ink-dim);
  line-height: 1.65;
}
```

**Phase dot states:**
- Default: hollow, `--border-strong` border, number in `--ink-muted`
- `.active`: filled gold, white number
- `.future`: hollow, teal border, number in `--ink-muted`

---

## Component: Phase Checklist

Checklist with custom empty checkbox squares:

```css
.phase-checklist {
  list-style: none;
  margin-top: 0.7rem;
}
.phase-checklist li {
  font-size: 13px;
  color: var(--ink-dim);
  padding: 4px 0;
  display: flex;
  gap: 8px;
  align-items: flex-start;
}
.phase-checklist li .ck {
  width: 14px; height: 14px;
  border: 1.5px solid var(--border-strong);
  border-radius: 3px;
  flex-shrink: 0;
  margin-top: 2px;
}
```

**HTML:**
```html
<ul class="phase-checklist">
  <li><span class="ck"></span>Checklist item text here.</li>
</ul>
```

---

## Component: Salary Bar Rows (Dark Panel)

Used inside `.salary-section` (dark panel). Progress bars with DM Mono range labels:

```css
.salary-rows { display: flex; flex-direction: column; gap: 1px; }
.salary-row {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 0.9rem 1rem;
  background: rgba(255,255,255,0.03);
  border-radius: 4px;
  flex-wrap: wrap;
}
.salary-row:hover { background: rgba(255,255,255,0.06); }
.salary-role { flex: 1; min-width: 180px; }
.salary-role-name {
  font-size: 13px;
  font-weight: 600;
  color: #e8e0d4;
}
.salary-role-note {
  font-size: 11px;
  color: #665f50;
  font-family: 'DM Mono', monospace;
}
.salary-bar-wrap { flex: 2; min-width: 200px; }
.salary-bar-track {
  height: 6px;
  background: rgba(255,255,255,0.06);
  border-radius: 3px;
}
.salary-bar-fill {
  height: 100%;
  border-radius: 3px;
  background: var(--accent-gold);
}
.salary-bar-fill.dim { background: #444444; }
.salary-nums {
  display: flex;
  justify-content: space-between;
  margin-top: 4px;
}
.salary-nums span {
  font-family: 'DM Mono', monospace;
  font-size: 11px;
  color: #a09880;
}
.salary-nums .hi {
  color: var(--accent-gold);
  font-weight: 600;
}
```

**HTML:**
```html
<div class="salary-row">
  <div class="salary-role">
    <div class="salary-role-name">Role Title</div>
    <div class="salary-role-note">annotation text</div>
  </div>
  <div class="salary-bar-wrap">
    <div class="salary-bar-track">
      <div class="salary-bar-fill" style="width:72%"></div>
    </div>
    <div class="salary-nums">
      <span>$120K</span>
      <span class="hi">$200K</span>
    </div>
  </div>
</div>
```

---

## Component: Proof / Small Info Cards

Small icon + title + description + status cards:

```css
.proof-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
  margin-bottom: 2rem;
}
.proof-card {
  background: var(--bg-card);
  border: var(--rule);
  border-radius: 8px;
  padding: 1.2rem;
}
.proof-card .proof-icon { font-size: 20px; margin-bottom: 0.6rem; }
.proof-card h4 {
  font-size: 13px;
  font-weight: 600;
  margin-bottom: 0.4rem;
  color: var(--ink);
}
.proof-card p {
  font-size: 12px;
  color: var(--ink-muted);
  line-height: 1.5;
}
.proof-exists {
  font-size: 11px;
  color: var(--accent-teal);
  font-family: 'DM Mono', monospace;
  margin-top: 6px;
  font-weight: 600;
}
.proof-todo {
  font-size: 11px;
  color: var(--accent-gold);
  font-family: 'DM Mono', monospace;
  margin-top: 6px;
  font-weight: 600;
}
```

---

## Component: Numbered Signal List

Numbered items in a stacked card list for prose tips or key points:

```css
.signal-list {
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
  margin-bottom: 1.5rem;
}
.signal-item {
  display: flex;
  gap: 1rem;
  align-items: flex-start;
  padding: 0.8rem 1rem;
  background: var(--bg-card);
  border: var(--rule);
  border-radius: 6px;
  font-size: 13.5px;
  color: var(--ink-dim);
}
.signal-item .si-num {
  font-family: 'DM Mono', monospace;
  font-size: 11px;
  color: var(--ink-muted);
  flex-shrink: 0;
  min-width: 20px;
}
```

---

## Component: Inline Code

```css
code {
  font-family: 'DM Mono', monospace;
  font-size: 12px;
  background: var(--bg);
  border: 1px solid var(--border);
  padding: 1px 5px;
  border-radius: 3px;
  color: var(--accent-blue);
}
```

---

## Component: Document Footer

```css
.doc-footer {
  border-top: var(--rule);
  padding: 2rem 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1rem;
}
.doc-footer p {
  font-family: 'DM Mono', monospace;
  font-size: 11px;
  color: var(--ink-muted);
  letter-spacing: 0.05em;
}
```

---

## Animation & Motion

**No keyframe animations** are present in this design system. Motion is limited to transitions only:

```css
/* Navigation tab hover */
.nav-tab {
  transition: color 0.15s, border-color 0.15s;
}

/* Salary row hover */
.salary-row {
  /* No transition — instant background change on hover */
}
```

This is a deliberate choice: the system projects analytical authority, not playfulness. All state changes are instant or near-instant (0.15s).

---

## Responsive Breakpoints

### `@media (max-width: 600px)`

```css
.split-grid { grid-template-columns: 1fr; }
```

The `.split-grid` collapses from 2 columns to 1 column at 600px.

All other grids use `repeat(auto-fit, minmax(Npx, 1fr))` which self-collapses responsively without explicit breakpoints.

### `@media print`

```css
.sticky-nav { display: none; }
```

The sticky navigation is hidden in print mode. All other content prints as-is.

---

## Micro-details & Signature Patterns

### The Eyebrow Label Pattern

Every major content region begins with an eyebrow label — a small DM Mono ALL-CAPS monospace line above the serif headline, gold-colored:

```html
<div class="eyebrow">Context · Sub-context · Date or scope</div>
<h1>Main <em>Serif</em> Headline</h1>
```

The `·` (middle dot, U+00B7) is the preferred separator character in eyebrow labels.

### The Section Number + Title Pattern

Every section is introduced by a numbered `01` / `02` pattern in DM Mono beside a DM Serif Display title, separated by a full-width ruled line below:

```html
<div class="section-header">
  <span class="section-number">01</span>
  <h2 class="section-title">Section Title Here</h2>
</div>
```

### The "Gap as Border" Grid Trick

The `.signal-grid` uses `gap: 1px; background: var(--border)` on the grid container with `background: var(--bg-card)` on each cell. The grid background bleeds through the 1px gaps, creating perfectly hairline borders between cells — no individual cell borders needed.

### The Negative Margin Full-Bleed Trick

Any section that needs to break out of the page container uses `margin: 0 -2rem` to bleed horizontally while maintaining the `.page`'s `padding: 0 2rem`:
- `.verdict-strip`: `margin: 0 -2rem`
- `.salary-section`: `margin: 0 -2rem`

### The 3px Top-Border Category Accent

Role cards and split cards use a `3px solid [accent-color]` top border as the primary category signal. The card border itself is the neutral `--border`. This creates a clean visual hierarchy: category → content.

### Icon / Symbol Vocabulary

| Symbol | Context | Color |
|---|---|---|
| `·` (U+00B7) | Eyebrow label separator | inherited gold |
| `→` | Default split-card list marker | `--ink-muted` |
| `✕` | Threat/negative list marker | `--accent-red` |
| `✓` | Opportunity/positive list marker | `--accent-teal` |
| `★` | Best-fit banner prefix | in `.best-fit-banner` gold |
| `⚠` | Warning/todo prefix | in `.proof-todo` text |
| `—` | Em-dash used inline in prose | standard typography |

### Border-Radius Philosophy

This design uses minimal radius:
- `20px` — pill shape: priority badges, already-badges, best-fit banner
- `10px` — role cards
- `8px` — signal grid (outer only), split cards, proof cards
- `6px` — callout (right sides only), table header corners, signal items
- `4px` — tags (tech chips), salary bar tracks, salary rows
- `3px` — inline code, checkboxes
- `0px` — callout left edge (flat against border accent), table cells

**Rule:** Never round the side that has a color-accent border. The callout's left side is `0px` because rounding would break the left-border visual.

---

## Design Rules — Do & Don't

### DO

- **Always use DM Mono for any text smaller than 13px** — never Space Grotesk below 13px
- **Always use DM Serif Display for display-scale numbers** — the `.signal-num` pattern looks wrong in any other font
- **Always use the `·` separator in eyebrow labels** — comma or pipe breaks the rhythm
- **Gold accents are for authority and achievement only** — eyebrows, section numbers, active states, "best" banners; never use gold for body text
- **Teal is for positive/existence signals** — salaries, "have", "opportunity", teal role cards
- **Red is for warnings and threats only** — never decorative
- **Maintain the light body + dark masthead + one dark inversion section structure** — this rhythm is what distinguishes the design from a generic dark-mode or light-mode layout
- **Use the negative-margin full-bleed trick** (`margin: 0 -2rem`) for verdict strips and inversion panels to break container bounds
- **Use `border-radius: 0 6px 6px 0` on callout boxes** — never fully round a component with a left-border accent
- **Table headers must be `var(--ink-2)` (#1e2530) dark** — they anchor the table and echo the masthead
- **All metadata, labels, badges, nav, footer = DM Mono** — zero exceptions
- **The `border-collapse: collapse` pattern for tables** — no cell spacing

### DON'T

- **Never use gradients anywhere** — not on backgrounds, not on cards, not on buttons. Every fill is flat.
- **Never add hover animations longer than 0.2s** — this is a document, not a landing page
- **Never use Inter, Roboto, or system-ui** — they destroy the editorial character
- **Never use border-radius > 10px on cards** — except the 20px pill badges
- **Never make the entire page dark** — the system's signature is the contrast between the dark masthead and the warm parchment body
- **Never use shadow or glow effects** — no `box-shadow`, no `text-shadow`, no `filter: drop-shadow`
- **Never use blue as the primary brand color** — blue is informational only (medium priority, inline code). Gold and teal carry the brand
- **Never put ALL CAPS in Space Grotesk** — only DM Mono carries uppercase labels
- **Never give section titles a font-weight above 400** — DM Serif Display is always 400; weight comes from size and serif presence, not bold
- **Never use the `--accent-purple` for anything other than the agent/AI category top-bar stripe** — it has no other role in this system
- **Never add borders to tech chip `.tag` containers** — only the individual tags get `border: 1px solid var(--border)`

---

## Composing a New Application in This System

### Base HTML Scaffold

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document Title — 2026</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Mono:wght@400;500&family=Space+Grotesk:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --ink: #0d1117;
    --ink-2: #1e2530;
    --ink-dim: #4a5568;
    --ink-muted: #718096;
    --bg: #f7f6f2;
    --bg-card: #ffffff;
    --bg-dark: #0d1117;
    --accent-gold: #c8922a;
    --accent-gold-light: #f5e6c8;
    --accent-teal: #0d7a5f;
    --accent-teal-light: #d1f0e8;
    --accent-red: #c0392b;
    --accent-red-light: #fdecea;
    --accent-blue: #1a5fa8;
    --accent-blue-light: #dbeafe;
    --accent-purple: #6b46c1;
    --accent-purple-light: #ede9fe;
    --border: #e2ddd6;
    --border-strong: #c8c0b4;
    --rule: 1px solid var(--border);
  }
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    font-family: 'Space Grotesk', sans-serif;
    background: var(--bg);
    color: var(--ink);
    font-size: 15px;
    line-height: 1.65;
    min-height: 100vh;
  }
  /* Paste all component CSS here */
</style>
</head>
<body>

<!-- MASTHEAD -->
<div class="masthead">
  <div class="masthead-inner">
    <div class="eyebrow">Context · Sub-context · Date</div>
    <h1>Primary <em>Italic Gold</em> Headline</h1>
    <p class="masthead-sub">Subtitle in Space Grotesk 15px at #a09880. Max-width 560px. Describes the document scope.</p>
    <div class="masthead-meta">
      <div class="meta-item">
        <span class="meta-label">Label</span>
        <span class="meta-value">Value</span>
      </div>
      <!-- Repeat meta-item as needed -->
    </div>
    <div class="verdict-strip">
      <span>Key finding:</span>
      <strong>The main verdict or takeaway in Space Grotesk 13px bold on gold background.</strong>
    </div>
  </div>
</div>

<!-- STICKY NAV -->
<nav class="sticky-nav">
  <div class="nav-inner">
    <a class="nav-tab" href="#section-1">Section One</a>
    <a class="nav-tab" href="#section-2">Section Two</a>
    <!-- Add tabs for each section -->
  </div>
</nav>

<!-- BODY CONTENT -->
<div class="page">

  <!-- SECTION with metric grid -->
  <div id="section-1">
    <div class="section-header">
      <span class="section-number">01</span>
      <h2 class="section-title">Section Title</h2>
    </div>
    <div class="signal-grid">
      <div class="signal-cell">
        <div class="signal-num">+85%</div>
        <div class="signal-label">Metric description</div>
      </div>
    </div>
    <div class="callout">
      <div class="callout-label">Context note</div>
      <p>Callout body text at 13.5px in #4a2c00 on gold-tinted background.</p>
    </div>
  </div>

  <!-- SECTION with split cards -->
  <div id="section-2">
    <div class="section-header">
      <span class="section-number">02</span>
      <h2 class="section-title">Comparison Section</h2>
    </div>
    <div class="split-grid">
      <div class="split-card threat">
        <h3>⚠ Negative Side</h3>
        <ul><li>Item one</li><li>Item two</li></ul>
      </div>
      <div class="split-card opp">
        <h3>✓ Positive Side</h3>
        <ul><li>Item one</li><li>Item two</li></ul>
      </div>
    </div>
  </div>

  <!-- DARK INVERSION SECTION (use once per document) -->
  <div id="section-dark" class="salary-section">
    <div class="section-header">
      <span class="section-number">03</span>
      <h2 class="section-title">Dark Panel Section</h2>
    </div>
    <div class="salary-rows">
      <div class="salary-row">
        <div class="salary-role">
          <div class="salary-role-name">Item Name</div>
          <div class="salary-role-note">annotation</div>
        </div>
        <div class="salary-bar-wrap">
          <div class="salary-bar-track">
            <div class="salary-bar-fill" style="width:72%"></div>
          </div>
          <div class="salary-nums"><span>Low</span><span class="hi">High</span></div>
        </div>
      </div>
    </div>
  </div>

  <!-- FOOTER -->
  <div class="doc-footer">
    <p>Document attribution · Date · Sources</p>
    <p>Additional colophon note</p>
  </div>

</div>
</body>
</html>
```

### Adapting Components for Common Needs

**Buttons:** No button component exists in the original. Follow the system: use DM Mono 11px uppercase, flat background, `var(--accent-gold)` fill for primary, `var(--border)` border for secondary, `border-radius: 4px` (not pill), no shadow.

**Forms / Inputs:** Use `border: var(--rule)`, `border-radius: 4px`, `font-family: 'Space Grotesk', sans-serif`, `font-size: 14px`, `padding: 8px 12px`. Labels above inputs use DM Mono 10px uppercase at `var(--ink-muted)`.

**Progress meters / percentages:** Adapt the `.salary-bar-track` + `.salary-bar-fill` pattern. Change `background` on `.salary-bar-fill` to match the relevant accent color.

**Alert / notification variants:** Adapt `.callout` — change the `border-left` color and `background` tint:
- Warning: `border-left: 3px solid var(--accent-gold)`, bg `var(--accent-gold-light)`
- Error: `border-left: 3px solid var(--accent-red)`, bg `var(--accent-red-light)`
- Success: `border-left: 3px solid var(--accent-teal)`, bg `var(--accent-teal-light)`
- Info: `border-left: 3px solid var(--accent-blue)`, bg `var(--accent-blue-light)`

**Data visualization charts:** Use `var(--accent-gold)`, `var(--accent-teal)`, `var(--accent-blue)`, `var(--accent-red)` as chart colors in that priority order. Background for chart containers: `var(--bg-card)` with `var(--rule)` border. Axis labels in DM Mono 11px `var(--ink-muted)`.

**Breadcrumbs / page paths:** DM Mono 11px at `var(--ink-muted)`, `·` separator, active item at `var(--ink)`.
