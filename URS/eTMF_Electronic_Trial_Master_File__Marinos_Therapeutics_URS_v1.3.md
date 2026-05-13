---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; expanded 2026-05-12 (T4 uplift to 162 requirements; DIA TMF Reference Model 3.3.1 explicit binding; ICH E6(R3) Step 4 binding; EU CTR 536/2014 Art. 56 + Annex I; CTIS submission packs; FDA BIMO; 21 CFR § 11 sub-section authority map; GDPR Arts. 6/9/32/35)"
seed_corpus_basis:
  - "ISPE GAMP 5 (2nd Edition, 2022) Cat 4 SaaS conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "21 CFR Part 312 (IND) + 21 CFR Part 314 (NDA)"
  - "FDA Guidance Computerized Systems Used in Clinical Investigations (2007)"
  - "FDA Bioresearch Monitoring (BIMO) Program — inspection-readiness expectations"
  - "ICH E6(R3) — Good Clinical Practice (Step 4, adopted 6 January 2025) §§ 4 + 5 + Annex 1 (Investigator + Sponsor + TMF content)"
  - "ICH E8(R1) — General Considerations for Clinical Studies"
  - "EU Clinical Trials Regulation 536/2014 — Art. 56 (archiving), Art. 57 (clinical trial master file), Art. 58 (archiving cadence), Annex I (application dossier)"
  - "EMA Guideline on the content, management and archiving of the clinical trial master file (paper and/or electronic) (EMA/INS/GCP/856758/2018 Rev 2)"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "DIA TMF Reference Model v3.3.1 (CDISC, 2023) — Zones 01-11 + Sections + Artefacts"
  - "ICH E2A (Safety Reporting) — for safety-letter cross-reference"
  - "GDPR (Reg. (EU) 2016/679) Arts. 6, 9 (health data), 32 (security), 35 (DPIA)"
  - "ISO/IEC 27001:2022"
  - "PIC/S PI 041 — Good Practices for Data Management and Integrity"
  - "BfArM (DE); Paul-Ehrlich-Institut (DE); Swissmedic (CH); AGES PharmMed (AT)"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# User Requirements Specification (URS)

## eTMF — Veeva Vault eTMF (24R3) — Electronic Trial Master File

**Document Number:** MRN-URS-ETMF-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Marinos Therapeutics PLC, Clinical Operations, Heraklion, Crete, Greece *(fictional)*
**System Owner:** Director, Trial Master File Operations
**Process Owner:** VP Clinical Operations
**Sponsor Representative:** Per ICH E6(R3) Annex 1 §2 + EU CTR 536/2014 Art. 71 (sponsor accountability)
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS; vendor handles infrastructure; site validates configuration)
**Project Mode:** Configuration project on commercial software product **Veeva Vault eTMF (24R3) — Electronic Trial Master File** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a/b/c/d/e/g/k), .30, .50, .70, .100, .200, .300; 21 CFR Part 312 + 314; FDA *Computerized Systems Used in Clinical Investigations* (2007); FDA BIMO inspection-readiness; ICH E6(R3) (Step 4, 6 January 2025) §§ 4–5 + Annex 1; ICH E8(R1); EU CTR 536/2014 Arts. 56-58 + Annex I; EMA Guideline on TMF content, management and archiving (Rev 2); EU GMP Annex 11 §§ 4, 6, 9, 11; DIA TMF Reference Model v3.3.1; GDPR Arts. 6, 9, 32, 35; ISO/IEC 27001:2022; PIC/S PI 041; BfArM (DE); Paul-Ehrlich-Institut (DE); Swissmedic (CH); AGES PharmMed (AT).

> **Note.** This URS covers the **sponsor-side eTMF** for managing trial-level + country-level + site-level documents per the DIA TMF Reference Model v3.3.1 across the full investigational lifecycle (start-up → conduct → close-out → archive). It is distinct from: (a) the **CTMS** (Dryad Pharma URS — operational trial management), (b) the **EDC** (Marigold Clinical URS — patient data capture), (c) the **RIM** (Nimbus Therapeutics URS — regulatory submissions), and (d) the **investigator-site file** (ISF) maintained by the site itself in paper or eRegulatory tooling.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, TMF Operations) | _____________ | _____________ | _____ |
| Reviewer (Vendor Assurance — Veeva relationship owner) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Privacy Officer — GDPR / DPIA) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs — CTIS / FDA Submissions) | _____________ | _____________ | _____ |
| Reviewer (Head of Clinical Quality + GCP Compliance) | _____________ | _____________ | _____ |
| Approver (VP Clinical Operations) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-08 | (synthetic) | Editorial fixes; vendor version bump to 24R3. |
| 1.2 | 2026-05-12 | (synthetic) | T4 uplift to 162 requirements (Tier T4 per § 2A.13 — mission-critical sponsor TMF system spanning DIA TMFR-3.3.1 indexing, document lifecycle, ISF mirror, e-signatures, completeness/timeliness/quality metrics, RTMF, FDA BIMO + EU CTR + CTIS inspection-readiness, GDPR Arts. 6/9/32/35, sponsor/CRO co-management, legacy migration). DIA TMF Reference Model 3.3.1 binding made explicit; ICH E6(R3) Step 4 (6 January 2025) replaces "E6(R3)"; EU CTR 536/2014 Arts. 56-58 added; § 11 sub-section authority map applied per § 2A.2; risk table expanded to 12 rows. |

## Definitions

