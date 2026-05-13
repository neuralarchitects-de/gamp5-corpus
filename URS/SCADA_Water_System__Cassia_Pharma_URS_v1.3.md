---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; expanded 2026-05-12 (T3 enrichment — pharma water + WFI/PW + Annex 1)"
seed_corpus_basis:
  - "josephiuliucci/SDLC-PB URS_SCADA + SDLC_CSA_HiveMQ"
  - "GAMP 5 (2nd ed.) Cat 5 conventions for custom control software"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11; Annex 1 (2022 revision); Annex 3"
  - "USP <1231> Water for Pharmaceutical Purposes; USP <645> Conductivity; USP <643> TOC; USP <85>/<86> Bacterial Endotoxin"
  - "EMA Note for Guidance on Quality of Water for Pharmaceutical Use (2020)"
  - "PIC/S PI 041; PIC/S PI 009 (API Inspection)"
  - "ASME BPE Bioprocess Equipment"
  - "ISA-88; ISA-95; ISA-101; ISA-18.2"
  - "FDA CSA (Feb 2026)"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## SCADA — Pharmaceutical Water System (Ignition 8.3 + custom Python scripts)

**Document Number:** CAS-URS-WATER-SCADA-001
**Version:** 1.2
**Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Cassia Pharma SpA, Sterile Manufacturing Plant 2, Sesto Fiorentino, Italy *(fictional)*
**System Owner:** Utilities Automation Lead
**Process Owner:** Head of Manufacturing — Sterile
**Development Owner:** Quality IT — Utilities Custom Apps
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom Application (Ignition 8.3 platform = Cat 4; site-authored Python control logic = Cat 5)
**Project Mode:** Custom-build project — site-developed system (GAMP 5 Category 5 — Bespoke; internal SDLC). System: Pharmaceutical Water System (Ignition 8.3 + custom Python scripts).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Annex 1 (2022 revision); EU GMP Annex 3; USP <1231>; USP <645>; USP <643>; USP <85>/<86>; EMA Water Note (2020); ISPE Baseline Guide *Water and Steam Systems*; ASME BPE; ISA-88; PIC/S PI 041; FDA CSA (Feb 2026).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead — Automation) | _____________ | _____________ | _____ |
| Reviewer (Utilities Automation Lead) | _____________ | _____________ | _____ |
| Reviewer (Microbiology / Water Quality Lead) | _____________ | _____________ | _____ |
| Reviewer (Process Engineer — WFI/PW) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Functional Safety Engineer) | _____________ | _____________ | _____ |
| Approver (Head of Manufacturing — Sterile) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Minor: alarm-rationalisation pointer clarified. |
| 1.2 | 2026-05-12 | (synthetic) | Tier-T3 enrichment: §5 broken into 13 subsections (WFI loop topology + dead-leg, online TOC + conductivity, sanitisation cycles, endotoxin per USP <86>, system trending + OOL/OOS, ASME BPE compliance, USP <1231> water-quality attributes, Annex 1 contamination control); risk table expanded; current-effective citations per METHODOLOGY § 2A.1. Authored to **Tier T3** (production utility SCADA spanning WFI + PW + CIP + SIP + sanitisation with online compendial monitoring; ~110-req target). |

## Definitions

| Term | Definition |
|---|---|
| SCADA | Supervisory Control and Data Acquisition |
| Ignition | Inductive Automation Ignition 8.3 (Cat 4 platform) |
| WFI | Water for Injection (USP <1231> / Ph.Eur. 0169) |
| PW | Purified Water (USP <1231> / Ph.Eur. 0008) |
| RO / EDI | Reverse Osmosis / Electrodeionization |
| MVR | Mechanical Vapour Recompression (cold-WFI generation) |
| CIP / SIP | Cleaning-in-Place / Sterilisation-in-Place |
| TOC | Total Organic Carbon (USP <643>; on-line analyzer integrated to SCADA) |
| Conductivity | USP <645> on-line measurement |
| Endotoxin | Bacterial endotoxin per USP <85> / USP <86> (LAL / rFC) |
| Hot WFI loop | WFI distribution at ≥ 80 °C (microbial-stasis design) |
| Cold WFI loop | WFI distribution at ≤ 25 °C with continuous sanitisation regime |
| Dead-leg | Branch length / diameter ratio in distribution piping; ASME BPE: ≤ 2× diameter on a closed branch |
| OOL / OOS | Out-of-Limit / Out-of-Specification |
| MES | Manufacturing Execution System (Werum PAS-X v3.2) |
| Veolia / MECO | WFI / PW generation skid vendors |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the SCADA controlling the pharmaceutical water system (PW generation, WFI generation, distribution loops, CIP / SIP cycles, point-of-use sampling, sanitisation regimes, online compendial monitoring) at Cassia Plant 2.

