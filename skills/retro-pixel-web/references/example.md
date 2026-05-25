# Complete Example Page

This is a fully standalone HTML page demonstrating every component in the Retro Pixel Web system with both English and Chinese text. Save this as `index.html` and open it in a browser.

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Retro Pixel Web</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Courier+Prime:wght@400;700&family=Noto+Sans+SC:wght@400;500;600;700&display=swap" rel="stylesheet">
  <script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>
  <style>
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
    }

    *, *::before, *::after { box-sizing: border-box; }

    html { font-size: 16px; -webkit-font-smoothing: antialiased; }

    body {
      margin: 0;
      font-family: var(--font-pixel);
      font-size: 14px;
      line-height: 1.6;
      color: var(--text-primary);
      background: var(--bg-base);
      min-height: 100vh;
    }

    h1, h2, h3 { font-family: var(--font-pixel); text-transform: uppercase; line-height: 1.4; margin: 0; color: var(--text-primary); }
    h1 { font-size: 20px; }
    h2 { font-size: 14px; }
    h3 { font-size: 12px; }
    p { margin: 0; color: var(--text-secondary); }

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

    .header__title { font-family: var(--font-pixel); font-size: 14px; text-transform: uppercase; color: var(--text-primary); }
    .header__spacer { flex: 1; }

    .main { padding: var(--space-6); max-width: 1400px; margin: 0 auto; }

    .page-header { margin-bottom: var(--space-6); }
    .page-header__title { font-size: 20px; margin-bottom: var(--space-2); }
    .page-header__subtitle { font-size: 14px; color: var(--text-secondary); }

    .grid { display: grid; gap: var(--space-4); grid-template-columns: repeat(4, 1fr); }
    @media (max-width: 1023px) { .grid { grid-template-columns: repeat(2, 1fr); } }
    @media (max-width: 767px) { .grid { grid-template-columns: 1fr; } .main { padding: var(--space-4); } }
    @media (max-width: 479px) { .header__title { display: none; } }

    .card { background: var(--bg-surface); border: 2px solid var(--border-default); border-radius: 10px; padding: var(--space-4); transition: transform 150ms ease-out, box-shadow 150ms ease-out; }
    .card:hover { transform: translateY(-2px); box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08); }

    .btn {
      display: inline-flex; align-items: center; justify-content: center; gap: var(--space-2);
      padding: 10px 20px; border-radius: 8px; font-family: var(--font-pixel); font-size: 10px;
      text-transform: uppercase; letter-spacing: 0.02em; line-height: 1; cursor: pointer;
      border: 2px solid var(--border-default); transition: all 150ms ease-out; text-decoration: none;
      background: none; color: inherit;
    }
    .btn:focus-visible { outline: 2px solid var(--border-accent); outline-offset: 2px; }
    .btn--primary { background: var(--accent-primary); color: #FFFFFF; }
    .btn--primary:hover { background: var(--accent-primary-hover); transform: translateY(-1px); }
    .btn--secondary { background: var(--bg-surface); color: var(--text-primary); }
    .btn--secondary:hover { background: var(--bg-base); }
    .btn--ghost { background: transparent; color: var(--accent-primary); border: none; padding: 8px 12px; }
    .btn--ghost:hover { text-decoration: underline; }
    .btn--sm { padding: 6px 12px; font-size: 8px; }
    .btn--icon { padding: 8px; }

    .badge {
      display: inline-flex; align-items: center; gap: var(--space-1); padding: 4px 10px;
      border-radius: 9999px; font-family: var(--font-pixel); font-size: 10px;
      text-transform: uppercase; letter-spacing: 0.05em; border: 1px solid; line-height: 1.4;
    }
    .badge--success { background: rgba(16, 185, 129, 0.15); color: var(--accent-success); border-color: rgba(16, 185, 129, 0.3); }
    .badge--warning { background: rgba(245, 158, 11, 0.15); color: var(--accent-warning); border-color: rgba(245, 158, 11, 0.3); }
    .badge--danger { background: rgba(239, 68, 68, 0.15); color: var(--accent-danger); border-color: rgba(239, 68, 68, 0.3); }

    .stat-card { background: var(--bg-surface); border: 2px solid var(--border-default); border-radius: 10px; padding: var(--space-5); transition: transform 150ms ease-out, box-shadow 150ms ease-out; }
    .stat-card:hover { transform: translateY(-2px); box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08); }
    .stat-card__label { font-family: var(--font-pixel); font-size: 10px; text-transform: uppercase; letter-spacing: 0.05em; color: var(--text-secondary); margin-bottom: var(--space-2); }
    .stat-card__value { font-family: var(--font-pixel); font-size: 32px; font-weight: 700; color: var(--accent-primary); line-height: 1.2; letter-spacing: -0.02em; }
    @media (max-width: 767px) { .stat-card__value { font-size: 24px; } }
    .stat-card__delta { font-family: var(--font-pixel); font-size: 13px; margin-top: var(--space-1); }
    .stat-card__delta--positive { color: var(--accent-success); }
    .stat-card__delta--negative { color: var(--accent-danger); }

    .table-container { background: var(--bg-surface); border: 2px solid var(--border-default); border-radius: 10px; overflow: hidden; }
    .table-wrapper { overflow-x: auto; }
    .table { width: 100%; border-collapse: collapse; font-size: 14px; }
    .table th { background: var(--bg-inset); font-family: var(--font-pixel); font-size: 10px; text-transform: uppercase; letter-spacing: 0.05em; color: var(--text-secondary); padding: var(--space-3) var(--space-4); text-align: left; font-weight: 400; white-space: nowrap; }
    .table td { padding: var(--space-3) var(--space-4); border-bottom: 1px solid var(--border-light); color: var(--text-primary); white-space: nowrap; }
    .table tbody tr:hover { background: var(--bg-base); }
    .table tbody tr:last-child td { border-bottom: none; }

    .tabs { display: flex; gap: var(--space-1); background: var(--bg-inset); padding: var(--space-1); border-radius: 10px; width: fit-content; }
    .tab { padding: var(--space-2) var(--space-4); border-radius: 8px; font-family: var(--font-pixel); font-size: 10px; text-transform: uppercase; letter-spacing: 0.02em; color: var(--text-secondary); background: transparent; border: 2px solid transparent; cursor: pointer; transition: all 150ms ease-out; }
    .tab:hover { color: var(--text-primary); }
    .tab:focus-visible { outline: 2px solid var(--border-accent); outline-offset: 2px; }
    .tab--active { background: var(--bg-surface); color: var(--text-primary); border-color: var(--border-default); }

    .input { width: 100%; padding: 10px 14px; font-size: 14px; font-family: var(--font-pixel); color: var(--text-primary); background: var(--bg-surface); border: 2px solid var(--border-light); border-radius: 8px; outline: none; transition: border-color 150ms ease-out; }
    .input::placeholder { color: var(--text-muted); }
    .input:focus { border-color: var(--border-accent); }
    .input--search { padding-left: 38px; }
    .input-wrapper { position: relative; }
    .input-wrapper .search-icon { position: absolute; left: 14px; top: 50%; transform: translateY(-50%); color: var(--text-muted); pointer-events: none; }


    .section { margin-bottom: var(--space-6); }
    .section__title { margin-bottom: var(--space-4); }

    @media (prefers-reduced-motion: reduce) {
      *, *::before, *::after { animation-duration: 0.01ms !important; animation-iteration-count: 1 !important; transition-duration: 0.01ms !important; }
    }
  </style>
