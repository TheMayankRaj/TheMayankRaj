<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mayank Raj — AI Developer & Creative Technologist</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #060610;
    --bg2: #0d0d1f;
    --cyan: #00e5ff;
    --orange: #ff5e1a;
    --violet: #7b5ea7;
    --white: #f0f0ff;
    --muted: #7070a0;
    --card: rgba(255,255,255,0.03);
    --border: rgba(0,229,255,0.12);
    --glow: 0 0 40px rgba(0,229,255,0.15);
  }

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    color: var(--white);
    overflow-x: hidden;
    cursor: none;
  }

  /* CUSTOM CURSOR */
  .cursor {
    position: fixed; top: 0; left: 0;
    width: 12px; height: 12px;
    background: var(--cyan);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9999;
    transform: translate(-50%, -50%);
    transition: transform 0.1s ease, width 0.2s ease, height 0.2s ease, opacity 0.2s ease;
    mix-blend-mode: screen;
  }
  .cursor-ring {
    position: fixed; top: 0; left: 0;
    width: 36px; height: 36px;
    border: 1.5px solid rgba(0,229,255,0.5);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9998;
    transform: translate(-50%, -50%);
    transition: transform 0.18s ease, width 0.25s ease, height 0.25s ease, border-color 0.2s ease;
  }
  .cursor.hover { width: 18px; height: 18px; }
  .cursor-ring.hover { width: 54px; height: 54px; border-color: var(--orange); }

  /* CANVAS BACKGROUND */
  #bg-canvas {
    position: fixed; top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    opacity: 0.6;
  }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 100;
    padding: 20px 60px;
    display: flex; justify-content: space-between; align-items: center;
    background: linear-gradient(to bottom, rgba(6,6,16,0.9), transparent);
    backdrop-filter: blur(2px);
  }
  .nav-logo {
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: 1.3rem;
    letter-spacing: -0.02em;
    color: var(--white);
  }
  .nav-logo span { color: var(--cyan); }
  .nav-links { display: flex; gap: 36px; list-style: none; }
  .nav-links a {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    color: var(--muted);
    text-decoration: none;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    transition: color 0.2s;
    position: relative;
  }
  .nav-links a::after {
    content: '';
    position: absolute; bottom: -4px; left: 0;
    width: 0; height: 1px;
    background: var(--cyan);
    transition: width 0.25s ease;
  }
  .nav-links a:hover { color: var(--cyan); }
  .nav-links a:hover::after { width: 100%; }

  /* SECTIONS */
  section { position: relative; z-index: 1; }

  /* HERO */
  #hero {
    min-height: 100vh;
    display: flex; align-items: center;
    padding: 120px 60px 80px;
    position: relative;
    overflow: hidden;
  }

  .hero-bg-text {
    position: absolute;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    font-family: 'Syne', sans-serif;
    font-size: clamp(80px, 18vw, 220px);
    font-weight: 800;
    color: rgba(0,229,255,0.03);
    white-space: nowrap;
    user-select: none;
    letter-spacing: -0.04em;
    z-index: 0;
    animation: floatText 8s ease-in-out infinite;
  }

  @keyframes floatText {
    0%, 100% { transform: translate(-50%, -50%) translateY(0px); }
    50% { transform: translate(-50%, -50%) translateY(-20px); }
  }

  .hero-content { position: relative; z-index: 2; max-width: 900px; }

  .hero-tag {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.78rem;
    color: var(--cyan);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 28px;
    display: flex; align-items: center; gap: 12px;
    opacity: 0;
    animation: fadeUp 0.7s ease forwards 0.3s;
  }
  .hero-tag::before {
    content: '';
    width: 32px; height: 1px;
    background: var(--cyan);
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(52px, 8vw, 110px);
    font-weight: 800;
    line-height: 0.92;
    letter-spacing: -0.04em;
    margin-bottom: 28px;
    opacity: 0;
    animation: fadeUp 0.8s ease forwards 0.5s;
  }

  .hero-name .line2 {
    color: transparent;
    -webkit-text-stroke: 1.5px rgba(0,229,255,0.5);
    display: block;
  }

  .hero-desc {
    font-size: 1.1rem;
    color: var(--muted);
    line-height: 1.75;
    max-width: 500px;
    margin-bottom: 48px;
    font-weight: 300;
    opacity: 0;
    animation: fadeUp 0.8s ease forwards 0.7s;
  }

  .hero-cta {
    display: flex; gap: 20px; align-items: center;
    opacity: 0;
    animation: fadeUp 0.8s ease forwards 0.9s;
  }

  .btn-primary {
    padding: 14px 36px;
    background: var(--cyan);
    color: var(--bg);
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 0.9rem;
    letter-spacing: 0.03em;
    border: none;
    cursor: none;
    text-decoration: none;
    clip-path: polygon(0 0, calc(100% - 12px) 0, 100% 12px, 100% 100%, 12px 100%, 0 calc(100% - 12px));
    transition: all 0.25s ease;
    position: relative;
    overflow: hidden;
  }
  .btn-primary::before {
    content: '';
    position: absolute; inset: 0;
    background: var(--orange);
    transform: translateX(-110%);
    transition: transform 0.3s ease;
    z-index: 0;
  }
  .btn-primary:hover::before { transform: translateX(0); }
  .btn-primary span { position: relative; z-index: 1; }

  .btn-ghost {
    padding: 14px 36px;
    background: transparent;
    color: var(--white);
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.8rem;
    letter-spacing: 0.1em;
    border: 1px solid var(--border);
    cursor: none;
    text-decoration: none;
    transition: all 0.25s ease;
  }
  .btn-ghost:hover { border-color: var(--cyan); color: var(--cyan); }

  .hero-scroll {
    position: absolute; bottom: 40px; left: 60px;
    display: flex; align-items: center; gap: 12px;
    opacity: 0;
    animation: fadeIn 1s ease forwards 1.5s;
  }
  .scroll-line {
    width: 1px; height: 60px;
    background: linear-gradient(to bottom, transparent, var(--cyan));
    animation: scrollPulse 2s ease infinite;
  }
  @keyframes scrollPulse {
    0%, 100% { opacity: 0.4; }
    50% { opacity: 1; }
  }
  .scroll-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    color: var(--muted);
    writing-mode: vertical-rl;
    letter-spacing: 0.2em;
    text-transform: uppercase;
  }

  .hero-stats {
    position: absolute; right: 60px; bottom: 60px;
    display: flex; flex-direction: column; gap: 24px;
    opacity: 0;
    animation: fadeIn 1s ease forwards 1.2s;
  }
  .stat { text-align: right; }
  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 2rem;
    font-weight: 800;
    color: var(--cyan);
    line-height: 1;
  }
  .stat-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    color: var(--muted);
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }

  /* ABOUT */
  #about {
    padding: 120px 60px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: center;
    border-top: 1px solid var(--border);
  }

  .about-visual {
    position: relative;
    height: 420px;
  }

  .about-card {
    position: absolute;
    background: var(--card);
    border: 1px solid var(--border);
    padding: 28px;
    backdrop-filter: blur(12px);
    transition: transform 0.4s ease, box-shadow 0.4s ease;
  }
  .about-card:hover { transform: translateY(-6px); box-shadow: var(--glow); }

  .card-main {
    width: 280px; top: 0; left: 0;
    clip-path: polygon(0 0, calc(100% - 20px) 0, 100% 20px, 100% 100%, 0 100%);
  }
  .card-float {
    width: 200px; bottom: 0; right: 0;
    clip-path: polygon(0 0, 100% 0, 100% 100%, 20px 100%, 0 calc(100% - 20px));
    background: rgba(0,229,255,0.05);
    border-color: rgba(0,229,255,0.2);
    animation: floatCard 5s ease-in-out infinite;
  }
  .card-accent {
    width: 160px; top: 50%; right: 20px;
    background: rgba(255,94,26,0.08);
    border-color: rgba(255,94,26,0.25);
    animation: floatCard 7s ease-in-out infinite 1s;
    padding: 20px;
  }

  @keyframes floatCard {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-12px); }
  }

  .card-icon { font-size: 2rem; margin-bottom: 12px; }
  .card-title {
    font-family: 'Syne', sans-serif;
    font-size: 1rem;
    font-weight: 700;
    color: var(--white);
    margin-bottom: 8px;
  }
  .card-desc { font-size: 0.82rem; color: var(--muted); line-height: 1.6; }

  .section-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.72rem;
    color: var(--cyan);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 16px;
    display: flex; align-items: center; gap: 10px;
  }
  .section-label::before {
    content: '';
    width: 24px; height: 1px;
    background: var(--cyan);
  }

  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(32px, 4vw, 52px);
    font-weight: 800;
    line-height: 1.05;
    letter-spacing: -0.03em;
    margin-bottom: 24px;
  }

  .section-title em {
    font-style: normal;
    color: var(--orange);
  }

  .about-text {
    font-size: 1rem;
    color: var(--muted);
    line-height: 1.85;
    font-weight: 300;
    margin-bottom: 36px;
  }

  .about-tags { display: flex; flex-wrap: wrap; gap: 10px; }
  .tag {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.72rem;
    padding: 6px 14px;
    border: 1px solid var(--border);
    color: var(--muted);
    letter-spacing: 0.05em;
    transition: all 0.2s;
  }
  .tag:hover { border-color: var(--cyan); color: var(--cyan); background: rgba(0,229,255,0.05); }

  /* SKILLS */
  #skills {
    padding: 120px 60px;
    border-top: 1px solid var(--border);
  }

  .skills-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    margin-bottom: 72px;
  }

  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 2px;
  }

  .skill-card {
    background: var(--card);
    border: 1px solid var(--border);
    padding: 28px 32px;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }
  .skill-card::before {
    content: '';
    position: absolute; top: 0; left: 0;
    width: 3px; height: 0;
    background: var(--cyan);
    transition: height 0.4s ease;
  }
  .skill-card:hover::before { height: 100%; }
  .skill-card:hover {
    background: rgba(0,229,255,0.04);
    transform: translateX(4px);
  }

  .skill-category {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    color: var(--orange);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 12px;
  }

  .skill-name {
    font-family: 'Syne', sans-serif;
    font-size: 1.05rem;
    font-weight: 700;
    color: var(--white);
    margin-bottom: 8px;
  }

  .skill-detail {
    font-size: 0.8rem;
    color: var(--muted);
    line-height: 1.5;
  }

  .skill-icon { font-size: 1.6rem; margin-bottom: 14px; }

  /* PROJECTS */
  #projects {
    padding: 120px 60px;
    border-top: 1px solid var(--border);
  }

  .projects-grid {
    display: grid;
    grid-template-columns: 1.5fr 1fr;
    gap: 2px;
    margin-top: 64px;
  }

  .project-card {
    background: var(--card);
    border: 1px solid var(--border);
    padding: 48px;
    position: relative;
    overflow: hidden;
    transition: all 0.35s ease;
    group: true;
  }

  .project-card::after {
    content: '';
    position: absolute; inset: 0;
    background: radial-gradient(circle at 80% 20%, rgba(0,229,255,0.06) 0%, transparent 60%);
    opacity: 0;
    transition: opacity 0.35s;
  }

  .project-card:hover::after { opacity: 1; }
  .project-card:hover { border-color: rgba(0,229,255,0.25); }

  .project-card.tall { grid-row: span 2; }

  .project-num {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    color: var(--muted);
    letter-spacing: 0.15em;
    margin-bottom: 32px;
    display: block;
  }

  .project-emoji { font-size: 2.5rem; margin-bottom: 24px; display: block; }

  .project-title {
    font-family: 'Syne', sans-serif;
    font-size: 1.5rem;
    font-weight: 800;
    line-height: 1.1;
    letter-spacing: -0.02em;
    margin-bottom: 16px;
  }

  .project-desc {
    font-size: 0.88rem;
    color: var(--muted);
    line-height: 1.75;
    margin-bottom: 32px;
  }

  .project-tags { display: flex; flex-wrap: wrap; gap: 8px; }
  .project-tag {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    padding: 4px 10px;
    background: rgba(0,229,255,0.08);
    border: 1px solid rgba(0,229,255,0.15);
    color: var(--cyan);
    letter-spacing: 0.05em;
  }

  .project-arrow {
    position: absolute; bottom: 48px; right: 48px;
    font-size: 1.4rem;
    color: var(--muted);
    transition: all 0.25s ease;
    transform: rotate(-45deg);
  }
  .project-card:hover .project-arrow { color: var(--cyan); transform: rotate(-45deg) scale(1.2); }

  /* EDUCATION */
  #education {
    padding: 120px 60px;
    border-top: 1px solid var(--border);
  }

  .edu-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 40px;
    margin-top: 64px;
  }

  .edu-card {
    border: 1px solid var(--border);
    padding: 40px;
    position: relative;
    background: var(--card);
    transition: all 0.3s;
    overflow: hidden;
  }

  .edu-card::before {
    content: attr(data-year);
    position: absolute;
    top: -10px; right: 24px;
    font-family: 'Syne', sans-serif;
    font-size: 5rem;
    font-weight: 800;
    color: rgba(0,229,255,0.04);
    line-height: 1;
    pointer-events: none;
  }

  .edu-card:hover { border-color: rgba(0,229,255,0.3); box-shadow: var(--glow); }

  .edu-icon { font-size: 2rem; margin-bottom: 20px; }

  .edu-degree {
    font-family: 'Syne', sans-serif;
    font-size: 1.2rem;
    font-weight: 800;
    margin-bottom: 8px;
    letter-spacing: -0.02em;
  }

  .edu-school {
    font-size: 0.9rem;
    color: var(--cyan);
    margin-bottom: 6px;
    font-weight: 500;
  }

  .edu-year {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.72rem;
    color: var(--muted);
    letter-spacing: 0.1em;
  }

  /* CONTACT */
  #contact {
    padding: 120px 60px;
    border-top: 1px solid var(--border);
    text-align: center;
    position: relative;
    overflow: hidden;
  }

  .contact-glow {
    position: absolute;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    width: 600px; height: 600px;
    background: radial-gradient(circle, rgba(0,229,255,0.06) 0%, transparent 70%);
    pointer-events: none;
  }

  .contact-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(44px, 8vw, 100px);
    font-weight: 800;
    letter-spacing: -0.04em;
    line-height: 0.9;
    margin-bottom: 32px;
    position: relative;
  }

  .contact-title .stroke {
    color: transparent;
    -webkit-text-stroke: 1.5px rgba(0,229,255,0.4);
  }

  .contact-sub {
    font-size: 1rem;
    color: var(--muted);
    max-width: 420px;
    margin: 0 auto 56px;
    font-weight: 300;
    line-height: 1.8;
  }

  .contact-links {
    display: flex;
    justify-content: center;
    gap: 16px;
    flex-wrap: wrap;
    margin-bottom: 60px;
  }

  .contact-link {
    display: flex; align-items: center; gap: 10px;
    padding: 16px 28px;
    border: 1px solid var(--border);
    color: var(--muted);
    text-decoration: none;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.78rem;
    letter-spacing: 0.05em;
    transition: all 0.25s ease;
    position: relative;
    overflow: hidden;
  }

  .contact-link::before {
    content: '';
    position: absolute; inset: 0;
    background: rgba(0,229,255,0.06);
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.3s ease;
  }
  .contact-link:hover::before { transform: scaleX(1); }
  .contact-link:hover { color: var(--cyan); border-color: rgba(0,229,255,0.3); }

  .contact-link .icon { font-size: 1rem; }

  /* FOOTER */
  footer {
    padding: 28px 60px;
    border-top: 1px solid var(--border);
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: relative; z-index: 1;
  }

  .footer-copy {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.68rem;
    color: var(--muted);
    letter-spacing: 0.08em;
  }

  .footer-status {
    display: flex; align-items: center; gap: 8px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.68rem;
    color: #4ade80;
    letter-spacing: 0.08em;
  }

  .status-dot {
    width: 6px; height: 6px;
    background: #4ade80;
    border-radius: 50%;
    animation: pulse 2s ease infinite;
  }

  @keyframes pulse {
    0%, 100% { opacity: 1; box-shadow: 0 0 0 0 rgba(74,222,128,0.4); }
    50% { opacity: 0.8; box-shadow: 0 0 0 6px rgba(74,222,128,0); }
  }

  /* KEYFRAMES */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }

  /* REVEAL ON SCROLL */
  .reveal {
    opacity: 0;
    transform: translateY(40px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible {
    opacity: 1;
    transform: none;
  }
  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }
  .reveal-delay-4 { transition-delay: 0.4s; }

  /* NOISE OVERLAY */
  .noise {
    position: fixed; inset: 0;
    z-index: 0;
    opacity: 0.025;
    pointer-events: none;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
    background-size: 128px 128px;
  }

  /* DIVIDER */
  .divider {
    width: 100%;
    height: 1px;
    background: linear-gradient(to right, transparent, var(--cyan), transparent);
    opacity: 0.2;
    margin: 0 60px;
    max-width: calc(100% - 120px);
  }

  /* RESPONSIVE */
  @media (max-width: 900px) {
    nav { padding: 20px 28px; }
    nav .nav-links { display: none; }
    #hero { padding: 100px 28px 80px; }
    #about { grid-template-columns: 1fr; padding: 80px 28px; }
    .about-visual { height: 320px; }
    #skills, #projects, #education, #contact { padding: 80px 28px; }
    .projects-grid { grid-template-columns: 1fr; }
    .project-card.tall { grid-row: auto; }
    .edu-grid { grid-template-columns: 1fr; }
    .hero-stats { display: none; }
    footer { padding: 24px 28px; }
  }

  /* TYPE CURSOR */
  .type-cursor {
    display: inline-block;
    width: 3px;
    height: 0.85em;
    background: var(--cyan);
    margin-left: 4px;
    vertical-align: middle;
    animation: blink 1.1s step-end infinite;
  }
  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>
<div class="noise"></div>
<canvas id="bg-canvas"></canvas>

<nav>
  <div class="nav-logo">MR<span>.</span></div>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#skills">Skills</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#education">Education</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-bg-text">MAYANK</div>
  <div class="hero-content">
    <div class="hero-tag">AI Developer & Creative Technologist</div>
    <h1 class="hero-name">
      Mayank<br>
      <span class="line2">Raj</span>
    </h1>
    <p class="hero-desc">Building AI-powered solutions at the intersection of data science, machine learning, and creative technology. Driven by curiosity, shipped through code.</p>
    <div class="hero-cta">
      <a href="#projects" class="btn-primary"><span>View Work</span></a>
      <a href="#contact" class="btn-ghost">Let's Collaborate</a>
    </div>
  </div>

  <div class="hero-scroll">
    <div class="scroll-line"></div>
    <span class="scroll-label">Scroll</span>
  </div>

  <div class="hero-stats">
    <div class="stat">
      <div class="stat-num" id="countSkills">14+</div>
      <div class="stat-label">Tech Skills</div>
    </div>
    <div class="stat">
      <div class="stat-num">∞</div>
      <div class="stat-label">Curiosity</div>
    </div>
    <div class="stat">
      <div class="stat-num">2025</div>
      <div class="stat-label">BSc AI Start</div>
    </div>
  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="about-visual">
    <div class="about-card card-main reveal">
      <div class="card-icon">🤖</div>
      <div class="card-title">AI & Machine Learning</div>
      <div class="card-desc">Supervised & unsupervised learning, classification, regression — building models that think.</div>
    </div>
    <div class="about-card card-float reveal reveal-delay-2">
      <div class="card-icon">📊</div>
      <div class="card-title">Data & Analytics</div>
      <div class="card-desc">EDA, Power BI dashboards, and visual storytelling from raw data.</div>
    </div>
    <div class="about-card card-accent reveal reveal-delay-3">
      <div class="card-icon">🎬</div>
      <div class="card-title">Creative Tech</div>
      <div class="card-desc">Video, content, brand design.</div>
    </div>
  </div>

  <div class="about-text-section">
    <div class="section-label reveal">About Me</div>
    <h2 class="section-title reveal reveal-delay-1">Built on <em>curiosity</em>,<br>wired for impact</h2>
    <p class="about-text reveal reveal-delay-2">An aspiring AI and Data Science professional who treats every project as a learning opportunity. I blend analytical precision with creative problem-solving — equally at home writing Python models and crafting visual narratives. Currently pursuing B.Sc. AI & Data Science at AAFT (2025–2028), building real-world skills alongside the curriculum.</p>
    <div class="about-tags reveal reveal-delay-3">
      <span class="tag">Python</span>
      <span class="tag">Machine Learning</span>
      <span class="tag">Power BI</span>
      <span class="tag">SQL</span>
      <span class="tag">Data Viz</span>
      <span class="tag">Video Editing</span>
      <span class="tag">Git & GitHub</span>
      <span class="tag">Automation</span>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="skills-header">
    <div>
      <div class="section-label reveal">What I Work With</div>
      <h2 class="section-title reveal reveal-delay-1">Technical<br><em>Toolkit</em></h2>
    </div>
  </div>

  <div class="skills-grid">
    <div class="skill-card reveal">
      <div class="skill-icon">🐍</div>
      <div class="skill-category">Language</div>
      <div class="skill-name">Python</div>
      <div class="skill-detail">Pandas · NumPy · Matplotlib · Seaborn</div>
    </div>
    <div class="skill-card reveal reveal-delay-1">
      <div class="skill-icon">🗄️</div>
      <div class="skill-category">Database</div>
      <div class="skill-name">SQL</div>
      <div class="skill-detail">MySQL · Oracle · MS SQL Server</div>
    </div>
    <div class="skill-card reveal reveal-delay-2">
      <div class="skill-icon">🧠</div>
      <div class="skill-category">AI / ML</div>
      <div class="skill-name">Machine Learning</div>
      <div class="skill-detail">Supervised & Unsupervised · Regression & Classification · Feature Engineering</div>
    </div>
    <div class="skill-card reveal reveal-delay-3">
      <div class="skill-icon">📈</div>
      <div class="skill-category">Analytics</div>
      <div class="skill-name">Power BI</div>
      <div class="skill-detail">Dashboards · Reports · DAX Basics · EDA</div>
    </div>
    <div class="skill-card reveal">
      <div class="skill-icon">🌐</div>
      <div class="skill-category">Frontend</div>
      <div class="skill-name">Web Dev</div>
      <div class="skill-detail">HTML · CSS · JavaScript · Bootstrap · Tailwind</div>
    </div>
    <div class="skill-card reveal reveal-delay-1">
      <div class="skill-icon">⚙️</div>
      <div class="skill-category">Dev Tools</div>
      <div class="skill-name">Dev Environment</div>
      <div class="skill-detail">Git & GitHub · Jupyter · Google Colab · VS Code · Anaconda</div>
    </div>
    <div class="skill-card reveal reveal-delay-2">
      <div class="skill-icon">📊</div>
      <div class="skill-category">Data Science</div>
      <div class="skill-name">Statistics & EDA</div>
      <div class="skill-detail">Model Evaluation · Performance Metrics · Data Preprocessing</div>
    </div>
    <div class="skill-card reveal reveal-delay-3">
      <div class="skill-icon">🎬</div>
      <div class="skill-category">Creative</div>
      <div class="skill-name">Content Creation</div>
      <div class="skill-detail">Video Editing · Brand Design · Visual Storytelling · Social Media</div>
    </div>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="section-label reveal">What I've Built</div>
  <h2 class="section-title reveal reveal-delay-1">Projects &<br><em>Experiments</em></h2>

  <div class="projects-grid">
    <div class="project-card tall reveal">
      <span class="project-num">001 — FEATURED</span>
      <span class="project-emoji">🤖</span>
      <div class="project-title">Mini AI & Python Automation Projects</div>
      <p class="project-desc">A series of hands-on Python and ML experiments focused on understanding core concepts through implementation — not just theory. Built automation scripts, explored datasets, and shipped small but complete builds that solve real problems.</p>
      <div class="project-tags">
        <span class="project-tag">Python</span>
        <span class="project-tag">NumPy</span>
        <span class="project-tag">Pandas</span>
        <span class="project-tag">Automation</span>
        <span class="project-tag">Jupyter</span>
      </div>
      <div class="project-arrow">↗</div>
    </div>

    <div class="project-card reveal reveal-delay-1">
      <span class="project-num">002</span>
      <span class="project-emoji">📊</span>
      <div class="project-title">Data Visualization & EDA</div>
      <p class="project-desc">Exploratory data analysis and dashboards using Python's visualization stack and Power BI — turning raw data into clear, insightful stories.</p>
      <div class="project-tags">
        <span class="project-tag">Matplotlib</span>
        <span class="project-tag">Seaborn</span>
        <span class="project-tag">Power BI</span>
        <span class="project-tag">EDA</span>
      </div>
      <div class="project-arrow">↗</div>
    </div>

    <div class="project-card reveal reveal-delay-2">
      <span class="project-num">003</span>
      <span class="project-emoji">🗄️</span>
      <div class="project-title">SQL Data Projects</div>
      <p class="project-desc">Structured queries, data modeling, and database exploration across MySQL, Oracle, and MS SQL Server for real-world data tasks.</p>
      <div class="project-tags">
        <span class="project-tag">MySQL</span>
        <span class="project-tag">Oracle</span>
        <span class="project-tag">MS SQL</span>
      </div>
      <div class="project-arrow">↗</div>
    </div>

    <div class="project-card reveal">
      <span class="project-num">004 — ONGOING</span>
      <span class="project-emoji">🎬</span>
      <div class="project-title">Creative & Content Portfolio</div>
      <p class="project-desc">Brand experiments, video editing, and digital content creation — proving that technical depth and creative vision aren't opposites.</p>
      <div class="project-tags">
        <span class="project-tag">Video Editing</span>
        <span class="project-tag">Brand Design</span>
        <span class="project-tag">Social Media</span>
      </div>
      <div class="project-arrow">↗</div>
    </div>
  </div>
</section>

<!-- EDUCATION -->
<section id="education">
  <div class="section-label reveal">Academic Journey</div>
  <h2 class="section-title reveal reveal-delay-1">Education &<br><em>Foundation</em></h2>

  <div class="edu-grid">
    <div class="edu-card reveal" data-year="2025">
      <div class="edu-icon">🎓</div>
      <div class="edu-degree">B.Sc. Artificial Intelligence & Data Science</div>
      <div class="edu-school">AAFT</div>
      <div class="edu-year">2025 — 2028 · IN PROGRESS</div>
    </div>
    <div class="edu-card reveal reveal-delay-1" data-year="12">
      <div class="edu-icon">📚</div>
      <div class="edu-degree">Class 10th & 12th</div>
      <div class="edu-school">David Model Senior Secondary School</div>
      <div class="edu-year">Completed</div>
    </div>
    <div class="edu-card reveal reveal-delay-2" data-year="∞">
      <div class="edu-icon">💡</div>
      <div class="edu-degree">Self-Learning & Projects</div>
      <div class="edu-school">Online Platforms & Personal Builds</div>
      <div class="edu-year">Ongoing · Always</div>
    </div>
    <div class="edu-card reveal reveal-delay-3" data-year="AI">
      <div class="edu-icon">🚀</div>
      <div class="edu-degree">Areas of Deep Interest</div>
      <div class="edu-school">AI/ML · Data Science · Automation · Creative Tech</div>
      <div class="edu-year">Continuously Expanding</div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="contact-glow"></div>
  <div class="section-label reveal" style="justify-content:center">Let's Talk</div>
  <h2 class="contact-title reveal reveal-delay-1">
    Let's build<br><span class="stroke">something.</span>
  </h2>
  <p class="contact-sub reveal reveal-delay-2">Open to internships, projects, collaborations, and any interesting learning opportunities. Always up for a conversation.</p>

  <div class="contact-links reveal reveal-delay-3">
    <a href="mailto:aayushraj3.4.2004@gmail.com" class="contact-link">
      <span class="icon">✉️</span> aayushraj3.4.2004@gmail.com
    </a>
    <a href="https://linkedin.com/in/mayank-raj" target="_blank" class="contact-link">
      <span class="icon">💼</span> linkedin.com/in/mayank-raj
    </a>
    <a href="https://github.com/TheMayankRaj" target="_blank" class="contact-link">
      <span class="icon">🐙</span> github.com/TheMayankRaj
    </a>
    <a href="tel:+919315500462" class="contact-link">
      <span class="icon">📞</span> +91-9315500462
    </a>
  </div>

  <a href="mailto:aayushraj3.4.2004@gmail.com" class="btn-primary reveal reveal-delay-4" style="display:inline-block"><span>Say Hello →</span></a>
</section>

<footer>
  <div class="footer-copy">© 2025 Mayank Raj. Designed & built with intention.</div>
  <div class="footer-status">
    <div class="status-dot"></div>
    Available for opportunities
  </div>
</footer>

<script>
  // CURSOR
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx + 'px';
    cursor.style.top = my + 'px';
  });

  function animateRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px';
    ring.style.top = ry + 'px';
    requestAnimationFrame(animateRing);
  }
  animateRing();

  document.querySelectorAll('a, button, .skill-card, .project-card, .edu-card, .tag').forEach(el => {
    el.addEventListener('mouseenter', () => { cursor.classList.add('hover'); ring.classList.add('hover'); });
    el.addEventListener('mouseleave', () => { cursor.classList.remove('hover'); ring.classList.remove('hover'); });
  });

  // CANVAS PARTICLE GRID
  const canvas = document.getElementById('bg-canvas');
  const ctx = canvas.getContext('2d');

  function resize() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  }
  resize();
  window.addEventListener('resize', resize);

  const COLS = Math.floor(window.innerWidth / 60);
  const ROWS = Math.floor(window.innerHeight / 60);
  let dots = [];
  let mouse = { x: -999, y: -999 };

  document.addEventListener('mousemove', e => { mouse.x = e.clientX; mouse.y = e.clientY; });

  for (let i = 0; i <= COLS; i++) {
    for (let j = 0; j <= ROWS; j++) {
      dots.push({
        x: (i / COLS) * window.innerWidth,
        y: (j / ROWS) * window.innerHeight,
        ox: (i / COLS) * window.innerWidth,
        oy: (j / ROWS) * window.innerHeight,
        size: Math.random() * 1.5 + 0.5,
        phase: Math.random() * Math.PI * 2,
        speed: Math.random() * 0.008 + 0.004
      });
    }
  }

  let t = 0;
  function drawCanvas() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    t += 0.5;

    dots.forEach(d => {
      const dx = mouse.x - d.ox;
      const dy = mouse.y - d.oy;
      const dist = Math.sqrt(dx * dx + dy * dy);
      const influence = Math.max(0, 1 - dist / 180);
      const push = influence * 20;

      d.x = d.ox - (dx / dist || 0) * push + Math.sin(t * d.speed + d.phase) * 3;
      d.y = d.oy - (dy / dist || 0) * push + Math.cos(t * d.speed + d.phase) * 3;

      const alpha = 0.08 + influence * 0.4;
      const size = d.size + influence * 2;

      ctx.beginPath();
      ctx.arc(d.x, d.y, size, 0, Math.PI * 2);
      ctx.fillStyle = `rgba(0, 229, 255, ${alpha})`;
      ctx.fill();
    });

    // Draw connecting lines between close dots
    for (let i = 0; i < dots.length; i++) {
      for (let j = i + 1; j < dots.length; j++) {
        const a = dots[i], b = dots[j];
        const dx = a.x - b.x, dy = a.y - b.y;
        const dist = Math.sqrt(dx * dx + dy * dy);
        if (dist < 65) {
          ctx.beginPath();
          ctx.moveTo(a.x, a.y);
          ctx.lineTo(b.x, b.y);
          ctx.strokeStyle = `rgba(0,229,255,${(1 - dist / 65) * 0.04})`;
          ctx.lineWidth = 0.5;
          ctx.stroke();
        }
      }
    }

    requestAnimationFrame(drawCanvas);
  }
  drawCanvas();

  // SCROLL REVEAL
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
      }
    });
  }, { threshold: 0.12 });

  reveals.forEach(el => observer.observe(el));

  // TYPING EFFECT in hero
  const heroName = document.querySelector('.hero-tag');
  const texts = ['AI Developer', 'Creative Technologist', 'Data Science Enthusiast', 'Problem Solver'];
  let textIdx = 0, charIdx = 0, deleting = false;
  const tagText = document.createElement('span');
  const cursor2 = document.createElement('span');
  cursor2.className = 'type-cursor';
  heroName.textContent = '';
  heroName.appendChild(tagText);
  heroName.appendChild(cursor2);

  function typeLoop() {
    const current = texts[textIdx];
    if (!deleting) {
      tagText.textContent = current.substring(0, charIdx + 1);
      charIdx++;
      if (charIdx === current.length) {
        deleting = true;
        setTimeout(typeLoop, 1800);
        return;
      }
    } else {
      tagText.textContent = current.substring(0, charIdx - 1);
      charIdx--;
      if (charIdx === 0) {
        deleting = false;
        textIdx = (textIdx + 1) % texts.length;
      }
    }
    setTimeout(typeLoop, deleting ? 40 : 80);
  }

  setTimeout(typeLoop, 1200);
</script>
</body>
</html>
