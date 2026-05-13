---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (T2 catch-up: per-ID rows; asset hierarchy; PM auto-gen idempotency; calibration back-trace; qualification-status gate; predictive maintenance)"
seed_corpus_basis:
  - "PHX-URS-CMMS-001 v1.0 (parent URS, T2)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 conventions"
  - "21 CFR Part 11; EU GMP Annex 11; ASTM E2500; ANSI/ISA-95; ISO 55001:2014"
parent_urs:
  document_number: PHX-URS-CMMS-001
  version: 1.0
  file: ../../URS/_generated/final/CMMS_Maintenance_Management__Phlox_Therapeutics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## CMMS — IBM Maximo Application Suite (MAS) 8.x — Manage

**Document Number:** PHX-FS-CMMS-001
**Version:** 1.1
**Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** PHX-URS-CMMS-001 v1.0
**Site:** Phlox Therapeutics SA, Lisbon, Portugal *(fictional)*
**System Class:** GAMP Cat 4 — Configured Product
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; ICH Q10; ASTM E2500; ANSI/ISA-95; ISO 55001:2014

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Maintenance Manager) | _____________ | _____________ | _____ |
| Reviewer (Calibration Manager) | _____________ | _____________ | _____ |
| Approver (Head of Engineering) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-12 | (synthetic) | T2 catch-up: per-ID rows; asset hierarchy per ANSI/ISA-95; PM auto-gen idempotency; calibration back-trace; qualification-status gate; predictive-maintenance integration. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies how Maximo Application Suite (MAS) 8.x is configured to satisfy `PHX-URS-CMMS-001` v1.0 (T2) — preventive / corrective / predictive maintenance, asset management, qualification-status gating, calibration management, spare-parts inventory.

## 2. Scope

Maximo MAS 8.x application; per-site asset register with hierarchy; PM schedule + auto-generation; work-order workflow; calibration workflow with NIST traceability; PdM platform integration; spare-parts catalog; integrations with eQMS, LIMS, AD.

## 3. System Architecture

```
   AD ──► Maximo MAS 8.x ──► eQMS (deviations) / LIMS (cal results) / PdM (anomalies)
                  │
                  ├──► Asset register + ISA-95 hierarchy
                  ├──► PM scheduler + auto-generator
                  ├──► Calibration management
                  ├──► Predictive Maintenance rules
                  └──► Spare-parts inventory + reorder
```

| ID | Component | GAMP Cat |
|---|---|---|
| C-01 | Maximo MAS 8.x (Manage) | 4 |
| C-02 | eQMS (MasterControl) | 4 |
| C-03 | LIMS (LabWare 8) | 4 |
| C-04 | PdM analytics platform | 4 |
| C-05 | Calibration management system | 4 |
| C-06 | AD (Keycloak federation) | (infra) |

## 4. Functional Specifications

### 4.1 Asset Master and Hierarchy (URS § 5.1)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ASSET-01 | URS-ASSET-01 | Asset register `maximo_asset` carries `gxp_critical` + `qualification_status` enum (DQ / IQ / OQ / PQ / REQUAL_DUE / DECOMMISSIONED); GxP assets require full metrics. |
| FS-ASSET-02 | URS-ASSET-02 | Asset-master change workflow `wf_asset_change` requires `Asset-Master-Author` ≠ `Asset-Master-Approver` e-signatures. |
| FS-ASSET-03 | URS-ASSET-03 | DELETE on `maximo_asset` blocked at DB layer; decommissioning sets status only. |
| FS-ASSET-04 | URS-ASSET-04 | ISA-95 hierarchy fields `enterprise_id`, `site_id`, `area_id`, `line_id`, `unit_id`, `module_id` in `maximo_asset`. |
| FS-ASSET-05 | URS-ASSET-05 | Re-parenting via `wf_hierarchy_move` captures `reason` ≥ 30 chars in audit trail. |
| FS-ASSET-06 | URS-ASSET-06 | Asset fields: make, model, serial, manufacturer, install_date, custodian — all required for GxP assets. |

### 4.2 Equipment Qualification Status Gating (URS § 5.2)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-QUAL-01 | URS-QUAL-01 | Per-asset qualification status with sub-states tracking DQ / IQ / OQ / PQ completion + dates. |
| FS-QUAL-02 | URS-QUAL-02 | WO-create against asset checks `qualification_status`; non-qualified blocks normal-mode WO; only `wo_type = REQUAL` permitted. |
| FS-QUAL-03 | URS-QUAL-03 | Status-change workflow `wf_qual_status` requires Qualification-Status Steward + QA e-signatures. |
| FS-QUAL-04 | URS-QUAL-04 | Requalification-due alerts at D-90 / D-30 / D-0 via Maximo task inbox. |

