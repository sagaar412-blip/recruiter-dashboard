<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>RecruiterOS — Naukri Intelligence Platform</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

:root {
  --bg: #0a0a0f;
  --bg2: #111118;
  --bg3: #18181f;
  --border: #2a2a35;
  --border2: #1e1e28;
  --text: #f0f0f5;
  --text2: #8888a0;
  --text3: #55556a;
  --accent: #f97316;
  --accent2: #fb923c;
  --accentdim: rgba(249,115,22,0.12);
  --accentglow: rgba(249,115,22,0.25);
  --green: #22c55e;
  --greendim: rgba(34,197,94,0.12);
  --blue: #3b82f6;
  --bluedim: rgba(59,130,246,0.12);
  --purple: #a855f7;
  --purpledim: rgba(168,85,247,0.12);
  --red: #ef4444;
  --reddim: rgba(239,68,68,0.12);
  --radius: 10px;
  --radius-lg: 16px;
  --shadow: 0 4px 24px rgba(0,0,0,0.4);
}

html, body { height: 100%; background: var(--bg); color: var(--text); font-family: 'DM Sans', sans-serif; font-size: 14px; line-height: 1.6; overflow: hidden; }

/* ── Scrollbar ── */
::-webkit-scrollbar { width: 4px; height: 4px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: var(--border); border-radius: 4px; }

/* ── Layout ── */
#app { display: flex; height: 100vh; }

/* ── Sidebar ── */
.sidebar {
  width: 220px; min-width: 220px;
  background: var(--bg2);
  border-right: 1px solid var(--border2);
  display: flex; flex-direction: column;
  padding: 0;
  position: relative;
  z-index: 10;
}
.sidebar-logo {
  padding: 20px 20px 16px;
  border-bottom: 1px solid var(--border2);
}
.logo-mark {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 18px;
  color: var(--text);
  letter-spacing: -0.5px;
  display: flex; align-items: center; gap: 8px;
}
.logo-dot { width: 8px; height: 8px; background: var(--accent); border-radius: 50%; flex-shrink: 0; animation: pulse 2s infinite; }
@keyframes pulse { 0%,100% { opacity:1; box-shadow: 0 0 0 0 var(--accentglow); } 50% { opacity:.9; box-shadow: 0 0 0 6px transparent; } }
.logo-sub { font-size: 10px; color: var(--text3); font-weight: 400; font-family: 'DM Sans', sans-serif; letter-spacing: 0.5px; margin-top: 2px; }

.sidebar-nav { flex: 1; padding: 12px 10px; overflow-y: auto; }
.nav-section-label { font-size: 10px; font-weight: 600; color: var(--text3); letter-spacing: 1px; text-transform: uppercase; padding: 8px 10px 4px; }
.nav-item {
  display: flex; align-items: center; gap: 10px;
  padding: 9px 10px; border-radius: 8px;
  color: var(--text2); font-size: 13px; font-weight: 500;
  cursor: pointer; transition: all 0.15s;
  margin-bottom: 1px; user-select: none;
}
.nav-item:hover { background: var(--bg3); color: var(--text); }
.nav-item.active { background: var(--accentdim); color: var(--accent); }
.nav-item .icon { font-size: 15px; width: 18px; text-align: center; flex-shrink: 0; }
.nav-badge { margin-left: auto; background: var(--accent); color: white; font-size: 10px; font-weight: 700; padding: 1px 6px; border-radius: 20px; }

.sidebar-footer { padding: 12px 10px; border-top: 1px solid var(--border2); }
.token-display {
  background: var(--bg3); border: 1px solid var(--border);
  border-radius: 8px; padding: 10px 12px;
  font-size: 11px; color: var(--text2);
}
.token-display .token-label { font-size: 9px; text-transform: uppercase; letter-spacing: 1px; color: var(--text3); margin-bottom: 4px; }
.token-val { font-family: 'DM Mono', monospace; font-size: 11px; color: var(--text2); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.token-status { display: flex; align-items: center; gap: 4px; margin-top: 6px; }
.status-dot { width: 6px; height: 6px; border-radius: 50%; background: var(--green); flex-shrink: 0; }
.status-dot.off { background: var(--red); }

/* ── Main ── */
.main { flex: 1; display: flex; flex-direction: column; overflow: hidden; }

/* ── Header ── */
.topbar {
  height: 56px; min-height: 56px;
  border-bottom: 1px solid var(--border2);
  display: flex; align-items: center;
  padding: 0 24px; gap: 16px;
  background: var(--bg2);
}
.topbar-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 16px; flex: 1; }
.topbar-actions { display: flex; align-items: center; gap: 8px; }

/* ── Buttons ── */
.btn {
  display: inline-flex; align-items: center; gap: 6px;
  padding: 8px 14px; border-radius: 8px; border: none;
  font-family: 'DM Sans', sans-serif; font-size: 13px; font-weight: 600;
  cursor: pointer; transition: all 0.15s; white-space: nowrap;
}
.btn-primary { background: var(--accent); color: white; }
.btn-primary:hover { background: var(--accent2); transform: translateY(-1px); box-shadow: 0 4px 12px var(--accentglow); }
.btn-secondary { background: var(--bg3); color: var(--text); border: 1px solid var(--border); }
.btn-secondary:hover { border-color: var(--accent); color: var(--accent); }
.btn-ghost { background: transparent; color: var(--text2); }
.btn-ghost:hover { background: var(--bg3); color: var(--text); }
.btn-sm { padding: 5px 10px; font-size: 12px; border-radius: 6px; }
.btn-danger { background: var(--reddim); color: var(--red); border: 1px solid var(--red); }
.btn:disabled { opacity: 0.5; cursor: not-allowed; transform: none !important; }

/* ── Content ── */
.content { flex: 1; overflow-y: auto; padding: 24px; }

/* ── Stats ── */
.stats-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 16px; margin-bottom: 24px; }
.stat-card {
  background: var(--bg2); border: 1px solid var(--border2);
  border-radius: var(--radius-lg); padding: 20px;
  position: relative; overflow: hidden;
  transition: border-color 0.2s;
}
.stat-card:hover { border-color: var(--border); }
.stat-card::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px;
  background: var(--accent-color, var(--accent));
}
.stat-card.green::before { --accent-color: var(--green); }
.stat-card.blue::before { --accent-color: var(--blue); }
.stat-card.purple::before { --accent-color: var(--purple); }
.stat-icon { font-size: 22px; margin-bottom: 10px; }
.stat-value { font-family: 'Syne', sans-serif; font-weight: 800; font-size: 32px; color: var(--text); line-height: 1; }
.stat-label { font-size: 12px; color: var(--text2); margin-top: 4px; }
.stat-sub { font-size: 11px; color: var(--text3); margin-top: 8px; }

/* ── Cards / Tables ── */
.card {
  background: var(--bg2); border: 1px solid var(--border2);
  border-radius: var(--radius-lg); overflow: hidden;
}
.card-header {
  display: flex; align-items: center; justify-content: space-between;
  padding: 16px 20px; border-bottom: 1px solid var(--border2);
}
.card-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 14px; }

/* ── Search/Filter bar ── */
.filter-bar { display: flex; gap: 10px; padding: 14px 20px; border-bottom: 1px solid var(--border2); align-items: center; }
.search-wrap { position: relative; flex: 1; }
.search-wrap input {
  width: 100%; padding: 8px 12px 8px 34px;
  background: var(--bg3); border: 1px solid var(--border);
  border-radius: 8px; color: var(--text); font-family: 'DM Sans', sans-serif; font-size: 13px;
  outline: none; transition: border-color 0.15s;
}
.search-wrap input:focus { border-color: var(--accent); }
.search-icon { position: absolute; left: 10px; top: 50%; transform: translateY(-50%); color: var(--text3); font-size: 14px; pointer-events: none; }
.filter-select {
  padding: 8px 12px; background: var(--bg3); border: 1px solid var(--border);
  border-radius: 8px; color: var(--text2); font-family: 'DM Sans', sans-serif; font-size: 13px;
  outline: none; cursor: pointer;
}
.filter-select:focus { border-color: var(--accent); }

