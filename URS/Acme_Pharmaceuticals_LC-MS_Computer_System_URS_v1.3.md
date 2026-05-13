---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — variant-synthesis 2026-04-26; T2 enrichment 2026-05-13 (Chunk A LC-MS)"
seed_corpus_basis:
  - "PharmaDevils HPLC / GC / FTIR / Karl Fischer / UV / Viscometer URS family"
  - "GAMP 5 (2nd Edition) Category 4 conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "21 CFR Part 211 §§ .68, .180, .192 (CGMP laboratory records)"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "USP <621> Chromatography; USP <1058> Analytical Instrument Qualification (AIQ); USP <1224>-<1226> ALCOA principles"
  - "ICH Q2(R2); ICH Q3A(R2); ICH Q3B(R2); ICH Q9(R1); ICH Q14"
  - "ISPE GAMP GPG: Validation of Laboratory Computerized Systems"
  - "PIC/S PI 041 — Good Practices for Data Management and Integrity"
  - "Waters Corporation — MassLynx 4.2 SCN1027 Installation + Configuration Reference (vendor doc)"
  - "Waters Corporation — TargetLynx XS Application Manager Reference"
  - "Waters Corporation — Acquity I-Class UPLC + Xevo TQ-S micro Hardware Reference"
do_not_use_as:
  - regulated_record
  - basis_for_real_validation_decisions
intended_use:
  - "LLM fine-tuning corpus seed (variant of natural corpus styles)"
  - "prompt-tuning evaluation"
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## LC-MS Computer System — Waters MassLynx 4.2 on Windows 11

**Document Number:** ACME-URS-LCMS-001
**Version:** 1.0
**Effective Date:** 2026-04-26 *(synthetic)*
**Status:** Draft — for synthetic-corpus use only
**Site:** Acme Pharmaceuticals Ltd, Quality Control Laboratory, Building 4, Pune, India *(fictional)*
**System Owner:** QC Manager
**Process Owner:** Head of Quality Control
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Waters MassLynx 4.2 on Windows 11** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a/b/c/d/e/g/k), .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <621>; USP <1058> AIQ; USP <1224>-<1226>; ICH Q2(R2); ICH Q3A(R2); ICH Q3B(R2); ICH Q9(R1); ICH Q14; PIC/S PI 041

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _______________________ | _______________________ | __________ |
| Reviewer (QC Manager / Process Owner) | _______________________ | _______________________ | __________ |
| Reviewer (IT / System Administrator) | _______________________ | _______________________ | __________ |
| Approver (Head of Quality Assurance) | _______________________ | _______________________ | __________ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-13 | (synthetic) | Authored to Tier T2 (Cat 4 configured lab instrument; 50-80 req target). Added §§ 5.13 System Suitability Test (SST), 5.14 Mass Calibration + Tune Management, 5.15 Calibration Curve + Quantitation, 5.16 Method Lifecycle + Reprocessing, 5.17 Mass Spectrum Library Management, 5.18 LIMS Interface. Expanded §§ 5.6 Part 11 (sub-section bindings), 5.7 ALCOA+. New risks (R-06..R-11): peak-integration drift, RT shift on column-lot change, ion-source contamination, library-version drift, calibration-curve outlier suppression, MS-tune drift. Web-research citations added: USP <621> System Suitability, USP <1058> AIQ data-quality triangle, 21 CFR § 211.194(a)(8), Waters MassLynx 4.2 SCN1027, TargetLynx XS application manager, Acquity I-Class UPLC, Xevo TQ-S micro. ICH M10 references intentionally omitted (this is QC release / impurity profiling, not bioanalytical method validation — see §3). |

## Definitions and Acronyms

| Term | Definition |
|---|---|
| LC-MS | Liquid Chromatography coupled with Mass Spectrometry |
| MassLynx | Waters Corporation chromatography data system, version 4.2 |
| QC | Quality Control |
| URS | User Requirements Specification |
| FS | Functional Specification |
| RA | Risk Assessment |
| RTM | Requirements Traceability Matrix |
| IQ / OQ / PQ | Installation / Operational / Performance Qualification |
| GxP | Good Practice (any of GLP, GCP, GMP, GVP, GDP) |
| 21 CFR Part 11 | Title 21 of the U.S. Code of Federal Regulations, Part 11 — Electronic Records; Electronic Signatures |
| Annex 11 | EU GMP Annex 11 — Computerised Systems |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

