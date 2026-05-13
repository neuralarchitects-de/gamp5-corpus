---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; enriched 2026-05-12 Wave 3 Chunk I (DI binding deepened + per-ID rows + AI-Act non-binding declared)"
seed_corpus_basis:
  - "HBS-URS-ATR-001 v1.2"
  - "GAMP 5 (2nd Edition, 2022) Category 5 conventions"
  - "21 CFR Part 11; 21 CFR Part 211"
  - "EU GMP Annex 11; PIC/S PI 041-1 (2021); MHRA DI Guidance (2018); FDA DI Q&A (2018)"
  - "FDA CSA (Feb 2026)"
parent_urs:
  document_number: HBS-URS-ATR-001
  version: 1.2
  file: ../../URS/_generated/final/Helios_Biosciences_Custom_Audit_Trail_Review_Workbench_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# Functional Specification (FS)

## Custom Audit Trail Review Workbench — Helios.ATR v1.0

**Document Number:** HBS-FS-ATR-001
**Version:** 1.2
**Effective Date:** 2026-04-26 *(synthetic)*
**Parent URS:** HBS-URS-ATR-001 v1.2
**Site:** Helios Biosciences GmbH, Quality IT, Building 17, Penzberg, Bavaria, Germany *(fictional)*
**System Owner:** QA Compliance Manager (Data Integrity)
**Development Owner:** Quality IT — Custom Applications
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom Application
**EU AI Act 2024/1689 classification:** **NOT in scope** (deterministic software, no AI inference; classification documented in URS § 3 and reviewed annually per FS-PR-03).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192; EU GMP Annex 11 §§ 4, 7, 9, 11, 12, 17; EU GMP Eudralex Vol 4 (Parts I + II); PIC/S PI 041-1 (1 July 2021); FDA Data Integrity Q&A (Dec 2018); MHRA GxP Data Integrity Guidance (March 2018); FDA CSA (final, February 2026); ICH Q9(R1); ICH Q10; ISPE GAMP 5 + GAMP RDI; WHO TRS 996 Annex 5.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (QA Compliance Manager — DI) | _____________ | _____________ | _____ |
| Reviewer (Quality IT Lead — Custom Applications) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (DI SME) | _____________ | _____________ | _____ |
| Approver (Head of QA Compliance) | _____________ | _____________ | _____ |
| Approver (Head of IT) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-13 | (synthetic) | FDA CSA citation currency to Feb 2026. |
| 1.2 | 2026-05-12 | (synthetic) | Wave 3 Chunk I rewrite: parent URS upgraded to v1.2. EU AI Act non-binding explicitly stated. Per-URS-ID rows replace range-compression. New FS rows for URS-INGEST-07/08, URS-PRIO-01..03, URS-EXC-01..04, URS-REV-08, URS-Q-01..03, URS-RT-01..04, URS-PRC-01..03, URS-AUD-05, URS-AUD-WB-01..02, URS-PART11-07..14, URS-ALC-01..02, URS-A11-01..02, URS-PICS-01..04, URS-MHRA-01..02, URS-FDA-DI-01..02, URS-DEV-08, URS-HEUR-01..04, URS-MET-01..04, URS-INT-SIEM-01, URS-PERF-03, URS-BAK-04, URS-SEC-06, URS-TRN-02, URS-PR-03. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## Definitions

Defined in `HBS-URS-ATR-001`. Additional FS-specific terms:

| Term | Definition |
|---|---|
| Connector | Adapter implementing the `BaseConnector` interface |
| Canonical Event | The normalized event schema produced by connectors and persisted in the Workbench |
| Heuristic | A configured deterministic rule that tags an event for "review-by-exception" surfacing (NOT AI) |
| OPA | Open Policy Agent — used for fine-grained authz policies |
| WeasyPrint | HTML-to-PDF rendering service used for PDF/A-3 export |

---

## 1. Purpose

This FS describes the implementation of `HBS-URS-ATR-001` v1.2 as a Cat-5 site-authored web application running on the site OpenShift cluster. The Workbench ingests audit-trail records from heterogeneous source systems via connectors, normalizes to a canonical event schema, and exposes role-controlled review workflows. The system is deterministic; no AI/ML/NLP is used; EU AI Act high-risk obligations are not in scope.

## 2. Scope

The Workbench application — backend (Python 3.12 + FastAPI + PostgreSQL 16 + RabbitMQ), frontend (React 19 SPA), connectors (Empower, Chromeleon, Dissolution Workstation, PAS-X, LIMS), integration with eQMS / SSO / Vault / SIEM / LMS. Out of scope: source-system internals; eQMS deviation-lifecycle internals.

## 3. System Architecture

### 3.1 Container Inventory

| Container | Image | Replicas | Resources |
|---|---|---|---|
| `atr-api` | `helios-cr.io/atr-api:1.2.0` | 3 | 2 vCPU, 4 GiB |
| `atr-frontend` | `helios-cr.io/atr-frontend:1.2.0` | 2 | 1 vCPU, 1 GiB |
| `atr-worker` (per connector) | `helios-cr.io/atr-worker:1.2.0` | 1–3 / connector | 2 vCPU, 4 GiB |
| `atr-postgres` | `pgsql:16` | 3 (Patroni cluster) | 4 vCPU, 16 GiB |
| `atr-rabbitmq` | `rabbitmq:3` | 3 | 2 vCPU, 4 GiB |