/* ── Candidate Table ── */
.table-wrap { overflow-x: auto; }
table { width: 100%; border-collapse: collapse; }
thead th {
  text-align: left; padding: 10px 20px;
  font-size: 10px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.8px;
  color: var(--text3); background: var(--bg);
  border-bottom: 1px solid var(--border2);
}
tbody tr {
  border-bottom: 1px solid var(--border2);
  transition: background 0.1s; cursor: pointer;
}
tbody tr:hover { background: var(--bg3); }
tbody tr:last-child { border-bottom: none; }
td { padding: 12px 20px; vertical-align: middle; }

/* ── Candidate Row ── */
.cand-name { font-weight: 600; color: var(--text); font-size: 13px; }
.cand-title { font-size: 12px; color: var(--text2); margin-top: 1px; }
.cand-email { font-size: 12px; color: var(--text2); font-family: 'DM Mono', monospace; }
.cand-phone { font-size: 12px; color: var(--text2); font-family: 'DM Mono', monospace; }

/* ── Tags / Chips ── */
.chip {
  display: inline-flex; align-items: center; gap: 4px;
  padding: 3px 8px; border-radius: 20px; font-size: 11px; font-weight: 500;
  white-space: nowrap;
}
.chip-orange { background: var(--accentdim); color: var(--accent); border: 1px solid rgba(249,115,22,0.2); }
.chip-green { background: var(--greendim); color: var(--green); border: 1px solid rgba(34,197,94,0.2); }
.chip-blue { background: var(--bluedim); color: var(--blue); border: 1px solid rgba(59,130,246,0.2); }
.chip-purple { background: var(--purpledim); color: var(--purple); border: 1px solid rgba(168,85,247,0.2); }
.chip-gray { background: var(--bg3); color: var(--text2); border: 1px solid var(--border); }

/* ── Empty state ── */
.empty { text-align: center; padding: 60px 20px; }
.empty-icon { font-size: 40px; margin-bottom: 12px; opacity: 0.4; }
.empty-title { font-family: 'Syne', sans-serif; font-size: 16px; font-weight: 700; color: var(--text2); }
.empty-sub { font-size: 13px; color: var(--text3); margin-top: 6px; }

/* ── Loading ── */
.skeleton { background: linear-gradient(90deg, var(--bg3) 25%, var(--border2) 50%, var(--bg3) 75%); background-size: 200% 100%; animation: shimmer 1.5s infinite; border-radius: 6px; }
@keyframes shimmer { 0% { background-position: -200% 0; } 100% { background-position: 200% 0; } }
.loading-row td { padding: 16px 20px; }
.skel-line { height: 12px; border-radius: 4px; }

/* ── Modal ── */
.modal-overlay {
  position: fixed; inset: 0; background: rgba(0,0,0,0.7);
  z-index: 1000; display: flex; align-items: center; justify-content: center;
  backdrop-filter: blur(4px);
  animation: fadeIn 0.15s ease;
}
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
.modal {
  background: var(--bg2); border: 1px solid var(--border);
  border-radius: var(--radius-lg); width: 680px; max-width: 95vw;
  max-height: 85vh; display: flex; flex-direction: column;
  box-shadow: var(--shadow);
  animation: slideUp 0.2s ease;
}
@keyframes slideUp { from { transform: translateY(20px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
.modal-header { padding: 20px 24px; border-bottom: 1px solid var(--border2); display: flex; align-items: center; justify-content: space-between; flex-shrink: 0; }
.modal-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 16px; }
.modal-body { padding: 24px; overflow-y: auto; flex: 1; }
.modal-footer { padding: 16px 24px; border-top: 1px solid var(--border2); display: flex; justify-content: flex-end; gap: 10px; flex-shrink: 0; }
.close-btn { background: var(--bg3); border: 1px solid var(--border); border-radius: 6px; color: var(--text2); width: 28px; height: 28px; display: flex; align-items: center; justify-content: center; cursor: pointer; font-size: 16px; }
.close-btn:hover { color: var(--text); border-color: var(--accent); }

/* ── Profile sections ── */
.profile-hero { display: flex; align-items: flex-start; gap: 16px; margin-bottom: 20px; }
.profile-avatar { width: 52px; height: 52px; border-radius: 12px; background: var(--accentdim); border: 2px solid var(--accent); display: flex; align-items: center; justify-content: center; font-family: 'Syne', sans-serif; font-weight: 800; font-size: 20px; color: var(--accent); flex-shrink: 0; }
.profile-name { font-family: 'Syne', sans-serif; font-weight: 800; font-size: 20px; color: var(--text); }
.profile-sub { font-size: 13px; color: var(--text2); margin-top: 3px; }
.profile-meta { display: flex; gap: 12px; flex-wrap: wrap; margin-top: 8px; }
.meta-item { display: flex; align-items: center; gap: 5px; font-size: 12px; color: var(--text2); }

.section-label { font-size: 10px; font-weight: 700; text-transform: uppercase; letter-spacing: 1px; color: var(--text3); margin-bottom: 10px; margin-top: 20px; }
.info-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
.info-item { background: var(--bg3); border: 1px solid var(--border2); border-radius: 8px; padding: 10px 12px; }
.info-label { font-size: 10px; color: var(--text3); text-transform: uppercase; letter-spacing: 0.5px; margin-bottom: 3px; }
.info-value { font-size: 13px; color: var(--text); font-weight: 500; }

.skills-wrap { display: flex; flex-wrap: wrap; gap: 6px; }

.work-item { display: flex; gap: 12px; margin-bottom: 12px; }
.work-dot { width: 8px; height: 8px; border-radius: 50%; background: var(--accent); flex-shrink: 0; margin-top: 5px; }
.work-content { flex: 1; }
.work-title { font-weight: 600; font-size: 13px; color: var(--text); }
.work-company { font-size: 12px; color: var(--text2); }
.work-dates { font-size: 11px; color: var(--text3); font-family: 'DM Mono', monospace; margin-top: 2px; }
.work-desc { font-size: 12px; color: var(--text2); margin-top: 4px; line-height: 1.5; }

/* ── Form ── */
.form-group { margin-bottom: 16px; }
.form-label { display: block; font-size: 12px; font-weight: 600; color: var(--text2); margin-bottom: 6px; }
.form-input, .form-select, .form-textarea {
  width: 100%; padding: 9px 12px;
  background: var(--bg3); border: 1px solid var(--border);
  border-radius: 8px; color: var(--text); font-family: 'DM Sans', sans-serif; font-size: 13px;
  outline: none; transition: border-color 0.15s;
}
.form-input:focus, .form-select:focus, .form-textarea:focus { border-color: var(--accent); }
.form-textarea { resize: vertical; min-height: 80px; }
.form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }

/* ── Jobs grid ── */
.jobs-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; }
.job-card {
  background: var(--bg2); border: 1px solid var(--border2);
  border-radius: var(--radius-lg); padding: 20px;
  cursor: pointer; transition: all 0.15s;
  position: relative; overflow: hidden;
}
.job-card:hover { border-color: var(--border); transform: translateY(-2px); box-shadow: var(--shadow); }
.job-card.selected { border-color: var(--accent); background: var(--accentdim); }
.job-card::after { content: ''; position: absolute; bottom: 0; left: 0; right: 0; height: 2px; background: var(--accent); opacity: 0; transition: opacity 0.15s; }
.job-card:hover::after { opacity: 1; }
.job-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 14px; color: var(--text); margin-bottom: 6px; }
.job-location { font-size: 12px; color: var(--text2); display: flex; align-items: center; gap: 4px; margin-bottom: 12px; }
.job-stats { display: flex; gap: 12px; }
.job-stat { text-align: center; }
.job-stat-n { font-family: 'Syne', sans-serif; font-weight: 800; font-size: 20px; color: var(--accent); }
.job-stat-l { font-size: 10px; color: var(--text3); }