---

## 1. Purpose

This User Requirements Specification (URS) defines the user, functional, regulatory, and non-functional requirements for the LC-MS Computer System used to acquire, process, and report mass-spectrometric and chromatographic data in support of GMP-regulated assay, identification, related-substances, and impurity-profiling activities at the Acme Pharmaceuticals QC Laboratory.

The URS is the controlling input to the Functional Specification (FS), Configuration Specification (CS), Risk Assessment (RA), Installation Qualification (IQ), Operational Qualification (OQ), Performance Qualification (PQ), and Requirements Traceability Matrix (RTM).

## 2. Scope

### 2.1 In scope

- One Waters Acquity I-Class UPLC chassis coupled with one Waters Xevo TQ-S micro tandem-quadrupole mass spectrometer.
- The associated dedicated workstation (HP Z4 G5) running Microsoft Windows 11 Pro 22H2 with Waters MassLynx 4.2 SCN1027 plus the TargetLynx XS application manager.
- Network connectivity to the site GMP file-server (`\\acme-gmp-fs01\masslynx-projects`) for daily backup of acquired data and processed results.
- Integration with the site Active Directory for named-user authentication and role-based access.
- Integration with the site NTP server for time synchronisation across acquisition workstation, file server, and network switch.
- Local printer (Brother HL-L6415DW) for QC sign-off hard copies.

### 2.2 Out of scope

- Sample preparation hardware (handled by an analyst-controlled Hamilton Microlab STARlet — separately validated).
- LIMS-side sample lifecycle (already validated under ACME-VAL-LIMS-007).
- Building utilities, power, and HVAC supplying the instrument room (handled under facility validation).
- Custom MassLynx scripts beyond vendor-supplied processing macros (any Acme-authored script triggers a separate Category 5 assessment).

### 2.3 System boundary diagram (textual)

```
[Sample] → [Acquity UPLC] → [Xevo TQ-S MS] → [MassLynx Workstation, Windows 11]
                                                  │
                                  named-user authentication via Active Directory
                                                  │
   ┌──────────────────────────────────────────────┼─────────────────────────────┐
   │                                              │                             │
   ▼                                              ▼                             ▼
File server `\\acme-gmp-fs01\masslynx-projects`   NTP server               Local printer
(daily backup, retention 7 years)                 (time sync, ALCOA+ "C")  (QC sign-off)
```

## 3. System Description and Intended Use

The LC-MS Computer System will be used by trained QC analysts for the following GMP-regulated activities:

- Assay determination of active pharmaceutical ingredients in finished product and stability samples.
- Quantification of related substances and impurities at or below the ICH Q3A/Q3B reporting threshold.
- Identification confirmation by retention time and product-ion mass-spectrum matching against a controlled reference library.
- Generation of analytical reports in compliance with ALCOA+ and 21 CFR Part 11.

The system is GAMP Category 4 (configurable off-the-shelf product). Vendor-supplied software is treated as supplied by Waters Corporation under their internal SDLC; site-level validation focuses on installation, configuration, intended-use functionality, and 21 CFR Part 11 controls.

## 4. User Roles

| Role | Description | Permissions (high level) |
|---|---|---|
| Analyst | Routine QC user. Acquires and processes data. | Acquire, integrate, process; no method or system-config edits. |
| Senior Analyst | Reviews analyst output. | All Analyst permissions plus second-person review actions. |
| Method Owner | Authors and edits acquisition / processing methods under change control. | Method create / edit; no system-config edits. |
| QC Manager (System Owner) | Approves results and methods. | Approve methods, approve results, lock projects. |
| System Administrator (IT) | Installation, patching, backup verification, time sync, audit-trail review configuration. | Full system-administration except QC sign-off. |
| Auditor (read-only) | Internal QA / external regulator. | Read all records, read all audit trails; cannot modify. |

Separation of duties is enforced: a user with the Analyst role cannot self-approve a method or a result (requirement URS-PART11-04 below).

## 5. User Requirements

