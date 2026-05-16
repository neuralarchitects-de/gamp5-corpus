---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (v1.0 corpus genesis per METHODOLOGY § 2B)"
seed_corpus_basis:
  - "KYM-FS-HIST-001 v1.2 (parent FS)"
  - "KYM-URS-HIST-001 v1.2 (parent URS — transitive)"
  - "GAMP 5 (2nd ed.) Cat 4 conventions (DS treats this historian as a Configured Product per site project mode; parent FS / URS designation Cat 3 reflects vendor-design reliance, but site-side configuration density warrants the full CS shape per METHODOLOGY § 2B.1)"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "PIC/S PI 041; ISA-95 (IEC 62264); ISA-88 (IEC 61512); OPC UA (IEC 62541); IEC 62443; ISO/IEC 27001:2022"
parent_fs:
  document_number: KYM-FS-HIST-001
  version: "1.2"
  file: "../../../FS_FDS/_generated/final/Kymeta_Bio_Process_Historian_PI_FS_v1.3.md"
parent_urs:
  document_number: KYM-URS-HIST-001
  version: "1.2"
  file: "../../../URS/_generated/final/Process_Historian__Kymeta_Bio_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Process Historian — AVEVA PI System 2024 (PI Server + PI AF + PI Event Frames + PI Vision + PI Integrator + PI Web API)

**Document Number:** KYM-DS-HIST-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** KYM-FS-HIST-001 v1.2
**Parent URS:** KYM-URS-HIST-001 v1.2 *(informational; transitive)*
**Site:** Kymeta Bio ehf, Manufacturing IT Operations, Reykjavík, Iceland *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (DS scope is configuration density per site project mode; parent FS / URS notes Cat 3 vendor-design-reliance reflects the platform's underlying COTS nature, but the AVEVA PI System 2024 site deployment carries a configuration surface — points, AF templates, EF templates, Vision displays, Integrator views, security mappings — that warrants the full Configuration Specification shape per METHODOLOGY § 2B.1).
**Project Mode:** Configuration project on commercial software product **AVEVA PI System 2024 (PI Server + PI Vision + PI Asset Framework + PI Event Frames + PI Integrator + PI Web API)** (GAMP 5 Category 4 — Configured Product, with the explicit constraint that any GxP-critical PI Asset Analytics expression with site-authored logic escalates to a Cat 5 sub-component under separate change control).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200; EU GMP Annex 11 §§ 4, 6, 9, 11; PIC/S PI 041; ISA-95; ISA-88; OPC UA; IEC 62443; ISO/IEC 27001:2022.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Manufacturing IT Lead — SME) | _____________ | _____________ | _____ |
| Reviewer (Automation Engineer — SME) | _____________ | _____________ | _____ |
| Reviewer (Process Engineer) | _____________ | _____________ | _____ |
| Reviewer (OT-Security Architect) | _____________ | _____________ | _____ |
| Approver (System Owner — Manufacturing IT Lead) | _____________ | _____________ | _____ |
| Approver (Head of Operations) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial issue. Inherited Tier T3 from parent URS+FS pair. DS covers 95/97 FS-IDs; 2 FS-IDs flagged as vendor-internal — no site design surface (FS-AV-01 vendor SLA; FS-PERF-04 PI Asset Analytics latency is vendor-internal except where a site-authored GxP-critical expression triggers Cat 5 sub-component handling). Generated as part of the DS v1.0 corpus ship per METHODOLOGY § 2B (DS treated as Configuration Specification for the site-configurable surface). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

DS-specific terms only — URS / FS definitions inherited by reference.

| Term | Definition |
|---|---|
| CS | Configuration Specification (this document) |
| CI | Configuration Item — one configurable parameter, value, default-vs-custom flag, justification |
| Collector | PI Interface or PI Connector node sourcing data from PLC / SCADA / BMS / instrument |
| Tag | PI Point — single named time-series stream |
| AF Element | PI Asset Framework element (asset instance) |
| EF | PI Event Frame — time-bounded interval for ISA-88 batch / phase |
| Compression Triple | The (`CompDev`, `CompMin`, `CompMax`) per-point swinging-door compression parameters |

## 1. Purpose

This Configuration Specification (CS) is the technical-design layer between `KYM-FS-HIST-001` v1.2 and downstream configuration / IQ / OQ / PQ Protocols for the AVEVA PI System 2024 deployment at Kymeta Bio Reykjavík core + Akureyri downstream-fill site (multi-site federation). The DS declares, per configuration item, the chosen value, default-vs-custom flag, FS-ID(s) traced, and planned verification. Vendor source-code internals (PI Server swinging-door engine, PI AF reference-formula evaluator, PI Vision rendering pipeline) are not redrawn here — those remain under AVEVA SDLC.

## 2. Scope

### In scope

- PI Server Collective (active + DR replication topology).
- PI Asset Framework — hierarchy + element templates per ISA-95 Levels 0–3.
- PI Event Frames — templates per ISA-88 batch / unit-procedure / operation / phase.
- PI Vision web servers + displays + per-display ACL.
- PI Web API — endpoint exposure + rate limits + AuthN.
- PI Integrator — asset-aware export views to Databricks lakehouse.
- PI Notification — rule-based alert configuration.
- PI Asset Analytics — per-expression GxP classification (with Cat 5 sub-component handling for GxP-critical expressions).
- PI Interfaces / Connectors / Edge Data Store — per-source binding + ≥ 7 d local buffer.
- Multi-site federation (Reykjavík ↔ Akureyri).
- Compression + retention policy per tag.
- Archive tier-down (90 d default) to cold SAS storage + S3 Object Lock long-term archive.
- Audit-trail bindings, 21 CFR Part 11 controls, ALCOA+ disciplines, back-fill exception workflow.
- Integration endpoints to PAS-X MES (EF source + Web API consumer), LIMS (EF attribute consumer), SPC platform (Notification consumer), Databricks lakehouse (Integrator export sink), AD / NTP / PKI / HashiCorp Vault.

### Out of scope

- PLC / SCADA / BMS / instrument source systems (each has its own URS / FS / DS).
- Analytics consumers downstream of the historian (JMP separate URS).
- LIMS, eQMS application internals.

## 3. Architectural Overview

### 3.1 Logical view

```
   ┌─────────────────────────────────────────────────────────────┐
   │  AD / Kerberos    NTP infra    Site PKI    HashiCorp Vault   │
   └────────────┬───────────────┬───────────────────────────────┬──┘
                │               │                               │
   ┌────────────▼───────────────▼───────────────────────────────▼──┐
   │                AVEVA PI System 2024 — Reykjavík core           │
   │   ┌──────────────────────┐  ┌──────────────────────────────┐  │
   │   │ PI Server (active)    │  │ PI Server (DR — collective)  │  │
   │   │ Win Server 2022       │  │ collective replication ≤ 30 s │  │
   │   └──────────────────────┘  └──────────────────────────────┘  │
   │   ┌──────────────────────┐  ┌──────────────────────────────┐  │
   │   │ PI Asset Framework    │  │ PI Event Frames               │  │
   │   │ (ISA-95 hierarchy)    │  │ (ISA-88 batch/phase)          │  │
   │   └──────────────────────┘  └──────────────────────────────┘  │
   │   ┌──────────────────────┐  ┌──────────────────────────────┐  │
   │   │ PI Vision (LB, TLS    │  │ PI Web API (HA, mTLS)         │  │
   │   │ 1.3 termination)      │  └──────────────────────────────┘  │
   │   └──────────────────────┘  ┌──────────────────────────────┐  │
   │   ┌──────────────────────┐  │ PI Notification + Analytics   │  │
   │   │ PI Integrator         │  │ (GxP-critical analytics → Cat 5│  │
   │   │ (Databricks export)   │  │  sub-component flag)          │  │
   │   └──────────────────────┘  └──────────────────────────────┘  │
   │   ┌──────────────────────────────────────────────────────┐    │
   │   │ PI Interfaces / Connectors / Edge Data Store         │    │
   │   │   OPC UA Sign+Encrypt Basic256Sha256                 │    │
   │   │   OPC HDA (legacy backfill)                          │    │
   │   │   Modbus TCP (legacy PLCs)                           │    │
   │   │   Custom connectors (documented per spec)            │    │
   │   │   ≥ 7 d local buffer on cloud-link loss              │    │
   │   └──────────────────────────────────────────────────────┘    │
   └────────────┬──────────────────────────────────────────────────┘
                │
   ─── Federation: read-only at core ◄── Akureyri PI Server ───
                │
                ▼
   ┌──────────────────────────────────────────────────────────────┐
   │   Sources: PLC / SCADA / BMS / instruments (per-system URSs)  │
   └──────────────────────────────────────────────────────────────┘
```

