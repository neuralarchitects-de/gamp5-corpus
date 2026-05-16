---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring 2026-05-15 (Chunk A LC-MS)"
seed_corpus_basis:
  - "ACME-FS-LCMS-001 v1.2 (parent FS, T2 rebuild 2026-05-13)"
  - "ACME-URS-LCMS-001 v1.2 (transitive parent URS)"
  - "GAMP 5 (2nd Edition) Category 4 — Configuration Specification conventions"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "USP <621>; USP <1058> AIQ"
  - "Waters MassLynx 4.2 SCN1027 System Administrator Guide (vendor configuration manual)"
  - "Waters TargetLynx XS Application Manager Reference"
parent_fs:
  document_number: ACME-FS-LCMS-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Acme_Pharmaceuticals_LC-MS_FS_v1.3.md
parent_urs:
  document_number: ACME-URS-LCMS-001
  version: 1.2
  file: ../../../URS/_generated/final/Acme_Pharmaceuticals_LC-MS_Computer_System_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## LC-MS Computer System — Waters Acquity I-Class UPLC + Xevo TQ-S micro + MassLynx 4.2 SCN1027

**Document Number:** ACME-DS-LCMS-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** ACME-FS-LCMS-001 v1.2 | **Parent URS:** ACME-URS-LCMS-001 v1.2 *(informational, transitive)*
**Site:** Acme Pharmaceuticals Ltd, QC Lab, Pune, India *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Waters MassLynx 4.2 on Windows 11** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <621>; USP <1058>; ICH Q2(R2); PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Mass-Spec Lead) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Approver (Head of QC / System Owner) | _____________ | _____________ | _____ |
| Approver (Head of QA / Process Owner) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T2 from parent URS+FS pair. DS covers 86/90 FS-IDs; 4 FS-IDs flagged as vendor-internal — no site design surface (FS-AUD-01 audit-trail event schema, FS-PROC-03 TargetLynx library-search engine internals, FS-QNT-01 calibration-curve engine internals, FS-LIB-02 per-component match-score computation). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from parent FS `ACME-FS-LCMS-001` and parent URS `ACME-URS-LCMS-001`. DS-specific terms:

| Term | Definition |
|---|---|
| CI (Configuration Item) | A single configurable parameter exposed by MassLynx / Windows / GPO / NetApp / Splunk that the site sets to a chosen value to satisfy one or more FS-IDs |
| `.PLC` (MassLynx Project Policy) | Per-project policy bundle file controlling raw-data-lock, audit, eSign, and RFC modes |
| Authority Set | MassLynx-internal name for a role's bundle of allowed actions (mapped 1:1 to AD groups via the User Manager) |
| GPO | Group Policy Object (Windows AD) |
| `wel-lcms` | Splunk heavy-index name reserved for this system's events |

## 1. Purpose

This Configuration Specification (CS) defines the technical design of the Waters MassLynx 4.2 SCN1027 + TargetLynx XS configuration that satisfies the functional behaviour specified in `ACME-FS-LCMS-001` v1.2. For each Configuration Item (CI) the CS records: vendor-named parameter, chosen value, default-vs-custom flag, justification anchored in the bound FS-IDs, and the planned IQ/OQ test that verifies the configuration choice. Workflow / business-rule design, role-permission matrix design, integration design, and the (small) site-developed-component design follow in §§ 5–8.

The CS is the controlled design baseline that the Installation Qualification (IQ) and Operational Qualification (OQ) execute against. Vendor internals (MassLynx UI rendering, TargetLynx library-search algorithm) are not redrawn here — they remain Waters' SDLC responsibility.

## 2. Scope

### 2.1 In scope

- MassLynx 4.2 SCN1027 + TargetLynx XS site-level configuration choices: project policy, user-role mapping, eSign mode, audit-trail mode, calibration validity windows, SST acceptance rules, method-state machine, reprocessing policy, library binding, LIMS Connector configuration.
- Workstation / Windows 11 / AD GPO design that bounds the MassLynx environment.
- Integration design for the four named partner systems: Active Directory, NTP, NetApp SnapLock file share, Splunk SIEM, LabWare LIMS 8.
- Site-deployed components: one MassLynx pre-run macro (FS-ACQ-02) and one TargetLynx Reason-Code closed-list extension (FS-PROC-01). Both treated as Cat 5-equivalent micro-SDS sub-sections in § 8.

### 2.2 Out of scope

- Vendor internals (MassLynx UI rendering, TargetLynx library-matching engine, .RAW binary format) — vendor SDLC.
- Custom reports / Excel-VBA macros (none in this baseline; any future addition triggers a fresh Cat 5 assessment).
- The LIMS-side configuration of LabWare LIMS 8 (validated under `ACME-VAL-LIMS-007`).
- Infrastructure-qualification artefacts (AD, NTP, NetApp, Splunk are qualified under their own IDS; this DS references those baselines).

## 3. Architectural Overview

The CS layers seven configuration domains on top of the FS § 3 component inventory: (1) Windows/AD policy, (2) MassLynx project policy, (3) MassLynx authority sets, (4) TargetLynx evaluator rules, (5) Acquity/Xevo calibration policy, (6) integration bindings, (7) audit-trail and retention bindings. The figure below expands FS § 3.2 with the configuration touchpoints (italic capital letters refer to § 4 CI rows).

```
                            AD `acme.local` (qualified infra)
                            │
                            │ AD group → MassLynx Authority Set
                            │ (CI-15..CI-22, see §6 matrix)
                            ▼
       ┌──────────────────────────────────────────────────────────────┐
       │ MassLynx Workstation (HP Z4 G5)                              │
       │   Win 11 Pro 22H2 (domain-joined)                            │
       │   GPO `GMP-Lab-Workstations` (CI-03, CI-04, CI-05, CI-06)    │
       │   ┌───────────────────────────────────────┐                  │
       │   │ MassLynx 4.2 SCN1027 + TargetLynx XS  │                  │
       │   │   Project Root  (CI-01)               │                  │
       │   │   Project Policy `.PLC`  (CI-07)      │                  │
       │   │   Require Sig Re-Auth  (CI-09)        │                  │
       │   │   eSign Meaning-of-Sig List (CI-10)   │                  │
       │   │   Authority Sets (CI-15..CI-22)       │                  │
       │   │   Calibration Validity Windows (CI-23)│                  │
       │   │   SST Verdict Block (CI-24)           │                  │
       │   │   Method State Machine (CI-25)        │                  │
       │   │   Library Binding (CI-27)             │                  │
       │   └────┬──────────────────────────────────┘                  │
       │        │ USB-3 to Acquity / Xevo (per FS-HW-01/02)            │
       │        │ SMB to file share                                    │
       └────────┼──────────────────────────────────────────────────────┘
                │
                │                       ┌──────────────────────────────┐
                ├──────► NTP ──────────►│ ntp.acme.local (CI-29)       │
                │                       └──────────────────────────────┘
                │                       ┌──────────────────────────────┐
                ├──────► SMB 3.1.1 ────►│ \\acme-gmp-fs01\masslynx-    │
                │      (FS-FS-01)       │ projects                     │
                │                       │ NetApp SnapLock Compliance   │
                │                       │ Retention 7y / 25y (CI-30)   │
                │                       └──────────────────────────────┘
                │                       ┌──────────────────────────────┐
                ├──────► TCP/9997 ─────►│ Splunk UF → heavy index      │
                │      (FS-SW-04)       │ `wel-lcms` (CI-31)           │
                │                       └──────────────────────────────┘
                │                       ┌──────────────────────────────┐
                └──────► HTTPS/mTLS ───►│ LabWare LIMS 8 via Waters    │
                       (FS-INT-LIMS-*)  │ LIMS Connector (CI-32..35)   │
                                        └──────────────────────────────┘
```

