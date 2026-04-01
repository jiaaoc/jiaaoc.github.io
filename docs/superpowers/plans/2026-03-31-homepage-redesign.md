# Homepage Redesign Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Redesign all pages of Jiaao Chen's academic homepage with a warm terracotta/sage/sand palette, card-based layout, SVG logo, improved SEO, and updated README.

**Architecture:** Custom styles in `_sass/_custom.scss` (imported via `assets/css/main.scss`), inline HTML in markdown pages for card/timeline/badge structure, enhanced Liquid templates for sidebar and nav. No JS, no new dependencies.

**Tech Stack:** Jekyll, SCSS, Liquid templates, inline HTML in Markdown, SVG

**Spec:** `docs/superpowers/specs/2026-03-31-homepage-redesign-design.md`

---

## Chunk 1: Foundation — CSS System + SCSS Import + Config

### Task 1: Enable custom SCSS import

**Files:**
- Modify: `assets/css/main.scss` (add import at end)

- [ ] **Step 1: Add `@import "custom"` to main.scss**

At the very end of `assets/css/main.scss` (after `@import "print";` on line 41), add:

```scss
@import "custom";
```

- [ ] **Step 2: Create `_sass/_custom.scss` with palette variables and global card system**

Create `_sass/_custom.scss` with the complete style system:

```scss
/* ==========================================================================
   CUSTOM STYLES — Terracotta/Sage/Sand Palette
   ========================================================================== */

/* --- Palette Variables --- */
$terracotta:       #e07a5f;
$terracotta-tint:  #fef0ec;
$sage:             #81b29a;
$sage-tint:        #ecf4ef;
$sand:             #c89442;
$sand-tint:        #fef9ee;
$navy:             #1a1a2e;
$body-text:        #555;
$warm-bg:          #faf6f1;
$card-border:      #e8ddd0;
$warm-divider:     #f0ebe4;
$purple-tint:      #f3eef8;
$purple-text:      #8b6aaf;
$blue-tint:        #eef4f8;
$blue-text:        #5a8aab;

/* --- Global Overrides --- */
body {
  background: $warm-bg;
  color: $body-text;
  line-height: 1.7;
}

a {
  color: $terracotta;
  &:hover {
    color: darken($terracotta, 10%);
  }
}

/* --- Navigation Bar --- */
.masthead {
  background: $warm-bg;
  border-bottom: 1px solid $card-border;

  .masthead__inner-wrap {
    .masthead__menu {
      .greedy-nav {
        background: $warm-bg;

        a {
          color: $body-text;
          text-decoration: none;
          &:hover {
            color: $terracotta;
          }
        }

        .masthead__menu-item--lg a {
          color: $navy;
          font-weight: 700;
        }

        .visible-links {
          a {
            &:before {
              background: $terracotta;
            }
          }
        }
      }
    }
  }
}

.site-logo {
  display: inline-block;
  margin-right: 8px;
  vertical-align: middle;
  position: relative;
  top: -1px;
}

/* --- Sidebar / Author Profile --- */
.sidebar {
  .author__avatar {
    img {
      border-radius: 50%;
      border: 3px solid $terracotta;
      padding: 0;
    }
  }

  .author__content {
    .author__name {
      color: $navy;
      font-weight: 700;
    }
    .author__bio {
      color: $terracotta;
      font-size: 0.85em;
    }
  }

  .author__urls-wrapper {
    .author__urls {
      li {
        a {
          color: $body-text;
          text-decoration: none;
          padding: 4px 8px;
          border-radius: 6px;
          transition: background 0.2s, color 0.2s;

          &:hover {
            background: $terracotta-tint;
            color: $terracotta;
          }
        }
      }
    }
  }
}

.cv-download-btn {
  display: block;
  width: 100%;
  padding: 8px 16px;
  margin-top: 12px;
  background: $terracotta;
  color: #fff !important;
  text-align: center;
  border-radius: 8px;
  font-weight: 600;
  font-size: 0.85em;
  text-decoration: none !important;
  transition: background 0.2s;

  &:hover {
    background: darken($terracotta, 8%);
    color: #fff !important;
  }
}

/* --- Page Content Overrides --- */
.page__content {
  h2 {
    color: $navy;
    border-bottom-color: $card-border;
  }

  a {
    color: $terracotta;
    text-decoration: none;
    &:hover {
      text-decoration: underline;
    }
  }
}

/* --- Card System --- */
.card-section {
  background: #fff;
  border: 1.5px solid $card-border;
  border-radius: 10px;
  padding: 20px;
  margin-bottom: 16px;

  h2 {
    font-size: 1rem;
    font-weight: 600;
    color: $navy;
    margin: 0 0 12px 0;
    padding-bottom: 0;
    border-bottom: none;
    border-left: none;
    padding-left: 0;
  }
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 12px;

  h2 {
    margin: 0 !important;
  }
}

.view-all-link {
  color: $terracotta;
  font-size: 0.85em;
  text-decoration: none;
  white-space: nowrap;

  &:hover {
    text-decoration: underline;
  }
}

/* --- Stats Bar --- */
.stats-bar {
  display: flex;
  gap: 12px;
  margin-bottom: 16px;
}

.stat-tile {
  flex: 1;
  text-align: center;
  padding: 14px 8px;
  border-radius: 10px;

  .stat-number {
    font-size: 1.6rem;
    font-weight: 800;
    line-height: 1.2;
  }

  .stat-label {
    font-size: 0.75rem;
    color: $body-text;
    margin-top: 2px;
  }

  &.terracotta {
    background: $terracotta-tint;
    .stat-number { color: $terracotta; }
  }

  &.sage {
    background: $sage-tint;
    .stat-number { color: $sage; }
  }

  &.sand {
    background: $sand-tint;
    .stat-number { color: $sand; }
  }
}

/* --- Pill Tags --- */
.pill-tag {
  display: inline-block;
  padding: 4px 12px;
  border-radius: 20px;
  font-size: 0.82em;
  font-weight: 500;
  margin: 3px 2px;

  &.terracotta { background: $terracotta-tint; color: $terracotta; }
  &.sage       { background: $sage-tint; color: $sage; }
  &.sand       { background: $sand-tint; color: $sand; }
  &.purple     { background: $purple-tint; color: $purple-text; }
  &.blue       { background: $blue-tint; color: $blue-text; }
  &.gray       { background: #f1f1f1; color: #777; }
}

/* --- News Timeline --- */
.news-item {
  display: flex;
  align-items: baseline;
  gap: 12px;
  margin-bottom: 6px;
  line-height: 1.6;

  .news-date {
    font-weight: 600;
    font-size: 0.85em;
    white-space: nowrap;

    &.terracotta { color: $terracotta; }
    &.sage       { color: $sage; }
    &.sand       { color: $sand; }
    &.purple     { color: $purple-text; }
  }

  .news-text {
    color: $body-text;
    font-size: 0.9em;
  }
}

/* --- Publication Entries --- */
.pub-entry {
  padding-bottom: 14px;
  margin-bottom: 14px;
  border-bottom: 1px solid $warm-divider;

  &:last-child {
    border-bottom: none;
    margin-bottom: 0;
    padding-bottom: 0;
  }

  .pub-title {
    font-weight: 600;
    color: $navy;
    font-size: 0.95em;
  }

  .pub-authors {
    color: #888;
    font-size: 0.85em;
    margin: 2px 0;
  }

  .pub-venue {
    font-size: 0.82em;
    font-weight: 500;
    margin-right: 6px;
  }

  .pub-links a {
    display: inline-block;
    padding: 2px 10px;
    border-radius: 12px;
    font-size: 0.78em;
    margin-right: 4px;
    text-decoration: none;
    font-weight: 500;

    &.link-pdf {
      background: $sage-tint;
      color: $sage;
      &:hover { background: darken($sage-tint, 5%); }
    }

    &.link-code {
      background: $terracotta-tint;
      color: $terracotta;
      &:hover { background: darken($terracotta-tint, 5%); }
    }
  }
}

/* Venue badges */
.venue-neurips  { color: $terracotta; }
.venue-iclr     { color: $sage; }
.venue-emnlp    { color: $sand; }
.venue-acl      { color: $purple-text; }
.venue-arxiv    { color: #777; }
.venue-other    { color: $body-text; }

/* Publication page year headers */
.page__content h2 {
  border-bottom: none;
  border-left: 4px solid $terracotta;
  padding-left: 12px;
  padding-bottom: 0;
  margin-top: 1.5em;
}

/* Scholar link buttons on publications page */
.scholar-links {
  display: flex;
  gap: 8px;
  margin-bottom: 16px;

  a {
    display: inline-block;
    padding: 6px 16px;
    border-radius: 8px;
    font-size: 0.85em;
    font-weight: 500;
    text-decoration: none;

    &.btn-scholar {
      background: $terracotta;
      color: #fff;
      &:hover { background: darken($terracotta, 8%); }
    }

    &.btn-semantic {
      background: $sage;
      color: #fff;
      &:hover { background: darken($sage, 8%); }
    }
  }
}

/* --- Experience Timeline --- */
.experience-timeline {
  position: relative;
  padding-left: 28px;

  &::before {
    content: '';
    position: absolute;
    left: 8px;
    top: 8px;
    bottom: 8px;
    width: 2px;
    background: $card-border;
  }
}

.timeline-item {
  position: relative;
  margin-bottom: 20px;

  &::before {
    content: '';
    position: absolute;
    left: -24px;
    top: 8px;
    width: 12px;
    height: 12px;
    border-radius: 50%;
    border: 2px solid #fff;
  }

  &.dot-terracotta::before { background: $terracotta; }
  &.dot-sage::before       { background: $sage; }
  &.dot-sand::before       { background: $sand; }

  .timeline-card {
    background: #fff;
    border: 1.5px solid $card-border;
    border-radius: 10px;
    padding: 16px;
  }

  .timeline-company {
    font-weight: 700;
    color: $navy;
    a { color: $navy; text-decoration: none; &:hover { color: $terracotta; } }
  }

  .timeline-role {
    color: $terracotta;
    font-weight: 500;
    font-size: 0.9em;
  }

  .timeline-meta {
    color: #999;
    font-size: 0.82em;
    margin-bottom: 8px;
  }

  ul {
    margin: 4px 0 0 0;
    padding-left: 18px;
    li {
      font-size: 0.88em;
      line-height: 1.6;
    }
  }
}

/* --- Experience Chips (homepage) --- */
.experience-chips {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;

  .exp-chip {
    padding: 6px 14px;
    background: $warm-bg;
    border: 1px solid $card-border;
    border-radius: 8px;
    font-size: 0.85em;
    color: $navy;

    strong {
      font-weight: 700;
    }
  }
}

/* --- Contact Card --- */
.contact-card {
  background: #fff;
  border: 1.5px solid $card-border;
  border-radius: 10px;
  padding: 24px;
  max-width: 500px;

  .contact-item {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 10px 0;
    border-bottom: 1px solid $warm-divider;
    font-size: 0.92em;

    &:last-child {
      border-bottom: none;
    }

    i {
      color: $terracotta;
      width: 20px;
      text-align: center;
    }

    a {
      color: $body-text;
      text-decoration: none;
      &:hover { color: $terracotta; }
    }
  }
}

/* --- Sidebar Card Container --- */
.sidebar {
  .author__avatar + .author__content,
  > div[itemscope] {
    background: $warm-bg;
    border: 1.5px solid $card-border;
    border-radius: 12px;
    padding: 16px;
  }
}

/* --- Responsive --- */
@include breakpoint(max-width $small) {
  .stats-bar {
    flex-direction: column;
  }

  .card-section {
    padding: 12px;
  }

  .experience-timeline {
    padding-left: 0;

    &::before {
      display: none;
    }
  }

  .timeline-item {
    &::before {
      display: none;
    }
  }
}
```

