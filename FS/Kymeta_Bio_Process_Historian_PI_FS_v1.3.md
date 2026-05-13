---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-26; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "KYM-URS-HIST-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd Ed., 2022) Cat 3 conventions for non-configured products"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11; PIC/S PI 041"
  - "ISA-95 / IEC 62264; ISA-88 / IEC 61512; OPC UA / IEC 62541; IEC 62443; ISO/IEC 27001:2022"
parent_urs:
  document_number: KYM-URS-HIST-001
  version: 1.2
  file: ../../URS/_generated/final/Process_Historian__Kymeta_Bio_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Process Historian — AVEVA PI System 2024

**Document Number:** KYM-FS-HIST-001
**Version:** 1.2
**Effective Date:** 2026-05-12 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Parent URS:** KYM-URS-HIST-001 v1.2
**Site:** Kymeta Bio ehf, Manufacturing IT Operations, Reykjavík, Iceland *(fictional)*
**System Owner:** Manufacturing IT Lead
**System Class (GAMP 5, 2nd ed.):** Category 3 — Non-Configured Product (standard configuration only)
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; PIC/S PI 041; ISA-95; ISA-88; OPC UA; IEC 62443; ISO/IEC 27001:2022

> **FS scope note (Cat 3).** Because this is a Cat 3 system, the FS proportionately addresses standard configuration (points, AF templates, Event-Frame templates, Vision displays, Integrator views, security mappings) rather than custom logic. Any non-trivial custom code (PI ACE / Asset Analytics expression with GxP-critical effect) is explicitly prohibited under change control without a separate Cat-5 sub-component RA + FS.

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Manufacturing IT Lead) | _____________ | _____________ | _____ |
| Reviewer (Automation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Process Engineer) | _____________ | _____________ | _____ |
| Approver (Head of Operations) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue, derived from KYM-URS-HIST-001 v1.0. |
| 1.2 | 2026-05-12 | (synthetic) | v1.2: aligned with parent URS v1.2 (T3); per-URS-ID expansion across § 4 + § 8 per METHODOLOGY § 2A.7. Added explicit modules: ISA-95 mapping, compression + retention, archive tier-down, interface devices (OPC-UA + edge + custom), batch + Event-Frame capture per ISA-88, visualisation + analytics + export, multi-site federation, real-time consumer APIs (Web API + Notification), data-integrity ALCOA+, cybersecurity per IEC 62443. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## Definitions

Inherited from KYM-URS-HIST-001. Additional FS-specific terms:

| Term | Definition |
|---|---|
| FS | Functional Specification (this document) |
| Collective | PI Server replication topology (active + DR) |
| AF Template | PI Asset Framework template — versioned class definition |
| PI Vision | Web visualisation client |
| Web API | PI Web API (REST) |
| Event Frame | PI Event Frame — time-bounded interval marker for ISA-88 batch / phase |
| Integrator | PI Integrator for Business Analytics |

---

## 1. Purpose

This FS specifies, at the system-design level, how AVEVA PI System 2024 is deployed and configured to satisfy `KYM-URS-HIST-001` v1.2. It is the controlling input to `KYM-CS-HIST-001`, `KYM-RA-HIST-001`, IQ / OQ / PQ Protocols, and `KYM-RTM-HIST-001`.

## 2. Scope

Per KYM-URS-HIST-001 §2: PI Server cluster (active + DR collective replication), PI AF, PI Event Frames, PI Vision web servers, PI Integrator, PI Web API + Notifications, PI interfaces / connectors to PLC / SCADA / BMS / instrument sources (~25,000 PI points), AD authentication, daily backup, NTP sync, archive tier-down to slower storage after configurable age, multi-site federation Reykjavík ↔ Akureyri. Out: source systems (per-system URSs), analytics consumers (separate URS).

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source / Vendor | Notes |
|---|---|---|---|---|---|
| C-01 | PI Server (active) | COTS | 3 | AVEVA | primary node |
| C-02 | PI Server (DR) | COTS | 3 | AVEVA | collective replication |
| C-03 | PI Asset Framework | COTS | 3 | AVEVA | hierarchy + templates |
| C-04 | PI Event Frames | COTS | 3 | AVEVA | ISA-88 batch / phase capture |
| C-05 | PI Vision web servers | COTS | 3 | AVEVA | read-only viz, load-balanced |
| C-06 | PI Web API | COTS | 3 | AVEVA | REST endpoint, HA |
| C-07 | PI Integrator for Business Analytics | COTS | 3 | AVEVA | asset-aware export |
| C-08 | PI Notification | COTS | 3 | AVEVA | rule-based alerts |
| C-09 | PI Asset Analytics | COTS | 3 (5 for GxP-critical) | AVEVA | derived attributes |
| C-10 | PI Interfaces / Connectors | COTS | 3 | AVEVA | OPC UA / OPC HDA / Modbus / custom |
| C-11 | PI Edge Data Store | COTS | 3 | AVEVA | local-buffer at edge |
| C-12 | AD / Kerberos | COTS infra | (infra) | Microsoft | AuthN |
| C-13 | NTP infra | COTS infra | (infra) | (site) | time sync |
| C-14 | HashiCorp Vault | COTS infra | (infra) | HashiCorp | service-account secrets |
| C-15 | Site PKI (X.509) | COTS infra | (infra) | (site) | auto-rotation |
| C-16 | PAS-X v3.2 (consumer) | COTS MES | 4 | Werum / Körber | consumes via Web API + EF |
| C-17 | JMP / SPC consumer | COTS | 3 | SAS Institute | consumes Notifications (CRN-URS-SPC-001) |
| C-18 | Databricks lakehouse | (infra) | 4 | (site) | Integrator export target |
| C-19 | Akureyri PI Server (federated) | COTS | 3 | AVEVA | downstream-fill site |

