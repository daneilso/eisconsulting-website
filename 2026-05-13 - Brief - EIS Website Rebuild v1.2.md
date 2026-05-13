# 2026-05-13 - Brief - EIS Website Rebuild v1.2

**Version:** 1.2
**Date:** 2026-05-13
**Author:** AI CustomWorks Ltd (Damo, Founder)
**For:** EIS Consulting Ltd (Damo, Founder)
**Classification:** Internal — Engagement Brief
**Status:** Final, ready for Stage 3
**Supersedes:** 2026-05-13 - Brief - EIS Website Rebuild v1.1
**Parent Documents:**
- 2026-04-30 - Project Instructions - AI CustomWorks PRISM v1.4
- 2026-05-11 - Canvas - EIS Master Value Canvas v0.10
- 2026-05-11 - Value Canvas - HMLR Defensible Requisition Blueprint v1.0
- 2026-05-13 - Audit - EIS Website Existing Site Inventory v1.0

---

## Version History

| Version | Date | Change |
|---|---|---|
| v1.0 | 2026-05-13 | Initial issue. Full brief covering home, legal, accountancy and general-practice stubs, contact hot-fix, privacy policy update, cross-cutting requirements. |
| v1.1 | 2026-05-13 | Three changes: em-dashes removed from all website copy; `/general-practice/` renamed to `/healthcare/` with 301 redirect; both stub sections confirmed as separate waitlists with sector-specific capture. |
| v1.2 | 2026-05-13 | Six changes resolving the v1.1 open items: (1) hero CTA confirmed as three sector-keyed buttons; (2) §6 sector cards retained as alternative considered path; (3) awkward prose items #1–#3 resolved using alternatives; (4) Company No and VAT No inserted into privacy policy spec; (5) Microsoft Clarity snippet baked in with project ID `wqha1gwbg3`; (6) waitlist anchor IDs added to stub pages for deep-linking from hero CTAs. |

---

## Executive Summary

This brief commissions Stage 3 of the EIS Consulting website rebuild. AICW will rebuild three pages (home, legal, contact), produce holding-page treatments for two sector stubs (accountancy, healthcare), and apply cross-cutting fixes for analytics instrumentation, social-share metadata, accessibility, and privacy policy disclosure.

The home page publishes the EIS Master Value Canvas v0.10 with three sector-keyed hero CTAs feeding the live Defensible Requisition Blueprint scorecard (law) and waitlists (healthcare, accountancy). The legal page publishes the HMLR Defensible Requisition Blueprint v1.0 proposition with a scorecard CTA. The two stub pages register the sector as in-scope without making promises EIS cannot yet deliver. Microsoft Clarity instrumentation is baked into every page. Existing design tokens and the Azure Static Web Apps hosting pipeline are inherited unchanged.

All copy is locked. Stage 3 implements; it does not redraft. Deviation requires re-issue at v1.3.

---

## Acronym Definition Table

| Acronym | Definition | Project-Specific Note |
|---|---|---|
| AICW | AI CustomWorks Ltd | Provider on this engagement |
| AR | Avoidable Requisition | HMLR's published metric for conveyancing errors |
| ARIA | Accessible Rich Internet Applications | W3C accessibility attribute specification |
| ATM | Ascending Transaction Model | DENT Global product-progression concept |
| CLS | Cumulative Layout Shift | Core Web Vitals metric |
| COLP | Compliance Officer for Legal Practice | SRA-required role in regulated law firms |
| CSP | Content Security Policy | HTTP response header controlling resource loading |
| CTA | Call to Action | Conversion-driving element |
| DENT | DENT Global | Daniel Priestley's KPI methodology organisation |
| DRB | Defensible Requisition Blueprint | EIS proposition for the legal sector |
| EIS | EIS Consulting Ltd | Customer on this engagement |
| GDPR | General Data Protection Regulation | UK data protection law |
| HMLR | His Majesty's Land Registry | UK government registration authority for land and property |
| ICO | Information Commissioner's Office | UK data protection regulator |
| ICP | Ideal Customer Profile | DENT canvas element identifying target buyer |
| KPI | Key Person of Influence | DENT Global brand-architecture programme |
| OG | Open Graph | Social media preview metadata protocol |
| PRISM | Purpose-led, Roadmapped, Integrated Systems Model | AICW internal operating model, not for external use |
| SoW | Statement of Work | Engagement-defining commercial document |
| SRA | Solicitors Regulation Authority | UK regulator for solicitors |
| SSM | Soft Systems Methodology | Checkland's problem-structuring discipline |
| TMF | Technology Management Framework | Five-stage governance model: Identification, Selection, Acquisition, Protection, Exploitation |
| VAT | Value Added Tax | UK indirect tax administered by HMRC |

---

## 1. Engagement Context

This engagement is the first end-to-end execution of the EIS-feeds-AICW model defined in PRISM Project Instructions v1.4. EIS Consulting has identified a problem (canvas-aligned public website needed to capture and qualify leads against the Defensible Requisition Blueprint proposition). AICW delivers the solution.

Treat this as the v1.0 instance of the AICW customer engagement template. A parallel Statement of Work governs commercial terms.

---

## 2. Scope

### 2.1 In Scope

| Page | URL | Treatment | Source canvas |
|---|---|---|---|
| Home | `/` | Full rebuild with three sector-keyed hero CTAs | Master Value Canvas v0.10 |
| Legal | `/legal/` | Full rebuild, live proposition page | DRB v1.0 |
| Accountancy | `/accountancy/` | Holding page with waitlist form | — |
| Healthcare | `/healthcare/` | Holding page with waitlist form. **Renamed from `/general-practice/`.** 301 redirect maintained from legacy URL. | — |
| Contact | `/contact/` | Hot-fix only (remove draft copy) | — |
| Privacy Policy | `/privacy-policy/` | Add Microsoft Clarity disclosure; insert Company No and VAT No | — |

