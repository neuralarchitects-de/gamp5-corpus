---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; v1.2 enrichment 2026-05-13"
seed_corpus_basis:
  - "PharmaDevils manufacturing-equipment URS family"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; EU GMP Annex 1 (2022 revised); ISO 17665-1:2024 + 17665-2; EN 285:2015+A1:2021; PDA TR1; ICH Q9(R1); PIC/S PI 041"
do_not_use_as:
  - regulated_record
  - basis_for_real_validation_decisions
intended_use:
  - LLM fine-tuning corpus seed
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Autoclave Computer System — Fedegari FOB 3 + Themis controller

**Document Number:** VEL-URS-AUTOCLAVE-001
**Version:** 1.2
**Effective Date:** 2026-05-13 *(synthetic)*
**Site:** Vela Therapeutics SRL, Sterile Manufacturing Plant 1, Parma, Italy *(fictional)*
**System Owner:** Sterilization Engineer
**Process Owner:** Head of Sterile Manufacturing
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Fedegari FOB 3 + Themis controller** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Annex 1 (2022 revised) §§ 5, 8, 9, 10; ISO 17665-1:2024 + ISO 17665-2; EN 285:2015+A1:2021 (large steam sterilizers); PDA TR1 (Validation of Moist Heat Sterilization Processes); HTM 01-01; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Sterilization Engineer) | _____________ | _____________ | _____ |
| Reviewer (Microbiology) | _____________ | _____________ | _____ |
| Reviewer (IT / Automation) | _____________ | _____________ | _____ |
| Approver (Head of Sterile Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Risk table reformatted to 5-column shape per v1.1 mechanical sweep. |
| 1.2 | 2026-05-13 | (synthetic) | Tier T2 enrichment (50-80 req target). Added cycle-type sub-section, F0 calculation, BI/CI qualification, recipe lifecycle, steam-quality per EN 285, Annex 1 (2022 revised) contamination-control sub-sections. Citations updated per METHODOLOGY § 2A.1. |

## Definitions

| Term | Definition |
|---|---|
| Autoclave / FOB 3 | Fedegari FOB 3 production-scale steam sterilizer with horizontal pre-vacuum chamber |
| Themis | Fedegari Themis supervisory controller (PLC-based with redundant CPU) |
| F0 | Equivalent integrated time of microbial lethality at 121.1 °C with z-value of 10 °C (ISO 17665-1) |
| BD | Bowie-Dick steam-penetration test (porous-load air-removal verification) |
| BI | Biological Indicator (Geobacillus stearothermophilus spores per USP <55>) |
| CI | Chemical Indicator (Type 1-6 per ISO 11140-1) |
| SAL | Sterility Assurance Level (target ≤ 10⁻⁶ for terminal sterilization) |
| PCD | Process Challenge Device |
| NCG | Non-Condensable Gas (steam quality parameter per EN 285) |
| MES | Werum / Körber PAS-X v3.2 |
| BMS | Building Management System (room-pressure interlock) |
| LDT | Sterilization Data Terminal — workstation running Themis-Manager |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| RTD | Resistance Temperature Detector (Pt100 chamber + load probe) |

## 1. Purpose

This URS defines requirements for the autoclave computer system controlling and recording the steam-sterilization cycles for equipment, garments, porous loads, liquid containers, and component parts at Vela Therapeutics Plant 1 (sterile parenteral fill-finish). The system supports terminal sterilization of components feeding aseptic-filling lines and instrument-set sterilization for cleanroom use, both governed by EU GMP Annex 1 (2022 revised) contamination-control requirements.

## 2. Scope

**In scope:**

- Fedegari FOB 3 autoclave cabinet (one unit, Plant 1 — see Annex 1 contamination-control strategy doc `VEL-CCS-PLANT1-001`).
- Themis embedded supervisory controller with redundant CPU pair (hot-standby switch-over).
- Supervisory workstation pair (active + standby on Windows Server 2022) running Themis-Manager.
- Data historian (Themis Historian — TimescaleDB backend).
- Integrations with PAS-X (recipe download / executed-cycle report) and the BMS (room pressure interlock).
- Active Directory authentication; daily backup; site PTP / NTP synchronisation.
- Recipe authoring environment for cycle types: vacuum/wrapped (porous load), gravity displacement, liquid (slow-exhaust), and sealed-vial.

**Out of scope:**

- Mechanical / piping / steam-generation / vacuum-pump hardware (covered under equipment qualification `EQ-AUTOCLAVE-001`).
- Biological / chemical-indicator sourcing (procurement procedure `PROC-BI-001`).
- Physical loading-pattern qualification per load family (separate validation: `VAL-LOAD-FAM-NNN`).
- Steam-supply qualification (covered by site utility validation `UTIL-STEAM-001`).
- Functional-safety SIL-rated PLC partition (managed under safety SDLC per IEC 61511).

```
                ┌──────────────────────────────────────┐
                │   PAS-X v3.2 MES (recipe / batch rpt) │
                └────────────────┬─────────────────────┘
                                 │
                                 ▼
   ┌────────────┐   ┌────────────────────────────────────────────────┐
   │ Site BMS   │◄──┤   FOB 3 + Themis (this URS)                     │
   │ (room      │   │   Active LDT + Standby LDT                      │
   │  press.)   │   │   PLC: redundant Themis CPU + TP1500 HMI panel  │
   └────────────┘   │   Historian (TimescaleDB) + Grafana             │
                    └────────────────────────────────────────────────┘
```

## 3. System Description and Intended Use

The system controls steam-sterilization cycles per validated load patterns, computes F0 in real time across distributed temperature probes (RTD Pt100), and produces an executed-cycle report bound to the load lot and the source MES batch. The system records steam-quality parameters (NCG / dryness / superheat per EN 285) at each cycle to demonstrate that the steam supplied meets ISO 17665-1 quality requirements.

GAMP Cat 4: Fedegari maintains the Themis SDLC; site validation focuses on installation, configuration, recipe-handling functionality, integrations, audit-trail behaviour, and Part 11 controls.

## 4. User Roles

| Role | Permissions |
|---|---|
| Operator | Load recipe; start / pause / abort cycle; document load contents and BI/CI/PCD placement. |
| Senior Operator / Line Lead | All Operator + second-person verification of critical-step events (load locked, cycle complete, BI retrieval). |
| Recipe Author | Create / edit recipes in DRAFT under change control. |
| Recipe Reviewer | Review recipes; cannot approve own. |
| Recipe Approver (QA) | Approve recipes to EFFECTIVE; retire. |
| Sterilization Engineer | Recipe parameter sign-off, BI/PCD configuration, cycle-engineering analysis. |
| Microbiology | BI batch certificate review and BI-cycle outcome disposition. |
| Maintenance Engineer | Run diagnostic / qualification / leak-test cycles; cannot run product cycles. |
| Quality Reviewer | Per-cycle review; gates cycle release to load disposition. |
| QA Compliance | Quarterly platform / audit-trail review; periodic-review owner. |
| System Administrator | Patching, AD groups, historian admin; cannot approve recipes or release cycles. |
| Auditor | Read-only across recipes, cycles, audit trails. |

Separation of duties: Operator ≠ Verifier on the same critical step; Recipe Author ≠ Approver of own recipe; Sterilization Engineer ≠ Quality Reviewer for the same cycle.

## 5. User Requirements

### 5.1 Platform / Hardware

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | The system shall provide an active / standby workstation pair with manual failover within 1 hour. |
| URS-PLAT-02 | H | R1 | The Themis controller and workstations shall be on UPS sized for ≥ 30 min controlled cycle hold; safety functions are SIL-rated and managed under a separate functional-safety SDLC. |
| URS-PLAT-03 | H | R1 | The system shall reside on a process-control VLAN with no office-network access from the operator station. |
| URS-PLAT-04 | H | R1 | The Themis controller shall include redundant CPUs with hot-standby switch-over; switch-over event shall be logged and shall not interrupt the running cycle's data capture. |
| URS-PLAT-05 | M | R2 | Historian shall retain ≥ 7 years of cycle data online; older data archived to immutable cold storage (WORM-class). |

### 5.2 Recipe / Load Pattern Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REC-01 | H | R1 | Recipes shall follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE; only EFFECTIVE recipes may be loaded for product cycles. |
| URS-REC-02 | H | R1 | Each recipe shall bind to a validated load pattern; an unvalidated load pattern shall not be permitted. |
| URS-REC-03 | H | R1 | Recipe transitions shall require role-restricted electronic signatures with separation of duties. |
| URS-REC-04 | H | R1 | EFFECTIVE recipes shall be immutable; changes shall create a new revision via change control. |
| URS-REC-05 | H | R1 | Recipe authoring shall enforce ISO 17665-1 cycle-design parameters: type (porous, gravity, liquid, sealed-vial), exposure-temperature setpoint (typically 121.1 °C or 134 °C), exposure time, F0 target, ramp-rate envelopes, pre-vacuum pulse sequence (number, depth, hold), drying time. |
| URS-REC-06 | H | R1 | Per-recipe approval shall require the Sterilization Engineer's electronic signature attesting to the validated load family + worst-case load qualification reference. |
| URS-REC-07 | M | R2 | Recipe diff between revisions shall be rendered in human-readable form for review (changed fields highlighted with old / new). |

### 5.3 Cycle-Type Specific Requirements

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CYCTYPE-01 | H | R1 | The system shall support porous-load cycles with pre-vacuum air-removal verification (Bowie-Dick or PCD-equivalent). |
| URS-CYCTYPE-02 | H | R1 | The system shall support gravity-displacement cycles for wrapped / non-porous loads where air-removal is by steam displacement. |
| URS-CYCTYPE-03 | H | R1 | The system shall support liquid-load (slow-exhaust) cycles with controlled cool-down and back-pressure phase to prevent container deformation / breakage. |
| URS-CYCTYPE-04 | H | R1 | The system shall support sealed-vial cycles with super-heated water spray (where the cabinet supports it) including counter-pressure control. |
| URS-CYCTYPE-05 | M | R2 | Recipe cycle-type selection shall enforce the corresponding mandatory pre-flight steps (e.g., daily BD test before first porous cycle of the day). |

### 5.4 Cycle Execution / F0 Calculation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CYC-01 | H | R1 | The system shall execute the loaded recipe per its setpoint envelopes; deviations shall trigger alarms classified (info / warning / critical). |
| URS-CYC-02 | H | R1 | Critical alarms (failure to reach exposure temperature, jacket pressure excursion, vacuum leak above acceptance, NCG above acceptance) shall require operator acknowledgement with reason; alarms shall not be self-clearing. |
| URS-CYC-03 | H | R1 | The temperature probe array (≥ 3 chamber + ≥ 3 load Pt100 RTDs, four-wire wiring) shall be recorded at ≥ 1 Hz; F0 shall be computed continuously per ISO 17665-1 Annex A using a z-value of 10 °C and reference temperature 121.1 °C. |
| URS-CYC-04 | H | R1 | Cycle release shall require F0 ≥ recipe-defined target value at every load-probe location; any probe below target shall fail the cycle even if the chamber-mean F0 exceeds target. |
| URS-CYC-05 | H | R1 | Manual setpoint override during a product cycle shall require dual signature (Operator + Sterilization Engineer) and a captured reason; the override shall be flagged in the executed cycle report and shall trigger an automatic deviation. |
| URS-CYC-06 | H | R1 | Cycle abort shall safe the system (isolate steam, controlled vent, drain) without compromising the audit trail or partial-cycle data. |
| URS-CYC-07 | H | R1 | Probe-failure detection (RTD open / short / drift > ± 0.5 °C against the paired chamber reference) shall trigger a critical alarm and shall exclude the failed probe from F0 calculation; cycles with insufficient remaining probes shall fail. |
| URS-CYC-08 | M | R2 | The system shall record cycle phase transitions (preconditioning → exposure → equalisation → drying → cool-down) with PTP-derived timestamps. |

### 5.5 F0 Worst-Case Load Qualification

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-F0-01 | H | R1 | The system shall record the qualified load-family reference (e.g., `LF-PARTS-A1`) associated with each cycle; cycles run against an unqualified or expired load family shall not be permitted. |
| URS-F0-02 | H | R1 | Load-family qualification shall include worst-case temperature-mapping evidence: ≥ 12 probe locations on the load with the slowest-to-heat point identified, repeated for three consecutive cycles per ISO 17665-1 § 9 (Performance Qualification). |
| URS-F0-03 | H | R1 | The system shall record the qualification cycle reference and BI-cycle reference together with each product cycle to maintain genealogy from cycle to qualification basis. |

### 5.6 Bowie-Dick, Leak, and Steam-Quality Tests

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BD-01 | H | R1 | A Bowie-Dick (or PCD-equivalent) test shall be required at the start of each operating day before the first porous-load cycle; failure shall block porous-load cycles until resolved. |
| URS-LEAK-01 | H | R1 | A vacuum-leak test shall be required at recipe-defined intervals (at minimum weekly); acceptance per EN 285 (leak rate ≤ 1.3 mbar/min); failure shall block the autoclave for use until investigated. |
| URS-SQ-01 | H | R1 | Steam quality shall be monitored at each cycle start per EN 285: non-condensable gas fraction (≤ 3.5% v/v), dryness value (≥ 0.95 for metal loads, ≥ 0.90 for porous), superheat (≤ 25 °C); excursions shall block the cycle. |
| URS-SQ-02 | M | R2 | The system shall record condensate-test evidence (where the cabinet supports automated sampling) or shall accept a manual entry of a logged-out condensate sample test result with the operator's signature. |

### 5.7 Biological & Chemical Indicator Cycle Qualification

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BI-01 | H | R1 | The system shall support BI-challenge cycles using Geobacillus stearothermophilus spore strips at recipe-defined PCD locations (≥ 1 per validated load family). |
| URS-BI-02 | H | R1 | BI lot, expiry, D-value, and population shall be recorded per cycle; BI-cycle disposition shall require Microbiology sign-off. |
| URS-CI-01 | H | R1 | Chemical-indicator (Type 5 integrating or Type 6 emulating per ISO 11140-1) results shall be recorded per cycle; CI failure shall require investigation before load release. |
| URS-BI-03 | M | R2 | The system shall maintain a BI-cycle calendar with frequency targets (at minimum quarterly per load family, plus on any change to load configuration or instrumentation). |

### 5.8 Audit Trail / Records

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | The system shall maintain a contemporaneous, time-stamped, secure audit trail covering recipe events, cycle events, alarm acknowledgements, signature events, and BI/CI/PCD entries (Annex 11 § 9). |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only; no user — including system administrators — shall be able to update or delete entries. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be performed by Quality Reviewer per cycle and by QA Compliance quarterly across the system. |
| URS-AUD-04 | H | R1 | Retention of cycle records and audit trails shall be ≥ 25 years from product expiry (sterile-product lifecycle plus statutory archival). |

### 5.9 21 CFR Part 11 / Annex 11 / Annex 1 (2022 revised)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Electronic signatures shall meet 21 CFR § 11.50: printed name + date / time + meaning of signing rendered in human-readable form. |
| URS-PART11-02 | H | R1 | Each signature shall be unique per 21 CFR § 11.100; user IDs shall not be reused or reassigned. |
| URS-PART11-03 | H | R1 | Signatures shall be cryptographically bound to the signed record per 21 CFR § 11.70; tampering shall be detectable on read. |
| URS-PART11-04 | H | R1 | Separation of duties shall be enforced per 21 CFR § 11.10(d) and § 11.10(g) authority checks. |
| URS-PART11-05 | H | R1 | Re-authentication at the moment of signing shall be required per 21 CFR § 11.200 (identity-based signature components). |
| URS-PART11-06 | H | R1 | Password / credential controls shall meet 21 CFR § 11.300 (uniqueness, periodic change, lockout). |
| URS-PART11-07 | H | R1 | Operational audit trail per § 11.10(e); accurate-and-complete copies per § 11.10(b); record protection over retention period per § 11.10(c). |
| URS-AN1-01 | H | R1 | Annex 1 (2022 revised) Contamination Control Strategy: the autoclave shall be referenced in the site CCS as a critical sterilization step with documented qualification + monitoring; loss-of-pressurisation of the adjacent cleanroom (where loads cross-transfer) shall block loading. |
| URS-AN1-02 | H | R1 | Annex 1 § 8 — Production and specific technologies: per-cycle records shall capture load lot, components / equipment included, F0 evidence, BI/CI results, and operator + verifier signatures. |

### 5.10 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-PASX-01 | H | R1 | Recipes shall be downloaded from PAS-X via REST over mTLS; checksum (SHA-256) + version validated against the local approved-recipe registry; mismatch shall block the cycle. |
| URS-INT-PASX-02 | H | R1 | An executed-cycle report (F0 evidence per probe + alarms + BI/CI + signatures + steam-quality summary) shall be pushed to PAS-X within 30 minutes of cycle end. |
| URS-INT-PASX-03 | H | R1 | The PAS-X-side EBR shall not allow downstream-step closure (e.g., release of the sterilized parts to the filling line) until the autoclave executed-cycle report is received and Quality-Reviewer-approved. |
| URS-INT-BMS-01 | H | R1 | Loss of cleanroom pressurisation (where applicable for the load family) shall block loading and signal the operator. |
| URS-INT-AD-01 | H | R1 | All authentication shall be via AD; service accounts shall use the site credential vault. |
| URS-INT-NTP-01 | H | R1 | PLC and workstations shall sync to the site PTP master (IEEE 1588); LDT clock skew shall be checked at cycle start and end (> 1 s shall trigger a cycle-quality flag). |

### 5.11 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | Records shall be Attributable to a named AD user. |
| URS-DI-02 | H | R1 | Records shall be Legible — exportable as structured PDF (with audit trail) and as CSV. |
| URS-DI-03 | H | R1 | Records shall be Contemporaneous — PLC-derived timestamps (PTP-synchronised). |
| URS-DI-04 | H | R1 | Original probe / F0 data shall be preserved unaltered; recalculations shall reference (not overwrite) originals. |
| URS-DI-05 | H | R1 | F0 + probe-array calculations shall be Accurate per OQ verification against a reference calculator. |
| URS-DI-06 | M | R2 | Records shall be Complete, Consistent, Enduring (25-yr retention) and Available (≤ 4 hours during inspection per PIC/S PI 041). |

### 5.12 Backup / Performance / Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | Historian shall be backed up nightly with WAL / point-in-time recovery; retention ≥ 25 years. |
| URS-BAK-02 | H | R1 | A documented restore test shall be performed quarterly; results filed in `RUN-BAK-RESTORE-NNN`. |
| URS-BAK-03 | M | R2 | RTO ≤ 4 hours (LDT failover); RPO ≤ 1 minute (real-time replication). |
| URS-PERF-01 | H | R1 | Sustained ≥ 1 Hz logging across all probes shall be maintained for the full cycle (typical 60-120 minutes; sealed-vial cycles up to 4 h) without data loss. |
| URS-PERF-02 | M | R2 | HMI alarm-acknowledgement latency shall be ≤ 1 s at the LDT under normal load. |
| URS-SEC-01 | H | R1 | Domain accounts only; local accounts shall be break-glass admin only with dual control. |
| URS-SEC-02 | H | R1 | Removable media shall be blocked except for vendor-approved engineering use under change control. |
| URS-SEC-03 | M | R2 | Vulnerability scans shall run monthly (Tenable Nessus); criticals remediated within 30 days. |

### 5.13 Training / Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Production access shall require role-specific LMS-recorded training, including alarm-acknowledgement and override-scenario practice. |
| URS-TRN-02 | M | R2 | Annual refresher training shall be required; Sterilization Engineer + Microbiology shall additionally complete a BI / PCD-placement competency assessment. |
| URS-PR-01 | H | R1 | Annual periodic review shall cover configuration baselines, recipe inventory + change history, audit-trail review evidence, deviation summary, alarm trends, BI-cycle outcome summary, steam-quality trends, backup-restore evidence, training currency; signed by Sterilization Engineer + Head of Sterile Mfg + Head of QA. |

### 5.14 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem with local OT cached credentials for offline operation; conditional-access policy `OT-Equipment Conditional Access (MFA at HMI session start; local cache validates last 24 h)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the cycle history DB + file-level capture of recipe and electronic batch records; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 25 y (sterilisation release record) per the consuming-record schedule. |

## 6. Acceptance Criteria

The system shall enter validated GMP use when:

1. FS, CS, RA, IQ, OQ, PQ Protocols approved per the order prescribed by GAMP 5 (2nd Edition).
2. IQ executed; configuration baseline frozen; all critical findings closed.
3. OQ executed including: alarm response (URS-CYC-02), F0 calculation verification (URS-CYC-03 / URS-CYC-04), dual-signature override (URS-CYC-05), probe-failure detection (URS-CYC-07), recipe-checksum reject (URS-INT-PASX-01), BMS interlock (URS-INT-BMS-01), audit-trail append-only (URS-AUD-02), Part 11 controls (URS-PART11-01 through -07).
4. PQ executed including: representative product cycles per validated load family, daily Bowie-Dick test, vacuum-leak test, BI-challenge cycle per load family, a probe-failure scenario triggering critical alarm, an executed-cycle report flowing to PAS-X.
5. VSR approved by Sterilization Engineer + Microbiology + Head of Sterile Mfg + Head of QA.
6. RTM shows every URS-ID mapped to ≥ 1 approved test case.

## 7. Constraints

- Vendor patches under change control; Fedegari security bulletins evaluated within 14 days, deployed within 30 days for criticals.
- PLC firmware changes (including the SIL-rated safety partition) shall require revalidation of safety functions per the safety SDLC.
- Recipe parameter changes shall be controlled through the recipe lifecycle (§ 5.2); changes affecting cycle-type or load family shall trigger PQ revalidation.
- No direct internet access from process-control VLAN; package mirrors are internal.

## 8. Assumptions

- PAS-X, BMS, AD, PTP master, NIST-traceable temperature standards, and the site QMS are validated infrastructure.
- Fedegari maintains its Themis SDLC and releases validated patches; safety partition is supplier-validated per IEC 61511.
- Steam-supply utility is qualified per `UTIL-STEAM-001` to deliver steam meeting EN 285.
- BIs are sourced from a qualified supplier with current D-value certification.

## 9. References

### US — FDA
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300 — Electronic Records; Electronic Signatures.
- 21 CFR Part 211 §§ .68 (automatic, mechanical, electronic equipment), .180 (general retention requirements), .192 (production record review).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).
- FDA *Guidance on Data Integrity and Compliance with cGMP* (2018).

