---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "GAMP 5 (2nd Ed., 2022) Cat 3 conventions for non-configured products"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "PIC/S PI 041 — Good Practices for Data Management and Integrity"
  - "ISA-95 (IEC 62264) Enterprise-Control System Integration"
  - "ISA-88 (IEC 61512) Batch Control"
  - "OPC UA (IEC 62541); ISO/IEC 27001:2022"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Process Historian — AVEVA PI System 2024 (PI Server + PI Vision + PI Asset Framework + PI Event Frames + PI Integrator + PI Web API)

**Document Number:** KYM-URS-HIST-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Kymeta Bio ehf, Manufacturing IT Operations, Reykjavík, Iceland *(fictional)*
**System Owner:** Manufacturing IT Lead | **Process Owner:** Head of Operations
**System Class (GAMP 5, 2nd ed.):** Category 3 — Non-Configured Product (commercial historian deployed to vendor's reference architecture; site authors only standard configuration — points, AF templates, Event-Frame templates, Vision displays, Integrator views — and no user code that materially affects control logic. PI ACE / Asset Analytics expressions that perform GxP-critical calculations are treated as Cat-5 sub-components under separate change control.)
**Project Mode:** Configuration project on non-configurable instrument / appliance **AVEVA PI System 2024 (PI Server + PI Vision + PI Asset Framework + PI Event Frames + PI Integrator + PI Web API)** (GAMP 5 Category 3 — Non-Configurable COTS).
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; PIC/S PI 041; ISA-95 (IEC 62264); ISA-88 (IEC 61512); OPC UA (IEC 62541); ISO/IEC 27001:2022

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Manufacturing IT Lead) | _____________ | _____________ | _____ |
| Reviewer (Automation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Process Engineer) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Approver (Head of Operations) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | v1.2 enrichment: tiered to T3 (100-150 reqs; this URS lands at 108 reqs). Added explicit modules per the brief: ISA-95 tag-hierarchy mapping, compression + retention policy, interface devices (OPC-UA + PI Interfaces + edge connectors), batch + event capture per ISA-88, asset framework, trend / analytics / export, archive + tier-down management, multi-site federation, real-time consumer APIs. References modernised per METHODOLOGY § 2A.1. |

## Definitions

| Term | Definition |
|---|---|
| Historian | AVEVA PI System 2024 |
| PI Server / Data Archive | The PI tag-data persistence + compression engine |
| PI Point | A single tag (sensor / signal) recorded over time |
| AF (Asset Framework) | PI Asset Framework — hierarchical asset / element / template model overlaid on tags |
| AF Template | Versioned class definition for an asset (e.g., `Bioreactor_V300`) |
| Event Frame | A bounded interval in time tagging a batch / phase / event (ISA-88 alignment) |
| PI Vision | Web-based visualisation client |
| PI Integrator | Asset-aware export tool to RDBMS / business intelligence |
| PI Web API | REST interface to PI Data Archive + AF |
| PI Interface | Vendor-supplied data-collection connector (e.g., OPC UA, OPC HDA, Modbus, custom) |
| Collective | PI Server replication topology (active + DR) |
| Compression | Swinging-door compression algorithm reducing stored values |
| MES | Werum PAS-X v3.2 |
| SCADA | Inductive Automation Ignition 8.3 (water-system SCADA — separate URS) |
| ISA-95 | Enterprise-control hierarchy (Level 0 sensors → Level 4 enterprise) |
| ISA-88 | Batch control hierarchy (Procedure → Unit Procedure → Operation → Phase) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

Define requirements for the process historian recording all GxP-relevant continuous-process data + batch event context across Kymeta Bio's manufacturing facilities. The historian is the read-only system of record for trend data and the event-frame layer that contextualises continuous data into ISA-88 batch / phase intervals; it does not control any process.

## 2. Scope

**In:** PI Server cluster (active + DR collective); PI Asset Framework (hierarchy mirroring ISA-95 Levels 0–3); PI Event Frames (ISA-88 batch / phase capture); PI Vision web servers; PI Integrator for asset-aware exports to the lakehouse; PI Web API; PI interfaces and connectors to PLC / SCADA / BMS / instrument sources via OPC UA + OPC HDA + Modbus TCP + custom interfaces; ~25,000 PI points across the site; AD authentication; daily backup; NTP sync; archive tier-down to slower storage after configurable age; multi-site federation to the parent Reykjavík core with the Akureyri downstream-fill site.

