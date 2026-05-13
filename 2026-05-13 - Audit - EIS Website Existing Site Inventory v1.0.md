# EIS Consulting Website — Existing Site Inventory v1.0

**Audit date:** 2026-05-13  
**Audited branch:** `audit/site-inventory`  
**Auditor:** Claude Code (read-only inspection)  
**Commissioned by:** Damo, Founder, EIS Consulting Ltd  
**Purpose:** Pre-rebuild baseline — Stage 1 of four-stage rebuild process

---

## 1. Repo State

### File Tree (top three levels)

```
eisconsulting-website/
├── .github/
│   └── workflows/
│       └── azure-static-web-apps-witty-cliff-0ea22e003.yml
├── src/
│   ├── accountancy/
│   │   └── index.html
│   ├── assets/
│   │   ├── .keep
│   │   ├── 180 px.png
│   │   ├── 192 px.png
│   │   ├── 48 px.png
│   │   ├── 512 px.png
│   │   ├── apple-touch-icon.png
│   │   ├── eis-consulting-logo-transx2.png
│   │   ├── eis-icon-transparent.png
│   │   ├── favicon-16.png
│   │   ├── favicon-32.png
│   │   ├── og.png
│   │   └── styles.css
│   ├── contact/
│   │   └── index.html
│   ├── general-practice/
│   │   └── index.html
│   ├── legal/
│   │   └── index.html
│   ├── privacy-policy/
│   │   └── index.html
│   ├── terms-of-use/
│   │   └── index.html
│   ├── favicon.png
│   ├── index.html
│   └── og.png
└── README.md
```

**Total tracked files (excluding `.git`):** 27  
**`/docs` folder:** Does not exist — audit placed at repo root.

### Git State

| Item | Detail |
|---|---|
| Current branch | `audit/site-inventory` |
| Production branch | `main` |
| First commit date | 2026-01-26 (UTC) |
| Last commit date | 2026-01-29 15:02 UTC |
| Total commits | 150 (all commits to date across all branches) |
| Last commit hash | `118a090` |
| Commit messages | Uniformly "Update index.html" — no structured commit convention in use |

### CI/CD Config

**File:** `.github/workflows/azure-static-web-apps-witty-cliff-0ea22e003.yml`

GitHub Actions workflow deploying to **Azure Static Web Apps** (free/standard tier). Trigger conditions:

- **Push to `main`** → deploy
- **PR opened/synchronised/reopened against `main`** → build and deploy preview environment
- **PR closed** → tear down preview environment

Key workflow config values:

```yaml
app_location:    "./src"   # source root
api_location:    ""        # no serverless API
output_location: "./src"   # same as source — no build step
```

### Build Tooling

**None.** There is no `package.json`, no bundler (Webpack, Vite, Parcel, etc.), no preprocessor (Sass, PostCSS), and no template engine. The site is plain HTML and CSS, served verbatim from `./src`. `app_location` equals `output_location` in the workflow, which confirms no build transformation occurs.

---

## 2. Pages

| # | File path | Apparent purpose | Intended URL | Status |
|---|---|---|---|---|
| 1 | `src/index.html` | Home / Landing — primary marketing page, service overview, sector cards | `/` | Live |
| 2 | `src/general-practice/index.html` | Sector offering — AI in General Practice (NHS GP practices) | `/general-practice/` | Live (stub) |
| 3 | `src/legal/index.html` | Sector offering — AI in Legal Services (waitlist + info cards) | `/legal/` | Coming soon |
| 4 | `src/accountancy/index.html` | Sector offering — AI in Accountancy (waitlist form) | `/accountancy/` | Coming soon |
| 5 | `src/contact/index.html` | Contact / Booking — email CTA for AI Compliance Diagnostic | `/contact/` | Live (stub) |
| 6 | `src/privacy-policy/index.html` | Legal — full Privacy Policy (UK GDPR compliant template) | `/privacy-policy/` | Live |
| 7 | `src/terms-of-use/index.html` | Legal — Terms of Use (template, 10 sections) | `/terms-of-use/` | Live |

**Total pages: 7**

### Notable observations

