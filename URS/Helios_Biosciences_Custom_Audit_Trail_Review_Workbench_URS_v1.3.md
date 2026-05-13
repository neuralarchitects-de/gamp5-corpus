---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline variant-synthesis, 2026-04-26; enriched 2026-05-12 Wave 3 Chunk I (DI binding deepened + T3 uplift + AI-Act non-binding declared)"
seed_corpus_basis:
  - "GAMP 5 (2nd Edition, 2022) Category 5 conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "21 CFR Part 211 §§ .68, .180, .192"
  - "EU GMP Annex 11 §§ 4, 7, 9, 11, 12, 17"
  - "EU GMP Eudralex Vol 4 (Parts I + II)"
  - "PIC/S PI 041-1 (1 July 2021) — Good Practices for Data Management and Integrity in Regulated GMP/GDP Environments"
  - "FDA Data Integrity and Compliance with Drug CGMP — Questions and Answers (December 2018)"
  - "MHRA GxP Data Integrity Guidance and Definitions (March 2018)"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026)"
  - "ICH Q9(R1); ICH Q10"
  - "ISPE GAMP 5 (2nd ed., 2022); ISPE GAMP GPG Records and Data Integrity (RDI)"
  - "ALCOA+ canonical interpretation per WHO TRS 996 Annex 5"
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

# User Requirements Specification (URS)

## Custom Audit Trail Review Workbench — Helios.ATR v1.0 (in-house)

**Document Number:** HBS-URS-ATR-001
**Version:** 1.2
**Effective Date:** 2026-04-26 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Site:** Helios Biosciences GmbH, Quality IT, Building 17, Penzberg, Bavaria, Germany *(fictional)*
**System Owner:** QA Compliance Manager (Data Integrity)
**Process Owner:** Head of QA Compliance
**Development Owner:** Quality IT — Custom Applications
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom Application
**Project Mode:** Custom-build project — site-developed system (GAMP 5 Category 5 — Bespoke; internal SDLC). System: Helios.ATR v1.0 (in-house).
**EU AI Act 2024/1689 classification:** **NOT in scope of EU AI Act high-risk obligations.** The Workbench is deterministic software (rule-based heuristics + structured workflows) used by QA reviewers; it does not perform AI inference, does not classify or predict, and does not autonomously decide outcomes — every disposition is recorded by a named human reviewer. The system is therefore neither Annex I (no safety component of a regulated product), nor Annex III (not in one of the 8 listed domains), nor under Art. 50 (no AI-generated content shown to a natural person). This classification is documented in § 3 and reviewed annually per URS-PR-03. Heuristics that surface events for review are deterministic rule-based filters, not AI predictions.
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192; EU GMP Annex 11 §§ 4, 7, 9, 11, 12, 17; EU GMP Eudralex Vol 4 (Parts I + II); PIC/S PI 041-1 (1 July 2021); FDA *Data Integrity and Compliance with Drug CGMP — Q&A* (Dec 2018); MHRA *GxP Data Integrity Guidance and Definitions* (March 2018); FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026); ICH Q9(R1); ICH Q10; ISPE GAMP 5 (2nd ed., 2022); ISPE GAMP GPG *Records and Data Integrity*; ALCOA+ per WHO TRS 996 Annex 5.

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _______________________ | _______________________ | __________ |
| Reviewer (QA Compliance Manager — DI) | _______________________ | _______________________ | __________ |
| Reviewer (Quality IT Lead — Custom Applications) | _______________________ | _______________________ | __________ |
| Reviewer (CSV Architect) | _______________________ | _______________________ | __________ |
| Reviewer (Security Architect) | _______________________ | _______________________ | __________ |
| Reviewer (Data Integrity SME) | _______________________ | _______________________ | __________ |
| Reviewer (Regulatory Affairs — DI inspection liaison) | _______________________ | _______________________ | __________ |
| Approver (Head of QA Compliance) | _______________________ | _______________________ | __________ |
| Approver (Head of IT) | _______________________ | _______________________ | __________ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-13 | (synthetic) | Minor citation currency fixes; FDA CSA cited as Feb 2026 final. |
| 1.2 | 2026-05-12 | (synthetic) | **Wave 3 Chunk I enrichment.** Tier T3 uplift. EU AI Act classification explicitly declared **not in scope** (the system is deterministic, not AI). DI binding deepened — added PIC/S PI 041-1 § 9 binding, MHRA 2018 binding, FDA DI Q&A binding, ALCOA+ per WHO TRS 996. New §5 subsections: 5.1a Risk-based review prioritisation; 5.1b Exception-based review (rule-based, NOT AI); 5.2a Review queue + assignment + escalation; 5.2b Reviewer training + qualification; 5.2c Periodic-review cadence + sampling; 5.3a Workbench audit-trail review by independent function; 5.5a ALCOA+ canonical mapping; 5.6a Annex 11 §11 periodic evaluation; 5.6b PIC/S PI 041-1 §9 second-person review; 5.6c MHRA 2018 binding; 5.6d FDA DI Q&A 2018 binding; 5.7a Heuristics catalogue + change-control + false-pos/neg tracking; 5.7b Findings → eQMS bridge metrics; 5.7c Review coverage + age-of-unreviewed metrics; new §9 risks. New ID series: URS-PRIO, URS-EXC, URS-Q, URS-RT, URS-PRC, URS-AUD-WB, URS-A11, URS-PICS, URS-MHRA, URS-FDA-DI, URS-HEUR, URS-MET. |

