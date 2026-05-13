---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-27; enriched 2026-05-12 (T3 uplift per METHODOLOGY § 2A.13)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 803 — Medical Device Reporting (subparts A, B, C, D, E)"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU MDR Reg. 2017/745 Arts. 87 (Serious incidents), 88 (Trend), 89 (FSCA), 92 (EUDAMED vigilance module)"
  - "EU IVDR Reg. 2017/746 Arts. 82, 83 (vigilance)"
  - "IMDRF AET — Adverse Event Terminology WG/N43 (Annexes A–G)"
  - "MDCG 2023-3 — Q&A on vigilance terms and concepts under MDR"
  - "ISO 14971:2019; ISO 13485:2016; ISO/IEC 27001:2022"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Medical-Device Adverse Event Database — Sparta Systems TrackWise Digital Quality (Vigilance Module)

**Document Number:** TEA-URS-MDR-001 | **Version:** 1.0 | **Effective Date:** 2026-04-27 *(synthetic)*
**Site:** Theia Pharma & Devices Ltd., Global Vigilance, Galway, Ireland *(fictional)* with regional vigilance hubs in München (DE) and Wien (AT)
**System Owner:** Director, Device Vigilance
**Process Owner:** Head of Post-Market Surveillance (HQ) — and PRRC (EU MDR Art. 15) for EU market
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Project Mode:** Configuration project on commercial software product **Sparta Systems TrackWise Digital Quality (Vigilance Module)** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 803 §§ .1–.58 (medical-device reporting, eMDR via FDA ESG); 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU MDR Reg. 2017/745 Arts. 87, 88, 89, 92; EU IVDR Reg. 2017/746 Arts. 82, 83; IMDRF AET (WG/N43); MDCG 2023-3; ISO 14971:2019; ISO 13485:2016.

