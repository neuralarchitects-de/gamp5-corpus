---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "PharmaDevils Stability-PC / HPLC URS family"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11; EU GMP Annex 11"
  - "USP <643> Total Organic Carbon; USP <645> Water Conductivity; USP <1231> Water for Pharmaceutical Purposes"
  - "USP <1058> Analytical Instrument Qualification"
  - "Ph. Eur. 2.2.44 Total Organic Carbon; Ph. Eur. 0008 Water for Injections; Ph. Eur. 0008/8 Highly Purified Water"
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

## TOC Analyzer Computer System — Sievers M9 + DataPro2 v2.4

**Document Number:** SOL-URS-TOC-001
**Version:** 1.2
**Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Solara Pharmaceuticals SA, Utilities Validation Lab, Plant 3, Mendrisio, Switzerland *(fictional)*
**System Owner:** QC Manager — Utilities
**Process Owner:** Head of Manufacturing Sciences
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Sievers M9 + DataPro2 v2.4** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a)/(d)/(e)/(k), .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .160, .165, .192, .194; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <643> Total Organic Carbon; USP <645> Water Conductivity; USP <1231>; USP <1058>; Ph. Eur. 2.2.44; ICH Q2(R2); PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Utilities) | _____________ | _____________ | _____ |
| Reviewer (IT / System Administrator) | _____________ | _____________ | _____ |
| Reviewer (Quality Assurance) | _____________ | _____________ | _____ |
| Approver (Head of Manufacturing Sciences) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | Authored to Tier T2 (Cat 4 utilities-water TOC analyzer with on-line + grab-sample mode; 60-req target). New § 5 subsections: USP <643> / Ph. Eur. 2.2.44 compendial; AIQ DQ/IQ/OQ/PQ per USP <1058>; SST + system suitability (sucrose / 1,4-benzoquinone); reagent + standard lifecycle; UV-lamp + reactor lifecycle; reportable result + OOS detection; per-clause Part 11 + ALCOA+. |

## Definitions

| Term | Definition |
|---|---|
| TOC | Total Organic Carbon |
| Sievers M9 | Veolia / Sievers M9 lab TOC analyzer (or M9 Portable / M9 Bench / e-series variants) — membrane-conductometric UV-persulfate / UV-only oxidation |
| DataPro2 v2.4 | Sievers DataPro2 software, on-instrument touchscreen + remote workstation client |
| WFI | Water for Injection (USP / Ph. Eur. 0008) |
| PW | Purified Water (USP / Ph. Eur. 0008) |
| HPW | Highly Purified Water (Ph. Eur. legacy 0008/8) |
| TOC limit | 500 ppb (0.50 mg C / L) per USP <643> for bulk WFI / PW / HPW |
| Sucrose | USP <643> system-suitability easy-to-oxidize reference standard (500 ppb prepared from USP RS) |
| 1,4-Benzoquinone | USP <643> system-suitability hard-to-oxidize reference standard (500 ppb prepared from USP RS) |
| Response efficiency | RE = (response_sucrose − response_water_blank) / (response_BQ − response_water_blank) — USP <643> requires 85% ≤ RE ≤ 115% |
| LIMS | LabWare LIMS 8 |
| RFC | Reason-for-change captured rationale on data modification |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| OOS | Out-of-Specification result per 21 CFR § 211.192 |

## 1. Purpose

This URS defines requirements for the TOC analyzer computer system used to release WFI and PW for sterile manufacturing per USP <643> and Ph. Eur. 2.2.44 at the Solara Pharma Plant 3 utilities lab. The system also supports trend monitoring of in-process water-system sample points and may be operated in on-line (continuous sample loop) or grab-sample mode.

## 2. Scope

**In:** one Sievers M9 lab TOC analyzer; dedicated workstation (HP EliteDesk 800 G9, Win 11 Pro 23H2) running DataPro2 v2.4; LIMS integration via DataShare 5; AD authentication on `solara.local`; daily backup; NTP sync; USP <643> SST (sucrose / 1,4-benzoquinone); reagent / standard register; UV-lamp + reactor lifecycle tracking; on-line and grab-sample acquisition modes.

