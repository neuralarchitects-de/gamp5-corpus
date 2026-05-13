---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; expanded 2026-05-12 (T2 uplift, asset master, work-order, PM, calibration, predictive, spare parts, qualification-status gating)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed., 2022) Cat 4 conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "ICH Q10 — Pharmaceutical Quality System"
  - "ASTM E2500-20 Specification, Design and Verification of Pharmaceutical and Biopharmaceutical Manufacturing Systems and Equipment"
  - "ANSI/ISA-95 Enterprise-Control System Integration"
  - "ISPE GAMP Good Practice Guide: Calibration Management"
  - "ISO 55001:2014 Asset Management"
  - "IBM Maximo Application Suite 8.x + Manage Application Reference"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## CMMS — IBM Maximo Application Suite (MAS) 8.x — Manage

**Document Number:** PHX-URS-CMMS-001
**Version:** 1.0
**Effective Date:** 2026-04-26 *(synthetic)*
**Site:** Phlox Therapeutics SA, Engineering Maintenance, Lisbon, Portugal *(fictional)*
**System Owner:** Engineering Maintenance Lead
**Process Owner:** Head of Engineering
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **IBM Maximo Application Suite (MAS) 8.x — Manage** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; ICH Q10; ASTM E2500; ANSI/ISA-95; ISO 55001:2014

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Engineering Maintenance Lead) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Calibration Manager) | _____________ | _____________ | _____ |
| Approver (Head of Engineering) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue (Tier T2 — 68 requirements covering asset master, asset hierarchy, work order lifecycle, PM scheduling + auto-generation, calibration + traceability, predictive maintenance, spare-parts inventory + reorder, equipment qualification status (DQ/IQ/OQ/PQ) gating, ASTM E2500 + ANSI/ISA-95 binding). |

## Definitions

| Term | Definition |
|---|---|
| CMMS | Computerised Maintenance Management System |
| Maximo | IBM Maximo Application Suite 8.x — Manage application |
| Asset | A site-registered piece of equipment with a unique tag |
| Hierarchy | Tree of parent-child asset relationships (system → sub-system → component) |
| PM | Preventive Maintenance task |
| PdM | Predictive Maintenance (sensor + analytics) |
| WO | Work Order |
| GxP-Critical Asset | Asset whose maintenance condition affects product quality / patient safety |
| Qualification Status | DQ / IQ / OQ / PQ state per ASTM E2500 |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

Define requirements for the CMMS managing preventive, corrective, and predictive maintenance of GxP-critical equipment at Phlox Therapeutics; calibration management; spare-parts inventory; equipment-qualification-status gating per ASTM E2500. Maintenance discipline is itself a GMP control; missed PM on a GxP-critical asset is a deviation.

## 2. Scope

**In:** Maximo MAS 8.x (Manage) on the site OpenShift cluster, asset register for ~1,200 assets (with GxP-critical flag and qualification status), parent-child hierarchy, PM scheduling + auto-generation, work-order workflow, calibration records, predictive-maintenance sensor + analytics, spare-parts catalog + reorder, integrations with the eQMS (deviation creation on missed PM / failed calibration), the calibration management system, the LIMS calibration-result feed, the PdM analytics platform, AD authentication.

**Out:** non-GxP assets (still in Maximo but out of GxP scope of this URS); inventory finance (handled in ERP).

## 3. System Description

Maximo is the system of record for maintenance activity on GxP-critical assets. Assets are organised in a hierarchy per ANSI/ISA-95 (Enterprise → Site → Area → Production Line → Unit → Equipment Module → Control Module). PMs are scheduled per asset; WOs are issued, executed, and closed with parts / labour / findings recorded. Missed-PM events on GxP-critical assets create deviations in eQMS automatically. Calibration records are signed + traced to NIST-traceable standards. PdM analytics ingest sensor data and surface anomaly events. Spare-parts inventory triggers reorders at min-stock. Equipment qualification status (DQ/IQ/OQ/PQ per ASTM E2500) is captured per asset and gates the asset's usability.

