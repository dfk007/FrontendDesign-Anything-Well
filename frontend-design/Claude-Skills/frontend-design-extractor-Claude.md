---
name: frontend-design-extractor-dfk
description: >
  Extracts a complete, reusable frontend design system from any given HTML file and
  produces a standalone frontend-design SKILL.md that a separate AI can use to recreate
  the same look and feel for any new application — without access to the original file.
  Use this skill whenever the user gives you an HTML file and asks you to "capture the
  design system", "extract the design language", "create a skill from this HTML",
  "make a frontend-design skill", "document this UI's design", or "create a SKILL.md
  from this design". Also trigger when the user says things like "replicate this look",
  "extract the style", "document how this looks", or "I want to reuse this design".
  Always trigger when an HTML file is provided alongside any intent to capture, document,
  or reproduce its visual design system.
---

# Frontend Design Extractor — DFK

Given an HTML file, perform a thorough forensic analysis of its design system and
produce a fully self-contained `frontend-design SKILL.md` that encodes every design
decision precisely enough for another AI to recreate the same look and feel from
scratch, without ever seeing the original file.

---

## Step 0 — Locate and read the HTML file

If the file is already in context (visible as text), read it directly.
If only a path is given (e.g. `/mnt/user-data/uploads/index.html`), use the `view`
tool to read it. For large files, read in chunks: first lines 1–600, then 600–1200,
etc., until you have seen all CSS and all key structural HTML patterns. Do NOT stop
at the first chunk — missing the CSS or the HTML structure will produce an incomplete
skill.

Read the full file before writing anything.

---

## Step 1 — Forensic Extraction

Work through every layer of the file systematically. For each layer, extract exact
values — never summarize, approximate, or omit. An AI reading the output SKILL.md
must be able to reproduce precise pixel values, exact hex codes, exact font names,
exact `font-variation-settings`, and exact animation timings.

### 1A — Typography

For every font family used, extract:
- Full Google Fonts (or other CDN) import URL, verbatim
- Every role the font plays (headings, body, labels, code, metadata, nav, footer, etc.)
- Exact `font-size` values per role (include `clamp()` expressions verbatim)
- Exact `font-weight` per role
- Exact `line-height` per role
- Exact `letter-spacing` per role
- `text-transform` rules (uppercase, etc.)
- `font-style` rules (italic, normal)
- `font-variation-settings` axes per usage context (critical for variable fonts — extract every distinct set of axis values)
- When each font is used vs. the others (the decision logic)

### 1B — Color System

Extract the full CSS custom property token system:
- Every `--variable-name: value;` from `:root` and any theme overrides (e.g., `[data-theme="light"]`)
- Group by semantic role: backgrounds (layered depth), text hierarchy, borders/rules, accent palette, semantic aliases (difficulty tiers, priority levels, status), code block colors
- Note exactly which variable maps to which role
- For any `rgba()` values in backgrounds, overlays, glows, or grid lines: extract the exact R,G,B,A values
- Note the theme switching mechanism (attribute, class, media query) and how variables are overridden

### 1C — Background & Atmosphere

Extract every atmospheric technique applied to `body`, `body::before`, `body::after`,
or any full-bleed background element:
- Grid/dot/noise/texture patterns: exact `background-image` expressions, `background-size`
- Overlay pseudo-elements: `position`, `inset`, `z-index`, `opacity`, `background` (full repeating-gradient expressions)
- Ambient glows or radial gradients: exact position, size, color stops, `border-radius`
- Z-index stacking order for all layers
- Light theme overrides for atmospheric elements (opacity changes, color changes)

### 1D — Layout Architecture

Document the top-level page structure:
- Max-width container: exact value, centering method, padding
- Top-level grid or flex layout for the page
- Every major structural region (masthead, hero, meta strip, nav, content, footer): its CSS class, layout method (`grid`/`flex`), `grid-template-columns`, `gap`, `padding`, `border` rules, `align-items`/`justify-content`
- Multi-column hero/header layouts: exact column ratios (e.g., `1.3fr 1fr`)
- Border rules used as structural dividers (which edges, which `--variable`)

### 1E — Component Inventory

For every distinct interactive or visual component, document:
- Component name and purpose
- Exact CSS class names
- Full CSS rules (background, border, color, font, padding, transition, hover/active/open states)
- State variations (hover, focus, active, open, disabled, theme-specific)
- Any left-border accent pattern (the "active indicator" idiom)
- Glow / box-shadow expressions for interactive elements
- Collapse/expand behavior if applicable

Typical components to look for: navigation tabs, accordion/Q&A panels, search inputs,
metric/stat cells, pull-quote/lede blocks, chips/badges, toggle buttons, section headers
with extending ruled lines, footers, colophons.

### 1F — Micro-details & Signature Patterns

These are the details that make a design distinctive. Extract:
- Border-radius philosophy (sharp/0px everywhere? small exceptions? where?)
- Icon/symbol language (Unicode symbols used: ◆, ◈, ◑, ▼, →, ✅, etc. — list all found)
- Eyebrow label pattern (small monospace ALL-CAPS labels above headings)
- Ruled-line dividers used as decorative or structural elements
- Left-border color accent on hover or active states
- Glow text-shadow on accent-colored text (exact rgba values)
- Co-name / context-line pattern above H1
- Three-column masthead/footer layout
- Colophon / typeset credit line at bottom

