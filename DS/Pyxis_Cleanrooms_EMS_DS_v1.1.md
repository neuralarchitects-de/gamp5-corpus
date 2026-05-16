---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (v1.0 corpus genesis per METHODOLOGY § 2B)"
seed_corpus_basis:
  - "PXC-FS-EMS-001 v1.2 (parent FS)"
  - "PXC-URS-EMS-001 v1.2 (parent URS — transitive)"
  - "GAMP 5 (2nd ed.) Cat 4"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11; EU GMP Annex 1 (2022 revised)"
  - "ISO 14644-1/-2/-3; ISO 14698; USP <1116>; PIC/S PI 041"
parent_fs:
  document_number: PXC-FS-EMS-001
  version: "1.2"
  file: "../../../FS_FDS/_generated/final/Pyxis_Cleanrooms_EMS_FS_v1.3.md"
parent_urs:
  document_number: PXC-URS-EMS-001
  version: "1.2"
  file: "../../../URS/_generated/final/Environmental_Monitoring_System__Pyxis_Cleanrooms_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Environmental Monitoring System — Vaisala viewLinc 5.2 + Lighthouse APM / ApexZ Continuous Particle Monitors

**Document Number:** PXC-DS-EMS-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** PXC-FS-EMS-001 v1.2
**Parent URS:** PXC-URS-EMS-001 v1.2 *(informational; URS-ID linkage transitive through the FS)*
**Site:** Pyxis Cleanrooms BV, Sterile Drug Substance Plant 1, Leiden, the Netherlands *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Vaisala viewLinc 5.2 + Lighthouse APM / ApexZ Continuous Particle Monitors** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Annex 1 (2022 revised); ISO 14644-1 / -2 / -3; ISO 14698; USP <1116>; PIC/S PI 041; FDA CSA (Feb 2026).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Facilities Engineering Lead) | _____________ | _____________ | _____ |
| Reviewer (Microbiology / EM Manager — SME) | _____________ | _____________ | _____ |
| Reviewer (OT-Security Architect) | _____________ | _____________ | _____ |
| Approver (System Owner — Facilities Engineering Lead) | _____________ | _____________ | _____ |
| Approver (Head of Sterile Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial issue. Inherited Tier T3 from parent URS+FS pair. DS covers 79/79 FS-IDs; 0 FS-IDs flagged as vendor-internal — no site design surface. Generated as part of the DS v1.0 corpus ship per METHODOLOGY § 2B (DS as Configuration Specification for Cat 4 — Configured Product). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

DS-specific terms only — URS / FS definitions inherited by reference.

| Term | Definition |
|---|---|
| CS | Configuration Specification (this document, per GAMP 5 2nd ed. for Cat 4) |
| CI | Configuration Item — one configurable parameter, value, default-vs-custom flag, justification |
| Location | viewLinc-modelled monitored space (cleanroom, warehouse) with grade + ISO class + limits |
| Gateway | Vaisala AP10 / VaiNet wireless gateway aggregating probe traffic |
| viewLinc Notification Channel | viewLinc-configured outbound channel (email, SMS, push) for alarm routing |
| CPM | Continuous Particle Monitor (Lighthouse APM at-grade-A/B locations) |
| Annex1Grade | EU GMP Annex 1 (2022) cleanroom grade enum (`A`, `B`, `C`, `D`, `CNC`) |

## 1. Purpose

This Configuration Specification (CS) is the technical-design layer between `PXC-FS-EMS-001` v1.2 and downstream configuration / IQ / OQ / PQ Protocols for the Vaisala viewLinc 5.2 + Lighthouse APM environmental monitoring deployment across Grade A/B/C/D cleanrooms at Pyxis Cleanrooms Plant 1. The DS declares, per configuration item, the chosen value, default-vs-custom flag, FS-ID(s) traced, and planned verification test. Vendor source-code internals (viewLinc historian engine, Lighthouse APM firmware) are not redrawn here — those remain under Vaisala and Lighthouse SDLC.

## 2. Scope

### In scope

- Vaisala viewLinc 5.2 Active + Warm-Standby server configuration on Windows Server 2022.
- VaiNet wireless gateway network configuration (with ≥ 1-hop redundancy per zone).
- ~180 Vaisala HMP / DPT / PTU probes registered per location with calibration metadata.
- ~25 Lighthouse APM continuous particle monitors (Grade A / B; HA pairing on Grade A).
- Lighthouse ApexZ portable particle counter inventory + at-rest classification scheduling.
- viewLinc Mobile (iOS) application configuration.
- Alarm-routing matrix (Information / Warning / Action Limit / Alert Limit) with two-channel redundancy on Grade A/B alarms.
- Viable-EM workflow (settle / contact / active-air) with LIMS integration.
- Trend engine (24-h / 7-d / 30-d), recurring-excursion detector, periodic-review report generation.
- Audit-trail bindings, 21 CFR Part 11 controls, ALCOA+ disciplines.
- Integration endpoints to MasterControl eQMS, BMS, Watson LIMS, PAS-X MES, Halcyon Stability, AD / NTP.

### Out of scope

- The HVAC system itself (separate URS).
- The cleanroom BMS internals (`BMS-CSV-2024-002`).
- Microbiology lab platform (separate URS).
- Physical viable EM sampling activities (manual workflow; results entered via the EMS).

## 3. Architectural Overview

### 3.1 Logical view

```
   ┌────────────────────────────────────────────────────────────────────┐
   │  AD / Kerberos (LDAPS)        NTP master (stratum-1)               │
   └─────────────┬─────────────────────────────┬─────────────────────────┘
                 │                             │
   ┌─────────────▼─────────────────────────────▼─────────────────────────┐
   │              Vaisala viewLinc 5.2 — Active + Warm-Standby             │
   │              (Win Server 2022; manual failover ≤ 1 h)                 │
   │   ┌────────────────┐  ┌─────────────────────────┐                    │
   │   │ Web client     │  │ viewLinc Mobile (iOS)    │                    │
   │   └────────────────┘  └─────────────────────────┘                    │
   │   ┌──────────────────────────────────────────────────────────┐       │
   │   │ VaiNet wireless gateway network — ≥ 1-hop redundancy per │       │
   │   │  zone; reduced-redundancy state surfaces GW_DEGRADED     │       │
   │   └──────────────────────────────────────────────────────────┘       │
   │   ┌──────────────────────────────────────────────────────────┐       │
   │   │ ~180 Vaisala HMP / DPT / PTU probes — wireless + wired   │       │
   │   └──────────────────────────────────────────────────────────┘       │
   │   ┌──────────────────────────────────────────────────────────┐       │
   │   │ Lighthouse APM CPM (Grade A/B; HA-pair on A)             │       │
   │   │ Lighthouse ApexZ portable (at-rest / qualification)      │       │
   │   └──────────────────────────────────────────────────────────┘       │
   │   ┌──────────────────────────────────────────────────────────┐       │
   │   │ Twilio SMS │ AWS SES email │ FCM push (two-channel       │       │
   │   │ redundancy on Grade A/B)                                 │       │
   │   └──────────────────────────────────────────────────────────┘       │
   └────────┬─────────────────────────────────────────┬─────────────────────┘
            │                                         │
            ▼                                         ▼
        BMS (cross-ref) │ MasterControl (deviation) │ LIMS (viable) │ PAS-X (batch) │ Halcyon (excursion)
```

### 3.2 Sensor / CPM layout per Grade (text diagram)

```
┌──── Grade A locations (filling line, isolators) ───────────────────────┐
│  ┌──────────┐ ┌──────────┐ ┌──────────┐                                │
│  │ HMP-A-01 │ │ DPT-A-01 │ │ HMP-A-02 │  ← T / RH / DP probes           │
│  └──────────┘ └──────────┘ └──────────┘                                │
│  ┌─────────────────────────────────────────────────────┐               │
│  │ CPM-A-01  ◄── HA pair ──►  CPM-A-02   (Lighthouse APM)│               │
│  │  ≥ 0.5 µm + ≥ 5 µm channels; Annex 1 § 9.16          │               │
│  └─────────────────────────────────────────────────────┘               │
│  Viable: settle plate locations SP-A-01..SP-A-08 (per shift)            │
│          contact plate CP-A-01..CP-A-12 (post-run)                      │
│          active-air AAS-A-01..AAS-A-04 (per shift)                      │
└────────────────────────────────────────────────────────────────────────┘

┌──── Grade B locations (background to Grade A) ─────────────────────────┐
│  HMP-B-01..HMP-B-08; DPT-B-01..DPT-B-04                                  │
│  CPM-B-01..CPM-B-06 (Lighthouse APM); single unit per location          │
│  Viable: per site EM plan                                                │
└────────────────────────────────────────────────────────────────────────┘

┌──── Grade C / D locations (support cleanrooms) ────────────────────────┐
│  HMP-C-01..HMP-C-12; HMP-D-01..HMP-D-20                                 │
│  No CPM required; viable per site EM plan                                │
└────────────────────────────────────────────────────────────────────────┘

┌──── Warehouses (CNC class) ─────────────────────────────────────────────┐
│  HMP-WH-01..HMP-WH-40; 5-min logging interval                            │
└────────────────────────────────────────────────────────────────────────┘
```

## 4. Configuration Specification

### 4.1 Platform / Hardware

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EMS-01 | viewLinc 5.2 Active server — host OS | Windows Server 2022 (21H2 LTSC) | Default (Vaisala-supported) | Matches Vaisala *viewLinc 5.2 Installation Reference* v1.0 § 2.1. | FS-PLAT-01 | OQ-PLAT-01 |
| DS-EMS-02 | viewLinc 5.2 Warm-Standby server — host OS | Windows Server 2022 (21H2 LTSC) — identical patch baseline | Custom | Identical baseline reduces failover-time risk; mirrors active-LDT pattern in autoclave DS. | FS-PLAT-01 | OQ-PLAT-01 |
| DS-EMS-03 | Failover mode | Manual failover; documented runbook `PXC-RB-EMS-FAILOVER-001`; target ≤ 1 h | Custom | FS-PLAT-01 mandate manual within 1 h; manual chosen so EM Reviewer confirms data-quality before resuming. | FS-PLAT-01 | OQ-FAILOVER-01 |
| DS-EMS-04 | DB replication mode | SQL Server 2022 always-on synchronous-commit availability group between active and standby | Custom | RPO ≤ 5 min per FS-BAK-03; synchronous required for that RPO. | FS-PLAT-01, FS-BAK-03 | OQ-FAILOVER-01 |
| DS-EMS-05 | UPS sizing for viewLinc servers | APC Smart-UPS SRT 5kVA per server; 30 min hold at 80% load | Custom | FS-PLAT-02 ride-through. | FS-PLAT-02 | OQ-UPS-HOLD-01 |
| DS-EMS-06 | UPS sizing for VaiNet gateways | Per-gateway APC Back-UPS Pro 1500; 30 min hold | Custom | FS-PLAT-02 ride-through extends to gateways. | FS-PLAT-02 | OQ-UPS-HOLD-01 |
| DS-EMS-07 | Facilities-IT VLAN ID | VLAN 230 | Custom | Site VLAN range 220-239 reserved for facilities; FS-PLAT-03 mandates segregation. | FS-PLAT-03 | OQ-NET-AUDIT-01 |
| DS-EMS-08 | Firewall policy — OT-DMZ to office network | Deny-by-default at FortiGate; no L3 route | Custom | FS-PLAT-03; matches site OT-security baseline. | FS-PLAT-03 | OQ-NET-AUDIT-01 |
| DS-EMS-09 | Gateway-network design | ≥ 1-hop redundancy per zone; VaiNet mesh topology; `GW_DEGRADED` alarm on single-gateway loss | Custom | FS-PLAT-04. | FS-PLAT-04 | OQ-GW-REDUNDANCY-01 |
| DS-EMS-10 | Gateway placement per Grade-A zone | ≥ 2 VaiNet AP10 gateways per Grade-A zone with overlapping coverage | Custom | (transitive via parent URS) redundancy + FS-PLAT-04. | FS-PLAT-04 | OQ-GW-REDUNDANCY-01 |

### 4.2 Cleanroom Grade A/B/C/D Mapping

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EMS-11 | Location table — `annex1_grade` enum | `{A, B, C, D, CNC}` (required per location) | Custom | FS-GRADE-01 verbatim. | FS-GRADE-01 | OQ-LOC-GRADE-01 |
| DS-EMS-12 | Location table — ISO 14644-1 class columns | `iso14644_class_at_rest`, `iso14644_class_in_operation` per location | Custom | FS-GRADE-02. | FS-GRADE-02 | OQ-LOC-GRADE-01 |
| DS-EMS-13 | Per-grade limit table | `limit_table_per_grade.yaml` stores T / RH / DP / particle limits at-rest + in-operation per grade; Microbiology Manager signature required on limit-change CRs | Custom | FS-GRADE-03 + Annex 1 § 9 + ISO 14644-1 limits. | FS-GRADE-03 | OQ-LIMIT-TABLE-01 |
| DS-EMS-14 | CPM-required locations | Grade-A + Grade-B locations enforced in `cpm_required_locations` table; missing CPM raises critical alarm | Custom | FS-GRADE-04 + Annex 1 § 9.16. | FS-GRADE-04 | OQ-CPM-PRESENCE-01 |
| DS-EMS-15 | Grade-A CPM HA pairing | ≥ 2 CPM units per Grade-A location; `CPM_LOSS_GRADE_A` critical alarm on loss of either | Custom | FS-GRADE-05. | FS-GRADE-05 | OQ-CPM-HA-01 |

### 4.3 Probes / Loggers / Particle Counters

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EMS-16 | `probe_inventory` table fields | unique-id, location, cal-cert-id, cal-due-date, probe_model, install_date, status | Default | FS-PROBE-01 + standard probe-inventory pattern. | FS-PROBE-01 | OQ-PROBE-INV-01 |
| DS-EMS-17 | Expired-calibration policy | Probes with `cal-due-date < now()` flagged `OUT-OF-SERVICE`; excluded from release-supporting reports | Custom | FS-PROBE-02. | FS-PROBE-02 | OQ-PROBE-CALEX-01 |
| DS-EMS-18 | Probe-drift detection | Configurable health-check thresholds per probe model; suspected drift raises `PROBE_DRIFT_<id>` maintenance alarm | Custom | FS-PROBE-03. | FS-PROBE-03 | OQ-PROBE-DRIFT-01 |
| DS-EMS-19 | Logging interval — cleanrooms | 1 minute default | Default | FS-PROBE-04; viewLinc default. | FS-PROBE-04 | OQ-LOG-RATE-01 |
| DS-EMS-20 | Logging interval — warehouses | 5 minutes default | Default | FS-PROBE-04. | FS-PROBE-04 | OQ-LOG-RATE-01 |
| DS-EMS-21 | Coincidence-loss correction | Lighthouse vendor coefficient applied at the boundary on CPM ingest | Default | FS-PROBE-05 + Lighthouse APM reference. | FS-PROBE-05 | OQ-CPM-COINCIDENCE-01 |

### 4.4 Continuous Particle Monitoring

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EMS-22 | Grade-A CPM acquisition | Continuous through entire critical-zone operation; ≥ 0.5 µm + ≥ 5 µm channels reported per Annex 1 § 9.16; OPC UA / Modbus from APM units; vendor sampling rate | Default (regulator-mandated) | FS-CPM-01 + Annex 1 § 9.16. | FS-CPM-01 | OQ-CPM-GRADE-A-01 |
| DS-EMS-23 | Grade-B CPM acquisition | Per site EM plan `cpm_schedule.yaml`; during operations | Custom | FS-CPM-02. | FS-CPM-02 | OQ-CPM-GRADE-B-01 |
| DS-EMS-24 | CPM-batch linkage | PAS-X `EM-batch-relevance` API queries; linked rows in `cpm_batch_link` | Custom | FS-CPM-03; required for batch-release reports. | FS-CPM-03 | OQ-CPM-BATCH-01 |
| DS-EMS-25 | At-rest classification scheduling | `qualification_scheduler` per location; results in `classification_results` | Custom | FS-CPM-04 + ISO 14644-2. | FS-CPM-04 | OQ-AT-REST-CLASS-01 |

### 4.5 Alarm Logic and Excursion Handling

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EMS-26 | Alarm severity classes | `{INFORMATION, WARNING, ACTION_LIMIT, ALERT_LIMIT}` enum | Default | FS-ALARM-01 verbatim. | FS-ALARM-01 | OQ-ALARM-CLASS-01 |
| DS-EMS-27 | Alarm-routing matrix | `alarm_routing.yaml` maps (severity × grade) → channels (operator screen, email, SMS, push) | Custom | FS-ALARM-01. | FS-ALARM-01 | OQ-ALARM-ROUTING-01 |
| DS-EMS-28 | Action/Alert acknowledgement requirement | Ack with reason captured; unacknowledged > 30 min window → auto-create MasterControl deviation | Custom | FS-ALARM-02. | FS-ALARM-02 | OQ-ALARM-ACK-01 |
| DS-EMS-29 | Grade-A/B redundant channels | Two independent channels (SMS via Twilio + email via AWS SES; push via FCM as third) | Custom | FS-ALARM-03 redundancy; multi-vendor avoids common-mode failure. | FS-ALARM-03 | OQ-ALARM-REDUNDANCY-01 |
| DS-EMS-30 | Channel-failure monitor | Synthetic ping per channel every 5 min; any-channel failure raises `CHANNEL_DEGRADED` warning | Custom | FS-ALARM-03 implementation; matches site OT-security baseline. | FS-ALARM-03 | OQ-CHANNEL-MONITOR-01 |
| DS-EMS-31 | Alarm-ack latency SLO | P95 ≤ 30 s; measured by synthetic monitoring runbook | Custom | FS-ALARM-04 + NFR-01. | FS-ALARM-04 | PQ-ALARM-LATENCY-01 |
| DS-EMS-32 | Excursion → batch linkage | PAS-X `EM-batch-relevance` API (location + time-window match); auto-deviation includes batch-impact list | Custom | FS-ALARM-05. | FS-ALARM-05 | OQ-EXCURSION-LINK-01 |

### 4.6 Viable Sampling Integration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EMS-33 | Viable-entry path | viewLinc form + REST pull from Watson LIMS `GET /viable/{location}/{date}` | Custom | FS-VIAB-01. | FS-VIAB-01 | OQ-VIAB-ENTRY-01 |
| DS-EMS-34 | Viable trend display | Unified dashboard with non-viable; exceedances vs `limit_table_per_grade.yaml` auto-deviate | Custom | FS-VIAB-02. | FS-VIAB-02 | OQ-VIAB-TREND-01 |
| DS-EMS-35 | Microbial-ID linkage | `microbial_id` table joined to viable-result records; surfaced in excursion-investigation view | Custom | FS-VIAB-03. | FS-VIAB-03 | OQ-MICROBIAL-ID-01 |
| DS-EMS-36 | Viable-sampling schedule | `viable_schedule.yaml` per location + cadence; `VIABLE_MISSED` warning on missed samples | Custom | FS-VIAB-04. | FS-VIAB-04 | OQ-VIABLE-SCHEDULE-01 |

### 4.7 Trend Analysis + Alert / Action Limits

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EMS-37 | Trend windows | 24-h, 7-d, 30-d rolling windows computed continuously | Default | FS-TREND-01. | FS-TREND-01 | OQ-TREND-WINDOW-01 |
| DS-EMS-38 | Trend dashboard | Grafana dashboard `pxc-em-trends` queries viewLinc Reporter API | Custom | FS-TREND-01 surfacing; Grafana already standard at site for trend visualisation. | FS-TREND-01 | OQ-TREND-DASH-01 |
| DS-EMS-39 | Recurring-excursion detector | ≥ N excursions in rolling window (N configurable per grade/parameter); triggers trend-investigation per Annex 1 § 9 | Custom | FS-TREND-02 + Annex 1 § 9. | FS-TREND-02 | OQ-TREND-RECURR-01 |
| DS-EMS-40 | Periodic-review report content | Aggregates: false-positive / false-negative metrics, alert/action limit excursions, calibration-overdue counts | Custom | FS-TREND-03. | FS-TREND-03 | OQ-PR-REPORT-01 |
| DS-EMS-41 | Limit-change tracking | `limit_change_history` records every limit change; trend-baseline recomputed automatically | Custom | FS-TREND-04. | FS-TREND-04 | OQ-LIMIT-CHANGE-01 |

### 4.8 Audit Trail

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EMS-42 | Audit-event coverage | `audit_events` table captures: config changes, data corrections, alarm acks, viable entries, signatures | Default | FS-AUD-01 + Annex 11 § 9. | FS-AUD-01 | OQ-AUD-COVERAGE-01 |
| DS-EMS-43 | Append-only enforcement | DB triggers prevent UPDATE / DELETE on `audit_events`; admin role denied at DB grant level | Custom | FS-AUD-02; DB-trigger pattern stronger than role-level alone. | FS-AUD-02 | OQ-AUD-APPENDONLY-01 |
| DS-EMS-44 | Monthly audit-trail review | EM Reviewer signs monthly review evidence; quarterly QA Compliance review | Default | FS-AUD-03. | FS-AUD-03 | OQ-AUD-REVIEW-01 |
| DS-EMS-45 | Audit-trail retention | 25 y in `audit_events_archive` on S3 Object Lock Compliance mode | Default (regulator-mandated) | FS-AUD-04; matches PIC/S PI 041 expectation. | FS-AUD-04 | OQ-ARCHIVAL-01 |

### 4.9 21 CFR Part 11

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EMS-46 | § 11.10(a) procedural controls | SOPs under `/sop/`; reviewed annually | Default | FS-PART11-01. | FS-PART11-01 | OQ-PART11-01 |
| DS-EMS-47 | § 11.10(d) access control | AD Kerberos + MFA via Yubikey at viewLinc Web client and Mobile | Custom | FS-PART11-02; site OT MFA standard. | FS-PART11-02 | OQ-PART11-02 |
| DS-EMS-48 | § 11.10(e) audit operations | Audit-trail per DS-EMS-42; review per DS-EMS-44 | Default | FS-PART11-03. | FS-PART11-03 | OQ-AUD-COVERAGE-01 |
| DS-EMS-49 | § 11.50 e-signature manifestation | Printed name + date/time + meaning text; meaning enum validated server-side | Default | FS-PART11-04. | FS-PART11-04 | OQ-PART11-04 |
| DS-EMS-50 | § 11.70 signature binding | SHA-256(record) bound to signature payload; tamper invalidates signature on read | Custom | FS-PART11-05; standard binding pattern. | FS-PART11-05 | OQ-PART11-05 |
| DS-EMS-51 | § 11.100 unique signatures | AD HR-feed; reuse blocked at AD provisioning | Default | FS-PART11-06. | FS-PART11-06 | OQ-PART11-06 |
| DS-EMS-52 | § 11.200 re-authentication | Fresh Kerberos ticket max-age 5 min for sign-off | Custom | FS-PART11-07 + 21 CFR § 11.200. | FS-PART11-07 | OQ-PART11-07 |
| DS-EMS-53 | § 11.300 password policy | AD password policy: ≥ 14 chars, complexity, 90 d rotation, MFA | Default (site) | FS-PART11-08 + site `SEC-AD-POLICY-001`. | FS-PART11-08 | OQ-PART11-08 |

### 4.10 Reporting

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EMS-54 | Batch-release EM report content | Locations, time window, alarm summary, viable summary, signature page, SHA-256 report hash | Custom | FS-RPT-01. | FS-RPT-01 | OQ-RPT-BATCH-01 |
| DS-EMS-55 | Periodic trend reports | Configurable daily / weekly / monthly / quarterly; signed by EM Reviewer + Microbiology Manager | Default | FS-RPT-02. | FS-RPT-02 | OQ-RPT-PERIODIC-01 |
| DS-EMS-56 | Reports reference probe-cal-cert IDs | Reports include cal-cert IDs valid for the reported window | Custom | FS-RPT-03; required for inspection traceability. | FS-RPT-03 | OQ-RPT-CALCERT-01 |
| DS-EMS-57 | Per-grade summaries | Grade A / B / C / D summaries with Annex 1 limits applied | Custom | FS-RPT-04. | FS-RPT-04 | OQ-RPT-GRADE-01 |

### 4.11 Integrations

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EMS-58 | eQMS deviation push | Unacknowledged alarms > 30 min auto-create MasterControl deviation via `POST /api/v2/deviations`; idempotency key | Custom | FS-INT-EQMS-01. | FS-INT-EQMS-01 | OQ-INT-EQMS-01 |
| DS-EMS-59 | BMS HVAC cross-reference | BMS HVAC trend data consumed read-only via OPC UA; surfaced as cross-reference panel in viewLinc dashboards | Custom | FS-INT-BMS-01. | FS-INT-BMS-01 | OQ-INT-BMS-01 |
| DS-EMS-60 | Watson LIMS integration | REST endpoints `/viable/...` + `/microbial-id/...` consumed; mTLS | Custom | FS-INT-LIMS-01. | FS-INT-LIMS-01 | OQ-INT-LIMS-01 |
| DS-EMS-61 | PAS-X EM-relevance integration | `GET /em-relevance?location=&from=&to=`; returns batches affected; used for excursion linkage | Custom | FS-INT-MES-01. | FS-INT-MES-01 | OQ-INT-MES-01 |
| DS-EMS-62 | Halcyon Stability push | Excursion events affecting stored samples pushed to `POST /stability/excursion-impact` | Custom | FS-INT-STAB-01. | FS-INT-STAB-01 | OQ-INT-STAB-01 |
| DS-EMS-63 | AD integration | LDAPS / Kerberos to `pyxis.local`; AD groups `EMS-Operator`, `EMS-Reviewer`, `EMS-Microbiology`, `EMS-FacilitiesEng`, `EMS-Cal`, `EMS-Approver`, `EMS-Admin`, `EMS-Auditor` | Custom | FS-INT-AD-01 + FS-XSYS-AD-01. | FS-INT-AD-01 | OQ-INT-AD-01 |

### 4.12 Data Integrity (ALCOA+)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EMS-64 | Audit-write NOT-NULL constraint | `audit_events.actor_id` NOT NULL DB constraint | Default | FS-DI-01. | FS-DI-01 | OQ-DI-ATTRIB-01 |
| DS-EMS-65 | Export validation | PDF/A-3 + CSV export validated at OQ | Default | FS-DI-02. | FS-DI-02 | OQ-EXPORT-01 |
| DS-EMS-66 | NTP + gateway buffering | Gateway-side buffering preserves probe-side timestamps during short network outages | Custom | FS-DI-03. | FS-DI-03 | OQ-NTP-BUFFER-01 |
| DS-EMS-67 | Raw-reading immutability | Raw probe readings immutable; corrections recorded as new annotated values referencing original | Default | FS-DI-04. | FS-DI-04 | OQ-DI-IMMUTABLE-01 |
| DS-EMS-68 | Math regression-test | Rolling-average + ISO 14644 classification math regression-tested at OQ | Custom | FS-DI-05. | FS-DI-05 | OQ-DI-MATH-01 |
| DS-EMS-69 | Inspection-mode retrieval | Retrievable ≤ 1 BD via inspection-mode query in viewLinc Reporter | Custom | FS-DI-06. | FS-DI-06 | OQ-INSPECTION-RETRIEVAL-01 |

### 4.13 Backup / Performance / Security

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EMS-70 | DB backup mode | Nightly PITR-enabled DB backup to S3; 25 y retention | Custom | FS-BAK-01. | FS-BAK-01 | OQ-BAK-PITR-01 |
| DS-EMS-71 | Restore-test cadence | Quarterly scripted restore; QA witness sign-off | Default | FS-BAK-02. | FS-BAK-02 | OQ-BAK-RESTORE-01 |
| DS-EMS-72 | DR replication | RTO ≤ 4 h, RPO ≤ 5 min via SQL Server always-on (DS-EMS-04) | Custom | FS-BAK-03. | FS-BAK-03 | OQ-DR-REPLICATION-01 |
| DS-EMS-73 | OQ stress test | ≥ 30 days continuous logging at configured interval without data loss | Custom | FS-PERF-01. | FS-PERF-01 | OQ-STRESS-30D-01 |
| DS-EMS-74 | Trend-report generation SLO | P95 ≤ 30 s for 96-h × 30 locations test case | Custom | FS-PERF-02. | FS-PERF-02 | PQ-PERF-REPORT-01 |
| DS-EMS-75 | Account management | AD-managed accounts; break-glass admin sealed in HashiCorp Vault | Custom | FS-SEC-01. | FS-SEC-01 | OQ-SEC-BREAKGLASS-01 |
| DS-EMS-76 | Channel auth + rate-limit | SMS / email / push channels authenticated + rate-limited; egress allow-listed at firewall | Custom | FS-SEC-02. | FS-SEC-02 | OQ-SEC-CHANNELS-01 |
| DS-EMS-77 | Vuln-scan cadence | Tenable Nessus monthly; 30-day SLA on critical findings | Default (site) | FS-SEC-03. | FS-SEC-03 | OQ-SEC-SCAN-01 |

### 4.14 Training / Periodic Review

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EMS-78 | LMS curriculum mapping | Cornerstone LMS `PXC-CURR-EMS-<role>-v1` per role | Custom | FS-TRN-01. | FS-TRN-01 | OQ-LMS-GATE-01 |
| DS-EMS-79 | Annual refresher | `EMS-2026-ANNUAL` covers Annex 1 (2022) updates + viable-sampling SOPs | Custom | FS-TRN-02. | FS-TRN-02 | OQ-LMS-GATE-01 |
| DS-EMS-80 | Periodic-review template | `PXC-PR-EMS-YYYYMMDD` covers configuration drift, calibration status, alarm performance, viable trends, limit changes, backup/restore, training; signed by Facilities Engineering Lead + Microbiology Manager + Head of QA | Custom | FS-PR-01. | FS-PR-01 | OQ-PR-RUNBOOK-01 |

### 4.15 Additional configuration detail

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EMS-81 | Probe firmware baseline | Vaisala HMP155 firmware v4.4.1; DPT145 v2.3.2; PTU307 v3.1.0 | Custom | Vendor-supported baselines at site go-live; pinned for revalidation triggering. | FS-PROBE-01 | OQ-PROBE-INV-01 |
| DS-EMS-82 | Lighthouse APM firmware baseline | Lighthouse APM v8.3 firmware (5004P / 5010P models) | Custom | Vendor-supported baseline; matches Lighthouse APM Reference Manual v3.0. | FS-CPM-01 | OQ-CPM-FIRMWARE-01 |
| DS-EMS-83 | CPM HA-pair failover detection window | 5 s loss-of-heartbeat before `CPM_LOSS_GRADE_A` critical alarm fires | Custom | Per Lighthouse APM reference; 5 s avoids transient-noise false positives while keeping detection latency low. | FS-GRADE-05 | OQ-CPM-HA-01 |
| DS-EMS-84 | Recurring-excursion detector — Grade A | ≥ 3 excursions in 7-d rolling window per location triggers trend-investigation | Custom | Site EM-plan threshold; tighter than Grade B/C/D per Annex 1 § 9 attention. | FS-TREND-02 | OQ-TREND-RECURR-01 |
| DS-EMS-85 | Recurring-excursion detector — Grade B/C/D | ≥ 5 excursions in 30-d rolling window per location | Custom | Site EM-plan threshold for less-critical grades. | FS-TREND-02 | OQ-TREND-RECURR-01 |
| DS-EMS-86 | `actor_id` audit-write constraint propagation | NOT NULL + FK to AD-principal table on every audit-trail-emitting table | Custom | FS-DI-01 hardened — FK ensures principal exists. | FS-DI-01 | OQ-DI-ATTRIB-01 |
| DS-EMS-87 | Periodic-review report runner schedule | Annual auto-run on first business day of Q1; manual on-demand permitted | Custom | FS-PR-01 + site annual-review calendar. | FS-PR-01 | OQ-PR-RUNBOOK-01 |
| DS-EMS-88 | Inspection-mode time-bound read-only access | 7 day default time-bound; tied to AD group `EMS-Inspection-RO` with auto-expiry | Custom | URS § 4 role + § 5.13 PR review; auto-expiry prevents stale access. | FS-PART11-02 | OQ-INSPECTION-MODE-01 |

## 5. Workflow + Business-Rule Design

### 5.1 Alarm-routing workflow

```
Probe / CPM reading
        │
        ▼
Limit-check (per `limit_table_per_grade.yaml`)
        │
        ▼
Severity classifier (`alarm_routing.yaml`)
        │
        ├─► INFORMATION → viewLinc operator screen only
        ├─► WARNING       → operator screen + email
        ├─► ACTION_LIMIT  → operator screen + email + SMS (two-channel for Grade A/B)
        └─► ALERT_LIMIT   → operator screen + email + SMS + FCM push (three-channel)
                                                │
                                                ▼
                                          Ack required within window (30 min default)
                                                │
                                                ▼
                                          Unacknowledged > window
                                                │
                                                ▼
                                          Auto-create MasterControl deviation
                                                │
                                                ▼
                                          Excursion → batch-impact lookup via PAS-X
                                                │
                                                ▼
                                          Halcyon Stability push (if stored samples affected)
```

### 5.2 Viable-EM workflow

1. EM Reviewer captures viable sample in field (settle / contact / active-air) per `viable_schedule.yaml`.
2. Sample submitted to Microbiology lab; LIMS records result + microbial ID.
3. Watson LIMS exposes result via REST `/viable/{location}/{date}`.
4. viewLinc pulls and persists viable result joined to (location, sample-time, grade, analyst).
5. Viable result evaluated against per-grade alert / action limits (DS-EMS-13). Exceedance triggers viewLinc alarm via DS-EMS-32 alarm pipeline.
6. Microbial-ID record linked via `microbial_id` table for excursion investigation (DS-EMS-35).

### 5.3 Excursion → batch-impact linkage

Triggered by any Action / Alert alarm or viable exceedance:

1. viewLinc queries PAS-X `GET /em-relevance?location=<loc>&from=<alarm_start - 4h>&to=<alarm_end>`.
2. PAS-X returns batches affected (batch_id, recipe, start_ts, end_ts).
3. viewLinc auto-creates MasterControl deviation including batch-impact list.
4. For Grade A/B locations affecting stored stability samples, push to Halcyon `POST /stability/excursion-impact`.

### 5.4 Limit-change workflow

1. Microbiology Manager + QA Approver author limit-change CR in MasterControl.
2. On CR approval, EMS Configuration Engineer applies via viewLinc Configuration UI.
3. Change captured in `limit_change_history`; trend baseline recomputed (DS-EMS-41).
4. Periodic-review report (DS-EMS-80) lists all limit changes in the period.

### 5.5 Gateway-degradation workflow

The VaiNet gateway mesh implements ≥ 1-hop redundancy per zone (DS-EMS-09). The viewLinc Gateway Health service runs every 60 seconds:

1. Probe-traffic counters checked per gateway; expected vs actual ratio computed.
2. If any zone's redundancy hops drops to 0 (single-gateway dependency), `GW_DEGRADED` WARNING alarm raises, routed to Facilities Engineer.
3. If a Grade-A zone loses all gateway coverage (unlikely; required mitigation), `GW_LOST_GRADE_A` ACTION_LIMIT alarm raises, routed via two-channel redundancy (DS-EMS-29).
4. Reduced-redundancy state surfaces in the EMS Operations dashboard with a coloured banner.

### 5.6 At-rest classification scheduling workflow

ISO 14644-2 at-rest classification (DS-EMS-25):

1. `qualification_scheduler` reads per-location cadence from `at_rest_class_schedule.yaml`.
2. On due-date, work order generated for Facilities Engineering to perform classification using Lighthouse ApexZ portable counters.
3. Classification results entered via viewLinc Classification UI; auto-compared against `iso14644_class_at_rest` for the location.
4. Pass/fail recorded in `classification_results`; fail triggers `AT_REST_CLASS_FAIL` ACTION_LIMIT alarm.

## 6. Role-Permission Matrix Design

| Action / Role | Operator / Shift Lead | EM Reviewer | Microbiology / EM Manager | Facilities Engineer | Calibration Coord. | EM Approver / QA | System Admin | Auditor | Inspection-Read-Only |
|---|---|---|---|---|---|---|---|---|---|
| View live status | R | R | R | R | R | R | R | R | R |
| Acknowledge alarms | C/U | C/U | — | — | — | — | — | — | — |
| Enter viable EM result | — | C/U | C/U | — | — | — | — | — | — |
| Approve viable-result final disposition | — | — | S | — | — | S | — | — | — |
| Configure locations / probes / alarm rules | — | — | — | C/U | — | — | — | — | — |
| Approve configuration change | — | — | — | — | — | S | — | — | — |
| Update probe calibration metadata | — | — | — | — | C/U | — | — | — | — |
| Author / approve EM report (batch release) | — | C/U | S | — | — | S | — | — | — |
| Co-approve alert/action limit change | — | — | S | — | — | S | — | — | — |
| Sign periodic review | — | — | S | S | — | S | — | — | — |
| Patch / OS / AD groups | — | — | — | — | — | — | C/U | — | — |
| Read-only audit-trail view | R | R | R | R | R | R | R | R | R |
| Read-only inspection mode (time-bound) | — | — | — | — | — | — | — | — | R |

Legend: R = read, C = create, U = update, S = sign (re-authenticated electronic signature), — = denied.

**Cell-level SoD denies (per URS § 4):**

- Operator ≠ Reviewer ≠ Approver of the same EM report.
- Facilities Engineer ≠ Approver of own configuration change.
- Limit-change CR requires Microbiology Manager AND QA Approver co-signatures; either party alone is denied.

## 7. Integration Design

| IF-ID | Counterparty | Endpoint | Protocol | Direction | AuthN | Message schema | Retry / DLQ | Audit emission | FS-IDs traced |
|---|---|---|---|---|---|---|---|---|---|
| IF-EQMS-01 | MasterControl eQMS | `POST https://eqms.pyxis.local/api/v2/deviations` | REST mTLS | outbound | mTLS + Entra workload-identity | JSON deviation incl. idempotency key `pxc-ems-{alarm_id}` | exponential backoff 1/2/4/8/16 s; DLQ at 5; idempotent on key | `audit_events.DEVIATION_RAISED` | FS-INT-EQMS-01, FS-XINT-EQMS-01 |
| IF-BMS-01 | Site BMS | `opc.tcp://bms.pyxis.local:4840` | OPC UA `Sign+Encrypt` Basic256Sha256 | inbound | site PKI client cert | OPC UA MonitoredItem subscriptions on BMS HVAC tags | local-cache last value 60 s on disconnect; `BMS_LINK_LOST` warning | `audit_events.BMS_LINK_STATUS` | FS-INT-BMS-01 |
| IF-LIMS-01 | Watson LIMS | `https://lims.pyxis.local/api/v1` (`/viable/*`, `/microbial-id/*`) | REST mTLS | bidirectional | mTLS + OAuth2 service account in Vault | JSON viable + microbial-ID schemas | exponential backoff; DLQ at 5; reconciliation job nightly | `audit_events.LIMS_FETCH` | FS-INT-LIMS-01 |
| IF-MES-01 | PAS-X v3.2 | `https://pasx.pyxis.local/api/v1/em-relevance` | REST mTLS | outbound query | mTLS | query `{location, from, to}` → JSON list of batches | exponential backoff; warning on persistent fail | `audit_events.MES_QUERY` | FS-INT-MES-01 |
| IF-STAB-01 | Halcyon Stability | `POST https://halcyon.pyxis.local/api/v1/stability/excursion-impact` | REST mTLS | outbound | mTLS | JSON impact payload incl. shipment-loc, time-window, excursion details | exponential backoff; DLQ at 5 + alarm | `audit_events.STAB_PUSH` | FS-INT-STAB-01 |
| IF-AD-01 | AD / Kerberos | `ldaps://ad.pyxis.local:636` + `kerberos://ad.pyxis.local:88` | LDAPS + Kerberos | bidirectional | machine cert + Kerberos | LDAP + Kerberos standard | local-cache 24 h offline | `audit_events.AUTHN` (forwarded to Splunk index `gxp-authn`) | FS-INT-AD-01, FS-XSYS-AD-01 |
| IF-NTP-01 | Site NTP master | `ntp://ntp.pyxis.local:123` | NTP v4 | inbound | none (isolated VLAN) | NTP standard | hold-over via local clock 5 min if master lost; > 1 s skew flagged | clock-skew metric in Prometheus | FS-DI-03 |
| IF-CHAN-SMS | Twilio | `https://api.twilio.com/2010-04-01/Accounts/<sid>/Messages.json` | REST HTTPS | outbound | API key in Vault | SMS payload `{to, body}` | exponential backoff; egress allow-listed | `audit_events.ALARM_CHANNEL_FIRE` | FS-ALARM-03, FS-SEC-02 |
| IF-CHAN-EMAIL | AWS SES | `https://email.eu-west-1.amazonaws.com/` | REST HTTPS | outbound | IAM signed (workload-identity) | SES message | exponential backoff | `audit_events.ALARM_CHANNEL_FIRE` | FS-ALARM-03, FS-SEC-02 |
| IF-CHAN-PUSH | FCM | `https://fcm.googleapis.com/fcm/send` | REST HTTPS | outbound | OAuth2 service account | FCM message | exponential backoff | `audit_events.ALARM_CHANNEL_FIRE` | FS-ALARM-03, FS-SEC-02 |
| IF-PKI-01 | Site PKI | site cert-manager service | ACME-equivalent | bidirectional | machine cert | cert-rotation ≤ 12 m | retry next interval; alert at 30 d before expiry | cert-rotation audit | FS-PLAT-06-equivalent (site default) |
| IF-VAULT-01 | HashiCorp Vault | `https://vault.pyxis.local/v1/kv/ems/*` | HTTPS AppRole | inbound | AppRole + Yubikey | KV v2 | retry on rotation interval | vault-access audit | FS-SEC-01, FS-XSYS-AD-01 (break-glass) |

### 7.0.1 Network port and certificate inventory

All inter-service communications between the viewLinc cluster, the integration counterparties, and the alarm-channel providers transit specific TCP/UDP ports. The site OT-DMZ firewall implements deny-by-default with the following allow-listed flows (one row per protocol-port-endpoint triple). Site PKI issues every TLS client cert with ≤ 12-month validity (DS-EMS site default).

- viewLinc Active ↔ AD `ldaps://ad.pyxis.local:636`, Kerberos `88/tcp`+`88/udp`; certs: viewLinc-server-cert, AD machine-cert.
- viewLinc Active ↔ MasterControl `https://eqms.pyxis.local:443`; mTLS; certs: viewLinc-client-cert, eQMS-server-cert.
- viewLinc Active ↔ Watson LIMS `https://lims.pyxis.local:443`; mTLS; certs: viewLinc-client-cert, lims-server-cert.
- viewLinc Active ↔ PAS-X `https://pasx.pyxis.local:443`; mTLS; certs: viewLinc-client-cert, pasx-server-cert.
- viewLinc Active ↔ Halcyon `https://halcyon.pyxis.local:443`; mTLS; certs: viewLinc-client-cert, halcyon-server-cert.
- viewLinc Active ↔ BMS `opc.tcp://bms.pyxis.local:4840`; OPC UA `Sign+Encrypt` Basic256Sha256; certs: viewLinc-opcua-cert, bms-opcua-cert.
- viewLinc Active → Twilio `api.twilio.com:443` (via egress proxy with allow-list).
- viewLinc Active → AWS SES `email.eu-west-1.amazonaws.com:443` (via egress proxy).
- viewLinc Active → FCM `fcm.googleapis.com:443` (via egress proxy).
- viewLinc Active ↔ Vault `https://vault.pyxis.local:8200`; AppRole.
- All servers ↔ Site NTP `ntp.pyxis.local:123` UDP.

### 7.1 Integration sequence — alarm-fire → eQMS deviation

1. Limit-check fires `ALERT_LIMIT` severity for Grade A location LOC-A-03 (CPM 0.5 µm channel above limit).
2. viewLinc routes to operator screen + Twilio SMS + AWS SES email + FCM push (DS-EMS-29).
3. Operator acknowledges within 30 min window: `audit_events.ALARM_ACK` written; deviation path NOT triggered.
4. If unacknowledged > 30 min: viewLinc queries PAS-X `GET /em-relevance` for batch-impact list.
5. viewLinc `POST /api/v2/deviations` to MasterControl with idempotency key `pxc-ems-<alarm_id>`; payload includes batch-impact list, location, time-window, parameter values.
6. On 2xx: emit `DEVIATION_RAISED` audit event; deviation_id stored on alarm record.
7. On 4xx/5xx: exponential backoff (1, 2, 4, 8, 16 s); after 5 attempts → DLQ + secondary alarm `DEVIATION_PUSH_FAILED`.

### 7.1.1 Idempotency contract for IF-EQMS-01

The deviation-create call uses idempotency key `pxc-ems-<alarm_id>`. MasterControl's `/api/v2/deviations` endpoint honours idempotent retries: repeated POSTs with the same key + identical body return the original deviation record (200 OK). The implementation never sends a "force-create" override flag. If a retry encounters a payload divergence vs the original (e.g., batch-impact list updated mid-retry), the endpoint returns 409 Conflict and viewLinc audit-logs the divergence as a `DEVIATION_RETRY_CONFLICT` event for manual reconciliation.

### 7.1.2 Status-callback handling (FS-XINT-EQMS-02)

eQMS ticket-status webhook `eqms.status.v1` is subscribed at `https://viewlinc.pyxis.local/api/v1/webhooks/eqms-status`. On receipt of a status update, the consumer rule maps eQMS status `(OPEN, IN-PROGRESS, EFFECTIVENESS, CLOSED)` onto the originating alarm record's `eqms_status` field. The originating alarm record's disposition workflow is gated: disposition cannot complete until `eqms_status = CLOSED`.

### 7.2 Integration sequence — viable result entry → excursion path

1. EM Reviewer enters viable result in viewLinc form, OR LIMS polling pulls fresh result.
2. Result joined to (location, sample-time, grade, analyst); `audit_events.VIABLE_ENTRY` written.
3. Limit-check vs per-grade alert/action limit (DS-EMS-13).
4. Exceedance enters the alarm pipeline (DS-EMS-26 .. DS-EMS-32).
5. If microbial ID available, linked via `microbial_id` table; surfaced in excursion-investigation view (DS-EMS-35).

## 8. Site-Deployed Components Design

The EMS includes the following site-deployed components beyond the vendor platform:

### 8.1 Grafana trend dashboard `pxc-em-trends` (DS-EMS-38)

- **Type:** Site-configured (declarative); no site-authored code.
- **Source:** viewLinc Reporter REST API; read-only.
- **Configuration:** `pxc-em-trends.json` panel definitions checked into site Grafana config repo under change control.
- **GAMP escalation:** Remains within Cat 4 scope; Grafana panels are declarative configuration.

### 8.2 Periodic-review report generator `pxc_pr_runner` (DS-EMS-80)

- **Type:** Vendor-supplied viewLinc Reporter template package; site-customised filters only (declarative).
- **Configuration:** Per-section query parameters in `pxc_pr_template.yaml`; templated via viewLinc Reporter macro language (no custom code).
- **GAMP escalation:** Remains within Cat 4; site customisation is declarative.

### 8.3 Reconciliation job `ems_reconcile.py` (LIMS / Halcyon / PAS-X integration housekeeping)

- **Type:** **Site-authored Python script** running on the viewLinc Active server (cron nightly).
- **Purpose:** Detects orphan excursions (no Halcyon assessment within 24 h), orphan viable-results (no LIMS microbial-ID within 7 d), stale BMS-link state.
- **Mini-SDS sub-section per METHODOLOGY § 2B.4 rule 6 (Cat 4 + Cat 5 hybrid component):**
  - **Module:** `ems_reconcile.py` v1.0.
  - **Inputs:** `audit_events` table reads; LIMS / Halcyon / PAS-X REST status queries; configuration YAML `reconcile_config.yaml`.
  - **Outputs:** Reconciliation report (CSV) written to `/var/log/ems-reconcile/`; alarms via viewLinc REST when orphans detected.
  - **Dependencies:** Python 3.12; `psycopg[binary]`, `requests`, `pyyaml`; pinned via `requirements.txt` + SHA-256.
  - **Tests:** pytest unit tests ≥ 85% line coverage; fixture-mocked source-system responses; pytest config in repo.
  - **Audit emission:** Every reconciliation cycle writes `audit_events.RECONCILIATION_RUN` with summary.
  - **Change control:** Source in site GitLab `pyxis/ems-reconcile`; signed commits required; deployment via ArgoCD requires CR.
  - **Verified by:** OQ-RECONCILE-01.
- **GAMP escalation:** Per METHODOLOGY § 2B.4 rule 6, this site-authored Python script makes this Cat 4 system a hybrid Cat 4 + Cat 5 for the scope of this script. The mini-SDS above is the Cat 5 sub-component's design surface.

## 9. References

### US — FDA / CFR / USP
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .22, .42.
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026).
- USP <1116>.

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EU GMP Annex 1 (2022 revised) — Manufacture of Sterile Medicinal Products; Contamination Control Strategy.
- EU GMP Chapter 4.

