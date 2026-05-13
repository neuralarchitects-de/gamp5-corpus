---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch 2026-04-27; T2 enrichment 2026-05-13 (Chunk A Liquid Handler)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed.) Cat 4/5 conventions for laboratory automation with site-authored methods (VENUS scripts)"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300"
  - "21 CFR Part 211 §§ .68, .180, .192"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "ICH Q2(R2); ICH Q9(R1)"
  - "ISO 8655 (volumetric apparatus accuracy + precision; parts 1-7)"
  - "USP <41> Balances; USP <1251> Weighing on an Analytical Balance"
  - "USP <1058> AIQ — Group B (liquid handler)"
  - "PIC/S PI 041"
  - "Hamilton — Microlab STAR + VENUS 6.x Configuration Reference (vendor doc)"
  - "Hamilton — STAR Hardware Reference (Channel + Multi-Probe Head + Track-Gripper)"
  - "Hamilton — VENUS Software Development Kit (SDK) Reference"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# User Requirements Specification (URS)

## Robotic Liquid Handler — Hamilton Microlab STAR + VENUS 6.x

**Document Number:** IRS-URS-LH-001 | **Version:** 1.0 | **Effective Date:** 2026-04-27 *(synthetic)*
**Site:** Iris BioMed Inc., QC Bioassay Lab, Salt Lake City, Utah, USA *(fictional)*
**System Owner:** QC Bioassay Lead
**Process Owner:** Head of Quality Control
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (with site-authored VENUS methods assessed as Category 5 sub-components)
**Project Mode:** Custom-build project — site-developed system (GAMP 5 Category 5 — Bespoke; internal SDLC). System: Hamilton Microlab STAR + VENUS 6.x.
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192; EU GMP Annex 11 §§ 4, 6, 9, 11; ICH Q2(R2); ICH Q9(R1); ISO 8655 (parts 1-7); USP <41>; USP <1251>; USP <1058> AIQ (Group B); PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Bioassay Lead) | _____________ | _____________ | _____ |
| Reviewer (Automation Engineer) | _____________ | _____________ | _____ |
| Approver (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-13 | (synthetic) | Authored to Tier T2 (50-80 req target; Cat 4 liquid handler with Cat 5 site-authored VENUS methods). Expanded §§ 5.4 Worklist execution with per-channel pacing + deck-state checks, 5.5 Audit Trail + Part 11 (sub-section bindings, no range compression). New sections 5.7 Deck Layout + Labware Management, 5.8 Liquid-Class Library, 5.9 Tip Pickup / Aspirate-Dispense Error Recovery, 5.10 ISO 8655 Verification Cadence, 5.11 Multi-Channel + Multi-Probe-Head Choreography, 5.12 Contamination Control + Cross-Over Prevention. New risks (R-05..R-11): tip-pickup failure leading to dry-channel dispense, deck-position drift, labware mis-identification, liquid-class mismatch (viscous vs aqueous), contamination cross-over between samples, method-import drift between simulator and instrument, ISO 8655 calibration lapse. Web-research citations: ISO 8655 parts 1-7, USP <41>, USP <1251>, USP <1058> AIQ Group B, 21 CFR § 211.68. |

## Definitions

| Term | Definition |
|---|---|
| Liquid Handler | Hamilton Microlab STAR robotic platform |
| VENUS | Hamilton's STAR control software, version 6.x |
| Method | A VENUS script defining a liquid-handling procedure |
| Worklist | A batch of method instantiations (samples, source / destination labware) |
| LIMS | LabWare LIMS 8 |
| Plate Reader | Downstream bioassay reader (separate URS) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the robotic liquid-handler computer system used in QC bioassay sample preparation (serial dilutions, plate-mapping, reagent dispensing) at Iris BioMed.

## 2. Scope

**In:** Hamilton Microlab STAR instrument (8-channel + Multi-Probe Head), VENUS 6.x control software on a dedicated PC (Win 11 LTSC), site-authored VENUS methods, AD authentication, integration with LIMS (worklist + provenance push), daily backup, NTP sync.
**Out:** STAR mechanical hardware (separate equipment qualification); plate readers (separate URS); LIMS sample lifecycle.

## 3. System Description

VENUS is the system of record for liquid-handling provenance — which sample was dispensed at which volume into which well, by which operator, when, using which method version. Methods are authored in the VENUS IDE; site treats authored methods as Cat 5 sub-components with SDLC. Approved methods are stored in a controlled folder; worklists are built and run; provenance reports are generated and pushed to LIMS.

GAMP Cat 4 for the platform; Cat 5 for site-authored methods (one method = one Cat-5 sub-component with FS / RA / OQ).

## 4. User Roles

| Role | Permissions |
|---|---|
| Operator | Run worklists from EFFECTIVE methods; cannot edit methods. |
| Senior Operator / Line Lead | All Operator + second-person verification of run set-up. |
| Method Author | Author / edit VENUS methods under SDLC + change control. |
| Method Reviewer | Review methods; cannot review own. |
| Method Approver (QA + QC Bioassay Lead) | Approve to EFFECTIVE. |
| Automation Engineer | Hamilton-tech-level configuration, CO calibration; cannot approve methods. |
| System Administrator | OS / app config, AD groups; cannot approve. |
| Auditor | Read-only across data and audit trails. |

Separation of duties: Method Author ≠ Approver; Operator ≠ Verifier.

## 5. User Requirements

### 5.1 Platform / Hardware

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | M | R2 | PC on lab-IT VLAN; UPS sized for ≥ 30 min controlled shutdown; instrument fail-safe to safe state on power loss. |
| URS-PLAT-02 | H | R1 | NTP-synced clock; skew ≤ 1 s monitored. |
| URS-PLAT-03 | M | R2 | Instrument volume verification per ISO 8655 at the configured cadence. |

### 5.2 VENUS Software Configuration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SW-01 | H | R1 | VENUS Part 11 module enabled (audit trail required, e-sign required, raw data lock); validated configuration baseline. |
| URS-SW-02 | H | R1 | Methods stored in a controlled methods folder; per-method access enforced via AD-mapped roles. |

### 5.3 Method SDLC (Cat 5 Sub-Component)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MTH-01 | H | R1 | Method SDLC documented: requirements (per-assay), code review, dry-run on simulator, wet-run on instrument, accuracy / precision verification, regression run before promotion. |
| URS-MTH-02 | H | R1 | Method lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE; only EFFECTIVE methods may be selected for GxP runs. |
| URS-MTH-03 | H | R1 | Method changes require role-restricted electronic signatures with separation of duties. |
| URS-MTH-04 | H | R1 | Method source version-controlled in the site VCS with signed authorship. |

### 5.4 Worklist Execution and Provenance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-WL-01 | H | R1 | Worklist run shall capture: operator, method-id + version, source labware (with lot ids), destination labware, per-channel volume, timestamp per dispense, error / exception events. |
| URS-WL-02 | H | R1 | Pre-run validator checks instrument readiness, calibration currency, method = EFFECTIVE, all source / destination labware identified; failure blocks run. |
| URS-WL-03 | H | R1 | Mid-run aspirate / dispense errors are logged with cause (clot detection, level sensor, no-tip detection); failure mode triggers operator decision (abort / retry / continue with deviation). |
| URS-WL-04 | H | R1 | Post-run provenance report generated as PDF + structured CSV; pushed to LIMS as the per-sample chain-of-custody record. |

### 5.5 Audit Trail and Records

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | The system shall maintain a contemporaneous, time-stamped audit trail covering methods (author + change), worklists (creation + run + completion + error events), calibration events (per-channel ISO 8655 verification), signatures (e-signature events), and configuration (deck layout, liquid-class assignment, labware-definition changes). |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only at the database level; the Automation Engineer and System Administrator roles shall not be able to modify entries. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be performed per-batch by a Senior Operator (event-driven) and monthly by QC Bioassay Lead (periodic); review evidence retained as a controlled record. |
| URS-AUD-04 | H | R1 | Retention shall be ≥ 7 years (general) and ≥ 25 years for runs linked to product release per 21 CFR § 211.180. |
| URS-AUD-05 | M | R2 | Audit-trail export (per method, per worklist, per date range, per user) shall be supported without disrupting routine operation. |

### 5.6 21 CFR Part 11 Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a), the system shall be validated to ensure accuracy, reliability, and consistent intended performance. |
| URS-PART11-02 | H | R1 | Per § 11.10(b), the system shall generate accurate and complete copies of records (PDF/A-3 + machine-readable) for inspection. |
| URS-PART11-03 | H | R1 | Per § 11.10(c), records shall be protected throughout the 25-year retention horizon (immutable file-share + daily backup). |
| URS-PART11-04 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via AD authentication. |
| URS-PART11-05 | H | R1 | Per § 11.10(e), operational audit trail per § 5.5 shall exist. |
| URS-PART11-06 | H | R1 | Per § 11.10(g), VENUS user-role authority shall be mapped to AD groups. |
| URS-PART11-07 | M | R2 | Per § 11.10(k), Hamilton SCN updates managed under site CR; system-operation manual maintained. |
| URS-PART11-08 | H | R1 | Per § 11.50, electronic signatures shall include the signer's printed name, date and time, and meaning (closed list: Author / Review / Approve / Lock). |
| URS-PART11-09 | H | R1 | Per § 11.70, signatures shall be cryptographically bound to the signed record. |
| URS-PART11-10 | H | R1 | Per § 11.100, each electronic signature shall be unique to the individual. |
| URS-PART11-11 | H | R1 | Per § 11.200, re-authentication required at the moment of signing. |
| URS-PART11-12 | H | R1 | Per § 11.300, password / credential controls per site InfoSec policy. |
| URS-PART11-13 | H | R1 | Separation of duties enforced: Method Author ≠ Method Reviewer ≠ Method Approver; Operator ≠ Verifier on the same run. |

### 5.6a Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | **Attributable:** every action attributable to a named user. |
| URS-DI-02 | H | R1 | **Legible:** records exportable as PDF/A-3 + CSV. |
| URS-DI-03 | H | R1 | **Contemporaneous:** event timestamps server-side. |
| URS-DI-04 | H | R1 | **Original:** raw acquisition data (per-channel volume + per-well log) preserved unaltered. |
| URS-DI-05 | H | R1 | **Accurate:** volume measurements traceable to ISO 8655 verification. |
| URS-DI-06 | M | R2 | **Complete / Consistent / Enduring / Available:** records meet GMP retention obligations and 1-business-day retrieval SLA. |

### 5.6b Integrations / Performance / Backup / Security / Training / PR

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-LIMS-01 | H | R1 | The system shall import worklists from LIMS (read-only on LIMS side); provenance push back to LIMS post-run. |
| URS-INT-AD-01 | H | R1 | Authentication shall be via AD; no local VENUS accounts other than break-glass. |
| URS-PERF-01 | M | R2 | Worklist start latency ≤ 10 s; provenance-report generation ≤ 60 s for a 384-well plate. |
| URS-PERF-02 | M | R2 | The system shall complete a typical 96-well plate worklist within method-validated cycle time. |
| URS-BAK-01 | H | R1 | Daily backup of methods, provenance records, and audit trail; retention ≥ 25 years for release-linked runs. |
| URS-BAK-02 | H | R1 | Quarterly restore test, witnessed by QA. |
| URS-BAK-03 | M | R2 | RTO ≤ 8 business hours after workstation failure; RPO ≤ 24 hours. |
| URS-SEC-01 | H | R1 | Removable media (USB, optical) blocked except vendor-approved engineering use under CR. |
| URS-SEC-02 | H | R1 | All accounts AD; quarterly access review. |
| URS-SEC-03 | M | R2 | Anti-malware (CrowdStrike) with Hamilton-approved exclusion list. |
| URS-TRN-01 | H | R1 | LMS-recorded role-specific training; competency assessment for Method Authors (script SDK fluency required). |
| URS-TRN-02 | M | R2 | Annual refresher training. |
| URS-PR-01 | H | R1 | Annual periodic review covering method inventory, calibration compliance, audit-trail review evidence, deviation summary, training currency; signed by QC Bioassay Lead + Head of QA. |
| URS-PR-02 | M | R2 | Periodic review shall produce a documented disposition for any drift findings. |

### 5.7 Deck Layout and Labware Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DECK-01 | H | R1 | Deck layouts shall be version-controlled in VENUS; each method shall reference a specific deck-layout-version; mismatch at run-start shall block execution. |
| URS-DECK-02 | H | R1 | Labware definitions (well-geometry, max-volume, dead-volume, material) shall be stored in the controlled labware library; method changes affecting labware shall trigger re-validation flow. |
| URS-DECK-03 | H | R1 | Pre-run deck verification (visual inspection prompted by VENUS, optionally with deck-camera or RFID confirmation) shall confirm presence + position of all method-required labware before run start. |
| URS-DECK-04 | M | R2 | Deck-position drift (offsets from teaching reference) shall be checked at PM; drift > 0.5 mm triggers re-teach. |
| URS-DECK-05 | M | R2 | Source-labware lot information shall be captured per run (reagent lot, plate lot, tip-rack lot). |

### 5.8 Liquid-Class Library

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LQC-01 | H | R1 | The liquid-class library shall contain method-validated parameters per liquid type (aqueous, viscous, organic, surfactant-containing, DMSO, blood-derived) governing aspirate flow rate, dispense flow rate, air-gap volume, blowout volume, tip-touch behaviour. |
| URS-LQC-02 | H | R1 | Each method-step shall reference a specific liquid-class; mismatch (e.g., default aqueous applied to a viscous reagent) flagged at method-promotion via static analysis. |
| URS-LQC-03 | H | R1 | Liquid-class additions / changes shall require Method Owner + Senior Bioanalyst eSign + a documented verification (volume accuracy + CV on the changed liquid class per ISO 8655). |
| URS-LQC-04 | M | R2 | Liquid-class library version shall be pinned per method-version. |

### 5.9 Tip Pickup, Aspirate / Dispense Error Recovery

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ERR-01 | H | R1 | Tip-pickup verification (capacitive level-sense at Z=expected-rack-Z) shall confirm presence of a tip on each channel before aspirate; failure shall route to operator-decision workflow (auto-retry on alternate tip / abort / continue-with-deviation). |
| URS-ERR-02 | H | R1 | Aspirate-clot detection (pressure-monitoring during aspirate, deviation > method-bound threshold) shall route to operator-decision workflow; default behaviour: abort + flag well as `ASPIRATE_FAIL`. |
| URS-ERR-03 | H | R1 | Air-bubble / no-liquid detection (Liquid-Level Detection failure) shall route to operator-decision; default behaviour: abort + flag well + capture decision rationale. |
| URS-ERR-04 | H | R1 | Per-channel pacing shall be supported (separate timing for 1-8 of the 8 channels) to handle reagents with different liquid-class settings on the same plate. |
| URS-ERR-05 | M | R2 | Mid-run abort shall capture all completed wells as valid; non-completed wells flagged `PENDING_ABORT` and excluded from downstream processing without explicit operator override. |

### 5.10 ISO 8655 Verification Cadence

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CAL-01 | H | R1 | ISO 8655 volume accuracy + precision verification shall be performed per-channel at the cadence defined in `IRS-CAL-PLAN-LH-001` (typical: gravimetric verification every 6 months; high-stakes channels quarterly). |
| URS-CAL-02 | H | R1 | Expired calibration on any channel shall block GxP runs using that channel; expired-calibration override shall require QC Lead eSign + documented impact assessment. |
| URS-CAL-03 | H | R1 | Verification shall test 3 volume points (10%, 50%, 100% of channel range) with n ≥ 10 replicates; accuracy + precision per ISO 8655 Part 2; results captured per channel and trended. |
| URS-CAL-04 | M | R2 | Trending (per-channel volume drift over time) shall be visualised; pattern-detected drift (e.g., monotonic > 1% over 3 verifications) shall flag the channel for PM. |

### 5.11 Multi-Channel and Multi-Probe-Head Choreography

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CHO-01 | H | R1 | The system shall support coordinated 8-channel and Multi-Probe-Head (96/384) operations within a single method; channel-vs-MPH conflicts (same well at same time) detected by static analysis at method-promotion. |
| URS-CHO-02 | M | R2 | MPH wash-station integration shall be supported between liquid-class changes. |
| URS-CHO-03 | M | R2 | Track-gripper labware movements (96-tip rack reload, plate-sealing handoff to peripheral) shall be logged with timestamp + position. |

### 5.12 Contamination Control and Cross-Over Prevention

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CONT-01 | H | R1 | Sample-to-sample cross-over shall be prevented by mandatory tip-change between samples for the analyte class (no tip re-use across different samples for GxP runs); tip re-use within a single sample (e.g., serial dilution) permitted only when method-bound and validated. |
| URS-CONT-02 | H | R1 | Wash-station integration (deep-well rinse + air-gap) shall be method-bound for sticky reagents; method-promotion validator shall enforce wash-step presence when liquid-class flag `sticky=true`. |
| URS-CONT-03 | M | R2 | The system shall track cumulative tip-use counter per tip-rack; counter shall reset on rack reload. |

### 5.13 Method SDLC, Worklist Execution, and Provenance

The legacy sub-sections (§ 5.3 Method SDLC and § 5.4 Worklist Execution and Provenance) remain authoritative for method-SDLC and worklist-execution requirements (URS-MTH-01..04 + URS-WL-01..04). Cross-references in § 5.5 audit-trail capture them.

### 5.14 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem; conditional-access policy `Lab-Workstation Conditional Access (MFA on interactive logon)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the Venus method / run DB plus file-level capture of method scripts; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 7 y per the consuming-record schedule. |

## 6. Acceptance Criteria

CS, RA, IQ, OQ (with ISO 8655 accuracy + precision verification), PQ approved and executed including representative end-to-end serial-dilution run with LIMS round-trip; VSR approved.

## 7. Constraints

- Hamilton patches under change control.
- Per-method Cat-5 sub-component RA before promotion.

## 8. Assumptions

- AD, LIMS, NTP are validated.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10(a/b/c/d/e/g/k), .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .68 (automatic equipment), .180 (general records), .192 (production-record review).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EudraLex Volume 4.

### ISO / USP — primary text for liquid handling
- ISO 8655 — Piston-Operated Volumetric Apparatus — Parts 1 (terminology), 2 (piston pipettes), 3 (piston burettes), 5 (dispensers), 6 (gravimetric methods), 7 (alternative methods), 8 (photometric methods).
- USP <41> — Balances.
- USP <1251> — Weighing on an Analytical Balance.
- USP <1058> — Analytical Instrument Qualification (AIQ); robotic liquid handler is Group B (medium-complexity instrument).

### International — ICH
- ICH Q2(R2) — Validation of Analytical Procedures.
- ICH Q9(R1) — Quality Risk Management.

### Industry guidance
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE GAMP GPG: *Validation of Laboratory Computerized Systems*.
- ISPE GAMP GPG: *Records and Data Integrity*.
- PIC/S PI 041.

### Vendor
- Hamilton — *Microlab STAR + VENUS 6.x Configuration Reference*.
- Hamilton — *STAR Hardware Reference (Channel + Multi-Probe Head + Track-Gripper)*.
- Hamilton — *VENUS Software Development Kit (SDK) Reference + Method Best Practices*.

### Site
- `IRS-CAL-PLAN-LH-001` — per-channel ISO 8655 verification plan + cadence.
- `IRS-SOP-LH-METHOD-SDLC-001` — VENUS method SDLC procedure.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