| Term | Definition |
|---|---|
| eTMF | Electronic Trial Master File |
| Vault eTMF | Veeva Vault eTMF (Release 24R3) |
| TMFR | DIA TMF Reference Model v3.3.1 (CDISC, 2023) — the industry zone/section/artefact taxonomy |
| Zone | Top-level TMFR grouping (Zones 01-11: Trial Management, Central Trial Documents, Regulatory, IRB/IEC + Other Approvals, Site Management, IP & Trial Supplies, Safety Reporting, Central + Local Testing, Third Parties, Data Management, Statistics) |
| Section | TMFR mid-tier grouping within a Zone (e.g., 04.01 Initial IRB/IEC Approval) |
| Artefact | TMFR leaf-level document class (e.g., 04.01.01 IRB/IEC Composition) |
| EDL | Expected Document List (per-study, per-country, per-site list of TMFR artefacts expected to exist before milestones) |
| RTMF | Real-Time TMF — filing within target service-level windows during trial conduct, not retrospectively at close-out |
| ISF | Investigator Site File — site-held regulatory binder; eTMF mirrors a subset for sponsor oversight |
| BIMO | FDA Bioresearch Monitoring Program — site / sponsor / IRB inspection cadre |
| CTIS | EU Clinical Trials Information System (EU CTR submission portal) |
| EDC | Medidata Rave (separate URS — Marigold Clinical) |
| CTMS | Veeva Vault CTMS (separate URS — Dryad Pharma) |
| RIM | Veeva Vault RIM (separate URS — Nimbus Therapeutics) |
| LMS | Cornerstone OnDemand (separate URS — Vega Pharma) |
| ePRO | Clario eCOA (separate URS — Iolanthe Clinical) |
| 1572 | FDA Form 1572 — Statement of Investigator (US sites) |
| FDF | Financial Disclosure Form (US sites, per 21 CFR Part 54) |
| ICF | Informed Consent Form |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| Completeness | % of EDL artefacts in FILED-FINAL state per per-study EDL |
| Timeliness | Time from event to FILED-FINAL versus the configured per-artefact SLA |
| Quality | Rate of rejected documents at first-pass review |

## 1. Purpose

Define the user requirements for the sponsor-side electronic Trial Master File at Marinos Therapeutics used to assemble, classify, lifecycle, review, sign, archive, and inspect TMF documentation across every interventional clinical study Marinos sponsors or co-sponsors. The system shall support GCP compliance per ICH E6(R3) (Step 4, 6 January 2025), EU CTR 536/2014 archiving obligations (Arts. 56-58), FDA BIMO inspection-readiness, and 21 CFR Part 11 electronic-records / electronic-signature controls.

## 2. Scope

**In scope:**
- Veeva Vault eTMF 24R3 multi-tenant SaaS configured for Marinos Therapeutics tenancy.
- DIA TMF Reference Model v3.3.1 implemented as the metadata schema (Zones 01-11 + Sections + Artefacts).
- Per-study TMF Index, per-country sub-binders, per-site sub-binders, ISF mirror views.
- Document lifecycle (DRAFT → IN-REVIEW → APPROVED → FILED-FINAL → SUPERSEDED), versioning, e-signatures, audit trail per § 11.10(e).
- Completeness / Timeliness / Quality (CTQ) metrics, Inspection-Readiness dashboard, Real-Time TMF (RTMF) operating model.
- Expected Document List (EDL) configuration per study / country / site / milestone.
- Integrations: Okta SAML 2.0 (SSO + MFA); Vault Connect to Vault CTMS (Dryad Pharma — study + site metadata), Vault QualityDocs (controlled procedures + SOPs), Vault RIM (Nimbus Therapeutics — cross-reference of regulatory submissions); EDC build artefacts feed from Medidata Rave (Marigold Clinical); LMS read-and-understood task trigger to Cornerstone (Vega Pharma) for CRA SOP changes; pharmacovigilance cross-reference to Sirius Argus (separate URS) for safety-letter artefacts.
- Inspection workflows: FDA BIMO, EU competent-authority (BfArM / PEI / Swissmedic / AGES) and CTIS-routed inspections, sponsor self-audit, CRO oversight.
- Sponsor / CRO co-management model (per-CRO scoped access, role-based permissions, hand-over workflows).
- Migration from legacy paper TMF + legacy electronic TMF systems for in-flight + historical studies.

**Out of scope:**
- Health-authority regulatory submission build / dispatch (Vault RIM — separate URS).
- Site-side investigator-site files (paper or eRegulatory at sites; eTMF holds the sponsor-side mirror).
- Pharmacovigilance case management (Sirius Argus URS).
- EDC / RTSM / IRT primary data capture (Marigold + separate RTSM URS).
- ePRO / eCOA patient-facing systems (Iolanthe Clinical URS).
- Veeva platform infrastructure (vendor-managed; covered by Veeva validation evidence + SOC 2 + ISO 27001).

## 3. System Description and Intended Use

Vault eTMF is the **system of record for trial-level + country-level + site-level master-file artefacts** across the Marinos Therapeutics clinical portfolio. The platform implements the **DIA TMF Reference Model v3.3.1** as its metadata taxonomy: every document is classified into one of ~250 artefacts within the 11 Zones at upload, and the per-study Expected Document List (EDL) defines which artefacts are mandatory or optional, by country / site / milestone. The system computes Completeness, Timeliness, and Quality (CTQ) metrics in real time, surfaces Inspection-Readiness status per study, and operates a **Real-Time TMF (RTMF)** filing model — documents are filed during trial conduct against configured per-artefact SLAs, not retrospectively at close-out.

The GAMP 5 (2nd Edition, 2022) category is **Category 4 — Configured Product**. Veeva maintains the platform SDLC; Marinos validates the per-tenancy configuration: TMF taxonomy + lifecycle states + role-based security + workflows + EDL templates + integrations + reporting.

Intended use scope:
- Phase I-IV interventional trials (small-molecule + biologic + cell + gene therapies + medical device combination products)
- Multi-region (US / EU / DACH / Japan / RoW) sponsorship
- Sponsor-direct conduct + CRO-conducted trials (full CRO + functional service provider models)
- Long-term retention obligations (≥ 25 years post-trial completion per EU CTR Art. 58 + ICH E6(R3) §5.5; longer per local jurisdiction where applicable)

## 4. User Roles

| Role | Permissions | SoD Constraints |
|---|---|---|
| Document Filer (Sponsor + CRO) | File, classify, link metadata, upload supporting documents | Cannot Review or Approve own filings |
| TMF Reviewer (Quality Reviewer) | Quality-review documents against TMFR + EDL expectations; reject / accept | Cannot file or approve same document |
| TMF Approver (CRA Lead / Country Lead) | Approve documents to FILED-FINAL | Cannot file or review same document |
| Study TMF Owner | Sign off TMF at major milestones (FPI, LPI, LPO, DBL, CSR, Archive) | Cannot bypass Reviewer / Approver |
| Inspection Coordinator | Configure inspection-readiness views; export TMF for inspection; manage inspector access | Cannot approve documents |
| Vault Administrator | Configuration changes under change control; cannot file, review, or approve documents | Strict SoD from operational TMF actions |
| TMF Architect (Configuration Author) | Author TMFR + lifecycle + workflow configuration in DEV / UAT | Cannot promote to PROD; requires Approver SoD |
| CRO Liaison (vendor user) | Scoped CRO access per contract; file + review per delegation | Cannot approve final closeout |
| Sponsor Pharmacovigilance Cross-Reference | Read-only cross-link to safety-letter artefacts in Zone 07 | Read-only |
| Sponsor Regulatory Affairs (RIM cross-reference) | Read-only of regulatory submissions cross-linked from RIM | Read-only |
| Auditor / Inspector | Read-only with time-bounded credentials | Strict read-only |
| Migration Specialist | Upload + reconcile legacy data during migration windows | Time-bounded role; revoked at migration close |

