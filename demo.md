<!DOCTYPE html>
<html lang="En">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <meta name="color-scheme" content="dark" />
  <title>OceanCentinell ENTERPRISE · Maritime Cyber</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Oxanium:wght@400;600;700;800&family=IBM+Plex+Mono:wght@400;500;600&display=swap" rel="stylesheet">

  <style>
    :root {
      --navy-950: #020c1b;
      --navy-900: #0a1628;
      --navy-800: #0d2240;
      --navy-700: #0f3460;
      --ocean-600: #1a5276;
      --cyan-500: #00d4ff;
      --cyan-400: #38bdf8;
      --cyan-300: #7dd3fc;
      --teal-400: #2dd4bf;
      --green-400: #34d399;
      --amber-400: #fbbf24;
      --red-400: #f87171;
      --rose-400: #fb7185;
      --text: #e8f4fd;
      --muted: #64748b;
      --muted-bright: #94a3b8;
      --card-bg: rgba(10, 22, 40, 0.85);
      --card-border: rgba(0, 212, 255, 0.12);
      --card-border-hover: rgba(0, 212, 255, 0.3);
      --radius: 18px;
      --radius-sm: 10px;
      --focus: 0 0 0 3px rgba(0, 212, 255, 0.4);
      --shadow-card: 0 8px 32px rgba(0, 0, 0, 0.4), 0 1px 0 rgba(0, 212, 255, 0.08) inset;
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html, body { height: 100%; }

    body {
      font-family: 'IBM Plex Mono', monospace;
      background: var(--navy-950);
      color: var(--text);
      overflow-x: hidden;
    }

    /* ─── ANIMATED OCEAN BACKGROUND ─── */
    #ocean-canvas {
      position: fixed;
      inset: 0;
      z-index: 0;
      pointer-events: none;
      opacity: 0.55;
    }

    .layout {
      position: relative;
      z-index: 1;
      max-width: 1800px;
      margin: 0 auto;
      padding: 1.5rem 2rem 2rem;
    }

    /* ─── HEADER ─── */
    .header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 1.5rem;
      flex-wrap: wrap;
      padding: 1.4rem 1.8rem;
      background: linear-gradient(135deg, rgba(10,22,40,0.97) 0%, rgba(15,52,96,0.9) 100%);
      border: 1px solid rgba(0, 212, 255, 0.2);
      border-radius: var(--radius);
      box-shadow: var(--shadow-card), 0 0 60px rgba(0, 212, 255, 0.06);
      backdrop-filter: blur(20px);
      animation: slideDown 0.6s cubic-bezier(0.16,1,0.3,1) both;
    }

    @keyframes slideDown {
      from { opacity: 0; transform: translateY(-20px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    .header-brand {
      display: flex;
      align-items: center;
      gap: 1rem;
    }

    .logo-ring {
      width: 48px; height: 48px;
      border-radius: 50%;
      background: radial-gradient(circle at 30% 30%, rgba(0,212,255,0.2), rgba(10,22,40,0.9));
      border: 1.5px solid rgba(0, 212, 255, 0.45);
      display: flex;
      align-items: center;
      justify-content: center;
      flex-shrink: 0;
      box-shadow: 0 0 20px rgba(0, 212, 255, 0.25), inset 0 0 10px rgba(0,212,255,0.05);
      animation: pulse-ring 3s ease-in-out infinite;
    }

    @keyframes pulse-ring {
      0%, 100% { box-shadow: 0 0 20px rgba(0,212,255,0.25), inset 0 0 10px rgba(0,212,255,0.05); }
      50%       { box-shadow: 0 0 35px rgba(0,212,255,0.5), inset 0 0 15px rgba(0,212,255,0.1); }
    }

    .logo-ring svg { width: 28px; height: 28px; }

    .brand-text h1 {
      font-family: 'Oxanium', sans-serif;
      font-size: clamp(1.4rem, 2.2vw, 2rem);
      font-weight: 800;
      letter-spacing: 0.04em;
      background: linear-gradient(90deg, #e8f4fd 0%, var(--cyan-500) 60%, var(--teal-400) 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      line-height: 1.1;
    }

    .brand-text p {
      font-size: 0.72rem;
      color: var(--muted-bright);
      letter-spacing: 0.06em;
      text-transform: uppercase;
      margin-top: 0.25rem;
    }

    .header-right {
      display: flex;
      align-items: center;
      gap: 1rem;
      flex-wrap: wrap;
    }

    .live-badge {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      padding: 0.45rem 1rem;
      border-radius: 999px;
      background: rgba(52, 211, 153, 0.1);
      border: 1px solid rgba(52, 211, 153, 0.4);
      font-size: 0.72rem;
      font-weight: 600;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      color: var(--green-400);
    }

    .live-dot {
      width: 7px; height: 7px;
      border-radius: 50%;
      background: var(--green-400);
      box-shadow: 0 0 0 0 rgba(52, 211, 153, 0.6);
      animation: ping 1.5s ease-out infinite;
    }

    @keyframes ping {
      0%   { box-shadow: 0 0 0 0 rgba(52,211,153,0.6); }
      70%  { box-shadow: 0 0 0 8px rgba(52,211,153,0); }
      100% { box-shadow: 0 0 0 0 rgba(52,211,153,0); }
    }

    .header-clock {
      font-family: 'IBM Plex Mono', monospace;
      font-size: 0.78rem;
      color: var(--cyan-400);
      opacity: 0.8;
      min-width: 80px;
      text-align: right;
    }

    /* ─── PLAN TABS ─── */
    .plan-strip {
      display: flex;
      gap: 0.5rem;
      flex-wrap: wrap;
      margin-top: 1rem;
      animation: fadeUp 0.7s 0.1s cubic-bezier(0.16,1,0.3,1) both;
    }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(12px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    .plan-tab {
      flex: 1;
      min-width: 180px;
      padding: 0.7rem 1rem;
      border-radius: var(--radius-sm);
      background: var(--card-bg);
      border: 1px solid var(--card-border);
      cursor: pointer;
      transition: all 0.2s ease;
      text-align: left;
    }

    .plan-tab:hover {
      border-color: var(--card-border-hover);
      background: rgba(0, 212, 255, 0.05);
    }

    .plan-tab.active {
      background: linear-gradient(135deg, rgba(0,212,255,0.15), rgba(45,212,191,0.1));
      border-color: rgba(0, 212, 255, 0.5);
    }

    .plan-tab-name {
      font-family: 'Oxanium', sans-serif;
      font-weight: 700;
      font-size: 0.82rem;
      color: var(--text);
    }

    .plan-tab.active .plan-tab-name { color: var(--cyan-400); }

    .plan-tab-desc {
      font-size: 0.68rem;
      color: var(--muted);
      margin-top: 0.2rem;
    }

    /* ─── MAIN GRID ─── */
    .main-grid {
      display: grid;
      grid-template-columns: 1fr 420px;
      gap: 1rem;
      margin-top: 1rem;
      animation: fadeUp 0.7s 0.2s cubic-bezier(0.16,1,0.3,1) both;
    }

    .card {
      background: var(--card-bg);
      border: 1px solid var(--card-border);
      border-radius: var(--radius);
      padding: 1.4rem;
      box-shadow: var(--shadow-card);
      backdrop-filter: blur(16px);
    }

    .section-label {
      font-family: 'Oxanium', sans-serif;
      font-size: 0.68rem;
      font-weight: 600;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--cyan-400);
      opacity: 0.7;
      margin-bottom: 0.8rem;
    }

    /* ─── METRICS ─── */
    .metrics-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 0.75rem;
    }

    .metric-card {
      background: linear-gradient(145deg, rgba(15,52,96,0.4), rgba(10,22,40,0.6));
      border: 1px solid rgba(0,212,255,0.1);
      border-radius: 14px;
      padding: 1.1rem 1rem;
      cursor: pointer;
      transition: all 0.18s ease;
      position: relative;
      overflow: hidden;
    }

    .metric-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 0;
      height: 1px;
      background: linear-gradient(90deg, transparent, rgba(0,212,255,0.4), transparent);
      opacity: 0;
      transition: opacity 0.2s;
    }

    .metric-card:hover::before, .metric-card.active::before { opacity: 1; }

    .metric-card:hover {
      border-color: rgba(0, 212, 255, 0.3);
      background: linear-gradient(145deg, rgba(0,212,255,0.08), rgba(10,22,40,0.7));
      transform: translateY(-2px);
    }

    .metric-card.active {
      border-color: rgba(0, 212, 255, 0.5);
      background: linear-gradient(145deg, rgba(0,212,255,0.12), rgba(10,22,40,0.7));
    }

    .metric-icon-wrap {
      width: 32px; height: 32px;
      border-radius: 8px;
      background: rgba(0,212,255,0.1);
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 0.6rem;
    }

    .metric-icon-wrap svg {
      width: 16px; height: 16px;
      stroke: var(--cyan-400);
      fill: none;
      stroke-width: 1.8;
    }

    .metric-value {
      font-family: 'Oxanium', sans-serif;
      font-size: clamp(1.5rem, 2vw, 2.1rem);
      font-weight: 800;
      color: var(--cyan-400);
      letter-spacing: -0.02em;
      line-height: 1;
    }

    .metric-value.risk-low    { color: var(--green-400); }
    .metric-value.risk-medium { color: var(--amber-400); }
    .metric-value.risk-high   { color: var(--red-400); }
    .metric-value.risk-crit   { color: var(--rose-400); }

    .metric-label {
      font-size: 0.68rem;
      color: var(--muted-bright);
      text-transform: uppercase;
      letter-spacing: 0.08em;
      margin-top: 0.3rem;
    }

    .metric-delta {
      font-size: 0.65rem;
      color: var(--muted);
      margin-top: 0.15rem;
    }

    /* ─── SPARKLINE ─── */
    .sparkline-wrap {
      margin-top: 0.8rem;
      padding: 0.9rem;
      background: rgba(2,12,27,0.8);
      border: 1px solid rgba(0,212,255,0.1);
      border-radius: var(--radius-sm);
    }

    .sparkline-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 0.5rem;
      font-size: 0.7rem;
      color: var(--muted-bright);
    }

    .sparkline-title { font-weight: 600; }

    canvas#sparkline {
      width: 100%;
      height: 50px;
      display: block;
    }

    /* ─── METRIC DETAIL ─── */
    .metric-detail-panel {
      margin-top: 0.8rem;
      padding: 0.9rem 1rem;
      background: rgba(2,12,27,0.8);
      border: 1px solid rgba(0,212,255,0.12);
      border-radius: var(--radius-sm);
      display: flex;
      gap: 0.8rem;
      align-items: flex-start;
      font-size: 0.8rem;
    }

    .detail-icon {
      width: 36px; height: 36px;
      border-radius: 9px;
      background: rgba(0,212,255,0.08);
      display: flex;
      align-items: center;
      justify-content: center;
      flex-shrink: 0;
    }

    .detail-icon svg {
      width: 18px; height: 18px;
      stroke: var(--cyan-400);
      fill: none;
      stroke-width: 1.8;
    }

    .detail-text-title {
      font-family: 'Oxanium', sans-serif;
      font-weight: 700;
      font-size: 0.82rem;
      color: var(--text);
      margin-bottom: 0.25rem;
    }

    .detail-text-body { color: var(--muted-bright); line-height: 1.5; }

    /* ─── MINI DASH BARS ─── */
    .mini-dash { margin-top: 0.7rem; }

    .mini-row {
      display: flex;
      align-items: center;
      gap: 0.6rem;
      margin-bottom: 0.45rem;
      font-size: 0.72rem;
    }

    .mini-label { flex: 0 0 80px; color: var(--muted); }
    .mini-val { color: var(--text); font-weight: 600; flex: 0 0 40px; text-align: right; }

    .mini-bar-track {
      flex: 1;
      height: 5px;
      border-radius: 999px;
      background: rgba(255,255,255,0.06);
      overflow: hidden;
    }

    .mini-bar-fill {
      height: 100%;
      border-radius: 999px;
      background: linear-gradient(90deg, var(--cyan-500), var(--teal-400));
      transition: width 0.6s cubic-bezier(0.16,1,0.3,1);
    }

    /* ─── STATUS ROW ─── */
    .status-row {
      display: flex;
      flex-wrap: wrap;
      gap: 0.6rem;
      margin-top: 0.8rem;
      align-items: center;
    }

    .status-pill {
      display: inline-flex;
      align-items: center;
      gap: 0.4rem;
      padding: 0.3rem 0.75rem;
      border-radius: 999px;
      background: rgba(255,255,255,0.04);
      border: 1px solid rgba(255,255,255,0.08);
      font-size: 0.7rem;
      color: var(--muted-bright);
      white-space: nowrap;
    }

    .status-pill strong { color: var(--text); }

    /* ─── THREATS PANEL ─── */
    .threats-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 0.8rem;
      flex-wrap: wrap;
      gap: 0.5rem;
    }

    .threats-title {
      font-family: 'Oxanium', sans-serif;
      font-weight: 700;
      font-size: 0.95rem;
    }

    .filter-pills {
      display: flex;
      gap: 0.3rem;
    }

    .filter-pill {
      padding: 0.2rem 0.6rem;
      border-radius: 999px;
      font-size: 0.65rem;
      cursor: pointer;
      border: 1px solid rgba(255,255,255,0.15);
      background: transparent;
      color: var(--muted-bright);
      transition: all 0.15s;
      text-transform: uppercase;
      letter-spacing: 0.05em;
      font-family: inherit;
    }

    .filter-pill:hover { border-color: rgba(0,212,255,0.4); color: var(--cyan-400); }
    .filter-pill.active { background: rgba(0,212,255,0.15); border-color: rgba(0,212,255,0.5); color: var(--cyan-400); }
    .filter-pill.fp-low.active    { background: rgba(52,211,153,0.12); border-color: var(--green-400); color: var(--green-400); }
    .filter-pill.fp-medium.active { background: rgba(251,191,36,0.12); border-color: var(--amber-400); color: var(--amber-400); }
    .filter-pill.fp-high.active   { background: rgba(248,113,113,0.12); border-color: var(--red-400); color: var(--red-400); }
    .filter-pill.fp-critical.active { background: rgba(251,113,133,0.12); border-color: var(--rose-400); color: var(--rose-400); }

    .legend {
      display: flex;
      gap: 0.7rem;
      margin-bottom: 0.6rem;
      flex-wrap: wrap;
    }

    .legend-dot {
      width: 7px; height: 7px;
      border-radius: 50%;
      flex-shrink: 0;
    }

    .legend-item { display: flex; align-items: center; gap: 0.25rem; font-size: 0.65rem; color: var(--muted-bright); }

    .incidents-feed {
      height: 360px;
      overflow-y: auto;
      overflow-x: hidden;
      padding-right: 0.3rem;
      scrollbar-width: thin;
      scrollbar-color: rgba(0,212,255,0.3) transparent;
    }

    .incidents-feed::-webkit-scrollbar { width: 4px; }
    .incidents-feed::-webkit-scrollbar-thumb { background: rgba(0,212,255,0.3); border-radius: 4px; }

    .incident-card {
      padding: 0.85rem;
      border-radius: 10px;
      border: 1px solid rgba(255,255,255,0.06);
      margin-bottom: 0.55rem;
      border-left: 3px solid transparent;
      transition: border-color 0.15s, background 0.15s;
      background: rgba(255,255,255,0.02);
      animation: slideIn 0.3s ease both;
    }

    @keyframes slideIn {
      from { opacity: 0; transform: translateX(10px); }
      to   { opacity: 1; transform: translateX(0); }
    }

    .incident-card.sev-low      { border-left-color: var(--green-400); }
    .incident-card.sev-medium   { border-left-color: var(--amber-400); }
    .incident-card.sev-high     { border-left-color: var(--red-400); }
    .incident-card.sev-critical { border-left-color: var(--rose-400); }

    .incident-card:hover { background: rgba(0,212,255,0.04); border-color: rgba(0,212,255,0.2); }

    .inc-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 0.5rem;
    }

    .inc-id {
      font-family: 'Oxanium', sans-serif;
      font-weight: 700;
      font-size: 0.8rem;
    }

    .risk-badge {
      display: inline-flex;
      align-items: center;
      padding: 0.15rem 0.55rem;
      border-radius: 999px;
      font-size: 0.65rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.06em;
      border: 1px solid transparent;
    }

    .risk-badge.low      { background: rgba(52,211,153,0.12); border-color: rgba(52,211,153,0.35); color: var(--green-400); }
    .risk-badge.medium   { background: rgba(251,191,36,0.12); border-color: rgba(251,191,36,0.35); color: var(--amber-400); }
    .risk-badge.high     { background: rgba(248,113,113,0.12); border-color: rgba(248,113,113,0.35); color: var(--red-400); }
    .risk-badge.critical { background: rgba(251,113,133,0.14); border-color: rgba(251,113,133,0.4); color: var(--rose-400); }

    .inc-tags {
      display: flex;
      gap: 0.35rem;
      flex-wrap: wrap;
      margin-top: 0.45rem;
    }

    .inc-tag {
      font-size: 0.65rem;
      padding: 0.15rem 0.5rem;
      border-radius: 999px;
      background: rgba(0,212,255,0.08);
      border: 1px solid rgba(0,212,255,0.2);
      color: var(--cyan-300);
    }

    .inc-meta {
      font-size: 0.62rem;
      color: var(--muted);
      margin-top: 0.4rem;
    }

    /* ─── WORKSPACE ─── */
    .workspace {
      margin-top: 1rem;
      animation: fadeUp 0.7s 0.35s cubic-bezier(0.16,1,0.3,1) both;
    }

    .ws-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      flex-wrap: wrap;
      gap: 0.5rem;
      margin-bottom: 0.9rem;
    }

    .ws-title {
      font-family: 'Oxanium', sans-serif;
      font-weight: 700;
      font-size: 1rem;
      color: var(--text);
    }

    .ws-subtitle { font-size: 0.72rem; color: var(--muted); margin-top: 0.2rem; }

    .ws-tabs {
      display: flex;
      flex-wrap: wrap;
      gap: 0.35rem;
    }

    .ws-tab {
      padding: 0.35rem 0.75rem;
      border-radius: 999px;
      background: rgba(255,255,255,0.04);
      border: 1px solid rgba(255,255,255,0.1);
      font-size: 0.7rem;
      color: var(--muted-bright);
      cursor: pointer;
      transition: all 0.15s;
      font-family: inherit;
    }

    .ws-tab:hover { border-color: rgba(0,212,255,0.3); color: var(--cyan-400); }

    .ws-tab[aria-selected="true"] {
      background: linear-gradient(135deg, rgba(0,212,255,0.18), rgba(45,212,191,0.12));
      border-color: rgba(0,212,255,0.5);
      color: var(--cyan-400);
      font-weight: 600;
    }

    .ws-panel {
      margin-top: 0.75rem;
      padding: 1rem 1.1rem;
      background: rgba(2,12,27,0.9);
      border: 1px solid rgba(0,212,255,0.12);
      border-radius: 12px;
      font-size: 0.82rem;
    }

    .ws-panel[hidden] { display: none; }

    .ws-panel-title {
      font-family: 'Oxanium', sans-serif;
      font-weight: 700;
      font-size: 0.85rem;
      margin-bottom: 0.8rem;
      color: var(--text);
    }

    .ws-form-row {
      display: flex;
      flex-wrap: wrap;
      gap: 0.7rem;
      margin-bottom: 0.7rem;
    }

    .ws-form-row label {
      display: flex;
      flex-direction: column;
      gap: 0.3rem;
      font-size: 0.68rem;
      color: var(--muted);
      text-transform: uppercase;
      letter-spacing: 0.06em;
    }

    .ws-form-row input,
    .ws-form-row select,
    .ws-form-row textarea {
      background: rgba(10,22,40,0.9);
      border: 1px solid rgba(0,212,255,0.2);
      border-radius: 8px;
      padding: 0.4rem 0.6rem;
      color: var(--text);
      font-size: 0.8rem;
      font-family: inherit;
      min-width: 160px;
      outline: none;
      transition: border-color 0.15s;
    }

    .ws-form-row input:focus,
    .ws-form-row select:focus { border-color: rgba(0,212,255,0.5); }

    .ws-chips { display: flex; gap: 0.5rem; flex-wrap: wrap; margin-bottom: 0.7rem; }

    .ws-chip {
      padding: 0.25rem 0.65rem;
      border-radius: 999px;
      border: 1px solid rgba(0,212,255,0.25);
      background: rgba(0,212,255,0.06);
      font-size: 0.68rem;
      color: var(--cyan-300);
    }

    .ws-actions { display: flex; flex-wrap: wrap; gap: 0.5rem; }

    .ws-log {
      margin-top: 0.7rem;
      padding: 0.6rem 0.8rem;
      border-radius: 8px;
      background: rgba(2,12,27,1);
      border: 1px solid rgba(0,212,255,0.15);
      max-height: 130px;
      overflow-y: auto;
      font-size: 0.72rem;
      color: var(--green-400);
      font-family: 'IBM Plex Mono', monospace;
      white-space: pre-wrap;
      scrollbar-width: thin;
      scrollbar-color: rgba(0,212,255,0.2) transparent;
    }

    .ws-table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 0.5rem;
      font-size: 0.72rem;
    }

    .ws-table th {
      color: var(--cyan-400);
      font-weight: 600;
      padding: 0.3rem 0.4rem;
      text-align: left;
      border-bottom: 1px solid rgba(0,212,255,0.15);
      font-family: 'Oxanium', sans-serif;
    }

    .ws-table td {
      padding: 0.28rem 0.4rem;
      border-bottom: 1px solid rgba(255,255,255,0.04);
    }

    /* ─── BUTTONS ─── */
    button {
      font-family: 'IBM Plex Mono', monospace;
      cursor: pointer;
      border: none;
      transition: all 0.15s ease;
      user-select: none;
    }

    .btn {
      display: inline-flex;
      align-items: center;
      gap: 0.45rem;
      padding: 0.65rem 1.1rem;
      border-radius: 10px;
      font-size: 0.78rem;
      font-weight: 600;
      border: 1px solid transparent;
    }

    .btn:hover { filter: brightness(1.08); transform: translateY(-1px); }
    .btn:active { transform: translateY(0); filter: brightness(0.95); }
    .btn:focus-visible { outline: none; box-shadow: var(--focus); }
    .btn[disabled] { opacity: 0.5; cursor: not-allowed; }
    .btn[disabled]:hover { filter: none; transform: none; }

    .btn-primary {
      background: linear-gradient(135deg, rgba(0,212,255,0.9), rgba(45,212,191,0.85));
      color: var(--navy-950);
      font-weight: 700;
    }

    .btn-secondary {
      background: rgba(0,212,255,0.1);
      border-color: rgba(0,212,255,0.35);
      color: var(--cyan-400);
    }

    .btn-success {
      background: linear-gradient(135deg, rgba(52,211,153,0.9), rgba(16,185,129,0.85));
      color: var(--navy-950);
      font-weight: 700;
    }

    .btn-ghost {
      background: rgba(255,255,255,0.04);
      border-color: rgba(255,255,255,0.12);
      color: var(--muted-bright);
    }

    .btn svg {
      width: 15px; height: 15px;
      stroke: currentColor;
      fill: none;
      stroke-width: 2;
      flex-shrink: 0;
    }

    /* ─── CTA BAR ─── */
    .cta-bar {
      display: flex;
      flex-wrap: wrap;
      gap: 0.6rem;
      justify-content: center;
      margin-top: 1rem;
      animation: fadeUp 0.7s 0.45s cubic-bezier(0.16,1,0.3,1) both;
    }

    .cta-bar .btn { padding: 0.75rem 1.3rem; font-size: 0.8rem; }

    /* ─── TOAST ─── */
    #toast-container {
      position: fixed;
      bottom: 1.5rem;
      right: 1.5rem;
      z-index: 9999;
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
      pointer-events: none;
    }

    .toast {
      display: flex;
      align-items: center;
      gap: 0.6rem;
      padding: 0.7rem 1rem;
      border-radius: 10px;
      background: rgba(10,22,40,0.97);
      border: 1px solid rgba(0,212,255,0.3);
      box-shadow: 0 8px 24px rgba(0,0,0,0.5);
      font-size: 0.78rem;
      color: var(--text);
      backdrop-filter: blur(12px);
      min-width: 240px;
      pointer-events: auto;
      animation: toastIn 0.35s cubic-bezier(0.16,1,0.3,1) both;
    }

    .toast.toast-exit { animation: toastOut 0.25s ease forwards; }

    @keyframes toastIn {
      from { opacity: 0; transform: translateX(30px); }
      to   { opacity: 1; transform: translateX(0); }
    }

    @keyframes toastOut {
      from { opacity: 1; transform: translateX(0); }
      to   { opacity: 0; transform: translateX(30px); }
    }

    .toast-dot {
      width: 8px; height: 8px;
      border-radius: 50%;
      flex-shrink: 0;
    }

    .toast-info  .toast-dot { background: var(--cyan-400); }
    .toast-success .toast-dot { background: var(--green-400); }
    .toast-warn  .toast-dot { background: var(--amber-400); }

    /* ─── FOOTER ─── */
    .footer {
      text-align: center;
      font-size: 0.65rem;
      color: var(--muted);
      margin-top: 1.5rem;
      padding: 1rem;
      border-top: 1px solid rgba(255,255,255,0.05);
      letter-spacing: 0.04em;
    }

    /* ─── SR ONLY ─── */
    .sr-only {
      position: absolute!important; width:1px; height:1px;
      padding:0; margin:-1px; overflow:hidden;
      clip:rect(0,0,0,0); white-space:nowrap; border:0;
    }

    /* ─── RESPONSIVE ─── */
    @media (max-width: 1200px) {
      .main-grid { grid-template-columns: 1fr; }
      .incidents-feed { height: 280px; }
    }

    @media (max-width: 800px) {
      .layout { padding: 1rem; }
      .metrics-grid { grid-template-columns: repeat(2,1fr); }
    }

    @media (max-width: 500px) {
      .metrics-grid { grid-template-columns: 1fr; }
      .cta-bar .btn { width: 100%; justify-content: center; }
    }
  </style>
