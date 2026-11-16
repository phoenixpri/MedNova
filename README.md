# MedNova
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<meta name="description" content="MEDNOVA brings biological rhythms, wearable signals and lab biomarkers into one calm, preventive health view." />
<meta name="theme-color" content="#060711" />
<title>MEDNOVA · Personal Health Intelligence</title>
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&family=Space+Grotesk:wght@500;600;700&display=swap" rel="stylesheet" />
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>
<style>
  :root {
    --bg: #060711;
    --sidebar: #090b19;
    --card: rgba(16, 19, 40, 0.78);
    --pink: #FF2A85;
    --pink-soft: rgba(255, 42, 133, 0.16);
    --yellow: #FFD60A;
    --yellow-soft: rgba(255, 214, 10, 0.13);
    --cyan: #00E5FF;
    --violet: #8B5CF6;
    --text: #F8FAFC;
    --muted: #94A3B8;
    --border: rgba(139, 92, 246, 0.28);
    --radius: 20px;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  html { scroll-behavior: smooth; }
  body {
    font-family: 'Inter', system-ui, sans-serif;
    background:
      radial-gradient(circle at 12% 12%, rgba(255, 42, 133, 0.14), transparent 40%),
      radial-gradient(circle at 90% 15%, rgba(255, 214, 10, 0.09), transparent 40%),
      radial-gradient(circle at 50% 95%, rgba(139, 92, 246, 0.18), transparent 50%),
      var(--bg);
    background-attachment: fixed;
    color: var(--text);
    min-height: 100vh;
    display: flex;
    -webkit-font-smoothing: antialiased;
    overflow-x: hidden;
  }
  h1, h2, h3, .display { font-family: 'Space Grotesk', sans-serif; letter-spacing: -0.02em; }
  button { font: inherit; color: inherit; }
  :focus-visible { outline: 2px solid var(--yellow); outline-offset: 2px; }
  .icon { width: 20px; height: 20px; flex: none; stroke: currentColor; fill: none; stroke-width: 1.8; stroke-linecap: round; stroke-linejoin: round; }

  /* Sidebar */
  .sidebar {
    width: 272px; position: fixed; inset: 0 auto 0 0; z-index: 30;
    background: var(--sidebar);
    border-right: 1px solid rgba(255, 42, 133, 0.22);
    padding: 24px 18px;
    display: flex; flex-direction: column; justify-content: space-between;
  }
  .brand { display: flex; align-items: center; gap: 12px; margin-bottom: 20px; }
  .brand-icon {
    width: 42px; height: 42px; border-radius: 12px; flex: none;
    background: linear-gradient(135deg, var(--pink), var(--yellow));
    display: grid; place-items: center; color: #0b0c1a;
    box-shadow: 0 0 22px rgba(255, 42, 133, 0.4);
  }
  .brand-title { font-weight: 700; font-size: 19px; }
  .brand-sub { font-size: 10px; letter-spacing: 0.14em; color: var(--yellow); font-weight: 600; }
  .demo-pill {
    background: var(--yellow-soft); border: 1px solid rgba(255, 214, 10, 0.3);
    color: var(--yellow); font-size: 11px; font-weight: 600;
    padding: 7px 12px; border-radius: 10px; margin-bottom: 22px; letter-spacing: 0.04em;
  }
  .nav-list { display: flex; flex-direction: column; gap: 6px; }
  .nav-btn {
    background: transparent; border: 1px solid transparent; color: var(--muted);
    padding: 12px 14px; border-radius: 12px; text-align: left;
    font-size: 14px; font-weight: 500; cursor: pointer;
    display: flex; align-items: center; gap: 12px; transition: all .25s ease;
  }
  .nav-btn:hover { color: #fff; background: rgba(255, 42, 133, 0.08); border-color: rgba(255, 42, 133, 0.25); }
  .nav-btn.active {
    background: linear-gradient(90deg, rgba(255, 42, 133, 0.22), rgba(139, 92, 246, 0.18));
    border-color: rgba(255, 42, 133, 0.5); color: #fff;
  }
  .focus-box {
    background: linear-gradient(145deg, rgba(45, 36, 14, 0.6), rgba(16, 19, 40, 0.9));
    border: 1px solid rgba(255, 214, 10, 0.3); border-radius: 14px; padding: 14px; margin-bottom: 14px;
  }
  .focus-box h4 { color: var(--yellow); font-size: 13px; margin-bottom: 6px; }
  .focus-box p { font-size: 12px; color: #E2E8F0; line-height: 1.5; margin-bottom: 10px; }
  .link-btn { background: none; border: none; color: var(--pink); font-size: 12px; font-weight: 600; cursor: pointer; padding: 0; }
  .link-btn:hover { text-decoration: underline; }
  .profile-mini {
    width: 100%; display: flex; align-items: center; gap: 12px; text-align: left;
    padding: 10px 12px; background: rgba(255, 42, 133, 0.1);
    border: 1px solid rgba(255, 42, 133, 0.3); border-radius: 12px; cursor: pointer;
  }
  .avatar {
    width: 36px; height: 36px; border-radius: 50%; flex: none;
    background: linear-gradient(135deg, var(--pink), var(--violet));
    display: grid; place-items: center; font-weight: 700; font-size: 13px;
  }

  /* Main */
  .main { margin-left: 272px; flex: 1; min-width: 0; padding: 24px 36px 48px; max-width: 1400px; }
  .topbar {
    display: flex; justify-content: space-between; align-items: center; gap: 12px; flex-wrap: wrap;
    background: rgba(13, 16, 33, 0.85); border: 1px solid rgba(255, 214, 10, 0.2);
    padding: 12px 22px; border-radius: 14px; margin-bottom: 28px; backdrop-filter: blur(10px);
  }
  .status { color: var(--cyan); font-weight: 700; font-size: 12px; letter-spacing: .04em; }
  .date { color: var(--muted); font-size: 12px; letter-spacing: .04em; }
  .row { display: flex; align-items: center; gap: 10px; flex-wrap: wrap; }
  .badge {
    padding: 4px 11px; border-radius: 999px; font-size: 11px; font-weight: 600;
    letter-spacing: 0.08em; text-transform: uppercase; display: inline-block;
  }
  .badge-pink { background: var(--pink-soft); color: #FF6EB0; border: 1px solid rgba(255, 42, 133, 0.5); }
  .badge-yellow { background: var(--yellow-soft); color: var(--yellow); border: 1px solid rgba(255, 214, 10, 0.45); }
  .badge-cyan { background: rgba(0, 229, 255, 0.13); color: var(--cyan); border: 1px solid rgba(0, 229, 255, 0.4); }

  .grid-2 { display: grid; grid-template-columns: 1.35fr 1fr; gap: 22px; margin-bottom: 22px; }
  .grid-equal { display: grid; grid-template-columns: 1fr 1fr; gap: 22px; margin-bottom: 22px; }
  .grid-4 { display: grid; grid-template-columns: repeat(4, 1fr); gap: 18px; margin-bottom: 22px; }
  .card {
    background: var(--card); border: 1px solid var(--border); border-radius: var(--radius);
    padding: 26px; backdrop-filter: blur(14px); box-shadow: 0 10px 30px rgba(0, 0, 0, .4);
    transition: border-color .3s ease;
  }
  .card:hover { border-color: rgba(255, 42, 133, 0.5); }
  .card-pink { background: linear-gradient(135deg, rgba(48, 15, 56, 0.85), rgba(14, 17, 36, 0.92)); border-color: rgba(255, 42, 133, 0.4); }
  .card-yellow { background: linear-gradient(135deg, rgba(44, 35, 14, 0.78), rgba(14, 17, 36, 0.92)); border-color: rgba(255, 214, 10, 0.4); }
  .eyebrow { font-size: 11px; color: var(--muted); letter-spacing: .08em; text-transform: uppercase; }
  .big { font-family: 'Space Grotesk', sans-serif; font-size: 30px; font-weight: 700; line-height: 1.15; }
  .big small { font-size: 13px; color: var(--muted); font-weight: 500; }

  .page-head { margin-bottom: 24px; }
  .page-head h2 { font-size: 32px; margin: 10px 0 6px; }
  .page-head p { color: var(--muted); max-width: 640px; line-height: 1.6; }

  .btn {
    padding: 11px 20px; border-radius: 12px; font-family: 'Space Grotesk', sans-serif;
    font-weight: 600; font-size: 14px; cursor: pointer; border: 1px solid transparent;
    transition: all .25s ease; display: inline-flex; align-items: center; gap: 8px;
  }
  .btn-primary { background: linear-gradient(90deg, var(--pink), var(--violet)); color: #fff; box-shadow: 0 4px 18px rgba(255, 42, 133, .35); }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 6px 24px rgba(255, 42, 133, .5); }
  .btn-secondary { background: var(--yellow-soft); color: var(--yellow); border-color: rgba(255, 214, 10, .4); }
  .btn-secondary:hover { background: rgba(255, 214, 10, .22); }

  .section { display: none; }
  .section.active { display: block; animation: fadeIn .35s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: none; } }

  .form-group { margin-bottom: 16px; }
  .form-group label { display: block; font-size: 11px; letter-spacing: .08em; color: var(--yellow); margin-bottom: 6px; text-transform: uppercase; font-weight: 600; }
  .form-control {
    width: 100%; background: rgba(6, 7, 17, .75); border: 1px solid rgba(139, 92, 246, .4);
    border-radius: 10px; padding: 11px 14px; color: #fff; font: inherit; font-size: 14px;
  }
  .form-control:focus { outline: none; border-color: var(--pink); box-shadow: 0 0 12px rgba(255, 42, 133, .25); }
  select.form-control option { background: #0d1021; }
  input[type="range"] { width: 100%; accent-color: var(--pink); cursor: pointer; }

  .tbl-wrap { overflow-x: auto; }
  table { width: 100%; border-collapse: collapse; margin-top: 14px; min-width: 460px; }
  th, td { padding: 12px 14px; text-align: left; border-bottom: 1px solid rgba(255, 255, 255, .08); font-size: 14px; }
  th { color: var(--yellow); font-size: 11px; letter-spacing: .08em; text-transform: uppercase; }

  .sleep-bar { display: flex; height: 38px; border-radius: 10px; overflow: hidden; margin-top: 16px; font-size: 12px; font-weight: 600; }
  .sleep-bar div { display: grid; place-items: center; white-space: nowrap; overflow: hidden; }
  .s-rem { width: 20.8%; background: var(--pink); }
  .s-deep { width: 23.5%; background: var(--yellow); color: #060711; }
  .s-light { width: 55.7%; background: var(--violet); }

  .dropzone { border: 2px dashed rgba(255, 42, 133, .45); border-radius: 16px; padding: 32px 20px; text-align: center; margin: 18px 0; background: rgba(255, 42, 133, .04); }
  .dropzone.drag { background: rgba(255, 42, 133, .12); }
  .note { font-size: 12px; color: var(--muted); line-height: 1.5; }

  .toast {
    position: fixed; right: 24px; bottom: 24px; z-index: 60;
    background: #101328; border: 1px solid var(--yellow); color: #fff;
    padding: 12px 18px; border-radius: 12px; font-size: 14px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, .5);
    opacity: 0; transform: translateY(10px); pointer-events: none; transition: all .3s ease;
  }
  .toast.show { opacity: 1; transform: none; }

  @media (max-width: 960px) {
    .sidebar { width: 78px; padding: 18px 10px; align-items: center; }
    .brand-text, .demo-pill, .focus-box, .profile-text, .nav-label { display: none; }
    .brand { margin-bottom: 24px; }
    .nav-btn { justify-content: center; padding: 12px; }
    .profile-mini { justify-content: center; padding: 8px; }
    .main { margin-left: 78px; padding: 20px 18px 40px; }
    .grid-2, .grid-equal { grid-template-columns: 1fr; }
    .grid-4 { grid-template-columns: 1fr 1fr; }
  }
  @media (max-width: 640px) {
    .sidebar {
      inset: auto 0 0 0; width: 100%; height: 64px; flex-direction: row; padding: 6px 10px;
      border-right: none; border-top: 1px solid rgba(255, 42, 133, .3); justify-content: center;
    }
    .sidebar > div:first-child { display: flex; width: 100%; }
    .sidebar > div:last-child, .brand { display: none; }
    .nav-list { flex-direction: row; width: 100%; justify-content: space-around; }
    .nav-btn { padding: 10px 12px; }
    .main { margin-left: 0; padding: 16px 14px 90px; }
    .page-head h2 { font-size: 26px; }
    .grid-4 { grid-template-columns: 1fr; }
    .card { padding: 20px; }
    .hero-title { font-size: 34px !important; }
    .toast { right: 14px; left: 14px; bottom: 78px; }
  }
  @media (prefers-reduced-motion: reduce) { * { animation: none !important; transition: none !important; } }
</style>
</head>
<body>

<!-- Icon sprite -->
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <symbol id="i-logo" viewBox="0 0 24 24"><path d="M12 3v18M7 6c0 3 10 3 10 6s-10 3-10 6M17 6c0 3-10 3-10 6s10 3 10 6"/></symbol>
  <symbol id="i-home" viewBox="0 0 24 24"><path d="M3 11l9-8 9 8M5 10v10h14V10"/></symbol>
  <symbol id="i-user" viewBox="0 0 24 24"><circle cx="12" cy="8" r="4"/><path d="M4 21c0-4 4-6 8-6s8 2 8 6"/></symbol>
  <symbol id="i-flask" viewBox="0 0 24 24"><path d="M9 3h6M10 3v6L4.5 19a1.5 1.5 0 001.3 2.2h12.4a1.5 1.5 0 001.3-2.2L14 9V3"/></symbol>
  <symbol id="i-clock" viewBox="0 0 24 24"><circle cx="12" cy="12" r="9"/><path d="M12 7v5l3 2"/></symbol>
  <symbol id="i-virus" viewBox="0 0 24 24"><circle cx="12" cy="12" r="5"/><path d="M12 2v3M12 19v3M2 12h3M19 12h3M5 5l2 2M17 17l2 2M19 5l-2 2M7 17l-2 2"/></symbol>
  <symbol id="i-watch" viewBox="0 0 24 24"><rect x="7" y="6" width="10" height="12" rx="3"/><path d="M9 6l1-3h4l1 3M9 18l1 3h4l1-3M12 10v2l1.5 1"/></symbol>
  <symbol id="i-file" viewBox="0 0 24 24"><path d="M14 3H7a2 2 0 00-2 2v14a2 2 0 002 2h10a2 2 0 002-2V8zM14 3v5h5M9 13h6M9 17h6"/></symbol>
  <symbol id="i-sync" viewBox="0 0 24 24"><path d="M20 11a8 8 0 00-14-4L4 9M4 4v5h5M4 13a8 8 0 0014 4l2-2M20 20v-5h-5"/></symbol>
</svg>

<aside class="sidebar">
  <div>
    <div class="brand">
      <div class="brand-icon"><svg class="icon" style="width:24px;height:24px"><use href="#i-logo"/></svg></div>
      <div class="brand-text">
        <div class="brand-title display">MEDNOVA</div>
        <div class="brand-sub">HEALTH INTELLIGENCE</div>
      </div>
    </div>
    <div class="demo-pill">● DEMO MODE · SAMPLE DATA</div>

    <nav class="nav-list" aria-label="Main navigation">
      <button class="nav-btn active" data-tab="overview"><svg class="icon"><use href="#i-home"/></svg><span class="nav-label">Overview</span></button>
      <button class="nav-btn" data-tab="profile"><svg class="icon"><use href="#i-user"/></svg><span class="nav-label">Health Profile</span></button>
      <button class="nav-btn" data-tab="labs"><svg class="icon"><use href="#i-flask"/></svg><span class="nav-label">Lab Analysis</span></button>
      <button class="nav-btn" data-tab="clock"><svg class="icon"><use href="#i-clock"/></svg><span class="nav-label">Biological Clock</span></button>
      <button class="nav-btn" data-tab="epidemic"><svg class="icon"><use href="#i-virus"/></svg><span class="nav-label">Epidemic Sim</span></button>
      <button class="nav-btn" data-tab="wearables"><svg class="icon"><use href="#i-watch"/></svg><span class="nav-label">Wearables</span></button>
    </nav>
  </div>

  <div>
    <div class="focus-box">
      <h4>One gentle focus</h4>
      <p>Protect your wind-down window tonight. Your recovery signal is trending up.</p>
      <button class="link-btn" data-tab="clock">Explore your rhythm →</button>
    </div>
    <button class="profile-mini" data-tab="profile" aria-label="Open health profile">
      <div class="avatar" id="sideAvatar">AM</div>
      <div class="profile-text">
        <div style="font-weight:600;font-size:13px" id="sideName">Alex Morgan</div>
        <div style="font-size:10px;color:#FF85B3;letter-spacing:.08em">PERSONAL PROFILE</div>
      </div>
    </button>
  </div>
</aside>

<main class="main">
  <div class="topbar">
    <div class="row" style="gap:14px">
      <span class="status">● ALL SYSTEMS STEADY</span>
      <span class="date" id="liveDate"></span>
    </div>
    <div class="row">
      <span class="badge badge-pink">AI Health Engine</span>
      <span class="badge badge-yellow" id="topBadge">O+ · 29 YRS</span>
    </div>
  </div>

  <!-- OVERVIEW -->
  <section id="overview" class="section active">
    <div class="grid-2">
      <div class="card card-pink">
        <div class="row" style="margin-bottom:18px">
          <span class="badge badge-yellow">Your health, in context</span>
        </div>
        <h1 class="hero-title" style="font-size:44px;line-height:1.12;margin-bottom:14px">
          <span id="greeting">Good morning</span>, <span style="color:var(--yellow)" id="heroName">Alex.</span>
        </h1>
        <p style="color:#CBD5E1;font-size:15px;line-height:1.7;max-width:520px;margin-bottom:26px">
          MEDNOVA brings your biological rhythms, wearable signals and clinical biomarkers into one calm view, shifting care from reactive treatment toward preventive clarity.
        </p>
        <div class="row" style="gap:12px">
          <button class="btn btn-primary" data-tab="profile">Complete profile →</button>
          <button class="btn btn-secondary" data-tab="labs">View latest insights</button>
        </div>
      </div>

      <div class="card">
        <div class="row" style="justify-content:space-between;margin-bottom:16px">
          <span class="eyebrow" style="color:var(--yellow);font-weight:700">Wellness index</span>
          <span style="color:var(--cyan);font-size:12px">● Within your baseline</span>
        </div>
        <div class="row" style="gap:24px;flex-wrap:nowrap">
          <div style="width:150px;height:150px;position:relative;flex:none">
            <canvas id="wellnessDonut" aria-label="Wellness score chart" role="img"></canvas>
            <div style="position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center">
              <span class="display" style="font-size:34px;font-weight:700" id="wellnessScoreText">84</span>
              <span style="font-size:11px;color:var(--yellow)">/ 100</span>
            </div>
          </div>
          <div style="flex:1">
            <div class="eyebrow">Sleep score</div>
            <div class="big" style="color:var(--yellow)" id="ovSleep">86 <small>/100</small></div>
            <div class="eyebrow" style="margin-top:14px">Recovery</div>
            <div class="big" style="color:var(--pink)" id="ovRecovery">79 <small>/100</small></div>
          </div>
        </div>
        <div style="margin-top:20px">
          <div class="row" style="justify-content:space-between;font-size:12px;margin-bottom:6px">
            <span style="color:var(--muted)">Profile completeness</span>
            <span style="color:var(--yellow);font-weight:600" id="compText">100%</span>
          </div>
          <div style="height:6px;background:rgba(255,255,255,.1);border-radius:99px;overflow:hidden">
            <div id="compBar" style="width:100%;height:100%;background:linear-gradient(90deg,var(--pink),var(--yellow));transition:width .4s"></div>
          </div>
        </div>
      </div>
    </div>

    <div class="grid-equal">
      <div class="card">
        <div class="row" style="justify-content:space-between;margin-bottom:10px">
          <div>
            <div class="eyebrow">7-day recovery</div>
            <div class="big" style="color:var(--yellow)">+12% <small style="color:var(--cyan)">improving</small></div>
          </div>
          <span class="badge badge-yellow">Weekly trend</span>
        </div>
        <div style="height:130px"><canvas id="recoverySparkline" aria-label="Seven day recovery trend" role="img"></canvas></div>
      </div>

      <div class="card card-yellow">
        <div class="row" style="justify-content:space-between;margin-bottom:14px">
          <span style="font-weight:700;color:var(--yellow);font-size:13px;letter-spacing:.08em">AI HEALTH LENS</span>
          <span class="badge badge-pink">Context synthesis</span>
        </div>
        <p style="font-size:15px;line-height:1.7;color:#F1F5F9;margin-bottom:18px" id="aiLensText">
          Your recovery is responding well to sleep consistency. Given your <b>seasonal rhinitis</b>, air filtration and protecting the hour before sleep are your highest-leverage preventive actions today.
        </p>
        <button class="btn btn-secondary" data-tab="clock">See circadian reasoning</button>
      </div>
    </div>
  </section>

  <!-- PROFILE -->
  <section id="profile" class="section">
    <div class="page-head">
      <span class="badge badge-pink">Digital profile</span>
      <h2>Your health context, made useful.</h2>
      <p>A living profile helps MEDNOVA connect biomarker patterns without losing the human story.</p>
    </div>
    <div class="grid-2">
      <div class="card card-pink">
        <div class="row" style="justify-content:space-between;margin-bottom:16px">
          <span class="badge badge-yellow" id="cardCompBadge">100% complete</span>
          <span class="display" style="font-size:24px;font-weight:700;color:var(--pink)" id="cardBlood">O+</span>
        </div>
        <h2 style="font-size:28px" id="cardName">Alex Morgan</h2>
        <p style="color:var(--yellow);font-size:14px;margin:4px 0 20px" id="cardMeta">29 years · they / them · O+ blood type</p>
        <div style="background:rgba(6,7,17,.65);border:1px solid rgba(255,42,133,.3);padding:14px;border-radius:12px;margin-bottom:12px">
          <div class="eyebrow" style="color:#FF85B3">Allergies</div>
          <div style="font-weight:600;margin-top:4px" id="cardAllergies">Penicillin</div>
        </div>
        <div style="background:rgba(6,7,17,.65);border:1px solid rgba(255,214,10,.3);padding:14px;border-radius:12px;margin-bottom:16px">
          <div class="eyebrow" style="color:var(--yellow)">Context flags</div>
          <div style="font-weight:600;margin-top:4px" id="cardConditions">Seasonal rhinitis</div>
        </div>
        <p class="note">Always review clinical decisions with a qualified healthcare professional.</p>
      </div>

      <form class="card" id="profileForm" autocomplete="off">
        <div class="grid-equal" style="margin-bottom:0">
          <div class="form-group"><label for="inName">Display name</label><input class="form-control" id="inName" value="Alex Morgan" /></div>
          <div class="form-group"><label for="inAge">Age</label><input type="number" min="0" max="120" class="form-control" id="inAge" value="29" /></div>
        </div>
        <div class="grid-equal" style="margin-bottom:0">
          <div class="form-group"><label for="inPronouns">Pronouns</label><input class="form-control" id="inPronouns" value="they / them" /></div>
          <div class="form-group">
            <label for="inBlood">Blood type</label>
            <select class="form-control" id="inBlood">
              <option>O+</option><option>O-</option><option>A+</option><option>A-</option>
              <option>B+</option><option>B-</option><option>AB+</option><option>AB-</option>
            </select>
          </div>
        </div>
        <div class="form-group"><label for="inAllergies">Allergies</label><input class="form-control" id="inAllergies" value="Penicillin" /></div>
        <div class="form-group"><label for="inConditions">Conditions / context flags</label><input class="form-control" id="inConditions" value="Seasonal rhinitis" /></div>
        <button type="submit" class="btn btn-primary">Save profile & update AI context</button>
      </form>
    </div>
  </section>

  <!-- LABS -->
  <section id="labs" class="section">
    <div class="page-head">
      <span class="badge badge-yellow">Lab analysis</span>
      <h2>Turn a report into a conversation.</h2>
      <p>Add a report to see lab values organised into plain-language questions for your clinician.</p>
    </div>
    <div class="grid-2">
      <div class="card">
        <span class="badge badge-pink">AI biomarker interpreter</span>
        <div class="dropzone" id="dropzone">
          <svg class="icon" style="width:38px;height:38px;color:var(--pink)"><use href="#i-file"/></svg>
          <h3 style="margin-top:10px">Drop a medical report here</h3>
          <p class="note" style="margin:6px 0 16px" id="fileHint">PDF, JPG or PNG · up to 10 MB</p>
          <input type="file" id="reportFile" accept=".pdf,.jpg,.jpeg,.png" hidden />
          <div class="row" style="justify-content:center">
            <button type="button" class="btn btn-secondary" id="chooseFile">Choose file</button>
            <button type="button" class="btn btn-primary" id="runLab">Run analysis</button>
          </div>
        </div>
        <p class="note" style="color:var(--yellow)">Educational interpretation only. No clinical diagnosis is made here.</p>
      </div>

      <div class="card card-pink">
        <div style="text-align:center;padding:44px 16px" id="labPlaceholder">
          <svg class="icon" style="width:38px;height:38px;color:var(--yellow)"><use href="#i-flask"/></svg>
          <div style="margin-top:12px"><span class="badge badge-pink">Signal map</span></div>
          <h3 style="margin-top:12px">Awaiting a report</h3>
          <p style="color:#CBD5E1;font-size:14px;margin-top:8px;line-height:1.6">Choose a file and select <b>Run analysis</b> to see a sample biomarker summary.</p>
        </div>
        <div id="labResults" hidden>
          <div class="row" style="justify-content:space-between">
            <span class="badge badge-yellow">Biomarker signal map · sample</span>
            <span style="color:var(--cyan);font-size:12px">4 markers</span>
          </div>
          <div class="tbl-wrap">
            <table>
              <thead><tr><th>Biomarker</th><th>Result</th><th>Reference</th><th>Signal</th></tr></thead>
              <tbody>
                <tr><td>Vitamin D (25-OH)</td><td><b>24 ng/mL</b></td><td>30 – 100</td><td><span class="badge badge-yellow">Slightly low</span></td></tr>
                <tr><td>hs-CRP</td><td><b>0.8 mg/L</b></td><td>&lt; 1.0</td><td><span class="badge badge-cyan">Optimal</span></td></tr>
                <tr><td>LDL cholesterol</td><td><b>118 mg/dL</b></td><td>&lt; 100</td><td><span class="badge badge-pink">Borderline</span></td></tr>
                <tr><td>HbA1c</td><td><b>5.2 %</b></td><td>4.0 – 5.6</td><td><span class="badge badge-cyan">Optimal</span></td></tr>
              </tbody>
            </table>
          </div>
          <div style="margin-top:18px;background:rgba(255,214,10,.1);border:1px solid rgba(255,214,10,.35);border-radius:12px;padding:16px">
            <div style="font-size:12px;font-weight:700;color:var(--yellow);margin-bottom:8px">Questions for your clinician</div>
            <ul style="font-size:13px;color:#E2E8F0;padding-left:18px;line-height:1.6">
              <li>With borderline LDL and low hs-CRP, should we try dietary changes before considering medication?</li>
              <li>What vitamin D target and approach do you recommend given my current level?</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- CLOCK -->
  <section id="clock" class="section">
    <div class="page-head">
      <span class="badge badge-pink">Biological clock</span>
      <h2>Work with your natural tempo.</h2>
      <p>Your circadian rhythm is a hormonal wave, not a performance score. Scrub through the day to align light and rest.</p>
    </div>
    <div class="grid-2">
      <div class="card">
        <div class="row" style="justify-content:space-between;margin-bottom:14px">
          <span class="eyebrow" style="color:var(--yellow);font-weight:700">24-hour hormone wave</span>
          <span class="badge badge-cyan" id="clockBadge">08:00 · selected</span>
        </div>
        <div style="height:250px"><canvas id="circadianChart" aria-label="Cortisol and melatonin over 24 hours" role="img"></canvas></div>
        <div style="margin-top:18px">
          <label for="hourSlider" style="font-size:12px;color:var(--muted);display:block;margin-bottom:6px">Hour of day: <b style="color:var(--yellow)" id="hourLabel">08:00</b></label>
          <input type="range" min="0" max="23" value="8" id="hourSlider" />
        </div>
      </div>
      <div class="card card-yellow">
        <span class="badge badge-pink" id="phaseTimeTag">At 08:00</span>
        <h2 style="font-size:30px;color:var(--yellow);margin:14px 0" id="phaseTitle">Cortisol awakening peak</h2>
        <div class="row" style="margin-bottom:18px">
          <span class="badge badge-yellow" id="cortisolState">Cortisol: rising</span>
          <span class="badge badge-pink" id="melatoninState">Melatonin: low</span>
        </div>
        <p style="font-size:15px;line-height:1.7" id="phaseCue"></p>
      </div>
    </div>
  </section>

  <!-- EPIDEMIC -->
  <section id="epidemic" class="section">
    <div class="page-head">
      <span class="badge badge-yellow">Epidemic simulation</span>
      <h2>See how small changes shift the curve.</h2>
      <p>A transparent Susceptible–Infected–Recovered (SIR) model showing how transmission, immunity and contact density influence spread. Illustrative only, not a forecast.</p>
    </div>
    <div class="grid-2">
      <div class="card card-pink">
        <span class="badge badge-yellow" style="margin-bottom:16px">Model controls</span>
        <div class="form-group">
          <label for="r0Slider">Transmission rate (R₀): <span style="color:#fff" id="r0Val">1.8</span></label>
          <input type="range" min="0.8" max="4.5" step="0.1" value="1.8" id="r0Slider" />
        </div>
        <div class="form-group">
          <label for="immSlider">Community immunity: <span style="color:#fff" id="immVal">24%</span></label>
          <input type="range" min="0" max="90" step="1" value="24" id="immSlider" />
        </div>
        <div class="form-group">
          <label for="denSlider">Contact density: <span style="color:#fff" id="denVal">58%</span></label>
          <input type="range" min="10" max="100" step="2" value="58" id="denSlider" />
        </div>
        <button class="btn btn-primary" id="recalc">Recalculate trajectory</button>
      </div>
      <div class="card">
        <div class="row" style="justify-content:space-between;margin-bottom:12px">
          <div>
            <div class="eyebrow">Peak infected</div>
            <div class="big" style="color:var(--pink)" id="peakStat">–</div>
          </div>
          <span class="badge badge-cyan">30-day projection</span>
        </div>
        <div style="height:250px"><canvas id="sirChart" aria-label="SIR epidemic curve" role="img"></canvas></div>
      </div>
    </div>
  </section>

  <!-- WEARABLES -->
  <section id="wearables" class="section">
    <div class="page-head">
      <span class="badge badge-pink">Wearable telemetry</span>
      <h2>Your body, in small signals.</h2>
      <p>Connect the dots between autonomic recovery, sleep architecture and resting cardiovascular load.</p>
    </div>
    <div class="card card-yellow row" style="justify-content:space-between;margin-bottom:22px;padding:22px 26px">
      <div>
        <span class="badge badge-cyan">Demo device</span>
        <h3 style="font-size:22px;margin-top:10px">Smart ring</h3>
        <p style="font-size:12px;color:var(--yellow);margin-top:2px" id="syncTimestamp">Simulated live stream</p>
      </div>
      <button class="btn btn-primary" id="syncBtn"><svg class="icon" style="width:18px;height:18px"><use href="#i-sync"/></svg>Simulate sync</button>
    </div>

    <div class="grid-4">
      <div class="card"><div class="eyebrow">HRV balance</div><div class="big" style="color:var(--pink);margin:8px 0" id="wHrv">58 <small>ms</small></div><div style="font-size:12px;color:var(--cyan)">● Stable</div></div>
      <div class="card"><div class="eyebrow">Resting HR</div><div class="big" style="color:var(--yellow);margin:8px 0" id="wRhr">62 <small>bpm</small></div><div style="font-size:12px;color:var(--yellow)">● Baseline</div></div>
      <div class="card"><div class="eyebrow">Sleep score</div><div class="big" style="color:var(--cyan);margin:8px 0" id="wSleep">86 <small>/100</small></div><div style="font-size:12px;color:var(--cyan)">● 7h 22m total</div></div>
      <div class="card"><div class="eyebrow">SpO₂</div><div class="big" style="color:var(--pink);margin:8px 0" id="wSpo2">98.2 <small>%</small></div><div style="font-size:12px;color:#FF85B3">● Normal overnight</div></div>
    </div>

    <div class="card">
      <div class="row" style="justify-content:space-between">
        <h3>Sleep architecture · 7h 22m</h3>
        <span class="badge badge-yellow">REM · Deep · Light</span>
      </div>
      <div class="sleep-bar" role="img" aria-label="REM 1h 32m, Deep 1h 44m, Light 4h 06m">
        <div class="s-rem">REM 1h 32m</div>
        <div class="s-deep">Deep 1h 44m</div>
        <div class="s-light">Light 4h 06m</div>
      </div>
    </div>
  </section>
</main>

<div class="toast" id="toast" role="status" aria-live="polite"></div>

<script>
  const $ = id => document.getElementById(id);
  const hasChart = typeof Chart !== 'undefined';
  if (hasChart) {
    Chart.defaults.font.family = "'Inter', sans-serif";
    Chart.defaults.color = '#94A3B8';
  }

  // Date & greeting
  const now = new Date();
  $('liveDate').textContent = now.toLocaleDateString('en-GB', { weekday: 'long', day: '2-digit', month: 'short', year: 'numeric' }).toUpperCase();
  const hr = now.getHours();
  $('greeting').textContent = hr < 12 ? 'Good morning' : hr < 18 ? 'Good afternoon' : 'Good evening';

  // Toast
  let toastTimer;
  function toast(msg) {
    const t = $('toast'); t.textContent = msg; t.classList.add('show');
    clearTimeout(toastTimer); toastTimer = setTimeout(() => t.classList.remove('show'), 2800);
  }

  // Navigation
  function switchTab(id) {
    document.querySelectorAll('.section').forEach(s => s.classList.toggle('active', s.id === id));
    document.querySelectorAll('.nav-btn').forEach(b => {
      const on = b.dataset.tab === id;
      b.classList.toggle('active', on);
      on ? b.setAttribute('aria-current', 'page') : b.removeAttribute('aria-current');
    });
    window.scrollTo({ top: 0, behavior: 'smooth' });
    if (hasChart) setTimeout(() => Object.values(Chart.instances).forEach(c => c.resize()), 50);
  }
  document.querySelectorAll('[data-tab]').forEach(el => el.addEventListener('click', () => switchTab(el.dataset.tab)));

  // Charts: overview
  let wellnessChart;
  if (hasChart) {
    wellnessChart = new Chart($('wellnessDonut'), {
      type: 'doughnut',
      data: { datasets: [{ data: [84, 16], backgroundColor: ['#FF2A85', 'rgba(255,255,255,0.08)'], borderWidth: 0, borderRadius: 10 }] },
      options: { cutout: '78%', plugins: { legend: { display: false }, tooltip: { enabled: false } } }
    });
    new Chart($('recoverySparkline'), {
      type: 'line',
      data: {
        labels: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
        datasets: [{ data: [68, 71, 70, 74, 76, 77, 79], borderColor: '#FFD60A', backgroundColor: 'rgba(255,214,10,0.14)', borderWidth: 3, pointBackgroundColor: '#FF2A85', pointRadius: 4, fill: true, tension: 0.4 }]
      },
      options: {
        responsive: true, maintainAspectRatio: false,
        plugins: { legend: { display: false } },
        scales: { x: { grid: { display: false } }, y: { display: false, min: 60, max: 90 } }
      }
    });
  }

  // Profile
  const KEY = 'mednova-profile';
  function applyProfile(p) {
    const initials = p.name.split(/\s+/).filter(Boolean).map(n => n[0]).join('').slice(0, 2).toUpperCase() || 'AM';
    $('sideAvatar').textContent = initials;
    $('sideName').textContent = p.name;
    $('heroName').textContent = (p.name.split(/\s+/)[0] || 'there') + '.';
    $('topBadge').textContent = `${p.blood} · ${p.age} YRS`;
    $('cardName').textContent = p.name;
    $('cardBlood').textContent = p.blood;
    $('cardMeta').textContent = `${p.age} years · ${p.pronouns} · ${p.blood} blood type`;
    $('cardAllergies').textContent = p.allergies;
    $('cardConditions').textContent = p.conditions;

    const fields = [p.name, p.age, p.pronouns, p.blood, p.allergies, p.conditions];
    const filled = fields.filter(v => String(v).trim() && !/^none$/i.test(String(v).trim())).length;
    const pct = Math.round(filled / fields.length * 100);
    $('compText').textContent = pct + '%';
    $('compBar').style.width = pct + '%';
    $('cardCompBadge').textContent = pct + '% complete';

    const lens = $('aiLensText');
    lens.textContent = '';
    const parts = ['Your recovery is responding well to sleep consistency. Given your ', null, ', protecting the hour before sleep and tracking environmental triggers are your highest-leverage preventive actions today.'];
    lens.append(parts[0]);
    const b = document.createElement('b'); b.textContent = p.conditions.toLowerCase(); lens.append(b);
    lens.append(parts[2]);
  }
  function readProfile() {
    return {
      name: $('inName').value.trim() || 'Alex Morgan',
      age: $('inAge').value || '29',
      pronouns: $('inPronouns').value.trim() || 'they / them',
      blood: $('inBlood').value,
      allergies: $('inAllergies').value.trim() || 'None',
      conditions: $('inConditions').value.trim() || 'Baseline'
    };
  }
  $('profileForm').addEventListener('submit', e => {
    e.preventDefault();
    const p = readProfile();
    applyProfile(p);
    try { localStorage.setItem(KEY, JSON.stringify(p)); } catch (_) {}
    toast('Profile saved. AI Health Lens updated.');
  });
  try {
    const saved = JSON.parse(localStorage.getItem(KEY) || 'null');
    if (saved) {
      $('inName').value = saved.name; $('inAge').value = saved.age; $('inPronouns').value = saved.pronouns;
      $('inBlood').value = saved.blood; $('inAllergies').value = saved.allergies; $('inConditions').value = saved.conditions;
    }
  } catch (_) {}
  applyProfile(readProfile());

  // Labs
  const fileInput = $('reportFile'), dz = $('dropzone');
  function showFile(f) { if (f) $('fileHint').textContent = f.name; }
  $('chooseFile').addEventListener('click', () => fileInput.click());
  fileInput.addEventListener('change', () => showFile(fileInput.files[0]));
  $('runLab').addEventListener('click', () => {
    $('labPlaceholder').hidden = true;
    $('labPlaceholder').style.display = 'none';
    $('labResults').hidden = false;
    toast('Sample analysis ready.');
  });
  ['dragenter', 'dragover'].forEach(ev => dz.addEventListener(ev, e => { e.preventDefault(); dz.classList.add('drag'); }));
  ['dragleave', 'drop'].forEach(ev => dz.addEventListener(ev, e => { e.preventDefault(); dz.classList.remove('drag'); }));
  dz.addEventListener('drop', e => showFile(e.dataTransfer.files[0]));

  // Circadian clock
  const hours = Array.from({ length: 24 }, (_, i) => `${String(i).padStart(2, '0')}:00`);
  const circ = (h, c) => { const d = Math.abs(h - c); return Math.min(d, 24 - d); };
  const cortisol = hours.map((_, h) => 20 + 80 * Math.exp(-Math.pow(circ(h, 8), 2) / 14));
  const melatonin = hours.map((_, h) => 8 + 92 * Math.exp(-Math.pow(circ(h, 2.5), 2) / 12));
  let clockChart;
  const marker = {
    id: 'marker',
    afterDatasetsDraw(chart) {
      const { ctx, chartArea, scales } = chart;
      const x = scales.x.getPixelForValue(+$('hourSlider').value);
      ctx.save(); ctx.strokeStyle = 'rgba(255,255,255,.55)'; ctx.setLineDash([4, 4]);
      ctx.beginPath(); ctx.moveTo(x, chartArea.top); ctx.lineTo(x, chartArea.bottom); ctx.stroke(); ctx.restore();
    }
  };
  if (hasChart) {
    clockChart = new Chart($('circadianChart'), {
      type: 'line',
      data: { labels: hours, datasets: [
        { label: 'Cortisol', data: cortisol, borderColor: '#FFD60A', borderWidth: 3, tension: 0.4, pointRadius: 0 },
        { label: 'Melatonin', data: melatonin, borderColor: '#FF2A85', borderWidth: 3, tension: 0.4, pointRadius: 0 }
      ] },
      options: {
        responsive: true, maintainAspectRatio: false,
        plugins: { legend: { labels: { color: '#E2E8F0', usePointStyle: true } } },
        scales: {
          x: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { maxTicksLimit: 8 } },
          y: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { display: false }, title: { display: true, text: 'Relative level' } }
        }
      },
      plugins: [marker]
    });
  }
  const phases = [
    { test: h => h >= 6 && h < 10, title: 'Cortisol awakening peak', c: 'Cortisol: rising', m: 'Melatonin: low', cue: 'Get ten minutes of outdoor daylight and some light movement to anchor your body clock.' },
    { test: h => h >= 10 && h < 16, title: 'Focus & activity window', c: 'Cortisol: steady', m: 'Melatonin: minimal', cue: 'Alertness and body temperature run high. A good window for deep work and training.' },
    { test: h => h >= 16 && h < 21, title: 'Wind-down begins', c: 'Cortisol: tapering', m: 'Melatonin: rising', cue: 'Dim bright overhead lights and finish heavy meals early to support overnight recovery.' },
    { test: () => true, title: 'Deep overnight repair', c: 'Cortisol: minimal', m: 'Melatonin: peak', cue: 'Keep your room cool and dark while tissue repair and memory consolidation peak.' }
  ];
  function updateClock() {
    const h = +$('hourSlider').value, f = `${String(h).padStart(2, '0')}:00`;
    const p = phases.find(x => x.test(h));
    $('hourLabel').textContent = f;
    $('clockBadge').textContent = `${f} · selected`;
    $('phaseTimeTag').textContent = `At ${f}`;
    $('phaseTitle').textContent = p.title;
    $('cortisolState').textContent = p.c;
    $('melatoninState').textContent = p.m;
    $('phaseCue').innerHTML = '<b>Gentle cue:</b> ' + p.cue;
    if (clockChart) clockChart.update('none');
  }
  $('hourSlider').addEventListener('input', updateClock);
  updateClock();

  // SIR model
  let sirChart;
  if (hasChart) {
    sirChart = new Chart($('sirChart'), {
      type: 'line',
      data: { labels: [], datasets: [
        { label: 'Infected', data: [], borderColor: '#FF2A85', backgroundColor: 'rgba(255,42,133,0.16)', fill: true, borderWidth: 3, pointRadius: 0, tension: 0.3 },
        { label: 'Recovered', data: [], borderColor: '#FFD60A', borderWidth: 2.5, pointRadius: 0, tension: 0.3 },
        { label: 'Susceptible', data: [], borderColor: '#00E5FF', borderDash: [5, 5], borderWidth: 2, pointRadius: 0, tension: 0.3 }
      ] },
      options: {
        responsive: true, maintainAspectRatio: false,
        plugins: { legend: { labels: { color: '#E2E8F0', usePointStyle: true } } },
        scales: {
          x: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { maxTicksLimit: 8 } },
          y: { min: 0, max: 100, grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { callback: v => v + '%' } }
        }
      }
    });
  }
  function runSIR() {
    const r0 = +$('r0Slider').value, imm = +$('immSlider').value, den = +$('denSlider').value;
    $('r0Val').textContent = r0.toFixed(1);
    $('immVal').textContent = imm + '%';
    $('denVal').textContent = den + '%';

    let R = imm, I = 1, S = Math.max(0, 100 - I - R);
    const gamma = 0.14, beta = r0 * gamma * (0.5 + den / 100);
    const labels = [], s = [], i = [], r = [];
    let peak = 0, peakDay = 0;
    for (let d = 0; d <= 30; d++) {
      labels.push('Day ' + d);
      s.push(+S.toFixed(1)); i.push(+I.toFixed(1)); r.push(+R.toFixed(1));
      if (I > peak) { peak = I; peakDay = d; }
      const ni = beta * S * I / 100, nr = gamma * I;
      S = Math.max(0, S - ni); I = Math.max(0, I + ni - nr); R = Math.min(100, R + nr);
    }
    $('peakStat').innerHTML = `${peak.toFixed(1)}% <small style="color:var(--yellow)">day ${peakDay}</small>`;
    if (sirChart) {
      sirChart.data.labels = labels;
      sirChart.data.datasets[0].data = i;
      sirChart.data.datasets[1].data = r;
      sirChart.data.datasets[2].data = s;
      sirChart.update();
    }
  }
  ['r0Slider', 'immSlider', 'denSlider'].forEach(id => $(id).addEventListener('input', runSIR));
  $('recalc').addEventListener('click', runSIR);
  runSIR();

  // Wearable sync
  const rnd = (a, b) => Math.floor(Math.random() * (b - a + 1)) + a;
  $('syncBtn').addEventListener('click', () => {
    const hrv = rnd(52, 74), rhr = rnd(56, 65), sleep = rnd(80, 94), rec = rnd(76, 91);
    const spo2 = (97.6 + Math.random() * 1.8).toFixed(1), well = Math.round((sleep + rec) / 2);
    $('wHrv').innerHTML = `${hrv} <small>ms</small>`;
    $('wRhr').innerHTML = `${rhr} <small>bpm</small>`;
    $('wSleep').innerHTML = `${sleep} <small>/100</small>`;
    $('wSpo2').innerHTML = `${spo2} <small>%</small>`;
    $('ovSleep').innerHTML = `${sleep} <small>/100</small>`;
    $('ovRecovery').innerHTML = `${rec} <small>/100</small>`;
    $('wellnessScoreText').textContent = well;
    if (wellnessChart) { wellnessChart.data.datasets[0].data = [well, 100 - well]; wellnessChart.update(); }
    $('syncTimestamp').textContent = `Today, ${new Date().toTimeString().slice(0, 5)} · Simulated sync complete`;
    toast('Sample data refreshed.');
  });
</script>
</body>
</html>
