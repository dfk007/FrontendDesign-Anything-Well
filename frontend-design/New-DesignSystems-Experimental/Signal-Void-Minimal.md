---
name: signal-void-minimal
description: >
  Ultra-minimal cyber-precision system for AI tools, monitoring dashboards,
  and single-purpose utilities. Near-pure-black void backgrounds, one
  crisp cyan signal accent, razor-sharp geometry, extreme whitespace, and
  data rendered as the primary visual content. Font stack: Michroma
  (condensed geometric display, sparing use), Inter (UI/body), JetBrains
  Mono (data). Signature: hairline focus rings, pulse-dot status
  indicators, orbital stat rings, and a command-palette-style search
  affordance. Use for AI agent consoles, telemetry dashboards, model
  monitoring tools, and futuristic single-purpose utilities that need to
  feel precise, quiet, and high-signal rather than busy or decorative.
---

# Signal Void Minimal — Design System Skill

## Concept & Aesthetic Direction

This system draws on sci-fi operating-system interfaces (think mission
control, not cyberpunk street neon) and modern minimalist SaaS. The
governing principle is **signal-to-noise**: nearly everything on the page
is void — pure dark space — and the few elements that appear (a number, a
status dot, a single line of type) are the entire point of the screen.

Where other systems in this collection use texture (grids, scanlines,
grain) to add atmosphere, this system uses **absence** — vast negative
space is the atmosphere. The one accent, a crisp signal-cyan, is used with
total restraint: a hairline ring, a small dot, a thin underline. It never
fills large areas.

**Use for**: AI agent/eval consoles, model monitoring and observability
dashboards, single-metric utilities, command-palette-driven tools,
real-time telemetry displays.

**Do not use for**: content-heavy documentation, long-form reading,
marketing pages, or anything where warmth/approachability is the goal.

---

## Typography

**Google Fonts import (verified, free):**
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Michroma&family=Inter:wght@300..800&family=JetBrains+Mono:wght@400..700&display=swap" rel="stylesheet">
```

### Michroma — Display (used sparingly, never for body)
A geometric, evenly-spaced display face with a technical/sci-fi character.
Because it has only one weight (400) and no italic, it is used exclusively
for short, high-impact moments — never more than one Michroma element
visible per screen at a time.

| Role | Size | Letter-spacing | Usage limit |
|---|---|---|---|
| App wordmark | `0.95rem` | `0.08em` | Once, in the nav/header |
| Hero stat headline | `clamp(3rem, 9vw, 6.5rem)` | `-0.01em` | Once per view — the single "hero number" |

### Inter — UI & Body
Handles everything else: navigation, buttons, prose, panel titles.

| Role | Size | Weight | Line-height | Letter-spacing |
|---|---|---|---|---|
| Panel title | `0.95rem` | 600 | 1.3 | `-0.005em` |
| Body / description | `0.9rem` | 400 | 1.6 | normal |
| Nav item | `0.85rem` | 500 | 1 | `-0.005em` |
| Button label | `0.82rem` | 600 | 1 | `0.01em` |
| Micro label | `0.72rem` | 500 | 1.2 | `0.02em` |

### JetBrains Mono — Data
All numeric/status content: metrics, timestamps, IDs, log lines, coordinates.

| Role | Size | Weight | Letter-spacing | Transform |
|---|---|---|---|---|
| Stat sub-label | `0.68rem` | 500 | `0.14em` | uppercase |
| Table/log data | `0.82rem` | 400 | normal | none |
| Timestamp | `0.72rem` | 400 | `0.02em` | none |
| Status pill text | `0.68rem` | 600 | `0.1em` | uppercase |

**Decision rule**: Michroma for the single hero moment on a screen only.
Inter for everything a human reads as language (labels, descriptions,
nav). JetBrains Mono for everything that is data (numbers, IDs,
timestamps, logs).

---

## Color System

```css
:root {
  /* Void surfaces — true near-black, minimal steps */
  --void:        #050607;
  --void-2:      #0B0D10;   /* panel surface */
  --void-3:      #12151A;   /* hover/elevated surface */

  /* Text */
  --text-hi:     #EDF1F5;
  --text-lo:     #6B7480;
  --text-dim:    #3E454E;   /* tertiary, near-invisible labels */

  /* Hairlines */
  --line:        #1B1F26;
  --line-hi:     #2A303A;

  /* The one accent — signal cyan */
  --signal:      #4CE0FF;
  --signal-dim:  rgba(76, 224, 255, 0.08);
  --signal-ring: rgba(76, 224, 255, 0.25);

  /* Secondary accent — used ONLY for critical alerts, never alongside signal */
  --alert:       #FF4C6D;
  --alert-dim:   rgba(255, 76, 109, 0.08);

  /* Status */
  --status-live: var(--signal);
  --status-idle: var(--text-lo);
  --status-error: var(--alert);
}