**Out:** sample preparation; water-system loop sanitization (separate validation `UTIL-CSV-2024-009`); on-line conductivity (companion USP <645> separate validation); LIMS sample-lifecycle (`LIMS-CSV-2024-014`); DataPro2 SDLC (Sievers-owned per Cat 4).

## 3. System Description and Intended Use

Trained QC analysts use the system to determine TOC in pharmaceutical-grade water at release and in-process points; results gate water-system release and trigger investigations on excursions per the site Water System SOP. GAMP Cat 4: Sievers / Veolia maintains its SDLC; site validation focuses on installation, configuration, intended-use functionality, Part 11 controls, USP <643> SST configuration, lamp / reactor lifecycle, and the LIMS interface.

```
[WFI / PW sample loop or grab vial] → [Sievers M9 TOC] → [DataPro2 Workstation, Win 11]
                                                                │
                                            AD-authenticated user │── DataShare 5 → LabWare LIMS 8
                                                                ├── Daily backup → site fileserver
                                                                ├── Reagent/Standard register (sucrose / BQ / blank)
                                                                └── NTP sync → ntp.solara.local
```

## 4. User Roles

| Role | Permissions |
|---|---|
| Analyst | Acquire, integrate, process; no method or system-config edits. |
| Senior Analyst | All Analyst permissions + second-person review. |
| Method Owner | Method create / edit under change control. |
| QC Manager | Approve, lock, release results to LIMS. |
| System Administrator | Installation, patching, AD groups; no QC sign-off. |
| Reagent Standard Custodian | Receive / log / dispose USP RS sucrose / 1,4-benzoquinone. |
| Auditor | Read-only across all records and audit trails. |

**Separation of Duties:** Analyst ≠ Reviewer ≠ Approver; Reagent Custodian ≠ Analyst on same SST.

## 5. User Requirements

### 5.1 Hardware / Installation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HW-01 | H | R1 | The system shall be installed on a dedicated workstation; shared workstations are prohibited. |
| URS-HW-02 | H | R1 | The workstation shall meet DataPro2 minimum: ≥ 16 GB RAM, ≥ 500 GB SSD, dedicated USB-3 ports for the M9. |
| URS-HW-03 | H | R1 | The workstation shall be on UPS for ≥ 30 min controlled shutdown. |
| URS-HW-04 | H | R1 | The workstation shall be on the GMP network segment; no office-segment access. |
| URS-HW-05 | M | R2 | UV lamp / reactor / cell parameters (output intensity, lamp hours, reactor temperature) shall be readable from DataPro2 with alarm thresholds per SOP. |
| URS-HW-06 | M | R2 | The sample loop / sample-vial autosampler shall be qualified per Sievers SOP at installation and after any servicing. |

### 5.2 Software Configuration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SW-01 | H | R1 | The OS shall be Windows 11 Pro 23H2, domain-joined to `solara.local`; QC users shall not have local-admin. |
| URS-SW-02 | H | R1 | DataPro2 v2.4 shall be installed by Sievers / Veolia or a Sievers-trained engineer. |
| URS-SW-03 | H | R1 | TOC projects shall reside on `\\sol-gmp-fs01\toc-projects`; no GxP data on local C:. |
| URS-SW-04 | H | R1 | Windows audit logs shall be forwarded to site SIEM (Splunk). |
| URS-SW-05 | H | R1 | The clock shall be synced to `ntp.solara.local`; skew shall be monitored with alert at > 1 s. |
| URS-SW-06 | M | R2 | Screen lock shall apply after 10 min idle; AD re-auth shall be required to unlock. |
| URS-SW-07 | H | R1 | DataPro2 Part 11 settings (audit trail, e-sign, raw data lock) shall be configured per the Configuration Specification. |
| URS-SW-08 | M | R2 | Vendor patches (Sievers DataPro2 SCN) shall be applied only after site change-control approval. |

