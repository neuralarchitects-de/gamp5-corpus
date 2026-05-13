---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "PharmaDevils QC instrument URS family"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11; EU GMP Annex 11"
  - "USP <1119> Near-Infrared Spectroscopy"
  - "USP <856> Near-Infrared Spectroscopy — Theory and Practice"
  - "USP <1058> Analytical Instrument Qualification"
  - "Ph. Eur. 2.2.40 Near-Infrared Spectroscopy"
  - "EMA Guideline on the use of Near Infrared Spectroscopy by the Pharmaceutical Industry (EMA/CHMP/CVMP/QWP/17760/2009 Rev 1, 2014)"
  - "ICH Q2(R2); ICH Q14; ICH Q8(R2); ICH Q9(R1); PIC/S PI 041"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## NIR Spectrometer Computer System — Bruker MPA II + OPUS 8.7

**Document Number:** KSP-URS-NIR-001
**Version:** 1.2
**Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Kestrel Pharma NV, Goods Receipt — Raw Materials, Antwerp, Belgium *(fictional)*
**System Owner:** Goods-Receipt QC Manager
**Process Owner:** Head of Supply Quality
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (chemometric models are Cat 5 sub-components authored under change control)
**Project Mode:** Configuration project on commercial software product **Bruker MPA II + OPUS 8.7** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a)/(d)/(e)/(k), .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .84, .160, .165, .194; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <1119>; USP <856>; USP <1058>; Ph. Eur. 2.2.40; EMA NIR Guideline (2014); ICH Q2(R2); ICH Q14; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Goods-Receipt QC Manager) | _____________ | _____________ | _____ |
| Reviewer (Chemometrics Lead) | _____________ | _____________ | _____ |
| Reviewer (IT / System Administrator) | _____________ | _____________ | _____ |
| Reviewer (Quality Assurance) | _____________ | _____________ | _____ |
| Approver (Head of Supply Quality) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Range-compression removed; per-ID Part 11 + DI breakouts. |
| 1.2 | 2026-05-12 | (synthetic) | Authored to Tier T2 (Cat 4 platform + Cat 5 chemometric sub-components; 65-req target; spans USP <1119> performance qualification + Ph. Eur. 2.2.40 monograph compliance + EMA NIR Guideline 2014 model lifecycle + chemometric model registry under ICH Q14 + AIQ DQ/IQ/OQ/PQ per USP <1058>). New § 5 subsections: USP/Ph. Eur. compendial compliance; AIQ + mechanical/optical qualification; system-suitability test battery; chemometric model lifecycle (PCA/PLS, ICH Q14 ATP linkage); reference standard + traceability mgmt; sample-presentation controls; per-clause Part 11 + ALCOA+. |

## Definitions

| Term | Definition |
|---|---|
| NIR | Near-Infrared spectroscopy (typical pharma range 780–2500 nm / 12 800–4000 cm⁻¹) |
| MPA II | Bruker Optics Multi-Purpose Analyzer II — FT-NIR spectrometer |
| OPUS 8.7 | Bruker Optics OPUS software v8.7 with IDENT, QUANT, and Validation modules |
| Library / Model | Chemometric NIR identification or quantitative model (typical: SIMCA, PCA, PLS, PLS-DA) |
| Chemometric model | A multivariate statistical model relating NIR spectra to identity or to a quantitative attribute (assay, moisture, blend uniformity) |
| ATP | Analytical Target Profile per ICH Q14 — pre-defined quality attributes the procedure must measure |
| PAT | Process Analytical Technology per ICH Q8(R2) / FDA PAT framework |
| ID | Identity (test per USP / Ph. Eur. monograph identification series) |
| SIMCA | Soft Independent Modelling of Class Analogies — distance-to-model classification |
| PLS / PCA | Partial Least Squares / Principal Component Analysis |
| LIMS | LabWare LIMS 8 |
| RFC | Reason-for-change captured rationale on data modification |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| OOS | Out-of-Specification result triggering investigation per 21 CFR § 211.192 |

## 1. Purpose

This URS defines requirements for the NIR spectrometer computer system used to perform identity testing of incoming raw materials at the Kestrel Pharma goods-receipt area, in lieu of compendial wet-chemistry identity testing per 21 CFR § 211.84(d) where the NIR identification model has been validated and approved for that material under USP <1119>, Ph. Eur. 2.2.40, and the EMA NIR Guideline (2014). The URS also enables future expansion to quantitative NIR applications (moisture, assay, blend uniformity) under the same chemometric-lifecycle controls.

## 2. Scope

