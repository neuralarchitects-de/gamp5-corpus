---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; expanded 2026-05-12 (T3 uplift, deviation/CAPA/CC/complaint/audit/risk-mgmt/training/supplier/APR/inspection-readiness lifecycle sub-sections; ICH Q9(R1) + Q10 PQR binding; 21 CFR § 820.198 complaints)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed., 2022) Cat 4 conventions for SaaS configurable platforms"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "21 CFR Part 820 §§ .30, .40, .70, .80, .90, .100, .198"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Chapter 1 (PQS)"
  - "ICH Q9(R1) Quality Risk Management"
  - "ICH Q10 — Pharmaceutical Quality System (incl. Product Quality Review)"
  - "ISO 13485:2016 §§ 8.2, 8.3, 8.5 — Measurement, NCR, CAPA"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026; supersedes the September 2025 guidance)"
  - "PIC/S PI 041; ISO/IEC 27001:2022"
  - "MasterControl QMS 2025 + Veeva Vault QMS 24R3 Validation Approach"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## eQMS — MasterControl Manufacturing Excellence + QMS 2025

**Document Number:** TLB-URS-EQMS-001
**Version:** 1.0
**Effective Date:** 2026-04-26 *(synthetic)*
**Site:** Talos Bio AB, Global QA Operations, Gothenburg, Sweden *(fictional)*
**System Owner:** Head of Global QA Operations
**Process Owner:** VP Quality Assurance
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS; vendor handles infrastructure; site validates configuration)
**Project Mode:** Configuration project on commercial software product **MasterControl Manufacturing Excellence + QMS 2025** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 820 §§ .30, .40, .70, .80, .90, .100, .198 (medical-device QMS where applicable); EU GMP Annex 11 §§ 4, 6, 9, 11; ICH Q9(R1); ICH Q10 (incl. PQR); ISO 13485:2016 §§ 8.2, 8.3, 8.5

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of Global QA Operations) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Vendor Assurance — MasterControl relationship owner) | _____________ | _____________ | _____ |
| Reviewer (Risk Management Lead — ICH Q9(R1)) | _____________ | _____________ | _____ |
| Reviewer (Inspection Readiness Lead) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue (Tier T3 — 121 requirements covering Deviation, CAPA with effectiveness check, Change Control with impact assessment, Complaint per 21 CFR § 820.198, internal + external Audit, Quality Risk Management per ICH Q9(R1), Training + Competency, Supplier Quality + Approved Vendor List, Annual Product Review per ICH Q10, Inspection-Readiness tenant, LIMS + EDMS + LMS + clinical PV integration). |

## Definitions

| Term | Definition |
|---|---|
| eQMS | Electronic Quality Management System |
| MasterControl | MasterControl Manufacturing Excellence + QMS 2025 |
| Process | A configured workflow (Deviation, CAPA, Change Control, Complaint, Audit, Supplier, Training, APR / PQR, Inspection Readiness) |
| EDMS | Electronic Document Management System (Veeva Vault QualityDocs — separate URS) |
| LMS | Learning Management System (Cornerstone) |
| CAPA | Corrective and Preventive Action |
| CR | Change Request |
| QRM | Quality Risk Management per ICH Q9(R1) |
| APR / PQR | Annual Product Review / Product Quality Review per ICH Q10 / 21 CFR § 211.180 |
| AVL | Approved Vendor List |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the eQMS used globally for deviation management, CAPA with effectiveness review, change control with impact assessment, complaint handling (incl. medical-device complaints per 21 CFR § 820.198), internal / external audits, quality risk management per ICH Q9(R1), training assignment + competency, supplier quality + AVL, Annual Product Review per ICH Q10, and an inspection-readiness tenant for live regulator interactions.

## 2. Scope

**In scope:** MasterControl Manufacturing Excellence + QMS 2025 multi-tenant SaaS instance; site configuration of processes (Deviation, CAPA, Change Control, Complaint, Audit, Supplier, Training, Risk Mgmt, APR / PQR, Inspection Readiness); SSO via Okta; integrations with Veeva Vault QualityDocs (controlled-document linkage), Cornerstone (training task creation / completion), Werum PAS-X (deviation creation from MES events), LabWare LIMS 8 (deviation creation from OOS), and the clinical pharmacovigilance database (post-market safety signals); vendor-assurance program covering MasterControl.

