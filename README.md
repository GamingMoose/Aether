# Aether
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Aether — AI Fitness Trainer</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=Space+Grotesk:wght@500;600;700&display=swap" rel="stylesheet" />
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" />
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>
  <style>
/* ===== Aether Design System ===== */
:root {
  --bg: #0b0d12;
  --bg-elevated: #12151d;
  --surface: rgba(255, 255, 255, 0.04);
  --surface-hover: rgba(255, 255, 255, 0.07);
  --border: rgba(255, 255, 255, 0.08);
  --text: #f4f5f7;
  --text-muted: #9aa3b2;
  --text-dim: #6b7385;
  --primary: #7c5cff;
  --primary-soft: rgba(124, 92, 255, 0.15);
  --teal: #2dd4bf;
  --coral: #ff6b6b;
  --gold: #fbbf24;
  --purple: #a78bfa;
  --success: #34d399;
  --danger: #f87171;
  --radius: 16px;
  --radius-sm: 10px;
  --shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
  --font: 'Inter', system-ui, sans-serif;
  --font-display: 'Space Grotesk', var(--font);
  --sidebar-w: 260px;
  --transition: 0.2s cubic-bezier(0.4, 0, 0.2, 1);
}

[data-theme="light"] {
  --bg: #f5f6fa;
  --bg-elevated: #ffffff;
  --surface: rgba(0, 0, 0, 0.03);
  --surface-hover: rgba(0, 0, 0, 0.06);
  --border: rgba(0, 0, 0, 0.08);
  --text: #0f1219;
  --text-muted: #5a6478;
  --text-dim: #8b95a8;
  --shadow: 0 8px 32px rgba(0, 0, 0, 0.08);
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

html { font-size: 15px; }

body {
  font-family: var(--font);
  background: var(--bg);
  color: var(--text);
  min-height: 100vh;
  line-height: 1.5;
  -webkit-font-smoothing: antialiased;
}

/* Background ambient */
body::before {
  content: '';
  position: fixed;
  inset: 0;
  background:
    radial-gradient(ellipse 80% 50% at 20% -10%, rgba(124, 92, 255, 0.18), transparent),
    radial-gradient(ellipse 60% 40% at 90% 10%, rgba(45, 212, 191, 0.1), transparent),
    radial-gradient(ellipse 50% 30% at 50% 100%, rgba(255, 107, 107, 0.06), transparent);
  pointer-events: none;
  z-index: 0;
}

button, input, select, textarea {
  font: inherit;
  color: inherit;
  border: none;
  outline: none;
  background: transparent;
}

button { cursor: pointer; }

a { color: inherit; text-decoration: none; }

ul { list-style: none; }

/* ===== Utilities ===== */
.hidden { display: none !important; }
.muted { color: var(--text-muted); }
.small { font-size: 0.85rem; }
.full { width: 100%; }

.glass {
  background: var(--surface);
  border: 1px solid var(--border);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-radius: var(--radius);
}

/* ===== Buttons ===== */
.btn-primary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 0.7rem 1.25rem;
  background: linear-gradient(135deg, #7c5cff, #5b3fd9);
  color: #fff;
  border-radius: 12px;
  font-weight: 600;
  font-size: 0.9rem;
  transition: var(--transition);
  box-shadow: 0 4px 16px rgba(124, 92, 255, 0.35);
}
.btn-primary:hover { transform: translateY(-1px); box-shadow: 0 6px 24px rgba(124, 92, 255, 0.45); }
.btn-primary:active { transform: translateY(0); }

.btn-ghost {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.6rem 1rem;
  border-radius: 10px;
  color: var(--text-muted);
  font-weight: 500;
  transition: var(--transition);
}
.btn-ghost:hover { background: var(--surface-hover); color: var(--text); }
.btn-ghost.small { font-size: 0.8rem; padding: 0.4rem 0.8rem; }

.btn-danger {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.6rem 1rem;
  border-radius: 10px;
  color: var(--danger);
  font-weight: 500;
  border: 1px solid rgba(248, 113, 113, 0.3);
  transition: var(--transition);
}
.btn-danger:hover { background: rgba(248, 113, 113, 0.1); }

.btn-icon {
  width: 40px;
  height: 40px;
  display: grid;
  place-items: center;
  border-radius: 12px;
  background: var(--surface);
  border: 1px solid var(--border);
  color: var(--text-muted);
  transition: var(--transition);
}
.btn-icon:hover { color: var(--text); background: var(--surface-hover); }
.btn-icon.primary {
  background: linear-gradient(135deg, #7c5cff, #5b3fd9);
  color: #fff;
  border: none;
}

/* ===== Onboarding ===== */
.onboarding {
  position: fixed;
  inset: 0;
  z-index: 100;
  display: grid;
  place-items: center;
  background: var(--bg);
  padding: 1.5rem;
}
.onboarding-card {
  width: 100%;
  max-width: 420px;
  background: var(--bg-elevated);
  border: 1px solid var(--border);
  border-radius: 24px;
  padding: 2.5rem 2rem;
  box-shadow: var(--shadow);
}
.onboarding-header { text-align: center; margin-bottom: 2rem; }
.onboarding-header .logo-mark {
  width: 56px;
  height: 56px;
  margin: 0 auto 1rem;
  background: linear-gradient(135deg, #7c5cff, #2dd4bf);
  border-radius: 16px;
  display: grid;
  place-items: center;
  font-family: var(--font-display);
  font-weight: 700;
  font-size: 1.5rem;
  color: #fff;
}
.onboarding-header h1 {
  font-family: var(--font-display);
  font-size: 1.75rem;
  font-weight: 700;
  margin-bottom: 0.4rem;
}
.onboarding-header p { color: var(--text-muted); font-size: 0.95rem; }

.step { display: none; }
.step.active { display: block; animation: fadeUp 0.35s ease; }
.step label {
  display: block;
  font-weight: 500;
  margin-bottom: 0.6rem;
  color: var(--text-muted);
  font-size: 0.9rem;
}
.step input {
  width: 100%;
  padding: 0.9rem 1rem;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 12px;
  font-size: 1rem;
  transition: var(--transition);
}
.step input:focus { border-color: var(--primary); box-shadow: 0 0 0 3px var(--primary-soft); }

.goal-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0.6rem;
}
.goal-btn {
  padding: 1rem 0.75rem;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 12px;
  font-weight: 500;
  transition: var(--transition);
  text-align: center;
}
.goal-btn:hover { background: var(--surface-hover); }
.goal-btn.selected {
  border-color: var(--primary);
  background: var(--primary-soft);
  color: #c4b5fd;
}

.onboarding-nav {
  display: flex;
  justify-content: space-between;
  margin-top: 2rem;
  gap: 1rem;
}
.onboarding-nav .btn-primary { flex: 1; }

/* ===== App Layout ===== */
.app {
  display: flex;
  min-height: 100vh;
  position: relative;
  z-index: 1;
}

.sidebar {
  width: var(--sidebar-w);
  flex-shrink: 0;
  background: var(--bg-elevated);
  border-right: 1px solid var(--border);
  display: flex;
  flex-direction: column;
  padding: 1.5rem 1rem;
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  z-index: 20;
}

.brand {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.5rem 0.75rem;
  margin-bottom: 2rem;
}
.brand .logo-mark {
  width: 36px;
  height: 36px;
  background: linear-gradient(135deg, #7c5cff, #2dd4bf);
  border-radius: 10px;
  display: grid;
  place-items: center;
  font-family: var(--font-display);
  font-weight: 700;
  color: #fff;
  font-size: 1rem;
}
.brand span {
  font-family: var(--font-display);
  font-weight: 700;
  font-size: 1.25rem;
  letter-spacing: -0.02em;
}

.nav-links { flex: 1; display: flex; flex-direction: column; gap: 0.25rem; }
.nav-links a {
  display: flex;
  align-items: center;
  gap: 0.85rem;
  padding: 0.75rem 1rem;
  border-radius: 12px;
  color: var(--text-muted);
  font-weight: 500;
  transition: var(--transition);
}
.nav-links a i { width: 20px; text-align: center; font-size: 1.05rem; }
.nav-links a:hover { background: var(--surface-hover); color: var(--text); }
.nav-links a.active {
  background: var(--primary-soft);
  color: #c4b5fd;
}

.sidebar-footer { margin-top: auto; padding-top: 1rem; }
.user-chip {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem;
  border-radius: 12px;
  background: var(--surface);
}
.avatar {
  width: 40px;
  height: 40px;
  border-radius: 12px;
  background: linear-gradient(135deg, #7c5cff, #a78bfa);
  display: grid;
  place-items: center;
  font-weight: 700;
  color: #fff;
  font-size: 0.95rem;
}
.user-chip strong { display: block; font-size: 0.9rem; }
.user-chip small { color: var(--text-dim); font-size: 0.75rem; text-transform: capitalize; }

.mobile-nav {
  display: none;
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background: var(--bg-elevated);
  border-top: 1px solid var(--border);
  padding: 0.6rem 0.5rem calc(0.6rem + env(safe-area-inset-bottom));
  z-index: 30;
  justify-content: space-around;
}
.mobile-nav a {
  width: 48px;
  height: 48px;
  display: grid;
  place-items: center;
  border-radius: 14px;
  color: var(--text-dim);
  font-size: 1.2rem;
  transition: var(--transition);
}
.mobile-nav a.active { color: var(--primary); background: var(--primary-soft); }

.main {
  flex: 1;
  margin-left: var(--sidebar-w);
  padding: 2rem 2.5rem 4rem;
  max-width: 1100px;
}

.view { display: none; animation: fadeUp 0.3s ease; }
.view.active { display: block; }

.view-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  margin-bottom: 2rem;
  gap: 1rem;
}
.eyebrow {
  font-size: 0.8rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--text-dim);
  margin-bottom: 0.25rem;
}
.view-header h1 {
  font-family: var(--font-display);
  font-size: 1.85rem;
  font-weight: 700;
  letter-spacing: -0.03em;
}

/* ===== Cards & Stats ===== */
.stats-row {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
  margin-bottom: 1.5rem;
}
.stat-card {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1.15rem 1.25rem;
}
.stat-icon {
  width: 44px;
  height: 44px;
  border-radius: 12px;
  display: grid;
  place-items: center;
  font-size: 1.1rem;
  flex-shrink: 0;
}
.stat-icon.purple { background: rgba(167, 139, 250, 0.15); color: var(--purple); }
.stat-icon.teal { background: rgba(45, 212, 191, 0.15); color: var(--teal); }
.stat-icon.coral { background: rgba(255, 107, 107, 0.15); color: var(--coral); }
.stat-icon.gold { background: rgba(251, 191, 36, 0.15); color: var(--gold); }
.stat-label { display: block; font-size: 0.75rem; color: var(--text-dim); font-weight: 500; }
.stat-value { font-size: 1.25rem; font-weight: 700; letter-spacing: -0.02em; }

.card {
  padding: 1.5rem;
  margin-bottom: 1.25rem;
}
.card-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 1rem;
}
.card-header h2, .card h3 {
  font-family: var(--font-display);
  font-size: 1.1rem;
  font-weight: 600;
}
.badge {
  font-size: 0.7rem;
  font-weight: 600;
  padding: 0.3rem 0.65rem;
  border-radius: 999px;
  background: var(--surface-hover);
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.04em;
}
.badge.active { background: rgba(52, 211, 153, 0.15); color: var(--success); }
.badge.rest { background: rgba(251, 191, 36, 0.15); color: var(--gold); }

.dash-grid {
  display: grid;
  grid-template-columns: 1.4fr 1fr;
  gap: 1.25rem;
  margin-bottom: 1.25rem;
}

.today-card .exercise-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.75rem 0;
  border-bottom: 1px solid var(--border);
}
.today-card .exercise-item:last-child { border-bottom: none; }
.today-card .ex-name { font-weight: 500; }
.today-card .ex-meta { font-size: 0.85rem; color: var(--text-muted); }