### 2.2 Cross-Cutting Work

- Microsoft Clarity analytics integration across all pages (project ID `wqha1gwbg3`)
- OG meta tag fixes (Azure preview URL to production domain) across all pages
- Accessibility fixes (skip-nav link, image dimensions, comment removal)
- ScoreApp CTA integration on legal page hero CTA AND legal page Prize section
- URL rename from `/general-practice/` to `/healthcare/` with 301 redirect

### 2.3 Out of Scope (Captured for Future Engagements)

- High-level business process aligned to each of the DRB method pillars *(queued)*
- Lead-handling processes for landing-page to ScoreApp to discovery funnel *(queued)*
- Sector scorecards for accountancy and healthcare
- Additional propositions for the legal page beyond DRB
- Coaching service line page
- Subscription platform page
- Custom domain DNS configuration (Damo executes via One.com once site is tested)

---

## 3. Brand and Design Constraints

The existing design system is inherited as-is. No new colours, no new fonts, no new components. The audit produced a complete inventory; Stage 3 reuses what is there.

| Token | Value | Use |
|---|---|---|
| `--bg` | `#0b1220` | Page background |
| `--card` | `#0f1a2e` | Card surface |
| `--text` | `#e8eefc` | Primary text |
| `--muted` | `#b8c6e6` | Secondary text |
| `--line` | `rgba(232,238,252,.12)` | Borders, dividers |
| `--accent` | `#6aa6ff` | Primary accent (blue) |
| `--accent2` | `#7cf0d6` | Secondary accent (mint) |
| `--radius` | `16px` | Card corners |
| `--shadow` | `0 12px 30px rgba(0,0,0,.35)` | Card shadow |
| `--max` | `1120px` | Max content width |

**Reuse components only:** `.hero`, `.hero--compact`, `.kicker`, `.h1`, `.h1--sm`, `.sub`, `.small`, `.ctas`, `.btn`, `.btn.primary`, `.card`, `.tag`, `.grid`, `.grid.cols-3`, `.stack`, `.stack--lg`, `.section-title`, `hr.sep`, `.container`, `.clean`, `.embed`.

**Permitted new utility class if needed:** `.grid.cols-4` for the four-principle Method section on the home page. Mirror the structure of `.grid.cols-3` at the 980px breakpoint.

**House style:** No em-dashes in any website copy. Em-dash replaced with comma and space (`, `). En-dashes used for numeric ranges (e.g. `5–20 fee earners`) are retained. Page titles use a pipe (`|`) as a separator where a separator is required.

---

## 4. Home Page Specification (`/index.html`)

### 4.1 Page Intent

Publish the EIS Master Value Canvas v0.10 in the buyer's voice. Speak to the Capacity-Constrained Owner-Principal across regulated SMEs. Surface a sector-keyed action in the hero for visitors who arrive ready to act, while preserving the Master canvas positioning narrative for visitors who need context first.

### 4.2 Section Order

1. Hero with three sector-keyed CTAs
2. The Pains (3-card grid)
3. The Mistakes (3-card grid)
4. The EIS Augmentation Method (4-card grid, new `.cols-4` variant)
5. The Payoffs (3-card grid)
6. The Prize and sector navigation (alternative considered path)
7. Footer (existing)

### 4.3 Locked Copy

**HERO**

- Kicker: `For owner-led firms in regulated sectors`
- H1: `Growth your firm sustains.`
- Sub: `EIS Consulting partners with managing partners and owner-principals to break the growth ceiling, without committing to permanent senior hires or fixed-cost expansion you can't yet justify.`
- Small: `Founded in the North East of England. Operating across the UK.`
- **CTAs:** Three buttons inside a `.ctas` container, laid out as a row on desktop and stacked on mobile. Button styling differentiates the live offering from the waitlists:

| Order | Label | Class | href | Click event |
|---|---|---|---|---|
| 1 | `Take the law diagnostic →` | `.btn.primary` | `[ScoreApp URL — to be supplied by Damo before push]` | `clarity('event','hero_cta_law_scorecard');` |
| 2 | `Join the healthcare waitlist →` | `.btn` | `/healthcare/#waitlist` | `clarity('event','hero_cta_healthcare_waitlist');` |
| 3 | `Join the accountancy waitlist →` | `.btn` | `/accountancy/#waitlist` | `clarity('event','hero_cta_accountancy_waitlist');` |

The law button is `.btn.primary` because it is the only converting product. The healthcare and accountancy buttons are `.btn` (bordered/secondary) because they capture interest rather than deliver a diagnostic. The visual hierarchy says "one of these three is the live thing." Hover and focus states are inherited from the existing button CSS.

**SECTION 2 — THE PAINS**

- Section title (`<h2 class="section-title">`): `Three pressures that move together`
- Sub-paragraph above grid (`<p class="sub">`): `For firms approaching their next stage of growth, these three pressures rarely arrive alone. Each one creates the conditions for the next, and the loop is closed from the inside.`
- Grid: `.grid.cols-3`
- Card structure: `.card` containing `<span class="tag">1</span>` (and 2, 3), `<h3>`, `<p>`

| # | h3 | p |
|---|---|---|
| 1 | Stalled Growth | Technology is one route through the growth ceiling, but the wisdom doesn't translate into specific decisions and action. Meanwhile, ambition and operational reality drift apart, and competitors who moved earlier extend their lead. |
| 2 | Leadership Drag | The technology work is being carried part-time by principals whose primary roles are business and department leadership. The result is shallow technology decisions and diluted leadership in the areas the firm most depends on its principals to lead. |
| 3 | Strained Decision-Making | Without dedicated technology management, technology decisions are being made under constrained inputs. The accumulated technology estate produces partial returns, and confidence in further investment quietly erodes. |

