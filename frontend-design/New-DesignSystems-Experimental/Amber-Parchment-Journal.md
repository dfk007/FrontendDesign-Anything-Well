---
name: amber-parchment-journal
description: >
  Warm editorial-luxury design system for long-form reports, research briefs,
  and premium knowledge tools. Light parchment body with an inverted deep-
  espresso masthead, restrained burgundy accent, and gold rule dividers.
  Font stack: Source Serif 4 (display, drop-cap headlines), Public Sans
  (body), Space Mono (metadata/labels). Signature: drop-cap opening
  paragraphs, gold hairline rules, footnote-style citations, and an inverted
  masthead/footer that bookends a light-mode reading experience. Use for
  research reports, career/industry guides, premium documentation, and any
  long-form content meant to feel authoritative, print-native, and unhurried.
---

# Amber Parchment Journal — Design System Skill

## Concept & Aesthetic Direction

This system draws from high-end print journalism — The New Yorker's
restraint, Monocle's warmth, and old-world financial almanacs — translated
into a modern light-mode reading surface. It is **not** a dashboard system;
it is built for sustained reading. Content is the hero. Chrome is minimal
and always in service of hierarchy, never decoration.

The defining move is **inversion at the edges**: the body of the page is
warm parchment with dark ink text, but the masthead and footer invert to
deep espresso with parchment text and a gold rule — like a book cover
wrapping light pages. This bookending device is the system's signature and
should appear on every page built with it.

**Use for**: research reports, industry/career guides, long-form technical
documentation, premium newsletters, executive briefings, knowledge-base
articles.

**Do not use for**: real-time dashboards, dense data tables, chat/agent
interfaces, or anything requiring dark-mode-first density.

---

## Typography

**Google Fonts import (verified, free):**
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Source+Serif+4:opsz,wght@8..60,300..700&family=Public+Sans:wght@300..700&family=Space+Mono:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
```

### Source Serif 4 — Display & Editorial Voice
A variable optical-size serif. Use the `opsz` axis deliberately: high
optical size for large display headlines (sharper, more refined at scale),
lower optical size for pull-quotes and sub-heads (warmer, more booklike at
small sizes).

| Role | Size | Weight | `font-variation-settings` | Line-height |
|---|---|---|---|---|
| Masthead title | `1.4rem` | 600 | `"opsz" 40` | 1.1 |
| Hero headline | `clamp(2.4rem, 5.5vw, 4.2rem)` | 600 | `"opsz" 60` | 1.05 |
| Section headline | `1.85rem` | 600 | `"opsz" 40` | 1.15 |
| Pull-quote / lede | `1.3rem` | 400 italic | `"opsz" 20` | 1.45 |
| Drop cap | `4.2rem` | 700 | `"opsz" 60` | 0.8 |

Letter-spacing on all Source Serif 4 headings: `-0.01em` (default; do not
tighten further — this font reads worse over-tracked-negative).

### Public Sans — Body
Clean, government-grade legible sans (originally built for USWDS) — chosen
for its exceptional readability at body sizes over long passages.

| Role | Size | Weight | Line-height | Max-width |
|---|---|---|---|---|
| Body paragraph | `1.05rem` | 400 | 1.72 | `68ch` |
| Lead paragraph | `1.2rem` | 400 | 1.6 | `62ch` |
| Caption / figure label | `0.85rem` | 400 italic | 1.5 | — |
| UI label (buttons, nav) | `0.85rem` | 600 | 1 | — |

### Space Mono — Metadata & Citation
Reserved strictly for numbers, dates, bylines, footnote markers, and
section counters — never for body prose.

| Role | Size | Weight | Letter-spacing | Transform |
|---|---|---|---|---|
| Eyebrow / kicker | `0.72rem` | 700 | `0.16em` | uppercase |
| Byline / date | `0.78rem` | 400 | `0.02em` | none |
| Footnote number | `0.7rem` | 700 | normal | none (superscript) |
| Page/section counter | `0.75rem` | 400 | `0.1em` | uppercase |

**Decision rule**: Source Serif 4 for anything meant to be *read* as
editorial voice (headlines, pull-quotes, drop caps). Public Sans for
anything meant to be *read* as body prose or UI copy. Space Mono for
anything that is a *fact/label* (date, number, byline, footnote) rather
than prose.

---

## Color System

```css
:root {
  /* Body surfaces — warm parchment, light-first */
  --parchment:     #F6F1E4;
  --parchment-2:   #EFE8D6;   /* card/panel surface */
  --parchment-3:   #E6DCC4;   /* hover/pressed surface */

  /* Inverted bookend surfaces */
  --espresso:      #241A12;
  --espresso-2:    #33251A;

  /* Text */
  --ink:           #241A12;   /* primary text on parchment */
  --ink-soft:      #5C4E3D;   /* secondary text on parchment */
  --cream:         #F6F1E4;   /* primary text on espresso */
  --cream-soft:    #C9BBA3;   /* secondary text on espresso */

  /* Rules & borders */
  --rule:          #D8CBA9;   /* standard divider on parchment */
  --rule-soft:     #E6DCC4;
  --rule-dark:     #4A3B29;   /* divider on espresso */

  /* Accent palette */
  --burgundy:      #7A2E2E;   /* primary accent — links, active states */
  --burgundy-soft: rgba(122, 46, 46, 0.08);
  --gold:          #B8862E;   /* rule lines, kickers, drop caps */
  --gold-soft:     rgba(184, 134, 46, 0.12);

  /* Semantic (sparing use) */
  --verdict-good:  #4A6B4A;
  --verdict-warn:  #A8752E;
  --verdict-bad:   #8C3A2E;
}