**Out of scope:** MasterControl infrastructure; product-specification documents (managed in Vault); training-content authoring (LMS); manufacturing-process-execution data (PAS-X).

## 3. System Description and Intended Use

MasterControl is the system of record for QMS process records. Each process (Deviation, CAPA, Change Control, Complaint, Audit, Supplier, Training, Risk Mgmt, APR / PQR) follows a configured workflow with role-restricted electronic signatures at each transition. Cross-process linkage (e.g., Deviation → CAPA → Change Control) is enforced. A separate Inspection-Readiness tenant exposes a curated, readonly slice for regulators. GAMP Cat 4: MasterControl maintains the platform under their published SDLC and customer-shared CSV evidence; site validation focuses on configuration of processes, the integration boundary, and Part 11 controls applied to that configuration.

## 4. User Roles

| Role | Permissions |
|---|---|
| Initiator | Create new process records (deviations / changes / etc.). |
| Investigator / Owner | Process the record; complete fields; raise tasks. |
| Reviewer | Review process records; cannot approve own. |
| Approver | Approve process records; cannot approve own. |
| QA Sign-off (CAPA Effectiveness) | Co-approve CAPA effectiveness review. |
| Risk Owner | Maintain risk register entries per ICH Q9(R1). |
| Complaint Handler | Triage + investigate complaints; 21 CFR § 820.198 fields enforced. |
| Audit Lead | Plan + execute internal / external audits; manage findings. |
| Supplier Quality Officer | Maintain AVL, supplier scorecards, requalification. |
| APR Author | Compile Annual Product Review per ICH Q10 / 211.180. |
| Inspection Tenant Curator | Approve content for the Inspection-Readiness tenant. |
| Process Configuration Author | Configure / edit process workflows under change control. |
| Process Configuration Approver (QA) | Approve workflow configuration changes to PRODUCTION. |
| eQMS Administrator | User / role provisioning, AD groups, configuration deployment. |
| Auditor | Read-only across records and audit trails. |

Separation of duties: Initiator ≠ Reviewer ≠ Approver of the same record; Configuration Author ≠ Configuration Approver; Risk Owner ≠ Risk Approver; APR Author ≠ APR Approver.

## 5. User Requirements

### 5.1 Vendor / Platform Assurance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-01 | H | R1 | MasterControl shall be qualified as a critical SaaS vendor with documented evidence: SOC 2 Type II, ISO 27001, HIPAA attestation, customer-shared CSV summary. |
| URS-VND-02 | H | R1 | Vendor releases (cadenced) shall be impact-assessed within 14 days; configuration-affecting changes shall trigger re-validation. |
| URS-VND-03 | M | R2 | SLA KPIs (≥ 99.7% availability) shall be reviewed quarterly. |
| URS-VND-04 | M | R2 | Vendor escalation runbook with named MasterControl contacts shall be on file. |

### 5.2 Process Configuration Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PROC-01 | H | R1 | Each process workflow shall follow a configured lifecycle with documented states (e.g., Deviation: OPEN → INVESTIGATING → AWAITING-DISPOSITION → APPROVED → CLOSED). |
| URS-PROC-02 | H | R1 | Process configuration changes shall follow DEV → QC → UAT → PRODUCTION; only PRODUCTION configurations may run for live records. |
| URS-PROC-03 | H | R1 | Configuration deployment shall require role-restricted signatures with separation of duties. |
| URS-PROC-04 | H | R1 | UAT shall execute documented test scripts covering each role's expected actions and the exception paths. |
| URS-PROC-05 | M | R2 | Configuration baselines shall be exportable for inspection. |

