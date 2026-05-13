---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; expanded 2026-05-12 (FS catch-up to URS v1.2 — T3 enrichment)"
seed_corpus_basis:
  - "CAS-URS-WATER-SCADA-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd Edition) Category 5 conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11; Annex 1; Annex 3"
  - "USP <1231>, <645>, <643>, <85>, <86>"
  - "ASME BPE; ISA-88; ISA-95; ISA-101; ISA-18.2"
  - "PIC/S PI 041"
parent_urs:
  document_number: CAS-URS-WATER-SCADA-001
  version: "1.2"
  file: "../../URS/_generated/final/SCADA_Water_System__Cassia_Pharma_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## SCADA — Pharmaceutical Water System (Ignition 8.3 + custom Python scripts)

**Document Number:** CAS-FS-WATER-SCADA-001
**Version:** 1.2
**Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** CAS-URS-WATER-SCADA-001 v1.2
**Site:** Cassia Pharma SpA, Sterile Manufacturing Plant 2, Sesto Fiorentino, Italy *(fictional)*
**System Owner:** Utilities Automation Lead
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom Application
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11; Annex 1; Annex 3; USP <1231>, <645>, <643>, <85>, <86>; ISPE Baseline Guide *Water and Steam Systems*; ASME BPE; ISA-88; ISA-101; ISA-18.2; PIC/S PI 041.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead — Automation) | _____________ | _____________ | _____ |
| Reviewer (Utilities Automation Lead) | _____________ | _____________ | _____ |
| Reviewer (Microbiology / Water Quality) | _____________ | _____________ | _____ |
| Reviewer (Process Engineer — WFI/PW) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Security / Vault Owner) | _____________ | _____________ | _____ |
| Approver (Head of Manufacturing — Sterile) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Minor: alarm-rationalisation reference. |
| 1.2 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.2: every URS-ID expanded to its own FS row with per-ID implementation detail; loop topology + dead-leg + online TOC + conductivity + sanitisation + endotoxin + trending implementations added. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## Definitions

Defined in `CAS-URS-WATER-SCADA-001`. Additional FS-specific terms:

| Term | Definition |
|---|---|
| Tag Provider | Ignition runtime data-source providing tags from PLCs |
| UDT | User-Defined Type in Ignition (template for assets) |
| Project | Ignition logical container of resources (perspective views, scripts, named queries) |
| Custom Module | Site-authored Python control logic implemented as an Ignition module + scripted gateway events |
| Cosign | Sigstore signing tool used to sign release artefacts |
| LoopModel | Configured topology of WFI / PW distribution loops with branches, drops, dead-legs, points-of-use |

---

## 1. Purpose

This Functional Specification defines the implementation of the user, functional, regulatory, and non-functional requirements specified in the parent URS `CAS-URS-WATER-SCADA-001` v1.2. The FS describes how Ignition 8.3 plus the site-authored Python control logic together satisfy those requirements.

## 2. Scope

This FS covers the Ignition Gateway cluster, the historian, the Python custom module, integrations with MES (PAS-X), eQMS (MasterControl), on-line TOC analyzer (Sievers M9), conductivity (Mettler-Toledo M800), endotoxin (Endosafe), EMS (Pyxis), Watson LIMS, and AD authentication. Out of scope: physical plant (RO / EDI / distillation / storage / distribution piping); upstream / downstream packaging.

## 3. System Architecture

### 3.1 Component Inventory

| Component | Type | Vendor | Version |
|---|---|---|---|
| Ignition Gateway | Software | Inductive Automation | 8.3 (most recent stable) |
| Ignition Vision / Perspective | Software | Inductive Automation | 8.3 |
| Custom Python module | Software | In-house | v1.0 (~2,500 LOC) |
| PLC | Hardware | Allen-Bradley | ControlLogix 5580 |
| Historian | Software | Ignition Tag Historian + InfluxDB 2 | 8.3 / InfluxDB 2.7 LTS |
| TOC analyzer | Hardware | Sievers | M9 |
| Conductivity analyzer | Hardware | Mettler-Toledo | M800 |
| Endotoxin analyzer | Hardware | Charles River | Endosafe nexgen-PTS |
| Workstations / iPads | Hardware | Various | MDM-managed |

