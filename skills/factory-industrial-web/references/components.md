# Complete Component CSS

This file contains the full CSS for the Factory Industrial Web system. Copy this into a CSS file or `<style>` block. Every value here is intentional — when in doubt, use it as-is rather than improvising.

## Table of Contents

1. Base — fonts, variables, reset
2. Hatched background
3. Layout shells (sidebar + main, full-width, centered marketing)
4. Card and section row
5. Buttons (primary, secondary, tertiary, danger)
6. Toggles
7. Inputs, selects, textareas
8. Monogram tile
9. Tables
10. Status chips and danger zone
11. Stat cards
12. Navigation (sidebar + top nav)
13. Rendering contracts (icons, form resets, mixed-script, transitions)

## 1. Base

```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Noto+Sans+SC:wght@400;500;600;700&display=swap');

:root {
  --font-sans: 'Inter', 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', 'SF Mono', ui-monospace, 'Cascadia Code', Consolas, monospace;

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

  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 20px;
  --space-6: 24px;
  --space-8: 32px;
  --space-10: 40px;
  --space-12: 48px;
}

*, *::before, *::after { box-sizing: border-box; }

html, body {
  margin: 0;
  padding: 0;
  min-height: 100%;
}

body {
  font-family: var(--font-sans);
  font-size: 14px;
  line-height: 1.5;
  color: var(--text-primary);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

h1, h2, h3, h4, h5, h6, p { margin: 0; }

button { font-family: inherit; cursor: pointer; }

input, select, textarea { font-family: inherit; }

a { color: var(--accent); text-decoration: none; }
a:hover { text-decoration: underline; }
```

## 2. Hatched Background

The signature element. Apply to `body` so it scrolls with content.

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

For pages that should *not* show the hatching (pure marketing landings where you want a clean white hero), wrap content in a `.surface-full` that paints `--bg-surface` over the body.

## 3. Layout Shells

### Sidebar + main (settings, admin, app shells)

```css
.app {
  display: grid;
  grid-template-columns: 240px 1fr;
  min-height: 100vh;
}

.sidebar {
  background: var(--bg-surface);
  border-right: 1px solid var(--border-default);
  padding: var(--space-6);
  position: sticky;
  top: 0;
  align-self: start;
  height: 100vh;
  overflow-y: auto;
}

.main {
  padding: var(--space-12);
  max-width: 1200px;
  width: 100%;
}

@media (max-width: 768px) {
  .app { grid-template-columns: 1fr; }
  .sidebar { position: static; height: auto; border-right: 0; border-bottom: 1px solid var(--border-default); }
  .main { padding: var(--space-6); }
}
```

### Full-width single column (dashboards, blog, content pages)

```css
.page {
  max-width: 1200px;
  margin: 0 auto;
  padding: var(--space-12) var(--space-6);
}

.page-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  margin-bottom: var(--space-10);
  padding-bottom: var(--space-6);
  border-bottom: 1px solid var(--border-default);
}

.page-title {
  font-size: 28px;
  font-weight: 600;
  letter-spacing: -0.01em;
}
```

### Centered marketing column

```css
.marketing {
  max-width: 880px;
  margin: 0 auto;
  padding: var(--space-12) var(--space-6);
}
```

## 4. Card and Section Row

```css
.card {
  background: var(--bg-surface);
  border: 1px solid var(--border-default);
  border-radius: 0;
  padding: 0;
}
.card + .card { margin-top: var(--space-10); }

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

.card-section-label--danger { color: var(--danger-text); }

/* Two-up: account + organization style */
.card-row--split {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--space-8);
}

@media (max-width: 768px) {
  .card-row--split { grid-template-columns: 1fr; }
}

/* Step row: label + description on left, button on right */
.step-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: var(--space-4);
  padding: var(--space-4) 0;
  border-top: 1px solid var(--border-light);
}
.step-row:first-of-type { border-top: 0; }

.step-row__label { font-size: 12px; font-weight: 500; }
.step-row__desc { color: var(--text-secondary); font-size: 13px; }
.step-row__action { min-width: 140px; }
```

## 5. Buttons

```css
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-2);
  padding: 10px 20px;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  border: 1px solid var(--border-default);
  border-radius: 0;
  background: var(--bg-surface);
  color: var(--text-primary);
  cursor: pointer;
  transition: background-color 120ms ease-out, color 120ms ease-out;
  user-select: none;
}

.btn:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 2px;
}

.btn--primary {
  background: var(--bg-button-primary);
  color: var(--text-on-dark);
  border-color: var(--bg-button-primary);
}
.btn--primary:hover { background: #1A1A1A; border-color: #1A1A1A; }

.btn--secondary { background: var(--bg-surface); color: var(--text-primary); }
.btn--secondary:hover { background: var(--bg-inset); }

.btn--tertiary {
  background: transparent;
  border-color: transparent;
  color: var(--accent);
  padding: 4px 0;
}
.btn--tertiary:hover { color: var(--accent-hover); text-decoration: underline; }

.btn--danger {
  background: var(--bg-surface);
  color: var(--danger-text);
  border-color: var(--danger-text);
}
.btn--danger:hover { background: rgba(211, 58, 44, 0.08); }

.btn[disabled] { opacity: 0.4; pointer-events: none; }

.btn--block { width: 100%; }
```