- [ ] **Step 3: Verify build**

Run: `cd /Users/jiaaoc/Desktop/jiaaoc.github.io && bundle exec jekyll build 2>&1 | tail -5`
Expected: Build succeeds with no SCSS errors.

- [ ] **Step 4: Commit**

```bash
git add assets/css/main.scss _sass/_custom.scss
git commit -m "feat: add custom SCSS with terracotta/sage/sand palette and card system"
```

### Task 2: Update _config.yml with SEO fields and structured data keys

**Files:**
- Modify: `_config.yml`

- [ ] **Step 1: Update site description**

In `_config.yml`, change line 13:
```yaml
description              : &description "Jiaao Chen — AI researcher specializing in LLM agents, post-training, and reasoning. Founding Member at Eigen AI. Ph.D. Georgia Tech/Stanford."
```

- [ ] **Step 2: Set og_image**

In `_config.yml`, change line 65:
```yaml
og_image                 : "profile.jpg"
```

- [ ] **Step 3: Set twitter username**

In `_config.yml`, change line 60:
```yaml
  username               : &twitter "jiaao_chen"
```

- [ ] **Step 4: Add social profile links**

In `_config.yml`, under `social:` (around line 70), update:
```yaml
social:
  type                   : "Person"
  name                   : "Jiaao Chen"
  links:
    - "https://scholar.google.com/citations?user=Pi9IVvUAAAAJ&hl=en"
    - "https://github.com/jiaaoc"
    - "https://www.linkedin.com/in/jiaao-chen-4997b0116"
    - "https://twitter.com/jiaao_chen"
```

- [ ] **Step 5: Add structured data keys to author section**

In `_config.yml`, under `author:` (after line 87), add:
```yaml
  job_title        : "Founding Member of Technical Staff"
  works_for        : "Eigen AI"
  alumni_of        : "Georgia Institute of Technology"
```

- [ ] **Step 6: Commit**

```bash
git add _config.yml
git commit -m "feat: add SEO fields, og_image, social links, structured data keys"
```

### Task 3: Create SVG logo and update favicon

**Files:**
- Create: `images/logo.svg`
- Modify: `_includes/head/custom.html`

- [ ] **Step 1: Create `images/logo.svg`**

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 36 36" width="36" height="36">
  <rect width="36" height="36" rx="8" fill="#e07a5f"/>
  <text x="18" y="24" text-anchor="middle" font-family="-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif" font-size="16" font-weight="600" fill="#ffffff">JC</text>
</svg>
```

- [ ] **Step 2: Add SVG favicon and update theme-color in `_includes/head/custom.html`**

Add after the existing PNG favicon links (after line 19, before the shortcut icon line):
```html
<link rel="icon" type="image/svg+xml" href="{{ base_path }}/images/logo.svg">
```

Change line 24 from:
```html
<meta name="theme-color" content="#ffffff">
```
to:
```html
<meta name="theme-color" content="#e07a5f">
```

- [ ] **Step 3: Commit**

```bash
git add images/logo.svg _includes/head/custom.html
git commit -m "feat: add JC monogram SVG logo and update favicon/theme-color"
```

---

## Chunk 2: Templates — Masthead, Sidebar, SEO

### Task 4: Update masthead with logo and warm styling

**Files:**
- Modify: `_includes/masthead.html`

- [ ] **Step 1: Add inline SVG logo before site title**

Replace the site title link line (line 9):
```html
          <li class="masthead__menu-item masthead__menu-item--lg"><a href="{{ base_path }}/">{{ site.title }}</a></li>