### 3.2 Logical Architecture (textual)

```
                ┌──────────────────────────────────────────────┐
                │   AD / Kerberos     │     NTP infra            │
                └──────────────┬───────────────────┬─────────────┘
                               │                   │
   ┌───────────────────────────▼───────────────────▼──────────────┐
   │                    AVEVA PI System 2024                       │
   │   ┌────────────────────┐  ┌────────────────────────────┐     │
   │   │ PI Server (active) │  │ PI Server (DR — collective)│     │
   │   └────────────────────┘  └────────────────────────────┘     │
   │   ┌────────────────────┐  ┌────────────────────────────┐     │
   │   │ PI Asset Framework │  │ PI Event Frames            │     │
   │   └────────────────────┘  └────────────────────────────┘     │
   │   ┌────────────────────┐  ┌────────────────────────────┐     │
   │   │ PI Vision (LB)     │  │ PI Web API (HA)            │     │
   │   └────────────────────┘  └────────────────────────────┘     │
   │   ┌────────────────────┐  ┌────────────────────────────┐     │
   │   │ PI Integrator      │  │ PI Notification + Analytics│     │
   │   └────────────────────┘  └────────────────────────────┘     │
   │   ┌─────────────────────────────────────────────────────┐    │
   │   │ PI Interfaces (OPC UA / OPC HDA / Modbus / custom)  │    │
   │   │ PI Edge Data Store (local-buffer)                   │    │
   │   └────────────────────┬────────────────────────────────┘    │
   └────────────────────────┼─────────────────────────────────────┘
                            │
              ┌─────────────┼─────────────┐
              ▼             ▼             ▼
         PLC / SCADA      BMS         Instruments
         (separate URSs each)

   ─── Federation ───►   Akureyri PI Server (read-only at core)
```

### 3.3 Functional Modules

| Module | URS sections |
|---|---|
| M-PLAT | URS-PLAT-* |
| M-TAG | URS-TAG-*, URS-ISA95-*, URS-AF-* |
| M-COMP | URS-COMP-*, URS-ARCH-* |
| M-IF | URS-IF-* |
| M-EF | URS-EF-* |
| M-VIZ | URS-VIZ-*, URS-ANL-*, URS-EXP-* |
| M-FED | URS-FED-* |
| M-API | URS-API-* |
| M-DI | URS-DI-* |
| M-AUD | URS-AUD-*, URS-PART11-* |
| M-SEC | URS-SEC-* |
| M-INT | URS-INT-* |
| M-PERF | URS-PERF-*, URS-AV-*, URS-BAK-* |
| M-TRN | URS-TRN-* |
| M-PR | URS-PR-* |

---

## 4. Functional Specifications

### 4.1 Architecture / Hardware / Platform (M-PLAT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | PI Collective with active + DR member; replication lag monitored via PI Collective Manager; RPO ≤ 5 min validated by `OQ-COLLECTIVE-FAILOVER-01`; RTO ≤ 4 h validated by `PQ-DR-FAILOVER-01`. |
| FS-PLAT-02 | URS-PLAT-02 | All servers and interface nodes on UPS / generator-backed power; PI Edge Data Store + PI interfaces buffer locally on network outage (≥ 7 days) and reconcile on reconnect; verified by `OQ-INTERFACE-BUFFER-01`. |
| FS-PLAT-03 | URS-PLAT-03 | Manufacturing IT VLAN; no office-network route; verified by network-config audit. |
| FS-PLAT-04 | URS-PLAT-04 | PI Vision web tier behind HA-Proxy active/active; TLS 1.3 termination; backend health checks per 10 s. |
| FS-PLAT-05 | URS-PLAT-05 | PI Web API + Integrator deployed on 2-node Windows Server failover cluster; auto-failover ≤ 60 s. |
| FS-PLAT-06 | URS-PLAT-06 | All TLS certificates issued from site PKI; auto-rotation via cert-manager; ≤ 12-month validity. |

### 4.2 Tag Naming + Point Configuration (M-TAG)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TAG-01 | URS-TAG-01 | PI points adhere to the site naming convention (`PLANT.AREA.UNIT.TAGTYPE.NAME`). |
| FS-TAG-02 | URS-TAG-02 | Per-point compression / archival settings configured per the GxP-fidelity matrix; for critical CIP / SIP tags `Compress = OFF`, archive every value; verified by `OQ-COMPRESSION-FIDELITY-01`. |
| FS-TAG-03 | URS-TAG-03 | `GxP-relevance` extended-attribute flag captured per point. |
| FS-TAG-04 | URS-TAG-04 | Point-creation workflow form (PI System Management Tools custom workflow + JIRA gate): mandatory fields enforced. |
| FS-TAG-05 | URS-TAG-05 | GxP-flagged-tag compression-change route through Point-Config-Approver workflow; non-GxP self-approval allowed. |