### 5.3 USP <643> / Ph. Eur. 2.2.44 Compendial Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CMP-01 | H | R1 | The system shall execute USP <643> calculations and shall compare TOC to the 500 ppb (0.50 mg C / L) limit for bulk WFI / PW; OOS at limit shall trigger investigation. |
| URS-CMP-02 | H | R1 | The instrument shall meet USP <643> system-suitability criterion: response efficiency 85% ≤ RE ≤ 115% computed from sucrose vs 1,4-benzoquinone responses. |
| URS-CMP-03 | H | R1 | The instrument shall meet Ph. Eur. 2.2.44 control criteria when used for EP-monograph water testing. |
| URS-CMP-04 | H | R1 | The system shall demonstrate limit of detection ≤ 0.05 mg C / L (50 ppb) at OQ. |
| URS-CMP-05 | M | R2 | Compendial method designations (USP-NF, Ph. Eur., JP) shall be captured in the method header. |

### 5.4 AIQ — DQ / IQ / OQ / PQ per USP <1058>

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AIQ-01 | H | R1 | DQ shall document fitness for intended use against TOC working range (1 ppb – 50 ppm typical), on-line + grab modes, water-grade compatibility (WFI / PW / HPW). |
| URS-AIQ-02 | H | R1 | IQ shall verify installation, AD bind, DataPro2 build hash, UV lamp installation, reactor + ICR (inorganic carbon remover) installation. |
| URS-AIQ-03 | H | R1 | OQ shall include: USP <643> SST (sucrose vs BQ), limit of detection, linearity (5-point from 50 ppb to 5 000 ppb), accuracy (% recovery on sucrose challenge), precision (RSD ≤ 5% on replicate 500-ppb challenges), carry-over. |
| URS-AIQ-04 | H | R1 | PQ shall be executed at go-live, on major change (UV lamp replacement, reactor service, software upgrade), and at least annually. |
| URS-AIQ-05 | M | R2 | A partial PQ (SST only) shall be permitted after planned maintenance not affecting the UV reactor. |
| URS-AIQ-06 | M | R2 | Qualification evidence shall be retained ≥ 25 years per product-release tie. |

### 5.5 System Suitability Test (SST)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SST-01 | H | R1 | The SST shall be configured per USP <643>: triplicate readings of (a) water blank, (b) 500-ppb sucrose, (c) 500-ppb 1,4-benzoquinone; the system shall compute response efficiency. |
| URS-SST-02 | H | R1 | SST shall be executed at the start of each release session and at the cadence in the method (typically daily for grab mode, weekly on-line). |
| URS-SST-03 | H | R1 | SST records shall be captured with operator, ts, USP RS lot, certificate expiry, computed RE, pass / fail (85% ≤ RE ≤ 115%). |
| URS-SST-04 | H | R1 | SST failure shall set the instrument to NOT READY; GxP acquisitions shall be blocked until SST re-passes. |
| URS-SST-05 | M | R2 | SST results shall be trended across rolling 12 months with early-warning band at RE ≤ 90% or RE ≥ 110% (within USP limits). |

### 5.6 Reagent / Standard Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REA-01 | H | R1 | USP RS sucrose and USP RS 1,4-benzoquinone shall be logged with lot, source, COA, receipt date, opening date, expiry; integrated with the SST workflow. |
| URS-REA-02 | H | R1 | The system shall block SST start when bound USP RS is expired. |
| URS-REA-03 | M | R2 | Prepared 500-ppb working standards shall be logged with prep date, prep analyst, and short shelf life (typically same day for sucrose; per stability data for BQ). |
| URS-REA-04 | M | R2 | TOC water blank (low-TOC water) shall be lot-tracked; certificate of < 50 ppb TOC required at receipt. |
| URS-REA-05 | M | R2 | Reagent waste shall be logged per site EHS SOP. |

### 5.7 UV Lamp + Reactor + ICR Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LIFE-01 | H | R1 | UV-lamp lifetime shall be tracked (Sievers recommendation 12 months); a 30-day warning shall fire prior to recommended replacement. |
| URS-LIFE-02 | H | R1 | UV-lamp replacement shall trigger full PQ per URS-AIQ-04. |
| URS-LIFE-02b | M | R2 | UV-lamp intensity reading shall be recorded per acquisition; drop below SOP threshold shall fire deviation. |
| URS-LIFE-03 | M | R2 | Reactor + ICR replacement / refresh shall be tracked; replacement shall trigger SST + partial OQ. |
| URS-LIFE-04 | M | R2 | Membrane CO₂ detector lifetime shall be tracked per Sievers recommendation. |