**Out:** PLC / SCADA / BMS source systems (per-system URSs); analytics tools consuming the historian (e.g., JMP — separate URS); LIMS; eQMS.

## 3. System Description

The historian collects time-series data from automation sources, organises tags in a PI Asset Framework hierarchy that mirrors the ISA-95 Levels 0–3 plant model, contextualises continuous data via Event Frames aligned to the ISA-88 batch / phase model, retains data per the configured compression + retention policy, and serves data read-only to consumer systems (analytics, batch-record support, deviation investigations, real-time SPC). Site authors no significant code beyond standard configuration; any GxP-critical analytics expression (PI ACE / Asset Analytics) is treated as a Cat-5 sub-component under separate change control.

The system supports multi-site federation: the Reykjavík core PI Server federates with the Akureyri downstream-fill site PI Server; data is replicated read-only to the core for enterprise reporting.

## 4. User Roles

| Role | Permissions |
|---|---|
| Operations Engineer | Read trend data via PI Vision; cannot modify points or AF. |
| Process Engineer | Author / approve ad-hoc Event Frame queries and PI Vision displays for engineering analysis. |
| AF Author | Add / modify AF templates and elements under change control. |
| AF Approver (QA + Head of Ops) | Approve AF changes affecting GxP-batch reconstruction. |
| Point Configuration Author | Add / modify PI points under change control. |
| Point Configuration Approver | Approve point compression / retention changes affecting GxP tags. |
| Event Frame Author | Author / modify Event Frame templates per ISA-88 phase model. |
| Backfill Exception Operator | Execute approved back-fill operations under captured reason + QA approval. |
| System Administrator | Patching, AD groups; cannot approve. |
| Federation Administrator | Manage multi-site federation; cannot author / approve site-specific tags. |
| Auditor | Read-only across configuration and audit logs. |

Separation of duties: AF Author ≠ Approver; Point Configuration Author ≠ Approver; Event Frame Author ≠ AF Approver (cross-role).

## 5. User Requirements

### 5.1 Architecture / Hardware / Platform

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | The system shall comprise a PI Server collective (active + DR) with collective replication; RTO ≤ 4 h; RPO ≤ 5 minutes. |
| URS-PLAT-02 | H | R1 | All servers shall reside on UPS / generator-backed power; data-collection interfaces shall buffer locally during a network outage and reconcile on reconnect. |
| URS-PLAT-03 | H | R1 | All servers shall reside on the manufacturing IT VLAN; no office-network access. |
| URS-PLAT-04 | H | R1 | PI Vision web servers shall be load-balanced behind a HA-Proxy front-end with TLS 1.3 termination. |
| URS-PLAT-05 | H | R1 | PI Web API + PI Integrator shall be deployed redundantly with auto-failover. |
| URS-PLAT-06 | H | R1 | All certificates shall be issued from the site PKI with auto-rotation ≤ 12-month validity. |

### 5.2 Tag Naming and Point Configuration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TAG-01 | H | R1 | PI points shall be configured per a documented naming convention `PLANT.AREA.UNIT.TAGTYPE.NAME` (ISA-95 hierarchical). |
| URS-TAG-02 | H | R1 | Compression / archival settings shall be configured to preserve fidelity required for GxP record reconstruction (e.g., on critical CIP / SIP tags, compression OFF + archive every value). |
| URS-TAG-03 | H | R1 | Per point, the `GxP-relevance` extended-attribute flag shall be captured. |
| URS-TAG-04 | H | R1 | The point-creation workflow shall require: source-system reference, unit of measure, scan-class, engineering-units, range, alarm-limits (where applicable), GxP-relevance, owner. |
| URS-TAG-05 | H | R1 | Compression settings on GxP-flagged tags shall require Point-Config-Approver sign-off; non-GxP tags can be self-approved by Point Configuration Author. |

