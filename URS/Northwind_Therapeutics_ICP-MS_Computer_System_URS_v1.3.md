---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline variant-synthesis 2026-04-26; T2 enrichment 2026-05-13 (Chunk A ICP-MS)"
seed_corpus_basis:
  - "PharmaDevils HPLC / GC / FTIR / Karl Fischer / UV / Viscometer URS family"
  - "GAMP 5 (2nd Edition) Category 4 conventions"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300"
  - "21 CFR Part 211 §§ .68, .180, .192, .194(a)(8)"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "USP <232> Limits / <233> Procedures / <730> Plasma Spectrochemistry"
  - "USP <1058> AIQ; USP <1224>-<1226>"
  - "ICH Q2(R2); ICH Q3D(R2) Elemental Impurities; ICH Q9(R1); ICH Q14"
  - "PIC/S PI 041"
  - "Thermo Fisher — Qtegra ISDS 2.10 Installation and Configuration Reference (vendor doc)"
  - "Thermo Fisher — TraceCERT plugin + Pharma Compliance plugin Reference"
  - "Thermo Fisher — iCAP RQ + Cetac ASX-560 Hardware Reference"
do_not_use_as:
  - regulated_record
  - basis_for_real_validation_decisions
intended_use:
  - "LLM fine-tuning corpus seed"
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## ICP-MS Computer System — Thermo Fisher iCAP RQ + Qtegra ISDS 2.10

**Document Number:** NWT-URS-ICPMS-001
**Version:** 1.0
**Effective Date:** 2026-04-26 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Site:** Northwind Therapeutics Pvt. Ltd., Quality Control Laboratory, Block C, Hinjewadi Phase II, Pune, Maharashtra, India *(fictional)*
**System Owner:** QC Manager — Trace Analytics
**Process Owner:** Head of Quality Control
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Thermo Fisher iCAP RQ + Qtegra ISDS 2.10** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192, .194(a)(8); EU GMP Annex 11 §§ 4, 6, 9, 11; ICH Q3D(R2) Elemental Impurities; ICH Q2(R2); ICH Q9(R1); USP <232> / <233> / <730>; USP <1058> AIQ; USP <1224>-<1226>; PIC/S PI 041

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _______________________ | _______________________ | __________ |
| Reviewer (QC Manager — Trace Analytics) | _______________________ | _______________________ | __________ |
| Reviewer (IT / System Administrator) | _______________________ | _______________________ | __________ |
| Approver (Head of Quality Assurance) | _______________________ | _______________________ | __________ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-13 | (synthetic) | Authored to Tier T2 (50-80 req target; Cat 4 ICP-MS). Added §§ 5.14 System Suitability / Tune verification, 5.15 Interference Correction + Internal Standards + Drift Monitoring, 5.16 Calibration Curve + Quantitation per USP <233>, 5.17 Method Lifecycle, 5.18 Sample Preparation Linkage. Expanded §§ 5.6 Part 11 (sub-section bindings). New risks (R-06..R-11): polyatomic-interference mis-correction, internal-standard drift, calibration-curve outlier suppression, plasma-instability mid-sequence, oxide/doubly-charged ratio drift between tunes, Q3D PDE limit mis-application. Web-research citations: USP <232>/<233>/<730>, USP <1058> AIQ, ICH Q3D(R2), 21 CFR § 211.194(a)(8). |

## Definitions and Acronyms

| Term | Definition |
|---|---|
| ICP-MS | Inductively Coupled Plasma — Mass Spectrometry |
| iCAP RQ | Thermo Fisher iCAP RQ single-quadrupole ICP-MS instrument |
| Qtegra ISDS | Thermo Fisher Intelligent Scientific Data Solution, version 2.10 |
| ICH Q3D | ICH guideline for elemental impurities in drug products |
| USP <232> / <233> | USP General Chapters on elemental impurities — limits and procedures |
| KED | Kinetic Energy Discrimination (helium collision-cell mode) |
| LIMS | Laboratory Information Management System (LabWare LIMS 8 — site standard) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

