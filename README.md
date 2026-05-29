<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Bakery Agent — Abstract</title>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500;600&family=Space+Grotesk:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#0a0c0f;
  --bg2:#0f1218;
  --bg3:#141820;
  --border:#1e2530;
  --border2:#2a3342;
  --accent:#f59e0b;
  --accent2:#fbbf24;
  --green:#22c55e;
  --red:#ef4444;
  --blue:#3b82f6;
  --muted:#4b5563;
  --text:#e2e8f0;
  --text2:#94a3b8;
  --text3:#64748b;
  --mono:'IBM Plex Mono',monospace;
  --sans:'Space Grotesk',sans-serif;
  --radius:8px;
}
body{background:var(--bg);color:var(--text);font-family:var(--sans);min-height:100vh;overflow-x:hidden}

/* SCROLLBAR */
::-webkit-scrollbar{width:4px}
::-webkit-scrollbar-track{background:var(--bg)}
::-webkit-scrollbar-thumb{background:var(--border2);border-radius:2px}

/* LAYOUT */
.shell{display:grid;grid-template-columns:240px 1fr;min-height:100vh}

/* SIDEBAR */
.sidebar{background:var(--bg2);border-right:1px solid var(--border);display:flex;flex-direction:column;padding:0}
.logo{padding:20px 20px 16px;border-bottom:1px solid var(--border);display:flex;align-items:center;gap:10px}
.logo-icon{width:32px;height:32px;background:var(--accent);border-radius:6px;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0}
.logo-text{font-family:var(--mono);font-size:14px;font-weight:600;color:var(--accent);letter-spacing:0.05em}
.logo-sub{font-size:10px;color:var(--text3);font-family:var(--mono)}