**SECTION 3 — THE MISTAKES**

- Section title: `Why the obvious responses don't work`
- Sub: `The standard market playbook for each pain has a built-in failure mode. Recognising the failure mode is the first step out of the loop.`
- Grid: `.grid.cols-3`
- Card structure: `.card` containing `<span class="tag">Mistake</span>`, `<h3>`, `<p>`

| # | h3 | p |
|---|---|---|
| 1 | Hiring through the ceiling | Growth and headcount are assumed to be linked, so the firm either commits to fixed cost it cannot justify against current revenue, or delays the growth decision indefinitely. Both leave the firm worse off than if a third path had been available. |
| 2 | Promoting into the technology seat | Distributed part-time technology leadership is producing weak outcomes, so the firm formalises the arrangement by giving an existing principal a clearer technology remit. The drag intensifies rather than resolving. The principal now carries the technology load alongside their existing role. |
| 3 | Buying advice instead of delivery | Consultancy reports describe what the firm should do, then leave. The firm's principals carry the same load they did before, only now with an unread report on the shelf. The output was different documents, when the firm needed different operations. |

**SECTION 4 — THE EIS AUGMENTATION METHOD**

- Section title: `The EIS Augmentation Method`
- Sub: `Four principles that operate together to import senior technology capability for the engagement period, deliver visible change, and graduate the firm to sustain the capability itself.`
- Grid: `.grid.cols-4` (new variant, reverts to single column below 980px)
- Card structure: `.card` containing `<span class="tag">Principle</span>`, `<h3>`, `<p>`

| # | h3 | p |
|---|---|---|
| 1 | Senior capability, fractional commitment | Senior technology leadership imported for the engagement period, at a cost proportionate to the engagement rather than to a permanent hire. The senior commitment ends when the engagement ends. |
| 2 | Specialist work, specialist hands | Technology leadership and delivery placed with people whose primary discipline this is, releasing the firm's principals to lead the business rather than carry the technology work alongside their primary roles. |
| 3 | Embedded delivery, visible change | EIS embeds in the firm's leadership structure, owns delivery of agreed projects, and produces visible change to how the firm operates. The output is different operations, not different documents. |
| 4 | Designed to end well | The engagement is structured from the outset to bring the firm to a position where it can sustain the capability internally, at which point the augmentation withdraws. Graduation is the success metric. |

**SECTION 5 — THE PAYOFFS**

- Section title: `What changes when the loop breaks`
- Sub: (none, three cards speak for themselves)
- Grid: `.grid.cols-3`
- Card structure: `.card` containing `<span class="tag">Payoff</span>`, `<h3>`, `<p>`

| # | h3 | p |
|---|---|---|
| 1 | Unlocked Growth | The firm achieves the next stage of growth without committing to the headcount and premises increase normally required. Ambition and operational reality come back into alignment. |
| 2 | Leadership Restored | The firm's principals are released to lead the business, without carrying part-time technology work. Strategic questions receive the principals' best thinking. |
| 3 | Confident Decisions | Technology decisions are made under conditions that match their importance. Investment produces anticipated outcomes, and confidence in further investment is restored. |

**SECTION 6 — THE PRIZE + SECTOR NAVIGATION**

This is the alternative considered path. The hero offers the fast route to action; §6 offers the route through context first.

- Section title: `Growth your firm sustains.` (use `.h1--sm`, not `.section-title`. The Prize is the destination.)
- Sub: `Want more context before you act? Read the sector proposition or interest page first.`
- Grid: `.grid.cols-3`
- Card structure: `.card` with `.tag` (status badge), `<h3>`, `<p>`, `.ctas` containing one `<a class="btn">` (no `.primary` on these, they are the alternative path)

| # | tag | h3 | p | Button label | Button href |
|---|---|---|---|---|---|
| 1 | `Live` | Law | The Defensible Requisition Blueprint. For managing partners of UK law firms with meaningful conveyancing volume who are carrying the weight of their firm's avoidable requisition rate. | Read the proposition → | `/legal/` |
| 2 | `In development` | Healthcare | The EIS Augmentation Method, translated for owner-principals in private practice, allied health, and healthcare services. Sector scorecard in development. | Read more → | `/healthcare/` |
| 3 | `In development` | Accountancy | The EIS Augmentation Method, translated for managing partners of UK accountancy practices. Sector scorecard in development. | Read more → | `/accountancy/` |

### 4.4 Page Metadata

- `<title>`: `EIS Consulting | Growth your firm sustains.`
- `<meta name="description">`: `EIS Consulting partners with managing partners and owner-principals in regulated UK SMEs to break the growth ceiling through fractional senior technology leadership, specialist delivery, and engagements designed to end when the firm can sustain the capability itself.`
- OG tags: see §9.2

---

## 5. Legal Page Specification (`/legal/index.html`)

### 5.1 Page Intent

Publish the Defensible Requisition Blueprint v1.0 proposition. Move the Requisition-Worried Managing Partner from recognition of the AR rate problem through the mechanism that perpetuates it, to the five-principle Blueprint that resolves it, to the 2% AR Rate Floor, and onward to the diagnostic scorecard.

### 5.2 Section Order

1. Hero
2. The Pains (3-card grid)
3. The Mistakes (5-card stack)
4. The Defensible Requisition Blueprint (5-card stack, paired with the Mistakes layout)
5. The Payoffs (3-card grid)
6. The Prize and ScoreApp CTA
7. Footer (existing)

### 5.3 Locked Copy

**HERO**

- Kicker: `For managing partners of UK conveyancing firms`
- H1: `Reach the 2% AR rate floor. Defend the rest.`
- Sub: `HMLR publishes your avoidable requisition rate. Some of the causes sit inside your firm. Some sit outside it. The Defensible Requisition Blueprint resolves the controllable portion and evidences the uncontrollable portion separately.`
- No hero buttons. CTA lives at the Prize section.

