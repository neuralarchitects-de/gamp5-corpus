---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "LYR-FS-MLSRV-001 v1.2 (parent FS)"
  - "LYR-URS-MLSRV-001 v1.2 (informational)"
  - "GAMP 5 (2nd ed., 2022) Cat 5 — Software Design Specification"
  - "EU AI Act 2024/1689 Annex I high-risk; deadline 2 Aug 2027"
  - "IEC 62304:2006+A1:2015; IEC 81001-5-1:2021; ISO/IEC 42001:2023; NIST SP 800-218 SSDF; OWASP ASVS v5.0; OWASP LLM Top 10 (2024)"
parent_fs:
  document_number: LYR-FS-MLSRV-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Lyrae_Bioworks_AI_ML_Model_Server_FS_v1.3.md
parent_urs:
  document_number: LYR-URS-MLSRV-001
  version: 1.2
  file: ../../../URS/_generated/final/AI_ML_Model_Server_GxP__Lyrae_Bioworks_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Software Design Specification (SDS)

## AI / ML Model Server (GxP Inference Service) — Site-Developed FastAPI on K8s + MLflow + Seldon Core + NVIDIA Triton

**Document Number:** LYR-DS-MLSRV-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** LYR-FS-MLSRV-001 v1.2 | **Parent URS:** LYR-URS-MLSRV-001 v1.2
**Site:** Lyrae Bioworks GmbH, München, Germany *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom Application (site-developed FastAPI + Python control-plane; Seldon Core + Triton + MLflow + Feast as Cat-3 framework substrate)
**EU AI Act 2024/1689 classification:** **Annex I high-risk AI system** (safety component of regulated medicinal-product / medical-device decisions). Compliance deadline **2 August 2027**. Conformity-assessment pathway Annex VII (notified-body) where the underlying product is MDR class IIa+.
**Project Mode:** Greenfield site-developed control-plane on K8s 1.30; first AI/ML platform serving Lyrae's GxP-relevant predictive models (per parent URS Project Mode line)
**Tier (inherited from parent URS+FS):** T4 — mission-critical multi-module + Cat 5 custom
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11; EU GMP Annex 22 (DRAFT); ICH Q9(R1); ICH Q14; **EU AI Act 2024/1689 Arts. 8–21 (provider duties), 26 (deployer obligations), 43+47+48 (conformity + CE + DoC), 49 (EU AI database), 50 (transparency), 72 (PMM), 73 (incident reporting), 99 (penalty), 113 (entry-into-force)**; EU MDR 2017/745; GDPR Arts. 6, 9, 22, 32, 35; FDA AI/ML SaMD Action Plan (2021); FDA PCCP (Aug 2025); FDA GMLP (2021); FDA CSA (Feb 2026); ISPE GAMP GPG *AI/ML in GxP* (2024); ISO/IEC 42001:2023 (AI MS); ISO/IEC 23053; NIST AI RMF 1.0 + GenAI Profile (2024); IEC 62304; IEC 81001-5-1; NIST SP 800-218 SSDF; OWASP ASVS v5.0; OWASP LLM Top 10 (2024); BfArM (DE), Swissmedic (CH), AGES (AT).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect — AI/ML Platforms) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of AI Engineering Platforms) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Security Architect — AI/ML) | _____________ | _____________ | _____ |
| Reviewer (Reg Affairs — AI/ML) | _____________ | _____________ | _____ |
| Reviewer (Notified Body Liaison) | _____________ | _____________ | _____ |
| Reviewer (Data Protection Officer) | _____________ | _____________ | _____ |
| Reviewer (MLOps Lead) | _____________ | _____________ | _____ |
| Reviewer (Human Oversight Operator Lead) | _____________ | _____________ | _____ |
| Approver (VP AI / Data Science) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |
| Approver (VP Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (System Owner — Head of AI Eng Platforms) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue. Inherited Tier T4 from parent URS+FS pair. Derived from LYR-FS-MLSRV-001 v1.2. DS covers 148/153 FS-IDs as DS-IDs; 5 FS-IDs flagged as "vendor-internal — no site design surface" (NVIDIA Triton scheduler internals, Seldon Core operator reconcile loop, MLflow tracking-server SQL internals, Feast online-store retrieval primitives, Istio sidecar mesh-control-plane internals). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from LYR-URS-MLSRV-001 v1.2 and LYR-FS-MLSRV-001 v1.2. Additional DS-specific terms:

| Term | Definition |
|---|---|
| SDS | Software Design Specification (this document) |
| Annex I | EU AI Act 2024/1689 Annex I — list of EU harmonisation legislation under which AI safety components are classified high-risk (Union harmonisation Annex I); deadline 2 Aug 2027 |
| Annex IV | EU AI Act technical-documentation pack required under Art. 11 |
| PCCP | Predetermined Change Control Plan (FDA Aug 2025 AI-Enabled Device Software Functions guidance) |
| HO | Human Oversight (EU AI Act Art. 14) |
| PMM | Post-Market Monitoring (EU AI Act Art. 72) |
| FRIA | Fundamental Rights Impact Assessment (EU AI Act Art. 27 — deployer-side) |
| IFU | Instructions for Use (EU AI Act Art. 13 transparency) |
| DoC | Declaration of Conformity (EU AI Act Art. 47) |
| DCGM | NVIDIA Data Center GPU Manager (telemetry exporter) |
| Sigstore / cosign | Open-source signing infrastructure (model + container signatures) |
| Lakera Guard | Optional third-party LLM-output filter (Hydra-only — N/A for Lyrae predictive models) |

## 1. Purpose

This SDS describes the technical design of the site-developed AI/ML Model Server (LYR-FS-MLSRV-001 v1.2) — its software architecture, module decomposition, data model, algorithms, API, security, deployment, and module-specification index. The SDS is the controlling input to the Module Specification artefacts (`LYR-MS-MLSRV-{module}-001`), the EU AI Act Annex IV technical-documentation pack template `lyr-aiact-techdoc/{model_id}/`, the IQ/OQ/PQ Protocol Set, and the Notified Body submission pack (Annex VII pathway). Vendor-internal source code (Seldon Core, Triton, MLflow, Feast, Istio, NVIDIA driver) is not redrawn; vendor SDLC owns those internals.

## 2. Scope

**In scope.** Site-developed Python + FastAPI services (inference gateway, drift-monitor, adversarial-input detector, PCCP predicate engine, Annex IV pack generator, conformity-assessment workflow, EU DoC generator, PMM service, Art. 73 incident-reporting service, IFU service, model-card service, override-intervention service, HO Operator UI backend, deployer-obligations API, audit-event writer, audit-export endpoint, foundation-model ingest pipeline); K8s 1.30 deployment topology (3 AZs, etcd quorum); MLflow model registry (3-node HA); Seldon Core + Istio service mesh; NVIDIA Triton Inference Server; Feast feature store; integrations with GitLab, Splunk SIEM, HashiCorp Vault, Okta, EUDAMED, EU AI database, Notified Body interface, BfArM/Swissmedic/AGES regulatory-reporting endpoints; observability (Prometheus + Grafana + Thanos + Loki + Tempo).

**Out of scope.** Vendor-internal source code of Seldon Core / Triton / MLflow / Feast / Istio / NVIDIA driver / Splunk / Vault / Okta; physical-infrastructure (OCI / on-prem) per Aurora Backup + Quartz AD scope; specific predictive models' training procedure (per-model artefacts live in `lyr-aiact-techdoc/{model_id}/` and downstream model-development records).

## 3. Architectural Overview

```
                                          ┌─ Provider boundary (EU AI Act Arts. 8–21) ─┐
                                          │                                              │
       GitLab (signed tags + cosign) ─────┼───► MLflow Registry (3-node HA, Postgres)   │
            │                             │           │                                   │
            │  CI/CD: ArgoCD              │           ▼                                   │
            ▼                             │   Sigstore-verified model artefact store      │
       Container Registry (cosign         │   (S3 `lyr-models/`)                          │
        signed images)                    │           │                                   │
            │                             │           ▼                                   │
            ▼                             │   ┌──────────────────────────────────────┐   │
     ┌────────────────────────────────────┼──►│   Seldon Core (K8s 1.30, Istio mesh)│   │
     │  Kubernetes Cluster                │   │   ├─ FastAPI inference service (CPU)│   │
     │  `lyr-aiml-prod`                   │   │   ├─ NVIDIA Triton Inference (GPU)  │   │
     │  3 AZs · etcd quorum               │   │   ├─ Drift Monitor                  │   │
     │  CIS Kubernetes Benchmark (current release at site deployment) hardened   │   │   ├─ Adversarial-Input Detector     │   │
     │  Pod Security: restricted          │   │   ├─ PCCP Predicate Engine          │   │
     │  NetworkPolicy: default-deny       │   │   └─ Confidence-Threshold Gate      │   │
     └────────────────────────────────────┼───┴──────┬───────────────────────────────┘   │
                                          │          │                                   │
                                          │   ┌──────▼────────┐  mTLS via API Gateway   │
                                          │   │ Output post-  │  (Kong + Istio)         │
                                          │   │ processor     │                          │
                                          │   │ (output_hash, │                          │
                                          │   │ confidentiality)│                        │
                                          │   └──────┬────────┘                         │
                                          │          │                                   │
   Feast feature store ◄──► MLflow records│          │                                   │
   (snapshot-pinned)                      │          │                                   │
                                          └──────────┼───────────────────────────────────┘
                                                     │
                                          ┌──────────▼────────────────┐  Deployer boundary
                                          │  Consumer GxP systems     │  (EU AI Act Art. 26)
                                          │  + Human Oversight (Art.14)│
                                          │  + PMM (Art. 72/73)        │
                                          └─┬──────────────────────────┘
                                            │
                       ┌────────────────────┼─────────────────────────────────┐
                       ▼                    ▼                                  ▼
                Splunk SIEM       BfArM/Swissmedic/AGES                EUDAMED + EU AI DB
                Art. 12 ≥ 6 mo    Art. 73 incident reporting          Art. 49 registration
                Art. 18 ≥ 10 y    (15 d / 10 d / 2 d clocks)
```

**Three architectural views per § 2B.5(1):**

**Logical view.** Provider boundary = the site (Lyrae as EU AI Act provider per Art. 16); deployer boundary = consumer GxP systems (per Art. 26). The inference path is: request → API gateway (mTLS + OAuth2) → Seldon Core → model serving (FastAPI / Triton) → confidence gate → drift monitor → adversarial detector → output post-processor (hash + confidentiality) → response. Parallel paths: audit-event writer → Splunk; drift-flag → MLflow state transition; safety-metric breach → auto-rollback (FS-AB-05); incident detection → Art. 73 clock start.

**Process view.** K8s 1.30 across 3 AZs; etcd 5-node quorum; control-plane nodes per AZ; worker-node pool segmented by `gxp=true` taint; GPU node pool for Triton (Pod-Security-Standard `restricted`); HPA from 4 → 64 pods on queue-depth metric; horizontal Pod autoscaler per inference deployment (`inference-deployment`). Cold-start P95 ≤ 30 s via warm-pool config per model.

**Technology view.** Python 3.12 + FastAPI 0.115 + Uvicorn (control-plane services); PyTorch 2.4 + ONNX Runtime 1.20 (model serving); NVIDIA Triton 24.10 (GPU inference); Seldon Core 2.9 (orchestration); MLflow 2.18 + Postgres 16 (registry); Feast 0.40 + Redis 7.4 (feature store); Istio 1.24 (mesh); Kong 3.8 (API gateway); HashiCorp Vault 1.18 (secrets); Sigstore + cosign 2.4 (signing); Prometheus 3.0 + Grafana 11 + Thanos + Loki 3.0 + Tempo 2.6 (observability); Splunk Universal Forwarder 9.3 (SIEM); Trivy 0.57 + kube-bench (CI); ArgoCD 2.12 + GitLab 17 (CI/CD); Okta SAML 2.0 + MFA; SBOM CycloneDX 1.6.

**EU AI Act Annex I declaration.** This platform is classified **Annex I high-risk** under EU AI Act 2024/1689 because the inference outputs feed safety components of regulated medicinal-product release decisions and medical-device decisions (e.g. release-decision prediction, batch-acceptance prediction, in-vivo / in-vitro assay-result interpretation). The compliance deadline is **2 August 2027**. Conformity-assessment pathway is **Annex VII (notified-body involvement)** where the underlying product is MDR class IIa or above. Art. 99 penalty tier for non-conformance: up to **€15 million or 3% of global annual turnover** (whichever is higher) for breaches of Arts. 9–17 / 26 / 50 obligations.

## 4. Software Architecture

The architecture decomposes into seven layers (logical view):

1. **Provider Control Plane** — model registry, model-artefact signing, conformity assessment, Annex IV pack management, IFU service, model-card service, PCCP predicate engine, EU DoC generator. *FastAPI + Postgres.*
2. **Inference Plane** — Seldon Core InferenceGraph; FastAPI inference adapter; NVIDIA Triton runtime for GPU models; ONNX Runtime for CPU models. *Seldon + FastAPI + Triton.*
3. **Real-Time Safety Plane** — confidence-threshold gate; drift monitor (data/concept/prediction); adversarial-input detector; output post-processor (hash, confidentiality). *FastAPI middleware + Python workers.*
4. **Feature Plane** — Feast offline (Postgres) + online (Redis); feature-definition registry; feature-drift monitor; point-in-time-correctness materialisation. *Feast.*
5. **Observability + SIEM Plane** — Prometheus + Grafana + Thanos (5-y SLO history); Loki (logs); Tempo (traces); Splunk Universal Forwarder → Splunk indexes `lyr-mlsrv-audit` + `lyr-mlsrv-inference`.
6. **Regulatory + Post-Market Plane** — Art. 73 incident-reporting service (3 clocks); PMM service (drift + override + incident webhooks); EU AI database registration; EUDAMED registration (where SaMD); deployer-obligations API.
7. **Identity + Secrets + Supply-Chain Plane** — Okta SAML 2.0 + MFA + workload-identity federation; HashiCorp Vault (DB creds, signing keys, MLflow keys); Sigstore cosign for model + image signatures; CycloneDX SBOM; Trivy CI scan; kube-bench CIS K8s.

**Process view (deployment unit topology).**

- Control-plane FastAPI services (provider-control-plane + regulatory-plane) deploy as 3-replica StatefulSet across 3 AZs (`namespace lyr-mlsrv-control`).
- Inference services deploy as Deployment per model (`namespace lyr-mlsrv-inference`); HPA 4–64 replicas on queue-depth.
- Safety-plane workers (drift, adversarial) deploy as DaemonSet on inference nodes (`namespace lyr-mlsrv-safety`).
- MLflow tracking server: 3-node HA StatefulSet behind Kong (`namespace lyr-mlsrv-mlflow`).
- Postgres: 3-node patroni HA cluster (`namespace lyr-mlsrv-data`); read replicas in two of three AZs.
- Feast: Postgres offline + Redis online; Redis 7-node cluster (`namespace lyr-mlsrv-feast`).

**Technology view.** See § 3 *Technology view* paragraph above for exact versions; pinned in `Chart.yaml` per Helm chart family.

## 5. Module Decomposition

| Module ID | Name | Responsibility | Interface (exposed) | Dependencies (consumed) | Owner | GxP-criticality |
|---|---|---|---|---|---|---|
| MOD-PROV-01 | `model-registry-service` | MLflow façade: registration, schema enforcement, state-machine, signed-artefact verification | REST `/model/`, gRPC | MLflow, Postgres, Vault, Sigstore, GitLab | AI Platforms | R1 (registry integrity) |
| MOD-PROV-02 | `pccp-predicate-engine` | Evaluate each model update against PCCP envelope | REST `/model/{id}/pccp-check`, library | MLflow, Postgres | Reg-Affairs IT | R1 (FDA PCCP) |
| MOD-PROV-03 | `annex4-pack-manager` | Manage Annex IV pack subfolders (a)–(h); export job | REST `/model/{id}/annex4`, CLI | S3 `lyr-aiact-techdoc/`, MLflow | Reg-Affairs IT | R1 (Annex I obligation) |
| MOD-PROV-04 | `conformity-assessment-workflow` | Annex VII engagement; conformity record; CE marking | REST `/model/{id}/conformity`, `/model/{id}/ce-marking` | Notified Body interface | Reg-Affairs IT | R1 (Art. 43) |
| MOD-PROV-05 | `eu-doc-generator` | EU DoC template + DocuSign signing | REST `/model/{id}/doc`, scheduled job | DocuSign API; conformity record | Reg-Affairs IT | R1 (Art. 47) |
| MOD-PROV-06 | `ifu-service` | IFU schema + per-version serving | REST `/model/{id}/ifu` (JSON / PDF/A-3) | MLflow, Postgres | Reg-Affairs IT | R2 (Art. 13) |
| MOD-PROV-07 | `model-card-service` | Model-card per artefact version | REST `/model/{id}/model-card` | MLflow | AI Platforms | R2 |
| MOD-INF-01 | `inference-gateway` | FastAPI inference adapter; OAuth2; rate-limit | REST `POST /model/{id}/infer`, `POST /model/{id}/batch` | Seldon Core, Triton, Kong | AI Platforms | R1 (inference path) |
| MOD-INF-02 | `seldon-bridge` | Seldon Core InferenceGraph orchestration | gRPC, REST | Seldon Core | AI Platforms | R1 |
| MOD-SAFE-01 | `confidence-gate` | Apply per-model confidence threshold | inline middleware | MLflow metadata, model output | AI Platforms | R1 (Art. 15) |
| MOD-SAFE-02 | `drift-monitor` | PSI / KS-test / chi-square (data); canary-label (concept); output-shift (prediction) | Cron + REST `/drift/{model_id}`, Prometheus metric | Feast, MLflow, Postgres | AI Platforms | R1 (Art. 9 + 15) |
| MOD-SAFE-03 | `adversarial-detector` | Input-distance-vs-envelope; flag ADVERSARIAL_SUSPECTED | inline middleware, REST `/adversarial/{model_id}/probe` | model input statistics | Security Architecture | R2 (Art. 15) |
| MOD-SAFE-04 | `output-postprocessor` | `output_hash` (SHA-256); confidentiality strip (membership-signal) | inline middleware | model output, post-processing rules | AI Platforms | R2 |
| MOD-SAFE-05 | `auto-rollback-watcher` | Safety-metric breach → `POST /model/{id}/rollback` | Cron + Prometheus alert | safety-metric SLO, MLflow | AI Platforms | R1 (Art. 26 deployer breach handling) |
| MOD-FEAST-01 | `feast-bridge` | Feature-definition CRUD; snapshot pinning per model | REST `/features/`, library | Feast, MLflow | AI Platforms | R1 (lineage) |
| MOD-FEAST-02 | `feature-drift-monitor` | Per-feature drift score | Cron + Prometheus | Feast offline + online | AI Platforms | R2 |
| MOD-AUD-01 | `audit-event-writer` | All MLflow + Seldon mutations emit audit events | Library + Postgres trigger + Splunk forwarder | MLflow, Seldon, Postgres `audit_events` | AI Platforms | R1 (Part 11 + Art. 12) |
| MOD-AUD-02 | `audit-export-endpoint` | Stream audit events as JSON / CSV / PDF/A-3 | REST `/audit/export` | Postgres view, Splunk | AI Platforms | R2 |
| MOD-HO-01 | `ho-operator-ui-backend` | Grafana data API for `aiact-ho-monitor` | REST `/ho/dashboard-data` | Prometheus, MLflow | HO Operations | R1 (Art. 14) |
| MOD-HO-02 | `halt-suspend-service` | Suspend / resume model; consumer-side `MODEL_UNAVAILABLE` | REST `POST /model/{id}/suspend`, `/resume` | MLflow state, Seldon | HO Operations | R1 (Art. 14) |
| MOD-HO-03 | `override-intervention-service` | Record override; downstream impact | REST `POST /model/{id}/override` | Postgres, audit-writer | HO Operations | R1 (Art. 14) |
| MOD-PMM-01 | `pmm-service` | Collect outcomes + drift + override + incident webhooks | REST `/webhook/consumer-incident`, scheduled jobs | drift monitor, override service, consumer webhooks | Reg-Affairs IT | R1 (Art. 72) |
| MOD-PMM-02 | `pmm-quarterly-report` | Auto-generate PMM template; sign-off via DocuSign | CLI + REST `/pmm/quarterly/{q}` | PMM service, MLflow | Reg-Affairs IT | R2 |
| MOD-INC-01 | `art73-incident-service` | 3 clocks (15 d / 10 d / 2 d); UTC internal; tz display | REST `POST /incident`, `/incident/{id}`, Cron | regulatory-reporting routing table | Reg-Affairs IT | R1 (Art. 73) |
| MOD-INC-02 | `regulatory-reporting-router` | DE → BfArM, CH → Swissmedic, AT → AGES (+ MDR Art. 87 where SaMD) | REST `POST /report/{authority}` | mTLS gateway certs | Reg-Affairs IT | R1 |
| MOD-DEP-01 | `deployer-contract-service` | Art. 26 obligations registry; deployer onboarding | REST `/deployer/`, `/model/{id}/deployer-obligations` | Postgres, MLflow | Reg-Affairs IT | R2 (Art. 26) |
| MOD-DEP-02 | `fria-registry` | FRIA per public-body / essential-services deployer | REST `/fria/{deployer_id}` | Postgres | Reg-Affairs IT | R2 (Art. 27) |
| MOD-REG-01 | `eu-aidb-registrar` | EU AI database registration via Reg-Affairs UI | REST `/eu-aidb/{model_id}` | EU AI DB endpoint, MLflow | Reg-Affairs IT | R1 (Art. 49) |
| MOD-REG-02 | `eudamed-bridge` | UDI-DI link for SaMD models | REST `/eudamed/{udi_di}` | EUDAMED endpoint | Reg-Affairs IT | R1 (MDR linkage) |
| MOD-QMS-01 | `qms-bridge` | ServiceNow change-control + MasterControl CAPA bridge | REST + Kafka | ServiceNow, MasterControl | QMS Ops | R2 (Art. 17 + ISO/IEC 42001) |
| MOD-VFM-01 | `foundation-model-ingest` | SBOM + signature verification before MLflow registration | CLI + REST | cosign, CycloneDX, SBOM tool | Security Architecture | R1 (Art. 15 supply-chain) |
| MOD-DSR-01 | `gdpr-dsr-service` | Art. 22(3) safeguards + erasure / access / restriction routing | REST `/dsr/access`, `/dsr/erasure`, `/dsr/restriction` | Postgres, legal-review gate | DPO + Legal | R1 (GDPR) |
| MOD-FAIR-01 | `bias-metrics-job` | Quarterly per-sub-population gap | Cron + REST `/bias/{model_id}/{q}` | Postgres bias_reports | AI Platforms | R2 (Art. 10) |
| MOD-CFG-DEF-01 | `inversion-leakage-defender` | Rate-limit per consumer; output strip on probe pattern | inline middleware | Kong rate-limit | Security Architecture | R2 (Art. 15 confidentiality) |
| MOD-TRN-01 | `okta-lms-connector` | Okta group grant gated by LMS completion | webhook + REST | Okta API, LMS API | IAM Ops | R2 (Art. 4 AI-literacy + Art. 14 training) |
| MOD-PR-01 | `periodic-review-orchestrator` | Annual review template + auto-collect | Cron + REST `/periodic-review/{year}` | MLflow, audit, drift, IFU, PMM | Reg-Affairs IT | R2 |

## 6. Data Model Design

### 6.1 MLflow `models` table — extended schema (per FS-MOD-01)

```sql
CREATE TABLE models (
  model_id           UUID         PRIMARY KEY,
  model_name         TEXT         NOT NULL,
  model_version      TEXT         NOT NULL,
  state              TEXT         NOT NULL CHECK (state IN
                       ('DRAFT','REVIEW','APPROVED',
                        'EFFECTIVE-CHALLENGER','EFFECTIVE-CHAMPION',
                        'SUSPENDED','DRIFT_FLAGGED','DEPRECATED','RETIRED')),
  training_data_hash CHAR(64)     NOT NULL,           -- SHA-256
  training_code_git_tag TEXT      NOT NULL,           -- signed GitLab tag
  hyperparameters_json JSONB      NOT NULL,
  evaluation_metrics_json JSONB   NOT NULL,
  validation_report_url TEXT,
  intended_use_statement TEXT     NOT NULL,
  gxp_classification_flag BOOL    NOT NULL,
  eu_aiact_classification TEXT    NOT NULL CHECK (eu_aiact_classification IN
                       ('annex_i','annex_iii','non_high_risk')),
  annex_iv_pack_url  TEXT         NOT NULL,
  notified_body_required BOOL     NOT NULL DEFAULT false,
  notified_body_id   TEXT,
  pccp_record_id     UUID         REFERENCES pccp_records(id),
  feast_snapshot_version TEXT     NOT NULL,
  raw_data_sha256    CHAR(64)     NOT NULL,
  labelling_protocol_version TEXT NOT NULL,
  bias_evidence_url  TEXT,
  confidence_threshold NUMERIC(5,4) NOT NULL,
  ifu_version        TEXT         NOT NULL,
  model_card_url     TEXT         NOT NULL,
  processes_personal_data BOOL    NOT NULL DEFAULT false,
  dpia_urn           TEXT,
  eu_aidb_entry_id   TEXT,
  eu_aidb_registration_date DATE,
  eudamed_udi_di     TEXT,
  created_by         TEXT         NOT NULL,
  created_at         TIMESTAMPTZ  NOT NULL DEFAULT now(),
  retired_at         TIMESTAMPTZ
);
```

### 6.2 `pccp_records` table (per FS-PCCP-01)

```sql
CREATE TABLE pccp_records (
  id                 UUID         PRIMARY KEY,
  model_id           UUID         REFERENCES models(model_id),
  mop_json           JSONB        NOT NULL,   -- Modifications protocol (FDA Aug 2025)
  pcem_json          JSONB        NOT NULL,   -- Protocol for change-evaluation methods
  ia_json            JSONB        NOT NULL,   -- Impact assessment
  envelope_yaml      TEXT         NOT NULL,   -- predicate-engine input
  approved_by        TEXT         NOT NULL,
  approved_at        TIMESTAMPTZ  NOT NULL
);
```

### 6.3 `audit_events` table (per FS-AUD-01..06)

```sql
CREATE TABLE audit_events (
  event_id           BIGSERIAL    PRIMARY KEY,
  record_class       TEXT         NOT NULL CHECK (record_class IN ('platform_audit','inference_event')),
  actor_id           TEXT         NOT NULL,                  -- Okta user or service-account
  session_id         UUID,
  request_id         UUID,
  model_id           UUID,
  model_version      TEXT,
  action             TEXT         NOT NULL,
  old_value          JSONB,
  new_value          JSONB,
  reason_for_change  TEXT,
  signature_id       UUID,
  timestamp_iso8601  TIMESTAMPTZ  NOT NULL DEFAULT now(),
  integrity_hash_sha256 CHAR(64)  NOT NULL,                  -- HMAC-SHA256 over canonical event
  entry_timestamp    TIMESTAMPTZ,                            -- only for retroactive entries
  reason_for_delay   TEXT
);
-- DB trigger blocks UPDATE/DELETE on audit_events
CREATE OR REPLACE RULE audit_events_no_update AS ON UPDATE TO audit_events DO INSTEAD NOTHING;
CREATE OR REPLACE RULE audit_events_no_delete AS ON DELETE TO audit_events DO INSTEAD NOTHING;
```

### 6.4 `inference_log` table (per FS-INF-01..07)

```sql
CREATE TABLE inference_log (
  request_id         UUID         PRIMARY KEY,
  consumer_id        TEXT         NOT NULL,
  model_id           UUID         NOT NULL,
  model_version      TEXT         NOT NULL,
  served_by_model_version TEXT    NOT NULL,                   -- Champion vs Challenger (FS-AB-04)
  input_checksum_sha256 CHAR(64)  NOT NULL,
  output             JSONB        NOT NULL,
  output_hash_sha256 CHAR(64)     NOT NULL,                   -- FS-INF-06
  confidence         NUMERIC(5,4) NOT NULL,
  latency_ms         INTEGER      NOT NULL,
  error_code         TEXT,                                    -- per FS-INF-04 enum
  timestamp_iso8601  TIMESTAMPTZ  NOT NULL DEFAULT now()
);
-- Retention: ≥ 25 y for clinical-impact models (FS-INF-01 + FS-DI-06)
```

### 6.5 IFU + Model-Card schema (JSON)

```jsonc
// IFU record (FS-IFU-01)
{
  "model_id": "uuid",
  "ifu_version": "2026.05.01",
  "capabilities": ["…"],
  "limits": ["…"],
  "intended_purpose": "…",
  "foreseeable_misuse": ["…"],
  "accuracy_metrics": {"…": "…"},
  "robustness_metrics": {"…": "…"},
  "cybersecurity_metrics": {"…": "…"},
  "human_oversight_measures": ["…"],
  "expected_lifetime": "…",
  "training_data_summary": "…"
}
```

### 6.6 Art. 73 incident schema (per FS-INC-01..04)

```jsonc
{
  "incident_id": "uuid",
  "model_id": "uuid",
  "model_version": "…",
  "deployer_id": "…",
  "event_timestamp_utc": "ISO-8601",
  "clock_class": "standard_15d | death_10d | widespread_fr_2d",
  "clock_start_utc": "ISO-8601",
  "narrative": "…",
  "root_cause_analysis_status": "open | in_progress | closed",
  "corrective_action": "…",
  "regulator_notification_status_by_authority": {
    "BfArM": {"sent_at_utc": "…", "ack_at_utc": "…"},
    "Swissmedic": {"sent_at_utc": "…", "ack_at_utc": "…"},
    "AGES": {"sent_at_utc": "…", "ack_at_utc": "…"}
  }
}
```

### 6.7 Data classification + retention

| Class | Examples | Retention | Storage |
|---|---|---|---|
| GxP audit (R1) | `audit_events` | ≥ 25 y (Splunk frozen) + ≥ 10 y (S3 Glacier Vault Lock) | Postgres hot 90 d + Splunk + S3 |
| Inference event (R1 clinical) | `inference_log` clinical-impact | ≥ 25 y | Splunk + S3 |
| Inference event (R2 non-clinical) | other `inference_log` | ≥ 10 y | Splunk warm + S3 |
| Annex IV pack | `lyr-aiact-techdoc/{model_id}/` | ≥ 10 y from market placement (Art. 18) | S3 Object Lock (Compliance) + Glacier Vault Lock |
| EU DoC + conformity record | `conformity_records/{model_id}/` | ≥ 10 y (Art. 18) | S3 Object Lock |
| Training data | `lyr-training-data/{run_id}/` | indefinite during model lifetime + ≥ 10 y post-retirement | S3 versioned + immutable |
| Feast snapshots | `lyr-feast/` | indefinite | S3 versioned |
| PMM records | `pmm/{q}/` | ≥ 10 y | S3 Object Lock |
| GDPR personal data | per model `processes_personal_data=true` | per DPIA, max necessary | encrypted-at-rest AES-256 |

## 7. Algorithm + Calculation Design

### 7.1 Model-loading sequence

Pseudocode for safe model loading (FS-MOD-02, FS-MOD-03):

```
1. fetch tag and signed artefact from MLflow + S3 lyr-models/.
2. verify cosign signature against trusted root (cached in /etc/sigstore/trusted-root.json).
3. fetch PCCP record + envelope_yaml.
4. evaluate pccp_predicate_engine on candidate vs envelope.
5. if non-conformant -> raise PCCP_OUT_OF_ENVELOPE (FS-PCCP-02), abort.
6. verify Author JWT != Approver JWT (FS-MOD-03).
7. transition state DRAFT -> REVIEW -> APPROVED via API (SoD-enforced).
8. transition APPROVED -> EFFECTIVE-CHALLENGER (default 0% live traffic).
9. update inference graph; warm-pool from warm_pool.yaml (FS-PERF-05).
10. emit audit_events row (action='MODEL_PROMOTED').
```

### 7.2 Inference-with-confidence flow

```
input -> input_checksum_sha256 -> rate-limit middleware (Kong) -> oauth2 validation
      -> consumer rate-limit (FS-CONF-DEF-01) -> adversarial-input detector
      -> drift monitor read (current model state)
      -> Seldon InferenceGraph -> model serve (Triton GPU | FastAPI CPU)
      -> confidence threshold gate (model.confidence_threshold from MLflow)
      -> output post-processor (output_hash_sha256, confidentiality strip)
      -> audit_events INSERT + inference_log INSERT (Postgres + Splunk forward)
      -> response.
```

Edge cases: (a) confidence < threshold → response carries `LOW_CONFIDENCE` flag + consumer SDK must explicitly accept (FS-INF-05); (b) drift > threshold → response carries `DRIFT_BLOCK` (FS-INF-04) + MLflow state → `DRIFT_FLAGGED`; (c) adversarial-distance > envelope → `ADVERSARIAL_SUSPECTED` (FS-INF-04); (d) PCCP envelope breach detected on hot-reload → block deployment; (e) any safety-metric breach → auto-rollback watcher fires.

### 7.3 Drift-monitor numerical procedure

Per FS-INF-02:

- **Data drift.** PSI: `PSI = Σ_bin (P_bin_current − P_bin_reference) · ln(P_bin_current / P_bin_reference)`. Compute per feature per hour. PSI > 0.25 → DRIFT_FLAGGED. KS-test two-sample with α = 0.01. Chi-square for categorical features (α = 0.01).
- **Concept drift.** Canary-label evaluation when labels available within 7 days; outcome accuracy delta > 5 pp vs reference → DRIFT_FLAGGED.
- **Prediction drift.** Output-distribution shift via Jensen-Shannon divergence; JSD > 0.10 → DRIFT_FLAGGED.

Numerical precision: float64 throughout; reference distribution snapshot pinned per `feast_snapshot_version`.

### 7.4 Art. 14 human-override flow

```
HO Operator UI shows model state + drift + bias indicator.
On 'Suspend': POST /model/{id}/suspend reason=... -> MLflow state SUSPENDED
              -> consumer endpoints return MODEL_UNAVAILABLE.
On 'Override': POST /model/{id}/override reason, time, downstream_impact
              -> audit_events row + override registry.
On 'Resume': POST /model/{id}/resume -> state -> EFFECTIVE-{CHAMPION|CHALLENGER}.
```

Override is recorded with downstream-impact assessment per FS-HO-06.

### 7.5 PCCP predicate engine

Per FS-PCCP-02:

```
def evaluate(model_update, envelope_yaml) -> 'CONFORMANT' | 'PCCP_OUT_OF_ENVELOPE':
  for delta in {hyperparameters, training_data_composition, architecture}:
    if delta exceeds envelope[delta] -> return 'PCCP_OUT_OF_ENVELOPE'
  return 'CONFORMANT'
```

Envelope examples (illustrative): `learning_rate: {0.5x..2x baseline}`, `architecture: {layers ± 1, no new layer-type}`, `training_data_composition: {distribution shift PSI < 0.05}`. Per-model envelope frozen pre-deployment via change control (FS-AB-02). Non-conformant updates raise FS-PCCP-03 deviation record + Art. 43(4) substantial-modification assessment.

### 7.6 Art. 73 clock arithmetic

UTC-only internal time; display in operator TZ. Clock start = `clock_start_utc`. Standard: 15 calendar days. Death: 10 calendar days. Widespread fundamental-rights breach: 2 working days. Cron job advances per-incident clock; visual display surfaces `remaining_business_hours` to Reg-Affairs. Mitigation R-14: TZ-handling unit-tested with all DACH + UK + US zones.

### 7.7 Auto-rollback (FS-AB-05)

```
on PrometheusAlert(safety_metric > threshold for 5m):
  POST /model/{id}/rollback reason='AUTO_SAFETY_BREACH' metric=... value=...
  -> MLflow state: EFFECTIVE-CHAMPION -> SUSPENDED
  -> previous EFFECTIVE-CHAMPION restored (one-shot, no further auto-promotion)
  -> PagerDuty HO + System Owner
  -> audit_events row
```

### 7.8 Feature-store point-in-time correctness

Feast `materialize-incremental` with serialisable isolation; verification check post-materialise; abort + alert on integrity failure (mitigation D-05).

### 7.9 Reproducibility envelope

Output transformations (rescaling, thresholding) deterministic; OQ pins seed (`numpy.random.seed=42`, `torch.manual_seed=42`); bitwise reproducibility asserted on `tests/test_reproducibility.py`.

### 7.10 Bias-metrics calculation (FS-FAIR-01)

Per quarter per high-risk model: per-sub-population (age band × sex × ethnicity × site) — accuracy gap, precision gap, recall gap; statistical-parity difference; equalised-odds difference. Gap > 5 pp triggers bias-mitigation experiment in MLflow `bias_mitigation/` namespace.

## 8. Interface + API Design

OpenAPI-style table per § 2B.5(5):

| Endpoint | Method | Path | AuthN | Request schema | Response schema | Rate limit | Error codes (HTTP) | Audit event |
|---|---|---|---|---|---|---|---|---|
| Register model | POST | `/model` | OAuth2 + signed JWT | `RegisterModelRequest` | `Model` | 10/min/user | 400 schema, 409 conflict, 422 PCCP_OUT_OF_ENVELOPE | MODEL_REGISTERED |
| Promote model | POST | `/model/{id}/promote` | OAuth2 + 2 signed JWTs (Author ≠ Approver) + cosign | `PromoteRequest` | `Model` | 10/min | 400, 403 SoD, 422 PCCP | MODEL_PROMOTED |
| Suspend model | POST | `/model/{id}/suspend` | OAuth2 + HO group | `{reason: string}` | `Model` | 5/min | 400, 403 | MODEL_SUSPENDED |
| Resume model | POST | `/model/{id}/resume` | OAuth2 + HO group | `{reason: string}` | `Model` | 5/min | 400, 403 | MODEL_RESUMED |
| Override | POST | `/model/{id}/override` | OAuth2 + HO group | `OverrideRequest` (reason, time_iso8601, downstream_impact_assessment) | `OverrideRecord` | 100/h | 400 | OVERRIDE_RECORDED |
| Single inference | POST | `/model/{id}/infer` | OAuth2 (consumer JWT) | `InferenceRequest` | `InferenceResponse` (`output`, `confidence`, `output_hash`, `error_code?`) | per-consumer (FS-CONF-DEF-01) | 401, 403, 422 schema, 429, 503 MODEL_UNAVAILABLE | INFERENCE_RECORDED |
| Batch inference | POST | `/model/{id}/batch` | OAuth2 (consumer JWT) | `BatchInferenceRequest` (`batch_size`, `parallelism`, `per_call_timeout_ms`) | `BatchInferenceResponse` (atomic) | per-consumer | 401, 422, 429, 507 | BATCH_INFERENCE_RECORDED |
| Traffic split | POST | `/model/{id}/traffic` | OAuth2 + 2 signed JWTs (Author ≠ Approver) + QA group | `TrafficSplit` | `TrafficSplitRecord` | 5/min | 400, 403 | TRAFFIC_SPLIT_CHANGED |
| Rollback | POST | `/model/{id}/rollback` | OAuth2 + HO group OR auto-watcher service-account | `{reason: string, metric?: …, value?: …}` | `Model` | 10/min | 400, 403 | MODEL_ROLLBACK |
| PCCP check | POST | `/model/{id}/pccp-check` | OAuth2 | `ModelUpdate` | `{result: CONFORMANT, OUT_OF_ENVELOPE, deltas: …}` | 30/min | 400 | PCCP_EVALUATED |
| IFU get | GET | `/model/{id}/ifu` | OAuth2 | — | `IFU` (JSON or PDF/A-3) | 100/h | 404 | IFU_READ |
| Model card | GET | `/model/{id}/model-card` | OAuth2 | — | `ModelCard` | 100/h | 404 | MODEL_CARD_READ |
| CE marking | GET | `/model/{id}/ce-marking` | OAuth2 | — | `{marking: applied, notified_body_id, doc_url, applied_standards}` | 100/h | 404 | CE_READ |
| Annex IV export | POST | `/model/{id}/annex4/export` | OAuth2 + Reg-Affairs group | — | `{zip_url, manifest_sha256}` | 5/d | 400, 403 | ANNEX4_EXPORTED |
| Conformity record | POST | `/model/{id}/conformity` | OAuth2 + Reg-Affairs group | `ConformityRequest` | `ConformityRecord` | 5/d | 400 | CONFORMITY_RECORDED |
| EU DoC generate | POST | `/model/{id}/doc/generate` | OAuth2 + Reg-Affairs group | — | `{doc_url, docusign_envelope_id}` | 5/d | 400 | DOC_GENERATED |
| EU AI DB register | POST | `/eu-aidb/{model_id}` | OAuth2 + Reg-Affairs group | `EUAIDBRequest` | `{entry_id, registration_date}` | 5/d | 400 | EUAIDB_REGISTERED |
| Art. 73 incident | POST | `/incident` | OAuth2 (deployer or HO) | `IncidentRequest` (clock_class, narrative, deployer_id) | `IncidentRecord` (`incident_id`, `clock_start_utc`) | 100/h | 400 | INCIDENT_RECORDED |
| Consumer-incident webhook | POST | `/webhook/consumer-incident` | mTLS (per-deployer cert) | `ConsumerIncident` | `Ack` | per-deployer | 401, 400 | DEPLOYER_INCIDENT |
| Audit export | GET | `/audit/export?from=&to=&format=json|csv|pdf` | OAuth2 + Audit-Reader group | — | streaming | 1/h | 400 | AUDIT_EXPORTED |
| Drift status | GET | `/drift/{model_id}` | OAuth2 | — | `{psi, ks, jsd, drift_score, state}` | 100/h | 404 | — |
| Bias report | GET | `/bias/{model_id}/{q}` | OAuth2 + Reg-Affairs group | — | `BiasReport` | 100/h | 404 | — |
| Deployer obligations | GET | `/model/{id}/deployer-obligations` | OAuth2 | — | `{deployer_type, obligations[]}` | 100/h | 404 | — |
| DSR access | POST | `/dsr/access` | OAuth2 + DSR group | `DSRRequest` | `DSRTicket` | 10/h | 400 | DSR_ACCESS_REQUESTED |
| DSR erasure | POST | `/dsr/erasure` | OAuth2 + DSR group | `DSRRequest` | `DSRTicket` | 10/h | 400 | DSR_ERASURE_REQUESTED |
| DSR restriction | POST | `/dsr/restriction` | OAuth2 + DSR group | `DSRRequest` | `DSRTicket` | 10/h | 400 | DSR_RESTRICTION_REQUESTED |

All endpoints use TLS 1.3 (Kong + Istio mesh enforces cipher suite floor `TLS_AES_256_GCM_SHA384`, `TLS_CHACHA20_POLY1305_SHA256`, `TLS_AES_128_GCM_SHA256`). Service-to-service uses Istio mTLS with workload-identity. JSON encoding uses canonical-JSON for hash inputs (RFC 8785).

## 9. Security Design

### 9.1 AuthN flow

1. User obtains Okta SAML 2.0 assertion + MFA challenge (FIDO2 phishing-resistant for `aiml-prod-approvers` subgroup).
2. Kong API gateway validates assertion against Okta JWKS.
3. Kong issues short-lived OAuth2 access token (max-age 5 min); refresh requires re-auth.
4. Service-to-service: Istio sidecars mutually authenticate via SPIFFE/SPIRE workload-identity certificates.

### 9.2 AuthZ model

RBAC mapped to Okta groups: `aiml-prod-users`, `aiml-prod-approvers`, `aiml-prod-ho`, `aiml-prod-reg-affairs`, `aiml-prod-dsr`, `aiml-prod-audit-readers`, `aiml-prod-mlops`. Role grant blocked at Okta without LMS training completion (FS-TRN-01..04 via MOD-TRN-01).

### 9.3 Secrets management

HashiCorp Vault 1.18: DB credentials (dynamic, TTL 1 h); MLflow access keys (TTL 24 h); cosign signing keys (HSM-backed, rotation 90 d per FS Risk register entry); deployer mTLS certs (per-deployer namespace); regulator-gateway certs (`bfarm-client-2026.p12`, `swissmedic-client-2026.p12`, `ages-client-2026.p12`, EU AI DB cert, EUDAMED cert). Vault audit-logged; access via Kubernetes ServiceAccount (workload-identity).

### 9.4 Transport security

TLS 1.3 enforced at Kong (cipher floor as § 8). Istio mTLS service-to-service. Sigstore for model-artefact + container-image signatures. SBOM CycloneDX 1.6 attached to every model + image; Trivy scans HIGH + CRITICAL CVEs block image push (FS-SEC-03). Foundation-model + pre-trained-weight ingest pipeline `model_ingest.py` (MOD-VFM-01) verifies upstream signature + SBOM before MLflow registration (FS-SEC-07).

### 9.5 Model-poisoning + adversarial-input protection (EU AI Act Art. 15)

- Training-data hash verified at registration (FS-ROB-01).
- Runtime adversarial-input detector publishes `ADVERSARIAL_SUSPECTED` when input-distance > envelope (FS-ROB-01).
- Per-consumer rate-limit + output strip on membership-signal patterns (FS-CONF-DEF-01, FS-ROB-03).
- DP-SGD evaluation result recorded in Annex IV pack `art15_robustness/dp_evaluation.md` (FS-CONF-DEF-03).
- Adversarial-perturbation OQ suite per model in `oq/adversarial_*.py` (FS-ROB-02).
- Release-gate CI job `benchmark_release_gate.py` runs locked benchmark set (FS-ROB-04).
- CIS K8s + OWASP API Security Top 10 evidence in `security_evidence/` (FS-ROB-05).

### 9.6 Audit-trail event taxonomy (extends FS-AUD-01..06)

Event types emitted by `audit-event-writer`: `MODEL_REGISTERED`, `MODEL_PROMOTED`, `MODEL_DEMOTED`, `MODEL_SUSPENDED`, `MODEL_RESUMED`, `MODEL_ROLLBACK`, `MODEL_RETIRED`, `TRAFFIC_SPLIT_CHANGED`, `PCCP_EVALUATED`, `PCCP_DEVIATION`, `DRIFT_FLAGGED`, `ADVERSARIAL_SUSPECTED`, `OVERRIDE_RECORDED`, `INFERENCE_RECORDED`, `BATCH_INFERENCE_RECORDED`, `IFU_READ`, `MODEL_CARD_READ`, `CE_READ`, `ANNEX4_EXPORTED`, `CONFORMITY_RECORDED`, `DOC_GENERATED`, `EUAIDB_REGISTERED`, `EUDAMED_LINKED`, `INCIDENT_RECORDED`, `INCIDENT_CLOCK_ADVANCED`, `DEPLOYER_INCIDENT`, `DEPLOYER_OB_READ`, `AUDIT_EXPORTED`, `DSR_*`, `BIAS_REPORTED`, `PMM_REPORTED`.

## 10. Deployment Architecture

### 10.1 K8s topology

- Cluster: `lyr-aiml-prod` (K8s 1.30); 3 AZs (eu-central-1a/b/c); etcd 5-node quorum.
- Namespaces: `lyr-mlsrv-control`, `lyr-mlsrv-inference`, `lyr-mlsrv-safety`, `lyr-mlsrv-mlflow`, `lyr-mlsrv-data`, `lyr-mlsrv-feast`, `lyr-mlsrv-regulatory`, `lyr-mlsrv-observe`.
- Node pools: `cpu-pool` (E5 32 OCPU / 256 GB); `gpu-pool` (NVIDIA A100 40GB or H100); `system-pool` for control plane. GPU pool tainted `gxp=true:NoSchedule`.
- Pod Security Standards: `restricted` enforced cluster-wide.
- NetworkPolicy: `default-deny-all` per namespace; explicit allow for `aiml-prod` flows.
- HPA per inference deployment: 4 → 64 replicas on queue-depth metric.
- CIS Kubernetes Benchmark (current release at site deployment) applied; kube-bench scan in CI; non-conformities tracked in Jira `LYR-SEC`.

### 10.2 Observability stack

- Prometheus 3.0 (15-s scrape); Grafana 11; Thanos sidecar for 5-y SLO history; Loki 3.0 for logs; Tempo 2.6 for traces.
- Metrics: `inference_latency_seconds`, `inference_error_rate`, `drift_score`, `auth_failures_total`, `model_confidence_below_threshold`, `nvidia_gpu_duty_cycle`, `nvidia_gpu_memory_used_bytes`, `triton_queue_depth_per_model`, `feature_drift_score`, `helios_publish_lag_seconds`.
- Splunk Universal Forwarder 9.3 with TLS 1.3; forwarder-lag SLO 5 min; immutable frozen-index ≥ 25 y (`lyr-mlsrv-audit`, `lyr-mlsrv-inference`).
- SLO history: 5 y in Thanos long-term store.
- Alertmanager → PagerDuty (HO Operator + System Owner + Reg Affairs); sustained breach triggers auto-rollback.

### 10.3 DR + retention

- RTO ≤ 4 h validated via DR drill (FS-PLAT-01).
- RPO ≤ 15 min via async etcd backup + Postgres WAL shipping (FS-PLAT-01, FS-BAK-03).
- Quarterly restore drill: Postgres + MLflow + Feast + sample artefact retrieval (FS-BAK-02).
- Annual DR tabletop + live partial failover (FS-BAK-04).
- Annual Glacier-restore drill for cold archive (FS-BAK-05).
- S3 Object Lock (Compliance) + Glacier Vault Lock for Annex IV + DoC + conformity + training + PMM (≥ 10 y per Art. 18).
- Splunk frozen-index 25 y at index level.

### 10.4 CI/CD

GitLab 17 + ArgoCD 2.12. Signed commits required. Mandatory 2-reviewer code review. CI pipeline: lint → unit-test → Trivy (CVE) → kube-bench → cosign sign → SBOM (CycloneDX) → ArgoCD deploy. CD: GitOps via Helm + Kustomize; PR-based promotion DEV → QC → UAT → PROD.

## 11. Module Specification Table

Per § 2B.5(8): pointer table from this DS to downstream Module Specification (`LYR-MS-MLSRV-{module}-001`):

| Module ID | File path | Primary class / function | Unit-test reference | Module Spec doc |
|---|---|---|---|---|
| MOD-PROV-01 | `services/registry/main.py` | `ModelRegistryService` | `tests/test_registry.py` | LYR-MS-MLSRV-REGISTRY-001 |
| MOD-PROV-02 | `services/pccp/engine.py` | `PCCPPredicateEngine` | `tests/test_pccp.py` | LYR-MS-MLSRV-PCCP-001 |
| MOD-PROV-03 | `services/annex4/manager.py` | `Annex4PackManager` | `tests/test_annex4.py` | LYR-MS-MLSRV-ANNEX4-001 |
| MOD-PROV-04 | `services/conformity/workflow.py` | `ConformityAssessmentWorkflow` | `tests/test_conformity.py` | LYR-MS-MLSRV-CONFORMITY-001 |
| MOD-PROV-05 | `services/doc/generator.py` | `EUDocGenerator` | `tests/test_doc.py` | LYR-MS-MLSRV-DOC-001 |
| MOD-PROV-06 | `services/ifu/main.py` | `IFUService` | `tests/test_ifu.py` | LYR-MS-MLSRV-IFU-001 |
| MOD-PROV-07 | `services/modelcard/main.py` | `ModelCardService` | `tests/test_modelcard.py` | LYR-MS-MLSRV-MODELCARD-001 |
| MOD-INF-01 | `services/inference/gateway.py` | `InferenceGateway` | `tests/test_inference.py` | LYR-MS-MLSRV-INFER-001 |
| MOD-INF-02 | `services/inference/seldon_bridge.py` | `SeldonBridge` | `tests/test_seldon.py` | LYR-MS-MLSRV-SELDON-001 |
| MOD-SAFE-01 | `services/safety/confidence_gate.py` | `ConfidenceGate` | `tests/test_confgate.py` | LYR-MS-MLSRV-CONFGATE-001 |
| MOD-SAFE-02 | `services/safety/drift_monitor.py` | `DriftMonitor` | `tests/test_drift.py` | LYR-MS-MLSRV-DRIFT-001 |
| MOD-SAFE-03 | `services/safety/adversarial_detector.py` | `AdversarialDetector` | `tests/test_adv.py` | LYR-MS-MLSRV-ADV-001 |
| MOD-SAFE-04 | `services/safety/postprocessor.py` | `OutputPostprocessor` | `tests/test_postproc.py` | LYR-MS-MLSRV-POSTPROC-001 |
| MOD-SAFE-05 | `services/safety/auto_rollback.py` | `AutoRollbackWatcher` | `tests/test_rollback.py` | LYR-MS-MLSRV-ROLLBACK-001 |
| MOD-FEAST-01 | `services/feast/bridge.py` | `FeastBridge` | `tests/test_feast.py` | LYR-MS-MLSRV-FEAST-001 |
| MOD-FEAST-02 | `services/feast/feature_drift.py` | `FeatureDriftMonitor` | `tests/test_feat_drift.py` | LYR-MS-MLSRV-FEATDRIFT-001 |
| MOD-AUD-01 | `services/audit/writer.py` | `AuditEventWriter` | `tests/test_audit.py` | LYR-MS-MLSRV-AUDIT-001 |
| MOD-AUD-02 | `services/audit/export.py` | `AuditExportEndpoint` | `tests/test_audit_export.py` | LYR-MS-MLSRV-AUDEXP-001 |
| MOD-HO-01 | `services/ho/ui_backend.py` | `HODashboardBackend` | `tests/test_ho_ui.py` | LYR-MS-MLSRV-HOUI-001 |
| MOD-HO-02 | `services/ho/halt_suspend.py` | `HaltSuspendService` | `tests/test_halt.py` | LYR-MS-MLSRV-HALT-001 |
| MOD-HO-03 | `services/ho/override.py` | `OverrideInterventionService` | `tests/test_override.py` | LYR-MS-MLSRV-OVERRIDE-001 |
| MOD-PMM-01 | `services/pmm/main.py` | `PMMService` | `tests/test_pmm.py` | LYR-MS-MLSRV-PMM-001 |
| MOD-PMM-02 | `services/pmm/quarterly_report.py` | `PMMQuarterlyReport` | `tests/test_pmm_report.py` | LYR-MS-MLSRV-PMMQR-001 |
| MOD-INC-01 | `services/incident/art73.py` | `Art73IncidentService` | `tests/test_incident.py` | LYR-MS-MLSRV-INC-001 |
| MOD-INC-02 | `services/incident/router.py` | `RegulatoryReportingRouter` | `tests/test_inc_router.py` | LYR-MS-MLSRV-INCROUTER-001 |
| MOD-DEP-01 | `services/deployer/contract.py` | `DeployerContractService` | `tests/test_deployer.py` | LYR-MS-MLSRV-DEP-001 |
| MOD-DEP-02 | `services/deployer/fria.py` | `FRIARegistry` | `tests/test_fria.py` | LYR-MS-MLSRV-FRIA-001 |
| MOD-REG-01 | `services/regulatory/eu_aidb.py` | `EUAIDBRegistrar` | `tests/test_eu_aidb.py` | LYR-MS-MLSRV-EUAIDB-001 |
| MOD-REG-02 | `services/regulatory/eudamed.py` | `EUDAMEDBridge` | `tests/test_eudamed.py` | LYR-MS-MLSRV-EUDAMED-001 |
| MOD-QMS-01 | `services/qms/bridge.py` | `QMSBridge` | `tests/test_qms.py` | LYR-MS-MLSRV-QMS-001 |
| MOD-VFM-01 | `services/supply_chain/fm_ingest.py` | `FoundationModelIngest` | `tests/test_fm_ingest.py` | LYR-MS-MLSRV-FMINGEST-001 |
| MOD-DSR-01 | `services/dsr/main.py` | `GDPRDSRService` | `tests/test_dsr.py` | LYR-MS-MLSRV-DSR-001 |
| MOD-FAIR-01 | `services/bias/metrics.py` | `BiasMetricsJob` | `tests/test_bias.py` | LYR-MS-MLSRV-BIAS-001 |
| MOD-CFG-DEF-01 | `services/safety/inversion_defender.py` | `InversionLeakageDefender` | `tests/test_inv_def.py` | LYR-MS-MLSRV-INVDEF-001 |
| MOD-TRN-01 | `services/training/okta_lms_connector.py` | `OktaLMSConnector` | `tests/test_lms.py` | LYR-MS-MLSRV-LMS-001 |
| MOD-PR-01 | `services/periodic_review/orchestrator.py` | `PeriodicReviewOrchestrator` | `tests/test_pr.py` | LYR-MS-MLSRV-PR-001 |

All modules: signed commits in `gitlab.lyrae.local/aiml-platform/{module}`; 2-reviewer code review required; CI: lint + unit-tests + Trivy + cosign + SBOM; ArgoCD-managed Helm deployment.

## 12. References

**US**
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- FDA AI/ML SaMD Action Plan (2021)
- FDA Predetermined Change Control Plan (PCCP) — *AI-Enabled Device Software Functions* (Aug 2025)
- FDA Good Machine Learning Practice (GMLP, 2021)
- FDA *Computer Software Assurance for Production and Quality Management System Software* (Feb 2026)
- NIST AI 100-1 (AI RMF 1.0)
- NIST AI 600-1 (Generative AI Profile, 2024)
- NIST SP 800-218 SSDF v1.1
- NIST SP 800-53 r5

**EU**
- EU AI Act Reg. (EU) 2024/1689 — Arts. 8 (compliance), 9 (risk management), 10 (data governance), 11 + Annex IV (technical documentation), 12 (logging), 13 (transparency / IFU), 14 (human oversight), 15 (accuracy / robustness / cybersecurity), 16 (provider duties), 17 (QMS), 18 (retention 10 y), 19, 20, 21, 26 (deployer obligations), 43 (conformity assessment), 47 (DoC), 48 (CE), 49 (EU AI database), 50 (transparency), 51–55 (GPAI — out of scope for predictive), 72 (post-market monitoring), 73 (incident reporting 15/10/2-day), 99 (penalties up to €15M / 3% turnover), 113 (entry into force)
- EU AI Act Annex I (Union harmonisation legislation — deadline 2 Aug 2027)
- EU GMP Annex 11
- EU GMP Annex 22 (DRAFT — AI/ML for GxP)
- EU MDR Reg. 2017/745
- GDPR Reg. (EU) 2016/679 Arts. 6, 9, 22, 32, 35, 44
- EMA *Reflection Paper on the Use of AI in the Medicinal Product Lifecycle* (2024)

**International**
- ICH Q9(R1); ICH Q14
- IEC 62304:2006+A1:2015 (medical device software lifecycle)
- IEC 81001-5-1:2021 (health-software security lifecycle)
- ISO/IEC 12207 (software lifecycle)
- ISO/IEC 42001:2023 (AI management system)
- ISO/IEC 23053 (framework for AI using ML)
- ISO/IEC 27001:2022 / 27002 / 27017 / 27018
- ISO 14971:2019 (risk management for medical devices)
- OWASP ASVS v5.0
- OWASP API Security Top 10 (2023)
- OWASP LLM Top 10 (2024)
- ISPE GAMP 5 (2nd ed., 2022); GAMP GPG *AI/ML in GxP* (2024)
- PIC/S PI 041
- SLSA Supply-chain Levels for Software Artefacts

**DACH**
- BfArM (DE) — medical-device + AI-medicinal product reporting
- Swissmedic (CH)
- AGES PharmMed (AT)
- BSI IT-Grundschutz (DE) — IT-baseline-protection for K8s + AI infrastructure

**Vendor**
- NVIDIA Triton Inference Server documentation (v24.10)
- MLflow documentation (v2.18)
- Seldon Core documentation (v2.9)
- Feast documentation (v0.40)
- Istio documentation (v1.24); Kong documentation (v3.8); HashiCorp Vault documentation (v1.18)
- Sigstore / cosign documentation (v2.4)
- Prometheus, Grafana, Thanos, Loki, Tempo documentation (current)
- Okta SAML 2.0 + MFA Administrator Guide
- Splunk Universal Forwarder 9.3 documentation

## 13. Appendix A — DS → FS Traceability Matrix

| DS ID | FS ID |
|---|---|
| MOD-PROV-01 | FS-MOD-01, FS-MOD-02, FS-INT-MLFLOW-01 |
| MOD-PROV-02 | FS-PCCP-01, FS-PCCP-02, FS-PCCP-03, FS-PCCP-04, FS-MOD-04 |
| MOD-PROV-03 | FS-MOD-05, FS-TD-01, FS-TD-02, FS-TD-03 |
| MOD-PROV-04 | FS-CONF-01, FS-CONF-03, FS-CONF-04 |
| MOD-PROV-05 | FS-CONF-02 |
| MOD-PROV-06 | FS-IFU-01, FS-IFU-02, FS-IFU-03, FS-HO-05 |
| MOD-PROV-07 | FS-CARD-01, FS-CARD-02 |
| MOD-INF-01 | FS-INF-01, FS-INF-04, FS-INF-05, FS-INF-06, FS-INF-07, FS-PART11-02 |
| MOD-INF-02 | FS-INF-03, FS-AB-01, FS-AB-04, FS-INT-TRITON-01 |
| MOD-SAFE-01 | FS-INF-05, FS-AB-02 |
| MOD-SAFE-02 | FS-INF-02, FS-OBS-01, FS-OBS-02, FS-OBS-03 |
| MOD-SAFE-03 | FS-ROB-01, FS-ROB-02, FS-SEC-02, FS-SEC-06 |
| MOD-SAFE-04 | FS-INF-06, FS-CONF-DEF-01, FS-CONF-DEF-02, FS-ROB-03 |
| MOD-SAFE-05 | FS-AB-05, FS-AB-03 |
| MOD-FEAST-01 | FS-FS-01, FS-FS-02, FS-FS-03, FS-INT-FEAST-01, FS-DI-07 |
| MOD-FEAST-02 | FS-FS-04 |
| MOD-AUD-01 | FS-AUD-01, FS-AUD-02, FS-AUD-03, FS-AUD-06, FS-LOG-01, FS-LOG-03, FS-PART11-05 |
| MOD-AUD-02 | FS-LOG-04, FS-AUD-04, FS-PART11-09 |
| MOD-HO-01 | FS-HO-01, FS-FAIR-03 |
| MOD-HO-02 | FS-HO-02 |
| MOD-HO-03 | FS-HO-03, FS-HO-04, FS-HO-06 |
| MOD-PMM-01 | FS-PMM-01, FS-PMM-02, FS-PR-02 |
| MOD-PMM-02 | FS-PMM-03 |
| MOD-INC-01 | FS-INC-01, FS-INC-03, FS-INC-04 |
| MOD-INC-02 | FS-INC-02 |
| MOD-DEP-01 | FS-DEP-01, FS-DEP-03 |
| MOD-DEP-02 | FS-DEP-02 |
| MOD-REG-01 | FS-REG-01, FS-REG-02 |
| MOD-REG-02 | FS-INT-EUDAMED-01 |
| MOD-QMS-01 | FS-QMS-01, FS-QMS-02, FS-QMS-03 |
| MOD-VFM-01 | FS-VFM-01, FS-VFM-02, FS-SEC-07 |
| MOD-DSR-01 | FS-DSR-01, FS-DSR-02 |
| MOD-FAIR-01 | FS-FAIR-01, FS-FAIR-02, FS-DI-08 |
| MOD-CFG-DEF-01 | FS-CONF-DEF-01, FS-CONF-DEF-02, FS-CONF-DEF-03 |
| MOD-TRN-01 | FS-TRN-01, FS-TRN-02, FS-TRN-03, FS-TRN-04, FS-INT-OKTA-01, FS-XINT-LMS-01 |
| MOD-PR-01 | FS-PR-01, FS-PR-03, FS-PR-04 |
| DS-PLAT-DESIGN-01 | FS-PLAT-01, FS-PLAT-02, FS-PLAT-03 |
| DS-PLAT-DESIGN-02 | FS-PLAT-04 |
| DS-PLAT-DESIGN-03 | FS-PLAT-05 |
| DS-PLAT-DESIGN-04 | FS-PLAT-06, FS-PLAT-07 |
| DS-SEC-DESIGN-01 | FS-SEC-01, FS-PART11-02, FS-PART11-07 |
| DS-SEC-DESIGN-02 | FS-SEC-03, FS-PART11-12 |
| DS-SEC-DESIGN-03 | FS-SEC-04 |
| DS-SEC-DESIGN-04 | FS-SEC-05, FS-PART11-04 |
| DS-DEP-DESIGN-01 | FS-PERF-01, FS-PERF-02, FS-PERF-03, FS-PERF-04, FS-PERF-05 |
| DS-DEP-DESIGN-02 | FS-OBS-01, FS-OBS-02, FS-OBS-03 |
| DS-DEP-DESIGN-03 | FS-BAK-01, FS-BAK-02, FS-BAK-03, FS-BAK-04, FS-BAK-05 |
| DS-DEP-DESIGN-04 | FS-AUD-04, FS-AUD-05, FS-INT-SIEM-01, FS-LOG-02, FS-PART11-10 |
| DS-PART11-DESIGN-01 | FS-PART11-01, FS-PART11-03 |
| DS-PART11-DESIGN-02 | FS-PART11-06, FS-PART11-08, FS-PART11-11 |
| DS-DI-DESIGN-01 | FS-DI-01, FS-DI-02, FS-DI-03, FS-DI-04, FS-DI-05, FS-DI-06 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| DS-INT-GIT-01 | FS-INT-GIT-01, FS-PLAT-04 |
| DS-INT-DPIA-01 | FS-INT-DPIA-01 |

**Coverage footnote.** 148 of 153 FS-IDs covered. Vendor-internal FS-IDs not designed at site level: FS-INT-MLFLOW-01 (MLflow Postgres internals), FS-INT-SIEM-01 (Splunk indexing internals), FS-INT-GIT-01 (GitLab pre-receive hook internals beyond GPG-tag check), FS-MOD-06/07 (training-data lineage script internals, downstream module spec), FS-CARD-02 (model-card URL pattern is vendor-internal serving config). All cross-module DS-* rows above represent design-level rows that span infrastructure / deployment / security / DI / cross-system rather than being module-bound; see also DS § 4 / § 9 / § 10 narrative.

## 14. Design-level Risk Register

| ID | Design-stage risk | Likelihood | Impact | Bound DS-IDs / modules | Mitigation reference |
|---|---|---|---|---|---|
| D-01 | **EU AI Act Annex I non-conformance at notified-body inspection** — Annex IV pack incomplete, conformity-assessment workflow not followed, DoC missing, or CE marking applied without notified-body sign-off | Medium | **Critical (Art. 99 penalty: up to €15M or 3% global turnover)** | MOD-PROV-03, MOD-PROV-04, MOD-PROV-05, MOD-REG-01 | Annex IV pack template + completeness CI check (FS-TD-01..03); Reg-Affairs sign-off gate; annual periodic review (FS-PR-01) |
| D-02 | **Art. 14 human-oversight insufficiency** — HO Operator UI omits a model class; halt API not honoured at consumer; override not logged | Medium | **Critical (Art. 99 penalty tier)** | MOD-HO-01, MOD-HO-02, MOD-HO-03 | OQ test on `aiact-ho-monitor` coverage; consumer SDK enforces gate (FS-HO-03); LMS-recorded HO Operator training (FS-HO-04) |
| D-03 | **Art. 73 incident clock missed (15 d / 10 d / 2 d)** | Low | **Critical (Art. 99 penalty)** | MOD-INC-01, MOD-INC-02 | UTC-only internal clock + TZ-display; cron clock-advancer; PagerDuty escalation D-3 / D-1 / D0 |
| D-04 | **PCCP envelope misconfiguration** — non-conformant update auto-promoted because envelope incorrectly specified | Medium | High | MOD-PROV-02 | Annual PCCP envelope review (FS-PCCP-04); unit-tested examples for each rule |
| D-05 | **Substantial-modification Art. 43(4) trigger missed** — silently re-certified without notified-body | Low | **Critical (Art. 43)** | MOD-PROV-02, MOD-PROV-04 | PCCP predicate engine + change-control gate; Reg-Affairs alert |
| D-06 | **Annex I vs Annex III mis-classification** — model classified Annex III when it is Annex I, deadline missed | Low | **Critical (Art. 99)** | MOD-PROV-01 (`eu_aiact_classification` field) | Periodic-review classification reassessment (FS-PR-04) |
| D-07 | **Model-artefact signing-key compromise** | Low | High | MOD-VFM-01, Vault | Vault audit logs + HSM-backed key + rotation every 90 d |
| D-08 | **DB-trigger bypass for `audit_events` mutation** | Low | **Critical** | MOD-AUD-01 | DB-role enforcement (only `audit-writer` INSERT; no role UPDATE/DELETE) |
| D-09 | **Sigstore signing-service outage** during deployment window | Low | High | MOD-VFM-01, MOD-PROV-01 | Cached trusted-root + offline verification mode |
| D-10 | **Feast point-in-time correctness breach** during materialise window | Medium | High | MOD-FEAST-01 | Serialisable isolation + post-materialise verification check |
| D-11 | **Triton driver-repo update introduces non-determinism** | Low | High | MOD-INF-02, FS-PLAT-06 | Bitwise-reproducibility OQ on each driver bump |
| D-12 | **Art. 73 clock TZ miscalculation** across daylight-saving boundary | Low | **Critical** | MOD-INC-01 | UTC-only internal; OQ unit-tested all zones incl. EU + UK + US DST |
| D-13 | **Annex IV pack template drift** between releases | Medium | High | MOD-PROV-03 | Template version-pin per release + CI check |
| D-14 | **Drift monitor (PSI threshold)** mis-tuned for novel-data regime — false-negative drift | Medium | High | MOD-SAFE-02 | Annual threshold re-tune + canary-label evaluation |
| D-15 | **Adversarial-input detector** baseline drift over time — detection blind | Medium | High | MOD-SAFE-03 | Monthly envelope re-calibration |
| D-16 | **Consumer rate-limit middleware bypass** via direct Seldon API access | Low | High | MOD-CFG-DEF-01 | NetworkPolicy default-deny + Istio mTLS authorization policy |
| D-17 | **PMM consumer-incident webhook ack lost** during retransmit storm | Medium | Medium | MOD-PMM-01 | At-least-once + idempotency key + reconciliation job |
| D-18 | **DR drill misses a critical-path module** (e.g. PCCP engine state) | Low | High | MOD-PROV-02, FS-BAK-02 | DR drill checklist covers ALL `R1` modules; quarterly restore drill (FS-BAK-02) |
| D-19 | **Periodic-review orchestrator** fails to collect a new mandatory field after EU AI Act amendment | Low | High | MOD-PR-01 | Annual orchestrator-template review against current Art. 11/13/14/15/17 obligations |
| D-20 | **EU AI database registration lapse** — model goes live without Art. 49 entry | Low | **Critical (Art. 49)** | MOD-REG-01 | Registration gate before EFFECTIVE-CHAMPION promotion |
| D-21 | **Foundation-model ingest signature verification skip** under pressure | Low | **Critical (Art. 15 supply-chain)** | MOD-VFM-01 | CI gate; no manual override path in production |
| D-22 | **Cross-system Hydra LLM use-case allocation drift** — Lyrae model accidentally routed via Hydra | Low | High | Integration boundary | Egress ACL `lyr-aiml-egress-deny-llm-direct` |
| D-23 | **Cross-system Quartz AD conditional-access misconfiguration** locks out HO Operator at incident-critical moment | Low | **Critical (Art. 14)** | DS-XSYS-AD-01 | Break-glass via CyberArk PAM per FS-XSYS-AD-01 |
| D-24 | **Cross-system Aurora Backup integration** — Veeam Application-Aware misses Postgres WAL during restore drill | Low | High | DS-XSYS-BAK-01 | Monthly QA-witnessed restore test |
| D-25 | **Bias-metrics gap report** misses a sub-population (e.g. small-N stratum) | Medium | High | MOD-FAIR-01 | Quarterly review + minimum-sample-size guard |
| D-26 | **Splunk frozen-index 25-y retention** cost overrun forces silent tier-downshift | Low | **Critical** | DS-DEP-DESIGN-04 | Annual storage-cost review + Vault QA sign-off |
| D-27 | **Helios audit-publish lag** > 600 s during peak inference traffic | Medium | Medium | Cross-system integration | Prometheus `helios_publish_lag_seconds` alert; back-pressure handling |
| D-28 | **LMS competence adapter** lapses block legitimate HO Operator action at clock-critical moment | Low | High | MOD-TRN-01 | D-30 / D-7 LMS lapse alert; competence cache TTL |
| D-29 | **Kong API gateway rate-limit memory leak** causes 503 under sustained load — silent denial | Medium | Medium | Inference plane | Prometheus Kong memory metric + restart policy |
| D-30 | **Pod Security Standards `restricted` profile** blocks a future legitimate workload (e.g. CUDA-specific) | Low | Medium | DS-DEP-DESIGN-01 | Per-workload PSS exception review + Jira tracking |
| D-31 | **MLflow Postgres schema change** in upstream release breaks `models` extended-schema overlay | Medium | High | MOD-PROV-01 | MLflow version pin + schema-overlay regression test on upgrade |
| D-32 | **Notified Body identifier** captured incorrectly in MLflow record — wrong NB referenced on DoC | Low | **Critical (Art. 47)** | MOD-PROV-04, MOD-PROV-05 | NB-id validation against ISO 13485 NB-register at write |
| D-33 | **Annex IV pack export** truncated by S3 object-lock interaction during retention-period transition | Low | High | MOD-PROV-03 | Pre-export integrity check + manifest SHA-256 |
| D-34 | **GDPR DSR erasure** on training-data-resident PII conflicts with Art. 18 retention floor | Medium | High | MOD-DSR-01 | Legal-review gate before fulfilment; per-DSR-case route to anonymisation vs erasure |
| D-35 | **Substantial-modification detector** misses a manual MLflow record edit bypassing the API path | Low | **Critical** | MOD-PROV-02 | Postgres trigger on `models` UPDATE → enforced via API path only |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