### 3.2 Logical Architecture (textual)

```
[Operator HMI / iPad MDM-managed] ──HTTPS──► [Ignition Gateway cluster]
                                                  │      │
                                                  │      └────► [Tag Historian + InfluxDB]
                                                  │
                                                  ├────► [Custom Python module — cassia_water_control]
                                                  │           │
                                                  ├────► [Ignition tag provider]
                                                  │           │
                                                  │           ▼
                                                  │      [AB ControlLogix PLCs]
                                                  │           │
                                                  │           ▼
                                                  │      [Water-system field instruments]
                                                  │
                                                  ├────► [Sievers M9 TOC via OPC UA mTLS]
                                                  ├────► [M-T M800 Conductivity via OPC UA mTLS]
                                                  ├────► [Endosafe nexgen-PTS via REST]
                                                  ├────► [PAS-X MES via REST mTLS]
                                                  ├────► [MasterControl eQMS via REST]
                                                  ├────► [Watson LIMS via REST]
                                                  ├────► [Pyxis EMS via REST]
                                                  └────► [AD via LDAPS / Kerberos]
```

### 3.3 Cluster Topology

- **Active Gateways:** 3 (gw1, gw2, gw3) on RHEL 9.2 in Plant-2 server room.
- **Standby Gateway:** 1 (gw4) cold-standby with auto-failover within 60 s.
- **Quorum:** Ignition Gateway Network with Cluster mode + redundant tag providers.
- **Database:** PostgreSQL 16 (3-node patroni cluster) for Ignition internal DB.
- **Historian:** InfluxDB 2.7 LTS, retention 5 years online + immutable cold-store ≥ 25 years.

---

## 4. Functional Specifications

### 4.1 Platform / Hardware (URS §5.1)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | Ignition Gateway cluster (3 active + 1 standby) on RHEL 9.2; auto-failover within 60 s tested via OQ procedure `CAS-OQ-FAILOVER-01`; cluster status surfaced on operator HMI. |
| FS-PLAT-02 | URS-PLAT-02 | Operator HMIs and Gateways on dedicated process-control VLAN 312; office-network firewall denies routing to/from VLAN 312. |
| FS-PLAT-03 | URS-PLAT-03 | UPS supplies allow ≥ 30-minute hold; AB ControlLogix outputs configured to safe-state defaults (CIP / SIP aborts to "draining and venting", interlocks to "all valves closed except vent"). |
| FS-PLAT-04 | URS-PLAT-04 | InfluxDB retention policy `online-5y` + `archive-25y` with cold-store on object-locked S3 storage. |
| FS-PLAT-05 | URS-PLAT-05 | Meinberg PTP grandmaster + NTP fallback; skew monitored via `ptp_skew_milliseconds` Prometheus exporter; > 1 s raises alarm. |

### 4.2 WFI Loop Topology + Dead-Legs (URS §5.2)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-LOOP-01 | URS-LOOP-01 | `LoopModel` table holds tag→location→branch/drop/dead-leg/point-of-use mapping traceable to ASME BPE as-built drawing IDs; model versioned in GitLab. |
| FS-LOOP-02 | URS-LOOP-02 | Hot-WFI loop temperature monitored at all configured probes; sustained < 80 °C ≥ T_window raises `HOT_WFI_TEMP_LOW` critical alarm + auto-deviation. |
| FS-LOOP-03 | URS-LOOP-03 | Cold-WFI loop continuous-sanitisation regime executed per recipe; deviation from regime sets `cold_loop_in_service = false` and blocks dependent operations. |
| FS-LOOP-04 | URS-LOOP-04 | Dead-leg flush sequences encoded per branch; executed by `DeadLegFlushScheduler`; recorded in `dead_leg_flush_events`; missed flush blocks dependent operations. |
| FS-LOOP-05 | URS-LOOP-05 | Flow / return-flow cross-check via paired flowmeters; mismatch > 5% sustained → `LOOP_FLOW_MISMATCH` maintenance alarm. |

