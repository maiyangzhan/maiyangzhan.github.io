# Apple UI Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the dark-tech Bootstrap theme on all 7 HTML pages with the Apple design language from DESIGN.md, using a shared `apple.css` stylesheet.

**Architecture:** Create one shared `apple.css` that overrides Bootstrap's dark theme with Apple tokens (white/parchment/near-black tile surfaces, single Action Blue #0066cc, no gradients, 17px body text). Each HTML page removes its `data-bs-theme="dark"` attribute and inline `<style>` block, links `apple.css`, and gets its HTML structure updated to use the tile/component classes.

**Tech Stack:** HTML5, Bootstrap 5.3.2 (kept for grid + collapse), Bootstrap Icons, custom CSS (apple.css)

---

## File Structure

| Action  | File                                       | Purpose                              |
|---------|--------------------------------------------|--------------------------------------|
| Create  | `apple.css`                                | Shared design system stylesheet      |
| Rewrite | `index.html`                               | Homepage — hero + blog preview + about tiles |
| Rewrite | `blogs.html`                               | Blog list page                       |
| Rewrite | `about_me.html`                            | About page                           |
| Rewrite | `blogs/neovim install.html`                | Blog post — article wrapper updated  |
| Rewrite | `blogs/tmux install without root.html`     | Blog post — article wrapper updated  |
| Rewrite | `blogs/linux terminal clash.html`          | Blog post — article wrapper updated  |
| Rewrite | `blogs/openclaw-macos-deploy.html`         | Blog post — article wrapper updated  |

---

## Task 1: Create apple.css

**Files:**
- Create: `apple.css`

- [ ] **Step 1: Write apple.css**

