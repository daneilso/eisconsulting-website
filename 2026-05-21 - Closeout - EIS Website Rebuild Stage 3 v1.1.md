# 2026-05-21 - Closeout - EIS Website Rebuild Stage 3 v1.1

**Date:** 2026-05-21
**Version:** v1.1
**Supersedes:** v1.0 (2026-05-13)
**Branch at engagement close:** `rebuild/v1` (merged to `main` on 2026-05-21 as PR #1)
**Stage 3 build executed by:** Claude Code (claude-sonnet-4-6) on behalf of AI CustomWorks Ltd
**Production cutover executed by:** Damo, assisted by Claude (claude.ai), Customer-side work per SoW §3.2 and §4
**For:** EIS Consulting Ltd (Damo, Founder)
**Brief:** 2026-05-13 - Brief - EIS Website Rebuild v1.2
**Change in v1.1:** Documents the production cutover, Azure DNS migration (unplanned scope), three hot-fix commits made during acceptance walkthrough, ScoreApp branded URL configuration, and backlog items surfaced. Adds PRISM-compliant Acronym Definition Table and Review Guide.

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

## 7. Post-PR Fix — Azure Deployment Validation Failure

**Date:** 2026-05-14
**Commit:** see `fix(routing)` commit on `rebuild/v1`

Initial Azure deployment failed validation because `staticwebapp.config.json` defined two redirect rules for `/general-practice/` and `/general-practice`. Azure Static Web Apps normalises these to the same internal route and treats them as a duplicate-rule error. Failure was caught at PR #1 deployment log line 40 before any live traffic was affected.

**Fix:** Consolidated both rules to a single wildcard rule:

```json
{
  "routes": [
    {
      "route": "/general-practice*",
      "redirect": "/healthcare/",
      "statusCode": 301
    }
  ]
}
```

The wildcard `*` covers both `/general-practice` and `/general-practice/` in one rule per Azure Static Web Apps documented redirect syntax.

**Brief note:** Brief §9.5 specified two separate rules (with and without trailing slash) as the example pattern. The working pattern for Azure is one wildcard rule. Brief v1.3 should update §9.5 to reflect the wildcard pattern for future engagements.

---

## 8. Stage 3 acceptance refinements

**Date:** 2026-05-14
**Commits:** `chore(nav):`, `feat(home):`, `feat(privacy):`, `docs:`
**Triggered by:** Damo's acceptance review of the Azure PR preview.

Four changes were made after PR open and initial Azure deployment, based on Damo's review of the deployed preview.

**Refinement A — Nav order corrected (all 7 pages)**
Navigation order changed from `Home | Healthcare | Legal | Accountancy | Contact` to `Home | Legal | Healthcare | Accountancy | Contact` on both the header nav and footer nav across all 7 pages. Legal and Healthcare positions were transposed. Rationale: Law is the live proposition; Healthcare and Accountancy are stubs in development. Priority order reflects the current state of delivery.

**Refinement B — Home page hero restructured to sector columns**
The single `.ctas` row of three buttons was replaced with a `.hero-sectors` grid of three labelled sector columns. Each column carries a `.kicker` sector label and stacked `.btn` elements. The LAW column has two buttons: (1) "Read the proposition first →" (`.btn`, href `/legal/`, event `hero_cta_law_proposition`) and (2) "Take the Avoidable Requisition Diagnostic →" (`.btn.primary`, ScoreApp URL, `target="_blank"`, event `hero_cta_law_diagnostic`). The HEALTHCARE and ACCOUNTANCY columns retain their single waitlist CTAs with unchanged event names. The `hero_cta_law_scorecard` event name was retired; replaced by `hero_cta_law_proposition` and `hero_cta_law_diagnostic`. New CSS utility class `.hero-sectors` added to `src/assets/styles.css`: 3-column grid on desktop (≥980px), single column on mobile (<980px), with `.hero-sectors .ctas{flex-direction:column;align-items:flex-start}` for vertical button stacking within each sector column.

**Refinement C — Privacy Policy: third-party destinations section added**
New §12 "Third-party destinations and form processing" inserted between the Clarity disclosure (§11) and "Changes to this policy" (renumbered §13). Discloses ScoreApp as an independent data controller for personal data submitted via the scorecard, and Microsoft Forms (Microsoft 365) as a data processor under the Microsoft Online Services Data Protection Addendum. "Last updated" date advanced from 13 May 2026 to 14 May 2026 (policy content materially changed).

**Refinement D — Closeout note appended (this section)**
This addendum records the four acceptance refinements in the project closeout document.

---

### Brief v1.3 candidate items

The following items are candidates for brief v1.3 or a subsequent engagement template:

1. **Nav order convention**: Legal before Healthcare (live proposition before development stubs) should be the default nav order pattern for multi-sector sites where sectors are at different stages of delivery.
2. **Hero sector-grouping pattern**: Three labelled sector columns with stacked CTAs per sector (the `.hero-sectors` pattern) is the preferred layout for multi-sector landing pages over a flat CTA row.
3. **Privacy policy template**: Template should include a "Third-party destinations and form processing" section as standard when ScoreApp and/or Microsoft Forms are in use.
4. **Clarity event naming convention**: Retire `_scorecard` suffix for ScoreApp CTAs; use `_proposition` (internal proposition page link) and `_diagnostic` (ScoreApp link) as the standard split for sector hero CTAs with two law-sector actions.

---

### Post-refinement changes (2026-05-14)

Three further changes applied in a single commit (`refine(home):`) after the four-commit acceptance batch above.

**Change 1 — Hero CTA hrefs: `#waitlist` fragments removed**
`/healthcare/#waitlist` → `/healthcare/` and `/accountancy/#waitlist` → `/accountancy/` in `src/index.html`. Rationale: auto-scrolling to the form bypassed sector positioning content the visitor needed to read first. The `id="waitlist"` anchors on both stub pages are retained for direct-link use from email, social, or future scorecard outcome pages.

**Change 2 — Law proposition button label updated**
"Read the proposition first →" → "How we help law firms grow →". Clarity event name `hero_cta_law_proposition` unchanged (internal; semantically correct).

**Change 3 — Hero sector buttons full-width**
New scoped CSS rule added to `src/assets/styles.css`: `.hero-sectors .btn{width:100%;box-sizing:border-box}`. Buttons within each sector column stretch to fill the column width; the longer label sets the column width and the shorter button matches. Global `.btn` class unchanged. Responsive: on mobile single-column layout, buttons fill available width naturally.

---
---

## 9. Production Cutover and Azure DNS Migration (2026-05-21)

This section documents work performed on 2026-05-21, after §11.18 sign-off. Per SoW §3.2 and §4, custom domain DNS work is Customer-side. Recorded here to keep the engagement record complete.

### 9.1 Acceptance walkthrough hot-fixes

Three commits made during the §11 walkthrough against the Azure preview URL, before merging PR #1 to `main`:

- `2c26e41` fix(home): correct H1 copy and reorder meta titles. H1 read "Growth your firm sustains" (grammatically incomplete). Corrected to "Growth your firm can sustain." in both H1 and section H2. Page `<title>`, `og:title`, `og:image:alt`, and `twitter:title` reordered to subject-first per Brief §3 house style, separator normalised to pipe.
- `ccca659` fix(legal): remove template-instruction placeholder text. Privacy Policy and Terms of Use each contained a sentence directing the site owner to review the template, visible to end users. Both contained em-dashes, violating house style. Both sentences deleted. Global pattern check confirmed no further placeholder or em-dash residue in `src/`.
- `7234c53` feat(scorecard): point CTAs to branded diagnostic subdomain. Home page hero and Legal page Prize CTAs updated from `damian-gbwjygw9.scoreapp.com` to `diagnostic.eisconsulting.co.uk`. Closes Handover item 6.

### 9.2 DNS infrastructure migration: Stackdns to Azure DNS

**Trigger:** During Phase 1 of the cutover (ScoreApp custom domain setup), CNAME records added through One.com's Personal DNS panel appeared in the panel UI but did not publish to the Stackdns authoritative nameservers (`ns1-4.stackdns.com`). The `diagnostic` CNAME and a test CNAME (`cnametest`) both failed to propagate. All four authoritative nameservers confirmed no record present, despite the panel showing them. Issue isolated to a One.com to Stackdns sync failure, not a Claude or user error.

**Decision:** Migrate DNS hosting from Stackdns to Azure DNS, keeping domain registration at One.com. Chosen over alternatives (waiting for One.com support to fix sync; reverting to One.com default nameservers, which risked breaking M365 records configured at Stackdns).

**Actions executed (EIS Azure tenant):**
- Created resource group `eis-dns` in `EIS Consulting Ltd - Pay As You Go` subscription, UK South region.
- Created Azure DNS zone `eisconsulting.co.uk`.
- Populated zone with records sourced from One.com Personal DNS panel (authoritative source of intent) rather than from Stackdns (which silently dropped some records, see §10).
- Records migrated as-is: apex A, AAAA, www A, AAAA, MX (Outlook), SPF TXT, autodiscover CNAME, sip CNAME, both Lync/Teams SRV records.
- Records deliberately not migrated: IPv6 wildcard AAAA (no longer applicable post-cutover).
- New record added: `diagnostic` CNAME → `dns.scoreapp.net`.
- Changed nameservers at One.com from `ns1-4.stackdns.com` to `ns1-07.azure-dns.com` / `ns2-07.azure-dns.net` / `ns3-07.azure-dns.org` / `ns4-07.azure-dns.info`.

**Propagation:** Nominet published the delegation change within ~30 minutes of save at One.com. All public resolvers visible to verification queries (Cloudflare, Google, Quad9) confirmed Azure DNS as authoritative before any cutover-affecting record changes were made.

### 9.3 Custom domain configuration in Azure SWA

**www subdomain:**
- CNAME validation chosen (Azure UI offered CNAME or TXT; CNAME does double duty as validation and production record).
- Azure DNS: `A` and `AAAA` placeholder records for `www` deleted; replaced with `CNAME www → witty-cliff-0ea22e003.6.azurestaticapps.net`.
- Validation completed within seconds. SSL certificate auto-provisioned by Azure.

**Apex (`eisconsulting.co.uk`):**
- DNS standards forbid a CNAME at zone apex. Azure DNS supports apex aliasing via an alias record set targeting the SWA resource directly (not a literal CNAME).
- TXT validation chosen for ownership verification (Azure-generated token added as a second TXT alongside the existing SPF, since multiple TXT records can co-exist at apex).
- After validation, the apex A and AAAA placeholder records were deleted; replaced with an Azure DNS alias A record targeting `/subscriptions/{aicw}/resourceGroups/rg-eis-websit/providers/Microsoft.Web/staticSites/EISConsultingWebsite`.
- Validation completed; SSL auto-provisioned; apex live with HTTPS.

### 9.4 Cross-tenant access setup

The EIS DNS zone lives in the EIS Azure tenant. The Static Web App lives in the AICW Azure tenant (subscription "AI CustomWorks Sandpit"). Azure DNS alias creation requires the CLI session to have read access to the target resource (the SWA in AICW), which the EIS account did not have by default.

**Resolution:**
- New EIS-domain account `Damian.Neilson@eisconsulting.co.uk` was invited as a Guest user in the AICW tenant.
- Granted **Reader** role on the EIS Static Web App resource only (least privilege).
- Granted **DNS Zone Contributor** role on the `eis-dns` resource group in the EIS tenant.
- This single account now performs cross-tenant operations cleanly.

### 9.5 ScoreApp branded URL live

After the Azure DNS migration completed, the `diagnostic` CNAME began publishing correctly (previously stuck in One.com / Stackdns sync failure). ScoreApp's custom domain validation, which had been "Pending DNS" since the previous day, completed. SSL provisioned by ScoreApp's Cloudflare layer. After enabling the custom domain toggle on the DRB scorecard within ScoreApp, `https://diagnostic.eisconsulting.co.uk` began serving the scorecard.

The two CTAs (home hero, legal Prize section) now point at the branded URL per commit `7234c53`.

---

### 9.6 Post-launch accessibility defect resolved

Microsoft Clarity's automated insight panel flagged "Dead clicks on skip links" during the post-launch session audit. The §11.4 acceptance check (skip-link keyboard navigation) had passed because it only tested Tab + Enter activation; it did not test that focus actually moved to the main content after activation.

Diagnosis: the `<main id="main-content">` element on all seven pages lacked `tabindex="-1"`. Without it, the browser cannot move keyboard focus to a non-interactive element. The skip link changed the URL hash and scrolled the page, but focus stayed on the skip link itself. The next Tab press returned the user to the nav, defeating the skip link's purpose.

Fix: added `tabindex="-1"` to every `<main id="main-content">` element across the seven pages. Verified live: after activating the skip link, Tab advances focus into the main content rather than back to the nav. Commit `e09b89f`.

This is a WCAG 2.4.1 Bypass Blocks (Level A) compliance fix. The defect did not exist in the original v1.2 brief; the implementation was incomplete on this criterion. §11.4 should be retested in this form (keyboard activation AND focus verification) in future acceptance walkthroughs.

---

## 10. DKIM and Teams CNAME Recovery

During the DNS migration audit, three CNAME records visible in the One.com Personal DNS panel were found to be missing from the authoritative Stackdns zone:

- `lyncdiscover.eisconsulting.co.uk` → `webdir.online.lync.com` (Teams discovery)
- `selector1._domainkey.eisconsulting.co.uk` → `selector1-eisconsulting-co-uk._domainkey.eisconsultingcouk.onmicrosoft.com` (DKIM)
- `selector2._domainkey.eisconsulting.co.uk` → `selector2-eisconsulting-co-uk._domainkey.eisconsultingcouk.onmicrosoft.com` (DKIM)

The DKIM records being absent meant EIS outbound mail had been sent without valid DKIM signatures since at least the start of today's session, and probably for an unknown period before. Net effect: degraded deliverability for any cold or bulk outreach.

All three records were recreated in Azure DNS with the values shown in the One.com panel. Post-migration verification confirmed all three records resolve correctly via public DNS. DKIM signing on EIS outbound mail is now operating as intended.

This was a side-effect benefit of the migration. The records had been "configured" in the One.com panel for some time but silently failing to publish to Stackdns.

---

## 11. Backlog Items Surfaced

Items raised by today's session that fall outside the engagement scope. Captured here for handoff to future EIS / AICW work.

| # | Item | Origin | Priority |
|---|---|---|---|
| 11.1 | One elevated-access user warning in AICW Azure tenant IAM. Identity and scope not yet investigated. | AICW tenant IAM blade banner | Medium (security review) |
| 11.2 | No DMARC record published for `eisconsulting.co.uk`. SPF and DKIM are present (post-migration). Adding a DMARC policy completes the email authentication trio and enables enforcement reporting. | Migration audit | Low/Medium (deliverability) |
| 11.3 | One.com Stackdns sync issue. Now moot since EIS DNS has left the provider; the support ticket (if opened) can be closed. | Today's diagnosis | Low (informational) |
| 11.4 | Unused One.com hosting records still present in One.com's Standard DNS: FTP, SFTP, SSH, phpMyAdmin, CalDAV, two SSHFP. Implies a One.com hosting product subscription is still active and being paid for. Worth a cleanup review. | One.com Standard DNS audit | Low (cost reduction) |
| 11.5 | AICW production workloads (the EIS Static Web App) are hosted in a subscription named "AI CustomWorks Sandpit". Naming suggests non-production scope. Review whether a separate production subscription should exist. TMF Protection question. | AICW tenant subscription listing | Medium (governance) |
| 11.6 | §11.10 acceptance criterion (LinkedIn OG preview check) was deferred per the criterion text until after DNS cutover. Now possible. Use LinkedIn Post Inspector at the production URL to validate. | Brief §11.10 | Low (validation) |
| 11.7 | The "FOR OWNER-LED FIRMS IN REGULATED SECTORS" subject-line text on the home hero and the equivalent on healthcare and accountancy were not re-examined post-launch. Worth a final tone check now that the site is live. | Walkthrough observation | Low (copy) |

---

## 12. Final Acceptance Status

All 18 Brief §11 criteria signed off on 2026-05-21.

| § | Criterion (summary) | Status |
|---|---|---|
| 11.1 | `v0-pre-rebuild` git tag at pre-rebuild commit, pushed to origin | Pass |
| 11.2 | `/general-practice/` 301 redirect to `/healthcare/` | Pass (verified on production) |
| 11.3 | Pages render correctly, no console errors | Pass (with noted Microsoft Forms service-worker warning on healthcare and accountancy, third-party origin, no functional impact) |
| 11.4 | Skip-to-content keyboard navigation | Pass |
| 11.5 | Clarity recording across all seven pages | Pass |
| 11.6 | Hero CTA structure per Closeout Refinement 2 | Pass |
| 11.7 | Hero CTA Clarity events fire | Pass (events renamed per Closeout Refinement 2: `_scorecard` → `_diagnostic`) |
| 11.8 | Healthcare and accountancy hero links per Closeout Refinement 3 | Pass |
| 11.9 | Legal Prize CTA + `scorecard_cta_click_drb` event | Pass |
| 11.10 | OG metadata production-URL check | Deferred per criterion text until post-cutover. Now possible, see Backlog 11.6. |
| 11.11 | No draft, placeholder, or comment text | Pass (after fixes via commits `2c26e41` and `ccca659`) |
| 11.12 | No em-dashes in website-rendered copy | Pass (after fixes in same commits) |
| 11.13 | Pains grid responsive (3 cols above 980px, 1 col below) | Pass |
| 11.14 | Method grid responsive (4 cols above 980px, 1 col below) | Pass |
| 11.15 | Legal Mistakes and Method paired vertical stacks | Pass |
| 11.16 | Microsoft Forms waitlist iframes on healthcare and accountancy | Pass |
| 11.17 | Privacy Policy company identity (Clarity disclosure + Co `08695848` + VAT `GB 173 8471 82`) | Pass |
| 11.18 | Visual sign-off | **Signed 2026-05-21** by Damo. Engagement formally closed under SoW §9.1(a). |

---

## 13. Acronym Definition Table

| Acronym | Meaning | Notes in this document |
|---|---|---|
| AICW | AI CustomWorks Ltd | Provider on the engagement per SoW |
| ALIAS | A DNS record type that points an apex name at another hostname or resource | Used as the Azure DNS alias mechanism for `eisconsulting.co.uk` apex |
| API | Application Programming Interface | |
| ARPU | Average Revenue Per User | SaaS as a Science vocabulary, not used in this document but standard in PRISM context |
| CLI | Command Line Interface | Azure CLI used for DNS migration |
| CNAME | Canonical Name (DNS record) | |
| CTA | Call To Action | The hero buttons and legal Prize CTA |
| DKIM | DomainKeys Identified Mail | Email authentication via cryptographic signing |
| DMARC | Domain-based Message Authentication, Reporting and Conformance | Policy layer atop SPF and DKIM, absent on EIS as of 2026-05-21 |
| DNS | Domain Name System | |
| DRB | Defensible Requisition Blueprint | The EIS Consulting flagship proposition; the diagnostic scorecard sits on top of this method |
| EIS | EIS Consulting Ltd | Customer on the engagement per SoW |
| GDPR | General Data Protection Regulation | UK GDPR baseline applies |
| H1 | First-level heading element in HTML | |
| HTTPS | Hypertext Transfer Protocol Secure | |
| IAM | Identity and Access Management | Azure RBAC blade |
| ICO | Information Commissioner's Office | UK data protection regulator |
| IP | Internet Protocol address | |
| KPI | Key Person of Influence (Daniel Priestley) | PRISM framework, not used in this document but standard in project context |
| LF / CRLF | Line Feed / Carriage Return + Line Feed | Windows vs Unix line ending convention; warning seen but benign |
| M365 | Microsoft 365 | Outlook, Teams, etc. on this domain |
| MFA | Multi-Factor Authentication | Required by AICW tenant for management API access |
| MX | Mail Exchanger (DNS record) | |
| NS | Name Server (DNS record) | |
| OG | Open Graph (HTML meta tag set) | Social link previews on LinkedIn, X, etc. |
| OS | Operating System | |
| PRISM | Purpose-led, Roadmapped, Integrated Systems Model | The AI CustomWorks operating model per Project Instructions v1.4 |
| PR | Pull Request | PR #1 was the rebuild branch into main |
| RBAC | Role-Based Access Control | Azure permission model |
| SaaS | Software as a Service | |
| SAFe | Scaled Agile Framework | PRISM framework, not used in this document but standard in project context |
| SoW | Statement of Work | 2026-05-13 SoW v1.0 governs the engagement |
| SOA | Start of Authority (DNS record) | |
| SPF | Sender Policy Framework | Email authentication record |
| SRV | Service (DNS record) | Used for Teams federation |
| SSHFP | SSH Fingerprint (DNS record) | One.com-provisioned for hosting access; unused by EIS |
| SSL / TLS | Secure Sockets Layer / Transport Layer Security | Auto-provisioned by Azure SWA for custom domains |
| SSM | Soft Systems Methodology (Checkland) | PRISM framework, not used in this document but standard in project context |
| SWA | Azure Static Web App | The hosting service for the EIS website |
| TLD | Top-Level Domain | `.co.uk` here |
| TMF | Technology Management Framework | PRISM governing framework for technology decisions |
| TTL | Time To Live (DNS record TTL) | |
| TXT | Text (DNS record) | Used for SPF, DMARC (if present), and validation tokens |
| UI / UX | User Interface / User Experience | |
| URL | Uniform Resource Locator | |
| VAT | Value Added Tax | Company identity field |

---

## 14. Review Guide

In accordance with PRISM Rule 12 and the Document Review Protocol v1.1.

### Confidence map by section

| Section | Confidence | Notes |
|---|---|---|
| §1 – §8 (v1.0 content) | High | Unchanged from v1.0; previously reviewed |
| §9 Production cutover | High | All actions executed and verified live via DNS queries and HTTP probes |
| §10 DKIM and Teams CNAME recovery | High | Verified post-migration that all three records resolve from public DNS |
| §11 Backlog | Medium | Items captured accurately; priorities are this author's read, not validated with stakeholders |
| §12 Acceptance status | High | Each criterion walked through by Damo on the preview URL on 2026-05-21 |
| §13 Acronym table | Medium | Standard meanings; one-line notes are this author's framing |

### Declared assumptions

1. The "AI CustomWorks Sandpit" subscription is acceptable as the production location for the EIS website. (Backlog 11.5 may revisit.)
2. The SoW §3.2 / §4 framing of DNS cutover as Customer-side work is accepted; today's work is documented in this engagement record but does not extend the engagement scope.
3. The Azure DNS migration was unplanned scope but acceptable under the related-party SoW arrangement, no separate billing or amendment needed.

### Unverified claims

1. The DKIM gap on Stackdns is assumed to have been silently broken for "an unknown period". No historical evidence was retrieved to confirm when it broke.
2. The §11.10 LinkedIn OG preview is not yet validated; deferred per criterion text and Backlog 11.6.

### Scope expansions versus original Brief and SoW

| Expansion | Recorded in |
|---|---|
| Three hot-fix commits during acceptance walkthrough | §9.1 |
| Azure DNS migration (full DNS hosting provider change) | §9.2 |
| Cross-tenant Azure access configuration | §9.4 |
| ScoreApp branded URL setup (originally deferred per Handover) | §9.5 |
| DKIM and Teams CNAME recovery as migration side-effect | §10 |

### Three priority review items

1. **Decide whether to keep the EIS website in the "AI CustomWorks Sandpit" subscription or migrate to a production-named subscription.** Affects naming hygiene and any future audit trail.
2. **Decide on DMARC policy for `eisconsulting.co.uk`.** SPF and DKIM are present; the natural next step is publishing a DMARC record (start with `p=none` for reporting only).
3. **Investigate the elevated-access warning in AICW tenant IAM.** Identify the user, verify whether the elevation is needed, and either narrow scope or accept and document.

### Estimated review time

15 to 20 minutes for a focused read of §9 onwards. The v1.0 content (§1 to §8) is unchanged and does not require re-review.

---

*Document produced under PRISM Project Instructions v1.4. Stage 3 delivery by AI CustomWorks Ltd for EIS Consulting Ltd. Production cutover documented post-engagement-close per SoW §9.1(a).*