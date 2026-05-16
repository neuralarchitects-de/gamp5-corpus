---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (v1.0 corpus genesis per METHODOLOGY § 2B)"
seed_corpus_basis:
  - "VSP-FS-CLNV-001 v1.2 (parent FS)"
  - "VSP-URS-CLNV-001 v1.2 (parent URS — transitive)"
  - "GAMP 5 (2nd Ed., 2022) Cat 4 conventions"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200"
  - "EU GMP Annex 11; EU GMP Annex 15"
  - "ICH Q9(R1); EMA HBEL Guideline 2014"
  - "FDA Cleaning Validation Guide 1993; PIC/S PI 006-3; APIC"
parent_fs:
  document_number: VSP-FS-CLNV-001
  version: "1.2"
  file: "../../../FS_FDS/_generated/final/Vesper_BioMed_Cleaning_Validation_FS_v1.3.md"
parent_urs:
  document_number: VSP-URS-CLNV-001
  version: "1.2"
  file: "../../../URS/_generated/final/Cleaning_Validation_System__Vesper_BioMed_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Cleaning Validation System — ValGenesis CV 5.0

**Document Number:** VSP-DS-CLNV-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** VSP-FS-CLNV-001 v1.2
**Parent URS:** VSP-URS-CLNV-001 v1.2 *(informational; transitive)*
**Site:** Vesper BioMed Oy, Cleaning Validation Operations, Helsinki, Finland *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **ValGenesis CV 5.0** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; EU GMP Annex 15; ICH Q9(R1); FDA *Guide to Inspections — Validation of Cleaning Processes* (1993); EMA *Guideline on Setting Health Based Exposure Limits* (EMA/CHMP/CVMP/SWP/169430/2012); APIC Cleaning Validation Guideline; PIC/S PI 006-3; USP <1072>, <1078>; PIC/S PI 041.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Cleaning Validation Lead — SME) | _____________ | _____________ | _____ |
| Reviewer (Toxicologist — PDE / HBEL) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Approver (System Owner — Cleaning Validation Lead) | _____________ | _____________ | _____ |
| Approver (Head of Manufacturing Sciences) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial issue. Inherited Tier T2–T3 from parent URS+FS pair (FS lands at 60 FS-IDs). DS covers 60/60 FS-IDs; 0 FS-IDs flagged as vendor-internal — no site design surface. Generated as part of the DS v1.0 corpus ship per METHODOLOGY § 2B. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

DS-specific terms only — URS / FS definitions inherited by reference.

| Term | Definition |
|---|---|
| CS | Configuration Specification (this document) |
| CI | Configuration Item — one configurable parameter, value, default-vs-custom flag, justification |
| MAC engine | The ValGenesis CV 5.0 MAC computation pipeline (HBEL + 10ppm + 1/1000 TDD trio) |
| HBEL register | The toxicology-controlled `tox_hbel` table feeding HBEL inputs into MAC computation |
| Worst-case selector | The `select_worst_case()` Python function bound to the ValGenesis nightly batch job |

## 1. Purpose

This Configuration Specification (CS) is the technical-design layer between `VSP-FS-CLNV-001` v1.2 and downstream configuration / IQ / OQ / PQ Protocols for the ValGenesis CV 5.0 deployment supporting cleaning-validation strategy, MAC computation, recovery + hold-time studies, cleaning-agent qualification, product changeover matrix, and inspection-readiness at Vesper BioMed Helsinki multi-product facility. The DS declares, per configuration item, the chosen value, default-vs-custom flag, FS-ID(s) traced, and planned verification. Vendor source-code internals (ValGenesis CV 5.0 platform code) are not redrawn here — those remain under ValGenesis SDLC.

## 2. Scope

### In scope

- ValGenesis CV 5.0 server on Linux + PostgreSQL 16.
- Equipment master + product master + worst-case selector configuration.
- MAC engine — HBEL + 10 ppm + 1/1000 TDD trio criteria; per-API hazard-class flagging.
- Sample plan (swab / rinse / visual) workflow + mobile data-capture.
- Recovery study lifecycle (DRAFT → APPROVED with 3-y re-verification).
- Hold-time studies (dirty + clean) with 5-y re-verification.
- Cleaning agent qualification (alkaline / acidic / neutral / oxidizer / surfactant).
- Product changeover matrix with PAS-X MES integration.
- Inspection-readiness dashboard.
- Audit-trail bindings, 21 CFR Part 11 controls.
- Integration endpoints: LabWare LIMS 8 (residue results), Werum PAS-X (changeover scheduling), MasterControl eQMS (deviations + CAPAs), Veeva Vault QualityDocs (controlled SOPs + reports), AD / Vault.

### Out of scope

- Physical cleaning equipment / CIP / SIP skids (separate URS).
- Analytical laboratory instruments (separate URSs).
- HBEL toxicology source data authorship (managed by toxicology / regulatory; the `tox_hbel` register is the integration point).

## 3. Architectural Overview

### 3.1 Logical view

