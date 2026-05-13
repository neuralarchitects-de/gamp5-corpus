---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; T4 hand-expansion 2026-05-12"
seed_corpus_basis:
  - "R Submissions Working Group ADRG (FDA-submitted clinical-data context)"
  - "GAMP 5 (2nd ed.) Cat 4 conventions for SaaS clinical-trial platforms"
  - "21 CFR Part 11; EU GMP Annex 11; ICH E6(R3) GCP (Step 4, 6 January 2025)"
  - "ICH E8(R1); ICH E9(R1); ICH E2A; ICH M11"
  - "CDISC SDTM v2.0 / ADaM v1.3 / CDASH v2.3 / ODM-XML v1.3.2 / Define-XML v2.1"
  - "EU CTR 536/2014 + CTIS Sponsor Handbook"
  - "FDA Computerized Systems Used in Clinical Investigations (May 2007)"
  - "FDA Electronic Source Data in Clinical Investigations (Sep 2013)"
  - "GDPR Arts. 6, 9, 22, 32, 35; HIPAA"
  - "Medidata Rave EDC 2024 vendor documentation"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## EDC — Medidata Rave EDC 2024

**Document Number:** MAR-URS-EDC-001
**Version:** 1.0
**Effective Date:** 2026-04-26 *(synthetic)*
**Site:** Marigold Clinical Operations GmbH, Clinical Data Management, München, Germany *(fictional)*
**System Owner:** Director, Clinical Data Management
**Process Owner:** VP Clinical Operations
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS; vendor handles infrastructure; site validates per-study build)
**Project Mode:** Configuration project on commercial software product **Medidata Rave EDC 2024** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a)–(k), .30, .50, .70, .100, .200, .300; ICH E6(R3) GCP (Step 4, adopted 6 January 2025); ICH E8(R1) General Considerations; ICH E9(R1) Estimands; ICH E2A Clinical Safety; EU CTR Reg. 536/2014 + CTIS; FDA *Computerized Systems Used in Clinical Investigations* (May 2007); FDA *Electronic Source Data in Clinical Investigations* (Sep 2013); EMA *Guideline on Computerised Systems and Electronic Data*; GDPR Arts. 6, 9, 22, 32, 35; HIPAA; CDISC SDTM / ADaM / CDASH / ODM-XML / Define-XML; BfArM + PEI gateways for German CTIS submissions.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Clinical Data Management) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Vendor Assurance — Medidata relationship owner) | _____________ | _____________ | _____ |
| Reviewer (Clinical Pharmacology / Statistics) | _____________ | _____________ | _____ |
| Reviewer (Pharmacovigilance Lead) | _____________ | _____________ | _____ |
| Reviewer (Data Protection Officer — GDPR) | _____________ | _____________ | _____ |
| Approver (VP Clinical Operations) | _____________ | _____________ | _____ |
| Approver (VP Quality Assurance) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Added DACH site relocation (Princeton, NJ → München, DE); CTIS gateway requirements; full Part 11 sub-section bindings. |
| 1.2 | 2026-05-12 | (synthetic) | **Authored to Tier T4 (EDC-class mission-critical clinical system; 170-req target; spans study design + per-study build + capture + edit-checks + coding + SDV + safety + lab/imaging integrations + RBM + data lock + CDISC export + eConsent + ePRO + DSMB + CTIS).** Added 27 new §5 sub-sections covering ICH E6(R3) RBM data-feed, ICH E9(R1) estimand-supporting data integrity, eConsent + re-consent, ePRO integration, IXRS / IRT, lab + imaging (DICOM), safety reconciliation (Argus), Coder MedDRA + WHODrug version-pinning, mid-study amendment workflow, DSMB / IDMC interim-analysis support, CTIS submission pack, data-lock workflow, SDTM/ADaM Define-XML export, GDPR Arts. 22 + 35 DPIA, FDA BIMO inspection-readiness, multi-language site activation, time-zone-aware visit calc, eSource direct capture, mobile / offline data entry, protocol-deviation workflow, query-management lifecycle, ALCOA+/PIC/S PI 041 bindings, and 14 new top-level risks. |

## Definitions

| Term | Definition |
|---|---|
| EDC | Electronic Data Capture |
| Rave | Medidata Rave EDC, version 2024 (multi-tenant SaaS) |
| Rave Architect | Per-study build authoring tool within Rave EDC |
| eCRF | Electronic Case Report Form |
| Casebook | The complete set of eCRFs for a single subject across all visits |
| Edit Check | Validation rule applied to data entered in eCRFs (univariate, cross-form, cross-visit) |
| Derivation | Deterministic, version-controlled computation producing a derived field from one or more source fields |
| SDV | Source Data Verification — comparison of eCRF data against the source record |
| SDR | Source Data Review — review of source records for accuracy / completeness / consistency (broader than SDV) |
| RBM | Risk-Based Monitoring (ICH E6(R3) § 3.10) — risk-proportionate combination of on-site, remote, and centralised monitoring |
| RBQM | Risk-Based Quality Management (broader than RBM; ICH E6(R3) § 3.0–3.12) |
| Critical-to-Quality (CtQ) Factor | Factor whose integrity is essential to participant rights/safety and trial-result reliability per ICH E8(R1) |
| Estimand | Precise description of the treatment effect per ICH E9(R1) — Treatment, Population, Variable, Intercurrent-Event strategy, Population-level summary |
| Intercurrent Event | Post-baseline event affecting interpretation or existence of outcome data (per ICH E9(R1)) |
| Protocol Deviation | Departure from the IRB / EC / CA-approved protocol |
| Important Protocol Deviation | A deviation that may significantly affect subject rights / safety / well-being or reliability of results |
| AE / SAE / SUSAR | Adverse Event / Serious Adverse Event / Suspected Unexpected Serious Adverse Reaction |
| MedDRA | Medical Dictionary for Regulatory Activities (adverse-event coding) |
| WHODrug | WHO Drug Dictionary (concomitant medication coding) |
| CDISC | Clinical Data Interchange Standards Consortium |
| SDTM | Study Data Tabulation Model (CDISC) — submission-ready tabulated data |
| ADaM | Analysis Data Model (CDISC) — analysis-ready datasets |
| CDASH | Clinical Data Acquisition Standards Harmonization (CDISC) — CRF-level standards |
| ODM-XML | Operational Data Model (CDISC) — exchange format for clinical data + metadata |
| Define-XML | CDISC metadata-submission standard (required by FDA + PMDA for every submission) |
| eTMF | Electronic Trial Master File (TMF Reference Model v3.3.x) |
| IRT / IXRS | Interactive Response Technology / Interactive Web/Voice Response System — randomisation + drug supply |
| ePRO / eCOA | Electronic Patient-Reported Outcome / Electronic Clinical Outcome Assessment |
| eSource | Direct electronic capture of clinical data without intermediate paper source |
| eConsent | Electronic informed consent (per FDA *Use of Electronic Informed Consent — Q&A*; 21 CFR Parts 11, 50, 56) |
| CTIS | Clinical Trials Information System (EU CTR 536/2014 sponsor portal) |
| DSMB / IDMC | Data Safety Monitoring Board / Independent Data Monitoring Committee |
| BIMO | FDA Bioresearch Monitoring program (sponsor + investigator + IRB inspections) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate + Complete, Consistent, Enduring, Available |
| DPIA | Data Protection Impact Assessment (GDPR Art. 35) |