```
with:
```html
          <li class="masthead__menu-item masthead__menu-item--lg"><a href="{{ base_path }}/"><span class="site-logo"><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 36 36" width="32" height="32"><rect width="36" height="36" rx="8" fill="#e07a5f"/><text x="18" y="24" text-anchor="middle" font-family="-apple-system,BlinkMacSystemFont,'Segoe UI',Helvetica,Arial,sans-serif" font-size="16" font-weight="600" fill="#fff">JC</text></svg></span>{{ site.title }}</a></li>
```

- [ ] **Step 2: Commit**

```bash
git add _includes/masthead.html
git commit -m "feat: add JC logo to navigation bar"
```

### Task 5: Modernize author profile sidebar

**Files:**
- Modify: `_includes/author-profile.html`

- [ ] **Step 1: Rewrite author-profile.html**

Replace the full contents of `_includes/author-profile.html` with:

```html
{% include base_path %}

{% if page.author and site.data.authors[page.author] %}
  {% assign author = site.data.authors[page.author] %}{% else %}{% assign author = site.author %}
{% endif %}

<div itemscope itemtype="http://schema.org/Person">

  <div class="author__avatar">
    {% if author.avatar contains "://" %}
      <img src="{{ author.avatar }}" alt="{{ author.name }}">
    {% else %}
      <img src="{{ author.avatar | prepend: "/images/" | prepend: base_path }}" class="author__avatar" alt="{{ author.name }}">
    {% endif %}
  </div>

  <div class="author__content">
    <h3 class="author__name">{{ author.name }}</h3>
    {% if author.bio %}<p class="author__bio">{{ author.bio }}</p>{% endif %}
  </div>

  <div class="author__urls-wrapper">
    <button class="btn btn--inverse">Follow</button>
    <ul class="author__urls social-icons">
      {% if author.location %}
        <li><i class="fa fa-fw fa-map-marker" aria-hidden="true"></i> {{ author.location }}</li>
      {% endif %}
      {% if author.employer %}
        <li><i class="fa fa-fw fa-building" aria-hidden="true"></i> {{ author.employer }}</li>
      {% endif %}
      {% if author.email %}
        <li><a href="mailto:{{ author.email }}"><i class="fas fa-fw fa-envelope" aria-hidden="true"></i> Email</a></li>
      {% endif %}
      {% if author.googlescholar %}
        <li><a href="{{ author.googlescholar }}"><i class="fas fa-fw fa-graduation-cap"></i> Google Scholar</a></li>
      {% endif %}
      {% if author.github %}
        <li><a href="https://github.com/{{ author.github }}"><i class="fab fa-fw fa-github" aria-hidden="true"></i> GitHub</a></li>
      {% endif %}
      {% if author.linkedin %}
        <li><a href="https://www.linkedin.com/in/{{ author.linkedin }}"><i class="fab fa-fw fa-linkedin" aria-hidden="true"></i> LinkedIn</a></li>
      {% endif %}
      {% if author.twitter %}
        <li><a href="https://twitter.com/{{ author.twitter }}"><i class="fab fa-fw fa-twitter-square" aria-hidden="true"></i> Twitter</a></li>
      {% endif %}
      {% if author.researchgate %}
        <li><a href="{{ author.researchgate }}"><i class="fab fa-fw fa-researchgate" aria-hidden="true"></i> ResearchGate</a></li>
      {% endif %}
      {% if author.orcid %}
        <li><a href="{{ author.orcid }}"><i class="ai ai-orcid-square ai-fw"></i> ORCID</a></li>
      {% endif %}
    </ul>
    <a href="{{ base_path }}/Jiaao_Chen_CV.pdf" class="cv-download-btn"><i class="fa fa-fw fa-download"></i> Download CV</a>
  </div>
</div>
```

- [ ] **Step 2: Commit**

```bash
git add _includes/author-profile.html
git commit -m "feat: modernize sidebar with streamlined links and CV download button"
```

### Task 6: Enhance SEO structured data

**Files:**
- Modify: `_includes/seo.html`

- [ ] **Step 1: Replace the Person schema block**

In `_includes/seo.html`, replace lines 115-125 (the `site.social` script block):

```html
{% if site.social %}
  <script type="application/ld+json">
    {
      "@context" : "http://schema.org",
      "@type" : "{% if site.social.type %}{{ site.social.type }}{% else %}Person{% endif %}",
      "name" : "{{ site.social.name | default: site.name }}",
      "url" : {{ seo_url | jsonify }},
      "sameAs" : {{ site.social.links | jsonify }}
    }
  </script>
{% endif %}
```

with:

```html
{% if site.social %}
  <script type="application/ld+json">
    {
      "@context" : "http://schema.org",
      "@type" : "{% if site.social.type %}{{ site.social.type }}{% else %}Person{% endif %}",
      "name" : "{{ site.social.name | default: site.name }}",
      "url" : {{ seo_url | jsonify }},
      "sameAs" : {{ site.social.links | jsonify }}{% if site.author.job_title %},
      "jobTitle" : {{ site.author.job_title | jsonify }}{% endif %}{% if site.author.works_for %},
      "worksFor" : {
        "@type" : "Organization",
        "name" : {{ site.author.works_for | jsonify }}
      }{% endif %}{% if site.author.alumni_of %},
      "alumniOf" : {
        "@type" : "CollegeOrUniversity",
        "name" : {{ site.author.alumni_of | jsonify }}
      }{% endif %}{% if site.author.avatar %},
      "image" : "{{ site.author.avatar | prepend: "/images/" | prepend: seo_url }}"{% endif %}
    }
  </script>
{% endif %}
```

- [ ] **Step 2: Commit**

```bash
git add _includes/seo.html
git commit -m "feat: enhance Person structured data with jobTitle, worksFor, alumniOf"
```

---

## Chunk 3: Homepage (about.md)

### Task 7: Rewrite about.md with impact-first layout

**Files:**
- Modify: `_pages/about.md`

- [ ] **Step 1: Rewrite about.md with full HTML structure**

Replace the entire contents of `_pages/about.md` with:

```markdown
---
permalink: /
title: "About me"
description: "Jiaao Chen's academic homepage. AI researcher working on LLM agents, post-training, and reasoning at Eigen AI."
excerpt: "Jiaao Chen's academic homepage. AI researcher working on LLM agents, post-training, and reasoning at Eigen AI."
author_profile: true
redirect_from: 
  - /about/
  - /about.html
  - /portfolio/
  - /portfolio.html
---

<div class="card-section">
  <p>Hello, I'm Jiaao Chen!</p>
  <p>I am a Founding Member of Technical Staff at <a href="https://www.eigen.ai/">Eigen AI</a>, where I lead the development of self-evolving multi-agent platforms for agentic AI systems. My work focuses on LLM post-training (SFT, GRPO/RL), tool-use agents, and multi-agent data pipelines.</p>
  <p>Previously, I was a Research Scientist at <a href="https://about.meta.com/">Meta</a> (GenAI team), where I worked on agentic post-training in TBD agent workstream, and an Applied Scientist at <a href="https://www.amazon.com/">Amazon</a>, working on LLM reasoning for e-commerce.</p>
  <p>I received my Ph.D. in Computer Science from <a href="https://www.gatech.edu/">Georgia Institute of Technology</a> / <a href="https://www.stanford.edu/">Stanford University</a> in 2024, advised by Prof. <a href="https://cs.stanford.edu/~diyiyang/">Diyi Yang</a>. I have 20+ first-author publications at top venues including NeurIPS, ICLR, EMNLP, and ACL.</p>
  <p>Before Georgia Tech, I obtained my bachelor's degree from <a href="http://www.zju.edu.cn/english/">Zhejiang University</a>, where I was in the ACEE Honor Class at Chu Kochen Honors College (top 40 out of 6,000 students).</p>
</div>

<!-- UPDATE STATS: last updated 2026-03-31 -->
<div class="stats-bar">
  <div class="stat-tile terracotta">
    <div class="stat-number">5,000+</div>
    <div class="stat-label">Citations</div>
  </div>
  <div class="stat-tile sage">
    <div class="stat-number">24</div>
    <div class="stat-label">h-index</div>
  </div>
  <div class="stat-tile sand">
    <div class="stat-number">20+</div>
    <div class="stat-label">First-Author Pubs</div>
  </div>
