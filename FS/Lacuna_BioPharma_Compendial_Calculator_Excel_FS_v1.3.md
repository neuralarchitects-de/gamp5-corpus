---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "LCN-URS-EXCEL-CC-001 v1.2 (parent URS)"
  - "PharmaDevils SOP-anchored Excel-validation guidance"
  - "GAMP 5 (2nd Ed., 2022) Category 3 conventions"
  - "ISPE GAMP GPG A Risk-Based Approach to Compliant GxP Computerized Systems"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11; PIC/S PI 041"
  - "USP <905>, <711>, <701>, <61>, <62>, <71>, <85>, <86>; EP equivalents; ICH Q2(R2)"
parent_urs:
  document_number: LCN-URS-EXCEL-CC-001
  version: 1.2
  file: ../../URS/_generated/final/Compendial_Calculator_Excel_Workbook__Lacuna_BioPharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Compendial Calculator Excel Workbook — Multi-Compendial Calculation Library (Microsoft Excel 365, macros disabled)

**Document Number:** LCN-FS-EXCEL-CC-001
**Version:** 1.2
**Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** LCN-URS-EXCEL-CC-001 v1.2
**Site:** Lacuna BioPharma DAC, QC Solid Dosage + Sterile, Cork, Ireland *(fictional)*
**System Owner:** QC Manager — Compendial Methods
**System Class (GAMP 5, 2nd ed.):** Category 3 — Non-Configured Product
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; USP <905>, <711>, <701>, <61>, <62>, <71>, <85>, <86>; EP 2.9.40, 2.9.3, 2.9.1, 5.1.4, 2.6.12, 2.6.13, 2.6.14; ICH Q2(R2)

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Compendial Methods) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Statistician) | _____________ | _____________ | _____ |
| Reviewer (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue — single USP <905> CU workbook. |
| 1.2 | 2026-05-12 | (synthetic) | v1.2 alignment to URS v1.2: multi-compendial workbook (USP <905>, <711>, <61>, <62>, <71>, <85>, <86> + assay LC + RS); per-URS-ID expansion across § 4 + § 11 per METHODOLOGY § 2A.7; added input-validation + formula-audit-trail + per-sheet sample-size gating modules; explicit macro-prohibition + Cat-3-preserving stance. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## Definitions

Defined in `LCN-URS-EXCEL-CC-001`. Additional FS-specific terms:

| Term | Definition |
|---|---|
| WORKBOOK | The single `.xlsx` artefact `LCN-CALC-CC-v1.0.xlsx` |
| PRINT TEMPLATE | The configured print area + headers + footers used to render the PDF output |
| GROUP POLICY (GPO) | Site Active Directory Group Policy controlling Office macros, ActiveX, etc. |
| VAULT URN | Veeva Vault QualityDocs deep link to a specific approved version |
| xlsxinspect | Site Python tool inspecting workbook structure (no VBA, named ranges, cell-locking, formula audit) |

---

## 1. Purpose

This FS describes the implementation of the parent URS as a single controlled Excel workbook hosted in Veeva Vault QualityDocs, with site Group Policy enforcing the Cat-3 invariants (no macros, no VBA, no add-ins). The FS specifies workbook structure (per-method calculation sheets), cell-protection scheme, formula logic per compendial sheet, output template, input validation, formula audit-trail, and deployment / retention controls.

## 2. Scope

The controlled workbook + the Vault lifecycle around it + the controlled-folder save location for output PDFs. Out of scope: Microsoft Excel itself (Cat-1 commodity infrastructure).

## 3. System Architecture

### 3.1 Component Inventory

| Component | Type | Vendor | Version |
|---|---|---|---|
| Microsoft Excel | Software (commodity) | Microsoft | Excel 365 — macros disabled by GPO |
| Workbook artefact | Configured calculator | In-house | `LCN-CALC-CC-v1.0.xlsx` |
| EDMS | SaaS | Veeva | Vault QualityDocs 24R1 |
| File server | Infrastructure | Site IT | `\\lcn-gmp-fs01\compendial-calc-output` (object-locked NTFS, see CI-04) |
| Backup | SaaS / on-prem | Veeam | B&R 12.1 (per `AUR-URS-BACKUP-001`) |
| xlsxinspect | Site tool | In-house | Python 3.12 utility |

### 3.2 Workbook Structure

| Sheet | Purpose | Visibility |
|---|---|---|
| `About` | Version, checksum, EFFECTIVE/SUPERSEDED status, change log | Visible, locked |
| `Inputs` | Batch ID, method ID + version, calculator selector | Visible, only input cells unlocked |
| `Calc-USP905` | USP <905> Content Uniformity Stage 1 + Stage 2 | Visible, calculation cells locked; inputs unlocked |
| `Calc-USP711-Disso` | USP <711> Dissolution Stages S1 / S2 / S3 | Visible, calculation cells locked; inputs unlocked |
| `Calc-USP61-62-Microbial` | USP <61> + <62> microbial limits | Visible, locked except input |
| `Calc-USP71-Sterility` | USP <71> Sterility evaluation | Visible, locked except input |
| `Calc-USP85-86-Endotoxin` | USP <85> + <86> endotoxin / pyrogen | Visible, locked except input |
| `Calc-Assay-LC` | % Label Claim (assay) per ICH Q2(R2) | Visible, locked except input |
| `Calc-RS` | % Related Substances + ICH Q3A/B threshold flags | Visible, locked except input |
| `Output` | Print-ready summary (analyst, reviewer, approver, disposition, hash) | Visible, fully locked |
| `Constants` | USP / EP constants, k values, AV thresholds, microbial limits per dosage form | Hidden |
| `Validation` | OQ regression test cases + formula inventory used at qualification | Hidden, locked |

### 3.3 Cell-Protection Scheme

- Sheet protection on every sheet except input regions of `Inputs` + per-calculator sheets; unlocked cells restricted to input fields only.
- Sheet-protection password is held only by the Method Author role (vendor-only password) and is not a security control — purely to prevent inadvertent edits.
- Workbook-protection (structure) prevents users from un-hiding `Constants` / `Validation`.
- Excel application option `Trust access to the VBA object model` disabled by GPO; ActiveX disabled by GPO; XLSTART disabled by GPO; the workbook contains no VBA, ActiveX, queries, or links.
- `xlsxinspect` script verifies (no VBA project, no macros, no external links, no queries, structure-protected, expected sheet inventory) at OQ + at every revision sign-off.

---

## 4. Functional Specifications

### 4.1 Workbook Lifecycle (URS §5.1)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-LC-01 | URS-LC-01 | Vault QualityDocs lifecycle `LCN-LC-CALCWB-001` provides states `DRAFT → IN-REVIEW → APPROVED → EFFECTIVE → SUPERSEDED`. |
| FS-LC-02 | URS-LC-02 | Vault download policy: only EFFECTIVE versions served to non-author roles; older downloads watermarked SUPERSEDED via Vault rendition rule. |
| FS-LC-03 | URS-LC-03 | Vault e-signature ceremony invoked at each transition; meanings `authorship / review / approval / retirement` enforced. |
| FS-LC-04 | URS-LC-04 | Vault EFFECTIVE versions immutable by configuration; new revisions are explicit "Major Version" promotions. |
| FS-LC-05 | URS-LC-05 | The `About` sheet records the SHA-256 of the file (computed externally and recorded in Vault metadata). Hash recomputation is part of the deployment runbook `LCN-RB-CALCWB-DEPLOY-001`. |

### 4.2 Workbook Configuration & Protection (URS §5.2)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CFG-01 | URS-CFG-01 | Site Group Policy `GMP-Lab-Workstations` disables Office macros, ActiveX, queries, external links, and the VBA Object Model. The workbook does not contain VBA, macros, ActiveX, or external connections — verified at OQ via `xlsxinspect`. |
| FS-CFG-02 | URS-CFG-02 | Cell-locking applied per §3.3; sheet-protection enforced on every sheet except input regions. |
| FS-CFG-03 | URS-CFG-03 | `&Z`/`&F` and a custom header tag display version + checksum + status on every printed page; `&D` shows export date. |
| FS-CFG-04 | URS-CFG-04 | Excel data-validation on input cells per per-sheet rule sets (FS-IV-01); mandatory; out-of-range disallowed. |
| FS-CFG-05 | URS-CFG-05 | Per-sheet named ranges `S1_inputs`, `S2_inputs`, `Disso_S1`, `Disso_S2`, `Disso_S3`, etc.; the per-sheet `Stage` selector toggles which named range is active and validates that only the active range is populated. |
| FS-CFG-06 | URS-CFG-06 | OQ-NO-VBA-01: `xlsxinspect` verifies no `xl/vbaProject.bin` and no macros at every release sign-off; any deviation blocks release. Macros prohibited entirely; future variant requiring macros = Cat 4 with new FS. |
| FS-CFG-07 | URS-CFG-07 | Workbook structure-protection prevents unhide; OQ-NO-UNHIDE-01 verifies. |

### 4.3 USP Compendial Calculation Library (URS §5.3)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CALC-01 | URS-CALC-01 | `Calc-USP905`: Mean = `=AVERAGE(...)`; AV = `=ABS(M - X) + k * s` per the configured `k` from `Constants`; Disposition = `=IF(AV<=L1, "PASS-S1", IF(AV<=L2, "PASS-S2", "FAIL"))` with `L1`, `L2` from `Constants`. |
| FS-CALC-02 | URS-CALC-02 | `Calc-USP711-Disso`: Stage 1 (n=6) check `=AND(all >= Q+5)`; Stage 2 (n=12 cumulative) check `=AND(AVERAGE>=Q, all >= Q-15)`; Stage 3 (n=24 cumulative) check `=AND(AVERAGE>=Q, COUNTIF(<Q-15) <= 2, COUNTIF(<Q-25) = 0)`. |
| FS-CALC-03 | URS-CALC-03 | `Calc-USP61-62-Microbial`: counts entered as CFU/g; dosage-form selector indexes `Constants` for TAMC + TYMC + specified-microorganism limits; result `PASS / FAIL` per limit. |
| FS-CALC-04 | URS-CALC-04 | `Calc-USP71-Sterility`: Membrane-filtration / Direct-inoculation pass/fail; growth observation entered + method-suitability reference cell required. |
| FS-CALC-05 | URS-CALC-05 | `Calc-USP85-86-Endotoxin`: Gel-clot endpoint or photometric quantitative; endotoxin limit `EL = K / M` with K + M from dosage-form selector indexing `Constants`. |
| FS-CALC-06 | URS-CALC-06 | `Calc-Assay-LC`: %LC = `(area_sample / area_std) * (concentration_std / concentration_sample) * (potency_std / 100) * 100`; result rendered with monograph acceptance range from `Constants`. |
| FS-CALC-07 | URS-CALC-07 | `Calc-RS`: individual impurity % = `(area_impurity / area_principal) * (RRF) * 100`; total RS = SUM(individuals); threshold flags per ICH Q3A(R2) / Q3B(R2) reporting / identification / qualification per dosage-form. |
| FS-CALC-08 | URS-CALC-08 | Rounding via `ROUND(value, n)` per `Constants.Rounding_n` per the site rounding SOP `LCN-SOP-QC-ROUND-001`; intermediate cells use full precision. |
| FS-CALC-09 | URS-CALC-09 | OQ test cases include AV near `L1 ± 0.05` and `L2 ± 0.05`, dissolution near `Q + 5 ± 0.05` boundaries, microbial near limit (10² + 1 CFU/g), endotoxin near EL (± 0.1 EU); decision-boundary behaviour verified. |

### 4.4 Input Validation and Range Gating (URS §5.4)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-IV-01 | URS-IV-01 | Per-sheet Excel data-validation: USP <905> 50–150 % LC; USP <711> 0–110 % Q; microbial 0–10⁸; endotoxin 0–10⁴ EU/mL; assay 50–150 %; RS 0–100 %. Out-of-range Excel error dialog. |
| FS-IV-02 | URS-IV-02 | Missing-input gating: `=IF(COUNT(range)<n_required, "MISSING — CANNOT CALCULATE", ...)`; result-disposition cell shows `#N/A` propagation. |
| FS-IV-03 | URS-IV-03 | Cell-format restricted to numeric via data-validation `whole number / decimal`; text-entry triggers Excel validation-error dialog. |
| FS-IV-04 | URS-IV-04 | Workbook saved with locale `en-IE` (decimal point); OQ verifies behaviour on `de-DE`-locale workstation (comma-as-decimal) — Excel auto-converts via Region settings; OQ flags any silent mis-parse. |

### 4.5 Formula Audit-Trail and Version Comparison (URS §5.5)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AT-01 | URS-AT-01 | `Validation` sheet contains formula inventory: cell reference, formula text, expected output type, reference test-case ID per OQ regression. |
| FS-AT-02 | URS-AT-02 | `xlsxinspect compare prev.xlsx new.xlsx` produces a diff report (formula changes, cell-protection changes, named-range changes); diff report appended to revision sign-off package in Vault. |
| FS-AT-03 | URS-AT-03 | Vault QualityDocs audit trail captures lifecycle transitions + downloads with user / timestamp / signature event per EU GMP Annex 11 § 9. |

### 4.6 Output (URS §5.6)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-OUT-01 | URS-OUT-01 | `Output` sheet print area includes: batch ID, method ID + version, individual results, computed AV (or per-stage disposition for dissolution), final disposition, workbook version + checksum, analyst, reviewer, approver, timestamps. PDF/A-3 export via Excel `Save As → PDF` with `ISO 19005-3 compliant` option. |
| FS-OUT-02 | URS-OUT-02 | Save-to-PDF macro path unavailable; analyst uses `File → Save As → PDF` to the controlled folder. The folder ACL allows the analyst only `Write` (no modify, no delete) per CI-04. |
| FS-OUT-03 | URS-OUT-03 | Site SOP `LCN-SOP-QC-LIMS-TRANS-001` controls dual-key transcription into LIMS; PDF filename + SHA-256 captured in LIMS result. |

### 4.7 21 CFR Part 11 (URS §5.7)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-50 | URS-PART11-50 | Vault e-signature dialog enforces `printedName + dateTime + meaning`. |
| FS-PART11-70 | URS-PART11-70 | Vault binds signature to document-hash. |
| FS-PART11-100 | URS-PART11-100 | Vault prevents reuse / reassignment. |
| FS-PART11-200 | URS-PART11-200 | Vault forces re-auth at signing. |
| FS-PART11-300 | URS-PART11-300 | AD password policy: 14 char min, 90 d rotation, complexity, loss-of-control workflow. |

### 4.8 Data Integrity (URS §5.8)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | Per `Output` sheet — analyst captured by site GPO `Insert username on save`. |
| FS-DI-02 | URS-DI-02 | PDF export generates PDF/A-3 via Excel's built-in PDF export. |
| FS-DI-03 | URS-DI-03 | Save-time = analysis-time per the SOP gate. |
| FS-DI-04 | URS-DI-04 | LIMS holds the source individual results; the workbook does not push back to LIMS. |
| FS-DI-05 | URS-DI-05 | Calculations Accurate per OQ regression per `Validation` sheet. |
| FS-DI-06 | URS-DI-06 | NetApp SnapLock retention policy; folder availability ≥ 99 % measured per Veeam reporting. |

### 4.9 Backup, Performance, Security (URS §5.9)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BAK-01 | URS-BAK-01 | Output folder included in Veeam backup job `gmp-fs01-daily`. |
| FS-PERF-01 | URS-PERF-01 | Workbook open / calculate / PDF-export benchmark on the standard Lab workstation: ≤ 5 s for n=30. |
| FS-SEC-01 | URS-SEC-01 | NTFS `deny-modify`, `deny-delete` for non-archive accounts on the output folder. |
| FS-SEC-02 | URS-SEC-02 | Vault deployment-only flow; out-of-band copies prohibited via training + GPO `BlockNonVaultLocalCopies` (best-effort) + audit-log review. |

### 4.10 Training, Periodic Review (URS §5.10)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Cornerstone curriculum `LCN-CURR-CALCWB-Analyst-v1` mandatory before access; per-calculator-sheet worked examples. |
| FS-PR-01 | URS-PR-01 | Periodic-review template `LCN-PR-CALCWB-YYYYMMDD`. |
| FS-PR-02 | URS-PR-02 | USP-revision tracker checks USP <905> / <711> / <61> / <62> / <71> / <85> / <86> updates each quarter; impact assessed within 90 days. |

---


### 4.11 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: AD-joined workstation interactive Kerberos authentication with site GPO `URS-GPO-03` macro-block path. Conditional-access binding to policy `Standard-User Conditional Access (workstation compliance + GPO macro-block)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam file-level capture of the controlled workbook master copy and the per-calculation evidence packages on the SharePoint site library; tier classification = T3; RPO ≤ 72 h; RTO ≤ 72 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; annual QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Interface Specifications

### 5.1 IF-VAULT-DEPLOY

- Vault download → user workstation; only EFFECTIVE versions; rendition watermark for non-EFFECTIVE.

### 5.2 IF-OUTPUT-FOLDER

- SMB path `\\lcn-gmp-fs01\compendial-calc-output`; per-user `Write` only ACL; DAC denies `Modify`/`Delete`/`TakeOwnership`; folder backed up nightly.

### 5.3 IF-LIMS-TRANSCRIPTION

- Manual + dual-keyboard verification per `LCN-SOP-QC-LIMS-TRANS-001` — out of system scope.

### 5.4 IF-XLSXINSPECT

- Site Python tool invoked at OQ + at every revision sign-off; outputs JSON report archived in Vault revision package.

---

## 6. Data Model (very high-level)

| Entity | Description |
|---|---|
| Workbook Version | A single `.xlsx` file with a Vault-managed lifecycle |
| Output PDF | Per-batch artefact saved to the controlled folder |
| Vault Signature | E-sign event captured by Vault on a workbook transition |
| Formula Inventory | `Validation` sheet enumerating every formula cell |

---

## 7. Non-Functional Specifications

| Aspect | Target | URS reference |
|---|---|---|
| Cycle time | ≤ 5 s | URS-PERF-01 |
| Output retention | ≥ 7 y; ≥ 25 y if linked to product release | URS-DI-06 |
| Vault availability | per Veeva SLA | URS-LC-* |
| Macro count | exactly 0 | URS-CFG-01 + URS-CFG-06 |

---

## 8. Configuration Items

| CI ID | Item | Value |
|---|---|---|
| CI-01 | Workbook filename | `LCN-CALC-CC-v1.0.xlsx` |
| CI-02 | Workbook SHA-256 | recorded in Vault metadata |
| CI-03 | Vault doc type | `Validated Excel Workbook` |
| CI-04 | Output folder ACL | `Write` only; deny `Modify` / `Delete` / `TakeOwnership` |
| CI-05 | Cornerstone curriculum | `LCN-CURR-CALCWB-Analyst-v1` |
| CI-06 | GPO reference | `GMP-Lab-Workstations` |
| CI-07 | xlsxinspect verification | every release sign-off |
| CI-08 | Site locale | en-IE (decimal point) |
| CI-09 | Calculator sheets | USP <905> / <711> / <61>+<62> / <71> / <85>+<86> / Assay-LC / RS |
| CI-10 | Sample-size enforced per stage | USP <905> n=10 (S1) / 30 (S2); USP <711> n=6 (S1) / 6 (S2) / 12 (S3) |

---

## 9. Constraints / Assumptions / Risks

Inherited from `LCN-URS-EXCEL-CC-001`. FS-specific risks:

| Risk | Mitigation |
|---|---|
| Excel locale settings change rounding | OQ regression run against locked locale + tested on de-DE locale |
| Out-of-band copy of the workbook used | URS-SEC-02 + workstation + audit |
| GPO drift re-enables macros | Quarterly GPO compliance scan + xlsxinspect at every release |
| Wrong stage selected (e.g., S1 inputs filled but S2 disposition computed) | FS-CFG-05 named-range toggle + sample-size gate |
| Tier-boundary rounding bias | FS-CALC-09 + edge-case OQ |

## 10. References

- `LCN-URS-EXCEL-CC-001 v1.2` (parent URS)
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300
- EU GMP Annex 11 §§ 4, 6, 9, 11
- USP <905>, <711>, <701>, <61>, <62>, <71>, <85>, <86>
- EP 2.9.40, 2.9.3, 2.9.1, 5.1.4, 2.6.12, 2.6.13, 2.6.14
- ICH Q2(R2); ICH Q3A(R2); ICH Q3B(R2); ICH Q4B Annex 6
- ISPE GAMP 5 (2nd Ed., 2022) — Category 3 conventions
- ISPE GAMP GPG *A Risk-Based Approach to Compliant GxP Computerized Systems*
- PIC/S PI 041
- Site documents: `LCN-SOP-CSV-EXCEL-001`, `LCN-RB-CALCWB-DEPLOY-001`, `LCN-CURR-CALCWB-Analyst-v1`

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | Implementing FS ID | Notes |
|---|---|---|
| URS-LC-01 | FS-LC-01 | |
| URS-LC-02 | FS-LC-02 | |
| URS-LC-03 | FS-LC-03 | |
| URS-LC-04 | FS-LC-04 | |
| URS-LC-05 | FS-LC-05 | |
| URS-CFG-01 | FS-CFG-01 | |
| URS-CFG-02 | FS-CFG-02 | |
| URS-CFG-03 | FS-CFG-03 | |
| URS-CFG-04 | FS-CFG-04 | |
| URS-CFG-05 | FS-CFG-05 | |
| URS-CFG-06 | FS-CFG-06 | |
| URS-CFG-07 | FS-CFG-07 | |
| URS-CALC-01 | FS-CALC-01 | |
| URS-CALC-02 | FS-CALC-02 | |
| URS-CALC-03 | FS-CALC-03 | |
| URS-CALC-04 | FS-CALC-04 | |
| URS-CALC-05 | FS-CALC-05 | |
| URS-CALC-06 | FS-CALC-06 | |
| URS-CALC-07 | FS-CALC-07 | |
| URS-CALC-08 | FS-CALC-08 | |
| URS-CALC-09 | FS-CALC-09 | |
| URS-IV-01 | FS-IV-01 | |
| URS-IV-02 | FS-IV-02 | |
| URS-IV-03 | FS-IV-03 | |
| URS-IV-04 | FS-IV-04 | |
| URS-AT-01 | FS-AT-01 | |
| URS-AT-02 | FS-AT-02 | |
| URS-AT-03 | FS-AT-03 | |
| URS-OUT-01 | FS-OUT-01 | |
| URS-OUT-02 | FS-OUT-02 | |
| URS-OUT-03 | FS-OUT-03 | |
| URS-PART11-50 | FS-PART11-50 | |
| URS-PART11-70 | FS-PART11-70 | |
| URS-PART11-100 | FS-PART11-100 | |
| URS-PART11-200 | FS-PART11-200 | |
| URS-PART11-300 | FS-PART11-300 | |
| URS-DI-01 | FS-DI-01 | |
| URS-DI-02 | FS-DI-02 | |
| URS-DI-03 | FS-DI-03 | |
| URS-DI-04 | FS-DI-04 | |
| URS-DI-05 | FS-DI-05 | |
| URS-DI-06 | FS-DI-06 | |
| URS-BAK-01 | FS-BAK-01 | |
| URS-PERF-01 | FS-PERF-01 | |
| URS-SEC-01 | FS-SEC-01 | |
| URS-SEC-02 | FS-SEC-02 | |
| URS-TRN-01 | FS-TRN-01 | |
| URS-PR-01 | FS-PR-01 | |
| URS-PR-02 | FS-PR-02 | |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Cell-protection bypass causing edited formula | Low | Critical | URS-CFG-02 + URS-CFG-07 + checksum verification on deployment (URS-LC-05) |
| R-02 | Macro re-enabled by GPO drift (and a future variant erroneously containing VBA) | Low | Critical | URS-CFG-01 + URS-CFG-06 + quarterly GPO compliance scan |
| R-03 | Workbook silently superseded but old copy used | Low | High | URS-LC-02 watermark + Vault deployment-only (URS-SEC-02) |
| R-04 | Rounding bias near tier boundary (USP <905> L1/L2; USP <711> S1/S2/S3) | Medium | High | URS-CALC-09 + edge-case OQ |
| R-05 | USP revision misses workbook update | Low | High | URS-PR-02 |
| R-06 | Saved PDF deleted | Low | Medium | URS-SEC-01 + URS-BAK-01 |
| R-07 | Locale mis-parse (comma decimal separator) on non-en-IE workstation | Low | High | URS-IV-04 |
| R-08 | Wrong sample-size used (e.g., n=12 USP <711> S2 vs n=6) | Medium | High | URS-CFG-05 |

Full eval in `LCN-RA-EXCEL-CC-001`.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
