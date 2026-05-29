---
name: "retro-pixel-web"
description: >-
  Retro typewriter web UI: cream backgrounds, bold dark borders,
  purple/indigo accent (#6366F1), pure monospace typography, card layouts.
  Use this skill when the user explicitly requests a retro, nostalgic,
  or typewriter aesthetic for a web page, landing page, blog, portfolio,
  dashboard, admin panel, or e-commerce site.
---

# Retro Pixel Web Skill

## Overview

This skill produces web interfaces that blend modern web functionality with retro typewriter-inspired aesthetics. The style is prescriptive — every decision below is fixed. Do not ask the user to choose between options. If a choice is unclear from context, default to the value specified here.

Signature characteristics:

- Cream/off-white page background with bold dark borders on all elevated surfaces
- Purple/indigo (`#6366F1`) as the primary action color
- Green and red/orange reserved exclusively for status indicators
- Card-based layouts with visible separation via borders (not shadows)
- Pure monospace font stack (Courier Prime for English, Sarasa Mono SC for Chinese) used **uniformly for all text** — headings, body, buttons, tables, inputs, and labels
- Lucide icons throughout
- WCAG-compliant contrast ratios

## Tech Stack Decision

Before generating code, determine the project's tech stack from context:

1. **Check the codebase** for existing framework usage (React, Vue, Svelte, etc.).
2. **If a framework is found**, write components in that framework's style with CSS Modules for styling.
3. **If no framework is detected or the user is unsure**, default to **vanilla HTML + CSS Modules**.
4. **Never** use CSS-in-JS libraries (styled-components, emotion) unless the project already uses them.
5. **Never** use inline styles for component styling.
6. For bundlers/build tools, follow whatever the project already uses. For a greenfield project with no build tool, use plain HTML/CSS files.

## Color System

Colors are defined as CSS custom properties in `:root`.

### Light Mode (default)

| Token | Value | Usage |
|-------|-------|-------|
| `--bg-base` | `#FFFDF5` | Page background (warm cream) |
| `--bg-surface` | `#FFFFFF` | Card backgrounds |
| `--bg-inset` | `#F5F0E8` | Nested/inset areas, chart backgrounds |
| `--text-primary` | `#1F2937` | Headings, primary content |
| `--text-secondary` | `#6B7280` | Labels, descriptions, metadata |
| `--text-muted` | `#9CA3AF` | Placeholders, disabled states |
| `--accent-primary` | `#6366F1` | Primary buttons, active states, links |
| `--accent-primary-hover` | `#4F46E5` | Primary button hover |
| `--accent-success` | `#10B981` | Success states, healthy indicators |
| `--accent-warning` | `#F59E0B` | Warnings, attention |
| `--accent-danger` | `#EF4444` | Errors, critical alerts |
| `--accent-info` | `#3B82F6` | Informational highlights |
| `--border-default` | `#1F2937` | Card borders, dividers (bold dark) |
| `--border-light` | `#E5E7EB` | Subtle internal borders |
| `--border-accent` | `#6366F1` | Focus rings, active tab borders |

### CSS Implementation

```css
:root {
  --bg-base: #FFFDF5;
  --bg-surface: #FFFFFF;
  --bg-inset: #F5F0E8;
  --text-primary: #1F2937;
  --text-secondary: #6B7280;
  --text-muted: #9CA3AF;
  --accent-primary: #6366F1;
  --accent-primary-hover: #4F46E5;
  --accent-success: #10B981;
  --accent-warning: #F59E0B;
  --accent-danger: #EF4444;
  --accent-info: #3B82F6;
  --border-default: #1F2937;
  --border-light: #E5E7EB;
  --border-accent: #6366F1;
}
```

## Typography

### Font Stack

```css
/* Pure monospace font stack for all text */
@import url('https://fonts.googleapis.com/css2?family=Courier+Prime:wght@400;700&family=Noto+Sans+SC:wght@400;500;600;700&display=swap');

:root {
  --font-pixel: 'Courier Prime', 'Sarasa Mono SC', 'Noto Sans Mono CJK SC', 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', monospace;
  --font-body: 'Courier Prime', 'Sarasa Mono SC', 'Noto Sans Mono CJK SC', 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', monospace;
}
```

**Font selection rationale:**
- `Courier Prime` — English and Latin characters, elegant typewriter-style monospace serif, excellent readability at all sizes (loaded from Google Fonts, weights: 400, 700)
- `Sarasa Mono SC` — Chinese monospace font (Iosevka + Source Han Sans blend), modern and clean, ideal pairing with Courier Prime (system-installed preferred)
- `Noto Sans Mono CJK SC` — Google's open-source Chinese monospace font (system-installed fallback)
- `Noto Sans SC` — High-quality Chinese sans-serif loaded from Google Fonts, serves as a reliable fallback when monospace Chinese fonts are unavailable
- `PingFang SC` / `Microsoft YaHei` — System default Chinese fonts (final fallback)
- `monospace` — Ultimate fallback

**Every piece of text on the page uses the same monospace stack.** There is no sans-serif font anywhere. English renders in Courier Prime; Chinese renders in Sarasa Mono SC (or the nearest available monospace/fallback). This creates a unified typewriter-terminal aesthetic throughout.

| Element | Font | Size | Weight | Letter-spacing | Line-height |
|---------|------|------|--------|----------------|-------------|
| Page title (h1) | `--font-pixel` | 20px | 400 | 0 | 1.4 |
| Section heading (h2) | `--font-pixel` | 14px | 400 | 0 | 1.4 |
| Card title (h3) | `--font-pixel` | 12px | 400 | 0 | 1.4 |
| Body text | `--font-body` | 14px | 400 | normal | 1.6 |
| Labels / metadata | `--font-pixel` | 10px | 400 | 0.05em | 1.4 |
| Large numbers / stats | `--font-body` | 32px | 700 | -0.02em | 1.2 |
| Button text | `--font-pixel` | 10px | 400 | 0.02em | 1 |

**Rules:**
- All text must use a monospace font. No sans-serif or serif fonts anywhere.
- Headings use `--font-pixel`. Body text, tables, inputs, and stat values use `--font-body`.
- Both `--font-pixel` and `--font-body` point to the exact same monospace stack. The two variables exist only to allow future differentiation if needed.
- Use `text-transform: uppercase` on heading/label/button text (for English/Latin script; Chinese text does not use uppercase transformation).
- All monospace text must have `line-height: 1.4` minimum to prevent clipping, especially when mixing English and Chinese.
- When mixing English and Chinese, ensure sufficient `line-height` (at least 1.4) to accommodate the taller Chinese glyphs.

## Icons

Use **Lucide icons** exclusively. Import via CDN or npm package `lucide-react` / `lucide-vue` / `lucide` depending on the framework.

**Icon sizing:**
- Navigation / header icons: 20px
- Card action icons: 16px
- Inline text icons: 16px
- Status indicator icons: 12px
- Button icons: 16px

**Icon color:** Inherit from parent text color. For status icons, match the status badge color.

**Implementation:**

```html
<!-- Vanilla HTML via CDN -->
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>
<script>
  lucide.createIcons();
</script>
<i data-lucide="activity" class="icon"></i>
```

```jsx
// React
import { Activity, AlertCircle, CheckCircle } from 'lucide-react';
<Activity size={16} />
```

## Spacing System

Base unit: `4px`. All spacing values are multiples of 4.

| Token | Value | Usage |
|-------|-------|-------|
| `--space-1` | 4px | Tight internal gaps |
| `--space-2` | 8px | Icon-to-text gaps |
| `--space-3` | 12px | Small padding |
| `--space-4` | 16px | Card padding, gap between cards |
| `--space-5` | 20px | Medium padding |
| `--space-6` | 24px | Page padding |
| `--space-8` | 32px | Large page padding |

## Layout Principles

### Page Structure

```
<body>
  <header class="header">...</header>
  <main class="main">
    <div class="page-header">...</div>
    <div class="grid">...</div>
  </main>
</body>
```

### Card Grid

- Desktop (>= 1024px): 3-4 columns
- Tablet (>= 768px): 2 columns
- Mobile (< 768px): 1 column
- Gap between cards: `16px`

### Card Design (Fixed)

```css
.card {
  background: var(--bg-surface);
  border: 2px solid var(--border-default);
  border-radius: 10px;
  padding: 16px;
}
```

- Background: white
- Border: `2px solid var(--border-default)` — this is the signature look
- Border-radius: `10px`
- Box-shadow: none — the border provides all definition
- Padding: `16px`

## Component Specifications

All components are fully specified below. Read `references/components.md` for complete CSS implementations. Do not deviate from these specifications.

### Buttons

**Primary Button**
- Background: `--accent-primary`
- Text: white, monospace font, 10px, uppercase
- Border: `2px solid var(--border-default)`
- Border-radius: `8px`
- Padding: `10px 20px`
- Hover: background shifts to `--accent-primary-hover`, `transform: translateY(-1px)`
- Focus: `outline: 2px solid var(--border-accent)`, `outline-offset: 2px`
- Transition: `all 150ms ease-out`

**Secondary Button**
- Background: `--bg-surface`
- Text: `--text-primary`, monospace font, 10px, uppercase
- Border: `2px solid var(--border-default)`
- Border-radius: `8px`
- Padding: `10px 20px`
- Hover: background shifts to `--bg-base`
- Focus: same as primary

**Ghost Button**
- Background: transparent
- Text: `--accent-primary`, monospace font, 10px, uppercase
- Border: none
- Hover: underline
- Focus: `outline: 2px solid var(--border-accent)`

### Status Badges

```css
.badge {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  padding: 4px 10px;
  border-radius: 9999px;
  font-family: var(--font-pixel);
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  border: 1px solid;
}

.badge--success {
  background: rgba(16, 185, 129, 0.15);
  color: var(--accent-success);
  border-color: rgba(16, 185, 129, 0.3);
}

.badge--warning {
  background: rgba(245, 158, 11, 0.15);
  color: var(--accent-warning);
  border-color: rgba(245, 158, 11, 0.3);
}

.badge--danger {
  background: rgba(239, 68, 68, 0.15);
  color: var(--accent-danger);
  border-color: rgba(239, 68, 68, 0.3);
}
```

Every status badge must include a Lucide icon (size: 10px) before the text:
- Success: `CheckCircle` icon
- Warning: `AlertTriangle` icon
- Danger: `XCircle` icon

### Stat Cards (formerly KPI Cards)

```css
.stat-card {
  background: var(--bg-surface);
  border: 2px solid var(--border-default);
  border-radius: 10px;
  padding: 20px;
}

.stat-card__label {
  font-family: var(--font-pixel);
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--text-secondary);
  margin-bottom: 8px;
}

.stat-card__value {
  font-family: var(--font-pixel);
  font-size: 32px;
  font-weight: 700;
  color: var(--accent-primary);
  line-height: 1.2;
  letter-spacing: -0.02em;
}

.stat-card__delta {
  font-family: var(--font-pixel);
  font-size: 13px;
  margin-top: 4px;
}

.stat-card__delta--positive { color: var(--accent-success); }
.stat-card__delta--negative { color: var(--accent-danger); }
```

Use stat cards for displaying key metrics, counts, or highlight numbers on any page type (dashboards, landing pages, product pages, etc.).

### Tables

```css
.table-container {
  background: var(--bg-surface);
  border: 2px solid var(--border-default);
  border-radius: 10px;
  overflow: hidden;
}

.table {
  width: 100%;
  border-collapse: collapse;
}

.table th {
  background: var(--bg-inset);
  font-family: var(--font-pixel);
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--text-secondary);
  padding: 12px 16px;
  text-align: left;
  font-weight: 400;
}

.table td {
  padding: 12px 16px;
  border-bottom: 1px solid var(--border-light);
  color: var(--text-primary);
  font-size: 14px;
}

.table tbody tr:hover {
  background: var(--bg-base);
}

.table tbody tr:last-child td {
  border-bottom: none;
}
```

### Tabs

```css
.tabs {
  display: flex;
  gap: 4px;
  background: var(--bg-inset);
  padding: 4px;
  border-radius: 10px;
}

.tab {
  padding: 8px 16px;
  border-radius: 8px;
  font-family: var(--font-pixel);
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.02em;
  color: var(--text-secondary);
  background: transparent;
  border: none;
  cursor: pointer;
  transition: all 150ms ease-out;
}

.tab:hover {
  color: var(--text-primary);
}

.tab--active {
  background: var(--bg-surface);
  color: var(--text-primary);
  border: 2px solid var(--border-default);
  box-shadow: 0 1px 2px rgba(0,0,0,0.05);
}
```

### Inputs

```css
.input {
  width: 100%;
  padding: 10px 14px;
  font-size: 14px;
  font-family: var(--font-pixel);
  color: var(--text-primary);
  background: var(--bg-surface);
  border: 2px solid var(--border-light);
  border-radius: 8px;
  outline: none;
  transition: border-color 150ms ease-out;
}

.input::placeholder {
  color: var(--text-muted);
}

.input:focus {
  border-color: var(--border-accent);
}
```

For search inputs, place a Lucide `Search` icon (16px, `--text-muted`) absolutely positioned inside the left padding (14px from left edge).

### Header / Navigation

```css
.header {
  height: 60px;
  background: var(--bg-base);
  border-bottom: 2px solid var(--border-default);
  display: flex;
  align-items: center;
  padding: 0 24px;
  gap: 16px;
}

.header__title {
  font-family: var(--font-pixel);
  font-size: 14px;
  text-transform: uppercase;
  color: var(--text-primary);
}
```

Header must contain (left to right):
1. A Lucide icon (20px) representing the app/page
2. Page title in monospace font
3. Spacer (`flex: 1`)
4. Status badges or actions (if applicable)

## Interaction Patterns

### Hover Effects
- Cards: `transform: translateY(-2px)` + `box-shadow: 0 4px 12px rgba(0,0,0,0.08)`. Transition: `transform 150ms ease-out, box-shadow 150ms ease-out`.
- Buttons: see component specs above.
- Table rows: background shifts to `--bg-base`.

### Focus States
Every interactive element must have a visible focus indicator:
- Default: `outline: 2px solid var(--border-accent)`, `outline-offset: 2px`
- Do not remove outlines with `outline: none` without a replacement.

### Active / Selected States
- Border color changes to `--border-accent`
- Background tint: `rgba(99, 102, 241, 0.1)` (use `background-color` not `background` to avoid overriding)

### Transitions
- Duration: `150ms`
- Easing: `ease-out` or `cubic-bezier(0.4, 0, 0.2, 1)`
- Properties: `all` or specific (`transform, box-shadow, background-color, border-color`)

## Accessibility (A11y)

### Color Contrast
All color combinations must meet WCAG AA standards:
- `--text-primary` on `--bg-surface`: 12.6:1 (passes AAA)
- `--text-secondary` on `--bg-surface`: 5.9:1 (passes AA)
- White text on `--accent-primary`: 4.5:1 (passes AA)
- `--accent-danger` text on badge background: 5.2:1 (passes AA)

Do not use color alone to convey meaning. Status badges must include an icon.

### Focus Management
- All interactive elements (buttons, links, inputs, table rows if clickable, tabs) must have visible focus indicators.
- Focus indicator: `outline: 2px solid var(--border-accent)` with `outline-offset: 2px`.
- Do not use `outline: none`.

### Semantic HTML
- Use `<header>`, `<main>`, `<nav>`, `<section>` where appropriate.
- Use `<button>` for actions, `<a>` for navigation. Do not use `<div>` with click handlers for buttons.
- Tables must use `<table>`, `<thead>`, `<tbody>`, `<th scope="col">`.
- Tabs must use `role="tablist"`, `role="tab"`, `role="tabpanel"` with `aria-selected` on active tab.
- Status badges should include `aria-label` describing the status.

### Reduced Motion

Respect `prefers-reduced-motion`:

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

## Implementation Checklist

Before declaring a page complete, verify:

- [ ] Page background is `--bg-base` (warm cream)
- [ ] All cards have `2px solid var(--border-default)` border and `10px` radius
- [ ] No card uses box-shadow as its primary elevation cue
- [ ] All text uses a monospace font (`--font-pixel` and `--font-body` share the same stack)
- [ ] Headings, body, buttons, tables, inputs — everything is monospace
- [ ] Chinese text uses the monospace font (Sarasa Mono SC / Noto Sans SC fallback)
- [ ] All icons are from Lucide
- [ ] Status badges include icons, not just color
- [ ] Purple/indigo is only used for primary actions and highlights
- [ ] Green/red are only used for status indicators
- [ ] Focus indicators are visible on all interactive elements
- [ ] Semantic HTML is used throughout
- [ ] `prefers-reduced-motion` is respected
- [ ] No gradients anywhere

## Complete Example

Read `references/example.md` for a full standalone HTML page demonstrating every component.

## Responsive Behavior

- Card grid: 4 cols -> 2 cols -> 1 col at breakpoints 1024px / 768px
- Header title: hide on screens < 480px, show icon only
- Table: horizontal scroll on mobile (`overflow-x: auto` on container)
- Stat values: scale down to 24px on mobile
- Page padding: 32px desktop -> 16px mobile