```css
/* ===========================================
   apple.css — Apple Design Language Override
   =========================================== */

/* --- Tokens --- */
:root {
  --color-canvas:       #ffffff;
  --color-parchment:    #f5f5f7;
  --color-tile-dark:    #272729;
  --color-tile-dark-2:  #2a2a2c;
  --color-nav-black:    #000000;
  --color-ink:          #1d1d1f;
  --color-muted:        #6e6e73;
  --color-on-dark:      #ffffff;
  --color-muted-dark:   #cccccc;
  --color-primary:      #0066cc;
  --color-primary-dark: #2997ff;
  --color-hairline:     #e0e0e0;
  --color-divider-soft: rgba(0,0,0,0.08);
  --spacing-section:    80px;
  --spacing-card:       24px;
  /* Override Bootstrap variables */
  --bs-card-box-shadow: none;
  --bs-border-color:    #e0e0e0;
  --bs-body-bg:         #ffffff;
  --bs-body-color:      #1d1d1f;
}

/* --- Base reset (override Bootstrap dark theme) --- */
html, body {
  background-color: var(--color-canvas) !important;
  color: var(--color-ink) !important;
}

body {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, sans-serif;
  font-size: 17px;
  font-weight: 400;
  line-height: 1.47;
  letter-spacing: -0.374px;
  background: var(--color-canvas) !important;
  background-image: none !important;
}

/* --- Global Nav --- */
.navbar {
  background: var(--color-nav-black) !important;
  height: 44px;
  padding: 0 !important;
  border-bottom: none !important;
  backdrop-filter: none !important;
  -webkit-backdrop-filter: none !important;
}

.navbar .container {
  height: 44px;
}

.navbar-brand {
  color: rgba(255,255,255,0.9) !important;
  font-size: 14px !important;
  font-weight: 400 !important;
  letter-spacing: -0.12px;
  padding: 0 !important;
  line-height: 44px;
}

/* Hide the old gradient logo icon */
.navbar-brand .logo-icon {
  display: none !important;
}

.navbar-nav .nav-link {
  color: rgba(255,255,255,0.85) !important;
  font-size: 12px !important;
  font-weight: 400 !important;
  letter-spacing: -0.12px;
  padding: 0 10px !important;
  line-height: 44px;
  border-radius: 0 !important;
  margin: 0 !important;
  background: none !important;
  border: none !important;
}

.navbar-nav .nav-link:hover {
  color: #fff !important;
  background: none !important;
}

.navbar-nav .nav-link.active {
  color: #fff !important;
  background: none !important;
  border: none !important;
}

.navbar-toggler {
  border-color: rgba(255,255,255,0.3) !important;
  padding: 4px 8px;
}

.navbar-toggler-icon {
  filter: invert(1);
}

/* Hamburger menu dropdown on dark */
.navbar-collapse {
  background: var(--color-nav-black);
  padding: 8px 0;
}

/* --- Reading Progress Bar --- */
.reading-progress {
  position: fixed;
  top: 0;
  left: 0;
  height: 3px;
  background: var(--color-primary);
  z-index: 1001;
  transition: width 0.1s;
}

/* --- Tile System --- */
.tile-white {
  background: var(--color-canvas);
  padding: var(--spacing-section) 0;
  color: var(--color-ink);
}

.tile-parchment {
  background: var(--color-parchment);
  padding: var(--spacing-section) 0;
  color: var(--color-ink);
}

.tile-dark {
  background: var(--color-tile-dark);
  padding: var(--spacing-section) 0;
  color: var(--color-on-dark);
}

.tile-dark-2 {
  background: var(--color-tile-dark-2);
  padding: var(--spacing-section) 0;
  color: var(--color-on-dark);
}

.tile-inner {
  max-width: 980px;
  margin: 0 auto;
  padding: 0 22px;
}

/* --- Typography --- */
.hero-display {
  font-size: 56px;
  font-weight: 600;
  line-height: 1.07;
  letter-spacing: -0.28px;
  color: var(--color-ink);
  margin-bottom: 12px;
}

.display-lg {
  font-size: 40px;
  font-weight: 600;
  line-height: 1.10;
  letter-spacing: 0;
  color: var(--color-ink);
  margin-bottom: 12px;
}

.display-lg-dark {
  font-size: 40px;
  font-weight: 600;
  line-height: 1.10;
  letter-spacing: 0;
  color: var(--color-on-dark);
  margin-bottom: 12px;
}

.lead-text {
  font-size: 21px;
  font-weight: 400;
  line-height: 1.14;
  letter-spacing: 0;
  color: var(--color-ink);
  margin-bottom: 24px;
}

.lead-text-dark {
  font-size: 21px;
  font-weight: 400;
  line-height: 1.14;
  color: var(--color-muted-dark);
  margin-bottom: 24px;
}

.caption-text {
  font-size: 14px;
  font-weight: 400;
  line-height: 1.43;
  letter-spacing: -0.224px;
  color: var(--color-muted);
}

/* --- Buttons --- */
.btn-apple-primary {
  display: inline-block;
  background: var(--color-primary);
  color: #fff !important;
  font-size: 17px;
  font-weight: 400;
  letter-spacing: -0.374px;
  padding: 11px 22px;
  border-radius: 9999px;
  text-decoration: none !important;
  border: none;
  cursor: pointer;
  transition: transform 0.1s;
}

.btn-apple-primary:active {
  transform: scale(0.95);
}

.btn-apple-ghost {
  display: inline-block;
  background: transparent;
  color: var(--color-primary) !important;
  font-size: 17px;
  font-weight: 400;
  letter-spacing: -0.374px;
  padding: 11px 22px;
  border-radius: 9999px;
  text-decoration: none !important;
  border: 1px solid var(--color-primary);
  cursor: pointer;
  transition: transform 0.1s;
}

.btn-apple-ghost:active {
  transform: scale(0.95);
}

.btn-row {
  display: flex;
  gap: 12px;
  justify-content: center;
  flex-wrap: wrap;
}

/* --- Blog Cards (used on parchment tiles) --- */
.blog-card {
  display: block;
  background: var(--color-canvas) !important;
  border: 1px solid var(--color-hairline) !important;
  border-radius: 18px;
  padding: var(--spacing-card);
  text-decoration: none !important;
  color: var(--color-ink) !important;
  height: 100%;
}

/* Remove old dark hover effects */
.blog-card::before { display: none !important; }

.blog-card:hover {
  transform: none;
  box-shadow: none !important;
  border-color: var(--color-hairline) !important;
}

.blog-card .blog-tag {
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.5px;
  text-transform: uppercase;
  color: var(--color-muted);
  margin-bottom: 8px;
}

.blog-card h3 {
  font-size: 17px !important;
  font-weight: 600;
  letter-spacing: -0.374px;
  color: var(--color-ink) !important;
  line-height: 1.24;
  margin: 0 0 8px 0;
}

.blog-card p {
  font-size: 14px;
  color: var(--color-muted) !important;
  line-height: 1.43;
  letter-spacing: -0.224px;
  margin-bottom: 0;
}

.blog-card .card-link {
  color: var(--color-primary);
  font-size: 14px;
  letter-spacing: -0.224px;
  text-decoration: none;
  margin-top: 12px;
  display: block;
}

.blog-meta {
  font-size: 12px;
  color: var(--color-muted);
  margin-top: 12px;
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
}

/* --- Tags --- */
.tag {
  background: rgba(0,102,204,0.08);
  color: var(--color-primary);
  padding: 2px 10px;
  border-radius: 9999px;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.3px;
  border: none !important;
  background-image: none !important;
}

/* --- Skill Chips (dark tile) --- */
.skill-chips {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: center;
  margin-top: 24px;
}

.skill-chip {
  background: rgba(255,255,255,0.08);
  color: var(--color-on-dark);
  font-size: 14px;
  font-weight: 400;
  letter-spacing: -0.224px;
  padding: 8px 18px;
  border-radius: 9999px;
  border: 1px solid rgba(255,255,255,0.12);
}

/* --- About Page Section Cards --- */
.about-section-card {
  background: var(--color-canvas);
  border: 1px solid var(--color-hairline);
  border-radius: 18px;
  padding: 32px;
  margin-bottom: 20px;
}

.about-section-card h3 {
  font-size: 21px;
  font-weight: 600;
  letter-spacing: -0.374px;
  color: var(--color-ink);
  margin-top: 0;
  margin-bottom: 16px;
}

.about-section-card p,
.about-section-card li {
  font-size: 17px;
  color: var(--color-ink);
  line-height: 1.47;
  letter-spacing: -0.374px;
}

.about-section-card a {
  color: var(--color-primary);
  text-decoration: none;
}

/* Override old dark timeline */
.timeline-item {
  border-left: 2px solid var(--color-hairline) !important;
  padding-left: 20px;
  margin: 16px 0;
  position: relative;
}

.timeline-item::before {
  content: '';
  width: 8px;
  height: 8px;
  background: var(--color-primary) !important;
  border-radius: 50%;
  position: absolute;
  left: -5px;
  top: 6px;
}

/* Override old gradient skill badges on about page */
.skill-badge {
  background: rgba(0,102,204,0.08) !important;
  background-image: none !important;
  color: var(--color-primary) !important;
  padding: 6px 14px;
  border-radius: 9999px;
  margin: 4px;
  display: inline-block;
  font-size: 14px;
  font-weight: 400;
  border: 1px solid rgba(0,102,204,0.2) !important;
}

/* --- Article body (blog posts) --- */
.article-body {
  max-width: 700px;
  margin: 0 auto;
  font-size: 17px;
  line-height: 1.47;
  letter-spacing: -0.374px;
  color: var(--color-ink);
  padding: 0 22px 80px;
}

.article-body h1 {
  font-size: 40px;
  font-weight: 600;
  letter-spacing: 0;
  color: var(--color-ink) !important;
  background: none !important;
  -webkit-background-clip: unset !important;
  -webkit-text-fill-color: var(--color-ink) !important;
  background-clip: unset !important;
  margin-top: 48px;
  margin-bottom: 12px;
}

.article-body h2 {
  font-size: 28px;
  font-weight: 600;
  letter-spacing: -0.374px;
  color: var(--color-ink);
  border-bottom: 1px solid var(--color-hairline) !important;
  padding-bottom: 8px;
  margin-top: 40px;
  margin-bottom: 16px;
}

.article-body h3 {
  font-size: 21px;
  font-weight: 600;
  letter-spacing: -0.374px;
  color: var(--color-ink);
  margin-top: 32px;
  margin-bottom: 12px;
}

.article-body p { margin-bottom: 20px; }

.article-body a {
  color: var(--color-primary);
  text-decoration: none;
  border-bottom: none !important;
}

.article-body a:hover { text-decoration: underline; }

.article-body ul,
.article-body ol {
  margin-bottom: 20px;
  padding-left: 24px;
}

.article-body li { margin-bottom: 8px; }

.article-body strong {
  font-weight: 600;
  color: var(--color-ink);
}

/* Code blocks */
.article-body pre {
  background: var(--color-parchment) !important;
  border: 1px solid var(--color-hairline);
  border-radius: 12px;
  padding: 20px !important;
  overflow-x: auto;
  margin: 24px 0;
}

.article-body code {
  font-family: 'JetBrains Mono', 'Fira Code', Consolas, monospace;
  font-size: 14px;
}

.article-body p code,
.article-body li code {
  background: rgba(0,0,0,0.05) !important;
  padding: 2px 6px;
  border-radius: 4px;
  color: var(--color-ink) !important;
  border: none !important;
  font-size: 14px;
}

/* Command blocks */
.article-body .command,
.command {
  background: var(--color-parchment) !important;
  background-image: none !important;
  border-left: 3px solid var(--color-primary);
  padding: 14px 20px;
  border-radius: 0 12px 12px 0;
  margin: 16px 0;
  font-family: 'JetBrains Mono', Consolas, monospace;
  font-size: 14px;
  overflow-x: auto;
  color: var(--color-ink) !important;
}

.article-body .command::before,
.command::before {
  content: '$ ';
  color: var(--color-primary);
  font-weight: 600;
}

.article-body .command strong,
.command strong {
  color: var(--color-ink) !important;
}

/* Article meta bar */
.article-meta {
  background: var(--color-parchment) !important;
  border: 1px solid var(--color-hairline) !important;
  border-radius: 12px;
  padding: 14px 20px;
  display: flex;
  gap: 20px;
  color: var(--color-muted);
  font-size: 14px;
  margin-bottom: 32px;
  flex-wrap: wrap;
}

.article-meta span {
  display: flex;
  align-items: center;
  gap: 6px;
}

/* Table of contents */
.toc {
  background: var(--color-parchment) !important;
  border-radius: 12px;
  padding: 20px;
  margin-bottom: 32px;
  border: 1px solid var(--color-hairline) !important;
}

.toc h4 {
  margin-top: 0;
  margin-bottom: 12px;
  font-size: 14px;
  font-weight: 600;
  color: var(--color-muted);
}

.toc ul { margin: 0; padding-left: 18px; }

.toc a {
  border: none !important;
  color: var(--color-primary) !important;
  font-size: 14px;
  text-decoration: none;
}

/* Alert boxes — light theme */
.alert-info {
  background: rgba(0,102,204,0.06) !important;
  border: 1px solid rgba(0,102,204,0.2) !important;
  border-radius: 12px;
  color: var(--color-ink);
}

.alert-warning {
  background: rgba(255,193,7,0.08) !important;
  border: 1px solid rgba(255,193,7,0.3) !important;
  border-radius: 12px;
  color: var(--color-ink);
}

/* Config file block (linux clash page) */
.config-file {
  background: var(--color-parchment) !important;
  border: 1px solid var(--color-hairline);
  border-radius: 12px;
  padding: 16px 20px;
  margin: 16px 0;
}

.config-file .filename {
  color: var(--color-primary) !important;
  font-size: 13px;
  margin-bottom: 10px;
  font-family: monospace;
}

/* --- Footer --- */
.site-footer {
  background: var(--color-parchment);
  border-top: 1px solid var(--color-hairline);
  padding: 40px 22px;
  color: var(--color-muted);
}

.footer-inner {
  max-width: 980px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 16px;
}

.footer-links {
  display: flex;
  gap: 24px;
}

.site-footer a {
  color: var(--color-primary);
  text-decoration: none;
  font-size: 14px;
  letter-spacing: -0.224px;
}

.footer-legal {
  font-size: 12px;
  color: var(--color-muted);
  letter-spacing: -0.12px;
  margin: 0;
}

/* --- Back to top --- */
.back-to-top {
  position: fixed;
  bottom: 30px;
  right: 30px;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background: var(--color-ink);
  color: white;
  border: none;
  cursor: pointer;
  opacity: 0;
  transition: opacity 0.3s;
  z-index: 1000;
  font-size: 16px;
  box-shadow: none !important;
}

.back-to-top.visible { opacity: 1; }

/* --- Override lingering Bootstrap/dark remnants --- */
.gradient-text {
  background: none !important;
  -webkit-background-clip: unset !important;
  -webkit-text-fill-color: var(--color-ink) !important;
  background-clip: unset !important;
  color: var(--color-ink) !important;
}

.gradient-separator { display: none; }

/* Bootstrap card overrides */
.card {
  background: var(--color-canvas) !important;
  border-color: var(--color-hairline) !important;
}

/* Links outside article-body */
a { color: var(--color-primary); }

/* Bootstrap text-muted override */
.text-muted { color: var(--color-muted) !important; }

/* --- Responsive --- */
@media (max-width: 640px) {
  .tile-white,
  .tile-parchment,
  .tile-dark,
  .tile-dark-2 {
    padding: 48px 0;
  }

  .hero-display { font-size: 34px; }

  .display-lg,
  .display-lg-dark { font-size: 28px; }

  .btn-apple-primary,
  .btn-apple-ghost {
    font-size: 15px;
    padding: 10px 18px;
  }

  .article-body { padding: 0 16px 48px; }
}

@media (max-width: 833px) {
  .navbar-collapse {
    padding: 8px 16px 16px;
  }

  .navbar-nav .nav-link {
    line-height: 2.2;
    padding: 0 !important;
  }
}
```