```
   ┌────────────────────────────────────────────────────────┐
   │                AD + MFA (LDAPS)                         │
   └─────────────────────┬──────────────────────────────────┘
                         │
   ┌─────────────────────▼──────────────────────────────────┐
   │             ValGenesis CV 5.0                           │
   │  Equipment MD │ Product MD │ Worst-Case │ MAC Engine     │
   │  Recovery │ Hold-Time │ Cleaning-Agent │ Changeover      │
   │  Sample Plan │ Verification │ Report │ Inspection Dash    │
   └────┬──────────┬────────────┬──────────────┬─────────────┘
        │          │            │              │
        ▼          ▼            ▼              ▼
   LabWare       Vault       PAS-X        MasterControl
   LIMS 8     QualityDocs    MES           eQMS
   (residue   (SOPs/reports) (schedule)   (deviations + CAPAs)
    results)
```

### 3.2 Equipment-train asset structure (text diagram)

```
Cleaning Validation Scope — Vesper BioMed Helsinki
├── Equipment Train T-API-1 (small-molecule API, dedicated)
│   ├── Reactor R-101 (SS-316L, 500 L)
│   ├── Filter F-101 (PTFE)
│   └── Dryer D-101 (SS-316L)
├── Equipment Train T-API-2 (multi-product, HPAPI-eligible)
│   ├── Reactor R-201 (Hastelloy C-22, 1000 L)
│   ├── Centrifuge C-201 (SS-316L)
│   └── Vacuum Dryer VD-201 (SS-316L)
├── Equipment Train T-OSD (oral solid dosage, multi-product)
│   ├── Granulator G-301
│   ├── Tablet Press TP-301
│   └── Coater CT-301
└── Equipment Train T-PARENT (sterile parenteral, dedicated)
    ├── Compounding Tank CT-401 (SS-316L)
    └── Filling Skid FS-401 (SS-316L + PTFE)

Sampling locations per train: worst-case identification per § 5.1 workflow.
```

## 4. Configuration Specification

### 4.1 Worst-Case Matrix and Equipment Grouping

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CLNV-01 | Equipment master schema | `cv_equipment` table: surface_area_cm², materials (SS-316L, EPDM, PTFE, Hastelloy C-22), complexity_score, dedicated_flag, CIP_SIP_flag; populated from site CMMS feed | Custom | FS-MX-01. | FS-MX-01 | OQ-EQUIP-MD-01 |
| DS-CLNV-02 | Product master HBEL linkage | `cv_product` table references HBEL / ADE / PDE via foreign key to toxicology register `tox_hbel`; direct edit of HBEL fields denied to CV roles | Custom | FS-MX-02; toxicology gate prevents drift. | FS-MX-02 | OQ-HBEL-GATE-01 |
| DS-CLNV-03 | Worst-case selector | Deterministic Python function `select_worst_case(group_id)`; nightly + on-demand runs; outputs to `cv_worstcase_history` | Custom | FS-MX-03. | FS-MX-03 | OQ-WORST-CASE-01 |
| DS-CLNV-04 | Equipment-group definition form | Mandatory justification text-field (similar geometry, contact materials, cleaning method); group-level worst-case via DS-CLNV-03 | Custom | FS-MX-04. | FS-MX-04 | OQ-EQUIP-GROUP-01 |
| DS-CLNV-05 | Re-evaluation triggers | CMMS equipment-change webhook + product-introduction workflow both invoke selector job | Custom | FS-MX-05. | FS-MX-05 | OQ-REEVAL-TRIGGER-01 |

### 4.2 MAC Calculation Engine

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CLNV-06 | HBEL-based MAC formula | `MAC = (HBEL × min_batch_size_next) / (max_daily_dose_next × shared_surface)` per EMA Guideline 2014 | Default (regulator) | FS-MACO-01; primary criterion. | FS-MACO-01 | OQ-MACO-HBEL-01 |
| DS-CLNV-07 | Trio criteria computation | HBEL-based + 10 ppm + 1/1000 TDD computed in parallel; most stringent selected; rationale captured in `cv_macp_decision` | Custom | FS-MACO-02 + APIC. | FS-MACO-02 | OQ-MACO-TRIO-01 |
| DS-CLNV-08 | MAC-input versioning | `cv_macp_inputs` table with `created_by, created_at, prior_version_id`; PUT on any input creates new version | Custom | FS-MACO-03. | FS-MACO-03 | OQ-MACO-VERSION-01 |
| DS-CLNV-09 | OQ edge-case test suite | Smallest-dose × largest-surface; HPAPI (HBEL < 10 µg/d); shared multi-product equipment | Custom | FS-MACO-04. | FS-MACO-04 | OQ-MACO-EDGECASE-01 |
| DS-CLNV-10 | Hazard-class force-HBEL flag | HPAPI / cytotoxic / sensitizer / hormone / β-lactam force `mac_engine.method = HBEL`; alert if 10 ppm / TDD less stringent | Custom | FS-MACO-05. | FS-MACO-05 | OQ-HAZARD-FORCE-01 |

