---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-27; expanded 2026-05-11 (§5 breakout + EU AI Act binding + DACH context); enriched 2026-05-12 Wave 3 Chunk I (Annex I 2027 re-classification + T4 depth uplift)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed., 2022) Cat 5 conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11"
  - "EU GMP Annex 22 (DRAFT, consultation closed October 2025) — cited as draft"
  - "ICH Q9(R1) — Quality Risk Management"
  - "ICH Q14 — Analytical Procedure Development"
  - "FDA AI/ML SaMD Action Plan (2021)"
  - "FDA Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions (August 2025)"
  - "FDA Good Machine Learning Practice for Medical Device Development — Guiding Principles (2021; subsequent guidance)"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026)"
  - "ISPE GAMP Good Practice Guide: AI/ML in GxP (2024)"
  - "EU AI Act 2024/1689 — Annex I high-risk classification (safety component of regulated product); Arts. 8–21, 26, 43, 47, 48, 49, 72, 73, 99, 113"
  - "EU MDR 2017/745 (where deployed models inform device decisions)"
  - "GDPR Reg. (EU) 2016/679 — Arts. 6, 9, 22, 32, 35"
  - "ISO/IEC 42001:2023 — Artificial Intelligence Management System"
  - "ISO/IEC 23053 — Framework for AI systems using ML"
  - "ISO/IEC 27001:2022 — Information Security Management Systems"
  - "ISO 14971:2019 — Risk Management (where applicable to SaMD)"
  - "NIST AI Risk Management Framework 1.0 (NIST AI 100-1, 2023)"
  - "NIST AI 600-1 — Generative AI Profile (July 2024) where the model serves GenAI workloads"
  - "EMA Reflection Paper on the Use of Artificial Intelligence in the Medicinal Product Lifecycle (2024)"
  - "BfArM AI guidance (DE); Swissmedic AI guidance (CH); AGES (AT)"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# User Requirements Specification (URS)

## AI / ML Model Server (GxP Inference Service) — Site-Developed FastAPI on K8s + MLflow + Seldon Core + NVIDIA Triton

**Document Number:** LYR-URS-MLSRV-001 | **Version:** 1.2 | **Effective Date:** 2026-04-27 *(synthetic)*
**Site:** Lyrae Bioworks GmbH, AI Engineering Platform, München, Germany *(fictional)*
**System Owner:** Head of AI Engineering Platforms
**Process Owner:** VP AI / Data Science
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom Application
**Project Mode:** Custom-build project — site-developed system (GAMP 5 Category 5 — Bespoke; internal SDLC). System: Site-Developed FastAPI on K8s + MLflow + Seldon Core + NVIDIA Triton.
**EU AI Act 2024/1689 classification:** **Annex I high-risk AI system** — the platform hosts ML models that act as safety components of regulated medicinal-product / medical-device decisions (PAT prediction feeding batch release; NGS variant classification feeding clinical-decision support; CV defect detection feeding sterile-product reject). High-risk-AI obligations under Arts. 8–21 apply. Conformity-assessment pathway is Annex VII (notified-body assessment) where the underlying product is a regulated medical device; otherwise inherits the medicinal-product QMS pathway (Eudralex Vol. 4 + ICH Q10). **Compliance deadline: 2 August 2027** (Annex I, 12-month extension over Annex III).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11; EU GMP Annex 22 (DRAFT); ICH Q9(R1); ICH Q14; EU AI Act 2024/1689 Arts. 8–21, 26, 43, 47, 48, 49, 72, 73, 99, 113; EU MDR 2017/745 (where applicable); GDPR Reg. (EU) 2016/679 Arts. 6, 9, 22, 32, 35; FDA AI/ML SaMD Action Plan (2021); FDA PCCP for AI-Enabled Device Software Functions (August 2025); FDA GMLP Guiding Principles (2021); FDA CSA (February 2026); ISPE GAMP GPG *AI/ML in GxP* (2024); ISO/IEC 42001:2023; ISO/IEC 23053; ISO 14971:2019; NIST AI RMF 1.0; EMA *Reflection Paper on the Use of AI in the Medicinal Product Lifecycle* (2024); BfArM (DE); Swissmedic (CH); AGES (AT).

> **Re-classification note (v1.2):** v1.1 declared Annex III + 2 August 2026. That was incorrect. Per METHODOLOGY § 2A.14, AI systems serving as safety components of a regulated medicinal product or medical-device decision are **Annex I** under EU AI Act 2024/1689, inheriting the underlying product regulation's CE-marking / conformity-assessment pathway. The compliance deadline for Annex I is **2 August 2027**, not 2026.

> **Note:** This URS covers the **inference platform** that hosts validated ML models used by GxP applications (the NIR PAT model server; the NGS variant-classification model; the CV defect-detection model registered by the Tessera Bio inspection system; document-quality classifiers). Each model has its own validation under the model SDLC; this URS defines the platform that runs them.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of AI Engineering Platforms) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (InfoSec) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs — AI/ML) | _____________ | _____________ | _____ |
| Reviewer (Notified Body Liaison — Medical Device) | _____________ | _____________ | _____ |
| Reviewer (Data Protection Officer — GDPR Art. 35 DPIA) | _____________ | _____________ | _____ |
| Approver (VP AI / Data Science) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |
| Approver (VP Regulatory Affairs) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | §5 broken out into 13 subsections; EU AI Act 2024/1689 Arts. 9–17 explicitly bound (incorrectly as Annex III); site relocated to München (DACH); BfArM + EMA AI Reflection Paper added to References; §9 Risks expanded to full table. |
| 1.2 | 2026-05-12 | (synthetic) | **Wave 3 Chunk I enrichment.** Tier T4 uplift (150–250 reqs target). EU AI Act re-classification Annex III → Annex I (deadline 2 Aug 2026 → 2 Aug 2027). New §5 subsections added: 5.2a model lifecycle Champion/Challenger A/B framework; 5.2b feature store + data lineage; 5.2c PCCP allowed-change envelope; 5.2d model retirement; 5.4a logging Art. 12 (≥ 6 mo); 5.4b transparency-to-deployers Art. 13 IFU; 5.4c Art. 15 robustness (data poisoning + model evasion + confidentiality defenses); 5.4d Art. 11 + Annex IV technical-documentation pack; 5.4e Art. 18 documentation retention (≥ 10 y after market placement); 5.4f Art. 43+47+48 conformity assessment + CE marking + EU DoC; 5.4g Art. 49 EU database registration; 5.4h Art. 72 post-market monitoring; 5.4i Art. 73 serious-incident reporting (15 d / 10 d / 2 d); 5.4j Art. 26 deployer obligations; 5.4k Art. 17 + ISO/IEC 42001 QMS; 5.9a inference observability SLO; 5.11a confidentiality-attack defenses; 5.11b model-card per Annex IV; new §9 risks for Art. 99 penalty exposure. |