### International — ISO / PIC/S
- ISO 14644-1, -2, -3.
- ISO 14698-1, -2.
- PIC/S PI 041.

### Industry — ISPE
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE Good Practice Guide — *Environmental Monitoring*.

### Vendor
- Vaisala — *viewLinc 5.2 Installation, Configuration, and Administration Reference* v1.0.
- Vaisala — *viewLinc 5.2 Reporter Macro Language Reference* v1.0.
- Lighthouse Worldwide Solutions — *APM Reference Manual* v3.0.
- Lighthouse Worldwide Solutions — *ApexZ Portable Particle Counter Reference* v2.0.

### Site
- `BMS-CSV-2024-002` — BMS validation reference.
- `PXC-RB-EMS-FAILOVER-001` — viewLinc failover runbook.
- `SEC-AD-POLICY-001` — site AD password policy.

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-EMS-01 | FS-PLAT-01 |
| DS-EMS-02 | FS-PLAT-01 |
| DS-EMS-03 | FS-PLAT-01 |
| DS-EMS-04 | FS-PLAT-01 / FS-BAK-03 |
| DS-EMS-05 | FS-PLAT-02 |
| DS-EMS-06 | FS-PLAT-02 |
| DS-EMS-07 | FS-PLAT-03 |
| DS-EMS-08 | FS-PLAT-03 |
| DS-EMS-09 | FS-PLAT-04 |
| DS-EMS-10 | FS-PLAT-04 |
| DS-EMS-11 | FS-GRADE-01 |
| DS-EMS-12 | FS-GRADE-02 |
| DS-EMS-13 | FS-GRADE-03 |
| DS-EMS-14 | FS-GRADE-04 |
| DS-EMS-15 | FS-GRADE-05 |
| DS-EMS-16 | FS-PROBE-01 |
| DS-EMS-17 | FS-PROBE-02 |
| DS-EMS-18 | FS-PROBE-03 |
| DS-EMS-19 | FS-PROBE-04 |
| DS-EMS-20 | FS-PROBE-04 |
| DS-EMS-21 | FS-PROBE-05 |
| DS-EMS-22 | FS-CPM-01 |
| DS-EMS-23 | FS-CPM-02 |
| DS-EMS-24 | FS-CPM-03 |
| DS-EMS-25 | FS-CPM-04 |
| DS-EMS-26 | FS-ALARM-01 |
| DS-EMS-27 | FS-ALARM-01 |
| DS-EMS-28 | FS-ALARM-02 |
| DS-EMS-29 | FS-ALARM-03 |
| DS-EMS-30 | FS-ALARM-03 |
| DS-EMS-31 | FS-ALARM-04 |
| DS-EMS-32 | FS-ALARM-05 |
| DS-EMS-33 | FS-VIAB-01 |
| DS-EMS-34 | FS-VIAB-02 |
| DS-EMS-35 | FS-VIAB-03 |
| DS-EMS-36 | FS-VIAB-04 |
| DS-EMS-37 | FS-TREND-01 |
| DS-EMS-38 | FS-TREND-01 |
| DS-EMS-39 | FS-TREND-02 |
| DS-EMS-40 | FS-TREND-03 |
| DS-EMS-41 | FS-TREND-04 |
| DS-EMS-42 | FS-AUD-01 |
| DS-EMS-43 | FS-AUD-02 |
| DS-EMS-44 | FS-AUD-03 |
| DS-EMS-45 | FS-AUD-04 |
| DS-EMS-46 | FS-PART11-01 |
| DS-EMS-47 | FS-PART11-02 |
| DS-EMS-48 | FS-PART11-03 |
| DS-EMS-49 | FS-PART11-04 |
| DS-EMS-50 | FS-PART11-05 |
| DS-EMS-51 | FS-PART11-06 |
| DS-EMS-52 | FS-PART11-07 |
| DS-EMS-53 | FS-PART11-08 |
| DS-EMS-54 | FS-RPT-01 |
| DS-EMS-55 | FS-RPT-02 |
| DS-EMS-56 | FS-RPT-03 |
| DS-EMS-57 | FS-RPT-04 |
| DS-EMS-58 | FS-INT-EQMS-01 |
| DS-EMS-59 | FS-INT-BMS-01 |
| DS-EMS-60 | FS-INT-LIMS-01 |
| DS-EMS-61 | FS-INT-MES-01 |
| DS-EMS-62 | FS-INT-STAB-01 |
| DS-EMS-63 | FS-INT-AD-01 / FS-XSYS-AD-01 |
| DS-EMS-64 | FS-DI-01 |
| DS-EMS-65 | FS-DI-02 |
| DS-EMS-66 | FS-DI-03 |
| DS-EMS-67 | FS-DI-04 |
| DS-EMS-68 | FS-DI-05 |
| DS-EMS-69 | FS-DI-06 |
| DS-EMS-70 | FS-BAK-01 |
| DS-EMS-71 | FS-BAK-02 |
| DS-EMS-72 | FS-BAK-03 |
| DS-EMS-73 | FS-PERF-01 |
| DS-EMS-74 | FS-PERF-02 |
| DS-EMS-75 | FS-SEC-01 |
| DS-EMS-76 | FS-SEC-02 |
| DS-EMS-77 | FS-SEC-03 |
| DS-EMS-78 | FS-TRN-01 |
| DS-EMS-79 | FS-TRN-02 |
| DS-EMS-80 | FS-PR-01 |
| DS-EMS-81 | FS-PROBE-01 |
| DS-EMS-82 | FS-CPM-01 |
| DS-EMS-83 | FS-GRADE-05 |
| DS-EMS-84 | FS-TREND-02 |
| DS-EMS-85 | FS-TREND-02 |
| DS-EMS-86 | FS-DI-01 |
| DS-EMS-87 | FS-PR-01 |
| DS-EMS-88 | FS-PART11-02 |