### 4.3 PM Scheduling and Auto-Generation (URS § 5.3)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PM-01 | URS-PM-01 | PM schedules per asset / task-type stored in `maximo_pm`; due-date alerts at D-30 / D-7 / D-0. |
| FS-PM-02 | URS-PM-02 | LBSPP `OnPmMissedCreateDeviation` calls eQMS `POST /api/v2/deviations`; idempotency key `cmms:pm:<id>:missed`; trigger on `due_date + grace_window`. |
| FS-PM-03 | URS-PM-03 | PM completion form captures technician, parts, time, findings, evidence (photo / measurement), supervisor sign-off. |
| FS-PM-04 | URS-PM-04 | PM-schedule changes affecting GxP assets follow change control via `wf_pm_change`. |
| FS-PM-05 | URS-PM-05 | PM auto-generator cron `phx-pm-autogen` runs nightly; creates WOs for upcoming PMs within configured horizon. |
| FS-PM-06 | URS-PM-06 | Auto-gen idempotency key = `pm_id + due_date_iso`; ON CONFLICT skip; covers concurrent schedule change scenario. |
| FS-PM-07 | URS-PM-07 | PM-compliance KPI report `phx_rpt_pm_kpi` quarterly per asset class. |

### 4.4 Work Order Lifecycle (URS § 5.4)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-WO-01 | URS-WO-01 | WO state machine `sm_wo`: NEW → APPROVED → IN-PROGRESS → COMPLETE → CLOSED; reverse transitions captured. |
| FS-WO-02 | URS-WO-02 | Completion gate on GxP assets requires `supervisor_signature_id` not-null + `tech_signature_id ≠ supervisor_signature_id`. |
| FS-WO-03 | URS-WO-03 | Findings flagged `quality_risk = true` trigger LBSPP `OnQualityRiskCreateDeviation` to eQMS. |
| FS-WO-04 | URS-WO-04 | Spare-part installation records `part_lot_id`; GxP spare-part installs require `coc_ref` (Certificate of Conformance reference). |
| FS-WO-05 | URS-WO-05 | Open child WO check blocks parent completion. |
| FS-WO-06 | URS-WO-06 | Attachments stored in S3 with SHA-256 hash preservation. |

### 4.5 Calibration Record and Traceability (URS § 5.5)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CAL-01 | URS-CAL-01 | Calibration record schema `maximo_cal_record`: `as_found`, `as_left`, `uncertainty`, `nist_standard_id`, `nist_cert_ref`, `cal_date`, `tech_id`, `manager_id`. |
| FS-CAL-02 | URS-CAL-02 | Failed calibration triggers eQMS deviation `phx_cmms_fail_cal_dev` + sets asset `usage_block = true` until requalified. |
| FS-CAL-03 | URS-CAL-03 | SoD via AD groups `Cal-Tech` ≠ `Cal-Manager`. |
| FS-CAL-04 | URS-CAL-04 | NIST-standard expiry monitor `maximo_nist_expiry_alert` at D-30 / D-7 / D-0. |
| FS-CAL-05 | URS-CAL-05 | Back-trace report `phx_rpt_cal_backtrace` lists batches measured by affected instrument between last-good and current-finding ts. |

### 4.6 Predictive Maintenance (URS § 5.6)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PDM-01 | URS-PDM-01 | PdM ingest via REST `POST /api/v1/cmms/pdm-event`; idempotency key `pdm:sensor:<id>:event:<ts>`. |
| FS-PDM-02 | URS-PDM-02 | Anomaly above threshold creates WO via `wf_pdm_wo_create`; threshold per asset / metric in `maximo_pdm_rules`. |
| FS-PDM-03 | URS-PDM-03 | Rule-change workflow `wf_pdm_rule_change` requires PdM Engineer + Engineering Lead e-sig. |
| FS-PDM-04 | URS-PDM-04 | Quarterly P/R report `phx_rpt_pdm_metrics`. |

