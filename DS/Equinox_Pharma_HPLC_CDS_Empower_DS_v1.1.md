---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring 2026-05-15 (Chunk A Empower)"
seed_corpus_basis:
  - "EQX-FS-EMPOWER-001 v1.2 (parent FS)"
  - "EQX-URS-EMPOWER-001 v1.2 (transitive parent URS)"
  - "GAMP 5 (2nd Edition) Category 4 — Configuration Specification"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "USP <621>; USP <1058>; USP <1224>-<1226>"
  - "Waters — Empower 3 FR5 System Administrator's Guide + Empower 3 FR5 Configuration Reference (vendor doc)"
  - "Waters — Empower-LIMS Connector 4.2 Installation and Configuration Guide"
parent_fs:
  document_number: EQX-FS-EMPOWER-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Equinox_Pharma_HPLC_CDS_Empower_FS_v1.3.md
parent_urs:
  document_number: EQX-URS-EMPOWER-001
  version: 1.2
  file: ../../../URS/_generated/final/HPLC_CDS_Empower_Computer_System__Equinox_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## HPLC Chromatography Data System — Waters Empower 3 FR5 (Networked, Citrix-published)

**Document Number:** EQX-DS-EMPOWER-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** EQX-FS-EMPOWER-001 v1.2 | **Parent URS:** EQX-URS-EMPOWER-001 v1.2 *(informational, transitive)*
**Site:** Equinox Pharma GmbH, QC HPLC Cluster, Stuttgart, Germany *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Waters Empower 3 FR5 (Networked, Citrix-published)** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192, .194(a)(8); EU GMP Annex 11 §§ 4, 6, 9, 11; USP <621>; USP <1058>; ICH Q2(R2); ICH Q9(R1); ICH Q14; PIC/S PI 041; BfArM

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Chromatography) | _____________ | _____________ | _____ |
| Reviewer (Empower System Administrator / Oracle DBA) | _____________ | _____________ | _____ |
| Reviewer (Citrix Architect) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Approver (Head of QA / Process Owner) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T2 from parent URS+FS pair. DS covers 88/92 FS-IDs; 4 FS-IDs flagged as vendor-internal — no site design surface (FS-AUD-01 Empower audit-trail event schema, FS-QNT-01 Empower curve-engine internals, FS-RPR-01 Empower reason-for-change dialog UI internals, FS-PROC-04 Empower spec-comparison rule engine internals). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from `EQX-FS-EMPOWER-001` and `EQX-URS-EMPOWER-001`. DS-specific terms:

| Term | Definition |
|---|---|
| Authority Set | Empower's internal name for a role's allowed-action bundle, mapped 1:1 to an AD group |
| `.eax` | Empower self-contained project archive bundle |
| LAC/E | Lab Acquisition and Control Engine (acquisition node) |
| RFC | Reason-for-Change capture feature in Empower |
| Spec-Set | Empower configuration object holding per-analyte limit thresholds (30/50/100%) |
| `wel-empower` | Splunk heavy-index name reserved for this system's events |

## 1. Purpose

This CS records the configuration design that satisfies `EQX-FS-EMPOWER-001` v1.2 — namely the Empower 3 FR5 server cluster (active + DR), 24 LAC/E acquisition nodes, Citrix-published client, Empower-LIMS Connector 4.2, and the supporting AD / NTP / SnapLock / Splunk integration. Each CI carries vendor-named parameter, chosen value, default-vs-custom flag, justification, FS-IDs traced, and the planned IQ/OQ test. Workflow, role-permission, integration, and site-deployed-component design follow in §§ 5–8. Vendor internals (Empower core, Oracle GRANT model implementation, Citrix ICA) remain Waters'/Microsoft's/Citrix's SDLC responsibility and are not redrawn.

## 2. Scope

### 2.1 In scope

- Empower 3 FR5 server cluster configuration: DB schema policy, role/authority sets, project policy (`Raw Data Lock=ON, eSign=ON, Audit=ON, RFC=ON`), method state machine, project-naming convention, SST evaluator, curve-engine r² floor, spec-set thresholds, federation grant table.
- LAC/E node baseline (×24): Windows + Waters install, GPO, AV exclusion list.
- Citrix-published client: fixed-version published image, non-persistent profiles.
- Empower-LIMS Connector 4.2 configuration.
- Oracle 19c policy: archived redo, RMAN backup schedule, audit-table GRANT model.
- Integration design: AD, NTP, NetApp SnapLock cold storage, Splunk SIEM, Kafka publish to Helios.

### 2.2 Out of scope

- Vendor internals (Empower core, eSign ledger, audit-trail engine, curve engine, RFC UI).
- LIMS-side configuration (validated under `LIMS-CSV-2025-014`).
- Physical instruments + detectors (instrument-level qualifications).

## 3. Architectural Overview

The CS layers eight configuration domains on top of FS § 3.2: (1) Empower server-cluster topology + Oracle, (2) LAC/E × 24 baseline, (3) Citrix publishing, (4) project / method / role bindings, (5) integration bindings, (6) audit + retention bindings, (7) federation bindings, (8) Helios audit-trail publish. The figure below expands FS § 3.2 with config touchpoints (italic CI-XX refers to § 4).

```
                         AD `equinox.local` (qualified infra)
                         │
                         │ LDAPS (svc) + Kerberos (Citrix interactive)
                         ▼
   ┌──────────────────────────────────────────────────────────────────┐
   │                Empower 3 FR5 Production Cluster                  │
   │  ┌──────────────────────────┐  ┌────────────────────────────┐    │
   │  │ App Server (active)      │  │ DB Server (Oracle 19c)     │    │
   │  │   ForceReAuthOnSig CI-09 │◄─┤  Audit-table GRANT (CI-13) │    │
   │  │   Project Policy bundle  │  │  RMAN backup (CI-50)       │    │
   │  │   Authority Sets         │  │  Data Guard → DR cluster   │    │
   │  │   (CI-15..21)            │  └────────────────────────────┘    │
   │  └─────────────┬────────────┘                                     │
   │                │                                                  │
   │   ┌────────────▼─────────────────────────────────────────────┐    │
   │   │ 24 × LAC/E acquisition nodes (CI-30..32)                  │    │
   │   │   GPO `GMP-LACE-Baseline` (CI-03..06)                     │    │
   │   └───────────────────────────────────────────────────────────┘    │
   │   ┌───────────────────────────────────────────────────────────┐    │
   │   │ Citrix Virtual Apps publishing Empower client (CI-33..35) │    │
   │   └───────────────────────────────────────────────────────────┘    │
   └────────┬─────────────────────────────────────────────────────────┘
            │
            │              ┌────────────────────────────────┐
            ├── NTP ──────►│ ntp.equinox.local (CI-22)      │
            │              └────────────────────────────────┘
            │              ┌────────────────────────────────┐
            ├── RMAN/SMB ─►│ NetApp SnapLock (25y immutable │
            │   + S3 obj-lock│ cold storage) (CI-50, CI-51) │
            │              └────────────────────────────────┘
            │              ┌────────────────────────────────┐
            ├── TCP/9997 ─►│ Splunk UF → `wel-empower`      │
            │              │ (CI-40)                        │
            │              └────────────────────────────────┘
            │              ┌────────────────────────────────┐
            ├── HTTPS/mTLS►│ LabWare LIMS 8 via Empower-    │
            │              │ LIMS Connector 4.2 (CI-43..46) │
            │              └────────────────────────────────┘
            │              ┌────────────────────────────────┐
            ├── Kafka ────►│ `helios.ingest.equinox.empower │
            │              │  .v1` (CI-60..62)              │
            │              └────────────────────────────────┘
            │              ┌────────────────────────────────┐
            └── LDAPS ────►│ Federated partner Empower      │
                           │ instance (BG; CI-55..56)       │
                           └────────────────────────────────┘
```