## Definitions

| Term | Definition |
|---|---|
| Model Server | Site-developed inference platform (FastAPI on K8s) |
| MLflow | Model registry / experiment-tracking system |
| Seldon Core | K8s-native model deployment + traffic management |
| Triton Inference Server | NVIDIA model-serving runtime supporting multi-framework inference |
| Inference | A single prediction request against a deployed model |
| Drift | Statistical change in input or output distributions vs validation baseline |
| Data Drift | Change in distribution of input features over time |
| Concept Drift | Change in relationship between inputs and outputs (label semantics) |
| Prediction Drift | Change in distribution of model outputs |
| Champion / Challenger | A/B traffic split for staged model rollout |
| Shadow Mode | Challenger model receives traffic without affecting consumer; outputs logged for comparison |
| Feature Store | Versioned store of derived input features with point-in-time correctness |
| Model Card | Annex IV technical documentation summary (architecture, training data, performance, limitations) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| PCCP | Predetermined Change Control Plan (FDA Aug 2025 guidance for AI-Enabled Device Software Functions) |
| DPIA | Data Protection Impact Assessment (GDPR Art. 35) |
| Annex I high-risk AI | EU AI Act 2024/1689 Art. 6(1): AI as safety component of regulated product. Deadline 2 Aug 2027. |
| Annex III high-risk AI | EU AI Act 2024/1689 Art. 6(2) + Annex III: AI in one of 8 listed domains. Deadline 2 Aug 2026. |
| EU DoC | EU Declaration of Conformity (Art. 47) |
| Notified Body | Conformity-assessment body designated under EU MDR / EU AI Act Art. 43 |
| Serious Incident | EU AI Act Art. 3(49) — defined event triggering Art. 73 reporting |

## 1. Purpose

This URS defines requirements for the GxP-validated inference platform that hosts ML models used by other GxP systems. The platform is a high-risk AI system under EU AI Act 2024/1689 Art. 6(1) (Annex I — safety component of a regulated product) because the models it serves inform GxP decisions affecting patient safety and product quality. The platform also serves as the conformity-assessment-relevant computing substrate for any deployed model that is itself a Software-as-a-Medical-Device (SaMD).

## 2. Scope

**In:** site-developed FastAPI inference services on K8s; MLflow model registry (HA); Seldon Core deployment with Istio service mesh; NVIDIA Triton Inference Server for GPU-accelerated workloads (PyTorch / ONNX / TensorRT / TensorFlow); feature store (Feast); SSO via Okta + MFA; integrations with the validated GitLab (model artefact source), the Postgres metadata store, the Splunk SIEM (audit logs), and consumer GxP systems (Tessera Bio CV inspection, NIR PAT, NGS variant classifier, Lonza Procurement Mgmt, etc.). EU AI Act-mandated technical documentation per Art. 11 + Annex IV (Art. 11 pack); risk-management system per Art. 9; data-governance documentation per Art. 10; record-keeping per Art. 12 (≥ 6 mo); transparency to deployers per Art. 13 (IFU); human-oversight controls per Art. 14; accuracy + robustness + cybersecurity evidence per Art. 15; QMS per Art. 17 (aligned ISO/IEC 42001:2023); documentation retention per Art. 18 (≥ 10 y); conformity-assessment artefacts per Arts. 43, 47, 48; EU-database registration where applicable per Art. 49; post-market monitoring per Art. 72; serious-incident reporting per Art. 73; deployer obligations per Art. 26 (handed off to consumer GxP systems).

**Out:** the consumer applications (each separately validated); model training pipelines (separate URS); non-GxP shadow models (clearly marked and routed); the underlying medical-device / medicinal-product regulatory dossier (per product RA); training-data labelling tooling (separate URS).

## 3. System Description

The platform is the system of record for production ML inference in GxP contexts. Models are registered in MLflow with full provenance (training-data hash, training-code git-tag, hyperparameters, evaluation metrics, validation report, Annex IV model card). Deployment is via signed change-request to a K8s namespace; Champion / Challenger traffic management is managed via Seldon. NVIDIA Triton runs GPU-accelerated model variants with dynamic batching + concurrent model execution. Each inference request is logged with model-id + version + input checksum + output + latency + confidence. Drift monitors compare runtime distributions against validation baselines along three axes (data drift, concept drift, prediction drift); drift > threshold flags the model for re-validation. The Art. 12 logging substrate retains the events ≥ 6 months on hot storage and ≥ 10 years on cold archive (Art. 18). Art. 73 incident-reporting service routes serious incidents to BfArM / Swissmedic / AGES on the regulatory clock (15 d standard / 10 d on death / 2 d on widespread fundamental-rights infringement).

GAMP Cat 5: full SDLC + per-model validation per ICH Q9(R1) / GAMP AI/ML GPG / FDA GMLP Guiding Principles.

EU AI Act Annex I high-risk classification triggers Arts. 8–21 obligations. Each obligation is addressed by a requirement set below.

## 4. User Roles

| Role | Permissions |
|---|---|
| Model Engineer | Author / register models; cannot deploy to PROD. |
| Model Reviewer | Review models; cannot review own. |
| Model Approver (QA + AI Lead) | Approve to PROD. |
| Conformity Assessment Coordinator | Maintain Art. 11 + Annex IV technical-documentation pack; liaise with Notified Body. |
| Platform Administrator | OS / K8s / configuration; cannot approve models. |
| Consumer Application | Service-account access via mTLS; rate-limited; per-consumer authorization. |
| Auditor | Read-only across model registry, deployments, audit. |
| Human Oversight Operator (per EU AI Act Art. 14) | Real-time monitoring; ability to override or halt model output; cannot author models. |
| Post-Market Monitoring Operator (per Art. 72) | Monitor incident feeds; trigger Art. 73 escalation. |
| Data Protection Officer | Review DPIA per use case; sign off on personal-data processing. |
| Regulatory Affairs (AI/ML) | Sign Art. 47 EU DoC; manage Art. 49 EU-database registration. |