---

## 1. Purpose

This URS defines the user, functional, regulatory, and non-functional requirements for the ICP-MS Computer System used to determine elemental impurities in finished pharmaceutical products, APIs, excipients, and packaging materials in support of ICH Q3D and USP <232>/<233> compliance at the Northwind Therapeutics QC Trace Analytics laboratory.

The URS is the controlling input to the Functional Specification (`NWT-FS-ICPMS-001`), Configuration Specification (`NWT-CS-ICPMS-001`), Risk Assessment (`NWT-RA-ICPMS-001`), IQ / OQ / PQ Protocols (`NWT-IQ/OQ/PQ-ICPMS-001`), and Requirements Traceability Matrix (`NWT-RTM-ICPMS-001`).

## 2. Scope

### 2.1 In scope

- One Thermo Fisher iCAP RQ single-quadrupole ICP-MS with autosampler (Cetac ASX-560), connected to a dedicated workstation.
- The dedicated workstation (Dell Precision 3680) running Microsoft Windows 11 Pro 22H2 with Qtegra ISDS 2.10 (build 2.10.4710.184) plus the Thermo Fisher TraceCERT and Pharma Compliance plugins.
- LIMS interface (read-only sample worklist import; one-way push of approved results to LabWare LIMS 8 via Qtegra LIMS Connector 1.6).
- Network connectivity to the site GMP file server (`\\nwt-gmp-fs02\qtegra-projects`) for daily backup.
- Active Directory integration for named-user authentication and role-based access (`NWT.local` domain).
- Time synchronisation to site NTP (`ntp.nwt.local`).
- Local barcode reader (Honeywell Voyager 1452g) for sample-vial identification.

### 2.2 Out of scope

- Sample digestion hardware (closed-vessel microwave digestor — Milestone UltraWAVE, validated separately).
- LIMS-side sample lifecycle (`LIMS-CSV-2025-014`).
- Internal-standard solution preparation (manual, governed by SOP-QC-LAB-088).
- Building utilities (chiller, exhaust, argon supply) — facility validation.

### 2.3 System boundary diagram (textual)

```
[Sample digestate]
     │
     ▼
[Cetac ASX-560 autosampler] ─► [iCAP RQ ICP-MS] ─► [Qtegra workstation, Windows 11]
                                                      │
                       AD-authenticated user session  │
                                                      │
   ┌──────────────────┬───────────────────────────────┼───────────────────────────────┐
   │                  │                               │                               │
   ▼                  ▼                               ▼                               ▼
File server          NTP server                 LIMS Connector                   Barcode reader
(daily backup,       (ALCOA+ "C")               (read worklist /                 (sample-vial ID)
 7-yr retention)                                 push approved results)
```

## 3. System Description and Intended Use

The ICP-MS Computer System is operated by trained QC analysts to:

- Quantify elemental impurities (As, Cd, Co, Cr, Cu, Hg, Ir, Mn, Mo, Ni, Os, Pb, Pd, Pt, Rh, Ru, Se, Sn, V, Zn) per ICH Q3D Class 1 / 2A / 2B / 3 against PDE-derived limits.
- Perform USP <233> Procedure 1 (quantitative) and Procedure 2 (limit) tests.
- Apply collision-cell (helium KED) and reaction-cell modes for polyatomic interference removal.
- Generate analytical reports compliant with ALCOA+ and 21 CFR Part 11.

The system is GAMP Category 4. Vendor-supplied software (Qtegra ISDS) is treated as supplied by Thermo Fisher Scientific under their internal SDLC; site-level validation focuses on installation, configuration, intended-use functionality, 21 CFR Part 11 controls, and the LIMS interface.

## 4. User Roles