**In:** one Bruker MPA II FT-NIR spectrometer; dedicated workstation (HP Z2 Mini G9, Windows 11 Pro 23H2) running OPUS 8.7 with the IDENT + QUANT + Validation modules; chemometric library / model registry under change control; barcode reader (Honeywell Voyager 1452g); AD authentication on `kestrel.local`; LIMS integration via OPUS LIMS Connector 3; daily backup; NTP sync; USP <1119> performance-qualification test battery; reference standards (NIST SRM 1920a wavelength polystyrene, USP / Ph. Eur. chemical reference substances).

**Out:** sample preparation (manual SOP); model-development environment (separate offline workstation under chemometrics SOP); LIMS sample lifecycle; production PAT integration (separate URS); OPUS SDLC (Bruker-owned per GAMP Cat 4).

## 3. System Description and Intended Use

The system performs NIR identification of incoming raw materials. Trained Goods-Receipt analysts scan the material barcode, present the sample (vial, fibre-optic probe, or integrating sphere depending on material class), run the configured chemometric model, and the system reports Pass / Fail per pre-validated thresholds. Quantitative methods (e.g. moisture by PLS) may be added under the same chemometric-lifecycle controls. The chemometric library is updated under change control; each library / model revision is a Cat 5 sub-component with documented validation per ICH Q2(R2) and EMA NIR Guideline (2014). GAMP Cat 4 platform: Bruker maintains OPUS SDLC; site validation focuses on installation, configuration, intended-use, Part 11, integrations, and the chemometric lifecycle.

## 4. User Roles

| Role | Permissions |
|---|---|
| Goods-Receipt Analyst | Acquire spectra; run identification; cannot edit models or system config. |
| Senior Analyst | All Analyst + second-person verification on borderline / failed identifications. |
| Chemometrics Engineer | Author / revise models in development environment; cannot deploy to production alone. |
| Chemometrics Approver (QA) | Co-approve model deployment to production. |
| QC Manager | Approve identification reports for material release; release to LIMS. |
| System Administrator | OS / patch / AD groups; cannot approve identifications or deploy models. |
| Reference Standard Custodian | Receive / log / dispose reference standards; cannot run identifications. |
| Auditor | Read-only across data and audit trails. |

**Separation of Duties:** Chemometrics Engineer ≠ Chemometrics Approver of own model; Analyst ≠ Reviewer ≠ Approver; System Administrator ≠ QC Approver; Chemometrics Engineer ≠ QC Manager.

## 5. User Requirements

### 5.1 Hardware / Installation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HW-01 | H | R1 | The system shall be installed on a dedicated workstation; shared workstations are prohibited. |
| URS-HW-02 | H | R1 | The workstation shall meet OPUS 8.7 minimum specification per the Bruker installation reference. |
| URS-HW-03 | H | R1 | The workstation shall be backed by a UPS sized for ≥ 30 min controlled shutdown. |
| URS-HW-04 | H | R1 | The instrument shall meet USP <1119> performance qualification (wavelength accuracy, photometric noise, photometric linearity, signal-to-noise) per a documented schedule. |
| URS-HW-05 | M | R2 | The Bruker MPA II shall be sited per vendor environmental envelope (15–30 °C; 20–80% RH non-condensing) with continuous environmental monitoring. |
| URS-HW-06 | M | R2 | The fibre-optic probe / integrating-sphere / sample-vial accessory shall be qualified per Bruker SOP at installation and after any servicing. |

### 5.2 Software Configuration (per GAMP Cat 4)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SW-01 | H | R1 | The OS shall be Windows 11 Pro 23H2, domain-joined to `kestrel.local`. |
| URS-SW-02 | H | R1 | OPUS 8.7 + IDENT + QUANT + Validation modules shall be installed by Bruker or by a Bruker-trained engineer. |
| URS-SW-03 | H | R1 | Project storage shall reside on `\\kst-gmp-fs01\nir-projects`; no GxP data shall be retained on local C:. |
| URS-SW-04 | H | R1 | The clock shall be synced to `ntp.kestrel.local`; skew shall be monitored with alert at > 1 s. |
| URS-SW-05 | H | R1 | OPUS Part 11 settings (audit trail required, e-sign required, raw data lock, project security) shall be configured per site policy and captured in the Configuration Specification. |
| URS-SW-06 | M | R2 | Vendor patches (Bruker OPUS revisions) shall be applied only after site change-control approval. |