[data-theme="dark"] {
  --parchment:     #1A1510;
  --parchment-2:   #221C15;
  --parchment-3:   #2C241A;
  --ink:           #EDE4D0;
  --ink-soft:      #A99A80;
  --rule:          #3A2F22;
  --rule-soft:     #2C241A;
  --burgundy:      #C77A7A;
  --burgundy-soft: rgba(199, 122, 122, 0.10);
  --gold:          #D6AC5E;
  --gold-soft:     rgba(214, 172, 94, 0.10);
  /* espresso/cream bookend stays constant across themes —
     the masthead/footer inversion is the constant anchor */
}
```

**Color rules**:
- Burgundy is for interactive elements only (links, active nav, hover
  states on cards). Gold is for structural rules and kickers only. They
  never both appear as the dominant color of the same element.
- The espresso masthead/footer NEVER changes with theme — it is the fixed
  "cover" regardless of whether the page body is light or dark parchment.
- Drop caps are always gold, regardless of theme.

---

## Background & Atmosphere

Unlike dark-terminal systems, this system uses **paper texture, not glow**.
A very faint noise/grain texture on the parchment body suggests physical
paper without becoming visible pattern.

```css
body {
  background-color: var(--parchment);
  background-image:
    repeating-linear-gradient(
      0deg,
      rgba(36, 26, 18, 0.012) 0px,
      transparent 1px,
      transparent 2px
    );
}
```

No glow, no scanlines, no radial gradients. The only "atmospheric" element
is this near-invisible fiber texture — subtlety is the point.

**Masthead/footer inversion band** (the system's core atmospheric device):
```css
.masthead, .footer-band {
  background: var(--espresso);
  color: var(--cream);
  border-top: 3px solid var(--gold);
  border-bottom: 1px solid var(--rule-dark);
}
.footer-band {
  border-top: 1px solid var(--rule-dark);
  border-bottom: 3px solid var(--gold);
}
```

---

## Layout

```css
.page-wrapper {
  max-width: 780px;   /* narrow — optimized for reading, not dashboards */
  margin: 0 auto;
}
.content-inset { padding: 0 2rem; }
```

Note the deliberately narrow `780px` measure — this system prioritizes
line-length for readability over dashboard density. Full-bleed elements
(masthead, footer, pull-quote blocks) may exceed this width; body prose
never should.

### Masthead
```css
.masthead {
  padding: 1.1rem 2rem;
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  font-family: 'Space Mono', monospace;
  font-size: 0.7rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
}
.masthead .center {
  font-family: 'Source Serif 4', serif;
  font-variation-settings: "opsz" 40;
  font-weight: 600;
  font-size: 1.4rem;
  letter-spacing: -0.01em;
  text-transform: none;
  color: var(--gold);
  text-align: center;
}
.masthead .right { text-align: right; }
```

### Hero
```css
.hero { padding: 3.5rem 2rem 2.5rem; text-align: left; }
.hero .kicker {
  font-family: 'Space Mono', monospace;
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--burgundy);
  display: block;
  margin-bottom: 1rem;
}
.hero h1 {
  font-family: 'Source Serif 4', serif;
  font-variation-settings: "opsz" 60;
  font-weight: 600;
  font-size: clamp(2.4rem, 5.5vw, 4.2rem);
  line-height: 1.05;
  color: var(--ink);
}
.hero .byline {
  margin-top: 1.2rem;
  font-family: 'Space Mono', monospace;
  font-size: 0.78rem;
  color: var(--ink-soft);
  padding-top: 0.9rem;
  border-top: 1px solid var(--rule);
}
```

---

## Components

### Drop Cap (signature opening device)
Applied to the first paragraph of a major section:
```css
.drop-cap::first-letter {
  font-family: 'Source Serif 4', serif;
  font-variation-settings: "opsz" 60;
  font-weight: 700;
  font-size: 4.2rem;
  line-height: 0.8;
  float: left;
  padding: 0.05em 0.08em 0 0;
  color: var(--gold);
}
```

### Gold Hairline Rule (section divider)
```css
.hairline {
  border: none;
  border-top: 1px solid var(--gold);
  width: 60px;
  margin: 2.5rem 0;
}
.hairline.full {
  width: 100%;
  border-top: 1px solid var(--rule);
}
```

### Pull-Quote Block
```css
.pull-quote {
  margin: 2.5rem 0;
  padding: 0 0 0 1.6rem;
  border-left: 3px solid var(--burgundy);
  font-family: 'Source Serif 4', serif;
  font-variation-settings: "opsz" 20;
  font-style: italic;
  font-size: 1.3rem;
  line-height: 1.45;
  color: var(--ink);
}
.pull-quote .attribution {
  display: block;
  margin-top: 0.8rem;
  font-family: 'Space Mono', monospace;
  font-style: normal;
  font-size: 0.75rem;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  color: var(--ink-soft);
}
```

### Footnote / Citation
```css
.footnote-ref {
  font-family: 'Space Mono', monospace;
  font-size: 0.7rem;
  font-weight: 700;
  color: var(--burgundy);
  vertical-align: super;
  cursor: pointer;
}
.footnotes {
  margin-top: 3rem;
  padding-top: 1.5rem;
  border-top: 1px solid var(--rule);
  font-family: 'Public Sans', sans-serif;
  font-size: 0.82rem;
  color: var(--ink-soft);
  line-height: 1.6;
}
.footnotes li { margin-bottom: 0.6rem; }
```

### Verdict Banner (report conclusion strip — inverted, full-bleed)
```css
.verdict-banner {
  background: var(--espresso);
  color: var(--cream);
  padding: 2rem;
  border-top: 3px solid var(--gold);
  border-bottom: 3px solid var(--gold);
  text-align: center;
  margin: 3rem 0;
}
.verdict-banner .label {
  font-family: 'Space Mono', monospace;
  font-size: 0.72rem;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--gold);
  display: block;
  margin-bottom: 0.6rem;
}
.verdict-banner .verdict {
  font-family: 'Source Serif 4', serif;
  font-variation-settings: "opsz" 40;
  font-weight: 600;
  font-size: 1.6rem;
}
```

### Card (for report sections, resource lists)
```css
.card {
  background: var(--parchment-2);
  border: 1px solid var(--rule);
  border-left: 3px solid var(--burgundy);
  padding: 1.5rem 1.75rem;
  border-radius: 2px;   /* the one soft exception in this system */
}
.card:hover { background: var(--parchment-3); }
.card .card-kicker {
  font-family: 'Space Mono', monospace;
  font-size: 0.68rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--burgundy);
  margin-bottom: 0.5rem;
}
```

### Footer Band
```css
.footer-band {
  padding: 1.4rem 2rem;
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  font-family: 'Space Mono', monospace;
  font-size: 0.68rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
}
.footer-band .center { color: var(--gold); text-align: center; }
```

---

## Animation & Motion

Minimal — this system favors stillness over motion, consistent with print.

```css
@keyframes settle {
  from { opacity: 0; transform: translateY(10px); }
  to   { opacity: 1; transform: translateY(0); }
}
.block { animation: settle 0.6s ease forwards; }
.block:nth-child(2) { animation-delay: 0.1s; }
.block:nth-child(3) { animation-delay: 0.2s; }
```

Transitions on interactive elements: `0.2s ease` for background/border
changes. No motion on scroll, no parallax — this system is deliberately
calm.

---

## Responsive Breakpoints

```css
@media (max-width: 720px) {
  .masthead, .footer-band { grid-template-columns: 1fr; text-align: center; gap: 0.4rem; }
  .content-inset { padding: 0 1.25rem; }
  .drop-cap::first-letter { font-size: 3rem; }
  .pull-quote { font-size: 1.1rem; padding-left: 1.2rem; }
}
```

## Print

```css
@media print {
  body { background: #fff; }
  .masthead, .footer-band { background: #fff !important; color: #000 !important; }
  .verdict-banner { background: #fff !important; color: #000 !important; border-color: #000; }
}
```
This system is inherently print-friendly by design; the print stylesheet
mainly neutralizes the inverted espresso bands so they don't waste toner.

---

## Design Rules — Do & Don't

### Do
- Reserve the espresso inversion for masthead, footer, and verdict banners
  only — it is a bookending device, not a general-purpose dark panel.
- Use the drop cap on the first paragraph of the hero/lede section only,
  not on every section.
- Keep body measure at or under `68ch` (roughly `780px` at base font size).
- Use gold exclusively for rules, kickers, and drop caps — never for large
  fills or buttons.
- Use burgundy exclusively for interactive/actionable elements (links,
  active states, card left-borders).

### Don't
- Never use more than one drop cap per page.
- Never put body prose inside the espresso-inverted bands — they're for
  short, declarative labels and verdicts only.
- Never use Space Mono for anything longer than a short label or citation
  — it kills readability in paragraph form.
- Never widen the reading column past ~800px; this system is not a
  dashboard grid.
- Never add glow, shadow-blur, or gradients — depth comes from the
  parchment/espresso surface contrast alone.

---

## Composing a New Application in This System

```html
<!DOCTYPE html>
<html lang="en" data-theme="light">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>REPORT TITLE · Amber Parchment Journal</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Source+Serif+4:opsz,wght@8..60,300..700&family=Public+Sans:wght@300..700&family=Space+Mono:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
  <style>
    /* 1. Tokens (light default + dark override) */
    /* 2. Reset + body texture */
    /* 3. .page-wrapper (780px) + .content-inset */
    /* 4. .masthead (inverted espresso) */
    /* 5. .hero + kicker + byline */
    /* 6. .drop-cap, .hairline, .pull-quote, .footnote-ref */
    /* 7. .card, .verdict-banner */
    /* 8. .footer-band (inverted espresso) */
    /* 9. Motion (settle keyframe) */
    /* 10. Responsive + print */
  </style>
</head>
<body>
  <div class="masthead block">
    <span class="left">Vol. I · No. 1</span>
    <span class="center">Journal Title</span>
    <span class="right">July 2026</span>
  </div>
  <div class="page-wrapper">
    <div class="content-inset">
      <section class="hero block">
        <span class="kicker">// Research Brief</span>
        <h1>The Headline Goes<br>Here, Set Large</h1>
        <div class="byline">By Author Name · 12 min read</div>
      </section>
      <p class="drop-cap block">Opening paragraph text begins here with a
      dramatic drop capital that anchors the reading experience...</p>
      <hr class="hairline block" />
      <blockquote class="pull-quote block">
        A key insight rendered as an editorial pull-quote.
        <span class="attribution">— Source, Context</span>
      </blockquote>
      <div class="verdict-banner block">
        <span class="label">Verdict</span>
        <div class="verdict">Recommended, with reservations.</div>
      </div>
    </div>
  </div>
  <div class="footer-band block">
    <span class="left">◈ Journal Name</span>
    <span class="center">End of Report</span>
    <span class="right">Page 1 of 1</span>
  </div>
</body>
</html>
```

### Adapting other components
- **Buttons**: `border: 1.5px solid var(--burgundy)`, `color: var(--burgundy)`,
  `border-radius: 2px`, fill burgundy on hover with cream text.
- **Tables**: header row in Space Mono uppercase with `border-bottom: 2px
  solid var(--gold)`; body rows in Public Sans with `border-bottom: 1px
  solid var(--rule)`.
- **Forms**: input borders `1px solid var(--rule)`, focus state
  `border-color: var(--burgundy)` — no glow, just a color shift plus a
  1px inset burgundy line.
- **Navigation lists**: numbered in Space Mono (`01 ·`, `02 ·`) with gold
  numerals, titles in Source Serif 4.