### 4.3 ISA-95 Mapping

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ISA95-01 | URS-ISA95-01 | AF hierarchy mirrors ISA-95: `Enterprise → Site → Area → Production Line → Process Cell → Unit → Equipment Module → Control Module`. |
| FS-ISA95-02 | URS-ISA95-02 | Nightly orphan-check job lists PI Points not linked into AF; report goes to AF Author + Manufacturing IT Lead. |
| FS-ISA95-03 | URS-ISA95-03 | AF templates version-tracked in `cv_af_template_versions`; element instantiation stamps `template_version_id`. |
| FS-ISA95-04 | URS-ISA95-04 | OPC UA Server interface exposes ISA-95 companion-spec views for Level-4 consumers. |

### 4.4 Asset Framework (AF)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AF-01 | URS-AF-01 | AF templates stored in site config-repo; version-controlled. |
| FS-AF-02 | URS-AF-02 | AF changes affecting GxP-batch reconstruction require role-restricted dual approval (AF Author ≠ Approver — QA + Head of Ops). Verified by `OQ-AF-CHANGE-DUAL-APPROVE-01`. |
| FS-AF-03 | URS-AF-03 | AF reference-attribute formulas with GxP impact classified per `cv_af_formula_classification`; GxP-critical formulas route through Cat-5 sub-component process. |
| FS-AF-04 | URS-AF-04 | AF template attributes expose UoM via OPC UA UA-100 codes. |

### 4.5 Compression and Retention Policy (M-COMP)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-COMP-01 | URS-COMP-01 | Swinging-door compression with per-point `CompDev`, `CompMin`, `CompMax`; `CompDev=0` enforced for GxP-critical tags via PI extended-attribute gate. |
| FS-COMP-02 | URS-COMP-02 | Retention ≥ 25 y for GxP-relevant tags via archival policy `pi-archive-25y`; non-GxP retention ≥ 5 y. |
| FS-COMP-03 | URS-COMP-03 | Compression-change workflow triggers downstream impact assessment via the change-control system. |
| FS-COMP-04 | URS-COMP-04 | Compression-loss report runnable via PI System Management Tools custom report. |

### 4.6 Archive Tier-Down (M-COMP / ARCH)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ARCH-01 | URS-ARCH-01 | PI Data Archive primary tier on NVMe SAN; cold tier on SAS RAID-6; storage-class indicated per archive shift. |
| FS-ARCH-02 | URS-ARCH-02 | Tier-down job at 90 d default; query latency P95 ≤ 5 s validated per `PQ-PERF-ARCH-01`. |
| FS-ARCH-03 | URS-ARCH-03 | Archive-shift checksum validation runs on every shift; failure raises P1 PagerDuty incident. |
| FS-ARCH-04 | URS-ARCH-04 | Export to AWS S3 with object-lock; SHA-256 manifest captured + verified. |

### 4.7 Interface Devices (M-IF)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-IF-OPCUA-01 | URS-IF-OPCUA-01 | PI Interface for OPC UA configured: security mode `Sign+Encrypt`, security policy `Basic256Sha256` (minimum); certificate trust list per PKI; rejected handshakes logged. |
| FS-IF-OPCUA-02 | URS-IF-OPCUA-02 | MonitoredItem subscription model; sampling + publishing intervals configured per tag class in `pi-opcua-config.yaml`. |
| FS-IF-OPCHDA-01 | URS-IF-OPCHDA-01 | OPC HDA backfill jobs use `ReadAtTime` + `ReadProcessed`; overlap reconciliation report runs after every backfill. |
| FS-IF-MODBUS-01 | URS-IF-MODBUS-01 | PI Interface for Modbus TCP for legacy PLCs; per-tag register-mapping documented. |
| FS-IF-EDGE-01 | URS-IF-EDGE-01 | PI Edge Data Store deployed at edge nodes; 7-day local buffer; reconciliation queue exposed via Prometheus. |
| FS-IF-CUSTOM-01 | URS-IF-CUSTOM-01 | Custom interfaces documented per `KYM-IF-CONNECTOR-SPEC-TEMPLATE.md`; integration-test evidence stored in Vault. |
| FS-IF-INV-01 | URS-IF-INV-01 | Connector inventory in `cv_connector_inventory` table: connector_id, source system, protocol, owner, GxP flag, last-tested date. |
| FS-IF-HEALTH-01 | URS-IF-HEALTH-01 | Per-connector status, latency, queue depth, last-message age exposed via PI Vision dashboard + Prometheus metrics; staleness > 5 min on GxP tag → PagerDuty. |