## Definitions and Acronyms

| Term | Definition |
|---|---|
| ATR | Audit Trail Review |
| Workbench / ATR-WB | Helios.ATR — the in-house Audit Trail Review Workbench |
| Source System | A GxP system whose audit trails are imported (HPLC CDS, GC, dissolution, MES, LIMS, etc.) |
| Connector | An adapter that ingests audit-trail records from a source system into the Workbench |
| Reviewer | A QA reviewer using the Workbench to perform routine or for-cause audit-trail review |
| Senior Reviewer | A reviewer qualified to perform second-person verification per PIC/S PI 041-1 § 9 |
| Disposition | The outcome of a reviewer's evaluation of an audit-trail entry: `noted` / `escalated` / `deviation_raised` |
| Routine review | Scheduled review per source system per the site SOP (daily / weekly / monthly) |
| For-cause review | Review triggered by deviation, complaint, OOS, or inspection |
| Risk-based review | Per PIC/S PI 041-1, sample selection prioritised by GMP-impact risk |
| Exception-based review | Pre-filtered view of events matching rule-based heuristics (NOT AI predictions) |
| Heuristic | A deterministic, configurable rule that tags an event for review-by-exception surfacing |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) per WHO TRS 996 Annex 5 |
| CSA | Computer Software Assurance (FDA, February 2026 final guidance) |
| DI | Data Integrity |
| QAU | Quality Assurance Unit |
| Second-person review | An independent review by a person other than the originator (PIC/S PI 041-1 § 9.7) |

---

## 1. Purpose

The Audit Trail Review Workbench (Helios.ATR) is an in-house custom application that consolidates GxP audit trails from heterogeneous source systems and provides a single, role-controlled interface for routine and for-cause audit-trail review. It exists because the site's current process — opening each source system separately to perform per-system audit-trail review — does not scale, is inconsistent, and has been the subject of regulatory observation in three peer companies' published Warning Letters in the last 24 months.

This URS defines the user, functional, regulatory, non-functional, and SDLC requirements for Helios.ATR. As a custom application, the system is GAMP Category 5 and requires the most rigorous validation rigor — full SDLC, design specification, configuration specification, IQ / OQ / PQ, and ongoing change control.

The system is **deterministic** — it ingests, normalises, filters, and presents audit-trail records to human reviewers. It does not perform AI inference or autonomous classification. The "review-by-exception" surfacing is built from configurable deterministic rules (heuristics catalogue), not machine-learned models. The system is therefore **not in scope of EU AI Act 2024/1689 high-risk obligations** (neither Annex I nor Annex III; nor Art. 50 since no AI-generated content is shown to a natural person).

The URS is the controlling input to the Functional Specification (`HBS-FS-ATR-001`), Design Specification (`HBS-DS-ATR-001`), Configuration Specification (`HBS-CS-ATR-001`), Risk Assessment (`HBS-RA-ATR-001`), IQ / OQ / PQ Protocols, the Vendor Assessment of open-source dependencies (`HBS-VA-OSS-ATR-001`), and the Requirements Traceability Matrix (`HBS-RTM-ATR-001`).

## 2. Scope

### 2.1 In scope

- Helios.ATR backend (Python 3.12, FastAPI, PostgreSQL 16, RabbitMQ for ingest workers).
- Helios.ATR frontend (Single-page application, React 19, served behind site SSO).
- Connectors for the following source systems (day-1):
  - Empower 3.x CDS (HPLC / UPLC) — DB read-only adapter.
  - Chromeleon 7.3 CDS (GC, IC) — DB read-only adapter.
  - Dissolution Workstation Pro v6 — file-watcher adapter (exports XML).
  - PAS-X v3.2 MES — REST API.
  - LabWare LIMS 8 — DB read-only adapter.
- Active Directory federation for named-user authentication.
- Hosting: site OpenShift 4.16 cluster, three replicas in DC-1 with PVCs replicated to DC-2 for DR.
- Backup, monitoring, and observability per site standards (Veeam, Prometheus, Loki, Grafana).
- Heuristics catalogue (deterministic rule-based filters) + heuristics change-control + false-positive / false-negative tracking.
- Metrics surface for QA management: review coverage, age of unreviewed events, finding rate per heuristic.