.tip-card p { color: var(--text-muted); line-height: 1.6; margin-bottom: 1rem; }

.activity-list li, .history-list li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.85rem 0;
  border-bottom: 1px solid var(--border);
  gap: 1rem;
}
.activity-list li:last-child, .history-list li:last-child { border-bottom: none; }
.act-title { font-weight: 500; }
.act-meta { font-size: 0.8rem; color: var(--text-dim); }

/* ===== Workouts ===== */
.tabs {
  display: flex;
  gap: 0.35rem;
  margin-bottom: 1.5rem;
  background: var(--surface);
  padding: 0.35rem;
  border-radius: 12px;
  border: 1px solid var(--border);
  width: fit-content;
}
.tab {
  padding: 0.55rem 1.1rem;
  border-radius: 9px;
  font-weight: 500;
  font-size: 0.9rem;
  color: var(--text-muted);
  transition: var(--transition);
}
.tab:hover { color: var(--text); }
.tab.active { background: var(--bg-elevated); color: var(--text); box-shadow: 0 2px 8px rgba(0,0,0,0.15); }

.tab-panel { display: none; }
.tab-panel.active { display: block; animation: fadeUp 0.25s ease; }

.filter-row {
  display: flex;
  gap: 0.75rem;
  margin-bottom: 1.25rem;
}
.filter-row input, .filter-row select {
  padding: 0.7rem 1rem;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 10px;
  flex: 1;
}
.filter-row select { max-width: 180px; }

.exercise-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
  gap: 1rem;
}
.ex-card {
  padding: 1.25rem;
  border-radius: var(--radius);
  background: var(--surface);
  border: 1px solid var(--border);
  transition: var(--transition);
  cursor: pointer;
}
.ex-card:hover { background: var(--surface-hover); border-color: rgba(124, 92, 255, 0.3); transform: translateY(-2px); }
.ex-card h4 { font-weight: 600; margin-bottom: 0.35rem; }
.ex-card .ex-tags { display: flex; flex-wrap: wrap; gap: 0.35rem; margin-top: 0.75rem; }
.ex-tag {
  font-size: 0.7rem;
  padding: 0.2rem 0.5rem;
  border-radius: 6px;
  background: var(--primary-soft);
  color: #c4b5fd;
  font-weight: 500;
  text-transform: capitalize;
}

.plans-list { display: flex; flex-direction: column; gap: 1rem; }
.plan-card {
  padding: 1.25rem 1.5rem;
  border-radius: var(--radius);
  background: var(--surface);
  border: 1px solid var(--border);
}
.plan-card h4 { font-weight: 600; margin-bottom: 0.5rem; }
.plan-card .plan-days { display: flex; flex-wrap: wrap; gap: 0.5rem; margin-top: 0.75rem; }
.plan-day {
  font-size: 0.8rem;
  padding: 0.35rem 0.7rem;
  border-radius: 8px;
  background: var(--bg-elevated);
  border: 1px solid var(--border);
}

/* Forms */
form label {
  display: block;
  font-size: 0.85rem;
  font-weight: 500;
  color: var(--text-muted);
  margin: 0.9rem 0 0.4rem;
}
form label:first-child { margin-top: 0; }
form input, form select, form textarea {
  width: 100%;
  padding: 0.75rem 1rem;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 10px;
  transition: var(--transition);
}
form input:focus, form select:focus, form textarea:focus {
  border-color: var(--primary);
  box-shadow: 0 0 0 3px var(--primary-soft);
}
form textarea { resize: vertical; min-height: 100px; }

/* ===== Progress ===== */
.chart-wrap {
  position: relative;
  height: 260px;
  margin-top: 0.5rem;
}