/* ── Toast ── */
.toast-container { position: fixed; bottom: 20px; right: 20px; z-index: 9999; display: flex; flex-direction: column; gap: 8px; }
.toast {
  background: var(--bg2); border: 1px solid var(--border);
  border-radius: 10px; padding: 12px 16px;
  display: flex; align-items: center; gap: 10px;
  font-size: 13px; min-width: 260px; max-width: 360px;
  box-shadow: var(--shadow);
  animation: toastIn 0.2s ease;
}
@keyframes toastIn { from { transform: translateX(20px); opacity: 0; } to { transform: translateX(0); opacity: 1; } }
.toast.success { border-left: 3px solid var(--green); }
.toast.error { border-left: 3px solid var(--red); }
.toast.info { border-left: 3px solid var(--blue); }
.toast-icon { font-size: 16px; }

/* ── Setup page ── */
.setup-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
.setup-card { background: var(--bg2); border: 1px solid var(--border2); border-radius: var(--radius-lg); padding: 24px; }
.setup-step { display: flex; gap: 14px; margin-bottom: 16px; }
.step-num { width: 28px; height: 28px; border-radius: 50%; background: var(--accentdim); border: 1px solid var(--accent); color: var(--accent); font-weight: 800; font-size: 13px; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
.step-body { flex: 1; }
.step-title { font-weight: 600; font-size: 13px; color: var(--text); margin-bottom: 4px; }
.step-desc { font-size: 12px; color: var(--text2); line-height: 1.5; }
.code-block { background: var(--bg); border: 1px solid var(--border2); border-radius: 8px; padding: 12px 14px; font-family: 'DM Mono', monospace; font-size: 12px; color: var(--text2); margin-top: 8px; word-break: break-all; position: relative; }
.copy-btn { position: absolute; top: 6px; right: 6px; background: var(--bg3); border: 1px solid var(--border); border-radius: 5px; color: var(--text3); font-size: 11px; padding: 3px 8px; cursor: pointer; }
.copy-btn:hover { color: var(--text); }

/* ── Dashboard activity feed ── */
.activity-item { display: flex; gap: 12px; padding: 12px 20px; border-bottom: 1px solid var(--border2); }
.activity-item:last-child { border-bottom: none; }
.activity-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; margin-top: 5px; }
.activity-text { font-size: 13px; color: var(--text); flex: 1; }
.activity-time { font-size: 11px; color: var(--text3); font-family: 'DM Mono', monospace; }

/* ── Scroll area ── */
.scroll-area { overflow-y: auto; }

/* ── Pipeline ── */
.pipeline { display: flex; gap: 12px; padding: 0 0 4px; overflow-x: auto; }
.pipeline-col { min-width: 200px; flex-shrink: 0; }
.pipeline-col-header { display: flex; justify-content: space-between; align-items: center; padding: 10px 12px; background: var(--bg3); border-radius: 8px 8px 0 0; border: 1px solid var(--border2); border-bottom: none; }
.pipeline-col-title { font-size: 12px; font-weight: 700; color: var(--text2); }
.pipeline-col-count { font-size: 11px; color: var(--text3); background: var(--bg2); padding: 2px 7px; border-radius: 20px; border: 1px solid var(--border2); }
.pipeline-col-body { background: var(--bg); border: 1px solid var(--border2); border-radius: 0 0 8px 8px; min-height: 200px; padding: 8px; }
.pipeline-card { background: var(--bg2); border: 1px solid var(--border2); border-radius: 8px; padding: 10px 12px; margin-bottom: 8px; cursor: pointer; transition: border-color 0.15s; }
.pipeline-card:hover { border-color: var(--accent); }
.pipeline-card-name { font-size: 13px; font-weight: 600; color: var(--text); }
.pipeline-card-sub { font-size: 11px; color: var(--text2); margin-top: 2px; }

/* ── Token input screen ── */
.token-screen { display: flex; align-items: center; justify-content: center; height: 100vh; background: var(--bg); }
.token-box { width: 400px; background: var(--bg2); border: 1px solid var(--border); border-radius: 20px; padding: 36px; }
.token-logo { font-family: 'Syne', sans-serif; font-weight: 800; font-size: 24px; margin-bottom: 6px; }
.token-sub { color: var(--text2); font-size: 13px; margin-bottom: 28px; }

/* ── Pagination ── */
.pagination { display: flex; align-items: center; justify-content: space-between; padding: 12px 20px; border-top: 1px solid var(--border2); }
.page-info { font-size: 12px; color: var(--text3); }
.page-btns { display: flex; gap: 4px; }
.page-btn { width: 30px; height: 30px; border-radius: 6px; display: flex; align-items: center; justify-content: center; font-size: 12px; cursor: pointer; border: 1px solid var(--border2); background: var(--bg3); color: var(--text2); transition: all 0.1s; }
.page-btn:hover, .page-btn.active { background: var(--accentdim); color: var(--accent); border-color: var(--accent); }
.page-btn:disabled { opacity: 0.4; cursor: not-allowed; }
</style>
</head>
<body>
<div id="app"></div>

<script>
const API_BASE = "https://blessed-salamander-994.convex.site";
const PAGE_SIZE = 25;

// ── State ──────────────────────────────────────────────────────────────────────
let state = {
  token: (localStorage.getItem("ra_token") || "").replace(/[^\x20-\x7E]/g, "").trim(),
  page: "dashboard",
  candidates: [],
  jobs: [],
  loading: false,
  candidatePage: 1,
  searchQuery: "",
  jobFilter: "",
  selectedCandidate: null,
  selectedJob: null,
  toasts: [],
  showNewJob: false,
  showSettings: false,
  stats: { total: 0, today: 0, thisWeek: 0, jobs: 0 },
};

// ── API ────────────────────────────────────────────────────────────────────────
// Sanitize token: strip any non-ASCII / non-printable characters that would
// cause "non ISO-8859-1 code point" header errors.
function cleanToken(t) {
  return (t || "").replace(/[^\x20-\x7E]/g, "").trim();
}

async function api(path, opts = {}) {
  const token = cleanToken(state.token);
  const res = await fetch(API_BASE + path, {
    ...opts,
    headers: {
      "Content-Type": "application/json",
      ...(token ? { "Authorization": "Bearer " + token } : {}),
      ...(opts.headers || {}),
    },
  });
  if (!res.ok) {
    const e = await res.json().catch(() => ({}));
    throw new Error(e.error || "HTTP " + res.status);
  }
  return res.json();
}

async function loadJobs() {
  try {
    const data = await api("/ext/jobs");
    state.jobs = data.jobs || [];
  } catch(e) {
    showToast("Failed to load jobs: " + e.message, "error");
  }
}

async function loadCandidates() {
  state.loading = true;
  render();
  try {
    // Try fetching candidates — fall back gracefully if endpoint varies
    const data = await api("/ext/candidates" + (state.jobFilter ? `?jobId=${state.jobFilter}` : ""));
    state.candidates = data.candidates || data.data || [];
    // Compute stats
    const now = Date.now();
    const dayMs = 86400000;
    state.stats = {
      total: state.candidates.length,
      today: state.candidates.filter(c => now - new Date(c._creationTime || c.createdAt || 0).getTime() < dayMs).length,
      thisWeek: state.candidates.filter(c => now - new Date(c._creationTime || c.createdAt || 0).getTime() < 7 * dayMs).length,
      jobs: state.jobs.length,
    };
  } catch(e) {
    // Backend might not have this endpoint yet — show empty with message
    state.candidates = [];
    state.stats = { total: 0, today: 0, thisWeek: 0, jobs: state.jobs.length };
  }
  state.loading = false;
  render();
}

