---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring 2026-05-15 (Chunk A ICP-MS)"
seed_corpus_basis:
  - "NWT-FS-ICPMS-001 v1.2 (parent FS)"
  - "NWT-URS-ICPMS-001 v1.2 (transitive parent URS)"
  - "GAMP 5 (2nd Edition) Category 4 — Configuration Specification"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "ICH Q3D(R2); USP <232>/<233>/<730>"
  - "Thermo Fisher — Qtegra ISDS 2.10 Pharma Compliance Configuration Guide (vendor)"
parent_fs:
  document_number: NWT-FS-ICPMS-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Northwind_Therapeutics_ICP-MS_Computer_System_FS_v1.3.md
parent_urs:
  document_number: NWT-URS-ICPMS-001
  version: 1.2
  file: ../../../URS/_generated/final/Northwind_Therapeutics_ICP-MS_Computer_System_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## ICP-MS Computer System — Thermo Fisher iCAP RQ + Qtegra ISDS 2.10

**Document Number:** NWT-DS-ICPMS-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** NWT-FS-ICPMS-001 v1.2 | **Parent URS:** NWT-URS-ICPMS-001 v1.2 *(informational, transitive)*
**Site:** Northwind Therapeutics Pvt. Ltd., QC Trace Analytics, Block C, Hinjewadi Phase II, Pune *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Thermo Fisher iCAP RQ + Qtegra ISDS 2.10** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192, .194(a)(8); EU GMP Annex 11 §§ 4, 6, 9, 11; ICH Q3D(R2); USP <232>/<233>/<730>; USP <1058>; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Trace Analytics) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Approver (Head of QC / System Owner) | _____________ | _____________ | _____ |
| Approver (Head of QA / Process Owner) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T2 from parent URS+FS pair. DS covers 77/80 FS-IDs; 3 FS-IDs flagged as vendor-internal — no site design surface (FS-AUD-01 Pharma-Compliance audit-trail engine schema, FS-PROC-01 Qtegra mass-bias / KED computation internals, FS-QNT-01 Qtegra Procedure-1 curve engine internals). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from `NWT-FS-ICPMS-001` and `NWT-URS-ICPMS-001`. DS-specific terms:

| Term | Definition |
|---|---|
| Tasklet | Qtegra workflow unit (vendor-supplied, site does not author) |
| Authority Set | Qtegra Pharma-Compliance internal role bundle, mapped 1:1 to an AD group |
| Tune Workflow | Qtegra Acquisition Tasklet sequence covering autotune + QPass + KED-mode checks |
| `wel-icpms` | Splunk heavy-index name reserved for this system's events |
| DCS | Drift Control Standard (USP <233>) |

## 1. Purpose

This Configuration Specification (CS) records the technical design that satisfies the functional behaviour in `NWT-FS-ICPMS-001` v1.2. It captures per-CI vendor-named parameters, chosen values, default-vs-custom flags, justification, FS-IDs traced, and IQ/OQ verification — followed by workflow/business-rule design (§ 5), role-permission matrix design (§ 6), integration design (§ 7), and the small site-deployed components (§ 8). Vendor internals of Qtegra ISDS / Pharma Compliance / TraceCERT remain Thermo Fisher's SDLC responsibility and are not redrawn.

## 2. Scope

### 2.1 In scope

- Qtegra ISDS 2.10 + TraceCERT + Pharma Compliance plugins configuration: project structure, authority sets, eSign policy, audit-trail bindings, method state machine, interference-equation set selection, internal-standard table binding, drift-QC schedule, USP <233> Procedure-1 / Procedure-2 engine binding, Q3D PDE-limit table per route of administration.
- Windows 11 / AD GPO baseline bounding the Qtegra workstation.
- Integration design for AD, NTP, NetApp SnapLock, Splunk SIEM, LabWare LIMS 8, and the Milestone UltraWAVE digestion-batch reference.
- Site-deployed components: one Qtegra pre-run validation tasklet extension (FS-ACQ-02) and one TraceCERT Q3D-PDE table extension (FS-QNT-04). Both treated as Cat 5-equivalent micro-SDS sub-sections in § 8.

### 2.2 Out of scope

- Vendor internals (Qtegra acquisition engine, KED collision-cell algorithm, Procedure-1 curve engine).
- LIMS-side configuration (validated under `LIMS-CSV-2025-014`).
- Milestone UltraWAVE digestion system (validated separately).

## 3. Architectural Overview

The CS layers seven configuration domains on top of FS § 3.2: (1) Windows/AD policy, (2) Qtegra project policy, (3) Qtegra authority sets, (4) Tune + drift policy, (5) Interference-equation set + internal-standard table bindings, (6) Q3D PDE-limit table per route of administration, (7) audit-trail and retention bindings. The figure below expands FS § 3.2 with configuration touchpoints (italic capital letters refer to § 4 CI rows).

```
                            AD `NWT.local` (qualified infra)
                            │
                            │ AD group → Qtegra Authority Set
                            │ (CI-15..CI-21)
                            ▼
       ┌──────────────────────────────────────────────────────────────┐
       │ Qtegra Workstation (Dell Precision 3680)                     │
       │   Win 11 Pro 22H2 (domain-joined)                            │
       │   GPO `GMP-Lab-Workstations` (CI-03, CI-04, CI-05, CI-06)    │
       │   ┌───────────────────────────────────────┐                  │
       │   │ Qtegra ISDS 2.10 + TraceCERT          │                  │
       │   │ + Pharma Compliance                    │                  │
       │   │   Project root path (CI-01)            │                  │
       │   │   RequireSignatureReAuth (CI-09)       │                  │
       │   │   BlockOnSstFailure (CI-24)            │                  │
       │   │   Authority Sets (CI-15..21)           │                  │
       │   │   Method state machine (CI-25)         │                  │
       │   │   Interference Eq Set (CI-30)          │                  │
       │   │   IS Table (CI-31)                     │                  │
       │   │   Q3D PDE Table (CI-32)                │                  │
       │   │   Drift-QC schedule (CI-33)            │                  │
       │   └────┬──────────────────────────────────┘                  │
       │        │ USB-3 to iCAP RQ + ASX-560 (FS-HW-01/02)             │
       │        │ SMB to file share                                    │
       └────────┼──────────────────────────────────────────────────────┘
                │
                │                       ┌──────────────────────────────┐
                ├──────► NTP ──────────►│ ntp.nwt.local (CI-22)        │
                │                       └──────────────────────────────┘
                │                       ┌──────────────────────────────┐
                ├──────► SMB 3.1.1 ────►│ \\nwt-gmp-fs02\qtegra-       │
                │      (FS-FS-01)       │ projects                     │
                │                       │ NetApp SnapLock Compliance   │
                │                       │ Retention 7y / 25y (CI-37)   │
                │                       └──────────────────────────────┘
                │                       ┌──────────────────────────────┐
                ├──────► TCP/9997 ─────►│ Splunk UF → heavy index      │
                │      (FS-SW-04)       │ `wel-icpms` (CI-38)          │
                │                       └──────────────────────────────┘
                │                       ┌──────────────────────────────┐
                ├──────► HTTPS/mTLS ───►│ LabWare LIMS 8 via Qtegra    │
                │      (FS-INT-*)       │ LIMS Connector 1.6 (CI-40..) │
                │                       └──────────────────────────────┘
                │                       ┌──────────────────────────────┐
                └─ FK reference ───────►│ Milestone UltraWAVE batch    │
                       (FS-PREP-01)     │ system (read-only ref)       │
                                        └──────────────────────────────┘
```