Each requirement carries a unique ID, a priority (`H` = high / business-critical, `M` = medium, `L` = low), and a GAMP-5 risk classification (`R1` = direct GxP impact, `R2` = indirect, `R3` = none).

### 5.1 Hardware and Installation Requirements

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-HW-01 | H | R1 | The system shall comprise the listed UPLC chassis, MS detector, and dedicated workstation; no shared workstations. |
| URS-HW-02 | H | R1 | The workstation shall meet or exceed Waters' minimum specification for MassLynx 4.2 SCN1027: ≥ 16 GB RAM, ≥ 1 TB SSD, dedicated GPU, two USB-3 ports for instrument communication. |
| URS-HW-03 | M | R2 | The workstation shall be connected to the site UPS to allow controlled shutdown for power-loss events of up to 30 minutes. |
| URS-HW-04 | H | R1 | The workstation shall be connected to the GMP network segment, not the office segment. |
| URS-HW-05 | M | R2 | The instrument room shall be temperature-controlled to 20 ± 3 °C and 30–60% RH; environmental monitoring is out of scope of this URS but shall be linked. |

### 5.2 Software Configuration Requirements

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-SW-01 | H | R1 | The system shall run Windows 11 Pro 22H2 on a domain-joined workstation; no local administrator accounts shall be available to QC users. |
| URS-SW-02 | H | R1 | The system shall run MassLynx 4.2 SCN1027 plus TargetLynx XS, installed by Waters or by a Waters-trained engineer per the vendor's installation procedure. |
| URS-SW-03 | H | R1 | All MassLynx project folders shall reside on the dedicated network share `\\acme-gmp-fs01\masslynx-projects`; no GMP data shall be stored on the local C: drive other than the active acquisition cache. |
| URS-SW-04 | H | R1 | The Windows audit policy shall log logon, logoff, and account-management events; logs shall be forwarded to the site SIEM. |
| URS-SW-05 | M | R2 | Anti-malware (CrowdStrike Falcon Sensor) shall be installed with vendor-approved exclusion list to avoid interfering with acquisition. |
| URS-SW-06 | H | R1 | The system clock shall be synchronised to the site NTP server (`ntp.acme.local`) with skew ≤ 1 second. |
| URS-SW-07 | M | R2 | The screen saver shall lock after 10 minutes of inactivity and require domain credentials to unlock. |

### 5.3 Functional Requirements (Acquisition)

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-ACQ-01 | H | R1 | The system shall allow analysts to load an approved acquisition method from the controlled methods library (read-only to analysts). |
| URS-ACQ-02 | H | R1 | The system shall reject the start of a sample sequence if any of the following are true: instrument not in Ready state; no approved method selected; project folder is locked. |
| URS-ACQ-03 | H | R1 | The system shall record sample injection sequence with sample identifier, vial position, injection volume, method ID, method version, instrument identifier, analyst user ID, and timestamp. |
| URS-ACQ-04 | M | R2 | The system shall allow pause / resume of an in-progress sequence with reason captured in the audit trail. |
| URS-ACQ-05 | H | R1 | The system shall capture system-suitability injections at the start of each sequence and reject results processing for the sequence if the SST acceptance criteria fail. |

### 5.4 Functional Requirements (Processing and Reporting)

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PROC-01 | H | R1 | The system shall integrate chromatographic peaks per the approved processing method; manual integration shall be permitted only with a captured reason for change. |
| URS-PROC-02 | H | R1 | The system shall preserve the raw acquired data file unaltered; all processing shall produce a derived result that references but does not overwrite the raw file. |
| URS-PROC-03 | H | R1 | The system shall perform mass-spectrum library matching against the controlled reference library (`ACME-MSLIB-2026Q2`) and report match score with a configurable threshold. |
| URS-PROC-04 | H | R1 | The system shall calculate and report assay, related substances, and impurity values per the configured equation set, with rounding rules per the site SOP. |
| URS-PROC-05 | H | R1 | The system shall generate a PDF analytical report containing: sample metadata, method ID and version, instrument ID, analyst, reviewer, approver, all integrated peaks, calculated results, ALCOA+ statement, and report hash. |
| URS-PROC-06 | M | R2 | The system shall allow report regeneration from the same processed data; the regenerated report shall be marked "RE-ISSUED" and reference the original report ID. |

