---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "GAMP 5 (2nd Ed., 2022) Cat 3 conventions for non-configured products"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "ICH Q8(R2); ICH Q9(R1); ICH Q10; ICH Q12"
  - "FDA Process Validation Guidance (2011) — Stage 3 Continued Process Verification"
  - "ASTM E2587 Practice for Use of Control Charts; ISO 7870 (parts 1-9)"
  - "USP <1010> Analytical Data Interpretation"
  - "PIC/S PI 041; ISPE GPG Validation of Computerized Systems in API and Drug Product Manufacturing"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## SPC — JMP Statistical Discovery 18 Pro

**Document Number:** CRN-URS-SPC-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Carina Pharmaceuticals SA, Process Sciences, Buenos Aires, Argentina *(fictional)*
**System Owner:** Process Sciences Lead | **Process Owner:** Head of Manufacturing Sciences
**System Class (GAMP 5, 2nd ed.):** Category 3 — Non-Configured Product (commercial statistical software used out-of-the-box; site-authored JSL scripts assessed as Cat-5 sub-components when used)
**Project Mode:** Configuration project on non-configurable instrument / appliance **JMP Statistical Discovery 18 Pro** (GAMP 5 Category 3 — Non-Configurable COTS).
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; ICH Q8(R2); ICH Q9(R1); ICH Q10; ICH Q12; FDA *Process Validation: General Principles and Practices* (2011) — Stage 3 Continued Process Verification

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Process Sciences Lead) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Statistician) | _____________ | _____________ | _____ |
| Approver (Head of Manufacturing Sciences) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | v1.2 enrichment: tiered to T2 (50-80 reqs; this URS lands at 55 reqs); explicit § 5 modules for control-chart catalogue, capability indices (Cp/Cpk/Pp/Ppk + ISO 22514-2), OOC/OOT rules (Western Electric + Nelson + custom), batch genealogy linkage, real-time SPC alerts, Phase-1 vs Phase-2 workflow. Modernised references per METHODOLOGY § 2A.1; risks expanded. |

## Definitions

| Term | Definition |
|---|---|
| SPC | Statistical Process Control |
| JMP | JMP Statistical Discovery 18 Pro by SAS Institute |
| JSL | JMP Scripting Language |
| CPV | Continued Process Verification (FDA Process Validation Stage 3) |
| Cp / Cpk | Process capability indices (within-batch) |
| Pp / Ppk | Process performance indices (overall, including between-batch variance) |
| Phase 1 / Phase 2 | Chart-establishment phase / monitoring phase per ASTM E2587 |
| Western Electric Rules | Four rules for detecting non-random patterns on Shewhart charts |
| Nelson Rules | Eight rules extending Western Electric coverage |
| MES | Werum PAS-X v3.2 |
| LIMS | LabWare LIMS 8 |
| Data Lakehouse | Site analytics platform (Databricks on Azure) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

Define requirements for the SPC platform used by Process Sciences to perform Stage-3 CPV trending, capability + performance analysis, OOC / OOT detection, real-time SPC alerts, and batch-genealogy investigations across commercial products at Carina Pharmaceuticals. The system supports continuous process verification per FDA's 2011 Process Validation guidance and the lifecycle approach to control strategy per ICH Q8/Q9/Q10/Q12.

## 2. Scope

**In:** JMP Statistical Discovery 18 Pro (concurrent-licensed installations on a controlled set of analyst workstations); the controlled JSL script library managed under Cat-5 sub-component change control; the Vault-managed CPV report templates; data feeds from the site Data Lakehouse (Databricks) aggregating MES + LIMS + EM data; the real-time SPC consumer of selected critical attributes via the AVEVA PI System; batch-genealogy linkage via the lakehouse genealogy schema.

**Out:** the data lakehouse pipeline (separate validation `LAKE-CSV-2024-005`); MES / LIMS / EM / PI source systems (per-system URSs); ad-hoc / exploratory analyses outside the controlled CPV process.

## 3. System Description

JMP is used to compute statistical summaries (control charts, capability + performance indices, mixed-effects models, regression) on data drawn from the site lakehouse. CPV reports are produced periodically per product / process and signed off as part of the Quality System. The system supports a Phase 1 workflow (chart establishment using historical reference batches) followed by a Phase 2 workflow (ongoing monitoring against established limits). Real-time SPC consumption of selected attributes uses the AVEVA PI System Notification engine forwarding excursions to MES + eQMS.

GAMP Category 3 — JMP is a vendor-supplied statistical product deployed without configuration. Site-authored JSL scripts that automate CPV calculations are treated as Cat-5 sub-components under separate change control.

