<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Urvashi Parashar — Tech-Legal Operator</title>
  <link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=Inter:wght@300;400;500;600&family=Space+Mono:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet" />
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      /* Fun Cyberpunk / Neon Palette */
      --bg:           #0b0614; /* Deep midnight purple */
      --bg-grid:      rgba(181, 55, 242, 0.05); /* Faint violet grid */
      --ink:          #F0EBF5;
      
      --accent-1:     #FF0055; /* Hot Neon Pink */
      --accent-2:     #00F0FF; /* Electric Cyan */
      --accent-3:     #FFDF00; /* Star Yellow */
      --accent-4:     #B537F2; /* Synth Purple */
      
      --threat:       #FF3C38; /* Vibrant Warning Red */
      --mid:          #8B949E;
      --rule:         #2A1E3D;
      --card-bg:      #130A21;
      
      --success-text: #00F0FF;
      --success-bg:   rgba(0, 240, 255, 0.08);
      
      --serif:        'DM Serif Display', Georgia, serif;
      --sans:         'Inter', system-ui, sans-serif;
      --mono:         'Space Mono', monospace;
    }

    html { scroll-behavior: smooth; background: var(--bg); }

    body {
      background-color: var(--bg);
      color: var(--ink);
      font-family: var(--sans);
      font-size: 15px;
      line-height: 1.7;
      -webkit-font-smoothing: antialiased;
      overflow-x: hidden;
      position: relative;
      cursor: crosshair; /* Fun target cursor */
    }

    /* ── War Room Background Effects ── */
    body::before {
      content: ''; position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
      background-image: 
        linear-gradient(var(--bg-grid) 1px, transparent 1px),
        linear-gradient(90deg, var(--bg-grid) 1px, transparent 1px);
      background-size: 40px 40px;
      z-index: -2; pointer-events: none;
    }

    .scanlines {
      position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
      background: linear-gradient(to bottom, rgba(255,255,255,0), rgba(255,255,255,0) 50%, rgba(0,0,0,0.15) 50%, rgba(0,0,0,0.15));
      background-size: 100% 4px;
      z-index: 9999; pointer-events: none; opacity: 0.5;
    }

    /* ── Shooting Star Canvas ── */
    #star-canvas {
      position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
      pointer-events: none; z-index: 9998;
    }

    /* ── Layout ── */
    .container {
      max-width: 760px; margin: 0 auto; padding: 0 24px; position: relative;
    }

    /* ── Scroll Progress Bar ── */
    #progress-bar {
      position: fixed; top: 0; left: 0; height: 3px;
      background: linear-gradient(90deg, var(--accent-1), var(--accent-2), var(--accent-3));
      box-shadow: 0 0 15px var(--accent-1);
      width: 0%; z-index: 10000; transition: width 0.1s ease;
    }

    /* ── Nav ── */
    nav {
      border-bottom: 1px solid var(--rule); padding: 20px 0;
      position: sticky; top: 0;
      background: rgba(11, 6, 20, 0.85);
      backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px);
      z-index: 100;
    }
    nav .container { display: flex; justify-content: space-between; align-items: center; }
    .nav-name {
      font-family: var(--mono); font-weight: 700; font-size: 14px;
      letter-spacing: 0.05em; color: var(--ink); text-decoration: none; text-transform: uppercase;
      display: flex; align-items: center; gap: 8px;
    }
    .nav-name::before {
      content: ''; display: block; width: 8px; height: 8px; 
      background: var(--accent-1); border-radius: 50%;
      box-shadow: 0 0 10px var(--accent-1); animation: pulse 1.5s infinite;
    }
    @keyframes pulse {
      0% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.4; transform: scale(0.7); }
      100% { opacity: 1; transform: scale(1); }
    }

    .nav-links { display: flex; gap: 28px; list-style: none; }
    .nav-links a {
      font-family: var(--mono); font-size: 11px; font-weight: 700;
      letter-spacing: 0.1em; text-transform: uppercase; color: var(--mid);
      text-decoration: none; transition: all 0.3s; position: relative;
    }
    .nav-links a:hover, .nav-links a.active {
      color: var(--accent-2); text-shadow: 0 0 10px var(--accent-2);
    }

    /* ── Animations ── */
    .reveal {
      opacity: 0; transform: translateY(20px);
      transition: all 0.8s cubic-bezier(0.0, 0.5, 0.2, 1);
    }
    .reveal.active { opacity: 1; transform: translateY(0); }
    .delay-1 { transition-delay: 0.1s; }
    .delay-2 { transition-delay: 0.2s; }
    .delay-3 { transition-delay: 0.3s; }

    /* ── Hero ── */
    .hero { padding: 120px 0 100px; border-bottom: 1px solid var(--rule); position: relative; }
    .hero-question {
      font-family: var(--serif); font-size: clamp(28px, 5vw, 42px); line-height: 1.25;
      font-style: italic; color: var(--mid); margin-bottom: 24px;
    }
    
    .hero-answer {
      font-family: var(--serif); font-size: clamp(40px, 8vw, 68px);
      line-height: 1.1; color: var(--ink); margin-bottom: 24px; letter-spacing: -0.02em;
    }
    .hero-answer span {
      background: linear-gradient(90deg, var(--accent-2), var(--accent-1));
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
      text-shadow: 0 0 25px rgba(0, 240, 255, 0.3);
    }
    
    .typewriter-text {
      display: inline-block; overflow: hidden; white-space: nowrap;
      border-right: 3px solid var(--accent-2);
      animation: typing 1.5s steps(40, end), blink-caret 0.75s step-end infinite;
      vertical-align: bottom;
    }
    @keyframes typing { from { width: 0 } to { width: 100% } }
    @keyframes blink-caret { from, to { border-color: transparent } 50% { border-color: var(--accent-2); } }

    .hero-sub {
      font-size: 14px; font-weight: 400; color: var(--accent-4);
      letter-spacing: 0.04em; margin-bottom: 36px; text-transform: uppercase;
    }
    .hero-desc { font-size: 16px; line-height: 1.75; color: #A1B0C0; max-width: 600px; margin-bottom: 48px; }
    
    .btn-primary {
      display: inline-flex; align-items: center; justify-content: center;
      background: linear-gradient(45deg, var(--accent-1), var(--accent-4));
      color: #fff; border: none; font-family: var(--mono);
      font-size: 12px; font-weight: 700; letter-spacing: 0.1em;
      text-transform: uppercase; padding: 16px 32px; text-decoration: none;
      transition: all 0.3s; box-shadow: 0 0 20px rgba(255, 0, 85, 0.4); cursor: pointer;
    }
    .btn-primary:hover {
      background: linear-gradient(45deg, var(--accent-2), var(--accent-1));
      box-shadow: 0 0 30px rgba(0, 240, 255, 0.6); transform: scale(1.02);
    }
    .btn-secondary {
      display: inline-flex; align-items: center; justify-content: center;
      border: 1px solid var(--accent-2); color: var(--accent-2);
      font-family: var(--mono); font-size: 12px; font-weight: 700; letter-spacing: 0.1em;
      text-transform: uppercase; padding: 15px 32px; text-decoration: none;
      margin-left: 16px; transition: all 0.3s; background: rgba(0, 240, 255, 0.05);
    }
    .btn-secondary:hover { background: var(--accent-2); color: var(--bg); box-shadow: 0 0 20px rgba(0, 240, 255, 0.4); transform: scale(1.02); }

    /* ── Section Label ── */
    section { padding: 80px 0; border-bottom: 1px dashed var(--rule); }
    section:last-of-type { border-bottom: none; }

    .section-label {
      font-family: var(--mono); font-size: 11px; font-weight: 700;
      letter-spacing: 0.15em; text-transform: uppercase; color: var(--accent-2);
      margin-bottom: 48px; display: flex; align-items: center; gap: 16px;
      text-shadow: 0 0 8px var(--accent-2);
    }
    .section-label::before { content: '[ '; color: var(--accent-4); text-shadow: none; }
    .section-label::after { content: ' ]'; color: var(--rule); flex: 1; letter-spacing: normal; text-shadow: none; }

    /* ── What I Do ── */
    .problem-grid { display: grid; gap: 40px; }
    .problem-item {
      padding-left: 24px; border-left: 2px solid var(--rule);
      transition: all 0.3s ease; position: relative;
    }
    .problem-item::before {
      content: ''; position: absolute; left: -2px; top: 0; width: 2px; height: 0%;
      background: linear-gradient(to bottom, var(--accent-2), var(--accent-1));
      transition: height 0.4s cubic-bezier(0.16, 1, 0.3, 1);
      box-shadow: 0 0 10px var(--accent-1);
    }
    .problem-item:hover { border-left-color: transparent; transform: translateX(8px); }
    .problem-item:hover::before { height: 100%; }
    
    .problem-item h3 { font-family: var(--serif); font-size: 20px; margin-bottom: 12px; color: var(--ink); }
    .problem-item p { font-size: 14.5px; color: var(--mid); line-height: 1.7; }

    /* ── Contract Portfolio Cards ── */
    .contract-list { display: grid; gap: 24px; }
    .contract-item {
      padding: 32px; border: 1px solid var(--rule); background: var(--card-bg);
      position: relative; overflow: hidden; transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .contract-item::before {
      content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 2px;
      background: linear-gradient(90deg, transparent, var(--accent-1), var(--accent-2), transparent);
      opacity: 0; transition: opacity 0.4s;
    }
    .contract-item:hover { 
      border-color: var(--accent-4); transform: translateY(-4px);
      box-shadow: 0 15px 30px rgba(0, 0, 0, 0.6), inset 0 0 20px rgba(181, 55, 242, 0.1);
    }
    .contract-item:hover::before { opacity: 1; }
    
    .contract-tag {
      font-family: var(--mono); font-size: 10px; font-weight: 700;
      letter-spacing: 0.1em; text-transform: uppercase; color: var(--accent-2);
      margin-bottom: 16px; display: inline-block; padding: 4px 8px;
      background: rgba(0, 240, 255, 0.1); border: 1px solid rgba(0, 240, 255, 0.3);
    }
    .contract-item h3 { font-family: var(--serif); font-size: 22px; margin-bottom: 12px; color: var(--ink); }
    .contract-item p { font-size: 14px; color: var(--mid); line-height: 1.7; }
    
    button.contract-status {
      margin-top: 24px; background: transparent; border: 1px solid var(--rule);
      color: var(--mid); font-family: var(--mono); font-size: 11px; font-weight: 700;
      letter-spacing: 0.1em; text-transform: uppercase; padding: 8px 16px;
      cursor: pointer; transition: all 0.3s; display: inline-flex; align-items: center; gap: 8px;
    }
    button.contract-status.ready { color: var(--success-text); border-color: rgba(0, 240, 255, 0.3); background: var(--success-bg); }
    button.contract-status.ready:hover {
      background: rgba(0, 240, 255, 0.15); box-shadow: 0 0 15px rgba(0, 240, 255, 0.3);
      transform: translateX(4px); color: #fff;
    }

    /* ── Writing ── */
    .writing-list { display: grid; gap: 0; }
    .writing-item {
      display: flex; justify-content: space-between; align-items: flex-start; gap: 24px;
      padding: 24px 0; border-bottom: 1px dashed var(--rule); transition: all 0.3s;
    }
    .writing-item:first-child { padding-top: 0; }
    .writing-item:last-child { border-bottom: none; padding-bottom: 0; }
    
    .writing-item:hover { transform: translateX(8px); }
    .writing-meta {
      font-family: var(--mono); font-size: 11px; color: var(--accent-4);
      margin-bottom: 8px; text-transform: uppercase; letter-spacing: 0.1em;
    }
    .writing-item h3 {
      font-family: var(--serif); font-size: 18px;
      color: var(--ink); margin-bottom: 8px; transition: color 0.3s;
    }
    .writing-item:hover h3 { color: var(--accent-1); text-shadow: 0 0 5px rgba(255, 0, 85, 0.4); }
    .writing-item p { font-size: 14px; color: var(--mid); line-height: 1.6; }
    
    .writing-link {
      font-family: var(--mono); flex-shrink: 0; font-size: 11px; font-weight: 700;
      letter-spacing: 0.1em; text-transform: uppercase; color: var(--bg);
      background: var(--accent-2); text-decoration: none; padding: 6px 12px;
      transition: all 0.3s; box-shadow: 0 0 10px rgba(0, 240, 255, 0.5); margin-top: 4px;
    }
    .writing-link:hover { background: #fff; box-shadow: 0 0 20px #fff; transform: scale(1.05); }

    /* ── Memos ── */
    .memo-placeholder {
      border: 1px dashed var(--accent-4); background: rgba(181, 55, 242, 0.03);
      padding: 48px; text-align: center; transition: all 0.3s;
    }
    .memo-placeholder:hover {
      border-color: var(--accent-1); background: rgba(255, 0, 85, 0.05);
      box-shadow: inset 0 0 30px rgba(255, 0, 85, 0.1); transform: scale(1.02);
    }
    .memo-placeholder strong {
      font-family: var(--serif); font-size: 18px; color: var(--ink);
      display: block; margin-bottom: 12px;
    }

    /* ── Background & Competencies ── */
    .bg-grid { display: grid; gap: 32px; }
    .bg-item { border-left: 2px solid var(--rule); padding-left: 20px; transition: border-color 0.3s; }
    .bg-item:hover { border-color: var(--accent-3); }
    .bg-item .bg-label {
      font-family: var(--mono); font-size: 10px; font-weight: 700;
      letter-spacing: 0.1em; text-transform: uppercase; color: var(--mid); margin-bottom: 8px;
    }
    .bg-item h3 { font-family: var(--serif); font-size: 18px; color: var(--ink); margin-bottom: 4px; }
    .bg-item p { font-size: 14px; color: var(--mid); }

    .comp-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin-top: 24px; }
    .comp-item {
      padding: 20px; border: 1px solid var(--rule); background: var(--card-bg);
      font-size: 13.5px; color: var(--mid); transition: all 0.3s;
    }
    .comp-item:hover { border-color: var(--accent-4); box-shadow: 0 0 15px rgba(181, 55, 242, 0.2); transform: translateY(-2px); }
    .comp-item strong {
      font-family: var(--mono); display: block; font-size: 12px; font-weight: 700;
      letter-spacing: 0.1em; text-transform: uppercase; color: var(--accent-3); margin-bottom: 8px;
    }

    /* ── Contact ── */
    .contact-block { display: flex; flex-direction: column; gap: 24px; }
    .contact-line { font-family: var(--serif); font-size: clamp(24px, 5vw, 36px); color: var(--ink); line-height: 1.3; }
    .email-container { display: inline-flex; align-items: center; gap: 12px; margin-top: 8px; }
    .contact-line a {
      color: var(--accent-1); text-decoration: none; 
      border-bottom: 2px solid rgba(255, 0, 85, 0.3); transition: all 0.3s;
      text-shadow: 0 0 10px rgba(255, 0, 85, 0.4);
    }
    .contact-line a:hover { border-color: var(--accent-1); text-shadow: 0 0 20px var(--accent-1); color: #fff; }
    
    .copy-btn {
      background: rgba(255, 0, 85, 0.1); border: 1px solid rgba(255, 0, 85, 0.3);
      color: var(--accent-1); width: 36px; height: 36px;
      display: flex; align-items: center; justify-content: center;
      cursor: pointer; transition: all 0.2s;
    }
    .copy-btn:hover { background: var(--accent-1); color: #fff; box-shadow: 0 0 15px rgba(255, 0, 85, 0.6); }
    .copy-btn svg { width: 16px; height: 16px; fill: currentColor; }
    
    .contact-detail { font-family: var(--sans); font-size: 13.5px; color: var(--mid); }
    .contact-detail a { color: var(--ink); text-decoration: none; border-bottom: 1px solid var(--rule); transition: all 0.2s; }
    .contact-detail a:hover { color: var(--accent-2); border-color: var(--accent-2); }

    /* ── Footer ── */
    footer { padding: 40px 0; border-top: 1px solid var(--rule); }
    footer .container { display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 12px; }
    footer p { font-family: var(--sans); font-size: 12px; color: var(--mid); }
    .footer-links { display: flex; gap: 24px; list-style: none; }
    .footer-links a { font-family: var(--sans); font-size: 12px; color: var(--mid); text-decoration: none; transition: color 0.2s; }
    .footer-links a:hover { color: var(--accent-1); text-shadow: 0 0 8px rgba(255, 0, 85, 0.5); }

    /* ── Modal ── */
    .modal-overlay {
      position: fixed; top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(0, 0, 0, 0.85); backdrop-filter: blur(8px);
      display: flex; align-items: center; justify-content: center;
      z-index: 10000; opacity: 0; pointer-events: none; transition: opacity 0.3s ease;
    }
    .modal-overlay.active { opacity: 1; pointer-events: auto; }
    .modal {
      background: var(--bg); padding: 40px; width: 100%; max-width: 500px;
      border: 1px solid var(--accent-2); box-shadow: 0 0 40px rgba(0, 240, 255, 0.15);
      transform: translateY(20px) scale(0.98); transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
      position: relative;
    }
    .modal-overlay.active .modal { transform: translateY(0) scale(1); }
    .modal-close {
      position: absolute; top: 20px; right: 20px;
      background: none; border: none; color: var(--mid); font-family: var(--mono); font-size: 20px;
      cursor: pointer; transition: color 0.2s;
    }
    .modal-close:hover { color: var(--threat); text-shadow: 0 0 10px rgba(255, 60, 56, 0.8); }
    
    .modal h3 { font-family: var(--serif); font-size: 22px; color: var(--ink); margin-bottom: 12px; }
    .modal p { font-size: 14px; color: var(--mid); margin-bottom: 24px; line-height: 1.6; }
    
    .modal input {
      width: 100%; padding: 14px 16px; border: 1px solid var(--rule);
      background: var(--card-bg); color: var(--ink); font-family: var(--sans); font-size: 14px;
      margin-bottom: 16px; outline: none; transition: border-color 0.2s;
    }
    .modal input:focus { border-color: var(--accent-1); box-shadow: inset 0 0 10px rgba(255, 0, 85, 0.2); }
    .modal button.submit {
      width: 100%; background: linear-gradient(90deg, var(--accent-2), var(--accent-4));
      color: #fff; border: none; padding: 16px; font-family: var(--sans); font-size: 13px; font-weight: 600;
      letter-spacing: 0.06em; text-transform: uppercase; cursor: pointer; transition: all 0.3s;
    }
    .modal button.submit:hover { box-shadow: 0 0 25px rgba(181, 55, 242, 0.6); transform: scale(1.02); }
    
    .modal-success { display: none; text-align: center; padding: 20px 0; }
    .modal-success.active { display: block; }
    .modal-form.hidden { display: none; }

    @media (max-width: 600px) {
      .nav-links { display: none; }
      .hero { padding: 80px 0 60px; }
      .comp-grid { grid-template-columns: 1fr; }
      .writing-item { flex-direction: column; gap: 16px;}
      .btn-secondary { margin-left: 0; margin-top: 12px; width: 100%; }
      .btn-primary { width: 100%; }
      .modal { padding: 32px 24px; width: calc(100% - 32px); }
      .email-container { flex-direction: column; align-items: flex-start; gap: 12px;}
    }
  </style>
</head>
<body>

  <!-- Background Overlays -->
  <div class="scanlines"></div>
  
  <!-- Fun Shooting Star Canvas -->
  <canvas id="star-canvas"></canvas>

  <div id="progress-bar"></div>

  <!-- Nav -->
  <nav>
    <div class="container">
      <a href="#" class="nav-name">Urvashi Parashar</a>
      <ul class="nav-links">
        <li><a href="#work" class="nav-link">Work</a></li>
        <li><a href="#writing" class="nav-link">Writing</a></li>
        <li><a href="#background" class="nav-link">Background</a></li>
        <li><a href="#contact" class="nav-link">Contact</a></li>
      </ul>
    </div>
  </nav>

  <!-- Hero -->
  <div class="hero reveal">
    <div class="container">
      <p class="hero-question">"Who legally owns the liability when our data vendor poisons our model?"</p>
      <h1 class="hero-answer">That's what I<br><span class="typewriter-text">architect.</span></h1>
      <p class="hero-sub">Tech-Legal Operator &nbsp;·&nbsp; AI Compliance Architecture &nbsp;·&nbsp; New Delhi, India</p>
      <p class="hero-desc">
        I help AI startups make their data pipelines, vendor agreements, and model infrastructure legally defensible. I work in the gap between what your engineering team is building and what Indian and EU regulators will scrutinise — before it becomes a due diligence problem.
      </p>
      <div style="display: flex; flex-wrap: wrap;">
        <a href="mailto:urvashiparashar01@gmail.com" class="btn-primary">Enquire about a retainer</a>
        <a href="https://www.linkedin.com/in/urvashi-parashar-a03913413?utm_source=share_via&utm_content=profile&utm_medium=member_android" onclick="window.open(this.href, '_blank'); return false;" target="_blank" rel="noopener noreferrer" class="btn-secondary">LinkedIn</a>
      </div>
    </div>
  </div>

  <!-- What I Do -->
  <section id="work" class="section-block">
    <div class="container">
      <div class="section-label reveal">What I solve</div>
      <div class="problem-grid">
        <div class="problem-item reveal delay-1">
          <h3>Your data vendor agreement has no poisoning clause</h3>
          <p>If a vendor's dataset contains Nightshade or Glaze-poisoned images and corrupts your model, you absorb the GPU retraining cost. Standard DPA templates do not address adversarial data liability. I draft clauses that shift that cost back to the vendor — with liquidated damages that make enforcement credible.</p>
        </div>
        <div class="problem-item reveal delay-2">
          <h3>Your ingestion pipeline classifies you as a Data Fiduciary</h3>
          <p>Under the DPDP Act, routing Indian user prompts to cloud inference (OpenAI, AWS, Azure) makes you a Data Fiduciary — triggering consent, erasure, and grievance obligations most startups have no architecture to fulfil. I map the edge inference structures that legally remove that classification.</p>
        </div>
        <div class="problem-item reveal delay-3">
          <h3>Your AI output liability is unwritten</h3>
          <p>When your model gives a user flawed financial, legal, or medical data — who holds the liability? The traditional contract playbook does not account for probabilistic outputs. I draft the three foundational liability shields your terms of service is missing.</p>
        </div>
        <div class="problem-item reveal delay-1">
          <h3>Your Series A due diligence has no compliance architecture report</h3>
          <p>VCs with technical due diligence teams will look at your data pipeline's legal defensibility. I prepare compliance architecture documentation that passes scrutiny — turning compliance from a cost centre into a fundable IP asset.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- Contract Portfolio -->
  <section class="section-block">
    <div class="container">
      <div class="section-label reveal">Contract Portfolio</div>
      <div class="contract-list">

        <div class="contract-item reveal delay-1">
          <div class="contract-tag">Draft Contract — Vendor Agreement</div>
          <h3>External Vendor DPA with No-Training Mandate</h3>
          <p>A Data Processing Addendum structured for vector database providers (e.g. Pinecone). Core operative clause prohibits the vendor from using client vector embeddings or query logs to train internal models or improve indexing algorithms — with annual audit rights and immediate termination trigger on breach. Drafted because standard DPA templates contain no such restriction.</p>
          <button class="contract-status ready" data-modal="External Vendor DPA">
            Portfolio Draft — Request Access
            <svg width="12" height="12" viewBox="0 0 256 256" fill="currentColor"><path d="M221.66,133.66l-72,72a8,8,0,0,1-11.32-11.32L196.69,136H40a8,8,0,0,1,0-16H196.69L138.34,61.66a8,8,0,0,1,11.32-11.32l72,72A8,8,0,0,1,221.66,133.66Z"></path></svg>
          </button>
        </div>

        <div class="contract-item reveal delay-2">
          <div class="contract-tag">Draft Contract — Liability Clause</div>
          <h3>Adversarial Data Poisoning Liability Clause</h3>
          <p>An operative indemnification clause allocating GPU model retraining costs to upstream data vendors upon confirmed adversarial poisoning events (Nightshade, Glaze, or equivalent). Liquidated damages set at the higher of 10× contract value or $50,000 — calibrated to make the penalty meaningful regardless of deal size. Trigger mechanism tied to C2PA manifest rejection or third-party forensic confirmation. No standard template exists for this clause.</p>
          <button class="contract-status ready" data-modal="Adversarial Data Poisoning Liability Clause">
            Portfolio Draft — Request Access
            <svg width="12" height="12" viewBox="0 0 256 256" fill="currentColor"><path d="M221.66,133.66l-72,72a8,8,0,0,1-11.32-11.32L196.69,136H40a8,8,0,0,1,0-16H196.69L138.34,61.66a8,8,0,0,1,11.32-11.32l72,72A8,8,0,0,1,221.66,133.66Z"></path></svg>
          </button>
        </div>

        <div class="contract-item reveal delay-3">
          <div class="contract-tag">Draft Contract — Commercial</div>
          <h3>AI Output Indemnification Clause for Enterprise SaaS</h3>
          <p>Three-part liability shield for generative AI platforms: (1) explicit redefinition of accuracy under a probabilistic model standard, eliminating implied perfection claims; (2) mandatory human-review verification burden shifted to the end user; (3) ironclad consequential damages waiver for AI-generated output errors. Structured for B2B enterprise SaaS terms of service.</p>
          <button class="contract-status ready" data-modal="AI Output Indemnification Clause">
            Portfolio Draft — Request Access
            <svg width="12" height="12" viewBox="0 0 256 256" fill="currentColor"><path d="M221.66,133.66l-72,72a8,8,0,0,1-11.32-11.32L196.69,136H40a8,8,0,0,1,0-16H196.69L138.34,61.66a8,8,0,0,1,11.32-11.32l72,72A8,8,0,0,1,221.66,133.66Z"></path></svg>
          </button>
        </div>

        <div class="contract-item reveal delay-1">
          <div class="contract-tag" style="color:var(--mid); border-color:var(--rule); background:transparent;">Coming — July 2026</div>
          <h3>Model Collapse Liability Framework</h3>
          <p>A contract framework allocating liability when recursive AI-generated training data degrades model performance over successive generations — an emerging risk with no existing legal precedent in Indian contract law.</p>
          <span style="font-size:11px;font-family:var(--mono);color:var(--mid);text-transform:uppercase;margin-top:14px;display:inline-block;">In progress</span>
        </div>

      </div>
    </div>
  </section>

  <!-- Compliance Memos -->
  <section class="section-block">
    <div class="container reveal">
      <div class="section-label">Compliance Memos</div>
      <div class="memo-placeholder">
        <strong>DPDP Act Exposure Analyses — Coming July 2026</strong>
        <p style="font-size:13px; color:var(--mid);">Applied compliance architecture memos for real Indian AI startups.</p>
        <p style="font-size:13px; color:var(--mid);">Covering Data Fiduciary classification risk, IT Act Section 79 safe-harbour gaps, and EU AI Act obligations for India-to-Europe expansion.</p>
      </div>
    </div>
  </section>

  <!-- Writing -->
  <section id="writing" class="section-block">
    <div class="container">
      <div class="section-label reveal">Published Analysis</div>
      <div class="writing-list">

        <div class="writing-item reveal delay-1">
          <div>
            <div class="writing-meta">LinkedIn · June 2026</div>
            <h3>Why Tech-Legal Operators Survive AI Replacement</h3>
            <p>On the U.S. v. Heppner ruling, attorney-client privilege destruction through non-enterprise AI tools, and why explicit legal gates are mandatory — not optional — when deploying LLMs in enterprise environments.</p>
          </div>
          <a href="https://www.linkedin.com/posts/urvashi-parashar-a03913413_legaltech-aigovernance-legalops-activity-7468213705827246080-9iW-?utm_source=social_share_send&utm_medium=android_app&rcm=ACoAAGlSBuMBTiKLms41MXiwgLhQ4ZoseqoTi9g&utm_campaign=copy_link" onclick="window.open(this.href, '_blank'); return false;" target="_blank" rel="noopener noreferrer" class="writing-link">Read →</a>
        </div>

        <div class="writing-item reveal delay-2">
          <div>
            <div class="writing-meta">LinkedIn · June 2026</div>
            <h3>The DPDP Act Compliance Loophole Built into Google Chrome</h3>
            <p>How Gemini Nano's on-device inference architecture legally removes Indian AI startups from Data Fiduciary classification — and what this means for your Q3/Q4 engineering roadmap and API cost structure.</p>
          </div>
          <a href="https://www.linkedin.com/posts/urvashi-parashar-a03913413_generativeai-fintech-dpdpact-share-7468984164927627264-RCNP/?utm_source=social_share_send&utm_medium=android_app&rcm=ACoAAGlSBuMBTiKLms41MXiwgLhQ4ZoseqoTi9g&utm_campaign=copy_link" onclick="window.open(this.href, '_blank'); return false;" target="_blank" rel="noopener noreferrer" class="writing-link">Read →</a>
        </div>

        <div class="writing-item reveal delay-3">
          <div>
            <div class="writing-meta">LinkedIn · June 2026</div>
            <h3>Three Liability Shields Your AI Terms of Service Is Missing</h3>
            <p>When your model produces a hallucination that costs a user money — who holds the liability? The traditional commercial contract playbook fails for probabilistic outputs. The three foundational clauses that close the gap.</p>
          </div>
          <a href="https://www.linkedin.com/posts/urvashi-parashar-a03913413_ailaw-legalops-techstartups-activity-7467836881213284352-fOV6?utm_source=social_share_send&utm_medium=android_app&rcm=ACoAAGlSBuMBTiKLms41MXiwgLhQ4ZoseqoTi9g&utm_campaign=copy_link" onclick="window.open(this.href, '_blank'); return false;" target="_blank" rel="noopener noreferrer" class="writing-link">Read →</a>
        </div>

        <div class="writing-item reveal delay-1">
          <div>
            <div class="writing-meta">Long-form · Coming July 2026</div>
            <h3>What Every Indian AI Startup Gets Wrong About Their Data Vendor Agreements</h3>
            <p>A full analysis of the unpriced legal liability sitting inside standard data licensing agreements — and the specific clauses that don't exist yet but should.</p>
          </div>
          <span style="font-size:11px;font-family:var(--mono);color:var(--mid);font-weight:700;letter-spacing:0.1em;text-transform:uppercase;margin-top:4px;display:inline-block;">In progress</span>
        </div>

        <div class="writing-item reveal delay-2">
          <div>
            <div class="writing-meta">Long-form · Coming July 2026</div>
            <h3>Adversarial Data Poisoning Creates Unpriced Legal Liability</h3>
            <p>How Nightshade and Glaze attacks expose AI companies to retraining costs with no contractual remedy — and the liability architecture that closes that gap.</p>
          </div>
          <span style="font-size:11px;font-family:var(--mono);color:var(--mid);font-weight:700;letter-spacing:0.1em;text-transform:uppercase;margin-top:4px;display:inline-block;">In progress</span>
        </div>

      </div>
    </div>
  </section>

  <!-- Background -->
  <section id="background" class="section-block">
    <div class="container">
      <div class="section-label reveal">Background</div>
      
      <div class="bg-grid">
        <div class="bg-item reveal delay-1">
          <div class="bg-label">Current</div>
          <h3>AI Compliance Architecture — Independent Research & Portfolio Development</h3>
          <p>January 2026 – Present · New Delhi, India</p>
        </div>
        <div class="bg-item reveal delay-2">
          <div class="bg-label">Legal Practice</div>
          <h3>Legal Intern — Gautam & Company, Advocates</h3>
          <p>February – May 2026 · Delhi High Court & Supreme Court of India</p>
        </div>
        <div class="bg-item reveal delay-3">
          <div class="bg-label">Education</div>
          <h3>B.A. LL.B. (Hons.) — MDU-CPAS, Gurugram</h3>
          <p>Class of 2026</p>
        </div>
        <div class="bg-item reveal delay-1">
          <div class="bg-label">Education — In Progress</div>
          <h3>LLM in AI & Technology</h3>
          <p>Expected 2027</p>
        </div>
      </div>

      <div style="margin-top: 64px;">
        <div class="section-label reveal">Core Competencies</div>
        <div class="comp-grid">
          <div class="comp-item reveal delay-1"><strong>Regulatory</strong>DPDP Act · EU AI Act (Art. 50) · IT Act Section 79 · C2PA Standards</div>
          <div class="comp-item reveal delay-2"><strong>Pipeline Auditing</strong>Adversarial poisoning defence · Data provenance · Anonymization gates · Edge inference</div>
          <div class="comp-item reveal delay-3"><strong>Contracting</strong>Vendor DPAs · No-Training mandates · Poisoning liability · Zero-retention protocols</div>
          <div class="comp-item reveal delay-4"><strong>Legal Analysis</strong>Manupatra research · Ratio Decidendi · Compliance architecture reporting</div>
        </div>
      </div>
    </div>
  </section>

  <!-- Contact -->
  <section id="contact" class="section-block">
    <div class="container">
      <div class="section-label reveal">Contact</div>
      <div class="contact-block reveal delay-1">
        <p class="contact-line">
          Available for remote retainer engagements.<br>
          <span class="email-container">
            <a href="mailto:urvashiparashar01@gmail.com" id="contact-email">urvashiparashar01@gmail.com</a>
            <button class="copy-btn" id="copy-btn" aria-label="Copy Email" title="Copy email address">
              <svg viewBox="0 0 256 256"><path d="M216,40H88a8,8,0,0,0-8,8V80H40a8,8,0,0,0-8,8V216a8,8,0,0,0,8,8H168a8,8,0,0,0,8-8V176h40a8,8,0,0,0,8-8V48A8,8,0,0,0,216,40Zm-56,168H48V96H160Zm48-48H176V88a8,8,0,0,0-8-8H96V56H208Z"></path></svg>
            </button>
          </span>
        </p>
        <p class="contact-detail">
          +91 7404105910 &nbsp;·&nbsp;
          <a href="https://www.linkedin.com/in/urvashi-parashar-a03913413?utm_source=share_via&utm_content=profile&utm_medium=member_android" onclick="window.open(this.href, '_blank'); return false;" target="_blank" rel="noopener noreferrer">LinkedIn</a> &nbsp;·&nbsp;
          New Delhi, India
        </p>
        <p style="font-size:14px;color:var(--mid);max-width:500px;line-height:1.7; border-left: 2px solid var(--rule); padding-left: 16px; font-family: var(--sans);">
          I work with AI startups, enterprise SaaS companies, and YC-backed founders on data pipeline compliance, vendor contract architecture, and regulatory due diligence preparation. Engagements are structured as professional retainers, not employment.
        </p>
      </div>
    </div>
  </section>

  <!-- Footer -->
  <footer>
    <div class="container">
      <p>© 2026 Urvashi Parashar. All rights reserved.</p>
      <ul class="footer-links">
        <li><a href="mailto:urvashiparashar01@gmail.com">Email</a></li>
        <li><a href="https://www.linkedin.com/in/urvashi-parashar-a03913413?utm_source=share_via&utm_content=profile&utm_medium=member_android" onclick="window.open(this.href, '_blank'); return false;" target="_blank" rel="noopener noreferrer">LinkedIn</a></li>
      </ul>
    </div>
  </footer>

  <!-- Request Modal -->
  <div class="modal-overlay" id="request-modal">
    <div class="modal">
      <button class="modal-close" id="modal-close">&times;</button>
      
      <div id="modal-form-view" class="modal-form">
        <h3>Request Draft Access</h3>
        <p>Enter your details to receive a secure link to view the <strong id="modal-doc-name" style="color:var(--accent-2);"></strong> draft.</p>
        <form id="portfolio-form" onsubmit="handleModalSubmit(event)">
          <input type="text" placeholder="Full Name" required />
          <input type="email" placeholder="Work Email" required />
          <button type="submit" class="submit">Request Access</button>
        </form>
      </div>
      
      <div id="modal-success-view" class="modal-success">
        <svg width="48" height="48" viewBox="0 0 256 256" style="fill: var(--accent-2); margin: 0 auto 16px; filter: drop-shadow(0 0 10px var(--accent-2));">
          <path d="M128,24A104,104,0,1,0,232,128,104.11,104.11,0,0,0,128,24Zm45.66,85.66-56,56a8,8,0,0,1-11.32,0l-24-24a8,8,0,0,1,11.32-11.32L112,148.69l50.34-50.35a8,8,0,0,1,11.32,11.32Z"></path>
        </svg>
        <h3>Request Received</h3>
        <p>I will review your request and share the portfolio draft via email shortly.</p>
      </div>
    </div>
  </div>

  <!-- Interactive Scripts -->
  <script>
    // 1. Fun Shooting Star Cursor Effect (Canvas)
    const canvas = document.getElementById('star-canvas');
    const ctx = canvas.getContext('2d');
    let w = canvas.width = window.innerWidth;
    let h = canvas.height = window.innerHeight;
    
    window.addEventListener('resize', () => {
      w = canvas.width = window.innerWidth;
      h = canvas.height = window.innerHeight;
    });

    const sparks = [];
    const trail = [];
    const colors = ['#FF0055', '#00F0FF', '#B537F2', '#FFDF00'];
    let lastPos = { x: w/2, y: h/2 };

    function addSpark(x, y, dx, dy) {
      sparks.push({
        x: x, y: y,
        vx: dx * 0.05 + (Math.random() - 0.5) * 6,
        vy: dy * 0.05 + (Math.random() - 0.5) * 6,
        life: 1,
        color: colors[Math.floor(Math.random() * colors.length)],
        size: Math.random() * 3 + 1
      });
    }

    function handleInput(x, y) {
      const dx = x - lastPos.x;
      const dy = y - lastPos.y;
      lastPos = {x, y};
      
      trail.push({x, y, life: 1});
      
      // Emit sparks based on movement speed
      if(Math.abs(dx) > 3 || Math.abs(dy) > 3) {
        for(let i=0; i<2; i++) addSpark(x, y, -dx, -dy);
      }
    }

    window.addEventListener('mousemove', e => handleInput(e.clientX, e.clientY));
    window.addEventListener('touchmove', e => {
      if(e.touches.length > 0) handleInput(e.touches[0].clientX, e.touches[0].clientY);
    });

    function animateStar() {
      ctx.clearRect(0, 0, w, h);
      
      // Draw Comet Trail
      if (trail.length > 1) {
        for(let i=1; i<trail.length; i++) {
          const p1 = trail[i-1];
          const p2 = trail[i];
          
          if (i === 1) p1.life -= 0.04;
          p2.life -= 0.04;
          
          if(p1.life <= 0) {
            trail.splice(i-1, 1);
            i--; continue;
          }
          
          ctx.beginPath();
          ctx.moveTo(p1.x, p1.y);
          ctx.lineTo(p2.x, p2.y);
          ctx.strokeStyle = `rgba(0, 240, 255, ${p2.life})`;
          ctx.lineWidth = p2.life * 8; // Tapering effect
          ctx.lineCap = 'round';
          ctx.stroke();
        }
      }

      // Draw Sparks
      ctx.globalCompositeOperation = 'screen';
      for(let i=0; i<sparks.length; i++) {
        const s = sparks[i];
        s.x += s.vx; s.y += s.vy;
        s.life -= 0.025;
        s.size *= 0.96;
        
        if(s.life <= 0) { sparks.splice(i, 1); i--; continue; }
        
        ctx.beginPath();
        ctx.arc(s.x, s.y, s.size, 0, Math.PI*2);
        ctx.fillStyle = s.color;
        ctx.globalAlpha = s.life;
        ctx.shadowBlur = 10;
        ctx.shadowColor = s.color;
        ctx.fill();
      }
      ctx.globalAlpha = 1;
      ctx.shadowBlur = 0;
      ctx.globalCompositeOperation = 'source-over';
      
      requestAnimationFrame(animateStar);
    }
    animateStar();

    // 2. Scroll Progress Bar
    window.addEventListener('scroll', () => {
      const winScroll = document.body.scrollTop || document.documentElement.scrollTop;
      const height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
      const scrolled = (winScroll / height) * 100;
      document.getElementById('progress-bar').style.width = scrolled + '%';
    });

    // 3. Scroll Reveal Animations
    const revealElements = document.querySelectorAll('.reveal');
    const revealObserver = new IntersectionObserver((entries, observer) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('active');
          observer.unobserve(entry.target);
        }
      });
    }, { rootMargin: "0px 0px -50px 0px", threshold: 0.1 });

    revealElements.forEach(el => revealObserver.observe(el));

    // 4. Active Nav Tracking
    const sections = document.querySelectorAll('.section-block');
    const navLinks = document.querySelectorAll('.nav-link');

    window.addEventListener('scroll', () => {
      let current = '';
      sections.forEach(section => {
        const sectionTop = section.offsetTop;
        if (scrollY >= (sectionTop - 200)) {
          current = section.getAttribute('id');
        }
      });
      navLinks.forEach(link => {
        link.classList.remove('active');
        if (link.getAttribute('href').includes(current)) {
          link.classList.add('active');
        }
      });
    });

    // 5. Portfolio Request Modal
    const modalOverlay = document.getElementById('request-modal');
    const modalClose = document.getElementById('modal-close');
    const requestBtns = document.querySelectorAll('button[data-modal]');
    const docNameSpan = document.getElementById('modal-doc-name');
    const formView = document.getElementById('modal-form-view');
    const successView = document.getElementById('modal-success-view');

    function openModal(docName) {
      docNameSpan.textContent = docName;
      formView.classList.remove('hidden');
      successView.classList.remove('active');
      document.getElementById('portfolio-form').reset();
      modalOverlay.classList.add('active');
    }

    function closeModal() {
      modalOverlay.classList.remove('active');
    }

    requestBtns.forEach(btn => {
      btn.addEventListener('click', (e) => {
        openModal(e.currentTarget.getAttribute('data-modal'));
      });
    });

    modalClose.addEventListener('click', closeModal);
    modalOverlay.addEventListener('click', (e) => {
      if(e.target === modalOverlay) closeModal();
    });

    function handleModalSubmit(e) {
      e.preventDefault();
      formView.classList.add('hidden');
      successView.classList.add('active');
      setTimeout(() => { closeModal(); }, 3000);
    }

    // 6. Copy to Clipboard
    const copyBtn = document.getElementById('copy-btn');
    const emailText = document.getElementById('contact-email').innerText;
    
    copyBtn.addEventListener('click', async () => {
      try {
        await navigator.clipboard.writeText(emailText);
        const originalIcon = copyBtn.innerHTML;
        copyBtn.innerHTML = '<svg viewBox="0 0 256 256" style="fill: var(--bg)"><path d="M173.66,98.34a8,8,0,0,1,0,11.32l-56,56a8,8,0,0,1-11.32,0l-24-24a8,8,0,0,1,11.32-11.32L112,148.69l50.34-50.35A8,8,0,0,1,173.66,98.34ZM232,128A104,104,0,1,1,128,24,104.11,104.11,0,0,1,232,128Zm-16,0a88,88,0,1,0-88,88A88.1,88.1,0,0,0,216,128Z"></path></svg>';
        copyBtn.style.background = 'var(--accent-1)';
        setTimeout(() => {
          copyBtn.innerHTML = originalIcon;
          copyBtn.style.background = '';
        }, 2000);
      } catch (err) {
        // Fallback
        const tempInput = document.createElement("input");
        tempInput.value = emailText;
        document.body.appendChild(tempInput);
        tempInput.select();
        document.execCommand("copy");
        document.body.removeChild(tempInput);
        
        const originalIcon = copyBtn.innerHTML;
        copyBtn.innerHTML = '<svg viewBox="0 0 256 256" style="fill: var(--bg)"><path d="M173.66,98.34a8,8,0,0,1,0,11.32l-56,56a8,8,0,0,1-11.32,0l-24-24a8,8,0,0,1,11.32-11.32L112,148.69l50.34-50.35A8,8,0,0,1,173.66,98.34ZM232,128A104,104,0,1,1,128,24,104.11,104.11,0,0,1,232,128Zm-16,0a88,88,0,1,0-88,88A88.1,88.1,0,0,0,216,128Z"></path></svg>';
        copyBtn.style.background = 'var(--accent-1)';
        setTimeout(() => { copyBtn.innerHTML = originalIcon; copyBtn.style.background = ''; }, 2000);
      }
    });
  </script>

</body>
</html>