### EU
- EU GMP Annex 11 §§ 4 (validation), 6 (accuracy), 9 (audit trail), 11 (periodic evaluation).
- EU GMP Annex 1 (2022 revised) §§ 5 (premises), 8 (production), 9 (viable/non-viable monitoring), 10 (quality control).
- EudraLex Vol 4 Part I § 5 (Production).
- EMA *Q&A on Annex 11*.

### International — ISO / EN
- ISO 17665-1:2024 — Sterilization of health care products — Moist heat — Part 1: Requirements for the development, validation and routine control of a sterilization process for medical devices.
- ISO 17665-2:2009 — Guidance on the application of ISO 17665-1.
- ISO 11140-1:2014 — Chemical indicators — General requirements.
- ISO 11138-1:2017 — Biological indicators — General requirements (Geobacillus stearothermophilus).
- EN 285:2015+A1:2021 — Sterilization — Steam sterilizers — Large sterilizers.
- ICH Q9(R1) — Quality Risk Management.

### Industry guidance
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE Baseline Guide *Sterile Product Manufacturing Facilities* (2nd ed.).
- PIC/S PI 041 — Good Practices for Data Management and Integrity.
- PDA Technical Report TR1 — *Validation of Moist Heat Sterilization Processes: Cycle Design, Development, Qualification and Ongoing Control*.
- USP <1211> — Sterilization and Sterility Assurance of Compendial Articles.
- USP <55> — Biological Indicators — Resistance Performance Tests.

### Vendor
- Fedegari — *FOB 3 / Themis Installation, Configuration, and Administration Reference*.
- Fedegari — *Themis Cycle-Design and F0 Calculation Theory of Operation*.

### Site
- `VEL-CCS-PLANT1-001` — Plant 1 Contamination Control Strategy per Annex 1 (2022 revised).
- `EQ-AUTOCLAVE-001` — FOB 3 equipment qualification.
- `UTIL-STEAM-001` — Site steam-supply qualification.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