### 4.7 Spare-Parts Inventory and Reorder (URS § 5.7)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART-01 | URS-PART-01 | Spare-parts catalog `maximo_part` with min-stock, on-hand, supplier, lead-time, gxp-criticality. |
| FS-PART-02 | URS-PART-02 | Reorder workflow `wf_part_reorder` triggers on `on_hand < min_stock`; procurement task created. |
| FS-PART-03 | URS-PART-03 | Receipt of GxP-critical part records `supplier_lot_id`, `coc_ref`. |
| FS-PART-04 | URS-PART-04 | Part decrement on WO closure FK-links to consuming WO. |

### 4.8 Audit Trail / Records / Part 11 / Data Integrity (URS § 5.8)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Maximo audit-trail covers asset / hierarchy / PM / WO / calibration / qualification-status / PdM-rule events. |
| FS-AUD-02 | URS-AUD-02 | DB role separation: `maximo-app` has INSERT/SELECT only on audit tables; UPDATE/DELETE blocked. |
| FS-AUD-03 | URS-AUD-03 | Monthly Maintenance-Lead review + quarterly QA Compliance review; evidence retained ≥ 25 y for product-impact events. |
| FS-AUD-04 | URS-AUD-04 | Retention: routine 7 y; product-impact 25 y via Maximo retention config. |
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural controls in `PHX-SOP-CSV-01`. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(b): PDF/A-3 + CSV export validated. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(d): AD + Keycloak MFA. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.50: printed name + ts + meaning. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.70: HMAC-SHA256 over record-hash + signer-id + ts. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.100: AD uniqueness constraint. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.200: re-auth at signing. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.300: password policy per site InfoSec. |
| FS-DI-01 | URS-DI-01 | **Attributable:** `actor_id` not-null. |
| FS-DI-04 | URS-DI-04 | **Original:** content preserved; corrections audited. |

### 4.9 Integrations / Performance / Backup / Security / Training / PR (URS § 5.9)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | Missed-PM, quality-risk, failed-cal push to MasterControl via REST `POST /api/v2/deviations` with idempotency. |
| FS-INT-CAL-01 | URS-INT-CAL-01 | Calibration-management-system feed `IF-CAL-IN`; auto-updates `maximo_asset` calibration fields. |
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | LIMS-sourced calibration via `IF-LIMS-CAL-IN`. |
| FS-INT-PDM-01 | URS-INT-PDM-01 | PdM platform feed `IF-PDM-IN`; idempotent. |
| FS-INT-AD-01 | URS-INT-AD-01 | AD + Keycloak MFA; service accounts in HashiCorp Vault. |
| FS-PERF-01 | URS-PERF-01 | WO open / list P95 ≤ 2 s; benchmarked by `PHX-LT-WO-200U`. |
| FS-AV-01 | URS-AV-01 | Availability ≥ 99.5% shift hours; dashboard `phx-cmms-avail`. |
| FS-BAK-01 | URS-BAK-01 | Nightly DB backup with PITR. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore test witnessed; `PHX-BAK-RESTORE-LOG`. |
| FS-SEC-01 | URS-SEC-01 | AD + MFA enforced. |
| FS-SEC-02 | URS-SEC-02 | HashiCorp Vault paths `kv/cmms/service-accounts/*`; 90 d rotation. |
| FS-TRN-01 | URS-TRN-01 | Cornerstone curriculum `PHX-CURR-CMMS-USER`. |
| FS-TRN-02 | URS-TRN-02 | Advanced curriculum `PHX-CURR-CAL-MANAGER + PHX-CURR-QUAL-STEWARD`. |
| FS-PR-01 | URS-PR-01 | Annual periodic-review template `PHX-PR-CMMS-YYYYMMDD`. |


### 4.10 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: SAML 2.0 via Entra ID. Conditional-access binding to policy `Standard SaaS Conditional Access (MFA + device-compliance)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the work-order DB; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Configuration Items (CI)

| CI ID | Item | Value |
|---|---|---|
| CI-01 | Asset criticality | GxP / non-GxP |
| CI-02 | PM due-date alerts | D-30 / D-7 / D-0 |
| CI-03 | Work-order signature | technician + supervisor (SoD) |
| CI-04 | Failed-cal disposition | eQMS deviation auto-create + asset block |
| CI-05 | Hierarchy levels | Enterprise / Site / Area / Line / Unit / Module |
| CI-06 | PM auto-gen horizon | 30 days |
| CI-07 | Auto-gen idempotency key | `pm_id + due_date_iso` |
| CI-08 | NIST expiry alerts | D-30 / D-7 / D-0 |
| CI-09 | Audit retention (routine) | 7 y |
| CI-10 | Audit retention (product-impact) | 25 y |

## 6. Risks