## 1. Purpose

This URS defines requirements for the Electronic Data Capture (EDC) system used to capture, validate, clean, code, monitor, lock, and export clinical-trial data across Marigold-sponsored interventional studies (Phase II / III oncology and rare-disease). The system is the **system of record for protocol-defined clinical-trial subject data** and the primary data source for the SDTM / ADaM submission package.

## 2. Scope

**In scope:** Medidata Rave EDC 2024 multi-tenant SaaS instance; site configuration of per-study eCRF builds, edit checks, derivations, custom functions, study security profiles, and standard CDISC mappings; integrations with Medidata Coder (MedDRA + WHODrug coding), Medidata RTSM / IXRS (randomization / drug supply), Medidata eTMF (TMF Reference Model v3.3.x), central labs (LabCorp / Q² Solutions / Eurofins) via CDISC LAB / ODM, imaging core lab (DICOM gateway), the safety database (Oracle Argus 8.4), Marigold's ePRO (Iolanthe), the Watson LIMS (bioanalytical / PK), the CTIS sponsor workspace (EU CTR submission pack), and the central monitoring / RBM platform; SSO via Okta SAML 2.0 + MFA; vendor-assurance evidence for Medidata.

**Out of scope:** Medidata-managed infrastructure (validated under vendor SDLC); ePRO authoring (covered by Iolanthe URS); IRT / RTSM internals (covered by RTSM URS); investigator delegation-log + 1572 management (CTMS scope — Dryad CTMS URS); financial / payments tracking; eTMF authoring (Marinos eTMF URS).

## 3. System Description and Intended Use

Rave is the system of record for protocol-defined clinical-trial data. Per study, a study build configures eCRFs (using CDASH-aligned templates), edit checks (univariate, cross-form, cross-visit), derivations, lab normal ranges, user roles, and the SDTM mapping. Investigator-site staff enter subject data; CRAs perform source data verification (SDV) and source data review (SDR); medical monitors review safety in near-real-time; data managers run cleaning workflows and query management; on database lock, the SDTM / ADaM tabulations + Define-XML are produced for analysis and regulatory submission.

GAMP Cat 4: Medidata maintains the platform under their published SDLC; the vendor publishes customer-shared CSV evidence (validation summary, SOC 2 Type II, ISO 27001, HIPAA / HITECH attestation, GDPR DPA). Site validation focuses on per-study configuration, edit checks, derivations, integration boundaries, and 21 CFR Part 11 controls applied to study security, signatures, audit trail, and retention.

**ICH E6(R3) posture:** the platform supports the sponsor's Quality-by-Design (QbD) approach — Critical-to-Quality (CtQ) factors are identified during protocol design (ICH E8(R1) discipline), bound to specific eCRF fields and edit checks at study build, and monitored via the central monitoring / RBM data feed throughout the trial (ICH E6(R3) § 3.10).

## 4. User Roles

| Role | Permissions |
|---|---|
| Investigator (PI / Sub-I) | Sign eCRFs / casebooks for their subjects; cannot edit data as Monitor / Manager; submit FDA Form 1572 declarations |
| Site Coordinator (CRC) | Enter and edit subject data per delegation log; raise queries; trigger re-consent workflow |
| CRA / Monitor | Source data verification + source data review; raise / answer / close queries; cannot edit data; close monitoring visits |
| Data Manager | Run cleaning workflows; manage queries; configure listings; cannot lock without dual approval |
| Medical Monitor | Review safety data; raise medical queries; trigger SAE reconciliation against Argus; cannot edit |
| Statistician / Biostatistician | Read-only with statistical-package access for analysis dataset extraction; estimand definitions read-only |
| Coder (MedDRA / WHODrug) | Code AEs (MedDRA) and conmeds (WHODrug); raise coding queries; cannot edit clinical data |
| Study Builder | Configure eCRFs / edit checks / derivations / custom functions under study change control |
| Study Approver | Approve study build to PRODUCTION; cannot author build content |
| Migration Specialist | Author mid-study amendment migration scripts; cannot promote |
| EDC Administrator | Manage user / role / site provisioning; cannot edit data; cannot promote builds |
| DSMB Statistician (sealed) | Read-only access to closed / unblinded DSMB dataset cuts via firewalled extract path |
| Auditor / Inspector (BIMO / EMA / BfArM) | Read-only across study, audit trails, queries, eCRFs, configuration, change history; export-only |
| Data Protection Officer (GDPR) | Read access to data-subject identifiers; controls subject-erasure (Art. 17) gating per CTR carve-out |

Separation of duties (SoD), enforced at the user level by Rave's identity layer + Okta IdP:

- Investigator ≠ data-entry user (PI cannot also be CRC for the same subject)
- Study Builder ≠ Study Approver
- Data Manager ≠ Database Lock Approver
- Author of mid-study migration script ≠ approver of migration
- CRA monitoring a site ≠ CRA Lead approving the visit report for the same site
- Coder ≠ medical-monitor on the same coding decision
- DSMB statistician (sealed) ≠ any study-conduct role

## 5. User Requirements