## 4. Configuration Specification

The table below records one row per Configuration Item. Vendor-named CIs follow the names that appear in *Waters MassLynx 4.2 SCN1027 System Administrator Guide* (rev. 2024-09) and *Waters TargetLynx XS Application Manager Reference* (rev. 2024-09). `Default` = vendor's out-of-the-box value retained; `Custom` = site-specific deviation with justification.

| CI-ID | Configuration item (named per vendor) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| CI-01 | MassLynx → Tools → Options → `Project Root` | `\\acme-gmp-fs01\masslynx-projects` | Custom | All GMP project data must live on the WORM-tier share; vendor default `C:\MassLynx` is not 7-y immutable. | FS-SW-03, FS-AUD-04 | IQ-CFG-01 |
| CI-02 | MassLynx → Tools → Options → `Local Cache Quota (GB)` | `50` | Custom | Bounded local cache prevents pre-sync silent buffer loss; aligns with FS-SW-03. | FS-SW-03 | IQ-CFG-02 |
| CI-03 | GPO `GMP-Lab-Workstations` → Screen-saver-lock timeout (min) | `10` | Custom | Mirrors FS-SW-07 and § 5.10 inactivity rule. | FS-SW-07 | IQ-GPO-01 |
| CI-04 | GPO `GMP-Lab-Workstations` → Local-admin GPO `Disable-Local-Accounts` | `Enabled` | Custom | Only `acme\bg-admin` retained per FS-SEC-01. | FS-SW-01, FS-PART11-04, FS-SEC-01 | IQ-GPO-02 |
| CI-05 | GPO `GMP-Lab-Workstations` → Audit Policy (Logon / Account Mgmt / Object Access) | `All Success + Failure` | Custom | Forwards to Splunk per FS-SW-04; 21 CFR § 11.10(e). | FS-SW-04, FS-PART11-05 | IQ-GPO-03 |
| CI-06 | GPO `GMP-Firewall` → Inbound/Outbound ruleset | `GMP-Segment baseline` (deny by default) | Custom | Per FS-SEC-05; mgmt subnet only inbound. | FS-SEC-05 | IQ-GPO-04 |
| CI-07 | MassLynx → Project Policy `.PLC` → bundle | `RawDataLock=ON; eSign=ON; Audit=ON; RFC=ON` | Custom | Vendor default omits RFC; site Part 11 posture requires reason-for-change on all GMP edits per FS-AUD-01. | FS-AUD-01, FS-PART11-08, FS-PROC-01 | IQ-CFG-03 |
| CI-08 | MassLynx → Project Policy `.PLC` → `Raw-Data-File ACL` | `nwt-svc-masslynx-acq` write @acquire; `Everyone:Read` after close; deny-delete | Custom | Implements FS-PROC-02/FS-DI-04 raw-immutable rule on NTFS layer. | FS-PROC-02, FS-DI-04 | IQ-CFG-04 |
| CI-09 | MassLynx → Security → `RequireSignatureReAuth` | `true` | Custom | Vendor default `false` would honour cached creds; FS-PART11-11 needs explicit re-auth per § 11.200. | FS-PART11-11 | OQ-PART11-11 |
| CI-10 | MassLynx → Security → `Meaning-of-Signature List` | `Review, Approve, Reject, Lock` | Custom | Closed list per § 11.50 / FS-PART11-08. | FS-PART11-08 | OQ-PART11-08 |
| CI-11 | MassLynx → Security → `Signature Hash Algorithm` | `SHA-256` | Default | Vendor default since SCN1024; satisfies FS-PART11-09. | FS-PART11-09, FS-DI-04 | OQ-PART11-09 |
| CI-12 | MassLynx → Security → `Reason-Code Closed List` | `baseline-noise, co-elution, peak-shoulder, integration-correction, instrument-glitch, sample-prep-error, calibration-overdue, other-with-justification` | Custom | Implements FS-PROC-01 closed-list reason capture; "other-with-justification" forces free text. | FS-PROC-01 | OQ-PROC-01 |
| CI-13 | MassLynx → Audit Trail → `.AT` file ACL | `Allow:Read Everyone; Deny:Modify+Delete BUILTIN\Administrators` | Custom | Enforces audit-trail immutability at NTFS layer per FS-AUD-02. | FS-AUD-02 | IQ-CFG-05 |
| CI-14 | MassLynx → Audit Trail → `Retrospective-Entry Flag` | `Enabled` (timestamp-divergence > 0 s flags entry) | Custom | Implements FS-DI-03 retrospective-entry flagging. | FS-DI-03 | OQ-DI-03 |
| CI-15 | MassLynx User Manager → AD-Group → Authority-Set mapping `Lab-LCMS-Analysts` | `Authority Set = Analyst` (acquire / integrate / process; no method-edit; no eSign-Approve) | Custom | Implements FS-PART11-06 / FS-PART11-13 separation-of-duties at user-manager layer. | FS-PART11-06, FS-PART11-13 | OQ-ROLE-01 |
| CI-16 | MassLynx User Manager → AD-Group `Lab-LCMS-SeniorAnalysts` | `Authority Set = SeniorAnalyst` (Analyst + Review-eSign) | Custom | Per FS-PART11-06; review tier. | FS-PART11-06 | OQ-ROLE-02 |
| CI-17 | MassLynx User Manager → AD-Group `Lab-LCMS-MethodOwners` | `Authority Set = MethodOwner` (Method create/edit; no Approve-eSign) | Custom | Per FS-ACQ-01 / FS-MTH-02; enforces Author ≠ Approver. | FS-ACQ-01, FS-MTH-02 | OQ-ROLE-03 |
| CI-18 | MassLynx User Manager → AD-Group `Lab-LCMS-QCManagers` | `Authority Set = QCManager` (Approve-eSign; LIMS export) | Custom | Per FS-INT-LIMS-02; only QCManager can flip LimsExport. | FS-INT-LIMS-02, FS-MTH-02 | OQ-ROLE-04 |
| CI-19 | MassLynx User Manager → AD-Group `Lab-LCMS-Auditors` | `Authority Set = Auditor` (read-only; export PDF) | Custom | Per FS-AUD-05. | FS-AUD-05 | OQ-ROLE-05 |
| CI-20 | MassLynx User Manager → AD-Group `Lab-LCMS-SystemAdmins` | `Authority Set = SystemAdmin` (config; no Approve-eSign on results / methods) | Custom | Operator-vs-approver separation per FS-PART11-13. | FS-PART11-13 | OQ-ROLE-06 |
| CI-21 | MassLynx User Manager → `Concurrent Authority Hold` | `Single-Authority-Set per user` (deny multi-set hold on same project) | Custom | Implements FS-PART11-13 dual-role prohibition. | FS-PART11-13 | OQ-ROLE-07 |
| CI-22 | MassLynx User Manager → Service principal `acme\nwt-svc-masslynx-acq` | `Authority Set = AcquisitionService` (write-during-acquire only) | Custom | Service-only; not human-mapped. | FS-PROC-02 | IQ-CFG-06 |
| CI-23 | TargetLynx XS → Calibration Validity Window (per type) | Lock-mass `7 d`; Mass-cal `14 d`; Full-tune `30 d` | Custom | Aligns with Waters-published cadence per FS-CAL-01; method may override per FS-CAL-02. | FS-CAL-01, FS-CAL-02 | OQ-CAL-01 |
| CI-24 | TargetLynx XS → `SST-Verdict-Blocks-Downstream` | `true` | Custom | Implements FS-SST-02 hard block on failed SST. | FS-SST-02 | OQ-SST-02 |
| CI-25 | TargetLynx XS → Method State Machine | `DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE` (Author ≠ Reviewer ≠ Approver) | Custom | Per FS-MTH-01 / FS-MTH-02. | FS-MTH-01, FS-MTH-02 | OQ-MTH-01 |
| CI-26 | TargetLynx XS → `Reprocess-Diff-Block-Pct` | `0.0` (any difference triggers `RESULT_DIFFERS_ON_REPROCESS`) | Custom | Per FS-MTH-04 — zero tolerance, dual eSign required on any drift. | FS-MTH-04 | OQ-MTH-04 |
| CI-27 | TargetLynx XS → `Active Library Binding` | `ACME-MSLIB-2026Q2` (SHA-256 fingerprint pinned at startup) | Custom | Implements FS-LIB-01 hash verification on every TargetLynx launch. | FS-LIB-01, FS-LIB-03 | OQ-LIB-01 |
| CI-28 | TargetLynx XS → `Calibration-Curve r² Floor` | `0.99` (quantitative assay) | Custom | Per FS-QNT-01; differs from vendor default 0.98. | FS-QNT-01 | OQ-QNT-01 |
| CI-29 | Windows Time service → NTP source | `ntp.acme.local`; skew threshold `1 s` | Custom | Per FS-SW-06; site NTP. | FS-SW-06 | IQ-NTP-01 |
| CI-30 | NetApp SnapLock Compliance → `masslynx-projects` retention | `7y` default; `25y` if metadata tag `retention=25y` | Custom | Implements FS-AUD-04 + FS-PART11-03. | FS-AUD-04, FS-PART11-03 | IQ-FS-01 |
| CI-31 | Splunk UF → heavy index | `wel-lcms` (TCP/9997 outbound to indexer cluster) | Custom | Per FS-SW-04 / FS-PERF-04 / FS-PART11-12. | FS-SW-04, FS-PART11-12, FS-PERF-04, FS-INT-LIMS-04 | IQ-SIEM-01 |
| CI-32 | Waters LIMS Connector → polling endpoint | `https://lims.acme.local/api/v3/worklist` every `60 s` | Custom | Per FS-INT-LIMS-01. | FS-INT-LIMS-01 | OQ-INT-01 |
| CI-33 | Waters LIMS Connector → service principal | `acme\svc-masslynx-limsread` (read-only AD group) | Custom | Per FS-INT-LIMS-01. | FS-INT-LIMS-01 | IQ-INT-01 |
| CI-34 | Waters LIMS Connector → push gating | `LimsExport == true && Approve-eSign valid` | Custom | Per FS-INT-LIMS-02. | FS-INT-LIMS-02 | OQ-INT-02 |
| CI-35 | Waters LIMS Connector → payload schema validator | `ACME-LIMS-PUSH-LCMS-v3.json` (mandatory: reportId, instrumentId, methodId+ver, libraryId+hash, calibrationCurveId, sstRecordId, analystId, reviewerId, approverId, rawFileHash, resultHash) | Custom | Per FS-INT-LIMS-03. | FS-INT-LIMS-03 | OQ-INT-03 |
| CI-36 | Waters LIMS Connector → failure-alert SLA | `5 min`; Splunk rule `wel-lcms-lims-failure` pages on-call | Custom | Per FS-INT-LIMS-04. | FS-INT-LIMS-04 | OQ-INT-04 |
| CI-37 | Cornerstone LMS → curriculum gating | `ACME-CURR-LCMS-Analyst-v1` mandatory pre AD-group add | Custom | Per FS-TRN-01. | FS-TRN-01, FS-TRN-02 | IQ-LMS-01 |
| CI-38 | UPS APC SMT2200RM2UC → SNMP shutdown threshold | `20%` remaining capacity | Custom | Per FS-HW-03. | FS-HW-03 | IQ-HW-03 |
| CI-39 | CrowdStrike Falcon → exclusion list | `Waters-approved MassLynx + TargetLynx temp paths` | Custom | Per FS-SW-05; vendor list pinned at install. | FS-SW-05, FS-SEC-04 | IQ-AV-01 |
| CI-40 | viewLinc EM → SIEM webhook for HVAC excursion | `T>23°C OR T<17°C OR RH<30% OR RH>60% → wel-lcms` | Custom | Per FS-HW-05. | FS-HW-05 | IQ-HW-05 |
| CI-41 | TargetLynx XS → `Bracketed-SST-Mode` | `Enabled for sequence length ≥ 30 injections` | Custom | Per FS-SST-04. | FS-SST-04 | OQ-SST-04 |
| CI-42 | TargetLynx XS → `Carryover-Ratio-Threshold` | `0.2% of LOQ peak area` | Custom | Per FS-SST-05 / USP <621>. | FS-SST-05 | OQ-SST-05 |
| CI-43 | TargetLynx XS → `Source-Tune Deviation Threshold` | `5%` (capillary/cone/source-T/desolv-T/desolv-gas) | Custom | Per FS-CAL-03; deviation triggers Method-Owner override. | FS-CAL-03 | OQ-CAL-03 |
| CI-44 | TargetLynx XS → `PM-Blocks-Run` flag | `PM_PENDING_TUNE_VERIFICATION` blocks GxP runs | Default | Vendor default behaviour retained per FS-CAL-04. | FS-CAL-04 | OQ-CAL-04 |
| CI-45 | TargetLynx XS → Outlier Rule (per-standard back-calc) | `±15% non-LOQ; ±20% LOQ` → `STANDARD_OUTLIER` | Default | Vendor rule retained per FS-QNT-02. | FS-QNT-02 | OQ-QNT-02 |
| CI-46 | TargetLynx XS → Method Matrix Validator | `MatrixType ∈ {drug-product, API, stability, dissolution}` enforced at sequence start | Custom | Per FS-QNT-03. | FS-QNT-03 | OQ-QNT-03 |
| CI-47 | TargetLynx XS → Numeric Precision | `IEEE-754 double` intermediate; rounding at final report only | Default | Vendor default per FS-QNT-04. | FS-QNT-04, FS-PROC-04 | OQ-QNT-04 |
| CI-48 | TargetLynx XS → Spec-Flag Thresholds | `30% TREND / 50% OOT / 100% OOS` | Custom | Per FS-QNT-05. | FS-QNT-05 | OQ-QNT-05 |
| CI-49 | TargetLynx XS → RTDB Column-Lot Drift Threshold | `0.05 min` | Custom | Per FS-LIB-04. | FS-LIB-04 | OQ-LIB-04 |
| CI-50 | TargetLynx XS → Borderline-Match Flag | `±5% of match-score threshold` → flag for Senior-Analyst review | Custom | Per FS-LIB-03. | FS-LIB-03 | OQ-LIB-03 |
| CI-51 | MassLynx → Report Template Registry → `ACME-RPT-LCMS-001-v1.0.qrt` | Active; PDF/A-3 with embedded fonts + ICC | Custom | Implements FS-PROC-05. | FS-PROC-05, FS-DI-02 | OQ-RPT-01 |
| CI-52 | MassLynx → Report Template Registry → `ACME-RPT-LCMS-AUDIT-001` | Active | Custom | Implements FS-AUD-03 audit-trail review template. | FS-AUD-03 | OQ-RPT-02 |
| CI-53 | MassLynx → Report → Re-Issue Watermark Template | `RE-ISSUED — supersedes <originalReportId>` | Custom | Per FS-PROC-06. | FS-PROC-06 | OQ-RPT-03 |
| CI-54 | Veeam B&R 12.1 → backup job | `masslynx-projects-daily` 02:00 IST + SHA-256 verify + off-site immutable replica | Custom | Per FS-BAK-01; tier T2 per FS-XSYS-BAK-01. | FS-BAK-01, FS-BAK-04, FS-XSYS-BAK-01 | IQ-BAK-01 |
| CI-55 | Veeam B&R 12.1 → SureBackup test schedule | Quarterly; QC witness sign-off; runbook `ACME-PROC-BAK-RESTORE-001` | Custom | Per FS-BAK-02. | FS-BAK-02 | IQ-BAK-02 |
| CI-56 | DR Runbook `ACME-RB-LCMS-DR-001` → RTO target | `8 business hours` | Custom | Per FS-BAK-03. | FS-BAK-03 | OQ-BAK-03 (DR drill) |
| CI-57 | Splunk Dashboard `wel-lcms-availability` | `99.0% business-hours availability target` | Custom | Per FS-PERF-04 / FS-DI-06. | FS-PERF-04, FS-DI-06 | OQ-PERF-04 |
| CI-58 | Splunk Alert `wel-lcms-lockout` | Trigger on AD lockout event for `Lab-LCMS-*` group members | Custom | Per FS-PART11-12. | FS-PART11-12 | OQ-PART11-12 |
| CI-59 | AD Password Policy (Default Domain Policy) | 14-char min; 90-d rotation; history 24; complexity ON; lockout 5/15 min/30 min | Custom | Per FS-SEC-02, FS-PART11-12. | FS-SEC-02, FS-PART11-12 | IQ-AD-01 |
| CI-60 | GPO `Block-RemovableMedia` → USB mass-storage class | `Denied` (override via signed CR `ACME-CR-IT-USB-LCMS`) | Custom | Per FS-SEC-03. | FS-SEC-03 | IQ-GPO-05 |
| CI-61 | AD → HR Feed binding (SID-on-rehire) | `New SID on rehire` (no SID reuse) | Custom | Per FS-PART11-10. | FS-PART11-10 | IQ-AD-02 |
| CI-62 | Site PKI → mTLS cert for LIMS push | `acme-lcms-2026q2` (auto-rotate 1y) | Custom | Per FS-INT-LIMS-02 payload-signing requirement. | FS-INT-LIMS-02 | IQ-PKI-01 |
| CI-63 | MassLynx → Asset Register binding | One-to-one workstation-serial ↔ Acquity-serial ↔ Xevo-serial; no shared workstations | Custom | Per FS-HW-01. | FS-HW-01 | IQ-HW-01 |
| CI-64 | HP Z4 G5 baseline spec | Xeon W3-2425 / 32 GB DDR5 ECC / 1 TB + 2 TB NVMe / NVIDIA T1000 / 4×USB-3.2 Gen 2 | Custom | Per FS-HW-02. | FS-HW-02 | IQ-HW-02 |
| CI-65 | Workstation VLAN binding | `VLAN 411 (GMP-Lab)` | Custom | Per FS-HW-04. | FS-HW-04 | IQ-HW-04 |
| CI-66 | LIMS Connector → OAuth client | `masslynx-lcms-limsread` | Custom | Per FS-INT-LIMS-01. | FS-INT-LIMS-01 | IQ-INT-02 |
| CI-67 | Periodic Review template binding | `ACME-PR-LCMS-YYYYMMDD` (QC Mgr + QA Mgr eSign meaning Approve) | Custom | Per FS-PR-01 / FS-PR-02. | FS-PR-01, FS-PR-02 | OQ-PR-01 |
| CI-68 | Validation Dossier binding | `ACME-VAL-LCMS-001` (IQ + OQ + PQ + RTM + VSR + PR) | Custom | Per FS-PART11-01. | FS-PART11-01 | (admin) |
| CI-69 | Batch Export (PDF/A-3 + native) | Enabled | Default | Vendor default per FS-PART11-02. | FS-PART11-02 | OQ-PART11-02 |
| CI-70 | System-operation manual binding | `ACME-RB-LCMS-OPS-001` | Custom | Per FS-PART11-07. | FS-PART11-07 | (admin) |
| CI-71 | OQ Stress-test protocol binding | `OQ-PERF-LCMS-50inj-01` | Custom | Per FS-PERF-01 / FS-PERF-02 / FS-PERF-03. | FS-PERF-01, FS-PERF-02, FS-PERF-03 | OQ-PERF-01 |
| CI-72 | OQ Calculation-regression protocol binding | 10 ref samples × 3 analytes × 2 methods; tolerance 0.01% spec limit | Custom | Per FS-DI-05. | FS-DI-05 | OQ-DI-05 |
| CI-73 | viewLinc EM probes — cadence | `1 min` T/RH sampling | Custom | Per FS-HW-05. | FS-HW-05 | IQ-EM-01 |
| CI-74 | TargetLynx → SST Record Schema | `method-id, criteria thresholds, observed/replicate, pass/fail-per-param, verdict, evaluator-version, sha256(sequence-id)` | Custom | Per FS-SST-03. | FS-SST-03 | OQ-SST-03 |
| CI-75 | TargetLynx → Sequence Pre-Run Validators | `instrument=Ready && method.state=EFFECTIVE && !project.lock && !calibration.expired` | Custom | Per FS-ACQ-02; implemented via site macro (see §8). | FS-ACQ-02 | OQ-ACQ-02 |
| CI-76 | TargetLynx → Sequence Template (mandatory fields) | `sample-id, vial-position, injection-volume; auto-bind method-id+ver, instrument-id+serial, analyst (AD session), UTC ts` | Custom | Per FS-ACQ-03. | FS-ACQ-03 | OQ-ACQ-03 |
| CI-77 | TargetLynx → Pause/Resume audit | `SequenceModified` event with mandatory reason text | Custom | Per FS-ACQ-04. | FS-ACQ-04 | OQ-ACQ-04 |
| CI-78 | TargetLynx → SST-Failure Sequence Status | `SST-FAILED` flips, blocks downstream `.PRO` generation | Custom | Per FS-ACQ-05. | FS-ACQ-05 | OQ-ACQ-05 |