### 4.3 Online TOC + Conductivity (URS §5.3)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MON-TOC-01 | URS-MON-TOC-01 | OPC UA mTLS to Sievers M9; tag-quality flagged at boundary; quality degraded triggers `TOC_QUALITY_DEGRADED`. |
| FS-MON-TOC-02 | URS-MON-TOC-02 | TOC alert / action limits per `water_quality_plan.yaml`; action-limit excursion → `TOC_ACTION_LIMIT` critical alarm + MasterControl deviation. |
| FS-MON-TOC-03 | URS-MON-TOC-03 | M800 conductivity via OPC UA mTLS; USP <645> Stage-1 temperature-compensated value consumed; Stage-2/-3 procedures referenced in cycle SOP. |
| FS-MON-COND-01 | URS-MON-COND-01 | Conductivity action-limit excursion → `COND_ACTION_LIMIT` critical alarm + auto-deviation. |
| FS-MON-COND-02 | URS-MON-COND-02 | Probe serial + calibration metadata persisted in `probe_inventory`; expired calibration sets status `OUT-OF-SERVICE`. |

### 4.4 Sanitisation Cycles (URS §5.4)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SAN-01 | URS-SAN-01 | `SanitisationScheduler` executes hot-water / ozone / chemical cycles per EFFECTIVE recipe; cycle profile recorded in `sanitisation_events`. |
| FS-SAN-02 | URS-SAN-02 | Sanitisation schedule table queried at the start of any dependent operation; missed sanitisation returns `BLOCKED` and the operation cannot start until verified completion is recorded. |
| FS-SAN-03 | URS-SAN-03 | Ozone-residual probes interlocked with loop-release valve; loop cannot re-open until residual ≤ release threshold for sustained T_window. |
| FS-SAN-04 | URS-SAN-04 | Sanitisation effectiveness trended via Grafana dashboard `CAS-GR-SAN-EFFECTIVENESS`. |
| FS-SAN-05 | URS-SAN-05 | Sanitisation-cycle CR template requires Microbiology Reviewer signature row. |

### 4.5 Recipes (URS §5.5)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REC-01 | URS-REC-01 | Recipe lifecycle: Postgres table `recipe_versions` with status enum `DRAFT / REVIEW / APPROVED / EFFECTIVE / OBSOLETE`; transitions enforced by stored procedures + signature checks. |
| FS-REC-02 | URS-REC-02 | Only `EFFECTIVE` recipes returned by runtime API endpoint `GET /api/recipes/effective`. |
| FS-REC-03 | URS-REC-03 | Transition endpoint `POST /api/recipes/transition` requires e-signature payload; verified server-side. |
| FS-REC-04 | URS-REC-04 | `EFFECTIVE` recipes immutable: ON-UPDATE/DELETE database triggers raise exception; SCADA UI hides edit controls. |
| FS-REC-05 | URS-REC-05 | Recipe download from MES validates SHA-256 + version; mismatch returns `409` and cycle is blocked. |
| FS-REC-06 | URS-REC-06 | Recipe schema includes `loop_coverage[]`, `exposure_time_s`, `target_temperature_c`, `chemistry`, `acceptance_criteria[]`. |