### 5.1 Vendor / Platform Assurance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-01 | H | R1 | Medidata shall be qualified as a critical SaaS vendor with documented vendor-assurance evidence: SOC 2 Type II, ISO 27001, HIPAA attestation, GDPR DPA, customer-shared CSV summary for the Rave platform, and vendor SDLC summary. |
| URS-VND-02 | H | R1 | Vendor releases (Rave is updated quarterly per Medidata's 2024.x release train) shall be impact-assessed within 14 days of release-notes publication; configuration-affecting changes trigger study-build re-validation per the affected studies' change-control plans. |
| URS-VND-03 | M | R2 | Vendor sub-processors used in Marigold's data path shall be enumerated in the DPA and reviewed annually; new sub-processors shall be impact-assessed before activation. |
| URS-VND-04 | H | R1 | Vendor incident notifications (security incident, data breach, prolonged outage) shall reach Marigold within the contracted SLA window (≤ 24 h for confirmed data breaches per GDPR Art. 33 propagation). |

### 5.2 Per-Study Build Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BUILD-01 | H | R1 | Each study build shall progress through environments DEV → QC → UAT → PRODUCTION; only PRODUCTION builds may capture subject data; subject data shall never appear in DEV / QC / UAT. |
| URS-BUILD-02 | H | R1 | Build promotion shall require role-restricted electronic signatures with separation of duties (Builder ≠ Approver) per § 11.50 + § 11.100. |
| URS-BUILD-03 | H | R1 | UAT shall execute documented test scripts derived from the protocol's eCRFs, edit checks, derivations, and visit schedule; sign-off by clinical lead and data manager prior to PRODUCTION promotion. |
| URS-BUILD-04 | H | R1 | Mid-study changes (amendments) shall follow a controlled mid-study build process with documented impact assessment, retest of affected forms, migration scripts validated in UAT, and a production migration window with documented checkpoints and rollback plan. |
| URS-BUILD-05 | H | R1 | Quick-Publish (typo fixes, label changes, edit-check expression updates not changing semantics) shall be permitted only via a documented Quick-Publish workflow with builder + approver signatures and explicit semantic-equivalence justification. |
| URS-BUILD-06 | H | R1 | Each promotion shall produce a build-package artefact containing eCRF metadata, edit-check definitions, derivation logic, code lists, and SDTM mapping, archived to eTMF with SHA-256 fingerprint. |
| URS-BUILD-07 | M | R2 | Study Architect templates shall be governed under platform-level change control; template changes propagate to new builds, not retroactively to existing studies. |
| URS-BUILD-08 | H | R1 | Per-study Critical-to-Quality (CtQ) factor register (ICH E8(R1)) shall be captured during the build and bound to specific eCRF fields, edit checks, and SDV configuration. |

### 5.3 Per-Study eCRF Library and CDASH Alignment

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CRF-01 | H | R1 | eCRF library shall use CDASH v2.3 (or current per protocol) controlled-terminology bindings; deviations from CDASH shall be justified and archived. |
| URS-CRF-02 | H | R1 | Required-field, mandatory-with-skip, conditional-display, and code-list constraints shall be configurable per field and enforced server-side. |
| URS-CRF-03 | H | R1 | Visit schedule shall be configurable per protocol with visit windows (early / nominal / late tolerance) and shall enforce visit-window violations as queries. |
| URS-CRF-04 | M | R2 | Casebook completion shall be measurable per subject, per visit, per form, with completion KPIs feeding the central monitoring dashboard. |
| URS-CRF-05 | M | R2 | Each eCRF shall be associated with one or more Critical-to-Quality (CtQ) tags from URS-BUILD-08 to permit RBM-targeted SDV per URS-SDV-*. |

### 5.4 Data Capture and Edit Checks

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DATA-01 | H | R1 | Subject data entry shall enforce eCRF field types, mandatoriness, code-list constraints, range checks, and unit handling. |
| URS-DATA-02 | H | R1 | Edit-check failures (univariate, cross-form, cross-visit) shall raise queries automatically; investigator / coordinator response shall be timestamped and audit-trailed (§ 11.10(e)). |
| URS-DATA-03 | H | R1 | Derivations shall be deterministic, version-controlled, and tested in UAT; production derivation logic changes follow URS-BUILD-04. |
| URS-DATA-04 | H | R1 | Custom functions (Rave's scripting layer) shall be reviewed under code-review, locked to specific build versions, and prohibited from per-study free-form modification in production without a Cat-5 sub-component RA. |
| URS-DATA-05 | H | R1 | Manually-entered date / time fields shall capture time-zone where clinically meaningful (e.g., dose, AE onset, vital-sign collection); the system shall canonicalise stored timestamps to UTC with the originating time-zone retained. |
| URS-DATA-06 | M | R2 | The system shall reject impossible date / time entries (e.g., future date of birth, dose before randomisation) at the field level. |
| URS-DATA-07 | H | R1 | Data entry shall be supported on mobile / tablet devices for sites approved per the protocol; offline capture shall queue locally and reconcile on reconnect with conflict-detection. |

### 5.5 eSource and Direct Capture

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ESRC-01 | H | R1 | Direct electronic capture (eSource) per FDA *Electronic Source Data in Clinical Investigations* (Sep 2013) shall be permitted for designated forms; the captured data shall be flagged as eSource in metadata. |
| URS-ESRC-02 | H | R1 | For eSource fields, no separate paper source shall be required; ALCOA+ contemporaneous-capture requirement is satisfied by the direct entry timestamp. |
| URS-ESRC-03 | M | R2 | eSource device authentication shall require Okta + MFA; device shall be enrolled in the per-study device registry. |
| URS-ESRC-04 | M | R2 | eSource entries shall be marked in the SDTM dataset with `--ORIG` provenance indicators per CDISC controlled-terminology guidance. |

### 5.6 Query Management Workflow

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-QRY-01 | H | R1 | Queries shall be raised by (a) the edit-check engine automatically, (b) CRA / Monitor manually, (c) Data Manager manually, (d) Medical Monitor manually, (e) Coder for coding queries, with distinct query types. |
| URS-QRY-02 | H | R1 | Each query shall carry: query-id, subject-id, form-id, field-path, rule-id (if auto), raised-by (system or user-id), raised-at, status {OPEN, ANSWERED, CLOSED, CANCELLED}, response, response-author, response-at, closure-author, closure-at. |
| URS-QRY-03 | H | R1 | Closed queries shall not be re-opened after database hard-lock without an unlock-workflow (URS-LOCK-02). |
| URS-QRY-04 | M | R2 | Query-aging KPIs (median time-to-response, time-to-close, % overdue) shall feed the central monitoring dashboard and the RBM data feed. |
| URS-QRY-05 | H | R1 | Bulk-query operations (e.g., re-running an edit check across previously entered data) shall produce per-record query events; no silent suppression. |

### 5.7 Source-Data Verification (SDV) and Source-Data Review (SDR)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SDV-01 | H | R1 | SDV workflow per RBM strategy: CtQ-tagged critical fields default to 100%; non-critical fields are risk-based per the per-study RBM plan; SDV completion shall be captured with monitor signature. |
| URS-SDV-02 | H | R1 | SDR (broader review of source for accuracy / completeness / consistency) shall be a distinct activity from SDV, separately recorded, and shall not be conflated with SDV in evidence. |
| URS-SDV-03 | H | R1 | SDV-bypass conditions (e.g., remote SDV only) shall be approved per the RBM plan and audit-trailed; a "remote-SDV" flag shall propagate to the central monitoring dashboard. |
| URS-SDV-04 | M | R2 | SDV exception reports (fields not yet SDV'd at lock checkpoint) shall be generated for the lock checklist (URS-LOCK-01). |

### 5.8 Risk-Based Monitoring (ICH E6(R3) § 3.10) Data Feed

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RBM-01 | H | R1 | The system shall expose a Risk-Based Monitoring data feed including site-level KPIs (enrolment rate, query-aging, deviation rate, SDV completeness, missing-data rate by CtQ field) consumable by the central monitoring platform on a configurable cadence (daily by default). |
| URS-RBM-02 | H | R1 | Per ICH E6(R3) § 3.10, the feed shall support the sponsor's combined on-site / remote / centralised monitoring strategy; site-risk indicators shall be derivable from feed data. |
| URS-RBM-03 | H | R1 | RBM feed failures shall raise system alerts; a feed gap > 48 h shall block database lock until reconciled. |
| URS-RBM-04 | M | R2 | The feed schema shall be versioned and backwards-compatible across minor releases; breaking changes follow URS-BUILD-04. |

### 5.9 Coding (MedDRA + WHODrug)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-COD-01 | H | R1 | Adverse-event terms shall be coded against the protocol-specified MedDRA version (frozen per study with effective-from date recorded in the study build). |
| URS-COD-02 | H | R1 | Concomitant medications shall be coded against the protocol-specified WHODrug version (frozen per study). |
| URS-COD-03 | H | R1 | Autocode + manual-review workflow shall be supported; each manual override shall be audit-trailed with coder-id, MedDRA / WHODrug version, decision-timestamp, and rationale. |
| URS-COD-04 | H | R1 | Mid-study dictionary version-upgrade shall require: documented rationale, impact assessment on key tables, a re-coding plan, archiving of both versions and release notes in the eTMF, and signed approval by Medical Monitor + Data Manager. |
| URS-COD-05 | M | R2 | Coding-decision audit trail shall be exportable for inspection-readiness per FDA BIMO and EMA inspections. |
| URS-COD-06 | M | R2 | Synonym lists used in autocoding shall be version-controlled and reviewable. |

### 5.10 Investigator Signature

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SIG-01 | H | R1 | Each subject's data shall be signed electronically by the principal investigator at the form / casebook level per ICH E6(R3) (§ 6 — Investigator obligations) and 21 CFR Part 11 §§ .50 + .70 + .100 + .200. |
| URS-SIG-02 | H | R1 | Post-signature changes invalidate the signature and require re-signing; the audit trail preserves the prior signature event and the chain of edits between signatures. |
| URS-SIG-03 | H | R1 | The signature meaning string shall include the investigator's role attestation per ICH E6(R3) (e.g., "I have reviewed and confirm the accuracy of these data for the subject(s) under my responsibility"). |
| URS-SIG-04 | M | R2 | Casebook PDF (signed) shall be generable for inspection / archival, with each signature manifesting printed name, date / time, meaning. |

### 5.11 21 CFR Part 11 — Sub-section-Specific Bindings

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | § 11.10(a) — Procedures and controls protecting electronic-record validity: SOPs for system access, change control, data entry, and review shall be in effect at every site. |
| URS-PART11-02 | H | R1 | § 11.10(b) — Generating accurate and complete copies: casebook PDFs and SDTM / Define-XML exports shall be reproducible from the database state with checksum verification. |
| URS-PART11-03 | H | R1 | § 11.10(c) — Protection of records throughout retention period: ≥ 25 years post-trial completion per URS-AUD-04; vendor-hosted with backup + DR per URS-BAK-*. |
| URS-PART11-04 | H | R1 | § 11.10(d) — Limiting access to authorised individuals: Okta + MFA + role-based per URS-SEC-*. |
| URS-PART11-05 | H | R1 | § 11.10(e) — Operational audit trail: per URS-AUD-*. |
| URS-PART11-06 | H | R1 | § 11.10(g) — Use of authority checks: signature / promotion / lock actions verify the actor's authority before commit. |
| URS-PART11-07 | H | R1 | § 11.10(k) — System operation manuals + change control: vendor manuals + Marigold's per-study SOPs are version-controlled; user training is gated on current manual version. |
| URS-PART11-08 | H | R1 | § 11.30 — Open systems: not applicable for the EDC platform itself (closed system per Medidata's architecture); CTIS gateway treated as a controlled bridge with the protections of § 11.30 propagated. |
| URS-PART11-09 | H | R1 | § 11.50 — Signature manifestations: printed name, date / time, meaning captured for every electronic signature. |
| URS-PART11-10 | H | R1 | § 11.70 — Signature / record linking: signatures cryptographically bound to record-state at signature time. |
| URS-PART11-11 | H | R1 | § 11.100 — Uniqueness: each user-id unique; never reassigned to a different individual; deactivation does not free the id. |
| URS-PART11-12 | H | R1 | § 11.200 — Components of identity-based signatures: re-authentication (password + MFA) required at every signature event; cached credentials disabled at the signature moment. |
| URS-PART11-13 | H | R1 | § 11.300 — Password / credential controls: enforced via Okta password policy + MFA + lockout after configured failed attempts. |

### 5.12 Audit Trail

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Audit trail shall capture all data entry, edit-check evaluation, query lifecycle, signature, lock, unlock, configuration, build-promotion, and user-administration events with actor-id, timestamp, action, entity, old-value, new-value, and reason-for-change where required. |
| URS-AUD-02 | H | R1 | Audit trail shall be append-only at the platform level (vendor-managed); reviewable in-system and exportable as CSV / PDF / ODM-XML. |
| URS-AUD-03 | H | R1 | Audit-trail review per the RBM plan: critical-data audit-trail reviews per visit; quality issue trends fed back to the central monitoring dashboard per URS-RBM-01. |
| URS-AUD-04 | H | R1 | Retention shall be at least 25 years post-trial completion (combined max of ICH + FDA + EMA + per-jurisdiction extensions for paediatric / oncology). |
| URS-AUD-05 | H | R1 | Audit trail shall **never be disabled** in production; any apparent disablement (e.g., audit-trail row gap) shall raise a P1 system alert and block all writes until remediated. *(Mitigates known BIMO finding pattern — audit trail off in production for weeks.)* |
| URS-AUD-06 | H | R1 | Audit-trail entries shall be reason-for-change-tagged for every data change post-initial-entry (per § 11.10(e) + FDA *Computerized Systems Used in Clinical Investigations*). |
| URS-AUD-07 | M | R2 | Reason-for-change shall use a controlled vocabulary (data-entry error / new information / query response / system-driven / protocol clarification / other-justify) to enable trend analysis. |

### 5.13 Database Lock and Export

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LOCK-01 | H | R1 | Soft-lock and hard-lock shall be distinct states; hard-lock shall require a documented checklist (queries closed, SDVV complete, medical review complete, listings reviewed, signatures complete, coding complete, SAE reconciliation reconciled with Argus, RBM feed up-to-date) and dual approval signatures. |
| URS-LOCK-02 | H | R1 | Post-hard-lock changes shall require an unlock workflow with justification, scope (forms / sites / time-window), and a re-lock signature on completion; unlock evidence shall be filed in eTMF. |
| URS-LOCK-03 | H | R1 | Final dataset shall be exported in CDISC ODM-XML v1.3.2 and SDTM v2.0 formats; SDTM export shall be accompanied by Define-XML v2.1 metadata; export integrity verified by SHA-256 checksum reconciliation against the source database. |
| URS-LOCK-04 | H | R1 | ADaM v1.3 analysis datasets shall be derivable from the locked SDTM via the per-study ADaM specification; ADaM lineage shall be traceable back to SDTM source records. |
| URS-LOCK-05 | M | R2 | Lock checkpoints shall produce a "what-changed-since-last-export" delta to support DSMB / IDMC interim analyses (URS-DSMB-*). |
| URS-LOCK-06 | H | R1 | Final-database-lock evidence pack shall include: lock-checklist (signed), SDTM + Define-XML export bundle, ADaM specification, query-closure summary, SDV evidence, coding-finalisation evidence, SAE reconciliation evidence — filed in eTMF. |

### 5.14 SDTM / ADaM / Define-XML / Submission Package

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SDTM-01 | H | R1 | SDTM mapping shall be configured per study at build time; mapping changes follow URS-BUILD-04. |
| URS-SDTM-02 | H | R1 | SDTM export shall validate against the protocol-specified SDTM-IG version (e.g., SDTM-IG v3.4 or current) and shall pass Pinnacle21 (CDISC OpenCDISC) validation; errors block submission-package generation. |
| URS-SDTM-03 | H | R1 | Define-XML v2.1 shall accompany every SDTM + ADaM submission with full controlled-terminology metadata, value-level metadata, and analysis-variable annotations. |
| URS-SDTM-04 | M | R2 | Dataset-JSON (CDISC Dataset-JSON 1.0) export shall be supported as an alternative to SAS XPT for studies submitting under the FDA Dataset-JSON pilot. |
| URS-SDTM-05 | H | R1 | The SDTM round-trip (eCRF → SDTM → export → re-import for verification) shall preserve data values byte-equivalently for verifiable fields; numeric / character mismatches block lock. |

### 5.15 Integrations — Coding (Medidata Coder)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-CODER-01 | H | R1 | AE / SAE verbatim terms shall be routed to Medidata Coder for MedDRA coding; coding decisions captured with coder-id, MedDRA version, decision-timestamp; manual overrides audit-trailed. |
| URS-INT-CODER-02 | H | R1 | Conmed verbatim terms shall be routed to Medidata Coder for WHODrug coding; same audit-trail provisions. |
| URS-INT-CODER-03 | M | R2 | Coding interface failure shall raise an integration alert and shall not silently fall back to local autocode. |

### 5.16 Integrations — IRT / RTSM / IXRS

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-RTSM-01 | H | R1 | Randomisation status and dispensing data shall flow from RTSM (Medidata RTSM or Calyx IRT/IXRS depending on study) to the EDC; mismatches shall raise system queries and block database lock until resolved. |
| URS-INT-RTSM-02 | H | R1 | Subject re-randomisation on duplicate enrolment shall be prevented by RTSM ↔ EDC cross-validation against subject screening-id and demographics hash. |
| URS-INT-RTSM-03 | H | R1 | Drug-accountability data (dispensed / returned / unused / destroyed kits) shall reconcile between IRT and EDC drug-accountability eCRFs; unreconciled discrepancies block lock. |
| URS-INT-RTSM-04 | M | R2 | IRT silent-failure detection: heartbeat checks every 15 min; missed heartbeat for ≥ 4 successive intervals raises a P1 alert (mitigates "IXRS integration silent failure" risk). |

### 5.17 Integrations — Central Lab

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-LAB-01 | H | R1 | Central-lab data shall be ingested via CDISC LAB / ODM-XML; reference-range derivation per visit and per lab; lab-specific normal ranges configured per protocol. |
| URS-INT-LAB-02 | H | R1 | Local-lab data, where used, shall be entered with site-specific normal ranges or mapped to a central normalisation table per protocol. |
| URS-INT-LAB-03 | M | R2 | Lab-data anomaly (e.g., value outside ± 5σ of historical range) shall trigger an automated query to the site. |

### 5.18 Integrations — Imaging (DICOM)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-IMG-01 | H | R1 | Imaging core-lab data (DICOM-derived clinical reads) shall be ingested via a controlled gateway with study-id + subject-id + visit-id matching; PHI scrubbing per the protocol's de-identification rules. |
| URS-INT-IMG-02 | M | R2 | Imaging-derived eCRF fields shall be flagged with `--ORIG = "ASSIGNED"` per CDISC controlled terminology to distinguish from investigator-entered observations. |

### 5.19 Integrations — Pharmacovigilance / Safety (Oracle Argus)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-SAFETY-01 | H | R1 | Serious adverse events shall be flagged and transmitted to Argus within **24 hours** of investigator confirmation per the SAE-reconciliation SOP; reconciliation between EDC and Argus documented daily. |
| URS-INT-SAFETY-02 | H | R1 | SUSAR-class events (per ICH E2A) shall trigger the expedited-reporting clock: **Day-0 = sponsor awareness**; fatal / life-threatening → 7 calendar days initial + 8-day follow-up; non-fatal / non-LT → 15 calendar days initial. The system shall expose the awareness-date to PV and shall not be the regulatory clock owner. |
| URS-INT-SAFETY-03 | H | R1 | SAE reconciliation drift (EDC SAE ↔ Argus SAE mismatch) shall be detected daily; unresolved drift > 5 business days shall block database lock. |
| URS-INT-SAFETY-04 | M | R2 | SAE narrative free-text shall be available read-only in EDC (sourced from Argus) for medical-monitor review; narrative is the regulatory record in Argus, not EDC. |

### 5.20 Integrations — eTMF

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-ETMF-01 | M | R2 | Configuration baselines, study-build documentation, validation evidence, lock-checklist evidence, and per-version Define-XML shall be filed in eTMF per the TMF Reference Model v3.3.x. |
| URS-INT-ETMF-02 | M | R2 | eTMF cross-link from CTMS site-record (per Dryad CTMS URS) shall be machine-resolvable via stable study + site identifiers. |

### 5.21 Integrations — ePRO (Iolanthe)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-EPRO-01 | H | R1 | ePRO data captured by the Iolanthe Patient Portal shall be ingested into the EDC via CDISC ODM-XML; subject-id / visit-id / timestamp triplets shall reconcile against the EDC casebook. |
| URS-INT-EPRO-02 | M | R2 | ePRO compliance KPIs (% completion per subject / visit) shall feed the central monitoring dashboard. |
| URS-INT-EPRO-03 | M | R2 | ePRO instrument version (e.g., EORTC QLQ-C30 v3.0) shall be pinned per study; mid-study version change follows URS-BUILD-04. |

### 5.22 Integrations — LIMS (Bioanalytical / PK)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-LIMS-01 | M | R2 | Bioanalytical PK / PD data from the Watson LIMS (Cetus Pharmacology) shall be ingested via CDISC LAB / ODM-XML; sample-id ↔ subject-id ↔ visit-id reconciled. |
| URS-INT-LIMS-02 | M | R2 | LIMS reports flagged as "preliminary" shall not be locked into EDC until confirmation status is received from the LIMS. |

### 5.23 Integrations — SSO (Okta)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-SSO-01 | H | R1 | Authentication shall be via Okta SAML 2.0 + MFA; Rave local accounts disabled in production. |
| URS-INT-SSO-02 | M | R2 | Per-study access shall be provisioned via Okta groups mapped to Rave roles + country / site scopes; deprovisioning on HR termination shall be ≤ 24 h. |

### 5.24 Mid-Study Amendment Workflow (Re-validation + Re-consent)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AMD-01 | H | R1 | Each protocol amendment shall trigger a documented impact assessment covering eCRFs, edit checks, derivations, visit schedule, SDV plan, RBM plan, and consent text. |
| URS-AMD-02 | H | R1 | Mid-study CRF changes shall not be deployed without re-validation per URS-BUILD-04; silent CRF changes without re-validation are forbidden. |
| URS-AMD-03 | H | R1 | If the amendment affects subject rights / safety / risk-benefit, the system shall trigger a re-consent workflow (URS-CONSENT-*); subject status shall be "re-consent-pending" until re-consent is captured. |
| URS-AMD-04 | M | R2 | Migration scripts for the amendment shall be validated in UAT against representative subject data with rollback evidence. |

### 5.25 eConsent and Re-Consent

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CONSENT-01 | H | R1 | The system shall capture electronic informed consent per FDA *Use of Electronic Informed Consent — Questions and Answers* and 21 CFR Parts 11, 50, 56; eIC contains all elements required by 21 CFR § 50.25. |
| URS-CONSENT-02 | H | R1 | Re-consent events triggered by protocol amendments (URS-AMD-03) shall be tracked per subject with consent-version, signed-at timestamp, signer (subject + investigator), and IRB / EC approval reference. |
| URS-CONSENT-03 | H | R1 | A subject without current-version consent shall not be enrolled in protocol activities under the new amendment; the system shall block data entry on amendment-affected forms until re-consent. |
| URS-CONSENT-04 | M | R2 | Withdrawal-of-consent shall be captured with effective-date and scope (full withdrawal / data-only / future-data-only) per ICH E6(R3) and EU CTR Art. 28(3). |

### 5.26 Protocol Deviation Tracking

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEV-01 | H | R1 | Protocol deviations shall be recorded per ICH E6(R3) (§ 5 / § 6 Investigator obligations) with deviation-id, subject-id, deviation-category, date-occurred, date-identified, description, root-cause, corrective action, importance (Important / Non-Important). |
| URS-DEV-02 | H | R1 | Important Protocol Deviations (IPDs) shall trigger Medical Monitor review and an entry in the CTMS deviation register (cross-link to Dryad CTMS URS-DEV-*). |
| URS-DEV-03 | M | R2 | Deviation KPIs (rate per site, rate per subject, IPD rate) shall feed the RBM data feed. |

### 5.27 DSMB / IDMC Interim Analysis Support

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DSMB-01 | H | R1 | The system shall support DSMB / IDMC interim-analysis dataset extraction via a firewalled extract path that prevents unblinded data from reaching the unblinded study-conduct team. |
| URS-DSMB-02 | H | R1 | Closed-report (unblinded) and open-report (blinded) DSMB datasets shall be separately generated per the DSMB charter; access lists shall be SoD-enforced (DSMB statistician ≠ any study-conduct role). |
| URS-DSMB-03 | M | R2 | Each DSMB extract shall produce a manifest (data-cut date, included subjects, included forms, version hash) filed in eTMF. |
| URS-DSMB-04 | M | R2 | Adaptive-design adaptations decided by the DSMB shall be implementable via the mid-study amendment workflow (URS-AMD-*); the system shall not auto-adapt. |

### 5.28 CTIS / EU CTR Submission Pack

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CTIS-01 | H | R1 | The system shall produce data extracts supporting CTIS sponsor obligations under EU CTR 536/2014 (Annual Safety Report; substantial-modification submissions; end-of-trial summary). |
| URS-CTIS-02 | H | R1 | SUSAR-related data extracts shall route through PV to EudraVigilance (Argus is the regulatory submitter; EDC is the source of investigator-reported SAE data). |
| URS-CTIS-03 | M | R2 | Multi-country trial extracts shall respect per-country data-protection carve-outs; BfArM + PEI national obligations shall be supportable for DE trials. |

### 5.29 ICH E9(R1) Estimand-Supporting Data Integrity

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-EST-01 | H | R1 | The system shall capture intercurrent events (per ICH E9(R1)) sufficient to operationalise the protocol's estimand strategies (treatment policy, hypothetical, composite, while-on-treatment, principal-stratum) — e.g., dose discontinuation, rescue medication, death-pre-outcome. |
| URS-EST-02 | M | R2 | The audit trail shall preserve the original baseline-cohort assignment such that retroactive re-classification of intercurrent events for analysis does not corrupt the source observation record. |

### 5.30 Performance / Availability / Backup

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | eCRF page load ≤ 3 s at the 95th percentile under nominal study load (≤ 200 concurrent users per study at peak). |
| URS-PERF-02 | M | R2 | SDTM export job for a 500-subject Phase II study ≤ 30 min wall-clock. |
| URS-AV-01 | H | R1 | Site availability target shall align with Medidata's published SLA (99.5% monthly); deviations escalated. |
| URS-BAK-01 | H | R1 | Vendor-managed backup; site verifies vendor-published RPO ≤ 4 h, RTO ≤ 24 h via vendor-assurance program. |
| URS-BAK-02 | M | R2 | Site exports a study-build configuration archive to eTMF on each major milestone (FPI, LPLV, hard-lock). |
| URS-BAK-03 | M | R2 | Disaster-recovery drill shall be evidenced annually by vendor and reviewed by Marigold vendor-assurance program. |

### 5.31 Security and Data Protection (GDPR + HIPAA)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | Authentication via Okta SAML 2.0 + MFA; session timeout ≤ 30 min idle; re-authentication at signature events. |
| URS-SEC-02 | H | R1 | Per-study access restricted by role and country / site; access reviewed at FPI, every 90 days during enrolment, and at LPLV. |
| URS-SEC-03 | H | R1 | Subject identifiers in eCRF shall be minimised per the protocol's data-protection plan (no direct identifiers in eCRF where prohibited); GDPR Art. 9 special-category controls applied. |
| URS-SEC-04 | H | R1 | GDPR Art. 22 — no automated individual decision-making against the subject shall be implemented in EDC; any automated classification (e.g., risk scoring) shall be flagged for human review before any downstream action. |
| URS-SEC-05 | H | R1 | GDPR Art. 32 — encryption at rest (AES-256) + in transit (TLS 1.3); vendor evidence reviewed annually. |
| URS-SEC-06 | H | R1 | GDPR Art. 35 — a per-study Data Protection Impact Assessment (DPIA) shall be conducted before FPI for studies involving special-category data (Art. 9); DPIA outcomes drive eCRF minimisation and access controls. |
| URS-SEC-07 | M | R2 | HIPAA-covered studies (US sites) shall apply the Vendor BAA controls; PHI-handling per the per-study HIPAA-authorisation. |
| URS-SEC-08 | M | R2 | Subject-erasure requests (GDPR Art. 17) shall be triaged against the EU CTR research-record-retention carve-out; documented justification for retention shall be filed where erasure is refused. |

### 5.32 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Production access shall require recorded role-specific training (LMS) plus protocol-specific training; expired training shall block access. |
| URS-TRN-02 | M | R2 | New-version-training shall be assigned automatically when the user-manual version advances or a Quick-Publish changes the user-visible behaviour. |
| URS-PR-01 | H | R1 | Annual periodic review at the platform level; per-study review at protocol amendments and at database lock; signed by Director CDM and VP Clinical Operations. |
| URS-PR-02 | M | R2 | Periodic review shall confirm the RBM feed health, audit-trail completeness, vendor-release impact assessments, and SAE-reconciliation status. |

### 5.33 FDA BIMO / EMA / BfArM Inspection-Readiness

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BIMO-01 | H | R1 | Per FDA BIMO Inspection Manual 7348.809 (updated 4 April 2025) and EMA / BfArM inspection expectations, the system shall produce on-demand: full audit trail per subject; query history per subject; signature history per subject; eCRF state at lock; SAE reconciliation evidence; coding decisions; protocol-deviation register. |
| URS-BIMO-02 | H | R1 | Inspector / auditor role shall be export-only, read-only across the full data + audit trail of the study under inspection; no edit / no signature affordances. |
| URS-BIMO-03 | M | R2 | Inspection-bundle export shall be generable in ≤ 60 min wall-clock for a 500-subject Phase II study. |

### 5.34 Multi-Language Site Activation and Time-Zone-Aware Visit Calc

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INTL-01 | M | R2 | eCRF labels and instructional text shall be localisable per site language (de-DE, de-AT, de-CH, fr-FR, en-GB, en-US, es-ES, it-IT, pl-PL, cs-CZ) without changing the underlying field semantics. |
| URS-INTL-02 | M | R2 | The visit-window calculator shall be time-zone-aware: subject's local time-zone shall be the basis for visit-window enforcement; the underlying stored timestamps shall be UTC (per URS-DATA-05). |
| URS-INTL-03 | M | R2 | Locale-specific date / number / unit display shall not corrupt the stored canonical values. |

### 5.35 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is SAML 2.0 via Entra ID with SCIM lifecycle provisioning; conditional-access policy `Clinical-Sensitive Conditional Access (FIDO2 phishing-resistant MFA + sponsor-tenant isolation)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with Oracle RMAN for the Medidata Rave Oracle backend; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 25 y per ICH E6(R3) per the consuming-record schedule. |

### 5.36 Cross-System Integration — Hydra protocol drafting + Helios

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HYD-01 | M | R2 | When the Marigold protocol-drafting GenAI feature is enabled (opt-in per sponsor-study), the feature shall invoke the Hydra GenAI Gateway (`HYD2-URS-GENAI-001`) exclusively; direct vendor-LLM calls shall be prohibited at the egress firewall. |
| URS-XINT-HYD-02 | H | R1 | Protocol-drafting use cases shall pass the Hydra per-use-case classification gate; sponsor-study-specific use cases shall be declared conditionally Annex I where the drafted protocol participates in a regulated dossier (clinical trial application); Art. 11 + Annex IV pack required when so declared. |
| URS-XINT-HYD-03 | H | R1 | Every GenAI-drafted protocol section inserted into a study shall carry the Hydra watermark + provenance metadata and shall require Medical Monitor + Biostatistician dual approval before study activation. |
| URS-XINT-HYD-04 | M | R2 | Inference events shall be forwarded to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract within 5 minutes. |

### 5.37 Cross-System Integration — Helios audit-trail handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HEL-01 | H | R1 | Medidata Rave EDC shall publish audit-trail events (Subject visit, form / question, query lifecycle, source-data verification, and protocol-deviation events) to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract (JSON Lines, schema-registry pinned, Kafka topic `helios.ingest.marigold.rave.v1`) within 5 minutes of event capture; 21 CFR § 11.10(e) audit-trail completeness shall be preserved end-to-end so that no event class is lost at the boundary. |
| URS-XINT-HEL-02 | H | R1 | Pre-handover audit-trail retention on the Medidata Rave EDC side shall be ≥ 25 y regardless of Helios availability; once Helios acknowledges ingest (per-message ack with idempotency key), Helios is the system-of-record for review and the Medidata Rave EDC local copy serves as the durability backstop until the local retention floor expires. |

### 5.38 Cross-System Integration — LMS competence handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-LMS-01 | H | R1 | Clinical-team members (Investigator, CRC, Data Manager, Monitor) shall pass an LMS competence check (curriculum `EDC-<role>-<study_id>`) before being assigned to a study at a site; LMS competence shall be re-checked at every site activation and at every protocol-amendment activation. |

## 6. Acceptance Criteria

The platform-level configuration enters validated use when **CS, RA, IQ** (per Medidata customer-shared evidence), **OQ** (signature, audit trail, integration, configuration, RBM feed, CTIS pack, DSMB extract, eConsent, ePRO ingest), **PQ** (representative end-to-end study build through subject data, query workflow, mid-study amendment, lock, export, SDTM + Define-XML round-trip) approved and executed; vendor-assurance evidence reviewed and accepted; **VSR** approved by Director CDM and VP QA; **RTM** demonstrates 100% URS-ID coverage. Each per-study build separately validated against this URS via study-specific protocols (`MAR-CSV-EDC-STUDY-NNN`).

## 7. Constraints

- Vendor releases quarterly per Medidata's 2024.x release train; vendor SDLC not under site change control.
- Per-study free-form custom-function scripting prohibited in production without a Cat-5 sub-component RA.
- Configuration baselines re-tested per quarterly release impact-assessment.
- CTIS gateway operated by the sponsor's regulatory affairs function — EDC is the data source, not the submitter.
- Argus is the SUSAR submission system of record; EDC is the source of investigator-reported SAEs.
- DSMB / IDMC processes are governed by the per-study DSMB charter; the EDC implements the data-feed boundary, not the DSMB decision logic.

## 8. Assumptions

- Okta, Medidata Coder, RTSM / IXRS, eTMF (Marinos), Argus, Iolanthe ePRO, Watson LIMS, central labs (LabCorp / Q² Solutions / Eurofins), imaging core lab, BfArM + PEI gateways, and CTIS are themselves validated under their own URS / vendor-assurance programs.
- Per-study DSMB charters, RBM plans, monitoring plans, eConsent IRB approvals, and DPIAs are in place before FPI.
- The sponsor's pharmacovigilance function owns the regulatory clock for SUSAR reporting; the EDC's role is sponsor-awareness propagation, not regulatory submission.
- BfArM and PEI national-CA gateways for DE trials are operated separately and consume CTIS-exported pack content.

## 9. References

### Jurisdiction — US (FDA)

- 21 CFR Part 11 §§ .10(a)–(k), .30, .50, .70, .100, .200, .300 — Electronic Records; Electronic Signatures
- 21 CFR Part 50 — Protection of Human Subjects (informed consent: § 50.25)
- 21 CFR Part 56 — Institutional Review Boards
- 21 CFR Part 312 — IND Applications (Form FDA 1572 per § 312.53(c))
- 21 CFR Part 314 — NDA Applications
- FDA *Computerized Systems Used in Clinical Investigations* (May 2007)
- FDA *Electronic Source Data in Clinical Investigations* (Sep 2013)
- FDA *Use of Electronic Informed Consent in Clinical Investigations — Questions and Answers* (final)
- FDA *Establishment and Operation of Clinical Trial Data Monitoring Committees* (current guidance, plus 2024 draft update)
- FDA BIMO Inspection Manual 7348.809 (updated 4 April 2025)
- FDA *Bioresearch Monitoring Program* (CBER + CDER)

### Jurisdiction — EU (EMA / European Commission)

- EU CTR Regulation (EU) No 536/2014 + CTIS Sponsor Handbook
- EU GMP Annex 11 §§ 4, 6, 9, 11 (Computerised Systems)
- EMA *Guideline on Computerised Systems and Electronic Data in Clinical Trials* (2023)
- GDPR Regulation (EU) 2016/679 — Arts. 6, 9, 17, 22, 32, 33, 35
- EU Pharmacovigilance Directive 2010/84/EU + Regulation 1235/2010

### Jurisdiction — International (ICH)

- ICH E6(R3) GCP (Step 4, adopted 6 January 2025)
- ICH E8(R1) General Considerations for Clinical Studies (Step 4, October 2021)
- ICH E9(R1) Statistical Principles for Clinical Trials: Addendum on Estimands and Sensitivity Analysis (Step 4, November 2019)
- ICH E2A Clinical Safety Data Management: Definitions and Standards for Expedited Reporting
- ICH E2B(R3) Electronic Transmission of Individual Case Safety Reports
- ICH M11 Clinical Electronic Structured Harmonised Protocol (CeSHaRP)

### CDISC Standards

- CDISC SDTM-IG v3.4 (or current per study); SDTM v2.0
- CDISC ADaM-IG v1.3
- CDISC CDASH-IG v2.3
- CDISC ODM-XML v1.3.2
- CDISC Define-XML v2.1
- CDISC Controlled Terminology (per release package, NCI-EVS pinned)
- CDISC Dataset-JSON v1.0 (FDA pilot)

### Industry Guidance (ISPE / PIC/S / ISO)

- ISPE GAMP 5 (2nd Edition, 2022)
- ISPE GAMP Good Practice Guide *Computerised Systems in Regulated GCP Environments*
- ISPE GAMP Good Practice Guide *Records and Data Integrity*
- PIC/S PI 041 — Good Practices for Data Management and Integrity
- ISO/IEC 27001:2022 — Information Security Management
- ISO 14155:2020 — Clinical investigation of medical devices

### DACH

- BfArM — Federal Institute for Drugs and Medical Devices (medicinal products + medical devices)
- Paul-Ehrlich-Institut (PEI) — biologicals + vaccines
- Anlage 7 GMP-Inspektion (DE) — inspection annex
- Swissmedic (CH) — Therapeutic Products Authority
- AGES PharmMed (AT)
- CTIS — Clinical Trials Information System (EU-level submission portal)
- EudraVigilance — pharmacovigilance database

### Vendor

- Medidata — *Rave EDC 2024 Validation Approach* (vendor white paper); Medidata Trust portal; Rave Architect Essentials documentation
- Medidata — *Rave EDC 2024.2.0 Release Notes* (vendor portal)
- Medidata Coder — MedDRA + WHODrug coding module documentation
- Medidata RTSM / IXRS-class — randomisation + supply documentation

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

