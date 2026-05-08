<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Parivallal J — Fullstack Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&display=swap" rel="stylesheet" />
<style>
  :root {
    --bg: #0a0c10;
    --surface: #111318;
    --surface2: #171b22;
    --border: rgba(255,255,255,0.07);
    --accent: #00e5ff;
    --accent2: #7c3aed;
    --accent3: #10b981;
    --text: #e8eaf0;
    --muted: #6b7280;
    --tag-bg: rgba(0,229,255,0.08);
  }
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-size: 15px;
    line-height: 1.7;
    overflow-x: hidden;
  }

  /* ── GRID BACKGROUND ─────────────────────────────────────── */
  body::before {
    content: '';
    position: fixed; inset: 0; z-index: 0; pointer-events: none;
    background-image:
      linear-gradient(rgba(0,229,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,229,255,0.03) 1px, transparent 1px);
    background-size: 48px 48px;
  }

  /* ── NOISE TEXTURE ──────────────────────────────────────── */
  body::after {
    content: '';
    position: fixed; inset: 0; z-index: 0; pointer-events: none;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    opacity: 0.5;
  }

  .container {
    max-width: 900px;
    margin: 0 auto;
    padding: 0 24px;
    position: relative; z-index: 1;
  }

  /* ── HEADER ─────────────────────────────────────────────── */
  header {
    padding: 80px 0 60px;
    position: relative;
  }

  .glow-blob {
    position: absolute;
    top: -120px; left: -200px;
    width: 600px; height: 600px;
    background: radial-gradient(circle, rgba(0,229,255,0.06) 0%, transparent 70%);
    pointer-events: none;
    border-radius: 50%;
  }

  .eyebrow {
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    letter-spacing: 0.2em;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 16px;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards;
  }

  h1 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(48px, 8vw, 88px);
    font-weight: 800;
    line-height: 0.95;
    letter-spacing: -0.03em;
    color: #fff;
    opacity: 0;
    animation: fadeUp 0.6s 0.1s ease forwards;
  }

  h1 span {
    background: linear-gradient(135deg, var(--accent) 0%, var(--accent2) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .tagline {
    margin-top: 20px;
    font-size: 17px;
    color: var(--muted);
    max-width: 520px;
    opacity: 0;
    animation: fadeUp 0.6s 0.2s ease forwards;
  }

  .meta-row {
    margin-top: 28px;
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
    opacity: 0;
    animation: fadeUp 0.6s 0.3s ease forwards;
  }

  .badge {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 6px 14px;
    border-radius: 100px;
    border: 1px solid var(--border);
    background: var(--surface);
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    color: var(--muted);
    text-decoration: none;
    transition: border-color 0.2s, color 0.2s;
  }
  .badge:hover { border-color: var(--accent); color: var(--accent); }
  .badge .dot { width: 6px; height: 6px; border-radius: 50%; background: var(--accent3); }

  /* ── SECTION TITLES ──────────────────────────────────────── */
  section { padding: 60px 0; }

  .sec-label {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 32px;
    display: flex; align-items: center; gap: 12px;
  }
  .sec-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  h2 {
    font-family: 'Syne', sans-serif;
    font-size: 28px;
    font-weight: 700;
    color: #fff;
    margin-bottom: 8px;
  }

  /* ── SUMMARY CARD ────────────────────────────────────────── */
  .summary-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 32px;
    position: relative;
    overflow: hidden;
  }
  .summary-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
  }
  .summary-card p {
    color: #adb5c8;
    font-size: 15.5px;
    line-height: 1.8;
  }
  .summary-card p + p { margin-top: 12px; }

  /* ── SKILLS GRID ─────────────────────────────────────────── */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
    gap: 16px;
  }

  .skill-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 24px;
    transition: border-color 0.2s, transform 0.2s;
  }
  .skill-card:hover { border-color: rgba(0,229,255,0.25); transform: translateY(-2px); }

  .skill-card-title {
    font-family: 'Syne', sans-serif;
    font-size: 13px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--accent);
    margin-bottom: 14px;
  }

  .tag-cloud { display: flex; flex-wrap: wrap; gap: 8px; }

  .tag {
    background: var(--tag-bg);
    border: 1px solid rgba(0,229,255,0.12);
    border-radius: 6px;
    padding: 4px 10px;
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    color: #9bb8c9;
  }
  .tag.hot { background: rgba(124,58,237,0.12); border-color: rgba(124,58,237,0.2); color: #b49de8; }
  .tag.green { background: rgba(16,185,129,0.1); border-color: rgba(16,185,129,0.18); color: #6ee7b7; }

  /* ── EXPERIENCE ──────────────────────────────────────────── */
  .exp-list { display: flex; flex-direction: column; gap: 24px; }

  .exp-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 28px 32px;
    position: relative;
    transition: border-color 0.2s;
  }
  .exp-card:hover { border-color: rgba(0,229,255,0.2); }

  .exp-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 6px;
  }

  .exp-role {
    font-family: 'Syne', sans-serif;
    font-size: 18px;
    font-weight: 700;
    color: #fff;
  }

  .exp-period {
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    color: var(--accent);
    background: var(--tag-bg);
    border: 1px solid rgba(0,229,255,0.15);
    border-radius: 100px;
    padding: 3px 12px;
    white-space: nowrap;
  }

  .exp-company {
    font-size: 13px;
    color: var(--muted);
    margin-bottom: 16px;
  }

  .exp-card ul {
    padding-left: 0;
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 8px;
  }
  .exp-card ul li {
    padding-left: 20px;
    position: relative;
    color: #9aa3b4;
    font-size: 14px;
    line-height: 1.6;
  }
  .exp-card ul li::before {
    content: '▸';
    position: absolute;
    left: 0;
    color: var(--accent);
    font-size: 10px;
    top: 4px;
  }

  .exp-stack {
    margin-top: 16px;
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
  }

  /* ── ACHIEVEMENTS ────────────────────────────────────────── */
  .ach-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(210px, 1fr));
    gap: 14px;
  }

  .ach-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 22px 20px;
    transition: border-color 0.2s, transform 0.2s;
    display: flex;
    flex-direction: column;
    gap: 8px;
  }
  .ach-card:hover { border-color: rgba(16,185,129,0.3); transform: translateY(-2px); }

  .ach-metric {
    font-family: 'Syne', sans-serif;
    font-size: 32px;
    font-weight: 800;
    background: linear-gradient(135deg, var(--accent3), var(--accent));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    line-height: 1;
  }

  .ach-desc {
    font-size: 13px;
    color: var(--muted);
    line-height: 1.5;
  }

  /* ── FOOTER ──────────────────────────────────────────────── */
  footer {
    border-top: 1px solid var(--border);
    padding: 40px 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 16px;
  }

  .footer-name {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    color: #fff;
    font-size: 16px;
  }

  .footer-links { display: flex; gap: 12px; }

  .cta-btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 10px 22px;
    border-radius: 100px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    color: #000;
    font-family: 'Syne', sans-serif;
    font-size: 13px;
    font-weight: 700;
    text-decoration: none;
    transition: opacity 0.2s, transform 0.2s;
  }
  .cta-btn:hover { opacity: 0.88; transform: translateY(-1px); }

  /* ── DIVIDER ─────────────────────────────────────────────── */
  .divider { height: 1px; background: var(--border); margin: 0; }

  /* ── ANIMATIONS ──────────────────────────────────────────── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(18px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .reveal {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.55s ease, transform 0.55s ease;
  }
  .reveal.visible { opacity: 1; transform: none; }

  /* ── OPEN TO WORK PILL ───────────────────────────────────── */
  .otw {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 6px 16px;
    border-radius: 100px;
    background: rgba(16,185,129,0.1);
    border: 1px solid rgba(16,185,129,0.25);
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    color: var(--accent3);
    margin-bottom: 20px;
    opacity: 0;
    animation: fadeUp 0.6s 0s ease forwards;
  }
  .otw-dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: var(--accent3);
    box-shadow: 0 0 6px var(--accent3);
    animation: pulse 2s infinite;
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.3; }
  }

  /* ── RESPONSIVE ──────────────────────────────────────────── */
  @media (max-width: 600px) {
    header { padding: 52px 0 40px; }
    .exp-card { padding: 22px 20px; }
    .ach-grid { grid-template-columns: 1fr 1fr; }
    footer { flex-direction: column; align-items: flex-start; }
  }
