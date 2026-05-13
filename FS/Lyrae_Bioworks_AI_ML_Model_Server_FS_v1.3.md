---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (FS catch-up to v1.1 URS); enriched 2026-05-12 Wave 3 Chunk I (Annex I 2027 re-classification + new URS-IDs)"
seed_corpus_basis:
  - "LYR-URS-MLSRV-001 v1.2"
  - "GAMP 5 (2nd ed., 2022) Cat 5"
  - "21 CFR Part 11"
  - "ICH Q9(R1)"
  - "FDA AI/ML SaMD Action Plan; FDA PCCP (Aug 2025); FDA GMLP (2021)"
  - "EU AI Act 2024/1689 (Annex I high-risk)"
  - "ISO/IEC 42001:2023; NIST AI RMF 1.0"
parent_urs:
  document_number: LYR-URS-MLSRV-001
  version: 1.2
  file: ../../URS/_generated/final/AI_ML_Model_Server_GxP__Lyrae_Bioworks_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# Functional Specification (FS)

## AI / ML Model Server (GxP Inference Service) — Site-Developed FastAPI on K8s + MLflow + Seldon Core + NVIDIA Triton

**Document Number:** LYR-FS-MLSRV-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** LYR-URS-MLSRV-001 v1.2 | **Site:** Lyrae Bioworks GmbH, München, Germany *(fictional)*
**System Class:** GAMP Cat 5 — Custom Application
**EU AI Act 2024/1689 classification:** **Annex I high-risk AI system** (safety component of regulated medicinal-product / medical-device decisions). Compliance deadline **2 August 2027**. Conformity-assessment pathway Annex VII (notified-body) where the underlying product is MDR class IIa+.
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11; EU GMP Annex 22 (DRAFT); ICH Q9(R1); ICH Q14; EU AI Act 2024/1689 Arts. 8–21, 26, 43, 47, 48, 49, 72, 73, 99, 113; EU MDR 2017/745 (where applicable); GDPR Arts. 6, 9, 22, 32, 35; FDA AI/ML SaMD Action Plan (2021); FDA PCCP (August 2025); FDA GMLP (2021); FDA CSA (February 2026); ISPE GAMP GPG *AI/ML in GxP* (2024); ISO/IEC 42001:2023; ISO/IEC 23053; NIST AI RMF 1.0; EMA *Reflection Paper on AI in the Medicinal Product Lifecycle* (2024); BfArM (DE); Swissmedic (CH); AGES (AT).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of AI Engineering Platforms) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (InfoSec) | _____________ | _____________ | _____ |
| Reviewer (Reg Affairs — AI/ML) | _____________ | _____________ | _____ |
| Reviewer (Notified Body Liaison) | _____________ | _____________ | _____ |
| Reviewer (Data Protection Officer) | _____________ | _____________ | _____ |
| Approver (VP AI / Data Science) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |
| Approver (VP Regulatory Affairs) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.1: EU AI Act Arts. 9–17 implementations; Human Oversight controls; PCCP via FDA Aug 2025; expanded Part 11 sub-section bindings; ALCOA+ implementation detail; Art. 15 cybersecurity hardening; DACH context. |
| 1.2 | 2026-05-12 | (synthetic) | Wave 3 Chunk I enrichment: parent URS upgraded to v1.2. EU AI Act re-classified Annex I (2 Aug 2027). New FS rows for URS-PLAT-06/07, URS-MOD-06/07, URS-AB-01..05, URS-FS-01..04, URS-PCCP-01..04, URS-INF-06/07, URS-HO-05/06, URS-LOG-01..04, URS-IFU-01..03, URS-ROB-01..05, URS-TD-01..03, URS-RET-01..02, URS-CONF-01..04, URS-REG-01..02, URS-PMM-01..03, URS-INC-01..04, URS-DEP-01..03, URS-QMS-01..03, URS-PART11-09..12, URS-DI-08, URS-INT-FEAST-01, URS-INT-TRITON-01, URS-INT-EUDAMED-01, URS-PERF-05, URS-OBS-01..03, URS-BAK-05, URS-SEC-07, URS-CONF-DEF-01..03, URS-CARD-01..02, URS-TRN-04, URS-AUD-06, URS-PR-04. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies the implementation of the AI/ML Model Server to satisfy the user requirements in `LYR-URS-MLSRV-001` v1.2. The platform is an **Annex I high-risk AI system** under EU AI Act 2024/1689 — implementation must satisfy Arts. 8–21 (provider duties, risk-mgmt, data governance, technical documentation, logging, transparency, human oversight, accuracy + robustness + cybersecurity, QMS, retention), Arts. 26 (deployer obligations), 43+47+48 (conformity + CE + DoC), 49 (EU database), 72 (PMM), 73 (incident reporting), 99 (penalty awareness).

## 2. Scope

Site-developed FastAPI services on K8s; MLflow model registry (3-node HA); Seldon Core deployment with Istio service mesh; NVIDIA Triton Inference Server for GPU-accelerated workloads; Feast feature store; integrations with validated GitLab (model artefact source), Splunk SIEM (audit forwarding), Postgres metadata store (HA pair), consumer GxP systems via site API Gateway with mTLS, HashiCorp Vault (secrets), Okta SSO + MFA, GDPR Art. 35 DPIA registry, EUDAMED (where SaMD), Notified Body interface.

## 3. System Architecture

```
   GitLab (signed tags) ──► MLflow Registry (HA) ──► Signed Model Artefact Store (Sigstore)
                                       │
                                       ▼
                              Seldon Core (K8s, Istio mesh)
                              ├─ NVIDIA Triton Inference Server (GPU)
                              ├─ FastAPI inference service (CPU)
                              │  CIS K8s benchmark hardened
                              │  Pod Security Standards: restricted
                              ▼
                       Per-model inference path
                       ├─ Confidence-threshold gate
                       ├─ Drift monitor (data / concept / prediction)
                       ├─ Adversarial-input anomaly detector
                       ├─ Output-hash + confidentiality post-processing
                       │  mTLS via site API Gateway
                       ▼
              ┌────────────────────────────┐
              │  Consumer GxP systems       │  (deployers per Art. 26)
              │  Human Oversight Operator   │  (Art. 14 monitoring + halt)
              │  PMM Operator               │  (Art. 72 monitoring + Art. 73 escalation)
              └────────────────────────────┘
                       │
                       ├─► Splunk SIEM (Art. 12 ≥ 6 mo hot, Art. 18 ≥ 10 y cold)
                       │
                       ├─► BfArM / Swissmedic / AGES (Art. 73 incident reporting)
                       │
                       ├─► EUDAMED + EU AI database (Art. 49 registration where applicable)
                       │
                       └─► Notified Body interface (Art. 43 conformity assessment)

   Feast feature store ◄─► MLflow model records (feature-snapshot pinning)
```