### 4.3 Sample Plan

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CLNV-11 | Sampling-plan form | Per CV protocol; sampler captures sample_loc_id + timestamp + user via mobile data-capture; chain-of-custody locked at submission | Custom | FS-SMP-01. | FS-SMP-01 | OQ-SMP-COC-01 |
| DS-CLNV-12 | Swab-location master | Per equipment: location_id, name, surface_area_cm², worst-case_flag, rationale | Default | FS-SMP-02. | FS-SMP-02 | OQ-SWAB-LOC-01 |
| DS-CLNV-13 | Rinse-acceptance formula | `rinse_acceptance = MAC × (rinse_volume / surface_area)` | Default (regulator math) | FS-SMP-03. | FS-SMP-03 | OQ-RINSE-CALC-01 |
| DS-CLNV-14 | Visual inspection baseline | Per FDA Cleaning Validation Guide 1993; recorded before swab / rinse | Default | FS-SMP-04. | FS-SMP-04 | OQ-VISUAL-01 |

### 4.4 Recovery Study Lifecycle

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CLNV-15 | Recovery-study capture fields | (surface_material, spike_level, recovery_method, analytical_method, n_replicates ≥ 3, recovery_factor, rsd_pct ≤ 20) | Default | FS-REC-01 + FDA guide. | FS-REC-01 | OQ-RECOVERY-01 |
| DS-CLNV-16 | Recovery factor invalid threshold | `recovery_factor < 0.50` → flag INVALID; MAC engine cannot apply | Custom | FS-REC-02. | FS-REC-02 | OQ-RECOVERY-INVALID-01 |
| DS-CLNV-17 | Re-verification due-date | `approval_date + 3 y`; dashboard ageing alert | Default | FS-REC-03. | FS-REC-03 | OQ-RECOVERY-REVER-01 |
| DS-CLNV-18 | Per-surface-material enforcement | MAC-engine join enforces recovery factor by surface-material match; SS-316L recovery cannot be applied to PTFE | Custom | FS-REC-04. | FS-REC-04 | OQ-RECOVERY-SURFACE-01 |

### 4.5 Hold-Time Studies

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CLNV-19 | Dirty hold-time form | (equipment_id, last_product, hold_hours, microbial_count, chemical_residue); acceptance per worst-case soiling study | Default | FS-HT-01. | FS-HT-01 | OQ-HT-DIRTY-01 |
| DS-CLNV-20 | Clean hold-time form | (equipment_id, post-clean hours, microbial_count, endotoxin where applicable) | Default | FS-HT-02. | FS-HT-02 | OQ-HT-CLEAN-01 |
| DS-CLNV-21 | PAS-X hold-time enforcement | Production schedule pulls hold-time limits per equipment via FS-INT-MES-01; exceed creates eQMS deviation | Custom | FS-HT-03. | FS-HT-03 | OQ-HT-MES-INT-01 |
| DS-CLNV-22 | Hold-time re-verification due-date | `approval_date + 5 y`; dashboard ageing alert | Default | FS-HT-04. | FS-HT-04 | OQ-HT-REVER-01 |

### 4.6 Cleaning Agent Qualification

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CLNV-23 | Cleaning-agent master | `cv_agent` table: composition, supplier_CoA_ref, removability_study_id, residue_detection_method, residue_acceptance | Default | FS-AGT-01. | FS-AGT-01 | OQ-AGENT-MD-01 |
| DS-CLNV-24 | Cleaning-agent MAC | Computed via FS-MACO-01..02 logic using agent's HBEL or default fallback | Default | FS-AGT-02. | FS-AGT-02 | OQ-AGENT-MAC-01 |
| DS-CLNV-25 | Agent-lot CoA-discrepancy job | Raises eQMS deviation via FS-INT-EQMS-01 | Custom | FS-AGT-03. | FS-AGT-03 | OQ-AGENT-LOT-01 |

### 4.7 Product Changeover Matrix

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CLNV-26 | Changeover matrix view | (prev_product, next_product, equipment_train, mac, cleaning_proc_id, agent_qual_status, sample_plan_id, last_verify_date) | Custom | FS-CHG-01. | FS-CHG-01 | OQ-CHG-MATRIX-01 |
| DS-CLNV-27 | MES integration endpoint | `GET /cv/api/v2/changeover-allowed?prev={p1}&next={p2}&equipment={e}`; HTTP 403 with reason on unsupported pair | Custom | FS-CHG-02. | FS-CHG-02 | OQ-CHG-MES-INT-01 |
| DS-CLNV-28 | New-product workflow | CV Engineer authors rows → CV Lead approves → matrix activated | Custom | FS-CHG-03. | FS-CHG-03 | OQ-NEW-PRODUCT-01 |
| DS-CLNV-29 | Matrix PDF export | `cv_inspection_changeover_binder.pdf` includes full matrix + per-pair details | Custom | FS-CHG-04. | FS-CHG-04 | OQ-CHG-EXPORT-01 |

