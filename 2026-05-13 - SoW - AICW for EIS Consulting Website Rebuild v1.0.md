# 2026-05-13 - SoW - AICW for EIS Consulting Website Rebuild v1.0

**Version:** 1.0
**Date:** 2026-05-13
**Author:** Damo, Founder, AI CustomWorks Ltd
**Classification:** Internal — Engagement Agreement
**Template:** This document is the v1.0 instance of the AICW Customer Engagement SoW template. Future external customer engagements will inherit this structure.

---

## Version History

| Version | Date | Change |
|---|---|---|
| v1.0 | 2026-05-13 | Initial issue. Defines the engagement between AICW (provider) and EIS Consulting Ltd (customer) for the EIS website rebuild scoped in `2026-05-13 - Brief - EIS Website Rebuild v1.2`. |

---

## Executive Summary

This Statement of Work governs the engagement between AI CustomWorks Ltd ("AICW") and EIS Consulting Ltd ("EIS") for the EIS website rebuild. The scope is defined in `2026-05-13 - Brief - EIS Website Rebuild v1.2`, which is incorporated by reference as Schedule A.

AICW will deliver the rebuild of seven website pages (home, legal, accountancy, healthcare, contact, privacy policy, terms of use) with cross-cutting work covering Microsoft Clarity analytics integration, OG meta tag corrections, accessibility fixes, the URL rename from `/general-practice/` to `/healthcare/` with redirect, and ScoreApp scorecard integration on the legal page. Acceptance criteria are defined in Schedule A §11.

This is a related-party transaction. Both AICW and EIS are wholly owned and directed by Damo. Commercial terms reflect arm's length pricing aligned to EIS's published service tiers. The engagement is structured to be transparent, defensible to HMRC, and reusable as the AICW customer engagement template for future external customer work.

---

## Acronym Definition Table

| Acronym | Definition | Project-Specific Note |
|---|---|---|
| AICW | AI CustomWorks Ltd | Provider on this engagement, UK limited company |
| AR | Avoidable Requisition | HMLR conveyancing metric, see brief |
| DRB | Defensible Requisition Blueprint | EIS proposition for the legal sector |
| EIS | EIS Consulting Ltd | Customer on this engagement, UK limited company |
| GDPR | General Data Protection Regulation | UK data protection law |
| HMRC | His Majesty's Revenue and Customs | UK tax authority |
| ICO | Information Commissioner's Office | UK data protection regulator |
| IP | Intellectual Property | Includes copyright, design rights, trademarks, and confidential information |
| NDA | Non-Disclosure Agreement | Confidentiality commitment, here folded into §8 of this SoW rather than a separate document |
| PRISM | Purpose-led, Roadmapped, Integrated Systems Model | AICW internal operating model |
| SoW | Statement of Work | This document |
| VAT | Value Added Tax | UK indirect tax |

---

## 1. Parties

**Provider:**
AI CustomWorks Ltd
Director: Damian Neilson
Registered in England and Wales
Trading name: AICW

**Customer:**
EIS Consulting Ltd
Director: Damian Neilson
Company number: 08695848
VAT number: GB 173 8471 82
Registered in England and Wales

**Related-party disclosure:** Both entities are owned and directed by the same individual. This SoW exists to:

1. Govern the engagement at arm's length terms,
2. Demonstrate to HMRC that the related-party transaction is conducted on a transfer-pricing-defensible basis, and
3. Provide a reusable template for AICW's future external customer engagements.

A separate accountant review of the commercial terms in §5 is recommended before invoicing to confirm transfer pricing compliance.

---

## 2. Engagement Summary

**Purpose:** EIS requires a public website that publishes the EIS Master Value Canvas v0.10 and the HMLR Defensible Requisition Blueprint v1.0 proposition, capturing qualified leads via a ScoreApp scorecard for the legal sector and waitlist forms for healthcare and accountancy. AICW provides the design, copy preparation, build supervision, and deployment work to deliver this.

**Engagement model:** Single-engagement project work at a defined fixed fee. Not a retainer. Not an ongoing service. Stage 3 completion plus a brief closeout period defines the boundary.

**Engagement start:** 2026-05-13 (effective on signature).

**Engagement end:** On the earlier of (a) Customer's written acceptance of the Stage 3 deliverables per Schedule A §11, or (b) 2026-06-30. If neither occurs, see §9.