## 4. Configuration Specification

One row per Configuration Item. Vendor-named CIs follow *Thermo Fisher Qtegra ISDS 2.10 Pharma Compliance Configuration Guide* (rev. 2024-08) and *Qtegra LIMS Connector 1.6 Installation and Configuration Guide* (rev. 2024-06).

| CI-ID | Configuration item (named per vendor) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| CI-01 | Qtegra → Application Settings → `Project root path` | `\\nwt-gmp-fs02\qtegra-projects` | Custom | All GMP project data on WORM-tier share; vendor default `C:\Qtegra\Projects` not 7-y immutable. | FS-SW-03, FS-AUD-04 | IQ-CFG-01 |
| CI-02 | Qtegra → Application Settings → `Local Project Cache (GB)` | `50` | Custom | Bounded cache; prevents pre-sync silent loss; aligns FS-SW-03. | FS-SW-03 | IQ-CFG-02 |
| CI-03 | GPO `GMP-Lab-Workstations` → Screen-saver lock timeout (min) | `10` | Custom | Per FS-SW-07. | FS-SW-07 | IQ-GPO-01 |
| CI-04 | GPO `Disable-Local-Accounts` | `Enabled` (only `NWT\bg-admin` retained) | Custom | Per FS-SW-01, FS-PART11-04, FS-SEC-01. | FS-SW-01, FS-PART11-04, FS-SEC-01 | IQ-GPO-02 |
| CI-05 | GPO Audit Policy (Logon / Account-Mgmt / Object-Access) | `All Success + Failure` | Custom | Forwards to Splunk per FS-SW-04. | FS-SW-04, FS-PART11-05 | IQ-GPO-03 |
| CI-06 | GPO `GMP-Firewall` | `GMP-Segment baseline` deny-by-default | Custom | Per FS-SEC-05. | FS-SEC-05 | IQ-GPO-04 |
| CI-07 | Qtegra Pharma Compliance → Project Policy bundle | `RawDataLock=ON; eSign=ON; Audit=ON; RFC=ON` | Custom | Per FS-AUD-01 / FS-PROC-02 / FS-PART11-08. | FS-AUD-01, FS-PROC-02, FS-PART11-08 | IQ-CFG-03 |
| CI-08 | Qtegra → RawData artefact ACL | `nwt-svc-qtegra-acq` write @ acquire; read-only after close; deny-delete | Custom | Implements FS-PROC-03 / FS-DI-04 on NTFS. | FS-PROC-03, FS-DI-04 | IQ-CFG-04 |
| CI-09 | Qtegra Pharma Compliance → `RequireSignatureReAuth` | `true` | Custom | Per FS-PART11-11; cached creds dropped. | FS-PART11-11 | OQ-PART11-11 |
| CI-10 | Qtegra Pharma Compliance → Meaning-of-Signature closed list | `Review, Approve, Reject, Lock` | Custom | Per FS-PART11-08. | FS-PART11-08 | OQ-PART11-08 |
| CI-11 | Qtegra Pharma Compliance → Signature hash | `SHA-256` | Default | Vendor default; satisfies FS-PART11-09. | FS-PART11-09, FS-DI-04 | OQ-PART11-09 |
| CI-12 | Qtegra Pharma Compliance → Reason-Code closed list | `mass-bias-recalc, IS-recalc, baseline-noise, integration-correction, instrument-glitch, sample-prep-error, drift-rework, other-with-justification` | Custom | Per FS-PROC-02 RFC capture. | FS-PROC-02 | OQ-PROC-02 |
| CI-13 | Qtegra DB → Audit-trail tables permissions | `INSERT/SELECT` only to `nwt-svc-qtegra-app`; deny-update/delete to all | Custom | Implements FS-AUD-02 append-only at DB layer. | FS-AUD-02 | IQ-CFG-05 |
| CI-14 | Qtegra Pharma Compliance → Retrospective-entry flag | `Enabled` (timestamp-divergence > 0 s flags entry) | Custom | Per FS-DI-03. | FS-DI-03 | OQ-DI-03 |
| CI-15 | Qtegra Authority Set ↔ AD-group → `Lab-ICPMS-Analysts` | `Analyst` (acquire / integrate / process; no method-edit; no Review/Approve eSign) | Custom | Per FS-PART11-06 / FS-PART11-13. | FS-PART11-06, FS-PART11-13 | OQ-ROLE-01 |
| CI-16 | Qtegra Authority Set ↔ `Lab-ICPMS-Senior` | `Senior` (Analyst + Review eSign) | Custom | Per FS-PART11-06. | FS-PART11-06 | OQ-ROLE-02 |
| CI-17 | Qtegra Authority Set ↔ `Lab-ICPMS-MethodOwners` | `MethodOwner` (method create/edit + interference-eq table + IS table) | Custom | Per FS-ACQ-01 / FS-MTH-02. | FS-ACQ-01, FS-MTH-02, FS-INTF-01 | OQ-ROLE-03 |
| CI-18 | Qtegra Authority Set ↔ `Lab-ICPMS-Manager` | `QCManager` (Approve eSign; LimsExport flip) | Custom | Per FS-INT-02. | FS-INT-02, FS-MTH-02 | OQ-ROLE-04 |
| CI-19 | Qtegra Authority Set ↔ `Lab-ICPMS-Auditor` | `Auditor` (read-only; PDF export) | Custom | Per FS-AUD-05. | FS-AUD-05 | OQ-ROLE-05 |
| CI-20 | Qtegra Authority Set ↔ `Lab-ICPMS-SysAdmin` | `SysAdmin` (config + plugin mgmt; no Approve eSign) | Custom | Per FS-PART11-13 operator/approver split. | FS-PART11-13 | OQ-ROLE-06 |
| CI-21 | Qtegra Pharma Compliance → `Concurrent Authority Hold` | `Single-Authority-Set per user on project` | Custom | Per FS-PART11-13. | FS-PART11-13 | OQ-ROLE-07 |
| CI-22 | Windows Time service → NTP source | `ntp.nwt.local`; skew threshold `1 s` | Custom | Per FS-SW-06. | FS-SW-06 | IQ-NTP-01 |
| CI-23 | Qtegra Tune workflow → `TuneCheck Tasklet` schedule | At sequence start; bracket-end for sequences ≥ 60 inj (CI-26) | Custom | Per FS-SST-01 / FS-SST-03. | FS-SST-01, FS-SST-03 | OQ-SST-01 |
| CI-24 | Qtegra Pharma Compliance → `BlockOnSstFailure` | `true` | Custom | Per FS-ACQ-05 / FS-SST-02. | FS-ACQ-05, FS-SST-02 | OQ-SST-02 |
| CI-25 | Qtegra Method State Machine | `DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE` (Author ≠ Reviewer ≠ Approver) | Custom | Per FS-MTH-01 / FS-MTH-02. | FS-MTH-01, FS-MTH-02 | OQ-MTH-01 |
| CI-26 | Qtegra Tune workflow → Bracketed-tune trigger | `Sequence length ≥ 60 injections` | Custom | Per FS-SST-03. | FS-SST-03 | OQ-SST-03 |
| CI-27 | Qtegra Tune workflow → Tune-criteria thresholds (method-bound default) | `CeO/Ce ≤ 3.0%; Ba²⁺/Ba ≤ 3.0%; ¹¹⁵In ≥ 50 000 cps` | Custom | Per FS-SST-01 (method may override). | FS-SST-01 | OQ-SST-01 |
| CI-28 | Qtegra Drift-QC workflow → DCS schedule | `Start + End of analytical run; ± 20% acceptance` | Custom | Per FS-SST-04 (USP <233>). | FS-SST-04 | OQ-SST-04 |
| CI-29 | Qtegra Drift-QC workflow → Drift-QC injection cadence | `Every 10 samples; ± 20% acceptance; DRIFT_FAIL flag` | Custom | Per FS-INTF-04. | FS-INTF-04 | OQ-INTF-04 |
| CI-30 | Qtegra Method → Interference-Equation Set binding | Active set `NWT-IES-ICPMS-2026Q2` (k-factors per analyte version-controlled) | Custom | Per FS-INTF-01 / FS-MTH-04. | FS-INTF-01, FS-MTH-04 | OQ-INTF-01 |
| CI-31 | Qtegra Method → Internal-Standard Table binding | Active table `NWT-IS-ICPMS-2026Q2` (⁴⁵Sc low, ⁷²Ge / ¹¹⁵In mid, ²⁰⁹Bi high) | Custom | Per FS-INTF-03 / FS-MTH-04. | FS-INTF-03, FS-MTH-04 | OQ-INTF-03 |
| CI-32 | TraceCERT Q3D-PDE Table binding | Active table `NWT-Q3D-PDE-v2024` (oral / parenteral / inhalation; Class 1/2A/2B/3) | Custom | Per FS-QNT-04. | FS-QNT-04, FS-PROC-04 | OQ-QNT-04 |
| CI-33 | TraceCERT → KED-mode method flag enforcement | `Block sequence-start when method demands KED but plasma not in KED mode` | Custom | Per FS-INTF-02. | FS-INTF-02 | OQ-INTF-02 |
| CI-34 | TraceCERT → IS Drift Threshold | `± 30% of initial-cal IS ratio → IS_DRIFT` | Custom | Per FS-INTF-03. | FS-INTF-03 | OQ-INTF-03 |
| CI-35 | TraceCERT → Matrix-Effect Threshold | `± 25% on 1× / 2× / 4× dilution check → Method-Owner review` | Custom | Per FS-INTF-05. | FS-INTF-05 | OQ-INTF-05 |
| CI-36 | TraceCERT → Procedure-1 r² Floor | `0.99` (quantitative); flagged < 0.99 | Custom | Per FS-QNT-01. | FS-QNT-01 | OQ-QNT-01 |
| CI-37 | NetApp SnapLock Compliance → `qtegra-projects` retention | `7y` default; `25y` if metadata tag `retention=25y` | Custom | Per FS-AUD-04 / FS-PART11-03. | FS-AUD-04, FS-PART11-03 | IQ-FS-01 |
| CI-38 | Splunk UF → heavy index | `wel-icpms` (TCP/9997 outbound) | Custom | Per FS-SW-04, FS-PERF-04, FS-PART11-12, FS-INT-04. | FS-SW-04, FS-PERF-04, FS-PART11-12, FS-INT-04, FS-SEC-04 | IQ-SIEM-01 |
| CI-39 | viewLinc EM → SIEM webhook | `T<18 or T>22 or RH<30 or RH>60 → wel-icpms` | Custom | Per FS-HW-06. | FS-HW-06 | IQ-HW-06 |
| CI-40 | Qtegra LIMS Connector 1.6 → polling endpoint | `https://lims.nwt.local/api/v3/worklist?projectId=<id>&fromDate=<iso8601>` every 60 s | Custom | Per FS-INT-01. | FS-INT-01 | OQ-INT-01 |
| CI-41 | Qtegra LIMS Connector 1.6 → inbound service principal | `NWT\svc-qtegra-limsread` (read-only AD group) | Custom | Per FS-INT-01. | FS-INT-01 | IQ-INT-01 |
| CI-42 | Qtegra LIMS Connector 1.6 → push gating | `LimsExport == true && Approve eSign valid` | Custom | Per FS-INT-02. | FS-INT-02 | OQ-INT-02 |
| CI-43 | Qtegra LIMS Connector 1.6 → payload schema validator | `NWT-LIMS-PUSH-v3.json` (mandatory: reportId, instrumentId, methodId+ver, reviewerId, approverId) | Custom | Per FS-INT-03. | FS-INT-03 | OQ-INT-03 |
| CI-44 | Qtegra LIMS Connector 1.6 → failure-alert SLA | `5 min`; Splunk rule `wel-icpms-lims-failure` pages on-call | Custom | Per FS-INT-04. | FS-INT-04 | OQ-INT-04 |
| CI-45 | Site PKI → mTLS cert for LIMS push | `nwt-icpms-2026q2` (auto-rotate 1y) | Custom | Per FS-INT-02. | FS-INT-02 | IQ-PKI-01 |
| CI-46 | Cornerstone OnDemand → curriculum gating | `NWT-CURR-ICPMS-Analyst-v1` mandatory pre AD-group add | Custom | Per FS-TRN-01 / FS-TRN-02. | FS-TRN-01, FS-TRN-02 | IQ-LMS-01 |
| CI-47 | UPS APC SMT3000RM2UC → SNMP shutdown threshold | `20%` remaining | Custom | Per FS-HW-03. | FS-HW-03 | IQ-HW-03 |
| CI-48 | CrowdStrike Falcon → exclusion list | Thermo-approved Qtegra paths | Custom | Per FS-SW-05 / FS-SEC-04. | FS-SW-05, FS-SEC-04 | IQ-AV-01 |
| CI-49 | Workstation VLAN binding | `VLAN 412 (GMP-Lab)` | Custom | Per FS-HW-04. | FS-HW-04 | IQ-HW-04 |
| CI-50 | iCAP RQ utility-monitoring → Ar / He pressure window | `Ar 3.5–6.5 bar; He 0.7–1.0 bar`; alarm via Qtegra | Custom | Per FS-HW-05. | FS-HW-05 | IQ-HW-05 |
| CI-51 | Veeam B&R 12.1 → backup job | `qtegra-projects-daily` 02:00 UTC + SHA-256 + off-site immutable + S3 Object Lock + LTO-9 monthly | Custom | Per FS-BAK-01 / FS-XSYS-BAK-01. | FS-BAK-01, FS-BAK-04, FS-XSYS-BAK-01 | IQ-BAK-01 |
| CI-52 | Veeam SureBackup → quarterly restore test | QC witness sign-off on `NWT-PROC-BAK-RESTORE-001` | Custom | Per FS-BAK-02. | FS-BAK-02 | IQ-BAK-02 |
| CI-53 | DR Runbook binding | `NWT-RB-ICPMS-DR-001` RTO 8 BH | Custom | Per FS-BAK-03. | FS-BAK-03 | OQ-BAK-03 |
| CI-54 | Splunk Dashboard `wel-icpms-availability` | `99.0% business-hours target` | Custom | Per FS-PERF-04 / FS-DI-06. | FS-PERF-04, FS-DI-06 | OQ-PERF-04 |
| CI-55 | Splunk Alert `wel-icpms-lockout` | Trigger on AD lockout for `Lab-ICPMS-*` group | Custom | Per FS-PART11-12. | FS-PART11-12 | OQ-PART11-12 |
| CI-56 | AD Password Policy | 14-char min / 90-d rotation / history 24 / lockout 5/15 min/30 min | Custom | Per FS-SEC-02 / FS-PART11-12. | FS-SEC-02, FS-PART11-12 | IQ-AD-01 |
| CI-57 | GPO `Block-RemovableMedia` | `Denied` (override via CR `NWT-CR-IT-USB`) | Custom | Per FS-SEC-03. | FS-SEC-03 | IQ-GPO-05 |
| CI-58 | AD → HR Feed binding | `New SID on rehire` | Custom | Per FS-PART11-10. | FS-PART11-10 | IQ-AD-02 |
| CI-59 | Qtegra → Asset Register binding | One-to-one workstation-serial ↔ iCAP-serial ↔ ASX-serial | Custom | Per FS-HW-01. | FS-HW-01 | IQ-HW-01 |
| CI-60 | Dell Precision 3680 baseline spec | i7-14700 / 64 GB DDR5 / 2 TB NVMe / NVIDIA T1000 / 4×USB-3.2 | Custom | Per FS-HW-02. | FS-HW-02 | IQ-HW-02 |
| CI-61 | Qtegra Report Template Registry → `NWT-RPT-ICPMS-001-v1.0.qrt` | Active; PDF/A-3 with embedded fonts + ICC | Custom | Per FS-PROC-06 / FS-DI-02. | FS-PROC-06, FS-DI-02 | OQ-RPT-01 |
| CI-62 | Qtegra Report Template Registry → `NWT-RPT-ICPMS-AUDIT-001` | Active | Custom | Per FS-AUD-03. | FS-AUD-03 | OQ-RPT-02 |
| CI-63 | Qtegra Report → Re-Issue watermark template | `RE-ISSUED — supersedes <originalReportId>` | Custom | Per FS-PROC-07. | FS-PROC-07 | OQ-RPT-03 |
| CI-64 | Qtegra Method → Outlier rule (per-standard back-calc) | `±15% non-LOQ; flag STANDARD_OUTLIER` | Custom | Per FS-QNT-03. | FS-QNT-03 | OQ-QNT-03 |
| CI-65 | Qtegra Method → Spec-Flag Thresholds | `30% TREND / 50% OOT / 100% OOS` per PDE | Custom | Per FS-QNT-05 / FS-PROC-05. | FS-QNT-05, FS-PROC-05 | OQ-QNT-05 |
| CI-66 | Qtegra → Numeric precision | `IEEE-754 double` intermediate; rounding only at final report | Default | Per FS-QNT-04 / FS-PREP-02. | FS-QNT-04, FS-PREP-02 | OQ-QNT-04 |
| CI-67 | Periodic Review template binding | `NWT-PR-ICPMS-YYYYMMDD` (QC Mgr + QA Mgr) | Custom | Per FS-PR-01 / FS-PR-02. | FS-PR-01, FS-PR-02 | OQ-PR-01 |
| CI-68 | Validation Dossier binding | `NWT-VAL-ICPMS-001` | Custom | Per FS-PART11-01. | FS-PART11-01 | (admin) |
| CI-69 | Batch Export (PDF/A-3 + native `.qrt`) | Enabled | Default | Per FS-PART11-02. | FS-PART11-02 | OQ-PART11-02 |
| CI-70 | System-operation manual binding | `NWT-RB-ICPMS-OPS-001` | Custom | Per FS-PART11-07. | FS-PART11-07 | (admin) |
| CI-71 | OQ Stress-test protocol binding | `OQ-PERF-ICPMS-60inj-01` | Custom | Per FS-PERF-01 / FS-PERF-02 / FS-PERF-03. | FS-PERF-01, FS-PERF-02, FS-PERF-03 | OQ-PERF-01 |
| CI-72 | OQ Calculation-regression protocol binding | 10 ref × 4 elements per FS-DI-05 | Custom | Per FS-DI-05. | FS-DI-05 | OQ-DI-05 |
| CI-73 | Honeywell Voyager 1452g barcode reader → driver | HID keyboard-wedge; suffix `Enter` | Default | Used at sample-vial scan; per FS-ACQ-03 sample-id input. | FS-ACQ-03 | IQ-BC-01 |
| CI-74 | Qtegra Method → MatrixType validator | `MatrixType ∈ {drug-product, API, excipient, packaging}` enforced at sequence-start | Custom | Per FS-PREP-03. | FS-PREP-03 | OQ-PREP-03 |
| CI-75 | Qtegra Method → Digestion-batch FK validator | `digestion_batch_id` mandatory; missing → block | Custom | Per FS-PREP-01; implemented in pre-run validation tasklet (§ 8.1). | FS-PREP-01 | OQ-PREP-01 |