### 4.6 Cycle Execution (URS §5.6)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CYC-01 | URS-CYC-01 | `RecipeRunner` evaluates setpoint deviations every 250 ms; alarms classified per the configured alarm-severity table (ISA-18.2). |
| FS-CYC-02 | URS-CYC-02 | Critical alarms persist with `selfAcknowledgement = false`; operator acknowledges with reason ≥ 10 chars; reason persisted in alarm-event audit table. |
| FS-CYC-03 | URS-CYC-03 | Conductivity, TOC, temperature, pressure, flow tags configured with InfluxDB write rate 1 Hz; PLC scan rate 100 ms with first-order on-change deadband. |
| FS-CYC-04 | URS-CYC-04 | Override workflow requires Operator + Senior Operator signatures; recorded in cycle profile and tagged in executed report. |
| FS-CYC-05 | URS-CYC-05 | Sanitisation-schedule check at any dependent-operation start; missed → `BLOCKED` (per FS-SAN-02). |

### 4.7 Endotoxin Monitoring (URS §5.7)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ENDO-01 | URS-ENDO-01 | Endosafe nexgen-PTS results consumed via secure REST `POST /api/v1/endotoxin`; payload signature verified; above-alert → `ENDOTOXIN_ALERT` critical alarm + auto-deviation. |
| FS-ENDO-02 | URS-ENDO-02 | Watson LIMS off-line endotoxin / micro results linked to point-of-use + cycle + time-window via `endotoxin_linkage` table; surfaced in trend dashboard. |
| FS-ENDO-03 | URS-ENDO-03 | Limits configured per loop + point-of-use in `water_quality_plan.yaml`; CR template requires Microbiology Reviewer signature. |

### 4.8 System Trending, OOL / OOS, Anomaly Detection (URS §5.8)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TREND-01 | URS-TREND-01 | Rolling-window trends (15-min / 1-hr / 24-hr) computed by `TrendEngine`; surfaced in Perspective dashboards `cas-water-trends`. |
| FS-TREND-02 | URS-TREND-02 | OOL / OOS detection per ASTM E2476 SPC rules (3σ, Western Electric); thresholds recipe-pinned via `spc_limits` table. |
| FS-TREND-03 | URS-TREND-03 | `AnomalyDetector` (isolation-forest + heuristic patterns for slow TOC creep, intermittent low-flow, post-sanitisation rebound); maintenance / warning alarms surfaced. |
| FS-TREND-04 | URS-TREND-04 | Export endpoints produce PDF/A-3 + CSV + JSON for periodic review. |

### 4.9 Custom Code (URS §5.9)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DEV-01 | URS-DEV-01 | The Cat-5 SDLC for `cassia_water_control` is documented in `CAS-SOP-IT-CAT5-001`; CI workflows enforce gates. |
| FS-DEV-02 | URS-DEV-02 | Source repo `git.cassia.local/utilities/cassia-water-control`; branch protection requires 1 reviewer + passing CI; Sigstore commit signing enforced. |
| FS-DEV-03 | URS-DEV-03 | Test coverage measured by Jacoco (Java) + coverage.py (Jython); fails CI below 90% on `safety/*` packages. |
| FS-DEV-04 | URS-DEV-04 | CI runs Ruff, mypy --strict, Bandit on Python; SpotBugs + PMD on Java; Trivy on container image. Critical findings break the build. |
| FS-DEV-05 | URS-DEV-05 | Releases packaged as Ignition `.modl` files signed via cosign; Gateway start-up checks signature against the site Sigstore public key. |
| FS-DEV-06 | URS-DEV-06 | Each release manifest `manifest.yaml` lists release notes, FS / DS / CS deltas, regression-test summary, security-scan report path, change-control record ID. |
| FS-DEV-07 | URS-DEV-07 | Determinism harness in OQ: canonical input replay produces bitwise-identical sequencing outputs. |