### 4.8 Verification, Reporting

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CLNV-30 | Results-evaluation engine | Joins LIMS residue results with MAC + recovery factor; computes pass/fail | Custom | FS-VER-01. | FS-VER-01 | OQ-VER-EVAL-01 |
| DS-CLNV-31 | OOS deviation gate | OOS auto-creates eQMS deviation; report progression blocked until investigation = CLOSED | Custom | FS-VER-02. | FS-VER-02 | OQ-OOS-GATE-01 |
| DS-CLNV-32 | Trending engine | Per equipment / product-pair / agent; OOT rules configurable per protocol; firing triggers investigation | Custom | FS-VER-03. | FS-VER-03 | OQ-TREND-CLNV-01 |
| DS-CLNV-33 | CV report PDF content | Scope, equipment, MAC, recovery factors, hold-time, agent qual, sampling, results, deviations, conclusion; signed by CV Lead + QA Approver | Custom | FS-RPT-01. | FS-RPT-01 | OQ-CV-REPORT-01 |

### 4.9 Inspection-Readiness Dashboard

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CLNV-34 | Dashboard tile-grid | CV-protocol status, MAC currency, recovery-study currency, hold-time currency, agent-qual currency, changeover-matrix currency, recent OOS / OOT count, PR status | Custom | FS-DASH-01. | FS-DASH-01 | OQ-DASH-01 |
| DS-CLNV-35 | PDF export per equipment / product | `cv_inspection_binder.pdf` | Custom | FS-DASH-02. | FS-DASH-02 | OQ-DASH-EXPORT-01 |
| DS-CLNV-36 | Ageing alerts | MAC > 3 y, recovery > 3 y, hold-time > 5 y → orange / red badges | Custom | FS-DASH-03. | FS-DASH-03 | OQ-AGEING-ALERT-01 |

### 4.10 Audit Trail / 21 CFR Part 11 / DI

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CLNV-37 | Audit-event coverage | MAC inputs, recovery, hold-time, agent qual, changeover, sampling, verification, signatures | Default | FS-AUD-01. | FS-AUD-01 | OQ-AUD-COVERAGE-01 |
| DS-CLNV-38 | Append-only enforcement | DB role-grant level: app role has INSERT only on audit table; UPDATE/DELETE revoked | Custom | FS-AUD-02. | FS-AUD-02 | OQ-AUD-APPENDONLY-01 |
| DS-CLNV-39 | Monthly CV-Lead audit-trail review | Evidence template `VSP-PR-AUD-001` | Default | FS-AUD-03. | FS-AUD-03 | OQ-AUD-REVIEW-01 |
| DS-CLNV-40 | Retention | ≥ 25 y per Vault archive policy | Default | FS-AUD-04. | FS-AUD-04 | OQ-RETENTION-01 |
| DS-CLNV-41 | § 11.10(a)–(e) procedures | Validation procedure + copy-generation per § 11.10(a)–(e) | Default | FS-PART11-10. | FS-PART11-10 | OQ-PART11-10 |
| DS-CLNV-42 | § 11.50 signature manifestation | Printed name + UTC timestamp + meaning text | Default | FS-PART11-50. | FS-PART11-50 | OQ-PART11-50 |
| DS-CLNV-43 | § 11.70 signature binding | HMAC-SHA-256 over record-hash + signer-id + ts | Custom | FS-PART11-70. | FS-PART11-70 | OQ-PART11-70 |
| DS-CLNV-44 | § 11.100 uniqueness | AD uniqueness constraint | Default | FS-PART11-100. | FS-PART11-100 | OQ-PART11-100 |
| DS-CLNV-45 | § 11.200 re-auth | Password + MFA at every signing event | Default | FS-PART11-200. | FS-PART11-200 | OQ-PART11-200 |
| DS-CLNV-46 | DI-Attributable | Records attributable via AD principal | Default | FS-DI-01. | FS-DI-01 | OQ-DI-ATTRIB-01 |
| DS-CLNV-47 | DI-Original preservation | Originals preserved; corrections recorded with reason field | Default | FS-DI-04. | FS-DI-04 | OQ-DI-IMMUTABLE-01 |
| DS-CLNV-48 | DI-Accurate | MAC / verification calc accurate per OQ | Default | FS-DI-05. | FS-DI-05 | OQ-DI-ACCURATE-01 |