### 3.2 Logical Architecture (textual)

```
[Reviewer browser] ──HTTPS──► [Ingress / WAF] ──► [atr-frontend SPA] ──► [atr-api]
                                                                              │
                                                                              ▼
                                                                  [PostgreSQL 16 (Patroni)]
                                                                              │
                                                                              ▲
                                                                              │
                              ┌──── RabbitMQ ───────────────────┐             │
                              │                                  │             │
            [atr-worker: Empower] [atr-worker: Chromeleon]  ...  └─────► (event sink)
                       │                  │
                       ▼                  ▼
                 [Empower DB]      [Chromeleon DB]      [Dissolution file-share]      [PAS-X REST]
                 (read-only role)  (read-only role)    (file watcher)                 (read-only token)

                          ▼
                   [MasterControl eQMS] (deviation egress, idempotent)
                          ▼
                   [Splunk SIEM] (immutable ≥ 10 y)
                          ▼
                   [Cornerstone LMS] (training-currency check)
```

### 3.3 Functional Modules

| Module | Function |
|---|---|
| Connector Framework | `BaseConnector` interface; per-source connector implementations; quarantine queue; nightly schema-drift contract tests. |
| Canonical Event Pipeline | Normalize source records to the canonical schema; deduplicate; integrity-hash; tag with source-system GxP-impact. |
| Review Workflow Engine | Routine / for-cause review scopes; disposition; second-person verification (PIC/S § 9.7); review queue + assignment + escalation. |
| Prioritisation Engine | Deterministic GMP-risk-weighted event surfacing. |
| Heuristics Engine | Configurable deterministic rule-based exception-review filters; per-heuristic false-pos / false-neg tracking. |
| Audit Trail Engine | Append-only audit-trail capture for the Workbench's own actions; independent-reviewer surface (Annex 11 § 11). |
| Sign-off Service | E-signature handling with re-auth + binding. |
| eQMS Integration | Deviation-creation client with idempotency. |
| Authorization | OPA-based fine-grained authz over canonical-event scopes. |
| Search / Index | Postgres GIN index on canonical-event JSON + Postgres FTS. |
| Metrics + Coverage | Review-coverage + age-of-unreviewed + findings-to-deviation metrics. |

---

## 4. Functional Specifications

### 4.1 Ingest (URS §5.1 + §5.1a + §5.1b)

| FS ID | URS ID | Description |
|---|---|---|
| FS-INGEST-01 | URS-INGEST-01 | Connector service accounts use read-only DB roles; the Workbench database does not have any privilege on source-system schemas; OQ verifies via attempted INSERT/UPDATE that fails with permission error. |
| FS-INGEST-02 | URS-INGEST-02 | Canonical-event schema validated by Pydantic v2 model on connector output; missing required fields route the record to the `quarantine` table with a notification. |
| FS-INGEST-03 | URS-INGEST-03 | Deduplication key = `(source_system, source_record_id, source_timestamp_utc)`; PostgreSQL UNIQUE constraint enforces; ON CONFLICT DO NOTHING preserves the original. |
| FS-INGEST-04 | URS-INGEST-04 | `integrity_hash` = SHA-256 over the canonical fields; replays from quarantine preserve the original hash by storing it pre-quarantine. |
| FS-INGEST-05 | URS-INGEST-05 | Connector schedules in `connector_schedules` table; cron expression per source; default hourly with exponential backoff (1, 2, 4 min) on failure. |
| FS-INGEST-06 | URS-INGEST-06 | Connector failure events posted to RabbitMQ topic `atr.alerts` and consumed by an alerting service (PagerDuty integration); ≥ 4 consecutive failures page on-call. |
| FS-INGEST-07 | URS-INGEST-07 | Nightly contract-test job `connector_contract_test.py` per connector against test instance; schema-drift events raise `SCHEMA_DRIFT_DETECTED` alert; ingest continues under prior schema where forward-compatible. |
| FS-INGEST-08 | URS-INGEST-08 | Canonical-event row carries `source_gxp_impact` enum (R1/R2/R3) inherited from source-system RA; feeds prioritisation engine. |
| FS-PRIO-01 | URS-PRIO-01 | Prioritisation engine `prioritisation.py` weights events: R1×10, R2×3, R3×1; per-rule weights configurable in `prioritisation_rules.yaml`. |
| FS-PRIO-02 | URS-PRIO-02 | Rule changes to `prioritisation_rules.yaml` via git PR + QA Compliance Manager sign-off; signed-commit enforced. |
| FS-PRIO-03 | URS-PRIO-03 | Per-event prioritisation surface in reviewer UI: shows applied rule IDs + cumulative weight. |
| FS-EXC-01 | URS-EXC-01 | "Review-by-exception" view applies heuristics catalogue at query time; standard heuristics: `after_hours_action`, `repeated_reason_for_change`, `manual_integration_hplc`, `tz_anomaly`, `signature_modification_pattern`, `delete_attempt`. |
| FS-EXC-02 | URS-EXC-02 | Heuristics expressed as SQL/JSONPath rules in `heuristics/{name}.yaml`; CI gate `assert_no_ai_imports.py` blocks any AI/ML library import in the engine module. |
| FS-EXC-03 | URS-EXC-03 | Per-event `triggered_heuristics: [heuristic_id]` field; reviewer UI shows rationale tooltip per heuristic. |
| FS-EXC-04 | URS-EXC-04 | Reviewer-disposition outcome (`noted` / `escalated` / `deviation_raised`) is fed back per `(heuristic_id, disposition)` pair to per-heuristic FP/FN counters; surfaced in heuristics-review report. |