### 5.5 Functional Requirements (Audit Trail and Records Management)

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | The system shall maintain a contemporaneous, time-stamped, secure audit trail capturing user, action, old value, new value, and reason-for-change for all GMP-relevant operations. |
| URS-AUD-02 | H | R1 | The audit trail shall not be editable or deletable by any user, including system administrators. |
| URS-AUD-03 | H | R1 | The audit trail shall be reviewable in human-readable form and exportable as PDF; review shall be performed by a Senior Analyst before each batch sign-off (event-driven), and by the QC Manager monthly (periodic). |
| URS-AUD-04 | H | R1 | The retention period for raw acquisition files, processed results, audit trails, and reports shall be 7 years from data acquisition (or longer if local regulation requires). |
| URS-AUD-05 | M | R2 | The system shall provide a documented mechanism to export audit trails for inspection during a regulatory audit without disrupting routine operation. |

### 5.6 21 CFR Part 11 Requirements

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per 21 CFR § 11.10(a), the system shall be validated to ensure accuracy, reliability, and consistent intended performance; procedures shall protect against record invalidity. |
| URS-PART11-02 | H | R1 | Per 21 CFR § 11.10(b), the system shall generate accurate and complete copies of records in human-readable (PDF/A-3) and electronic form suitable for inspection. |
| URS-PART11-03 | H | R1 | Per 21 CFR § 11.10(c), records shall be protected throughout the 7-year retention period (WORM file-share + verified daily backup; integrity hash on every project archive). |
| URS-PART11-04 | H | R1 | Per 21 CFR § 11.10(d), access shall be limited to authorised individuals via Active Directory authentication; local accounts disabled. |
| URS-PART11-05 | H | R1 | Per 21 CFR § 11.10(e), a contemporaneous operational audit trail shall exist (see §5.5). |
| URS-PART11-06 | H | R1 | Per 21 CFR § 11.10(g), authority checks shall be enforced (role-based access via MassLynx user-management bound to AD groups). |
| URS-PART11-07 | M | R2 | Per 21 CFR § 11.10(k), system operation manuals and change control shall be in place; vendor SCN updates managed under site CR with impact assessment. |
| URS-PART11-08 | H | R1 | Per 21 CFR § 11.50, electronic signatures shall include the signer's printed name, the date and time of signature, and the meaning (e.g., review, approval, lock). |
| URS-PART11-09 | H | R1 | Per 21 CFR § 11.70, electronic signatures shall be cryptographically linked to the signed record so any subsequent change to the record invalidates the signature. |
| URS-PART11-10 | H | R1 | Per 21 CFR § 11.100, each electronic signature shall be unique to the individual and shall not be reused or reassigned to anyone else. |
| URS-PART11-11 | H | R1 | Per 21 CFR § 11.200, the system shall require re-authentication at the moment of signing (no cached credentials); for non-biometric identity-based signatures, the first signing of a continuous session uses both ID and password components, subsequent signings within the session may use one component. |
| URS-PART11-12 | H | R1 | Per 21 CFR § 11.300, password and credential controls shall enforce complexity, expiry, and lockout — failed-login attempts beyond a configurable threshold (default 5 within 15 minutes) shall lock the account and notify the System Administrator. |
| URS-PART11-13 | H | R1 | The system shall enforce separation of duties: a user with the Analyst role shall not be able to apply a Reviewer or Approver signature on the same record. |

### 5.7 Data Integrity (ALCOA+)

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | All records shall be Attributable to a named domain user. |
| URS-DI-02 | H | R1 | All records shall be Legible and exportable as human-readable PDF. |
| URS-DI-03 | H | R1 | All records shall be Contemporaneous; entries posted retrospectively shall be flagged with the actual entry timestamp and a reason. |
| URS-DI-04 | H | R1 | The Original raw file shall be preserved unaltered; processing produces derived files that reference but do not overwrite. |
| URS-DI-05 | H | R1 | Calculations shall be Accurate; the configured equations and rounding shall be tested per the OQ protocol. |
| URS-DI-06 | M | R2 | Records shall be Complete (all expected metadata fields populated), Consistent (chronological order preserved), Enduring (7-year retention with verified daily backup), and Available (retrievable within 1 business day during an inspection). |