/* ===== Coach ===== */
.coach-layout {
  display: grid;
  grid-template-columns: 1fr 300px;
  gap: 1.25rem;
  height: calc(100vh - 180px);
  min-height: 480px;
}
.chat-panel {
  display: flex;
  flex-direction: column;
  overflow: hidden;
  padding: 0;
}
.chat-messages {
  flex: 1;
  overflow-y: auto;
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
.msg {
  display: flex;
  gap: 0.75rem;
  max-width: 90%;
  animation: fadeUp 0.3s ease;
}
.msg.user { align-self: flex-end; flex-direction: row-reverse; }
.msg-avatar {
  width: 32px;
  height: 32px;
  border-radius: 10px;
  background: linear-gradient(135deg, #7c5cff, #2dd4bf);
  display: grid;
  place-items: center;
  font-weight: 700;
  font-size: 0.8rem;
  color: #fff;
  flex-shrink: 0;
}
.msg.user .msg-avatar { background: linear-gradient(135deg, #64748b, #475569); }
.msg-bubble {
  padding: 0.85rem 1.1rem;
  border-radius: 14px;
  background: var(--surface);
  border: 1px solid var(--border);
  line-height: 1.55;
  font-size: 0.95rem;
}
.msg.user .msg-bubble {
  background: var(--primary-soft);
  border-color: rgba(124, 92, 255, 0.25);
}
.msg-bubble p { margin-bottom: 0.5rem; }
.msg-bubble p:last-child { margin-bottom: 0; }
.msg-bubble ul { margin: 0.4rem 0; padding-left: 1.2rem; }
.msg-bubble li { list-style: disc; margin: 0.2rem 0; }

.chat-input {
  display: flex;
  gap: 0.6rem;
  padding: 1rem 1.25rem;
  border-top: 1px solid var(--border);
}
.chat-input input {
  flex: 1;
  padding: 0.75rem 1rem;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 12px;
}
.chat-input input:focus { border-color: var(--primary); }

.coach-sidebar { display: flex; flex-direction: column; gap: 1rem; }
.quick-btn {
  display: block;
  width: 100%;
  text-align: left;
  padding: 0.7rem 0.9rem;
  margin-bottom: 0.4rem;
  border-radius: 10px;
  background: var(--surface);
  border: 1px solid var(--border);
  font-size: 0.85rem;
  color: var(--text-muted);
  transition: var(--transition);
}
.quick-btn:hover { background: var(--surface-hover); color: var(--text); border-color: rgba(124, 92, 255, 0.3); }
.context-list li {
  font-size: 0.85rem;
  color: var(--text-muted);
  padding: 0.35rem 0;
}
.context-list strong { color: var(--text); }

/* ===== Profile ===== */
.profile-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.25rem;
}
.calc-row {
  display: flex;
  justify-content: space-between;
  padding: 0.75rem 0;
  border-bottom: 1px solid var(--border);
  font-size: 0.95rem;
}
.calc-row:last-of-type { border-bottom: none; }
.danger-zone { grid-column: 1 / -1; display: flex; gap: 1rem; align-items: center; flex-wrap: wrap; }
.danger-zone h3 { margin-right: auto; }

/* ===== Modal ===== */
.modal {
  position: fixed;
  inset: 0;
  z-index: 50;
  display: grid;
  place-items: center;
  background: rgba(0, 0, 0, 0.6);
  backdrop-filter: blur(6px);
  padding: 1.5rem;
}
.modal-card {
  width: 100%;
  max-width: 480px;
  max-height: 85vh;
  overflow-y: auto;
  padding: 2rem;
  position: relative;
}
.modal-close {
  position: absolute;
  top: 1rem;
  right: 1rem;
  width: 36px;
  height: 36px;
  display: grid;
  place-items: center;
  border-radius: 10px;
  color: var(--text-muted);
  transition: var(--transition);
}
.modal-close:hover { background: var(--surface-hover); color: var(--text); }

/* ===== Toast ===== */
.toast {
  position: fixed;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  z-index: 60;
  padding: 0.85rem 1.5rem;
  background: var(--bg-elevated);
  border: 1px solid var(--border);
  border-radius: 12px;
  box-shadow: var(--shadow);
  font-weight: 500;
  animation: fadeUp 0.3s ease;
}

/* ===== Animations ===== */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(8px); }
  to { opacity: 1; transform: translateY(0); }
}

/* ===== Responsive ===== */
@media (max-width: 900px) {
  .sidebar { display: none; }
  .main { margin-left: 0; padding: 1.5rem 1.25rem 6rem; }
  .mobile-nav { display: flex; }
  .stats-row { grid-template-columns: 1fr 1fr; }
  .dash-grid { grid-template-columns: 1fr; }
  .coach-layout { grid-template-columns: 1fr; height: auto; }
  .coach-sidebar { order: -1; }
  .profile-grid { grid-template-columns: 1fr; }
  .tabs { width: 100%; overflow-x: auto; }
}

@media (max-width: 480px) {
  .stats-row { grid-template-columns: 1fr; }
  .view-header h1 { font-size: 1.5rem; }
}
</style>
</head>
<body>
  <!-- Onboarding Overlay -->
  <div id="onboarding" class="onboarding hidden">
    <div class="onboarding-card">
      <div class="onboarding-header">
        <div class="logo-mark">A</div>
        <h1>Welcome to Aether</h1>
        <p>Your personal AI fitness trainer. Let's build your profile.</p>
      </div>
      <div class="onboarding-steps">
        <div class="step active" data-step="1">
          <label>What should we call you?</label>
          <input type="text" id="ob-name" placeholder="Your name" maxlength="24" />
        </div>
        <div class="step" data-step="2">
          <label>Your current weight (kg)</label>
          <input type="number" id="ob-weight" placeholder="75" min="30" max="250" step="0.1" />
          <label style="margin-top:1rem">Height (cm)</label>
          <input type="number" id="ob-height" placeholder="175" min="100" max="250" />
        </div>
        <div class="step" data-step="3">
          <label>Primary goal</label>
          <div class="goal-grid">
            <button class="goal-btn" data-goal="strength">💪 Strength</button>
            <button class="goal-btn" data-goal="fatloss">🔥 Fat Loss</button>
            <button class="goal-btn" data-goal="muscle">🏋️ Muscle</button>
            <button class="goal-btn" data-goal="endurance">🏃 Endurance</button>
            <button class="goal-btn" data-goal="general">✨ General Fitness</button>
          </div>
        </div>
        <div class="step" data-step="4">
          <label>Experience level</label>
          <div class="goal-grid">
            <button class="goal-btn" data-level="beginner">Beginner</button>
            <button class="goal-btn" data-level="intermediate">Intermediate</button>
            <button class="goal-btn" data-level="advanced">Advanced</button>
          </div>
        </div>
      </div>
      <div class="onboarding-nav">
        <button id="ob-back" class="btn-ghost hidden">Back</button>
        <button id="ob-next" class="btn-primary">Continue</button>
      </div>
    </div>
  </div>

  <!-- App Shell -->
  <div id="app" class="app hidden">
    <!-- Sidebar / Nav -->
    <nav class="sidebar">
      <div class="brand">
        <div class="logo-mark">A</div>
        <span>Aether</span>
      </div>
      <ul class="nav-links">
        <li><a href="#" data-view="dashboard" class="active"><i class="fa-solid fa-house"></i><span>Dashboard</span></a></li>
        <li><a href="#" data-view="workouts"><i class="fa-solid fa-dumbbell"></i><span>Workouts</span></a></li>
        <li><a href="#" data-view="progress"><i class="fa-solid fa-chart-line"></i><span>Progress</span></a></li>
        <li><a href="#" data-view="coach"><i class="fa-solid fa-robot"></i><span>AI Coach</span></a></li>
        <li><a href="#" data-view="profile"><i class="fa-solid fa-user"></i><span>Profile</span></a></li>
      </ul>
      <div class="sidebar-footer">
        <div class="user-chip" id="sidebar-user">
          <div class="avatar" id="avatar">A</div>
          <div>
            <strong id="sidebar-name">Athlete</strong>
            <small id="sidebar-goal">Strength</small>
          </div>
        </div>
      </div>
    </nav>

    <!-- Mobile bottom nav -->
    <nav class="mobile-nav">
      <a href="#" data-view="dashboard" class="active"><i class="fa-solid fa-house"></i></a>
      <a href="#" data-view="workouts"><i class="fa-solid fa-dumbbell"></i></a>
      <a href="#" data-view="progress"><i class="fa-solid fa-chart-line"></i></a>
      <a href="#" data-view="coach"><i class="fa-solid fa-robot"></i></a>
      <a href="#" data-view="profile"><i class="fa-solid fa-user"></i></a>
    </nav>

    <!-- Main Content -->
    <main class="main">
      <!-- DASHBOARD -->
      <section id="view-dashboard" class="view active">
        <header class="view-header">
          <div>
            <p class="eyebrow" id="greeting">Good morning</p>
            <h1 id="dash-name">Ready to train?</h1>
          </div>
          <button class="btn-icon" id="theme-toggle" title="Toggle theme"><i class="fa-solid fa-moon"></i></button>
        </header>

        <div class="stats-row">
          <div class="stat-card glass">
            <div class="stat-icon purple"><i class="fa-solid fa-fire"></i></div>
            <div>
              <span class="stat-label">Streak</span>
              <strong class="stat-value" id="stat-streak">0 days</strong>
            </div>
          </div>
          <div class="stat-card glass">
            <div class="stat-icon teal"><i class="fa-solid fa-dumbbell"></i></div>
            <div>
              <span class="stat-label">Workouts</span>
              <strong class="stat-value" id="stat-workouts">0</strong>
            </div>
          </div>
          <div class="stat-card glass">
            <div class="stat-icon coral"><i class="fa-solid fa-weight-scale"></i></div>
            <div>
              <span class="stat-label">Weight</span>
              <strong class="stat-value" id="stat-weight">— kg</strong>
            </div>
          </div>
          <div class="stat-card glass">
            <div class="stat-icon gold"><i class="fa-solid fa-trophy"></i></div>
            <div>
              <span class="stat-label">This week</span>
              <strong class="stat-value" id="stat-week">0 / 4</strong>
            </div>
          </div>
        </div>

        <div class="dash-grid">
          <div class="card glass today-card">
            <div class="card-header">
              <h2>Today's Session</h2>
              <span class="badge" id="today-badge">Rest Day</span>
            </div>
            <div id="today-workout">
              <p class="muted">No workout scheduled. Generate one with AI Coach or pick from Workouts.</p>
            </div>
            <button class="btn-primary full" id="start-today" style="display:none">Start Workout</button>
          </div>

          <div class="card glass tip-card">
            <div class="card-header">
              <h2>AI Insight</h2>
              <i class="fa-solid fa-sparkles"></i>
            </div>
            <p id="ai-tip">Complete your profile to get personalized coaching.</p>
            <button class="btn-ghost small" id="refresh-tip">New tip</button>
          </div>
        </div>

        <div class="card glass recent-card">
          <div class="card-header">
            <h2>Recent Activity</h2>
          </div>
          <ul class="activity-list" id="recent-list">
            <li class="muted">No workouts logged yet. Let's change that.</li>
          </ul>
        </div>
      </section>

      <!-- WORKOUTS -->
      <section id="view-workouts" class="view">
        <header class="view-header">
          <div>
            <p class="eyebrow">Train</p>
            <h1>Workouts</h1>
          </div>
          <button class="btn-primary" id="generate-plan"><i class="fa-solid fa-wand-magic-sparkles"></i> AI Plan</button>
        </header>

        <div class="tabs">
          <button class="tab active" data-tab="library">Exercise Library</button>
          <button class="tab" data-tab="plans">My Plans</button>
          <button class="tab" data-tab="log">Log Workout</button>
        </div>

        <div id="tab-library" class="tab-panel active">
          <div class="filter-row">
            <input type="search" id="exercise-search" placeholder="Search exercises..." />
            <select id="muscle-filter">
              <option value="">All muscles</option>
              <option value="chest">Chest</option>
              <option value="back">Back</option>
              <option value="shoulders">Shoulders</option>
              <option value="arms">Arms</option>
              <option value="legs">Legs</option>
              <option value="core">Core</option>
              <option value="full">Full Body</option>
            </select>
          </div>
          <div class="exercise-grid" id="exercise-grid"></div>
        </div>

        <div id="tab-plans" class="tab-panel">
          <div id="plans-list" class="plans-list"></div>
        </div>

        <div id="tab-log" class="tab-panel">
          <div class="card glass">
            <h3>Log a Workout</h3>
            <form id="log-form">
              <label>Workout name</label>
              <input type="text" id="log-name" placeholder="e.g. Upper Body Strength" required />
              <label>Duration (minutes)</label>
              <input type="number" id="log-duration" min="5" max="180" value="45" required />
              <label>Exercises (one per line: name — sets × reps)</label>
              <textarea id="log-exercises" rows="5" placeholder="Bench Press — 4 × 8&#10;Pull-ups — 3 × 10"></textarea>
              <label>Notes (optional)</label>
              <input type="text" id="log-notes" placeholder="Felt strong today..." />
              <button type="submit" class="btn-primary full">Save Workout</button>
            </form>
          </div>
        </div>
      </section>

      <!-- PROGRESS -->
      <section id="view-progress" class="view">
        <header class="view-header">
          <div>
            <p class="eyebrow">Track</p>
            <h1>Progress</h1>
          </div>
          <button class="btn-primary" id="log-weight-btn"><i class="fa-solid fa-plus"></i> Log Weight</button>
        </header>

        <div class="stats-row">
          <div class="stat-card glass">
            <span class="stat-label">Current</span>
            <strong class="stat-value" id="prog-weight">— kg</strong>
          </div>
          <div class="stat-card glass">
            <span class="stat-label">Change</span>
            <strong class="stat-value" id="prog-change">—</strong>
          </div>
          <div class="stat-card glass">
            <span class="stat-label">Workouts</span>
            <strong class="stat-value" id="prog-total">0</strong>
          </div>
          <div class="stat-card glass">
            <span class="stat-label">Avg / week</span>
            <strong class="stat-value" id="prog-avg">0</strong>
          </div>
        </div>

        <div class="card glass">
          <div class="card-header">
            <h2>Weight Trend</h2>
          </div>
          <div class="chart-wrap">
            <canvas id="weight-chart"></canvas>
          </div>
        </div>

        <div class="card glass">
          <div class="card-header">
            <h2>Workout History</h2>
          </div>
          <ul class="history-list" id="history-list">
            <li class="muted">No history yet.</li>
          </ul>
        </div>
      </section>

      <!-- AI COACH -->
      <section id="view-coach" class="view">
        <header class="view-header">
          <div>
            <p class="eyebrow">Coach</p>
            <h1>AI Trainer</h1>
          </div>
        </header>

        <div class="coach-layout">
          <div class="chat-panel glass">
            <div class="chat-messages" id="chat-messages">
              <div class="msg ai">
                <div class="msg-avatar">A</div>
                <div class="msg-bubble">
                  <p>Hey! I'm your Aether coach. Ask me anything about training, recovery, form, or programming. I know your goals and will tailor advice to you.</p>
                </div>
              </div>
            </div>
            <form class="chat-input" id="chat-form">
              <input type="text" id="chat-input" placeholder="Ask your coach..." autocomplete="off" />
              <button type="submit" class="btn-icon primary"><i class="fa-solid fa-paper-plane"></i></button>
            </form>
          </div>
          <div class="coach-sidebar">
            <div class="card glass">
              <h3>Quick Actions</h3>
              <button class="quick-btn" data-prompt="Generate a 4-day strength plan for me">4-day Strength Plan</button>
              <button class="quick-btn" data-prompt="What should I eat after a heavy leg day?">Post-workout Nutrition</button>
              <button class="quick-btn" data-prompt="How can I improve my bench press form?">Form Tips</button>
              <button class="quick-btn" data-prompt="I'm feeling sore — should I train today?">Recovery Advice</button>
              <button class="quick-btn" data-prompt="Give me a 20-minute home workout">Quick Home Session</button>
            </div>
            <div class="card glass">
              <h3>Your Context</h3>
              <ul class="context-list" id="coach-context">
                <li>Loading...</li>
              </ul>
            </div>
          </div>
        </div>
      </section>

      <!-- PROFILE -->
      <section id="view-profile" class="view">
        <header class="view-header">
          <div>
            <p class="eyebrow">You</p>
            <h1>Profile</h1>
          </div>
        </header>

        <div class="profile-grid">
          <div class="card glass">
            <h3>Body Stats</h3>
            <form id="profile-form">
              <label>Name</label>
              <input type="text" id="pf-name" />
              <label>Weight (kg)</label>
              <input type="number" id="pf-weight" step="0.1" />
              <label>Height (cm)</label>
              <input type="number" id="pf-height" />
              <label>Goal</label>
              <select id="pf-goal">
                <option value="strength">Strength</option>
                <option value="fatloss">Fat Loss</option>
                <option value="muscle">Muscle Gain</option>
                <option value="endurance">Endurance</option>
                <option value="general">General Fitness</option>
              </select>
              <label>Experience</label>
              <select id="pf-level">
                <option value="beginner">Beginner</option>
                <option value="intermediate">Intermediate</option>
                <option value="advanced">Advanced</option>
              </select>
              <button type="submit" class="btn-primary full">Save Changes</button>
            </form>
          </div>

          <div class="card glass">
            <h3>Calculated</h3>
            <div class="calc-row">
              <span>BMI</span>
              <strong id="calc-bmi">—</strong>
            </div>
            <div class="calc-row">
              <span>Est. BMR</span>
              <strong id="calc-bmr">— kcal</strong>
            </div>
            <div class="calc-row">
              <span>Est. TDEE</span>
              <strong id="calc-tdee">— kcal</strong>
            </div>
            <p class="muted small" style="margin-top:1rem">Estimates use Mifflin-St Jeor. TDEE assumes moderate activity.</p>
          </div>

          <div class="card glass danger-zone">
            <h3>Data</h3>
            <button class="btn-ghost" id="export-data">Export JSON</button>
            <button class="btn-danger" id="reset-data">Reset All Data</button>
          </div>
        </div>
      </section>
    </main>
  </div>

  <!-- Modals -->
  <div id="modal" class="modal hidden">
    <div class="modal-card glass">
      <button class="modal-close" id="modal-close"><i class="fa-solid fa-xmark"></i></button>
      <div id="modal-body"></div>
    </div>
  </div>

  <div id="toast" class="toast hidden"></div>

<script>
/* ===== Aether AI Fitness Trainer ===== */

const STORAGE_KEY = 'aether_v1';

const EXERCISES = [
  { id: 'bp', name: 'Barbell Bench Press', muscle: 'chest', level: 'intermediate', equipment: 'barbell', cues: 'Retract scapula, feet planted, lower to mid-chest, press up explosively.' },
  { id: 'dbp', name: 'Dumbbell Bench Press', muscle: 'chest', level: 'beginner', equipment: 'dumbbell', cues: 'Neutral grip option available. Full range of motion.' },
  { id: 'pu', name: 'Push-ups', muscle: 'chest', level: 'beginner', equipment: 'bodyweight', cues: 'Body straight, core tight, chest to floor.' },
  { id: 'dip', name: 'Dips', muscle: 'chest', level: 'intermediate', equipment: 'bodyweight', cues: 'Lean forward for chest emphasis. Control the descent.' },
  { id: 'fly', name: 'Dumbbell Flyes', muscle: 'chest', level: 'intermediate', equipment: 'dumbbell', cues: 'Slight bend in elbows, stretch at bottom, squeeze at top.' },
  { id: 'row', name: 'Barbell Row', muscle: 'back', level: 'intermediate', equipment: 'barbell', cues: 'Hinge at hips, pull to lower chest, squeeze scapulae.' },
  { id: 'pullup', name: 'Pull-ups', muscle: 'back', level: 'intermediate', equipment: 'bodyweight', cues: 'Full hang to chin over bar. Avoid kipping unless intentional.' },
  { id: 'lat', name: 'Lat Pulldown', muscle: 'back', level: 'beginner', equipment: 'cable', cues: 'Pull to upper chest, lean slightly back, control the return.' },
  { id: 'sp', name: 'Seated Cable Row', muscle: 'back', level: 'beginner', equipment: 'cable', cues: 'Chest up, pull handles to torso, squeeze mid-back.' },
  { id: 'dl', name: 'Conventional Deadlift', muscle: 'back', level: 'advanced', equipment: 'barbell', cues: 'Neutral spine, drive through floor, lock hips and knees together.' },
  { id: 'ohp', name: 'Overhead Press', muscle: 'shoulders', level: 'intermediate', equipment: 'barbell', cues: 'Brace core, press straight up, head through at top.' },
  { id: 'dbohp', name: 'Dumbbell Shoulder Press', muscle: 'shoulders', level: 'beginner', equipment: 'dumbbell', cues: 'Seated or standing. Full lockout without excessive lean.' },
  { id: 'lateral', name: 'Lateral Raises', muscle: 'shoulders', level: 'beginner', equipment: 'dumbbell', cues: 'Slight bend, raise to just above parallel, control eccentric.' },
  { id: 'face', name: 'Face Pulls', muscle: 'shoulders', level: 'beginner', equipment: 'cable', cues: 'Pull to face, external rotation at end. Great for posture.' },
  { id: 'curl', name: 'Barbell Curl', muscle: 'arms', level: 'beginner', equipment: 'barbell', cues: 'Elbows fixed, no swing. Full stretch at bottom.' },
  { id: 'hc', name: 'Hammer Curl', muscle: 'arms', level: 'beginner', equipment: 'dumbbell', cues: 'Neutral grip targets brachialis and forearms.' },
  { id: 'tri', name: 'Tricep Pushdown', muscle: 'arms', level: 'beginner', equipment: 'cable', cues: 'Elbows locked at sides, full extension, squeeze.' },
  { id: 'skull', name: 'Skull Crushers', muscle: 'arms', level: 'intermediate', equipment: 'barbell', cues: 'Lower behind head or to forehead. Keep upper arms still.' },
  { id: 'squat', name: 'Back Squat', muscle: 'legs', level: 'intermediate', equipment: 'barbell', cues: 'Break at hips and knees together, depth below parallel if mobility allows.' },
  { id: 'fsquat', name: 'Front Squat', muscle: 'legs', level: 'advanced', equipment: 'barbell', cues: 'Elbows high, torso upright, quads emphasized.' },
  { id: 'rdl', name: 'Romanian Deadlift', muscle: 'legs', level: 'intermediate', equipment: 'barbell', cues: 'Soft knees, hinge until hamstring stretch, drive hips forward.' },
  { id: 'lunges', name: 'Walking Lunges', muscle: 'legs', level: 'beginner', equipment: 'bodyweight', cues: 'Long stride, knee tracks over mid-foot, upright torso.' },
  { id: 'legpress', name: 'Leg Press', muscle: 'legs', level: 'beginner', equipment: 'machine', cues: 'Feet mid-platform, full range without lower back rounding.' },
  { id: 'calf', name: 'Standing Calf Raise', muscle: 'legs', level: 'beginner', equipment: 'machine', cues: 'Full stretch at bottom, pause at top.' },
  { id: 'plank', name: 'Plank', muscle: 'core', level: 'beginner', equipment: 'bodyweight', cues: 'Body straight, glutes and core braced. Breathe.' },
  { id: 'hang', name: 'Hanging Leg Raise', muscle: 'core', level: 'intermediate', equipment: 'bodyweight', cues: 'Control swing, lift with abs not momentum.' },
  { id: 'crunch', name: 'Cable Crunch', muscle: 'core', level: 'beginner', equipment: 'cable', cues: 'Round spine, pull with abs, not arms.' },
  { id: 'bird', name: 'Bird Dog', muscle: 'core', level: 'beginner', equipment: 'bodyweight', cues: 'Opposite arm/leg, keep hips level, slow and controlled.' },
  { id: 'burpee', name: 'Burpees', muscle: 'full', level: 'intermediate', equipment: 'bodyweight', cues: 'Chest to floor option. Explosive jump.' },
  { id: 'kbswing', name: 'Kettlebell Swing', muscle: 'full', level: 'intermediate', equipment: 'kettlebell', cues: 'Hinge pattern, power from hips, arms relaxed.' },
];

const TIPS = {
  strength: [
    "Prioritize progressive overload. Add weight or reps every week when form stays clean.",
    "Compound lifts first. Squat, hinge, press, and pull before isolation work.",
    "Sleep is a performance drug. Aim for 7–9 hours — strength gains happen during recovery.",
    "Warm up with the empty bar and ramp sets. Cold max attempts invite injury.",
    "Track every set. What gets measured gets improved."
  ],
  fatloss: [
    "A small calorie deficit (300–500 kcal) preserves muscle better than aggressive cuts.",
    "Keep protein high (1.6–2.2 g/kg). It protects muscle and keeps you full.",
    "Lift heavy even while cutting. Muscle is metabolically expensive tissue you want to keep.",
    "NEAT matters more than you think. Walk 8–10k steps daily.",
    "Consistency beats perfection. One bad meal doesn't erase a week of good ones."
  ],
  muscle: [
    "Volume is the main driver of hypertrophy. 10–20 hard sets per muscle per week is a solid range.",
    "Close to failure (0–3 RIR) on most sets. Leave 1–2 reps in the tank on heavy compounds.",
    "Eat in a slight surplus. Muscle growth requires energy and building blocks.",
    "Vary rep ranges: 6–12 for most work, occasional 15–20 for metabolic stress.",
    "Mind-muscle connection is real for isolation. Slow the eccentric."
  ],
  endurance: [
    "Zone 2 base building (conversational pace) develops your aerobic engine without excess fatigue.",
    "One quality interval session per week is often enough for most goals.",
    "Strength training still matters — it improves running economy and injury resilience.",
    "Fuel longer sessions. Under-fueling endurance work is a fast path to burnout.",
    "Recovery runs should feel easy. If they're hard, you're not recovering."
  ],
  general: [
    "Something is better than nothing. A 20-minute session beats a skipped one.",
    "Master the fundamentals before chasing novelty. Squats, hinges, pushes, pulls, carries.",
    "Consistency compounds. Three solid sessions a week for a year transforms you.",
    "Listen to your joints more than your ego. Pain is information.",
    "Celebrate non-scale victories: better sleep, more energy, clothes fitting differently."
  ]
};

const PLANS = {
  strength: {
    name: "4-Day Strength Foundation",
    days: [
      { name: "Day 1 — Upper Push", exercises: [
        { name: "Barbell Bench Press", sets: "4 × 5" },
        { name: "Overhead Press", sets: "3 × 6–8" },
        { name: "Dips", sets: "3 × 8–12" },
        { name: "Lateral Raises", sets: "3 × 12–15" },
        { name: "Tricep Pushdown", sets: "3 × 10–12" }
      ]},
      { name: "Day 2 — Lower", exercises: [
        { name: "Back Squat", sets: "4 × 5" },
        { name: "Romanian Deadlift", sets: "3 × 6–8" },
        { name: "Walking Lunges", sets: "3 × 10/leg" },
        { name: "Standing Calf Raise", sets: "4 × 12–15" },
        { name: "Plank", sets: "3 × 45s" }
      ]},
      { name: "Day 3 — Upper Pull", exercises: [
        { name: "Pull-ups", sets: "4 × AMRAP" },
        { name: "Barbell Row", sets: "4 × 6–8" },
        { name: "Face Pulls", sets: "3 × 15" },
        { name: "Barbell Curl", sets: "3 × 8–12" },
        { name: "Hammer Curl", sets: "2 × 12" }
      ]},
      { name: "Day 4 — Full / Power", exercises: [
        { name: "Conventional Deadlift", sets: "3 × 3–5" },
        { name: "Dumbbell Bench Press", sets: "3 × 8" },
        { name: "Front Squat", sets: "3 × 6" },
        { name: "Kettlebell Swing", sets: "3 × 15" },
        { name: "Hanging Leg Raise", sets: "3 × 10" }
      ]}
    ]
  },
  fatloss: {
    name: "4-Day Metabolic Strength",
    days: [
      { name: "Day 1 — Full Body A", exercises: [
        { name: "Back Squat", sets: "4 × 8" },
        { name: "Dumbbell Bench Press", sets: "3 × 10" },
        { name: "Barbell Row", sets: "3 × 10" },
        { name: "Walking Lunges", sets: "3 × 12/leg" },
        { name: "Plank", sets: "3 × 40s" }
      ]},
      { name: "Day 2 — Conditioning", exercises: [
        { name: "Kettlebell Swing", sets: "5 × 15" },
        { name: "Burpees", sets: "4 × 10" },
        { name: "Push-ups", sets: "3 × max" },
        { name: "Bird Dog", sets: "3 × 10/side" }
      ]},
      { name: "Day 3 — Full Body B", exercises: [
        { name: "Romanian Deadlift", sets: "4 × 8" },
        { name: "Overhead Press", sets: "3 × 10" },
        { name: "Pull-ups", sets: "3 × AMRAP" },
        { name: "Leg Press", sets: "3 × 12" },
        { name: "Cable Crunch", sets: "3 × 15" }
      ]},
      { name: "Day 4 — Upper Density", exercises: [
        { name: "Dumbbell Shoulder Press", sets: "3 × 12" },
        { name: "Lat Pulldown", sets: "3 × 12" },
        { name: "Lateral Raises", sets: "3 × 15" },
        { name: "Tricep Pushdown", sets: "3 × 12" },
        { name: "Barbell Curl", sets: "3 × 12" }
      ]}
    ]
  },
  muscle: {
    name: "5-Day Hypertrophy Split",
    days: [
      { name: "Day 1 — Chest", exercises: [
        { name: "Barbell Bench Press", sets: "4 × 6–8" },
        { name: "Dumbbell Flyes", sets: "3 × 10–12" },
        { name: "Dips", sets: "3 × 8–12" },
        { name: "Push-ups", sets: "2 × max" }
      ]},
      { name: "Day 2 — Back", exercises: [
        { name: "Pull-ups", sets: "4 × AMRAP" },
        { name: "Barbell Row", sets: "4 × 8" },
        { name: "Seated Cable Row", sets: "3 × 10–12" },
        { name: "Face Pulls", sets: "3 × 15" }
      ]},
      { name: "Day 3 — Legs", exercises: [
        { name: "Back Squat", sets: "4 × 6–8" },
        { name: "Romanian Deadlift", sets: "3 × 8–10" },
        { name: "Leg Press", sets: "3 × 12" },
        { name: "Walking Lunges", sets: "3 × 10/leg" },
        { name: "Standing Calf Raise", sets: "4 × 12–15" }
      ]},
      { name: "Day 4 — Shoulders & Arms", exercises: [
        { name: "Overhead Press", sets: "4 × 6–8" },
        { name: "Lateral Raises", sets: "4 × 12–15" },
        { name: "Barbell Curl", sets: "3 × 8–12" },
        { name: "Skull Crushers", sets: "3 × 10" },
        { name: "Hammer Curl", sets: "2 × 12" }
      ]},
      { name: "Day 5 — Full / Weak Points", exercises: [
        { name: "Front Squat", sets: "3 × 8" },
        { name: "Dumbbell Bench Press", sets: "3 × 10" },
        { name: "Lat Pulldown", sets: "3 × 12" },
        { name: "Hanging Leg Raise", sets: "3 × 12" },
        { name: "Bird Dog", sets: "3 × 10/side" }
      ]}
    ]
  },
  endurance: {
    name: "3-Day Strength + Conditioning",
    days: [
      { name: "Day 1 — Lower + Conditioning", exercises: [
        { name: "Back Squat", sets: "3 × 8" },
        { name: "Romanian Deadlift", sets: "3 × 8" },
        { name: "Walking Lunges", sets: "3 × 12/leg" },
        { name: "Kettlebell Swing", sets: "4 × 20" },
        { name: "Plank", sets: "3 × 45s" }
      ]},
      { name: "Day 2 — Upper + Core", exercises: [
        { name: "Push-ups", sets: "4 × max" },
        { name: "Pull-ups", sets: "4 × AMRAP" },
        { name: "Dumbbell Shoulder Press", sets: "3 × 10" },
        { name: "Face Pulls", sets: "3 × 15" },
        { name: "Hanging Leg Raise", sets: "3 × 12" }
      ]},
      { name: "Day 3 — Full Body Circuit", exercises: [
        { name: "Burpees", sets: "5 × 8" },
        { name: "Kettlebell Swing", sets: "5 × 15" },
        { name: "Walking Lunges", sets: "3 × 20 steps" },
        { name: "Push-ups", sets: "3 × max" },
        { name: "Bird Dog", sets: "3 × 12/side" }
      ]}
    ]
  },
  general: {
    name: "3-Day Full Body",
    days: [
      { name: "Day A", exercises: [
        { name: "Back Squat", sets: "3 × 8" },
        { name: "Barbell Bench Press", sets: "3 × 8" },
        { name: "Barbell Row", sets: "3 × 8" },
        { name: "Plank", sets: "3 × 40s" }
      ]},
      { name: "Day B", exercises: [
        { name: "Romanian Deadlift", sets: "3 × 8" },
        { name: "Overhead Press", sets: "3 × 8" },
        { name: "Pull-ups", sets: "3 × AMRAP" },
        { name: "Walking Lunges", sets: "3 × 10/leg" }
      ]},
      { name: "Day C", exercises: [
        { name: "Front Squat", sets: "3 × 6" },
        { name: "Dumbbell Bench Press", sets: "3 × 10" },
        { name: "Seated Cable Row", sets: "3 × 10" },
        { name: "Hanging Leg Raise", sets: "3 × 10" },
        { name: "Lateral Raises", sets: "2 × 15" }
      ]}
    ]
  }
};

// ===== State =====
let state = {
  profile: null,
  workouts: [],
  weights: [],
  plans: [],
  streak: 0,
  lastWorkoutDate: null,
  chatHistory: []
};

let weightChart = null;
let onboardingStep = 1;
let selectedGoal = null;
let selectedLevel = null;

// ===== Persistence =====
function load() {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (raw) {
      const data = JSON.parse(raw);
      state = { ...state, ...data };
    }
  } catch (e) {
    console.warn('Failed to load state', e);
  }
}