This is **GAMP Category 5 overall** because the site-authored Python control logic in Ignition (CIP / SIP sequencing, sanitisation scheduling, anomaly detection on TOC / conductivity / temperature) is custom code that materially affects product quality. The Ignition platform itself is Cat 4; the platform + custom code combined are validated as Cat 5.

## 2. Scope

**In scope:** Ignition 8.3 Gateway cluster (3 active + 1 standby on RHEL 9.2), tag historian (Ignition Tag Historian + InfluxDB 2.7 LTS), Vision / Perspective HMI clients on shop-floor stations and operator iPads, Allen-Bradley ControlLogix 5580 PLCs (firmware version controlled separately), site-authored Python control scripts (~2,500 lines across CIP / SIP / sanitisation / interlocks / anomaly detection), integrations with the MES (PAS-X recipe download for CIP / SIP, batch report on completion), MasterControl eQMS (deviation creation on critical alarms), on-line TOC analyzers (Sievers M9 — separate URS), on-line conductivity (Mettler-Toledo M800), on-line endotoxin (Charles River Endosafe nexgen-PTS — separate URS), and AD authentication.

**Out of scope:** Physical plant (Veolia MECO Vapor WFI still + RO / EDI / distillation / storage tanks / distribution piping) — handled under utilities qualification `EQ-WATER-001`; the MES itself; the eQMS; off-line water analyses (microbiology, full endotoxin per USP <85>) — manual workflow.

## 3. System Description and Intended Use

The SCADA continuously monitors and controls the water system: starts and stops generation skids, manages storage-tank levels with N2-blanket pressure, sequences CIP / SIP cycles per recipe, executes scheduled sanitisations (hot-water flush, ozone, chemical), monitors TOC / conductivity / temperature / pressure / flow continuously per USP <645> + <643>, raises and routes alarms, and records all events. Recipes for CIP / SIP are downloaded from PAS-X; completed cycles produce executed-batch reports back to PAS-X. Site-authored Python implements the sequencing logic and the anomaly-detection layer for early warning of microbial-growth precursors. ASME BPE compliance is the design basis for the underlying piping system; SCADA enforces operational rules (dead-leg flushing, low-point-drain interlocks, valve-sequencing for sanitisation) consistent with ASME BPE.

## 4. User Roles

| Role | Permissions |
|---|---|
| Operator | Acknowledge alarms; start / stop predefined operations within the recipe envelope. |
| Senior Operator | All Operator + second-person verification of critical-step events. |
| CIP / SIP / Sanitisation Recipe Author | Create / edit recipes in DRAFT under change control. |
| CIP / SIP / Sanitisation Recipe Reviewer | Review recipes; cannot review own. |
| CIP / SIP / Sanitisation Recipe Approver (QA) | Approve recipes to EFFECTIVE. |
| Microbiology / Water Quality Reviewer | Co-approve sanitisation cadence; review TOC / conductivity / endotoxin trends. |
| Maintenance Engineer | Run diagnostic / qualification cycles; cannot run product cycles. |
| Automation Engineer (Cat 5 SDLC) | Modify Python code under change control + signed releases. |
| Automation Reviewer (CSV) | Review Python releases; cannot approve own. |
| QA Cat 5 Reviewer | Review / approve Python releases. |
| Functional Safety Engineer | SIS-side logic governance per IEC 61511. |
| System Administrator | OS / patch / AD groups; cannot approve recipes or releases. |
| Auditor | Read-only across recipes, code, alarms, audit trails. |
| Inspection-Read-Only | Time-bound read-only access for regulator inspection (Annex 11 § 6). |