## 4. Configuration Specification

One row per CI. Vendor-named CIs follow *Waters Empower 3 FR5 System Administrator's Guide* (rev. 2024-09) and *Empower-LIMS Connector 4.2 Installation and Configuration Guide* (rev. 2024-06).

| CI-ID | Configuration item (named per vendor) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| CI-01 | Empower → Configuration Manager → Project Policy `Raw Data Lock` | `ON` | Custom | Vendor default OFF; all GxP projects per FS-SW-03 / FS-PROC-03 / FS-DI-04. | FS-SW-03, FS-PROC-03, FS-DI-04, FS-EMP-01 | OQ-PROJECT-POLICY-01 |
| CI-02 | Empower → Configuration Manager → Project Policy `eSign / Audit / Reason-for-Change` | `ALL=ON` | Custom | Per FS-EMP-01 / FS-AUD-01. | FS-SW-03, FS-EMP-01, FS-AUD-01, FS-RPR-01 | OQ-PROJECT-POLICY-01 |
| CI-03 | GPO `GMP-LACE-Baseline` → Local-admin disable | Enabled (only `equinox\bg-emp-admin` retained) | Custom | Per FS-SEC-01 / FS-PART11-04. | FS-SEC-01, FS-PART11-04 | IQ-GPO-02 |
| CI-04 | GPO Audit Policy (Logon / Account-Mgmt / Object-Access) | `All Success + Failure` | Custom | Forwards to Splunk per FS-AUD-01 / FS-PART11-05. | FS-PART11-05 | IQ-GPO-03 |
| CI-05 | GPO `GMP-Firewall` → segment ruleset | App-DB / LAC/E / Citrix three-VLAN baseline | Custom | Per FS-SEC-05. | FS-SEC-05 | IQ-GPO-04 |
| CI-06 | GPO `Block-RemovableMedia` on LAC/E + Citrix workers | Denied (override CR `EQX-CR-IT-USB-EMP`) | Custom | Per FS-SEC-03. | FS-SEC-03 | IQ-GPO-05 |
| CI-07 | Empower → Project-Naming Convention validator | `<PROGRAMME>-<PRODUCT>-<TYPE>` regex enforced at project-create | Custom | Per FS-EMP-01. | FS-EMP-01 | OQ-EMP-01 |
| CI-08 | Empower → AD-role-map file `empower-role-map.yaml` | Version-controlled in git; quarterly review | Custom | Per FS-EMP-02. | FS-EMP-02 | OQ-EMP-02 |
| CI-09 | Empower → System Policies → `ForceReAuthOnSignature` | `true` | Custom | Per FS-PART11-11. | FS-PART11-11 | OQ-PART11-11 |
| CI-10 | Empower → eSign → Meaning-of-Signature closed list | `Review, Approve, Reject, Lock` | Custom | Per FS-PART11-08. | FS-PART11-08 | OQ-PART11-08 |
| CI-11 | Empower → eSign → Signature hash algorithm | `SHA-256` | Default | Per FS-PART11-09. | FS-PART11-09 | OQ-PART11-09 |
| CI-12 | Empower → Reason-for-Change closed-list reasons | `baseline-noise, co-elution, peak-shoulder, wrong-integration-window, instrument-glitch, sample-prep-error, calibration-overdue, other-with-justification` | Custom | Per FS-PROC-02 / FS-RPR-01. | FS-PROC-02, FS-RPR-01 | OQ-REINTEGRATE-REASON-01 |
| CI-13 | Oracle 19c → Audit-table GRANT model | `INSERT only` to Empower service role; `UPDATE/DELETE denied` to all roles | Custom | Implements FS-AUD-02 at the database level. | FS-AUD-02 | OQ-AUD-APPENDONLY-01 |
| CI-14 | Empower → Audit-Trail → Retrospective-entry flag | `Enabled` (timestamp-divergence flags entry) | Custom | Per FS-DI-03. | FS-DI-03 | OQ-DI-03 |
| CI-15 | Empower Authority Set ↔ AD-group → `Lab-Empower-Analysts` | `Analyst` (acquire / integrate / process; no method-edit; no Review eSign) | Custom | Per FS-PART11-06 / FS-PART11-13. | FS-PART11-06, FS-PART11-13 | OQ-ROLE-01 |
| CI-16 | Empower Authority Set ↔ `Lab-Empower-Senior` | `Senior` (Analyst + Review eSign) | Custom | Per FS-PART11-06. | FS-PART11-06 | OQ-ROLE-02 |
| CI-17 | Empower Authority Set ↔ `Lab-Empower-MethodOwners` | `MethodOwner` (method create/edit) | Custom | Per FS-ACQ-01 / FS-MTH-02. | FS-ACQ-01, FS-MTH-02 | OQ-ROLE-03 |
| CI-18 | Empower Authority Set ↔ `Lab-Empower-QCManagers` | `QCManager` (Approve eSign; LimsExport flip) | Custom | Per FS-INT-LIMS-02. | FS-INT-LIMS-02, FS-MTH-02 | OQ-ROLE-04 |
| CI-19 | Empower Authority Set ↔ `Lab-Empower-QAApprovers` | `QAApprover` (final release eSign) | Custom | Per FS-REL-01. | FS-REL-01 | OQ-ROLE-05 |
| CI-20 | Empower Authority Set ↔ `Lab-Empower-SysAdmin` | `SysAdmin` (configuration; no Approve eSign) | Custom | Per FS-PART11-13. | FS-PART11-13 | OQ-ROLE-06 |
| CI-21 | Empower Authority Set ↔ `Lab-Empower-Auditor` | `Auditor` (read-only) | Custom | Per FS-AUD-05. | FS-AUD-05 | OQ-ROLE-07 |
| CI-22 | Windows Time → NTP source | `ntp.equinox.local`; skew threshold 1 s | Custom | Per FS-SW-04. | FS-SW-04 | IQ-NTP-01 |
| CI-23 | Empower → Method State Machine | `DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE` (Author ≠ Reviewer ≠ Approver) | Custom | Per FS-ACQ-01 / FS-MTH-01 / FS-MTH-02. | FS-ACQ-01, FS-MTH-01, FS-MTH-02 | OQ-MTH-01 |
| CI-24 | Empower → Sequence-Start Validator | `instrument=Ready && method.state=EFFECTIVE && !project.lock` | Custom | Per FS-ACQ-02. | FS-ACQ-02 | OQ-ACQ-02 |
| CI-25 | Empower → SST Evaluator → criteria binding | Method-bound R / Tf / N / RT-RSD / Area-RSD on n=5 replicates | Custom | Per FS-SST-01. | FS-SST-01 | OQ-SST-01 |
| CI-26 | Empower → `BlockOnSstFailure` | `true` | Custom | Per FS-SST-02 / FS-ACQ-04. | FS-SST-02, FS-ACQ-04 | OQ-SST-02 |
| CI-27 | Empower → SST-Record schema binding | `criteria, observed, pass/fail-per-param, verdict, evaluator-version, sha256(sequence-id)` | Custom | Per FS-SST-03. | FS-SST-03 | OQ-SST-03 |
| CI-28 | Empower → Bracketed-SST mode trigger | `Sequence length ≥ 30 injections` | Custom | Per FS-SST-04. | FS-SST-04 | OQ-SST-04 |
| CI-29 | Empower → Calibration-curve r² floor | `0.99` (quantitative assay) | Custom | Per FS-QNT-01. | FS-QNT-01 | OQ-QNT-01 |
| CI-30 | LAC/E baseline → Win Server 2022 image | SCCM-deployed; domain-joined `equinox.local` | Custom | Per FS-SW-01 / FS-PLAT-03. | FS-SW-01, FS-PLAT-03 | IQ-LACE-01 |
| CI-31 | LAC/E baseline → UPS sizing | `30 min controlled shutdown` per LAC/E | Custom | Per FS-PLAT-02. | FS-PLAT-02 | IQ-LACE-02 |
| CI-32 | LAC/E baseline → CrowdStrike Falcon exclusion list | Waters-approved LAC/E paths | Custom | Per FS-SEC-04. | FS-SEC-04 | IQ-AV-01 |
| CI-33 | Citrix Virtual Apps → Empower published app | Fixed Empower 3 FR5 client version | Custom | Per FS-SW-05. | FS-SW-05 | IQ-CITRIX-01 |
| CI-34 | Citrix Virtual Apps → User Profile mode | `Non-persistent profile` | Custom | Per FS-SW-05. | FS-SW-05 | IQ-CITRIX-02 |
| CI-35 | Citrix Virtual Apps → Image-drift trigger | Re-validation event on Empower client version change | Custom | Per FS-SW-05. | FS-SW-05 | OQ-CITRIX-01 |
| CI-36 | Empower → Outlier rule (per-standard back-calc) | `±15% non-LOQ; ±20% LOQ → STANDARD_OUTLIER` | Default | Per FS-QNT-02. | FS-QNT-02 | OQ-QNT-02 |
| CI-37 | Empower → Spec-Set thresholds | `30% TREND / 50% OOT / 100% OOS` per analyte | Custom | Per FS-PROC-04 / FS-QNT-04. | FS-PROC-04, FS-QNT-04 | OQ-QNT-04 |
| CI-38 | Empower → Numeric precision | `IEEE-754 double` intermediate; rounding only at final report | Default | Per FS-QNT-03. | FS-QNT-03 | OQ-QNT-03 |
| CI-39 | Empower → Report template `EQX-RPT-EMP-001-v1.0` | Active; PDF/A-3 with embedded fonts + ICC | Custom | Per FS-PROC-05 / FS-DI-02. | FS-PROC-05, FS-DI-02 | OQ-RPT-01 |
| CI-40 | Splunk UF → heavy index | `wel-empower` (TCP/9997 outbound) | Custom | Per FS-AUD-01 / FS-PART11-05 / FS-AV-01 / FS-INT-LIMS-04. | FS-AUD-01, FS-PART11-05, FS-AV-01, FS-INT-LIMS-04, FS-SEC-04 | IQ-SIEM-01 |
| CI-41 | Splunk Dashboard `wel-empower-availability` | `99.5% business-hours target` | Custom | Per FS-AV-01. | FS-AV-01 | OQ-AV-01 |
| CI-42 | Splunk Alert `wel-empower-lockout` | Trigger on AD lockout for `Lab-Empower-*` | Custom | Per FS-PART11-12. | FS-PART11-12 | OQ-PART11-12 |
| CI-43 | Empower-LIMS Connector 4.2 → poll endpoint | `https://lims.equinox.local/api/v3/worklist` every 60 s | Custom | Per FS-INT-LIMS-01. | FS-INT-LIMS-01 | OQ-INT-01 |
| CI-44 | Empower-LIMS Connector 4.2 → inbound service principal | `equinox\svc-empower-limsread` (read-only AD group) | Custom | Per FS-INT-LIMS-01. | FS-INT-LIMS-01 | IQ-INT-01 |
| CI-45 | Empower-LIMS Connector 4.2 → push gate | `LimsExport == true && (Approve eSign valid && (QAApprover eSign valid if release-bound))` | Custom | Per FS-INT-LIMS-02 / FS-REL-01. | FS-INT-LIMS-02, FS-REL-01 | OQ-INT-02 |
| CI-46 | Empower-LIMS Connector 4.2 → payload schema | `EQX-LIMS-PUSH-EMP-v3.json` (mandatory fields per FS-INT-LIMS-03) | Custom | Per FS-INT-LIMS-03. | FS-INT-LIMS-03 | OQ-INT-03 |
| CI-47 | Empower-LIMS Connector 4.2 → failure-alert SLA | `5 min`; Splunk rule `wel-empower-lims-failure` | Custom | Per FS-INT-LIMS-04. | FS-INT-LIMS-04 | OQ-INT-04 |
| CI-48 | Site PKI → mTLS cert for LIMS push | `equinox-empower-2026q2` (auto-rotate 1y) | Custom | Per FS-INT-LIMS-02. | FS-INT-LIMS-02 | IQ-PKI-01 |
| CI-49 | LMS Cornerstone → curriculum gate | `EQX-CURR-EMP-Analyst-v1` mandatory pre AD-group add | Custom | Per FS-TRN-01 / FS-TRN-02. | FS-TRN-01, FS-TRN-02 | IQ-LMS-01 |
| CI-50 | Oracle 19c → RMAN backup schedule | Nightly full + continuous archived redo shipping to NetApp SnapLock cold | Custom | Per FS-BAK-01 / FS-PART11-03. | FS-BAK-01, FS-PART11-03 | IQ-DB-01 |
| CI-51 | NetApp SnapLock Compliance retention | `25y` (release-linked) / `7y` (general) | Custom | Per FS-AUD-04 / FS-PART11-03. | FS-AUD-04, FS-PART11-03 | IQ-FS-01 |
| CI-52 | Oracle Data Guard → standby DB Server | Active-passive failover; RPO ≤ 15 min via continuous redo | Custom | Per FS-PLAT-01 / FS-BAK-03. | FS-PLAT-01, FS-BAK-03 | IQ-DB-02 |
| CI-53 | DR Restore-test procedure binding | `EQX-PROC-EMP-RESTORE-001` quarterly + QA witness | Custom | Per FS-BAK-02. | FS-BAK-02 | IQ-BAK-02 |
| CI-54 | DR Annual full-failover drill | `Failover + DR-LACE acquisition + failback`, signed QC Mgr + IT Ops | Custom | Per FS-BAK-04. | FS-BAK-04 | OQ-BAK-04 |
| CI-55 | Empower Federation Grant Table | Per-project explicit grant rows; no implicit sharing | Custom | Per FS-FED-01. | FS-FED-01 | OQ-FED-01 |
| CI-56 | Empower Federation → write-attempt handler | `FED_READ_ONLY` error + audit-entry on remote write | Custom | Per FS-FED-02. | FS-FED-02 | OQ-FED-02 |
| CI-57 | Empower Federation Health Monitor | Lag > 24 h → Splunk alert; result-hash divergence → alert | Custom | Per FS-FED-03. | FS-FED-03 | OQ-FED-03 |
| CI-58 | AD Password Policy | 14-char min / 90-d rotation / history 24 / lockout 5/15 min/30 min | Custom | Per FS-SEC-02 / FS-PART11-12. | FS-SEC-02, FS-PART11-12 | IQ-AD-01 |
| CI-59 | AD HR Feed → SID-on-rehire | New SID on rehire | Custom | Per FS-PART11-10. | FS-PART11-10 | IQ-AD-02 |
| CI-60 | Helios Audit-Trail publisher → Kafka topic | `helios.ingest.equinox.empower.v1` (schema-registry pinned) | Custom | Per FS-XINT-HEL-01. | FS-XINT-HEL-01 | OQ-HEL-01 |
| CI-61 | Helios Audit-Trail publisher → idempotency key | `{source_system, event_id}` | Custom | Per FS-XINT-HEL-01. | FS-XINT-HEL-01 | OQ-HEL-01 |
| CI-62 | Helios Audit-Trail publisher → back-pressure alert | Prometheus `helios_publish_lag_seconds`; alert > 600 s sustained 5 min | Custom | Per FS-XINT-HEL-01. | FS-XINT-HEL-01 | OQ-HEL-02 |
| CI-63 | Helios Audit-Trail reconciliation job | Daily count parity; > 0.01% mismatch → MasterControl deviation | Custom | Per FS-XINT-HEL-02. | FS-XINT-HEL-02 | OQ-HEL-03 |
| CI-64 | Empower Method Lifecycle → MatrixType + ColumnLot validator | Block sequence-start on mismatch | Custom | Per FS-MTH-03. | FS-MTH-03 | OQ-MTH-03 |
| CI-65 | Empower Method-Change-Impact engine | Reports in-flight projects + result-sets touched; eSign before promotion | Custom | Per FS-MTH-04. | FS-MTH-04 | OQ-MTH-04 |
| CI-66 | Empower Reprocessing → diff-block tolerance | `0%` (any drift → `RESULT_DIFFERS_ON_REPROCESS` + dual eSign) | Custom | Per FS-RPR-03. | FS-RPR-03 | OQ-RPR-03 |
| CI-67 | Empower Result Lineage Export | DOT (graphviz) + JSON; included in `.eax` | Default | Per FS-RPR-04. | FS-RPR-04, FS-EMP-05 | OQ-RPR-04 |
| CI-68 | Empower Release Workflow eSign chain | Analyst → Senior → QC Mgr → QA Approver; held release expires 30 d | Custom | Per FS-REL-01..03. | FS-REL-01, FS-REL-02, FS-REL-03 | OQ-REL-01 |
| CI-69 | Empower Stability tagging validator | `stability_time_point + storage_condition` mandatory; mismatch flagged at Senior step | Custom | Per FS-REL-02. | FS-REL-02 | OQ-REL-02 |
| CI-70 | Empower Project-Rename eSign chain | QC Mgr + Head of QA dual eSign + alias preserved | Custom | Per FS-EMP-03. | FS-EMP-03 | OQ-EMP-03 |
| CI-71 | Empower Result-Method binding immutability | Locked on Senior review; rebind requires deviation | Custom | Per FS-EMP-04. | FS-EMP-04 | OQ-EMP-04 |
| CI-72 | Empower `.eax` archive scope | methods + raw + results + audit + sigs + lib pointers | Default | Per FS-EMP-05 / FS-PART11-02. | FS-EMP-05, FS-PART11-02 | OQ-EMP-05 |
| CI-73 | Validation Dossier binding | `EQX-VAL-EMPOWER-001` | Custom | Per FS-PART11-01. | FS-PART11-01 | (admin) |
| CI-74 | System-operation manual binding | `EQX-RB-EMP-OPS-001` | Custom | Per FS-PART11-07. | FS-PART11-07 | (admin) |
| CI-75 | Periodic-Review template binding | `EQX-PR-EMP-YYYYMMDD` (QC Mgr + Head of QA) | Custom | Per FS-PR-01 / FS-PR-02. | FS-PR-01, FS-PR-02 | OQ-PR-01 |
| CI-76 | OQ Calculation regression protocol binding | 20 ref × 3 analytes; ±0.01% spec limit | Custom | Per FS-DI-05. | FS-DI-05 | OQ-DI-05 |
| CI-77 | PQ Concurrent-acquisition protocol binding | `PQ-PERF-CONCURRENT-01` (24-instrument) | Custom | Per FS-PERF-01. | FS-PERF-01 | PQ-PERF-01 |
| CI-78 | Citrix APM agent → P95 latency capture | `Open project ≤ 10 s P95`; `Sequence-start ≤ 5 s P95` | Custom | Per FS-PERF-02 / FS-PERF-03. | FS-PERF-02, FS-PERF-03 | OQ-PERF-02 |
| CI-79 | LAC/E count (operational) | `24` LAC/E nodes; one per bench | Custom | Per FS-PLAT-01 / URS scope. | FS-PERF-01 | IQ-LACE-COUNT |