</style>
</head>
<body>

<!-- ── HEADER ────────────────────────────────────────────── -->
<header>
  <div class="container">
    <div class="glow-blob"></div>

    <div class="otw">
      <div class="otw-dot"></div>
      Open to Opportunities
    </div>

    <p class="eyebrow">Fullstack Developer · AI/LLM Integration · Cloud & DevOps</p>
    <h1>Parivallal <span>J</span></h1>
    <p class="tagline">Building high-performance, AI-powered web applications — from responsive frontends to serverless cloud infrastructure.</p>

    <div class="meta-row">
      <a href="mailto:parivallalj56@gmail.com" class="badge">✉ parivallalj56@gmail.com</a>
      <a href="https://github.com/parivallaljv" target="_blank" class="badge">⌥ github.com/parivallaljv</a>
      <span class="badge"><span class="dot"></span> Chennai, India</span>
    </div>
  </div>
</header>

<div class="divider"></div>

<!-- ── SUMMARY ────────────────────────────────────────────── -->
<section>
  <div class="container">
    <p class="sec-label reveal">About</p>
    <div class="summary-card reveal">
      <p>Results-driven Full Stack Developer with <strong style="color:#e8eaf0">2.5+ years</strong> of professional experience building high-performance web applications using <strong style="color:#e8eaf0">React.js, Next.js, TypeScript, Node.js, Express.js,</strong> and <strong style="color:#e8eaf0">Python (FastAPI, SQLAlchemy, Pydantic)</strong>. Proficient across the entire stack, creating scalable, responsive, and user-friendly applications.</p>
      <p>Deep hands-on experience integrating <strong style="color:var(--accent)">Claude API (Anthropic)</strong> and building <strong style="color:var(--accent)">RAG pipelines</strong>. Strong AWS expertise across Lambda, DynamoDB, S3, Cognito, Amplify, and CloudFormation. Actively leverages <strong style="color:var(--accent)">Claude Code, Cursor AI, and GitHub Copilot</strong> to accelerate development velocity.</p>
    </div>
  </div>