Separation of duties: Automation Engineer ≠ QA Cat 5 Reviewer of own release; Operator ≠ Verifier on the same critical step; Recipe Author ≠ Approver; Microbiology Reviewer co-approves sanitisation-cadence changes.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` direct GxP impact / `R2` indirect / `R3` none), and a verifiable `shall`-clause.

### 5.1 Platform / Hardware

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | Ignition Gateway cluster N+1 with automatic failover within 60 s; cluster status visible from the HMI. |
| URS-PLAT-02 | H | R1 | All clients on a process-control VLAN (Purdue Level 2/3); no office-network access from operator stations. |
| URS-PLAT-03 | H | R1 | UPS coverage allowing controlled shutdown for ≥ 30 min; safety-rated PLC outputs default to safe states on power loss. |
| URS-PLAT-04 | M | R2 | Tag historian retains ≥ 5 years online; older data archived to immutable cold storage with checksum. |
| URS-PLAT-05 | H | R1 | Time synchronisation via PTP (IEEE 1588) / NTP; skew ≤ 1 s monitored; degraded sync raises alarm. |

### 5.2 WFI Loop Topology + Dead-Legs (ASME BPE compliance)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LOOP-01 | H | R1 | The SCADA shall maintain a configured model of the WFI + PW distribution loop topology: tag → location → branch / drop / dead-leg / point-of-use, traceable to the as-built ASME BPE drawing set. |
| URS-LOOP-02 | H | R1 | Hot-WFI loop temperature shall be controlled to ≥ 80 °C at all monitored points; sustained excursion < 80 °C on any monitored point shall trigger a critical alarm + auto-deviation. |
| URS-LOOP-03 | H | R1 | Cold-WFI loop (when in service) shall execute a recipe-defined continuous-sanitisation regime; deviation from the regime shall block dependent operations. |
| URS-LOOP-04 | H | R1 | Dead-leg flush sequences shall be automatable per branch; the sequence shall be recorded in the executed-cycle report; missed flush blocks dependent operations. |
| URS-LOOP-05 | M | R2 | Loop flow / return-flow cross-check shall be monitored; sustained mismatch > 5% shall raise a maintenance alarm (leak / valve indication). |

### 5.3 Online TOC + Conductivity Monitoring (USP <643> + <645>)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MON-TOC-01 | H | R1 | Online TOC shall be consumed from Sievers M9 analyzers via OPC UA over TLS with mutual authentication; data quality flagged at boundary. |
| URS-MON-TOC-02 | H | R1 | TOC alert / action limits per the site water-quality plan (USP <1231> / <643>); action-limit excursion shall be a critical alarm + auto-deviation. |
| URS-MON-TOC-03 | H | R1 | Online conductivity (USP <645> Stage 1 — temperature-compensated) shall be consumed from Mettler-Toledo M800; Stage-2 / Stage-3 fallback procedures shall be documented in the cycle SOP, not in SCADA. |
| URS-MON-COND-01 | H | R1 | Conductivity action-limit excursion (per recipe-pinned threshold) shall be a critical alarm + auto-deviation. |
| URS-MON-COND-02 | M | R2 | Conductivity probes shall be tracked by serial number + calibration status; expired calibration shall flag the probe `OUT-OF-SERVICE`. |

### 5.4 Sanitisation Cycles (Hot-Water / Ozone / Chemical)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SAN-01 | H | R1 | Sanitisation cycles (hot-water flush ≥ 80 °C for the validated duration; ozone-based for cold loop; periodic chemical) shall be scheduled, executed, and recorded per the EFFECTIVE recipe. |
| URS-SAN-02 | H | R1 | Sanitisation schedules shall not be silently skipped; missed sanitisation shall be flagged and shall block dependent operations until completed and verified. |
| URS-SAN-03 | H | R1 | Ozone-based sanitisation shall be interlocked with point-of-use ozone-residual probes; ozone residual shall be below the release-threshold before re-opening the loop for production. |
| URS-SAN-04 | M | R2 | Sanitisation effectiveness shall be trended (cycle duration, end-temperatures, post-sanitisation microbial spot-check) for periodic-review evidence. |
| URS-SAN-05 | M | R2 | Sanitisation-cycle CRs shall require Microbiology Reviewer co-approval. |

### 5.5 CIP / SIP / Sanitisation Recipes (ISA-88)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REC-01 | H | R1 | Recipes shall follow the lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE. |
| URS-REC-02 | H | R1 | Only EFFECTIVE recipes shall be loadable for product cycles. |
| URS-REC-03 | H | R1 | Recipe transitions shall require role-restricted electronic signatures with separation of duties. |
| URS-REC-04 | H | R1 | EFFECTIVE recipes shall be immutable; changes shall create new revisions via change control. |
| URS-REC-05 | H | R1 | Recipe download from MES shall validate checksum / version against the local approved registry; mismatch shall block the cycle. |
| URS-REC-06 | H | R1 | Recipes shall encode loop coverage (which dead-legs / drops / points-of-use are in scope), exposure time, temperature / chemistry, and acceptance criteria. |

### 5.6 Cycle Execution and Process Data

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CYC-01 | H | R1 | The SCADA shall execute the loaded recipe per its setpoint envelopes; deviations shall trigger alarms classified by severity (info / warning / critical) per ISA-18.2. |
| URS-CYC-02 | H | R1 | Critical alarms (loss of distribution-loop temperature ≥ 80 °C on hot WFI, conductivity excursion, TOC excursion, RO/EDI fault) shall be acknowledged with reason and shall not be self-clearing. |
| URS-CYC-03 | H | R1 | Conductivity, TOC, temperature, pressure, and flow shall be recorded at ≥ 1 Hz across all critical points. |
| URS-CYC-04 | H | R1 | Manual setpoint override during a production cycle shall require dual signature (Operator + Senior Operator) and a captured reason; overrides flagged in the executed cycle report. |
| URS-CYC-05 | H | R1 | Missed sanitisation per § 5.4 shall block dependent operations until completed and verified. |

### 5.7 Endotoxin Monitoring (USP <85> / <86>) and Microbial Excursion

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ENDO-01 | H | R1 | Endotoxin results from the in-line Endosafe analyzer (where deployed) shall be consumed via secure REST; out-of-trend / above-alert-limit values shall raise a critical alarm + auto-deviation. |
| URS-ENDO-02 | H | R1 | Off-line endotoxin / microbial results from Watson LIMS shall be linked to the point-of-use, cycle, and time window for trend reporting. |
| URS-ENDO-03 | M | R2 | Endotoxin alert / action limits shall be configurable per loop + per point-of-use per the site water-quality plan; limit changes shall require Microbiology Reviewer co-approval. |

### 5.8 System Trending, OOL / OOS Detection, Anomaly Detection

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TREND-01 | H | R1 | TOC + conductivity + temperature + pressure trends shall be computed continuously over rolling windows (15-min, 1-hr, 24-hr) and exposed via Perspective dashboards. |
| URS-TREND-02 | H | R1 | OOL / OOS detection shall use statistically-rationalised limits (per ASTM E2476 / SPC); alert and action thresholds shall be recipe-pinned. |
| URS-TREND-03 | M | R2 | Anomaly detection (Python-side) shall surface microbial-growth-precursor patterns (slow TOC creep, intermittent low-flow on a drop, post-sanitisation rebound) as maintenance / warning alarms. |
| URS-TREND-04 | M | R2 | Trend data shall be exportable for periodic-review (PDF/A-3 + CSV / JSON). |

### 5.9 Custom Code (Cat 5) — SDLC

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEV-01 | H | R1 | Site-authored Python control logic shall be developed under a documented Cat-5 SDLC. |
| URS-DEV-02 | H | R1 | All code shall be version-controlled with signed commits; merges to `main` require peer review and a passing CI build. |
| URS-DEV-03 | H | R1 | Unit-test coverage shall be ≥ 90% on safety-relevant modules (CIP / SIP / sanitisation sequencing, interlocks, anomaly detection). |
| URS-DEV-04 | H | R1 | Static analysis (Ruff, mypy strict, Bandit) and dependency scanning shall run on every CI build; criticals block the build. |
| URS-DEV-05 | H | R1 | Releases shall be cryptographically signed (cosign); the deployed Gateway shall verify the signature before loading new code. |
| URS-DEV-06 | H | R1 | Each release ships with: release notes, updated FS / DS / CS, regression-test report, security-scan report, approved change-control record. |
| URS-DEV-07 | M | R2 | Determinism of sequencing logic shall be verified at OQ via canonical-input replay; bitwise reproducibility required. |

### 5.10 Audit Trail / 21 CFR Part 11 / Data Integrity

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Audit trail covering recipe transitions, cycle events, alarm acknowledgements, signatures, code releases, configuration changes. |
| URS-AUD-02 | H | R1 | Audit trail append-only; no application or admin update / delete (Annex 11 § 9). |
| URS-AUD-03 | H | R1 | Audit-trail review by Quality Reviewer per cycle and by QA Compliance quarterly. |
| URS-AUD-04 | H | R1 | Retention: cycle data + audit trails ≥ 25 years from product expiry. |
| URS-PART11-01 | H | R1 | Per § 11.10(a): procedural controls protect electronic-record validity. |
| URS-PART11-02 | H | R1 | Per § 11.10(d): access limited to authorised individuals via AD + MFA. |
| URS-PART11-03 | H | R1 | Per § 11.10(e): operational audit trail per URS-AUD-01. |
| URS-PART11-04 | H | R1 | Per § 11.50: e-signatures include printed name, date / time, meaning. |
| URS-PART11-05 | H | R1 | Per § 11.70: signatures cryptographically linked to the signed record. |
| URS-PART11-06 | H | R1 | Per § 11.100: signatures unique per individual; reuse / reassignment blocked. |
| URS-PART11-07 | H | R1 | Per § 11.200: re-authentication required at the moment of signing. |
| URS-PART11-08 | H | R1 | Per § 11.300: password / credential controls per InfoSec policy. |
| URS-AN1-01 | H | R1 | Annex 1 §§ 9-10: contamination-control implications of any setpoint override shall be evaluated per the site contamination-control strategy (CCS) and recorded with the override. |
| URS-DI-01 | H | R1 | **Attributable:** records attributable to a named user. |
| URS-DI-02 | H | R1 | **Legible:** records exportable as PDF/A-3 + CSV / JSON. |
| URS-DI-03 | H | R1 | **Contemporaneous:** PTP-synchronised timestamps from PLC level up. |
| URS-DI-04 | H | R1 | **Original:** raw probe readings preserved unaltered; corrections recorded as new annotated values referencing the original. |
| URS-DI-05 | H | R1 | **Accurate:** calculations (rolling averages, USP <645> temperature compensation, F0-style integrals) Accurate per OQ. |
| URS-DI-06 | M | R2 | **Complete / Consistent / Enduring / Available:** ≥ 25-yr retention; available ≤ 4 hours during inspection. |

### 5.11 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-MES-01 | H | R1 | Recipe download from MES (PAS-X) via REST over mTLS; checksum + version validated before load. |
| URS-INT-MES-02 | H | R1 | Executed-cycle report (profile + alarms + signatures) pushed to MES within 30 minutes of cycle end. |
| URS-INT-EQMS-01 | H | R1 | Critical alarms not closed within the configured window shall auto-create deviations in MasterControl via REST with idempotency. |
| URS-INT-TOC-01 | H | R1 | TOC values consumed via OPC UA over TLS with mutual authentication; gaps in TOC data on a hot loop trigger alarms. |
| URS-INT-COND-01 | H | R1 | Conductivity values from M800 via OPC UA mTLS; gaps trigger alarms. |
| URS-INT-ENDO-01 | M | R2 | Endosafe results via secure REST; payload signature verified. |
| URS-INT-EMS-01 | M | R2 | EMS (Pyxis / Vaisala viewLinc) cleanroom dP / T / RH consumed as cross-reference for cleanroom-supporting cycles. |
| URS-INT-AD-01 | H | R1 | Authentication via AD; service accounts via vault. |

### 5.12 Backup / DR / Performance / Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | Tag historian backed up nightly with PITR; retention ≥ 25 years. |
| URS-BAK-02 | H | R1 | Quarterly restore test, witnessed by QA. |
| URS-BAK-03 | M | R2 | RTO ≤ 4 hours; RPO ≤ 1 minute (replication). |
| URS-PERF-01 | H | R1 | Sustained ≥ 1 Hz logging across all critical channels in OQ over a 30-day window with no data loss. |
| URS-PERF-02 | M | R2 | HMI faceplate ≤ 500 ms P95; alarm-ack latency ≤ 1 s P95. |
| URS-SEC-01 | H | R1 | All authentication via AD; service accounts via vault; no local accounts other than break-glass admin. |
| URS-SEC-02 | H | R1 | All HMI traffic via TLS 1.2+; mTLS between Gateway and PLC where supported. |
| URS-SEC-03 | M | R2 | Vulnerability scans monthly; criticals remediated within 30 days. |
| URS-SEC-04 | M | R2 | Removable media blocked by GPO except vendor-approved engineering use under CR. |

### 5.13 Training / Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Production access requires recorded role-specific training (LMS). |
| URS-TRN-02 | H | R1 | Annual refresher training including current alarm / contamination scenarios. |
| URS-PR-01 | H | R1 | Annual periodic review covering configuration drift, code-release register, audit-trail review evidence, deviation / change-control summary, alarm trends, sanitisation-schedule compliance, TOC + conductivity + endotoxin trend summary, training, fitness for use; signed by Utilities Automation Lead, Head of Manufacturing — Sterile, Head of QA, Microbiology Reviewer. |

### 5.14 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem with local OT cached credentials for offline operation; conditional-access policy `OT-SCADA Conditional Access (MFA at engineering workstation; operator stations named-location + role-bound smart cards)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the SCADA historian DB plus file-level capture of PLC programs; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 15 y (utility-history) per the consuming-record schedule. |