## 5. Workflow + Business-Rule Design

### 5.1 Method Lifecycle Workflow `QTG-WF-METHOD-ICPMS`

Implemented in Qtegra Pharma Compliance state machine (CI-25). Steps DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE. Author ≠ Reviewer ≠ Approver enforced server-side (CI-15..18, CI-21). Method record carries `interference_equation_set_id`, `internal_standard_table_id`, `calibration_standard_inventory_id` per FS-MTH-04 (CI-30, CI-31). Only EFFECTIVE selectable at sequence start.

### 5.2 Tune + SST Workflow `QTG-WF-TUNECHECK`

Per FS-SST-01..04. TuneCheck Tasklet (CI-23) runs at sequence start; bracket-end if length ≥ 60 inj (CI-26). Criteria CeO/Ce ≤ 3%, Ba²⁺/Ba ≤ 3%, ¹¹⁵In ≥ 50 000 cps (CI-27) — method may override per analyte. DCS injected at run start + end with ± 20% acceptance (CI-28). Verdict FAIL flips status `SST-FAILED` and Pharma-Compliance `BlockOnSstFailure` (CI-24) prevents results processing.

### 5.3 Drift + Interference Correction Workflow `QTG-WF-DRIFT-INTF`

Drift-QC injected every 10 samples (CI-29); ± 20% acceptance → `DRIFT_FAIL` flag. Interference equation set CI-30 applied at processing; KED-mode method flag enforced at sequence start (CI-33). IS ratio computed per injection vs initial calibration (CI-31); ± 30% deviation flags `IS_DRIFT` (CI-34). Matrix-effect check (1×/2×/4×) per CI-35.

