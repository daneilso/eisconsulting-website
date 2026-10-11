# Claude Code Set Up: PWA Baseline on Azure and GitHub

A repeatable process for building Progressive Web Apps that install and run on phones and in desktop browsers. Everything here is a **default**. If a project needs to deviate, record the deviation and the reason in that project's own `CLAUDE.md`.

Last reviewed: 2026-10-11. Version numbers and preview-feature status change quickly, so work through section 10 before relying on any of them.

---

## 1. Strategy in one page

| Layer | Default | Why |
|---|---|---|
| Frontend | Next.js (App Router) + TypeScript, **static export** | PWA tooling is mature, and the output is plain files Azure Static Web Apps (SWA) serves well |
| Hosting | Azure Static Web Apps | Global CDN, free TLS, custom domains, and a preview environment for every pull request |
| Backend API | Azure Functions (HTTP triggers), Node.js + TypeScript | One language across the stack. Managed by SWA, so same origin and no CORS |
| Database | Azure Cosmos DB for NoSQL (serverless), or Azure SQL (serverless) | See the decision table in section 5 |
| CI/CD | GitHub Actions | PR opens: preview. Merge to `main`: production |
| Infrastructure | Bicep in `infra/` | Reviewable, repeatable, and works with `what-if` |
| Secrets | Azure Key Vault and SWA application settings. Never the repo | |

Design principles:

1. **Serverless and scale-to-zero by default.** A new project should cost close to nothing while idle.
2. **Static first.** Pre-render everything possible. Dynamic behaviour goes in the API, not server-side rendering, until there's a proven need.
3. **Same origin.** The frontend calls `/api/*` on its own domain. This avoids CORS configuration and keeps cookies and auth simple.
4. **Every change is previewed.** Nothing reaches production without having run in a PR preview environment first.
5. **Offline is a feature you design.** Decide per screen what works offline. Don't bolt it on afterwards.

---

## 2. Infrastructure stack

```
 Browser / installed PWA
        │  HTTPS
        ▼
 ┌──────────────────────────── Azure Static Web Apps ───────────────────────────┐
 │  Static files (web/out)   staticwebapp.config.json (routes, headers, auth)   │
 │  /.auth/*  built-in auth (Entra ID, GitHub)                                  │
 │  /api/*  ───────────►  Azure Functions (managed, HTTP triggers)              │
 └───────────────────────────────────────────────┬──────────────────────────────┘
                                                 │ SDK, connection from app settings
                                                 ▼
                              Cosmos DB (serverless)  or  Azure SQL (serverless)

 Alongside: Application Insights + Log Analytics, Key Vault, optional Entra app registration
```

### Azure Static Web Apps

- **Free plan** for development and small projects. **Standard plan** when you need SLA, bring-your-own Functions, custom Entra ID auth, private networking, or more preview environments.
- `staticwebapp.config.json` lives in `web/public/` so it's copied into `web/out/`. It controls routing, 404 handling, response headers and role-based access.
- SWA creates a **staging environment per pull request** (frontend and managed API together) and deletes it when the PR closes.

### Azure Functions