### 2.2 Out of scope

- Source-system validation — each source system is separately validated.
- Read-write integration with source systems — the Workbench is **read-only** with respect to source data; it never modifies source-system records.
- Periodic-review workflow for the source systems themselves (handled by per-system SOPs).
- Full e-signature ceremony for source-system records — the Workbench captures reviewer disposition; source-system signatures live in the source systems.
- AI / ML / NLP — explicitly out of scope. Any future addition would re-trigger EU AI Act classification under § 3.

### 2.3 System boundary diagram (textual)

```
                ┌──────────────────────────────────────────────────────┐
                │   Active Directory / SSO (Keycloak federation)        │
                └────────────────────────┬─────────────────────────────┘
                                         │ OIDC
                                         ▼
   ┌─────────────────────────────────────────────────────────────────┐
   │                       Helios.ATR (Cat 5 custom)                  │
   │   React SPA  ◄──►  FastAPI backend  ◄──►  PostgreSQL 16          │
   │                              ▲                                   │
   │                              │ RabbitMQ                           │
   │                    ┌─────────┴────────┐                          │
   │                    │  Ingest workers  │                          │
   │                    └──┬───┬───┬───┬───┘                          │
   └───────────────────────┼───┼───┼───┼──────────────────────────────┘
                           │   │   │   │   read-only
            ┌──────────────┘   │   │   └──────────────────┐
            ▼                  ▼   ▼                       ▼
     Empower 3.x CDS      Chromeleon 7.3   PAS-X v3.2 MES   LabWare LIMS 8
                          + Dissolution    (REST API)       (DB read-only)
                            file-watcher

                          ▼
                   MasterControl eQMS (deviation-creation egress, idempotent)
```

## 3. System Description and Intended Use

The Workbench ingests audit-trail records from the listed source systems via dedicated connectors, normalizes them into a canonical event schema (`actor`, `action`, `entity_type`, `entity_id`, `old_value`, `new_value`, `reason`, `source_system`, `source_record_id`, `source_timestamp_utc`, `ingested_at_utc`, `integrity_hash`), and presents them to QA reviewers in role-controlled views.

Reviewers perform two types of review:

- **Routine review** — scheduled per source system (daily / weekly / monthly per the site SOP). Reviewer selects a time window and a source-system scope, marks each filtered event as `noted` / `escalated` / `deviation_raised`, and on completion electronically signs the review record.
- **For-cause review** — triggered by a deviation, complaint, OOS, or inspection. Reviewer searches across systems by actor, time window, entity, or free-text reason. Outcomes feed into the same disposition workflow.

The Workbench does **not** modify source-system data. Reviewer dispositions are stored in the Workbench's own database and are themselves audit-trailed.

The Workbench is the operational realisation of PIC/S PI 041-1 § 9 audit-trail review obligations — specifically § 9.4 (review of audit trails), § 9.5 (review of audit-trail metadata), § 9.6 (frequency based on risk), § 9.7 (second-person review where applicable). The Workbench enforces these obligations through the workflows specified in § 5 below.

## 4. User Roles

| Role | Description | Permissions |
|---|---|---|
| Reviewer | QA reviewer who performs routine and for-cause review. | Read all imported events; record disposition; sign review record. |
| Senior Reviewer | Performs second-person review on escalated dispositions per PIC/S PI 041-1 § 9.7. | All Reviewer permissions plus second-person escalation review. |
| QA Compliance Manager (System Owner) | Approves review records and reads system-level metrics. | All Reviewer permissions plus approve, read-only metrics. |
| Heuristics Steward | Authors + reviews + retires heuristics in the catalogue; cannot disposition. | Heuristic CRUD; cannot disposition. |
| Connector Administrator | Configures connectors and ingest schedules. | Connector CRUD; cannot disposition. |
| System Administrator | Backend deployment, patching, AD groups, observability. | Full administration except disposition and approval. |
| Auditor | Internal QA / external regulator. | Read all events, dispositions, and audit trails; cannot modify. |
| Independent ATR Reviewer | Performs Workbench's own audit-trail review (per Annex 11 § 11 periodic evaluation). Independent of System Owner. | Read Workbench's own audit trail; sign quarterly review report. |

**Separation of duties (URS-PART11-04):** a Reviewer cannot self-approve; the Connector Administrator and System Administrator cannot record dispositions or signatures. Heuristics Steward cannot disposition (independence of rule-author from rule-applier). Independent ATR Reviewer is independent from System Owner (Annex 11 § 11 effectiveness check).

## 5. User Requirements

