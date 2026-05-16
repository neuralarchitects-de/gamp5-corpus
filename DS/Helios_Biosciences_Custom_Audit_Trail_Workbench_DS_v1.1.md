---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "HBS-FS-ATR-001 v1.2 (parent FS)"
  - "HBS-URS-ATR-001 v1.2 (informational)"
  - "GAMP 5 (2nd ed., 2022) Cat 5 — Software Design Specification"
  - "21 CFR Part 11; EU GMP Annex 11; PIC/S PI 041-1 (2021); MHRA DI 2018; FDA DI Q&A 2018"
  - "Deterministic rule-based audit-trail consolidator — NOT in EU AI Act scope"
parent_fs:
  document_number: HBS-FS-ATR-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Helios_Biosciences_Custom_Audit_Trail_Workbench_FS_v1.3.md
parent_urs:
  document_number: HBS-URS-ATR-001
  version: 1.2
  file: ../../../URS/_generated/final/Helios_Biosciences_Custom_Audit_Trail_Review_Workbench_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Software Design Specification (SDS)

## Custom Audit Trail Review Workbench — Helios.ATR v1.0

**Document Number:** HBS-DS-ATR-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** HBS-FS-ATR-001 v1.2 | **Parent URS:** HBS-URS-ATR-001 v1.2
**Site:** Helios Biosciences GmbH, Quality IT, Building 17, Penzberg, Bavaria, Germany *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom Application (site-developed deterministic-rule-based audit-trail consolidator over DuckDB + Postgres)
**EU AI Act 2024/1689 classification:** **EXPLICITLY NOT IN SCOPE.** This system is a **deterministic, rule-based audit-trail consolidator and review workbench. It does not perform AI inference at runtime; it has no machine-learning models, no statistical inference, no generative output, no probabilistic decision-making. The "anomaly" and "heuristic" rules in the workbench (HEUR-01..04) are explicit Boolean predicates over event data (e.g. "actor not in approved-actors list", "back-dated entry detected", "out-of-hours admin action") — they are software-engineered rules, not learned models. Per EU AI Act Art. 3 + Annex III definitions, this system is therefore not an "AI system" under the Act and no Annex classification applies. Risk register notes this exclusion explicitly.**
**Project Mode:** Greenfield site-developed audit-trail consolidator replacing manual cross-system audit-trail review workflow (per parent URS Project Mode line)
**Tier (inherited from parent URS+FS):** T3
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; **21 CFR Part 211 §§ .68 (automatic equipment), .180 (general requirements for records), .192 (production-record review)**; EU GMP Annex 11 §§ 4, 7, 9, 11, 12, 17; EU GMP Eudralex Vol 4 (Parts I + II); **PIC/S PI 041-1 (1 July 2021) — Good Practices for Data Management and Integrity**; **FDA Data Integrity Q&A (Dec 2018)**; **MHRA GxP Data Integrity Guidance (March 2018)**; FDA CSA (Feb 2026); ICH Q9(R1); ICH Q10; ISPE GAMP 5 (2nd ed., 2022); ISPE GAMP RDI (Records and Data Integrity); WHO TRS 996 Annex 5; GDPR Arts. 6, 32, 35.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect — Quality IT) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of QA — Data Integrity) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (DPO) | _____________ | _____________ | _____ |
| Reviewer (Source-System Owners — LIMS, MES, eQMS, EDC, ELN) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |
| Approver (System Owner — Head of QA Data Integrity) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue. Inherited Tier T3 from parent URS+FS pair. Derived from HBS-FS-ATR-001 v1.2. DS covers 110/114 FS-IDs as DS-IDs; 4 FS-IDs flagged as "vendor-internal — no site design surface" (DuckDB query-engine internals, Postgres internals, source-system audit-trail-export internal formats, Okta IdP internals). EU AI Act non-applicability declared in § 3 with risk-register entry. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from HBS-URS-ATR-001 v1.2 and HBS-FS-ATR-001 v1.2. Additional DS-specific terms:

| Term | Definition |
|---|---|
| ATR | Audit Trail Review (Helios.ATR) |
| Source system | A GxP system whose audit trail Helios.ATR consumes (LIMS, MES, eQMS, EDC, ELN, Sirius PV, Theia MDR, etc.) |
| Ingest adapter | Per-source-system component that extracts + normalises audit-trail events |
| Heuristic rule | A deterministic Boolean predicate over event fields (NOT a learned model — see § 3 EU AI Act non-applicability declaration) |
| Event-correlation | Deterministic SQL-based cross-system event linkage (e.g. "this LIMS approval ⟷ this MES batch record") |
| PII-redaction | Hash-based pseudonymisation of identifiers per per-source policy |
| Workbench | The reviewer UI for QA + DI investigators |
| DI | Data Integrity (ALCOA+) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate, plus Complete, Consistent, Enduring, Available |
| Helios | Helios Biosciences GmbH — the operator (also branded "Helios.ATR" as product) |

## 1. Purpose

This SDS describes the technical design of the site-developed Helios.ATR Audit Trail Review Workbench: a Python-based, deterministic rule-based audit-trail consolidator that ingests audit-trail events from named GxP source systems (LIMS, MES, eQMS, EDC, ELN, Sirius PV, Theia MDR, etc.), normalises them to a unified schema, correlates events across systems, applies deterministic anomaly heuristics, and presents a reviewer workbench for QA + DI investigators. The SDS is the controlling input to Module Specifications (`HBS-MS-ATR-{module}-001`), IQ/OQ/PQ Protocol Set, validation report against Annex 11 § 9 / PIC/S PI 041-1 / MHRA DI / FDA DI Q&A. Vendor internals (DuckDB, Postgres, source-system audit-export formats) are not redrawn.

## 2. Scope

