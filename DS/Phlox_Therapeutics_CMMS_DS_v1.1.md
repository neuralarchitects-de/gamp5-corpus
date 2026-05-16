---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (v1.0 corpus genesis per METHODOLOGY § 2B)"
seed_corpus_basis:
  - "PHX-FS-CMMS-001 v1.1 (parent FS)"
  - "PHX-URS-CMMS-001 v1.0 (parent URS — transitive)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "ICH Q10; ASTM E2500-20; ANSI/ISA-95; ISO 55001:2014"
parent_fs:
  document_number: PHX-FS-CMMS-001
  version: "1.1"
  file: "../../../FS_FDS/_generated/final/Phlox_Therapeutics_CMMS_FS_v1.3.md"
parent_urs:
  document_number: PHX-URS-CMMS-001
  version: "1.1"
  file: "../../../URS/_generated/final/CMMS_Maintenance_Management__Phlox_Therapeutics_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## CMMS — IBM Maximo Application Suite (MAS) 8.x — Manage

**Document Number:** PHX-DS-CMMS-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** PHX-FS-CMMS-001 v1.1
**Parent URS:** PHX-URS-CMMS-001 v1.0 *(informational; transitive)*
**Site:** Phlox Therapeutics SA, Engineering Maintenance, Lisbon, Portugal *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **IBM Maximo Application Suite (MAS) 8.x — Manage** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; ICH Q10; ASTM E2500-20; ANSI/ISA-95; ISO 55001:2014.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Engineering Maintenance Lead — SME) | _____________ | _____________ | _____ |
| Reviewer (Calibration Manager — SME) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Approver (System Owner — Engineering Maintenance Lead) | _____________ | _____________ | _____ |
| Approver (Head of Engineering) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial issue. Inherited Tier T2–T3 from parent URS+FS pair (URS lands at 68 reqs; FS at 60 FS-IDs). DS covers 60/60 FS-IDs; 0 FS-IDs flagged as vendor-internal — no site design surface. Generated as part of the DS v1.0 corpus ship per METHODOLOGY § 2B. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

DS-specific terms only — URS / FS definitions inherited by reference.

