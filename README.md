<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0"/>
<meta name="theme-color" content="#0D1F0D"/>
<title>Edumobile — Coal City Learns</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=IBM+Plex+Sans:wght@400;500;600;700&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet"/>

<!-- =====================================================================
  EDUMOBILE — COAL CITY LEARNS
  Built for Enugu Smart Bus Digital Inclusion Platform
  -----------------------------------------------------------------------
  QUICK EDIT GUIDE
  All user-facing content lives in the CONFIG object inside <script>.
  Change names, modules, exam rules, cert details there — not in the HTML.
  Colors are CSS variables in :root — one place to retheme the whole app.
  ===================================================================== -->

<style>
/* ── THEME VARIABLES (edit here to retheme) ─────────────────────────── */
:root {
  --bg:           #0D1F0D;   /* main background */
  --bg-deep:      #0A180A;   /* darker background (status bar, nav) */
  --bg-card:      rgba(255,255,255,0.04);
  --green:        #4AC578;   /* completed / success */
  --amber:        #F5A623;   /* active / accent */
  --red:          #E85D5D;   /* error / warning */
  --text:         #FFFFFF;
  --text-muted:   rgba(255,255,255,0.45);
  --text-dim:     rgba(255,255,255,0.25);
  --border:       rgba(255,255,255,0.09);
  --serif:        'Playfair Display', Georgia, serif;
  --mono:         'IBM Plex Mono', 'Courier New', monospace;
  --sans:         'IBM Plex Sans', sans-serif;
  --radius-card:  18px;
  --radius-btn:   12px;
}

/* ── RESET ───────────────────────────────────────────────────────────── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
html { scroll-behavior: smooth; }
body {
  font-family: var(--sans);
  background: var(--bg);
  color: var(--text);
  min-height: 100vh;
  max-width: 430px;
  margin: 0 auto;
  position: relative;
  overflow-x: hidden;
}
::-webkit-scrollbar { display: none; }
button { font-family: var(--sans); }

/* ── ANIMATIONS ──────────────────────────────────────────────────────── */
@keyframes fadeUp  { from { opacity:0; transform:translateY(14px); } to { opacity:1; transform:translateY(0); } }
@keyframes spin    { to { transform: rotate(360deg); } }
@keyframes pulse   { 0%,100% { opacity:1; } 50% { opacity:.35; } }
@keyframes glow    { 0%,100% { box-shadow:0 0 12px rgba(245,166,35,0.25); } 50% { box-shadow:0 0 28px rgba(245,166,35,0.55); } }

.fade-up { animation: fadeUp 0.45s ease both; }
.d1{animation-delay:.05s} .d2{animation-delay:.10s} .d3{animation-delay:.15s}
.d4{animation-delay:.20s} .d5{animation-delay:.25s} .d6{animation-delay:.30s}

/* ── STATUS BAR ──────────────────────────────────────────────────────── */
#statusBar {
  background: var(--bg-deep);
  padding: 10px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: sticky;
  top: 0;
  z-index: 50;
  border-bottom: 1px solid var(--border);
}
.status-left  { display:flex; align-items:center; gap:8px; }
.status-dot   { width:8px; height:8px; border-radius:50%; background:var(--green); animation:pulse 2s infinite; }
.status-label { color:var(--text-muted); font-size:11px; font-family:var(--mono); letter-spacing:1px; }
.status-right { display:flex; align-items:center; gap:10px; }

.lite-btn {
  background: rgba(74,197,120,0.15);
  border: 1px solid rgba(74,197,120,0.4);
  border-radius: 6px; padding: 3px 9px;
  color: var(--green); font-size:10px;
  font-family: var(--mono); letter-spacing:.5px;
  cursor: pointer; transition: all .2s;
}
.lite-btn.off { background:rgba(255,255,255,0.07); border-color:rgba(255,255,255,0.15); color:var(--text-dim); }