### 5.1 Ingest

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-INGEST-01 | H | R1 | Each connector shall be **read-only** with respect to source-system data. The Workbench shall not write, modify, or delete any source-system record. |
| URS-INGEST-02 | H | R1 | Each ingested event shall include all fields of the canonical schema; missing fields shall fail the event into a quarantine queue with operator notification. |
| URS-INGEST-03 | H | R1 | Events shall be deduplicated by (`source_system`, `source_record_id`, `source_timestamp_utc`); duplicate detection shall not lose data. |
| URS-INGEST-04 | H | R1 | Each event shall carry an `integrity_hash` over its canonical fields; replays from quarantine shall preserve the original hash. |
| URS-INGEST-05 | M | R2 | Connector schedules shall be configurable per source system; default is hourly with retry-on-failure (max 3 retries, exponential backoff). |
| URS-INGEST-06 | H | R1 | Connector failures (auth failure, schema mismatch, timeout) shall raise alerts to the Connector Administrator within 15 minutes; sustained failures (4 consecutive) shall page the on-call. |
| URS-INGEST-07 | H | R1 | Schema-drift detection: each connector shall run a contract test against the source system nightly; schema-drift events shall raise alerts; ingestion shall continue under the prior schema where possible (forward-compatible). |
| URS-INGEST-08 | H | R1 | All ingested data shall be tagged with the source-system GxP-impact classification (R1 / R2 / R3 inherited from the source system's RA) to enable risk-based review prioritisation. |

### 5.1a Risk-Based Review Prioritisation

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PRIO-01 | H | R1 | Per PIC/S PI 041-1 § 9.6, the Workbench shall surface events with weighting by GMP-impact risk (R1 highest, R3 lowest); higher-impact source systems shall receive proportionally more review attention. |
| URS-PRIO-02 | H | R1 | Prioritisation logic shall be deterministic + configurable in `prioritisation_rules.yaml`; rule changes are change-controlled. |
| URS-PRIO-03 | M | R2 | The prioritisation surface shall expose the rule-id and weighting per event so reviewers can see why an event is prioritised. |

### 5.1b Exception-Based Review (Deterministic Heuristics — Not AI)

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-EXC-01 | H | R1 | A "review-by-exception" view shall pre-filter events that match the heuristics catalogue (after-hours actions, repeated reason-for-change codes, manual-integration on HPLC, time-zone anomalies, signature-modification patterns, deletion attempts, etc.). |
| URS-EXC-02 | H | R1 | Each heuristic shall be a deterministic rule expression (SQL / DSL) over the canonical schema. The system shall NOT use AI / ML / NLP. |
| URS-EXC-03 | H | R1 | Heuristic outputs shall be auditable: per event, the heuristic-id(s) that flagged the event shall be recorded; the reviewer shall see the trigger rationale in-context. |
| URS-EXC-04 | M | R2 | False-positive / false-negative tracking per heuristic shall feed the annual heuristics review (URS-HEUR-01). |

### 5.2 Review Workflow

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-REV-01 | H | R1 | A reviewer shall be able to scope a routine review by source system, time window, actor, entity type, and event-class filter. |
| URS-REV-02 | H | R1 | The reviewer shall record a disposition for each event in scope: `noted`, `escalated`, or `deviation_raised`; un-dispositioned events shall block review closure. |
| URS-REV-03 | H | R1 | Escalated dispositions shall require a second-person review by a Senior Reviewer per PIC/S PI 041-1 § 9.7 before review closure. |
| URS-REV-04 | H | R1 | A `deviation_raised` disposition shall create a deviation record in the site eQMS (MasterControl) via the eQMS API; failure of the eQMS push shall block review closure. |
| URS-REV-05 | M | R2 | The reviewer shall be able to attach free-text comments per event and per review record; comments are themselves audit-trailed. |
| URS-REV-06 | H | R1 | On review closure the reviewer shall sign the review record electronically; the signature binds to a snapshot hash of all events in scope. |
| URS-REV-07 | H | R1 | A "review-by-exception" view shall be available per URS-EXC-01..04. |
| URS-REV-08 | M | R2 | Review records shall be reopenable for amendment with an audit-trailed reason; amendment shall require a new signature; the prior signature shall be preserved. |

### 5.2a Review Queue + Assignment + Escalation

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-Q-01 | H | R1 | A review queue shall expose pending reviews per source system + per scope + per due-date; reviewers shall self-claim or be assigned by the QA Compliance Manager. |
| URS-Q-02 | H | R1 | Overdue reviews (past site-SOP cadence by ≥ 1 cadence-interval) shall escalate to the QA Compliance Manager + paged. |
| URS-Q-03 | M | R2 | Workload-balancing dashboards shall expose per-reviewer queue depth + age. |

### 5.2b Reviewer Training + Qualification

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-RT-01 | H | R1 | Reviewer qualification shall include: site DI policy, heuristics-catalogue familiarisation, source-system audit-trail semantics, regulator-DI-guidance training (PIC/S PI 041-1 + MHRA 2018 + FDA DI Q&A 2018). |
| URS-RT-02 | H | R1 | Senior Reviewer qualification shall additionally include: second-person-review procedure, escalation workflow, regulator-inspection-readiness training. |
| URS-RT-03 | M | R2 | Training currency shall be checked at session start (URS-INT-LMS-01); non-current users shall be blocked from disposition. |
| URS-RT-04 | M | R2 | Annual refresher training including any new regulator advisories or heuristic-catalogue changes. |

### 5.2c Periodic-Review Cadence + Sampling

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PRC-01 | H | R1 | Per source system, the review cadence shall be specified in the site SOP (daily / weekly / monthly) based on GMP impact + event volume; the Workbench shall enforce cadence completeness (every scheduled window has a signed review record). |
| URS-PRC-02 | H | R1 | Where 100% review of all events is impractical, a documented risk-based sampling plan shall be applied per PIC/S PI 041-1 § 9.6; sampling parameters (sample size, sampling method) shall be auditable. |
| URS-PRC-03 | H | R1 | Sampling shall always be augmented by 100% review of: any event from the heuristics-flagged set, any event with `deviation_raised` upstream, any event during a regulatory-investigation window. |

### 5.3 Audit Trail (of the Workbench itself)

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | The Workbench shall maintain its own audit trail covering ingest, configuration changes, dispositions, signatures, access events, and heuristics-catalogue changes. |
| URS-AUD-02 | H | R1 | The Workbench audit trail shall be append-only at the database level; the application role shall not have UPDATE / DELETE on the audit-trail table. |
| URS-AUD-03 | H | R1 | The Workbench audit trail shall be reviewable in human-readable form and exportable as PDF and JSONL. |
| URS-AUD-04 | H | R1 | Workbench audit-trail review shall be performed quarterly by the Independent ATR Reviewer (Annex 11 § 11 periodic evaluation surface) — independent from the System Owner. |
| URS-AUD-05 | H | R1 | All workbench audit-trail events shall meet ALCOA+ at the event level: attributable to named user, legible, contemporaneous (PTP-NTP timestamp), original (no in-place edits), accurate (verified by integrity-hash). |

### 5.3a Workbench Audit-Trail Review by Independent Function

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-AUD-WB-01 | H | R1 | Per Annex 11 § 11 + PIC/S PI 041-1, the Workbench's own audit trail shall be periodically reviewed by a function independent of the System Owner (the Independent ATR Reviewer role). |
| URS-AUD-WB-02 | M | R2 | Findings shall feed CAPA where applicable; findings + closure shall be linked from the periodic-review record. |

### 5.4 21 CFR Part 11 / Annex 11

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Electronic signatures shall meet 21 CFR § 11.50: printed name, date and time, and meaning. |
| URS-PART11-02 | H | R1 | Each signature shall be unique and shall not be reused or reassigned (§ 11.100). |
| URS-PART11-03 | H | R1 | Signatures shall be cryptographically bound to the snapshot hash of the signed record (§ 11.70). |
| URS-PART11-04 | H | R1 | The system shall enforce separation of duties per role definitions in § 4. |
| URS-PART11-05 | H | R1 | Re-authentication shall be required at the moment of signing (§ 11.200). |
| URS-PART11-06 | H | R1 | The system shall comply with EU GMP Annex 11 §§ 4 (validation), 7 (data storage), 9 (audit trails), 11 (periodic evaluation), 12 (security), 17 (printouts). |
| URS-PART11-07 | H | R1 | Per § 11.10(a), procedures + controls protecting record validity shall be enforced. |
| URS-PART11-08 | H | R1 | Per § 11.10(b), the system shall produce accurate + complete copies in both electronic and human-readable form for inspection. |
| URS-PART11-09 | H | R1 | Per § 11.10(c), records shall be protected throughout the 10-year retention period. |
| URS-PART11-10 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals (OIDC / Keycloak / AD). |
| URS-PART11-11 | H | R1 | Per § 11.10(e), an operational audit trail shall exist (see § 5.3). |
| URS-PART11-12 | H | R1 | Per § 11.10(g), authority checks shall be enforced via OPA (URS-PART11-04). |
| URS-PART11-13 | H | R1 | Per § 11.10(k), SOPs + change-control records shall be maintained; reviewed annually. |
| URS-PART11-14 | H | R1 | Per § 11.300, password / credential controls shall meet site InfoSec policy (MFA mandatory, lockout 5 fails / 15 min, complexity per standard). |

### 5.5 Data Integrity (ALCOA+ for the Workbench's own records)

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | All Workbench records shall be Attributable to a named user. |
| URS-DI-02 | H | R1 | Records shall be Legible — exportable as PDF and JSONL. |
| URS-DI-03 | H | R1 | Records shall be Contemporaneous — system clock synchronised to PKI-signed NTP with skew ≤ 1 second. |
| URS-DI-04 | H | R1 | Original ingested events shall be preserved; corrections to canonical fields are recorded as a new corrected-event record referencing the original (no in-place edits). |
| URS-DI-05 | H | R1 | Calculations and heuristics shall be Accurate — verified per OQ. |
| URS-DI-06 | M | R2 | Records shall be Complete, Consistent, Enduring (10-year retention with verified backup), and Available (retrievable within 1 business day for inspection). |

### 5.5a ALCOA+ Canonical Mapping

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-ALC-01 | H | R1 | Per WHO TRS 996 Annex 5 and ALCOA+ canonical interpretation, each canonical-event field shall be evaluated against ALCOA+: Attributable (actor), Legible (human-readable export), Contemporaneous (PTP timestamp), Original (immutable), Accurate (integrity-hash), Complete (no missing required field), Consistent (deduplication + chronology), Enduring (retention floor), Available (retrieval SLA). |
| URS-ALC-02 | H | R1 | OQ test shall verify each ALCOA+ property against representative records. |

### 5.6 Regulatory Binding (DI Cluster)

### 5.6a Annex 11 § 11 Periodic Evaluation

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-A11-01 | H | R1 | Per Annex 11 § 11, the Workbench shall undergo periodic evaluation by an independent function; findings shall feed back into change control. |
| URS-A11-02 | H | R1 | The periodic evaluation shall include: system fitness for purpose, change-control effectiveness, security-control effectiveness, training currency, finding trends from URS-AUD-WB-01. |

### 5.6b PIC/S PI 041-1 § 9 Second-Person Review

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PICS-01 | H | R1 | Per PIC/S PI 041-1 § 9.4, audit-trail review shall be a routine part of GMP review; the Workbench provides the surface. |
| URS-PICS-02 | H | R1 | Per § 9.5, audit-trail metadata (timestamp accuracy, user identity, action context) shall be preserved + reviewable. |
| URS-PICS-03 | H | R1 | Per § 9.6, review frequency shall be risk-based (URS-PRC-01); 100% review where risk warrants. |
| URS-PICS-04 | H | R1 | Per § 9.7, second-person review by an independent qualified person shall be enforced for escalated dispositions (URS-REV-03). |

### 5.6c MHRA Data Integrity Guidance (March 2018) Binding

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-MHRA-01 | H | R1 | Per MHRA 2018 § 6.3 + § 6.4, audit-trail review shall be performed by appropriately-trained personnel; routine + targeted; risk-based; documented. |
| URS-MHRA-02 | H | R1 | Per MHRA 2018 § 6.6, where audit-trail review is delegated to a system, the system's own integrity shall be subject to independent review (URS-AUD-WB-01). |

### 5.6d FDA Data Integrity Q&A (Dec 2018) Binding

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-FDA-DI-01 | H | R1 | Per FDA DI Q&A 2018 Q4 + Q5, audit-trail review shall capture data deletions, data modifications, and changes to critical metadata; the Workbench's canonical schema captures these per URS-INGEST-02. |
| URS-FDA-DI-02 | H | R1 | Per FDA DI Q&A 2018 Q7, the QU shall have responsibility for audit-trail review; the System Owner is the QA Compliance Manager (DI). |

### 5.7 Custom-Software Development (Cat 5 SDLC)

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-DEV-01 | H | R1 | The application shall be developed under a documented SDLC: requirements → design → code → unit test → integration test → security scan → user acceptance → release. Each gate shall require a documented sign-off. |
| URS-DEV-02 | H | R1 | All source code shall be version-controlled in the site Git enterprise instance with signed commits; commits to `main` shall require a passing CI build, code review by ≥ 1 peer, and a passing security scan. |
| URS-DEV-03 | H | R1 | Unit-test coverage shall be ≥ 80% on application code; coverage on the canonical-event schema layer shall be 100%. |
| URS-DEV-04 | H | R1 | Static analysis (Ruff, mypy strict, Bandit) and dependency scanning (Trivy + Snyk) shall run on every CI build. Critical findings shall block the build. |
| URS-DEV-05 | H | R1 | Releases shall be cryptographically signed (cosign) and the signature recorded in the release manifest. |
| URS-DEV-06 | H | R1 | Each release shall ship with: release notes, updated FS / DS / CS, regression test report, security scan report, and a change-control record approved by QA. |
| URS-DEV-07 | M | R2 | Open-source dependencies shall be assessed via the vendor-assessment process for OSS (`HBS-VA-OSS-ATR-001`); license, vulnerability, and maintainership reviewed annually. |
| URS-DEV-08 | H | R1 | Per FDA CSA (Feb 2026), test-effort shall be risk-based — focused testing on high-impact components (canonical schema, audit-trail integrity, signature path, heuristics engine). |

### 5.7a Heuristics Catalogue + Change Control + False-Pos/Neg Tracking

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-HEUR-01 | H | R1 | The heuristics catalogue shall be versioned + change-controlled; heuristic additions / modifications / retirements shall require QA Compliance Manager sign-off. |
| URS-HEUR-02 | H | R1 | Each heuristic shall declare its purpose (DI risk addressed), expression (rule), test cases (events that should match / not match), expected false-positive rate. |
| URS-HEUR-03 | H | R1 | Per-heuristic false-positive + false-negative tracking shall be supported; reviewer disposition outcomes shall be fed back to label-and-improve heuristics. |
| URS-HEUR-04 | M | R2 | Annual heuristics review shall consider observed performance, recent regulator advisories, peer-company Warning Letters. |

### 5.7b Findings → eQMS Bridge Metrics

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-MET-01 | H | R1 | The Workbench shall expose to QA management: total findings raised, findings by source system, findings by heuristic, average finding-to-deviation time, deviation outcomes. |
| URS-MET-02 | M | R2 | Findings + outcomes shall be reconcilable with the eQMS deviation system to detect missed pushes. |

### 5.7c Review Coverage + Age-of-Unreviewed Metrics

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-MET-03 | H | R1 | Review coverage shall be measured per source system + per cadence window: events ingested vs events dispositioned + signed off. |
| URS-MET-04 | H | R1 | Age-of-unreviewed-events shall be measured + surfaced; ages beyond site-SOP threshold shall page QA Compliance. |

### 5.8 Integrations

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-INT-EQMS-01 | H | R1 | Deviation records shall be created in MasterControl via the documented REST API. Idempotency keys shall prevent duplicate deviations on retry. |
| URS-INT-LMS-01 | M | R2 | Reviewer training records shall be retrieved from the site LMS (Cornerstone OnDemand) at session start; reviewers without current training shall be blocked from disposition. |
| URS-INT-AD-01 | H | R1 | Authentication shall federate to Active Directory via Keycloak; service accounts for connectors shall use credential vaulting (HashiCorp Vault). |
| URS-INT-SIEM-01 | H | R1 | Authentication + authorization + disposition events shall be forwarded to Splunk within 60 s of occurrence; SIEM retention immutable ≥ 10 y. |

### 5.9 Performance and Availability

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | Search across the last 90 days of events shall return the first page in ≤ 2 seconds at the 95th percentile under nominal load. |
| URS-PERF-02 | M | R2 | Ingest throughput shall sustain 5,000 events / minute per connector during catch-up after an outage. |
| URS-PERF-03 | L | R3 | Disposition recording latency ≤ 500 ms at the 95th percentile. |
| URS-AV-01 | H | R1 | System availability shall be ≥ 99.5% during business hours; planned-maintenance windows excluded. |

### 5.10 Backup, Restore, Disaster Recovery

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | The PostgreSQL database shall be backed up nightly with PITR continuously archived; retention 10 years. |
| URS-BAK-02 | H | R1 | Quarterly restore tests shall be performed and documented. |
| URS-BAK-03 | M | R2 | RTO ≤ 4 hours; RPO ≤ 15 minutes (replicated PVCs). |
| URS-BAK-04 | M | R2 | Annual cold-archive retrieval drill — sample 5-year-old records restored within 24 h documented. |

### 5.11 Security

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | Authentication via AD / Keycloak; no local accounts other than break-glass. |
| URS-SEC-02 | H | R1 | All client-server traffic via TLS 1.3 with current cipher suites; mTLS for ingest workers ↔ connectors. |
| URS-SEC-03 | H | R1 | Connector service-account credentials shall be retrieved from HashiCorp Vault at start-up; never on disk in clear, never in environment variables. |
| URS-SEC-04 | M | R2 | Vulnerability scans (Tenable Nessus, Trivy on container images) shall run weekly; criticals remediated within 30 days. |
| URS-SEC-05 | H | R1 | The application shall log all authentication, authorization, and disposition events to the site SIEM (Splunk Enterprise) within 60 seconds of occurrence. |
| URS-SEC-06 | H | R1 | DB role enforcement: the application role shall only have INSERT/SELECT on audit-trail tables; no role shall have UPDATE/DELETE on audit-trail tables. |

### 5.12 Training

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Production access requires completed role-specific training recorded in the LMS (curriculum per URS-RT-01..02). |
| URS-TRN-02 | M | R2 | Reviewers shall complete annual refresher training including site DI policy and the Workbench heuristics catalogue. |

### 5.13 Periodic Review and Continuous Improvement

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PR-01 | H | R1 | Periodic review at least annually examining: configuration drift, audit-trail review evidence (URS-AUD-WB-01), deviation / change-control summary, ingest health, false-positive / false-negative rate of heuristics (URS-HEUR-03), training currency, review-coverage metrics, age-of-unreviewed-events metrics. |
| URS-PR-02 | M | R2 | Periodic review shall be signed by QA Compliance Manager + Head of QA Compliance + Independent ATR Reviewer. |
| URS-PR-03 | M | R2 | Heuristics catalogue shall be reviewed and updated annually based on observed dispositions and recent regulator guidance (URS-HEUR-04); EU AI Act classification re-confirmation occurs at the same cadence. |

### 5.14 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is Kerberos on-prem for interactive reviewer logon (Keycloak federation to AD for the Workbench UI); conditional-access policy `Quality-App Conditional Access (MFA + device-compliance) plus reviewer-training currency check at every session start` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the Workbench event store plus object-replica for the long-term audit-trail cold archive in S3; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 25 y (audit-trail master) per the consuming-record schedule. |

### 5.15 Cross-System Integration — LMS competence handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-LMS-01 | H | R1 | Workbench reviewers shall pass an LMS competence check (curriculum `HELIOS-REVIEWER-v1.x` + per-source-system addendum) before being assigned to a review queue; LMS competence shall be re-checked at every session start (max-age 12 h cache); on lapse, the reviewer shall be auto-removed from queues and their open items reassigned. |

## 6. Acceptance Criteria

The system shall enter validated routine GMP use when:

1. FS, DS, CS, RA, IQ, OQ, PQ Protocols approved.
2. SDLC artifacts present and approved: design review minutes, code-review records, unit-test results, integration-test results, security-scan results.
3. IQ executed; all critical findings closed.
4. OQ executed; all critical and major findings closed; minor findings dispositioned.
5. PQ executed including connector ingest of representative volumes per source system, end-to-end review workflow (routine + for-cause), exception-based review against heuristic-flagged corpus, second-person-review path (URS-PICS-04), deviation creation in MasterControl, periodic-evaluation rehearsal per Annex 11 § 11.
6. DR failover tested.
7. Annual cold-archive retrieval rehearsed.
8. Validation Summary Report approved by QA Compliance Manager + Head of IT + Independent ATR Reviewer.
9. RTM shows every URS requirement mapped to at least one approved test case.

## 7. Constraints

- The Workbench shall not modify source-system data under any circumstance; this is a hard architectural invariant enforced at the connector layer (read-only DB roles, read-only API tokens) and re-tested in OQ.
- The Workbench is GAMP Cat 5; all changes are change-controlled. Hot-fixes follow an emergency change procedure with retrospective change-control filing within 5 business days.
- No direct internet egress from production; package mirrors are internal.
- The Workbench shall not employ AI / ML / NLP. Any future AI addition would re-trigger EU AI Act classification under § 3.
- Per FDA CSA (Feb 2026), test-effort is risk-based; effort emphasis on high-impact components (canonical schema, audit-trail integrity, signature path).

## 8. Assumptions

- Source systems are themselves validated and continue to expose stable audit-trail interfaces.
- Active Directory, Keycloak, HashiCorp Vault, Splunk, MasterControl, and Cornerstone are validated infrastructure or themselves CSV-validated.
- Quality IT — Custom Applications team is staffed with developers trained on the site's GxP SDLC.
- BfArM is the German regulator with GMP-inspection authority for the Penzberg site (medicinal products); BfR GLP-Bundesstelle is the German GLP authority — out of scope for this URS.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 — Electronic Records; Electronic Signatures (§§ .10, .30, .50, .70, .100, .200, .300).
- 21 CFR Part 211 §§ .68 (automatic equipment validation), .180 (records general requirements), .192 (production records review).
- FDA *Data Integrity and Compliance with Drug CGMP — Questions and Answers* (December 2018).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).

### EU — EMA / Commission
- EU GMP Annex 11 — Computerised Systems (§§ 4, 7, 9, 11, 12, 17).
- EU GMP Eudralex Volume 4 — Good Manufacturing Practice (Parts I + II).
- EMA Q&A on Annex 11.

### UK — MHRA
- MHRA *GxP Data Integrity Guidance and Definitions* (March 2018).

### International — ICH / ISPE / PIC/S / WHO
- ICH Q9(R1) — Quality Risk Management.
- ICH Q10 — Pharmaceutical Quality System.
- ISPE GAMP 5 (2nd Edition, 2022); ISPE GAMP Good Practice Guide *Records and Data Integrity*.
- PIC/S PI 041-1 — Good Practices for Data Management and Integrity in Regulated GMP/GDP Environments (1 July 2021).
- WHO Technical Report Series 996 Annex 5 — *Guidance on good data and record management practices*.

### DACH-specific
- BfArM (DE) — German medicinal-product + medical-device authority; GMP-inspection coverage for Penzberg.
- BfR GLP-Bundesstelle (DE) — out of scope for GMP-only Workbench but noted for separation.

### Internal
- Helios SDLC Standard for Custom GxP Applications (`HBS-SOP-IT-CUST-001`).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
