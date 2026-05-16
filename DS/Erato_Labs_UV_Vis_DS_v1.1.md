---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "ERA-FS-UVVIS-001 v1.2 (parent FS)"
  - "ERA-URS-UVVIS-001 v1.2 (parent URS — informational)"
  - "GAMP 5 (2nd ed.) Cat 4 — Configuration Specification conventions"
  - "21 CFR Part 11; EU GMP Annex 11; USP <857>; USP <1058>; Ph. Eur. 2.2.25"
  - "Agilent Cary 3500 + UV WorkStation v3 System Administrator Guide (v3.2)"
parent_fs:
  document_number: ERA-FS-UVVIS-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Erato_Labs_UV_Vis_FS_v1.3.md
parent_urs:
  document_number: ERA-URS-UVVIS-001
  version: 1.2
  file: ../../../URS/_generated/final/UV-Vis_Spectrophotometer_Computer_System__Erato_Labs_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## UV-Vis Spectrophotometer Computer System — Agilent Cary 3500 + UV WorkStation v3

**Document Number:** ERA-DS-UVVIS-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** ERA-FS-UVVIS-001 v1.2 | **Parent URS:** ERA-URS-UVVIS-001 v1.2 *(informational)*
**Site:** Erato Labs (fictional)
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Agilent Cary 3500 + UV WorkStation v3** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; USP <857>; USP <1058>; USP <1225>; Ph. Eur. 2.2.25; ICH Q2(R2); PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Spectroscopy Lead) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Approver (System Owner — QC Manager Spectroscopy) | _____________ | _____________ | _____ |
| Approver (Process Owner — Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T2 from parent URS+FS pair (ERA-URS-UVVIS-001 / ERA-FS-UVVIS-001 v1.2). DS covers 85/85 FS-IDs. No FS-IDs deferred; no FS-IDs flagged vendor-internal. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

DS-specific terms only (URS + FS definitions inherited by reference).

| Term | Definition |
|---|---|
| CI | Configuration Item — a single parameter in the Cary 3500 / UV WorkStation v3 configuration surface that has a discrete chosen value. |
| Project Policy | UV WorkStation v3 named policy bundle attaching Part 11, audit-trail, and signature settings to one or more `.uvp` project files. |
| GxP Profile | Cary 3500 instrument-level setting set marking the chamber as regulated-mode (locks firmware-level configuration). |
| `.uvd` | Raw scan file emitted by the Cary 3500 / UV WorkStation v3 acquisition module. |
| `.uvp` | UV WorkStation v3 project file (binds method + sequence + acquired data). |

## 1. Purpose

This DS specifies the technical Cary 3500 + UV WorkStation v3 configuration values and integration design that implement the functional behaviour defined in `ERA-FS-UVVIS-001` v1.2. It is the controlling input to `ERA-IQ-UVVIS-001`, `ERA-OQ-UVVIS-001`, and `ERA-PQ-UVVIS-001` configuration-section testing, and is the authoritative baseline used by the change-control workflow `CCR-UVVIS-*`.

## 2. Scope

In scope: the named configuration values + workflow definitions + role-permission matrix + integration endpoint specifications + site-deployed components (LIMS-side adapter scripts, archival job script) for the Cary 3500 / UV WorkStation v3 deployment at Erato Labs Reykjavík. Out of scope: vendor source-code internals (Agilent SDLC owns OPUS-equivalent rendering and instrument firmware design); Cary 3500 instrument-level equipment qualification (separate DQ/IQ artefacts); LIMS sample-lifecycle internals (LabWare LIMS 8 DS owns these).

## 3. Architectural Overview

### 3.1 Logical View

```
                         ┌──────────────────────────┐
                         │  AD (erato.local)        │
                         │  LDAPS + Kerberos        │
                         │  NTP pool ntp1/ntp2      │
                         └──────────┬───────────────┘
                                    │
                                    ▼
┌──────────────────────────────────────────────────────────────┐
│  UV WorkStation v3 Workstation  (era-uvvis-ws-01)            │
│  Win 11 LTSC · UV WorkStation v3 SCN-3.2.1                   │
│  Project Policy = ERATO_QC_PART11                             │
│  Project Storage: \\era-fs01\uvvis\methods + ...\data         │
└─────────┬─────────────────────────────────────────────┬──────┘
          │                                              │
          ▼                                              ▼
┌──────────────────────────┐                ┌────────────────────────┐
│  Cary 3500 instrument    │                │  LabWare LIMS 8        │
│  USB-3 over fibre        │                │  Connector v2.4        │
│  Compact / Multicell     │                │  worklist + result push │
│  GxP Profile = ON        │                │  HTTPS REST (mTLS)      │
└──────────────────────────┘                └────────────────────────┘
```

### 3.2 Deployment Topology

| Component | Host / Path | Version pin | Hardening |
|---|---|---|---|
| UV WorkStation v3 application | `era-uvvis-ws-01` | SCN-3.2.1 | Win 11 LTSC + Erato hardening baseline `ERA-HBL-LAB-001` |
| Cary 3500 instrument firmware | Bench instrument | FW 1.42.0 | GxP Profile ON; tamper-evident USB seal |
| Project store | `\\era-fs01\uvvis\` | NTFS ACL | Inherited deny + AD-group-scoped allow |
| Audit trail DB | UV WorkStation v3 embedded SQLite (vendor-owned) | per SCN | append-only constraint per FS-AUD-02 |
| LIMS connector | UV WorkStation v3 plugin `AgilentLimsBridge` | 2.4 | mTLS cert from site PKI |
| Archive volume | `\\era-fs01\uvvis\qual` + `...\archive` | WORM | NetApp SnapLock Compliance mode |

## 4. Configuration Specification

The per-CI table below names every parameter set at deployment time. `D = vendor default`; `C = site custom (deviation from default)`.

### 4.1 Platform Configuration

| CI-ID | Configuration Item (vendor-named) | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-PLAT-01 | Network attachment — UV WorkStation host NIC binding | `vlan-lab-spec` only; corporate NIC disabled in BIOS | C | FS-PLAT-01 requires no corporate-network bind; defence-in-depth | FS-PLAT-01 | IQ-NET-01 |
| DS-PLAT-02 | Windows Firewall outbound allowlist | AD/LDAPS:636; NTP:123; LIMS:443; SIEM:514 — all others deny | C | Implements FS-PLAT-01 egress restriction | FS-PLAT-01 | IQ-FW-01 |
| DS-PLAT-03 | w32time NTP peer list | `ntp1.erato.local`, `ntp2.erato.local`; poll 64 s; MaxPosPhaseCorrection 1000 ms | C | FS-PLAT-02 skew alert binding | FS-PLAT-02 | OQ-NTP-01 |
| DS-PLAT-04 | APC PowerChute graceful-shutdown threshold | 20% remaining; runtime estimate ≥ 30 min at observed load | D | FS-PLAT-03 sizing met by APC SMT1500 vendor-default profile | FS-PLAT-03 | IQ-UPS-01 |
| DS-PLAT-05 | EMS sensor thresholds (T / RH alarm) | `T_low=14 °C`, `T_high=31 °C`, `RH_low=18%`, `RH_high=82%` | C | FS-PLAT-04 thresholds; sensor reports to facility historian PI tag `ERA.UVVIS.ENV.*` | FS-PLAT-04 | IQ-EMS-01 |
| DS-PLAT-06 | Windows Event-Log subscription to SIEM | Event IDs 4663/6416/6420 forwarded via wevtutil/winlogbeat → Splunk index `gxp-endpoint` | C | FS-PLAT-05 USB / removable-media event coverage | FS-PLAT-05 | OQ-SIEM-01 |

### 4.2 UV WorkStation v3 Application Configuration

| CI-ID | Configuration Item (vendor-named) | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-SW-01 | UV WorkStation Part 11 Module flag | `Part11Enabled=true` (vendor admin → Compliance → Enable 21 CFR Part 11) | C | FS-SW-01; enables audit trail + eSign + raw-data-lock subsystems | FS-SW-01 | IQ-SW-01 |
| DS-SW-02 | Project Policy applied to all GxP projects | `ERATO_QC_PART11` (audit_trail=mandatory; esign=mandatory; raw_data_lock=immediate) | C | FS-SW-01 + FS-SW-05 binding | FS-SW-01, FS-SW-05 | IQ-SW-02 |
| DS-SW-03 | Method-library NTFS ACL | `ERA-UVVIS-METHOD-OWNER`: RWX; `ERA-UVVIS-METHOD-APPROVER`: RX; `ERA-UVVIS-ANALYST`: R; inheritance: DENY | C | FS-SW-02; deny-inheritance prevents parent-folder permission leak | FS-SW-02 | IQ-ACL-01 |
| DS-SW-04 | SST Scheduler cadence | Daily: wavelength_accuracy + photometric + stray_light; Weekly: full battery incl. linearity | C | FS-SW-03 cadence | FS-SW-03 | OQ-SST-01 |
| DS-SW-05 | AD GPO password policy | `ERA-LAB-USERS-PWD`: min_length=12; complexity=3-of-4; max_age=90 d; lockout_threshold=5 | C | FS-SW-04 | IQ-GPO-01 | IQ-GPO-01 |
| DS-SW-06 | Change-control hook for vendor SCN updates | Workflow `CCR-UVVIS-*` mandatory before any UV WorkStation build install; CS baseline rev incremented | C | FS-SW-06 | OQ-CC-01 | OQ-CC-01 |
| DS-MTH-01 | Method-lifecycle state machine | `DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE`; configured in vendor admin → Method Workflow | C | FS-MTH-01 lifecycle binding | OQ-MTH-01 | OQ-MTH-01 |
| DS-MTH-02 | Method-approval signature role-binding | Author ∈ AD group `ERA-UVVIS-METHOD-AUTHOR`; Approver ∈ `ERA-UVVIS-METHOD-APPROVER`; same-user-block ON | C | FS-MTH-02 author-cannot-approve rule | OQ-MTH-02 | OQ-MTH-02 |
| DS-MTH-03 | Method-edit-trigger field set | `calibration_tie, ref_std_id, slit_width, lambda_target` → fires re-verification protocol selector | C | FS-MTH-03 | OQ-MTH-03 | OQ-MTH-03 |
| DS-MTH-04 | Method version-history retention | All versions retained; diff renderer enabled (vendor admin → Method → Versioning → Diff = ON) | D | FS-MTH-04 | OQ-MTH-04 | OQ-MTH-04 |
| DS-ACQ-01 | Acquisition-header mandatory fields | `sample_id, cuvette_path_length, baseline_scan_id, blank_scan_id, SST_status, SST_record_id` | C | FS-ACQ-01 binding | OQ-ACQ-01 | OQ-ACQ-01 |
| DS-ACQ-02 | Sequence pre-flight checker rules | Eval `SST_overdue OR instrument_state≠READY OR method_state≠EFFECTIVE` → block + emit blocking-reason audit | C | FS-ACQ-02 | OQ-ACQ-02 | OQ-ACQ-02 |
| DS-ACQ-03 | Per-acquisition metadata capture | `spectral_bandwidth_nm, scan_rate_nm_per_min, integration_time_s, detector_mode` | C | FS-ACQ-03 | OQ-ACQ-03 | OQ-ACQ-03 |
| DS-ACQ-04 | Baseline / 100%T correction logging | Vendor admin → Audit → BaselineEvents = `ENABLED`; emit `op_id + ts` per event | C | FS-ACQ-04 | OQ-ACQ-04 | OQ-ACQ-04 |
| DS-ACQ-05 | Bracket-reference evaluator threshold | `|Δ_pct| > 2.0%` reject on assay methods; method-configurable for non-assay | C | FS-ACQ-05 | OQ-ACQ-05 | OQ-ACQ-05 |

### 4.3 Compendial / SST / AIQ Configuration

| CI-ID | Configuration Item (vendor-named) | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-CMP-01 | Holmium-oxide OQ wavelength-accuracy peak list | 241.13, 287.15, 361.31, 451.30, 536.64, 640.49 nm; tolerance ±1 nm (UV) / ±3 nm (Vis) | C | FS-CMP-01 USP <857> | OQ-WV-01 | OQ-WV-01 |
| DS-CMP-02 | K₂Cr₂O₇ photometric-accuracy test setup | 60 mg/L in 0.005 M H₂SO₄; wavelengths 235/257/313/350 nm; tolerance ±1.0% A | C | FS-CMP-02 USP <857> + Ph. Eur. 2.2.25 | OQ-PH-01 | OQ-PH-01 |
| DS-CMP-03 | Stray-light test reagent + acceptance config | KCl 12 g/L @ 200 nm; NaI 10 g/L @ 220 nm; NaNO₂ 50 g/L @ 340 nm; max A per USP <857> spec | C | FS-CMP-03 | OQ-SL-01 | OQ-SL-01 |
| DS-CMP-04 | EP-monograph K₂Cr₂O₇ ratio-band check (Ph. Eur. 2.2.25) | `Compendium=EP` activates control-of-absorbance ratio bands; block runs on fail | C | FS-CMP-04 | OQ-EP-01 | OQ-EP-01 |
| DS-CMP-05 | Photometric-linearity standard curve config | K₂Cr₂O₇ 5-point 0–2.0 A; r²≥0.999 enforced; archived per OQ batch | C | FS-CMP-05 | OQ-LIN-01 | OQ-LIN-01 |
| DS-CMP-06 | Compendium-rounding lookup table | `USP-NF 7.20`, `Ph. Eur. 1. General Notices`, JP equivalent; frozen at method APPROVED | C | FS-CMP-06 + FS-CALC-01 | OQ-RND-01 | OQ-RND-01 |
| DS-AIQ-01 | DQ document reference | `ERA-DQ-UVVIS-001`; captures intended-use, Beer-Lambert range 0.2–2.0 A, λ working range 190–800 nm | C | FS-AIQ-01 | DQ-REF-01 | DQ-REF-01 |
| DS-AIQ-02 | IQ protocol bindings | `ERA-IQ-UVVIS-001`: physical install per Agilent SOP, AD bind, build-hash check, lamp install (D2 + tungsten halogen), optical-alignment certificate | C | FS-AIQ-02 | IQ-AIQ-01 | IQ-AIQ-01 |
| DS-AIQ-03 | OQ battery composition (USP <857>) | wavelength + repeatability(5); photometric + linearity; stray-light(3 λ); toluene-in-hexane resolution (A269/A266); noise (200/240/656 nm); drift (60 min); baseline flatness (200–800 nm) | C | FS-AIQ-03 | OQ-AIQ-01 | OQ-AIQ-01 |
| DS-AIQ-04 | PQ schedule + reminder cadence | Go-live, on major change, annual; PQ delegate auto-notified 30 d before due via Outlook calendar reminder + ServiceNow | C | FS-AIQ-04 | OQ-PQ-01 | OQ-PQ-01 |
| DS-AIQ-05 | Re-qualification matrix | D2 lamp → full PQ; tungsten-halogen lamp → full PQ; monochromator service → full PQ; planned PM (no optical-bench impact) → partial SST | C | FS-AIQ-05 | OQ-RQ-01 | OQ-RQ-01 |
| DS-AIQ-06 | Qualification-evidence WORM volume | `\\era-fs01\uvvis\qual` SnapLock Compliance mode; retention = 25 y | C | FS-AIQ-06 | IQ-WORM-01 | IQ-WORM-01 |
| DS-SST-01 | SST battery suite bindings | `SST_BATTERY_USP857`: wavelength + photometric + stray; bound `ref_std_id` mandatory | C | FS-SST-01 | OQ-SST-02 | OQ-SST-02 |
| DS-SST-02 | SST record schema (immutable) | `op_id, ts, ref_std_id, certificate_expiry, computed_value, acceptance_limits, verdict_pass_fail`; post-write lock = ON | C | FS-SST-02 | OQ-SST-03 | OQ-SST-03 |
| DS-SST-03 | SST-fail FSM transition | Instrument FSM → NOT_READY; sequence runner rejects launch; override = `ERA-UVVIS-QA-APPROVER` co-sign + RFC | C | FS-SST-03 | OQ-SST-04 | OQ-SST-04 |
| DS-SST-04 | SST trending engine config | Rolling 12-month window; early-warning band = 0.5 × USP <857> limit; alert via Site EMS dashboard | C | FS-SST-04 | OQ-SST-05 | OQ-SST-05 |
| DS-SST-05 | Monthly audit-trail review template | `ERA-AUD-REVIEW-UVVIS` with "SST trend review" section + sign-off | C | FS-SST-05 | OQ-AUD-01 | OQ-AUD-01 |
| DS-REF-01 | Reference Standard Register schema | `ref_std_id, type, source, lot, COA_id, NIST_traceability_flag, receipt_date, opening_date, expiry, custodian` | C | FS-REF-01 | OQ-REF-01 | OQ-REF-01 |
| DS-REF-02 | Pre-flight ref-expiry block rule | Pre-flight rejects sequence on `expiry < today OR ref_std_id IS NULL`; reason codes `REF_EXPIRED` / `REF_UNKNOWN` | C | FS-REF-02 | OQ-REF-02 | OQ-REF-02 |
| DS-REF-03 | Method-header ref-binding requirement | `ref_std_id` is required field for SST + bracketed assay methods | C | FS-REF-03 | OQ-REF-03 | OQ-REF-03 |
| DS-REF-04 | Disposal log gating rule | `DISPOSED` transition requires `disposal_route` + `operator` fields populated | C | FS-REF-04 | OQ-REF-04 | OQ-REF-04 |
| DS-REF-05 | In-house re-qualification workflow | `ERA-WF-REFREQ-UVVIS`; QA approval required before bind to any method | C | FS-REF-05 | OQ-REF-05 | OQ-REF-05 |
| DS-CELL-01 | Cuvette qualification thresholds | Path-length tol ±0.005 cm @ 1 cm; matched-pair |ΔA| ≤ 0.005 A at λ_method | C | FS-CELL-01 | IQ-CELL-01 | IQ-CELL-01 |
| DS-CELL-02 | Cuvette-ID capture mechanism | Barcode reader integrated; manual fallback under audit; field name `cuvette_id` mandatory | C | FS-CELL-02 | OQ-CELL-01 | OQ-CELL-01 |
| DS-CELL-03 | Carry-over verification injection | Methods with `carryover_relevant=true` auto-insert carry-over verification step; references SOP `ERA-SOP-UVVIS-CLEAN` | C | FS-CELL-03 | OQ-CELL-02 | OQ-CELL-02 |
| DS-CELL-04 | Multi-cell position mismatch check | Scanner-read position vs method-assigned → prompt + audit on mismatch | C | FS-CELL-04 | OQ-CELL-03 | OQ-CELL-03 |
| DS-CALC-01 | Rounding-rule freeze trigger | On method APPROVED transition, rounding rule from compendium-rounding lookup table is bound and frozen | C | FS-CALC-01 | OQ-CALC-01 | OQ-CALC-01 |
| DS-CALC-02 | OOS evaluator + LIMS-flag transport | `reportable_result < spec_low OR > spec_high` → flag=OOS; LIMS payload field `oos_flag=true` | C | FS-CALC-02 + § 211.192 routing | OQ-CALC-02 | OQ-CALC-02 |
| DS-CALC-03 | Significant-figures rule per method-category | assay = 4 sig fig; identification = qualitative; limit-test = 2 sig fig; enforced at report-render | C | FS-CALC-03 | OQ-CALC-03 | OQ-CALC-03 |
| DS-CALC-04 | Report-PDF template content set | raw absorbances; baseline + blank scans; SST status; ref_std_ids; calculation step-trace; intermediates; reportable result | C | FS-CALC-04 | OQ-RPT-01 | OQ-RPT-01 |
| DS-CALC-05 | Replicate-RSD evaluator config | Per-method `replicate_count` (n=3 or n=6 typical); reject when `RSD > method_limit_pct` | C | FS-CALC-05 | OQ-CALC-04 | OQ-CALC-04 |
| DS-PROC-01 | RFC dialog content + minimum length | 10-char free text + RFC category dropdown; mandatory on baseline / peak-pick / integration-boundary edits | C | FS-PROC-01 | OQ-PROC-01 | OQ-PROC-01 |
| DS-PROC-02 | Raw-data-lock dual layer | NTFS read-only on `*.uvd` after acquisition close; UV WorkStation app-layer lock = ON; deletion → DBA + QA co-sign + audit | C | FS-PROC-02 | OQ-PROC-02 | OQ-PROC-02 |
| DS-PROC-03 | Report SHA-256 hash binding | Vendor admin → Reports → Hash = SHA-256; rendered in PDF footer; verifiable on export | C | FS-PROC-03 | OQ-PROC-03 | OQ-PROC-03 |

### 4.4 Audit-Trail + 21 CFR Part 11 + Data-Integrity Configuration

| CI-ID | Configuration Item (vendor-named) | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-AUD-01 | Audit-trail event-coverage filter | Methods, sequences, results, project policy, sign-on/off, ref-std register, SST events ALL = enabled | C | FS-AUD-01 | OQ-AUD-02 | OQ-AUD-02 |
| DS-AUD-02 | Audit-trail DB append-only constraint | DB trigger `audit_trail_no_update_delete`; vendor + DBA delete-grants revoked | C | FS-AUD-02 | OQ-AUD-03 | OQ-AUD-03 |
| DS-AUD-03 | Audit-review templates + cadence | Per-batch (Senior Analyst) → `ERA-AUD-REVIEW-UVVIS-BATCH`; monthly (QC Manager) → `ERA-AUD-REVIEW-UVVIS-MONTH` | C | FS-AUD-03 | OQ-AUD-04 | OQ-AUD-04 |
| DS-AUD-04 | Archival-job retention bindings | `ERA-JOB-ARCH-UVVIS`: 25 y product-release-linked; 7 y default | C | FS-AUD-04 | OQ-ARCH-01 | OQ-ARCH-01 |
| DS-PART11-01 | § 11.10(a) procedural-controls reference set | `ERA-SOP-CC-UVVIS` + `ERA-SOP-IR-UVVIS` referenced from CS | C | FS-PART11-01 | OQ-P11-01 | OQ-P11-01 |
| DS-PART11-02 | § 11.10(b) export format set | PDF (per-result report) + CSV (raw data); both regenerable from raw with hash match | C | FS-PART11-02 | OQ-P11-02 | OQ-P11-02 |
| DS-PART11-03 | § 11.10(c) retention-protection design | Archival job writes to WORM volume; SHA-256 manifest verified on monthly integrity scan | C | FS-PART11-03 | OQ-P11-03 | OQ-P11-03 |
| DS-PART11-04 | § 11.10(d) access-review cadence | Quarterly access review per `ERA-WF-ACC-REVIEW`; AD-mapped roles per § 4 URS | C | FS-PART11-04 | OQ-P11-04 | OQ-P11-04 |
| DS-PART11-05 | § 11.50 e-sign manifestation format | Signature record carries `username + datetime(NTP) + meaning(Author/Reviewer/Approver)` | C | FS-PART11-05 | OQ-P11-05 | OQ-P11-05 |
| DS-PART11-06 | § 11.70 signature↔record linking | Cryptographic SHA-256 hash binding; export carries hash for offline verification | C | FS-PART11-06 | OQ-P11-06 | OQ-P11-06 |
| DS-PART11-07 | § 11.100 uniqueness binding | AD UPN = unique identifier; reuse / reassignment governed by `ERA-SOP-ID-LCM` | C | FS-PART11-07 | OQ-P11-07 | OQ-P11-07 |
| DS-PART11-08 | § 11.200 re-auth on Approve | Password re-entry mandatory at every Approve action; biometric / smartcard out of scope | C | FS-PART11-08 | OQ-P11-08 | OQ-P11-08 |
| DS-DI-01 | ALCOA+ Attributable capture | `op_id` captured on acquire / process / approve / RFC events | C | FS-DI-01 | OQ-DI-01 | OQ-DI-01 |
| DS-DI-02 | ALCOA+ Legible — font + export | Report renderer min font 10pt; PDF/A-2b export | C | FS-DI-02 | OQ-DI-02 | OQ-DI-02 |
| DS-DI-03 | ALCOA+ Contemporaneous timestamp | NTP-derived ts; manual ts entry prohibited (UI control disabled in GxP Profile) | C | FS-DI-03 | OQ-DI-03 | OQ-DI-03 |
| DS-DI-04 | ALCOA+ Original raw file pointer | `.uvd` raw = source-of-truth; processing emits `.proc` referencing parent `raw_id` | C | FS-DI-04 | OQ-DI-04 | OQ-DI-04 |
| DS-DI-05 | ALCOA+ Accurate gates | SST pre-flight + bracket-reference (DS-ACQ-05) gate every run | C | FS-DI-05 | OQ-DI-05 | OQ-DI-05 |
| DS-DI-06 | ALCOA+ Complete archival manifest | Manifest verifies raw + audit + signature + method-version per result | C | FS-DI-06 | OQ-DI-06 | OQ-DI-06 |

## 5. Workflow + Business-Rule Design

### 5.1 Method-Lifecycle Workflow (`ERA-WF-METHOD-UVVIS`)

States: `DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE`. Transitions:

| From | To | Role required | Signature meaning | Side-effects |
|---|---|---|---|---|
| DRAFT | REVIEW | `ERA-UVVIS-METHOD-AUTHOR` | "Author submitted for review" | Method locked from edit |
| REVIEW | APPROVED | `ERA-UVVIS-METHOD-REVIEWER` (≠ Author) | "Review approved" | Rounding rule frozen (DS-CALC-01) |
| APPROVED | EFFECTIVE | `ERA-UVVIS-METHOD-APPROVER` | "Method approved for use" | Method exposed to worklist runner; trigger fires re-verify protocol selector (DS-MTH-03) |
| EFFECTIVE | OBSOLETE | `ERA-UVVIS-METHOD-APPROVER` + QA | "Method retired" | Method removed from worklist selector; history retained |

### 5.2 Sequence Pre-Flight Workflow (`ERA-WF-PREFLIGHT-UVVIS`)

Implements DS-ACQ-02 + DS-REF-02 + DS-CELL-04. Eval order:

1. `instrument_state == READY` ?
2. `SST_state == VALID AND SST_age < cadence_limit` ?
3. `method_state == EFFECTIVE` ?
4. `ref_std_expiry > today` ?
5. `cuvette_position_match == true` ?
6. Bracket-reference within ±2% (DS-ACQ-05) ?

Any FALSE → block, emit `blocking_reason` audit record, route to Senior Analyst queue.

### 5.3 SST-Failure Override Workflow (`ERA-WF-SST-OVERRIDE-UVVIS`)

Trigger: SST FAIL but instrument required for non-product-release diagnostic. Path: Senior Analyst raises RFC → QA Approver (`ERA-UVVIS-QA-APPROVER`) co-signs → instrument FSM transitioned to `READY_DIAG_ONLY` (non-GxP). All `DIAG_ONLY` acquisitions watermarked NON-GMP in report.

### 5.4 LIMS Push Business Rules

| Rule | Behaviour | FS-ID |
|---|---|---|
| `result_state == APPROVED` | Required for push | FS-INT-LIMS-02 |
| `SST_status IN (PASS, VALID)` | Required for push | FS-INT-LIMS-03 |
| `oos_flag == true` | Allowed; LIMS carries flag to § 211.192 workflow | FS-CALC-02 |
| Reject conditions | LIMS-side error code `ERA-UVVIS-NOT-APPROVED` | FS-INT-LIMS-02 |

## 6. Role-Permission Matrix Design

| AD Group → / Permission ↓ | ANALYST | SR-ANALYST | METHOD-AUTHOR | METHOD-REVIEWER | METHOD-APPROVER | QA-APPROVER | SYS-ADMIN |
|---|---|---|---|---|---|---|---|
| Run acquisition | ✓ | ✓ | — | — | — | — | — |
| Approve result | — | ✓ | — | — | — | — | — |
| Edit method (DRAFT) | — | — | ✓ | — | — | — | — |
| Review method (DRAFT→APPROVED) | — | — | — | ✓ | — | — | — |
| Approve method (APPROVED→EFFECTIVE) | — | — | — | — | ✓ | — | — |
| Retire method (→OBSOLETE) | — | — | — | — | ✓ | ✓ | — |
| Edit configuration / CS | — | — | — | — | — | — | ✓ (via CCR) |
| RFC on baseline / peak-pick | — | ✓ | — | — | — | — | — |
| SST override sign | — | — | — | — | — | ✓ | — |
| Read audit trail | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Export audit trail | — | ✓ | — | — | — | ✓ | ✓ |
| Bind reference standard | — | ✓ | — | — | — | ✓ | — |

Approver-Author separation enforced at AD group level: a single user account shall NOT be a member of both `ERA-UVVIS-METHOD-AUTHOR` and `ERA-UVVIS-METHOD-APPROVER` simultaneously. Quarterly access review (`ERA-WF-ACC-REVIEW`) verifies separation.

## 7. Integration Design

### 7.1 LabWare LIMS 8 Connector (FS-INT-LIMS-*)

| Aspect | Value | FS-ID |
|---|---|---|
| Endpoint (worklist GET) | `https://lims.erato.local/api/v2/worklist?instrument=ERA-UVVIS-01` | FS-INT-LIMS-01 |
| Endpoint (result POST) | `https://lims.erato.local/api/v2/results` | FS-INT-LIMS-02 |
| Protocol | HTTPS REST + mTLS (site PKI cert `ERA-PKI-UVVIS-WS01`) | — |
| Polling cadence | every 5 min | FS-INT-LIMS-01 |
| Request schema | JSON `{worklist_id, items: [{sample_id, method_id, lims_id, ...}]}` | — |
| Retry policy | 3 attempts; exponential back-off 2s/8s/32s; on final fail → operator alert in UV WorkStation tray | — |
| Error-handling | LIMS-side reject codes consumed: `LIMS-SAMPLE-NOT-FOUND`, `LIMS-METHOD-MISMATCH`, `ERA-UVVIS-NOT-APPROVED` | FS-INT-LIMS-02 |
| Pre-push validation | SST_status check (FS-INT-LIMS-03) inline before POST | FS-INT-LIMS-03 |
| Audit emission | every push + every reject emits audit event `LIMS_PUSH_*` | FS-AUD-01 |

### 7.2 AD / LDAPS Integration (FS-INT-AD-01)

| Aspect | Value |
|---|---|
| Bind type | LDAPS to `ldap.erato.local:636` |
| Service account | `svc-uvvis-ldap` (rotation every 180 d via CyberArk) |
| Group scope | OU=Lab,OU=Spectroscopy,DC=erato,DC=local |
| Break-glass account | `ERA-BG-UVVIS` (CyberArk-vaulted; post-use review SOP `ERA-SOP-BG-REVIEW`) |
| MFA | Inherited from AD GPO (interactive logon) |
| Conditional access | Policy `Lab-Workstation Conditional Access (MFA on interactive logon)` per FS-XSYS-AD-01 |

### 7.3 Backup Integration (FS-BAK-* + FS-XSYS-BAK-01)

| Aspect | Value |
|---|---|
| Backup engine | Veeam B&R 12.1 — file-level capture |
| Artefacts | methods, raw `.uvd`, audit DB SQLite, ref-std register, CS files |
| Schedule | nightly `ERA-JOB-BAK-UVVIS` at 02:00 local |
| Tier | T3 (RPO ≤ 72 h; RTO ≤ 72 BH per FS-XSYS-BAK-01) |
| Immutability | S3 Object Lock Compliance mode, geo-replicated |
| Air-gap | LTO-9 monthly rotation |
| Restore drill | quarterly per `ERA-SOP-RESTORE-TEST`; QA-witnessed |

### 7.4 SIEM Forwarding (FS-PLAT-05 + FS-XSYS-AD-01)

| Aspect | Value |
|---|---|
| Forwarder | winlogbeat 8.x → Splunk HEC |
| Indices | `gxp-endpoint` (Event IDs 4663/6416/6420); `gxp-authn` (interactive logon events via AD) |
| Latency target | ≤ 5 min ingestion to Splunk |
| Transport | syslog RFC 5424 over TLS |

## 8. Site-Deployed Components

Two site-developed scripts qualify as Cat 5 sub-components inside this Cat 4 system. Each receives a mini-SDS treatment.

### 8.1 LIMS-Push Pre-Validator (`ERA-SCRIPT-LIMSPUSH-UVVIS.ps1`)

- **Language / runtime:** PowerShell 7.4 (signed by site code-signing cert `ERA-PKI-CSIGN-02`).
- **Responsibility:** Pre-push hook invoked by UV WorkStation `OnResultApproved` event; re-validates SST_status + ref_std_expiry against the audit DB before POST.
- **Interface:** invoked by vendor `AgilentLimsBridge` plugin; reads from SQLite audit DB read-replica; writes to `\\era-fs01\uvvis\logs\limspush.log`.
- **Verification:** OQ-LIMSPUSH-01 — unit + integration tests against a sandbox LIMS instance.
- **Module Specification reference:** `ERA-MS-LIMSPUSH-001` (downstream artefact).

### 8.2 Archival Manifest Generator (`ERA-SCRIPT-ARCH-UVVIS.ps1`)

- **Language / runtime:** PowerShell 7.4 (same code-signing cert as 8.1).
- **Responsibility:** Nightly job emits SHA-256 manifest of all artefacts written to `\\era-fs01\uvvis\archive\` during the previous 24h; manifest hashed and written to WORM.
- **Interface:** scheduled via Windows Task Scheduler under `ERA-SVC-ARCH`; writes manifest to `\\era-fs01\uvvis\archive\manifests\YYYY-MM-DD.sha256`.
- **Verification:** OQ-ARCH-01 — round-trip restore-and-verify against manifest.
- **Module Specification reference:** `ERA-MS-ARCH-001` (downstream artefact).

## 9. References

### US
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .68, .160, .165, .192, .194
- FDA Data Integrity and Compliance Guidance (2018)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EMA Q&A on EU GMP Annex 11

### DACH
- BfArM bekanntmachungen on computerised systems (informational)

### International
- USP <857>; USP <1058>; USP <1225>; USP <1226>; Ph. Eur. 2.2.25; ICH Q2(R2); PIC/S PI 041; ISPE GAMP 5 (2nd ed., 2022)
- NIST SP 800-53 (control reference)

### Vendor
- Agilent Technologies — *Cary 3500 + UV WorkStation v3 System Administrator Guide*, document G6860-90020, revision F (synthetic placeholder for vendor docs)
- Agilent Technologies — *Cary 3500 21 CFR Part 11 Compliance Configuration Reference*, v3.2.1

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) |
|---|---|
| DS-PLAT-01 | FS-PLAT-01 |
| DS-PLAT-02 | FS-PLAT-01 |
| DS-PLAT-03 | FS-PLAT-02 |
| DS-PLAT-04 | FS-PLAT-03 |
| DS-PLAT-05 | FS-PLAT-04 |
| DS-PLAT-06 | FS-PLAT-05 |
| DS-SW-01 | FS-SW-01 |
| DS-SW-02 | FS-SW-01, FS-SW-05 |
| DS-SW-03 | FS-SW-02 |
| DS-SW-04 | FS-SW-03 |
| DS-SW-05 | FS-SW-04 |
| DS-SW-06 | FS-SW-06 |
| DS-MTH-01 | FS-MTH-01 |
| DS-MTH-02 | FS-MTH-02 |
| DS-MTH-03 | FS-MTH-03 |
| DS-MTH-04 | FS-MTH-04 |
| DS-ACQ-01 | FS-ACQ-01 |
| DS-ACQ-02 | FS-ACQ-02 |
| DS-ACQ-03 | FS-ACQ-03 |
| DS-ACQ-04 | FS-ACQ-04 |
| DS-ACQ-05 | FS-ACQ-05 |
| DS-CMP-01 | FS-CMP-01 |
| DS-CMP-02 | FS-CMP-02 |
| DS-CMP-03 | FS-CMP-03 |
| DS-CMP-04 | FS-CMP-04 |
| DS-CMP-05 | FS-CMP-05 |
| DS-CMP-06 | FS-CMP-06 |
| DS-AIQ-01 | FS-AIQ-01 |
| DS-AIQ-02 | FS-AIQ-02 |
| DS-AIQ-03 | FS-AIQ-03 |
| DS-AIQ-04 | FS-AIQ-04 |
| DS-AIQ-05 | FS-AIQ-05 |
| DS-AIQ-06 | FS-AIQ-06 |
| DS-SST-01 | FS-SST-01 |
| DS-SST-02 | FS-SST-02 |
| DS-SST-03 | FS-SST-03 |
| DS-SST-04 | FS-SST-04 |
| DS-SST-05 | FS-SST-05 |
| DS-REF-01 | FS-REF-01 |
| DS-REF-02 | FS-REF-02 |
| DS-REF-03 | FS-REF-03 |
| DS-REF-04 | FS-REF-04 |
| DS-REF-05 | FS-REF-05 |
| DS-CELL-01 | FS-CELL-01 |
| DS-CELL-02 | FS-CELL-02 |
| DS-CELL-03 | FS-CELL-03 |
| DS-CELL-04 | FS-CELL-04 |
| DS-CALC-01 | FS-CALC-01 |
| DS-CALC-02 | FS-CALC-02 |
| DS-CALC-03 | FS-CALC-03 |
| DS-CALC-04 | FS-CALC-04 |
| DS-CALC-05 | FS-CALC-05 |
| DS-PROC-01 | FS-PROC-01 |
| DS-PROC-02 | FS-PROC-02 |
| DS-PROC-03 | FS-PROC-03 |
| DS-AUD-01 | FS-AUD-01 |
| DS-AUD-02 | FS-AUD-02 |
| DS-AUD-03 | FS-AUD-03 |
| DS-AUD-04 | FS-AUD-04 |
| DS-PART11-01 | FS-PART11-01 |
| DS-PART11-02 | FS-PART11-02 |
| DS-PART11-03 | FS-PART11-03 |
| DS-PART11-04 | FS-PART11-04 |
| DS-PART11-05 | FS-PART11-05 |
| DS-PART11-06 | FS-PART11-06 |
| DS-PART11-07 | FS-PART11-07 |
| DS-PART11-08 | FS-PART11-08 |
| DS-DI-01 | FS-DI-01 |
| DS-DI-02 | FS-DI-02 |
| DS-DI-03 | FS-DI-03 |
| DS-DI-04 | FS-DI-04 |
| DS-DI-05 | FS-DI-05 |
| DS-DI-06 | FS-DI-06 |
| DS-INT-LIMS-01 | FS-INT-LIMS-01, FS-INT-LIMS-02, FS-INT-LIMS-03 |
| DS-INT-AD-01 | FS-INT-AD-01, FS-XSYS-AD-01 |
| DS-BAK-01 | FS-BAK-01, FS-BAK-02, FS-XSYS-BAK-01 |
| DS-SIEM-01 | FS-PLAT-05 |
| DS-PERF-01 | FS-PERF-01 |
| DS-SEC-01 | FS-SEC-01 |
| DS-TRN-01 | FS-TRN-01 |
| DS-PR-01 | FS-PR-01 |
| DS-SCR-LIMSPUSH-01 | FS-INT-LIMS-03 |
| DS-SCR-ARCH-01 | FS-AUD-04, FS-PART11-03 |

## 11. Appendix B — Design-level Risk Register

| ID | Design risk | Likelihood | Impact | Mitigation in this DS |
|---|---|---|---|---|
| DR-01 | Hardening baseline drift on `era-uvvis-ws-01` re-enables corporate-NIC binding via vendor service-pack reset | Low | High | DS-PLAT-01 (BIOS-level disable) + quarterly hardening compliance scan |
| DR-02 | mTLS cert expiry on LIMS connector silently blocks result push | Medium | High | DS-INT-LIMS-01 cert rotation 90 d before expiry via `ERA-PKI-MON`; operator-tray alert at 30 d |
| DR-03 | SQLite audit DB corruption on power-loss despite UPS | Low | High | DS-PLAT-04 PowerChute + DS-AUD-04 nightly logical-export + SHA-256 manifest |
| DR-04 | Role-permission overlap: same user added to both METHOD-AUTHOR + METHOD-APPROVER through manual AD edit | Medium | High | DS-MTH-02 same-user-block + quarterly access review (DS-PART11-04) |
| DR-05 | SCN update reverts Part 11 toggle to vendor default | Medium | Critical | DS-SW-06 CCR-UVVIS-* mandatory; post-install OQ partial verifies DS-SW-01 + DS-SW-02 |
| DR-06 | Reference-standard register clock-skew vs NTP causes false-expiry pre-flight rejections | Low | Medium | DS-PLAT-03 w32time peer redundancy + DS-DI-03 NTP-only timestamps |
| DR-07 | Site-deployed PowerShell scripts (8.1, 8.2) drift from CS baseline through unmanaged hotfix | Medium | High | code-signing cert (`ERA-PKI-CSIGN-02`) verification at every run + version-pin in CS; OQ-LIMSPUSH-01 / OQ-ARCH-01 re-execution |
| DR-08 | NetApp SnapLock policy mis-configuration leaves archive WORM-bit OFF on new volume | Low | Critical | DS-AIQ-06 + DS-AUD-04 + IQ-WORM-01 pre-deployment SnapLock state verification |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