- **General Practice** (`src/general-practice/index.html:53–56`): the "What's on this page" card contains placeholder text ("We help GP practices make defensible, inspection-ready decisions…") identical to the hero subtitle. This is a stub, not a completed page.
- **Contact** (`src/contact/index.html:39`): a draft/internal note is visible as live content: _"For now, use email booking. We can add a scheduler later (Microsoft Bookings or similar)."_ — this text is in `.sub` class and rendered as body copy to all visitors.
- **Accountancy** page embeds a Microsoft Forms iframe but has no supporting copy beyond the hero kicker and subtitle.
- **Privacy Policy** (`src/privacy-policy/index.html:54`): contains an HTML comment visible in page source: `<!-- OPTIONAL: add Company No / VAT No if you want -->`.

---

## 3. CSS Architecture

### Files

| File | Location | Lines | Notes |
|---|---|---|---|
| `styles.css` | `src/assets/styles.css` | 380 | Single shared stylesheet, linked via absolute path `/assets/styles.css` |

**One stylesheet. No CSS modules, no component-scoped styles, no preprocessor output files.**

### Methodology

**Ad-hoc / utility-influenced semantic CSS.** The approach is closer to a handcrafted component library than a recognised methodology:

- No strict BEM (Block__Element--Modifier) naming. Class names are flat and semantic (`.btn`, `.card`, `.hero`, `.nav`, `.footer-grid`).
- Some modifier variants exist (`.btn.primary`, `.hero--compact`, `.h1--sm`, `.stack--lg`) using a BEM-modifier-style double-hyphen, but inconsistently applied.
- No utility class framework (Tailwind, Tachyons). Occasional inline `style` attributes used for layout tweaks (e.g. `src/index.html:124`: `style="margin-top:14px;"`).
- Logical grouping by component via CSS comments (e.g. `/* Header */`, `/* Core components */`, `/* Footer */`).

### CSS Custom Properties (Design Tokens)

All defined in `:root` at `src/assets/styles.css:1–12`:

```css
:root {
  --bg:     #0b1220;                       /* page background */
  --card:   #0f1a2e;                       /* card background */
  --text:   #e8eefc;                       /* primary text */
  --muted:  #b8c6e6;                       /* secondary/muted text */
  --line:   rgba(232,238,252,.12);         /* borders and dividers */
  --accent: #6aa6ff;                       /* primary accent (blue) */
  --accent2:#7cf0d6;                       /* secondary accent (mint/teal) */
  --radius: 16px;                          /* card/container corner radius */
  --shadow: 0 12px 30px rgba(0,0,0,.35);  /* card shadow */
  --max:    1120px;                        /* max content width */
}
```

**Dead CSS:** `.home-layout` and `.home-sidebar` classes (`styles.css:165–166`) are defined but not used in any HTML file.

---

## 4. Design Tokens

### Colour Palette

| Token / usage | Value | Role |
|---|---|---|
| `--bg` | `#0b1220` | Page background (deep navy) |
| `--card` | `#0f1a2e` | Card background |
| Card rendered | `rgba(15,26,46,.78)` | Semi-transparent card surface (`styles.css:253`) |
| `--text` | `#e8eefc` | Primary body text (near-white) |
| `--muted` | `#b8c6e6` | Secondary text, nav links, subtitles |
| Smallprint | `rgba(184,198,230,.95)` | Footer small text (`styles.css:358`) — close to `--muted` but hardcoded separately |
| `--line` | `rgba(232,238,252,.12)` | Borders, `hr.sep`, card borders |
| `--accent` | `#6aa6ff` | Primary accent — gradient start, focus ring, active underline |
| `--accent2` | `#7cf0d6` | Secondary accent — gradient end |
| Primary button gradient | `linear-gradient(135deg, #6aa6ff, #7cf0d6)` | Primary CTA fill |
| Primary button text | `#08101d` | Dark near-black text on gradient button |
| Header background | `rgba(11,18,32,.75)` | Frosted glass nav bar |
| Body radial glow 1 | `rgba(106,166,255,.18)` | Background ambient light (accent) |
| Body radial glow 2 | `rgba(124,240,214,.12)` | Background ambient light (accent2) |
| `theme-color` meta | `#0b1220` | Mobile browser UI colour |

### Typography Stack

**Font family** (`styles.css:18`):

```css
font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Arial,
             "Apple Color Emoji", "Segoe UI Emoji";
```

System font stack only. **No web fonts loaded** (no Google Fonts, Adobe Fonts, or self-hosted `.woff2` files).