Standard SoD; Champion vs Challenger toggle requires QA co-approval. Author ≠ Approver enforced at signature level. Conformity Assessment Coordinator ≠ Model Engineer ≠ Model Approver.

## 5. User Requirements

Each requirement carries a unique ID, a priority (`H` / `M` / `L`), and a GAMP-5 risk classification (`R1` direct GxP impact / `R2` indirect / `R3` none).

### 5.1 Platform / Hardware (Cat 5 SDLC)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | K8s control plane + worker nodes shall be deployed multi-AZ with RTO ≤ 4 h and RPO ≤ 15 min. |
| URS-PLAT-02 | H | R1 | Patching cadence shall meet the site SLA: critical CVE within 7 days, high within 30 days, others within 90 days. |
| URS-PLAT-03 | H | R1 | Service traffic shall ride a dedicated VLAN; mTLS shall enforce mutual authentication between consumer and platform. |
| URS-PLAT-04 | H | R1 | Site-developed code shall be maintained under the site SDLC with code review, signed commits, and CI/CD pipeline traceability. |
| URS-PLAT-05 | M | R2 | The platform shall expose Prometheus metrics for inference latency, error rate, drift indicators, and authorisation failures. |
| URS-PLAT-06 | H | R1 | GPU nodes hosting Triton Inference Server shall be subject to NVIDIA driver-version pinning under change control; un-approved driver upgrades shall be blocked. |
| URS-PLAT-07 | M | R2 | The platform shall expose per-model GPU utilisation, memory consumption, and queue-depth metrics for capacity planning. |

### 5.2 Model Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MOD-01 | H | R1 | Each model shall be registered in MLflow with: training-data hash, training-code git-tag, hyperparameters, evaluation metrics, validation report, intended-use statement, GxP-classification flag, EU AI Act high-risk classification flag (Annex I vs III), annex-IV model-card pointer. |
| URS-MOD-02 | H | R1 | Model lifecycle states shall be DRAFT → REVIEW → APPROVED → EFFECTIVE-CHALLENGER (shadow) → EFFECTIVE-CHAMPION → DEPRECATED → RETIRED. State transitions shall require signed change records. |
| URS-MOD-03 | H | R1 | Deployment shall require Author ≠ Approver re-authenticated electronic signatures and a signed model artefact (SHA-256 + Sigstore signature). |
| URS-MOD-04 | H | R1 | A pre-approved Predetermined Change Control Plan (per FDA August 2025 guidance for Artificial Intelligence-Enabled Device Software Functions) shall govern allowed model updates; updates outside the plan shall require a new validation cycle and an EU AI Act Art. 43 substantial-modification assessment. |
| URS-MOD-05 | H | R1 | Each model shall carry an EU AI Act Art. 11 + Annex IV Technical Documentation file linked in MLflow; the file shall include the data-governance description (Art. 10), the risk-management documentation (Art. 9), the testing evidence (Art. 15), the IFU (Art. 13), and the model card. |
| URS-MOD-06 | H | R1 | Training-data lineage shall be preserved end-to-end: each training run shall link to feature-store snapshot version, raw-data SHA-256, labelling-protocol version, and bias-mitigation evidence per Art. 10. |
| URS-MOD-07 | H | R1 | Model retirement shall trigger: archival of all artefacts to immutable cold storage, retention of inference logs ≥ 10 years (Art. 18), and registry-record retention indefinitely. |

### 5.2a Champion / Challenger A/B Framework

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AB-01 | H | R1 | Challenger models shall be deployed in shadow mode by default; consumer traffic shall be served only by the Champion until the Challenger meets pre-declared promotion criteria. |
| URS-AB-02 | H | R1 | Promotion criteria shall be declared in writing per model before Challenger deployment and shall include: minimum traffic volume, statistical-significance threshold for performance comparison, no-regression bounds on safety-critical metrics. |
| URS-AB-03 | H | R1 | Traffic-split percentages shall be configurable per model; non-zero consumer-affecting splits shall require Author ≠ Approver signatures plus QA co-approval. |
| URS-AB-04 | H | R1 | Per-traffic-split inference outcomes shall be logged separately to enable post-hoc analysis; aggregation shall preserve attribution to the Champion vs Challenger model version. |
| URS-AB-05 | M | R2 | Automatic rollback shall trigger when Challenger metrics breach pre-declared safety bounds within a configurable observation window; rollback events shall be audit-logged. |

### 5.2b Feature Store + Data Lineage

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-FS-01 | H | R1 | A feature store (Feast) shall serve as the single source of truth for derived inputs used by GxP models; features shall be versioned and point-in-time correct. |
| URS-FS-02 | H | R1 | Each feature definition shall carry a SHA-256 hash, schema, source-of-truth pointer, freshness SLA, and bias-evaluation evidence per Art. 10. |
| URS-FS-03 | H | R1 | Feature mutations (definition change, source change, schema change) shall require change-control approval; downstream models pinned to the prior feature version shall continue serving until re-pinned. |
| URS-FS-04 | M | R2 | Feature-distribution drift shall be monitored separately from model-input drift; feature-drift alerts shall route to the Feature Owner role. |

### 5.2c PCCP Allowed-Change Envelope

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PCCP-01 | H | R1 | The PCCP per model shall enumerate the **modifications-only protocol (MoP)**, the **performance-and-clinical-evaluation method (PCEM)**, and the **impact assessment (IA)** per FDA August 2025 PCCP guidance. |
| URS-PCCP-02 | H | R1 | A predicate engine shall verify each model update against the PCCP envelope before allowing promotion; non-conformant updates shall block automatically. |
| URS-PCCP-03 | H | R1 | A PCCP-deviation flag shall be raised when an update is detected outside the envelope; deviations require Art. 43 substantial-modification assessment. |
| URS-PCCP-04 | M | R2 | PCCP envelopes shall be reviewed annually as part of periodic review; envelope amendments shall be re-approved by Reg Affairs + VP QA. |