### 4.2 Review Workflow (URS §5.2 + §5.2a + §5.2b + §5.2c)

| FS ID | URS ID | Description |
|---|---|---|
| FS-REV-01 | URS-REV-01 | Scope-builder UI generates a Postgres query against `canonical_events` filtered by source / window / actor / entity / event-class; results paginated server-side. |
| FS-REV-02 | URS-REV-02 | Each event-row in the scope must carry a non-null `disposition` enum (`noted`, `escalated`, `deviation_raised`) before "Close Review" enables. |
| FS-REV-03 | URS-REV-03 | Escalated events queue into the `senior_review` view; Senior-Reviewer signature required before "Close Review" enables on the parent review record. |
| FS-REV-04 | URS-REV-04 | `deviation_raised` triggers `eqms_client.create_deviation(payload)`; failure (non-2xx) blocks closure with an actionable error UI. |
| FS-REV-05 | URS-REV-05 | Comments stored in `event_comments` table; each comment is itself audit-trailed in the Workbench audit trail. |
| FS-REV-06 | URS-REV-06 | Close-review writes the snapshot hash (SHA-256 over the in-scope event IDs and their dispositions) and binds to the closing signature. |
| FS-REV-07 | URS-REV-07 | Heuristics catalogue stored in `heuristics` table; the "review-by-exception" view applies the EFFECTIVE heuristic set as Postgres views over `canonical_events`. |
| FS-REV-08 | URS-REV-08 | Review-amendment workflow: status `AMENDMENT_DRAFT` → new disposition → new signature; prior signature preserved + linked via `prior_signature_id`. |
| FS-Q-01 | URS-Q-01 | Review queue UI exposes pending reviews; reviewers can self-claim via "Claim" button; QA Compliance Manager can assign via "Assign" workflow. |
| FS-Q-02 | URS-Q-02 | Overdue-review detector `overdue_monitor.py` runs hourly; overdue (past site-SOP cadence + 1 interval) → escalate to QA Compliance Manager + PagerDuty page. |
| FS-Q-03 | URS-Q-03 | Workload-balancing dashboard `queue_health.json` per reviewer: queue depth + average age. |
| FS-RT-01 | URS-RT-01 | LMS curriculum `HBS-CURR-ATR-Reviewer-v2` covers site DI policy + heuristics-catalogue + source-system audit-trail semantics + PIC/S PI 041-1 + MHRA 2018 + FDA DI Q&A 2018. |
| FS-RT-02 | URS-RT-02 | LMS curriculum `HBS-CURR-ATR-SeniorReviewer-v2` adds second-person review procedure + escalation + inspection-readiness modules. |
| FS-RT-03 | URS-RT-03 | LMS API call at session start (FS-INT-LMS-01); non-current users receive 403 blocking disposition. |
| FS-RT-04 | URS-RT-04 | Annual refresher tracked in LMS recertification job; reminders 60 d / 30 d / 7 d before lapse. |
| FS-PRC-01 | URS-PRC-01 | Cadence enforcement: per source system, scheduled-review-window records created automatically; missed windows surface as `MISSING_REVIEW` in the queue. |
| FS-PRC-02 | URS-PRC-02 | Sampling-plan record per source-system review: `sampling_method`, `sample_size`, `population_size`, justification per PIC/S § 9.6; OQ test exercises sampling-plan instantiation. |
| FS-PRC-03 | URS-PRC-03 | 100%-review categories implemented as filter overrides: heuristic-flagged events + upstream `deviation_raised` events + regulatory-investigation-window events are always included regardless of sampling. |

### 4.3 Audit Trail (Workbench's Own) (URS §5.3 + §5.3a)

| FS ID | URS ID | Description |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | All ingest, configuration, disposition, signature, access, and heuristics-catalogue events written to `audit_events` with ALCOA+ fields. |
| FS-AUD-02 | URS-AUD-02 | DB role `atr_app` granted only INSERT/SELECT on `audit_events`; UPDATE/DELETE denied at PostgreSQL level. |
| FS-AUD-03 | URS-AUD-03 | Audit-trail review UI exports as PDF via the WeasyPrint service; JSONL export endpoint also available. |
| FS-AUD-04 | URS-AUD-04 | Quarterly review report template `HBS-RPT-ATR-AUDIT-QUARTERLY`; auto-scheduled + assigned to the Independent ATR Reviewer (NOT the System Owner). |
| FS-AUD-05 | URS-AUD-05 | Per-event ALCOA+ field tags asserted at write: `actor_id` (Attributable), exportable (Legible), `timestamp_iso8601` PTP-NTP (Contemporaneous), `parent_event_id` immutability (Original), `integrity_hash` (Accurate). |
| FS-AUD-WB-01 | URS-AUD-WB-01 | Independent-ATR-Reviewer Splunk saved-search `atr_self_review_q{n}` over Workbench's own audit-trail; quarterly report signed by Independent role. |
| FS-AUD-WB-02 | URS-AUD-WB-02 | Findings link into MasterControl via `eqms_client.create_finding()`; closure records linked from the next periodic-review report. |