### 5.3 Deviation Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEV-01 | H | R1 | Deviation records shall capture: source, classification (Minor / Major / Critical), product / batch / equipment scope, root-cause analysis, immediate actions, disposition. |
| URS-DEV-02 | H | R1 | Critical deviations shall escalate to QA within 24 hours of creation. |
| URS-DEV-03 | H | R1 | Root-cause analysis shall capture method (5-Why, Ishikawa, FMEA reference) and supporting evidence (LIMS / PAS-X / EM links). |
| URS-DEV-04 | H | R1 | Deviation closure shall require disposition signed by QA Approver; closure without disposition shall be blocked. |
| URS-DEV-05 | M | R2 | Deviation trending per product / equipment / category shall be available per quarter. |
| URS-DEV-06 | M | R2 | Recurrence detection (same root-cause within 90 days) shall surface to the Risk Owner. |

### 5.4 CAPA Lifecycle and Effectiveness Check

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CAPA-01 | H | R1 | CAPAs shall link to source deviations / complaints / audits / risk-register entries at creation; orphan CAPAs shall be blocked. |
| URS-CAPA-02 | H | R1 | CAPA effectiveness review shall be required before CLOSED; effectiveness criteria shall be defined at CAPA creation. |
| URS-CAPA-03 | H | R1 | Effectiveness review shall require a separate QA Effectiveness signature with SoD (Effectiveness Reviewer ≠ CAPA Owner). |
| URS-CAPA-04 | H | R1 | An ineffective-CAPA outcome shall reopen the CAPA or trigger a new CAPA referencing the original. |
| URS-CAPA-05 | M | R2 | CAPA aging shall be reported; CAPAs older than 180 days shall escalate to VP QA. |
| URS-CAPA-06 | M | R2 | A CAPA-effectiveness dashboard shall surface effective / ineffective / pending rates per quarter. |

### 5.5 Change Control and Impact Assessment

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CC-01 | H | R1 | Change Control records shall capture impact assessment across (process, product, equipment, validation, regulatory, training, supply) categories. |
| URS-CC-02 | H | R1 | Change Control approval shall require QA, regulatory, and process-owner signatures per the configured matrix. |
| URS-CC-03 | H | R1 | Risk assessment per ICH Q9(R1) (severity × probability × detectability) shall be captured at CR creation. |
| URS-CC-04 | H | R1 | A CR's training-impact shall trigger LMS training-task creation; closure shall require training-completion evidence. |
| URS-CC-05 | M | R2 | A CR's regulatory-impact shall route to Regulatory Affairs for variation / notification disposition. |
| URS-CC-06 | M | R2 | Emergency CRs shall be supported with shortened workflow but additional post-implementation review. |

### 5.6 Complaint Handling per 21 CFR § 820.198

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-COMP-01 | H | R1 | Complaints shall capture per 21 CFR § 820.198(e): complainant identifier, complaint date, device name + serial / lot, complainant's stated nature of complaint, investigation outcome, reply to complainant. |
| URS-COMP-02 | H | R1 | Complaints classified as "device failure" or "potential reportable event" shall trigger MDR (Medical Device Report) decision logic within 24 hours. |
| URS-COMP-03 | H | R1 | Complaint records shall link to source PV signal (where complaint originates from PV database) and to any related CAPA. |
| URS-COMP-04 | M | R2 | Complaint trend reporting per device family / failure mode shall be available per quarter. |
| URS-COMP-05 | M | R2 | Reply-to-complainant SLA shall be configurable per market / device class. |

### 5.7 Internal and External Audit Workflow

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-IA-01 | H | R1 | Audit records shall capture scope, plan, agenda, audit team, audit-trail evidence, observations, findings, and CAPA links. |
| URS-AUD-IA-02 | H | R1 | Internal audit plan shall follow an annual schedule; missed audits shall create deviations. |
| URS-AUD-IA-03 | H | R1 | External audit findings (FDA / EMA / BfArM / Swissmedic / Notified Body) shall be captured with regulator + finding-class + response-due-date. |
| URS-AUD-IA-04 | M | R2 | Audit findings shall escalate to CAPA per a configurable class-rule matrix. |

