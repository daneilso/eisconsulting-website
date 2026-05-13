# 2026-05-13 - Closeout - EIS Website Rebuild Stage 3 v1.0

**Date:** 2026-05-13
**Branch:** `rebuild/v1`
**Executed by:** Claude Code (claude-sonnet-4-6) on behalf of AI CustomWorks Ltd
**For:** EIS Consulting Ltd (Damo, Founder)
**Brief:** 2026-05-13 - Brief - EIS Website Rebuild v1.2

---

## 1. Scope Delivered

Seven pages rebuilt, updated, or instrumented per brief v1.2:

| Page | File | Treatment | Status |
|---|---|---|---|
| Home | `src/index.html` | Full rebuild — Master Value Canvas v0.10 | Complete |
| Legal | `src/legal/index.html` | Full rebuild — DRB v1.0 proposition | Complete |
| Healthcare | `src/healthcare/index.html` | New stub with waitlist (renamed from `general-practice`) | Complete |
| Accountancy | `src/accountancy/index.html` | Stub update with waitlist | Complete |
| Contact | `src/contact/index.html` | Hot-fix — draft copy removed | Complete |
| Privacy Policy | `src/privacy-policy/index.html` | Clarity disclosure and company identifiers added | Complete |
| Terms of Use | `src/terms-of-use/index.html` | Clarity script injection and cross-cutting fixes only | Complete |

Cross-cutting work completed in-page during Step 4 (not as a separate pass):

- Microsoft Clarity (`wqha1gwbg3`) injected on all 7 pages
- OG meta tags updated to `eisconsulting.co.uk` on all 7 pages (Azure preview URL removed); OG tags added to pages that previously had none (legal, healthcare, accountancy, contact, privacy-policy, terms-of-use)
- Skip-to-content link added to all 7 pages
- `id="main-content"` added to `<main>` on all 7 pages
- Nav badge (`.badge` element) removed from all 7 pages (see Refinement 1 below)
- Nav updated to Healthcare on all 7 pages (replacing General Practice)
- Image dimensions (`width`/`height`) added to all logo `<img>` elements
- `loading="lazy"` added to footer logo on all 7 pages
- Footer tagline updated on all 7 pages (see Refinement 5 below)
- `src/staticwebapp.config.json` created with 301 redirects from `/general-practice/` and `/general-practice` to `/healthcare/`
- `.grid.cols-4` and `.skip-link` added to `src/assets/styles.css`
- `v0-pre-rebuild` annotated git tag created against `main` HEAD (`118a090`) and pushed to origin

---

## 2. Implementation Refinements Beyond the Brief

Five changes were made during Stage 3 that go beyond the explicit brief specification. All were approved by Damo in-session. Brief v1.3 will incorporate them retrospectively if Damo decides to formalise.

**Refinement 1 — Nav badge removed**
The `.badge` element ("Adopt AI safely, with evidence." and variants) was removed from the `<header>` nav on all 7 pages. The brief did not specify removing it. Decision: the badge text, carrying the old AI-compliance positioning, actively undermines the authority the new proposition pages establish. Approved by Damo before home page was written. Applied globally.

**Refinement 2 — ScoreApp CTA opens in new tab**
Both ScoreApp links — the home page hero primary button and the legal page Prize CTA — received `target="_blank" rel="noopener noreferrer"`. The brief specified neither attribute. Decision: ScoreApp operates on a different domain; opening in a new tab preserves the visitor's EIS context. The `rel="noopener noreferrer"` prevents the opened tab acquiring a reference to the EIS page (security best practice). Healthcare and accountancy waitlist links were left same-tab as they navigate to internal `#waitlist` anchors. Approved by Damo before home page was written.