### 5.8 Backup, Restore, and Disaster Recovery

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | The MassLynx project share shall be backed up daily to the site backup target with cryptographic integrity verification. |
| URS-BAK-02 | H | R1 | A documented restore test shall be performed quarterly by the System Administrator with witness from QC. |
| URS-BAK-03 | M | R2 | The recovery time objective (RTO) for the LC-MS Computer System after total workstation failure shall be ≤ 8 business hours from a documented hardware-replaced-and-software-reinstalled baseline. |
| URS-BAK-04 | M | R2 | The recovery point objective (RPO) shall be ≤ 24 hours (last successful daily backup). |

### 5.9 Performance and Reliability

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | The workstation shall complete a typical 50-injection sequence acquisition without crashing or losing data integrity. |
| URS-PERF-02 | M | R2 | Chromatographic processing of a 50-injection sequence shall complete within 15 minutes on the dedicated workstation. |
| URS-PERF-03 | L | R3 | The user interface response time for routine UI actions (open project, load method) shall be ≤ 3 seconds at the 95th percentile. |
| URS-PERF-04 | M | R2 | The system shall be available for production use ≥ 99.0% during business hours, excluding planned maintenance windows. |

### 5.10 Security

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | All user accounts shall be domain accounts; local accounts other than the System Administrator break-glass account shall be disabled. |
| URS-SEC-02 | H | R1 | Password complexity and rotation shall meet the site Information Security policy. |
| URS-SEC-03 | H | R1 | Removable media (USB drives, optical disks) shall be blocked except for vendor-approved engineering use under change control. |
| URS-SEC-04 | M | R2 | Anti-malware definitions shall be updated daily and reported to the IT compliance dashboard. |
| URS-SEC-05 | M | R2 | The Windows firewall shall be enabled with the GMP-segment ruleset deployed via Group Policy. |

### 5.11 Training

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | No user shall be granted production access until role-specific training has been completed and recorded in the site Learning Management System. |
| URS-TRN-02 | M | R2 | Annual refresher training shall be required for all named users. |

### 5.12 Periodic Review

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PR-01 | H | R1 | A periodic review of the validated state of the LC-MS Computer System shall be performed at least annually, examining: configuration drift, audit-trail review evidence, deviations / change controls, backup-restore test evidence, training currency, and continued fitness for use. |
| URS-PR-02 | M | R2 | The periodic review shall be signed by the QC Manager and the QA Manager. |

### 5.13 System Suitability Test (SST) per USP <621>

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-SST-01 | H | R1 | The system shall execute a method-specific System Suitability Test (SST) at the start of every analytical sequence per USP <621>; SST parameters shall include resolution (R ≥ method-specified), tailing factor (Tf ≤ method-specified, typ. 2.0), theoretical plates (N ≥ method-specified), retention-time RSD (≤ 1.0%), and peak-area RSD on replicate injections (≤ 2.0% for assay, ≤ 15% near LOQ). |
| URS-SST-02 | H | R1 | SST acceptance shall be evaluated automatically by TargetLynx XS against the method-bound criteria; the system shall block release of any quantitative result downstream of a failed SST until the SST is repeated and passes. |
| URS-SST-03 | H | R1 | The system shall record SST evaluation as a discrete record with method-id, criteria thresholds, observed values, pass/fail flag per parameter, and overall verdict; the SST record shall be bound to the sequence by a cryptographic reference. |
| URS-SST-04 | M | R2 | The system shall support bracketed SST per USP <621> (SST at start AND end of long sequences ≥ 30 injections); failure of the bracket-end SST shall flag all bracketed results as suspect pending investigation. |
| URS-SST-05 | M | R2 | The system shall support carryover assessment in the SST (blank injection after the highest standard, peak area ≤ 0.2% of LOQ peak area per USP <621>); carryover failure shall block release. |

