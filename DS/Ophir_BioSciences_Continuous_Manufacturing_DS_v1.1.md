---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (Cat 4 / Tier T3)"
seed_corpus_basis:
  - "OPH-FS-CM-001 v1.2 (parent FS)"
  - "OPH-URS-CM-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd Edition) Category 4 — Configuration Specification conventions"
  - "21 CFR Part 11; 21 CFR Part 211"
  - "EU GMP Annex 11; Annex 15"
  - "ICH Q13 (Continuous Mfg); ICH Q14; ICH Q12; ICH Q8/Q9/Q10"
  - "FDA CSA (Feb 2026); ANSI/ISA-88; ANSI/ISA-95; IEC 61511 SIL 2"
  - "PIC/S PI 041"
parent_fs:
  document_number: OPH-FS-CM-001
  version: "1.2"
  file: "../../../FS_FDS/_generated/final/Ophir_BioSciences_Continuous_Manufacturing_FS_v1.3.md"
parent_urs:
  document_number: OPH-URS-CM-001
  version: "1.2"
  file: "../../../URS/_generated/final/Continuous_Manufacturing_Control_System__Ophir_BioSciences_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Continuous Manufacturing Control System — Site-Authored CM Orchestrator (Python + Ignition 8.3 + Allen-Bradley ControlLogix 5580)