## 5. Workflow + Business-Rule Design

### 5.1 Method Lifecycle Workflow `MLX-WF-METHOD-LCMS`

Implemented in TargetLynx XS state machine (CI-25). Steps:

1. **DRAFT** — Method Owner creates draft; no eSign required at this step. Audit-trail entry recorded.
2. **REVIEW** — Method Owner promotes to REVIEW. Second Method Owner (acting as Reviewer) eSigns `Review`. System enforces Author ≠ Reviewer at user-manager layer (CI-15, CI-21).
3. **APPROVED** — QC Manager eSigns `Approve`. System enforces Reviewer ≠ Approver.
4. **EFFECTIVE** — System Administrator promotes (no eSign — administrative action recorded in audit trail). Method becomes selectable at sequence-start.
5. **SUPERSEDED** — automatic on next APPROVED method with same MethodFamilyId reaching EFFECTIVE. 24-hour migration grace window per FS-MTH-05 / CI-26.
6. **OBSOLETE** — manual; QC Manager eSign `Approve`. Method no longer selectable.

Decision points: (a) Author ≠ Reviewer ≠ Approver check at every transition; (b) on SUPERSEDED, in-flight sequences may complete under prior version.

### 5.2 Reprocessing Workflow `MLX-WF-REPROCESS`