## 5. Workflow + Business-Rule Design

### 5.1 Method Lifecycle Workflow `EMP-WF-METHOD`

Implemented in Empower (CI-23). DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE. Author ≠ Reviewer ≠ Approver enforced server-side via Authority Sets (CI-15..18). MatrixType + ColumnLot enforcement (CI-64) at sequence start. Method-change-impact report (CI-65) eSigned before promotion.

### 5.2 Sequence Acquisition Workflow `EMP-WF-ACQ`

Sequence-start validator (CI-24) gates on instrument-Ready / method-EFFECTIVE / project-not-locked. SST (CI-25) runs at start; bracket-end for sequences ≥ 30 inj (CI-28). Verdict FAIL → `BlockOnSstFailure` (CI-26) blocks results acceptance. Per-injection metadata captured (FS-ACQ-03).

### 5.3 Reprocessing Workflow `EMP-WF-REPROCESS`

Per FS-RPR-01..04. Reason-for-Change closed list (CI-12) + free-text justification mandatory. Diff-block tolerance 0% (CI-66) — any drift triggers `RESULT_DIFFERS_ON_REPROCESS`. Method Owner + QC Manager dual eSign + deviation record required to unblock. Lineage exported per CI-67.

### 5.4 Release Workflow `EMP-WF-RELEASE`