### 4.4 21 CFR Part 11 / Annex 11 (URS §5.4)

| FS ID | URS ID | Description |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Sign-off API enforces `printed_name + date_time_utc + meaning`; meaning enum `authorship | review | approval | execution_witness | release | retirement`. |
| FS-PART11-02 | URS-PART11-02 | Each user identity from Keycloak ↔ AD ↔ HR — uniqueness preserved end-to-end. |
| FS-PART11-03 | URS-PART11-03 | Signature payload binds to the snapshot hash; verification at retrieval re-computes the hash and validates. |
| FS-PART11-04 | URS-PART11-04 | OPA authz policies enforce role separation per the URS-§4 matrix; tested via the `opa-test` CI job. |
| FS-PART11-05 | URS-PART11-05 | Sign-off endpoint requires a fresh OIDC ID token (`auth_time` < 60 s). |
| FS-PART11-06 | URS-PART11-06 | Annex 11 §§ 4 / 7 / 9 / 11 / 12 / 17 controls mapped one-to-one against URS / FS items + traceability index `annex11_map.md`. |
| FS-PART11-07 | URS-PART11-07 | Procedural controls SOP `/sop/atr-controls.md` enforced; reviewed annually. |
| FS-PART11-08 | URS-PART11-08 | Export endpoints (FS-AUD-03) produce both JSON (electronic) and PDF/A-3 (human-readable) copies; hash compare verifies consistency. |
| FS-PART11-09 | URS-PART11-09 | Retention 10 y enforced via S3 Object Lock + Patroni base backups; OQ test attempts delete pre-floor → 403. |
| FS-PART11-10 | URS-PART11-10 | Access via Keycloak OIDC; AD federated; no local accounts other than break-glass. |
| FS-PART11-11 | URS-PART11-11 | Operational audit trail per FS-AUD-01. |
| FS-PART11-12 | URS-PART11-12 | OPA policy bundle enforces authority checks per § 11.10(g); `opa-test` CI job validates. |
| FS-PART11-13 | URS-PART11-13 | SOP repo `/sop/` annual review tracked in `sop_review_calendar.yaml`. |
| FS-PART11-14 | URS-PART11-14 | Keycloak password policy: MFA mandatory, 5-fail-15-min lockout, complexity per site standard. |

### 4.5 Data Integrity (URS §5.5 + §5.5a)

| FS ID | URS ID | Description |
|---|---|---|
| FS-DI-01 | URS-DI-01 | All Workbench records carry `created_by` / `updated_by` set from the authenticated principal. |
| FS-DI-02 | URS-DI-02 | PDF export via WeasyPrint; JSONL export streamed for large result sets. |
| FS-DI-03 | URS-DI-03 | Application clock synced to PKI-signed NTP `ntp.helios.local`; OQ measures skew. |
| FS-DI-04 | URS-DI-04 | Original ingested events are immutable; corrections recorded as new `correction_event` rows referencing the original by `parent_event_id`. |
| FS-DI-05 | URS-DI-05 | Heuristics + decision logic Accurate per OQ regression test (`heuristic_oq.py`). |
| FS-DI-06 | URS-DI-06 | Retention 10 y on PostgreSQL + S3 object-lock cold archive; restore tested quarterly. |
| FS-ALC-01 | URS-ALC-01 | ALCOA+ canonical-mapping document `alcoa_plus_mapping.md` links each field to a property; per-field OQ checks. |
| FS-ALC-02 | URS-ALC-02 | OQ test suite `alcoa_oq.py` enumerates each ALCOA+ property + verifies on representative records. |

### 4.6 Regulatory Binding (URS §5.6a–§5.6d)

| FS ID | URS ID | Description |
|---|---|---|
| FS-A11-01 | URS-A11-01 | Annex 11 § 11 periodic evaluation: Independent ATR Reviewer role separate from System Owner; quarterly evaluation report. |
| FS-A11-02 | URS-A11-02 | Evaluation report covers: fitness for purpose, change-control effectiveness, security-control effectiveness, training currency, finding trends — captured in `periodic_eval_template.md`. |
| FS-PICS-01 | URS-PICS-01 | PIC/S § 9.4 surface: all canonical events routed through review queues; review evidence retained per FS-REV-06. |
| FS-PICS-02 | URS-PICS-02 | PIC/S § 9.5 metadata preserved: per-event metadata fields `actor` + `timestamp_utc` + `action` + `entity_id` + integrity-hash. |
| FS-PICS-03 | URS-PICS-03 | PIC/S § 9.6 frequency: per FS-PRC-01 cadence enforcement + sampling FS-PRC-02. |
| FS-PICS-04 | URS-PICS-04 | PIC/S § 9.7 second-person review: enforced via FS-REV-03 (escalated events require Senior-Reviewer signature). |
| FS-MHRA-01 | URS-MHRA-01 | MHRA 2018 § 6.3-6.4 — reviewer qualification via FS-RT-01..04; risk-based + routine + targeted per FS-PRC-01..03; documented in review records FS-REV-06. |
| FS-MHRA-02 | URS-MHRA-02 | MHRA 2018 § 6.6 — Workbench's own audit-trail subject to independent review per FS-AUD-WB-01. |
| FS-FDA-DI-01 | URS-FDA-DI-01 | FDA DI Q&A 2018 Q4-Q5 — canonical schema captures `old_value` / `new_value` + `action` enum including `delete` / `modify` / `metadata_change`. |
| FS-FDA-DI-02 | URS-FDA-DI-02 | FDA DI Q&A 2018 Q7 — System Owner is QA Compliance Manager (DI); ownership documented in System Operating Manual + LMS curriculum. |

