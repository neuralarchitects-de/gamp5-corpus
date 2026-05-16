---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (Cat 4 / Tier T3)"
seed_corpus_basis:
  - "CRC-FS-BIOSCADA-001 v1.2 (parent FS)"
  - "CRC-URS-BIOSCADA-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd Edition) Category 4 — Configuration Specification conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11; Annex 1 (2022 revision); Annex 2; Annex 15"
  - "ICH Q9(R1); ICH Q11; ICH Q12; ICH Q13"
  - "USP <1043>; ATMP Guidelines"
  - "ISA-88; ISA-95; ISA-101; ISA-18.2; IEC 61511"
  - "PIC/S PI 041; ISPE GAMP GPG PAT"
parent_fs:
  document_number: CRC-FS-BIOSCADA-001
  version: "1.2"
  file: "../../../FS_FDS/_generated/final/Crocus_Pharma_Bioreactor_SCADA_FS_v1.3.md"
parent_urs:
  document_number: CRC-URS-BIOSCADA-001
  version: "1.2"
  file: "../../../URS/_generated/final/Bioreactor_Continuous_Fermentation_SCADA__Crocus_Pharma_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Bioreactor Continuous-Fermentation SCADA — Inductive Automation Ignition 8.3 + Emerson DeltaV v15.3 + Site Python Orchestrator (Cat 5)

**Document Number:** CRC-DS-BIOSCADA-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** CRC-FS-BIOSCADA-001 v1.2
**Parent URS:** CRC-URS-BIOSCADA-001 v1.2 *(informational, transitive)*
**Site:** Crocus Pharma (Suzhou) Plant 1, Suzhou Industrial Park, China *(fictional)*
**System Owner:** Bioprocess Automation Lead
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (Ignition 8.3 + DeltaV v15.3 platform), with site-developed Python Orchestrator + APC + SoftSensor assessed as Cat 5 sub-components (mini-SDS in § 8)
**Project Mode:** Configuration project on commercial software products **Ignition 8.3** + **Emerson DeltaV v15.3** (GAMP 5 Category 4) with embedded Cat-5 site Python Orchestrator under hybrid governance.
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Annex 1 (2022); EU GMP Annex 2; EU GMP Annex 15; ICH Q9(R1); ICH Q11; ICH Q12; ICH Q13; USP <1043>; ATMP Guidelines; ISA-88; ISA-95; ISA-101; ISA-18.2; IEC 61511; PIC/S PI 041.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect — BioSCADA) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Bioprocess Engineer) | _____________ | _____________ | _____ |
| Reviewer (PAT Chemometrician) | _____________ | _____________ | _____ |
| Reviewer (Functional Safety Engineer) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Security Architect — OT) | _____________ | _____________ | _____ |
| Approver (System Owner — Bioprocess Automation Lead) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Design Control

- **Document Number:** CRC-DS-BIOSCADA-001
- **Version:** 1.1
- **Effective Date:** 2026-05-15 *(synthetic)*
- **Parent FS:** CRC-FS-BIOSCADA-001 v1.2
- **Parent URS:** CRC-URS-BIOSCADA-001 v1.2 *(informational)*
- **Site:** Crocus Pharma (Suzhou) Plant 1, Suzhou Industrial Park, China
- **System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (Ignition + DeltaV) with embedded Cat-5 Python Orchestrator
- **Project Mode:** Hybrid Cat 4 + Cat 5 — § 4–§ 7 CS rules; § 8 mini-SDS for Orchestrator
- **Regulatory Scope:** as above

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T3 from parent URS+FS pair. DS covers 97/97 FS-IDs from CRC-FS-BIOSCADA-001 v1.2. No FS-IDs flagged vendor-internal — Ignition + DeltaV configuration surfaces site-designable; SIS partition (DeltaV SIS SIL 2) vendor-validated but configuration of bypass + event mirror is site-designed and covered here. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from CRC-FS-BIOSCADA-001 and CRC-URS-BIOSCADA-001. DS-specific terms:

| Term | Definition |
|---|---|
| Orchestrator | Site-authored Python service on OpenShift 4.14 (~6,500 LOC) implementing recipe / phase / APC / SoftSensor |
| APC | Advanced Process Control sub-module of the Orchestrator |
| SoftSensor | Inferential-sensor sub-module (capacitance + Raman + off-gas → VCD / titer / quality) |
| PatModel | Versioned chemometric model (MLflow-tracked) |
| ATMP | Advanced Therapy Medicinal Product |
| ATF 6 | Repligen XCell ATF 6 perfusion skid (cell retention) |
| TMP | Trans-membrane pressure (perfusion membrane) |

---

## 1. Purpose

This DS specifies the technical design that satisfies the FS `CRC-FS-BIOSCADA-001` v1.2 for the Crocus Pharma Suzhou Plant-1 bioreactor continuous-fermentation SCADA. It records the Ignition 8.3 + DeltaV v15.3 + Orchestrator CI inventory, the recipe / ISA-88 phase / feed / PAT / single-use-vs-stainless / ATMP / alarm / HMI / SDLC / audit / integration workflow + business-rule design, the role-permission matrix, the per-interface integration design (PAS-X, MasterControl, Aspen IP.21, Watson LIMS, BMS, PAT instruments, AD), and a mini-SDS for the site Python Orchestrator. Controlling input to IQ / OQ / PQ / RTM `CRC-RTM-BIOSCADA-001`.

## 2. Scope

**In scope.** Configuration of Ignition 8.3 Gateway cluster (active + DR), DeltaV v15.3 controllers + ApplicationStation pair + DeltaV SIS (SIL 2 partition), Orchestrator on OpenShift 4.14 (3 replicas + DR), MLflow PAT-model registry, all integrations (PAS-X v3.2, MasterControl, Aspen IP.21, Watson LIMS, BMS, Kaiser RamanRxn4 / Hamilton Incyte / Thermo Prima Pro / Sartorius BioPAT Spectro), Sartorius STR / Cytiva XDR / ABEC CSTR config-matrix, Repligen ATF 6, Watson-Marlow Quantum pumps, AD `crocus.local`, and the Python Orchestrator (Cat-5).

**Out of scope.** Vendor-internal Ignition / DeltaV / SIS code; physical bioreactor equipment; downstream IQ/OQ/PQ protocols (referenced only); MLflow PAT-model lifecycle artefacts (governed under `PAT-MODEL-LCM-001`, separate).

## 3. Architectural Overview

```
        ┌────────────────────────────────────────────────────────────┐
        │  AD/Kerberos (crocus.local) │ PKI │ PTP IEEE 1588 master      │
        └────────────────────┬───────────────────────────────────────┘
                             │
    ┌────────────────────────▼──────────────────────────────────────┐
    │   Ignition 8.3 Gateway Cluster (Active + DR; failover ≤ 60 s)   │
    │   ┌──────────────────────────┐  ┌─────────────────────────────┐ │
    │   │ Vision/Perspective HMI    │  │ Tag Provider (DeltaV bridge) │ │
    │   │ (ISA-101 hierarchy)       │  │                              │ │
    │   └──────────────────────────┘  └─────────────────────────────┘ │
    └────────────────────────┬──────────────────────────────────────┘
                             │ OPC UA mTLS
                             ▼
    ┌──────────────────────────────────────────────────────────────┐
    │  OpenShift 4.14 namespace `bioscada-prod` (3 replicas + DR)     │
    │  ┌────────────────────────────────────────────────────────┐  │
    │  │  Python Orchestrator (Cat 5, ~6.5k LOC) — § 8            │  │
    │  │  - Recipe engine (ICH Q13)                              │  │
    │  │  - PhaseStateMachine (ISA-88)                           │  │
    │  │  - APC + SoftSensor (Kalman fusion)                     │  │
    │  │  - PatLossHandler + SafeStateEnter                      │  │
    │  │  - DeterministicLogger                                  │  │
    │  └────────────────────────────────────────────────────────┘  │
    └────────┬──────────────────┬──────────────┬──────────────┬────┘
             │                  │              │              │
             ▼                  ▼              ▼              ▼
       DeltaV v15.3       PAT Bus       PAS-X / eQMS    Aspen IP.21
       Controllers +      (OPC UA mTLS) (REST mTLS)     (OPC HDA / UA)
       SIS SIL 2          Raman /                       Watson LIMS
       1oo2D              Capacitance /                 (REST + USP <1043>)
                          Off-gas / VCD                 BMS (OPC UA)
                                                        Repligen ATF 6
                                                        + Quantum pumps
```