### 5.14 Mass Calibration and Tune Management

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-CAL-01 | H | R1 | The Xevo TQ-S micro mass calibration (m/z) shall be performed and verified per the Waters-published cadence (daily lock-mass check; weekly mass calibration with sodium-iodide / leucine-enkephalin reference; monthly full tune); calibration records shall be retained with the run-records they qualify. |
| URS-CAL-02 | H | R1 | The system shall block sample acquisition when the active mass-calibration record is expired against the method-specified validity window. |
| URS-CAL-03 | H | R1 | Source-tune parameters (capillary voltage, cone voltage, source temperature, desolvation temperature, desolvation gas flow) shall be method-pinned; any deviation from method-pinned values shall require Method Owner override with reason captured. |
| URS-CAL-04 | M | R2 | The system shall capture instrument-PM events (cleaning of source, replacement of cone / capillary, replacement of skimmer / hexapole) and require a re-tune + SST verification before the next GxP run after PM. |

### 5.15 Calibration Curve and Quantitation

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-QNT-01 | H | R1 | The system shall construct calibration curves from validated standards (minimum 6 non-zero levels for quantitative assay; minimum 5 for related-substances per ICH Q2(R2)); curve coefficient of determination (r² ≥ 0.99 for quantitative assay) shall be evaluated automatically. |
| URS-QNT-02 | H | R1 | The system shall flag calibration-curve outliers using validated outlier rules (% back-calculation outside ± 15% of nominal for non-LOQ standards, ± 20% at LOQ); exclusion of any standard from the curve shall require Method Owner signature with reason. |
| URS-QNT-03 | H | R1 | The system shall apply matrix-matched calibration where the method-bound matrix flag is set; mis-matched matrix shall block run start. |
| URS-QNT-04 | H | R1 | The system shall compute results in the method-specified units (µg/mL, %, ppm, or mass fraction) using the method-bound equation set with rounding rules per the site SOP; intermediate precision shall be preserved (no rounding before final answer). |
| URS-QNT-05 | M | R2 | The system shall flag any result exceeding 30%, 50%, and 100% of the specification limit (for trending, OOT, and OOS investigation per FDA Guidance for Industry on OOS results). |

### 5.16 Method Lifecycle, Reprocessing, and Report Re-issue

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-MTH-01 | H | R1 | Acquisition and processing methods shall follow lifecycle states {DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE}; only methods in state EFFECTIVE may be selected for GxP runs. |
| URS-MTH-02 | H | R1 | Method creation, edit, and state transitions shall require an electronic signature with Author ≠ Reviewer ≠ Approver separation of duties; method history shall be retained immutably. |
| URS-MTH-03 | H | R1 | Reprocessing of acquired data with a new processing-method version shall be permitted only against the original raw file (no re-acquisition); the reprocessed result shall reference both the original and the reprocessing method versions and shall be marked as a reprocessing. |
| URS-MTH-04 | H | R1 | Where reprocessing produces a result that differs from the previously approved result, the system shall require a deviation record + Method Owner / QC Manager dual signature before the new result may be reported externally. |
| URS-MTH-05 | M | R2 | The system shall support method-version migration: when a method is superseded, in-flight sequences may complete with the previous version; new sequences default to the new EFFECTIVE version. |

### 5.17 Mass Spectrum Library Management

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-LIB-01 | H | R1 | The reference mass-spectrum library (`ACME-MSLIB-2026Q2`) shall be version-controlled; library updates shall require Method Owner approval + Senior Analyst review under change control with a defined acceptance test (re-process N reference samples, verify match-scores stable within tolerance). |
| URS-LIB-02 | H | R1 | The system shall record the library version, library hash, and per-component match-score threshold for every identification result. |
| URS-LIB-03 | M | R2 | The system shall flag identifications where the match-score falls within ± 5% of the configured threshold (borderline) for Senior Analyst attention. |
| URS-LIB-04 | M | R2 | Retention-time database (RTDB) entries supporting library matching shall be qualified per column lot (RT shift recalibration); column-lot change shall trigger an RTDB drift check before GxP use. |

### 5.18 LIMS Interface

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-INT-LIMS-01 | H | R1 | The system shall import sample worklists from LabWare LIMS 8 via a one-way read connector; each imported worklist shall be cached locally and bound to the sequence. |
| URS-INT-LIMS-02 | H | R1 | The system shall push approved analytical results (QC Manager approval state) to LIMS only; rejected, in-review, or unapproved results shall be blocked at the connector layer. |
| URS-INT-LIMS-03 | H | R1 | Result payloads to LIMS shall include the report-id, instrument-id, method-id + version, library-id + version, calibration-curve-id, SST-record-id, analyst-id, reviewer-id, approver-id, raw-file hash, and result hash; LIMS shall reject payloads missing any of these fields. |
| URS-INT-LIMS-04 | M | R2 | LIMS interface failures (connection, schema mismatch, duplicate report) shall be logged to the site SIEM within 5 minutes; the System Administrator shall be paged. |