### 4.7 Custom-Software SDLC (URS §5.7)

| FS ID | URS ID | Description |
|---|---|---|
| FS-DEV-01 | URS-DEV-01 | The Cat-5 SDLC for `helios-atr` is documented in `HBS-SOP-IT-CUST-001`; CI workflows enforce gates. |
| FS-DEV-02 | URS-DEV-02 | Repo `git.helios.local/quality-it/helios-atr`; branch protection requires 1 reviewer + passing CI; commit signing via Sigstore enforced. |
| FS-DEV-03 | URS-DEV-03 | Coverage measured by `pytest-cov`; CI fails below 80% on application code, 100% on canonical-event schema layer. |
| FS-DEV-04 | URS-DEV-04 | Ruff + mypy --strict + Bandit + Trivy + Snyk on every CI build; criticals break the build. |
| FS-DEV-05 | URS-DEV-05 | Container images cosign-signed; release manifest signed; OpenShift Image Policy verifies signature pre-deploy. |
| FS-DEV-06 | URS-DEV-06 | Each release `manifest.yaml` lists release notes, FS / DS / CS deltas, regression-test summary, security-scan report path, change-control record ID. |
| FS-DEV-07 | URS-DEV-07 | OSS-dependency vendor-assurance per `HBS-VA-OSS-ATR-001`; annual review covers license, vulnerability, maintainership. |
| FS-DEV-08 | URS-DEV-08 | Per FDA CSA (Feb 2026), test-effort is risk-based: high-effort on canonical-schema layer (100% coverage + property tests), signature-path module (mutation tests), heuristics engine (table-driven OQ); lower-effort on UI components. |

### 4.7a Heuristics + Metrics (URS §5.7a + §5.7b + §5.7c)

| FS ID | URS ID | Description |
|---|---|---|
| FS-HEUR-01 | URS-HEUR-01 | Heuristic-catalogue versioning in git `heuristics/`; QA Compliance Manager sign-off enforced via branch protection. |
| FS-HEUR-02 | URS-HEUR-02 | Per-heuristic spec template `heuristics/_template.md`: purpose, rule expression, expected FP rate, test cases. |
| FS-HEUR-03 | URS-HEUR-03 | Per-heuristic FP / FN counters in `heuristic_stats` table; reviewer disposition outcomes feed via FS-EXC-04. |
| FS-HEUR-04 | URS-HEUR-04 | Annual heuristics review template `heuristics_annual_review.md`; outcomes feed catalogue PRs. |
| FS-MET-01 | URS-MET-01 | Metrics dashboard `qa_metrics_dashboard.json`: findings raised + findings by source + findings by heuristic + finding-to-deviation lead-time + deviation outcomes. |
| FS-MET-02 | URS-MET-02 | Reconciliation job `metrics_reconciliation.py` nightly compares Workbench findings vs eQMS deviations; missing-push alerts. |
| FS-MET-03 | URS-MET-03 | Coverage metric `review_coverage.py`: ingested vs dispositioned-and-signed per source per cadence window; surfaced on QA dashboard. |
| FS-MET-04 | URS-MET-04 | Age-of-unreviewed monitor `age_monitor.py`; PagerDuty page on threshold breach to QA Compliance. |

### 4.8 Integrations (URS §5.8)

| FS ID | URS ID | Description |
|---|---|---|
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | `eqms_client.create_deviation()` posts to MasterControl with idempotency key `atr:review:<reviewId>:event:<eventId>`; retries with backoff; failure surfaces in the close-review UI. |
| FS-INT-LMS-01 | URS-INT-LMS-01 | `lms_client.training_status(userId, curriculumId)` call at session start; non-current users receive a `403` blocking disposition actions. |
| FS-INT-AD-01 | URS-INT-AD-01 | OIDC via Keycloak federated to AD; service accounts retrieve secrets from HashiCorp Vault at startup via the Vault Agent sidecar. |
| FS-INT-SIEM-01 | URS-INT-SIEM-01 | Splunk Universal Forwarder forwards auth / authz / disposition events; SLO 60 s; immutable retention ≥ 10 y. |

### 4.9 Performance, Backup, Security, Training, PR (URS §5.9–§5.13)