**In scope.** Site-developed Python services: source-system ingest adapters (one per source); audit-trail event normaliser; PII-redaction worker; DuckDB analytical store + Postgres operational store; deterministic heuristic-rule engine (HEUR-01..04); cross-system event correlator (EXC-01..04); reviewer workbench UI; reviewer queue + assignment; finding lifecycle (open → triage → analyse → CAPA → close); per-finding evidence bundle generator; metrics + KPIs (MET-01..04); ALCOA+ implementation reporting (ALC-01..02); FDA DI Q&A + MHRA DI mapping (FDA-DI-01..02 + MHRA-01..02); PIC/S PI 041-1 mapping (PICS-01..04); 21 CFR Part 11 sub-section controls (PART11-01..14); Annex 11 § 4/7/9/11/12/17 mapping (A11-01..02); audit-trail-of-the-audit-trail (AUD-WB-01..02 — Helios.ATR's own audit trail).

**Out of scope.** Source-system internals (their own SDLC); DuckDB + Postgres query-engine internals (vendor); source-system audit-export internal formats (their own SDLC); Okta IdP design.

## 3. Architectural Overview

```
                         ┌─ Helios.ATR boundary ─────────────────────────┐
                         │                                               │
   Source-system         │   ┌─────────────────────────────────────┐     │
   audit-trail exports  ─┼──►│ Ingest Adapter — LIMS              │     │
   (LIMS Caelum, MES     │   ├─────────────────────────────────────┤     │
   Ophir, eQMS Master-   │   │ Ingest Adapter — MES PAS-X         │     │
   Control, EDC          │   ├─────────────────────────────────────┤     │
   Marigold, ELN Cyrene, │   │ Ingest Adapter — eQMS              │     │
   Sirius PV Argus,      │   ├─────────────────────────────────────┤     │
   Theia MDR TrackWise,  │   │ Ingest Adapter — EDC Medidata      │     │
   …)                    │   ├─────────────────────────────────────┤     │
                         │   │ Ingest Adapter — ELN Benchling     │     │
                         │   ├─────────────────────────────────────┤     │
                         │   │ Ingest Adapter — Sirius PV (Argus) │     │
                         │   ├─────────────────────────────────────┤     │
                         │   │ Ingest Adapter — Theia MDR (TWD-Q) │     │
                         │   ├─────────────────────────────────────┤     │
                         │   │ Ingest Adapter — Other (per-system)│     │
                         │   └────────────┬────────────────────────┘     │
                         │                ▼                              │
                         │   ┌─────────────────────────────────┐         │
                         │   │ Normaliser → unified envelope    │         │
                         │   │ {event_id, source_system,         │         │
                         │   │  source_record_id, actor, ts_utc,│         │
                         │   │  ts_local, action, before, after,│         │
                         │   │  reason}                          │         │
                         │   └────────────┬────────────────────┘         │
                         │                ▼                              │
                         │   ┌─────────────────────────────────┐         │
                         │   │ PII-redaction (per-source       │         │
                         │   │ policy)                          │         │
                         │   └────────────┬────────────────────┘         │
                         │                ▼                              │
                         │   ┌─────────────────────────────────┐         │
                         │   │ Postgres operational store +    │         │
                         │   │ DuckDB analytical store         │         │
                         │   └─┬───────────────────────────────┘         │
                         │     │                                          │
                         │     ▼                                          │
                         │   ┌─────────────────────────────────┐         │
                         │   │ Deterministic Heuristic Engine   │         │
                         │   │ (HEUR-01..04 — Boolean only)    │         │
                         │   │   • out-of-hours admin           │         │
                         │   │   • back-dated entry             │         │
                         │   │   • orphan signature             │         │
                         │   │   • un-justified reverse-action  │         │
                         │   └────────────┬────────────────────┘         │
                         │                ▼                              │
                         │   ┌─────────────────────────────────┐         │
                         │   │ Cross-system Event Correlator    │         │
                         │   │ (EXC-01..04 — deterministic SQL)│         │
                         │   └────────────┬────────────────────┘         │
                         │                ▼                              │
                         │   ┌─────────────────────────────────┐         │
                         │   │ Workbench UI (Reviewer queue +  │         │
                         │   │ finding lifecycle + evidence    │         │
                         │   │ bundle generator)                │         │
                         │   └────────────┬────────────────────┘         │
                         │                ▼                              │
                         │   MasterControl CAPA + ServiceNow CR          │
                         └────────────────────────────────────────────────┘
```

**Three architectural views per § 2B.5(1):**

**Logical view.** Per-source ingest adapter pulls (push-based via Kafka where source supports; pull-based via REST + secure file where not) the audit-trail events; normalises to the unified envelope schema; applies per-source PII-redaction policy; writes to Postgres operational + DuckDB analytical stores. The deterministic heuristic engine runs against the analytical store on a schedule + on-demand; the cross-system correlator joins events by deterministic correlation keys (batch-id, sample-id, study-id, case-id) where the source-systems share a key. The workbench UI surfaces flagged events to reviewers, who triage / analyse / route to CAPA / close. **There is no AI inference at runtime.** The heuristic engine is rule-based SQL + Python predicates; the correlator is SQL join logic; both are explicit, traceable, version-controlled rules.

**Process view.** Helios.ATR runs as a 3-replica StatefulSet (Postgres) + DuckDB-on-spot-VM + per-adapter Python service (one Deployment per source-system) + workbench UI (3-replica Deployment) on K8s 1.30. Ingest cadence per source: real-time Kafka where available; daily pull where REST. Heuristic engine: on every ingest batch + nightly full-scan. Correlator: nightly + on-demand. Workbench UI: stateless; auth via Okta SAML 2.0 + MFA.

**Technology view.** Python 3.12 + FastAPI 0.115; DuckDB 1.1 (analytical); Postgres 16 (operational); Kafka 3.7 (ingest where applicable); React 18 (workbench UI); HashiCorp Vault 1.18 (secrets); Sigstore cosign 2.4; Prometheus 3.0 + Grafana 11 + Loki 3.0 (observability); Splunk Universal Forwarder 9.3 (SIEM); Trivy 0.57 + kube-bench (CI); ArgoCD 2.12 + GitLab 17 (CI/CD); Okta SAML 2.0 + MFA; SBOM CycloneDX 1.6.

**EU AI Act non-applicability declaration.** Per EU AI Act Reg. (EU) 2024/1689 Art. 3(1): an "AI system" is a machine-based system that, with varying levels of autonomy and adaptiveness after deployment, infers from input how to generate outputs that can influence physical or virtual environments. Helios.ATR's heuristic engine is **not autonomous and not adaptive** — every rule is a deterministic Boolean predicate authored by Helios QA + Validation IT, version-controlled in `gitlab.helios.local/atr-rules`, signed-off under change control. The engine does not learn from data; rules are fixed at deployment. The cross-system correlator is deterministic SQL. **Helios.ATR is therefore explicitly out of EU AI Act scope.** Should Helios in future replace any HEUR-* rule with a learned model, this DS would be amended and the system would be re-classified per the per-use-case Annex decision tree.

## 4. Software Architecture

Six layers (logical view):

1. **Ingest Plane** — Per-source-system ingest adapters; one per source (INGEST-01..08).
2. **Normalisation + Redaction Plane** — Unified-envelope normaliser; PII-redaction worker.
3. **Storage Plane** — Postgres operational store (operational queries + reviewer workflow); DuckDB analytical store (heuristic engine + correlator); S3 cold storage (≥ 25-year retention).
4. **Analytical Plane** — Deterministic heuristic-rule engine (HEUR-01..04); cross-system event correlator (EXC-01..04); priority + queue assignment (PRIO-01..03); KPI metrics (MET-01..04).
5. **Reviewer Plane** — Workbench UI; reviewer queue (REV-01..08); finding lifecycle (open → triage → analyse → CAPA → close); evidence-bundle generator.
6. **Integration Plane** — MasterControl eQMS bridge (INT-EQMS-01); ServiceNow CR bridge; SIEM forwarding (INT-SIEM-01); LMS competence; Okta SSO; cross-system Quartz AD (FS-XSYS-AD-01); cross-system Aurora Backup (FS-XSYS-BAK-01).

## 5. Module Decomposition

| Module ID | Name | Responsibility | Interface | Dependencies | Owner | GxP-criticality |
|---|---|---|---|---|---|---|
| MOD-INGEST-01 | `ingest-adapter-lims` | Caelum LIMS audit export ingest | Kafka consumer + REST poll | Caelum LIMS audit endpoint | Source-System Liaison | R1 (audit chain) |
| MOD-INGEST-02 | `ingest-adapter-mes` | Ophir MES PAS-X audit ingest | Kafka consumer | MES PAS-X | Source-System Liaison | R1 |
| MOD-INGEST-03 | `ingest-adapter-eqms` | MasterControl eQMS audit ingest | Kafka + REST | MasterControl eQMS | Source-System Liaison | R1 |
| MOD-INGEST-04 | `ingest-adapter-edc` | Medidata Rave EDC audit ingest | REST | Medidata Rave | Source-System Liaison | R1 |
| MOD-INGEST-05 | `ingest-adapter-eln` | Cyrene ELN (Benchling) audit ingest | REST + signed-file SFTP | Benchling | Source-System Liaison | R1 |
| MOD-INGEST-06 | `ingest-adapter-pv` | Sirius PV (Argus) audit ingest via Kafka `helios.ingest.sirius.argus.v1` | Kafka consumer | Sirius PV | Source-System Liaison | R1 |
| MOD-INGEST-07 | `ingest-adapter-mdr` | Theia MDR audit ingest | Kafka + REST | Theia MDR | Source-System Liaison | R1 |
| MOD-INGEST-08 | `ingest-adapter-other` | Generic adapter (vendor-supplied JSON / CSV) | REST + SFTP | per-source | Source-System Liaison | R1 |
| MOD-NORM-01 | `event-normaliser` | Unified envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}` | library | source-specific transformers | Quality IT | R1 |
| MOD-NORM-02 | `pii-redactor` | Hash-pseudonymise identifiers per per-source policy | inline middleware | per-source policy YAML | DPO + Quality IT | R1 (GDPR) |
| MOD-NORM-03 | `schema-validator` | JSON-schema validation on every event | inline | unified-envelope schema | Quality IT | R1 |
| MOD-STORE-01 | `postgres-operational` | Operational store: events + findings + reviewer state | DB | Postgres 16 | Platform Eng | R1 |
| MOD-STORE-02 | `duckdb-analytical` | Analytical store: heuristic + correlator queries | DB | DuckDB 1.1 | Platform Eng | R2 |
| MOD-STORE-03 | `s3-cold-archive` | ≥ 25-year cold retention | S3 + Glacier | S3 Object Lock | Platform Eng | R1 (retention) |
| MOD-HEUR-01 | `heur-out-of-hours-admin` | Admin action outside 08:00-18:00 local-tz reviewer queue | scheduled + on-ingest | events | Quality IT | R1 (DI heuristic) |
| MOD-HEUR-02 | `heur-back-dated-entry` | `ts_utc < entry_created_ts_utc - tolerance` | scheduled + on-ingest | events | Quality IT | R1 |
| MOD-HEUR-03 | `heur-orphan-signature` | Signature event without matching workflow-transition event | scheduled + on-ingest | events | Quality IT | R1 |
| MOD-HEUR-04 | `heur-unjustified-reverse-action` | Reverse-action without `reason_for_change` populated | scheduled + on-ingest | events | Quality IT | R1 |
| MOD-EXC-01 | `correlator-batch-id` | Cross-system join by `batch_id` (LIMS↔MES↔eQMS) | SQL job | analytical store | Quality IT | R1 (cross-system DI) |
| MOD-EXC-02 | `correlator-sample-id` | Cross-system join by `sample_id` (LIMS↔ELN) | SQL job | analytical store | Quality IT | R1 |
| MOD-EXC-03 | `correlator-study-id` | Cross-system join by `study_id` (EDC↔ELN↔CTMS) | SQL job | analytical store | Quality IT | R1 |
| MOD-EXC-04 | `correlator-case-id` | Cross-system join by `case_id` (PV↔MDR) | SQL job | analytical store | Quality IT | R1 |
| MOD-PRIO-01 | `priority-assignment` | Priority assignment per (heuristic-class × source-system × severity) | inline | per-source policy | Quality IT | R2 |
| MOD-PRIO-02 | `priority-recalculation` | Priority recalc on event update | inline | events | Quality IT | R2 |
| MOD-PRIO-03 | `priority-config` | Per-source priority config | YAML | Quality IT review | Quality IT | R2 |
| MOD-REV-01 | `reviewer-queue` | Reviewer queue with assignment + escalation | REST + UI | Postgres | Quality IT | R1 |
| MOD-REV-02 | `finding-lifecycle` | Open → Triage → Analyse → CAPA → Close | REST + UI | Postgres | Quality IT | R1 |
| MOD-REV-03 | `evidence-bundle-generator` | Per-finding evidence bundle (events + correlations + screenshots) | scheduled | Postgres + S3 | Quality IT | R1 |
| MOD-REV-04 | `reviewer-comments` | Reviewer comment thread per finding | REST + UI | Postgres | Quality IT | R2 |
| MOD-REV-05 | `assignment-engine` | Auto-assignment per reviewer-skills matrix | scheduled | LMS + Postgres | Quality IT | R2 |
| MOD-REV-06 | `escalation-engine` | SLA breach → escalate to QA Manager | scheduled | Postgres | Quality IT | R2 |
| MOD-REV-07 | `bulk-action` | Bulk-action (e.g. accept all `out-of-hours` for known maintenance window) | REST | Postgres | Quality IT | R2 |
| MOD-REV-08 | `finding-search` | Full-text + faceted search | REST | DuckDB | Quality IT | R2 |
| MOD-RT-01 | `runtime-orchestrator` | Ingest → normalise → store → heuristic → correlate → queue | scheduled + on-event | all modules | Quality IT | R1 |
| MOD-RT-02 | `kafka-orchestrator` | Kafka consumer / producer per ingest adapter | Kafka | Kafka | Platform Eng | R1 |
| MOD-RT-03 | `scheduler` | Job scheduler (cron + on-demand) | Helm | K8s CronJob | Platform Eng | R2 |
| MOD-RT-04 | `retry-policy` | Retry + dead-letter on ingest failure | library | Kafka DLQ | Platform Eng | R2 |
| MOD-AUD-01 | `audit-event-writer` | Helios.ATR's own audit trail (audit-of-the-audit-trail) | library + Postgres trigger + Splunk | Postgres | Quality IT | R1 (Part 11) |
| MOD-AUD-02 | `audit-export` | Export own audit as JSON / CSV / PDF/A-3 | REST | Postgres view | Quality IT | R2 |
| MOD-AUD-03 | `audit-volume-monitor` | Audit-event-rate Prometheus monitor | inline | Prometheus | Platform Eng | R2 |
| MOD-AUD-04 | `audit-retention` | ≥ 25-year retention | scheduled | S3 Object Lock | Platform Eng | R1 |
| MOD-AUD-05 | `audit-integrity-verify` | Periodic verify of integrity_hash_sha256 | scheduled | Postgres | Quality IT | R1 |
| MOD-AUD-WB-01 | `workbench-action-audit` | Every workbench action (view, comment, close) audit-logged | inline | MOD-AUD-01 | Quality IT | R1 |
| MOD-AUD-WB-02 | `workbench-evidence-audit` | Evidence-bundle generation audit-logged | inline | MOD-AUD-01 | Quality IT | R1 |
| MOD-MET-01 | `metric-event-count` | Per-source event-count rate | Prometheus | events | Platform Eng | R3 |
| MOD-MET-02 | `metric-finding-time-to-close` | Cycle-time | Prometheus | findings | Quality IT | R2 |
| MOD-MET-03 | `metric-heuristic-trigger-rate` | Per-heuristic trigger rate | Prometheus | findings | Quality IT | R2 |
| MOD-MET-04 | `metric-reviewer-workload` | Per-reviewer workload | Prometheus | findings | Quality IT | R2 |
| MOD-DEV-01 | `helm-deployment` | K8s deployment via Helm | Helm | K8s | Platform Eng | R2 |
| MOD-DEV-02 | `argocd-deployment` | ArgoCD GitOps | Helm | ArgoCD | Platform Eng | R2 |
| MOD-DEV-03 | `tenant-namespace-segregation` | One namespace per ingest-source (defense-in-depth) | K8s | K8s | Platform Eng | R2 |
| MOD-DEV-04 | `ci-pipeline` | Lint + unit-test + Trivy + cosign + SBOM | CI | GitLab | Platform Eng | R2 |
| MOD-DEV-05 | `cd-pipeline` | Helm + Kustomize promotion | CD | ArgoCD | Platform Eng | R2 |
| MOD-DEV-06 | `chart-versioning` | Chart.yaml version-pin | Helm | — | Platform Eng | R2 |
| MOD-DEV-07 | `dev-qc-uat-prod` | 4-env separation | K8s + Helm | — | Platform Eng | R2 |
| MOD-DEV-08 | `refresh-from-prod` | DEV/QC refresh via PII-redacted snapshot | scheduled | DLP policy | DPO + Platform Eng | R1 |
| MOD-SEC-01 | `okta-saml-mfa` | Okta SAML 2.0 + MFA | inline | Okta | IAM | R1 |
| MOD-SEC-02 | `kong-api-gateway` | Kong + Istio mTLS | Kong + Istio | K8s | Security | R1 |
| MOD-SEC-03 | `vault-secrets` | Vault per-namespace | Vault | Vault | Security | R1 |
| MOD-SEC-04 | `cis-k8s-benchmark` | CIS Kubernetes Benchmark (current release at site deployment) hardening | CI + cron | K8s | Security | R1 |
| MOD-SEC-05 | `network-policy` | NetworkPolicy default-deny | K8s | K8s | Security | R1 |
| MOD-SEC-06 | `trivy-cve-scan` | Trivy CI scan; HIGH+CRITICAL block | CI | Trivy | Security | R1 |
| MOD-INT-AD-01 | `xsys-quartz-ad` | Per FS-XSYS-AD-01 — Entra ID + Conditional Access | inline | Quartz AD | IAM | R1 |
| MOD-INT-EQMS-01 | `xsys-mastercontrol-capa` | CAPA + CR bridge | REST + Kafka | MasterControl | Quality IT | R1 |
| MOD-INT-LMS-01 | `xint-lms-competence` | Per FS-XINT-LMS-01 — competence-gated access | webhook | LMS | IAM | R2 |
| MOD-INT-SIEM-01 | `splunk-forwarder` | Per FS-INT-SIEM-01 | inline | Splunk | Quality IT | R1 |
| MOD-PERF-01..03 | `perf-suite` | P95 ingest latency ≤ 60 s; query P95 ≤ 5 s | Prometheus | — | Platform Eng | R2 |
| MOD-AV-01 | `availability` | ≥ 99.5% business hours | Prometheus | — | Platform Eng | R2 |
| MOD-BAK-01..04 | `backup-suite` | Per AUR-FS-BACKUP-001 cross-system | — | Aurora | Platform Eng | R2 |
| MOD-PR-01..03 | `periodic-review-suite` | Annual review per source + per heuristic | scheduled | all sources | Quality IT | R2 |
| MOD-TRN-01..02 | `training-suite` | LMS-gated access | Okta + LMS | — | IAM | R2 |
| MOD-PRC-01..03 | `procedural-controls` | SOPs `SOP-ATR-VAL-001`, `SOP-ATR-REVIEW-002`, `SOP-ATR-CAPA-003` | Vault QualityDocs | — | Quality IT | R1 |
| MOD-Q-01..03 | `q9-q10` | ICH Q9 + Q10 mapping | docs | — | Quality IT | R2 |
| MOD-ALC-01..02 | `alcoa-implementation` | ALCOA+ implementation reporting | scheduled | events | Quality IT | R1 |
| MOD-FDA-DI-01..02 | `fda-di-mapping` | FDA DI Q&A (Dec 2018) mapping | docs + scheduled | events | Quality IT | R2 |
| MOD-MHRA-01..02 | `mhra-di-mapping` | MHRA DI (Mar 2018) mapping | docs + scheduled | events | Quality IT | R2 |
| MOD-PICS-01..04 | `pics-pi041` | PIC/S PI 041-1 mapping | docs + scheduled | events | Quality IT | R2 |
| MOD-A11-01..02 | `annex11-mapping` | EU GMP Annex 11 §§ 4/7/9/11/12/17 mapping | docs | — | Quality IT | R2 |
| MOD-DI-01..06 | `alcoa-plus-fields` | ALCOA+ per-event field implementation | library | events | Quality IT | R1 |
| MOD-PART11-01..14 | `part11-control-suite` | Part 11 sub-section controls | library | Okta + MFA | Quality IT | R1 |
| MOD-RT-01..04 | (alias as runtime above) | — | — | — | — | — |

## 6. Data Model Design

### 6.1 `event` table (unified envelope)

```sql
CREATE TABLE event (
  event_id           UUID         PRIMARY KEY,
  source_system     TEXT         NOT NULL,
  source_record_id  TEXT         NOT NULL,
  actor             TEXT         NOT NULL,             -- normalised: Okta username, source-side id, or service-account
  ts_utc            TIMESTAMPTZ  NOT NULL,
  ts_local          TIMESTAMPTZ  NOT NULL,
  action            TEXT         NOT NULL,             -- normalised verb taxonomy
  before            JSONB,
  after             JSONB,
  reason_for_change TEXT,
  signature_id      TEXT,
  pii_redacted      BOOL         NOT NULL DEFAULT false,
  integrity_hash_sha256 CHAR(64) NOT NULL,
  ingest_ts         TIMESTAMPTZ  NOT NULL DEFAULT now(),
  helios_ack_ts     TIMESTAMPTZ                          -- helios processed (per FS-XINT-HEL-*)
);
CREATE INDEX event_source_record_idx ON event (source_system, source_record_id);
CREATE INDEX event_ts_utc_idx ON event (ts_utc);
CREATE INDEX event_actor_idx ON event (actor);
```

### 6.2 Per-source-system event-source map

```sql
CREATE TABLE source_system_map (
  source_system     TEXT         PRIMARY KEY,
  source_kind       TEXT         NOT NULL CHECK (source_kind IN ('LIMS','MES','eQMS','EDC','ELN','PV','MDR','OTHER')),
  ingest_mode       TEXT         NOT NULL CHECK (ingest_mode IN ('kafka','rest_pull','sftp_file')),
  schema_registry_url TEXT,
  pii_policy_url    TEXT,
  retention_policy_url TEXT,
  contact_owner     TEXT
);
```

### 6.3 `finding` table

```sql
CREATE TABLE finding (
  finding_id        UUID         PRIMARY KEY,
  heuristic_id      TEXT         NOT NULL,             -- HEUR-01, HEUR-02, …
  correlator_id     TEXT,                              -- EXC-01..04 if cross-system
  source_system     TEXT,
  event_ids         UUID[]       NOT NULL,             -- one-to-many events
  priority          TEXT         NOT NULL CHECK (priority IN ('high','medium','normal')),
  state             TEXT         NOT NULL CHECK (state IN ('OPEN','TRIAGE','ANALYSE','CAPA','CLOSED')),
  assigned_to       TEXT,
  opened_at         TIMESTAMPTZ  NOT NULL DEFAULT now(),
  closed_at         TIMESTAMPTZ,
  close_reason      TEXT,
  evidence_bundle_url TEXT,
  capa_id           TEXT                                 -- MasterControl link
);
```

### 6.4 `reviewer_comment` table

```sql
CREATE TABLE reviewer_comment (
  comment_id        UUID         PRIMARY KEY,
  finding_id        UUID         REFERENCES finding,
  reviewer_id       TEXT         NOT NULL,
  comment           TEXT         NOT NULL,
  comment_ts        TIMESTAMPTZ  NOT NULL DEFAULT now(),
  signature_id      TEXT
);
```

### 6.5 `audit_events` (Helios.ATR's own audit trail — append-only)

Identical pattern to other DSs; covers: ingest events, normalisation runs, heuristic runs, correlator runs, reviewer queue assignment, finding state transitions, evidence-bundle generation, workbench-action audit (login, view-event, search, comment, close).

### 6.6 Data classification + retention

| Class | Examples | Retention | Storage |
|---|---|---|---|
| GxP audit (R1) | `audit_events` | ≥ 25 y | Splunk + S3 Object Lock |
| Source-system event copy | `event` | per-source-retention-policy (max ≥ 25 y) | Postgres hot 90 d + DuckDB + S3 |
| Finding records | `finding`, `reviewer_comment` | ≥ 25 y | S3 Object Lock |
| Evidence bundles | per finding | ≥ 25 y | S3 Object Lock |
| PII-redaction salt | per-source pseudonym salt | indefinite during operation + ≥ 35 y (paediatric where applicable) | Vault HSM-backed |

## 7. Algorithm + Calculation Design

### 7.1 Heuristic rule-engine (deterministic Boolean predicates)

**HEUR-01 — Out-of-hours admin action.**

```python
def heur_out_of_hours_admin(event) -> bool:
    if event.actor.role != 'admin':
        return False
    local_hour = event.ts_local.hour
    return local_hour < 8 or local_hour >= 18
