---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "PharmaDevils Stability-PC + UV-Vis URS family"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11; EU GMP Annex 11"
  - "USP <711> Dissolution; USP <724> Drug Release"
  - "USP <1092> The Dissolution Procedure: Development and Validation"
  - "USP <1058> Analytical Instrument Qualification"
  - "USP <2040> Disintegration and Dissolution of Dietary Supplements"
  - "Ph. Eur. 2.9.3 Dissolution Test for Solid Dosage Forms"
  - "Ph. Eur. 2.9.4 Dissolution Test for Transdermal Patches"
  - "ICH Q4B Annex 7; ICH Q6A; PIC/S PI 041"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Dissolution Apparatus Computer System — Distek Evolution 6300 + ezfill 5300 + DissoTrack 5

**Document Number:** SOL-URS-DISSO-001
**Version:** 1.2
**Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Solenne Pharma SAS, QC Solid Dosage, Plant 2, Lyon, France *(fictional)*
**System Owner:** QC Manager — Solid Dosage
**Process Owner:** Head of Quality Control
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Distek Evolution 6300 + ezfill 5300 + DissoTrack 5** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a)/(d)/(e)/(k), .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .160, .165, .192, .194; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <711>; USP <724>; USP <1058>; USP <1092>; Ph. Eur. 2.9.3; Ph. Eur. 2.9.4; ICH Q4B Annex 7; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Solid Dosage) | _____________ | _____________ | _____ |
| Reviewer (IT / System Administrator) | _____________ | _____________ | _____ |
| Reviewer (Quality Assurance) | _____________ | _____________ | _____ |
| Approver (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | Authored to Tier T2 (Cat 4 dissolution apparatus with on-line / off-line readback; 65-req target). New § 5 subsections: USP <711> + <1092> compendial compliance; AIQ DQ/IQ/OQ/PQ per USP <1058>; Mechanical Qualification (MQ) per USP <711> + <1058> (paddle/basket alignment, vibration, dimensional verification); Chemical Performance Test (CPT) with USP RS prednisone tablets; media + reagent lifecycle; per-clause Part 11 + ALCOA+; multi-apparatus support (1/2 with explicit forward-looking apparatus 3/4/5/6/7 placeholders). |

## Definitions

| Term | Definition |
|---|---|
| Apparatus 1 | USP <711> rotating basket |
| Apparatus 2 | USP <711> paddle |
| Apparatus 3 | USP <711> reciprocating cylinder (Bio-Dis) |
| Apparatus 4 | USP <711> flow-through cell |
| Apparatus 5 | USP <724> paddle-over-disc (transdermals) |
| Apparatus 6 | USP <724> rotating cylinder (transdermals) |
| Apparatus 7 | USP <724> reciprocating disc / holder (transdermals + modified release) |
| Distek Evolution 6300 | Distek 6-position dissolution bath (Apparatus 1 / 2 capable; Apparatus 5/6/7 with accessory kits) |
| ezfill 5300 | Distek automated media dispensing system |
| DissoTrack 5 | Distek dissolution-management software with LIMS Connector 2.1 |
| TruAlign | Distek paddle / shaft mechanical-alignment verification fixture |
| MQ | Mechanical Qualification per USP <711> + <1058>: alignment, level, wobble, vertical distance, vibration |
| CPT | Chemical Performance Test using USP Prednisone Tablets RS (replacement for the deleted USP Calibrator Tablets) |
| S1 / S2 / S3 | USP <711> acceptance stages (n=6, n=12, n=24) |
| LIMS | LabWare LIMS 8 |
| RFC | Reason-for-change captured rationale on data modification |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| OOS | Out-of-Specification result per 21 CFR § 211.192 |

## 1. Purpose

This URS defines requirements for the dissolution-apparatus computer system used to perform USP Apparatus 1 / 2 dissolution testing for solid oral dosage release and stability programmes at Solenne Pharma Plant 2, with provision for future Apparatus 5 / 6 / 7 use on transdermal products per USP <724>. The URS binds the system to USP <711>, USP <724>, USP <1092>, USP <1058> (AIQ), Ph. Eur. 2.9.3 / 2.9.4, 21 CFR Part 11, EU GMP Annex 11, and PIC/S PI 041.

## 2. Scope

**In:** one Distek Evolution 6300 dissolution bath (6 vessels); ezfill 5300 media-dispensing system; dedicated controller workstation (HP Z2 Mini G9, Win 11 Pro 23H2) running DissoTrack 5 with LIMS Connector 2.1; LIMS integration to LabWare LIMS 8 via DataShare; AD authentication on `solenne.local`; daily backup; site NTP sync; integration with offline Agilent Cary 60 UV-Vis (separate validation `QC-CSV-2024-018`); TruAlign mechanical-alignment fixture; USP Prednisone Tablets RS for CPT; media + reagent register; vessel + paddle / basket register.

**Out:** sample preparation; UV-Vis filter wheel and spectrometer hardware (separately validated); cleaning and bath maintenance procedures (manual SOP); DissoTrack 5 SDLC (Distek-owned per Cat 4); LIMS sample-lifecycle.

## 3. System Description and Intended Use

Trained QC analysts use the system to run dissolution tests per USP <711> and <1092>. The system controls the bath (paddle / basket speed, temperature 37 °C ± 0.5 °C), automates media dispensing via ezfill, captures sample timepoints, and integrates results from the offline UV-Vis or HPLC. GAMP Cat 4: Distek maintains DissoTrack 5 SDLC; site validation focuses on installation, configuration, intended-use functionality, Part 11 controls, mechanical qualification, chemical performance test, and the LIMS / UV-Vis interfaces.

Intended use: dissolution testing of immediate-release (IR) tablets and capsules, extended-release (ER) solid oral dosage forms, and (future) transdermal patches. Out-of-scope intended uses include physiological flow-through systems for biorelevant media simulation (BioRelevant or PhysioCell) unless added under a future URS revision.

## 4. User Roles

| Role | Permissions |
|---|---|
| Analyst | Run methods; capture results; cannot edit method parameters. |
| Senior Analyst | All Analyst + second-person review. |
| Method Owner | Author / edit methods under change control. |
| QC Manager | Approve, lock, release results to LIMS. |
| System Administrator | OS / patching / AD groups; cannot approve results. |
| Mechanical Qualification Engineer | Execute MQ + CPT; cannot approve product runs. |
| Reagent Standard Custodian | Receive / log / dispose USP Prednisone RS and media reagents. |
| Auditor | Read-only across data and audit trails. |

**Separation of Duties:** Analyst ≠ Reviewer ≠ Approver; MQ Engineer ≠ QC Approver of product runs.

## 5. User Requirements

### 5.1 Hardware / Installation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HW-01 | H | R1 | The system shall be installed on a dedicated workstation; shared workstations are prohibited. |
| URS-HW-02 | H | R1 | The workstation shall meet DissoTrack 5 minimum specification (≥ 16 GB RAM, ≥ 500 GB SSD, two USB-3 ports). |
| URS-HW-03 | H | R1 | The workstation shall be on UPS for ≥ 30 min controlled shutdown. |
| URS-HW-04 | H | R1 | TruAlign mechanical-alignment verification shall be performed at installation and after any maintenance affecting paddle / basket geometry. |
| URS-HW-05 | M | R2 | Bath temperature probes shall be NIST-traceable to an accredited calibration provider; calibration evidence shall be retained. |
| URS-HW-06 | M | R2 | Vessel set, paddles, baskets shall be qualified per USP <711> dimensional requirements; dimensions logged in a vessel / paddle / basket register. |
| URS-HW-07 | M | R2 | Bath water level + degassing state shall be monitored per Distek SOP; deviations shall be logged. |

### 5.2 Software Configuration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SW-01 | H | R1 | The OS shall be Windows 11 Pro 23H2, domain-joined to `solenne.local`; QC users shall not have local-admin. |
| URS-SW-02 | H | R1 | DissoTrack 5 + LIMS Connector 2.1 shall be installed by Distek or a Distek-trained engineer. |
| URS-SW-03 | H | R1 | Project storage shall reside on `\\sol-gmp-fs01\disso-projects`; no GxP data on local C:. |
| URS-SW-04 | H | R1 | The clock shall be synced to `ntp.solenne.local`; skew shall be monitored with alert at > 1 s. |
| URS-SW-05 | M | R2 | Screen lock shall apply after 10 min idle; AD re-auth shall be required to unlock. |
| URS-SW-06 | H | R1 | DissoTrack 5 Part 11 settings (audit trail, e-sign, raw data lock) shall be configured per the Configuration Specification. |
| URS-SW-07 | M | R2 | Vendor patches (DissoTrack 5 SCN) shall be applied only after site change-control approval. |

### 5.3 USP <711> / <724> / Ph. Eur. 2.9.3 Compendial Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CMP-01 | H | R1 | The system shall support USP Apparatus 1 (basket) and Apparatus 2 (paddle) per USP <711>; future expansion to Apparatus 3 / 4 / 5 / 6 / 7 shall be enabled by software with hardware kit qualification. |
| URS-CMP-02 | H | R1 | The system shall enforce USP <711> temperature 37 °C ± 0.5 °C in each vessel during test (continuously monitored). |
| URS-CMP-03 | H | R1 | The system shall enforce paddle / basket rotation tolerance ± 4% per USP <711>. |
| URS-CMP-04 | H | R1 | The system shall evaluate S1 / S2 / S3 stage acceptance per USP <711> acceptance tables for IR and ER products; stage progression shall be tracked per run. |
| URS-CMP-05 | H | R1 | For transdermal-product use (Apparatus 5 / 6 / 7), the system shall apply USP <724> acceptance criteria. |
| URS-CMP-06 | H | R1 | The system shall meet Ph. Eur. 2.9.3 control criteria when used for EP-monograph methods; for transdermal monographs, Ph. Eur. 2.9.4 applies. |
| URS-CMP-07 | M | R2 | Compendial method designations (USP-NF, Ph. Eur., JP) shall be captured in the method header with locked rounding rules. |

### 5.4 AIQ — DQ / IQ / OQ / PQ per USP <1058>

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AIQ-01 | H | R1 | DQ shall document fitness for intended use against the product portfolio (IR + ER tablets, capsules; future transdermals). |
| URS-AIQ-02 | H | R1 | IQ shall verify installation, AD bind, DissoTrack 5 build hash, vessel set installation, paddle / basket installation, temperature-probe calibration certificates. |
| URS-AIQ-03 | H | R1 | OQ shall include: rotation accuracy (± 4% across the operating range), temperature accuracy (37 °C ± 0.5 °C), timer accuracy, ezfill dispense volume accuracy (± 1%), vibration measurement, dissolved-oxygen check per USP <711>. |
| URS-AIQ-04 | H | R1 | PQ shall execute the Chemical Performance Test (CPT) using USP Prednisone Tablets RS per USP <711> guidance, at go-live, after mechanical maintenance affecting paddle / basket / vessel, and at least annually. |
| URS-AIQ-05 | M | R2 | A partial PQ (CPT only) shall be permitted after routine PM not affecting bath alignment. |
| URS-AIQ-06 | M | R2 | Qualification evidence shall be retained ≥ 25 years per product-release tie. |

### 5.5 Mechanical Qualification (MQ) per USP <711> + <1058>

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MQ-01 | H | R1 | Paddle / basket centering (centering pin or laser) shall be ≤ 2 mm deviation from vessel center per USP <711>. |
| URS-MQ-02 | H | R1 | Paddle / basket wobble shall be ≤ 1.0 mm per USP <711>. |
| URS-MQ-03 | H | R1 | Vertical distance from vessel inside bottom to paddle / basket shall be 25 ± 2 mm per USP <711>. |
| URS-MQ-04 | H | R1 | Bath level shall be verified at MQ; level alarm shall fire on deviation. |
| URS-MQ-05 | H | R1 | Vibration shall be measured at the vessel-holder plate at all operational speeds; verified within USP <711> acceptable limits. |
| URS-MQ-06 | M | R2 | Vessel verticality shall be within ± 0.5° of plumb per USP <711>. |
| URS-MQ-07 | H | R1 | MQ shall be re-executed after any maintenance affecting paddle / basket geometry; results logged with operator + ts. |

### 5.6 Chemical Performance Test (CPT)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CPT-01 | H | R1 | The CPT shall use USP Prednisone Tablets RS at the cadence in URS-AIQ-04; acceptance criterion per current USP CPT guidance ranges (e.g., 38–63% Q at 30 min for the disintegrating-tablet RS under Apparatus 2 @ 50 rpm). |
| URS-CPT-02 | H | R1 | CPT records shall be captured with operator, ts, RS lot, certificate expiry, computed mean + RSD, acceptance verdict. |
| URS-CPT-03 | H | R1 | CPT failure shall block product runs until investigation closes; the run shall be tagged with the failing CPT record-id. |
| URS-CPT-04 | M | R2 | CPT trend shall be reviewed quarterly by QC Manager + MQ Engineer; out-of-trend pattern shall trigger MQ re-execution. |

### 5.7 Media + Reagent Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MED-01 | H | R1 | Dissolution media (buffer concentrates, surfactants, USP RS for assay readback) shall be logged with lot, source, COA, receipt date, opening date, expiry. |
| URS-MED-02 | H | R1 | The system shall block run start when bound media lot is expired. |
| URS-MED-03 | M | R2 | Prepared media (e.g. simulated gastric / intestinal fluids) shall be logged with prep date, prep analyst, pH-verification record, and short shelf-life expiry per Site SOP. |
| URS-MED-04 | M | R2 | Media degassing (per USP <711> if specified by monograph) shall be method-bound and recorded per acquisition. |
| URS-MED-05 | M | R2 | Disposal of spent media + waste shall be logged per site EHS SOP. |

### 5.8 Method and Run Execution

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-METH-01 | H | R1 | Methods shall follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE; only EFFECTIVE methods may be selected. |
| URS-METH-02 | H | R1 | Method selection from the controlled methods library shall be read-only to analysts. |
| URS-METH-03 | M | R2 | Method changes affecting apparatus, rotation, media composition, or acceptance criteria shall require re-verification per USP <1226> or re-validation per <1225>. |
| URS-RUN-01 | H | R1 | The system shall reject the start of a run if any of: bath not at 37 °C ± 0.5 °C, paddle / basket speed out of envelope, ezfill priming not confirmed, project locked, CPT overdue / failed, MQ overdue, media expired. |
| URS-RUN-02 | H | R1 | Each run shall capture: sample IDs, vessel positions, method ID + version, instrument ID, analyst, timestamp at each scheduled timepoint, media lot, paddle / basket ID. |
| URS-RUN-03 | H | R1 | Per-vessel temperature shall be recorded continuously throughout the run; deviations beyond 37 °C ± 0.5 °C shall raise alarms and be flagged in the report. |
| URS-RUN-04 | H | R1 | Manual sampling-time override shall require captured reason + supervisor signature; flagged in report. |
| URS-RUN-05 | M | R2 | Sampling-volume replacement (if method requires media replacement) shall be tracked per timepoint. |

### 5.9 Results, Calculation, Reporting

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RES-01 | H | R1 | The system shall ingest UV-Vis / HPLC results via LIMS Connector against vessel + timepoint identifiers. |
| URS-RES-02 | H | R1 | Calculations shall apply the method-defined equation set (concentration → % dissolved); rounding rules per the compendium-rounding table. |
| URS-RES-03 | H | R1 | Results shall be evaluated against the dissolution acceptance criteria (S1 / S2 / S3 per USP <711>); stage progression shall be tracked. |
| URS-RES-04 | H | R1 | The system shall generate a PDF analytical report including: sample metadata, method, analyst, reviewer, approver, per-vessel and per-timepoint values, S-stage outcome, CPT status, MQ status, ALCOA+ statement, and SHA-256 hash. |
| URS-RES-05 | M | R2 | OOS at S3 shall trigger downstream § 211.192 investigation; the LIMS sample-state shall transition to HOLD. |

### 5.10 Audit Trail / Records / Part 11 / DI

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | The audit trail shall be time-stamped, secure, and shall capture user, action, old / new value, reason. |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only; admin update / delete shall be cryptographically prevented. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be conducted by a Senior Analyst per batch and by the QC Manager monthly. |
| URS-AUD-04 | H | R1 | Retention shall be ≥ 7 y for QC records; ≥ 25 y if linked to product release. |
| URS-PART11-01 | H | R1 | The system shall implement procedural controls per 21 CFR § 11.10(a). |
| URS-PART11-02 | H | R1 | The system shall limit access to authorised individuals per § 11.10(d). |
| URS-PART11-03 | H | R1 | E-signatures shall manifest name, date / time, and meaning per § 11.50. |
| URS-PART11-04 | H | R1 | Signatures shall be linked to records per § 11.70. |
| URS-PART11-05 | H | R1 | Signatures shall be unique per § 11.100. |
| URS-PART11-06 | H | R1 | Identity-based signature components shall require re-authentication per § 11.200. |
| URS-PART11-07 | H | R1 | Password and credential controls per § 11.300 shall apply; account lock after 5 failed logins in 15 minutes. |
| URS-DI-01 | H | R1 | Records shall be Attributable. |
| URS-DI-02 | H | R1 | Records shall be Legible. |
| URS-DI-03 | H | R1 | Records shall be Contemporaneous; retrospective entries flagged. |
| URS-DI-04 | H | R1 | Original raw run data shall be preserved; reprocessing shall produce a derived record. |
| URS-DI-05 | H | R1 | Calculations shall be Accurate — verified per OQ + CPT. |
| URS-DI-06 | M | R2 | Records shall be Complete / Consistent / Enduring / Available. |

### 5.11 LIMS / UV-Vis Interfaces

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-LIMS-01 | H | R1 | Worklist import from LIMS shall be read-only via DataShare. |
| URS-INT-LIMS-02 | H | R1 | Approved results shall be pushed to LIMS only after QC Manager approval. |
| URS-INT-LIMS-03 | M | R2 | The interface shall reject result push when CPT is failed / expired or MQ is overdue. |
| URS-INT-UV-01 | H | R1 | UV-Vis result ingest shall preserve source-file pointer + hash; no manipulation of UV-Vis source data. |

### 5.12 Backup / Performance / Security / Training / PR

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | Daily backup (Veeam) with cryptographic integrity verification shall be executed. |
| URS-BAK-02 | H | R1 | A quarterly restore test shall be witnessed by QC. |
| URS-BAK-03 | M | R2 | RTO shall be ≤ 8 business hours; RPO ≤ 24 hours. |
| URS-PERF-01 | M | R2 | The workstation shall complete a typical 6-vessel multi-timepoint run without crashing or losing data. |
| URS-SEC-01 | H | R1 | Domain accounts shall be the only authentication path; local accounts disabled (except break-glass). |
| URS-SEC-02 | H | R1 | Removable media shall be blocked except for vendor-approved engineering use under change control. |
| URS-TRN-01 | H | R1 | Production access shall require recorded role-specific training (LMS); MQ + CPT execution training annual. |
| URS-PR-01 | H | R1 | An annual periodic review shall cover configuration, audit-trail review evidence, MQ + CPT trends, deviations, backup-restore, training; signed by QC Manager + Head of QA. |

### 5.13 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem; conditional-access policy `Lab-Workstation Conditional Access (MFA on interactive logon)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the dissolution result DB; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 7 y (≥ 25 y if release-linked) per the consuming-record schedule. |

## 6. Acceptance Criteria

CS, RA, IQ, OQ (rotation + temperature + timer + dispense volume + vibration + dissolved-oxygen), PQ (MQ per USP <711> + CPT with USP Prednisone Tablets RS per USP <711>) approved and executed; PQ shall include a documented S1 / S2 / S3 stage logic verification; VSR approved; RTM closed at 100% URS-ID coverage.

## 7. Constraints

- Vendor patches under change control.
- Method changes follow controlled lifecycle.
- USP Prednisone Tablets RS supply chain must remain qualified.
- Bath water for media preparation shall meet site water-quality spec.

## 8. Assumptions

- AD, LIMS, NTP, UV-Vis system, Veeam are validated.
- NIST-traceable calibration provider current.
- USP RS supply chain stable.

## 9. References

**US / FDA:**
- 21 CFR Part 11 §§ .10(a)/(b)/(c)/(d)/(e)/(k), .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .68, .160, .165, .192, .194
- FDA *Guidance on Dissolution Testing of Immediate Release Solid Oral Dosage Forms* (1997)
- FDA *Guidance on Extended Release Oral Dosage Forms* (1997)
- FDA *Guidance on Data Integrity and Compliance with cGMP* (2018)

**EU / EMA:**
- EU GMP Annex 11 §§ 4, 6, 9, 11
- Ph. Eur. 2.9.3 — Dissolution Test for Solid Dosage Forms
- Ph. Eur. 2.9.4 — Dissolution Test for Transdermal Patches
- EudraLex Volume 4 — GMP Parts I + III

**International:**
- USP <711> — Dissolution
- USP <724> — Drug Release (Transdermal Apparatus 5, 6, 7)
- USP <1058> — Analytical Instrument Qualification
- USP <1092> — The Dissolution Procedure: Development and Validation
- USP <2040> — Disintegration and Dissolution of Dietary Supplements
- USP <1225> — Validation of Compendial Procedures
- USP <1226> — Verification of Compendial Procedures
- ICH Q4B Annex 7 — Dissolution Test Evaluation and Recommendation
- ICH Q6A — Specifications: Test Procedures and Acceptance Criteria for New Drug Substances and New Drug Products
- PIC/S PI 041
- ISPE GAMP 5 (2nd Edition, 2022)

**Vendor:**
- Distek — *Evolution 6300 Dissolution Bath Configuration Reference* (current rev.)
- Distek — *ezfill 5300 Media-Dispenser Reference*
- Distek — *DissoTrack 5 Installation, Configuration, and Administration Reference*
- Distek — *DissoTrack 5 21 CFR Part 11 Compliance Guide*

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

