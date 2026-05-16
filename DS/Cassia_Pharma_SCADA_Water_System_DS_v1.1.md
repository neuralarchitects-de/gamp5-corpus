---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (Cat 4 / Tier T3)"
seed_corpus_basis:
  - "CAS-FS-WATER-SCADA-001 v1.2 (parent FS)"
  - "CAS-URS-WATER-SCADA-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd Edition) Category 4 — Configuration Specification conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11; Annex 1 (2022 revision); Annex 3; Annex 15"
  - "USP <1231>, <645>, <643>, <85>, <86>"
  - "ASME BPE; ISA-88; ISA-95; ISA-101; ISA-18.2"
  - "PIC/S PI 041"
parent_fs:
  document_number: CAS-FS-WATER-SCADA-001
  version: "1.2"
  file: "../../../FS_FDS/_generated/final/Cassia_Pharma_SCADA_Water_System_FS_v1.3.md"
parent_urs:
  document_number: CAS-URS-WATER-SCADA-001
  version: "1.2"
  file: "../../../URS/_generated/final/SCADA_Water_System__Cassia_Pharma_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## SCADA — Pharmaceutical Water System (Ignition 8.3 + custom Python scripts)

**Document Number:** CAS-DS-WATER-SCADA-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** CAS-FS-WATER-SCADA-001 v1.2
**Parent URS:** CAS-URS-WATER-SCADA-001 v1.2 *(informational, transitive)*
**Site:** Cassia Pharma SpA, Sterile Manufacturing Plant 2, Sesto Fiorentino, Italy *(fictional)*
**System Owner:** Utilities Automation Lead
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (Ignition 8.3 platform), with site-authored Python control module `cassia_water_control` assessed as Category 5 sub-component (mini-SDS in § 8)
**Project Mode:** Configuration project on commercial software product **Inductive Automation Ignition 8.3** (GAMP 5 Category 4) with embedded site-authored Cat-5 Python module under hybrid configuration/development governance.
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11; Annex 1 (2022 revision); Annex 3; Annex 15; USP <1231>, <645>, <643>, <85>, <86>; ISPE Baseline Guide *Water and Steam Systems*; ASME BPE; ISA-88; ISA-101; ISA-18.2; PIC/S PI 041.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect — SCADA) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer — Automation) | _____________ | _____________ | _____ |
| Reviewer (Utilities Automation Lead) | _____________ | _____________ | _____ |
| Reviewer (Microbiology / Water Quality Lead) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Security Architect — OT) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — Sterile) | _____________ | _____________ | _____ |
| Approver (System Owner — Utilities Automation Lead) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Design Control

- **Document Number:** CAS-DS-WATER-SCADA-001
- **Version:** 1.1
- **Effective Date:** 2026-05-15 *(synthetic)*
- **Parent FS:** CAS-FS-WATER-SCADA-001 v1.2
- **Parent URS:** CAS-URS-WATER-SCADA-001 v1.2 *(informational)*
- **Site:** Cassia Pharma SpA, Plant 2, Sesto Fiorentino, Italy
- **System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (Ignition 8.3) with embedded Cat 5 site Python module
- **Project Mode:** Hybrid Cat 4 + Cat 5; § 4–§ 7 follow CS rules (§ 2B.4); § 8 follows SDS rules (§ 2B.5) for the site Python control module only
- **Regulatory Scope:** as above

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T3 from parent URS+FS pair. DS covers 84/84 FS-IDs from CAS-FS-WATER-SCADA-001 v1.2; no FS-IDs flagged vendor-internal (Ignition 8.3 configuration surface and site-authored Cat-5 module both have site design surface). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from CAS-FS-WATER-SCADA-001 and CAS-URS-WATER-SCADA-001. DS-specific terms:

| Term | Definition |
|---|---|
| CI | Configuration Item — one configurable parameter on Ignition / Python module / interface |
| UDT | Ignition User-Defined Type — Gateway template binding |
| Tag Provider | Ignition runtime data-source name |
| Project | Ignition logical container of resources (Perspective views, scripts, named queries) |
| Gateway Event Script | Server-side Python event hook (startup, shutdown, tag-change, scheduled) |
| SDS | Software Design Specification (§ 8 mini-SDS for the Cat-5 site module) |
| LoopModel YAML | Configuration document binding tag→branch→drop→dead-leg→point-of-use, traceable to ASME BPE drawing IDs |

---

## 1. Purpose

This DS specifies the technical design that satisfies the Functional Specification `CAS-FS-WATER-SCADA-001` v1.2. It is the third document in the V-model (URS → FS → DS) for the Cassia Pharma Water-System SCADA. The DS records the concrete configuration values, workflow/business-rule design, role-permission matrix design, integration design, and the mini-SDS for the site-authored Python control module. It is the controlling input to the IQ (Configuration IQ), OQ (Functional / Integration Test), PQ (User Acceptance / Performance Qualification), and the Requirements Traceability Matrix `CAS-RTM-WATER-SCADA-001`.

## 2. Scope

**In scope.** Configuration of the Ignition 8.3 Gateway cluster (gw1-gw4), Vision / Perspective projects, Tag Provider, UDTs, Gateway Event Scripts, Tag Historian + InfluxDB 2.7 LTS retention policies, PostgreSQL 16 (patroni cluster) for Ignition internal DB, alarm pipeline (ISA-18.2-aligned), e-signature workflow design, integrations (PAS-X MES, MasterControl eQMS, Sievers M9 TOC, Mettler-Toledo M800 conductivity, Charles River Endosafe nexgen-PTS, Pyxis EMS, Watson LIMS, AD/Kerberos), and the mini-SDS for `cassia_water_control` (site Python module).

**Out of scope.** Vendor-internal Ignition Gateway source code (Inductive Automation SDLC); physical water-system equipment (RO / EDI / WFI distillation / storage / distribution piping); upstream/downstream packaging; downstream IQ/OQ/PQ protocols (referenced only).

This scope mirrors FS § 2 and adds DS-specific boundary statements: (a) vendor internals of Ignition, M800, M9, Endosafe firmware are not redrawn; (b) site Python module receives Cat-5 SDS treatment in § 8.

## 3. Architectural Overview

The system implements the FS § 3 logical architecture with concrete design choices recorded below.

### 3.1 Topology

```
                  ┌─────────────────────────────────────────────────┐
                  │  Active Directory (cassia.local) + Site PKI       │
                  │  + Meinberg PTP/NTP master (ptp.cassia.local)     │
                  └────────────────────┬────────────────────────────┘
                                       │ LDAPS / Kerberos / IEEE-1588
                                       ▼
              ┌────────────────────────────────────────────────────────┐
              │   Ignition Gateway Cluster (Process-Control VLAN 312)   │
              │   ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌────────┐ │
              │   │ gw1 ACT  │  │ gw2 ACT  │  │ gw3 ACT  │  │ gw4 SB │ │
              │   │ RHEL 9.2 │  │ RHEL 9.2 │  │ RHEL 9.2 │  │ RHEL 9.2│ │
              │   └────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬───┘ │
              │        └─────────────┴─────────────┴────────────┘     │
              │                  Gateway Network (cluster mode)        │
              │   ┌─────────────────────────────────────────────────┐  │
              │   │  Site Python Module: cassia_water_control v1.0   │  │
              │   │  (Cat 5) — see § 8                               │  │
              │   └─────────────────────────────────────────────────┘  │
              │   ┌────────────────────────┐ ┌──────────────────────┐  │
              │   │ Vision / Perspective    │ │ Tag Historian +      │  │
              │   │ Projects (HMI)          │ │ InfluxDB 2.7 LTS     │  │
              │   └────────────────────────┘ └──────────────────────┘  │
              │   ┌─────────────────────────────────────────────────┐  │
              │   │ PostgreSQL 16 (3-node patroni cluster)           │  │
              │   │  — Ignition internal DB + recipe_versions +      │  │
              │   │     audit_events + loop_model + alarm_events     │  │
              │   └─────────────────────────────────────────────────┘  │
              └─────┬───────────┬─────────┬─────────┬───────────┬─────┘
                    │           │         │         │           │
                    ▼           ▼         ▼         ▼           ▼
            ControlLogix    Sievers     M-T M800   Endosafe   PAS-X v3.2
            5580 PLC        M9 TOC      Cond.      nexgen-PTS MES
            (OPC UA mTLS    (OPC UA     (OPC UA    (REST mTLS (REST mTLS)
             — water field   mTLS)       mTLS)      payload-
             instruments)                           signed)
                                                                 │
                    ┌───────────┬────────────┬─────────┐         │
                    ▼           ▼            ▼         ▼         ▼
                MasterControl  Watson      Pyxis    Operator   AD LDAPS
                eQMS (REST)    LIMS        EMS       HMI /     / Kerberos
                                (REST)     (REST)    iPad MDM
```

### 3.2 Cluster Design Choices (text)