### 5.3 USP / Ph. Eur. / EMA Compendial Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CMP-01 | H | R1 | The instrument shall meet USP <1119> wavelength accuracy criterion ± 1 nm in the 780–2500 nm range using NIST SRM 1920a polystyrene or rare-earth-oxide reference. |
| URS-CMP-02 | H | R1 | The instrument shall meet USP <1119> photometric noise ≤ specification (typical RMS noise ≤ 30 µAU at 1.0 A across the working range). |
| URS-CMP-03 | H | R1 | The instrument shall meet USP <1119> photometric linearity criteria across the working range using NIST-traceable transmittance standards. |
| URS-CMP-04 | H | R1 | The instrument shall meet Ph. Eur. 2.2.40 control tests when used for EP-monograph methods. |
| URS-CMP-05 | H | R1 | NIR identification methods shall be authored per the EMA NIR Guideline (EMA/CHMP/CVMP/QWP/17760/2009 Rev 1, 2014) including specification of variable selection, spectral pre-processing, classification thresholds, and reference-method correlation. |
| URS-CMP-06 | M | R2 | Quantitative NIR methods shall be authored with the ATP defined per ICH Q14 and validated per ICH Q2(R2) accuracy / precision / specificity / linearity / range / robustness criteria. |
| URS-CMP-07 | M | R2 | Compendial method designations (USP-NF, Ph. Eur., JP) shall be captured in the method header. |

### 5.4 AIQ — DQ / IQ / OQ / PQ per USP <1058>

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AIQ-01 | H | R1 | Design Qualification shall document fitness for intended use against the wavelength range, sampling accessories, chemometric model classes, and Part 11 integration. |
| URS-AIQ-02 | H | R1 | Installation Qualification shall verify physical installation, network / AD integration, software build hash, optical alignment, source replacement record. |
| URS-AIQ-03 | H | R1 | Operational Qualification shall include: wavelength accuracy + repeatability, photometric noise + linearity, signal-to-noise, scan reproducibility, resolution. |
| URS-AIQ-04 | H | R1 | Performance Qualification shall be executed at go-live, on major change (source replacement, detector service, software upgrade, sampling-accessory change), and annually. |
| URS-AIQ-05 | M | R2 | A partial PQ (SST only) shall be permitted after planned maintenance not affecting the optical bench. |
| URS-AIQ-06 | M | R2 | Qualification evidence shall be retained ≥ 25 years per product-release tie. |

### 5.5 System Suitability Test (SST) Battery

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SST-01 | H | R1 | An SST battery shall be executed at the cadence in URS-SW-* and shall include: wavelength accuracy (polystyrene or rare-earth standard), photometric noise (open beam or 99% reflectance ceramic), signal-to-noise (background), and instrument warm-up verification. |
| URS-SST-02 | H | R1 | SST records shall be captured with operator identity, timestamp, reference-standard ID, certificate expiry, and pass / fail evaluation against USP <1119> criteria. |
| URS-SST-03 | H | R1 | An SST failure shall set the instrument to NOT READY; the system shall block GxP acquisitions until SST is re-passed. |
| URS-SST-04 | M | R2 | The system shall trend SST results across rolling 12 months and alert on drift exceeding ½ of the USP <1119> acceptance limit. |
| URS-SST-05 | M | R2 | Periodic SST review shall be a documented step in the monthly audit-trail review. |

### 5.6 Chemometric Model Lifecycle (Cat 5 sub-components)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MODEL-01 | H | R1 | Each NIR identification or quantitative model shall have a documented Model Card including training-set composition, calibration / validation statistics, threshold rules, spectral pre-processing, variable selection, factor count, and known limitations. |
| URS-MODEL-02 | H | R1 | A new model shall not be deployed unless validated against the locked validation set per ICH Q2(R2) and per the EMA NIR Guideline (2014); approval requires Chemometrics Approver + QC Manager co-sign. |
| URS-MODEL-03 | H | R1 | Deployed models shall be cryptographically hashed; OPUS shall verify hash before use and shall block on hash mismatch. |
| URS-MODEL-04 | H | R1 | Model retraining triggers (drift detected, new supplier qualified, new grade introduced, OOS rate exceeding alert threshold) shall be documented and audit-trailed. |
| URS-MODEL-05 | H | R1 | Model performance shall be trended (false-pass / false-fail rate, distance-to-model statistics, residual variance) and reviewed quarterly by the Chemometrics Lead. |
| URS-MODEL-06 | H | R1 | Reference-method correlation (NIR vs HPLC / Karl Fischer / wet-chemistry per EMA NIR Guideline § 2.4) shall be re-verified at model deployment and at periodic review. |
| URS-MODEL-07 | M | R2 | A model retirement workflow shall be defined: superseded models are flagged READ-ONLY but retained for traceability of historical records. |
| URS-MODEL-08 | M | R2 | Out-of-specification (out-of-model-space) spectra shall be flagged automatically by SIMCA distance / PLS Hotelling T² + Q residual thresholds. |
| URS-MODEL-09 | M | R2 | The development → validation → production model promotion path shall be enforced: production environment cannot import models that have not transited the validation environment. |

