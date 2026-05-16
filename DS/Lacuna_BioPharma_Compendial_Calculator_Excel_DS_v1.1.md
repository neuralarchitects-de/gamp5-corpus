---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "LCN-FS-EXCEL-CC-001 v1.2 (parent FS)"
  - "LCN-URS-EXCEL-CC-001 v1.2 (parent URS — informational)"
  - "GAMP 5 (2nd ed.) Cat 5 — Software Design Specification conventions (hybrid Cat-4 + Cat-5 treatment for user-developed Excel)"
  - "21 CFR Part 11; EU GMP Annex 11; USP <905>, <711>, <61>, <62>, <71>, <85>, <86>; ICH Q2(R2); Q3A/B"
  - "Microsoft — Office Cell Functions Reference (Excel 365)"
parent_fs:
  document_number: LCN-FS-EXCEL-CC-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Lacuna_BioPharma_Compendial_Calculator_Excel_FS_v1.3.md
parent_urs:
  document_number: LCN-URS-EXCEL-CC-001
  version: 1.2
  file: ../../../URS/_generated/final/Compendial_Calculator_Excel_Workbook__Lacuna_BioPharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Software Design Specification (SDS)

## Compendial Calculator Excel Workbook — Multi-Compendial Calculation Library (Microsoft Excel 365)