### 4.10 Audit Trail / Part 11 / DI (URS §5.10)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit events written to PostgreSQL `audit_events` with full ALCOA+ fields. |
| FS-AUD-02 | URS-AUD-02 | DB role has only INSERT/SELECT on `audit_events`; UPDATE/DELETE denied. |
| FS-AUD-03 | URS-AUD-03 | `Audit Trail Review` Perspective view filterable by date / actor / action; export to PDF/A-3 + JSONL. |
| FS-AUD-04 | URS-AUD-04 | Retention 25 y in `audit_events_archive` (S3 with object-lock). |
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural controls in `/sop/`; reviewed annually. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(d): AD Kerberos auth + MFA. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(e): operational audit per FS-AUD-01. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.50: e-signature endpoint enforces `printedName + dateTime + meaning`; meaning enum validated. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.70: signature payload includes SHA-256(record); tamper invalidates signature. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.100: AD signer mapping fixed via HR feed; reuse blocked at provisioning. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.200: sign-off endpoint requires fresh Kerberos ticket (max-age 5 min); cached tokens rejected. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.300: AD password policy ≥ 14 chars + complexity + 90 d rotation + MFA. |
| FS-AN1-01 | URS-AN1-01 | Override workflow auto-links to the site CCS (Contamination Control Strategy) doc; CCS doc-ref stored on the override event. |
| FS-DI-01 | URS-DI-01 | DB NOT-NULL on `actor_id` at audit-write. |
| FS-DI-02 | URS-DI-02 | Exports PDF/A-3 + JSON / CSV; validated at OQ. |
| FS-DI-03 | URS-DI-03 | PTP timestamps from PLC up; retroactive flagged with reason. |
| FS-DI-04 | URS-DI-04 | InfluxDB point-write only; corrections recorded as new annotated tags referencing original. |
| FS-DI-05 | URS-DI-05 | F0-style + USP <645> Stage 1 conductivity compensation + rolling-window math regression-tested at OQ. |
| FS-DI-06 | URS-DI-06 | Metadata completeness validated; retrievable within 4 h via inspection-mode query API. |

### 4.11 Integrations (URS §5.11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-MES-01 | URS-INT-MES-01 | `RecipeFetcher` connects to `https://pasx.cassia.local/api/v1/recipes/{id}/effective`; mTLS via cert `cassia-water-scada-2026q2`; checksum + version validated. |
| FS-INT-MES-02 | URS-INT-MES-02 | `BatchReporter` posts cycle profile + alarms + signatures to `https://pasx.cassia.local/api/v1/cycles`; idempotency key `cycleId`. |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | `DeviationCreator` posts unacknowledged-alarm events to `https://eqms.cassia.local/api/v2/deviations`; idempotency key. |
| FS-INT-TOC-01 | URS-INT-TOC-01 | OPC UA client to Sievers M9 with mutual auth; tag-quality monitoring; gaps on hot loop drive `TOC_LOSS_HOT_LOOP` alarm. |
| FS-INT-COND-01 | URS-INT-COND-01 | OPC UA mTLS to M800; gaps drive `COND_LOSS` alarm. |
| FS-INT-ENDO-01 | URS-INT-ENDO-01 | Endosafe REST adapter with payload-signature verification. |
| FS-INT-EMS-01 | URS-INT-EMS-01 | EMS REST adapter pulls dP / T / RH for the affected cleanroom on cycle start; cross-reference recorded in cycle report. |
| FS-INT-AD-01 | URS-INT-AD-01 | LDAPS / Kerberos to `cassia.local`; AD groups `Util-Water-Operator`, `Util-Water-SeniorOperator`, `Util-Water-RecipeAuthor`, `Util-Water-RecipeApprover`, `Util-Water-AutomationEngineer`, `Util-Water-CSV-Reviewer`, `Util-Water-Auditor`, `Util-Water-Microbiology`. |