async function createJob(jobData) {
  const data = await api("/ext/jobs", { method: "POST", body: JSON.stringify(jobData) });
  await loadJobs();
  showToast("Job created!", "success");
  return data;
}

async function deleteCandidate(id) {
  try {
    await api(`/ext/candidates/${id}`, { method: "DELETE" });
    state.candidates = state.candidates.filter(c => c._id !== id);
    state.selectedCandidate = null;
    showToast("Candidate removed", "info");
    render();
  } catch(e) {
    showToast("Delete failed: " + e.message, "error");
  }
}

// ── Toast ──────────────────────────────────────────────────────────────────────
function showToast(msg, type = "info") {
  const id = Date.now();
  state.toasts.push({ id, msg, type });
  render();
  setTimeout(() => {
    state.toasts = state.toasts.filter(t => t.id !== id);
    render();
  }, 4000);
}

function copyToClipboard(text) {
  navigator.clipboard.writeText(text).then(() => showToast("Copied!", "success"));
}

// ── Helpers ───────────────────────────────────────────────────────────────────
function timeAgo(ts) {
  if (!ts) return "—";
  const diff = Date.now() - new Date(ts).getTime();
  const mins = Math.floor(diff / 60000);
  if (mins < 1) return "just now";
  if (mins < 60) return `${mins}m ago`;
  const hrs = Math.floor(mins / 60);
  if (hrs < 24) return `${hrs}h ago`;
  const days = Math.floor(hrs / 24);
  return `${days}d ago`;
}

function fmt(v, fallback = "—") { return v || fallback; }

function initials(name) {
  if (!name) return "?";
  return name.split(" ").filter(Boolean).slice(0, 2).map(w => w[0]).join("").toUpperCase();
}

function filteredCandidates() {
  let list = state.candidates;
  if (state.searchQuery) {
    const q = state.searchQuery.toLowerCase();
    list = list.filter(c =>
      (c.name||"").toLowerCase().includes(q) ||
      (c.email||"").toLowerCase().includes(q) ||
      (c.currentTitle||"").toLowerCase().includes(q) ||
      (c.currentCompany||"").toLowerCase().includes(q) ||
      (c.location||"").toLowerCase().includes(q) ||
      (c.skills||[]).some(s => s.toLowerCase().includes(q))
    );
  }
  if (state.jobFilter) {
    list = list.filter(c => c.jobId === state.jobFilter);
  }
  return list;
}

function pagedCandidates() {
  const list = filteredCandidates();
  const start = (state.candidatePage - 1) * PAGE_SIZE;
  return { list: list.slice(start, start + PAGE_SIZE), total: list.length };
}

// ── Raw data parsing (from rawData JSON string) ────────────────────────────────
function parseRaw(c) {
  try { return c._rawData ? JSON.parse(c._rawData) : (c.rawData ? JSON.parse(c.rawData) : {}); }
  catch { return {}; }
}

// ── RENDER ─────────────────────────────────────────────────────────────────────
function render() {
  const app = document.getElementById("app");
  if (!state.token) { app.innerHTML = renderTokenScreen(); bindTokenScreen(); return; }
  app.innerHTML = renderShell();
  bindShell();
}

function renderTokenScreen() {
  return `
  <div class="token-screen">
    <div class="token-box">
      <div class="logo-mark" style="margin-bottom:8px"><div class="logo-dot"></div>RecruiterOS</div>
      <div class="token-sub">Paste your auth token from the Recruiter App to connect your dashboard.</div>
      <div class="form-group">
        <label class="form-label">Auth Token</label>
        <input class="form-input" id="tokenInput" type="password" placeholder="ra_live_..." autocomplete="off" />
      </div>
      <button class="btn btn-primary" style="width:100%" id="tokenSubmit">Connect Dashboard →</button>
      <div style="margin-top:16px;font-size:12px;color:var(--text3)">Get your token from the Recruiter App → Settings → Extension Setup</div>
    </div>
  </div>`;
}

function bindTokenScreen() {
  document.getElementById("tokenSubmit").onclick = async () => {
    const val = document.getElementById("tokenInput").value.trim();
    if (!val) return;
    state.token = cleanToken(val);
    localStorage.setItem("ra_token", state.token);
    await loadJobs();
    await loadCandidates();
    render();
  };
  document.getElementById("tokenInput").onkeydown = e => {
    if (e.key === "Enter") document.getElementById("tokenSubmit").click();
  };
}

function renderShell() {
  return `
  ${renderToasts()}
  <div class="sidebar">
    ${renderSidebar()}
  </div>
  <div class="main">
    <div class="topbar">
      ${renderTopbar()}
    </div>
    <div class="content" id="mainContent">
      ${renderPage()}
    </div>
  </div>
  ${state.selectedCandidate ? renderCandidateModal() : ""}
  ${state.showNewJob ? renderNewJobModal() : ""}
  ${state.showSettings ? renderSettingsModal() : ""}
  `;
}

function renderSidebar() {
  const nav = (id, icon, label, badge) => `
    <div class="nav-item ${state.page === id ? 'active' : ''}" data-nav="${id}">
      <span class="icon">${icon}</span> ${label}
      ${badge ? `<span class="nav-badge">${badge}</span>` : ""}
    </div>`;
  return `
  <div class="sidebar-logo">
    <div class="logo-mark"><div class="logo-dot"></div>RecruiterOS</div>
    <div class="logo-sub">Naukri Intelligence Platform</div>
  </div>
  <div class="sidebar-nav">
    <div class="nav-section-label">Main</div>
    ${nav("dashboard","⚡","Dashboard")}
    ${nav("candidates","👥","Candidates", state.stats.total || "")}
    ${nav("jobs","💼","Jobs", state.jobs.length || "")}
    ${nav("pipeline","🔄","Pipeline")}
    <div class="nav-section-label">Config</div>
    ${nav("setup","🔌","Extension Setup")}
    ${nav("settings","⚙️","Settings")}
  </div>
  <div class="sidebar-footer">
    <div class="token-display">
      <div class="token-label">Connected as</div>
      <div class="token-val">${state.token ? state.token.slice(0,28)+"…" : "—"}</div>
      <div class="token-status">
        <div class="status-dot ${state.token ? '' : 'off'}"></div>
        <span style="font-size:11px;color:var(--text3)">${state.token ? "Connected" : "Disconnected"}</span>
      </div>
    </div>
  </div>`;
}

function renderTopbar() {
  const titles = { dashboard:"Dashboard", candidates:"Candidates", jobs:"Jobs", pipeline:"Pipeline", setup:"Extension Setup", settings:"Settings" };
  return `
  <div class="topbar-title">${titles[state.page] || ""}</div>
  <div class="topbar-actions">
    ${state.page === "candidates" ? `<button class="btn btn-secondary btn-sm" id="refreshBtn">↻ Refresh</button>` : ""}
    ${state.page === "jobs" ? `<button class="btn btn-primary btn-sm" id="newJobBtn">+ New Job</button>` : ""}
    <button class="btn btn-ghost btn-sm" id="logoutBtn">Sign out</button>
  </div>`;
}

function renderPage() {
  switch(state.page) {
    case "dashboard": return renderDashboard();
    case "candidates": return renderCandidates();
    case "jobs": return renderJobs();
    case "pipeline": return renderPipeline();
    case "setup": return renderSetup();
    case "settings": return renderSettings();
    default: return renderDashboard();
  }
}