### 4.8 Batch + Event Capture per ISA-88 (M-EF)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-EF-01 | URS-EF-01 | Event Frame templates capture (start_ts, end_ts, batch_id, equipment, recipe_version); auto-generated from MES batch-execution events. |
| FS-EF-02 | URS-EF-02 | Recipe-version field auto-populated from PAS-X recipe-version registry; EF template versioned alongside. |
| FS-EF-03 | URS-EF-03 | PI-MES interface (PAS-X EBR adapter) emits start / end / pause / resume events to PI Event Frames; cross-reference deterministic via batch_id. |
| FS-EF-04 | URS-EF-04 | EF immutability enforced via PI EF Security; correction workflow logs annotated edit + QA-approval reference. |
| FS-EF-05 | URS-EF-05 | Per-phase roll-ups (min/max/mean/integral) computed by PI Asset Analytics expression bound to EF template; expression version captured. |
| FS-EF-06 | URS-EF-06 | EF nesting (procedure → unit procedure → operation → phase) configured per ISA-88; visible in PI Event Frame Manager. |

### 4.9 Visualisation, Analytics, Export (M-VIZ)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VIZ-01 | URS-VIZ-01 | PI Vision elements (trend, gauge, table, EF-aware); displays in version-controlled folder; published displays signed off by Process Engineer. |
| FS-VIZ-02 | URS-VIZ-02 | Per-display ACLs via AD groups; PI Vision security model enforces read / edit / publish. |
| FS-VIZ-03 | URS-VIZ-03 | URL deep-link template `https://pi-vision.kymeta.local/PIVision/#/Displays/<id>?StartTime=<ef-start>&EndTime=<ef-end>`. |
| FS-ANL-01 | URS-ANL-01 | PI Asset Analytics expressions registered in `cv_pi_analytics_inventory`; GxP-critical entries flagged → Cat-5 sub-component validation. |
| FS-ANL-02 | URS-ANL-02 | PI Integrator views push asset-aware structured exports to Databricks lakehouse via `pi-integrator-lakehouse.yaml`; schema versioned. |
| FS-EXP-01 | URS-EXP-01 | PI Web API REST `GET /piwebapi/streams/{webId}/recorded?startTime=&endTime=` for ad-hoc export; GxP-flagged tag exports audit-logged with user / scope / ts. |
| FS-EXP-02 | URS-EXP-02 | Export meter: per-user rolling-hour byte / row counter; > 1 M rows / hour triggers security alert in Splunk. |

### 4.10 Multi-Site Federation (M-FED)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-FED-01 | URS-FED-01 | Reykjavík ↔ Akureyri federation via PI-to-PI interface (read-only at core); Akureyri write-back denied at security layer. |
| FS-FED-02 | URS-FED-02 | Site-of-origin attribute attached to every federated point; AF view at core merges via `Federated` namespace. |
| FS-FED-03 | URS-FED-03 | Federation replication-lag monitor; > 5 min alert via PagerDuty. |
| FS-FED-04 | URS-FED-04 | Cross-site EF stitching via `parent_batch_id` foreign key; product genealogy view in PI Vision EF-aware display. |

### 4.11 Real-Time Consumer APIs (M-API)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-API-01 | URS-API-01 | PI Web API endpoints exposed: `/streams/{webId}/value`, `/streams/{webId}/recorded`, `/eventframes/...`, `/streamsets/{webId}/value` (snapshot subscription). |
| FS-API-02 | URS-API-02 | PI Notification configured to fire on (rule-firing, deviation, alarm) ≤ 60 s; delivery to MES, eQMS, on-call paging. |
| FS-API-03 | URS-API-03 | AD-bound service accounts; HashiCorp Vault credential broker; scope-restricted PI security mapping. |
| FS-API-04 | URS-API-04 | Rate limits via HA-Proxy: per-token tokens / sec configurable; abusive 429 + Splunk alert. |
| FS-API-05 | URS-API-05 | OPC UA Server interface exposes a curated tag subset for Level-4 ERP / BI consumers per ISA-95 Level 3→4. |

### 4.12 Read-Only Discipline (M-DI)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | Data-update permissions removed from all role mappings except `BackfillException`; back-fill operations require QA approval + captured reason; back-fill events flagged in audit trail. |
| FS-DI-02 | URS-DI-02 | Source-system timestamps preferred when available; PI Server clock NTP-synced (skew ≤ 1 s monitored). |
| FS-DI-03 | URS-DI-03 | Original raw values retained per the configured retention; corrections are recorded as new annotated values referencing the original — never overwriting. |
| FS-DI-04 | URS-DI-04 | Configuration changes attributed to a named user via AD authentication. |
| FS-DI-05 | URS-DI-05 | Records Legible / Contemporaneous / Original / Accurate / Complete / Consistent / Enduring / Available — verified by ALCOA+ readiness checklist. |
| FS-DI-06 | URS-DI-06 | Back-fill log records (tag, time_window, reason, qa_approver, executor, original_value, corrected_value). |
| FS-DI-07 | URS-DI-07 | Storage in UTC; per-user display TZ via PI Vision personalisation; stored data unchanged. |

