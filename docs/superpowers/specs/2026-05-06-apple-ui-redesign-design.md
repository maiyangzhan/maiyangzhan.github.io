# Apple UI Redesign — Design Spec

**Date:** 2026-05-06
**Scope:** maiyangzhan.github.io — all pages
**Approach:** Keep Bootstrap framework; override all visual styles with Apple design language from DESIGN.md

---

## Goals

Replace the current dark-tech (deep blue/black gradient, multi-color, Bootstrap dark theme) with the Apple design language described in DESIGN.md:

- Near-invisible UI that puts content first
- Alternating full-bleed white/parchment ↔ near-black tile sections
- Single Action Blue (#0066cc) for all interactive elements
- No decorative gradients, no UI shadows, no second accent color
- Clean typographic hierarchy at 17px body

**Constraint:** No hero photography available — design must rely on typography and tile rhythm rather than product imagery.

---

## Design Tokens (CSS Variables)

Replace all `:root` CSS variables across every page:

```css
:root {
  /* Surfaces */
  --color-canvas:       #ffffff;
  --color-parchment:    #f5f5f7;
  --color-tile-dark:    #272729;
  --color-tile-dark-2:  #2a2a2c;
  --color-nav-black:    #000000;

  /* Text */
  --color-ink:          #1d1d1f;
  --color-muted:        #6e6e73;
  --color-on-dark:      #ffffff;
  --color-muted-dark:   #cccccc;

  /* Accent — single brand color */
  --color-primary:      #0066cc;
  --color-primary-dark: #2997ff;   /* links on dark tiles only */

  /* Borders */
  --color-hairline:     #e0e0e0;
  --color-divider-soft: rgba(0,0,0,0.08);

  /* Spacing */
  --spacing-section:    80px;
  --spacing-card:       24px;
}
```

---

## Typography

Remove Bootstrap's font stack. Apply across all pages:

```css
body {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, sans-serif;
  font-size: 17px;
  font-weight: 400;
  line-height: 1.47;
  letter-spacing: -0.374px;
  color: var(--color-ink);
  background: var(--color-canvas);
}
```

Headline scale:

| Class          | Size  | Weight | Line-height | Letter-spacing |
|----------------|-------|--------|-------------|----------------|
| `.hero-display`| 56px  | 600    | 1.07        | -0.28px        |
| `.display-lg`  | 40px  | 600    | 1.10        | 0              |
| `.lead`        | 21px  | 400    | 1.14        | 0              |
| `.body`        | 17px  | 400    | 1.47        | -0.374px       |
| `.caption`     | 14px  | 400    | 1.43        | -0.224px       |
| `.nav-link`    | 12px  | 400    | 1.0         | -0.12px        |

Weight ladder: 400 / 600 only (no 500, no 700 except taglines).

---

## Components

### Global Nav
- Background: `#000` (pure black)
- Height: 44px
- Brand mark: simple text or Unicode symbol (no gradient logo icon)
- Nav links: 12px / 400 / rgba(255,255,255,0.85)
- Spacing: links ~10px horizontal padding
- Sticky, `z-index` above tiles
- Mobile (≤834px): collapse to brand + hamburger

### Tile System (replaces all section backgrounds)

Every page section is a full-width tile. No borders between tiles — the background color change is the divider.

| Tile              | Background      | Text color     |
|-------------------|-----------------|----------------|
| `.tile-white`     | `#ffffff`       | `#1d1d1f`      |
| `.tile-parchment` | `#f5f5f7`       | `#1d1d1f`      |
| `.tile-dark`      | `#272729`       | `#ffffff`      |
| `.tile-dark-2`    | `#2a2a2c`       | `#ffffff`      |

Tile padding: `80px 0` desktop / `48px 0` mobile (≤640px).
Inner content: `max-width: 980px; margin: 0 auto; padding: 0 22px`.

### Buttons
- `.btn-primary`: background `#0066cc`, text white, `border-radius: 9999px`, padding `11px 22px`, font-size 17px
- `.btn-ghost`: transparent background, `color: #0066cc`, `border: 1px solid #0066cc`, same radius/padding
- Active state: `transform: scale(0.95)` on all buttons
- No shadows on buttons

### Blog Cards (on parchment tile)
- Background: `#ffffff`
- Border: `1px solid #e0e0e0`
- Border-radius: 18px
- Padding: 24px
- Grid: 3-col desktop / 2-col tablet / 1-col mobile
- Tag: 11px / 600 / `#6e6e73` / uppercase
- Title: 17px / 600 / `#1d1d1f`
- Excerpt: 14px / `#6e6e73`
- Link: `color: #0066cc`, 14px

### Footer
- Background: `#f5f5f7`
- Top border: `1px solid #e0e0e0`
- Padding: 40px 22px
- Links: 14px / `#0066cc`
- Legal: 12px / `#6e6e73`

---

## Page-by-Page Layout

### index.html — Homepage

Tile stack (top → bottom):

1. **Global Nav** — black, sticky
2. **Hero Tile** (white) — `hero-display` name, `lead` subtitle, two pill CTAs (primary + ghost)
3. **Blog List Tile** (parchment) — `display-lg` heading, 3-column blog cards
4. **About Tile** (dark) — `display-lg` heading, one-line bio, single primary CTA, skill chips
5. **Footer** (parchment)

### blogs.html — Blog List

1. **Global Nav**
2. **Hero Tile** (white) — page title "博客", subtitle
3. **Full Blog List Tile** (parchment) — all posts as cards, possibly 2-col or 1-col list
4. **Footer**

### about_me.html — About Page

1. **Global Nav**
2. **Hero Tile** (white) — name + title + one-liner
3. **Bio Tile** (parchment) — longer text sections (skills, experience, links)
4. **Contact/Links Tile** (dark) — GitHub, email, social links as Action Blue links on dark
5. **Footer**

### Blog Post Pages (blogs/*.html)

1. **Global Nav**
2. **Article Header Tile** (white) — post title in `display-lg`, date/tag in caption
3. **Article Body Tile** (white, or alternating) — single column, `max-width: 700px`, 17px body text, `line-height: 1.47`
4. **Footer**

---

## What to Remove / Override

- Remove `data-bs-theme="dark"` from `<html>`
- Remove all `:root` gradient/glow variables (`--bg-primary`, `--bg-secondary`, `--color-purple`, `--color-green`, `--color-orange`)
- Remove all `background: linear-gradient(...)` from body, navbar, cards, hero sections
- Remove all `box-shadow` from buttons, cards, nav brand icon
- Remove Bootstrap `.bg-dark`, `.card.bg-dark`, any dark-card overrides
- Replace Bootstrap `.navbar-dark` with custom black nav
- Remove logo gradient icon — replace with plain text brand
- Remove multi-color accent variables; use only `--color-primary: #0066cc`

---

## Bootstrap Compatibility Notes

- Keep Bootstrap grid (`.container`, `.row`, `.col-*`) for responsive layout
- Keep Bootstrap collapse for mobile nav
- Override Bootstrap's color variables via `:root` — Bootstrap 5.3 reads from CSS custom properties
- Set `data-bs-theme` to nothing (light, or remove entirely)
- Bootstrap cards: override `.card` with tile-card styles; remove `.card` shadows via `--bs-card-box-shadow: none`

---

## Responsive Breakpoints

| Breakpoint    | Width     | Changes                                          |
|---------------|-----------|--------------------------------------------------|
| Desktop       | ≥1069px   | Full layout, 3-col cards, hero-display 56px      |
| Small desktop | 1024–1068 | Same layout, minor padding adjustment            |
| Tablet        | 834–1023  | 2-col cards, nav starts collapsing               |
| Mobile        | ≤833px    | Nav collapses to hamburger, 1-col cards          |
| Small mobile  | ≤640px    | Tile padding 48px, hero font drops to 34px       |
