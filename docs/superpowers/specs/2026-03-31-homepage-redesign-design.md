# Homepage Redesign — Design Spec

## Overview

Redesign Jiaao Chen's academic homepage (Jekyll/AcademicPages theme) with a modern, warm, approachable aesthetic. The redesign covers all pages: homepage (about), publications, experience, and contact.

## Design Decisions

- **Layout:** Enhanced sidebar + card-based main content (Option B from brainstorm)
- **Color palette:** Terracotta + Sage / Sand (Option D from brainstorm)
  - Primary: Terracotta `#e07a5f`
  - Secondary: Sage green `#81b29a`
  - Tertiary: Sand/gold `#c89442`
  - Text: Dark navy `#1a1a2e`
  - Body text: `#555`
  - Background: Warm off-white `#faf6f1`
  - Card background: `#ffffff`
  - Card border: `#e8ddd0`
  - Light tints: Terracotta `#fef0ec`, Sage `#ecf4ef`, Sand `#fef9ee`
- **Content arrangement:** Impact-First (Option A from brainstorm)
- **Typography:** Existing sans-serif stack, increased line-height (1.7 for body), slightly larger base size

## Files to Modify

| File | Change |
|------|--------|
| `assets/css/main.scss` | **Add `@import "custom";` at the end** — required for `_custom.scss` to load (currently not imported) |
| `_sass/_custom.scss` | All new styles — palette, cards, stats bar, pills, timeline, nav, sidebar, publication entries, experience timeline |
| `_pages/about.md` | Restructure into: bio → stats bar → research interests (pills) → news (timeline) → selected publications → experience chips. Uses inline HTML with CSS class wrappers. |
| `_pages/publication.md` | Restructure with inline HTML: wrap each venue in `<span class="venue-neurips">` etc. for colored badges, wrap entries in `<div class="pub-entry">`, add citation stats bar HTML at top |
| `_pages/experience.md` | Restructure with inline HTML: wrap each role in `<div class="timeline-item">`, add timeline structure with dots/line, wrap sections in `<div class="card-section">` |
| `_pages/contact.md` | Card-based layout with styled links (inline HTML) |
| `_includes/author-profile.html` | Modernize sidebar: terracotta photo border ring, styled social links, prominent CV download button |
| `_includes/masthead.html` | Warm-palette nav bar with terracotta active/hover states, inline SVG logo |
| `_includes/seo.html` | Add enhanced Person structured data with `jobTitle`, `worksFor`, `alumniOf` from new `_config.yml` keys |
| `_includes/head/custom.html` | Add SVG favicon link (keep existing PNG favicons), update `theme-color` to `#e07a5f` |
| `_config.yml` | SEO fields: `description`, `og_image`, `twitter.username`, `social.links`, `social.type`; new keys for structured data: `author.job_title`, `author.works_for`, `author.alumni_of` |
| `_data/navigation.yml` | No changes |
| `images/logo.svg` | New SVG logo file |
| `README.md` | Replace with project-specific README |

## Homepage (about.md) — Section by Section

### Sidebar (author-profile.html)
- Profile photo: circular with 3px `#e07a5f` border ring
- Name: bold, `#1a1a2e`
- Title: `#e07a5f`
- Location: muted gray
- Social links: rounded items with hover states, icon + label
- **Download CV** button: solid terracotta background, white text, full-width, rounded
- Sidebar card: `#faf6f1` background, `#e8ddd0` border, `border-radius: 12px`

### 1. Bio Card
- White card, warm border, `border-radius: 10px`
- Existing intro paragraph text, clean typography
- No heading — the text speaks for itself

### 2. Stats Bar
- Three side-by-side metric tiles in a flex row
- **5,000+ Citations** — terracotta tint background `#fef0ec`, number in `#e07a5f`
- **h-index 24** — sage tint `#ecf4ef`, number in `#81b29a`
- **20+ First-Author** — sand tint `#fef9ee`, number in `#c89442`
- Large bold numbers (24-28px), small label below
- `border-radius: 10px`, no border (tinted background is enough)