Triggered when a user reprocesses a `.RAW` artefact with a different processing-method version (FS-MTH-03):

1. TargetLynx creates new `.PRO` with parent-pointer to `.RAW.sha256` and new processing-method-id+ver.
2. TargetLynx compares result to previously approved result.
3. If `|new - prior| / prior > CI-26` (0.0 in this baseline → any drift): flag `RESULT_DIFFERS_ON_REPROCESS`, block LIMS push.
4. Method Owner eSign + QC Manager eSign (dual) + deviation record `DEV-LCMS-YYYYMMDD-NN` required to unblock.

### 5.3 SST + Bracketed-SST Workflow `MLX-WF-SST-USP621`

Per FS-SST-01..05: TargetLynx evaluates USP <621> parameters at sequence start (and bracket-end for sequences ≥ 30 injections per CI-41). Verdict FAIL flips status `SST-FAILED` (CI-78). Bracket-end FAIL flips bracketed results to `SUSPECT — END-SST-FAILED` (FS-SST-04). Carryover ratio computed per CI-42.

### 5.4 Result Approval + LIMS Push Workflow `MLX-WF-APPROVE-LIMS`

1. Analyst processes data; result enters state `PROCESSED`.
2. Senior Analyst eSigns `Review` (FS-AUD-03 batch sign-off precondition).
3. QC Manager eSigns `Approve` → MassLynx flips `LimsExport=true` (CI-34) and signs payload with `acme-lcms-2026q2` cert (CI-62).
4. Waters LIMS Connector picks up record, validates against schema CI-35, POSTs to `https://lims.acme.local/api/v3/result` (mTLS).
5. On failure: Splunk alert CI-36 within 5 min.

