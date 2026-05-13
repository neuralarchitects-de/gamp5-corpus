---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-27; expanded 2026-05-12 (T3 floor uplift: protocol authoring per-module, execution capture with handhelds + offline + e-sig, deviation lifecycle per execution, RTM auto-gen + completeness gate, CSV training + certification, GitLab + Vault + eQMS integration, multi-site federation; FDA CSA Feb 2026 citation fix)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed., 2022) Cat 4 SaaS conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11 (Computerised Systems) §§ 4, 6, 9, 11; EU GMP Chapter 4 (Documentation)"
  - "ICH Q9(R1) Quality Risk Management"
  - "ICH Q10 Pharmaceutical Quality System"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026; supersedes the September 2025 guidance)"
  - "ISPE GAMP 5 (2nd Edition, 2022) — Risk-Based Approach"
  - "ISPE GAMP Good Practice Guide: Records and Data Integrity"
  - "ISPE Validation Master Plan Guide"
  - "PIC/S PI 041 Good Practices for Data Management and Integrity"
  - "BfArM (DE) Anlage 7 GMP-Inspektion; Swissmedic (CH) inspection guidance"
  - "ValGenesis VLM 5.x — Validation Approach and Customer-Shared CSV Summary"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Validation Lifecycle Management (VLM) — ValGenesis VLM 5.x

**Document Number:** CYG-URS-VLM-001
**Version:** 1.2
**Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Cygnus Pharma AG, Global Validation Operations, Konstanz, Germany *(fictional)*
**System Owner:** Director, Validation Operations
**Process Owner:** VP Quality Assurance
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Project Mode:** Configuration project on commercial software product **ValGenesis VLM 5.x** (GAMP 5 Category 4 — Configured Product).
**FDA CSA classification:** Critical system — supports manufacturing-quality-system validation portfolio; CSA risk-based testing applies per FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Chapter 4; ICH Q9(R1); ICH Q10; FDA CSA (Feb 2026 final); ISPE GAMP 5 (2nd ed., 2022); ISPE GAMP GPG *A Risk-Based Approach to Compliant Computerised Systems*; PIC/S PI 041; BfArM (DE) Anlage 7; Swissmedic (CH).

> **Note:** This system is a "validation of validation" platform — it manages CSV documents (URS, FS, RTM, IQ, OQ, PQ protocols + execution) and the validation lifecycle for other GxP systems. Therefore it is itself validated rigorously. The system supports the FDA CSA (Feb 2026) risk-based-testing paradigm: testing depth scales to system risk and intended use, not to a one-size-fits-all template.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Validation Operations) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Vendor Assurance — ValGenesis owner) | _____________ | _____________ | _____ |
| Reviewer (FDA CSA Liaison) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |
| Approver (VP IT Compliance) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-12 | (synthetic) | §5 broken out into 12 subsections; DACH relocation (Konstanz, DE); FDA CSA explicit binding with risk-based-testing classification; ISPE GAMP 5 Risk-Based Approach + ICH Q9(R1) explicit; BfArM Anlage 7 + Swissmedic added; risk table expanded to 12 rows. |
| 1.2 | 2026-05-12 | (synthetic) | T3-floor uplift (~125 reqs): per-module protocol authoring (FS/CS/DS/IQ/OQ/PQ), execution capture (handhelds + offline + e-sig), deviation lifecycle per execution, RTM auto-gen + completeness gate, CSV training + certification, GitLab release-linked validation, multi-site federation, Vault + eQMS integration. FDA CSA citation corrected to Feb 2026 final. |

## Definitions

