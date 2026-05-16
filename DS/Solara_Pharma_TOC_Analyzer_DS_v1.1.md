---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring 2026-05-15 (Chunk A TOC Analyzer)"
seed_corpus_basis:
  - "SOL-FS-TOC-001 v1.2 (parent FS)"
  - "SOL-URS-TOC-001 v1.2 (transitive parent URS)"
  - "GAMP 5 (2nd Edition) Category 4 — Configuration Specification"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .192, .194"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "USP <643>; USP <645>; USP <1058>; Ph. Eur. 2.2.44"
  - "Sievers / Veolia — DataPro2 v2.4 Installation, Configuration, and Administration Reference (vendor)"
  - "Sievers / Veolia — DataPro2 21 CFR Part 11 Compliance Guide (vendor)"
parent_fs:
  document_number: SOL-FS-TOC-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Solara_Pharma_TOC_Analyzer_FS_v1.3.md
parent_urs:
  document_number: SOL-URS-TOC-001
  version: 1.2
  file: ../../../URS/_generated/final/TOC_Analyzer_Computer_System__Solara_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## TOC Analyzer Computer System — Sievers M9 + DataPro2 v2.4

**Document Number:** SOL-DS-TOC-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** SOL-FS-TOC-001 v1.2 | **Parent URS:** SOL-URS-TOC-001 v1.2 *(informational, transitive)*
**Site:** Solara Pharmaceuticals SA, Utilities Validation Lab, Plant 3, Mendrisio, Switzerland *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Sievers M9 + DataPro2 v2.4** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .160, .165, .192, .194; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <643>; USP <645>; USP <1058>; Ph. Eur. 2.2.44; ICH Q2(R2); PIC/S PI 041; Swissmedic (CH)

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Utilities) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Reviewer (Reagent Standard Custodian) | _____________ | _____________ | _____ |
| Approver (Head of Manufacturing Sciences / Process Owner) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T2 from parent URS+FS pair. DS covers 76/80 FS-IDs; 4 FS-IDs flagged as vendor-internal — no site design surface (FS-AUD-01 DataPro2 audit-trail event schema, FS-PROC-01 DataPro2 calibration + blank-correction engine internals, FS-CMP-02 RE computation algorithm internals, FS-PROC-04 limit-band evaluator internals). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from `SOL-FS-TOC-001` and `SOL-URS-TOC-001`. DS-specific terms:

| Term | Definition |
|---|---|
| `.dpr` | DataPro2 raw data file format |
| `.proc` | DataPro2 derived / processed result file format |
| RE | Response Efficiency (USP <643>): (response_sucrose − blank) / (response_BQ − blank) |
| Authority Set | DataPro2 internal role bundle mapped 1:1 to AD group |
| USP RS Register | Site reagent register tracking USP Reference Standard lots |
| `wel-toc` | Splunk heavy-index name reserved for this system |

## 1. Purpose

This CS records the design that satisfies `SOL-FS-TOC-001` v1.2 — the Sievers M9 + DataPro2 v2.4 configuration plus the integration to LabWare LIMS 8 (via DataShare 5), AD, NTP, NetApp file share, Splunk SIEM, and the USP RS / UV lamp lifecycle bookkeeping. Each CI carries vendor-named parameter, chosen value, default-vs-custom flag, justification, FS-IDs traced, and the planned IQ/OQ verification.

Vendor internals (DataPro2 oxidation calculation engine, membrane CO₂ detector firmware, M9 reactor control firmware) remain Sievers / Veolia's SDLC responsibility.

## 2. Scope

### 2.1 In scope

- DataPro2 v2.4 configuration: Part 11 module, project policy `SOL_TOC_PART11`, authority sets, SST workflow `SOL-SST-USP643`, USP RS register, UV lamp / reactor / ICR lifecycle store, on-line / grab mode, calibration limit banding, LIMS DataShare 5 connector.
- Windows 11 Pro 23H2 + AD GPO baseline.
- Integration design: AD, NTP, NetApp file share, Splunk SIEM, LabWare LIMS 8 via DataShare 5.
- Site-deployed components: SST scheduler hook (FS-SST-02), USP RS pre-flight gate (FS-REA-02).

### 2.2 Out of scope

- Vendor internals (DataPro2 oxidation engine, M9 reactor firmware).
- Sample preparation; water-system loop sanitization (separate validations).
- LIMS-side sample lifecycle (separate validation).

## 3. Architectural Overview

```
                    AD `solara.local` + NTP `ntp.solara.local`
                    │
                    ▼
   ┌───────────────────────────────────────────────────────────┐
   │ TOC Workstation (HP EliteDesk 800 G9, Win 11 Pro 23H2)    │
   │   GPO `SOL-UTIL-LAB-WS` (CI-04, CI-06)                    │
   │   ┌───────────────────────────────────────┐               │
   │   │ DataPro2 v2.4 + Part 11 Module         │              │
   │   │   Project Policy `SOL_TOC_PART11`      │              │
   │   │   (CI-01, CI-02)                       │              │
   │   │   Authority Sets (CI-15..21)           │              │
   │   │   SST Workflow `SOL-SST-USP643`        │              │
   │   │   (CI-30..34)                          │              │
   │   │   USP RS Register (CI-40..44)          │              │
   │   │   UV-Lamp + Reactor Lifecycle (CI-50..54)│             │
   │   │   Limit-band evaluator (CI-60)         │              │
   │   │   DataShare 5 → LIMS (CI-65..68)       │              │
   │   └────┬─────────────────────────────────┘                │
   │        │ USB-3 to Sievers M9                              │
   └────────┼─────────────────────────────────────────────────┘
            │
            ├──► NetApp `\\sol-gmp-fs01\toc-projects` (CI-25)
            ├──► NetApp `\\sol-gmp-fs01\toc-qual` (WORM, 25 y) (CI-26)
            ├──► Splunk UF → `wel-toc` (CI-70)
            └──► LabWare LIMS 8 (DataShare 5, CI-65..68)
```

## 4. Configuration Specification

Vendor-named CIs per *Sievers DataPro2 v2.4 Installation, Configuration, and Administration Reference* (rev. 2024-08) and *DataPro2 21 CFR Part 11 Compliance Guide* (rev. 2024-08).