Separation of duties (SoD) is system-enforced: Filer ≠ Reviewer ≠ Approver of the same document; Vault Administrator cannot file or approve documents; Inspection Coordinator cannot approve documents; CRO Liaison cannot final-close out their own scope without sponsor approval.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` direct GxP impact / `R2` indirect / `R3` none), and a verifiable `shall`-clause.

### 5.1 Vendor / Platform Assurance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-01 | H | R1 | Veeva shall be qualified as a critical SaaS vendor with documented evidence on file: SOC 2 Type II, ISO/IEC 27001:2022, HIPAA where applicable, customer-shared Veeva Vault eTMF 24R3 CSV summary; annual re-qualification. |
| URS-VND-02 | H | R1 | Vendor releases shall be impact-assessed within 14 calendar days of release-note publication; configuration-affecting releases shall trigger re-validation per the site change-control SOP. |
| URS-VND-03 | H | R1 | Vendor SDLC evidence (Veeva validation approach, OQ + PQ deliverables, change-control logs) shall be reviewed annually and stored in a vendor-assurance dossier. |
| URS-VND-04 | M | R2 | Vendor sub-processor list (per GDPR Art. 28(2)) shall be reviewed quarterly; new sub-processors trigger DPIA review per § 5.13. |
| URS-VND-05 | H | R1 | Vendor SLA shall be evidenced quarterly via SLA-report review; SLA breaches shall be logged in the vendor-assurance dossier and tracked through the site eQMS. |

### 5.2 DIA TMF Reference Model 3.3.1 Adherence (Zones 01-11)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TMFR-01 | H | R1 | The eTMF metadata schema shall implement the DIA TMF Reference Model v3.3.1 Zones 01-11 verbatim (Trial Management, Central Trial Documents, Regulatory, IRB/IEC + Other Approvals, Site Management, IP & Trial Supplies, Safety Reporting, Central + Local Testing, Third Parties, Data Management, Statistics). |
| URS-TMFR-02 | H | R1 | All TMFR v3.3.1 Sections and Artefacts shall be configured per the published taxonomy; deviations from the taxonomy shall be documented in the per-study configuration spec with rationale. |
| URS-TMFR-03 | H | R1 | When DIA / CDISC publishes a new TMFR version, the impact-assessment shall be completed within 60 days; migration to a new TMFR version shall preserve historical zone / section / artefact assignments for already-FILED-FINAL documents. |
| URS-TMFR-04 | H | R1 | TMFR sub-artefacts (v3.3.1 sub-artefact list) shall be available for selection where the taxonomy distinguishes them. |
| URS-TMFR-05 | M | R2 | Per-study TMF Index shall be derivable from the master TMFR taxonomy with study-specific filters (Phase, indication, regions, IMP class). |
| URS-TMFR-06 | H | R1 | The eTMF shall enforce that every filed document is classified to exactly one TMFR Zone + Section + Artefact tuple at FILED-FINAL state. |

### 5.3 Document Lifecycle and Versioning

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DOC-01 | H | R1 | Document lifecycle shall be DRAFT → IN-REVIEW → APPROVED → FILED-FINAL → SUPERSEDED → ARCHIVED; only FILED-FINAL and ARCHIVED states count toward completeness metrics. |
| URS-DOC-02 | H | R1 | Lifecycle transitions shall require role-restricted electronic signatures with SoD enforced at the transition (per § 5.7 and § 11.50 / § 11.70). |
| URS-DOC-03 | H | R1 | FILED-FINAL documents shall be immutable; corrections shall create a new revision in a new DRAFT state, and the prior revision shall enter SUPERSEDED with reason-for-change captured. |
| URS-DOC-04 | H | R1 | Document version numbering shall be monotonic per artefact instance; gaps or duplicates shall be blocked by the system. |
| URS-DOC-05 | M | R2 | Document renditions (PDF/A-3 for archive, native format for editing) shall be maintained; PDF/A-3 shall be generated automatically on FILED-FINAL transition. |
| URS-DOC-06 | H | R1 | Documents shall carry classification metadata: Zone, Section, Artefact, Sub-artefact, Country, Site, Study, Milestone, Document date, Effective date. |
| URS-DOC-07 | H | R1 | Reason-for-change shall be captured on every revision after first FILED-FINAL; reason-codes shall align with site SOP categories (Editorial / Substantive / Regulatory). |
| URS-DOC-08 | M | R2 | Bulk-classification operations shall be permitted only via authenticated API or batch tool, with full audit trail per item; manual bulk re-classification through the UI shall be limited to ≤ 50 items per action. |

### 5.4 Document Type Library and Per-Study Expected Document List (EDL)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-EDL-01 | H | R1 | The system shall maintain a master Document Type Library aligned with TMFR v3.3.1, configurable for company-specific extensions; extensions shall be approved by Director TMF Operations + Head of GCP Compliance. |
| URS-EDL-02 | H | R1 | Per-study EDLs shall be configurable from the master library + study-specific add-ons (e.g., protocol-amendment-driven artefacts, country-mandatory artefacts). |
| URS-EDL-03 | H | R1 | Per-country EDL overlays shall be configurable (e.g., BfArM-mandated documents for DE, PEI for DE biologicals, Swissmedic for CH, AGES for AT, FDA for US, CTIS-routed for EU). |
| URS-EDL-04 | H | R1 | Per-site EDL overlays shall be configurable (site initiation, site activation, site closure artefact sets per site type). |
| URS-EDL-05 | H | R1 | Per-milestone EDL filters shall surface artefacts expected at milestones: FPI (First Patient In), LPI (Last Patient In), LPO (Last Patient Out), DBL (Database Lock), CSR (Clinical Study Report), Archive. |
| URS-EDL-06 | M | R2 | EDL changes mid-study shall be impact-assessed; retrospective EDL changes shall be approved by Study TMF Owner + Head of GCP Compliance. |

### 5.5 Per-Country and Per-Site Binders + Investigator Site File (ISF) Mirror

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BIND-01 | H | R1 | The eTMF shall expose per-country binders that aggregate trial-level documents shared across that country's sites plus country-specific regulatory + IRB/IEC + competent-authority filings. |
| URS-BIND-02 | H | R1 | The eTMF shall expose per-site binders that aggregate the site-specific subset of the TMF (Form 1572, FDF, CVs, site-IRB/IEC approvals, site-ICF version log, delegation log, monitoring visit reports). |
| URS-BIND-03 | H | R1 | The eTMF shall provide an **Investigator Site File (ISF) mirror view** showing the sponsor-side records that mirror the site-held ISF (Form 1572, IRB/IEC approvals, ICF versions in use, delegation logs, training records, screening + enrolment logs). |
| URS-BIND-04 | H | R1 | ISF mirror discrepancy reports (sponsor-side vs site-acknowledged) shall be generated per monitoring visit. |
| URS-BIND-05 | M | R2 | Country / site binder views shall be exportable as inspection-ready PDF/A-3 packages within 4 business hours of an inspection-readiness request. |

### 5.6 Completeness, Timeliness, Quality (CTQ) + Real-Time TMF (RTMF)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CTQ-01 | H | R1 | The **Completeness metric** shall be calculated as the percentage of EDL artefacts in FILED-FINAL state per per-study EDL, broken out per country + per site. |
| URS-CTQ-02 | H | R1 | The **Timeliness metric** shall measure time-from-event-to-FILED-FINAL against configured per-artefact SLAs (e.g., safety letter ≤ 5 business days; site-initiation pack ≤ 10 business days; protocol amendment ≤ 15 business days). |
| URS-CTQ-03 | H | R1 | The **Quality metric** shall measure first-pass review-rejection rate, surfacing per-filer + per-CRO + per-country quality trends. |
| URS-CTQ-04 | H | R1 | A study shall not transition to "Inspection Ready" status until Completeness ≥ 95% for required artefacts AND Timeliness 95th-percentile within configured SLA AND Quality first-pass-acceptance ≥ 90%. |
| URS-CTQ-05 | H | R1 | **RTMF operating model:** documents shall be FILED-FINAL within their configured SLA windows during trial conduct; the system shall surface RTMF dashboard with overdue artefacts highlighted. |
| URS-CTQ-06 | M | R2 | RTMF feed-delay (events recorded in source systems vs filed in eTMF) shall be alerted when > 24 hours for safety-critical artefacts and > 5 business days for standard artefacts. |
| URS-CTQ-07 | H | R1 | TMF Health Metrics report shall be produced weekly during conduct + at every milestone; signed off by Study TMF Owner. |
| URS-CTQ-08 | M | R2 | Forecasted Completeness at upcoming milestones shall be projected based on current filing velocity; risk flags shall be raised when projected miss > 15% of EDL. |

### 5.7 Electronic Signatures and 21 CFR Part 11 Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a), procedural and system controls shall protect the validity of electronic records throughout the retention period; the operating SOP shall be referenced from the system documentation. |
| URS-PART11-02 | H | R1 | Per § 11.10(b), the system shall generate accurate and complete copies of records in human-readable PDF/A-3 + machine-readable XML / JSON for inspection. |
| URS-PART11-03 | H | R1 | Per § 11.10(c), records shall be protected throughout the EU CTR Art. 58 retention (≥ 25 years post-trial completion); cryptographic integrity checks shall be verifiable on retrieval. |
| URS-PART11-04 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via Okta SAML 2.0 + MFA; service accounts shall use mTLS only. |
| URS-PART11-05 | H | R1 | Per § 11.10(e), an operational audit trail shall capture user, action, timestamp, prior value, new value, reason-for-change for filing, classification, lifecycle, signatures, configuration changes. |
| URS-PART11-06 | H | R1 | Per § 11.10(g), authority checks shall enforce role-based permissions; users acting outside their authority shall be blocked at API and UI. |
| URS-PART11-07 | H | R1 | Per § 11.10(k), system operation manuals shall be maintained under change control; manual updates shall trigger LMS read-and-understood tasks for affected roles. |
| URS-PART11-08 | H | R1 | Per § 11.30, vendor-internet-exposed components (e.g., inspector portal) shall apply additional controls: short-lived tokens, IP allow-listing where contractual, encrypted channels (TLS 1.3). |
| URS-PART11-09 | H | R1 | Per § 11.50, electronic signatures applied at lifecycle transitions (Form 1572 sign-off, FDF, ICF approval, study TMF milestone sign-off) shall include signer's printed name, date and time of signing, and meaning of signature; manifestation shall be readable in PDF/A-3 export. |
| URS-PART11-10 | H | R1 | Per § 11.70, electronic signatures shall be cryptographically linked to the signed record (HMAC-SHA256 over record-hash + signer-id + timestamp); tampered records shall be flagged on read. |
| URS-PART11-11 | H | R1 | Per § 11.100, electronic-signature identifiers shall be unique to one individual; reuse / reassignment shall be blocked at provisioning via Okta uniqueness constraint. |
| URS-PART11-12 | H | R1 | Per § 11.200, identity-based signatures shall require re-authentication at the moment of signing for critical artefacts (Form 1572, FDF, ICF approval, TMF milestone sign-off); cached credentials shall be rejected. |
| URS-PART11-13 | H | R1 | Per § 11.300, password / credential controls shall align with site InfoSec policy: MFA mandatory for all users, lockout after 5 failed attempts in 15 minutes, password complexity per ISO 27001 baseline. |
| URS-SOD-01 | H | R1 | Separation of Duties shall be system-enforced: Filer ≠ Reviewer ≠ Approver of the same document. |
| URS-SOD-02 | H | R1 | Vault Administrator role shall not permit filing, reviewing, or approving documents. |
| URS-SOD-03 | H | R1 | CRO Liaison shall not approve final-closeout of their own scope without sponsor co-signature. |

### 5.8 eSignature Workflows — Form 1572, FDF, ICF, IRB/IEC, Protocol Amendments

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ESW-01 | H | R1 | The system shall provide a configurable e-signature workflow for FDA Form 1572 (Statement of Investigator, US sites) capturing investigator + sub-investigator signatures + dates; signatures shall meet § 11.50 / § 11.70 / § 11.200. |
| URS-ESW-02 | H | R1 | The system shall provide a Financial Disclosure Form (FDF) workflow per 21 CFR Part 54 with investigator + sub-investigator signatures + annual re-confirmation reminders. |
| URS-ESW-03 | H | R1 | Informed Consent Form (ICF) versioning workflow shall track per-language + per-country variants; only the IRB/IEC-approved + sponsor-released ICF version shall be marked CURRENT for any given site / date range. |
| URS-ESW-04 | H | R1 | IRB/IEC approval letters shall be filed in Zone 04 with expiry-tracking (annual continuing-review reminders, lapse blocks). |
| URS-ESW-05 | H | R1 | Protocol amendments shall trigger downstream EDL refresh + per-country impact assessment + LMS read-and-understood tasks for affected roles. |

### 5.9 Quality Review and Completeness Checking

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-QC-01 | H | R1 | The system shall provide a Quality Review queue per artefact type, filterable by country, site, CRO, filer. |
| URS-QC-02 | H | R1 | Quality Review checks per artefact shall include configurable rules (signature presence, date validity, country-flag consistency, IRB/IEC version match against current). |
| URS-QC-03 | H | R1 | Completeness-check rules shall be evaluated against the per-study EDL with per-artefact gating logic; false-positive / false-negative completeness verdicts shall be auditable. |
| URS-QC-04 | M | R2 | Quality Review reject codes shall map to a controlled vocabulary (Editorial / Substantive / Wrong Classification / Wrong Country / Missing Signature / Other-with-reason). |
| URS-QC-05 | M | R2 | A periodic Quality Review calibration session shall be held quarterly; inter-reviewer agreement shall be tracked. |

### 5.10 TMF Health Metrics and Inspection-Readiness

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INSP-01 | H | R1 | An Inspection-Readiness dashboard shall surface per-study Completeness + Timeliness + Quality + last-review-date + open-deviations. |
| URS-INSP-02 | H | R1 | Inspection-Readiness export shall produce a regulator-ready package (PDF/A-3 + machine-readable index + classification matrix) within 4 business hours of request. |
| URS-INSP-03 | H | R1 | A read-only inspector workspace shall be configurable with time-bounded credentials (default 30 days, extensible), full audit trail of inspector activity, and watermark on exported documents. |
| URS-INSP-04 | H | R1 | The dashboard shall flag overdue artefacts, expiring IRB/IEC approvals (< 30 days), expiring ICFs, expiring investigator credentials (CVs, GCP training, medical licenses). |
| URS-INSP-05 | H | R1 | FDA BIMO inspection-readiness shall include site selection rationale, monitoring evidence (CRA visit reports), deviation logs, source-data-verification (SDV) evidence linkage to EDC. |
| URS-INSP-06 | H | R1 | EU competent-authority inspection (BfArM / PEI / Swissmedic / AGES) readiness shall include CTIS-routed submission references, EU CTR Art. 56-58 archive provenance, EudraVigilance cross-references for safety. |

### 5.11 CTIS Submission Pack Support

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CTIS-01 | H | R1 | The system shall produce CTIS-compatible submission packs for EU CTR Art. 25 applications + Art. 81 transparency publication; output shall align with current CTIS submission specification + EMA technical standards. |
| URS-CTIS-02 | H | R1 | CTIS submission pack content shall be assembled from Zone 01-04 artefacts (protocol, IB, IMPD, application form, GMP statements, IRB/IEC approvals); missing required artefacts shall block pack assembly. |
| URS-CTIS-03 | M | R2 | CTIS pack version history shall be retained; resubmissions / amendments shall be tracked through Vault RIM (Nimbus Therapeutics) with cross-link. |

### 5.12 Audit Trail / ALCOA+ / Data Integrity

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | A time-stamped, secure operational audit trail shall capture every filing, classification, lifecycle transition, signature, configuration change, role assignment, EDL change. |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only at the platform level; tenant administrators shall not have UPDATE / DELETE on audit records. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be performed monthly by the Director TMF Operations + sampled per-study at milestones. |
| URS-AUD-04 | H | R1 | Audit-trail retention shall be ≥ 25 years post-trial completion per EU CTR Art. 58; longer per jurisdiction where required (e.g., FDA 21 CFR § 312.62 retention). |
| URS-AUD-05 | H | R1 | Audit-trail exports for inspection shall be cryptographically signed by the platform; signature shall be verifiable independently of the platform. |
| URS-DI-01 | H | R1 | **Attributable:** every filing + edit + signature shall carry a named user-id or service-account-id; anonymous or shared accounts shall be prohibited. |
| URS-DI-02 | H | R1 | **Legible:** records shall be exportable as human-readable PDF/A-3 + machine-readable XML / JSON. |
| URS-DI-03 | H | R1 | **Contemporaneous:** server-side NTP-synced timestamps shall be authoritative; retroactive filings shall be flagged with delay reason. |
| URS-DI-04 | H | R1 | **Original:** raw uploads shall be preserved unaltered; derivative renditions (PDF/A-3, OCR text) shall reference but not overwrite the original. |
| URS-DI-05 | H | R1 | **Accurate:** completeness + timeliness + quality calculations shall be deterministic and validated under OQ. |
| URS-DI-06 | M | R2 | **Complete / Consistent / Enduring / Available:** records shall meet ALCOA+ retention obligations (≥ 25 years per EU CTR Art. 58 + ICH E6(R3) §5.5); retrievable within 1 business day for routine, 4 hours for inspection. |

### 5.13 Privacy — GDPR + HIPAA

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PRV-01 | H | R1 | Per **GDPR Art. 6**, lawful basis for processing TMF personal data (investigator / staff / patient pseudonymised data referenced in TMF artefacts) shall be documented per study + per region. |
| URS-PRV-02 | H | R1 | Per **GDPR Art. 9** (special-category health data), patient data in TMF artefacts shall be pseudonymised; only investigator + staff identifying data is permitted as identifiable. |
| URS-PRV-03 | H | R1 | Per **GDPR Art. 32**, encryption at rest (AES-256) and in transit (TLS 1.3) shall be enforced; vendor evidence shall be on file. |
| URS-PRV-04 | H | R1 | Per **GDPR Art. 35**, a Data Protection Impact Assessment shall be on file per study before patient enrolment in EU sites; the DPIA shall be referenced from the per-study TMF master record. |
| URS-PRV-05 | H | R1 | HIPAA Business Associate Agreement (BAA) with Veeva shall be on file for US trials processing PHI. |
| URS-PRV-06 | M | R2 | Cross-border transfer routes (EU patient data to US sponsor) shall be documented per study via SCCs + supplementary measures; routes shall be reviewed annually. |

### 5.14 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-CTMS-01 | H | R1 | Study + site + investigator metadata shall sync bidirectionally from Vault CTMS (Dryad Pharma) via Vault Connect; conflict-resolution shall favour CTMS as system-of-record for operational metadata. |
| URS-INT-EDC-01 | M | R2 | Study-build artefacts (eCRF library, edit-check spec, blank CRF, CCG) shall be auto-filed from Medidata Rave (Marigold Clinical) at protocol-amendment + database-lock milestones. |
| URS-INT-RIM-01 | M | R2 | Regulatory submission references shall be cross-linked from Vault RIM (Nimbus Therapeutics) via Vault Connect; eCTD sequence IDs shall be visible from cross-reference. |
| URS-INT-EDMS-01 | H | R1 | Controlled procedures + SOPs shall be cross-referenced from Vault QualityDocs (Vellis Pharma) via Vault Connect URN. |
| URS-INT-LMS-01 | H | R1 | CRA / monitor SOP changes (effective in QualityDocs) shall trigger read-and-understood tasks in Cornerstone (Vega Pharma) for affected roles. |
| URS-INT-PV-01 | M | R2 | Safety-letter cross-references shall be visible from Sirius Argus (separate URS); Zone 07 artefacts shall cross-link to Argus case IDs. |
| URS-INT-EPRO-01 | L | R3 | ePRO study-build documentation from Iolanthe Clinical shall be auto-deposited to Zone 04 + Zone 08 on study-build approval. |
| URS-INT-SSO-01 | H | R1 | User authentication shall be via Okta SAML 2.0 + MFA; SCIM 2.0 provisioning from the identity authority. |
| URS-INT-API-01 | H | R1 | Vault Connect APIs shall be authenticated via OAuth 2.0 client-credentials with short-lived tokens; service-account changes shall require Change Advisory Board approval. |

### 5.15 Performance, Availability, Backup

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | Document open / list response shall be ≤ 3 s at the 95th percentile under nominal load (10,000 concurrent sessions, 250 active studies). |
| URS-PERF-02 | M | R2 | Inspection-readiness export of a 100k-document study shall complete in ≤ 4 hours. |
| URS-PERF-03 | M | R2 | EDL re-evaluation across 250 active studies shall complete in ≤ 30 minutes per scheduled batch. |
| URS-AV-01 | H | R1 | Platform availability shall meet Veeva SLA: ≥ 99.5% normal, ≥ 99.9% during sponsor-critical windows (DBL, milestone sign-off, inspection); planned-maintenance windows announced ≥ 14 days in advance. |
| URS-BAK-01 | H | R1 | Vendor-managed backup with daily integrity verification; site shall verify Veeva-published RPO ≤ 4 h, RTO ≤ 24 h via annual vendor-assurance review. |
| URS-BAK-02 | H | R1 | Site shall maintain a tenant-data export (vault dump) with ≥ 25-year cold-storage retention; restoration drill shall be performed annually. |
| URS-BAK-03 | H | R1 | DR-site failover shall be tested annually by Veeva; site shall review the DR test report. |

### 5.16 Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | All data in transit shall use TLS 1.3; data at rest AES-256. |
| URS-SEC-02 | H | R1 | Per-study + per-country access controls shall be configurable; CRO access shall be scoped per contract. |
| URS-SEC-03 | H | R1 | Vendor SOC 2 Type II + ISO/IEC 27001:2022 evidence shall be reviewed annually; gaps shall be escalated under change control. |
| URS-SEC-04 | M | R2 | Penetration testing of sponsor + inspector-facing endpoints shall be performed annually; high/critical findings shall be remediated within 30 days. |
| URS-SEC-05 | H | R1 | Inspector-portal credentials shall be time-bounded with default validity 30 days; credentials shall be revocable on demand. |

### 5.17 Sponsor + CRO Co-Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CRO-01 | H | R1 | The system shall support sponsor-CRO co-management with per-CRO scoped access, per-protocol delegation, sponsor-oversight workflows. |
| URS-CRO-02 | H | R1 | CRO transitions (CRO change-over mid-study) shall preserve filing history + audit trail; hand-over workflows shall capture sponsor sign-off. |
| URS-CRO-03 | M | R2 | CRO quality dashboards (per-CRO Completeness + Timeliness + Quality) shall be available to sponsor oversight. |
| URS-CRO-04 | M | R2 | CRO contracted scope shall be documented per protocol and reflected in role-permissions; out-of-scope CRO actions shall be blocked. |

### 5.18 Legacy Migration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MIG-01 | H | R1 | Legacy paper-TMF + legacy-electronic-TMF migration shall preserve original document content, applied signatures, original metadata, and reason-for-change history; migration shall be audit-trailed. |
| URS-MIG-02 | H | R1 | Migration validation shall produce a per-study migration verification report with sampling-based document-content equivalence + metadata-completeness checks; report shall be approved by Director TMF Operations + Head of QA. |
| URS-MIG-03 | M | R2 | Migration-specialist role shall be time-bounded to the migration window; permissions revoked at migration close. |
| URS-MIG-04 | M | R2 | Migration discrepancies shall be tracked through the site eQMS as deviations until resolved. |

### 5.19 Document Expiry, Obsolescence, and Effective-Date Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-EXP-01 | H | R1 | The system shall track document expiry / continuing-review dates for IRB/IEC approvals, ICFs, investigator licenses, GCP training certificates, IB versions, IMPD versions. |
| URS-EXP-02 | H | R1 | Documents within 30 calendar days of expiry shall be flagged on the Inspection-Readiness dashboard; expired documents shall block dependent workflows (e.g., site activation if site IRB/IEC expired). |
| URS-EXP-03 | H | R1 | Effective-date logic shall ensure only the currently-effective ICF version is in use per site; superseded ICFs shall be visible in version history but not selectable for new consents. |
| URS-EXP-04 | M | R2 | Obsolescence workflow shall move SUPERSEDED documents from active TMF views to historical views while preserving retrievability. |

### 5.20 Multi-language and Per-Country Variant Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LANG-01 | H | R1 | The system shall support multi-language document storage with language-locale metadata (e.g., de-DE, de-AT, de-CH, fr-FR, en-US) per document. |
| URS-LANG-02 | H | R1 | Per-country ICF + patient-information-sheet variants shall be tracked as linked sibling artefacts under a common parent; cross-variant linkage shall be preserved through revisions. |
| URS-LANG-03 | M | R2 | Translation provenance (translator + back-translator + certification) shall be filed alongside translated artefacts where regulator requires (e.g., BfArM, AGES). |
| URS-LANG-04 | M | R2 | Per-country submission variants (BfArM cover letter vs Swissmedic cover letter) shall be selectable for inspection-readiness exports by country. |

### 5.21 Investigator + Site Closeout

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CLS-01 | H | R1 | Site closeout workflow shall enforce an EDL of close-out artefacts (final monitoring visit report, drug accountability log, sample disposition, site-archive certification, IP destruction certificate). |
| URS-CLS-02 | H | R1 | Investigator closeout shall capture investigator + sponsor sign-off; signatures meet § 11.50 / § 11.70. |
| URS-CLS-03 | H | R1 | Study-archive transition shall freeze the TMF index, generate a hash-pinned archive manifest, and produce a long-term-retention package. |
| URS-CLS-04 | M | R2 | Sponsor-archive package shall be exportable in PDF/A-3 + machine-readable index for long-term cold storage; integrity checks shall be runnable annually. |

### 5.22 Inspector Portal (External Read-Only Workspace)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INSP-PORTAL-01 | H | R1 | The inspector portal shall provide read-only access to the configured inspection scope with watermarked downloads and time-bounded credentials (default 30 days). |
| URS-INSP-PORTAL-02 | H | R1 | Inspector activity (logins, document opens, exports) shall be audit-trailed with the same § 11.10(e) controls as internal users. |
| URS-INSP-PORTAL-03 | M | R2 | Inspector portal traffic shall be tagged and reportable separately from internal traffic for security-monitoring. |

### 5.23 Reporting and Search

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RPT-01 | M | R2 | Full-text search across TMF documents shall be available to authorised users; search shall respect access-control scopes. |
| URS-RPT-02 | M | R2 | Saved-search definitions shall be shareable per role; saved-search configuration shall be audit-trailed. |
| URS-RPT-03 | M | R2 | Standard report library shall include: TMF Health Metrics, Country Completeness, Site Completeness, CRO Quality, Overdue Artefacts, Expiring Documents, Audit-Trail Review Report. |
| URS-RPT-04 | L | R3 | Ad-hoc report builder shall be available to Study TMF Owner + Inspection Coordinator roles. |
| URS-RPT-05 | M | R2 | Per-Zone (TMFR 01-11) Completeness sub-reports shall be drillable from the TMF Health Metrics report; deviations from EDL shall be listed per Zone. |
| URS-RPT-06 | L | R3 | Report-rendering performance shall complete standard reports (TMF Health Metrics across 250 studies) in ≤ 5 minutes. |

### 5.24 Notifications and Alerts

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-NOT-01 | M | R2 | The system shall send role-targeted email + in-app notifications for: assigned reviews, expiring documents, RTMF SLA-breach, EDL gap alerts, audit-trail review reminders. |
| URS-NOT-02 | M | R2 | Notification cadence + thresholds shall be configurable per role + per study; configuration changes audit-trailed. |
| URS-NOT-03 | L | R3 | Email-bounce + delivery-failure handling shall escalate to user-administrator after 3 consecutive failures. |
| URS-NOT-04 | M | R2 | Inspection-imminent notifications shall trigger an enriched dashboard with priority-overdue artefacts at the top. |

### 5.25 Configuration Management and Change Control

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CCM-01 | H | R1 | Configuration changes shall flow through DEV → UAT → PROD with SoD-enforced approvals; PROD promotion shall require change-record reference. |
| URS-CCM-02 | H | R1 | Configuration baselines shall be versioned + exportable; configuration drift between environments shall be detectable via baseline-diff reports. |
| URS-CCM-03 | M | R2 | Emergency-change configuration paths shall require post-implementation review within 5 business days. |
| URS-CCM-04 | M | R2 | Vendor-driven configuration changes (e.g., release 24R3 → 24R4) shall be impact-assessed against the per-tenancy CS within 14 days. |

### 5.26 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Role-specific eTMF training shall be completed in Cornerstone (Vega Pharma) before any user receives production access; ICH E6(R3) GCP training shall be current for filers + reviewers + approvers. |
| URS-TRN-02 | M | R2 | Annual refresher training shall cover ICH E6(R3) updates, TMFR taxonomy changes, vendor release-note impact, BIMO + CTIS inspection-readiness practice. |
| URS-PR-01 | H | R1 | Annual Periodic Review shall cover TMFR configuration currency, CTQ trends, vendor-assurance status, audit-trail review evidence, DPIA currency, training currency, integration health, security posture; signed by Director TMF Operations + Head of GCP Compliance + Head of QA + VP Clinical Operations. |

### 5.27 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is SAML 2.0 via Entra ID with SCIM lifecycle provisioning; conditional-access policy `Clinical-Sensitive Conditional Access (FIDO2 phishing-resistant MFA + sponsor-tenant isolation)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the metadata DB plus object-replica for TMF binaries; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 25 y per ICH E6(R3) per the consuming-record schedule. |