function save() {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
}

// ===== Helpers =====
function $(sel) { return document.querySelector(sel); }
function $$(sel) { return document.querySelectorAll(sel); }

function toast(msg, duration = 2800) {
  const el = $('#toast');
  el.textContent = msg;
  el.classList.remove('hidden');
  clearTimeout(el._t);
  el._t = setTimeout(() => el.classList.add('hidden'), duration);
}

function greeting() {
  const h = new Date().getHours();
  if (h < 12) return 'Good morning';
  if (h < 17) return 'Good afternoon';
  return 'Good evening';
}

function formatDate(iso) {
  const d = new Date(iso);
  return d.toLocaleDateString(undefined, { month: 'short', day: 'numeric', year: 'numeric' });
}

function daysAgo(iso) {
  const diff = Date.now() - new Date(iso).getTime();
  return Math.floor(diff / 86400000);
}

function calcBMI(weight, height) {
  if (!weight || !height) return null;
  const m = height / 100;
  return +(weight / (m * m)).toFixed(1);
}

function calcBMR(weight, height, age = 30, sex = 'male') {
  // Mifflin-St Jeor (male default for simplicity)
  if (!weight || !height) return null;
  return Math.round(10 * weight + 6.25 * height - 5 * age + 5);
}

function calcStreak() {
  if (!state.workouts.length) return 0;
  const dates = [...new Set(state.workouts.map(w => w.date.slice(0, 10)))].sort().reverse();
  let streak = 0;
  let cursor = new Date();
  cursor.setHours(0, 0, 0, 0);

  for (const d of dates) {
    const wd = new Date(d);
    wd.setHours(0, 0, 0, 0);
    const diff = Math.round((cursor - wd) / 86400000);
    if (diff === 0 || diff === 1) {
      streak++;
      cursor = wd;
      cursor.setDate(cursor.getDate() - 1);
    } else break;
  }
  return streak;
}