### 4.12 Backup / DR / Performance / Security (URS §5.12)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BAK-01 | URS-BAK-01 | InfluxDB nightly backup via `influxd backup` to S3; retention 25 y; integrity-verified. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore test scripted; QA witness sign-off. |
| FS-BAK-03 | URS-BAK-03 | Hot-spare gateway provides RTO ≤ 4 h; replication lag ≤ 1 min monitored. |
| FS-PERF-01 | URS-PERF-01 | OQ stress run logs ≥ 1 Hz across critical channels for 30 days; verified via Grafana `cas-water-scada-perf`. |
| FS-PERF-02 | URS-PERF-02 | HMI faceplate + alarm-ack SLOs measured via synthetic monitoring. |
| FS-SEC-01 | URS-SEC-01 | All auth via AD; service accounts in HashiCorp Vault. |
| FS-SEC-02 | URS-SEC-02 | TLS 1.2+ on all HMI ↔ Gateway; mTLS Gateway ↔ PLC where AB Gateway supports. |
| FS-SEC-03 | URS-SEC-03 | Tenable Nessus monthly scans; 30-day SLA on critical findings. |
| FS-SEC-04 | URS-SEC-04 | Removable media blocked by GPO; vendor-approved exceptions under CR. |

### 4.13 Training / Periodic Review (URS §5.13)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Cornerstone curriculum `CAS-CURR-WATER-SCADA-<role>-v1`. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher `WATER-2026-ANNUAL`. |
| FS-PR-01 | URS-PR-01 | Periodic-review template `CAS-PR-WATER-SCADA-YYYYMMDD`. |

---


### 4.14 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem with local OT cached credentials for offline operation. Conditional-access binding to policy `OT-SCADA Conditional Access (MFA at engineering workstation; operator stations named-location + role-bound smart cards)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the SCADA historian DB plus file-level capture of PLC programs; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Interface Specifications

### 5.1 IF-MES-RECIPE-IN
- HTTPS GET `/api/v1/recipes/{id}/effective`; mTLS with cert `cassia-water-scada-2026q2`; payload recipe JSON + SHA-256.

### 5.2 IF-MES-CYCLE-OUT
- HTTPS POST `/api/v1/cycles`; idempotency key `cycleId`.

### 5.3 IF-EQMS-DEV-OUT
- HTTPS POST `/api/v2/deviations`; idempotency `alarmId`; retry 1 / 5 / 30 s.

### 5.4 IF-TOC-IN
- OPC UA over TLS, mutual auth; tag map `cas:water:toc:loop1` etc.

### 5.5 IF-COND-IN
- OPC UA mTLS to M800; tag map `cas:water:cond:loop1` etc.

### 5.6 IF-ENDO-IN
- REST POST endotoxin results; signature verified.

### 5.7 IF-EMS-IN
- REST pull cleanroom dP / T / RH.

### 5.8 IF-LIMS-IN
- REST pull off-line endotoxin / microbial results.

### 5.9 IF-AD-AUTH
- LDAPS / Kerberos to `cassia.local`; AD groups per FS-INT-AD-01.

---

## 6. Data Model (high-level)

| Entity | Description |
|---|---|
| Recipe | Versioned cycle definition (CIP / SIP / sanitisation) |
| RecipeVersion | Lifecycle state + signatures + hash |
| Cycle | Single execution of a recipe (immutable once started) |
| LoopModel | Topology configuration |
| AlarmEvent | Each alarm raise / clear / acknowledge |
| OverrideEvent | Setpoint override during a cycle |
| SanitisationEvent | Each sanitisation execution |
| DeadLegFlushEvent | Each dead-leg flush |
| EndotoxinResult | In-line + off-line endotoxin reading |
| AuditEvent | Append-only audit-trail entry |
| DeploymentRecord | Custom-module release with cosign signature ID |
| ProbeInventory | Probe + calibration metadata |
| WaterQualityPlan | Configured alert / action limits per loop / point-of-use |

---

## 7. Non-Functional Specifications

| Aspect | Target | URS reference |
|---|---|---|
| Cluster failover | ≤ 60 s | URS-PLAT-01 |
| Logging rate | ≥ 1 Hz on critical channels | URS-PERF-01 |
| HMI faceplate P95 | ≤ 500 ms | URS-PERF-02 |
| Availability | 99.5% during operations | URS-PERF-01 (implied) |
| Audit-trail retention | ≥ 25 y | URS-AUD-04 |
| RTO / RPO | 4 h / 1 min | URS-BAK-03 |
| Determinism | bitwise on canonical input | URS-DEV-07 |

