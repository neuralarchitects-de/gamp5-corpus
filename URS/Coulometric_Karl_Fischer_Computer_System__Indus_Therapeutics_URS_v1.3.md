---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "PharmaDevils Karl Fischer URS family"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11; EU GMP Annex 11"
  - "USP <921> Water Determination Method Ic"
  - "Ph. Eur. 2.5.32 Water: Micro Determination"
  - "USP <1058> Analytical Instrument Qualification"
  - "ICH Q2(R2); PIC/S PI 041"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Coulometric Karl Fischer Computer System — Mettler Toledo C30S + LabX 2024

**Document Number:** IND-URS-CKF-001
**Version:** 1.2
**Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Indus Therapeutics Pvt Ltd, QC Chemical Lab, Hyderabad, Telangana, India *(fictional)*
**System Owner:** QC Manager — Chemical
**Process Owner:** Head of Quality Control
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Mettler Toledo C30S + LabX 2024** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a)/(d)/(e), .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .160, .165, .194; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <921> Method Ic (Coulometric); USP <1058> AIQ; Ph. Eur. 2.5.32; ICH Q2(R2); PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Chemical) | _____________ | _____________ | _____ |
| Reviewer (IT / System Administrator) | _____________ | _____________ | _____ |
| Reviewer (Quality Assurance) | _____________ | _____________ | _____ |
| Approver (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | Authored to Tier T1 (Cat 4 simple titrator with limited config surface; 40-req target). New § 5 subsections: USP <921> / Ph. Eur. 2.5.32 compendial compliance; AIQ DQ/IQ/OQ/PQ per USP <1058>; SST + drift / blank management; reagent + titrant lifecycle; per-clause Part 11 + ALCOA+. |

## Definitions

| Term | Definition |
|---|---|
| KF | Karl Fischer titration |
| Coulometric KF | KF Method Ic — water consumed by iodine generated electrochemically; suitable for low-water samples (typical 10 µg–10 mg H₂O / sample, 0.001–5% w/w) |
| Volumetric KF | KF Method Ia — water titrated by Karl Fischer reagent of known iodine titre; suitable for high-water samples (out of scope; see future URS) |
| C30S | Mettler Toledo C30S coulometric Karl Fischer titrator |
| LabX 2024 | Mettler Toledo LabX 2024 instrument-management software |
| Anolyte / Catholyte | KF cell reagents in the diaphragm cell (anolyte = methanol-imidazole-SO₂ formulation; catholyte = catholyte solution) |
| Drift | Background-water introduction rate measured before titration (µg H₂O / min); USP <921> threshold typically ≤ 25 µg / min for cells in use |
| Blank | Pre-titration consumption equivalent attributable to background water in the reagent and cell |
| Water standard | Certified water-standard solution (e.g. Hydranal Water Standard 1.0 / 10 / 100 / 1000, NIST-traceable) used for SST + accuracy verification |
| LIMS | LabWare LIMS 8 |
| RFC | Reason-for-change captured rationale on data modification |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| OOS | Out-of-Specification result per 21 CFR § 211.192 |

## 1. Purpose

This URS defines requirements for the coulometric Karl Fischer titrator computer system used to determine water content (Method Ic) in API and finished products at the Indus Therapeutics QC Chemical Lab. The system supports compendial water-content testing per USP <921> Method Ic and Ph. Eur. 2.5.32, with reagent and cell lifecycle controls that protect against the most common KF failure modes: cell-drift inflation, expired reagent, and blank-correction drift.

## 2. Scope

**In:** one Mettler Toledo C30S titrator; dedicated workstation (Lenovo ThinkCentre M70t, Windows 11 Pro 23H2) running LabX 2024 with the LIMS Connector module; LIMS integration to LabWare LIMS 8; AD authentication on `indus.local`; daily backup; NTP sync; reagent / titrant register (anolyte, catholyte, water standards); USP <921> SST procedures.

**Out:** sample preparation (manual SOP); LIMS sample-lifecycle (sample login, COA generation); LabX 2024 SDLC (Mettler-owned per GAMP Cat 4); cell maintenance hardware procedures (Engineering SOP).

## 3. System Description and Intended Use

The system performs coulometric KF titration per USP <921> Method Ic / Ph. Eur. 2.5.32. LabX controls the titrator, applies the configured method, captures replicate water-content values, applies blank correction, and reports values against the assigned specification. GAMP Cat 4: Mettler Toledo maintains LabX SDLC; site validation focuses on installation, configuration, intended-use, Part 11, reagent / titrant lifecycle, and the LIMS interface.

Intended use: water determination for API release, finished-product release, in-process control, and stability time-points where water content is a specification.

## 4. User Roles

| Role | Permissions |
|---|---|
| Analyst | Acquire and process; cannot edit method or system configuration. |
| Senior Analyst | All Analyst + second-person review (audit-trail per batch). |
| Method Owner | Author / edit methods under change control. |
| QC Manager | Approve, lock, release results to LIMS. |
| System Administrator | OS / patch / AD groups; cannot approve. |
| Reagent Custodian | Log / dispose reagents and water standards. |
| Auditor | Read-only across data and audit trails. |

**Separation of Duties:** Analyst ≠ Reviewer ≠ Approver. Reagent Custodian ≠ Analyst on same run.

## 5. User Requirements

### 5.1 Hardware / Software Configuration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HW-01 | H | R1 | The system shall be installed on a dedicated workstation; shared workstations are prohibited. |
| URS-HW-02 | H | R1 | The workstation shall meet LabX 2024 minimum specification and shall be on UPS for ≥ 30 min controlled shutdown. |
| URS-HW-03 | M | R2 | The titrator shall be sited in a low-humidity environment (≤ 60% RH typical) with bench-top monitoring; high-humidity events shall be logged. |
| URS-SW-01 | H | R1 | The OS shall be Windows 11 Pro 23H2, domain-joined to `indus.local`; QC users shall not have local-admin. |
| URS-SW-02 | H | R1 | LabX 2024 + LIMS Connector shall be installed by Mettler Toledo or a Mettler-trained engineer. |
| URS-SW-03 | H | R1 | Project storage shall reside on `\\ind-gmp-fs01\labx-projects`; local C: shall not retain GxP data. |
| URS-SW-04 | H | R1 | The clock shall be synced to `ntp.indus.local`; skew shall be monitored with alert at > 1 s. |
| URS-SW-05 | H | R1 | LabX Part 11 settings (audit trail, e-sign, raw data lock) shall be configured per the Configuration Specification. |

### 5.2 USP <921> / Ph. Eur. 2.5.32 Compendial Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CMP-01 | H | R1 | The system shall execute Method Ic per USP <921> with electrochemically generated iodine, with current measurement and water-content calculation per the 96485 C / mol electron-equivalent stoichiometry. |
| URS-CMP-02 | H | R1 | The system shall meet Ph. Eur. 2.5.32 control criteria for micro-determination of water when used for EP-monograph methods. |
| URS-CMP-03 | H | R1 | Water-standard recovery shall meet ± 3% of nominal per USP <921> at the start of each session and after major maintenance events. |
| URS-CMP-04 | M | R2 | Compendial method designations (USP-NF, Ph. Eur., JP) shall be captured in the method header. |

### 5.3 AIQ — DQ / IQ / OQ / PQ per USP <1058>

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AIQ-01 | H | R1 | DQ shall document fitness for intended use against the water-content working range, the relevant compendial monographs, and Part 11 integration. |
| URS-AIQ-02 | H | R1 | IQ shall verify installation, AD bind, LabX build, cell installation, electrode integrity. |
| URS-AIQ-03 | H | R1 | OQ shall include: cell-drift verification, blank-determination, water-standard recovery accuracy (± 3% at 100 µg, 1000 µg levels), precision (RSD ≤ 3% on replicate water-standard injections), linearity across the working range. |
| URS-AIQ-04 | H | R1 | PQ shall be executed at go-live, after cell-fluid replacement / electrode replacement / software upgrade, and at least annually. |

### 5.4 SST + Drift / Blank Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SST-01 | H | R1 | At session start, the system shall measure cell drift; runs shall be blocked when drift exceeds the method-defined threshold (typically ≤ 25 µg / min for routine use, ≤ 10 µg / min for low-water samples). |
| URS-SST-02 | H | R1 | At session start, water-standard recovery shall be verified within ± 3% per USP <921>; failure shall block GxP runs. |
| URS-SST-03 | H | R1 | Blank determination shall be performed per the method-defined cadence; blank value shall be captured per acquisition. |
| URS-SST-04 | M | R2 | Drift and blank shall be trended across rolling 30 days; an alert shall fire when 7-day rolling average exceeds ½ the SOP threshold (early-warning band). |
| URS-SST-05 | M | R2 | SST results shall be recorded with operator, timestamp, water-standard lot, certificate expiry, and pass / fail. |

### 5.5 Reagent / Titrant Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REA-01 | H | R1 | Anolyte and catholyte lot, source, COA, receipt date, opening date, and expiry shall be logged in a register integrated with LabX. |
| URS-REA-02 | H | R1 | Expired reagent shall be blocked at session start. |
| URS-REA-03 | H | R1 | Cell-fluid change shall require operator entry of new lot ID + opened-date; the system shall block runs when reagent lot is not registered. |
| URS-REA-04 | M | R2 | Water standards (Hydranal 1.0 / 10 / 100 / 1000) shall be logged with lot, expiry, opened-date; the system shall block use of expired standards. |
| URS-REA-05 | M | R2 | Disposal of cell waste shall be logged per site EHS SOP. |

### 5.6 Method and Run Execution

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-METH-01 | H | R1 | Methods shall follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE; only EFFECTIVE methods may be selected. |
| URS-METH-02 | H | R1 | Method state transitions shall require role-restricted e-signatures (Author ≠ Approver). |
| URS-RUN-01 | H | R1 | The system shall reject the start of a sequence when drift > threshold (URS-SST-01), water-standard recovery is overdue / failed, expired reagent / standard is bound, no approved method, or the project is locked. |
| URS-RUN-02 | H | R1 | The system shall capture sample-injection metadata: sample ID, weight, blank correction, method ID + version, instrument ID, analyst, timestamp. |
| URS-RUN-03 | H | R1 | The system shall reject manual reweigh / re-run unless a captured RFC is provided. |
| URS-RUN-04 | M | R2 | Replicate count and acceptance RSD shall be method-defined; runs not meeting the acceptance RSD shall be flagged. |

### 5.7 Processing / Reporting / OOS Detection

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PROC-01 | H | R1 | The system shall apply the approved processing method (mean, %RSD across replicates) and shall apply blank correction. |
| URS-PROC-02 | H | R1 | Raw data shall be preserved unaltered; reprocessing shall produce a derived record referencing the original raw_id. |
| URS-PROC-03 | H | R1 | The system shall compare result to spec and shall flag at 30 / 50 / 100% of limit (trend / OOT / OOS); OOS flag shall trigger downstream § 211.192 investigation (delegated to LIMS). |
| URS-PROC-04 | H | R1 | The system shall generate a PDF report including raw values per replicate, mean, %RSD, blank, drift, water-standard recovery, limit status, ALCOA+ statement, and SHA-256 hash. |

### 5.8 Audit Trail / Part 11 / Data Integrity

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | The audit trail shall be time-stamped, secure, and shall cover methods, sequences, results, configuration, reagent register, and signature events. |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only; admin update / delete shall be cryptographically prevented. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be conducted by a Senior Analyst per batch and by the QC Manager monthly. |
| URS-AUD-04 | H | R1 | Audit-trail retention shall be ≥ 7 years; ≥ 25 years if linked to product release. |
| URS-PART11-01 | H | R1 | The system shall implement procedural controls per 21 CFR § 11.10(a). |
| URS-PART11-02 | H | R1 | The system shall limit access to authorised individuals per § 11.10(d). |
| URS-PART11-03 | H | R1 | E-signatures shall manifest name, date / time, and meaning per § 11.50. |
| URS-PART11-04 | H | R1 | Signatures shall be linked to records per § 11.70. |
| URS-PART11-05 | H | R1 | Signatures shall be unique per § 11.100. |
| URS-PART11-06 | H | R1 | Identity-based signature components shall require re-authentication at signing per § 11.200. |
| URS-PART11-07 | H | R1 | Password and credential controls per § 11.300 shall apply. |
| URS-DI-01 | H | R1 | Data shall be Attributable. |
| URS-DI-02 | H | R1 | Data shall be Legible. |
| URS-DI-03 | H | R1 | Data shall be Contemporaneous (NTP timestamps). |
| URS-DI-04 | H | R1 | Data shall be Original (raw preserved). |
| URS-DI-05 | H | R1 | Calculations shall be Accurate (blank + drift gate verified per OQ). |

### 5.9 LIMS Interface / Backup / Performance / Security / Training / PR

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-LIMS-01 | H | R1 | The system shall import worklists from LIMS (read-only). |
| URS-INT-LIMS-02 | H | R1 | Approved results shall be pushed to LIMS only after QC Manager approval. |
| URS-INT-LIMS-03 | M | R2 | The interface shall reject result push when SST is failed / expired. |
| URS-BAK-01 | H | R1 | Daily backup with checksum shall be executed. |
| URS-BAK-02 | H | R1 | A quarterly restore test shall be witnessed and recorded. |
| URS-PERF-01 | M | R2 | The system shall sustain acquisition for a typical batch session without crash or data loss. |
| URS-SEC-01 | H | R1 | Authentication shall be via domain accounts only (break-glass excepted). |
| URS-SEC-02 | H | R1 | Removable media shall be blocked except for vendor-approved engineering use under change control. |
| URS-TRN-01 | H | R1 | LMS-recorded training shall be required; SST + reagent-lifecycle training annual. |
| URS-PR-01 | H | R1 | An annual periodic review shall cover method inventory, audit-trail review evidence, SST + reagent register health, deviations, training; signed by QC Manager + Head of QA. |

### 5.10 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem; conditional-access policy `Lab-Workstation Conditional Access (MFA on interactive logon)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T3 with RPO ≤ 72 h and RTO ≤ 72 BH; backup integration shall use Veeam file-level capture of the per-instrument result store and method library; the application team shall participate in annual application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 7 y per the consuming-record schedule. |

## 6. Acceptance Criteria

CS, RA, IQ, OQ (USP <921> water-standard recovery ± 3%, drift / blank verification), PQ approved and executed; VSR approved by QC Manager + Head of QA; RTM closed at 100% URS-ID coverage.

## 7. Constraints

- Vendor patches under change control.
- Anolyte / catholyte from approved supplier list only.
- Water-standard supply chain: Hydranal-grade NIST-traceable per supplier list.

## 8. Assumptions

- AD, LIMS, NTP are validated.
- KF reagent and water-standard supply chain traceable.
- LabX 2024 SDLC evidence is available via the vendor.

## 9. References

**US / FDA:**
- 21 CFR Part 11 §§ .10(a)/(b)/(c)/(d)/(e)/(k), .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .68, .160, .165, .192, .194
- FDA *Guidance on Data Integrity and Compliance with cGMP* (2018)

**EU / EMA:**
- EU GMP Annex 11 §§ 4, 6, 9, 11
- Ph. Eur. 2.5.32 — Water: Micro Determination
- EudraLex Volume 4 — GMP Parts I + III

**International:**
- USP <921> Water Determination (Method Ic Coulometric Titration)
- USP <1058> Analytical Instrument Qualification
- USP <1225> Validation of Compendial Procedures
- ICH Q2(R2) — Validation of Analytical Procedures
- PIC/S PI 041
- ISPE GAMP 5 (2nd Edition, 2022); GAMP GPG *Validation of Laboratory Computerized Systems*

**Vendor:**
- Mettler Toledo — *C30S Coulometric KF Configuration Reference* (current rev.)
- Mettler Toledo — *LabX 2024 Installation, Configuration, and Administration Reference*
- Mettler Toledo — *LabX 2024 21 CFR Part 11 Compliance Guide*

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