| Term | Definition |
|---|---|
| VLM | Validation Lifecycle Management |
| Protocol | IQ / OQ / PQ test protocol with steps + expected results |
| Execution | Witnessed execution of a protocol with attached evidence |
| Deviation | In-execution test failure with disposition |
| Project | A validation project encapsulating a system under validation |
| RTM | Requirements Traceability Matrix |
| VMP | Validation Master Plan |
| VSR | Validation Summary Report |
| CSA | Computer Software Assurance (FDA Feb 2026 final; supersedes Sep 2025) |
| RBA | Risk-Based Approach (per ISPE GAMP 5 + ICH Q9(R1)) |
| ALARP | As Low As Reasonably Practicable |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| FS / CS / DS | Functional / Configuration / Design Specification |
| Handheld | Tablet / phone used for in-room execution capture |

## 1. Purpose

This URS defines requirements for the VLM platform used to author, review, approve, execute, and archive CSV / CSA deliverables across Cygnus Pharma's GxP system portfolio in 5 production sites (Konstanz DE, Basel CH, Vienna AT, Boston MA, Singapore). The platform supports the FDA CSA (Feb 2026) risk-based-testing paradigm: testing depth scales to declared system risk + intended use, with documented critical-thinking justification.

## 2. Scope

**In:** ValGenesis VLM 5.x multi-tenant SaaS instance; per-project configuration (protocol templates, role matrices, risk-classification matrices); SSO via Okta + MFA; integrations with Vault QualityDocs (controlled-document references), the eQMS (deviation linkage), the application portfolio (system inventory + criticality classification), and validated GitLab (release-linked validation); per-module protocol authoring (FS, CS, DS, IQ, OQ, PQ); in-room execution via handhelds with offline + sync; multi-site federation across 5 sites; vendor-assurance program covering ValGenesis (SOC 2, ISO 27001, customer-shared CSV summary).

**Out:** vendor infrastructure (ValGenesis-managed); the validated systems themselves (each separately validated using artefacts authored in this VLM tool); regulatory submission of validation summaries (separate scope).

## 3. System Description

VLM is the system of record for CSV / CSA deliverables — URS, FS, CS, DS, RTM, IQ, OQ, PQ, VSR, VMP — across projects. Documents follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE; protocols are executed in-app or in-room via handhelds (with offline mode + sync) with electronic capture of step-by-step results, witness signatures, evidence attachments; deviations during execution route to the eQMS. Per-project RTMs are maintained automatically with broken-link detection. Risk-based-testing depth per FDA CSA (Feb 2026): the platform supports critical-thinking justification capture per requirement. Validation campaigns can be linked to specific GitLab release tags.

GAMP Cat 4: ValGenesis maintains the SDLC; site validates per-tenancy configuration, template inventory, integration boundaries, and Part 11 controls. ICH Q9(R1) risk-management methodology guides per-project risk classification.

## 4. User Roles

| Role | Permissions |
|---|---|
| Document Author | Create / edit DRAFT documents. |
| Reviewer | Review; cannot self-approve. |
| Approver (QA + System Owner) | Approve to EFFECTIVE. |
| Executor | Execute protocols; capture evidence. |
| Witness | Witness critical steps; cannot self-execute. |
| Project Lead | Manage project; assign roles; classify project risk per ICH Q9(R1). |
| Template Author | Create / edit protocol templates under change control. |
| Template Approver (QA) | Approve templates to EFFECTIVE. |
| Risk Classifier (CSA Liaison) | Classify each system per FDA CSA + GAMP 5 RBA; assign testing-depth tier. |
| Multi-Site Federation Steward | Authorise inter-site template + project transfer. |
| CSV Trainer | Author + deliver CSV training curricula. |
| Certification Officer | Issue role certifications (Executor, Witness, Risk Classifier). |
| VLM Administrator | Configure; cannot approve documents / executions. |
| Auditor | Read-only. |

Standard SoD: Author ≠ Reviewer ≠ Approver; Executor ≠ Witness; Template Author ≠ Template Approver; Risk Classifier ≠ Project Lead; CSV Trainer ≠ Certification Officer.

## 5. User Requirements

Each requirement carries a unique ID, priority, GAMP-5 risk classification, and a verifiable `shall`-clause.

