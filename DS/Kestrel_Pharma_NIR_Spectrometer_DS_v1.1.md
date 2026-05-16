---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "KSP-FS-NIR-001 v1.2 (parent FS)"
  - "KSP-URS-NIR-001 v1.2 (parent URS — informational)"
  - "GAMP 5 (2nd ed.) Cat 4 — Configuration Specification conventions"
  - "21 CFR Part 11; EU GMP Annex 11; USP <1119>; USP <1058>; Ph. Eur. 2.2.40; EMA NIR Guideline (2014)"
  - "Bruker OPUS 8.7 System Administrator Guide (rev D)"
parent_fs:
  document_number: KSP-FS-NIR-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Kestrel_Pharma_NIR_Spectrometer_FS_v1.3.md
parent_urs:
  document_number: KSP-URS-NIR-001
  version: 1.2
  file: ../../../URS/_generated/final/NIR_Spectrometer_Computer_System__Kestrel_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## NIR Spectrometer Computer System — Bruker MPA II + OPUS 8.7

**Document Number:** KSP-DS-NIR-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** KSP-FS-NIR-001 v1.2 | **Parent URS:** KSP-URS-NIR-001 v1.2 *(informational)*
**Site:** Kestrel Pharma (fictional)
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (chemometric models are Cat 5 sub-components)
**Project Mode:** Configuration project on commercial software product **Bruker MPA II + OPUS 8.7** (GAMP 5 Category 4 — Configured Product) with embedded Cat 5 chemometric-model sub-components.
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; USP <1119>; USP <856>; USP <1058>; Ph. Eur. 2.2.40; EMA NIR Guideline (2014); ICH Q2(R2); ICH Q14; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Chemometrics Lead) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Goods Receipt) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Approver (System Owner — Head of Supply Quality) | _____________ | _____________ | _____ |
| Approver (Process Owner — Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T2 from parent URS+FS pair (KSP-URS-NIR-001 / KSP-FS-NIR-001 v1.2). DS covers 90/90 FS-IDs. Chemometric-model embedded sub-component design captured in § 8.1. No FS-IDs deferred. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

DS-specific terms only (URS + FS inherited).

| Term | Definition |
|---|---|
| OPUS Project | Bruker OPUS 8.7 project file (`.opus`) binding instrument, method, model, and acquisition data. |
| Model Card | OPUS Validation-module artefact describing a deployed PCA / PLS / SIMCA chemometric model (training set, threshold, stats). |
| `.q2` | Bruker OPUS quantitative-model file. |
| `.simca` | Umetrics-format identification-model file consumed by OPUS via SIMCA-bridge. |
| GxP Profile | OPUS instrument-level setting set marking the bench as regulated-mode. |

## 1. Purpose

This DS specifies the technical Bruker MPA II + OPUS 8.7 configuration values, chemometric-model lifecycle design, and integration design that implement the functional behaviour defined in `KSP-FS-NIR-001` v1.2. It is the controlling input to `KSP-IQ-NIR-001`, `KSP-OQ-NIR-001`, and `KSP-PQ-NIR-001` configuration-section testing.

## 2. Scope

In scope: OPUS 8.7 application configuration values + IDENT/QUANT/Validation module settings + chemometric-model registry design + Model Card schema + reference-standard register + LIMS connector + AD/SIEM integration + site-deployed model-hash verification script. Out of scope: Bruker source-code internals (Bruker SDLC owns OPUS rendering / FT-NIR firmware); sample preparation; chemometric model-development environment (separate Cat 5 DS).

## 3. Architectural Overview

### 3.1 Logical View

```
                  ┌────────────────────────────────┐
                  │  AD (kestrel.local) · NTP      │
                  └──────────────┬─────────────────┘
                                 │
                                 ▼
┌─────────────────────────────────────────────────────────────┐
│  OPUS 8.7 Workstation `kst-nir-ws-01`                       │
│  Win 11 Pro 23H2 · OPUS 8.7 build 8.7.41                    │
│  Modules: IDENT + QUANT + Validation                         │
│  Project Policy = KSP_NIR_PART11                             │
│  Project Storage: \\kst-gmp-fs01\nir-projects                │
└──────┬─────────────────┬──────────────────┬─────────────────┘
       │                 │                  │
       ▼                 ▼                  ▼
┌──────────────┐  ┌──────────────────┐  ┌───────────────────────┐
│ Bruker MPA II│  │ Chemometric Model│  │ LabWare LIMS 8        │
│ FT-NIR       │  │ Registry (.q2,   │  │ OPUS LIMS Connector 3 │
│ USB-3 over   │  │  .simca)         │  │ HTTPS REST (mTLS)     │
│ shielded     │  │ SHA-256 signed   │  │                       │
│ cable        │  │                  │  └───────────────────────┘
└──────────────┘  └──────────────────┘
```

### 3.2 Deployment Topology

| Component | Host / Path | Version pin | Hardening |
|---|---|---|---|
| OPUS 8.7 application | `kst-nir-ws-01` | build 8.7.41 | Win 11 Pro 23H2 + GPO `KSP-LAB-USERS-WS-23H2` |
| Bruker MPA II firmware | Bench instrument | FW 2.18.5 | GxP Profile ON |
| Project store | `\\kst-gmp-fs01\nir-projects` | NTFS ACL | AD-group bound; local C: blocked for GxP writes |
| Audit trail DB | OPUS embedded MSSQL Compact (vendor) | per build | append-only via DB role grant |
| Model registry | `\\kst-gmp-fs01\nir-models\` | WORM after sign | NetApp SnapLock Compliance |
| Qualification archive | `\\kst-gmp-fs01\nir-qual` | WORM | 25 y retention |

## 4. Configuration Specification

`D = vendor default`; `C = site custom`.

### 4.1 Hardware + Platform Configuration

| CI-ID | Configuration Item (vendor-named) | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-HW-01 | Workstation reservation | `kst-nir-ws-01` reserved for OPUS only; no other Bruker / vendor app installed | C | FS-HW-01 | IQ-HW-01 |
| DS-HW-02 | Workstation hardware spec | HP Z2 Mini G9; 32 GB DDR5; 1 TB NVMe; meets OPUS 8.7 min spec | D | FS-HW-02 vendor spec compliance | IQ-HW-02 |
| DS-HW-03 | UPS sizing | APC SMT1500; runtime ≥ 30 min at measured load; PowerChute graceful at 20% | D | FS-HW-03 | IQ-UPS-01 |
| DS-HW-04 | USP <1119> PQ cadence | OPUS Validation-module PQ scheduled annual + on major change | C | FS-HW-04 | OQ-PQ-01 |
| DS-HW-05 | EMS thresholds | T 14/31 °C; RH 18/82 %; alarm to facility historian | C | FS-HW-05 | IQ-EMS-01 |
| DS-HW-06 | Sampling-accessory qualification list | vial holder QAL-VIAL-01; fibre-optic probe QAL-PROBE-01; integrating sphere QAL-SPH-01 — each per Bruker SOP at install + post-service | C | FS-HW-06 | IQ-ACC-01 |
| DS-SW-01 | OS + domain bind | Win 11 Pro 23H2; joined to `kestrel.local`; GPO `KSP-LAB-USERS-WS-23H2` applied | C | FS-SW-01 | IQ-SW-01 |
| DS-SW-02 | OPUS install scope | OPUS 8.7 + IDENT + QUANT + Validation; install by Bruker engineer; install record `KSP-IR-OPUS-001` retained | C | FS-SW-02 | IQ-SW-02 |
| DS-SW-03 | Project storage ACL | `\\kst-gmp-fs01\nir-projects` NTFS: `KSP-NIR-ANALYST` R; `KSP-NIR-METHOD-OWNER` RWX; `KSP-NIR-CHEM-LEAD` RWX; local C: GxP write blocked | C | FS-SW-03 | IQ-ACL-01 |
| DS-SW-04 | NTP peer + skew alert | `ntp.kestrel.local`; poll 64 s; w32time MaxPosPhaseCorrection 1000 ms | C | FS-SW-04 | OQ-NTP-01 |
| DS-SW-05 | OPUS Project Policy | `KSP_NIR_PART11` (audit_trail=mandatory; esign=mandatory; raw_data_lock=immediate) | C | FS-SW-05 | IQ-SW-03 |
| DS-SW-06 | OPUS SCN change-control hook | `CCR-NIR-*` mandatory; post-install OQ partial verifies build hash | C | FS-SW-06 | OQ-CC-01 |

### 4.2 Compendial + AIQ + SST Configuration

| CI-ID | Configuration Item (vendor-named) | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-CMP-01 | OQ wavelength-accuracy peak list (NIST SRM 1920a polystyrene) | bands at 1689, 1726, 2152, 2261, 2353 nm; tolerance ±1 nm across 780–2500 nm | C | FS-CMP-01 USP <1119> | OQ-WV-01 |
| DS-CMP-02 | OQ photometric-noise threshold | RMS noise on 99% reflectance ceramic ≤ 30 µAU @ 1.0 A | D | FS-CMP-02 USP <1119> default | OQ-NOISE-01 |
| DS-CMP-03 | OQ photometric-linearity standards | NIST-traceable transmittance set 10/30/50/80/99 %T | C | FS-CMP-03 | OQ-LIN-01 |
| DS-CMP-04 | EP-monograph activation flag | Method header `Compendium=EP` → Ph. Eur. 2.2.40 control tests mandatory at SST | C | FS-CMP-04 | OQ-EP-01 |
| DS-CMP-05 | Method-authoring EMA-template mandatory fields | variable_selection, pre_processing, threshold_rule, reference_method_correlation | C | FS-CMP-05 EMA NIR Guideline 2014 | OQ-EMA-01 |
| DS-CMP-06 | ICH Q14 ATP binding | Quantitative methods require ATP definition + Q2(R2) validation evidence at deployment | C | FS-CMP-06 | OQ-ATP-01 |
| DS-CMP-07 | Compendium enum | `compendium ∈ {USP, EP, JP, NON-COMP}` | C | FS-CMP-07 | OQ-CMP-01 |
| DS-AIQ-01 | DQ document | `KSP-DQ-NIR-001`: intended-use, λ range 780–2500 nm, accessories, model classes, Part 11 binding | C | FS-AIQ-01 | DQ-REF-01 |
| DS-AIQ-02 | IQ protocol | `KSP-IQ-NIR-001`: install, AD bind, OPUS build hash, optical alignment, source-replacement record | C | FS-AIQ-02 | IQ-AIQ-01 |
| DS-AIQ-03 | OQ battery composition | wavelength acc + repeatability(5); photometric noise; photometric linearity; SNR; scan reproducibility; resolution | C | FS-AIQ-03 | OQ-AIQ-01 |
| DS-AIQ-04 | PQ schedule | go-live + major change + annual; 30-d advance notify | C | FS-AIQ-04 | OQ-PQ-02 |
| DS-AIQ-05 | Re-qualification matrix | source → full PQ; detector → full PQ; accessory change → full PQ; routine PM → SST partial | C | FS-AIQ-05 | OQ-RQ-01 |
| DS-AIQ-06 | Qualification-evidence archive | `\\kst-gmp-fs01\nir-qual` WORM 25 y | C | FS-AIQ-06 | IQ-WORM-01 |
| DS-SST-01 | SST scheduler cadence | daily: wavelength + noise + SNR + warm-up; weekly: full battery + linearity | C | FS-SST-01 | OQ-SST-01 |
| DS-SST-02 | SST record schema | `op_id, ts, ref_std_id, certificate_expiry, computed_value, acceptance_limit, verdict`; immutable post-write | C | FS-SST-02 | OQ-SST-02 |
| DS-SST-03 | SST-fail FSM | NOT_READY; sequence-runner block; override via `KSP-NIR-QA-APPROVER` co-sign + RFC | C | FS-SST-03 | OQ-SST-03 |
| DS-SST-04 | SST trending engine | 12-month rolling; early-warning band = 0.5 × USP <1119> limit; alert via Site EMS dashboard | C | FS-SST-04 | OQ-SST-04 |
| DS-SST-05 | Audit-trail review template | monthly review includes "SST trend review" sign-off | C | FS-SST-05 | OQ-AUD-01 |

### 4.3 Chemometric-Model Lifecycle Configuration (Cat 5 Sub-component Bindings)

| CI-ID | Configuration Item (vendor-named) | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-MODEL-01 | Model Card template (OPUS Validation) | Schema: `training_set, calibration_stats, validation_stats, threshold, pre_processing, variables, factors, limitations` | C | FS-MODEL-01 | OQ-MODEL-01 |
| DS-MODEL-02 | Model-deployment workflow | `KSP-WF-MODEL-DEPLOY` — Chemometrics Approver + QC Manager e-signatures; AD groups `KSP-NIR-CHEM-APPROVER` + `KSP-NIR-QC-MGR` | C | FS-MODEL-02 | OQ-MODEL-02 |
| DS-MODEL-03 | Model-file hash binding | SHA-256 of every `.q2` / `.simca` stored in registry; OPUS pre-acquisition hook verifies; mismatch → block run + audit | C | FS-MODEL-03 | OQ-MODEL-03 |
| DS-MODEL-04 | Retraining-trigger ruleset | Hotelling T² > threshold OR Q residual > threshold OR new supplier qualified OR rolling-monthly OOS > 1 % → fire retraining workflow + audit | C | FS-MODEL-04 | OQ-MODEL-04 |
| DS-MODEL-05 | Model-performance dashboard | false-pass rate; false-fail rate; distance-to-model statistic; residual variance — Bruker OPUS dashboard widget; quarterly review by Chemometrics Lead | C | FS-MODEL-05 | OQ-MODEL-05 |
| DS-MODEL-06 | Reference-method correlation record | NIR vs HPLC / KF correlation recorded at deployment + annual review | C | FS-MODEL-06 + EMA NIR § 2.4 | OQ-MODEL-06 |
| DS-MODEL-07 | Retired-model flag | OPUS registry sets `READ_ONLY=true`; acquisition selector excludes; record retained | C | FS-MODEL-07 | OQ-MODEL-07 |
| DS-MODEL-08 | T² + Q residual thresholds | Per-model bound at deployment; out-of-bounds → spectrum verdict = INCONCLUSIVE | C | FS-MODEL-08 | OQ-MODEL-08 |
| DS-MODEL-09 | Promotion-pipeline binding | env = {dev, val, prod}; production OPUS rejects models without `val_approved=true` registry flag | C | FS-MODEL-09 | OQ-MODEL-09 |
| DS-REF-01 | Reference Standard Register schema | `ref_std_id, type, source, lot, COA_id, NIST_traceability_flag, receipt_date, opening_date, expiry, custodian` | C | FS-REF-01 | OQ-REF-01 |
| DS-REF-02 | Pre-flight ref-expiry block | SST start rejects on `expiry < today` | C | FS-REF-02 | OQ-REF-02 |
| DS-REF-03 | SST ref-binding requirement | `ref_std_id` mandatory at SST execution | C | FS-REF-03 | OQ-REF-03 |
| DS-REF-04 | Re-qualification workflow | `KSP-WF-REFREQ-NIR` requires QA approval before bind | C | FS-REF-04 | OQ-REF-04 |
| DS-SAMP-01 | Method-accessory binding | Method header `sampling_accessory`; probe-ID query at run start → mismatch → block | C | FS-SAMP-01 | OQ-SAMP-01 |
| DS-SAMP-02 | Acquisition-record fields | `sampling_mode, vial_or_probe_id, accessory_serial` | C | FS-SAMP-02 | OQ-SAMP-02 |
| DS-SAMP-03 | Probe-condition SST check | reference-spectrum overlay vs probe-baseline; deviation > tol → block | C | FS-SAMP-03 | OQ-SAMP-03 |

### 4.4 Acquisition + Identification Configuration

| CI-ID | Configuration Item (vendor-named) | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-ACQ-01 | Barcode-binding rule | Honeywell Voyager 1452g scan binds `material_code + lot` to spectrum; scan-fail → manual entry under audit | C | FS-ACQ-01 | OQ-ACQ-01 |
| DS-ACQ-02 | Pre-flight checker rules | Eval `SST_overdue OR PQ_overdue OR model_state≠EFFECTIVE OR project_locked` → block | C | FS-ACQ-02 | OQ-ACQ-02 |
| DS-ACQ-03 | Acquisition metadata schema | `material_code, lot, model_id, model_version, instrument_id, analyst_id, sampling_mode, accessory_id, ts` | C | FS-ACQ-03 | OQ-ACQ-03 |
| DS-ID-01 | ID-result verdict enum + routing | `{PASS, FAIL, BORDERLINE, INCONCLUSIVE}`; BORDERLINE / FAIL → Senior Analyst queue | C | FS-ID-01 | OQ-ID-01 |
| DS-ID-02 | LIMS FAIL routing | LIMS interface posts FAIL flag → LIMS sample-state HOLD; material blocked from release | C | FS-ID-02 | OQ-ID-02 |
| DS-ID-03 | INCONCLUSIVE routing | T² / Q out-of-model-space → INCONCLUSIVE; routes to Chemometrics Engineer + Senior Analyst for disposition; CANNOT be reported as PASS | C | FS-ID-03 | OQ-ID-03 |

### 4.5 Audit + Part 11 + DI + Integration Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-AUD-01 | Audit event-coverage filter | spectra, methods, models, deployments, configuration, sign-on/off, ref-std register, SST events = ALL | C | FS-AUD-01 | OQ-AUD-02 |
| DS-AUD-02 | DB append-only constraint | OPUS MSSQL Compact trigger `audit_no_update_delete`; delete-grants revoked at vendor + DBA level | C | FS-AUD-02 | OQ-AUD-03 |
| DS-AUD-03 | Audit-review templates | per-session (`KSP-AUD-REVIEW-NIR-SESSION`) + monthly (`KSP-AUD-REVIEW-NIR-MONTH`) | C | FS-AUD-03 | OQ-AUD-04 |
| DS-AUD-04 | Archival-retention bindings | `KSP-JOB-ARCH-NIR` 25 y product-release-linked; 7 y default | C | FS-AUD-04 | OQ-ARCH-01 |
| DS-PART11-01 | § 11.10(a) procedural-controls reference | `KSP-SOP-CC-NIR` + `KSP-SOP-IR-NIR` | C | FS-PART11-01 | OQ-P11-01 |
| DS-PART11-02 | § 11.10(d) access review cadence | quarterly per `KSP-WF-ACC-REVIEW`; AD-mapped roles | C | FS-PART11-02 | OQ-P11-02 |
| DS-PART11-03 | § 11.50 e-sign manifestation | `username + datetime(NTP) + meaning(Author/Reviewer/Approver)` | C | FS-PART11-03 | OQ-P11-03 |
| DS-PART11-04 | § 11.70 record↔signature binding | SHA-256 cryptographic hash; export verifiable | C | FS-PART11-04 | OQ-P11-04 |
| DS-PART11-05 | § 11.100 uniqueness | AD UPN as unique identifier; lifecycle per AD SOP | C | FS-PART11-05 | OQ-P11-05 |
| DS-PART11-06 | § 11.200 re-auth on Approve | password re-entry mandatory | C | FS-PART11-06 | OQ-P11-06 |
| DS-PART11-07 | § 11.300 password policy | AD GPO `KSP-LAB-USERS-PWD` (12 char, complexity 3-of-4, 90 d, lockout=5) | C | FS-PART11-07 | OQ-P11-07 |
| DS-DI-01 | ALCOA+ Attributable | `op_id` per event | C | FS-DI-01 | OQ-DI-01 |
| DS-DI-02 | ALCOA+ Legible | report min font 10pt + PDF/A-2b export | C | FS-DI-02 | OQ-DI-02 |
| DS-DI-03 | ALCOA+ Contemporaneous | NTP-only ts; manual ts disabled in GxP Profile | C | FS-DI-03 | OQ-DI-03 |
| DS-DI-04 | ALCOA+ Original | `.0` raw = source-of-truth; `.proc` references parent `raw_id` | C | FS-DI-04 | OQ-DI-04 |
| DS-DI-05 | ALCOA+ Accurate | SST pre-flight + model-hash check gate every run | C | FS-DI-05 | OQ-DI-05 |
| DS-DI-06 | ALCOA+ Complete | archival manifest verifies raw + audit + signature + model-version | C | FS-DI-06 | OQ-DI-06 |

## 5. Workflow + Business-Rule Design

### 5.1 Chemometric-Model Deployment Workflow (`KSP-WF-MODEL-DEPLOY`)

States: `dev → val → prod`. Transitions:

| From | To | Role required | Signature meaning | Side-effects |
|---|---|---|---|---|
| dev | val | `KSP-NIR-CHEM-ENGINEER` | "Model promoted to validation" | Validation-test battery (T²/Q threshold sanity + reference-method correlation) executes |
| val | prod | `KSP-NIR-CHEM-APPROVER` + `KSP-NIR-QC-MGR` (dual sign) | "Model approved for production" | Registry `val_approved=true`; SHA-256 frozen; OPUS prod accepts |
| prod | retired | `KSP-NIR-CHEM-APPROVER` + QA | "Model retired" | `READ_ONLY=true`; selector excludes |

### 5.2 Acquisition Pre-Flight Workflow

Implements DS-ACQ-02 + DS-SAMP-01 + DS-MODEL-03 + DS-MODEL-08:

1. `instrument_state == READY` ?
2. `SST_state == VALID AND SST_age < cadence` ?
3. `PQ_state == VALID` ?
4. `model_state == EFFECTIVE AND project_unlocked` ?
5. `model_sha256 matches registry` ?
6. `sampling_accessory_id matches method header` ?

Any FALSE → block + emit `blocking_reason` audit + Senior Analyst queue.

### 5.3 Retraining-Trigger Workflow

DS-MODEL-04 wires four triggers to a single `KSP-WF-MODEL-RETRAIN` workflow with statistical-justification template + Chemometrics Lead approval before next deployment.

## 6. Role-Permission Matrix Design

| AD Group → / Permission ↓ | ANALYST | SR-ANALYST | METHOD-OWNER | CHEM-ENGINEER | CHEM-APPROVER | QC-MGR | QA-APPROVER | SYS-ADMIN |
|---|---|---|---|---|---|---|---|---|
| Run acquisition | ✓ | ✓ | — | — | — | — | — | — |
| Approve ID result | — | ✓ | — | — | — | — | — | — |
| Edit method (DRAFT) | — | — | ✓ | — | — | — | — | — |
| Approve method | — | — | — | — | — | ✓ | — | — |
| Deploy model dev→val | — | — | — | ✓ | — | — | — | — |
| Approve model val→prod | — | — | — | — | ✓ | ✓ | — | — |
| Retire model | — | — | — | — | ✓ | — | ✓ | — |
| INCONCLUSIVE disposition | — | ✓ | — | ✓ | — | — | — | — |
| SST override sign | — | — | — | — | — | — | ✓ | — |
| Edit CS / configuration | — | — | — | — | — | — | — | ✓ (CCR) |
| Read audit | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

Author-Approver separation: a user shall NOT simultaneously hold `KSP-NIR-CHEM-ENGINEER` AND `KSP-NIR-CHEM-APPROVER`. Verified quarterly per FS-PART11-02.

## 7. Integration Design

### 7.1 LabWare LIMS 8 Connector (FS-INT-LIMS-*)

| Aspect | Value |
|---|---|
| Endpoint (worklist GET) | `https://lims.kestrel.local/api/v2/worklist?instrument=KSP-NIR-01` |
| Endpoint (result POST) | `https://lims.kestrel.local/api/v2/results` |
| Protocol | HTTPS REST + mTLS (cert `KSP-PKI-NIR-WS01`) |
| Polling cadence | 5 min |
| Pre-push validation | `result_state == APPROVED AND SST_state ∈ {PASS, VALID}` |
| LIMS payload extras | `spectrum_hash, model_id, model_version, instrument_id, reviewer_id, approver_id` |
| Reject error code | `KSP-NIR-NOT-APPROVED` |
| Audit emission | per push + per reject |

### 7.2 AD + SIEM Integration

| Aspect | Value |
|---|---|
| AD bind | LDAPS to `ldap.kestrel.local:636` |
| Service account | `svc-nir-ldap` rotated 180 d via CyberArk |
| Break-glass | `KSP-BG-NIR` CyberArk-vaulted |
| MFA | per FS-XSYS-AD-01 conditional-access |
| SIEM | Splunk index `gxp-authn` via syslog RFC 5424; ≤ 5 min ingestion |

### 7.3 Backup Integration

| Aspect | Value |
|---|---|
| Engine | Veeam B&R 12.1 Application-Aware with MS SQL Server VSS for NIR result DB |
| Artefacts | spectra, methods, model registry, audit DB, ref-std register |
| Schedule | nightly `KSP-JOB-BAK-NIR` 02:00 |
| Tier | T2 (RPO ≤ 24 h; RTO ≤ 24 BH) |
| Immutability | S3 Object Lock Compliance + LTO-9 monthly air-gap |
| Restore drill | quarterly per `KSP-SOP-RESTORE-TEST` |

## 8. Site-Deployed Components

### 8.1 Model-Hash Verification Hook (`KSP-SCRIPT-MODELHASH-NIR.ps1`)

- **Language:** PowerShell 7.4, signed via site code-signing cert `KSP-PKI-CSIGN-01`.
- **Responsibility:** Invoked by OPUS `OnAcquisitionStart` event; recomputes SHA-256 of model file referenced in method header and compares against registry value; mismatch → emit `MODEL_HASH_MISMATCH` event + block.
- **Interface:** reads `\\kst-gmp-fs01\nir-models\registry.json`; writes to OPUS audit-event API.
- **Verification:** OQ-MODELHASH-01 — controlled hash-mutation test verifies block path fires.
- **Module Spec reference:** `KSP-MS-MODELHASH-001`.

### 8.2 Reference-Method Correlation Report Generator (`KSP-SCRIPT-CORREL-NIR.py`)

- **Language:** Python 3.12 inside controlled conda env `ksp-nir-correl-env`; signed via cosign.
- **Responsibility:** Annual job pulls NIR vs HPLC/KF result pairs from LIMS, computes correlation per EMA NIR Guideline § 2.4, emits PDF report archived to Vault.
- **Interface:** invoked by scheduled task `KSP-SVC-CORREL-NIR`; pulls via LIMS REST read-only credentials.
- **Verification:** OQ-CORREL-01 — synthetic dataset round-trip with known correlation.
- **Module Spec reference:** `KSP-MS-CORREL-001`.

## 9. References

### US
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .68, .84, .194
- FDA Process Analytical Technology Guidance (2004)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EMA *Guideline on the use of near infrared spectroscopy by the pharmaceutical industry* (2014)

### DACH
- PEI / BfArM bekanntmachungen on chemometric methods (informational)

### International
- USP <1119>; USP <856>; USP <1058>; USP <1225>; Ph. Eur. 2.2.40; ICH Q2(R2); ICH Q14; ICH Q8(R2); PIC/S PI 041; ISPE GAMP 5 (2nd ed., 2022)
- ASTM E1655 (multivariate quantitative analysis)

### Vendor
- Bruker Optics — *OPUS 8.7 System Administrator Guide*, document M5300, revision D (synthetic placeholder)
- Bruker Optics — *MPA II FT-NIR Spectrometer Reference Manual*, v2.18 (synthetic placeholder)
- Bruker Optics — *OPUS Validation Module — 21 CFR Part 11 Configuration Reference*, v8.7

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) |
|---|---|
| DS-HW-01 | FS-HW-01 |
| DS-HW-02 | FS-HW-02 |
| DS-HW-03 | FS-HW-03 |
| DS-HW-04 | FS-HW-04 |
| DS-HW-05 | FS-HW-05 |
| DS-HW-06 | FS-HW-06 |
| DS-SW-01 | FS-SW-01 |
| DS-SW-02 | FS-SW-02 |
| DS-SW-03 | FS-SW-03 |
| DS-SW-04 | FS-SW-04 |
| DS-SW-05 | FS-SW-05 |
| DS-SW-06 | FS-SW-06 |
| DS-CMP-01 | FS-CMP-01 |
| DS-CMP-02 | FS-CMP-02 |
| DS-CMP-03 | FS-CMP-03 |
| DS-CMP-04 | FS-CMP-04 |
| DS-CMP-05 | FS-CMP-05 |
| DS-CMP-06 | FS-CMP-06 |
| DS-CMP-07 | FS-CMP-07 |
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
| DS-MODEL-01 | FS-MODEL-01 |
| DS-MODEL-02 | FS-MODEL-02 |
| DS-MODEL-03 | FS-MODEL-03 |
| DS-MODEL-04 | FS-MODEL-04 |
| DS-MODEL-05 | FS-MODEL-05 |
| DS-MODEL-06 | FS-MODEL-06 |
| DS-MODEL-07 | FS-MODEL-07 |
| DS-MODEL-08 | FS-MODEL-08 |
| DS-MODEL-09 | FS-MODEL-09 |
| DS-REF-01 | FS-REF-01 |
| DS-REF-02 | FS-REF-02 |
| DS-REF-03 | FS-REF-03 |
| DS-REF-04 | FS-REF-04 |
| DS-SAMP-01 | FS-SAMP-01 |
| DS-SAMP-02 | FS-SAMP-02 |
| DS-SAMP-03 | FS-SAMP-03 |
| DS-ACQ-01 | FS-ACQ-01 |
| DS-ACQ-02 | FS-ACQ-02 |
| DS-ACQ-03 | FS-ACQ-03 |
| DS-ID-01 | FS-ID-01 |
| DS-ID-02 | FS-ID-02 |
| DS-ID-03 | FS-ID-03 |
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
| DS-DI-01 | FS-DI-01 |
| DS-DI-02 | FS-DI-02 |
| DS-DI-03 | FS-DI-03 |
| DS-DI-04 | FS-DI-04 |
| DS-DI-05 | FS-DI-05 |
| DS-DI-06 | FS-DI-06 |
| DS-INT-LIMS-01 | FS-INT-LIMS-01, FS-INT-LIMS-02, FS-INT-LIMS-03, FS-INT-LIMS-04 |
| DS-INT-AD-01 | FS-SEC-01, FS-XSYS-AD-01 |
| DS-BAK-01 | FS-BAK-01, FS-BAK-02, FS-XSYS-BAK-01 |
| DS-PERF-01 | FS-PERF-01 |
| DS-SEC-02 | FS-SEC-02 |
| DS-TRN-01 | FS-TRN-01 |
| DS-PR-01 | FS-PR-01 |
| DS-SCR-MODELHASH-01 | FS-MODEL-03 |
| DS-SCR-CORREL-01 | FS-MODEL-06 |