function workoutsThisWeek() {
  const now = new Date();
  const start = new Date(now);
  start.setDate(now.getDate() - now.getDay());
  start.setHours(0, 0, 0, 0);
  return state.workouts.filter(w => new Date(w.date) >= start).length;
}

// ===== Onboarding =====
function showOnboarding() {
  $('#onboarding').classList.remove('hidden');
  $('#app').classList.add('hidden');
  onboardingStep = 1;
  updateOnboardingUI();
}

function updateOnboardingUI() {
  $$('.step').forEach(s => s.classList.toggle('active', +s.dataset.step === onboardingStep));
  $('#ob-back').classList.toggle('hidden', onboardingStep === 1);
  $('#ob-next').textContent = onboardingStep === 4 ? 'Start Training' : 'Continue';
}

function finishOnboarding() {
  const name = $('#ob-name').value.trim() || 'Athlete';
  const weight = parseFloat($('#ob-weight').value) || 75;
  const height = parseFloat($('#ob-height').value) || 175;
  state.profile = {
    name,
    weight,
    height,
    goal: selectedGoal || 'general',
    level: selectedLevel || 'beginner',
    createdAt: new Date().toISOString()
  };
  state.weights = [{ date: new Date().toISOString(), weight }];
  save();
  $('#onboarding').classList.add('hidden');
  $('#app').classList.remove('hidden');
  renderAll();
  toast(`Welcome, ${name}. Let's build something strong.`);
}