| CI-ID | Configuration item (named per vendor) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| CI-01 | DataPro2 → Part 11 Module → `Audit Trail Required` | `true` | Custom | Per FS-SW-07 / FS-AUD-01. | FS-SW-07, FS-AUD-01 | IQ-CFG-01 |
| CI-02 | DataPro2 → Part 11 Module → `eSign Required` + `Raw Data Lock` | `true` (both) | Custom | Per FS-SW-07 / FS-DI-04. | FS-SW-07, FS-DI-04 | IQ-CFG-02 |
| CI-03 | DataPro2 → Project Policy → `SOL_TOC_PART11` | Active | Custom | Per FS-SW-07. | FS-SW-07 | OQ-PROJECT-POLICY-01 |
| CI-04 | GPO `SOL-UTIL-LAB-WS` → Local-admin disable | Enabled (only `solara\bg-toc-admin`) | Custom | Per FS-SEC-01 / FS-PART11-02. | FS-SEC-01, FS-PART11-02 | IQ-GPO-01 |
| CI-05 | GPO Audit Policy (Logon / Account-Mgmt / Object-Access) | All Success + Failure | Custom | Forwards to Splunk per FS-SW-04. | FS-SW-04 | IQ-GPO-02 |
| CI-06 | GPO `SOL-LAB-LOCK` → screen lock | 10 min idle; AD re-auth required | Custom | Per FS-SW-06. | FS-SW-06 | IQ-GPO-03 |
| CI-07 | GPO `SOL-LAB-USB-BLOCK` | USB mass-storage denied; override via CR | Custom | Per FS-SEC-02. | FS-SEC-02 | IQ-GPO-04 |
| CI-08 | Workstation VLAN | `vlan-gmp-utilities` | Custom | Per FS-HW-04. | FS-HW-04 | IQ-NW-01 |
| CI-09 | DataPro2 → eSign → `RequireReAuthOnSign` | `true` | Custom | Per FS-PART11-06. | FS-PART11-06 | OQ-PART11-06 |
| CI-10 | DataPro2 → eSign → Meaning-of-Signature closed list | `Review, Approve, Reject, Lock, USP-RS-Acceptance, Lamp-Replacement, Reactor-Replacement` | Custom | Per FS-PART11-03 / FS-LIFE-02 / FS-REA-01. | FS-PART11-03, FS-LIFE-02, FS-REA-01 | OQ-PART11-03 |
| CI-11 | DataPro2 → eSign → Signature hash | `SHA-256` | Default | Per FS-PART11-04. | FS-PART11-04 | OQ-PART11-04 |
| CI-12 | DataPro2 → Reason-for-Change closed list (operations) | `baseline-noise, blank-correction-adjustment, integration-correction, sample-loop-flush, instrument-glitch, sample-prep-error, other-with-justification` | Custom | Per FS-PROC-02. | FS-PROC-02 | OQ-PROC-02 |
| CI-13 | DataPro2 → Audit-trail DB constraint | `Append-only` (DELETE grant revoked at DBA + vendor level) | Custom | Per FS-AUD-02. | FS-AUD-02 | OQ-AUD-APPENDONLY-01 |
| CI-14 | DataPro2 → Retrospective-entry flag | Enabled (mandatory delay reason) | Custom | Per FS-DI-03. | FS-DI-03 | OQ-DI-03 |
| CI-15 | DataPro2 Authority Set ↔ AD-group `Lab-TOC-Analysts` | `Analyst` (acquire / integrate; no method-edit; no Approve eSign) | Custom | Per FS-PART11-02. | FS-PART11-02, FS-ACQ-01 | OQ-ROLE-01 |
| CI-16 | DataPro2 Authority Set ↔ `Lab-TOC-SeniorAnalysts` | `SeniorAnalyst` (Review eSign) | Custom | Per FS-AUD-03. | FS-AUD-03 | OQ-ROLE-02 |
| CI-17 | DataPro2 Authority Set ↔ `Lab-TOC-MethodOwners` | `MethodOwner` (method create/edit) | Custom | Per FS-ACQ-01. | FS-ACQ-01 | OQ-ROLE-03 |
| CI-18 | DataPro2 Authority Set ↔ `Lab-TOC-QCManagers` | `QCManager` (Approve eSign; LIMS-export flip; SST override) | Custom | Per FS-SST-04 / FS-INT-02. | FS-SST-04, FS-INT-02 | OQ-ROLE-04 |
| CI-19 | DataPro2 Authority Set ↔ `Lab-TOC-ReagentCustodians` | `ReagentCustodian` (USP RS register write; SST eSign-acceptance) | Custom | Per FS-REA-01 / URS § 4 SoD rule. | FS-REA-01 | OQ-ROLE-05 |
| CI-20 | DataPro2 Authority Set ↔ `Lab-TOC-SysAdmin` | `SysAdmin` (config; cannot Approve) | Custom | Per FS-PART11-02 (operator/approver split). | FS-PART11-02 | OQ-ROLE-06 |
| CI-21 | DataPro2 Authority Set ↔ `Lab-TOC-Auditor` | `Auditor` (read-only) | Custom | Per URS § 4 + FS-AUD-05 pattern. | FS-AUD-03 | OQ-ROLE-07 |
| CI-22 | DataPro2 → SoD enforcement | Analyst ≠ Reviewer ≠ Approver on same record; Reagent Custodian ≠ Analyst on same SST | Custom | Per URS § 4 SoD + FS-PART11-06 pattern. | FS-AUD-03, FS-REA-01 | OQ-ROLE-SOD |
| CI-23 | Windows Time → NTP source | `ntp.solara.local`; skew threshold 1 s | Custom | Per FS-SW-05. | FS-SW-05 | IQ-NTP-01 |
| CI-24 | UPS APC SMT1500 → PowerChute shutdown | 20% remaining | Custom | Per FS-HW-03. | FS-HW-03 | IQ-HW-03 |
| CI-25 | NetApp share → TOC projects | `\\sol-gmp-fs01\toc-projects` (NTFS ACL: local C: write blocked) | Custom | Per FS-SW-03. | FS-SW-03 | IQ-FS-01 |
| CI-26 | NetApp SnapLock Compliance share → Qual evidence | `\\sol-gmp-fs01\toc-qual` (WORM, 25 y) | Custom | Per FS-AIQ-06 / FS-AUD-04. | FS-AIQ-06, FS-AUD-04 | IQ-FS-02 |
| CI-27 | HP EliteDesk 800 G9 baseline | 32 GB RAM, 1 TB SSD, 4× USB-3 dedicated | Custom | Per FS-HW-02. | FS-HW-02 | IQ-HW-02 |
| CI-28 | DataPro2 → Asset-register binding | One-to-one workstation ↔ M9 serial | Custom | Per FS-HW-01. | FS-HW-01 | IQ-HW-01 |
| CI-29 | DataPro2 → Autosampler qualification | Sievers SOP qualification record at install + post-service | Custom | Per FS-HW-06. | FS-HW-06 | IQ-HW-06 |
| CI-30 | DataPro2 → SST Workflow `SOL-SST-USP643` | triplicate water-blank → triplicate 500 ppb sucrose → triplicate 500 ppb BQ; auto-compute RE; verdict 85% ≤ RE ≤ 115% | Custom | Per FS-SST-01 / FS-CMP-02. | FS-SST-01, FS-CMP-02 | OQ-SST-01 |
| CI-31 | DataPro2 → SST Scheduler | Daily (grab) / Weekly (on-line); per-method override on EFFECTIVE | Custom | Per FS-SST-02. | FS-SST-02 | OQ-SST-02 |
| CI-32 | DataPro2 → SST Record schema | `op_id, ts, USP_RS_lot, cert_expiry, blank_value, sucrose_value, BQ_value, RE, verdict` (immutable) | Custom | Per FS-SST-03. | FS-SST-03 | OQ-SST-03 |
| CI-33 | DataPro2 → SST-Failure FSM transition | Instrument → `NOT_READY`; sequence runner blocks; override requires `Lab-TOC-QCManagers` co-sign + RFC | Custom | Per FS-SST-04. | FS-SST-04 | OQ-SST-04 |
| CI-34 | DataPro2 → SST 12-month trend dashboard | Early-warning band at RE ≤ 90% or ≥ 110% | Custom | Per FS-SST-05. | FS-SST-05 | OQ-SST-05 |
| CI-40 | DataPro2 → USP RS Register schema | `rs_id, type (sucrose/BQ/blank), source, lot, COA_id, receipt_date, opening_date, expiry, custodian` | Custom | Per FS-REA-01. | FS-REA-01 | OQ-REA-01 |
| CI-41 | DataPro2 → SST Pre-Flight USP RS gate | Reject SST start when bound `USP_RS_lot.expires_at < now()` | Custom | Per FS-REA-02. | FS-REA-02 | OQ-REA-02 |
| CI-42 | DataPro2 → Working-Standard Register | `prep_date, prep_analyst, source_RS_lot, expiry (same-day sucrose)` | Custom | Per FS-REA-03. | FS-REA-03 | OQ-REA-03 |
| CI-43 | DataPro2 → Low-TOC Water Blank register | Lot + COA showing < 50 ppb TOC at receipt | Custom | Per FS-REA-04. | FS-REA-04 | OQ-REA-04 |
| CI-44 | DataPro2 → Waste Disposal log | `SOL-LOG-WASTE-TOC`; EHS SOP reference | Custom | Per FS-REA-05. | FS-REA-05 | OQ-REA-05 |
| CI-50 | DataPro2 → UV-Lamp Lifecycle store | install_date + 30-d-warning at 11 months + 12-m replacement target | Custom | Per FS-LIFE-01. | FS-LIFE-01 | OQ-LIFE-01 |
| CI-51 | DataPro2 → UV-Lamp Replacement Workflow `SOL-WF-LAMP-CHANGE` | Triggers full PQ per FS-AIQ-04 | Custom | Per FS-LIFE-02. | FS-LIFE-02 | OQ-LIFE-02 |
| CI-52 | DataPro2 → Lamp-Intensity per-acquisition capture | SOP threshold configurable; drop below → deviation | Custom | Per FS-LIFE-02b / FS-HW-05. | FS-LIFE-02b, FS-HW-05 | OQ-LIFE-02b |
| CI-53 | DataPro2 → Reactor + ICR Replacement Log | Replacement → SST + partial OQ trigger | Custom | Per FS-LIFE-03. | FS-LIFE-03 | OQ-LIFE-03 |
| CI-54 | DataPro2 → Membrane CO₂ Detector Replacement schedule | Per Sievers spec | Custom | Per FS-LIFE-04. | FS-LIFE-04 | OQ-LIFE-04 |
| CI-55 | DataPro2 → Compendial Limit binding (WFI / PW) | `500 ppb` default; per-method override on APPROVED methods only | Custom | Per FS-CMP-01. | FS-CMP-01 | OQ-CMP-01 |
| CI-56 | DataPro2 → EP-monograph compendium flag | `Compendium ∈ {USP, EP, JP, NON-COMP}`; EP enables Ph. Eur. 2.2.44 control tests | Custom | Per FS-CMP-03 / FS-CMP-05. | FS-CMP-03, FS-CMP-05 | OQ-CMP-03 |
| CI-57 | OQ LOD protocol binding | Replicate 50 ppb sucrose; verify 3×SD(blank) ≤ 50 ppb | Custom | Per FS-CMP-04 / FS-AIQ-03. | FS-CMP-04, FS-AIQ-03 | OQ-CMP-04 |
| CI-58 | OQ Battery binding (`SOL-OQ-TOC-001`) | RE + LOD + 5-point linearity 50-5000 ppb + accuracy + precision RSD ≤ 5% + carry-over | Custom | Per FS-AIQ-03. | FS-AIQ-03 | OQ-AIQ-03 |
| CI-59 | DQ + PQ binding | `SOL-DQ-TOC-001` + `SOL-PQ-TOC-001` (annual + on major change) | Custom | Per FS-AIQ-01 / FS-AIQ-04 / FS-AIQ-05. | FS-AIQ-01, FS-AIQ-04, FS-AIQ-05 | (admin) |
| CI-60 | DataPro2 → Limit-band evaluator binding | `30% TREND / 50% OOT / 100% OOS` of 500 ppb (or method-defined) | Custom | Per FS-PROC-04. | FS-PROC-04 | OQ-PROC-04 |
| CI-61 | DataPro2 → Mode-binding | On-line uses sample loop continuous draw; Grab uses autosampler; mode-specific SST cadence per CI-31 | Custom | Per FS-ACQ-04. | FS-ACQ-04 | OQ-ACQ-04 |
| CI-62 | DataPro2 → Pre-flight checker | `instrument_state.Ready && method.state=EFFECTIVE && SST.valid && !project.lock` | Custom | Per FS-ACQ-02. | FS-ACQ-02 | OQ-ACQ-02 |
| CI-63 | DataPro2 → Acquisition metadata schema | `sample_id, source_point, method_id+ver, instrument_id, analyst_id, ts, mode, lamp_hours, reactor_lot` | Custom | Per FS-ACQ-03. | FS-ACQ-03 | OQ-ACQ-03 |
| CI-64 | DataPro2 → OOS workflow trigger | OOS flag → LIMS workflow `LIMS-WF-211192`; sample-point → HOLD | Custom | Per FS-PROC-06. | FS-PROC-06 | OQ-PROC-06 |
| CI-65 | DataShare 5 → LIMS worklist poll | `https://lims.solara.local/api/v3/worklist` every 5 min (read-only) | Custom | Per FS-INT-01. | FS-INT-01 | OQ-INT-01 |
| CI-66 | DataShare 5 → Result push gate | `result_state == APPROVED && SST.valid` | Custom | Per FS-INT-02 / FS-INT-04. | FS-INT-02, FS-INT-04 | OQ-INT-02 |
| CI-67 | DataShare 5 → Payload schema | `report_id, instrument_id, method_id+ver, reviewer_id, approver_id, sst_status` | Custom | Per FS-INT-03. | FS-INT-03 | OQ-INT-03 |
| CI-68 | Site PKI → mTLS cert | `solara-toc-2026q2` (auto-rotate 1y) | Custom | (Mirrors corpus integration pattern for FS-INT-02 mTLS) | FS-INT-02 | IQ-PKI-01 |
| CI-69 | Veeam B&R 12.1 → backup job `SOL-JOB-BAK-TOC` | Daily + SHA-256 manifest + S3 Object Lock + LTO-9 | Custom | Per FS-BAK-01 / FS-XSYS-BAK-01. | FS-BAK-01, FS-XSYS-BAK-01 | IQ-BAK-01 |
| CI-70 | Splunk UF → heavy index | `wel-toc` (TCP/9997 outbound) | Custom | Per FS-SW-04 / FS-AUD-01 / FS-XSYS-AD-01. | FS-SW-04, FS-XSYS-AD-01 | IQ-SIEM-01 |
| CI-71 | Splunk Alert `wel-toc-availability` | Workstation up + DataPro2 service running | Custom | Per FS-PERF-01. | FS-PERF-01 | OQ-PERF-01 |
| CI-72 | Splunk Alert `wel-toc-lockout` | AD lockout for `Lab-TOC-*` group | Custom | Per FS-PART11-07. | FS-PART11-07 | OQ-PART11-07 |
| CI-73 | AD Password Policy | 12-char / 90-d / complexity 3-of-4 / lockout 5/15 min (GPO `SOL-LAB-USERS-PWD`) | Custom | Per FS-PART11-07. | FS-PART11-07 | IQ-AD-01 |
| CI-74 | AD HR Feed → SID-on-rehire | New SID on rehire | Custom | Per FS-PART11-05 (uniqueness). | FS-PART11-05 | IQ-AD-02 |
| CI-75 | CrowdStrike Falcon → exclusion list | Sievers-approved DataPro2 paths | Custom | Per FS-SW-08 / FS-SEC-02. | FS-SW-08 | IQ-AV-01 |
| CI-76 | Cornerstone LMS → curriculum gate | `SOL-TOC-101` (Analyst) + `SOL-TOC-201` (SST + lifecycle); annual re-completion | Custom | Per FS-TRN-01. | FS-TRN-01 | IQ-LMS-01 |
| CI-77 | Periodic Review template binding | `SOL-PR-TOC` (QC Mgr + QA Mgr eSign) | Custom | Per FS-PR-01. | FS-PR-01 | OQ-PR-01 |
| CI-78 | Validation Dossier binding | `SOL-VAL-TOC-001` | Custom | Per FS-PART11-01. | FS-PART11-01 | (admin) |
| CI-79 | DR Runbook binding | RTO 8 h / RPO 24 h per `SOL-SOP-RESTORE-TEST` | Custom | Per FS-BAK-02 / FS-BAK-03. | FS-BAK-02, FS-BAK-03 | IQ-BAK-02 |
| CI-80 | PDF/A-3 Report template `SOL-RPT-TOC` | Active; embedded fonts + ICC | Custom | Per FS-PROC-05 / FS-DI-02. | FS-PROC-05, FS-DI-02 | OQ-RPT-01 |
| CI-81 | DataPro2 → SCN change-control binding | `CCR-TOC-*`; build hash verified at partial-OQ re-test | Custom | Per FS-SW-08. | FS-SW-08 | (admin) |
| CI-82 | DataPro2 → AD-bind LDAPS endpoint | `ldaps://solara.local:636` | Custom | Per FS-SEC-01 / FS-XSYS-AD-01. | FS-SEC-01, FS-XSYS-AD-01 | IQ-AD-03 |
| CI-83 | Break-glass `solara\bg-toc-admin` vault | CyberArk PAM (24h password rotation, dual-witness) | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | IQ-PAM-01 |
| CI-84 | Audit-Trail Review templates | `SOL-AUD-REVIEW-TOC-BATCH` (per batch) + `SOL-AUD-REVIEW-TOC-MONTH` (monthly) | Custom | Per FS-AUD-03. | FS-AUD-03 | OQ-AUD-03 |

