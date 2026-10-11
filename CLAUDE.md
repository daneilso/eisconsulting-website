# CLAUDE.md

Marketing website for **EIS Consulting Ltd**, live at **https://eisconsulting.co.uk**. EIS offers senior technology and delivery capability, on a proportionate commitment, to regulated organisations: UK law firms and central government. The site was rebuilt in May 2026 under an AICW (AI CustomWorks) engagement and signed off on 2026-05-21. In October 2026 it moved from three sector pages (legal, accountancy, healthcare) to two pathways (legal, government) built on the same method, using the v3.0 copy document in the repo root.

## Tech stack

- **Plain static HTML + CSS.** No framework, no build step, no `package.json`.
- The only JavaScript is the Microsoft Clarity analytics snippet in each page's `<head>`, plus inline `onclick` Clarity events on some CTAs.
- 8 hand-written pages, one `index.html` per folder:
  - `src/index.html`: home, with a hero offering two pathway buttons (Legal AI Governance, Government Agile Delivery)
  - `src/legal/`: Legal AI Governance, home of the From Policy to Practice offer
  - `src/legal/avoidable-requisitions/`: the conveyancing service and home of the Avoidable Requisition Diagnostic. It is listed under Legal in the footer navigation only, because the header has no sub menu. The header highlights Legal on this page using `aria-current="true"`.
  - `src/government/`, `src/approach/` (the EIS Augmentation Method, assembled from the home page sections), `src/contact/`, `src/privacy-policy/`, `src/terms-of-use/`
- The old healthcare and accountancy pages were deleted in October 2026 and can be recovered from git history. Their URLs 301-redirect to `/` through the rules below.
- One stylesheet, `src/assets/styles.css`, shared by every page.
- `src/staticwebapp.config.json` holds three wildcard rules, each a 301 to `/`: `/general-practice*`, `/healthcare*` and `/accountancy*`. Azure SWA treats `/x` and `/x/` as the same route, so separate rules for each fail deployment validation. Use one wildcard rule per retired path.
  - Redirects are applied by Azure only. `python -m http.server` ignores them. The local SWA emulator (`npx @azure/static-web-apps-cli start src --swa-config-location src`) loads the file but only matches the bare path for a trailing `*`, so it redirects `/healthcare` but not `/healthcare/`. That is an emulator limit, as the older `/general-practice*` rule behaves the same way. Confirm redirects on the PR preview site, for example `curl -I https://<preview-host>/healthcare/`.
- Assets are in `src/assets/` (logos, favicons, `og.png`). There are also copies of `og.png` and `favicon.png` in `src/` itself, which the social tags and the root favicon link point to.

### Conventions and house style

- **Every link and asset path is root-absolute** (`/assets/styles.css`, `/legal/`), so `src/` is the web root. To preview locally, serve it as root, for example `npx serve src` or `python -m http.server -d src`.
- The header, nav, footer and Clarity snippet are **duplicated in all 8 pages**, because there are no templates. A change to any of them must be made in every file.
- Every page has its own `<head>` with:
  - title, description and favicons
  - a `rel="canonical"` link to the **apex** URL (`https://eisconsulting.co.uk/<page>/`), which is the canonical form; `www` is secondary
  - Open Graph and Twitter tags using apex URLs
- Accessibility: a skip link targets `<main id="main-content" tabindex="-1">`. The `tabindex="-1"` is what lets focus actually move there (WCAG 2.4.1), so keep it.
- Copy rules: UK English (`lang="en-GB"`), **no em-dashes** in rendered copy, no placeholder or template text, and titles written subject-first with a pipe (`|`) separator.
- The copy source of truth is `2026-10-11 - Copywrite - EIS Consulting — Homepage Copy & LinkedIn Micro-Posts v3.0.md` in the repo root, which also holds the ten house style rules. For example: say "proportionate", never "fractional"; no hyphens in prose; qualify rather than assert; write full sentences; frame the end of an engagement as a transfer, not an exit. The rendered copy matches that document word for word.
- Content still waiting on real material (anonymised client references, LinkedIn article cards, the From Policy to Practice PDF link, the contact form) is already built but sits inside HTML comments that begin `HIDDEN UNTIL FILLED`. Search for that phrase to find them. Each comment says how to publish it.

### Analytics events (Microsoft Clarity, project `wqha1gwbg3`)

CTAs fire custom events using `onclick="if(window.clarity)clarity('event','<name>');"`. Keep these names unchanged, since reporting depends on them:

| Page | Events |
|---|---|
| Home | `hero_cta_law_proposition` (Legal AI Governance button), `hero_cta_government_proposition` (Government Agile Delivery button) |
| Avoidable requisitions | `scorecard_cta_click_drb` (both diagnostic CTAs, hero and closing) |

`scorecard_cta_click_drb` moved with the diagnostic CTA from the Legal page to the avoidable requisitions page. `hero_cta_law_diagnostic`, `hero_cta_healthcare_waitlist` and `hero_cta_accountancy_waitlist` were retired with the old home hero and are no longer fired.

The privacy policy discloses Clarity, so update it if analytics or third parties change.

