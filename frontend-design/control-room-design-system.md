---
name: control-room
description: >
  Dark, monospace-typographic frontend design system for single-file, local-first
  tools. Built around a deep ink background, a single warm signal-orange accent
  (used for the playhead, focus, and active state only), and a 3-font stack
  where Instrument Serif italic carries every "title" moment, Inter handles
  body, and JetBrains Mono is reserved for data. Signature device: a thin
  horizontal "ribbon" used as a structural timeline (playlist progress, plan
  progress, anything ordered). Use this skill for local players, dashboards,
  developer tools, read-it-later apps, single-file HTML utilities, and any
  interface where a single-user, keyboard-driven, no-account experience needs
  to feel considered rather than generated. Skip for marketing sites, social
  apps, multi-tenant SaaS, or anything that wants to feel friendly by default.
---

# Control Room — Design System

A frontend system for small, keyboard-driven, single-file tools. Dark by default. Almost no color. Mono as a structural device. The signature is the **ribbon** — a thin horizontal line that turns any ordered thing (playlist, plan, queue, set of steps) into a structural device the page is built around.

## Concept & Aesthetic Direction

The system fuses two traditions:

1. **Studio / control-room reference points** — small, dark, single-user UIs where the work is in front of you and everything around it is muted. Think audio mastering plug-ins, broadcast switchers, code editors in low-light mode.
2. **Editorial typesetting** — display serif italic used with restraint for the one thing that matters (the now-playing filename, the headline). Mono everywhere data appears, because mono says "this is a number, not a sentence."

It is **not** the AI default of dark + purple gradient + glassmorphism. There are no gradients, no glows, no drop-shadows used for atmosphere, no backdrop-blur cards, no glass. Color is a single saturated accent used four times in a layout, never as a fill.

When to use: local-first tools, single-file apps, dashboards where a single user does a focused task. When *not* to use: anything multi-tenant, anything that needs to feel warm/approachable on first contact, anything where the "delight" comes from motion rather than restraint.

## Typography

Three faces, all from Google Fonts CDN. Each has a job. Do not reassign roles — the system breaks if Inter does the work of the display face, or if mono is used for prose.