### 4.13 Audit Trail / 21 CFR Part 11 (M-AUD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit trail captures point creation / modification, AF changes, EF template changes, security changes, back-fill, configuration deployments, federation events. |
| FS-AUD-02 | URS-AUD-02 | Append-only at the platform level; export to CSV + Splunk forward; verified by `OQ-AUD-APPENDONLY-01`. |
| FS-AUD-03 | URS-AUD-03 | Manufacturing IT Lead reviews audit trail monthly; review evidence filed in QA dossier. |
| FS-AUD-04 | URS-AUD-04 | Retention ≥ 25 years for GxP-relevant tags + audit trail via archival policy + Splunk frozen index on object-locked S3. |
| FS-AUD-05 | URS-AUD-05 | Correlation across PI + AF + Vision via correlation-id header propagated by AD-bound service accounts. |
| FS-PART11-10 | URS-PART11-10 | Validation procedure (`KYM-SOP-CSV-001`) + copy-generation API per § 11.10(a)–(e). |
| FS-PART11-30 | URS-PART11-30 | If PI Web API exposed beyond manufacturing-IT VLAN, deployed behind WAF + mTLS + non-repudiation logging per § 11.30. |
| FS-PART11-50 | URS-PART11-50 | Configuration changes signed in the change-control system (eQMS) rather than in PI itself; PI does not natively gate user actions with e-signatures. The CR record + eQMS signature is the regulated artefact. |
| FS-PART11-100 | URS-PART11-100 | AD enforces user-id uniqueness; deactivated accounts cannot be reassigned. |
| FS-PART11-200 | URS-PART11-200 | eQMS step-up re-auth (password + MFA) at every signing event for PI configuration changes. |

### 4.14 Security / Cybersecurity (M-SEC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SEC-01 | URS-SEC-01 | Domain accounts only; break-glass admin per emergency-access SOP. |
| FS-SEC-02 | URS-SEC-02 | Service-account secrets in HashiCorp Vault; rotated annually via auto-rotation job. |
| FS-SEC-03 | URS-SEC-03 | TLS 1.3 with mTLS where supported across PI Server, AF, Vision, Web API. |
| FS-SEC-04 | URS-SEC-04 | IEC 62443 zone-and-conduit: PI Server in `Production Zone`; PI Vision in `DMZ Zone`; firewall rules enforce minimum-necessary traffic. |
| FS-SEC-05 | URS-SEC-05 | Patching SOP `KYM-SOP-PATCH-001`; emergency-patch runbook `KYM-RB-EMERGENCY-PATCH-001`. |
| FS-SEC-06 | URS-SEC-06 | Quarterly access review; orphan / dormant accounts disabled. |

### 4.15 Integrations (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-PLC-01 | URS-INT-PLC-01 | Each PI interface registered in the connector inventory (FS-IF-INV-01). |
| FS-INT-MES-01 | URS-INT-MES-01 | PAS-X reads historian via PI Web API for batch-record reconstruction; auth via AD service account; access scoped to read-only. |
| FS-INT-AD-01 | URS-INT-AD-01 | AD-managed accounts; service accounts via credential vault; rotated annually. |
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | LIMS REST consumer of EF attributes via `/eventframes/{webId}/values` per stability / EM workflows. |
| FS-INT-SPC-01 | URS-INT-SPC-01 | PI Notification subscriptions consumed by SPC platform (CRN-URS-SPC-001) for real-time SPC. |
| FS-INT-LAKE-01 | URS-INT-LAKE-01 | PI Integrator views push to Databricks lakehouse via Kafka topic `pi-asset-events`. |

### 4.16 Performance / Availability / Backup (M-PERF)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | Sustained ingest at ~25,000 points × configured rates without backpressure; DR collective replication lag ≤ 30 s; verified by `PQ-PERF-INGEST-01`. |
| FS-PERF-02 | URS-PERF-02 | PI Vision dashboard P95 load time ≤ 5 s under nominal user load. |
| FS-PERF-03 | URS-PERF-03 | PI Web API single-tag 1-day query P95 ≤ 2 s. |
| FS-PERF-04 | URS-PERF-04 | PI Asset Analytics expression evaluation P95 ≤ 30 s for nominal expressions. |
| FS-AV-01 | URS-AV-01 | Read availability ≥ 99.9 %; write (interface) availability ≥ 99.95 %; uptime probes monitored 24×7. |
| FS-BAK-01 | URS-BAK-01 | Database backed up nightly; collective replication for hot DR. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore-test runbook with QA witness; results filed in `RUN-BAK-RESTORE-NNN`. |
| FS-BAK-03 | URS-BAK-03 | Annual full DR-failover exercise per `KYM-RB-DR-EXERCISE-001`. |

### 4.17 Training / Periodic Review

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | LMS-recorded role-specific training required for production access. |
| FS-TRN-02 | URS-TRN-02 | Role-specific Cornerstone curricula `KYM-CURR-AF-Author-v1`, `KYM-CURR-Point-Author-v1`, `KYM-CURR-EF-Author-v1`, `KYM-CURR-Fed-Admin-v1`. |
| FS-PR-01 | URS-PR-01 | Annual periodic-review run-book covering AF / point inventory, audit-trail review evidence, ingest-health metrics, training currency, federation health, archive tier-down status; signed by Manufacturing IT Lead + Head of QA. |
| FS-PR-02 | URS-PR-02 | Semi-annual connector inventory review; stale connectors (> 30 d) reviewed for retirement. |