---

## 8. Configuration Items

| CI ID | Item | Value |
|---|---|---|
| CI-01 | Gateway URL (active cluster) | `https://water-scada.cassia.local` |
| CI-02 | InfluxDB retention online | 5 y |
| CI-03 | Cosign public key | `cassia-sigstore-pubkey-2026q2` |
| CI-04 | MES recipe endpoint | `https://pasx.cassia.local/api/v1` |
| CI-05 | eQMS deviation endpoint | `https://eqms.cassia.local/api/v2` |
| CI-06 | NTP / PTP master | `ntp.cassia.local` / `ptp.cassia.local` |
| CI-07 | Sigstore project | `git.cassia.local/utilities/cassia-water-control` |
| CI-08 | Water-quality plan | `water_quality_plan.yaml` (recipe-pinned) |
| CI-09 | Loop model | `loop_model.yaml` (ASME BPE-traced) |

---

## 9. Constraints / Assumptions / Risks

Inherited from `CAS-URS-WATER-SCADA-001`. FS-specific risks added:

| Risk | Mitigation |
|---|---|
| Cosign public-key rotation breaks runtime module load | Documented rotation procedure with paired-key transition window |
| InfluxDB upgrade silently changes retention semantics | Quarterly retention audit |
| Jython 2.7 EOL impacts long-term support | Roadmap to migrate Python control logic to Ignition 9.x JS / Java when available |
| TOC analyzer firmware divergence | Vendor patch under CR; signal-quality monitored |
| LoopModel divergence from ASME BPE drawings after physical retrofit | Annual reconciliation review under PR-01 |

## 10. References