- **Cluster mode:** Ignition Gateway Network in Cluster mode; gw1/2/3 ACT + gw4 SB; auto-failover budget ≤ 60 s (FS-PLAT-01).
- **Tag Provider:** redundant tag providers configured on each ACT gateway pointing at the same ControlLogix backplane via OPC UA mTLS.
- **PostgreSQL:** 3-node patroni cluster (pg-water-01..03) with synchronous-commit on the primary; auto-failover via etcd quorum.
- **InfluxDB:** single-writer (gw-active), buckets `water-online-5y` (retention 1825 d) + `water-archive-25y` (Object-Lock S3 cold-store).
- **PTP:** Meinberg Lantime M1000 grandmaster + Boundary clocks at the switch fabric; `ptp_skew_milliseconds` Prometheus exporter alerts > 1 s.
- **VLAN:** all gateways + PLC + analyzers on VLAN 312; office firewall denies routing in/out.

---

## 4. Configuration Specification

The table below records every Configuration Item (CI) of the Ignition 8.3 platform, the site Python module's runtime parameters, the InfluxDB / PostgreSQL persistence layer, and the AD / Vault wiring. Vendor-source-code internals are NOT redrawn — only configurable surfaces. Where a CI is a workflow rather than a single value, it is forwarded to § 5; where a CI is a role-permission cell, it is forwarded to § 6; integration CIs live in § 7; site-developed-code CIs (Cat 5 mini-SDS) live in § 8.

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-WATER-01 | Ignition > Gateway > Cluster Mode | `Cluster` (gw1/gw2/gw3 ACT + gw4 SB) | Custom | FS-PLAT-01 requires 3 active + 1 standby with auto-failover ≤ 60 s | FS-PLAT-01 | OQ `CAS-OQ-FAILOVER-01` |
| DS-WATER-02 | Ignition > Gateway > Failover Timeout (ms) | `30000` (30 s detection + 30 s promote) | Custom | Total failover ≤ 60 s budget per FS-PLAT-01 | FS-PLAT-01 | OQ `CAS-OQ-FAILOVER-01` |
| DS-WATER-03 | Ignition > Network > Listen Address (VLAN 312) | `10.31.2.0/24` interface only | Custom | FS-PLAT-02 process-control VLAN segregation | FS-PLAT-02 | IQ `CAS-IQ-NET-01` |
| DS-WATER-04 | OS-level firewall (firewalld) > zone `ot` | deny-by-default; allow-list `pasx.cassia.local:443`, `eqms.cassia.local:443`, `lims.cassia.local:443`, `m9.cassia.local:4840`, `m800.cassia.local:4840`, `pyxis.cassia.local:443`, `ad.cassia.local:636,88` | Custom | FS-PLAT-02 office-network firewall denial | FS-PLAT-02 | IQ `CAS-IQ-NET-02` |
| DS-WATER-05 | ControlLogix Output Hold Behaviour | `Safe-State` (CIP/SIP → "draining and venting"; interlocks → "all valves closed except vent") | Custom | FS-PLAT-03 power-loss safe-state requirements | FS-PLAT-03 | OQ `CAS-OQ-SAFE-STATE-01` |
| DS-WATER-06 | UPS Hold Time | ≥ 30 min (APC Symmetra LX 32 kVA, sized) | Custom | FS-PLAT-03 ≥ 30-min UPS hold | FS-PLAT-03 | IQ `CAS-IQ-UPS-01` |
| DS-WATER-07 | InfluxDB > Retention Policy `online-5y` | `1825d` (5 y) | Custom | FS-PLAT-04 5-y online retention | FS-PLAT-04 | OQ `CAS-OQ-INFLUX-RET-01` |
| DS-WATER-08 | InfluxDB > Retention Policy `archive-25y` | object-locked S3 cold-store (bucket `cas-water-archive-25y`, AWS S3 Compliance Mode, 25 y) | Custom | FS-PLAT-04 25-y archive on object-lock | FS-PLAT-04 | OQ `CAS-OQ-INFLUX-ARCH-01` |
| DS-WATER-09 | Meinberg PTP > Grandmaster Mode | enabled; stratum-1 GPS source `ptp.cassia.local` | Custom | FS-PLAT-05 PTP grandmaster + NTP fallback | FS-PLAT-05 | OQ `CAS-OQ-PTP-01` |
| DS-WATER-10 | Prometheus exporter `ptp_skew_milliseconds` > Alert Threshold | `> 1000` (ms) → `PTP_SKEW_DEGRADED` | Custom | FS-PLAT-05 PTP skew alarm > 1 s | FS-PLAT-05 | OQ `CAS-OQ-PTP-ALARM-01` |
| DS-WATER-11 | Postgres table `loop_model` | YAML serialised + version-pinned in GitLab `git.cassia.local/utilities/loop-model`; ASME BPE drawing ID FK | Custom | FS-LOOP-01 — LoopModel binding to ASME BPE drawing IDs | FS-LOOP-01 | OQ `CAS-OQ-LOOP-01` |
| DS-WATER-12 | Site Python rule `HotWfiTempMonitor.threshold_C` | `80.0` continuously; T_window = `300 s` | Custom | FS-LOOP-02 — sustained < 80 °C ≥ T_window alarm | FS-LOOP-02 | OQ `CAS-OQ-HOT-WFI-01` |
| DS-WATER-13 | Site Python `ColdLoopSanitisationGate` | binds `cold_loop_in_service` flag to `last_sanitisation_event.success`; expiry → false | Custom | FS-LOOP-03 — cold-WFI sanitisation regime gate | FS-LOOP-03 | OQ `CAS-OQ-COLD-WFI-01` |
| DS-WATER-14 | Site Python `DeadLegFlushScheduler.cron` | per-branch in `loop_model.yaml`: typical `0 */6 * * *` (every 6 h); branch-specific overrides allowed | Custom | FS-LOOP-04 — dead-leg flush per branch | FS-LOOP-04 | OQ `CAS-OQ-DEAD-LEG-01` |
| DS-WATER-15 | Site Python `LoopFlowCrosscheck.tolerance_pct` | `5.0`%; sustained-window = `120 s` | Custom | FS-LOOP-05 — flow vs return-flow > 5% sustained | FS-LOOP-05 | OQ `CAS-OQ-FLOW-XCHK-01` |
| DS-WATER-16 | Sievers M9 TOC Channel > OPC UA Endpoint | `opc.tcp://m9.cassia.local:4840` mTLS cert `cassia-water-scada-2026q2` | Custom | FS-MON-TOC-01 — OPC UA mTLS to Sievers M9 | FS-MON-TOC-01 | OQ `CAS-OQ-TOC-OPC-01` |
| DS-WATER-17 | TOC Action-Limit Engine > `water_quality_plan.yaml` schema | per-loop / per-point-of-use alert + action limits (ppb C) | Custom | FS-MON-TOC-02 — recipe-pinned TOC limits | FS-MON-TOC-02 | OQ `CAS-OQ-TOC-LIMITS-01` |
| DS-WATER-18 | Mettler-Toledo M800 Conductivity > OPC UA Endpoint | `opc.tcp://m800.cassia.local:4840` mTLS | Custom | FS-MON-TOC-03 / FS-MON-COND-01 — USP <645> Stage-1 conductivity ingest | FS-MON-TOC-03, FS-MON-COND-01 | OQ `CAS-OQ-COND-OPC-01` |
| DS-WATER-19 | Conductivity USP <645> Stage 1 Compensation Mode | `temperature-compensated value` (per M800 `cas:water:cond:loop1.tc_value`) | Default | FS-MON-TOC-03 USP <645> Stage 1 | FS-MON-TOC-03 | OQ `CAS-OQ-COND-USP645-01` |
| DS-WATER-20 | Postgres table `probe_inventory` schema | `(probe_id, serial, last_cal_date, next_cal_due, status enum {IN-SERVICE, OUT-OF-SERVICE, EXPIRED})`; expired-cal trigger sets status OUT-OF-SERVICE | Custom | FS-MON-COND-02 — probe calibration metadata | FS-MON-COND-02 | OQ `CAS-OQ-PROBE-CAL-01` |
| DS-WATER-21 | Site Python `SanitisationScheduler.recipe_source` | `recipe_versions` table where `status='EFFECTIVE'` only | Custom | FS-SAN-01 — execute per EFFECTIVE recipe | FS-SAN-01 | OQ `CAS-OQ-SAN-SCHED-01` |
| DS-WATER-22 | Sanitisation-Schedule Gate at Dependent-Op Start | runs at API call `op-precheck`; missed → returns `BLOCKED` | Custom | FS-SAN-02 / FS-CYC-05 — gate at dependent-op start | FS-SAN-02, FS-CYC-05 | OQ `CAS-OQ-SAN-GATE-01` |
| DS-WATER-23 | Ozone-Residual Interlock > release-threshold (ppm) | `≤ 0.05` ppm sustained ≥ `120 s` | Custom | FS-SAN-03 — loop reopens only when residual ≤ threshold | FS-SAN-03 | OQ `CAS-OQ-OZONE-01` |
| DS-WATER-24 | Grafana Dashboard `CAS-GR-SAN-EFFECTIVENESS` | configured panels: per-loop hot-water exposure heatmap, ozone-cycle residual trend, chemical-cycle pH trend, missed-sanitisation count | Custom | FS-SAN-04 — sanitisation-effectiveness trending | FS-SAN-04 | IQ `CAS-IQ-GR-01` |
| DS-WATER-25 | Sanitisation-Cycle CR Template | includes Microbiology Reviewer signature row (required) | Custom | FS-SAN-05 — Microbiology co-approval | FS-SAN-05 | OQ `CAS-OQ-SAN-CR-01` |
| DS-WATER-26 | Postgres table `recipe_versions` > status enum | `('DRAFT','REVIEW','APPROVED','EFFECTIVE','OBSOLETE')` | Custom | FS-REC-01 — recipe lifecycle states | FS-REC-01 | OQ `CAS-OQ-REC-STATES-01` |
| DS-WATER-27 | Stored procedure `recipe_transition_p` | enforces state transitions + signature-row insert + record-hash binding | Custom | FS-REC-01 / FS-REC-03 — transition enforcement | FS-REC-01, FS-REC-03 | OQ `CAS-OQ-REC-TRANS-01` |
| DS-WATER-28 | API endpoint `GET /api/recipes/effective` | filters `status='EFFECTIVE'`; others return HTTP 404 | Custom | FS-REC-02 — only EFFECTIVE returned to runtime | FS-REC-02 | OQ `CAS-OQ-REC-EFF-01` |
| DS-WATER-29 | API endpoint `POST /api/recipes/transition` | requires signed JWT payload `{recordId, recordHash, signerId, meaning, signatureBlock}`; verifies server-side | Custom | FS-REC-03 — e-signature on transition | FS-REC-03 | OQ `CAS-OQ-REC-ESIG-01` |
| DS-WATER-30 | DB trigger `recipe_versions_no_update_when_effective` | raises exception on UPDATE/DELETE when `status='EFFECTIVE'` | Custom | FS-REC-04 — immutability of EFFECTIVE recipes | FS-REC-04 | OQ `CAS-OQ-REC-IMMUT-01` |
| DS-WATER-31 | MES Recipe-Fetcher > SHA-256 + Version Validator | block-on-mismatch returns HTTP 409 | Custom | FS-REC-05 / FS-INT-MES-01 — checksum + version validation | FS-REC-05, FS-INT-MES-01 | OQ `CAS-OQ-REC-CKSUM-01` |
| DS-WATER-32 | Recipe Schema (JSON Schema) > required fields | `loop_coverage[]`, `exposure_time_s`, `target_temperature_c`, `chemistry`, `acceptance_criteria[]` | Custom | FS-REC-06 — recipe schema | FS-REC-06 | OQ `CAS-OQ-REC-SCHEMA-01` |
| DS-WATER-33 | Site Python `RecipeRunner.tick_ms` | `250` ms (deviation evaluation period) | Custom | FS-CYC-01 — 250 ms deviation tick | FS-CYC-01 | OQ `CAS-OQ-RUNNER-TICK-01` |
| DS-WATER-34 | Alarm Severity Table (ISA-18.2) | `alarm_table.yaml` enum: `INFO / WARNING / CRITICAL / SIS` with response, ack-requirement, escalation | Custom | FS-CYC-01 / FS-PART11-04 — ISA-18.2 classification | FS-CYC-01 | OQ `CAS-OQ-ALARM-TABLE-01` |
| DS-WATER-35 | Critical Alarm > `selfAcknowledgement` | `false` (operator ack required); reason min length `10` chars | Custom | FS-CYC-02 — critical-alarm ack policy | FS-CYC-02 | OQ `CAS-OQ-ALARM-ACK-01` |
| DS-WATER-36 | InfluxDB Write Rate (CPP tags) | `1 Hz`; PLC scan `100 ms` with first-order on-change deadband (deadband = 0.5% of range) | Custom | FS-CYC-03 — 1 Hz log rate | FS-CYC-03 | OQ `CAS-OQ-LOG-RATE-01` |
| DS-WATER-37 | Override Workflow > Required Signatures | Operator + Senior Operator dual-sign; reason ≥ 10 chars | Custom | FS-CYC-04 — override dual signatures | FS-CYC-04 | OQ `CAS-OQ-OVERRIDE-01` |
| DS-WATER-38 | Endosafe REST Endpoint | `POST /api/v1/endotoxin` with payload-signature verification (ECDSA-P256, vendor public key `endosafe-cassia-2026q2.pub`) | Custom | FS-ENDO-01 — Endosafe REST integration | FS-ENDO-01 | OQ `CAS-OQ-ENDO-IN-01` |
| DS-WATER-39 | Postgres table `endotoxin_linkage` schema | `(linkage_id, point_of_use, cycle_id, time_window_start, time_window_end, lims_result_id, in_line_result_id)` | Custom | FS-ENDO-02 — endotoxin linkage table | FS-ENDO-02 | OQ `CAS-OQ-ENDO-LINK-01` |
| DS-WATER-40 | `water_quality_plan.yaml` > Endotoxin Limits | per-loop + per-point-of-use alert + action (EU/mL); Microbiology Reviewer signature row required on CR | Custom | FS-ENDO-03 — Microbiology co-approval | FS-ENDO-03 | OQ `CAS-OQ-ENDO-LIMITS-01` |
| DS-WATER-41 | Site Python `TrendEngine.windows` | `[15min, 1h, 24h]` rolling | Custom | FS-TREND-01 — rolling trends | FS-TREND-01 | OQ `CAS-OQ-TREND-01` |
| DS-WATER-42 | Site Python `OolOosDetector.rules` | ASTM E2476 + Western Electric (3σ); thresholds via `spc_limits` table (recipe-pinned) | Custom | FS-TREND-02 — SPC rules | FS-TREND-02 | OQ `CAS-OQ-SPC-01` |
| DS-WATER-43 | Site Python `AnomalyDetector.model` | isolation-forest sklearn `contamination=0.01`, with heuristic ladder (slow-TOC-creep, intermittent-low-flow, post-san-rebound); model file `anomaly_v1.joblib` cosign-signed | Custom | FS-TREND-03 — anomaly detector | FS-TREND-03 | OQ `CAS-OQ-ANOMALY-01` |
| DS-WATER-44 | Periodic-Review Export Renderer | PDF/A-3 + CSV + JSON; PDF/A-3 via wkhtmltopdf + Ghostscript /PDF/A-3 mode | Custom | FS-TREND-04 — export formats | FS-TREND-04 | OQ `CAS-OQ-EXPORT-01` |
| DS-WATER-45 | Postgres table `audit_events` schema | `(event_id, actor_id NOT NULL, action, entity_type, entity_id, old_value JSONB, new_value JSONB, reason, timestamp_ptp, record_hash, signature_event_id NULLABLE)` | Custom | FS-AUD-01 / FS-DI-01 — ALCOA+ schema | FS-AUD-01, FS-DI-01 | OQ `CAS-OQ-AUDIT-SCHEMA-01` |
| DS-WATER-46 | Postgres role `app_role` permissions on `audit_events` | `INSERT, SELECT` only; `UPDATE, DELETE` denied; `DBA` access via break-glass with QA witness | Custom | FS-AUD-02 — append-only audit | FS-AUD-02 | OQ `CAS-OQ-AUDIT-RBAC-01` |
| DS-WATER-47 | Perspective View `Audit Trail Review` | filters: date / actor / action; export PDF/A-3 + JSONL | Custom | FS-AUD-03 — audit-review view | FS-AUD-03 | OQ `CAS-OQ-AUDIT-VIEW-01` |
| DS-WATER-48 | S3 Bucket `audit_events_archive` Object-Lock | Compliance Mode; retention 25 y; cross-region replication enabled | Custom | FS-AUD-04 — 25-y immutable archive | FS-AUD-04 | OQ `CAS-OQ-AUDIT-ARCH-01` |
| DS-WATER-49 | `/sop/` SharePoint Library — Annual Review Workflow | annual reminder + signed-attestation row | Custom | FS-PART11-01 — § 11.10(a) procedural controls | FS-PART11-01 | PR `CAS-PR-WATER-SCADA-YYYYMMDD` |
| DS-WATER-50 | AD Kerberos + MFA Policy | LDAPS + Kerberos `cassia.local`; Yubikey MFA at every sign-on | Custom | FS-PART11-02 — § 11.10(d) | FS-PART11-02 | OQ `CAS-OQ-AUTHN-01` |
| DS-WATER-51 | E-Signature API > Signature Payload Schema | `{printedName, dateTime_ptp, meaning enum('authorship','review','approval','release','retirement','verification')}` server-validated; SHA-256 of record bound to payload | Custom | FS-PART11-04 / FS-PART11-05 — § 11.50 + § 11.70 | FS-PART11-04, FS-PART11-05 | OQ `CAS-OQ-ESIG-01` |
| DS-WATER-52 | AD Signer Mapping > HR Feed Source | `hr.cassia.local/api/v1/personnel` daily sync; user-id reuse blocked at provisioning | Custom | FS-PART11-06 — § 11.100 user-id uniqueness | FS-PART11-06 | OQ `CAS-OQ-USERID-01` |
| DS-WATER-53 | Kerberos Ticket Max-Age (sign-off endpoint) | `5 min` (fresh-ticket only); cached tokens rejected | Custom | FS-PART11-07 — § 11.200 fresh ticket | FS-PART11-07 | OQ `CAS-OQ-KRB-FRESH-01` |
| DS-WATER-54 | AD Password Policy `SEC-AD-POLICY-001` | min 14 chars + complexity + 90-d rotation + MFA + lockout after 5 failed | Custom | FS-PART11-08 — § 11.300 | FS-PART11-08 | OQ `CAS-OQ-PASSWD-01` |
| DS-WATER-55 | Override Event > CCS Linkage Field | `ccs_doc_ref` (FK to MasterControl doc) — required at override save | Custom | FS-AN1-01 — Annex 1 CCS linkage | FS-AN1-01 | OQ `CAS-OQ-CCS-LINK-01` |
| DS-WATER-56 | DB Constraint `audit_events.actor_id NOT NULL` | enforced | Custom | FS-DI-01 — attribution NOT NULL | FS-DI-01 | OQ `CAS-OQ-AUDIT-ATTRIB-01` |
| DS-WATER-57 | Export Renderer Validation | PDF/A-3 (ISO 19005-3) + JSON / CSV; rendering OQ-validated | Custom | FS-DI-02 — export validation | FS-DI-02 | OQ `CAS-OQ-EXPORT-01` |
| DS-WATER-58 | Timestamp Source > PLC + PTP | PLC writes timestamp from PTP boundary clock; retroactive entries flagged with `retroactive_reason` | Custom | FS-DI-03 — PTP timestamps + retroactive flag | FS-DI-03 | OQ `CAS-OQ-PTP-AUDIT-01` |
| DS-WATER-59 | InfluxDB Tag-Write Mode | `point-write only`; corrections recorded as new annotated tags referencing original (`corrects_point_id`) | Custom | FS-DI-04 — immutable points | FS-DI-04 | OQ `CAS-OQ-INFLUX-IMMUT-01` |
| DS-WATER-60 | Math Engine OQ Regression Dataset | F0-style + USP <645> Stage 1 conductivity-compensation + rolling-window math; canonical input file `cas_math_regress_v1.json` | Custom | FS-DI-05 — math regression | FS-DI-05 | OQ `CAS-OQ-MATH-01` |
| DS-WATER-61 | Inspection-Mode Query API > SLA | `≤ 4 h` retrievable per inspection-readiness runbook | Custom | FS-DI-06 — 4-h retrieval | FS-DI-06 | OQ `CAS-OQ-INSP-API-01` |
| DS-WATER-62 | Cat-5 SDLC SOP Reference | `CAS-SOP-IT-CAT5-001` (controlled doc) | Custom | FS-DEV-01 — Cat-5 SDLC | FS-DEV-01 | (governance) |
| DS-WATER-63 | Source Repo Branch Protection | `git.cassia.local/utilities/cassia-water-control`: 1+ reviewer + passing CI + Sigstore signed commits | Custom | FS-DEV-02 — branch protection | FS-DEV-02 | (CI) |
| DS-WATER-64 | CI Coverage Gate (safety/*) | `≥ 90%` (coverage.py for Python; Jacoco for Java sub-modules) | Custom | FS-DEV-03 — coverage gate | FS-DEV-03 | (CI) |
| DS-WATER-65 | CI Static-Analysis Stack | Ruff + mypy --strict + Bandit (Python); SpotBugs + PMD (Java); Trivy (container image); critical findings break build | Custom | FS-DEV-04 — static analysis | FS-DEV-04 | (CI) |
| DS-WATER-66 | Release Packaging | Ignition `.modl` files; cosign-signed against `cassia-sigstore-pubkey-2026q2` | Custom | FS-DEV-05 — cosign signing | FS-DEV-05 | (CI) + OQ `CAS-OQ-COSIGN-01` |
| DS-WATER-67 | Release Manifest `manifest.yaml` schema | `release_notes`, `fs_ds_cs_deltas`, `regression_test_summary`, `security_scan_report_path`, `cr_id` | Custom | FS-DEV-06 — manifest fields | FS-DEV-06 | (CI) |
| DS-WATER-68 | Determinism Harness — Canonical Input Replay | 1000× replay; bitwise-identical output verified at OQ via Python `hashlib.sha256` on output bundle | Custom | FS-DEV-07 — determinism harness | FS-DEV-07 | OQ `CAS-OQ-DETERMINISM-01` |
| DS-WATER-69 | TLS Configuration (HMI ↔ Gateway) | TLS 1.2+ mandatory; ciphers per NIST SP 800-52 Rev 2; mTLS Gateway ↔ PLC where supported | Custom | FS-SEC-02 — TLS posture | FS-SEC-02 | OQ `CAS-OQ-TLS-01` |
| DS-WATER-70 | Tenable Nessus Scan Schedule | monthly; criticals to remediation SLA 30 d | Custom | FS-SEC-03 — vuln scan | FS-SEC-03 | (governance) |
| DS-WATER-71 | Windows GPO — Removable-Media Block | block-by-default; vendor-approved exception path via CR | Custom | FS-SEC-04 — removable-media block | FS-SEC-04 | OQ `CAS-OQ-USB-01` |
| DS-WATER-72 | Service Accounts > HashiCorp Vault | short-lived (1 h TTL) creds for MES / eQMS / LIMS / Pyxis fetchers | Custom | FS-SEC-01 — service-account vaulting | FS-SEC-01 | OQ `CAS-OQ-VAULT-01` |
| DS-WATER-73 | InfluxDB Nightly Backup Schedule | `influxd backup` at 02:00 CET → S3 bucket `cas-water-influx-backups`; integrity verified via SHA-256 | Custom | FS-BAK-01 — nightly backup | FS-BAK-01 | OQ `CAS-OQ-BAK-NIGHTLY-01` |
| DS-WATER-74 | Restore-Test Cadence | quarterly; QA witness sign-off; runbook `CAS-RUN-WATER-RESTORE-01` | Custom | FS-BAK-02 — quarterly restore test | FS-BAK-02 | PR-01 |
| DS-WATER-75 | Hot-Spare Gateway RTO + Replication Lag | RTO ≤ 4 h; replication lag ≤ 1 min monitored via Prometheus `ignition_repl_lag_seconds` | Custom | FS-BAK-03 — DR posture | FS-BAK-03 | OQ `CAS-OQ-DR-01` |
| DS-WATER-76 | Cornerstone LMS Curriculum | `CAS-CURR-WATER-SCADA-<role>-v1` per role; production access gated by LMS completion attribute on AD group | Custom | FS-TRN-01 — training gate | FS-TRN-01 | (governance) |
| DS-WATER-77 | Annual Refresher Curriculum | `WATER-2026-ANNUAL` (alarm scenarios + USP <645>/<86> updates) | Custom | FS-TRN-02 — annual refresher | FS-TRN-02 | (governance) |
| DS-WATER-78 | Periodic-Review Template | `CAS-PR-WATER-SCADA-YYYYMMDD` covers config drift, code-release register, audit-trail review, alarm trends, training currency | Custom | FS-PR-01 — annual periodic review | FS-PR-01 | PR-01 |
| DS-WATER-79 | AD Conditional-Access Policy `OT-SCADA Conditional Access` | MFA at engineering workstation; operator stations named-location + role-bound smart cards | Custom | FS-XSYS-AD-01 — conditional access | FS-XSYS-AD-01 | OQ `CAS-OQ-CONDACC-01` |
| DS-WATER-80 | SIEM Forwarder (rsyslog → Splunk) | RFC 5424 to Splunk index `gxp-authn` within 5 min | Custom | FS-XSYS-AD-01 — SIEM forwarding | FS-XSYS-AD-01 | OQ `CAS-OQ-SIEM-01` |
| DS-WATER-81 | CyberArk PAM > Break-Glass Account Policy | 24-h password rotation + dual-witness check-out | Custom | FS-XSYS-AD-01 — break-glass gating | FS-XSYS-AD-01 | (governance) |
| DS-WATER-82 | Veeam Backup > Application-Aware Job | MS SQL Server VSS for the SCADA historian DB + file-level capture of PLC programs; tier T1; RPO ≤ 4 h; RTO ≤ 4 BH | Custom | FS-XSYS-BAK-01 — Veeam VSS | FS-XSYS-BAK-01 | OQ `CAS-OQ-VEEAM-01` |
| DS-WATER-83 | S3 Cloud-Tier Backup Bucket | Object-Lock Compliance Mode (geo-replicated); air-gap LTO-9 monthly rotation | Custom | FS-XSYS-BAK-01 — immutable cloud tier | FS-XSYS-BAK-01 | (governance) |
| DS-WATER-84 | Restore-Certificate Retention | ≥ 25 y in MasterControl eQMS | Custom | FS-XSYS-BAK-01 — restore-cert retention | FS-XSYS-BAK-01 | (governance) |

---

## 5. Workflow + Business-Rule Design

### 5.1 Sanitisation-Cycle Workflow (configured in site Python module + DB tables)

**Steps:** `SCHEDULE → PRE-FLUSH → MAIN-PHASE → RESIDUAL-DRAIN → POST-CHECK → CLOSE`. State transitions implemented in `SanitisationStateMachine` (Python module — see § 8). Each step persists a row in `sanitisation_events` with PTP timestamp + signing user + entry-condition snapshot.

| Step | Decision point | Rule | Actor | Signature meaning |
|---|---|---|---|---|
| SCHEDULE | Recipe EFFECTIVE? | Reject if not EFFECTIVE | (system) | n/a |
| PRE-FLUSH | Loop drained? | Drain-flowmeter reading < 0.5 L/min for 60 s | (system) | n/a |
| MAIN-PHASE | Hot-water / ozone / chemical per recipe | Setpoint + duration per recipe | Operator | `authorship` (cycle start) |
| RESIDUAL-DRAIN | Ozone residual ≤ 0.05 ppm for ≥ 120 s | Block close until threshold met | (system) | n/a |
| POST-CHECK | Microbiology Reviewer co-sign on CR | If CR open, route to Reviewer queue | Microbiology Reviewer | `review` |
| CLOSE | Close cycle, write to MES, set `cold_loop_in_service=true` | All signatures present + microbiology release | Senior Operator | `release` |

### 5.2 Recipe-Lifecycle Workflow (Postgres-enforced)

| Transition | Pre-condition | Required signatures | Resulting state |
|---|---|---|---|
| DRAFT → REVIEW | Author committed | Author `authorship` | REVIEW |
| REVIEW → APPROVED | All Reviewers signed | Reviewer `review` (n ≥ 2: Automation + Microbiology); CSV Reviewer `review` | APPROVED |
| APPROVED → EFFECTIVE | Variation gate (FS-PR-02) clear | Approver `approval` (Head of Manufacturing — Sterile + Head of QA dual-sign) | EFFECTIVE |
| EFFECTIVE → OBSOLETE | Superseded by new revision | Manufacturing Lead `retirement` | OBSOLETE |
| any → any (bypass) | not permitted | n/a — blocked by `recipe_transition_p` stored proc | rejected |

### 5.3 Override-Workflow Business Rule

Operator initiates override → UI presents reason field (≥ 10 chars) → Senior Operator countersign within 60 s → `override_events` row written → Pre-signed CCS-doc-ref attached → MasterControl auto-deviation created → cycle continues with `override_flag=true` on the cycle profile.

### 5.4 Alarm-Handling Business Rules (ISA-18.2)

- **INFO:** non-blocking, no ack required, 24 h auto-clear, no audit row beyond raise event.
- **WARNING:** ack required by Operator, reason optional, escalates to SMS on-call after 15 min.
- **CRITICAL:** ack required with reason ≥ 10 chars; persists until acknowledged; escalates SMS + email after 5 min; auto-deviation to MasterControl if unacknowledged > 30 min.
- **SIS (none in Water-SCADA; placeholder for future):** mirrored to dedicated `sis_events` table.

### 5.5 Endotoxin / TOC Action-Limit Decision Tree

```
TOC reading
     │
     ▼
Quality flag GOOD? ──No──► Raise TOC_QUALITY_DEGRADED (WARNING)
     │
    Yes
     ▼
Value > Action Limit (per water_quality_plan.yaml)?
     │
     ├─Yes──► Raise TOC_ACTION_LIMIT (CRITICAL) → auto-deviation MasterControl
     │
     └─No──► Append to trend ChannelLog; check Alert Limit for warning escalation
```

---

## 6. Role-Permission Matrix Design

The AD-group → permission mapping is the authoritative role surface. AD-groups are configured at `cassia.local` per FS-INT-AD-01. The table below records the permission matrix for the Ignition Perspective project and the site Python API endpoints.

| AD Group | View HMI | Acknowledge alarm | Author recipe | Approve recipe | Sign override | Microbiology release | Audit-trail review export | Admin (DB) |
|---|---|---|---|---|---|---|---|---|
| `Util-Water-Operator` | Y | Y (WARNING) | — | — | initiate | — | — | — |
| `Util-Water-SeniorOperator` | Y | Y (CRITICAL) | — | — | countersign | — | — | — |
| `Util-Water-RecipeAuthor` | Y | — | Y | — | — | — | — | — |
| `Util-Water-RecipeApprover` | Y | — | review | approve | — | — | — | — |
| `Util-Water-AutomationEngineer` | Y | Y | Y | — | — | — | — | — |
| `Util-Water-CSV-Reviewer` | Y | — | — | review (CSV) | — | — | Y | — |
| `Util-Water-Auditor` | Y (read-only) | — | — | — | — | — | Y | — |
| `Util-Water-Microbiology` | Y | — | — | — | — | Y | — | — |
| Break-Glass `Util-Water-DBA` (vaulted) | — | — | — | — | — | — | — | Y (with QA witness) |

Role-bound permissions enforced server-side at the API layer (Python module, see § 8) and at the Postgres `app_role` GRANT level. UI controls hide / disable based on group membership but never function as the sole enforcement (defense-in-depth). FS-IDs traced: FS-INT-AD-01, FS-PART11-04 (SoD), FS-CYC-04 (override dual-sign).

---

## 7. Integration Design

The DS records per-interface design choices. Vendor-internal protocol implementations are NOT redrawn (e.g., M9's internal OPC UA server stack is vendor-owned).

### 7.1 IF-MES-RECIPE-IN (PAS-X recipe download)

- **Endpoint:** `GET https://pasx.cassia.local/api/v1/recipes/{id}/effective`
- **Protocol:** HTTPS + mTLS; client cert `cassia-water-scada-2026q2` (rotation: 365 d via cert-manager)
- **Schema (response):** `{recipe_id, version, status, sha256, payload: <recipe JSON per § 4 CI DS-WATER-32>}`
- **Retry:** 1 s / 5 s / 30 s exponential backoff; circuit-breaker open after 5 consecutive failures (5 min cooldown)
- **Error handling:** `409` on checksum/version mismatch → block cycle + MasterControl deviation; `404` → operator notification; `5xx` → retry per above
- **Audit-trail emission:** every fetch writes an `audit_events` row with action `recipe_fetch` + outcome
- **FS-IDs:** FS-REC-05, FS-INT-MES-01

### 7.2 IF-MES-CYCLE-OUT (PAS-X cycle-profile push)

- **Endpoint:** `POST https://pasx.cassia.local/api/v1/cycles`
- **Protocol:** HTTPS + mTLS
- **Schema:** `{cycle_id (idempotency key), recipe_id, recipe_version, started_at, ended_at, channel_log_uri, alarm_log_uri, signatures[], overrides[]}`
- **Idempotency:** `cycle_id` is the dedup key on PAS-X side; duplicate POSTs return prior result
- **Retry:** as 7.1
- **Audit-trail emission:** action `cycle_report_post`
- **FS-IDs:** FS-INT-MES-02

### 7.3 IF-EQMS-DEV-OUT (MasterControl deviation creator)

- **Endpoint:** `POST https://eqms.cassia.local/api/v2/deviations`
- **Protocol:** HTTPS + mTLS (mTLS optional per MasterControl tenancy; client cert preferred)
- **Schema:** `{idempotency_key=alarm_id, severity, raised_at_ptp, source_system='CAS-WATER-SCADA', linked_records[]}`
- **Retry:** 1/5/30 s; escalates to on-call after 5 failures
- **Audit-trail emission:** action `deviation_post`
- **FS-IDs:** FS-INT-EQMS-01

### 7.4 IF-TOC-IN (Sievers M9 OPC UA)

- **Endpoint:** `opc.tcp://m9.cassia.local:4840`
- **Protocol:** OPC UA Binary over TLS (mutual auth); SecurityPolicy `Basic256Sha256`; cert `cassia-water-scada-2026q2`
- **Tag map:** `cas:water:toc:loop1` etc. mapped to Ignition Tag Provider `m9-prov`
- **Quality gate:** OPC UA `StatusCode` consumed; non-`Good` triggers `TOC_QUALITY_DEGRADED`
- **Error handling:** subscription loss → reconnect within 30 s; sustained loss > 5 min on hot loop → `TOC_LOSS_HOT_LOOP` critical alarm
- **FS-IDs:** FS-MON-TOC-01, FS-INT-TOC-01

### 7.5 IF-COND-IN (Mettler-Toledo M800 OPC UA)

- **Endpoint:** `opc.tcp://m800.cassia.local:4840` mTLS
- **Tag map:** `cas:water:cond:loop1.tc_value` (USP <645> Stage-1 temperature-compensated) + raw uncompensated value
- **Error handling:** loss → `COND_LOSS` warning; sustained loss → critical
- **FS-IDs:** FS-MON-TOC-03, FS-MON-COND-01, FS-INT-COND-01

### 7.6 IF-ENDO-IN (Charles River Endosafe REST)

- **Endpoint:** `POST /api/v1/endotoxin` (Endosafe pushes results to SCADA)
- **Protocol:** HTTPS; payload signed via ECDSA-P256 with vendor key `endosafe-cassia-2026q2.pub`; signature verified at boundary
- **Schema:** `{result_id, point_of_use, eu_per_ml, ts_ptp, signature, instrument_serial}`
- **Error handling:** invalid signature → reject + `ENDO_SIG_INVALID` critical alarm
- **FS-IDs:** FS-ENDO-01, FS-INT-ENDO-01

### 7.7 IF-EMS-IN (Pyxis EMS pull)

- **Endpoint:** `GET https://pyxis.cassia.local/api/v1/cleanroom/{room_id}/env` (dP, T, RH)
- **Protocol:** HTTPS
- **Cadence:** poll at cycle-start; cross-reference recorded in `cycle_environment_xref` table
- **FS-IDs:** FS-INT-EMS-01

### 7.8 IF-LIMS-IN (Watson LIMS)

- **Endpoint:** `GET https://lims.cassia.local/api/v1/results?type=endotoxin|micro&since={ts}`
- **Protocol:** HTTPS + mTLS
- **Linkage:** results linked to point-of-use + cycle + time-window per `endotoxin_linkage`
- **FS-IDs:** FS-ENDO-02

### 7.9 IF-AD-AUTH (LDAPS / Kerberos)

- **Endpoint:** `ldaps://ad.cassia.local:636` + Kerberos KDC `ad.cassia.local:88`
- **Schema (groups consumed):** `Util-Water-Operator`, `Util-Water-SeniorOperator`, `Util-Water-RecipeAuthor`, `Util-Water-RecipeApprover`, `Util-Water-AutomationEngineer`, `Util-Water-CSV-Reviewer`, `Util-Water-Auditor`, `Util-Water-Microbiology`
- **MFA:** Yubikey-backed; Conditional-Access policy per DS-WATER-79
- **SIEM:** events forwarded to Splunk index `gxp-authn` per DS-WATER-80
- **FS-IDs:** FS-INT-AD-01, FS-XSYS-AD-01

### 7.10 Integration Risk Register (per-interface)

| Interface | Risk | Mitigation |
|---|---|---|
| IF-MES-RECIPE-IN | mTLS cert expiry stalls fetch | cert-manager auto-rotation 365 d; alert at 30 d to expiry |
| IF-EQMS-DEV-OUT | MasterControl rate-limit | exponential backoff + circuit-breaker; deferred-deviation queue |
| IF-TOC-IN | M9 firmware divergence | vendor patch under CR; signal-quality monitored |
| IF-ENDO-IN | vendor key compromise | annual key rotation + revocation list at boundary |
| IF-AD-AUTH | AD outage | local OT-cached credentials (24 h) per `OT-SCADA Conditional Access` |

---

## 8. Site-Deployed Components — Mini-SDS for `cassia_water_control` (Cat 5)

Per § 2B.4 rule 6 — the embedded site Python module escalates this Cat 4 system to a hybrid Cat 4 + Cat 5. This section follows the Cat 5 SDS rules (§ 2B.5) at proportional depth for the ~2,500-LOC scope.

### 8.1 Software Architecture (logical view)

```
              ┌────────────────────────────────────────────────┐
              │  cassia_water_control (Ignition .modl, ~2.5k LOC) │
              │  ┌──────────────────────┐  ┌──────────────────┐ │
              │  │  api/                 │  │  rules/           │ │
              │  │  - RecipeApi         │  │  - HotWfiTempMon  │ │
              │  │  - SignatureApi      │  │  - ColdLoopGate   │ │
              │  │  - InspectionApi     │  │  - DeadLegSched   │ │
              │  └──────────────────────┘  │  - FlowXcheck     │ │
              │  ┌──────────────────────┐  │  - SanState       │ │
              │  │  engines/             │  └──────────────────┘ │
              │  │  - RecipeRunner       │  ┌──────────────────┐ │
              │  │  - TrendEngine        │  │  safety/          │ │
              │  │  - OolOosDetector     │  │  - PatLossHandler │ │
              │  │  - AnomalyDetector    │  │  - SafeStateEnter │ │
              │  └──────────────────────┘  └──────────────────┘ │
              │  ┌──────────────────────────────────────────┐   │
              │  │  integrations/                            │   │
              │  │  - RecipeFetcher / BatchReporter /        │   │
              │  │    DeviationCreator / EndoIngest /        │   │
              │  │    EmsPuller / LimsPuller                 │   │
              │  └──────────────────────────────────────────┘   │
              └────────────────────────────────────────────────┘
```

Stack: Python 3.11 on Ignition 8.3 Jython compatibility layer (where Jython 2.7 EOL constraints apply, modules quarantined; long-term migration to JVM via Ignition 9.x is on the roadmap per FS § 9).

### 8.2 Module Decomposition

| Module ID | Module name | Responsibility | Interface (exposes) | Dependencies | GxP class |
|---|---|---|---|---|---|
| MS-01 | `api.RecipeApi` | REST endpoints for recipe lifecycle | `GET /recipes/effective`, `POST /recipes/transition` | Postgres `recipe_versions`; SignatureApi | R1 |
| MS-02 | `api.SignatureApi` | E-signature verification + persist | `POST /signature` | AD Kerberos; `signature_events` table | R1 |
| MS-03 | `api.InspectionApi` | Read-only window-bound query for auditors | `GET /inspection/*` | `audit_events` (read-only); `cycle_report` | R2 |
| MS-04 | `engines.RecipeRunner` | 250 ms tick — evaluates deviations, classifies alarms | tag subscriptions; emits `alarm_events` | tag provider; rules/ | R1 |
| MS-05 | `engines.TrendEngine` | Rolling 15-min/1-h/24-h trend computation | writes to Perspective dashboard | InfluxDB query | R2 |
| MS-06 | `engines.OolOosDetector` | ASTM E2476 + Western Electric SPC rules | emits SPC alarms | `spc_limits` table | R1 |
| MS-07 | `engines.AnomalyDetector` | isolation-forest + heuristic patterns | emits maintenance alarms | model artefact (cosign-signed) | R2 |
| MS-08 | `rules.HotWfiTempMonitor` | hot-WFI < 80 °C ≥ T_window | emits `HOT_WFI_TEMP_LOW` | tag subscription | R1 |
| MS-09 | `rules.ColdLoopSanitisationGate` | gate `cold_loop_in_service` flag | reads `sanitisation_events` | DB | R1 |
| MS-10 | `rules.DeadLegFlushScheduler` | cron-driven flush per branch | writes `dead_leg_flush_events` | DB; tag writes | R1 |
| MS-11 | `rules.LoopFlowCrosscheck` | flow vs return-flow mismatch detection | emits `LOOP_FLOW_MISMATCH` | tag subscriptions | R2 |
| MS-12 | `rules.SanitisationStateMachine` | full cycle state machine | emits per-step events; transitions | DB; recipe API | R1 |
| MS-13 | `safety.PatLossHandler` | analyzer-loss safe-state activator | emits `*_LOSS` alarms + safe-state command | tag subscriptions; safe-state writer | R1 |
| MS-14 | `safety.SafeStateEnter` | writes safe-state setpoints to PLC | tag writes (CIP→drain, valves→close-except-vent) | PLC OPC UA | R1 |
| MS-15 | `integrations.RecipeFetcher` | mTLS client to PAS-X | callable from RecipeApi | PAS-X endpoint; Vault for service-creds | R1 |
| MS-16 | `integrations.BatchReporter` | mTLS post of cycle profile | end-of-cycle callable | PAS-X endpoint | R2 |
| MS-17 | `integrations.DeviationCreator` | mTLS post to MasterControl | alarm-handler callback | MasterControl endpoint | R1 |
| MS-18 | `integrations.EndoIngest` | REST receiver + ECDSA verifier | inbound endpoint | Endosafe public key | R1 |
| MS-19 | `integrations.EmsPuller` | poll Pyxis at cycle start | scheduled cycle hook | Pyxis endpoint | R2 |
| MS-20 | `integrations.LimsPuller` | poll Watson LIMS | scheduled | LIMS endpoint | R2 |

### 8.3 Data Model (DB schema highlights)

| Table | Key columns | Constraints | Retention | Encryption |
|---|---|---|---|---|
| `recipe_versions` | `recipe_id, version` (PK); `status` (enum); `sha256`; `signatures` (JSONB) | trigger blocks UPDATE/DELETE on EFFECTIVE | indefinite | at-rest AES-256 (Postgres TDE) |
| `audit_events` | `event_id` (PK); `actor_id` NOT NULL; `timestamp_ptp` | append-only via role GRANT; FK on `signature_event_id` | 25 y (online 5 y + S3 archive 25 y) | at-rest AES-256 |
| `alarm_events` | `alarm_id` (PK); `severity`; `ack_by`, `ack_at`, `reason` | reason CHECK length ≥ 10 when severity='CRITICAL' | 25 y | at-rest AES-256 |
| `sanitisation_events` | `cycle_id`; `phase`; `started_at`, `ended_at` | FK to recipe_version | 25 y | at-rest AES-256 |
| `dead_leg_flush_events` | `event_id`; `branch_id`; `flushed_at` | NOT-NULL on `branch_id` | 25 y | at-rest AES-256 |
| `override_events` | `override_id`; `cycle_id`; `op_id`, `senior_id`; `reason`; `ccs_doc_ref` | reason CHECK length ≥ 10 | 25 y | at-rest AES-256 |
| `signature_events` | `sig_id`; `record_id`; `record_hash`; `signer_id`; `meaning` | PKI signature payload bound | 25 y | at-rest AES-256 |
| `loop_model` | branch / drop / dead-leg / point-of-use FK to ASME BPE drawing | YAML schema validated at load | indefinite | at-rest AES-256 |

InfluxDB schemas: per-tag measurement with fields `value`, `quality_flag`, `source_tag`; tags include `loop`, `point_of_use`, `recipe_version`. Bucket retention per DS-WATER-07/08.

### 8.4 Algorithm + Calculation Design

| Algorithm | Inputs | Output | Formula / Procedure | Numerical-precision note | Reference |
|---|---|---|---|---|---|
| USP <645> Stage-1 Conductivity Compensation | M800 raw conductivity + temperature | compensated conductivity (µS/cm) | M800 native compensation (vendor-validated); SCADA consumes `tc_value` directly | IEEE-754 double; trust vendor 6-sig-fig | USP <645> Stage 1 |
| F0-style accumulated exposure (sanitisation effectiveness proxy) | shelf / loop T over time | accumulated F0 (min) | `F0 = ∫ 10^((T - 121.1) / z) dt`, z=10 | Trapezoidal integration; 1 s step; Decimal for cumulative | PDA TR-3 (informational) |
| Ozone Residual Compliance | residual ppm series | compliant boolean | residual ≤ 0.05 ppm sustained ≥ 120 s window | float64; threshold from `water_quality_plan.yaml` | USP <1231> |
| Pirani-vs-CM ratio (not used here; reserved cross-product) | (n/a) | (n/a) | (n/a) | (n/a) | (Boreas lyo DS) |
| Anomaly score (isolation forest) | tag-window matrix (15-min) | `is_anomaly ∈ {0,1}` + score | sklearn `IsolationForest(contamination=0.01)` | float32; model cosign-signed | (sklearn ref) |
| OOL/OOS — Western Electric Rule 1 | rolling-window readings | rule-fire boolean | reading > μ + 3σ | per-recipe σ stored in `spc_limits` | ASTM E2476 |
| Rolling-window mean / σ | tag time-series | mean, σ | numerically-stable Welford algorithm | float64; reset at recipe change | (Welford 1962) |

Determinism harness (FS-DEV-07): canonical input replay 1000× → bitwise-identical output, enforced via IEEE-754 round-mode pin (`numpy.errstate`) on all numeric paths.

### 8.5 Interface + API Design (Cat-5 module API)

| Endpoint | Method | AuthN | Request schema | Response schema | Idempotency | Audit-trail event |
|---|---|---|---|---|---|---|
| `/api/recipes/effective` | GET | Kerberos | `recipe_id (path)` | `RecipeVersion JSON` | safe | `recipe_fetch` |
| `/api/recipes/transition` | POST | Kerberos + signature payload | `{recordId, recordHash, signerId, meaning, signatureBlock}` | `{new_status, sig_id}` | by recordHash | `recipe_transition` |
| `/api/signature` | POST | Kerberos (fresh ticket ≤ 5 min) | `{recordId, recordHash, signerId, meaning}` | `{sig_id, pki_signature}` | by recordHash + meaning | `signature_emit` |
| `/api/override` | POST | Kerberos | `{cycle_id, op_id, senior_id, reason, ccs_doc_ref}` | `{override_id}` | by cycle_id + ts | `override_create` |
| `/api/endotoxin` | POST | mTLS (Endosafe boundary cert) | `{result_id, point_of_use, eu_per_ml, ts_ptp, signature}` | `{accepted: bool, alarm_raised: bool}` | by result_id | `endotoxin_ingest` |
| `/api/inspection/audit` | GET | Kerberos (Auditor group) | window query params | JSONL stream | safe | `inspection_query` |

Rate limit: 100 req/s per IP; error codes follow HTTP semantics with structured error JSON `{code, message, correlation_id}`.

### 8.6 Security Design

- **AuthN flow:** Kerberos ticket → SPNEGO at HTTPS layer → user-id binding → group lookup
- **AuthZ model:** AD-group → role mapping table (per § 6); evaluated server-side at every endpoint
- **Secret management:** HashiCorp Vault at `vault.cassia.local`; service-account creds 1-h TTL; mTLS client certs auto-rotated 365 d via cert-manager
- **Transport security:** TLS 1.2+ enforced; SecurityPolicy `Basic256Sha256` on OPC UA; ciphers per NIST SP 800-52 Rev 2
- **Audit-trail event taxonomy:** `recipe_fetch`, `recipe_transition`, `signature_emit`, `cycle_start`, `cycle_end`, `alarm_raise`, `alarm_ack`, `override_create`, `endotoxin_ingest`, `inspection_query`, `module_deploy`, `module_signature_verify`

### 8.7 Deployment Architecture

- **Packaging:** Ignition `.modl` file + auxiliary Python wheels; cosign-signed against `cassia-sigstore-pubkey-2026q2`
- **Topology:** Gateway-installed module loaded on each ACT gateway (gw1/2/3) and SB gateway (gw4); Gateway Event Scripts hook startup, shutdown, tag-change, scheduled
- **Observability:** Prometheus exporters (`recipe_runner_tick_ms`, `alarm_event_count`, `signature_emit_count`, `ptp_skew_milliseconds`); Grafana dashboards `CAS-GR-WATER-RUNTIME`; logs forwarded to Splunk
- **DR:** RTO ≤ 4 h to standby gateway (gw4); RPO ≤ 1 min via Postgres + InfluxDB replication

### 8.8 Module Specification Table (pointer)

| Module ID | File path | Unit-test ref |
|---|---|---|
| MS-01 — MS-20 | `git.cassia.local/utilities/cassia-water-control/{api,engines,rules,safety,integrations}/*.py` | `<repo>/tests/unit/test_<module>.py` (coverage ≥ 90% safety; ≥ 80% overall) |

Full Module Specifications live downstream as `CAS-MS-WATER-NN` artefacts (not in scope for v1.0 DS corpus).

---

## 9. References

### US
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .68, .180, .192
- USP <1231>, <645>, <643>, <85>, <86>
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EU GMP Annex 1 (2022 revision)
- EU GMP Annex 3
- EU GMP Annex 15
- EMA *Note for Guidance on Quality of Water for Pharmaceutical Use* (2020)

### DACH
- AMWHV (Arzneimittel- und Wirkstoffherstellungsverordnung)
- BSI IT-Grundschutz baseline (OT segmentation reference)

### International
- ISPE GAMP 5 (2nd Edition, 2022)
- ISPE Baseline Guide *Water and Steam Systems*
- ISPE GAMP GPG *Records and Data Integrity*
- ICH Q9(R1); ICH Q10; ICH Q12
- ISA-88 Part 1 + Part 2; ISA-95 Part 1; ISA-101; ISA-18.2
- IEC 61131-3 (PLC programming languages — informational, ControlLogix context)
- ASME BPE Bioprocess Equipment
- ASTM E2476
- PIC/S PI 041; PIC/S PI 009
- ISO/IEC 27001:2022; ISO/IEC 27002

### Vendor
- Inductive Automation — *Ignition 8.3 Reference* + *Ignition 8.3 System Administrator Guide*
- Sievers — *M9 TOC Reference Manual*
- Mettler-Toledo — *M800 Multi-Parameter Transmitter Reference*
- Allen-Bradley — *ControlLogix 5580 Reference Manual*
- Charles River — *Endosafe nexgen-PTS Integration Manual*

### Site
- `CAS-URS-WATER-SCADA-001` v1.2 (informational)
- `CAS-FS-WATER-SCADA-001` v1.2 (parent)
- `CAS-SOP-IT-CAT5-001` (Cat-5 SDLC)
- `CAS-OQ-*` (OQ protocols cited above)
- `CAS-PR-WATER-SCADA-YYYYMMDD` (periodic-review template)
- `CAS-RTM-WATER-SCADA-001` (RTM)

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-WATER-01 | FS-PLAT-01 |
| DS-WATER-02 | FS-PLAT-01 |
| DS-WATER-03 | FS-PLAT-02 |
| DS-WATER-04 | FS-PLAT-02 |
| DS-WATER-05 | FS-PLAT-03 |
| DS-WATER-06 | FS-PLAT-03 |
| DS-WATER-07 | FS-PLAT-04 |
| DS-WATER-08 | FS-PLAT-04 |
| DS-WATER-09 | FS-PLAT-05 |
| DS-WATER-10 | FS-PLAT-05 |
| DS-WATER-11 | FS-LOOP-01 |
| DS-WATER-12 | FS-LOOP-02 |
| DS-WATER-13 | FS-LOOP-03 |
| DS-WATER-14 | FS-LOOP-04 |
| DS-WATER-15 | FS-LOOP-05 |
| DS-WATER-16 | FS-MON-TOC-01 |
| DS-WATER-17 | FS-MON-TOC-02 |
| DS-WATER-18 | FS-MON-TOC-03 / FS-MON-COND-01 |
| DS-WATER-19 | FS-MON-TOC-03 |
| DS-WATER-20 | FS-MON-COND-02 |
| DS-WATER-21 | FS-SAN-01 |
| DS-WATER-22 | FS-SAN-02 / FS-CYC-05 |
| DS-WATER-23 | FS-SAN-03 |
| DS-WATER-24 | FS-SAN-04 |
| DS-WATER-25 | FS-SAN-05 |
| DS-WATER-26 | FS-REC-01 |
| DS-WATER-27 | FS-REC-01 / FS-REC-03 |
| DS-WATER-28 | FS-REC-02 |
| DS-WATER-29 | FS-REC-03 |
| DS-WATER-30 | FS-REC-04 |
| DS-WATER-31 | FS-REC-05 / FS-INT-MES-01 |
| DS-WATER-32 | FS-REC-06 |
| DS-WATER-33 | FS-CYC-01 |
| DS-WATER-34 | FS-CYC-01 |
| DS-WATER-35 | FS-CYC-02 |
| DS-WATER-36 | FS-CYC-03 |
| DS-WATER-37 | FS-CYC-04 |
| DS-WATER-38 | FS-ENDO-01 |
| DS-WATER-39 | FS-ENDO-02 |
| DS-WATER-40 | FS-ENDO-03 |
| DS-WATER-41 | FS-TREND-01 |
| DS-WATER-42 | FS-TREND-02 |
| DS-WATER-43 | FS-TREND-03 |
| DS-WATER-44 | FS-TREND-04 |
| DS-WATER-45 | FS-AUD-01 / FS-DI-01 |
| DS-WATER-46 | FS-AUD-02 |
| DS-WATER-47 | FS-AUD-03 |
| DS-WATER-48 | FS-AUD-04 |
| DS-WATER-49 | FS-PART11-01 |
| DS-WATER-50 | FS-PART11-02 / FS-PART11-03 |
| DS-WATER-51 | FS-PART11-04 / FS-PART11-05 |
| DS-WATER-52 | FS-PART11-06 |
| DS-WATER-53 | FS-PART11-07 |
| DS-WATER-54 | FS-PART11-08 |
| DS-WATER-55 | FS-AN1-01 |
| DS-WATER-56 | FS-DI-01 |
| DS-WATER-57 | FS-DI-02 |
| DS-WATER-58 | FS-DI-03 |
| DS-WATER-59 | FS-DI-04 |
| DS-WATER-60 | FS-DI-05 |
| DS-WATER-61 | FS-DI-06 |
| DS-WATER-62 | FS-DEV-01 |
| DS-WATER-63 | FS-DEV-02 |
| DS-WATER-64 | FS-DEV-03 |
| DS-WATER-65 | FS-DEV-04 |
| DS-WATER-66 | FS-DEV-05 |
| DS-WATER-67 | FS-DEV-06 |
| DS-WATER-68 | FS-DEV-07 |
| DS-WATER-69 | FS-SEC-02 |
| DS-WATER-70 | FS-SEC-03 |
| DS-WATER-71 | FS-SEC-04 |
| DS-WATER-72 | FS-SEC-01 |
| DS-WATER-73 | FS-BAK-01 |
| DS-WATER-74 | FS-BAK-02 |
| DS-WATER-75 | FS-BAK-03 / FS-PERF-01 / FS-PERF-02 |
| DS-WATER-76 | FS-TRN-01 |
| DS-WATER-77 | FS-TRN-02 |
| DS-WATER-78 | FS-PR-01 |
| DS-WATER-79 | FS-XSYS-AD-01 |
| DS-WATER-80 | FS-XSYS-AD-01 |
| DS-WATER-81 | FS-XSYS-AD-01 |
| DS-WATER-82 | FS-XSYS-BAK-01 |
| DS-WATER-83 | FS-XSYS-BAK-01 |
| DS-WATER-84 | FS-XSYS-BAK-01 |
| MS-01 — MS-20 | (Cat-5 mini-SDS § 8.2 — supporting site-developed code; transitively traces FS-DEV-01..07 + FS-REC-* + FS-CYC-* + FS-LOOP-* + FS-SAN-* + FS-ENDO-* + FS-TREND-* + FS-AUD-* + FS-INT-*) |

---

## 11. Design-level Risk Register

Per § 2B.8 — design-stage risks originating in design choices (not user wishes / functional behaviour / implementation defects). The formal Risk Assessment lives in `CAS-RA-WATER-SCADA-001` (synthetic, downstream).

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| DR-01 | Cosign public-key rotation breaks runtime module load (`.modl` signature verification fails after key roll) | Low | High | Paired-key transition window + monitoring; documented rotation procedure (DS-WATER-66 + DS-WATER-68) |
| DR-02 | Jython 2.7 EOL impacts long-term support of Python control logic | Medium | Medium | Roadmap to migrate to Ignition 9.x JS / Java runtime when GA; quarantine Jython-only modules |
| DR-03 | LoopModel divergence from ASME BPE as-built drawings after physical retrofit (DS-WATER-11 binding stale) | Medium | High | Annual reconciliation review under PR-01 + change-control gate on physical work-order |
| DR-04 | InfluxDB 2.x retention semantics change on minor-version upgrade (DS-WATER-07/08 silent break) | Low | High | Quarterly retention audit; pin to InfluxDB 2.7 LTS only |
| DR-05 | Postgres patroni cluster split-brain (etcd quorum loss) corrupting `audit_events` | Low | Critical | etcd 3-node odd quorum + fencing; restore-test quarterly |
| DR-06 | Determinism harness (DS-WATER-68) gives false-pass when canonical input does not cover edge cases | Medium | Medium | Annual expansion of canonical input set + targeted edge-case tests; coverage-by-rule metric |
| DR-07 | Conditional-Access policy (DS-WATER-79) too tight → operator lockout on iPad MDM device loss | Low | Medium | Operator named-location fallback to plant network; CyberArk break-glass |
| DR-08 | Endosafe vendor key (DS-WATER-38 ECDSA pubkey) compromise; payload signature bypass risk | Low | High | Annual rotation + revocation-list check at boundary; mutual-TLS additionally on transport |
| DR-09 | mTLS cert `cassia-water-scada-2026q2` expiry during weekend stall recipe fetch | Low | High | cert-manager rotation at 30 d prior to expiry + on-call alert; circuit-breaker degrades to cached EFFECTIVE recipe with cycle-block after 4 h |
| DR-10 | Site Python module hot-deploy on ACT gateway introduces drift vs SB gateway (gw4) | Low | Medium | Module deployment gated by all-gateway cosign verification at startup (DS-WATER-66) |
| DR-11 | Alarm-table YAML (DS-WATER-34) misconfiguration suppresses critical-class on a tag | Low | High | OQ verification of every tag's class entry; quarterly alarm-rationalisation audit |
| DR-12 | OPC UA `Basic256Sha256` deprecation by vendor mid-life (10-year platform lifespan) | Low | Medium | Roadmap to `Aes256_Sha256_RsaPss` when vendor + PLC support |
| DR-13 | InfluxDB cold-store S3 Object-Lock retention misconfigured to Governance Mode instead of Compliance Mode (silently mutable by root) | Low | Critical | IQ verification of Object-Lock mode at bucket creation + annual recheck |
| DR-14 | Vault TTL too short causes service-account churn → fetch-storm on rotation | Medium | Medium | TTL pinned to 1 h with 5-min overlap; rate-limit on Vault token issuance |
| DR-15 | AD-group naming drift (Util-Water-* renamed by AD team) silently breaks role-mapping | Low | High | Group-name SID stored in role-mapping table (not name); annual reconciliation |
| DR-16 | PTP grandmaster single point of failure | Low | High | Boundary-clock redundancy + NTP fallback per FS-PLAT-05 |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