// ===== Rendering =====
function renderAll() {
  if (!state.profile) return;
  renderSidebar();
  renderDashboard();
  renderExercises();
  renderPlans();
  renderProgress();
  renderProfile();
  renderCoachContext();
}

function renderSidebar() {
  const p = state.profile;
  $('#sidebar-name').textContent = p.name;
  $('#sidebar-goal').textContent = p.goal;
  $('#avatar').textContent = p.name.charAt(0).toUpperCase();
}

function renderDashboard() {
  const p = state.profile;
  $('#greeting').textContent = greeting();
  $('#dash-name').textContent = `${p.name}, ready to train?`;
  $('#stat-streak').textContent = `${calcStreak()} days`;
  $('#stat-workouts').textContent = state.workouts.length;
  $('#stat-weight').textContent = `${p.weight} kg`;
  $('#stat-week').textContent = `${workoutsThisWeek()} / 4`;

  // AI tip
  const tips = TIPS[p.goal] || TIPS.general;
  const tip = tips[Math.floor(Math.random() * tips.length)];
  $('#ai-tip').textContent = tip;

  // Recent
  const list = $('#recent-list');
  if (!state.workouts.length) {
    list.innerHTML = '<li class="muted">No workouts logged yet. Let\'s change that.</li>';
  } else {
    list.innerHTML = state.workouts.slice(0, 5).map(w => `
      <li>
        <div>
          <div class="act-title">${w.name}</div>
          <div class="act-meta">${formatDate(w.date)} · ${w.duration} min</div>
        </div>
        <span class="badge">${w.exercises?.length || 0} moves</span>
      </li>
    `).join('');
  }

  // Today's session (simple: show first plan day if exists)
  const todayEl = $('#today-workout');
  const badge = $('#today-badge');
  const startBtn = $('#start-today');
  if (state.plans.length) {
    const plan = state.plans[0];
    const dayIdx = workoutsThisWeek() % plan.days.length;
    const day = plan.days[dayIdx];
    badge.textContent = day.name;
    badge.className = 'badge active';
    todayEl.innerHTML = day.exercises.map(e => `
      <div class="exercise-item">
        <span class="ex-name">${e.name}</span>
        <span class="ex-meta">${e.sets}</span>
      </div>
    `).join('');
    startBtn.style.display = 'block';
    startBtn.onclick = () => {
      // Pre-fill log form
      switchView('workouts');
      document.querySelector('[data-tab="log"]').click();
      $('#log-name').value = day.name;
      $('#log-exercises').value = day.exercises.map(e => `${e.name} — ${e.sets}`).join('\n');
    };
  } else {
    badge.textContent = 'Rest Day';
    badge.className = 'badge rest';
    todayEl.innerHTML = '<p class="muted">No workout scheduled. Generate one with AI Coach or pick from Workouts.</p>';
    startBtn.style.display = 'none';
  }
}

function renderExercises() {
  const q = ($('#exercise-search')?.value || '').toLowerCase();
  const muscle = $('#muscle-filter')?.value || '';
  const grid = $('#exercise-grid');
  const filtered = EXERCISES.filter(e => {
    const matchQ = !q || e.name.toLowerCase().includes(q) || e.muscle.includes(q);
    const matchM = !muscle || e.muscle === muscle;
    return matchQ && matchM;
  });
  grid.innerHTML = filtered.map(e => `
    <div class="ex-card" data-id="${e.id}">
      <h4>${e.name}</h4>
      <p class="muted small">${e.cues}</p>
      <div class="ex-tags">
        <span class="ex-tag">${e.muscle}</span>
        <span class="ex-tag">${e.level}</span>
        <span class="ex-tag">${e.equipment}</span>
      </div>
    </div>
  `).join('');

  grid.querySelectorAll('.ex-card').forEach(card => {
    card.addEventListener('click', () => {
      const ex = EXERCISES.find(x => x.id === card.dataset.id);
      openModal(`
        <h2 style="margin-bottom:0.75rem;font-family:var(--font-display)">${ex.name}</h2>
        <p style="color:var(--text-muted);margin-bottom:1rem">${ex.cues}</p>
        <div class="ex-tags" style="margin-bottom:1.5rem">
          <span class="ex-tag">${ex.muscle}</span>
          <span class="ex-tag">${ex.level}</span>
          <span class="ex-tag">${ex.equipment}</span>
        </div>
        <button class="btn-primary full" id="add-to-log">Add to Log Form</button>
      `);
      $('#add-to-log').onclick = () => {
        switchView('workouts');
        document.querySelector('[data-tab="log"]').click();
        const ta = $('#log-exercises');
        ta.value = (ta.value ? ta.value + '\n' : '') + `${ex.name} — 3 × 10`;
        closeModal();
        toast('Added to log form');
      };
    });
  });
}