### 5.3 Inference Operation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INF-01 | H | R1 | Each inference shall be logged with: request-id, consumer-id, model-id + version, input checksum, output, latency, timestamp, confidence; full input shall be retained per the GxP retention policy (≥ 25 years for clinical-impact models). |
| URS-INF-02 | H | R1 | Drift monitors shall compare runtime distributions against the validation baseline along three axes: data drift (input feature distributions), concept drift (input-output relationship), prediction drift (output distribution); drift > threshold shall raise an alert and flag the model for re-validation. The threshold and detector shall be approved per model. |
| URS-INF-03 | H | R1 | Champion / Challenger split shall be managed by Seldon; traffic-percentage changes shall require Author ≠ Approver signatures with QA co-approval. |
| URS-INF-04 | H | R1 | Inference-failure modes (model server unavailable, schema mismatch, timeout, drift-block, low-confidence-below-threshold) shall return structured errors with documented error codes; consumer GxP systems must not silently consume nulls or defaults. |
| URS-INF-05 | H | R1 | The platform shall enforce per-model confidence thresholds where applicable; outputs below threshold shall return `LOW_CONFIDENCE` and shall not be auto-consumed by GxP decisioning. |
| URS-INF-06 | H | R1 | Each inference response shall carry a deterministic `output_hash` over the response body to enable consumer-side integrity verification. |
| URS-INF-07 | M | R2 | Batch inference jobs shall be runnable with explicit batch-size, parallelism, and per-call timeout parameters; failures shall fail the batch as a whole rather than silently dropping records. |

### 5.4 Human Oversight (EU AI Act Art. 14)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HO-01 | H | R1 | A designated Human Oversight Operator shall have access to real-time inference monitoring (model id, model version, inference rate, drift indicator, error rate, confidence-distribution histogram) for all production models. |
| URS-HO-02 | H | R1 | The Human Oversight Operator shall have authority to halt a model (mark `EFFECTIVE → SUSPENDED`) without requiring a separate approval; the halt event shall be logged with reason. |
| URS-HO-03 | H | R1 | Consumer GxP systems shall not auto-approve any safety-critical or quality-critical decision based solely on model output; a documented human-in-the-loop checkpoint shall be enforced upstream of release. |
| URS-HO-04 | M | R2 | Periodic operator training shall be documented; the Human Oversight Operator role shall not be granted without role-specific training including failure-mode awareness. |
| URS-HO-05 | H | R1 | The Human Oversight Operator UI shall surface the model's declared capabilities, limits, and known failure modes (Art. 13 IFU surface) to the operator in-context with each monitored model. |
| URS-HO-06 | H | R1 | Override interventions by the Human Oversight Operator shall be recorded with reason-for-override, time, and downstream-impact assessment; override logs shall be reviewable in periodic review. |

### 5.4a Record-keeping / Logging (Art. 12)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LOG-01 | H | R1 | The platform shall automatically generate event logs covering: model state transitions, deployment events, inference requests + responses, drift detections, override interventions, configuration changes, authentication events, and Art. 73 incident triggers. |
| URS-LOG-02 | H | R1 | Logs shall be retained on hot storage **≥ 6 months** per Art. 12 minimum, and on cold archive **≥ 10 years** post market-placement per Art. 18; retention shall be policy-enforced at storage-class level. |
| URS-LOG-03 | H | R1 | Logs shall be traceable end-to-end: each event shall carry actor-id, session-id, request-id, model-id + version, timestamp (ISO 8601 with timezone), and an integrity hash. |
| URS-LOG-04 | M | R2 | Log exports for inspection shall be supported in JSON, CSV, and PDF/A-3; export shall not disrupt routine operation. |

### 5.4b Transparency to Deployers (Art. 13 IFU)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-IFU-01 | H | R1 | Each model shall carry an Instructions-for-Use (IFU) document per Art. 13 specifying: capabilities, limits, intended purpose, foreseeable misuse, accuracy / robustness / cybersecurity metrics, human-oversight measures, expected lifetime, training-data characteristics summary. |
| URS-IFU-02 | H | R1 | The IFU shall be served programmatically via `GET /model/{id}/ifu` so consumer GxP systems can fetch and surface the current IFU to deployer operators. |
| URS-IFU-03 | H | R1 | IFU updates shall be versioned; consumers shall pin to a specific IFU version and be notified of new versions via webhook. |

### 5.4c Robustness + Cybersecurity (Art. 15)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ROB-01 | H | R1 | Each high-risk model shall be tested for **data-poisoning defenses** under OQ: training-data integrity verified via hash + provenance; runtime-input outlier detection raises `ADVERSARIAL_SUSPECTED`. |
| URS-ROB-02 | H | R1 | Each high-risk model shall be tested for **model-evasion robustness** (adversarial perturbations); declared performance levels shall hold within a documented perturbation envelope. |
| URS-ROB-03 | H | R1 | **Confidentiality-attack defenses** shall include: rate limiting per consumer to deter membership-inference attacks, output post-processing to limit model-inversion leakage where applicable, no return of training-data examples in inference responses. |
| URS-ROB-04 | H | R1 | Declared accuracy + robustness metrics shall be measured per release on a locked benchmark set and recorded in the Annex IV pack; release shall be blocked if metrics regress beyond pre-declared envelopes. |
| URS-ROB-05 | M | R2 | Cybersecurity hardening per Art. 15(5) shall be evidenced against CIS Kubernetes Benchmark + OWASP API Security Top 10; non-conformities tracked. |

### 5.4d Technical Documentation Pack (Art. 11 + Annex IV)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TD-01 | H | R1 | Each high-risk model shall maintain an Annex IV technical-documentation pack containing: (a) general description, (b) detailed description of design + development including SDLC + algorithmic methods, (c) information about training / validation / test datasets per Art. 10, (d) detailed description of monitoring + functioning + control, (e) declared performance metrics + their evaluation methods, (f) risk-management documentation per Art. 9, (g) lifecycle change management evidence, (h) compliance-with-harmonised-standards statement. |
| URS-TD-02 | H | R1 | The pack shall be kept up-to-date over the model's entire deployed lifetime; lifecycle changes shall trigger pack revision under change control. |
| URS-TD-03 | M | R2 | The pack shall be exportable on demand for notified-body inspection within 1 business day. |

