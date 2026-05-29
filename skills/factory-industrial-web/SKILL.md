---
name: "factory-industrial-web"
description: |-
  Creates web interfaces with an industrial-blueprint aesthetic: 

    light gray base with diagonal hairline stripe overlay, sharp 1px black borders with no rounded corners, oversized monogram tiles for identity blocks, all-caps section labels, solid black pill-free buttons, and a single pumpkin-orange accent (#F06D2D) reserved for toggles, primary highlights, and warning links. Typography is Inter for English and Noto Sans SC / PingFang SC for Chinese, sans-serif throughout, with tabular numerals on data. 

    Invoke whenever the user wants a settings page, account/preferences UI, admin panel, dashboard, landing page, marketing site, blog, portfolio, e-commerce page, configuration interface, status page, developer console, or any web surface — even if they don't name the style explicitly — when their reference shows engineering/blueprint vibes, brutalist sharp-edged cards on hatched paper, factory.ai-like layouts, or asks for an industrial, technical, schematic, brutalist, paper-engineering, or typewriter-but-modern look. 

    Use this skill any time the user describes a desired aesthetic with words like industrial, brutalist, blueprint, schematic, engineering, paper-craft, draftsman, factory, technical-document, hatched, striped, pin-stripe, anything-but-rounded, or asks to imitate UI screenshots that match the visual signature above.
---

# Factory Industrial Web Skill

## Overview

This skill produces web interfaces that feel like engineering drawings or industrial control panels rendered for the browser: hatched paper backgrounds, hairline borders, oversized identity tiles, all-caps section labels, and solid black call-to-action buttons. The aesthetic is prescriptive — every choice below is fixed. Don't ask the user to pick between options. If something is unclear from context, default to the value specified here.

The intent of these defaults is to keep the visual signature unmistakable across every page type. The same rules should produce a settings page, a marketing landing page, a dashboard, or an admin console — only the components change, never the language.

Signature characteristics:

- Light gray page background (`#EAEAEA`) overlaid with thin diagonal stripes — the hatched-paper backdrop is the single most recognizable trait
- Pure white surfaces (cards, panels) sit on top of the hatched background and define structure
- Hairline 1px black borders everywhere — cards, buttons, inputs, dividers — never thicker than 1px, never softer than `#111`
- Zero border-radius on structural elements (cards, buttons, inputs). Subtle radii (4px max) are allowed only on tiny chips like badges
- Pumpkin orange `#F06D2D` is the **only** non-neutral accent — used sparingly on toggles, primary highlights, "danger zone" link text, and a single optional floating action chip
- Solid black buttons (`#0A0A0A` background, white uppercase text) for primary actions
- Section labels in `ALL CAPS` with letter-spacing, paired with hairline horizontal rules
- Oversized "monogram" tiles where identity is shown — square gray block with 1-2 large characters centered
- Sans-serif body text (Inter for English, Noto Sans SC / PingFang SC for Chinese), tabular numerals on numeric content

## Tech Stack Decision

Before generating code, determine the project's tech stack from context:

1. **Check the codebase** for existing framework usage (React, Vue, Svelte, etc.).
2. **If a framework is found**, write components in that framework's style with CSS Modules for styling.
3. **If no framework is detected or the user is unsure**, default to **vanilla HTML + a single `<style>` block or CSS file**.
4. **Don't** use CSS-in-JS libraries (styled-components, emotion) unless the project already uses them.
5. **Don't** use inline styles for component styling.
6. For greenfield projects with no build tool, output a single self-contained HTML file. This makes the result easy to preview and share.

## Color System

Colors are CSS custom properties on `:root`. The palette is intentionally narrow — neutrals carry almost everything, orange is the spark.

| Token | Value | Usage |
|-------|-------|-------|
| `--bg-base` | `#EAEAEA` | Page background, before stripes are layered |
| `--bg-stripe` | `rgba(0, 0, 0, 0.04)` | The diagonal stripe ink color |
| `--bg-surface` | `#FFFFFF` | Cards, panels, modals — anything that floats on the hatched paper |
| `--bg-inset` | `#F4F4F4` | Inset blocks: monogram tiles, table headers, disabled fields |
| `--bg-button-primary` | `#0A0A0A` | Solid primary buttons |
| `--text-primary` | `#0A0A0A` | Body text, headings |
| `--text-secondary` | `#4A4A4A` | Field labels, captions |
| `--text-muted` | `#8A8A8A` | Placeholders, supporting metadata |
| `--text-on-dark` | `#FFFFFF` | Text on black buttons |
| `--accent` | `#F06D2D` | Pumpkin orange — toggles, "Edit" links, danger-zone text, focus rings |
| `--accent-hover` | `#D85B1F` | Slightly darker orange on hover |
| `--border-default` | `#111111` | All structural 1px borders |
| `--border-light` | `#E0E0E0` | Subtle inner separators in tables, list rows |
| `--danger-text` | `#D33A2C` | "DANGER ZONE" headers and destructive copy (slightly redder than accent) |

### CSS Implementation

```css
:root {
  --bg-base: #EAEAEA;
  --bg-stripe: rgba(0, 0, 0, 0.04);
  --bg-surface: #FFFFFF;
  --bg-inset: #F4F4F4;
  --bg-button-primary: #0A0A0A;
  --text-primary: #0A0A0A;
  --text-secondary: #4A4A4A;
  --text-muted: #8A8A8A;
  --text-on-dark: #FFFFFF;
  --accent: #F06D2D;
  --accent-hover: #D85B1F;
  --border-default: #111111;
  --border-light: #E0E0E0;
  --danger-text: #D33A2C;
}
```

### The Hatched Background

This is the signature element. Implement on `body` (or the main scroll container) so the stripes scroll with content:

```css
body {
  background-color: var(--bg-base);
  background-image: repeating-linear-gradient(
    135deg,
    var(--bg-stripe) 0,
    var(--bg-stripe) 1px,
    transparent 1px,
    transparent 7px
  );
}
```

Why these numbers: 135deg gives the classic technical-drawing diagonal; 1px stripe + 7px gap reads as "hatched paper" rather than as a busy texture. Going below a 6px gap turns it into a moiré; going above 9px reads as polka-dotted lines.

White surfaces sit on top — every card, panel, table, and modal has `background: var(--bg-surface)` so it cleanly punches through the hatching. **Don't** apply the stripes to surfaces themselves; the contrast between hatched ground and clean white is the whole effect.

## Typography

```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Noto+Sans+SC:wght@400;500;600;700&display=swap');

:root {
  --font-sans: 'Inter', 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', 'SF Mono', ui-monospace, 'Cascadia Code', Consolas, monospace;
}

body {
  font-family: var(--font-sans);
  font-feature-settings: 'cv11', 'ss01', 'ss03';
  -webkit-font-smoothing: antialiased;
}

/* Tabular numerals for any numeric content (stats, tables, prices, IDs) */
.num, table, .stat-value, [data-numeric] {
  font-variant-numeric: tabular-nums;
}
```

| Element | Font | Size | Weight | Letter-spacing | Transform |
|---------|------|------|--------|----------------|-----------|
| Page title (h1) | sans | 28px | 600 | -0.01em | none |
| Section heading (h2) | sans | 11px | 600 | 0.08em | uppercase |
| Card title (h3) | sans | 14px | 600 | 0 | none |
| Body text | sans | 14px | 400 | 0 | none |
| Field label | sans | 12px | 500 | 0 | none |
| Caption / helper | sans | 12px | 400 | 0 | none |
| Monogram glyph | sans | 64px | 600 | -0.04em | none |
| Stat value | sans | 32px | 600 | -0.02em | none |
| Button text | sans | 11px | 600 | 0.08em | uppercase |
| Code / commands | mono | 13px | 400 | 0 | none |

**Rules of thumb:**
- Section labels (`YOUR ACCOUNT`, `SET UP YOUR CODEBASE`, `DANGER ZONE`) are always uppercase + letter-spaced. They belong on a row with a hairline rule extending across the rest of the card.
- Chinese text never gets `text-transform: uppercase` (it has no effect and can break shaping). Apply caps only when the run is Latin.
- Headings stay in `--text-primary`; only "DANGER ZONE" uses `--danger-text`.
- Don't bold body copy mid-sentence for emphasis. If something needs emphasis, wrap it in a chip or move it into a label row.

### Heading emphasis: the punctuation accent (preferred) vs. the highlight pill

When you need to draw attention to a phrase in a heading, the default move in this aesthetic is **not** a colored background block around the word. A full orange pill behind "ceramic" or "every Friday" pulls the visual weight *off* the typography and turns the hero into something that reads like a marketing banner — which is the opposite of the industrial-blueprint feel.

The preferred move is a small accent at the **end** of the phrase, like an architect's annotation mark on a drawing. The heading stays pure black, the typography carries the meaning, and the orange shows up as one decisive stroke:

```html
<h1 class="hero__title">
  Coffee, fired<br />
  like ceramics.<span class="accent-mark">/</span>
</h1>
```

```css
.accent-mark {
  color: var(--accent);
  display: inline-block;
  margin-left: 0.08em;
  font-weight: 800;          /* slightly heavier than the heading itself */
  font-style: italic;        /* a single italic glyph in an otherwise upright heading reads as "marked by hand" */
  transform: skewX(-8deg);   /* optional — adds tooling feel */
}
```

Variants for the accent mark (pick one per page; don't mix):
- `/` — the most legible "engineer's tick"
- `■` or `█` — solid square (terminal-cursor look)
- `—` followed by something tiny (e.g. `— ▲`)
- `_` — underscore that extends just past the last word

This is the default. Use the highlight pill only when (a) the user explicitly asks for a banner/marketing feel, or (b) the phrase being emphasized is a multi-word value mid-sentence that genuinely needs to be picked out visually (e.g. a feature list label, an alert).

If you do use a pill, the descender contract above applies without exception.

## Icons

Use **Lucide icons** exclusively, in stroke style at the default 1.5px stroke width. The hairline stroke matches the page's 1px border language.

**Sizing:**
- Sidebar nav icons: 16px
- Inline icons inside labels: 14px
- Button icons: 14px
- Logo / brand glyph slot: 24px

**Color:** Inherit from text. Don't tint icons unless they're inside a status chip or sit on the orange accent.

```html
<!-- Vanilla via CDN -->
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>
<i data-lucide="settings"></i>
<script>lucide.createIcons();</script>
```

```jsx
import { Settings, Github, Gitlab } from 'lucide-react';
<Settings size={16} strokeWidth={1.5} />
```

## Spacing System

Base unit: `4px`. Spacing values are multiples of 4. Industrial layouts feel cleaner with generous, consistent gutters — don't be stingy with padding.

| Token | Value | Usage |
|-------|-------|-------|
| `--space-1` | 4px | Tight internal gaps |
| `--space-2` | 8px | Icon-to-text gaps |
| `--space-3` | 12px | Form field spacing |
| `--space-4` | 16px | Default content padding |
| `--space-5` | 20px | Card content padding |
| `--space-6` | 24px | Card outer padding |
| `--space-8` | 32px | Between sections inside a card |
| `--space-10` | 40px | Between top-level cards |
| `--space-12` | 48px | Page padding (desktop) |

## Layout Principles

### Page Structure

Three main shapes show up across every page type — sidebar shell, full-width single column, and centered marketing column. Pick the one that fits the content; the visual language stays the same.

```
<body>          ← hatched background lives here
  <aside>       ← optional, white surface, fixed width
  <main>        ← max-width 1200px on full-width pages
    <header>    ← page title + breadcrumb / utility actions
    <section>   ← stack of cards, each with internal section rows
  </main>
</body>
```

### The Card

The card is the workhorse. Every meaningful chunk of content lives in one.

```css
.card {
  background: var(--bg-surface);
  border: 1px solid var(--border-default);
  border-radius: 0;            /* sharp corners — non-negotiable */
  padding: 0;                  /* padding lives on .card-row */
}
.card + .card {
  margin-top: var(--space-10);
}
```

- Background: pure white
- Border: 1px solid `--border-default`
- Border-radius: `0`
- Box-shadow: **none** — the border carries all the weight
- Padding: applied to interior rows, not the card itself, so section rules can extend edge-to-edge

### The Section Row

Inside a card, content is organized into rows separated by hairline horizontal rules. Each row starts with an uppercase label.

```css
.card-row {
  padding: var(--space-6);
  border-bottom: 1px solid var(--border-light);
}
.card-row:last-child { border-bottom: 0; }

.card-section-label {
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--text-primary);
  margin-bottom: var(--space-4);
}
```

This row+label pattern is what makes the layout feel like a printed form. Use it everywhere a card has more than one logical chunk.

### Grids

- Two-up panels (e.g., "YOUR ACCOUNT" + "YOUR ORGANIZATION"): 1fr 1fr, gap 16px
- Step rows ("STEP 1 / STEP 2" with action button on the right): use a flex row with `justify-content: space-between` and a min-width 140px button column
- Card grids on dashboards/landings: `repeat(auto-fit, minmax(280px, 1fr))`, gap 16px
- Mobile (<768px): collapse to single column, keep card padding consistent

## Component Specifications

The complete CSS for every component lives in `references/components.md`. Read that file before writing CSS. The high-level rules below are enough to plan the page; the reference fills in the exact values.

### Buttons

**Primary (solid black):** `#0A0A0A` bg, white uppercase text, 1px black border, 0 radius, 10px 20px padding. Hover lifts background to `#1A1A1A`. Used for the main action in a row.

**Secondary (outline):** white bg, black text, 1px black border, 0 radius. Hover swaps to `--bg-inset`.

**Tertiary / link:** no border, accent-colored uppercase text. Used for "Edit" / "Cancel" inline actions.

**Danger:** white bg, `--danger-text` text, 1px solid `--danger-text` border. Used only inside a danger-zone row.

All buttons have `font-weight: 600`, `letter-spacing: 0.08em`, `text-transform: uppercase`. Don't soften this — the typography is doing structural work.

### Toggles

The toggle is the one place orange shows up consistently. It's a `36px × 20px` pill-shaped track with a 16px white thumb. **On** = orange track, thumb on right. **Off** = light gray (`#D0D0D0`) track, thumb on left. The toggle is the only component allowed to be fully rounded; it's a deliberate contrast against the hard-edged everything-else.

### Inputs / Selects

White bg, 1px black border, 0 radius, 10px 12px padding, 14px text. Focus state shows an inset 2px orange ring (`box-shadow: inset 0 0 0 2px var(--accent)`), no outline. Don't use rounded corners on inputs even when frameworks default to them.

### Monogram Tile

The signature identity element. A square block (typically 96px or 120px on a side) of `--bg-inset` with 1-2 large characters centered:

```css
.monogram {
  width: 120px;
  height: 120px;
  background: var(--bg-inset);
  display: grid;
  place-items: center;
  font-size: 64px;
  font-weight: 600;
  letter-spacing: -0.04em;
  color: var(--text-primary);
}
```

Use it for: account avatars, organization tiles, brand glyphs in marketing hero, big "this is who/what this is" anchors. If the user has a Chinese name, render the family-given pair (e.g., 靖易) at this size — Chinese glyphs are even more striking at this scale than Latin initials.

### Tables

Sharp-edged, hairline-separated, no zebra striping. Header row has `--bg-inset` background, uppercase label typography, 1px bottom border `--border-default`. Data rows separated by `--border-light`. Numeric columns get tabular numerals and right alignment.

### Status / Section Labels

Use the same typography across ALL section-defining text — section labels, card row labels, table headers, badge labels. This typographic uniformity is what makes the design feel coherent.

### Danger Zone

Always the last row in settings-style cards. Label uses `--danger-text` color but identical typography to other section labels. Action button uses the danger button variant.

For the full styles (selectors, hover/focus states, every spacing value), read `references/components.md`.

## A Worked Example

For a complete walkthrough showing how all of these pieces fit together in a single HTML file (the same Settings/Account layout from the reference image, plus a Dashboard variant and a Landing variant), read `references/example.md`. It's the fastest way to build a mental model of how the design language behaves across page types — refer to it whenever you're unsure how a layout should be assembled.

## Generalization Guidance

The user's content type varies wildly — settings, dashboards, marketing pages, product detail, blog, admin tools, status pages. The visual language above is fixed; what changes per page type is which components you reach for. Some patterns to internalize:

- **Marketing / landing**: hero uses the monogram tile (or a giant version of it) as a brand block, body becomes a stack of cards each with a labeled section row. CTA is a solid black button.
- **Dashboard**: replace the "step row" pattern with stat cards in a grid; tables sit in their own card with a labeled header.
- **Admin / Settings**: the reference image — sidebar + stacked cards + "STEP 1 / STEP 2" rows + danger zone at the bottom.
- **Blog / Portfolio**: list rows separated by hairline rules; each post entry has a small label for date/category in the uppercase typography. Hero monogram for the author.
- **Status / Health page**: rows of services with their state in a chip on the right; orange shows up when something needs attention, the orange `--accent` is the warning, and `--danger-text` is the outage.

When in doubt, ask: "would this make sense on graph paper?" If yes, you're on track. If a design choice softens the page (rounded corners, drop shadows, gradients, multiple accent colors), drop it.

## Density and Restraint

This aesthetic looks busy if you treat it as a license to add more. It isn't. The visual signature — hatched ground, sharp white cards, hairline borders, uppercase labels — is doing all the heavy lifting on its own. Your job is to give it room to breathe, not to crowd it with extra "engineering vibes" decoration.

Specifically, watch for these temptations and resist them:

**One label, not three.** A page header should have a single title — not eyebrow + title + monospace subtitle stacked together. If you find yourself writing a top-of-card row that looks like `Sector 04 // North Atlantic Lane` above `Shipment Control` above `Live tracking // 1,284 active manifests // window 24h`, you've added three competing labels where one would do. Pick the one that names the thing. Move the rest into the body of the page if they're really useful, or delete them if they're not.

**No `//` chains as decoration.** Splitting a single sentence with `//` separators (e.g. `Live tracking // 1,284 active manifests // window 24h`) reads as engineering-document cosplay rather than as actual data. If those values matter, render them as discrete elements — a chip, a stat cell, a line in a table. If they don't, drop them.

**Don't number what doesn't need numbering.** Adding tiny corner labels like `KPI · 01 / 04`, `§ 04 — The Field Report`, or `01 / 03` to every card is a tic, not a feature. Use those numeric tags only when ordering matters (a "STEP 1 / STEP 2" workflow, a numbered table of contents) — and keep them in one place per page.

**Don't put a sparkline in every stat.** Stat cards in this system are intentionally simple: label, big number, optional one-line delta. Adding a mini bar-chart or sparkline to every KPI clutters the row, fights the tabular numerals for attention, and breaks the "everything's at the same density" rhyme. If a chart belongs on the page, give it its own card.

**Cap header actions.** A page header with three buttons (`Filter` + `Export` + `New +`) crowds the title and forces the eye to pick. Show one primary action plus at most one secondary; move the rest into a toolbar inside the card they belong to.

**Whitespace is a load-bearing part of the design.** When a card has only a label and one row of content, that's correct — don't fill the empty space with a "since X · Y · Z" run of metadata. The hatched background outside the card is doing the visual work.

The single best self-check before declaring a layout done: count the small text strings in the header area of any page or card. If there are more than two distinct lines of label/eyebrow/subtitle text, you're over-decorating. Cut.

## Rendering Contracts

Style is mostly right by now if you've followed the rules above. What still trips this aesthetic up is the small stuff — icons drifting half a pixel off the text baseline, the browser drawing its own rounded corner on a `<select>`, a long tracking ID overflowing a table cell, Chinese glyphs clipping against the next line. These aren't visual style choices; they're rendering bugs. The contracts in this section close those gaps.

Treat them as load-bearing. If any single contract isn't met, the page looks "almost right but off" — which is the worst place to be.

### Highlight pill fallback (when pill is unavoidable)

The preferred heading emphasis is the punctuation accent described in the Typography section. But if a project genuinely needs an inline highlight pill — e.g. the user asks for a banner, or you're highlighting a value mid-sentence — the pill must not render with descender clipping (`y/g/p/j/q` poking below the colored block). This is a hard rendering contract:

```css
.has-highlight { line-height: 1.15; }     /* never below 1.1; never line-height: 1 */

.hl {
  background: var(--accent);
  color: var(--text-on-dark);
  padding: 0.12em 0.35em;                  /* em-based, scales with font-size */
  display: inline;                          /* not inline-block — let it wrap naturally */
  box-decoration-break: clone;
  -webkit-box-decoration-break: clone;
}
```

A `padding: 0 8px` (px-based, no vertical padding) on a 44px heading is the canonical broken case — it gives 0 room for a `y` descender at 50px+ glyph height. Use em-based padding so the colored block scales with the type size.

### Icons (Lucide)

Icons sit beside text constantly in this aesthetic, so getting them to share a baseline matters more than usual.

- **Stroke width 1.5px**, not the Lucide default of 2. The heavier default fights the hairline 1px borders everywhere else. Set this once globally: `<svg ... stroke-width="1.5">` or `lucide.createIcons({ attrs: { 'stroke-width': '1.5' } });`. In React/Vue, pass `strokeWidth={1.5}` on every component import.
- **Always set both width and height**, never one without the other. Lucide's CDN renders at 24×24 by default and will look subtly oversized unless explicitly sized. Use the sizes from the Icons section.
- **Vertical alignment.** `<i data-lucide>` renders as inline; the rendered `<svg>` defaults to baseline-aligned, which sits a few pixels too low next to body text. Fix with one CSS rule:
  ```css
  [data-lucide], .lucide, svg.lucide { vertical-align: -0.15em; }
  ```
  Or, simpler and more robust: put icons inside a flex container with `align-items: center`. Nav items, buttons, chips, and label rows all use flex — so icons there are fine. The bug shows up only when an icon is dropped into prose or a heading without a flex wrapper.
- **Icon color inherits from text.** Don't set `color` on the icon itself unless it's a status icon (in a chip/badge). The hairline stroke + inherited color is what makes them feel like part of the type.

### Form elements

Browsers paint their own decorations on form controls and *they will break this aesthetic* unless you explicitly reset them. The cost of forgetting is a rounded `<select>` chevron in the middle of an otherwise sharp-cornered page — a tell that everything in the design is fighting.

- **Reset `appearance: none`** on every `input`, `select`, and `textarea`. Then `border-radius: 0` (don't trust browser defaults to be 0 even after appearance reset).
- **Custom `<select>` chevron.** With `appearance: none` the chevron disappears. Re-add it as a background-image SVG so you control its color, weight, and position. The chevron must be hairline stroke matching the icon stroke width (1.5px).
- **Placeholder color** is `--text-muted`. Set it explicitly via `::placeholder` — browser defaults render placeholders too dark.
- **Disabled state** uses `--bg-inset` background, `--text-muted` text, `cursor: not-allowed`. Don't dim with opacity; that breaks the hairline border contrast.
- **Focus ring.** The inset 2px orange ring on inputs is the canonical focus state. For buttons (which don't have an inset), use `outline: 2px solid var(--accent); outline-offset: 2px`. Tertiary buttons that are bare text need a focus ring too — don't let "no border" mean "no focus indicator."
- **Number inputs** should use `font-variant-numeric: tabular-nums` so the value doesn't shift horizontally as digits change.

The exact reset CSS is in `references/components.md` under "Form element resets" — copy it as-is, don't improvise.

### Tables

Tables in this aesthetic carry a lot of data — they're where rendering bugs are most visible.

- **Cell padding is `16px` vertical, `16px` horizontal.** Don't go below `12px` on either axis — cells feel cramped fast in a sharp-edged design where nothing is rounded to give visual breathing room.
- **Identifier columns use mono.** Anything that's a fixed-width alphanumeric token — tracking numbers, order IDs, SHAs, UUIDs, API keys, IP addresses, timestamps with `:` separators — uses `var(--font-mono)` at `12.5–13px`. This isn't decoration; mono distinguishes `0/O`, `1/I/l`, and lets readers compare two IDs at a glance. Sans-serif IDs are a real legibility regression.
- **Pure numeric columns** (counts, currency, percentages, durations in human form like "2h 14m") stay in `var(--font-sans)` with `font-variant-numeric: tabular-nums` and right-aligned. Don't mono these — mono digits are wider and look "industrial cosplay" when applied to all numbers indiscriminately.
- **Long text columns** (origins, destinations, descriptions) need a max-width and `text-overflow: ellipsis` with `white-space: nowrap`. Don't let one over-long row blow up the table layout. For columns that legitimately wrap, set `white-space: normal` and let them breathe — but pick one behavior per column.
- **Status cells** wrap the chip in a single flex container; don't stack chips inside a table cell.
- **Header row** is `--bg-inset` background, uppercase + letter-spaced label typography, 1px bottom border in `--border-default` (not `--border-light` — the header needs to feel anchored).
- **Hover state** on data rows: `background: rgba(0, 0, 0, 0.02)`. Subtle enough not to compete with status chips.

### Stat delta colors

The skill's color rules say orange + red are the only non-neutrals, with one deliberate exception: **stat deltas use the dashboard convention of success-green for "up" and danger-red for "down."** Long-running data conventions matter more than aesthetic purity here — engineers read green/red on a dashboard pre-attentively. The greens elsewhere in the system stay banned; this is the only sanctioned use.

```css
--accent-up: #2A8F4D;   /* allowed only on .stat__delta and inline +/-N% inside a stat card */
```

If you're tempted to use `--accent-up` anywhere outside a stat delta — a chip, a status indicator, an "online" dot, a checkmark — stop. Use the chip system instead.

### Typography: CJK and mixed-script

Inter and Noto Sans SC have different x-heights and stroke densities. Pure-English `line-height: 1.5` becomes visibly tight when Chinese glyphs are interleaved with it.

- **Body text containing Chinese:** use `line-height: 1.7` instead of `1.5`. The extra 0.2 keeps strokes off the row above when characters like 鬱/體/襯 appear.
- **Headings containing Chinese:** never go below `line-height: 1.3` (even when English-only headings use `line-height: 1` for tight engineering aesthetic). Chinese needs the breathing room.
- **`text-transform: uppercase` on mixed-script runs.** Uppercase has no effect on CJK but `letter-spacing` does, and aggressive letter-spacing (`0.08em+`) on Chinese makes glyphs visually drift apart. When a label is mixed-script, drop letter-spacing to `0.04em` or split the run: `<span class="latin">YOUR ACCOUNT</span> · <span class="cjk">账户</span>`, only letter-space the latin span.
- **Don't end a CJK heading with Latin punctuation** like `.` — the period sits awkwardly against the wide CJK character. Either drop the punctuation or use the full-width equivalent (`。`).
- **Hanging punctuation.** When a paragraph starts with `"` or `「`, set `hanging-punctuation: first allow-end last` so the opening quote hangs in the margin and the optical edge of the column stays clean.

### Buttons and interaction polish

- **Transition timing**: `transition: background-color 120ms ease-out, color 120ms ease-out, border-color 120ms ease-out;`. Don't transition `all` — it animates `width/height/layout` if anything changes them, which causes jitter.
- **Icon-text gap** inside buttons and chips is `var(--space-2)` (8px). Set it on the parent via `gap: var(--space-2)` — don't `margin-right` on the icon.
- **Cursor on disabled** is `not-allowed`, not `default`. Cursor is the cheapest affordance — use it.
- **Tap targets** are `min-height: 40px` on mobile, including ghost/tertiary buttons. Don't shrink them below 40px even when the design looks "tighter" small — accessibility wins this argument every time.

## What to Avoid

These will quietly destroy the aesthetic — watch for them in your output:

- Any `border-radius` greater than 0 on cards, buttons, inputs (toggles and tiny chips are the only exceptions)
- Drop shadows on cards (`box-shadow` outside of focus rings)
- Multiple accent colors. Orange is the only non-neutral. If you need a second signal, use the danger red — never blue, green, purple, or yellow as decoration.
- Sans-serif heavy weights below 500 — looks anemic against the strong borders.
- Gradients of any kind.
- The hatched stripes applied to white surfaces (it should only appear on `body`/page background).
- Generic "elevated card" feel from drop shadows or color tints — the border alone defines structure.
- Rounded "pill" buttons. Buttons are rectangles.
- Inline `<span>` highlights with `padding: 0 8px` (no vertical padding). Descenders in `y / g / p / j / q` will poke below the colored background. Use `padding: 0.12em 0.35em` and `line-height: 1.15+` on the parent heading.
- Stacked eyebrow + title + monospace subtitle in page headers. Pick one label.
- Sparklines or mini-bar charts baked into every stat card. If a chart matters, give it its own card.
- `//` separator chains used as decorative metadata strings. They read as costume, not data.
- Tiny index labels like `KPI · 01 / 04` or `§ 03` on every card. Use ordinal numbering only when sequence is the point.
- `<i data-lucide>` icons without a global `vertical-align: -0.15em` rule (or without flex container) — they sit a pixel or two below the text baseline and look "off."
- `<select>` / `<input>` without `appearance: none` — the browser draws its own rounded chevron/inner shadow, which fights the design.
- Sans-serif tracking numbers, hashes, and timestamps in tables. Use `var(--font-mono)` so `0/O` and `1/I/l` are distinguishable.
- Mono on every number in sight. Pure numeric columns stay sans + `tabular-nums`; mono is for fixed-width identifiers.
- Body Chinese text at `line-height: 1.5`. Mixed-script body needs `line-height: 1.7`; mixed-script headings need at least `1.3`.
- Aggressive `letter-spacing` on mixed-script labels — Chinese characters drift apart visibly above `0.04em`. Either split the latin and CJK spans or relax the spacing.
- `transition: all` on interactive elements. Be specific: `transition: background-color 120ms ease-out, color 120ms ease-out, border-color 120ms ease-out`.
- `cursor: default` on disabled elements. Always `cursor: not-allowed`.
- Tap targets under 40px on mobile, including ghost/tertiary buttons.
- Defaulting to an orange highlight pill behind a phrase in a hero heading. The pill is a heavy-handed marketing-banner move that buries the typography under a color block. Default to the punctuation accent (`/`, `■`, `_`) at the end of the phrase — it preserves the engineering-drawing feel and gives the orange a single, decisive footprint instead of a broad background.

## Accessibility

- Color contrast: `#0A0A0A` on `#FFFFFF` is 19.5:1 (AAA). `#F06D2D` on `#FFFFFF` is 3.5:1 — large/bold UI only (toggles, button text on orange backgrounds is fine; orange body text is not, which is why orange is reserved for chips, toggles, and short link text).
- Focus rings: 2px inset orange ring on inputs; 2px outset orange outline with 2px offset on buttons.
- Tap targets: minimum 40px × 40px for any interactive element on touch devices.
- Don't rely on color alone to convey state — pair orange/red with an icon or label.