### 5.1 Vendor Assurance and Configuration Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-01 | H | R1 | ValGenesis shall be qualified as a critical SaaS vendor with SOC 2 Type II + ISO 27001 + customer-shared CSV summary on file; annual re-qualification. |
| URS-VND-02 | H | R1 | Vendor releases shall be impact-assessed within 14 days of release notes publication. |
| URS-VND-03 | M | R2 | A vendor escalation runbook with named ValGenesis contacts shall be on file. |
| URS-CFG-01 | H | R1 | Per-tenancy and per-project configuration shall follow DEV → QC → UAT → PRODUCTION; promotion shall require SoD-enforced signatures (Author ≠ Approver). |
| URS-CFG-02 | M | R2 | Configuration backups shall be exportable for inspection. |

### 5.2 Document Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DOC-01 | H | R1 | Documents (URS, FS, CS, DS, RTM, IQ, OQ, PQ, VSR, VMP) shall follow DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE; transitions e-signed; SoD enforced. |
| URS-DOC-02 | H | R1 | Document templates shall be version-controlled; template promotion shall require Author ≠ Approver. |
| URS-DOC-03 | H | R1 | Document references (e.g., FS → URS, RTM → URS + FS + tests) shall be maintained as first-class links; broken references shall be flagged at sign-off. |
| URS-DOC-04 | H | R1 | Documents shall be exportable in a regulator-friendly format (PDF/A-3) for audit / inspection purposes. |

### 5.3 Per-Module Protocol Authoring (FS / CS / DS / IQ / OQ / PQ)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUTH-01 | H | R1 | FS shall be authored with traceability to URS lines via typed links; orphan URS lines surfaced at sign-off. |
| URS-AUTH-02 | H | R1 | CS (Configuration Specification) shall capture per-configurable-item values + verification method. |
| URS-AUTH-03 | H | R1 | DS (Design Specification) shall capture custom-development design decisions for Cat 5 sub-components. |
| URS-AUTH-04 | H | R1 | IQ shall list installed components, versions, environment, with vendor-IQ inheritance for vendor-shared evidence. |
| URS-AUTH-05 | H | R1 | OQ shall list test cases per URS / FS / CS / DS line with expected results and acceptance criteria. |
| URS-AUTH-06 | H | R1 | PQ shall test end-to-end against representative production scenarios. |
| URS-AUTH-07 | M | R2 | Protocol templates per module (FS/CS/DS/IQ/OQ/PQ) shall be curated and versioned by Template Author + Template Approver. |

### 5.4 Risk-Based Testing per FDA CSA (Feb 2026) and GAMP 5 RBA

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RBT-01 | H | R1 | Each system under validation shall be classified per FDA CSA (Feb 2026): production / quality-system criticality + intended-use category drive testing depth. |
| URS-RBT-02 | H | R1 | Per ICH Q9(R1), risk classification shall be documented at project start with critical-thinking justification; classification shall drive protocol depth (full IQ/OQ/PQ vs lean OQ-only) and evidence requirements. |
| URS-RBT-03 | H | R1 | Per ISPE GAMP 5 RBA, GAMP category (Cat 1/3/4/5) shall be declared per system and shall drive default protocol structure. |
| URS-RBT-04 | H | R1 | Risk reclassification (e.g., post-release expansion of intended use) shall trigger re-evaluation of testing-depth tier. |
| URS-RBT-05 | M | R2 | The platform shall report on testing-depth distribution across the portfolio for management review. |