### 4.11 Integrations / Performance / Backup / Security / Training / PR

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CLNV-49 | LIMS REST integration | `POST /lims/api/v2/samples` + `GET /lims/api/v2/results`; idempotency key `(cv_run_id, sample_loc_id)` | Custom | FS-INT-LIMS-01. | FS-INT-LIMS-01 | OQ-INT-LIMS-01 |
| DS-CLNV-50 | MasterControl deviation push | REST deviation-create on OOS / hold-time exceedance | Default | FS-INT-EQMS-01. | FS-INT-EQMS-01 | OQ-INT-EQMS-01 |
| DS-CLNV-51 | Vault QualityDocs reference | URN refs on protocol + report records | Custom | FS-INT-VAULT-01. | FS-INT-VAULT-01 | OQ-INT-VAULT-01 |
| DS-CLNV-52 | PAS-X changeover query | Per DS-CLNV-27 | Default | FS-INT-MES-01. | FS-INT-MES-01 | OQ-CHG-MES-INT-01 |
| DS-CLNV-53 | AD authN | LDAPS + Kerberos; service accounts in Vault | Default | FS-INT-AD-01. | FS-INT-AD-01 | OQ-INT-AD-01 |
| DS-CLNV-54 | APR / PQR summary endpoint | `GET /cv/api/v2/summary?product={p}` read-only | Custom | FS-INT-APR-01. | FS-INT-APR-01 | OQ-INT-APR-01 |
| DS-CLNV-55 | MAC recompute latency SLO | ≤ 30 s on master-data change | Custom | FS-PERF-01. | FS-PERF-01 | PQ-PERF-MACO-01 |
| DS-CLNV-56 | DB backup | `pg_basebackup` + WAL nightly to object-locked S3; retention ≥ 25 y | Custom | FS-BAK-01. | FS-BAK-01 | OQ-BAK-PITR-01 |
| DS-CLNV-57 | Quarterly restore test | `VSP-RB-RESTORE-001` runbook; QA witness | Default | FS-BAK-02. | FS-BAK-02 | OQ-BAK-RESTORE-01 |
| DS-CLNV-58 | AD + MFA + quarterly access review | Per site IAM SOP | Default | FS-SEC-01. | FS-SEC-01 | OQ-SEC-ACCESS-01 |
| DS-CLNV-59 | LMS curriculum | Cornerstone `VSP-CURR-CV-Engineer-v1` | Custom | FS-TRN-01. | FS-TRN-01 | OQ-LMS-GATE-01 |
| DS-CLNV-60 | Periodic-review template | `VSP-PR-CV-YYYYMMDD`; signed by CV Lead + Head of Manufacturing Sciences + Head of QA | Custom | FS-PR-01. | FS-PR-01 | OQ-PR-RUNBOOK-01 |

## 5. Workflow + Business-Rule Design

### 5.1 Worst-case selection workflow

```
Trigger (nightly cron OR on-demand OR equipment-change webhook OR new-product workflow)
   │
   ▼
[Worst-case selector — Python function]
   │  Inputs: cv_equipment (DS-CLNV-01) + cv_product (DS-CLNV-02) + tox_hbel
   │  Algorithm (deterministic):
   │   1. Per equipment-group, list all products that share the train.
   │   2. For each (product, next-product) pair, compute trio MACs (DS-CLNV-07).
   │   3. Select the (product, next-product) pair with the SMALLEST MAC value —
   │      that pair is the worst-case for this group.
   │   4. Record decision in cv_worstcase_history with full input fingerprint
   │      (SHA-256 of all inputs at run time).
   │
   ▼
[Output: per equipment-group worst-case decision]
   │  → drives sampling-plan generation
   │  → drives MAC for verification
```

### 5.2 MAC computation trio criteria workflow

For every (residue, next-product, equipment) tuple:

1. Read HBEL from `tox_hbel` for residue.
2. Compute HBEL-based MAC via DS-CLNV-06 formula.
3. Compute 10 ppm MAC as parallel comparator.
4. Compute 1/1000 TDD MAC as parallel comparator.
5. If residue's `hazard_class` ∈ {HPAPI, cytotoxic, sensitizer, hormone, β-lactam}: force `mac_engine.method = HBEL`; if 10 ppm or 1/1000 TDD would be less stringent, alert engineer.
6. Otherwise: select most stringent value across the three criteria.
7. Capture rationale in `cv_macp_decision` table with all three computed values + selected method + selection reason.

### 5.3 OOS investigation workflow

1. LIMS analytical result arrives via DS-CLNV-49 integration; joined to CV sample record.
2. Results-evaluation engine (DS-CLNV-30) computes pass / fail vs MAC × recovery factor.
3. On fail (OOS): MasterControl deviation auto-created via DS-CLNV-50; `cv_run.report_progression = BLOCKED`.
4. Investigation conducted in eQMS; CAPA linked.
5. eQMS status webhook (FS-XINT-EQMS-02) → CLOSED unblocks `report_progression`.
6. Trending engine (DS-CLNV-32) also evaluates the OOS in rolling trend windows.

### 5.4 Product-changeover scheduling gate

PAS-X production-scheduling service queries `GET /cv/api/v2/changeover-allowed`:

- HTTP 200 + payload `{allowed: true, mac, sample_plan_id}` → schedule permitted.
- HTTP 403 + reason `unsupported_pair / expired_verification / missing_recovery_factor` → schedule blocked.
- The decision is logged in PAS-X scheduling audit-trail with timestamp + reason.

### 5.5 New-product introduction workflow