### 5.4e Documentation Retention (Art. 18)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RET-01 | H | R1 | All Art. 11 + Annex IV technical documentation, EU DoC, conformity-assessment records, training records, and post-market monitoring records shall be retained **at least 10 years after the model is placed on the market or put into service** per Art. 18. |
| URS-RET-02 | H | R1 | Retention enforcement shall be policy-coded at the storage-class level; deletion attempts before the retention floor shall be blocked. |

### 5.4f Conformity Assessment + CE + EU DoC (Arts. 43, 47, 48)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CONF-01 | H | R1 | Each Annex I high-risk model that constitutes a SaMD or device-safety-component shall undergo conformity assessment **before being placed on the market or put into service** per Art. 43; the pathway is Annex VII (notified-body) where the underlying product is an MDR class IIa+ device. |
| URS-CONF-02 | H | R1 | An EU Declaration of Conformity per Art. 47 shall be on file for each high-risk model; the DoC shall be signed by Regulatory Affairs (AI/ML) and shall name the provider, model, applied harmonised standards, and notified-body identifier where applicable. |
| URS-CONF-03 | H | R1 | The CE marking per Art. 48 shall be affixed (logically, via the platform's transparency surfaces) to each conformity-assessed model; the marking shall be retrievable via `GET /model/{id}/ce-marking`. |
| URS-CONF-04 | M | R2 | Substantial modifications per Art. 43(4) shall trigger renewed conformity assessment; the PCCP envelope (URS-PCCP-01..04) partitions allowed updates from substantial modifications. |

### 5.4g EU Database Registration (Art. 49)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REG-01 | H | R1 | Where a deployed model meets Annex III high-risk criteria (e.g., where models serve essential-services access decisions), the model shall be registered in the EU AI database **before placement on the market or putting into service** per Art. 49. Annex I models inherit the underlying product's existing registration (EUDAMED for MDR devices). |
| URS-REG-02 | M | R2 | Registration evidence (database entry ID, registration date) shall be linked from the MLflow record. |

### 5.4h Post-Market Monitoring (Art. 72)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PMM-01 | H | R1 | A post-market monitoring system shall actively collect performance data from deployers, evaluate compliance with Art. 9–15 obligations over the model's lifetime, and feed findings into the QMS per Art. 17. |
| URS-PMM-02 | H | R1 | PMM data sources shall include: per-inference outcomes, drift detections, override interventions, consumer-side incident reports, and field-observed failure modes. |
| URS-PMM-03 | M | R2 | PMM reports shall be generated quarterly and reviewed by Regulatory Affairs + VP QA; findings shall trigger CAPA where warranted. |

### 5.4i Serious-Incident Reporting (Art. 73)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INC-01 | H | R1 | Serious incidents per Art. 3(49) shall be reported to the market-surveillance authority within **15 days standard / 10 days if death / 2 days for widespread fundamental-rights infringement**. |
| URS-INC-02 | H | R1 | Routing shall be authority-aware: BfArM for DE-deployed contexts, Swissmedic for CH, AGES for AT, with cross-reference to EU MDR Art. 87 incident channels where the underlying product is a regulated device. |
| URS-INC-03 | H | R1 | The Art. 73 clock shall start at the moment a serious incident is identified by the provider or reported by a deployer; the clock shall be tracked per incident and surfaced to Regulatory Affairs (AI/ML). |
| URS-INC-04 | M | R2 | Incident records shall include: model id + version, deployer, timestamp, narrative, root-cause analysis status, corrective action, regulator notification status. |

### 5.4j Deployer Obligations (Art. 26)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEP-01 | H | R1 | Consumer GxP systems acting as deployers shall be contractually required to: use the model per the IFU, ensure input data is relevant and representative, assign trained human oversight (per URS-HO-05), monitor operation and suspend on identified risk, keep logs ≥ 6 months on their side, and inform workers' representatives where AI is used in workplace decisions. |
| URS-DEP-02 | H | R1 | Where a deployer is a public-body or an essential-services private deployer of an Annex III model, the deployer shall conduct a **Fundamental Rights Impact Assessment (FRIA)** before first deployment; the FRIA shall be on file with the deployer and referenced from the deployer contract. |
| URS-DEP-03 | M | R2 | The platform shall expose `GET /model/{id}/deployer-obligations` returning a structured representation of Art. 26 duties so consumer systems can drive their compliance flows. |

### 5.4k Quality Management System (Art. 17 + ISO/IEC 42001:2023)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-QMS-01 | H | R1 | The platform's QMS shall conform to EU AI Act Art. 17 (design + V&V + data management + risk management + post-market monitoring + incident reporting) and shall be aligned with ISO/IEC 42001:2023 AI Management System. |
| URS-QMS-02 | H | R1 | QMS effectiveness shall be reviewed annually by VP QA + Head of AI Engineering Platforms + Regulatory Affairs; review evidence shall feed into periodic review. |
| URS-QMS-03 | M | R2 | The QMS shall integrate with the wider site GxP QMS (ICH Q10) such that AI lifecycle changes flow through the same change-control + CAPA + deviation pipelines. |

### 5.5 Audit Trail and Records Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | The platform shall maintain a contemporaneous, time-stamped, secure audit trail capturing user, action, model-id, model-version, old value, new value, and reason-for-change for all model lifecycle transitions and traffic-management actions. |
| URS-AUD-02 | H | R1 | The audit trail shall not be editable or deletable by any user, including Platform Administrators. |
| URS-AUD-03 | H | R1 | The audit trail shall capture drift detection events, Champion ↔ Challenger transitions, model deployment + suspension events, PCCP-deviation flags, override interventions, and Art. 73 incident triggers. |
| URS-AUD-04 | H | R1 | Audit logs shall be forwarded to Splunk within 5 minutes of generation; SIEM retention shall be immutable and ≥ 25 years. |
| URS-AUD-05 | M | R2 | Audit-trail review shall be performed weekly by the System Owner (event-driven) and annually by the QA team (periodic), with documented review evidence. |
| URS-AUD-06 | H | R1 | The audit trail of the platform's own actions shall be distinguishable from logged inference events to avoid surface-area conflation under audit. |

### 5.6 21 CFR Part 11 Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a), the system shall enforce procedures and controls protecting the validity of electronic records (model artefacts, audit trails, configuration). |
| URS-PART11-02 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via Okta SSO + MFA; service-account access via mTLS only. |
| URS-PART11-03 | H | R1 | Per § 11.10(e), an operational audit trail capturing user, action, date, time shall exist for all electronic records (see § 5.5). |
| URS-PART11-04 | H | R1 | Per § 11.50, electronic signatures applied to model approval and traffic-management changes shall include signer's printed name, date and time of signing, and meaning of signature. |
| URS-PART11-05 | H | R1 | Per § 11.70, signatures shall be cryptographically linked to the signed record (model artefact + manifest); subsequent record changes shall invalidate the signature. |
| URS-PART11-06 | H | R1 | Per § 11.100, electronic signatures shall be unique to one individual and shall not be reused or reassigned. |
| URS-PART11-07 | H | R1 | Per § 11.200, re-authentication shall be required at the moment of signing (no cached credentials); session re-use shall be blocked. |
| URS-PART11-08 | H | R1 | Per § 11.300, password / credential controls shall meet site InfoSec policy: MFA mandatory, account lockout after 5 failed attempts in 15 minutes, password complexity per site standard. |
| URS-PART11-09 | H | R1 | Per § 11.10(b), the system shall be capable of producing accurate and complete copies of records in both human-readable and electronic form for inspection. |
| URS-PART11-10 | H | R1 | Per § 11.10(c), the system shall protect records for the full retention period (≥ 10 y per Art. 18; ≥ 25 y for clinical-impact contexts). |
| URS-PART11-11 | H | R1 | Per § 11.10(k), the system operation manuals and change-control records shall be maintained; SOPs shall be reviewed annually. |
| URS-PART11-12 | H | R1 | Per § 11.30, the open-system controls (encryption-in-transit, digital signatures with non-repudiation) shall apply at all internet-facing boundaries. |

### 5.7 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | **Attributable:** Every inference and every lifecycle event shall be attributed to a named user or service account. |
| URS-DI-02 | H | R1 | **Legible:** Audit trail and inference logs shall be exportable as human-readable JSON / PDF. |
| URS-DI-03 | H | R1 | **Contemporaneous:** Events shall be recorded at time of occurrence; retroactive entries shall be flagged with the actual entry timestamp and a reason-for-delay. |
| URS-DI-04 | H | R1 | **Original:** Raw inference inputs and outputs shall be preserved unaltered; derivative analyses shall reference but not overwrite the original. |
| URS-DI-05 | H | R1 | **Accurate:** Model output transformations (rescaling, thresholding) shall be deterministic and validated under OQ; non-deterministic outputs shall be flagged. |
| URS-DI-06 | M | R2 | **Complete / Consistent / Enduring / Available:** Records shall be complete (all metadata populated), chronologically consistent, retained per Art. 18 (≥ 10 y) with verified backup, and retrievable within 1 business day. |
| URS-DI-07 | H | R1 | Training data lineage shall be preserved: the training-data hash registered in MLflow shall be reproducible from the data source via documented provenance. |
| URS-DI-08 | H | R1 | Per Art. 10 data governance, training / validation / test datasets shall be **relevant, representative, statistically sound**; bias-mitigation evidence shall be documented per model. |

### 5.8 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-GIT-01 | H | R1 | Model source shall reside in validated GitLab; release tags shall be GPG-signed by the Model Engineer. |
| URS-INT-MLFLOW-01 | H | R1 | MLflow registry shall be the system of record for model metadata; registry mutations shall be audit-logged. |
| URS-INT-SIEM-01 | H | R1 | Audit logs shall be forwarded to Splunk within 5 minutes; Splunk retention shall be immutable ≥ 25 years. |
| URS-INT-OKTA-01 | H | R1 | All human authentication shall flow through site Okta SSO with MFA enforced. |
| URS-INT-DPIA-01 | H | R1 | Where models process personal data, a GDPR Art. 35 DPIA shall be on file and referenced from the model's MLflow record. |
| URS-INT-FEAST-01 | H | R1 | The feature store (Feast) shall integrate with MLflow such that each model registers the feature-store snapshot version it consumes. |
| URS-INT-TRITON-01 | H | R1 | NVIDIA Triton Inference Server shall be exposed via Seldon-managed deployments; Triton model-repository updates shall be audit-logged + signature-verified. |
| URS-INT-EUDAMED-01 | M | R2 | Where a hosted model is a SaMD component of an MDR-registered device, the platform shall publish the linkage to EUDAMED via documented reference (UDI-DI) recorded in the MLflow record. |

### 5.9 Performance and Reliability

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | Inference P95 shall be ≤ 200 ms for production-tier models under nominal load. |
| URS-PERF-02 | M | R2 | The platform shall sustain ≥ 1,000 inferences/second across all models without degradation. |
| URS-PERF-03 | H | R1 | Availability shall be ≥ 99.9% measured monthly, excluding planned maintenance announced ≥ 7 days in advance. |
| URS-PERF-04 | M | R2 | The platform shall auto-scale worker pods between 4 and 64 instances based on inference queue depth. |
| URS-PERF-05 | M | R2 | Cold-start latency for newly-promoted models shall be ≤ 30 s P95; warm-pool pre-loading shall be configurable per model. |

### 5.9a Inference Observability SLO

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-OBS-01 | H | R1 | Per-model SLOs shall be declared and tracked for: inference P95 latency, error rate, drift score, confidence-distribution shift, and accuracy on canary samples (where canary labels are available). |
| URS-OBS-02 | H | R1 | SLO breaches shall raise alerts to the Human Oversight Operator + System Owner; sustained breaches shall trigger automatic suspension per URS-AB-05. |
| URS-OBS-03 | M | R2 | SLO targets shall be reviewed per release; SLO history shall be retained for trend analysis. |

### 5.10 Backup, Restore, and Disaster Recovery

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | MLflow registry data, model artefact storage, feature-store snapshots, and audit logs shall be backed up daily with cryptographic integrity verification. |
| URS-BAK-02 | H | R1 | A documented restore test shall be performed quarterly by the Platform Administrator with witness from QA. |
| URS-BAK-03 | M | R2 | RTO shall be ≤ 4 hours for the inference plane after total-cluster failure; RPO ≤ 15 minutes for inference logs. |
| URS-BAK-04 | M | R2 | DR-site failover shall be tested annually with a tabletop exercise plus a live partial failover. |
| URS-BAK-05 | H | R1 | Cold-archive restoration of Art. 18 retention records shall be exercise-tested annually with documented retrieval times ≤ 24 hours. |

### 5.11 Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | EU AI Act Art. 15(5) cybersecurity: the platform shall be hardened per CIS K8s benchmark; non-conformities tracked under change control. |
| URS-SEC-02 | H | R1 | Model-poisoning defences: training-data integrity shall be verified via hash at registration; inference-time adversarial inputs above an anomaly threshold shall trigger alerts. |
| URS-SEC-03 | H | R1 | Container images shall be scanned for CVEs at build time and at runtime; HIGH and CRITICAL CVEs shall block deployment. |
| URS-SEC-04 | H | R1 | Secrets (DB credentials, API keys, signing keys) shall be stored in HashiCorp Vault with audit logging; no plaintext secrets in container images or configmaps. |
| URS-SEC-05 | M | R2 | The platform shall enforce Pod Security Standards (restricted profile) and NetworkPolicies isolating model namespaces. |
| URS-SEC-06 | H | R1 | EU AI Act Art. 15(4) robustness: stress-testing under representative adversarial perturbation shall be documented for high-risk models prior to deployment. |
| URS-SEC-07 | H | R1 | Supply-chain integrity: all third-party model dependencies (foundation models, pre-trained weights) shall be SBOM-tracked + signed before ingest. |

### 5.11a Confidentiality-Attack Defenses

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CONF-DEF-01 | H | R1 | Membership-inference attack mitigation: per-consumer rate limits + output post-processing shall be applied for models trained on personal data; mitigation evidence shall be in the Annex IV pack. |
| URS-CONF-DEF-02 | H | R1 | Model-inversion attack mitigation: inference outputs shall not return raw training examples; output structures shall be reviewed for inversion leakage during validation. |
| URS-CONF-DEF-03 | M | R2 | Differential-privacy or equivalent techniques shall be evaluated for models trained on sensitive personal data; the decision (apply / not apply / not applicable) shall be documented. |

### 5.11b Model Card per Annex IV

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CARD-01 | H | R1 | Each model shall publish a model card summarising: intended use, training data characteristics, evaluation metrics + benchmarks, known limitations + failure modes, deployment recommendations, regulatory classification, version, contact for questions. |
| URS-CARD-02 | H | R1 | Model cards shall be served programmatically and shall be version-pinned alongside the model artefact. |

### 5.12 Training

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | No user shall be granted production access (Model Approver, Platform Administrator, Human Oversight Operator, Post-Market Monitoring Operator, Conformity Assessment Coordinator) until role-specific training is completed and recorded in the site LMS. |
| URS-TRN-02 | M | R2 | Annual refresher training shall cover EU AI Act obligations (Arts. 8–21 + 26 + 72 + 73 + 99), model-drift handling, and incident response. |
| URS-TRN-03 | M | R2 | Consumer-application developers integrating with the platform shall complete onboarding training on structured-error handling per URS-INF-04. |
| URS-TRN-04 | M | R2 | AI literacy obligation per Art. 4 shall be evidenced for all staff interacting with AI outputs in regulated contexts; training records ≥ 5 years. |

### 5.13 Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PR-01 | H | R1 | An annual periodic review shall cover: model inventory, drift evidence, PCCP adherence, audit-trail review evidence, EU AI Act Art. 17 QMS effectiveness, ISO/IEC 42001:2023 conformance, training currency, post-market monitoring findings, and continued fitness for use. Review shall be signed by Head of AI Engineering Platforms + VP QA + Regulatory Affairs (AI/ML) + Conformity Assessment Coordinator. |
| URS-PR-02 | H | R1 | Per EU AI Act Art. 72, post-market monitoring of model performance shall be active; serious incidents shall be reported to the competent authority (BfArM for DE, Swissmedic for CH, AGES for AT) per Art. 73 within the regulatory timeline (15 d / 10 d / 2 d). |
| URS-PR-03 | M | R2 | The periodic review shall trigger model-level re-validation where drift, PCCP-deviation, or performance-degradation evidence indicates the model is no longer fit for purpose. |
| URS-PR-04 | M | R2 | Each periodic review shall reassess EU AI Act classification (Annex I vs III vs non-high-risk + Art. 50) per current model use; classification changes shall be change-controlled. |

### 5.14 Model Bias + Fairness Monitoring (Art. 10)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-FAIR-01 | H | R1 | For each high-risk model, bias-metric reporting shall be performed on a documented cadence (at minimum quarterly); metrics shall cover per-sub-population performance gaps relevant to the model's deployment context. |
| URS-FAIR-02 | H | R1 | Bias-mitigation actions (data augmentation, re-sampling, model-architecture changes) shall be tracked + their effect measured against pre-mitigation baselines. |
| URS-FAIR-03 | M | R2 | Bias evidence shall be linked from the Annex IV pack + surfaced to the Human Oversight Operator. |

### 5.15 Data-Subject Rights for AI-Processed Personal Data (GDPR Arts. 15–22)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DSR-01 | H | R1 | Where models process personal data, the platform shall support GDPR Art. 15 (right of access), Art. 17 (right to erasure where applicable), and Art. 22 (automated decision-making restrictions); request workflows shall be defined per use case. |
| URS-DSR-02 | H | R1 | Art. 22(3) safeguards (right to human intervention, right to express view, right to contest the decision) shall be operationalised via the HITL framework (URS-HO-03). |

### 5.16 Vendor Foundation-Model Provenance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VFM-01 | H | R1 | For models built atop external foundation models, the foundation-model's licence + source + version + training-data summary shall be recorded in MLflow; consumed foundation models shall be SBOM-tracked. |
| URS-VFM-02 | M | R2 | Foundation-model security advisories shall be subscribed to + alert the System Owner. |

### 5.17 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is OIDC via Entra ID with workload-identity federation for service-to-service; conditional-access policy `AI-Platform Conditional Access (FIDO2 + device-compliance + risk-based step-up)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the model-registry catalogue and MinIO/S3 object-replica for model binaries + Annex IV artefacts; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 10 y after market placement (Art. 18) per the consuming-record schedule. |

### 5.18 Cross-System Integration — LMS competence handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-LMS-01 | H | R1 | Before assigning a user to the Model Owner, Approver, or Human Oversight Operator role for any served model, the platform shall query the LMS (`VGA-URS-LMS-001`) for current training competence in the role-specific curriculum (`MLOPS-OWNER-v1.x` / `MLOPS-APPROVER-v1.x` / `HOO-v1.x`); non-current users shall be blocked from the role assignment; LMS competence shall be re-checked at every authorisation decision (max-age 24 h cache). |

## 6. Acceptance Criteria

The platform shall be accepted into validated routine GxP use when:

1. FS, CS, RA, IQ, OQ, PQ approved and executed (full Cat-5 set with explicit EU AI Act Art. 11 + Annex IV Technical Documentation pack).
2. PQ shall include representative end-to-end coverage: model registration → Annex IV pack assembly → champion rollout → drift detection → re-validation → human-oversight halt → audit-trail review → Art. 73 incident-reporting drill → cold-archive restoration.
3. EU AI Act Art. 17 QMS evidence demonstrated; ISO/IEC 42001:2023 conformance attested.
4. EU AI Act Art. 43 conformity assessment performed for each Annex I model where the deployed system meets safety-component criteria (Notified Body assessment per Annex VII where the underlying product is MDR class IIa+).
5. EU Declaration of Conformity per Art. 47 signed; CE marking surface (URS-CONF-03) verified.
6. EU database registration per Art. 49 completed where applicable.
7. VSR approved by VP AI / Data Science + VP QA + Regulatory Affairs (AI/ML) + Notified Body Liaison.
8. Site-developed code shall pass site SDLC quality gates (code review, security scan, dependency-vulnerability scan, unit + integration test coverage thresholds).
9. RTM shall demonstrate every URS requirement mapped to at least one approved test case.

## 7. Constraints

- Model SDLC shall be enforced per ICH Q9(R1) and GAMP AI/ML GPG + FDA GMLP Guiding Principles; each model shall have its own URS / FS / RA / OQ.
- The platform shall not auto-deploy any model to production without signed change-control approval.
- The platform shall not expose models classified as `non_GxP_shadow` to GxP-classified consumer applications.
- EU AI Act Annex I high-risk-AI obligations apply from **2 August 2027**; the platform shall demonstrate compliance from that date. Annex III high-risk obligations apply from 2 August 2026 for models in scope.
- Consumer GxP systems acting as deployers must adhere to Art. 26 deployer obligations; non-compliant deployers shall not be permitted access.

## 8. Assumptions

- GitLab, Okta, Splunk, K8s control plane, HashiCorp Vault, MLflow, Feast, NVIDIA Triton are themselves qualified or under qualification.
- BfArM (or relevant competent authority per Member State) is the EU AI Act market-surveillance authority for the deploying entity.
- The DPIA per GDPR Art. 35 has been performed for any model touching personal data.
- The Notified Body designated under EU MDR is engaged for conformity assessment of any model that is a SaMD or safety-component of an MDR class IIa+ device.
- The corresponding consumer GxP applications maintain their own EU AI Act Art. 26 deployer obligations.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 — Electronic Records; Electronic Signatures (§§ .10, .30, .50, .70, .100, .200, .300).
- FDA *Artificial Intelligence/Machine Learning–Based Software as a Medical Device Action Plan* (2021).
- FDA *Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions* (August 2025).
- FDA *Good Machine Learning Practice for Medical Device Development — Guiding Principles* (2021; subsequent guidance).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).

