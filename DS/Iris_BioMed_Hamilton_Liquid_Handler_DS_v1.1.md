---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring 2026-05-15 (Chunk A Liquid Handler)"
seed_corpus_basis:
  - "IRS-FS-LH-001 v1.2 (parent FS)"
  - "IRS-URS-LH-001 v1.2 (transitive parent URS)"
  - "GAMP 5 (2nd Ed.) Category 4 — Configuration Specification with Cat-5 sub-components (site-authored VENUS methods)"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "ISO 8655 (parts 1-7); USP <41>; USP <1251>; USP <1058> Group B"
  - "Hamilton — Microlab STAR + VENUS 6.x System Administration Guide (vendor doc)"
  - "Hamilton — VENUS SDK Reference (rev. 2024-08)"
parent_fs:
  document_number: IRS-FS-LH-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Iris_BioMed_Hamilton_Liquid_Handler_FS_v1.3.md
parent_urs:
  document_number: IRS-URS-LH-001
  version: 1.2
  file: ../../../URS/_generated/final/Liquid_Handler_Hamilton_STAR_Computer_System__Iris_BioMed_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Robotic Liquid Handler — Hamilton Microlab STAR + VENUS 6.x

**Document Number:** IRS-DS-LH-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** IRS-FS-LH-001 v1.2 | **Parent URS:** IRS-URS-LH-001 v1.2 *(informational, transitive)*
**Site:** Iris BioMed Inc., QC Bioassay Lab, Salt Lake City, Utah, USA *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (with site-authored VENUS methods assessed as Category 5 sub-components)
**Project Mode:** Custom-build project — site-developed system (GAMP 5 Category 5 — Bespoke; internal SDLC). System: Hamilton Microlab STAR + VENUS 6.x.
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192; EU GMP Annex 11 §§ 4, 6, 9, 11; ICH Q2(R2); ICH Q9(R1); ISO 8655 (parts 1-7); USP <41>; USP <1251>; USP <1058> AIQ (Group B); PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Bioassay Lead) | _____________ | _____________ | _____ |
| Reviewer (Automation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Approver (Head of QC / System Owner) | _____________ | _____________ | _____ |
| Approver (Head of QA / Process Owner) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T2 from parent URS+FS pair. DS covers 73/77 FS-IDs; 4 FS-IDs flagged as vendor-internal — no site design surface (FS-AUD-01 VENUS audit-trail event schema, FS-ERR-01 capacitive level-sense internals, FS-ERR-02 pressure-monitor algorithm, FS-CHO-01 method-promotion static analyser engine internals). Cat-5 sub-component (one example VENUS method) is mini-SDS'd in § 8.3 as a reference pattern; per-method full SDS lives under each method's own `IRS-MS-LH-<assay>-NN` artefact. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from `IRS-FS-LH-001` and `IRS-URS-LH-001`. DS-specific terms:

| Term | Definition |
|---|---|
| `.lay` | VENUS Deck Layout file format |
| `.med` | VENUS Method file format |
| Liquid Class | VENUS configuration object holding aspirate/dispense kinematics per liquid type |
| Authority Set | VENUS Part 11 module role bundle, mapped 1:1 to AD group |
| Tip Counter | Per-rack `tips_used` field |
| `wel-lh` | Splunk heavy-index name reserved for this system's events |

## 1. Purpose

This Configuration Specification records the technical design that satisfies `IRS-FS-LH-001` v1.2 — the Hamilton Microlab STAR + VENUS 6.x configuration plus the Cat-5 site-authored-method SDLC envelope. Each CI carries vendor-named parameter, chosen value, default-vs-custom flag, justification, FS-IDs traced, and the planned IQ/OQ test. Workflow, role-permission, integration, and the Cat-5 mini-SDS template follow in §§ 5–8. Vendor internals (VENUS core, level-sense firmware, pressure-monitor DSP) remain Hamilton's SDLC responsibility and are not redrawn.

## 2. Scope

### 2.1 In scope

- VENUS 6.x configuration: Part 11 module settings, authority sets, project policy, method state machine, liquid-class library, deck-layout binding, tip-pickup verification, calibration cadence, contamination control.
- Windows 11 LTSC / AD GPO baseline.
- Integration design: AD, NTP, NetApp SnapLock, Splunk SIEM, LabWare LIMS 8.
- Cat-5 site-authored-method SDLC envelope (one mini-SDS template — § 8.3 — that each per-method `IRS-MS-LH-<assay>-NN` instantiates).

### 2.2 Out of scope

- Vendor internals (VENUS core, STAR hardware firmware, MPH/Track-Gripper kinematics).
- Per-method full SDS (each method gets its own `IRS-MS-LH-<assay>-NN` downstream artefact).
- LIMS-side configuration.

## 3. Architectural Overview

```
                       AD `iris.local` (qualified infra)
                       │
                       │ AD group → VENUS Authority Set
                       │ (CI-15..21)
                       ▼
       ┌─────────────────────────────────────────────────────────┐
       │ VENUS Workstation (Dell Precision 3680)                 │
       │   Win 11 LTSC (domain-joined)                           │
       │   GPO `GMP-LH-Baseline` (CI-03..06)                     │
       │   ┌────────────────────────────────────┐                │
       │   │ VENUS 6.x + Part 11 Module          │               │
       │   │   Project Policy bundle (CI-07)     │               │
       │   │   Authority Sets (CI-15..21)        │               │
       │   │   Method state machine (CI-25)      │               │
       │   │   Liquid-class library (CI-30)      │               │
       │   │   Tip-pickup verification (CI-32)   │               │
       │   │   Calibration cadence (CI-35)       │               │
       │   │   Contamination static-analyser     │               │
       │   │   (CI-40, CI-41)                    │               │
       │   └────┬───────────────────────────────┘                │
       │        │ USB-3 to STAR + MPH + Track-Gripper            │
       └────────┼───────────────────────────────────────────────┘
                │
                ├──► NTP `ntp.iris.local` (CI-22)
                ├──► SMB → NetApp SnapLock `\\iris-gmp-fs01\venus-methods` (CI-50)
                ├──► TCP/9997 → Splunk UF `wel-lh` (CI-45)
                ├──► HTTPS/mTLS → LabWare LIMS 8 (CI-55..58)
                └──► HTTPS → site GitLab `iris-venus-methods` + `iris-venus-decks` (CI-08, CI-29)
```

## 4. Configuration Specification

Vendor-named CIs per *Hamilton Microlab STAR + VENUS 6.x System Administration Guide* (rev. 2024-08) and *VENUS SDK Reference* (rev. 2024-08).

| CI-ID | Configuration item (named per vendor) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| CI-01 | VENUS → Part 11 Module → `Audit Trail Required` | `true` | Custom | Per FS-SW-01 / FS-AUD-01. | FS-SW-01, FS-AUD-01 | IQ-CFG-01 |
| CI-02 | VENUS → Part 11 Module → `eSign Required` | `true` | Custom | Per FS-SW-01 / FS-PART11-08. | FS-SW-01, FS-PART11-08 | IQ-CFG-02 |
| CI-03 | VENUS → Part 11 Module → `Raw Data Lock` | `true` | Custom | Per FS-SW-01 / FS-DI-04. | FS-SW-01, FS-DI-04 | IQ-CFG-03 |
| CI-04 | GPO `GMP-LH-Baseline` → Local-admin disable | Enabled (only `iris\bg-lh-admin`) | Custom | Per FS-PART11-04 / FS-SEC-02. | FS-PART11-04, FS-SEC-02 | IQ-GPO-01 |
| CI-05 | GPO `Block-RemovableMedia` | Denied (override via CR `IRS-CR-IT-USB-LH`) | Custom | Per FS-SEC-01. | FS-SEC-01 | IQ-GPO-02 |
| CI-06 | GPO Audit Policy (Logon / Account-Mgmt / Object-Access) | All Success + Failure | Custom | Forwards to Splunk per FS-PART11-05. | FS-PART11-05 | IQ-GPO-03 |
| CI-07 | VENUS → Project Policy bundle for GxP projects | `AuditTrailRequired=ON; eSign=ON; RawDataLock=ON; ReasonForChange=ON` | Custom | Per FS-SW-01. | FS-SW-01 | OQ-PROJECT-POLICY-01 |
| CI-08 | VENUS → Methods folder binding | `\\iris-gmp-fs01\venus-methods` (NetApp SnapLock for EFFECTIVE) | Custom | Per FS-SW-02. | FS-SW-02, FS-MTH-04 | IQ-FS-01 |
| CI-09 | VENUS → eSign → `RequireSignatureReAuth` | `true` | Custom | Per FS-PART11-11. | FS-PART11-11 | OQ-PART11-11 |
| CI-10 | VENUS → eSign → Meaning-of-Signature closed list | `Author, Review, Approve, Lock` | Custom | Per FS-PART11-08. | FS-PART11-08 | OQ-PART11-08 |
| CI-11 | VENUS → eSign → Signature hash | `SHA-256` | Default | Per FS-PART11-09. | FS-PART11-09 | OQ-PART11-09 |
| CI-12 | VENUS → Reason-Code closed list (operator decisions on error) | `clot-retry, clot-abort, no-tip-retry-alt, no-tip-abort, no-liquid-abort, deviation-continue, other-with-justification` | Custom | Per FS-ERR-01..03 operator-decision workflow + FS-AUD-01 reason capture. | FS-ERR-01, FS-ERR-02, FS-ERR-03, FS-AUD-01 | OQ-ERR-DECISION |
| CI-13 | VENUS DB → Audit-trail tables permissions | INSERT-only to VENUS service; UPDATE/DELETE denied to all | Custom | Per FS-AUD-02. | FS-AUD-02 | OQ-AUD-APPENDONLY-01 |
| CI-14 | VENUS → Retrospective-entry flag | Enabled (timestamp-divergence flags entry) | Custom | Per FS-DI-03. | FS-DI-03 | OQ-DI-03 |
| CI-15 | VENUS Authority Set ↔ AD-group `Lab-LH-Operators` | `Operator` (run worklists from EFFECTIVE methods; no method-edit; no Approve eSign) | Custom | Per FS-PART11-06, FS-PART11-13. | FS-PART11-06, FS-PART11-13 | OQ-ROLE-01 |
| CI-16 | VENUS Authority Set ↔ `Lab-LH-SeniorOps` | `SeniorOperator` (Operator + Verifier eSign on run set-up) | Custom | Per FS-PART11-13 (Operator ≠ Verifier). | FS-PART11-13, FS-WL-02 | OQ-ROLE-02 |
| CI-17 | VENUS Authority Set ↔ `Lab-LH-MethodAuthors` | `MethodAuthor` (method create/edit; eSign meaning `Author`) | Custom | Per FS-MTH-03 / FS-MTH-04. | FS-MTH-03, FS-MTH-04 | OQ-ROLE-03 |
| CI-18 | VENUS Authority Set ↔ `Lab-LH-MethodReviewers` | `MethodReviewer` (review eSign; cannot Approve) | Custom | Per FS-MTH-03 / FS-PART11-13. | FS-MTH-03, FS-PART11-13 | OQ-ROLE-04 |
| CI-19 | VENUS Authority Set ↔ `Lab-LH-MethodApprovers` | `MethodApprover` (QA + QC Bioassay Lead; promote to EFFECTIVE) | Custom | Per FS-MTH-03. | FS-MTH-03 | OQ-ROLE-05 |
| CI-20 | VENUS Authority Set ↔ `Lab-LH-AutomationEng` | `AutomationEngineer` (hardware config; calibration; no method/eSign Approve) | Custom | Per FS-CAL-* + URS roles. | FS-CAL-01, FS-CAL-02 | OQ-ROLE-06 |
| CI-21 | VENUS Authority Set ↔ `Lab-LH-Auditor` | `Auditor` (read-only) | Custom | Per FS-AUD-05. | FS-AUD-05 | OQ-ROLE-07 |
| CI-22 | Windows Time → NTP source | `ntp.iris.local`; skew `1 s` | Custom | Per FS-PLAT-02. | FS-PLAT-02 | IQ-NTP-01 |
| CI-23 | UPS APC SMT1500 → controlled shutdown threshold | `20%` remaining | Custom | Per FS-PLAT-01. | FS-PLAT-01 | IQ-PLAT-01 |
| CI-24 | Workstation VLAN | `VLAN 421 (Lab-IT)` | Custom | Per FS-PLAT-01. | FS-PLAT-01 | IQ-NW-01 |
| CI-25 | VENUS Method State Machine | `DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE` (Author ≠ Reviewer ≠ Approver) | Custom | Per FS-MTH-02 / FS-MTH-03. | FS-MTH-02, FS-MTH-03 | OQ-MTH-02 |
| CI-26 | Method SDLC procedure binding | `IRS-SOP-LH-METHOD-SDLC-001` (requirements → code review → simulator → wet-run → ISO 8655 → regression) | Custom | Per FS-MTH-01. | FS-MTH-01 | OQ-MTH-01 |
| CI-27 | Method-source repo | site GitLab `iris-venus-methods` with required signed commits | Custom | Per FS-MTH-04. | FS-MTH-04 | OQ-MTH-04 |
| CI-28 | Method promotion checklist binding | `IRS-CHK-LH-METHOD-PROMOTE-001` | Custom | Per FS-MTH-01 / FS-LQC-02 / FS-CHO-01 / FS-CONT-01. | FS-MTH-01, FS-LQC-02, FS-CHO-01, FS-CONT-01 | OQ-MTH-PROMOTE |
| CI-29 | Deck-Layout `.lay` repo | site GitLab `iris-venus-decks`; method references specific layout hash | Custom | Per FS-DECK-01. | FS-DECK-01 | OQ-DECK-01 |
| CI-30 | VENUS Liquid-Class library version pin | `IRS-LQC-LIB-2026Q2` (hashed; method-version-pinned) | Custom | Per FS-LQC-01 / FS-LQC-04. | FS-LQC-01, FS-LQC-04 | OQ-LQC-01 |
| CI-31 | VENUS Method-Promotion Static Analyser → liquid-class-mismatch rule | Block on default-aqueous-on-viscous | Custom | Per FS-LQC-02. | FS-LQC-02 | OQ-LQC-02 |
| CI-32 | VENUS Tip-Pickup Verification → capacitive level-sense | `Z = expected-rack-Z` ± tolerance | Custom | Per FS-ERR-01. | FS-ERR-01 | OQ-ERR-01 |
| CI-33 | VENUS Aspirate Pressure-Monitor → clot-detection threshold | `±30% deviation from method-bound profile` (per liquid class) | Custom | Per FS-ERR-02. | FS-ERR-02 | OQ-ERR-02 |
| CI-34 | VENUS LLD → No-Liquid handler | Default abort + flag `NO_LIQUID` + capture rationale | Default | Per FS-ERR-03. | FS-ERR-03 | OQ-ERR-03 |
| CI-35 | ISO 8655 verification cadence | per `IRS-CAL-PLAN-LH-001` (typ. 6-month / high-stakes quarterly) | Custom | Per FS-CAL-01. | FS-CAL-01 | OQ-CAL-01 |
| CI-36 | Calibration-expired channel block | Pre-run validator denies use of channel where calibration expired | Custom | Per FS-CAL-02. | FS-CAL-02 | OQ-CAL-02 |
| CI-37 | ISO 8655 verification protocol | 3 volume points (10/50/100%) × n ≥ 10 replicates per channel | Custom | Per FS-CAL-03. | FS-CAL-03 | OQ-CAL-03 |
| CI-38 | Calibration trending dashboard | Monotonic > 1% over 3 verifications → channel flagged PM | Custom | Per FS-CAL-04. | FS-CAL-04 | OQ-CAL-04 |
| CI-39 | Pre-run Validator (FS-WL-02 implementation) | `instrument.Ready && method.state=EFFECTIVE && labware.present && per-channel-cal.valid` | Custom | Per FS-WL-02 / FS-MTH-02 / FS-DECK-03. | FS-WL-02, FS-MTH-02, FS-DECK-03 | OQ-WL-02 |
| CI-40 | Method-Promotion Static Analyser → channel-vs-MPH conflict rule | Block on same-well same-time conflict | Custom | Per FS-CHO-01. | FS-CHO-01 | OQ-CHO-01 |
| CI-41 | Method-Promotion Static Analyser → contamination rule | Block on tip-re-use across samples for GxP runs; require wash-step when liquid-class `sticky=true` | Custom | Per FS-CONT-01 / FS-CONT-02. | FS-CONT-01, FS-CONT-02 | OQ-CONT-01 |
| CI-42 | Tip counter field | `tips_used` per rack; reset on rack-reload event | Default | Per FS-CONT-03. | FS-CONT-03 | OQ-CONT-03 |
| CI-43 | Deck-Position-Drift threshold | `0.5 mm` (re-teach trigger) | Custom | Per FS-DECK-04. | FS-DECK-04 | OQ-DECK-04 |
| CI-44 | Pre-Run Deck-Verification screen | RFID-confirmed labware where supported; otherwise operator confirmation eSigned | Custom | Per FS-DECK-03. | FS-DECK-03 | OQ-DECK-03 |
| CI-45 | Splunk UF → heavy index | `wel-lh` (TCP/9997 outbound) | Custom | Per FS-PART11-05 / FS-PART11-12 / FS-BAK alerts. | FS-PART11-05, FS-PART11-12, FS-INT-LIMS-01 | IQ-SIEM-01 |
| CI-46 | Splunk Alert `wel-lh-lockout` | AD lockout for `Lab-LH-*` group → page | Custom | Per FS-PART11-12. | FS-PART11-12 | OQ-PART11-12 |
| CI-47 | Splunk Dashboard `wel-lh-availability` | Workstation up + VENUS service running | Custom | Per FS-PERF-01 / FS-DI-06. | FS-PERF-01, FS-DI-06 | OQ-PERF-01 |
| CI-48 | AD Password Policy | 14-char / 90-d / hist 24 / lockout 5/15 min / 30 min | Custom | Per FS-PART11-12. | FS-PART11-12 | IQ-AD-01 |
| CI-49 | AD HR Feed → SID-on-rehire | New SID on rehire | Custom | Per FS-PART11-10. | FS-PART11-10 | IQ-AD-02 |
| CI-50 | NetApp SnapLock Compliance retention | `25y` release-linked; `7y` general | Custom | Per FS-AUD-04 / FS-PART11-03. | FS-AUD-04, FS-PART11-03 | IQ-FS-02 |
| CI-51 | Veeam B&R 12.1 → backup job | `venus-methods-and-provenance-daily` 02:00 MST + SHA-256 + S3 Object Lock + LTO-9 | Custom | Per FS-BAK-01 / FS-XSYS-BAK-01. | FS-BAK-01, FS-XSYS-BAK-01 | IQ-BAK-01 |
| CI-52 | Veeam SureBackup → quarterly | QA witness on `IRS-PROC-LH-RESTORE-001` | Custom | Per FS-BAK-02. | FS-BAK-02 | IQ-BAK-02 |
| CI-53 | DR Runbook binding | `IRS-RB-LH-DR-001` RTO 8 BH | Custom | Per FS-BAK-03. | FS-BAK-03 | OQ-BAK-03 |
| CI-54 | CrowdStrike Falcon → exclusion list | Hamilton-approved VENUS paths | Custom | Per FS-SEC-03. | FS-SEC-03 | IQ-AV-01 |
| CI-55 | LIMS connector → poll endpoint | `https://lims.iris.local/api/v3/worklist` every 60 s | Custom | Per FS-INT-LIMS-01. | FS-INT-LIMS-01 | OQ-INT-01 |
| CI-56 | LIMS connector → inbound service principal | `iris\svc-lh-limsread` (read-only AD group) | Custom | Per FS-INT-LIMS-01. | FS-INT-LIMS-01 | IQ-INT-01 |
| CI-57 | LIMS connector → push gate | `Operator + Senior Operator eSign valid` | Custom | Per FS-INT-LIMS-01 (provenance push). | FS-INT-LIMS-01, FS-WL-04 | OQ-INT-02 |
| CI-58 | Site PKI → mTLS cert for LIMS push | `iris-lh-2026q2` (auto-rotate 1y) | Custom | Per FS-INT-LIMS-01. | FS-INT-LIMS-01 | IQ-PKI-01 |
| CI-59 | LMS Cornerstone → curriculum gating | `IRS-CURR-LH-Operator-v1` + Method-Author SDK competency `IRS-CURR-LH-MethodAuthor-v1` | Custom | Per FS-TRN-01 / FS-TRN-02. | FS-TRN-01, FS-TRN-02 | IQ-LMS-01 |
| CI-60 | Periodic Review template binding | `IRS-PR-LH-YYYYMMDD` (QC Bioassay Lead + Head of QA) | Custom | Per FS-PR-01 / FS-PR-02. | FS-PR-01, FS-PR-02 | OQ-PR-01 |
| CI-61 | Validation dossier binding | `IRS-VAL-LH-001` | Custom | Per FS-PART11-01. | FS-PART11-01 | (admin) |
| CI-62 | System-operation manual binding | `IRS-RB-LH-OPS-001` | Custom | Per FS-PART11-07. | FS-PART11-07 | (admin) |
| CI-63 | PDF/A-3 + CSV export pipeline | Active | Default | Per FS-PART11-02 / FS-DI-02. | FS-PART11-02, FS-DI-02 | OQ-PART11-02 |
| CI-64 | Provenance Report template | `IRS-RPT-LH-PROV-001` | Custom | Per FS-WL-04. | FS-WL-04 | OQ-RPT-01 |
| CI-65 | Worklist Provenance Schema | `operator-id, method-id+ver, source-labware+lots, dest-labware+lots, per-channel-per-well-volume, per-dispense-ts, errors` | Custom | Per FS-WL-01 / FS-DECK-05. | FS-WL-01, FS-DECK-05 | OQ-WL-01 |
| CI-66 | Track-Gripper movement log | Source/dest position + timestamp | Default | Per FS-CHO-03. | FS-CHO-03 | OQ-CHO-03 |
| CI-67 | MPH wash-station configuration | Wash-step between liquid-class changes; method-builder UI prompts | Custom | Per FS-CHO-02. | FS-CHO-02 | OQ-CHO-02 |
| CI-68 | Per-channel pacing | Independent scheduling when liquid-classes differ | Default | Per FS-ERR-04. | FS-ERR-04 | OQ-ERR-04 |
| CI-69 | Mid-Run Abort handler | Completed wells valid; pending `PENDING_ABORT`; explicit override to include | Custom | Per FS-ERR-05. | FS-ERR-05 | OQ-ERR-05 |
| CI-70 | Method-Promotion eSign chain | Author → Reviewer → Approver (QA + QC Bioassay Lead) | Custom | Per FS-MTH-03. | FS-MTH-03 | OQ-MTH-03 |

## 5. Workflow + Business-Rule Design

### 5.1 Method SDLC Workflow `VENUS-WF-METHOD-SDLC`

Implemented per FS-MTH-01..04 (CI-25..28). Steps: (1) Author creates DRAFT in GitLab `iris-venus-methods` (signed commit, CI-27); (2) Peer + Method Reviewer code review (PR approvals); (3) Dry-run on VENUS simulator; (4) Wet-run on instrument; (5) ISO 8655 accuracy + precision verification on the changed channels / liquid classes; (6) Regression run (10 reference samples); (7) Method-Promotion Static Analyser (CI-31, CI-40, CI-41) — blocks promotion on any violation; (8) Promotion eSign chain Author → Reviewer → Approver (CI-70).

### 5.2 Worklist Execution Workflow `VENUS-WF-WORKLIST`

Per FS-WL-01..04. Operator selects EFFECTIVE method + labware. Pre-run validator (CI-39): instrument-Ready + per-channel cal valid (CI-36) + method-EFFECTIVE + labware present (CI-44). On run: per-channel pacing (CI-68); pressure-monitor / LLD / tip-pickup checks (CI-32..34) route to operator-decision (CI-12). Post-run: provenance report (CI-64) + LIMS push (CI-57) signed by Operator + Senior Operator (Verifier).

### 5.3 Error Recovery Workflow `VENUS-WF-ERROR-DECISION`

Per FS-ERR-01..05. Tip-pickup failure → auto-retry alternate / abort / continue-with-deviation. Clot-detection (CI-33) → abort + flag `ASPIRATE_FAIL`. LLD failure → abort + flag `NO_LIQUID`. Mid-run abort (CI-69) preserves completed wells; pending flagged `PENDING_ABORT`. All decisions captured via Reason-Code closed list (CI-12).

### 5.4 ISO 8655 Calibration Workflow `VENUS-WF-CAL`

Per FS-CAL-01..04. Automation Engineer runs verification at cadence CI-35; 3 volume points × n ≥ 10 replicates (CI-37); pass/fail per channel; results trended (CI-38). Expired channel blocked at pre-run (CI-36); override requires QC Bioassay Lead eSign + impact assessment.

### 5.5 Audit-Trail Review Workflow `VENUS-WF-AUDIT-REVIEW`

Per FS-AUD-03. Per-batch by Senior Operator (event-driven); monthly by QC Bioassay Lead.

### 5.6 Method-Promotion Static Analysis Workflow `VENUS-WF-PROMOTE-STATIC`

Three rule sets at promotion time: (a) Liquid-class explicit-assignment rule (CI-31) per FS-LQC-02; (b) Channel-vs-MPH conflict rule (CI-40) per FS-CHO-01; (c) Contamination rule (CI-41) per FS-CONT-01/02. Any violation blocks promotion.

### 5.7 Liquid-Class Lifecycle Workflow `VENUS-WF-LQC`

Per FS-LQC-01..04. Adds/changes require Method Owner + Senior Bioanalyst eSign + ISO 8655 volume-accuracy + CV verification on the changed liquid class. Library version hash (CI-30) pinned per method-version.

## 6. Role-Permission Matrix Design

Implements FS-PART11-06 / FS-PART11-13. AD groups bind 1:1 to Authority Sets (CI-15..21).

| Permission | Operator | SeniorOp | MethodAuthor | MethodReviewer | MethodApprover | AutoEng | SysAdmin | Auditor |
|---|---|---|---|---|---|---|---|---|
| Run worklist on EFFECTIVE method | ✓ | ✓ | – | – | – | – | – | – |
| Verifier eSign on run set-up | – | ✓ | – | – | – | – | – | – |
| Method create / edit | – | – | ✓ | – | – | – | – | – |
| Method `Author` eSign | – | – | ✓ | – | – | – | – | – |
| Method `Review` eSign | – | – | – | ✓ | – | – | – | – |
| Method `Approve` eSign → EFFECTIVE | – | – | – | – | ✓ (QA + QC Bioassay Lead dual) | – | – | – |
| Deck-layout edit | – | – | – | – | – | ✓ | – | – |
| Labware-definition edit | – | – | ✓ (with eSign + re-validation flow) | – | – | – | – | – |
| Liquid-class library edit | – | – | ✓ (with Senior Bioanalyst dual eSign + ISO 8655 verify) | – | – | – | – | – |
| ISO 8655 verification run | – | – | – | – | – | ✓ | – | – |
| Hamilton SCN apply (under CR) | – | – | – | – | – | – | ✓ | – |
| AD group membership change | – | – | – | – | – | – | ✓ (via ticket) | – |
| Read audit trail | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Export audit trail (PDF/CSV) | – | ✓ | – | – | ✓ | – | ✓ | ✓ |

Hard constraint: Operator ≠ Verifier on same run; Method Author ≠ Method Reviewer ≠ Method Approver on same method. Enforced server-side per FS-PART11-13.

## 7. Integration Design

### 7.1 IF-AD (LDAPS + Kerberos)

| Aspect | Design |
|---|---|
| Endpoint | `ldaps://iris.local:636`; Kerberos KDC via SRV |
| Groups | `Lab-LH-Operators`, `-SeniorOps`, `-MethodAuthors`, `-MethodReviewers`, `-MethodApprovers`, `-AutomationEng`, `-Auditor` |
| Conditional Access | `Lab-Workstation Conditional Access (MFA on interactive logon)` per FS-XSYS-AD-01 |
| Audit binding | Logon / Lockout → Splunk `wel-lh` (CI-45, CI-46) |
| FS-IDs traced | FS-INT-AD-01, FS-PART11-04, FS-PART11-06, FS-XSYS-AD-01 |

### 7.2 IF-NTP

| Aspect | Design |
|---|---|
| Endpoint | `ntp.iris.local` UDP/123 |
| Skew threshold | `1 s` (CI-22) |
| FS-IDs traced | FS-PLAT-02 |

### 7.3 IF-FS (NetApp SnapLock SMB 3.1.1)

| Aspect | Design |
|---|---|
| Endpoint | `\\iris-gmp-fs01\venus-methods`, `\\iris-gmp-fs01\venus-labware` |
| Retention | 7y / 25y (CI-50) |
| WORM | SnapLock Compliance deny-delete/modify on EFFECTIVE method versions |
| Backup | Veeam daily (CI-51) + SHA-256 |
| FS-IDs traced | FS-SW-02, FS-AUD-04, FS-PART11-03 |

### 7.4 IF-SIEM (Splunk Universal Forwarder)

| Aspect | Design |
|---|---|
| Endpoint | UF → indexer cluster TCP/9997 |
| Heavy index | `wel-lh` (CI-45) |
| Source-types | `WinEventLog:Security`, `VENUS:Audit`, `LIMSConnector:App` |
| Alert rules | `wel-lh-lockout` (CI-46), `wel-lh-availability` (CI-47), `wel-lh-lims-failure` |
| FS-IDs traced | FS-PART11-05, FS-PART11-12, FS-INT-LIMS-01 |

### 7.5 IF-LIMS (LabWare LIMS 8)

| Aspect | Design |
|---|---|
| Inbound | `https://lims.iris.local/api/v3/worklist` polled 60 s (CI-55, CI-56) |
| Outbound | `https://lims.iris.local/api/v3/provenance` mTLS via `iris-lh-2026q2` (CI-58) |
| Push gate | Operator + Senior Operator eSign (CI-57) |
| Schema | `IRS-LIMS-PUSH-LH-v3.json` |
| FS-IDs traced | FS-INT-LIMS-01, FS-WL-04 |

### 7.6 IF-GIT (Site GitLab — method + deck repos)

| Aspect | Design |
|---|---|
| Endpoint | `https://gitlab.iris.local` |
| Repos | `iris-venus-methods` (CI-27); `iris-venus-decks` (CI-29) |
| Commit signing | Required (CI-27) |
| Branch protection | PR approvals from Method Reviewer + Method Approver before merge to `main` |
| FS-IDs traced | FS-MTH-04, FS-DECK-01 |

## 8. Site-Deployed Components (micro-SDS)

The platform-level configuration has two site plugins; the VENUS method body is a Cat-5 sub-component template instantiated per assay.

### 8.1 `LH-PLUGIN-STATIC-ANALYSER-01` — Method-Promotion Static Analyser

| Field | Value |
|---|---|
| Type | VENUS SDK plugin (C++) registered as method-promotion hook |
| Responsibility | FS-LQC-02 + FS-CHO-01 + FS-CONT-01/02 rule enforcement (CI-31, CI-40, CI-41) |
| Inputs | Method `.med` file + bound liquid-class library + bound deck layout |
| Outputs | `PROMOTE-OK` or `PROMOTE-BLOCK <rule> <details>` |
| Algorithm | Parse method steps; for each aspirate-dispense: (a) check liquid-class explicit + library-match; (b) check channel-vs-MPH same-well-same-time graph (cycle-detection); (c) check tip-re-use across `sample_id`; (d) check `sticky=true` step → wash-step adjacency |
| Storage | VENUS plugin registry (Automation Engineer write-only via signed CR) |
| Unit-test | OQ-MTH-PROMOTE (one fixture per rule + happy path) |
| FS-IDs traced | FS-LQC-02, FS-CHO-01, FS-CONT-01, FS-CONT-02 |

### 8.2 `LH-PLUGIN-PRE-RUN-01` — Pre-Run Validator plugin

| Field | Value |
|---|---|
| Type | VENUS SDK plugin (C++) registered as worklist-start hook |
| Responsibility | FS-WL-02 + FS-MTH-02 + FS-DECK-03 + FS-CAL-02 |
| Inputs | Worklist + bound method + bound deck layout + per-channel calibration record |
| Outputs | `RUN-OK` or `RUN-BLOCK <reason>` |
| Algorithm | `if !instrument.Ready: BLOCK; if method.state != "EFFECTIVE": BLOCK; if any channel-used has cal.expires_at < now: BLOCK; if any labware not present-or-RFID-confirmed: BLOCK; else OK` |
| Storage | VENUS plugin registry |
| Unit-test | OQ-WL-02 (one fixture per BLOCK branch + happy path) |
| FS-IDs traced | FS-WL-02, FS-MTH-02, FS-DECK-03, FS-CAL-02 |

### 8.3 Cat-5 Method Mini-SDS Template (one per `.med` file)

Each site-authored VENUS method instantiates its own SDS at `IRS-MS-LH-<assay>-NN`. The DS captures the **template** the SDS must follow per FS-MTH-01 / GAMP 5 Cat 5 sub-component rules:

| Field | Required content |
|---|---|
| Responsibility | What the method accomplishes (e.g., `Serial dilution 1:10 × 7 steps for IL-6 ELISA standard curve`) |
| Inputs | Source labware + lots; expected concentrations; channel selection |
| Outputs | Destination labware layout; per-well volumes |
| Algorithm | Step-by-step aspirate/dispense graph with per-step liquid-class assignment; per-step channel-or-MPH selection; explicit wash-steps for sticky reagents |
| Bound Liquid-Class library version | Pin hash CI-30 |
| Bound Deck-Layout version | Pin hash CI-29 |
| Verification | ISO 8655 accuracy + CV on the method-relevant channels and liquid classes; regression suite (10 reference samples) |
| Sign-off | Author + Reviewer + Approver eSign per CI-70 |
| Unit-test references | Per-step OQ test IDs |
| Risk register | Method-specific risks (e.g., reagent contamination, dilution-error propagation) |

The DS does NOT enumerate every method's content; per-method SDSes are downstream artefacts. The DS guarantees the SDLC envelope produces a consistent SDS shape across all methods.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .68, .180, .192.

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.

### DACH
- (Site is US; DACH-specific not applicable; included for corpus consistency: site Information Security Policy `IRS-IS-POL-PASSWORD`.)

### International
- ISPE GAMP 5 (2nd Ed., 2022) — Cat 5 sub-component handling within Cat 4 systems.
- GAMP GPG *Validation of Laboratory Computerized Systems*.
- ISO 8655 parts 1-7; USP <41>, <1251>, <1058> Group B.
- ICH Q2(R2), ICH Q9(R1); PIC/S PI 041.

### Vendor
- Hamilton — *Microlab STAR + VENUS 6.x System Administration Guide* (rev. 2024-08).
- Hamilton — *STAR Hardware Reference (Channel + Multi-Probe Head + Track-Gripper)*.
- Hamilton — *VENUS SDK Reference + Method Best Practices* (rev. 2024-08).

### Site / parent
- `IRS-FS-LH-001 v1.2`; `IRS-URS-LH-001 v1.2`.
- `IRS-SOP-LH-METHOD-SDLC-001`; `IRS-CAL-PLAN-LH-001`; `IRS-VAL-LH-001`; `IRS-RB-LH-OPS-001`; `IRS-PROC-LH-RESTORE-001`; `IRS-RB-LH-DR-001`.

## Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) | Design intent (brief) | Verified by |
|---|---|---|---|
| DS-PLAT-01 | FS-PLAT-01 | UPS + VLAN 421 (CI-23, CI-24) | IQ-PLAT-01 |
| DS-PLAT-02 | FS-PLAT-02 | NTP + 1 s skew (CI-22) | IQ-NTP-01 |
| DS-PLAT-03 | FS-PLAT-03 | ISO 8655 cadence (CI-35) | OQ-CAL-01 |
| DS-SW-01 | FS-SW-01 | Part 11 module ON (CI-01..03, CI-07) | IQ-CFG-01..03 |
| DS-SW-02 | FS-SW-02, FS-MTH-04 | Methods folder + SnapLock (CI-08) | IQ-FS-01 |
| DS-MTH-01 | FS-MTH-01 | SDLC procedure binding (CI-26) | OQ-MTH-01 |
| DS-MTH-02 | FS-MTH-02 | Method state machine (CI-25) | OQ-MTH-02 |
| DS-MTH-03 | FS-MTH-03 | Author ≠ Reviewer ≠ Approver eSign chain (CI-70, CI-17..19) | OQ-MTH-03 |
| DS-MTH-04 | FS-MTH-04 | GitLab signed commits (CI-27) | OQ-MTH-04 |
| DS-WL-01 | FS-WL-01 | Worklist Provenance schema (CI-65) | OQ-WL-01 |
| DS-WL-02 | FS-WL-02 | Pre-run validator plugin (§ 8.2, CI-39) | OQ-WL-02 |
| DS-WL-03 | FS-WL-03 | Error-decision reason-code list (CI-12) | OQ-ERR-DECISION |
| DS-WL-04 | FS-WL-04 | Provenance report + LIMS push (CI-64, CI-57) | OQ-RPT-01 |
| DS-AUD-01 | (vendor-internal — VENUS audit-trail event schema) | n/a (flagged) | n/a |
| DS-AUD-02 | FS-AUD-02 | DB audit-table GRANT model (CI-13) | OQ-AUD-APPENDONLY-01 |
| DS-AUD-03 | FS-AUD-03 | Per-batch Senior + monthly QC Lead review | OQ-AUD-REVIEW |
| DS-AUD-04 | FS-AUD-04, FS-PART11-03 | SnapLock 7y/25y (CI-50) | IQ-FS-02 |
| DS-AUD-05 | FS-AUD-05 | Auditor authority + export (CI-21, CI-63) | OQ-ROLE-07 |
| DS-PART11-01 | FS-PART11-01 | Validation dossier (CI-61) | (admin) |
| DS-PART11-02 | FS-PART11-02 | PDF/A-3 + native export (CI-63) | OQ-PART11-02 |
| DS-PART11-03 | FS-PART11-03 | SnapLock + Veeam (CI-50, CI-51) | IQ-FS-02 |
| DS-PART11-04 | FS-PART11-04 | AD-bound + local-admin disable (CI-04) | IQ-GPO-01 |
| DS-PART11-05 | FS-PART11-05 | Audit policy → Splunk (CI-06, CI-45) | IQ-GPO-03 |
| DS-PART11-06 | FS-PART11-06 | AD group → Authority Set (CI-15..21) | OQ-ROLE-01..07 |
| DS-PART11-07 | FS-PART11-07 | Ops manual binding (CI-62) | (admin) |
| DS-PART11-08 | FS-PART11-08 | Meaning-of-sig list (CI-10) | OQ-PART11-08 |
| DS-PART11-09 | FS-PART11-09 | SHA-256 sig payload (CI-11) | OQ-PART11-09 |
| DS-PART11-10 | FS-PART11-10 | AD SID-on-rehire (CI-49) | IQ-AD-02 |
| DS-PART11-11 | FS-PART11-11 | RequireSignatureReAuth (CI-09) | OQ-PART11-11 |
| DS-PART11-12 | FS-PART11-12 | AD password policy + lockout alert (CI-48, CI-46) | OQ-PART11-12 |
| DS-PART11-13 | FS-PART11-13 | SoD enforced (CI-15..21 + Operator≠Verifier matrix) | OQ-PART11-SOD-01 |
| DS-DI-01 | FS-DI-01 | actor_id AD-bound (Authority Set binding) | OQ-DI-01 |
| DS-DI-02 | FS-DI-02 | PDF/A-3 + CSV export (CI-63) | OQ-PART11-02 |
| DS-DI-03 | FS-DI-03 | Retrospective-entry flag (CI-14) | OQ-DI-03 |
| DS-DI-04 | FS-DI-04 | Raw Data Lock (CI-03) | OQ-DI-04 |
| DS-DI-05 | FS-DI-05 | ISO 8655 calibration record per channel (CI-35, CI-37) | OQ-CAL-03 |
| DS-DI-06 | FS-DI-06 | Metadata-completeness validator (CI-65) + availability dashboard (CI-47) | OQ-WL-01 |
| DS-INT-LIMS-01 | FS-INT-LIMS-01 | Connector poll + push (CI-55..58) | OQ-INT-01..02 |
| DS-INT-AD-01 | FS-INT-AD-01 | LDAPS + Kerberos (§ 7.1) | IQ-AD-01 |
| DS-PERF-01 | FS-PERF-01 | Worklist-start latency P95 ≤ 10 s; provenance ≤ 60 s/384 | OQ-PERF-01 |
| DS-PERF-02 | FS-PERF-02 | PQ stress 96-well plate | PQ-PERF-01 |
| DS-BAK-01 | FS-BAK-01, FS-XSYS-BAK-01 | Veeam daily + SnapLock + S3 + LTO (CI-50, CI-51) | IQ-BAK-01 |
| DS-BAK-02 | FS-BAK-02 | Quarterly SureBackup (CI-52) | IQ-BAK-02 |
| DS-BAK-03 | FS-BAK-03 | DR runbook RTO 8 BH (CI-53) | OQ-BAK-03 |
| DS-SEC-01 | FS-SEC-01 | GPO Block-RemovableMedia (CI-05) | IQ-GPO-02 |
| DS-SEC-02 | FS-SEC-02 | Quarterly access review (CI-15..21 lifecycle) | OQ-PR-01 |
| DS-SEC-03 | FS-SEC-03 | CrowdStrike exclusion (CI-54) | IQ-AV-01 |
| DS-TRN-01 | FS-TRN-01 | LMS curriculum + Method-Author competency (CI-59) | IQ-LMS-01 |
| DS-TRN-02 | FS-TRN-02 | Annual refresher (CI-59) | IQ-LMS-01 |
| DS-PR-01 | FS-PR-01, FS-PR-02 | Periodic-review template + dual eSign (CI-60) | OQ-PR-01 |
| DS-DECK-01 | FS-DECK-01 | Deck-layout repo + hash pin (CI-29) | OQ-DECK-01 |
| DS-DECK-02 | FS-DECK-02 | Labware-def share + re-validation flow | OQ-DECK-02 |
| DS-DECK-03 | FS-DECK-03 | Pre-run deck-verification screen (CI-44, § 8.2) | OQ-DECK-03 |
| DS-DECK-04 | FS-DECK-04 | Drift threshold 0.5 mm (CI-43) | OQ-DECK-04 |
| DS-DECK-05 | FS-DECK-05 | Per-run lot capture in provenance (CI-65) | OQ-WL-01 |
| DS-LQC-01 | FS-LQC-01 | Liquid-class library binding (CI-30) | OQ-LQC-01 |
| DS-LQC-02 | FS-LQC-02 | Static-analyser liquid-class rule (CI-31, § 8.1) | OQ-LQC-02 |
| DS-LQC-03 | FS-LQC-03 | Library-change dual eSign + ISO 8655 verify | OQ-LQC-03 |
| DS-LQC-04 | FS-LQC-04 | Library version hash pinned per method-version (CI-30) | OQ-LQC-04 |
| DS-ERR-01 | (vendor-internal — capacitive level-sense firmware) + tip-pickup verification config CI-32 | Tip-pickup Z-check (CI-32) | OQ-ERR-01 |
| DS-ERR-02 | (vendor-internal — pressure-monitor DSP) + threshold CI-33 | Pressure-deviation threshold (CI-33) | OQ-ERR-02 |
| DS-ERR-03 | FS-ERR-03 | LLD no-liquid handler default (CI-34) | OQ-ERR-03 |
| DS-ERR-04 | FS-ERR-04 | Per-channel pacing (CI-68) | OQ-ERR-04 |
| DS-ERR-05 | FS-ERR-05 | Mid-run abort handler (CI-69) | OQ-ERR-05 |
| DS-CAL-01 | FS-CAL-01 | ISO 8655 cadence (CI-35) | OQ-CAL-01 |
| DS-CAL-02 | FS-CAL-02 | Expired-channel block (CI-36, § 8.2) | OQ-CAL-02 |
| DS-CAL-03 | FS-CAL-03 | 3-point × n ≥ 10 protocol (CI-37) | OQ-CAL-03 |
| DS-CAL-04 | FS-CAL-04 | Trending dashboard (CI-38) | OQ-CAL-04 |
| DS-CHO-01 | (vendor-internal — VENUS static analyser engine) + rule CI-40 | Channel-vs-MPH rule (CI-40, § 8.1) | OQ-CHO-01 |
| DS-CHO-02 | FS-CHO-02 | MPH wash-station config (CI-67) | OQ-CHO-02 |
| DS-CHO-03 | FS-CHO-03 | Track-Gripper movement log (CI-66) | OQ-CHO-03 |
| DS-CONT-01 | FS-CONT-01 | Static-analyser contamination rule (CI-41, § 8.1) | OQ-CONT-01 |
| DS-CONT-02 | FS-CONT-02 | Wash-step requirement on `sticky=true` (CI-41) | OQ-CONT-02 |
| DS-CONT-03 | FS-CONT-03 | Tip counter per rack (CI-42) | OQ-CONT-03 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 | LDAPS + Conditional Access (§ 7.1) | IQ-AD-01 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 | Veeam T2 + S3 Object Lock + LTO-9 (CI-51) | IQ-BAK-01 |

## Appendix B — Design-level Risk Register

| ID | Risk | Likelihood | Impact | Mitigation reference | Design surface |
|---|---|---|---|---|---|
| DR-01 | Method-Promotion Static Analyser (§ 8.1) silently passes a misclassified liquid-class step on plugin exception | Low | Critical | Plugin authored with default-BLOCK on exception; OQ-LQC-02 negative-path injects exception | § 8.1, CI-31 |
| DR-02 | Pre-Run Validator plugin (§ 8.2) crash → pre-run check skipped silently | Low | Critical | Plugin authored with default-BLOCK on crash; SCM watchdog restarts on crash with audit-trail entry; OQ-WL-02 negative-path test | § 8.2, CI-39 |
| DR-03 | Authority Set ↔ AD-group drift on group rename without VENUS re-binding | Low | Critical | Quarterly access review (CI-60) + VENUS user-manager export reconciled with AD | CI-15..21 |
| DR-04 | Liquid-class library hash drift (manual update outside change control) | Low | High | Hash pinned per method-version (CI-30); pre-run verification compares hash; mismatch blocks run | CI-30, CI-31 |
| DR-05 | Deck-layout `.lay` divergence between sister-site repos and production workstation | Low | High | Method references specific layout hash (CI-29); CI/CD on `iris-venus-decks` blocks unsigned merges | CI-29 |
| DR-06 | ISO 8655 calibration certificate expiry slips past pre-run check due to time-zone drift | Low | High | Cert `expires_at` stored in UTC; NTP enforced 1 s skew (CI-22) | CI-35, CI-36 |
| DR-07 | RFID-confirmation of labware (CI-44) bypassed when RFID-tagged labware temporarily unavailable | Medium | Medium | Operator-confirmation eSign fallback documented; quarterly audit of CI-44 logs for fallback frequency | CI-44 |
| DR-08 | Per-method SDS (§ 8.3 template) varies in quality across method authors → inconsistent regression coverage | Medium | High | Method-promotion checklist `IRS-CHK-LH-METHOD-PROMOTE-001` enforces SDS sections; Method Approver gate (CI-70) | § 8.3, CI-28, CI-70 |
| DR-09 | Hamilton SCN upgrade reverts vendor-default CI (e.g., signature hash) | Low | Critical | Post-upgrade IQ delta-check across all 70 CIs + FS-PART11-09 re-test | CI-09, CI-11 |
| DR-10 | LIMS push mTLS cert `iris-lh-2026q2` expiry blocks provenance upload silently | Low | High | 30-d pre-expiry pager alert + auto-rotation | CI-58 |
| DR-11 | Tip-counter (CI-42) reset event missed when rack hot-swapped during a worklist | Low | High | Hot-swap event triggers blocking dialog requiring rack-reload acknowledgement | CI-42 |
| DR-12 | GitLab `iris-venus-methods` PR-approval bypass via direct-push by automation engineer | Low | Critical | Branch protection (CI-27) denies direct push to `main`; quarterly audit of merged-without-PR commits | CI-27 |
| DR-13 | Operator-decision Reason-Code closed list (CI-12) growth outside change control | Medium | Medium | Quarterly review of reason-code distribution in `wel-lh` SIEM | CI-12 |
| DR-14 | Method-Author training (CI-59 competency) lapses → unqualified author commits | Low | High | LMS gates AD-group membership on competency; competency assessment re-test cycle in Cornerstone | CI-59 |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