4-eyes-plus-QA chain (CI-68): Analyst → Senior → QC Mgr → QA Approver. Stability tagging validator (CI-69) at Senior step. Held release records expire 30 d (CI-68 logic).

### 5.5 LIMS Push Workflow `EMP-WF-LIMS-PUSH`

Per FS-INT-LIMS-01..04. Worklist polled (CI-43); push gate (CI-45) requires QC Manager Approve eSign (and QA Approver eSign if release-bound); payload signed with mTLS cert CI-48; schema validator CI-46. Failures alerted within 5 min (CI-47).

### 5.6 Audit-Trail Review Workflow `EMP-WF-AUDIT-REVIEW`

Per FS-AUD-03: per-batch Senior review + monthly QC Manager review; PDF/A-3 + signed CSV export per CI-67-style template. Helios publish (CI-60..63) provides cross-system review backstop.

### 5.7 Federation Grant Workflow `EMP-WF-FEDERATION`

Per FS-FED-01..03. Federation Grant Table (CI-55) per-project; explicit grant only. Remote write attempts return `FED_READ_ONLY` (CI-56). Health monitor (CI-57) alerts on lag > 24 h or hash divergence.

### 5.8 Project Lifecycle Workflow `EMP-WF-PROJECT`

Project naming validator (CI-07); GxP project policy applied automatically (CI-01, CI-02); rename requires QC Mgr + Head of QA dual eSign (CI-70). Result-method binding locked at Senior review (CI-71). `.eax` archive (CI-72) covers methods + raw + results + audit + sigs + lib pointers.