**Document Number:** LCN-DS-EXCEL-CC-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** LCN-FS-EXCEL-CC-001 v1.2 | **Parent URS:** LCN-URS-EXCEL-CC-001 v1.2 *(informational)*
**Site:** Lacuna BioPharma DAC, QC Solid Dosage + Sterile, Cork, Ireland *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom / Site-Developed *(hybrid posture: Excel application = Cat 1 commodity; the user-developed formula library + named ranges + cell-protection scheme + optional VBA macro scaffolding constitute Cat 5 code — see § 4)*
**Project Mode:** Site-developed Excel workbook (formula library + optional VBA macros) hosted on commercial product **Microsoft Excel 365**. Treated as Cat 5 SDS per GAMP 5 2nd ed. § 8 — user-developed code inside a commodity host elevates the artefact's category.
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; USP <905>, <711>, <701>, <61>, <62>, <71>, <85>, <86>; EP 2.9.40, 2.9.3, 2.9.1, 5.1.4, 2.6.12, 2.6.13, 2.6.14; ICH Q2(R2); Q3A(R2); Q3B(R2)

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Statistician) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Compendial Methods) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Approver (System Owner — Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue (SDS shape for user-developed Excel workbook). Inherited Tier T1-T2 hybrid from parent URS+FS pair (LCN-URS-EXCEL-CC-001 / LCN-FS-EXCEL-CC-001 v1.2). DS covers 51/51 FS-IDs. **Posture note:** parent FS positions the workbook as "macros disabled / Cat 3 preserving." This DS retains that no-VBA-at-v1.0 posture but adopts the Cat 5 SDS shape because the user-developed formula library, named ranges, decision-boundary formulae, and (optional future) VBA macro scaffolding constitute code under GAMP 5 2nd ed. § 8. VBA macro module map is documented as **empty in v1.0** per FS-CFG-06 hard prohibition; the SDS reserves the module-map section for the formal Cat-4-with-Cat-5-sub-component upgrade path. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

DS-specific terms only (URS + FS inherited).

| Term | Definition |
|---|---|
| Calculator Sheet | One of the per-compendium-method calculation sheets (`Calc-USP905`, etc.). |
| Named Range | An Excel-level named cell-range scoped to one calculator sheet, used by formulas + data-validation. |
| Decision-boundary Cell | A cell whose formula encodes a compendial pass/fail decision (e.g., AV vs L1/L2 in USP <905>). |
| Formula Inventory | The `Validation` sheet table enumerating every formula cell + its expected output type + the regression test-case ID. |
| xlsxinspect | Site Python tool that scans `.xlsx` files for VBA, ActiveX, queries, external links, sheet-protection state, named-range integrity. |

## 1. Purpose

This DS specifies the technical design of the Lacuna BioPharma Compendial Calculator Excel workbook `LCN-CALC-CC-v1.0.xlsx`: workbook architecture, per-sheet module decomposition, data model (worksheet schemas + cell-ranges + named ranges), per-compendium algorithm design, file-interface design, security design, and deployment design. It implements `LCN-FS-EXCEL-CC-001` v1.2 and is the controlling input to OQ regression (`LCN-OQ-EXCEL-CC-001`) + PQ user-acceptance (`LCN-PQ-EXCEL-CC-001`).

## 2. Scope

In scope: workbook formula-as-code design; named-range design; cell-protection scheme; per-compendium algorithm specification; xlsxinspect verification design; Vault QualityDocs deployment design; signature template design. Out of scope: Microsoft Excel itself (Cat 1 commodity); Veeva Vault QualityDocs internals (separate Cat 4 DS); LIMS transcription workflow (out of system per FS-OUT-03).

## 3. Architectural Overview

### 3.1 Logical View

```
   ┌──────────────────────────────────────────────────────────────┐
   │  Veeva Vault QualityDocs 24R1 (lifecycle DRAFT → SUPERSEDED) │
   └────────────────────────────┬─────────────────────────────────┘
                                │ EFFECTIVE download only
                                ▼
   ┌──────────────────────────────────────────────────────────────┐
   │  Microsoft Excel 365 — GPO `GMP-Lab-Workstations`             │
   │  Macros DISABLED · ActiveX DISABLED · VBA Object Model OFF    │
   └────┬───────────────────────────┬────────────────────────┬─────┘
        ▼                           ▼                        ▼
   ┌──────────┐         ┌──────────────────────────┐  ┌──────────────┐
   │ Inputs   │  ◄───►  │ Calc-USP905              │  │ Output       │
   │ sheet    │         │ Calc-USP711-Disso        │  │ sheet        │
   │ (input   │         │ Calc-USP61-62-Microbial  │  │ (print-      │
   │  cells   │         │ Calc-USP71-Sterility     │  │  ready PDF/A)│
   │  only    │         │ Calc-USP85-86-Endotoxin  │  └──────┬───────┘
   │ unlocked)│         │ Calc-Assay-LC            │         │
   └────┬─────┘         │ Calc-RS                  │         ▼
        │               └──────────┬───────────────┘   ┌────────────────┐
        │                          │                   │ Controlled     │
        ▼                          ▼                   │ folder         │
   ┌──────────────┐         ┌──────────────┐           │ (Write-only    │
   │ Constants    │         │ Validation   │           │  ACL)          │
   │ (hidden)     │         │ (hidden,     │           └────────────────┘
   │ k, L1, L2,   │         │  formula     │
   │ TAMC/TYMC,   │         │  inventory + │
   │ EL params    │         │  test-case   │
   └──────────────┘         │  IDs)        │
                            └──────────────┘
```

### 3.2 Process View

| Process | Trigger | Steps |
|---|---|---|
| Analyst calculation run | Analyst opens EFFECTIVE workbook from Vault | (a) populate `Inputs` per active calculator selector; (b) Excel re-calculates dependent cells; (c) `Output` sheet renders disposition; (d) analyst e-signs in Vault on PDF/A export |
| Workbook revision | Method Author opens DRAFT copy in Vault checkout | (a) edit formulas; (b) update `Validation` sheet inventory; (c) run xlsxinspect locally; (d) check-in → Vault lifecycle DRAFT → IN-REVIEW → APPROVED → EFFECTIVE |

### 3.3 Technology View

| Layer | Technology | Version |
|---|---|---|
| Workbook host | Microsoft Excel 365 | current channel |
| Workbook file format | OOXML `.xlsx` | ISO/IEC 29500-1:2016 |
| EDMS | Veeva Vault QualityDocs | 24R1 |
| Output PDF format | PDF/A-3 (ISO 19005-3) | via Excel built-in export |
| GPO management | Active Directory Group Policy | GMP-Lab-Workstations |
| Inspection tooling | Python 3.12 `openpyxl` + `oletools` | site tool `xlsxinspect` v1.4 |
| Backup | Veeam B&R 12.1 | per AUR-FS-BACKUP-001 |

## 4. Software Architecture

The workbook is structurally **a multi-sheet formula library + data-validation rules + cell-protection scheme**. The "code" of the workbook is the union of:

- per-cell formulas (declarative functional language — Excel formula grammar);
- named ranges (the workbook's data-model bindings);
- data-validation rules (the input-domain enforcement layer);
- cell-protection / sheet-protection / workbook-protection (the integrity-enforcement layer);
- print template (the output-rendering layer);
- VBA module map (**empty in v1.0** per FS-CFG-06; reserved for the upgrade path).

| Architectural component | Responsibility |
|---|---|
| Input layer (`Inputs` sheet + per-calculator input regions) | Capture batch ID, method ID, calculator selector, per-stage input values. |
| Validation layer (Excel Data Validation on input cells) | Enforce numeric type, in-range, sample-size gates. |
| Calculation layer (per-calculator-sheet formula cells) | Compute per-compendium decision logic: AV (USP <905>), stage-progression (USP <711>), TAMC/TYMC limits (USP <61>/<62>), Q5 sterility verdict (USP <71>), endotoxin limit (USP <85>/<86>), %LC + RS (Assay/RS). |
| Constants layer (`Constants` hidden sheet) | Compendium constants: k, L1, L2, AV thresholds, microbial limits per dosage form, EL = K/M parameters. |
| Output layer (`Output` sheet + print template + PDF/A export) | Render analyst-readable summary; full lock; PDF/A-3 export-only path. |
| Integrity layer (sheet/workbook protection + GPO macro-block) | Prevent inadvertent formula modification; structure-protection prevents unhide; GPO blocks VBA Object Model. |
| Inspection layer (xlsxinspect external tool) | Verify no VBA / macros / ActiveX / external links + sheet-protection state + named-range inventory at every release. |

## 5. Module Decomposition

The workbook decomposes into the following "modules" (each is one logical sheet or a closely-coupled group of named ranges + formulas):

| Module ID | Module name | Responsibility | Interface (what it exposes) | Dependencies | GxP-criticality |
|---|---|---|---|---|---|
| M-01 | `About` | Version, checksum, lifecycle status, change log | Read-only metadata cells | None | R3 |
| M-02 | `Inputs` | Batch ID, method ID + version, calculator selector | Named cells `BATCH_ID`, `METHOD_ID`, `METHOD_VER`, `CALC_SEL` | M-01 | R1 (drives downstream calc) |
| M-03 | `Calc-USP905` | USP <905> Content Uniformity Stage 1 + Stage 2 | Named ranges `S1_inputs`, `S2_inputs`; outputs `S1_AV`, `S2_AV`, `DISPOSITION` | M-02, M-09 (Constants) | R1 |
| M-04 | `Calc-USP711-Disso` | USP <711> Dissolution Stages S1/S2/S3 | Named ranges `Disso_S1`, `Disso_S2`, `Disso_S3`; outputs `S1_PASS`, `S2_PASS`, `S3_PASS`, `STAGE_DISPOSITION` | M-02, M-09 | R1 |
| M-05 | `Calc-USP61-62-Microbial` | USP <61>+<62> microbial limits | Named ranges `TAMC_in`, `TYMC_in`, `Specified_in`; outputs `TAMC_verdict`, `TYMC_verdict` | M-02, M-09 | R1 |
| M-06 | `Calc-USP71-Sterility` | USP <71> sterility | Named ranges `Sterility_in`; outputs `STERILITY_VERDICT` | M-02, M-09 | R1 |
| M-07 | `Calc-USP85-86-Endotoxin` | USP <85>+<86> endotoxin | Named ranges `Endo_in`, `K`, `M_dose`; outputs `EL`, `ENDO_VERDICT` | M-02, M-09 | R1 |
| M-08 | `Calc-Assay-LC` + `Calc-RS` | %LC + RS calculations per ICH Q2(R2) + Q3A/B | Named ranges `Assay_in`, `RS_in`; outputs `pct_LC`, `RS_total`, `RS_threshold_flag` | M-02, M-09 | R1 |
| M-09 | `Constants` (hidden) | Compendium constants + k + L1 + L2 + microbial limits + EL params | Read-only named-range table | None | R1 |
| M-10 | `Validation` (hidden) | Formula inventory + OQ regression test-case IDs | Read-only named-range table + named cells `FORMULA_INV` | M-01..M-08 | R2 |
| M-11 | `Output` | Print-ready summary; PDF/A-3 export anchor | Locked output cells + print area + header/footer tags | All M-03..M-08 + M-09 + M-10 | R1 |
| M-12 | VBA module map (**empty in v1.0**) | Reserved for future Cat-4-with-Cat-5-sub-component upgrade — only used if FS-CFG-06 is amended | n/a | n/a | n/a |

## 6. Data Model Design

### 6.1 Worksheet Schemas (per-sheet cell-range design)

| Sheet | Region | Cells | Type | Locked? |
|---|---|---|---|---|
| `About` | Header | A1:F1 | string | yes |
| `About` | Version + checksum + status | B3:B6 | string | yes |
| `Inputs` | Batch + method ID | B3:B4 | string | NO |
| `Inputs` | Method version + calculator selector | B5:B6 | string + enum | NO |
| `Calc-USP905` | S1 inputs (n=10) | B7:B16 | numeric (50–150 %LC) | NO |
| `Calc-USP905` | S2 inputs (n=20 add) | B17:B36 | numeric | NO |
| `Calc-USP905` | Computed M, X, s, AV | D7:D9, D11 | numeric (formula) | yes |
| `Calc-USP905` | Disposition cell | F7 | string (formula) | yes |
| `Calc-USP711-Disso` | S1 (n=6) | B7:B12 | numeric (0–110 %Q) | NO |
| `Calc-USP711-Disso` | S2 (+ n=6) | B13:B18 | numeric | NO |
| `Calc-USP711-Disso` | S3 (+ n=12) | B19:B30 | numeric | NO |
| `Calc-USP711-Disso` | Stage disposition cells | F7, F13, F19 | string (formula) | yes |
| `Calc-USP61-62-Microbial` | TAMC + TYMC + specified | B7:B14 | numeric (0–1e8 CFU/g) | NO |
| `Calc-USP71-Sterility` | Method-suitability + growth obs | B7:B11 | bool / string | NO |
| `Calc-USP85-86-Endotoxin` | EU/mL + dose + K factor | B7:B12 | numeric (0–1e4 EU/mL) | NO |
| `Calc-Assay-LC` | Areas + concentrations + potency | B7:B14 | numeric | NO |
| `Calc-RS` | Per-impurity area + RRF | B7:F26 | numeric matrix | NO |
| `Constants` (hidden) | k, L1, L2, AV thresholds, TAMC/TYMC limits, EL K/M tables, Rounding_n | A:E (named ranges) | typed | yes (workbook-protected unhide) |
| `Validation` (hidden) | Formula inventory: cell-ref, formula-text, expected-output-type, OQ-test-ID | A:D | typed | yes |
| `Output` | All fields | A1:G80 | mixed (formula-driven) | yes (entire sheet) |

### 6.2 Named Range Inventory

| Named range | Sheet | Range | Type | Justification |
|---|---|---|---|---|
| `BATCH_ID` | Inputs | B3 | string | Single source of batch identification |
| `METHOD_ID` | Inputs | B4 | string | — |
| `METHOD_VER` | Inputs | B5 | string | — |
| `CALC_SEL` | Inputs | B6 | enum | Active-calculator selector — used to gate per-sheet inputs |
| `S1_inputs` | Calc-USP905 | B7:B16 | numeric vector (10) | USP <905> S1 |
| `S2_inputs` | Calc-USP905 | B17:B36 | numeric vector (20) | USP <905> S2 |
| `Disso_S1` | Calc-USP711-Disso | B7:B12 | numeric vector (6) | USP <711> S1 |
| `Disso_S2` | Calc-USP711-Disso | B13:B18 | numeric vector (6) | USP <711> S2 |
| `Disso_S3` | Calc-USP711-Disso | B19:B30 | numeric vector (12) | USP <711> S3 |
| `k_905`, `L1_905`, `L2_905` | Constants | per-dosage-form | numeric | USP <905> per-form k + L thresholds |
| `Q_711` | Constants | per-monograph | numeric | USP <711> Q value |
| `TAMC_lim`, `TYMC_lim` | Constants | per-dosage-form | numeric | USP <61>/<62> per-form limits |
| `K_endo`, `M_endo` | Constants | per-dosage-form / route | numeric | USP <85>/<86> EL = K/M |
| `Rounding_n` | Constants | per-method-type | int | USP-NF 7.20 / EP per-method rounding |
| `FORMULA_INV` | Validation | per-formula row | typed | OQ regression coverage |

### 6.3 Retention + Encryption

| Aspect | Value |
|---|---|
| Workbook file storage | Vault QualityDocs 24R1 (vendor-managed encryption-at-rest) |
| Output PDF storage | `\\lcn-gmp-fs01\compendial-calc-output` — NetApp SnapLock Compliance mode |
| Retention | ≥ 7 y default; ≥ 25 y if linked to product release |
| Backup | Veeam file-level capture (Tier T3) |
| Data classification | GxP (no PHI / PII expected in inputs) |

## 7. Algorithm Design (per-Compendium pseudocode)

### 7.1 USP <905> Content Uniformity (M-03)

Input domain: per-unit `%LC` values in 50–150 %.

```
function uniformity_AV(values, k, L1, L2):
    n = COUNT(values)
    M = mean(values)
    s = stdev(values, sample=True)
    X = clamp(M, 98.5, 101.5)   // per USP <905>
    AV = ABS(M - X) + k * s
    if AV <= L1:
        return ("PASS-S1", AV)
    elif n_total_S2 reached AND AV <= L2:
        return ("PASS-S2", AV)
    else:
        return ("FAIL", AV)
```

Implementation: `Calc-USP905!F7 = IF(AV<=L1, "PASS-S1", IF(AV<=L2, "PASS-S2", "FAIL"))`. Numerical precision: full Excel double-precision (IEEE 754) on intermediate cells; rounding via `ROUND(value, Rounding_n)` at presentation only.

### 7.2 USP <711> Dissolution Stage Progression (M-04)

```
function dissolution_stage(S1, S2, S3, Q):
    if min(S1) >= Q + 5:
        return ("PASS-S1")
    pooled_S2 = S1 ∪ S2  // n=12
    if mean(pooled_S2) >= Q AND min(pooled_S2) >= Q - 15:
        return ("PASS-S2")
    pooled_S3 = pooled_S2 ∪ S3  // n=24
    if mean(pooled_S3) >= Q AND
       COUNTIF(pooled_S3 < Q-15) <= 2 AND
       COUNTIF(pooled_S3 < Q-25) == 0:
        return ("PASS-S3")
    return ("FAIL")
```

### 7.3 USP <61> / <62> Microbial Limits (M-05)

```
function microbial_verdict(TAMC, TYMC, specified_obs, dosage_form):
    TAMC_lim = lookup(Constants, dosage_form, "TAMC")
    TYMC_lim = lookup(Constants, dosage_form, "TYMC")
    spec_lim = lookup(Constants, dosage_form, "Specified")
    pass_tamc = TAMC <= TAMC_lim
    pass_tymc = TYMC <= TYMC_lim
    pass_spec = specified_obs == "absent"  // per USP <62>
    return ("PASS" if all([pass_tamc, pass_tymc, pass_spec]) else "FAIL")
```

### 7.4 USP <85> / <86> Endotoxin (M-07)

```
function endotoxin_verdict(observed_eu_per_ml, K_factor, M_dose):
    EL = K_factor / M_dose       // EU/mL
    if observed_eu_per_ml < EL:
        return ("PASS", EL)
    else:
        return ("FAIL", EL)
```

### 7.5 Assay %LC + Related Substances (M-08)

```
function pct_LC(area_sample, area_std, conc_std, conc_sample, potency_std_pct):
    return (area_sample / area_std) * (conc_std / conc_sample) * (potency_std_pct / 100.0) * 100.0

function RS_threshold(impurity_pct, dosage_form):
    reporting = lookup_Q3A_reporting(dosage_form)
    identification = lookup_Q3A_identification(dosage_form)
    qualification = lookup_Q3A_qualification(dosage_form)
    if impurity_pct < reporting:
        return "BELOW_REPORTING"
    elif impurity_pct < identification:
        return "REPORT"
    elif impurity_pct < qualification:
        return "REPORT + IDENTIFY"
    else:
        return "REPORT + IDENTIFY + QUALIFY"
```

### 7.6 Edge-case OQ Test Vectors

Per FS-CALC-09 the `Validation` sheet enumerates boundary OQ test cases:
- USP <905>: AV at `L1 - 0.05`, `L1`, `L1 + 0.05`, `L2 - 0.05`, `L2`, `L2 + 0.05`
- USP <711>: per-stage minimum at `Q + 5 - 0.05`, `Q + 5`, `Q + 5 + 0.05`
- USP <61>/<62>: TAMC at `lim - 1`, `lim`, `lim + 1` (boundary at integer CFU/g)
- USP <85>/<86>: observed at `EL - 0.1`, `EL`, `EL + 0.1` EU/mL

## 8. Interface Design

### 8.1 File-format Interface (IF-FILE)

| Aspect | Value | FS-ID |
|---|---|---|
| Workbook format | `.xlsx` (OOXML, ISO/IEC 29500-1:2016) | — |
| Output format | PDF/A-3 (ISO 19005-3) via Excel `Save As → PDF` with `ISO 19005-3 compliant` option | FS-OUT-01 |
| Save target | `\\lcn-gmp-fs01\compendial-calc-output\<batch_id>_<method_id>_<ts>.pdf` | FS-OUT-02 |
| ACL | analyst `Write` only; deny `Modify`/`Delete`/`TakeOwnership` | FS-SEC-01 |

### 8.2 Vault Deployment Interface (IF-VAULT-DEPLOY)

| Aspect | Value |
|---|---|
| Source | Vault QualityDocs lifecycle `LCN-LC-CALCWB-001` |
| Allowed download state | EFFECTIVE only |
| Watermark on non-EFFECTIVE | "SUPERSEDED" rendition rule applied by Vault |
| E-signature meanings | `authorship / review / approval / retirement` per FS-LC-03 |
| Audit trail | Vault append-only per EU GMP Annex 11 § 9 |

### 8.3 Signature Template Interface (IF-SIGN)

| Element | Value | FS-ID |
|---|---|---|
| Signature manifestation fields | `printedName + dateTime + meaning` | FS-PART11-50 |
| Hash binding | Vault binds signature to document SHA-256 | FS-PART11-70 |
| Uniqueness | AD UPN enforced by Vault | FS-PART11-100 |
| Re-auth | Vault forces re-auth at signing | FS-PART11-200 |

### 8.4 xlsxinspect Interface (IF-XLSXINSPECT)

| Aspect | Value |
|---|---|
| Invocation | site Python tool `xlsxinspect inspect <file.xlsx>` at OQ + at every revision sign-off |
| Output | JSON report archived to Vault revision package |
| Verification rules | no `xl/vbaProject.bin`; no ActiveX; no external links; no queries; sheet-protection ON; structure-protection ON; expected sheet inventory matches `LCN-CALC-CC-SCHEMA-v1.0.json` |

## 9. Security Design

| Layer | Mechanism | FS-ID |
|---|---|---|
| Macro / VBA | GPO `GMP-Lab-Workstations` disables Office macros, ActiveX, queries, VBA Object Model | FS-CFG-01 |
| Workbook contents | NO VBA, NO macros, NO ActiveX, NO queries — enforced by xlsxinspect at every release | FS-CFG-06 |
| Sheet protection | every sheet protected except per-sheet input regions; sheet-protection password held by Method Author role (anti-fat-finger, not a security control) | FS-CFG-02 + § 3.3 of FS |
| Workbook structure protection | prevents unhide of `Constants` / `Validation` sheets | FS-CFG-07 |
| Storage encryption | Vault QualityDocs at-rest encryption (vendor); SnapLock Compliance mode on output folder | FS-SEC-01 + FS-DI-06 |
| AuthN | AD interactive Kerberos to workstation; Vault SSO via SAML | FS-XSYS-AD-01 |
| AuthZ — workbook access | Vault role-based (Method Author / Reviewer / Approver / Analyst) | FS-LC-01..05 |
| AuthZ — output folder | NTFS Write-only for analyst accounts; deny modify/delete/take-ownership | FS-SEC-01 |
| Transport | SMB 3.1.1 with signing + encryption to file server | — |
| Audit-trail | Vault append-only (Annex 11 § 9); workbook-side `Output` user + ts captured via GPO `Insert username on save` | FS-AT-03 + FS-DI-01 |
| Password policy | AD GPO 14 char min, 90 d rotation, complexity, loss-of-control workflow | FS-PART11-300 |
| Removable-media block | GPO `BlockNonVaultLocalCopies` (best-effort) + training + audit-log review | FS-SEC-02 |

## 10. Deployment Design

| Aspect | Value |
|---|---|
| Distribution model | Controlled-workbook: Vault QualityDocs ONLY; out-of-band copies prohibited |
| Deployment runbook | `LCN-RB-CALCWB-DEPLOY-001`: (a) author check-in; (b) reviewer e-sign; (c) approver e-sign; (d) effective-promotion + SHA-256 recompute → `About` sheet metadata + Vault metadata; (e) xlsxinspect run → JSON report attached to Vault revision package |
| Hash management | SHA-256 of `.xlsx` recorded in Vault metadata + on `About` sheet at promotion |
| Version pinning | Workbook major-version promotion only (Vault config); no silent in-place patches |
| Quarterly GPO compliance scan | verifies macro-block GPO + ActiveX-block + VBA-Object-Model-disabled still applied to all lab workstations |
| USP-revision tracker | quarterly check of USP <905>/<711>/<61>/<62>/<71>/<85>/<86> updates per FS-PR-02; impact assessment within 90 days |
| Backup | Output folder in Veeam job `gmp-fs01-daily`; Tier T3 (RPO ≤ 72 h; RTO ≤ 72 BH); S3 Object Lock Compliance + LTO-9 monthly air-gap |
| Restore drill | annual QA-witnessed per AUR-FS-BACKUP-001 |
| Training | Cornerstone curriculum `LCN-CURR-CALCWB-Analyst-v1` mandatory before access |
| Periodic review | `LCN-PR-CALCWB-YYYYMMDD` annually |

## 11. Module Specification Table

Per § 2B.5(8) of METHODOLOGY — pointer table; full Module Specification artefact lives downstream.

| Module ID | Module Spec doc | Notes |
|---|---|---|
| M-03 USP <905> | `LCN-MS-USP905-001` | formula + boundary tests |
| M-04 USP <711> | `LCN-MS-USP711-001` | stage-progression logic |
| M-05 USP <61>/<62> | `LCN-MS-MICRO-001` | dosage-form lookup |
| M-06 USP <71> | `LCN-MS-STER-001` | method-suitability binding |
| M-07 USP <85>/<86> | `LCN-MS-ENDO-001` | EL = K/M lookup |
| M-08 Assay-LC + RS | `LCN-MS-ASSAY-RS-001` | %LC + Q3A/B threshold flags |
| M-09 Constants | `LCN-MS-CONST-001` | constant-table provenance + USP revision tracker |
| M-10 Validation | `LCN-MS-VALID-001` | formula inventory + OQ test-case IDs |
| xlsxinspect tool | `LCN-MS-XLSXINSPECT-001` | Python implementation + acceptance vectors |

## 12. References

### US
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300
- USP <905>, <711>, <701>, <61>, <62>, <71>, <85>, <86>

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EP 2.9.40, 2.9.3, 2.9.1, 5.1.4, 2.6.12, 2.6.13, 2.6.14

### International
- ICH Q2(R2); ICH Q3A(R2); ICH Q3B(R2); ICH Q4B Annex 6
- ISPE GAMP 5 (2nd Ed., 2022) — Cat 5 conventions for user-developed code in commodity host (§ 8)
- ISPE GAMP GPG *A Risk-Based Approach to Compliant GxP Computerized Systems*
- ISO/IEC 29500-1:2016 (OOXML); ISO 19005-3 (PDF/A-3)
- OWASP ASVS v4 — A.4 Access Control (folder ACL)
- NIST SP 800-218 SSDF (informational for the xlsxinspect tool SDLC)

### DACH
- BSI IT-Grundschutz APP.1.1 Office-Anwendungen (informational)

### Vendor
- Microsoft Office — *Excel 365 Functions Reference* (current channel)
- Microsoft — *Group Policy Settings Reference Spreadsheet for Office* (current)

## 13. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) |
|---|---|
| DS-LC-01 | FS-LC-01 |
| DS-LC-02 | FS-LC-02 |
| DS-LC-03 | FS-LC-03 |
| DS-LC-04 | FS-LC-04 |
| DS-LC-05 | FS-LC-05 |
| DS-CFG-01 | FS-CFG-01 |
| DS-CFG-02 | FS-CFG-02 |
| DS-CFG-03 | FS-CFG-03 |
| DS-CFG-04 | FS-CFG-04 |
| DS-CFG-05 | FS-CFG-05 |
| DS-CFG-06 | FS-CFG-06 |
| DS-CFG-07 | FS-CFG-07 |
| DS-CALC-01 | FS-CALC-01 |
| DS-CALC-02 | FS-CALC-02 |
| DS-CALC-03 | FS-CALC-03 |
| DS-CALC-04 | FS-CALC-04 |
| DS-CALC-05 | FS-CALC-05 |
| DS-CALC-06 | FS-CALC-06 |
| DS-CALC-07 | FS-CALC-07 |
| DS-CALC-08 | FS-CALC-08 |
| DS-CALC-09 | FS-CALC-09 |
| DS-IV-01 | FS-IV-01 |
| DS-IV-02 | FS-IV-02 |
| DS-IV-03 | FS-IV-03 |
| DS-IV-04 | FS-IV-04 |
| DS-AT-01 | FS-AT-01 |
| DS-AT-02 | FS-AT-02 |
| DS-AT-03 | FS-AT-03 |
| DS-OUT-01 | FS-OUT-01 |
| DS-OUT-02 | FS-OUT-02 |
| DS-OUT-03 | FS-OUT-03 |
| DS-PART11-50 | FS-PART11-50 |
| DS-PART11-70 | FS-PART11-70 |
| DS-PART11-100 | FS-PART11-100 |
| DS-PART11-200 | FS-PART11-200 |
| DS-PART11-300 | FS-PART11-300 |
| DS-DI-01 | FS-DI-01 |
| DS-DI-02 | FS-DI-02 |
| DS-DI-03 | FS-DI-03 |
| DS-DI-04 | FS-DI-04 |
| DS-DI-05 | FS-DI-05 |
| DS-DI-06 | FS-DI-06 |
| DS-BAK-01 | FS-BAK-01, FS-XSYS-BAK-01 |
| DS-PERF-01 | FS-PERF-01 |
| DS-SEC-01 | FS-SEC-01 |
| DS-SEC-02 | FS-SEC-02 |
| DS-TRN-01 | FS-TRN-01 |
| DS-PR-01 | FS-PR-01 |
| DS-PR-02 | FS-PR-02 |
| DS-INT-AD-01 | FS-XSYS-AD-01 |
| DS-MOD-XLSXINSPECT-01 | FS-CFG-06, FS-AT-01, FS-AT-02 |
| DS-MOD-CONSTANTS-01 | FS-CALC-01..07, FS-PR-02 |

Note on DS-ID convention: this is an SDS not a CS, so DS-IDs reflect § 4 architectural components + § 5 module + § 7 algorithm decisions in addition to per-CI bindings inherited from the FS namespace.

## 14. Appendix B — Design-level Risk Register

| ID | Design risk | Likelihood | Impact | Mitigation in this DS |
|---|---|---|---|---|
| DR-01 | Cell-protection bypass via Excel password-removal exploit on legacy `.xls` re-save path | Low | Critical | DS-CFG-02 + DS-CFG-07 + xlsxinspect verifies sheet-protection state at every release sign-off |
| DR-02 | Future workbook variant adds VBA macros, escalating to Cat 4+Cat 5 hybrid without SDS amendment | Low | Critical | M-12 module slot reserved + DS-MOD-XLSXINSPECT-01 hard-blocks merge on `xl/vbaProject.bin` presence + change-control workflow flags any FS-CFG-06 amendment as new FS requirement |
| DR-03 | Rounding bias near USP <905> L1/L2 tier boundary or USP <711> Q±15 / Q-25 boundary | Medium | High | DS-CALC-08 ROUND-at-presentation-only + DS-CALC-09 boundary OQ vector list (§ 7.6) |
| DR-04 | Locale mis-parse on non-en-IE workstation (comma-decimal) silently coerces numeric input | Low | High | DS-IV-04 + xlsxinspect locale check + analyst-workstation GPO locale lock |
| DR-05 | Wrong stage selected (e.g., S1 inputs filled but S2 disposition computed) | Medium | High | DS-CFG-05 named-range toggle + missing-input sample-size gate (DS-IV-02) returns `MISSING — CANNOT CALCULATE` |
| DR-06 | USP revision missed, workbook stale relative to current compendium | Low | High | DS-PR-02 quarterly USP-revision tracker + 90 d impact-assessment window |
| DR-07 | Saved PDF deleted from controlled folder by misconfigured ACL change | Low | Medium | DS-SEC-01 deny-modify/delete/take-ownership ACL + DS-BAK-01 nightly Veeam capture |
| DR-08 | Constants sheet drift (k, L1, L2, EL params) when new dosage form added without OQ regression update | Medium | High | DS-MOD-CONSTANTS-01 schema-versioning + Validation sheet OQ-test-ID coverage check at xlsxinspect run |
| DR-09 | GPO drift re-enables macros across lab workstations | Low | Critical | DS-SEC-02 quarterly GPO compliance scan + xlsxinspect at every release |
| DR-10 | Vault rendition watermark for SUPERSEDED versions misconfigured, allowing stale-version use | Low | High | DS-LC-02 Vault rendition rule verified at quarterly Vault config audit |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