/* ── HERO ────────────────────────────────────────────────────────────── */
#hero {
  background: linear-gradient(160deg,#122412 0%,#0D1F0D 60%,#091509 100%);
  padding: 24px 20px 0;
  position: relative;
  overflow: hidden;
}
#hero::before {
  content:''; position:absolute; inset:0; pointer-events:none;
  background:
    radial-gradient(circle at 80% 20%, rgba(245,166,35,0.07) 0%, transparent 55%),
    radial-gradient(circle at 15% 85%, rgba(74,197,120,0.05) 0%, transparent 50%);
}
.hero-top      { display:flex; justify-content:space-between; align-items:flex-start; margin-bottom:22px; position:relative; }
.hero-eyebrow  { color:var(--text-dim); font-size:11px; letter-spacing:2px; font-family:var(--mono); margin-bottom:5px; }
.hero-title    { color:#fff; font-size:22px; font-family:var(--serif); font-weight:900; line-height:1.25; }
.hero-title span { color:var(--amber); }
.avatar {
  width:44px; height:44px; border-radius:12px; font-size:20px; flex-shrink:0;
  background:linear-gradient(135deg,#1E3A1E,#2A4E2A);
  border:1.5px solid rgba(255,255,255,0.12);
  display:flex; align-items:center; justify-content:center;
}

/* ── PROGRESS CARD ───────────────────────────────────────────────────── */
.progress-card {
  background:var(--bg-card); border:1px solid var(--border);
  border-radius:20px; padding:18px; margin-bottom:18px;
  display:flex; align-items:center; gap:18px; position:relative;
}
.arc-wrap  { position:relative; flex-shrink:0; }
.arc-label {
  position:absolute; inset:0;
  display:flex; flex-direction:column; align-items:center; justify-content:center;
}
.arc-pct { color:#fff; font-size:22px; font-weight:700; font-family:var(--serif); line-height:1; }
.arc-sub  { color:var(--text-dim); font-size:9px; font-family:var(--mono); letter-spacing:1px; margin-top:2px; }
.prog-info    { flex:1; }
.prog-eyebrow { color:var(--text-muted); font-size:10px; letter-spacing:1.2px; font-family:var(--mono); margin-bottom:4px; }
.prog-count   { color:#fff; font-size:14px; font-weight:600; margin-bottom:10px; line-height:1.3; }
.module-bars  { display:flex; gap:5px; margin-bottom:12px; }
.mbar         { height:4px; flex:1; border-radius:2px; background:rgba(255,255,255,0.11); transition:background .4s; }
.mbar.done    { background:var(--green); }
.mbar.active  { background:var(--amber); }

.sync-btn {
  background:rgba(245,166,35,0.14); border:1.5px solid rgba(245,166,35,0.38);
  border-radius:10px; padding:8px 13px;
  color:var(--amber); font-size:12px; font-weight:600;
  cursor:pointer; display:flex; align-items:center; gap:6px; white-space:nowrap;
  transition:background .2s, transform .1s;
}
.sync-btn:active { transform:scale(.97); }

/* ── RESUME CTA ──────────────────────────────────────────────────────── */
.resume-cta {
  background:linear-gradient(135deg,rgba(245,166,35,0.14),rgba(245,166,35,0.04));
  border:1.5px solid rgba(245,166,35,0.24);
  border-radius:16px; padding:13px 16px; margin-bottom:24px;
  display:flex; align-items:center; justify-content:space-between;
  cursor:pointer; transition:border-color .2s, transform .1s;
}
.resume-cta:active { transform:scale(.99); }
.resume-icon  { width:40px; height:40px; background:rgba(245,166,35,0.18); border-radius:10px; display:flex; align-items:center; justify-content:center; font-size:19px; flex-shrink:0; }
.resume-meta  { flex:1; margin-left:12px; }
.resume-tag   { color:var(--text-dim); font-size:10px; letter-spacing:1.2px; font-family:var(--mono); margin-bottom:2px; }
.resume-title { color:#fff; font-size:14px; font-weight:600; }
.resume-sub   { color:var(--text-dim); font-size:11px; margin-top:2px; }
.play-btn {
  width:36px; height:36px; background:var(--amber); border-radius:10px; flex-shrink:0;
  display:flex; align-items:center; justify-content:center; transition:transform .15s;
}
.resume-cta:hover .play-btn { transform:scale(1.08); }

/* ── CONTENT + SECTION HEADERS ───────────────────────────────────────── */
#content   { padding:0 20px 130px; }
.sec-head  { display:flex; justify-content:space-between; align-items:center; margin:22px 0 13px; }
.sec-title { color:#fff; font-size:15px; font-family:var(--serif); font-weight:700; }
.sec-badge { color:var(--text-dim); font-size:11px; font-family:var(--mono); }

/* ── MODULE LIST ─────────────────────────────────────────────────────── */
.module-list  { display:flex; flex-direction:column; gap:10px; }
.module-item  {
  border-radius:16px; padding:13px 15px;
  display:flex; align-items:center; gap:13px;
  position:relative; overflow:hidden;
  transition:transform .15s, border-color .2s;
}
.module-item:not(.locked) { cursor:pointer; }
.module-item:not(.locked):active { transform:scale(.99); }
.module-item.done   { background:rgba(74,197,120,0.10);  border:1px solid rgba(74,197,120,0.28); }
.module-item.active { background:rgba(245,166,35,0.09);  border:1px solid rgba(245,166,35,0.32); }
.module-item.locked { background:rgba(255,255,255,0.03); border:1px solid rgba(255,255,255,0.08); }
.module-item.active::before {
  content:''; position:absolute; left:0; top:0; bottom:0; width:3px;
  background:var(--amber); border-radius:0 2px 2px 0;
}
.module-emoji { width:42px; height:42px; background:rgba(255,255,255,0.06); border-radius:12px; display:flex; align-items:center; justify-content:center; font-size:20px; flex-shrink:0; }
.module-item.locked .module-emoji { filter:grayscale(1) opacity(.35); }
.module-body { flex:1; min-width:0; }
.module-row  { display:flex; align-items:center; gap:6px; margin-bottom:3px; }
.module-name { color:#fff; font-size:14px; font-weight:600; }
.module-item.locked .module-name { color:rgba(255,255,255,0.24); }
.badge-active { background:rgba(245,166,35,0.18); color:var(--amber); font-size:9px; font-family:var(--mono); letter-spacing:.5px; padding:1px 6px; border-radius:4px; }
.module-meta  { color:var(--text-dim); font-size:11px; display:flex; gap:6px; align-items:center; }
.module-meta .sep    { opacity:.4; }
.module-meta .bus-id { font-family:var(--mono); }
.module-status       { width:28px; height:28px; border-radius:8px; display:flex; align-items:center; justify-content:center; flex-shrink:0; font-size:13px; }
.module-status.done   { background:rgba(74,197,120,0.15); color:var(--green); }
.module-status.active { background:rgba(245,166,35,0.15); color:var(--amber); }
.module-status.locked { background:rgba(255,255,255,0.05); color:var(--text-dim); }

/* ── CBT EXAM CARD (dashboard) ───────────────────────────────────────── */
.exam-card {
  background:rgba(255,255,255,0.03); border:1.5px solid var(--border);
  border-radius:var(--radius-card); padding:20px;
  position:relative; overflow:hidden; transition:border-color .3s;
}
.exam-card.unlocked { background:rgba(74,197,120,0.07); border-color:rgba(74,197,120,0.25); }
.exam-lock-overlay {
  position:absolute; inset:0; background:rgba(13,31,13,0.55);
  backdrop-filter:blur(2px); border-radius:var(--radius-card); z-index:3;
  display:flex; align-items:center; justify-content:center; flex-direction:column; gap:8px;
  transition:opacity .4s;
}
.exam-lock-overlay.hidden { opacity:0; pointer-events:none; }
.lock-icon { font-size:30px; }
.exam-lock-overlay p     { color:rgba(255,255,255,0.5); font-size:13px; font-weight:500; }
.exam-lock-overlay small { color:var(--text-dim); font-size:11px; }
.exam-head     { display:flex; justify-content:space-between; align-items:flex-start; margin-bottom:14px; }
.exam-eyebrow  { color:var(--text-muted); font-size:10px; letter-spacing:1.5px; font-family:var(--mono); margin-bottom:4px; }
.exam-title    { color:#fff; font-size:16px; font-weight:700; font-family:var(--serif); }
.time-pill     { background:rgba(245,166,35,0.1); border-radius:10px; padding:6px 10px; text-align:center; flex-shrink:0; }
.time-num      { color:var(--amber); font-size:18px; font-weight:700; line-height:1; }
.time-unit     { color:var(--text-dim); font-size:9px; font-family:var(--mono); }
.exam-tags     { display:flex; gap:8px; flex-wrap:wrap; margin-bottom:16px; }
.etag          { background:rgba(255,255,255,0.05); border:1px solid rgba(255,255,255,0.1); border-radius:6px; padding:4px 10px; color:rgba(255,255,255,0.4); font-size:11px; font-family:var(--mono); }

/* shared button base */
.btn-primary {
  width:100%; border:none; border-radius:var(--radius-btn); padding:15px;
  font-weight:700; font-size:15px; font-family:var(--sans);
  transition:background .3s, color .3s, transform .1s, opacity .2s;
}
.btn-primary:active { transform:scale(.98); }
.btn-locked   { background:rgba(255,255,255,0.05); color:rgba(255,255,255,0.22); cursor:not-allowed; }
.btn-green    { background:var(--green); color:#0D1F0D; cursor:pointer; animation:glow 2s infinite; }
.btn-amber    { background:var(--amber); color:#0D1F0D; cursor:pointer; }
.btn-outline  { background:rgba(255,255,255,0.04); border:1.5px solid rgba(255,255,255,0.1); color:rgba(255,255,255,0.3); cursor:not-allowed; }
.btn-outline.ready { background:rgba(245,166,35,0.12); border-color:rgba(245,166,35,0.35); color:var(--amber); cursor:pointer; }

/* ── CERT CARD (dashboard) ───────────────────────────────────────────── */
.cert-card {
  background:linear-gradient(135deg,#122412,#0A180A);
  border:1.5px solid rgba(255,255,255,0.1);
  border-radius:var(--radius-card); padding:20px;
  position:relative; overflow:hidden;
}
.cert-card::before { content:''; position:absolute; top:-30px; right:-30px; width:130px; height:130px; background:radial-gradient(circle,rgba(245,166,35,0.09),transparent 70%); pointer-events:none; }
.cert-card::after  { content:''; position:absolute; bottom:-20px; left:-20px; width:110px; height:110px; background:radial-gradient(circle,rgba(74,197,120,0.06),transparent 70%);  pointer-events:none; }
.cert-header     { display:flex; align-items:center; gap:10px; margin-bottom:16px; position:relative; z-index:1; }
.cert-eyebrow    { color:var(--text-dim); font-size:10px; letter-spacing:1.5px; font-family:var(--mono); margin-bottom:2px; }
.cert-name-title { color:#fff; font-size:14px; font-weight:600; }
.cert-id-box     { background:rgba(255,255,255,0.04); border-radius:12px; padding:11px 14px; margin-bottom:14px; position:relative; z-index:1; }
.cert-id-label   { color:var(--text-dim); font-size:9px; letter-spacing:1px; font-family:var(--mono); margin-bottom:4px; }
.cert-id-value   { color:var(--amber); font-size:13px; font-family:var(--mono); letter-spacing:1px; }
.cert-signers    { display:flex; gap:8px; margin-bottom:16px; position:relative; z-index:1; }
.signer          { flex:1; background:rgba(255,255,255,0.04); border:1px solid rgba(255,255,255,0.08); border-radius:10px; padding:8px 10px; text-align:center; }
.signer-label    { color:var(--text-dim); font-size:9px; font-family:var(--mono); letter-spacing:.5px; margin-bottom:2px; }
.signer-name     { color:rgba(255,255,255,0.6); font-size:11px; font-weight:500; line-height:1.25; }
.cert-footer     { color:rgba(255,255,255,0.2); font-size:10px; text-align:center; margin-top:10px; font-family:var(--mono); line-height:1.6; position:relative; z-index:1; }

/* ── BOTTOM NAV ──────────────────────────────────────────────────────── */
#bottomNav {
  position:fixed; bottom:0; left:50%; transform:translateX(-50%);
  width:100%; max-width:430px;
  background:rgba(10,24,10,0.96); backdrop-filter:blur(20px);
  border-top:1px solid rgba(255,255,255,0.08);
  padding:10px 20px 22px; z-index:50;
}
.nav-items { display:flex; justify-content:space-around; }
.nav-item  { flex:1; background:transparent; border:none; cursor:pointer; padding:6px 4px; display:flex; flex-direction:column; align-items:center; gap:4px; position:relative; }
.nav-item::before { content:''; position:absolute; top:-10px; left:50%; transform:translateX(-50%); width:32px; height:3px; background:var(--amber); border-radius:0 0 4px 4px; opacity:0; transition:opacity .2s; }
.nav-item.active::before { opacity:1; }
.nav-emoji { font-size:20px; line-height:1; filter:grayscale(1) opacity(.38); transition:filter .2s; }
.nav-item.active .nav-emoji { filter:none; }
.nav-label { font-size:10px; font-family:var(--mono); letter-spacing:.3px; color:var(--text-dim); transition:color .2s; }
.nav-item.active .nav-label { color:var(--amber); font-weight:600; }

/* ── MODAL ───────────────────────────────────────────────────────────── */
#modalOverlay {
  position:fixed; inset:0; background:rgba(0,0,0,0.72); z-index:100;
  display:flex; align-items:flex-end;
  opacity:0; pointer-events:none; transition:opacity .25s;
}
#modalOverlay.open { opacity:1; pointer-events:all; }
#modalSheet {
  background:#1A2E1A; width:100%; border-radius:24px 24px 0 0;
  padding:28px 24px 44px;
  transform:translateY(100%); transition:transform .3s cubic-bezier(.4,0,.2,1);
}
#modalOverlay.open #modalSheet { transform:translateY(0); }
.sheet-handle    { width:40px; height:4px; background:rgba(255,255,255,0.18); border-radius:2px; margin:0 auto 24px; }
.sheet-title-row { display:flex; align-items:center; gap:10px; margin-bottom:6px; }
.sheet-title     { color:#fff; font-size:18px; font-family:var(--serif); font-weight:700; }
.sheet-sub       { color:rgba(255,255,255,0.5); font-size:13px; margin-bottom:22px; line-height:1.55; }
#phaseInput    { display:block; }
#phaseScanning { display:none; }
#phaseSynced   { display:none; }
.input-row  { display:flex; gap:10px; margin-bottom:15px; }
.bus-input  {
  flex:1; background:rgba(255,255,255,0.07); border:1.5px solid rgba(255,255,255,0.15);
  border-radius:12px; padding:13px 16px; color:#fff; font-size:16px;
  font-family:var(--mono); letter-spacing:2px; outline:none; transition:border-color .2s;
}
.bus-input:focus { border-color:rgba(245,166,35,0.5); }
.qr-btn     { background:rgba(245,166,35,0.12); border:1.5px solid rgba(245,166,35,0.35); border-radius:12px; padding:0 15px; color:var(--amber); cursor:pointer; font-size:18px; transition:background .2s; }
.qr-btn:hover { background:rgba(245,166,35,0.2); }
.cancel-btn { width:100%; background:transparent; border:none; color:rgba(255,255,255,0.35); padding:13px; cursor:pointer; font-size:14px; margin-top:4px; }
.spinner    { width:48px; height:48px; border:3px solid var(--amber); border-top-color:transparent; border-radius:50%; margin:0 auto 16px; animation:spin .8s linear infinite; }
.scanning-text { color:rgba(255,255,255,0.55); font-size:14px; text-align:center; }
.synced-icon   { width:56px; height:56px; background:rgba(74,197,120,0.15); border-radius:50%; display:flex; align-items:center; justify-content:center; margin:0 auto 14px; font-size:26px; color:var(--green); }
.synced-title  { color:var(--green); font-weight:700; font-size:16px; text-align:center; margin-bottom:6px; }
.synced-sub    { color:rgba(255,255,255,0.45); font-size:13px; text-align:center; margin-bottom:22px; }

/* ── PAGES ───────────────────────────────────────────────────────────── */
.page              { display:none; animation:fadeUp .35s ease; }
.page.active       { display:block; }
#pageDashboard     { display:block; padding:0; }
#pageDashboard.active { display:block; }
.page-body         { padding:20px 20px 130px; }
.page-hero         { background:linear-gradient(135deg,#122412,#0A180A); padding:24px 20px 20px; border-bottom:1px solid var(--border); }
.page-title        { color:#fff; font-family:var(--serif); font-size:22px; font-weight:900; margin-bottom:4px; }
.page-sub          { color:var(--text-muted); font-size:13px; }

/* ── MODULES PAGE ────────────────────────────────────────────────────── */
.lesson-card { background:var(--bg-card); border:1px solid var(--border); border-radius:16px; padding:16px; margin-bottom:12px; cursor:pointer; transition:transform .15s, border-color .2s; }
.lesson-card:hover  { border-color:rgba(255,255,255,0.18); transform:translateY(-1px); }
.lesson-card:active { transform:scale(.99); }
.lesson-card.active-card { border-color:rgba(245,166,35,0.3); background:rgba(245,166,35,0.06); }
.lesson-card.locked-card { opacity:.5; cursor:not-allowed; }
.lesson-head  { display:flex; justify-content:space-