### 5.19 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is Kerberos (interactive) and LDAPS (service-account bind) on-prem; conditional-access policy `Lab-Workstation Conditional Access (MFA on interactive logon)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the Chromeleon SQL backend; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 7 y (≥ 25 y if release-linked) per the consuming-record schedule. |

## 6. Acceptance Criteria

The system shall be accepted into validated routine GMP use when:

1. The Functional Specification, Configuration Specification, Risk Assessment, IQ Protocol, OQ Protocol, and PQ Protocol have been authored and approved.
2. The IQ has been executed and all critical findings closed.
3. The OQ has been executed and all critical and major findings closed; minor findings have a documented disposition.
4. The PQ has been executed and all critical and major findings closed.
5. The Validation Summary Report has been authored and approved by the QC Manager and the QA Manager.
6. All named users for go-live have completed training.
7. The Requirements Traceability Matrix shows every URS requirement mapped to at least one approved test case in OQ or PQ.

## 7. Constraints

- The system shall not introduce custom code (Category 5) without a separate Category-5 assessment.
- Vendor patches and SCN releases shall be evaluated under change control before deployment.
- Direct internet access from the workstation is not permitted.

## 8. Assumptions

- Waters Corporation maintains its internal SDLC and continues to release validated SCN updates.
- The site Active Directory is itself qualified.
- The site SIEM is operational and retains logs in line with the site retention policy.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 — Electronic Records; Electronic Signatures §§ .10(a), .10(b), .10(c), .10(d), .10(e), .10(g), .10(k), .50, .70, .100, .200, .300.
- 21 CFR Part 211 — Current Good Manufacturing Practice §§ .68 (Automatic, mechanical, and electronic equipment), .180 (General requirements for records), .192 (Production record review), .194(a)(8) (laboratory records — complete record of all data secured in the course of each test).
- FDA *Guidance for Industry: Investigating Out-of-Specification (OOS) Test Results for Pharmaceutical Production* (2022).
- FDA *Guidance on Data Integrity and Compliance With cGMP* (2018).

### EU
- EU GMP Annex 11 — Computerised Systems §§ 4 (validation), 6 (accuracy checks), 9 (audit trail), 11 (periodic evaluation).
- EudraLex Volume 4 — Good Manufacturing Practice.

### USP — primary text for chromatography
- USP <621> — Chromatography (system suitability parameters: resolution, tailing factor, theoretical plates, repeatability).
- USP <1058> — Analytical Instrument Qualification (AIQ) — 4Q model (DQ / IQ / OQ / PQ); instrument classification A/B/C (LC-MS is Group C).
- USP <1224> — Transfer of Analytical Procedures; USP <1225> — Validation of Compendial Procedures; USP <1226> — Verification of Compendial Procedures.

### International — ICH
- ICH Q2(R2) — Validation of Analytical Procedures.
- ICH Q3A(R2) — Impurities in New Drug Substances; ICH Q3B(R2) — Impurities in New Drug Products.
- ICH Q9(R1) — Quality Risk Management.
- ICH Q14 — Analytical Procedure Development.

### Industry guidance
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE GAMP Good Practice Guide: *Validation of Laboratory Computerized Systems*.
- ISPE GAMP Good Practice Guide: *Records and Data Integrity*.
- PIC/S PI 041 — Good Practices for Data Management and Integrity in Regulated GMP/GDP Environments.

### Vendor
- Waters Corporation — *MassLynx 4.2 SCN1027 Installation and Configuration Reference*.
- Waters Corporation — *TargetLynx XS Application Manager Reference*.
- Waters Corporation — *Acquity I-Class UPLC + Xevo TQ-S micro Hardware Reference + Maintenance Guide*.

### Site / context
- Site SOP *SOP-QC-CHROM-INTEGRATION-002* (manual integration justification).
- LIMS validation `ACME-VAL-LIMS-007`.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