// ── DASHBOARD ──────────────────────────────────────────────────────────────────
function renderDashboard() {
  const recent = [...state.candidates].sort((a,b) => new Date(b._creationTime||b.createdAt||0) - new Date(a._creationTime||a.createdAt||0)).slice(0, 8);
  return `
  <div class="stats-grid">
    ${statCard("👥", state.stats.total, "Total Candidates", "All time", "")}
    ${statCard("📅", state.stats.today, "Added Today", "Last 24 hours", "green")}
    ${statCard("📊", state.stats.thisWeek, "This Week", "Last 7 days", "blue")}
    ${statCard("💼", state.stats.jobs, "Active Jobs", "Open positions", "purple")}
  </div>
  <div style="display:grid;grid-template-columns:1fr 360px;gap:16px">
    <div class="card">
      <div class="card-header">
        <div class="card-title">Recent Candidates</div>
        <button class="btn btn-ghost btn-sm" data-nav="candidates">View all →</button>
      </div>
      ${recent.length === 0 ? `<div class="empty"><div class="empty-icon">👥</div><div class="empty-title">No candidates yet</div><div class="empty-sub">Import candidates using the Chrome extension</div></div>` : `
      <div class="table-wrap">
        <table>
          <thead><tr><th>Name</th><th>Role</th><th>Location</th><th>Added</th></tr></thead>
          <tbody>
            ${recent.map(c => `
            <tr class="cand-row" data-id="${c._id}">
              <td><div class="cand-name">${fmt(c.name)}</div><div class="cand-email">${fmt(c.email)}</div></td>
              <td><div class="cand-title">${fmt(c.currentTitle)}</div><div style="font-size:11px;color:var(--text3)">${fmt(c.currentCompany)}</div></td>
              <td><span class="chip chip-gray">${fmt(c.location)}</span></td>
              <td><span style="font-size:12px;color:var(--text3)">${timeAgo(c._creationTime || c.createdAt)}</span></td>
            </tr>`).join("")}
          </tbody>
        </table>
      </div>`}
    </div>
    <div class="card">
      <div class="card-header"><div class="card-title">Jobs Overview</div></div>
      ${state.jobs.length === 0 ? `<div class="empty" style="padding:30px"><div class="empty-icon">💼</div><div class="empty-title">No jobs</div></div>` :
        state.jobs.map(j => `
        <div class="activity-item">
          <div class="activity-dot" style="background:var(--accent)"></div>
          <div class="activity-text">${j.title}<div style="font-size:11px;color:var(--text3)">${j.location || "Remote"}</div></div>
          <span class="chip chip-orange" style="font-size:10px">${j._id ? state.candidates.filter(c=>c.jobId===j._id).length : 0}</span>
        </div>`).join("")
      }
    </div>
  </div>`;
}

function statCard(icon, val, label, sub, color) {
  return `<div class="stat-card ${color}">
    <div class="stat-icon">${icon}</div>
    <div class="stat-value">${val ?? 0}</div>
    <div class="stat-label">${label}</div>
    <div class="stat-sub">${sub}</div>
  </div>`;
}

// ── CANDIDATES ─────────────────────────────────────────────────────────────────
function renderCandidates() {
  const { list, total } = pagedCandidates();
  const totalPages = Math.max(1, Math.ceil(total / PAGE_SIZE));
  const jobOptions = state.jobs.map(j => `<option value="${j._id}">${j.title}</option>`).join("");
  return `
  <div class="card">
    <div class="filter-bar">
      <div class="search-wrap">
        <span class="search-icon">🔍</span>
        <input class="form-input" id="searchInput" placeholder="Search candidates, skills, company…" value="${state.searchQuery}" style="padding-left:34px" />
      </div>
      <select class="filter-select" id="jobFilter">
        <option value="">All Jobs</option>
        ${jobOptions}
      </select>
      <span style="font-size:12px;color:var(--text3);white-space:nowrap">${total} result${total !== 1 ? 's' : ''}</span>
    </div>
    ${state.loading ? renderSkeletonRows() : `
    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>Candidate</th>
            <th>Role & Company</th>
            <th>Contact</th>
            <th>Experience</th>
            <th>Location</th>
            <th>Skills</th>
            <th>Added</th>
          </tr>
        </thead>
        <tbody>
          ${list.length === 0 ? `<tr><td colspan="7"><div class="empty"><div class="empty-icon">🔍</div><div class="empty-title">${state.searchQuery ? "No matches" : "No candidates yet"}</div><div class="empty-sub">${state.searchQuery ? "Try a different search" : "Use the Chrome extension to import from Naukri"}</div></div></td></tr>` :
            list.map(c => renderCandidateRow(c)).join("")}
        </tbody>
      </table>
    </div>
    <div class="pagination">
      <div class="page-info">Showing ${Math.min((state.candidatePage-1)*PAGE_SIZE+1, total)}–${Math.min(state.candidatePage*PAGE_SIZE, total)} of ${total}</div>
      <div class="page-btns">
        <button class="page-btn" id="prevPage" ${state.candidatePage <= 1 ? 'disabled' : ''}>‹</button>
        ${Array.from({length: Math.min(totalPages, 7)}, (_,i) => {
          const p = i + 1;
          return `<button class="page-btn ${p === state.candidatePage ? 'active' : ''}" data-page="${p}">${p}</button>`;
        }).join("")}
        <button class="page-btn" id="nextPage" ${state.candidatePage >= totalPages ? 'disabled' : ''}>›</button>
      </div>
    </div>`}
  </div>`;
}

function renderCandidateRow(c) {
  const raw = parseRaw(c);
  const skills = (c.skills || raw.keySkills || []).slice(0, 3);
  const exp = c.experienceYears != null ? `${c.experienceYears}y` : (raw.totalExperience ? `${raw.totalExperience}y` : "—");
  return `
  <tr class="cand-row" data-id="${c._id}">
    <td>
      <div style="display:flex;align-items:center;gap:10px">
        <div style="width:32px;height:32px;border-radius:8px;background:var(--accentdim);border:1px solid var(--accent);display:flex;align-items:center;justify-content:center;font-family:'Syne',sans-serif;font-weight:800;font-size:12px;color:var(--accent);flex-shrink:0">${initials(c.name)}</div>
        <div><div class="cand-name">${fmt(c.name)}</div><div style="font-size:11px;color:var(--text3)">${timeAgo(c._creationTime || c.createdAt)}</div></div>
      </div>
    </td>
    <td>
      <div style="font-size:13px;color:var(--text);font-weight:500">${fmt(c.currentTitle)}</div>
      <div style="font-size:11px;color:var(--text2)">${fmt(c.currentCompany)}</div>
    </td>
    <td>
      <div class="cand-email" style="font-size:11px">${fmt(c.email)}</div>
      <div class="cand-phone" style="font-size:11px">${fmt(c.phone)}</div>
    </td>
    <td><span class="chip chip-blue">${exp}</span></td>
    <td><span style="font-size:12px;color:var(--text2)">${fmt(c.location)}</span></td>
    <td>
      <div style="display:flex;gap:4px;flex-wrap:wrap">
        ${skills.map(s => `<span class="chip chip-gray" style="font-size:10px">${s}</span>`).join("")}
        ${(c.skills||[]).length > 3 ? `<span class="chip chip-gray" style="font-size:10px">+${(c.skills||[]).length-3}</span>` : ""}
      </div>
    </td>
    <td>
      ${c.jobId ? `<span class="chip chip-orange" style="font-size:10px">${(state.jobs.find(j=>j._id===c.jobId)||{}).title||"Job"}</span>` : ""}
    </td>
  </tr>`;
}