| Class / element | Size | Line-height | Weight | Notes |
|---|---|---|---|---|
| `body` | (inherited) | `1.5` | normal | Base |
| `.h1` | `42px` | `1.08` | (bold, inherited) | Max-width `18ch` |
| `.h1` (mobile <980px) | `36px` | `1.08` | — | — |
| `.h1--sm` | `34px` | `1.08` | — | — |
| `.h1--sm` (mobile) | `30px` | `1.08` | — | — |
| `.sub` | `18px` | `1.5` | normal | Max-width `70ch` |
| `.section-title` (h2) | `18px` | `1.5` | normal | — |
| `.card h3` | `18px` | `1.5` | normal | — |
| `.links a` (nav) | `14px` | — | `600` | Mobile: `13px` |
| `.small` | `14px` | — | normal | — |
| `.site-footer` | `13px` | — | normal | — |
| `.footer-title` | `13px` | — | `800` | — |
| `.badge` | `12px` | — | normal | — |
| `.tag` | `12px` | — | `800` | — |
| `.smallprint` | `12px` | — | normal | — |
| `.kicker` | `12px` | — | `700` | Uppercase, letter-spacing `.4px` |
| `.brand` | (inherited) | — | `700` | letter-spacing `.2px` |
| `.btn` | (inherited) | — | `800` | — |

### Spacing Scale

No formal scale defined. Values used in the stylesheet:

`6px` · `10px` · `12px` · `14px` · `16px` · `18px` · `22px` · `24px` · `26px` · `42px`

Key spacing declarations:
- `.container` padding: `24px` (`styles.css:35`)
- `.nav` padding: `14px 24px` (`styles.css:54`)
- `.hero` padding: `42px 0 22px`, gap: `18px` (`styles.css:179–181`)
- `.card` padding: `18px` (`styles.css:258`)
- `.grid` gap: `14px` (`styles.css:243`)
- `hr.sep` margin: `22px 0` (`styles.css:276`)
- `.btn` padding: `12px 16px` (`styles.css:229`)

### Border-Radius Values

| Context | Value | Source |
|---|---|---|
| `--radius` (cards, embeds) | `16px` | `styles.css:9` |
| `.btn` | `12px` | `styles.css:232` |
| Pill shapes (`.badge`, `.tag`, active underline) | `999px` | `styles.css:83`, `styles.css:273`, `styles.css:116` |
| Focus-visible outline | `10px` | `styles.css:32` |

### Shadow Definitions

| Token | Value | Source |
|---|---|---|
| `--shadow` | `0 12px 30px rgba(0,0,0,.35)` | `styles.css:10` |

Applied to `.card` only (`styles.css:257`). No other shadow definitions.

### Breakpoint Values

| Breakpoint | Value | Usage |
|---|---|---|
| Mobile/tablet | `max-width: 980px` | Nav grid reflow, 3-col → 1-col grid, h1 size reduction, iframe height change |
| Desktop | `min-width: 980px` | `.home-layout` 2-col, `.footer-grid` 3-col |

**Single breakpoint at 980px.** No intermediate breakpoints (no tablet-specific states). No `min-width: 1120px` guard for content beyond `--max`.

---

## 5. Components

All components are HTML-in-CSS pattern classes. No JS framework components. No web components.

### Navigation / Header

**Structure:** `<header class="header">` → `<div class="nav">` → `<div class="brand">` + `<nav class="links">`

| Class | Element | Description |
|---|---|---|
| `.header` | `<header>` | Sticky top bar; frosted glass background (`backdrop-filter: blur(10px)`) |
| `.nav` | `<div>` | Flex row (desktop) / 2×2 grid (mobile); holds brand and links |
| `.brand` | `<div>` | Column flex; logo link + badge tagline |
| `.brand-link` | `<a>` | Inline-flex logo anchor with `aria-label` |
| `.logo` | `<img>` | 40px tall logo; 34px mobile |
| `.badge` | `<span>` | Pill label with tagline; truncates with ellipsis on desktop, wraps on mobile |
| `.links` | `<nav>` | Flex row of nav `<a>` tags |
| `.links a.active` / `[aria-current="page"]` | `<a>` | Active state: full text colour + 2px gradient underline |

### Hero Section

**Structure:** `<section class="hero">` (variant: `class="hero hero--compact"`)

