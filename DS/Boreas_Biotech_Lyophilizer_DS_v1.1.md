---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (Cat 4 / Tier T2)"
seed_corpus_basis:
  - "BBT-FS-LYO-001 v1.2 (parent FS)"
  - "BBT-URS-LYO-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd Edition) Category 4 — Configuration Specification conventions"
  - "21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; EU GMP Annex 1 (2022 revised)"
  - "ICH Q9(R1); USP <1207>; USP <1208>; USP <790>"
  - "IEC 61511 SIL 2 (supplier-validated safety partition); ANSI/ISA-88; ISA-18.2"
  - "PDA TR68; PIC/S PI 041"
parent_fs:
  document_number: BBT-FS-LYO-001
  version: "1.2"
  file: "../../../FS_FDS/_generated/final/Boreas_Biotech_Lyophilizer_FS_v1.3.md"
parent_urs:
  document_number: BBT-URS-LYO-001
  version: "1.2"
  file: "../../../URS/_generated/final/Lyophilizer_Computer_System__Boreas_Biotech_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Lyophilizer Computer System — SP Industries LyoStar 4.5 + LyoControl 5

**Document Number:** BBT-DS-LYO-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** BBT-FS-LYO-001 v1.2
**Parent URS:** BBT-URS-LYO-001 v1.2 *(informational, transitive)*
**Site:** Boreas Biotech AB, Sterile Manufacturing Plant 1, Strängnäs, Sweden *(fictional)*
**System Owner:** Lyophilization Engineer
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (SP Industries LyoStar 4.5 + LyoControl 5 + Siemens S7-1500F PLC; embedded SIL-2 safety partition supplier-validated)
**Project Mode:** Configuration project on commercial equipment-control software products **SP Industries LyoControl 5** + **Siemens S7-1500F + TP1500 HMI** (GAMP 5 Category 4). Embedded SIL-2 safety partition is supplier-validated under IEC 61511; treated as black box, only exposed interface validated.
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; EU GMP Annex 1 (2022 revised); ICH Q9(R1); PIC/S PI 041; USP <1207>; USP <1208>; USP <790>; IEC 61511 SIL 2 (supplier-validated); ANSI/ISA-88; ANSI/ISA-18.2.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect — Equipment Control) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Lyophilization Engineer) | _____________ | _____________ | _____ |
| Reviewer (PAT Scientist) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (IT / Automation) | _____________ | _____________ | _____ |
| Approver (System Owner — Lyophilization Engineer) | _____________ | _____________ | _____ |
| Approver (Head of Sterile Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Design Control

- **Document Number:** BBT-DS-LYO-001
- **Version:** 1.1
- **Effective Date:** 2026-05-15 *(synthetic)*
- **Parent FS:** BBT-FS-LYO-001 v1.2
- **Parent URS:** BBT-URS-LYO-001 v1.2 *(informational)*
- **Site:** Boreas Biotech AB, Plant 1, Strängnäs, Sweden
- **System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (LyoControl 5 + S7-1500F)
- **Project Mode:** Configuration only — no site Cat-5 code; SIL-2 partition vendor-validated
- **Regulatory Scope:** as above

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T2 from parent URS+FS pair. DS covers 78/78 FS-IDs from BBT-FS-LYO-001 v1.2. No FS-IDs flagged vendor-internal — LyoControl 5 configuration surface is site-designable; SIL-2 partition firmware vendor-validated, but the partition configuration interface (DI/DO segregation, redundancy mode, bypass-attempt OQ scenarios) is site-designed and covered here. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from BBT-FS-LYO-001 and BBT-URS-LYO-001. DS-specific terms:

| Term | Definition |
|---|---|
| LDT | Lyophilization Data Terminal — workstation hosting LyoControl 5 |
| TP1500 | Siemens HMI panel at the cabinet |
| Pirani-CM-ratio | Pirani gauge reading divided by Capacitance Manometer reading |
| TDLAS | Tunable Diode Laser Absorption Spectroscopy (line 1 only) |
| RGA | Residual-Gas Analysis (line 1 only) |
| CCI | Container Closure Integrity (Wilco/Bonfiglioli AIM 5000) |
| Tc' | Eutectic / collapse temperature (recipe-defined safety margin) |

---

## 1. Purpose

This DS specifies the technical design that satisfies the FS `BBT-FS-LYO-001` v1.2 for the Boreas Plant-1 lyophilizer. It records LyoControl 5 + S7-1500F + LDT pair CI inventory; recipe per-phase / cycle / PAT / shelf-mapping / vacuum / CCI / alarm / isolator / CIP workflow + business-rule design; role-permission matrix; per-interface integration design (PAS-X, BMS, Wilco AIM 5000 CCI, MasterControl, AD, PTP, PAT instruments). Controlling input to IQ / OQ / PQ / RTM `BBT-RTM-LYO-001`.

## 2. Scope

**In scope.** Configuration of LyoControl 5 active/standby LDT pair, S7-1500F redundant CPU pair (1oo2), TP1500 HMI, Coating Historian (InfluxDB backend), Grafana read-only trends, integrations (PAS-X v3.2, site BMS, AIM 5000 CCI, MasterControl eQMS, AD, PTP master, PAT instruments — Pirani / CM-pair / TDLAS / RGA), isolator / cleanroom interlocks, CIP cycle records, shelf-mapping registry.

**Out of scope.** Vendor-internal LyoControl 5 source code; Siemens S7-1500F firmware (including SIL-2 partition); physical cabinet / chamber / condenser / vacuum-pump hardware; PAT instrument firmware; Wilco AIM 5000 internal validation (separate URS/FS).

## 3. Architectural Overview

```
                ┌───────────────────────────────────────────────────┐
                │  AD (`boreas.local`) │ Site PKI │ PTP master         │
                └────────────────────┬──────────────────────────────┘
                                     │
   ┌─────────────────────────────────▼─────────────────────────────────┐
   │   Process-Control VLAN (no office-network route)                   │
   │   ┌───────────────────────────────────────────────────────────┐    │
   │   │  LyoControl 5 Active LDT ←─ replication ─→ Standby LDT       │
   │   │  (auto-failover ≤ 30 s)                                      │
   │   │  - Recipe UI │ Cycle UI │ PAT Decision Viewer                 │
   │   │  - Historian (InfluxDB) + Grafana (read-only)                 │
   │   └───────────────────────────────────────────────────────────┘    │
   │           │ OPC UA mTLS         │ REST mTLS                         │
   │           ▼                     ▼                                    │
   │   ┌─────────────────┐  ┌──────────────────┐  ┌─────────────────┐  │
   │   │ S7-1500F PLC    │  │ PAS-X v3.2       │  │ Wilco AIM 5000   │  │
   │   │ + TP1500 HMI    │  └──────────────────┘  │ CCI station      │  │
   │   │ + PAT instr.    │                        └─────────────────┘  │
   │   │ + Safety SIL 2  │  ┌──────────────────┐  ┌─────────────────┐  │
   │   │   (1oo2 CPU)    │  │ Site BMS         │  │ MasterControl    │  │
   │   └─────────────────┘  │ (room pressure)  │  │ eQMS (deviation) │  │
   │                        └──────────────────┘  └─────────────────┘  │
   └─────────────────────────────────────────────────────────────────────┘
```

Design: LDT pair on UPS ≥ 30 min; PLC + TP1500 on separate UPS branch; S7-1500F redundant CPU pair (1oo2) hot-standby with PROFINET-IRT sync, switch-over ≤ 100 ms; safety partition isolated by hardware DI/DO from supervisory; no bidirectional control coupling.

---

## 4. Configuration Specification

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-LYO-01 | LyoControl 5 > LDT Pair Replication | active / standby; PostgreSQL streaming; auto-failover ≤ 30 s | Custom | FS-PLAT-01 | FS-PLAT-01 | OQ `OQ-FAILOVER-01` |
| DS-LYO-02 | LDT UPS Hold | ≥ 30 min; PLC + TP1500 separate branch | Custom | FS-PLAT-02 | FS-PLAT-02 | OQ `OQ-UPS-HOLD-01` |
| DS-LYO-03 | Process-Control VLAN | no office-network route; network-config audit | Custom | FS-PLAT-03 | FS-PLAT-03 | IQ `BBT-IQ-NET-01` |
| DS-LYO-04 | Historian Retention | ≥ 5 y online + immutable cold storage | Custom | FS-PLAT-04 | FS-PLAT-04 | OQ `BBT-OQ-HIST-RET-01` |
| DS-LYO-05 | Safety Partition (S7-1500F) | dedicated runtime; supervisory I/O segregated by hardware DI/DO; no bidirectional control coupling | Custom | FS-PLAT-05 | FS-PLAT-05 | OQ `OQ-SAFETY-PARTITION-01` |
| DS-LYO-06 | Redundant CPU Pair (1oo2) | hot-standby; sync over PROFINET-IRT; switch-over ≤ 100 ms | Custom | FS-PLAT-06 | FS-PLAT-06 | OQ `OQ-CPU-REDUNDANCY-01` |
| DS-LYO-07 | Recipe State Machine | `DRAFT / REVIEW / APPROVED / EFFECTIVE / OBSOLETE` server-side enforced | Custom | FS-REC-01 | FS-REC-01 | OQ `BBT-OQ-REC-STATES-01` |
| DS-LYO-08 | Cycle-Load Endpoint | non-EFFECTIVE → `RECIPE_NOT_EFFECTIVE` | Custom | FS-REC-02 | FS-REC-02 | OQ `BBT-OQ-REC-EFF-01` |
| DS-LYO-09 | Transition E-Signature | re-auth; role-mapped permission | Custom | FS-REC-03 | FS-REC-03 | OQ `BBT-OQ-REC-ESIG-01` |
| DS-LYO-10 | EFFECTIVE Immutability | revision N+1 in DRAFT | Custom | FS-REC-04 | FS-REC-04 | OQ `BBT-OQ-REC-IMMUT-01` |
| DS-LYO-11 | Recipe Download SHA-256 + Version | validated against local approved-recipe registry; mismatch blocks | Custom | FS-REC-05 | FS-REC-05 | OQ `BBT-OQ-REC-CKSUM-01` |
| DS-LYO-12 | Freezing-Phase Block Validators | `start_T_C, end_T_C, ramp_rate_C_per_min, nucleation_method (passive/ControLyo/ice-fog), hold_time_min, vial_T_band_C` | Custom | FS-REC-06 | FS-REC-06 | OQ `OQ-REC-FREEZE-PARAMS-01` |
| DS-LYO-13 | Primary-Drying Block Validators | `shelf_T_set, chamber_P_mTorr_set, max_product_T (Tc' − margin), expected_duration_h, end_point_criterion (enum: time_based / pirani_cm_ratio / tdlas_rate)` | Custom | FS-REC-07 | FS-REC-07 | OQ `OQ-REC-PRIMDRY-PARAMS-01` |
| DS-LYO-14 | Secondary-Drying Block Validators | `ramp + hold, chamber_P_set, expected_duration_h, residual_moisture_target_pct` | Custom | FS-REC-08 | FS-REC-08 | OQ `OQ-REC-SECDRY-PARAMS-01` |
| DS-LYO-15 | Stoppering Block Validators | `hydraulic_pressure_set_bar, atmosphere (enum: N2/sterile_air/partial_vacuum), verification_required=true` | Custom | FS-REC-09 | FS-REC-09 | OQ `OQ-REC-STOPPER-PARAMS-01` |
| DS-LYO-16 | Recipe-Diff Renderer | per-phase block changes with old/new + change-reason | Custom | FS-REC-10 | FS-REC-10 | OQ `BBT-OQ-REC-DIFF-01` |
| DS-LYO-17 | Cycle Engine Setpoint-Envelope | per recipe step; deviations classified info / warning / critical | Custom | FS-CYC-01 | FS-CYC-01 | OQ `BBT-OQ-CYC-ENV-01` |
| DS-LYO-18 | Critical-Alarm Types | chamber leak, condenser failure, vacuum loss, shelf-T OOE > 2 min, product-T > Tc' > 10 s → ack + reason | Custom | FS-CYC-02 | FS-CYC-02 | OQ `BBT-OQ-CRIT-ALARM-01` |
| DS-LYO-19 | Channel Logging | ≥ 1 Hz: shelf T per zone, product T (TC array ≥ 6 vials), chamber P (redundant CM + Pirani), condenser T, vial-headspace P, comparative P | Custom | FS-CYC-03 | FS-CYC-03 | OQ `BBT-OQ-LOG-RATE-01` |
| DS-LYO-20 | PTP Timestamps + LDT Skew Check | > 1 s → cycle-quality flag | Custom | FS-CYC-04 | FS-CYC-04 | OQ `BBT-OQ-PTP-01` |
| DS-LYO-21 | Manual-Override Dual-Sign | Operator + Lyophilization Engineer; auto-deviation MasterControl | Custom | FS-CYC-05 | FS-CYC-05 | OQ `BBT-OQ-OVR-01` |
| DS-LYO-22 | Critical-Step Verification | loading-complete + stoppering-complete; verifier ≠ operator | Custom | FS-CYC-06 | FS-CYC-06 | OQ `BBT-OQ-CRIT-VER-01` |
| DS-LYO-23 | Cycle-Abort Sequence | vacuum break + shelves to safe T + condenser controlled discharge; audit-trail integrity preserved | Custom | FS-CYC-07 | FS-CYC-07 | OQ `BBT-OQ-ABORT-01` |
| DS-LYO-24 | Per-TC Drift Monitor | each probe vs median of remaining; drift > ± 1 °C → warning + probe-exclusion | Custom | FS-CYC-08 | FS-CYC-08 | OQ `OQ-TC-DRIFT-DETECT-01` |
| DS-LYO-25 | Pirani + CM Pair Inputs | ≥ 1 Hz OPC UA; both readings to ChannelLog; one-CM failure → redundancy alarm but continue | Custom | FS-PAT-01 | FS-PAT-01 | OQ `BBT-OQ-CM-OPCUA-01` |
| DS-LYO-26 | Pirani-vs-CM-Ratio Computation | `Pirani_mTorr / CM_mean_mTorr`; recipe-defined band typ `[0.95, 1.05]` ≥ `recipe_dwell_min` → end-of-primary-drying | Custom | FS-PAT-02 | FS-PAT-02 | OQ `OQ-PIRANI-CM-RATIO-01` |
| DS-LYO-27 | TDLAS Subscription (line 1) | 1 Hz sublimation-rate (g/h); rate < threshold ≥ dwell → alternative end-point | Custom | FS-PAT-03 | FS-PAT-03 | OQ `BBT-OQ-TDLAS-01` |
| DS-LYO-28 | RGA Subscription (line 1) | m/z 28 + m/z 32; trending for non-condensable-gas ingress; threshold alarm | Custom | FS-PAT-04 | FS-PAT-04 | OQ `BBT-OQ-RGA-01` |
| DS-LYO-29 | End-of-Primary-Drying Decision Log | `(criterion_id, input_window, decision_value, threshold, decision_timestamp, signature_event)`; reconstructable | Custom | FS-PAT-05 | FS-PAT-05 | OQ `OQ-PAT-DETERMINISTIC-01` |
| DS-LYO-30 | CM-Loss Watchdog | ≥ 3 missed samples from both CMs → critical alarm + time-based fallback; disposition gate "Lyo Engineer review required" | Custom | FS-PAT-06 | FS-PAT-06 | OQ `OQ-PAT-CM-LOSS-FALLBACK-01` |
| DS-LYO-31 | PAT Calibration-State Gate | OUT_OF_CAL disables PAT-based phase transition (forces time-based fallback) + engineering alarm | Custom | FS-PAT-07 | FS-PAT-07 | OQ `BBT-OQ-PAT-CAL-01` |
| DS-LYO-32 | OQ Shelf-Mapping Test | range −50 to +60 °C in 10 °C steps; ≥ 9 probe positions per shelf; acceptance ± 1.5 °C steady-state spread | Custom | FS-SHELF-01 | FS-SHELF-01 | OQ `OQ-SHELF-MAP-01` |
| DS-LYO-33 | Recipe-Load Shelf-Mapping Gate | expired / void mapping → block | Custom | FS-SHELF-02 | FS-SHELF-02 | OQ `OQ-SHELF-MAP-GATE-01` |
| DS-LYO-34 | Per-Cycle Shelf-Spread Metric | (max − min) during steady-state phases; > envelope → engineering review | Custom | FS-SHELF-03 | FS-SHELF-03 | OQ `BBT-OQ-SHELF-SPREAD-01` |
| DS-LYO-35 | Vacuum-Pump Telemetry | rotation rate + motor current + oil temperature ≥ 0.1 Hz; predictive-maintenance alerts | Custom | FS-VAC-01 | FS-VAC-01 | OQ `BBT-OQ-VAC-TEL-01` |
| DS-LYO-36 | Scheduled Vacuum-Leak-Test Cycle | recipe-defined, monthly minimum; failure → OUT_OF_SERVICE | Custom | FS-VAC-02 | FS-VAC-02 | OQ `BBT-OQ-LEAK-TEST-01` |
| DS-LYO-37 | Condenser-Coil-T Monitor | ≥ 1 Hz; failure to maintain ≤ recipe target → critical alarm | Custom | FS-VAC-03 | FS-VAC-03 | OQ `BBT-OQ-COND-T-01` |
| DS-LYO-38 | Condenser-Ice-Load Estimate | mass-balance from sublimation rate × elapsed time; > capacity → warning | Custom | FS-VAC-04 | FS-VAC-04 | OQ `BBT-OQ-COND-LOAD-01` |
| DS-LYO-39 | CCI Handshake Payload | `(batch_id, stoppering_atmosphere, headspace_summary, vial_count, fill_line_ref)` REST mTLS to AIM 5000; signed | Custom | FS-CCI-01 | FS-CCI-01 | OQ `OQ-CCI-HANDSHAKE-01` |
| DS-LYO-40 | PAS-X Release-Step Gate | queries CCI result via callback; pass-rate < USP <1207> threshold blocks release | Custom | FS-CCI-02 | FS-CCI-02 | OQ `OQ-CCI-EBR-GATE-01` |
| DS-LYO-41 | Headspace-Pressure-Summary Aggregator | per-batch min / mean / max / σ; QA dashboard | Custom | FS-CCI-03 | FS-CCI-03 | OQ `BBT-OQ-HEADSPACE-01` |
| DS-LYO-42 | Audit-Trail Coverage | recipe + cycle + alarm acks + signature + PAT-decision events; PTP timestamps | Custom | FS-AUD-01 | FS-AUD-01 | OQ `BBT-OQ-AUDIT-COV-01` |
| DS-LYO-43 | Audit Append-Only DB | revoked DELETE/UPDATE; DBA dual control | Custom | FS-AUD-02 | FS-AUD-02 | OQ `BBT-OQ-AUDIT-APPEND-01` |
| DS-LYO-44 | QR Audit Review per Batch + Quarterly Platform Review | filed in QA dossier | Custom | FS-AUD-03 | FS-AUD-03 | OQ `BBT-OQ-AUDIT-REV-01` |
| DS-LYO-45 | 25-Y Retention to Immutable Storage | S3 Object-Lock Compliance Mode | Custom | FS-AUD-04 | FS-AUD-04 | (governance) |
| DS-LYO-46 | Signature Render | printed name + ts + meaning into audit + PDFs | Custom | FS-PART11-01 | FS-PART11-01 | OQ `BBT-OQ-SIG-RENDER-01` |
| DS-LYO-47 | User-ID Uniqueness | deactivated never reassigned | Custom | FS-PART11-02 | FS-PART11-02 | OQ `BBT-OQ-USERID-01` |
| DS-LYO-48 | PKI-Signed Signature Payload | bound to signed record | Custom | FS-PART11-03 | FS-PART11-03 | OQ `BBT-OQ-SIG-PKI-01` |
| DS-LYO-49 | SoD Enforcement | Operator ≠ Verifier on same critical step; Recipe Author ≠ Approver on same recipe | Custom | FS-PART11-04 | FS-PART11-04 | OQ `BBT-OQ-SOD-01` |
| DS-LYO-50 | Re-Auth at Every Signature | cached creds disabled | Custom | FS-PART11-05 | FS-PART11-05 | OQ `BBT-OQ-REAUTH-01` |
| DS-LYO-51 | AD Password Policy | min 14 chars + 90-d expiry + lockout | Custom | FS-PART11-06 | FS-PART11-06 | (governance) |
| DS-LYO-52 | Audit Coverage + Export | per § 11.10(b)/(c)/(e) | Custom | FS-PART11-07 | FS-PART11-07 | OQ `BBT-OQ-PART11-COV-01` |
| DS-LYO-53 | Annex 1 — CCS Reference | `VEL-CCS-PLANT1-001` § 7.4; loading gated on cleanroom pressurisation | Custom | FS-AN1-01 | FS-AN1-01 | OQ `BBT-OQ-CCS-LINK-01` |
| DS-LYO-54 | Freeze-Step Dual-Sign on Manual Override | Op + Eng | Custom | FS-AN1-02 | FS-AN1-02 | OQ `OQ-FREEZE-OVERRIDE-DUAL-SIG-01` |
| DS-LYO-55 | Stoppering-Atmosphere + Pressure Qualification Reference | enforced at cycle-load; missing / expired → block | Custom | FS-AN1-03 | FS-AN1-03 | OQ `OQ-STOPPER-QUAL-GATE-01` |
| DS-LYO-56 | PAS-X Recipe Download | REST mTLS; SHA-256 + version validated | Custom | FS-INT-PASX-01 | FS-INT-PASX-01 | OQ `BBT-OQ-PASX-IN-01` |
| DS-LYO-57 | Cycle Report POST | within 30 min; exponential-backoff retry | Custom | FS-INT-PASX-02 | FS-INT-PASX-02 | OQ `BBT-OQ-PASX-OUT-01` |
| DS-LYO-58 | PAS-X Release-Step Gate | cleared on QA approval + CCI station pass | Custom | FS-INT-PASX-03 | FS-INT-PASX-03 | OQ `BBT-OQ-PASX-GATE-01` |
| DS-LYO-59 | BMS Room-Pressure OPC UA | loss aborts loading + operator alert | Custom | FS-INT-BMS-01 | FS-INT-BMS-01 | OQ `BBT-OQ-BMS-01` |
| DS-LYO-60 | AD Credential Vault | service accounts via HashiCorp Vault | Custom | FS-INT-AD-01 | FS-INT-AD-01 | OQ `BBT-OQ-AD-VAULT-01` |
| DS-LYO-61 | AIM 5000 CCI mTLS Connection | retry exponential; persistent failure blocks batch closure + raises deviation | Custom | FS-INT-CCI-01 | FS-INT-CCI-01 | OQ `BBT-OQ-CCI-MTLS-01` |
| DS-LYO-62 | PTP IEEE 1588 PLC + WS Sync | LDT clock-skew check; > 1 s → cycle-quality flag | Custom | FS-INT-NTP-01 | FS-INT-NTP-01 | OQ `BBT-OQ-PTP-AUDIT-01` |
| DS-LYO-63 | AD User-ID Attribution | all writes attributed | Custom | FS-DI-01 | FS-DI-01 | OQ `BBT-OQ-DI-ATTRIB-01` |
| DS-LYO-64 | Batch-Report Export PDF + CSV | OQ-validated | Custom | FS-DI-02 | FS-DI-02 | OQ `OQ-EXPORT-01` |
| DS-LYO-65 | PTP Skew Gate at Signature | > 5 s rejects | Custom | FS-DI-03 | FS-DI-03 | OQ `BBT-OQ-PTP-AUDIT-02` |
| DS-LYO-66 | Originals Immutable + Derivations Separate | derivations table referencing originals | Custom | FS-DI-04 | FS-DI-04 | OQ `BBT-OQ-DI-LIN-01` |
| DS-LYO-67 | Math Engine Deterministic | Pirani-vs-CM ratio + sublimation-rate decay + mass-flow on vacuum break | Custom | FS-DI-05 | FS-DI-05 | OQ `OQ-CALC-01` |
| DS-LYO-68 | 25-Y Retention + 4-h Retrieval | inspection runbook | Custom | FS-DI-06 | FS-DI-06 | OQ `BBT-OQ-RETR-01` |
| DS-LYO-69 | InfluxDB Backup | nightly + continuous WAL → S3 Object-Lock; PITR 30 d; archive 25 y | Custom | FS-BAK-01 | FS-BAK-01 | OQ `BBT-OQ-BAK-01` |
| DS-LYO-70 | Quarterly Restore Test | witnessed | Custom | FS-BAK-02 | FS-BAK-02 | PR-01 |
| DS-LYO-71 | LDT RTO ≤ 4 h | (practice ≤ 30 s per DS-LYO-01); RPO ≤ 1 min via real-time replication | Custom | FS-BAK-03 | FS-BAK-03 | OQ `BBT-OQ-DR-01` |
| DS-LYO-72 | Sustained ≥ 1 Hz Logging | ≥ 96-h cycle | Custom | FS-PERF-01 | FS-PERF-01 | PQ `PQ-PERF-DATA-LOG-01` |
| DS-LYO-73 | HMI Alarm-Ack Latency | ≤ 1 s | Custom | FS-PERF-02 | FS-PERF-02 | OQ `BBT-OQ-HMI-ACK-01` |
| DS-LYO-74 | AD-Managed Accounts | break-glass admin only; quarterly access review | Custom | FS-SEC-01 | FS-SEC-01 | OQ `BBT-OQ-SEC-ACC-01` |
| DS-LYO-75 | Removable-Media GPO | block-by-default; vendor-approved CR exception | Custom | FS-SEC-02 | FS-SEC-02 | OQ `BBT-OQ-USB-01` |
| DS-LYO-76 | Tenable Nessus Monthly Scan | criticals 30 d | Custom | FS-SEC-03 | FS-SEC-03 | (governance) |
| DS-LYO-77 | Alarm Class Enum (ISA-18.2) | info / warning / critical → UI styling + ack + escalation | Custom | FS-ALM-01 | FS-ALM-01 | OQ `BBT-OQ-ALARM-CLASS-01` |
| DS-LYO-78 | Alarm-History Table Index | `(lyo_id, alarm_class, raised_at)`; 12-mo query ≤ 30 s | Custom | FS-ALM-02 | FS-ALM-02 | OQ `BBT-OQ-ALARM-HIST-01` |
| DS-LYO-79 | Alarm-Flood Detector | > 10 critical in 60 s → engineering-review event | Custom | FS-ALM-03 | FS-ALM-03 | OQ `BBT-OQ-ALARM-FLOOD-01` |
| DS-LYO-80 | Per-Cycle Alarm-Summary Aggregator | count by class + top-5 recurring → batch report | Custom | FS-ALM-04 | FS-ALM-04 | OQ `BBT-OQ-ALARM-SUM-01` |
| DS-LYO-81 | Alarm-Shelving Endpoint | recipe-defined non-critical only; auto-expires 1 h; logged | Custom | FS-ALM-05 | FS-ALM-05 | OQ `BBT-OQ-ALARM-SHELVE-01` |
| DS-LYO-82 | Isolator-Ready Interlock | OPC UA; loading API blocked when state ≠ READY | Custom | FS-ISO-01 | FS-ISO-01 | OQ `BBT-OQ-ISO-01` |
| DS-LYO-83 | EMS Critical-Event Webhook | flips loading-state to BLOCKED + alarm | Custom | FS-ISO-02 | FS-ISO-02 | OQ `BBT-OQ-EMS-WH-01` |
| DS-LYO-84 | Loading + Stoppering-Bridge Transition Log | for CCS aggregation | Custom | FS-ISO-03 | FS-ISO-03 | OQ `BBT-OQ-ISO-LOG-01` |
| DS-LYO-85 | Cleaning-Cycle Record Schema | operator + verifier signatures captured | Custom | FS-CIP-01 | FS-CIP-01 | OQ `BBT-OQ-CIP-01` |
| DS-LYO-86 | Dirty-Hold + Clean-Hold Gates | per recipe; expiry blocks next-batch dispatch | Custom | FS-CIP-02 | FS-CIP-02 | OQ `BBT-OQ-CIP-GATE-01` |
| DS-LYO-87 | Manual-Cleaning-Entry UI | witness-signature capture | Custom | FS-CIP-03 | FS-CIP-03 | OQ `BBT-OQ-CIP-MAN-01` |
| DS-LYO-88 | LMS-Gated Production Access | role-specific training completion | Custom | FS-TRN-01 | FS-TRN-01 | (governance) |
| DS-LYO-89 | Annual Refresher | alarm-ack scenario practice | Custom | FS-TRN-02 | FS-TRN-02 | (governance) |
| DS-LYO-90 | PAT-Decision-Logic Competency Assessment | Lyo Engineer + PAT Scientist | Custom | FS-TRN-03 | FS-TRN-03 | (governance) |
| DS-LYO-91 | Periodic-Review Runbook | configuration + recipe inventory + audit-trail review + deviation summary + alarm trends + PAT-decision summary + shelf-mapping currency + leak-test history + backup-restore + training | Custom | FS-PR-01 | FS-PR-01 | PR-01 |
| DS-LYO-92 | AD Conditional Access `OT-Equipment Conditional Access` | MFA at HMI session start; 24-h local cache; SIEM → Splunk `gxp-authn`; CyberArk PAM break-glass | Custom | FS-XSYS-AD-01 | FS-XSYS-AD-01 | OQ `BBT-OQ-CONDACC-01` |
| DS-LYO-93 | Veeam Backup | App-aware MS SQL VSS for cycle-history DB + file-level recipe + EBR; tier T2; RPO ≤ 24 h; RTO ≤ 24 BH; S3 Compliance + LTO-9 monthly | Custom | FS-XSYS-BAK-01 | FS-XSYS-BAK-01 | OQ `BBT-OQ-VEEAM-01` |

---

## 5. Workflow + Business-Rule Design

### 5.1 Cycle-Execution Workflow

```
Cleanroom pressurisation OK (BMS) + Isolator READY (EMS) →
Recipe LOAD (EFFECTIVE only, checksum verified, shelf-mapping current, stoppering-qual ref valid) →
LOADING (critical-step verifier ≠ operator) →
FREEZING (validated freeze-block params; dual-sign override per Annex 1) →
PRIMARY DRYING (end-point: time / pirani-cm / TDLAS; CM-loss watchdog) →
SECONDARY DRYING (validated sec-dry params; moisture target) →
STOPPERING (critical-step verifier ≠ operator; atmosphere per recipe) →
Cycle abort sequence (if needed): vacuum break → shelves safe T → condenser discharge →
CCI HANDSHAKE (REST mTLS to AIM 5000; pass-rate gate) →
Cycle Report POST to PAS-X → QA Reviewer → PAS-X release-step gate
```

### 5.2 Recipe-Approval Workflow

| Transition | Required signatures |
|---|---|
| DRAFT → REVIEW | Author `authorship` |
| REVIEW → APPROVED | Lyophilization Engineer + PAT Scientist + CSV Reviewer `review` |
| APPROVED → EFFECTIVE | Head of Sterile Manufacturing + Head of QA `approval` |
| EFFECTIVE → OBSOLETE | Lyo Engineer `retirement` |

### 5.3 PAT End-of-Primary-Drying Decision

Recipe `end_point_criterion` enum:
- **`time_based`:** time elapsed ≥ expected_duration_h
- **`pirani_cm_ratio`:** ratio ∈ [0.95, 1.05] (recipe-defined) sustained ≥ `recipe_dwell_min`
- **`tdlas_rate`:** sublimation rate < recipe-defined threshold sustained ≥ `recipe_dwell_min`

CM-loss watchdog (DS-LYO-30): ≥ 3 missed samples from both CMs → critical alarm + force `time_based` fallback + disposition gate "Lyo Engineer review required".

PAT calibration-state gate (DS-LYO-31): OUT_OF_CAL forces `time_based` regardless of recipe.

### 5.4 Annex 1 Rules

- **Loading gated on cleanroom pressurisation** (BMS OPC UA, DS-LYO-59)
- **Freeze-step manual setpoint changes require dual signature** (DS-LYO-54)
- **Stoppering-atmosphere qualification reference enforced at cycle-load** (DS-LYO-55)

### 5.5 CCI Handshake Rules

At cycle end: signed payload to AIM 5000 (DS-LYO-39); PAS-X release-step gate queries CCI station via callback (DS-LYO-58); pass-rate < USP <1207> threshold blocks release.

### 5.6 Alarm-Handling Rules (ISA-18.2)

- **INFO:** UI-display only
- **WARNING:** ack required
- **CRITICAL:** reason ≥ 10; persists until ack; auto-deviation if unack > T_escalate
- **Shelving:** recipe-defined non-critical only; auto-expires 1 h (DS-LYO-81)
- **Flood:** > 10 critical / 60 s → engineering review (DS-LYO-79)

---

## 6. Role-Permission Matrix Design

| AD Group | View HMI | Ack WARN | Ack CRIT | Author recipe | Approve recipe | Sign override | Sign freeze override | Verify critical step | Audit export | Admin |
|---|---|---|---|---|---|---|---|---|---|---|
| `Lyo-Operator` | Y | Y | — | — | — | initiate | initiate | as verifier | — | — |
| `Lyo-Senior-Operator` | Y | Y | Y | — | — | countersign | — | as verifier | — | — |
| `Lyo-Engineer` | Y | Y | Y | review | — | countersign | countersign | — | — | — |
| `Lyo-Recipe-Author` | Y | — | — | Y | — | — | — | — | — | — |
| `Lyo-Recipe-Approver` | Y | — | — | review | approve | — | — | — | — | — |
| `Lyo-PAT-Scientist` | Y | — | — | review | — | — | — | — | — | — |
| `Lyo-Quality-Reviewer` | Y | — | — | — | — | — | — | — | Y | — |
| `Lyo-CSV-Reviewer` | Y (RO) | — | — | — | review (CSV) | — | — | — | Y | — |
| `Lyo-Auditor` | Y (RO) | — | — | — | — | — | — | — | Y | — |
| Break-glass DBA (vaulted) | — | — | — | — | — | — | — | — | — | DB |

FS-IDs traced: FS-INT-AD-01, FS-PART11-04 (SoD), FS-CYC-05 (override), FS-AN1-02 (freeze override), FS-CYC-06 (critical-step verifier ≠ operator).

---

## 7. Integration Design

### 7.1 IF-PASX-01..03 (Werum PAS-X v3.2)

- Recipe download (REST mTLS, SHA-256 + version)
- Cycle-report POST within 30 min (exponential backoff)
- Release-step gate callback (cleared on QA + CCI pass)
- FS-IDs: FS-INT-PASX-01..03

### 7.2 IF-PLC-01 (S7-1500F PLC + PAT)

- Protocol: OPC UA mTLS (tag values + alarms + PAT signals)
- FS-IDs: FS-CYC-*, FS-PAT-*

### 7.3 IF-PAT-01 (Pirani / CM / TDLAS / RGA)

- Protocol: OPC UA mTLS; ≥ 1 Hz for Pirani+CM; vendor-defined for TDLAS / RGA
- FS-IDs: FS-PAT-01..04

### 7.4 IF-BMS-01 (Site BMS)

- Protocol: OPC UA (room pressure)
- Behaviour: loss of pressure aborts loading + alerts operator
- FS-IDs: FS-INT-BMS-01

### 7.5 IF-CCI-01 (Wilco AIM 5000)

- Protocol: REST mTLS bidirectional (handshake + result)
- Behaviour: persistent failure blocks batch closure + deviation
- FS-IDs: FS-INT-CCI-01

### 7.6 IF-AD-01 / IF-PTP-01

- LDAPS / Kerberos + IEEE 1588
- FS-IDs: FS-INT-AD-01, FS-INT-NTP-01, FS-SEC-01

### 7.7 IF-EQMS-01 (MasterControl)

- REST outbound: auto-deviation on override
- FS-IDs: FS-CYC-05

### 7.8 Integration Risk Register

| Interface | Risk | Mitigation |
|---|---|---|
| IF-PASX | cert expiry | cert-manager 365-d + 30-d alert |
| IF-PAT | CM pair simultaneous failure | redundant pair + DS-LYO-30 watchdog + time-based fallback |
| IF-BMS | OPC UA outage during loading | loading API blocked when state ≠ READY |
| IF-CCI | AIM 5000 handshake failure | retry + persistent-failure deviation; batch held |
| IF-AD | outage | local OT-cached creds 24 h |

---

## 8. Site-Deployed Components

**None in scope.** Per FS § 9 Constraints: *"SP Industries patches under change control; PLC firmware changes (including SIL 2 partition) require revalidation per EQ-LYO-001."* No Cat-5 site code is delivered with this system; therefore § 8 mini-SDS is not required per § 2B.4 rule 6.

---

## 9. References

### US
- 21 CFR Part 11; 21 CFR Part 211
- FDA CSA (final, February 2026)
- USP <1207>; USP <1208>; USP <790>

### EU
- EU GMP Annex 11
- EU GMP Annex 1 (2022 revised)
- EU GMP Annex 15

### DACH
- AMWHV
- BSI IT-Grundschutz baseline

### International
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE Baseline Guide *Sterile Product Manufacturing Facilities*
- ICH Q9(R1)
- ANSI/ISA-88 Part 1 + Part 2; ANSI/ISA-18.2
- IEC 61511 SIL 2 (supplier-validated safety partition)
- IEC 61131-3
- PIC/S PI 041
- PDA TR68 — *Hardware and Process Validation of Lyophilization*
- ISO/IEC 27001:2022

### Vendor
- SP Industries — *LyoStar 4.5 / LyoControl 5 Configuration Reference*
- Siemens — *S7-1500F + TP1500 Manual*
- Wilco / Bonfiglioli — *AIM 5000 CCI Integration Manual*
- MKS / Inficon — *Capacitance Manometer Reference*
- Physical Sciences Inc. — *TDLAS Reference (line 1)*
- Stanford Research — *RGA Manual (line 1)*

### Site
- `BBT-URS-LYO-001` v1.2 (informational)
- `BBT-FS-LYO-001` v1.2 (parent)
- `VEL-CCS-PLANT1-001` (Contamination Control Strategy)
- `EQ-LYO-001` (equipment qualification)
- `EQ-LYO-PAT-001` (PAT instrument qualification)
- `EQ-CCI-001` (CCI station qualification)
- `BBT-PR-LYO-YYYYMMDD` (periodic-review template)

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-LYO-01 | FS-PLAT-01 |
| DS-LYO-02 | FS-PLAT-02 |
| DS-LYO-03 | FS-PLAT-03 |
| DS-LYO-04 | FS-PLAT-04 |
| DS-LYO-05 | FS-PLAT-05 |
| DS-LYO-06 | FS-PLAT-06 |
| DS-LYO-07 | FS-REC-01 |
| DS-LYO-08 | FS-REC-02 |
| DS-LYO-09 | FS-REC-03 |
| DS-LYO-10 | FS-REC-04 |
| DS-LYO-11 | FS-REC-05 |
| DS-LYO-12 | FS-REC-06 |
| DS-LYO-13 | FS-REC-07 |
| DS-LYO-14 | FS-REC-08 |
| DS-LYO-15 | FS-REC-09 |
| DS-LYO-16 | FS-REC-10 |
| DS-LYO-17 | FS-CYC-01 |
| DS-LYO-18 | FS-CYC-02 |
| DS-LYO-19 | FS-CYC-03 |
| DS-LYO-20 | FS-CYC-04 |
| DS-LYO-21 | FS-CYC-05 |
| DS-LYO-22 | FS-CYC-06 |
| DS-LYO-23 | FS-CYC-07 |
| DS-LYO-24 | FS-CYC-08 |
| DS-LYO-25 | FS-PAT-01 |
| DS-LYO-26 | FS-PAT-02 |
| DS-LYO-27 | FS-PAT-03 |
| DS-LYO-28 | FS-PAT-04 |
| DS-LYO-29 | FS-PAT-05 |
| DS-LYO-30 | FS-PAT-06 |
| DS-LYO-31 | FS-PAT-07 |
| DS-LYO-32 | FS-SHELF-01 |
| DS-LYO-33 | FS-SHELF-02 |
| DS-LYO-34 | FS-SHELF-03 |
| DS-LYO-35 | FS-VAC-01 |
| DS-LYO-36 | FS-VAC-02 |
| DS-LYO-37 | FS-VAC-03 |
| DS-LYO-38 | FS-VAC-04 |
| DS-LYO-39 | FS-CCI-01 |
| DS-LYO-40 | FS-CCI-02 |
| DS-LYO-41 | FS-CCI-03 |
| DS-LYO-42 | FS-AUD-01 |
| DS-LYO-43 | FS-AUD-02 |
| DS-LYO-44 | FS-AUD-03 |
| DS-LYO-45 | FS-AUD-04 |
| DS-LYO-46 | FS-PART11-01 |
| DS-LYO-47 | FS-PART11-02 |
| DS-LYO-48 | FS-PART11-03 |
| DS-LYO-49 | FS-PART11-04 |
| DS-LYO-50 | FS-PART11-05 |
| DS-LYO-51 | FS-PART11-06 |
| DS-LYO-52 | FS-PART11-07 |
| DS-LYO-53 | FS-AN1-01 |
| DS-LYO-54 | FS-AN1-02 |
| DS-LYO-55 | FS-AN1-03 |
| DS-LYO-56 | FS-INT-PASX-01 |
| DS-LYO-57 | FS-INT-PASX-02 |
| DS-LYO-58 | FS-INT-PASX-03 |
| DS-LYO-59 | FS-INT-BMS-01 |
| DS-LYO-60 | FS-INT-AD-01 |
| DS-LYO-61 | FS-INT-CCI-01 |
| DS-LYO-62 | FS-INT-NTP-01 |
| DS-LYO-63 | FS-DI-01 |
| DS-LYO-64 | FS-DI-02 |
| DS-LYO-65 | FS-DI-03 |
| DS-LYO-66 | FS-DI-04 |
| DS-LYO-67 | FS-DI-05 |
| DS-LYO-68 | FS-DI-06 |
| DS-LYO-69 | FS-BAK-01 |
| DS-LYO-70 | FS-BAK-02 |
| DS-LYO-71 | FS-BAK-03 |
| DS-LYO-72 | FS-PERF-01 |
| DS-LYO-73 | FS-PERF-02 |
| DS-LYO-74 | FS-SEC-01 |
| DS-LYO-75 | FS-SEC-02 |
| DS-LYO-76 | FS-SEC-03 |
| DS-LYO-77 | FS-ALM-01 |
| DS-LYO-78 | FS-ALM-02 |
| DS-LYO-79 | FS-ALM-03 |
| DS-LYO-80 | FS-ALM-04 |
| DS-LYO-81 | FS-ALM-05 |
| DS-LYO-82 | FS-ISO-01 |
| DS-LYO-83 | FS-ISO-02 |
| DS-LYO-84 | FS-ISO-03 |
| DS-LYO-85 | FS-CIP-01 |
| DS-LYO-86 | FS-CIP-02 |
| DS-LYO-87 | FS-CIP-03 |
| DS-LYO-88 | FS-TRN-01 |
| DS-LYO-89 | FS-TRN-02 |
| DS-LYO-90 | FS-TRN-03 |
| DS-LYO-91 | FS-PR-01 |
| DS-LYO-92 | FS-XSYS-AD-01 |
| DS-LYO-93 | FS-XSYS-BAK-01 |

---

## 11. Design-level Risk Register

Per § 2B.8. Formal RA in `BBT-RA-LYO-001` (synthetic).

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| DR-01 | Undetected probe failure → cake collapse / under-drying | Medium | High | DS-LYO-18 + DS-LYO-19 channel coverage + DS-LYO-24 TC drift detection |
| DR-02 | Recipe-version drift on load | Medium | High | DS-LYO-11 SHA-256 + version |
| DR-03 | Unauthorised setpoint override | Low | High | DS-LYO-21 dual-sign + auto-deviation |
| DR-04 | Audit-trail tampering | Low | Critical | DS-LYO-43 append-only + DBA dual control |
| DR-05 | Loss of pressure during loading | Medium | High | DS-LYO-59 BMS interlock + DS-LYO-53 Annex 1 CCS link |
| DR-06 | Shelf-temperature gradient > qualified envelope → batch-uniformity loss | Medium | High | DS-LYO-32/33/34 shelf-mapping gate + per-cycle spread metric |
| DR-07 | Premature end-of-primary-drying → residual moisture → stability fail | Medium | Critical | DS-LYO-26..30 PAT decision + Lyo Engineer disposition |
| DR-08 | CM failure during primary drying masking pressure excursion | Low | Critical | DS-LYO-25 redundant + DS-LYO-30 fallback |
| DR-09 | Stoppering-pressure deviation → CCI fail in finished product | Medium | Critical | DS-LYO-15 + DS-LYO-39..41 CCI handshake |
| DR-10 | Vacuum-pump failure mid-cycle | Low | High | DS-LYO-35 telemetry + alarm |
| DR-11 | Condenser overload → chamber-pressure rise above Tc' window | Medium | High | DS-LYO-37 + DS-LYO-38 |
| DR-12 | TDLAS / RGA model drift (line 1) | Low | Medium | DS-LYO-31 calibration linkage |
| DR-13 | Loss of PTP → audit-trail timestamp anomaly | Low | High | DS-LYO-62 + DS-LYO-65 |
| DR-14 | Multi-vial-array TC bias undetected | Medium | High | DS-LYO-24 drift detection + probe-exclusion logic |
| DR-15 | Sterile-air / N₂ supply purity defect at stoppering | Low | Critical | DS-LYO-55 + utility validation |
| DR-16 | Pirani-vs-CM ratio band (DS-LYO-26) miscalibrated for product class | Low | High | Recipe-pinned band; OQ validation per product |
| DR-17 | S7-1500F CPU pair (DS-LYO-06) switchover causes brief data-plane gap | Low | Medium | OQ verifies ≤ 100 ms; data plane buffers blip |
| DR-18 | Safety partition (DS-LYO-05) bypass attempt via supervisory I/O misconfig | Low | Critical | Hardware DI/DO segregation + OQ bypass-attempt scenarios |
| DR-19 | Veeam VSS backup contention with high-rate PAT writes during 96-h cycle | Low | Medium | Backup outside high-rate windows |
| DR-20 | AD Conditional Access (DS-LYO-92) blocks emergency Lyo Engineer access | Low | High | Named-location exception + CyberArk break-glass |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