</head>
<body>

<!-- Ocean background canvas -->
<canvas id="ocean-canvas"></canvas>

<!-- Toast container -->
<div id="toast-container" aria-live="polite" aria-atomic="false"></div>

<div class="layout">

  <!-- HEADER -->
  <header class="header">
    <div class="header-brand">
      <div class="logo-ring">
        <svg viewBox="0 0 40 40" role="img" aria-label="OceanCentinell logo">
          <defs>
            <linearGradient id="tG" x1="0" y1="0" x2="0" y2="1">
              <stop offset="0%" stop-color="#e8f4fd"/>
              <stop offset="100%" stop-color="#64748b"/>
            </linearGradient>
            <radialGradient id="lG" cx="0.5" cy="0.2" r="0.8">
              <stop offset="0%" stop-color="#00d4ff" stop-opacity="0.9"/>
              <stop offset="100%" stop-color="#00d4ff" stop-opacity="0"/>
            </radialGradient>
          </defs>
          <rect x="2" y="27" width="36" height="9" rx="4" fill="rgba(0,212,255,0.15)"/>
          <path d="M20 10 L38 16 L20 22 Z" fill="url(#lG)" opacity="0.9"/>
          <rect x="17" y="14" width="6" height="15" rx="1.5" fill="url(#tG)"/>
          <rect x="16" y="12" width="8" height="3" rx="1" fill="#a5f3fc"/>
          <polygon points="15,12 25,12 20,8" fill="#0e7490"/>
        </svg>
      </div>
      <div class="brand-text">
        <h1>OceanCentinell ENTERPRISE</h1>
        <p>Integrated maritime cyber · Fleets · Ports · Offshore</p>
      </div>
    </div>
    <div class="header-right">
      <div class="live-badge">
        <span class="live-dot"></span>
        Live monitoring
      </div>
      <div class="header-clock" id="clockEl">--:--:--</div>
    </div>
  </header>

  <!-- PLAN TABS -->
  <div class="plan-strip" role="group" aria-label="Commercial plans">
    <button class="plan-tab active" data-plan="starter" type="button">
      <div class="plan-tab-name">Fleet Starter</div>
      <div class="plan-tab-desc">Hasta 25 embarcaciones · Una región</div>
    </button>
    <button class="plan-tab" data-plan="advanced" type="button">
      <div class="plan-tab-name">Port & Offshore Advanced</div>
      <div class="plan-tab-desc">Puertos, terminales y clusters offshore</div>
    </button>
    <button class="plan-tab" data-plan="enterprise" type="button">
      <div class="plan-tab-name">Enterprise 360</div>
      <div class="plan-tab-desc">Multi-flota · Multi-región · Governance</div>
    </button>
  </div>

  <!-- MAIN GRID -->
  <div class="main-grid">

    <!-- LEFT: METRICS + STATUS -->
    <div class="card" aria-label="Métricas clave">
      <div class="section-label">Métricas en tiempo real</div>

      <div class="metrics-grid" role="group">
        <button class="metric-card" type="button" data-key="risk">
          <div class="metric-icon-wrap">
            <svg viewBox="0 0 24 24"><path d="M12 3l7 3v5c0 4.2-2.7 8-7 9-4.3-1-7-4.8-7-9V6l7-3z"/></svg>
          </div>
          <div class="metric-value" id="riskScore">–</div>
          <div class="metric-label">Risk Index</div>
          <div class="metric-delta" id="riskDelta"></div>
        </button>

        <button class="metric-card" type="button" data-key="assets">
          <div class="metric-icon-wrap">
            <svg viewBox="0 0 24 24"><path d="M3 17l3 3h12l3-3-6-2-3 1-3-1-6 2z"/><path d="M6 10l6-3 6 3-1 3H7l-1-3z"/><path d="M12 4v3"/></svg>
          </div>
          <div class="metric-value" id="assetsCount">–</div>
          <div class="metric-label">Activos</div>
          <div class="metric-delta" id="assetsDelta"></div>
        </button>

        <button class="metric-card" type="button" data-key="uptime">
          <div class="metric-icon-wrap">
            <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="8"/><path d="M12 8v4l3 2"/></svg>
          </div>
          <div class="metric-value" id="uptimeMetric">–</div>
          <div class="metric-label">Uptime</div>
          <div class="metric-delta" id="uptimeDelta"></div>
        </button>

        <button class="metric-card" type="button" data-key="eps">
          <div class="metric-icon-wrap">
            <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="8"/><circle cx="12" cy="12" r="3"/><path d="M12 12L18 6"/></svg>
          </div>
          <div class="metric-value" id="epsMetric">–</div>
          <div class="metric-label">EPS</div>
          <div class="metric-delta" id="epsDelta"></div>
        </button>
      </div>

      <!-- Sparkline -->
      <div class="sparkline-wrap">
        <div class="sparkline-header">
          <span class="sparkline-title">Historial Risk Index (últimas 30 lecturas)</span>
          <span id="sparkLabel" style="color:var(--cyan-400);font-weight:600;"></span>
        </div>
        <canvas id="sparkline"></canvas>
      </div>

      <!-- Detail panel -->
      <div class="metric-detail-panel" id="detailPanel" aria-live="polite">
        <div class="detail-icon" id="detailIconWrap">
          <svg id="detailIcon" viewBox="0 0 24 24"><path d="M12 3l7 3v5c0 4.2-2.7 8-7 9-4.3-1-7-4.8-7-9V6l7-3z"/></svg>
        </div>
        <div>
          <div class="detail-text-title" id="detailTitle">Risk Index</div>
          <div class="detail-text-body" id="detailBody">Selecciona una métrica para ver información ejecutiva.</div>
        </div>
      </div>

      <!-- Mini dash -->
      <div class="mini-dash" id="miniDash"></div>

      <!-- Status row -->
      <div class="status-row">
        <div class="status-pill">
          <span class="live-dot" id="autoDot" style="background:var(--muted);box-shadow:none;animation:none;width:7px;height:7px;border-radius:50%;"></span>
          <span id="autoText">Auto: –</span>
        </div>
        <div class="status-pill">
          Plan: <strong id="planPill">–</strong>
        </div>
        <div class="status-pill">
          Actualizado: <strong id="lastUpdate">–</strong>
        </div>
        <div class="status-pill">
          Buffer: <strong id="bufferCount">0</strong>
        </div>
        <div class="status-pill">
          Incidentes: <strong id="incidentCounter">0</strong>
        </div>
      </div>
    </div>

    <!-- RIGHT: THREATS -->
    <div class="card" aria-label="Amenazas activas">
      <div class="threats-header">
        <div class="threats-title">Amenazas Activas</div>
        <div class="filter-pills" role="group" aria-label="Filtrar por severidad">
          <button class="filter-pill active" data-filter="all" type="button">Todo</button>
          <button class="filter-pill fp-low" data-filter="LOW" type="button">Low</button>
          <button class="filter-pill fp-medium" data-filter="MEDIUM" type="button">Med</button>
          <button class="filter-pill fp-high" data-filter="HIGH" type="button">High</button>
          <button class="filter-pill fp-critical" data-filter="CRITICAL" type="button">Crit</button>
        </div>
      </div>

      <div class="legend" aria-hidden="true">
        <div class="legend-item"><span class="legend-dot" style="background:var(--green-400)"></span>Low</div>
        <div class="legend-item"><span class="legend-dot" style="background:var(--amber-400)"></span>Medium</div>
        <div class="legend-item"><span class="legend-dot" style="background:var(--red-400)"></span>High</div>
        <div class="legend-item"><span class="legend-dot" style="background:var(--rose-400)"></span>Critical</div>
        <span style="margin-left:auto;font-size:0.62rem;color:var(--muted)">Demo simulado · Sin datos reales</span>
      </div>

      <div class="incidents-feed" id="incidentsFeed">
        <p style="color:var(--muted);font-size:0.78rem;">Esperando datos...</p>
      </div>

      <p class="sr-only" id="srAnnounce" aria-live="polite" aria-atomic="true"></p>
    </div>
  </div>

  <!-- WORKSPACE -->
  <div class="card workspace" aria-label="Workspace operacional">
    <div class="ws-header">
      <div>
        <div class="ws-title" id="wsTitle">Ejecución · Fleet Registry</div>
        <div class="ws-subtitle" id="wsSubtitle">Vincula el alcance comercial a la ejecución operacional en flotas, puertos y tenants offshore.</div>
      </div>
      <span style="font-size:0.68rem;color:var(--muted)">Agnóstico por región · Tenant-aware · Nivel de junta directiva</span>
    </div>

    <div class="ws-tabs" role="tablist">
      <button class="ws-tab" role="tab" aria-selected="true" data-page="fleet">1 · Fleet Registry</button>
      <button class="ws-tab" role="tab" aria-selected="false" data-page="satcom">2 · SatCom</button>
      <button class="ws-tab" role="tab" aria-selected="false" data-page="vhf">3 · VHF Guard</button>
      <button class="ws-tab" role="tab" aria-selected="false" data-page="ais">4 · AIS Integrity</button>
      <button class="ws-tab" role="tab" aria-selected="false" data-page="endpoints">5 · Endpoints</button>
      <button class="ws-tab" role="tab" aria-selected="false" data-page="access">6 · Acceso</button>
      <button class="ws-tab" role="tab" aria-selected="false" data-page="drills">7 · Simulacros</button>
      <button class="ws-tab" role="tab" aria-selected="false" data-page="geofence">8 · Geo-Fences</button>
      <button class="ws-tab" role="tab" aria-selected="false" data-page="compliance">9 · Compliance</button>
      <button class="ws-tab" role="tab" aria-selected="false" data-page="failover">10 · Failover</button>
    </div>

    <!-- Fleet -->
    <div class="ws-panel" data-page="fleet">
      <div class="ws-panel-title">Registro de embarcaciones (pesca y servicio)</div>
      <div class="ws-form-row">
        <label>Nombre del buque<input id="fleetName" placeholder="ej. F/V Victoria"/></label>
        <label>MMSI / Indicativo<input id="fleetId" placeholder="ej. 123456789"/></label>
        <label>Rol<select id="fleetRole">
          <option value="fishing">Pesca</option>
          <option value="service">Servicio / apoyo</option>
          <option value="research">Investigación</option>
        </select></label>
      </div>
      <div class="ws-actions">
        <button class="btn btn-primary" id="btnAddVessel" type="button">
          <svg viewBox="0 0 24 24"><path d="M12 5v14M5 12h14"/></svg>Agregar buque
        </button>
        <button class="btn btn-ghost" id="btnClearFleet" type="button">Limpiar lista</button>
      </div>
      <table class="ws-table" id="fleetTable">
        <thead><tr><th>Buque</th><th>ID</th><th>Rol</th><th>Registrado</th></tr></thead>
        <tbody></tbody>
      </table>
    </div>

    <!-- SatCom -->
    <div class="ws-panel" data-page="satcom" hidden>
      <div class="ws-panel-title">Salud de comunicaciones satelitales</div>
      <div class="ws-form-row">
        <label>Perfil de enlace<select id="satProfile">
          <option value="basic">Flota básica (banda L)</option>
          <option value="enterprise">Flota enterprise (banda Ku)</option>
          <option value="resilient">Perfil alta resiliencia</option>
        </select></label>
        <label>Buque objetivo<input id="satVessel" placeholder="Cualquier buque registrado"/></label>
      </div>
      <div class="ws-actions">
        <button class="btn btn-primary" id="btnSatHealth" type="button">
          <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="3"/><path d="M6.3 6.3a8 8 0 000 11.4M17.7 6.3a8 8 0 010 11.4"/></svg>Check de salud
        </button>
        <button class="btn btn-ghost" id="btnSatBaseline" type="button">Actualizar baseline</button>
      </div>
      <div class="ws-log" id="satLog">Esperando pruebas SatCom…</div>
    </div>

    <!-- VHF -->
    <div class="ws-panel" data-page="vhf" hidden>
      <div class="ws-panel-title">Guardia de canal VHF/UHF</div>
      <div class="ws-form-row">
        <label><input type="checkbox" class="vhf-ch" value="16" checked/> Canal 16 (socorro)</label>
        <label><input type="checkbox" class="vhf-ch" value="70"/> Canal DSC 70</label>
        <label><input type="checkbox" class="vhf-ch" value="13"/> Maniobra Ch 13</label>
        <label><input type="checkbox" class="vhf-ch" value="Custom"/> Canal operaciones</label>
      </div>
      <div class="ws-actions">
        <button class="btn btn-primary" id="btnApplyVhf" type="button">Aplicar política VHF</button>
      </div>
      <div class="ws-log" id="vhfLog">Sin política VHF aplicada.</div>
    </div>

    <!-- AIS -->
    <div class="ws-panel" data-page="ais" hidden>
      <div class="ws-panel-title">Integridad AIS y seguimiento</div>
      <div class="ws-chips">
        <span class="ws-chip">Detección de spoofing</span>
        <span class="ws-chip">Buques silenciosos</span>
        <span class="ws-chip">Encuentros inesperados</span>
        <span class="ws-chip">Anomalías de posición</span>
      </div>
      <div class="ws-actions">
        <button class="btn btn-primary" id="btnAisScan" type="button">
          <svg viewBox="0 0 24 24"><path d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/></svg>Escanear AIS
        </button>
      </div>
      <div class="ws-log" id="aisLog">Sin escaneo AIS ejecutado.</div>
    </div>

    <!-- Endpoints -->
    <div class="ws-panel" data-page="endpoints" hidden>
      <div class="ws-panel-title">Salud de endpoints a bordo</div>
      <div class="ws-form-row">
        <label>Grupo<select id="epGroup">
          <option value="bridge">Sistemas de puente</option>
          <option value="engineering">Sala de máquinas</option>
          <option value="fleet">Toda la flota</option>
        </select></label>
        <label>Profundidad<select id="epDepth">
          <option value="quick">Check rápido</option>
          <option value="full">Escaneo completo</option>
        </select></label>
      </div>
      <div class="ws-actions">
        <button class="btn btn-primary" id="btnEpScan" type="button">
          <svg viewBox="0 0 24 24"><path d="M9 3H5a2 2 0 00-2 2v14a2 2 0 002 2h14a2 2 0 002-2V9l-6-6z"/><path d="M9 3v6h6"/></svg>Ejecutar escaneo
        </button>
      </div>
      <div class="ws-log" id="epLog">Sin escaneos ejecutados.</div>
    </div>

    <!-- Access -->
    <div class="ws-panel" data-page="access" hidden>
      <div class="ws-panel-title">Control de acceso y MFA de tripulación</div>
      <div class="ws-form-row">
        <label>Política de contraseñas<select id="accPolicy">
          <option value="standard">Estándar (12 chars)</option>
          <option value="strong">Fuerte (16 chars, símbolos)</option>
          <option value="hardened">Reforzada (20 chars, rotación)</option>
        </select></label>
        <label>Alcance MFA<select id="accMfa">
          <option value="bridge-only">Solo consolas de puente</option>
          <option value="all-crew">Toda la tripulación</option>
          <option value="contractors">Contratistas y remotos</option>
        </select></label>
      </div>
      <div class="ws-actions">
        <button class="btn btn-primary" id="btnApplyAccess" type="button">
          <svg viewBox="0 0 24 24"><path d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"/></svg>Aplicar política
        </button>
      </div>
      <div class="ws-log" id="accLog">Sin cambios de política pendientes.</div>
    </div>

    <!-- Drills -->
    <div class="ws-panel" data-page="drills" hidden>
      <div class="ws-panel-title">Simulacros de incidentes cibernéticos</div>
      <div class="ws-form-row">
        <label>Escenario<select id="drillScenario">
          <option value="phishing">Phishing contra capitán</option>
          <option value="ransomware">Ransomware en PC de puente</option>
          <option value="gps-jam">GPS jamming cerca de caladeros</option>
        </select></label>
        <label>Buque objetivo<input id="drillVessel" placeholder="Nombre del buque (opcional)"/></label>
      </div>
      <div class="ws-actions">
        <button class="btn btn-primary" id="btnLaunchDrill" type="button">
          <svg viewBox="0 0 24 24"><path d="M13 10V3L4 14h7v7l9-11h-7z"/></svg>Lanzar simulacro
        </button>
      </div>
      <div class="ws-log" id="drillLog">Sin simulacros lanzados.</div>
    </div>

    <!-- Geo-fences -->
    <div class="ws-panel" data-page="geofence" hidden>
      <div class="ws-panel-title">Geo-cercas operacionales</div>
      <div class="ws-form-row">
        <label>Nombre de la cerca<input id="geoName" placeholder="ej. Caladero A"/></label>
        <label>Radio (NM)<input id="geoRadius" type="number" min="1" max="500" value="25"/></label>
      </div>
      <div class="ws-actions">
        <button class="btn btn-primary" id="btnApplyGeo" type="button">
          <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="3"/><path d="M12 2v3M12 19v3M2 12h3M19 12h3"/></svg>Aplicar geo-cerca
        </button>
      </div>
      <div class="ws-log" id="geoLog">Sin geo-cercas configuradas.</div>
    </div>

    <!-- Compliance -->
    <div class="ws-panel" data-page="compliance" hidden>
      <div class="ws-panel-title">Retención de logs y perfil de compliance</div>
      <div class="ws-form-row">
        <label>Retención (días)<input id="cmpRetention" type="number" min="7" max="365" value="180"/></label>
        <label>Perfil<select id="cmpProfile">
          <option value="baseline">Baseline fleet</option>
          <option value="iso">ISO 27001 marítimo</option>
          <option value="extended">Archivo extendido</option>
        </select></label>
      </div>
      <div class="ws-actions">
        <button class="btn btn-primary" id="btnSaveCompliance" type="button">
          <svg viewBox="0 0 24 24"><path d="M19 21H5a2 2 0 01-2-2V5a2 2 0 012-2h11l5 5v11a2 2 0 01-2 2z"/><path d="M17 21v-8H7v8M7 3v5h8"/></svg>Guardar perfil
        </button>
      </div>
      <div class="ws-log" id="cmpLog">Sin perfil de compliance guardado.</div>
    </div>

    <!-- Failover -->
    <div class="ws-panel" data-page="failover" hidden>
      <div class="ws-panel-title">Failover de comunicaciones de emergencia</div>
      <div class="ws-form-row">
        <label>Enlace principal<select id="foPrimary">
          <option value="satcom">Proveedor SatCom</option>
          <option value="shore">Red radio costera</option>
        </select></label>
        <label>Enlace de respaldo<select id="foBackup">
          <option value="cellular">4G/5G costero</option>
          <option value="hf">Radio HF</option>
          <option value="alt-sat">SatCom alternativo</option>
        </select></label>
      </div>
      <div class="ws-actions">
        <button class="btn btn-primary" id="btnTestFailover" type="button">
          <svg viewBox="0 0 24 24"><path d="M4 4v6h6"/><path d="M5 13a7 7 0 0012 3"/><path d="M20 11V5h-6"/><path d="M19 11a7 7 0 00-12-3"/></svg>Probar failover
        </button>
      </div>
      <div class="ws-log" id="foLog">Sin prueba de failover ejecutada.</div>
    </div>
  </div>

  <!-- CTA BAR -->
  <div class="cta-bar" role="group">
    <button class="btn btn-primary" id="ctaProposal" type="button">
      <svg viewBox="0 0 24 24"><path d="M4 4v6h6"/><path d="M5 13a7 7 0 0012 3"/></svg>
      Solicitar Propuesta Enterprise
    </button>
    <button class="btn btn-secondary" id="ctaDemo" type="button">
      <svg viewBox="0 0 24 24"><path d="M4 4h16v4H4z"/><path d="M4 10h16v10H4z"/><path d="M8 2v4M16 2v4"/></svg>
      Agendar Demo Técnico
    </button>
    <button class="btn btn-ghost" id="ctaSales" type="button">
      <svg viewBox="0 0 24 24"><path d="M4 5h16v9H5l-1 4z"/></svg>
      Hablar con Ventas
    </button>
    <button class="btn btn-success" id="exportBtn" type="button">
      <svg viewBox="0 0 24 24"><path d="M12 3v12M8 7l4-4 4 4M5 14v4a2 2 0 002 2h10a2 2 0 002-2v-4"/></svg>
      Exportar Briefing Ejecutivo
    </button>
  </div>

  <footer class="footer">
    OceanCentinell · División de CentinellSuite Defense · Operado por Victoria en Cristo Jesús LLC · Todos los derechos reservados · Creado el 19 de febrero de 2026
  </footer>