## 5. Workflow + Business-Rule Design

### 5.1 USP <643> SST Workflow `SOL-SST-USP643`

Per FS-SST-01..05. Triplicate water blank → triplicate 500 ppb sucrose → triplicate 500 ppb BQ (CI-30). Auto-compute RE = (response_sucrose − blank) / (response_BQ − blank). Verdict pass when 85% ≤ RE ≤ 115% per USP <643> / FS-CMP-02. Failure flips instrument FSM to `NOT_READY` (CI-33); QC Manager co-sign + RFC required to override. Scheduler (CI-31) daily for grab, weekly for on-line. 12-month rolling trend (CI-34) flags early-warning bands.

### 5.2 USP RS Lifecycle Workflow `SOL-WF-USPRS`

Per FS-REA-01..05. Reagent Custodian receives USP RS sucrose / 1,4-benzoquinone; logs to register (CI-40). SST pre-flight (CI-41) rejects start when bound USP_RS_lot expired. Working-standard register (CI-42) tracks per-prep records; sucrose same-day shelf life. Low-TOC water blank register (CI-43). Waste log (CI-44). Reagent Custodian ≠ Analyst on same SST enforced via CI-22.

### 5.3 UV Lamp + Reactor + ICR Lifecycle Workflow `SOL-WF-LAMP-CHANGE`