- [ ] **Step 2: Verify the file was created**

Run: `ls -la apple.css`
Expected: file exists, ~8–10 KB

- [ ] **Step 3: Commit**

```bash
git add apple.css
git commit -m "feat: add apple.css shared design system stylesheet"
```

---

## Task 2: Rewrite index.html

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace index.html with Apple-style layout**

Write the following complete file to `index.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Luka Mai</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.1/font/bootstrap-icons.css">
    <link rel="stylesheet" href="/apple.css">
  </head>
  <body>

    <!-- Global Nav -->
    <nav class="navbar navbar-expand-lg sticky-top">
      <div class="container">
        <a class="navbar-brand" href="/">Luka Mai</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item"><a class="nav-link active" href="/">Home</a></li>
            <li class="nav-item"><a class="nav-link" href="/blogs.html">Blogs</a></li>
            <li class="nav-item"><a class="nav-link" href="/about_me.html">About</a></li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- Hero Tile — white -->
    <section class="tile-white text-center">
      <div class="tile-inner">
        <h1 class="hero-display">Luka Mai</h1>
        <p class="lead-text">Graduate Student · AI Chip Researcher · Vimmer</p>
        <div class="btn-row">
          <a href="/blogs.html" class="btn-apple-primary">Read My Blogs</a>
          <a href="/about_me.html" class="btn-apple-ghost">About Me</a>
        </div>
      </div>
    </section>

    <!-- Blog Preview Tile — parchment -->
    <section class="tile-parchment">
      <div class="tile-inner">
        <h2 class="display-lg text-center">Latest Articles</h2>
        <p class="caption-text text-center mb-4">记录学习历程，分享技术心得</p>
        <div class="row g-3">
          <div class="col-md-4">
            <a href="/blogs/openclaw-macos-deploy.html" class="blog-card">
              <div class="blog-tag">macOS · AI</div>
              <h3>如何在 MacOS 上部署 OpenClaw</h3>
              <p>OpenClaw 是一个强大的 AI 助手框架，介绍如何在 MacOS 上快速部署。</p>
              <span class="card-link">阅读全文 →</span>
            </a>
          </div>
          <div class="col-md-4">
            <a href="/blogs/tmux install without root.html" class="blog-card">
              <div class="blog-tag">Linux · Terminal</div>
              <h3>tmux install without root</h3>
              <p>详细介绍如何在没有 root 权限的情况下从源码编译安装 tmux。</p>
              <span class="card-link">阅读全文 →</span>
            </a>
          </div>
          <div class="col-md-4">
            <a href="/blogs/neovim install.html" class="blog-card">
              <div class="blog-tag">Neovim · Editor</div>
              <h3>neovim install</h3>
              <p>Neovim + LazyVim 完整安装配置指南，解决 Git 版本过旧导致的插件问题。</p>
              <span class="card-link">阅读全文 →</span>
            </a>
          </div>
        </div>
        <div class="text-center mt-4">
          <a href="/blogs.html" class="btn-apple-primary" style="font-size:15px;padding:9px 20px;">查看全部文章</a>
        </div>
      </div>
    </section>

    <!-- About Tile — dark -->
    <section class="tile-dark text-center">
      <div class="tile-inner">
        <h2 class="display-lg-dark">About Me</h2>
        <p class="lead-text-dark">
          Graduate student at SYSU, researching Compute in SRAM and AI Chips.<br>
          A vimer who loves basketball and fitness.
        </p>
        <div class="btn-row">
          <a href="/about_me.html" class="btn-apple-primary">Learn More</a>
        </div>
        <div class="skill-chips">
          <span class="skill-chip">AI Chips</span>
          <span class="skill-chip">Compute in SRAM</span>
          <span class="skill-chip">Python</span>
          <span class="skill-chip">Verilog</span>
          <span class="skill-chip">Vim</span>
          <span class="skill-chip">Linux</span>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="site-footer">
      <div class="footer-inner">
        <div class="footer-links">
          <a href="https://github.com/maiyangzhan" target="_blank" rel="noopener">GitHub</a>
          <a href="mailto:maiyangzhan@outlook.com">Email</a>
          <a href="/blogs.html">Blogs</a>
        </div>
        <p class="footer-legal">© 2026 Luka Mai. All rights reserved.</p>
      </div>
    </footer>

  </body>
</html>
```