### 5.28 Cross-System Integration — Helios audit-trail handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HEL-01 | H | R1 | eTMF shall publish audit-trail events (TMF artefact lifecycle, completeness milestone, and freeze / lock events) to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract (JSON Lines, schema-registry pinned, Kafka topic `helios.ingest.marinos.etmf.v1`) within 5 minutes of event capture; 21 CFR § 11.10(e) audit-trail completeness shall be preserved end-to-end so that no event class is lost at the boundary. |
| URS-XINT-HEL-02 | H | R1 | Pre-handover audit-trail retention on the eTMF side shall be ≥ 25 y regardless of Helios availability; once Helios acknowledges ingest (per-message ack with idempotency key), Helios is the system-of-record for review and the eTMF local copy serves as the durability backstop until the local retention floor expires. |

### 5.29 Cross-System Integration — EDMS handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-EDMS-01 | H | R1 | Clinical SOPs, protocols, and informed-consent templates referenced from the eTMF shall be retrieved from the EDMS (`VLP-URS-EDMS-001`) via the EDMS read API with read-only pinning to the artefact's EFFECTIVE version at the time of retrieval; the eTMF artefact lifecycle shall track the EDMS version pin and shall raise a TMF-completeness flag when the linked EDMS document is superseded. |

### 5.30 Cross-System Integration — LMS competence handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-LMS-01 | H | R1 | eTMF role assignments (Sponsor user, CRO user, Investigator-Site user) shall include an LMS-competence check (curriculum `ETMF-<role>-v1.x`); non-current users shall be auto-removed from TMF access on lapse + 30 d grace; lapse evidence retained in the TMF system audit trail. |