function renderSkeletonRows() {
  return `<div class="table-wrap"><table><tbody>
    ${Array.from({length:8}).map(() => `
    <tr class="loading-row">
      <td><div class="skeleton skel-line" style="width:120px"></div></td>
      <td><div class="skeleton skel-line" style="width:100px"></div></td>
      <td><div class="skeleton skel-line" style="width:140px"></div></td>
      <td><div class="skeleton skel-line" style="width:40px"></div></td>
      <td><div class="skeleton skel-line" style="width:80px"></div></td>
      <td><div class="skeleton skel-line" style="width:120px"></div></td>
      <td><div class="skeleton skel-line" style="width:60px"></div></td>
    </tr>`).join("")}
  </tbody></table></div>`;
}

// ── CANDIDATE MODAL ────────────────────────────────────────────────────────────
function renderCandidateModal() {
  const c = state.selectedCandidate;
  const raw = parseRaw(c);
  const wh = raw.workHistory || c.workHistory || [];
  const edu = raw.education || c.education || [];
  const langs = raw.languages || c.languages || [];
  const skills = [...(c.skills || []), ...(raw.keySkills || [])].filter((s,i,a) => a.indexOf(s)===i);
  const salary = raw.salary || c.salary;
  const expSalary = raw.expectedSalary || c.expectedSalary;
  const notice = raw.noticePeriod || c.noticePeriod;
  const prefLoc = raw.preferredLocations || c.preferredLocations;
  const exp = c.experienceYears != null ? `${c.experienceYears} years` : "—";
  const aiSummary = raw.aiSummary || c.aiSummary;
  const summary = c.summary || raw.workSummary || c.workSummary || c.summary;
  const jobName = state.jobs.find(j => j._id === c.jobId)?.title || "—";

  return `
  <div class="modal-overlay" id="modalOverlay">
    <div class="modal">
      <div class="modal-header">
        <div class="modal-title">Candidate Profile</div>
        <div style="display:flex;gap:8px;align-items:center">
          ${c.profileUrl ? `<a href="${c.profileUrl}" target="_blank" class="btn btn-secondary btn-sm">↗ Naukri Profile</a>` : ""}
          <button class="close-btn" id="closeModal">✕</button>
        </div>
      </div>
      <div class="modal-body">
        <div class="profile-hero">
          <div class="profile-avatar">${initials(c.name)}</div>
          <div style="flex:1">
            <div class="profile-name">${fmt(c.name)}</div>
            <div class="profile-sub">${fmt(c.currentTitle)}${c.currentCompany ? ` · ${c.currentCompany}` : ""}</div>
            <div class="profile-meta">
              ${c.location ? `<span class="meta-item">📍 ${c.location}</span>` : ""}
              ${exp !== "—" ? `<span class="meta-item">💼 ${exp} exp</span>` : ""}
              ${notice ? `<span class="meta-item">⏱ ${notice}</span>` : ""}
              ${salary ? `<span class="meta-item">💰 ${salary}</span>` : ""}
            </div>
          </div>
          <div style="text-align:right">
            <span class="chip chip-orange">${jobName}</span>
            <div style="font-size:11px;color:var(--text3);margin-top:6px">${timeAgo(c._creationTime || c.createdAt)}</div>
          </div>
        </div>

        ${aiSummary ? `
        <div style="background:var(--purpledim);border:1px solid rgba(168,85,247,0.2);border-radius:10px;padding:14px 16px;margin-bottom:4px">
          <div style="font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:1px;color:var(--purple);margin-bottom:6px">✨ AI Summary</div>
          <div style="font-size:13px;color:var(--text);line-height:1.6">${aiSummary}</div>
        </div>` : ""}

        ${summary ? `
        <div class="section-label">Summary</div>
        <div style="font-size:13px;color:var(--text2);line-height:1.6;background:var(--bg3);border-radius:8px;padding:12px">${summary}</div>` : ""}

        <div class="section-label">Contact & Details</div>
        <div class="info-grid">
          <div class="info-item"><div class="info-label">Email</div><div class="info-value" style="font-family:'DM Mono',monospace;font-size:12px">${fmt(c.email)}</div></div>
          <div class="info-item"><div class="info-label">Phone</div><div class="info-value" style="font-family:'DM Mono',monospace;font-size:12px">${fmt(c.phone)}</div></div>
          <div class="info-item"><div class="info-label">Current Salary</div><div class="info-value">${fmt(salary)}</div></div>
          <div class="info-item"><div class="info-label">Expected Salary</div><div class="info-value">${fmt(expSalary)}</div></div>
          <div class="info-item"><div class="info-label">Notice Period</div><div class="info-value">${fmt(notice)}</div></div>
          <div class="info-item"><div class="info-label">Preferred Locations</div><div class="info-value">${fmt(prefLoc)}</div></div>
          ${raw.gender ? `<div class="info-item"><div class="info-label">Gender</div><div class="info-value">${raw.gender}</div></div>` : ""}
          ${raw.dateOfBirth ? `<div class="info-item"><div class="info-label">Date of Birth</div><div class="info-value">${raw.dateOfBirth}</div></div>` : ""}
          ${raw.maritalStatus ? `<div class="info-item"><div class="info-label">Marital Status</div><div class="info-value">${raw.maritalStatus}</div></div>` : ""}
          ${raw.industry ? `<div class="info-item"><div class="info-label">Industry</div><div class="info-value">${raw.industry}</div></div>` : ""}
        </div>

        ${skills.length ? `
        <div class="section-label">Skills</div>
        <div class="skills-wrap">
          ${skills.map(s => `<span class="chip chip-orange">${s}</span>`).join("")}
        </div>` : ""}

        ${wh.length ? `
        <div class="section-label">Work Experience</div>
        ${wh.map(w => `
        <div class="work-item">
          <div class="work-dot"></div>
          <div class="work-content">
            <div class="work-title">${fmt(w.title)}</div>
            <div class="work-company">${fmt(w.company)}</div>
            <div class="work-dates">${w.tenure || (w.startDate ? `${w.startDate} – ${w.endDate||"Present"}` : "")}</div>
            ${w.description ? `<div class="work-desc">${String(w.description).slice(0,300)}</div>` : ""}
          </div>
        </div>`).join("")}` : ""}

        ${edu.length ? `
        <div class="section-label">Education</div>
        ${edu.map(e => `
        <div class="work-item">
          <div class="work-dot" style="background:var(--blue)"></div>
          <div class="work-content">
            <div class="work-title">${fmt(e.degree)}${e.specialization ? ` · ${e.specialization}` : ""}</div>
            <div class="work-company">${fmt(e.college)}</div>
            <div class="work-dates">${fmt(e.year)}</div>
          </div>
        </div>`).join("")}` : ""}

        ${langs.length ? `
        <div class="section-label">Languages</div>
        <div class="skills-wrap">${langs.map(l => `<span class="chip chip-blue">${l}</span>`).join("")}</div>` : ""}
      </div>
      <div class="modal-footer">
        <button class="btn btn-danger btn-sm" id="deleteBtn">🗑 Remove</button>
        ${c.profileUrl ? `<a href="${c.profileUrl}" target="_blank" class="btn btn-secondary btn-sm">↗ Open in Naukri</a>` : ""}
        <button class="btn btn-primary btn-sm" id="closeModal2">Close</button>
      </div>
    </div>
  </div>`;
}