function renderPlans() {
  const list = $('#plans-list');
  if (!state.plans.length) {
    list.innerHTML = `
      <div class="card glass">
        <p class="muted">No plans yet. Hit <strong>AI Plan</strong> to generate a program tailored to your goal (${state.profile.goal}).</p>
      </div>`;
    return;
  }
  list.innerHTML = state.plans.map((p, i) => `
    <div class="plan-card">
      <h4>${p.name}</h4>
      <p class="muted small">${p.days.length} training days</p>
      <div class="plan-days">
        ${p.days.map(d => `<span class="plan-day">${d.name}</span>`).join('')}
      </div>
      <div style="margin-top:1rem;display:flex;gap:0.5rem">
        <button class="btn-ghost small use-plan" data-idx="${i}">Use Today</button>
        <button class="btn-ghost small delete-plan" data-idx="${i}" style="color:var(--danger)">Remove</button>
      </div>
    </div>
  `).join('');

  list.querySelectorAll('.use-plan').forEach(btn => {
    btn.onclick = () => {
      const plan = state.plans[+btn.dataset.idx];
      const day = plan.days[0];
      switchView('workouts');
      document.querySelector('[data-tab="log"]').click();
      $('#log-name').value = day.name;
      $('#log-exercises').value = day.exercises.map(e => `${e.name} — ${e.sets}`).join('\n');
      toast('Loaded into log form');
    };
  });
  list.querySelectorAll('.delete-plan').forEach(btn => {
    btn.onclick = () => {
      state.plans.splice(+btn.dataset.idx, 1);
      save();
      renderPlans();
      renderDashboard();
      toast('Plan removed');
    };
  });
}

function renderProgress() {
  const p = state.profile;
  $('#prog-weight').textContent = `${p.weight} kg`;
  $('#prog-total').textContent = state.workouts.length;

  if (state.weights.length >= 2) {
    const first = state.weights[0].weight;
    const last = state.weights[state.weights.length - 1].weight;
    const diff = +(last - first).toFixed(1);
    $('#prog-change').textContent = `${diff > 0 ? '+' : ''}${diff} kg`;
    $('#prog-change').style.color = diff < 0 ? 'var(--success)' : diff > 0 ? 'var(--coral)' : 'inherit';
  } else {
    $('#prog-change').textContent = '—';
  }

  const weeks = Math.max(1, Math.ceil((Date.now() - new Date(p.createdAt || Date.now()).getTime()) / (7 * 86400000)));
  $('#prog-avg').textContent = (state.workouts.length / weeks).toFixed(1);

  // History
  const hist = $('#history-list');
  if (!state.workouts.length) {
    hist.innerHTML = '<li class="muted">No history yet.</li>';
  } else {
    hist.innerHTML = state.workouts.map(w => `
      <li>
        <div>
          <div class="act-title">${w.name}</div>
          <div class="act-meta">${formatDate(w.date)} · ${w.duration} min${w.notes ? ' · ' + w.notes : ''}</div>
        </div>
      </li>
    `).join('');
  }

  // Chart
  renderWeightChart();
}