**Document Number:** OPH-DS-CM-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** OPH-FS-CM-001 v1.2
**Parent URS:** OPH-URS-CM-001 v1.2 *(informational, transitive)*
**Site:** Ophir BioSciences (fictional)
**System Owner:** Continuous-Manufacturing Automation Lead
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (Ignition 8.3 SCADA + Allen-Bradley ControlLogix 5580 PLC platforms), with site-developed CM Orchestrator (Python) assessed as Cat 5 sub-component (mini-SDS in § 8)
**Project Mode:** Configuration project on commercial software products **Ignition 8.3** + **Allen-Bradley FactoryTalk / ControlLogix 5580** (GAMP 5 Category 4) with embedded Cat-5 site CM Orchestrator under hybrid governance.
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; EU GMP Annex 15; ICH Q13 (Continuous Mfg); ICH Q14 (Analytical Procedure); ICH Q12 (Lifecycle Management); ICH Q9(R1); ICH Q10; ICH Q8(R2); FDA CSA (Feb 2026); PIC/S PI 041; ANSI/ISA-88; ANSI/ISA-95; IEC 61511 SIL 2.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect — CM) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Continuous Mfg SME) | _____________ | _____________ | _____ |
| Reviewer (PAT Scientist) | _____________ | _____________ | _____ |
| Reviewer (Functional Safety Engineer) | _____________ | _____________ | _____ |
| Reviewer (Quality IT Lead) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs — ICH Q12) | _____________ | _____________ | _____ |
| Approver (Head of Continuous Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |
| Approver (Qualified Person) | _____________ | _____________ | _____ |

## Design Control

- **Document Number:** OPH-DS-CM-001
- **Version:** 1.1
- **Effective Date:** 2026-05-15 *(synthetic)*
- **Parent FS:** OPH-FS-CM-001 v1.2
- **Parent URS:** OPH-URS-CM-001 v1.2 *(informational)*
- **Site:** Ophir BioSciences
- **System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (Ignition + ControlLogix) with embedded Cat-5 CM Orchestrator
- **Project Mode:** Hybrid Cat 4 + Cat 5 — § 4–§ 7 CS rules; § 8 mini-SDS for Orchestrator
- **Regulatory Scope:** as above

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T3 from parent URS+FS pair. DS covers 83/83 FS-IDs from OPH-FS-CM-001 v1.2. No FS-IDs flagged vendor-internal — Ignition + ControlLogix configuration surfaces site-designable; SIL-2 safety partition embedded firmware vendor-validated, configuration of trip rules + diverter actuation is site-designed and covered here. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from OPH-FS-CM-001 and OPH-URS-CM-001. DS-specific terms:

| Term | Definition |
|---|---|
| Orchestrator | Site-authored Python service on OpenShift — recipe + state-of-control + RTRT + diverter decision logic |
| EC | Established Condition (ICH Q12) |
| APL | Analytical Procedure Lifecycle (ICH Q14) doc |
| RTRT | Real-Time Release Testing |
| RTD | Residence-Time Distribution (model) |
| Diverter | Pneumatic gate that diverts non-conforming material to quarantine |
| CSA | Computer Software Assurance (FDA Feb 2026) |
| LIW | Loss-In-Weight (feeder) |

---

## 1. Purpose

This DS specifies the technical design that satisfies the FS `OPH-FS-CM-001` v1.2. It records the Ignition 8.3 + ControlLogix 5580 + CM Orchestrator CI inventory; recipe / state-of-control / Q12-EC / Q13-batch-definition / Q14-APL / diversion / material-tracking / SDLC / audit workflow + business-rule design; role-permission matrix; per-interface integration design (PAS-X, MasterControl, Aspen IP.21, NIR/Raman/LIW/PSD PAT, AD); and a mini-SDS for the site Python Orchestrator. Controlling input to IQ / OQ / PQ / RTM `OPH-RTM-CM-001`.

## 2. Scope

**In scope.** Configuration of Ignition 8.3 Gateway cluster, Allen-Bradley ControlLogix 5580 safety PLC (SIL-2 partition), OpenShift 4.14 Orchestrator cluster (3 active + 1 DR), PostgreSQL 16, all integrations (PAS-X v3.2, MasterControl eQMS, Aspen IP.21, NIR / Raman / LIW + mass-flow / particle-size PAT, AD, HashiCorp Vault, PTP), diverter mechanism (pneumatic gate with SIL-2 trip), and CM Orchestrator (Cat-5 ~10k LOC).

**Out of scope.** Vendor-internal Ignition / FactoryTalk code; PLC firmware (vendor SDLC); physical compactor / mill / blender / tableter equipment; PAT instruments (separate URS/FS).

## 3. Architectural Overview

```
        ┌────────────────────────────────────────────────────────────┐
        │  AD/PKI │ PTP IEEE 1588 │ HashiCorp Vault                    │
        └────────────────────┬───────────────────────────────────────┘
                             │
   ┌─────────────────────────▼─────────────────────────────────────┐
   │  PAS-X v3.2 (recipe / batch context)                            │
   └───┬──────────────────────────────────────────────────┬─────────┘
       │ recipe + batch                                    │ batch report
       ▼                                                   ▲
   ┌────────────────────────────────────────────────────────────┐
   │  CM Orchestrator (Cat 5, Python) — OpenShift 4.14            │
   │  3 active + 1 DR replicas; HAProxy + PodAntiAffinity         │
   │  ┌───────────────────────────────────────────────────────┐   │
   │  │  Recipe engine (Q13 control strategy)                  │   │
   │  │  State-of-control + SPC (Western Electric + Nelson)    │   │
   │  │  PAT-fusion + RTRT decision                            │   │
   │  │  Material-tracking (RTD model)                         │   │
   │  │  Diverter command + actuator-health monitor            │   │
   │  │  EC-change gate (Q12) + APL gate (Q14)                 │   │
   │  │  QP override endpoint                                  │   │
   │  └───────────────────────────────────────────────────────┘   │
   └────────┬──────────────────────┬──────────────────────┬───────┘
            │                      │                       │
            ▼                      ▼                       ▼
        Ignition 8.3            PAT (OPC UA + REST)    ControlLogix 5580
        SCADA + phase           NIR / Raman / LIW /    safety PLC + diverter
        logic                   mass-flow / PSD        (SIL-2 partition)
            │                                              │
            ▼                                              ▼
        Aspen IP.21                                    SIS / safe-state
        historian                                      logic (SIL 2)
            │
            ▼
        MasterControl eQMS (deviation push)
```

Cluster design: 3 active replicas + 1 DR; HPA disabled (deterministic load); PodAntiAffinity across ≥ 2 fault domains; PostgreSQL 16 with patroni cluster; Ignition Gateway cluster mode.

---

## 4. Configuration Specification

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CM-01 | OpenShift Namespace + Replicas | `cm-prod` 3 active + 1 DR; DR cluster `cm-dr`; HAProxy + health-check | Custom | FS-PLAT-01 | FS-PLAT-01 | OQ `OPH-OQ-OS-REPL-01` |
| DS-CM-02 | Ignition Gateway N+1 Cluster | hot failover | Custom | FS-PLAT-01 | FS-PLAT-01 | OQ `OPH-OQ-IG-FAIL-01` |
| DS-CM-03 | UPS Hold (OpenShift nodes) | ≥ 30 min | Custom | FS-PLAT-02 | FS-PLAT-02 | IQ `OPH-IQ-UPS-01` |
| DS-CM-04 | ControlLogix Safety SAFE_STATE | safety functions revert to SAFE_STATE on power loss; diverter holds last position with SIL-2 fail-safe to REJECT | Custom | FS-PLAT-02 — safety SAFE_STATE | FS-PLAT-02 | OQ `OPH-OQ-SAFE-STATE-01` |
| DS-CM-05 | Process-Control VLAN | VLAN 521; no L3 route to office; firewalled at OT-DMZ | Custom | FS-PLAT-03 | FS-PLAT-03 | IQ `OPH-IQ-NET-01` |
| DS-CM-06 | Cosign Module Verification | at process start + on every module reload; verification failure halts startup | Custom | FS-PLAT-04 | FS-PLAT-04 | OQ `OQ-COSIGN-VERIFY-01` |
| DS-CM-07 | OpenShift PodAntiAffinity | replicas across ≥ 2 physical fault domains | Custom | FS-PLAT-05 | FS-PLAT-05 | IQ `OPH-IQ-FAULT-DOMAIN-01` |
| DS-CM-08 | Recipe State Machine | `DRAFT / REVIEW / APPROVED / EFFECTIVE / OBSOLETE` enforced server-side | Custom | FS-REC-01 | FS-REC-01 | OQ `OPH-OQ-REC-STATES-01` |
| DS-CM-09 | Recipe Schema Validator | CQA list + CPP list + diversion rules + PAT-source bindings + ICH Q13 fields | Custom | FS-REC-02 / FS-REC-06 | FS-REC-02, FS-REC-06 | OQ `OQ-REC-PARAM-ENFORCE-01` |
| DS-CM-10 | Cycle-Load Endpoint Gate | state = EFFECTIVE only | Custom | FS-REC-03 | FS-REC-03 | OQ `OPH-OQ-REC-EFF-01` |
| DS-CM-11 | Transition E-Signature | re-auth; role-restricted; SoD enforced | Custom | FS-REC-04 | FS-REC-04 | OQ `OPH-OQ-REC-ESIG-01` |
| DS-CM-12 | EFFECTIVE Immutability | DB constraint + service guard; revision N+1 in DRAFT | Custom | FS-REC-05 | FS-REC-05 | OQ `OPH-OQ-REC-IMMUT-01` |
| DS-CM-13 | Recipe-Diff Renderer | field-by-field old/new + change-reason | Custom | FS-REC-07 | FS-REC-07 | OQ `OPH-OQ-REC-DIFF-01` |
| DS-CM-14 | Design-Space Monitor | per-tick CPP/CQA tuple vs recipe-encoded design-space polytope; excursion → event + alarm + auto-deviation | Custom | FS-SOC-01 | FS-SOC-01 | OQ `OQ-DESIGN-SPACE-MON-01` |
| DS-CM-15 | State-of-Control Indicator | rolling diversion-rate + CPP-drift slope + alarm-frequency; loss → campaign-pause-review workflow | Custom | FS-SOC-02 | FS-SOC-02 | OQ `OQ-STATE-OF-CONTROL-01` |
| DS-CM-16 | SPC Layer | CUSUM + EWMA on configured CQAs/CPPs; Western Electric + Nelson rules | Custom | FS-SOC-03 | FS-SOC-03 | OQ `OQ-SPC-ALARMS-01` |
| DS-CM-17 | State-of-Control + Design-Space REST | metrics exposed for APR ingestion | Custom | FS-SOC-04 | FS-SOC-04 | OQ `OPH-OQ-SOC-REST-01` |
| DS-CM-18 | Per-EC Recipe Schema Field | `ec_id, parameter_path, reporting_category` (enum `prior_approval / CBE_30 / annual / not_reportable`) | Custom | FS-Q12-01 | FS-Q12-01 | OQ `OQ-EC-CLASS-01` |
| DS-CM-19 | EC-Change Gate | CR-ID required; RA signature for prior_approval / CBE_30 | Custom | FS-Q12-02 | FS-Q12-02 | OQ `OQ-EC-CHANGE-GATE-01` |
| DS-CM-20 | EC-Change Audit Report Runner | exports per-EC change history with CR-IDs | Custom | FS-Q12-03 | FS-Q12-03 | OQ `OPH-OQ-EC-AUDIT-01` |
| DS-CM-21 | Batch-Definition Engine | three modes: `time_based / equipment_volume_based / production_volume_based`; boundary deterministic + reconstructable | Custom | FS-Q13-01 | FS-Q13-01 | OQ `OQ-BATCH-DEFINITION-01` |
| DS-CM-22 | Material Time-Resolution | per slowest-RTD-residence-time; diverted-material genealogy preserved | Custom | FS-Q13-02 | FS-Q13-02 | OQ `OPH-OQ-MAT-TIMERES-01` |
| DS-CM-23 | Disturbance-Response Table | maps disturbance-type → auto-divert / auto-pause / alarm-only | Custom | FS-Q13-03 | FS-Q13-03 | PQ `PQ-DISTURB-RESP-01` |
| DS-CM-24 | APL-Doc-ID Recipe Field | enforced at recipe-load | Custom | FS-Q13-04 / FS-Q14-01 | FS-Q13-04, FS-Q14-01 | OQ `OQ-APL-GATE-01` |
| DS-CM-25 | Method-Registry Table | `apl_doc_id` per PAT method; recipe-validation rejects methods without APL doc | Custom | FS-Q14-01 | FS-Q14-01 | OQ `OQ-APL-GATE-01` |
| DS-CM-26 | Model-Loader Verification | cosign + model_id + version + validation_dossier_id at startup; mismatch → block | Custom | FS-Q14-02 | FS-Q14-02 | OQ `OQ-MODEL-VERIFY-01` |
| DS-CM-27 | Model-Performance Monitor | rolling R²cv + RMSEP + residual-trend; degradation > threshold → alarm + PAT-Scientist review queue | Custom | FS-Q14-03 | FS-Q14-03 | OQ `OQ-MODEL-PERF-MON-01` |
| DS-CM-28 | Setpoint-Envelope Evaluator | deviations classified info / warning / critical | Custom | FS-RUN-01 | FS-RUN-01 | OQ `OPH-OQ-RUN-ENV-01` |
| DS-CM-29 | Critical-Alarm Types | PAT loss on CQA, sustained CPP excursion, diverter-actuator fault — ack + reason; persistent | Custom | FS-RUN-02 | FS-RUN-02 | OQ `OPH-OQ-CRIT-ALARM-01` |
| DS-CM-30 | High-Rate Ingest Pipeline | PAT 5-20 Hz, process 1 Hz to PostgreSQL + IP.21 | Custom | FS-RUN-03 | FS-RUN-03 | OQ `OPH-OQ-INGEST-01` |
| DS-CM-31 | Diversion Decision Engine | per-CQA rule evaluation in deterministic order; logged with inputs + thresholds + code_version | Custom | FS-RUN-04 | FS-RUN-04 | OQ `OQ-DIVERSION-DETERMINISTIC-01` |
| DS-CM-32 | Manual-Override Lockout | disabled during PRODUCT_RUN state; ESTOP path only | Custom | FS-RUN-05 | FS-RUN-05 | OQ `OQ-MANUAL-OVERRIDE-DENY-01` |
| DS-CM-33 | Control-Strategy Revalidation Triggers | instrument_id, calibration_window, control-strategy formula changes | Custom | FS-RUN-06 | FS-RUN-06 | (governance) |
| DS-CM-34 | Diverter-Actuation Latency Tracking | per actuation; P95 ≤ 100 ms enforced; threshold → warning | Custom | FS-RUN-07 / FS-PERF-02 | FS-RUN-07, FS-PERF-02 | OQ `OQ-DIVERTER-LATENCY-01` |
| DS-CM-35 | Actuator-Health Monitor | cycle-count + pressure-trend + position-sense error rate; predictive-maintenance | Custom | FS-RUN-08 | FS-RUN-08 | OQ `OPH-OQ-ACT-HEALTH-01` |
| DS-CM-36 | RTD-Model Service | per-unit-op residence-time distribution; PQ-qualified `PQ-RTD-MODEL-01`; revalidation on equipment change | Custom | FS-MAT-01 | FS-MAT-01 | PQ `PQ-RTD-MODEL-01` |
| DS-CM-37 | Time-Resolved Genealogy | API lot + per-feeder excipient lot consumption logged at 1 Hz; RTD-convolution reconstruction | Custom | FS-MAT-02 | FS-MAT-02 | PQ `PQ-MAT-GENEALOGY-01` |
| DS-CM-38 | Diverted-Material Quarantine | `(divert_ts, RTD-back-projected input lots, quantity-mass-estimate)` | Custom | FS-MAT-03 | FS-MAT-03 | OQ `OQ-DIVERT-QUARANTINE-01` |
| DS-CM-39 | Campaign-End Mass-Balance | `closure_ε = input − accepted − diverted − scrap`; > threshold → investigation | Custom | FS-MAT-04 | FS-MAT-04 | OQ `OPH-OQ-MASS-BAL-01` |
| DS-CM-40 | Cat-5 SDLC `SDLC-CM-ORCH-001` | requirements → design → code → tests → security scan → UAT → release | Custom | FS-DEV-01 | FS-DEV-01 | (governance) |
| DS-CM-41 | GitLab + Branch Protection | signed commits (GPG); peer-review + green CI required | Custom | FS-DEV-02 | FS-DEV-02 | (CI) |
| DS-CM-42 | Unit-Test Coverage Gate | ≥ 95% on `control_strategy/`, `diversion/`, `rtd_model/` | Custom | FS-DEV-03 | FS-DEV-03 | OQ `OQ-DEV-COVERAGE-01` |
| DS-CM-43 | CI Static-Analysis | SonarQube + Snyk + Bandit; criticals block merge | Custom | FS-DEV-04 | FS-DEV-04 | (CI) |
| DS-CM-44 | Release Signing | cosign-signed release tags; runtime verifies (DS-CM-06) | Custom | FS-DEV-05 | FS-DEV-05 | (CI) + OQ `OQ-COSIGN-VERIFY-01` |
| DS-CM-45 | Release-Bundle Template | `release-notes + FS-DS-delta + regression-report + security-report + CR-link` | Custom | FS-DEV-06 | FS-DEV-06 | (CI) |
| DS-CM-46 | CSA Risk-Classification Doc | per release; risk-justified-testing rationale | Custom | FS-DEV-07 | FS-DEV-07 | OQ `OQ-CSA-RISK-DOC-01` |
| DS-CM-47 | Audit-Trail Coverage | recipe lifecycle + diversion + alarm acks + signatures + code releases + model deployments + EC changes | Custom | FS-AUD-01 | FS-AUD-01 | OQ `OPH-OQ-AUDIT-COV-01` |
| DS-CM-48 | Audit Append-Only DB | revoked DELETE/UPDATE; DBA dual control | Custom | FS-AUD-02 | FS-AUD-02 | OQ `OPH-OQ-AUDIT-APPEND-01` |
| DS-CM-49 | Per-Batch QR Audit Review UI | quarterly QA-Compliance platform review | Custom | FS-AUD-03 | FS-AUD-03 | OQ `OPH-OQ-AUDIT-REV-01` |
| DS-CM-50 | 25-Year Immutable Cold Storage | S3 Object-Lock | Custom | FS-AUD-04 | FS-AUD-04 | (governance) |
| DS-CM-51 | Signature Render | printed name + ts + meaning into audit + PDFs | Custom | FS-PART11-01 | FS-PART11-01 | OQ `OPH-OQ-SIG-RENDER-01` |
| DS-CM-52 | User-ID Uniqueness | AD-enforced; non-reuse policy | Custom | FS-PART11-02 | FS-PART11-02 | OQ `OPH-OQ-USERID-01` |
| DS-CM-53 | PKI-Signed Signature Payload | tamper detection on read | Custom | FS-PART11-03 | FS-PART11-03 | OQ `OPH-OQ-SIG-PKI-01` |
| DS-CM-54 | SoD Policy Engine | conflicts rejected | Custom | FS-PART11-04 | FS-PART11-04 | OQ `OPH-OQ-SOD-01` |
| DS-CM-55 | Re-Auth + MFA at Every Signature | cached creds disabled | Custom | FS-PART11-05 | FS-PART11-05 | OQ `OPH-OQ-REAUTH-01` |
| DS-CM-56 | AD Password Policy `SEC-AD-POLICY-001` | per central policy doc | Custom | FS-PART11-06 | FS-PART11-06 | (governance) |
| DS-CM-57 | Audit Coverage + Export | per § 11.10(b)/(c)/(e) | Custom | FS-PART11-07 | FS-PART11-07 | OQ `OPH-OQ-PART11-COV-01` |
| DS-CM-58 | PAS-X REST mTLS | SHA-256 + version validated | Custom | FS-INT-MES-01 | FS-INT-MES-01 | OQ `OPH-OQ-MES-IN-01` |
| DS-CM-59 | Batch Report POST | within 30 min of cycle end; retry with backoff | Custom | FS-INT-MES-02 | FS-INT-MES-02 | OQ `OPH-OQ-MES-OUT-01` |
| DS-CM-60 | MasterControl Auto-Deviation | unacknowledged critical alarms past SLA | Custom | FS-INT-EQMS-01 | FS-INT-EQMS-01 | OQ `OPH-OQ-EQMS-01` |
| DS-CM-61 | PAT Subscriptions | OPC UA + REST mTLS; loss-of-signal watchdog (≥ 3 missed samples) → safe-state diversion | Custom | FS-INT-PAT-01 | FS-INT-PAT-01 | OQ `OQ-PAT-LOSS-SAFE-STATE-01` |
| DS-CM-62 | Ignition / DCS Phase Commands | OPC UA mTLS | Custom | FS-INT-DCS-01 | FS-INT-DCS-01 | OQ `OPH-OQ-DCS-01` |
| DS-CM-63 | Aspen IP.21 SDK Adapter | channel data streamed at native rate | Custom | FS-INT-HIST-01 | FS-INT-HIST-01 | OQ `OPH-OQ-ASPEN-01` |
| DS-CM-64 | QP Override Endpoint | QP-role + MFA + reason; events POSTed to MasterControl | Custom | FS-INT-QP-01 | FS-INT-QP-01 | OQ `OQ-QP-OVERRIDE-01` |
| DS-CM-65 | AD User-ID Attribution | all writes attributed | Custom | FS-DI-01 | FS-DI-01 | OQ `OPH-OQ-DI-ATTRIB-01` |
| DS-CM-66 | Export PDF + CSV + JSON | | Custom | FS-DI-02 | FS-DI-02 | OQ `OPH-OQ-EXPORT-01` |
| DS-CM-67 | PTP Clock-Skew Gate | enforced | Custom | FS-DI-03 | FS-DI-03 | OQ `OPH-OQ-PTP-01` |
| DS-CM-68 | Originals Immutable + Derivations Separate | | Custom | FS-DI-04 | FS-DI-04 | OQ `OPH-OQ-DI-LIN-01` |
| DS-CM-69 | Control-Strategy Calc Engine | deterministic; IEEE-754 round-mode pin | Custom | FS-DI-05 | FS-DI-05 | OQ `OQ-CALC-01` |
| DS-CM-70 | 25-Y Retention + 4-h Retrieval | | Custom | FS-DI-06 | FS-DI-06 | OQ `OPH-OQ-RETR-01` |
| DS-CM-71 | LIW Feeder Mass-Flow | 10 Hz via OPC UA; rolling deviation evaluator | Custom | FS-FEED-01 | FS-FEED-01 | OQ `OPH-OQ-LIW-FLOW-01` |
| DS-CM-72 | Refill-Event Watcher | tags channel-log with `refill_state ∈ {steady, refill}` | Custom | FS-FEED-02 | FS-FEED-02 | OQ `OPH-OQ-REFILL-01` |
| DS-CM-73 | Compactor Channels | force + gap + roll-speed ≥ 1 Hz; CPP-envelope evaluator | Custom | FS-FEED-03 | FS-FEED-03 | OQ `OPH-OQ-COMP-01` |
| DS-CM-74 | Feeder Calibration-State Gate | OUT_OF_CAL blocks recipe-load | Custom | FS-FEED-04 | FS-FEED-04 | OQ `OPH-OQ-FEED-CAL-01` |
| DS-CM-75 | SIMULATOR_MODE Flag | PAT-input replay subsystem; actuator outputs intercepted | Custom | FS-SIM-01 | FS-SIM-01 | OQ `OPH-OQ-SIM-MODE-01` |
| DS-CM-76 | CI Scenario Regression in SIM | gate on PR merge | Custom | FS-SIM-02 | FS-SIM-02 | (CI) |
| DS-CM-77 | Simulator Runs Tagged | audit + report header `"SIMULATOR — NON-PRODUCTION"` | Custom | FS-SIM-03 | FS-SIM-03 | OQ `OPH-OQ-SIM-TAG-01` |
| DS-CM-78 | Deployment Endpoint > Linked-CR-ID | missing → HTTP 400 | Custom | FS-PMCM-01 | FS-PMCM-01 | OQ `OPH-OQ-DEPLOY-CR-01` |
| DS-CM-79 | Post-Deployment Monitoring Window Flag | set on first N batches (recipe-defined); elevated review in QA dashboard | Custom | FS-PMCM-02 | FS-PMCM-02 | OQ `OPH-OQ-PMCM-01` |
| DS-CM-80 | CQA-Compute Latency Budget | ≤ 200 ms P95; load-tested 30 d | Custom | FS-PERF-01 | FS-PERF-01 | PQ `PQ-PERF-CQA-LATENCY-01` |
| DS-CM-81 | Availability Target | ≥ 99.5% production windows; external-probe measured | Custom | FS-AV-01 | FS-AV-01 | (governance) |
| DS-CM-82 | Postgres Backup | nightly + continuous WAL → S3 Object-Lock; PITR | Custom | FS-BAK-01 | FS-BAK-01 | OQ `OPH-OQ-BAK-PITR-01` |
| DS-CM-83 | Quarterly Restore Test | witnessed | Custom | FS-BAK-02 | FS-BAK-02 | PR-01 |
| DS-CM-84 | Vault Service Accounts | short-lived secrets | Custom | FS-SEC-01 | FS-SEC-01 | OQ `OPH-OQ-VAULT-01` |
| DS-CM-85 | Removable-Media GPO | block-by-default | Custom | FS-SEC-02 | FS-SEC-02 | OQ `OPH-OQ-USB-01` |
| DS-CM-86 | LMS-Recorded Training | role-specific | Custom | FS-TRN-01 | FS-TRN-01 | (governance) |
| DS-CM-87 | Annual CM-Decision-Logic Competency Assessment | PAT Scientist + CM Lead + QP | Custom | FS-TRN-02 | FS-TRN-02 | (governance) |
| DS-CM-88 | Periodic-Review Runbook | configuration drift + code-release register + audit-trail review + deviation summary + control-strategy verification + EC-change history + model-performance trends + RTD-qualification currency | Custom | FS-PR-01 | FS-PR-01 | PR-01 |
| DS-CM-89 | AD Conditional Access `OT-SCADA Conditional Access` | MFA at HMI session start; named-location restriction to plant network; SIEM → Splunk `gxp-authn`; CyberArk PAM break-glass | Custom | FS-XSYS-AD-01 | FS-XSYS-AD-01 | OQ `OPH-OQ-CONDACC-01` |
| DS-CM-90 | Veeam Backup | App-aware MS SQL VSS for recipe / batch-history DB + file-level PLC program backups; tier T1; RPO ≤ 4 h; RTO ≤ 4 BH; S3 Compliance Mode + LTO-9 monthly | Custom | FS-XSYS-BAK-01 | FS-XSYS-BAK-01 | OQ `OPH-OQ-VEEAM-01` |

---

## 5. Workflow + Business-Rule Design

### 5.1 Recipe-Approval Workflow

| Transition | Required signatures | Resulting state |
|---|---|---|
| DRAFT → REVIEW | Author `authorship` | REVIEW |
| REVIEW → APPROVED | CM SME + PAT Scientist + FSE + Quality IT Lead `review` (n=4); EC-class gate (DS-CM-19) clear | APPROVED |
| APPROVED → EFFECTIVE | Head of CM + Head of QA + QP `approval` (triple sign); if prior_approval EC → Regulatory Affairs co-sign | EFFECTIVE |
| EFFECTIVE → OBSOLETE | CM Lead `retirement` | OBSOLETE |

EC-change gate (DS-CM-19) blocks approval until CR-ID linked and RA signature obtained for `prior_approval / CBE_30` categories.

### 5.2 Diversion Decision Workflow (deterministic order)

```
Per-CQA rule evaluation in deterministic order from recipe.diversion_rules[]
     │
     ▼
For each rule: if (cqa_value violates rule) → divert_decision=true
     │
     ▼
Aggregate: any divert_decision=true → DIVERT
     │
     ▼
Log {decision_id, inputs, thresholds, decision, code_version, ts_ptp} →
     ▼
Send diverter actuation command to ControlLogix (target P95 ≤ 100 ms)
     ▼
Diverter-position-ack → record latency → quarantine genealogy write
```

### 5.3 State-of-Control Workflow

Continuous evaluation: rolling diversion-rate + CPP-drift slope + alarm-frequency → state-of-control indicator. Loss-of-state → `campaign-pause-review` workflow → CM Lead + QA review → resume or campaign-end.

### 5.4 ICH Q14 APL / Q12 EC Rules

- **APL gate (DS-CM-25):** recipe-validation rejects methods without `apl_doc_id`.
- **Q12 EC gate (DS-CM-19):** EC modifications require CR-ID; RA signature for `prior_approval / CBE_30`.

### 5.5 Manual-Override Lockout Rule (FS-RUN-05 / DS-CM-32)

During `PRODUCT_RUN` state, manual-override endpoint returns HTTP 403. Only ESTOP path available. Override allowed only in non-PRODUCT_RUN states with dual-sign + reason.

### 5.6 Simulator-Mode Audit Tagging Rule

All Simulator-mode runs (DS-CM-75) carry header `"SIMULATOR — NON-PRODUCTION"` in audit + report; gate prevents simulator data from contaminating production reports.

### 5.7 Post-Market Change Management (FS-PMCM-* / DS-CM-78/79)

Deployment requires `cr_id` in payload; first N batches post-deploy flagged with `pmcm_window=true`; elevated QA review surfaced in dashboard.

### 5.8 RTRT Decision

PAT-fusion engine consumes NIR + Raman + LIW mass-flow + PSD; computes per-tablet probability-of-release; rule-based decision via recipe.rtrt_decision_rules; result logged with model-id + version + inputs; reconstructable from logs.

---

## 6. Role-Permission Matrix Design

| AD Group | View HMI | Ack alarm | Author recipe | Approve recipe | Sign EC change | QP override | Approve model | Audit export | Admin |
|---|---|---|---|---|---|---|---|---|---|
| `CM-Operator` | Y | WARN | — | — | — | — | — | — | — |
| `CM-Senior-Operator` | Y | CRIT | — | — | — | — | — | — | — |
| `CM-Lead` | Y | — | — | approve | — | — | — | — | — |
| `CM-Continuous-Mfg-SME` | Y | — | review | review | — | — | — | — | — |
| `CM-PAT-Scientist` | Y | — | review | review | — | — | author + review | — | — |
| `CM-FSE` | Y | — | review | review | — | — | — | — | — |
| `CM-Quality-IT-Lead` | Y | — | review | review | — | — | — | — | — |
| `CM-Regulatory-Affairs` | Y (RO) | — | — | sign (prior_approval / CBE_30) | sign | — | — | — | — |
| `CM-Quality-Approver` | Y | — | — | approve (QA) | — | — | approve | Y | — |
| `CM-Qualified-Person` | Y | — | — | approve (QP) | — | Y (with MFA) | — | Y | — |
| `CM-Auditor` | Y (RO) | — | — | — | — | — | — | Y | — |
| Break-glass DBA (vaulted) | — | — | — | — | — | — | — | — | DB |

FS-IDs traced: FS-PART11-04, FS-Q12-02, FS-INT-QP-01, FS-PAT-07 / FS-Q14-02.

---

## 7. Integration Design

### 7.1 IF-MES-01/02 (PAS-X v3.2)

- Endpoints REST mTLS for recipe + batch context (in) and batch report (out). Idempotency on `batchId`. Retry with backoff. SHA-256 + version validation at recipe-load.
- FS-IDs: FS-INT-MES-01/02

### 7.2 IF-EQMS-01 (MasterControl)

- `POST /api/v2/deviations` for unacknowledged critical alarms past SLA. Retry 1/5/30 s.
- FS-IDs: FS-INT-EQMS-01

### 7.3 IF-PAT-01 (NIR / Raman / LIW / PSD)

- OPC UA + REST mTLS. Watchdog ≥ 3 missed samples → `PatLossHandler` safe-state diversion.
- FS-IDs: FS-INT-PAT-01

### 7.4 IF-DCS-01 (Ignition / DCS)

- OPC UA mTLS — phase commands; loss raises `DCS_LOSS` and pauses run.
- FS-IDs: FS-INT-DCS-01

### 7.5 IF-HIST-01 (Aspen IP.21)

- IP.21 SDK; native-rate streaming; store-and-forward at gateway.
- FS-IDs: FS-INT-HIST-01

### 7.6 IF-QP-01 (QP Override)

- REST + UI; QP-role + MFA + reason capture; override events POSTed to MasterControl deviation.
- FS-IDs: FS-INT-QP-01

### 7.7 IF-AD-01 / IF-PTP-01

- LDAPS / Kerberos for auth; PTP for time sync (clock-skew gate at signature).
- FS-IDs: FS-SEC-01 / FS-DI-03

### 7.8 Integration Risk Register

| Interface | Risk | Mitigation |
|---|---|---|
| IF-MES | recipe-version drift on download | SHA-256 validate at receiver + reject |
| IF-PAT | sensor desync across PAT bus | PTP-aligned timestamps + watchdog |
| IF-EQMS | deviation post lost during eQMS upgrade | DLQ + replay |
| IF-DCS | OPC UA cert expiry | cert-manager 365-d rotation |
| IF-QP | override path bypassed via direct DB write | API-only enforcement + DB role lacks override-table write |
| IF-AD | outage | local OT-cached creds 24 h |

---

## 8. Site-Deployed Components — Mini-SDS for CM Orchestrator (Cat 5)

### 8.1 Software Architecture

```
   ┌────────────────────────────────────────────────────────────┐
   │  CM Orchestrator (Python 3.11, ~10k LOC)                     │
   │  ┌──────────────────────────┐  ┌─────────────────────────┐   │
   │  │  recipe/                  │  │  control_strategy/       │   │
   │  │  - RecipeApi              │  │  - DesignSpaceMonitor    │   │
   │  │  - RecipeReceiver         │  │  - StateOfControl        │   │
   │  └──────────────────────────┘  │  - SpcEngine (CUSUM/EWMA)│   │
   │  ┌──────────────────────────┐  └─────────────────────────┘   │
   │  │  q12_q14/                 │  ┌─────────────────────────┐   │
   │  │  - EcChangeGate           │  │  diversion/              │   │
   │  │  - AplGate                │  │  - DiversionEngine       │   │
   │  │  - ModelLoader            │  │  - DiverterController    │   │
   │  │  - ModelPerformanceMon    │  │  - ActuatorHealthMon     │   │
   │  └──────────────────────────┘  └─────────────────────────┘   │
   │  ┌──────────────────────────┐  ┌─────────────────────────┐   │
   │  │  rtd_model/               │  │  feed/                   │   │
   │  │  - RtdConvolver           │  │  - LiwMassFlow           │   │
   │  │  - GenealogyLinker        │  │  - RefillWatcher         │   │
   │  │  - MassBalance            │  │  - CompactorMonitor      │   │
   │  └──────────────────────────┘  └─────────────────────────┘   │
   │  ┌──────────────────────────┐  ┌─────────────────────────┐   │
   │  │  safety/                  │  │  integration/            │   │
   │  │  - SafeStateEnter         │  │  - PatBus / MesClient    │   │
   │  │  - QpOverrideApi          │  │  - EqmsClient / Ip21Adptr│   │
   │  └──────────────────────────┘  └─────────────────────────┘   │
   └────────────────────────────────────────────────────────────┘
```

### 8.2 Module Decomposition

| Module ID | Module name | Responsibility | Interface | Dependencies | GxP class |
|---|---|---|---|---|---|
| MS-01 | `recipe.RecipeApi` | REST endpoints | `GET /recipes/effective`, `POST /recipes/transition` | Postgres | R1 |
| MS-02 | `recipe.RecipeReceiver` | PAS-X recipe fetch + checksum | scheduled | PAS-X | R1 |
| MS-03 | `control_strategy.DesignSpaceMonitor` | per-tick polytope check | tick callback | tag subs | R1 |
| MS-04 | `control_strategy.StateOfControl` | rolling indicator | scheduled | DB metrics | R1 |
| MS-05 | `control_strategy.SpcEngine` | CUSUM + EWMA + Western Electric + Nelson | tick | DB metrics | R1 |
| MS-06 | `diversion.DiversionEngine` | per-CQA rule evaluation | tick | recipe + PAT | R1 |
| MS-07 | `diversion.DiverterController` | command + ack tracking | tick | ControlLogix OPC UA | R1 |
| MS-08 | `diversion.ActuatorHealthMon` | cycle-count + position-error | scheduled | tag subs | R2 |
| MS-09 | `rtd_model.RtdConvolver` | RTD-convolution for genealogy | callable | qualified RTD | R1 |
| MS-10 | `rtd_model.GenealogyLinker` | per-window lot consumption | callable | DB | R1 |
| MS-11 | `rtd_model.MassBalance` | campaign-end closure | scheduled | DB | R2 |
| MS-12 | `feed.LiwMassFlow` | 10-Hz mass-flow processing | tick | OPC UA | R1 |
| MS-13 | `feed.RefillWatcher` | tags refill state | event | LIW signal | R2 |
| MS-14 | `feed.CompactorMonitor` | force/gap/roll-speed | tick | OPC UA | R2 |
| MS-15 | `q12_q14.EcChangeGate` | EC reporting-category enforcement | API | recipe + CR | R1 |
| MS-16 | `q12_q14.AplGate` | APL-doc-id enforcement | recipe-load | method registry | R1 |
| MS-17 | `q12_q14.ModelLoader` | cosign + id + version + dossier | startup | cosign + MLflow | R1 |
| MS-18 | `q12_q14.ModelPerformanceMon` | rolling R²cv + RMSEP + residuals | scheduled | InfluxDB | R1 |
| MS-19 | `safety.SafeStateEnter` | safe-state command path | event | tag writer | R1 |
| MS-20 | `safety.QpOverrideApi` | QP-role override endpoint | API | MFA + MasterControl | R1 |

### 8.3 Data Model

| Table | Key columns | Constraints | Retention |
|---|---|---|---|
| `recipe` | per FS schema | EFFECTIVE-immutability trigger | indefinite |
| `batch_instance` | `batch_id, recipe_id, recipe_version, batch_def_mode, started_at, ended_at, state` | NOT NULL on all | 25 y |
| `channel_log` | `channel, ts, value, source_tag, quality_flag` | indexed on `ts` | 25 y |
| `pat_signal` | `instrument, ts, value, model_id, model_version, calibration_state` | NOT NULL | 25 y |
| `diversion_decision` | `decision_id, batch_id, ts, inputs JSONB, threshold, decision, code_version` | NOT NULL on all | 25 y |
| `genealogy` | `window_start, window_end, api_lot, excipient_lots[], rtd_state` | NOT NULL | 25 y |
| `diversion` | `divert_id, batch_id, gate_actuation_ts, position_ack_ts, mass_estimate, genealogy_ref` | latency tracked | 25 y |
| `alarm` | per FS | append-only | 25 y |
| `ec_change` | `ec_id, old, new, cr_id, reg_affairs_sig, ts` | NOT NULL on cr_id | indefinite |
| `release` | `release_id, ts, sha256, csa_risk_class, regression_report_id` | NOT NULL | indefinite |
| `signature` | per FS | PKI bound | 25 y |
| `audit_event` | per FS-AUD-01 | append-only role GRANT | 25 y |

### 8.4 Algorithm + Calculation Design

| Algorithm | Inputs | Output | Procedure | Numerical-precision note | Reference |
|---|---|---|---|---|---|
| Design-space polytope check | CPP+CQA tuple | inside/outside | n-dim polytope inclusion test | float64; IEEE-754 round-mode pinned | ICH Q8(R2) |
| CUSUM | series | upper / lower CUSUM | recipe-defined h, k | float64 | NIST/SEMATECH |
| EWMA | series | EWMA value + alarm | λ recipe-defined | float64 | NIST/SEMATECH |
| Western Electric Rule 1-8 | series | rule fire booleans | per ASTM E2476 | int + bool | ASTM E2476 |
| Nelson Rules 1-8 | series | rule fire booleans | per Nelson 1984 | int + bool | Nelson (1984) |
| RTD convolution | recent feed-state vector + RTD kernel | downstream concentration | discrete convolution at `Δt = slowest_residence/N` | float64; pinned step | site model + PQ-RTD-MODEL-01 |
| Mass balance | inputs[], accepted, diverted, scrap | closure_ε | algebraic; threshold per recipe | Decimal | site |
| Rolling R²cv | predicted, observed series | R²cv | rolling-window correlation | float64 | model PERF lifecycle |
| Diverter-latency P95 | latency series per actuation | P95 latency | t-digest sketch | float64 | site |

Determinism harness: 1000× canonical input replay bitwise-identical (DS-CM-69).

### 8.5 Interface + API Design

| Endpoint | Method | AuthN | Request | Response | Idempotency | Audit |
|---|---|---|---|---|---|---|
| `/api/recipes/effective` | GET | Kerberos | `recipe_id` | RecipeVersion JSON | safe | `recipe_fetch` |
| `/api/recipes/transition` | POST | Kerberos + signature | `{recordHash, signerId, meaning, ec_cr_id?}` | new state | by recordHash | `recipe_transition` |
| `/api/diversion/decision/{id}` | GET | Kerberos | path | decision JSON | safe | `diversion_query` |
| `/api/qp-override` | POST | Kerberos QP + MFA | `{batch_id, reason}` | override_id | by batch + ts | `qp_override` |
| `/api/models/transition` | POST | Kerberos PAT-Scientist/QA + signature | model lifecycle event | sig_id | by model_id + version | `model_transition` |
| `/api/deploy` | POST | Kerberos Release-Mgr | `{release_id, cr_id}` | accepted/rejected | by release_id | `deploy_attempt` |
| `/api/sim/start` | POST | Kerberos | scenario | simrun_id | by scenario hash | `sim_start` |

### 8.6 Security Design

- **AuthN:** AD + Yubikey MFA; service accounts via Vault
- **AuthZ:** AD-group → role per § 6; SoD enforced
- **Secrets:** HashiCorp Vault; CyberArk PAM for break-glass
- **Transport:** TLS 1.2+; mTLS for all integrations
- **Audit-event taxonomy:** `recipe_*`, `diversion_*`, `model_*`, `qp_override`, `ec_change`, `deploy_*`, `sim_*`, `signature_emit`

### 8.7 Deployment Architecture

- **Packaging:** container images cosign-signed; CR-bound
- **Topology:** OpenShift 4.14 `cm-prod` 3 replicas + DR `cm-dr`; PodAntiAffinity across fault domains
- **Observability:** Prometheus + Grafana `OPH-GR-CM-RUNTIME`; Splunk `gxp-cm`
- **DR:** geo-paired DR site; RTO ≤ 4 h

### 8.8 Module Specification Table

| Module ID | Source location | Unit-test ref |
|---|---|---|
| MS-01..MS-20 | `gitlab.ophir.local/cm/orchestrator/{recipe,control_strategy,diversion,rtd_model,feed,q12_q14,safety,integration}/*.py` | `<repo>/tests/unit/test_<module>.py` (coverage ≥ 95% safety/*) |

Full Module Specifications: `OPH-MS-CM-NN` (downstream).

---

## 9. References

### US
- 21 CFR Part 11; 21 CFR Part 211
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026)
- FDA ICH Q13 implementation (2024)

### EU
- EU GMP Annex 11
- EU GMP Annex 15
- Directive 2001/83/EC Art. 51 (QP)

### DACH
- AMWHV
- BSI IT-Grundschutz baseline

### International
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE Baseline Guide *Continuous Manufacturing of Solid Oral Dosage Forms*
- ICH Q13; ICH Q14; ICH Q12; ICH Q9(R1); ICH Q10; ICH Q8(R2)
- ANSI/ISA-88 Part 1 + Part 2; ANSI/ISA-95 Part 1
- IEC 61131-3; IEC 61511 (SIL 2)
- ASTM E2476
- PIC/S PI 041
- ISO/IEC 27001:2022

### Vendor
- Inductive Automation — *Ignition 8.3 Reference*
- Allen-Bradley / Rockwell — *ControlLogix 5580 + FactoryTalk Reference*
- Werum / Körber — *PAS-X v3.2 Integration Guide*
- AspenTech — *IP.21 SDK Reference*
- MasterControl — *eQMS REST API Reference*

### Site
- `OPH-URS-CM-001` v1.2 (informational)
- `OPH-FS-CM-001` v1.2 (parent)
- `SDLC-CM-ORCH-001` (Cat-5 SDLC)
- `PAT-MODEL-LCM-001` (model lifecycle)
- `OPH-PR-CM-YYYYMMDD` (periodic-review template)

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-CM-01 | FS-PLAT-01 |
| DS-CM-02 | FS-PLAT-01 |
| DS-CM-03 | FS-PLAT-02 |
| DS-CM-04 | FS-PLAT-02 |
| DS-CM-05 | FS-PLAT-03 |
| DS-CM-06 | FS-PLAT-04 |
| DS-CM-07 | FS-PLAT-05 |
| DS-CM-08 | FS-REC-01 |
| DS-CM-09 | FS-REC-02 / FS-REC-06 |
| DS-CM-10 | FS-REC-03 |
| DS-CM-11 | FS-REC-04 |
| DS-CM-12 | FS-REC-05 |
| DS-CM-13 | FS-REC-07 |
| DS-CM-14 | FS-SOC-01 |
| DS-CM-15 | FS-SOC-02 |
| DS-CM-16 | FS-SOC-03 |
| DS-CM-17 | FS-SOC-04 |
| DS-CM-18 | FS-Q12-01 |
| DS-CM-19 | FS-Q12-02 |
| DS-CM-20 | FS-Q12-03 |
| DS-CM-21 | FS-Q13-01 |
| DS-CM-22 | FS-Q13-02 |
| DS-CM-23 | FS-Q13-03 |
| DS-CM-24 | FS-Q13-04 / FS-Q14-01 |
| DS-CM-25 | FS-Q14-01 |
| DS-CM-26 | FS-Q14-02 |
| DS-CM-27 | FS-Q14-03 |
| DS-CM-28 | FS-RUN-01 |
| DS-CM-29 | FS-RUN-02 |
| DS-CM-30 | FS-RUN-03 |
| DS-CM-31 | FS-RUN-04 |
| DS-CM-32 | FS-RUN-05 |
| DS-CM-33 | FS-RUN-06 |
| DS-CM-34 | FS-RUN-07 / FS-PERF-02 |
| DS-CM-35 | FS-RUN-08 |
| DS-CM-36 | FS-MAT-01 |
| DS-CM-37 | FS-MAT-02 |
| DS-CM-38 | FS-MAT-03 |
| DS-CM-39 | FS-MAT-04 |
| DS-CM-40 | FS-DEV-01 |
| DS-CM-41 | FS-DEV-02 |
| DS-CM-42 | FS-DEV-03 |
| DS-CM-43 | FS-DEV-04 |
| DS-CM-44 | FS-DEV-05 |
| DS-CM-45 | FS-DEV-06 |
| DS-CM-46 | FS-DEV-07 |
| DS-CM-47 | FS-AUD-01 |
| DS-CM-48 | FS-AUD-02 |
| DS-CM-49 | FS-AUD-03 |
| DS-CM-50 | FS-AUD-04 |
| DS-CM-51 | FS-PART11-01 |
| DS-CM-52 | FS-PART11-02 |
| DS-CM-53 | FS-PART11-03 |
| DS-CM-54 | FS-PART11-04 |
| DS-CM-55 | FS-PART11-05 |
| DS-CM-56 | FS-PART11-06 |
| DS-CM-57 | FS-PART11-07 |
| DS-CM-58 | FS-INT-MES-01 |
| DS-CM-59 | FS-INT-MES-02 |
| DS-CM-60 | FS-INT-EQMS-01 |
| DS-CM-61 | FS-INT-PAT-01 |
| DS-CM-62 | FS-INT-DCS-01 |
| DS-CM-63 | FS-INT-HIST-01 |
| DS-CM-64 | FS-INT-QP-01 |
| DS-CM-65 | FS-DI-01 |
| DS-CM-66 | FS-DI-02 |
| DS-CM-67 | FS-DI-03 |
| DS-CM-68 | FS-DI-04 |
| DS-CM-69 | FS-DI-05 |
| DS-CM-70 | FS-DI-06 |
| DS-CM-71 | FS-FEED-01 |
| DS-CM-72 | FS-FEED-02 |
| DS-CM-73 | FS-FEED-03 |
| DS-CM-74 | FS-FEED-04 |
| DS-CM-75 | FS-SIM-01 |
| DS-CM-76 | FS-SIM-02 |
| DS-CM-77 | FS-SIM-03 |
| DS-CM-78 | FS-PMCM-01 |
| DS-CM-79 | FS-PMCM-02 |
| DS-CM-80 | FS-PERF-01 |
| DS-CM-81 | FS-AV-01 |
| DS-CM-82 | FS-BAK-01 |
| DS-CM-83 | FS-BAK-02 |
| DS-CM-84 | FS-SEC-01 |
| DS-CM-85 | FS-SEC-02 |
| DS-CM-86 | FS-TRN-01 |
| DS-CM-87 | FS-TRN-02 |
| DS-CM-88 | FS-PR-01 |
| DS-CM-89 | FS-XSYS-AD-01 |
| DS-CM-90 | FS-XSYS-BAK-01 |
| MS-01..MS-20 | Cat-5 mini-SDS § 8.2 — CM Orchestrator; transitively traces FS-DEV-01..07 + FS-REC-* + FS-SOC-* + FS-Q12-* + FS-Q13-* + FS-Q14-* + FS-RUN-* + FS-MAT-* |

---

## 11. Design-level Risk Register

Per § 2B.8. Formal RA in `OPH-RA-CM-001` (synthetic).

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| DR-01 | Defect in control-strategy code causing missed diversion of OOS material | Medium | Critical | FS-DEV-01..07 + FS-RUN-04 deterministic + 1000× determinism replay |
| DR-02 | PAT loss not triggering safe state | Medium | High | DS-CM-61 watchdog + PatLossHandler |
| DR-03 | Cosign signature compromise | Medium | Medium | DS-CM-06 startup verify + paired-key rotation procedure |
| DR-04 | Audit-trail tampering by privileged user | Low | Critical | DS-CM-48 append-only + DBA dual-control |
| DR-05 | RTD-model drift leading to genealogy mis-assignment | Medium | High | DS-CM-36 PQ-revalidation triggers |
| DR-06 | Multivariate model staleness causing false RTRT pass | Medium | Critical | DS-CM-27 performance monitor + PAT-Scientist review |
| DR-07 | EC unreported regulatory change | Low | Critical | DS-CM-19 EC gate + RA signature gate |
| DR-08 | Diverter actuator failure | Low | Critical | DS-CM-35 actuator-health + SIL-2 fail-safe |
| DR-09 | State-of-control loss undetected (drift) | Medium | High | DS-CM-15 + DS-CM-16 SPC alarms |
| DR-10 | Design-space excursion without investigation | Low | High | DS-CM-14 monitor + auto-deviation creation |
| DR-11 | Race condition between diverter command + material-tracking propagation | Low | High | DS-CM-31 deterministic + RTD-σ tolerance |
| DR-12 | Mass-balance closure failure undetected | Medium | Medium | DS-CM-39 threshold-driven investigation |
| DR-13 | QP override audit-gap | Low | Critical | DS-CM-64 API + MasterControl push + signature |
| DR-14 | Loss of PTP causing audit-trail timestamp anomaly | Low | High | DS-CM-67 clock-skew gate |
| DR-15 | Manual-override lockout bypass via direct OPC UA write | Low | Critical | OPC UA role limited; ControlLogix safe-state rule |
| DR-16 | SIMULATOR_MODE accidentally enabled in production | Low | Critical | Startup config validated; audit header "SIMULATOR" + UI banner |
| DR-17 | Post-deployment monitoring window flag (DS-CM-79) not reset → permanent elevated review | Low | Low | Auto-clear after N batches; PR-01 review |
| DR-18 | Model-loader (DS-CM-26) cosign verification race during hot-reload | Low | High | Startup-only model load; runtime reload requires explicit CR |
| DR-19 | Veeam VSS backup contention with high-frequency PAT writes | Low | Medium | Backup window outside high-rate; monitored |
| DR-20 | AD Conditional Access (DS-CM-89) blocks emergency QP override | Low | High | Named-location exception + CyberArk break-glass |
| DR-21 | Disturbance-response table (DS-CM-23) misclassifies novel disturbance type as alarm-only | Medium | High | Periodic-review (DS-CM-88) reviews disturbance-classifier evidence; CR for table updates |
| DR-22 | Diverter-actuation latency P95 ≤ 100 ms breached on first-of-day load | Medium | Medium | Warm-up routine + DS-CM-34 per-actuation latency tracking + alerting |
| DR-23 | RTD-model (DS-CM-36) revalidation deferred during equipment swap | Low | High | Revalidation trigger hard-coded in `equipment_change` CR; deployment blocked until PQ-RTD redo |
| DR-24 | Helios-style audit egress (not yet in scope for Ophir) absent — gaps if regulator requests external stream | Low | Medium | Roadmap to add Kafka egress per Veridian pattern in v1.1 DS revision |

### Design-level risk summary

Risks split into four categories:

1. **Algorithmic-correctness risks** (DR-01, DR-05, DR-06, DR-09, DR-10, DR-11, DR-12) — control-strategy / RTD-model / SPC / mass-balance algorithms.
2. **Safety-critical-path risks** (DR-02, DR-08, DR-13, DR-15) — PAT loss / diverter actuator / QP override / manual-override bypass.
3. **Configuration-immutability risks** (DR-03, DR-04, DR-07, DR-16, DR-17, DR-18) — cosign verify / audit append-only / EC gate / sim-mode tag / PMCM flag / model-loader race.
4. **Infrastructure-tier risks** (DR-14, DR-19, DR-20, DR-22, DR-23, DR-24) — PTP / Veeam / Conditional Access / latency / RTD revalidation / external audit egress.

Each row carries a mitigation reference to a specific DS-CM-NN CI or governance instrument. The formal Risk Assessment artefact `OPH-RA-CM-001` (synthetic, downstream) re-evaluates these with FMEA / HAZOP rigor.

#### CI Density Notes

The 90 DS-CM-NN CIs distribute as: 7 platform / 6 recipe / 4 state-of-control / 3 Q12 / 4 Q13 / 3 Q14 / 8 run execution / 4 material tracking / 7 SDLC / 4 audit / 7 Part-11 / 7 integrations / 6 data integrity / 4 upstream feeder + compactor / 3 simulator / 2 post-market CM / 1 performance + 1 availability / 2 backup / 2 security / 2 training / 1 periodic review / 2 cross-system. Each FS-ID is covered by ≥ 1 DS-ID; FS-PERF-02, FS-Q13-04 are referenced by multiple DS-IDs (latency tracking, APL gate cross-reference).

#### Mini-SDS Decomposition Rationale (§ 8)

The CM Orchestrator (Cat 5, ~10k LOC) is decomposed across 20 modules grouped into 7 packages: `recipe` (MS-01..02), `control_strategy` (MS-03..05), `diversion` (MS-06..08), `rtd_model` (MS-09..11), `feed` (MS-12..14), `q12_q14` (MS-15..18), `safety` (MS-19..20). Safety-critical modules (MS-06 DiversionEngine, MS-07 DiverterController, MS-19 SafeStateEnter, MS-20 QpOverrideApi) carry the highest coverage gate (≥ 95%) and the strictest determinism requirement (1000× bitwise replay).

#### Coverage gap analysis

All 83 FS-IDs are covered by at least one DS-CM-NN CI. Cross-cutting FS-IDs receive multiple-CI coverage: FS-PERF-02 (diverter latency) is referenced by DS-CM-34 (per-actuation tracking) and DS-CM-80 (CQA-compute latency); FS-DI-03 (PTP) is referenced by DS-CM-67 (clock-skew gate) and indirectly by DS-CM-30 (high-rate ingest with PTP timestamps). No FS-ID is uncovered; no DS-ID is an orphan.

#### ICH Q13 / Q14 / Q12 compliance argument

The DS satisfies modern-regulatory continuous-manufacturing requirements through three coordinated design choices:

- **Q13 (Continuous Manufacturing):** batch-definition engine (DS-CM-21) supports the three regulator-recognised batch-boundary modes; material-tracking layer (DS-CM-22 / DS-CM-37) preserves per-time-resolution genealogy at slowest-RTD-residence-time; disturbance-response table (DS-CM-23) maps disturbance type → response and is PQ-validated.
- **Q14 (Analytical Procedure Lifecycle):** method-registry (DS-CM-25) enforces `apl_doc_id` per PAT method; model-loader (DS-CM-26) verifies cosign + version + dossier_id at startup; model-performance monitor (DS-CM-27) catches drift through rolling R²cv + RMSEP + residual-trend.
- **Q12 (Lifecycle Management):** per-EC recipe schema (DS-CM-18) classifies each EC with reporting category; EC-change gate (DS-CM-19) blocks recipe approval without CR-ID + RA signature for prior_approval/CBE_30 categories; audit-trail report runner (DS-CM-20) exports per-EC change history for regulatory submission.

The combination forms a coherent technical surface for continuous-manufacturing inspection — inspectors auditing Q13 readiness can verify batch-definition determinism via DS-CM-21 + OQ test; Q14 readiness via DS-CM-25/26/27 chain; Q12 readiness via DS-CM-18/19/20 chain.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