---


### 4.18 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem with local OT cached credentials for offline operation. Conditional-access binding to policy `OT-Historian Conditional Access (MFA at engineering workstation; collector services use named-location + service-account bind)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the PI metadata DB plus PI-native archive-shipping for time-series archives; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Interface Specifications

| IF ID | URS ID | Counterparty | Protocol | Direction | Notes |
|---|---|---|---|---|---|
| IF-PLC-01 | URS-INT-PLC-01 / URS-IF-* | PLC / SCADA / BMS / instruments | OPC UA / HDA / Modbus / custom | inbound | per-source connector |
| IF-MES-01 | URS-INT-MES-01 | PAS-X v3.2 | PI Web API (REST) + EF events | bidirectional | read-only data; EF event-feed inbound |
| IF-AD-01 | URS-INT-AD-01 | AD | LDAPS / Kerberos | bidirectional | AuthN |
| IF-NTP-01 | URS-DI-02 | NTP infra | NTP | inbound | time sync |
| IF-LIMS-01 | URS-INT-LIMS-01 | LIMS | PI Web API (REST) | outbound | EF attributes |
| IF-SPC-01 | URS-INT-SPC-01 | JMP SPC platform | PI Notification (push) | outbound | real-time alerts |
| IF-LAKE-01 | URS-INT-LAKE-01 | Databricks lakehouse | PI Integrator / Kafka | outbound | structured exports |
| IF-FED-01 | URS-FED-01 | Akureyri PI Server | PI-to-PI | inbound | federation |
| IF-PKI-01 | URS-PLAT-06 | site PKI | ACME / cert-manager | inbound | cert auto-rotation |
| IF-VAULT-01 | URS-SEC-02 | HashiCorp Vault | AppRole / KV | inbound | service-account secrets |

## 6. Data Model (high-level)

| Entity | Attributes (illustrative) |
|---|---|
| PI Point | tag_name, source_id, scan_class, compression (CompDev/Min/Max), archival_policy, gxp_relevance, owner, uom, range, alarm_limits |
| AF Element | element_path, template_id, template_version, attributes[] |
| AF Template | template_id, version, approver_id, approved_at, gxp_class |
| EF Template | template_id, version, recipe_version, phase_hierarchy, rollup_expressions |
| Event Frame | ef_id, template_id, start_ts, end_ts, batch_id, equipment_path, recipe_version, immutability_state |
| ConnectorInventory | connector_id, source_system, protocol, owner, last_tested_at, gxp_relevance, health_status |
| AuditEvent | event_id, user_id, action, entity, old, new, timestamp, correlation_id |
| BackfillEvent | event_id, tag_name, time_window, reason, qa_approver_id, executor_id, original_value, corrected_value, approved_at |
| FederationLag | site_pair, lag_seconds, ts |

## 7. Non-Functional Specifications

| NFR ID | Specification |
|---|---|
| NFR-01 | Sustained ingest ≥ site nominal rate without backpressure |
| NFR-02 | DR replication lag ≤ 30 s |
| NFR-03 | Read availability ≥ 99.9 % |
| NFR-04 | Write availability ≥ 99.95 % |
| NFR-05 | NTP skew ≤ 1 s |
| NFR-06 | PI Vision P95 load ≤ 5 s |
| NFR-07 | PI Web API P95 ≤ 2 s |
| NFR-08 | Asset Analytics expr P95 ≤ 30 s |
| NFR-09 | Audit trail append-only |
| NFR-10 | Retention ≥ 25 y (GxP-relevant) |
| NFR-11 | Federation lag ≤ 60 s nominal |
| NFR-12 | Real-time Notification delivery ≤ 60 s |
| NFR-13 | Archive tier-down query penalty P95 ≤ 5 s |

## 8. Configuration Items (CI)

| CI ID | Item | Configured Value | Source |
|---|---|---|---|
| CI-01 | Topology | Collective: 1 active + 1 DR | URS-PLAT-01 |
| CI-02 | RPO target | 5 min | URS-PLAT-01 |
| CI-03 | RTO target | 4 h | URS-PLAT-01 |
| CI-04 | Network | Manufacturing IT VLAN, no office route | URS-PLAT-03 |
| CI-05 | Naming convention | `PLANT.AREA.UNIT.TAGTYPE.NAME` | URS-TAG-01 |
| CI-06 | Critical-tag compression | OFF; archive every value | URS-TAG-02 |
| CI-07 | AF-change approval | Author ≠ Approver (QA + Head of Ops) | URS-AF-02 |
| CI-08 | Backfill exception | requires QA approval + reason | URS-DI-01 |
| CI-09 | NTP skew alert | > 1 s | URS-DI-02 |
| CI-10 | Audit-review cadence | monthly | URS-AUD-03 |
| CI-11 | Retention | ≥ 25 y (GxP-relevant) | URS-AUD-04 |
| CI-12 | DR replication-lag alert | > 30 s | URS-PERF-01 |
| CI-13 | Restore-test cadence | quarterly | URS-BAK-02 |
| CI-14 | DR exercise cadence | annual | URS-BAK-03 |
| CI-15 | Service-account rotation | annual | URS-SEC-02 |
| CI-16 | OPC UA security policy | Basic256Sha256 minimum | URS-IF-OPCUA-01 |
| CI-17 | Edge buffer | ≥ 7 d | URS-IF-EDGE-01 |
| CI-18 | Connector staleness alert | > 5 min (GxP) | URS-IF-HEALTH-01 |
| CI-19 | Archive tier-down age | 90 d default | URS-ARCH-02 |
| CI-20 | Federation direction | read-only core ← remote | URS-FED-01 |
| CI-21 | Federation lag alert | > 5 min | URS-FED-03 |
| CI-22 | Notification delivery target | ≤ 60 s | URS-API-02 |
| CI-23 | API rate-limit baseline | per-token, configurable | URS-API-04 |
| CI-24 | EF immutability | enforced post-completion | URS-EF-04 |
| CI-25 | Export meter threshold | 1 M rows / hour | URS-EXP-02 |