| Term | Definition |
|---|---|
| CS | Configuration Specification (this document) |
| CI | Configuration Item — one configurable parameter, value, default-vs-custom flag, justification |
| LBSPP | Logic-Based Script Plug-in Point (IBM Maximo's automation script binding mechanism — declarative configuration) |
| WO | Work Order in Maximo |
| PM | Preventive Maintenance task in Maximo |
| PdM | Predictive Maintenance |
| Qualification status | DQ / IQ / OQ / PQ state per ASTM E2500 |

## 1. Purpose

This Configuration Specification (CS) is the technical-design layer between `PHX-FS-CMMS-001` v1.1 and downstream configuration / IQ / OQ / PQ Protocols for the IBM Maximo Application Suite 8.x — Manage deployment at Phlox Therapeutics Engineering Maintenance, supporting ~1,200 assets, calibration management, predictive maintenance, spare-parts inventory, and ASTM E2500 qualification-status gating. The DS declares, per configuration item, the chosen value, default-vs-custom flag, FS-ID(s) traced, and planned verification. Vendor source-code internals (Maximo MAS platform; embedded automation-script engine) are not redrawn here — those remain under IBM SDLC.

## 2. Scope

### In scope

- Maximo MAS 8.x (Manage) on site OpenShift cluster.
- Asset register for ~1,200 assets (GxP-critical flag + qualification status DQ/IQ/OQ/PQ per ASTM E2500).
- ANSI/ISA-95 parent-child asset hierarchy (Enterprise → Site → Area → Production Line → Unit → Equipment Module → Control Module).
- PM scheduling + auto-generation with idempotency.
- Work-order workflow with SoD gates.
- Calibration records with NIST-traceable standards + back-trace report.
- Predictive Maintenance ingest + rule-firing → WO creation.
- Spare-parts catalog + min-stock reorder workflow.
- Equipment qualification-status gating on WO scheduling.
- Audit-trail bindings, 21 CFR Part 11 controls.
- Integration endpoints: MasterControl eQMS (deviations), calibration management system, LIMS, PdM analytics platform, AD (Entra ID SAML 2.0 + Keycloak MFA), HashiCorp Vault.

### Out of scope

- Non-GxP assets within Maximo (still in Maximo register but out of GxP DS scope; covered by site asset-management operational SOP only).
- Inventory finance (handled in SAP ERP).

## 3. Architectural Overview

### 3.1 Logical view

```
   ┌─────────────────────────────────────────────────────────────┐
   │                AD (Entra ID SAML 2.0) + Keycloak MFA          │
   └─────────────────────┬───────────────────────────────────────┘
                         │
   ┌─────────────────────▼───────────────────────────────────────┐
   │              Maximo MAS 8.x — Manage                          │
   │              (site OpenShift cluster, multi-pod)              │
   │   ┌──────────────────────────────────────────────────┐        │
   │   │ Asset register + ISA-95 hierarchy                 │        │
   │   └──────────────────────────────────────────────────┘        │
   │   ┌──────────────────────────────────────────────────┐        │
   │   │ PM scheduler + auto-generator (cron)              │        │
   │   └──────────────────────────────────────────────────┘        │
   │   ┌──────────────────────────────────────────────────┐        │
   │   │ Work-order workflow + state machine sm_wo         │        │
   │   └──────────────────────────────────────────────────┘        │
   │   ┌──────────────────────────────────────────────────┐        │
   │   │ Calibration management + NIST back-trace          │        │
   │   └──────────────────────────────────────────────────┘        │
   │   ┌──────────────────────────────────────────────────┐        │
   │   │ Predictive Maintenance rules + sensor ingest      │        │
   │   └──────────────────────────────────────────────────┘        │
   │   ┌──────────────────────────────────────────────────┐        │
   │   │ Spare-parts catalog + reorder workflow            │        │
   │   └──────────────────────────────────────────────────┘        │
   └────┬──────────┬────────────┬──────────────┬──────────────┘
        │          │            │              │
        ▼          ▼            ▼              ▼
   MasterControl  Calibration  LIMS          PdM Analytics
   eQMS           Mgmt Sys     (cal results)  Platform
   (deviations)
```

### 3.2 ISA-95 asset-tree topology (text diagram)

```
Phlox Therapeutics Enterprise
└── Lisbon Site
    ├── Area: API Manufacturing
    │   ├── Production Line: API Line 1
    │   │   ├── Unit: Reactor R-101 (GxP-Critical, IQ/OQ/PQ done)
    │   │   │   ├── Equipment Module: Agitation
    │   │   │   ├── Equipment Module: Heating/Cooling
    │   │   │   └── Equipment Module: Pressure Control
    │   │   ├── Unit: Centrifuge C-101 (GxP-Critical)
    │   │   └── Unit: Dryer D-101 (GxP-Critical)
    │   └── Production Line: API Line 2
    ├── Area: Finished-Product Manufacturing
    ├── Area: Utilities (WFI loop, Pure Steam, HVAC — all GxP-Critical)
    └── Area: QC Labs (instruments tagged but separately validated)

Total: ~1,200 assets, ~800 GxP-Critical, ~400 non-GxP.
```

## 4. Configuration Specification

### 4.1 Asset Master and Hierarchy

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CMMS-01 | GxP-critical flag + qualification-status enum | `gxp_critical` boolean + `qualification_status ∈ {DQ, IQ, OQ, PQ, REQUAL_DUE, DECOMMISSIONED}` | Custom | FS-ASSET-01. | FS-ASSET-01 | OQ-ASSET-FLAG-01 |
| DS-CMMS-02 | Asset-master change workflow | `wf_asset_change` Maximo workflow with Asset-Master-Author ≠ Asset-Master-Approver AD-group enforcement | Custom | FS-ASSET-02. | FS-ASSET-02 | OQ-ASSET-CHANGE-SOD-01 |
| DS-CMMS-03 | DELETE-block at DB layer | DELETE on `maximo_asset` blocked at DB role-grant level; decommissioning sets status only | Custom | FS-ASSET-03. | FS-ASSET-03 | OQ-ASSET-NODELETE-01 |
| DS-CMMS-04 | ISA-95 hierarchy fields | `enterprise_id, site_id, area_id, line_id, unit_id, module_id` in `maximo_asset` | Custom | FS-ASSET-04 + IEC 62264. | FS-ASSET-04 | OQ-ISA95-HIER-01 |
| DS-CMMS-05 | Re-parenting audit | `wf_hierarchy_move` workflow captures `reason ≥ 30 chars` in audit trail | Custom | FS-ASSET-05. | FS-ASSET-05 | OQ-HIER-REPARENT-01 |
| DS-CMMS-06 | Asset field set | make, model, serial, manufacturer, install_date, custodian — all required for GxP assets | Default | FS-ASSET-06. | FS-ASSET-06 | OQ-ASSET-FIELDS-01 |

### 4.2 Equipment Qualification Status Gating

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CMMS-07 | Per-asset qualification sub-states | DQ_done, IQ_done, OQ_done, PQ_done flags + dates per asset | Custom | FS-QUAL-01 + ASTM E2500. | FS-QUAL-01 | OQ-QUAL-STATE-01 |
| DS-CMMS-08 | WO-create qualification gate | WO-create against asset checks `qualification_status`; non-qualified blocks normal-mode WO; only `wo_type = REQUAL` permitted | Custom | FS-QUAL-02. | FS-QUAL-02 | OQ-WO-QUAL-GATE-01 |
| DS-CMMS-09 | Status-change workflow | `wf_qual_status` requires Qualification-Status Steward + QA e-signatures | Custom | FS-QUAL-03. | FS-QUAL-03 | OQ-QUAL-CHANGE-SOD-01 |
| DS-CMMS-10 | Requalification-due alerts | D-90 / D-30 / D-0 via Maximo task inbox | Custom | FS-QUAL-04. | FS-QUAL-04 | OQ-QUAL-ALERTS-01 |

### 4.3 PM Scheduling and Auto-Generation

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CMMS-11 | PM schedule storage | `maximo_pm` table per asset / task-type; due-date alerts at D-30 / D-7 / D-0 | Default | FS-PM-01. | FS-PM-01 | OQ-PM-SCHEDULE-01 |
| DS-CMMS-12 | Missed-PM deviation creation | LBSPP `OnPmMissedCreateDeviation` calls eQMS `POST /api/v2/deviations`; idempotency key `cmms:pm:<id>:missed`; trigger at `due_date + grace_window` | Custom | FS-PM-02. | FS-PM-02 | OQ-PM-MISSED-01 |
| DS-CMMS-13 | PM grace window | 7 calendar days default; configurable per asset class | Custom | FS-PM-02 explicit grace concept. | FS-PM-02 | OQ-PM-GRACE-01 |
| DS-CMMS-14 | PM completion capture | Technician, parts, time, findings, evidence (photo / measurement), supervisor sign-off | Default | FS-PM-03. | FS-PM-03 | OQ-PM-COMPLETION-01 |
| DS-CMMS-15 | PM-schedule change workflow | `wf_pm_change` for GxP asset PMs | Custom | FS-PM-04. | FS-PM-04 | OQ-PM-CHANGE-SOD-01 |
| DS-CMMS-16 | PM auto-generator cron | `phx-pm-autogen` nightly; creates WOs for upcoming PMs within configured horizon (30 d default) | Custom | FS-PM-05. | FS-PM-05 | OQ-PM-AUTOGEN-01 |
| DS-CMMS-17 | Auto-gen idempotency key | `pm_id + due_date_iso`; ON CONFLICT skip | Custom | FS-PM-06. | FS-PM-06 | OQ-PM-IDEMPOTENT-01 |
| DS-CMMS-18 | PM-compliance KPI report | `phx_rpt_pm_kpi` quarterly per asset class | Default | FS-PM-07. | FS-PM-07 | OQ-PM-KPI-01 |

### 4.4 Work Order Lifecycle

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CMMS-19 | WO state machine | `sm_wo`: NEW → APPROVED → IN-PROGRESS → COMPLETE → CLOSED; reverse transitions captured with reason | Default | FS-WO-01. | FS-WO-01 | OQ-WO-LIFECYCLE-01 |
| DS-CMMS-20 | GxP-asset WO supervisor sign-off | Completion gate: `supervisor_signature_id` not-null + `tech_signature_id ≠ supervisor_signature_id` | Custom | FS-WO-02. | FS-WO-02 | OQ-WO-SUPERVISOR-01 |
| DS-CMMS-21 | Quality-risk-finding escalation | LBSPP `OnQualityRiskCreateDeviation` triggers eQMS deviation on findings with `quality_risk = true` | Custom | FS-WO-03. | FS-WO-03 | OQ-WO-QR-DEVIATION-01 |
| DS-CMMS-22 | Spare-part GxP installation record | `part_lot_id` + `coc_ref` (Certificate of Conformance) required for GxP spare-part installs | Custom | FS-WO-04. | FS-WO-04 | OQ-WO-PART-LOT-01 |
| DS-CMMS-23 | Open-child-WO completion block | Parent WO completion blocked if open child WOs exist | Custom | FS-WO-05. | FS-WO-05 | OQ-WO-CHILD-01 |
| DS-CMMS-24 | Attachment hash preservation | Attachments stored in S3 with SHA-256 hash; integrity verified on retrieval | Custom | FS-WO-06. | FS-WO-06 | OQ-WO-ATTACH-01 |

### 4.5 Calibration Record and Traceability

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CMMS-25 | Calibration record schema | `maximo_cal_record`: as_found, as_left, uncertainty, nist_standard_id, nist_cert_ref, cal_date, tech_id, manager_id | Default | FS-CAL-01. | FS-CAL-01 | OQ-CAL-RECORD-01 |
| DS-CMMS-26 | Failed-calibration disposition | Triggers eQMS deviation `phx_cmms_fail_cal_dev`; asset `usage_block = true` until requalified | Custom | FS-CAL-02. | FS-CAL-02 | OQ-CAL-FAIL-01 |
| DS-CMMS-27 | Cal-tech ≠ cal-manager SoD | AD groups `Cal-Tech` ≠ `Cal-Manager` mutually exclusive | Custom | FS-CAL-03. | FS-CAL-03 | OQ-CAL-SOD-01 |
| DS-CMMS-28 | NIST-standard expiry monitor | `maximo_nist_expiry_alert` job at D-30 / D-7 / D-0 | Custom | FS-CAL-04. | FS-CAL-04 | OQ-NIST-EXPIRY-01 |
| DS-CMMS-29 | Back-trace report | `phx_rpt_cal_backtrace` lists batches measured by affected instrument between last-good and current-finding timestamp | Custom | FS-CAL-05. | FS-CAL-05 | OQ-CAL-BACKTRACE-01 |

### 4.6 Predictive Maintenance

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CMMS-30 | PdM ingest endpoint | `POST /api/v1/cmms/pdm-event`; idempotency key `pdm:sensor:<id>:event:<ts>` | Custom | FS-PDM-01. | FS-PDM-01 | OQ-PDM-INGEST-01 |
| DS-CMMS-31 | PdM anomaly → WO | Anomaly above threshold creates WO via `wf_pdm_wo_create`; threshold per asset / metric in `maximo_pdm_rules` | Custom | FS-PDM-02. | FS-PDM-02 | OQ-PDM-WO-01 |
| DS-CMMS-32 | PdM rule-change workflow | `wf_pdm_rule_change` requires PdM Engineer + Engineering Lead e-sig | Custom | FS-PDM-03. | FS-PDM-03 | OQ-PDM-RULE-SOD-01 |
| DS-CMMS-33 | PdM P/R quarterly report | `phx_rpt_pdm_metrics`; tracks precision / recall per rule | Default | FS-PDM-04. | FS-PDM-04 | OQ-PDM-METRICS-01 |

### 4.7 Spare-Parts Inventory and Reorder

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CMMS-34 | Spare-parts catalog | `maximo_part`: min-stock, on-hand, supplier, lead-time, gxp-criticality | Default | FS-PART-01. | FS-PART-01 | OQ-PART-CATALOG-01 |
| DS-CMMS-35 | Reorder workflow | `wf_part_reorder` on `on_hand < min_stock`; procurement task created | Custom | FS-PART-02. | FS-PART-02 | OQ-PART-REORDER-01 |
| DS-CMMS-36 | GxP-part receipt record | `supplier_lot_id` + `coc_ref` captured at receipt | Custom | FS-PART-03. | FS-PART-03 | OQ-PART-RECEIPT-01 |
| DS-CMMS-37 | Part-WO consumption link | Part decrement on WO closure FK-links to consuming WO | Default | FS-PART-04. | FS-PART-04 | OQ-PART-WO-LINK-01 |

### 4.8 Audit Trail / 21 CFR Part 11 / DI

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CMMS-38 | Audit-trail coverage | Asset / hierarchy / PM / WO / calibration / qualification-status / PdM-rule events | Default | FS-AUD-01. | FS-AUD-01 | OQ-AUD-COVERAGE-01 |
| DS-CMMS-39 | DB role separation | `maximo-app` role: INSERT / SELECT only on audit tables; UPDATE/DELETE blocked | Custom | FS-AUD-02. | FS-AUD-02 | OQ-AUD-APPENDONLY-01 |
| DS-CMMS-40 | Audit-review cadence | Monthly Maintenance-Lead + quarterly QA Compliance; evidence retained ≥ 25 y for product-impact events | Default | FS-AUD-03. | FS-AUD-03 | OQ-AUD-REVIEW-01 |
| DS-CMMS-41 | Retention | Routine 7 y; product-impact 25 y via Maximo retention config | Custom | FS-AUD-04. | FS-AUD-04 | OQ-RETENTION-01 |
| DS-CMMS-42 | § 11.10(a) procedural controls | SOPs in `PHX-SOP-CSV-01` | Default | FS-PART11-01. | FS-PART11-01 | OQ-PART11-01 |
| DS-CMMS-43 | § 11.10(b) copies | PDF/A-3 + CSV export validated | Default | FS-PART11-02. | FS-PART11-02 | OQ-PART11-02 |
| DS-CMMS-44 | § 11.10(d) access control | AD (Entra ID SAML 2.0) + Keycloak MFA | Custom | FS-PART11-03 + FS-XSYS-AD-01. | FS-PART11-03 | OQ-PART11-03 |
| DS-CMMS-45 | § 11.50 signature manifestation | Printed name + UTC timestamp + meaning text | Default | FS-PART11-04. | FS-PART11-04 | OQ-PART11-04 |
| DS-CMMS-46 | § 11.70 binding | HMAC-SHA256 over record-hash + signer-id + ts | Custom | FS-PART11-05. | FS-PART11-05 | OQ-PART11-05 |
| DS-CMMS-47 | § 11.100 uniqueness | AD uniqueness constraint | Default | FS-PART11-06. | FS-PART11-06 | OQ-PART11-06 |
| DS-CMMS-48 | § 11.200 re-auth | Re-auth at signing | Default | FS-PART11-07. | FS-PART11-07 | OQ-PART11-07 |
| DS-CMMS-49 | § 11.300 password policy | Per site InfoSec policy | Default | FS-PART11-08. | FS-PART11-08 | OQ-PART11-08 |
| DS-CMMS-50 | DI-Attributable | `actor_id` NOT NULL on every audit-emitting table | Default | FS-DI-01. | FS-DI-01 | OQ-DI-ATTRIB-01 |
| DS-CMMS-51 | DI-Original | Content preserved; corrections audit-trailed | Default | FS-DI-04. | FS-DI-04 | OQ-DI-IMMUTABLE-01 |

### 4.9 Integrations / Performance / Backup / Security / Training / PR

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CMMS-52 | eQMS deviation push | `POST /api/v2/deviations` with idempotency; missed-PM + quality-risk + failed-cal triggers | Default | FS-INT-EQMS-01. | FS-INT-EQMS-01 | OQ-INT-EQMS-01 |
| DS-CMMS-53 | Calibration-management-system feed | `IF-CAL-IN`; auto-updates `maximo_asset` calibration fields | Custom | FS-INT-CAL-01. | FS-INT-CAL-01 | OQ-INT-CAL-01 |
| DS-CMMS-54 | LIMS-sourced cal feed | `IF-LIMS-CAL-IN` for instrument calibration | Default | FS-INT-LIMS-01. | FS-INT-LIMS-01 | OQ-INT-LIMS-01 |
| DS-CMMS-55 | PdM platform feed | `IF-PDM-IN`; idempotent (DS-CMMS-30) | Default | FS-INT-PDM-01. | FS-INT-PDM-01 | OQ-INT-PDM-01 |
| DS-CMMS-56 | AD integration | Entra ID SAML 2.0 + Keycloak MFA; service accounts in HashiCorp Vault | Custom | FS-INT-AD-01 + FS-XSYS-AD-01. | FS-INT-AD-01 | OQ-INT-AD-01 |
| DS-CMMS-57 | WO list response SLO | P95 ≤ 2 s; benchmarked via `PHX-LT-WO-200U` | Custom | FS-PERF-01. | FS-PERF-01 | PQ-PERF-WO-01 |
| DS-CMMS-58 | Availability SLO | ≥ 99.5% shift hours; dashboard `phx-cmms-avail` | Default | FS-AV-01. | FS-AV-01 | OQ-AVAIL-MONITOR-01 |
| DS-CMMS-59 | DB nightly backup | Nightly with PITR | Default | FS-BAK-01. | FS-BAK-01 | OQ-BAK-PITR-01 |
| DS-CMMS-60 | Quarterly restore test | `PHX-BAK-RESTORE-LOG` evidence | Default | FS-BAK-02. | FS-BAK-02 | OQ-BAK-RESTORE-01 |
| DS-CMMS-61 | Account control | AD + MFA enforced; quarterly access review | Default | FS-SEC-01. | FS-SEC-01 | OQ-SEC-ACCESS-01 |
| DS-CMMS-62 | Service-account rotation | Vault paths `kv/cmms/service-accounts/*`; 90 d rotation | Custom | FS-SEC-02. | FS-SEC-02 | OQ-VAULT-ROTATE-01 |
| DS-CMMS-63 | LMS curriculum | Cornerstone `PHX-CURR-CMMS-USER` | Custom | FS-TRN-01. | FS-TRN-01 | OQ-LMS-GATE-01 |
| DS-CMMS-64 | Advanced curricula | `PHX-CURR-CAL-MANAGER` + `PHX-CURR-QUAL-STEWARD` | Custom | FS-TRN-02. | FS-TRN-02 | OQ-LMS-ADV-01 |
| DS-CMMS-65 | Periodic-review template | `PHX-PR-CMMS-YYYYMMDD`; signed by Maintenance Lead + Head of Engineering + Head of QA | Custom | FS-PR-01. | FS-PR-01 | OQ-PR-RUNBOOK-01 |

## 5. Workflow + Business-Rule Design

### 5.1 PM auto-generation and missed-PM detection workflow

```
[Nightly cron — phx-pm-autogen]
   │
   ▼  Reads maximo_pm table; selects PMs with due_date <= now() + 30 d
[PM auto-generator]
   │  For each upcoming PM:
   │   1. Compute idempotency key = pm_id + due_date_iso (DS-CMMS-17)
   │   2. INSERT INTO maximo_wo (...) ON CONFLICT (pm_id, due_date_iso) DO NOTHING
   │   3. If new WO created, send notification to assigned crew
   │
   ▼
[Day-of execution]
   │  Technician executes; Supervisor signs off (DS-CMMS-20)
   │
   ▼
[Missed-PM detector — runs at due_date + grace_window]
   │  If WO state != COMPLETE / CLOSED:
   │   1. LBSPP OnPmMissedCreateDeviation fires (DS-CMMS-12)
   │   2. POST eQMS deviation with idempotency cmms:pm:<id>:missed
   │   3. Asset entered in PM-compliance KPI report (DS-CMMS-18)
```

### 5.2 Calibration back-trace workflow

When a failed calibration is reported (DS-CMMS-26):

1. `phx_rpt_cal_backtrace` job runs against the affected instrument.
2. Job identifies the last KNOWN-good calibration timestamp `last_good_cal_ts`.
3. Job queries LIMS for all batches measured by the instrument between `last_good_cal_ts` and the failed-calibration timestamp.
4. Report lists every batch with: batch_id, measurement timestamp, measurement value, deviation severity.
5. Report attached to the eQMS deviation auto-created by DS-CMMS-26.
6. Quality Reviewer + Cal Manager review the back-trace; batches potentially affected go through impact assessment.

### 5.3 Qualification-status gating workflow

WO-create transaction:

1. WO request submitted with target asset_id.
2. Maximo loads asset; reads `gxp_critical` + `qualification_status`.
3. Decision tree:
   - If `gxp_critical = false`: allow WO regardless of qualification status.
   - If `gxp_critical = true` AND `qualification_status ∈ {DQ, IQ, OQ, PQ}` (qualified): allow WO of any type.
   - If `gxp_critical = true` AND `qualification_status ∈ {REQUAL_DUE, DECOMMISSIONED}` AND `wo_type != REQUAL`: BLOCK with reason `asset-not-qualified`.
4. Blocked requests audited to `cmms_audit.WO_CREATE_BLOCKED` for trend analysis.

### 5.4 Predictive Maintenance rule-fire → WO workflow

1. PdM platform pushes sensor anomaly via `POST /api/v1/cmms/pdm-event` (DS-CMMS-30).
2. Maximo PdM rule engine evaluates `maximo_pdm_rules` for that sensor / metric.
3. Rule fire → `wf_pdm_wo_create` workflow creates WO with priority + suggested task.
4. Maintenance Supervisor reviews + assigns.
5. PdM precision / recall captured per rule (DS-CMMS-33) — quarterly review.

## 6. Role-Permission Matrix Design

| Action / Role | Maint. Tech. | Maint. Supervisor | Asset Master Author | Asset Master Approver (QA) | PM Schedule Author | PM Schedule Approver (Eng + QA) | Cal Tech | Cal Manager | PdM Eng. | Qual.-Status Steward | Spare-Parts Custodian | System Admin | Auditor |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Execute WO; record parts / labour / findings | C/U | — | — | — | — | — | — | — | — | — | — | — | — |
| Assign WO; approve completion | — | C/U / S | — | — | — | — | — | — | — | — | — | — | — |
| Add / modify asset master + hierarchy | — | — | C/U | — | — | — | — | — | — | — | — | — | — |
| Approve master change (GxP) | — | — | — | S | — | — | — | — | — | — | — | — | — |
| Define / revise PM schedule | — | — | — | — | C/U | — | — | — | — | — | — | — | — |
| Approve PM schedule change (GxP) | — | — | — | — | — | S | — | — | — | — | — | — | — |
| Execute calibration | — | — | — | — | — | — | C/U | — | — | — | — | — | — |
| Approve calibration; manage NIST standards | — | — | — | — | — | — | — | S | — | — | — | — | — |
| Maintain PdM rules + thresholds | — | — | — | — | — | — | — | — | C/U / S | — | — | — | — |
| Maintain qualification status | — | — | — | — | — | — | — | — | — | C/U / S | — | — | — |
| Maintain spare-parts catalog + min-stock | — | — | — | — | — | — | — | — | — | — | C/U | — | — |
| Patching, AD groups | — | — | — | — | — | — | — | — | — | — | — | C/U | — |
| Read-only across data + audit trails | R | R | R | R | R | R | R | R | R | R | R | R | R |

Legend: R = read, C = create, U = update, S = sign (re-authenticated electronic signature), — = denied.

SoD denies per URS § 4:

- Asset Master Author ≠ Approver.
- PM Schedule Author ≠ Approver.
- Technician ≠ Supervisor of own WO.
- Cal Tech ≠ Cal Manager.
- Qualification-Status Steward ≠ Asset Master Author.

## 7. Integration Design

| IF-ID | Counterparty | Endpoint | Protocol | Direction | AuthN | Message schema | Retry / DLQ | Audit emission | FS-IDs traced |
|---|---|---|---|---|---|---|---|---|---|
| IF-EQMS-01 | MasterControl | `POST https://eqms.phlox.local/api/v2/deviations` | REST mTLS | outbound | mTLS + workload-identity | JSON deviation incl. idempotency `cmms:<source>:<id>` | exponential backoff 1/2/4/8/16 s; DLQ at 5 + alarm | `cmms_audit.DEVIATION_RAISED` | FS-INT-EQMS-01 |
| IF-CAL-IN | Calibration management system (Beamex CMX) | inbound webhook → Maximo `/api/v1/cmms/cal-result` | REST mTLS | inbound | mTLS + signed webhook | JSON cal-result schema | webhook retry from source; reconciliation nightly | `cmms_audit.CAL_INGEST` | FS-INT-CAL-01 |
| IF-LIMS-CAL-IN | LabWare LIMS 8 | inbound webhook → Maximo `/api/v1/cmms/lims-cal` | REST mTLS | inbound | mTLS + signed webhook | JSON LIMS cal-result | webhook retry | `cmms_audit.LIMS_CAL_INGEST` | FS-INT-LIMS-01 |
| IF-PDM-IN | PdM analytics platform | `POST /api/v1/cmms/pdm-event` | REST mTLS | inbound | mTLS + workload-identity | JSON PdM event incl. idempotency `pdm:sensor:<id>:event:<ts>` | webhook retry from PdM; reconciliation nightly | `cmms_audit.PDM_INGEST` | FS-INT-PDM-01 |
| IF-AD-01 | AD / Entra ID + Keycloak | SAML 2.0 to Entra; OIDC step-up to Keycloak | SAML + OIDC | bidirectional | SAML signed assertions + MFA | SAML + OIDC standard | retry per SDK | `cmms_audit.AUTHN` → Splunk `gxp-authn` | FS-INT-AD-01, FS-XSYS-AD-01 |
| IF-VAULT-01 | HashiCorp Vault | `https://vault.phlox.local/v1/kv/cmms/*` | HTTPS AppRole | inbound | AppRole | KV v2; 90 d rotation | retry on rotation | vault-access audit | FS-SEC-02 |

## 8. Site-Deployed Components Design

### 8.1 LBSPP automation scripts

Maximo's Logic-Based Script Plug-in Points used in this configuration:

- `OnPmMissedCreateDeviation` (DS-CMMS-12) — declarative configuration: triggers on (WO state at due_date+grace) → outbound REST POST.
- `OnQualityRiskCreateDeviation` (DS-CMMS-21) — declarative: triggers on (WO finding flagged quality_risk=true) → outbound REST POST.

These LBSPPs are declarative configuration (rule-based; no site-authored procedural code). They remain within Cat 4 scope.

### 8.2 Reports and KPI runners

- `phx_rpt_pm_kpi` (DS-CMMS-18) — Maximo BIRT report; declarative.
- `phx_rpt_pdm_metrics` (DS-CMMS-33) — Maximo BIRT report; declarative.
- `phx_rpt_cal_backtrace` (DS-CMMS-29) — Maximo BIRT report joined to LIMS read-only view; declarative.

All three are Cat 4 declarative.

### 8.3 Site-authored extensions

At v1.0 corpus ship, no site-authored procedural-code extension is deployed within Maximo. All workflow and reporting is achieved through declarative configuration (LBSPP rules + BIRT reports + workflow XML). Should a future extension be authored (e.g., a complex back-trace algorithm requiring Java logic), the corresponding mini-SDS sub-section will be added per METHODOLOGY § 2B.4 rule 6.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.

### International — ICH
- ICH Q10.

### Industry
- ASTM E2500-20.
- ANSI/ISA-95.
- ISO 55001:2014.
- ISPE GAMP 5 (2nd ed., 2022).
- ISPE GAMP Good Practice Guide *Calibration Management*.
- ISO/IEC 27001:2022.

### Vendor
- IBM — *Maximo Application Suite 8.x — Manage Reference* v8.10.
- IBM — *Maximo Automation Scripting Reference* v8.10.
- IBM — *Maximo BIRT Reporting Reference* v8.10.

### Site
- `PHX-SOP-CSV-01` — CSV procedure.
- `PHX-BAK-RESTORE-LOG` — restore-test log.
- `PHX-LT-WO-200U` — load-test runbook.

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-CMMS-01 | FS-ASSET-01 |
| DS-CMMS-02 | FS-ASSET-02 |
| DS-CMMS-03 | FS-ASSET-03 |
| DS-CMMS-04 | FS-ASSET-04 |
| DS-CMMS-05 | FS-ASSET-05 |
| DS-CMMS-06 | FS-ASSET-06 |
| DS-CMMS-07 | FS-QUAL-01 |
| DS-CMMS-08 | FS-QUAL-02 |
| DS-CMMS-09 | FS-QUAL-03 |
| DS-CMMS-10 | FS-QUAL-04 |
| DS-CMMS-11 | FS-PM-01 |
| DS-CMMS-12 | FS-PM-02 |
| DS-CMMS-13 | FS-PM-02 |
| DS-CMMS-14 | FS-PM-03 |
| DS-CMMS-15 | FS-PM-04 |
| DS-CMMS-16 | FS-PM-05 |
| DS-CMMS-17 | FS-PM-06 |
| DS-CMMS-18 | FS-PM-07 |
| DS-CMMS-19 | FS-WO-01 |
| DS-CMMS-20 | FS-WO-02 |
| DS-CMMS-21 | FS-WO-03 |
| DS-CMMS-22 | FS-WO-04 |
| DS-CMMS-23 | FS-WO-05 |
| DS-CMMS-24 | FS-WO-06 |
| DS-CMMS-25 | FS-CAL-01 |
| DS-CMMS-26 | FS-CAL-02 |
| DS-CMMS-27 | FS-CAL-03 |
| DS-CMMS-28 | FS-CAL-04 |
| DS-CMMS-29 | FS-CAL-05 |
| DS-CMMS-30 | FS-PDM-01 |
| DS-CMMS-31 | FS-PDM-02 |
| DS-CMMS-32 | FS-PDM-03 |
| DS-CMMS-33 | FS-PDM-04 |
| DS-CMMS-34 | FS-PART-01 |
| DS-CMMS-35 | FS-PART-02 |
| DS-CMMS-36 | FS-PART-03 |
| DS-CMMS-37 | FS-PART-04 |
| DS-CMMS-38 | FS-AUD-01 |
| DS-CMMS-39 | FS-AUD-02 |
| DS-CMMS-40 | FS-AUD-03 |
| DS-CMMS-41 | FS-AUD-04 |
| DS-CMMS-42 | FS-PART11-01 |
| DS-CMMS-43 | FS-PART11-02 |
| DS-CMMS-44 | FS-PART11-03 / FS-XSYS-AD-01 |
| DS-CMMS-45 | FS-PART11-04 |
| DS-CMMS-46 | FS-PART11-05 |
| DS-CMMS-47 | FS-PART11-06 |
| DS-CMMS-48 | FS-PART11-07 |
| DS-CMMS-49 | FS-PART11-08 |
| DS-CMMS-50 | FS-DI-01 |
| DS-CMMS-51 | FS-DI-04 |
| DS-CMMS-52 | FS-INT-EQMS-01 |
| DS-CMMS-53 | FS-INT-CAL-01 |
| DS-CMMS-54 | FS-INT-LIMS-01 |
| DS-CMMS-55 | FS-INT-PDM-01 |
| DS-CMMS-56 | FS-INT-AD-01 / FS-XSYS-AD-01 |
| DS-CMMS-57 | FS-PERF-01 |
| DS-CMMS-58 | FS-AV-01 |
| DS-CMMS-59 | FS-BAK-01 |
| DS-CMMS-60 | FS-BAK-02 |
| DS-CMMS-61 | FS-SEC-01 |
| DS-CMMS-62 | FS-SEC-02 |
| DS-CMMS-63 | FS-TRN-01 |
| DS-CMMS-64 | FS-TRN-02 |
| DS-CMMS-65 | FS-PR-01 |

**FS-IDs in parent FS NOT covered (with rationale):**

- FS-XSYS-BAK-01 (Veeam backup integration) — covered at site enterprise-backup-service DS level per `AUR-URS-BACKUP-001`; site binding via DS-CMMS-59 + DS-CMMS-60.

## 11. Appendix B — Design-level Risk Register

| DR-ID | Design-stage risk | Origin design choice | Mitigation reference |
|---|---|---|---|
| DR-01 | Missed-PM detection LBSPP could fail silently if Maximo cron daemon hangs | DS-CMMS-12 LBSPP + DS-CMMS-16 cron | External cron-health monitor via Prometheus; alert on missed cron execution |
| DR-02 | Auto-gen idempotency key (DS-CMMS-17) could collide if `due_date_iso` precision is per-day but PM schedule has multiple same-day runs | DS-CMMS-17 key shape | Schema constraint: same-day duplicate-PM schedules rejected at PM-schedule creation; periodic-review item |
| DR-03 | Qualification-status gate bypass via direct DB update on `qualification_status` field | DS-CMMS-08 + DS-CMMS-09 | DB role grants restrict UPDATE on the field; audit-trail captures direct changes; monthly review |
| DR-04 | Cal-tech ≠ cal-manager SoD bypass if user holds both AD groups | DS-CMMS-27 | AD group mutual-exclusion policy at Entra ID; conditional-access verification |
| DR-05 | PdM rule defect could cause WO storm (false-positive anomalies) | DS-CMMS-31 + DS-CMMS-32 rule-change SoD | Rate-limit per rule (max 10 WO/day per sensor); alert on exceeded rate |
| DR-06 | NIST standard expiry alert (DS-CMMS-28) at D-0 may be too late if standard already in use | DS-CMMS-28 D-30/D-7/D-0 | D-30 provides advance warning; procurement workflow tied to D-30 trigger |
| DR-07 | Back-trace report (DS-CMMS-29) depends on LIMS measurement-timestamp accuracy | DS-CMMS-29 | LIMS NTP sync required (LIMS-side URS); cross-system clock-skew monitor |
| DR-08 | GxP-part `coc_ref` field could be set to placeholder text by Maintenance Technician under pressure | DS-CMMS-22 | Field validation against supplier-CoA repository; mandatory cross-check |
| DR-09 | Decommissioned asset retained in PM auto-generator schedule | DS-CMMS-03 status-only + DS-CMMS-16 cron | Auto-generator filter excludes `DECOMMISSIONED` status; OQ-PM-AUTOGEN-01 |
| DR-10 | Audit-trail tampering by privileged DBA | DS-CMMS-39 DB role separation | DBA dual-control for any UPDATE on audit tables; monthly review |
| DR-11 | Quality-risk-finding LBSPP (DS-CMMS-21) depends on Technician self-flagging `quality_risk = true` | DS-CMMS-21 | Required-field; Supervisor sign-off cross-checks; periodic-review item |
| DR-12 | PdM event idempotency key (DS-CMMS-30) uses sensor-id + ts; could collide if two anomalies fire at exact same ts | DS-CMMS-30 key | Key extended with anomaly-type discriminator; OQ-PDM-INGEST-01 tests collision |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