### EU — EMA / Commission
- EU GMP Annex 11 — Computerised Systems.
- EU GMP Annex 22 — Artificial Intelligence (DRAFT, consultation closed October 2025; cited as draft).
- EU AI Act 2024/1689 — **Annex I high-risk classification (Art. 6(1))**; Arts. 8 (provider duties), 9 (risk management), 10 (data governance), 11 + Annex IV (technical documentation), 12 (record-keeping ≥ 6 mo), 13 (transparency to deployers / IFU), 14 (human oversight), 15 (accuracy + robustness + cybersecurity), 17 (QMS), 18 (documentation retention ≥ 10 y after market placement), 19–21, 26 (deployer obligations + FRIA), 43 (conformity assessment), 47 (EU DoC), 48 (CE marking), 49 (EU database registration), 72 (post-market monitoring), 73 (serious-incident reporting 15 d / 10 d / 2 d), 99 (penalties €35M / €15M / €7.5M), 113 (timeline). **Annex I deadline: 2 August 2027.**
- EU MDR Reg. 2017/745 (where deployed models are SaMD components of regulated devices).
- EMA *Reflection Paper on the Use of Artificial Intelligence in the Medicinal Product Lifecycle* (2024).
- GDPR (Regulation (EU) 2016/679) — Articles 6 (lawfulness), 9 (special-category health data), 22 (automated decision-making), 32 (security), 35 (DPIA).