Per FS-LIFE-01..04. Lamp install logged (CI-50); 30-d warning at 11 months. Replacement (CI-51) triggers full PQ per CI-58 / CI-59. Per-acquisition lamp intensity captured (CI-52); SOP-threshold drop → deviation. Reactor + ICR replacement (CI-53) triggers SST + partial OQ. Membrane CO₂ replacement (CI-54) tracked per Sievers spec.

### 5.4 Acquisition + Processing + OOS Workflow `SOL-WF-RUN`

Per FS-ACQ-01..04 / FS-PROC-01..06. Pre-flight checker (CI-62) gates on instrument-Ready / method-EFFECTIVE / SST-valid / project-not-locked. Mode binding (CI-61) for on-line vs grab. Metadata (CI-63). Limit-band evaluator (CI-60) flags 30/50/100% TREND/OOT/OOS. OOS triggers LIMS workflow `LIMS-WF-211192` (CI-64) and HOLDs water-system sample point.

### 5.5 Approval + LIMS Push Workflow `SOL-WF-APPROVE-LIMS`

Analyst → Senior Analyst eSign Review → QC Manager eSign Approve flips `LimsExport=true`. DataShare 5 push gate (CI-66) requires APPROVED + SST.valid. Payload (CI-67) signed with mTLS cert CI-68.