.nav{padding:12px 8px;flex:1}
.nav-section{font-size:10px;font-family:var(--mono);color:var(--text3);padding:8px 12px 4px;letter-spacing:0.12em}
.nav-item{display:flex;align-items:center;gap:10px;padding:9px 12px;border-radius:var(--radius);cursor:pointer;font-size:13px;color:var(--text2);transition:all 0.15s;margin-bottom:1px}
.nav-item:hover{background:var(--bg3);color:var(--text)}
.nav-item.active{background:rgba(245,158,11,0.1);color:var(--accent);border:1px solid rgba(245,158,11,0.2)}
.nav-item .ni{font-size:16px;width:18px;text-align:center}
.nav-badge{margin-left:auto;background:var(--accent);color:#000;font-size:10px;font-family:var(--mono);padding:2px 6px;border-radius:999px;font-weight:600}
.nav-badge.green{background:var(--green)}
.nav-badge.red{background:var(--red)}

.sidebar-footer{padding:16px;border-top:1px solid var(--border)}
.wallet-card{background:var(--bg3);border:1px solid var(--border);border-radius:var(--radius);padding:12px}
.wallet-label{font-size:10px;font-family:var(--mono);color:var(--text3);margin-bottom:4px;letter-spacing:0.08em}
.wallet-addr{font-family:var(--mono);font-size:11px;color:var(--text2)}
.wallet-bal{font-family:var(--mono);font-size:13px;color:var(--accent);font-weight:600;margin-top:6px}

/* MAIN */
.main{overflow-y:auto;background:var(--bg)}
.topbar{display:flex;align-items:center;justify-content:space-between;padding:16px 24px;border-bottom:1px solid var(--border);background:var(--bg2);position:sticky;top:0;z-index:10}
.topbar-title{font-size:15px;font-weight:600;color:var(--text)}
.topbar-right{display:flex;align-items:center;gap:12px}
.status-pill{display:flex;align-items:center;gap:6px;padding:6px 12px;border-radius:999px;font-size:12px;font-family:var(--mono);cursor:pointer;border:1px solid}
.status-pill.running{border-color:rgba(34,197,94,0.3);background:rgba(34,197,94,0.08);color:var(--green)}
.status-pill.stopped{border-color:rgba(239,68,68,0.3);background:rgba(239,68,68,0.08);color:var(--red)}
.status-pill.idle{border-color:var(--border2);background:var(--bg3);color:var(--text3)}
.pulse{width:7px;height:7px;border-radius:50%;background:currentColor;animation:pulse 1.6s ease-in-out infinite}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:0.4;transform:scale(0.8)}}
.btn{padding:7px 14px;border-radius:var(--radius);font-size:12px;font-family:var(--mono);font-weight:500;cursor:pointer;transition:all 0.15s;border:1px solid}
.btn-primary{background:var(--accent);color:#000;border-color:var(--accent)}
.btn-primary:hover{background:var(--accent2)}
.btn-danger{background:transparent;color:var(--red);border-color:rgba(239,68,68,0.4)}
.btn-danger:hover{background:rgba(239,68,68,0.1)}
.btn-ghost{background:transparent;color:var(--text2);border-color:var(--border2)}
.btn-ghost:hover{border-color:var(--accent);color:var(--accent)}

.content{padding:24px}

/* STAT CARDS */
.stats-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:24px}
.stat-card{background:var(--bg2);border:1px solid var(--border);border-radius:10px;padding:16px;position:relative;overflow:hidden}
.stat-card::before{content:'';position:absolute;top:0;left:0;right:0;height:2px}
.stat-card.cookies::before{background:linear-gradient(90deg,var(--accent),transparent)}
.stat-card.score::before{background:linear-gradient(90deg,var(--blue),transparent)}
.stat-card.bakes::before{background:linear-gradient(90deg,var(--green),transparent)}
.stat-card.rank::before{background:linear-gradient(90deg,#a855f7,transparent)}
.stat-label{font-size:11px;font-family:var(--mono);color:var(--text3);margin-bottom:8px;letter-spacing:0.06em}
.stat-val{font-size:22px;font-weight:600;font-family:var(--mono);color:var(--text)}
.stat-val.cookies{color:var(--accent)}
.stat-val.bakes{color:var(--green)}
.stat-val.rank{color:#a855f7}
.stat-delta{font-size:11px;font-family:var(--mono);color:var(--text3);margin-top:4px}
.stat-delta.up{color:var(--green)}
.stat-delta.down{color:var(--red)}

/* TWO-COL LAYOUT */
.two-col{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-bottom:16px}
.three-col{display:grid;grid-template-columns:2fr 1fr;gap:16px;margin-bottom:16px}

/* PANEL */
.panel{background:var(--bg2);border:1px solid var(--border);border-radius:10px;overflow:hidden}
.panel-head{display:flex;align-items:center;justify-content:space-between;padding:14px 16px;border-bottom:1px solid var(--border)}
.panel-title{font-size:12px;font-family:var(--mono);font-weight:600;color:var(--text);letter-spacing:0.06em}
.panel-body{padding:16px}

/* AGENT CONTROLS */
.agent-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.toggle-row{display:flex;align-items:center;justify-content:space-between;padding:10px 12px;background:var(--bg3);border:1px solid var(--border);border-radius:var(--radius)}
.toggle-label{font-size:12px;font-family:var(--mono);color:var(--text2)}
.toggle{position:relative;width:40px;height:22px;cursor:pointer}
.toggle input{opacity:0;width:0;height:0}
.toggle-track{position:absolute;inset:0;background:var(--border2);border-radius:999px;transition:0.2s}
.toggle input:checked+.toggle-track{background:var(--accent)}
.toggle-thumb{position:absolute;top:3px;left:3px;width:16px;height:16px;background:#fff;border-radius:50%;transition:0.2s}
.toggle input:checked~.toggle-thumb{left:21px}
.toggle-row.disabled{opacity:0.4;pointer-events:none}

/* CONFIG ROWS */
.config-row{display:flex;align-items:center;justify-content:space-between;padding:10px 0;border-bottom:1px solid var(--border)}
.config-row:last-child{border-bottom:none;padding-bottom:0}
.config-key{font-size:12px;font-family:var(--mono);color:var(--text2)}
.config-val{font-size:12px;font-family:var(--mono);color:var(--accent);font-weight:500}
.config-val.muted{color:var(--text3)}
.config-val.green{color:var(--green)}
.config-val.red{color:var(--red)}

/* LOG */
.log-container{height:220px;overflow-y:auto;font-family:var(--mono);font-size:11px}
.log-line{display:flex;gap:10px;padding:4px 0;border-bottom:1px solid rgba(255,255,255,0.03);line-height:1.5}
.log-time{color:var(--text3);flex-shrink:0;width:75px}
.log-tag{flex-shrink:0;padding:1px 6px;border-radius:3px;font-size:10px;font-weight:600}
.log-tag.ok{background:rgba(34,197,94,0.15);color:var(--green)}
.log-tag.err{background:rgba(239,68,68,0.15);color:var(--red)}
.log-tag.info{background:rgba(59,130,246,0.15);color:var(--blue)}
.log-tag.warn{background:rgba(245,158,11,0.15);color:var(--accent)}
.log-msg{color:var(--text2);flex:1}

/* TIMER */
.timer-ring-wrap{display:flex;flex-direction:column;align-items:center;justify-content:center;padding:20px}
.timer-ring{position:relative;width:120px;height:120px}
.timer-ring svg{transform:rotate(-90deg)}
.timer-circle-bg{fill:none;stroke:var(--border2);stroke-width:6}
.timer-circle{fill:none;stroke:var(--accent);stroke-width:6;stroke-linecap:round;stroke-dasharray:345;transition:stroke-dashoffset 1s linear}
.timer-text{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center}
.timer-countdown{font-family:var(--mono);font-size:22px;font-weight:600;color:var(--text)}
.timer-sub{font-size:10px;font-family:var(--mono);color:var(--text3);margin-top:2px}
.next-bake-label{font-size:11px;font-family:var(--mono);color:var(--text3);margin-top:8px;text-align:center}
.bake-btn-wrap{margin-top:12px;width:100%;display:flex;justify-content:center}

/* BOOST TABLE */
.boost-row{display:flex;align-items:center;gap:10px;padding:9px 0;border-bottom:1px solid var(--border)}
.boost-row:last-child{border-bottom:none}
.boost-icon{width:28px;height:28px;border-radius:6px;display:flex;align-items:center;justify-content:center;font-size:14px;flex-shrink:0}
.boost-name{font-size:12px;font-family:var(--mono);color:var(--text);flex:1}
.boost-status{font-size:10px;font-family:var(--mono);padding:2px 8px;border-radius:3px}
.boost-status.active{background:rgba(34,197,94,0.12);color:var(--green)}
.boost-status.inactive{background:var(--bg3);color:var(--text3)}
.boost-status.cooldown{background:rgba(245,158,11,0.12);color:var(--accent)}
.boost-time{font-size:10px;font-family:var(--mono);color:var(--text3);min-width:60px;text-align:right}

/* RUG RADAR */
.rug-row{display:flex;align-items:center;gap:10px;padding:8px 0;border-bottom:1px solid var(--border)}
.rug-row:last-child{border-bottom:none}
.rug-name{font-size:12px;font-family:var(--mono);color:var(--text);flex:1}
.rug-ratio{font-size:11px;font-family:var(--mono);color:var(--text3)}
.rug-risk{font-size:10px;padding:2px 8px;border-radius:3px;font-family:var(--mono)}
.rug-risk.low{background:rgba(34,197,94,0.12);color:var(--green)}
.rug-risk.med{background:rgba(245,158,11,0.12);color:var(--accent)}
.rug-risk.high{background:rgba(239,68,68,0.12);color:var(--red)}
.rug-cost{font-size:10px;font-family:var(--mono);color:var(--text3);min-width:70px;text-align:right}

/* SKILL BADGE */
.skill-badge{display:inline-flex;align-items:center;gap:6px;padding:6px 12px;border-radius:6px;background:rgba(245,158,11,0.1);border:1px solid rgba(245,158,11,0.25);font-size:12px;font-family:var(--mono);color:var(--accent)}
.skill-dot{width:6px;height:6px;border-radius:50%;background:var(--accent)}

/* PROGRESS BAR */
.prog-wrap{margin:8px 0}
.prog-label{display:flex;justify-content:space-between;font-size:11px;font-family:var(--mono);color:var(--text3);margin-bottom:5px}
.prog-label span{color:var(--text2)}
.prog-bar{height:5px;background:var(--border2);border-radius:999px;overflow:hidden}
.prog-fill{height:100%;border-radius:999px;transition:width 0.5s}

/* LEADERBOARD */
.lb-row{display:flex;align-items:center;gap:10px;padding:8px 0;border-bottom:1px solid var(--border)}
.lb-row:last-child{border-bottom:none}
.lb-rank{font-family:var(--mono);font-size:11px;color:var(--text3);width:20px;text-align:center}
.lb-rank.top{color:var(--accent);font-weight:600}
.lb-name{font-size:12px;font-family:var(--mono);flex:1;color:var(--text)}
.lb-name.mine{color:var(--accent)}
.lb-score{font-size:11px;font-family:var(--mono);color:var(--text2)}
.lb-pct{font-size:10px;font-family:var(--mono);color:var(--text3);min-width:40px;text-align:right}

/* SETTINGS */
.input-row{display:flex;flex-direction:column;gap:4px;margin-bottom:12px}
.input-label{font-size:11px;font-family:var(--mono);color:var(--text3)}
.input-field{background:var(--bg3);border:1px solid var(--border2);border-radius:var(--radius);padding:8px 10px;font-family:var(--mono);font-size:12px;color:var(--text);outline:none;transition:border-color 0.15s}
.input-field:focus{border-color:var(--accent)}
select.input-field option{background:var(--bg3)}

/* PAGE SWITCHER */
.page{display:none}
.page.active{display:block}

/* SEASON EVENT */
.event-banner{display:flex;align-items:center;gap:12px;padding:12px 16px;background:rgba(245,158,11,0.06);border:1px solid rgba(245,158,11,0.2);border-radius:var(--radius);margin-bottom:16px}
.event-icon{font-size:24px}
.event-name{font-size:13px;font-weight:600;font-family:var(--mono);color:var(--accent)}
.event-desc{font-size:11px;font-family:var(--mono);color:var(--text3);margin-top:2px}
.event-timer{margin-left:auto;font-family:var(--mono);font-size:12px;color:var(--accent);font-weight:600}

/* UPGRADE GRID */
.upgrade-card{background:var(--bg3);border:1px solid var(--border);border-radius:var(--radius);padding:12px;margin-bottom:8px}
.upgrade-head{display:flex;align-items:center;justify-content:space-between;margin-bottom:8px}
.upgrade-name{font-size:12px;font-family:var(--mono);font-weight:600;color:var(--text)}
.upgrade-tag{font-size:10px;font-family:var(--mono);padding:2px 7px;border-radius:3px}
.upgrade-tag.active{background:rgba(34,197,94,0.12);color:var(--green)}
.upgrade-tag.locked{background:var(--bg);color:var(--text3);border:1px solid var(--border)}

/* RESPONSIVE NOTE */
.warn-box{background:rgba(245,158,11,0.06);border:1px solid rgba(245,158,11,0.2);border-radius:var(--radius);padding:10px 14px;font-size:11px;font-family:var(--mono);color:var(--text3);line-height:1.6;margin-bottom:16px}
.warn-box strong{color:var(--accent)}

/* MULTIPLIER MODAL */
.modal-backdrop{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.7);z-index:100;align-items:center;justify-content:center}
.modal-backdrop.open{display:flex}
.modal{background:var(--bg2);border:1px solid var(--border2);border-radius:12px;width:520px;max-width:95vw;overflow:hidden}
.modal-head{display:flex;align-items:center;justify-content:space-between;padding:16px 20px;border-bottom:1px solid var(--border)}
.modal-title{font-family:var(--mono);font-size:13px;font-weight:600;color:var(--text);letter-spacing:0.06em}
.modal-close{background:none;border:none;color:var(--text3);font-size:18px;cursor:pointer;padding:2px 6px;border-radius:4px;line-height:1}
.modal-close:hover{color:var(--text);background:var(--bg3)}
.modal-body{padding:20px}
.modal-footer{padding:14px 20px;border-top:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;gap:10px}

/* MULTIPLIER COMPONENT ROWS */
.mult-row{display:flex;align-items:center;gap:10px;padding:9px 12px;background:var(--bg3);border:1px solid var(--border);border-radius:var(--radius);margin-bottom:6px}
.mult-row.locked{opacity:0.45}
.mult-icon{font-size:16px;width:22px;text-align:center;flex-shrink:0}
.mult-name{font-size:12px;font-family:var(--mono);color:var(--text2);flex:1}
.mult-source{font-size:10px;font-family:var(--mono);color:var(--text3);flex-shrink:0;min-width:60px}
.mult-input{width:72px;background:var(--bg2);border:1px solid var(--border2);border-radius:5px;padding:5px 8px;font-family:var(--mono);font-size:12px;color:var(--accent);text-align:right;outline:none;transition:border-color 0.15s}
.mult-input:focus{border-color:var(--accent)}
.mult-input:disabled{color:var(--text3);cursor:not-allowed}
.mult-tag{font-size:10px;font-family:var(--mono);padding:2px 7px;border-radius:3px;flex-shrink:0}
.mult-tag.skill{background:rgba(168,85,247,0.12);color:#a855f7}
.mult-tag.boost{background:rgba(245,158,11,0.12);color:var(--accent)}
.mult-tag.event{background:rgba(34,197,94,0.12);color:var(--green)}
.mult-tag.upgrade{background:rgba(59,130,246,0.12);color:var(--blue)}
.mult-tag.locked{background:var(--bg);color:var(--text3);border:1px solid var(--border)}

.mult-total-row{display:flex;align-items:center;justify-content:space-between;padding:12px;background:rgba(245,158,11,0.06);border:1px solid rgba(245,158,11,0.2);border-radius:var(--radius);margin-top:10px}
.mult-total-label{font-family:var(--mono);font-size:12px;color:var(--text2)}
.mult-total-val{font-family:var(--mono);font-size:18px;font-weight:600;color:var(--accent)}
.mult-output-row{display:flex;align-items:center;justify-content:space-between;padding:6px 12px;margin-top:4px}
.mult-output-label{font-family:var(--mono);font-size:11px;color:var(--text3)}
.mult-output-val{font-family:var(--mono);font-size:11px;color:var(--text2)}

/* RESET LINK */
.mult-reset{font-family:var(--mono);font-size:11px;color:var(--text3);cursor:pointer;text-decoration:underline}
.mult-reset:hover{color:var(--accent)}
</style>
</head>
<body>

<div class="shell">

<!-- SIDEBAR -->
<aside class="sidebar">
  <div class="logo">
    <div class="logo-icon">🍪</div>
    <div>
      <div class="logo-text">BAKERY AGENT</div>
      <div class="logo-sub">Abstract · Season 7</div>
    </div>
  </div>

  <nav class="nav">
    <div class="nav-section">OVERVIEW</div>
    <div class="nav-item active" onclick="switchPage('dashboard',this)">
      <span class="ni">📊</span> Dashboard
    </div>
    <div class="nav-item" onclick="switchPage('agent',this)">
      <span class="ni">🤖</span> Agent Control
      <span class="nav-badge green" id="agent-badge">ON</span>
    </div>
    <div class="nav-item" onclick="switchPage('log',this)">
      <span class="ni">📋</span> Activity Log
      <span class="nav-badge" id="log-badge" style="background:var(--blue)">0</span>
    </div>

    <div class="nav-section" style="margin-top:8px">GAMEPLAY</div>
    <div class="nav-item" onclick="switchPage('boosts',this)">
      <span class="ni">⚡</span> Boosts & Rugs
    </div>
    <div class="nav-item" onclick="switchPage('upgrades',this)">
      <span class="ni">🏗️</span> Bakery Upgrades
    </div>
    <div class="nav-item" onclick="switchPage('leaderboard',this)">
      <span class="ni">🏆</span> Leaderboard
    </div>

    <div class="nav-section" style="margin-top:8px">CONFIG</div>
    <div class="nav-item" onclick="switchPage('settings',this)">
      <span class="ni">⚙️</span> Settings
    </div>
  </nav>

  <div class="sidebar-footer">
    <div class="wallet-card">
      <div class="wallet-label">CONNECTED WALLET</div>
      <div class="wallet-addr" id="wallet-display">0x4f2a...c9b1</div>
      <div class="wallet-bal" id="wallet-eth">0.0482 ETH</div>
    </div>
  </div>
</aside>

<!-- MAIN -->
<main class="main">

  <!-- TOPBAR -->
  <div class="topbar">
    <div class="topbar-title" id="page-title">Dashboard</div>
    <div class="topbar-right">
      <div class="status-pill running" id="agent-status-pill" onclick="toggleAgent()">
        <div class="pulse"></div>
        <span id="agent-status-label">Agent Running</span>
      </div>
      <button class="btn btn-ghost" onclick="syncState()">↻ Sync</button>
    </div>
  </div>

  <!-- ===== DASHBOARD PAGE ===== -->
  <div class="page active content" id="page-dashboard">

    <div class="warn-box">
      <strong>⚠ Live mode disclaimer:</strong> This dashboard simulates agent behavior. To connect a real wallet and execute on-chain, deploy with Wagmi + Abstract AGW SDK. Always fetch <code>/agent.json</code> before any value-bearing action.
    </div>

    <!-- ACTIVE EVENT BANNER -->
    <div class="event-banner" id="event-banner">
      <div class="event-icon">🌟</div>
      <div>
        <div class="event-name">GOLDEN BATCH ACTIVE</div>
        <div class="event-desc">+20% bake output for 45 min — your bakery is boosted!</div>
      </div>
      <div class="event-timer" id="event-timer">38:22</div>
    </div>

    <!-- STAT CARDS -->
    <div class="stats-grid">
      <div class="stat-card cookies">
        <div class="stat-label">COOKIE BALANCE</div>
        <div class="stat-val cookies" id="stat-cookies">0</div>
        <div class="stat-delta up" id="stat-cookies-delta">+0 this session</div>
      </div>
      <div class="stat-card score">
        <div class="stat-label">SEASON SCORE</div>
        <div class="stat-val" id="stat-score" style="color:var(--blue)">0</div>
        <div class="stat-delta up" id="stat-score-delta">+0 today</div>
      </div>
      <div class="stat-card bakes">
        <div class="stat-label">BAKES (SESSION)</div>
        <div class="stat-val bakes" id="stat-bakes">0</div>
        <div class="stat-delta" id="stat-bakes-delta" style="color:var(--text3)">Every 5 blocks (~25s)</div>
      </div>
      <div class="stat-card rank">
        <div class="stat-label">BAKERY RANK</div>
        <div class="stat-val rank" id="stat-rank">#—</div>
        <div class="stat-delta" id="stat-rank-delta" style="color:var(--text3)">of 10 qualifying</div>
      </div>
    </div>

    <!-- ROW 2 -->
    <div class="three-col">
      <!-- BAKE TIMER -->
      <div class="panel">
        <div class="panel-head">
          <span class="panel-title">AUTO-BAKE ENGINE</span>
          <span class="skill-badge"><span class="skill-dot"></span>Perfectionist · 1.04×</span>
        </div>
        <div class="panel-body" style="display:flex;align-items:center;gap:20px">
          <div class="timer-ring-wrap" style="padding:0">
            <div class="timer-ring">
              <svg width="120" height="120" viewBox="0 0 120 120">
                <circle class="timer-circle-bg" cx="60" cy="60" r="54"/>
                <circle class="timer-circle" id="timer-circle" cx="60" cy="60" r="54" stroke-dashoffset="0"/>
              </svg>
              <div class="timer-text">
                <div class="timer-countdown" id="timer-countdown">--</div>
                <div class="timer-sub" id="timer-sub">NEXT BAKE</div>
              </div>
            </div>
          </div>
          <div style="flex:1">
            <div class="config-row">
              <span class="config-key">BAKE INTERVAL</span>
              <span class="config-val">5 blocks (~25s)</span>
            </div>
            <div class="config-row">
              <span class="config-key">COOKIE_SCALE</span>
              <span class="config-val" id="cookie-scale-val">1,000</span>
            </div>
            <div class="config-row">
              <span class="config-key">MULTIPLIER</span>
              <span class="config-val green" id="effective-mult">1.248×</span>
            </div>
            <div class="config-row">
              <span class="config-key">OUTPUT/BAKE</span>
              <span class="config-val" id="output-per-bake">1,248</span>
            </div>
            <div class="config-row">
              <span class="config-key">AUTO-BAKE</span>
              <span class="config-val green" id="autobake-status">ENABLED</span>
            </div>
            <div style="margin-top:12px;display:flex;gap:8px">
              <button class="btn btn-primary" id="manual-bake-btn" onclick="manualBake()">🍪 Bake Now</button>
              <button class="btn btn-ghost" onclick="switchPage('agent',document.querySelector('.nav-item:nth-child(2)'))">Configure</button>
            </div>
          </div>
        </div>
      </div>

      <!-- ACTIVE BOOSTS SIDEBAR -->
      <div class="panel">
        <div class="panel-head">
          <span class="panel-title">ACTIVE EFFECTS</span>
        </div>
        <div class="panel-body" style="padding:10px 16px">
          <div class="boost-row">
            <div class="boost-icon" style="background:rgba(245,158,11,0.12)">⚡</div>
            <div class="boost-name">Sugar Rush</div>
            <div class="boost-status active">ACTIVE</div>
            <div class="boost-time" id="boost1-time">18:42</div>
          </div>
          <div class="boost-row">
            <div class="boost-icon" style="background:rgba(34,197,94,0.12)">🌟</div>
            <div class="boost-name">Golden Batch</div>
            <div class="boost-status active">EVENT</div>
            <div class="boost-time" id="boost2-time">38:22</div>
          </div>
          <div class="boost-row">
            <div class="boost-icon" style="background:rgba(59,130,246,0.12)">🏗️</div>
            <div class="boost-name">Oven Upgrade</div>
            <div class="boost-status active">PASSIVE</div>
            <div class="boost-time">+1%</div>
          </div>
          <div class="boost-row">
            <div class="boost-icon" style="background:rgba(100,116,139,0.12)">🧹</div>
            <div class="boost-name">Cleanup Shield</div>
            <div class="boost-status inactive">INACTIVE</div>
            <div class="boost-time">—</div>
          </div>
        </div>
      </div>
    </div>

    <!-- UPGRADE PROGRESS -->
    <div class="panel" style="margin-bottom:16px">
      <div class="panel-head">
        <span class="panel-title">UPGRADE PROGRESS</span>
        <span style="font-size:11px;font-family:var(--mono);color:var(--text3)">Level <span id="bakery-level">1</span> / 4</span>
      </div>
      <div class="panel-body">
        <div style="display:grid;grid-template-columns:1fr 1fr;gap:16px">
          <div>
            <div class="prog-wrap">
              <div class="prog-label"><span>Oven (Active)</span><span id="oven-pct">62%</span></div>
              <div class="prog-bar"><div class="prog-fill" id="oven-bar" style="width:62%;background:var(--accent)"></div></div>
            </div>
            <div class="prog-wrap">
              <div class="prog-label"><span>Propaganda (Active)</span><span id="prop-pct">28%</span></div>
              <div class="prog-bar"><div class="prog-fill" id="prop-bar" style="width:28%;background:var(--blue)"></div></div>
            </div>
          </div>
          <div>
            <div class="prog-wrap">
              <div class="prog-label"><span>Cleaners (Passive)</span><span id="clean-pct">85%</span></div>
              <div class="prog-bar"><div class="prog-fill" id="clean-bar" style="width:85%;background:var(--green)"></div></div>
            </div>
            <div class="prog-wrap">
              <div class="prog-label"><span>Sabotage (Active)</span><span id="sab-pct">11%</span></div>
              <div class="prog-bar"><div class="prog-fill" id="sab-bar" style="width:11%;background:#a855f7"></div></div>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>

  <!-- ===== AGENT PAGE ===== -->
  <div class="page content" id="page-agent">
    <div class="two-col">
      <!-- CORE SETTINGS -->
      <div class="panel">
        <div class="panel-head"><span class="panel-title">AGENT CORE SETTINGS</span></div>
        <div class="panel-body">
          <div class="agent-grid">
            <div class="toggle-row">
              <span class="toggle-label">AUTO-BAKE</span>
              <label class="toggle">
                <input type="checkbox" id="tog-autobake" checked onchange="updateAgentToggle('autobake',this.checked)">
                <div class="toggle-track"></div>
                <div class="toggle-thumb"></div>
              </label>
            </div>
            <div class="toggle-row">
              <span class="toggle-label">BOOST MONITOR</span>
              <label class="toggle">
                <input type="checkbox" id="tog-boost" checked onchange="updateAgentToggle('boost',this.checked)">
                <div class="toggle-track"></div>
                <div class="toggle-thumb"></div>
              </label>
            </div>
            <div class="toggle-row">
              <span class="toggle-label">RUG DEFENSE</span>
              <label class="toggle">
                <input type="checkbox" id="tog-defense" checked onchange="updateAgentToggle('defense',this.checked)">
                <div class="toggle-track"></div>
                <div class="toggle-thumb"></div>
              </label>
            </div>
            <div class="toggle-row">
              <span class="toggle-label">AUTO-CLEANUP</span>
              <label class="toggle">
                <input type="checkbox" id="tog-cleanup" onchange="updateAgentToggle('cleanup',this.checked)">
                <div class="toggle-track"></div>
                <div class="toggle-thumb"></div>
              </label>
            </div>
            <div class="toggle-row">
              <span class="toggle-label">EVENT DETECT</span>
              <label class="toggle">
                <input type="checkbox" id="tog-event" checked onchange="updateAgentToggle('event',this.checked)">
                <div class="toggle-track"></div>
                <div class="toggle-thumb"></div>
              </label>
            </div>
            <div class="toggle-row">
              <span class="toggle-label">UPGRADE CONTRIB</span>
              <label class="toggle">
                <input type="checkbox" id="tog-upgrade" onchange="updateAgentToggle('upgrade',this.checked)">
                <div class="toggle-track"></div>
                <div class="toggle-thumb"></div>
              </label>
            </div>
          </div>
        </div>
      </div>

      <!-- STRATEGY CONFIG -->
      <div class="panel">
        <div class="panel-head"><span class="panel-title">BAKE STRATEGY</span></div>
        <div class="panel-body">
          <div class="input-row">
            <div class="input-label">STRATEGY MODE</div>
            <select class="input-field" id="strategy-select" onchange="applyStrategy(this.value)">
              <option value="score">Max Score (Recommended)</option>
              <option value="cookies">Max Cookies</option>
              <option value="safe">Safe Mode (no rugs sent)</option>
              <option value="custom">Custom</option>
            </select>
          </div>
          <div class="input-row">
            <div class="input-label">BAKE INTERVAL OVERRIDE (seconds, 0=auto)</div>
            <input class="input-field" type="number" id="bake-interval" value="0" min="0" placeholder="0 = use block cadence (25s)">
          </div>
          <div class="input-row">
            <div class="input-label">COOKIE RESERVE (do not spend below)</div>
            <input class="input-field" type="number" id="cookie-reserve" value="10000" min="0">
          </div>
          <div class="input-row">
            <div class="input-label">RUG BUDGET PER HOUR (cookies)</div>
            <input class="input-field" type="number" id="rug-budget" value="5000" min="0">
          </div>
          <div style="margin-top:4px">
            <button class="btn btn-primary" onclick="saveStrategy()">Save Strategy</button>
          </div>
        </div>
      </div>
    </div>

    <!-- EFFICIENCY BREAKDOWN -->
    <div class="panel" style="margin-bottom:16px">
      <div class="panel-head">
        <span class="panel-title">EFFICIENCY BREAKDOWN</span>
        <button class="btn btn-ghost" style="font-size:11px;padding:5px 12px" onclick="openMultModal()">✏️ Modify Multipliers</button>
      </div>
      <div class="panel-body">
        <div style="display:grid;grid-template-columns:repeat(3,1fr);gap:16px">
          <div>
            <div class="config-row">
              <span class="config-key">BASE MULT</span><span class="config-val">1.000×</span>
            </div>
            <div class="config-row">
              <span class="config-key">Perfectionist</span><span class="config-val green" id="eff-skill">+0.040×</span>
            </div>
            <div class="config-row">
              <span class="config-key">Sugar Rush</span><span class="config-val green" id="eff-sr">+0.100×</span>
            </div>
          </div>
          <div>
            <div class="config-row">
              <span class="config-key">Golden Batch</span><span class="config-val green" id="eff-gb">+0.200×</span>
            </div>
            <div class="config-row">
              <span class="config-key">Oven Passive</span><span class="config-val green" id="eff-ovenp">+0.010×</span>
            </div>
            <div class="config-row">
              <span class="config-key">Oven Active</span><span class="config-val" style="color:var(--text3)">locked</span>
            </div>
          </div>
          <div>
            <div class="config-row">
              <span class="config-key">TOTAL MULT</span><span class="config-val" id="eff-total" style="font-size:16px">1.350×</span>
            </div>
            <div class="config-row">
              <span class="config-key">OUTPUT/BAKE</span><span class="config-val" id="eff-output">1,350</span>
            </div>
            <div class="config-row">
              <span class="config-key">EST. /HOUR</span><span class="config-val green" id="eff-hourly">194,400</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- SKILL PANEL -->
    <div class="panel">
      <div class="panel-head"><span class="panel-title">ACTIVE SKILL</span></div>
      <div class="panel-body">
        <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:8px">
          <div id="sk-lucky" class="toggle-row" style="flex-direction:column;align-items:flex-start;cursor:pointer;gap:4px" onclick="selectSkill('lucky')">
            <span style="font-size:16px">🍀</span>
            <span class="toggle-label">Lucky</span>
            <span style="font-size:10px;color:var(--text3);font-family:var(--mono)">+4% boost hit</span>
          </div>
          <div id="sk-perfectionist" class="toggle-row" style="flex-direction:column;align-items:flex-start;cursor:pointer;gap:4px;border-color:rgba(245,158,11,0.4);background:rgba(245,158,11,0.06)" onclick="selectSkill('perfectionist')">
            <span style="font-size:16px">🎯</span>
            <span class="toggle-label" style="color:var(--accent)">Perfectionist ✓</span>
            <span style="font-size:10px;color:var(--accent);font-family:var(--mono)">1.04× bake output</span>
          </div>
          <div id="sk-booster" class="toggle-row" style="flex-direction:column;align-items:flex-start;cursor:pointer;gap:4px" onclick="selectSkill('booster')">
            <span style="font-size:16px">⚡</span>
            <span class="toggle-label">Booster</span>
            <span style="font-size:10px;color:var(--text3);font-family:var(--mono)">−5% boost cost</span>
          </div>
          <div id="sk-sweeper" class="toggle-row" style="flex-direction:column;align-items:flex-start;cursor:pointer;gap:4px" onclick="selectSkill('sweeper')">
            <span style="font-size:16px">🧹</span>
            <span class="toggle-label">Sweeper</span>
            <span style="font-size:10px;color:var(--text3);font-family:var(--mono)">Free cleanup/12h</span>
          </div>
        </div>
        <div style="margin-top:10px;font-size:11px;font-family:var(--mono);color:var(--text3)">
          Starter replacement: 5,000 cookies · Advanced: 20,000 cookies · First selection is free
        </div>
      </div>
    </div>
  </div>

  <!-- ===== LOG PAGE ===== -->
  <div class="page content" id="page-log">
    <div class="panel">
      <div class="panel-head">
        <span class="panel-title">ACTIVITY LOG</span>
        <div style="display:flex;gap:8px">
          <button class="btn btn-ghost" onclick="clearLog()">Clear</button>
          <button class="btn btn-ghost" onclick="exportLog()">Export</button>
        </div>
      </div>
      <div class="panel-body">
        <div class="log-container" id="log-container"></div>
      </div>
    </div>
  </div>

  <!-- ===== BOOSTS PAGE ===== -->
  <div class="page content" id="page-boosts">
    <div class="two-col">
      <div class="panel">
        <div class="panel-head"><span class="panel-title">ACTIVE BOOSTS ON YOUR BAKERY</span></div>
        <div class="panel-body">
          <div class="boost-row">
            <div class="boost-icon" style="background:rgba(245,158,11,0.12)">⚡</div>
            <div><div class="boost-name">Sugar Rush</div><div style="font-size:10px;font-family:var(--mono);color:var(--text3)">+10% bake output</div></div>
            <div style="margin-left:auto;text-align:right">
              <div class="boost-status active">18:42</div>
            </div>
          </div>
          <div class="boost-row">
            <div class="boost-icon" style="background:rgba(34,197,94,0.12)">🌟</div>
            <div><div class="boost-name">Golden Batch (Event)</div><div style="font-size:10px;font-family:var(--mono);color:var(--text3)">+20% bake output</div></div>
            <div style="margin-left:auto">
              <div class="boost-status active">38:22</div>
            </div>
          </div>
          <div style="margin-top:16px">
            <button class="btn btn-primary" onclick="addLog('INFO','Boost purchase requested — send exact VRF fee as msg.value')">+ Buy Boost</button>
          </div>
        </div>
      </div>

      <div class="panel">
        <div class="panel-head"><span class="panel-title">RUG RADAR — ENEMY BAKERIES</span></div>
        <div class="panel-body">
          <div class="rug-row">
            <div class="rug-name">CookieMafia</div>
            <div class="rug-ratio">85% ratio</div>
            <div class="rug-risk low">LOW COST</div>
            <div class="rug-cost">1.00× · 95% hit</div>
          </div>
          <div class="rug-row">
            <div class="rug-name">BreadFactory</div>
            <div class="rug-ratio">55% ratio</div>
            <div class="rug-risk med">MED COST</div>
            <div class="rug-cost">1.15× · 85% hit</div>
          </div>
          <div class="rug-row">
            <div class="rug-name">GlitchOvens</div>
            <div class="rug-ratio">18% ratio</div>
            <div class="rug-risk high">HIGH COST</div>
            <div class="rug-cost">2.00× · 40% hit</div>
          </div>
          <div class="rug-row">
            <div class="rug-name">DogeKitchen</div>
            <div class="rug-ratio">130% ratio</div>
            <div class="rug-risk low">FULL HIT</div>
            <div class="rug-cost">1.00× · 100%</div>
          </div>
          <div style="margin-top:16px;font-size:10px;font-family:var(--mono);color:var(--text3)">
            * Ratio = your baked cookies / target baked cookies. Must be same division. Post-expiry congestion adds up to +100% cost decaying over 30 min.
          </div>
        </div>
      </div>
    </div>

    <!-- CLEANUP -->
    <div class="panel" style="margin-top:0">
      <div class="panel-head"><span class="panel-title">DEFENSE STATUS</span></div>
      <div class="panel-body">
        <div style="display:grid;grid-template-columns:repeat(3,1fr);gap:12px">
          <div class="toggle-row" style="flex-direction:column;align-items:flex-start;gap:6px">
            <span style="font-size:20px">🧹</span>
            <span class="toggle-label">Cleanup Crew</span>
            <span style="font-size:10px;font-family:var(--mono);color:var(--green)">READY</span>
            <button class="btn btn-ghost" style="font-size:10px;padding:4px 10px;margin-top:4px" onclick="addLog('OK','Cleanup Crew launched — targeting strongest active rug')">Use</button>
          </div>
          <div class="toggle-row" style="flex-direction:column;align-items:flex-start;gap:6px">
            <span style="font-size:20px">🤖</span>
            <span class="toggle-label">Robotic Cleaners</span>
            <span style="font-size:10px;font-family:var(--mono);color:var(--text3)">+5 min protection</span>
            <button class="btn btn-ghost" style="font-size:10px;padding:4px 10px;margin-top:4px" onclick="addLog('INFO','Robotic Cleaners active — protection window extended')">Activate</button>
          </div>
          <div class="toggle-row" style="flex-direction:column;align-items:flex-start;gap:6px">
            <span style="font-size:20px">🛡️</span>
            <span class="toggle-label">Shield Window</span>
            <span style="font-size:10px;font-family:var(--mono);color:var(--text3)">INACTIVE</span>
            <span style="font-size:10px;font-family:var(--mono);color:var(--text3);margin-top:4px">10 min post-cleanup</span>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- ===== UPGRADES PAGE ===== -->
  <div class="page content" id="page-upgrades">
    <div class="warn-box">
      Upgrade targets scale with committed members. A committed member = 10+ qualifying bake actions. Cookie contributions are permanent — they do not refund.
    </div>

    <div class="upgrade-card">
      <div class="upgrade-head">
        <span class="upgrade-name">🔥 Oven</span>
        <span class="upgrade-tag active">PASSIVE UNLOCKED</span>
      </div>
      <div style="font-size:11px;font-family:var(--mono);color:var(--text3);margin-bottom:8px">Passive: +1% bake output · Active: +4% bake output, −5% incoming rug severity</div>
      <div class="prog-wrap">
        <div class="prog-label"><span>Active path (cookies)</span><span>62%</span></div>
        <div class="prog-bar"><div class="prog-fill" style="width:62%;background:var(--accent)"></div></div>
      </div>
      <div style="margin-top:8px;font-size:11px;font-family:var(--mono);color:var(--text3)">Base: 7,000 cookies/member · Unlock order: 1.00× · 20 unique contributors needed</div>
      <button class="btn btn-ghost" style="margin-top:10px;font-size:11px" onclick="addLog('INFO','Contribute to Oven upgrade — server-signed authorization required')">Contribute Cookies</button>
    </div>

    <div class="upgrade-card">
      <div class="upgrade-head">
        <span class="upgrade-name">📢 Propaganda</span>
        <span class="upgrade-tag locked">LOCKED</span>
      </div>
      <div style="font-size:11px;font-family:var(--mono);color:var(--text3);margin-bottom:8px">Passive: −2% boost cost · Active: −8% boost cost, +3pp boost success chance</div>
      <div class="prog-wrap">
        <div class="prog-label"><span>Active path (cookies)</span><span>28%</span></div>
        <div class="prog-bar"><div class="prog-fill" style="width:28%;background:var(--blue)"></div></div>
      </div>
      <div style="margin-top:8px;font-size:11px;font-family:var(--mono);color:var(--text3)">Base: 10,500 cookies/member · Unlock order: 1.20× · 15 unique contributors needed</div>
      <button class="btn btn-ghost" style="margin-top:10px;font-size:11px" onclick="addLog('INFO','Contribute to Propaganda upgrade')">Contribute Cookies</button>
    </div>

    <div class="upgrade-card">
      <div class="upgrade-head">
        <span class="upgrade-name">🧹 Cleaners</span>
        <span class="upgrade-tag locked">PASSIVE 85%</span>
      </div>
      <div style="font-size:11px;font-family:var(--mono);color:var(--text3);margin-bottom:8px">Passive: −5% cleanup cost · Active: −15% cleanup cost, +5 min protection, −15% incoming rug duration</div>
      <div class="prog-wrap">
        <div class="prog-label"><span>Passive path (actions)</span><span>85%</span></div>
        <div class="prog-bar"><div class="prog-fill" style="width:85%;background:var(--green)"></div></div>
      </div>
      <div style="margin-top:8px;font-size:11px;font-family:var(--mono);color:var(--text3)">Requires 30 full-size cleanup actions · Almost there!</div>
    </div>

    <div class="upgrade-card">
      <div class="upgrade-head">
        <span class="upgrade-name">💣 Sabotage</span>
        <span class="upgrade-tag locked">LOCKED</span>
      </div>
      <div style="font-size:11px;font-family:var(--mono);color:var(--text3);margin-bottom:8px">Passive: −2% rug cost · Active: −8% rug cost, +3pp rug success vs stronger targets</div>
      <div class="prog-wrap">
        <div class="prog-label"><span>Active path (cookies)</span><span>11%</span></div>
        <div class="prog-bar"><div class="prog-fill" style="width:11%;background:#a855f7"></div></div>
      </div>
      <div style="margin-top:8px;font-size:11px;font-family:var(--mono);color:var(--text3)">Base: 27,000 cookies/member · Unlock order: 1.75×</div>
      <button class="btn btn-ghost" style="margin-top:10px;font-size:11px" onclick="addLog('INFO','Contribute to Sabotage upgrade')">Contribute Cookies</button>
    </div>
  </div>

  <!-- ===== LEADERBOARD PAGE ===== -->
  <div class="page content" id="page-leaderboard">
    <div class="panel">
      <div class="panel-head">
        <span class="panel-title">SEASON 7 — TOP BAKERIES</span>
        <span style="font-size:11px;font-family:var(--mono);color:var(--text3)">Top 10 split prize pool by score share</span>
      </div>
      <div class="panel-body">
        <div class="lb-row" style="padding-bottom:6px;margin-bottom:4px;border-bottom:1px solid var(--border2)">
          <span style="width:20px;font-size:10px;font-family:var(--mono);color:var(--text3)">#</span>
          <span style="flex:1;font-size:10px;font-family:var(--mono);color:var(--text3)">BAKERY</span>
          <span style="font-size:10px;font-family:var(--mono);color:var(--text3)">SCORE</span>
          <span style="min-width:40px;text-align:right;font-size:10px;font-family:var(--mono);color:var(--text3)">SHARE</span>
        </div>
        <div id="lb-rows">
          <!-- filled by JS -->
        </div>
      </div>
    </div>
    <div style="margin-top:12px;font-size:11px;font-family:var(--mono);color:var(--text3);padding:0 2px">
      Payout formula: <span style="color:var(--accent)">bakeryPayout = bakeryFinalScore / totalTop10Score × totalPrizePool</span><br>
      Your member payout: <span style="color:var(--accent)">memberPayout = yourFinalScore / bakeryFinalScore × bakeryPayout</span>
    </div>
  </div>

  <!-- ===== SETTINGS PAGE ===== -->
  <div class="page content" id="page-settings">
    <div class="two-col">
      <div class="panel">
        <div class="panel-head"><span class="panel-title">WALLET & NETWORK</span></div>
        <div class="panel-body">
          <div class="input-row">
            <div class="input-label">WALLET ADDRESS (Abstract Global Wallet)</div>
            <input class="input-field" id="wallet-input" type="text" placeholder="0x..." value="0x4f2a8c3d1e9f7b6a5c2d0e8f4b3a2c1d9e8f7c9b1">
          </div>
          <div class="input-row">
            <div class="input-label">RPC ENDPOINT (Abstract)</div>
            <input class="input-field" type="text" value="https://api.mainnet.abs.xyz" placeholder="https://api.mainnet.abs.xyz">
          </div>
          <div class="input-row">
            <div class="input-label">BAKERY ID (current season)</div>
            <input class="input-field" id="bakery-id-input" type="text" placeholder="e.g. 42" value="42">
          </div>
          <button class="btn btn-primary" onclick="saveSettings()">Save & Reconnect</button>
        </div>
      </div>

      <div class="panel">
        <div class="panel-head"><span class="panel-title">LIVE STATE</span></div>
        <div class="panel-body">
          <div class="config-row">
            <span class="config-key">SEASON</span><span class="config-val">7 (db id 9)</span>
          </div>
          <div class="config-row">
            <span class="config-key">CHAIN ID</span><span class="config-val">2741</span>
          </div>
          <div class="config-row">
            <span class="config-key">BUY-IN</span><span class="config-val" id="buyin-val">Fetch /agent.json</span>
          </div>
          <div class="config-row">
            <span class="config-key">VRF FEE</span><span class="config-val" id="vrf-val">Fetch /agent.json</span>
          </div>
          <div class="config-row">
            <span class="config-key">COOKIE_SCALE</span><span class="config-val">1,000</span>
          </div>
          <div class="config-row">
            <span class="config-key">MEMBER CAP</span><span class="config-val">50</span>
          </div>
          <div class="config-row">
            <span class="config-key">LAST SYNC</span><span class="config-val muted" id="last-sync">Never</span>
          </div>
          <button class="btn btn-ghost" style="margin-top:12px" onclick="syncState()">↻ Fetch /agent.json</button>
        </div>
      </div>
    </div>

    <div class="panel">
      <div class="panel-head"><span class="panel-title">AGENT INTEGRATION GUIDE</span></div>
      <div class="panel-body">
        <div style="font-size:12px;font-family:var(--mono);color:var(--text2);line-height:2">
          <div style="color:var(--text3);margin-bottom:8px">To connect this dashboard to a live on-chain agent:</div>
          <div>1. Install <span style="color:var(--accent)">@abstract-foundation/agw-client</span> and Wagmi</div>
          <div>2. Fetch <span style="color:var(--accent)">https://rugpull.bakery/agent.json</span> on load for live addresses</div>
          <div>3. Connect AGW with <span style="color:var(--accent)">useAbstractClient()</span></div>
          <div>4. Call <span style="color:var(--accent)">bake()</span> every 5 blocks via block subscription</div>
          <div>5. Monitor <span style="color:var(--accent)">BoostManager</span> events for incoming rugs</div>
          <div>6. Use session keys for unattended <span style="color:var(--accent)">bake / purchaseBoost / launchAttack</span></div>
          <div>7. Always send exact <span style="color:var(--accent)">getVrfFee()</span> as <span style="color:var(--accent)">msg.value</span> for boosts/rugs</div>
          <div style="margin-top:10px;color:var(--text3)">⚠ Registration and bakery creation require explicit wallet confirmation — no session keys.</div>
        </div>
      </div>
    </div>
  </div>

</main>
</div>

<!-- MULTIPLIER MODAL -->
<div class="modal-backdrop" id="mult-modal" onclick="closeMultModalOutside(event)">
  <div class="modal">
    <div class="modal-head">
      <span class="modal-title">⚙ MULTIPLIER EDITOR</span>
      <button class="modal-close" onclick="closeMultModal()">✕</button>
    </div>
    <div class="modal-body">
      <div style="font-size:11px;font-family:var(--mono);color:var(--text3);margin-bottom:14px;line-height:1.7">
        Adjust each component's contribution to your effective bake multiplier.<br>
        <strong style="color:var(--accent)">Formula:</strong> output = COOKIE_SCALE × (sum of all components) / 10,000
      </div>

      <!-- COMPONENT ROWS -->
      <div id="mult-rows-container"></div>

      <!-- TOTAL -->
      <div class="mult-total-row">
        <span class="mult-total-label">EFFECTIVE MULTIPLIER</span>
        <span class="mult-total-val" id="modal-total">1.350×</span>
      </div>
      <div class="mult-output-row">
        <span class="mult-output-label">OUTPUT PER BAKE</span>
        <span class="mult-output-val" id="modal-output">1,350 cookies</span>
      </div>
      <div class="mult-output-row">
        <span class="mult-output-label">ESTIMATED PER HOUR</span>
        <span class="mult-output-val" id="modal-hourly">194,400 cookies/hr</span>
      </div>
    </div>
    <div class="modal-footer">
      <span class="mult-reset" onclick="resetMultipliers()">↺ Reset to defaults</span>
      <div style="display:flex;gap:8px">
        <button class="btn btn-ghost" onclick="closeMultModal()">Cancel</button>
        <button class="btn btn-primary" onclick="applyMultipliers()">Apply Multipliers</button>
      </div>
    </div>
  </div>
</div>

<script>
// ─── STATE ──────────────────────────────────────────────────
// MULTIPLIER COMPONENTS — each editable independently
const DEFAULT_MULT_COMPONENTS = [
  { id:'base',    icon:'🎂', name:'Base Multiplier',    tag:'',        source:'contract', val:1.000, locked:false,  step:0.001, min:0.1,  max:5.0  },
  { id:'skill',   icon:'🎯', name:'Skill (Perfectionist)', tag:'skill', source:'season',   val:0.040, locked:false,  step:0.001, min:0,    max:0.5  },
  { id:'sr',      icon:'⚡', name:'Sugar Rush Boost',   tag:'boost',   source:'purchased',val:0.100, locked:false,  step:0.01,  min:0,    max:2.0  },
  { id:'gb',      icon:'🌟', name:'Golden Batch Event', tag:'event',   source:'event',    val:0.200, locked:false,  step:0.01,  min:0,    max:2.0  },
  { id:'of',      icon:'🔥', name:'Oven Frenzy Event',  tag:'event',   source:'event',    val:0.000, locked:false,  step:0.01,  min:0,    max:2.0  },
  { id:'oven_p',  icon:'🏗️', name:'Oven Passive',       tag:'upgrade', source:'upgrade',  val:0.010, locked:false,  step:0.001, min:0,    max:0.5  },
  { id:'oven_a',  icon:'🔩', name:'Oven Active',        tag:'locked',  source:'upgrade',  val:0.000, locked:true,   step:0.001, min:0,    max:0.5  },
  { id:'custom',  icon:'✨', name:'Custom Override',    tag:'boost',   source:'manual',   val:0.000, locked:false,  step:0.001, min:0,    max:10.0 },
];

let multComponents = DEFAULT_MULT_COMPONENTS.map(c => ({...c}));
const state = {
  agentRunning: true,
  cookies: 482300,
  cookiesDelta: 0,
  score: 1284500,
  scoreDelta: 0,
  bakes: 0,
  rank: 4,
  timerSec: 25,
  timerMax: 25,
  boostTimer1: 1122,  // 18:42
  boostTimer2: 2302,  // 38:22
  eventTimer: 2302,
  logs: [],
  logCount: 0,
  autobake: true,
  toggles: { boost:true, defense:true, cleanup:false, event:true, upgrade:false },
  cookieScale: 1000,
  effectiveMult: 1.35
};

const leaderboardData = [
  { name: 'SugarRushGang', score: 9280400, mine: false },
  { name: 'CookieMafia', score: 8100200, mine: false },
  { name: 'OvenLords', score: 7440000, mine: false },
  { name: '🍪 MY BAKERY', score: 6820000, mine: true },
  { name: 'BreadFactory', score: 5900000, mine: false },
  { name: 'GlitchOvens', score: 4700000, mine: false },
  { name: 'DogeKitchen', score: 3200000, mine: false },
  { name: 'AbstractChefs', score: 2800000, mine: false },
  { name: 'Crumbs DAO', score: 1900000, mine: false },
  { name: 'ByteBakery', score: 900000, mine: false },
];

// ─── MULTIPLIER MODAL ───────────────────────────────────────
function openMultModal() {
  renderMultRows();
  document.getElementById('mult-modal').classList.add('open');
}
function closeMultModal() {
  document.getElementById('mult-modal').classList.remove('open');
}
function closeMultModalOutside(e) {
  if(e.target === document.getElementById('mult-modal')) closeMultModal();
}

function calcTotalMult() {
  return multComponents.reduce((sum, c) => sum + (c.locked ? 0 : parseFloat(c.val)||0), 0);
}

function renderMultRows() {
  const container = document.getElementById('mult-rows-container');
  container.innerHTML = multComponents.map((c,i) => `
    <div class="mult-row ${c.locked?'locked':''}">
      <span class="mult-icon">${c.icon}</span>
      <span class="mult-name">${c.name}</span>
      <span class="mult-source">${c.source}</span>
      ${c.tag ? `<span class="mult-tag ${c.tag}">${c.tag}</span>` : '<span style="width:46px"></span>'}
      <input
        class="mult-input"
        type="number"
        step="${c.step}"
        min="${c.min}"
        max="${c.max}"
        value="${c.val.toFixed(3)}"
        ${c.locked ? 'disabled' : ''}
        oninput="onMultInput(${i}, this.value)"
        onblur="onMultBlur(${i}, this.value)"
      >
    </div>
  `).join('');
  updateModalTotals();
}

function onMultInput(i, val) {
  const parsed = parseFloat(val);
  if(!isNaN(parsed)) {
    multComponents[i].val = Math.min(Math.max(parsed, multComponents[i].min), multComponents[i].max);
    updateModalTotals();
  }
}

function onMultBlur(i, val) {
  const parsed = parseFloat(val);
  const clamped = isNaN(parsed)
    ? multComponents[i].min
    : Math.min(Math.max(parsed, multComponents[i].min), multComponents[i].max);
  multComponents[i].val = clamped;
  // re-render to show clamped value
  renderMultRows();
}

function updateModalTotals() {
  const total = calcTotalMult();
  const output = Math.floor(1000 * total);
  const hourly = Math.floor(output * (3600 / 25));
  document.getElementById('modal-total').textContent = total.toFixed(3) + '×';
  document.getElementById('modal-output').textContent = output.toLocaleString() + ' cookies';
  document.getElementById('modal-hourly').textContent = hourly.toLocaleString() + ' cookies/hr';
}

function applyMultipliers() {
  const total = calcTotalMult();
  state.effectiveMult = total;
  // Update dashboard displays
  document.getElementById('effective-mult').textContent = total.toFixed(3) + '×';
  const outputPerBake = Math.floor(state.cookieScale * total);
  document.getElementById('output-per-bake').textContent = outputPerBake.toLocaleString();
  // Update efficiency breakdown static rows
  const perfComp = multComponents.find(c => c.id === 'skill');
  const srComp   = multComponents.find(c => c.id === 'sr');
  const gbComp   = multComponents.find(c => c.id === 'gb');
  const ovenP    = multComponents.find(c => c.id === 'oven_p');
  document.getElementById('eff-skill').textContent = '+' + perfComp.val.toFixed(3) + '×';
  document.getElementById('eff-sr').textContent    = '+' + srComp.val.toFixed(3) + '×';
  document.getElementById('eff-gb').textContent    = '+' + gbComp.val.toFixed(3) + '×';
  document.getElementById('eff-ovenp').textContent = '+' + ovenP.val.toFixed(3) + '×';
  document.getElementById('eff-total').textContent = total.toFixed(3) + '×';
  document.getElementById('eff-output').textContent = outputPerBake.toLocaleString();
  document.getElementById('eff-hourly').textContent = Math.floor(outputPerBake * (3600/25)).toLocaleString();
  addLog('OK', 'Multiplier updated · total=' + total.toFixed(3) + '× · output/bake=' + outputPerBake.toLocaleString());
  closeMultModal();
}

function resetMultipliers() {
  multComponents = DEFAULT_MULT_COMPONENTS.map(c => ({...c}));
  renderMultRows();
  addLog('INFO','Multipliers reset to defaults');
}


const pageTitles = { dashboard:'Dashboard', agent:'Agent Control', log:'Activity Log', boosts:'Boosts & Rugs', upgrades:'Bakery Upgrades', leaderboard:'Leaderboard', settings:'Settings' };

function switchPage(id, el) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  if(el) el.classList.add('active');
  document.getElementById('page-title').textContent = pageTitles[id] || id;
}

// ─── AGENT TOGGLE ───────────────────────────────────────────
function toggleAgent() {
  state.agentRunning = !state.agentRunning;
  updateStatusPill();
  const badge = document.getElementById('agent-badge');
  if(state.agentRunning) {
    addLog('OK','Agent started — auto-bake enabled');
    badge.textContent = 'ON'; badge.style.background = 'var(--green)';
  } else {
    addLog('WARN','Agent stopped by user');
    badge.textContent = 'OFF'; badge.style.background = 'var(--red)';
  }
}

function updateStatusPill() {
  const pill = document.getElementById('agent-status-pill');
  const label = document.getElementById('agent-status-label');
  pill.className = 'status-pill ' + (state.agentRunning ? 'running' : 'stopped');
  label.textContent = state.agentRunning ? 'Agent Running' : 'Agent Stopped';
}

function updateAgentToggle(key, val) {
  if(key === 'autobake') { state.autobake = val; document.getElementById('autobake-status').textContent = val ? 'ENABLED' : 'DISABLED'; document.getElementById('autobake-status').className = 'config-val ' + (val ? 'green' : 'red'); }
  else state.toggles[key] = val;
  addLog('INFO', key.toUpperCase() + ' ' + (val ? 'enabled' : 'disabled'));
}

// ─── BAKE ENGINE ────────────────────────────────────────────
function bakeOnce() {
  if(!state.agentRunning || !state.autobake) return;
  const output = Math.floor(state.cookieScale * state.effectiveMult);
  state.cookies += output;
  state.cookiesDelta += output;
  state.score += output;
  state.scoreDelta += output;
  state.bakes++;
  updateStats();
  addLog('OK', 'bake() confirmed · +' + output.toLocaleString() + ' cookies · score +' + output.toLocaleString());
}

function manualBake() {
  const output = Math.floor(state.cookieScale * state.effectiveMult);
  state.cookies += output;
  state.cookiesDelta += output;
  state.score += output;
  state.scoreDelta += output;
  state.bakes++;
  updateStats();
  addLog('OK', 'Manual bake() · +' + output.toLocaleString() + ' cookies');
}

// ─── TIMER ──────────────────────────────────────────────────
function updateTimer() {
  state.timerSec--;
  if(state.timerSec <= 0) {
    state.timerSec = state.timerMax;
    bakeOnce();
  }
  const circle = document.getElementById('timer-circle');
  const pct = state.timerSec / state.timerMax;
  circle.style.strokeDashoffset = 345 * (1 - pct);
  document.getElementById('timer-countdown').textContent = state.timerSec + 's';
}

function updateBoostTimers() {
  if(state.boostTimer1 > 0) state.boostTimer1--;
  if(state.boostTimer2 > 0) {
    state.boostTimer2--;
    state.eventTimer--;
  }
  document.getElementById('boost1-time').textContent = formatTime(state.boostTimer1);
  document.getElementById('boost2-time').textContent = formatTime(state.boostTimer2);
  document.getElementById('event-timer').textContent = formatTime(state.eventTimer);
}

function formatTime(s) {
  if(s <= 0) return 'EXPIRED';
  const m = Math.floor(s/60);
  const sec = s%60;
  return m + ':' + String(sec).padStart(2,'0');
}

// ─── STATS UPDATE ───────────────────────────────────────────
function updateStats() {
  document.getElementById('stat-cookies').textContent = state.cookies.toLocaleString();
  document.getElementById('stat-cookies-delta').textContent = '+' + state.cookiesDelta.toLocaleString() + ' this session';
  document.getElementById('stat-score').textContent = state.score.toLocaleString();
  document.getElementById('stat-score-delta').textContent = '+' + state.scoreDelta.toLocaleString() + ' today';
  document.getElementById('stat-bakes').textContent = state.bakes.toLocaleString();
  document.getElementById('stat-rank').textContent = '#' + state.rank;
}

// ─── LOG ────────────────────────────────────────────────────
function addLog(tag, msg) {
  const now = new Date();
  const t = now.getHours().toString().padStart(2,'0') + ':' + now.getMinutes().toString().padStart(2,'0') + ':' + now.getSeconds().toString().padStart(2,'0');
  state.logs.unshift({tag, msg, t});
  if(state.logs.length > 200) state.logs.pop();
  renderLog();
  state.logCount++;
  document.getElementById('log-badge').textContent = state.logCount > 99 ? '99+' : state.logCount;
}

function renderLog() {
  const c = document.getElementById('log-container');
  c.innerHTML = state.logs.slice(0,80).map(l =>
    `<div class="log-line"><span class="log-time">${l.t}</span><span class="log-tag ${l.tag.toLowerCase()}">${l.tag}</span><span class="log-msg">${l.msg}</span></div>`
  ).join('');
}

function clearLog() { state.logs = []; state.logCount = 0; renderLog(); document.getElementById('log-badge').textContent = '0'; }
function exportLog() {
  const text = state.logs.map(l => `[${l.t}] [${l.tag}] ${l.msg}`).join('\n');
  const a = document.createElement('a'); a.href = 'data:text/plain;charset=utf-8,' + encodeURIComponent(text);
  a.download = 'bakery-agent-log.txt'; a.click();
}

// ─── LEADERBOARD ────────────────────────────────────────────
function renderLeaderboard() {
  const total = leaderboardData.reduce((a,b) => a+b.score, 0);
  document.getElementById('lb-rows').innerHTML = leaderboardData.map((b,i) => `
    <div class="lb-row">
      <span class="lb-rank ${i<3?'top':''}">${i+1}</span>
      <span class="lb-name ${b.mine?'mine':''}">${b.name}</span>
      <span class="lb-score">${(b.score/1e6).toFixed(2)}M</span>
      <span class="lb-pct">${(b.score/total*100).toFixed(1)}%</span>
    </div>
  `).join('');
}

// ─── SYNC ───────────────────────────────────────────────────
function syncState() {
  addLog('INFO','Fetching /agent.json — checking live season state, VRF fee, buy-in...');
  setTimeout(() => {
    addLog('OK','agent.json synced · season=9 (S7) · scale=1000 · tierIds=[1,2]');
    document.getElementById('last-sync').textContent = new Date().toLocaleTimeString();
    document.getElementById('buyin-val').textContent = '~0.001 ETH';
    document.getElementById('vrf-val').textContent = '~0.0001 ETH';
  }, 800);
}

// ─── SETTINGS ───────────────────────────────────────────────
function saveSettings() {
  const addr = document.getElementById('wallet-input').value;
  if(addr) {
    document.getElementById('wallet-display').textContent = addr.slice(0,6) + '...' + addr.slice(-4);
    addLog('OK','Wallet updated · ' + addr.slice(0,8) + '...');
  }
}

function saveStrategy() {
  addLog('OK','Strategy saved · mode=' + document.getElementById('strategy-select').value);
}

function applyStrategy(val) {
  if(val === 'score') addLog('INFO','Strategy: Max Score — prioritize bake output, maintain boost uptime');
  if(val === 'cookies') addLog('INFO','Strategy: Max Cookies — bake aggressively, hold reserves');
  if(val === 'safe') addLog('INFO','Strategy: Safe Mode — no rugs sent, cleanup on incoming');
  if(val === 'custom') addLog('INFO','Strategy: Custom — configure manually below');
}

function selectSkill(s) {
  ['lucky','perfectionist','booster','sweeper'].forEach(k => {
    const el = document.getElementById('sk-'+k);
    if(el) { el.style.borderColor=''; el.style.background=''; el.querySelector('.toggle-label').style.color=''; }
  });
  const el = document.getElementById('sk-'+s);
  if(el) {
    el.style.borderColor='rgba(245,158,11,0.4)'; el.style.background='rgba(245,158,11,0.06)';
    el.querySelector('.toggle-label').style.color='var(--accent)';
  }
  addLog('INFO','Skill selected: ' + s + ' · claimSkill() requires server-signed grant');
}

// ─── INIT ───────────────────────────────────────────────────
function init() {
  updateStats();
  renderLeaderboard();
  addLog('OK','Agent initialized · Season 7 · Abstract mainnet (chain 2741)');
  addLog('INFO','Always fetch /agent.json before value-bearing actions');
  addLog('OK','Auto-bake active · 5-block cadence · Perfectionist skill loaded');
  addLog('INFO','Golden Batch event active · +20% bake output for 38 min');
  syncState();
}

// ─── TICK ───────────────────────────────────────────────────
setInterval(() => {
  updateTimer();
  updateBoostTimers();
}, 1000);

init();
</script>
</body>
</html>