| Class | Element | Description |
|---|---|---|
| `.hero` | `<section>` | Grid with 18px gap; 42px top padding |
| `.hero--compact` | modifier | Reduced padding (24px top) and gap (12px); used on Privacy Policy / Terms pages |
| `.kicker` | `<div>` | Uppercase muted label above heading |
| `.h1` | `<h1>` | Main page heading, 42px |
| `.h1--sm` | modifier on `<h1>` | Smaller heading variant (34px), used on legal pages |
| `.sub` | `<p>` | Subtitle text at 18px, muted colour |
| `.small` | `<p>` | Disclaimer/secondary text at 14px |
| `.ctas` | `<div>` | Flex row of button links |

### Buttons

**Structure:** `<a class="btn">` (default) or `<a class="btn primary">`

| Class | Description |
|---|---|
| `.btn` | Ghost/bordered button: translucent white background, `--line` border, `--text` colour |
| `.btn.primary` | Filled gradient button: `#6aa6ff` → `#7cf0d6`, dark text `#08101d`, no border |

Both are `<a>` elements styled as buttons. No `<button>` elements used in the codebase.

### Card

**Structure:** `<div class="card">`

| Class | Description |
|---|---|
| `.card` | Semi-transparent dark surface, `--radius` corners, `--shadow` drop shadow, `18px` padding |
| `.tag` | Pill badge inside card header (e.g. "Live", "Coming soon", "Decision assurance") |
| `h3` inside `.card` | 18px, 8px bottom margin |
| `p` inside `.card` | Muted colour, no margin |
| `.ctas` inside `.card` | Button group with 12px top margin |

### Grid Layout

| Class | Description |
|---|---|
| `.grid` | CSS Grid container, 14px gap |
| `.grid.cols-3` | Three equal columns on desktop; single column on mobile (<980px) |

### Section Separator and Title

| Class | Element | Description |
|---|---|---|
| `hr.sep` | `<hr>` | Full-width hairline separator (`--line` colour), `22px` vertical margin |
| `.section-title` | `<h2>` | 18px section heading, `0 0 10px` margin |

### Stack Layout

| Class | Description |
|---|---|
| `.stack` | Grid container, `14px` gap — vertical card stacks |
| `.stack--lg` | Same but `22px` gap |

### Embed Container

| Class | Description |
|---|---|
| `.embed` | Rounded container with border and subtle background for iframes |
| `.embed iframe` | 100% width, `760px` height desktop / `900px` height mobile |

Used on `/legal/` and `/accountancy/` for Microsoft Forms embeds.

### Footer

**Structure:** `<footer class="site-footer">` → `.footer-grid` (3 columns) + `.footer-bottom`

| Class | Description |
|---|---|
| `.site-footer` | Top border, muted text, 13px font |
| `.footer-grid` | 1-column mobile / 3-column desktop grid (`1.2fr 1fr 0.8fr`) |
| `.footer-brand` | Flex row: logo image + company name + tagline |
| `.footer-logo` | 34px tall footer logo |
| `.footer-title` | Bold 13px column heading |
| `.footer-links` | Grid of footer links/text, 6px gap |
| `.footer-bottom` | Flex row: copyright left / legal links right; top border |
| `.footer-legal` | Flex row of Privacy + Terms links with `|` separator |
| `.smallprint` | 12px `rgba(184,198,230,.95)` text |

### Utility / Other

| Class | Description |
|---|---|
| `.container` | Max-width `1120px` centred wrapper with `24px` padding |
| `.clean` | Styled `<ul>` with left-padding `18px`, muted colour, `6px` item spacing |
| `.home-layout` | Defined in CSS but **not used** in any current HTML |
| `.home-sidebar` | Defined in CSS but **not used** in any current HTML |

---

## 6. Brand Assets

### Logo Files

| File | Path | Size | Usage |
|---|---|---|---|
| EIS Consulting logo (2×) | `src/assets/eis-consulting-logo-transx2.png` | 9.5 KB | Nav and footer on every page |
| EIS icon (standalone) | `src/assets/eis-icon-transparent.png` | 60 KB | **Not referenced in any HTML** — unused |

The `transx2` suffix suggests this is a 2× (Retina/HiDPI) resolution version. No `srcset` or `<picture>` element is used — the high-resolution image is served to all screen densities.

### Favicon / App Icon Set