**SECTION 2 — THE PAINS**

- Section title: `Three pressures the AR rate creates`
- Sub: `If you are running a conveyancing department of 5–20 fee earners and the AR number has reached partner-level attention, you will recognise these.`
- Grid: `.grid.cols-3`

| # | h3 | p |
|---|---|---|
| 1 | Matters bounce back with requisitions | After submission, the same preventable issues keep triggering requisitions. The supervisor queue fills with "can you just look at this one" messages. Fee earners reopen files they thought were finished, post-completion becomes a loop of resubmissions, and time-to-register stretches. Non-billable rework drags on capacity that should be on live matters. |
| 2 | Files stuck in pending with no clean answer | Paused requisitions stop fee earners giving clients, lenders, and agents a clean answer to "is it registered yet?" The team absorbs repeated "what's stuck at HMLR?" check-ins. Supervisors chase status updates instead of preventing the next requisition. Post-completion feels like a black hole to everyone outside the firm. |
| 3 | A public number that includes causes you don't control | HMLR's published AR data includes firm-caused, HMLR-caused, and third-party-caused requisitions in a single headline rate. Panels, referrers, and clients form opinions from that rate even though the data cannot separate causes. The reputational weight of a blended number sits on the managing partner. |

**SECTION 3 — THE MISTAKES**

- Section title: `Why the standard responses don't move the number`
- Sub: `Five mistakes in thinking and action that keep the AR rate where it is. Each one maps to a stage of the matter lifecycle where intervention is possible and being missed.`
- Layout: `.stack--lg` of `.card` elements (vertical stack at 22px gap, not grid, five items)
- Card structure: `.card` with `.tag` (the principle area), `<h3>` (the wrong thinking, in quotes), `<p>` (the wrong action)

| # | tag | h3 (in quotes) | p |
|---|---|---|---|
| 1 | Intake | "We can tidy up Land Registry detail post-completion." | Thin intake means execution wording and restriction requirements are only discovered when HMLR bounces the application. By then the matter has already closed and the evidence is harder to recover. |
| 2 | Document pack | "The team knows what's needed, a checklist will slow us down." | Each fee earner builds their own pack. Certificates and supporting evidence get missed or are the wrong version. The variation lands as a requisition. |
| 3 | Submission review | "Everyone's already looked at the file, a final check is duplication." | No deliberate end-to-end review before submission, so HMLR is the first thing comparing the pack as one unit. Errors that any pre-submission cross-check would have caught are surfaced 20 business days later. |
| 4 | Tracking | "It's with HMLR now, tracking won't change anything." | Registration sits in limbo until a client chase or requisition triggers a fire drill. The 20-business-day response window starts ticking before the firm is paying attention. |
| 5 | Workflow | "HMLR's training is doing the heavy lifting, reminders and topping it up will get our AR rate to zero." | Partner emails and spot checks substitute for mapped, enforced workflow change. People revert under pressure, and the residual uncontrollable AR portion is mistaken for ongoing process failure. |

**SECTION 4 — THE DEFENSIBLE REQUISITION BLUEPRINT**

- Section title: `The Defensible Requisition Blueprint`
- Sub: `Five operational principles that resolve the controllable AR causes across the matter lifecycle, and evidence the uncontrollable portion separately. Together they describe what EIS delivers to a conveyancing department working under this engagement.`
- Layout: `.stack--lg` of `.card` elements (paired structurally with §3, same vertical rhythm)
- Card structure: `.card` with `.tag` (principle number), `<h3>` (principle name), `<p>` (principle description)

| # | tag | h3 | p |
|---|---|---|---|
| 1 | Principle 1 | Requisition-Proof Intake | Capture every execution detail, restriction requirement, and supporting-document trigger at the point of instruction, before exchange. The matter file leaves intake with the evidence HMLR will look for already assembled, not with a list of things to chase later. |
| 2 | Principle 2 | Document Pack Discipline | Standardise the exact supporting documents, certificates, and evidence per matter type, with versioned templates rather than fee-earner memory. The pack assembled for any transaction matches HMLR's practice guides every time, regardless of who built it. |
| 3 | Principle 3 | Submission Pack Reconciliation | One deliberate end-to-end cross-check before submission. Names, dates, plans, fees, SDLT/LTT evidence, and property descriptions are reconciled across every document in the pack. The submission is treated as a single unit before lodgement, not as a collection of separately-prepared parts. |
| 4 | Principle 4 | Submission-to-Registration Tracking | Registration treated as a tracked workflow with clear statuses, owners, and response windows. When HMLR raises a requisition, the firm sees it, owns it, and responds inside the 20-business-day window, and evidences the response trail when the cause sits outside the firm's control. |
| 5 | Principle 5 | Workflow Hardening | The discipline of the first four principles built into the firm's case management system through required fields, peer review gates, prompts, and submission blocks that prevent applications progressing while gaps remain. The workflow enforces the standard so individual memory does not have to. |

**SECTION 5 — THE PAYOFFS**

- Section title: `What changes when the Blueprint is in place`
- Grid: `.grid.cols-3`

| # | h3 | p |
|---|---|---|
| 1 | An AR rate you can stand behind | A public AR rate at the irreducible floor. Controllable causes resolved across the matter lifecycle. The uncontrollable residual separately evidenced through tracking, so panels and referrers see a number that tells a credible quality story. |
| 2 | Right-first-time submissions | Errors caught pre-submission rather than discovered through HMLR's response. Standardised packs reconciled as a single unit before lodgement. Fee earners able to give clients, lenders, and agents a clean answer to "is it registered yet?" |
| 3 | Public data on your side | The HMLR public dataset converted from a defensive reputational liability into an active quality signal. Panels and referrers see a measure the firm stands behind, supported by operational evidence rather than asserted by claim. |