Cat 4: IBM maintains the platform; site validation focuses on configuration of asset master data, hierarchy, PM schedules, work-order workflow, calibration workflow, PdM rules, spare-parts catalog, and integrations.

## 4. User Roles

| Role | Permissions |
|---|---|
| Maintenance Technician | Execute WOs; record parts / labour / findings; cannot edit master data. |
| Maintenance Supervisor | Assign WOs; approve completion; cannot edit asset master. |
| Asset Master Author | Add / modify asset master data + hierarchy under change control. |
| Asset Master Approver (QA) | Approve master changes affecting GxP-critical assets. |
| PM Schedule Author | Define / revise PM schedules under change control. |
| PM Schedule Approver (Engineering + QA) | Approve PM schedule changes affecting GxP-critical assets. |
| Calibration Technician | Execute calibrations; record as-found / as-left + uncertainty. |
| Calibration Manager | Approve calibrations; manage NIST standards traceability. |
| PdM Engineer | Maintain PdM rules + thresholds; review anomalies. |
| Qualification-Status Steward | Maintain DQ/IQ/OQ/PQ status per asset + change. |
| Spare-Parts Custodian | Maintain spare-parts catalog + min-stock thresholds. |
| System Administrator | Patching, AD groups; cannot approve. |
| Auditor | Read-only across data and audit trails. |

Separation of duties: Asset Master Author ≠ Approver; PM Schedule Author ≠ Approver; Technician ≠ Supervisor of own WO; Calibration Tech ≠ Calibration Manager; Qualification-Status Steward ≠ Asset Master Author.

## 5. User Requirements

### 5.1 Asset Master and Hierarchy

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ASSET-01 | H | R1 | Each GxP-critical asset shall be flagged with the `gxp_critical = true` attribute and shall list its current qualification status (DQ / IQ / OQ / PQ / re-qualification due / decommissioned). |
| URS-ASSET-02 | H | R1 | Asset-master changes affecting GxP-critical assets shall require role-restricted signatures with separation of duties. |
| URS-ASSET-03 | H | R1 | Asset-master changes shall be change-controlled; deletion shall be prohibited (decommissioning is a status change). |
| URS-ASSET-04 | H | R1 | The system shall maintain a parent-child asset hierarchy per ANSI/ISA-95 (Enterprise → Site → Area → Line → Unit → Module). |
| URS-ASSET-05 | M | R2 | Hierarchy moves (re-parenting) shall be captured in audit trail with reason. |
| URS-ASSET-06 | M | R2 | Asset records shall capture make, model, serial, manufacturer, install-date, custodian. |

### 5.2 Equipment Qualification Status (DQ/IQ/OQ/PQ) Gating

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-QUAL-01 | H | R1 | Each GxP-critical asset shall carry its current qualification status (DQ done, IQ done, OQ done, PQ done) per ASTM E2500. |
| URS-QUAL-02 | H | R1 | WO scheduling against an asset shall verify the asset's qualification status; non-qualified assets shall block normal-mode WO scheduling (only requalification WOs permitted). |
| URS-QUAL-03 | H | R1 | Qualification-status changes shall require Qualification-Status Steward + QA signatures. |
| URS-QUAL-04 | M | R2 | The system shall surface assets due for requalification at D-90 / D-30 / D-0. |

### 5.3 PM Scheduling and Auto-Generation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PM-01 | H | R1 | PM schedules shall enforce the validated frequency for each GxP-critical asset (calendar-based or counter-based). |
| URS-PM-02 | H | R1 | A missed PM (beyond the configured grace window) on a GxP-critical asset shall auto-create a deviation in eQMS. |
| URS-PM-03 | H | R1 | PM completion shall capture: technician, parts used, time, findings, attached evidence (photos / measurements), and supervisor sign-off. |
| URS-PM-04 | H | R1 | PM-schedule changes affecting GxP-critical assets shall follow change control. |
| URS-PM-05 | H | R1 | PM auto-generation shall run nightly, creating WOs for upcoming PMs within the configured horizon. |
| URS-PM-06 | M | R2 | PM-generation race conditions (e.g., simultaneous schedule change + nightly run) shall be guarded by idempotent generation logic. |
| URS-PM-07 | M | R2 | PM-compliance KPIs shall be reported per asset class per quarter. |