### 5.8 Acquisition / Processing / Reportable Result + OOS

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ACQ-01 | H | R1 | The system shall load approved methods from a controlled methods library (read-only to analysts). |
| URS-ACQ-02 | H | R1 | Sequence start shall be rejected when the instrument is not Ready, no approved method is bound, SST is overdue / failed, or the project is locked. |
| URS-ACQ-03 | H | R1 | Per-injection metadata shall be captured: sample ID, source point, method ID + version, instrument ID, analyst, ts, sample mode (on-line / grab), UV lamp hours, reactor lot. |
| URS-ACQ-04 | H | R1 | The system shall support on-line mode (continuous sample loop) and grab-sample mode (vial autosampler) with mode-specific SST cadence. |
| URS-PROC-01 | H | R1 | The system shall apply the approved processing method (peak integration, calibration, blank correction). |
| URS-PROC-02 | H | R1 | Manual reprocessing shall require captured RFC. |
| URS-PROC-03 | H | R1 | Raw data shall be preserved unaltered; processing shall produce a derived result that references but does not overwrite the raw record. |
| URS-PROC-04 | H | R1 | The system shall compare result to compendial limit (500 ppb); shall flag values at 30 / 50 / 100% of limit (trend / OOT / OOS). |
| URS-PROC-05 | H | R1 | The system shall generate a PDF report including sample metadata, method, analyst, reviewer, approver, raw + derived results, SST status, limit status, ALCOA+ statement, SHA-256 hash. |
| URS-PROC-06 | M | R2 | An OOS result shall trigger the downstream § 211.192 investigation workflow (delegated to LIMS) and shall set the water-system sample-point to HOLD in LIMS. |

### 5.9 Audit Trail / Part 11 / Data Integrity

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | The audit trail shall be time-stamped, secure, and shall capture user, action, old / new value, reason. |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only; admin update / delete shall be cryptographically prevented. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be conducted by a Senior Analyst per batch (event-driven) and by the QC Manager monthly (periodic). |
| URS-AUD-04 | H | R1 | Raw data, audit trails, and reports shall be retained ≥ 7 years; ≥ 25 years if linked to product release. |
| URS-PART11-01 | H | R1 | The system shall implement procedural controls per 21 CFR § 11.10(a). |
| URS-PART11-02 | H | R1 | The system shall limit access to authorised individuals per § 11.10(d). |
| URS-PART11-03 | H | R1 | E-signatures shall manifest name, date / time, and meaning per § 11.50. |
| URS-PART11-04 | H | R1 | Signatures shall be linked to records per § 11.70. |
| URS-PART11-05 | H | R1 | Signatures shall be unique per § 11.100. |
| URS-PART11-06 | H | R1 | Identity-based signature components shall require re-authentication per § 11.200. |
| URS-PART11-07 | H | R1 | Password and credential controls per § 11.300 shall apply; account lock after 5 failed logins in 15 minutes. |
| URS-DI-01 | H | R1 | Data shall be Attributable. |
| URS-DI-02 | H | R1 | Data shall be Legible. |
| URS-DI-03 | H | R1 | Data shall be Contemporaneous; retrospective entries shall be flagged with actual timestamp + reason. |
| URS-DI-04 | H | R1 | Original raw files shall be preserved unaltered. |
| URS-DI-05 | H | R1 | Calculations shall be Accurate — verified per OQ (URS-AIQ-03) + SST-on-acquisition gate. |
| URS-DI-06 | M | R2 | Records shall be Complete / Consistent / Enduring (≥ 7 y retention) / Available (≤ 1 business day). |