| FS ID | URS ID | Description |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | Postgres indexes (GIN on JSON + B-tree on `created_at`, `actor`); `EXPLAIN ANALYZE` performance baselines; OQ asserts ≤ 2 s P95 search 90-day window. |
| FS-PERF-02 | URS-PERF-02 | Worker concurrency configured per connector; OQ asserts 5,000 events/min sustained per connector during catch-up. |
| FS-PERF-03 | URS-PERF-03 | Disposition recording endpoint p95 latency ≤ 500 ms verified by k6 PQ script. |
| FS-AV-01 | URS-AV-01 | OpenShift HPA + readiness probes; SLO 99.5% during business hours. |
| FS-BAK-01 | URS-BAK-01 | Patroni base backups + WAL-G to S3 nightly + continuous WAL archiving; retention 10 y + cold archive. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore test scripted in `helios-atr-dr` repo; QA witness sign-off. |
| FS-BAK-03 | URS-BAK-03 | RTO ≤ 4 h via DR-site PVC replication; RPO ≤ 15 min via WAL streaming. |
| FS-BAK-04 | URS-BAK-04 | Annual cold-archive retrieval drill; sample 5-year-old records restored + integrity-hash verified within 24 h documented. |
| FS-SEC-01 | URS-SEC-01 | OIDC + MFA at Keycloak; no local accounts other than break-glass. |
| FS-SEC-02 | URS-SEC-02 | TLS 1.3 at the ingress; mTLS service-to-service via Istio. |
| FS-SEC-03 | URS-SEC-03 | Secrets retrieved from Vault Agent sidecar; OQ verifies no credentials on disk / env. |
| FS-SEC-04 | URS-SEC-04 | Tenable + Trivy weekly; criticals SLA 30 days. |
| FS-SEC-05 | URS-SEC-05 | Splunk forwarder; OQ asserts < 60 s SIEM forward latency. |
| FS-SEC-06 | URS-SEC-06 | DB role `atr_app` granted INSERT/SELECT on audit-trail only; UPDATE/DELETE explicitly denied; OQ attempts UPDATE → permission denied. |
| FS-TRN-01 | URS-TRN-01 | Cornerstone curriculum `HBS-CURR-ATR-Reviewer-v2` (per FS-RT-01..04). |
| FS-TRN-02 | URS-TRN-02 | Annual refresher reminder job in LMS; lapse blocks disposition. |
| FS-PR-01 | URS-PR-01 | Periodic-review template `HBS-PR-ATR-YYYYMMDD` covers: config drift, audit-trail review evidence, deviation / CR summary, ingest health, heuristic FP / FN rate, training currency, review-coverage + age-of-unreviewed metrics. |
| FS-PR-02 | URS-PR-02 | QA Compliance Manager + Head of QA Compliance + Independent ATR Reviewer signatures. |
| FS-PR-03 | URS-PR-03 | Heuristics catalogue annual review tracked in `heuristics_review_calendar`; EU AI Act classification re-confirmation occurs at the same cadence. |

---


### 4.10 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: Kerberos on-prem for interactive reviewer logon (Keycloak federation to AD for the Workbench UI). Conditional-access binding to policy `Quality-App Conditional Access (MFA + device-compliance) plus reviewer-training currency check at every session start`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the Workbench event store plus object-replica for the long-term audit-trail cold archive in S3; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.11 Cross-System Integration — LMS handover (M-XINT-LMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-LMS-01 | URS-XINT-LMS-01 | LMS-competence adapter `<sys>-LMS-CLIENT-1.x` performs `GET /lms/competence/{user_id}?curriculum=...` over mTLS + Entra workload-identity; cache TTL per system (12-24 h); on `current=false` the consumer blocks the gated action and records `lms_lapse_user={user_id}` in the consumer audit trail; periodic reconciliation job verifies that no gated action proceeded with a lapsed competence. |

## 5. Interface Specifications

### 5.1 IF-SOURCE-EMPOWER

- Direct connection to Empower Oracle DB via `atr-svc-empower-ro` Oracle role (read-only); SQL queries parameterised.

### 5.2 IF-SOURCE-CHROMELEON

- Direct connection to Chromeleon SQL DB via `atr-svc-chromeleon-ro` SQL role (read-only).

### 5.3 IF-SOURCE-DISSOLUTION

- File-watcher on `\\\\dissolution-export\\share`; XML files parsed and posted to RabbitMQ ingest queue.

### 5.4 IF-SOURCE-PASX

- HTTPS GET `https://pasx.helios.local/api/v1/audit?from=<iso8601>&to=<iso8601>`; OAuth2 client-credentials with read-only scope.

### 5.5 IF-SOURCE-LIMS

- Direct connection to LabWare LIMS Oracle DB via `atr-svc-lims-ro` Oracle role (read-only).

### 5.6 IF-EQMS-OUT

- HTTPS POST `https://eqms.helios.local/api/v2/deviations`; idempotency key.

### 5.7 IF-AUTH

- OIDC against `https://keycloak.helios.local/realms/helios`; AD federation; JWT carries roles + groups.

### 5.8 IF-LMS

- HTTPS GET `https://cornerstone.helios.local/api/v1/training-status?user={uid}&curriculum={cid}`.

### 5.9 IF-SIEM

- Splunk HTTP Event Collector (HEC); index `wel-atr`.

---

## 6. Data Model (high-level)

| Entity | Description |
|---|---|
| canonical_events | Normalized audit-trail events (immutable; corrections via correction_event); carries `source_gxp_impact` + `triggered_heuristics` |
| reviews | Routine / for-cause review records |
| event_dispositions | Per-event disposition within a review |
| audit_events | Workbench's own audit trail (append-only) |
| signatures | E-signature records with snapshot-hash binding |
| heuristics | Configured heuristic rules + spec metadata |
| heuristic_stats | Per-heuristic FP / FN counters |
| connector_schedules | Per-source ingest schedules |
| quarantine | Records that failed schema validation pending operator action |
| review_windows | Cadence-window records (auto-created; one per source × cadence period) |
| amendments | Linked prior + current signature records for amended reviews |

---

## 7. Non-Functional Specifications