### 5.4 Work Order Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-WO-01 | H | R1 | WO lifecycle shall be NEW → APPROVED → IN-PROGRESS → COMPLETE → CLOSED; reverse transitions shall be captured with reason. |
| URS-WO-02 | H | R1 | WOs on GxP-critical assets shall require Supervisor sign-off at completion. |
| URS-WO-03 | H | R1 | Findings indicating product-quality risk shall escalate to QA via deviation creation. |
| URS-WO-04 | M | R2 | Parts traceability — WO shall record the lot of any GxP-critical spare part installed. |
| URS-WO-05 | M | R2 | WO completion shall block if open child WOs exist. |
| URS-WO-06 | M | R2 | WOs shall support attachments (photos, measurements, supplier docs) with hash preservation. |

### 5.5 Calibration Record and Traceability

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CAL-01 | H | R1 | Calibration records shall capture as-found, as-left, measurement uncertainty, NIST-traceable standard ID + cert reference, calibration date, calibration tech, calibration manager. |
| URS-CAL-02 | H | R1 | Failed calibration shall auto-create a deviation in eQMS and block the affected asset from production use. |
| URS-CAL-03 | H | R1 | Calibration tech ≠ calibration manager SoD shall be enforced. |
| URS-CAL-04 | M | R2 | NIST standard expiry shall be alerted at D-30 / D-7 / D-0. |
| URS-CAL-05 | M | R2 | Out-of-tolerance calibrations shall back-trace which batches were measured by the affected instrument between the last good calibration and the current finding. |

### 5.6 Predictive Maintenance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PDM-01 | M | R2 | The system shall ingest sensor data from the PdM analytics platform with timestamp + sensor-id + metric. |
| URS-PDM-02 | M | R2 | PdM anomaly detections beyond configured thresholds shall create WOs for inspection or maintenance. |
| URS-PDM-03 | M | R2 | PdM rule changes shall follow change control with PdM Engineer + Engineering Lead signatures. |
| URS-PDM-04 | L | R3 | PdM detection precision/recall metrics shall be reported quarterly. |

### 5.7 Spare-Parts Inventory and Reorder

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART-01 | M | R2 | The spare-parts catalog shall list each part with min-stock, on-hand, supplier, lead time, and GxP-criticality flag. |
| URS-PART-02 | M | R2 | On-hand below min-stock shall trigger a reorder workflow (procurement task). |
| URS-PART-03 | M | R2 | Receipt of GxP-critical spare parts shall record supplier-lot, certificate-of-conformance reference. |
| URS-PART-04 | M | R2 | Decremented parts shall link to the consuming WO. |

### 5.8 Audit Trail / Records / Part 11 / Data Integrity

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | A time-stamped, secure audit trail per § 11.10(e) shall cover asset-master changes, hierarchy moves, PM schedules, WO lifecycle, calibration events, qualification-status changes, PdM rule changes, signatures. |
| URS-AUD-02 | H | R1 | Audit trail shall be append-only; no application or admin update / delete. |
| URS-AUD-03 | H | R1 | Audit-trail review per Annex 11 § 9 shall be performed monthly by Maintenance Lead and quarterly by QA Compliance. |
| URS-AUD-04 | H | R1 | Retention shall be ≥ 7 years for routine records; ≥ 25 years for events linked to product impact. |
| URS-PART11-01 | H | R1 | Per § 11.10(a) procedural controls shall protect record validity. |
| URS-PART11-02 | H | R1 | Per § 11.10(b) accurate + complete copies for inspection. |
| URS-PART11-03 | H | R1 | Per § 11.10(d) access limited to authorised individuals via AD with MFA. |
| URS-PART11-04 | H | R1 | Per § 11.50 e-signatures shall include printed name, date / time, meaning. |
| URS-PART11-05 | H | R1 | Per § 11.70 signatures shall be cryptographically bound. |
| URS-PART11-06 | H | R1 | Per § 11.100 signatures shall be unique. |
| URS-PART11-07 | H | R1 | Per § 11.200 re-authentication at signing. |
| URS-PART11-08 | H | R1 | Per § 11.300 password policy per site InfoSec. |
| URS-DI-01 | H | R1 | Records shall be Attributable. |
| URS-DI-04 | H | R1 | Originals shall be preserved unaltered; corrections audit-trailed. |