## 6. Role-Permission Matrix Design

Implements FS-PART11-06 / FS-PART11-13 / FS-AUD-05 / FS-REL-01 at the Empower Authority-Set layer. AD groups bind 1:1 to Authority Sets (CI-15..21).

| Permission | Analyst | Senior | MethodOwner | QCManager | QAApprover | SysAdmin | Auditor |
|---|---|---|---|---|---|---|---|
| Acquire sequence | ✓ | ✓ | ✓ | ✓ | – | – | – |
| Integrate (auto) | ✓ | ✓ | ✓ | ✓ | – | – | – |
| Manual reintegrate (with RFC) | ✓ | ✓ | ✓ | ✓ | – | – | – |
| Process result | ✓ | ✓ | ✓ | ✓ | – | – | – |
| eSign `Review` | – | ✓ | – | – | – | – | – |
| eSign `Approve` (result) | – | – | – | ✓ | – | – | – |
| eSign `Approve` (method) | – | – | – | ✓ | – | – | – |
| eSign QA final release | – | – | – | – | ✓ | – | – |
| eSign `Reject` | – | ✓ | – | ✓ | ✓ | – | – |
| eSign `Lock` (project) | – | – | – | ✓ | – | – | – |
| Method create / edit | – | – | ✓ | – | – | – | – |
| Method state transition Author / Reviewer / Approver | – | – | (Author) | (Approver) | – | – | – |
| Project rename (with Head of QA dual eSign) | – | – | – | ✓ | – | – | – |
| Federation grant edit | – | – | – | ✓ | (QA dual) | – | – |
| Flip `LimsExport` | – | – | – | ✓ | – | – | – |
| Empower config edit (Authority Sets etc.) | – | – | – | – | – | ✓ | – |
| AD group membership change | – | – | – | – | – | ✓ (via ticket) | – |
| Read audit trail | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Export audit trail (PDF/CSV) | – | ✓ | – | ✓ | ✓ | ✓ | ✓ |
| Read raw / result / report | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

Hard constraint: Analyst on a result cannot also be the Reviewer or Approver on the same result; SysAdmin cannot Approve. Enforced server-side per FS-PART11-13 / FS-REL-01.

## 7. Integration Design

### 7.1 IF-AD (LDAPS + Kerberos via Citrix)

| Aspect | Design |
|---|---|
| Endpoint | `ldaps://equinox.local:636`; Kerberos KDC via SRV |
| AuthN | Citrix interactive Kerberos (workstation logon); Empower service-account LDAPS bind |
| Groups | `Lab-Empower-Analysts`, `-Senior`, `-MethodOwners`, `-QCManagers`, `-QAApprovers`, `-SysAdmin`, `-Auditor` |
| Conditional Access | `Lab-Workstation Conditional Access (MFA on interactive logon; LAC/E nodes named-location)` per FS-XSYS-AD-01 |
| Audit binding | Logon / Lockout → Splunk `wel-empower` (CI-40, CI-42) |
| FS-IDs traced | FS-PART11-04, FS-PART11-06, FS-XSYS-AD-01 |

### 7.2 IF-NTP

| Aspect | Design |
|---|---|
| Endpoint | `ntp.equinox.local` UDP/123 |
| Skew threshold | `1 s` (CI-22) |
| Monitoring | w32time 35/29 → Splunk; alert > 1 s |
| FS-IDs traced | FS-SW-04 |

### 7.3 IF-CITRIX (ICA published Empower client)

| Aspect | Design |
|---|---|
| Endpoint | Citrix Virtual Apps farm (CI-33) |
| Profile | Non-persistent (CI-34) |
| Drift trigger | Re-validation event on client version change (CI-35) |
| FS-IDs traced | FS-SW-05 |

### 7.4 IF-DB (Oracle 19c + Data Guard)

| Aspect | Design |
|---|---|
| Primary | Oracle 19c on `equinox.local`; archived redo logs continuous (CI-50) |
| Standby | Data Guard active-passive (CI-52) |
| Audit-table GRANT | INSERT-only to Empower service; UPDATE/DELETE denied (CI-13) |
| Backup | RMAN nightly to SnapLock cold (CI-50, CI-51) |
| FS-IDs traced | FS-PLAT-01, FS-BAK-01, FS-BAK-03, FS-AUD-02, FS-PART11-03 |

### 7.5 IF-SIEM (Splunk Universal Forwarder)

| Aspect | Design |
|---|---|
| Endpoint | UF → indexer cluster TCP/9997 |
| Heavy index | `wel-empower` (CI-40) |
| Source-types | `WinEventLog:Security`, `Empower:Audit`, `EmpowerLIMSConnector:App`, `Oracle:Audit` |
| Alert rules | `wel-empower-lockout` (CI-42); `wel-empower-lims-failure` (CI-47); `wel-empower-availability` (CI-41); federation lag (CI-57) |
| FS-IDs traced | FS-PART11-05, FS-PART11-12, FS-INT-LIMS-04, FS-AV-01, FS-SEC-04, FS-FED-03 |

### 7.6 IF-LIMS-WORKLIST-IN + IF-LIMS-RESULT-OUT (Empower-LIMS Connector 4.2)

