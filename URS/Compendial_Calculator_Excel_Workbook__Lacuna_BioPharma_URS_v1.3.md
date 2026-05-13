---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "PharmaDevils SOP-anchored Excel-validation guidance"
  - "GAMP 5 (2nd Ed., 2022) Cat 3 conventions for non-configured products"
  - "ISPE GAMP Good Practice Guide A Risk-Based Approach to Compliant GxP Computerized Systems"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11; PIC/S PI 041"
  - "USP <905>, <711>, <701>, <61>, <62>, <71>, <85>, <86>; EP 2.9.40, 2.9.3, 2.9.1, 5.1.4, 2.6.12, 2.6.13, 2.6.14"
  - "ICH Q2(R2); ICH Q4B Annex 6"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Compendial Calculator Excel Workbook — Multi-Compendial Calculation Library (Microsoft Excel 365, macros disabled)

**Document Number:** LCN-URS-EXCEL-CC-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Lacuna BioPharma DAC, QC Solid Dosage + Sterile, Cork, Ireland *(fictional)*
**System Owner:** QC Manager — Compendial Methods
**Process Owner:** Head of Quality Control
**System Class (GAMP 5, 2nd ed.):** Category 3 — Non-Configured Product (Excel, no macros, no VBA — pure formula-driven workbook used out-of-the-box; per ISPE GAMP GPG *A Risk-Based Approach to Compliant GxP Computerized Systems*, spreadsheet content is treated as a configured calculator + the surrounding workbook lifecycle is the regulated artefact.)
**Project Mode:** Configuration project on non-configurable instrument / appliance **Multi-Compendial Calculation Library (Microsoft Excel 365, macros disabled)** (GAMP 5 Category 3 — Non-Configurable COTS).
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; USP <905> Content Uniformity; USP <711> Dissolution; USP <701> Disintegration; USP <61>, <62>, <71>, <85>, <86> Microbial Limits / Sterility / Bacterial Endotoxins; EP 2.9.40, 2.9.3, 2.9.1, 5.1.4, 2.6.12, 2.6.13, 2.6.14; ICH Q2(R2); ICH Q4B Annex 6

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Compendial Methods) | _____________ | _____________ | _____ |
| Reviewer (Statistician) | _____________ | _____________ | _____ |
| Reviewer (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue — single USP <905> CU calculator. |
| 1.2 | 2026-05-12 | (synthetic) | v1.2 enrichment: tiered to T1 (30-50 reqs; this URS lands at 47 reqs). Scope expanded from a single USP <905> workbook to a multi-compendial calculator covering: USP <905> Content Uniformity, USP <711> Dissolution S1/S2/S3, USP <61>/<62>/<71>/<85>/<86> microbial limits/sterility/endotoxin, assay (% LC) and related-substances (% RS) per ICH Q2(R2). Each calculator implemented as a separate sheet within a single controlled `.xlsx`. Cat 3 (no macros) invariant preserved. Added explicit § 5 modules: spreadsheet lifecycle, cell protection + macro signing, USP compendial calculation library, formula audit-trail + version-comparison, input validation + range gating. References modernised per METHODOLOGY § 2A.1. |

## Definitions

| Term | Definition |
|---|---|
| Compendial Calculator | Pre-validated Excel workbook implementing a library of compendial calculations |
| AV | Acceptance Value (USP <905>) |
| L1 / L2 / L3 | Tier acceptance limits per USP <905> / <711> |
| RSD | Relative Standard Deviation |
| LC | Label Claim |
| RS | Related Substances |
| LOD / LOQ | Limit of Detection / Limit of Quantitation |
| EDMS | Veeva Vault QualityDocs |
| LIMS | LabWare LIMS 8 |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the Compendial Calculator — a controlled Excel workbook used by QC analysts to compute compendial acceptance values from individual test results during in-process and finished-product testing. The workbook implements a library of compendial calculations spanning USP <905> Content Uniformity, USP <711> Dissolution Stages S1/S2/S3, USP <61>/<62>/<71>/<85>/<86> microbial / sterility / endotoxin compendial acceptance, plus the % Label Claim (assay) and % Related Substances calculations per ICH Q2(R2).

The workbook is **GAMP Category 3** because it is a non-configured product: a vendor-supplied spreadsheet engine (Excel 365, macros disabled) with site-authored formula content but no scripting, VBA, or add-ins. Validation effort is proportionate per ISPE GAMP 5 (2nd ed.) §6 and the ISPE GAMP GPG *A Risk-Based Approach to Compliant GxP Computerized Systems*.

## 2. Scope

**In scope:** the controlled Excel workbook (`LCN-CALC-CC-v1.0.xlsx`) hosted in Veeva Vault QualityDocs as a controlled document; the deployment process (Vault → controlled local copies opened read-only by analysts); the workbook lifecycle (draft / review / approved / effective / superseded); training of users; QC-procedure integration. The workbook contains separate sheets per compendial calculation: `Calc-USP905`, `Calc-USP711-Disso`, `Calc-USP61-62-Microbial`, `Calc-USP71-Sterility`, `Calc-USP85-86-Endotoxin`, `Calc-Assay-LC`, `Calc-RS`.

**Out of scope:** Excel itself (vendor-managed; Cat-1-style infrastructure assurance); LIMS sample-lifecycle handling; results entry into LIMS (manual transcription with second-person verification — separate SOP).

## 3. System Description and Intended Use

The workbook accepts per-method input ranges (assay results, dissolution Q values, individual-unit assay results, microbial counts, endotoxin EU/mL), applies the compendial equations per sheet, and reports tier disposition (L1/L2/L3 where applicable) or pass/fail per the relevant compendial decision tree. Cells are protected; only the input cells are editable. The workbook emits a printable PDF with a snapshot signature page recording analyst, reviewer, batch ID, method, timestamp, and a workbook-version checksum.

Macros are disabled across the site Excel deployment (Group Policy); the workbook contains no VBA, ActiveX, or external connections. This eliminates a class of risk and keeps the validation surface minimal.

## 4. User Roles

| Role | Permissions |
|---|---|
| Analyst | Open read-only copy; enter individual-unit results; produce signed PDF. |
| Senior Analyst | Second-person review of input values vs. source data. |
| Method Owner | Author / revise the workbook under change control. |
| Method Approver (QA) | Approve the workbook to EFFECTIVE. |
| QC Manager | Approve the calculator-produced result alongside the LIMS result. |
| EDMS Administrator | Manage the Vault lifecycle of the workbook; cannot author. |
| Auditor | Read-only across workbook revisions, audit trails, and produced PDFs. |

Separation of duties: Method Author ≠ Method Approver; Analyst ≠ Reviewer ≠ Approver of the same calculator output.

## 5. User Requirements

### 5.1 Spreadsheet Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LC-01 | H | R1 | The workbook shall follow the lifecycle DRAFT → IN-REVIEW → APPROVED → EFFECTIVE → SUPERSEDED in Vault QualityDocs. |
| URS-LC-02 | H | R1 | Only EFFECTIVE versions shall be downloadable for production use; older versions shall be watermarked SUPERSEDED on download. |
| URS-LC-03 | H | R1 | Lifecycle transitions shall require role-restricted electronic signatures with separation of duties. |
| URS-LC-04 | H | R1 | EFFECTIVE versions shall be immutable; changes (formula correction, USP revision, sampling-plan update) shall create a new revision via change control. |
| URS-LC-05 | H | R1 | Each EFFECTIVE version shall carry a documented SHA-256 checksum printed on the workbook's "About" sheet and recorded in the Vault metadata. |

### 5.2 Workbook Configuration, Cell Protection, Macro Signing

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CFG-01 | H | R1 | The site Excel deployment shall have macros disabled by Group Policy; the workbook shall not contain VBA, ActiveX, or external connections. |
| URS-CFG-02 | H | R1 | All cells except designated input cells shall be cell-locked; the worksheet shall be sheet-protected without a user password (vendor-only password to prevent inadvertent editing — not a security control). |
| URS-CFG-03 | H | R1 | The workbook shall display its version, checksum, and "EFFECTIVE / SUPERSEDED" status at the top of every printed page. |
| URS-CFG-04 | H | R1 | Input cells shall enforce Excel data-validation: numeric only, within plausible range, mandatory for the configured sampling plan. |
| URS-CFG-05 | H | R1 | Per-sheet sample-size gating shall enforce the compendial sample-size per stage (e.g., USP <905> Stage 1 n=10 / Stage 2 n=30; USP <711> S1 n=6 / S2 n=6 / S3 n=12; USP <61> ≥1 g sample per Test 1.2.1); alternative sample sizes shall be blocked. |
| URS-CFG-06 | H | R1 | The workbook shall NOT contain digitally-signed macros — macros are prohibited entirely. If any future variant requires macros, that variant shall be re-classified as Cat 4 with an explicit FS for digital-signature trust + Trust-Center configuration. |
| URS-CFG-07 | H | R1 | Workbook-structure protection shall prevent un-hiding of `Constants` / `Validation` sheets. |

### 5.3 USP Compendial Calculation Library

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CALC-01 | H | R1 | The `Calc-USP905` sheet shall compute mean, deviation, and acceptance value (AV) per USP <905> Stage 1 + Stage 2 equations and shall report L1 (Stage 1 pass), Stage-2 required, L2 (overall pass), or fail per the USP <905> decision tree. |
| URS-CALC-02 | H | R1 | The `Calc-USP711-Disso` sheet shall implement USP <711> dissolution Stages S1 (n=6), S2 (n=6, total n=12), S3 (n=12, total n=24); shall compute per-stage acceptance per the Q-value criterion (S1: each ≥ Q+5 %; S2: average ≥ Q + each ≥ Q−15 %; S3: average ≥ Q + ≤ 2 below Q−15 % + none below Q−25 %); shall report S1/S2/S3 disposition. |
| URS-CALC-03 | H | R1 | The `Calc-USP61-62-Microbial` sheet shall implement USP <61> Total Aerobic Microbial Count + Total Yeasts and Molds Count + USP <62> Tests for Specified Microorganisms; shall apply the compendial limits per dosage form (e.g., oral non-aqueous: TAMC ≤ 10³ CFU/g; TYMC ≤ 10² CFU/g; absence of E. coli per gram). |
| URS-CALC-04 | H | R1 | The `Calc-USP71-Sterility` sheet shall implement USP <71> Membrane Filtration / Direct Inoculation pass/fail evaluation including method-suitability evidence reference. |
| URS-CALC-05 | H | R1 | The `Calc-USP85-86-Endotoxin` sheet shall implement USP <85> Bacterial Endotoxins (Gel-Clot Limit / Photometric Methods) + USP <86> Pyrogen Test (rabbit) evaluation; shall enforce the endotoxin limit per dosage form (e.g., parenteral non-intrathecal: EL = 5 EU/(kg·h × M)). |
| URS-CALC-06 | H | R1 | The `Calc-Assay-LC` sheet shall compute % Label Claim from peak-response + reference-standard potency + dilution factors per ICH Q2(R2); shall report % LC against the monograph acceptance range. |
| URS-CALC-07 | H | R1 | The `Calc-RS` sheet shall compute % Related Substances (each individual impurity + total RS) using either external standard or area-percent method per ICH Q3A(R2) / Q3B(R2) thresholds; shall flag impurities exceeding identification / qualification thresholds. |
| URS-CALC-08 | H | R1 | Rounding rules shall follow the site's documented rounding SOP `LCN-SOP-QC-ROUND-001`; rounding shall occur only at the final reported value (intermediate values use full precision). |
| URS-CALC-09 | H | R1 | No calculation shall round in a way that biases the result across a tier boundary (L1/L2/L3 of USP <905> / <711>); OQ shall verify edge-case behaviour. |

### 5.4 Input Validation and Range Gating

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-IV-01 | H | R1 | Each calculator sheet shall enforce numeric input validation (Excel data validation) with sheet-specific plausible-range bounds (e.g., USP <905>: 50 %–150 % of label claim; USP <711>: 0 %–110 % of Q; microbial: 0–10⁸ CFU/g; endotoxin: 0–10⁴ EU/mL). |
| URS-IV-02 | H | R1 | Missing inputs shall be highlighted and shall block calculation (`#N/A` propagation with explicit user warning). |
| URS-IV-03 | H | R1 | The workbook shall not silently accept text entries in numeric cells; text entry shall trigger an Excel validation-error dialog. |
| URS-IV-04 | M | R2 | Locale-dependent decimal separators shall be normalized per the site locale config `en-IE`; OQ shall verify behaviour under alternative locales does not silently mis-parse. |

### 5.5 Formula Audit-Trail and Version Comparison

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AT-01 | H | R1 | Every formula in scope (calculation sheets) shall be inventoried in the validation `Validation` sheet with: cell reference, formula text, expected output type, reference test-case ID. |
| URS-AT-02 | H | R1 | Workbook-to-workbook version comparison shall be supported via the `xlsxinspect` script comparing formula text + cell protection + named ranges across versions; the comparison report shall be appended to each new revision's validation record. |
| URS-AT-03 | H | R1 | Vault-side audit trail shall capture every lifecycle transition + download with user / timestamp / signature per EU GMP Annex 11 § 9. |

### 5.6 Output, Audit, and Records

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-OUT-01 | H | R1 | Output shall be a printable PDF/A-3 including: batch ID, method ID + version, individual results, computed acceptance value (or per-stage disposition for dissolution), final disposition, workbook version + checksum, analyst, reviewer, approver, timestamps. |
| URS-OUT-02 | H | R1 | The PDF shall be saved to a controlled folder (`\\lcn-gmp-fs01\compendial-calc-output`) read-only after save; the folder is part of the GxP-server backup scope (Veeam). |
| URS-OUT-03 | H | R1 | The result shall be transcribed into LIMS by the Analyst with second-person verification (separate SOP); the LIMS result shall reference the saved PDF filename + checksum. |

### 5.7 21 CFR Part 11

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-50 | H | R1 | Workbook lifecycle signatures (Vault) shall meet § 11.50: printed name, date / time, meaning. |
| URS-PART11-70 | H | R1 | Vault signatures shall be cryptographically bound to the document hash per § 11.70. |
| URS-PART11-100 | H | R1 | Each Vault signature shall be unique to an individual; no reuse / reassignment per § 11.100. |
| URS-PART11-200 | H | R1 | Re-authentication shall be required at Vault signing per § 11.200. |
| URS-PART11-300 | H | R1 | Password and credential controls shall meet § 11.300. |

### 5.8 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | Records shall be Attributable to a named user (analyst on the PDF; signers in Vault). |
| URS-DI-02 | H | R1 | Records shall be Legible — the PDF/A-3 is a fixed-format readable artefact; the source `.xlsx` is not a record (it is a calculator). |
| URS-DI-03 | H | R1 | Records shall be Contemporaneous — the PDF is generated at the time of the calculation; analyst dates / signs immediately. |
| URS-DI-04 | H | R1 | Originals (the analyst's individual results) shall be preserved in LIMS unaltered; the workbook does not modify source data. |
| URS-DI-05 | H | R1 | Calculations shall be Accurate — verified per OQ over the L1 / L2 / L3 decision boundaries + the microbial / endotoxin limit edges. |
| URS-DI-06 | M | R2 | Complete / Consistent / Enduring (≥ 7-yr PDF retention; ≥ 25-yr if linked to product release) / Available. |

### 5.9 Backup, Performance, Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | The output folder shall be in scope of the site backup system (`AUR-URS-BACKUP-001`). |
| URS-PERF-01 | L | R3 | Workbook open / calculate / PDF-export shall complete ≤ 5 seconds for a typical 30-unit input. |
| URS-SEC-01 | H | R1 | Output folder ACLs shall allow Analyst write-once; no user can delete or modify saved PDFs (NTFS deny-modify, deny-delete except for archive process). |
| URS-SEC-02 | H | R1 | Deployment from Vault to local copies shall use only the EDMS download mechanism; out-of-band copies are prohibited. |

### 5.10 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Production use shall require recorded role-specific training in the LMS, including a competency assessment with worked examples per calculator sheet. |
| URS-PR-01 | H | R1 | Annual periodic review covering USP / EP revision status, workbook version status, deviation summary, training currency, fitness for use; signed by QC Manager + Head of QA. |
| URS-PR-02 | M | R2 | When a USP / EP revision is published affecting an in-scope monograph, the workbook shall be impact-assessed within 90 days. |

### 5.11 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is AD-joined workstation interactive Kerberos authentication with site GPO `URS-GPO-03` macro-block path; conditional-access policy `Standard-User Conditional Access (workstation compliance + GPO macro-block)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T3 with RPO ≤ 72 h and RTO ≤ 72 BH; backup integration shall use Veeam file-level capture of the controlled workbook master copy and the per-calculation evidence packages on the SharePoint site library; the application team shall participate in annual application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 7 y (computation-evidence record) per the consuming-record schedule. |

## 6. Acceptance Criteria

The system shall be accepted into validated GMP use when:
1. CS, RA, IQ (vendor-shared Excel infra), OQ (calculation verification across each calculator sheet's decision space + edge cases — USP <905> L1/L2 boundary, USP <711> S1/S2/S3 boundaries, microbial / endotoxin limit edges, assay specification edge), PQ (representative end-to-end batch through Vault → analyst → PDF → LIMS for ≥ 3 calculator sheets) approved and executed.
2. The workbook checksum is recorded in the Vault metadata and verified at deployment.
3. VSR approved by QC Manager + Head of QA.
4. RTM maps every URS-ID to ≥ 1 approved test case.

## 7. Constraints

- The workbook is Cat 3; no VBA, no macros, no external data connections, no add-ins. Adding any of these triggers re-classification (likely Cat 4 or Cat 5).
- The workbook is not a record; the record is the saved PDF and the LIMS entry. The `.xlsx` source is treated as a controlled tool.
- The LIMS transcription with second-person verification is the controlling result-entry path.

## 8. Assumptions

- Microsoft Excel 365 is itself a Cat-1 commodity infrastructure component covered under the site IT-asset assurance program.
- Veeva Vault QualityDocs, LIMS, and the backup system are validated.
- The site Group Policy disabling macros is enforced on every workstation that opens the workbook.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .67, .166, .192

### EU / EP
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EP 2.9.40 Uniformity of Dosage Units
- EP 2.9.3 Dissolution Test for Solid Dosage Forms
- EP 2.9.1 Disintegration of Tablets and Capsules
- EP 5.1.4 Microbiological Quality of Non-Sterile Pharmaceutical Preparations
- EP 2.6.12 Microbiological Examination of Non-Sterile Products: Microbial Enumeration
- EP 2.6.13 Tests for Specified Microorganisms
- EP 2.6.14 Bacterial Endotoxins

### Pharmacopoeial — USP
- USP <905> Uniformity of Dosage Units
- USP <711> Dissolution
- USP <701> Disintegration
- USP <61> Microbiological Examination of Non-Sterile Products: Microbial Enumeration Tests
- USP <62> Microbiological Examination of Non-Sterile Products: Tests for Specified Microorganisms
- USP <71> Sterility Tests
- USP <85> Bacterial Endotoxins Test
- USP <86> Pyrogen Test

### International — ICH
- ICH Q2(R2) — Validation of Analytical Procedures
- ICH Q3A(R2) — Impurities in New Drug Substances
- ICH Q3B(R2) — Impurities in New Drug Products
- ICH Q4B Annex 6 — Compendial Harmonisation: Uniformity of Dosage Units

### Industry guidance — ISPE / PIC/S
- ISPE GAMP 5 (2nd Ed., 2022) — Category 3 conventions
- ISPE GAMP Good Practice Guide *A Risk-Based Approach to Compliant GxP Computerized Systems* (spreadsheet validation)
- PIC/S PI 041 — Good Practices for Data Management and Integrity
- Internal: Lacuna SOP `LCN-SOP-CSV-EXCEL-001` Excel Workbook Validation

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