## 6. Acceptance Criteria

1. **Configuration Specification (CS)** approved — TMF taxonomy, lifecycle, workflows, EDL templates, role permissions, integrations.
2. **Risk Assessment (RA)** approved per ICH Q9(R1) — `MRN-RA-ETMF-001` (synthetic).
3. **Installation Qualification (IQ)** — vendor-shared IQ evidence reviewed; tenancy provisioned per CS.
4. **Operational Qualification (OQ)** — lifecycle, signatures, EDL, completeness/timeliness/quality calculations, audit trail, integrations validated.
5. **Performance Qualification (PQ)** — representative end-to-end study lifecycle (filing → review → final → CTQ at milestone → inspection-readiness export → migration); ≥ 1 EU site + ≥ 1 US site + ≥ 1 DACH site.
6. **Validation Summary Report (VSR)** approved by VP Clinical Operations + Head of GCP Compliance + Head of QA + Privacy Officer.
7. **Requirements Traceability Matrix (RTM)** demonstrating every URS-ID maps to ≥ 1 approved test case.
8. **DPIA** approved per study before patient enrolment in EU sites.
9. **HIPAA BAA** executed with Veeva for US trials.

## 7. Constraints

- Vendor releases are continuous; site does not control vendor SDLC; vendor release notes are reviewed under change control within 14 days.
- TMFR v3.3.1 is the current taxonomy; v4 is expected ~2027; impact assessment within 60 days of new version release.
- EU CTR transparency obligations (Art. 81) impose publication timelines that affect TMF closure cadence.
- HIPAA + GDPR + Swiss FADP + AT DSG cross-border transfer routes shall be SCC-governed where adequacy decisions absent.
- CTIS submission specification version drift requires CI-based contract testing of pack outputs.

