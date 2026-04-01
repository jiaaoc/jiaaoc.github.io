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
| `_sass/_custom.scss` | All new styles — palette, cards, stats bar, pills, timeline, nav, sidebar, publication entries, experience timeline |
| `_pages/about.md` | Restructure into: bio → stats bar → research interests (pills) → news (timeline) → selected publications → experience chips |
| `_pages/publication.md` | Add year-header accents, card-style entries, venue badges, styled pdf/code links, citation stats bar at top |
| `_pages/experience.md` | Timeline-style layout with vertical line + colored dots, card per role, card grouping for education/teaching/service/awards |
| `_pages/contact.md` | Card-based layout with styled links |
| `_includes/author-profile.html` | Modernize sidebar: terracotta photo border ring, styled social links, prominent CV download button |
| `_includes/masthead.html` | Warm-palette nav bar with terracotta active/hover states |
| `_config.yml` | No structural changes expected; minor tweaks only if needed |
| `_data/navigation.yml` | No changes |

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
- Stats bar: stack vertically on very small screens
- Experience chips: wrap naturally
- Cards: full width, reduced padding on mobile

## Implementation Notes
- All styles go in `_custom.scss` to avoid modifying theme core files
- About page content uses HTML directly in `about.md` (Jekyll supports inline HTML in markdown)
- Publications page stays as markdown lists but styled via CSS targeting `.page__content` selectors
- Experience page same approach — markdown content, CSS card styling via class wrappers
- No JavaScript required — pure CSS redesign
- No new dependencies or gems
