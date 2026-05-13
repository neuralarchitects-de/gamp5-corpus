---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; v1.2 enrichment 2026-05-13"
seed_corpus_basis:
  - "OPH-URS-CM-001 (parent URS)"
  - "GAMP 5 (2nd ed.) Cat 5 conventions for custom control software"
  - "21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; EU GMP Annex 15"
  - "ICH Q13 (Continuous Mfg); ICH Q14; ICH Q12; ICH Q8/Q9/Q10"
  - "FDA CSA (Feb 2026); ANSI/ISA-88; ANSI/ISA-95; IEC 61511 SIL 2"
parent_urs:
  document_number: OPH-URS-CM-001
  version: 1.2
  file: ../../URS/_generated/final/Continuous_Manufacturing_Control_System__Ophir_BioSciences_URS_v1.3.md
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

## Continuous Manufacturing Control System — Site-Authored CM Orchestrator (Python + Ignition + AB ControlLogix)

**Document Number:** OPH-FS-CM-001
**Version:** 1.2
**Effective Date:** 2026-05-13 *(synthetic)*
**Parent URS:** OPH-URS-CM-001 v1.2
**Site:** Ophir BioSciences (fictional)
**System Class:** GAMP Cat 5 — Custom Application
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; EU GMP Annex 15; ICH Q13; ICH Q14; ICH Q12; ICH Q9/Q10; PIC/S PI 041; ANSI/ISA-88; ANSI/ISA-95; IEC 61511

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Continuous Mfg SME) | _____________ | _____________ | _____ |
| Reviewer (PAT Scientist) | _____________ | _____________ | _____ |
| Reviewer (Functional Safety Engineer) | _____________ | _____________ | _____ |
| Reviewer (Quality IT Lead) | _____________ | _____________ | _____ |
| Approver (Head of Continuous Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |
| Approver (Qualified Person) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-13 | (synthetic) | Expanded to per-URS-ID specifications (no range compression) per METHODOLOGY § 2A.7. Added state-of-control + design-space, ICH Q12 Established Conditions, ICH Q13 batch definition, ICH Q14 APL gate, RTD genealogy, diverter-actuation latency. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

Specify the site-developed continuous-manufacturing CM Orchestrator orchestrating Ignition SCADA + PAT (NIR / Raman / mass-flow / particle-size) + ControlLogix safety PLC to satisfy `OPH-URS-CM-001` v1.2.

## 2. Scope

Per parent URS § 2.

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source / Vendor |
|---|---|---|---|---|
| C-01 | CM Orchestrator (Python service) | Custom app | 5 | Site (Quality IT) |
| C-02 | Ignition 8.3 Gateway cluster | COTS SCADA | 4 | Inductive Automation |
| C-03 | ControlLogix 5580 safety PLC | Embedded | 4 (SIL 2 partition) | Rockwell Automation |
| C-04 | OpenShift cluster | COTS infra | (infra) | Red Hat |
| C-05 | PostgreSQL 16 | COTS DB | (infra) | (vendor) |
| C-06 | NIR PAT (blend uniformity + CU) | PAT instr | 4 | (vendor — separate URS) |
| C-07 | Raman PAT (assay) | PAT instr | 4 | (vendor — separate URS) |
| C-08 | LIW Feeders + mass-flow PAT | PAT instr | 4 | (vendor — separate URS) |
| C-09 | Particle-size PAT (acoustic + light-scatter) | PAT instr | 4 | (vendor — separate URS) |
| C-10 | Diverter mechanism (pneumatic gate) | Equipment | 4 (with SIL-2 trip) | (vendor) |
| C-11 | PAS-X v3.2 | COTS MES | 4 (separate URS/FS) | Werum / Körber |
| C-12 | MasterControl eQMS | COTS eQMS | 4 | MasterControl |
| C-13 | Aspen IP.21 historian | COTS historian | 4 | AspenTech |
| C-14 | HashiCorp Vault | COTS secrets | (infra) | HashiCorp |
| C-15 | AD / PKI | COTS infra | (infra) | Microsoft |
| C-16 | PTP master | COTS infra | (infra) | (site) |

### 3.2 Logical Architecture

```
                ┌──────────────────────────────────────────────┐
                │              PAS-X v3.2                        │
                └──────┬─────────────────────────────────┬─────┘
                       │ recipe / batch report              │
                       ▼                                    ▼
   ┌──────────────────────────────────────────────────────────────┐
   │   CM Orchestrator (Cat 5, Python) — HA on OpenShift           │
   │   - Recipe engine (ICH Q13 control strategy)                  │
   │   - State-of-control + SPC engine (Q10)                       │
   │   - PAT-fusion + RTRT decision                                │
   │   - Material-tracking (RTD model)                             │
   │   - Diverter command + actuator-health monitor                │
   │   - EC-change gate (Q12)                                      │
   │   - QP override endpoint                                      │
   └────────┬────────────────────┬────────────────────┬────────────┘
            │                    │                    │
            ▼                    ▼                    ▼
        Ignition SCADA        PAT instr.        ControlLogix
        (DCS / phase logic)   (NIR/Raman/...)   safety PLC + diverter
            │                                       │
            ▼                                       ▼
        Aspen IP.21                              SIS / safe-state
        historian                                logic (SIL 2)
```

### 3.3 Functional Modules

| Module | URS sections |
|---|---|
| M-PLAT | URS-PLAT-* |
| M-REC | URS-REC-* |
| M-SOC | URS-SOC-* |
| M-Q12 | URS-Q12-* |
| M-Q13 | URS-Q13-* |
| M-Q14 | URS-Q14-* |
| M-RUN | URS-RUN-* |
| M-MAT | URS-MAT-* |
| M-DEV | URS-DEV-* |
| M-AUD | URS-AUD-* |
| M-PART11 | URS-PART11-* |
| M-INT | URS-INT-* |
| M-DI | URS-DI-* |
| M-PERF | URS-PERF-*, URS-BAK-* |
| M-SEC | URS-SEC-* |
| M-TRN | URS-TRN-* |
| M-PR | URS-PR-* |

## 4. Functional Specifications

### 4.1 Platform / Hardware (M-PLAT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | Orchestrator deployed as 3 active replicas + 1 DR replica on site OpenShift; HAProxy + health-check; DR cluster in secondary DC; Ignition Gateway N+1 cluster with hot failover. |
| FS-PLAT-02 | URS-PLAT-02 | UPS for OpenShift nodes ≥ 30 min; ControlLogix safety functions revert to SAFE_STATE on power loss; diverter holds last commanded position with SIL-2 fail-safe to REJECT. |
| FS-PLAT-03 | URS-PLAT-03 | Process-control VLAN (VLAN 521); no L3 route to office network; firewalled at OT-DMZ. |
| FS-PLAT-04 | URS-PLAT-04 | At process start + on every module reload, Orchestrator runtime verifies cosign signature of all loaded Python modules + container images against trusted-keys store; verification failure halts startup; verified `OQ-COSIGN-VERIFY-01`. |
| FS-PLAT-05 | URS-PLAT-05 | Replica distribution constraint via OpenShift PodAntiAffinity across ≥ 2 physical fault domains. |

### 4.2 Recipe / Control-Strategy Lifecycle (M-REC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REC-01 | URS-REC-01 | Recipe state machine {DRAFT, REVIEW, APPROVED, EFFECTIVE, OBSOLETE} enforced server-side. |
| FS-REC-02 | URS-REC-02 | Recipe schema validates: CQA list, CPP list, diversion rules, PAT-source bindings. |
| FS-REC-03 | URS-REC-03 | Cycle-load endpoint validates state = EFFECTIVE; non-EFFECTIVE rejected. |
| FS-REC-04 | URS-REC-04 | Re-authenticated electronic signature at each transition; role-restricted + SoD enforced. |
| FS-REC-05 | URS-REC-05 | EFFECTIVE recipes immutable (DB constraint + service guard); change creates revision N+1 in DRAFT. |
| FS-REC-06 | URS-REC-06 | Recipe-schema validator (JSON Schema-based) enforces ICH Q13 fields; missing / out-of-range blocks approval; verified `OQ-REC-PARAM-ENFORCE-01`. |
| FS-REC-07 | URS-REC-07 | Recipe-diff renderer presents field-by-field old/new + change-reason. |

### 4.3 State-of-Control + Design-Space (M-SOC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SOC-01 | URS-SOC-01 | Design-space monitor evaluates per-tick CPP / CQA tuple against recipe-encoded design-space polytope; excursion logs "design-space breach" event + raises alarm + auto-creates eQMS deviation; verified `OQ-DESIGN-SPACE-MON-01`. |
| FS-SOC-02 | URS-SOC-02 | State-of-control indicator computed from rolling diversion-rate + CPP-drift slope + alarm-frequency; thresholds recipe-defined; loss-of-state triggers campaign-pause-review workflow; verified `OQ-STATE-OF-CONTROL-01`. |
| FS-SOC-03 | URS-SOC-03 | SPC layer implements CUSUM + EWMA on configured CQAs / CPPs; Western Electric + Nelson rules; alarms feed the alarm engine; verified `OQ-SPC-ALARMS-01`. |
| FS-SOC-04 | URS-SOC-04 | State-of-control + design-space metrics exposed via REST to APR ingestion. |

### 4.4 ICH Q12 Established Conditions (M-Q12)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-Q12-01 | URS-Q12-01 | Recipe schema includes per-EC entry: ec_id, parameter_path, reporting_category (enum: prior_approval, CBE_30, annual, not_reportable); rendered in recipe cover sheet; verified `OQ-EC-CLASS-01`. |
| FS-Q12-02 | URS-Q12-02 | EC-change gate at recipe-approval: if any EC modified, change-control record-ID required; regulatory-affairs signature required for prior_approval / CBE_30; verified `OQ-EC-CHANGE-GATE-01`. |
| FS-Q12-03 | URS-Q12-03 | EC-change audit-trail report runner exports the per-EC change history with linked CR-IDs. |

### 4.5 ICH Q13 Continuous Manufacturing (M-Q13)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-Q13-01 | URS-Q13-01 | Batch-definition engine supports three modes: time_based (recipe-defined hours), equipment_volume_based (cumulative kg through unit op), production_volume_based (good-tablet count); boundary deterministic + reconstructable; verified `OQ-BATCH-DEFINITION-01`. |
| FS-Q13-02 | URS-Q13-02 | Material-tracking layer (FS-MAT-*) records per-time-resolution at ≤ slowest-RTD-residence-time; diverted-material genealogy preserved. |
| FS-Q13-03 | URS-Q13-03 | Disturbance-response table (config) maps disturbance-type → response (auto-divert / auto-pause / alarm-only); validated at PQ. |
| FS-Q13-04 | URS-Q13-04 | Per-method APL-doc-ID enforced at recipe-load (per FS-Q14-01). |

### 4.6 ICH Q14 Analytical Procedure (M-Q14)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-Q14-01 | URS-Q14-01 | Method-registry table stores apl_doc_id per PAT method; recipe-validation rejects recipes referencing methods without APL doc; verified `OQ-APL-GATE-01`. |
| FS-Q14-02 | URS-Q14-02 | Model-loader verifies cosign signature + model_id + model_version + validation_dossier_id at startup; mismatch blocks Orchestrator startup; verified `OQ-MODEL-VERIFY-01`. |
| FS-Q14-03 | URS-Q14-03 | Model-performance monitor computes rolling R²cv, RMSEP, residual-trend metrics; degradation > recipe threshold raises alarm + flags PAT-Scientist review queue; verified `OQ-MODEL-PERF-MON-01`. |

### 4.7 Run Execution / Diversion / RTRT (M-RUN)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RUN-01 | URS-RUN-01 | Setpoint-envelope evaluator; deviations classified info / warning / critical. |
| FS-RUN-02 | URS-RUN-02 | Critical-alarm types (PAT loss on CQA, sustained CPP excursion, diverter-actuator fault) require ack + reason; persistent until acknowledged. |
| FS-RUN-03 | URS-RUN-03 | High-rate ingest pipeline: PAT 5-20 Hz, process 1 Hz, all written to PostgreSQL + IP.21. |
| FS-RUN-04 | URS-RUN-04 | Diversion-decision engine: per-CQA rule evaluation in deterministic order; decision logged with inputs + thresholds + code_version; reconstructable from logs; verified `OQ-DIVERSION-DETERMINISTIC-01`. |
| FS-RUN-05 | URS-RUN-05 | Manual-override endpoint disabled during PRODUCT_RUN state; only ESTOP path available; verified `OQ-MANUAL-OVERRIDE-DENY-01`. |
| FS-RUN-06 | URS-RUN-06 | Control-strategy revalidation triggers: any change to instrument_id, calibration_window, control-strategy formula in the recipe; gate at recipe-approval. |
| FS-RUN-07 | URS-RUN-07 | Diverter-actuation latency measured per actuation (decision_ts → gate_position_ack_ts); P95 ≤ 100 ms enforced; > threshold raises warning; verified `OQ-DIVERTER-LATENCY-01`. |
| FS-RUN-08 | URS-RUN-08 | Actuator-health monitor tracks cycle-count, pressure-trend, position-sense error rate; predictive-maintenance alerts. |

### 4.8 Material Tracking + Genealogy (M-MAT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MAT-01 | URS-MAT-01 | RTD-model service computes per-unit-op residence-time distribution; model qualified at PQ (`PQ-RTD-MODEL-01`); revalidation on equipment change. |
| FS-MAT-02 | URS-MAT-02 | Time-resolved genealogy: API lot consumption (g/s) and per-feeder excipient lot consumption logged at 1 Hz; downstream genealogy reconstruction via RTD-convolution; verified `PQ-MAT-GENEALOGY-01`. |
| FS-MAT-03 | URS-MAT-03 | Diverted-material quarantine writes a genealogy record (divert_ts, RTD-back-projected input lots, quantity-mass-estimate); verified `OQ-DIVERT-QUARANTINE-01`. |
| FS-MAT-04 | URS-MAT-04 | Campaign-end mass-balance: closure_ε = (input − accepted − diverted − scrap); > recipe-threshold flags investigation. |

### 4.9 Custom Software (Cat-5) SDLC (M-DEV)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DEV-01 | URS-DEV-01 | SDLC controlled by `SDLC-CM-ORCH-001`: requirements → design → code → tests → security scan → UAT → release. |
| FS-DEV-02 | URS-DEV-02 | Site GitLab Enterprise; signed commits (GPG); protected-branch on `main`; peer-review + green CI required. |
| FS-DEV-03 | URS-DEV-03 | Unit-test coverage ≥ 95% on `control_strategy/`, `diversion/`, `rtd_model/`; gate on PR merge; verified `OQ-DEV-COVERAGE-01`. |
| FS-DEV-04 | URS-DEV-04 | CI pipeline runs SonarQube + Snyk + Bandit; criticals block merge. |
| FS-DEV-05 | URS-DEV-05 | cosign signs release tags; runtime verifies (FS-PLAT-04); verified `OQ-COSIGN-VERIFY-01`. |
| FS-DEV-06 | URS-DEV-06 | Release-bundle template requires release-notes + FS-DS-delta + regression-report + security-report + CR-link. |
| FS-DEV-07 | URS-DEV-07 | Each release carries CSA risk-classification (per FDA Feb 2026) + risk-justified-testing rationale doc; verified `OQ-CSA-RISK-DOC-01`. |

### 4.10 Audit Trail / Part 11 (M-AUD / M-PART11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit trail captures recipe lifecycle, diversion decisions, alarm acks, signatures, code releases, model deployments, EC changes. |
| FS-AUD-02 | URS-AUD-02 | DB-level append-only; revoked DELETE/UPDATE; DBA dual control. |
| FS-AUD-03 | URS-AUD-03 | Per-batch Quality Reviewer audit-trail UI; quarterly QA-Compliance platform review. |
| FS-AUD-04 | URS-AUD-04 | 25-y retention; immutable cold storage. |
| FS-PART11-01 | URS-PART11-01 | Signature renders printed name + date / time + meaning into audit + PDFs. |
| FS-PART11-02 | URS-PART11-02 | User-id uniqueness enforced via AD; non-reuse policy. |
| FS-PART11-03 | URS-PART11-03 | PKI-signed signature payload; tamper detection on read. |
| FS-PART11-04 | URS-PART11-04 | SoD policy engine; conflicts rejected. |
| FS-PART11-05 | URS-PART11-05 | Re-auth + MFA at every signature; cached creds disabled. |
| FS-PART11-06 | URS-PART11-06 | AD password policy per `SEC-AD-POLICY-001`. |
| FS-PART11-07 | URS-PART11-07 | Audit coverage per § 11.10(e); accurate-copy export per § 11.10(b); retention per § 11.10(c). |

### 4.11 Integrations (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-MES-01 | URS-INT-MES-01 | Recipes / batch-context downloaded from PAS-X via REST mTLS; SHA-256 + version validated. |
| FS-INT-MES-02 | URS-INT-MES-02 | Executed-batch report posted to PAS-X within 30 min of cycle end; retry with backoff. |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | Unacknowledged critical alarms past recipe-defined SLA auto-create MasterControl deviations via REST. |
| FS-INT-PAT-01 | URS-INT-PAT-01 | PAT subscriptions via OPC UA + REST mTLS; loss-of-signal watchdog (≥ 3 missed samples) triggers safe-state diversion per FS-RUN-04; verified `OQ-PAT-LOSS-SAFE-STATE-01`. |
| FS-INT-DCS-01 | URS-INT-DCS-01 | Ignition / DCS phase commands via OPC UA mTLS. |
| FS-INT-HIST-01 | URS-INT-HIST-01 | Channel data streamed to Aspen IP.21 via the IP.21 SDK adapter at native rate. |
| FS-INT-QP-01 | URS-INT-QP-01 | QP override endpoint requires QP-role + MFA signature with reason; override events POSTed to MasterControl deviation; verified `OQ-QP-OVERRIDE-01`. |

### 4.12 Data Integrity (M-DI)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | All record writes attributed to AD user-id. |
| FS-DI-02 | URS-DI-02 | Export as PDF + CSV + JSON. |
| FS-DI-03 | URS-DI-03 | PTP sync; clock-skew gate. |
| FS-DI-04 | URS-DI-04 | Originals immutable; derivations stored separately. |
| FS-DI-05 | URS-DI-05 | Control-strategy calculation engine deterministic; verified per `OQ-CALC-01` + IEEE-754 round-mode pin. |
| FS-DI-06 | URS-DI-06 | 25-y retention; ≤ 4 h retrieval. |

### 4.13a Upstream Feeder + Compactor (M-FEED)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-FEED-01 | URS-FEED-01 | Feeder mass-flow consumed at 10 Hz via OPC UA; rolling-deviation evaluator vs recipe setpoint; > tolerance raises alarm + feeds diversion engine. |
| FS-FEED-02 | URS-FEED-02 | Refill-event watcher tags channel-log with refill_state ∈ {steady, refill}; steady-state vs refill-window evaluations separated. |
| FS-FEED-03 | URS-FEED-03 | Compactor channels (force, gap, roll-speed) logged ≥ 1 Hz; CPP-envelope evaluator integrated. |
| FS-FEED-04 | URS-FEED-04 | Recipe-load handler queries feeder.calibration_state; any OUT_OF_CAL blocks. |

### 4.13b Simulator-Based Testing (M-SIM)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SIM-01 | URS-SIM-01 | SIMULATOR_MODE flag in Orchestrator config; PAT-input replay subsystem reads pre-recorded traces; actuator outputs intercepted (no physical actuation). |
| FS-SIM-02 | URS-SIM-02 | CI pipeline executes scenario regression in SIMULATOR_MODE; gate on PR merge. |
| FS-SIM-03 | URS-SIM-03 | Simulator runs tagged in audit + report (header "SIMULATOR — NON-PRODUCTION"). |

### 4.13c Post-Market Change Management (M-PMCM)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PMCM-01 | URS-PMCM-01 | Deployment endpoint requires linked-CR-ID; missing CR-ID rejected with HTTP 400. |
| FS-PMCM-02 | URS-PMCM-02 | Post-deployment monitoring window flag set on first N batches (recipe-defined); elevated review surfaced in QA dashboard. |

### 4.14 Performance / Availability / Backup / Security / Training / PR

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | CQA-compute pipeline latency budgeted ≤ 200 ms P95; load-tested under PAT ingest for 30 d; verified `PQ-PERF-CQA-LATENCY-01`. |
| FS-PERF-02 | URS-PERF-02 | Diverter-decision-to-actuation latency ≤ 100 ms P95; measured per actuation. |
| FS-AV-01 | URS-AV-01 | ≥ 99.5% availability during production windows; external-probe measured. |
| FS-BAK-01 | URS-BAK-01 | PostgreSQL nightly + continuous WAL → S3 object-lock; PITR. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore-test, witnessed. |
| FS-SEC-01 | URS-SEC-01 | AD-managed accounts; service accounts via HashiCorp Vault short-lived secrets. |
| FS-SEC-02 | URS-SEC-02 | Removable-media GPO-blocked. |
| FS-TRN-01 | URS-TRN-01 | LMS-recorded role-specific training. |
| FS-TRN-02 | URS-TRN-02 | Annual CM-decision-logic competency assessment for PAT Scientist + CM Lead + QP. |
| FS-PR-01 | URS-PR-01 | Annual periodic-review runbook auto-collects configuration drift, code-release register, audit-trail review, deviation summary, control-strategy verification, EC-change history, model-performance trends, RTD-qualification currency. |


### 4.15 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem with local OT cached credentials for offline operation. Conditional-access binding to policy `OT-SCADA Conditional Access (MFA at HMI session start; named-location restriction to plant network)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the recipe / batch history DB plus file-level capture of PLC program backups; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Interface Specifications

| IF ID | URS ID | Counterparty | Protocol | Direction | Notes |
|---|---|---|---|---|---|
| IF-MES-01 | URS-INT-MES-01 | PAS-X v3.2 | REST mTLS | inbound | recipe + batch-context |
| IF-MES-02 | URS-INT-MES-02 | PAS-X v3.2 | REST mTLS | outbound | batch report |
| IF-EQMS-01 | URS-INT-EQMS-01 | MasterControl | REST mTLS | outbound | deviation push |
| IF-PAT-01 | URS-INT-PAT-01 | NIR / Raman / LIW / PSD | OPC UA + REST mTLS | inbound | PAT signals + model outputs |
| IF-DCS-01 | URS-INT-DCS-01 | Ignition / DeltaV | OPC UA mTLS | bidirectional | phase commands |
| IF-HIST-01 | URS-INT-HIST-01 | Aspen IP.21 | IP.21 SDK | outbound | tags |
| IF-QP-01 | URS-INT-QP-01 | (UI + REST) | REST + UI | inbound | QP override |
| IF-AD-01 | URS-SEC-01 | AD / PKI | LDAPS / Kerberos | bidirectional | AuthN + sig certs |
| IF-PTP-01 | (DI-03) | PTP master | IEEE 1588 | inbound | time sync |

## 6. Data Model (high-level)

| Entity | Attributes (illustrative) |
|---|---|
| Recipe | recipe_id, version, state, cqa_list, cpp_list, diversion_rules, pat_bindings, ec_list[reporting_category], sha256, signatures[] |
| BatchInstance | batch_id, recipe_id, recipe_version, batch_def_mode, started_at, ended_at, state |
| ChannelLog | channel, ts, value, source_tag, quality_flag |
| PATSignal | instrument, ts, value, model_id, model_version, calibration_state |
| DiversionDecision | decision_id, batch_id, ts, inputs{}, threshold, decision, code_version, signature_id? |
| Genealogy | window_start, window_end, api_lot, excipient_lots[], rtd_state |
| Diversion | divert_id, batch_id, gate_actuation_ts, position_ack_ts, mass_estimate, genealogy_ref |
| Alarm | alarm_id, batch_id, severity, raised_at, ack_by, ack_at, reason |
| ECChange | ec_id, old, new, cr_id, reg_affairs_sig, ts |
| Release | release_id, ts, sha256, csa_risk_class, regression_report_id |
| Signature | sig_id, record_id, signer_id, meaning, ts, payload_hash |
| AuditEvent | event_id, user_id, action, entity, old, new, ts |

## 7. Non-Functional Specifications

| NFR ID | Specification |
|---|---|
| NFR-01 | CQA compute latency ≤ 200 ms P95 |
| NFR-02 | Diverter decision-to-actuation ≤ 100 ms P95 |
| NFR-03 | Availability ≥ 99.5% production hours |
| NFR-04 | Sustained ingest from PAT ≥ 30 d without loss |
| NFR-05 | Audit trail append-only; PKI tamper detection |
| NFR-06 | Retention ≥ 25 y from product expiry |
| NFR-07 | Replicas across ≥ 2 fault domains |
| NFR-08 | PAT-loss watchdog ≤ 3 missed samples |
| NFR-09 | Unit-test coverage ≥ 95% on safety-relevant modules |

## 8. Configuration Items (CI)

| CI ID | Item | Configured Value | Source |
|---|---|---|---|
| CI-01 | Orchestrator replicas | 3 + 1 DR | URS-PLAT-01 |
| CI-02 | UPS hold | ≥ 30 min | URS-PLAT-02 |
| CI-03 | cosign trust-store | site PKI | URS-PLAT-04 |
| CI-04 | Recipe states | DRAFT,REVIEW,APPROVED,EFFECTIVE,OBSOLETE | URS-REC-01 |
| CI-05 | SPC rules | Western Electric + Nelson | URS-SOC-03 |
| CI-06 | EC reporting categories | prior_approval, CBE_30, annual, not_reportable | URS-Q12-01 |
| CI-07 | Batch-def modes | time / equipment-volume / production-volume | URS-Q13-01 |
| CI-08 | Diverter latency budget | ≤ 100 ms P95 | URS-RUN-07 |
| CI-09 | PAT-loss watchdog | 3 missed samples | URS-INT-PAT-01 |
| CI-10 | RTD-model source | per-unit-op qualified | URS-MAT-01 |
| CI-11 | Coverage gate | ≥ 95% | URS-DEV-03 |
| CI-12 | Audit retention | ≥ 25 y | URS-AUD-04 |
| CI-13 | Backup window | nightly + WAL | URS-BAK-01 |
| CI-14 | Restore-test cadence | quarterly | URS-BAK-02 |

## 9. Constraints / Assumptions / Risks

- **Constraints:** Cat-5 SDLC governs Orchestrator code; PLC firmware follows IEC 61511 safety SDLC; PAT changes require revalidation per FS-RUN-06; ICH Q12 EC-class changes follow regulatory affairs CR.
- **Assumptions:** MES, eQMS, AD, Vault, PAT instruments validated; OpenShift cluster validated under `INFRA-OS-CSV-001`; multivariate model lifecycle governed under `PAT-MODEL-LCM-001`.
- **FS-level risks:** control-strategy code defect (FS-DEV-01..07 + FS-RUN-04 deterministic logging); PAT loss not triggering safe-state (FS-INT-PAT-01 watchdog); model staleness (FS-Q14-03); EC unreported change (FS-Q12-02 gate); diverter actuator failure (FS-RUN-07..08 + SIL-2 fail-safe); RTD model drift (FS-MAT-01 revalidation).

## 10. References

- OPH-URS-CM-001 v1.2 (parent URS).
- 21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; EU GMP Annex 15.
- ICH Q13 (FDA implementing 2024); ICH Q14; ICH Q12; ICH Q9(R1); ICH Q10; ICH Q8(R2).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026).
- ISPE GAMP 5 (2nd ed., 2022); ISPE Baseline Guide *Continuous Manufacturing of Solid Oral Dosage Forms*; PIC/S PI 041.
- ANSI/ISA-88 Part 1 + Part 2; ANSI/ISA-95 Part 1; IEC 61511.
- Directive 2001/83/EC Art. 51 (QP).

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID(s) | Notes |
|---|---|---|
| URS-PLAT-01 | FS-PLAT-01 | |
| URS-PLAT-02 | FS-PLAT-02 | |
| URS-PLAT-03 | FS-PLAT-03 | |
| URS-PLAT-04 | FS-PLAT-04 | |
| URS-PLAT-05 | FS-PLAT-05 | |
| URS-REC-01 | FS-REC-01 | |
| URS-REC-02 | FS-REC-02 | |
| URS-REC-03 | FS-REC-03 | |
| URS-REC-04 | FS-REC-04 | |
| URS-REC-05 | FS-REC-05 | |
| URS-REC-06 | FS-REC-06 | |
| URS-REC-07 | FS-REC-07 | |
| URS-SOC-01 | FS-SOC-01 | |
| URS-SOC-02 | FS-SOC-02 | |
| URS-SOC-03 | FS-SOC-03 | |
| URS-SOC-04 | FS-SOC-04 | |
| URS-Q12-01 | FS-Q12-01 | |
| URS-Q12-02 | FS-Q12-02 | |
| URS-Q12-03 | FS-Q12-03 | |
| URS-Q13-01 | FS-Q13-01 | |
| URS-Q13-02 | FS-Q13-02 | |
| URS-Q13-03 | FS-Q13-03 | |
| URS-Q13-04 | FS-Q13-04 | |
| URS-Q14-01 | FS-Q14-01 | |
| URS-Q14-02 | FS-Q14-02 | |
| URS-Q14-03 | FS-Q14-03 | |
| URS-RUN-01 | FS-RUN-01 | |
| URS-RUN-02 | FS-RUN-02 | |
| URS-RUN-03 | FS-RUN-03 | |
| URS-RUN-04 | FS-RUN-04 | |
| URS-RUN-05 | FS-RUN-05 | |
| URS-RUN-06 | FS-RUN-06 | |
| URS-RUN-07 | FS-RUN-07 | |
| URS-RUN-08 | FS-RUN-08 | |
| URS-MAT-01 | FS-MAT-01 | |
| URS-MAT-02 | FS-MAT-02 | |
| URS-MAT-03 | FS-MAT-03 | |
| URS-MAT-04 | FS-MAT-04 | |
| URS-DEV-01 | FS-DEV-01 | |
| URS-DEV-02 | FS-DEV-02 | |
| URS-DEV-03 | FS-DEV-03 | |
| URS-DEV-04 | FS-DEV-04 | |
| URS-DEV-05 | FS-DEV-05 | |
| URS-DEV-06 | FS-DEV-06 | |
| URS-DEV-07 | FS-DEV-07 | |
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
| URS-INT-MES-01 | FS-INT-MES-01 / IF-MES-01 | |
| URS-INT-MES-02 | FS-INT-MES-02 / IF-MES-02 | |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 / IF-EQMS-01 | |
| URS-INT-PAT-01 | FS-INT-PAT-01 / IF-PAT-01 | |
| URS-INT-DCS-01 | FS-INT-DCS-01 / IF-DCS-01 | |
| URS-INT-HIST-01 | FS-INT-HIST-01 / IF-HIST-01 | |
| URS-INT-QP-01 | FS-INT-QP-01 / IF-QP-01 | |
| URS-DI-01 | FS-DI-01 | |
| URS-DI-02 | FS-DI-02 | |
| URS-DI-03 | FS-DI-03 | |
| URS-DI-04 | FS-DI-04 | |
| URS-DI-05 | FS-DI-05 | |
| URS-DI-06 | FS-DI-06 | |
| URS-PERF-01 | FS-PERF-01 | |
| URS-PERF-02 | FS-PERF-02 | |
| URS-AV-01 | FS-AV-01 | |
| URS-BAK-01 | FS-BAK-01 | |
| URS-BAK-02 | FS-BAK-02 | |
| URS-SEC-01 | FS-SEC-01 | |
| URS-SEC-02 | FS-SEC-02 | |
| URS-FEED-01 | FS-FEED-01 | |
| URS-FEED-02 | FS-FEED-02 | |
| URS-FEED-03 | FS-FEED-03 | |
| URS-FEED-04 | FS-FEED-04 | |
| URS-SIM-01 | FS-SIM-01 | |
| URS-SIM-02 | FS-SIM-02 | |
| URS-SIM-03 | FS-SIM-03 | |
| URS-PMCM-01 | FS-PMCM-01 | |
| URS-PMCM-02 | FS-PMCM-02 | |
| URS-TRN-01 | FS-TRN-01 | |
| URS-TRN-02 | FS-TRN-02 | |
| URS-PR-01 | FS-PR-01 | |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