| Role | Description | Permissions (high level) |
|---|---|---|
| Analyst | Routine QC user. Acquires and processes data. | Acquire, integrate, process; no method or system-config edits. |
| Senior Analyst / Reviewer | Reviews analyst output, performs second-person review. | All Analyst permissions plus second-person review actions; cannot approve. |
| Method Owner | Authors and edits acquisition / processing methods under change control. | Method create / edit; no system-config edits. |
| QC Manager (System Owner) | Approves results and methods; locks projects. | Approve, lock, release to LIMS. |
| System Administrator (IT) | Installation, patching, backup verification, time-sync, AD group management. | Full system administration except QC sign-off. |
| Auditor (read-only) | Internal QA / external regulator. | Read all records and audit trails; cannot modify. |

**Separation of duties (URS-PART11-04):** an Analyst cannot self-approve a method or a result.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), and GAMP-5 risk classification (`R1` direct GxP / `R2` indirect / `R3` none).

### 5.1 Hardware and Installation

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-HW-01 | H | R1 | The system shall comprise the iCAP RQ ICP-MS, ASX-560 autosampler, and dedicated workstation; no shared workstations. |
| URS-HW-02 | H | R1 | The workstation shall meet or exceed Thermo Fisher's minimum spec for Qtegra 2.10: ≥ 32 GB RAM, ≥ 1 TB SSD, dedicated GPU, two USB-3 ports for instrument and autosampler communication. |
| URS-HW-03 | H | R1 | The workstation shall be connected to the site UPS to allow controlled shutdown for power-loss events of up to 30 minutes. |
| URS-HW-04 | H | R1 | The workstation shall be on the GMP network segment, not the office segment. |
| URS-HW-05 | M | R2 | Argon supply pressure and chiller status shall be readable from Qtegra; alarm thresholds per the site SOP. |
| URS-HW-06 | M | R2 | The instrument room shall be temperature-controlled to 20 ± 2 °C and 30–60% RH; environmental monitoring is out of scope of this URS but shall be linked. |

### 5.2 Software Configuration

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-SW-01 | H | R1 | The system shall run Windows 11 Pro 22H2, domain-joined to `NWT.local`; no local administrator accounts shall be available to QC users. |
| URS-SW-02 | H | R1 | The system shall run Qtegra ISDS 2.10 (build 2.10.4710.184) plus TraceCERT and Pharma Compliance plugins, installed by Thermo Fisher or by a Thermo-trained engineer. |
| URS-SW-03 | H | R1 | All Qtegra projects shall reside on `\\nwt-gmp-fs02\qtegra-projects`; no GMP data on the local C: drive other than the active acquisition cache. |
| URS-SW-04 | H | R1 | The Windows audit policy shall log logon, logoff, and account-management events; logs shall be forwarded to the site SIEM (Splunk Enterprise). |
| URS-SW-05 | M | R2 | Anti-malware (CrowdStrike Falcon Sensor) shall be installed with vendor-approved exclusions to avoid acquisition interference. |
| URS-SW-06 | H | R1 | The system clock shall be synchronised to `ntp.nwt.local` with skew ≤ 1 second. |
| URS-SW-07 | M | R2 | The screen saver shall lock after 10 minutes of inactivity and require domain credentials to unlock. |

### 5.3 Acquisition

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-ACQ-01 | H | R1 | The system shall load an approved acquisition method from the controlled methods library (read-only to analysts). |
| URS-ACQ-02 | H | R1 | The system shall reject the start of a sample sequence if any of: instrument not in plasma-on Ready state; no approved method selected; project folder locked; argon pressure below threshold. |
| URS-ACQ-03 | H | R1 | The system shall record sample-injection metadata: sample ID, vial position, dilution factor, internal-standard ID, method ID + version, instrument ID, analyst user ID, timestamp. |
| URS-ACQ-04 | H | R1 | The system shall capture system-suitability injections (tune solution + Q-pass criteria — sensitivity, oxide ratio, doubly-charged ratio, stability) at the start of each sequence. |
| URS-ACQ-05 | H | R1 | If SST acceptance criteria fail, results processing for the sequence shall be blocked until corrective action is documented and SST is repeated. |
| URS-ACQ-06 | M | R2 | The system shall allow pause / resume of a sequence with reason captured in the audit trail. |

