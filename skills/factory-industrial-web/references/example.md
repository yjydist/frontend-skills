# Worked Examples

Three end-to-end HTML examples that demonstrate how the design language carries across page types. Same colors, same fonts, same border style, same spacing — only the components reach for change.

If you're new to the skill, read example 1 in full, then skim 2 and 3 to see how the same primitives recompose. Whenever you're unsure how to assemble a layout, lift the matching shape from one of these.

## Example 1 — Settings / Account Page

The reference image: sidebar shell, stacked cards with labeled sections, step rows with right-aligned action buttons, monogram tiles for identity, danger zone at the bottom.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Settings — Factory</title>
<link href="components.css" rel="stylesheet" />
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>
</head>
<body>
  <div class="top-banner">
    <i data-lucide="info" style="width:14px;height:14px;"></i>
    You're not on a paid subscription. <a href="#">Upgrade plan</a> for managed models and cloud features.
  </div>

  <div class="app">
    <aside class="sidebar">
      <div class="nav-brand"><i data-lucide="hexagon"></i> FACTORY</div>
      <a class="nav-item" href="#"><i data-lucide="chevron-left" class="nav-item__icon"></i> Back to App</a>
      <div class="nav-section-label">Settings</div>
      <a class="nav-item nav-item--active"><i data-lucide="settings" class="nav-item__icon"></i> General</a>
      <a class="nav-item"><i data-lucide="building-2" class="nav-item__icon"></i> Organization</a>
      <a class="nav-item"><i data-lucide="users" class="nav-item__icon"></i> Members</a>
      <a class="nav-item"><i data-lucide="key" class="nav-item__icon"></i> API Keys</a>
      <a class="nav-item"><i data-lucide="credit-card" class="nav-item__icon"></i> Billing</a>
      <a class="nav-item"><i data-lucide="bar-chart-3" class="nav-item__icon"></i> Usage</a>
      <a class="nav-item"><i data-lucide="cpu" class="nav-item__icon"></i> Droid Computers</a>
      <a class="nav-item"><i data-lucide="shield" class="nav-item__icon"></i> Session Management</a>
      <a class="nav-item"><i data-lucide="life-buoy" class="nav-item__icon"></i> Support</a>
    </aside>

    <main class="main">
      <!-- Account + Organization -->
      <section class="card">
        <div class="card-row card-row--split">
          <div>
            <div class="card-section-label">Your Account</div>
            <div class="identity">
              <div class="monogram">靖易</div>
              <div class="identity__fields">
                <span class="identity__key">Name</span>   <span class="identity__value">靖远 易</span>
                <span class="identity__key">Email</span>  <span class="identity__value">yjydist@163.com</span>
              </div>
            </div>
          </div>
          <div>
            <div class="card-section-label">
              Your Organization
              <a href="#" class="btn btn--tertiary" style="float:right;">Edit</a>
            </div>
            <div class="identity">
              <div class="monogram">Y</div>
              <div class="identity__fields">
                <span class="identity__key">Organization name</span>
                <span class="identity__value">yjydist</span>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Codebase -->
      <section class="card">
        <div class="card-row">
          <div class="card-section-label">Set Up Your Codebase</div>
          <div class="card-row--split" style="padding:0;">
            <div>
              <div style="display:flex;align-items:center;gap:8px;margin-bottom:16px;">
                <i data-lucide="github"></i><strong>GITHUB</strong>
              </div>
              <div class="step-row">
                <div>
                  <div class="step-row__label">STEP 1</div>
                  <div class="step-row__desc">Connect your GitHub organization</div>
                </div>
                <button class="btn btn--primary step-row__action">Connect</button>
              </div>
              <div class="step-row">
                <div>
                  <div class="step-row__label">STEP 2</div>
                  <div class="step-row__desc">Connect your personal GitHub account</div>
                </div>
                <button class="btn btn--primary step-row__action">Connect</button>
              </div>
            </div>
            <div>
              <div style="display:flex;align-items:center;gap:8px;margin-bottom:16px;">
                <i data-lucide="git-branch" style="color:#FC6D26;"></i><strong>GITLAB</strong>
              </div>
              <div class="step-row">
                <div>
                  <div class="step-row__label">STEP 1</div>
                  <div class="step-row__desc">Connect your GitLab organization</div>
                </div>
                <button class="btn btn--primary step-row__action">Connect</button>
              </div>
              <div class="step-row">
                <div>
                  <div class="step-row__label">STEP 2</div>
                  <div class="step-row__desc">Connect your personal GitLab account</div>
                </div>
                <button class="btn btn--primary step-row__action">Connect</button>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Preferences -->
      <section class="card">
        <div class="card-row">
          <div class="card-section-label">Preferences</div>
          <div class="step-row">
            <div class="step-row__label">Disable dynamic loading statuses</div>
            <label class="toggle"><input type="checkbox" /><span class="toggle__track"></span><span class="toggle__thumb"></span></label>
          </div>
        </div>
        <div class="card-row">
          <div class="card-section-label">Keyboard Shortcuts</div>
          <div class="step-row">
            <span class="step-row__label">Toggle spec mode (Shift+Tab)</span>
            <label class="toggle"><input type="checkbox" checked /><span class="toggle__track"></span><span class="toggle__thumb"></span></label>
          </div>
          <div class="step-row">
            <span class="step-row__label">Cycle reasoning level (Tab)</span>
            <label class="toggle"><input type="checkbox" checked /><span class="toggle__track"></span><span class="toggle__thumb"></span></label>
          </div>
          <div class="step-row">
            <span class="step-row__label">Open model selector (Ctrl+N)</span>
            <label class="toggle"><input type="checkbox" checked /><span class="toggle__track"></span><span class="toggle__thumb"></span></label>
          </div>
          <div class="step-row">
            <span class="step-row__label">Cycle autonomy level (Ctrl+L)</span>
            <label class="toggle"><input type="checkbox" checked /><span class="toggle__track"></span><span class="toggle__thumb"></span></label>
          </div>
        </div>
      </section>

      <!-- Danger zone -->
      <section class="card">
        <div class="card-row">
          <div class="card-section-label card-section-label--danger">Danger Zone</div>
          <div class="danger-zone__row">
            <div class="danger-zone__copy">Cancel Subscription — Your payment details will not be stored</div>
            <button class="btn btn--danger">Cancel</button>
          </div>
        </div>
      </section>
    </main>
  </div>

  <script>lucide.createIcons();</script>