**Import (single block, use verbatim):**

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
```

**Roles:**

| Role           | Family              | Use it for                                                  |
| -------------- | ------------------- | ----------------------------------------------------------- |
| Display        | Instrument Serif, italic | The one large type per page: the now-playing filename, the page headline, a section label. Set italic. |
| Body / UI      | Inter               | Buttons, controls, paragraphs, list items, labels.          |
| Mono (data)    | JetBrains Mono       | Timecodes, FPS, file sizes, indices, keyboard keys, eyebrows, the topbar clock, counters, any number. |

**Type scale (use these exact tokens):**

| Token          | Size | Used for                                                    |
| -------------- | ---- | ----------------------------------------------------------- |
| `--type-xs`    | 11px | Eyebrows, mono labels, kbd caps, count, dot text.          |
| `--type-sm`    | 12px | Small meta, mono body bits.                                 |
| `--type-md`    | 13px | Default body / UI text.                                     |
| `--type-lg`    | 14px | Slightly emphasized body, lead text, question copy.        |
| `--type-xl`    | 16px | Lead body, empty-state titles, key captions.                |
| `--type-2xl`   | 20px | Section labels, brand name, button-lede type.              |
| `--type-3xl`   | 28px | Empty/hero moments (drop overlay title).                    |
| `--type-display` | 44px | The now-playing filename. The single largest type on the page. |
| `--type-hero`  | 64px | Long-form doc hero title (only on dedicated doc pages).     |

**Type rules:**

- The display face is always italic when set at `--type-display` or `--type-hero` / `--type-2xl` for section labels. It is *never* set upright except inside code blocks.
- Mono is sentence-case only when it's a label. When it's a value (timecode, count, size, index), it uses whatever casing the data has — `00:42`, `1920×1080`, `2.4 MB`.
- Letter-spacing on uppercase mono labels: `0.10em` to `0.16em`. Anything tighter reads as body text.
- `text-transform: uppercase` is reserved for mono labels and eyebrows. Never uppercase Inter.
- The display face appears **once per viewport at large size**, plus a few `--type-2xl` section labels. Do not let it become ambient.

## Color System

Five semantic roles, plus a soft variant of the signal. Total: 6 tokens. There is no second accent. There are no gradients.

**Full `:root` block (use verbatim):**

```css
:root {
    --ink: #0E0E10;
    --surface: #16161A;
    --elevated: #1F1F25;
    --line: #2A2A31;
    --paper: #E8E4D9;
    --paper-dim: #A8A39A;
    --muted: #6B6B73;
    --signal: #D97757;
    --signal-soft: rgba(217, 119, 87, 0.14);
}
```

**Semantic mapping:**

| Token          | Hex / rgba             | Role                                                      |
| -------------- | ---------------------- | --------------------------------------------------------- |
| `--ink`        | `#0E0E10`              | Page background. The base layer.                          |
| `--surface`    | `#16161A`              | Cards, panels, queue head, callouts, phase blocks.        |
| `--elevated`   | `#1F1F25`              | Inputs, kbd caps, hover row, anything that "sits above" surface. |
| `--line`       | `#2A2A31`              | Hairline rules, dividers, borders, separators.            |
| `--paper`      | `#E8E4D9`              | Primary text — warm cream, not pure white. The now-playing filename uses this. |
| `--paper-dim`  | `#A8A39A`              | Secondary text, body copy, list items.                    |
| `--muted`      | `#6B6B73`              | Tertiary text — eyebrows, count, timecode-done, kbd labels. |
| `--signal`     | `#D97757`              | The single accent. Used for: the playhead, the active row's left border, the focus ring, the "current" digit in a timecode, the recommended-cut marker, the dot in the topbar, the brand mark. |
| `--signal-soft` | `rgba(217,119,87,0.14)` | Active row background, recommended-cut segment fill, anything that needs a wash of the signal. |

**Color rules (do not break):**

- The signal appears in **at most four places per viewport**: a dot, a left border, a focus ring, and a single text element (a current time, a recommended tag, a count).
- `--paper` is the only color used for *primary* body. Never use `--paper-dim` for the now-playing filename or any "headline" moment — it reads as a placeholder.
- The signal is **never** used as a fill on a button. It is a border, a text color, a 1px line, a 6px dot — never a chunky block.
- No drop-shadows. No `box-shadow` for "elevation" — borders (`1px solid var(--line)`) carry that job.
- No gradients. The two existing gradient instances in the system are *text-clipping* gradients on the empty-state's `empty-title` and the drop-overlay's `drop-title` — and even those should be replaced with solid `--paper` italic in production. If you find yourself reaching for `linear-gradient`, you've left the system.
- `--signal-soft` over `--ink` reads darker than `--signal-soft` over `--surface` — pick the base deliberately.

## Background & Atmosphere

There is no atmosphere. The page background is `--ink`, full stop. No pseudo-element overlays, no grain, no grid. The discipline is the atmosphere.

**Body base:**

```css
html, body {
    background: var(--ink);
    color: var(--paper);
    font-family: var(--font-body);
    font-size: var(--type-md);
    line-height: 1.5;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
```

**Z-index stacking order** (when you do need one):

1. Page content (`z-index: auto`)
2. Action popups inside the video wrapper (`z-index: 10`)
3. In-player overlays (`z-index: 11`)
4. Drop overlay (`z-index: 100`)

No layer above 100. There is no modal in this system. If you need one, you've left the system.

## Layout

The system is single-page-app-shaped. Two structural patterns are available: **stage-and-queue** (player-style: a primary content region + a side panel) and **document** (long-form prose + sidebar or in-line cards).

