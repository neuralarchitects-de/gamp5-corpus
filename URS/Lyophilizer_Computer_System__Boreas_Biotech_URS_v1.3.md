---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; v1.2 enrichment 2026-05-13"
seed_corpus_basis:
  - "PharmaDevils Stability-PC + manufacturing-equipment URS family"
  - "GAMP 5 (2nd ed.) Cat 4 conventions for configured equipment-control systems"
  - "21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; EU GMP Annex 1 (2022 revised); ICH Q9(R1); PIC/S PI 041; USP <1207> Container Closure Integrity; IEC 61511 SIL 2"
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

## Lyophilizer Computer System — SP Industries LyoStar 4.5 + LyoControl 5

**Document Number:** BBT-URS-LYO-001
**Version:** 1.2
**Effective Date:** 2026-05-13 *(synthetic)*
**Site:** Boreas Biotech AB, Sterile Manufacturing Plant 1, Strängnäs, Sweden *(fictional)*
**System Owner:** Lyophilization Engineer
**Process Owner:** Head of Sterile Manufacturing
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (embedded safety partition validated per IEC 61511 SIL 2)
**Project Mode:** Configuration project on commercial software product **SP Industries LyoStar 4.5 + LyoControl 5** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Annex 1 (2022 revised) §§ 5, 8, 9; ICH Q9(R1); PIC/S PI 041; USP <1207> Container Closure Integrity Testing; USP <1208> Sterility Testing; IEC 61511 (functional safety); ANSI/ISA-88

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Lyophilization Engineer) | _____________ | _____________ | _____ |
| Reviewer (Process Sciences / PAT) | _____________ | _____________ | _____ |
| Reviewer (IT / Automation) | _____________ | _____________ | _____ |
| Reviewer (Microbiology / Sterility) | _____________ | _____________ | _____ |
| Approver (Head of Sterile Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Risk-table reformatted per v1.1 mechanical sweep. |
| 1.2 | 2026-05-13 | (synthetic) | Tier T3 enrichment (100-150 req target). Added recipe-lifecycle sub-sections per cycle phase (freezing → primary drying → secondary drying → stoppering); PAT (Pirani / capacitance manometer / residual gas analysis / end-of-primary-drying); container closure integrity; shelf-temperature mapping; vacuum + condenser monitoring; Annex 1 (2022 revised) sub-sections. Citations updated per METHODOLOGY § 2A.1. |

## Definitions

| Term | Definition |
|---|---|
| Lyo / Lyophilizer | Pharmaceutical freeze-dryer (production-scale) |
| LyoStar 4.5 | SP Industries production-scale lyophilizer (typical 30-200 m² shelf area, 5-50 kg ice capacity) |
| LyoControl 5 | SP Industries supervisory control software |
| PLC | Programmable Logic Controller (Siemens S7-1500F embedded) |
| HMI | Human-Machine Interface (LyoControl 5 client + Siemens TP1500) |
| MES | Manufacturing Execution System (Werum / Körber PAS-X v3.2) |
| LDT | Lyophilization Data Terminal — workstation running LyoControl 5 |
| Primary Drying | Sublimation phase (ice → water vapour under vacuum) |
| Secondary Drying | Desorption phase (removal of bound water) |
| Pirani gauge | Thermal-conductivity pressure gauge (gas-composition sensitive) |
| Capacitance Manometer (CM) | Gas-composition-independent absolute pressure gauge |
| Pirani-vs-CM ratio | End-of-primary-drying surrogate: ratio converges to 1 when water vapour is depleted |
| TDLAS | Tunable Diode Laser Absorption Spectroscopy (PAT for sublimation rate) |
| RGA | Residual Gas Analyser (mass-spec for chamber composition) |
| CCI | Container Closure Integrity |
| Tc / Tc' | Collapse temperature / glass-transition temperature of frozen formulation |
| Eutectic temperature | Lowest temperature at which formulation remains crystalline |
| SIL 2 | Safety Integrity Level 2 (IEC 61508 / 61511) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the lyophilizer computer system — the supervisory control + recipe-management software for the LyoStar 4.5 production freeze-dryer used in sterile parenteral fill-finish at Boreas Biotech Plant 1. The system controls the cycle through freezing, primary drying, secondary drying, and post-drying stoppering; it consumes PAT signals (Pirani / capacitance manometer / optional TDLAS / optional RGA) to determine phase endpoints; it produces a per-batch report bound to PAS-X.

## 2. Scope

**In scope:**

- LyoStar 4.5 cabinet (chamber + condenser + vacuum pumps + heat-transfer fluid skid).
- Embedded Siemens S7-1500F PLC with SIL-2 safety partition (vendor + supplier-validated).
- LyoControl 5 supervisory software on a redundant pair of LDTs (Dell OptiPlex 7060, Windows 11 IoT Enterprise LTSC).
- Historian (LyoControl Historian — InfluxDB backend).
- PAT instruments: Pirani gauge, Capacitance Manometer pair, optional TDLAS sublimation-rate sensor, optional RGA.
- Integrations: PAS-X v3.2 (recipe download / batch report), site BMS (room pressurisation interlock), AD authentication, site PTP master.
- Container Closure Integrity verification handshake with downstream automated CCI station (Wilco / Bonfiglioli AIM 5000).

**Out of scope:**

- Mechanical / cryogenic / vacuum hardware (handled under equipment qualification `EQ-LYO-001`).
- Validated cleaning cycles (`CLEAN-LYO-001`).
- Product-specific lyo recipes (developed under `PROC-DEV-PROD-XXX` and approved into the recipe registry).
- Container Closure Integrity instrument validation (`EQ-CCI-001`).
- Functional-safety partition validation (managed under safety SDLC `SAFETY-SDLC-001`).

```
                     ┌──────────────────────────────┐
                     │   PAS-X v3.2 MES (recipe /    │
                     │   batch report)               │
                     └────────────┬──────────────────┘
                                  │
                                  ▼
   ┌────────────┐   ┌────────────────────────────────────────────────┐
   │ Site BMS   │◄──┤   LyoStar 4.5 + LyoControl 5 (this URS)         │
   │ (room      │   │   Active LDT + Standby LDT (Win 11 IoT LTSC)    │
   │  press.)   │   │   PLC: Siemens S7-1500F + TP1500 HMI panel      │
   └────────────┘   │   PAT: Pirani / CM / opt. TDLAS / opt. RGA       │
                    │   Historian (InfluxDB + Grafana)                │
                    └────────────────────────────────────────────────┘
                                  │
                                  ▼
                     ┌──────────────────────────────┐
                     │ Downstream CCI Station        │
                     │ (Wilco / Bonfiglioli AIM 5000)│
                     └──────────────────────────────┘
```

## 3. System Description and Intended Use

The system controls and records the lyophilization cycle (freezing → primary drying → secondary drying → vial closure / stoppering → vial unloading) for sterile injectable products. Recipes are downloaded from PAS-X for each batch; cycle data (shelf temp, product temp via multi-thermocouple array, chamber pressure via redundant CM + Pirani, condenser temp, vial-headspace pressure, comparative pressure measurement, optional TDLAS sublimation flux) is recorded at ≥ 1 Hz; deviations from setpoint envelopes raise alarms. On completion, an executed-batch report is pushed to PAS-X and the stoppered vials are routed downstream to the automated CCI station.

GAMP Cat 4: SP Industries maintains the LyoControl SDLC; the embedded PLC code (safety functions in Cat 5 partition) is supplier-validated per IEC 61511 SIL 2; site validation focuses on installation, configuration, recipe-handling functionality, Part 11 controls, integrations, and the PAT-feedback decision logic.

## 4. User Roles

| Role | Permissions |
|---|---|
| Operator | Load recipe (from approved set); start / pause / abort cycle; document in-process events. |
| Senior Operator / Line Lead | All Operator + second-person verification of critical-step events (loading complete, stoppering complete, end-of-primary-drying confirmation). |
| Recipe Author | Create / edit recipes in DRAFT under change control. |
| Recipe Reviewer | Review recipes; cannot approve own. |
| Recipe Approver (QA) | Approve recipes to EFFECTIVE; retire. |
| Lyophilization Engineer | Recipe parameter sign-off; PAT-model + end-point criterion configuration; cycle disposition for anomalies. |
| PAT Scientist | TDLAS / RGA / Pirani-vs-CM configuration; cannot approve recipe. |
| Maintenance Engineer | Run diagnostic / qualification / leak-test cycles; cannot run product cycles. |
| Quality Reviewer | Per-batch review; gates downstream CCI step. |
| QA Compliance | Quarterly audit-trail / platform review. |
| System Administrator | Patching, AD groups, historian admin; no recipe approval. |
| Auditor | Read-only across all records and audit trails. |

Separation of duties: Operator ≠ Verifier on the same critical step; Recipe Author ≠ Approver of same recipe; PAT Scientist ≠ Recipe Approver on the same recipe; Lyophilization Engineer ≠ Quality Reviewer for the same batch.

## 5. User Requirements

### 5.1 Platform / Hardware

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | The system shall provide an active / standby LDT pair with automatic failover within 30 seconds; no operator action shall be required. |
| URS-PLAT-02 | H | R1 | LDTs shall be on UPS sized for ≥ 30 min controlled cycle hold; PLC and TP1500 shall be on a separate UPS branch. |
| URS-PLAT-03 | H | R1 | All LDTs and the historian shall reside on a dedicated process-control VLAN; no office-network access shall be permitted. |
| URS-PLAT-04 | M | R2 | Historian shall retain ≥ 5 years of cycle data online; older data shall be archived to immutable cold storage. |
| URS-PLAT-05 | H | R1 | The safety partition of the PLC (SIL 2) shall be physically and logically separated from the supervisory functions; supervisory-software defects shall not be able to bypass safety functions. |
| URS-PLAT-06 | M | R2 | Hot-standby switch-over time (within the PLC redundant CPU pair) shall be ≤ 100 ms; switch-over event shall be logged and shall not interrupt cycle data capture. |

### 5.2 Recipe Lifecycle and Per-Phase Parameters

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REC-01 | H | R1 | Recipes shall follow a documented lifecycle: DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE. |
| URS-REC-02 | H | R1 | Only EFFECTIVE recipes may be loaded for product cycles. |
| URS-REC-03 | H | R1 | Recipe transitions shall require an electronic signature from a user with the appropriate role. |
| URS-REC-04 | H | R1 | EFFECTIVE recipes shall be immutable; changes shall create a new revision via change control. |
| URS-REC-05 | H | R1 | Recipe download from PAS-X shall validate a checksum/version match against the local approved-recipe registry; mismatch shall block the cycle. |
| URS-REC-06 | H | R1 | The freezing phase shall be parameterised: shelf-temperature target ramp (start_T, end_T, rate °C/min), nucleation-control method (passive / controlled — ControLyo / ice-fog), hold time at target temperature, vial-temperature acceptance band. |
| URS-REC-07 | H | R1 | The primary drying phase shall be parameterised: shelf-temperature setpoint, chamber-pressure setpoint (typically 30-300 mTorr), maximum allowed product temperature (constrained to ≤ Tc' − safety margin), expected duration, end-point criterion (time-based / Pirani-vs-CM-based / TDLAS-based). |
| URS-REC-08 | H | R1 | The secondary drying phase shall be parameterised: shelf-temperature ramp + hold, chamber-pressure setpoint, expected duration, residual-moisture target (informing release-test plan). |
| URS-REC-09 | H | R1 | The stoppering step shall be parameterised: hydraulic-press pressure target, stoppering atmosphere (N₂ / sterile air / partial vacuum), stoppering-complete second-person verification. |
| URS-REC-10 | M | R2 | The recipe-diff renderer shall show field-by-field old/new on revision review for each phase block. |

### 5.3 Cycle Execution and Data Capture

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CYC-01 | H | R1 | The system shall execute the loaded recipe per its setpoint envelope; deviations shall trigger alarms classified by severity (info / warning / critical). |
| URS-CYC-02 | H | R1 | Critical alarms (chamber leak above acceptance, condenser failure, loss of vacuum, shelf temperature out of envelope > 2 minutes, product temperature exceeding Tc' for > 10 s) shall be acknowledged with reason; unacknowledged criticals shall block cycle progression beyond the next recipe step. |
| URS-CYC-03 | H | R1 | Shelf temperature (multiple zones), product temperature (multi-thermocouple array — ≥ 6 representative vials), chamber pressure (redundant CM + Pirani), condenser temperature, vial-headspace pressure, and comparative pressure measurement shall be recorded at ≥ 1 Hz throughout the cycle. |
| URS-CYC-04 | H | R1 | Cycle data shall be timestamped with PLC-derived time (synchronised to site PTP master); LDT clock skew shall be checked at cycle start and end. |
| URS-CYC-05 | H | R1 | Manual setpoint override during a product cycle shall require dual signature (Operator + Lyophilization Engineer) and a captured reason; overrides shall be flagged in the batch report and shall trigger an automatic deviation. |
| URS-CYC-06 | H | R1 | Loading-complete and stoppering-complete events are critical steps requiring second-person verification with separate signatures. |
| URS-CYC-07 | M | R2 | Cycle abort shall safe the system (vacuum break, shelves to safe temperature, condenser controlled discharge) without compromising audit trail. |
| URS-CYC-08 | H | R1 | Thermocouple drift detection shall identify probes drifting > ± 1 °C against the median of remaining probes; flagged probes shall be excluded from end-of-phase decision logic. |

### 5.4 Process Analytical Technology (Pirani, Capacitance Manometer, TDLAS, RGA)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PAT-01 | H | R1 | The system shall continuously read the chamber pressure via both a Pirani gauge and a Capacitance Manometer (gas-composition-independent reference). |
| URS-PAT-02 | H | R1 | The Pirani-vs-CM ratio shall be computed and trended throughout primary drying; convergence to a recipe-defined ratio (typically ~1.0 ± tolerance) shall be one of the end-of-primary-drying criteria. |
| URS-PAT-03 | H | R1 | Where TDLAS instrumentation is installed (line 1), sublimation-rate data shall be consumed; rate decay below a recipe-defined threshold for a recipe-defined duration shall be an alternative end-of-primary-drying criterion. |
| URS-PAT-04 | M | R2 | Where an RGA is installed (line 1), residual-gas composition shall be trended to detect non-condensable gas ingress or leak signatures (m/z 28 nitrogen + m/z 32 oxygen tracking). |
| URS-PAT-05 | H | R1 | End-of-primary-drying determination shall be deterministic, repeatable, and reconstructable from logged inputs and the configured criterion. |
| URS-PAT-06 | H | R1 | Loss of CM during primary drying shall trigger a critical alarm; the system shall fall back to time-based phase transition per recipe contingency and shall require Lyophilization Engineer disposition. |
| URS-PAT-07 | M | R2 | PAT instrument calibration records shall be available to the LyoControl UI; an out-of-calibration PAT instrument shall not permit a PAT-based phase transition. |

### 5.5 Shelf-Temperature Mapping

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SHELF-01 | H | R1 | Shelf-surface temperature uniformity shall be qualified at OQ across the operating range (typ −50 °C to +60 °C); acceptance per ISPE Baseline Guide *Sterile Product Manufacturing Facilities* (typically ± 1.5 °C across shelf at steady state). |
| URS-SHELF-02 | H | R1 | The recipe registry shall store the shelf-mapping qualification reference; cycles run against an expired or void shelf-mapping shall not be permitted. |
| URS-SHELF-03 | M | R2 | The system shall record actual shelf-zone temperature spread per cycle; spread > qualified envelope shall flag the cycle for engineering review. |

### 5.6 Vacuum + Condenser Monitoring

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VAC-01 | H | R1 | Vacuum-pump status (rotation rate, motor current, oil temperature where applicable) shall be monitored continuously; degradation indicators shall raise predictive-maintenance alerts. |
| URS-VAC-02 | H | R1 | A scheduled vacuum-leak test (recipe-defined cadence, at minimum monthly) shall be required; failure shall block the lyophilizer from product use. |
| URS-VAC-03 | H | R1 | Condenser-coil temperature shall be monitored continuously; failure to maintain ≤ recipe-defined target (typically ≤ −60 °C) during primary drying shall raise a critical alarm. |
| URS-VAC-04 | M | R2 | Condenser-ice-load estimation shall be computed and tracked; exceeding capacity threshold shall raise a warning. |

### 5.7 Container Closure Integrity (CCI) Handshake

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CCI-01 | H | R1 | At cycle end, the system shall pass an electronic batch-record handshake to the downstream CCI station (Wilco / Bonfiglioli AIM 5000) including: batch-ID, stoppering atmosphere, headspace-pressure summary, vial count, fill-line cross-reference. |
| URS-CCI-02 | H | R1 | The PAS-X EBR for the batch shall not allow batch release until the CCI station returns a pass-rate summary meeting USP <1207> sample acceptance. |
| URS-CCI-03 | M | R2 | Headspace-pressure measurement (via comparative pressure measurement or laser-headspace analyser where available) shall be trended per batch to monitor stoppering-process consistency. |

### 5.8 Audit Trail / Records

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Time-stamped, secure audit trail covering recipe events, cycle events, alarm acknowledgements, signature events, and PAT-decision events (Annex 11 § 9). |
| URS-AUD-02 | H | R1 | Audit trail shall be append-only; no user shall edit or delete entries. |
| URS-AUD-03 | H | R1 | Audit-trail review by Quality Reviewer per batch and by QA Compliance quarterly. |
| URS-AUD-04 | H | R1 | Retention: cycle data + audit trails ≥ 25 years from product expiry. |

### 5.9 21 CFR Part 11 / Annex 11 / Annex 1 (2022 revised)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | E-signatures shall meet 21 CFR § 11.50: printed name + date / time + meaning rendered in human-readable form. |
| URS-PART11-02 | H | R1 | Each signature shall be unique per 21 CFR § 11.100; user IDs shall not be reused. |
| URS-PART11-03 | H | R1 | Signatures shall be cryptographically bound to the signed record per 21 CFR § 11.70. |
| URS-PART11-04 | H | R1 | Separation of duties shall be enforced per 21 CFR § 11.10(d) + § 11.10(g). |
| URS-PART11-05 | H | R1 | Re-authentication shall be required at the moment of signing per 21 CFR § 11.200. |
| URS-PART11-06 | H | R1 | Password / credential controls shall meet 21 CFR § 11.300. |
| URS-PART11-07 | H | R1 | Operational audit trail per § 11.10(e); accurate-and-complete copies per § 11.10(b); record protection per § 11.10(c). |
| URS-AN1-01 | H | R1 | Annex 1 (2022 revised) Contamination Control Strategy: the lyophilizer shall be referenced in the site CCS as a critical sterile-processing step with documented qualification and monitoring; loading shall be blocked on loss of cleanroom pressurisation. |
| URS-AN1-02 | H | R1 | Annex 1 § 8 — manual setpoint changes during the freeze step that could impact product quality shall require dual signature. |
| URS-AN1-03 | H | R1 | Annex 1 § 8.123 — automated stoppering in the lyophilizer shall be qualified for stoppering atmosphere and stoppering pressure; non-conformance shall block batch release. |

### 5.10 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-PASX-01 | H | R1 | Recipes shall be downloaded from PAS-X via REST over mTLS; version + checksum validated before load. |
| URS-INT-PASX-02 | H | R1 | Executed-batch report (cycle profile + alarms + PAT decisions + signatures) shall be pushed to PAS-X within 30 minutes of cycle end. |
| URS-INT-PASX-03 | H | R1 | The PAS-X-side EBR shall not allow batch-release-step closure until the lyo cycle report + CCI station result are received and Quality-Reviewer-approved. |
| URS-INT-BMS-01 | H | R1 | The system shall consume room-pressure interlock from the BMS; loss of pressurisation shall abort loading and signal the operator. |
| URS-INT-AD-01 | H | R1 | Authentication via AD; service accounts use credential vault. |
| URS-INT-CCI-01 | H | R1 | The system shall transmit a CCI-handshake payload (URS-CCI-01) to the downstream CCI station; persistent transmission failure shall block batch closure. |
| URS-INT-NTP-01 | H | R1 | PLC + workstations shall sync to site PTP master; LDT clock skew shall be checked at cycle start and end. |

### 5.11 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | Records shall be Attributable to a named AD user. |
| URS-DI-02 | H | R1 | Records shall be Legible — exportable as structured PDF + CSV. |
| URS-DI-03 | H | R1 | Records shall be Contemporaneous — synchronised PTP-derived timestamps. |
| URS-DI-04 | H | R1 | Original cycle data preserved unaltered; recalculations reference (not overwrite) originals. |
| URS-DI-05 | H | R1 | Calculations Accurate — Pirani-vs-CM ratio, mass-flow on vacuum break, sublimation rate verified per OQ. |
| URS-DI-06 | M | R2 | Records Complete / Consistent / Enduring (25-yr retention) / Available (≤ 4 hours during inspection). |

### 5.12 Backup / DR / Performance / Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | Historian backed up nightly with PITR; retention 25 years. |
| URS-BAK-02 | H | R1 | Quarterly restore test, witnessed. |
| URS-BAK-03 | M | R2 | RTO ≤ 4 hours (LDT failover); RPO ≤ 1 minute (real-time replication). |
| URS-PERF-01 | H | R1 | Sustained ≥ 1 Hz logging across all critical channels for full cycle (≥ 96 hours). |
| URS-PERF-02 | M | R2 | Alarm acknowledgement latency ≤ 1 second at the HMI. |
| URS-SEC-01 | H | R1 | All accounts AD-managed; no local QC / Operator accounts; break-glass admin only. |
| URS-SEC-02 | H | R1 | Removable media blocked except for vendor-approved engineering use under change control. |
| URS-SEC-03 | M | R2 | Vulnerability scans monthly; criticals remediated within 30 days. |

### 5.13 Alarm Management and History

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ALM-01 | H | R1 | All alarms shall be classified (info / warning / critical) per ANSI/ISA-18.2; class-specific handling shall be enforced. |
| URS-ALM-02 | H | R1 | Alarm-history shall be retained for ≥ 10 years; queries for inspection shall return ≤ 30 s for any 12-month window. |
| URS-ALM-03 | H | R1 | Alarm flood detection (> 10 critical alarms in 60 s) shall trigger an engineering review event and shall not silently suppress alarms. |
| URS-ALM-04 | M | R2 | Per-cycle alarm-summary shall be rendered in the batch report (count by class + top-5 by recurrence). |
| URS-ALM-05 | M | R2 | Alarm-shelving (operator-acknowledged suspension of a noisy non-critical alarm) shall be limited to recipe-defined non-critical alarms and shall auto-expire within 1 hour. |

### 5.14 Isolator / Cleanroom Interface

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ISO-01 | H | R1 | Where the lyophilizer is fed from an isolator-based aseptic filling line, the system shall consume the isolator's "ready-to-receive" interlock signal; loading shall be blocked if the isolator is not READY. |
| URS-ISO-02 | M | R2 | Cleanroom-class-change (e.g., Grade A breach detected by EMS) shall raise a critical alarm and shall block loading. |
| URS-ISO-03 | M | R2 | The system shall log all loading and stoppering-bridge transitions for batch-genealogy reference into the cleanroom CCS. |

### 5.15 Cleaning + CIP Cycle Records

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CIP-01 | H | R1 | The system shall record cleaning-cycle references (date, cleaning recipe, operator + verifier signatures) applied between product batches. |
| URS-CIP-02 | H | R1 | The "dirty-hold time" + "clean-hold time" between cleaning and next batch start shall be enforced per recipe; expiry shall block the next batch until re-cleaning. |
| URS-CIP-03 | M | R2 | Manual-cleaning entries (non-automated cleaning steps) shall be capturable with witness signature. |

### 5.16 Training / Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Production access requires recorded role-specific training (LMS). |
| URS-TRN-02 | M | R2 | Annual refresher training, including alarm-acknowledgement scenarios. |
| URS-TRN-03 | M | R2 | Lyophilization Engineer + PAT Scientist shall complete a PAT-decision-logic competency assessment. |
| URS-PR-01 | H | R1 | Annual periodic review covering configuration, recipe inventory, audit-trail review evidence, deviation summary, alarm trends, PAT-decision summary, shelf-mapping currency, leak-test history, CIP / cleaning cycle history, backup-restore, training, fitness for use; signed by Lyophilization Engineer + Head of Sterile Mfg + Head of QA. |

### 5.17 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem with local OT cached credentials for offline operation; conditional-access policy `OT-Equipment Conditional Access (MFA at HMI session start; local cache validates last 24 h)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the cycle-history DB plus file-level capture of recipe and electronic batch records; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 25 y (sterilisation / batch release record) per the consuming-record schedule. |

## 6. Acceptance Criteria

The system shall enter validated GMP use when FS / CS / RA / IQ / OQ / PQ are approved and executed; PQ shall include: ≥ 3 representative product cycles spanning slow / fast cake matrices; 1 LDT failover; 1 vacuum-leak-test cycle; 1 critical-alarm scenario (e.g., simulated CM loss); 1 PAT-based phase transition (Pirani-vs-CM); 1 manual-override dual-signature test; an end-to-end CCI handshake to the downstream station; cycle-report flow to PAS-X verified. VSR approved by Lyo Engineer + Head of Sterile Mfg + Head of QA; RTM maps every URS to ≥ 1 approved test case.

## 7. Constraints

- SP Industries patches under change control.
- PLC firmware changes (especially SIL 2 partition) require revalidation of safety functions per `SAFETY-SDLC-001`.
- Recipe parameter changes affecting Tc'/end-point criteria require Lyophilization Engineer sign-off + PQ revalidation.
- No direct internet access from process-control VLAN.

## 8. Assumptions

- PAS-X, BMS, AD, PTP master are validated infrastructure.
- PAT instruments are calibrated per `CAL-LYO-PAT-001` and qualified per `EQ-LYO-PAT-001`.
- Downstream CCI station is qualified under `EQ-CCI-001`.
- Steam-supply utility is qualified per `UTIL-STEAM-001`.

## 9. References

### US — FDA
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .68, .180, .192.
- FDA *Guidance for Industry — PAT: A Framework for Innovative Pharmaceutical Development, Manufacturing, and Quality Assurance* (2004).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EU GMP Annex 1 (2022 revised) §§ 5, 8 (8.123 stoppering qualification), 9.
- EudraLex Vol 4 Part I.

### International — ICH / ISO / USP
- ICH Q9(R1) — Quality Risk Management.
- ICH Q8(R2) — Pharmaceutical Development.
- ICH Q14 — Analytical Procedure Development.
- USP <1207> — Container Closure Integrity Evaluation.
- USP <1208> — Sterility Testing — Validation of Isolator Systems.
- USP <790> — Visible Particulates in Injections.
- ISO 11608 — Needle-based injection systems (where in scope downstream).
- IEC 61511 — Functional Safety for Process Industry; IEC 61508 (general).
- ANSI/ISA-88 — Batch control.

### Industry guidance
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE Baseline Guide *Sterile Product Manufacturing Facilities* (2nd ed.).
- PIC/S PI 041 — Good Practices for Data Management and Integrity.
- PDA Technical Report TR68 — *Hardware and Process Validation of Lyophilization*.

### Vendor
- SP Industries — *LyoStar 4.5 / LyoControl 5 Installation, Configuration, and Administration Reference*.
- SP Industries — *Pirani-vs-CM End-of-Primary-Drying Theory of Operation*.
- Wilco / Bonfiglioli — *AIM 5000 CCI Station Integration Manual*.

### Site
- `EQ-LYO-001` equipment qualification.
- `EQ-LYO-PAT-001` PAT instrument qualification.
- `EQ-CCI-001` CCI station qualification.
- `SAFETY-SDLC-001` safety partition SDLC.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