**FS-IDs in parent FS not directly covered by a DS-ID row** but addressed in § 7 Integration Design and § 8 Site-Deployed Components: FS-XSYS-BAK-01 (Veeam backup integration — site enterprise-backup-service binding, addressed at site backup-platform DS level per `AUR-URS-BACKUP-001`); FS-XINT-EQMS-02 (eQMS status webhook — covered by IF-EQMS-01 integration row + DS-EMS-58 idempotency / status-update behaviour). All FS-IDs accounted for.

## 11. Appendix B — Design-level Risk Register

| DR-ID | Design-stage risk | Origin design choice | Mitigation reference |
|---|---|---|---|
| DR-01 | SQL Server always-on synchronous-commit could block writes if standby goes down — viable-result entry and alarm-ack might stall | DS-EMS-04 chose synchronous for RPO ≤ 5 min | OQ-DR-REPLICATION-01 + degraded-mode runbook + read-only fallback design |
| DR-02 | Twilio / AWS SES / FCM channel outages could land simultaneously despite multi-vendor choice | DS-EMS-29 multi-vendor choice mitigates common-mode, not common-incident | DS-EMS-30 channel-health monitor + viewLinc operator-screen as ultimate fallback |
| DR-03 | 30-min ack window may be too long for Grade-A Annex 1 critical alarms during filling | DS-EMS-28 default 30 min | Site-SOP override to 5 min for Grade-A action-limit alarms; configurable per location |
| DR-04 | VaiNet wireless mesh could degrade under EMI from new HVAC commissioning without surfacing | DS-EMS-09 + DS-EMS-10 redundancy + `GW_DEGRADED` alarm | `GW_DEGRADED` alarm routed as WARNING; periodic-review reviews gateway-health history |
| DR-05 | CPM HA pair on Grade A could both fail from common-cause (power, cabling) | DS-EMS-15 HA pair on Grade A | Per-CPM separate power feed (site facilities scope); periodic-review item |
| DR-06 | Lighthouse coincidence-loss correction depends on vendor coefficient which may shift between firmware versions | DS-EMS-21 applies at boundary | Vendor-release impact-assessment SOP; periodic-review item |
| DR-07 | `audit_events` DB triggers preventing UPDATE/DELETE could be disabled by privileged DBA without detection | DS-EMS-43 DB trigger + role grant | DBA dual-control + monthly audit-trail review (DS-EMS-44) cross-checks |
| DR-08 | Grafana dashboard `pxc-em-trends` outage could mask trend degradation | DS-EMS-38 | Grafana is supplementary; viewLinc Reporter remains authoritative trend surface |
| DR-09 | `ems_reconcile.py` (DS-EMS site-authored Python) carries Cat 5 sub-component risk — defect could miss orphan excursions | § 8.3 mini-SDS | Cat 5 SDLC discipline: code review, ≥ 85% test coverage, signed commits, CR-gated deployment, regression tests vs fixture mocks |
| DR-10 | viewLinc Mobile (iOS) MFA via Yubikey requires hardware-token availability in cleanroom | DS-EMS-47 Yubikey choice | Operational SOP: per-shift Yubikey assignment; backup tokens available |
| DR-11 | S3 Object Lock Compliance mode + 25 y retention is irreversible — wrong-data-archived cannot be deleted | DS-EMS-45 Compliance mode | Pre-archive validation step; chosen Compliance over Governance for strongest tamper-resistance |
| DR-12 | Trend-baseline auto-recompute on limit change (DS-EMS-41) could mask gradual limit-creep over time | DS-EMS-41 + limit-change SoD (Microbiology Manager + QA Approver) | Periodic-review item tracks limit-change history; Microbiology Manager co-approval gate |
| DR-13 | Kerberos ticket max-age 5 min for sign-off could create operational friction at high alarm-volume periods | DS-EMS-52 chose 5 min over default 10 min | Operational acceptance per site SOP; alternative would weaken § 11.200 control |
| DR-14 | Probe firmware drift between vendor patches could shift drift-detection threshold sensitivity | DS-EMS-81 pinned firmware baseline | Vendor-release impact-assessment SOP; periodic-review item tracks firmware-update history |
| DR-15 | Lighthouse APM firmware update could change coincidence-loss coefficient | DS-EMS-82 pinned firmware baseline | Vendor-release impact-assessment SOP; re-verification at next at-rest classification cycle |
| DR-16 | Recurring-excursion threshold (DS-EMS-84/85) may produce false positives from sensor recalibration events | DS-EMS-84 + DS-EMS-85 thresholds | Microbiology Manager review of trend-investigation triggers; threshold reviewed at PR |
| DR-17 | Inspection-mode time-bound access (DS-EMS-88) could be re-issued repeatedly to circumvent ≥ 7 d limit | DS-EMS-88 auto-expiry | Re-issue requires QA Compliance signature; logged in audit-trail; periodic-review item |
| DR-18 | Annual auto-run of periodic review (DS-EMS-87) on Q1 first business day may collide with year-end maintenance windows | DS-EMS-87 schedule | Manual run permitted as fallback; operational SOP coordinates with maintenance |