Cluster design choices: OpenShift PodDisruptionBudget min available = 2; HPA disabled in prod (deterministic load); Ignition Gateway cluster mode with redundant tag providers; DeltaV ProfessionalPLUS + ApplicationStation redundant; SIS pair 1oo2D; Aspen IP.21 store-and-forward at gateway for blip recovery.

---

## 4. Configuration Specification

Per § 2B.4 — every CI listed once. Vendor source code not redrawn.

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-BIO-01 | OpenShift Namespace + Replicas | `bioscada-prod`, 3 replicas + DR cluster `bioscada-dr` | Custom | FS-PLAT-01 — 3 replicas + DR | FS-PLAT-01 | OQ `CRC-OQ-OS-REPL-01` |
| DS-BIO-02 | Ignition Gateway Cluster | `gw1-gw4` ACT + SB; auto-failover ≤ 60 s | Custom | FS-PLAT-01 — Ignition failover | FS-PLAT-01 | OQ `CRC-OQ-IG-FAIL-01` |
| DS-BIO-03 | DeltaV Redundant Pair | per Emerson reference | Default | FS-PLAT-01 — DeltaV redundancy | FS-PLAT-01 | OQ `CRC-OQ-DV-FAIL-01` |
| DS-BIO-04 | HMI `gw-cluster-health` Faceplate | sources `audit_events` failover rows | Custom | FS-PLAT-01 — failover surfacing | FS-PLAT-01 | OQ `CRC-OQ-FACE-CLUSTER-01` |
| DS-BIO-05 | Schneider Galaxy UPS Hold | ≥ 30 min; DeltaV SIS isolated UPS branch | Custom | FS-PLAT-02 — UPS | FS-PLAT-02 | IQ `CRC-IQ-UPS-01` |
| DS-BIO-06 | Default-Safe-State Config | perfusion stop, glucose feed stop, agitator 30 rpm min, jacket hold last SP, vent-valve open | Custom | FS-PLAT-02 — safe-state | FS-PLAT-02 | OQ `CRC-OQ-SAFE-STATE-01` |
| DS-BIO-07 | Process-Control VLAN | VLAN 312 (Purdue Level 2/3); firewall + DMZ to corporate; allow-list egress to PAS-X / eQMS / IP.21 / LIMS | Custom | FS-PLAT-03 — VLAN | FS-PLAT-03 | IQ `CRC-IQ-NET-01` |
| DS-BIO-08 | Meinberg PTP Grandmaster | enabled; `ptp_skew_milliseconds` Prometheus exporter; > 1 ms → `PTP_SKEW_DEGRADED` | Custom | FS-PLAT-04 — PTP skew | FS-PLAT-04 | OQ `CRC-OQ-PTP-01` |
| DS-BIO-09 | Hardware/Firmware Refresh CR | `CRC-SOP-CR-001` with impact-assessment scope | Custom | FS-PLAT-05 — change control | FS-PLAT-05 | (governance) |
| DS-BIO-10 | Postgres `recipe_versions` Lifecycle Enum | `('DRAFT','REVIEW','APPROVED','EFFECTIVE','OBSOLETE')`; stored-proc-enforced transitions + signatures | Custom | FS-REC-01 — lifecycle | FS-REC-01 | OQ `CRC-OQ-REC-STATES-01` |
| DS-BIO-11 | ISA-88 Recipe Tables | `master_recipe`, `site_recipe`, `control_recipe` with version-pinned FKs | Custom | FS-REC-02 — ISA-88 hierarchy | FS-REC-02 | OQ `CRC-OQ-REC-HIER-01` |
| DS-BIO-12 | Recipe Schema Required Fields | `cqa_list, cpp_envelope, pat_rule_set, perfusion_schedule, feed_strategy_envelope, harvest_decision_rules, alarm_thresholds` | Custom | FS-REC-03 — recipe schema | FS-REC-03 | OQ `CRC-OQ-REC-SCHEMA-01` |
| DS-BIO-13 | Runtime API `GET /api/recipes/effective` | filters `status='EFFECTIVE'`; HTTP 404 otherwise | Custom | FS-REC-04 — EFFECTIVE only | FS-REC-04 | OQ `CRC-OQ-REC-EFF-01` |
| DS-BIO-14 | DB Trigger > EFFECTIVE Immutability | UPDATE/DELETE blocked when EFFECTIVE; UI hides edit controls | Custom | FS-REC-05 — immutability | FS-REC-05 | OQ `CRC-OQ-REC-IMMUT-01` |
| DS-BIO-15 | Transition Endpoint `/api/recipes/transition` | signed-JWT payload + dual-token validation | Custom | FS-REC-06 — JWT + dual-sign | FS-REC-06 | OQ `CRC-OQ-REC-JWT-01` |
| DS-BIO-16 | PAS-X Recipe Receiver | SHA-256 + version validation; mismatch → 409 + MasterControl deviation | Custom | FS-REC-07 / FS-INT-MES-01 — checksum | FS-REC-07, FS-INT-MES-01 | OQ `CRC-OQ-REC-CKSUM-01` |
| DS-BIO-17 | APPROVAL Workflow Reference Check | verifies PAT-model + phase-logic versions exist + APPROVED; broken → `RECIPE_BROKEN_REFS` | Custom | FS-REC-08 — broken-refs gate | FS-REC-08 | OQ `CRC-OQ-REC-REFCHK-01` |
| DS-BIO-18 | CR Template — Recipe Change | captures impacted CQAs / CPPs + ICH Q12 EC classification + variation-status flag | Custom | FS-REC-09 — Q12 EC class | FS-REC-09 | OQ `CRC-OQ-REC-Q12-01` |
| DS-BIO-19 | ISA-88 Procedural Tables | `procedure / unit_procedure / operation / phase` | Custom | FS-PHASE-01 — ISA-88 procedural | FS-PHASE-01 | OQ `CRC-OQ-PHASE-PROC-01` |
| DS-BIO-20 | `PhaseStateMachine` Enum | `INOCULATION, EXPONENTIAL_GROWTH, STEADY_STATE_PERFUSION, HARVEST_DECISION, HARVEST_BLEED, CAMPAIGN_END, CIP, SIP` with entry/exit conditions in `phase_rules.yaml` | Custom | FS-PHASE-02 — state machine | FS-PHASE-02 | OQ `CRC-OQ-PHASE-SM-01` |
| DS-BIO-21 | `phase_events` Append-Only Table | PTP timestamp + entry/exit snapshot + signing user | Custom | FS-PHASE-03 — phase events | FS-PHASE-03 | OQ `CRC-OQ-PHASE-EVT-01` |
| DS-BIO-22 | `phase_safe_state.yaml` Schema | `safe_state_on_pat_loss`, `safe_state_on_utility_loss`, `safe_state_on_abort`; validated at APPROVAL | Custom | FS-PHASE-04 — safe-state metadata | FS-PHASE-04 | OQ `CRC-OQ-PHASE-SAFE-01` |
| DS-BIO-23 | Out-of-Envelope Transition Workflow | Operator + Senior Operator dual-sign + reason ≥ 10 chars + input-snapshot pointer | Custom | FS-PHASE-05 — out-of-envelope | FS-PHASE-05 | OQ `CRC-OQ-PHASE-OOE-01` |
| DS-BIO-24 | Prometheus Exporters (phase) | `phase_duration_seconds`, `phase_deviation_count`, `phase_signed_events_count` | Custom | FS-PHASE-06 — observability | FS-PHASE-06 | (CI) |
| DS-BIO-25 | `GlucoseFeedController` Config | Raman PLS predictions consumed; rule version pinned via `feed_rule_version` FK; output to Watson-Marlow Quantum via OPC UA | Custom | FS-FEED-01 — glucose feed | FS-FEED-01 | OQ `CRC-OQ-FEED-GLUC-01` |
| DS-BIO-26 | `PerfusionController` Sensor Fusion | Kalman filter on capacitance + on-line VCD; demotion authority per `PerfusionAuthorityMatrix` | Custom | FS-FEED-02 — perfusion control | FS-FEED-02 | OQ `CRC-OQ-FEED-PERF-01` |
| DS-BIO-27 | Override Workflow | Op + Senior dual-sign; input-snapshot S3 URI on `override_events` | Custom | FS-FEED-03 — override | FS-FEED-03 | OQ `CRC-OQ-OVR-01` |
| DS-BIO-28 | Pump-Integrity Cross-Check | `rotation_sensor` vs `flow_meter` every 5 s; mismatch ≥ 5% > 60 s → `PUMP_CROSSCHECK_FAIL` + open-loop fallback | Custom | FS-FEED-04 — pump integrity | FS-FEED-04 | OQ `CRC-OQ-PUMP-XCHK-01` |
| DS-BIO-29 | `BleedRateController` | target-VCD setpoint; alarms per `bleed_alarm_table.yaml` | Custom | FS-FEED-05 — bleed rate | FS-FEED-05 | OQ `CRC-OQ-BLEED-01` |
| DS-BIO-30 | `FoulingPredictor` | hourly on ATF 6 TMP + flux trends; `ATF_FOULING_PRECURSOR` maintenance alarm | Custom | FS-FEED-06 — fouling predictor | FS-FEED-06 | OQ `CRC-OQ-FOUL-01` |
| DS-BIO-31 | PAT Instrument OPC UA Endpoints | per instrument: `opc.tcp://<instr>.crocus.local:4840` mTLS; `PatQualityGate` checks tag-quality < `GOOD_LOCAL_OVERRIDE` | Custom | FS-PAT-01 / FS-INT-PAT-01 — OPC UA + quality gate | FS-PAT-01, FS-INT-PAT-01 | OQ `CRC-OQ-PAT-OPC-01` |
| DS-BIO-32 | MLflow PAT-Model Registry | states `DRAFT/CALIBRATED/CROSS-VALIDATED/APPROVED/EFFECTIVE/OBSOLETE`; signature-gated transitions | Custom | FS-PAT-02 — model registry | FS-PAT-02 | OQ `CRC-OQ-PAT-LCM-01` |
| DS-BIO-33 | Runtime Model Loader | verifies `model_version == effective_recipe.pat_model_version`; mismatch → `PAT_MODEL_VERSION_MISMATCH` | Custom | FS-PAT-03 — version match | FS-PAT-03 | OQ `CRC-OQ-PAT-VER-01` |
| DS-BIO-34 | `PatLossHandler` | recipe-defined safe-state: open-loop feed + APC demotion + deviation creation; deterministic | Custom | FS-PAT-04 / FS-RUN-06 — PAT loss | FS-PAT-04, FS-RUN-06 | OQ `CRC-OQ-PAT-LOSS-01` |
| DS-BIO-35 | `PatPerformanceMonitor` | rolling residual / Hotelling T² / Q-statistic per ASTM E2476; OOS → `PAT_MODEL_OUT_OF_CONTROL` | Custom | FS-PAT-05 — performance monitor | FS-PAT-05 | OQ `CRC-OQ-PAT-PERF-01` |
| DS-BIO-36 | Reference-Method Calibration Cadence | 12 h steady-state (recipe-defined); LIMS HPLC / cell-counter deltas logged | Custom | FS-PAT-06 — reference calibration | FS-PAT-06 | OQ `CRC-OQ-PAT-CAL-01` |
| DS-BIO-37 | PAT-Model Approval Workflow | Chemometrician + Process Sciences + QA sign; regulator-impacting linked to `variation_record_id` | Custom | FS-PAT-07 — approval workflow | FS-PAT-07 | OQ `CRC-OQ-PAT-APPR-01` |
| DS-BIO-38 | `RecipeRunner.tick_ms` | `250` ms | Custom | FS-RUN-01 — 250 ms tick | FS-RUN-01 | OQ `CRC-OQ-RUNNER-TICK-01` |
| DS-BIO-39 | Critical Alarm Ack Policy | `selfAcknowledgement=false`; reason ≥ 10 chars persisted | Custom | FS-RUN-02 — critical ack | FS-RUN-02 | OQ `CRC-OQ-ALARM-ACK-01` |
| DS-BIO-40 | Log Rates | CPP 1 Hz; Raman 1/min; capacitance 30 s; off-gas 5 s; VCD 30 s; PLC scan 100 ms with on-change deadband | Custom | FS-RUN-03 — log rates | FS-RUN-03 | OQ `CRC-OQ-LOG-RATE-01` |
| DS-BIO-41 | Decision Payload Schema | `decision_id, recipe_version, pat_model_version, code_release, input_snapshot_uri, output, timestamp_ptp` | Custom | FS-RUN-04 — decision schema | FS-RUN-04 | OQ `CRC-OQ-DECISION-01` |
| DS-BIO-42 | `CommandSequenceGuard` | rejects out-of-sequence operator commands; signed-reason override path | Custom | FS-RUN-08 — sequence guard | FS-RUN-08 | OQ `CRC-OQ-SEQ-GUARD-01` |
| DS-BIO-43 | PAS-X Production-Order Ingestion | transactional + idempotent recipe-load | Custom | FS-RUN-07 — order ingestion | FS-RUN-07 | OQ `CRC-OQ-ORD-INGEST-01` |
| DS-BIO-44 | `alarm_rationalisation.yaml` | per tag: INFO/WARNING/CRITICAL/SIS + response + ack + escalation | Custom | FS-ALM-01 — rationalisation | FS-ALM-01 | OQ `CRC-OQ-ALARM-RAT-01` |
| DS-BIO-45 | Critical Alarm Escalation | reason ≥ 10; unack > T_escalate → SMS + email on-call | Custom | FS-ALM-02 — escalation | FS-ALM-02 | OQ `CRC-OQ-ALARM-ESC-01` |
| DS-BIO-46 | Alarm-Flood Detector | rate > N/min → shelving per ISA-18.2; events to `alarm_shelving_events` | Custom | FS-ALM-03 — flood detector | FS-ALM-03 | OQ `CRC-OQ-ALARM-FLOOD-01` |
| DS-BIO-47 | DeltaV SIS Event Mirror | events mirrored to `sis_events` (read-only); FSE-signed CR for bypass | Custom | FS-ALM-04 — SIS mirror | FS-ALM-04 | OQ `CRC-OQ-SIS-MIRROR-01` |
| DS-BIO-48 | Prometheus Exporter `alarm_metrics` | rate, ack-latency P50/P95, top-talkers, shelving freq | Custom | FS-ALM-05 — alarm metrics | FS-ALM-05 | OQ `CRC-OQ-ALARM-METRICS-01` |
| DS-BIO-49 | Perspective ISA-101 Hierarchy | Level 1-4; navigation ≤ 3 clicks audited at `CRC-HMI-DR-01` | Custom | FS-HMI-01 — ISA-101 | FS-HMI-01 | OQ `CRC-OQ-HMI-NAV-01` |
| DS-BIO-50 | HMI Palette | greys normal; saturated abnormal; red=critical, amber=warning, blue=info, magenta=SIS | Custom | FS-HMI-02 — palette | FS-HMI-02 | OQ `CRC-OQ-HMI-PALETTE-01` |
| DS-BIO-51 | Faceplate SLO | P95 ≤ 500 ms via synthetic monitoring | Custom | FS-HMI-03 — faceplate SLO | FS-HMI-03 | OQ `CRC-OQ-HMI-SLO-01` |
| DS-BIO-52 | HMI CR + `gw-test` Gateway | regression run before deploy | Custom | FS-HMI-04 — HMI CR | FS-HMI-04 | OQ `CRC-OQ-HMI-CR-01` |
| DS-BIO-53 | Cat-5 SDLC SOP | `CRC-SOP-IT-CAT5-001` | Custom | FS-DEV-01 — Cat-5 SDLC | FS-DEV-01 | (governance) |
| DS-BIO-54 | Source Repo + Branch Protection | `git.crocus.local/bioprocess/orchestrator`; 1+ reviewer + green CI + Sigstore-signed | Custom | FS-DEV-02 — repo controls | FS-DEV-02 | (CI) |
| DS-BIO-55 | Coverage Gate (safety/*) | < 95% breaks CI | Custom | FS-DEV-03 — coverage | FS-DEV-03 | (CI) |
| DS-BIO-56 | CI Static-Analysis | Ruff + mypy --strict + Bandit (Python); Trivy (containers); critical findings break build | Custom | FS-DEV-04 — static analysis | FS-DEV-04 | (CI) |
| DS-BIO-57 | Container Image Signing | cosign-signed against `crocus-sigstore-pubkey-2026q2`; runtime verifies | Custom | FS-DEV-05 — cosign | FS-DEV-05 | (CI) + OQ `CRC-OQ-COSIGN-01` |
| DS-BIO-58 | Release Manifest `manifest.yaml` Schema | `release_notes, fs_ds_deltas, regression_summary, security_scan_path, cr_id` | Custom | FS-DEV-06 — manifest | FS-DEV-06 | (CI) |
| DS-BIO-59 | Determinism Harness | pin random seed; 1000× canonical input; bitwise reproducibility verified; IEEE-754 round-mode pin via `numpy.errstate` | Custom | FS-DEV-07 — determinism | FS-DEV-07 | OQ `CRC-OQ-DETERMINISM-01` |
| DS-BIO-60 | Container CVE Gate | Trivy + Snyk Container; HIGH/CRITICAL CVE blocks promotion | Custom | FS-DEV-08 — CVE gate | FS-DEV-08 | (CI) |
| DS-BIO-61 | `audit_events` Schema | `actor_id, action, old_value, new_value, reason, timestamp_ptp, record_hash` ALCOA+ | Custom | FS-AUD-01 / FS-DI-01 — ALCOA+ | FS-AUD-01, FS-DI-01 | OQ `CRC-OQ-AUDIT-SCHEMA-01` |
| DS-BIO-62 | Audit RBAC | `app_role` INSERT/SELECT only; admin via break-glass with QA witness | Custom | FS-AUD-02 — RBAC | FS-AUD-02 | OQ `CRC-OQ-AUDIT-RBAC-01` |
| DS-BIO-63 | Perspective `Audit Trail Review` | filterable; PDF/A-3 + JSONL signed export | Custom | FS-AUD-03 — review view | FS-AUD-03 | OQ `CRC-OQ-AUDIT-VIEW-01` |
| DS-BIO-64 | `audit_events_archive` | S3 Object-Lock Compliance Mode + cross-region replication; 25 y | Custom | FS-AUD-04 — retention | FS-AUD-04 | (governance) |
| DS-BIO-65 | Control-Action Reconstruction Audit | `input_snapshot_uri` S3 reference on every decision row | Custom | FS-AUD-05 — reconstruction | FS-AUD-05 | OQ `OQ-AUD-RECONSTRUCT-01` |
| DS-BIO-66 | `/sop/` SharePoint Library | annual review workflow | Custom | FS-PART11-01 — § 11.10(a) | FS-PART11-01 | PR-01 |
| DS-BIO-67 | AD Kerberos + MFA Yubikey | enforced; service accounts mTLS-only | Custom | FS-PART11-02 — § 11.10(d) | FS-PART11-02 | OQ `CRC-OQ-AUTHN-01` |
| DS-BIO-68 | E-Signature Meaning Enum | `authorship, review, approval, release, retirement, verification`; role-matrix SoD denial | Custom | FS-PART11-04 — § 11.50 + SoD | FS-PART11-04 | OQ `CRC-OQ-ESIG-01` |
| DS-BIO-69 | E-Signature Payload Hash | SHA-256(record); edit invalidates; tampered flagged on read | Custom | FS-PART11-05 — § 11.70 | FS-PART11-05 | OQ `CRC-OQ-ESIG-HASH-01` |
| DS-BIO-70 | AD HR-Derived Feed + ID-Reuse Block | enforced at provisioning | Custom | FS-PART11-06 — § 11.100 | FS-PART11-06 | OQ `CRC-OQ-HRFEED-01` |
| DS-BIO-71 | Kerberos Fresh Ticket Max-Age | 5 min at sign-off | Custom | FS-PART11-07 — § 11.200 | FS-PART11-07 | OQ `CRC-OQ-KRB-FRESH-01` |
| DS-BIO-72 | AD Password Policy | ≥ 14 chars + complexity + 90-d rotation + MFA | Custom | FS-PART11-08 — § 11.300 | FS-PART11-08 | (governance) |
| DS-BIO-73 | DB Constraint actor_id NOT NULL | enforced | Custom | FS-DI-01 — attribution | FS-DI-01 | OQ `CRC-OQ-AUDIT-ATTRIB-01` |
| DS-BIO-74 | Export PDF/A-3 + JSON / CSV | OQ-validated | Custom | FS-DI-02 — export | FS-DI-02 | OQ `CRC-OQ-EXPORT-01` |
| DS-BIO-75 | PTP Timestamps from DCS/PLC | retroactive entries flagged with `retroactive_reason` | Custom | FS-DI-03 — PTP | FS-DI-03 | OQ `CRC-OQ-PTP-AUDIT-01` |
| DS-BIO-76 | InfluxDB Point-Write Only | corrections recorded as new annotated tags; PAT raw frames archived to S3 | Custom | FS-DI-04 — point-write | FS-DI-04 | OQ `CRC-OQ-INFLUX-IMMUT-01` |
| DS-BIO-77 | OQ Math Regression Dataset | feed-control + Kalman-filter + Hotelling math | Custom | FS-DI-05 — math regression | FS-DI-05 | OQ `CRC-OQ-MATH-01` |
| DS-BIO-78 | `CompletenessChecker` + Archive-Query API | metadata completeness validated; retrievable ≤ 1 BD | Custom | FS-DI-06 — retrieval | FS-DI-06 | OQ `CRC-OQ-INSP-01` |
| DS-BIO-79 | `BioreactorConfigMatrix` Table | per-config parameters (Sartorius STR / Cytiva XDR / Thermo HyPerforma / ABEC CSTR / Pall Allegro); EFFECTIVE recipe pins `bioreactor_config_id` | Custom | FS-CFG-01 — config matrix | FS-CFG-01 | OQ `CRC-OQ-CFG-MATRIX-01` |
| DS-BIO-80 | Config-Envelope Enforcement | recipe-load + runtime; cross-config leak → `CONFIG_ENVELOPE_LEAKAGE` | Custom | FS-CFG-02 — envelope enforcement | FS-CFG-02 | OQ `CRC-OQ-CFG-ENV-01` |
| DS-BIO-81 | Single-Use Bag Scan | barcode at batch start (bag-id + manufacturer + lot + expiry); verified vs Watson LIMS | Custom | FS-CFG-03 — single-use scan | FS-CFG-03 | OQ `CRC-OQ-SINGLEUSE-01` |
| DS-BIO-82 | Config-Changeover CR Template `CR-CFG-CHANGEOVER` | revalidation scope per impact assessment | Custom | FS-CFG-04 — changeover | FS-CFG-04 | (CR system) |
| DS-BIO-83 | `AtmpIsolationGuard` | 1 ATMP patient batch per train; interlock on shared resource access; violation → `ATMP_CROSSOVER_RISK` critical deviation | Custom | FS-ATMP-01 — isolation | FS-ATMP-01 | OQ `CRC-OQ-ATMP-ISO-01` |
| DS-BIO-84 | Donor-Traceability Schema | `{donor_id_deidentified, tissue_bank_ref, donor_lot}`; flows to PAS-X + Watson LIMS | Custom | FS-ATMP-02 — donor traceability | FS-ATMP-02 | OQ `CRC-OQ-ATMP-DONOR-01` |
| DS-BIO-85 | `Usp1043MaterialCheck` | queries Watson LIMS for ancillary-material qualification + expiry; non-qual blocks start | Custom | FS-ATMP-03 — USP <1043> | FS-ATMP-03 | OQ `CRC-OQ-USP1043-01` |
| DS-BIO-86 | ATMP QP Review Flag | `requires_qp_review=true`; PAS-X routes to QP queue | Custom | FS-ATMP-04 — QP review | FS-ATMP-04 | OQ `CRC-OQ-ATMP-QP-01` |
| DS-BIO-87 | PAS-X Recipe Fetcher | `https://pasx.crocus.local/api/v1/recipes/{id}/effective` mTLS cert `crocus-bioscada-2026q2` | Custom | FS-INT-MES-01 — recipe fetch | FS-INT-MES-01 | OQ `CRC-OQ-MES-01` |
| DS-BIO-88 | Batch Reporter | `POST /api/v1/batches` idempotent on `batchId`; within 30 min | Custom | FS-INT-MES-02 — batch report | FS-INT-MES-02 | OQ `CRC-OQ-BATCH-RPT-01` |
| DS-BIO-89 | DeviationCreator → MasterControl | `POST /api/v2/deviations` idempotent on `alarmId`; retry 1/5/30 s | Custom | FS-INT-EQMS-01 — eQMS | FS-INT-EQMS-01 | OQ `CRC-OQ-EQMS-01` |
| DS-BIO-90 | OPC UA Cert Rotation | annual via cert-manager | Custom | FS-INT-PAT-01 — cert rotation | FS-INT-PAT-01 | (cert-manager) |
| DS-BIO-91 | Aspen IP.21 Tag Stream | OPC HDA / UA; Ignition Tag Historian store-and-forward at gateway; lossless verified at OQ | Custom | FS-INT-HIST-01 — Aspen | FS-INT-HIST-01 | OQ `CRC-OQ-ASPEN-01` |
| DS-BIO-92 | Watson LIMS REST | `GET /materials/{lot}/status` (only `QC_RELEASED` accepted); `GET /donors/{deidentified_id}` | Custom | FS-INT-LIMS-01 — LIMS | FS-INT-LIMS-01 | OQ `CRC-OQ-LIMS-01` |
| DS-BIO-93 | BMS OPC UA | clean-steam P + WFI/PW availability + HVAC dP; loss → `UTILITY_LOSS_<resource>` and safe unit op | Custom | FS-INT-BMS-01 — BMS | FS-INT-BMS-01 | OQ `CRC-OQ-BMS-01` |
| DS-BIO-94 | AD Groups Consumed | `BioSCADA-Operator, BioSCADA-SeniorOperator, BioSCADA-RecipeAuthor, BioSCADA-RecipeApprover, BioSCADA-Chemometrician, BioSCADA-OrchAuthor, BioSCADA-CSV-Reviewer, BioSCADA-Auditor` | Custom | FS-INT-AD-01 — AD groups | FS-INT-AD-01 | OQ `CRC-OQ-AD-GROUPS-01` |
| DS-BIO-95 | Control-Loop Latency SLO | Prometheus histogram `control_loop_latency_seconds`; P95 ≤ 0.5 s | Custom | FS-PERF-01 — control-loop SLO | FS-PERF-01 | OQ `CRC-OQ-CTRL-LOOP-01` |
| DS-BIO-96 | OQ Stress Run | ≥ 1 Hz across CQA/CPP/PAT for 60 days; dashboard `CRC-GR-LOG-RATE` | Custom | FS-PERF-02 — stress run | FS-PERF-02 | OQ `CRC-OQ-STRESS-01` |
| DS-BIO-97 | HMI Synthetic Monitoring | P95 SLOs tracked | Custom | FS-PERF-03 — HMI SLO | FS-PERF-03 | OQ `CRC-OQ-HMI-SYNTH-01` |
| DS-BIO-98 | Availability Target | ≥ 99.5% monthly; maintenance windows logged | Custom | FS-AV-01 — availability | FS-AV-01 | (governance) |
| DS-BIO-99 | Nightly Backup | Postgres dump + InfluxDB → S3 cross-region replication; integrity-verified | Custom | FS-BAK-01 — nightly backup | FS-BAK-01 | OQ `CRC-OQ-BAK-NIGHTLY-01` |
| DS-BIO-100 | Restore-Test Script `restore_test.sh` | quarterly; QA witness sign-off | Custom | FS-BAK-02 — restore test | FS-BAK-02 | PR-01 |
| DS-BIO-101 | DR Site RTO + Lag | RTO ≤ 4 h; replication lag ≤ 1 min monitored | Custom | FS-BAK-03 — DR | FS-BAK-03 | OQ `CRC-OQ-DR-01` |
| DS-BIO-102 | Break-Glass Admin | sealed in Vault with split knowledge | Custom | FS-SEC-01 — break-glass | FS-SEC-01 | OQ `CRC-OQ-BREAKGLASS-01` |
| DS-BIO-103 | TLS Policy | TLS 1.2+ minimum; mTLS HMI ↔ Gateway and Gateway ↔ PLC where supported | Custom | FS-SEC-02 — TLS | FS-SEC-02 | OQ `CRC-OQ-TLS-01` |
| DS-BIO-104 | Tenable Nessus Monthly Scan | criticals SLA 30 d | Custom | FS-SEC-03 — vuln scan | FS-SEC-03 | (governance) |
| DS-BIO-105 | Windows GPO Removable-Media Block | vendor-approved engineering use via signed CR | Custom | FS-SEC-04 — removable media | FS-SEC-04 | OQ `CRC-OQ-USB-01` |
| DS-BIO-106 | Cornerstone LMS Curriculum | `CRC-CURR-BIOSCADA-<role>-v1`; production access gated by completion | Custom | FS-TRN-01 — LMS gate | FS-TRN-01 | (governance) |
| DS-BIO-107 | Annual Refresher `BIOSCADA-2026-ANNUAL` | ICH Q13 + EU GMP Annex 2/1 + ATMP updates | Custom | FS-TRN-02 — refresher | FS-TRN-02 | (governance) |
| DS-BIO-108 | Periodic-Review Template | `CRC-PR-BIOSCADA-YYYYMMDD` covers config drift + code-release register + audit-trail review + alarm trends + control-strategy verification + PAT-model performance + ATMP coverage | Custom | FS-PR-01 — periodic review | FS-PR-01 | PR-01 |
| DS-BIO-109 | Variation-Tracking Gate | prevents EFFECTIVE promotion if `variation_pending=true` | Custom | FS-PR-02 — variation gate | FS-PR-02 | OQ `CRC-OQ-VAR-GATE-01` |
| DS-BIO-110 | AD Conditional Access `OT-SCADA Conditional Access` | MFA at HMI session start; named-location restriction to plant network; SIEM → Splunk `gxp-authn`; CyberArk PAM break-glass | Custom | FS-XSYS-AD-01 | FS-XSYS-AD-01 | OQ `CRC-OQ-CONDACC-01` |
| DS-BIO-111 | Veeam Backup | App-aware MS SQL VSS for SCADA historian DB; tier T2; RPO ≤ 24 h; RTO ≤ 24 BH; S3 Compliance Mode + LTO-9 monthly | Custom | FS-XSYS-BAK-01 | FS-XSYS-BAK-01 | OQ `CRC-OQ-VEEAM-01` |

---

## 5. Workflow + Business-Rule Design

### 5.1 ISA-88 PhaseStateMachine Workflow

**States:** INOCULATION → EXPONENTIAL_GROWTH → STEADY_STATE_PERFUSION → HARVEST_DECISION → HARVEST_BLEED → CAMPAIGN_END (with CIP / SIP as separate state branches).

| Transition | Entry condition | Exit condition | Required signatures |
|---|---|---|---|
| `_initial_ → INOCULATION` | recipe EFFECTIVE + bioreactor config validated + single-use scan OK | inoculum delivered | Operator `authorship` |
| INOCULATION → EXPONENTIAL_GROWTH | viable-cell density threshold (recipe) | growth rate band achieved | (system) |
| EXPONENTIAL → STEADY_STATE_PERFUSION | target VCD reached | PerfusionController active | Senior Operator `verification` |
| STEADY_STATE → HARVEST_DECISION | recipe `harvest_decision_rules` triggered | decision logged | Bioprocess Engineer `review` |
| HARVEST_DECISION → HARVEST_BLEED | decision = HARVEST | bleed complete | Senior Operator `release` |
| HARVEST_BLEED → CAMPAIGN_END | campaign duration reached | batch report posted | Bioprocess Engineer `release` |
| any → CIP | maintenance scheduled | CIP complete | Senior Operator `verification` |
| any → SIP | sterilization needed | SIP complete | Senior Operator `verification` |
| out-of-envelope | recipe band breach | dual-sign + snapshot pointer | Op + Senior Op `verification` |

### 5.2 Recipe-Lifecycle Workflow (Postgres-enforced)

| Transition | Required signatures | Resulting state |
|---|---|---|
| DRAFT → REVIEW | Author `authorship` | REVIEW |
| REVIEW → APPROVED | Chemometrician + Bioprocess Engineer + CSV Reviewer `review` | APPROVED |
| APPROVED → EFFECTIVE | Head of Biologics Mfg + Head of QA `approval` (dual); variation gate clear | EFFECTIVE |
| EFFECTIVE → OBSOLETE | Biologics Mfg `retirement` | OBSOLETE |

### 5.3 PAT-Loss Safe-State Decision Rules

```
PAT instrument quality < GOOD_LOCAL_OVERRIDE OR sustained loss > recipe_dwell_min
     │
     ▼
PatLossHandler activates
     ├── Open-loop feed schedule (recipe-defined fallback)
     ├── APC demotion (PerfusionAuthorityMatrix downgrade)
     └── Deviation auto-create (MasterControl)
```

### 5.4 ATMP Mode Business Rules (FS-ATMP-01..04)

- **One ATMP patient batch per train** — `AtmpIsolationGuard` interlocks shared-resource access; violation → critical deviation
- **Donor metadata captured at start** — de-identified ID + tissue-bank ref + donor lot; PII isolated at storage boundary (KMS-encrypted)
- **USP <1043> material check** — non-qualified / expired ancillary blocks batch start
- **QP review flag** — all ATMP batches routed to QP queue

### 5.5 Single-Use vs Stainless Configuration Rules

Configuration-changeover requires `CR-CFG-CHANGEOVER` with revalidation scope per impact assessment. Cross-config leakage at runtime → blocking deviation.

### 5.6 Alarm-Handling (ISA-18.2)

Per `alarm_rationalisation.yaml` (DS-BIO-44). Critical alarms require reason ≥ 10; unack > T_escalate → SMS + email. Alarm flood → shelving per ISA-18.2; SIS alarms isolated on DeltaV SIS partition with one-way mirror.

---

## 6. Role-Permission Matrix Design

| AD Group | View HMI | Ack alarm | Author recipe | Approve recipe | Sign override | Approve PAT model | Approve ATMP | Audit export | Admin |
|---|---|---|---|---|---|---|---|---|---|
| `BioSCADA-Operator` | Y | WARN | — | — | initiate | — | — | — | — |
| `BioSCADA-SeniorOperator` | Y | CRIT | — | — | countersign | — | — | — | — |
| `BioSCADA-RecipeAuthor` | Y | — | Y | — | — | — | — | — | — |
| `BioSCADA-RecipeApprover` | Y | — | review | approve | — | — | — | — | — |
| `BioSCADA-Chemometrician` | Y | — | — | — | — | author + review | — | — | — |
| `BioSCADA-OrchAuthor` | Y | — | — | — | — | — | — | — | — |
| `BioSCADA-CSV-Reviewer` | Y (RO) | — | — | review (CSV) | — | review | — | Y | — |
| `BioSCADA-Auditor` | Y (RO) | — | — | — | — | — | — | Y | — |
| Process Sciences | Y | — | — | — | — | review | — | — | — |
| QA | Y | — | — | approve | — | approve | approve | Y | — |
| Break-glass DBA (vaulted) | — | — | — | — | — | — | — | — | DB-only |

FS-IDs traced: FS-INT-AD-01, FS-PART11-04 (SoD), FS-FEED-03 (override), FS-PAT-07 (PAT approval), FS-ATMP-04 (QP review).

---

## 7. Integration Design

### 7.1 IF-PASX-RECIPE-IN / IF-PASX-BATCH-OUT

- **Endpoints:** `GET https://pasx.crocus.local/api/v1/recipes/{id}/effective`; `POST .../api/v1/batches`
- **Protocol:** mTLS `crocus-bioscada-2026q2`
- **Schemas:** SHA-256 + version (recipe in); profile + alarms + signatures + PAT-trace (batch out)
- **Idempotency:** `batchId`
- **Retry:** 1/5/30 s
- **FS-IDs:** FS-INT-MES-01/02

### 7.2 IF-EQMS-DEV-OUT

- **Endpoint:** `POST https://eqms.crocus.local/api/v2/deviations`
- **Idempotency:** `alarmId`
- **Retry:** 1/5/30 s; escalation to on-call
- **FS-IDs:** FS-INT-EQMS-01

### 7.3 IF-PAT-IN (PAT bus)

- **Protocol:** OPC UA mTLS per instrument; annual cert rotation
- **Quality gate:** `PatQualityGate` consumes tag-quality attribute
- **FS-IDs:** FS-INT-PAT-01

### 7.4 IF-HIST-OUT (Aspen IP.21)

- **Protocol:** OPC HDA / OPC UA + Ignition store-and-forward buffer
- **FS-IDs:** FS-INT-HIST-01

### 7.5 IF-LIMS-IN (Watson LIMS)

- **Endpoint:** `GET /materials/{lot}/status`, `GET /donors/{deidentified_id}` over mTLS
- **Acceptance:** only `QC_RELEASED`
- **FS-IDs:** FS-INT-LIMS-01

### 7.6 IF-BMS-IN

- **Protocol:** OPC UA mTLS — utility-status tags
- **Behaviour:** loss raises `UTILITY_LOSS_<resource>` + safes unit op
- **FS-IDs:** FS-INT-BMS-01

### 7.7 IF-AD-AUTH

- **Protocol:** LDAPS / Kerberos `crocus.local`; AD groups per DS-BIO-94; CyberArk PAM for break-glass
- **FS-IDs:** FS-INT-AD-01, FS-XSYS-AD-01

### 7.8 Integration Risk Register

| Interface | Risk | Mitigation |
|---|---|---|
| IF-PASX | cert expiry | cert-manager 365-d + 30-d alert |
| IF-PAT | instrument firmware divergence | vendor-coordinated CR + signal-quality monitor |
| IF-LIMS | ATMP donor metadata leak | de-identification at boundary + S3 KMS |
| IF-AD | outage | local OT-cached credentials 24 h |
| IF-HIST | Aspen ingest backpressure during 60-d run | store-and-forward + circuit breaker |

---

## 8. Site-Deployed Components — Mini-SDS for Python Orchestrator (Cat 5)

### 8.1 Software Architecture

```
   ┌────────────────────────────────────────────────────────────┐
   │  Site Python Orchestrator (Python 3.11, ~6.5k LOC)           │
   │  ┌──────────────────────────┐  ┌─────────────────────────┐   │
   │  │  recipe/                  │  │  phase/                  │   │
   │  │  - RecipeApi              │  │  - PhaseStateMachine     │   │
   │  │  - RecipeReceiver         │  │  - PhaseRules            │   │
   │  └──────────────────────────┘  └─────────────────────────┘   │
   │  ┌──────────────────────────┐  ┌─────────────────────────┐   │
   │  │  feed/                    │  │  pat/                    │   │
   │  │  - GlucoseFeedController  │  │  - PatQualityGate        │   │
   │  │  - PerfusionController    │  │  - PatLossHandler        │   │
   │  │  - BleedRateController    │  │  - PatPerformanceMonitor │   │
   │  │  - FoulingPredictor       │  │  - SoftSensor (Kalman)   │   │
   │  └──────────────────────────┘  └─────────────────────────┘   │
   │  ┌──────────────────────────┐  ┌─────────────────────────┐   │
   │  │  atmp/                    │  │  config/                 │   │
   │  │  - AtmpIsolationGuard     │  │  - BioreactorConfigMatrix│   │
   │  │  - Usp1043MaterialCheck   │  │  - SingleUseScan         │   │
   │  └──────────────────────────┘  └─────────────────────────┘   │
   │  ┌──────────────────────────────────────────────────────┐    │
   │  │  safety/ - SafeStateEnter / PumpCrossCheck            │    │
   │  └──────────────────────────────────────────────────────┘    │
   └────────────────────────────────────────────────────────────┘
```

Stack: Python 3.11; OpenShift 4.14 deployment; MLflow PAT-model registry; sklearn / numpy / scipy for PAT compute; psycopg2 for Postgres; influxdb-client for InfluxDB.

### 8.2 Module Decomposition

| Module ID | Module name | Responsibility | Interface | Dependencies | GxP class |
|---|---|---|---|---|---|
| MS-01 | `recipe.RecipeApi` | REST endpoints | `GET /recipes/effective`, `POST /recipes/transition` | Postgres recipe_versions | R1 |
| MS-02 | `recipe.RecipeReceiver` | PAS-X recipe fetch + SHA-256 validation | scheduled | PAS-X endpoint | R1 |
| MS-03 | `phase.PhaseStateMachine` | ISA-88 phase state machine | transition() | phase_rules.yaml | R1 |
| MS-04 | `phase.PhaseRules` | entry/exit condition evaluator | check() | tag subs | R1 |
| MS-05 | `feed.GlucoseFeedController` | Raman PLS → pump SP | tick callback | PAT bus | R1 |
| MS-06 | `feed.PerfusionController` | Kalman fusion → ATF-rate SP | tick callback | PAT bus + ATF | R1 |
| MS-07 | `feed.BleedRateController` | VCD-target → bleed SP | tick callback | VCD | R1 |
| MS-08 | `feed.FoulingPredictor` | TMP+flux trend → maintenance alarm | hourly callback | ATF telemetry | R2 |
| MS-09 | `pat.PatQualityGate` | OPC UA quality consumption + alarms | tag-change | OPC UA | R1 |
| MS-10 | `pat.PatLossHandler` | safe-state on PAT loss | event-driven | safe-state writer | R1 |
| MS-11 | `pat.PatPerformanceMonitor` | rolling residuals + Hotelling T² + Q | scheduled | InfluxDB | R1 |
| MS-12 | `pat.SoftSensor` | inferential VCD / titer via Kalman | tick | capacitance + VCD + Raman | R1 |
| MS-13 | `atmp.AtmpIsolationGuard` | one ATMP batch/train interlock | API guard | shared-resource model | R1 |
| MS-14 | `atmp.Usp1043MaterialCheck` | LIMS check before start | API | Watson LIMS | R1 |
| MS-15 | `config.BioreactorConfigMatrix` | per-config envelope enforcement | validate() | Postgres | R1 |
| MS-16 | `config.SingleUseScan` | barcode at start | API | LIMS | R1 |
| MS-17 | `safety.SafeStateEnter` | writes safe-state tag setpoints | command | tag writer | R1 |
| MS-18 | `safety.PumpCrossCheck` | rotation vs flow integrity | 5-s callback | tag sub | R1 |

### 8.3 Data Model

| Table | Key columns | Constraints | Retention |
|---|---|---|---|
| `recipe_versions` | recipe_id, version, status, sha256, signatures (JSONB) | trigger blocks UPDATE/DELETE on EFFECTIVE | indefinite |
| `master_recipe / site_recipe / control_recipe` | per ISA-88 | FK pinned | indefinite |
| `phase_events` | phase_id, batch_id, ts_ptp, entry/exit snapshot, signing_user | append-only | 25 y |
| `audit_events` | per FS-AUD-01 | append-only via role GRANT | 25 y |
| `override_events` | override_id, op_id, senior_id, reason, ccs_doc_ref, input_snapshot_uri | reason CHECK len ≥ 10 | 25 y |
| `decision_events` | decision_id, ts_ptp, code_release, model_version, input_snapshot_uri | NOT NULL on all | 25 y |
| `pat_model_versions` | model_id, version, state, mlflow_run_id | MLflow-tracked | indefinite |
| `bioreactor_config_matrix` | config_id, vendor, parameters JSONB | (CHECK on parameters) | indefinite |
| `atmp_batches` | batch_id, donor_id_deidentified, isolation_train | KMS-encrypted at-rest (donor fields) | 25 y |
| `usp1043_materials` | lot_id, qualification_record, expiry | NOT NULL | 25 y |
| `pump_crosscheck_events` | event_id, batch_id, rotation, flow, mismatch_pct, ts_ptp | NOT NULL | 25 y |

### 8.4 Algorithm + Calculation Design

| Algorithm | Inputs | Output | Procedure | Numerical-precision note | Reference |
|---|---|---|---|---|---|
| Raman PLS prediction → glucose setpoint | Raman spectrum (recipe-pinned λ-window) | glucose_sp_g_L | recipe-pinned MLflow PLS model; `predict(X)` | float32; IEEE-754 round-mode pinned via `numpy.errstate` | ASTM E2476 / vendor model |
| Kalman fusion (capacitance + VCD) | sensor stream | fused VCD estimate | linear KF with recipe-defined Q, R matrices; sensor-loss demotes authority | float64; deterministic | site |
| Pump cross-check | rotation, flow | mismatch_pct, alarm_bool | `|rotation × cal − flow|/flow`; threshold ≥ 5% sustained > 60 s | float64 | site |
| Hotelling T² + Q-statistic | residual matrix | T², Q + alarm | PCA-projected per recipe model; thresholds recipe-defined | float64 | ASTM E2476 |
| Residual rolling mean / σ | residual series | mean, σ | Welford algorithm | float64 | (Welford 1962) |
| TMP fouling precursor | TMP + flux series | precursor_alarm | regression slope > threshold | float64 | site |
| Reference-method delta logging | LIMS HPLC vs PAT prediction | delta + trend | per-window comparison | float64 | site |

Determinism harness (FS-DEV-07 / DS-BIO-59): 1000× canonical input replay bitwise-identical.

### 8.5 Interface + API Design

| Endpoint | Method | AuthN | Request | Response | Idempotency | Audit |
|---|---|---|---|---|---|---|
| `/api/recipes/effective` | GET | Kerberos | `recipe_id` | RecipeVersion JSON | safe | `recipe_fetch` |
| `/api/recipes/transition` | POST | Kerberos + signed JWT | `{recordHash, signerId, meaning}` | new state | by recordHash | `recipe_transition` |
| `/api/phases/{phase_id}/transition` | POST | Kerberos | `{from, to, reason}` | phase_event_id | by snapshot ts | `phase_transition` |
| `/api/override` | POST | Kerberos + Op/Senior dual | `{batch_id, reason, ccs_doc_ref}` | override_id | by batch_id + ts | `override_create` |
| `/api/pat/models/{id}/transition` | POST | Kerberos Chemometrician/QA | `{newState, signature}` | sig_id | by record_hash | `pat_model_transition` |
| `/api/atmp/start` | POST | Kerberos + QP review | `{donor_id_deidentified, tissue_bank_ref}` | batch_id | by donor + ts | `atmp_start` |

### 8.6 Security Design

- **AuthN:** AD Kerberos + Yubikey MFA; service accounts mTLS-only via Vault
- **AuthZ:** AD-group → role per § 6; SoD policy denies conflicting roles
- **Secrets:** HashiCorp Vault; CyberArk PAM for break-glass
- **Transport:** TLS 1.2+; mTLS for all integrations
- **Donor PII (ATMP):** S3 KMS encryption + de-identification at boundary
- **Audit-event taxonomy:** comprehensive — `recipe_*`, `phase_*`, `pat_model_*`, `override_*`, `atmp_*`, `signature_emit`, `module_deploy`

### 8.7 Deployment Architecture

- **Packaging:** container images signed via cosign against `crocus-sigstore-pubkey-2026q2`
- **Topology:** OpenShift 4.14 namespace `bioscada-prod`, 3 replicas + DR; PodDisruptionBudget min=2; HPA disabled (deterministic load)
- **Observability:** Prometheus + Grafana `CRC-GR-BIOSCADA-RUNTIME`; Splunk `gxp-bioscada`
- **DR:** geo-paired `bioscada-dr`; RTO ≤ 4 h; replication lag ≤ 1 min

### 8.8 Module Specification Table

| Module ID | Source location | Unit-test ref |
|---|---|---|
| MS-01..MS-18 | `git.crocus.local/bioprocess/orchestrator/{recipe,phase,feed,pat,atmp,config,safety}/*.py` | `<repo>/tests/unit/test_<module>.py` (coverage ≥ 95% safety/*) |

Full Module Specifications: `CRC-MS-BIOSCADA-NN` (downstream).

---

## 9. References

### US
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .68, .184, .192
- FDA CSA (final, February 2026)
- FDA PAT (2004)
- FDA Q13 (2024)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EU GMP Annex 1 (2022 revision)
- EU GMP Annex 2 (ATMP)
- EU GMP Annex 15

### DACH
- AMWHV
- BSI IT-Grundschutz baseline

### International
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE Baseline Guide *Biopharmaceutical Manufacturing Facilities*
- ISPE GAMP GPG *PAT*
- ICH Q9(R1); ICH Q11; ICH Q12; ICH Q13
- USP <1043>; ATMP Guidelines
- ISA-88 Part 1 + Part 2; ISA-95 Part 1; ISA-101; ISA-18.2
- ASTM E2476
- IEC 61131-3; IEC 61511; IEC 61508
- PIC/S PI 041
- ISO/IEC 27001:2022

### Vendor
- Inductive Automation — *Ignition 8.3 Reference*
- Emerson — *DeltaV v15.3 Reference + SIS Safety Manual*
- Sartorius — *Biostat STR / BioPAT Spectro Reference*
- Cytiva — *XDR Reference*
- Thermo — *HyPerforma DynaDrive Reference*
- Kaiser — *RamanRxn4 Manual*
- Hamilton — *Incyte Reference*
- Repligen — *XCell ATF Manual*
- Watson-Marlow — *Quantum Pump Reference*

### Site
- `CRC-URS-BIOSCADA-001` v1.2 (informational)
- `CRC-FS-BIOSCADA-001` v1.2 (parent)
- `CRC-SOP-IT-CAT5-001` (Cat-5 SDLC)
- `PAT-MODEL-LCM-001` (PAT-model lifecycle)
- `CRC-SOP-CR-001` (change control)
- `CRC-PR-BIOSCADA-YYYYMMDD` (periodic-review template)

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-BIO-01 | FS-PLAT-01 |
| DS-BIO-02 | FS-PLAT-01 |
| DS-BIO-03 | FS-PLAT-01 |
| DS-BIO-04 | FS-PLAT-01 |
| DS-BIO-05 | FS-PLAT-02 |
| DS-BIO-06 | FS-PLAT-02 |
| DS-BIO-07 | FS-PLAT-03 |
| DS-BIO-08 | FS-PLAT-04 |
| DS-BIO-09 | FS-PLAT-05 |
| DS-BIO-10 | FS-REC-01 |
| DS-BIO-11 | FS-REC-02 |
| DS-BIO-12 | FS-REC-03 |
| DS-BIO-13 | FS-REC-04 |
| DS-BIO-14 | FS-REC-05 |
| DS-BIO-15 | FS-REC-06 |
| DS-BIO-16 | FS-REC-07 / FS-INT-MES-01 |
| DS-BIO-17 | FS-REC-08 |
| DS-BIO-18 | FS-REC-09 |
| DS-BIO-19 | FS-PHASE-01 |
| DS-BIO-20 | FS-PHASE-02 |
| DS-BIO-21 | FS-PHASE-03 |
| DS-BIO-22 | FS-PHASE-04 |
| DS-BIO-23 | FS-PHASE-05 |
| DS-BIO-24 | FS-PHASE-06 |
| DS-BIO-25 | FS-FEED-01 |
| DS-BIO-26 | FS-FEED-02 |
| DS-BIO-27 | FS-FEED-03 |
| DS-BIO-28 | FS-FEED-04 |
| DS-BIO-29 | FS-FEED-05 |
| DS-BIO-30 | FS-FEED-06 |
| DS-BIO-31 | FS-PAT-01 / FS-INT-PAT-01 |
| DS-BIO-32 | FS-PAT-02 |
| DS-BIO-33 | FS-PAT-03 |
| DS-BIO-34 | FS-PAT-04 / FS-RUN-06 |
| DS-BIO-35 | FS-PAT-05 |
| DS-BIO-36 | FS-PAT-06 |
| DS-BIO-37 | FS-PAT-07 |
| DS-BIO-38 | FS-RUN-01 |
| DS-BIO-39 | FS-RUN-02 |
| DS-BIO-40 | FS-RUN-03 |
| DS-BIO-41 | FS-RUN-04 |
| DS-BIO-42 | FS-RUN-08 |
| DS-BIO-43 | FS-RUN-07 |
| DS-BIO-44 | FS-ALM-01 |
| DS-BIO-45 | FS-ALM-02 |
| DS-BIO-46 | FS-ALM-03 |
| DS-BIO-47 | FS-ALM-04 |
| DS-BIO-48 | FS-ALM-05 |
| DS-BIO-49 | FS-HMI-01 |
| DS-BIO-50 | FS-HMI-02 |
| DS-BIO-51 | FS-HMI-03 |
| DS-BIO-52 | FS-HMI-04 |
| DS-BIO-53 | FS-DEV-01 |
| DS-BIO-54 | FS-DEV-02 |
| DS-BIO-55 | FS-DEV-03 |
| DS-BIO-56 | FS-DEV-04 |
| DS-BIO-57 | FS-DEV-05 |
| DS-BIO-58 | FS-DEV-06 |
| DS-BIO-59 | FS-DEV-07 |
| DS-BIO-60 | FS-DEV-08 |
| DS-BIO-61 | FS-AUD-01 / FS-DI-01 |
| DS-BIO-62 | FS-AUD-02 |
| DS-BIO-63 | FS-AUD-03 |
| DS-BIO-64 | FS-AUD-04 |
| DS-BIO-65 | FS-AUD-05 |
| DS-BIO-66 | FS-PART11-01 |
| DS-BIO-67 | FS-PART11-02 / FS-PART11-03 |
| DS-BIO-68 | FS-PART11-04 |
| DS-BIO-69 | FS-PART11-05 |
| DS-BIO-70 | FS-PART11-06 |
| DS-BIO-71 | FS-PART11-07 |
| DS-BIO-72 | FS-PART11-08 |
| DS-BIO-73 | FS-DI-01 |
| DS-BIO-74 | FS-DI-02 |
| DS-BIO-75 | FS-DI-03 |
| DS-BIO-76 | FS-DI-04 |
| DS-BIO-77 | FS-DI-05 |
| DS-BIO-78 | FS-DI-06 |
| DS-BIO-79 | FS-CFG-01 |
| DS-BIO-80 | FS-CFG-02 |
| DS-BIO-81 | FS-CFG-03 |
| DS-BIO-82 | FS-CFG-04 |
| DS-BIO-83 | FS-ATMP-01 |
| DS-BIO-84 | FS-ATMP-02 |
| DS-BIO-85 | FS-ATMP-03 |
| DS-BIO-86 | FS-ATMP-04 |
| DS-BIO-87 | FS-INT-MES-01 |
| DS-BIO-88 | FS-INT-MES-02 |
| DS-BIO-89 | FS-INT-EQMS-01 |
| DS-BIO-90 | FS-INT-PAT-01 |
| DS-BIO-91 | FS-INT-HIST-01 |
| DS-BIO-92 | FS-INT-LIMS-01 |
| DS-BIO-93 | FS-INT-BMS-01 |
| DS-BIO-94 | FS-INT-AD-01 |
| DS-BIO-95 | FS-PERF-01 |
| DS-BIO-96 | FS-PERF-02 |
| DS-BIO-97 | FS-PERF-03 |
| DS-BIO-98 | FS-AV-01 |
| DS-BIO-99 | FS-BAK-01 |
| DS-BIO-100 | FS-BAK-02 |
| DS-BIO-101 | FS-BAK-03 |
| DS-BIO-102 | FS-SEC-01 |
| DS-BIO-103 | FS-SEC-02 |
| DS-BIO-104 | FS-SEC-03 |
| DS-BIO-105 | FS-SEC-04 |
| DS-BIO-106 | FS-TRN-01 |
| DS-BIO-107 | FS-TRN-02 |
| DS-BIO-108 | FS-PR-01 |
| DS-BIO-109 | FS-PR-02 |
| DS-BIO-110 | FS-XSYS-AD-01 |
| DS-BIO-111 | FS-XSYS-BAK-01 |
| MS-01..MS-18 | Cat-5 mini-SDS § 8.2 — Python Orchestrator; transitively traces FS-DEV-01..08 + FS-REC-* + FS-PHASE-* + FS-FEED-* + FS-PAT-* + FS-ATMP-* + FS-CFG-* |

---

## 11. Design-level Risk Register

Per § 2B.8 — design-stage risks. Formal RA in `CRC-RA-BIOSCADA-001` (synthetic).

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| DR-01 | Floating-point non-determinism across pod restarts | Medium | High | FS-DEV-07 + IEEE-754 round-mode pin + `decimal` for currency-class math (DS-BIO-59) |
| DR-02 | PAT-model-version-pin bypass (DS-BIO-33) | Low | Critical | FS-PAT-03 contract test in CI rejecting mismatched-version predictions |
| DR-03 | Cosign key rotation breaks runtime module load | Low | High | Paired-key transition window + monitoring; documented rotation procedure |
| DR-04 | Aspen IP.21 ingest backpressure during 60-d run | Medium | High | Store-and-forward buffer + circuit breaker (DS-BIO-91) |
| DR-05 | Single-use bag barcode scanner failure | Low | High | Manual entry with QA witness as fallback (signed) |
| DR-06 | ATMP donor metadata leak via misconfigured S3 KMS | Low | Critical | De-identification at boundary + S3 KMS + bucket-policy review |
| DR-07 | SIS event mirror creates write-back vector | Low | High | One-way only; SIS network isolated; firewall enforcement |
| DR-08 | OpenShift PodDisruptionBudget (min 2) breached during cluster maintenance | Low | High | Maintenance window + manual drain procedure |
| DR-09 | Kalman-filter divergence on noisy capacitance + VCD signals | Medium | Medium | Recipe-defined Q/R matrices + sensor-loss demotion (DS-BIO-26) |
| DR-10 | `AtmpIsolationGuard` interlock false-positive blocks legitimate batch | Low | Medium | Train-state model validated under PQ; override path with QA + QP dual-sign |
| DR-11 | USP <1043> material check (DS-BIO-85) miss when LIMS sync lags | Low | High | LIMS webhook complement + manual override with reason |
| DR-12 | `BioreactorConfigMatrix` (DS-BIO-79) parameter type mismatch on new config addition | Low | Medium | Schema validator + CR gate on matrix edits |
| DR-13 | MLflow PAT-model registry (DS-BIO-32) drift vs runtime loader | Low | High | Runtime loader verifies model_id + version + dossier_id at startup |
| DR-14 | OPC UA cert (annual rotation per DS-BIO-90) expires during 60-d run | Low | High | Mid-run rotation tested at OQ; pre-emptive renewal at 30 d to expiry |
| DR-15 | Reference-method delta logging (DS-BIO-36) misses calibration drift | Medium | Medium | Quarterly trend review + threshold tightening |
| DR-16 | Audit retention S3 Object-Lock in Governance instead of Compliance Mode | Low | Critical | IQ verification at bucket creation + annual recheck |
| DR-17 | `PerfusionAuthorityMatrix` (DS-BIO-26) demotion logic incorrect on multi-sensor partial loss | Medium | High | Authority-matrix unit tests + 1000× determinism replay |
| DR-18 | Variation gate (DS-BIO-109) bypass via manual recipe-version override | Low | High | API-level enforcement; manual override requires QA + RA dual-sign |
| DR-19 | Veeam VSS backup window collides with high-frequency PAT writes | Low | Medium | Backup scheduled outside PAT high-rate windows; monitored |
| DR-20 | AD Conditional Access named-location restriction blocks remote engineering session during emergency | Low | High | Pre-approved exception list + break-glass via CyberArk PAM |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