## 6. Toggles

The only fully-rounded element in the system. Orange when on.

```css
.toggle {
  position: relative;
  display: inline-block;
  width: 36px;
  height: 20px;
  flex-shrink: 0;
}
.toggle input {
  position: absolute;
  opacity: 0;
  width: 100%;
  height: 100%;
  margin: 0;
  cursor: pointer;
}
.toggle__track {
  display: block;
  width: 100%;
  height: 100%;
  background: #D0D0D0;
  border-radius: 9999px;
  transition: background-color 120ms ease-out;
}
.toggle__thumb {
  position: absolute;
  top: 2px;
  left: 2px;
  width: 16px;
  height: 16px;
  background: #FFFFFF;
  border-radius: 50%;
  transition: transform 120ms ease-out;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
}
.toggle input:checked ~ .toggle__track { background: var(--accent); }
.toggle input:checked ~ .toggle__thumb { transform: translateX(16px); }
.toggle input:focus-visible ~ .toggle__track {
  box-shadow: 0 0 0 3px rgba(240, 109, 45, 0.3);
}
```

## 7. Inputs, Selects, Textareas

```css
.field {
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
}

.field__label {
  font-size: 12px;
  font-weight: 500;
  color: var(--text-secondary);
}

.input,
.select,
.textarea {
  width: 100%;
  padding: 10px 12px;
  font-size: 14px;
  font-family: inherit;
  color: var(--text-primary);
  background: var(--bg-surface);
  border: 1px solid var(--border-default);
  border-radius: 0;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  transition: box-shadow 120ms ease-out, border-color 120ms ease-out;
}

/* Reset browser quirks that the appearance reset alone doesn't catch */
.input { box-shadow: none; }
.input[type="number"] {
  font-variant-numeric: tabular-nums;
  -moz-appearance: textfield;
}
.input[type="number"]::-webkit-outer-spin-button,
.input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Custom select chevron — hairline stroke, matches icon weight */
.select {
  padding-right: 36px;
  background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 24 24' fill='none' stroke='%230A0A0A' stroke-width='1.5' stroke-linecap='square' stroke-linejoin='miter'><polyline points='6 9 12 15 18 9'/></svg>");
  background-repeat: no-repeat;
  background-position: right 12px center;
  cursor: pointer;
}

.input::placeholder,
.textarea::placeholder { color: var(--text-muted); opacity: 1; }

.input:focus,
.select:focus,
.textarea:focus {
  box-shadow: inset 0 0 0 2px var(--accent);
  border-color: var(--accent);
}

.input[disabled],
.select[disabled],
.textarea[disabled] {
  background: var(--bg-inset);
  color: var(--text-muted);
  cursor: not-allowed;
}

.textarea { min-height: 96px; resize: vertical; }
```

## 8. Monogram Tile

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
  flex-shrink: 0;
}

.monogram--sm { width: 64px; height: 64px; font-size: 32px; }
.monogram--lg { width: 200px; height: 200px; font-size: 96px; }

/* Identity row: monogram + key/value pairs */
.identity {
  display: flex;
  gap: var(--space-6);
  align-items: center;
}

.identity__fields {
  display: grid;
  grid-template-columns: max-content 1fr;
  gap: var(--space-3) var(--space-6);
  align-items: baseline;
}

.identity__key {
  font-size: 12px;
  font-weight: 500;
  color: var(--text-secondary);
}

.identity__value {
  font-size: 14px;
  color: var(--text-primary);
}
```

## 9. Tables

```css
.table {
  width: 100%;
  border-collapse: collapse;
  border: 1px solid var(--border-default);
  background: var(--bg-surface);
  font-variant-numeric: tabular-nums;
  table-layout: auto;
}

.table th {
  background: var(--bg-inset);
  padding: var(--space-3) var(--space-4);
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  text-align: left;
  color: var(--text-primary);
  border-bottom: 1px solid var(--border-default);
  white-space: nowrap;
}

.table td {
  padding: var(--space-4);
  border-bottom: 1px solid var(--border-light);
  font-size: 14px;
  color: var(--text-primary);
  vertical-align: middle;
}