### External services embedded or linked

- **Microsoft Forms** (`forms.cloud.microsoft`): the contact form is planned as an iframe embed on `contact/`, hidden until the form exists (see the comment in that file). The old waitlist embeds on the healthcare and accountancy pages were removed with those pages and survive only in git history. Responses go to the M365 tenant. Embedding them causes a harmless service-worker console warning.
- **ScoreApp** at `https://diagnostic.eisconsulting.co.uk`: the diagnostic scorecard, linked from the hero and closing CTAs of `legal/avoidable-requisitions/`.

## Deployment (CI/CD)

- **Host:** Azure Static Web Apps, resource `EISConsultingWebsite`.
  - Default hostname: `witty-cliff-0ea22e003.6.azurestaticapps.net`
  - Tenant and subscription: AICW tenant, subscription "AI CustomWorks Sandpit"
  - Resource group: `rg-eis-websit`
- **Pipeline:** `.github/workflows/azure-static-web-apps-witty-cliff-0ea22e003.yml`, using `Azure/static-web-apps-deploy@v1`.

| Trigger | Job | Result |
|---|---|---|
| Push to `main` | `build_and_deploy_job` | Deploys to production |
| PR to `main` opened or updated | `build_and_deploy_job` | Deploys a preview site for the PR |
| PR closed | `close_pull_request_job` | Deletes the preview site |

- **Config:** `app_location: "./src"`, `output_location: "./src"`, `api_location: ""`. There's no build step and no Functions API.
- **Auth:** the GitHub secret `AZURE_STATIC_WEB_APPS_API_TOKEN_WITTY_CLIFF_0EA22E003`, plus `GITHUB_TOKEN` for PR comments.
- **Workflow:** branch, then open a PR and check the preview site. Merging to `main` deploys to production straight away.
- The GitHub repo is `daneilso/eisconsulting-website`. It was previously named `EIS-Website-v2`, and the old URL redirects. The tag `v0-pre-rebuild` marks the site before the rebuild.

## Infrastructure

- **No backend, API or database.** The repo contains no connection strings or secrets apart from the GitHub Actions secret references above.
- **DNS:** Azure DNS zone `eisconsulting.co.uk`.
  - Location: EIS tenant, resource group `eis-dns`, UK South
  - Nameservers: `ns*-07.azure-dns.*`
  - The domain is registered at One.com. The One.com hosting subscription was renewed on 2026-10-11, mainly to keep its five legacy mailboxes. The website itself is not hosted there.
- **DNS records:**
  - Apex: an alias A record pointing to the SWA resource
  - `www`: CNAME to the SWA default hostname
  - SSL is provisioned automatically by Azure
  - `diagnostic`: CNAME to `dns.scoreapp.net`
  - The zone also holds the M365 mail and Teams records (MX, SPF, DKIM `selector1` and `selector2`, DMARC `p=none`, autodiscover, lyncdiscover and SIP/SRV)
- **Cross-tenant setup:** the DNS zone is in the EIS tenant and the SWA is in the AICW tenant. The guest account `Damian.Neilson@eisconsulting.co.uk` has Reader on the SWA and DNS Zone Contributor on `eis-dns`.
- **Engagement records:** the dated `2026-05-*.md` files in the repo root are the audit, brief, SoW and closeouts for the rebuild. The Stage 3 Closeout v1.1 is the most complete record of decisions, the cutover and the backlog.

## Open items (from Closeout v1.1, as of 2026-10-11)

- **One.com mailboxes: resolved, data safe.** The subscription was renewed on 2026-10-11, before the 2026-10-21 expiry, so the five mailboxes (~680 MB) are kept and no longer at risk. Before the next renewal, decide whether they're still needed or should be migrated to M365 (Backlog 11.9, no longer urgent).
- Tighten DMARC from `p=none` to `quarantine`, then `reject`, after reviewing the aggregate reports.
- Production SWA is in a subscription named "Sandpit" (governance review, Backlog 11.5).
- Investigate the elevated-access user warning in the AICW tenant IAM (Backlog 11.1).
- Housekeeping:
  - `src/assets/{48,180,192,512} px.png` (with spaces in their names) and `eis-icon-transparent.png` aren't referenced by any page.
  - `README.md` is just a heading.

### Added with the v3.0 copy rebuild (2026-10-11)

- **Contact form:** the copy document specifies a form (name, organisation, role, sector, free text) but the site has no backend. Create the Microsoft Form, then un-hide the embed in `src/contact/index.html`. Until then the page shows only the direct contact details.
- **Placeholders to fill:** article cards (home), client references and further reading (legal, avoidable requisitions, government), the From Policy to Practice PDF link (legal).
- **Approach page** reuses the home page principles and steps. A longer treatment is still to be written.
- **Privacy policy** still mentions waitlists (sections 2, 3 and 4). Review it and update its "Last updated" date.
- **`og.png`** still reads "AI Compliance for UK Regulated Businesses" and does not mention government. Replace it, and bump the `?v=` query on the social tags.
- **Mobile footer:** the footer brand block clips at the right edge on phones. This predates the rebuild and needs a CSS fix.