> **Note:** Distinct from the Vega PMS database (VGD-URS-PMS-001) which covers proactive PMS, PSURs, trending. This URS covers **reactive vigilance** — eMDR / MIR / national IRIS submissions per Art. 87 serious-incident and Art. 88 trend obligations.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Device Vigilance) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (PRRC — EU MDR Art. 15) | _____________ | _____________ | _____ |
| Reviewer (Vigilance Operations Manager) | _____________ | _____________ | _____ |
| Reviewer (Risk Management Lead — ISO 14971) | _____________ | _____________ | _____ |
| Approver (Head of Post-Market Surveillance) | _____________ | _____________ | _____ |
| Approver (VP Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | T3 enrichment per METHODOLOGY § 2A.13 (100–150 reqs): § 5 broken out into 13 subsections; complaint-intake channels expanded; MDR/eMDR decision-tree explicit (§ 5.4); IMDRF AET coding lifecycle per WG/N43 (§ 5.5); 5-day initial + 30-day standard timelines explicit (§ 5.6); follow-up reports (§ 5.7); Art. 88 trend reporting (§ 5.8); FSCA tracking (§ 5.9); MAUDE prep + EUDAMED routing (§ 5.10); Risk-Management-File link per ISO 14971 (§ 5.11); 21 CFR Part 11 sub-section-explicit (§ 5.12); DACH national CA gateways (§ 5.13); Combination-product cross-ref to Sirius PV (§ 5.14); FS catch-up to follow. |

## Definitions

| Term | Definition |
|---|---|
| eMDR | Electronic Medical Device Report (FDA, per 21 CFR Part 803 + FDA ESG submission) |
| MIR | Manufacturer Incident Report (EU MDR vigilance form for serious incidents) |
| MAUDE | FDA's Manufacturer and User Facility Device Experience database (public-facing MDR records) |
| FDA ESG | FDA Electronic Submissions Gateway |
| EUDAMED | EU Database on Medical Devices (vigilance module per Art. 92) |
| IMDRF AET | IMDRF Adverse Event Terminology (WG/N43); Annexes A–G coding hierarchy |
| MDCG | Medical Device Coordination Group (EU) |
| FSCA | Field Safety Corrective Action (per EU MDR Art. 89) |
| FSN | Field Safety Notice (the communication of an FSCA) |
| PRRC | Person Responsible for Regulatory Compliance (EU MDR Art. 15) |
| Serious Incident | EU MDR Art. 2(65): death / serious deterioration in health / serious public-health threat |
| Trend | EU MDR Art. 88: statistically significant increase in frequency or severity of non-serious incidents / expected side-effects |
| Reportability | Determination whether an event meets jurisdictional reporting criteria |
| Reportable Event | Event meeting reportability criteria per applicable regulation |
| UDI-DI | Unique Device Identifier — Device Identifier portion |
| ISO 13485 | Medical-device QMS standard |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the medical-device adverse-event database used by Theia Pharma & Devices to receive, code, assess, submit, and track vigilance reports for marketed medical devices and IVDs across the FDA eMDR, EU EUDAMED (when live) + national CA gateways, Health Canada, and DACH national gateways, with cross-reference to the combination-product PV system (Sirius Argus) where applicable.

## 2. Scope

**In:** Sparta TrackWise Digital Quality (Vigilance Module) multi-tenant SaaS; per-device configuration; SSO via Okta SAML 2.0 + MFA; integrations with FDA eMDR gateway (FDA ESG, HL7 ICSR XML), EUDAMED vigilance module (when live), BfArM (DE) IRIS interface, Swissmedic (CH) ElViS interface, AGES (AT), Health Canada CIPARS, the Sirius PV database (Argus) for combination-product cross-reference, MasterControl eQMS (CAPA + deviation linkage), Vault QualityDocs for IFU + risk-file references, Atlas Serialization (UDI-DI device-master), the literature-surveillance feed.

**Out:** vendor infrastructure (Sparta-managed); clinical-trial AE reporting (separate Sirius Argus URS); patient-support call-centre; pre-market device evaluation; commercial CRM.

## 3. System Description

The vigilance module is the system of record for device incident reports across spontaneous, complaint-derived, distributor-reported, and trend-driven sources. Cases flow Intake → Triaged → Investigated → Reportability-Decided (per regulation-specific decision tree) → Approved → Submitted via the appropriate gateway → Closed, with reporting clocks enforced per jurisdiction. The system supports IMDRF Annex A–G coding (per WG/N43), the EU MDR Art. 87 serious-incident decision flow, Art. 88 trend reporting, Art. 89 FSCA tracking, and Risk-Management-File feedback per ISO 14971:2019 §10.

GAMP Cat 4: Sparta maintains the platform SDLC; site validates per-device workflow configuration, reporting-rule configuration, integration boundaries, and 21 CFR Part 11 controls. No site-authored custom code.

## 4. User Roles

| Role | Permissions | SoD constraint |
|---|---|---|
| Case Intake | Create / triage cases from intake channels; cannot assess. | ≠ Reviewer, Approver |
| Case Investigator | Investigate, code (IMDRF Annexes), complete fields. | ≠ Reportability Reviewer, Approver of same case |
| Reportability Reviewer | Decide reportability per applicable regulation; cannot self-approve. | ≠ Investigator, Approver of same case |
| Submission Approver | Approve submission; QPP-equivalent (US) / PRRC (EU). | ≠ Investigator, Reportability Reviewer of same case |
| PRRC (EU) | EU MDR Art. 15 compliance for EU market; statutory role. | Cannot delegate Art. 15 sign-offs |
| Submissions Specialist | Send eMDR / MIR / national reports; reconcile acks. | ≠ Case content editor |
| FSCA Coordinator | Manage FSCAs and FSNs per Art. 89; cannot approve. | ≠ FSCA Approver |
| Trender / Signal Reviewer | Triage Art. 88 trend signals; cannot self-approve closure. | ≠ Trend Approver |
| Vigilance Administrator | Configure workflows / rules; cannot approve. | ≠ Approver |
| Auditor | Read-only across cases, audit trails, submissions. | Read-only |

**Separation of duties:** Investigator ≠ Reportability Reviewer ≠ Approver of the same case; Vigilance Administrator cannot approve cases or submit reports.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` direct GxP impact / `R2` indirect / `R3` none), and a verifiable `shall`-clause.

### 5.1 Vendor / Platform Assurance and Configuration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-01 | H | R1 | Sparta shall be qualified as a critical SaaS vendor with SOC 2 Type II, ISO 27001, ISO 13485 evidence, customer-shared CSV summary, BAA, and DPA; re-qualified annually. |
| URS-VND-02 | H | R1 | Vendor releases shall be impact-assessed within 14 days of release; configuration-affecting changes shall trigger re-validation. |
| URS-VND-03 | M | R2 | Annual Sparta TR-Audit summary shall be filed in the Vendor Assurance dossier. |
| URS-CFG-01 | H | R1 | Per-device configuration (UDI-DI binding, reportability rules per jurisdiction, IMDRF coding pack version, gateway profiles) shall follow DRAFT → REVIEW → APPROVED → EFFECTIVE; SoD-enforced signatures. |
| URS-CFG-02 | M | R2 | Configuration changes shall be exportable as version-stamped artefacts for inspection. |

### 5.2 Complaint Intake Channels

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INTAKE-01 | H | R1 | The system shall ingest complaints from spontaneous channels: HCP via portal `hcp.theia.com`, patient via secure web form, distributor / importer via REST API, partner-exchange via E2B(R3)-equivalent feed. |
| URS-INTAKE-02 | H | R1 | Email-gateway parser (`vigilance@theia.com`) shall extract structured fields with audit-trail of source email retained. |
| URS-INTAKE-03 | H | R1 | Phone-call ticket integration shall create an intake record with operator-id, recording reference, transcription where consented. |
| URS-INTAKE-04 | H | R1 | Complaint-derived cases shall be linked to the originating complaint record; complaints flowing from the eQMS shall flow back with case-id reference. |
| URS-INTAKE-05 | M | R2 | Literature-surveillance hits shall create cases when reportability is plausible, with citation captured. |
| URS-INTAKE-06 | M | R2 | Distributor / importer obligations per EU MDR Arts. 14, 16 shall be enforced via chain-of-custody fields. |

### 5.3 Case Lifecycle and State Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CASE-01 | H | R1 | Each case shall be assigned a unique, monotonic case-id, intake-date, awareness-date, UDI-DI / device-id, reporter-type, reporter-country, complaint description, suspected-event. |
| URS-CASE-02 | H | R1 | Workflow lifecycle shall be {Intake → Triaged → Investigated → Reportability-Decided → Approved → Submitted → Closed}; reverse transitions shall require captured reason + electronic signature. |
| URS-CASE-03 | H | R1 | Awareness-date shall be the earliest date at which the manufacturer (or its representative) became aware that the event might constitute a reportable event; awareness-date capture shall be explicit. |
| URS-CASE-04 | H | R1 | Follow-up information arriving post-submission shall create a new case version; the version delta shall determine whether a follow-up report is required. |
| URS-CASE-05 | H | R1 | Re-classification (e.g., non-serious → serious) shall re-trigger reporting clocks and re-route the case. |
| URS-CASE-06 | M | R2 | Case priority shall be auto-assigned (high / medium / normal) per a configurable matrix based on event-severity + device-class. |
| URS-CASE-07 | M | R2 | Duplicate-detection shall run on intake against (UDI-DI + complainant identifiers + event-date proximity + event description similarity); suspected duplicates routed to merge decision. |

### 5.4 MDR / eMDR Decision Tree

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MDR-01 | H | R1 | The reportability decision tree shall classify each event per 21 CFR Part 803.20 categories: (1) device may have caused or contributed to a death, (2) device may have caused or contributed to a serious injury, (3) device malfunctioned and would be likely to cause or contribute to death or serious injury if recurring. |
| URS-MDR-02 | H | R1 | EU MDR Art. 2(65) classification shall apply: serious incident (death / serious deterioration / public-health threat) vs non-serious incident vs use error. |
| URS-MDR-03 | H | R1 | Reportability decision shall be captured with rule-applied + reasoning narrative + decision-maker-id + timestamp; non-reportable decisions shall be auditable and reviewed at QA cadence. |
| URS-MDR-04 | H | R1 | Reportability rules shall be configurable per jurisdiction with version control; rule changes shall be re-validated via OQ. |
| URS-MDR-05 | M | R2 | Decision-tree pre-population from event-type coding shall be supported to reduce reviewer cognitive load; pre-population is suggestion-only, not auto-decision. |

### 5.5 IMDRF AET Coding (per WG/N43)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CODE-01 | H | R1 | Cases shall be coded per IMDRF Adverse Event Terminology (WG/N43): Annex A (event-type), Annex B (medical-device problem), Annex C (component / part), Annex D (investigation), Annex E (clinical-sign / symptom / condition — patient outcome), Annex F (investigation result), Annex G (event-conclusion / health-effect). |
| URS-CODE-02 | H | R1 | Coding decisions shall be captured with coder-id, IMDRF version, coding timestamp, and manual override reason if applicable. |
| URS-CODE-03 | H | R1 | IMDRF annual release shall be impact-assessed and migrated under change control; open cases shall be re-coded per a defined policy. |
| URS-CODE-04 | M | R2 | Coding QC shall be performed on a sample (≥ 2% / month); discrepancies feed coder training. |
| URS-CODE-05 | M | R2 | IMDRF–MedDRA cross-walk shall be supported for combination-product cases that also require Sirius Argus MedDRA coding. |

### 5.6 Reporting Timelines and Submission Engine

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TIME-01 | H | R1 | FDA reporting timelines per 21 CFR Part 803 shall be enforced: 30-day standard MDR for serious-injury / malfunction; 5-day Initial Report for events requiring remedial action to prevent unreasonable risk of substantial harm to public health (per 21 CFR 803.53). |
| URS-TIME-02 | H | R1 | EU MDR Art. 87 timelines shall be enforced: serious-public-health-threat report ≤ 2 days; death / unanticipated serious deterioration ≤ 10 days; other serious incidents ≤ 15 days from awareness-date. |
| URS-TIME-03 | H | R1 | DACH national-CA-specific timelines (BfArM, Swissmedic, AGES) shall be enforced per local rule packs. |
| URS-TIME-04 | H | R1 | Pre-deadline alerts shall fire at D-3, D-1, D0; D0 breach shall trigger escalation to Vigilance Operations Manager + PRRC. |
| URS-TIME-05 | H | R1 | Reporting-clock calculations shall be deterministic, validated under OQ via golden-test pack of 25 timeline scenarios. |
| URS-SUB-01 | H | R1 | The system shall generate eMDR HL7 ICSR XML compliant with FDA 21 CFR Part 803.21 + FDA's eMDR Implementation Guide; schema validation pre-send. |
| URS-SUB-02 | H | R1 | EU MIR XML shall be generated per the EUDAMED MIR-form schema (or national-CA equivalent during EUDAMED transition); per-CA profiles supported. |
| URS-SUB-03 | H | R1 | Submission shall be transmitted via FDA ESG (eMDR), EUDAMED (when live), BfArM IRIS, Swissmedic ElViS, AGES, Health Canada CIPARS; ack messages reconciled to case. |
| URS-SUB-04 | H | R1 | Negative ack shall open a structured Exception with error-code mapping; resubmission within regulator grace period; escalation to PRRC on breach. |

### 5.7 Follow-Up Reports

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-FU-01 | H | R1 | Follow-up information shall be captured as a new case version; delta computation shall trigger Supplemental Report (per 21 CFR 803.10) or follow-up MIR per EU MDR. |
| URS-FU-02 | H | R1 | Investigation completion shall trigger a Final Report submission; final reports shall be tracked separately from initial reports. |
| URS-FU-03 | M | R2 | Open follow-up commitments (e.g., 30-day investigation due) shall be tracked with due-date alerts. |

### 5.8 Trend Reporting (EU MDR Art. 88)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRD-01 | H | R1 | Trending shall be performed per device / per failure-mode / per use-error per ISO 14971:2019; statistical methods (Poisson rate-change / CUSUM / EWMA) configurable per device-class. |
| URS-TRD-02 | H | R1 | Art. 88 trend reporting: when a non-serious incident rate trend reaches configurable statistical significance threshold, an Art. 88 report shall be generated and submitted to the competent authority. |
| URS-TRD-03 | H | R1 | Trend reports shall include denominator (sales-volume from Atlas Serialization), numerator (incident count by IMDRF coding), and the statistical-test result. |
| URS-TRD-04 | M | R2 | Trend-detection KPIs shall be reported monthly to Director of Vigilance. |

### 5.9 FSCA Tracking (EU MDR Art. 89)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-FSCA-01 | H | R1 | FSCA decisions shall be captured with rationale, scope (UDI-DI list + lot numbers + serial numbers), communication plan, and competent-authority notifications. |
| URS-FSCA-02 | H | R1 | FSN generation shall use the MDCG-prescribed template per Art. 89; multi-language support for affected markets. |
| URS-FSCA-03 | H | R1 | FSCA effectiveness shall be tracked post-action with quantitative measure (e.g., % field-units recovered, repeat-event rate). |
| URS-FSCA-04 | H | R1 | FSCA notifications shall be routed to applicable CAs (FDA, EUDAMED, BfArM, Swissmedic, AGES, Health Canada). |

### 5.10 MAUDE Preparation and EUDAMED Routing

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MAUDE-01 | H | R1 | The system shall produce a MAUDE-search preparation report per device-line showing recent FDA-submitted MDRs that will appear in the MAUDE public database; the report shall be reviewed prior to product-launch and quarterly thereafter. |
| URS-MAUDE-02 | M | R2 | MAUDE narrative-redaction guidance shall be enforced (PII / patient identifiers stripped) before FDA submission per FDA's redaction expectations. |
| URS-EUDAMED-01 | H | R1 | EUDAMED routing: when EUDAMED vigilance module is live for the relevant device class, submission shall route to EUDAMED; until then, national-CA gateways shall be used per the transition rules. |
| URS-EUDAMED-02 | M | R2 | EUDAMED module-readiness shall be configurable per device class with audit-trail of activation. |

### 5.11 Risk-Management-File Link (ISO 14971:2019)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RMF-01 | H | R1 | Each device shall have a bidirectional link to its Risk-Management File per ISO 14971:2019; case events shall be linked to known hazards / hazardous situations. |
| URS-RMF-02 | H | R1 | New hazards identified through vigilance shall trigger a Risk-Management-File update workflow per ISO 14971 §10.3 (Production and post-production information). |
| URS-RMF-03 | M | R2 | Risk-control-effectiveness metrics shall be calculated using post-market data and fed into the Risk-Management Report. |

### 5.12 21 CFR Part 11 Compliance (sub-section-explicit per METHODOLOGY § 2A.2)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a), procedures and controls protecting electronic-record validity (cases, signatures, audit, submissions) shall be documented and reviewed annually. |
| URS-PART11-02 | H | R1 | Per § 11.10(b), the system shall generate accurate and complete copies of records suitable for inspection (PDF representations of cases, eMDR XML, audit-trail extracts). |
| URS-PART11-03 | H | R1 | Per § 11.10(c), records shall be protected throughout the retention period (≥ life-of-product + 10 y; ≥ 15 y for implantables per EU MDR Art. 10(8)); immutable cold storage. |
| URS-PART11-04 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via Okta SAML 2.0 + MFA. |
| URS-PART11-05 | H | R1 | Per § 11.10(e), the operational audit trail shall capture case content, coding, assessments, signatures, configuration, submission events. |
| URS-PART11-06 | H | R1 | Per § 11.50, signature events shall include printed name + date / time + meaning. |
| URS-PART11-07 | H | R1 | Per § 11.70, signatures cryptographically bound to record state at signing. |
| URS-PART11-08 | H | R1 | Per § 11.100, signature uniqueness; user-ids never reassigned. |
| URS-PART11-09 | H | R1 | Per § 11.200, re-authentication required at every critical signature event (submission approval, FSCA approval). |
| URS-PART11-10 | H | R1 | Per § 11.300, password / credential controls per InfoSec policy. |

### 5.13 DACH National CA Gateways

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-NCA-BFARM-01 | H | R1 | BfArM (DE) IRIS interface shall be supported for device-vigilance reporting per MPDG; quarterly connectivity test; certificate rotation under change control. |
| URS-NCA-SWISS-01 | H | R1 | Swissmedic (CH) ElViS interface shall be supported per MepV; CH-specific timelines configurable. |
| URS-NCA-AGES-01 | H | R1 | AGES (AT) interface shall be supported per AMG (AT). |
| URS-NCA-LANG-01 | M | R2 | DACH FSN templates shall support de-DE, de-AT, de-CH variants. |

### 5.14 Combination Products and Cross-Reference to PV

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-COMBO-01 | H | R1 | Combination-product cases (device + drug) shall be cross-referenced to the Sirius PV (Argus) database via case-id mapping; daily reconciliation. |
| URS-COMBO-02 | M | R2 | Combination-product reportability shall apply both 21 CFR Part 803 + 21 CFR Part 314.80 / EU MDR Art. 87 + EU GVP rules; the dominant-mode-of-action regulation shall drive the primary report. |

### 5.15 Audit Trail and Records Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Audit trail covering all case content, coding, reportability decisions, signatures, configuration changes, submission events with user, action, old / new value, reason, timestamp. |
| URS-AUD-02 | H | R1 | Audit trail append-only at the database level; tenant administrators included. |
| URS-AUD-03 | H | R1 | Retention: ≥ life-of-product + 10 y; ≥ 15 y for implantables per EU MDR Art. 10(8). |
| URS-AUD-04 | H | R1 | Audit-trail review monthly (case-level event-driven) + quarterly (platform-level by QA). |

### 5.16 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-FDA-01 | H | R1 | FDA ESG eMDR gateway connectivity tested quarterly; certificate rotation under change control. |
| URS-INT-EUDAMED-01 | H | R1 | EUDAMED gateway when live; transition routing to national gateways documented. |
| URS-INT-PV-01 | H | R1 | Cross-reference to Sirius PV (Argus) for combination products; daily reconciliation. |
| URS-INT-EQMS-01 | H | R1 | Linkage to MasterControl eQMS deviations for CAPA flow. |
| URS-INT-SSO-01 | H | R1 | SSO via Okta SAML 2.0 + MFA. |
| URS-INT-UDI-01 | H | R1 | UDI-DI device-master integration with Atlas Serialization for product identification + sales-volume context. |
| URS-INT-LIT-01 | M | R2 | Literature-surveillance feed for proactive vigilance. |

### 5.17 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | **Attributable:** records attributable to a named user. |
| URS-DI-02 | H | R1 | **Legible:** PDF/A-3 + eMDR XML exportable. |
| URS-DI-03 | H | R1 | **Contemporaneous:** server-side NTP-synced timestamps. |
| URS-DI-04 | H | R1 | **Original:** source preserved; corrections recorded as new versions. |
| URS-DI-05 | H | R1 | **Accurate:** reporting-clock + trend calculations deterministic; OQ-verified. |
| URS-DI-06 | H | R1 | **Complete / Consistent / Enduring / Available:** records meet retention obligations. |

### 5.18 Performance / Availability / Security / Training / PR

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | Case-page navigation P95 ≤ 3s. |
| URS-AV-01 | H | R1 | Availability ≥ 99.7% per vendor SLA; 24×7 for gateway during submission windows. |
| URS-BAK-01 | H | R1 | Vendor-managed backup; site verifies RPO ≤ 4h, RTO ≤ 24h annually. |
| URS-SEC-01 | H | R1 | Okta SSO + MFA; per-device / per-region access. |
| URS-SEC-02 | H | R1 | TLS 1.3 in transit; AES-256 at rest. |
| URS-SEC-03 | M | R2 | Annual penetration test; high/critical findings remediated within 60 days. |
| URS-TRN-01 | H | R1 | LMS-recorded role-specific training; PRRC competency for EU; eMDR competency for US. |
| URS-TRN-02 | M | R2 | Annual refresher covering FDA guidance updates, EU MDCG updates, IMDRF AET annual release. |
| URS-PR-01 | H | R1 | Annual periodic review covering vendor qualification, configuration drift, IMDRF version status, gateway connectivity, FSCA effectiveness summary, deviation summary, training currency; signed by Director Device Vigilance + PRRC + VP Regulatory Affairs + VP QA. |

### 5.19 Inspection Readiness and Health-Authority Correspondence

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INSP-01 | H | R1 | An inspection-readiness export shall produce a dossier per device covering complaint summary, eMDR / MIR submission log, FSCA history, trend reports, RMF link, training records, audit trail extracts; retrievable ≤ 4 h. |
| URS-INSP-02 | H | R1 | Health-authority correspondence (CA queries, follow-up requests, inspector questions) shall be tracked in a structured register with sender, due-date, response-due-date, status. |
| URS-INSP-03 | M | R2 | Pre-inspection mock-audit workflow shall capture rehearsal findings and remediation status. |

### 5.20 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is SAML 2.0 via Entra ID with SCIM lifecycle provisioning; conditional-access policy `PV-Sensitive Conditional Access (FIDO2 phishing-resistant MFA + named-location enforcement)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with PostgreSQL pg_basebackup + continuous WAL archiving; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 30 y (PV) per the consuming-record schedule. |

### 5.21 Cross-System Integration — eQMS CAPA handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-EQMS-01 | H | R1 | On detection of Vigilance signal-detection finding (trigger: Signal-detection threshold breach, IMDRF AET coding finding, reportability decision finding), the system shall push a CAPA-ticket creation event to the Talos MasterControl eQMS (`TLB-URS-EQMS-001`) via the eQMS event-push channel with required metadata {originating_system, originating_record_id, finding_class, severity, evidence_package_uri, detection_ts_utc, detection_user, regulatory_basis}; severity per MDCG 2020-1 + site PV procedure. |
| URS-XINT-EQMS-02 | H | R1 | The eQMS ticket-creation call shall be idempotent on `{originating_system, originating_record_id, finding_class}`; the eQMS status-callback shall be ingested and reflected on the originating record with a hyperlink to the eQMS ticket; closed-loop verification per ICH Q9(R1) + ICH Q10 shall be evidenced before the originating record is dispositioned. |

### 5.22 Cross-System Integration — PMS DB handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-PMS-01 | H | R1 | FSCA decisions, MDR/eMDR submissions, and combination-product PV cross-references shall be published to the EU MDR PMS DB (`VGD-URS-PMS-001`) via the FSCA-callback channel `theia.fsca.callback.v1` so that the device PMS plan and the next PSUR cycle inherit the FSCA evidence in a closed loop. |
| URS-XINT-PMS-02 | H | R1 | PMS DB-originated vigilance signals ingested into the AE DB shall preserve the originating PMS record ID as a first-class attribute on the AE case for bidirectional traceability per EU MDR Art. 87 + 88. |

## 6. Acceptance Criteria

CS, RA, IQ (vendor-shared), OQ (workflow / coding / signature / submission / FSCA / audit), PQ (end-to-end scenarios: spontaneous → eMDR; serious-incident → 10-day MIR; trend → Art. 88 report; FSCA → FSN + multi-CA routing; follow-up + final-report; combination-product cross-ref to Argus; DR failover) approved and executed; VSR approved by Director Device Vigilance + PRRC + VP Reg Affairs + VP QA; RTM maps every URS-ID to ≥ 1 approved test case.

## 7. Constraints

- Vendor releases not under site change control but evaluated within 14 days before promotion.
- IMDRF version upgrades managed annually.
- PRRC sign-off non-delegatable.
- EUDAMED vigilance module availability constrains routing transition.

## 8. Assumptions

- Okta, Argus (Sirius PV), MasterControl eQMS, Atlas Serialization, FDA ESG, EUDAMED, BfArM IRIS, Swissmedic ElViS, AGES, Health Canada CIPARS are validated.
- IMDRF AET subscription current.

## 9. References

### US

- 21 CFR Part 803 §§ .1–.58 — Medical Device Reporting (subparts A General, B Definitions, C MDR for user facilities, D MDR for importers, E MDR for manufacturers).
- 21 CFR 803.10 — Supplemental + Follow-up reports.
- 21 CFR 803.20 — Reportable event criteria.
- 21 CFR 803.21 — eMDR format (HL7 ICSR).
- 21 CFR 803.53 — 5-day reports.
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- FDA *eMDR Implementation Guide* (current revision).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).

### EU

- EU MDR Reg. 2017/745 Arts. 10, 14, 15, 16, 87, 88, 89, 92.
- EU IVDR Reg. 2017/746 Arts. 82, 83.
- MDCG 2023-3 — Q&A on vigilance terms and concepts under MDR.
- MDCG 2019-9 — Summary of safety and clinical performance.
- EUDAMED — vigilance module specification.

### DACH (per METHODOLOGY § 2A.6)

- BfArM (DE) MPDG; IRIS reporting interface.
- Swissmedic (CH) MepV; ElViS reporting interface.
- AGES PharmMed (AT); AMG (AT) device-vigilance reporting.

### International

- IMDRF AET (WG/N43) — Annexes A–G.
- ISO 14971:2019; ISO/TR 24971:2020; ISO 13485:2016; ISO/IEC 27001:2022.
- ISPE GAMP 5 (2nd Edition, 2022); PIC/S PI 041.

### Vendor

- Sparta Systems — *TrackWise Digital Quality (Vigilance Module) 2025 Configuration Reference*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