.table tbody tr:hover { background: rgba(0, 0, 0, 0.02); }
.table tr:last-child td { border-bottom: 0; }

/* Numeric columns: right-aligned, tabular sans */
.table td--num,
.table th--num { text-align: right; }

/* Identifier columns: mono for fixed-width tokens (tracking #, SHA, UUID, IP, timestamp) */
.table td--id,
.table .col-id {
  font-family: var(--font-mono);
  font-size: 12.5px;
  font-weight: 500;
  letter-spacing: 0.02em;
  color: var(--text-primary);
  white-space: nowrap;
}

/* Long text columns: ellipsis with a sensible max-width */
.table td--ellipsis {
  max-width: 240px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

/* Status cells wrap chips in a flex container — never stacked vertically */
.table td--status { display: table-cell; }
.table td--status > * { display: inline-flex; align-items: center; gap: var(--space-1); }
```

## 10. Chips and Danger Zone

```css
.chip {
  display: inline-flex;
  align-items: center;
  gap: var(--space-1);
  padding: 2px 8px;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  border: 1px solid var(--border-default);
  border-radius: 4px;
  background: var(--bg-surface);
  color: var(--text-primary);
}

.chip--accent {
  background: var(--accent);
  border-color: var(--accent);
  color: var(--text-on-dark);
}

.chip--danger {
  background: var(--bg-surface);
  border-color: var(--danger-text);
  color: var(--danger-text);
}

.chip--muted { color: var(--text-secondary); border-color: var(--border-light); }

/* Danger zone — bottom row of cards */
.danger-zone__title {
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--danger-text);
  margin-bottom: var(--space-4);
}

.danger-zone__row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: var(--space-4);
  padding: var(--space-3) 0;
  border-top: 1px solid var(--border-light);
}
.danger-zone__row:first-of-type { border-top: 0; }
.danger-zone__copy { font-size: 13px; color: var(--text-primary); }
```

### Heading emphasis — preferred: punctuation accent

The default way to put orange into a heading is a single accent stroke at the end of the phrase, not a pill behind a word. The heading stays pure black; the orange shows up as one decisive punctuation mark, like a draftsman's annotation tick. This reads as engineering-drawing, where a pill reads as marketing banner.

```css
.accent-mark {
  color: var(--accent);
  display: inline-block;
  margin-left: 0.08em;
  font-weight: 800;
  font-style: italic;
  transform: skewX(-8deg);   /* optional — adds tooling feel */
}
```

```html
<h1 class="hero__title">
  Coffee, fired<br />
  like ceramics.<span class="accent-mark">/</span>
</h1>
```

Accent variants (pick one per page, don't mix):
- `/` — engineer's tick (most legible)
- `■` `█` — solid square (terminal-cursor look)
- `_` — underscore extending past the last word
- `— ▲` — em-dash plus small symbol

### Heading emphasis — fallback: highlight pill (only when explicitly needed)

Use only if the user asks for a banner feel or you're highlighting a multi-word value mid-sentence that genuinely needs to be picked out. Otherwise prefer the punctuation accent above.

The pill has one hard rendering contract: descenders (`y/g/p/j/q`) must not clip out of the colored block. Use em-based padding and a parent line-height ≥ 1.15.

```css
.has-highlight {
  line-height: 1.15;
}

.hl {
  background: var(--accent);
  color: var(--text-on-dark);
  padding: 0.12em 0.35em;
  display: inline;
  box-decoration-break: clone;
  -webkit-box-decoration-break: clone;
}
```

Usage:

```html
<h2 class="has-highlight">
  One letter,<br />
  <span class="hl">every Friday</span>.
</h2>
```

## 11. Stat Cards

```css
.stat-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: var(--space-4);
}

.stat {
  background: var(--bg-surface);
  border: 1px solid var(--border-default);
  padding: var(--space-5);
}

.stat__label {
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--text-secondary);
  margin-bottom: var(--space-2);
}

.stat__value {
  font-size: 32px;
  font-weight: 600;
  letter-spacing: -0.02em;
  color: var(--text-primary);
  font-variant-numeric: tabular-nums;
}

.stat__delta {
  font-size: 12px;
  font-weight: 500;
  margin-top: var(--space-1);
  font-variant-numeric: tabular-nums;
  display: inline-flex;
  align-items: center;
  gap: var(--space-1);
}