### 3. Research Interests Card
- Section heading: "Research Interests", `#1a1a2e`, bold
- Each interest as a pill/tag with its own accent color:
  - LLM Agents & Tool Use → terracotta tint
  - LLM Post-Training → sage tint
  - LLM Reasoning → sand tint
  - Data-Efficient NLP → light purple `#f3eef8` / `#8b6aaf`
  - Language Generation → light blue `#eef4f8` / `#5a8aab`
- Pills: `border-radius: 20px`, padding `4px 12px`

### 4. News Card
- Section heading: "News"
- Each entry: colored date label (rotating terracotta/sage/sand) + description
- Most recent first, compact line-height
- Max ~5 entries visible

### 5. Selected Publications Card
- Section heading: "Selected Publications" with "View all →" link (terracotta) aligned right
- Top 3-4 papers:
  - Paper title in bold `#1a1a2e`
  - Authors on next line, muted
  - Venue + year as colored text (`#e07a5f`)
  - [pdf] link as small sage-colored link
- Entries separated by thin warm divider (`#f0ebe4`)

### 6. Experience Chips Card
- Section heading: "Experience" with "Full details →" link aligned right
- Compact chips: `Company · Year range` in warm-tinted rounded boxes
- Shows: Eigen AI · 2026–, Meta · 2025, Amazon · 2024, GT/Stanford · Ph.D.

## Publications Page

### Top Section
- Citation stats bar (same component as homepage)
- Links to Google Scholar and Semantic Scholar as styled buttons

### Publication Entries
- Each publication rendered as a clean block within its year group
- Year headers: `h2` with terracotta left-border accent (4px `#e07a5f` left border)
- Per entry:
  - Title in bold `#1a1a2e`
  - Authors: muted, with user's name highlighted in bold
  - Venue: as a colored pill badge
    - NeurIPS → terracotta
    - ICLR → sage
    - EMNLP → sand
    - ACL → purple
    - arXiv → gray
    - Other → default muted
  - [pdf] and [code] links: small rounded buttons with terracotta/sage styling
- Entries within a year separated by thin warm dividers
- Equal contribution notation (`*`) preserved as-is

## Experience Page

### Professional Experience
- Vertical timeline layout:
  - Thin vertical line (`#e8ddd0`) on the left
  - Colored dots on the line (rotating terracotta/sage/sand)
  - Each role as a card to the right of the dot:
    - Company name + link: bold, `#1a1a2e`
    - Role title: `#e07a5f`
    - Dates + location: muted
    - Bullet points: clean, standard styling
  - Cards: white, warm border, rounded

### Education
- Same card treatment as experience, but simpler (no timeline, just stacked cards)

### Teaching & Advising
- Single card with clean list styling
- TA roles and advised students

### Professional Service
- Single card with role categories (Area Chair, Reviewer, etc.)
- Venues as inline pills

### Awards & Honors
- Single card with clean list
- Award names with year in muted text

## Contact Page
- Single centered card with:
  - Email (mailto link, terracotta)
  - Social links as styled icon+label rows
- Consistent warm card styling

## Navigation Bar (masthead.html)
- Background: `#faf6f1` (warm off-white)
- Site title: `#1a1a2e`, bold
- Nav links: `#555`, hover → `#e07a5f`
- Active page: `#e07a5f` with subtle bottom border
- Clean bottom border: `1px solid #e8ddd0`

## Global Card System (CSS)
- `.card-section`: white bg, `border: 1.5px solid #e8ddd0`, `border-radius: 10px`, `padding: 20px`, `margin-bottom: 16px`
- `.card-section h2`: `font-size: 1rem`, `font-weight: 600`, `color: #1a1a2e`, `margin-bottom: 12px`
- `.stats-bar`: flex row, gap 12px
- `.stat-tile`: flex-1, centered, tinted background, large number + small label
- `.pill-tag`: inline-block, rounded, padded, tinted bg + matching text
- `.pub-entry`: padding-bottom, border-bottom warm divider
- `.timeline-item`: flex row with dot + card
- `.view-all-link`: terracotta, small, aligned right

## Responsive Behavior

- On mobile: sidebar collapses above content (existing theme behavior, preserved)
- Stats bar: `flex-wrap: wrap` — tiles stack on screens below `$small` breakpoint (~600px)
- Experience chips: `flex-wrap: wrap` — wrap naturally
- Cards: full width, padding reduced to `12px` on screens below `$small`
- Timeline layout: on mobile, hide vertical line, stack cards normally
- Uses existing theme breakpoint variables: `$small`, `$medium`, `$large`, `$x-large` from `_variables.scss`

