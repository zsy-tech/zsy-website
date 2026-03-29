<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Zhou Siyu 周思鈺</title>
<link href="https://fonts.googleapis.com/css2?family=EB+Garamond:ital,wght@0,400;0,500;1,400&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --ink: #1a1814;
    --paper: #f4f0e8;
    --muted: #8a8478;
    --accent: #c8b89a;
    --red: #8b3a2a;
  }

  html { font-size: 16px; }

  body {
    background: var(--paper);
    color: var(--ink);
    font-family: 'EB Garamond', Georgia, serif;
    min-height: 100vh;
    cursor: crosshair;
    overflow-x: hidden;
  }

  /* GRAIN OVERLAY */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1000;
    opacity: 0.4;
  }

  /* NAV */
  nav {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 100;
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    padding: 1.4rem 2.4rem;
    mix-blend-mode: multiply;
  }

  .nav-name {
    font-family: 'Space Mono', monospace;
    font-size: 0.72rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--ink);
    text-decoration: none;
  }

  .nav-links {
    display: flex;
    gap: 2rem;
    list-style: none;
  }

  .nav-links a {
    font-family: 'Space Mono', monospace;
    font-size: 0.65rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--muted);
    text-decoration: none;
    transition: color 0.2s;
  }

  .nav-links a:hover { color: var(--ink); }

  /* HERO */
  .hero {
    min-height: 100vh;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr auto;
    padding: 6rem 2.4rem 3rem;
    position: relative;
  }

  .hero-text {
    grid-column: 1;
    grid-row: 1;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    padding-bottom: 4rem;
  }

  .hero-tagline {
    font-size: clamp(2.2rem, 4vw, 3.6rem);
    line-height: 1.15;
    font-weight: 400;
    font-style: italic;
    max-width: 18ch;
    opacity: 0;
    transform: translateY(20px);
    animation: fadeUp 1.2s ease forwards 0.3s;
  }

  .hero-sub {
    margin-top: 2rem;
    font-family: 'Space Mono', monospace;
    font-size: 0.68rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--muted);
    opacity: 0;
    animation: fadeUp 1s ease forwards 0.7s;
  }

  .hero-sub span {
    display: block;
    margin-top: 0.4rem;
  }

  .hero-image {
    grid-column: 2;
    grid-row: 1 / 3;
    position: relative;
    overflow: hidden;
    opacity: 0;
    animation: fadeIn 1.4s ease forwards 0.5s;
  }

  .hero-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    filter: grayscale(30%) contrast(1.05);
    mix-blend-mode: multiply;
  }

  .hero-image-caption {
    position: absolute;
    bottom: 1.2rem;
    right: 1.2rem;
    font-family: 'Space Mono', monospace;
    font-size: 0.58rem;
    letter-spacing: 0.1em;
    color: var(--paper);
    text-transform: uppercase;
    mix-blend-mode: difference;
  }

  /* BANYAN TEXT SECTION */
  .banyan {
    padding: 8rem 2.4rem;
    display: grid;
    grid-template-columns: 1fr 2fr;
    gap: 4rem;
    border-top: 1px solid var(--accent);
  }

  .banyan-label {
    font-family: 'Space Mono', monospace;
    font-size: 0.62rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--muted);
    padding-top: 0.3rem;
  }

  .banyan-text {
    font-size: 1.18rem;
    line-height: 1.85;
    color: var(--ink);
  }

  .banyan-text p + p {
    margin-top: 1.4em;
  }

  .banyan-text em {
    font-style: italic;
    color: var(--red);
  }

  /* FRAGMENTS GRID */
  .fragments {
    padding: 6rem 2.4rem;
    border-top: 1px solid var(--accent);
  }

  .fragments-header {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    margin-bottom: 4rem;
  }

  .fragments-title {
    font-size: 0.62rem;
    font-family: 'Space Mono', monospace;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--muted);
  }

  .fragments-count {
    font-family: 'Space Mono', monospace;
    font-size: 0.62rem;
    color: var(--accent);
  }

  .fragments-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 0;
  }

  .fragment {
    border: 1px solid var(--accent);
    margin: -1px 0 0 -1px;
    padding: 2.4rem;
    transition: background 0.3s;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }

  .fragment::after {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--ink);
    opacity: 0;
    transition: opacity 0.3s;
  }

  .fragment:hover::after { opacity: 0.04; }

  .fragment-number {
    font-family: 'Space Mono', monospace;
    font-size: 0.58rem;
    color: var(--accent);
    letter-spacing: 0.1em;
    margin-bottom: 1.4rem;
  }

  .fragment-title {
    font-size: 1.4rem;
    font-style: italic;
    line-height: 1.2;
    margin-bottom: 1rem;
  }

  .fragment-chinese {
    font-size: 1rem;
    color: var(--muted);
    margin-bottom: 1.4rem;
  }

  .fragment-desc {
    font-family: 'Space Mono', monospace;
    font-size: 0.6rem;
    letter-spacing: 0.08em;
    color: var(--muted);
    line-height: 1.7;
  }

  /* COORDINATES */
  .coordinates {
    padding: 6rem 2.4rem 4rem;
    border-top: 1px solid var(--accent);
    display: grid;
    grid-template-columns: 2fr 1fr;
    gap: 4rem;
    align-items: end;
  }

  .coordinates-text {
    font-size: 1.05rem;
    line-height: 1.9;
    color: var(--muted);
    font-style: italic;
  }

  .coordinates-contact {
    font-family: 'Space Mono', monospace;
    font-size: 0.62rem;
    letter-spacing: 0.1em;
    line-height: 2.2;
  }

  .coordinates-contact a {
    color: var(--ink);
    text-decoration: none;
    display: block;
    transition: color 0.2s;
  }

  .coordinates-contact a:hover { color: var(--red); }

  .coordinates-contact .label {
    color: var(--muted);
    font-size: 0.55rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    display: block;
    margin-top: 1rem;
  }

  /* FOOTER */
  footer {
    padding: 1.4rem 2.4rem;
    border-top: 1px solid var(--accent);
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  footer span {
    font-family: 'Space Mono', monospace;
    font-size: 0.58rem;
    letter-spacing: 0.1em;
    color: var(--muted);
    text-transform: uppercase;
  }

  /* FLOATING DATE */
  .floating-date {
    position: fixed;
    bottom: 2rem;
    left: 2.4rem;
    font-family: 'Space Mono', monospace;
    font-size: 0.58rem;
    letter-spacing: 0.1em;
    color: var(--muted);
    text-transform: uppercase;
    z-index: 50;
    writing-mode: vertical-lr;
    transform: rotate(180deg);
  }

  /* SCROLL LINE */
  .scroll-indicator {
    position: fixed;
    right: 2.4rem;
    top: 50%;
    transform: translateY(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.4rem;
    z-index: 50;
  }

  .scroll-line {
    width: 1px;
    height: 60px;
    background: var(--accent);
    transform-origin: top;
    animation: scrollPulse 2s ease-in-out infinite;
  }

  @keyframes scrollPulse {
    0%, 100% { opacity: 0.3; transform: scaleY(1); }
    50% { opacity: 1; transform: scaleY(0.6); }
  }

  /* ANIMATIONS */
  @keyframes fadeUp {
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes fadeIn {
    to { opacity: 1; }
  }

  /* RESPONSIVE */
  @media (max-width: 768px) {
    .hero { grid-template-columns: 1fr; padding-top: 8rem; }
    .hero-image { grid-column: 1; grid-row: 2; height: 60vw; margin-top: 2rem; }
    .banyan { grid-template-columns: 1fr; gap: 2rem; }
    .fragments-grid { grid-template-columns: 1fr; }
    .coordinates { grid-template-columns: 1fr; }
    .scroll-indicator { display: none; }
  }
</style>
</head>
<body>

<nav>
  <a href="#" class="nav-name">Zhou Siyu 周思鈺</a>
  <ul class="nav-links">
    <li><a href="#work">Work</a></li>
    <li><a href="#fragments">Field</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<div class="floating-date">Ruili — Zürich — 2024–2026</div>

<div class="scroll-indicator">
  <div class="scroll-line"></div>
</div>

<!-- HERO -->
<section class="hero">
  <div class="hero-text">
    <h1 class="hero-tagline">Fragments of migration. Working across scales.</h1>
    <div class="hero-sub">
      <span>Anthropology · Ethnographic Writing</span>
      <span>University of Zurich</span>
    </div>
</section>

<!-- BANYAN -->
<section class="banyan" id="work">
  <div class="banyan-label">On Ruili</div>
  <div class="banyan-text">
    <p>As a banyan tree grows, its branches send down aerial roots — roots that hang suspended in the air until they touch the ground, take hold, and thicken into new trunks. This quality makes the banyan one of the most invasive of plants. It strangles everything around it: bodhi trees, banana trees, rubber trees, and, given time, temples and drainage ditches alike.</p>
    <p>This is why the streets of Ruili were planted with palm trees instead. Yet the banyan's strangling force prevailed regardless — birds carried its seeds into the humus collecting at the crowns of the palms, and the banyan quietly reclaimed the streets, <em>one palm tree at a time.</em></p>
    <p>It is said that the Buddha attained enlightenment beneath a great banyan tree. They place Buddha statues at the foot of century-old trees. Over time, the banyan — making no distinctions — slowly engulfs the statues. People come to worship the Buddha. They end up worshipping the tree as well.</p>
  </div>
</section>

<!-- FRAGMENTS -->
<section class="fragments" id="fragments">
  <div class="fragments-header">
    <span class="fragments-title">Field fragments</span>
    <span class="fragments-count">04 entries</span>
  </div>
  <div class="fragments-grid">
    <div class="fragment">
      <div class="fragment-number">001</div>
      <div class="fragment-title">A blank patch on the map</div>
      <div class="fragment-chinese">迷雾</div>
      <div class="fragment-desc">On my electric scooter, I rode into a blank patch on the map. Ahead, small clusters of people — girls with white stripes painted across their cheeks.</div>
    </div>
    <div class="fragment">
      <div class="fragment-number">002</div>
      <div class="fragment-title">Only our own hands</div>
      <div class="fragment-chinese">双手</div>
      <div class="fragment-desc">She never buys chicken. The workers only have chicken in the canteen. They don't want to eat chicken at restaurants during their time off.</div>
    </div>
    <div class="fragment">
      <div class="fragment-number">003</div>
      <div class="fragment-title">22.3.2026</div>
      <div class="fragment-chinese">日记</div>
      <div class="fragment-desc">Mama, it has been 18 years since I left home. Seven of those years I have not returned. I want to go back. I want to come back to you.</div>
    </div>
    <div class="fragment">
      <div class="fragment-number">004</div>
      <div class="fragment-title">The wrong ID</div>
      <div class="fragment-chinese">无名</div>
      <div class="fragment-desc">She died on the 14th from a heart condition. Her body is in cold storage. We cannot find her family. Her ID card has incorrect information.</div>
    </div>
  </div>
</section>

<!-- COORDINATES -->
<section class="coordinates" id="contact">
  <div class="coordinates-text">
    "Resilient Meshworks in the Shadow of the Wall: Undocumented Myanmar Workers' Collective Imaginaries of Alternative Futures in Border China"
  </div>
  <div class="coordinates-contact">
    <span class="label">Contact</span>
    <a href="mailto:siyu.zhou@uzh.ch">siyu.zhou@uzh.ch</a>
    <span class="label">Instagram</span>
    <a href="https://instagram.com/zhousiyu207">@zhousiyu207</a>
    <span class="label">Institution</span>
    <a href="#">University of Zurich</a>
  </div>
</section>

<footer>
  <span>Zhou Siyu 周思鈺 — 2026</span>
  <span>Fragments of migration</span>
</footer>

</body>
</html>