### 5.8 Quality Risk Management per ICH Q9(R1)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-QRM-01 | H | R1 | The risk register shall capture risks per ICH Q9(R1): description, source, severity, probability, detectability, RPN, mitigation, residual risk, owner, review date. |
| URS-QRM-02 | H | R1 | Risk register entries shall link to deviations, CAPAs, change controls that affect them. |
| URS-QRM-03 | M | R2 | RPN re-calculation shall be automated when severity / probability / detectability change. |
| URS-QRM-04 | M | R2 | Risk-register periodic review per ICH Q9(R1) shall be calendared per risk class. |

### 5.9 Training and Competency

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Training tasks shall be created in Cornerstone for role-specific curricula and for read-and-understood tasks from EDMS. |
| URS-TRN-02 | H | R1 | Competency assessments shall be captured for critical roles (QA Approver, Sterile Filling Operator, CAPA Effectiveness Reviewer). |
| URS-TRN-03 | M | R2 | Production access gating shall depend on Cornerstone completion-flag for the role. |
| URS-TRN-04 | M | R2 | Annual refresher cycle shall be enforced for every role designated as quality-critical. |

### 5.10 Supplier Quality and Approved Vendor List

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SUPP-01 | H | R1 | The AVL shall list every supplier with qualification status, audit-cycle, scorecards, and risk class. |
| URS-SUPP-02 | H | R1 | Procurement from non-AVL suppliers shall be blocked; emergency override shall require Head-of-QA signature + deviation. |
| URS-SUPP-03 | M | R2 | Supplier audits shall be calendared per risk class; missed audits shall create deviations. |
| URS-SUPP-04 | M | R2 | Supplier scorecards shall include OOS rate, on-time delivery, complaint rate, audit findings. |

### 5.11 Annual Product Review per ICH Q10 / 21 CFR § 211.180(e)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-APR-01 | H | R1 | The system shall compile APR / PQR per product per ICH Q10, pulling batch data, OOS / OOT, deviations, complaints, change controls, returned product, stability, in-process control data. |
| URS-APR-02 | H | R1 | APR sign-off shall require Author ≠ Approver SoD (APR Author + APR Approver + QA Head). |
| URS-APR-03 | M | R2 | APR cadence shall be configurable per product / market; the system shall surface overdue APRs. |
| URS-APR-04 | M | R2 | APR outcome (no-action / minor-CR / major-CR) shall route to Change Control. |

### 5.12 Inspection-Readiness Tenant

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INSP-01 | H | R1 | The Inspection-Readiness tenant shall be a separate, read-only slice exposing curated documents and records for live regulator inspections. |
| URS-INSP-02 | H | R1 | Content promotion from main tenant to inspection tenant shall require Inspection Tenant Curator approval. |
| URS-INSP-03 | M | R2 | The inspection tenant shall surface deviation, CAPA, complaint, and audit-finding aging at-a-glance for inspector view. |
| URS-INSP-04 | M | R2 | A documented inspection-runbook shall accompany the tenant. |

### 5.13 Audit Trail

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AT-01 | H | R1 | Time-stamped, secure audit trail per § 11.10(e) shall cover all record state transitions, content edits, approvals, configuration changes, role assignments. |
| URS-AT-02 | H | R1 | Audit trail shall be append-only; reviewable in-app and exportable. |
| URS-AT-03 | H | R1 | Audit-trail review per Annex 11 § 9 shall be performed monthly by QA Compliance and quarterly at the platform level. |
| URS-AT-04 | H | R1 | Retention shall be ≥ 25 years from product expiry; 50-year retention shall be available for selected processes. |
| URS-AT-05 | M | R2 | A focused audit-trail-review tool shall filter to material events (approvals, configuration changes, role grants, mass deletes). |