## 8. Assumptions

- Okta, Vault CTMS, Vault QualityDocs, Vault RIM, Medidata Rave, Cornerstone, Sirius Argus, Clario eCOA are validated independently and their integration APIs are stable per documented contracts.
- Veeva maintains its certifications (SOC 2 Type II, ISO 27001, HIPAA) and provides advance notice of platform changes.
- DPA between Marinos and Veeva is executed per GDPR Art. 28; sub-processor list is reviewable.
- ICH E6(R3) Step 4 (6 January 2025) is the current GCP framework; transition arrangements per ICH implementation guidance.
- DIA TMF Reference Model v3.3.1 is the operative taxonomy; Marinos participates in the TMFR Discussion Forum for v4 input.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 — Electronic Records; Electronic Signatures (§§ .10(a/b/c/d/e/g/k), .30, .50, .70, .100, .200, .300).
- 21 CFR Part 312 — Investigational New Drug Application (§ 312.62 retention).
- 21 CFR Part 314 — Applications for FDA Approval to Market a New Drug.
- 21 CFR Part 54 — Financial Disclosure by Clinical Investigators.
- FDA *Guidance for Industry: Computerized Systems Used in Clinical Investigations* (2007).
- FDA Bioresearch Monitoring (BIMO) Program — inspection-readiness practice.