**Refinement 3 — Prize section uses `<h2>` not `<h1>` for `.h1--sm` heading**
The brief specifies "use `.h1--sm`" for the Prize section heading on the home page ("Growth your firm sustains.") and the legal page Prize heading ("2% AR rate floor."). The brief does not specify the HTML element. The `.h1--sm` class was applied to `<h2>` rather than a second `<h1>` on each page, preserving a single `<h1>` per page and maintaining correct heading hierarchy. This is standard HTML5 accessibility practice. Visual output is unchanged — `.h1--sm` controls only font size.

**Refinement 4 — Privacy Policy "Last updated" date advanced**
The "Last updated" date was advanced from "27 January 2026" to "13 May 2026". The brief did not specify updating this date. Decision: the policy content was materially changed (Clarity disclosure added, company and VAT numbers inserted). A policy whose content changes should reflect the change date. Applied to `src/privacy-policy/index.html` only. The Terms of Use "Last updated" date was left at "27 January 2026" because its content was not changed.

**Refinement 5 — Footer tagline updated across all pages**
The footer brand tagline was updated from "Adopt AI safely, with evidence." (old positioning) to "Senior technology capability, fractionally committed." (new positioning, condensed from Method Principle 1 of the EIS Augmentation Method). The brief specifies "Footer (existing)" which was interpreted as structural inheritance, not a directive to retain copy from the old positioning. An intermediate version ("Growth your firm sustains.") was raised during implementation but rejected by Damo as diluting the Prize, which already appears as the home page H1 and the Section 6 heading. "Senior technology capability, fractionally committed." does positioning work in the footer without repeating the Prize copy. Applied globally across all 7 pages.

---

## 3. Colour Contrast Verification (§9.3)

The brief requires contrast verification and documentation in this closeout note for two values:

**`.muted` text (`#b8c6e6`) on page background (`#0b1220`):**
Estimated relative luminance: foreground ≈ 0.56, background ≈ 0.004. Estimated contrast ratio: approximately 11:1. This exceeds WCAG AA (4.5:1 for normal text, 3:1 for large text) comfortably.

**Primary button text (`#08101d`) on gradient endpoint (`#7cf0d6`):**
Estimated relative luminance: foreground ≈ 0.003, background ≈ 0.72. Estimated contrast ratio: approximately 14:1. This exceeds WCAG AA comfortably.

**Caveat:** These are manually estimated ratios using a simplified luminance formula. A tool-based verification (e.g. WebAIM Contrast Checker) is recommended before final DNS cutover sign-off. No values were changed because neither estimate falls close to the WCAG AA threshold.

---

## 4. Acceptance Criteria Tick-List (Step 6)

Self-check performed by Claude Code against the 18 criteria in brief §11. Acceptance is Damo's to give (criterion 18).