</body>
</html>
```

Key takeaways from this example:

- The two-up `card-row--split` shape carries both "account+organization" and "github+gitlab" — same shape, different content. Don't invent new layout grids when a card-row split would work.
- "STEP 1 / STEP 2" is just a `step-row`. Whenever you have label + description on the left and an action button on the right, reach for it.
- The orange `--accent` only appears on toggles and the "Edit" link. Resist using it elsewhere even if you have "primary" content to highlight.
- `DANGER ZONE` lives at the bottom of the last card. The label is colored differently but typographically identical to other section labels.

## Example 2 — Dashboard

Stat grid + a table + a chart placeholder. Same building blocks.

```html
<main class="page">
  <header class="page-header">
    <div>
      <h1 class="page-title">Operations Overview</h1>
      <p style="color:var(--text-secondary);font-size:14px;">Last 30 days · UTC</p>
    </div>
    <div style="display:flex;gap:12px;">
      <button class="btn btn--secondary">Export</button>
      <button class="btn btn--primary">New Report</button>
    </div>
  </header>

  <section class="stat-grid" style="margin-bottom:40px;">
    <div class="stat">
      <div class="stat__label">Total Runs</div>
      <div class="stat__value">12,847</div>
      <div class="stat__delta stat__delta--up">+8.2% vs prev</div>
    </div>
    <div class="stat">
      <div class="stat__label">Success Rate</div>
      <div class="stat__value">98.4%</div>
      <div class="stat__delta stat__delta--up">+0.3 pts</div>
    </div>
    <div class="stat">
      <div class="stat__label">Avg Latency</div>
      <div class="stat__value">312<span style="font-size:18px;color:var(--text-secondary);">ms</span></div>
      <div class="stat__delta stat__delta--down">+24ms</div>
    </div>
    <div class="stat">
      <div class="stat__label">Open Incidents</div>
      <div class="stat__value">3</div>
      <div class="stat__delta">No change</div>
    </div>
  </section>

  <section class="card">
    <div class="card-row">
      <div class="card-section-label">Recent Runs</div>
      <table class="table">
        <thead>
          <tr>
            <th>Run ID</th><th>Started</th><th>Duration</th><th>Status</th><th class="table__cell--num">Tokens</th>
          </tr>
        </thead>
        <tbody>
          <tr><td>r-9c4f1a</td><td>2026-05-23 14:02</td><td>00:42</td><td><span class="chip">Success</span></td><td style="text-align:right;">84,200</td></tr>
          <tr><td>r-9c4f1b</td><td>2026-05-23 13:51</td><td>02:18</td><td><span class="chip chip--accent">Running</span></td><td style="text-align:right;">—</td></tr>
          <tr><td>r-9c4f1c</td><td>2026-05-23 13:39</td><td>00:11</td><td><span class="chip chip--danger">Failed</span></td><td style="text-align:right;">3,118</td></tr>
        </tbody>
      </table>
    </div>
  </section>