- [ ] **Step 2: Visually verify in browser**

Open `index.html` in a browser (or `open index.html`). Check:
- Black nav bar, 44px height, white small text, no gradient logo
- White hero section with large "Luka Mai" headline, blue pill buttons
- Parchment blog section with 3 white cards
- Dark section with skill chips
- Parchment footer with blue links
- No gradient backgrounds anywhere

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: rewrite index.html with Apple tile layout"
```

---

## Task 3: Rewrite blogs.html

**Files:**
- Modify: `blogs.html`

- [ ] **Step 1: Replace blogs.html with Apple-style layout**

Write the following complete file to `blogs.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Blogs - Luka Mai</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.1/font/bootstrap-icons.css">
    <link rel="stylesheet" href="/apple.css">
  </head>
  <body>

    <!-- Global Nav -->
    <nav class="navbar navbar-expand-lg sticky-top">
      <div class="container">
        <a class="navbar-brand" href="/">Luka Mai</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item"><a class="nav-link" href="/">Home</a></li>
            <li class="nav-item"><a class="nav-link active" href="/blogs.html">Blogs</a></li>
            <li class="nav-item"><a class="nav-link" href="/about_me.html">About</a></li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- Hero Tile — white -->
    <section class="tile-white text-center">
      <div class="tile-inner">
        <h1 class="hero-display">Blogs</h1>
        <p class="lead-text">记录学习历程，分享技术心得</p>
      </div>
    </section>

    <!-- Blog List Tile — parchment -->
    <section class="tile-parchment">
      <div class="tile-inner">
        <h2 class="display-lg mb-4">All Articles</h2>
        <div class="row g-3">

          <div class="col-md-6">
            <a href="/blogs/openclaw-macos-deploy.html" class="blog-card">
              <div class="blog-tag">macOS · AI</div>
              <h3>如何在 MacOS 上部署 OpenClaw</h3>
              <p>OpenClaw 是一个强大的 AI 助手框架，这篇博客介绍如何在 MacOS 上快速部署。</p>
              <div class="blog-meta">
                <span><i class="bi bi-calendar3"></i> 2026-03-13</span>
                <span><i class="bi bi-clock"></i> 5 min</span>
              </div>
              <span class="card-link">阅读全文 →</span>
            </a>
          </div>

          <div class="col-md-6">
            <a href="/blogs/tmux install without root.html" class="blog-card">
              <div class="blog-tag">Linux · Terminal</div>
              <h3>tmux install without root</h3>
              <p>详细介绍如何在没有 root 权限的情况下从源码编译安装 tmux，包含所有依赖库的安装步骤。</p>
              <div class="blog-meta">
                <span><i class="bi bi-calendar3"></i> 2024-02-06</span>
                <span><i class="bi bi-clock"></i> 5 min</span>
              </div>
              <span class="card-link">阅读全文 →</span>
            </a>
          </div>

          <div class="col-md-6">
            <a href="/blogs/neovim install.html" class="blog-card">
              <div class="blog-tag">Neovim · Editor · Vim</div>
              <h3>neovim install</h3>
              <p>Neovim + LazyVim 完整安装配置指南，解决 Git 版本过旧导致的插件安装问题。</p>
              <div class="blog-meta">
                <span><i class="bi bi-calendar3"></i> 2024-02-06</span>
                <span><i class="bi bi-clock"></i> 3 min</span>
              </div>
              <span class="card-link">阅读全文 →</span>
            </a>
          </div>

          <div class="col-md-6">
            <a href="/blogs/linux terminal clash.html" class="blog-card">
              <div class="blog-tag">Linux · Proxy · Clash</div>
              <h3>linux terminal clash</h3>
              <p>Linux 终端 Clash 配置教程，配置终端代理实现 Git 加速和科学上网。</p>
              <div class="blog-meta">
                <span><i class="bi bi-calendar3"></i> 2024-02-06</span>
                <span><i class="bi bi-clock"></i> 4 min</span>
              </div>
              <span class="card-link">阅读全文 →</span>
            </a>
          </div>

        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="site-footer">
      <div class="footer-inner">
        <div class="footer-links">
          <a href="https://github.com/maiyangzhan" target="_blank" rel="noopener">GitHub</a>
          <a href="mailto:maiyangzhan@outlook.com">Email</a>
          <a href="/">Home</a>
        </div>
        <p class="footer-legal">© 2026 Luka Mai. All rights reserved.</p>
      </div>
    </footer>

    <!-- Back to Top -->
    <button class="back-to-top" id="backToTop" aria-label="返回顶部">
      <i class="bi bi-arrow-up"></i>
    </button>

    <script>
      const backToTop = document.getElementById('backToTop');
      window.addEventListener('scroll', () => {
        backToTop.classList.toggle('visible', window.scrollY > 300);
      });
      backToTop.addEventListener('click', () => {
        window.scrollTo({ top: 0, behavior: 'smooth' });
      });
    </script>

  </body>