The following risks are noted for downstream evaluation in the Risk Assessment.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Defect in control-strategy code causing missed diversion of OOS material | Medium | Critical | URS-DEV-01..07 + URS-RUN-04 |
| R-02 | PAT loss not triggering safe state | Medium | High | URS-INT-PAT-01 |
| R-03 | Signature compromise | Medium | Medium | URS-DEV-05 cosign verify |
| R-04 | Audit-trail tampering | Low | Critical | URS-AUD-02 |
| R-05 | RTD-model drift leading to genealogy mis-assignment | Medium | High | URS-MAT-01 + revalidation triggers |
| R-06 | Multivariate model staleness causing false RTRT pass | Medium | Critical | URS-Q14-03 model-performance monitoring |
| R-07 | EC unreported regulatory change | Low | Critical | URS-Q12-01..02 EC gate |
| R-08 | Diverter actuator failure | Low | Critical | URS-RUN-07..08 + safe-state design |
| R-09 | State-of-control loss undetected (drift) | Medium | High | URS-SOC-01..03 + SPC alarms |
| R-10 | Design-space excursion without investigation | Low | High | URS-SOC-01 |
| R-11 | Race condition between diverter command + material-tracking propagation | Low | High | URS-RUN-04 deterministic + RTD-σ tolerance |
| R-12 | Mass-balance closure failure undetected | Medium | Medium | URS-MAT-04 |
| R-13 | QP override audit-gap (override not logged) | Low | Critical | URS-INT-QP-01 |
| R-14 | Loss of PTP causing audit-trail timestamp anomaly | Low | High | URS-INT-NTP via DI-03 |

Full evaluation in `OPH-RA-CM-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