// ── JOBS ────────────────────────────────────────────────────────────────────────
function renderJobs() {
  return `
  ${state.jobs.length === 0 ? `
  <div class="empty" style="margin-top:80px">
    <div class="empty-icon">💼</div>
    <div class="empty-title">No jobs created yet</div>
    <div class="empty-sub">Create a job to start organizing candidates</div>
    <button class="btn btn-primary" style="margin-top:16px" id="newJobBtn2">+ Create First Job</button>
  </div>` : `
  <div class="jobs-grid">
    ${state.jobs.map(j => {
      const count = state.candidates.filter(c => c.jobId === j._id).length;
      return `
      <div class="job-card ${state.selectedJob?._id === j._id ? 'selected' : ''}" data-jobid="${j._id}">
        <div class="job-title">${j.title}</div>
        <div class="job-location">📍 ${j.location || "Not specified"}</div>
        <div class="job-stats">
          <div class="job-stat"><div class="job-stat-n">${count}</div><div class="job-stat-l">Candidates</div></div>
        </div>
        <div style="margin-top:12px">
          <button class="btn btn-secondary btn-sm" data-filterjob="${j._id}">View Candidates →</button>
        </div>
      </div>`;
    }).join("")}
  </div>`}`;
}

// ── PIPELINE ───────────────────────────────────────────────────────────────────
function renderPipeline() {
  const stages = ["Sourced","Screened","Interview","Offer","Hired","Rejected"];
  const colors = { Sourced:"var(--blue)", Screened:"var(--purple)", Interview:"var(--accent)", Offer:"var(--green)", Hired:"var(--green)", Rejected:"var(--red)" };
  return `
  <div style="overflow-x:auto;padding-bottom:8px">
    <div class="pipeline">
      ${stages.map(stage => {
        const cands = state.candidates.filter(c => (c.stage || "Sourced") === stage);
        return `
        <div class="pipeline-col">
          <div class="pipeline-col-header" style="border-top:2px solid ${colors[stage]}">
            <span class="pipeline-col-title">${stage}</span>
            <span class="pipeline-col-count">${cands.length}</span>
          </div>
          <div class="pipeline-col-body">
            ${cands.slice(0,10).map(c => `
            <div class="pipeline-card cand-row" data-id="${c._id}">
              <div class="pipeline-card-name">${fmt(c.name)}</div>
              <div class="pipeline-card-sub">${fmt(c.currentTitle)} · ${fmt(c.experienceYears,"?")}y</div>
              <div style="margin-top:6px;display:flex;gap:4px;flex-wrap:wrap">
                ${(c.skills||[]).slice(0,2).map(s=>`<span class="chip chip-gray" style="font-size:10px">${s}</span>`).join("")}
              </div>
            </div>`).join("")}
            ${cands.length === 0 ? `<div style="text-align:center;padding:20px;font-size:12px;color:var(--text3)">No candidates</div>` : ""}
          </div>
        </div>`;
      }).join("")}
    </div>
  </div>`;
}

// ── SETUP ──────────────────────────────────────────────────────────────────────
function renderSetup() {
  const token = state.token;
  return `
  <div style="background:var(--accentdim);border:1px solid rgba(249,115,22,0.3);border-radius:12px;padding:16px 20px;margin-bottom:20px;display:flex;align-items:flex-start;gap:12px">
    <div style="font-size:22px;flex-shrink:0">👋</div>
    <div>
      <div style="font-family:'Syne',sans-serif;font-weight:700;font-size:14px;color:var(--accent);margin-bottom:6px">How to use RecruiterOS in 3 steps</div>
      <div style="font-size:13px;color:var(--text);line-height:1.8">
        <strong>Step 1</strong> — Copy your token below and paste it into the Chrome extension popup (click the 🟠 extension icon in Chrome toolbar)<br>
        <strong>Step 2</strong> — In the extension popup, click <em>Verify</em>, select a job, then <em>Save Settings</em><br>
        <strong>Step 3</strong> — Go to <strong>resdex.naukri.com</strong>, search for candidates, check the boxes → click <strong>Import Selected</strong>. Candidates appear here automatically.
      </div>
    </div>
  </div>
  <div class="setup-grid">
    <div>
      <div class="setup-card" style="margin-bottom:16px">
        <div class="card-title" style="margin-bottom:20px">📦 Install Extension</div>
        <div class="setup-step">
          <div class="step-num">1</div>
          <div class="step-body">
            <div class="step-title">Download Extension Files</div>
            <div class="step-desc">Download the Naukri Recruiter App extension files from your project folder.</div>
          </div>
        </div>
        <div class="setup-step">
          <div class="step-num">2</div>
          <div class="step-body">
            <div class="step-title">Open Chrome Extensions</div>
            <div class="step-desc">Go to <strong>chrome://extensions</strong> and enable Developer Mode (top-right toggle).</div>
          </div>
        </div>
        <div class="setup-step">
          <div class="step-num">3</div>
          <div class="step-body">
            <div class="step-title">Load Unpacked</div>
            <div class="step-desc">Click <strong>Load unpacked</strong> and select your extension folder.</div>
          </div>
        </div>
        <div class="setup-step">
          <div class="step-num">4</div>
          <div class="step-body">
            <div class="step-title">Configure Auth Token</div>
            <div class="step-desc">Click the extension icon → paste your token below → click Verify → select a job → Save Settings.</div>
          </div>
        </div>
      </div>

      <div class="setup-card">
        <div class="card-title" style="margin-bottom:16px">🔍 Troubleshooting</div>
        <div style="font-size:13px;color:var(--text2);line-height:1.8">
          <div><strong style="color:var(--text)">Checkboxes not showing?</strong><br>Hard refresh the Naukri page (Ctrl+Shift+R) after reloading the extension.</div>
          <div style="margin-top:12px"><strong style="color:var(--text)">Import not working?</strong><br>Open DevTools Console and check for <code>[ra]</code> logs to see what's happening.</div>
          <div style="margin-top:12px"><strong style="color:var(--text)">Candidates not appearing here?</strong><br>The dashboard syncs automatically. Try refreshing this page.</div>
        </div>
      </div>
    </div>

    <div>
      <div class="setup-card" style="margin-bottom:16px">
        <div class="card-title" style="margin-bottom:16px">🔑 Your Auth Token</div>
        <div class="code-block">
          ${token || "No token set"}
          <button class="copy-btn" onclick="copyToClipboard('${token}')">Copy</button>
        </div>
        <div style="font-size:12px;color:var(--text3);margin-top:10px">Paste this into the extension popup → Auth Token field</div>
      </div>

      <div class="setup-card" style="margin-bottom:16px">
        <div class="card-title" style="margin-bottom:16px">⚡ Connection Test</div>
        <div style="font-size:13px;color:var(--text2);margin-bottom:12px">Test that your token is valid and the backend is reachable.</div>
        <button class="btn btn-primary" id="testConn" style="width:100%">Run Connection Test</button>
        <div id="testResult" style="margin-top:12px;font-size:13px"></div>
      </div>

      <div class="setup-card">
        <div class="card-title" style="margin-bottom:16px">📡 API Endpoints</div>
        <div style="font-size:12px;color:var(--text3);margin-bottom:8px">Backend URL</div>
        <div class="code-block">${API_BASE}<button class="copy-btn" onclick="copyToClipboard('${API_BASE}')">Copy</button></div>
        <div style="font-size:12px;color:var(--text3);margin-top:12px;margin-bottom:8px">Candidates endpoint</div>
        <div class="code-block">${API_BASE}/ext/candidates</div>
        <div style="font-size:12px;color:var(--text3);margin-top:12px;margin-bottom:8px">Jobs endpoint</div>
        <div class="code-block">${API_BASE}/ext/jobs</div>
      </div>
    </div>
  </div>`;
}