</section>

<!-- ── ACHIEVEMENTS ───────────────────────────────────────── -->
<section>
  <div class="container">
    <p class="sec-label reveal">Impact</p>
    <div class="ach-grid">
      <div class="ach-card reveal"><div class="ach-metric">−40%</div><div class="ach-desc">API latency via AI call caching</div></div>
      <div class="ach-card reveal"><div class="ach-metric">−60%</div><div class="ach-desc">Deployment time with Docker + Jenkins CI/CD</div></div>
      <div class="ach-card reveal"><div class="ach-metric">+35%</div><div class="ach-desc">User engagement from social API integrations</div></div>
      <div class="ach-card reveal"><div class="ach-metric">+40%</div><div class="ach-desc">Onboarding improvement via gamification flows</div></div>
      <div class="ach-card reveal"><div class="ach-metric">−45%</div><div class="ach-desc">Production bugs with Cypress + pytest E2E testing</div></div>
      <div class="ach-card reveal"><div class="ach-metric">−30%</div><div class="ach-desc">API response times via Node.js + DB optimization</div></div>
      <div class="ach-card reveal"><div class="ach-metric">+25%</div><div class="ach-desc">User upgrades from Pro features & leaderboards</div></div>
      <div class="ach-card reveal"><div class="ach-metric">RAG</div><div class="ach-desc">Context-aware AI content generation pipeline</div></div>
    </div>
  </div>
</section>