### 5.14 21 CFR Part 11 / Annex 11

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a) procedural controls shall protect record validity. |
| URS-PART11-02 | H | R1 | Per § 11.10(b) accurate + complete copies for inspection. |
| URS-PART11-03 | H | R1 | Per § 11.10(d) access shall be limited to authorised individuals via Okta SAML 2.0 + MFA. |
| URS-PART11-04 | H | R1 | Per § 11.50 e-signatures shall include printed name, date / time, meaning. |
| URS-PART11-05 | H | R1 | Per § 11.70 signatures shall be cryptographically bound to record state. |
| URS-PART11-06 | H | R1 | Per § 11.100 signatures shall be unique to a single individual. |
| URS-PART11-07 | H | R1 | Per § 11.200 re-authentication shall be required at signing. |
| URS-PART11-08 | H | R1 | Per § 11.300 password / credential controls per site InfoSec policy. |
| URS-ANX11-01 | H | R1 | Per Annex 11 § 4 validation evidence kept current. |
| URS-ANX11-02 | H | R1 | Per Annex 11 § 6 accuracy checks at data-entry boundaries. |

### 5.15 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-VAULT-01 | H | R1 | Controlled-document references in process records shall resolve to Vault QualityDocs URNs; broken references shall be flagged in monthly reconciliation. |
| URS-INT-LMS-01 | H | R1 | CAPA training tasks shall create read-and-understood tasks in Cornerstone for the assigned audience. |
| URS-INT-PASX-01 | H | R1 | PAS-X-originated deviations shall create eQMS records via REST with idempotency; failed pushes shall alert PAS-X within 5 minutes. |
| URS-INT-LIMS-01 | H | R1 | LIMS OOS shall auto-create deviation records via REST with idempotency. |
| URS-INT-PV-01 | H | R1 | The clinical pharmacovigilance database shall push post-market safety signals into eQMS complaints with idempotency. |
| URS-INT-SSO-01 | H | R1 | All authentication shall be via Okta SAML 2.0 + MFA. |

### 5.16 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | Records shall be Attributable. |
| URS-DI-02 | H | R1 | Records shall be Legible — exportable as PDF / CSV. |
| URS-DI-03 | H | R1 | Records shall be Contemporaneous (vendor-platform NTP-synced timestamps). |
| URS-DI-04 | H | R1 | Original record content preserved; corrections recorded as new audit-trail entries. |
| URS-DI-05 | H | R1 | Workflow logic Accurate per OQ. |
| URS-DI-06 | M | R2 | Complete / Consistent / Enduring / Available. |

### 5.17 Performance / Availability / Backup / Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | Record open / list response shall be ≤ 3 s at 95th percentile. |
| URS-PERF-02 | M | R2 | APR compilation for a typical product shall complete within 30 min. |
| URS-AV-01 | H | R1 | Availability target shall align with vendor SLA (≥ 99.7%). |
| URS-BAK-01 | H | R1 | Vendor-managed backup; site shall verify vendor-published RPO ≤ 4 h, RTO ≤ 24 h via vendor-assurance program. |
| URS-BAK-02 | M | R2 | Site annual configuration export (workflows, security profiles) for traceability. |
| URS-SEC-01 | H | R1 | All access via Okta SSO + MFA. |
| URS-SEC-02 | H | R1 | Role-based access; cross-process visibility restricted by region / product where required. |
| URS-SEC-03 | M | R2 | Bulk-export events shall trigger audit-trail review. |

### 5.18 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-PR-01 | H | R1 | Production access shall require recorded role-specific training (LMS). |
| URS-TRN-PR-02 | M | R2 | Risk Owners + APR Authors + Inspection Curators shall complete an advanced QMS training. |
| URS-PR-01 | H | R1 | An annual periodic review per Annex 11 § 11 shall cover configuration drift, audit-trail review evidence, vendor-assurance status, integration health, training currency, CAPA-effectiveness rate, APR currency, inspection-tenant freshness, signed by Head of Global QA Operations + VP QA. |

### 5.19 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is SAML 2.0 via Entra ID with SCIM lifecycle provisioning; conditional-access policy `Quality-App Conditional Access (MFA + device-compliance for CAPA / deviation e-signature)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the MasterControl SQL backend; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 25 y (Quality record) per the consuming-record schedule. |