## 6. Acceptance Criteria

System enters validated GMP use when FS, DS, CS, RA, IQ, OQ, PQ are approved and executed; PQ includes representative production cycles, ≥ 3 sanitisation cycles (hot-water + ozone + chemical), alarm-acknowledgement scenarios for each severity, Gateway failover, missed-sanitisation-block scenario, dead-leg flush coverage, and a code-release deployment under the Cat-5 SDLC; VSR approved by Utilities Automation Lead, Head of Manufacturing — Sterile, Head of QA, Microbiology Reviewer; RTM maps every URS to ≥ 1 approved test case.

## 7. Constraints

- Cat-5 SDLC governs all code changes.
- PLC firmware changes follow `EQ-WATER-001`.
- Vendor (Inductive Automation) patches under change control.
- ASME BPE constraints govern piping design; SCADA cannot relax them via configuration.
- USP / Ph.Eur. compendial limits cannot be relaxed via recipe configuration.

## 8. Assumptions

- MES, eQMS, AD, on-line TOC analyzers, conductivity analyzers, Endosafe, Watson LIMS, EMS are validated.
- PLC-level safety functions (interlocks) are SIL-rated and managed under a separate functional safety SDLC.
- Microbiology lab routinely performs off-line water-system monitoring per the site sampling plan.