## 4. User Roles

| Role | Permissions |
|---|---|
| Process Sciences Analyst | Run controlled JSL scripts; produce signed CPV reports; investigate OOC / OOT. |
| Senior Analyst | Second-person review of CPV report inputs + chart-rule firings. |
| JSL Script Author (Quality IT) | Author / modify JSL under Cat-5 SDLC. |
| JSL Script Approver (QA + Process Sciences Lead) | Co-approve script releases. |
| Statistician | Approve Phase 1 → Phase 2 transitions; approve capability-method choices. |
| CPV Report Approver (Head of Manufacturing Sciences + Head of QA) | Co-approve CPV reports. |
| System Administrator | JMP installation, licensing, AD groups; cannot approve. |
| Auditor | Read-only across script library and CPV report archive. |

Separation of duties: JSL Author ≠ Approver; CPV Analyst ≠ CPV Approver; Statistician ≠ Author of the JSL being approved.

## 5. User Requirements

### 5.1 JMP Deployment / Configuration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEP-01 | H | R1 | JMP installations shall reside on a controlled set of analyst workstations under the site asset register. |
| URS-DEP-02 | H | R1 | JMP version shall be fixed for a given CPV programme; major version upgrades shall follow change control + revalidation of affected JSL scripts. |
| URS-DEP-03 | H | R1 | Workstation Group Policy shall disable Office macros (already enforced at the site); JMP add-ins shall be restricted to the approved JSL script library. |

### 5.2 JSL Script Library (Cat-5 Sub-component)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-JSL-01 | H | R1 | JSL scripts shall be under version control with signed commits; releases shall be reviewed and approved per the SDLC. |
| URS-JSL-02 | H | R1 | Each script shall have a Model Card: intended use, inputs, outputs, statistical assumptions, validation evidence, known limitations. |
| URS-JSL-03 | H | R1 | Scripts shall be cryptographically signed (cosign-equivalent for JSL); signature shall be verified before execution. |
| URS-JSL-04 | H | R1 | Unit tests shall exist with reference inputs and expected outputs; CI shall verify test pass before release. |
| URS-JSL-05 | H | R1 | Script execution shall log inputs, parameters, outputs, version, executor, timestamp to the JMP audit log + SIEM. |

### 5.3 Control Chart Catalogue

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CHT-01 | H | R1 | The system shall support Shewhart charts: X̄-R, X̄-s, I-MR for variables data; p-, np-, c-, u- for attributes data per ISO 7870 parts 2 + 8. |
| URS-CHT-02 | H | R1 | The system shall support time-weighted charts EWMA (default λ = 0.2) and CUSUM (default h = 4σ, k = 0.5σ) for slow-drift detection per ISO 7870 parts 4 + 6. |
| URS-CHT-03 | H | R1 | The system shall support multivariate charts (Hotelling T², MEWMA) for correlated CQAs / CPPs. |
| URS-CHT-04 | H | R1 | Chart selection per attribute shall be documented per a chart-decision register (variable type, subgroup structure, autocorrelation considerations); chart-rule activation shall require QA approval. |

### 5.4 Capability + Performance Indices

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CAP-01 | H | R1 | The system shall compute Cp, Cpk (within-batch), Pp, Ppk (overall) per ISO 22514-2; the normality assumption shall be tested (Anderson–Darling); on non-normal distribution Box–Cox transform or non-parametric (Clements) method shall be selected per attribute config. |
| URS-CAP-02 | H | R1 | Capability indices computed on n < 30 shall be flagged "indicative only — small-sample"; n < 10 shall be suppressed and reported as `INSUFFICIENT_N`. |
| URS-CAP-03 | H | R1 | The Cp / Cpk vs Pp / Ppk distinction shall be rendered explicitly in every CPV report; within-batch vs overall variance contributions shall be visualised. |
| URS-CAP-04 | M | R2 | Confidence intervals on Cpk / Ppk shall be reported at 95 % (Bissell approximation). |

### 5.5 OOC / OOT Detection Rules

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-OOC-01 | H | R1 | Western Electric Rules 1–4 shall be implementable per attribute: Rule 1 (1 pt > 3σ), Rule 2 (2 of 3 > 2σ same side), Rule 3 (4 of 5 > 1σ same side), Rule 4 (8 in a row same side of centerline). |
| URS-OOC-02 | H | R1 | Nelson Rules 1–8 shall be implementable per attribute (extension of Western Electric); rule activation shall be configurable per attribute. |
| URS-OOC-03 | H | R1 | Custom site-specific rules (e.g., 3-of-3 above warning limit on the same shift) shall be supported with statistician approval. |
| URS-OOC-04 | H | R1 | Rule firings shall record (batch_id, attribute, rule_no, ruleset, timestamp, value) and shall route to eQMS deviation via REST. |
| URS-OOC-05 | M | R2 | The system shall report false-alarm rate per ruleset (e.g., All-Western-Electric rules ≈ ARL₀ 91 vs Rule-1-only ≈ 370); rulesets with ARL₀ < 30 shall require statistician sign-off. |

