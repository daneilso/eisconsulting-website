# CLAUDE.md

Marketing website for **EIS Consulting Ltd**, live at **https://eisconsulting.co.uk**. EIS offers fractional senior technology leadership to owner-led firms in regulated UK sectors: legal, accountancy and healthcare. The site was rebuilt in May 2026 under an AICW (AI CustomWorks) engagement and signed off on 2026-05-21.

## Tech stack

- **Plain static HTML + CSS.** No framework, no build step, no `package.json`.
- The only JavaScript is the Microsoft Clarity analytics snippet in each page's `<head>`, plus inline `onclick` Clarity events on some CTAs.
- 7 hand-written pages, one `index.html` per folder:
  - `src/index.html`: home, with a hero split into sector columns
  - `src/legal/`, `src/accountancy/`, `src/healthcare/`: sector pages
  - `src/contact/`, `src/privacy-policy/`, `src/terms-of-use/`
- One stylesheet, `src/assets/styles.css`, shared by every page.
- `src/staticwebapp.config.json` holds a single wildcard rule: `/general-practice*` 301-redirects to `/healthcare/`. Azure SWA treats `/x` and `/x/` as the same route, so separate rules for each fail deployment validation. Use one wildcard rule.
- Assets are in `src/assets/` (logos, favicons, `og.png`). There are also copies of `og.png` and `favicon.png` in `src/` itself, which the social tags and the root favicon link point to.

### Conventions and house style

- **Every link and asset path is root-absolute** (`/assets/styles.css`, `/legal/`), so `src/` is the web root. To preview locally, serve it as root, for example `npx serve src` or `python -m http.server -d src`.
- The header, nav, footer and Clarity snippet are **duplicated in all 7 pages**, because there are no templates. A change to any of them must be made in every file.
- Every page has its own `<head>` with:
  - title, description and favicons
  - a `rel="canonical"` link to the **apex** URL (`https://eisconsulting.co.uk/<page>/`), which is the canonical form; `www` is secondary
  - Open Graph and Twitter tags using apex URLs
- Accessibility: a skip link targets `<main id="main-content" tabindex="-1">`. The `tabindex="-1"` is what lets focus actually move there (WCAG 2.4.1), so keep it.
- Copy rules: UK English (`lang="en-GB"`), **no em-dashes** in rendered copy, no placeholder or template text, and titles written subject-first with a pipe (`|`) separator.

### Analytics events (Microsoft Clarity, project `wqha1gwbg3`)

CTAs fire custom events using `onclick="if(window.clarity)clarity('event','<name>');"`. Keep these names unchanged, since reporting depends on them:

| Page | Events |
|---|---|
| Home | `hero_cta_law_proposition`, `hero_cta_law_diagnostic`, `hero_cta_healthcare_waitlist`, `hero_cta_accountancy_waitlist` |
| Legal | `scorecard_cta_click_drb` |

The privacy policy discloses Clarity, so update it if analytics or third parties change.

### External services embedded or linked

- **Microsoft Forms** (`forms.cloud.microsoft`): waitlist iframes on `healthcare/` and `accountancy/`. Responses go to the M365 tenant. Embedding them causes a harmless service-worker console warning.
- **ScoreApp** at `https://diagnostic.eisconsulting.co.uk`: the diagnostic scorecard, linked from the home hero and the Legal page CTA.

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
  - The domain is registered at One.com, which now provides the domain only.
- **DNS records:**
  - Apex: an alias A record pointing to the SWA resource
  - `www`: CNAME to the SWA default hostname
  - SSL is provisioned automatically by Azure
  - `diagnostic`: CNAME to `dns.scoreapp.net`
  - The zone also holds the M365 mail and Teams records (MX, SPF, DKIM `selector1` and `selector2`, DMARC `p=none`, autodiscover, lyncdiscover and SIP/SRV)
- **Cross-tenant setup:** the DNS zone is in the EIS tenant and the SWA is in the AICW tenant. The guest account `Damian.Neilson@eisconsulting.co.uk` has Reader on the SWA and DNS Zone Contributor on `eis-dns`.
- **Engagement records:** the dated `2026-05-*.md` files in the repo root are the audit, brief, SoW and closeouts for the rebuild. The Stage 3 Closeout v1.1 is the most complete record of decisions, the cutover and the backlog.

## Open items (from Closeout v1.1, as of 2026-10-11)

- **Overdue: One.com mailbox audit** (Backlog 11.9, due 2026-09-30). The One.com hosting plan expires on **2026-10-21**, and its five mailboxes (~680 MB) will be deleted then unless exported.
- Tighten DMARC from `p=none` to `quarantine`, then `reject`, after reviewing the aggregate reports.
- Production SWA is in a subscription named "Sandpit" (governance review, Backlog 11.5).
- Investigate the elevated-access user warning in the AICW tenant IAM (Backlog 11.1).
- Housekeeping:
  - `src/assets/{48,180,192,512} px.png` (with spaces in their names) and `eis-icon-transparent.png` aren't referenced by any page.
  - `README.md` is just a heading.