1. Toxicology authors HBEL in `tox_hbel` register (out of CV-system scope; Toxicologist role).
2. CV Engineer authors `cv_product` row referencing toxicology HBEL.
3. CV Engineer authors changeover-matrix rows for every existing product × new product × equipment train.
4. Recovery-study coverage check: for each (new-product, surface-material) combo, is there a valid recovery study? If not, recovery-study CR raised.
5. Worst-case selector re-runs to evaluate impact of new product on existing groups.
6. CV Lead reviews + approves changeover-matrix rows.
7. Matrix activated; PAS-X scheduling can now propose changeovers involving the new product.

## 6. Role-Permission Matrix Design

| Action / Role | CV Engineer | CV Lead | Toxicologist | Sampling Operator | Analyst (LIMS) | Cleaning-Agent SME | QA Approver | System Admin | Auditor |
|---|---|---|---|---|---|---|---|---|---|
| Author CV protocol + MAC inputs | C/U | — | — | — | — | — | — | — | — |
| Approve protocol + MAC | — | S | — | — | — | — | — | — | — |
| Maintain HBEL library | — | — | C/U / S | — | — | — | — | — | — |
| Execute sampling per protocol | — | — | — | C/U | — | — | — | — | — |
| Process LIMS samples | — | — | — | — | C/U | — | — | — | — |
| Author cleaning-agent qualification | — | — | — | — | — | C/U | — | — | — |
| Approve CV report (release decision) | — | — | — | — | — | — | S | — | — |
| OS / patch / AD groups | — | — | — | — | — | — | — | C/U | — |
| Read-only across data + audit trails | R | R | R | R | R | R | R | R | R |

Legend: R = read, C = create, U = update, S = sign (re-authenticated electronic signature), — = denied.

SoD denies per URS § 4:

- CV Engineer ≠ CV Lead approving same protocol.
- Sampling Operator ≠ Analyst (cannot self-process own sample).
- Cleaning-Agent SME ≠ QA Approver.

## 7. Integration Design

| IF-ID | Counterparty | Endpoint | Protocol | Direction | AuthN | Message schema | Retry / DLQ | Audit emission | FS-IDs traced |
|---|---|---|---|---|---|---|---|---|---|
| IF-LIMS-01 | LabWare LIMS 8 | `https://lims.vesper.local/lims/api/v2/samples` + `https://lims.vesper.local/lims/api/v2/results` | REST mTLS | bidirectional | mTLS + service account in Vault | JSON sample + result schemas | exponential backoff 1/2/4/8/16 s; DLQ at 5 + alarm; idempotent on (cv_run_id, sample_loc_id) | `cv_audit.LIMS_SAMPLE` / `cv_audit.LIMS_RESULT` | FS-INT-LIMS-01 |
| IF-EQMS-01 | MasterControl | `POST https://eqms.vesper.local/api/v2/deviations` | REST mTLS | outbound | mTLS + workload-identity | JSON deviation incl. idempotency `vsp-clnv-{cv_run_id}-{seq}` | exponential backoff; DLQ at 5 + alarm | `cv_audit.DEVIATION_RAISED` | FS-INT-EQMS-01, FS-XINT-EQMS-01 |
| IF-VAULT-DOC-01 | Veeva Vault QualityDocs | `https://vault.vesper.local/api/v24.1/objects/quality_docs/{id}` | REST | bidirectional | OAuth2 service account | Vault standard | exponential backoff | `cv_audit.VAULT_REF` | FS-INT-VAULT-01 |
| IF-MES-01 | PAS-X v3.2 | `https://cv.vesper.local/cv/api/v2/changeover-allowed` (CV-side endpoint queried by PAS-X) | REST mTLS | inbound query | mTLS | query `{prev, next, equipment}` → JSON allowed-decision | n/a (synchronous) | `cv_audit.CHANGEOVER_QUERY` | FS-INT-MES-01 |
| IF-AD-01 | AD | `ldaps://ad.vesper.local:636` + `kerberos://ad.vesper.local:88` | LDAPS + Kerberos | bidirectional | machine cert + Kerberos | LDAP + Kerberos standard | local-cache 24 h offline | `cv_audit.AUTHN` → Splunk | FS-INT-AD-01, FS-XSYS-AD-01 |
| IF-APR-01 | APR / PQR tool | `https://cv.vesper.local/cv/api/v2/summary` (CV-side endpoint queried by APR) | REST mTLS | inbound query | mTLS | query `{product}` → JSON summary | n/a | `cv_audit.APR_QUERY` | FS-INT-APR-01 |
| IF-CMMS-01 | Site CMMS (Maximo) | webhook `POST /cv/api/v2/equipment-change` | REST mTLS | inbound | mTLS + signed webhook | JSON equipment-change event | n/a (push from CMMS) | `cv_audit.CMMS_WEBHOOK` | FS-MX-05 |
| IF-VAULT-SEC-01 | HashiCorp Vault | `https://vault-sec.vesper.local/v1/kv/clnv/*` | HTTPS AppRole | inbound | AppRole | KV v2 | retry on rotation | vault-access audit | FS-SEC-01 |

### 7.1 OOS handover idempotency contract