### DACH-specific
- BfArM (DE) — Bundesinstitut für Arzneimittel und Medizinprodukte, AI guidance for medicinal products; EU AI Act market-surveillance authority for DE.
- Swissmedic (CH) — guidance on the use of AI in regulated medicinal contexts.
- AGES (AT) — Österreichische Agentur für Gesundheit und Ernährungssicherheit.

### International — ICH / ISPE / ISO / NIST
- ICH Q9(R1) — Quality Risk Management.
- ICH Q10 — Pharmaceutical Quality System.
- ICH Q14 — Analytical Procedure Development.
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE GAMP Good Practice Guide: *AI/ML in GxP* (2024).
- ISO/IEC 42001:2023 — Artificial Intelligence Management System.
- ISO/IEC 23053 — Framework for AI systems using machine learning.
- ISO/IEC 27001:2022 — Information Security Management Systems.
- ISO 14971:2019 — Medical Devices — Application of Risk Management (where SaMD).
- NIST AI Risk Management Framework 1.0 (NIST AI 100-1, 2023).
- NIST AI 600-1 — Generative AI Profile (July 2024) where GenAI workloads are served.

### Vendor / Open-source
- NVIDIA Triton Inference Server documentation.
- MLflow Tracking + Model Registry documentation.
- Seldon Core MLOps framework documentation.
- Feast feature-store documentation.
- Sigstore / cosign artefact-signing project.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