**SECTION 6 — THE PRIZE + CTA**

- Section title: `2% AR rate floor.` (use `.h1--sm`)
- Sub: `The irreducible floor of avoidable requisitions for a firm running the Blueprint. Controllable causes resolved, uncontrollable causes separately defensible. The diagnostic below shows where your firm sits today and what the path looks like.`
- CTA container: `.ctas` centred under sub
- Primary button: `<a class="btn primary">`, label: `Take the diagnostic`; href: **[ScoreApp URL — to be supplied by Damo before push to main]**; click event: `clarity('event','scorecard_cta_click_drb');`
- Small text under button: `Five minutes. Fifteen questions. Your firm's AR position scored across the five Blueprint principles.`

### 5.4 Page Metadata

- `<title>`: `Defensible Requisition Blueprint | EIS Consulting`
- `<meta name="description">`: `For managing partners of UK conveyancing firms carrying the weight of HMLR's published AR rate. The Defensible Requisition Blueprint resolves controllable causes across the matter lifecycle and evidences the uncontrollable portion separately. Reach the 2% AR rate floor. Defend the rest.`

---

## 6. Stub Page Specifications

Both stubs follow the same structure: kicker, h1 (using `.h1--sm`), sub, three explanatory cards, and a waitlist form. **Each sector carries its own Microsoft Forms waitlist**, with sector-scoped capture fields. The waitlist form section carries the `id="waitlist"` anchor for deep-linking from the home page hero CTAs.

### 6.1 Healthcare (`/healthcare/index.html`)

**URL change from v1.0:** The page directory is renamed from `src/general-practice/` to `src/healthcare/`. A 301 redirect is configured in §9.5 to handle the legacy URL.

**Locked copy:**

- Kicker: `For owner-principals in healthcare`
- H1 (`h1--sm`): `Healthcare scorecard in development.`
- Sub: `EIS Consulting is producing a sector scorecard for owner-principals across private practice, allied health, and healthcare services. The Master EIS Augmentation Method is sector-agnostic; the healthcare-specific diagnostic is in development.`
- Section title: `What we're working on`
- Three cards (`.grid.cols-3`):

| # | h3 | p |
|---|---|---|
| 1 | The sector scope | Healthcare sub-sectors carry structural differences. Variable headcount, mixed clinical-business duality, and different regulatory regimes (CQC, GDC, GMC, NMC depending on sub-sector). The scorecard will surface these without flattening them. |
| 2 | The diagnostic | A short structured assessment showing where your practice sits against the conditions the EIS Augmentation Method resolves: stalled growth, leadership drag, and strained technology decision-making. |
| 3 | The next step | Release expected during 2026. Register your interest below to be notified when the diagnostic opens. |

- **Waitlist form section** — this section gets `id="waitlist"` on its container so `/healthcare/#waitlist` scrolls directly to it:
  - Section container: `<section id="waitlist">`
  - Section title: `Join the healthcare waitlist`
  - Sub: `Be notified when the healthcare diagnostic opens. We'll also send the first edition of the EIS healthcare positioning paper when it's published.`
  - Embed: Microsoft Forms iframe inside the existing `.embed` component
  - Form fields (Damo configures inside Microsoft Forms):
    - Name (required)
    - Email (required)
    - Organisation name (required)
    - Role (required)
    - Healthcare sub-sector (required, single-select: Private practice / Allied health / Healthcare services / Other)
    - What triggered your interest? (optional, short text)
  - Form URL: **[Microsoft Forms healthcare URL — to be supplied by Damo before push to main]**

### 6.2 Accountancy (`/accountancy/index.html`)

**Locked copy:**

- Kicker: `For managing partners of UK accountancy practices`
- H1 (`h1--sm`): `Accountancy scorecard in development.`
- Sub: `EIS Consulting is producing a sector scorecard for managing partners of UK accountancy practices facing the conditions the EIS Augmentation Method resolves. The Master EIS Augmentation Method is sector-agnostic; the accountancy-specific diagnostic is in development.`
- Section title: `What we're working on`
- Three cards (`.grid.cols-3`):

| # | h3 | p |
|---|---|---|
| 1 | The sector scope | UK accountancy practices typically operating with 5–25 staff, mixed assurance and advisory work, owner-principal led. The scorecard is built for managing partners carrying the firm's growth and operational decisions personally. |
| 2 | The diagnostic | A short structured assessment showing where your practice sits against the three pressures that move together: stalled growth, leadership drag, and strained technology decision-making. |
| 3 | The next step | Release expected during 2026. Register your interest below to be notified when the diagnostic opens. |

- **Waitlist form section** — section gets `id="waitlist"` for deep-linking from home hero:
  - Section container: `<section id="waitlist">`
  - Section title: `Join the accountancy waitlist`
  - Sub: `Be notified when the accountancy diagnostic opens. We'll also send the first edition of the EIS accountancy positioning paper when it's published.`
  - Embed: Microsoft Forms iframe inside the existing `.embed` component
  - Form fields (Damo configures inside Microsoft Forms):
    - Name (required)
    - Email (required)
    - Firm name (required)
    - Role (required, single-select: Managing Partner / Partner / Director / Other)
    - Headcount band (optional, single-select: Under 5 / 5–10 / 11–25 / 26–50 / 50+)
    - What triggered your interest? (optional, short text)
  - Form URL: **[Microsoft Forms accountancy URL — to be supplied by Damo before push to main]**

---

## 7. Contact Page Hot-Fix (`/contact/index.html`)

The existing page contains live draft text: `"For now, use email booking. We can add a scheduler later (Microsoft Bookings or similar)."`

