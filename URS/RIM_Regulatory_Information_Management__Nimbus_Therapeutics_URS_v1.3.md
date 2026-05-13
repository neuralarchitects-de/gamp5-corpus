---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; expanded 2026-05-12 (T3 uplift to 115 requirements; ICH M4 CTD + ICH M8 eCTD explicit; IDMP ISO 11238/11239/11240/11615/11616; EMA SPOR; 21 CFR § 11 sub-section authority map; CTIS Art. 25; FDA ESG)"
seed_corpus_basis:
  - "ISPE GAMP 5 (2nd Edition, 2022) Cat 4 SaaS conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "21 CFR Part 314 (NDA) + Part 312 (IND)"
  - "FDA Providing Regulatory Submissions in Electronic Format — Drug Establishment Registration and Drug Listing"
  - "FDA Electronic Submissions Gateway (ESG) Guidance"
  - "ICH M2 ESTRI; ICH M4 — Common Technical Document; ICH M8 — eCTD (Electronic Common Technical Document)"
  - "EMA EU eCTD specifications + EU Module 1 Specification"
  - "EMA Q&A on eCTD v4"
  - "IDMP — ISO 11238 (Substances), ISO 11239 (Pharmaceutical Dose Forms), ISO 11240 (Units of Measurement), ISO 11615 (Medicinal Products), ISO 11616 (Pharmaceutical Products)"
  - "EMA SPOR — Substances / Products / Organisations / Referentials master data services"
  - "EU CTR 536/2014 Art. 25 (application dossier) + Art. 81 (transparency)"
  - "PMDA / Health Canada / TGA / ANVISA / NMPA regional eCTD Module 1 specifications"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "GDPR Arts. 6, 32; ISO/IEC 27001:2022; PIC/S PI 041"
  - "BfArM (DE); Paul-Ehrlich-Institut (DE); Swissmedic (CH); AGES PharmMed (AT)"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# User Requirements Specification (URS)

## RIM — Veeva Vault RIM Suite (Submissions + Registrations + Submissions Archive) 24R3

**Document Number:** NIM-URS-RIM-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Nimbus Therapeutics Limited, Global Regulatory Operations, Auckland, New Zealand *(fictional)*
**System Owner:** Head of Regulatory Operations
**Process Owner:** VP Regulatory Affairs
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS; vendor handles infrastructure; site validates configuration)
**Project Mode:** Configuration project on commercial software product **Veeva Vault RIM Suite (Submissions + Registrations + Submissions Archive) 24R3** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a/b/c/d/e/g/k), .30, .50, .70, .100, .200, .300; 21 CFR Parts 312 + 314; FDA *Providing Regulatory Submissions in Electronic Format* (eCTD); FDA ESG Guidance; ICH M2 ESTRI; ICH M4 CTD; ICH M8 eCTD; EMA EU eCTD + EU Module 1; EMA Q&A on eCTD v4; IDMP ISO 11238/11239/11240/11615/11616; EMA SPOR; EU CTR 536/2014 Arts. 25 + 81; PMDA / Health Canada / TGA / ANVISA / NMPA Module 1 specifications; EU GMP Annex 11 §§ 4, 6, 9, 11; GDPR Arts. 6, 32; ISO/IEC 27001:2022; PIC/S PI 041; BfArM (DE); PEI (DE); Swissmedic (CH); AGES PharmMed (AT).