### 5.4 Processing and Reporting

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PROC-01 | H | R1 | The system shall apply the approved processing method (mass-bias correction, internal-standard normalization, KED interference correction). |
| URS-PROC-02 | H | R1 | Manual reprocessing (re-fit calibration, re-select internal standard) shall require a captured reason for change. |
| URS-PROC-03 | H | R1 | Raw acquired data shall be preserved unaltered; processing produces a derived result that references but does not overwrite the raw file. |
| URS-PROC-04 | H | R1 | The system shall calculate concentration in µg/g or µg/day (per dose-based PDE) and compare against the configured ICH Q3D / USP <232> limits. |
| URS-PROC-05 | H | R1 | The system shall flag any result exceeding 30%, 50%, and 100% of the configured limit (for trending, OOT, and OOS respectively). |
| URS-PROC-06 | H | R1 | The system shall generate a PDF analytical report containing: sample metadata, method ID and version, instrument ID, analyst, reviewer, approver, integrated peaks, calculated concentrations, limit status, ALCOA+ statement, and report hash. |
| URS-PROC-07 | M | R2 | The system shall allow report regeneration from the same processed data; the regenerated report shall be marked "RE-ISSUED" and reference the original report ID. |

### 5.5 Audit Trail and Records

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | The system shall maintain a contemporaneous, time-stamped, secure audit trail capturing user, action, old value, new value, and reason-for-change for all GMP-relevant operations. |
| URS-AUD-02 | H | R1 | The audit trail shall not be editable or deletable by any user, including system administrators. |
| URS-AUD-03 | H | R1 | The audit trail shall be reviewable in human-readable form and exportable as PDF. Review shall be performed by a Senior Analyst before each batch sign-off (event-driven), and by the QC Manager monthly (periodic). |
| URS-AUD-04 | H | R1 | Retention for raw files, processed results, audit trails, and reports shall be 7 years from acquisition (or longer if local law requires). |
| URS-AUD-05 | M | R2 | A documented mechanism shall exist to export audit trails for regulatory inspection without disrupting routine operation. |

### 5.6 21 CFR Part 11

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a), the system shall be validated to ensure accuracy, reliability, and consistent intended performance. |
| URS-PART11-02 | H | R1 | Per § 11.10(b), the system shall generate accurate and complete copies of records in human-readable (PDF/A-3) and electronic form. |
| URS-PART11-03 | H | R1 | Per § 11.10(c), records shall be protected throughout the 7-year retention period via WORM file-share + verified daily backup. |
| URS-PART11-04 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via AD authentication. |
| URS-PART11-05 | H | R1 | Per § 11.10(e), operational audit trail per § 5.5 shall exist. |
| URS-PART11-06 | H | R1 | Per § 11.10(g), Qtegra Pharma-Compliance authority sets shall be mapped to AD groups; authority checks enforced at every privileged action. |
| URS-PART11-07 | M | R2 | Per § 11.10(k), Qtegra SCN updates managed under site CR; system-operation manual maintained. |
| URS-PART11-08 | H | R1 | Per § 11.50, electronic signatures shall include the signer's printed name, date and time, and meaning (closed list: Review / Approve / Reject / Lock). |
| URS-PART11-09 | H | R1 | Per § 11.70, electronic signatures shall be cryptographically linked to the signed record so any change invalidates the signature. |
| URS-PART11-10 | H | R1 | Per § 11.100, each electronic signature shall be unique to the individual and shall not be reused or reassigned. |
| URS-PART11-11 | H | R1 | Per § 11.200, the system shall require re-authentication at the moment of signing (no cached credentials). |
| URS-PART11-12 | H | R1 | Per § 11.300, failed-login attempts beyond a configurable threshold (default 5 within 15 minutes) shall lock the account and notify the System Administrator. |
| URS-PART11-13 | H | R1 | The system shall enforce separation of duties: an Analyst shall not be able to apply a Reviewer or Approver signature on the same record. |