</div>

<div class="card-section">
  <h2>Research Interests</h2>
  <div>
    <span class="pill-tag terracotta">LLM Agents &amp; Tool Use</span>
    <span class="pill-tag sage">LLM Post-Training (SFT/RL)</span>
    <span class="pill-tag sand">LLM Reasoning</span>
    <span class="pill-tag purple">Data-Efficient NLP</span>
    <span class="pill-tag blue">Language Generation</span>
  </div>
</div>

<div class="card-section">
  <h2>News</h2>
  <div class="news-item"><span class="news-date terracotta">Jan. 2026</span> <span class="news-text">Joined <a href="https://www.eigen.ai/">Eigen AI</a> as Founding Member of Technical Staff.</span></div>
  <div class="news-item"><span class="news-date sage">2026</span> <span class="news-text">EigenData paper on self-evolving multi-agent platform for function-calling data released (<a href="https://arxiv.org/abs/2603.05553">arXiv</a>).</span></div>
  <div class="news-item"><span class="news-date sand">2024</span> <span class="news-text">DARG accepted at NeurIPS 2024; DyVal accepted at ICLR 2024.</span></div>
  <div class="news-item"><span class="news-date purple">May 2024</span> <span class="news-text">Completed Ph.D. from Georgia Tech / Stanford.</span></div>
</div>

<div class="card-section">
  <div class="card-header">
    <h2>Selected Publications</h2>
    <a href="/publication.html" class="view-all-link">View all →</a>
  </div>
  <div class="pub-entry">
    <div class="pub-title">EigenData: A Self-Evolving Multi-Agent Platform for Function-Calling Data Synthesis, Auditing, and Repair</div>
    <div class="pub-authors"><strong>Jiaao Chen</strong>, Jingyuan Qi, Mingye Gao, Wei-Chen Wang, Hanrui Wang, and Di Jin</div>
    <div><span class="pub-venue venue-arxiv">arXiv, 2026</span> <span class="pub-links"><a href="https://arxiv.org/abs/2603.05553" class="link-pdf">pdf</a></span></div>
  </div>
  <div class="pub-entry">
    <div class="pub-title">DARG: Dynamic Evaluation of Large Language Models via Adaptive Reasoning Graph</div>
    <div class="pub-authors">Zhehao Zhang, <strong>Jiaao Chen</strong>, and Diyi Yang</div>
    <div><span class="pub-venue venue-neurips">NeurIPS, 2024</span> <span class="pub-links"><a href="https://arxiv.org/abs/2406.17271" class="link-pdf">pdf</a></span></div>
  </div>
  <div class="pub-entry">
    <div class="pub-title">DyVal: Graph-informed Dynamic Evaluation of Large Language Models</div>
    <div class="pub-authors">Kaijie Zhu*, <strong>Jiaao Chen*</strong>, Jindong Wang, Neil Zhenqiang Gong, Diyi Yang, Xing Xie</div>
    <div><span class="pub-venue venue-iclr">ICLR, 2024</span> <span class="pub-links"><a href="https://arxiv.org/abs/2309.17167" class="link-pdf">pdf</a></span></div>
  </div>
  <div class="pub-entry">
    <div class="pub-title">Skills-in-context Prompting: Unlocking Compositionality in Large Language Models</div>
    <div class="pub-authors"><strong>Jiaao Chen</strong>, Xiaoman Pan, Dian Yu, Kaiqiang Song, Xiaoyang Wang, Dong Yu and Jianshu Chen</div>
    <div><span class="pub-venue venue-emnlp">EMNLP Findings, 2024</span> <span class="pub-links"><a href="https://arxiv.org/abs/2308.00304" class="link-pdf">pdf</a></span></div>
  </div>
</div>

<div class="card-section">
  <div class="card-header">
    <h2>Experience</h2>
    <a href="/experience.html" class="view-all-link">Full details →</a>
  </div>
  <div class="experience-chips">
    <span class="exp-chip"><strong>Eigen AI</strong> · 2026–</span>
    <span class="exp-chip"><strong>Meta</strong> · 2025</span>
    <span class="exp-chip"><strong>Amazon</strong> · 2024</span>
    <span class="exp-chip"><strong>Tencent AI</strong> · 2023</span>
    <span class="exp-chip"><strong>Amazon AWS</strong> · 2022</span>
    <span class="exp-chip"><strong>GT/Stanford</strong> · Ph.D. 2024</span>
  </div>