> **Note.** This URS covers Nimbus Therapeutics' enterprise Regulatory Information Management platform covering: (a) Submission Planning + Tracking per region, (b) Registration Tracking per market, (c) Product Master Data (IDMP-aligned), (d) Substance + Organisation + Referential master data sync with EMA SPOR, (e) Submission Build + Publishing + Archive (eCTD Modules 1-5), (f) Health Authority correspondence + commitments + variations + renewals, (g) Inspection-readiness for HA inspections. It is distinct from the **eTMF** (Marinos Therapeutics — clinical trial master file), **CTMS** (Dryad — clinical operations), **PV** (Sirius — pharmacovigilance), and **EDMS** (Vellis — controlled documents).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of Regulatory Operations) | _____________ | _____________ | _____ |
| Reviewer (Vendor Assurance — Veeva relationship owner) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Privacy Officer — GDPR) | _____________ | _____________ | _____ |
| Reviewer (Head of Submissions Operations) | _____________ | _____________ | _____ |
| Approver (VP Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-08 | (synthetic) | Editorial fixes; vendor version 24R3. |
| 1.2 | 2026-05-12 | (synthetic) | T3 uplift to 115 requirements (Tier T3 per § 2A.13 — large enterprise system spanning Submission Planning + Tracking, Registrations, Product Master / IDMP, SPOR sync, eCTD publishing, Submission Archive, HA Correspondence, Commitments + Variations + Renewals, ESG dispatch). ICH M4 + M8 explicit; IDMP ISO 11238/11239/11240/11615/11616; EMA SPOR; FDA ESG; § 11 sub-section authority map applied per § 2A.2; risk table expanded to 10 rows. |

## Definitions

| Term | Definition |
|---|---|
| RIM | Regulatory Information Management |
| Vault RIM | Veeva Vault RIM Suite (Submissions + Registrations + Submissions Archive + RIM Platform) Release 24R3 |
| CTD | Common Technical Document (ICH M4) |
| eCTD | Electronic Common Technical Document (ICH M8) — file-and-folder hierarchy + index XML for HA submissions |
| Module 1 | Region-specific administrative + prescribing information (per HA Module 1 spec) |
| Modules 2-5 | ICH-harmonised content (Summaries, Quality, Nonclinical, Clinical) |
| Sequence | A submission unit numbered per the receiving HA's eCTD spec |
| Lifecycle Operator | eCTD lifecycle operation: new, append, replace, delete |
| HA | Health Authority (FDA, EMA, PMDA, Health Canada, TGA, ANVISA, NMPA, etc.) |
| IDMP | Identification of Medicinal Products (ISO 11238 substances, 11239 dose forms, 11240 units, 11615 medicinal products, 11616 pharmaceutical products) |
| SPOR | EMA Substances / Products / Organisations / Referentials master-data services |
| ESG | FDA Electronic Submissions Gateway |
| ECTR | EU Clinical Trials Regulation 536/2014 |
| MAA | Marketing Authorisation Application (EU) |
| NDA | New Drug Application (US) |
| Variation | Post-authorisation submission modifying terms of MA |
| Renewal | Periodic MA renewal submission |
| Commitment | Post-authorisation commitment / condition tracked per HA |
| EDMS | Vault QualityDocs / Vellis Pharma (separate URS) |
| eTMF | Marinos Therapeutics (separate URS) |
| PV | Sirius Pharma Argus (separate URS) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

Define the user requirements for the regulatory information management platform that Nimbus Therapeutics uses to author, manage, plan, track, build, publish, dispatch, archive, and report eCTD submissions + registrations + product master data + commitments globally, in compliance with ICH M4 + M8, region-specific Module 1 specifications, IDMP, EMA SPOR, FDA ESG, EU CTR 536/2014, and 21 CFR Part 11.

## 2. Scope

**In scope:**
- Veeva Vault RIM Suite 24R3 multi-tenant SaaS: Submissions, Registrations, Submissions Archive, RIM Platform.
- Per-region eCTD configuration (FDA Module 1, EMA Module 1, PMDA, Health Canada, TGA, ANVISA, NMPA).
- Submission lifecycle (DRAFT → IN-REVIEW → APPROVED → READY-TO-PUBLISH → PUBLISHED → SUPERSEDED) with e-signatures and SoD.
- Sequence build + validation + dispatch (gateway-based: FDA ESG, EMA gateway, regional HA gateways).
- IDMP master data (ISO 11238 substances, 11239 dose forms, 11240 units, 11615 medicinal products, 11616 pharmaceutical products); EMA SPOR sync.
- Registration tracking per market with state transitions (planned, in-review, approved, suspended, withdrawn).
- HA correspondence inbound / outbound capture with classification + source + commitment / submission linkage.
- Variations + renewals + post-approval commitments tracking with due-date escalation.
- Inspection-readiness for HA inspections.
- Integrations: Okta SSO + MFA; Vault Connect → Vault QualityDocs (Vellis), Vault eTMF (Marinos), Vault PV (Sirius Argus); EMA SPOR API; FDA ESG; regional HA gateways.

**Out of scope:**
- HA gateway agent infrastructure (vendor-managed).
- Pharmacovigilance case management (Sirius Argus URS).
- Clinical trial master file (Marinos eTMF URS).
- Document authoring tools (Microsoft Word + Veeva annotation tools at user desktops).

## 3. System Description and Intended Use

Vault RIM is the system of record for Nimbus Therapeutics' regulatory information across the product portfolio: product master data (IDMP), registrations per market, planned + in-flight + archived submissions, HA correspondence, commitments, variations, renewals. Sequences are authored against HA-specific eCTD Module 1 configurations + ICH M4/M8 Modules 2-5 content, validated against HA-specific rule sets, dispatched via gateway, and archived immutably.

GAMP 5 (2nd Edition, 2022) Category 4 — Configured Product. Veeva maintains the platform SDLC; Nimbus validates configuration (region eCTD specs, product / region / lifecycle metadata, workflows, integrations, SPOR sync rules).

## 4. User Roles

| Role | Permissions | SoD Constraints |
|---|---|---|
| Regulatory Author | Author + edit submission documents in DRAFT | Cannot review or approve own work |
| Regulatory Reviewer | Review documents; cannot approve | Cannot author or approve same document |
| Regulatory Approver | Approve documents + sequences | Cannot self-approve; cannot author same doc |
| Submissions Coordinator | Build, validate, dispatch sequences | Cannot approve; cannot author |
| Registration Manager | Maintain registration records per market | Cannot author submission documents |
| Product Master Steward | Maintain IDMP master data + SPOR sync | Cannot approve submissions |
| HA Correspondence Owner | Capture inbound / outbound HA correspondence | Read-only on submissions |
| Commitments Owner | Track post-approval commitments + due dates | Cannot approve submissions |
| Vendor (CRO) User | Read / write per contracted scope | Restricted views per product / region |
| RIM Administrator | Configuration changes under change control | Cannot author or approve |
| Auditor / Inspector | Read-only with time-bounded credentials | Strict read-only |

Separation of duties: Author ≠ Reviewer ≠ Approver of the same submission; Submissions Coordinator ≠ Approver; Product Master Steward ≠ Submissions Approver.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` / `R2` / `R3`), and a verifiable `shall`-clause.

### 5.1 Vendor / Platform Assurance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-01 | H | R1 | Veeva shall be qualified as a critical SaaS vendor; SOC 2 Type II, ISO/IEC 27001:2022, customer-shared CSV summary for Vault RIM 24R3; annual re-qualification. |
| URS-VND-02 | H | R1 | Vendor releases shall be impact-assessed within 14 days; configuration-affecting changes shall trigger re-validation. |
| URS-VND-03 | H | R1 | Vendor SDLC evidence shall be reviewed annually; checklist stored in vendor-assurance dossier. |
| URS-VND-04 | M | R2 | Vendor sub-processor list shall be reviewed quarterly per GDPR Art. 28(2). |

### 5.2 Configuration / Region eCTD + Module 1 Specifications

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CFG-01 | H | R1 | Country / region / product / submission-type metadata shall be maintained per current HA requirements; configuration changes through change control. |
| URS-CFG-02 | H | R1 | eCTD specifications (FDA Module 1, EMA Module 1, ICH M4 + M8, PMDA, Health Canada, TGA, ANVISA, NMPA) shall be configured to current published versions; version updates impact-assessed within 30 days of publication. |
| URS-CFG-03 | H | R1 | Region-specific Module 1 controlled vocabularies (e.g., FDA submission types, EMA procedure types) shall be maintained per current HA terminology. |
| URS-CFG-04 | H | R1 | Document lifecycle states shall be: DRAFT → IN-REVIEW → APPROVED → READY-TO-PUBLISH → PUBLISHED → SUPERSEDED. |
| URS-CFG-05 | H | R1 | Lifecycle transitions shall require role-restricted electronic signatures with SoD enforced. |
| URS-CFG-06 | M | R2 | eCTD v4 (ICH M8) readiness configuration shall be deployable per HA-published v4 implementation timelines. |

### 5.3 Submission Planning and Tracking

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLN-01 | H | R1 | A multi-region submission plan shall be maintainable per product per submission type, with target HA dates, content owners, dependencies, milestones. |
| URS-PLN-02 | H | R1 | Critical-path tracking shall surface late tasks against committed HA dates; configurable lead-time alerts (D-60, D-30, D-14, D-7, D-0). |
| URS-PLN-03 | H | R1 | Per-region submission status (Planned, In Build, In Review, Ready to Publish, Published, Acknowledged, Approved, Withdrawn) shall be tracked. |
| URS-PLN-04 | M | R2 | Resource-planning view shall surface workload per author / reviewer / approver against submission deadlines. |
| URS-PLN-05 | M | R2 | Plan baseline + revisions shall be retained for retrospective slip analysis. |

### 5.4 Sequence Build, Validate, Dispatch

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEQ-01 | H | R1 | Sequence build shall assemble documents per the HA-specific eCTD Module 1 + ICH M4/M8 Modules 2-5 structure; missing required documents shall block the build. |
| URS-SEQ-02 | H | R1 | Sequence validation shall run the configured rule set (HA-specific validators); validation failures shall block dispatch. |
| URS-SEQ-03 | H | R1 | Lifecycle operator handling (new, append, replace, delete) shall conform to ICH M8 specification; lifecycle integrity verified on build. |
| URS-SEQ-04 | H | R1 | Sequence numbering shall be unique per HA per product; gaps / duplicates shall be blocked. |
| URS-SEQ-05 | H | R1 | Dispatch via the HA gateway (FDA ESG, EMA, regional) shall produce an MDN / acknowledgement; non-acknowledgement within configured window shall escalate to Regulatory Operations. |
| URS-SEQ-06 | H | R1 | Cross-references between sequences + supporting documents (eTMF, QualityDocs) shall be maintained; broken references shall be flagged monthly. |
| URS-SEQ-07 | H | R1 | Sequence content shall be cryptographically hashed (SHA-256) at READY-TO-PUBLISH state; hash shall match Archive hash on dispatch. |
| URS-SEQ-08 | M | R2 | Submission package preview (rendered HA-style view) shall be available prior to dispatch. |

### 5.5 Submissions Archive

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ARC-01 | H | R1 | Every dispatched sequence + acknowledgement shall be archived immutably with SHA-256 content checksums. |
| URS-ARC-02 | H | R1 | Sequences shall be retrievable in original dispatched form for inspection within 4 business hours. |
| URS-ARC-03 | H | R1 | Retention shall meet the longest applicable retention from any HA receiving the submission (typically ≥ 30 years post-licence-discontinuation; longer per jurisdictional minimums). |
| URS-ARC-04 | M | R2 | Archive integrity verification shall be run quarterly; integrity failures shall be deviated and remediated. |
| URS-ARC-05 | M | R2 | Archive export shall support regulator-requested formats (eCTD v3.2.2 + v4 future). |

### 5.6 Registrations and Product Master Data (IDMP)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REG-01 | H | R1 | Registration records per product per country with state {PLANNED, IN-REVIEW, APPROVED, SUSPENDED, WITHDRAWN}; state transitions audit-trailed. |
| URS-REG-02 | H | R1 | Variations + renewals + line extensions shall be tracked against the parent registration with submission-sequence linkage. |
| URS-REG-03 | H | R1 | Approval letter + label-version + indication-version linkage shall be maintained per registration. |
| URS-IDMP-01 | H | R1 | Product master data shall conform to **ISO 11615** (Medicinal Product Identification); identifiers per HA region maintained. |
| URS-IDMP-02 | H | R1 | Substance master data shall conform to **ISO 11238** (Substance Identification); UNII / EMA SMS identifiers reconciled. |
| URS-IDMP-03 | H | R1 | Pharmaceutical product data shall conform to **ISO 11616** (Pharmaceutical Product Identification). |
| URS-IDMP-04 | H | R1 | Pharmaceutical dose forms + routes shall conform to **ISO 11239**; controlled vocabulary maintained. |
| URS-IDMP-05 | H | R1 | Units of measurement shall conform to **ISO 11240**. |
| URS-IDMP-06 | H | R1 | IDMP data shall be exportable in HL7 FHIR R5 + ISO XML formats for HA submission. |

### 5.7 EMA SPOR Sync (Substances, Products, Organisations, Referentials)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SPOR-01 | H | R1 | The system shall synchronise Substance Management Service (SMS) entries with EMA SPOR; sync cadence nightly with conflict-resolution workflow when local vs SPOR diverge. |
| URS-SPOR-02 | H | R1 | The system shall synchronise Product Management Service (PMS) entries with EMA SPOR. |
| URS-SPOR-03 | H | R1 | The system shall synchronise Organisation Management Service (OMS) entries with EMA SPOR. |
| URS-SPOR-04 | H | R1 | The system shall synchronise Referential Management Service (RMS) entries (controlled vocabularies, e.g., dose forms, routes) with EMA SPOR. |
| URS-SPOR-05 | M | R2 | SPOR sync conflicts shall be queued for Product Master Steward resolution; resolution decisions shall be audit-trailed. |
| URS-SPOR-06 | M | R2 | SPOR referential drift shall be detected via daily diff report; drift > 5% shall raise a deviation. |

### 5.8 Health Authority Correspondence Tracking

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-COR-01 | H | R1 | Inbound + outbound HA correspondence shall be captured with classification, source, target submission / commitment linkage, response-required flag, due-date. |
| URS-COR-02 | H | R1 | Response due-dates shall trigger D-30 / D-14 / D-7 / D-0 alerts; overdue responses shall escalate to VP Regulatory Affairs. |
| URS-COR-03 | M | R2 | Correspondence shall be cross-linked to commitments + variations + renewals it relates to. |
| URS-COR-04 | M | R2 | Correspondence archive shall be searchable by HA + product + submission + classification. |

### 5.9 Commitments + Variations + Renewals Tracking

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CMT-01 | H | R1 | Post-approval commitments per HA shall be tracked with due-date; alerts at D-30 / D-7 / D-0; overdue escalates to VP Regulatory Affairs. |
| URS-CMT-02 | H | R1 | Commitment status (Open / In Progress / Submitted / Closed / Withdrawn) shall be tracked; closure shall reference closing submission sequence. |
| URS-VAR-01 | H | R1 | Variations shall be tracked per HA with category (Type IA, IB, II, etc. for EMA; CBE, CBE-30, PAS for FDA), state, submission-sequence linkage. |
| URS-VAR-02 | M | R2 | Variation patterns (multi-region simultaneous variations) shall be groupable as variation campaigns. |
| URS-RNW-01 | H | R1 | Renewal tracking per HA shall surface upcoming renewal dates; lead-time alerts configurable (12 months / 6 months / 3 months / 1 month). |

### 5.10 Audit Trail / 21 CFR Part 11 / Data Integrity

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Audit trail shall cover document edits, lifecycle, sequence build / validation / dispatch, configuration changes, signatures, registration state changes, IDMP / SPOR updates. |
| URS-AUD-02 | H | R1 | Audit trail shall be append-only at the platform level; tenant administrators shall not have UPDATE / DELETE on audit records. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be performed monthly by the Head of Regulatory Operations. |
| URS-AUD-04 | H | R1 | Audit-trail retention shall be ≥ 30 years post-licence-discontinuation. |
| URS-PART11-01 | H | R1 | Per § 11.10(a), procedural controls shall protect electronic-record validity. |
| URS-PART11-02 | H | R1 | Per § 11.10(b), accurate + complete copies shall be exportable. |
| URS-PART11-03 | H | R1 | Per § 11.10(c), records shall be protected throughout retention. |
| URS-PART11-04 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via Okta SAML 2.0 + MFA. |
| URS-PART11-05 | H | R1 | Per § 11.10(e), operational audit trail per URS-AUD-01. |
| URS-PART11-06 | H | R1 | Per § 11.10(g), authority checks shall enforce role-based permissions. |
| URS-PART11-07 | H | R1 | Per § 11.10(k), system operation manuals shall be maintained under change control. |
| URS-PART11-08 | H | R1 | Per § 11.30, internet-exposed components shall apply additional controls (TLS 1.3, short-lived tokens). |
| URS-PART11-09 | H | R1 | Per § 11.50, e-signatures shall include signer's printed name, date and time, and meaning of signature. |
| URS-PART11-10 | H | R1 | Per § 11.70, signatures shall be cryptographically bound to the signed record. |
| URS-PART11-11 | H | R1 | Per § 11.100, signature identifiers shall be unique per individual; reuse blocked. |
| URS-PART11-12 | H | R1 | Per § 11.200, re-authentication shall be required at the moment of signing critical sequence approvals + dispatch authorisations. |
| URS-PART11-13 | H | R1 | Per § 11.300, password / credential controls per InfoSec policy; MFA mandatory, lockout 5 fails / 15 min. |
| URS-DI-01 | H | R1 | **Attributable** — every action carries actor_id. |
| URS-DI-02 | H | R1 | **Legible** — PDF/A-3 + machine-readable XML/JSON exports. |
| URS-DI-03 | H | R1 | **Contemporaneous** — NTP-synced server timestamps authoritative. |
| URS-DI-04 | H | R1 | **Original** — original document content preserved unaltered. |
| URS-DI-05 | H | R1 | **Accurate** — sequence build + validation calculations deterministic. |
| URS-DI-06 | M | R2 | **Complete / Consistent / Enduring / Available** — ≥ 30 years retention. |

### 5.11 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-EDMS-01 | H | R1 | RIM shall consume controlled documents from Vault QualityDocs (Vellis) via Vault Connect. |
| URS-INT-ETMF-01 | M | R2 | Cross-references to Marinos eTMF for clinical-trial artefacts cited in regulatory submissions. |
| URS-INT-PV-01 | M | R2 | Pharmacovigilance commitments / data shall cross-link to Sirius Argus PV (separate URS); PSUR / PBRER references resolvable. |
| URS-INT-PUBLISH-01 | H | R1 | Publishing engine invocation via documented API; output gateway connectivity tested per quarter. |
| URS-INT-ESG-01 | H | R1 | FDA Electronic Submissions Gateway integration shall conform to FDA ESG technical specification; ESG account credentials managed under Reg Ops controls. |
| URS-INT-SPOR-01 | H | R1 | EMA SPOR API integration shall conform to EMA SPOR technical spec (REST + OAuth 2.0); nightly sync. |
| URS-INT-SSO-01 | H | R1 | Okta SAML 2.0 + MFA for user authentication; SCIM 2.0 provisioning. |
| URS-INT-API-01 | M | R2 | Vault Connect APIs shall be authenticated via OAuth 2.0 client-credentials; short-lived tokens. |

### 5.12 Performance, Availability, Backup, Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | Document open / list response ≤ 3 s at 95th percentile. |
| URS-PERF-02 | M | R2 | Sequence build time shall scale linearly with sequence size; nominal 1,500-document sequence builds in ≤ 30 minutes. |
| URS-AV-01 | H | R1 | Availability per Veeva SLA; ≥ 99.9% during regulator-deadline windows (HA target dates). |
| URS-BAK-01 | H | R1 | Vendor-managed backup; site shall verify vendor-published RPO ≤ 4 h / RTO ≤ 24 h annually. |
| URS-BAK-02 | M | R2 | Site shall maintain tenant-data export ≥ 30 y cold storage. |
| URS-SEC-01 | H | R1 | TLS 1.3 in transit + AES-256 at rest. |
| URS-SEC-02 | H | R1 | Per-product / per-region access restricted by role. |
| URS-SEC-03 | H | R1 | Vendor SOC 2 + ISO 27001 evidence reviewed annually. |
| URS-SEC-04 | M | R2 | Annual penetration testing of regulatory-author + gateway-dispatch endpoints. |

### 5.13 Inspection-Readiness

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INSP-01 | H | R1 | HA inspection-readiness dashboard shall surface registrations + recent submissions + commitments status + open variations + correspondence backlog. |
| URS-INSP-02 | H | R1 | Inspection export shall produce a regulator-ready package (PDF/A-3 + machine-readable index) within 4 business hours of request. |
| URS-INSP-03 | M | R2 | Inspector workspace shall provide read-only access with time-bounded credentials (30 d default), watermarked downloads, audit-trailed activity. |
| URS-INSP-04 | M | R2 | Inspection-pack contents shall be configurable per HA (FDA BIMO, EMA, BfArM, PEI, Swissmedic, AGES, PMDA) per published inspection-program scope. |

### 5.14 Reporting and Search

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RPT-01 | M | R2 | Standard report library shall include: Submission Pipeline, Registration Status by Market, Commitment Aging, Variation Backlog, Correspondence Backlog, IDMP Currency, SPOR Drift. |
| URS-RPT-02 | M | R2 | Full-text search across submission documents shall respect access-control scopes. |
| URS-RPT-03 | M | R2 | Ad-hoc report builder shall be available to Head of Regulatory Operations + Submissions Coordinator roles. |
| URS-RPT-04 | L | R3 | Report rendering performance shall complete standard reports in ≤ 5 minutes. |

### 5.15 Configuration Management and Change Control

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CCM-01 | H | R1 | Configuration changes shall flow through DEV → UAT → PROD with SoD-enforced approvals. |
| URS-CCM-02 | H | R1 | Configuration baselines shall be versioned and exportable; drift detectable via baseline-diff reports. |
| URS-CCM-03 | M | R2 | Vendor release impact-assessment shall be completed ≤ 14 days. |
| URS-CCM-04 | M | R2 | HA-spec-driven configuration changes (Module 1 updates, eCTD validator updates) shall be tested in UAT against a regression suite before PROD promotion. |

### 5.16 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Role-specific RIM training in Cornerstone (Vega) shall be completed before any user receives production access. |
| URS-TRN-02 | M | R2 | Annual refresher training shall cover ICH M4 + M8 updates, IDMP / SPOR changes, HA Module 1 spec updates. |
| URS-PR-01 | H | R1 | Annual Periodic Review shall cover eCTD specification status per region, IDMP / SPOR sync currency, audit-trail review evidence, vendor-assurance status, training currency, security posture; signed by Head of Regulatory Operations + VP Regulatory Affairs + Head of QA. |

### 5.17 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is SAML 2.0 via Entra ID with SCIM lifecycle provisioning; conditional-access policy `Regulatory-App Conditional Access (FIDO2 phishing-resistant MFA)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the RIM metadata DB plus object-replica for submission artefacts; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ Product-lifetime + 25 y per the consuming-record schedule. |

## 6. Acceptance Criteria

1. CS, RA, IQ (vendor-shared), OQ, PQ approved and executed.
2. PQ shall include representative end-to-end submission to FDA (ESG) + EMA + 1 RoW HA (e.g., PMDA), plus IDMP master-data sync round-trip with EMA SPOR.
3. VSR approved by VP Regulatory Affairs + Head of QA.
4. RTM demonstrating every URS-ID maps to ≥ 1 approved test case.

## 7. Constraints

- Vendor releases not under site change control; impact-assessed within 14 days.
- HA specifications change frequently — site impact assessment within 30 days of HA publication.
- eCTD v4 transition follows HA-published implementation timelines; not all HAs will adopt simultaneously.

## 8. Assumptions

- Okta, Vault QualityDocs, Vault eTMF, Sirius Argus, EMA SPOR, FDA ESG are validated independently and stable per documented contracts.
- Veeva maintains SOC 2 + ISO 27001 + HIPAA certifications and provides advance notice of platform changes.
- DPA between Nimbus and Veeva is executed per GDPR Art. 28.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- 21 CFR Parts 312 + 314.
- FDA *Providing Regulatory Submissions in Electronic Format* — current edition.
- FDA Electronic Submissions Gateway (ESG) Guidance.

### EU — EMA / Commission
- EU Module 1 Specification — current published version.
- EMA Q&A on eCTD v4.
- EU CTR 536/2014 Arts. 25, 81.
- EMA SPOR — SMS / PMS / OMS / RMS service specifications.

### International — ICH
- ICH M2 — ESTRI.
- ICH M4 — Common Technical Document.
- ICH M8 — eCTD (Electronic Common Technical Document).

### IDMP — ISO
- ISO 11238 — Substance Identification.
- ISO 11239 — Pharmaceutical Dose Forms / Units / Routes of Administration / Packaging.
- ISO 11240 — Units of Measurement.
- ISO 11615 — Medicinal Product Identification.
- ISO 11616 — Pharmaceutical Product Identification.

### Regional
- PMDA — Module 1 specification.
- Health Canada — Module 1 specification.
- TGA (AU) — Module 1 specification.
- ANVISA (BR) — Module 1 specification.
- NMPA (CN) — Module 1 specification.

### DACH-specific competent authorities
- **BfArM (DE)** — medicinal products + medical devices.
- **Paul-Ehrlich-Institut (DE)** — biological medicinal products + vaccines.
- **Swissmedic (CH)** — Swiss Agency for Therapeutic Products.
- **AGES PharmMed (AT)** — Österreichische Agentur.

### Industry guidance / standards
- ISPE GAMP 5 (2nd Edition, 2022).
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- PIC/S PI 041.
- ISO/IEC 27001:2022.
- GDPR Arts. 6, 32.

### Vendor
- Veeva — *Vault RIM Suite 24R3 Validation Approach* + *Configuration Reference*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