| File | Path | Size | Usage |
|---|---|---|---|
| Favicon (root) | `src/favicon.png` | — | `<link rel="icon">` + `<link rel="shortcut icon">` on home page only |
| Favicon 16px | `src/assets/favicon-16.png` | 589 B | All pages |
| Favicon 32px | `src/assets/favicon-32.png` | 1.1 KB | All pages |
| Apple Touch Icon | `src/assets/apple-touch-icon.png` | 4.9 KB | All pages (180×180) |
| 48px icon | `src/assets/48 px.png` | 1.6 KB | Not referenced in any HTML |
| 192px icon | `src/assets/192 px.png` | 5.3 KB | Not referenced in any HTML |
| 180px icon | `src/assets/180 px.png` | 4.9 KB | Not referenced in any HTML |
| 512px icon | `src/assets/512 px.png` | 15 KB | Not referenced in any HTML |

The 48/192/180/512px icons are likely intended for a Web App Manifest or PWA configuration, but **no `manifest.json` and no `<link rel="manifest">` exist**. The filenames also contain a space character (`180 px.png`) which is non-standard and could cause URL encoding issues.

### OG / Social Preview Image

| File | Path | Size | Notes |
|---|---|---|---|
| OG image (assets) | `src/assets/og.png` | 98 KB | Referenced by OpenGraph meta tags using hardcoded Azure URL |
| OG image (root) | `src/og.png` | — | Present at root; likely a legacy copy — not referenced in any current HTML meta tag |

The OG `og:image` meta tags on the home page (`src/index.html:41–42`) point to an absolute Azure Static Apps URL:
```
https://witty-cliff-0ea22e003.6.azurestaticapps.net/og.png?v=10
```
This references `og.png` at the **site root** (not `/assets/og.png`), which matches `src/og.png`. On other pages, no OG tags are present at all.

### Icon Set

**None.** No icon library (Font Awesome, Heroicons, Phosphor, etc.) is loaded. No SVG icons are used anywhere.

### Fonts

**System font stack only.** No web fonts are loaded. No `@font-face` declarations. No external font service (Google Fonts, Adobe Fonts). No self-hosted `.woff` / `.woff2` files in the repository.

### Image Conventions

- All images are PNG format.
- No SVG, WebP, AVIF, or JPEG assets.
- No lazy loading (`loading="lazy"`) applied to any images.
- No `width`/`height` attributes on `<img>` elements (risks layout shift / CLS).

---

## 7. JavaScript

**No JavaScript is present anywhere in the repository.**

- No `.js` or `.ts` files found.
- No `<script>` tags in any HTML page.
- No framework (React, Vue, Angular, Astro, etc.).
- No analytics script (Google Analytics, Plausible, etc.).
- No cookie consent script.

Interactive elements on the site:
- Navigation uses CSS-only active state (class + `aria-current` set in HTML at build time).
- Waitlist forms (Legal, Accountancy) are Microsoft Forms embedded via `<iframe>` — all interactivity is handled by Microsoft's servers.

---

## 8. Accessibility Baseline

This is a posture check, not a WCAG audit.

### Positive signals

| Item | Finding |
|---|---|
| Language attribute | `lang="en-GB"` on all `<html>` elements ✓ |
| Nav landmark | `<nav aria-label="Primary navigation">` on every page ✓ |
| Logo link label | `<a aria-label="EIS Consulting home">` on every page ✓ |
| Logo alt text | `alt="EIS Consulting logo"` on all logo `<img>` elements ✓ |
| Active nav state | Both `class="active"` and `aria-current="page"` used — redundant but correct ✓ |
| Iframe titles | Both embedded forms have `title` attributes (`"AI in Legal Services waitlist form"`, `"AI in Accountancy waitlist form"`) ✓ |
| Focus visible | CSS `:focus-visible` provides visible 2px accent-coloured outline (`styles.css:29–33`) ✓ |
| Interactive elements | All CTAs are `<a>` elements with `href` — no `div` or `span` used as buttons ✓ |
| Semantic structure | Correct use of `<header>`, `<main>`, `<footer>`, `<nav>`, `<section>` landmarks ✓ |

### Issues and concerns