<!-- ── SKILLS ─────────────────────────────────────────────── -->
<section>
  <div class="container">
    <p class="sec-label reveal">Tech Stack</p>
    <div class="skills-grid">
      <div class="skill-card reveal">
        <div class="skill-card-title">Frontend</div>
        <div class="tag-cloud">
          <span class="tag">React.js</span><span class="tag">Next.js</span><span class="tag">Redux</span>
          <span class="tag">TypeScript</span><span class="tag">JavaScript ES6+</span>
          <span class="tag">Tailwind CSS</span><span class="tag">Radix UI</span><span class="tag">Hero UI</span>
          <span class="tag">HTML5 / CSS3</span>
        </div>
      </div>
      <div class="skill-card reveal">
        <div class="skill-card-title">Backend</div>
        <div class="tag-cloud">
          <span class="tag">Node.js</span><span class="tag">Express.js</span>
          <span class="tag hot">Python</span><span class="tag hot">FastAPI</span>
          <span class="tag hot">Pydantic</span><span class="tag hot">Mangum</span>
          <span class="tag">SQLAlchemy</span>
          <span class="tag">MongoDB</span><span class="tag">PostgreSQL</span><span class="tag">MySQL</span><span class="tag">DynamoDB</span>
        </div>
      </div>
      <div class="skill-card reveal">
        <div class="skill-card-title">Cloud & DevOps</div>
        <div class="tag-cloud">
          <span class="tag">AWS Lambda</span><span class="tag">S3</span><span class="tag">Cognito</span>
          <span class="tag">API Gateway</span><span class="tag">Amplify</span>
          <span class="tag">CloudWatch</span><span class="tag">CloudFormation</span>
          <span class="tag">Serverless Framework</span>
          <span class="tag">Docker</span><span class="tag">Jenkins</span><span class="tag">GitHub Actions</span>
        </div>
      </div>
      <div class="skill-card reveal">
        <div class="skill-card-title">AI & LLM</div>
        <div class="tag-cloud">
          <span class="tag green">Claude API</span><span class="tag green">Claude Code</span>
          <span class="tag green">RAG Pipelines</span><span class="tag green">Prompt Engineering</span>
          <span class="tag green">OpenAI API</span>
          <span class="tag green">Vector / Embeddings</span>
          <span class="tag">Cursor AI</span><span class="tag">GitHub Copilot</span>
        </div>
      </div>
      <div class="skill-card reveal">
        <div class="skill-card-title">Tools & Methods</div>
        <div class="tag-cloud">
          <span class="tag">Git / GitHub / BitBucket</span>
          <span class="tag">JIRA</span><span class="tag">Agile / Scrum</span>
          <span class="tag">Cypress</span><span class="tag">pytest</span>
          <span class="tag">Apollo Client</span><span class="tag">Next Auth</span>
          <span class="tag">VS Code</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ── EXPERIENCE ─────────────────────────────────────────── -->