- **Managed Functions** (in the SWA's `api/` folder) are the default. They're free with SWA, same-origin and zero extra setup. They are HTTP-trigger only.
- Move to **bring-your-own Functions** (a separate Function App linked to SWA, Standard plan) when you need any of the following:
  - timers
  - queues
  - Durable Functions
  - managed identity to the database
  - VNet integration
  - non-HTTP triggers
- Use the Node.js v4 programming model (`@azure/functions` v4) in TypeScript. For C#, use the **isolated worker** model only. The in-process model is being retired.

### Database

- Provisioned in Bicep. Access from the API goes through the official SDK with the connection string in an application setting. Move to managed identity when the backend becomes bring-your-own Functions.
- **Previews must never touch production data.** See section 4.

### Cross-cutting

- **Observability:** Application Insights for the API, with sampling on, and a Log Analytics workspace.
- **Cost control:** set a budget alert on the resource group at creation time, prefer serverless tiers, and keep log retention short.
- **Region:** pick one region near the users (UK South for UK projects) and keep all resources in it.

---

## 3. Tech stack selection

### Frontend: Next.js + TypeScript (static export)

- Next.js App Router, TypeScript in `strict` mode, `output: "export"`, `trailingSlash: true`, `images.unoptimized: true`.
- Because it's a static export, these are **unavailable**: Next.js API routes, middleware, server components that fetch at request time, and image optimisation. Anything dynamic goes through `/api/*` on Functions.
- **Alternative: Vite + React + `vite-plugin-pwa`.** Choose this instead when the app is a pure single-page application with no SEO or marketing pages. It has the simplest and best-supported PWA tooling and the fewest hosting surprises. Everything else in this document applies unchanged.
- **Next.js hybrid rendering on SWA** (server-side rendering, incremental static regeneration) exists but has had preview status and size limits. Do not use it by default. Check section 10 if a project genuinely needs it.

### PWA layer

- **Manifest:** `app/manifest.ts` (or `public/manifest.webmanifest`) with name, short name, `start_url`, `display: "standalone"`, theme and background colours, and icons at 192, 512 and maskable 512.
- **Service worker:** build it **independently of the Next.js bundler** (Workbox `injectManifest` or Serwist's standalone build as a post-build step, writing `web/public/sw.js` or `web/out/sw.js`). That way a bundler change can't silently break offline support.
- **Caching strategy:**
  - Precache the app shell.
  - Stale-while-revalidate for safe `GET` API calls.
  - Cache-first for hashed static assets.
  - Never cache authenticated API responses without an explicit decision.
- **Offline:** ship an offline fallback page. Queue writes in IndexedDB. Background Sync isn't available in Safari or on iOS, so build a retry-on-reconnect path that works without it.
- **iOS specifics:** include `apple-touch-icon` (180×180) and the `apple-mobile-web-app-*` meta tags. iOS has no automatic install prompt, so provide a small "Add to Home Screen" hint. Web Push works only for installed PWAs.
- **Updates:** show a "new version available, reload" prompt when a new service worker is waiting. Don't skip waiting silently.

### Backend: Node.js + TypeScript (default) or C#

| Choose | When |
|---|---|
| **Node.js + TypeScript** (default) | A single language across frontend and backend, a small team, typical CRUD and integration logic |
| **C# (.NET isolated)** | Heavy domain logic, existing .NET libraries or team skills, or performance-critical processing |

- Validate every request body with **Zod** (TypeScript) or FluentValidation (C#) before it reaches any logic.
- Return a consistent error shape and never leak stack traces.
- Pick the highest Node.js LTS version that **both** SWA managed Functions and Azure Functions list as supported. Don't assume the newest.

### Tooling

- npm, with exact version pins and a committed lockfile. ESLint and Prettier. Vitest for unit tests. Playwright for end-to-end tests.
- Azure CLI (`az`), Azure Functions Core Tools (`func`), SWA CLI (`swa`), GitHub CLI (`gh`), Bicep (`az bicep`).
- Lighthouse for performance, accessibility, best practices and SEO. **Lighthouse no longer has a PWA category**, so check installability separately (manifest checks in a Playwright test, plus DevTools, Application panel).

---

## 4. Deployment pipeline (GitHub Actions)

| Event | Result |
|---|---|
| Pull request opened, updated or reopened | Lint, typecheck, test and build, then deploy a **preview environment**. SWA comments the preview URL on the PR |
| Pull request closed | The preview environment is deleted |
| Merge or push to `main` | The same checks, then deploy to **production** |

### Rules

- `main` is protected: changes arrive only by PR, with the CI check required to pass.
- **Build once, deploy what you tested.** The web app is built in CI and the exact output folder is deployed with `skip_app_build: true`. The API is built by SWA's build service from `api/`.
- **Previews use a dev database.** Set preview-environment application settings to a separate dev Cosmos DB (or SQL database), never production. Confirm this works before the first PR is opened.
- **Production deploys need no secrets in the repo.** The only stored secret is the SWA deployment token, kept as a GitHub secret.
- Optional: add `environment: production` on the production job and require a reviewer for releases that need a manual gate.
- **Rollback** is a revert commit on `main`. SWA has no one-click production rollback, so keep merges small.
- Infrastructure changes (Bicep) use a **separate workflow** that logs in to Azure with OIDC (federated credentials, no stored password). It runs `what-if` on PRs and applies only on merge, and only when `infra/**` changes.

### Baseline workflow

Save as `.github/workflows/azure-static-web-apps.yml`. Adjust the Node version and token secret name.

```yaml
name: Azure Static Web Apps CI/CD

on:
  push:
    branches: [main]
  pull_request:
    types: [opened, synchronize, reopened, closed]
    branches: [main]

concurrency:
  group: swa-${{ github.ref }}
  cancel-in-progress: true

jobs:
  build_and_deploy:
    if: github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed')
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version-file: .nvmrc
          cache: npm
          cache-dependency-path: |
            web/package-lock.json
            api/package-lock.json
      - name: Web checks and build
        working-directory: web
        run: |
          npm ci
          npm run lint
          npm run typecheck
          npm test --if-present
          npm run build
      - name: API checks
        working-directory: api
        run: |
          npm ci
          npm run lint
          npm run typecheck
          npm test --if-present
      - name: Deploy
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}
          repo_token: ${{ secrets.GITHUB_TOKEN }}
          action: upload
          app_location: web/out
          skip_app_build: true
          api_location: api
          output_location: ""

  close_pull_request:
    if: github.event_name == 'pull_request' && github.event.action == 'closed'
    runs-on: ubuntu-latest
    steps:
      - uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}
          action: close
```

---

## 5. Choosing the database

| | **Cosmos DB for NoSQL (serverless)** | **Azure SQL (serverless)** |
|---|---|---|
| Best for | Document-shaped data, per-user data, simple access patterns, offline-sync friendly | Relational data, joins, reporting, strict transactions |
| Idle cost | Pay per request, near zero | Auto-pauses, small storage cost |
| Free option | One free-tier account per subscription | A free offer is available per subscription (check current terms) |
| Gotchas | Design the **partition key** up front. Cross-partition queries cost more | Cold-start delay after auto-pause. Schema migrations need a process |
| SDK | `@azure/cosmos` | `mssql` or Prisma |

**Default: Cosmos DB (serverless)** unless the data is clearly relational or needs reporting. Record the choice and, for Cosmos, the partition key in the project's `CLAUDE.md`.

---

## 6. Repository layout

```
<project>/
├─ web/                       Next.js PWA (own package.json and lockfile)
│  ├─ public/                 sw.js (generated), icons, staticwebapp.config.json
│  └─ src/app/                manifest.ts, offline page, layout, pages
├─ api/                       Azure Functions (own package.json and lockfile)
│  ├─ src/functions/          one file per HTTP function (health.ts first)
│  ├─ host.json
│  └─ local.settings.sample.json     (local.settings.json is gitignored)
├─ infra/                     main.bicep, parameters per environment
├─ e2e/                       Playwright tests
├─ .github/workflows/         azure-static-web-apps.yml, infra.yml
├─ .nvmrc
├─ CLAUDE.md                  project facts, written as you scaffold
└─ README.md
```

`web/` and `api/` are deliberately **independent npm projects**. Sharing code between them (request and response types) is the one thing this makes harder. Start with a hand-maintained `web/src/lib/api-types.ts`. If duplication starts to hurt, move to an npm workspace with a `shared/` package, and switch the API to a CI-built deploy because SWA's build service can't see code outside `api/`.

---

## 7. Scaffolding instructions for Claude Code

Follow these in order. **Ask the user before step 8** (creating Azure resources costs money and is outward-facing). Commit after each numbered step that changes files.

### 1. Gather inputs

Ask for, and don't guess:

- Project name (kebab-case) and display name
- Azure subscription and region
- GitHub owner and repository name (new or existing)
- Database choice (section 5). If unsure, use the default
- Whether sign-in is needed (built-in SWA auth with Entra ID or GitHub)
- Backend language (default TypeScript)

### 2. Preflight

Check what's installed and report gaps. Don't install silently.

```bash
node -v && npm -v && git --version
gh --version        # winget install GitHub.cli
az version          # winget install Microsoft.AzureCLI
func --version      # winget install Microsoft.Azure.FunctionsCoreTools
az bicep version    # az bicep install
```

Confirm `gh auth status` and `az account show` point at the right account.

### 3. Create the repo and skeleton

Create the folders from section 6. Add `.gitignore` (`node_modules`, `out`, `.next`, `dist`, `local.settings.json`, `.env*`), `.nvmrc`, and a `README.md`. Protect `main` once the repo exists on GitHub.

### 4. Scaffold the web app

```bash
npx create-next-app@latest web --typescript --app --eslint --src-dir --use-npm --import-alias "@/*"
```

Then set `web/next.config.ts`:

```ts
import type { NextConfig } from "next";

const config: NextConfig = {
  output: "export",
  trailingSlash: true,
  images: { unoptimized: true },
};

export default config;
```

Add `typecheck` (`tsc --noEmit`) and `test` scripts to `web/package.json`. Run `npm run build` and confirm `web/out/index.html` exists.

### 5. Add the PWA layer

1. `web/src/app/manifest.ts` with the fields in section 3. Create icons (192, 512, maskable 512, and a 180×180 `apple-touch-icon`) in `web/public/`.
2. A service worker built as a post-build step (Workbox `injectManifest` or Serwist standalone) that outputs `sw.js` into `web/out/`.
3. A small client component that registers the worker and shows the "new version available" prompt.
4. `web/src/app/offline/page.tsx`, precached and used as the navigation fallback.
5. `apple-mobile-web-app-*` meta tags in the root layout.
6. After `npm run build`, confirm `web/out/manifest.webmanifest` and `web/out/sw.js` both exist.

### 6. Add `staticwebapp.config.json`

Put it in `web/public/`:

```json
{
  "routes": [
    { "route": "/sw.js", "headers": { "cache-control": "no-cache" } },
    { "route": "/manifest.webmanifest", "headers": { "cache-control": "no-cache" } },
    { "route": "/_next/static/*", "headers": { "cache-control": "public, max-age=31536000, immutable" } }
  ],
  "responseOverrides": {
    "404": { "rewrite": "/404.html" }
  },
  "globalHeaders": {
    "X-Content-Type-Options": "nosniff",
    "Referrer-Policy": "strict-origin-when-cross-origin",
    "Permissions-Policy": "camera=(), microphone=(), geolocation=()"
  }
}
```

The service worker file **must** be served with `no-cache`, or users get stuck on old versions. For protected APIs, add `{ "route": "/api/*", "allowedRoles": ["authenticated"] }`. Add a `Content-Security-Policy` after testing it as Report-Only first. Next.js's inline bootstrap scripts need hashes or `'unsafe-inline'` in a static export.

### 7. Scaffold the API

```bash
func init api --worker-runtime node --language typescript --model V4
cd api && func new --template "HTTP trigger" --name health
```

Make `health` return `{ "status": "ok" }` and check it responds at `/api/health`. Add a Zod validation helper, a consistent error response, and `local.settings.sample.json` listing every setting name with placeholder values. Add `lint`, `typecheck` and `test` scripts. Check that the SWA CLI can run the app and API together:

```bash
npx @azure/static-web-apps-cli start http://localhost:3000 --run "npm run dev --prefix web" --api-location api
```

### 8. Provision Azure (confirm with the user first)

Write `infra/main.bicep` for these resources:

- the Static Web App
- the database account (and database and container, or SQL server and database)
- Application Insights and Log Analytics
- Key Vault
- a budget alert

Show the user the plan before applying anything:

```bash
az group create -n rg-<project> -l <region>
az deployment group what-if -g rg-<project> -f infra/main.bicep
# apply only after the user approves:
az deployment group create -g rg-<project> -f infra/main.bicep
```

Set application settings (database connection, anything secret) on the SWA. Make sure the preview environment points at a **dev** database, not production.

### 9. Wire up CI/CD

1. Fetch the SWA deployment token and store it **without printing it**, for example by piping it straight into `gh secret set AZURE_STATIC_WEB_APPS_API_TOKEN`.
2. Add `.github/workflows/azure-static-web-apps.yml` from section 4.
3. Add the infra workflow with OIDC login (federated credential on an Entra app registration), `what-if` on PRs and apply on merge.
4. Require the CI check on `main` in branch protection.

### 10. Add tests and quality gates

- A Playwright smoke test: the home page loads, `/api/health` returns ok, the manifest is valid and linked, and the service worker registers.
- Lighthouse CI for performance, accessibility, best practices and SEO, with thresholds set in the repo.
- A short check that `sw.js` and the manifest are served with the expected headers.

### 11. Prove the pipeline end to end

Open a PR from a feature branch. Confirm that checks run, a preview URL is posted, and the preview works and uses the dev database. Install it on a phone and on desktop. Merge, and confirm production updates and the old preview is deleted.

### 12. Write the project's `CLAUDE.md`

Record the actual facts: names and region, database choice (and partition key), resource group, workflow file names, secret names, preview/production data setup, and any deviation from this baseline. Do not copy this document into it. Link to it.

---

## 8. Rules for Claude Code sessions

- **Confirm before** creating or deleting Azure resources, changing DNS, force-pushing, or anything else that is hard to reverse or costs money.
- **Never commit** secrets, `local.settings.json`, `.env` files or tokens. Never print a deployment token or connection string into the terminal output or a doc.
- Work on a branch and open a PR. Don't push straight to `main`.
- Use `what-if` for infrastructure before applying it.
- Don't invent version numbers. Look up the current supported versions at scaffold time (section 10).
- On Windows with Defender Controlled Folder Access, shell tools other than git may be blocked from writing to protected folders. Use the file edit tools for file changes.

---

## 9. Definition of done for a new PWA project

- [ ] `web/` builds to a static export. `web/out` contains `manifest.webmanifest` and `sw.js`
- [ ] The app installs on Android (Chrome), iOS (Safari, Add to Home Screen) and desktop (Chrome or Edge)
- [ ] The offline fallback page appears when the network is off
- [ ] `/api/health` works locally and in the preview
- [ ] A PR creates a preview and closing the PR removes it
- [ ] Merging to `main` deploys to production
- [ ] Previews use a dev database, and production data can't be reached from a preview
- [ ] No secrets in the repo. The infra workflow uses OIDC
- [ ] Security headers are set. CSP is at least in Report-Only
- [ ] `sw.js` and the manifest are served `no-cache`
- [ ] Lighthouse thresholds pass, and the budget alert exists
- [ ] The project's `CLAUDE.md` records the real setup

---

## 10. Verify at scaffold time

These details were written from memory and not checked against live documentation. Before relying on any of them, check the current Microsoft and Next.js docs and update this file if they've changed:

1. **Next.js on SWA:** the current status and limits of hybrid rendering, and that `output: "export"` is still the recommended path.
2. **Managed Functions limits:** supported runtimes and versions (Node.js, .NET, Python), HTTP-trigger-only, and whether managed identity or Key Vault references are supported on the Free and Standard plans.
3. **Plan limits:** staging environment counts, bandwidth, app size and custom domain limits on Free versus Standard.
4. **Per-environment application settings:** exactly how to give preview environments different settings from production.
5. **Deploy action:** that `skip_app_build`, `app_location` pointing at a pre-built folder, and the URL output behave as in section 4.
6. **Service worker tooling:** which of Workbox `injectManifest` and Serwist works with the current Next.js bundler.
7. **Database free offers:** current terms for the Cosmos DB free tier and the Azure SQL free offer.
8. **SWA database connections (Data API builder):** whether it's generally available. It could replace hand-written CRUD functions for simple data access.
9. **Lighthouse:** confirm the PWA category is still absent, and decide how installability is checked.
10. **.NET:** that the in-process model is retired and only isolated worker remains.
