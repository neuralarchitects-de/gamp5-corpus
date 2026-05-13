---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (FS catch-up to URS v1.2 — T3 enrichment)"
seed_corpus_basis:
  - "CRC-URS-BIOSCADA-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd ed.) Cat 5 conventions for site-customised SCADA"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11; Annex 1; Annex 2; ICH Q9(R1); ICH Q13"
  - "PIC/S PI 041; ISA-88; ISA-95; ISA-101; ISA-18.2; IEC 61511"
  - "FDA CSA (Feb 2026); FDA PAT (2004); FDA Q13 (2024)"
  - "USP <1043>; ATMP Guidelines"
parent_urs:
  document_number: CRC-URS-BIOSCADA-001
  version: "1.2"
  file: "../../URS/_generated/final/Bioreactor_Continuous_Fermentation_SCADA__Crocus_Pharma_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# Functional Specification (FS)

## Bioreactor Continuous-Fermentation SCADA — Inductive Automation Ignition 8.3 + Emerson DeltaV v15.3 + Site Python Orchestrator (Cat 5)

**Document Number:** CRC-FS-BIOSCADA-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** CRC-URS-BIOSCADA-001 v1.2 | **Site:** Crocus Pharma (Suzhou) Plant 1 *(fictional)*
**System Class:** GAMP Cat 5 — Custom Application (Ignition 8.3 + DeltaV v15.3 platform = Cat 4; site-developed Python Orchestrator + APC + SoftSensor = Cat 5)
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Annex 1 (2022); EU GMP Annex 2; ICH Q9(R1); ICH Q11; ICH Q13; USP <1043>; ISA-88; ISA-95; ISA-101; ISA-18.2; IEC 61511; PIC/S PI 041.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Bioprocess Engineer) | _____________ | _____________ | _____ |
| Reviewer (PAT Chemometrician) | _____________ | _____________ | _____ |
| Reviewer (Functional Safety Engineer) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Approver (Head of Biologics Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Minor: PAT-loss safe-state implementation detail clarified. |
| 1.2 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.2 (T3 enrichment): every URS-ID expanded to its own FS row with per-ID implementation; recipe-phase state machine, feed/perfusion control, PAT chemometrics, single-use/stainless config, ATMP mode, ISA-88/95/101/18.2 implementations added. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies the deployment, configuration, and integration of the bioreactor continuous-fermentation SCADA at Crocus Pharma Plant 1 to satisfy `CRC-URS-BIOSCADA-001` v1.2.

## 2. Scope

Per the URS: Ignition 8.3 gateway cluster (active + DR), DeltaV v15.3 DCS + DeltaV SIS (SIL 2 partition), site-developed Python Orchestrator on OpenShift 4.14 (3 replicas + DR), PAT instruments (Kaiser RamanRxn4 + Hamilton Incyte + Thermo Prima Pro + Sartorius BioPAT Spectro), Sartorius Biostat STR-200 / Cytiva XDR / ABEC CSTR configurations, Repligen ATF 6 perfusion skids, Watson-Marlow Quantum feed pumps, integrations with PAS-X v3.2 (recipe / batch), MasterControl eQMS, Aspen IP.21 historian, Watson LIMS, BMS, AD `crocus.local`.

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | GAMP Cat | Notes |
|---|---|---|---|
| C-01 | Ignition 8.3 gateway (active cluster) | 4 | platform; N+1 |
| C-02 | Ignition 8.3 gateway (DR) | 4 | replicated; ≤ 60 s failover |
| C-03 | Site Python Orchestrator (Cat 5) | **5** | ~6,500 LOC; OpenShift 4.14; 3 replicas + DR |
| C-04 | Site Python APC / SoftSensor modules | **5** | sub-modules, each with own SDLC artefacts |
| C-05 | Emerson DeltaV v15.3 DCS controllers | 4 | redundant pair per ref. arch. |
| C-06 | Emerson DeltaV SIS (SIL 2) | 4 | safety partition; IEC 61511 |
| C-07 | PAS-X v3.2 | 4 | recipe / batch counterparty |
| C-08 | Aspen IP.21 historian | 4 | tag stream consumer |
| C-09 | MasterControl eQMS | 4 | deviation counterparty |
| C-10 | Watson LIMS | 4 | material + ATMP donor counterparty |
| C-11 | Kaiser RamanRxn4 PAT | 4 | OPC UA / mTLS |
| C-12 | Hamilton Incyte capacitance | 4 | OPC UA / mTLS |
| C-13 | Thermo Prima Pro off-gas mass-spec | 4 | OPC UA / mTLS |
| C-14 | Sartorius BioPAT Spectro VCD | 4 | OPC UA / mTLS |
| C-15 | Repligen ATF 6 perfusion skid | 4 | embedded firmware |
| C-16 | Watson-Marlow Quantum feed pumps | 4 | rotation+flow cross-check |
| C-17 | BMS (utility status) | 4 | interlock counterparty |
| C-18 | AD / Kerberos / PKI / PTP | (infra) | AuthN + signing + time |

### 3.2 Logical Architecture (textual)

```
                ┌──────────────────────────────────────────────┐
                │   AD/Kerberos │ PKI │ PTP IEEE 1588 master    │
                └────────────────────┬─────────────────────────┘
                                     │
   ┌─────────────────────────────────▼─────────────────────────────────┐
   │           Ignition 8.3 (active cluster + DR)                       │
   │   ┌────────────────────────┐  ┌───────────────────────────────┐   │
   │   │  Vision/Perspective    │  │  Site Python Orchestrator (5) │   │
   │   │  HMI (ISA-101)         │  │   - State machine (ISA-88)    │   │
   │   └────────────────────────┘  │   - APC + SoftSensor          │   │
   │                                │   - PAT-loss safe-state       │   │
   │                                │   - Determinism-verified math │   │
   │                                └───────────────────────────────┘   │
   └────────┬───────────────────────────────┬──────────────────────────┘
            │                               │
            ▼                               ▼
        DeltaV v15.3                  PAT bus (OPC UA mTLS)
        + DeltaV SIS (SIL 2)          Raman / Capacitance /
        (recipe execution)            Off-gas / VCD
            │                               │
            ▼                               ▼
        Reactor train               Cell-retention (ATF 6)
        (Biostat STR /              + feed pumps + bleed
         Cytiva XDR /
         ABEC CSTR)
            │
            ▼
        PAS-X v3.2  ◄──recipe──▶  MasterControl eQMS
        Aspen IP.21 (historian)   Watson LIMS (USP <1043>)
        BMS (interlocks)
```

### 3.3 Cluster Topology

- **Orchestrator:** OpenShift 4.14, namespace `bioscada-prod`, 3 replicas + DR; PodDisruptionBudget min available = 2; HPA disabled in prod (deterministic load).
- **Ignition Gateway:** cluster mode with redundant tag providers; active gateways `gw1-3` + standby `gw4`.
- **DeltaV:** redundant ProfessionalPLUS + ApplicationStation; redundant M-series controllers; SIS logic-solver pair (SIL 2).
- **Historian:** Aspen IP.21 (separate validation); store-and-forward on the SCADA side via Ignition Tag Historian for blip recovery.

## 4. Functional Specifications

### 4.1 Platform / Hardware (URS § 5.1)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | OpenShift 4.14 `bioscada-prod` namespace runs Orchestrator with 3 replicas + DR (`bioscada-dr` in geo-paired site); Ignition Gateway cluster `gw1-gw4` with automatic failover ≤ 60 s; DeltaV redundant pair per Emerson reference; failover events logged to `audit_events` and surfaced on the HMI `gw-cluster-health` faceplate. |
| FS-PLAT-02 | URS-PLAT-02 | Schneider Galaxy UPS sized for ≥ 30 min hold; DeltaV SIS on isolated UPS branch; default-safe-state config: perfusion pumps stop, glucose-feed pump stops, agitator at 30 rpm minimum, jacket holds last-known setpoint, vent-valve open. |
| FS-PLAT-03 | URS-PLAT-03 | Process-control VLAN 312 (Purdue Level 2/3); firewall + DMZ between SCADA / DCS and corporate; only allow-listed egress to PAS-X / eQMS / IP.21 / LIMS endpoints. |
| FS-PLAT-04 | URS-PLAT-04 | Meinberg PTP grandmaster + boundary clocks; max skew ≤ 1 ms continuously monitored via Prometheus `ptp_skew_milliseconds` exporter; > 1 ms raises `PTP_SKEW_DEGRADED` alarm. |
| FS-PLAT-05 | URS-PLAT-05 | Hardware / firmware refresh under approved CR; impact assessment per change-control SOP `CRC-SOP-CR-001`; revalidation scope = full or partial per RA outcome. |

### 4.2 Recipe / Control-Strategy Lifecycle (URS § 5.2)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REC-01 | URS-REC-01 | Recipe lifecycle implemented as Postgres table `recipe_versions` with status enum `DRAFT / REVIEW / APPROVED / EFFECTIVE / OBSOLETE`; transitions enforced by stored procedures + signature checks. |
| FS-REC-02 | URS-REC-02 | ISA-88 three-level hierarchy persisted in `master_recipe`, `site_recipe`, `control_recipe` tables; foreign keys enforce version-pinned cross-level references. |
| FS-REC-03 | URS-REC-03 | Recipe schema fields include `cqa_list`, `cpp_envelope`, `pat_rule_set`, `perfusion_schedule`, `feed_strategy_envelope`, `harvest_decision_rules`, `alarm_thresholds`. |
| FS-REC-04 | URS-REC-04 | Runtime API `GET /api/recipes/effective` returns only `status='EFFECTIVE'`; other statuses return HTTP 404. |
| FS-REC-05 | URS-REC-05 | `EFFECTIVE` recipes immutable: ON-UPDATE/DELETE database triggers raise exception; SCADA UI hides edit controls on EFFECTIVE state. |
| FS-REC-06 | URS-REC-06 | Transition endpoint `POST /api/recipes/transition` requires signed-JWT payload `{recordId, recordHash, signerId, meaning, signatureBlock}`; dual-sign enforced via two-token validation. |
| FS-REC-07 | URS-REC-07 | Recipe download from PAS-X validates SHA-256 + version; mismatch returns HTTP 409 + creates MasterControl deviation. |
| FS-REC-08 | URS-REC-08 | Recipe APPROVAL workflow checks referenced PAT-model + phase-logic versions; broken references reject with `RECIPE_BROKEN_REFS`. |
| FS-REC-09 | URS-REC-09 | Recipe-change CR template captures impacted CQAs/CPPs + ICH Q12 EC classification + variation-status flag. |

### 4.3 Recipe Phases — ISA-88 Batch State Machine (URS § 5.3)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PHASE-01 | URS-PHASE-01 | ISA-88 procedural-control hierarchy implemented as `procedure → unit_procedure → operation → phase` tables; each Phase is a versioned artefact in GitLab `bioscada-phases` repo; deployment under Cat-5 SDLC. |
| FS-PHASE-02 | URS-PHASE-02 | State machine `PhaseStateMachine` with enum: `INOCULATION`, `EXPONENTIAL_GROWTH`, `STEADY_STATE_PERFUSION`, `HARVEST_DECISION`, `HARVEST_BLEED`, `CAMPAIGN_END`, `CIP`, `SIP`; transitions guarded by entry/exit conditions in `phase_rules.yaml`. |
| FS-PHASE-03 | URS-PHASE-03 | Phase transitions logged to `phase_events` with PTP timestamp + entry/exit-condition snapshot + signing user; immutable. |
| FS-PHASE-04 | URS-PHASE-04 | Each Phase declares `safe_state_on_pat_loss`, `safe_state_on_utility_loss`, `safe_state_on_abort` in `phase_safe_state.yaml`; validated at recipe APPROVAL. |
| FS-PHASE-05 | URS-PHASE-05 | Out-of-envelope phase transition requires Operator + Senior Operator dual-sign with reason ≥ 10 chars; recorded with input-snapshot pointer in executed-batch report. |
| FS-PHASE-06 | URS-PHASE-06 | Phase metrics exposed via Prometheus exporter `phase_duration_seconds`, `phase_deviation_count`, `phase_signed_events_count`; dashboard `CRC-GR-PHASE`. |

### 4.4 Feed and Perfusion Control (URS § 5.4)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-FEED-01 | URS-FEED-01 | `GlucoseFeedController` consumes Raman PLS predictions; control rule version pinned to EFFECTIVE recipe via `feed_rule_version` FK; rule outputs setpoint to Watson-Marlow Quantum pump via OPC UA. |
| FS-FEED-02 | URS-FEED-02 | `PerfusionController` consumes capacitance + on-line VCD with Kalman-filter sensor fusion; sensor loss demotes control authority per `PerfusionAuthorityMatrix`; output drives ATF 6 exchange-rate setpoint. |
| FS-FEED-03 | URS-FEED-03 | Override workflow requires both Operator + Senior Operator signatures; override event written to `override_events` with input-snapshot pointer (S3 URI). |
| FS-FEED-04 | URS-FEED-04 | Pump-integrity check: every 5 s `rotation_sensor` vs `flow_meter` cross-check; mismatch ≥ 5% for > 60 s triggers `PUMP_CROSSCHECK_FAIL` critical alarm + fallback to validated open-loop schedule. |
| FS-FEED-05 | URS-FEED-05 | `BleedRateController` maintains target VCD; deviation alarms classified per `bleed_alarm_table.yaml`. |
| FS-FEED-06 | URS-FEED-06 | TMP + flux trends consumed from ATF 6 telemetry; `FoulingPredictor` runs hourly, raises `ATF_FOULING_PRECURSOR` maintenance alarm at threshold. |

### 4.5 PAT Integration and Chemometric-Model Lifecycle (URS § 5.5)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PAT-01 | URS-PAT-01 | OPC UA over TLS with mTLS to each PAT instrument; tag-quality attribute consumed via `PatQualityGate`; quality < `GOOD_LOCAL_OVERRIDE` raises alarm. |
| FS-PAT-02 | URS-PAT-02 | PAT models stored as MLflow-tracked artefacts with state enum `DRAFT / CALIBRATED / CROSS-VALIDATED / APPROVED / EFFECTIVE / OBSOLETE`; lifecycle gates signed. |
| FS-PAT-03 | URS-PAT-03 | Runtime model loader verifies `model_version == effective_recipe.pat_model_version`; mismatch rejects prediction with `PAT_MODEL_VERSION_MISMATCH`. |
| FS-PAT-04 | URS-PAT-04 | `PatLossHandler` activates recipe-defined safe-state: open-loop feed schedule + APC demotion + deviation creation; deterministic, reproducible from logged inputs + code-version + PAT-model-version. |
| FS-PAT-05 | URS-PAT-05 | On-line residual / Hotelling T² / Q-statistic computed per ASTM E2476 by `PatPerformanceMonitor`; OOS conditions alarmed `PAT_MODEL_OUT_OF_CONTROL`. |
| FS-PAT-06 | URS-PAT-06 | Reference-method calibration triggered at recipe-defined cadence (default 12 h steady-state); off-line HPLC / cell-counter results consumed from Watson LIMS; delta logged. |
| FS-PAT-07 | URS-PAT-07 | PAT-model approval workflow: Chemometrician + Process Sciences + QA sign; regulator-impacting changes linked to `variation_record_id` in regulatory-reporting service. |

### 4.6 Run Execution and Continuous Control (URS § 5.6)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RUN-01 | URS-RUN-01 | `RecipeRunner` evaluates setpoint deviations every 250 ms; alarm classification per `alarm_table.yaml`. |
| FS-RUN-02 | URS-RUN-02 | Critical alarms persist with `selfAcknowledgement = false`; operator acknowledges with reason ≥ 10 chars; reason persisted in `alarm_events` table. |
| FS-RUN-03 | URS-RUN-03 | InfluxDB write rate 1 Hz on CPP tags; PAT cadence per instrument (Raman 1 spectrum / min, capacitance 30 s, off-gas 5 s, VCD 30 s); PLC scan 100 ms with on-change deadband. |
| FS-RUN-04 | URS-RUN-04 | Decision payload schema: `decision_id`, `recipe_version`, `pat_model_version`, `code_release`, `input_snapshot_uri`, `output`, `timestamp_ptp`; bitwise reproducibility verified at OQ via FS-DEV-07. |
| FS-RUN-05 | URS-RUN-05 | Override workflow as FS-FEED-03; override flagged in `executed_batch_report.overrides[]` with snapshot pointer. |
| FS-RUN-06 | URS-RUN-06 | Reuses FS-PAT-04 PatLossHandler. |
| FS-RUN-07 | URS-RUN-07 | PAS-X production-order ingestion is transactional (DB transaction + idempotent recipe-load); failure rolls back. |
| FS-RUN-08 | URS-RUN-08 | Out-of-sequence operator commands rejected by `CommandSequenceGuard`; authorised override requires signed reason. |

### 4.7 Alarm Management — ISA-18.2 (URS § 5.7)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ALM-01 | URS-ALM-01 | Alarm rationalisation table `alarm_rationalisation.yaml` classifies each tag `INFO/WARNING/CRITICAL/SIS` with response, ack-requirement, escalation path. |
| FS-ALM-02 | URS-ALM-02 | Criticals require ack with reason ≥ 10 chars; unacknowledged > T_escalate triggers SMS + email to on-call. |
| FS-ALM-03 | URS-ALM-03 | Alarm-flood detector: rate > N/min triggers shelving per ISA-18.2; shelving events logged to `alarm_shelving_events`. |
| FS-ALM-04 | URS-ALM-04 | SIS alarms handled by DeltaV SIS SIL 2 partition; events mirrored to `sis_events` table; bypassed only with FSE-signed CR. |
| FS-ALM-05 | URS-ALM-05 | Prometheus exporter `alarm_metrics`: rate, ack-latency P50/P95, top-talkers, shelving frequency; dashboard `CRC-GR-ALARMS`. |

### 4.8 HMI — ISA-101 (URS § 5.8)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-HMI-01 | URS-HMI-01 | Perspective views hierarchical Level 1-4 per ISA-101; navigation budget ≤ 3 clicks audited in HMI design review `CRC-HMI-DR-01`. |
| FS-HMI-02 | URS-HMI-02 | High-performance HMI palette: greys for normal, saturated colours only for abnormal indications; alarm-priority colour map fixed (red=critical, amber=warning, blue=info, magenta=SIS). |
| FS-HMI-03 | URS-HMI-03 | Faceplate response measured via synthetic monitoring; P95 ≤ 500 ms; SLO tracked. |
| FS-HMI-04 | URS-HMI-04 | HMI changes via approved CR; non-prod gateway `gw-test` runs regression before deploy. |

### 4.9 Custom Software (Cat-5) SDLC (URS § 5.9)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DEV-01 | URS-DEV-01 | Cat-5 SDLC documented in `CRC-SOP-IT-CAT5-001`; CI workflows enforce each gate. |
| FS-DEV-02 | URS-DEV-02 | Source repo `git.crocus.local/bioprocess/orchestrator`; branch protection: 1+ reviewer + passing CI + signed commits (Sigstore). |
| FS-DEV-03 | URS-DEV-03 | Coverage measured by coverage.py + JaCoCo (where Java sub-modules); fails CI < 95% on `safety/*` packages. |
| FS-DEV-04 | URS-DEV-04 | CI runs Ruff + mypy --strict + Bandit on Python; Trivy on container images; critical findings break build. |
| FS-DEV-05 | URS-DEV-05 | Releases packaged as signed container images via cosign; runtime verifies signature against `crocus-sigstore-pubkey-2026q2`. |
| FS-DEV-06 | URS-DEV-06 | Release manifest `manifest.yaml` lists release notes, FS / DS deltas, regression summary, security-scan path, CR ID. |
| FS-DEV-07 | URS-DEV-07 | Determinism harness: OQ pins random seed + repeats 1000× on canonical input set; bitwise reproducibility required; floating-point IEEE-754 round-mode pin enforced via `numpy.errstate`. |
| FS-DEV-08 | URS-DEV-08 | Trivy + Snyk Container in CI; HIGH/CRITICAL CVE blocks promotion. |

### 4.10 Audit Trail / 21 CFR Part 11 / Data Integrity (URS § 5.10)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit events written to `audit_events` with full ALCOA+ fields: `actor_id`, `action`, `old_value`, `new_value`, `reason`, `timestamp_ptp`, `record_hash`. |
| FS-AUD-02 | URS-AUD-02 | DB role `app_role` has INSERT/SELECT only on `audit_events`; UPDATE/DELETE denied; admin role gated by break-glass procedure with QA witness. |
| FS-AUD-03 | URS-AUD-03 | `Audit Trail Review` Perspective view filterable by date / actor / action; export PDF/A-3 + JSONL; review records signed. |
| FS-AUD-04 | URS-AUD-04 | Retention 25 y in `audit_events_archive` (S3 with object-lock + cross-region replication). |
| FS-AUD-05 | URS-AUD-05 | Control-action audit entries include `input_snapshot_uri` (S3) for full reconstruction; reconstruction OQ test `OQ-AUD-RECONSTRUCT-01`. |
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural controls documented in `/sop/` SharePoint library; reviewed annually. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(d): AD-mapped Kerberos auth + MFA (Yubikey); service accounts mTLS-only. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(e): operational audit per FS-AUD-01. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.50: e-signature endpoint enforces `printedName + dateTime + meaning`; meaning enum (`authorship`, `review`, `approval`, `release`, `retirement`, `verification`); role-matrix denies SoD violations. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.70: signature payload includes SHA-256(record); subsequent edit invalidates signature; tampered records flagged on read. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.100: AD signer mapping fixed via HR-derived feed; reuse blocked at provisioning. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.200: re-auth required at sign-off (fresh Kerberos ticket, max-age 5 min); cached creds rejected. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.300: AD password policy ≥ 14 chars + complexity + 90 d rotation + MFA. |
| FS-DI-01 | URS-DI-01 | DB NOT-NULL constraint on `actor_id` at audit-write. |
| FS-DI-02 | URS-DI-02 | Export endpoints produce PDF/A-3 + JSON / CSV; rendering validated at OQ. |
| FS-DI-03 | URS-DI-03 | PTP timestamps from DCS / PLC up; retroactive entries flagged with delay reason. |
| FS-DI-04 | URS-DI-04 | InfluxDB point-write only; corrections recorded as new annotated tags referencing original; PAT raw frames archived to S3. |
| FS-DI-05 | URS-DI-05 | Determinism + arithmetic validated at OQ via FS-DEV-07 + regression dataset. |
| FS-DI-06 | URS-DI-06 | Metadata completeness validated by `CompletenessChecker`; retrievable within 1 BD via archive-query API. |

### 4.11 Single-Use vs Stainless Configuration Management (URS § 5.11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CFG-01 | URS-CFG-01 | `BioreactorConfigMatrix` declares per-configuration parameters (Sartorius STR / Cytiva XDR / Thermo HyPerforma / ABEC CSTR / Pall Allegro); EFFECTIVE recipe pins active config via `bioreactor_config_id`. |
| FS-CFG-02 | URS-CFG-02 | Config-specific envelopes enforced at recipe-load + at runtime; cross-config leakage rejected with `CONFIG_ENVELOPE_LEAKAGE`. |
| FS-CFG-03 | URS-CFG-03 | Single-use bag scan (bag-id + manufacturer + lot + expiry) captured at batch start via barcode scanner; verified against Watson LIMS; mismatch / expired blocks start with `SINGLE_USE_INVALID`. |
| FS-CFG-04 | URS-CFG-04 | Config changeover CR template `CR-CFG-CHANGEOVER` requires revalidation scope per impact assessment. |

### 4.12 ATMP Cell-Therapy Mode (URS § 5.12)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ATMP-01 | URS-ATMP-01 | `AtmpIsolationGuard` enforces: one ATMP patient batch per train; cross-patient prevention via interlock on shared-resource access; violation creates immediate `ATMP_CROSSOVER_RISK` critical deviation. |
| FS-ATMP-02 | URS-ATMP-02 | Donor-traceability metadata schema `{donor_id_deidentified, tissue_bank_ref, donor_lot}` captured at batch start; flows to PAS-X + Watson LIMS for COI / COC. |
| FS-ATMP-03 | URS-ATMP-03 | `Usp1043MaterialCheck` queries Watson LIMS for ancillary-material qualification status (lot + expiry + qualification record); non-qualified / expired blocks start. |
| FS-ATMP-04 | URS-ATMP-04 | ATMP batches flagged `requires_qp_review = true`; PAS-X batch-closure workflow routes to QP queue. |

### 4.13 ISA-95 Enterprise Integration / Integrations (URS § 5.13)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-MES-01 | URS-INT-MES-01 | `RecipeFetcher` HTTP client → `https://pasx.crocus.local/api/v1/recipes/{id}/effective`; mTLS via `crocus-bioscada-2026q2` cert; SHA-256 + version validated. |
| FS-INT-MES-02 | URS-INT-MES-02 | `BatchReporter` posts profile + alarms + signatures + PAT-trace to `https://pasx.crocus.local/api/v1/batches`; idempotency key `batchId`; within 30 min of event. |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | `DeviationCreator` posts alarms unacknowledged > window to `https://eqms.crocus.local/api/v2/deviations`; idempotency key; retry with backoff 1/5/30 s. |
| FS-INT-PAT-01 | URS-INT-PAT-01 | OPC UA mTLS to PAT instruments; cert rotation every 365 days via cert-manager. |
| FS-INT-HIST-01 | URS-INT-HIST-01 | All GxP tags streamed to Aspen IP.21 via OPC HDA / OPC UA; Ignition Tag Historian store-and-forward for network blips; lossless verified at OQ. |
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | Watson LIMS REST `GET /materials/{lot}/status`; only `QC_RELEASED` accepted; ATMP donor metadata via `GET /donors/{deidentified_id}`. |
| FS-INT-BMS-01 | URS-INT-BMS-01 | BMS exposes utility status (clean-steam pressure, WFI/PW availability, HVAC dP) via OPC UA; loss raises `UTILITY_LOSS_<resource>` and safes the unit op. |
| FS-INT-AD-01 | URS-INT-AD-01 | LDAPS / Kerberos to `crocus.local`; AD groups `BioSCADA-Operator`, `BioSCADA-SeniorOperator`, `BioSCADA-RecipeAuthor`, `BioSCADA-RecipeApprover`, `BioSCADA-Chemometrician`, `BioSCADA-OrchAuthor`, `BioSCADA-CSV-Reviewer`, `BioSCADA-Auditor`. |

### 4.14 Performance / Availability / Backup / Security / Training / Periodic Review (URS § 5.14)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | Control-loop latency measured via Prometheus `control_loop_latency_seconds` histogram; P95 ≤ 0.5 s SLO. |
| FS-PERF-02 | URS-PERF-02 | OQ stress run logs ≥ 1 Hz across CQA/CPP/PAT for 60 days; verified via dashboard `CRC-GR-LOG-RATE`. |
| FS-PERF-03 | URS-PERF-03 | HMI faceplate + alarm-ack P95 SLOs tracked in synthetic monitoring. |
| FS-AV-01 | URS-AV-01 | Availability ≥ 99.5% tracked monthly; maintenance windows logged. |
| FS-BAK-01 | URS-BAK-01 | Nightly Postgres dump + InfluxDB backup → S3 with cross-region replication; cryptographic integrity verification on restore. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore-test scripted in `restore_test.sh`; QA witness sign-off. |
| FS-BAK-03 | URS-BAK-03 | Geo-paired DR site RTO ≤ 4 h; replication lag ≤ 1 min monitored. |
| FS-SEC-01 | URS-SEC-01 | All auth via AD; service accounts in HashiCorp Vault; break-glass admin sealed in vault with split knowledge. |
| FS-SEC-02 | URS-SEC-02 | TLS 1.2+ minimum; mTLS HMI ↔ Gateway and Gateway ↔ PLC where supported. |
| FS-SEC-03 | URS-SEC-03 | Tenable Nessus monthly scans; 30-day SLA on critical findings. |
| FS-SEC-04 | URS-SEC-04 | Removable media blocked by Windows GPO; vendor-approved engineering use via signed CR. |
| FS-TRN-01 | URS-TRN-01 | Cornerstone LMS curriculum `CRC-CURR-BIOSCADA-<role>-v1`; production access gated by LMS completion. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher `BIOSCADA-2026-ANNUAL`: ICH Q13 + EU GMP Annex 2/1 + ATMP updates. |
| FS-PR-01 | URS-PR-01 | Periodic-review template `CRC-PR-BIOSCADA-YYYYMMDD` covers configuration drift, code-release register, audit-trail review, alarm trends, control-strategy verification, PAT-model performance trends, ATMP coverage; signed by Bioprocess Automation Lead + Head of Biologics Mfg + Head of QA. |
| FS-PR-02 | URS-PR-02 | Variation-tracking gate prevents EFFECTIVE promotion for rules with `variation_pending = true`. |


### 4.15 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem with local OT cached credentials for offline operation. Conditional-access binding to policy `OT-SCADA Conditional Access (MFA at HMI session start; named-location restriction to plant network)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the SCADA historian DB; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Interface Specifications

### 5.1 IF-PASX-RECIPE-IN
- HTTPS GET `/api/v1/recipes/{id}/effective`; mTLS cert `crocus-bioscada-2026q2`; payload recipe JSON + SHA-256.

### 5.2 IF-PASX-BATCH-OUT
- HTTPS POST `/api/v1/batches`; idempotency `batchId`; payload profile + alarms + signatures + PAT-trace.

### 5.3 IF-EQMS-DEV-OUT
- HTTPS POST `/api/v2/deviations`; idempotency `alarmId`; retry 1 / 5 / 30 s; escalates to on-call on failure.

### 5.4 IF-PAT-IN
- OPC UA / TLS mTLS; tag map per `tag_catalogue.yaml`; tag-quality consumed.

### 5.5 IF-HIST-OUT
- OPC HDA / OPC UA → Aspen IP.21; store-and-forward buffer at gateway.

### 5.6 IF-LIMS-IN
- HTTPS `/materials/{lot}/status` + `/donors/{id}` (ATMP); mTLS.

### 5.7 IF-BMS-IN
- OPC UA mTLS; utility-status tags.

### 5.8 IF-AD-AUTH
- LDAPS / Kerberos to `crocus.local`; AD groups per FS-INT-AD-01.

## 6. Data Model (high-level)

| Entity | Description |
|---|---|
| MasterRecipe | Campaign-template recipe |
| SiteRecipe | Site-fitted recipe |
| ControlRecipe | Per-batch instantiation |
| PhaseRule | ISA-88 phase entry/exit conditions |
| PatModel | Versioned chemometric model + state |
| Batch | Single fermentation campaign instance |
| PhaseEvent | Phase-transition log entry |
| AlarmEvent | Each alarm raise / clear / acknowledge |
| OverrideEvent | Setpoint / feed / phase override during a batch |
| DecisionEvent | Control-action decision with input-snapshot pointer |
| AuditEvent | Append-only audit-trail entry |
| DeploymentRecord | Orchestrator release with cosign signature ID |
| SingleUseLot | Bag/component lot + expiry + scan |
| AtmpDonorRecord | De-identified donor reference (ATMP mode) |
| Usp1043Material | Ancillary-material qualification reference |

## 7. Non-Functional Specifications

| Aspect | Target | URS reference |
|---|---|---|
| Cluster failover | ≤ 60 s | URS-PLAT-01 |
| Control-loop latency P95 | ≤ 500 ms | URS-PERF-01 |
| HMI faceplate P95 | ≤ 500 ms | URS-HMI-03 / URS-PERF-03 |
| Logging rate | ≥ 1 Hz CPP | URS-PERF-02 / URS-RUN-03 |
| Continuous run | ≥ 60 d | URS-PERF-02 |
| Availability | 99.5% | URS-AV-01 |
| Audit retention | ≥ 25 y | URS-AUD-04 |
| RTO / RPO | 4 h / 1 min | URS-BAK-03 |
| Determinism | 1000× bitwise | URS-DEV-07 |

## 8. Configuration Items (CI)

| CI ID | Item | Value |
|---|---|---|
| CI-01 | Active + DR gateways | required |
| CI-02 | OPC UA cert rotation | annual |
| CI-03 | CPP envelopes | recipe-defined |
| CI-04 | APC override workflow | dual signature |
| CI-05 | Tag logging rate | ≥ 1 Hz |
| CI-06 | Cosign public key | `crocus-sigstore-pubkey-2026q2` |
| CI-07 | PAS-X recipe endpoint | `https://pasx.crocus.local/api/v1` |
| CI-08 | eQMS deviation endpoint | `https://eqms.crocus.local/api/v2` |
| CI-09 | PTP master | `ptp.crocus.local` |
| CI-10 | Bioreactor config matrix | Sartorius STR / Cytiva XDR / Thermo HyPerforma / ABEC / Pall |
| CI-11 | ATMP isolation guard | enabled when `campaign.mode=ATMP` |
| CI-12 | Determinism OQ harness | 1000× canonical input |

## 9. Constraints / Assumptions / Risks

- **Constraints:** Ignition + DeltaV patches under change control; Orchestrator changes follow Cat-5 SDLC; PAT-model changes follow chemometric-model lifecycle; ICH Q12 variation gate before EFFECTIVE promotion.
- **Assumptions:** PAS-X, MasterControl, Watson LIMS, Aspen IP.21, BMS, AD, Vault, DeltaV SIS validated.
- **Risks:**

| Risk | Mitigation |
|---|---|
| Floating-point non-determinism across pod restarts | FS-DEV-07 + IEEE-754 round-mode pin + `decimal` for currency-class math |
| PAT-model-version-pin bypass | FS-PAT-03 contract test in CI rejecting mismatched-version predictions |
| Cosign public-key rotation breaks runtime module load | Paired-key transition window + monitoring |
| Aspen IP.21 ingest backpressure during 60-day run | Store-and-forward buffer + circuit breaker |
| Single-use bag barcode scanner failure | Manual entry with QA witness as fallback (signed) |
| ATMP donor metadata leak | De-identification at boundary + S3 KMS encryption |

## 10. References

- `CRC-URS-BIOSCADA-001 v1.2` (parent URS).
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11; Annex 1; Annex 2; ICH Q9(R1); ICH Q11; ICH Q12; ICH Q13.
- FDA CSA (Feb 2026); FDA PAT (2004); FDA Q13 (2024).
- USP <1043>; ATMP Guidelines.
- ISPE GAMP 5 (2nd ed., 2022); ISPE Baseline Guide *Biopharmaceutical Manufacturing Facilities*; ISPE GAMP GPG *PAT*.
- ISA-88; ISA-95; ISA-101; ISA-18.2; IEC 61511; ASTM E2476.
- PIC/S PI 041.
- Inductive Automation — *Ignition 8.3 Reference*; Emerson — *DeltaV v15.3 + SIS Reference*; Sartorius — *Biostat STR Manual*; Cytiva — *XDR Reference*; Thermo — *HyPerforma DynaDrive Reference*; Kaiser — *RamanRxn4 Manual*; Hamilton — *Incyte Reference*; Repligen — *XCell ATF Manual*.
- Site documents: `CRC-SOP-IT-CAT5-001`, `CRC-OQ-*`, `CRC-PR-BIOSCADA-YYYYMMDD`.

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-PLAT-01 | FS-PLAT-01 |
| URS-PLAT-02 | FS-PLAT-02 |
| URS-PLAT-03 | FS-PLAT-03 |
| URS-PLAT-04 | FS-PLAT-04 |
| URS-PLAT-05 | FS-PLAT-05 |
| URS-REC-01 | FS-REC-01 |
| URS-REC-02 | FS-REC-02 |
| URS-REC-03 | FS-REC-03 |
| URS-REC-04 | FS-REC-04 |
| URS-REC-05 | FS-REC-05 |
| URS-REC-06 | FS-REC-06 |
| URS-REC-07 | FS-REC-07 |
| URS-REC-08 | FS-REC-08 |
| URS-REC-09 | FS-REC-09 |
| URS-PHASE-01 | FS-PHASE-01 |
| URS-PHASE-02 | FS-PHASE-02 |
| URS-PHASE-03 | FS-PHASE-03 |
| URS-PHASE-04 | FS-PHASE-04 |
| URS-PHASE-05 | FS-PHASE-05 |
| URS-PHASE-06 | FS-PHASE-06 |
| URS-FEED-01 | FS-FEED-01 |
| URS-FEED-02 | FS-FEED-02 |
| URS-FEED-03 | FS-FEED-03 |
| URS-FEED-04 | FS-FEED-04 |
| URS-FEED-05 | FS-FEED-05 |
| URS-FEED-06 | FS-FEED-06 |
| URS-PAT-01 | FS-PAT-01 |
| URS-PAT-02 | FS-PAT-02 |
| URS-PAT-03 | FS-PAT-03 |
| URS-PAT-04 | FS-PAT-04 |
| URS-PAT-05 | FS-PAT-05 |
| URS-PAT-06 | FS-PAT-06 |
| URS-PAT-07 | FS-PAT-07 |
| URS-RUN-01 | FS-RUN-01 |
| URS-RUN-02 | FS-RUN-02 |
| URS-RUN-03 | FS-RUN-03 |
| URS-RUN-04 | FS-RUN-04 |
| URS-RUN-05 | FS-RUN-05 |
| URS-RUN-06 | FS-RUN-06 |
| URS-RUN-07 | FS-RUN-07 |
| URS-RUN-08 | FS-RUN-08 |
| URS-ALM-01 | FS-ALM-01 |
| URS-ALM-02 | FS-ALM-02 |
| URS-ALM-03 | FS-ALM-03 |
| URS-ALM-04 | FS-ALM-04 |
| URS-ALM-05 | FS-ALM-05 |
| URS-HMI-01 | FS-HMI-01 |
| URS-HMI-02 | FS-HMI-02 |
| URS-HMI-03 | FS-HMI-03 |
| URS-HMI-04 | FS-HMI-04 |
| URS-DEV-01 | FS-DEV-01 |
| URS-DEV-02 | FS-DEV-02 |
| URS-DEV-03 | FS-DEV-03 |
| URS-DEV-04 | FS-DEV-04 |
| URS-DEV-05 | FS-DEV-05 |
| URS-DEV-06 | FS-DEV-06 |
| URS-DEV-07 | FS-DEV-07 |
| URS-DEV-08 | FS-DEV-08 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
| URS-AUD-05 | FS-AUD-05 |
| URS-PART11-01 | FS-PART11-01 |
| URS-PART11-02 | FS-PART11-02 |
| URS-PART11-03 | FS-PART11-03 |
| URS-PART11-04 | FS-PART11-04 |
| URS-PART11-05 | FS-PART11-05 |
| URS-PART11-06 | FS-PART11-06 |
| URS-PART11-07 | FS-PART11-07 |
| URS-PART11-08 | FS-PART11-08 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-CFG-01 | FS-CFG-01 |
| URS-CFG-02 | FS-CFG-02 |
| URS-CFG-03 | FS-CFG-03 |
| URS-CFG-04 | FS-CFG-04 |
| URS-ATMP-01 | FS-ATMP-01 |
| URS-ATMP-02 | FS-ATMP-02 |
| URS-ATMP-03 | FS-ATMP-03 |
| URS-ATMP-04 | FS-ATMP-04 |
| URS-INT-MES-01 | FS-INT-MES-01 |
| URS-INT-MES-02 | FS-INT-MES-02 |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 |
| URS-INT-PAT-01 | FS-INT-PAT-01 |
| URS-INT-HIST-01 | FS-INT-HIST-01 |
| URS-INT-LIMS-01 | FS-INT-LIMS-01 |
| URS-INT-BMS-01 | FS-INT-BMS-01 |
| URS-INT-AD-01 | FS-INT-AD-01 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-PERF-03 | FS-PERF-03 |
| URS-AV-01 | FS-AV-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-BAK-03 | FS-BAK-03 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-PR-02 | FS-PR-02 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Defect in control-strategy code causing biased VCD / titer | Medium | High | URS-DEV-01..08 + URS-RUN-04 + URS-DEV-07 |
| R-02 | PAT loss not triggering safe state | Low | Critical | URS-PAT-04 + URS-RUN-06 + URS-INT-PAT-01 |
| R-03 | Manual override without justification | Medium | Medium | URS-RUN-05 + URS-FEED-03 |
| R-04 | Audit-trail tampering by privileged user | Low | High | URS-AUD-02 |
| R-05 | Recipe-version drift between PAS-X and runtime | Low | High | URS-REC-07 + URS-INT-MES-01 |
| R-06 | PAT-model drift consumed without re-validation | Medium | High | URS-PAT-05 + URS-PAT-07 |
| R-07 | Cell-retention device (ATF) fouling → control regression | Medium | Medium | URS-FEED-06 |
| R-08 | HMI alarm flood overwhelms operator | Medium | Medium | URS-ALM-03 + URS-ALM-05 |
| R-09 | Probe drift / fouling on capacitance / Raman | Medium | Medium | URS-PAT-05 + URS-PAT-06 |
| R-10 | Single-use component mismatch / expired bag | Low | High | URS-CFG-03 |
| R-11 | ATMP patient-batch crossover | Low | Critical | URS-ATMP-01 |
| R-12 | USP <1043> ancillary-material non-qualified | Low | High | URS-ATMP-03 + URS-INT-LIMS-01 |
| R-13 | SIS bypass / proof-test gap | Low | Critical | URS-ALM-04 + IEC 61511 proof-test plan |
| R-14 | Gateway / OpenShift cluster failover defect | Low | High | URS-PLAT-01 + URS-BAK-03 |

Full evaluation in `CRC-RA-BIOSCADA-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