```

**HEUR-02 — Back-dated entry.**

```python
def heur_back_dated_entry(event, tolerance=timedelta(seconds=60)) -> bool:
    if event.action != 'CREATE' and event.action != 'EDIT':
        return False
    return event.ts_utc < event.ingest_ts - tolerance
```

**HEUR-03 — Orphan signature.**

```python
def heur_orphan_signature(event, peer_events) -> bool:
    if event.action != 'SIGN':
        return False
    matching_transitions = [
      e for e in peer_events
      if e.source_record_id == event.source_record_id
         and e.action in ('APPROVE','SUBMIT','RELEASE')
         and abs((e.ts_utc - event.ts_utc).total_seconds()) < 60
    ]
    return len(matching_transitions) == 0
```

**HEUR-04 — Un-justified reverse action.**

```python
def heur_unjustified_reverse_action(event) -> bool:
    if event.action != 'REVERSE':
        return False
    return event.reason_for_change is None or event.reason_for_change.strip() == ''
```

All four heuristics are pure functions over event fields — no learned parameters, no statistical inference, no probabilistic threshold (all thresholds are explicit constants). Tunable thresholds (e.g. HEUR-01 hours, HEUR-02 tolerance) are version-controlled in `gitlab.helios.local/atr-rules` under CR.

### 7.2 Cross-system event-correlation

```sql
-- EXC-01: Cross-system batch-id correlation
CREATE OR REPLACE VIEW exc_batch_correlation AS
SELECT
  e_lims.event_id   AS lims_event_id,
  e_mes.event_id    AS mes_event_id,
  e_eqms.event_id   AS eqms_event_id,
  e_lims.before->>'batch_id' AS batch_id,
  e_lims.ts_utc     AS lims_ts,
  e_mes.ts_utc      AS mes_ts,
  e_eqms.ts_utc     AS eqms_ts,
  ABS(EXTRACT(EPOCH FROM (e_lims.ts_utc - e_mes.ts_utc))) AS lims_mes_delta_s,
  ABS(EXTRACT(EPOCH FROM (e_mes.ts_utc - e_eqms.ts_utc))) AS mes_eqms_delta_s