### 1G — Animation & Motion

For every `@keyframes`, `transition`, or animation:
- Exact keyframe name and `from`/`to` values
- Which elements use it, with what `animation-delay` stagger pattern
- `animation-duration`, `animation-fill-mode`, `animation-timing-function`
- `transition` shorthand values per component (duration, property, easing)
- Theme transition on `body` (if present)

### 1H — Responsive Breakpoints

For every `@media` query:
- Exact breakpoint value
- Every layout change (grid-column collapse, flex-direction change, padding reduction, font-size reduction, border changes)
- Mobile text alignment overrides

### 1I — Print Styles

If `@media print` exists, document every override.

### 1J — JavaScript Behavior

Document every interactive behavior implemented in JS:
- Theme toggle (mechanism, localStorage key, default value)
- Tab/section switching (which elements toggle, which CSS classes)
- Accordion/expand (single-open vs. multi-open, class toggled)
- Search/filter (scope, matching logic)
- Any other interactions

---

## Step 2 — Synthesis & Skill Writing

After completing the extraction, write the output `frontend-design SKILL.md`.

The output must be **fully self-contained** — an AI reading it must never need to see
the original HTML file. Every section must contain exact values, never vague
descriptions.

### Required sections in the output SKILL.md

Use this structure (adapt headings to the actual design system found):

```
---
name: frontend-design
description: >
  [One paragraph: name the aesthetic, name the primary accent, name the fonts,
   name the key structural patterns. Mention when to use this system.]
---

# [Design System Name] — Design System Skill

## Concept & Aesthetic Direction
[The "feel" of the system. What two or three design traditions does it fuse?
What is it NOT? When is it appropriate to use?]

## Typography
[Full import block. Per-font: every role, every exact CSS value per role.
Include font-variation-settings axes verbatim. Include the decision logic
for which font to use when.]

## Color System
[Full :root token block as a CSS code block. Full theme-override block.
Prose explanation of semantic groupings. Color usage rules.]

## Background & Atmosphere
[Every atmospheric technique with full CSS code blocks.
Z-index layer diagram in text. Light theme overrides.]

## Layout
[Page wrapper. Every structural region with full CSS.
Asymmetric column ratios. Border-as-structure patterns.]

## [Each major component — one H2 per component]
[Full CSS for every state. HTML structure example. JS behavior if applicable.]

## Design Rules — Do & Don't
[Explicit list of what defines this system vs. what violates it.
This is the most important section for an AI reading the skill —
it prevents drift toward generic defaults.]

## Composing a New Application in This System
[Page structure HTML scaffold. Component adaptation notes for data tables,
buttons, forms, code blocks, badges, progress meters, etc.]
```

---

## Step 3 — Output

Write the complete SKILL.md to `/mnt/user-data/outputs/frontend-design-SKILL.md`.

Then call `present_files` with that path so the user can download it.

Confirm completion with a brief summary of what was captured:
- Font stack (names)
- Primary accent color
- Theme system (dark/light/single)
- Number of components documented
- Key signature patterns identified

---

## Quality Checklist

Before writing the output file, verify:

- [ ] Every CSS `--variable` from `:root` is in the output
- [ ] Every `font-variation-settings` combination is documented
- [ ] Atmospheric pseudo-elements (`::before`, `::after`) are fully reproduced
- [ ] All `@keyframes` are reproduced verbatim
- [ ] All `transition` values per component are included
- [ ] All `@media` breakpoints are covered
- [ ] All JS behaviors are documented
- [ ] The Do/Don't section explicitly names what makes this design distinctive
- [ ] The HTML scaffold in "Composing a New Application" is complete enough to start from
- [ ] No value is described as "approximately" or "roughly" — exact values only
- [ ] The output SKILL.md could stand alone: no reference to "the original file" anywhere in its prose

---

## Common Failure Modes — Avoid These

**Incomplete CSS extraction**: Stopping after reading only the first chunk of a large
file. Always read the entire file.

**Vague color descriptions**: Writing "a dark navy background" instead of `#0b0f18`.
Always use exact hex/rgba values.

**Missing variable axes**: Writing `font-family: 'Fraunces', serif` without documenting
the `font-variation-settings` is incomplete for variable fonts. Extract every distinct
axis combination.

**Skipping atmospheric layers**: The `body::before` scanline overlay and `body::after`
ambient glow are often what makes a design feel distinctive. Never skip pseudo-elements.

**Generic Do/Don't**: Writing "use good typography" is useless. Write the specific
constraints: "Never use border-radius > 4px", "All metadata labels must use JetBrains
Mono uppercase", "Teal accent must always carry a text-shadow glow".

**Missing component states**: Document hover, focus, open/active, and disabled states
for every interactive component — not just the resting state.

**Omitting the HTML scaffold**: The output skill must include a full composable HTML
page template so an AI can start building immediately without inferring structure.