</main>
```

Notes:
- Stat cards use the same 1px border, sharp corners, and uppercase label typography as the section labels in cards. The visual rhyme is what holds the system together.
- Tables get tabular numerals automatically via `.table` selector. Right-align numeric columns — never center.
- Three chip variants (default, accent, danger) cover almost every status case. Don't add more colors.

## Example 3 — Marketing Landing

Hero with a giant monogram, a feature grid, a CTA card.

```html
<main class="marketing">
  <section style="display:flex;align-items:center;gap:48px;padding:64px 0;border-bottom:1px solid var(--border-default);">
    <div class="monogram monogram--lg">F</div>
    <div>
      <div style="font-size:11px;font-weight:600;letter-spacing:0.08em;text-transform:uppercase;color:var(--text-secondary);margin-bottom:12px;">v 2.0 — Out Now</div>
      <h1 style="font-size:48px;font-weight:600;letter-spacing:-0.02em;line-height:1.1;margin-bottom:16px;">
        Build software the way you'd build a machine.
      </h1>
      <p style="font-size:16px;color:var(--text-secondary);max-width:520px;margin-bottom:24px;">
        A precision toolchain for shipping reliable systems — designed for engineers who treat code like the load-bearing thing it is.
      </p>
      <div style="display:flex;gap:12px;">
        <button class="btn btn--primary">Get Started</button>
        <button class="btn btn--secondary">Read Docs</button>
      </div>
    </div>
  </section>

  <section style="padding:64px 0;">
    <div class="card-section-label" style="margin-bottom:24px;">What's Inside</div>
    <div class="stat-grid">
      <article class="stat">
        <div style="display:flex;align-items:center;gap:8px;margin-bottom:12px;">
          <i data-lucide="cpu" style="width:18px;height:18px;"></i>
          <strong>Droid Computers</strong>
        </div>
        <p style="color:var(--text-secondary);font-size:13px;">Spin up isolated runtimes per task. No long-lived state, no dependency drift.</p>
      </article>
      <article class="stat">
        <div style="display:flex;align-items:center;gap:8px;margin-bottom:12px;">
          <i data-lucide="git-merge" style="width:18px;height:18px;"></i>
          <strong>Spec Mode</strong>
        </div>
        <p style="color:var(--text-secondary);font-size:13px;">Define what before how. The toolchain holds you to your contract.</p>
      </article>
      <article class="stat">
        <div style="display:flex;align-items:center;gap:8px;margin-bottom:12px;">
          <i data-lucide="shield" style="width:18px;height:18px;"></i>
          <strong>Audit Trail</strong>
        </div>
        <p style="color:var(--text-secondary);font-size:13px;">Every run is reproducible. Every change is signed.</p>
      </article>
    </div>
  </section>

  <section class="card">
    <div class="card-row" style="display:flex;justify-content:space-between;align-items:center;gap:24px;">
      <div>
        <div class="card-section-label">Ready to Start</div>
        <p style="color:var(--text-secondary);">Free for personal projects. Pay when your team grows.</p>
      </div>
      <button class="btn btn--primary">Create Account</button>
    </div>
  </section>
</main>
```

What changed between examples — and what didn't:

- The hero is just an oversized monogram + heading. The monogram tile that anchored the settings page now anchors the marketing page. Same component, different scale.
- Feature cards are stat cards with prose instead of a number. The `.stat` class works fine for both because the visual structure (1px border, no radius, uppercase label, tight padding) is the point.
- The CTA at the bottom is a card with a single split row. No new component invented.

This is the deal: the system is small. When you're tempted to invent a new shape, look back here first — odds are one of the existing pieces stretches to fit.