### 5.6 Audit-Trail Review Workflow `SOL-WF-AUDIT-REVIEW`

Per FS-AUD-03. Per-batch Senior Analyst review (`SOL-AUD-REVIEW-TOC-BATCH`); monthly QC Manager review (`SOL-AUD-REVIEW-TOC-MONTH`) (CI-84).

### 5.7 Annual Periodic Review Workflow `SOL-WF-PR`

Per FS-PR-01. Template `SOL-PR-TOC` (CI-77) covers configuration, audit-trail evidence, SST trend, lifecycle health, reagent register, deviations, backup-restore, training. Signed QC Mgr + QA Mgr.

## 6. Role-Permission Matrix Design

Implements FS-PART11-02 / FS-AUD-03 / FS-REA-01 / FS-SST-04. AD groups bind 1:1 to Authority Sets (CI-15..21).

| Permission | Analyst | SeniorAnalyst | MethodOwner | QCManager | ReagentCustodian | SysAdmin | Auditor |
|---|---|---|---|---|---|---|---|
| Acquire sequence | ✓ | ✓ | ✓ | ✓ | – | – | – |
| Integrate / process | ✓ | ✓ | ✓ | ✓ | – | – | – |
| Manual reprocess (with RFC) | ✓ | ✓ | ✓ | ✓ | – | – | – |
| eSign `Review` | – | ✓ | – | – | – | – | – |
| eSign `Approve` (result) | – | – | – | ✓ | – | – | – |
| eSign `Approve` (method) | – | – | – | ✓ | – | – | – |
| eSign `Reject` | – | ✓ | – | ✓ | – | – | – |
| SST override (after FAIL) | – | – | – | ✓ (co-sign + RFC) | – | – | – |
| USP RS Register write | – | – | – | – | ✓ | – | – |
| USP RS Acceptance eSign | – | – | – | – | ✓ | – | – |
| Lamp / Reactor lifecycle log write | – | – | – | – | – | ✓ | – |
| Method create / edit | – | – | ✓ | – | – | – | – |
| Flip `LimsExport` | – | – | – | ✓ | – | – | – |
| DataPro2 config edit | – | – | – | – | – | ✓ | – |
| AD group membership change | – | – | – | – | – | ✓ (via ticket) | – |
| Read audit trail | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Export audit trail (PDF) | – | ✓ | – | ✓ | – | ✓ | ✓ |
| Read raw / processed / report | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

Hard constraints (CI-22): Analyst ≠ Reviewer ≠ Approver on same record; Reagent Custodian ≠ Analyst on same SST.

## 7. Integration Design

### 7.1 IF-AD (LDAPS)

| Aspect | Design |
|---|---|
| Endpoint | `ldaps://solara.local:636` (CI-82) |
| Groups | `Lab-TOC-Analysts`, `-SeniorAnalysts`, `-MethodOwners`, `-QCManagers`, `-ReagentCustodians`, `-SysAdmin`, `-Auditor` |
| Conditional Access | `Lab-Workstation Conditional Access (MFA on interactive logon)` per FS-XSYS-AD-01 |
| Break-glass | CyberArk PAM (CI-83) |
| FS-IDs traced | FS-SEC-01, FS-PART11-02, FS-XSYS-AD-01 |

### 7.2 IF-NTP

| Aspect | Design |
|---|---|
| Endpoint | `ntp.solara.local` UDP/123 |
| Skew | `1 s` (CI-23) |
| FS-IDs traced | FS-SW-05 |

### 7.3 IF-FS (NetApp SMB / SnapLock)

| Aspect | Design |
|---|---|
| TOC projects | `\\sol-gmp-fs01\toc-projects` (CI-25) |
| Qual evidence WORM | `\\sol-gmp-fs01\toc-qual` (CI-26) 25 y |
| FS-IDs traced | FS-SW-03, FS-AIQ-06, FS-AUD-04 |