[data-theme="light"] {
  /* This system is dark-native; "light" mode raises the void floor
     rather than inverting to white, preserving the void's character */
  --void:        #E8EBEF;
  --void-2:      #F3F5F8;
  --void-3:      #FFFFFF;
  --text-hi:     #0B0D10;
  --text-lo:     #5C6570;
  --text-dim:    #9AA2AC;
  --line:        #D3D8DE;
  --line-hi:     #BCC3CC;
  --signal:      #0090AD;   /* darkened for AA contrast on light void */
  --signal-dim:  rgba(0, 144, 173, 0.08);
  --signal-ring: rgba(0, 144, 173, 0.25);
  --alert:       #D62E4E;
  --alert-dim:   rgba(214, 46, 78, 0.08);
}
```

**Color rules**:
- Signal-cyan never fills an area larger than a status dot or a 1–2px
  ring/line. If you need a larger highlighted area, use `--signal-dim`
  as a background wash instead of full-opacity signal.
- Alert-red follows the identical restraint rule and is mutually
  exclusive with signal-cyan in any single component — a component is
  either in a "nominal" (signal) or "error" (alert) state, never both.
- Text hierarchy is three steps only: `--text-hi` (primary), `--text-lo`
  (secondary/labels), `--text-dim` (near-invisible chrome, e.g. disabled
  states or watermark-level annotations).

---

## Background & Atmosphere

The void itself is the atmosphere. There is no grid, no grain, no glow by
default — only when a panel is actively "live" does it emit a very
subtle signal-tinted radial glow to indicate real-time state.

```css
body {
  background: var(--void);
}

/* Applied only to panels currently receiving live data —
   not a global effect */
