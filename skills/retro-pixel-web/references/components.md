# Complete Component CSS

This file contains the full CSS for all components in the Retro Pixel Web system. Copy this into a CSS Module file or plain CSS file as appropriate.

## Full Component Stylesheet

```css
/* ============================================
   RETRO PIXEL WEB - Complete CSS
   ============================================ */

/* --- Fonts --- */
/* Pure monospace font stack for all text */
@import url('https://fonts.googleapis.com/css2?family=Courier+Prime:wght@400;700&display=swap');

/* --- CSS Variables --- */
:root {
  --font-pixel: 'Courier Prime', 'Sarasa Mono SC', 'Noto Sans Mono CJK SC', 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', monospace;
  --font-body: 'Courier Prime', 'Sarasa Mono SC', 'Noto Sans Mono CJK SC', 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', monospace;

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

  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 20px;
  --space-6: 24px;
  --space-8: 32px;
}

/* --- Reset & Base --- */
*, *::before, *::after {
  box-sizing: border-box;
}

html {
  font-size: 16px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  margin: 0;
  font-family: var(--font-pixel);
  font-size: 14px;
  line-height: 1.6;
  color: var(--text-primary);
  background: var(--bg-base);
  min-height: 100vh;
}

/* --- Typography --- */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-pixel);
  text-transform: uppercase;
  line-height: 1.4;
  margin: 0;
  color: var(--text-primary);
}

h1 { font-size: 20px; }
h2 { font-size: 14px; }
h3 { font-size: 12px; }

p {
  margin: 0;
  color: var(--text-secondary);
}

/* --- Layout --- */
.header {
  height: 60px;
  background: var(--bg-base);
  border-bottom: 2px solid var(--border-default);
  display: flex;
  align-items: center;
  padding: 0 var(--space-6);
  gap: var(--space-4);
  position: sticky;
  top: 0;
  z-index: 100;
}

.header__title {
  font-family: var(--font-pixel);
  font-size: 14px;
  text-transform: uppercase;
  color: var(--text-primary);
}

.header__spacer {
  flex: 1;
}

.main {
  padding: var(--space-6);
  max-width: 1400px;
  margin: 0 auto;
}

.page-header {
  margin-bottom: var(--space-6);
}

.page-header__title {
  font-size: 20px;
  margin-bottom: var(--space-2);
}

.page-header__subtitle {
  font-size: 14px;
  color: var(--text-secondary);
}

.grid {
  display: grid;
  gap: var(--space-4);
  grid-template-columns: repeat(4, 1fr);
}

@media (max-width: 1023px) {
  .grid { grid-template-columns: repeat(2, 1fr); }
}

@media (max-width: 767px) {
  .grid { grid-template-columns: 1fr; }
  .main { padding: var(--space-4); }
  .header { padding: 0 var(--space-4); }
}

@media (max-width: 479px) {
  .header__title { display: none; }
}

/* --- Card --- */
.card {
  background: var(--bg-surface);
  border: 2px solid var(--border-default);
  border-radius: 10px;
  padding: var(--space-4);
  transition: transform 150ms ease-out, box-shadow 150ms ease-out;
}

.card:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
}

.card__header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: var(--space-3);
}

.card__title {
  font-size: 12px;
  color: var(--text-primary);
}

/* --- Buttons --- */
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-2);
  padding: 10px 20px;
  border-radius: 8px;
  font-family: var(--font-pixel);
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.02em;
  line-height: 1;
  cursor: pointer;
  border: 2px solid var(--border-default);
  transition: all 150ms ease-out;
  text-decoration: none;
}

.btn:focus-visible {
  outline: 2px solid var(--border-accent);
  outline-offset: 2px;
}

.btn--primary {
  background: var(--accent-primary);
  color: #FFFFFF;
}

.btn--primary:hover {
  background: var(--accent-primary-hover);
  transform: translateY(-1px);
}

.btn--secondary {
  background: var(--bg-surface);
  color: var(--text-primary);
}

.btn--secondary:hover {
  background: var(--bg-base);
}

.btn--ghost {
  background: transparent;
  color: var(--accent-primary);
  border: none;
  padding: 8px 12px;
}

.btn--ghost:hover {
  text-decoration: underline;
}

.btn--sm {
  padding: 6px 12px;
  font-size: 8px;
}

.btn--icon {
  padding: 8px;
}

/* --- Status Badges --- */
.badge {
  display: inline-flex;
  align-items: center;
  gap: var(--space-1);
  padding: 4px 10px;
  border-radius: 9999px;
  font-family: var(--font-pixel);
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  border: 1px solid;
  line-height: 1.4;
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

.badge--info {
  background: rgba(59, 130, 246, 0.15);
  color: var(--accent-info);
  border-color: rgba(59, 130, 246, 0.3);
}

/* --- Stat Cards --- */
.stat-card {
  background: var(--bg-surface);
  border: 2px solid var(--border-default);
  border-radius: 10px;
  padding: var(--space-5);
  transition: transform 150ms ease-out, box-shadow 150ms ease-out;
}

.stat-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
}

.stat-card__label {
  font-family: var(--font-pixel);
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--text-secondary);
  margin-bottom: var(--space-2);
}

.stat-card__value {
  font-family: var(--font-pixel);
  font-size: 32px;
  font-weight: 700;
  color: var(--accent-primary);
  line-height: 1.2;
  letter-spacing: -0.02em;
}

@media (max-width: 767px) {
  .stat-card__value { font-size: 24px; }
}

.stat-card__delta {
  font-family: var(--font-pixel);
  font-size: 13px;
  margin-top: var(--space-1);
}

.stat-card__delta--positive { color: var(--accent-success); }
.stat-card__delta--negative { color: var(--accent-danger); }

/* --- Tables --- */
.table-container {
  background: var(--bg-surface);
  border: 2px solid var(--border-default);
  border-radius: 10px;
  overflow: hidden;
}

.table-wrapper {
  overflow-x: auto;
}

.table {
  width: 100%;
  border-collapse: collapse;
  font-size: 14px;
}

.table th {
  background: var(--bg-inset);
  font-family: var(--font-pixel);
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--text-secondary);
  padding: var(--space-3) var(--space-4);
  text-align: left;
  font-weight: 400;
  white-space: nowrap;
}

.table td {
  padding: var(--space-3) var(--space-4);
  border-bottom: 1px solid var(--border-light);
  color: var(--text-primary);
  white-space: nowrap;
}

.table tbody tr:hover {
  background: var(--bg-base);
}

.table tbody tr:last-child td {
  border-bottom: none;
}

/* --- Tabs --- */
.tabs {
  display: flex;
  gap: var(--space-1);
  background: var(--bg-inset);
  padding: var(--space-1);
  border-radius: 10px;
  width: fit-content;
}

.tab {
  padding: var(--space-2) var(--space-4);
  border-radius: 8px;
  font-family: var(--font-pixel);
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.02em;
  color: var(--text-secondary);
  background: transparent;
  border: 2px solid transparent;
  cursor: pointer;
  transition: all 150ms ease-out;
}

.tab:hover {
  color: var(--text-primary);
}

.tab:focus-visible {
  outline: 2px solid var(--border-accent);
  outline-offset: 2px;
}

.tab--active {
  background: var(--bg-surface);
  color: var(--text-primary);
  border-color: var(--border-default);
}

/* --- Inputs --- */
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

.input--search {
  padding-left: 38px;
}

.input-wrapper {
  position: relative;
}

.input-wrapper .lucide-search {
  position: absolute;
  left: 14px;
  top: 50%;
  transform: translateY(-50%);
  color: var(--text-muted);
  pointer-events: none;
}

/* --- Reduced Motion --- */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```