### 3.2 Asset-Framework tree topology (ISA-95 Levels 0–3)

```
Enterprise
└── Kymeta Bio
    ├── Reykjavík Site
    │   ├── Area: Upstream Bulk
    │   │   ├── Production Line: Bioreactor Line 1
    │   │   │   ├── Process Cell: Cell-1A
    │   │   │   │   ├── Unit: BR-300A (Bioreactor 300 L)
    │   │   │   │   │   ├── Equipment Module: Agitation
    │   │   │   │   │   │   └── Control Module: AGIT-CTRL-01 (tags: speed_rpm, torque_nm, motor_temp_c)
    │   │   │   │   │   ├── Equipment Module: pH Control
    │   │   │   │   │   ├── Equipment Module: DO Control
    │   │   │   │   │   └── Equipment Module: Temperature Control
    │   │   │   │   └── Unit: BR-300B (Bioreactor 300 L)
    │   │   │   └── Process Cell: Cell-1B
    │   │   └── Production Line: Bioreactor Line 2
    │   ├── Area: Downstream Recovery
    │   ├── Area: Buffer Prep
    │   └── Area: Utilities (CIP / SIP / WFI / Pure Steam — GxP-critical tags)
    └── Akureyri Site
        ├── Area: Fill / Finish
        └── Area: Utilities
```

### 3.3 Collector layout (text diagram)

```
┌── Reykjavík core ────────────────────────────────────────────────┐
│  PI Interface Node 1 (PI-INT-01)  → OPC UA → Siemens S7-1500 PLCs│
│   tags: ~8,000 across bioreactor / downstream / buffer-prep      │
│  PI Interface Node 2 (PI-INT-02)  → OPC UA → AVEVA System Platform│
│   (SCADA)  tags: ~6,000 utility + WFI / pure-steam                │
│  PI Interface Node 3 (PI-INT-03)  → OPC HDA → legacy historian   │
│   backfill source for migration period                           │
│  PI Interface Node 4 (PI-INT-04)  → Modbus TCP → 4 legacy PLCs   │
│  PI Connector for OSIsoft Asset Analytics (vendor connector)    │
└──────────────────────────────────────────────────────────────────┘
┌── Akureyri downstream-fill ──────────────────────────────────────┐
│  PI Edge Data Store (PI-EDGE-AK-01)                              │
│   tags: ~3,500 fill / finish + utility                            │
│   7 d local buffer; federation to Reykjavík core                  │
└──────────────────────────────────────────────────────────────────┘
```

## 4. Configuration Specification

### 4.1 Platform / Hardware

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-01 | PI Server topology | Collective: 1 active + 1 DR | Default (AVEVA-recommended) | FS-PLAT-01; collective is AVEVA's standard HA pattern. | FS-PLAT-01 | OQ-COLLECTIVE-FAILOVER-01 |
| DS-HIST-02 | RPO target | ≤ 5 min via collective replication | Custom | FS-PLAT-01. | FS-PLAT-01 | OQ-COLLECTIVE-FAILOVER-01 |
| DS-HIST-03 | RTO target | ≤ 4 h via documented failover runbook `KYM-RB-PI-FAILOVER-001` | Custom | FS-PLAT-01. | FS-PLAT-01 | PQ-DR-FAILOVER-01 |
| DS-HIST-04 | Power resilience | All PI servers + interface nodes on UPS / generator-backed power | Default (site) | FS-PLAT-02; matches site OT infrastructure baseline. | FS-PLAT-02 | OQ-INTERFACE-BUFFER-01 |
| DS-HIST-05 | Edge buffer capacity | ≥ 7 d local-store capacity on PI Edge Data Store + interface nodes | Custom | FS-IF-EDGE-01; conservative buffer for Iceland inter-site link outage scenarios. | FS-PLAT-02, FS-IF-EDGE-01 | OQ-INTERFACE-BUFFER-01 |
| DS-HIST-06 | Manufacturing IT VLAN ID | VLAN 600 (Reykjavík); VLAN 605 (Akureyri); inter-site VPN tunnel | Custom | FS-PLAT-03 segregation from office network. | FS-PLAT-03 | OQ-NET-AUDIT-01 |
| DS-HIST-07 | PI Vision web tier | HA-Proxy active/active behind TLS 1.3 termination; backend health checks per 10 s | Custom | FS-PLAT-04. | FS-PLAT-04 | OQ-VISION-HA-01 |
| DS-HIST-08 | PI Web API + Integrator HA | 2-node Windows Server failover cluster; auto-failover ≤ 60 s | Custom | FS-PLAT-05. | FS-PLAT-05 | OQ-API-FAILOVER-01 |
| DS-HIST-09 | TLS certificate management | All certs issued from site PKI; auto-rotation via cert-manager; ≤ 12-month validity | Custom | FS-PLAT-06. | FS-PLAT-06 | OQ-PKI-ROTATE-01 |

### 4.2 Tag Naming + Point Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-10 | Tag naming convention | `PLANT.AREA.UNIT.TAGTYPE.NAME` (ISA-95 hierarchical) | Custom | FS-TAG-01. | FS-TAG-01 | OQ-TAG-NAMING-01 |
| DS-HIST-11 | GxP-critical-tag compression | `Compress = OFF`; archive every value | Custom | FS-TAG-02; required to preserve fidelity for GxP record reconstruction. | FS-TAG-02 | OQ-COMPRESSION-FIDELITY-01 |
| DS-HIST-12 | Non-GxP-tag compression | Swinging-door defaults (`CompDev=0.5*EngUnit_range`, `CompMin=1s`, `CompMax=8h`) | Default (AVEVA) | FS-TAG-02; non-GxP tags follow AVEVA defaults to reduce archive volume. | FS-TAG-02 | OQ-COMPRESSION-NONGXP-01 |
| DS-HIST-13 | GxP-relevance extended attribute | `GxP-relevance` boolean flag captured per point | Custom | FS-TAG-03. | FS-TAG-03 | OQ-TAG-ATTR-01 |
| DS-HIST-14 | Point-creation workflow form | Mandatory fields: source-system reference, UoM, scan-class, engineering-units, range, alarm-limits (where applicable), GxP-relevance, owner | Custom | FS-TAG-04. | FS-TAG-04 | OQ-POINT-WORKFLOW-01 |
| DS-HIST-15 | GxP-tag compression-change approval route | Point-Config-Approver workflow for GxP tags; non-GxP self-approval allowed | Custom | FS-TAG-05. | FS-TAG-05 | OQ-COMP-APPROVAL-01 |

