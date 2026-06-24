# Frontend Design — Editorial Craft System

> An editorial print aesthetic for the browser. Warm parchment, ink-on-paper typography, rust-red accents, and zero glassmorphism. Designed to be loaded as a skill into AI coding assistants (Claude Code, opencode, etc.) so that plain HTML pages can be restyled into field-manual-grade interfaces with a single prompt.

---

## What this skill produces

Given any ordinary HTML file, the skill rewrites the design system to match the editorial craft aesthetic below:

- **Warm parchment background** (`#f0e7d2`) layered with a 40px blueprint grid and a fixed SVG noise-grain overlay.
- **Newspaper-style masthead** with a 3-column grid, double-rule top border, and `JetBrains Mono` uppercase metadata.
- **Asymmetric hero** with a `Fraunces` display headline on the left and a rust-bordered italic lede on the right.
- **Meta bar** of `Fraunces` italic numerals in uppercase mono cells, divided by `1px solid var(--rule-soft)`.
- **Lifted-paper cards** — zero `border-radius`, a `::before` shadow-offset pseudo-element that makes the card look like a sheet of paper sitting on top of another.
- **Ruled phase dividers** (`4px double var(--ink)`), rust italic `em` words inside `Fraunces` headings (with `SOFT` and `WONK` variable axes set to their maximum).
- **Forest-green answer blocks** with a mustard left border, and **dark-brown code blocks** with rust-soft syntax highlighting.
- **Persistent light/dark theme toggle** (◐ button, top-right) with a 0.4s ease background transition and `localStorage` persistence.

The look is closer to a 1970s technical journal than a 2025 SaaS dashboard. No gradients. No frosted blur. No `Inter`.

---

## Using the skill with an AI coding assistant

The skill lives at [`frontend-design/skill.md`](frontend-design/skill.md). The recommended workflow:

1. **Load the skill into your assistant.** Most agents that support a `skill` tool will pick up `frontend-design/skill.md` automatically. If yours doesn't, paste the entire file into the system prompt or context.
2. **Provide the HTML you want revamped.** Either as a file path the agent can read, or pasted inline.
3. **Write a short prompt.** The prompt is usually just: *"Update the following HTML using the frontend-design skill"* followed by the file.
4. **Review the output.** The skill is opinionated but not destructive — semantic content, copy, and code blocks are preserved. Only the design system changes.

That's the entire workflow. No CLI, no build step, no configuration. The skill is a single Markdown file that any sufficiently capable LLM can read and apply.

### Minimal prompt template

```text
Using the frontend-design skill at frontend-design/skill.md, update this HTML
file: <path-to-file.html>. Preserve all content, copy, and code blocks.
Only the design system (CSS + structure where needed) should change.
```

### Variant — paste the skill inline

If your agent doesn't auto-discover skill files, paste the skill body directly into the prompt and reference it:

```text
Here is the frontend-design skill to apply:
<paste entire contents of frontend-design/skill.md>

Now apply it to <path-to-file.html>.
```

---

## What the skill actually does

The skill is a 15-section design specification covering tokens, type, colour, texture, layout, components, navigation, animation, heading hierarchy, dividers, list styles, responsive behaviour, do/don't rules, document shell, and React adaptation notes. When the agent follows it, the output is:

| Area | Before (typical) | After (skill applied) |
|---|---|---|
| Background | Flat `#070b12` | Parchment `#f0e7d2` + 40px grid + SVG noise |
| Headings | `Syne` 800, white, gradient clip | `Fraunces` 360, ink black, rust italic `em` with `SOFT`/`WONK` axes |
| Body | `DM Mono` everywhere | `Geist` for body, `JetBrains Mono` for labels |
| Cards | `border-radius: 2px` + cyan accent stripe | `border-radius: 0` + `::before` shadow-offset + hover lift |
| Code blocks | Bordered slate | Dark brown `#2a1f12`, rust-soft left rule, mustard strings |
| Theme | None | ◐ toggle, light + dark via `[data-theme]`, 0.4s transition, `localStorage` |

The result is a single self-contained HTML file with no external assets except three Google Fonts (`Fraunces`, `Geist`, `JetBrains Mono`) and a tiny inline SVG noise filter. No CSS framework. No JavaScript framework. No build pipeline.

---

## Examples — same base HTML, two different models

The repo includes a worked example. Three files sit side-by-side in [`examples/BaseHtml-Revamped-with-DesignSkill/BaseUI-and-Revamped-Ui-Files/`](examples/BaseHtml-Revamped-with-DesignSkill/BaseUI-and-Revamped-Ui-Files/):

- **`base-html-file.html`** — the original. A "DevOps → AI DevOps Engineer Roadmap" page built with `Syne` + `DM Mono`, flat dark `#070b12` background, cyan/purple/green neon accents, `border-radius: 2px` cards, and gradient-clip text.
- **`Revamped_By-DeepseekV4-flash.html`** — the same content, restyled by the skill. Generated using **DeepSeek V4 Flash** via **NVIDIA NIM**.
- **`Revamped_by_Minimax-m3-free.html`** — the same content, restyled by the skill. Generated using **MiniMax-M3 Free** via **OpenCode Zen**.

The two revamped versions are consistent with `frontend-design/skill.md` end to end: same colour tokens, same type scale, same component patterns, same masthead/hero/meta-bar/phase-divider/step-card/footer-rule skeleton. They differ only in implementation micro-details (one is more heavily commented, the other is more compact), not in design intent. **Both are stable, responsive, and visually faithful to the skill.**

This is the proof that the skill works across model providers and route layers. Whether the model is a frontier-tier paid model or a free-tier model, the output converges on the same design system because the skill is precise enough to remove ambiguity.

---

## Repository structure

```
.
├── README.md                                  ← you are here
├── frontend-design/
│   └── skill.md                               ← the skill itself (load this into your agent)
└── examples/
    └── BaseHtml-Revamped-with-DesignSkill/
        ├── Prompts/
        │   └── first-RevampAttempt-prompt.md  ← the prompt that produced both revamps
        └── BaseUI-and-Revamped-Ui-Files/
            ├── base-html-file.html            ← original (pre-skill)
            ├── Revamped_By-DeepseekV4-flash.html
            └── Revamped_by_Minimax-m3-free.html
```

---

## Extending the skill

The skill is one file. Edit it freely:

- **New colour tokens** — add to `:root` and `[data-theme="dark"]` in section 3.
- **New components** — add a section between 6.x and renumber.
- **Different aesthetic direction** — the skill's load-bearing rules (zero `border-radius`, no blurred shadows, no glassmorphism, `Fraunces` + `Geist` + `JetBrains Mono` only) are the things that make it look the way it looks. Override them and you get a different design system.

If you fork the skill, keep the `em` rust-italic rule for headings — it's the most recognisable single fingerprint of the system, and dropping it makes the output generic.

---

## License

MIT. Use it, fork it, ship it.