.panel.is-live {
  position: relative;
}
.panel.is-live::after {
  content: '';
  position: absolute;
  top: -40%; right: -20%;
  width: 240px; height: 240px;
  background: radial-gradient(circle, var(--signal-dim) 0%, transparent 70%);
  pointer-events: none;
  z-index: 0;
}
```

This is the opposite approach from ambient-glow systems: glow here is
**earned, not ambient** — it signals "this element is actively updating,"
not "this is the theme."

---

## Layout

```css
.page-wrapper {
  max-width: 1400px;
  margin: 0 auto;
  padding: 2.5rem 3rem 6rem;
}
```

Whitespace scale (use consistently — this system depends on rhythm):
```css
:root {
  --space-1: 0.5rem;
  --space-2: 1rem;
  --space-3: 1.75rem;
  --space-4: 3rem;
  --space-5: 5rem;
  --space-6: 8rem;
}
```

### Nav bar (thin, floating, no border unless scrolled)
```css
.topnav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1.5rem 0;
}
.topnav .wordmark {
  font-family: 'Michroma', sans-serif;
  font-size: 0.95rem;
  letter-spacing: 0.08em;
  color: var(--text-hi);
}
.topnav .wordmark .dot {
  color: var(--signal);
  margin-right: 0.4rem;
}
.topnav nav {
  display: flex;
  gap: 2.5rem;
  font-family: 'Inter', sans-serif;
  font-size: 0.85rem;
  font-weight: 500;
  color: var(--text-lo);
}
.topnav nav a.active { color: var(--text-hi); }
```

### Command Palette Trigger (signature affordance)
```css
.cmd-trigger {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  background: var(--void-2);
  border: 1px solid var(--line);
  padding: 0.55rem 0.9rem;
  color: var(--text-lo);
  font-family: 'Inter', sans-serif;
  font-size: 0.82rem;
  border-radius: 6px;
  cursor: pointer;
  transition: border-color 0.15s ease;
}
.cmd-trigger:hover { border-color: var(--line-hi); }
.cmd-trigger kbd {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.68rem;
  background: var(--void-3);
  border: 1px solid var(--line-hi);
  border-radius: 3px;
  padding: 0.1rem 0.35rem;
  color: var(--text-dim);
}
```

---

## Components

### Hero Stat (the single largest visual element on any screen)
```css
.hero-stat {
  padding: var(--space-5) 0 var(--space-4);
  text-align: left;
}
.hero-stat .label {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.68rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--signal);
  display: block;
  margin-bottom: 1rem;
}
.hero-stat .value {
  font-family: 'Michroma', sans-serif;
  font-size: clamp(3rem, 9vw, 6.5rem);
  color: var(--text-hi);
  letter-spacing: -0.01em;
  line-height: 1;
}
.hero-stat .value .unit {
  font-family: 'Inter', sans-serif;
  font-size: 0.35em;
  font-weight: 400;
  color: var(--text-lo);
  margin-left: 0.5rem;
}
```

### Pulse-Dot Status Indicator (signature idiom)
```css
.pulse-dot {
  width: 8px; height: 8px;
  border-radius: 50%;
  background: var(--signal);
  display: inline-block;
  position: relative;
}
.pulse-dot::after {
  content: '';
  position: absolute;
  inset: -4px;
  border-radius: 50%;
  border: 1px solid var(--signal);
  animation: pulse-ring 2s ease-out infinite;
}
@keyframes pulse-ring {
  0%   { transform: scale(0.6); opacity: 0.8; }
  100% { transform: scale(2.2); opacity: 0; }
}
.pulse-dot.error { background: var(--alert); }
.pulse-dot.error::after { border-color: var(--alert); }
.pulse-dot.idle { background: var(--text-dim); }
.pulse-dot.idle::after { display: none; }
```

### Orbital Stat Ring (secondary metric visualization)
```css
.stat-ring {
  width: 84px; height: 84px;
  position: relative;
}
.stat-ring svg { transform: rotate(-90deg); }
.stat-ring circle {
  fill: none;
  stroke-width: 3;
}
.stat-ring .track { stroke: var(--line); }
.stat-ring .fill {
  stroke: var(--signal);
  stroke-linecap: round;
  transition: stroke-dashoffset 0.6s ease;
}
.stat-ring .center-label {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.78rem;
  color: var(--text-hi);
}
```

### Panel (base container — hairline border only)
```css
.panel {
  background: var(--void-2);
  border: 1px solid var(--line);
  border-radius: 8px;
  padding: var(--space-3);
}
.panel-title {
  font-family: 'Inter', sans-serif;
  font-weight: 600;
  font-size: 0.95rem;
  color: var(--text-hi);
  margin-bottom: var(--space-2);
  display: flex;
  align-items: center;
  gap: 0.6rem;
}
```

### Hairline Focus Ring (signature focus/selection idiom)
```css
:focus-visible {
  outline: none;
  box-shadow: 0 0 0 1px var(--void), 0 0 0 3px var(--signal-ring);
  border-radius: 4px;
}
.selectable.is-selected {
  border: 1px solid var(--signal);
  box-shadow: 0 0 0 3px var(--signal-ring);
}
```
This 1px-border-plus-3px-ring combination is the system's precise,
technical alternative to a soft glow — it reads as a targeting reticle,
not a blur.

### Log Line (for telemetry/event streams)
```css
.log-line {
  display: grid;
  grid-template-columns: 90px 70px 1fr;
  gap: 1rem;
  padding: 0.5rem 0;
  border-bottom: 1px solid var(--line);
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.78rem;
}
.log-line .ts { color: var(--text-dim); }
.log-line .level { text-transform: uppercase; letter-spacing: 0.05em; }
.log-line .level.info { color: var(--signal); }
.log-line .level.error { color: var(--alert); }
.log-line .msg { color: var(--text-lo); }
```

### Button
```css
.btn {
  font-family: 'Inter', sans-serif;
  font-weight: 600;
  font-size: 0.82rem;
  padding: 0.65rem 1.3rem;
  border-radius: 6px;
  border: 1px solid var(--line-hi);
  background: transparent;
  color: var(--text-hi);
  cursor: pointer;
  transition: border-color 0.15s ease, box-shadow 0.15s ease;
}
.btn:hover { border-color: var(--signal); }
.btn.primary {
  background: var(--signal);
  color: var(--void);
  border-color: var(--signal);
}
.btn.primary:hover { box-shadow: 0 0 0 3px var(--signal-ring); }
```

### Status Badge
```css
.badge {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.68rem;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  padding: 0.3rem 0.65rem;
  border-radius: 4px;
  background: var(--signal-dim);
  color: var(--signal);
}
.badge.error { background: var(--alert-dim); color: var(--alert); }
.badge.idle { background: transparent; color: var(--text-dim); border: 1px solid var(--line); }
```

---

## Animation & Motion

Minimal, purposeful, never decorative. Motion communicates state change
only — it never plays for its own sake.

```css
@keyframes fade-rise {
  from { opacity: 0; transform: translateY(8px); }
  to   { opacity: 1; transform: translateY(0); }
}
.block { animation: fade-rise 0.5s ease forwards; }
.block:nth-child(2) { animation-delay: 0.06s; }
.block:nth-child(3) { animation-delay: 0.12s; }
.block:nth-child(4) { animation-delay: 0.18s; }
```

The `pulse-ring` keyframe (see Pulse-Dot component) is the only continuous
looping animation permitted in this system, and it is reserved
exclusively for "live" status indicators — never used decoratively.

Standard interactive transitions: `0.15s ease` for border/color/shadow.
`0.6s ease` for data-driven transitions (e.g., stat ring fill updates).

---

## Responsive Breakpoints

```css
@media (max-width: 860px) {
  .page-wrapper { padding: 1.5rem 1.25rem 4rem; }
  .topnav nav { display: none; } /* collapse into cmd-trigger only */
  .hero-stat .value { font-size: clamp(2.4rem, 12vw, 3.5rem); }
  .log-line { grid-template-columns: 60px 1fr; }
  .log-line .level { display: none; }
}
```

## Print
This system is not intended for print (real-time dashboards don't print
meaningfully); if print support is required, fall back to a flat
light-mode rendering with all `::after` glow effects removed and pulse
animations disabled.

---

## Design Rules — Do & Don't

### Do
- Treat whitespace as a primary design element — when in doubt, remove
  content or increase spacing rather than adding a border to separate
  things.
- Use exactly one Michroma element per screen — the hero stat/wordmark.
  More than one competes for attention and breaks the "single signal"
  premise.
- Keep signal-cyan restricted to: dots, thin rings/borders, small text,
  and `-dim` background washes. Never a large solid fill.
- Use the pulse-dot exclusively to mean "this is live/updating right now."
- Use the hairline focus ring (1px border + 3px soft ring) for all
  selection/focus states instead of glow-blur.

### Don't
- Never use more than 2 accent colors visible at once (signal + alert,
  and only when showing a genuine error state).
- Never fill large background areas with signal-cyan or alert-red.
- Never add decorative looping animation outside the pulse-dot idiom.
- Never use Michroma for body text or more than a few words at a time —
  it has poor readability past short strings.
- Never crowd panels — maintain generous internal padding
  (`var(--space-3)` minimum) even when data density tempts you to
  tighten it.

---

## Composing a New Application in This System

```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>APP NAME — Signal Void Minimal</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Michroma&family=Inter:wght@300..800&family=JetBrains+Mono:wght@400..700&display=swap" rel="stylesheet">
  <style>
    /* 1. Tokens (dark-native + light override) */
    /* 2. Reset + body void background */
    /* 3. .page-wrapper + spacing scale */
    /* 4. .topnav + .cmd-trigger */
    /* 5. .hero-stat */
    /* 6. .panel, .pulse-dot, .stat-ring, .log-line */
    /* 7. .btn, .badge */
    /* 8. Focus ring + motion (fade-rise, pulse-ring) */
    /* 9. Responsive */
  </style>