| Issue | Severity | Detail |
|---|---|---|
| No skip navigation link | Medium | No `<a href="#main-content">Skip to main content</a>` at page top — keyboard-only users must tab through the 5-item nav on every page load |
| Draft copy visible to users | High (content) | `src/contact/index.html:39`: `"For now, use email booking. We can add a scheduler later (Microsoft Bookings or similar)."` is rendered as live body copy, not a comment |
| Heading hierarchy gap | Low | `src/general-practice/index.html:53`: card uses `<h3>What's on this page</h3>` without a preceding `<h2>` in the main content, creating a jump from `<h1>` to `<h3>` |
| No `width`/`height` on images | Low | All `<img>` elements lack explicit `width` and `height` attributes; may cause Cumulative Layout Shift (CLS) |
| No lazy loading on images | Low | Logo images rendered in footer on every page with no `loading="lazy"` |
| Colour contrast (untested) | Medium | `.small` / `.muted` text (`#b8c6e6`) on `#0b1220` background needs verification; primary button text (`#08101d`) on gradient endpoint `#7cf0d6` may be borderline at WCAG AA |
| No `<meta name="robots">` | Info | No explicit robots directives; Azure Static Web Apps default behaviour applies |
| Missing `<main id>` | Low | No `id` on `<main>` elements — skip link target cannot be added without HTML edit |

---

## 9. Archive Recommendation

### Recommended approach: Git tag on `main` HEAD

**Action:** Before any rebuild work begins on `main`, create an annotated tag:

```bash
git tag -a v0-pre-rebuild -m "Pre-rebuild snapshot: existing 7-page static site, Jan 2026"
git push origin v0-pre-rebuild
```

**Why this is the right call:**

- A git tag is **immutable** — it permanently marks a specific commit and cannot be accidentally moved or overwritten.
- **Zero working-directory clutter** — the rebuild can proceed directly in `main` without legacy files competing for attention in the file tree.
- Tags are listed in GitHub releases/tags UI, making the snapshot easy to find and share.
- The existing `audit/site-inventory` branch (containing this document) provides additional reference context and should be retained until the rebuild is complete.

### Trade-offs of alternatives

| Approach | Pro | Con |
|---|---|---|
| **Git tag (recommended)** | Permanent, zero clutter, recoverable at any time | Files not browsable in GitHub file tree without checkout |
| **`/archive/v0/` directory in `main`** | Files directly visible in GitHub UI | Pollutes working tree; build config (`app_location: ./src`) requires updating; adds permanence where none is needed |
| **Long-lived `archive/v0` branch** | Files browsable on GitHub without checkout | Another branch to manage; may create confusion about what is "current"; does not add over the tag approach |
| **Combination: tag + archive branch** | Maximum redundancy | Overkill for a 7-page static site; maintenance overhead |

### Naming convention

- Tag: `v0-pre-rebuild` (or `v0.1.0` if you adopt semantic versioning for site releases)
- Existing audit branch: keep as `audit/site-inventory` until rebuild is merged

---

## A. Acronym Definition Table

| Acronym | Definition |
|---|---|
| AI | Artificial Intelligence |
| API | Application Programming Interface |
| ARIA | Accessible Rich Internet Applications (W3C specification for accessibility attributes) |
| AVIF | AV1 Image File Format (next-generation image format) |
| BEM | Block Element Modifier (CSS naming methodology) |
| CDN | Content Delivery Network |
| CI/CD | Continuous Integration / Continuous Deployment |
| CLS | Cumulative Layout Shift (Core Web Vitals metric) |
| CQC | Care Quality Commission (UK healthcare regulator) |
| CSS | Cascading Style Sheets |
| CTA | Call to Action |
| DPIA | Data Protection Impact Assessment |
| EIS | EIS Consulting Ltd (Employer and Information Services — assumed; company name; exact long-form not confirmed in source) |
| GDPR | General Data Protection Regulation |
| GP | General Practice (NHS primary care) |
| HiDPI | High Dots Per Inch (high-resolution display) |
| HTML | HyperText Markup Language |
| HTTP | HyperText Transfer Protocol |
| ICP | Ideal Customer Profile |
| ICO | Information Commissioner's Office (UK data protection regulator) |
| JS | JavaScript |
| NHS | National Health Service |
| OG | Open Graph (social media preview metadata protocol) |
| PNG | Portable Network Graphics |
| PR | Pull Request |
| PWA | Progressive Web App |
| SME | Small and Medium-sized Enterprise |
| SVG | Scalable Vector Graphics |
| UK | United Kingdom |
| URL | Uniform Resource Locator |
| WCAG | Web Content Accessibility Guidelines |
| WebP | Web Picture format (Google-developed image format) |