| Aspect | Design |
|---|---|
| Inbound | `https://lims.equinox.local/api/v3/worklist` polled 60 s (CI-43); service principal CI-44 |
| Outbound | `https://lims.equinox.local/api/v3/result` mTLS via `equinox-empower-2026q2` (CI-48) |
| Push gate | LimsExport + QC Mgr Approve (+ QA Approver if release) (CI-45) |
| Schema | `EQX-LIMS-PUSH-EMP-v3.json` (CI-46) |
| Retry | 30 s / 1 min / 5 min back-off; 3 fails → page (CI-47) |
| Idempotency | `reportId` |
| FS-IDs traced | FS-INT-LIMS-01..04 |

### 7.7 IF-HEL (Helios Audit-Trail Handover, Kafka)

| Aspect | Design |
|---|---|
| Topic | `helios.ingest.equinox.empower.v1` schema-registry pinned (CI-60) |
| Delivery | At-least-once; idempotency key `{source_system, event_id}` (CI-61) |
| Back-pressure | Prometheus `helios_publish_lag_seconds` alert > 600 s sustained 5 min (CI-62) |
| Reconciliation | Daily count parity; > 0.01% mismatch → MasterControl deviation (CI-63) |
| FS-IDs traced | FS-XINT-HEL-01, FS-XINT-HEL-02 |

### 7.8 IF-FED (Empower Federation to partner site)

| Aspect | Design |
|---|---|
| Endpoint | Partner Empower instance LDAPS-bound under Empower's federation feature |
| Grant model | Per-project explicit grant (CI-55) |
| Direction | Read-only at destination (CI-56) |
| Health | Lag + hash-divergence monitor (CI-57) |
| FS-IDs traced | FS-FED-01..03 |

## 8. Site-Deployed Components (micro-SDS)

Two small site-developed components:

### 8.1 `EMP-PLUGIN-SEQ-VALIDATOR-01` — Sequence Pre-Run Validator plugin