// ── SETTINGS ───────────────────────────────────────────────────────────────────
function renderSettings() {
  return `
  <div style="max-width:500px">
    <div class="setup-card" style="margin-bottom:16px">
      <div class="card-title" style="margin-bottom:16px">⚙️ Settings</div>
      <div class="form-group">
        <label class="form-label">Auth Token</label>
        <input class="form-input" id="settingsToken" type="password" value="${state.token}" placeholder="ra_live_..." />
      </div>
      <button class="btn btn-primary" id="saveSettings">Save Token</button>
    </div>
    <div class="setup-card">
      <div class="card-title" style="margin-bottom:16px">🗑 Danger Zone</div>
      <div style="font-size:13px;color:var(--text2);margin-bottom:12px">Sign out of the dashboard. Your data in the backend will remain.</div>
      <button class="btn btn-danger" id="logoutBtn2">Sign Out</button>
    </div>
  </div>`;
}

// ── NEW JOB MODAL ──────────────────────────────────────────────────────────────
function renderNewJobModal() {
  return `
  <div class="modal-overlay" id="newJobOverlay">
    <div class="modal" style="width:480px">
      <div class="modal-header">
        <div class="modal-title">Create New Job</div>
        <button class="close-btn" id="closeNewJob">✕</button>
      </div>
      <div class="modal-body">
        <div class="form-group">
          <label class="form-label">Job Title *</label>
          <input class="form-input" id="jobTitle" placeholder="e.g. Inside Sales Executive" />
        </div>
        <div class="form-grid">
          <div class="form-group">
            <label class="form-label">Location</label>
            <input class="form-input" id="jobLocation" placeholder="Mumbai, Remote…" />
          </div>
          <div class="form-group">
            <label class="form-label">Department</label>
            <input class="form-input" id="jobDept" placeholder="Sales, Tech…" />
          </div>
        </div>
        <div class="form-group">
          <label class="form-label">Description</label>
          <textarea class="form-textarea" id="jobDesc" placeholder="Job description…"></textarea>
        </div>
      </div>
      <div class="modal-footer">
        <button class="btn btn-secondary" id="closeNewJob2">Cancel</button>
        <button class="btn btn-primary" id="submitNewJob">Create Job →</button>
      </div>
    </div>
  </div>`;
}

// ── SETTINGS MODAL ─────────────────────────────────────────────────────────────
function renderSettingsModal() {
  return ``;
}

// ── TOASTS ─────────────────────────────────────────────────────────────────────
function renderToasts() {
  if (state.toasts.length === 0) return `<div class="toast-container" id="toastContainer"></div>`;
  const icons = { success:"✅", error:"❌", info:"ℹ️" };
  return `<div class="toast-container">
    ${state.toasts.map(t => `
    <div class="toast ${t.type}">
      <span class="toast-icon">${icons[t.type]||"ℹ️"}</span>
      <span>${t.msg}</span>
    </div>`).join("")}
  </div>`;
}

// ── BIND EVENTS ────────────────────────────────────────────────────────────────
function bindShell() {
  // Nav
  document.querySelectorAll("[data-nav]").forEach(el => {
    el.onclick = () => { state.page = el.dataset.nav; render(); };
  });

  // Topbar
  const refreshBtn = document.getElementById("refreshBtn");
  if (refreshBtn) refreshBtn.onclick = () => loadCandidates();

  const newJobBtn = document.getElementById("newJobBtn") || document.getElementById("newJobBtn2");
  if (newJobBtn) newJobBtn.onclick = () => { state.showNewJob = true; render(); };

  const logoutBtn = document.getElementById("logoutBtn") || document.getElementById("logoutBtn2");
  if (logoutBtn) logoutBtn.onclick = () => {
    localStorage.removeItem("ra_token");
    state.token = "";
    state.candidates = [];
    state.jobs = [];
    render();
  };

  // Candidate rows
  document.querySelectorAll(".cand-row[data-id]").forEach(row => {
    row.onclick = () => {
      state.selectedCandidate = state.candidates.find(c => c._id === row.dataset.id) || null;
      render();
    };
  });

  // Candidate modal
  const closeModal = document.getElementById("closeModal") || document.getElementById("closeModal2");
  if (closeModal) closeModal.onclick = () => { state.selectedCandidate = null; render(); };
  const overlay = document.getElementById("modalOverlay");
  if (overlay) overlay.onclick = e => { if (e.target === overlay) { state.selectedCandidate = null; render(); } };
  const deleteBtn = document.getElementById("deleteBtn");
  if (deleteBtn) deleteBtn.onclick = () => {
    if (confirm(`Remove ${state.selectedCandidate?.name}?`)) deleteCandidate(state.selectedCandidate._id);
  };

  // Search
  const searchInput = document.getElementById("searchInput");
  if (searchInput) {
    searchInput.oninput = e => { state.searchQuery = e.target.value; state.candidatePage = 1; render(); };
    searchInput.focus();
  }

  // Job filter
  const jobFilter = document.getElementById("jobFilter");
  if (jobFilter) {
    jobFilter.value = state.jobFilter;
    jobFilter.onchange = e => { state.jobFilter = e.target.value; state.candidatePage = 1; render(); };
  }

  // Pagination
  const prevPage = document.getElementById("prevPage");
  if (prevPage) prevPage.onclick = () => { state.candidatePage--; render(); };
  const nextPage = document.getElementById("nextPage");
  if (nextPage) nextPage.onclick = () => { state.candidatePage++; render(); };
  document.querySelectorAll("[data-page]").forEach(btn => {
    btn.onclick = () => { state.candidatePage = parseInt(btn.dataset.page); render(); };
  });

  // Jobs
  document.querySelectorAll("[data-filterjob]").forEach(btn => {
    btn.onclick = e => { e.stopPropagation(); state.jobFilter = btn.dataset.filterjob; state.page = "candidates"; render(); };
  });

  // New job modal
  const closeNewJob = document.getElementById("closeNewJob") || document.getElementById("closeNewJob2");
  if (closeNewJob) closeNewJob.onclick = () => { state.showNewJob = false; render(); };
  const submitNewJob = document.getElementById("submitNewJob");
  if (submitNewJob) submitNewJob.onclick = async () => {
    const title = document.getElementById("jobTitle").value.trim();
    if (!title) { showToast("Job title is required", "error"); return; }
    submitNewJob.disabled = true;
    submitNewJob.textContent = "Creating…";
    try {
      await createJob({
        title,
        location: document.getElementById("jobLocation").value.trim(),
        department: document.getElementById("jobDept").value.trim(),
        description: document.getElementById("jobDesc").value.trim(),
      });
      state.showNewJob = false;
      render();
    } catch(e) {
      showToast("Failed: " + e.message, "error");
      submitNewJob.disabled = false;
      submitNewJob.textContent = "Create Job →";
    }
  };
  const newJobOverlay = document.getElementById("newJobOverlay");
  if (newJobOverlay) newJobOverlay.onclick = e => { if (e.target === newJobOverlay) { state.showNewJob = false; render(); } };

  // Settings
  const saveSettings = document.getElementById("saveSettings");
  if (saveSettings) saveSettings.onclick = () => {
    const t = document.getElementById("settingsToken").value.trim();
    if (!t) return;
    state.token = cleanToken(t);
    localStorage.setItem("ra_token", state.token);
    showToast("Token saved!", "success");
  };

  // Connection test
  const testConn = document.getElementById("testConn");
  if (testConn) testConn.onclick = async () => {
    const result = document.getElementById("testResult");
    testConn.disabled = true;
    testConn.textContent = "Testing…";
    try {
      const data = await api("/ext/jobs");
      result.innerHTML = `<span style="color:var(--green)">✅ Connected! Found ${(data.jobs||[]).length} jobs.</span>`;
    } catch(e) {
      result.innerHTML = `<span style="color:var(--red)">❌ Failed: ${e.message}</span>`;
    }
    testConn.disabled = false;
    testConn.textContent = "Run Connection Test";
  };
}

// ── INIT ────────────────────────────────────────────────────────────────────────
async function init() {
  render();
  if (state.token) {
    await loadJobs();
    await loadCandidates();
    render();
  }
}

init();
</script>
</body>
</html>