## 4. Functional Specifications

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | K8s 1.30 control plane + worker nodes across 3 AZs; etcd quorum; cluster-API readiness probes; RTO ≤ 4 h validated via DR drill; RPO ≤ 15 min via async etcd backup. |
| FS-PLAT-02 | URS-PLAT-02 | Patching pipeline: critical CVE → 7 d, high → 30 d, others → 90 d; tracked in Jira board with change-management approval. |
| FS-PLAT-03 | URS-PLAT-03 | Dedicated VLAN `vlan-mlinf-prod`; mTLS via Istio service mesh; mutual cert validation enforced by Envoy sidecar. |
| FS-PLAT-04 | URS-PLAT-04 | Site SDLC: signed commits in GitLab; mandatory 2-reviewer code review; CI/CD pipeline with GitLab → ArgoCD → K8s; signed container images via cosign. |
| FS-PLAT-05 | URS-PLAT-05 | Prometheus metrics: `inference_latency_seconds`, `inference_error_rate`, `drift_score`, `auth_failures_total`, `model_confidence_below_threshold`. |
| FS-PLAT-06 | URS-PLAT-06 | NVIDIA driver-version pinning via DaemonSet manifest under git change control; pre-deployment admission webhook blocks GPU node admission if driver-SHA does not match pinned manifest. |
| FS-PLAT-07 | URS-PLAT-07 | DCGM exporter publishes per-GPU `nvidia_gpu_duty_cycle`, `nvidia_gpu_memory_used_bytes`, `triton_queue_depth_per_model`; surfaced in Grafana capacity-planning board. |
| FS-MOD-01 | URS-MOD-01 | MLflow `models` table extended schema: `training_data_hash` (SHA-256), `training_code_git_tag`, `hyperparameters_json`, `evaluation_metrics_json`, `validation_report_url`, `intended_use_statement`, `gxp_classification_flag`, `eu_aiact_classification` (`annex_i` / `annex_iii` / `non_high_risk`), `annex_iv_pack_url`. |
| FS-MOD-02 | URS-MOD-02 | State machine in MLflow with DB-enforced state transitions: DRAFT → REVIEW → APPROVED → EFFECTIVE-CHALLENGER → EFFECTIVE-CHAMPION → DEPRECATED → RETIRED. Out-of-order transitions raise 4xx. |
| FS-MOD-03 | URS-MOD-03 | Deployment endpoint requires two signed JWTs (Author ≠ Approver) plus a cosign-verified model-artefact signature; signature verification implemented via Sigstore. |
| FS-MOD-04 | URS-MOD-04 | PCCP record per model (FDA Aug 2025 AI-Enabled Device Software Functions) linked from MLflow; allowed-update predicate engine checks each model update against the approved PCCP rules; non-conformant updates auto-block. |
| FS-MOD-05 | URS-MOD-05 | EU AI Act Art. 11 + Annex IV Technical Documentation pack stored in S3-bucket `lyr-aiact-techdoc/`; MLflow record carries pointer; pack includes Art. 9 risk-mgmt + Art. 10 data-governance + Art. 15 testing-evidence + Art. 13 IFU + model-card subfolders. |
| FS-MOD-06 | URS-MOD-06 | Training-data lineage: each MLflow run records `feast_snapshot_version`, `raw_data_sha256`, `labelling_protocol_version`, and `bias_evidence_url`; lineage reproducible via documented `data-pipeline.py` script under version control. |
| FS-MOD-07 | URS-MOD-07 | Retirement workflow: state transition to RETIRED triggers archival job to `lyr-archive/` cold storage (10 y retention enforced via S3 Object Lock + Glacier Vault Lock); inference logs retention extended to 10 y; MLflow registry record marked `RETIRED` with retention indefinite. |
| FS-AB-01 | URS-AB-01 | Seldon traffic-split default `champion: 100%, challenger: shadow` for new Challengers; shadow mode replicates inference requests without affecting consumer responses. |
| FS-AB-02 | URS-AB-02 | Promotion-criteria record `promotion_criteria.yaml` in MLflow per model: `min_traffic_volume`, `significance_threshold`, `safety_metric_bounds`; values frozen pre-deployment via change-control sign-off. |
| FS-AB-03 | URS-AB-03 | Traffic-split changes via `POST /model/{id}/traffic` require two signed JWTs (Author ≠ Approver) + QA group membership; payload audit-logged with old → new percentages. |
| FS-AB-04 | URS-AB-04 | Inference-log schema carries `served_by_model_version`; aggregation views in Grafana partition by Champion vs Challenger. |
| FS-AB-05 | URS-AB-05 | Auto-rollback watcher monitors safety-metric breach; on breach triggers `POST /model/{id}/rollback` with `reason: AUTO_SAFETY_BREACH`; audit-logged with metric values. |
| FS-FS-01 | URS-FS-01 | Feast feature store backed by Postgres offline + Redis online; canonical feature definitions in git-versioned `features.yaml`; point-in-time correctness enforced by Feast `materialize-incremental`. |
| FS-FS-02 | URS-FS-02 | Feature-definition schema: `feature_name`, `version`, `sha256`, `schema_json`, `source_of_truth_url`, `freshness_sla_seconds`, `bias_evidence_url`. |
| FS-FS-03 | URS-FS-03 | Feature mutations require change-control PR with peer review; new feature versions are additive; downstream models pin via `feast_snapshot_version` (URS-MOD-06). |
| FS-FS-04 | URS-FS-04 | Feature-drift monitor publishes `feature_drift_score` per feature per hour; alerts route to `feature-owners` Slack channel. |
| FS-PCCP-01 | URS-PCCP-01 | PCCP record schema enforces MoP + PCEM + IA fields per FDA Aug 2025 guidance; record stored in MLflow `pccp/` namespace. |
| FS-PCCP-02 | URS-PCCP-02 | `pccp_predicate_engine` v1.0 evaluates each model update against the PCCP envelope (delta in hyperparameters, training-data composition, architecture); non-conformant updates return `PCCP_OUT_OF_ENVELOPE` and block promotion. |
| FS-PCCP-03 | URS-PCCP-03 | PCCP deviations open a `pccp_deviation` record + trigger Art. 43(4) substantial-modification assessment workflow; Reg Affairs notified. |
| FS-PCCP-04 | URS-PCCP-04 | PCCP envelope reviewed annually as part of `FS-PR-01` periodic review; envelope changes require Reg-Affairs + VP-QA sign-off. |
| FS-INF-01 | URS-INF-01 | Inference log schema (JSON): `request_id`, `consumer_id`, `model_id`, `model_version`, `input_checksum_sha256`, `output`, `latency_ms`, `timestamp_iso8601`, `confidence`. Stored in Postgres + forwarded to Splunk. Retention ≥ 25 y for clinical-impact models. |
| FS-INF-02 | URS-INF-02 | Drift monitor: per-model PSI / KS-test / chi-square (data drift); concept-drift via canary-label evaluation when labels available; prediction drift via output-distribution shift; drift_score > threshold raises Splunk alert + flips model state in MLflow to `DRIFT_FLAGGED`. |
| FS-INF-03 | URS-INF-03 | Seldon traffic split (% champion / % challenger); change requires two signed JWTs (Author ≠ Approver) + QA co-approval. Change audit-logged with old → new percentages. |
| FS-INF-04 | URS-INF-04 | Structured error codes: `MODEL_UNAVAILABLE`, `SCHEMA_MISMATCH`, `INFERENCE_TIMEOUT`, `DRIFT_BLOCK`, `LOW_CONFIDENCE`, `PCCP_OUT_OF_ENVELOPE`, `ADVERSARIAL_SUSPECTED`. Consumer SDK throws typed exceptions; no fallback to null in client. |
| FS-INF-05 | URS-INF-05 | Per-model confidence-threshold table; outputs below threshold returned with `LOW_CONFIDENCE` flag; consumer must explicitly accept before downstream consumption. |
| FS-INF-06 | URS-INF-06 | Each inference response carries `output_hash` = SHA-256 over the canonical JSON of `output` field; consumer-side SDK verifies hash on receive. |
| FS-INF-07 | URS-INF-07 | Batch endpoint `POST /model/{id}/batch` accepts `batch_size`, `parallelism`, `per_call_timeout_ms`; batch fails atomically on any sub-call failure with structured per-record error list. |
| FS-HO-01 | URS-HO-01 | Human Oversight Operator UI: Grafana dashboard `aiact-ho-monitor` with real-time inference rate, drift indicator, error rate, model-version-in-production per consumer, confidence-distribution histogram. |
| FS-HO-02 | URS-HO-02 | Halt API: `POST /model/{id}/suspend` with reason; halt event audit-logged; transitions model state to `SUSPENDED`; consumer endpoints return `MODEL_UNAVAILABLE` until reinstated. |
| FS-HO-03 | URS-HO-03 | Consumer SDK enforces human-in-the-loop gate for safety-critical / quality-critical consumers via `requires_human_approval=True` flag; auto-approve forbidden in this code path. |
| FS-HO-04 | URS-HO-04 | LMS-recorded HO Operator training requirement enforced by Okta group membership; role-grant blocked without training completion. |
| FS-HO-05 | URS-HO-05 | HO Operator UI panel "Capabilities + Limits + Known Failure Modes" loaded from `GET /model/{id}/ifu`; displays in-context with each monitored model. |
| FS-HO-06 | URS-HO-06 | Override-intervention API `POST /model/{id}/override` records `reason`, `time_iso8601`, `downstream_impact_assessment`; logs available via `GET /audit/overrides`. |
| FS-LOG-01 | URS-LOG-01 | Event-log writer emits to `audit_events` table + Splunk index `lyr-mlsrv-audit`; event types enumerated in `event_types.py`. |
| FS-LOG-02 | URS-LOG-02 | Storage tiers: Postgres hot (90 days), Splunk warm (6 mo per Art. 12), S3 + Glacier cold (10 y per Art. 18); ILM policy enforced at storage-class level. |
| FS-LOG-03 | URS-LOG-03 | Event-row schema: `actor_id`, `session_id`, `request_id`, `model_id`, `model_version`, `timestamp_iso8601`, `integrity_hash_sha256`. |
| FS-LOG-04 | URS-LOG-04 | Export endpoint `GET /audit/export?format={json,csv,pdf}&from=...&to=...` streaming; does not block live ingest path. |
| FS-IFU-01 | URS-IFU-01 | IFU record schema: `capabilities`, `limits`, `intended_purpose`, `foreseeable_misuse`, `accuracy_metrics`, `robustness_metrics`, `cybersecurity_metrics`, `human_oversight_measures`, `expected_lifetime`, `training_data_summary`. |
| FS-IFU-02 | URS-IFU-02 | API endpoint `GET /model/{id}/ifu` returns the IFU as JSON or PDF/A-3; surfaced via consumer SDK helper `model.get_ifu()`. |
| FS-IFU-03 | URS-IFU-03 | IFU versions stored in MLflow `ifu/{version}.json`; consumers subscribe via webhook `POST /webhook/ifu-update`; pinning via `ifu_version` request header. |
| FS-ROB-01 | URS-ROB-01 | Training-data integrity verified at registration (hash compared against feature-store snapshot); runtime adversarial-input detector publishes `ADVERSARIAL_SUSPECTED` when input-distance > envelope. |
| FS-ROB-02 | URS-ROB-02 | Adversarial-perturbation OQ suite per model in `oq/adversarial_*.py`; declared performance levels asserted within documented envelope. |
| FS-ROB-03 | URS-ROB-03 | Rate-limit middleware per consumer (configurable); output post-processor enforces no training-example return; review checklist in `validation/confidentiality_review.md`. |
| FS-ROB-04 | URS-ROB-04 | Release-gate CI job `benchmark_release_gate.py` runs locked benchmark set; release blocked if metrics regress beyond per-model envelopes recorded in `promotion_criteria.yaml`. |
| FS-ROB-05 | URS-ROB-05 | CIS K8s + OWASP API Security Top 10 evidence in `security_evidence/`; non-conformities tracked in Jira `LYR-SEC`. |
| FS-TD-01 | URS-TD-01 | Annex IV pack template `annex_iv_template/` with required sub-folders (a)–(h); each model maintains its instance under `lyr-aiact-techdoc/{model_id}/`. |
| FS-TD-02 | URS-TD-02 | Change-control hook on MLflow state transitions triggers Annex IV pack revision review; revision required before EFFECTIVE-CHAMPION promotion. |
| FS-TD-03 | URS-TD-03 | Export job `annex_iv_export.py` produces zipped pack within 1 business day; Reg-Affairs signs export manifest. |
| FS-RET-01 | URS-RET-01 | Retention policies coded in S3 Object Lock (Governance / Compliance mode) + Glacier Vault Lock: 10 y for Annex IV pack, EU DoC, conformity records, training records, PMM records. |
| FS-RET-02 | URS-RET-02 | Delete attempts return `403 RetentionLockActive` until floor passed; admin-side delete impossible during retention. |
| FS-CONF-01 | URS-CONF-01 | Conformity-assessment workflow `conformity_assessment.py` triggers Notified Body engagement for Annex VII pathway when MLflow flag `notified_body_required=true`; record stored in `conformity_records/{model_id}/`. |
| FS-CONF-02 | URS-CONF-02 | EU DoC template `eu_doc_template.docx` populated per model via `generate_doc.py`; signed by Reg-Affairs (AI/ML) via DocuSign; stored in `conformity_records/{model_id}/doc.pdf`. |
| FS-CONF-03 | URS-CONF-03 | CE-marking surface `GET /model/{id}/ce-marking` returns structured `{marking: applied, notified_body_id, doc_url, applied_standards}`. |
| FS-CONF-04 | URS-CONF-04 | Substantial-modification detection by `pccp_predicate_engine` (FS-PCCP-02); on detection triggers renewed conformity-assessment workflow. |
| FS-REG-01 | URS-REG-01 | EU AI database registration via Reg-Affairs UI `eu_aidb_register.py`; for Annex I models inheriting EUDAMED registration, captured `udi_di` linkage in MLflow record. |
| FS-REG-02 | URS-REG-02 | MLflow record carries `eu_aidb_entry_id`, `eu_aidb_registration_date`, `eudamed_udi_di`. |
| FS-PMM-01 | URS-PMM-01 | PMM service collects per-inference outcomes, drift detections, override events, consumer-side incident webhooks; feeds CAPA-compatible findings into the QMS via `qms_capa_sink.py`. |
| FS-PMM-02 | URS-PMM-02 | PMM data sources configured in `pmm_sources.yaml`; webhook receiver `/webhook/consumer-incident` accepts deployer reports. |
| FS-PMM-03 | URS-PMM-03 | Quarterly PMM report template `pmm_report.md.j2`; auto-generated + signed by Reg-Affairs + VP QA via `pmm_report_signoff.py`. |
| FS-INC-01 | URS-INC-01 | Art. 73 incident-reporting service tracks 3 clocks: standard 15 d, death 10 d, widespread fundamental-rights 2 d; per-incident clock advancement audit-logged. |
| FS-INC-02 | URS-INC-02 | Authority-routing table `authority_routing.yaml`: DE → BfArM (+ EU MDR Art. 87 channel where SaMD), CH → Swissmedic, AT → AGES. |
| FS-INC-03 | URS-INC-03 | Clock-start event triggered by `POST /incident` or by Auto-Detector on safety-metric breach (FS-AB-05); clock-display surfaced to Reg-Affairs. |
| FS-INC-04 | URS-INC-04 | Incident schema: `model_id`, `model_version`, `deployer_id`, `event_timestamp`, `narrative`, `root_cause_analysis_status`, `corrective_action`, `regulator_notification_status_by_authority`. |
| FS-DEP-01 | URS-DEP-01 | Deployer-contract template `deployer_contract_template.md` codifies Art. 26 obligations; signed deployer-contract presence enforced before consumer onboarding completes. |
| FS-DEP-02 | URS-DEP-02 | FRIA registry `fria_registry/` per public-body / essential-services deployer; presence enforced for any Annex III model exposed to such deployer. |
| FS-DEP-03 | URS-DEP-03 | API endpoint `GET /model/{id}/deployer-obligations` returns structured Art. 26 duties keyed by deployer type. |
| FS-QMS-01 | URS-QMS-01 | QMS conformance to Art. 17 + ISO/IEC 42001:2023 evidenced in `qms_manual.md`; controls mapped against ISO/IEC 42001 clauses A.2.x–A.10.x. |
| FS-QMS-02 | URS-QMS-02 | Annual QMS effectiveness review by VP QA + Head of AI Eng Platforms + Reg-Affairs; report stored in `qms_review/{year}/`. |
| FS-QMS-03 | URS-QMS-03 | QMS integration: AI lifecycle changes flow through site change-control system (ServiceNow) + CAPA system (MasterControl) via `qms_integration_bridge.py`. |
| FS-AUD-01 | URS-AUD-01 | Audit-trail schema: `actor`, `action`, `model_id`, `model_version`, `old_value`, `new_value`, `reason_for_change`, `timestamp_iso8601`, `signature_id`. All MLflow + Seldon write operations emit audit events. |
| FS-AUD-02 | URS-AUD-02 | Audit-trail table append-only (DB trigger blocks UPDATE / DELETE); SIEM-forwarded copy in Splunk frozen-index immutable. |
| FS-AUD-03 | URS-AUD-03 | Audit captures drift-detection events (`DRIFT_FLAGGED`), Champion ↔ Challenger transitions, deployment / suspend events, PCCP-deviation flags, override interventions, Art. 73 incident triggers. |
| FS-AUD-04 | URS-AUD-04 | Splunk forwarder with TLS + retry; forwarder-lag SLO 5 min. Splunk frozen-index 25-year retention configured at index level. |
| FS-AUD-05 | URS-AUD-05 | Audit-trail review workflow: weekly review by System Owner via Splunk saved-search; annual review by QA with documented evidence. |
| FS-AUD-06 | URS-AUD-06 | Audit-trail records carry `record_class` enum (`platform_audit` / `inference_event`); Splunk indexes separated `lyr-mlsrv-audit` vs `lyr-mlsrv-inference`. |
| FS-PART11-01 | URS-PART11-01 | Procedural controls documented in `/sop/aiml-platform-controls.md`; reviewed annually. |
| FS-PART11-02 | URS-PART11-02 | All human access via Okta SAML 2.0 + MFA; service accounts via mTLS only; no shared accounts. |
| FS-PART11-03 | URS-PART11-03 | Operational audit trail per FS-AUD-01 above. |
| FS-PART11-04 | URS-PART11-04 | Electronic-signature record schema includes `signer_printed_name`, `signing_timestamp_iso8601`, `signing_meaning` (REVIEW / APPROVE / SUSPEND / OVERRIDE / RETIRE). |
| FS-PART11-05 | URS-PART11-05 | Signature → record link via HMAC-SHA256 over record-hash + signer-ID + timestamp; verification on read; tampered records flagged. |
| FS-PART11-06 | URS-PART11-06 | Signature record carries `signer_id` uniqueness constraint in DB; reuse / reassignment blocked at provisioning. |
| FS-PART11-07 | URS-PART11-07 | Re-auth: signing endpoint requires fresh OAuth2 access-token (max-age 5 min); cached credentials rejected. |
| FS-PART11-08 | URS-PART11-08 | Okta password policy: MFA mandatory, lockout 5 fails / 15 min, complexity per site standard. |
| FS-PART11-09 | URS-PART11-09 | Export endpoints (FS-LOG-04) produce both JSON (electronic) and PDF/A-3 (human-readable) copies; consistency verified by hash compare. |
| FS-PART11-10 | URS-PART11-10 | Retention enforced by FS-RET-01..02 + Splunk frozen-index 25 y; cold archive 10 y minimum per Art. 18. |
| FS-PART11-11 | URS-PART11-11 | SOPs in `/sop/` git repo; annual review tracked in `sop_review_calendar.yaml`. |
| FS-PART11-12 | URS-PART11-12 | TLS 1.3 enforced at site API Gateway (Kong); digital-signature non-repudiation via Sigstore at internet boundaries. |
| FS-DI-01 | URS-DI-01 | All actions carry `actor_id` (named Okta user or named service-account); enforced at audit write. |
| FS-DI-02 | URS-DI-02 | Audit + inference export endpoints render JSON or PDF; PDF/A-3 for archival. |
| FS-DI-03 | URS-DI-03 | Audit `timestamp_iso8601` is server-time at event; retroactive entries (rare) flagged with `entry_timestamp` + `reason_for_delay`. |
| FS-DI-04 | URS-DI-04 | Raw inference inputs + outputs stored in immutable S3-bucket `lyr-inference-raw/`; derivative analyses in separate prefix. |
| FS-DI-05 | URS-DI-05 | Output transformations (rescaling, thresholding) coded in `transforms/` module; deterministic; OQ test pins seed and verifies bitwise reproducibility. |
| FS-DI-06 | URS-DI-06 | Inference + audit + MLflow records: complete metadata fields validated; chronological order DB-enforced; ≥ 10 y retention (Art. 18) + ≥ 25 y for clinical-impact; export ≤ 1 business day. |
| FS-DI-07 | URS-DI-07 | Training-data lineage: hash in MLflow links to immutable `lyr-training-data/` S3 prefix; lineage reproducible via documented data-pipeline script. |
| FS-DI-08 | URS-DI-08 | Art. 10 data-governance template `art10_data_governance_template.md` populated per model; bias-mitigation evidence linked from Annex IV pack. |
| FS-INT-GIT-01 | URS-INT-GIT-01 | GitLab pre-receive hook enforces GPG-signed tags; tags without signature rejected. |
| FS-INT-MLFLOW-01 | URS-INT-MLFLOW-01 | MLflow Postgres backend audit-logged; mutation triggers emit audit event. |
| FS-INT-SIEM-01 | URS-INT-SIEM-01 | Splunk Universal Forwarder TLS 1.3; forwarder SLO 5 min; immutable frozen-index ≥ 25 y. |
| FS-INT-OKTA-01 | URS-INT-OKTA-01 | Okta SAML 2.0; MFA-required group `aiml-prod-users`; group membership = access path. |
| FS-INT-DPIA-01 | URS-INT-DPIA-01 | DPIA URN field in MLflow `models` table; mandatory for models flagged `processes_personal_data=true`. |
| FS-INT-FEAST-01 | URS-INT-FEAST-01 | Feast registry shared with MLflow; per-model `feast_snapshot_version` recorded at model registration. |
| FS-INT-TRITON-01 | URS-INT-TRITON-01 | Triton model-repository deployed as Seldon InferenceGraph; repository pulls trigger cosign verification; updates audit-logged in `triton_audit/`. |
| FS-INT-EUDAMED-01 | URS-INT-EUDAMED-01 | EUDAMED UDI-DI captured in MLflow for SaMD components; publication via Reg-Affairs workflow. |
| FS-PERF-01 | URS-PERF-01 | Inference P95 ≤ 200 ms verified via Grafana `histogram_quantile(0.95, inference_latency_seconds)`. |
| FS-PERF-02 | URS-PERF-02 | Load test ≥ 1,000 inferences/second sustained; verified via k6 PQ script. |
| FS-PERF-03 | URS-PERF-03 | Availability ≥ 99.9% / month: uptime sensor + Grafana SLO board. |
| FS-PERF-04 | URS-PERF-04 | HorizontalPodAutoscaler scales `inference-deployment` from 4 to 64 pods on queue-depth metric. |
| FS-PERF-05 | URS-PERF-05 | Warm-pool config in `warm_pool.yaml` per model; cold-start P95 ≤ 30 s verified in PQ. |
| FS-OBS-01 | URS-OBS-01 | Per-model SLO definitions in `slo/{model_id}.yaml`; Prometheus + Grafana SLO board with burn-rate alerts. |
| FS-OBS-02 | URS-OBS-02 | SLO-breach alerts route via PagerDuty to HO Operator + System Owner; sustained breach triggers FS-AB-05 auto-rollback. |
| FS-OBS-03 | URS-OBS-03 | SLO history retained in Prometheus long-term store (Thanos) for 5 y. |
| FS-BAK-01 | URS-BAK-01 | MLflow Postgres nightly pg_dump with SHA-256 integrity; S3 versioned bucket; model artefact store + Feast snapshot S3 versioned + lifecycle. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore drill: restore Postgres + MLflow + Feast + sample artefact retrieval; QA witness signature. |
| FS-BAK-03 | URS-BAK-03 | RTO ≤ 4 h verified via DR drill; RPO ≤ 15 min via async etcd backup + WAL shipping. |
| FS-BAK-04 | URS-BAK-04 | Annual DR tabletop + live partial failover; report signed by VP IT Compliance. |
| FS-BAK-05 | URS-BAK-05 | Annual Glacier-restore drill: retrieve sample Annex IV pack + DoC + conformity record from cold archive; documented retrieval time ≤ 24 h. |
| FS-SEC-01 | URS-SEC-01 | CIS Kubernetes Benchmark v1.9 applied; kube-bench scan in CI; non-conformities tracked in Jira. |
| FS-SEC-02 | URS-SEC-02 | Training-data hash verified at registration; runtime adversarial-input anomaly detector emits `ADVERSARIAL_SUSPECTED` alert when input-distance > threshold. |
| FS-SEC-03 | URS-SEC-03 | Trivy scan in CI on every build; HIGH + CRITICAL CVEs block image push to registry. |
| FS-SEC-04 | URS-SEC-04 | HashiCorp Vault stores DB credentials, MLflow access keys, cosign signing keys; access audit-logged. |
| FS-SEC-05 | URS-SEC-05 | Pod Security Admission `restricted` profile cluster-wide; NetworkPolicy `default-deny-all` then explicit allows for `aiml-prod` namespace. |
| FS-SEC-06 | URS-SEC-06 | Adversarial robustness stress-test per high-risk model documented in Art. 11 pack; runs in CI before model promotion to EFFECTIVE-CHAMPION. |
| FS-SEC-07 | URS-SEC-07 | Foundation-model + pre-trained-weight ingest pipeline `model_ingest.py` produces SBOM (CycloneDX) + verifies upstream signature before MLflow registration. |
| FS-CONF-DEF-01 | URS-CONF-DEF-01 | Per-consumer rate limit middleware in API Gateway; output post-processor strips potential membership signals where applicable. |
| FS-CONF-DEF-02 | URS-CONF-DEF-02 | Inversion-leakage review checklist in `validation/inversion_review.md`; OQ test asserts no training-example return on probing inputs. |
| FS-CONF-DEF-03 | URS-CONF-DEF-03 | DP-SGD evaluation result recorded in Annex IV pack under `art15_robustness/dp_evaluation.md`. |
| FS-CARD-01 | URS-CARD-01 | Model-card template `model_card_template.md`; populated per model at promotion; served via `GET /model/{id}/model-card`. |
| FS-CARD-02 | URS-CARD-02 | Model-card version pinned to model-artefact version; URL pattern `/model/{id}/model-card?version={v}`. |
| FS-TRN-01 | URS-TRN-01 | Okta group provisioning blocked without LMS training completion; integration via Okta-LMS connector. |
| FS-TRN-02 | URS-TRN-02 | Annual LMS refresher: course `AIACT-2026-ANNUAL`; covers EU AI Act Arts. 8–21 + 26 + 72 + 73 + 99 + drift + incident response. |
| FS-TRN-03 | URS-TRN-03 | Consumer-app onboarding course `AIML-INTEGRATION-ONBOARDING`; required before consumer SDK key issued. |
| FS-TRN-04 | URS-TRN-04 | AI literacy course `AI-LITERACY-ART4` assigned to all staff with AI-output exposure; LMS records 5 y retention. |
| FS-PR-01 | URS-PR-01 | Annual Periodic Review template includes model inventory, drift evidence, PCCP adherence, audit-trail review evidence, Art. 17 QMS, ISO/IEC 42001:2023 conformance, training currency, PMM findings, fitness-for-use; signed by Head of AI Eng Platforms + VP QA + Reg Affairs (AI/ML) + Conformity Assessment Coordinator. |
| FS-PR-02 | URS-PR-02 | Post-market monitoring per EU AI Act Art. 72: incident-detector emits structured incident records; serious incidents trigger Art. 73 notifications to BfArM / Swissmedic / AGES via the regulatory-reporting service per FS-INC-01..04. |
| FS-PR-03 | URS-PR-03 | Periodic review may flag a model for re-validation; re-validation workflow invoked via MLflow state transition. |
| FS-PR-04 | URS-PR-04 | Classification-reassessment checklist run per model; reclassification triggers change-control + URS update + FS update. |
| FS-FAIR-01 | URS-FAIR-01 | Quarterly bias-metric job `bias_metrics_job.py` per high-risk model; per-sub-population gap reports stored in `bias_reports/{model_id}/{q}.md`. |
| FS-FAIR-02 | URS-FAIR-02 | Bias-mitigation experiment tracking in MLflow `bias_mitigation/` experiment namespace; baseline + post-mitigation metrics linked. |
| FS-FAIR-03 | URS-FAIR-03 | Bias-evidence panel `aiact-ho-monitor` includes per-model bias-status indicator; Annex IV pack `art10_data_governance/bias_evidence.md` cross-linked. |
| FS-DSR-01 | URS-DSR-01 | GDPR DSR API endpoints: `POST /dsr/access`, `POST /dsr/erasure`, `POST /dsr/restriction`; routed per use case; legal-review gate before fulfilment. |
| FS-DSR-02 | URS-DSR-02 | Art. 22(3) safeguard surfaces: human-intervention request → HO Operator queue; contest workflow → Reg-Affairs review. |
| FS-VFM-01 | URS-VFM-01 | Foundation-model registration form in MLflow: `foundation_model_name`, `version`, `source`, `licence`, `training_data_summary_url`; SBOM (CycloneDX) attached. |
| FS-VFM-02 | URS-VFM-02 | Foundation-model advisory subscription `fm_advisory_subscriber.py`; alerts to System Owner + Reg-Affairs on vendor security disclosure. |