### 7.4 IF-SIEM (Splunk UF)

| Aspect | Design |
|---|---|
| Endpoint | TCP/9997 outbound |
| Heavy index | `wel-toc` (CI-70) |
| Alerts | `wel-toc-availability` (CI-71); `wel-toc-lockout` (CI-72) |
| FS-IDs traced | FS-SW-04, FS-PERF-01, FS-PART11-07 |

### 7.5 IF-LIMS (LabWare LIMS 8 via DataShare 5)

| Aspect | Design |
|---|---|
| Worklist poll | `https://lims.solara.local/api/v3/worklist` every 5 min (CI-65) |
| Push gate | APPROVED + SST.valid (CI-66) |
| Schema | `report_id, instrument_id, method_id+ver, reviewer_id, approver_id, sst_status` (CI-67) |
| mTLS | `solara-toc-2026q2` cert (CI-68) |
| FS-IDs traced | FS-INT-01..04 |

### 7.6 IF-Backup (Veeam → S3 Object Lock + LTO-9)

| Aspect | Design |
|---|---|
| Job | `SOL-JOB-BAK-TOC` daily (CI-69) |
| Cold tier | S3 Object Lock Compliance + LTO-9 monthly |
| Restore test | Quarterly QC-witnessed `SOL-SOP-RESTORE-TEST` (CI-79) |
| FS-IDs traced | FS-BAK-01, FS-BAK-02, FS-BAK-03, FS-XSYS-BAK-01 |

## 8. Site-Deployed Components (micro-SDS)

Two minor site components extend the DataPro2 platform.

### 8.1 `SOL-PLUGIN-SST-PREFLIGHT-01` — SST Pre-Flight Gate