</div>
```

- [ ] **Step 2: Verify build**

Run: `cd /Users/jiaaoc/Desktop/jiaaoc.github.io && bundle exec jekyll build 2>&1 | tail -5`
Expected: Build succeeds.

- [ ] **Step 3: Commit**

```bash
git add _pages/about.md
git commit -m "feat: redesign homepage with impact-first layout, stats bar, pills, and cards"
```

---

## Chunk 4: Publications Page

### Task 8: Redesign publications page

**Files:**
- Modify: `_pages/publication.md`

- [ ] **Step 1: Rewrite publication.md with styled HTML structure**

Replace the entire contents of `_pages/publication.md` with the following complete file. Venue class mapping used: NeurIPS→`venue-neurips`, ICLR→`venue-iclr`, EMNLP/EMNLP Findings→`venue-emnlp`, ACL/ACL Findings→`venue-acl`, arXiv→`venue-arxiv`, all others (NAACL, AAAI, SIGIR, TACL, Comp. Linguistics, EACL, workshops)→`venue-other`.

````markdown
---
permalink: /publication.html
redirect_from: 
  - /publication/
  - /publications/
title: "Publications"
description: "Publications by Jiaao Chen. 5,000+ citations, h-index 24. Research in LLM agents, reasoning, and NLP."
excerpt: "Publications by Jiaao Chen. 5,000+ citations, h-index 24. Research in LLM agents, reasoning, and NLP."
author_profile: true
---

<!-- UPDATE STATS: last updated 2026-03-31 -->
<div class="stats-bar">
  <div class="stat-tile terracotta">
    <div class="stat-number">5,000+</div>
    <div class="stat-label">Citations</div>
  </div>
  <div class="stat-tile sage">
    <div class="stat-number">24</div>
    <div class="stat-label">h-index</div>
  </div>
  <div class="stat-tile sand">
    <div class="stat-number">30</div>
    <div class="stat-label">i10-index</div>
  </div>
</div>

<div class="scholar-links">
  <a href="https://scholar.google.com/citations?user=Pi9IVvUAAAAJ&hl=en" class="btn-scholar">Google Scholar</a>
  <a href="https://www.semanticscholar.org/author/Jiaao-Chen/47739850" class="btn-semantic">Semantic Scholar</a>
</div>

(\* denotes equal contribution)

## Preprints

<div class="pub-entry">
  <div class="pub-title">EigenData: A Self-Evolving Multi-Agent Platform for Function-Calling Data Synthesis, Auditing, and Repair</div>
  <div class="pub-authors"><strong>Jiaao Chen</strong>, Jingyuan Qi, Mingye Gao, Wei-Chen Wang, Hanrui Wang, and Di Jin</div>
  <div><span class="pub-venue venue-arxiv">arXiv, 2026</span> <span class="pub-links"><a href="https://arxiv.org/abs/2603.05553" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">From Self-Evolving Synthetic Data to Verifiable-Reward RL: Post-Training Multi-turn Interactive Tool-Using Agents</div>
  <div class="pub-authors">Jiaxuan Gao, <strong>Jiaao Chen</strong>, Chuyi He, Wei-Chen Wang, Shusheng Xu, Hanrui Wang, Di Jin, and Yi Wu</div>
  <div><span class="pub-venue venue-arxiv">arXiv, 2026</span> <span class="pub-links"><a href="https://arxiv.org/abs/2601.22607" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Maslab: A Unified and Comprehensive Codebase for LLM-based Multi-Agent Systems</div>
  <div class="pub-authors">Rui Ye, Keduan Huang, Qimin Wu, Yuzhu Cai, Tian Jin, Xianghe Pang, Xiangrui Liu, Jiaqi Su, Chen Qian, Bohan Tang, et al</div>
  <div><span class="pub-venue venue-arxiv">arXiv, 2025</span> <span class="pub-links"><a href="https://arxiv.org/abs/2505.16988" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Agentic Workflows for Conversational Human-AI Interaction Design</div>
  <div class="pub-authors">Arthur Caetano, Kavya Verma, Atieh Taheri, Radha Kumaran, Zichen Chen, <strong>Jiaao Chen</strong>, Tobias Hollerer, and Misha Sra</div>
  <div><span class="pub-venue venue-arxiv">arXiv, 2025</span> <span class="pub-links"><a href="https://arxiv.org/abs/2501.18002" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Standard Benchmarks Fail -- Auditing LLM Agents in Finance Must Prioritize Risk</div>
  <div class="pub-authors">Zichen Chen, <strong>Jiaao Chen</strong>, Jianda Chen, and Misha Sra</div>
  <div><span class="pub-venue venue-arxiv">arXiv, 2025</span> <span class="pub-links"><a href="https://arxiv.org/abs/2502.15865" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Are We There Yet? Revealing the Risks of Utilizing Large Language Models in Scholarly Peer Review</div>
  <div class="pub-authors">Rui Ye, Xianghe Pang, Jingyi Chai, <strong>Jiaao Chen</strong>, Zhenfei Yin, Zhen Xiang, Xiaowen Dong, Jing Shao, and Siheng Chen</div>
  <div><span class="pub-venue venue-arxiv">arXiv, 2024</span> <span class="pub-links"><a href="https://arxiv.org/abs/2412.01708" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Dynamic Skill Adaptation for Large Language Models</div>
  <div class="pub-authors"><strong>Jiaao Chen</strong> and Diyi Yang</div>
  <div><span class="pub-venue venue-arxiv">arXiv, 2024</span> <span class="pub-links"><a href="https://arxiv.org/abs/2412.19361" class="link-pdf">pdf</a></span></div>
</div>

## 2026

<div class="pub-entry">
  <div class="pub-title">WorkForceAgent-R1: Incentivizing Reasoning Capability in LLM-based Web Agents via Reinforcement Learning</div>
  <div class="pub-authors">Yuchen Zhuang, Di Jin, <strong>Jiaao Chen</strong>, Wenqi Shi, Hanrui Wang, and Chao Zhang</div>
  <div><span class="pub-venue venue-other">EACL, 2026</span> <span class="pub-links"><a href="https://arxiv.org/abs/2505.22942" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Learning Multi-step Reasoning via Persistent Latent State Propagation</div>
  <div class="pub-authors">Yixiao Li, <strong>Jiaao Chen</strong>, Xin Tang, Fangzhou Wu, Jiahui Yu, Haotian Qi, Wei Xuan, Hao Zhao, Peng Nie, and Di Jin</div>
  <div><span class="pub-venue venue-other">Workshop on Latent &amp; Implicit Thinking, 2026</span></div>
</div>

## 2025

<div class="pub-entry">
  <div class="pub-title">From Tasks to Teams: A Risk-First Evaluation Framework for Multi-Agent LLM Systems in Finance</div>
  <div class="pub-authors">Zichen Chen, Jianda Chen, <strong>Jiaao Chen</strong>, and Misha Sra</div>
  <div><span class="pub-venue venue-other">ICML 2025 Workshop</span></div>
</div>

## 2024

<div class="pub-entry">
  <div class="pub-title">DARG: Dynamic Evaluation of Large Language Models via Adaptive Reasoning Graph</div>
  <div class="pub-authors">Zhehao Zhang, <strong>Jiaao Chen</strong>, and Diyi Yang</div>
  <div><span class="pub-venue venue-neurips">NeurIPS, 2024</span> <span class="pub-links"><a href="https://arxiv.org/abs/2406.17271" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">From Scroll to Misbelief: Modeling the Unobservable Susceptibility to Misinformation on Social Media</div>
  <div class="pub-authors">Yanchen Liu, Mingyu Derek Ma, Wenna Qin, Azure Zhou, <strong>Jiaao Chen</strong>, Weiyan Shi, Wei Wang and Diyi Yang</div>
  <div><span class="pub-venue venue-emnlp">EMNLP, 2024</span> <span class="pub-links"><a href="https://arxiv.org/abs/2311.09630" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Skills-in-context Prompting: Unlocking Compositionality in Large Language Models</div>
  <div class="pub-authors"><strong>Jiaao Chen</strong>, Xiaoman Pan, Dian Yu, Kaiqiang Song, Xiaoyang Wang, Dong Yu and Jianshu Chen</div>
  <div><span class="pub-venue venue-emnlp">EMNLP Findings, 2024</span> <span class="pub-links"><a href="https://arxiv.org/abs/2308.00304" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">DyVal: Graph-informed Dynamic Evaluation of Large Language Models</div>
  <div class="pub-authors">Kaijie Zhu*, <strong>Jiaao Chen*</strong>, Jindong Wang, Neil Zhenqiang Gong, Diyi Yang, Xing Xie</div>
  <div><span class="pub-venue venue-iclr">ICLR, 2024</span> <span class="pub-links"><a href="https://arxiv.org/abs/2309.17167" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Can Large Language Models Transform Computational Social Science?</div>
  <div class="pub-authors">Caleb Ziems, William Held, Omar Shaikh, <strong>Jiaao Chen</strong>, Zhehao Zhang and Diyi Yang</div>
  <div><span class="pub-venue venue-other">Computational Linguistics, 2024</span> <span class="pub-links"><a href="https://arxiv.org/abs/2305.03514" class="link-pdf">pdf</a></span></div>
</div>

## 2023

<div class="pub-entry">
  <div class="pub-title">Unlearn What You Want to Forget: Efficient Unlearning for LLMs</div>
  <div class="pub-authors"><strong>Jiaao Chen</strong> and Diyi Yang</div>
  <div><span class="pub-venue venue-emnlp">EMNLP, 2023</span> <span class="pub-links"><a href="https://arxiv.org/abs/2310.20150" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">A Cheaper and Better Diffusion Language Model with Soft-Masked Noise</div>
  <div class="pub-authors"><strong>Jiaao Chen</strong> and Diyi Yang</div>
  <div><span class="pub-venue venue-emnlp">EMNLP, 2023</span> <span class="pub-links"><a href="https://arxiv.org/abs/2304.04746" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Is ChatGPT a General-Purpose Natural Language Processing Task Solver?</div>
  <div class="pub-authors">Chengwei Qin, Aston Zhang, Zhuosheng Zhang, <strong>Jiaao Chen</strong>, Michihiro Yasunaga, and Diyi Yang</div>
  <div><span class="pub-venue venue-emnlp">EMNLP, 2023</span> <span class="pub-links"><a href="https://arxiv.org/abs/2302.06476" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Mitigating Biases in Hate Speech Detection from A Causal Perspective</div>
  <div class="pub-authors">Zhehao Zhang, <strong>Jiaao Chen</strong>, and Diyi Yang</div>
  <div><span class="pub-venue venue-emnlp">EMNLP Findings, 2023</span> <span class="pub-links"><a href="https://aclanthology.org/2023.findings-emnlp.440/" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Where Does Your News Come From? Predicting Information Pathways in Social Media</div>
  <div class="pub-authors">Alexander K Taylor, Nuan Wen, Po-Nien Kung, <strong>Jiaao Chen</strong>, Violet Peng, and Wei Wang</div>
  <div><span class="pub-venue venue-other">SIGIR, 2023</span> <span class="pub-links"><a href="https://dl.acm.org/doi/abs/10.1145/3539618.3592087" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Controllable Conversation Generation with Conversation Structures via Diffusion Models</div>
  <div class="pub-authors"><strong>Jiaao Chen</strong>, and Diyi Yang</div>
  <div><span class="pub-venue venue-acl">ACL Findings, 2023</span> <span class="pub-links"><a href="https://aclanthology.org/2023.findings-acl.454/" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Human-in-the-loop Abstractive Dialogue Summarization</div>
  <div class="pub-authors"><strong>Jiaao Chen</strong>, Mohan Dodda, and Diyi Yang</div>
  <div><span class="pub-venue venue-acl">ACL Findings, 2023</span> <span class="pub-links"><a href="https://aclanthology.org/2023.findings-acl.584/" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Compositional Data Augmentation for Abstractive Conversation Summarization</div>
  <div class="pub-authors">Siru Ouyang, <strong>Jiaao Chen</strong>, Jiawei Han, and Diyi Yang</div>
  <div><span class="pub-venue venue-acl">ACL, 2023</span> <span class="pub-links"><a href="https://aclanthology.org/2023.acl-long.82/" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Parameter-Efficient Fine-Tuning Design Spaces</div>
  <div class="pub-authors"><strong>Jiaao Chen</strong>, Aston Zhang, Xingjian Shi, Mu Li, Alex Smola, and Diyi Yang</div>
  <div><span class="pub-venue venue-iclr">ICLR, 2023</span> <span class="pub-links"><a href="https://arxiv.org/abs/2301.01821" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">An Empirical Survey of Data Augmentation for Limited Data Learning in NLP</div>
  <div class="pub-authors"><strong>Jiaao Chen*</strong>, Derek Tam*, Colin Raffel, Mohit Bansal, and Diyi Yang</div>
  <div><span class="pub-venue venue-other">TACL, 2023</span> <span class="pub-links"><a href="https://arxiv.org/abs/2106.07499" class="link-pdf">pdf</a></span></div>
</div>

## 2022

<div class="pub-entry">
  <div class="pub-title">When FLUE Meets FLANG: Benchmarks and Large Pretrained Language Model for Financial Domain</div>
  <div class="pub-authors">Raj Sanjay Shah, Kunal Chawla, Dheeraj Eidnani, Agam Shah, Wendi Du, Sudheer Chava, Natraj Raman, Charese Smiley, <strong>Jiaao Chen</strong>, and Diyi Yang</div>
  <div><span class="pub-venue venue-emnlp">EMNLP, 2022</span> <span class="pub-links"><a href="https://arxiv.org/abs/2211.00083" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">E-VALUE: Understanding Dialect Disparity in NLU</div>
  <div class="pub-authors">Caleb Ziems*, <strong>Jiaao Chen*</strong>, Camille Harris, Jessica Anderson, and Diyi Yang</div>
  <div><span class="pub-venue venue-acl">ACL, 2022</span> <span class="pub-links"><a href="https://arxiv.org/abs/2204.03031" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Focus on the Action: Learning to Highlight and Summarize Jointly for Email To-Do Items Summarization</div>
  <div class="pub-authors">Kexun Zhang, <strong>Jiaao Chen</strong>, Diyi Yang</div>
  <div><span class="pub-venue venue-acl">ACL, 2022</span> <span class="pub-links"><a href="https://aclanthology.org/2022.findings-acl.323/" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Leveraging Expert Guided Adversarial Augmentation For Improving Generalization in Named Entity Recognition</div>
  <div class="pub-authors">Aaron Reich, <strong>Jiaao Chen</strong>, Aastha Agrawal, Yanzhe Zhang, Diyi Yang</div>
  <div><span class="pub-venue venue-acl">ACL Findings, 2022</span> <span class="pub-links"><a href="https://arxiv.org/abs/2203.10693" class="link-pdf">pdf</a></span></div>
</div>

## 2021

<div class="pub-entry">
  <div class="pub-title">Simple Conversational Data Augmentation for Semi-supervised Abstractive Dialogue Summarization</div>
  <div class="pub-authors"><strong>Jiaao Chen</strong>, Diyi Yang</div>
  <div><span class="pub-venue venue-emnlp">EMNLP, 2021</span> <span class="pub-links"><a href="https://aclanthology.org/2021.emnlp-main.530/" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">HiddenCut: Simple Data Augmentation for Natural Language Understanding with Better Generalization</div>
  <div class="pub-authors"><strong>Jiaao Chen</strong>, Dinghan Shen, Weizhu Chen, and Diyi Yang</div>
  <div><span class="pub-venue venue-acl">ACL, 2021</span> <span class="pub-links"><a href="https://arxiv.org/abs/2106.00149" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Structure-Aware Abstractive Conversation Summarization via Discourse and Action Graphs</div>
  <div class="pub-authors"><strong>Jiaao Chen</strong>, Diyi Yang</div>
  <div><span class="pub-venue venue-other">NAACL, 2021</span> <span class="pub-links"><a href="https://arxiv.org/abs/2104.08400" class="link-pdf">pdf</a> <a href="https://github.com/GT-SALT/Structure-Aware-BART" class="link-code">code</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Continual Learning for Text Classification with Information Disentanglement Based Regularization</div>
  <div class="pub-authors">Yufan Huang, Yanzhe Zhang, <strong>Jiaao Chen</strong>, Xuezhi Wang and Diyi Yang</div>
  <div><span class="pub-venue venue-other">NAACL, 2021</span> <span class="pub-links"><a href="https://arxiv.org/abs/2104.05489" class="link-pdf">pdf</a> <a href="https://github.com/GT-SALT/IDBR" class="link-code">code</a></span></div>
</div>

## 2020

<div class="pub-entry">
  <div class="pub-title">Weakly-Supervised Hierarchical Models for Predicting Persuasive Strategies in Good-faith Textual Requests</div>
  <div class="pub-authors"><strong>Jiaao Chen</strong>, Diyi Yang</div>
  <div><span class="pub-venue venue-other">AAAI, 2021</span> <span class="pub-links"><a href="https://arxiv.org/abs/2101.06351" class="link-pdf">pdf</a> <a href="https://github.com/GT-SALT/Persuasion_Strategy_WVAE" class="link-code">code</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Multi-View Sequence-to-Sequence Models with Conversational Structure for Abstractive Dialogue Summarization</div>
  <div class="pub-authors"><strong>Jiaao Chen</strong>, Diyi Yang</div>
  <div><span class="pub-venue venue-emnlp">EMNLP, 2020</span> <span class="pub-links"><a href="https://arxiv.org/abs/2010.01672" class="link-pdf">pdf</a> <a href="https://github.com/GT-SALT/Multi-View-Seq2Seq" class="link-code">code</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Local Additivity Based Data Augmentation for Semi-supervised NER</div>
  <div class="pub-authors"><strong>Jiaao Chen*</strong>, Zhenghui Wang*, Ran Tian, Zichao Yang and Diyi Yang</div>
  <div><span class="pub-venue venue-emnlp">EMNLP, 2020</span> <span class="pub-links"><a href="https://arxiv.org/abs/2010.01677" class="link-pdf">pdf</a> <a href="https://github.com/GT-SALT/LADA" class="link-code">code</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Examining the Ordering of Rhetorical Strategies in Persuasive Requests</div>
  <div class="pub-authors">Omar Shaikh, <strong>Jiaao Chen</strong>, Jon Saad-Falcon, Polo Chau and Diyi Yang</div>
  <div><span class="pub-venue venue-emnlp">EMNLP Findings, 2020</span> <span class="pub-links"><a href="https://arxiv.org/abs/2010.04625" class="link-pdf">pdf</a> <a href="https://github.com/GT-SALT/Persuasive-Orderings" class="link-code">code</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">MixText: Linguistically-Informed Interpolation of Hidden Space for Semi-Supervised Text Classification</div>
  <div class="pub-authors"><strong>Jiaao Chen</strong>, Zichao Yang, Diyi Yang</div>
  <div><span class="pub-venue venue-acl">ACL, 2020</span> <span class="pub-links"><a href="https://arxiv.org/abs/2004.12239" class="link-pdf">pdf</a> <a href="https://github.com/GT-SALT/MixText" class="link-code">code</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Semi-supervised Models via Data Augmentation for Classifying Interactive Affective Responses</div>
  <div class="pub-authors"><strong>Jiaao Chen*</strong>, Yuwei Wu*, Diyi Yang</div>
  <div><span class="pub-venue venue-other">AAAI Workshop on Affective Content Analysis, 2020</span> <span class="pub-links"><a href="https://arxiv.org/abs/2004.10972" class="link-pdf">pdf</a> <a href="https://github.com/GT-SALT/AAAI_CLF" class="link-code">code</a></span></div>
</div>

## 2019

<div class="pub-entry">
  <div class="pub-title">Let's Make Your Request More Persuasive: Modeling Persuasive Strategies via Semi Supervised Neural Nets on Crowdfunding Platforms</div>
  <div class="pub-authors">Diyi Yang*, <strong>Jiaao Chen*</strong>, Zichao Yang, Dan Jurafsky, Eduard Hovy</div>
  <div><span class="pub-venue venue-other">NAACL, 2019 (oral)</span> <span class="pub-links"><a href="https://aclanthology.org/N19-1364/" class="link-pdf">pdf</a></span></div>
</div>

<div class="pub-entry">
  <div class="pub-title">Incorporating Structured Commonsense Knowledge in Story Completion</div>
  <div class="pub-authors"><strong>Jiaao Chen</strong>, Jianshu Chen, Zhou Yu</div>
  <div><span class="pub-venue venue-other">AAAI, 2019</span> <span class="pub-links"><a href="https://arxiv.org/abs/1811.00625" class="link-pdf">pdf</a></span></div>
</div>
````

- [ ] **Step 2: Verify build**

Run: `cd /Users/jiaaoc/Desktop/jiaaoc.github.io && bundle exec jekyll build 2>&1 | tail -5`

- [ ] **Step 3: Commit**

```bash
git add _pages/publication.md
git commit -m "feat: redesign publications page with venue badges and styled entries"
```

---

## Chunk 5: Experience + Contact Pages

### Task 9: Redesign experience page with timeline layout

**Files:**
- Modify: `_pages/experience.md`

- [ ] **Step 1: Rewrite experience.md with timeline HTML**

Replace the entire contents of `_pages/experience.md` with:

````markdown
---
permalink: /experience.html
redirect_from: 
  - /experience/
title: "Experience"
description: "Professional experience of Jiaao Chen. Eigen AI, Meta, Amazon, Georgia Tech/Stanford."
excerpt: "Professional experience of Jiaao Chen. Eigen AI, Meta, Amazon, Georgia Tech/Stanford."
author_profile: true
---

## Professional Experience

<div class="experience-timeline">

<div class="timeline-item dot-terracotta">
<div class="timeline-card">
<div class="timeline-company"><a href="https://www.eigen.ai/">Eigen AI</a></div>
<div class="timeline-role">Founding Member of Technical Staff</div>
<div class="timeline-meta">Palo Alto, USA · Jan. 2026 – Present</div>
<ul>
<li>Leading EigenData, a self-evolving multi-agent platform for function-calling data synthesis and quality assurance</li>
<li>Building EigenLoop, a full post-training pipeline (SFT, GRPO/RL, evaluation) for production agentic AI systems</li>
</ul>
</div>
</div>

<div class="timeline-item dot-sage">
<div class="timeline-card">
<div class="timeline-company"><a href="https://about.meta.com/">Meta</a> (MSL)</div>
<div class="timeline-role">Research Scientist</div>
<div class="timeline-meta">Menlo Park, USA · Mar. 2025 – Jan. 2026</div>
<ul>
<li>Built agentic synthetic data generation pipeline with verified tasks and LLM-as-judge for agentic RL in TBD agent workstream</li>
<li>Led agentic post-training that improved Llama 4 Maverick's BFCL function-calling performance from ~50 to 72</li>
</ul>
</div>
</div>

<div class="timeline-item dot-sand">
<div class="timeline-card">
<div class="timeline-company"><a href="https://www.amazon.com/">Amazon</a></div>
<div class="timeline-role">Applied Scientist</div>
<div class="timeline-meta">Palo Alto, USA · May 2024 – Mar. 2025</div>
<ul>
<li>Improved LLM reasoning for modeling customer shopping behaviors and personalized recommendation</li>
</ul>
</div>
</div>

<div class="timeline-item dot-terracotta">
<div class="timeline-card">
<div class="timeline-company"><a href="https://ai.tencent.com/">Tencent AI (US)</a></div>
<div class="timeline-role">Research Intern</div>
<div class="timeline-meta">Seattle, USA · May 2023 – Aug. 2023</div>
<ul>
<li>Developed Skills-in-Context Prompting for compositional reasoning in LLMs (EMNLP 2024)</li>
</ul>
</div>
</div>

<div class="timeline-item dot-sage">
<div class="timeline-card">
<div class="timeline-company"><a href="https://aws.amazon.com/">Amazon (AWS)</a></div>
<div class="timeline-role">Applied Scientist Intern</div>
<div class="timeline-meta">Santa Clara, USA · June 2022 – Jan. 2023</div>
<ul>
<li>Parameter-efficient fine-tuning design spaces (ICLR 2023); Diffusion language model (EMNLP 2023)</li>
</ul>
</div>
</div>

<div class="timeline-item dot-sand">
<div class="timeline-card">
<div class="timeline-company"><a href="https://allenai.org/">Allen Institute for AI (AI2)</a></div>
<div class="timeline-role">Research Intern, Mosaic Team</div>
<div class="timeline-meta">Seattle, USA · June 2021 – Sep. 2021</div>
<ul>
<li>Compositional data augmentation for commonsense QA with Yejin Choi's group</li>
</ul>
</div>
</div>

<div class="timeline-item dot-terracotta">
<div class="timeline-card">
<div class="timeline-company"><a href="https://www.microsoft.com/en-us/research/">Microsoft Research</a></div>
<div class="timeline-role">Researcher, Dynamics 365 AI</div>
<div class="timeline-meta">Seattle, USA · Dec. 2020 – May 2021</div>
<ul>
<li>Created HiddenCut (ACL 2021) and Mixture of Virtual Prompts for efficient fine-tuning</li>
</ul>
</div>
</div>

<div class="timeline-item dot-sage">
<div class="timeline-card">
<div class="timeline-company">Georgia Institute of Technology / Stanford University</div>
<div class="timeline-role">Research Assistant</div>
<div class="timeline-meta">Aug. 2019 – May 2024</div>
<ul>
<li>Advisor: Prof. Diyi Yang. Published 20+ first-author papers at NeurIPS, ICLR, EMNLP, ACL, NAACL</li>
</ul>
</div>
</div>

<div class="timeline-item dot-sand">
<div class="timeline-card">
<div class="timeline-company">Carnegie Mellon University</div>
<div class="timeline-role">Research Intern</div>
<div class="timeline-meta">Sep. 2018 – Mar. 2019</div>
<ul>
<li>Advised by Prof. Robert Kraut</li>
</ul>
</div>
</div>

<div class="timeline-item dot-terracotta">
<div class="timeline-card">
<div class="timeline-company">UC Davis</div>
<div class="timeline-role">Visiting Researcher</div>
<div class="timeline-meta">Jun. 2018 – Aug. 2018</div>
<ul>
<li>Working with Prof. Zhou Yu</li>
</ul>
</div>
</div>

</div>

## Education

<div class="card-section">
<p><strong>Ph.D. in Computer Science</strong>, Georgia Institute of Technology / Stanford University, Aug. 2019 – May 2024<br>
Advisor: Prof. Diyi Yang</p>
<p><strong>B.Eng. in Computer Science and Technology</strong>, Zhejiang University, Sep. 2015 – Jul. 2019<br>
Minor in Advanced Honor Class of Engineering Education, Chu Kochen Honors College (40/6,000)</p>
</div>

## Teaching &amp; Advising

<div class="card-section">
<ul>
<li>Teaching Assistant, NLP (CS-4650/7650), Georgia Tech, with Prof. Mark Riedl, Spring 2023</li>
<li>Teaching Assistant, NLP (CS-4650/7650), Georgia Tech, with Prof. Diyi Yang, Spring 2020</li>
<li>Teaching Assistant, Computer Organization, Zhejiang University, Spring 2018</li>
<li>Advised Master's Students: Aaron Reich, Aastha Agrawal, Yufan Huang, Kunal Chawla, Nikhil Gupta (2020–2022)</li>
<li>Advised Undergraduate Students: Zhehao Zhang, Siru Ouyang, Mohan Dodda, Wenna Qin, Kexun Zhang, and others (2019–2024)</li>
<li>Co-advised students published at ACL, EMNLP, NeurIPS, and SIGIR</li>
</ul>
</div>

## Professional Service

<div class="card-section">
<p><strong>Area Chair:</strong> ARR 2025 (April, October)</p>
<p><strong>Program Committee / Reviewer:</strong>
<span class="pill-tag terracotta">ACL 2021–2024</span>
<span class="pill-tag sage">EMNLP 2020–2024</span>
<span class="pill-tag sand">NAACL 2021</span>
<span class="pill-tag purple">ICLR 2022–2023</span>
<span class="pill-tag blue">NeurIPS 2025</span>
<span class="pill-tag gray">ICML 2025</span>
<span class="pill-tag gray">CHI 2023</span>
<span class="pill-tag gray">UIST 2022</span>
<span class="pill-tag gray">WWW 2021</span>
<span class="pill-tag gray">AAAI 2020–2021</span>
<span class="pill-tag gray">IJHCI 2023</span>
</p>
<p><strong>Conference Volunteer:</strong> ACL 2020</p>
<p><strong>Organizer:</strong> Georgia Tech NLP Seminar (2019–2021)</p>
</div>

## Selected Awards &amp; Honors

<div class="card-section">
<ul>
<li>Outstanding Undergraduate Thesis, Zhejiang University, <span style="color:#999">2019</span></li>
<li>Honorable Mention, MCM/ICM Mathematical Contest in Modeling, <span style="color:#999">2017</span></li>
<li>Academic Physics Contest, Zhejiang University, fourth place, <span style="color:#999">2017</span></li>
<li>ACEE Honor Class, Chu Kochen Honors College, Zhejiang University (40/6,000), <span style="color:#999">2016</span></li>
<li>Scholarship for Academic Achievement, Zhejiang University, <span style="color:#999">2016</span></li>
<li>Scholarship for All-around Achievement, Zhejiang University, <span style="color:#999">2016</span></li>
<li>ACM School Trial, Zhejiang University, third prize, <span style="color:#999">2016</span></li>
</ul>
</div>
````

- [ ] **Step 2: Verify build**

Run: `cd /Users/jiaaoc/Desktop/jiaaoc.github.io && bundle exec jekyll build 2>&1 | tail -5`

- [ ] **Step 3: Commit**

```bash
git add _pages/experience.md
git commit -m "feat: redesign experience page with timeline layout and card sections"
```

### Task 10: Redesign contact page

**Files:**
- Modify: `_pages/contact.md`

- [ ] **Step 1: Rewrite contact.md with card layout**

```markdown
---
permalink: /contact.html
redirect_from: 
  - /contact/