</html>
```

- [ ] **Step 2: Visually verify in browser**

Open `blogs.html`. Check:
- White hero tile with large "Blogs" headline
- Parchment background with 2×2 white blog cards
- Cards have tag (uppercase muted), title, excerpt, date, "阅读全文 →" link in blue
- No gradient anywhere, no dark blue background

- [ ] **Step 3: Commit**

```bash
git add blogs.html
git commit -m "feat: rewrite blogs.html with Apple tile layout"
```

---

## Task 4: Rewrite about_me.html

**Files:**
- Modify: `about_me.html`

- [ ] **Step 1: Replace about_me.html with Apple-style layout**

Write the following complete file to `about_me.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>About Me - Luka Mai</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.1/font/bootstrap-icons.css">
    <link rel="stylesheet" href="/apple.css">
  </head>
  <body>

    <!-- Global Nav -->
    <nav class="navbar navbar-expand-lg sticky-top">
      <div class="container">
        <a class="navbar-brand" href="/">Luka Mai</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item"><a class="nav-link" href="/">Home</a></li>
            <li class="nav-item"><a class="nav-link" href="/blogs.html">Blogs</a></li>
            <li class="nav-item"><a class="nav-link active" href="/about_me.html">About</a></li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- Hero Tile — white -->
    <section class="tile-white text-center">
      <div class="tile-inner">
        <h1 class="hero-display">Luka Mai</h1>
        <p class="lead-text">Graduate Student · AI Chip Researcher · Vimmer</p>
      </div>
    </section>

    <!-- Bio Tile — parchment -->
    <section class="tile-parchment">
      <div class="tile-inner" style="max-width:760px;">

        <div class="about-section-card">
          <h3><i class="bi bi-person me-2" style="color:var(--color-primary)"></i>About Me</h3>
          <p>I am a graduate student at <strong>Sun Yat-sen University (SYSU)</strong>, majoring in Computer Science. My research focuses on <strong>Compute in SRAM</strong> and <strong>AI Chips</strong>.</p>
          <p>I am passionate about building efficient computing systems and exploring the intersection of hardware and AI.</p>
        </div>

        <div class="about-section-card">
          <h3><i class="bi bi-mortarboard me-2" style="color:var(--color-primary)"></i>Education</h3>
          <div class="timeline-item">
            <h5 style="font-size:17px;font-weight:600;margin:0 0 4px">Sun Yat-sen University (SYSU)</h5>
            <p class="caption-text mb-1">Master's Degree · 2022 – Present</p>
            <p>Computer Science · Research: AI Chips, Compute in SRAM</p>
          </div>
          <div class="timeline-item">
            <h5 style="font-size:17px;font-weight:600;margin:0 0 4px">Undergraduate</h5>
            <p class="caption-text mb-0">Bachelor's Degree · 2018 – 2022</p>
          </div>
        </div>

        <div class="about-section-card">
          <h3><i class="bi bi-lightbulb me-2" style="color:var(--color-primary)"></i>Research Interests</h3>
          <ul>
            <li><strong>Compute in SRAM:</strong> In-memory computing for AI workloads</li>
            <li><strong>AI Chips:</strong> Energy-efficient accelerator design</li>
            <li><strong>Hardware-Software Co-design:</strong> Optimizing AI systems from algorithm to hardware</li>
          </ul>
        </div>

        <div class="about-section-card">
          <h3><i class="bi bi-tools me-2" style="color:var(--color-primary)"></i>Technical Skills</h3>
          <div>
            <span class="skill-badge"><i class="bi bi-cpu me-1"></i>AI Chip Design</span>
            <span class="skill-badge"><i class="bi bi-memory me-1"></i>SRAM Computing</span>
            <span class="skill-badge"><i class="bi bi-filetype-py me-1"></i>Python</span>
            <span class="skill-badge"><i class="bi bi-filetype-v me-1"></i>Verilog</span>
            <span class="skill-badge"><i class="bi bi-hdd me-1"></i>FPGA</span>
            <span class="skill-badge"><i class="bi bi-terminal me-1"></i>Vim</span>
            <span class="skill-badge"><i class="bi bi-git me-1"></i>Git</span>
            <span class="skill-badge"><i class="bi bi-ubuntu me-1"></i>Linux</span>
            <span class="skill-badge"><i class="bi bi-filetype-md me-1"></i>Markdown</span>
          </div>
        </div>

        <div class="about-section-card">
          <h3><i class="bi bi-heart me-2" style="color:var(--color-primary)"></i>Interests &amp; Hobbies</h3>
          <ul>
            <li><strong>Basketball:</strong> Love the teamwork and energy</li>
            <li><strong>Fitness:</strong> Keeping healthy, staying strong</li>
            <li><strong>Vim:</strong> A dedicated vimmer, efficiency enthusiast</li>
            <li><strong>Open Source:</strong> Believes in sharing knowledge</li>
          </ul>
        </div>

      </div>
    </section>

    <!-- Contact Tile — dark -->
    <section class="tile-dark text-center">
      <div class="tile-inner">
        <h2 class="display-lg-dark">Connect With Me</h2>
        <p class="lead-text-dark" style="margin-bottom:32px;">
          <a href="mailto:maiyangzhan@outlook.com" style="color:var(--color-primary-dark)">maiyangzhan@outlook.com</a>
        </p>
        <div class="btn-row">
          <a href="https://github.com/maiyangzhan" target="_blank" rel="noopener" class="btn-apple-primary">
            <i class="bi bi-github me-2"></i>GitHub
          </a>
          <a href="mailto:maiyangzhan@outlook.com" class="btn-apple-ghost" style="color:#2997ff;border-color:#2997ff;">Email</a>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="site-footer">
      <div class="footer-inner">
        <div class="footer-links">
          <a href="https://github.com/maiyangzhan" target="_blank" rel="noopener">GitHub</a>
          <a href="/blogs.html">Blogs</a>
          <a href="/">Home</a>
        </div>
        <p class="footer-legal">© 2026 Luka Mai. All rights reserved.</p>
      </div>
    </footer>

  </body>