function renderWeightChart() {
  const ctx = $('#weight-chart');
  if (!ctx) return;
  const labels = state.weights.map(w => formatDate(w.date));
  const data = state.weights.map(w => w.weight);

  if (weightChart) weightChart.destroy();

  weightChart = new Chart(ctx, {
    type: 'line',
    data: {
      labels,
      datasets: [{
        label: 'Weight (kg)',
        data,
        borderColor: '#7c5cff',
        backgroundColor: 'rgba(124, 92, 255, 0.12)',
        fill: true,
        tension: 0.35,
        pointRadius: 4,
        pointBackgroundColor: '#7c5cff',
        pointBorderColor: '#fff',
        pointBorderWidth: 2
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: { display: false }
      },
      scales: {
        x: {
          grid: { color: 'rgba(255,255,255,0.04)' },
          ticks: { color: '#6b7385', maxTicksLimit: 8 }
        },
        y: {
          grid: { color: 'rgba(255,255,255,0.06)' },
          ticks: { color: '#6b7385' }
        }
      }
    }
  });
}

function renderProfile() {
  const p = state.profile;
  $('#pf-name').value = p.name;
  $('#pf-weight').value = p.weight;
  $('#pf-height').value = p.height;
  $('#pf-goal').value = p.goal;
  $('#pf-level').value = p.level;

  const bmi = calcBMI(p.weight, p.height);
  const bmr = calcBMR(p.weight, p.height);
  $('#calc-bmi').textContent = bmi ?? '—';
  $('#calc-bmr').textContent = bmr ? `${bmr} kcal` : '—';
  $('#calc-tdee').textContent = bmr ? `${Math.round(bmr * 1.55)} kcal` : '—';
}

function renderCoachContext() {
  const p = state.profile;
  $('#coach-context').innerHTML = `
    <li><strong>Name:</strong> ${p.name}</li>
    <li><strong>Goal:</strong> ${p.goal}</li>
    <li><strong>Level:</strong> ${p.level}</li>
    <li><strong>Weight:</strong> ${p.weight} kg</li>
    <li><strong>Workouts logged:</strong> ${state.workouts.length}</li>
    <li><strong>Current streak:</strong> ${calcStreak()} days</li>
  `;
}

// ===== AI Coach =====
function generateAIResponse(userMsg) {
  const p = state.profile;
  const msg = userMsg.toLowerCase();
  let reply = '';

  // Plan generation
  if (msg.includes('plan') || msg.includes('program') || msg.includes('routine') || msg.includes('4-day') || msg.includes('5-day')) {
    const plan = PLANS[p.goal] || PLANS.general;
    state.plans = [plan];
    save();
    renderPlans();
    renderDashboard();
    reply = `I've created a **${plan.name}** based on your ${p.goal} goal and ${p.level} level.\n\n`;
    plan.days.forEach(d => {
      reply += `**${d.name}**\n`;
      d.exercises.forEach(e => reply += `• ${e.name} — ${e.sets}\n`);
      reply += '\n';
    });
    reply += `You can find it under Workouts → My Plans. Want me to adjust volume, add a day, or swap any exercises?`;
    return reply;
  }

  // Nutrition
  if (msg.includes('eat') || msg.includes('nutrition') || msg.includes('food') || msg.includes('protein') || msg.includes('calorie')) {
    const bmr = calcBMR(p.weight, p.height) || 1800;
    const tdee = Math.round(bmr * 1.55);
    if (p.goal === 'fatloss') {
      reply = `For fat loss at your stats, aim for roughly **${tdee - 400}–${tdee - 250} kcal** per day with **${Math.round(p.weight * 1.8)}–${Math.round(p.weight * 2.2)} g protein**.\n\nPost-workout: a meal with protein + carbs within a few hours is ideal — chicken/rice, Greek yogurt + fruit, or a shake if you're on the go. Don't overthink the "anabolic window"; total daily intake matters more.`;
    } else if (p.goal === 'muscle') {
      reply = `For muscle gain, target around **${tdee + 200}–${tdee + 400} kcal** and **${Math.round(p.weight * 1.6)}–${Math.round(p.weight * 2.2)} g protein** daily.\n\nAfter heavy sessions, prioritize protein (30–40 g) and some carbs to refill glycogen. Whole foods first; supplements are optional.`;
    } else {
      reply = `Maintenance is roughly **${tdee} kcal**. Keep protein around **${Math.round(p.weight * 1.6)} g**.\n\nPost-workout nutrition: protein + carbs supports recovery. Timing is flexible — just hit your daily targets consistently.`;
    }
    return reply;
  }

  // Form
  if (msg.includes('form') || msg.includes('technique') || msg.includes('bench') || msg.includes('squat') || msg.includes('deadlift')) {
    if (msg.includes('bench')) {
      reply = `**Bench Press form cues:**\n• Retract and depress your scapulae (shoulder blades pinched and down)\n• Feet planted, slight arch is fine\n• Lower the bar to mid-chest with control\n• Elbows ~45–70° from torso (not flared 90°)\n• Drive up explosively, lock out without hyperextending\n\nCommon mistakes: bouncing off the chest, excessive elbow flare, and lifting your butt. Film yourself from the side if possible.`;
    } else if (msg.includes('squat')) {
      reply = `**Squat form cues:**\n• Brace your core hard (as if about to be punched)\n• Break at hips and knees together\n• Knees track over mid-foot\n• Depth: ideally hip crease below knee if mobility allows\n• Drive through mid-foot, keep chest up\n\nIf you round your lower back at the bottom, reduce depth or improve ankle/hip mobility first.`;
    } else if (msg.includes('deadlift')) {
      reply = `**Deadlift form cues:**\n• Bar over mid-foot, shins close\n• Neutral spine (neither rounded nor hyperextended)\n• Hips high enough that hamstrings are loaded\n• Push the floor away; don't "pull" with your back\n• Lock hips and knees together at the top\n\nIf your back rounds, the weight is too heavy or your setup is off. Reset and go lighter.`;
    } else {
      reply = `Form is non-negotiable. Film your sets from the side and review them. Key principles for almost every lift:\n• Neutral spine under load\n• Controlled eccentric (lowering)\n• Full range of motion when possible\n• Brace before you move\n\nTell me which lift you want cues for and I'll get specific.`;
    }
    return reply;
  }

  // Recovery / sore
  if (msg.includes('sore') || msg.includes('recovery') || msg.includes('rest') || msg.includes('hurt') || msg.includes('pain')) {
    reply = `Soreness (DOMS) is normal, especially when starting or changing programs. It usually peaks 24–48 h later.\n\n**Train through mild soreness** if movement quality is still good. **Skip or modify** if:\n• Sharp or joint pain (not muscle)\n• Range of motion is significantly limited\n• You feel run-down systemically\n\nActive recovery (walk, light mobility, easy cycling) often helps more than complete rest. Sleep, protein, and managing stress are your highest-leverage recovery tools.`;
    return reply;
  }

  // Home / quick workout
  if (msg.includes('home') || msg.includes('20-minute') || msg.includes('quick') || msg.includes('no equipment') || msg.includes('bodyweight')) {
    reply = `**20-minute home session** (no equipment):\n\n1. **Push-ups** — 3 × max (knee variation ok)\n2. **Walking Lunges** or reverse lunges — 3 × 10/leg\n3. **Plank** — 3 × 30–45 s\n4. **Bird Dog** — 3 × 8/side\n5. **Burpees** or squat jumps — 3 × 8\n\nRest 45–60 s between sets. Move with intent. Want a harder version or one that uses a backpack for load?`;
    return reply;
  }

  // Motivation / general
  if (msg.includes('motivat') || msg.includes('stuck') || msg.includes('plateau') || msg.includes('tired')) {
    reply = `Plateaus and low motivation are part of the process, not a sign you're failing.\n\nPractical resets:\n• Drop volume 30–40% for a week (deload)\n• Change one variable: rep range, exercise variation, or rest times\n• Revisit why you started — write it down\n• Shrink the goal: just show up for 20 minutes\n\nYou've logged ${state.workouts.length} workouts. That consistency already puts you ahead of most people. Keep stacking days.`;
    return reply;
  }

  // Default contextual reply
  const goalAdvice = {
    strength: "Focus on progressive overload on the big compounds and keep recovery high.",
    fatloss: "Lift to preserve muscle, walk more, and keep the deficit modest and sustainable.",
    muscle: "Prioritize volume and proximity to failure, and make sure you're eating enough.",
    endurance: "Build your aerobic base and protect strength with 2 short lifting sessions.",
    general: "Consistency with the fundamentals will take you further than any fancy program."
  };

  reply = `Got it. Based on your **${p.goal}** goal and **${p.level}** experience:\n\n${goalAdvice[p.goal] || goalAdvice.general}\n\nYou can ask me for a full program, form cues on any lift, nutrition targets, recovery advice, or a quick session. What do you want to work on?`;
  return reply;
}

function addChatMessage(text, isUser = false) {
  const container = $('#chat-messages');
  const div = document.createElement('div');
  div.className = `msg ${isUser ? 'user' : 'ai'}`;
  // Simple markdown-ish: **bold** and newlines
  const html = text
    .replace(/\*\*(.+?)\*\*/g, '<strong>$1</strong>')
    .replace(/\n/g, '<br>');
  div.innerHTML = `
    <div class="msg-avatar">${isUser ? state.profile.name.charAt(0).toUpperCase() : 'A'}</div>
    <div class="msg-bubble"><p>${html}</p></div>
  `;
  container.appendChild(div);
  container.scrollTop = container.scrollHeight;
}

// ===== Navigation =====
function switchView(view) {
  $$('.view').forEach(v => v.classList.remove('active'));
  $(`#view-${view}`)?.classList.add('active');
  $$('.nav-links a, .mobile-nav a').forEach(a => {
    a.classList.toggle('active', a.dataset.view === view);
  });
}

// ===== Modal =====
function openModal(html) {
  $('#modal-body').innerHTML = html;
  $('#modal').classList.remove('hidden');
}
function closeModal() {
  $('#modal').classList.add('hidden');
}

// ===== Events =====
function bindEvents() {
  // Onboarding
  $('#ob-next').onclick = () => {
    if (onboardingStep === 1) {
      if (!$('#ob-name').value.trim()) return toast('Please enter your name');
      onboardingStep = 2;
    } else if (onboardingStep === 2) {
      onboardingStep = 3;
    } else if (onboardingStep === 3) {
      if (!selectedGoal) return toast('Pick a goal');
      onboardingStep = 4;
    } else {
      if (!selectedLevel) return toast('Pick your experience level');
      finishOnboarding();
      return;
    }
    updateOnboardingUI();
  };
  $('#ob-back').onclick = () => {
    if (onboardingStep > 1) {
      onboardingStep--;
      updateOnboardingUI();
    }
  };
  $$('.goal-btn[data-goal]').forEach(btn => {
    btn.onclick = () => {
      $$('.goal-btn[data-goal]').forEach(b => b.classList.remove('selected'));
      btn.classList.add('selected');
      selectedGoal = btn.dataset.goal;
    };
  });
  $$('.goal-btn[data-level]').forEach(btn => {
    btn.onclick = () => {
      $$('.goal-btn[data-level]').forEach(b => b.classList.remove('selected'));
      btn.classList.add('selected');
      selectedLevel = btn.dataset.level;
    };
  });

  // Nav
  $$('[data-view]').forEach(a => {
    a.addEventListener('click', e => {
      e.preventDefault();
      switchView(a.dataset.view);
    });
  });

  // Tabs
  $$('.tab').forEach(tab => {
    tab.onclick = () => {
      $$('.tab').forEach(t => t.classList.remove('active'));
      tab.classList.add('active');
      $$('.tab-panel').forEach(p => p.classList.remove('active'));
      $(`#tab-${tab.dataset.tab}`).classList.add('active');
    };
  });

  // Search / filter
  $('#exercise-search')?.addEventListener('input', renderExercises);
  $('#muscle-filter')?.addEventListener('change', renderExercises);

  // Log workout
  $('#log-form').onsubmit = e => {
    e.preventDefault();
    const name = $('#log-name').value.trim();
    const duration = +$('#log-duration').value;
    const raw = $('#log-exercises').value.trim();
    const notes = $('#log-notes').value.trim();
    const exercises = raw ? raw.split('\n').map(line => {
      const [n, s] = line.split('—').map(x => x.trim());
      return { name: n || line, sets: s || '' };
    }) : [];
    state.workouts.unshift({
      id: Date.now(),
      name,
      duration,
      exercises,
      notes,
      date: new Date().toISOString()
    });
    save();
    $('#log-form').reset();
    $('#log-duration').value = 45;
    renderAll();
    toast('Workout saved. Nice work.');
    switchView('dashboard');
  };

  // Generate plan
  $('#generate-plan').onclick = () => {
    const plan = PLANS[state.profile.goal] || PLANS.general;
    state.plans = [JSON.parse(JSON.stringify(plan))];
    save();
    renderPlans();
    renderDashboard();
    document.querySelector('[data-tab="plans"]').click();
    toast(`Generated: ${plan.name}`);
  };

  // Weight log
  $('#log-weight-btn').onclick = () => {
    openModal(`
      <h2 style="margin-bottom:1rem;font-family:var(--font-display)">Log Weight</h2>
      <label>Weight (kg)</label>
      <input type="number" id="modal-weight" step="0.1" value="${state.profile.weight}" style="width:100%;padding:0.75rem 1rem;background:var(--surface);border:1px solid var(--border);border-radius:10px;margin-bottom:1.25rem" />
      <button class="btn-primary full" id="save-weight">Save</button>
    `);
    $('#save-weight').onclick = () => {
      const w = parseFloat($('#modal-weight').value);
      if (!w || w < 30 || w > 250) return toast('Enter a valid weight');
      state.weights.push({ date: new Date().toISOString(), weight: w });
      state.profile.weight = w;
      save();
      closeModal();
      renderAll();
      toast('Weight logged');
    };
  };

  // Profile save
  $('#profile-form').onsubmit = e => {
    e.preventDefault();
    state.profile.name = $('#pf-name').value.trim() || state.profile.name;
    state.profile.weight = parseFloat($('#pf-weight').value) || state.profile.weight;
    state.profile.height = parseFloat($('#pf-height').value) || state.profile.height;
    state.profile.goal = $('#pf-goal').value;
    state.profile.level = $('#pf-level').value;
    // Also push weight entry if changed
    const last = state.weights[state.weights.length - 1];
    if (!last || last.weight !== state.profile.weight) {
      state.weights.push({ date: new Date().toISOString(), weight: state.profile.weight });
    }
    save();
    renderAll();
    toast('Profile updated');
  };

  // Chat
  $('#chat-form').onsubmit = e => {
    e.preventDefault();
    const input = $('#chat-input');
    const text = input.value.trim();
    if (!text) return;
    addChatMessage(text, true);
    input.value = '';
    setTimeout(() => {
      const reply = generateAIResponse(text);
      addChatMessage(reply, false);
    }, 400 + Math.random() * 400);
  };

  $$('.quick-btn').forEach(btn => {
    btn.onclick = () => {
      const prompt = btn.dataset.prompt;
      addChatMessage(prompt, true);
      setTimeout(() => {
        const reply = generateAIResponse(prompt);
        addChatMessage(reply, false);
      }, 500);
    };
  });

  // Theme
  $('#theme-toggle').onclick = () => {
    const html = document.documentElement;
    const next = html.getAttribute('data-theme') === 'light' ? null : 'light';
    if (next) html.setAttribute('data-theme', next);
    else html.removeAttribute('data-theme');
    $('#theme-toggle').innerHTML = next ? '<i class="fa-solid fa-sun"></i>' : '<i class="fa-solid fa-moon"></i>';
  };

  // Refresh tip
  $('#refresh-tip').onclick = () => {
    const tips = TIPS[state.profile.goal] || TIPS.general;
    $('#ai-tip').textContent = tips[Math.floor(Math.random() * tips.length)];
  };

  // Export / Reset
  $('#export-data').onclick = () => {
    const blob = new Blob([JSON.stringify(state, null, 2)], { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `aether-export-${new Date().toISOString().slice(0, 10)}.json`;
    a.click();
    URL.revokeObjectURL(url);
    toast('Exported');
  };
  $('#reset-data').onclick = () => {
    if (confirm('This will erase all your data. Are you sure?')) {
      localStorage.removeItem(STORAGE_KEY);
      location.reload();
    }
  };

  // Modal close
  $('#modal-close').onclick = closeModal;
  $('#modal').onclick = e => { if (e.target === $('#modal')) closeModal(); };
}

// ===== Init =====
function init() {
  load();
  bindEvents();
  if (!state.profile) {
    showOnboarding();
  } else {
    $('#app').classList.remove('hidden');
    renderAll();
  }
}

init();
</script>
</body>
</html>