### 5.4 USP <233> Procedure-1 + Procedure-2 Engines `QTG-WF-USP233`

Procedure-1 (quantitative): TraceCERT curve engine builds curve from ≥ 3 standards / analyte; r² floor 0.99 (CI-36); curve outliers flagged per CI-64. Procedure-2 (limit test): sample peak-area vs single standard at Q3D PDE limit; sample > standard → `EXCEEDS_LIMIT`. PDE table CI-32 selected per method-bound `RouteOfAdministration` (oral / parenteral / inhalation); mis-selection blocked.

### 5.5 Result Approval + LIMS Push Workflow `QTG-WF-APPROVE-LIMS`

1. Analyst processes data → state `PROCESSED`.
2. Senior eSign `Review` (FS-AUD-03 pre-condition for batch sign-off).
3. QC Manager eSign `Approve` → Pharma Compliance flips `LimsExport=true` (CI-42); payload signed with `nwt-icpms-2026q2` (CI-45).
4. Qtegra LIMS Connector 1.6 picks up record, validates schema CI-43, POSTs to `https://lims.nwt.local/api/v3/result` (mTLS).
5. On failure: alert CI-44 within 5 min.

### 5.6 Audit-Trail Review Workflow `QTG-WF-AUDIT-REVIEW`

Per FS-AUD-03: per-batch Senior review + monthly QC Manager review. Template CI-62 exported as PDF/A-3.