| Aspect | Target | URS reference |
|---|---|---|
| Search P95 (90-day window) | ≤ 2 s | URS-PERF-01 |
| Ingest throughput / connector | 5,000 events/min | URS-PERF-02 |
| Disposition latency P95 | ≤ 500 ms | URS-PERF-03 |
| Availability | ≥ 99.5% business hours | URS-AV-01 |
| RPO / RTO | 15 min / 4 h | URS-BAK-03 |
| Audit retention | 10 y online + 10 y cold | URS-DI-06 |
| Cold archive retrieval drill | annual ≤ 24 h | URS-BAK-04 |
| SIEM forward latency | ≤ 60 s | URS-SEC-05 |

---

## 8. Configuration Items

| CI ID | Item | Value |
|---|---|---|
| CI-01 | Container registry | `helios-cr.io/quality-it/helios-atr` |
| CI-02 | Cosign public key | `helios-sigstore-pubkey-2026q2` |
| CI-03 | Keycloak realm | `helios` |
| CI-04 | Vault path | `secrets/quality-it/helios-atr/*` |
| CI-05 | OPA policy bundle | `helios-atr-opa-bundle:1.2.0` |
| CI-06 | NTP | `ntp.helios.local` |
| CI-07 | SIEM | Splunk index `wel-atr` |
| CI-08 | LMS curricula | `HBS-CURR-ATR-Reviewer-v2`, `HBS-CURR-ATR-SeniorReviewer-v2` |
| CI-09 | Heuristics catalogue base path | `heuristics/` |
| CI-10 | Prioritisation rules | `prioritisation_rules.yaml` |
| CI-11 | Cold archive | S3 + Glacier Vault Lock (10 y) |
| CI-12 | EU AI Act scope | OUT OF SCOPE (deterministic; reviewed annually) |

---

## 9. Constraints / Assumptions / Risks

Inherited from `HBS-URS-ATR-001` v1.2. FS-specific:

| Risk | Mitigation |
|---|---|
| OPA policy bundle mismatch | OPA policies cosign-signed; CI verifies signature |
| Connector schema drift | Contract tests in CI run nightly against test instances (FS-INGEST-07) |
| Reviewer training gap blocks disposition | URS-INT-LMS-01 + grace-period escalation procedure |
| Heuristics-engine module accidentally importing AI library | `assert_no_ai_imports.py` CI gate (FS-EXC-02) |
| WeasyPrint rendering failure on PDF/A-3 export | Fallback to plain-PDF + alert + manual rendering |
| Cohen-κ-style label-rating not applicable (no AI labelling) | Out of scope by FS-EXC-02 constraint |

## 10. References