### 5.5 Protocol Execution — Handhelds, Offline, E-Signature

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-EXE-01 | H | R1 | Protocol execution shall capture step-by-step actual-results, evidence attachments, executor + witness signatures, timestamps. |
| URS-EXE-02 | H | R1 | Test-step deviations shall route to the eQMS for disposition; execution may continue per the deviation-disposition flag. |
| URS-EXE-03 | H | R1 | Execution lock: completed executions shall be immutable; corrections shall be via amendment with re-signature and audit trail. |
| URS-EXE-04 | H | R1 | Evidence attachments shall be hash-verified at upload and at archive; tampered attachments shall be flagged. |
| URS-EXE-05 | M | R2 | Execution time-stamps shall be NTP-synced across executors. |
| URS-EXE-06 | H | R1 | Handheld (tablet / phone) execution shall be supported with in-room evidence capture (photo / barcode). |
| URS-EXE-07 | H | R1 | Offline execution shall be supported; sync on reconnection shall reconcile execution records with the server; conflicts shall surface for resolution. |
| URS-EXE-08 | H | R1 | E-signature on handhelds shall require fresh re-authentication; biometric (where supported) is acceptable when bound to Okta identity. |

### 5.6 Deviation Lifecycle per Execution

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEV-01 | H | R1 | Deviations raised in execution shall capture: test-step reference, observed result, expected result, immediate-action, disposition, root cause linkage (if any). |
| URS-DEV-02 | H | R1 | Deviation push to MasterControl shall be idempotent; failed pushes shall block execution finalisation. |
| URS-DEV-03 | M | R2 | Deviation severity (Minor / Major / Critical) shall drive routing (Project Lead / QA / VP QA). |
| URS-DEV-04 | M | R2 | A deviation summary shall be embedded in the VSR. |

### 5.7 RTM Maintenance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RTM-01 | H | R1 | RTM shall be auto-generated from typed links between URS / FS / RTM / test cases; orphan URS items shall be flagged. |
| URS-RTM-02 | H | R1 | RTM completeness gate at VSR sign-off; orphan items must be justified or addressed in the VSR. |
| URS-RTM-03 | H | R1 | Per FDA CSA (Feb 2026), the RTM shall reflect risk-based-testing depth: not every URS requires full IQ/OQ/PQ coverage; the gating logic shall accept risk-justified exemptions documented in the RTM. |
| URS-RTM-04 | M | R2 | RTM versions shall be snapshotted at each milestone (VSR draft, VSR final). |

### 5.8 CSV Training and Certification

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-CERT-01 | H | R1 | The CSV curriculum library shall hold role-specific curricula (Executor, Witness, Risk Classifier, Project Lead). |
| URS-TRN-CERT-02 | H | R1 | Certification shall be required before a role can be assigned to a project; expiry shall trigger re-certification. |
| URS-TRN-CERT-03 | M | R2 | Annual refresher training shall cover GAMP 5 / FDA CSA updates and audit-trail review best practices. |
| URS-TRN-CERT-04 | M | R2 | Certification records shall be exportable per inspector request. |

### 5.9 Multi-Site Federation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-FED-01 | H | R1 | Templates + role-matrices + risk-classification matrices shall federate across the 5 sites with documented authoritative-site rules. |
| URS-FED-02 | H | R1 | Cross-site project transfer shall require Multi-Site Federation Steward signature. |
| URS-FED-03 | M | R2 | Federation lag shall be monitored; lag > 10 min shall raise an alert. |

### 5.10 Audit Trail and Records Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | A contemporaneous, time-stamped audit trail shall capture user, action, old value, new value, reason-for-change for all document lifecycle transitions, protocol executions, deviations, configuration changes, and signature events. |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only at the platform level; not editable by tenant administrators. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be performed monthly by Validation Operations and quarterly by QA per EU GMP Annex 11 § 9. |
| URS-AUD-04 | H | R1 | Retention shall be life-of-system + ≥ 25 years per the system being validated; retention enforcement shall block premature deletion. |
| URS-AUD-05 | M | R2 | A focused-audit-trail-review tool shall filter to material events (signatures, deviations, configuration changes, RTM exemptions). |