### 5.7 Sample Preparation Linkage `QTG-WF-PREP-LINK`

Per FS-PREP-01..03. Sequence-start validator (CI-75, § 8.1 tasklet) requires `digestion_batch_id` FK to Milestone UltraWAVE batch system; dilution factor captured per sample and applied at equation step (CI-66); `prep_deviation` flag propagated to result + LIMS payload (CI-74).

## 6. Role-Permission Matrix Design

Implements FS-PART11-06 / FS-PART11-13 / FS-AUD-05 at the Pharma Compliance Authority-Set layer. AD groups map 1:1 to Authority Sets (CI-15..21).

| Permission | Analyst | Senior | MethodOwner | QCManager | SysAdmin | Auditor |
|---|---|---|---|---|---|---|
| Acquire sequence | ✓ | ✓ | ✓ | ✓ | – | – |
| Apply interference correction (auto) | ✓ | ✓ | ✓ | ✓ | – | – |
| Manual reprocess (with RFC) | ✓ | ✓ | ✓ | ✓ | – | – |
| Process result | ✓ | ✓ | ✓ | ✓ | – | – |
| eSign `Review` | – | ✓ | – | – | – | – |
| eSign `Approve` (result) | – | – | – | ✓ | – | – |
| eSign `Approve` (method) | – | – | – | ✓ | – | – |
| eSign `Reject` | – | ✓ | – | ✓ | – | – |
| eSign `Lock` (project) | – | – | – | ✓ | – | – |
| Method create / edit | – | – | ✓ | – | – | – |
| Interference-Eq Set edit (CI-30) | – | – | ✓ | – | – | – |
| Internal-Standard Table edit (CI-31) | – | – | ✓ | – | – | – |
| Q3D PDE table edit (CI-32) | – | – | – | ✓ (with QA dual eSign) | – | – |
| Method state transition (Author→Reviewer→Approver) | – | – | (Author) | (Approver) | – | – |
| Flip `LimsExport` | – | – | – | ✓ | – | – |
| Qtegra config edit | – | – | – | – | ✓ | – |
| AD group membership change | – | – | – | – | ✓ (via ticket) | – |
| Read audit trail | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Export audit trail (PDF) | – | ✓ | – | ✓ | ✓ | ✓ |
| Read raw / processed / report | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

Hard constraint (CI-21): single Authority Set per user per project. Analyst + Senior or Analyst + QCManager combinations denied at provisioning (FS-PART11-13).

## 7. Integration Design

### 7.1 IF-AD-AUTH (LDAPS + Kerberos)

| Aspect | Design |
|---|---|
| Endpoint | `ldaps://nwt.local:636`; Kerberos KDC via SRV records |
| AuthN | Kerberos interactive logon; LDAPS bind for Pharma-Compliance authority resolution |
| Groups consumed | `Lab-ICPMS-Analysts`, `-Senior`, `-MethodOwners`, `-Manager`, `-SysAdmin`, `-Auditor` |
| Conditional Access | `Lab-Workstation Conditional Access (MFA on interactive logon)` per FS-XSYS-AD-01 |
| Audit binding | Logon / Logoff / Lockout / Password-Change forwarded to `wel-icpms` (CI-38, CI-55) |
| FS-IDs traced | FS-PART11-04, FS-PART11-06, FS-XSYS-AD-01 |

### 7.2 IF-NTP

| Aspect | Design |
|---|---|
| Endpoint | `ntp.nwt.local` UDP/123 |
| Skew threshold | `1 s` (CI-22) |
| Monitoring | w32time 35/29 → Splunk; alert on skew > 1 s |
| FS-IDs traced | FS-SW-06 |

### 7.3 IF-FS (NetApp SnapLock SMB 3.1.1)

| Aspect | Design |
|---|---|
| Endpoint | `\\nwt-gmp-fs02\qtegra-projects` (SMB 3.1.1, encrypted) |
| Retention | 7y default; 25y tag (CI-37) |
| WORM | SnapLock Compliance deny-delete/modify |
| Backup | Veeam daily (CI-51) + SHA-256 verify |
| FS-IDs traced | FS-SW-03, FS-AUD-04, FS-PART11-03 |

### 7.4 IF-SIEM (Splunk Universal Forwarder)

| Aspect | Design |
|---|---|
| Endpoint | UF → indexer cluster TCP/9997 |
| Heavy index | `wel-icpms` (CI-38) |
| Source-types | `WinEventLog:Security`, `WinEventLog:System`, `Qtegra:Audit`, `QtegraLIMSConnector:App` |
| Alert rules | `wel-icpms-lockout` (CI-55); `wel-icpms-lims-failure` (CI-44); `wel-icpms-availability` (CI-54); `wel-icpms-av` (CI-48) |
| FS-IDs traced | FS-SW-04, FS-PART11-05, FS-PART11-12, FS-INT-04, FS-PERF-04, FS-SEC-04 |