### 4.3 ISA-95 Mapping

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-16 | AF hierarchy depth | 8 levels: Enterprise → Site → Area → Production Line → Process Cell → Unit → Equipment Module → Control Module | Default (ISA-95 spec) | FS-ISA95-01 + IEC 62264. | FS-ISA95-01 | OQ-ISA95-DEPTH-01 |
| DS-HIST-17 | Orphan-point check | Nightly orphan-check job lists PI Points not linked into AF; report to AF Author + Manufacturing IT Lead | Custom | FS-ISA95-02. | FS-ISA95-02 | OQ-ORPHAN-CHECK-01 |
| DS-HIST-18 | AF template versioning | `cv_af_template_versions` table; element instantiation stamps `template_version_id` | Custom | FS-ISA95-03. | FS-ISA95-03 | OQ-AF-VERSION-01 |
| DS-HIST-19 | OPC UA Server ISA-95 companion | PI OPC UA Server interface exposes ISA-95 companion-spec views for Level-4 consumers (ERP / BI) | Custom | FS-ISA95-04. | FS-ISA95-04 | OQ-OPCUA-COMPANION-01 |

### 4.4 Asset Framework

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-20 | AF template storage | Site config-repo `kymeta/pi-af-templates` GitLab; version-controlled; signed commits | Custom | FS-AF-01. | FS-AF-01 | OQ-AF-REPO-01 |
| DS-HIST-21 | AF-change dual-approval (GxP-batch reconstruction) | AF Author ≠ Approver; QA + Head of Ops co-approval at AD-group level | Custom | FS-AF-02. | FS-AF-02 | OQ-AF-CHANGE-DUAL-APPROVE-01 |
| DS-HIST-22 | AF formula GxP classification | `cv_af_formula_classification` table; GxP-critical formulas route through Cat-5 sub-component process | Custom | FS-AF-03. | FS-AF-03 | OQ-AF-FORMULA-CLASS-01 |
| DS-HIST-23 | AF UoM exposure | AF template attributes expose UoM via OPC UA UA-100 unit codes | Default | FS-AF-04. | FS-AF-04 | OQ-AF-UOM-01 |

### 4.5 Compression and Retention Policy

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-24 | Swinging-door params for GxP | `CompDev = 0` (no compression) | Custom | FS-COMP-01; required for GxP fidelity. | FS-COMP-01 | OQ-COMPRESSION-FIDELITY-01 |
| DS-HIST-25 | GxP retention | ≥ 25 y via archival policy `pi-archive-25y` | Default (regulator) | FS-COMP-02. | FS-COMP-02 | OQ-RETENTION-25Y-01 |
| DS-HIST-26 | Non-GxP retention | ≥ 5 y unless business-justified longer | Custom | FS-COMP-02. | FS-COMP-02 | OQ-RETENTION-5Y-01 |
| DS-HIST-27 | Compression-change downstream impact | Triggers impact assessment via change-control system; MES / LIMS consumers re-tested | Custom | FS-COMP-03. | FS-COMP-03 | OQ-COMP-CHANGE-IMPACT-01 |
| DS-HIST-28 | Compression-loss report | Runnable via PI SMT custom report on demand; actual vs theoretical archive size + value-recovery loss | Custom | FS-COMP-04. | FS-COMP-04 | OQ-COMP-LOSS-REPORT-01 |

### 4.6 Archive Tier-Down

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-29 | Primary storage tier | NVMe SAN; current archive shift + recent | Custom | FS-ARCH-01. | FS-ARCH-01 | OQ-STORAGE-TIER-01 |
| DS-HIST-30 | Cold tier | SAS RAID-6; prior archive shifts | Custom | FS-ARCH-01. | FS-ARCH-01 | OQ-STORAGE-TIER-01 |
| DS-HIST-31 | Tier-down age | 90 days default | Default | FS-ARCH-02. | FS-ARCH-02 | PQ-PERF-ARCH-01 |
| DS-HIST-32 | Query latency penalty after tier-down | P95 ≤ 5 s | Custom | FS-ARCH-02; matches (transitive via parent URS) SLO. | FS-ARCH-02 | PQ-PERF-ARCH-01 |
| DS-HIST-33 | Archive-shift integrity validation | SHA-256 checksum at every archive-shift event; failure → P1 PagerDuty | Custom | FS-ARCH-03. | FS-ARCH-03 | OQ-ARCH-INTEGRITY-01 |
| DS-HIST-34 | Long-term immutable archive | AWS S3 with Object Lock Compliance mode (25 y); SHA-256 manifest captured + verified | Custom | FS-ARCH-04. | FS-ARCH-04 | OQ-S3-EXPORT-01 |

### 4.7 Interface Devices (OPC UA / OPC HDA / Modbus / Edge)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-35 | OPC UA security mode | `Sign+Encrypt` | Default (vendor-recommended) | FS-IF-OPCUA-01. | FS-IF-OPCUA-01 | OQ-OPCUA-SEC-01 |
| DS-HIST-36 | OPC UA security policy floor | `Basic256Sha256` minimum | Default | FS-IF-OPCUA-01; matches OPC UA WG recommendation. | FS-IF-OPCUA-01 | OQ-OPCUA-SEC-01 |
| DS-HIST-37 | OPC UA certificate trust list | Governed by site PKI; rejected handshakes logged to `pi_audit.OPCUA_REJECT` | Custom | FS-IF-OPCUA-01. | FS-IF-OPCUA-01 | OQ-OPCUA-SEC-01 |
| DS-HIST-38 | OPC UA subscription model | `MonitoredItem`; sampling + publishing intervals per tag class in `pi-opcua-config.yaml` | Default | FS-IF-OPCUA-02. | FS-IF-OPCUA-02 | OQ-OPCUA-SUB-01 |
| DS-HIST-39 | OPC HDA backfill mechanism | `ReadAtTime` + `ReadProcessed`; overlap reconciliation report after every backfill | Custom | FS-IF-OPCHDA-01. | FS-IF-OPCHDA-01 | OQ-OPCHDA-BACKFILL-01 |
| DS-HIST-40 | Modbus TCP per-tag register mapping | Documented per legacy PLC in `pi-modbus-config.yaml` | Custom | FS-IF-MODBUS-01. | FS-IF-MODBUS-01 | OQ-MODBUS-MAP-01 |
| DS-HIST-41 | PI Edge Data Store local buffer | 7-day capacity; reconciliation queue exposed via Prometheus | Custom | FS-IF-EDGE-01. | FS-IF-EDGE-01 | OQ-EDGE-BUFFER-01 |
| DS-HIST-42 | Custom connector specification template | `KYM-IF-CONNECTOR-SPEC-TEMPLATE.md`; integration-test evidence stored in Vault | Custom | FS-IF-CUSTOM-01. | FS-IF-CUSTOM-01 | OQ-CONNECTOR-SPEC-01 |
| DS-HIST-43 | Connector inventory | `cv_connector_inventory` table: connector_id, source_system, protocol, owner, gxp_flag, last_tested_at | Custom | FS-IF-INV-01. | FS-IF-INV-01 | OQ-CONNECTOR-INV-01 |
| DS-HIST-44 | Connector health monitoring | Per-connector status / latency / queue depth / last-message age via PI Vision dashboard + Prometheus metrics; > 5 min staleness on GxP tag → PagerDuty | Custom | FS-IF-HEALTH-01. | FS-IF-HEALTH-01 | OQ-CONNECTOR-HEALTH-01 |