### 5.6 Phase 1 vs Phase 2 Workflow

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PH-01 | H | R1 | Phase 1 (chart-establishment) shall use ≥ 20–25 reference batches (per ASTM E2587) to compute trial control limits + capability baseline; Phase 1 output shall require statistician + QA approval. |
| URS-PH-02 | H | R1 | Phase 1 → Phase 2 transition shall lock the control limits + capability baseline; any subsequent change shall require change control + statistician approval. |
| URS-PH-03 | H | R1 | Phase 2 (monitoring) shall apply locked limits + ruleset; out-of-control conditions in Phase 2 shall trigger OOC/OOT investigations. |
| URS-PH-04 | M | R2 | Limit revision in Phase 2 (e.g., after a documented process improvement reducing variance) shall require ≥ 20 post-change batches + statistician approval. |

### 5.7 Batch Genealogy Linkage

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-GEN-01 | H | R1 | Every CPV record shall link to its parent batch genealogy via the lakehouse genealogy schema (raw materials → intermediates → final batch → market). |
| URS-GEN-02 | H | R1 | OOC / OOT firings shall be traceable to: process step, equipment train, raw-material lot, operator, environmental condition (where captured). |
| URS-GEN-03 | M | R2 | Genealogy-based "trace forward" shall enumerate all batches potentially affected by a discovered root cause (e.g., a defective raw-material lot). |

### 5.8 Real-Time SPC Alerts

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RT-01 | H | R1 | Selected critical attributes (per the CPV control strategy) shall be subscribed to the AVEVA PI System Notification engine; alerts shall fire within 60 s of detection. |
| URS-RT-02 | H | R1 | Real-time alerts shall route to MES + eQMS + Process Engineering on-call; eQMS deviation creation shall be idempotent. |
| URS-RT-03 | M | R2 | The real-time engine shall provide alert acknowledgement + suppression workflow with statistician review of suppression patterns. |

### 5.9 CPV Workflow

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CPV-01 | H | R1 | CPV reports shall be produced per product / process at the configured cadence (e.g., quarterly). |
| URS-CPV-02 | H | R1 | Inputs to CPV reports shall be drawn from the lakehouse via documented queries; queries shall be version-controlled and signed by data engineering. |
| URS-CPV-03 | H | R1 | The CPV report shall include: control charts (per chart-decision register), capability indices (Cp / Cpk / Pp / Ppk), trend evaluations, OOC / OOT investigations cross-referenced from eQMS, batch-genealogy summary, change-control summary. |
| URS-CPV-04 | H | R1 | CPV report shall be signed by CPV Analyst, Senior Analyst, Statistician, and approved by Head of Manufacturing Sciences + Head of QA. |
| URS-CPV-05 | M | R2 | CPV report shall be archived in Veeva Vault QualityDocs. |

### 5.10 Audit Trail / 21 CFR Part 11 / DI

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Lakehouse query execution shall be logged with timestamp, user, query version. |
| URS-AUD-02 | H | R1 | JSL execution shall be logged in a controlled JMP-add-in audit log forwarded to SIEM. |
| URS-AUD-03 | H | R1 | CPV reports' signatures shall be captured in Vault audit trail (append-only). |
| URS-AUD-04 | H | R1 | Retention ≥ 25 years for CPV reports. |
| URS-PART11-50 | H | R1 | E-signatures (in Vault) per § 11.50. |
| URS-PART11-100 | H | R1 | Unique signatures per § 11.100. |
| URS-PART11-200 | H | R1 | Re-authentication at Vault signing per § 11.200. |
| URS-DI-01 | H | R1 | Records Attributable. |
| URS-DI-04 | H | R1 | Lakehouse source data immutable; CPV report references query version + execution timestamp for reproducibility. |
| URS-DI-05 | H | R1 | Statistical outputs Accurate per OQ on reference datasets per ASTM E2587 examples + AIAG SPC reference. |