`cv_audit.DEVIATION_RAISED` events use idempotency key `vsp-clnv-{cv_run_id}-{seq}` where `seq` increments per round (initial OOS = 1; re-test = 2; investigation re-open = 3, etc.). MasterControl's `/api/v2/deviations` endpoint returns the existing deviation_id on repeated POST with identical key + payload; divergent payload returns 409 + `cv_audit.DEVIATION_RETRY_CONFLICT` for manual reconciliation.

### 7.2 Status-callback handling (FS-XINT-EQMS-02)

eQMS status webhook subscribed at `https://cv.vesper.local/api/v2/webhooks/eqms-status`. On `eqms_status = CLOSED`, the corresponding `cv_run.report_progression` flips from BLOCKED → UNBLOCKED, allowing the CV report to proceed to CV Lead + QA Approver signatures.

## 8. Site-Deployed Components Design

### 8.1 Worst-case selector (`select_worst_case` Python function)

- **Type:** Site-authored Python function — hybrid Cat 4 + Cat 5 component (per METHODOLOGY § 2B.4 rule 6).
- **Mini-SDS:**
  - **Module:** `select_worst_case.py` v1.0 within ValGenesis CV 5.0 custom-extension namespace.
  - **Inputs:** Read `cv_equipment`, `cv_product`, `tox_hbel`.
  - **Outputs:** Write to `cv_worstcase_history` with input-fingerprint SHA-256.
  - **Algorithm:** Deterministic per § 5.1 workflow.
  - **Tests:** pytest ≥ 90% line coverage; regression fixtures cover (a) single-product train, (b) multi-product non-HPAPI, (c) multi-product with HPAPI residue, (d) post-equipment-change.
  - **Change control:** Source in `vesper/clnv-extensions` GitLab; signed commits; ValGenesis-validated extension-loading mechanism; CR-gated.
  - **Verified by:** OQ-WORST-CASE-01.

### 8.2 Trending engine custom rules (DS-CLNV-32)

- **Type:** Per-protocol OOT rules configured via ValGenesis CV declarative rule editor — Cat 4 declarative only.
- **No site-authored code.**

### 8.3 `cv_inspection_binder.pdf` template

- **Type:** ValGenesis CV report template (declarative XML + JasperReports config) — Cat 4 declarative.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200.
- 21 CFR Part 211 §§ .67, .113.
- FDA *Guide to Inspections — Validation of Cleaning Processes* (1993).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026).

### EU
- EU GMP Annex 11 §§ 4, 6, 9.
- EU GMP Annex 15.
- EU GMP Chapter 3; Chapter 5.
- EMA *Guideline on Setting Health Based Exposure Limits* (EMA/CHMP/CVMP/SWP/169430/2012, Nov 2014).

### International — ICH
- ICH Q9(R1).

### Industry guidance
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE Baseline Guide *Risk-Based Manufacture of Pharmaceutical Products* (RiskMaPP).
- PIC/S PI 006-3.
- APIC *Cleaning Validation Guideline* (latest rev.).
- USP <1072>, <1078>.
- PIC/S PI 041.