### 5.11 21 CFR Part 11 Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a), procedures and controls shall protect the validity of validation records. |
| URS-PART11-02 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via Okta SSO + MFA. |
| URS-PART11-03 | H | R1 | Per § 11.10(e), operational audit trail per § 5.10 shall exist. |
| URS-PART11-04 | H | R1 | Per § 11.50, electronic signatures applied to document approvals and execution sign-offs shall include signer's printed name, date and time, and meaning of signature. |
| URS-PART11-05 | H | R1 | Per § 11.70, signatures shall be cryptographically linked to the signed record; subsequent record changes shall invalidate the signature. |
| URS-PART11-06 | H | R1 | Per § 11.200, re-authentication shall be required at the moment of signing. |
| URS-PART11-07 | H | R1 | Per § 11.300, password / credential controls per site InfoSec policy. |

### 5.12 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | **Attributable:** Every action attributable to a named user. |
| URS-DI-02 | H | R1 | **Legible:** Records exportable as PDF/A-3 + machine-readable XML. |
| URS-DI-03 | H | R1 | **Contemporaneous:** Events recorded at time of occurrence. |
| URS-DI-04 | H | R1 | **Original:** Execution evidence preserved unaltered. |
| URS-DI-05 | H | R1 | **Accurate:** RTM auto-generation deterministic and validated under OQ. |
| URS-DI-06 | M | R2 | **Complete / Consistent / Enduring / Available:** Records meet ALCOA+ retention obligations (life-of-system + ≥ 25 y). |

### 5.13 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-VAULT-01 | H | R1 | Vault QualityDocs URN resolution shall provide bidirectional linkage to controlled documents. |
| URS-INT-EQMS-01 | H | R1 | Deviation push to MasterControl on execution test-step failures shall propagate audit trail. |
| URS-INT-PORT-01 | M | R2 | Application-portfolio sync (system inventory, criticality classification, owner) shall be supported. |
| URS-INT-GIT-01 | H | R1 | Release-linked validation: validation campaign linked to GitLab tag / commit for the system being validated. |
| URS-INT-SSO-01 | H | R1 | Okta SAML 2.0 + MFA shall be used for all human authentication. |

### 5.14 Performance and Availability

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | Document open + edit latency P95 ≤ 3 seconds. |
| URS-PERF-02 | M | R2 | The platform shall support ≥ 500 concurrent executors during peak validation campaigns. |
| URS-PERF-03 | M | R2 | Offline-handheld sync ≤ 60 s for a representative execution of 50 test steps. |
| URS-AV-01 | H | R1 | Availability ≥ 99.5% per ValGenesis SLA; maintenance windows announced ≥ 7 days in advance. |

### 5.15 Backup, Restore, and Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | Vendor-managed backup with daily integrity verification; site shall verify vendor RPO ≤ 4 h, RTO ≤ 24 h via annual vendor-assurance review. |
| URS-BAK-02 | H | R1 | Site shall maintain a tenant-data export with life-of-system + ≥ 25-year retention in cold storage. |
| URS-SEC-01 | H | R1 | TLS 1.3 in transit; AES-256 at rest. |
| URS-SEC-02 | H | R1 | Role-based access reviewed quarterly. |
| URS-SEC-03 | M | R2 | Penetration testing annually; high/critical findings remediated under change control. |

### 5.16 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Role-specific training in the site LMS shall be completed before access; Risk Classifier role shall require advanced FDA CSA + ICH Q9(R1) training. |
| URS-TRN-02 | M | R2 | Annual refresher training shall cover GAMP 5 / FDA CSA updates and audit-trail review best practices. |
| URS-PR-01 | H | R1 | Annual periodic review per EU GMP Annex 11 § 11 shall cover: vendor qualification currency, configuration drift, template inventory, audit-trail review evidence, integration health, training currency, security posture, RTM-completeness statistics, deviation patterns, federation-replication health. Signed by Director Validation Operations + VP QA + VP IT Compliance. |

### 5.17 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is SAML 2.0 via Entra ID with SCIM lifecycle provisioning; conditional-access policy `Quality-App Conditional Access (MFA + device-compliance for validation e-signature)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the ValGenesis SQL backend; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 25 y (validation record) per the consuming-record schedule. |