- `HBS-URS-ATR-001 v1.2` (parent URS)
- 21 CFR Part 11; 21 CFR Part 211 §§ .68, .180, .192
- EU GMP Annex 11 §§ 4, 7, 9, 11, 12, 17; EU GMP Eudralex Vol 4
- PIC/S PI 041-1 (1 July 2021)
- MHRA *GxP Data Integrity Guidance and Definitions* (March 2018)
- FDA *Data Integrity and Compliance with Drug CGMP — Q&A* (Dec 2018); FDA CSA (final, Feb 2026)
- ISPE GAMP 5 (2nd ed., 2022); ISPE GAMP GPG *Records & Data Integrity*
- WHO Technical Report Series 996 Annex 5
- BfArM (DE)
- Site documents: `HBS-SOP-IT-CUST-001`, `HBS-VA-OSS-ATR-001`, `HBS-RPT-ATR-AUDIT-QUARTERLY`

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | Implementing FS ID |
|---|---|
| URS-INGEST-01 | FS-INGEST-01 |
| URS-INGEST-02 | FS-INGEST-02 |
| URS-INGEST-03 | FS-INGEST-03 |
| URS-INGEST-04 | FS-INGEST-04 |
| URS-INGEST-05 | FS-INGEST-05 |
| URS-INGEST-06 | FS-INGEST-06 |
| URS-INGEST-07 | FS-INGEST-07 |
| URS-INGEST-08 | FS-INGEST-08 |
| URS-PRIO-01 | FS-PRIO-01 |
| URS-PRIO-02 | FS-PRIO-02 |
| URS-PRIO-03 | FS-PRIO-03 |
| URS-EXC-01 | FS-EXC-01 |
| URS-EXC-02 | FS-EXC-02 |
| URS-EXC-03 | FS-EXC-03 |
| URS-EXC-04 | FS-EXC-04 |
| URS-REV-01 | FS-REV-01 |
| URS-REV-02 | FS-REV-02 |
| URS-REV-03 | FS-REV-03 |
| URS-REV-04 | FS-REV-04 |
| URS-REV-05 | FS-REV-05 |
| URS-REV-06 | FS-REV-06 |
| URS-REV-07 | FS-REV-07 |
| URS-REV-08 | FS-REV-08 |
| URS-Q-01 | FS-Q-01 |
| URS-Q-02 | FS-Q-02 |
| URS-Q-03 | FS-Q-03 |
| URS-RT-01 | FS-RT-01 |
| URS-RT-02 | FS-RT-02 |
| URS-RT-03 | FS-RT-03 |
| URS-RT-04 | FS-RT-04 |
| URS-PRC-01 | FS-PRC-01 |
| URS-PRC-02 | FS-PRC-02 |
| URS-PRC-03 | FS-PRC-03 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
| URS-AUD-05 | FS-AUD-05 |
| URS-AUD-WB-01 | FS-AUD-WB-01 |
| URS-AUD-WB-02 | FS-AUD-WB-02 |
| URS-PART11-01 | FS-PART11-01 |
| URS-PART11-02 | FS-PART11-02 |
| URS-PART11-03 | FS-PART11-03 |
| URS-PART11-04 | FS-PART11-04 |
| URS-PART11-05 | FS-PART11-05 |
| URS-PART11-06 | FS-PART11-06 |
| URS-PART11-07 | FS-PART11-07 |
| URS-PART11-08 | FS-PART11-08 |
| URS-PART11-09 | FS-PART11-09 |
| URS-PART11-10 | FS-PART11-10 |
| URS-PART11-11 | FS-PART11-11 |
| URS-PART11-12 | FS-PART11-12 |
| URS-PART11-13 | FS-PART11-13 |
| URS-PART11-14 | FS-PART11-14 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-ALC-01 | FS-ALC-01 |
| URS-ALC-02 | FS-ALC-02 |
| URS-A11-01 | FS-A11-01 |
| URS-A11-02 | FS-A11-02 |
| URS-PICS-01 | FS-PICS-01 |
| URS-PICS-02 | FS-PICS-02 |
| URS-PICS-03 | FS-PICS-03 |
| URS-PICS-04 | FS-PICS-04 |
| URS-MHRA-01 | FS-MHRA-01 |
| URS-MHRA-02 | FS-MHRA-02 |
| URS-FDA-DI-01 | FS-FDA-DI-01 |
| URS-FDA-DI-02 | FS-FDA-DI-02 |
| URS-DEV-01 | FS-DEV-01 |
| URS-DEV-02 | FS-DEV-02 |
| URS-DEV-03 | FS-DEV-03 |
| URS-DEV-04 | FS-DEV-04 |
| URS-DEV-05 | FS-DEV-05 |
| URS-DEV-06 | FS-DEV-06 |
| URS-DEV-07 | FS-DEV-07 |
| URS-DEV-08 | FS-DEV-08 |
| URS-HEUR-01 | FS-HEUR-01 |
| URS-HEUR-02 | FS-HEUR-02 |
| URS-HEUR-03 | FS-HEUR-03 |
| URS-HEUR-04 | FS-HEUR-04 |
| URS-MET-01 | FS-MET-01 |
| URS-MET-02 | FS-MET-02 |
| URS-MET-03 | FS-MET-03 |
| URS-MET-04 | FS-MET-04 |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 |
| URS-INT-LMS-01 | FS-INT-LMS-01 |
| URS-INT-AD-01 | FS-INT-AD-01 |
| URS-INT-SIEM-01 | FS-INT-SIEM-01 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-PERF-03 | FS-PERF-03 |
| URS-AV-01 | FS-AV-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-BAK-03 | FS-BAK-03 |
| URS-BAK-04 | FS-BAK-04 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-SEC-05 | FS-SEC-05 |
| URS-SEC-06 | FS-SEC-06 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-PR-02 | FS-PR-02 |
| URS-PR-03 | FS-PR-03 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-LMS-01 | FS-XINT-LMS-01 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Connector defect causing missed events from a source system | Medium | Critical | URS-INGEST-02..06 + integration tests |
| R-02 | Read-only invariant violated through misconfiguration | Low | Critical | URS-DEV-01..08 + URS-INGEST-01 + tested in OQ |
| R-03 | Heuristics over- or under-flag, masking real DI issues | Medium | High | URS-HEUR-01..04 + annual heuristics review + reviewer feedback loop |
| R-04 | Privileged user tampers with Workbench audit trail | Low | Critical | URS-AUD-02 (DB role separation) + URS-SEC-05 (SIEM) + URS-SEC-06 |
| R-05 | Sustained connector failure goes unnoticed | Low | High | URS-INGEST-06 + paging on consecutive failures |
| R-06 | eQMS deviation push fails silently | Low | High | URS-REV-04 + idempotency + reviewer-visible failure indicator |
| R-07 | Schema drift in a source system breaks ingest | Medium | High | URS-INGEST-07 (contract tests run in CI nightly) |
| R-08 | Review backlog (age-of-unreviewed > threshold) | Medium | High | URS-MET-03..04 + URS-Q-02 escalation |
| R-09 | Reviewer fatigue / disposition rubber-stamping | Medium | High | URS-EXC-04 + URS-Q-03 workload-balancing + URS-HEUR-03 false-pos tracking |
| R-10 | Workbench's own audit trail not independently reviewed | Low | Critical | URS-AUD-WB-01 + URS-A11-01 + Independent ATR Reviewer role |
| R-11 | Sampling plan inappropriate for risk → blind spot | Low | High | URS-PRC-02..03 + risk-based sampling justification |
| R-12 | Second-person review by-passed | Low | Critical | URS-REV-03 + URS-PICS-04 (enforced in workflow) |
| R-13 | Training currency lapse → unqualified reviewer dispositioning | Low | High | URS-RT-03 + URS-INT-LMS-01 |
| R-14 | EU AI Act scope-creep (e.g., adding ML-based heuristic) without re-classification | Low | High | URS-PR-03 + change-control gate |

These risks are formally evaluated in `HBS-RA-ATR-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