### 4.8 Batch + Event Capture per ISA-88

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-45 | EF template capture fields | (start_ts, end_ts, batch_id, equipment, recipe_version) | Default | FS-EF-01. | FS-EF-01 | OQ-EF-TEMPLATE-01 |
| DS-HIST-46 | EF recipe-version source | Auto-populated from PAS-X recipe-version registry; EF template versioned alongside | Custom | FS-EF-02. | FS-EF-02 | OQ-EF-RECIPE-01 |
| DS-HIST-47 | PI-MES interface | PAS-X EBR adapter emits start / end / pause / resume events to PI Event Frames; cross-reference deterministic via batch_id | Custom | FS-EF-03. | FS-EF-03 | OQ-PI-MES-IF-01 |
| DS-HIST-48 | EF immutability post-completion | Enforced via PI EF Security; correction workflow logs annotated edit + QA-approval reference | Custom | FS-EF-04. | FS-EF-04 | OQ-EF-IMMUTABLE-01 |
| DS-HIST-49 | Per-phase roll-up expressions | min / max / mean / integral via PI Asset Analytics expression bound to EF template; expression version captured | Custom | FS-EF-05. | FS-EF-05 | OQ-EF-ROLLUP-01 |
| DS-HIST-50 | EF nesting depth | Procedure → unit procedure → operation → phase (4 levels per ISA-88) | Default | FS-EF-06. | FS-EF-06 | OQ-EF-NESTING-01 |

### 4.9 Visualisation, Analytics, Export

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-51 | PI Vision element catalogue | trend, gauge, table, EF-aware display elements; version-controlled in `kymeta/pi-vision-displays` repo | Custom | FS-VIZ-01. | FS-VIZ-01 | OQ-VISION-ELEM-01 |
| DS-HIST-52 | Per-display ACLs | AD-group-based read / edit / publish via PI Vision security model | Default | FS-VIZ-02. | FS-VIZ-02 | OQ-VISION-ACL-01 |
| DS-HIST-53 | Deep-link template | `https://pi-vision.kymeta.local/PIVision/#/Displays/<id>?StartTime=<ef-start>&EndTime=<ef-end>` | Custom | FS-VIZ-03. | FS-VIZ-03 | OQ-VISION-DEEPLINK-01 |
| DS-HIST-54 | PI Analytics inventory | `cv_pi_analytics_inventory` table; GxP-critical entries flagged → Cat-5 sub-component validation pipeline | Custom | FS-ANL-01. | FS-ANL-01 | OQ-ANALYTICS-INV-01 |
| DS-HIST-55 | PI Integrator export sink | Databricks lakehouse via `pi-integrator-lakehouse.yaml`; schema versioned | Custom | FS-ANL-02. | FS-ANL-02 | OQ-INTEGRATOR-01 |
| DS-HIST-56 | Web API ad-hoc export endpoint | `GET /piwebapi/streams/{webId}/recorded?startTime=&endTime=`; GxP-flagged tag exports audit-logged with user / scope / ts | Custom | FS-EXP-01. | FS-EXP-01 | OQ-API-EXPORT-01 |
| DS-HIST-57 | Export-volume metering | Per-user rolling-hour byte / row counter; > 1 M rows / hour triggers security alert in Splunk | Custom | FS-EXP-02. | FS-EXP-02 | OQ-EXPORT-METER-01 |

### 4.10 Multi-Site Federation

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-58 | Federation direction | Read-only at core (Reykjavík); Akureyri write-back denied at security layer | Custom | FS-FED-01. | FS-FED-01 | OQ-FED-DIRECTION-01 |
| DS-HIST-59 | Site-of-origin attribute | Attached to every federated point; AF view at core merges via `Federated` namespace | Custom | FS-FED-02. | FS-FED-02 | OQ-FED-NAMESPACE-01 |
| DS-HIST-60 | Federation lag alert | > 5 min lag → PagerDuty alert | Custom | FS-FED-03. | FS-FED-03 | OQ-FED-LAG-01 |
| DS-HIST-61 | Cross-site EF stitching | `parent_batch_id` foreign key links upstream Reykjavík bulk → downstream Akureyri fill / finish | Custom | FS-FED-04. | FS-FED-04 | OQ-FED-STITCH-01 |

### 4.11 Real-Time Consumer APIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-62 | PI Web API endpoint set | `/streams/{webId}/value`, `/streams/{webId}/recorded`, `/eventframes/...`, `/streamsets/{webId}/value` | Default | FS-API-01. | FS-API-01 | OQ-API-ENDPOINTS-01 |
| DS-HIST-63 | PI Notification firing latency | ≤ 60 s end-to-end (rule-firing → MES / eQMS / paging) | Custom | FS-API-02. | FS-API-02 | OQ-NOTIFICATION-LATENCY-01 |
| DS-HIST-64 | API service-account credentials | HashiCorp Vault credential broker; scope-restricted PI security mapping | Custom | FS-API-03. | FS-API-03 | OQ-API-VAULT-01 |
| DS-HIST-65 | API rate limits | HA-Proxy per-token tokens / sec configurable; abusive → 429 + Splunk alert | Custom | FS-API-04. | FS-API-04 | OQ-API-RATELIMIT-01 |
| DS-HIST-66 | OPC UA Server Level-4 exposure | Curated tag subset for ERP / BI consumers per ISA-95 Level 3→4 | Custom | FS-API-05. | FS-API-05 | OQ-OPCUA-LEVEL4-01 |

### 4.12 Read-Only Discipline (DI)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-67 | Data-update permission removal | All role mappings except `BackfillException` denied UPDATE on time-series data | Custom | FS-DI-01. | FS-DI-01 | OQ-DI-READ-ONLY-01 |
| DS-HIST-68 | Source-timestamp preference | Source-system timestamps preferred when available; PI Server NTP-synced (skew ≤ 1 s monitored) | Default | FS-DI-02. | FS-DI-02 | OQ-NTP-SKEW-01 |
| DS-HIST-69 | Correction-as-new-annotation | Corrections recorded as new annotated values referencing the original — never overwriting | Custom | FS-DI-03. | FS-DI-03 | OQ-DI-IMMUTABLE-01 |
| DS-HIST-70 | Attribution via AD principal | All configuration changes attributed to AD-authenticated user via Kerberos ticket | Default | FS-DI-04. | FS-DI-04 | OQ-DI-ATTRIB-01 |
| DS-HIST-71 | ALCOA+ checklist | Verified by ALCOA+ readiness checklist runbook `KYM-RB-ALCOA-PLUS-001` | Custom | FS-DI-05. | FS-DI-05 | PQ-ALCOA-CHECKLIST-01 |
| DS-HIST-72 | Back-fill exception logging | (tag, time_window, reason, qa_approver, executor, original_value, corrected_value) | Custom | FS-DI-06. | FS-DI-06 | OQ-BACKFILL-LOG-01 |
| DS-HIST-73 | Time-zone storage | UTC at storage; per-user display TZ via PI Vision personalisation; stored data unchanged | Default | FS-DI-07. | FS-DI-07 | OQ-TZ-STORE-01 |