### 4.1 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: OIDC via Entra ID with workload-identity federation for service-to-service. Conditional-access binding to policy `AI-Platform Conditional Access (FIDO2 + device-compliance + risk-based step-up)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the model-registry catalogue and MinIO/S3 object-replica for model binaries + Annex IV artefacts; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.2 Cross-System Integration — LMS handover (M-XINT-LMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-LMS-01 | URS-XINT-LMS-01 | LMS-competence adapter `<sys>-LMS-CLIENT-1.x` performs `GET /lms/competence/{user_id}?curriculum=...` over mTLS + Entra workload-identity; cache TTL per system (12-24 h); on `current=false` the consumer blocks the gated action and records `lms_lapse_user={user_id}` in the consumer audit trail; periodic reconciliation job verifies that no gated action proceeded with a lapsed competence. |

## 5. Configuration Items (CI)

| CI | Item | Value |
|---|---|---|
| CI-01 | K8s cluster name | `lyr-aiml-prod` |
| CI-02 | Champion / Challenger | enabled via Seldon |
| CI-03 | Drift threshold (per model) | configured in MLflow `model_metadata` |
| CI-04 | Audit retention | ≥ 25 years (Splunk frozen-index) + ≥ 10 y cold archive (S3 Object Lock + Glacier Vault Lock) |
| CI-05 | Inference confidence-threshold (per model) | configured in MLflow `model_metadata.confidence_threshold` |
| CI-06 | PCCP rule-engine | `pccp_predicate_engine` v1.0 |
| CI-07 | Okta MFA-required group | `aiml-prod-users` |
| CI-08 | Splunk forwarder SLO | 5 minutes |
| CI-09 | AZ count | 3 |
| CI-10 | HPA pod range | 4 – 64 |
| CI-11 | Feast snapshot store | S3-versioned `lyr-feast/` |
| CI-12 | Triton model repository | `lyr-triton-models/` (Sigstore-verified) |
| CI-13 | Art. 73 clocks | 15 d / 10 d / 2 d (per FS-INC-01) |
| CI-14 | Annex IV pack base path | `s3://lyr-aiact-techdoc/` |
| CI-15 | Annex-IV-pack retention | 10 y from market placement (Art. 18) |
| CI-16 | Notified-Body identifier | recorded per high-risk model in conformity record |