---

## B. Review Guide

### Confidence Map by Section

| Section | Confidence | Rationale |
|---|---|---|
| 1. Repo state | **High** | Full file tree, git log, and workflow YAML read directly — no inference required |
| 2. Pages | **High** | All 7 HTML files read in full; purpose and status derived from visible content |
| 3. CSS architecture | **High** | Single CSS file read in full; methodology assessment is interpretive but grounded in the file |
| 4. Design tokens | **High** | All values quoted verbatim from `styles.css:root` and inline declarations |
| 5. Components | **High** | All classes derived from reading the full CSS file and cross-referencing HTML usage |
| 6. Brand assets | **Medium** | File presence confirmed; file contents (actual logo appearance, OG image content) not visually inspectable by this tool — descriptions inferred from filenames and context |
| 7. JavaScript | **High** | Absence confirmed via glob search of all `.js`/`.ts` files and inspection of all HTML `<head>` and `<body>` elements |
| 8. Accessibility | **Medium** | Structural patterns confirmed by reading HTML; colour contrast ratios not numerically calculated — flagged as requiring tool-based verification |
| 9. Archive recommendation | **High** | Based on complete understanding of repo structure; recommendation is standard practice |

### Declared Assumptions

1. **"EIS" long-form:** The full meaning of the "EIS" initialism in "EIS Consulting Ltd" is not stated anywhere in the source files. The acronym table entry is marked as assumed pending confirmation.
2. **Deployment domain:** The production domain (`eisconsulting.co.uk`) is referenced in footer contact details and email addresses, but the OG meta tags still point to the Azure Static Apps preview URL (`witty-cliff-0ea22e003.6.azurestaticapps.net`). Assumed DNS has not been pointed to the custom domain as of the last commit (2026-01-29).
3. **`src/og.png` vs `src/assets/og.png`:** The root-level `src/og.png` is assumed to be a legacy copy from before the asset was moved to `src/assets/og.png`. OG meta tags reference the root path via the Azure URL. Both files likely contain the same image.
4. **Icon asset intent:** The 48/192/180/512px PNG files in `src/assets/` are assumed to be intended for a future PWA manifest, since no manifest file currently exists.
5. **`transx2` logo:** Assumed to mean 2× pixel-density version based on common naming conventions. The audit cannot confirm pixel dimensions without an image inspection tool.
6. **Google commit author:** All 150 commits are attributed to "daneilso" — assumed to be a single developer (Damo) working directly in the GitHub web editor (all commit messages are "Update index.html" which is the default GitHub web UI commit message).

### Three Priority Review Items

1. **Draft copy visible to all visitors** — `src/contact/index.html:39` contains `"For now, use email booking. We can add a scheduler later (Microsoft Bookings or similar)."` This is live, public-facing body text that reads as an internal note. It should be replaced with a visitor-facing description before the current site is used in any marketing activity — regardless of the rebuild timeline.

2. **OG meta tags point to Azure preview URL, not production domain** — All social preview images and URLs in `src/index.html:39–54` reference `witty-cliff-0ea22e003.6.azurestaticapps.net`. When the rebuild goes live on `eisconsulting.co.uk`, sharing the home page on LinkedIn, Twitter/X, or in email will generate a preview card with the Azure URL visible in the metadata. Update these to the production domain before any marketing launch.

3. **No analytics, no consent mechanism, no cookie notice** — The site has zero analytics. Before a rebuild goes live with any marketing spend behind it, a decision on analytics tooling (e.g. privacy-friendly options like Plausible or Fathom that require no consent banner under UK ICO guidance) will affect both the rebuild architecture and the Privacy Policy, which currently states "We do not currently use advertising cookies. If we add analytics or marketing tools in future, we will update this policy." This is the right time to decide.

### Estimated Review Time

**15–20 minutes** to read through this document in full.  
**Additional 10 minutes** if you wish to visually cross-check the CSS token table against the live site in a browser.  
**Additional 5 minutes** to verify the contact page draft text issue and OG URL issue live in the browser.

Total: ~30 minutes for a thorough review pass.