### 5.3 Tag Hierarchy + ISA-95 Mapping

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ISA95-01 | H | R1 | The AF hierarchy shall mirror the ISA-95 (IEC 62264) plant model: Enterprise → Site → Area → Production Line → Process Cell → Unit → Equipment Module → Control Module. |
| URS-ISA95-02 | H | R1 | Every PI Point shall be reachable via an AF element path; orphan points (not linked into AF) shall be flagged for review. |
| URS-ISA95-03 | H | R1 | AF templates shall be versioned; element instantiation shall reference the template version in force at instantiation time. |
| URS-ISA95-04 | M | R2 | The AF shall expose ISA-95 Levels 1–3 via the OPC UA companion specification when consumed by Level-4 MES / ERP. |

### 5.4 Asset Framework (AF) Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AF-01 | H | R1 | AF hierarchy shall reflect the site asset structure; AF templates shall be version-controlled. |
| URS-AF-02 | H | R1 | AF changes affecting GxP-batch reconstruction shall require role-restricted signatures with separation of duties. |
| URS-AF-03 | H | R1 | AF reference-attribute formulas (e.g., calculated KPIs) shall be GxP-classified and shall be Cat-5 sub-component-validated when GxP-critical. |
| URS-AF-04 | M | R2 | AF templates shall expose unit-of-measure metadata; UoM conversions shall be defined per OPC UA UA-100 unit codes. |

### 5.5 Compression and Retention Policy

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-COMP-01 | H | R1 | The system shall support swinging-door compression configurable per point (`CompDev`, `CompMin`, `CompMax`); for GxP-critical tags `CompDev = 0` (no compression). |
| URS-COMP-02 | H | R1 | Retention shall be ≥ 25 years for GxP-relevant tags; non-GxP tags shall be ≥ 5 years unless business-justified longer. |
| URS-COMP-03 | H | R1 | Compression changes on GxP tags shall trigger validation re-run for any downstream consumer (e.g., MES batch records) per impact assessment. |
| URS-COMP-04 | M | R2 | Compression-loss reports shall be runnable on demand showing actual vs theoretical archive size + value-recovery loss. |

### 5.6 Archive + Tier-Down Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ARCH-01 | H | R1 | The PI Data Archive shall use a primary high-IO storage tier (NVMe SAN) for the current archive shift + a secondary cold tier (SAS) for prior shifts. |
| URS-ARCH-02 | H | R1 | Tier-down to cold storage shall occur after a configurable age (default 90 days) without data loss; GxP query latency penalty ≤ 5 s at 95th percentile. |
| URS-ARCH-03 | H | R1 | Archive integrity shall be verified via checksum validation at every archive-shift event; integrity failure shall raise a P1 incident. |
| URS-ARCH-04 | M | R2 | The system shall support archive export to immutable object storage (S3 with object-lock) for long-term retention; export integrity verified via SHA-256 manifest. |

### 5.7 Interface Devices (OPC UA + PI Interfaces + Edge Connectors)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-IF-OPCUA-01 | H | R1 | The system shall consume data from OPC UA (IEC 62541) servers; security mode = `Sign+Encrypt`; security policy ≥ `Basic256Sha256`; certificate trust list governed by PKI. |
| URS-IF-OPCUA-02 | H | R1 | OPC UA subscriptions shall use the `MonitoredItem` model with configurable sampling + publishing intervals per tag class. |
| URS-IF-OPCHDA-01 | H | R1 | Legacy OPC HDA interfaces shall be supported for backfill from non-UA-capable sources; HDA pulls shall be reconciled with current values to detect overlap inconsistencies. |
| URS-IF-MODBUS-01 | M | R2 | Modbus TCP interfaces shall be supported for legacy PLCs without OPC capability. |
| URS-IF-EDGE-01 | H | R1 | Edge connectors (PI Connector / PI Edge Data Store) shall buffer locally on network outage with ≥ 7 days local-store capacity. |
| URS-IF-CUSTOM-01 | M | R2 | Custom interfaces shall include a documented connector specification + integration-test evidence before deployment. |
| URS-IF-INV-01 | H | R1 | A connector inventory shall be maintained with: connector_id, source system, protocol, owner, GxP-relevance flag, last-tested date. |
| URS-IF-HEALTH-01 | H | R1 | Per-connector health (status, latency, queue depth, last-message age) shall be exposed via PI Vision + Prometheus; staleness > 5 min on a GxP tag shall raise an alert. |