### 5.5 Audit-Trail Review Workflow `MLX-WF-AUDIT-REVIEW`

Per FS-AUD-03: per-batch review by Senior Analyst (event-driven; precondition for batch sign-off); monthly review by QC Manager (periodic). Both use template CI-52 (ACME-RPT-LCMS-AUDIT-001) exported as PDF/A-3.

### 5.6 Calibration + Tune Cadence `MLX-WF-CAL-CADENCE`

Per FS-CAL-01..04. Daily lock-mass (leucine-enkephalin, m/z 556.2771); weekly mass-cal (NaI); monthly full source tune. Pre-run macro (CI-75) checks `cal.expires_at > now()`; expired → blocking dialog. Method-pinned tune parameter deviation > CI-43 → Method-Owner override workflow.

## 6. Role-Permission Matrix Design

Implements FS-PART11-06 / FS-PART11-13 / FS-AUD-05 at the MassLynx User Manager layer. AD groups bind 1:1 to Authority Sets (CI-15..CI-22).

| Permission | Analyst | SeniorAnalyst | MethodOwner | QCManager | SystemAdmin | Auditor |
|---|---|---|---|---|---|---|
| Acquire sequence | ✓ | ✓ | ✓ | ✓ | – | – |
| Integrate peaks (auto) | ✓ | ✓ | ✓ | ✓ | – | – |
| Manual integration (with RFC) | ✓ | ✓ | ✓ | ✓ | – | – |
| Process result | ✓ | ✓ | ✓ | ✓ | – | – |
| eSign `Review` | – | ✓ | – | – | – | – |
| eSign `Approve` (result) | – | – | – | ✓ | – | – |
| eSign `Approve` (method) | – | – | – | ✓ | – | – |
| eSign `Reject` | – | ✓ | – | ✓ | – | – |
| eSign `Lock` (project) | – | – | – | ✓ | – | – |
| Method create / edit | – | – | ✓ | – | – | – |
| Method state transition (Author→Reviewer→Approver) | – | – | (Author) | (Approver) | – | – |
| Flip `LimsExport` | – | – | – | ✓ | – | – |
| Library binding update (with CR) | – | – | ✓ | – | – | – |
| MassLynx config edit | – | – | – | – | ✓ | – |
| AD group membership change | – | – | – | – | ✓ (provisioning ticket) | – |
| Read audit trail | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Export audit trail (PDF) | – | ✓ | – | ✓ | ✓ | ✓ |
| Read raw / processed / report | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

Hard constraints (enforced by CI-21): no user holds two Authority Sets on the same project at the same time. Analyst + SeniorAnalyst or Analyst + QCManager combinations are denied at user-manager provisioning (FS-PART11-13).

## 7. Integration Design

### 7.1 IF-AD-01 (Active Directory, LDAPS + Kerberos)

| Aspect | Design |
|---|---|
| Endpoint | `ldaps://acme.local:636` (LDAPS) + Kerberos KDC discovery via SRV records |
| AuthN | Kerberos for interactive workstation logon; LDAPS bind for MassLynx service principal lookup |
| Groups consumed | `Lab-LCMS-Analysts`, `Lab-LCMS-SeniorAnalysts`, `Lab-LCMS-MethodOwners`, `Lab-LCMS-QCManagers`, `Lab-LCMS-SystemAdmins`, `Lab-LCMS-Auditors` |
| Conditional Access | `Lab-Workstation Conditional Access (MFA on interactive logon)` enforced per FS-XSYS-AD-01 |
| Failure handling | Failed bind → MassLynx login dialog rejects; event sent to Splunk via UF (CI-31) |
| Audit binding | Logon / Logoff / Lockout / Password-Change events forwarded to `wel-lcms` index (CI-05, CI-31, CI-58) |

### 7.2 IF-NTP-01 (NTP)

| Aspect | Design |
|---|---|
| Endpoint | `ntp.acme.local` (UDP/123) |
| Skew threshold | `1 s` (Windows Time service) per CI-29 |
| Monitoring | `w32time` event-ID 35/29 forwarded to Splunk; alert on skew > 1 s |
| FS-IDs traced | FS-SW-06 |

### 7.3 IF-FS-01 (NetApp SnapLock SMB 3.1.1)

| Aspect | Design |
|---|---|
| Endpoint | `\\acme-gmp-fs01\masslynx-projects` (SMB 3.1.1, encrypted in transit) |
| Retention | 7y default; 25y if metadata tag `retention=25y` (CI-30) |
| WORM mode | SnapLock Compliance (deny-delete; deny-modify) |
| Backup | Daily Veeam (CI-54); SHA-256 verify per backup |
| FS-IDs traced | FS-SW-03, FS-AUD-04, FS-PART11-03 |

### 7.4 IF-SIEM-01 (Splunk via Universal Forwarder)