| # | Criterion | Result | Method |
|---|---|---|---|
| 1 | `v0-pre-rebuild` tag created and pushed to origin | VERIFIED | `git tag -v` and push output confirmed |
| 2 | `general-practice` renamed to `healthcare`; 301 redirect operational | VERIFIED | `git mv` tracked; `staticwebapp.config.json` covers both URL forms |
| 3 | All 7 pages render on Azure preview URL with no console errors | PENDING | Requires live PR preview |
| 4 | All 7 pages pass screen-reader navigation via skip link | PENDING | Skip link present on all 7 pages (grep verified); functional test requires browser |
| 5 | Clarity recording on all 7 pages visible in dashboard within 24hrs | PENDING | Snippet confirmed on all 7 pages (grep verified); live verification requires deployment |
| 6 | Home hero: 3 CTAs, correct order, correct classes | VERIFIED | `src/index.html:85–96` — law `.btn.primary`, healthcare/accountancy `.btn` |
| 7 | Hero CTAs fire distinct Clarity events on click | VERIFIED | `onclick` handlers confirmed: `hero_cta_law_scorecard`, `hero_cta_healthcare_waitlist`, `hero_cta_accountancy_waitlist` |
| 8 | Healthcare and accountancy hero links deep-link to `#waitlist` | VERIFIED | hrefs `/healthcare/#waitlist` and `/accountancy/#waitlist` confirmed; `<section id="waitlist">` confirmed on both stub pages |
| 9 | Legal Prize CTA navigates to ScoreApp URL and fires `scorecard_cta_click_drb` | VERIFIED | `src/legal/index.html:205–208` confirmed |
| 10 | OG metadata references `eisconsulting.co.uk` on all 7 pages | VERIFIED | Grep for `azurestaticapps` returns clean across all of `src/` |
| 11 | No draft, placeholder, or comment text in any page source | VERIFIED | Grep for `OPTIONAL`, `for now, use`, `scheduler later`, HTML comments — all clean |
| 12 | No em-dashes (U+2014) in any visible page copy | VERIFIED | UTF-8 byte sequence search returns clean across all HTML files |
| 13 | Home page Pains grid: 3 columns above 980px, 1 column below | VERIFIED | `styles.css:257–261` |
| 14 | Home page Method grid: 4 columns above 980px, 1 column below | VERIFIED | `styles.css:258–262` |
| 15 | Legal Mistakes and Blueprint: paired vertical stacks, visually balanced | PENDING | Both use `class="stack stack--lg"` (source verified); visual balance requires browser at width |
| 16 | Both stub pages embed Microsoft Forms iframes with sector-appropriate fields | VERIFIED | Correct distinct `forms.cloud.microsoft` URLs on healthcare and accountancy; `<section id="waitlist">` on both |
| 17 | Privacy Policy contains Clarity disclosure, Company No `08695848`, VAT No `GB 173 8471 82` | VERIFIED | `src/privacy-policy/index.html:83`, `:191`, `:193` |
| 18 | Damo signs off preview URL before DNS cutover | NOT MINE TO GIVE | Damo's acceptance after reviewing the Azure PR preview |

---

## 5. Files Changed

```
M  src/assets/styles.css          Added .skip-link and .grid.cols-4
RM src/general-practice/index.html -> src/healthcare/index.html
M  src/index.html                 Full rebuild
M  src/legal/index.html           Full rebuild
M  src/accountancy/index.html     Stub update
M  src/contact/index.html         Hot-fix + cross-cutting
M  src/privacy-policy/index.html  §8 changes + cross-cutting
M  src/terms-of-use/index.html    Clarity + cross-cutting
A  src/staticwebapp.config.json   301 redirects (new file)
```

Tag pushed to origin: `v0-pre-rebuild` → `118a090`

---

## 6. Remaining Actions (Damo)

1. **Review the Azure PR preview URL** — generated automatically when the PR is opened. Check all 7 pages visually, including mobile widths.
2. **Verify Clarity is recording** — within 24 hours of PR preview deployment, check project `wqha1gwbg3` in the Clarity dashboard for session activity.
3. **Test the three hero CTAs** — confirm ScoreApp opens in a new tab and the two waitlist deep-links scroll to the `#waitlist` section on their respective pages.
4. **Test the legal Prize CTA** — confirm ScoreApp opens in a new tab.
5. **Verify the 301 redirect** — request `/general-practice/` on the Azure preview URL and confirm it redirects to `/healthcare/`.
6. **Verify colour contrast** — use the WebAIM Contrast Checker or equivalent to confirm both values documented in §3 above.
7. **ScoreApp URL confirmation** — confirm `https://damian-gbwjygw9.scoreapp.com` is the production URL (typo `ttps://` noted during handoff, corrected to `https://` for implementation).
8. **DNS cutover** — once you have signed off the preview URL, issue the DNS change at One.com to point `eisconsulting.co.uk` to the Azure Static Web Apps deployment. LinkedIn Post Inspector and X Card Validator should be used to force OG cache refresh after DNS propagation.

---

*Document produced under PRISM Project Instructions v1.4. Stage 3 delivery by AI CustomWorks Ltd for EIS Consulting Ltd.*