### 5.8 Batch + Event Capture per ISA-88

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-EF-01 | H | R1 | The Event Frame layer shall capture ISA-88 batch / unit-procedure / operation / phase intervals; event frames shall include start_ts, end_ts, batch_id, equipment, recipe_version. |
| URS-EF-02 | H | R1 | Event Frame templates shall mirror the recipe library; recipe-version changes shall propagate to Event Frame template versions. |
| URS-EF-03 | H | R1 | Event Frames shall be sourced from PAS-X MES batch-execution events via PI-MES interface; cross-reference shall be deterministic. |
| URS-EF-04 | H | R1 | Event Frames flagged GxP-relevant shall be immutable post-completion; corrections shall be recorded as annotated edits with reason + QA approval. |
| URS-EF-05 | H | R1 | Event Frame attribute roll-ups (min, max, mean, integral over phase) shall be configurable per phase template; calculation-method version shall be captured. |
| URS-EF-06 | M | R2 | Event Frames shall support nesting (procedure → unit procedure → operation → phase) per ISA-88 hierarchy. |

### 5.9 Trend Visualisation + Analytics + Export

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VIZ-01 | H | R1 | PI Vision shall provide trend, gauge, table, and event-frame-aware display elements; displays shall be version-controlled. |
| URS-VIZ-02 | H | R1 | Per-display permissions (read / edit / publish) shall be enforced via AD groups; published displays shall require Process-Engineer approval. |
| URS-VIZ-03 | M | R2 | PI Vision URL parameters shall support deep-linking to specific batch / phase via Event Frame ID for batch-record-reconstruction workflows. |
| URS-ANL-01 | H | R1 | PI Asset Analytics expressions shall be supported for derived attributes; GxP-critical expressions shall be Cat-5 sub-component validated. |
| URS-ANL-02 | M | R2 | The system shall integrate with the site Data Lakehouse via PI Integrator for asset-aware structured exports; export schemas shall be version-controlled. |
| URS-EXP-01 | H | R1 | Ad-hoc data export to CSV / Parquet shall be supported via PI Web API; exports of GxP-relevant data shall be audit-logged with user + scope + timestamp. |
| URS-EXP-02 | M | R2 | Export volume per user shall be metered; excessive volume (> 1 M rows / hour) shall raise a security alert. |

### 5.10 Multi-Site Federation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-FED-01 | H | R1 | The system shall federate the Reykjavík core PI Server with the Akureyri downstream-fill site PI Server; federation shall be read-only from core to remote (no write-back). |
| URS-FED-02 | H | R1 | Site-local tags shall remain authoritative at the site of origin; federation shall expose a unified AF view at the core. |
| URS-FED-03 | H | R1 | Federation replication lag ≤ 60 s under nominal conditions; > 5 min lag shall raise an alert. |
| URS-FED-04 | M | R2 | Federation shall support cross-site Event Frame stitching for product genealogy (upstream Reykjavík bulk → downstream Akureyri fill / finish). |

### 5.11 Real-Time Consumer APIs

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-API-01 | H | R1 | PI Web API shall expose authenticated REST endpoints for tag-value retrieval, trend retrieval, event-frame query, and snapshot subscription. |
| URS-API-02 | H | R1 | PI Notification (Asset Analytics) shall fire on configurable conditions to subscribers (MES alarm, SPC real-time, on-call paging); delivery ≤ 60 s end-to-end. |
| URS-API-03 | H | R1 | API access shall be authenticated via AD-bound service accounts with scope-restricted role-mapping; service-account credentials shall reside in HashiCorp Vault. |
| URS-API-04 | M | R2 | API rate limits shall be configurable per consumer; abusive patterns shall be throttled. |
| URS-API-05 | M | R2 | OPC UA Server interface shall expose select PI tags for Level-4 ERP / business intelligence consumers per ISA-95 Level 3→4. |