**Action:** Remove the draft text. Replace with the locked copy below.

- Existing kicker, h1, and primary copy remain unchanged.
- Replace the offending `<p class="sub">` (or `.small`, whichever the draft text occupies) with:

> `If you'd prefer to start with the sector diagnostic, take the Defensible Requisition Blueprint scorecard (for law firms) or register your interest in the accountancy or healthcare scorecards from the relevant sector page.`

---

## 8. Privacy Policy Update (`/privacy-policy/index.html`)

Two changes:

**Change 1, add Microsoft Clarity disclosure.** Append a new section after the existing "Cookies" section (or equivalent):

> **Behavioural analytics, Microsoft Clarity**
>
> This website uses Microsoft Clarity to understand how visitors interact with our pages. Clarity captures anonymised session recordings and heatmaps. Microsoft processes this data as our processor under the terms of the Microsoft Online Services Data Protection Addendum. No personally identifying information is intentionally captured. You can read Microsoft's privacy statement at https://privacy.microsoft.com/en-gb/privacystatement.
>
> Under current UK ICO guidance, Microsoft Clarity used in its default configuration does not require a consent banner because it does not set cookies that identify individuals. We have configured Clarity in its default privacy-preserving mode and do not enable any feature that would change this position.

**Change 2, insert Company No and VAT No, remove HTML comment.** The line `<!-- OPTIONAL: add Company No / VAT No if you want -->` is present in the page source. Remove it and insert the company identifiers:

> **EIS Consulting Ltd**
> Registered in England and Wales. Company number: **08695848**. VAT registration number: **GB 173 8471 82**.

Placement: in the footer section of the privacy policy that identifies the data controller, or in whatever existing "Who we are" section is present. Damo (or Claude Code) places it in the most natural location based on the page's existing structure.

---

## 9. Cross-Cutting Requirements

### 9.1 Microsoft Clarity Integration

**Status:** Project created. Project ID: `wqha1gwbg3`.

**Snippet to inject** (in the `<head>` of every page, immediately before `</head>`):

```html
<script type="text/javascript">
    (function(c,l,a,r,i,t,y){
        c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)};
        t=l.createElement(r);t.async=1;t.src="https://www.clarity.ms/tag/"+i;
        y=l.getElementsByTagName(r)[0];y.parentNode.insertBefore(t,y);
    })(window, document, "clarity", "script", "wqha1gwbg3");
</script>
```

**Pages requiring injection:**

- `/index.html`
- `/legal/index.html`
- `/accountancy/index.html`
- `/healthcare/index.html`
- `/contact/index.html`
- `/privacy-policy/index.html`
- `/terms-of-use/index.html`

**Custom event tagging on hero CTAs (home page):**

The three hero buttons on the home page each fire a distinct Clarity custom event on click. Use the `onclick` pattern below for each. The `if(window.clarity)` guard prevents errors if the Clarity script fails to load.

```html
<a class="btn primary" 
   href="[SCOREAPP_URL]"
   onclick="if(window.clarity)clarity('event','hero_cta_law_scorecard');">
  Take the law diagnostic →
</a>

<a class="btn" 
   href="/healthcare/#waitlist"
   onclick="if(window.clarity)clarity('event','hero_cta_healthcare_waitlist');">
  Join the healthcare waitlist →
</a>

<a class="btn" 
   href="/accountancy/#waitlist"
   onclick="if(window.clarity)clarity('event','hero_cta_accountancy_waitlist');">
  Join the accountancy waitlist →
</a>
```

**Custom event tagging on legal page Prize CTA:**

```html
<a class="btn primary" 
   href="[SCOREAPP_URL]"
   onclick="if(window.clarity)clarity('event','scorecard_cta_click_drb');">
  Take the diagnostic
</a>
```

**The four custom events together provide the conversion diagnostic for the Growth Ceiling (PRISM Rule 6):**

| Event | Signal |
|---|---|
| `hero_cta_law_scorecard` | Home-page visitor self-identifying as law, taking direct action |
| `hero_cta_healthcare_waitlist` | Home-page visitor self-identifying as healthcare, capturing interest |
| `hero_cta_accountancy_waitlist` | Home-page visitor self-identifying as accountancy, capturing interest |
| `scorecard_cta_click_drb` | Legal-page visitor converting after reading the proposition |

The ratio between `hero_cta_law_scorecard` and `scorecard_cta_click_drb` is a useful early signal: if hero-route conversions far outweigh proposition-route conversions, the hero CTA is the primary funnel and the legal page is reference. If the inverse, the proposition page is doing real work.

### 9.2 OG Meta Tag Updates

The current home page references the Azure preview URL in OG meta tags. Replace across all pages.

**Before:**

```html
<meta property="og:url" content="https://witty-cliff-0ea22e003.6.azurestaticapps.net/" />
<meta property="og:image" content="https://witty-cliff-0ea22e003.6.azurestaticapps.net/og.png?v=10" />
```

**After:**

```html
<meta property="og:url" content="https://eisconsulting.co.uk/" />
<meta property="og:image" content="https://eisconsulting.co.uk/og.png?v=11" />
```

(Adjust the URL path per page, e.g. `https://eisconsulting.co.uk/legal/` for the legal page.)

**Note on the cached preview:** Social platforms (LinkedIn, Twitter/X) cache OG metadata. After deployment and DNS cutover, validate previews via LinkedIn Post Inspector and X Card Validator. If a stale Azure preview appears, force re-scrape through those tools.

**Add OG tags to pages that currently lack them:** The audit identified that only the home page carries OG tags. The legal page and the two stub pages should also carry full OG tag sets, each pointing to its own URL with a sensible `og:title` and `og:description` (re-use the `<title>` and `<meta name="description">` content for each page).

### 9.3 Accessibility Fixes