- Overdue PM on GxP asset undetected → FS-PM-02 + alerts + escalation.
- Failed calibration not surfaced → FS-CAL-02 deviation + asset block.
- Auto-gen race → FS-PM-06 idempotent key.
- Non-qualified asset used in production → FS-QUAL-02 WO-create gate.
- NIST standard expired during use → FS-CAL-04 alert + procurement task.
- Audit-trail tampering → FS-AUD-02 DB role separation.

## 7. References

- PHX-URS-CMMS-001 v1.0
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11
- ICH Q10; ASTM E2500-20; ANSI/ISA-95; ISO 55001:2014
- ISPE GAMP 5 (2nd ed., 2022); ISPE GAMP GPG: Calibration Management
- IBM — *Maximo Application Suite 8.x — Manage Reference*

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-ASSET-01 | FS-ASSET-01 |
| URS-ASSET-02 | FS-ASSET-02 |
| URS-ASSET-03 | FS-ASSET-03 |
| URS-ASSET-04 | FS-ASSET-04 |
| URS-ASSET-05 | FS-ASSET-05 |
| URS-ASSET-06 | FS-ASSET-06 |
| URS-QUAL-01 | FS-QUAL-01 |
| URS-QUAL-02 | FS-QUAL-02 |
| URS-QUAL-03 | FS-QUAL-03 |
| URS-QUAL-04 | FS-QUAL-04 |
| URS-PM-01 | FS-PM-01 |
| URS-PM-02 | FS-PM-02 |
| URS-PM-03 | FS-PM-03 |
| URS-PM-04 | FS-PM-04 |
| URS-PM-05 | FS-PM-05 |
| URS-PM-06 | FS-PM-06 |
| URS-PM-07 | FS-PM-07 |
| URS-WO-01 | FS-WO-01 |
| URS-WO-02 | FS-WO-02 |
| URS-WO-03 | FS-WO-03 |
| URS-WO-04 | FS-WO-04 |
| URS-WO-05 | FS-WO-05 |
| URS-WO-06 | FS-WO-06 |
| URS-CAL-01 | FS-CAL-01 |
| URS-CAL-02 | FS-CAL-02 |
| URS-CAL-03 | FS-CAL-03 |
| URS-CAL-04 | FS-CAL-04 |
| URS-CAL-05 | FS-CAL-05 |
| URS-PDM-01 | FS-PDM-01 |
| URS-PDM-02 | FS-PDM-02 |
| URS-PDM-03 | FS-PDM-03 |
| URS-PDM-04 | FS-PDM-04 |
| URS-PART-01 | FS-PART-01 |
| URS-PART-02 | FS-PART-02 |
| URS-PART-03 | FS-PART-03 |
| URS-PART-04 | FS-PART-04 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
| URS-PART11-01 | FS-PART11-01 |
| URS-PART11-02 | FS-PART11-02 |
| URS-PART11-03 | FS-PART11-03 |
| URS-PART11-04 | FS-PART11-04 |
| URS-PART11-05 | FS-PART11-05 |
| URS-PART11-06 | FS-PART11-06 |
| URS-PART11-07 | FS-PART11-07 |
| URS-PART11-08 | FS-PART11-08 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-04 | FS-DI-04 |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 |
| URS-INT-CAL-01 | FS-INT-CAL-01 |
| URS-INT-LIMS-01 | FS-INT-LIMS-01 |
| URS-INT-PDM-01 | FS-INT-PDM-01 |
| URS-INT-AD-01 | FS-INT-AD-01 |
| URS-PERF-01 | FS-PERF-01 |
| URS-AV-01 | FS-AV-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Missed PM on GxP-critical asset undetected | Medium | High | URS-PM-02 |
| R-02 | Incorrect asset GxP flag | Medium | High | URS-ASSET-01 |
| R-03 | WO-completion without supervisor sign-off | Medium | High | URS-WO-02 |
| R-04 | Failed calibration not surfaced | Low | Critical | URS-CAL-02 |
| R-05 | NIST standard expired during use | Low | High | URS-CAL-04 |
| R-06 | Non-qualified asset used in production | Low | Critical | URS-QUAL-02 |
| R-07 | PM auto-generation race producing duplicate WOs | Low | Medium | URS-PM-06 |
| R-08 | Audit-trail tampering | Low | Critical | URS-AUD-02 |
| R-09 | PdM rule false-negative misses developing failure | Medium | High | URS-PDM-02..04 |

Full evaluation in `PHX-RA-CMMS-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