### 5.11 Integrations / Performance / Security / Training / PR

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-LAKE-01 | H | R1 | Lakehouse data access via authenticated, audited queries; service accounts via vault. |
| URS-INT-VAULT-01 | M | R2 | CPV reports filed in Vault QualityDocs. |
| URS-INT-EQMS-01 | H | R1 | OOC / OOT firings push to MasterControl eQMS via REST (idempotent on rule-violation-id). |
| URS-INT-PI-01 | H | R1 | Real-time consumer of selected attributes via AVEVA PI System Notification (KYM-URS-HIST-001 cross-reference). |
| URS-INT-MES-01 | M | R2 | Real-time alerts forwarded to PAS-X MES Production Alarms. |
| URS-INT-APR-01 | M | R2 | Read-only CPV summary endpoint consumed by APR / PQR tool (MIR-URS-APR-001). |
| URS-PERF-01 | L | R3 | A typical CPV report shall run in ≤ 15 minutes wall-clock on a baseline workstation. |
| URS-SEC-01 | H | R1 | Domain accounts only. |
| URS-TRN-01 | H | R1 | LMS-recorded role-specific training; CPV Analysts shall complete statistician-curated SPC competency assessment. |
| URS-PR-01 | H | R1 | Annual periodic review covering JSL script library, OOC / OOT trends, CPV-report cadence, false-alarm rate per ruleset, real-time alert suppression patterns, training; signed by Process Sciences Lead + Head of QA. |

### 5.12 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem; conditional-access policy `Quality-App Conditional Access (MFA on first logon per session)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the SPC mart DB; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 15 y (process-control record) per the consuming-record schedule. |

### 5.13 Cross-System Integration — eQMS CAPA handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-EQMS-01 | H | R1 | On detection of SPC rule-violation (trigger: Western Electric / Nelson rule violation, control-limit exceedance, capability drop), the system shall push a CAPA-ticket creation event to the Talos MasterControl eQMS (`TLB-URS-EQMS-001`) via the eQMS event-push channel with required metadata {originating_system, originating_record_id, finding_class, severity, evidence_package_uri, detection_ts_utc, detection_user, regulatory_basis}; severity per SPC procedure; CpK < 1.33 → major. |
| URS-XINT-EQMS-02 | H | R1 | The eQMS ticket-creation call shall be idempotent on `{originating_system, originating_record_id, finding_class}`; the eQMS status-callback shall be ingested and reflected on the originating record with a hyperlink to the eQMS ticket; closed-loop verification per ICH Q9(R1) + ICH Q10 shall be evidenced before the originating record is dispositioned. |

## 6. Acceptance Criteria

CS (configuration of JMP install + JSL library), RA, IQ, OQ (calculation verification on reference datasets including the AIAG SPC reference + ASTM E2587 examples), PQ (representative CPV report end-to-end through query → JSL → JMP → Vault → signature; plus representative Phase 1 → Phase 2 transition; plus representative real-time alert firing) approved and executed; VSR approved; RTM maps every URS-ID to ≥ 1 approved test case.

## 7. Constraints

- JSL script changes follow Cat-5 SDLC.
- Major JMP upgrades follow change control.
- Real-time alerts piggy-back on PI Notification infrastructure (separate URS).

## 8. Assumptions

- Lakehouse, Vault, AD, PI System are validated.
- Reference datasets exist for OQ.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200
- 21 CFR Part 211 §§ .68, .192
- FDA *Process Validation: General Principles and Practices* (2011) — Stage 3 CPV
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EU GMP Annex 15 — Qualification and Validation

### International — ICH
- ICH Q8(R2) — Pharmaceutical Development
- ICH Q9(R1) — Quality Risk Management
- ICH Q10 — Pharmaceutical Quality System
- ICH Q12 — Lifecycle Management

### Industry / ISO / ASTM / USP
- ISPE GAMP 5 (2nd Ed., 2022) — Cat 3 conventions
- ISPE GAMP Good Practice Guide *Validation of Computerized Systems Used in Manufacturing of API and Drug Product*
- ASTM E2587-22 — Standard Practice for Use of Control Charts in Statistical Process Control
- ISO 7870-1:2019 — Control charts (overview)
- ISO 7870-2:2023 — Shewhart control charts
- ISO 7870-4:2021 — Cumulative sum charts (CUSUM)
- ISO 7870-6:2016 — EWMA control charts
- ISO 7870-8:2017 — Charting techniques for short runs and small mixed batches
- ISO 22514-2:2017 — Capability and performance — Time-dependent process models
- USP <1010> Analytical Data — Interpretation and Treatment
- PIC/S PI 041 — Good Practices for Data Management and Integrity

### Vendor
- SAS Institute — *JMP 18 Pro Reference*
- AVEVA PI System 2024 (cross-reference KYM-URS-HIST-001)

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