### 4.13 Audit Trail / 21 CFR Part 11

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-74 | Audit-event coverage | Point creation / modification, AF changes, EF template changes, security changes, back-fill, configuration deployments, federation events | Default | FS-AUD-01. | FS-AUD-01 | OQ-AUD-COVERAGE-01 |
| DS-HIST-75 | Audit append-only enforcement | Platform-level append-only; export to CSV + Splunk forward | Default | FS-AUD-02. | FS-AUD-02 | OQ-AUD-APPENDONLY-01 |
| DS-HIST-76 | Monthly audit-review | Manufacturing IT Lead signs monthly review; evidence in QA dossier | Default | FS-AUD-03. | FS-AUD-03 | OQ-AUD-REVIEW-01 |
| DS-HIST-77 | Audit retention | ≥ 25 y for GxP-relevant tags + audit trail via archival policy + Splunk frozen index on object-locked S3 | Default | FS-AUD-04. | FS-AUD-04 | OQ-RETENTION-25Y-01 |
| DS-HIST-78 | Audit correlation across components | Correlation-id header propagated by AD-bound service accounts | Custom | FS-AUD-05. | FS-AUD-05 | OQ-AUD-CORRELATION-01 |
| DS-HIST-79 | § 11.10(a)–(e) validation procedure | `KYM-SOP-CSV-001` + copy-generation API | Default | FS-PART11-10. | FS-PART11-10 | OQ-PART11-10 |
| DS-HIST-80 | § 11.30 open-system controls (where applicable) | If PI Web API exposed beyond manufacturing-IT VLAN: deployed behind WAF + mTLS + non-repudiation logging | Custom | FS-PART11-30. | FS-PART11-30 | OQ-PART11-30 |
| DS-HIST-81 | § 11.50 — eQMS-side signing model | PI configuration changes signed in the change-control system (eQMS), not in PI itself; CR + eQMS signature is the regulated artefact | Custom (corpus-pattern) | FS-PART11-50; PI does not natively gate user actions with e-signatures. | FS-PART11-50 | OQ-PART11-50 |
| DS-HIST-82 | § 11.100 user-id uniqueness | AD enforces; deactivated accounts cannot be reassigned | Default | FS-PART11-100. | FS-PART11-100 | OQ-PART11-100 |
| DS-HIST-83 | § 11.200 re-authentication | eQMS step-up re-auth (password + MFA) at every signing event for PI configuration changes | Custom | FS-PART11-200. | FS-PART11-200 | OQ-PART11-200 |

### 4.14 Security / Cybersecurity

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-84 | Account management | Domain accounts only; break-glass admin per emergency-access SOP | Default | FS-SEC-01. | FS-SEC-01 | OQ-SEC-BREAKGLASS-01 |
| DS-HIST-85 | Service-account secret rotation | HashiCorp Vault auto-rotation job; annual rotation | Custom | FS-SEC-02. | FS-SEC-02 | OQ-VAULT-ROTATE-01 |
| DS-HIST-86 | Inter-service TLS | TLS 1.3 with mTLS where supported across PI Server, AF, Vision, Web API | Custom | FS-SEC-03. | FS-SEC-03 | OQ-TLS-INTER-01 |
| DS-HIST-87 | IEC 62443 zone-and-conduit | PI Server in `Production Zone`; PI Vision in `DMZ Zone`; firewall rules enforce minimum-necessary traffic | Custom | FS-SEC-04. | FS-SEC-04 | OQ-IEC-62443-01 |
| DS-HIST-88 | Patching SOP | `KYM-SOP-PATCH-001` + emergency runbook `KYM-RB-EMERGENCY-PATCH-001` | Default (site) | FS-SEC-05. | FS-SEC-05 | OQ-PATCH-SOP-01 |
| DS-HIST-89 | Quarterly access review | Orphan / dormant accounts disabled; evidence in QA dossier | Default | FS-SEC-06. | FS-SEC-06 | OQ-ACCESS-REVIEW-01 |

### 4.15 Integrations

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-90 | Source-connector inventory binding | Each PI interface registered in connector inventory (DS-HIST-43) | Default | FS-INT-PLC-01. | FS-INT-PLC-01 | OQ-CONNECTOR-INV-01 |
| DS-HIST-91 | PAS-X consumer access | PAS-X reads via PI Web API for batch-record reconstruction; AD service account; read-only scope | Custom | FS-INT-MES-01. | FS-INT-MES-01 | OQ-INT-MES-01 |
| DS-HIST-92 | AD integration | AD-managed accounts; service accounts in Vault; annual rotation | Default | FS-INT-AD-01 + FS-XSYS-AD-01. | FS-INT-AD-01 | OQ-INT-AD-01 |
| DS-HIST-93 | LIMS EF-attribute consumer | LIMS REST consumer of EF attributes via `/eventframes/{webId}/values` per stability / EM workflows | Custom | FS-INT-LIMS-01. | FS-INT-LIMS-01 | OQ-INT-LIMS-01 |
| DS-HIST-94 | SPC platform subscription | PI Notification subscriptions consumed by JMP SPC platform per `CRN-URS-SPC-001` | Custom | FS-INT-SPC-01. | FS-INT-SPC-01 | OQ-INT-SPC-01 |
| DS-HIST-95 | Lakehouse export | PI Integrator views to Databricks via Kafka topic `pi-asset-events` | Custom | FS-INT-LAKE-01. | FS-INT-LAKE-01 | OQ-INT-LAKE-01 |

### 4.16 Performance / Backup

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-96 | Sustained-ingest target | ~25,000 points × configured rates without backpressure; DR replication lag ≤ 30 s | Custom | FS-PERF-01. | FS-PERF-01 | PQ-PERF-INGEST-01 |
| DS-HIST-97 | PI Vision dashboard P95 load | ≤ 5 s under nominal user load | Custom | FS-PERF-02. | FS-PERF-02 | PQ-PERF-VISION-01 |
| DS-HIST-98 | PI Web API query P95 | ≤ 2 s for 1-day single-tag queries | Custom | FS-PERF-03. | FS-PERF-03 | PQ-PERF-API-01 |
| DS-HIST-99 | DB backup mode | Nightly base-backup; collective replication for hot DR | Default | FS-BAK-01. | FS-BAK-01 | OQ-BAK-01 |
| DS-HIST-100 | Quarterly restore test | DBA + QA witness; results in `RUN-BAK-RESTORE-NNN` | Default | FS-BAK-02. | FS-BAK-02 | OQ-BAK-RESTORE-01 |
| DS-HIST-101 | Annual DR exercise | Full DR-failover per `KYM-RB-DR-EXERCISE-001` | Default | FS-BAK-03. | FS-BAK-03 | PQ-DR-EXERCISE-01 |

### 4.17 Training / Periodic Review

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-HIST-102 | LMS-recorded training | Required for production access; AD-group expiry tied to LMS course-completion | Default | FS-TRN-01. | FS-TRN-01 | OQ-LMS-GATE-01 |
| DS-HIST-103 | Role-specific curricula | `KYM-CURR-AF-Author-v1`, `KYM-CURR-Point-Author-v1`, `KYM-CURR-EF-Author-v1`, `KYM-CURR-Fed-Admin-v1` | Custom | FS-TRN-02. | FS-TRN-02 | OQ-LMS-CURRICULA-01 |
| DS-HIST-104 | Annual periodic-review runbook | Covers AF / point inventory, audit-trail review evidence, ingest-health metrics, training currency, federation health, archive tier-down status | Default | FS-PR-01. | FS-PR-01 | OQ-PR-RUNBOOK-01 |
| DS-HIST-105 | Semi-annual connector review | Stale connectors (> 30 d no message) reviewed for retirement | Default | FS-PR-02. | FS-PR-02 | OQ-PR-CONNECTOR-01 |

## 5. Workflow + Business-Rule Design

### 5.1 Point-creation workflow

```
[AD Group: Point-Configuration-Author]
   │
   ▼  Form submission with mandatory fields (DS-HIST-14)
[PI SMT custom workflow]
   │  Validates: source-system reference, UoM, scan-class, eng-units, range,
   │  alarm-limits, GxP-relevance, owner
   │
   ├─ GxP-relevance = true → route to Point-Config-Approver (DS-HIST-15)
   │                            │
   │                            ▼  re-auth signature
   │                          Approved → point created with CompDev=0
   │
   └─ GxP-relevance = false → self-approval allowed → point created with
                              swinging-door defaults (DS-HIST-12)
```