### 7.5 IF-LIMS-WORKLIST-IN + IF-LIMS-RESULT-OUT (LabWare LIMS 8 via Qtegra LIMS Connector 1.6)

| Aspect | Design |
|---|---|
| Inbound (worklist) | `https://lims.nwt.local/api/v3/worklist?projectId=<id>&fromDate=<iso8601>` polled 60 s (CI-40) |
| Outbound (push) | `https://lims.nwt.local/api/v3/result` mTLS via `nwt-icpms-2026q2` (CI-45) |
| AuthN inbound | OAuth2 client credentials + `NWT\svc-qtegra-limsread` (CI-41) |
| AuthN outbound | mTLS payload sign + OAuth2 client creds |
| Schema validator | `NWT-LIMS-PUSH-v3.json` (CI-43) |
| Retry policy | Exponential back-off 30 s / 1 min / 5 min; 3 fails → page (CI-44) |
| Idempotency | `reportId` |
| FS-IDs traced | FS-INT-01..04 |

### 7.6 IF-PREP-FK (Milestone UltraWAVE digestion-batch reference)

| Aspect | Design |
|---|---|
| Endpoint | Read-only FK lookup against `https://ultrawave.nwt.local/api/v1/batch/<id>` |
| AuthN | OAuth2 client credentials (Qtegra service principal) |
| Use | Sequence-start validator (§ 8.1) verifies `digestion_batch_id` resolves; missing → block |
| FS-IDs traced | FS-PREP-01 |

## 8. Site-Deployed Components (micro-SDS)

Two small site-developed components push this Cat 4 into a Cat 4 + Cat 5 hybrid sliver.

### 8.1 `QTG-TASKLET-PRECHECK-01` — Pre-Run Validation Tasklet Extension