</div>

<script>
(() => {
  "use strict";

  /* ── OCEAN CANVAS BACKGROUND ── */
  const canvas = document.getElementById('ocean-canvas');
  const ctx = canvas.getContext('2d');
  let W, H;
  function resizeCanvas() {
    W = canvas.width = window.innerWidth;
    H = canvas.height = window.innerHeight;
  }
  resizeCanvas();
  window.addEventListener('resize', resizeCanvas);

  const waves = [
    { amp: 28, period: 0.006, speed: 0.0008, phase: 0,   color: 'rgba(0,212,255,0.04)' },
    { amp: 18, period: 0.009, speed: 0.0012, phase: 2.1, color: 'rgba(45,212,191,0.035)' },
    { amp: 12, period: 0.013, speed: 0.0018, phase: 4.5, color: 'rgba(0,212,255,0.025)' },
  ];

  let raf;
  function drawOcean(t) {
    ctx.clearRect(0, 0, W, H);
    waves.forEach(w => {
      w.phase += w.speed;
      ctx.beginPath();
      ctx.moveTo(0, H * 0.65);
      for (let x = 0; x <= W; x += 3) {
        const y = H * 0.65 + Math.sin(x * w.period + w.phase) * w.amp
                             + Math.sin(x * w.period * 1.7 + w.phase * 0.8) * (w.amp * 0.4);
        ctx.lineTo(x, y);
      }
      ctx.lineTo(W, H); ctx.lineTo(0, H); ctx.closePath();
      ctx.fillStyle = w.color;
      ctx.fill();
    });
    raf = requestAnimationFrame(drawOcean);
  }
  drawOcean(0);

  /* ── CLOCK ── */
  const clockEl = document.getElementById('clockEl');
  function updateClock() {
    const now = new Date();
    clockEl.textContent = now.toLocaleTimeString(undefined, { hour12: false });
  }
  setInterval(updateClock, 1000);
  updateClock();

  /* ── TOAST ── */
  function toast(msg, type = 'info') {
    const c = document.getElementById('toast-container');
    const el = document.createElement('div');
    el.className = `toast toast-${type}`;
    el.innerHTML = `<span class="toast-dot"></span><span>${msg}</span>`;
    c.appendChild(el);
    setTimeout(() => {
      el.classList.add('toast-exit');
      setTimeout(() => el.remove(), 300);
    }, 3200);
  }

  /* ── SPARKLINE ── */
  const sparkCanvas = document.getElementById('sparkline');
  const sparkCtx = sparkCanvas.getContext('2d');
  const sparkHistory = [];
  const SPARK_MAX = 30;

  function drawSparkline() {
    const dpr = window.devicePixelRatio || 1;
    const rect = sparkCanvas.getBoundingClientRect();
    sparkCanvas.width = rect.width * dpr;
    sparkCanvas.height = rect.height * dpr;
    sparkCtx.scale(dpr, dpr);
    const W = rect.width, H = rect.height;

    sparkCtx.clearRect(0, 0, W, H);
    if (sparkHistory.length < 2) return;

    const min = Math.min(...sparkHistory);
    const max = Math.max(...sparkHistory);
    const range = max - min || 1;

    const pts = sparkHistory.map((v, i) => ({
      x: (i / (sparkHistory.length - 1)) * W,
      y: H - ((v - min) / range) * (H - 6) - 3
    }));

    // Gradient fill
    const grad = sparkCtx.createLinearGradient(0, 0, 0, H);
    grad.addColorStop(0, 'rgba(0,212,255,0.25)');
    grad.addColorStop(1, 'rgba(0,212,255,0)');
    sparkCtx.beginPath();
    sparkCtx.moveTo(pts[0].x, H);
    pts.forEach(p => sparkCtx.lineTo(p.x, p.y));
    sparkCtx.lineTo(pts[pts.length-1].x, H);
    sparkCtx.closePath();
    sparkCtx.fillStyle = grad;
    sparkCtx.fill();

    // Line
    sparkCtx.beginPath();
    pts.forEach((p, i) => i === 0 ? sparkCtx.moveTo(p.x, p.y) : sparkCtx.lineTo(p.x, p.y));
    sparkCtx.strokeStyle = 'rgba(0,212,255,0.8)';
    sparkCtx.lineWidth = 1.5;
    sparkCtx.stroke();

    // Last dot
    const last = pts[pts.length-1];
    sparkCtx.beginPath();
    sparkCtx.arc(last.x, last.y, 3, 0, Math.PI*2);
    sparkCtx.fillStyle = '#00d4ff';
    sparkCtx.fill();
  }

  /* ── SIEM ── */
  const PLANS = {
    starter:    { label: 'Fleet Starter' },
    advanced:   { label: 'Port & Offshore Advanced' },
    enterprise: { label: 'Enterprise 360' },
  };
  let ACTIVE_PLAN = 'starter';

  const fmtTime = new Intl.DateTimeFormat(undefined, {
    hour: '2-digit', minute: '2-digit', second: '2-digit'
  });

  function riskBucket(score) {
    if (score >= 90) return 'CRITICAL';
    if (score >= 75) return 'HIGH';
    if (score >= 50) return 'MEDIUM';
    return 'LOW';
  }

  const incidents = [];
  let metrics = {};
  let activeVessel = null;
  let filterSev = 'all';
  let prevMetrics = {};
  let totalIncidentsEver = 0;

  function updateMetrics() {
    prevMetrics = { ...metrics };
    const risk = +(20 + Math.random()*78).toFixed(1);
    metrics = {
      risk_score: risk,
      assets: Math.floor(20 + Math.random()*220),
      uptime: +(99 + Math.random()*0.9).toFixed(2),
      eps: Math.floor(3000 + Math.random()*5000),
      risk_level: riskBucket(risk),
      updated_at: new Date()
    };
    sparkHistory.push(risk);
    if (sparkHistory.length > SPARK_MAX) sparkHistory.shift();
  }

  function appendIncidents() {
    const vectors = ['Phishing','Port Scan','Malware Beacon','Ransomware','Brute Force','DDoS'];
    const regions = ['Zona Operacional Alpha','Zona Operacional Bravo','Sector Offshore 1','Sector Portuario 2'];
    const assetNames = ['Bridge Server','NavCom','Radar Host','AIS Node','Fleet Gateway'];
    const sevs = ['LOW','MEDIUM','HIGH','CRITICAL'];
    const batch = 2 + Math.floor(Math.random()*4);
    totalIncidentsEver += batch;
    const now = Date.now();
    const items = [];
    for (let i = 0; i < batch; i++) {
      items.push({
        id: 'INC-' + (1000 + Math.floor(Math.random()*9000)),
        risk: sevs[Math.floor(Math.random()*sevs.length)],
        vector: vectors[Math.floor(Math.random()*vectors.length)],
        region: regions[Math.floor(Math.random()*regions.length)],
        asset: assetNames[Math.floor(Math.random()*assetNames.length)],
        vessel: activeVessel || 'Cualquier buque registrado',
        timestamp: new Date(now - Math.floor(Math.random()*300000)).toISOString()
      });
    }
    incidents.unshift(...items);
    if (incidents.length > 60) incidents.length = 60;
  }

  function renderMetrics() {
    const m = metrics;
    const rs = document.getElementById('riskScore');
    rs.textContent = m.risk_score != null ? m.risk_score.toFixed(1) : '–';
    rs.className = 'metric-value';
    const rl = (m.risk_level || '').toLowerCase();
    if (rl === 'low') rs.classList.add('risk-low');
    else if (rl === 'medium') rs.classList.add('risk-medium');
    else if (rl === 'high') rs.classList.add('risk-high');
    else if (rl === 'critical') rs.classList.add('risk-crit');

    document.getElementById('assetsCount').textContent = m.assets ?? '–';
    document.getElementById('uptimeMetric').textContent = m.uptime != null ? m.uptime.toFixed(2) + '%' : '–';
    document.getElementById('epsMetric').textContent = m.eps != null ? (m.eps/1000).toFixed(1)+'K' : '–';

    // Deltas
    function delta(cur, prev, unit='') {
      if (prev == null || cur == null) return '';
      const d = cur - prev;
      if (Math.abs(d) < 0.01) return '';
      return (d > 0 ? '▲ +' : '▼ ') + Math.abs(d).toFixed(1) + unit;
    }
    document.getElementById('riskDelta').textContent = delta(m.risk_score, prevMetrics.risk_score);
    document.getElementById('assetsDelta').textContent = delta(m.assets, prevMetrics.assets);
    document.getElementById('uptimeDelta').textContent = delta(m.uptime, prevMetrics.uptime, '%');
    document.getElementById('epsDelta').textContent = delta(m.eps ? m.eps/1000 : null, prevMetrics.eps ? prevMetrics.eps/1000 : null, 'K');

    document.getElementById('lastUpdate').textContent = m.updated_at ? fmtTime.format(m.updated_at) : '–';
    document.getElementById('bufferCount').textContent = incidents.length;
    document.getElementById('incidentCounter').textContent = totalIncidentsEver;
    document.getElementById('planPill').textContent = PLANS[ACTIVE_PLAN].label;

    drawSparkline();
    document.getElementById('sparkLabel').textContent = m.risk_score != null ? m.risk_score.toFixed(1) + ' ' + (m.risk_level || '') : '';
  }

  function renderIncidents() {
    const feed = document.getElementById('incidentsFeed');
    const filtered = filterSev === 'all' ? incidents : incidents.filter(i => i.risk === filterSev);
    if (!filtered.length) {
      feed.innerHTML = '<p style="color:var(--muted);font-size:0.78rem;">Sin incidentes para mostrar.</p>';
      return;
    }
    const frag = document.createDocumentFragment();
    for (const inc of filtered) {
      const card = document.createElement('div');
      const riskLow = inc.risk.toLowerCase();
      card.className = `incident-card sev-${riskLow}`;
      card.innerHTML = `
        <div class="inc-header">
          <span class="inc-id">${inc.id}</span>
          <span class="risk-badge ${riskLow}">${inc.risk}</span>
        </div>
        <div class="inc-tags">
          <span class="inc-tag">${inc.vector}</span>
          <span class="inc-tag">${inc.asset}</span>
          <span class="inc-tag">${inc.region}</span>
        </div>
        <div class="inc-meta">${fmtTime.format(new Date(inc.timestamp))} · ${inc.vessel}</div>
      `;
      frag.appendChild(card);
    }
    feed.replaceChildren(frag);
  }

  function refresh() {
    updateMetrics();
    appendIncidents();
    renderMetrics();
    renderIncidents();
    if (activeMetricKey) updateDetailPanel(activeMetricKey);
  }

  /* ── AUTO REFRESH ── */
  let timer = null;
  function startAuto() {
    const dot = document.getElementById('autoDot');
    dot.style.background = 'var(--green-400)';
    dot.style.animation = 'ping 1.5s ease-out infinite';
    dot.style.boxShadow = '0 0 0 0 rgba(52,211,153,0.6)';
    document.getElementById('autoText').textContent = 'Auto: ON';
    timer = setInterval(() => {
      refresh();
    }, 4000);
  }

  /* ── METRIC DETAIL ── */
  let activeMetricKey = null;

  const METRIC_DEFS = {
    risk:   { title: 'Risk Index', icon: '<path d="M12 3l7 3v5c0 4.2-2.7 8-7 9-4.3-1-7-4.8-7-9V6l7-3z"/>' },
    assets: { title: 'Activos Protegidos', icon: '<path d="M3 17l3 3h12l3-3-6-2-3 1-3-1-6 2z"/><path d="M6 10l6-3 6 3-1 3H7l-1-3z"/><path d="M12 4v3"/>' },
    uptime: { title: 'Uptime de Plataforma', icon: '<circle cx="12" cy="12" r="8"/><path d="M12 8v4l3 2"/>' },
    eps:    { title: 'Eventos por Segundo', icon: '<circle cx="12" cy="12" r="8"/><circle cx="12" cy="12" r="3"/><path d="M12 12L18 6"/>' },
  };

  const METRIC_TEXT = {
    risk:   m => `Índice de riesgo cibernético a nivel de junta directiva. Score actual: ${m.risk_score != null ? m.risk_score.toFixed(1) : '–'} (${m.risk_level || '–'}).`,
    assets: m => `Activos marítimos críticos bajo monitoreo continuo. Total en scope: ${m.assets ?? '–'}.`,
    uptime: m => `Disponibilidad de la plataforma OceanCentinell en todos los tenants. Uptime actual: ${m.uptime != null ? m.uptime.toFixed(2) + '%' : '–'}.`,
    eps:    m => `Tasa de ingesta de telemetría de seguridad en flotas y puertos. EPS actual: ${m.eps ?? '–'} eventos/seg.`,
  };

  const METRIC_MINI = {
    risk(m, incs) {
      const score = m.risk_score ?? 0;
      const sev = { LOW:0, MEDIUM:0, HIGH:0, CRITICAL:0 };
      incs.slice(0,40).forEach(i => { if (sev[i.risk] != null) sev[i.risk]++; });
      const pct = Math.max(0, Math.min(100, score));
      return `
        <div class="mini-row"><span class="mini-label">Índice</span>
          <div class="mini-bar-track"><div class="mini-bar-fill" style="width:${pct}%"></div></div>
          <span class="mini-val">${score.toFixed(1)}</span></div>
        <div class="mini-row"><span class="mini-label">Low</span><span class="mini-val">${sev.LOW}</span></div>
        <div class="mini-row"><span class="mini-label">Medium</span><span class="mini-val">${sev.MEDIUM}</span></div>
        <div class="mini-row"><span class="mini-label">High</span><span class="mini-val">${sev.HIGH}</span></div>
        <div class="mini-row"><span class="mini-label">Critical</span><span class="mini-val">${sev.CRITICAL}</span></div>`;
    },
    assets(m) {
      const t = m.assets ?? 0;
      const g = Math.round(t * 0.85);
      const gap = t - g;
      const pct = t ? (g/t*100).toFixed(0) : 0;
      return `
        <div class="mini-row"><span class="mini-label">Total</span><span class="mini-val">${t}</span></div>
        <div class="mini-row"><span class="mini-label">Protegidos</span>
          <div class="mini-bar-track"><div class="mini-bar-fill" style="width:${pct}%"></div></div>
          <span class="mini-val">${g}</span></div>
        <div class="mini-row"><span class="mini-label">Gap</span><span class="mini-val">${gap}</span></div>`;
    },
    uptime(m) {
      const up = m.uptime ?? 0;
      const pct = Math.max(0, Math.min(100, up));
      const down = ((100-up)/100 * 30*24*60).toFixed(0);
      return `
        <div class="mini-row"><span class="mini-label">Uptime</span>
          <div class="mini-bar-track"><div class="mini-bar-fill" style="width:${pct}%"></div></div>
          <span class="mini-val">${up.toFixed(2)}%</span></div>
        <div class="mini-row"><span class="mini-label">Downtime est.</span><span class="mini-val">${down}m</span></div>`;
    },
    eps(m) {
      const eps = m.eps ?? 0;
      const cap = 8000;
      const pct = Math.max(0,Math.min(100,eps/cap*100)).toFixed(0);
      return `
        <div class="mini-row"><span class="mini-label">Actual</span>
          <div class="mini-bar-track"><div class="mini-bar-fill" style="width:${pct}%"></div></div>
          <span class="mini-val">${(eps/1000).toFixed(1)}K</span></div>
        <div class="mini-row"><span class="mini-label">Headroom</span><span class="mini-val">${cap-eps} EPS</span></div>
        <div class="mini-row"><span class="mini-label">Capacidad</span><span class="mini-val">${cap} EPS</span></div>`;
    },
  };

  const PAGE_FOR_METRIC = { risk:'fleet', assets:'fleet', uptime:'endpoints', eps:'satcom' };

  function updateDetailPanel(key) {
    const def = METRIC_DEFS[key];
    if (!def) return;
    document.getElementById('detailIcon').innerHTML = def.icon;
    document.getElementById('detailTitle').textContent = def.title;
    document.getElementById('detailBody').textContent = METRIC_TEXT[key](metrics);
    const mini = METRIC_MINI[key];
    document.getElementById('miniDash').innerHTML = mini ? mini(metrics, incidents) : '';
    document.querySelectorAll('.metric-card').forEach(c => c.classList.toggle('active', c.dataset.key === key));
    activateWsPage(PAGE_FOR_METRIC[key] || 'fleet');
    activeMetricKey = key;
  }

  document.querySelectorAll('.metric-card').forEach(card => {
    card.addEventListener('click', () => updateDetailPanel(card.dataset.key));
  });

  /* ── WORKSPACE TABS ── */
  function activateWsPage(pageId) {
    document.querySelectorAll('.ws-tab').forEach(t => {
      t.setAttribute('aria-selected', t.dataset.page === pageId ? 'true' : 'false');
    });
    document.querySelectorAll('.ws-panel').forEach(p => {
      p.hidden = p.dataset.page !== pageId;
    });
    const tab = document.querySelector(`.ws-tab[data-page="${pageId}"]`);
    if (tab) document.getElementById('wsTitle').textContent = 'Ejecución · ' + tab.textContent.replace(/^\d+ · /, '');
  }

  document.querySelectorAll('.ws-tab').forEach(tab => {
    tab.addEventListener('click', () => activateWsPage(tab.dataset.page));
  });

  /* ── PLAN BUTTONS ── */
  document.querySelectorAll('.plan-tab').forEach(btn => {
    btn.addEventListener('click', () => {
      ACTIVE_PLAN = btn.dataset.plan;
      document.querySelectorAll('.plan-tab').forEach(b => b.classList.toggle('active', b === btn));
      renderMetrics();
      toast(`Plan cambiado a ${PLANS[ACTIVE_PLAN].label}`, 'info');
    });
  });

  /* ── FILTER PILLS ── */
  document.querySelectorAll('.filter-pill').forEach(pill => {
    pill.addEventListener('click', () => {
      filterSev = pill.dataset.filter;
      document.querySelectorAll('.filter-pill').forEach(p => p.classList.toggle('active', p === pill));
      renderIncidents();
    });
  });

  /* ── FLEET REGISTRY ── */
  const fleetBody = document.querySelector('#fleetTable tbody');
  document.getElementById('btnAddVessel').addEventListener('click', () => {
    const name = document.getElementById('fleetName').value.trim();
    const id = document.getElementById('fleetId').value.trim();
    const role = document.getElementById('fleetRole').value;
    if (!name || !id) { toast('Completa nombre e ID del buque', 'warn'); return; }
    const tr = document.createElement('tr');
    tr.innerHTML = `<td>${name}</td><td>${id}</td><td>${role}</td><td>${fmtTime.format(new Date())}</td>`;
    fleetBody.appendChild(tr);
    if (!activeVessel) {
      activeVessel = name;
      document.getElementById('wsSubtitle').textContent = `Scope de ejecución: incidentes simulados enfocados en ${name}.`;
    }
    document.getElementById('fleetName').value = '';
    document.getElementById('fleetId').value = '';
    toast(`Buque "${name}" agregado al registro`, 'success');
  });

  document.getElementById('btnClearFleet').addEventListener('click', () => {
    fleetBody.replaceChildren();
    activeVessel = null;
    document.getElementById('wsSubtitle').textContent = 'Vincula el alcance comercial a la ejecución operacional.';
    toast('Lista de flota limpiada', 'info');
  });

  /* ── SATCOM ── */
  document.getElementById('btnSatHealth').addEventListener('click', () => {
    const profile = document.getElementById('satProfile').value;
    const vessel = document.getElementById('satVessel').value || (activeVessel || 'todos los buques');
    const latency = (400 + Math.random()*300).toFixed(0);
    const loss = (Math.random()*1.5).toFixed(2);
    document.getElementById('satLog').textContent =
      `[${fmtTime.format(new Date())}] Check SatCom en ${vessel} (${profile})\nLatencia: ${latency}ms · Pérdida: ${loss}%`;
    toast(`SatCom OK — Latencia ${latency}ms`, 'success');
  });
  document.getElementById('btnSatBaseline').addEventListener('click', () => {
    document.getElementById('satLog').textContent = `[${fmtTime.format(new Date())}] Baseline SatCom actualizado.`;
    toast('Baseline actualizado', 'info');
  });

  /* ── VHF ── */
  document.getElementById('btnApplyVhf').addEventListener('click', () => {
    const chks = Array.from(document.querySelectorAll('.vhf-ch:checked'));
    const list = chks.length ? chks.map(c => 'Ch'+c.value).join(', ') : 'ningún canal';
    document.getElementById('vhfLog').textContent = `[${fmtTime.format(new Date())}] Política VHF aplicada: ${list}`;
    toast('Política VHF aplicada', 'success');
  });

  /* ── AIS ── */
  document.getElementById('btnAisScan').addEventListener('click', () => {
    const anomalies = Math.floor(Math.random()*4);
    document.getElementById('aisLog').textContent =
      `[${fmtTime.format(new Date())}] Escaneo AIS completado.\nAnomalías detectadas: ${anomalies}`;
    toast(`AIS: ${anomalies} anomalía(s) detectada(s)`, anomalies > 0 ? 'warn' : 'success');
  });

  /* ── ENDPOINTS ── */
  document.getElementById('btnEpScan').addEventListener('click', () => {
    const group = document.getElementById('epGroup').value;
    const depth = document.getElementById('epDepth').value;
    document.getElementById('epLog').textContent =
      `[${fmtTime.format(new Date())}] Escaneo de endpoints "${depth}" lanzado para grupo "${group}" (simulado).`;
    toast('Escaneo de endpoints iniciado', 'info');
  });

  /* ── ACCESS ── */
  document.getElementById('btnApplyAccess').addEventListener('click', () => {
    const policy = document.getElementById('accPolicy').value;
    const mfa = document.getElementById('accMfa').value;
    document.getElementById('accLog').textContent =
      `[${fmtTime.format(new Date())}] Política "${policy}" con MFA scope "${mfa}" aplicada.`;
    toast('Política de acceso actualizada', 'success');
  });

  /* ── DRILLS ── */
  document.getElementById('btnLaunchDrill').addEventListener('click', () => {
    const scen = document.getElementById('drillScenario').value;
    const vessel = document.getElementById('drillVessel').value || (activeVessel || 'flota completa');
    document.getElementById('drillLog').textContent =
      `[${fmtTime.format(new Date())}] Simulacro lanzado: ${scen}\nObjetivo: ${vessel} (simulado)`;
    toast(`Simulacro "${scen}" iniciado`, 'warn');
  });

  /* ── GEO-FENCE ── */
  document.getElementById('btnApplyGeo').addEventListener('click', () => {
    const name = document.getElementById('geoName').value || 'Cerca sin nombre';
    const radius = document.getElementById('geoRadius').value || 25;
    document.getElementById('geoLog').textContent =
      `[${fmtTime.format(new Date())}] Geo-cerca "${name}" aplicada con radio ${radius} NM.`;
    toast(`Geo-cerca "${name}" configurada`, 'success');
  });

  /* ── COMPLIANCE ── */
  document.getElementById('btnSaveCompliance').addEventListener('click', () => {
    const days = document.getElementById('cmpRetention').value;
    const profile = document.getElementById('cmpProfile').value;
    document.getElementById('cmpLog').textContent =
      `[${fmtTime.format(new Date())}] Perfil "${profile}" guardado · Retención: ${days} días.`;
    toast('Perfil de compliance guardado', 'success');
  });

  /* ── FAILOVER ── */
  document.getElementById('btnTestFailover').addEventListener('click', () => {
    const primary = document.getElementById('foPrimary').value;
    const backup = document.getElementById('foBackup').value;
    const ok = Math.random() > 0.1;
    document.getElementById('foLog').textContent =
      `[${fmtTime.format(new Date())}] Failover ${primary} → ${backup}: ` +
      (ok ? 'EXITOSO (simulado).' : 'PROBLEMAS detectados — revisar configuración.');
    toast(ok ? `Failover exitoso: ${primary} → ${backup}` : 'Failover con problemas detectados', ok ? 'success' : 'warn');
  });

  /* ── CTAs ── */
  document.getElementById('ctaProposal').addEventListener('click', () => {
    window.location.href = 'mailto:sales@oceancentinell.com?subject=OceanCentinell%20Enterprise%20Proposal';
  });
  document.getElementById('ctaDemo').addEventListener('click', () => toast('Función de demo en desarrollo.', 'info'));
  document.getElementById('ctaSales').addEventListener('click', () => toast('Función de ventas en desarrollo.', 'info'));

  /* ── EXPORT ── */
  document.getElementById('exportBtn').addEventListener('click', () => {
    const plan = PLANS[ACTIVE_PLAN];
    const ts = new Date().toISOString();
    const report = {
      platform: 'OceanCentinell ENTERPRISE (Demo)',
      organization: 'Victoria en Cristo Jesús LLC',
      commercial_plan: plan.label,
      exported_at: ts,
      metrics,
      total_incidents_session: totalIncidentsEver,
      incidents,
    };
    const blob = new Blob([JSON.stringify(report, null, 2)], { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `OceanCentinell_${plan.label.replace(/\s/g,'_')}_${ts.slice(0,10)}.json`;
    document.body.appendChild(a);
    a.click();
    a.remove();
    setTimeout(() => URL.revokeObjectURL(url), 1500);
    toast('Briefing ejecutivo exportado', 'success');
  });

  /* ── INIT ── */
  refresh();
  startAuto();
  setTimeout(() => {
    updateDetailPanel('risk');
    activateWsPage('fleet');
  }, 800);

})();
</script>
</body>
</html>