</html>
```

- [ ] **Step 2: Visually verify in browser**

Open `about_me.html`. Check:
- White hero tile with large name
- Parchment background with white rounded section cards (About, Education, Research, Skills, Hobbies)
- Education timeline uses blue dot + left hairline border
- Skill badges are blue pill shape, no gradient
- Dark contact tile with blue links
- Parchment footer

- [ ] **Step 3: Commit**

```bash
git add about_me.html
git commit -m "feat: rewrite about_me.html with Apple tile layout"
```

---

## Task 5: Rewrite blogs/neovim install.html

**Files:**
- Modify: `blogs/neovim install.html`

- [ ] **Step 1: Replace the file with Apple-style wrapper**

The article body content (everything between the `<article>` tags in the current file) is preserved exactly. Only the wrapper changes. Write the following complete file:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>neovim install - Luka's Blog</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.1/font/bootstrap-icons.css">
    <link rel="stylesheet" href="/apple.css">
  </head>
  <body>
    <div class="reading-progress" id="progressBar"></div>

    <!-- Global Nav -->
    <nav class="navbar navbar-expand-lg sticky-top">
      <div class="container">
        <a class="navbar-brand" href="/">Luka Mai</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item"><a class="nav-link" href="/">Home</a></li>
            <li class="nav-item"><a class="nav-link active" href="/blogs.html">Blogs</a></li>
            <li class="nav-item"><a class="nav-link" href="/about_me.html">About</a></li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- Article — white tile -->
    <section class="tile-white">
      <article class="article-body">
        <h1><i class="bi bi-code-square me-2" style="color:var(--color-primary)"></i>neovim install</h1>

        <div class="article-meta">
          <span><i class="bi bi-calendar3"></i> 2024-02-06</span>
          <span><i class="bi bi-clock"></i> 3 min</span>
          <span><i class="bi bi-tag"></i> Neovim, Editor, Vim</span>
        </div>

        <div class="toc">
          <h4><i class="bi bi-list-ul me-2"></i>目录</h4>
          <ul>
            <li><a href="#准备工作">准备工作</a></li>
            <li><a href="#安装nvim">安装 nvim</a></li>
            <li><a href="#安装lazyvim">安装 LazyVim</a></li>
            <li><a href="#常见问题">常见问题</a></li>
          </ul>
        </div>

        <div class="alert alert-info">
          <i class="bi bi-lightbulb me-2"></i>
          <strong>提示：</strong>建议先配置终端代理，因为 LazyVim 插件需要从 GitHub 下载，内网无法连接。
        </div>

        <h2 id="准备工作"><i class="bi bi-check-circle me-2"></i>准备工作</h2>
        <p>先配置终端代理，参考博客 <a href="/blogs/linux terminal clash.html">Linux Terminal Clash</a></p>

        <h2 id="安装nvim"><i class="bi bi-download me-2"></i>安装 nvim</h2>
        <div class="command">curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim.appimage</div>
        <div class="command">chmod u+x nvim.appimage</div>
        <div class="command">./nvim.appimage</div>

        <p>如果能打开 nvim，代表安装成功。</p>

        <p>可以将 nvim.appimage 移动到 <code>~/.local/bin/</code> 中并改名为 <code>nvim</code>：</p>
        <div class="command">mv nvim.appimage ~/.local/bin/nvim</div>

        <p>确保 <code>~/.local/bin/</code> 在 <code>PATH</code> 中，然后就可以通过 <code>nvim</code> 命令打开了。</p>

        <h2 id="安装lazyvim"><i class="bi bi-box-seam me-2"></i>安装 LazyVim</h2>
        <div class="command">git clone https://github.com/LazyVim/starter ~/.config/nvim</div>
        <div class="command">rm -rf ~/.config/nvim/.git</div>
        <div class="command">nvim</div>

        <h2 id="常见问题"><i class="bi bi-exclamation-triangle me-2"></i>常见问题</h2>

        <div class="alert alert-warning">
          <i class="bi bi-bug me-2"></i>
          <strong>错误：</strong>LazyVim nvim bug: module 'lazy' not found
        </div>

        <p>LazyVim 的 issue 中有类似的问题，问题出现的原因是 <strong>Git 版本过旧</strong>，不支持 <code>--filter=blob:none</code> 导致 lazy.nvim 安装失败。</p>

        <h3>解决方案：升级 Git</h3>

        <p>Git 版本 2.33.0 开始支持上面的 git 选项。首先查看当前版本：</p>
        <div class="command">git --version</div>

        <p>如果版本低于 2.33.0，升级 Git：</p>
        <div class="command">wget https://github.com/git/git/archive/refs/tags/v2.43.0.tar.gz</div>
        <div class="command">tar -zxvf v2.43.0.tar.gz</div>
        <div class="command">cd git-2.43.0</div>
        <div class="command">make configure</div>
        <div class="command">./configure --prefix=/home/myz/git-2.43.0</div>
        <div class="command">make &amp;&amp; make install</div>

        <h3>添加环境变量</h3>
        <p>在 <code>~/.bashrc</code> 中添加：</p>
        <pre><code class="language-bash">export PATH=/home/myz/git-2.43.0/bin:$PATH
export GIT_EXEC_PATH=/home/myz/git-2.43.0/libexec/git-core</code></pre>

        <div class="command">source ~/.bashrc</div>
        <div class="command">git --version</div>

        <div class="alert alert-info">
          <i class="bi bi-info-circle me-2"></i>
          如果版本还不对，可能是环境变量位置放得不对，调整顺序试试。
        </div>

        <hr class="my-4" style="border-color:var(--color-hairline)">
        <p class="caption-text text-center">感谢阅读</p>
      </article>
    </section>

    <!-- Footer -->
    <footer class="site-footer">
      <div class="footer-inner">
        <div class="footer-links">
          <a href="/blogs.html">← All Blogs</a>
          <a href="/">Home</a>
        </div>
        <p class="footer-legal">© 2026 Luka Mai. All rights reserved.</p>
      </div>
    </footer>

    <button class="back-to-top" id="backToTop" aria-label="返回顶部">
      <i class="bi bi-arrow-up"></i>
    </button>

    <script>
      window.addEventListener('scroll', () => {
        const winScroll = document.body.scrollTop || document.documentElement.scrollTop;
        const height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
        document.getElementById('progressBar').style.width = (winScroll / height * 100) + '%';
      });
      const backToTop = document.getElementById('backToTop');
      window.addEventListener('scroll', () => {
        backToTop.classList.toggle('visible', window.scrollY > 300);
      });
      backToTop.addEventListener('click', () => {
        window.scrollTo({ top: 0, behavior: 'smooth' });
      });
    </script>
  </body>
</html>
```

- [ ] **Step 2: Visually verify in browser**