---

## 3. Scope

### 3.1 In Scope

The scope is the rebuild work defined in Schedule A (`2026-05-13 - Brief - EIS Website Rebuild v1.2`), specifically:

- Rebuild of seven HTML pages
- Microsoft Clarity analytics integration (project ID `wqha1gwbg3`)
- ScoreApp CTA integration on the legal page hero and Prize section
- Microsoft Forms waitlist integration on healthcare and accountancy stubs
- URL rename from `/general-practice/` to `/healthcare/` with 301 redirect
- OG meta tag corrections
- Accessibility fixes per Schedule A §9.3
- Privacy policy update including Microsoft Clarity disclosure and Company/VAT number insertion
- Stage 3 archive step (git tag) before any code changes
- Production of a Stage 3 closeout note documenting any deviations from this SoW or Schedule A

### 3.2 Out of Scope

Items explicitly outside this engagement, captured for future scoping:

- High-level business process design aligned to each of the DRB method pillars (queued for separate engagement)
- Lead-handling processes for landing-page-to-ScoreApp-to-discovery funnel (queued for separate engagement)
- Sector scorecards for accountancy and healthcare (separate proposition-level canvas work first)
- Additional propositions for the legal page beyond DRB
- Coaching service line page
- Subscription platform page
- Custom domain DNS configuration at One.com (Customer's responsibility)
- ScoreApp scorecard build (Customer's responsibility)
- Microsoft Forms creation for the waitlists (Customer's responsibility)
- Microsoft Clarity property creation (Customer's responsibility, already completed)
- Any work that materially alters the design system inventoried in Schedule A §3

Customer responsibilities — items that must be in place before Stage 3 begins:

1. ScoreApp DRB scorecard live with a stable URL
2. Microsoft Forms waitlist URLs for healthcare and accountancy
3. Microsoft Clarity project active (already completed; project ID `wqha1gwbg3`)
4. GitHub repository accessible to Damo's local Claude Code environment (already in place)

---

## 4. Deliverables

The engagement produces the following deliverables, each linked to acceptance criteria in Schedule A §11.

| # | Deliverable | Format | Acceptance reference |
|---|---|---|---|
| 1 | `v0-pre-rebuild` git tag at the pre-rebuild commit | git tag pushed to GitHub origin | Schedule A §11.1 |
| 2 | Seven rebuilt HTML pages deployed to the Azure Static Web Apps preview URL | Deployed and visible on preview | Schedule A §11.3, §11.6–§11.17 |
| 3 | Microsoft Clarity instrumentation operational on all pages | Sessions visible in project `wqha1gwbg3` dashboard | Schedule A §11.5 |
| 4 | ScoreApp CTA integration with custom-event tracking | Two CTAs (hero and Prize section), both firing distinct Clarity events | Schedule A §11.6–§11.9 |
| 5 | URL rename with 301 redirect | Operational on Azure preview | Schedule A §11.2 |
| 6 | Privacy policy update with Clarity disclosure and company identifiers | Visible in privacy policy page | Schedule A §11.17 |
| 7 | Stage 3 closeout note | Markdown file in the repository documenting any deviations from this SoW or Schedule A, and recording any decisions made during implementation | Filed as `2026-MM-DD - Closeout - EIS Website Rebuild Stage 3 v1.0.md` |
| 8 | Customer sign-off of Azure preview URL | Damo's written confirmation before DNS cutover | Schedule A §11.18 |

DNS cutover via One.com is **not** a deliverable. It is the Customer's responsibility post-acceptance.

---

## 5. Commercial Terms

### 5.1 Fee

**Engagement fee:** £2,500 (two thousand five hundred pounds sterling), exclusive of VAT.

**Rationale for fee setting:** The fee reflects the scope defined in Schedule A and is set at the lower-band level of EIS's own service pricing structure (£1,250 for data analysis through £7,750 for full DRB service). This SoW work — produced fully by AICW for a customer with whom the founder happens to also be the director — sits at the production end of that range, comparable to small-scope-website-build engagements typically priced between £2,000 and £5,000 in the UK market for similar bounded HTML/CSS deliverables with copy preparation and analytics setup.

**Related-party transfer pricing position:** £2,500 represents an arm's length price for the scope. Customer's accountant should confirm before invoicing if the related-party position is to be formally documented for HMRC purposes.

### 5.2 Payment

| Milestone | Trigger | Amount |
|---|---|---|
| Invoice on engagement start | This SoW countersigned | 100% (£2,500 + VAT) |
| Payment terms | 30 days from invoice date | — |

AICW will invoice EIS within five working days of SoW countersignature. Invoice payable by bank transfer in pounds sterling.

### 5.3 Expenses

No expenses are recoverable on this engagement. All software licences (Claude Code, GitHub, Microsoft 365, ScoreApp, Microsoft Clarity, Azure Static Web Apps) are in place and bear no marginal cost to either party.

### 5.4 Out-of-scope work

Any work requested beyond Schedule A is subject to change control per §10 and is not included in the £2,500 fee. Out-of-scope work is quoted separately.

---

## 6. Intellectual Property

### 6.1 Customer-specific work product

The HTML, CSS, copy text, and configuration files specifically produced for the EIS website under this engagement vest in the Customer (EIS) on payment of the engagement fee in full. This is a work-for-hire arrangement for the customer-specific instance of the work.

### 6.2 AICW patterns, templates, and methods

AICW retains all rights in:

- The audit format and structure (template instance: `2026-05-13 - Audit - EIS Website Existing Site Inventory v1.0`)
- The brief format and structure (template instance: `2026-05-13 - Brief - EIS Website Rebuild v1.2`)
- The SoW format and structure (template instance: this document)
- The four-stage engagement model (Audit → Brief → Build → Closeout) and the principles by which it is executed

These are AICW's reusable assets, applied to this engagement, and re-applicable to future customer engagements. The customer receives the specific instance, not the underlying pattern.

### 6.3 Third-party material

Material licensed from third parties (e.g. Microsoft Clarity, ScoreApp, Microsoft Forms) remains subject to the licence terms of the relevant third party. Neither AICW nor EIS grants the other any rights in third-party material beyond what those third-party licences permit.

### 6.4 Source canvas content

The EIS Master Value Canvas v0.10 and HMLR Defensible Requisition Blueprint v1.0 are EIS-owned intellectual property. AICW's role is to translate canvas content into web-published form, not to author the canvas content. Canvas IP remains with EIS.

---

## 7. Data Protection and Security

### 7.1 Roles under UK GDPR

For data captured through the EIS website (Clarity analytics, ScoreApp scorecard submissions, Microsoft Forms waitlist submissions), **EIS is the data controller**. AICW is **not** a data processor under this engagement; AICW does not access, hold, or process personal data captured by the website beyond test data necessarily generated during Stage 3 validation.

If during Stage 3 testing AICW generates any session recordings, scorecard responses, or form submissions, these are test artefacts and should be deleted or excluded from EIS's analytical view of the data.

### 7.2 Data captured by the website

| System | Data controller | Notes |
|---|---|---|
| Microsoft Clarity | EIS | Anonymised session recordings, heatmaps. Processor: Microsoft. |
| ScoreApp | EIS | Lead capture, scorecard responses. Processor: ScoreApp. |
| Microsoft Forms | EIS | Waitlist submissions. Processor: Microsoft. |

EIS's privacy policy (rebuilt under Schedule A §8) discloses each of these to website visitors.

### 7.3 Security baseline

AICW operates within Cyber Essentials baseline practices. Code is committed to GitHub (Microsoft-owned, ISO 27001 certified). No customer data is held on AICW's local development environment beyond test data necessarily generated during Stage 3.

### 7.4 Sub-processors and AI tools

AICW uses Anthropic's Claude (via Claude.ai and Claude Code) to assist with the work. Inputs to Claude during this engagement include the canvas documents, the audit, the brief, and the SoW (this document). These inputs are processed under Anthropic's commercial terms which exclude training on customer data by default. No EIS customer personal data is or will be sent to Claude or any other LLM as part of this engagement.

---

## 8. Confidentiality

Both parties commit to keeping confidential any non-public information shared during this engagement, including but not limited to:

- The canvas documents
- The audit findings
- This SoW
- Any commercial terms, fees, or pricing structures
- Customer lead data captured through the website

Confidentiality obligations survive termination of this engagement for three years from the engagement end date. Both parties remain free to use general skills, knowledge, and methods learned from the engagement provided no confidential information is disclosed.

---

## 9. Term and Termination

### 9.1 Start and end

The engagement starts on 2026-05-13 and ends on the earlier of:

(a) Customer's written acceptance of the Stage 3 deliverables (Schedule A §11.18 sign-off), or
(b) 2026-06-30.

### 9.2 Termination for convenience

Either party may terminate this engagement by giving seven calendar days' written notice. On termination for convenience, AICW invoices for work completed to the point of termination at a pro-rated portion of the £2,500 fee. The pro-ration is calculated against the percentage of Schedule A §11 acceptance criteria completed at the termination date.

### 9.3 Termination for cause

Either party may terminate immediately for material breach by the other party that is not remedied within seven days of written notice. On termination for cause:

- If by Customer (for AICW breach): Customer pays for accepted deliverables only.
- If by AICW (for Customer breach, e.g. non-payment): full fee remains payable on standard terms.

### 9.4 What survives termination

The IP terms in §6, the data protection commitments in §7, the confidentiality obligations in §8, and any unpaid invoice obligations survive termination.

---

## 10. Change Control

The scope is governed by Schedule A (the brief). The brief is versioned (currently v1.2). Material scope changes require a new brief version (v1.3, v1.4, etc.) and may require a corresponding SoW addendum (v1.1, v1.2, etc.) where the change affects fee, timeline, or commercial terms.

The change control flow is:

1. Customer requests a change in writing (email to AICW is sufficient).
2. AICW assesses the change against the current brief and proposes a brief revision plus any SoW addendum.
3. Customer accepts or rejects the proposal in writing.
4. If accepted, the new brief version becomes the operative scope and AICW proceeds.
5. If the change has fee or timeline implications, those are agreed before work proceeds.

Minor clarifications that do not change scope, fee, or timeline do not require a brief revision. The judgement on what is "material" sits with AICW in the first instance, subject to Customer's right to dispute through change control.

---

## 11. Liability

### 11.1 Cap

AICW's total aggregate liability under this engagement is capped at the engagement fee (£2,500), other than for matters that cannot be limited under UK law (death or personal injury caused by negligence, fraud, fraudulent misrepresentation).

### 11.2 Exclusions

Neither party is liable for indirect, consequential, or special loss, including loss of profit, loss of goodwill, or loss of business opportunity, however arising.

### 11.3 No warranty on third-party services

AICW makes no warranty in respect of third-party services integrated into the deliverables (Microsoft Clarity, ScoreApp, Microsoft Forms, Azure Static Web Apps). These are subject to the relevant third-party terms.

---

## 12. Governing Law

This engagement is governed by the laws of England and Wales. Any dispute that cannot be resolved through good-faith discussion is subject to the exclusive jurisdiction of the courts of England and Wales.

---

## 13. Schedules

| Schedule | Document | Notes |
|---|---|---|
| A | `2026-05-13 - Brief - EIS Website Rebuild v1.2` | The operative scope and acceptance criteria. Versioned independently per §10. |
| B | `2026-05-13 - Audit - EIS Website Existing Site Inventory v1.0` | The baseline assessment of the pre-rebuild site. |

Both schedules are incorporated by reference into this SoW.

---

## 14. Signatures

This SoW is executed in counterparts. Each party retains a signed copy.

**For AI CustomWorks Ltd:**

Signature: _______________________
Name: Damian Neilson
Title: Director
Date: __________________________

**For EIS Consulting Ltd:**

Signature: _______________________
Name: Damian Neilson
Title: Director
Date: __________________________

---

## A. Acronym Definition Table

*(See top of document.)*

---

## B. Review Guide

*Per PRISM Project Instructions v1.4, Rule 12, Document Review Protocol v1.1*

### Confidence Map by Section

| Section | Confidence | Rationale |
|---|---|---|
| §1 Parties | High | Both legal entities exist, Damo is the director of both, related-party disclosure is straightforward. |
| §2 Engagement Summary | High | Mirrors Schedule A scope. |
| §3 Scope | High | Direct reference to Schedule A. Customer responsibilities surfaced explicitly. |
| §4 Deliverables | High | Each deliverable maps to a Schedule A §11 acceptance criterion. |
| §5 Commercial Terms | Medium | Fee is set at AICW's best estimate of arm's length pricing for the scope. Subject to accountant review for transfer pricing defensibility. Other commercial terms (payment timing, expenses) are standard for small UK engagements. |
| §6 IP | High | Standard work-for-hire structure with AICW retaining pattern/template rights. This is the v1.0 of the AICW IP position and is reusable. |
| §7 Data Protection | High | Reflects the data flows established in Schedule A. EIS as data controller for all website-captured data is correct. AICW non-processor position is correct because AICW does not access lead data. |
| §8 Confidentiality | High | Standard mutual confidentiality with three-year survival. |
| §9 Term and Termination | High | Cleanly bounded engagement with clear end conditions. Termination for convenience and cause both addressed. |
| §10 Change Control | High | Brief versioning is the operative mechanism; this is consistent with how all PRISM documents are governed. |
| §11 Liability | High | Standard liability cap at fee level. UK law mandatory exclusions respected. |
| §12 Governing Law | High | England and Wales is the only sensible choice given both entities and the work location. |
| §13 Schedules | High | Both schedules exist and are incorporated by reference. |

### Declared Assumptions

1. **The £2,500 fee is defensible as arm's length.** Based on AICW's assessment of UK market rates for small-scope-website-build engagements with copy preparation and analytics setup. Accountant review recommended before invoicing.
2. **Both entities have separate accounting and bank arrangements.** The intra-portfolio invoice is treated as a real transaction with VAT recovery and corporation tax implications on both sides.
3. **VAT applies.** AICW is assumed VAT-registered or will be by the invoice date. If not, the fee is the gross figure.
4. **EIS will provide the ScoreApp URL and Microsoft Forms URLs before Stage 3 push to main.** These are EIS's deliverables to AICW under §3.2 Customer responsibilities.
5. **No external lawyer review is sought before signature.** This is a related-party SoW between two single-director companies with the same beneficial owner. The pragmatic position is signature based on Damo's judgement as director of both. For future external customer engagements, this SoW v1.0 template should be reviewed by a commercial lawyer before reuse.

### Unverified Claims

1. **The arm's length price is £2,500.** Based on AICW's market scan, not validated against three or more comparable engagements with documented pricing. The fee could be defended in the £2,000–£3,500 range; £2,500 sits in the middle.
2. **AICW operates within Cyber Essentials baseline (per §7.3).** Asserted on the basis of PRISM Rule 9 (UK regulatory context is always active). Formal Cyber Essentials certification has not been confirmed during SoW drafting. If AICW is not certified, the language should be softened to "AICW operates in alignment with Cyber Essentials principles" or similar.
3. **No EIS customer personal data is sent to Claude during this engagement (per §7.4).** True as of the SoW drafting. If at any point during Stage 3 lead data does flow through Claude (e.g. for content drafting based on real submissions), §7.4 needs revision.

### Scope Expansions

None. The SoW is bounded by Schedule A.

### Three Priority Review Items

1. **The £2,500 fee.** This is the single most reviewable commercial decision in the document. Verify it reads correctly for the scope. If it feels too low or too high, change before signature. Damo's accountant review is recommended before invoicing.
2. **The Cyber Essentials claim in §7.3.** Confirm or soften. If AICW does not currently hold Cyber Essentials certification, the line should be revised to "AICW operates in alignment with Cyber Essentials principles, with formal certification under assessment." This protects against any later challenge to the assertion.
3. **The IP position in §6.** Specifically §6.2 (AICW retains pattern/template rights). This is a deliberate choice that protects future external customer engagements. If Damo wants to relinquish pattern rights to EIS, §6.2 is rewritten. Strong recommendation: keep §6.2 as drafted. The pattern rights are the asset that makes AICW a real provider rather than just a labour arrangement.

### Estimated Review Time

Twenty minutes for a thorough read. Particular attention to §5 (commercial terms), §6 (IP), and §7 (data protection). Other sections are standard UK SoW boilerplate adapted for this engagement.

---

*Document produced under PRISM Project Instructions v1.4. Subject to PRISM Rules 12 (Review Guide) and 13 (Acronym Definition Table). Filed under EIS Consulting Ltd document naming convention. v1.0 of the AICW Customer Engagement SoW template; future engagements inherit the structure with customer-specific variables substituted.*
