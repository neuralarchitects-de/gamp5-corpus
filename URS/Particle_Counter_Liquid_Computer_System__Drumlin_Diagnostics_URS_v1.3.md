---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "PharmaDevils QC instrument URS family"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11; EU GMP Annex 11"
  - "USP <788> Particulate Matter in Injections (Method 1 light-obscuration + Method 2 microscopic)"
  - "USP <789> Particulate Matter in Ophthalmic Solutions"
  - "USP <1058> Analytical Instrument Qualification"
  - "Ph. Eur. 2.9.19 Particulate Contamination: Sub-visible Particles"
  - "ISO 21501-3:2019 Determination of particle size distribution — single particle light interaction methods — Part 3: Light extinction liquid-borne particle counter"
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

## Liquid Particle Counter Computer System — Beckman Coulter HIAC 9703+ + PharmSpec 5

**Document Number:** DRD-URS-PCL-001
**Version:** 1.2
**Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Drumlin Diagnostics Ltd, QC Microbiology / Particulates Lab, Edinburgh, United Kingdom *(fictional)*
**System Owner:** QC Manager — Particulates
**Process Owner:** Head of Quality Control
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Beckman Coulter HIAC 9703+ + PharmSpec 5** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a)/(d)/(e)/(k), .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .160, .165, .192, .194; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <788> Method 1; USP <789>; USP <1058>; Ph. Eur. 2.9.19; ISO 21501-3:2019; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Particulates) | _____________ | _____________ | _____ |
| Reviewer (IT / System Administrator) | _____________ | _____________ | _____ |
| Reviewer (Quality Assurance) | _____________ | _____________ | _____ |
| Approver (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | Authored to Tier T1 (Cat 4 standalone particle counter, limited config surface; 45-req target). New § 5 subsections: USP <788> / <789> / Ph. Eur. 2.9.19 / ISO 21501-3 compendial; AIQ DQ/IQ/OQ/PQ per USP <1058>; SST + counted-bead reference verification; reference standard + traceability lifecycle; sample-handling / diluent control; reportable result + OOS detection; per-clause Part 11 + ALCOA+. |

## Definitions

| Term | Definition |
|---|---|
| HIAC 9703+ | Beckman Coulter HIAC liquid particle counter, model 9703+ |
| PharmSpec 5 | Beckman Coulter PharmSpec software, version 5 |
| LO | Light Obscuration — USP <788> Method 1 / Ph. Eur. 2.9.19 Method 1 |
| MM | Microscopic Method — USP <788> Method 2 / Ph. Eur. 2.9.19 Method 2 (out-of-scope at v1.2) |
| Sample volume | Method-defined drawn volume per run (typical 1 mL with 4 replicates for SVP, ≥ 5 mL for LVP) |
| Counted-bead suspension | NIST-traceable polystyrene size + count reference standard for SST / OQ (typical 10-µm size with certified concentration) |
| Sensor blank | Method-defined particulate-free water run to verify background |
| LVP | Large-Volume Parenteral (typically ≥ 100 mL); per-container limits per USP <788> |
| SVP | Small-Volume Parenteral (typically < 100 mL); cumulative-volume-based limits per USP <788> |
| LIMS | LabWare LIMS 8 |
| RFC | Reason-for-change captured rationale on data modification |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| OOS | Out-of-Specification result per 21 CFR § 211.192 |

## 1. Purpose

This URS defines requirements for the liquid particle counter computer system used to quantify sub-visible particulates (≥ 10 µm and ≥ 25 µm thresholds, with extended channels per method) in parenteral and ophthalmic products at Drumlin Diagnostics QC. The system performs USP <788> Method 1 (Light Obscuration), USP <789> ophthalmic-solution testing, and Ph. Eur. 2.9.19 equivalent measurements; the instrument is qualified per ISO 21501-3 single-particle light-extinction performance criteria.

## 2. Scope

**In:** one HIAC 9703+ instrument with auto-sampler; dedicated workstation (Dell OptiPlex 7080, Windows 11 Pro 23H2) running PharmSpec 5; AD authentication on `drumlin.local`; LIMS integration via PharmSpec LIMS Connector 4; daily backup; site NTP sync; SST procedures (counted-bead, sensor blank, sample-volume accuracy); reference-standard register (NIST-traceable counted beads, sizing beads).

**Out:** sample preparation (manual SOP); off-line calibration of size standards (laboratory chain); LIMS-side sample lifecycle (`LIMS-CSV-2024-014`); USP <788> Method 2 microscopic testing (separate URS / facility); PharmSpec 5 SDLC (Beckman Coulter-owned per Cat 4).

## 3. System Description and Intended Use

The system performs LO-based sub-visible particulate counting per USP <788> Method 1, USP <789>, and Ph. Eur. 2.9.19. PharmSpec controls the sampler, applies the configured method, captures replicate particle counts, applies dilution factors, evaluates against compendial limits (≥ 10 µm and ≥ 25 µm thresholds; extended channels available), and routes results to LIMS. GAMP Cat 4: Beckman Coulter maintains the SDLC; site validation focuses on installation, configuration, intended-use, Part 11 controls, SST + counted-bead lifecycle, and the LIMS interface.

Intended use: release testing of LVP and SVP parenterals, ophthalmic solutions, and in-process samples where sub-visible particulate counts are a specification.

## 4. User Roles

| Role | Permissions |
|---|---|
| Analyst | Acquire and process; cannot edit method or system configuration. |
| Senior Analyst | All Analyst + second-person review. |
| Method Owner | Author / edit methods under change control. |
| QC Manager | Approve, lock, release results to LIMS. |
| System Administrator | OS / patch / AD groups; cannot approve. |
| Reference Standard Custodian | Receive / log / dispose counted-bead and sizing-bead suspensions. |
| Auditor | Read-only across data and audit trails. |

**Separation of Duties:** Analyst ≠ Reviewer ≠ Approver of the same result. Reference Standard Custodian ≠ Analyst on same SST.

## 5. User Requirements

### 5.1 Hardware / Installation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HW-01 | H | R1 | The system shall be installed on a dedicated workstation; shared workstations are prohibited. |
| URS-HW-02 | H | R1 | The workstation shall meet PharmSpec 5 minimum specification. |
| URS-HW-03 | H | R1 | The workstation shall be on UPS for ≥ 30 min controlled shutdown. |
| URS-HW-04 | H | R1 | The lab shall maintain NIST-traceable counted-bead and sizing-bead suspensions for periodic verification per a documented schedule. |
| URS-HW-05 | M | R2 | The instrument shall be sited in a low-particle environment (ISO Class 8 or better at the open-cup sampling area) with monitored background. |

### 5.2 Software Configuration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SW-01 | H | R1 | The OS shall be Windows 11 Pro 23H2, domain-joined to `drumlin.local`; QC users shall not have local-admin. |
| URS-SW-02 | H | R1 | PharmSpec 5 shall be installed by Beckman Coulter or a Beckman-trained engineer. |
| URS-SW-03 | H | R1 | Project storage shall reside on `\\drd-gmp-fs01\hiac-projects`. |
| URS-SW-04 | H | R1 | The clock shall be synced to `ntp.drumlin.local`; skew shall be monitored with alert at > 1 s. |
| URS-SW-05 | H | R1 | PharmSpec 5 Part 11 settings (audit trail, e-sign, raw data lock) shall be configured per the Configuration Specification. |
| URS-SW-06 | M | R2 | Vendor patches (Beckman Coulter PharmSpec 5 SCN) shall be applied only after site change-control approval. |

### 5.3 USP <788> / <789> / Ph. Eur. 2.9.19 / ISO 21501-3 Compendial Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CMP-01 | H | R1 | The system shall implement USP <788> Method 1 acceptance: LVP per-container limits 25 / mL (≥ 10 µm) and 3 / mL (≥ 25 µm); SVP cumulative-volume limits 6000 / container (≥ 10 µm) and 600 / container (≥ 25 µm). |
| URS-CMP-02 | H | R1 | The system shall implement USP <789> ophthalmic-solution limits 50 / mL (≥ 10 µm), 5 / mL (≥ 25 µm), 2 / mL (≥ 50 µm). |
| URS-CMP-03 | H | R1 | The system shall implement Ph. Eur. 2.9.19 Test 1A and 1B acceptance criteria when used for EP-monograph products. |
| URS-CMP-04 | H | R1 | The instrument shall meet ISO 21501-3:2019 performance criteria: size accuracy ± 10% at calibrated channels; counting efficiency 50% ± 20% at the size-threshold and 100% ± 10% above 1.5× threshold; coincidence loss ≤ 10% at operational concentration. |
| URS-CMP-05 | M | R2 | Compendial method designations (USP-NF, Ph. Eur., JP) shall be captured in the method header. |

### 5.4 AIQ — DQ / IQ / OQ / PQ per USP <1058>

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AIQ-01 | H | R1 | DQ shall document fitness for intended use against working range, particle size channels, and Part 11 integration. |
| URS-AIQ-02 | H | R1 | IQ shall verify installation, AD bind, PharmSpec 5 build, sensor installation, syringe-pump installation. |
| URS-AIQ-03 | H | R1 | OQ shall include: size accuracy (NIST-traceable sizing beads at 10 + 25 µm), counting accuracy (counted-bead suspension), sample-volume accuracy (gravimetric ± 1%), sensor blank, resolution, coincidence-loss verification per ISO 21501-3. |
| URS-AIQ-04 | H | R1 | PQ shall be executed at go-live, after sensor / syringe-pump replacement, and at least annually. |
| URS-AIQ-05 | M | R2 | A partial PQ (SST only) shall be permitted after routine PM not affecting the sensor. |
| URS-AIQ-06 | M | R2 | Qualification evidence shall be retained ≥ 25 years per product-release tie. |

### 5.5 SST Battery (Counted-Bead + Sensor Blank + Sample Volume)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SST-01 | H | R1 | The SST shall be executed at the start of each session per USP <788> Section 3: (a) counted-bead suspension recovery within manufacturer-specified ± 10%; (b) sensor blank ≤ method limit (typical ≤ 25 particles ≥ 10 µm per 5 mL); (c) sample-volume accuracy gravimetric ± 1%. |
| URS-SST-02 | H | R1 | SST records shall be captured with operator, ts, counted-bead lot, certificate expiry, blank-volume passed, recovery %, verdict. |
| URS-SST-03 | H | R1 | SST failure shall set the instrument to NOT READY; GxP acquisitions shall be blocked until SST re-passes. |
| URS-SST-04 | M | R2 | SST trend (rolling 12 months) shall be reviewed; early-warning band at ± 7% of nominal recovery. |
| URS-SST-05 | M | R2 | Periodic SST review shall be a documented step in the monthly audit-trail review. |

### 5.6 Reference Standard and Traceability Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REF-01 | H | R1 | Counted-bead suspensions (NIST-traceable size + concentration) and sizing-bead standards shall be logged with lot, source, COA, NIST traceability, receipt date, opening date, expiry, custodian. |
| URS-REF-02 | H | R1 | The system shall block SST start when bound reference standard is expired. |
| URS-REF-03 | M | R2 | The Reference Standard Custodian shall maintain a register integrated with PharmSpec such that SST execution captures the reference-standard ID. |
| URS-REF-04 | M | R2 | Disposal of expired counted-bead suspensions shall be logged. |

### 5.7 Sample Handling / Diluent Controls

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SAMP-01 | H | R1 | The diluent / particle-free water lot used for blanks and dilutions shall be logged; each batch shall be verified ≤ method limit at the start of each session. |
| URS-SAMP-02 | M | R2 | Open-cup vs closed sampling mode shall be method-bound; environment particulate background shall be controlled to ISO Class 8 or better. |
| URS-SAMP-03 | M | R2 | Sample-degassing (per method specification) shall be captured per acquisition; bubbles shall be detected and flagged. |
| URS-SAMP-04 | M | R2 | Container-to-sampler transfer methodology (probe immersion depth, swirl pattern) shall be method-bound and trained. |

### 5.8 Acquisition / Processing / Reportable Result + OOS

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ACQ-01 | H | R1 | Methods shall follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE; only EFFECTIVE methods may be selected. |
| URS-ACQ-02 | H | R1 | The system shall reject the start of a sequence when instrument not Ready, SST overdue / failed, no approved method, project locked, expired reference standard / diluent bound. |
| URS-ACQ-03 | H | R1 | Each acquisition shall capture sample ID, dilution factor, vessel ID, replicate count, method ID + version, instrument ID, analyst, timestamp. |
| URS-PROC-01 | H | R1 | The system shall apply the approved processing method (replicate averaging, outlier handling per USP <788>; first-replicate discard rule when method-defined). |
| URS-PROC-02 | H | R1 | Manual reprocessing shall require captured RFC. |
| URS-PROC-03 | H | R1 | Raw data shall be preserved; processing shall produce derived records. |
| URS-PROC-04 | H | R1 | The system shall compare cumulative counts to compendial limits; flag at 30 / 50 / 100% of limit (trend / OOT / OOS). |
| URS-PROC-05 | H | R1 | The system shall generate a PDF report including raw counts per replicate, dilution-corrected counts, SST status, limit status, ALCOA+ statement, SHA-256 hash. |
| URS-PROC-06 | M | R2 | An OOS shall trigger downstream § 211.192 investigation (delegated to LIMS) and shall set sample-state to HOLD. |

### 5.9 Audit Trail / Part 11 / Data Integrity

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | The audit trail shall be time-stamped and secure. |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only; admin update / delete shall be cryptographically prevented. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be conducted by Senior Analyst per batch and QC Manager monthly. |
| URS-AUD-04 | H | R1 | Retention shall be ≥ 7 years; ≥ 25 years if linked to product release. |
| URS-PART11-01 | H | R1 | The system shall implement procedural controls per 21 CFR § 11.10(a). |
| URS-PART11-02 | H | R1 | The system shall limit access to authorised individuals per § 11.10(d). |
| URS-PART11-03 | H | R1 | E-signatures shall manifest per § 11.50. |
| URS-PART11-04 | H | R1 | Signatures shall be linked to records per § 11.70. |
| URS-PART11-05 | H | R1 | Signatures shall be unique per § 11.100. |
| URS-PART11-06 | H | R1 | Identity-based signature components shall require re-authentication per § 11.200. |
| URS-PART11-07 | H | R1 | Password and credential controls per § 11.300 shall apply. |
| URS-DI-01 | H | R1 | Records shall be Attributable. |
| URS-DI-02 | H | R1 | Records shall be Legible (PDF export). |
| URS-DI-03 | H | R1 | Records shall be Contemporaneous. |
| URS-DI-04 | H | R1 | Originals shall be preserved. |
| URS-DI-05 | H | R1 | Calculations shall be Accurate. |
| URS-DI-06 | M | R2 | Records shall be Complete / Consistent / Enduring / Available. |

### 5.10 LIMS Interface

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-LIMS-01 | H | R1 | Worklists shall be imported from LIMS via the PharmSpec Connector (read-only). |
| URS-INT-LIMS-02 | H | R1 | Approved results shall be pushed to LIMS only after QC Manager approval. |
| URS-INT-LIMS-03 | H | R1 | The LIMS-bound result shall include report ID, instrument ID, method ID + version, reviewer / approver, SST status. |
| URS-INT-LIMS-04 | M | R2 | The interface shall reject result push when SST is failed / expired. |

### 5.11 Backup / DR / Performance / Security / Training / PR

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | Daily backup with checksum verification shall be executed. |
| URS-BAK-02 | H | R1 | A quarterly restore test shall be witnessed. |
| URS-BAK-03 | M | R2 | RTO shall be ≤ 8 business hours; RPO ≤ 24 hours. |
| URS-PERF-01 | M | R2 | The system shall sustain acquisition for a typical batch session without crash or data loss. |
| URS-SEC-01 | H | R1 | Domain accounts shall be the only authentication path; local accounts disabled (except break-glass). |
| URS-SEC-02 | H | R1 | Removable media shall be blocked except by approved exception. |
| URS-TRN-01 | H | R1 | Production access shall require LMS-recorded role-specific training; SST + reference-standard training annual. |
| URS-PR-01 | H | R1 | An annual periodic review shall cover method inventory, audit-trail review evidence, SST trend, counted-bead register health, deviations, training; signed by QC Manager + Head of QA. |

### 5.12 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem; conditional-access policy `Lab-Workstation Conditional Access (MFA on interactive logon)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T3 with RPO ≤ 72 h and RTO ≤ 72 BH; backup integration shall use Veeam file-level capture of the per-instrument result store and configuration; the application team shall participate in annual application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 7 y per the consuming-record schedule. |

## 6. Acceptance Criteria

CS, RA, IQ, OQ (USP <788> SST + ISO 21501-3 size + counting efficiency + sample-volume accuracy + coincidence-loss), PQ approved and executed; PQ includes counted-bead reference verification meeting USP <788> Section 3 criteria; VSR approved; RTM closed at 100% URS-ID coverage.

## 7. Constraints

- Vendor patches under change control.
- Size-standards calibration current; NIST-traceable supplier list maintained.
- Counted-bead working suspensions short shelf-life per supplier (typical 6 months refrigerated).

## 8. Assumptions

- AD, LIMS, NTP, NIST-traceable size-standards provider current.
- PharmSpec 5 SDLC evidence is available via the vendor.

## 9. References

**US / FDA:**
- 21 CFR Part 11 §§ .10(a)/(b)/(c)/(d)/(e)/(k), .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .68, .160, .165, .192, .194
- FDA *Guidance on Data Integrity and Compliance with cGMP* (2018)

**EU / EMA:**
- EU GMP Annex 11 §§ 4, 6, 9, 11
- Ph. Eur. 2.9.19 — Particulate Contamination: Sub-visible Particles
- EudraLex Volume 4 — GMP Parts I + III

**International:**
- USP <788> — Particulate Matter in Injections (Methods 1 + 2)
- USP <789> — Particulate Matter in Ophthalmic Solutions
- USP <1058> — Analytical Instrument Qualification
- USP <1225> — Validation of Compendial Procedures
- ISO 21501-3:2019 — Determination of particle size distribution — Single particle light interaction methods — Part 3: Light extinction liquid-borne particle counter
- ICH Q2(R2) — Validation of Analytical Procedures
- PIC/S PI 041
- ISPE GAMP 5 (2nd Edition, 2022)

**Vendor:**
- Beckman Coulter — *HIAC 9703+ Configuration Reference* (current rev.)
- Beckman Coulter — *PharmSpec 5 Installation, Configuration, and Administration Reference*
- Beckman Coulter — *PharmSpec 5 21 CFR Part 11 Compliance Guide*

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