| Aspect | Design |
|---|---|
| Endpoint | Splunk UF → indexer cluster TCP/9997 |
| Heavy index | `wel-lcms` (CI-31) |
| Source-types | `WinEventLog:Security`, `WinEventLog:System`, `MassLynx:Audit`, `WatersLIMSConnector:App` |
| Retention | 7y hot+warm; per site SIEM IDS |
| Alert rules | `wel-lcms-lockout` (CI-58); `wel-lcms-lims-failure` (CI-36); `wel-lcms-availability` dashboard (CI-57); `wel-lcms-av` AV-coverage dashboard (CI-39) |
| FS-IDs traced | FS-SW-04, FS-PART11-05, FS-PART11-12, FS-INT-LIMS-04, FS-PERF-04, FS-SEC-04 |

### 7.5 IF-LIMS-01 / IF-LIMS-02 (LabWare LIMS 8 via Waters LIMS Connector)

| Aspect | Design |
|---|---|
| Inbound endpoint (worklist) | `https://lims.acme.local/api/v3/worklist` polled every 60 s (CI-32) |
| Outbound endpoint (result push) | `https://lims.acme.local/api/v3/result` (mTLS via cert `acme-lcms-2026q2` CI-62) |
| AuthN | Inbound: AD service principal `acme\svc-masslynx-limsread` (CI-33). Outbound: OAuth2 client-credentials + mTLS payload sign |
| Schema validator | `ACME-LIMS-PUSH-LCMS-v3.json` (CI-35) — mandatory fields per FS-INT-LIMS-03 |
| Retry policy | Exponential back-off 30 s / 1 min / 5 min; after 3 failures → page on-call (CI-36) |
| Error handling | Schema-mismatch → reject + Splunk alert; duplicate reportId → reject + audit-trail entry |
| FS-IDs traced | FS-INT-LIMS-01..04 |

## 8. Site-Deployed Components (micro-SDS)

Two small site-developed components escalate this Cat 4 system into a hybrid Cat 4 + Cat 5 sliver. Each is treated under Cat 5 rules per METHODOLOGY § 2B.4 (5).

### 8.1 `MLX-MACRO-PRECHECK-01` — Sequence Pre-Run Validator macro