### 5.9 Integrations / Performance / Backup / Security / Training / PR

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-EQMS-01 | H | R1 | Missed-PM, quality-risk findings, and failed calibrations shall create deviations in MasterControl via REST with idempotency. |
| URS-INT-CAL-01 | H | R1 | Calibration data from the calibration management system shall flow into Maximo asset record on completion. |
| URS-INT-LIMS-01 | M | R2 | LIMS-sourced calibration results (for instruments where applicable) shall update Maximo asset record. |
| URS-INT-PDM-01 | M | R2 | PdM platform shall push sensor anomalies via REST with idempotency. |
| URS-INT-AD-01 | H | R1 | Authentication shall use AD with MFA; service accounts via vault. |
| URS-PERF-01 | M | R2 | WO open / list response shall be ≤ 2 s at 95th percentile. |
| URS-AV-01 | H | R1 | Availability shall be ≥ 99.5% during shift hours. |
| URS-BAK-01 | H | R1 | Database shall be backed up nightly with PITR. |
| URS-BAK-02 | H | R1 | Quarterly restore test shall be witnessed. |
| URS-SEC-01 | H | R1 | Authentication shall be via AD + MFA. |
| URS-SEC-02 | M | R2 | Service-account credentials shall live in HashiCorp Vault; rotation 90 d. |
| URS-TRN-01 | H | R1 | LMS-recorded role-specific training shall gate production access. |
| URS-TRN-02 | M | R2 | Calibration Manager + Qualification-Status Steward shall complete advanced training. |
| URS-PR-01 | H | R1 | An annual periodic review per Annex 11 § 11 shall cover asset inventory, missed-PM trend, calibration compliance, qualification-status currency, PdM performance, audit-trail review evidence, deviation summary, training; signed by Maintenance Lead + Head of Engineering + Head of QA. |

### 5.10 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is SAML 2.0 via Entra ID; conditional-access policy `Standard SaaS Conditional Access (MFA + device-compliance)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the work-order DB; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 10 y (calibration / maintenance history) per the consuming-record schedule. |

## 6. Acceptance Criteria

CS, RA, IQ, OQ, PQ shall be approved and executed; PQ shall include a representative PM cycle (including missed-PM scenario creating an eQMS deviation), a representative calibration cycle (incl. failed-calibration → deviation), a representative qualification-status change, and a representative PdM-anomaly-to-WO cycle; VSR shall be approved by Maintenance Lead + Head of Engineering + Head of QA.

## 7. Constraints

- Vendor patches shall be under change control.
- Non-qualified assets blocked from normal-mode WO scheduling.

## 8. Assumptions

- eQMS, calibration system, LIMS, PdM platform, AD are independently validated.
- Asset register is current at go-live.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11

### International — ICH
- ICH Q10 — Pharmaceutical Quality System

### Industry
- ASTM E2500-20 — Specification, Design and Verification of Pharmaceutical and Biopharmaceutical Manufacturing Systems and Equipment
- ANSI/ISA-95 — Enterprise-Control System Integration
- ISO 55001:2014 — Asset Management
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE GAMP Good Practice Guide: *Calibration Management*
- ISO/IEC 27001:2022

### Vendor
- IBM — *Maximo Application Suite 8.x — Manage Application Reference*

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