## 11. Appendix B — Design-level Risk Register

| ID | Design risk | Likelihood | Impact | Mitigation in this DS |
|---|---|---|---|---|
| DR-01 | Chemometric model deployed to prod with stale T²/Q thresholds bound at dev | Medium | Critical | DS-MODEL-08 + DS-MODEL-09 promotion-pipeline binding + dual-sign val→prod gate |
| DR-02 | OPUS SCN reverts Part 11 toggle to vendor default | Medium | Critical | DS-SW-06 CCR-NIR-* mandatory; post-install OQ partial reverifies DS-SW-05 |
| DR-03 | SHA-256 model-hash check bypassed if registry corrupted | Low | Critical | DS-SCR-MODELHASH-01 fail-closed default (block on registry read error) + nightly registry-integrity scan |
| DR-04 | Sampling-accessory probe wear silently degrades spectra without SST detecting it | Medium | High | DS-SAMP-03 probe-condition SST + DS-MODEL-08 INCONCLUSIVE routing |
| DR-05 | Retraining-trigger thresholds (T²/Q) drift over time as model-space expands | Medium | High | DS-MODEL-04 + DS-MODEL-05 quarterly Chemometrics Lead review |
| DR-06 | LIMS connector mTLS cert expiry blocks result push silently | Medium | High | DS-INT-LIMS-01 cert rotation 90 d before expiry + 30 d operator alert |
| DR-07 | INCONCLUSIVE results reported as PASS due to operator UI confusion | Low | Critical | DS-ID-03 hard route to Chemometrics Engineer + Senior Analyst; cannot be reported as PASS at UI level |
| DR-08 | Audit-trail MSSQL Compact DB corruption under sustained write load | Low | High | DS-AUD-02 append-only + nightly logical export + DS-BAK-01 hourly WAL |
| DR-09 | Reference-standard register clock-skew vs NTP causes false-expiry | Low | Medium | DS-SW-04 redundant NTP + DS-DI-03 NTP-only timestamps |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