## Site Logo

Create an inline SVG logo for the navigation bar and favicon. Design:
- Monogram "JC" in a rounded square
- Background: terracotta `#e07a5f`
- Letters: white, clean sans-serif weight 600
- Size: 36x36px in nav, scalable
- Rounded corners: 8px
- Used in `_includes/masthead.html` next to site title
- Also generate a favicon.svg version for `_includes/head/custom.html`

Files to modify/create:
| File | Change |
|------|--------|
| `_includes/masthead.html` | Add inline SVG logo before site title |
| `_includes/head/custom.html` | Add SVG favicon link |
| `images/logo.svg` | Standalone SVG file for reuse |

## SEO Improvements

### _config.yml changes
- Add `description` with keyword-rich text: "Jiaao Chen — AI researcher specializing in LLM agents, post-training, and reasoning. Founding Member at Eigen AI. Ph.D. Georgia Tech/Stanford."
- Set `og_image` to `profile.jpg` (for social sharing previews)
- Set `twitter.username` to `jiaao_chen` (top-level `twitter:` block, line 60 — this is what `seo.html` reads for Twitter Card meta tags, distinct from `author.twitter`)
- Add `social.links` array with Google Scholar, GitHub, LinkedIn, Twitter URLs
- Set `social.type` to `Person`
- Add new author keys for structured data: `author.job_title: "Founding Member of Technical Staff"`, `author.works_for: "Eigen AI"`, `author.alumni_of: "Georgia Institute of Technology"`

### Page-level SEO
- Add `description` and `excerpt` frontmatter to each page:
  - `about.md`: "Jiaao Chen's academic homepage. AI researcher working on LLM agents, post-training, and reasoning at Eigen AI."
  - `publication.md`: "Publications by Jiaao Chen. 5,000+ citations, h-index 24. Research in LLM agents, reasoning, and NLP."
  - `experience.md`: "Professional experience of Jiaao Chen. Eigen AI, Meta, Amazon, Georgia Tech/Stanford."
  - `contact.md`: "Contact Jiaao Chen — email, Google Scholar, GitHub, LinkedIn, Twitter."

### Structured Data (seo.html)

Enhance the existing Person schema (lines 115-125) with richer fields:
- `jobTitle`: read from `site.author.job_title`
- `worksFor`: `{ "@type": "Organization", "name": site.author.works_for }`
- `alumniOf`: `{ "@type": "CollegeOrUniversity", "name": site.author.alumni_of }`
- `sameAs`: read from existing `site.social.links` array
- `image`: `site.author.avatar | prepend: "/images/" | prepend: base_path`
- Keep existing schema logic, add Liquid conditionals for new fields (e.g., `{% if site.author.job_title %}"jobTitle": {{ site.author.job_title | jsonify }},{% endif %}`)

### head/custom.html

- Add SVG favicon `<link>` alongside existing PNG favicons (keep all existing favicon links)
- Update `theme-color` meta tag from `#ffffff` to `#e07a5f` (terracotta)

## README Update

Replace the generic AcademicPages README with a project-specific one:

```
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

## Implementation Notes

- **Critical:** `assets/css/main.scss` must add `@import "custom";` at the end for any styles to load
- All styles go in `_sass/_custom.scss` to avoid modifying theme core SCSS files
- `about.md`, `publication.md`, `experience.md`, and `contact.md` all use inline HTML with CSS class wrappers (Jekyll renders HTML in markdown files)
- Publication venue badges require explicit `<span class="venue-XYZ">` wrappers in `publication.md` — pure CSS cannot distinguish venue text content
- Experience timeline requires `<div class="timeline-item">` wrappers in `experience.md` — plain markdown lists cannot create the timeline layout
- No JavaScript required — pure CSS + HTML restructuring
- No new dependencies or gems
- SVG logo is inline in masthead (no external image dependency)
- Stats bar values (citations, h-index, first-author count) are hardcoded in `about.md` and `publication.md` — must be manually updated when they change
