---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-27; expanded 2026-05-12 (T3 enrichment — DCS DeltaV + ISA-88/95/101/18.2 + IEC 61511 + NAMUR)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed.) Cat 4 + Cat 5 conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11; Annex 1; ICH Q9(R1); ICH Q10"
  - "ISA-88 (Batch Control); ISA-95 (Enterprise Integration); ISA-101 (HMI); ISA-18.2 (Alarm Management)"
  - "IEC 61508; IEC 61511 (Process-industry safety)"
  - "NAMUR NA 102 (Lifecycle), NE 33 (DCS-System-Integration), NA 65 (Safety-Instrumented Functions), NE 159 (Functional Safety)"
  - "PIC/S PI 041; FDA CSA (Feb 2026); ISPE GAMP GPG DCS"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## DCS — Emerson DeltaV v15.3 (Bioprocess Suite)

**Document Number:** TET-URS-DCS-001
**Version:** 1.2
**Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Tethys Pharma S.A., Biologics Drug Substance Plant 1, Lyon, France *(fictional)*
**System Owner:** Process Automation Lead
**Process Owner:** Head of Drug Substance Manufacturing
**Development Owner:** Quality IT — Process Automation
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (with site-authored phase logic + master recipes assessed as Cat 5 sub-components)
**Project Mode:** Configuration project on commercial software product **Emerson DeltaV v15.3 (Bioprocess Suite)** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .22, .68, .180, .192; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Annex 1 (2022 revision); ICH Q9(R1); ICH Q10; ICH Q11; ISA-88; ISA-95; ISA-101; ISA-18.2; IEC 61508; IEC 61511; NAMUR NA 102 / NE 33 / NA 65 / NE 159; PIC/S PI 041; FDA CSA (Feb 2026).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Process Automation Lead) | _____________ | _____________ | _____ |
| Reviewer (Manufacturing IT Lead) | _____________ | _____________ | _____ |
| Reviewer (Functional Safety Engineer — IEC 61511) | _____________ | _____________ | _____ |
| Reviewer (DCS Engineering Manager) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Approver (Head of Drug Substance Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Minor: SIS proof-test scope clarified. |
| 1.2 | 2026-05-12 | (synthetic) | Tier-T3 enrichment: §5 broken into 13 subsections (ISA-88 batch state machine, ISA-101 HMI, ISA-18.2 alarm philosophy + rationalisation, redundancy + failover, engineering workstation change control, recipe Master/Site/Control hierarchy, OPC-UA + Foundation Fieldbus + HART integration, NAMUR bindings); 16-row risk table. Authored to **Tier T3** (production DCS spanning 6 trains × end-to-end DSP unit operations + SIS partition + batch + continuous control + multi-protocol field bus). |

## Definitions

| Term | Definition |
|---|---|
| DCS | Distributed Control System |
| DeltaV | Emerson DeltaV v15.3 process automation suite |
| Phase Logic | ISA-88 phase implementing a unit-procedure step |
| SIS | Safety-Instrumented System (DeltaV SIS, IEC 61511 / SIL 2 partition) |
| SIF | Safety-Instrumented Function |
| Recipe | ISA-88 master / site / control recipe |
| ProfessionalPLUS | Emerson DeltaV engineering workstation |
| ApplicationStation | Emerson DeltaV application/integration node |
| OperatorStation | Emerson DeltaV HMI client |
| MES | Werum PAS-X v3.2 |
| Historian | Aspen IP.21 (separate URS) |
| FF | Foundation Fieldbus |
| HART | Highway Addressable Remote Transducer |
| OPC UA | OPC Unified Architecture |
| NAMUR | Normenarbeitsgemeinschaft für Mess- und Regeltechnik in der chemischen Industrie (user-association best-practice recommendations) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the DCS used to control GMP bioprocess manufacturing at Tethys Pharma DSP1 — fermentation, harvest, primary capture, polishing chromatography, UF/DF, and bulk fill — across a 6-train suite.

## 2. Scope

**In scope:** DeltaV v15.3 ProfessionalPLUS (engineering station), ApplicationStation (×2 redundant), OperatorStations (12), DeltaV controllers (M-series, 24 nodes, redundant pairs), I/O cards (CHARMs + traditional), DeltaV SIS logic solvers (SIL 2, redundant), DeltaV Batch (ISA-88 batch engine), DeltaV Operate (HMI), DeltaV Live (Web HMI), DeltaV Live Configuration, the DeltaV Configuration Database; site-authored phase logic + master recipes (Cat 5 sub-components); integrations with PAS-X (recipe download / batch report) via OPC UA, Aspen IP.21 (historian) via OPC HDA / UA, Site BMS (utility-status interlocks) via OPC UA, instrument bus (Foundation Fieldbus H1 + HART 7 + WirelessHART), AD `tethys.local`.

**Out of scope:** Field instrumentation (separate equipment qualification); Aspen IP.21 historian (separate URS); BMS (separate URS); analytical labs; Watson LIMS (separate URS, consumed via PAS-X).

## 3. System Description and Intended Use

DeltaV is the system of record for batch execution within DSP1. Master recipes are downloaded from PAS-X for a production order; DeltaV instantiates a control recipe; phase logic runs the unit-procedure steps (charge buffer, ramp temperature, hold pH, transfer); operators monitor and intervene per the operating procedure; on completion, the executed-batch report is pushed back to PAS-X. SIS logic runs in a SIL 2 partition validated by Emerson per IEC 61508 / IEC 61511. NAMUR recommendations (NA 102 for system lifecycle, NE 33 for system integration, NA 65 for safety-instrumented functions, NE 159 for functional safety governance) shape design and operations.

GAMP Cat 4 for the platform; Cat 5 for site-authored phase logic and master recipes.

## 4. User Roles

| Role | Permissions |
|---|---|
| Operator | Execute operator-level commands; respond to alarms; capture comments. |
| Senior Operator / Line Lead | All Operator + second-person verification of critical steps. |
| Recipe Author | Author / edit master recipes under change control. |
| Recipe Reviewer | Review recipes; cannot review own. |
| Recipe Approver (QA + Production) | Approve recipes to EFFECTIVE. |
| Phase Logic Author | Author / edit phase logic under SDLC and change control. |
| Phase Logic Reviewer | Review phase logic; cannot review own. |
| Phase Logic Approver | Approve phase logic to PRODUCTION. |
| DCS Engineer | Configure controllers, I/O, OperatorStations under change control. |
| DCS Engineering Manager | Approve DCS engineering changes; co-signs HMI graphic + control-logic CRs. |
| Functional Safety Engineer | Author / review SIS logic under IEC 61511; manages SIL-rated SIFs + proof-tests. |
| FSE Approver | Approves SIS-side CRs; required for any SIF change. |
| System Administrator | Patching, AD groups, OperatorStation provisioning; cannot approve recipes / phase logic. |
| Auditor | Read-only across configuration, batch records, audit trails. |
| Inspection-Read-Only | Time-bound read-only for regulator inspection (Annex 11 § 6). |

**Separation of duties:** Operator ≠ Verifier on the same critical step; Recipe Author ≠ Approver of same recipe; Phase Logic Author ≠ Approver; FSE ≠ FSE Approver of own SIF change; DCS Engineer ≠ DCS Engineering Manager on own HMI/control-logic change.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` / `R2` / `R3`), and a verifiable `shall`-clause.

### 5.1 Platform / Hardware

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | Redundant ProfessionalPLUS + ApplicationStation pair; redundant controllers (M-series pairs); 12 OperatorStations on a fault-tolerant Ethernet ring. |
| URS-PLAT-02 | H | R1 | DCS network on a dedicated process-control VLAN; firewall + DMZ between DCS and the corporate network per NAMUR NE 153 zone model. |
| URS-PLAT-03 | H | R1 | UPS sized for ≥ 30 min controlled shutdown for all DCS nodes; SIS logic solvers on a separate UPS branch. |
| URS-PLAT-04 | H | R1 | Time synchronisation via PTP (IEEE 1588); skew ≤ 1 s monitored; degraded sync raises alarm. |
| URS-PLAT-05 | M | R2 | Controller / IO firmware updates shall follow Emerson + site change control with impact assessment; SIS-partition firmware shall additionally follow IEC 61511 functional-safety-management procedure. |

### 5.2 Redundancy + Failover (NAMUR NE 33 + Emerson reference architecture)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RDN-01 | H | R1 | Controllers shall be deployed in redundant pairs with bumpless transfer; failover shall be ≤ 1 s for control loops; events logged. |
| URS-RDN-02 | H | R1 | ApplicationStations shall be redundant with auto-failover; HMI sessions shall transparently reconnect to the surviving node. |
| URS-RDN-03 | H | R1 | I/O network shall be ring-topology with self-healing; single fault tolerance verified at OQ. |
| URS-RDN-04 | H | R1 | SIS logic-solver pair shall provide 1oo2D (one-out-of-two with diagnostic) for SIL 2 SIFs per IEC 61511. |
| URS-RDN-05 | M | R2 | Failover events shall be surfaced on the HMI overview faceplate and recorded in the audit trail. |

### 5.3 Recipe Management — ISA-88 Master / Site / Control Hierarchy

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REC-01 | H | R1 | Master recipes shall follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE. |
| URS-REC-02 | H | R1 | Recipes shall be authored at three ISA-88 levels: Master Recipe (campaign-template), Site Recipe (site-fitted to physical model), Control Recipe (per-batch instantiation); references shall be version-pinned. |
| URS-REC-03 | H | R1 | Only EFFECTIVE master recipes may be downloaded from PAS-X; checksum + version validated before instantiation. |
| URS-REC-04 | H | R1 | Recipe transitions shall require role-restricted electronic signatures with separation of duties. |
| URS-REC-05 | H | R1 | Recipes reference EFFECTIVE phase-logic versions; broken references shall block APPROVAL. |
| URS-REC-06 | H | R1 | EFFECTIVE recipes shall be immutable; changes require a new revision via change control. |
| URS-REC-07 | M | R2 | Recipe physical-model bindings (units / equipment-modules / control-modules per ISA-88 Part 2) shall be persisted and surfaced for impact-assessment. |

### 5.4 Phase Logic (Cat 5 Sub-Component) — ISA-88 Batch State Machine

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PHL-01 | H | R1 | Phase logic shall be developed under documented SDLC: code review, unit tests, integration tests on a non-prod controller, simulation tests where applicable. |
| URS-PHL-02 | H | R1 | Phase logic deployment to PRODUCTION shall require approved CR + successful regression-test run. |
| URS-PHL-03 | H | R1 | Phase logic source shall be version-controlled (DeltaV Version Control) with signed authorship. |
| URS-PHL-04 | H | R1 | Phase logic shall implement the ISA-88 state model (IDLE / RUNNING / HELD / RESTARTING / STOPPING / STOPPED / ABORTING / ABORTED / COMPLETE) with deterministic transitions. |
| URS-PHL-05 | H | R1 | Phase logic shall declare its safe-state response on utility loss, SIS demand, or operator-initiated abort. |
| URS-PHL-06 | M | R2 | Phase-logic execution metrics shall be exposed for periodic-review. |

### 5.5 Batch Execution

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAT-01 | H | R1 | Each batch shall be instantiated atomically from a PAS-X production order; failure shall roll back without partial creation. |
| URS-BAT-02 | H | R1 | Step ordering shall be enforced per the master recipe; out-of-sequence operator actions shall be blocked unless an authorised override is signed. |
| URS-BAT-03 | H | R1 | Critical steps (CIP cycle complete, sterilising-grade filter integrity OK, transfer initiated) shall require second-person verification with a separate signature. |
| URS-BAT-04 | H | R1 | Process parameters shall be captured at ≥ 1 Hz on critical channels (temperature, pH, DO, pressure, flow). |
| URS-BAT-05 | H | R1 | Manual setpoint override during a product batch shall require Operator + Senior Operator dual signature with reason. |
| URS-BAT-06 | M | R2 | Batch abort sequence shall safe the unit operation per the recipe-defined safe state. |
| URS-BAT-07 | H | R1 | Continuous-control modules (PID + cascade + ratio) shall execute on the redundant controller pair with bumpless transfer on failover. |

### 5.6 Alarms — ISA-18.2 Alarm Philosophy

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ALM-01 | H | R1 | Alarms shall be rationalised per ISA-18.2 with classifications: `INFO`, `WARNING`, `CRITICAL`, `SIS`; each shall have a defined response, acknowledgement requirement, and escalation path. |
| URS-ALM-02 | H | R1 | Critical alarms shall require operator acknowledgement with reason; unacknowledged criticals shall trigger escalation per the alarm-rationalisation table. |
| URS-ALM-03 | H | R1 | An alarm philosophy document `TET-AP-DCS-01` shall govern alarm-management lifecycle (identify → rationalise → design → implement → operate → maintain → manage-of-change). |
| URS-ALM-04 | H | R1 | Alarm-rate metrics (alarms/operator/hour, peak rate, top-talkers, standing-alarm count, alarm-flood frequency) shall be monitored and surfaced in periodic-review. |
| URS-ALM-05 | M | R2 | Alarm shelving (per ISA-18.2 § 7) shall be supported, audited, and time-bounded. |

### 5.7 SIS — Safety-Instrumented System (IEC 61511 / SIL 2)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SIS-01 | H | R1 | SIS-classified alarms shall invoke pre-defined SIS responses (e.g., emergency shutdown of utility lines, isolation valves) without operator intervention; events shall be logged in the SIS event recorder. |
| URS-SIS-02 | H | R1 | SIS proof-tests shall be executed per the proof-test plan with documented evidence; SIF coverage shall be verified at the demand-rate interval per IEC 61511. |
| URS-SIS-03 | H | R1 | SIS bypass shall require FSE + FSE Approver dual signature with timed-bypass policy; auto-revert on timer expiration. |
| URS-SIS-04 | M | R2 | SIL verification calculation (PFDavg) shall be revisited annually under NA 65 / NE 159. |

### 5.8 HMI — ISA-101 Design Standard

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HMI-01 | H | R1 | OperatorStation screens shall follow ISA-101 hierarchical design (Level 1 overview / Level 2 unit / Level 3 diagnostic / Level 4 engineering); navigation depth ≤ 3 clicks. |
| URS-HMI-02 | H | R1 | High-performance HMI palette shall be applied: muted greys for normal state; saturated colours reserved for abnormal indications; alarm-priority colour-map fixed. |
| URS-HMI-03 | H | R1 | OperatorStation alarm-ack latency ≤ 1 s; faceplate response ≤ 500 ms. |
| URS-HMI-04 | H | R1 | HMI graphic changes shall be under change control; DCS Engineer authors, DCS Engineering Manager approves, QA co-signs. |
| URS-HMI-05 | M | R2 | DeltaV Live (web HMI) sessions shall require fresh AD auth + MFA; web access logged. |

### 5.9 Engineering Workstation + Control Logic Change Control

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-EWS-01 | H | R1 | ProfessionalPLUS access shall be restricted to DCS Engineers + DCS Engineering Manager + FSE; all changes shall be under CR with impact assessment. |
| URS-EWS-02 | H | R1 | DCS Configuration Database changes shall be exported, diffed, and signed as part of CR closure. |
| URS-EWS-03 | H | R1 | Control-module changes affecting CPPs shall require regression testing against the simulator before deployment to production. |
| URS-EWS-04 | H | R1 | HMI graphic + control-logic + recipe changes shall be tracked in a single CR register with cross-references. |
| URS-EWS-05 | M | R2 | Annual configuration-baseline audit shall reconcile production against the Configuration Database. |

### 5.10 Audit Trail / 21 CFR Part 11 / Data Integrity

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Audit trail covering recipe events, phase-logic deployments, batch events, alarm acks, SIS events, configuration changes, signature events; PTP-derived timestamps. |
| URS-AUD-02 | H | R1 | Audit trail append-only; system administrators cannot edit. |
| URS-AUD-03 | H | R1 | Audit-trail review by Quality Reviewer per batch; QA Compliance quarterly. |
| URS-AUD-04 | H | R1 | Retention ≥ 25 years from product expiry. |
| URS-PART11-01 | H | R1 | Per § 11.10(a): procedural controls protect electronic-record validity. |
| URS-PART11-02 | H | R1 | Per § 11.10(d): access limited to authorised individuals via AD + MFA. |
| URS-PART11-03 | H | R1 | Per § 11.10(e): operational audit trail per URS-AUD-01. |
| URS-PART11-04 | H | R1 | Per § 11.50: e-signatures include printed name, date / time, meaning; SoD enforced. |
| URS-PART11-05 | H | R1 | Per § 11.70: signatures cryptographically linked to the signed record. |
| URS-PART11-06 | H | R1 | Per § 11.100: signatures unique per individual; reuse / reassignment blocked. |
| URS-PART11-07 | H | R1 | Per § 11.200: re-authentication required at the moment of signing critical events. |
| URS-PART11-08 | H | R1 | Per § 11.300: password / credential controls per InfoSec policy. |
| URS-DI-01 | H | R1 | **Attributable:** records attributable to a named user. |
| URS-DI-02 | H | R1 | **Legible:** records exportable as PDF/A-3 + CSV / JSON. |
| URS-DI-03 | H | R1 | **Contemporaneous:** PTP timestamps; retroactive flagged with reason. |
| URS-DI-04 | H | R1 | **Original:** raw process values preserved unaltered; corrections recorded as annotated values referencing original. |
| URS-DI-05 | H | R1 | **Accurate:** PID / cascade / phase calculations verified per OQ. |
| URS-DI-06 | M | R2 | **Complete / Consistent / Enduring / Available:** ≥ 25-yr retention; retrievable within 4 h during inspection. |

### 5.11 Integrations (ISA-95 + OPC UA + Foundation Fieldbus + HART)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-PASX-01 | H | R1 | Master-recipe download from PAS-X via REST over mTLS or OPC UA over TLS with mutual authentication; checksum + version validated. |
| URS-INT-PASX-02 | H | R1 | Executed-batch report (parameter profile + alarms + SIS events + signatures) pushed to PAS-X within 30 minutes of batch end. |
| URS-INT-HIST-01 | H | R1 | All GxP-relevant tags streamed to Aspen IP.21 via OPC HDA / OPC UA; lossless during DCS network blips via local buffering. |
| URS-INT-BMS-01 | H | R1 | BMS-driven utility-status interlocks (clean steam pressure, WFI / PW quality, HVAC status) consumed by DCS via OPC UA; loss safes the affected unit operation. |
| URS-INT-FF-01 | H | R1 | Foundation Fieldbus H1 segments shall be designed per Emerson reference + ISA-50.02; segment health monitored. |
| URS-INT-HART-01 | H | R1 | HART 7 device data shall be acquired via CHARMs or HART multiplexer; secondary variables shall be available for diagnostics. |
| URS-INT-WHART-01 | M | R2 | WirelessHART devices (Emerson Rosemount) shall be configured per NAMUR NE 124 (wireless security). |
| URS-INT-AD-01 | H | R1 | Authentication via AD; service accounts via vault. |

### 5.12 Performance / Availability / Backup / Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | H | R1 | OperatorStation alarm-ack latency ≤ 1 s; faceplate response ≤ 500 ms. |
| URS-AV-01 | H | R1 | DCS availability ≥ 99.95% during operating campaigns. |
| URS-BAK-01 | H | R1 | Configuration database backed up nightly; full-image backup before any change deployment. |
| URS-BAK-02 | H | R1 | Quarterly restore test; annual full-DR test including SIS proof-test integration. |
| URS-SEC-01 | H | R1 | AD-managed accounts; role-based access; OperatorStation auto-lockout after inactivity. |
| URS-SEC-02 | H | R1 | Removable media blocked by Windows GPO except for vendor-approved engineering use under change control. |
| URS-SEC-03 | M | R2 | Vulnerability scans monthly; criticals to remediation in 30 days (with vendor-approved patches). |
| URS-SEC-04 | M | R2 | Network segmentation per NAMUR NE 153 zone model with documented data-flow allow-list. |

### 5.13 Training / Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | LMS-recorded role-specific training; SIS-related roles require functional-safety competency per IEC 61511. |
| URS-TRN-02 | M | R2 | Annual refresher including alarm-handling scenarios + recent deviation lessons. |
| URS-PR-01 | H | R1 | Annual periodic review covering recipe / phase-logic inventory, alarm-rationalisation drift, SIS proof-test compliance, audit-trail review evidence, deviation summary, training currency, configuration baseline reconciliation; signed by Process Automation Lead + FSE + DCS Engineering Manager + Head of QA. |

### 5.14 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem with local OT cached credentials for offline operation; conditional-access policy `OT-DCS Conditional Access (MFA at engineering workstation; operator stations use named-location plus role-bound smart cards)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the DeltaV historian DB plus file-level capture of controller and operator-station configuration; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 15 y (batch-history) per the consuming-record schedule. |

## 6. Acceptance Criteria

CS, RA, IQ, OQ, PQ approved and executed; PQ includes representative end-to-end batches across the 6-train suite, alarm-handling, SIS proof-test integration, PAS-X / IP.21 round-trip, FF / HART device-replacement scenario, redundant-controller failover, and HMI regression; VSR approved by Process Automation Lead + FSE + DCS Engineering Manager + Head of QA; RTM maps every URS to ≥ 1 approved test case.

## 7. Constraints

- DeltaV firmware patches under Emerson + site CR.
- SIS partition changes follow IEC 61511 functional-safety lifecycle.
- Phase-logic changes follow Cat-5 SDLC.
- NAMUR recommendations binding for system-integration design choices.

## 8. Assumptions

- PAS-X, Aspen IP.21, BMS, AD, Vault, field instrumentation are validated.
- Emerson supplies DeltaV under its published SDLC with vendor-side validation evidence.
- SIS hardware + logic are pre-certified to SIL 2 by Emerson.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .22, .68, .180, .192.
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11 — Computerised Systems.
- EU GMP Annex 1 (2022 revision) — Sterile Medicinal Products.
- EU GMP Chapter 4 — Documentation.

### International — ICH / ISA / IEC / NAMUR
- ICH Q9(R1) — Quality Risk Management.
- ICH Q10 — Pharmaceutical Quality System.
- ICH Q11 — Development and Manufacture of Drug Substances.
- ISA-88 (Batch Control) Parts 1-4.
- ISA-95 (Enterprise-Control System Integration) Parts 1-5.
- ISA-101 (HMI Design).
- ISA-18.2 (Alarm Management for the Process Industries).
- ISA-50.02 (Foundation Fieldbus H1 Physical Layer).
- IEC 61508 — Functional Safety of Electrical/Electronic/Programmable Electronic Safety-Related Systems.
- IEC 61511 — Functional Safety: Safety Instrumented Systems for the Process Industry Sector.
- NAMUR NA 102 — Process Control System Lifecycle.
- NAMUR NE 33 — DCS System Integration.
- NAMUR NA 65 — Safety-Instrumented Functions.
- NAMUR NE 153 — Automation Security.
- NAMUR NE 159 — Functional Safety Governance.
- NAMUR NE 124 — Wireless Field Devices Security.

### Industry — ISPE / PIC/S
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE GAMP Good Practice Guide — *Process Control Systems (DCS / SCADA / PLC)*.
- PIC/S PI 041.

### Vendor
- Emerson — *DeltaV v15.3 Configuration Reference*.
- Emerson — *DeltaV SIS Safety Manual*.
- Emerson — *DeltaV Live HMI Reference*.
- Emerson Rosemount — *Foundation Fieldbus + HART + WirelessHART Reference*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