### 5.18 Cross-System Integration — Helios audit-trail handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HEL-01 | H | R1 | ValGenesis VLM shall publish audit-trail events (Validation deliverable lifecycle (URS / FS / RA / IQ / OQ / PQ / VSR), test-result entry, and e-signature events) to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract (JSON Lines, schema-registry pinned, Kafka topic `helios.ingest.cygnus.valgenesis.v1`) within 5 minutes of event capture; 21 CFR § 11.10(e) audit-trail completeness shall be preserved end-to-end so that no event class is lost at the boundary. |
| URS-XINT-HEL-02 | H | R1 | Pre-handover audit-trail retention on the ValGenesis VLM side shall be ≥ 25 y regardless of Helios availability; once Helios acknowledges ingest (per-message ack with idempotency key), Helios is the system-of-record for review and the ValGenesis VLM local copy serves as the durability backstop until the local retention floor expires. |

### 5.19 Cross-System Integration — eQMS CAPA handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-EQMS-01 | H | R1 | On detection of Validation failure (trigger: IQ/OQ/PQ failed test execution, change-control validation gap), the system shall push a CAPA-ticket creation event to the Talos MasterControl eQMS (`TLB-URS-EQMS-001`) via the eQMS event-push channel with required metadata {originating_system, originating_record_id, finding_class, severity, evidence_package_uri, detection_ts_utc, detection_user, regulatory_basis}; severity per site validation procedure. |
| URS-XINT-EQMS-02 | H | R1 | The eQMS ticket-creation call shall be idempotent on `{originating_system, originating_record_id, finding_class}`; the eQMS status-callback shall be ingested and reflected on the originating record with a hyperlink to the eQMS ticket; closed-loop verification per ICH Q9(R1) + ICH Q10 shall be evidenced before the originating record is dispositioned. |

## 6. Acceptance Criteria

1. CS, RA, IQ (vendor-shared), OQ (lifecycle / signature / execution / RTM / audit / risk-classification / handheld + offline / federation), PQ (representative end-to-end project including URS → VSR through full lifecycle with deviation handling + FDA CSA risk-based-testing example + handheld execution + offline sync) approved and executed.
2. VSR approved by VP QA + VP IT Compliance + Director Validation Operations.
3. RTM shall demonstrate every URS requirement mapped to at least one approved test case (or risk-justified exemption per FDA CSA).
4. FDA CSA risk-classification matrix validated and signed off.

## 7. Constraints

- Vendor releases not under site change control but impact-assessed.
- The platform shall not bypass the SoD model under any condition (Author ≠ Approver is non-overridable).
- Risk reclassification of an EFFECTIVE system shall require concurrent regression of executions where testing-depth tier changes.

## 8. Assumptions

- Okta, Vault, MasterControl, GitLab, application-portfolio system are themselves validated.
- FDA CSA (Feb 2026) final guidance interpretation is consistent across the site's QA + IT-Compliance teams.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 — Electronic Records; Electronic Signatures (§§ .10, .30, .50, .70, .100, .200, .300).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).

### EU
- EU GMP Annex 11 — Computerised Systems (§§ 4, 6, 9, 11).
- EU GMP Chapter 4 — Documentation.

### DACH-specific
- **BfArM (DE)** — Bundesinstitut für Arzneimittel und Medizinprodukte; **Anlage 7** (Aspekte der GMP-Inspektion).
- **Swissmedic (CH)** — guidance on computerised system inspection.
- **AGES PharmMed (AT)**.

### International — ICH
- ICH Q9(R1) — Quality Risk Management.
- ICH Q10 — Pharmaceutical Quality System.

### ISPE
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE GAMP Good Practice Guide: *A Risk-Based Approach to Compliant Computerised Systems*.
- ISPE GAMP Good Practice Guide: *Records and Data Integrity*.
- ISPE *Validation Master Plan Guide*.

### PIC/S
- PIC/S PI 041 — Good Practices for Data Management and Integrity.

### Vendor
- ValGenesis — *VLM 5.x Validation Approach and Customer-Shared CSV Summary*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