- `CAS-URS-WATER-SCADA-001 v1.2` (parent URS).
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11; Annex 1; Annex 3.
- USP <1231>, <645>, <643>, <85>, <86>.
- EMA Water Note (2020); Ph.Eur. 0008 / 0169.
- ISPE GAMP 5 (2nd ed., 2022); ISPE Baseline *Water and Steam Systems*.
- ASME BPE; ISA-88; ISA-101; ISA-18.2; ASTM E2476.
- PIC/S PI 041; PIC/S PI 009.
- Inductive Automation — *Ignition 8.3 Reference*; Sievers — *M9 TOC Reference*; M-T — *M800 Reference*; AB — *ControlLogix 5580 Reference*; Charles River — *Endosafe nexgen-PTS Reference*.
- Site documents: `CAS-SOP-IT-CAT5-001`, `CAS-OQ-FAILOVER-01`, `CAS-PR-WATER-SCADA-YYYYMMDD`.

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-PLAT-01 | FS-PLAT-01 |
| URS-PLAT-02 | FS-PLAT-02 |
| URS-PLAT-03 | FS-PLAT-03 |
| URS-PLAT-04 | FS-PLAT-04 |
| URS-PLAT-05 | FS-PLAT-05 |
| URS-LOOP-01 | FS-LOOP-01 |
| URS-LOOP-02 | FS-LOOP-02 |
| URS-LOOP-03 | FS-LOOP-03 |
| URS-LOOP-04 | FS-LOOP-04 |
| URS-LOOP-05 | FS-LOOP-05 |
| URS-MON-TOC-01 | FS-MON-TOC-01 |
| URS-MON-TOC-02 | FS-MON-TOC-02 |
| URS-MON-TOC-03 | FS-MON-TOC-03 |
| URS-MON-COND-01 | FS-MON-COND-01 |
| URS-MON-COND-02 | FS-MON-COND-02 |
| URS-SAN-01 | FS-SAN-01 |
| URS-SAN-02 | FS-SAN-02 |
| URS-SAN-03 | FS-SAN-03 |
| URS-SAN-04 | FS-SAN-04 |
| URS-SAN-05 | FS-SAN-05 |
| URS-REC-01 | FS-REC-01 |
| URS-REC-02 | FS-REC-02 |
| URS-REC-03 | FS-REC-03 |
| URS-REC-04 | FS-REC-04 |
| URS-REC-05 | FS-REC-05 |
| URS-REC-06 | FS-REC-06 |
| URS-CYC-01 | FS-CYC-01 |
| URS-CYC-02 | FS-CYC-02 |
| URS-CYC-03 | FS-CYC-03 |
| URS-CYC-04 | FS-CYC-04 |
| URS-CYC-05 | FS-CYC-05 |
| URS-ENDO-01 | FS-ENDO-01 |
| URS-ENDO-02 | FS-ENDO-02 |
| URS-ENDO-03 | FS-ENDO-03 |
| URS-TREND-01 | FS-TREND-01 |
| URS-TREND-02 | FS-TREND-02 |
| URS-TREND-03 | FS-TREND-03 |
| URS-TREND-04 | FS-TREND-04 |
| URS-DEV-01 | FS-DEV-01 |
| URS-DEV-02 | FS-DEV-02 |
| URS-DEV-03 | FS-DEV-03 |
| URS-DEV-04 | FS-DEV-04 |
| URS-DEV-05 | FS-DEV-05 |
| URS-DEV-06 | FS-DEV-06 |
| URS-DEV-07 | FS-DEV-07 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
| URS-PART11-01 | FS-PART11-01 |
| URS-PART11-02 | FS-PART11-02 |
| URS-PART11-03 | FS-PART11-03 |
| URS-PART11-04 | FS-PART11-04 |
| URS-PART11-05 | FS-PART11-05 |
| URS-PART11-06 | FS-PART11-06 |
| URS-PART11-07 | FS-PART11-07 |
| URS-PART11-08 | FS-PART11-08 |
| URS-AN1-01 | FS-AN1-01 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-INT-MES-01 | FS-INT-MES-01 |
| URS-INT-MES-02 | FS-INT-MES-02 |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 |
| URS-INT-TOC-01 | FS-INT-TOC-01 |
| URS-INT-COND-01 | FS-INT-COND-01 |
| URS-INT-ENDO-01 | FS-INT-ENDO-01 |
| URS-INT-EMS-01 | FS-INT-EMS-01 |
| URS-INT-AD-01 | FS-INT-AD-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-BAK-03 | FS-BAK-03 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Defect in custom Python sequencing causing missed sanitisation | Medium | High | URS-CYC-05 + URS-SAN-02 + URS-DEV-01..07 |
| R-02 | Silent override of contamination-control interlock | Low | High | URS-CYC-04 + URS-AN1-01 |
| R-03 | Audit-trail tampering | Low | High | URS-AUD-02 |
| R-04 | Historian data loss | Medium | High | URS-BAK-01 |
| R-05 | Gateway failover defect | Low | Medium | URS-PLAT-01 |
| R-06 | Dead-leg colonisation due to missed flush | Medium | High | URS-LOOP-04 |
| R-07 | TOC excursion not detected (analyzer fault) | Low | High | URS-MON-TOC-01..02 |
| R-08 | Cold-loop sanitisation regime lapse | Medium | High | URS-LOOP-03 + URS-SAN-03 |
| R-09 | Online conductivity probe drift / fouling | Medium | Medium | URS-MON-COND-02 |
| R-10 | Endotoxin alert / action-limit creep | Low | High | URS-ENDO-03 + Microbiology co-approval |
| R-11 | PLC firmware mismatch / un-validated update | Low | High | EQ-WATER-001 + URS-DEV-06 |
| R-12 | Alarm flood overwhelms operator | Medium | Medium | URS-CYC-01 + ISA-18.2 |

Full evaluation in `CAS-RA-WATER-SCADA-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