### 5.7 Data Integrity (ALCOA+)

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | All records shall be Attributable to a named domain user. |
| URS-DI-02 | H | R1 | All records shall be Legible and exportable as human-readable PDF. |
| URS-DI-03 | H | R1 | All records shall be Contemporaneous; entries posted retrospectively shall be flagged with the actual entry timestamp and a reason. |
| URS-DI-04 | H | R1 | The Original raw file shall be preserved unaltered. |
| URS-DI-05 | H | R1 | Calculations shall be Accurate; the configured equations and rounding shall be tested per the OQ protocol. |
| URS-DI-06 | M | R2 | Records shall be Complete (all metadata fields populated), Consistent (chronological order preserved), Enduring (7-year retention with verified daily backup), and Available (retrievable within 1 business day during inspection). |

### 5.8 LIMS Interface

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-INT-01 | H | R1 | The system shall import sample worklists from LabWare LIMS 8 via the Qtegra LIMS Connector 1.6 (one-way, read-only). |
| URS-INT-02 | H | R1 | Approved analytical results shall be pushed to LIMS only after QC Manager approval; rejected/draft results shall not be transmitted. |
| URS-INT-03 | H | R1 | Each LIMS-bound result shall include the report ID, instrument ID, method ID + version, and reviewer/approver identifiers; LIMS shall reject any result missing these. |
| URS-INT-04 | M | R2 | LIMS interface failures (connection, schema mismatch, duplicate report) shall be logged and surface to the System Administrator within 5 minutes. |

### 5.9 Backup, Restore, Disaster Recovery

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | The Qtegra project share shall be backed up daily to the site backup target (Veeam) with cryptographic integrity verification. |
| URS-BAK-02 | H | R1 | A documented restore test shall be performed quarterly with witness from QC. |
| URS-BAK-03 | M | R2 | RTO after total workstation failure: ≤ 8 business hours from a documented hardware-replaced-and-software-reinstalled baseline. |
| URS-BAK-04 | M | R2 | RPO ≤ 24 hours (last successful daily backup). |

### 5.10 Performance

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | The workstation shall complete a typical 60-injection sequence acquisition without crashing or losing data integrity. |
| URS-PERF-02 | M | R2 | Processing of a 60-injection sequence shall complete within 10 minutes on the dedicated workstation. |
| URS-PERF-03 | L | R3 | UI response time for routine actions (open project, load method) ≤ 3 seconds at the 95th percentile. |
| URS-PERF-04 | M | R2 | System availability ≥ 99.0% during business hours, excluding planned maintenance. |

### 5.11 Security

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | All user accounts shall be domain accounts; local accounts other than a System Administrator break-glass account shall be disabled. |
| URS-SEC-02 | H | R1 | Password complexity and rotation shall meet the site Information Security policy. |
| URS-SEC-03 | H | R1 | Removable media (USB drives, optical disks) shall be blocked except for vendor-approved engineering use under change control. |
| URS-SEC-04 | M | R2 | Anti-malware definitions shall be updated daily and reported to the IT compliance dashboard. |
| URS-SEC-05 | M | R2 | The Windows firewall shall be enabled with the GMP-segment ruleset deployed via Group Policy. |

### 5.12 Training

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | No user shall be granted production access until role-specific training has been completed and recorded in the site LMS (Cornerstone OnDemand). |
| URS-TRN-02 | M | R2 | Annual refresher training shall be required for all named users. |

### 5.13 Periodic Review

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PR-01 | H | R1 | A periodic review shall be performed at least annually, examining: configuration drift, audit-trail review evidence, deviations / change controls, backup-restore test evidence, training currency, continued fitness for use. |
| URS-PR-02 | M | R2 | The periodic review shall be signed by the QC Manager and the QA Manager. |