### EU — EMA / Commission
- EU Clinical Trials Regulation 536/2014 — Arts. 25 (application dossier), 56 (archiving), 57 (CTMF), 58 (archiving cadence), 71 (sponsor obligations), 81 (transparency), Annex I.
- CTIS — Clinical Trials Information System (current technical specification).
- EMA *Guideline on the content, management and archiving of the clinical trial master file (paper and/or electronic)* (EMA/INS/GCP/856758/2018 Rev 2).
- EU GMP Annex 11 §§ 4 (validation), 6 (accuracy), 9 (audit trail), 11 (periodic evaluation).
- GDPR (Regulation (EU) 2016/679) — Arts. 6, 9, 32, 35.

### DACH-specific competent authorities
- **BfArM (DE)** — Bundesinstitut für Arzneimittel und Medizinprodukte — medicinal products + medical devices.
- **Paul-Ehrlich-Institut (DE)** — biological medicinal products + vaccines.
- **Swissmedic (CH)** — Swiss Agency for Therapeutic Products.
- **AGES PharmMed (AT)** — Österreichische Agentur für Gesundheit und Ernährungssicherheit.

### International — ICH
- ICH E6(R3) — Good Clinical Practice (Step 4, adopted 6 January 2025).
- ICH E8(R1) — General Considerations for Clinical Studies.
- ICH E2A — Clinical Safety Data Management.

### Industry guidance / standards
- DIA TMF Reference Model v3.3.1 (CDISC, 2023) — Zones 01-11 + Sections + Artefacts + Sub-artefacts.
- ISPE GAMP 5 (2nd Edition, 2022).
- PIC/S PI 041 — Good Practices for Data Management and Integrity in Regulated GMP/GDP Environments.
- ISO/IEC 27001:2022 — Information Security Management Systems.

### Vendor
- Veeva — *Vault eTMF 24R3 Validation Approach* + *24R3 Release Notes*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