### 5.10 LIMS Interface

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-01 | H | R1 | The system shall import sample worklists from LabWare LIMS 8 via DataShare 5 (read-only). |
| URS-INT-02 | H | R1 | Approved results shall be pushed to LIMS only after QC Manager approval. |
| URS-INT-03 | H | R1 | The LIMS-bound result shall include report ID, instrument ID, method ID + version, reviewer / approver IDs, SST status. |
| URS-INT-04 | M | R2 | The interface shall reject result push when SST is failed / expired. |

### 5.11 Backup / DR / Performance / Security / Training / PR

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | Daily backup shall be executed to a Veeam target with cryptographic integrity check. |
| URS-BAK-02 | H | R1 | A quarterly restore test shall be witnessed by QC. |
| URS-BAK-03 | M | R2 | RTO shall be ≤ 8 business hours; RPO ≤ 24 hours. |
| URS-PERF-01 | M | R2 | The workstation shall complete a typical 30-injection sequence without crashing or losing data integrity. |
| URS-PERF-02 | L | R3 | UI response shall be ≤ 3 s at the 95th percentile. |
| URS-SEC-01 | H | R1 | All accounts shall be domain accounts; local accounts shall be disabled (except break-glass admin). |
| URS-SEC-02 | H | R1 | Removable media shall be blocked except for approved engineering use under change control. |
| URS-TRN-01 | H | R1 | Production access shall require recorded role-specific training (LMS); SST + reagent-lifecycle training annual. |
| URS-PR-01 | H | R1 | An annual periodic review shall cover configuration, audit-trail review evidence, SST trend, lamp / reactor lifecycle, reagent register health, deviations, backup-restore, training, fitness for use; signed by QC Manager + QA Manager. |

### 5.12 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem; conditional-access policy `Lab-Workstation Conditional Access (MFA on interactive logon)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T3 with RPO ≤ 72 h and RTO ≤ 72 BH; backup integration shall use Veeam file-level capture of the per-instrument result store and method library; the application team shall participate in annual application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 7 y per the consuming-record schedule. |

## 6. Acceptance Criteria

CS, RA, IQ, OQ (USP <643> SST + LOD + linearity + accuracy + precision), PQ approved and executed; VSR approved by QC + QA; RTM closed at 100% URS-ID coverage; all named users trained.

## 7. Constraints

- No custom code.
- Vendor patches under change control.
- No direct internet.
- UV lamp lifetime tracked (Sievers recommendation 12 months); replacement triggers PQ.
- Sucrose working standard prepared same day per stability data.

## 8. Assumptions

- Sievers / Veolia maintains DataPro2 SDLC.
- AD and LIMS are validated.
- USP RS sucrose + 1,4-benzoquinone supply chain stable.

## 9. References

**US / FDA:**
- 21 CFR Part 11 §§ .10(a)/(b)/(c)/(d)/(e)/(k), .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .68, .160, .165, .192, .194
- FDA *Guidance for Industry — High Purity Water Systems* (1993, current)
- FDA *Guidance on Data Integrity and Compliance with cGMP* (2018)

**EU / EMA:**
- EU GMP Annex 11 §§ 4, 6, 9, 11
- Ph. Eur. 2.2.44 — Total Organic Carbon
- Ph. Eur. 0008 — Water for Injections (current rev.)
- EudraLex Volume 4 — GMP Parts I + III

**International:**
- USP <643> — Total Organic Carbon
- USP <645> — Water Conductivity (referenced for paired conductivity check)
- USP <1231> — Water for Pharmaceutical Purposes
- USP <1058> — Analytical Instrument Qualification
- USP <1225> — Validation of Compendial Procedures
- ICH Q2(R2) — Validation of Analytical Procedures
- PIC/S PI 041
- ISPE GAMP 5 (2nd Edition, 2022); ISPE *Baseline Guide Vol. 4: Water and Steam Systems*

**Vendor:**
- Sievers / Veolia — *M9 TOC Analyzer Configuration Reference* (current rev.)
- Sievers / Veolia — *DataPro2 v2.4 Installation, Configuration, and Administration Reference*
- Sievers / Veolia — *DataPro2 21 CFR Part 11 Compliance Guide*

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

