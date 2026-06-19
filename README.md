<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>slippy-spider | HQ</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet"/>
<style>
  :root {
    --green: #00ff41;
    --dim: #00aa2a;
    --red: #ff003c;
    --blue: #00cfff;
    --purple: #b800ff;
    --bg: #030a03;
    --card: #060f06;
    --border: #00ff4133;
  }

  *{margin:0;padding:0;box-sizing:border-box;}

  body {
    background: var(--bg);
    color: var(--green);
    font-family: 'Share Tech Mono', monospace;
    overflow-x: hidden;
    cursor: crosshair;
  }

  /* ── MATRIX RAIN ── */
  #matrix {
    position: fixed; top:0; left:0;
    width:100%; height:100%;
    z-index:0; opacity:.13;
    pointer-events:none;
  }

  /* ── SCANLINES ── */
  body::after {
    content:'';
    position:fixed; top:0; left:0;
    width:100%; height:100%;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,.15) 2px,
      rgba(0,0,0,.15) 4px
    );
    pointer-events:none;
    z-index:9999;
    animation: scanmove 8s linear infinite;
  }
  @keyframes scanmove {
    0%{background-position:0 0}
    100%{background-position:0 100vh}
  }

  /* ── CONTENT WRAPPER ── */
  .wrap { position:relative; z-index:10; max-width:1100px; margin:0 auto; padding:20px; }

  /* ── BOOT SEQUENCE ── */
  #boot {
    position:fixed; inset:0;
    background:#000;
    z-index:99999;
    display:flex; flex-direction:column;
    justify-content:center; align-items:flex-start;
    padding:40px; font-size:14px;
    color: var(--green);
  }
  #boot.hidden { display:none; }
  .boot-line { opacity:0; margin:3px 0; }
  .boot-line.show { animation: fadein .1s forwards; }
  @keyframes fadein{ to{ opacity:1; } }

  /* ── GLITCH HERO ── */
  .hero {
    text-align:center;
    padding: 60px 20px 40px;
    perspective: 800px;
  }
  .hero-name {
    font-family:'Orbitron',monospace;
    font-size: clamp(2.5rem, 8vw, 5.5rem);
    font-weight:900;
    letter-spacing:.1em;
    color: var(--green);
    text-shadow:
      0 0 10px var(--green),
      0 0 30px var(--green),
      0 0 60px var(--green);
    animation: glitch 3s infinite;
    transform-style: preserve-3d;
  }
  @keyframes glitch {
    0%,90%,100%{ text-shadow: 0 0 10px var(--green),0 0 30px var(--green),0 0 60px var(--green); transform:skewX(0deg); }
    91%{ text-shadow: -4px 0 var(--red), 4px 0 var(--blue); transform:skewX(-3deg); }
    93%{ text-shadow: 4px 0 var(--red), -4px 0 var(--blue); transform:skewX(3deg); }
    95%{ text-shadow: 0 0 10px var(--green),0 0 30px var(--green); transform:skewX(0); }
    97%{ text-shadow: -2px 0 var(--purple), 2px 0 var(--red); transform:skewX(-1deg); }
  }

  .hero-sub {
    font-size:1rem;
    color: var(--dim);
    margin-top:12px;
    letter-spacing:.3em;
    text-transform:uppercase;
  }

  #typewriter {
    font-size:1.1rem;
    color: var(--green);
    margin-top:18px;
    min-height:1.5em;
  }
  #typewriter::after { content:'█'; animation: blink .7s step-end infinite; }
  @keyframes blink{ 50%{ opacity:0; } }

  /* ── SPIDER HEX AVATAR ── */
  .avatar-wrap {
    display:flex; justify-content:center; margin:30px 0 10px;
  }
  .hex {
    width:140px; height:160px;
    background: var(--bg);
    clip-path: polygon(50% 0%,100% 25%,100% 75%,50% 100%,0% 75%,0% 25%);
    border: none;
    display:flex; align-items:center; justify-content:center;
    font-size:5rem;
    position:relative;
    box-shadow: 0 0 0 3px var(--green), 0 0 30px var(--green), 0 0 60px #00ff4144;
    animation: hexglow 2s ease-in-out infinite alternate;
  }
  @keyframes hexglow{
    from{ box-shadow:0 0 0 3px var(--green),0 0 20px var(--green),0 0 40px #00ff4144; }
    to{   box-shadow:0 0 0 3px var(--green),0 0 40px var(--green),0 0 80px #00ff4177; }
  }

  /* ── STATUS BAR ── */
  .status-bar {
    display:flex; justify-content:center; gap:20px; flex-wrap:wrap;
    margin:20px 0;
  }
  .status-pill {
    padding:6px 16px;
    border:1px solid var(--green);
    font-size:.75rem;
    letter-spacing:.2em;
    color: var(--green);
    background: #00ff410a;
    box-shadow: 0 0 8px var(--green);
    animation: pillpulse 2s ease-in-out infinite alternate;
  }
  @keyframes pillpulse{
    from{ box-shadow:0 0 4px var(--green); }
    to{   box-shadow:0 0 16px var(--green); }
  }
  .status-pill.red{ border-color:var(--red); color:var(--red); box-shadow:0 0 8px var(--red); }
  .status-pill.blue{ border-color:var(--blue); color:var(--blue); box-shadow:0 0 8px var(--blue); }

  /* ── GRID ── */
  .grid { display:grid; gap:18px; margin:30px 0; }
  .grid-2{ grid-template-columns:repeat(auto-fit,minmax(300px,1fr)); }
  .grid-3{ grid-template-columns:repeat(auto-fit,minmax(200px,1fr)); }

  /* ── CARD ── */
  .card {
    background: var(--card);
    border:1px solid var(--border);
    padding:22px;
    position:relative;
    transition: transform .2s, box-shadow .2s;
  }
  .card::before {
    content:'';
    position:absolute; top:0; left:0;
    width:4px; height:100%;
    background: var(--green);
    box-shadow: 0 0 10px var(--green);
  }
  .card:hover {
    transform: translateY(-4px) rotateX(2deg);
    box-shadow: 0 12px 30px #00ff4122, 0 0 0 1px var(--green);
  }
  .card-title {
    font-family:'Orbitron',monospace;
    font-size:.75rem;
    color: var(--dim);
    letter-spacing:.3em;
    margin-bottom:14px;
  }

  /* ── WHOAMI CARD ── */
  .info-row { display:flex; gap:10px; margin:5px 0; font-size:.9rem; }
  .info-key { color:var(--dim); min-width:90px; }
  .info-val { color:#fff; }
  .info-val.green{ color:var(--green); }

  /* ── SKILL BARS ── */
  .skill-row{ margin:8px 0; }
  .skill-label{ display:flex; justify-content:space-between; font-size:.8rem; margin-bottom:4px; }
  .skill-track{ height:8px; background:#111; border:1px solid #00ff4122; }
  .skill-fill{
    height:100%;
    background: linear-gradient(90deg, #003300, var(--green));
    box-shadow: 0 0 8px var(--green);
    width:0;
    transition: width 1.5s cubic-bezier(.4,0,.2,1);
  }

  /* ── STAT BOXES ── */
  .stat-box {
    background: var(--card);
    border:1px solid var(--border);
    padding:20px;
    text-align:center;
    position:relative;
    overflow:hidden;
    transition: transform .2s;
  }
  .stat-box:hover{ transform:scale(1.04); }
  .stat-num {
    font-family:'Orbitron',monospace;
    font-size:2.2rem;
    font-weight:900;
    color:var(--green);
    text-shadow:0 0 20px var(--green);
  }
  .stat-label{ font-size:.7rem; color:var(--dim); letter-spacing:.2em; margin-top:4px; }
  .stat-box::after{
    content:'';
    position:absolute; bottom:0; left:0;
    width:100%; height:2px;
    background: linear-gradient(90deg, transparent, var(--green), transparent);
    animation: scanH 3s linear infinite;
  }
  @keyframes scanH{ 0%{transform:scaleX(0);opacity:0} 50%{transform:scaleX(1);opacity:1} 100%{transform:scaleX(0);opacity:0} }

  /* ── PROJECT CARDS ── */
  .proj-card {
    background:var(--card);
    border:1px solid var(--border);
    padding:18px;
    transition: transform .2s, box-shadow .2s;
    position:relative;
    overflow:hidden;
  }
  .proj-card::before{
    content:'';
    position:absolute; top:0; left:0; right:0;
    height:2px;
    background: linear-gradient(90deg, var(--green), var(--blue), var(--purple));
    box-shadow: 0 0 10px var(--green);
  }
  .proj-card:hover{
    transform:translateY(-6px) rotateY(2deg);
    box-shadow:0 16px 40px #00ff4133;
  }
  .proj-name{
    font-family:'Orbitron',monospace;
    font-size:.9rem;
    color:var(--green);
    margin-bottom:6px;
  }
  .proj-desc{ font-size:.8rem; color:#aaa; margin-bottom:10px; }
  .proj-tag{
    display:inline-block;
    padding:2px 8px;
    border:1px solid var(--blue);
    color:var(--blue);
    font-size:.65rem;
    margin:2px;
    letter-spacing:.1em;
  }
  .status-live{ color:var(--green); font-size:.7rem; }
  .status-build{ color:var(--red); font-size:.7rem; animation:blink .8s step-end infinite; }

  /* ── TERMINAL ── */
  .terminal {
    background:#000;
    border:1px solid var(--green);
    padding:20px;
    box-shadow: 0 0 20px #00ff4122, inset 0 0 20px #00ff4105;
  }
  .term-bar{
    display:flex; gap:8px; margin-bottom:14px;
    border-bottom:1px solid #00ff4122; padding-bottom:10px;
  }
  .dot{ width:12px;height:12px;border-radius:50%; }
  .dot.r{background:var(--red);}
  .dot.y{background:#ffcc00;}
  .dot.g{background:var(--green);}
  .term-title{ font-size:.75rem; color:var(--dim); margin-left:auto; letter-spacing:.2em; }
  .term-line{ font-size:.85rem; margin:4px 0; color:#ccc; }
  .term-line .prompt{ color:var(--green); }
  .term-line .cmd{ color:#fff; }
  .term-line .ok{ color:var(--green); }
  .term-line .err{ color:var(--red); }
  .term-line .info{ color:var(--blue); }

  /* ── GAMING SECTION ── */
  .game-card {
    background:var(--card);
    border:1px solid #b800ff33;
    padding:18px;
    text-align:center;
    transition:transform .2s;
  }
  .game-card::before{
    content:'';
    position:absolute;top:0;left:0;right:0;
    height:2px;
    background: linear-gradient(90deg, var(--purple), var(--red));
  }
  .game-card{ position:relative; overflow:hidden; }
  .game-card:hover{ transform:translateY(-4px); box-shadow:0 10px 30px #b800ff33; }
  .game-icon{ font-size:2.5rem; margin-bottom:8px; }
  .game-name{ font-family:'Orbitron',monospace; font-size:.8rem; color:#b800ff; letter-spacing:.1em; }
  .game-rank{ font-size:.75rem; color:var(--red); margin-top:4px; }

  /* ── SECTION HEADER ── */
  .sec-head {
    font-family:'Orbitron',monospace;
    font-size:.8rem;
    letter-spacing:.4em;
    color:var(--dim);
    margin:40px 0 16px;
    display:flex; align-items:center; gap:12px;
  }
  .sec-head::before, .sec-head::after{
    content:'';flex:1;
    height:1px;
    background: linear-gradient(90deg, transparent, var(--green));
  }
  .sec-head::after{ background: linear-gradient(90deg, var(--green), transparent); }

  /* ── FOOTER ── */
  footer {
    text-align:center;
    padding:40px 20px;
    border-top:1px solid var(--border);
    font-size:.8rem;
    color:var(--dim);
    letter-spacing:.2em;
    margin-top:40px;
  }

  /* ── CORNER DECO ── */
  .corner-tl, .corner-br {
    position:fixed; width:60px;height:60px;
    border-color:var(--green);
    border-style:solid;
    z-index:100;
    opacity:.4;
  }
  .corner-tl{ top:10px;left:10px; border-width:2px 0 0 2px; }
  .corner-br{ bottom:10px;right:10px; border-width:0 2px 2px 0; }
</style>
</head>
<body>

<!-- BOOT SCREEN -->
<div id="boot">
  <div class="boot-line">> BIOS v2.0.77 — SPIDER-SYS</div>
  <div class="boot-line">> Initializing memory banks... [OK]</div>
  <div class="boot-line">> Loading kernel modules... [OK]</div>
  <div class="boot-line">> Scanning for threats... [NONE FOUND]</div>
  <div class="boot-line">> Mounting /home/slippy-spider... [OK]</div>
  <div class="boot-line">> Loading gaming subsystem... [OK]</div>
  <div class="boot-line">> Caffeine level: OPTIMAL ☕</div>
  <div class="boot-line">> All systems NOMINAL</div>
  <div class="boot-line" style="color:#00ff41;margin-top:16px;">> ACCESS GRANTED — Welcome back, Nakib 🕷️</div>
</div>

<!-- MATRIX CANVAS -->
<canvas id="matrix"></canvas>

<!-- CORNER DECORATIONS -->
<div class="corner-tl"></div>
<div class="corner-br"></div>

<div class="wrap">

  <!-- HERO -->
  <div class="hero">
    <div class="avatar-wrap">
      <div class="hex">🕷️</div>
    </div>
    <div class="hero-name">SLIPPY-SPIDER</div>
    <div class="hero-sub">Tamzid Ahmed Nakib · Bangladesh 🇧🇩</div>
    <div id="typewriter"></div>

    <div class="status-bar" style="margin-top:20px;">
      <div class="status-pill">🟢 ONLINE</div>
      <div class="status-pill blue">⚡ CODING</div>
      <div class="status-pill red">🎮 GAMING</div>
      <div class="status-pill">📡 BDT UTC+6</div>
    </div>
  </div>

  <!-- WHOAMI + SKILLS -->
  <div class="sec-head">&gt; IDENTITY_MATRIX</div>
  <div class="grid grid-2">
    <div class="card">
      <div class="card-title">// WHOAMI</div>
      <div class="info-row"><span class="info-key">Name</span><span class="info-val">::  Tamzid Ahmed Nakib</span></div>
      <div class="info-row"><span class="info-key">Handle</span><span class="info-val green">::  slippy-spider</span></div>
      <div class="info-row"><span class="info-key">Role</span><span class="info-val">::  Beginner Programmer</span></div>
      <div class="info-row"><span class="info-key">Location</span><span class="info-val">::  Bangladesh 🇧🇩</span></div>
      <div class="info-row"><span class="info-key">Focus</span><span class="info-val">::  Web Dev + Fulltime Gaming</span></div>
      <div class="info-row"><span class="info-key">Status</span><span class="info-val green">::  Always Dreaming... ∞</span></div>
      <div class="info-row"><span class="info-key">Motto</span><span class="info-val">::  Choices have consequences 👍</span></div>
    </div>

    <div class="card">
      <div class="card-title">// SKILL_SCAN</div>
      <div class="skill-row">
        <div class="skill-label"><span>JavaScript</span><span>90%</span></div>
        <div class="skill-track"><div class="skill-fill" data-w="90"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>React.js</span><span>80%</span></div>
        <div class="skill-track"><div class="skill-fill" data-w="80"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>Node.js</span><span>70%</span></div>
        <div class="skill-track"><div class="skill-fill" data-w="70"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>Python</span><span>75%</span></div>
        <div class="skill-track"><div class="skill-fill" data-w="75"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>MongoDB</span><span>60%</span></div>
        <div class="skill-track"><div class="skill-fill" data-w="60"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>Git / GitHub</span><span>75%</span></div>
        <div class="skill-track"><div class="skill-fill" data-w="75"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span style="color:#b800ff">Gaming 🎮</span><span style="color:#b800ff">99%</span></div>
        <div class="skill-track"><div class="skill-fill" data-w="99" style="background:linear-gradient(90deg,#330033,#b800ff);box-shadow:0 0 8px #b800ff;"></div></div>
      </div>
    </div>
  </div>

  <!-- STATS -->
  <div class="sec-head">&gt; SYSTEM_STATS</div>
  <div class="grid grid-3">
    <div class="stat-box"><div class="stat-num" id="cnt-commits">0</div><div class="stat-label">TOTAL COMMITS</div></div>
    <div class="stat-box"><div class="stat-num" id="cnt-repos">0</div><div class="stat-label">REPOSITORIES</div></div>
    <div class="stat-box"><div class="stat-num" id="cnt-streak">0</div><div class="stat-label">DAY STREAK</div></div>
    <div class="stat-box" style="border-color:#b800ff33;"><div class="stat-num" style="color:#b800ff;text-shadow:0 0 20px #b800ff;" id="cnt-hours">0</div><div class="stat-label" style="color:#b800ff99;">HOURS GAMED</div></div>
    <div class="stat-box"><div class="stat-num" id="cnt-projects">0</div><div class="stat-label">PROJECTS BUILT</div></div>
    <div class="stat-box" style="border-color:#00cfff33;"><div class="stat-num" style="color:#00cfff;text-shadow:0 0 20px #00cfff;">∞</div><div class="stat-label" style="color:#00cfff99;">COFFEE CUPS</div></div>
  </div>

  <!-- PROJECTS -->
  <div class="sec-head">&gt; PROJECT_LOG</div>
  <div class="grid grid-2">
    <div class="proj-card">
      <div class="proj-name">🕸️ career-hub</div>
      <div class="proj-desc">Career portal for professionals — job listings, applications & profiles</div>
      <div><span class="proj-tag">React</span><span class="proj-tag">Node</span><span class="proj-tag">MongoDB</span></div>
      <div class="status-live" style="margin-top:8px;">● LIVE</div>
    </div>
    <div class="proj-card">
      <div class="proj-name">🕸️ student-hub</div>
      <div class="proj-desc">Student management system with dashboards & grade tracking</div>
      <div><span class="proj-tag">React</span><span class="proj-tag">Express</span><span class="proj-tag">MySQL</span></div>
      <div class="status-live" style="margin-top:8px;">● LIVE</div>
    </div>
    <div class="proj-card">
      <div class="proj-name">🕸️ web-project</div>
      <div class="proj-desc">Full stack web application — responsive & modern UI/UX</div>
      <div><span class="proj-tag">JavaScript</span><span class="proj-tag">CSS</span><span class="proj-tag">HTML</span></div>
      <div class="status-live" style="margin-top:8px;">● ACTIVE</div>
    </div>
    <div class="proj-card">
      <div class="proj-name">🕸️ api-project</div>
      <div class="proj-desc">REST API architecture with auth, CRUD & documentation</div>
      <div><span class="proj-tag">Node.js</span><span class="proj-tag">Express</span><span class="proj-tag">JWT</span></div>
      <div class="status-build" style="margin-top:8px;">▶ BUILDING...</div>
    </div>
  </div>

  <!-- GAMING -->
  <div class="sec-head">&gt; GAMING_MODE_ACTIVE</div>
  <div class="grid grid-3">
    <div class="game-card">
      <div class="game-icon">🎮</div>
      <div class="game-name">MAIN GAMER</div>
      <div class="game-rank">Status: ALWAYS ONLINE</div>
    </div>
    <div class="game-card">
      <div class="game-icon">🏆</div>
      <div class="game-name">RANKED GRINDER</div>
      <div class="game-rank">Mode: COMPETITIVE</div>
    </div>
    <div class="game-card">
      <div class="game-icon">⚔️</div>
      <div class="game-name">SPIDER'S LAIR</div>
      <div class="game-rank">Threat Level: MAXIMUM</div>
    </div>
  </div>

  <!-- TERMINAL -->
  <div class="sec-head">&gt; TERMINAL_ACCESS</div>
  <div class="terminal">
    <div class="term-bar">
      <div class="dot r"></div><div class="dot y"></div><div class="dot g"></div>
      <div class="term-title">slippy-spider@kali:~$</div>
    </div>
    <div class="term-line"><span class="prompt">┌──(slippy-spider㉿kali)-[~/]<br/>└─$ </span><span class="cmd">whoami</span></div>
    <div class="term-line"><span class="ok">Tamzid Ahmed Nakib — Beginner Programmer & Fulltime Gamer</span></div>
    <div class="term-line" style="margin-top:8px;"><span class="prompt">└─$ </span><span class="cmd">cat /etc/motto</span></div>
    <div class="term-line"><span class="info">"Choices have consequences 👍"</span></div>
    <div class="term-line" style="margin-top:8px;"><span class="prompt">└─$ </span><span class="cmd">systemctl status spider</span></div>
    <div class="term-line"><span class="ok">● spider.service — ACTIVE (running)</span></div>
    <div class="term-line">&nbsp;&nbsp;&nbsp;Started: Always</div>
    <div class="term-line">&nbsp;&nbsp;&nbsp;Tasks: Coding, Gaming, Dreaming</div>
    <div class="term-line" style="margin-top:8px;"><span class="prompt">└─$ </span><span class="cmd">ping github.com/slippy-spider</span></div>
    <div class="term-line"><span class="ok">PONG — 0ms. Spider web is live. 🕷️</span></div>
    <div class="term-line" style="margin-top:8px;"><span class="prompt">└─$ </span><span id="cursor-line" class="cmd"></span><span style="color:var(--green)">█</span></div>
  </div>

  <!-- TECH STACK -->
  <div class="sec-head">&gt; WEAPONS_ARSENAL</div>
  <div style="display:flex;flex-wrap:wrap;gap:10px;justify-content:center;">
    <img src="https://img.shields.io/badge/JavaScript-0d0d0d?style=for-the-badge&logo=javascript&logoColor=00ff41"/>
    <img src="https://img.shields.io/badge/React-0d0d0d?style=for-the-badge&logo=react&logoColor=00ff41"/>
    <img src="https://img.shields.io/badge/Node.js-0d0d0d?style=for-the-badge&logo=node.js&logoColor=00ff41"/>
    <img src="https://img.shields.io/badge/Python-0d0d0d?style=for-the-badge&logo=python&logoColor=00ff41"/>
    <img src="https://img.shields.io/badge/MongoDB-0d0d0d?style=for-the-badge&logo=mongodb&logoColor=00ff41"/>
    <img src="https://img.shields.io/badge/Express-0d0d0d?style=for-the-badge&logo=express&logoColor=00ff41"/>
    <img src="https://img.shields.io/badge/MySQL-0d0d0d?style=for-the-badge&logo=mysql&logoColor=00ff41"/>
    <img src="https://img.shields.io/badge/HTML5-0d0d0d?style=for-the-badge&logo=html5&logoColor=00ff41"/>
    <img src="https://img.shields.io/badge/CSS3-0d0d0d?style=for-the-badge&logo=css3&logoColor=00ff41"/>
    <img src="https://img.shields.io/badge/Tailwind-0d0d0d?style=for-the-badge&logo=tailwindcss&logoColor=00ff41"/>
    <img src="https://img.shields.io/badge/Git-0d0d0d?style=for-the-badge&logo=git&logoColor=00ff41"/>
    <img src="https://img.shields.io/badge/Linux-0d0d0d?style=for-the-badge&logo=linux&logoColor=00ff41"/>
  </div>

  <footer>
    <div style="font-family:'Orbitron',monospace;font-size:1.1rem;color:var(--green);text-shadow:0 0 10px var(--green);margin-bottom:10px;">🕷️ SLIPPY-SPIDER</div>
    <div>> Coded with ❤️ & ☕ from Bangladesh 🇧🇩</div>
    <div style="margin-top:6px;color:#005510;">> "In the web of code, every thread matters."</div>
  </footer>

</div><!-- /wrap -->

<script>
// ── BOOT SEQUENCE ──
(function(){
  const lines = document.querySelectorAll('.boot-line');
  lines.forEach((l,i)=>{
    setTimeout(()=>{
      l.classList.add('show');
      if(i===lines.length-1){
        setTimeout(()=>{ document.getElementById('boot').classList.add('hidden'); }, 900);
      }
    }, i*300);
  });
})();

// ── MATRIX RAIN ──
(function(){
  const canvas = document.getElementById('matrix');
  const ctx = canvas.getContext('2d');
  let W,H,cols,drops;
  const chars='ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789@#$%^&*()_+-=[]{}|;:,.<>?/\\~`';
  function resize(){
    W=canvas.width=window.innerWidth;
    H=canvas.height=window.innerHeight;
    cols=Math.floor(W/16);
    drops=Array(cols).fill(1);
  }
  resize();
  window.addEventListener('resize',resize);
  function draw(){
    ctx.fillStyle='rgba(3,10,3,0.05)';
    ctx.fillRect(0,0,W,H);
    ctx.fillStyle='#00ff41';
    ctx.font='14px Share Tech Mono';
    drops.forEach((y,i)=>{
      const c=chars[Math.floor(Math.random()*chars.length)];
      ctx.fillText(c,i*16,y*16);
      if(y*16>H&&Math.random()>.975) drops[i]=0;
      drops[i]++;
    });
  }
  setInterval(draw,50);
})();

// ── TYPEWRITER ──
(function(){
  const lines=[
    '> Beginner Programmer / Fulltime Gamer',
    '> Web Developer @ Bangladesh 🇧🇩',
    '> Building: career-hub | student-hub',
    '> Status: ALWAYS DREAMING... ∞',
    '> Choices have consequences 👍',
  ];
  let li=0,ci=0,del=false;
  const el=document.getElementById('typewriter');
  function tick(){
    const txt=lines[li];
    if(!del){ el.textContent=txt.slice(0,++ci); if(ci===txt.length){ del=true; setTimeout(tick,1800); return; } }
    else{ el.textContent=txt.slice(0,--ci); if(ci===0){ del=false; li=(li+1)%lines.length; } }
    setTimeout(tick, del?40:80);
  }
  tick();
})();

// ── SKILL BARS ──
window.addEventListener('load',()=>{
  setTimeout(()=>{
    document.querySelectorAll('.skill-fill').forEach(el=>{
      el.style.width=el.dataset.w+'%';
    });
  }, 1500);
});

// ── COUNT UP ──
function countUp(id,target,duration){
  const el=document.getElementById(id);
  let start=0, step=target/duration*16;
  const t=setInterval(()=>{
    start+=step;
    if(start>=target){ el.textContent=target; clearInterval(t); return; }
    el.textContent=Math.floor(start);
  },16);
}
setTimeout(()=>{
  countUp('cnt-commits',247,1200);
  countUp('cnt-repos',12,800);
  countUp('cnt-streak',21,800);
  countUp('cnt-hours',1337,1500);
  countUp('cnt-projects',8,800);
},1800);
</script>
</body>
</html>