</head>
<body>
  <div class="page-wrapper">
    <div class="topnav block">
      <span class="wordmark"><span class="dot">●</span>APP NAME</span>
      <nav>
        <a href="#" class="active">Overview</a>
        <a href="#">Agents</a>
        <a href="#">Logs</a>
      </nav>
      <div class="cmd-trigger">Search <kbd>⌘K</kbd></div>
    </div>
    <section class="hero-stat block">
      <span class="label">// Active Throughput</span>
      <div class="value">1,204<span class="unit">req/s</span></div>
    </section>
    <div class="panel is-live block">
      <div class="panel-title">
        <span class="pulse-dot"></span> Live Agent Status
      </div>
      <!-- log lines, stat rings, etc. -->
    </div>
  </div>
  <script>
    /* command palette open/close, live data polling, stat ring updates */
  </script>
</body>
</html>
```

### Adapting other components
- **Forms**: inputs use `background: var(--void-2)`, `border: 1px solid
  var(--line)`, focus applies the hairline-ring pattern directly.
- **Tables**: no cell borders — use `border-bottom: 1px solid var(--line)`
  on rows only, header row in Inter 600 uppercase-free (this system
  avoids uppercase body/table content, reserving uppercase for
  JetBrains Mono labels only).
- **Charts**: single-color line/area charts in `--signal`, gridlines in
  `--line` at reduced opacity, no fill gradients — flat `--signal-dim`
  fill under line charts only.
- **Modals**: `background: var(--void-2)`, `border: 1px solid
  var(--line-hi)`, backdrop `rgba(5,6,7,0.7)` with no blur.