### 5.2 AF-change workflow for GxP-batch reconstruction

1. AF Author authors change in `kymeta/pi-af-templates` GitLab repo with signed commit.
2. MR (Merge Request) requires ≥ 1 architect + ≥ 1 QA reviewer approval.
3. On MR merge, ArgoCD applies to PI AF active server; collective replication propagates to DR.
4. Dual-approval signatures captured in eQMS CR per DS-HIST-21 (AF Author ≠ Approver — QA + Head of Ops co-approval).
5. Template-version stamped on element instantiation per DS-HIST-18.

### 5.3 Back-fill exception workflow

Per FS-DI-01 / DS-HIST-67 the historian is read-only; back-fill is treated as an exception:

1. Process Engineer raises back-fill request via PI SMT custom form with: tag, time-window, reason.
2. QA Approver signs approval via eQMS step-up MFA (DS-HIST-83).
3. Backfill-Exception Operator (AD group with time-bound permission) executes the back-fill.
4. `BackfillEvent` row written with (tag, time_window, reason, qa_approver_id, executor_id, original_value, corrected_value, approved_at) per DS-HIST-72.
5. Audit-trail event `BACKFILL_EXECUTED` emitted.

### 5.4 OPC UA handshake-rejection investigation

OPC UA security misconfig is a critical risk (DR-05 in § 11). The rejection pipeline:

1. PI Interface for OPC UA logs every rejected handshake to `pi_audit.OPCUA_REJECT` with (source IP, cert subject, rejection reason).
2. Nightly review job lists rejections; > 5 per day from a single source → security alert in Splunk.
3. OT-Security Architect reviews; if expected (cert rotation) — note in change log; if unexpected — investigate per OT incident-response SOP.

### 5.5 Federation lag handling

1. Federation lag monitor polls every 60 s; computes `federation_lag_seconds` per (Akureyri → Reykjavík) tag pair.
2. > 60 s nominal → INFO logged.
3. > 5 min → PagerDuty alert (DS-HIST-60); ops investigates inter-site VPN tunnel status.
4. Sustained lag > 30 min → escalation per `KYM-RB-FED-DEGRADED-001`.

## 6. Role-Permission Matrix Design

| Action / Role | Operations Eng. | Process Eng. | AF Author | AF Approver (QA + Head Ops) | Point-Config Author | Point-Config Approver | EF Author | Backfill-Exception Op. | System Admin | Federation Admin | Auditor |
|---|---|---|---|---|---|---|---|---|---|---|---|
| View trend data via PI Vision | R | R | R | R | R | R | R | R | R | R | R |
| Author / approve ad-hoc EF queries + Vision displays | — | C/U / S (publish) | — | — | — | — | — | — | — | — | — |
| Add / modify AF templates + elements | — | — | C/U | — | — | — | — | — | — | — | — |
| Approve AF change (GxP-batch reconstruction) | — | — | — | S (QA + Head Ops co-sign) | — | — | — | — | — | — | — |
| Add / modify PI points | — | — | — | — | C/U | — | — | — | — | — | — |
| Approve point compression / retention change (GxP) | — | — | — | — | — | S | — | — | — | — | — |
| Author / modify EF templates per ISA-88 | — | — | — | — | — | — | C/U | — | — | — | — |
| Execute back-fill (under captured reason + QA approval) | — | — | — | — | — | — | — | C/U | — | — | — |
| Patching, AD groups | — | — | — | — | — | — | — | — | C/U | — | — |
| Manage multi-site federation | — | — | — | — | — | — | — | — | — | C/U | — |
| Read-only across configuration + audit logs | R | R | R | R | R | R | R | R | R | R | R |

Legend: R = read, C = create, U = update, S = sign (re-authenticated electronic signature in eQMS), — = denied.

SoD denies per URS § 4:

- AF Author ≠ AF Approver (cross-role).
- Point-Configuration Author ≠ Point-Configuration Approver.
- EF Author ≠ AF Approver (cross-role).
- Federation Admin cannot author / approve site-specific tags.

## 7. Integration Design

| IF-ID | Counterparty | Endpoint | Protocol | Direction | AuthN | Message schema | Retry / DLQ | Audit emission | FS-IDs traced |
|---|---|---|---|---|---|---|---|---|---|
| IF-PLC-01 | PLC / SCADA / BMS / instruments | per-source endpoints (Siemens S7-1500 OPC UA, AVEVA System Platform OPC UA, legacy Modbus) | OPC UA `Sign+Encrypt` Basic256Sha256 / OPC HDA / Modbus TCP | inbound | site PKI client cert / vendor-specific | per-protocol | edge buffer 7 d; reconciliation on reconnect | `pi_audit.SOURCE_BIND` | FS-INT-PLC-01, FS-IF-OPCUA-01, FS-IF-OPCHDA-01, FS-IF-MODBUS-01 |
| IF-MES-01 | PAS-X v3.2 | `https://pi-webapi.kymeta.local/piwebapi/` + EF event feed `https://pi-events.kymeta.local/api/v1/events` | PI Web API REST + EF events | bidirectional | AD service account + mTLS | PI Web API standard + EF event JSON | exponential backoff; reconciliation job nightly | `pi_audit.MES_QUERY` | FS-INT-MES-01, FS-EF-03 |
| IF-AD-01 | AD | `ldaps://ad.kymeta.local:636` + `kerberos://ad.kymeta.local:88` | LDAPS + Kerberos | bidirectional | machine cert + Kerberos ticket | LDAP + Kerberos standard | local-cache 24 h offline | `pi_audit.AUTHN` → Splunk `gxp-authn` | FS-INT-AD-01, FS-XSYS-AD-01 |
| IF-NTP-01 | NTP infra | `ntp://ntp.kymeta.local:123` | NTP v4 | inbound | none (isolated VLAN) | NTP standard | hold-over via local clock 5 min if master lost; > 1 s skew flagged | clock-skew metric in Prometheus | FS-DI-02 |
| IF-LIMS-01 | LIMS | `https://pi-webapi.kymeta.local/piwebapi/eventframes/{webId}/values` | REST | outbound query | LIMS service account + mTLS | PI Web API EF response | exponential backoff | `pi_audit.LIMS_QUERY` | FS-INT-LIMS-01 |
| IF-SPC-01 | JMP SPC platform | PI Notification push subscription | PI Notification (push) | outbound | service-account JWT | Notification payload | exponential backoff | `pi_audit.SPC_NOTIFY` | FS-INT-SPC-01 |
| IF-LAKE-01 | Databricks lakehouse | Kafka topic `pi-asset-events` | Kafka (TLS + SASL/SCRAM) | outbound | SASL/SCRAM credentials in Vault | Avro schema (versioned) | Kafka native retry; DLQ at broker | `pi_audit.LAKE_EXPORT` | FS-INT-LAKE-01 |
| IF-FED-01 | Akureyri PI Server | PI-to-PI federation | PI-to-PI | inbound | site PKI client cert | PI native | local buffer at Akureyri; reconciliation on link restore | `pi_audit.FED_REPLICATE` | FS-FED-01 |
| IF-PKI-01 | Site PKI | site cert-manager | ACME-equivalent | bidirectional | machine cert | cert rotation ≤ 12 m | retry on interval; 30 d before-expiry alert | cert-rotation audit | FS-PLAT-06 |
| IF-VAULT-01 | HashiCorp Vault | `https://vault.kymeta.local/v1/kv/pi/*` | HTTPS AppRole | inbound | AppRole + machine cert | KV v2 | retry on rotation | vault-access audit | FS-SEC-02 |

### 7.1 OPC UA configuration profile

Per FS-IF-OPCUA-01 / DS-HIST-35..37:

- Security mode: `Sign+Encrypt` (no fallback to `Sign` or `None`).
- Security policy: `Basic256Sha256` minimum; `Aes256_Sha256_RsaPss` accepted if vendor supports.
- Application instance cert: site PKI-issued; 12-month validity; SAN includes both DNS and URI.
- Trust list: per source system, pinned to source's application instance cert; rotation under change control.
- Rejected handshakes: logged with subject + reason; reviewed nightly per § 5.4.

### 7.2 OPC HDA backfill reconciliation contract

After every backfill from a legacy source via OPC HDA:

1. Backfill job records (`source_id`, `time_range_start`, `time_range_end`, `expected_row_count`).
2. Post-backfill, reconciliation report compares `expected_row_count` vs `actual_inserted` vs `overlap_with_existing`.
3. Overlap inconsistencies (different values at same timestamp) raise `HDA_OVERLAP_INCONSISTENCY` for manual investigation.

### 7.3 PI Web API exposure decision tree

Per § 11.30 decision (DS-HIST-80): PI Web API exposed beyond manufacturing-IT VLAN is treated as an "open system":

- Default deployment: behind site-internal load balancer; not exposed to office network or internet.
- If a consumer requires office-network access (e.g., a non-OT analytics user): expose via reverse proxy at the DMZ Zone with WAF + mTLS + non-repudiation logging per DS-HIST-80.
- No anonymous access; no read-only-without-AD; no public endpoints.

## 8. Site-Deployed Components Design

### 8.1 Nightly orphan-point check job

- **Type:** Vendor PI SMT custom report — declarative only.
- **Purpose:** Lists PI Points not linked into AF; report goes to AF Author + Manufacturing IT Lead.
- **GAMP escalation:** Remains within Cat 4 — purely declarative report definition.
- **Verified by:** OQ-ORPHAN-CHECK-01.

### 8.2 Compression-loss report runner

- **Type:** PI SMT custom report — declarative.
- **GAMP escalation:** Cat 4 declarative.
- **Verified by:** OQ-COMP-LOSS-REPORT-01.

### 8.3 PI Asset Analytics GxP-critical expressions

- **Type:** Per FS-AF-03 / FS-ANL-01, any GxP-critical analytics expression with site-authored formula logic is a **Cat 5 sub-component**.
- **Inventory:** `cv_pi_analytics_inventory` table (DS-HIST-54); GxP-flagged entries listed below (illustrative — actual list managed under change control).
  - `KYM-PIANA-001` — Bioreactor BR-300A specific-productivity calculation per phase.
  - `KYM-PIANA-002` — WFI conductivity rolling-mean per CIP cycle.
  - `KYM-PIANA-003` — Pure-steam endotoxin trending per shift.
- **Mini-SDS per METHODOLOGY § 2B.4 rule 6 (Cat 5 sub-component process for each GxP-critical expression):**
  - Source code (expression text) version-controlled in `kymeta/pi-analytics-expressions` repo.
  - Per-expression URS / FS / DS / RA / OQ artefact set with the parent system's prefix + `-PIANA-NN`.
  - Unit-test fixture data + expected output regression-tested before activation.
  - Cat 5 sub-component change control: Author ≠ Approver, ≥ 1 statistician peer review where statistical math involved.
- **Verified by:** Per-expression OQ in addition to OQ-ANALYTICS-INV-01.

### 8.4 Site-authored connector specifications

- **Type:** Custom integration adapters (FS-IF-CUSTOM-01) — if any are deployed beyond vendor-supplied PI Interfaces.
- **GAMP escalation:** Per METHODOLOGY § 2B.4 rule 6, site-authored connectors with non-trivial logic escalate to Cat 5 hybrid. At v1.0 corpus ship, no site-authored connector exists; all sources use vendor PI Interfaces. Should a future custom connector be authored, the corresponding mini-SDS sub-section will be added per the rule.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200.
- 21 CFR Part 211 §§ .68, .192.
- FDA *Data Integrity and Compliance with cGMP* (2018).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EU GMP Annex 15.

### International — ICH
- ICH Q9(R1).

### Industry / Standards
- ISPE GAMP 5 (2nd Ed., 2022).
- ISPE GAMP Good Practice Guide *Records and Data Integrity*.
- PIC/S PI 041.
- ISA-95 / IEC 62264.
- ISA-88 / IEC 61512.
- OPC UA / IEC 62541.
- IEC 62443.
- ISO/IEC 27001:2022.

### Vendor
- AVEVA — *PI System 2024 Reference* (PI Server, PI AF, PI Vision, PI Integrator, PI Web API, PI Event Frames, PI Asset Analytics, PI Connector / Edge Data Store).
- AVEVA — *PI System Security Configuration Guide* v2024.1.
- AVEVA — *PI Asset Framework Template Reference* v2024.1.
- AVEVA — *PI Event Frames Best Practices* v2024.1.
- AVEVA — *PI Web API Reference* v2024.1.