| Field | Value |
|---|---|
| Type | Empower-side Toolkit plugin (C#) registered as sequence-start hook |
| Responsibility | FS-ACQ-02 + FS-MTH-03 pre-run gating (CI-24, CI-64) |
| Inputs | Sequence handle |
| Outputs | `OK` or `BLOCK <reason>` with audit-trail entry |
| Algorithm | `if !instrument.Ready: BLOCK; if method.state != "EFFECTIVE": BLOCK; if project.lock: BLOCK; if method.MatrixType != sample.MatrixType: BLOCK "Matrix mismatch"; if method.ColumnLot != instrument.ColumnLot: BLOCK "Column-lot mismatch"; else OK` |
| Storage | Empower configuration manager → toolkit plugin registry |
| Unit-test | OQ-ACQ-02 + OQ-MTH-03 (one per BLOCK branch + happy path) |
| FS-IDs traced | FS-ACQ-02, FS-MTH-03 |

### 8.2 `EMP-PUBLISHER-HELIOS-01` — Helios Audit-Trail Publisher service

| Field | Value |
|---|---|
| Type | Site-developed sidecar service (.NET 8) consuming Empower audit-trail events from Oracle change-data-capture and publishing to Kafka |
| Responsibility | FS-XINT-HEL-01 / FS-XINT-HEL-02 |
| Inputs | Oracle audit-table CDC stream |
| Outputs | Kafka topic `helios.ingest.equinox.empower.v1` JSON-Lines envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}` |
| Algorithm | Read CDC LSN; transform to Helios envelope; publish with idempotency key `{source_system, event_id}`; persist `helios_ack_ts` on broker ack; daily reconciliation job (CI-63) |
| Storage | Container image in site registry; deployed via Helm to Kubernetes cluster |
| Unit-test | Contract test against schema registry + reconciliation test |
| FS-IDs traced | FS-XINT-HEL-01, FS-XINT-HEL-02 |

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .68, .180, .192, .194(a)(8).
- FDA *Data Integrity and Compliance With cGMP* (2018); FDA *OOS Guidance* (2022).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.

### DACH
- BfArM — Bundesinstitut für Arzneimittel und Medizinprodukte (DE inspecting authority for this site).
- Site `EQX-IS-POL-PASSWORD`.

### International
- ISPE GAMP 5 (2nd Ed., 2022); GAMP GPG *Validation of Laboratory Computerized Systems*.
- USP <621> / <1058> / <1224>-<1226>.
- ICH Q2(R2), ICH Q9(R1), ICH Q14.
- PIC/S PI 041.

### Vendor
- Waters — *Empower 3 FR5 System Administrator's Guide* (rev. 2024-09).
- Waters — *Empower 3 FR5 Configuration Reference* (rev. 2024-09).
- Waters — *Empower-LIMS Connector 4.2 Installation and Configuration Guide* (rev. 2024-06).
- Oracle — *Oracle Database 19c Administrator's Guide* (Oracle Data Guard, RMAN, audit-trail GRANT model).
- Citrix — *Citrix Virtual Apps and Desktops 2402 Administrator Documentation*.

### Site / parent
- `EQX-FS-EMPOWER-001 v1.2`; `EQX-URS-EMPOWER-001 v1.2`.
- `EQX-VAL-EMPOWER-001`, `EQX-PROC-EMP-RESTORE-001`, `EQX-RB-EMP-OPS-001`.

## Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) | Design intent (brief) | Verified by |
|---|---|---|---|
| DS-PLAT-01 | FS-PLAT-01, FS-BAK-03 | Oracle Data Guard active-passive + RPO 15 min (CI-52) | IQ-DB-02 |
| DS-PLAT-02 | FS-PLAT-02 | LAC/E UPS sizing (CI-31) | IQ-LACE-02 |
| DS-PLAT-03 | FS-PLAT-03 | Lab-IT VLAN three-tier baseline (CI-05) | IQ-GPO-04 |
| DS-SW-01 | FS-SW-01 | Waters install + SCN CR | IQ-INSTALL-01 |
| DS-SW-02 | FS-SW-02 | AD-mapped role table file (CI-08) | OQ-EMP-02 |
| DS-SW-03 | FS-SW-03, FS-EMP-01 | Project Policy bundle ON (CI-01, CI-02, CI-07) | OQ-PROJECT-POLICY-01 |
| DS-SW-04 | FS-SW-04 | NTP + 1 s skew (CI-22) | IQ-NTP-01 |
| DS-SW-05 | FS-SW-05 | Citrix non-persistent + drift trigger (CI-33..35) | IQ-CITRIX-01 |
| DS-ACQ-01 | FS-ACQ-01, FS-MTH-01 | Method state machine (CI-23) | OQ-MTH-01 |
| DS-ACQ-02 | FS-ACQ-02 | Sequence-start validator + plugin (CI-24, § 8.1) | OQ-ACQ-02 |
| DS-ACQ-03 | FS-ACQ-03 | Per-injection metadata fields (Empower vendor default + Project Policy CI-02) | OQ-ACQ-03 |
| DS-ACQ-04 | FS-ACQ-04, FS-SST-02 | SST + BlockOnSstFailure (CI-25, CI-26) | OQ-SST-01..02 |
| DS-PROC-01 | FS-PROC-01 | Approved processing method auto-apply (vendor default + Project Policy) | OQ-PROC-01 |
| DS-PROC-02 | FS-PROC-02, FS-RPR-01 | RFC closed list (CI-12) | OQ-REINTEGRATE-REASON-01 |
| DS-PROC-03 | FS-PROC-03, FS-DI-04 | Raw Data Lock = ON (CI-01) | OQ-RAW-DATA-LOCK-01 |
| DS-PROC-04 | (vendor-internal — Empower spec-comparison rule engine) + spec-set thresholds CI-37 | n/a (engine) / CI-37 (thresholds) | OQ-QNT-04 |
| DS-PROC-05 | FS-PROC-05, FS-DI-02 | PDF/A-3 report template (CI-39) | OQ-RPT-01 |
| DS-AUD-01 | (vendor-internal — Empower audit-trail event schema) | n/a (flagged) | n/a |
| DS-AUD-02 | FS-AUD-02 | Oracle audit-table GRANT model (CI-13) | OQ-AUD-APPENDONLY-01 |
| DS-AUD-03 | FS-AUD-03 | Per-batch Senior + monthly QC Mgr eSign review | OQ-AUD-REVIEW-01 |
| DS-AUD-04 | FS-AUD-04, FS-PART11-03 | SnapLock retention 7y/25y (CI-51) | IQ-FS-01 |
| DS-AUD-05 | FS-AUD-05 | Audit-trail export (Empower default + CI-67-style) | OQ-AUD-EXPORT-01 |
| DS-PART11-01 | FS-PART11-01 | Validation dossier (CI-73) | (admin) |
| DS-PART11-02 | FS-PART11-02, FS-EMP-05 | PDF/A-3 + .eax (CI-39, CI-72) | OQ-PART11-02 |
| DS-PART11-03 | FS-PART11-03 | RMAN + SnapLock + S3 (CI-50, CI-51) | IQ-DB-01 |
| DS-PART11-04 | FS-PART11-04 | AD-bound + local-admin disable (CI-03) | IQ-GPO-02 |
| DS-PART11-05 | FS-PART11-05 | Audit policy → Splunk (CI-04, CI-40) | IQ-GPO-03 |
| DS-PART11-06 | FS-PART11-06 | AD-group → Authority Set (CI-15..21) | OQ-ROLE-01..07 |
| DS-PART11-07 | FS-PART11-07 | Ops manual + SCN CR (CI-74) | (admin) |
| DS-PART11-08 | FS-PART11-08 | Meaning-of-sig closed list (CI-10) | OQ-PART11-08 |
| DS-PART11-09 | FS-PART11-09 | SHA-256 signature payload (CI-11) | OQ-PART11-09 |
| DS-PART11-10 | FS-PART11-10 | AD SID-on-rehire (CI-59) | IQ-AD-02 |
| DS-PART11-11 | FS-PART11-11 | ForceReAuthOnSignature (CI-09) | OQ-PART11-11 |
| DS-PART11-12 | FS-PART11-12, FS-SEC-02 | AD password policy + lockout alert (CI-58, CI-42) | OQ-PART11-12 |
| DS-PART11-13 | FS-PART11-13 | SoD enforced via Authority Sets (CI-15..21) | OQ-PART11-SOD-01 |
| DS-EMP-01 | FS-EMP-01 | Project naming + GxP policy auto-apply (CI-07, CI-01) | OQ-EMP-01 |
| DS-EMP-02 | FS-EMP-02 | Role-map file version-controlled (CI-08) | OQ-EMP-02 |
| DS-EMP-03 | FS-EMP-03 | Project-rename eSign chain (CI-70) | OQ-EMP-03 |
| DS-EMP-04 | FS-EMP-04 | Method-result binding immutability (CI-71) | OQ-EMP-04 |
| DS-EMP-05 | FS-EMP-05 | .eax archive scope (CI-72) | OQ-EMP-05 |
| DS-SST-01 | FS-SST-01 | SST evaluator binding (CI-25) | OQ-SST-01 |
| DS-SST-02 | FS-SST-02 | BlockOnSstFailure (CI-26) | OQ-SST-02 |
| DS-SST-03 | FS-SST-03 | SST-Record schema (CI-27) | OQ-SST-03 |
| DS-SST-04 | FS-SST-04 | Bracketed-SST trigger (CI-28) | OQ-SST-04 |
| DS-QNT-01 | (vendor-internal — Empower curve engine) + r² floor CI-29 | r² floor 0.99 (CI-29) | OQ-QNT-01 |
| DS-QNT-02 | FS-QNT-02 | Outlier rule ±15%/±20% (CI-36) | OQ-QNT-02 |
| DS-QNT-03 | FS-QNT-03 | IEEE-754 + rounding-final (CI-38) | OQ-QNT-03 |
| DS-QNT-04 | FS-QNT-04, FS-PROC-04 | Spec-set thresholds (CI-37) | OQ-QNT-04 |
| DS-RPR-01 | (vendor-internal — Empower RFC dialog UI) + closed list CI-12 | RFC closed list (CI-12) | OQ-REINTEGRATE-REASON-01 |
| DS-RPR-02 | FS-RPR-02 | Lineage entity (vendor default + CI-67 export) | OQ-RPR-02 |
| DS-RPR-03 | FS-RPR-03 | Diff-block 0% + dual eSign (CI-66) | OQ-RPR-03 |
| DS-RPR-04 | FS-RPR-04, FS-EMP-05 | Lineage export DOT+JSON (CI-67) | OQ-RPR-04 |
| DS-FED-01 | FS-FED-01 | Federation grant table (CI-55) | OQ-FED-01 |
| DS-FED-02 | FS-FED-02 | FED_READ_ONLY handler (CI-56) | OQ-FED-02 |
| DS-FED-03 | FS-FED-03 | Federation health monitor (CI-57) | OQ-FED-03 |
| DS-MTH-01 | FS-MTH-01 | Method state machine (CI-23) | OQ-MTH-01 |
| DS-MTH-02 | FS-MTH-02 | Author ≠ Reviewer ≠ Approver (CI-15..18) | OQ-MTH-02 |
| DS-MTH-03 | FS-MTH-03 | MatrixType + ColumnLot validator (CI-64, § 8.1) | OQ-MTH-03 |
| DS-MTH-04 | FS-MTH-04 | Method-Change-Impact engine (CI-65) | OQ-MTH-04 |
| DS-REL-01 | FS-REL-01 | Release workflow 4-eyes+QA (CI-68) | OQ-REL-01 |
| DS-REL-02 | FS-REL-02 | Stability tagging validator (CI-69) | OQ-REL-02 |
| DS-REL-03 | FS-REL-03 | Held release 30-d expiry (CI-68 logic) | OQ-REL-03 |
| DS-DI-01 | FS-DI-01 | Domain-user attribution (Authority-Set binding) | OQ-DI-01 |
| DS-DI-02 | FS-DI-02 | PDF/A-3 fonts + ICC (CI-39) | OQ-RPT-01 |
| DS-DI-03 | FS-DI-03 | Retrospective-entry flag (CI-14) | OQ-DI-03 |
| DS-DI-04 | FS-DI-04, FS-PROC-03 | Raw Data Lock = ON (CI-01) | OQ-RAW-DATA-LOCK-01 |
| DS-DI-05 | FS-DI-05 | OQ regression 20×3 (CI-76) | OQ-DI-05 |
| DS-DI-06 | FS-DI-06, FS-AV-01 | Availability dashboard (CI-41) | OQ-AV-01 |
| DS-INT-01 | FS-INT-LIMS-01 | Connector poll + service principal (CI-43, CI-44) | OQ-INT-01 |
| DS-INT-02 | FS-INT-LIMS-02 | Push gate + mTLS (CI-45, CI-48) | OQ-INT-02 |
| DS-INT-03 | FS-INT-LIMS-03 | Payload schema (CI-46) | OQ-INT-03 |
| DS-INT-04 | FS-INT-LIMS-04 | Failure-alert SLA 5 min (CI-47) | OQ-INT-04 |
| DS-BAK-01 | FS-BAK-01, FS-XSYS-BAK-01 | Oracle RMAN + SnapLock + S3 + LTO (CI-50, CI-51) | IQ-DB-01 |
| DS-BAK-02 | FS-BAK-02 | Quarterly restore test + QA witness (CI-53) | IQ-BAK-02 |
| DS-BAK-03 | FS-BAK-03 | Data Guard failover RTO 4 h + RPO 15 min (CI-52) | IQ-DB-02 |
| DS-BAK-04 | FS-BAK-04 | Annual DR drill failover + failback (CI-54) | OQ-BAK-04 |
| DS-PERF-01 | FS-PERF-01 | PQ 24-instrument concurrent (CI-77, CI-79) | PQ-PERF-01 |
| DS-PERF-02 | FS-PERF-02 | Citrix APM P95 ≤ 10 s (CI-78) | OQ-PERF-02 |
| DS-PERF-03 | FS-PERF-03 | Sequence-start P95 ≤ 5 s (CI-78) | OQ-PERF-03 |
| DS-AV-01 | FS-AV-01 | Availability dashboard (CI-41) | OQ-AV-01 |
| DS-SEC-01 | FS-SEC-01 | Break-glass + AD-only (CI-03) | IQ-GPO-02 |
| DS-SEC-02 | FS-SEC-02 | AD password policy (CI-58) | IQ-AD-01 |
| DS-SEC-03 | FS-SEC-03 | GPO Block-RemovableMedia (CI-06) | IQ-GPO-05 |
| DS-SEC-04 | FS-SEC-04 | CrowdStrike daily + dashboard (CI-32) | IQ-AV-01 |
| DS-SEC-05 | FS-SEC-05 | Three-VLAN baseline + firewall (CI-05) | IQ-GPO-04 |
| DS-TRN-01 | FS-TRN-01, FS-TRN-02 | Cornerstone gate (CI-49) | IQ-LMS-01 |
| DS-PR-01 | FS-PR-01, FS-PR-02 | Periodic-review template + dual eSign (CI-75) | OQ-PR-01 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 | LDAPS + Kerberos + Conditional Access (§ 7.1) | IQ-AD-01..02 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 | Veeam T2 + S3 Object Lock + LTO-9 (CI-50, CI-51) | IQ-DB-01 |
| DS-XINT-HEL-01 | FS-XINT-HEL-01 | Kafka publisher + idempotency + back-pressure (CI-60..62, § 8.2) | OQ-HEL-01..02 |
| DS-XINT-HEL-02 | FS-XINT-HEL-02 | Daily reconciliation job (CI-63, § 8.2) | OQ-HEL-03 |

## Appendix B — Design-level Risk Register

| ID | Risk | Likelihood | Impact | Mitigation reference | Design surface |
|---|---|---|---|---|---|
| DR-01 | Reprocess-diff-block at 0% (CI-66) generates dual-eSign burden for benign re-integrations below floating-point noise | Medium | Low | Operational SOP `EQX-SOP-CHROM-INTEGRATION-002` + post-go-live tuning review at month 3 | CI-66 |
| DR-02 | Authority-Set ↔ AD-group drift on group rename without Empower re-binding | Low | Critical | Quarterly access review (FS-PR-01) + Authority-Set export reconciled with AD | CI-15..21 |
| DR-03 | SnapLock retention metadata `25y` tag not applied to release-linked Oracle archives → silent demotion to 7 y | Low | Critical | Pre-archive metadata-tag verification + quarterly audit | CI-51 |
| DR-04 | mTLS cert `equinox-empower-2026q2` expiry blocks LIMS push silently | Low | High | 30-day pre-expiry pager alert + auto-rotation | CI-48, CI-47 |
| DR-05 | EMP-PLUGIN-SEQ-VALIDATOR-01 (§ 8.1) silently fails open on plugin exception | Low | Critical | Plugin authored with default-BLOCK on exception; OQ-ACQ-02 negative-path test | § 8.1, CI-24 |
| DR-06 | RFC closed-list (CI-12) growth outside change control dilutes audit story | Medium | Medium | Quarterly reason-code distribution review in `wel-empower` | CI-12 |
| DR-07 | SCN upgrade silently changes vendor-default CI (e.g., `Signature hash` to SHA-1) | Low | Critical | Post-upgrade IQ delta-check across all 79 CIs + FS-PART11-09 re-test | CI-09, CI-11 |
| DR-08 | Federation grant table (CI-55) drift between sites — partner site adds grants without home-site eSign | Medium | High | Federation grant entries replicated bi-directionally + flagged as deviation if asymmetric | CI-55, CI-57 |
| DR-09 | Helios Kafka publisher (§ 8.2) silently drops events on schema-registry mismatch | Low | Critical | Schema-evolution gate at publisher startup; reconciliation job (CI-63) catches gap within 24 h | § 8.2, CI-60, CI-63 |
| DR-10 | Citrix profile drift — published Empower client version reverts on Citrix farm refresh | Low | High | Image-drift trigger (CI-35) re-validates; Citrix farm-refresh runbook includes pin check | CI-33, CI-35 |
| DR-11 | Oracle Data Guard replication lag uncaught → RPO drifts > 15 min silently | Low | Critical | Data Guard lag metric → Splunk alert; quarterly RPO measurement during restore test | CI-52, CI-53 |
| DR-12 | LAC/E node CrowdStrike exclusion list drift on agent update | Low | High | LAC/E baseline IQ delta-check after every Falcon agent SCN | CI-32 |
| DR-13 | Empower role-map.yaml (CI-08) merge conflict at quarterly review introduces silent permission grant | Low | High | Two-reviewer pull-request gate on role-map repo + diff posted to quarterly review meeting | CI-08 |
| DR-14 | Federation read-only enforcement (CI-56) bypassed via Empower Toolkit script on partner side | Low | Critical | Toolkit script registry quarterly export reconciled with both sites | CI-56 |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
