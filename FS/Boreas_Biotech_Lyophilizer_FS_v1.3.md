---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-26; v1.2 enrichment 2026-05-13"
seed_corpus_basis:
  - "BBT-URS-LYO-001 (parent URS)"
  - "GAMP 5 (2nd ed.) Cat 4 conventions for configured equipment-control systems"
  - "21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; EU GMP Annex 1 (2022 revised); PIC/S PI 041"
  - "IEC 61511 SIL 2 (for embedded safety functions)"
parent_urs:
  document_number: BBT-URS-LYO-001
  version: 1.2
  file: ../../URS/_generated/final/Lyophilizer_Computer_System__Boreas_Biotech_URS_v1.3.md
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

# Functional Specification (FS)

## Lyophilizer Computer System — SP Industries LyoStar 4.5 + LyoControl 5

**Document Number:** BBT-FS-LYO-001
**Version:** 1.2
**Effective Date:** 2026-05-13 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Parent URS:** BBT-URS-LYO-001 v1.2
**Site:** Boreas Biotech AB, Sterile Manufacturing Plant 1, Strängnäs, Sweden *(fictional)*
**System Owner:** Lyophilization Engineer
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (embedded PLC safety partition supplier-validated per IEC 61511 SIL 2)
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; EU GMP Annex 1 (2022 revised); ICH Q9(R1); PIC/S PI 041; USP <1207>

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect / Automation) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Lyophilization Engineer) | _____________ | _____________ | _____ |
| Reviewer (PAT Scientist) | _____________ | _____________ | _____ |
| Reviewer (IT / Automation) | _____________ | _____________ | _____ |
| Approver (Head of Sterile Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue, derived from BBT-URS-LYO-001 v1.0. |
| 1.2 | 2026-05-13 | (synthetic) | Expanded to per-URS-ID specifications (no range compression) per METHODOLOGY § 2A.7. Added Recipe-lifecycle per-phase (freeze / primary / secondary / stoppering), PAT (Pirani/CM/TDLAS/RGA), shelf-mapping, vacuum + condenser, CCI handshake. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## Definitions

Inherited from BBT-URS-LYO-001. Additional FS-specific terms:

| Term | Definition |
|---|---|
| FS | Functional Specification (this document) |
| LDT | Lyophilization Data Terminal |
| RPD | Recipe parameter definition |
| TP1500 | Siemens HMI panel at the cabinet |
| PTP | Precision Time Protocol (IEEE 1588) |
| SIL 2 | Safety Integrity Level 2 (IEC 61511) |
| Pirani-CM-ratio | Pirani gauge reading divided by Capacitance Manometer reading |

---

## 1. Purpose

This FS specifies, at the system-design level, how LyoStar 4.5 + LyoControl 5 are configured and integrated to satisfy `BBT-URS-LYO-001` v1.2. The embedded Siemens S7-1500F safety partition is supplier-validated per IEC 61511 SIL 2; the FS treats it as a black-box safety function and validates its exposed interface only.

## 2. Scope

Per BBT-URS-LYO-001 § 2.

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source / Vendor | Notes |
|---|---|---|---|---|---|
| C-01 | LyoStar 4.5 cabinet | Equipment | (equipment) | SP Industries | mechanical / cryo / vacuum |
| C-02 | Siemens S7-1500F PLC | Embedded controller | 4 (safety partition supplier-validated SIL 2) | Siemens | inside cabinet |
| C-03 | TP1500 HMI | Embedded HMI | 4 | Siemens | cabinet-mounted touch panel |
| C-04 | LyoControl 5 | COTS app | 4 | SP Industries | supervisory app |
| C-05 | Active LDT | Workstation | 4 | Dell | Win 11 IoT LTSC |
| C-06 | Standby LDT | Workstation | 4 | Dell | warm-standby |
| C-07 | LyoControl Historian | COTS app | 4 | SP Industries | InfluxDB backend |
| C-08 | Grafana | COTS app | (read-only viz) | Grafana Labs | trend-display only |
| C-09 | PAS-X v3.2 | COTS MES | 4 (separate URS/FS) | Werum / Körber | recipe + batch report counterparty |
| C-10 | Site BMS | COTS BMS | 4 | (site) | room-pressure interlock |
| C-11 | Capacitance Manometer (pair) | PAT instrument | 4 | MKS / Inficon | redundant |
| C-12 | Pirani gauge | PAT instrument | 4 | (vendor) | thermal-conductivity |
| C-13 | TDLAS (line 1 only) | PAT instrument | 4 | Physical Sciences Inc. | sublimation rate |
| C-14 | RGA (line 1 only) | PAT instrument | 4 | Stanford Research | residual-gas analysis |
| C-15 | Wilco/Bonfiglioli AIM 5000 CCI | Downstream station | 4 (separate URS/FS) | Wilco | CCI handshake |
| C-16 | AD / PKI | COTS infra | (infra) | Microsoft | AuthN + signature |
| C-17 | PTP master | COTS infra | (infra) | (site) | IEEE 1588 |

### 3.2 Logical Architecture

```
                       ┌──────────────────────────────────────┐
                       │  Active Directory + Site PKI + PTP    │
                       └──────────────┬───────────────────────┘
                                      │
                                      ▼
   ┌────────────────────────────────────────────────────────────────┐
   │      LyoControl 5 Active LDT  ←──→  Standby LDT (auto ≤ 30 s)  │
   │   ┌──────────────────────────┐  ┌──────────────────────────┐   │
   │   │  Recipe + cycle UI       │  │  Historian (InfluxDB) +  │   │
   │   │  PAT decision viewer     │  │  Grafana (read-only)     │   │
   │   └──────────────────────────┘  └──────────────────────────┘   │
   └────────┬──────────────────────┬─────────────────────────────────┘
            │ OPC UA mTLS          │ REST mTLS / vendor protocol
            ▼                      ▼
   ┌────────────────────┐    ┌────────────────────────────────────┐
   │ S7-1500F PLC + TP  │    │ PAS-X v3.2 MES (recipe / batch rpt)│
   │ + PAT instruments  │    └────────────────────────────────────┘
   │ Safety partition   │
   │ (SIL 2 supplier-   │    ┌────────────────────────────────────┐
   │  validated)        │    │ Site BMS (room-press. interlock)   │
   └────────────────────┘    └────────────────────────────────────┘
                              ┌────────────────────────────────────┐
                              │ Wilco/Bonfiglioli AIM 5000 CCI     │
                              └────────────────────────────────────┘
```

### 3.3 Functional Modules

| Module | URS sections |
|---|---|
| M-PLAT | URS-PLAT-* |
| M-REC | URS-REC-* |
| M-CYC | URS-CYC-* |
| M-PAT | URS-PAT-* |
| M-SHELF | URS-SHELF-* |
| M-VAC | URS-VAC-* |
| M-CCI | URS-CCI-* |
| M-AUD | URS-AUD-* |
| M-PART11 | URS-PART11-*, URS-AN1-* |
| M-INT | URS-INT-* |
| M-DI | URS-DI-* |
| M-PERF | URS-PERF-*, URS-BAK-* |
| M-SEC | URS-SEC-* |
| M-TRN | URS-TRN-* |
| M-PR | URS-PR-* |

---

## 4. Functional Specifications

### 4.1 Platform / Hardware (M-PLAT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | Active / standby LDT pair with shared replicated state via PostgreSQL streaming replication; auto-failover ≤ 30 s; verified `OQ-FAILOVER-01`. |
| FS-PLAT-02 | URS-PLAT-02 | LDTs on UPS (≥ 30 min hold), PLC + TP1500 on separate UPS branch; verified `OQ-UPS-HOLD-01`. |
| FS-PLAT-03 | URS-PLAT-03 | Process-control VLAN with no route to office network; verified by network-config audit. |
| FS-PLAT-04 | URS-PLAT-04 | Historian retains ≥ 5 y online; archival to immutable cold storage. |
| FS-PLAT-05 | URS-PLAT-05 | Safety partition runs in dedicated S7-1500F runtime; supervisory I/O segregated by hardware DI/DO; no bidirectional control coupling from supervisory; `OQ-SAFETY-PARTITION-01` exercises bypass-attempt scenarios. |
| FS-PLAT-06 | URS-PLAT-06 | Redundant CPU pair (1oo2) in hot-standby; sync over PROFINET-IRT; switch-over ≤ 100 ms; event logged to audit trail; verified `OQ-CPU-REDUNDANCY-01`. |

### 4.2 Recipe Lifecycle and Per-Phase Parameters (M-REC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REC-01 | URS-REC-01 | Recipe state machine {DRAFT, REVIEW, APPROVED, EFFECTIVE, OBSOLETE}; transitions API-enforced server-side. |
| FS-REC-02 | URS-REC-02 | Cycle-load endpoint validates state = EFFECTIVE; non-EFFECTIVE rejected with `RECIPE_NOT_EFFECTIVE`. |
| FS-REC-03 | URS-REC-03 | Re-authenticated electronic signature at each transition; role-mapped permission. |
| FS-REC-04 | URS-REC-04 | EFFECTIVE recipes immutable; changes create revision N+1 in DRAFT. |
| FS-REC-05 | URS-REC-05 | Recipe download from PAS-X delivers content + version + SHA-256 checksum; LDT validates against local approved-recipe registry; mismatch blocks cycle. |
| FS-REC-06 | URS-REC-06 | Freezing-phase block validates: start_T_C, end_T_C, ramp_rate_C_per_min, nucleation_method (passive / ControLyo / ice-fog), hold_time_min, vial_T_band_C; out-of-range fields block approval; verified `OQ-REC-FREEZE-PARAMS-01`. |
| FS-REC-07 | URS-REC-07 | Primary-drying block validates: shelf_T_set, chamber_P_mTorr_set, max_product_T (required to specify Tc' − margin), expected_duration_h, end_point_criterion (enum: time_based / pirani_cm_ratio / tdlas_rate); criterion-specific parameters validated; verified `OQ-REC-PRIMDRY-PARAMS-01`. |
| FS-REC-08 | URS-REC-08 | Secondary-drying block validates: ramp + hold, chamber_P_set, expected_duration_h, residual_moisture_target_pct; verified `OQ-REC-SECDRY-PARAMS-01`. |
| FS-REC-09 | URS-REC-09 | Stoppering block validates: hydraulic_pressure_set_bar, atmosphere (enum: N2 / sterile_air / partial_vacuum), verification_required = true; verified `OQ-REC-STOPPER-PARAMS-01`. |
| FS-REC-10 | URS-REC-10 | Recipe-diff renderer presents per-phase block changes with old/new + change-reason. |

### 4.3 Cycle Execution and Data Capture (M-CYC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CYC-01 | URS-CYC-01 | Cycle engine evaluates setpoint envelope per recipe step; deviations classified info / warning / critical per recipe-defined thresholds. |
| FS-CYC-02 | URS-CYC-02 | Critical alarms (chamber leak, condenser failure, loss of vacuum, shelf-T OOE > 2 min, product-T > Tc' for > 10 s) require ack + reason; unacknowledged criticals block step progression. |
| FS-CYC-03 | URS-CYC-03 | Channels logged at ≥ 1 Hz: shelf temperature (per zone), product temperature (TC array — ≥ 6 vials), chamber pressure (redundant CM + Pirani), condenser temperature, vial-headspace pressure, comparative pressure measurement. |
| FS-CYC-04 | URS-CYC-04 | Timestamps PLC-derived (PTP-master); LDT clock skew checked at cycle start + end; skew > 1 s triggers a cycle-quality flag. |
| FS-CYC-05 | URS-CYC-05 | Manual setpoint override during product cycle requires Operator + Lyophilization Engineer dual signature with reason captured; auto-deviation to MasterControl eQMS. |
| FS-CYC-06 | URS-CYC-06 | Loading-complete and stoppering-complete steps configured as critical-step verification points; second-person verification widget mandatory; verifier user-id ≠ operator user-id. |
| FS-CYC-07 | URS-CYC-07 | Cycle-abort sequence safes the system (vacuum break, shelves to safe temperature, condenser controlled discharge) without disturbing audit-trail integrity. |
| FS-CYC-08 | URS-CYC-08 | Per-TC drift monitor evaluates each probe vs median of remaining probes; drift > ± 1 °C triggers warning + probe-exclusion from end-of-phase logic; verified `OQ-TC-DRIFT-DETECT-01`. |

### 4.4 Process Analytical Technology (M-PAT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PAT-01 | URS-PAT-01 | Pirani + CM(pair) inputs polled at ≥ 1 Hz via OPC UA; both readings written to ChannelLog; failure of one CM triggers redundancy alarm but continues with surviving CM. |
| FS-PAT-02 | URS-PAT-02 | Pirani-vs-CM-ratio = Pirani_mTorr / CM_mean_mTorr computed at each sample; recipe-defined convergence band (typically ratio ∈ [0.95, 1.05] for ≥ recipe_dwell_min) drives end-of-primary-drying call; verified `OQ-PIRANI-CM-RATIO-01`. |
| FS-PAT-03 | URS-PAT-03 | TDLAS subscription (line 1) consumes sublimation-rate (g/h) at 1 Hz; rate < recipe-defined threshold for ≥ recipe_dwell_min is alternative end-point criterion. |
| FS-PAT-04 | URS-PAT-04 | RGA subscription (line 1) consumes m/z 28 + m/z 32 intensities; trending shows non-condensable-gas ingress signatures; alarm on threshold breach. |
| FS-PAT-05 | URS-PAT-05 | End-of-primary-drying decision recorded with: criterion_id, input_window, decision_value, threshold, decision_timestamp, signature event; reconstructable from logs; verified `OQ-PAT-DETERMINISTIC-01`. |
| FS-PAT-06 | URS-PAT-06 | CM-loss watchdog (≥ 3 missed samples from both CMs) triggers critical alarm + falls back to time-based phase transition per recipe contingency; cycle disposition gate set to "Lyo Engineer review required"; verified `OQ-PAT-CM-LOSS-FALLBACK-01`. |
| FS-PAT-07 | URS-PAT-07 | PAT-instrument-calibration-state queried at cycle start; OUT_OF_CAL state disables PAT-based phase transition (forces time-based fallback) and raises engineering alarm. |

### 4.5 Shelf-Temperature Mapping (M-SHELF)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SHELF-01 | URS-SHELF-01 | OQ shelf-mapping test exercises operating range (−50 °C to +60 °C in 10 °C steps) with ≥ 9 probe positions per shelf; acceptance ± 1.5 °C steady-state spread; results stored in shelf-mapping registry. |
| FS-SHELF-02 | URS-SHELF-02 | Recipe-load handler queries shelf-mapping registry; cycles run against expired / void mapping blocked; verified `OQ-SHELF-MAP-GATE-01`. |
| FS-SHELF-03 | URS-SHELF-03 | Per-cycle shelf-spread metric (max − min across shelf zones during steady-state phases) logged; > qualified envelope flags cycle for engineering review. |

### 4.6 Vacuum + Condenser (M-VAC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VAC-01 | URS-VAC-01 | Vacuum-pump rotation rate (RPM), motor current (A), oil temperature (°C) polled ≥ 0.1 Hz; predictive-maintenance alerts on degradation patterns. |
| FS-VAC-02 | URS-VAC-02 | Scheduled vacuum-leak-test cycle (recipe-defined, monthly minimum); acceptance per cabinet leak-rate spec; failure flips lyophilizer state to OUT_OF_SERVICE. |
| FS-VAC-03 | URS-VAC-03 | Condenser-coil-T monitored ≥ 1 Hz; failure to maintain ≤ recipe target during primary drying raises critical alarm. |
| FS-VAC-04 | URS-VAC-04 | Condenser-ice-load estimate computed (mass-balance from sublimation rate × elapsed time); > capacity_threshold raises warning. |

### 4.7 Container Closure Integrity Handshake (M-CCI)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CCI-01 | URS-CCI-01 | At cycle end, CCI-handshake payload (batch_id, stoppering_atmosphere, headspace_summary, vial_count, fill_line_ref) sent to AIM 5000 station via REST mTLS; payload signed; verified `OQ-CCI-HANDSHAKE-01`. |
| FS-CCI-02 | URS-CCI-02 | PAS-X batch-release-step gate state queries CCI station result via callback; pass-rate < USP <1207> acceptance threshold blocks release; verified `OQ-CCI-EBR-GATE-01`. |
| FS-CCI-03 | URS-CCI-03 | Headspace-pressure-summary aggregator computes per-batch min / mean / max / σ; trended in QA dashboard. |

### 4.8 Audit Trail (M-AUD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit trail captures recipe events, cycle events, alarm acknowledgements, signature events, PAT-decision events; PTP-derived timestamps. |
| FS-AUD-02 | URS-AUD-02 | DB-level append-only on the audit table; revoked DELETE / UPDATE on the audit schema; DBA dual control. |
| FS-AUD-03 | URS-AUD-03 | Quality Reviewer audit-trail review per batch; QA Compliance quarterly platform review; both filed in QA dossier. |
| FS-AUD-04 | URS-AUD-04 | Cycle data + audit trail retention ≥ 25 years from product expiry; archived to immutable storage. |

### 4.9 Part 11 / Annex 11 / Annex 1 (M-PART11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Signature events render printed name + date / time + meaning into audit trail and into batch-report PDFs. |
| FS-PART11-02 | URS-PART11-02 | User-id uniqueness enforced via AD; deactivated user-ids never reassigned. |
| FS-PART11-03 | URS-PART11-03 | Signatures cryptographically bound to the signed record (PKI-signed payload). |
| FS-PART11-04 | URS-PART11-04 | SoD enforced: Operator ≠ Verifier on the same critical step; Recipe Author ≠ Approver on the same recipe. |
| FS-PART11-05 | URS-PART11-05 | Re-authentication required at every signature event; cached creds disabled. |
| FS-PART11-06 | URS-PART11-06 | AD password policy per `SEC-AD-POLICY-001` (min 14 chars, 90-day expiry, lockout). |
| FS-PART11-07 | URS-PART11-07 | Audit coverage per § 11.10(e); accurate-copy export per § 11.10(b); retention archive per § 11.10(c). |
| FS-AN1-01 | URS-AN1-01 | Lyo referenced in `VEL-CCS-PLANT1-001` § 7.4 as critical sterile-processing step; loading gated on cleanroom pressurisation. |
| FS-AN1-02 | URS-AN1-02 | Manual setpoint changes during the freeze step require dual signature; verified by `OQ-FREEZE-OVERRIDE-DUAL-SIG-01`. |
| FS-AN1-03 | URS-AN1-03 | Stoppering-atmosphere + stoppering-pressure qualification reference enforced at cycle-load; missing / expired reference blocks cycle; verified `OQ-STOPPER-QUAL-GATE-01`. |

### 4.10 Integrations (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-PASX-01 | URS-INT-PASX-01 | Recipe download via REST over mTLS; payload includes version + SHA-256; LDT validates checksum + version before load. |
| FS-INT-PASX-02 | URS-INT-PASX-02 | Executed-batch report (cycle profile + alarm log + PAT decisions + signatures) pushed to PAS-X within 30 minutes of cycle end; retry policy with exponential backoff. |
| FS-INT-PASX-03 | URS-INT-PASX-03 | PAS-X batch-release-step gate cleared only after Quality Reviewer approval + CCI station pass-result received. |
| FS-INT-BMS-01 | URS-INT-BMS-01 | Room-pressure interlock signal consumed via OPC UA from BMS; loss of pressurisation aborts loading and signals operator. |
| FS-INT-AD-01 | URS-INT-AD-01 | AD-managed accounts; service accounts use credential vault; no local Operator / QC accounts. |
| FS-INT-CCI-01 | URS-INT-CCI-01 | REST mTLS connection to AIM 5000; transmission retry with exponential backoff; persistent failure blocks batch closure + raises deviation. |
| FS-INT-NTP-01 | URS-INT-NTP-01 | PLC + workstations sync to site PTP master (IEEE 1588); LDT clock-skew check; > 1 s flips cycle-quality flag. |

### 4.11 Data Integrity (M-DI)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | All record writes attributed to AD-authenticated user-id. |
| FS-DI-02 | URS-DI-02 | Batch-report export as structured PDF (with audit trail) and CSV. |
| FS-DI-03 | URS-DI-03 | PTP synchronisation; clock-skew check at every signature event; > 5 s rejects signature. |
| FS-DI-04 | URS-DI-04 | Original captured data immutable; derivations stored in separate table referencing originals. |
| FS-DI-05 | URS-DI-05 | Pirani-vs-CM ratio, sublimation-rate decay, mass-flow on vacuum break computed deterministically; verified per `OQ-CALC-01`. |
| FS-DI-06 | URS-DI-06 | 25-y retention; ≤ 4 h retrieval via inspection-readiness runbook. |

### 4.12 Backup / Performance / Security (M-PERF / M-SEC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BAK-01 | URS-BAK-01 | Historian backed up nightly + continuous WAL; PITR available within 30 days; archive retention 25 y. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore test, witnessed; results filed `RUN-BAK-RESTORE-NNN`. |
| FS-BAK-03 | URS-BAK-03 | LDT failover RTO ≤ 4 h (in practice ≤ 30 s per FS-PLAT-01); RPO ≤ 1 min via real-time replication. |
| FS-PERF-01 | URS-PERF-01 | Sustained ≥ 1 Hz logging across all critical channels for ≥ 96-hour cycle; verified `PQ-PERF-DATA-LOG-01`. |
| FS-PERF-02 | URS-PERF-02 | HMI alarm-acknowledgement latency ≤ 1 s. |
| FS-SEC-01 | URS-SEC-01 | AD-managed accounts; break-glass admin only; quarterly access review. |
| FS-SEC-02 | URS-SEC-02 | Removable media blocked at GPO level except vendor-approved engineering use under CR. |
| FS-SEC-03 | URS-SEC-03 | Monthly vulnerability scans (Tenable); criticals to remediation in 30 days. |

### 4.13a Alarm Management and History (M-ALM)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ALM-01 | URS-ALM-01 | Alarm-class enum per ANSI/ISA-18.2 (info / warning / critical); class drives UI styling + ack-requirement + escalation. |
| FS-ALM-02 | URS-ALM-02 | Alarm-history table indexed on (lyo_id, alarm_class, raised_at); query API returns 12-month window ≤ 30 s. |
| FS-ALM-03 | URS-ALM-03 | Alarm-flood detector counts critical alarms in rolling 60 s; > 10 triggers engineering-review event + audit entry. |
| FS-ALM-04 | URS-ALM-04 | Per-cycle alarm-summary aggregator renders count by class + top-5 by recurrence into batch report. |
| FS-ALM-05 | URS-ALM-05 | Alarm-shelving endpoint accepts only recipe-defined non-critical alarms; auto-expires within 1 h; logged. |

### 4.13b Isolator / Cleanroom Interface (M-ISO)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ISO-01 | URS-ISO-01 | Isolator-ready interlock consumed via OPC UA; loading API blocked when state ≠ READY. |
| FS-ISO-02 | URS-ISO-02 | EMS critical-event webhook flips loading-state to BLOCKED + raises alarm. |
| FS-ISO-03 | URS-ISO-03 | Loading + stoppering-bridge transitions logged for CCS aggregation. |

### 4.13c Cleaning + CIP (M-CIP)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CIP-01 | URS-CIP-01 | Cleaning-cycle-record schema; operator + verifier signatures captured. |
| FS-CIP-02 | URS-CIP-02 | Dirty-hold + clean-hold gates per recipe; expiry blocks next-batch dispatch. |
| FS-CIP-03 | URS-CIP-03 | Manual-cleaning-entry UI with witness-signature capture. |

### 4.14 Training / Periodic Review (M-TRN / M-PR)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Production access gated by completed role-specific LMS training. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher training including alarm-acknowledgement scenario practice. |
| FS-TRN-03 | URS-TRN-03 | PAT-decision-logic competency assessment for Lyophilization Engineer + PAT Scientist. |
| FS-PR-01 | URS-PR-01 | Annual periodic-review run-book covering configuration, recipe inventory, audit-trail review evidence, deviation summary, alarm trends, PAT-decision summary, shelf-mapping currency, leak-test history, backup-restore evidence, training currency. |

---


### 4.15 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem with local OT cached credentials for offline operation. Conditional-access binding to policy `OT-Equipment Conditional Access (MFA at HMI session start; local cache validates last 24 h)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the cycle-history DB plus file-level capture of recipe and electronic batch records; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Interface Specifications

| IF ID | URS ID | Counterparty | Protocol | Direction | Notes |
|---|---|---|---|---|---|
| IF-PLC-01 | URS-CYC-* | S7-1500F PLC | OPC UA mTLS | bidirectional | tag values + alarms |
| IF-PAT-01 | URS-PAT-01..04 | Pirani / CM / TDLAS / RGA | OPC UA mTLS | inbound | PAT signals |
| IF-PASX-01 | URS-INT-PASX-01 | PAS-X v3.2 | REST mTLS | inbound | recipe download |
| IF-PASX-02 | URS-INT-PASX-02 | PAS-X v3.2 | REST mTLS | outbound | batch-report push |
| IF-PASX-03 | URS-INT-PASX-03 | PAS-X v3.2 | REST callback | outbound | downstream-gate clear |
| IF-BMS-01 | URS-INT-BMS-01 | Site BMS | OPC UA | inbound | pressurisation interlock |
| IF-CCI-01 | URS-INT-CCI-01 | AIM 5000 CCI | REST mTLS | bidirectional | handshake + result |
| IF-AD-01 | URS-INT-AD-01 / URS-SEC-01 | AD / PKI | LDAPS / Kerberos | bidirectional | AuthN + sig certs |
| IF-PTP-01 | URS-INT-NTP-01 | PTP master | IEEE 1588 | inbound | time sync |
| IF-EQMS-01 | URS-CYC-05 | MasterControl eQMS | REST | outbound | auto-deviation on override |

## 6. Data Model (high-level)

| Entity | Attributes (illustrative) |
|---|---|
| Recipe | recipe_id, version, state, freeze{}, primary_dry{}, secondary_dry{}, stoppering{}, end_point_criterion, sha256, signatures[] |
| ShelfMapping | mapping_id, lyo_id, qualified_until, mapping_data, signatures[] |
| Cycle | cycle_id, recipe_id, recipe_version, batch_id, started_at, ended_at, state, mapping_ref |
| ChannelLog | cycle_id, channel, ts, value, source_tag, quality_flag |
| PATSignal | cycle_id, instrument, ts, value, calibration_state |
| PATDecision | cycle_id, criterion_id, window, decision_value, threshold, decided_at, signature_id |
| Alarm | alarm_id, cycle_id, severity, raised_at, ack_by, ack_at, reason |
| Override | override_id, cycle_id, parameter, old, new, op_id, eng_id, reason, ts |
| CCIHandshake | handshake_id, cycle_id, payload_hash, station_response, pass_rate, ts |
| Signature | sig_id, record_id, signer_id, meaning, timestamp, payload_hash |
| AuditEvent | event_id, user_id, action, entity, old, new, timestamp |

## 7. Non-Functional Specifications

| NFR ID | Specification |
|---|---|
| NFR-01 | LDT failover ≤ 30 s automatic |
| NFR-02 | Sustained ≥ 1 Hz logging on all critical channels for ≥ 96-h cycle |
| NFR-03 | HMI alarm-ack latency ≤ 1 s |
| NFR-04 | Audit trail append-only |
| NFR-05 | Retention ≥ 25 y from product expiry |
| NFR-06 | RPO ≤ 1 min, RTO ≤ 4 h |
| NFR-07 | Process-control VLAN; no office-network route |
| NFR-08 | CM-loss watchdog ≤ 3 missed samples |
| NFR-09 | PAT-decision deterministic; reconstructable from logs |
| NFR-10 | PLC CPU switch-over ≤ 100 ms transparent to data plane |

## 8. Configuration Items (CI)

| CI ID | Item | Configured Value | Source |
|---|---|---|---|
| CI-01 | LDT failover target | ≤ 30 s | URS-PLAT-01 |
| CI-02 | UPS hold (LDT) | ≥ 30 min | URS-PLAT-02 |
| CI-03 | Historian retention online | ≥ 5 y | URS-PLAT-04 |
| CI-04 | PLC CPU redundancy | 1oo2 hot-standby | URS-PLAT-06 |
| CI-05 | Recipe states | DRAFT,REVIEW,APPROVED,EFFECTIVE,OBSOLETE | URS-REC-01 |
| CI-06 | Recipe-load checksum | SHA-256 | URS-REC-05, URS-INT-PASX-01 |
| CI-07 | Channel logging rate | ≥ 1 Hz | URS-CYC-03 |
| CI-08 | Critical-alarm types | chamber leak, condenser failure, vacuum loss, shelf-T OOE > 2 min, product-T > Tc' > 10 s | URS-CYC-02 |
| CI-09 | Dual-sig override | required during product cycle | URS-CYC-05, URS-AN1-02 |
| CI-10 | Time source | PTP master | URS-INT-NTP-01 |
| CI-11 | Pirani-vs-CM ratio target | recipe-defined band (typ 0.95-1.05) | URS-PAT-02 |
| CI-12 | TDLAS threshold | recipe-defined | URS-PAT-03 |
| CI-13 | CM-loss watchdog | 3 missed samples | URS-PAT-06 |
| CI-14 | Shelf-spread acceptance | ± 1.5 °C steady-state | URS-SHELF-01 |
| CI-15 | Leak-test cadence | monthly minimum | URS-VAC-02 |
| CI-16 | Condenser target T | recipe-defined (typ ≤ −60 °C) | URS-VAC-03 |
| CI-17 | CCI handshake payload | batch_id + atmosphere + headspace + count | URS-CCI-01 |
| CI-18 | Audit retention | ≥ 25 y from expiry | URS-AUD-04 |
| CI-19 | Backup window | nightly + WAL | URS-BAK-01 |
| CI-20 | Restore-test cadence | quarterly | URS-BAK-02 |
| CI-21 | Vuln-scan cadence | monthly | URS-SEC-03 |

## 9. Constraints / Assumptions / Risks

- **Constraints:** SP Industries patches under change control; PLC firmware changes (including SIL 2 partition) require revalidation per `EQ-LYO-001`.
- **Assumptions:** PAS-X, BMS, AD, PTP-master are validated infrastructure; PAT instruments qualified `EQ-LYO-PAT-001`; AIM 5000 CCI qualified `EQ-CCI-001`.
- **FS-level risks:** undetected probe failure (FS-CYC-02 + FS-CYC-08 + redundant TCs); recipe-version drift on load (FS-INT-PASX-01 + checksum); unauthorised override (FS-CYC-05 + dual sig); audit-trail tampering (FS-AUD-02 + DB controls); loss of pressure during loading (FS-INT-BMS-01); CM-loss masking pressure excursion (FS-PAT-01 redundant + FS-PAT-06 fallback); PAT-model drift (FS-PAT-07 cal-state gate); CCI station handshake failure (FS-INT-CCI-01 retry + deviation); stoppering-atmosphere qualification expiry (FS-AN1-03 gate).

## 10. References

- BBT-URS-LYO-001 v1.2 (parent URS).
- 21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; EU GMP Annex 1 (2022 revised).
- ICH Q9(R1); ISPE GAMP 5 (2nd ed., 2022); PIC/S PI 041; ISPE Baseline Guide *Sterile Product Manufacturing Facilities*.
- USP <1207>; USP <1208>; USP <790>.
- IEC 61511 SIL 2 (supplier-validated safety partition); ANSI/ISA-88.
- PDA TR68 — *Hardware and Process Validation of Lyophilization*.
- SP Industries — *LyoStar 4.5 / LyoControl 5 Configuration Reference*.
- Wilco / Bonfiglioli — *AIM 5000 CCI Integration Manual*.

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID(s) | Notes |
|---|---|---|
| URS-PLAT-01 | FS-PLAT-01 | |
| URS-PLAT-02 | FS-PLAT-02 | |
| URS-PLAT-03 | FS-PLAT-03 | |
| URS-PLAT-04 | FS-PLAT-04 | |
| URS-PLAT-05 | FS-PLAT-05 | |
| URS-PLAT-06 | FS-PLAT-06 | |
| URS-REC-01 | FS-REC-01 | |
| URS-REC-02 | FS-REC-02 | |
| URS-REC-03 | FS-REC-03 | |
| URS-REC-04 | FS-REC-04 | |
| URS-REC-05 | FS-REC-05 | |
| URS-REC-06 | FS-REC-06 | |
| URS-REC-07 | FS-REC-07 | |
| URS-REC-08 | FS-REC-08 | |
| URS-REC-09 | FS-REC-09 | |
| URS-REC-10 | FS-REC-10 | |
| URS-CYC-01 | FS-CYC-01 | |
| URS-CYC-02 | FS-CYC-02 | |
| URS-CYC-03 | FS-CYC-03 | |
| URS-CYC-04 | FS-CYC-04 | |
| URS-CYC-05 | FS-CYC-05 | |
| URS-CYC-06 | FS-CYC-06 | |
| URS-CYC-07 | FS-CYC-07 | |
| URS-CYC-08 | FS-CYC-08 | |
| URS-PAT-01 | FS-PAT-01 | |
| URS-PAT-02 | FS-PAT-02 | |
| URS-PAT-03 | FS-PAT-03 | |
| URS-PAT-04 | FS-PAT-04 | |
| URS-PAT-05 | FS-PAT-05 | |
| URS-PAT-06 | FS-PAT-06 | |
| URS-PAT-07 | FS-PAT-07 | |
| URS-SHELF-01 | FS-SHELF-01 | |
| URS-SHELF-02 | FS-SHELF-02 | |
| URS-SHELF-03 | FS-SHELF-03 | |
| URS-VAC-01 | FS-VAC-01 | |
| URS-VAC-02 | FS-VAC-02 | |
| URS-VAC-03 | FS-VAC-03 | |
| URS-VAC-04 | FS-VAC-04 | |
| URS-CCI-01 | FS-CCI-01 | |
| URS-CCI-02 | FS-CCI-02 | |
| URS-CCI-03 | FS-CCI-03 | |
| URS-AUD-01 | FS-AUD-01 | |
| URS-AUD-02 | FS-AUD-02 | |
| URS-AUD-03 | FS-AUD-03 | |
| URS-AUD-04 | FS-AUD-04 | |
| URS-PART11-01 | FS-PART11-01 | |
| URS-PART11-02 | FS-PART11-02 | |
| URS-PART11-03 | FS-PART11-03 | |
| URS-PART11-04 | FS-PART11-04 | |
| URS-PART11-05 | FS-PART11-05 | |
| URS-PART11-06 | FS-PART11-06 | |
| URS-PART11-07 | FS-PART11-07 | |
| URS-AN1-01 | FS-AN1-01 | |
| URS-AN1-02 | FS-AN1-02 | |
| URS-AN1-03 | FS-AN1-03 | |
| URS-INT-PASX-01 | FS-INT-PASX-01 / IF-PASX-01 | |
| URS-INT-PASX-02 | FS-INT-PASX-02 / IF-PASX-02 | |
| URS-INT-PASX-03 | FS-INT-PASX-03 / IF-PASX-03 | |
| URS-INT-BMS-01 | FS-INT-BMS-01 / IF-BMS-01 | |
| URS-INT-AD-01 | FS-INT-AD-01 / IF-AD-01 | |
| URS-INT-CCI-01 | FS-INT-CCI-01 / IF-CCI-01 | |
| URS-INT-NTP-01 | FS-INT-NTP-01 / IF-PTP-01 | |
| URS-DI-01 | FS-DI-01 | |
| URS-DI-02 | FS-DI-02 | |
| URS-DI-03 | FS-DI-03 | |
| URS-DI-04 | FS-DI-04 | |
| URS-DI-05 | FS-DI-05 | |
| URS-DI-06 | FS-DI-06 | |
| URS-BAK-01 | FS-BAK-01 | |
| URS-BAK-02 | FS-BAK-02 | |
| URS-BAK-03 | FS-BAK-03 | |
| URS-PERF-01 | FS-PERF-01 | |
| URS-PERF-02 | FS-PERF-02 | |
| URS-SEC-01 | FS-SEC-01 | |
| URS-SEC-02 | FS-SEC-02 | |
| URS-SEC-03 | FS-SEC-03 | |
| URS-ALM-01 | FS-ALM-01 | |
| URS-ALM-02 | FS-ALM-02 | |
| URS-ALM-03 | FS-ALM-03 | |
| URS-ALM-04 | FS-ALM-04 | |
| URS-ALM-05 | FS-ALM-05 | |
| URS-ISO-01 | FS-ISO-01 | |
| URS-ISO-02 | FS-ISO-02 | |
| URS-ISO-03 | FS-ISO-03 | |
| URS-CIP-01 | FS-CIP-01 | |
| URS-CIP-02 | FS-CIP-02 | |
| URS-CIP-03 | FS-CIP-03 | |
| URS-TRN-01 | FS-TRN-01 | |
| URS-TRN-02 | FS-TRN-02 | |
| URS-TRN-03 | FS-TRN-03 | |
| URS-PR-01 | FS-PR-01 | |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

The following risks are noted for downstream evaluation in the Risk Assessment.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Undetected probe failure causing miscontrolled product temperature → cake collapse or under-drying | Medium | High | URS-CYC-02, URS-CYC-03, URS-CYC-08 |
| R-02 | Recipe-version drift on load | Medium | High | URS-INT-PASX-01 + URS-REC-04 |
| R-03 | Unauthorized setpoint override | Low | High | URS-CYC-05 dual signature + auto-deviation |
| R-04 | Audit-trail tampering | Low | Critical | URS-AUD-02 + DBA dual control |
| R-05 | Loss of pressure during loading | Medium | High | URS-INT-BMS-01 + URS-AN1-01 |
| R-06 | Shelf-temperature gradient exceeding qualified envelope → batch-uniformity loss | Medium | High | URS-SHELF-01..03 |
| R-07 | Premature end-of-primary-drying call → residual moisture → stability fail | Medium | Critical | URS-PAT-02..06 + Lyo Engineer disposition |
| R-08 | CM failure during primary drying masking pressure excursion | Low | Critical | URS-PAT-01 redundant + URS-PAT-06 fallback |
| R-09 | Stoppering-pressure deviation → CCI fail in finished product | Medium | Critical | URS-REC-09 + URS-CCI-01..03 |
| R-10 | Vacuum-pump failure mid-cycle | Low | High | URS-VAC-01..02 + alarm |
| R-11 | Condenser overload causing chamber-pressure rise above Tc' window | Medium | High | URS-VAC-03..04 |
| R-12 | TDLAS / RGA model drift (line 1) | Low | Medium | URS-PAT-07 calibration linkage |
| R-13 | Loss of PTP causing audit-trail timestamp anomaly | Low | High | URS-INT-NTP-01 |
| R-14 | Multi-vial-array thermocouple bias undetected | Medium | High | URS-CYC-08 drift detection |
| R-15 | Sterile-air / N₂ supply purity defect at stoppering | Low | Critical | URS-AN1-03 + utility validation |

Full evaluation in `BBT-RA-LYO-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