/* Stat delta is the ONE place success-green is allowed. Don't reach for it elsewhere. */
.stat__delta--up { color: #2A8F4D; }
.stat__delta--down { color: var(--danger-text); }
.stat__delta--flat { color: var(--text-muted); }
```

## 12. Navigation

```css
.nav-brand {
  display: flex;
  align-items: center;
  gap: var(--space-2);
  font-size: 14px;
  font-weight: 600;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  margin-bottom: var(--space-8);
}

.nav-section-label {
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.05em;
  color: var(--text-muted);
  margin: var(--space-6) 0 var(--space-2);
}

.nav-item {
  display: flex;
  align-items: center;
  gap: var(--space-2);
  padding: var(--space-2) var(--space-3);
  font-size: 13px;
  color: var(--text-primary);
  border-left: 2px solid transparent;
  cursor: pointer;
  text-decoration: none;
}
.nav-item:hover { background: var(--bg-inset); text-decoration: none; }
.nav-item--active {
  background: var(--bg-inset);
  border-left-color: var(--text-primary);
  font-weight: 500;
}

.nav-item__icon { width: 16px; height: 16px; color: var(--text-secondary); flex-shrink: 0; }

.top-banner {
  background: var(--bg-base);
  background-image: repeating-linear-gradient(135deg, var(--bg-stripe) 0, var(--bg-stripe) 1px, transparent 1px, transparent 7px);
  border-bottom: 1px solid var(--border-default);
  padding: var(--space-3) var(--space-6);
  font-size: 13px;
  color: var(--text-primary);
  display: flex;
  align-items: center;
  gap: var(--space-2);
}
.top-banner a { color: var(--accent); }
```

## 13. Rendering Contracts

The styles in this section are not visual choices — they're the bug-prevention layer. Drop them in once near the top of the stylesheet (after `:root`) and the small rendering glitches that make the design feel "almost right but off" go away.

### Icon alignment + stroke

```css
/* Lucide icons: hairline stroke + inline baseline fix */
[data-lucide],
.lucide,
svg.lucide {
  stroke-width: 1.5;
  vertical-align: -0.15em;
  flex-shrink: 0;
}
```

Initialize Lucide with stroke-width 1.5 globally:

```html
<script>
  lucide.createIcons({ attrs: { 'stroke-width': '1.5' } });
</script>
```

For React: `<Settings size={16} strokeWidth={1.5} />` on every import. For Vue: same pattern via the prop.

### CJK and mixed-script line-height

Apply at the body level when the page is known to contain Chinese, or at the section level when only some sections have it:

```css
body {
  /* Default body line-height stays 1.5 for English-only contexts */
  line-height: 1.5;
}

html[lang^="zh"] body,
.has-cjk {
  line-height: 1.7;
}

html[lang^="zh"] h1,
html[lang^="zh"] h2,
html[lang^="zh"] h3,
.has-cjk h1, .has-cjk h2, .has-cjk h3 {
  line-height: 1.3;
}

/* Hanging punctuation for clean optical column edges */
p { hanging-punctuation: first allow-end last; }
```

When a label is mixed-script, split the runs so letter-spacing only hits Latin characters:

```html
<div class="card-section-label">
  <span class="latin">Your Account</span>
  <span class="cjk">· 您的账户</span>
</div>
```

```css
.card-section-label .latin {
  letter-spacing: 0.08em;
  text-transform: uppercase;
}
.card-section-label .cjk {
  letter-spacing: 0.04em;     /* much gentler — Chinese drifts apart above this */
  margin-left: 4px;
}
```

### Form element resets (universal)

If you can't apply the per-component classes everywhere, this universal reset does the heavy lifting:

```css
input, select, textarea, button {
  font-family: inherit;
  font-size: inherit;
  color: inherit;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  border-radius: 0;
  background-clip: padding-box;
}

button { cursor: pointer; }
button:disabled { cursor: not-allowed; }

/* Remove iOS rounded corners on inputs */
input { -webkit-border-radius: 0; }

/* Search input: kill the cancel cross + magnifying glass */
input[type="search"]::-webkit-search-decoration,
input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-results-button,
input[type="search"]::-webkit-search-results-decoration {
  display: none;
}
```

### Focus ring for tertiary / link buttons

Tertiary buttons have no border, so the standard outline-on-button pattern doesn't read. Use a 2px under-text accent line for keyboard focus:

```css
.btn--tertiary:focus-visible {
  outline: none;
  box-shadow: 0 2px 0 0 var(--accent);
}
```

### Universal transition baseline

Don't write `transition: all` anywhere. Every interactive element transitions only the properties that actually change:

```css
.btn,
.input,
.select,
.textarea,
.toggle__track,
.toggle__thumb,
.nav-item {
  transition: background-color 120ms ease-out,
              color 120ms ease-out,
              border-color 120ms ease-out,
              box-shadow 120ms ease-out,
              transform 120ms ease-out;
}
```

### Tap target minimum (mobile)

```css
@media (max-width: 768px) {
  .btn,
  .nav-item,
  .toggle,
  a[role="button"] {
    min-height: 40px;
  }
}
```