### 5.20 Cross-System Integration — Helios audit-trail handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HEL-01 | H | R1 | MasterControl eQMS shall publish audit-trail events (CAPA, deviation, change-control, audit-finding, and complaint-investigation lifecycle events) to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract (JSON Lines, schema-registry pinned, Kafka topic `helios.ingest.talos.mastercontrol.v1`) within 5 minutes of event capture; 21 CFR § 11.10(e) audit-trail completeness shall be preserved end-to-end so that no event class is lost at the boundary. |
| URS-XINT-HEL-02 | H | R1 | Pre-handover audit-trail retention on the MasterControl eQMS side shall be ≥ 25 y regardless of Helios availability; once Helios acknowledges ingest (per-message ack with idempotency key), Helios is the system-of-record for review and the MasterControl eQMS local copy serves as the durability backstop until the local retention floor expires. |

### 5.21 Cross-System Integration — CAPA ingestion from originating GxP systems

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-EQMS-INGEST-01 | H | R1 | The MasterControl eQMS shall expose a CAPA-ticket-creation endpoint that accepts events from originating GxP systems with the required metadata set {originating_system, originating_record_id, finding_class, severity, evidence_package_uri, detection_ts_utc, detection_user, regulatory_basis}; the endpoint shall be rate-limited (default 100 req/min/originating_system, burst 300) with token-bucket back-pressure. |
| URS-XINT-EQMS-INGEST-02 | H | R1 | CAPA-ticket dedup shall use `{originating_system, originating_record_id, finding_class}` as the natural key; duplicate creations within 7 days shall reopen / link to the existing ticket rather than create a new one; the originating-system identity shall be cryptographically asserted (mTLS client cert from the site PKI per `QTZ-URS-AD-001` URS-PKI-*). |
| URS-XINT-EQMS-INGEST-03 | H | R1 | The CAPA ticket schema shall include the originating-system field as a first-class attribute and shall permit per-originating-system reporting / filtering in the eQMS dashboards; ticket count by originating system shall be exposed in the monthly Quality Council pack. |
| URS-XINT-EQMS-INGEST-04 | H | R1 | The eQMS shall emit a status-callback webhook `eqms.status.v1` to the originating system on every CAPA state transition with retry semantics (at-least-once delivery, exponential back-off, DLQ at 10 attempts); the originating-system signing-key for webhook verification shall be retrieved from HashiCorp Vault. |

### 5.22 Cross-System Integration — EDMS handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-EDMS-01 | H | R1 | When a CAPA action item is of type `procedure-update`, the eQMS shall create a linked controlled-document revision request in the EDMS via the EDMS API; the EDMS revision shall be cross-linked to the originating CAPA ID and closed-loop verification shall require the EDMS document to be EFFECTIVE before the CAPA can transition to EFFECTIVENESS state. |

## 6. Acceptance Criteria

System shall enter validated GxP use when CS (configuration), RA, IQ (vendor-shared), OQ (workflow / signature / integration), PQ (representative end-to-end records through full lifecycle including LMS task creation, CAPA-effectiveness gate, APR compilation, complaint-with-MDR-decision, inspection-tenant promotion) are approved and executed; vendor-assurance evidence shall be reviewed and accepted; VSR shall be approved by Head of Global QA Operations + VP QA; the RTM shall map every URS to ≥ 1 approved test case.

## 7. Constraints

- Vendor releases are not under site change control.
- Site impact assessment shall be completed within 14 days.

## 8. Assumptions

- Okta, Vault, Cornerstone, PAS-X, LIMS, PV-DB are independently validated.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- 21 CFR Part 820 §§ .30, .40, .70, .80, .90, .100, .198
- 21 CFR Part 211 §§ .22, .180, .192
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EU GMP Chapter 1 (Pharmaceutical Quality System)

### International — ICH
- ICH Q9(R1) — Quality Risk Management
- ICH Q10 — Pharmaceutical Quality System

### Industry
- ISO 13485:2016 §§ 8.2, 8.3, 8.5
- ISPE GAMP 5 (2nd ed., 2022)
- PIC/S PI 041; ISO/IEC 27001:2022

### Vendor
- MasterControl — *QMS 2025 Validation Approach* (vendor white paper)

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