## 9. References

### US — FDA / CFR / USP
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .22, .68 (water + facilities).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026).
- FDA *Guide to Inspections of High Purity Water Systems* (HPW; reference).
- USP <1231> — Water for Pharmaceutical Purposes.
- USP <645> — Water Conductivity.
- USP <643> — Total Organic Carbon.
- USP <85> / USP <86> — Bacterial Endotoxins (LAL / rFC).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11 — Computerised Systems.
- EU GMP Annex 1 (2022 revision) — Sterile Medicinal Products; Contamination Control Strategy.
- EU GMP Annex 3 — Radiopharmaceuticals (reference only).
- EU GMP Chapter 4 — Documentation (retention).
- EMA *Note for Guidance on Quality of Water for Pharmaceutical Use* (2020 / current revision).
- Ph.Eur. monographs 0008 (Purified Water), 0169 (Water for Injection).

### International — ICH / Industry
- ICH Q9(R1) — Quality Risk Management.
- ICH Q10 — Pharmaceutical Quality System.
- ISA-88 (Batch Control); ISA-95; ISA-101 (HMI); ISA-18.2 (Alarm Management).
- ASTM E2476 — Multivariate Statistical Process Control.

### Industry — ISPE / PIC/S / ASME
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE Baseline Guide — *Water and Steam Systems* (current edition).
- ISPE GAMP Good Practice Guide — *A Risk-Based Approach to Operation of GxP Computerized Systems*.
- ASME Bioprocessing Equipment (BPE) — current edition.
- PIC/S PI 041 — Good Practices for Data Management and Integrity.
- PIC/S PI 009 — API Inspection (water-system aspects).

### Vendor
- Inductive Automation — *Ignition 8.3 Reference*.
- Veolia / MECO — *WFI / PW Generation Skid Manual*.
- Allen-Bradley / Rockwell Automation — *ControlLogix 5580 Reference*.
- Mettler-Toledo — *M800 Conductivity Reference*.
- Sievers — *M9 TOC Analyzer Reference*.
- Charles River — *Endosafe nexgen-PTS Reference*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