| Field | Value |
|---|---|
| Type | DataPro2 plugin (Sievers SDK; C#) registered as SST-start hook |
| Responsibility | FS-REA-02 USP RS expiry block + FS-SST-04 SST-failure FSM transition gate |
| Inputs | SST run handle + bound USP_RS_lot |
| Outputs | `SST-OK` or `SST-BLOCK <reason>` with audit-trail entry |
| Algorithm | `if rs_lot.expires_at < now(): BLOCK "USP RS expired"; if instrument.state != Ready: BLOCK "Instrument not ready"; if lamp.expires_at < now(): BLOCK "Lamp lifecycle expired"; else OK` |
| Storage | DataPro2 plugin registry (SysAdmin write via signed CR) |
| Unit-test | OQ-REA-02 + OQ-SST-04 (one fixture per BLOCK branch + happy path) |
| FS-IDs traced | FS-REA-02, FS-SST-04 |

### 8.2 `SOL-PLUGIN-SST-SCHEDULER-01` — SST Cadence Scheduler

| Field | Value |
|---|---|
| Type | DataPro2 plugin (C# Windows service) |
| Responsibility | FS-SST-02 mode-aware SST cadence enforcement |
| Inputs | DataPro2 method-mode binding (on-line / grab) |
| Outputs | SST due/overdue state; updates DataPro2 instrument FSM |
| Algorithm | Daily tick: read mode; if grab and last_sst > 24 h, mark SST overdue; if on-line and last_sst > 7 d, mark SST overdue; on overdue, set instrument → SST_OVERDUE; QC Manager eSign required to bypass for method-override window |
| Storage | DataPro2 plugin registry |
| Unit-test | OQ-SST-02 (one fixture per mode + overdue path) |
| FS-IDs traced | FS-SST-02 |

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .68, .160, .165, .192, .194.
- FDA *Guidance for Industry — High Purity Water Systems* (1993).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- Ph. Eur. 2.2.44 — Total Organic Carbon; Ph. Eur. 0008 — Water for Injections.

### DACH
- Swissmedic — Swiss water-system inspection guidance (site is Mendrisio, CH).

### International
- USP <643>; USP <645>; USP <1058>; USP <1225>; USP <1231>.
- ICH Q2(R2); PIC/S PI 041.
- ISPE GAMP 5 (2nd Ed., 2022); ISPE *Baseline Guide Vol. 4: Water and Steam Systems*.

### Vendor
- Sievers / Veolia — *M9 TOC Analyzer Configuration Reference* (rev. 2024-08).
- Sievers / Veolia — *DataPro2 v2.4 Installation, Configuration, and Administration Reference* (rev. 2024-08).
- Sievers / Veolia — *DataPro2 21 CFR Part 11 Compliance Guide* (rev. 2024-08).

### Site / parent
- `SOL-FS-TOC-001 v1.2`; `SOL-URS-TOC-001 v1.2`.
- `SOL-VAL-TOC-001`; `SOL-SOP-CC-TOC`; `SOL-SOP-IR-TOC`; `SOL-SOP-RESTORE-TEST`.

## Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) | Design intent (brief) | Verified by |
|---|---|---|---|
| DS-HW-01 | FS-HW-01 | Asset-register one-to-one (CI-28) | IQ-HW-01 |
| DS-HW-02 | FS-HW-02 | HP EliteDesk 800 G9 baseline (CI-27) | IQ-HW-02 |
| DS-HW-03 | FS-HW-03 | UPS APC SMT1500 + 20% shutdown (CI-24) | IQ-HW-03 |
| DS-HW-04 | FS-HW-04 | GMP-VLAN (CI-08) | IQ-NW-01 |
| DS-HW-05 | FS-HW-05 | Lamp / reactor stream + alarm thresholds (CI-52) | OQ-LIFE-02b |
| DS-HW-06 | FS-HW-06 | Autosampler qualification (CI-29) | IQ-HW-06 |
| DS-SW-01 | FS-SW-01 | Win 11 Pro 23H2 image + AD-bind (CI-04) | IQ-GPO-01 |
| DS-SW-02 | FS-SW-02 | DataPro2 install record (Sievers engineer) | IQ-INSTALL-01 |
| DS-SW-03 | FS-SW-03 | TOC projects share + local-C: ACL (CI-25) | IQ-FS-01 |
| DS-SW-04 | FS-SW-04 | Splunk forwarder (CI-70) | IQ-SIEM-01 |
| DS-SW-05 | FS-SW-05 | NTP + 1 s skew (CI-23) | IQ-NTP-01 |
| DS-SW-06 | FS-SW-06 | Screen-lock GPO (CI-06) | IQ-GPO-03 |
| DS-SW-07 | FS-SW-07 | Project Policy SOL_TOC_PART11 (CI-01..03) | OQ-PROJECT-POLICY-01 |
| DS-SW-08 | FS-SW-08 | SCN CR + CrowdStrike exclusion (CI-75, CI-81) | IQ-AV-01 |
| DS-CMP-01 | FS-CMP-01 | Compendial limit binding 500 ppb (CI-55) | OQ-CMP-01 |
| DS-CMP-02 | (vendor-internal — RE computation algorithm) + CI-30 SST workflow | SST Workflow SOL-SST-USP643 (CI-30) | OQ-SST-01 |
| DS-CMP-03 | FS-CMP-03 | EP compendium flag (CI-56) | OQ-CMP-03 |
| DS-CMP-04 | FS-CMP-04 | OQ LOD protocol (CI-57) | OQ-CMP-04 |
| DS-CMP-05 | FS-CMP-05 | Method header `compendium` enum (CI-56) | OQ-CMP-03 |
| DS-AIQ-01 | FS-AIQ-01 | DQ SOL-DQ-TOC-001 (CI-59) | (admin) |
| DS-AIQ-02 | FS-AIQ-02 | IQ SOL-IQ-TOC-001 — install + AD-bind + build hash + lamp/reactor | IQ-AIQ-02 |
| DS-AIQ-03 | FS-AIQ-03 | OQ battery SOL-OQ-TOC-001 (CI-58) | OQ-AIQ-03 |
| DS-AIQ-04 | FS-AIQ-04 | PQ schedule (CI-59) — go-live + lamp / reactor / SW upgrade / annual | (admin) |
| DS-AIQ-05 | FS-AIQ-05 | Partial PQ post-PM (CI-59) | OQ-AIQ-05 |
| DS-AIQ-06 | FS-AIQ-06 | Qual evidence WORM 25 y (CI-26) | IQ-FS-02 |
| DS-SST-01 | FS-SST-01 | SST workflow (CI-30) | OQ-SST-01 |
| DS-SST-02 | FS-SST-02 | SST scheduler + plugin § 8.2 (CI-31) | OQ-SST-02 |
| DS-SST-03 | FS-SST-03 | SST record schema (CI-32) | OQ-SST-03 |
| DS-SST-04 | FS-SST-04 | NOT_READY transition + override (CI-33, § 8.1) | OQ-SST-04 |
| DS-SST-05 | FS-SST-05 | 12-month RE trend (CI-34) | OQ-SST-05 |
| DS-REA-01 | FS-REA-01 | USP RS Register schema (CI-40) | OQ-REA-01 |
| DS-REA-02 | FS-REA-02 | SST pre-flight USP RS gate (CI-41, § 8.1) | OQ-REA-02 |
| DS-REA-03 | FS-REA-03 | Working-standard register (CI-42) | OQ-REA-03 |
| DS-REA-04 | FS-REA-04 | Low-TOC water blank register (CI-43) | OQ-REA-04 |
| DS-REA-05 | FS-REA-05 | Waste log (CI-44) | OQ-REA-05 |
| DS-LIFE-01 | FS-LIFE-01 | Lamp lifecycle store + warning (CI-50) | OQ-LIFE-01 |
| DS-LIFE-02 | FS-LIFE-02 | Lamp-replacement workflow (CI-51) | OQ-LIFE-02 |
| DS-LIFE-02b | FS-LIFE-02b | Per-acq lamp intensity (CI-52) | OQ-LIFE-02b |
| DS-LIFE-03 | FS-LIFE-03 | Reactor + ICR replacement log (CI-53) | OQ-LIFE-03 |
| DS-LIFE-04 | FS-LIFE-04 | Membrane CO₂ schedule (CI-54) | OQ-LIFE-04 |
| DS-ACQ-01 | FS-ACQ-01 | Method library ACL + EFFECTIVE binding | OQ-ACQ-01 |
| DS-ACQ-02 | FS-ACQ-02 | Pre-flight checker (CI-62) | OQ-ACQ-02 |
| DS-ACQ-03 | FS-ACQ-03 | Acquisition metadata schema (CI-63) | OQ-ACQ-03 |
| DS-ACQ-04 | FS-ACQ-04 | Mode binding on-line / grab (CI-61) | OQ-ACQ-04 |
| DS-PROC-01 | (vendor-internal — DataPro2 calibration + blank-correction engine) | Engine consumed; per-method config | OQ-PROC-01 |
| DS-PROC-02 | FS-PROC-02 | RFC closed list (CI-12) | OQ-PROC-02 |
| DS-PROC-03 | FS-PROC-03 | Raw `.dpr` preserved; `.proc` parent ptr (vendor + CI-02 Raw Data Lock) | OQ-PROC-03 |
| DS-PROC-04 | (vendor-internal — limit-band evaluator engine) + thresholds CI-60 | Threshold binding 30/50/100% (CI-60) | OQ-PROC-04 |
| DS-PROC-05 | FS-PROC-05 | PDF/A-3 report template (CI-80) | OQ-RPT-01 |
| DS-PROC-06 | FS-PROC-06 | OOS → LIMS-WF-211192 + HOLD (CI-64) | OQ-PROC-06 |
| DS-AUD-01 | (vendor-internal — DataPro2 audit-trail event schema) | n/a (flagged) | n/a |
| DS-AUD-02 | FS-AUD-02 | Append-only DB constraint (CI-13) | OQ-AUD-APPENDONLY-01 |
| DS-AUD-03 | FS-AUD-03 | Per-batch + monthly review templates (CI-84) | OQ-AUD-03 |
| DS-AUD-04 | FS-AUD-04 | SnapLock retention 25y/7y (CI-26) | IQ-FS-02 |
| DS-PART11-01 | FS-PART11-01 | SOP catalogue (CI-78) | (admin) |
| DS-PART11-02 | FS-PART11-02 | AD-bound access (CI-04, CI-15..21) | OQ-ROLE-01..07 |
| DS-PART11-03 | FS-PART11-03 | Meaning-of-sig closed list (CI-10) | OQ-PART11-03 |
| DS-PART11-04 | FS-PART11-04 | SHA-256 sig payload (CI-11) | OQ-PART11-04 |
| DS-PART11-05 | FS-PART11-05 | AD UPN + SID-on-rehire (CI-74) | IQ-AD-02 |
| DS-PART11-06 | FS-PART11-06 | RequireReAuthOnSign (CI-09) | OQ-PART11-06 |
| DS-PART11-07 | FS-PART11-07 | AD password policy + lockout alert (CI-73, CI-72) | OQ-PART11-07 |
| DS-DI-01 | FS-DI-01 | op_id captured (Authority Set binding) | OQ-DI-01 |
| DS-DI-02 | FS-DI-02 | PDF/A-3 render (CI-80) | OQ-RPT-01 |
| DS-DI-03 | FS-DI-03 | Retrospective-entry flag (CI-14) | OQ-DI-03 |
| DS-DI-04 | FS-DI-04 | Raw `.dpr` preserved (Project Policy CI-02) | OQ-PROC-03 |
| DS-DI-05 | FS-DI-05 | SST + OQ calibration verify (CI-30, CI-58) | OQ-AIQ-03 |
| DS-DI-06 | FS-DI-06 | Archival manifest (CI-26 + Veeam SHA-256) | IQ-BAK-01 |
| DS-INT-01 | FS-INT-01 | DataShare 5 poll (CI-65) | OQ-INT-01 |
| DS-INT-02 | FS-INT-02 | Push gate APPROVED (CI-66, CI-68) | OQ-INT-02 |
| DS-INT-03 | FS-INT-03 | Payload schema (CI-67) | OQ-INT-03 |
| DS-INT-04 | FS-INT-04 | SST-valid pre-push (CI-66) | OQ-INT-04 |
| DS-BAK-01 | FS-BAK-01, FS-XSYS-BAK-01 | Veeam daily + S3 + LTO (CI-69) | IQ-BAK-01 |
| DS-BAK-02 | FS-BAK-02 | Quarterly restore drill (CI-79) | IQ-BAK-02 |
| DS-BAK-03 | FS-BAK-03 | RTO 8 h / RPO 24 h verified (CI-79) | IQ-BAK-02 |
| DS-PERF-01 | FS-PERF-01 | PQ 30-injection (CI-71) | PQ-PERF-01 |
| DS-PERF-02 | FS-PERF-02 | UI P95 ≤ 3 s (PQ) | OQ-PERF-02 |
| DS-SEC-01 | FS-SEC-01 | LDAPS bind + CyberArk break-glass (CI-82, CI-83) | IQ-PAM-01 |
| DS-SEC-02 | FS-SEC-02 | GPO USB block (CI-07) | IQ-GPO-04 |
| DS-TRN-01 | FS-TRN-01 | LMS curriculum gate (CI-76) | IQ-LMS-01 |
| DS-PR-01 | FS-PR-01 | Periodic-review template (CI-77) | OQ-PR-01 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 | LDAPS + Conditional Access + CyberArk + Splunk (§ 7.1, CI-83) | IQ-AD-03 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 | Veeam T3 + S3 Object Lock + LTO-9 (CI-69) | IQ-BAK-01 |

## Appendix B — Design-level Risk Register

| ID | Risk | Likelihood | Impact | Mitigation reference | Design surface |
|---|---|---|---|---|---|
| DR-01 | SST Pre-Flight Plugin (§ 8.1) silently fails open on plugin exception → expired USP RS used in SST | Low | Critical | Plugin authored with default-BLOCK on exception; OQ-REA-02 negative-path test injects exception | § 8.1, CI-41 |
| DR-02 | SST Scheduler Plugin (§ 8.2) drift on Windows time-zone change → SST shown as not-overdue when it is | Low | High | Scheduler reads UTC; OQ-SST-02 tests time-zone transition | § 8.2, CI-31 |
| DR-03 | Authority Set ↔ AD-group rename drift | Low | Critical | Quarterly access review + Authority Set export reconciled with AD | CI-15..21 |
| DR-04 | Compendial limit (CI-55) per-method override granted on unapproved method via Method-Owner script | Low | High | Method-state machine prevents override on non-APPROVED methods; OQ-CMP-01 negative path | CI-55 |
| DR-05 | UV-lamp 30-day warning (CI-50) suppressed by Sievers SCN update default-toggle | Low | Critical | Post-SCN delta check + post-upgrade IQ delta-check; FS-AIQ-04 PQ re-test on SCN | CI-50, CI-81 |
| DR-06 | Reagent Custodian role (CI-19) re-purposed to also analyse — SoD constraint (CI-22) bypassed via group nesting | Low | Critical | Quarterly access review checks AD group nesting; OQ-ROLE-SOD includes nested-group test | CI-19, CI-22 |
| DR-07 | Limit-band evaluator (CI-60) thresholds drift from per-method `compendium` definition | Low | High | Method-promotion validator pins thresholds; periodic review verifies | CI-60, CI-55 |
| DR-08 | DataShare 5 mTLS cert (CI-68) expiry blocks LIMS push silently | Low | High | 30-d pre-expiry pager alert + auto-rotation | CI-68 |
| DR-09 | RE trend dashboard (CI-34) drift not noticed when SST drift is within 85-115% but trending toward limit | Medium | High | Early-warning bands 90/110% (CI-34); monthly review surfaces trend | CI-34 |
| DR-10 | OOS → LIMS HOLD propagation (CI-64) blocked when LIMS down → water-system released without HOLD | Low | Critical | DataPro2 local HOLD state retained; pre-release LIMS-availability check at QC sign-off | CI-64 |
| DR-11 | Reactor + ICR replacement log (CI-53) misses a hardware swap done by Sievers field service without site-side entry | Low | High | Sievers FS service ticket cross-reference required; site-side log entry mandated by SOP | CI-53 |
| DR-12 | Membrane CO₂ detector replacement (CI-54) cadence slips past Sievers spec → false-high readings | Low | High | CI-54 schedule monitored; SOP includes override eSign requirement | CI-54 |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