### 5.7 Reference Standard and Traceability Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REF-01 | H | R1 | Reference standards (NIST SRM 1920a polystyrene, rare-earth-oxide wavelength standard, transmittance standards, USP / Ph. Eur. CRS for identity verification) shall be logged with lot, source, COA, NIST-traceability flag, receipt date, opening date, expiry. |
| URS-REF-02 | H | R1 | The system shall block use of an expired reference standard at SST start. |
| URS-REF-03 | M | R2 | The Reference Standard Custodian shall maintain a register integrated with OPUS such that SST execution captures the reference-standard ID. |
| URS-REF-04 | M | R2 | Reference standard re-qualification (where permitted) shall require QA approval. |

### 5.8 Sample Presentation Controls

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SAMP-01 | H | R1 | Each sample-presentation mode (vial, fibre-optic probe, integrating sphere) shall be method-bound; the wrong accessory shall be detected at acquisition and shall block the run. |
| URS-SAMP-02 | M | R2 | Method-execution shall capture sample-presentation mode, vial / probe ID, and accessory serial number per acquisition. |
| URS-SAMP-03 | M | R2 | Fibre-optic probe contamination / scratching shall be checked at SST cadence via reference-spectrum overlay. |

### 5.9 Acquisition / Identification

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ACQ-01 | H | R1 | The system shall scan the material barcode and shall link the spectrum to material code + lot. |
| URS-ACQ-02 | H | R1 | The system shall reject the start of a measurement if instrument PQ / SST is overdue, no approved model is available, or the project is locked. |
| URS-ACQ-03 | H | R1 | Each spectrum captured shall include material code, lot, model ID + version, instrument ID, analyst, sample-presentation mode, accessory ID, timestamp. |
| URS-ID-01 | H | R1 | Identification result shall be Pass / Fail per the model's threshold; borderline / fail outcomes shall route to Senior Analyst for second-person verification. |
| URS-ID-02 | H | R1 | A failed identification shall block release of the material lot in LIMS until disposition. |
| URS-ID-03 | M | R2 | An out-of-model-space spectrum (per URS-MODEL-08) shall be flagged as inconclusive and shall not be reported as Pass. |

### 5.10 Audit Trail / Part 11 / DI

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | The audit trail shall be time-stamped, secure, and shall cover spectra, methods, models, deployments, configuration, and signature events. |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only; admin update / delete shall be cryptographically prevented at the application layer. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be conducted by a Senior Analyst per session and by the QC Manager monthly. |
| URS-AUD-04 | H | R1 | Audit-trail retention shall be ≥ 7 years; ≥ 25 years if linked to product release. |
| URS-PART11-01 | H | R1 | The system shall implement procedural and operational controls protecting electronic-record validity per 21 CFR § 11.10(a). |
| URS-PART11-02 | H | R1 | The system shall limit access to authorised individuals per § 11.10(d) via AD-mapped role bindings. |
| URS-PART11-03 | H | R1 | E-signatures shall manifest name, date / time, and meaning per § 11.50. |
| URS-PART11-04 | H | R1 | Signatures shall be cryptographically linked to records per § 11.70. |
| URS-PART11-05 | H | R1 | Signatures shall be unique per § 11.100; reuse / reassignment shall be prevented. |
| URS-PART11-06 | H | R1 | Identity-based signature components shall require re-authentication at signing per § 11.200. |
| URS-PART11-07 | H | R1 | Password and credential controls per § 11.300 shall apply (min length 12; complexity; rotation ≤ 90 d; lockout 5 attempts). |
| URS-DI-01 | H | R1 | Data shall be Attributable (operator + role captured per event). |
| URS-DI-02 | H | R1 | Data shall be Legible (reports + audit trails render in human-readable form). |
| URS-DI-03 | H | R1 | Data shall be Contemporaneous (NTP timestamps; manual entry prohibited). |
| URS-DI-04 | H | R1 | Data shall be Original (raw spectra preserved unaltered; derived results trace back). |
| URS-DI-05 | H | R1 | Data shall be Accurate (SST status gates the run; model hash verified). |
| URS-DI-06 | M | R2 | Data shall be Complete / Consistent / Enduring / Available throughout the retention period. |