<section>
  <div class="container">
    <p class="sec-label reveal">Experience</p>
    <div class="exp-list">

      <!-- Data DNA – PwC -->
      <div class="exp-card reveal">
        <div class="exp-header">
          <div class="exp-role">Fullstack Developer — PwC Admin Portal</div>
          <span class="exp-period">Mar 2026 – Present</span>
        </div>
        <div class="exp-company">Data DNA, Chennai · partnered with Alpine Strategies, US</div>
        <ul>
          <li>Maintaining and enhancing an enterprise admin portal with RBAC supporting Organizations, Regions, Brands, Rules, and Users (Org Admin, Region Admin, Brand Admin, User Admin).</li>
          <li>Building features with Next.js App Router, Radix UI, Apollo Client, and Redux for a performant, type-safe frontend.</li>
          <li>Developing Python FastAPI backend with SQLAlchemy ORM, Pydantic schemas, and Mangum as the AWS Lambda adapter.</li>
          <li>Managing deployments via GitHub Actions CI/CD pipelines to AWS Amplify and Lambda.</li>
          <li>Implemented shell script automation to streamline code migration between GitHub (dev) and Azure Repo (client) — eliminating manual file-copy handoffs and reducing errors.</li>
          <li>Leveraging Claude Code, Cursor AI (Plan, Ask, Debug, Agent mode), and GitHub Copilot for AI-assisted development.</li>
        </ul>
        <div class="exp-stack">
          <span class="tag">Next.js App Router</span><span class="tag">Next Auth</span><span class="tag">Radix UI</span>
          <span class="tag">Apollo Client</span><span class="tag">Redux</span>
          <span class="tag hot">Python FastAPI</span><span class="tag hot">SQLAlchemy</span><span class="tag hot">Pydantic</span><span class="tag hot">Mangum</span>
          <span class="tag">AWS Lambda</span><span class="tag">Amplify</span><span class="tag">GitHub Actions</span>
          <span class="tag green">Claude Code</span><span class="tag green">Cursor AI</span>
        </div>
      </div>

      <!-- Data DNA – Test Series -->
      <div class="exp-card reveal">
        <div class="exp-header">
          <div class="exp-role">Fullstack Developer — Test Series Platform</div>
          <span class="exp-period">Jan 2026 – Feb 2026</span>
        </div>
        <div class="exp-company">Data DNA, Chennai · partnered with Alpine Strategies, US</div>
        <ul>
          <li>Built role-based dashboards for Student, Teacher, and Admin portals — including assessment generator, adaptive content generator, and full authentication flows.</li>
          <li>Built AI-powered learning features — sticky notes, ready reckoners, mind maps, and diagrammatic representations — using RAG pipeline via Python FastAPI integrated with Claude and OpenAI APIs.</li>
          <li>Engineered a dynamic question paper generator (unit test, quarterly, half-yearly, annual) with rich customization options.</li>
          <li>Implemented secure login flows using AWS Cognito with JWT token-based API authentication validated in FastAPI middleware.</li>
          <li>Refactored Python/FastAPI codebase into a structured, modular architecture for long-term maintainability.</li>
        </ul>
        <div class="exp-stack">
          <span class="tag">React.js</span><span class="tag">TypeScript</span><span class="tag">Redux</span><span class="tag">Hero UI</span>
          <span class="tag hot">FastAPI</span><span class="tag hot">Pydantic</span><span class="tag hot">Serverless Framework</span>
          <span class="tag">AWS Lambda</span><span class="tag">DynamoDB</span><span class="tag">Cognito</span><span class="tag">CloudFormation</span>
          <span class="tag green">RAG</span><span class="tag green">Claude API</span><span class="tag green">Prompt Engineering</span>
        </div>
      </div>

      <!-- Experience.com -->
      <div class="exp-card reveal">
        <div class="exp-header">
          <div class="exp-role">Fullstack Developer</div>
          <span class="exp-period">Jun 2023 – Dec 2025</span>
        </div>
        <div class="exp-company">Experience.com · Product-Based Company, Chennai</div>
        <ul>
          <li>Built responsive React.js interfaces using Redux, TypeScript, and Tailwind CSS with reusable component patterns and integrated RESTful APIs via Axios in Agile sprints.</li>
          <li>Developed international expansion features using Google Maps API and libphonenumber-js for address and phone validation across regions.</li>
          <li>Integrated Google, Facebook, and Instagram APIs via Node.js to let users create and manage social posts within the platform — driving a 35% uplift in engagement.</li>
          <li>Delivered Pro features including rank previews, reviews, and leaderboards, contributing to a 25% boost in user upgrades.</li>
          <li>Added gamification features and onboarding flows using React Hooks and TypeScript, improving onboarding completion by 40%.</li>
          <li>Improved SEO via structured metadata, dynamic routing, and server-side rendering with Next.js.</li>
          <li>Set up CI/CD pipelines with GitHub, Jenkins, and Docker; E2E tests with Cypress — reducing production bugs by 45%.</li>
        </ul>
        <div class="exp-stack">
          <span class="tag">React.js</span><span class="tag">Next.js</span><span class="tag">Redux</span>
          <span class="tag">TypeScript</span><span class="tag">Tailwind CSS</span>
          <span class="tag">Node.js</span><span class="tag">Express.js</span>
          <span class="tag">MongoDB</span><span class="tag">MySQL</span><span class="tag">AWS S3</span>
          <span class="tag">Docker</span><span class="tag">Jenkins</span><span class="tag">Cypress</span>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- ── EDUCATION ──────────────────────────────────────────── -->
<section>
  <div class="container">
    <p class="sec-label reveal">Education</p>
    <div class="exp-card reveal" style="max-width:460px">
      <div class="exp-header">
        <div class="exp-role">Bachelor of Engineering</div>
        <span class="exp-period">2017 – 2021</span>
      </div>
      <div class="exp-company">Anna University (Affiliated), Tamil Nadu</div>
    </div>
  </div>
</section>

<!-- ── FOOTER ─────────────────────────────────────────────── -->
<div class="divider"></div>
<footer>
  <div class="container" style="display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:16px; width:100%">
    <div>
      <div class="footer-name">Parivallal J</div>
      <div style="font-size:13px; color:var(--muted); margin-top:2px">Open to full-time opportunities</div>
    </div>
    <div class="footer-links">
      <a href="mailto:parivallalj56@gmail.com" class="badge">✉ Email</a>
      <a href="https://github.com/parivallaljv" target="_blank" class="badge">⌥ GitHub</a>
      <a href="mailto:parivallalj56@gmail.com" class="cta-btn">Let's Talk →</a>
    </div>
  </div>
</footer>

<script>
  // Intersection Observer for reveal animations
  const obs = new IntersectionObserver((entries) => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        setTimeout(() => e.target.classList.add('visible'), i * 60);
        obs.unobserve(e.target);
      }
    });
  }, { threshold: 0.08 });

  document.querySelectorAll('.reveal').forEach(el => obs.observe(el));
</script>
</body>
</html>