| Issue | Fix |
|---|---|
| No skip-to-content link | Add `<a class="skip-link" href="#main-content">Skip to main content</a>` as the first element inside `<body>` on every page. Style with a new `.skip-link` class that is visually hidden but focusable. |
| No `id` on `<main>` | Add `id="main-content"` to the `<main>` element on every page. |
| Heading hierarchy gap | Resolves naturally with the rebuild. New page structure does not skip from h1 to h3. |
| No `width`/`height` on images | Add explicit `width` and `height` attributes to every `<img>` element. Values: logo nav image `width="155" height="40"`, footer logo `width="132" height="34"`, OG image not applicable. |
| No `loading="lazy"` on non-critical images | Add `loading="lazy"` to footer logo images on every page. Keep nav logo eager (above the fold). |
| Colour contrast on `.muted` and primary button text | Verified during Stage 3 using a contrast checker. If `.muted` (`#b8c6e6` on `#0b1220`) or button text (`#08101d` on gradient endpoint `#7cf0d6`) falls below WCAG AA, raise to the nearest passing value. Document the actual ratio in the Stage 3 closeout note. |

### 9.4 Stage 3 Archive Step

Before any code changes are made on the `main` branch, execute the archive recommendation from the Stage 1 audit:

```bash
git tag -a v0-pre-rebuild -m "Pre-rebuild snapshot: existing 7-page static site, Jan 2026"
git push origin v0-pre-rebuild
```

This is the first action Stage 3 takes. Without it, the current site is not recoverable post-rebuild without commit-hash detective work.

### 9.5 URL Rename and 301 Redirect

**Directory rename:** Rename the `src/general-practice/` directory to `src/healthcare/`. Move `src/general-practice/index.html` to `src/healthcare/index.html` and apply the locked copy from §6.1.

**301 redirect:** Azure Static Web Apps supports redirects via a `staticwebapp.config.json` file at the deployment root. Create or update this file at `src/staticwebapp.config.json` with:

```json
{
  "routes": [
    {
      "route": "/general-practice/",
      "redirect": "/healthcare/",
      "statusCode": 301
    },
    {
      "route": "/general-practice",
      "redirect": "/healthcare/",
      "statusCode": 301
    }
  ]
}
```

Both URL forms (with and without trailing slash) are covered. Damo confirms no inbound links to the legacy URL exist, so this is defensive insurance against bookmarks, draft emails, or LinkedIn posts that may reference the legacy path.

---

## 10. ScoreApp Integration

**Customer task:** EIS Consulting completes the Defensible Requisition Blueprint scorecard build in ScoreApp today. The scorecard structure should align to the five Blueprint principles, with three questions per principle (15 questions total) and an outcome page that shows the firm's position against the 2% AR Rate Floor.

**AICW task (Stage 3):** Embed the ScoreApp URL in **two places** on the EIS site:

1. The **home page hero** primary button ("Take the law diagnostic →")
2. The **legal page Prize section** CTA ("Take the diagnostic")

Both use the same ScoreApp URL. The two paths give visitors a fast route (hero) and a considered route (proposition page first).

**Cross-domain consideration:** The CTA is an external link, not an embed. The visitor leaves the EIS domain when they take the scorecard. ScoreApp captures the lead. ScoreApp's outbound integrations (email notification to Damo, optional CRM sync) are configured inside ScoreApp itself and are out of scope for this brief.

**Pricing:** Per Damo's instruction, pricing is not displayed on the page. The £1,250 (data analysis) / £7,750 (full service) bands are surfaced in discovery only, not on the public surface.

---

## 11. Stage 3 Acceptance Criteria

Stage 3 is complete when the following are all true:

1. The `v0-pre-rebuild` git tag has been created and pushed to origin.
2. The `src/general-practice/` directory has been renamed to `src/healthcare/` and the 301 redirect is operational from `/general-practice/` to `/healthcare/` on the Azure preview URL.
3. All seven pages render correctly on the Azure preview URL with no console errors.
4. All seven pages pass a manual screen-reader navigation test using the skip-to-content link.
5. Microsoft Clarity is recording sessions across all seven pages, visible in the Clarity dashboard at project `wqha1gwbg3` within 24 hours.
6. The home page hero contains three sector-keyed CTAs in the order law, healthcare, accountancy. Each navigates to the correct destination on click. The law button is `.btn.primary`; the healthcare and accountancy buttons are `.btn` (secondary).
7. The home page hero CTAs each fire a distinct Clarity custom event on click (`hero_cta_law_scorecard`, `hero_cta_healthcare_waitlist`, `hero_cta_accountancy_waitlist`), verified through test clicks visible in the dashboard.
8. The healthcare and accountancy hero links deep-link to the `#waitlist` section on the respective stub pages, scrolling the visitor directly to the form.
9. The legal page Prize section CTA navigates to the correct ScoreApp URL on click and fires the `scorecard_cta_click_drb` custom event in Clarity.
10. OG metadata for all seven pages references `eisconsulting.co.uk`, not the Azure preview URL. LinkedIn Post Inspector returns a clean preview when fed the production URLs (validated after DNS cutover).
11. No draft, placeholder, or comment text is visible in any page source or rendered output.
12. No em-dashes appear in any visible page copy. (Verified by searching the deployed pages for the U+2014 character.)
13. The home page Pains section card grid renders as three columns above 980px and one column below.
14. The home page Method section renders as four columns above 980px and one column below.
15. The legal page Mistakes and Method sections render as paired vertical stacks, visually balanced.
16. Both stub pages embed working Microsoft Forms waitlist iframes with sector-appropriate capture fields.
17. The Privacy Policy contains the Microsoft Clarity disclosure section and the EIS Company Number (08695848) and VAT Number (GB 173 8471 82) inserted into the appropriate company-identity section.
18. Damo signs off the preview URL visually before DNS cutover instruction is issued to One.com.