## 6. Risks (FS-level)

Implementation-level risks (URS § 9 RA already documents R-01..R-20). Additional FS-side risks:

- Model-artefact signing key compromise → mitigation: Vault audit logs + key rotation every 90 days
- DB trigger bypass for audit-table mutation → mitigation: enforced at DB role level (only `audit-writer` role can INSERT; no role can UPDATE / DELETE)
- Sigstore signing service outage → mitigation: cached trusted-root + offline verification mode
- PCCP predicate-engine miscoded → mitigation: PCCP envelope review annually + unit-tested examples for each PCCP rule
- Feast point-in-time correctness breach during materialise window → mitigation: serialisable isolation + verification check
- Triton driver-repository update introducing non-determinism → mitigation: bitwise-reproducibility OQ on each driver bump
- Art. 73 clock miscalculation across timezones → mitigation: UTC-only internal clock + display in operator TZ
- Annex IV pack-template drift between releases → mitigation: template version-pinned per release + CI check

## 7. References

- LYR-URS-MLSRV-001 v1.2
- 21 CFR Part 11; EU GMP Annex 11; EU GMP Annex 22 (DRAFT)
- EU AI Act 2024/1689 Arts. 8–21, 26, 43, 47, 48, 49, 72, 73, 99, 113
- EU MDR Reg. 2017/745
- GDPR Arts. 6, 9, 22, 32, 35
- ICH Q9(R1); ICH Q14; FDA AI/ML SaMD Action Plan (2021); FDA PCCP (Aug 2025); FDA GMLP (2021)
- ISPE GAMP 5 (2nd ed., 2022); GAMP GPG *AI/ML in GxP*
- ISO/IEC 42001:2023; ISO/IEC 23053; ISO/IEC 27001:2022; ISO 14971:2019
- NIST AI 100-1 (AI RMF 1.0); NIST AI 600-1 (GenAI Profile, 2024)
- BfArM (DE); Swissmedic (CH); AGES (AT)
- NVIDIA Triton Inference Server documentation; MLflow documentation; Seldon Core documentation; Feast documentation; Sigstore / cosign

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-PLAT-01 | FS-PLAT-01 |
| URS-PLAT-02 | FS-PLAT-02 |
| URS-PLAT-03 | FS-PLAT-03 |
| URS-PLAT-04 | FS-PLAT-04 |
| URS-PLAT-05 | FS-PLAT-05 |
| URS-PLAT-06 | FS-PLAT-06 |
| URS-PLAT-07 | FS-PLAT-07 |
| URS-MOD-01 | FS-MOD-01 |
| URS-MOD-02 | FS-MOD-02 |
| URS-MOD-03 | FS-MOD-03 |
| URS-MOD-04 | FS-MOD-04 |
| URS-MOD-05 | FS-MOD-05 |
| URS-MOD-06 | FS-MOD-06 |
| URS-MOD-07 | FS-MOD-07 |
| URS-AB-01 | FS-AB-01 |
| URS-AB-02 | FS-AB-02 |
| URS-AB-03 | FS-AB-03 |
| URS-AB-04 | FS-AB-04 |
| URS-AB-05 | FS-AB-05 |
| URS-FS-01 | FS-FS-01 |
| URS-FS-02 | FS-FS-02 |
| URS-FS-03 | FS-FS-03 |
| URS-FS-04 | FS-FS-04 |
| URS-PCCP-01 | FS-PCCP-01 |
| URS-PCCP-02 | FS-PCCP-02 |
| URS-PCCP-03 | FS-PCCP-03 |
| URS-PCCP-04 | FS-PCCP-04 |
| URS-INF-01 | FS-INF-01 |
| URS-INF-02 | FS-INF-02 |
| URS-INF-03 | FS-INF-03 |
| URS-INF-04 | FS-INF-04 |
| URS-INF-05 | FS-INF-05 |
| URS-INF-06 | FS-INF-06 |
| URS-INF-07 | FS-INF-07 |
| URS-HO-01 | FS-HO-01 |
| URS-HO-02 | FS-HO-02 |
| URS-HO-03 | FS-HO-03 |
| URS-HO-04 | FS-HO-04 |
| URS-HO-05 | FS-HO-05 |
| URS-HO-06 | FS-HO-06 |
| URS-LOG-01 | FS-LOG-01 |
| URS-LOG-02 | FS-LOG-02 |
| URS-LOG-03 | FS-LOG-03 |
| URS-LOG-04 | FS-LOG-04 |
| URS-IFU-01 | FS-IFU-01 |
| URS-IFU-02 | FS-IFU-02 |
| URS-IFU-03 | FS-IFU-03 |
| URS-ROB-01 | FS-ROB-01 |
| URS-ROB-02 | FS-ROB-02 |
| URS-ROB-03 | FS-ROB-03 |
| URS-ROB-04 | FS-ROB-04 |
| URS-ROB-05 | FS-ROB-05 |
| URS-TD-01 | FS-TD-01 |
| URS-TD-02 | FS-TD-02 |
| URS-TD-03 | FS-TD-03 |
| URS-RET-01 | FS-RET-01 |
| URS-RET-02 | FS-RET-02 |
| URS-CONF-01 | FS-CONF-01 |
| URS-CONF-02 | FS-CONF-02 |
| URS-CONF-03 | FS-CONF-03 |
| URS-CONF-04 | FS-CONF-04 |
| URS-REG-01 | FS-REG-01 |
| URS-REG-02 | FS-REG-02 |
| URS-PMM-01 | FS-PMM-01 |
| URS-PMM-02 | FS-PMM-02 |
| URS-PMM-03 | FS-PMM-03 |
| URS-INC-01 | FS-INC-01 |
| URS-INC-02 | FS-INC-02 |
| URS-INC-03 | FS-INC-03 |
| URS-INC-04 | FS-INC-04 |
| URS-DEP-01 | FS-DEP-01 |
| URS-DEP-02 | FS-DEP-02 |
| URS-DEP-03 | FS-DEP-03 |
| URS-QMS-01 | FS-QMS-01 |
| URS-QMS-02 | FS-QMS-02 |
| URS-QMS-03 | FS-QMS-03 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
| URS-AUD-05 | FS-AUD-05 |
| URS-AUD-06 | FS-AUD-06 |
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
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-DI-07 | FS-DI-07 |
| URS-DI-08 | FS-DI-08 |
| URS-INT-GIT-01 | FS-INT-GIT-01 |
| URS-INT-MLFLOW-01 | FS-INT-MLFLOW-01 |
| URS-INT-SIEM-01 | FS-INT-SIEM-01 |
| URS-INT-OKTA-01 | FS-INT-OKTA-01 |
| URS-INT-DPIA-01 | FS-INT-DPIA-01 |
| URS-INT-FEAST-01 | FS-INT-FEAST-01 |
| URS-INT-TRITON-01 | FS-INT-TRITON-01 |
| URS-INT-EUDAMED-01 | FS-INT-EUDAMED-01 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-PERF-03 | FS-PERF-03 |
| URS-PERF-04 | FS-PERF-04 |
| URS-PERF-05 | FS-PERF-05 |
| URS-OBS-01 | FS-OBS-01 |
| URS-OBS-02 | FS-OBS-02 |
| URS-OBS-03 | FS-OBS-03 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-BAK-03 | FS-BAK-03 |
| URS-BAK-04 | FS-BAK-04 |
| URS-BAK-05 | FS-BAK-05 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-SEC-05 | FS-SEC-05 |
| URS-SEC-06 | FS-SEC-06 |
| URS-SEC-07 | FS-SEC-07 |
| URS-CONF-DEF-01 | FS-CONF-DEF-01 |
| URS-CONF-DEF-02 | FS-CONF-DEF-02 |
| URS-CONF-DEF-03 | FS-CONF-DEF-03 |
| URS-CARD-01 | FS-CARD-01 |
| URS-CARD-02 | FS-CARD-02 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-TRN-03 | FS-TRN-03 |
| URS-TRN-04 | FS-TRN-04 |
| URS-PR-01 | FS-PR-01 |
| URS-PR-02 | FS-PR-02 |
| URS-PR-03 | FS-PR-03 |
| URS-PR-04 | FS-PR-04 |
| URS-FAIR-01 | FS-FAIR-01 |
| URS-FAIR-02 | FS-FAIR-02 |
| URS-FAIR-03 | FS-FAIR-03 |
| URS-DSR-01 | FS-DSR-01 |
| URS-DSR-02 | FS-DSR-02 |
| URS-VFM-01 | FS-VFM-01 |
| URS-VFM-02 | FS-VFM-02 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-LMS-01 | FS-XINT-LMS-01 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Silent model drift consumed in GxP decision | Medium | Critical | URS-INF-02, URS-PR-03, URS-OBS-01..03 |
| R-02 | Silent inference failure (null / default consumed by consumer) | Medium | Critical | URS-INF-04, consumer-side defensive coding |
| R-03 | Audit-tampering | Low | Critical | URS-AUD-02, URS-INT-SIEM-01 (immutable retention) |
| R-04 | Model artefact tampering at deployment | Low | High | URS-MOD-03 (signed artefact + Author ≠ Approver) |
| R-05 | Training-data contamination at registration | Low | High | URS-MOD-01 (hash verification), URS-DI-07 (lineage), URS-ROB-01 |
| R-06 | EU AI Act non-conformance on Art. 14 human oversight | Medium | High | URS-HO-01..06 |
| R-07 | Model-poisoning / adversarial-input attack | Low | High | URS-SEC-02, URS-SEC-06, URS-ROB-01..05 |
| R-08 | Authorisation bypass | Low | Critical | URS-PART11-02, URS-PART11-07, URS-SEC-01 |
| R-09 | Inference-log SIEM forwarding outage | Medium | Medium | URS-INT-SIEM-01, monitoring alert on forwarder health |
| R-10 | PCCP deviation (model update outside approved plan) | Medium | High | URS-MOD-04, URS-AUD-03 (deviation flag), URS-PCCP-01..04 |
| R-11 | Substantial modification triggering Art. 43 re-assessment missed | Low | Critical | URS-MOD-04 + change-control gate + URS-PCCP-03 |
| R-12 | DR-site activation under load fails | Low | High | URS-BAK-03, URS-BAK-04 (annual DR test) |
| R-13 | Membership-inference / model-inversion attack discloses training data | Low | High | URS-CONF-DEF-01..03 |
| R-14 | EU AI Act Art. 73 incident-clock missed (15 d / 10 d / 2 d) | Low | Critical | URS-INC-01..04 + clock-tracking instrumentation |
| R-15 | EU AI Act Annex I vs III mis-classification | Low | Critical | URS-PR-04 + classification reassessment in periodic review |
| R-16 | Annex IV technical-documentation pack incomplete at notified-body inspection | Medium | High | URS-TD-01..03 + URS-PR-01 audit of pack completeness |
| R-17 | Art. 18 retention floor (10 y) breached by premature deletion | Low | Critical | URS-RET-01..02 (policy-coded enforcement) |
| R-18 | EU AI Act Art. 99 penalty exposure (up to €15M / 3% turnover for high-risk non-compliance) | Low | Critical | URS-PR-01 + URS-QMS-01..03 + URS-INC-01..04 |
| R-19 | Feature-store drift not propagated to model performance | Medium | High | URS-FS-04 + URS-INF-02 |
| R-20 | GPU driver / Triton runtime upgrade introduces non-determinism | Low | High | URS-PLAT-06 + URS-DI-05 (deterministic transforms OQ-validated) |

Full evaluation in `LYR-RA-MLSRV-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
