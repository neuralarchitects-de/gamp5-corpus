---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "SOL-FS-DISSO-001 v1.2 (parent FS)"
  - "SOL-URS-DISSO-001 v1.2 (parent URS — informational)"
  - "GAMP 5 (2nd ed.) Cat 4 — Configuration Specification conventions"
  - "21 CFR Part 11; EU GMP Annex 11; USP <711>; USP <724>; USP <1058>; USP <1092>; Ph. Eur. 2.9.3"
  - "Distek DissoTrack 5 System Administrator Guide (rev E)"
parent_fs:
  document_number: SOL-FS-DISSO-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Solenne_Pharma_Dissolution_FS_v1.3.md
parent_urs:
  document_number: SOL-URS-DISSO-001
  version: 1.2
  file: ../../../URS/_generated/final/Dissolution_Apparatus_Computer_System__Solenne_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Dissolution Apparatus Computer System — Distek Evolution 6300 + ezfill 5300 + DissoTrack 5

**Document Number:** SOL-DS-DISSO-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** SOL-FS-DISSO-001 v1.2 | **Parent URS:** SOL-URS-DISSO-001 v1.2 *(informational)*
**Site:** Solenne Pharma (fictional)
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Distek DissoTrack 5 + Evolution 6300 + ezfill 5300** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; USP <711>; USP <724>; USP <1058>; USP <1092>; Ph. Eur. 2.9.3; Ph. Eur. 2.9.4; ICH Q4B Annex 7; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Solid Dosage) | _____________ | _____________ | _____ |
| Reviewer (Dissolution SME) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Approver (System Owner — Head of QC) | _____________ | _____________ | _____ |
| Approver (Process Owner — Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T2 from parent URS+FS pair (SOL-URS-DISSO-001 / SOL-FS-DISSO-001 v1.2). DS covers 90/90 FS-IDs. No FS-IDs deferred. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

DS-specific terms only.

| Term | Definition |
|---|---|
| DissoTrack Method | Stored measurement procedure (apparatus, RPM, temperature, media, sampling time-points, acceptance). |
| TruAlign | Distek mechanical-qualification fixture for paddle / basket centering + wobble + vertical-distance measurement. |
| CPT | Chemical Performance Test using USP Prednisone Tablets RS. |
| MQ | Mechanical Qualification per USP <711> + USP <1092>. |
| `.dtr` | DissoTrack raw run file. |
| GxP Profile | DissoTrack instrument-level setting set marking the bath as regulated-mode. |

## 1. Purpose

This DS specifies the technical Distek Evolution 6300 / ezfill 5300 / DissoTrack 5 configuration values, mechanical-qualification workflow design, CPT workflow, and integration design that implement the functional behaviour defined in `SOL-FS-DISSO-001` v1.2.

## 2. Scope

In scope: DissoTrack 5 application configuration; bath + ezfill instrument settings; MQ workflow; CPT workflow; vessel / paddle / basket register; media + reagent register; UV-Vis ingest binding; LIMS connector; AD + SIEM + backup integration; site-deployed MQ-data import script. Out of scope: Distek source-code internals; UV-Vis SDLC (separate validation per its own DS); LIMS sample-lifecycle.

## 3. Architectural Overview

### 3.1 Logical View

```
                  ┌───────────────────────────┐
                  │  AD (solenne.local) · NTP │
                  └─────────────┬─────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────┐
│  DissoTrack 5 Workstation `sol-disso-ws-01`                  │
│  Win 11 Pro 23H2 · DissoTrack 5.4.2                          │
│  Project Policy = SOL_DISSO_PART11                            │
│  Project Storage: \\sol-gmp-fs01\disso-projects               │
└─────┬─────────────┬───────────────┬───────────────┬──────────┘
      │             │               │               │
      ▼             ▼               ▼               ▼
┌──────────┐ ┌────────────┐ ┌──────────────┐ ┌──────────────────┐
│ Evolution│ │ ezfill 5300│ │ Cary 60 UV-V │ │ LabWare LIMS 8   │
│ 6300 bath│ │ media disp │ │ offline rdbk │ │ Connector 2.1    │
│ USB-3    │ │ USB-3      │ │ network share│ │ HTTPS REST (mTLS)│
└──────────┘ └────────────┘ └──────────────┘ └──────────────────┘
```

### 3.2 Deployment Topology

| Component | Host / Path | Version pin | Hardening |
|---|---|---|---|
| DissoTrack 5 application | `sol-disso-ws-01` | 5.4.2 | Win 11 Pro 23H2 + GPO `SOL-LAB-WS-23H2` |
| Evolution 6300 firmware | Bench bath | FW 1.18.3 | GxP Profile ON; tamper-evident USB |
| ezfill 5300 firmware | Bench dispenser | FW 1.04.2 | GxP Profile ON |
| Project store | `\\sol-gmp-fs01\disso-projects` | NTFS ACL | AD-group bound; local C: blocked |
| Audit trail DB | DissoTrack embedded MSSQL Express (vendor) | per build | append-only DB trigger |
| Qualification archive | `\\sol-gmp-fs01\disso-qual` | WORM | 25 y retention |

## 4. Configuration Specification

`D = vendor default`; `C = site custom`.

### 4.1 Hardware + Platform Configuration

| CI-ID | Configuration Item (vendor-named) | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-HW-01 | Workstation reservation | `sol-disso-ws-01` reserved for DissoTrack only | C | FS-HW-01 | IQ-HW-01 |
| DS-HW-02 | Workstation hardware spec | HP Z2 Mini G9 · 16 GB · 1 TB SSD · 2× USB-3 ports for bath + ezfill | D | FS-HW-02 vendor spec compliance | IQ-HW-02 |
| DS-HW-03 | UPS sizing | APC SMT1500; runtime ≥ 30 min at observed load; PowerChute graceful at 20% | D | FS-HW-03 | IQ-UPS-01 |
| DS-HW-04 | TruAlign-fixture-based MQ schedule | execute at install + post-maintenance; results captured to § FS-MQ-* | C | FS-HW-04 | IQ-MQ-01 |
| DS-HW-05 | Bath-probe calibration cadence | calibration interval per Site SOP `SOL-SOP-PROBE-CAL`; NIST-traceable certs archived | C | FS-HW-05 | IQ-PROBE-01 |
| DS-HW-06 | Vessel / paddle / basket register schema | `id, type, dim_measurements, qual_date, qual_evidence_path` integrated with DissoTrack at run binding | C | FS-HW-06 | OQ-VES-01 |
| DS-HW-07 | Bath-level + degas-mode alarm wiring | level sensor + degas-mode flag wired into DissoTrack runtime; alarm at out-of-level | C | FS-HW-07 | OQ-BATH-01 |
| DS-SW-01 | OS + domain bind | Win 11 Pro 23H2 joined to `solenne.local`; GPO `SOL-LAB-WS-23H2` | C | FS-SW-01 | IQ-SW-01 |
| DS-SW-02 | DissoTrack install record | Installed by Distek engineer; install record `SOL-IR-DISSO-001` retained | C | FS-SW-02 | IQ-SW-02 |
| DS-SW-03 | Project storage ACL | NTFS: `SOL-DISSO-ANALYST` R; `SOL-DISSO-METHOD-OWNER` RWX; local C: blocked | C | FS-SW-03 | IQ-ACL-01 |
| DS-SW-04 | NTP peer + skew | `ntp.solenne.local`; w32time MaxPosPhaseCorrection 1000 ms | C | FS-SW-04 | OQ-NTP-01 |
| DS-SW-05 | GPO screen lock | `SOL-LAB-LOCK`: lock at 10 min idle | C | FS-SW-05 | IQ-GPO-01 |
| DS-SW-06 | DissoTrack Project Policy | `SOL_DISSO_PART11` (audit_trail=mandatory; esign=mandatory; raw_data_lock=immediate) | C | FS-SW-06 | IQ-SW-03 |
| DS-SW-07 | DissoTrack SCN change-control hook | `CCR-DISSO-*` mandatory; build hash verified at partial-OQ | C | FS-SW-07 | OQ-CC-01 |

### 4.2 Compendial + AIQ + MQ + CPT Configuration

| CI-ID | Configuration Item (vendor-named) | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-CMP-01 | Apparatus enumeration | `{1,2,3,4,5,6,7}`; method-defined apparatus + qualified vessel-kit bound at run start | C | FS-CMP-01 | OQ-APP-01 |
| DS-CMP-02 | Per-vessel temperature sampling + alarm | 1 Hz sampling; out-of-band `37 °C ± 0.5 °C` → alarm + report flag | C | FS-CMP-02 | OQ-TEMP-01 |
| DS-CMP-03 | RPM tachometer sampling + alarm | 1 Hz; out-of-band ±4% of set → deviation event | C | FS-CMP-03 | OQ-RPM-01 |
| DS-CMP-04 | USP <711> stage evaluator | S1 (n=6) / S2 (n=12 cumulative) / S3 (n=24 cumulative) per IR + ER acceptance tables | C | FS-CMP-04 | OQ-S123-01 |
| DS-CMP-05 | USP <724> acceptance activation | when `apparatus ∈ {5,6,7}` | C | FS-CMP-05 | OQ-S724-01 |
| DS-CMP-06 | Ph. Eur. 2.9.3 / 2.9.4 activation | `Compendium=EP` → EP control-criteria active | C | FS-CMP-06 | OQ-EP-01 |
| DS-CMP-07 | Compendium enum + rounding-rule freeze | `{USP, EP, JP, NON-COMP}`; rounding frozen at method approval | C | FS-CMP-07 | OQ-CMP-01 |
| DS-AIQ-01 | DQ document | `SOL-DQ-DISSO-001` — IR / ER / future transdermal portfolio | C | FS-AIQ-01 | DQ-REF-01 |
| DS-AIQ-02 | IQ protocol | `SOL-IQ-DISSO-001` — install, AD bind, build hash, vessel-set / paddle / basket install, probe-cal certs | C | FS-AIQ-02 | IQ-AIQ-01 |
| DS-AIQ-03 | OQ battery | rotation accuracy ±4%; temp accuracy 37 ± 0.5 °C; timer accuracy; ezfill dispense ±1%; vibration; dissolved-O₂ check | C | FS-AIQ-03 | OQ-AIQ-01 |
| DS-AIQ-04 | PQ + CPT cadence | go-live, post-mechanical-maintenance, annual; CPT included | C | FS-AIQ-04 | OQ-PQ-01 |
| DS-AIQ-05 | Partial-PQ permission rule | CPT-only after PM not affecting bath alignment | C | FS-AIQ-05 | OQ-PQP-01 |
| DS-AIQ-06 | Qualification archive | `\\sol-gmp-fs01\disso-qual` WORM 25 y | C | FS-AIQ-06 | IQ-WORM-01 |
| DS-MQ-01 | TruAlign paddle/basket centering | pass ≤ 2 mm deviation from vessel center | C | FS-MQ-01 USP <711> | OQ-MQ-01 |
| DS-MQ-02 | TruAlign wobble | pass ≤ 1.0 mm | C | FS-MQ-02 | OQ-MQ-02 |
| DS-MQ-03 | Vertical-distance measurement | `25 ± 2 mm` vessel inside bottom → paddle/basket | C | FS-MQ-03 | OQ-MQ-03 |
| DS-MQ-04 | Bath-level verification | spirit-level + DissoTrack level sensor; alarm on out-of-level | C | FS-MQ-04 | OQ-MQ-04 |
| DS-MQ-05 | Vibration measurement | accelerometer at vessel-holder plate at all operational RPM; within USP <711> limits | C | FS-MQ-05 | OQ-MQ-05 |
| DS-MQ-06 | Vessel verticality plumb-line | pass within ±0.5° per vessel | C | FS-MQ-06 | OQ-MQ-06 |
| DS-MQ-07 | MQ workflow trigger | `SOL-WF-MQ` fires automatically on cell-fluid / paddle / basket maintenance event; MQ Engineer signs | C | FS-MQ-07 | OQ-MQ-07 |
| DS-CPT-01 | CPT method config | `SOL-CPT-PRED-50`: USP Prednisone Tablets RS · Apparatus 2 @ 50 rpm · 900 mL water · sampling 30 min · n=6; acceptance per current USP CPT range | C | FS-CPT-01 | OQ-CPT-01 |
| DS-CPT-02 | CPT record schema | `op_id, ts, RS_lot, cert_expiry, mean_Q, RSD, verdict`; immutable | C | FS-CPT-02 | OQ-CPT-02 |
| DS-CPT-03 | CPT FAIL → product-run block | FAIL record-id tagged on subsequent attempts; cleared by re-PQ | C | FS-CPT-03 | OQ-CPT-03 |
| DS-CPT-04 | Quarterly CPT trend review | QC Manager + MQ Engineer joint review; OOT → MQ re-execution | C | FS-CPT-04 | OQ-CPT-04 |

### 4.3 Method + Run + Result Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-MED-01 | Media + reagent register schema | `lot, source, COA_id, receipt_date, opening_date, expiry, custodian` | C | FS-MED-01 | OQ-MED-01 |
| DS-MED-02 | Pre-flight media-expiry block | run rejects when bound media lot `expiry < today`; reason `MEDIA_EXPIRED` | C | FS-MED-02 | OQ-MED-02 |
| DS-MED-03 | Prepared-media register | `prep_date, prep_analyst, pH_verification_value, short-shelf-life expiry` | C | FS-MED-03 | OQ-MED-03 |
| DS-MED-04 | Degas-method binding | method `degas` enum `{vacuum, helium_sparge, sonication}` captured per acquisition | C | FS-MED-04 | OQ-MED-04 |
| DS-MED-05 | Waste-log gating | `SOL-LOG-WASTE-DISSO` entry mandatory before register → DISPOSED | C | FS-MED-05 | OQ-MED-05 |
| DS-METH-01 | Method-lifecycle states | `DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE` | C | FS-METH-01 | OQ-METH-01 |
| DS-METH-02 | Method-library NTFS ACL | `ERA-DISSO-ANALYST`: R; `ERA-DISSO-METHOD-OWNER`: RW | C | FS-METH-02 | IQ-METH-01 |
| DS-METH-03 | Method-change trigger fields | `apparatus, rotation, media, acceptance` → `SOL-WF-METH-REVAL` | C | FS-METH-03 | OQ-METH-02 |
| DS-RUN-01 | Pre-flight checker rules | Eval temp, RPM, ezfill priming, project_lock, CPT_state, MQ_state, media_state; block + emit blocking-reason audit | C | FS-RUN-01 | OQ-PRE-01 |
| DS-RUN-02 | Acquisition metadata schema | `sample_ids, vessel_positions, method_id+version, instrument_id, analyst_id, ts_per_timepoint, media_lot, paddle_basket_id` | C | FS-RUN-02 | OQ-RUN-02 |
| DS-RUN-03 | Per-vessel temp logging | 1 Hz throughout run; deviation events highlighted in report | C | FS-RUN-03 | OQ-RUN-03 |
| DS-RUN-04 | RFC + supervisor e-sig on sampling-time override | mandatory; report flagged | C | FS-RUN-04 | OQ-RUN-04 |
| DS-RUN-05 | Media-replacement volume capture | when method `replace_media=true`; per-timepoint volume captured | C | FS-RUN-05 | OQ-RUN-05 |
| DS-RES-01 | UV-Vis / HPLC result-ingest binding key | per-vessel × per-timepoint binding via `(run_id, vessel_pos, tp_min)` | C | FS-RES-01 | OQ-RES-01 |
| DS-RES-02 | Calculation engine config | method-defined equations; rounding from compendium-rounding lookup | C | FS-RES-02 | OQ-RES-02 |
| DS-RES-03 | Stage evaluator progression | S1 → S2 → S3 per acceptance table; per-stage outcome captured | C | FS-RES-03 | OQ-RES-03 |
| DS-RES-04 | PDF report template content | sample metadata, method, analyst/reviewer/approver, per-vessel × per-tp values, stage outcome, CPT + MQ status, ALCOA+ block, SHA-256 | C | FS-RES-04 | OQ-RES-04 |
| DS-RES-05 | OOS at S3 routing | LIMS workflow `LIMS-WF-211192`; sample-state HOLD | C | FS-RES-05 | OQ-RES-05 |

### 4.4 Audit + Part 11 + DI Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-AUD-01 | Audit event-coverage filter | methods, sequences, results, configuration, MQ events, CPT events, media register, sign-on/off = ALL | C | FS-AUD-01 | OQ-AUD-01 |
| DS-AUD-02 | DB append-only | MSSQL Express trigger `audit_no_update_delete`; vendor + DBA delete-grants revoked | C | FS-AUD-02 | OQ-AUD-02 |
| DS-AUD-03 | Audit-review cadence | per-batch (Senior Analyst); monthly (QC Manager) | C | FS-AUD-03 | OQ-AUD-03 |
| DS-AUD-04 | Archival retention | 25 y product-release-linked; 7 y default; job `SOL-JOB-ARCH-DISSO` | C | FS-AUD-04 | OQ-ARCH-01 |
| DS-PART11-01 | § 11.10(a) procedural controls | SOPs referenced from CS | C | FS-PART11-01 | OQ-P11-01 |
| DS-PART11-02 | § 11.10(d) access review | quarterly; AD-mapped roles | C | FS-PART11-02 | OQ-P11-02 |
| DS-PART11-03 | § 11.50 e-sign manifestation | `username + datetime + meaning` | C | FS-PART11-03 | OQ-P11-03 |
| DS-PART11-04 | § 11.70 record↔signature | SHA-256 cryptographic hash binding | C | FS-PART11-04 | OQ-P11-04 |
| DS-PART11-05 | § 11.100 uniqueness | AD UPN | C | FS-PART11-05 | OQ-P11-05 |
| DS-PART11-06 | § 11.200 re-auth on Approve | password re-entry mandatory | C | FS-PART11-06 | OQ-P11-06 |
| DS-PART11-07 | § 11.300 password policy | AD GPO `SOL-LAB-USERS-PWD` (12 char, complexity, 90 d, lockout=5) | C | FS-PART11-07 | OQ-P11-07 |
| DS-DI-01 | ALCOA+ Attributable | `op_id` per event | C | FS-DI-01 | OQ-DI-01 |
| DS-DI-02 | ALCOA+ Legible | PDF/A-2b export | C | FS-DI-02 | OQ-DI-02 |
| DS-DI-03 | ALCOA+ Contemporaneous | NTP-only ts | C | FS-DI-03 | OQ-DI-03 |
| DS-DI-04 | ALCOA+ Original | `.dtr` raw preserved; derived files reference parent | C | FS-DI-04 | OQ-DI-04 |
| DS-DI-05 | ALCOA+ Accurate | SST + CPT + MQ gates verified per OQ | C | FS-DI-05 | OQ-DI-05 |
| DS-DI-06 | ALCOA+ Complete | manifest verifies raw + audit + signature + method-version | C | FS-DI-06 | OQ-DI-06 |

## 5. Workflow + Business-Rule Design

### 5.1 MQ Workflow (`SOL-WF-MQ`)

Trigger conditions: cell-fluid maintenance OR paddle/basket maintenance OR vessel replacement OR bath service. Steps:

1. MQ Engineer mounts TruAlign fixture → captures centering, wobble, vertical-distance per vessel.
2. Vibration measurement at all operational RPM via accelerometer.
3. Vessel-verticality plumb-line check per vessel.
4. Bath-level + dissolved-O₂ + temperature verification.
5. Results uploaded via DS-SCR-MQIMP-01 (site script); MQ Engineer e-signs `SOL-WF-MQ-FORM-001`.
6. Triggers CPT execution (`SOL-CPT-PRED-50`) before product runs resume.

### 5.2 CPT Workflow (`SOL-WF-CPT`)

Bound to MQ workflow + annual cadence. CPT FAIL flips `CPT_state=FAIL`, tagged on every subsequent pre-flight (DS-CPT-03). Cleared only by successful re-CPT after MQ remediation.

### 5.3 Sequence Pre-Flight Workflow

Eval order:

1. `instrument_state == READY` ?
2. `CPT_state == PASS AND CPT_age < cadence` ?
3. `MQ_state == PASS` ?
4. `media_lot.expiry > today` ?
5. `method_state == EFFECTIVE` ?
6. `vessel/paddle/basket_id qualified` ?

Any FALSE → block + emit blocking-reason audit.

### 5.4 LIMS Push Business Rules

| Rule | Behaviour | FS-ID |
|---|---|---|
| `result_state == APPROVED` | required for push | FS-INT-LIMS-02 |
| `CPT_state == PASS AND MQ_state == PASS` | required for push | FS-INT-LIMS-03 |
| Reject conditions | LIMS error code `SOL-DISSO-NOT-APPROVED` | FS-INT-LIMS-02 |

## 6. Role-Permission Matrix Design

| AD Group → / Permission ↓ | ANALYST | SR-ANALYST | METHOD-OWNER | MQ-ENGINEER | QC-MGR | QA-APPROVER | SYS-ADMIN |
|---|---|---|---|---|---|---|---|
| Run dissolution acquisition | ✓ | ✓ | — | — | — | — | — |
| Approve result | — | ✓ | — | — | — | — | — |
| Edit method (DRAFT) | — | — | ✓ | — | — | — | — |
| Approve method | — | — | — | — | ✓ | — | — |
| Execute MQ | — | — | — | ✓ | — | — | — |
| Sign MQ form | — | — | — | ✓ | — | ✓ | — |
| Execute CPT | — | ✓ | — | ✓ | — | — | — |
| Approve CPT | — | — | — | — | ✓ | — | — |
| RFC on sampling-time override | — | ✓ | — | — | — | — | — |
| Override CPT FAIL → READY | — | — | — | — | — | ✓ | — |
| Edit CS / configuration | — | — | — | — | — | — | ✓ (CCR) |
| Read audit | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

Author-Approver separation: a user shall NOT simultaneously hold `SOL-DISSO-METHOD-OWNER` AND `SOL-QC-MGR` AD-group membership.

## 7. Integration Design

### 7.1 LabWare LIMS 8 Connector (FS-INT-LIMS-*)

| Aspect | Value |
|---|---|
| Endpoint (worklist GET) | `https://lims.solenne.local/api/v2/worklist?instrument=SOL-DISSO-01` |
| Endpoint (result POST) | `https://lims.solenne.local/api/v2/results` |
| Protocol | HTTPS REST + mTLS (cert `SOL-PKI-DISSO-WS01`) |
| Polling cadence | 5 min |
| Pre-push validation | `result_state == APPROVED AND CPT_state == PASS AND MQ_state == PASS` |
| Reject code | `SOL-DISSO-NOT-APPROVED` |

### 7.2 UV-Vis Ingest Integration (FS-INT-UV-01)

| Aspect | Value |
|---|---|
| Source | Agilent Cary 60 offline readback over network share `\\sol-uvvis\readback\` |
| Hash preservation | source file SHA-256 captured at ingest; no manipulation of UV-Vis raw |
| Binding key | `(run_id, vessel_pos, tp_min)` |
| Ingest audit | per file emits `UV_INGEST_*` event |

### 7.3 AD + SIEM Integration

| Aspect | Value |
|---|---|
| AD bind | LDAPS to `ldap.solenne.local:636` |
| Break-glass | `SOL-BG-DISSO` CyberArk-vaulted |
| Conditional access | `Lab-Workstation Conditional Access (MFA on interactive logon)` |
| SIEM | Splunk index `gxp-authn` + `gxp-endpoint` via syslog RFC 5424 |

### 7.4 Backup Integration

| Aspect | Value |
|---|---|
| Engine | Veeam B&R 12.1 Application-Aware with MS SQL Server VSS for DissoTrack result DB |
| Schedule | nightly `SOL-JOB-BAK-DISSO` 02:00 |
| Tier | T2 (RPO ≤ 24 h; RTO ≤ 24 BH per FS-XSYS-BAK-01) |
| Immutability | S3 Object Lock Compliance + LTO-9 monthly |
| Restore drill | quarterly per `SOL-SOP-RESTORE-TEST` |

## 8. Site-Deployed Components

### 8.1 MQ Data Import Script (`SOL-SCRIPT-MQIMP-DISSO.ps1`)

- **Language:** PowerShell 7.4 signed with `SOL-PKI-CSIGN-01`.
- **Responsibility:** Parses TruAlign CSV export, validates against `SOL-MQ-SCHEMA-001`, posts each MQ measurement to DissoTrack `/api/internal/mq-import` with idempotency key `(serial, fixture_run_ts)`.
- **Verification:** OQ-MQIMP-01.
- **Module Spec reference:** `SOL-MS-MQIMP-001`.

### 8.2 Vessel Register Reconciliation Job (`SOL-SCRIPT-VESREC-DISSO.py`)

- **Language:** Python 3.12 inside `sol-disso-vesrec-env` (cosign-signed).
- **Responsibility:** Weekly cross-check of vessel / paddle / basket register vs physical-asset CMMS pull; emits drift report to QC Manager.
- **Verification:** OQ-VESREC-01.
- **Module Spec reference:** `SOL-MS-VESREC-001`.

## 9. References

### US
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .68, .192, .194
- FDA Dissolution Testing of Immediate Release Solid Oral Dosage Forms (1997)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11

### DACH
- BfArM bekanntmachungen (informational)

### International
- USP <711>; USP <724>; USP <1058>; USP <1092>; Ph. Eur. 2.9.3; Ph. Eur. 2.9.4; ICH Q4B Annex 7; PIC/S PI 041; ISPE GAMP 5 (2nd ed., 2022)

### Vendor
- Distek Inc. — *DissoTrack 5 System Administrator Guide*, document DT5-SAG-005, revision E (synthetic placeholder)
- Distek Inc. — *Evolution 6300 Operations Reference*, v1.18 (synthetic placeholder)
- Distek Inc. — *TruAlign Mechanical Qualification Tool Procedure*, v2.3 (synthetic placeholder)

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) |
|---|---|
| DS-HW-01 | FS-HW-01 |
| DS-HW-02 | FS-HW-02 |
| DS-HW-03 | FS-HW-03 |
| DS-HW-04 | FS-HW-04 |
| DS-HW-05 | FS-HW-05 |
| DS-HW-06 | FS-HW-06 |
| DS-HW-07 | FS-HW-07 |
| DS-SW-01 | FS-SW-01 |
| DS-SW-02 | FS-SW-02 |
| DS-SW-03 | FS-SW-03 |
| DS-SW-04 | FS-SW-04 |
| DS-SW-05 | FS-SW-05 |
| DS-SW-06 | FS-SW-06 |
| DS-SW-07 | FS-SW-07 |
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
| DS-MQ-01 | FS-MQ-01 |
| DS-MQ-02 | FS-MQ-02 |
| DS-MQ-03 | FS-MQ-03 |
| DS-MQ-04 | FS-MQ-04 |
| DS-MQ-05 | FS-MQ-05 |
| DS-MQ-06 | FS-MQ-06 |
| DS-MQ-07 | FS-MQ-07 |
| DS-CPT-01 | FS-CPT-01 |
| DS-CPT-02 | FS-CPT-02 |
| DS-CPT-03 | FS-CPT-03 |
| DS-CPT-04 | FS-CPT-04 |
| DS-MED-01 | FS-MED-01 |
| DS-MED-02 | FS-MED-02 |
| DS-MED-03 | FS-MED-03 |
| DS-MED-04 | FS-MED-04 |
| DS-MED-05 | FS-MED-05 |
| DS-METH-01 | FS-METH-01 |
| DS-METH-02 | FS-METH-02 |
| DS-METH-03 | FS-METH-03 |
| DS-RUN-01 | FS-RUN-01 |
| DS-RUN-02 | FS-RUN-02 |
| DS-RUN-03 | FS-RUN-03 |
| DS-RUN-04 | FS-RUN-04 |
| DS-RUN-05 | FS-RUN-05 |
| DS-RES-01 | FS-RES-01 |
| DS-RES-02 | FS-RES-02 |
| DS-RES-03 | FS-RES-03 |
| DS-RES-04 | FS-RES-04 |
| DS-RES-05 | FS-RES-05 |
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
| DS-INT-LIMS-01 | FS-INT-LIMS-01, FS-INT-LIMS-02, FS-INT-LIMS-03 |
| DS-INT-UV-01 | FS-INT-UV-01 |
| DS-INT-AD-01 | FS-SEC-01, FS-XSYS-AD-01 |
| DS-BAK-01 | FS-BAK-01, FS-BAK-02, FS-BAK-03, FS-XSYS-BAK-01 |
| DS-PERF-01 | FS-PERF-01 |
| DS-SEC-02 | FS-SEC-02 |
| DS-TRN-01 | FS-TRN-01 |
| DS-PR-01 | FS-PR-01 |
| DS-SCR-MQIMP-01 | FS-MQ-07 |
| DS-SCR-VESREC-01 | FS-HW-06 |

## 11. Appendix B — Design-level Risk Register

| ID | Design risk | Likelihood | Impact | Mitigation in this DS |
|---|---|---|---|---|
| DR-01 | TruAlign-fixture mis-handling produces falsely-passing MQ centering measurement | Medium | High | DS-MQ-01 + DS-MQ-02 + dual-witness sign-off on MQ form (DS-MQ-07 + role matrix) |
| DR-02 | Bath probe-calibration certificate expires unnoticed | Medium | High | DS-HW-05 + DS-SCR-VESREC-01 weekly drift report extended to probe-cert tracking |
| DR-03 | DissoTrack SCN update reverts Part 11 toggle to vendor default | Medium | Critical | DS-SW-07 CCR-DISSO-* mandatory; post-install OQ partial re-verifies DS-SW-06 |
| DR-04 | MQ data-import script silently drops rows on CSV schema drift | Medium | High | DS-SCR-MQIMP-01 hard-validates against `SOL-MQ-SCHEMA-001`; OQ-MQIMP-01 schema-drift test |
| DR-05 | UV-Vis raw file integrity broken if `\\sol-uvvis\readback\` ACL drifts | Low | High | DS-INT-UV-01 SHA-256 hash preservation + ingest-time hash verify |
| DR-06 | Vibration drift (motor / mount aging) undetected between MQ executions | Medium | High | DS-MQ-05 + DS-CPT-04 quarterly trend review (early-warning) |
| DR-07 | Wrong vessel / paddle / basket bound to method at run start | Low | High | DS-HW-06 + pre-flight binding check (5.3 step 6) |
| DR-08 | mTLS cert expiry on LIMS connector silently blocks result push | Medium | High | DS-INT-LIMS-01 90 d rotation + 30 d operator alert |
| DR-09 | Audit-trail MSSQL Express corruption under sustained 1 Hz temp logging | Low | High | DS-AUD-02 append-only + nightly logical export + DS-BAK-01 hourly WAL |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