| Field | Value |
|---|---|
| Type | Qtegra Tasklet Extension (C# plugin via Qtegra Pharma Compliance Tasklet SDK) |
| Responsibility | FS-ACQ-02 pre-run gating + FS-PREP-01 digestion-batch FK + FS-INTF-02 KED-mode check |
| Inputs | Sequence context (Qtegra) |
| Outputs | `OK` or `BLOCK <reason>` with audit-trail entry |
| Algorithm | `if !instrument.PlasmaReady: BLOCK "Plasma not Ready"; if method.state != "EFFECTIVE": BLOCK "Method not EFFECTIVE"; if project.lock: BLOCK "Project locked"; if !pressure_in_range(Ar,He): BLOCK "Argon/Helium pressure out of range"; if !digestion_batch_id.resolves(): BLOCK "Digestion batch missing"; if method.requires_KED && !plasma.KEDMode: BLOCK "KED mode required by method"; if calibration.expires_at < now(): BLOCK "Tune expired"; else OK` |
| Storage | Method library `Method Library\tasklets\` (MethodOwner write) |
| Unit-test | OQ-ACQ-02 (one per BLOCK branch + happy path) |
| FS-IDs traced | FS-ACQ-02, FS-PREP-01, FS-INTF-02, FS-HW-05 |

### 8.2 `QTG-PDE-EXT-Q3D-2024` — TraceCERT Q3D-PDE Table Extension

| Field | Value |
|---|---|
| Type | TraceCERT XML configuration extension (declarative) |
| Responsibility | FS-QNT-04 PDE table per route of administration |
| Inputs | Method-bound `RouteOfAdministration ∈ {oral, parenteral, inhalation}` |
| Outputs | Per-analyte PDE limit (µg/day) from ICH Q3D(R2) Table A.2.1 / A.2.2 / A.2.3 |
| Storage | `C:\Qtegra\Config\Q3D-PDE-2024.xml` (SysAdmin write) |
| Unit-test | OQ-QNT-04 (one selection per route × Class 1/2A/2B/3) |
| FS-IDs traced | FS-QNT-04, FS-PROC-04 |

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .68, .180, .192, .194(a)(8).
- FDA *Data Integrity and Compliance With cGMP* (2018).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.

### DACH
- Site Information Security Policy `NWT-IS-POL-PASSWORD`.

### International
- ISPE GAMP 5 (2nd Ed., 2022).
- ISPE GAMP GPG *Validation of Laboratory Computerized Systems*.
- USP <232> / <233> / <730> / <1058>.
- ICH Q3D(R2), ICH Q2(R2), ICH Q9(R1), ICH Q14.
- PIC/S PI 041.

### Vendor
- Thermo Fisher — *Qtegra ISDS 2.10 Pharma Compliance Configuration Guide* (rev. 2024-08).
- Thermo Fisher — *Qtegra LIMS Connector 1.6 Installation and Configuration Guide* (rev. 2024-06).
- Thermo Fisher — *iCAP RQ + Cetac ASX-560 Hardware Reference + Maintenance Guide*.
- Thermo Fisher — *TraceCERT Plugin Reference* (rev. 2024-08).
- Milestone — *UltraWAVE Closed-Vessel Microwave Digestion Reference*.

### Site / parent documents
- `NWT-FS-ICPMS-001 v1.2`; `NWT-URS-ICPMS-001 v1.2`.
- `NWT-VAL-ICPMS-001`, `NWT-PROC-BAK-RESTORE-001`, `NWT-RB-ICPMS-DR-001`, `NWT-RB-ICPMS-OPS-001`.

## Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) | Design intent (brief) | Verified by |
|---|---|---|---|
| DS-HW-01 | FS-HW-01 | Asset-register binding workstation/iCAP/ASX serials (CI-59) | IQ-HW-01 |
| DS-HW-02 | FS-HW-02 | Dell Precision 3680 baseline (CI-60) | IQ-HW-02 |
| DS-HW-03 | FS-HW-03 | UPS SMT3000RM2UC SNMP shutdown 20% (CI-47) | IQ-HW-03 |
| DS-HW-04 | FS-HW-04 | VLAN 412 binding (CI-49) | IQ-HW-04 |
| DS-HW-05 | FS-HW-05 | Ar/He pressure window + Qtegra alarm (CI-50; pre-run check § 8.1) | IQ-HW-05 |
| DS-HW-06 | FS-HW-06 | viewLinc 1-min + SIEM webhook (CI-39) | IQ-HW-06 |
| DS-SW-01 | FS-SW-01, FS-SEC-01, FS-PART11-04 | Win 11 22H2 image + AD-bind + local-admin disable (CI-04) | IQ-GPO-02 |
| DS-SW-02 | FS-SW-02 | Thermo install procedure THER-FS-PROC-2024-014 | IQ-INSTALL-01 |
| DS-SW-03 | FS-SW-03 | Project root + 50 GB local cache (CI-01, CI-02) | IQ-CFG-01 |
| DS-SW-04 | FS-SW-04, FS-PART11-05 | Audit policy + Splunk forwarding (CI-05, CI-38) | IQ-GPO-03 |
| DS-SW-05 | FS-SW-05, FS-SEC-04 | CrowdStrike exclusion list (CI-48) | IQ-AV-01 |
| DS-SW-06 | FS-SW-06 | NTP + 1 s skew (CI-22) | IQ-NTP-01 |
| DS-SW-07 | FS-SW-07 | Screen-saver-lock 10 min (CI-03) | IQ-GPO-01 |
| DS-ACQ-01 | FS-ACQ-01 | Method-library ACL + Method-Owner separation (CI-17) | OQ-ROLE-03 |
| DS-ACQ-02 | FS-ACQ-02 | Pre-run validation tasklet QTG-TASKLET-PRECHECK-01 (§ 8.1) | OQ-ACQ-02 |
| DS-ACQ-03 | FS-ACQ-03 | Sequence template fields + barcode scan (CI-73) | OQ-ACQ-03 |
| DS-ACQ-04 | FS-ACQ-04 | TuneCheck Tasklet schedule (CI-23) | OQ-SST-01 |
| DS-ACQ-05 | FS-ACQ-05 | BlockOnSstFailure (CI-24) | OQ-SST-02 |
| DS-ACQ-06 | FS-ACQ-06 | Pause/Resume audit event (Qtegra default) | OQ-ACQ-06 |
| DS-PROC-01 | (vendor-internal — Qtegra mass-bias / KED computation; site binds method only) | Interference Eq Set binding (CI-30) | OQ-INTF-01 |
| DS-PROC-02 | FS-PROC-02 | Reason-Code closed list (CI-12) | OQ-PROC-02 |
| DS-PROC-03 | FS-PROC-03, FS-DI-04 | RawData ACL flip immutable (CI-08) | OQ-PROC-03 |
| DS-PROC-04 | FS-PROC-04, FS-QNT-04 | Q3D PDE table binding per route (CI-32, § 8.2) | OQ-QNT-04 |
| DS-PROC-05 | FS-PROC-05 | Spec-flag thresholds 30/50/100% (CI-65) | OQ-QNT-05 |
| DS-PROC-06 | FS-PROC-06, FS-DI-02 | Report template PDF/A-3 (CI-61) | OQ-RPT-01 |
| DS-PROC-07 | FS-PROC-07 | Re-issue watermark (CI-63) | OQ-RPT-03 |
| DS-AUD-01 | (vendor-internal — Pharma-Compliance audit-trail engine event schema) | n/a (flagged) | n/a |
| DS-AUD-02 | FS-AUD-02 | Audit-trail DB INSERT-only + ACL (CI-13) | IQ-CFG-05 |
| DS-AUD-03 | FS-AUD-03 | Audit-trail review template (CI-62) | OQ-RPT-02 |
| DS-AUD-04 | FS-AUD-04, FS-PART11-03 | SnapLock 7y/25y (CI-37) | IQ-FS-01 |
| DS-AUD-05 | FS-AUD-05 | Auditor authority set (CI-19) | OQ-ROLE-05 |
| DS-PART11-01 | FS-PART11-01 | Validation dossier binding (CI-68) | (admin) |
| DS-PART11-02 | FS-PART11-02 | Batch export PDF/A-3 + .qrt (CI-69) | OQ-PART11-02 |
| DS-PART11-03 | FS-PART11-03 | SnapLock + Veeam (CI-37, CI-51) | IQ-FS-01 |
| DS-PART11-04 | FS-PART11-04 | AD-bound + local-admin disable (CI-04) | IQ-GPO-02 |
| DS-PART11-05 | FS-PART11-05 | Audit policy → Splunk (CI-05, CI-38) | IQ-GPO-03 |
| DS-PART11-06 | FS-PART11-06 | AD-group → Authority-Set (CI-15..20) | OQ-ROLE-01..06 |
| DS-PART11-07 | FS-PART11-07 | Ops manual + SCN CR binding (CI-70) | (admin) |
| DS-PART11-08 | FS-PART11-08 | Meaning-of-sig closed list (CI-10) | OQ-PART11-08 |
| DS-PART11-09 | FS-PART11-09 | SHA-256 signature payload (CI-11) | OQ-PART11-09 |
| DS-PART11-10 | FS-PART11-10 | AD SID-on-rehire (CI-58) | IQ-AD-02 |
| DS-PART11-11 | FS-PART11-11 | RequireSignatureReAuth (CI-09) | OQ-PART11-11 |
| DS-PART11-12 | FS-PART11-12, FS-SEC-02 | AD password policy + lockout alert (CI-56, CI-55) | OQ-PART11-12 |
| DS-PART11-13 | FS-PART11-13 | Single Authority Set per user (CI-21) | OQ-ROLE-07 |
| DS-DI-01 | FS-DI-01 | Pharma-Compliance attributes domain\user on every artefact (vendor default + CI-15..20 binding) | OQ-DI-01 |
| DS-DI-02 | FS-DI-02 | PDF/A-3 fonts + ICC (CI-61) | OQ-RPT-01 |
| DS-DI-03 | FS-DI-03 | Retrospective-entry flag (CI-14) | OQ-DI-03 |
| DS-DI-04 | FS-DI-04, FS-PROC-03 | RawData immutable on close (CI-08) | OQ-PROC-03 |
| DS-DI-05 | FS-DI-05 | OQ calculation regression protocol (CI-72) | OQ-DI-05 |
| DS-DI-06 | FS-DI-06, FS-PERF-04 | Availability dashboard (CI-54) | OQ-PERF-04 |
| DS-INT-01 | FS-INT-01 | LIMS Connector poll endpoint + service principal (CI-40, CI-41) | OQ-INT-01 |
| DS-INT-02 | FS-INT-02 | Push gate + mTLS cert (CI-42, CI-45) | OQ-INT-02 |
| DS-INT-03 | FS-INT-03 | Payload schema validator (CI-43) | OQ-INT-03 |
| DS-INT-04 | FS-INT-04 | Failure-alert SLA 5 min (CI-44) | OQ-INT-04 |
| DS-BAK-01 | FS-BAK-01, FS-BAK-04, FS-XSYS-BAK-01 | Veeam daily + SHA-256 + immutable + S3 + LTO (CI-51) | IQ-BAK-01 |
| DS-BAK-02 | FS-BAK-02 | Quarterly SureBackup (CI-52) | IQ-BAK-02 |
| DS-BAK-03 | FS-BAK-03 | DR runbook RTO 8 BH (CI-53) | OQ-BAK-03 |
| DS-BAK-04 | FS-BAK-04 | RPO 24 h | IQ-BAK-01 |
| DS-PERF-01 | FS-PERF-01 | OQ stress 60 inj (CI-71) | OQ-PERF-01 |
| DS-PERF-02 | FS-PERF-02 | Processing ≤ 10 min (CI-71) | OQ-PERF-02 |
| DS-PERF-03 | FS-PERF-03 | UI P95 ≤ 3 s (CI-71) | OQ-PERF-03 |
| DS-PERF-04 | FS-PERF-04 | Availability dashboard (CI-54) | OQ-PERF-04 |
| DS-SEC-01 | FS-SEC-01 | Break-glass quarterly + AD-only (CI-04) | IQ-GPO-02 |
| DS-SEC-02 | FS-SEC-02 | AD password policy (CI-56) | IQ-AD-01 |
| DS-SEC-03 | FS-SEC-03 | GPO Block-RemovableMedia (CI-57) | IQ-GPO-05 |
| DS-SEC-04 | FS-SEC-04 | CrowdStrike daily + dashboard (CI-48) | IQ-AV-01 |
| DS-SEC-05 | FS-SEC-05 | GPO GMP-Firewall (CI-06) | IQ-GPO-04 |
| DS-TRN-01 | FS-TRN-01, FS-TRN-02 | Cornerstone gate (CI-46) | IQ-LMS-01 |
| DS-PR-01 | FS-PR-01, FS-PR-02 | Periodic-review template + dual eSign (CI-67) | OQ-PR-01 |
| DS-SST-01 | FS-SST-01 | TuneCheck Tasklet + thresholds (CI-23, CI-27) | OQ-SST-01 |
| DS-SST-02 | FS-SST-02 | Tune record + BlockOnSstFailure (CI-24) | OQ-SST-02 |
| DS-SST-03 | FS-SST-03 | Bracketed-tune trigger (CI-26) | OQ-SST-03 |
| DS-SST-04 | FS-SST-04 | DCS start+end ± 20% (CI-28) | OQ-SST-04 |
| DS-INTF-01 | FS-INTF-01 | Interference-Eq Set binding (CI-30) | OQ-INTF-01 |
| DS-INTF-02 | FS-INTF-02 | KED-mode check at sequence start (CI-33, § 8.1) | OQ-INTF-02 |
| DS-INTF-03 | FS-INTF-03 | IS table binding + drift threshold (CI-31, CI-34) | OQ-INTF-03 |
| DS-INTF-04 | FS-INTF-04 | Drift-QC every 10 samples ± 20% (CI-29) | OQ-INTF-04 |
| DS-INTF-05 | FS-INTF-05 | Matrix-effect threshold ± 25% (CI-35) | OQ-INTF-05 |
| DS-QNT-01 | (vendor-internal — Procedure-1 curve engine) + FS-QNT-01 r² floor configurable | r² floor 0.99 (CI-36) | OQ-QNT-01 |
| DS-QNT-02 | FS-QNT-02 | Procedure-2 limit-test engine (vendor) bound to PDE table (CI-32) | OQ-QNT-02 |
| DS-QNT-03 | FS-QNT-03 | Outlier rule ±15% (CI-64) | OQ-QNT-03 |
| DS-QNT-04 | FS-QNT-04 | PDE table + route validator (CI-32, § 8.2) | OQ-QNT-04 |
| DS-QNT-05 | FS-QNT-05 | Spec-flag thresholds (CI-65) | OQ-QNT-05 |
| DS-MTH-01 | FS-MTH-01 | Method state machine (CI-25) | OQ-MTH-01 |
| DS-MTH-02 | FS-MTH-02 | Author ≠ Reviewer ≠ Approver (CI-15..18, CI-21) | OQ-MTH-02 |
| DS-MTH-03 | FS-MTH-03 | Reprocess lineage (Qtegra default + audit) | OQ-MTH-03 |
| DS-MTH-04 | FS-MTH-04 | Method record schema bound to CI-30/31/32 | OQ-MTH-04 |
| DS-PREP-01 | FS-PREP-01 | Digestion-batch FK validator (CI-75, § 8.1) | OQ-PREP-01 |
| DS-PREP-02 | FS-PREP-02 | Dilution factor at equation step (CI-66) | OQ-PREP-02 |
| DS-PREP-03 | FS-PREP-03 | Prep-deviation flag + matrix validator (CI-74) | OQ-PREP-03 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 | LDAPS + Kerberos + Conditional Access + SIEM (§ 7.1) | IQ-AD-01..02 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 | Veeam T2 + S3 Object Lock + LTO-9 (CI-51) | IQ-BAK-01 |

## Appendix B — Design-level Risk Register

| ID | Risk | Likelihood | Impact | Mitigation reference | Design surface |
|---|---|---|---|---|---|
| DR-01 | Interference-Eq Set (CI-30) version not updated when KED mode toggled per analyte → silent under-correction of polyatomic interference | Medium | Critical | Method-Owner change-control + post-edit OQ-INTF-01 re-test | CI-30, CI-33 |
| DR-02 | Q3D PDE table (CI-32) `RouteOfAdministration` field mis-mapped at method build → wrong PDE limit applied | Low | Critical | Method-build validator (§ 8.2) requires explicit selection; OQ-QNT-04 exercises all three routes | CI-32, § 8.2 |
| DR-03 | Authority-Set ↔ AD-group binding drift (rename of AD group without Pharma-Compliance re-bind) | Low | Critical | Quarterly access review (FS-PR-01) + Pharma-Compliance authority export reconciled with AD | CI-15..20 |
| DR-04 | SnapLock retention metadata `retention=25y` mis-applied on batch-linked projects | Low | Critical | Pre-backup metadata-tag verification in Veeam hook | CI-37 |
| DR-05 | mTLS cert `nwt-icpms-2026q2` expiry blocks LIMS push silently | Low | High | 30-day pre-expiry pager alert + auto-rotation | CI-45, CI-44 |
| DR-06 | Pre-run tasklet (§ 8.1) silently fails-open on plugin exception | Low | Critical | Plugin authored with default-BLOCK on exception; OQ-ACQ-02 includes negative-path test | § 8.1, CI-75 |
| DR-07 | Reason-Code list growth (CI-12) outside change control dilutes audit | Medium | Medium | Quarterly review of reason-code distribution in `wel-icpms` | CI-12 |
| DR-08 | SCN upgrade reverts vendor-default CI (e.g., `Signature hash` CI-11 to SHA-1) | Low | Critical | Post-upgrade IQ delta-check across all 75 CIs + FS-PART11-09 re-test | CI-09, CI-11 |
| DR-09 | KED-mode check (CI-33) bypassed when method's `requires_KED` flag mis-set at method build | Low | High | Method-build validator enforces flag-vs-equation-set consistency at promotion to APPROVED | CI-33, CI-30 |
| DR-10 | Drift-QC schedule (CI-29) cadence widened in production due to throughput pressure | Low | High | Cadence pinned at method level (MethodOwner-only edit); deviation flagged in periodic review | CI-29 |
| DR-11 | VLAN 412 mis-tagged at switch allowing office-VLAN routing | Low | High | Network IQ-HW-04 traceroute fails to office-segment host | CI-49 |
| DR-12 | Splunk index `wel-icpms` retention < 7 y due to indexer-cluster sizing pressure | Low | High | SIEM IDS retention pin + quarterly audit | CI-38 |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