title: "Contact"
description: "Contact Jiaao Chen — email, Google Scholar, GitHub, LinkedIn, Twitter."
excerpt: "Contact Jiaao Chen — email, Google Scholar, GitHub, LinkedIn, Twitter."
author_profile: true
---

<div class="contact-card">
  <div class="contact-item">
    <i class="fas fa-fw fa-envelope"></i>
    <a href="mailto:chenjiaao1998@gmail.com">chenjiaao1998@gmail.com</a>
  </div>
  <div class="contact-item">
    <i class="fas fa-fw fa-globe"></i>
    <a href="https://www.jiaaochen.com">jiaaochen.com</a>
  </div>
  <div class="contact-item">
    <i class="fas fa-fw fa-graduation-cap"></i>
    <a href="https://scholar.google.com/citations?user=Pi9IVvUAAAAJ&hl=en">Google Scholar</a>
  </div>
  <div class="contact-item">
    <i class="fab fa-fw fa-github"></i>
    <a href="https://github.com/jiaaoc">GitHub</a>
  </div>
  <div class="contact-item">
    <i class="fab fa-fw fa-linkedin"></i>
    <a href="https://www.linkedin.com/in/jiaao-chen-4997b0116">LinkedIn</a>
  </div>
  <div class="contact-item">
    <i class="fab fa-fw fa-twitter"></i>
    <a href="https://twitter.com/jiaao_chen">@jiaao_chen</a>
  </div>