### 5.11 LIMS Interface

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-LIMS-01 | H | R1 | Worklists shall be imported from LIMS via the OPUS Connector (read-only). |
| URS-INT-LIMS-02 | H | R1 | Approved Pass / Fail results shall be pushed to LIMS only after QC Manager approval. |
| URS-INT-LIMS-03 | H | R1 | Each LIMS-bound result shall include spectrum hash, model ID + version, instrument ID, reviewer / approver. |
| URS-INT-LIMS-04 | M | R2 | The interface shall reject result push when SST is failed / expired. |

### 5.12 Backup / Performance / Security / Training / PR

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | Daily backup with checksum shall be executed; backed-up artefacts include spectra, methods, model registry, audit trails, reference-standard register. |
| URS-BAK-02 | H | R1 | A quarterly restore test shall be witnessed and recorded. |
| URS-PERF-01 | M | R2 | Identification time shall be ≤ 60 seconds per measurement at the 95th percentile. |
| URS-SEC-01 | H | R1 | Domain accounts shall be the only authentication path; no local accounts except break-glass. |
| URS-SEC-02 | H | R1 | Removable media shall be blocked except for vendor-approved engineering use under change control. |
| URS-TRN-01 | H | R1 | LMS-recorded role-specific training shall be required; chemometric-model-execution training shall be re-qualified annually. |
| URS-PR-01 | H | R1 | An annual periodic review shall cover model registry, drift trends, identification false-pass / false-fail rate, deviations, SST trend, and training currency; signed by QC Manager + Head of QA. |

### 5.13 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem; conditional-access policy `Lab-Workstation Conditional Access (MFA on interactive logon)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the NIR result DB plus file-level capture of model files and chemometric calibrations; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 7 y (≥ 25 y if release-linked) per the consuming-record schedule. |

## 6. Acceptance Criteria

CS, RA, IQ, OQ (USP <1119> battery + USP <1058> mechanical / optical), PQ (including representative chemometric model deployment under the Cat 5 sub-component lifecycle and an ID failure scenario blocking material release) approved and executed; VSR approved; RTM closed at 100% URS-ID coverage.

## 7. Constraints

- Model retraining + redeployment is change-controlled with Chemometrics Approver + QC Manager co-sign.
- Vendor patches under change control.
- The EMA NIR Guideline (2014) is the governing guideline for any NIR-replaces-wet-chemistry identification.

## 8. Assumptions

- AD, LIMS, NTP are validated upstream.
- Reference materials (NIST SRMs, USP / Ph. Eur. CRS) are available and supply chain is stable.
- Bruker OPUS 8.7 SDLC evidence is available via the vendor for the Cat 4 vendor-reliance section of the CS.

## 9. References

**US / FDA:**
- 21 CFR Part 11 §§ .10(a)/(b)/(c)/(d)/(e)/(k), .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .68 (equipment), .84 (testing and approval or rejection of components), .160, .165 (testing and release for distribution), .194 (laboratory records)
- FDA *Guidance for Industry — PAT: A Framework for Innovative Pharmaceutical Development, Manufacturing, and Quality Assurance* (2004)
- FDA *Guidance on Data Integrity and Compliance with cGMP* (2018)

**EU / EMA:**
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EMA *Guideline on the use of Near Infrared Spectroscopy by the Pharmaceutical Industry and the Data Requirements for New Submissions and Variations* (EMA/CHMP/CVMP/QWP/17760/2009 Rev 1, 27 March 2014)
- Ph. Eur. 2.2.40 — Near-Infrared Spectroscopy

**International:**
- ICH Q2(R2) — Validation of Analytical Procedures
- ICH Q14 — Analytical Procedure Development
- ICH Q8(R2) — Pharmaceutical Development
- ICH Q9(R1) — Quality Risk Management
- USP <1119> — Near-Infrared Spectroscopy
- USP <856> — Near-Infrared Spectroscopy — Theory and Practice
- USP <1058> — Analytical Instrument Qualification
- USP <1225> — Validation of Compendial Procedures
- PIC/S PI 041 — Good Practices for Data Management and Integrity
- ISPE GAMP 5 (2nd Edition, 2022); ISPE GAMP GPG *Process Analytical Technology* (PAT)

**Vendor:**
- Bruker Optics — *MPA II FT-NIR Configuration Reference* (current rev.)
- Bruker Optics — *OPUS 8.7 Installation, Configuration, and Administration Reference*
- Bruker Optics — *OPUS Validation Module 21 CFR Part 11 Compliance Guide*

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