Open `blogs/neovim install.html`. Check:
- Black nav, reading progress bar is blue (not gradient)
- White background throughout article
- Article title is dark (#1d1d1f), not gradient text
- Command blocks have parchment background + blue left border
- Code inline is light gray, not pink
- TOC and article-meta have parchment background with hairline border
- Alert boxes are light blue/yellow (not dark)
- Footer is parchment with blue links

- [ ] **Step 3: Commit**

```bash
git add "blogs/neovim install.html"
git commit -m "feat: rewrite neovim install blog post with Apple style"
```

---

## Task 6: Rewrite blogs/tmux install without root.html

**Files:**
- Modify: `blogs/tmux install without root.html`

- [ ] **Step 1: Replace the file with Apple-style wrapper**

Write the following complete file to `blogs/tmux install without root.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>tmux install without root - Luka's Blog</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.1/font/bootstrap-icons.css">
    <link rel="stylesheet" href="/apple.css">
  </head>
  <body>
    <div class="reading-progress" id="progressBar"></div>

    <nav class="navbar navbar-expand-lg sticky-top">
      <div class="container">
        <a class="navbar-brand" href="/">Luka Mai</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item"><a class="nav-link" href="/">Home</a></li>
            <li class="nav-item"><a class="nav-link active" href="/blogs.html">Blogs</a></li>
            <li class="nav-item"><a class="nav-link" href="/about_me.html">About</a></li>
          </ul>
        </div>
      </div>
    </nav>

    <section class="tile-white">
      <article class="article-body">
        <h1><i class="bi bi-terminal me-2" style="color:var(--color-primary)"></i>tmux install without root</h1>

        <div class="article-meta">
          <span><i class="bi bi-calendar3"></i> 2024-02-06</span>
          <span><i class="bi bi-clock"></i> 5 min</span>
          <span><i class="bi bi-tag"></i> Linux, Terminal</span>
        </div>

        <div class="toc">
          <h4><i class="bi bi-list-ul me-2"></i>目录</h4>
          <ul>
            <li><a href="#步骤1">步骤1：下载依赖</a></li>
            <li><a href="#步骤2">步骤2：解压文件</a></li>
            <li><a href="#步骤3">步骤3：安装 libevent 和 ncurses</a></li>
            <li><a href="#步骤4">步骤4：安装 tmux</a></li>
            <li><a href="#常用命令">常用命令</a></li>
          </ul>
        </div>

        <h2 id="步骤1"><i class="bi bi-1-circle me-2"></i>步骤1：下载依赖</h2>
        <p>下载 tmux 及其依赖软件：</p>
        <div class="command">wget -c https://github.com/tmux/tmux/releases/tag/3.3a/tmux-3.3a.tar.gz</div>
        <div class="command">wget -c https://github.com/libevent/libevent/releases/download/release-2.1.11-stable/libevent-2.1.11-stable.tar.gz</div>
        <div class="command">wget -c https://ftp.gnu.org/gnu/ncurses/ncurses-6.2.tar.gz</div>

        <h2 id="步骤2"><i class="bi bi-2-circle me-2"></i>步骤2：解压文件</h2>
        <p>解压这三个压缩包：</p>
        <div class="command">tar -zxvf ***.tar.gz</div>
        <div class="alert alert-info">
          <i class="bi bi-info-circle me-2"></i>
          64位服务器可能不支持直接解压wget下载的压缩包，需要先传到服务器再解压。
        </div>

        <h2 id="步骤3"><i class="bi bi-3-circle me-2"></i>步骤3：安装 libevent 和 ncurses</h2>
        <p>分别源码安装这些依赖：</p>

        <h3>安装 libevent</h3>
        <div class="command">cd libevent-2.1.12-stable/</div>
        <div class="command">./configure --prefix=/home/myz/tmux --disable-shared</div>
        <div class="command">make &amp;&amp; make install</div>
        <p><code>libevent</code> 会安装在 <code>/tmux/lib</code></p>

        <h3>安装 ncurses</h3>
        <div class="command">cd ncurses-6.2</div>
        <div class="command">./configure --prefix=/home/myz/tmux</div>
        <div class="command">make &amp;&amp; make install</div>
        <p><code>ncurses</code> 会安装在 <code>/tmux/include</code></p>

        <h2 id="步骤4"><i class="bi bi-4-circle me-2"></i>步骤4：安装 tmux</h2>
        <div class="command">cd tmux-3.3a/</div>
        <div class="command">./configure CFLAGS="-I/home/myz/tmux/include -I/home/myz/tmux/include/ncurses" LDFLAGS="-L/home/myz/tmux/lib -L/home/myz/tmux/include/ncurses -L/home/myz/tmux/include"</div>
        <div class="command">make</div>
        <div class="command">cp tmux /home/myz/tmux/bin</div>

        <h3>设置环境变量</h3>
        <div class="command">export PATH=/home/myz/tmux/bin:$PATH</div>
        <div class="command">source ~/.bashrc</div>

        <div class="alert alert-warning">
          <i class="bi bi-exclamation-triangle me-2"></i>
          <strong>注意：</strong>在 tmux 下使用 vim 按 ESC 会有延迟，需要在 <code>~/.tmux.conf</code> 中增加：
          <pre style="margin:8px 0 0;background:transparent;border:none;padding:0;">set -g escape-time 0</pre>
        </div>

        <h2 id="常用命令"><i class="bi bi-terminal me-2"></i>常用命令</h2>

        <h3>1）新建会话</h3>
        <div class="command">tmux new -s ccc</div>
        <p>加上参数 <code>-d</code>，表示在后台新建会话：</p>
        <div class="command">tmux new -s shibo -d</div>

        <h3>2）查看所有会话</h3>
        <div class="command">tmux ls</div>

        <h3>3）接入会话</h3>
        <div class="command">tmux attach -t ccc</div>

        <h3>4）杀死会话</h3>
        <div class="command">tmux kill-session -t ccc</div>

        <hr class="my-4" style="border-color:var(--color-hairline)">
        <p class="caption-text text-center">感谢阅读</p>
      </article>
    </section>

    <footer class="site-footer">
      <div class="footer-inner">
        <div class="footer-links">
          <a href="/blogs.html">← All Blogs</a>
          <a href="/">Home</a>
        </div>
        <p class="footer-legal">© 2026 Luka Mai. All rights reserved.</p>
      </div>
    </footer>

    <button class="back-to-top" id="backToTop" aria-label="返回顶部">
      <i class="bi bi-arrow-up"></i>
    </button>

    <script>
      window.addEventListener('scroll', () => {
        const winScroll = document.body.scrollTop || document.documentElement.scrollTop;
        const height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
        document.getElementById('progressBar').style.width = (winScroll / height * 100) + '%';
      });
      const backToTop = document.getElementById('backToTop');
      window.addEventListener('scroll', () => {
        backToTop.classList.toggle('visible', window.scrollY > 300);
      });
      backToTop.addEventListener('click', () => {
        window.scrollTo({ top: 0, behavior: 'smooth' });
      });
    </script>
  </body>
</html>
```

- [ ] **Step 2: Visually verify in browser**

Open `blogs/tmux install without root.html`. Check:
- Same Apple style as neovim install page
- Command blocks, alerts, TOC all on light background
- No dark gradients, no glow effects

- [ ] **Step 3: Commit**

```bash
git add "blogs/tmux install without root.html"
git commit -m "feat: rewrite tmux install blog post with Apple style"
```

---

## Task 7: Rewrite blogs/linux terminal clash.html

**Files:**
- Modify: `blogs/linux terminal clash.html`

- [ ] **Step 1: Read the article body content from the existing file**

Run: `cat "blogs/linux terminal clash.html" | grep -n "<main>" `

Then read from that line onward to capture all article content between `<main>` and `</main>`. You need to preserve the `.config-file` blocks and their content exactly.

- [ ] **Step 2: Replace the file with Apple-style wrapper**

Write the following to `blogs/linux terminal clash.html`. The head, nav, section wrapper, and footer are new; paste the article body content (everything that was inside `<article class="py-4">` in the original) inside `<article class="article-body">`:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>linux terminal clash - Luka's Blog</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.1/font/bootstrap-icons.css">
    <link rel="stylesheet" href="/apple.css">
  </head>
  <body>
    <div class="reading-progress" id="progressBar"></div>

    <nav class="navbar navbar-expand-lg sticky-top">
      <div class="container">
        <a class="navbar-brand" href="/">Luka Mai</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item"><a class="nav-link" href="/">Home</a></li>
            <li class="nav-item"><a class="nav-link active" href="/blogs.html">Blogs</a></li>
            <li class="nav-item"><a class="nav-link" href="/about_me.html">About</a></li>
          </ul>
        </div>
      </div>
    </nav>

    <section class="tile-white">
      <article class="article-body">
        <!-- PASTE ARTICLE CONTENT HERE:
             Copy everything that was between <article class="py-4"> and </article>
             in the original blogs/linux terminal clash.html file.
             The .config-file and .filename elements will be styled by apple.css. -->
      </article>
    </section>

    <footer class="site-footer">
      <div class="footer-inner">
        <div class="footer-links">
          <a href="/blogs.html">← All Blogs</a>
          <a href="/">Home</a>
        </div>
        <p class="footer-legal">© 2026 Luka Mai. All rights reserved.</p>
      </div>
    </footer>

    <button class="back-to-top" id="backToTop" aria-label="返回顶部">
      <i class="bi bi-arrow-up"></i>
    </button>

    <script>
      window.addEventListener('scroll', () => {
        const winScroll = document.body.scrollTop || document.documentElement.scrollTop;
        const height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
        document.getElementById('progressBar').style.width = (winScroll / height * 100) + '%';
      });
      const backToTop = document.getElementById('backToTop');
      window.addEventListener('scroll', () => {
        backToTop.classList.toggle('visible', window.scrollY > 300);
      });
      backToTop.addEventListener('click', () => {
        window.scrollTo({ top: 0, behavior: 'smooth' });
      });
    </script>
  </body>
</html>
```

**Important:** The article title's gradient text style will be cancelled by `.article-body h1` in apple.css — no manual change needed in the HTML.

- [ ] **Step 3: Visually verify in browser**

Open `blogs/linux terminal clash.html`. Check:
- Light background throughout
- `.config-file` blocks have parchment background and blue filename text
- No dark backgrounds

- [ ] **Step 4: Commit**

```bash
git add "blogs/linux terminal clash.html"
git commit -m "feat: rewrite linux terminal clash blog post with Apple style"
```

---

## Task 8: Rewrite blogs/openclaw-macos-deploy.html

**Files:**
- Modify: `blogs/openclaw-macos-deploy.html`

- [ ] **Step 1: Read the article body content from the existing file**

Run: `grep -n "<article\|</article" "blogs/openclaw-macos-deploy.html"`

Then read the article body content to copy it.

- [ ] **Step 2: Replace the file with Apple-style wrapper**

Write the following to `blogs/openclaw-macos-deploy.html`, pasting the article body content inside `<article class="article-body">`:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>如何在 MacOS 上部署 OpenClaw - Luka's Blog</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.1/font/bootstrap-icons.css">
    <link rel="stylesheet" href="/apple.css">
  </head>
  <body>
    <div class="reading-progress" id="progressBar"></div>

    <nav class="navbar navbar-expand-lg sticky-top">
      <div class="container">
        <a class="navbar-brand" href="/">Luka Mai</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ms-auto">
            <li class="nav-item"><a class="nav-link" href="/">Home</a></li>
            <li class="nav-item"><a class="nav-link active" href="/blogs.html">Blogs</a></li>
            <li class="nav-item"><a class="nav-link" href="/about_me.html">About</a></li>
          </ul>
        </div>
      </div>
    </nav>

    <section class="tile-white">
      <article class="article-body">
        <!-- PASTE ARTICLE CONTENT HERE:
             Copy everything that was between <article class="py-4"> and </article>
             in the original blogs/openclaw-macos-deploy.html file. -->
      </article>
    </section>

    <footer class="site-footer">
      <div class="footer-inner">
        <div class="footer-links">
          <a href="/blogs.html">← All Blogs</a>
          <a href="/">Home</a>
        </div>
        <p class="footer-legal">© 2026 Luka Mai. All rights reserved.</p>
      </div>
    </footer>

    <button class="back-to-top" id="backToTop" aria-label="返回顶部">
      <i class="bi bi-arrow-up"></i>
    </button>

    <script>
      window.addEventListener('scroll', () => {
        const winScroll = document.body.scrollTop || document.documentElement.scrollTop;
        const height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
        document.getElementById('progressBar').style.width = (winScroll / height * 100) + '%';
      });
      const backToTop = document.getElementById('backToTop');
      window.addEventListener('scroll', () => {
        backToTop.classList.toggle('visible', window.scrollY > 300);
      });
      backToTop.addEventListener('click', () => {
        window.scrollTo({ top: 0, behavior: 'smooth' });
      });
    </script>
  </body>
</html>
```

- [ ] **Step 3: Visually verify in browser**

Open `blogs/openclaw-macos-deploy.html`. Check same Apple style as other blog posts.

- [ ] **Step 4: Commit**

```bash
git add "blogs/openclaw-macos-deploy.html"
git commit -m "feat: rewrite openclaw blog post with Apple style"
```

---

## Final verification

- [ ] **Cross-page check**

Open each of the 7 pages and confirm:
1. Nav is identical black bar across all pages (correct `active` link per page)
2. No page has a dark/gradient body background
3. All links are `#0066cc` (Action Blue) — no green, orange, or purple links
4. Footer is identical parchment with blue links across all pages
5. Blog post pages: article text is dark on white, code blocks are parchment

- [ ] **Final commit**

```bash
git add .
git commit -m "feat: complete Apple UI redesign across all pages"
```