</div>
```

- [ ] **Step 2: Commit**

```bash
git add _pages/contact.md
git commit -m "feat: redesign contact page with card layout"
```

---

## Chunk 6: README + Final Verification

### Task 11: Update README

**Files:**
- Modify: `README.md`

- [ ] **Step 1: Replace README.md**

```markdown
# Jiaao Chen — Academic Homepage

Personal academic website for Jiaao Chen, built with Jekyll on the AcademicPages theme.

## About

Jiaao Chen is a Founding Member of Technical Staff at Eigen AI, specializing in LLM agents, post-training, and reasoning. Ph.D. from Georgia Tech/Stanford (2024).

- Live site: https://www.jiaaochen.com
- Google Scholar: https://scholar.google.com/citations?user=Pi9IVvUAAAAJ

## Local Development

1. Install dependencies: `bundle install`
2. Serve locally: `bundle exec jekyll liveserve`
3. Open http://localhost:4000

## Structure

- `_pages/` — Main pages (about, publications, experience, contact)
- `_sass/_custom.scss` — Custom styles (terracotta/sage/sand palette)
- `_includes/` — Template partials (sidebar, nav, SEO)
- `_config.yml` — Site configuration
- `images/` — Profile photo, logo, favicons

## Design

Warm terracotta + sage + sand color palette with card-based layout. See `docs/superpowers/specs/` for the full design spec.
```

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: replace generic AcademicPages README with project-specific one"
```

### Task 12: Final build verification

- [ ] **Step 1: Full build test**

Run: `cd /Users/jiaaoc/Desktop/jiaaoc.github.io && bundle exec jekyll build 2>&1`
Expected: Clean build, no errors or warnings (deprecation warnings from old gems are OK).

- [ ] **Step 2: Verify generated pages exist**

Run: `ls _site/index.html _site/publication.html _site/experience.html _site/contact.html`
Expected: All four files exist.

- [ ] **Step 3: Local serve for visual verification**

Run: `cd /Users/jiaaoc/Desktop/jiaaoc.github.io && bundle exec jekyll serve --port 4000 &`
Then open http://localhost:4000 and visually verify:
- Homepage: stats bar, research pills, news timeline, selected pubs, experience chips
- Publications: year headers with left border, venue badges, styled links
- Experience: timeline with dots, card sections
- Contact: centered card with icons
- Sidebar: terracotta photo ring, CV download button
- Nav: JC logo, warm styling