### Vendor
- ValGenesis — *CV 5.0 Reference* v5.0.
- ValGenesis — *CV 5.0 Custom Extension Development Guide* v5.0 (governs the `select_worst_case` extension's loading mechanism).

### Site
- `VSP-RB-RESTORE-001` — restore-test runbook.
- `VSP-SOP-CV-001` — Cleaning Validation procedure.
- `VSP-PR-AUD-001` — audit-trail review template.
- `VSP-PR-CV-YYYYMMDD` — periodic-review template.

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-CLNV-01 | FS-MX-01 |
| DS-CLNV-02 | FS-MX-02 |
| DS-CLNV-03 | FS-MX-03 |
| DS-CLNV-04 | FS-MX-04 |
| DS-CLNV-05 | FS-MX-05 |
| DS-CLNV-06 | FS-MACO-01 |
| DS-CLNV-07 | FS-MACO-02 |
| DS-CLNV-08 | FS-MACO-03 |
| DS-CLNV-09 | FS-MACO-04 |
| DS-CLNV-10 | FS-MACO-05 |
| DS-CLNV-11 | FS-SMP-01 |
| DS-CLNV-12 | FS-SMP-02 |
| DS-CLNV-13 | FS-SMP-03 |
| DS-CLNV-14 | FS-SMP-04 |
| DS-CLNV-15 | FS-REC-01 |
| DS-CLNV-16 | FS-REC-02 |
| DS-CLNV-17 | FS-REC-03 |
| DS-CLNV-18 | FS-REC-04 |
| DS-CLNV-19 | FS-HT-01 |
| DS-CLNV-20 | FS-HT-02 |
| DS-CLNV-21 | FS-HT-03 |
| DS-CLNV-22 | FS-HT-04 |
| DS-CLNV-23 | FS-AGT-01 |
| DS-CLNV-24 | FS-AGT-02 |
| DS-CLNV-25 | FS-AGT-03 |
| DS-CLNV-26 | FS-CHG-01 |
| DS-CLNV-27 | FS-CHG-02 |
| DS-CLNV-28 | FS-CHG-03 |
| DS-CLNV-29 | FS-CHG-04 |
| DS-CLNV-30 | FS-VER-01 |
| DS-CLNV-31 | FS-VER-02 |
| DS-CLNV-32 | FS-VER-03 |
| DS-CLNV-33 | FS-RPT-01 |
| DS-CLNV-34 | FS-DASH-01 |
| DS-CLNV-35 | FS-DASH-02 |
| DS-CLNV-36 | FS-DASH-03 |
| DS-CLNV-37 | FS-AUD-01 |
| DS-CLNV-38 | FS-AUD-02 |
| DS-CLNV-39 | FS-AUD-03 |
| DS-CLNV-40 | FS-AUD-04 |
| DS-CLNV-41 | FS-PART11-10 |
| DS-CLNV-42 | FS-PART11-50 |
| DS-CLNV-43 | FS-PART11-70 |
| DS-CLNV-44 | FS-PART11-100 |
| DS-CLNV-45 | FS-PART11-200 |
| DS-CLNV-46 | FS-DI-01 |
| DS-CLNV-47 | FS-DI-04 |
| DS-CLNV-48 | FS-DI-05 |
| DS-CLNV-49 | FS-INT-LIMS-01 |
| DS-CLNV-50 | FS-INT-EQMS-01 |
| DS-CLNV-51 | FS-INT-VAULT-01 |
| DS-CLNV-52 | FS-INT-MES-01 |
| DS-CLNV-53 | FS-INT-AD-01 / FS-XSYS-AD-01 |
| DS-CLNV-54 | FS-INT-APR-01 |
| DS-CLNV-55 | FS-PERF-01 |
| DS-CLNV-56 | FS-BAK-01 |
| DS-CLNV-57 | FS-BAK-02 |
| DS-CLNV-58 | FS-SEC-01 |
| DS-CLNV-59 | FS-TRN-01 |
| DS-CLNV-60 | FS-PR-01 |

**FS-IDs in parent FS NOT covered (with rationale):**

- FS-XSYS-BAK-01 (Veeam backup integration) — covered at site enterprise-backup-service DS level per `AUR-URS-BACKUP-001`; site binding via DS-CLNV-56.
- FS-XINT-EQMS-02 (eQMS status webhook) — covered in § 7.2 status-callback handling.

## 11. Appendix B — Design-level Risk Register

| DR-ID | Design-stage risk | Origin design choice | Mitigation reference |
|---|---|---|---|
| DR-01 | Toxicology HBEL drift if `tox_hbel` register edited without CV-side re-trigger of MAC recompute | DS-CLNV-02 + DS-CLNV-08 | CMMS-equivalent webhook from toxicology register to MAC engine; periodic-review item |
| DR-02 | Trio criteria selection could be gamed (rounding the most-stringent across criteria) | DS-CLNV-07 decision capture | `cv_macp_decision` table captures all three values; full rationale persisted |
| DR-03 | Hazard-class force-HBEL flag (DS-CLNV-10) depends on accurate hazard classification at product master | DS-CLNV-10 | Toxicologist co-approval on hazard-class change; periodic-review item |
| DR-04 | Recovery factor < 0.50 INVALID flag could be bypassed by recovery-study revision artifact | DS-CLNV-16 | Audit-trail captures revision history; trend job tracks recovery-factor evolution |
| DR-05 | Hold-time MES integration (DS-CLNV-21) could fail silently — PAS-X schedules production without hold-time-limit check | DS-CLNV-21 | Daily integration-health check; alert on missed hold-time-query pattern |
| DR-06 | Unsupported changeover pair scheduling could occur during MES-integration outage | DS-CLNV-27 + IF-MES-01 | PAS-X fail-closed on CV-API unavailability; integration-health monitor |
| DR-07 | Cleaning-agent residue overlooked (focus on API residue only) | DS-CLNV-24 | Agent MAC enforced parallel to API MAC; OQ-AGENT-MAC-01 explicit test |
| DR-08 | Worst-case selector defect (DS-CLNV-03) could yield non-conservative worst-case | § 8.1 mini-SDS | Cat 5 SDLC: ≥ 90% test coverage; regression fixtures; CR-gated deployment |
| DR-09 | OOS gate bypass via direct DB manipulation | DS-CLNV-38 append-only + role grants | DBA dual-control; monthly audit-trail review |
| DR-10 | Recovery-factor surface-material mis-application (SS-316L recovery applied to PTFE) | DS-CLNV-18 enforcement | Configuration-level constraint at MAC-engine join; OQ negative tests |
| DR-11 | Ageing alerts (DS-CLNV-36) may not propagate to operational queues if dashboard not reviewed daily | DS-CLNV-36 dashboard | Email digest to CV Lead daily; periodic-review item |
| DR-12 | New-product workflow gap — product introduced without changeover matrix expansion | § 5.5 workflow + DS-CLNV-28 | Workflow gating: scheduling cannot proceed until matrix rows for new-product pairs approved; OQ-NEW-PRODUCT-01 |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