## 12. Appendix C — Configuration Item Index by FS Module

For inspection-readiness, the table below indexes DS-IDs by the FS § 4 module they implement.

| FS Module | DS-IDs implementing |
|---|---|
| § 4.1 Platform / Hardware | DS-EMS-01 .. DS-EMS-10 |
| § 4.2 Cleanroom Grade A/B/C/D Mapping | DS-EMS-11 .. DS-EMS-15 |
| § 4.3 Probes / Loggers / Particle Counters | DS-EMS-16 .. DS-EMS-21, DS-EMS-81, DS-EMS-82 |
| § 4.4 Continuous Particle Monitoring | DS-EMS-22 .. DS-EMS-25, DS-EMS-83 |
| § 4.5 Alarm Logic and Excursion Handling | DS-EMS-26 .. DS-EMS-32 |
| § 4.6 Viable Sampling Integration | DS-EMS-33 .. DS-EMS-36 |
| § 4.7 Trend Analysis + Alert / Action Limits | DS-EMS-37 .. DS-EMS-41, DS-EMS-84, DS-EMS-85 |
| § 4.8 Audit Trail | DS-EMS-42 .. DS-EMS-45, DS-EMS-86 |
| § 4.9 21 CFR Part 11 | DS-EMS-46 .. DS-EMS-53, DS-EMS-88 |
| § 4.10 Reporting | DS-EMS-54 .. DS-EMS-57 |
| § 4.11 Integrations | DS-EMS-58 .. DS-EMS-63 |
| § 4.12 Data Integrity | DS-EMS-64 .. DS-EMS-69 |
| § 4.13 Backup / Performance / Security | DS-EMS-70 .. DS-EMS-77 |
| § 4.14 Training / Periodic Review | DS-EMS-78 .. DS-EMS-80, DS-EMS-87 |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