### Site
- `KYM-SOP-CSV-001` — CSV procedure.
- `KYM-SOP-PATCH-001` — patching SOP.
- `KYM-RB-EMERGENCY-PATCH-001` — emergency-patch runbook.
- `KYM-RB-DR-EXERCISE-001` — DR exercise runbook.
- `KYM-RB-ALCOA-PLUS-001` — ALCOA+ readiness checklist runbook.
- `KYM-RB-FED-DEGRADED-001` — federation degradation runbook.

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-HIST-01 | FS-PLAT-01 |
| DS-HIST-02 | FS-PLAT-01 |
| DS-HIST-03 | FS-PLAT-01 |
| DS-HIST-04 | FS-PLAT-02 |
| DS-HIST-05 | FS-PLAT-02 / FS-IF-EDGE-01 |
| DS-HIST-06 | FS-PLAT-03 |
| DS-HIST-07 | FS-PLAT-04 |
| DS-HIST-08 | FS-PLAT-05 |
| DS-HIST-09 | FS-PLAT-06 |
| DS-HIST-10 | FS-TAG-01 |
| DS-HIST-11 | FS-TAG-02 |
| DS-HIST-12 | FS-TAG-02 |
| DS-HIST-13 | FS-TAG-03 |
| DS-HIST-14 | FS-TAG-04 |
| DS-HIST-15 | FS-TAG-05 |
| DS-HIST-16 | FS-ISA95-01 |
| DS-HIST-17 | FS-ISA95-02 |
| DS-HIST-18 | FS-ISA95-03 |
| DS-HIST-19 | FS-ISA95-04 |
| DS-HIST-20 | FS-AF-01 |
| DS-HIST-21 | FS-AF-02 |
| DS-HIST-22 | FS-AF-03 |
| DS-HIST-23 | FS-AF-04 |
| DS-HIST-24 | FS-COMP-01 |
| DS-HIST-25 | FS-COMP-02 |
| DS-HIST-26 | FS-COMP-02 |
| DS-HIST-27 | FS-COMP-03 |
| DS-HIST-28 | FS-COMP-04 |
| DS-HIST-29 | FS-ARCH-01 |
| DS-HIST-30 | FS-ARCH-01 |
| DS-HIST-31 | FS-ARCH-02 |
| DS-HIST-32 | FS-ARCH-02 |
| DS-HIST-33 | FS-ARCH-03 |
| DS-HIST-34 | FS-ARCH-04 |
| DS-HIST-35 | FS-IF-OPCUA-01 |
| DS-HIST-36 | FS-IF-OPCUA-01 |
| DS-HIST-37 | FS-IF-OPCUA-01 |
| DS-HIST-38 | FS-IF-OPCUA-02 |
| DS-HIST-39 | FS-IF-OPCHDA-01 |
| DS-HIST-40 | FS-IF-MODBUS-01 |
| DS-HIST-41 | FS-IF-EDGE-01 |
| DS-HIST-42 | FS-IF-CUSTOM-01 |
| DS-HIST-43 | FS-IF-INV-01 |
| DS-HIST-44 | FS-IF-HEALTH-01 |
| DS-HIST-45 | FS-EF-01 |
| DS-HIST-46 | FS-EF-02 |
| DS-HIST-47 | FS-EF-03 |
| DS-HIST-48 | FS-EF-04 |
| DS-HIST-49 | FS-EF-05 |
| DS-HIST-50 | FS-EF-06 |
| DS-HIST-51 | FS-VIZ-01 |
| DS-HIST-52 | FS-VIZ-02 |
| DS-HIST-53 | FS-VIZ-03 |
| DS-HIST-54 | FS-ANL-01 |
| DS-HIST-55 | FS-ANL-02 |
| DS-HIST-56 | FS-EXP-01 |
| DS-HIST-57 | FS-EXP-02 |
| DS-HIST-58 | FS-FED-01 |
| DS-HIST-59 | FS-FED-02 |
| DS-HIST-60 | FS-FED-03 |
| DS-HIST-61 | FS-FED-04 |
| DS-HIST-62 | FS-API-01 |
| DS-HIST-63 | FS-API-02 |
| DS-HIST-64 | FS-API-03 |
| DS-HIST-65 | FS-API-04 |
| DS-HIST-66 | FS-API-05 |
| DS-HIST-67 | FS-DI-01 |
| DS-HIST-68 | FS-DI-02 |
| DS-HIST-69 | FS-DI-03 |
| DS-HIST-70 | FS-DI-04 |
| DS-HIST-71 | FS-DI-05 |
| DS-HIST-72 | FS-DI-06 |
| DS-HIST-73 | FS-DI-07 |
| DS-HIST-74 | FS-AUD-01 |
| DS-HIST-75 | FS-AUD-02 |
| DS-HIST-76 | FS-AUD-03 |
| DS-HIST-77 | FS-AUD-04 |
| DS-HIST-78 | FS-AUD-05 |
| DS-HIST-79 | FS-PART11-10 |
| DS-HIST-80 | FS-PART11-30 |
| DS-HIST-81 | FS-PART11-50 |
| DS-HIST-82 | FS-PART11-100 |
| DS-HIST-83 | FS-PART11-200 |
| DS-HIST-84 | FS-SEC-01 |
| DS-HIST-85 | FS-SEC-02 |
| DS-HIST-86 | FS-SEC-03 |
| DS-HIST-87 | FS-SEC-04 |
| DS-HIST-88 | FS-SEC-05 |
| DS-HIST-89 | FS-SEC-06 |
| DS-HIST-90 | FS-INT-PLC-01 |
| DS-HIST-91 | FS-INT-MES-01 |
| DS-HIST-92 | FS-INT-AD-01 / FS-XSYS-AD-01 |
| DS-HIST-93 | FS-INT-LIMS-01 |
| DS-HIST-94 | FS-INT-SPC-01 |
| DS-HIST-95 | FS-INT-LAKE-01 |
| DS-HIST-96 | FS-PERF-01 |
| DS-HIST-97 | FS-PERF-02 |
| DS-HIST-98 | FS-PERF-03 |
| DS-HIST-99 | FS-BAK-01 |
| DS-HIST-100 | FS-BAK-02 |
| DS-HIST-101 | FS-BAK-03 |
| DS-HIST-102 | FS-TRN-01 |
| DS-HIST-103 | FS-TRN-02 |
| DS-HIST-104 | FS-PR-01 |
| DS-HIST-105 | FS-PR-02 |

**FS-IDs in parent FS NOT covered (with rationale):**

- FS-AV-01 (Availability ≥ 99.9% read / 99.95% write) — **vendor-internal — no site design surface**: governed by site Manufacturing-IT operational SLA, not by DS configuration.
- FS-PERF-04 (PI Asset Analytics expression evaluation P95 ≤ 30 s) — **vendor-internal except where Cat 5 sub-component applies**: site-authored expressions covered by per-expression mini-SDS in § 8.3.
- FS-XSYS-BAK-01 (Veeam backup integration) — covered at site enterprise-backup-service DS level per `AUR-URS-BACKUP-001`; site-level binding via DS-HIST-99..101.

## 11. Appendix B — Design-level Risk Register

| DR-ID | Design-stage risk | Origin design choice | Mitigation reference |
|---|---|---|---|
| DR-01 | GxP-tag `CompDev=0` policy could explode archive volume if accidentally applied to non-GxP tags | DS-HIST-11 + DS-HIST-12 | GxP-relevance gate at point-creation (DS-HIST-14); compression-loss report (DS-HIST-28) monitors archive size growth |
| DR-02 | Federation lag > 5 min could yield stale batch reconstruction at Reykjavík core | DS-HIST-60 alerting | PagerDuty alert; `KYM-RB-FED-DEGRADED-001` runbook |
| DR-03 | EF template version mismatch with recipe-version could produce wrong roll-ups | DS-HIST-46 + DS-HIST-49 | OQ-EF-RECIPE-01 + OQ-EF-ROLLUP-01 |
| DR-04 | Archive tier-down latency penalty could exceed 5 s for very-cold-stored queries during reconstruction | DS-HIST-31 + DS-HIST-32 | PQ-PERF-ARCH-01 with worst-case query mix |
| DR-05 | OPC UA security misconfig (operator selects `None` or `Basic128`) could expose data plane to tampering | DS-HIST-35 + DS-HIST-36 enforce minimum | OQ-OPCUA-SEC-01 with negative tests; nightly rejected-handshake review (§ 5.4) |
| DR-06 | Orphan PI Points (not in AF) could escape GxP retention | DS-HIST-17 nightly check | Periodic-review item; remediation workflow |
| DR-07 | PI Web API exposed beyond manufacturing-IT VLAN without § 11.30 controls could create open-system violation | DS-HIST-80 decision tree | DS-HIST-80 + WAF + mTLS + non-repudiation logging for any exposure |
| DR-08 | GxP-critical analytics expression deployed without Cat 5 sub-component validation | DS-HIST-54 inventory flag | `cv_pi_analytics_inventory` gating + per-expression mini-SDS (§ 8.3) |
| DR-09 | Edge buffer 7 d exhausted during prolonged inter-site link outage in Iceland weather events | DS-HIST-41 | Operational SOP escalation at 5 d; alternative satellite uplink as backup |
| DR-10 | Compression-change on GxP tag affecting downstream MES batch records | DS-HIST-27 impact-assessment | Change-control system gates compression changes; downstream regression tests |
| DR-11 | NTP skew > 1 s on PI Server could violate contemporaneous-records ALCOA principle | DS-HIST-68 skew monitor | Alert fires per FS-DI-02; falls back to local clock with logged degradation |
| DR-12 | Back-fill exception workflow could be over-used as routine correction path | DS-HIST-67 read-only + DS-HIST-72 exception logging | Monthly review identifies back-fill volume per executor; trending |
| DR-13 | Connector inventory drift (added connectors not recorded) | DS-HIST-43 + DS-HIST-44 health metrics | Semi-annual connector review (DS-HIST-105); discrepancy investigation |
| DR-14 | EF nesting cycle (ISA-88 violation: phase → procedure parenting) | DS-HIST-50 | Schema constraint prevents cycle; OQ-EF-NESTING-01 |
| DR-15 | Federation read-only direction violated if Akureyri admin enables write-back at security layer | DS-HIST-58 | Periodic security-layer audit; configuration-drift detection job |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
