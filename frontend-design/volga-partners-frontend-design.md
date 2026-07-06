---
name: volga-partners-frontend-design
description: >
  Dark-tech, high-contrast interview prep UI with teal accent. Uses Fraunces (variable serif for headings), Geist (sans), JetBrains Mono (mono). Features subtle grid background, atmospheric glows, asymmetric layouts, left-border accents, and sophisticated interactive components like accordions, flashcards, and diagram viewers. Perfect for professional tech dashboards, documentation sites, or AI tool interfaces.
---

# Volga Partners Tech Interview Prep Design System — Design System Skill

## Concept & Aesthetic Direction
This is a premium dark-mode technical documentation / interview prep interface with a sophisticated cyber-tech aesthetic. It fuses modern variable typography, subtle grid overlays, teal neon accents, and precise left-border indicators. It feels professional yet futuristic — like a high-end dev tool or internal knowledge base for AI engineering teams. 

It is NOT generic Material or Tailwind defaults. It emphasizes precise variable fonts, layered paper backgrounds, ruled dividers, and interactive polish (magnifier lenses, 3D flashcards, live Graphviz).

Use this system for technical dashboards, RAG/knowledge tools, interview prep apps, or any product that needs to convey precision and expertise.

## Typography
**Google Fonts Import:**
```html
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght,SOFT,WONK@9..144,300..900,0..100,0..1&family=Geist:wght@300..900&family=JetBrains+Mono:ital,wght@0,300..700;1,300..700&display=swap" rel="stylesheet">
```

**Font Roles & Exact Specs:**

- **Fraunces (serif, variable)**: Primary display/headings
  - Hero H1: `font-variation-settings: "opsz" 144, "SOFT" 0, "WONK" 0`; `font-weight: 300`; `font-size: clamp(2.6rem, 6vw, 5rem)`; `line-height: 0.92`; `letter-spacing: -0.04em`
  - Emphasized text in H1: `"opsz" 144, "SOFT" 80, "WONK" 1`
  - Section titles: `"opsz" 72`; `font-size: 1.9rem`; `font-weight: 360`
  - Lede text: `"opsz" 36, "SOFT" 20`; `font-size: 1.08rem`
  - Flashcard questions: `"opsz" 72, "SOFT" 10`

- **Geist (sans-serif)**: Body text, values, answers
  - Base: `font-family: 'Geist', sans-serif`; `font-size: 1rem`; `line-height: 1.55`
  - Questions/strong text: `font-size: 0.93rem`; `font-weight: 600`

- **JetBrains Mono**: All UI labels, metadata, code, nav, mono elements
  - Uppercase labels, tabs, masthead: `font-size: 0.65-0.72rem`; `letter-spacing: 0.1-0.3em`; `text-transform: uppercase`
  - Code blocks: `font-size: 0.77-0.78rem`

## Color System
```css
:root {
  --paper:        #0b0f18;
  --paper-2:      #111827;
  --paper-3:      #1a2236;
  --tile:         #131c2e;
  --ink:          #e8edf5;
  --ink-2:        #c2cfe0;
  --muted:        #5e7394;
  --rule:         #1e2e44;
  --rule-soft:    #162033;
  --grid-line:    rgba(100,160,255,0.04);
  --teal:         #00c8a0;   /* Primary accent */
  --teal-soft:    #00a880;
  --blue:         #3b82f6;
  --amber:        #f59e0b;
  --violet:       #8b5cf6;
  --coral:        #f87171;
  /* Semantic difficulty */
  --easy:         #00c8a0;
  --intermediate: #3b82f6;
  --hard:         #8b5cf6;
  --other:        #f59e0b;
  --jd-col:       #f87171;
  /* Accents */
  --accent-1:     #00c8a0;
  /* ... full set as in :root */
  --code-bg:      #050910;
  --code-text:    #a8d8b8;
}
[data-theme="light"] { /* full light overrides with desaturated tones */ }
```

**Primary accent**: Teal `#00c8a0`. Used for borders, glows, active states, icons.

## Background & Atmosphere
- Body grid: `linear-gradient` 44px subtle blue grid.
- `body::before`: Fixed repeating scanline overlay with teal tint (opacity 0.22 dark / 0.06 light).
- `body::after`: Large fixed radial teal glow in top-right.
- Layering: z-index 0 (glow), 1 (scanline), 2 (content).

## Layout
- `.page-wrapper`: `max-width: 1200px`; centered; padding 1.5rem.
- Masthead/Hero/Footer: 3-column grid `1fr auto 1fr`.
- Hero: Asymmetric `1.3fr 1fr`.
- Ruled borders extensively used as dividers (top/bottom with `--rule` or `--teal`).

## Major Components

**Masthead & Hero**: Detailed in extraction.

**Q&A Accordion**: Left-accent hover, expandable with arrow rotation.

**Nav Tabs**: Color-coded active states per category.

**Flashcards**: 3D flip with `perspective`, front/back faces.

**Diagram Cards**: Hover magnifier lens + zoom panel + lightbox.

**Theme Toggle**: Fixed circular button with glow.

## Design Rules — Do & Don't
**Do:**
- Always use left-border teal accents for active/hover states.
- Use JetBrains Mono uppercase for all metadata/eyebrows.
- Apply text-shadow glows on teal elements.
- Maintain sharp 6px border-radius only on cards.
- Use variable font axes precisely for Fraunces.

**Don't:**
- Use border-radius > 6px.
- Apply generic shadows without teal glow component.
- Use sans-serif for headings.
- Forget the grid background and atmospheric layers.

## Composing a New Application in This System
```html
<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <!-- Fonts + variables -->
</head>
<body>
  <button class="theme-toggle">◑</button>
  <div class="page-wrapper">
    <!-- Masthead, Hero, etc. -->
  </div>
</body>
</html>
```

Adapt components by copying exact CSS classes and rules.

**Summary of Capture:**
- Fonts: Fraunces, Geist, JetBrains Mono
- Primary accent: Teal #00c8a0
- Theme: Dark/light with data-theme attribute + localStorage
- Components: 12+ (masthead, hero, accordion, tabs, flashcards, diagrams, etc.)
- Signature: Grid bg, left accents, variable typography, zoom interactions.