| Field | Value |
|---|---|
| Type | MassLynx VB-Script pre-run macro |
| Responsibility | Implements FS-ACQ-02 pre-run gating (CI-75) |
| Inputs | Sequence handle (TargetLynx context) |
| Outputs | `OK` → sequence proceeds; `BLOCK <reason>` → blocking dialog + audit-trail entry |
| Algorithm | `if !instrument.Ready: BLOCK "Instrument not Ready"; if method.state != "EFFECTIVE": BLOCK "Method not EFFECTIVE"; if project.lock: BLOCK "Project locked"; if calibration.expires_at < now(): BLOCK "Mass calibration expired — re-tune required"; else OK` |
| Storage | Method library folder `Method Library\macros\` (Method-Owner write only) |
| Unit-test | OQ-ACQ-02 (5 scenarios, one per BLOCK branch + happy path) |
| FS-IDs traced | FS-ACQ-02 |

### 8.2 `MLX-RFCEXT-REASONCODES-01` — Reason-Code Closed-List Extension

| Field | Value |
|---|---|
| Type | MassLynx Reason-Code configuration extension (XML descriptor) |
| Responsibility | Implements FS-PROC-01 closed-list reason capture (CI-12) |
| Inputs | User selection from closed list |
| Outputs | Audit-trail entry with `reasonCode` enum + mandatory free-text justification when `reasonCode == "other-with-justification"` |
| Algorithm | declarative — XML enum file consumed by MassLynx eSign dialog |
| Storage | `C:\MassLynx\Config\ReasonCodes.xml` (System Admin write only) |
| Unit-test | OQ-PROC-01 (one selection from each closed-list value + the free-text branch) |
| FS-IDs traced | FS-PROC-01 |

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .68, .180, .192, .194(a)(8).
- FDA *Guidance on Data Integrity and Compliance With cGMP* (2018).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EudraLex Volume 4 — GMP.

### DACH
- Site Information Security Policy `ACME-IS-POL-PASSWORD`.

### International
- ISPE GAMP 5 (2nd Ed., 2022), §§ on Cat 4 Configuration Specification.
- ISPE GAMP GPG *Validation of Laboratory Computerized Systems*.
- USP <621> Chromatography; USP <1058> AIQ; USP <1224>-<1226>.
- ICH Q2(R2), ICH Q3A(R2), ICH Q3B(R2), ICH Q9(R1), ICH Q14.
- PIC/S PI 041.

### Vendor
- Waters Corporation — *MassLynx 4.2 SCN1027 System Administrator Guide* (rev. 2024-09).
- Waters Corporation — *TargetLynx XS Application Manager Reference* (rev. 2024-09).
- Waters Corporation — *Waters LIMS Connector for MassLynx — Installation and Configuration Guide* (rev. 2024-06).
- Waters Corporation — *Acquity I-Class UPLC + Xevo TQ-S micro Hardware Reference + Maintenance Guide*.

### Site / parent documents
- `ACME-FS-LCMS-001 v1.2` (parent FS).
- `ACME-URS-LCMS-001 v1.2` (transitive parent URS).
- `ACME-VAL-LCMS-001` (validation dossier).
- `ACME-PROC-BAK-RESTORE-001`, `ACME-RB-LCMS-DR-001`, `ACME-RB-LCMS-OPS-001`.

## Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) | Design intent (brief) | Verified by |
|---|---|---|---|
| DS-HW-01 | FS-HW-01 | Asset-register one-to-one workstation/UPLC/MS serial binding (CI-63) | IQ-HW-01 |
| DS-HW-02 | FS-HW-02 | HP Z4 G5 baseline spec (CI-64) | IQ-HW-02 |
| DS-HW-03 | FS-HW-03 | UPS SMT2200RM2UC 20% SNMP shutdown (CI-38) | IQ-HW-03 |
| DS-HW-04 | FS-HW-04 | VLAN 411 binding (CI-65) | IQ-HW-04 |
| DS-HW-05 | FS-HW-05 | viewLinc 1-min cadence + SIEM webhook on excursion (CI-40, CI-73) | IQ-HW-05 |
| DS-SW-01 | FS-SW-01, FS-SEC-01, FS-PART11-04 | Win 11 22H2 image + AD-bind + local-admin disable GPO (CI-04) | IQ-GPO-02 |
| DS-SW-02 | FS-SW-02 | Vendor install procedure WAT-FS-MLX-2024-007 binding | IQ-INSTALL-01 |
| DS-SW-03 | FS-SW-03 | MassLynx Project Root + 50 GB local cache (CI-01, CI-02) | IQ-CFG-01 |
| DS-SW-04 | FS-SW-04, FS-PART11-05 | Audit policy + Splunk forwarding (CI-05, CI-31) | IQ-GPO-03 |
| DS-SW-05 | FS-SW-05, FS-SEC-04 | CrowdStrike exclusion list (CI-39) | IQ-AV-01 |
| DS-SW-06 | FS-SW-06 | Windows Time → ntp.acme.local, skew 1 s (CI-29) | IQ-NTP-01 |
| DS-SW-07 | FS-SW-07 | Screen-saver-lock 10 min (CI-03) | IQ-GPO-01 |
| DS-ACQ-01 | FS-ACQ-01 | Method Library ACL + Method-Owner separation (CI-17) | OQ-ROLE-03 |
| DS-ACQ-02 | FS-ACQ-02 | Pre-run validator macro MLX-MACRO-PRECHECK-01 (§ 8.1, CI-75) | OQ-ACQ-02 |
| DS-ACQ-03 | FS-ACQ-03 | Sequence template mandatory fields (CI-76) | OQ-ACQ-03 |
| DS-ACQ-04 | FS-ACQ-04 | Pause/Resume SequenceModified audit (CI-77) | OQ-ACQ-04 |
| DS-ACQ-05 | FS-ACQ-05 | SST-FAILED status flip (CI-78) | OQ-ACQ-05 |
| DS-PROC-01 | FS-PROC-01 | Reason-Code closed-list extension MLX-RFCEXT-REASONCODES-01 (§ 8.2, CI-12) | OQ-PROC-01 |
| DS-PROC-02 | FS-PROC-02, FS-DI-04 | Raw `.RAW` ACL flip to immutable (CI-08, CI-22) | OQ-PROC-02 |
| DS-PROC-03 | (vendor-internal — TargetLynx library-search engine; FS-PROC-03 covered by CI-27 library-binding only) | Library binding `ACME-MSLIB-2026Q2` SHA-256 pinned (CI-27) | OQ-LIB-01 |
| DS-PROC-04 | FS-PROC-04, FS-QNT-04 | Equation set + IEEE-754 + rounding only at final (CI-47) | OQ-QNT-04 |
| DS-PROC-05 | FS-PROC-05, FS-DI-02 | PDF/A-3 report template (CI-51) | OQ-RPT-01 |
| DS-PROC-06 | FS-PROC-06 | Re-issue watermark template (CI-53) | OQ-RPT-03 |
| DS-AUD-01 | (vendor-internal — MassLynx audit-trail event-schema; site has no design surface) | n/a (flagged) | n/a |
| DS-AUD-02 | FS-AUD-02 | `.AT` ACL deny-modify+delete (CI-13) | IQ-CFG-05 |
| DS-AUD-03 | FS-AUD-03 | Audit-trail review template ACME-RPT-LCMS-AUDIT-001 (CI-52) | OQ-RPT-02 |
| DS-AUD-04 | FS-AUD-04, FS-PART11-03 | SnapLock retention 7y/25y (CI-30) | IQ-FS-01 |
| DS-AUD-05 | FS-AUD-05 | Auditor authority set (CI-19) | OQ-ROLE-05 |
| DS-PART11-01 | FS-PART11-01 | Validation dossier binding `ACME-VAL-LCMS-001` (CI-68) | (admin) |
| DS-PART11-02 | FS-PART11-02 | Batch export PDF/A-3 + native (CI-69) | OQ-PART11-02 |
| DS-PART11-03 | FS-PART11-03 | SnapLock + Veeam (CI-30, CI-54) | IQ-FS-01 |
| DS-PART11-04 | FS-PART11-04 | AD-bound access + local-admin disable (CI-04, CI-15..20) | IQ-GPO-02 |
| DS-PART11-05 | FS-PART11-05 | Audit policy → Splunk (CI-05, CI-31) | IQ-GPO-03 |
| DS-PART11-06 | FS-PART11-06 | AD group → Authority Set mapping (CI-15..20) | OQ-ROLE-01..06 |
| DS-PART11-07 | FS-PART11-07 | Ops manual + SCN change-control binding (CI-70) | (admin) |
| DS-PART11-08 | FS-PART11-08 | Meaning-of-signature closed list (CI-10) | OQ-PART11-08 |
| DS-PART11-09 | FS-PART11-09 | SHA-256 signature payload (CI-11) | OQ-PART11-09 |
| DS-PART11-10 | FS-PART11-10 | AD SID-on-rehire (CI-61) | IQ-AD-02 |
| DS-PART11-11 | FS-PART11-11 | RequireSignatureReAuth = true (CI-09) | OQ-PART11-11 |
| DS-PART11-12 | FS-PART11-12, FS-SEC-02 | AD password policy 14/90/24/lockout 5/15/30 (CI-59); lockout alert (CI-58) | OQ-PART11-12 |
| DS-PART11-13 | FS-PART11-13 | Single-Authority-Set per user (CI-21) | OQ-ROLE-07 |
| DS-DI-01 | FS-DI-01 | `.AT` records `domain\user` (vendor-default; ACL CI-13 enforces non-tamper) | OQ-DI-01 |
| DS-DI-02 | FS-DI-02 | PDF/A-3 embedded fonts + ICC (CI-51) | OQ-RPT-01 |
| DS-DI-03 | FS-DI-03 | Retrospective-entry flag (CI-14) | OQ-DI-03 |
| DS-DI-04 | FS-DI-04, FS-PROC-02 | Raw immutable on close (CI-08) | OQ-PROC-02 |
| DS-DI-05 | FS-DI-05 | OQ calculation regression protocol binding (CI-72) | OQ-DI-05 |
| DS-DI-06 | FS-DI-06, FS-PERF-04 | Availability dashboard wel-lcms-availability (CI-57) | OQ-PERF-04 |
| DS-BAK-01 | FS-BAK-01, FS-BAK-04, FS-XSYS-BAK-01 | Veeam daily 02:00 IST + SHA-256 + off-site immutable (CI-54) | IQ-BAK-01 |
| DS-BAK-02 | FS-BAK-02 | Quarterly SureBackup + witness (CI-55) | IQ-BAK-02 |
| DS-BAK-03 | FS-BAK-03 | DR runbook RTO 8 BH (CI-56) | OQ-BAK-03 |
| DS-BAK-04 | FS-BAK-04 | RPO 24 h derived from daily backup window | IQ-BAK-01 |
| DS-PERF-01 | FS-PERF-01 | OQ stress 50 inj (CI-71) | OQ-PERF-01 |
| DS-PERF-02 | FS-PERF-02 | Processing benchmark ≤ 15 min (CI-71) | OQ-PERF-02 |
| DS-PERF-03 | FS-PERF-03 | UI P95 ≤ 3 s (CI-71) | OQ-PERF-03 |
| DS-PERF-04 | FS-PERF-04 | Availability dashboard (CI-57) | OQ-PERF-04 |
| DS-SEC-01 | FS-SEC-01 | Break-glass account quarterly review + AD-only otherwise (CI-04) | IQ-GPO-02 |
| DS-SEC-02 | FS-SEC-02 | AD password policy (CI-59) | IQ-AD-01 |
| DS-SEC-03 | FS-SEC-03 | GPO Block-RemovableMedia (CI-60) | IQ-GPO-05 |
| DS-SEC-04 | FS-SEC-04 | CrowdStrike daily + dashboard (CI-39) | IQ-AV-01 |
| DS-SEC-05 | FS-SEC-05 | GPO GMP-Firewall (CI-06) | IQ-GPO-04 |
| DS-TRN-01 | FS-TRN-01, FS-TRN-02 | Cornerstone curriculum gate + annual refresher (CI-37) | IQ-LMS-01 |
| DS-PR-01 | FS-PR-01, FS-PR-02 | Periodic-review template + QC Mgr + QA Mgr eSign (CI-67) | OQ-PR-01 |
| DS-SST-01 | FS-SST-01 | TargetLynx USP <621> evaluator (CI-23..CI-28 baseline; method-specific thresholds bound at method) | OQ-SST-01 |
| DS-SST-02 | FS-SST-02 | SST-Verdict-Blocks-Downstream (CI-24) | OQ-SST-02 |
| DS-SST-03 | FS-SST-03 | SST record schema (CI-74) | OQ-SST-03 |
| DS-SST-04 | FS-SST-04 | Bracketed-SST mode (CI-41) | OQ-SST-04 |
| DS-SST-05 | FS-SST-05 | Carryover-ratio threshold 0.2% LOQ (CI-42) | OQ-SST-05 |
| DS-CAL-01 | FS-CAL-01 | Calibration validity windows 7/14/30 d (CI-23) | OQ-CAL-01 |
| DS-CAL-02 | FS-CAL-02 | Pre-run macro calibration-expiry block (CI-75, § 8.1) | OQ-ACQ-02 |
| DS-CAL-03 | FS-CAL-03 | Source-tune deviation threshold 5% (CI-43) | OQ-CAL-03 |
| DS-CAL-04 | FS-CAL-04 | PM_PENDING_TUNE_VERIFICATION flag (CI-44) | OQ-CAL-04 |
| DS-QNT-01 | FS-QNT-01 | Calibration-curve r² floor 0.99 (CI-28); curve engine itself = vendor-internal | OQ-QNT-01 |
| DS-QNT-02 | FS-QNT-02 | Outlier rule ±15%/±20% (CI-45) | OQ-QNT-02 |
| DS-QNT-03 | FS-QNT-03 | Matrix validator (CI-46) | OQ-QNT-03 |
| DS-QNT-04 | FS-QNT-04 | IEEE-754 double + rounding only at final (CI-47) | OQ-QNT-04 |
| DS-QNT-05 | FS-QNT-05 | Spec-flag thresholds 30/50/100% (CI-48) | OQ-QNT-05 |
| DS-MTH-01 | FS-MTH-01 | Method state machine (CI-25) | OQ-MTH-01 |
| DS-MTH-02 | FS-MTH-02 | Author ≠ Reviewer ≠ Approver via Authority Sets (CI-15..18, CI-21) | OQ-MTH-02 |
| DS-MTH-03 | FS-MTH-03 | Reprocess workflow MLX-WF-REPROCESS (§ 5.2) | OQ-MTH-03 |
| DS-MTH-04 | FS-MTH-04 | Reprocess-diff-block 0% (CI-26) | OQ-MTH-04 |
| DS-MTH-05 | FS-MTH-05 | 24-h migration grace window (CI-26 logic + workflow § 5.1) | OQ-MTH-05 |
| DS-LIB-01 | FS-LIB-01 | Active library binding + SHA-256 startup check (CI-27) | OQ-LIB-01 |
| DS-LIB-02 | (vendor-internal — per-component match-score computation; site binds threshold only) | Threshold bound per method (CI-50 borderline flag) | OQ-LIB-03 |
| DS-LIB-03 | FS-LIB-03 | Borderline-match flag ±5% (CI-50) | OQ-LIB-03 |
| DS-LIB-04 | FS-LIB-04 | RTDB column-lot drift threshold 0.05 min (CI-49) | OQ-LIB-04 |
| DS-INT-LIMS-01 | FS-INT-LIMS-01 | Connector poll endpoint + service principal + OAuth client (CI-32, CI-33, CI-66) | OQ-INT-01 |
| DS-INT-LIMS-02 | FS-INT-LIMS-02 | LimsExport gate + payload mTLS cert (CI-34, CI-62) | OQ-INT-02 |
| DS-INT-LIMS-03 | FS-INT-LIMS-03 | Payload schema validator (CI-35) | OQ-INT-03 |
| DS-INT-LIMS-04 | FS-INT-LIMS-04 | Failure-alert SLA 5 min (CI-36) | OQ-INT-04 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 | LDAPS + Kerberos + Conditional Access + SIEM forwarding (§ 7.1) | IQ-AD-01..02 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 | Veeam T2 + S3 Object Lock + LTO-9 (CI-54) | IQ-BAK-01 |

## Appendix B — Design-level Risk Register

Design-stage risks specific to the configuration choices above. Per-FS-ID GxP-criticality (R1/R2/R3) is inherited from the parent FS and not duplicated here. These risks seed the formal Risk Assessment `ACME-RA-LCMS-001`.

| ID | Risk | Likelihood | Impact | Mitigation reference | Design surface |
|---|---|---|---|---|---|
| DR-01 | Reprocess-diff-block at 0% (CI-26) generates dual-eSign burden for benign re-integrations that drift below floating-point noise | Medium | Low | Operational SOP `SOP-QC-CHROM-INTEGRATION-002` + post-go-live tuning review at month 3 | CI-26 |
| DR-02 | Authority-Set ↔ AD-group mapping drift if AD group renamed without MassLynx re-binding | Low | Critical | Quarterly access review (FS-PR-01) + MassLynx User-Manager export reconciled with AD | CI-15..20 |
| DR-03 | SnapLock retention metadata tag `retention=25y` mis-applied or omitted on batch-linked projects → 7-y retention applied incorrectly | Low | Critical | Per-batch metadata-tag verification in Veeam pre-backup hook | CI-30 |
| DR-04 | Waters LIMS Connector mTLS cert `acme-lcms-2026q2` expiry blocks LIMS push; CI-36 alert fires but result backlog grows | Low | High | Cert auto-rotation + 30-day pre-expiry pager alert via Splunk | CI-62, CI-36 |
| DR-05 | MLX-MACRO-PRECHECK-01 silently fails open if VB-Script error path returns `OK` by default | Low | Critical | Macro authored with explicit `BLOCK` on exception; OQ-ACQ-02 includes negative-path test that injects script exception | § 8.1, CI-75 |
| DR-06 | Reason-Code closed list (CI-12) growth outside change control dilutes the audit story by allowing `other-with-justification` to dominate | Medium | Medium | Quarterly review of reason-code distribution in `wel-lcms` SIEM dashboard | CI-12 |
| DR-07 | SCN upgrade silently changes a vendor-default CI (e.g., `Signature Hash Algorithm` CI-11 reverting to SHA-1 on a hotfix) | Low | Critical | Post-upgrade IQ delta-check across all 78 CIs + FS-PART11-09 re-test in OQ | CI-09, CI-11 |
| DR-08 | TargetLynx Outlier Rule (CI-45) at vendor default but matrix-specific tolerance differs from method-bound threshold → silent false-pass | Low | High | Per-method outlier-threshold review at method-state EFFECTIVE promotion | CI-45 |
| DR-09 | Workstation VLAN 411 mis-tagged at switch level allowing routing to office VLAN | Low | High | Network IQ-HW-04 includes traceroute from workstation to office-segment host (must fail) | CI-65 |
| DR-10 | Splunk heavy-index `wel-lcms` retention shorter than the GxP record retention (7y) due to indexer-cluster sizing pressure | Low | High | SIEM IDS contract pin + quarterly retention-window audit | CI-31 |
| DR-11 | Cornerstone curriculum gate (CI-37) bypassed via AD group direct-add by SystemAdmin in emergency | Low | High | SystemAdmin Authority Set lacks AD-write directly — provisioning tickets only; quarterly AD reconciliation | CI-37, CI-20 |
| DR-12 | Library SHA-256 pin (CI-27) drift not noticed at TargetLynx startup if startup-check log not forwarded to SIEM | Low | Critical | Startup-check event forwarded to `wel-lcms` with alert rule on hash-mismatch | CI-27, CI-31 |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