### 5.12 Data Integrity (Read-Only Discipline + ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | Point values shall be read-only to all users at runtime; manual data entry shall be prohibited (any need for back-fill shall be treated as an exception with QA approval and a captured reason). |
| URS-DI-02 | H | R1 | Time stamps shall be sourced from the PLC / SCADA wherever possible; PI clock synced to NTP with skew ≤ 1 s. |
| URS-DI-03 | H | R1 | Original raw values shall be preserved per the configured retention; corrections shall be recorded as new annotated values referencing the original. |
| URS-DI-04 | H | R1 | Records shall be Attributable; configuration changes shall be attributed to a named user. |
| URS-DI-05 | H | R1 | Records shall be Legible / Contemporaneous / Original / Accurate / Complete / Consistent / Enduring / Available. |
| URS-DI-06 | H | R1 | Back-fill operations shall log: tag, time window, reason, QA approver, executor, original-vs-corrected value pair. |
| URS-DI-07 | H | R1 | Time-zone shall be UTC at storage; per-user display shall apply local TZ + DST without modifying stored data. |

### 5.13 Audit Trail / 21 CFR Part 11

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Audit trail shall cover point creation / modification, AF changes, Event Frame template changes, security changes, manual data adjustments (back-fill), configuration deployments, federation events. |
| URS-AUD-02 | H | R1 | Audit trail shall be append-only; reviewable in-app + exportable to SIEM. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be performed monthly by Manufacturing IT Lead. |
| URS-AUD-04 | H | R1 | Retention ≥ 25 years for GxP-relevant tags + audit trail. |
| URS-AUD-05 | M | R2 | Audit-trail correlation across PI Server + AF + PI Vision shall be supported via shared user-id + timestamp + correlation-id. |
| URS-PART11-10 | H | R1 | Procedures and controls protecting electronic-record validity per 21 CFR § 11.10(a)–(e); copies generable per § 11.10(b); retention statement per § 11.10(c). |
| URS-PART11-30 | M | R2 | PI Web API exposed beyond manufacturing-IT VLAN shall be treated as an "open system" per § 11.30 with TLS + authentication + non-repudiation controls. |
| URS-PART11-50 | H | R1 | E-signatures (where applied via eQMS gating PI changes) shall include printed name, date / time, meaning per § 11.50. |
| URS-PART11-100 | H | R1 | Unique signatures per § 11.100 — enforced via AD uniqueness + deactivated-account non-reassignment. |
| URS-PART11-200 | H | R1 | Re-authentication at every Vault e-sign event per § 11.200. |

**Note on § 11.50 / signing model:** PI does not natively gate user actions with e-signatures; configuration changes are signed in the change-control system rather than in PI itself. The CR record + eQMS signature is the regulated artefact.

### 5.14 Security / Cybersecurity

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | Domain accounts only; break-glass admin only for emergency. |
| URS-SEC-02 | H | R1 | Service-account secrets shall reside in HashiCorp Vault; rotated annually. |
| URS-SEC-03 | H | R1 | All inter-service communication shall use TLS 1.3 with mutual authentication where possible. |
| URS-SEC-04 | H | R1 | Network segmentation per IEC 62443 zone-and-conduit model; PI Server in `Production Zone`; PI Vision in `DMZ Zone`. |
| URS-SEC-05 | H | R1 | Security patches shall be applied per the site patching SOP under change control; out-of-band emergency patches per the rapid-response runbook. |
| URS-SEC-06 | M | R2 | Quarterly access review of AD-mapped roles; orphan / dormant accounts removed. |

### 5.15 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-PLC-01 | H | R1 | PI interfaces to PLC / SCADA / BMS / instruments via documented protocols (OPC UA, OPC HDA, Modbus, custom). Each interface shall be a documented connector with an owner (per URS-IF-INV-01). |
| URS-INT-MES-01 | M | R2 | MES (PAS-X) shall consume historian data via PI Web API for batch-record reconstruction. |
| URS-INT-AD-01 | H | R1 | Authentication via AD; service accounts via vault. |
| URS-INT-LIMS-01 | M | R2 | LIMS shall consume tagged Event Frame attributes for stability + EM context. |
| URS-INT-SPC-01 | H | R1 | PI Notification subscriptions consumed by the SPC platform (CRN-URS-SPC-001) for real-time SPC alerts. |
| URS-INT-LAKE-01 | M | R2 | Asset-aware exports to the Databricks lakehouse via PI Integrator with schema versioning. |