---

## A. Acronym Definition Table

*(See top of document.)*

---

## B. Review Guide

*Per PRISM Project Instructions v1.4, Rule 12, Document Review Protocol v1.1*

### Confidence Map by Section

| Section | Confidence | Rationale |
|---|---|---|
| Acronym Table | High | Standard project acronyms plus DRB, ScoreApp, and VAT additions |
| §1 Engagement Context | High | Directly grounded in PRISM v1.4 |
| §2 Scope | High | Reflects all Damo decisions to date |
| §3 Brand and Design Constraints | High | Tokens and components quoted from Stage 1 audit. House style rule covers em-dash and title separator policy. |
| §4 Home Page Spec | High | Copy locked from Master Canvas v0.10. Hero CTA structure confirmed in v1.2. The `.grid.cols-4` variant is new and requires testing on mobile. |
| §5 Legal Page Spec | High | Copy locked from DRB Canvas v1.0 verbatim where source language was strong |
| §6 Stub Page Specs | Medium-High | Both stubs confirmed as separate waitlists with deep-link anchors |
| §7 Contact Page Hot-Fix | High | Replacement copy is minimal and surgical |
| §8 Privacy Policy Update | High | Microsoft Clarity disclosure language reflects current UK ICO guidance. Company and VAT numbers inserted in v1.2. |
| §9 Cross-Cutting Requirements | High | Technical specifications derived from Stage 1 audit. Clarity snippet and event tagging concrete in v1.2. |
| §10 ScoreApp Integration | High | The cross-domain CTA pattern is straightforward and now applies in two locations (hero + Prize) |
| §11 Acceptance Criteria | High | Testable, measurable. Eighteen criteria covering all sections. |

### Declared Assumptions

1. **The `.grid.cols-4` variant works at the 980px breakpoint.** The existing CSS defines `.grid.cols-3` with a single-column reflow below 980px. The new `.cols-4` variant assumes the same reflow pattern. Stage 3 will test this and document the actual CSS change in the closeout note.
2. **ScoreApp produces a stable, embeddable URL today.** Both the home hero primary button and the legal page Prize CTA require a working ScoreApp URL by the time Stage 3 deploys. If the URL is not ready, deploy with a `mailto:` fallback and update the URLs post-deployment.
3. **The Microsoft Forms iframes on the stub pages will continue to function.** The existing accountancy page already embeds a Microsoft Forms iframe; we assume Microsoft Forms remains available as an M365 surface for lead capture. Each stub now carries its own form with a `#waitlist` anchor.
4. **The `eisconsulting.co.uk` domain is configured at One.com and not in conflict with another tenant.** DNS cutover is Damo's task post-deployment.
5. **The DRB scorecard structure aligns to the five Blueprint principles.** This is the assumed ScoreApp content; the brief recommends it but does not specify the question content.
6. **Em-dash removal applies to website-rendered text only.** Brief documents, internal artefacts, and Claude responses are unaffected.
7. **§6 sector cards on the home page are retained as the alternative considered path.** v1.2 implements this. If Damo decides to remove §6 to tighten the page, this is a v1.3 revision; the change is purely additive to remove §6 (the hero CTAs already cover the conversion paths).
8. **Three hero CTAs on the home page fit cleanly within the existing `.ctas` component on both desktop and mobile.** Existing CSS supports button rows; mobile stacking is the default for narrow viewports.

### Resolved in v1.2

| Item | Resolution |
|---|---|
| Hero CTA position | Three sector-keyed CTAs added. Law (primary, scorecard URL); healthcare and accountancy (secondary, deep-linked waitlist anchors). |
| Awkward prose items #1, #2 (page titles) | Pipe separator (`|`) applied to both home and legal page titles. |
| Awkward prose item #3 (legal hero H1) | Two-sentence form applied: `Reach the 2% AR rate floor. Defend the rest.` |
| Awkward prose items #4, #5, #6 (mid-page copy) | Restructured to two-sentence forms during v1.1; v1.2 confirms no further change needed. |
| Privacy policy company and VAT numbers | Inserted: Company No `08695848`, VAT No `GB 173 8471 82`. |
| Microsoft Clarity snippet | Project ID `wqha1gwbg3` baked into §9.1. Ready for Stage 3. |
| Healthcare URL | Renamed `/general-practice/` → `/healthcare/` with 301 redirect (resolved in v1.1). |

### Open Items at v1.2

None. The brief is ready for Stage 3 implementation.

### Three Priority Review Items

1. **Read §4.3 hero CTAs one more time.** This is the most material change between v1.1 and v1.2. Three buttons on a hero is more aggressive than the original positional intent. Verify on a quick read that the structure feels right before Stage 3 begins. If you decide the §6 sector cards become redundant alongside the hero CTAs, say so and I'll patch to v1.3 by removing §6.

2. **Confirm the ScoreApp URL is live.** This is the only remaining blocker for Stage 3 push to main. The brief specifies two locations where the URL is embedded (home hero, legal Prize). Both can use the same URL.

3. **Confirm the two Microsoft Forms URLs (healthcare waitlist, accountancy waitlist) are ready.** Each stub page embeds its own form. The forms can use Damo's existing M365 Forms surface.

### Estimated Review Time

Fifteen to twenty minutes for a focused review of the v1.2 changes (sections §4.3 hero, §8 with company numbers, §9.1 with the live Clarity snippet, §11 acceptance criteria). Full document review remains twenty-five to thirty-five minutes for someone seeing it fresh.

---

*Document produced under PRISM Project Instructions v1.4. Subject to PRISM Rules 12 (Review Guide) and 13 (Acronym Definition Table). Filed under EIS Consulting Ltd document naming convention.*