### 5.14 System Suitability and Tune Verification per USP <730>

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-SST-01 | H | R1 | Per USP <730> (Plasma Spectrochemistry), the system shall execute a tune-verification injection at sequence start to assess sensitivity (cps for ¹¹⁵In or ²⁰⁹Bi), oxide ratio (CeO⁺/Ce⁺ ≤ 2-3% typical), and doubly-charged-ion ratio (Ba²⁺/Ba⁺ ≤ 3% typical); criteria method-bound. |
| URS-SST-02 | H | R1 | The system shall record tune-verification observed values vs criteria as a discrete record bound to the sequence; failure shall block sample acquisition until tune corrective action is documented and tune is repeated. |
| URS-SST-03 | M | R2 | The system shall require bracketed tune-verification for sequences ≥ 60 injections (bracket-end tune-check); failure shall flag bracketed results as suspect. |
| URS-SST-04 | H | R1 | The system shall capture USP <233> System Suitability per Procedure 1 / Procedure 2 — drift control standard (DCS) ± 20% of expected concentration at start and end of analytical run; failure blocks release. |

### 5.15 Interference Correction, Internal Standards, and Drift Monitoring

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-INTF-01 | H | R1 | The system shall apply method-bound polyatomic-interference correction equations (mathematical correction) for known interferences (e.g., ⁴⁰Ar¹⁶O⁺ on ⁵⁶Fe; ⁴⁰Ar¹²C⁺ on ⁵²Cr; ⁴⁰Ar²³Na⁺ on ⁶³Cu); equation set version-controlled. |
| URS-INTF-02 | H | R1 | The system shall apply Kinetic Energy Discrimination (KED) helium collision-cell mode per the method for analytes where polyatomic interference removal is mandated. |
| URS-INTF-03 | H | R1 | Internal-standard normalisation shall be applied per analyte (⁴⁵Sc for low-mass, ⁷²Ge / ¹¹⁵In for mid-mass, ²⁰⁹Bi for high-mass per ICH Q3D analytical guidance); internal-standard ion-ratio deviation > 30% from initial calibration shall flag the sample as `IS_DRIFT`. |
| URS-INTF-04 | H | R1 | The system shall monitor instrument drift via periodic QC standards (every 10 samples) and flag drift > ± 20% of nominal concentration; drift-flagged batch shall be re-acquired or bracketed re-calibrated per USP <233>. |
| URS-INTF-05 | M | R2 | The system shall capture matrix-matched dilution checks; matrix-effect outside ± 25% shall trigger Method-Owner review. |

### 5.16 Calibration Curve and Quantitation per USP <233>

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-QNT-01 | H | R1 | Per USP <233> Procedure 1 (quantitative), calibration curves shall use ≥ 3 standards per analyte spanning the expected concentration range; linearity r² ≥ 0.99 evaluated automatically. |
| URS-QNT-02 | H | R1 | Per USP <233> Procedure 2 (limit test), the system shall compare sample response to a single calibration standard at the Q3D PDE limit; sample response > standard response shall flag the sample as `EXCEEDS_LIMIT`. |
| URS-QNT-03 | H | R1 | Calibration outliers shall be flagged using validated rules (% back-calculation outside ± 15% of nominal); exclusion of any standard shall require Method-Owner signature with reason. |
| URS-QNT-04 | H | R1 | Results shall be computed in IEEE-754 double precision; ICH Q3D PDE limits per route of administration (oral / parenteral / inhalation) shall be selected per the method-bound `RouteOfAdministration` field; mis-selection blocked. |
| URS-QNT-05 | H | R1 | The system shall flag results at 30%, 50%, and 100% of the PDE limit (Trend / OOT / OOS) per FDA OOS guidance (2022). |

### 5.17 Method Lifecycle and Reprocessing

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-MTH-01 | H | R1 | Methods shall follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE; only EFFECTIVE methods may be selected for GxP runs. |
| URS-MTH-02 | H | R1 | Method state-transitions shall require eSign with Author ≠ Reviewer ≠ Approver. |
| URS-MTH-03 | H | R1 | Reprocessing with a new processing-method shall create a new `ProcessedResult` artefact pointing to the original `RawData`; lineage retained. |
| URS-MTH-04 | M | R2 | A method's bound interference-equation-set, internal-standard list, and calibration-standard inventory shall be captured in the method record. |