### 5.16 Performance / Availability / Backup

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | H | R1 | Sustained ingest at the nominal site rate (~25,000 points × configured rates) without backpressure; DR replication lag ≤ 30 seconds. |
| URS-PERF-02 | M | R2 | PI Vision dashboard load time ≤ 5 s at 95th percentile. |
| URS-PERF-03 | M | R2 | PI Web API query response P95 ≤ 2 s for 1-day single-tag queries. |
| URS-PERF-04 | M | R2 | PI Asset Analytics expression evaluation latency P95 ≤ 30 s for nominal expressions. |
| URS-AV-01 | H | R1 | Availability ≥ 99.9 % for read; 99.95 % for write (interfaces). |
| URS-BAK-01 | H | R1 | Database backed up nightly; collective replication for hot DR. |
| URS-BAK-02 | H | R1 | Quarterly restore test, witnessed. |
| URS-BAK-03 | H | R1 | Annual full DR-failover exercise with QA witness. |

### 5.17 Training / Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | LMS-recorded training shall be required for production access. |
| URS-TRN-02 | M | R2 | Role-specific training shall be required for AF Author, Point Configuration Author, Event Frame Author, Federation Administrator roles. |
| URS-PR-01 | H | R1 | Annual periodic review shall cover AF / point inventory, audit-trail review, ingest-health metrics, training currency, federation health, archive-tier-down status; signed by Manufacturing IT Lead + Head of QA. |
| URS-PR-02 | M | R2 | Connector inventory review shall be performed semi-annually; stale connectors (no message > 30 d) shall be reviewed for retirement. |

### 5.18 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem with local OT cached credentials for offline operation; conditional-access policy `OT-Historian Conditional Access (MFA at engineering workstation; collector services use named-location + service-account bind)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the PI metadata DB plus PI-native archive-shipping for time-series archives; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 15 y (batch-history-linked tag history) per the consuming-record schedule. |

## 6. Acceptance Criteria

CS, RA, IQ, OQ, PQ approved and executed (proportionate to Cat 3); PQ shall include: representative ingest at nominal rate, DR-failover scenario, batch-record reconstruction via Event Frame query, real-time SPC notification end-to-end, multi-site federation lag test, archive-tier-down + recall test, ALCOA+ readiness checklist, back-fill exception workflow; VSR approved; RTM maps every URS-ID to ≥ 1 approved test case.

## 7. Constraints

- Vendor patches under change control.
- Non-trivial scripting (custom PI ACE / Asset Analytics with GxP-critical impact) triggers Cat-5 sub-component validation.
- Federation read-only direction is non-negotiable; site-local writes only at site of origin.

## 8. Assumptions

- PLC / SCADA / BMS sources are validated and provide accurate timestamps.
- AD + NTP are validated infrastructure.
- PKI is operational with auto-rotation.
- Site IEC 62443 zone-and-conduit model is in force.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200
- 21 CFR Part 211 §§ .68, .192
- FDA *Data Integrity and Compliance with cGMP* (2018)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11 — Computerised Systems
- EU GMP Annex 15 — Qualification and Validation

### International — ICH
- ICH Q9(R1) — Quality Risk Management

### Industry / Standards
- ISPE GAMP 5 (2nd Ed., 2022) — Cat 3 conventions
- ISPE GAMP Good Practice Guide *Records and Data Integrity*
- PIC/S PI 041 — Good Practices for Data Management and Integrity
- ISA-95 / IEC 62264 — Enterprise-Control System Integration
- ISA-88 / IEC 61512 — Batch Control
- OPC UA / IEC 62541
- IEC 62443 — Industrial Communication Networks Security
- ISO/IEC 27001:2022 — Information Security Management

### Vendor
- AVEVA — *PI System 2024 Reference* (PI Server, PI AF, PI Vision, PI Integrator, PI Web API, PI Event Frames, PI Asset Analytics, PI Connector / Edge Data Store)
- AVEVA — *PI System Security Configuration Guide*

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