</head>
<body>
  <header class="header">
    <i data-lucide="layout-dashboard" style="width:20px;height:20px;color:var(--accent-primary);"></i>
    <span class="header__title">Server Monitor</span>
    <div class="header__spacer"></div>
    <span class="badge badge--success" role="status" aria-label="System status: all systems operational">
      <i data-lucide="check-circle" style="width:10px;height:10px;"></i>
      Online
    </span>
  </header>

  <main class="main">
    <div class="page-header">
      <h1 class="page-header__title">Dashboard</h1>
      <p class="page-header__subtitle">Overview of your infrastructure status</p>
    </div>

    <section class="section">
      <div class="grid">
        <div class="stat-card">
          <div class="stat-card__label">Uptime</div>
          <div class="stat-card__value">99.97%</div>
          <div class="stat-card__delta stat-card__delta--positive">+0.02%</div>
        </div>
        <div class="stat-card">
          <div class="stat-card__label">Requests</div>
          <div class="stat-card__value">2.4M</div>
          <div class="stat-card__delta stat-card__delta--positive">+12.5%</div>
        </div>
        <div class="stat-card">
          <div class="stat-card__label">Latency</div>
          <div class="stat-card__value">42ms</div>
          <div class="stat-card__delta stat-card__delta--negative">+3ms</div>
        </div>
        <div class="stat-card">
          <div class="stat-card__label">Errors</div>
          <div class="stat-card__value">0.01%</div>
          <div class="stat-card__delta stat-card__delta--positive">-0.003%</div>
        </div>
      </div>
    </section>

    <section class="section">
      <h2 class="section__title">Services</h2>
      <div class="table-container">
        <div class="table-wrapper">
          <table class="table">
            <thead>
              <tr>
                <th scope="col">Service</th>
                <th scope="col">Status</th>
                <th scope="col">Region</th>
                <th scope="col">Latency</th>
                <th scope="col">Uptime</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><strong>API Gateway</strong></td>
                <td><span class="badge badge--success"><i data-lucide="check-circle" style="width:10px;height:10px;"></i> Healthy</span></td>
                <td>US-East</td>
                <td>12ms</td>
                <td>99.99%</td>
              </tr>
              <tr>
                <td><strong>Auth Service</strong></td>
                <td><span class="badge badge--success"><i data-lucide="check-circle" style="width:10px;height:10px;"></i> Healthy</span></td>
                <td>US-East</td>
                <td>8ms</td>
                <td>99.97%</td>
              </tr>
              <tr>
                <td><strong>Database</strong></td>
                <td><span class="badge badge--warning"><i data-lucide="alert-triangle" style="width:10px;height:10px;"></i> Degraded</span></td>
                <td>EU-West</td>
                <td>145ms</td>
                <td>98.50%</td>
              </tr>
              <tr>
                <td><strong>Cache</strong></td>
                <td><span class="badge badge--success"><i data-lucide="check-circle" style="width:10px;height:10px;"></i> Healthy</span></td>
                <td>US-East</td>
                <td>2ms</td>
                <td>99.99%</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </section>

    <section class="section">
      <div style="display:flex; align-items:center; justify-content:space-between; margin-bottom:var(--space-4);">
        <h2 class="section__title" style="margin-bottom:0;">Recent Activity</h2>
        <div class="tabs" role="tablist" aria-label="Activity filter">
          <button class="tab tab--active" role="tab" aria-selected="true">All</button>
          <button class="tab" role="tab" aria-selected="false">Errors</button>
          <button class="tab" role="tab" aria-selected="false">Warnings</button>
        </div>
      </div>
      <div class="card">
        <div class="input-wrapper" style="margin-bottom:var(--space-4);">
          <span class="search-icon"><i data-lucide="search" style="width:16px;height:16px;"></i></span>
          <input type="text" class="input input--search" placeholder="Search logs...">
        </div>
        <div style="display:flex; flex-direction:column; gap:var(--space-3);">
          <div style="display:flex; align-items:center; gap:var(--space-3); padding:var(--space-3); border-radius:8px; border:1px solid var(--border-light);">
            <i data-lucide="check-circle" style="width:16px;height:16px;color:var(--accent-success);"></i>
            <div style="flex:1;">
              <div style="font-weight:600; color:var(--text-primary);">Deployment completed</div>
              <div style="font-size:13px; color:var(--text-secondary);">v2.4.1 deployed to production</div>
            </div>
            <span style="font-size:12px; color:var(--text-muted); font-family:var(--font-pixel); font-size:8px;">2m ago</span>
          </div>
          <div style="display:flex; align-items:center; gap:var(--space-3); padding:var(--space-3); border-radius:8px; border:1px solid var(--border-light);">
            <i data-lucide="alert-triangle" style="width:16px;height:16px;color:var(--accent-warning);"></i>
            <div style="flex:1;">
              <div style="font-weight:600; color:var(--text-primary);">High latency detected</div>
              <div style="font-size:13px; color:var(--text-secondary);">Database response time > 100ms</div>
            </div>
            <span style="font-size:12px; color:var(--text-muted); font-family:var(--font-pixel); font-size:8px;">15m ago</span>
          </div>
          <div style="display:flex; align-items:center; gap:var(--space-3); padding:var(--space-3); border-radius:8px; border:1px solid var(--border-light);">
            <i data-lucide="x-circle" style="width:16px;height:16px;color:var(--accent-danger);"></i>
            <div style="flex:1;">
              <div style="font-weight:600; color:var(--text-primary);">Failed login attempt</div>
              <div style="font-size:13px; color:var(--text-secondary);">IP 192.168.1.100 - 3 attempts</div>
            </div>
            <span style="font-size:12px; color:var(--text-muted); font-family:var(--font-pixel); font-size:8px;">1h ago</span>
          </div>
        </div>
      </div>
    </section>

    <section class="section">
      <h2 class="section__title">Quick Actions</h2>
      <div style="display:flex; gap:var(--space-3); flex-wrap:wrap;">
        <button class="btn btn--primary">
          <i data-lucide="refresh-cw" style="width:14px;height:14px;"></i>
          Restart Services
        </button>
        <button class="btn btn--secondary">
          <i data-lucide="download" style="width:14px;height:14px;"></i>
          Export Logs
        </button>
        <button class="btn btn--ghost">
          <i data-lucide="settings" style="width:14px;height:14px;"></i>
          Settings
        </button>
      </div>
    </section>
  </main>

  <script>
    lucide.createIcons();
  </script>
</body>
</html>
```

To use this example:

1. Copy the code above into `index.html`
2. Open it in any modern browser
3. Observe how all components render consistently
4. Note that both English and Chinese headings use the monospace font