### 5.18 Sample Preparation Linkage

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PREP-01 | H | R1 | Each sample run shall reference the digestion-batch record (Milestone UltraWAVE) by digestion-batch-id; missing reference blocks GxP run. |
| URS-PREP-02 | H | R1 | Dilution factor shall be captured per sample; computed concentration shall account for the dilution factor without rounding intermediate values. |
| URS-PREP-03 | M | R2 | Sample-preparation deviations (digestion incomplete, transfer loss) shall be flagged on the sample record and propagated to the result. |

### 5.19 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem; conditional-access policy `Lab-Workstation Conditional Access (MFA on interactive logon)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the ICP-MS data system DB; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 7 y (≥ 25 y if release-linked) per the consuming-record schedule. |

## 6. Acceptance Criteria

The system shall be accepted into validated routine GMP use when:

1. The FS, CS, RA, IQ, OQ, PQ Protocols have been authored and approved.
2. The IQ has been executed and all critical findings closed.
3. The OQ has been executed and all critical and major findings closed; minor findings have a documented disposition.
4. The PQ has been executed and all critical and major findings closed.
5. The Validation Summary Report has been authored and approved by the QC Manager and the QA Manager.
6. All named users for go-live have completed training.
7. The RTM shows every URS requirement mapped to at least one approved test case.

## 7. Constraints

- The system shall not introduce custom code (Category 5) without a separate Cat-5 assessment.
- Vendor patches and SCN/SP releases shall be evaluated under change control before deployment.
- Direct internet access from the workstation is not permitted.
- Argon and helium supply purity shall meet Thermo Fisher's published recommendations (≥ 99.999% Ar; ≥ 99.999% He).

## 8. Assumptions

- Thermo Fisher maintains its internal SDLC and continues to release validated SCN updates.
- Active Directory is itself qualified.
- LabWare LIMS 8 is itself validated under `LIMS-CSV-2025-014`.
- The site SIEM is operational.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10(a/b/c/d/e/g/k), .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .68, .180, .192, .194(a)(8).
- FDA *Guidance for Industry: Investigating Out-of-Specification (OOS) Test Results* (2022).
- FDA *Guidance on Data Integrity and Compliance With cGMP* (2018).

### EU
- EU GMP Annex 11 — Computerised Systems §§ 4, 6, 9, 11.
- EudraLex Volume 4.

### USP — primary text for elemental impurities + plasma spectrochemistry
- USP <232> — Elemental Impurities — Limits.
- USP <233> — Elemental Impurities — Procedures (Procedure 1 quantitative; Procedure 2 limit test).
- USP <730> — Plasma Spectrochemistry (ICP-OES / ICP-MS).
- USP <1058> — Analytical Instrument Qualification (AIQ); ICP-MS is Group C (complex instrument).
- USP <1224>-<1226>.

### International — ICH
- ICH Q3D(R2) — Guideline for Elemental Impurities (PDE per route of administration: oral, parenteral, inhalation).
- ICH Q2(R2) — Validation of Analytical Procedures.
- ICH Q9(R1) — Quality Risk Management.
- ICH Q14 — Analytical Procedure Development.

### Industry guidance
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE GAMP GPG: *Validation of Laboratory Computerized Systems*.
- ISPE GAMP GPG: *Records and Data Integrity*.
- PIC/S PI 041 — Good Practices for Data Management and Integrity.

### Vendor
- Thermo Fisher — *Qtegra ISDS 2.10 Installation and Configuration Reference*.
- Thermo Fisher — *TraceCERT and Pharma Compliance Plugin Reference*.
- Thermo Fisher — *iCAP RQ + Cetac ASX-560 Hardware Reference + Maintenance Guide*.
- Milestone — *UltraWAVE Closed-Vessel Microwave Digestion Reference* (sample-prep linkage).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