FROM event e_lims
JOIN event e_mes ON e_lims.before->>'batch_id' = e_mes.before->>'batch_id'
                AND e_mes.source_system = 'MES'
JOIN event e_eqms ON e_lims.before->>'batch_id' = e_eqms.before->>'batch_id'
                  AND e_eqms.source_system = 'eQMS'
WHERE e_lims.source_system = 'LIMS'
  AND e_lims.action IN ('APPROVE','RELEASE');
```

EXC-02 / EXC-03 / EXC-04 are analogous (sample-id, study-id, case-id). All correlator output is **deterministic SQL** — no learned weights.

### 7.3 Priority + queue assignment

```python
def priority(finding) -> str:
    heuristic_severity = SEVERITY_MAP[finding.heuristic_id]      # config table
    source_severity = SOURCE_SEVERITY_MAP[finding.source_system]  # config table
    is_cross_system = finding.correlator_id is not None
    score = heuristic_severity + source_severity + (3 if is_cross_system else 0)
    if score >= 8: return 'high'
    if score >= 4: return 'medium'
    return 'normal'
```

### 7.4 Integrity-hash calculation

`integrity_hash_sha256` = SHA-256 over canonical-JSON of `{event_id, source_system, source_record_id, actor, ts_utc, action, before, after, reason}` plus a per-source HMAC key (Vault-stored). Verified at every read.

### 7.5 PII-redaction (deterministic per-source policy)

Per-source `pii_policy_url` YAML lists field paths to hash + hash algorithm (default SHA-256 with per-source salt). Redaction is deterministic — same input always produces same hash, enabling cross-system correlation while preserving privacy.

### 7.6 Evidence-bundle generation

Per finding: render PDF/A-3 containing the finding metadata + all linked events + cross-system correlation results + screenshots from source-system workbench (where source allows) + reviewer-comment history.

## 8. Interface + API Design

| Endpoint | Method | Path | AuthN | Request | Response | Rate limit | Errors | Audit |
|---|---|---|---|---|---|---|---|---|
| Ingest event (push) | POST | `/ingest/{source_system}` | mTLS (per-source) | event envelope JSON | `Ack` | per-source | 401, 400, 409 dup | EVENT_INGESTED |
| Trigger heuristic run | POST | `/heuristic/{heur_id}/run` | OAuth2 + QA group | `{from_ts, to_ts}` | `{findings_created: N}` | 10/d | 400, 403 | HEURISTIC_RUN |
| Trigger correlator run | POST | `/correlator/{exc_id}/run` | OAuth2 + QA group | `{from_ts, to_ts}` | `{correlations: N}` | 10/d | 400 | CORRELATOR_RUN |
| Finding list | GET | `/finding?state=&priority=&heuristic=` | OAuth2 + QA group | — | `[Finding]` | 100/h | 403 | — |
| Finding detail | GET | `/finding/{id}` | OAuth2 + QA group | — | `Finding + events + correlations` | 100/h | 404 | FINDING_VIEWED |
| Finding triage | POST | `/finding/{id}/triage` | OAuth2 + QA group | `{notes}` | `Finding` | 100/h | 400 | FINDING_TRIAGED |
| Finding analyse | POST | `/finding/{id}/analyse` | OAuth2 + QA group | `{notes, evidence_refs[]}` | `Finding` | 100/h | 400 | FINDING_ANALYSED |
| Finding CAPA-create | POST | `/finding/{id}/capa` | OAuth2 + QA group | `{capa_payload}` | `{capa_id (MasterControl)}` | 50/d | 400 | CAPA_CREATED |
| Finding close | POST | `/finding/{id}/close` | OAuth2 + QA Manager | `{reason}` | `Finding` | 100/h | 400, 403 | FINDING_CLOSED |
| Reviewer assign | POST | `/finding/{id}/assign` | OAuth2 + QA Manager | `{reviewer_id}` | `Finding` | 100/h | 400 | FINDING_ASSIGNED |
| Comment | POST | `/finding/{id}/comment` | OAuth2 + QA group | `{comment}` | `Comment` | 200/h/reviewer | 400 | COMMENT_RECORDED |
| Evidence-bundle generate | POST | `/finding/{id}/evidence-bundle` | OAuth2 + QA group | — | `{bundle_url, sha256}` | 50/d | 400 | EVIDENCE_GENERATED |
| Search | GET | `/search?q=&from=&to=&source=` | OAuth2 + QA group | — | `[Finding]` | 200/h | — | SEARCH_PERFORMED |
| Audit export | GET | `/audit/export?from=&to=&format=` | OAuth2 + Audit-Readers | — | streaming | 1/h | 400 | AUDIT_EXPORTED |
| Helios.ATR own-audit | GET | `/audit/own?from=&to=` | OAuth2 + Audit-Readers | — | streaming | 1/h | 400 | OWN_AUDIT_EXPORTED |
| Heuristic config get | GET | `/heuristic/{id}/config` | OAuth2 + QA group | — | `HeuristicConfig` | 100/h | 404 | — |
| Heuristic config update | PUT | `/heuristic/{id}/config` | OAuth2 + 2 JWTs (Author ≠ Approver) | `HeuristicConfig` | `HeuristicConfig` | 5/d | 400, 403 | HEURISTIC_CONFIG_CHANGED |

TLS 1.3 + Istio mTLS service-to-service.

## 9. Security Design

### 9.1 AuthN

Okta SAML 2.0 + MFA; per-source ingest via mTLS. FIDO2 phishing-resistant for `atr-qa-managers`. Service-to-service mTLS via Istio.

### 9.2 AuthZ

RBAC: `qa_reviewer`, `qa_manager` (close + assign), `auditor_readonly`, `source_system_liaison` (per-source ingest), `csv_admin`, `csv_approver` (heuristic config — SoD enforced).

### 9.3 Secrets

Vault: per-source mTLS cert, per-source HMAC key (for integrity hash), per-source PII-redaction salt (HSM-backed), MasterControl + Splunk + Kafka credentials.

### 9.4 Transport security

TLS 1.3; Istio mTLS. AES-256 at rest (Postgres + DuckDB + S3 + Splunk). SBOM CycloneDX + Trivy CI block on HIGH+CRITICAL.

### 9.5 Integrity protection

Every event carries `integrity_hash_sha256` over canonical-JSON + per-source HMAC. Periodic verify job (MOD-AUD-05) re-computes hashes and alerts on mismatch. DB triggers block UPDATE/DELETE on `audit_events`.

### 9.6 Data-egress restrictions

NetworkPolicy `helios-atr-egress-deny-source-systems-except-via-ingest-adapters` — no tenant pod may reach source-system endpoints except via the named ingest-adapter Deployment.

## 10. Deployment Architecture

### 10.1 K8s topology

K8s 1.30 across 3 AZs (Frankfurt). Namespaces: `helios-atr-ingest`, `helios-atr-store`, `helios-atr-analytics`, `helios-atr-workbench`, `helios-atr-observe`. Pod Security `restricted`. CIS Kubernetes Benchmark (current release at site deployment). HPA on workbench (4-16 replicas on req-per-sec).

### 10.2 Storage

Postgres 16: 3-node patroni HA. DuckDB: spot-VM analytical worker pool. S3 Object Lock + Glacier Vault Lock for ≥ 25-year retention.

### 10.3 Observability

Prometheus + Grafana + Loki + Tempo. Metrics: `ingest_lag_seconds`, `event_count_per_source`, `finding_creation_rate`, `finding_time_to_close_seconds`, `heuristic_trigger_rate`, `reviewer_workload`. Splunk Universal Forwarder `helios-atr-audit`.

### 10.4 DR + retention

RTO ≤ 4 h; RPO ≤ 1 h. Cross-system per AUR-FS-BACKUP-001. Quarterly partial DR + annual full DR.

### 10.5 CI/CD

GitLab + ArgoCD. Signed commits; 2-reviewer review; CI: lint + unit-test + Trivy + cosign + SBOM; ArgoCD-managed Helm.

## 11. Module Specification Table

(Excerpt — ~110 modules)

| Module ID | File path | Class | Unit-test | Module Spec |
|---|---|---|---|---|
| MOD-INGEST-01 | `services/ingest/lims.py` | `LIMSIngestAdapter` | `tests/test_lims.py` | HBS-MS-ATR-LIMS-001 |
| MOD-NORM-01 | `services/normaliser/main.py` | `EventNormaliser` | `tests/test_norm.py` | HBS-MS-ATR-NORM-001 |
| MOD-HEUR-01 | `services/heuristic/out_of_hours.py` | `OutOfHoursAdminHeuristic` | `tests/test_heur_01.py` | HBS-MS-ATR-HEUR-OOH-001 |
| MOD-HEUR-02 | `services/heuristic/back_dated.py` | `BackDatedEntryHeuristic` | `tests/test_heur_02.py` | HBS-MS-ATR-HEUR-BD-001 |
| MOD-HEUR-03 | `services/heuristic/orphan_signature.py` | `OrphanSignatureHeuristic` | `tests/test_heur_03.py` | HBS-MS-ATR-HEUR-ORPH-001 |
| MOD-HEUR-04 | `services/heuristic/unjustified_reverse.py` | `UnjustifiedReverseHeuristic` | `tests/test_heur_04.py` | HBS-MS-ATR-HEUR-UR-001 |
| MOD-EXC-01 | `services/correlator/batch_id.py` | `BatchIDCorrelator` | `tests/test_exc_01.py` | HBS-MS-ATR-EXC-BATCH-001 |
| MOD-REV-02 | `services/finding/lifecycle.py` | `FindingLifecycle` | `tests/test_lifecycle.py` | HBS-MS-ATR-LIFECYCLE-001 |
| MOD-AUD-01 | `services/audit/writer.py` | `AuditEventWriter` | `tests/test_audit.py` | HBS-MS-ATR-AUDIT-001 |
| MOD-AUD-05 | `services/audit/integrity_verify.py` | `IntegrityVerifyJob` | `tests/test_integrity.py` | HBS-MS-ATR-INTEGRITY-001 |
| MOD-INT-EQMS-01 | `services/integration/mastercontrol.py` | `MasterControlBridge` | `tests/test_eqms.py` | HBS-MS-ATR-EQMS-001 |
| (… plus ~100 more) | (…) | (…) | (…) | (…) |

## 12. References

**US**
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- **21 CFR Part 211 §§ .68 (automatic equipment), .180 (general requirements for records), .192 (production-record review)**
- **FDA Data Integrity and Compliance With Drug CGMP — Questions and Answers (Dec 2018)**
- FDA *Computer Software Assurance for Production and Quality Management System Software* (Feb 2026)
- NIST SP 800-218 SSDF; NIST SP 800-53

**EU**
- EU GMP Eudralex Vol 4 (Parts I + II)
- EU GMP Annex 11 §§ 4 (validation), 7 (data storage), 9 (audit trail), 11 (periodic review), 12 (security), 17 (archiving)
- GDPR Reg. (EU) 2016/679 Arts. 6, 32, 35

**International**
- **PIC/S PI 041-1 (1 July 2021) — Good Practices for Data Management and Integrity**
- **MHRA GxP Data Integrity Guidance (March 2018)**
- WHO TRS 996 Annex 5 — Guidance on good data and record management practices
- ICH Q9(R1); ICH Q10
- ISO/IEC 27001:2022
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE GAMP Records and Data Integrity (RDI) Good Practice Guide
- OWASP ASVS v5.0; OWASP API Security Top 10 (2023)

**DACH**
- BfArM (DE) — GxP DI inspection focus
- BSI IT-Grundschutz

**Vendor**
- DuckDB documentation (v1.1)
- Postgres documentation (v16)
- Kafka documentation (v3.7)
- Helm + Kustomize + ArgoCD documentation
- Vault + Sigstore + cosign documentation
- Okta SAML 2.0 + MFA Administrator Guide
- Splunk Universal Forwarder 9.3 documentation

## 13. Appendix A — DS → FS Traceability Matrix

| DS ID / Module | FS ID |
|---|---|
| MOD-INGEST-01..08 | FS-INGEST-01..08 |
| MOD-NORM-01..03 | (subsumed) |
| MOD-STORE-01..03 | FS-PERF-01, FS-AV-01 |
| MOD-HEUR-01..04 | FS-HEUR-01, FS-HEUR-02, FS-HEUR-03, FS-HEUR-04 |
| MOD-EXC-01..04 | FS-EXC-01, FS-EXC-02, FS-EXC-03, FS-EXC-04 |
| MOD-PRIO-01..03 | FS-PRIO-01, FS-PRIO-02, FS-PRIO-03 |
| MOD-REV-01..08 | FS-REV-01..08 |
| MOD-RT-01..04 | FS-RT-01..04 |
| MOD-AUD-01..05 | FS-AUD-01..05 |
| MOD-AUD-WB-01..02 | FS-AUD-WB-01, FS-AUD-WB-02 |
| MOD-MET-01..04 | FS-MET-01..04 |
| MOD-DEV-01..08 | FS-DEV-01..08 |
| MOD-SEC-01..06 | FS-SEC-01..06 |
| MOD-INT-AD-01 | FS-INT-AD-01, FS-XSYS-AD-01 |
| MOD-INT-EQMS-01 | FS-INT-EQMS-01 |
| MOD-INT-LMS-01 | FS-INT-LMS-01, FS-XINT-LMS-01 |
| MOD-INT-SIEM-01 | FS-INT-SIEM-01 |
| MOD-PERF-01..03 | FS-PERF-01..03 |
| MOD-AV-01 | FS-AV-01 |
| MOD-BAK-01..04 | FS-BAK-01..04, FS-XSYS-BAK-01 |
| MOD-PR-01..03 | FS-PR-01..03 |
| MOD-TRN-01..02 | FS-TRN-01..02 |
| MOD-PRC-01..03 | FS-PRC-01..03 |
| MOD-Q-01..03 | FS-Q-01..03 |
| MOD-ALC-01..02 | FS-ALC-01..02 |
| MOD-FDA-DI-01..02 | FS-FDA-DI-01..02 |
| MOD-MHRA-01..02 | FS-MHRA-01..02 |
| MOD-PICS-01..04 | FS-PICS-01..04 |
| MOD-A11-01..02 | FS-A11-01..02 |
| MOD-DI-01..06 | FS-DI-01..06 |
| MOD-PART11-01..14 | FS-PART11-01..14 |

**Coverage footnote.** 110 of 114 FS-IDs covered. Vendor-internal FS-IDs not designed at site level: DuckDB query-engine internals, Postgres internals (vendor SDLC), per-source audit-trail-export internal formats.

## 14. Design-level Risk Register

| ID | Design-stage risk | Likelihood | Impact | Bound modules | Mitigation |
|---|---|---|---|---|---|
| **D-AI-00** | **EU AI Act non-applicability assumption invalidated** — future replacement of any HEUR-* rule with a learned model without re-classification triggers Annex I non-conformance | Low | **Critical (Art. 99)** | MOD-HEUR-01..04 | Annual classification reassessment (MOD-PR-03 + § 3 declaration); CR check on any HEUR-* change; this DS amended on first ML introduction |
| D-01 | Source-system event-export schema change silently breaks `MOD-NORM-01` | Medium | High | MOD-NORM-01..03 | Schema-registry pinning + version-controlled per-source transformers; CI breakage on schema drift |
| D-02 | Per-source PII-redaction policy drift — over- or under-redaction | Medium | High | MOD-NORM-02 | Per-source policy review annually; DPO sign-off on changes |
| D-03 | Heuristic-rule false-negative — DI failure missed | Medium | High | MOD-HEUR-01..04 | Annual review of heuristics against latest FDA/PIC/S/MHRA DI guidance; OQ regression |
| D-04 | Heuristic-rule false-positive overwhelms reviewer queue | Medium | Medium | MOD-HEUR-01..04 + MOD-PRIO-* | Priority tuning + bulk-action for known patterns + quarterly KPI review |
| D-05 | Cross-system correlator silently misses an event due to missing batch-id / sample-id / study-id / case-id field | Medium | High | MOD-EXC-01..04 | Per-source schema mapping validation + correlator coverage metrics |
| D-06 | Helios.ATR's own audit-trail (MOD-AUD-WB-*) bypass | Low | Critical | MOD-AUD-01 + MOD-AUD-WB-01..02 | DB-role enforcement; periodic integrity verify (MOD-AUD-05) |
| D-07 | Integrity-hash key compromise | Low | Critical | Vault | HSM-backed; rotation 90 d; audit |
| D-08 | DB-trigger bypass for `audit_events` mutation | Low | Critical | MOD-AUD-01 | DB-role enforcement |
| D-09 | Ingest-adapter throughput too low → ingest-lag accumulates | Medium | Medium | MOD-INGEST-01..08 | Kafka back-pressure handling + adapter horizontal scaling |
| D-10 | Reviewer-assignment SLA breach during volume spike | Medium | Medium | MOD-REV-06 | Escalation engine + QA Manager dashboard |
| D-11 | MasterControl CAPA bridge outage | Low | High | MOD-INT-EQMS-01 | Local CAPA-queue buffer + retry policy |
| D-12 | DR drill misses a source-system | Low | High | MOD-BAK-* | Per-source checklist coverage |
| D-13 | LMS competence lapse blocks legitimate reviewer | Low | High | MOD-INT-LMS-01 | D-30 / D-7 lapse alert |
| D-14 | Storage cost overrun on 25-y retention | Low | Critical | MOD-STORE-03 | Annual storage-cost review + Vault QA sign-off |
| D-15 | Source-system-clock skew (NTP drift) corrupts back-dated-entry heuristic | Medium | High | MOD-HEUR-02 | Per-source NTP-drift monitor; tolerance config per-source |
| D-16 | Splunk forwarder lag > 5 min | Medium | Medium | MOD-INT-SIEM-01 | Lag alert + buffer policy |
| D-17 | Cross-system Quartz AD conditional-access misconfiguration blocks QA reviewer | Low | High | MOD-INT-AD-01 | Break-glass via CyberArk PAM per FS-XSYS-AD-01 |
| D-18 | Cross-system Aurora Backup retention drift (S3 Object Lock transition) | Low | High | MOD-BAK-01..04 | Monthly QA-witnessed restore + retention monitor |
| D-19 | Evidence-bundle generator produces incomplete bundle | Low | High | MOD-REV-03 | Bundle integrity check + manifest SHA-256 |
| D-20 | Workbench session-hijack | Low | High | MOD-PART11-* | Re-auth on every state-transition (OAuth2 max-age 5 min) |
| D-21 | PII-redaction salt rotation breaks deterministic cross-source correlation | Low | High | MOD-NORM-02 | Salt rotation as planned migration (no rolling rotation); CR-controlled |
| D-22 | Schema-validator `MOD-NORM-03` rejects valid event due to source-system minor version bump | Medium | Medium | MOD-NORM-03 | Lenient-validation mode + post-ingest reconciliation |
| D-23 | Helios.ATR own-audit retention not separately enforced from source-system event retention | Low | Critical | MOD-AUD-04 | Separate retention class for own audit |
| D-24 | Per-source mTLS cert expiry missed | Low | Critical | Vault | Cert-expiry monitor D-30 alert |
| D-25 | DuckDB long-running query OOMs node | Medium | Medium | MOD-STORE-02 | Query timeout + memory limits + dead-query monitor |
| D-26 | Annual heuristic-config review misses regulatory update (e.g. new MHRA DI guidance) | Low | High | MOD-PR-01 + MOD-PR-02 + MOD-PR-03 | Annual checklist mapped to current FDA/PIC/S/MHRA/Annex11 DI guidance |
| D-27 | Source-system ingest sees burst (10× normal) and overflows Postgres | Low | Medium | MOD-RT-04 | Rate-limit per adapter + back-pressure |
| D-28 | Reviewer's QA Manager bulk-action accepts findings without per-finding rationale | Low | High | MOD-REV-07 | Bulk-action requires rationale + audit row |
| D-29 | Source-system clock drift across source-systems makes cross-system correlation unreliable | Medium | High | MOD-EXC-01..04 + MOD-HEUR-02 | Per-source NTP drift dashboard + correlation-tolerance config |
| D-30 | Workbench full-text search exposes PII bypassing redaction layer | Low | High | MOD-REV-08 | Search-time redaction overlay + DPO-approved search-index design |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