## 9. Constraints / Assumptions / Risks

- **Constraints (FS-level):** Cat 3 — no site-authored custom logic in production; non-trivial PI ACE / Asset Analytics scripting requires Cat-5 sub-component RA + FS. Federation direction is read-only core ← remote.
- **Assumptions:** PLC / SCADA / BMS / instrument sources are validated and provide accurate timestamps; AD + NTP + PKI + HashiCorp Vault are validated infrastructure.
- **FS-level risks:** manual data adjustment causing record loss (FS-DI-01 + back-fill QA approval); compression-setting misconfig losing GxP fidelity (FS-TAG-02 + per-tag matrix + verification OQ); audit-trail tampering (FS-AUD-02 + platform append-only); ingest backpressure dropping data (FS-PERF-01 + edge buffer); OPC UA security misconfig (FS-IF-OPCUA-01 + handshake-rejection log review); federation lag undetected (FS-FED-03 + PagerDuty); EF recipe-version mismatch (FS-EF-02); archive-tier-down latency penalty exceeding budget (FS-ARCH-02 + PQ); orphan PI Points (FS-ISA95-02 nightly job); § 11.30 misclassification on internet-exposed Web API (FS-PART11-30).

## 10. References

- KYM-URS-HIST-001 v1.2 (parent URS)
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200
- EU GMP Annex 11 §§ 4, 6, 9, 11
- PIC/S PI 041
- ISA-95 / IEC 62264; ISA-88 / IEC 61512; OPC UA / IEC 62541
- IEC 62443 (industrial communication security)
- ISO/IEC 27001:2022
- ISPE GAMP 5 (2nd Ed., 2022) — Category 3 conventions
- ISPE GAMP Good Practice Guide *Records and Data Integrity*
- AVEVA — *PI System 2024 Reference* (PI Server, AF, EF, Vision, Web API, Integrator, Notification, Asset Analytics, Connector / Edge Data Store)
- AVEVA — *PI System Security Configuration Guide*

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID | Notes |
|---|---|---|
| URS-PLAT-01 | FS-PLAT-01 | |
| URS-PLAT-02 | FS-PLAT-02 | |
| URS-PLAT-03 | FS-PLAT-03 | |
| URS-PLAT-04 | FS-PLAT-04 | |
| URS-PLAT-05 | FS-PLAT-05 | |
| URS-PLAT-06 | FS-PLAT-06 | |
| URS-TAG-01 | FS-TAG-01 | |
| URS-TAG-02 | FS-TAG-02 | |
| URS-TAG-03 | FS-TAG-03 | |
| URS-TAG-04 | FS-TAG-04 | |
| URS-TAG-05 | FS-TAG-05 | |
| URS-ISA95-01 | FS-ISA95-01 | |
| URS-ISA95-02 | FS-ISA95-02 | |
| URS-ISA95-03 | FS-ISA95-03 | |
| URS-ISA95-04 | FS-ISA95-04 | |
| URS-AF-01 | FS-AF-01 | |
| URS-AF-02 | FS-AF-02 | |
| URS-AF-03 | FS-AF-03 | |
| URS-AF-04 | FS-AF-04 | |
| URS-COMP-01 | FS-COMP-01 | |
| URS-COMP-02 | FS-COMP-02 | |
| URS-COMP-03 | FS-COMP-03 | |
| URS-COMP-04 | FS-COMP-04 | |
| URS-ARCH-01 | FS-ARCH-01 | |
| URS-ARCH-02 | FS-ARCH-02 | |
| URS-ARCH-03 | FS-ARCH-03 | |
| URS-ARCH-04 | FS-ARCH-04 | |
| URS-IF-OPCUA-01 | FS-IF-OPCUA-01 | |
| URS-IF-OPCUA-02 | FS-IF-OPCUA-02 | |
| URS-IF-OPCHDA-01 | FS-IF-OPCHDA-01 | |
| URS-IF-MODBUS-01 | FS-IF-MODBUS-01 | |
| URS-IF-EDGE-01 | FS-IF-EDGE-01 | |
| URS-IF-CUSTOM-01 | FS-IF-CUSTOM-01 | |
| URS-IF-INV-01 | FS-IF-INV-01 | |
| URS-IF-HEALTH-01 | FS-IF-HEALTH-01 | |
| URS-EF-01 | FS-EF-01 | |
| URS-EF-02 | FS-EF-02 | |
| URS-EF-03 | FS-EF-03 | |
| URS-EF-04 | FS-EF-04 | |
| URS-EF-05 | FS-EF-05 | |
| URS-EF-06 | FS-EF-06 | |
| URS-VIZ-01 | FS-VIZ-01 | |
| URS-VIZ-02 | FS-VIZ-02 | |
| URS-VIZ-03 | FS-VIZ-03 | |
| URS-ANL-01 | FS-ANL-01 | |
| URS-ANL-02 | FS-ANL-02 | |
| URS-EXP-01 | FS-EXP-01 | |
| URS-EXP-02 | FS-EXP-02 | |
| URS-FED-01 | FS-FED-01 | |
| URS-FED-02 | FS-FED-02 | |
| URS-FED-03 | FS-FED-03 | |
| URS-FED-04 | FS-FED-04 | |
| URS-API-01 | FS-API-01 | |
| URS-API-02 | FS-API-02 | |
| URS-API-03 | FS-API-03 | |
| URS-API-04 | FS-API-04 | |
| URS-API-05 | FS-API-05 | |
| URS-DI-01 | FS-DI-01 | |
| URS-DI-02 | FS-DI-02 | |
| URS-DI-03 | FS-DI-03 | |
| URS-DI-04 | FS-DI-04 | |
| URS-DI-05 | FS-DI-05 | |
| URS-DI-06 | FS-DI-06 | |
| URS-DI-07 | FS-DI-07 | |
| URS-AUD-01 | FS-AUD-01 | |
| URS-AUD-02 | FS-AUD-02 | |
| URS-AUD-03 | FS-AUD-03 | |
| URS-AUD-04 | FS-AUD-04 | |
| URS-AUD-05 | FS-AUD-05 | |
| URS-PART11-10 | FS-PART11-10 | |
| URS-PART11-30 | FS-PART11-30 | |
| URS-PART11-50 | FS-PART11-50 | Signed in eQMS, not in PI |
| URS-PART11-100 | FS-PART11-100 | |
| URS-PART11-200 | FS-PART11-200 | |
| URS-SEC-01 | FS-SEC-01 | |
| URS-SEC-02 | FS-SEC-02 | |
| URS-SEC-03 | FS-SEC-03 | |
| URS-SEC-04 | FS-SEC-04 | |
| URS-SEC-05 | FS-SEC-05 | |
| URS-SEC-06 | FS-SEC-06 | |
| URS-INT-PLC-01 | FS-INT-PLC-01 / IF-PLC-01 | |
| URS-INT-MES-01 | FS-INT-MES-01 / IF-MES-01 | |
| URS-INT-AD-01 | FS-INT-AD-01 / IF-AD-01 | |
| URS-INT-LIMS-01 | FS-INT-LIMS-01 / IF-LIMS-01 | |
| URS-INT-SPC-01 | FS-INT-SPC-01 / IF-SPC-01 | |
| URS-INT-LAKE-01 | FS-INT-LAKE-01 / IF-LAKE-01 | |
| URS-PERF-01 | FS-PERF-01 | |
| URS-PERF-02 | FS-PERF-02 | |
| URS-PERF-03 | FS-PERF-03 | |
| URS-PERF-04 | FS-PERF-04 | |
| URS-AV-01 | FS-AV-01 | |
| URS-BAK-01 | FS-BAK-01 | |
| URS-BAK-02 | FS-BAK-02 | |
| URS-BAK-03 | FS-BAK-03 | |
| URS-TRN-01 | FS-TRN-01 | |
| URS-TRN-02 | FS-TRN-02 | |
| URS-PR-01 | FS-PR-01 | |
| URS-PR-02 | FS-PR-02 | |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Manual data adjustment causing record loss | Medium | High | URS-DI-01 + URS-DI-06 |
| R-02 | Compression-setting misconfig losing GxP fidelity | Medium | High | URS-TAG-02 + URS-COMP-01..03 |
| R-03 | Audit-trail tampering | Low | Critical | URS-AUD-02 + URS-PART11-10 |
| R-04 | Ingest backpressure dropping data | Medium | High | URS-PERF-01 + URS-IF-EDGE-01 buffering |
| R-05 | OPC UA security misconfig (Basic128 / None) exposing tampering | Low | Critical | URS-IF-OPCUA-01 |
| R-06 | Federation replication lag undetected → stale batch reconstruction | Low | High | URS-FED-03 alerting |
| R-07 | Event-Frame template mismatched to recipe version → wrong roll-up | Medium | High | URS-EF-02 + URS-EF-05 |
| R-08 | Archive-tier-down causing query timeout in batch-record reconstruction | Low | High | URS-ARCH-02 + PQ latency test |
| R-09 | Orphan PI Points (not in AF) miss GxP retention | Medium | High | URS-ISA95-02 |
| R-10 | PI Web API exposed to office network without § 11.30 controls | Low | High | URS-PART11-30 + URS-SEC-04 |

Full evaluation in `KYM-RA-HIST-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