**Page wrapper:**

```css
body { padding: 28px 32px 40px; }
.container { max-width: 1400px; margin: 0 auto; }     /* player */
.container { max-width: 980px;  margin: 0 auto; }     /* document */
```

Pick the max-width to the genre: 1400px for tools, 980px for documents. Never 1200px (it's a default), never 100% (it loses the framing).

**Top bar** (used on every page in this system):

```css
.topbar {
    display: flex;
    align-items: baseline;
    justify-content: space-between;
    padding-bottom: 20px;
    border-bottom: 1px solid var(--line);
    margin-bottom: 24px;     /* 36px on document pages */
}
```

The topbar is a **structural rule**, not a navigation. It carries: brand mark (signal mono), brand name (italic display), brand sub (muted mono uppercase), and 1–2 right-side meta items (mono, uppercase, tracking 0.10em). The first meta item often starts with a `dot` — a 6px signal circle.

**Stage-and-queue layout (player):**

```css
.player-layout {
    display: grid;
    grid-template-columns: 1fr 380px;
    gap: 24px;
    align-items: start;
}
```

The right column (380px) is **sticky**:

```css
.queue-section {
    position: sticky;
    top: 28px;
    max-height: calc(100vh - 100px);
}
```

**Document layout** uses a single 980px column with section blocks separated by `margin-top: 64px`, each section starting with a `.section-label` (mono num + italic display label) above a hairline.

**Border-as-structure.** Use `1px solid var(--line)` to separate regions. Never use a 4–8px gap with no rule. The line *is* the structure. Padding inside a region is `16–22px`; padding between regions is provided by the line itself, not by gap.

## The Ribbon — Signature Component

The single memorable element. A 2px-tall horizontal track that represents any ordered thing. Used as a queue-progress strip, a plan-progress track, or any "where am I in this sequence" indicator. Below the ribbon: a fill (the played/visited portion) and a playhead (the current position).

**Default ribbon (player queue):**

```css
.timeline-ribbon {
    position: relative;
    height: 2px;
    background: var(--elevated);
    border-radius: 1px;
    overflow: hidden;
}
.timeline-ribbon-fill {
    position: absolute; top: 0; left: 0; height: 100%;
    background: var(--signal);
    width: 0%;
    transition: width 0.4s ease;
}
.timeline-ribbon-playhead {
    position: absolute; top: -2px; left: 0;
    width: 1px; height: 6px;
    background: var(--signal);
    transition: left 0.4s ease;
}
```

**Segmented ribbon (plan / sequence of discrete items):**

```css
.plan-ribbon-track {
    position: relative;
    display: flex;
    height: 24px;
    border: 1px solid var(--line);
    border-radius: var(--r-sm);
    overflow: hidden;
    background: var(--surface);
}
.plan-ribbon-seg {
    flex: 1;
    position: relative;
    border-right: 1px solid var(--ink);
}
.plan-ribbon-seg:last-child { border-right: none; }
.plan-ribbon-seg.is-cut { background: var(--signal-soft); }
.plan-ribbon-seg.is-cut .seg-num { color: var(--signal); }
```

**Rules:**

- The ribbon is always 2px tall for a continuous progress, 24px tall for a segmented (one-cell-per-item) view.
- The fill and the playhead share the same easing. Use 0.4s `ease` for both.
- The ribbon is the *first* thing in its parent container, never the last. It sets up the region.
- A ribbon can be the entire reason a region exists. If a section doesn't have a ribbon, the section needs a different reason to exist (a section-label, a callout, a hero).

## The Hero Strip — "Now Playing" Pattern

A horizontal band that lives between the topbar and the primary content. Two columns: a name/title on the left (display italic at `--type-display`), a live numeric read-out on the right (mono). This is where the *most important thing on the page* lives.

```css
.now-playing {
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 16px;
    align-items: end;
    padding: 18px 4px 22px;
    border-bottom: 1px solid var(--line);
    margin-bottom: 18px;
}
.now-playing-eyebrow {
    font-family: var(--font-mono);
    font-size: var(--type-xs);
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.14em;
    margin-bottom: 8px;
}
.now-playing-title {
    font-family: var(--font-display);
    font-style: italic;
    font-size: var(--type-display);
    line-height: 1.05;
    color: var(--paper);
    letter-spacing: -0.01em;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
.now-playing-time {
    font-family: var(--font-mono);
    font-size: var(--type-md);
    color: var(--paper-dim);
    text-align: right;
    white-space: nowrap;
}
.now-playing-time .current { color: var(--signal); }
```

**Rules:**

- The title element gets the `.empty` modifier when nothing is selected — `color: var(--muted)`, italic kept.
- The live read-out on the right uses one "current" element in `--signal` and the rest in `--paper-dim`. One signal moment, per region.
- Never center-align the hero strip. Always grid 1fr / auto, baseline-aligned.

## Buttons & Controls

Outline-only buttons. Never filled. The fill-state reserved for is-active is `--signal-soft` over `--ink`, with a `--signal` border and `--signal` text.

**Base control:**

```css
.control-btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 8px 14px;
    border: 1px solid var(--line);
    border-radius: var(--r-sm);
    background: transparent;
    color: var(--paper);
    font-family: var(--font-body);
    font-size: var(--type-md);
    cursor: pointer;
    transition: background 0.15s ease, border-color 0.15s ease, color 0.15s ease;
}
.control-btn:hover:not(:disabled) {
    background: var(--elevated);
    border-color: var(--paper-dim);
}
.control-btn:focus-visible {
    outline: 2px solid var(--signal);
    outline-offset: 2px;
}
.control-btn:disabled { opacity: 0.35; cursor: not-allowed; }
.control-btn.is-active {
    background: var(--signal-soft);
    border-color: var(--signal);
    color: var(--signal);
}
```

**Keyboard hint inside a button (`.kbd`):**

```css
.control-btn .kbd {
    font-family: var(--font-mono);
    font-size: var(--type-xs);
    color: var(--muted);
    padding: 2px 5px;
    border: 1px solid var(--line);
    border-radius: 3px;
}
```

Use `⌃` for Ctrl, `⇧` for Shift, `⌥` for Alt, `→ ← ↑ ↓` for arrows. Don't spell out "Ctrl" inside a button — there's no room.

## Inputs

Single text-input style for everything (search, filter, name field). 1px line border, transparent-ish bg, mono font, signal focus.

```css
.search-box input {
    width: 100%;
    padding: 7px 10px;
    border: 1px solid var(--line);
    border-radius: var(--r-sm);
    background: var(--ink);
    color: var(--paper);
    font-family: var(--font-body);
    font-size: var(--type-md);
    outline: none;
    transition: border-color 0.15s ease;
}
.search-box input::placeholder { color: var(--muted); }
.search-box input:focus { border-color: var(--signal); }
```

## Range Slider (volume / scrubber)

WebKit and Moz separately. The track is `--line`, 2px tall, 1px radius. The thumb is `--signal`, 10px circle, no border. No fill state on the track — the signal lives in the thumb.

```css
.volume-slider {
    -webkit-appearance: none;
    appearance: none;
    width: 90px;
    height: 2px;
    background: var(--line);
    border-radius: 1px;
    outline: none;
}
.volume-slider::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 10px; height: 10px;
    border-radius: 50%;
    background: var(--signal);
    cursor: pointer;
    border: none;
}
.volume-slider::-moz-range-thumb {
    width: 10px; height: 10px;
    border-radius: 50%;
    background: var(--signal);
    cursor: pointer;
    border: none;
}
```

## List Items (queue / rows)

A 32-px mono index column, a 1fr body, a small right-side kind marker. The active row gets a `--signal-soft` background and a 2px left border in `--signal`. Hover is `--elevated`, no border change. The transition is 0.12s — faster than buttons, because rows are clicked more often.

```css
.queue-item {
    display: grid;
    grid-template-columns: 32px 1fr auto;
    align-items: center;
    gap: 10px;
    padding: 10px 18px;
    cursor: pointer;
    border-left: 2px solid transparent;
    transition: background 0.12s ease, border-color 0.12s ease;
}
.queue-item:hover { background: var(--elevated); }
.queue-item.is-active {
    background: var(--signal-soft);
    border-left-color: var(--signal);
}
.queue-item-index {
    font-family: var(--font-mono);
    font-size: var(--type-xs);
    color: var(--muted);
    text-align: right;
}
.queue-item.is-active .queue-item-index { color: var(--signal); }
.queue-item-title {
    font-size: var(--type-md);
    color: var(--paper);
    white-space: nowrap; overflow: hidden; text-overflow: ellipsis;
}
.queue-item.is-active .queue-item-title { color: var(--paper); font-weight: 500; }
```

The `.queue-item-meta` (file size, etc.) is mono, `--muted`, uppercase, letter-spacing `0.08em`. The right-side `.queue-item-kind` (`V` / `A`) is mono, `--muted`, uppercase, letter-spacing `0.10em`, and flips to `--signal` when active.

## Cards (callouts, phases, questions)

Generic card. The `border-left: 2px solid var(--signal)` is reserved for *recommended* / *primary* / *this-is-the-one* cards. A normal card has only the 1px `--line` border.

```css
.callout {
    padding: 28px 28px 26px;
    background: var(--surface);
    border: 1px solid var(--line);
    border-left: 2px solid var(--signal);
    border-radius: var(--r-md);
}
```

Card labels combine a mono `num` (signal, uppercase) with a display `label` (italic, `--type-2xl`, paper):

```css
.callout-label { display: flex; align-items: baseline; gap: 12px; margin-bottom: 16px; }
.callout-label .num {
    font-family: var(--font-mono);
    font-size: var(--type-xs);
    color: var(--signal);
    text-transform: uppercase;
    letter-spacing: 0.14em;
}
.callout-label .label {
    font-family: var(--font-display);
    font-style: italic;
    font-size: var(--type-2xl);
    color: var(--paper);
}
```

## Phase / Section Blocks (accordion)

Used in long-form docs. Head row is a grid of `[56px num] [1fr title] [auto tag] [auto toggle]`. Click to expand. The `+` toggle rotates 45° to `×` and color-flips to `--signal` when open. Body has `max-height: 0` collapse with `0.3s ease`.

```css
.phase-head {
    display: grid;
    grid-template-columns: 56px 1fr auto;
    align-items: center;
    gap: 18px;
    padding: 18px 20px;
    cursor: pointer;
    user-select: none;
}
.phase-head:hover { background: var(--elevated); }
.phase-toggle { transition: transform 0.2s ease; }
.phase.is-open .phase-toggle { transform: rotate(45deg); color: var(--signal); }
.phase-body { max-height: 0; overflow: hidden; transition: max-height 0.3s ease; }
.phase.is-open .phase-body { max-height: 1000px; }
```

**Tag pill (`.phase-tag`):** mono, `--muted`, 1px line border, 3px×8px padding, `r-sm`. On `data-cut="true"` it becomes signal-orange with a signal border.

## Code Inline

```css
.phase-body li code, .callout-list .cut-body code {
    font-family: var(--font-mono);
    font-size: var(--type-sm);
    color: var(--paper);
    background: var(--ink);
    padding: 1px 5px;
    border-radius: 3px;
    border: 1px solid var(--line);
}
```

Always on `--ink` (the page bg), never on `--surface` — it makes the code feel "embedded in the page" rather than "in the card."

## Action Popup (in-player notification)

A small mono pill that floats above the video. Used to confirm a keyboard action ("Paused", "Forward 6s", `Speed 1.25x`).

```css
.action-popup {
    position: absolute;
    left: 50%; bottom: 20px;
    transform: translateX(-50%) translateY(8px);
    background: rgba(14, 14, 16, 0.92);
    color: var(--paper);
    padding: 8px 14px;
    border-radius: var(--r-sm);
    border: 1px solid var(--line);
    font-family: var(--font-mono);
    font-size: var(--type-sm);
    backdrop-filter: blur(8px);
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.18s ease, transform 0.18s ease;
    z-index: 10;
    white-space: pre-line;
    line-height: 1.5;
}
.action-popup.visible {
    opacity: 1;
    transform: translateX(-50%) translateY(0);
}
```

`white-space: pre-line` is used so multi-line properties (`P`) display naturally. Default duration: 1400ms. Multi-line: 2400ms.

## Drop Overlay

Full-screen overlay shown during drag-and-drop. `--ink` background at 0.85 alpha, with a 1px dashed `--signal` border around a centered content block.

```css
.drop-overlay {
    position: fixed; inset: 0;
    background: rgba(14, 14, 16, 0.85);
    backdrop-filter: blur(4px);
    display: flex; align-items: center; justify-content: center;
    z-index: 100;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.15s ease;
}
.drop-overlay.is-active { opacity: 1; pointer-events: all; }
.drop-overlay-inner {
    border: 1px dashed var(--signal);
    border-radius: var(--r-lg);
    padding: 60px 80px;
    text-align: center;
}
.drop-overlay-inner .drop-title {
    font-family: var(--font-display);
    font-style: italic;
    font-size: var(--type-3xl);
    margin-bottom: 8px;
}
.drop-overlay-inner .drop-sub {
    font-family: var(--font-mono);
    font-size: var(--type-sm);
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.1em;
}
```

## Empty States

The system has one empty-state shape: centered text, a title in italic display (`--type-xl`, `--paper-dim`), a body line, and an optional `<kbd>` hint. Never a sad illustration, never an icon.

```css
.empty-state { text-align: center; padding: 48px 20px; color: var(--muted); }
.empty-state .empty-title {
    font-family: var(--font-display);
    font-style: italic;
    font-size: var(--type-xl);
    color: var(--paper-dim);
    margin-bottom: 8px;
}
.empty-state p { font-size: var(--type-md); line-height: 1.6; }
.empty-state kbd {
    display: inline-block;
    padding: 2px 6px;
    border: 1px solid var(--line);
    border-radius: 3px;
    background: var(--ink);
    font-family: var(--font-mono);
    font-size: var(--type-xs);
    color: var(--paper);
    margin: 0 2px;
}
```

## Scrollbars (WebKit only — degrade silently elsewhere)

```css
.queue-list::-webkit-scrollbar { width: 6px; }
.queue-list::-webkit-scrollbar-track { background: transparent; }
.queue-list::-webkit-scrollbar-thumb { background: var(--line); border-radius: 3px; }
.queue-list::-webkit-scrollbar-thumb:hover { background: var(--elevated); }
```

Thin, signal-adjacent (line, not signal). The thumb shifts to `--elevated` on hover, not to `--signal`. Hover should be quiet.

## Design Rules — Do & Don't

**Do**

- Use the display face **once** at large size per viewport. The player page uses it for the now-playing filename; the doc page uses it for the hero headline. Pick one.
- Use mono for any number, any index, any timecode, any shortcut, any kbd, any count, any size.
- Use the signal accent four times max per viewport: a dot, a left border, a focus ring, a single text element.
- Treat the ribbon as the **first** element in any region that has one. It sets up the region.
- Use `border-left: 2px solid var(--signal)` to mean *this is the one*.
- Use sentence case in body copy, sentence case in buttons ("Add files", "Next", "Play / pause").
- Use mono uppercase with `letter-spacing: 0.10–0.16em` for any meta/eyebrow/count text.

**Don't**

- Don't use gradients. Anywhere. The system is not interested in them.
- Don't use box-shadow for elevation. Borders carry that.
- Don't use a second accent. There is `--signal`, and there is everything else.
- Don't use Inter for the page's "title" moment. That's the display face's job.
- Don't uppercase Inter. Mono uppercase is the only uppercase in the system.
- Don't use `border-radius > 12px`. The tokens are `--r-sm: 4px`, `--r-md: 8px`, `--r-lg: 12px`. Stay in those.
- Don't use a sans-serif fallback for the display face — fall back to `Georgia, serif`, not `serif` alone, so the italic weight looks deliberate.
- Don't add a "light theme" override. The system is dark. If you need light, you've left the system.
- Don't add emoji to UI. The one exception: a single `▶` for the brand mark.
- Don't add icons. Symbols are mono glyphs (kbd, ⇧, ⌃, ✕, ▶) or nothing.

## Composing a New Application in This System

**HTML scaffold (player-style):**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>App Name</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
    <style>
        :root {
            --ink: #0E0E10; --surface: #16161A; --elevated: #1F1F25;
            --line: #2A2A31; --paper: #E8E4D9; --paper-dim: #A8A39A;
            --muted: #6B6B73; --signal: #D97757;
            --signal-soft: rgba(217, 119, 87, 0.14);
            --type-xs: 11px; --type-sm: 12px; --type-md: 13px; --type-lg: 14px;
            --type-xl: 16px; --type-2xl: 20px; --type-3xl: 28px; --type-display: 44px;
            --font-display: 'Instrument Serif', Georgia, serif;
            --font-body: 'Inter', system-ui, -apple-system, sans-serif;
            --font-mono: 'JetBrains Mono', 'SF Mono', Menlo, monospace;
            --r-sm: 4px; --r-md: 8px; --r-lg: 12px;
        }
        /* ... rest of the CSS from the system ... */
    </style>
</head>
<body>
    <div class="container">
        <div class="topbar">
            <div class="brand">
                <span class="brand-mark">▶</span>
                <span class="brand-name">App Name</span>
                <span class="brand-sub">Subtitle · Mono</span>
            </div>
            <div class="topbar-meta">
                <span><span class="dot"></span>State</span>
                <span>Meta</span>
            </div>
        </div>

        <div class="player-layout">
            <section class="player-section">
                <div class="now-playing">
                    <div>
                        <div class="now-playing-eyebrow">Now doing</div>
                        <div class="now-playing-title empty">Nothing selected</div>
                    </div>
                    <div class="now-playing-time">
                        <span class="current">00:00</span> / 00:00
                    </div>
                </div>
                <!-- primary content area -->
                <div class="controls-bar">
                    <button class="control-btn">Action</button>
                </div>
            </section>

            <aside class="queue-section">
                <div class="queue-head">
                    <div class="timeline-ribbon">
                        <div class="timeline-ribbon-fill"></div>
                        <div class="timeline-ribbon-playhead"></div>
                    </div>
                    <div class="queue-head-row">
                        <div class="queue-title">Region</div>
                        <div class="queue-count">0 items</div>
                    </div>
                </div>
                <div class="queue-list">
                    <!-- list items -->
                </div>
            </aside>
        </div>
    </div>
</body>
</html>
```

**HTML scaffold (document-style):** drop the topbar meta on the right, replace `player-layout` with a single `.container` at `max-width: 980px`, and use `.section-label` + `.callout` + `.questions` blocks as the building units.

**Adaptation notes for common patterns:**

- **Data tables** — header row in mono uppercase, body in Inter, borders in `--line`. No row hover, no zebra striping. If a row is "current," apply the same treatment as a queue item (`is-active` class with `--signal-soft` bg and 2px left border).
- **Modals** — there are none in this system. If you need confirmation, use an inline expanding region under the button that triggered it, signal-bordered.
- **Tooltips** — use the action-popup pattern: small mono pill, fixed-position, fade.
- **Status badges** — mono uppercase, 3px×8px padding, 1px line border, `--muted` text. If the status is "the important one," use signal text + signal border.
- **Progress bars** — use the ribbon. 2px tall, `--elevated` track, `--signal` fill, no label. If you need a label, put it in mono above the ribbon.
- **Form fields** — same shape as `.search-box input`. Signal focus border. No floating labels, no helper text under the field — put helper text in mono `--muted` *above* the field as a 13px label.
- **Tabs** — underline tabs in `--line`; active tab has a 1px bottom border in `--signal`. Mono uppercase for labels.
- **Notifications / toasts** — same shape as the action popup. No slide-in from the corner.

## JavaScript Behavior

**Theme switching** — there is none. The system is dark.

**Keyboard handling** — always use a single document-level `keydown` listener, ignore keys when `e.target.tagName` is `INPUT` or `TEXTAREA`, and call `e.preventDefault()` *inside* each case so the default behavior only stops for known keys. Always use `e.key` (not `e.keyCode`).

**Object URL lifecycle** — when adding files via `URL.createObjectURL`, track the URLs so they can be revoked on remove or library clear. This is the only "leak" the system has ever had; mention it when extending.

**Time formatting** — `mm:ss` for under an hour, `h:mm:ss` otherwise. Always `padStart(2, '0')` for both minutes and seconds. Use the same `formatTimecode(seconds)` helper everywhere.

**Bytes formatting** — KB below 1 MB, MB below 1 GB, GB above. One decimal for MB, two for GB, zero for KB. Same `formatBytes(bytes)` helper.

**Playback rate** — clamp to `[0.25, 4.0]`, step `0.25`. Display as `${rate.toFixed(2)}x` after stripping trailing zero.

**File size and metadata for media** — the action popup is the only metadata surface. Use `white-space: pre-line` and `\n` to break it into 2–3 lines. Two-line pops get 1400–1800ms; three-line (with FPS) gets 2400ms.

**Drop overlay** — count `dragenter`/`dragleave` with a depth counter so a child element leaving doesn't dismiss the overlay.

## Responsive

Two breakpoints only.

**Tablet (max-width: 1024px):** collapse the stage-and-queue grid to a single column. The right column becomes `position: static` with `max-height: 480px`.

**Mobile (max-width: 640px):** body padding shrinks to `16px`. Topbar stacks vertically. `--type-display` shrinks to `32px`. Phase-head and question grids simplify (column drops for the right-side meta).

```css
@media (max-width: 1024px) {
    .player-layout { grid-template-columns: 1fr; }
    .queue-section { position: static; max-height: 480px; }
}
@media (max-width: 640px) {
    body { padding: 16px; }
    .topbar { flex-direction: column; gap: 8px; align-items: flex-start; }
    .now-playing-title { font-size: 32px; }
}
```

There is no third breakpoint. The system does not design for 360px viewports as a primary target.

## Reduced Motion

```css
@media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
        transition-duration: 0.01ms !important;
        animation-duration: 0.01ms !important;
    }
}
```

Set this on every page in the system. No exceptions.

## Accessibility

- The signal is the only "active" indicator. It must be paired with another signal — `font-weight: 500` on the active title, a 2px left border, and the bg wash — so colorblind users have two non-color cues.
- Focus rings are 2px `--signal` with 2px offset, not removed.
- Buttons have explicit `disabled` opacity (0.35), not "pointer-events: none" alone.
- Timecode updates (`aria-live="polite"`) on the action popup.
- Form inputs and kbd hints get a `min-width` to prevent layout shift.
- The drop overlay traps `aria-hidden="true"` on the underlying content while active (toggle this in JS).
