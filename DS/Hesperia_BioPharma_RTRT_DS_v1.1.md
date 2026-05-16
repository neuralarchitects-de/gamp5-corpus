---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (v1.0 DS corpus ship; T4 Cat 5 SDS)"
seed_corpus_basis:
  - "HSP2-FS-RTRT-001 v1.2 (parent FS, T4 Cat 5)"
  - "HSP2-URS-RTRT-001 v1.2 (parent URS, transitive)"
  - "GAMP 5 (2nd ed., 2022) Cat 5 Software Design Specification conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11"
  - "Directive 2001/83/EC Art. 51 (QP); EU AI Act Annex I (2027)"
  - "ICH Q8(R2), Q9(R1), Q10, Q11, Q12, Q13, Q14; ASTM E2476"
  - "FDA RTRT Guidance (2018); FDA Q13 Guidance (2024); EMA RTRT Reflection Paper (2012)"
  - "Swissmedic (CH); BfArM (DE); AGES (AT); ANVISA RDC 1/2024; PMDA JP G6"
  - "IEC 62304; IEC 81001-5-1; OWASP ASVS; OWASP LLM Top 10; NIST SP 800-218 SSDF; SLSA"
parent_fs:
  document_number: HSP2-FS-RTRT-001
  version: "1.2"
  file: ../../../FS_FDS/_generated/final/Hesperia_BioPharma_RTRT_FS_v1.3.md
parent_urs:
  document_number: HSP2-URS-RTRT-001
  version: "1.2"
  file: ../../../URS/_generated/final/Real_Time_Release_Testing_Platform__Hesperia_BioPharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Software Design Specification (SDS)

## Real-Time Release Testing (RTRT) Platform — Site-Developed Python on K8s + Decision-Rule Engine + Lyrae AI Inference Binding — Hesperia BioPharma Visp

**Document Number:** HSP2-DS-RTRT-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** HSP2-FS-RTRT-001 v1.2
**Parent URS:** HSP2-URS-RTRT-001 v1.2
**Site:** Hesperia BioPharma AG, Visp, Switzerland *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom / Site-Developed Application (Python on Kubernetes; consumes Lyrae AI Model Server for NIR PAT predictions; multi-jurisdiction filing-aware)
**Project Mode:** Greenfield-Cat5 (in-house Python on K8s; ICH Q12 EC-classified rule store; Lyrae AI inference binding)
**EU AI Act classification:** Annex I — high-risk obligations apply from 2027; NIR PAT predictions feed batch-release decisions (medicinal product safety implication per Annex I product-safety category)
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; EU GMP Chapter 4; Directive 2001/83/EC Art. 51 (QP); ICH Q8(R2), Q9(R1), Q10, Q11, Q12, Q13, Q14; FDA RTRT Guidance (2018); FDA Q13 Guidance (2024); EMA RTRT Reflection Paper (2012); Swissmedic (CH); BfArM (DE); AGES (AT); ANVISA RDC 1/2024 (BR); PMDA JP G6 (JP); EU AI Act Annex I (2027); IEC 62304; IEC 81001-5-1; OWASP ASVS; OWASP LLM Top 10; NIST SP 800-218 SSDF; SLSA

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (RTRT Lead) | _____________ | _____________ | _____ |
| Reviewer (Statistician / Chemometrician) | _____________ | _____________ | _____ |
| Reviewer (PAT Model Owner) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs — RTRT Filing Lead) | _____________ | _____________ | _____ |
| Reviewer (Qualified Person — EU Batch Release) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (QA Reviewer) | _____________ | _____________ | _____ |
| Reviewer (System Owner — Head of Continuous Manufacturing) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — VP Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (Head of Continuous Manufacturing) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |
| Approver (VP Regulatory Affairs) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue. Inherited Tier T4 from parent URS+FS pair. DS covers 92/92 FS-IDs; 0 FS-IDs flagged as vendor-internal — no site design surface. Full Cat 5 SDS shape per METHODOLOGY § 2B.5 (§§ 4–11). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

| Term | Definition |
|---|---|
| RTRT | Real-Time Release Testing per ICH Q8/Q10 + FDA RTRT Guidance (2018) |
| EC | Established Conditions (ICH Q12) |
| PAT | Process Analytical Technology (NIR spectroscopy via Faro instruments) |
| Lyrae | The Lyrae Bioworks AI Model Server (parent URS `LYR-URS-MLSRV-001`) — vendor-managed inference endpoint for the NIR PAT model |
| QP | Qualified Person per Directive 2001/83/EC Art. 51 |
| PSI | Population Stability Index — drift metric |
| Annex I | EU AI Act Annex I (high-risk product-safety category, applies 2027) |
| Verified by | Planned IQ / OQ / PQ test |

## 1. Purpose

This Software Design Specification (SDS) records the technical design of the Hesperia BioPharma RTRT decision platform — a site-developed Cat 5 Python-on-Kubernetes application — that consumes NIR PAT predictions from the Lyrae AI Model Server, applies ICH Q12 EC-classified decision rules, captures batch-release decisions with Annex I (2027) traceability, and integrates with Ophir CRC, Faro PAT, LabWare LIMS (via the Caelum-tenancy adapter contract), Aspen IP.21 historian, MasterControl eQMS, Veeva Vault QualityDocs, PAS-X MES, and the QP signature gateway, satisfying `HSP2-FS-RTRT-001` v1.2.

## 2. Scope

**In scope:** Cat 5 site-developed Python micro-services on Kubernetes (`rtrt-prod` namespace); decision-rule engine; multi-jurisdiction filing registry (EU / CH / DE / AT / BR / JP); PAT-model lifecycle store; control-strategy reconciliation; QP override gateway integration; regulatory-reporting service; Lyrae AI Model Server inference binding (model-version pin + prediction-confidence threshold + fallback-to-SME-review); GitOps deployment via ArgoCD; observability stack; Helios audit handover.

**Out of scope:** Lyrae AI Model Server internals (vendor — see `LYR-DS-AIMS-001`); Faro NIR instrument firmware; Aspen IP.21 internals; PAS-X MES internals; MasterControl internals; Vault internals; QP signature-gateway internals.

## 3. Architectural Overview

The RTRT platform is a Python micro-service stack deployed on Kubernetes (Hesperia private cluster, Visp site, with DR site Geneva). Decision-rule execution is gated by Established-Conditions per ICH Q12; NIR PAT predictions are consumed via the Lyrae AI Model Server with hard model-version pinning. QP override and regulator-reporting integrations are isolated services. Determinism is verified bitwise via OQ.

```
                ┌───────────────────────────────────────────────────────────────┐
                │ INPUT SOURCES                                                  │
                │  ┌──────┐  ┌──────┐  ┌──────┐  ┌──────┐  ┌──────┐  ┌────────┐ │
                │  │ Ophir │  │ Faro │  │ LIMS │  │ IP.21 │  │ Vault │  │ Lyrae   │ │
                │  │ CRC   │  │ NIR  │  │      │  │ HIST  │  │       │  │ AI Inf  │ │
                │  └──┬───┘  └──┬───┘  └──┬───┘  └──┬───┘  └──┬───┘  └──┬─────┘ │
                └─────┼─────────┼─────────┼─────────┼─────────┼─────────┼───────┘
                      │         │         │         │         │         │
                      ▼         ▼         ▼         ▼         ▼         ▼
            ┌─────────────────────────────────────────────────────────────────┐
            │  RTRT Decision Engine (Cat 5 Python on K8s — `rtrt-prod` namespace) │
            │  ┌──────────────────────────────────────────────────────────┐  │
            │  │ rtrt-api (FastAPI) — REST endpoints + auth                │  │
            │  │ rtrt-rule-loader — filing-pinned rule store               │  │
            │  │ rtrt-input-validator — completeness + freshness + EC      │  │
            │  │ rtrt-lyrae-client (HSP-LYR-CLIENT-1.x) — Lyrae binding    │  │
            │  │ rtrt-decision-engine — deterministic arithmetic           │  │
            │  │ rtrt-decision-recorder — append-only ledger writer        │  │
            │  │ rtrt-pat-model-store — PAT model lifecycle state          │  │
            │  │ rtrt-cs-reconciler — nightly CS-pack vs deployed-rule diff │  │
            │  │ rtrt-mjr — multi-jurisdiction filing registry             │  │
            │  │ rtrt-pqs-adapter — MasterControl bi-directional bridge   │  │
            │  │ rtrt-helios-publisher — audit-event Kafka producer        │  │
            │  └──────────────────────────────────────────────────────────┘  │
            └────────────────┬───────────────┬────────────────┬───────────────┘
                             │               │                │
                             ▼               ▼                ▼
                         PAS-X MES      MasterControl    QP Signature Gateway
                         (release-      (deviations /   (Art. 51 D 2001/83/EC)
                          decision)      CAPA / PQS)
                             │
                             ▼
                         Regulatory-Reporting Service
                         (Swissmedic / BfArM / AGES / ANVISA / PMDA)
```

### 3.1 Logical view (text)

The platform is a 10-component micro-service stack. `rtrt-api` is the ingress; `rtrt-decision-engine` is the deterministic core (decimal arithmetic + IEEE-754 round-mode pin); `rtrt-lyrae-client` is the only path to PAT predictions and enforces model-version pinning + endpoint mTLS; `rtrt-decision-recorder` writes the append-only PostgreSQL ledger; `rtrt-cs-reconciler` runs nightly cron to detect divergence between deployed EFFECTIVE rules and filed control-strategy pack; `rtrt-mjr` holds the per-jurisdiction filing-state machine; `rtrt-pqs-adapter` posts deviation / CAPA / PQS-metrics events to MasterControl; `rtrt-helios-publisher` emits audit events to the Helios Kafka topic.

### 3.2 Process view (deployment)

`rtrt-prod` namespace deploys each component as a Kubernetes Deployment with HPA scaling (2–16 worker pods on queue depth). ArgoCD manages GitOps from `git.hesperia.local/rtrt/rtrt-platform`. Container images are signed via cosign; CVE gate blocks HIGH / CRITICAL via OPA-policy in ArgoCD.

### 3.3 Technology view

| Layer | Choice |
|---|---|
| Language | Python 3.11 |
| Framework | FastAPI 0.115 |
| Container | OCI images (Wolfi base); signed via cosign |
| Orchestrator | Kubernetes 1.29 (Hesperia private cluster, Visp + DR Geneva) |
| GitOps | ArgoCD 2.13 |
| Database | PostgreSQL 16 (decision ledger; partitioned by month) |
| Object store | S3 (Object Lock COMPLIANCE; input-snapshot archive) |
| Stream | Kafka 3.7 (Helios audit topic) |
| Observability | Prometheus + Grafana + OpenTelemetry + Splunk SIEM |
| Identity | Okta SAML 2.0 + MFA + OIDC for service tokens |
| Secrets | HashiCorp Vault |
| License | site-internal proprietary (Cat 5 Hesperia-developed) |

---

## 4. Software Architecture

### 4.1 Logical-view components

| Component | Responsibility | Key interactions |
|---|---|---|
| `rtrt-api` | REST ingress + Okta authN/authZ + rate-limit | Inbound: clients; Outbound: decision-engine, mjr, pat-model-store |
| `rtrt-rule-loader` | loads filing-pinned EFFECTIVE rules at start; refresh on rule-promotion event | Reads: PostgreSQL `decision_rules`; writes: in-memory cache |
| `rtrt-input-validator` | input completeness + freshness + EC-range check | Reads: Ophir / Faro / LIMS / IP.21 / Vault; writes: decision input snapshot |
| `rtrt-lyrae-client` (`HSP-LYR-CLIENT-1.x`) | Lyrae AI inference client; enforces model-version pin + mTLS + drift handling | Outbound: Lyrae inference endpoint |
| `rtrt-decision-engine` | deterministic decision computation | Reads: rule cache + input snapshot; calls `rtrt-lyrae-client` |
| `rtrt-decision-recorder` | writes immutable decision record + input-snapshot pointer to S3 | Writes: PostgreSQL + S3 |
| `rtrt-pat-model-store` | PAT-model lifecycle state machine (`DRAFT/CALIBRATED/CROSS-VALIDATED/APPROVED/EFFECTIVE/OBSOLETE`) | Writes: PostgreSQL `pat_model_versions` |
| `rtrt-cs-reconciler` | nightly cron — compare deployed EFFECTIVE rules vs filed CS pack | Outbound: critical PQS event on divergence |
| `rtrt-mjr` | per-jurisdiction filing registry; variation state machine | Reads/writes: PostgreSQL `filing_registry` |
| `rtrt-pqs-adapter` | bi-directional bridge to MasterControl | Outbound: MasterControl REST; inbound: webhook |
| `rtrt-helios-publisher` | Kafka producer for audit events | Outbound: Helios Kafka topic |

### 4.2 Process-view (deployment topology) — ASCII

```
         Kubernetes 1.29 — Hesperia Visp cluster (DR: Geneva)
         ──────────────────────────────────────────────────────
         namespace: rtrt-prod

         ┌─────────────────────────────────────────────────────┐
         │ Ingress (NGINX Ingress Controller + cert-manager)   │
         └───────────────────────┬─────────────────────────────┘
                                 │ TLS 1.3 + mTLS
                                 ▼
         ┌─────────────────────────────────────────────────────┐
         │ rtrt-api Deployment (replicas: 2-4 HPA)             │
         └───────┬──────────┬───────────┬───────────┬─────────┘
                 │          │           │           │
                 ▼          ▼           ▼           ▼
         ┌─────────┐ ┌──────────┐ ┌─────────────┐ ┌──────────┐
         │ rtrt-   │ │ rtrt-    │ │ rtrt-input- │ │ rtrt-mjr │
         │ rule-   │ │ decision-│ │ validator   │ │          │
         │ loader  │ │ engine   │ │             │ │          │
         │ (2)     │ │ (2-16)   │ │ (2-8)       │ │ (2)      │
         └─────────┘ └────┬─────┘ └─────────────┘ └──────────┘
                          │
                          ▼
                  ┌───────────────┐
                  │ rtrt-lyrae-   │ ──► Lyrae AI Model Server
                  │ client (2-8)  │      (mTLS + Entra workload-identity)
                  └───────────────┘

         ┌──────────────────┐   ┌────────────────┐
         │ rtrt-decision-   │   │ rtrt-pat-model-│
         │ recorder (2)     │   │ store (1)      │
         └──┬──────────┬────┘   └────────────────┘
            │          │
            ▼          ▼
       PostgreSQL    S3 Object Lock (COMPLIANCE)
       (partitioned  ── input-snapshot archive
        decision     ── ≥ 25 y retention
        ledger)

         ┌────────────────┐  ┌────────────────┐  ┌─────────────────┐
         │ rtrt-cs-       │  │ rtrt-pqs-      │  │ rtrt-helios-    │
         │ reconciler     │  │ adapter        │  │ publisher       │
         │ (CronJob)      │  │ (2)            │  │ (2)             │
         └────────────────┘  └────────────────┘  └─────────────────┘
                                                          │
                                                          ▼
                                              Kafka 3.7 (Helios)
```

### 4.3 Technology view + Lyrae AI Model Server inference-endpoint configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-K8S-01 | Cluster (`K8S_CLUSTER`) | Hesperia private K8s 1.29; Visp primary + Geneva DR | Custom | Per FS-AV-02 + FS-BAK-04 | FS-AV-01, FS-AV-02 | IQ-K8S-01 |
| DS-K8S-02 | Namespace (`NAMESPACE`) | `rtrt-prod` | Custom | Workload isolation | FS-SEC-04 | OQ-NS-01 |
| DS-K8S-03 | Pod-Security profile | `restricted` | Default | Hardening | FS-SEC-04 | OQ-POD-SEC-01 |
| DS-K8S-04 | NetworkPolicy | deny-by-default; named allow-rules per service | Custom | Hardening | FS-SEC-04 | OQ-NETPOL-01 |
| DS-K8S-05 | HPA worker bounds (`DECISION_ENGINE_HPA`) | min 2, max 16 on queue depth | Custom | Per FS-AV-02 | FS-AV-02 | PQ-HPA-01 |
| DS-K8S-06 | Image signing (`COSIGN_KEY`) | cosign Sigstore key per Hesperia rotation | Custom | Supply chain | FS-DEV-03 | OQ-COSIGN-01 |
| DS-K8S-07 | GitOps controller | ArgoCD 2.13 + OPA-policy CVE gate (HIGH / CRITICAL block) | Custom | Per FS-DEV-03 + FS-DEV-06 | FS-DEV-03, FS-DEV-06 | OQ-ARGO-OPA-01 |
| DS-LYR-EP-01 | Lyrae inference endpoint (`CI-LYR-ENDPOINT`) | `https://lyrae-prod.hesperia.local/api/v1/infer` | Custom | Per FS-XINT-LYR-01 | FS-XINT-LYR-01 | OQ-LYR-EP-01 |
| DS-LYR-EP-02 | Lyrae transport | mTLS + Entra workload-identity (managed cert) | Custom | Per FS-XINT-LYR-01 | FS-XINT-LYR-01 | OQ-LYR-MTLS-01 |
| DS-LYR-EP-03 | Lyrae model-alias request shape (`MODEL_ALIAS_TPL`) | `NIR-PAT-<product>`; non-matching aliases rejected | Custom | Per FS-XINT-LYR-01 | FS-XINT-LYR-01 | OQ-LYR-ALIAS-01 |
| DS-LYR-EP-04 | Lyrae model-version pin enforcement | runtime checks `Lyrae.model_version == effective_rule.pat_model_version`; mismatch → `PAT_MODEL_VERSION_MISMATCH` | Custom | Per FS-PMOD-02 + FS-XINT-LYR-01 | FS-PMOD-02, FS-XINT-LYR-01 | OQ-PAT-VERSION-PIN-01 |
| DS-LYR-EP-05 | Lyrae inference SLO (`CI-LYR-SLO`) | P95 ≤ 750 ms; P99 ≤ 2000 ms; APM probe `apm-hsp-lyr-latency` | Custom | Per FS-XINT-LYR-02 | FS-XINT-LYR-02 | PQ-LYR-LAT-01 |
| DS-LYR-EP-06 | SLO-breach action | state-machine transition `RTRT_FALLBACK`; MasterControl deviation pushed | Custom | Per FS-XINT-LYR-02 | FS-XINT-LYR-02 | OQ-LYR-SLO-BREACH-01 |
| DS-LYR-EP-07 | Lyrae model-card + envelope pre-release gate | reads `GET /models/{alias}/card` + `GET /models/{alias}/pccp/envelope`; evaluates `model_version ∈ approved_envelope` AND `intended_use ∋ {product, strength, route}`; pins model-card + envelope JSON to batch dossier | Custom | Per FS-XINT-LYR-03 | FS-XINT-LYR-03 | OQ-LYR-CARD-GATE-01 |
| DS-LYR-EP-08 | Lyrae drift webhook | subscribed via OIDC; payload `lyrae.drift.v1`; consumer-rule: PSI > 0.20 OR distribution-shift KS > threshold OR ground-truth lag > 7 d → safety-net override | Custom | Per FS-XINT-LYR-04 | FS-XINT-LYR-04 | OQ-LYR-DRIFT-01 |
| DS-LYR-EP-09 | Prediction-confidence threshold (`PCT_NIR_PAT`) | configurable per product; default `0.90` (90% prediction-confidence floor); below threshold triggers fallback-to-SME-review via deviation push (per Annex I (2027) "human-in-the-loop" expectation for AI-assisted regulated decisions) | Custom | Per EU AI Act Annex I obligation | FS-RUN-03, FS-PMOD-03 | OQ-PCT-THRESHOLD-01 |
| DS-LYR-EP-10 | Fallback-to-SME-review rule | confidence < `PCT_NIR_PAT` OR `RTRT_FALLBACK` state OR drift-override → batch routed to manual SME review path (traditional release) + MasterControl deviation `RTRT_FALLBACK_<reason>` | Custom | Per FS-RUN-03 + FS-PMOD-03 + Annex I | FS-RUN-03, FS-PMOD-03 | OQ-SME-FALLBACK-01 |
| DS-LYR-EP-11 | Helios pre-handover retention (Lyrae path) | RTRT side retains Lyrae inference events ≥ 2 y before Helios system-of-record | Custom | Per FS-XINT-LYR-05 | FS-XINT-LYR-05 | OQ-LYR-RETENTION-01 |
| DS-DB-01 | PostgreSQL version | 16 | Custom | LTS | FS-DEV-02 | IQ-PG-01 |
| DS-DB-02 | Decision ledger partition strategy | monthly partitions on `decision_ts` | Custom | Performance + retention | FS-AUD-04 | OQ-PG-PARTITION-01 |
| DS-DB-03 | Encryption-at-rest | AES-256 via cluster volume encryption | Custom | InfoSec | FS-SEC-02 | IQ-ENCRYPTION-01 |
| DS-S3-01 | S3 bucket (`RTRT_RAW_BUCKET`) | `s3://hesperia-rtrt-raw` Object Lock COMPLIANCE; ≥ 25 y | Custom | Immutable input archive | FS-AUD-04, FS-BAK-01 | IQ-S3-OBJLOCK-01 |
| DS-OBS-01 | Observability stack | Prometheus + Grafana + OpenTelemetry + Splunk SIEM | Custom | Per FS-PERF-01 + FS-AV-01 | FS-PERF-01, FS-AV-01 | OQ-OBSERVABILITY-01 |
| DS-OBS-02 | Prometheus histogram for decision latency (`rtrt_decision_latency_seconds`) | P95 ≤ 60 s alert | Custom | Per FS-PERF-01 | FS-PERF-01 | PQ-DECISION-LAT-01 |

---

## 5. Module Decomposition

| Module ID | Module | Responsibility | Interface (exposes) | Dependencies | Owner | GxP-criticality | FS-IDs traced |
|---|---|---|---|---|---|---|---|
| MOD-API-01 | `rtrt-api` | REST ingress; auth; rate-limit | FastAPI routes per § 8 | `rtrt-decision-engine`, `rtrt-mjr`, `rtrt-pat-model-store` | RTRT Platform Team | R1 | FS-DEV-01, FS-PART11-02 |
| MOD-RL-01 | `rtrt-rule-loader` | filing-pinned rule cache | `load_rules()`, `refresh()` | PostgreSQL `decision_rules` | RTRT Platform Team | R1 | FS-RULE-01, FS-RULE-04 |
| MOD-INPUT-01 | `rtrt-input-validator` | completeness + freshness + EC-range pre-check | `validate(input_snapshot) -> ValidationResult` | `rtrt-rule-loader`, Ophir/Faro/LIMS/IP.21/Vault clients | R1 | RTRT Platform Team | FS-RUN-02, FS-RUN-03 |
| MOD-LYR-01 | `rtrt-lyrae-client` (`HSP-LYR-CLIENT-1.x`) | Lyrae inference + model-version-pin enforcement + drift handling | `infer(model_alias, payload) -> Prediction`; `get_card(alias)`, `get_envelope(alias)` | Lyrae endpoint via mTLS | RTRT Platform Team + PAT Model Owner | R1 | FS-XINT-LYR-01..05, FS-PMOD-02..03 |
| MOD-DEC-01 | `rtrt-decision-engine` | deterministic decision computation (`decimal` + IEEE-754 round-mode pin) | `compute(rule, input_snapshot) -> DecisionRecord` | `rtrt-rule-loader`, `rtrt-input-validator`, `rtrt-lyrae-client` | RTRT Platform Team | R1 | FS-DEV-04, FS-RUN-01..06, FS-RULE-01..06 |
| MOD-REC-01 | `rtrt-decision-recorder` | immutable decision-record writer | `record(decision) -> RecordId` | PostgreSQL + S3 | RTRT Platform Team | R1 | FS-AUD-01..03, FS-RUN-01 |
| MOD-PAT-01 | `rtrt-pat-model-store` | PAT-model lifecycle state machine | `transition(model_id, new_state, signers[]) -> Transition`; `read(model_id)` | PostgreSQL `pat_model_versions` | PAT Model Owner | R1 | FS-PMOD-01..05 |
| MOD-CS-01 | `rtrt-cs-reconciler` | nightly CS-pack vs deployed-rule diff | CronJob `reconcile_at(ts)` | `rtrt-rule-loader`, Vault QualityDocs | R1 | Regulatory Affairs Lead | FS-CS-01..03 |
| MOD-MJR-01 | `rtrt-mjr` | multi-jurisdiction filing registry + variation state machine | `record_filing(jurisdiction, state)`, `gate_for_market(rule_id, market)` | PostgreSQL `filing_registry` | Regulatory Affairs Lead | R1 | FS-MJR-01..04, FS-RULE-05..06 |
| MOD-PQS-01 | `rtrt-pqs-adapter` | bi-directional bridge to MasterControl | `push_deviation(...)`, `push_capa(...)`, webhook handler | MasterControl REST | RTRT Platform Team | R1 | FS-PQS-01..03 |
| MOD-HEL-01 | `rtrt-helios-publisher` | Kafka audit-event producer | `publish(event) -> ack` | Kafka 3.7; schema-registry | RTRT Platform Team | R2 | FS-XINT-HEL-01..02 |
| MOD-QP-01 | `rtrt-qp-gateway-client` | QP signature-gateway client | `override(decision_id, reason)` | QP Gateway service | RTRT Platform Team | R1 | FS-RUN-05, FS-INT-QP-01 |
| MOD-REG-01 | `rtrt-reg-reporter` | regulatory-reporting state machine | `notify(jurisdiction, payload)` | per-CA endpoints in `reg_reporting_config.yaml` | Regulatory Affairs Lead | R1 | FS-INT-REG-01, FS-RULE-05 |
| MOD-RECON-01 | `rtrt-reconstruct` | decision-reconstruction tool | CLI `reconstruct --decision-id <id>` | S3 + PostgreSQL | RTRT Platform Team | R1 | FS-RUN-06 |
| MOD-LIMS-01 | `rtrt-lims-read` (`HSP-LIMS-READ-1.x`) | LIMS read adapter | `get_results(batch_id) -> Result[]` | LabWare LIMS REST | RTRT Platform Team | R1 | FS-XINT-LIMS-01..02 |
| MOD-MES-01 | `rtrt-mes-release` (`HSP-MES-CTX-1.x`) | MES release-signal publisher + context fetcher | `release(batch_id, decision_id)`, `get_context(batch_id)` | PAS-X MES REST | RTRT Platform Team | R1 | FS-XINT-MES-01..02, FS-INT-MES-01 |

---

## 6. Data Model Design

### 6.1 PostgreSQL schema (decision ledger)

| Table | Columns | Constraints | Retention | Encryption |
|---|---|---|---|---|
| `decision_rules` | `rule_id PK, rule_version, state, control_strategy_version FK, ec_class, approved_range_min, approved_range_max, approved_ranges_per_jurisdiction (JSONB), pat_model_version FK, signers JSONB, created_at, effective_from, obsoleted_at` | UNIQUE `(rule_id, rule_version)`; NOT NULL state | life-of-system + 25 y | AES-256 at-rest |
| `pat_model_versions` | `model_id PK, model_alias, model_version, state, calibration_evidence_urn, cross_validation_evidence_urn, signers JSONB, created_at, effective_from, obsoleted_at` | UNIQUE `(model_alias, model_version)` | life-of-system + 25 y | AES-256 |
| `decision_records` | `decision_id PK, batch_id, rule_id FK, rule_version, input_snapshot_s3_uri, input_snapshots JSONB, lyrae_prediction JSONB, lyrae_model_version, lyrae_pccp_envelope JSONB, confidence_score, decision (release/hold/oos/fallback), confidence_interval, timestamps_iso8601 JSONB, qp_override JSONB?, created_at` | NOT NULL all critical fields; partitioned monthly on `created_at` | ≥ 25 y per EU GMP Ch. 4 | AES-256 |
| `audit_events` | `event_id PK, actor_id, action, old JSONB, new JSONB, reason, ts_utc, ts_local, source_system, source_record_id` | append-only via trigger; UPDATE/DELETE blocked | ≥ 25 y | AES-256 |
| `filing_registry` | `filing_id PK, jurisdiction (enum: EU/CH/DE/AT/BR/JP), control_strategy_version, document_refs JSONB, approval_date, status (enum: SUBMITTED/UNDER_REVIEW/APPROVED/IMPLEMENTED/OBSOLETE)` | UNIQUE `(jurisdiction, control_strategy_version)` | life-of-system + 25 y | AES-256 |
| `variation_state` | `variation_id PK, rule_id FK, jurisdiction, state, submitted_at, decided_at, decision_evidence_urn` | NOT NULL all critical | ≥ 25 y | AES-256 |
| `cs_reconcile_log` | `reconcile_id PK, run_ts, deployed_rule_ids[], filed_cs_version, divergences JSONB, status (clean/divergent), reviewer_id?, reviewed_at?` | append-only | ≥ 25 y | AES-256 |
| `lyrae_drift_events` | `event_id PK, model_alias, model_version, psi, ks_statistic, ground_truth_lag_days, severity, ts_utc, override_action JSONB` | append-only | ≥ 25 y | AES-256 |

### 6.2 Message schemas

| Schema | Format | Use |
|---|---|---|
| `rtrt.decision.v1` | JSON Schema | internal decision-record envelope |
| `rtrt.fallback.v1` | JSON Schema | MasterControl deviation payload for `RTRT_FALLBACK_*` |
| `lyrae.drift.v1` | JSON Schema (Lyrae-owned) | inbound webhook from Lyrae |
| `eqms.ticket.v1` | JSON Schema | MasterControl CAPA push payload |
| `helios.audit.v1` | Avro (schema-registry pinned) | Kafka envelope per FS-XINT-HEL-01 |
| `veridian.batch.release.v1` | JSON Schema | outbound to PAS-X MES |
| `caelum.lims.result.amended.v1` | JSON Schema (Caelum-owned) | inbound LIMS-amendment webhook |

### 6.3 Data classification

| Class | Data | Storage |
|---|---|---|
| GxP-critical | decision_records, audit_events, pat_model_versions, decision_rules, filing_registry | PostgreSQL + S3 Object Lock |
| GxP-supporting | cs_reconcile_log, variation_state, lyrae_drift_events | PostgreSQL |
| Non-GxP | observability metrics, application logs | Prometheus + SIEM |
| PII | none expected; QP / Approver `actor_id` is employee-ID only (no health data) | – |

---

## 7. Algorithm + Calculation Design

### 7.1 Decision-rule evaluation (deterministic arithmetic)

| Algorithm | Input | Output | Procedure |
|---|---|---|---|
| `evaluate_rule(rule, snapshot, lyrae_prediction)` | rule + input snapshot + Lyrae prediction | DecisionRecord(release/hold/oos/fallback, confidence_interval) | (1) verify input completeness; (2) verify EC-range per `approved_ranges_per_jurisdiction[batch.markets]` — most-restrictive selected; (3) verify Lyrae prediction confidence ≥ `PCT_NIR_PAT` (90% default); (4) evaluate rule expression using `decimal.Decimal` for currency-class arithmetic + IEEE-754 `decimal.ROUND_HALF_EVEN` for fp; (5) if any check fails → `fallback`; (6) record |

**Numerical precision:** all decision-critical arithmetic uses `decimal.Decimal` with `Context(prec=28, rounding=ROUND_HALF_EVEN)`. Floating-point quantities from Lyrae predictions are cast to Decimal with explicit precision before comparison. Bitwise-reproducibility verified via OQ-DEV-04.

**Edge cases:**
- Missing input field → fallback with reason `INPUT_INCOMPLETE`
- Input freshness exceeded (configured staleness window) → fallback with reason `INPUT_STALE`
- Lyrae timeout (P99 > 2000 ms) → fallback with reason `LYRAE_SLO_BREACH`
- Lyrae model-version mismatch → fallback with reason `PAT_MODEL_VERSION_MISMATCH`
- Multi-jurisdiction range conflict → use most-restrictive range; record decision with all jurisdiction ranges in record

### 7.2 PAT-model drift monitoring (per ASTM E2476)

| Metric | Formula | Threshold | Action |
|---|---|---|---|
| Residual | `sum((y_true - y_pred)^2) / n` over rolling N-batch window | `> 2σ baseline` | warning |
| Hotelling T² | per ASTM E2476 § 6.3 | window-dependent | warning |
| Q-statistic | per ASTM E2476 § 6.4 | window-dependent | warning |
| Sustained OOS (3 of 5 windows) | – | – | `PAT_MODEL_OOS` event → batches in-flight fallback to traditional release |

### 7.3 CS-pack reconciliation algorithm

| Algorithm | Input | Output | Procedure |
|---|---|---|---|
| `reconcile_cs_pack()` | EFFECTIVE rules in `decision_rules`; filed CS pack via Vault URN | divergence report | (1) fetch filed CS pack via Vault URN resolver; (2) compare deployed EFFECTIVE rules' `control_strategy_version` and `ec_class` ranges against filed pack; (3) any divergence raises critical PQS event (`CS_PACK_DRIFT`) + halts new-rule promotion until reviewed |

### 7.4 Drift handler

| Algorithm | Trigger | Action |
|---|---|---|
| `handle_drift(drift_event)` | inbound Lyrae webhook `lyrae.drift.v1` | (1) parse PSI, KS, ground-truth-lag; (2) if PSI > 0.20 OR KS > threshold OR ground-truth-lag > 7 d → safety-net override: any in-flight decision uses fallback path; (3) write override evidence packet `{batch_id, model_version, drift_metrics, override_user, override_ts}` to batch record; (4) raise MasterControl deviation |

### 7.5 QP override

| Algorithm | Trigger | Action |
|---|---|---|
| `qp_override(decision_id, reason)` | QP-authenticated POST to `/decision/{id}/override` | (1) verify QP role + ADCS certificate; (2) verify re-auth (fresh 5-min token); (3) record override + reason ≥ 100 chars; (4) decision is final |

---

## 8. Interface + API Design

### 8.1 RTRT REST API (FastAPI on `rtrt-api`)

| Method + Path | AuthN | Request schema | Response schema | Rate limit | Errors | Audit event |
|---|---|---|---|---|---|---|
| `POST /decisions` | Okta SAML 2.0 + MFA + service token | `{batch_id, rule_id, input_overrides?}` | `{decision_id, decision, confidence, ts}` | 100/min/user | 400 INPUT_INCOMPLETE; 409 RULE_OUT_OF_FILING; 503 LYRAE_SLO_BREACH | `rtrt.decision.created` |
| `GET /decisions/{decision_id}` | Okta + role `RTRT-Viewer` | – | `DecisionRecord` | 1000/min | 404 NOT_FOUND | – |
| `POST /decisions/{decision_id}/override` | Okta + role `QP` + ADCS cert + fresh 5-min token | `{reason: ≥100 chars}` | `{override_id, ts}` | 10/min | 403 NOT_QP; 401 REAUTH_REQUIRED | `rtrt.decision.qp_override` |
| `POST /rules` | Okta + role `Rule-Author` | `{rule_id, rule_version, ec_class, approved_range_min, approved_range_max, approved_ranges_per_jurisdiction, pat_model_version, signers[3]}` | `{rule_id, rule_version, state=DRAFT}` | 50/day | 400 RULE_INVALID; 403 NOT_AUTHOR | `rtrt.rule.created` |
| `POST /rules/{rule_id}/promote` | Okta + role `Rule-Approver` ≠ Author + 3 JWTs (QA + Mfg Head + Reg Affairs) | `{new_state}` | `{rule_id, state}` | 50/day | 403 SOD_VIOLATION; 409 VARIATION_PENDING | `rtrt.rule.promoted` |
| `POST /pat-models` | Okta + role `PAT-Model-Owner` | `{model_alias, model_version, calibration_evidence_urn, cross_validation_evidence_urn}` | `{model_id, state=DRAFT}` | 20/day | 400 INVALID | `rtrt.pat_model.created` |
| `POST /pat-models/{model_id}/transition` | Okta + 3 JWTs (Statistician + PAT-Model-Owner + QA) | `{new_state, signers[3]}` | `{model_id, state}` | 20/day | 403 SOD_VIOLATION | `rtrt.pat_model.transition` |
| `GET /reports/filings/{jurisdiction}` | Okta + role `Reg-Affairs` | – | PDF/A-3 or JSON | 100/min | – | – |
| `GET /reconstruct/{decision_id}` | Okta + role `RTRT-Auditor` | – | `ReconstructionResult` | 10/min | 404 NOT_FOUND | `rtrt.reconstruct.requested` |

OpenAPI artefact: `git.hesperia.local/rtrt/rtrt-platform/docs/openapi.yaml` (generated from FastAPI; pinned per release).

### 8.2 Inbound webhooks

| Path | Source | Schema | Idempotency | Action |
|---|---|---|---|---|
| `POST /webhooks/lyrae/drift` | Lyrae AI Model Server | `lyrae.drift.v1` | event-id-based | invoke `handle_drift()` |
| `POST /webhooks/eqms/status` | MasterControl | `eqms.status.v1` | event-id-based | update CAPA-status state |
| `POST /webhooks/lims/amended` | LabWare LIMS (Caelum tenancy) | `caelum.lims.result.amended.v1` | event-id-based | raise deviation `HSP-LIMS-AMEND-AFTER-RELEASE` |

### 8.3 Outbound clients (per-counterparty)

| Counterparty | Adapter | Protocol | AuthN | Idempotency |
|---|---|---|---|---|
| Lyrae AI Inference (FS-XINT-LYR-01) | `HSP-LYR-CLIENT-1.x` | HTTPS + mTLS + Entra workload-identity | client cert | request-id-based |
| Ophir CRC | `rtrt-ophir-client` | REST + webhook | mTLS | event-id-based |
| Faro NIR (FS-INT-PAT-01) | `rtrt-pat-grpc-client` | gRPC | mTLS | – |
| LabWare LIMS (FS-XINT-LIMS-01) | `HSP-LIMS-READ-1.x` | REST | mTLS + bearer | – |
| Aspen IP.21 (FS-INT-HIST-01) | `rtrt-pi-client` | PI Web API | bearer | – |
| Vault QualityDocs (FS-INT-VAULT-01) | `rtrt-vault-client` | REST | mTLS + bearer | – |
| MasterControl (FS-INT-EQMS-01) | `rtrt-pqs-adapter` (MOD-PQS-01) | REST | mTLS + bearer | event-id-based |
| PAS-X MES (FS-XINT-MES-01) | `HSP-MES-CTX-1.x` | REST | mTLS | `{batch_id, release_decision_id}` |
| QP Gateway (FS-INT-QP-01) | `rtrt-qp-gateway-client` | REST | mTLS + ADCS QP-cert | decision-id-based |
| Regulatory Reporting (FS-INT-REG-01) | `rtrt-reg-reporter` | per-CA REST | per-CA cert (signed REST) | submission-id-based |
| Helios (FS-XINT-HEL-01) | `rtrt-helios-publisher` | Kafka 3.7 | mTLS + SASL | `{source_system, event_id}` |

### 8.4 SLOs + error budgets

| SLO | Target | Window | Action on breach |
|---|---|---|---|
| RTRT decision latency P95 | ≤ 60 s | 5-min rolling | Prometheus alert; pager |
| Lyrae inference P95 (`apm-hsp-lyr-latency`) | ≤ 750 ms | 5-min rolling | state-machine transition `RTRT_FALLBACK` + deviation |
| Decision throughput | ≥ 10 decisions/min sustained | per campaign | HPA scales worker pods 2–16 |
| Availability | ≥ 99.9% during campaigns | rolling 30-day | DR + incident response |
| Audit-event publish lag | ≤ 600 s | 5-min | Prometheus alert; reconciliation |

---

## 9. Security Design

### 9.1 AuthN flow

```
[User] → Okta SAML 2.0 → ID token → rtrt-api
         ↓ MFA (TOTP / WebAuthn)
         ↓ token issued with role-claim
[Service] → SPIFFE/SPIRE identity → mTLS → counterparty
            ↓ Entra workload-identity for Lyrae
```

Re-auth max-age: 300 s (5 min) for all signing operations. ADCS-issued hardware-token QP-certificate required for QP-override signing per FS-XSYS-AD-01.

### 9.2 AuthZ model

- Role-based: `RTRT-Viewer`, `RTRT-Auditor`, `Rule-Author`, `Rule-Approver`, `PAT-Model-Owner`, `Statistician`, `QA-Approver`, `QP`, `Reg-Affairs`, `Mfg-Head`, `Platform-Admin`, `RTRT-Fallback-Approver`
- SoD: `Rule-Author ∩ Rule-Approver = ∅`; rule-approval requires 3 signed JWTs from `(QA-Approver, Mfg-Head, Reg-Affairs)`; PAT-model transition requires 3 JWTs from `(Statistician, PAT-Model-Owner, QA-Approver)`
- Attribute / claim mapping: Okta role-claims → in-process RBAC enforcement at every endpoint

### 9.3 Secret management

- Store: HashiCorp Vault (`kv/rtrt/*`)
- Rotation cadence: 90 d for service tokens; 24 h for break-glass via CyberArk PAM
- mTLS certs: cert-manager auto-renewal; alert at T-30 d

### 9.4 Transport security

- TLS: 1.3 floor (1.2 transitional support disabled by 2026-07-01)
- Cipher suite floor: `TLS_AES_256_GCM_SHA384`, `TLS_CHACHA20_POLY1305_SHA256`
- mTLS for all service-to-service traffic + Lyrae endpoint

### 9.5 Audit-trail event taxonomy

| Event type | Trigger | Payload fields | Helios-published |
|---|---|---|---|
| `rtrt.decision.created` | `POST /decisions` | decision_id, batch_id, rule_id+version, lyrae_model_version, confidence, decision | Yes |
| `rtrt.decision.qp_override` | QP override | decision_id, qp_actor_id, reason | Yes |
| `rtrt.rule.created` | `POST /rules` | rule_id, version, author | Yes |
| `rtrt.rule.promoted` | `POST /rules/{id}/promote` | rule_id, new_state, signers[] | Yes |
| `rtrt.rule.signed` | per JWT issuance | signer_id, signature_hash | Yes |
| `rtrt.pat_model.transition` | model lifecycle change | model_id, new_state, signers[] | Yes |
| `rtrt.fallback.triggered` | confidence < threshold OR Lyrae SLO breach OR drift | decision_id, reason, drift_metrics? | Yes |
| `rtrt.cs.reconcile_divergent` | `rtrt-cs-reconciler` finds drift | reconcile_id, divergences | Yes |
| `rtrt.config.changed` | platform config edit | actor_id, change-diff | Yes |
| `rtrt.security.auth_failed` | failed authN | actor_id, ip, reason | Yes |

---

## 10. Deployment Architecture

### 10.1 Container / VM topology

Kubernetes 1.29 cluster; `rtrt-prod` namespace; 13 services (deployments) per § 4.2; HPA bounds per service per FS-AV-02; pod-security `restricted` per FS-SEC-04; network-policy deny-by-default with named allow-rules.

### 10.2 Orchestration + scaling

- Orchestrator: Kubernetes 1.29 (Hesperia private cluster, Visp + Geneva DR)
- GitOps: ArgoCD 2.13 from `git.hesperia.local/rtrt/rtrt-platform`
- Image registry: Hesperia private OCI registry; cosign-signed; OPA-policy in ArgoCD blocks HIGH / CRITICAL CVEs (Trivy + Snyk in CI; cert-manager-renewed certificates)
- Scaling: `rtrt-decision-engine` HPA 2–16 on queue depth; `rtrt-lyrae-client` HPA 2–8

### 10.3 Observability

| Layer | Tool | Configuration |
|---|---|---|
| Logs | Splunk SIEM | RFC 5424 syslog index `gxp-rtrt`; ≤ 5 min lag |
| Metrics | Prometheus + Grafana | scrape interval 15 s; retention 90 d hot + 25 y cold via Thanos |
| Traces | OpenTelemetry | 10% sample rate; head sampling on decision-id |
| SIEM target | Splunk `gxp-rtrt` | per FS-XSYS-AD-01 |

### 10.4 Disaster recovery

| Component | RPO | RTO | DR site | Restore sequence |
|---|---|---|---|---|
| PostgreSQL decision ledger | ≤ 15 min | ≤ 4 h | Geneva | pg_basebackup + WAL replay; restore-cert to eQMS |
| S3 input-snapshot archive | ≤ 1 min (S3 replication) | ≤ 1 h | geo-replicated | failover region |
| Kubernetes workloads | ≤ 5 min | ≤ 4 h | Geneva | ArgoCD re-sync from Git |
| Lyrae endpoint | – | – | vendor-managed | failover per Lyrae DR plan |

Annual DR test: tabletop + live partial failover per FS-BAK-04.

---

## 11. Module Specification Table

Per METHODOLOGY § 2B.5.8, the full Module Specification artefact lives downstream as `<DOC-PREFIX>-MS-<DOMAIN>-NN`; the DS only references it.

| Module ID | Module | Class / file pointer (in `git.hesperia.local/rtrt/rtrt-platform`) | Unit-test ref | Module Spec ID |
|---|---|---|---|---|
| MOD-API-01 | `rtrt-api` | `src/rtrt_api/main.py` (FastAPI app) | `tests/unit/api/test_routes.py` | `HSP2-MS-API-01` |
| MOD-RL-01 | `rtrt-rule-loader` | `src/rtrt_rule_loader/loader.py` | `tests/unit/rule_loader/test_loader.py` | `HSP2-MS-RL-01` |
| MOD-INPUT-01 | `rtrt-input-validator` | `src/rtrt_input_validator/validator.py` | `tests/unit/input/test_validator.py` | `HSP2-MS-INPUT-01` |
| MOD-LYR-01 | `rtrt-lyrae-client` | `src/rtrt_lyrae_client/client.py` (Pydantic v2 models) | `tests/unit/lyrae/test_client.py` + `tests/contract/test_lyrae_contract.py` | `HSP2-MS-LYR-01` |
| MOD-DEC-01 | `rtrt-decision-engine` | `src/rtrt_decision/engine.py` (Decimal-based arithmetic) | `tests/unit/decision/test_engine.py` + `tests/determinism/test_bitwise.py` | `HSP2-MS-DEC-01` |
| MOD-REC-01 | `rtrt-decision-recorder` | `src/rtrt_decision/recorder.py` | `tests/unit/decision/test_recorder.py` | `HSP2-MS-REC-01` |
| MOD-PAT-01 | `rtrt-pat-model-store` | `src/rtrt_pat_model/store.py` | `tests/unit/pat/test_store.py` | `HSP2-MS-PAT-01` |
| MOD-CS-01 | `rtrt-cs-reconciler` | `src/rtrt_cs_reconciler/reconciler.py` | `tests/unit/cs/test_reconciler.py` | `HSP2-MS-CS-01` |
| MOD-MJR-01 | `rtrt-mjr` | `src/rtrt_mjr/registry.py` | `tests/unit/mjr/test_registry.py` | `HSP2-MS-MJR-01` |
| MOD-PQS-01 | `rtrt-pqs-adapter` | `src/rtrt_pqs/adapter.py` | `tests/unit/pqs/test_adapter.py` | `HSP2-MS-PQS-01` |
| MOD-HEL-01 | `rtrt-helios-publisher` | `src/rtrt_helios/publisher.py` | `tests/unit/helios/test_publisher.py` | `HSP2-MS-HEL-01` |
| MOD-QP-01 | `rtrt-qp-gateway-client` | `src/rtrt_qp/client.py` | `tests/unit/qp/test_client.py` | `HSP2-MS-QP-01` |
| MOD-REG-01 | `rtrt-reg-reporter` | `src/rtrt_reg_reporter/service.py` | `tests/unit/reg/test_reporter.py` | `HSP2-MS-REG-01` |
| MOD-RECON-01 | `rtrt-reconstruct` | `src/rtrt_reconstruct/cli.py` | `tests/unit/reconstruct/test_cli.py` | `HSP2-MS-RECON-01` |
| MOD-LIMS-01 | `rtrt-lims-read` | `src/rtrt_lims/reader.py` | `tests/contract/test_lims_contract.py` | `HSP2-MS-LIMS-01` |
| MOD-MES-01 | `rtrt-mes-release` | `src/rtrt_mes/release.py` | `tests/contract/test_mes_contract.py` | `HSP2-MS-MES-01` |

---

## 12. References

### US
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- FDA *Guidance for Industry: Real Time Release Testing* (2018)
- FDA *Guidance for Industry: Q13 Continuous Manufacturing of Drug Substances and Drug Products* (2024)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EU GMP Chapter 4
- Directive 2001/83/EC Art. 51 (QP)
- EMA *Reflection Paper on Real Time Release Testing* (2012)
- **EU AI Act (Regulation (EU) 2024/1689) — Annex I (high-risk product-safety category)** — applies 2027; obligations Arts. 9–18, 26, 43, 47–49, 50, 72, 73, 99 (penalty tier up to €15M / 3% global turnover for high-risk non-compliance; €35M / 7% applies only to prohibited Art. 5 practices, not in scope here)

### DACH
- Swissmedic (CH) — release-decision filing
- BfArM (DE) — release-decision filing per Anlage 7
- AGES (AT) — release-decision filing

### International
- ICH Q8(R2), Q9(R1), Q10, Q11, Q12 (Established Conditions), Q13, Q14
- ANVISA RDC 1/2024 (BR)
- PMDA JP G6 (JP)
- ASTM E2476 *Standard Guide for the Control and Monitoring of PAT Models*
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE GAMP GPGs *Records & Data Integrity*, *PAT*, *RTRT*
- IEC 62304 (medical-device software lifecycle — referenced for SDLC discipline)
- IEC 81001-5-1 (security of health software)
- OWASP ASVS; OWASP LLM Top 10 (Lyrae-binding LLM-class threat surfaces)
- NIST SP 800-218 SSDF
- SLSA (Supply-chain Levels for Software Artifacts) — target SLSA Level 3
- PIC/S PI 041
- ISO/IEC 27001:2022

### Vendor
- Lyrae Bioworks — *AI Model Server Inference Endpoint Reference* (parent URS `LYR-URS-MLSRV-001`)
- Ophir — *CRC API Reference*
- Faro — *NIR Spectrometer gRPC API Reference*
- Aspen Technology — *IP.21 PI Web API Reference*

---

## 13. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-K8S-01 | FS-AV-01, FS-AV-02 |
| DS-K8S-02 | FS-SEC-04 |
| DS-K8S-03 | FS-SEC-04 |
| DS-K8S-04 | FS-SEC-04 |
| DS-K8S-05 | FS-AV-02 |
| DS-K8S-06 | FS-DEV-03 |
| DS-K8S-07 | FS-DEV-03 |
| DS-LYR-EP-01 | FS-XINT-LYR-01 |
| DS-LYR-EP-02 | FS-XINT-LYR-01 |
| DS-LYR-EP-03 | FS-XINT-LYR-01 |
| DS-LYR-EP-04 | FS-PMOD-02, FS-XINT-LYR-01 |
| DS-LYR-EP-05 | FS-XINT-LYR-02 |
| DS-LYR-EP-06 | FS-XINT-LYR-02 |
| DS-LYR-EP-07 | FS-XINT-LYR-03 |
| DS-LYR-EP-08 | FS-XINT-LYR-04 |
| DS-LYR-EP-09 | FS-RUN-03, FS-PMOD-03 |
| DS-LYR-EP-10 | FS-RUN-03, FS-PMOD-03 |
| DS-LYR-EP-11 | FS-XINT-LYR-05 |
| DS-DB-01 | FS-DEV-02 |
| DS-DB-02 | FS-AUD-04 |
| DS-DB-03 | FS-SEC-02 |
| DS-S3-01 | FS-AUD-04, FS-BAK-01 |
| DS-OBS-01 | FS-PERF-01, FS-AV-01 |
| DS-OBS-02 | FS-PERF-01 |
| MOD-API-01 | FS-DEV-01, FS-PART11-02 |
| MOD-RL-01 | FS-RULE-01, FS-RULE-04 |
| MOD-INPUT-01 | FS-RUN-02, FS-RUN-03 |
| MOD-LYR-01 | FS-XINT-LYR-01, FS-XINT-LYR-02, FS-XINT-LYR-03, FS-XINT-LYR-04, FS-XINT-LYR-05, FS-PMOD-02, FS-PMOD-03 |
| MOD-DEC-01 | FS-DEV-04, FS-RUN-01, FS-RUN-02, FS-RUN-03, FS-RUN-04, FS-RUN-05, FS-RUN-06, FS-RULE-01, FS-RULE-02, FS-RULE-03, FS-RULE-04, FS-RULE-05, FS-RULE-06 |
| MOD-REC-01 | FS-AUD-01, FS-AUD-02, FS-AUD-03, FS-RUN-01 |
| MOD-PAT-01 | FS-PMOD-01, FS-PMOD-02, FS-PMOD-03, FS-PMOD-04, FS-PMOD-05 |
| MOD-CS-01 | FS-CS-01, FS-CS-02, FS-CS-03 |
| MOD-MJR-01 | FS-MJR-01, FS-MJR-02, FS-MJR-03, FS-MJR-04, FS-RULE-05, FS-RULE-06 |
| MOD-PQS-01 | FS-PQS-01, FS-PQS-02, FS-PQS-03 |
| MOD-HEL-01 | FS-XINT-HEL-01, FS-XINT-HEL-02 |
| MOD-QP-01 | FS-RUN-05, FS-INT-QP-01 |
| MOD-REG-01 | FS-INT-REG-01, FS-RULE-05 |
| MOD-RECON-01 | FS-RUN-06 |
| MOD-LIMS-01 | FS-XINT-LIMS-01, FS-XINT-LIMS-02 |
| MOD-MES-01 | FS-XINT-MES-01, FS-XINT-MES-02, FS-INT-MES-01 |

(Additional DS-IDs implicitly covered through Module IDs above include all `MOD-` rows; the table per METHODOLOGY § 2B.2 lists DS-IDs as design choices — the per-module SDLC/security/observability design captured in §§ 4–10 maps each Module to its parent FS-IDs.)

Auxiliary DS-ID → FS-ID rows for cross-cutting design choices captured in §§ 9–10:

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-SEC-AUTH-01 | FS-PART11-02, FS-PART11-06, FS-PART11-07 |
| DS-SEC-SIG-01 | FS-PART11-04, FS-PART11-05 |
| DS-SEC-PASS-01 | FS-PART11-08 |
| DS-SEC-VAULT-01 | FS-SEC-02 |
| DS-SEC-TLS-01 | FS-SEC-01 |
| DS-SEC-AT-01 | FS-AUD-01, FS-AUD-02, FS-AUD-05 |
| DS-OPS-LOGS-01 | FS-XSYS-AD-01 |
| DS-OPS-METRICS-01 | FS-PERF-01, FS-AV-01 |
| DS-OPS-DR-PG-01 | FS-BAK-01, FS-BAK-02, FS-BAK-03 |
| DS-OPS-DR-S3-01 | FS-BAK-01 |
| DS-OPS-DR-K8S-01 | FS-BAK-04 |
| DS-AT-PUBLISH-01 | FS-XINT-HEL-01, FS-XINT-HEL-02 |
| DS-PR-01 | FS-PR-01, FS-PR-02 |
| DS-TRN-01 | FS-TRN-01 |
| DS-TRN-02 | FS-TRN-02 |
| DS-DI-01 | FS-DI-01 |
| DS-DI-02 | FS-DI-02 |
| DS-DI-03 | FS-DI-03 |
| DS-DI-04 | FS-DI-04 |
| DS-DI-05 | FS-DI-05 |
| DS-DI-06 | FS-DI-06 |
| DS-INT-CRC-01 | FS-INT-CRC-01 |
| DS-INT-PAT-01 | FS-INT-PAT-01 |
| DS-INT-LIMS-NATIVE-01 | FS-INT-LIMS-01 |
| DS-INT-HIST-01 | FS-INT-HIST-01 |
| DS-INT-VAULT-01 | FS-INT-VAULT-01 |
| DS-INT-EQMS-01 | FS-INT-EQMS-01 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 |
| DS-XSYS-AD-02 | FS-XSYS-AD-01 |
| DS-XSYS-AD-03 | FS-XSYS-AD-01 |
| DS-XSYS-AD-04 | FS-XSYS-AD-01 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| DS-XSYS-BAK-02 | FS-XSYS-BAK-01 |
| DS-XSYS-BAK-03 | FS-XSYS-BAK-01 |
| DS-XSYS-BAK-04 | FS-XSYS-BAK-01 |

---

## 14. Design-level Risk Register

| ID | Design-level risk | Origin (DS-ID / design choice) | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|---|
| DR-01 | Rule executes outside filed range without variation due to MJR market-gate miss | DS-LYR-EP-04 + MOD-MJR-01 | Medium | Critical | OQ-MJR-MARKET-GATE-01 + OQ-LYR-VERSION-PIN-01 |
| DR-02 | Silent input gap leads to decision on incomplete data (MOD-INPUT-01 false-pass) | MOD-INPUT-01 | Medium | Critical | Completeness OQ + freshness OQ |
| DR-03 | Decision-rule defect releases off-spec batch | MOD-DEC-01 | Low | Critical | ≥ 90% unit-test coverage + 3-JWT promotion gate |
| DR-04 | Floating-point non-determinism produces inconsistent decisions across pod restarts | DS-DB-02 + MOD-DEC-01 | Low | High | `decimal.Decimal` + IEEE-754 round-mode pin; OQ bitwise-reproducibility (1000× canonical) |
| DR-05 | Out-of-design-space not detected by validator (EC-range miss) | MOD-INPUT-01 + MOD-MJR-01 | Low | Critical | Most-restrictive-range rule + auto-deviation trigger |
| DR-06 | QP override unavailable during production (cert expiry / gateway outage) | MOD-QP-01 | Low | Critical | cert-manager auto-renewal + monitoring + manual fallback runbook |
| DR-07 | Audit-trail tampering by privileged user (DBA role) | DS-DB-02 + MOD-REC-01 | Low | Critical | DB trigger UPDATE/DELETE block; DBA dual-control |
| DR-08 | Variation lag — rule effective before regulator approval | MOD-MJR-01 + FS-PR-02 | Low | High | Variation-tracking gate; per-jurisdiction state machine |
| DR-09 | PAT model drift consumed without re-validation | MOD-LYR-01 + MOD-PAT-01 | Medium | High | model-version pin + T²/Q monitoring + drift webhook handler |
| DR-10 | Decision rendering latency exceeds campaign cycle time (P95 breach) | DS-OBS-02 + MOD-DEC-01 | Low | Medium | HPA 2-16 + Prometheus alert |
| DR-11 | Backup / restore failure during disaster (Geneva DR) | DS-OPS-DR-PG-01 | Low | High | Annual DR test; PostgreSQL pg_basebackup + WAL replay |
| DR-12 | Control-strategy document drift between filed + production references | MOD-CS-01 | Low | High | Nightly reconciliation + halt-promotion on divergence |
| DR-13 | Multi-jurisdiction rule application to wrong market (BR rule applied to EU batch) | MOD-MJR-01 + DS-LYR-EP-04 | Low | Critical | Market-gate OQ scenario + per-jurisdiction enum |
| DR-14 | PAT model retraining bypasses lifecycle gates (rogue model deployment) | MOD-PAT-01 | Low | High | 3-JWT transition gate + Lyrae model-version pin |
| DR-15 | Lyrae endpoint mTLS cert renewal failure → all decisions stall | DS-LYR-EP-02 | Low | High | cert-manager + 30-day expiry alert |
| DR-16 | Lyrae returns incorrect model_version (vendor regression) | DS-LYR-EP-04 + MOD-LYR-01 | Low | Critical | Runtime pin verification → reject prediction; contract test in CI |
| DR-17 | **EU AI Act Annex I (2027) non-conformance** — NIR PAT prediction without prediction-confidence threshold enforcement leads to AI-driven release without human-in-the-loop fallback; Article 99 penalty exposure up to €15M / 3% global turnover for high-risk non-compliance | DS-LYR-EP-09 + DS-LYR-EP-10 + MOD-LYR-01 | Low | Critical | `PCT_NIR_PAT = 0.90` threshold + automatic SME-fallback rule + OQ-PCT-THRESHOLD-01; quarterly AI Act compliance review (Art. 9 risk management) |
| DR-18 | Annex I (2027) Art. 26 "post-market monitoring" obligation gap — drift events not surfaced to PMS | DS-LYR-EP-08 + MOD-PQS-01 | Medium | High | Drift webhook → PQS adapter → MasterControl deviation; quarterly Annex I post-market review |
| DR-19 | Annex I (2027) Art. 12 "logging" obligation gap — decision-event audit trail missing required `model_version + pccp_envelope` fields | DS-LYR-EP-07 + § 6.1 schema | Low | High | Schema column NOT-NULL; OQ-AUDIT-COVERAGE-AI-01 |
| DR-20 | Annex I (2027) Art. 14 "human oversight" gap — QP override path not exercised due to UX friction | MOD-QP-01 | Low | High | UX monitoring of QP-override path; annual exercise PQ-QP-OVERRIDE-01 |
| DR-21 | Floating-point reproducibility breaks when Python 3.11 → 3.12 lands a `math.fsum` change | DS-DB-01 + MOD-DEC-01 | Low | High | Decimal-only path; Python-version pin; regression suite |
| DR-22 | Helios Kafka producer back-pressure stalls decision-recorder | MOD-HEL-01 + MOD-REC-01 | Low | Medium | Local buffer + Prometheus `helios_publish_lag_seconds` alert; decoupled write path |
| DR-23 | Lyrae drift-webhook payload schema change breaks handler | DS-LYR-EP-08 | Low | High | Schema-registry pinning + contract test in CI |
| DR-24 | MasterControl webhook outage stalls disposition closed-loop | MOD-PQS-01 | Low | Medium | Retry + DLQ + manual unblock workflow |
| DR-25 | LIMS amendment after release missed → released batch retains stale LIMS result | MOD-LIMS-01 | Low | High | LIMS-amendment webhook subscription + deviation `HSP-LIMS-AMEND-AFTER-RELEASE` |
| DR-26 | PAS-X release-signal idempotency collision (`{batch_id, release_decision_id}`) | MOD-MES-01 | Low | Medium | Idempotency uniqueness + DLQ at 10 attempts |
| DR-27 | ArgoCD OPA CVE-policy bypass (HIGH/CRITICAL slips into prod) | DS-K8S-07 + FS-DEV-06 | Low | High | Layered scan (Trivy + Snyk + cosign verify) |
| DR-28 | Reg-reporting service variation-gate race — rule promoted while variation pending | MOD-REG-01 + MOD-MJR-01 | Low | High | Variation-state machine check at promotion time |
| DR-29 | Decision-reconstruction tool gives non-deterministic result when re-run | MOD-RECON-01 | Low | High | Deterministic-input replay test; OQ-RECONSTRUCT-01 |
| DR-30 | S3 Object Lock COMPLIANCE retention policy prevents legitimate redaction of mistakenly-included PII (none expected but design-stage risk) | DS-S3-01 | Low | Medium | Pre-write PII-scrubber; legal-hold policy CR-controlled |

The full formal Risk Assessment is `HSP2-RA-RTRT-001` (synthetic, separate document).

---

## 15. Appendix B — Lyrae AI Inference Binding Design Narrative (Annex I (2027) — High-Risk AI System)

### 15.1 Why this is the load-bearing design surface

The Lyrae AI Model Server binding is the single most consequential design boundary in this Cat 5 system: it is the only path through which NIR PAT predictions enter the batch-release decision flow. Under EU AI Act Annex I (2027), this binding crosses the threshold from "AI-assisted analytics" to "high-risk AI system used as safety component of a regulated product," triggering Article 9 (risk management), Article 12 (logging), Article 13 (transparency), Article 14 (human oversight), Article 26 (post-market monitoring), Article 47 (conformity), Article 50 (transparency to deployers), Article 72 (post-market monitoring plan), and Article 99 (penalty tier up to €15M / 3% global turnover for high-risk non-compliance — the €35M / 7% cap applies only to prohibited Art. 5 practices, not in scope here) obligations from 2027.

This appendix documents how the design choices in §§ 4–10 satisfy each Annex I obligation without bolt-on retrofits.

### 15.2 Mapping of Annex I obligations to design choices

| AI Act Article | Obligation | Design choice in this DS |
|---|---|---|
| Art. 9 (Risk Management) | Continuous risk management throughout AI system lifecycle | `MOD-PAT-01` lifecycle states (`DRAFT/CALIBRATED/CROSS-VALIDATED/APPROVED/EFFECTIVE/OBSOLETE`) with 3-JWT transitions enforce risk-review at every state change; `MOD-CS-01` nightly reconciliation surfaces divergence as critical PQS event; DR-17 risk-register entry tracks Annex I non-conformance |
| Art. 12 (Logging) | Automatic event logging across lifecycle | `audit_events` table (append-only DB trigger) + `lyrae_drift_events` + `decision_records` with `lyrae_model_version` + `lyrae_pccp_envelope` + `confidence_score` columns NOT-NULL; Helios Kafka publisher provides immutable downstream archive |
| Art. 13 (Transparency) | Information to deployers | Decision-reconstruction tool `rtrt-reconstruct` (MOD-RECON-01) replays any historical decision deterministically; `GET /reports/filings/{jurisdiction}` exports per-CA-formatted reports |
| Art. 14 (Human Oversight) | Meaningful human oversight at all times | DS-LYR-EP-09 prediction-confidence threshold (`PCT_NIR_PAT = 0.90` default) automatically routes low-confidence batches to SME-review fallback; DS-LYR-EP-10 fallback rule covers SLO breach + drift override + threshold floor; QP override endpoint (MOD-QP-01) provides ultimate human authority |
| Art. 26 (Post-Market Monitoring — general) | Implement post-market plan | `MOD-PQS-01` pushes drift events + override events to MasterControl PQS dashboard; `lyrae_drift_events` table feeds quarterly review |
| Art. 47 (Conformity Assessment) | Conformity assessment by notified body for Annex I high-risk AI systems | Conformity assessment scope = the integrated RTRT + Lyrae system; this DS plus `LYR-DS-AIMS-001` constitute the technical-documentation evidence per Annex IV; conformity assessment lives in a separate `<DOC-PREFIX>-CONFORMITY-NN` artefact (out-of-scope here) |
| Art. 50 (Transparency to Deployers) | Inform deployers about model performance + limits | Lyrae `GET /models/{alias}/card` returned card pinned in decision record (DS-LYR-EP-07); intended-use envelope validated at every decision |
| Art. 72 (Post-Market Monitoring Plan) | Documented PMM plan | Linked to `HSP-PMM-RTRT-001` (out of scope here; cross-referenced) |
| Art. 99 (Penalties) | Up to €15M / 3% global turnover for high-risk non-compliance (the €35M / 7% tier covers prohibited Art. 5 practices only, not in scope for this Annex I safety-component system) | DR-17 design-level risk register entry; AI Act non-conformance is the highest-criticality risk in this DS |

### 15.3 Threshold-driven fallback design: numerical detail

The `PCT_NIR_PAT` prediction-confidence threshold is the single most important design parameter under Annex I, because it determines when AI inference is permitted to influence release decisions vs when human review is mandatory. Design choices:

- **Default value: 0.90 (90% prediction-confidence floor).** Selected based on validated NIR PAT model performance during qualification campaigns (cross-validation R² ≥ 0.95; prediction interval ≤ ±2σ for assay attribute; 90% confidence floor preserves ≥ 95% sensitivity for spec-violating batches).
- **Per-product configurability via `decision_rules.approved_ranges_per_jurisdiction`.** Products with narrower spec windows may carry a tighter threshold (e.g., 0.95) per filed control-strategy version.
- **Threshold change requires 3-JWT rule promotion (QA + Mfg Head + Reg Affairs).** Threshold is treated as an EC; out-of-range threshold loads are rejected.
- **Below-threshold behaviour: hard fallback, no soft warning.** Decision rendered as `fallback`; MasterControl deviation `RTRT_FALLBACK_LOW_CONFIDENCE` raised; batch enters manual SME-review path (traditional release per FDA RTRT 2018 + EU GMP Annex 11).
- **Audit-trail capture: every fallback persists `lyrae_prediction` + `confidence_score` + `lyrae_pccp_envelope` JSON for post-hoc analysis.**

### 15.4 Drift handling — design-level pseudocode

```python
def handle_drift(event: LyraeDriftEvent) -> DriftAction:
    # Per ASTM E2476 + Annex I Art. 14 (human oversight)
    is_psi_alert = event.psi > 0.20
    is_ks_alert  = event.ks_statistic > KS_THRESHOLD_PER_MODEL[event.model_alias]
    is_gt_lag    = event.ground_truth_lag_days > 7

    if is_psi_alert or is_ks_alert or is_gt_lag:
        # Safety-net override: in-flight + new decisions route to fallback
        Override.activate(
            model_alias=event.model_alias,
            model_version=event.model_version,
            scope="all in-flight decisions",
            reason=event.severity,
            override_user="system",
            override_ts=now_utc(),
        )
        # Push deviation to MasterControl PQS
        pqs_adapter.push_deviation(
            category=f"PAT_MODEL_DRIFT_{event.severity}",
            evidence={...},
            criticality="Critical" if (is_psi_alert and is_ks_alert) else "Major",
        )
        # Log to lyrae_drift_events (append-only)
        drift_log.append(event)
        # Halt new EFFECTIVE rule deployment pending PAT Model Owner review
        rule_loader.halt_promotion(scope=event.model_alias)
        return DriftAction.SAFETY_NET_OVERRIDE
    else:
        # Sub-threshold drift: surveillance only
        drift_log.append(event)
        return DriftAction.MONITOR_ONLY
```

Deterministic operation guaranteed: `decimal.Decimal` for all float comparisons; KS-threshold table loaded at start + immutable until next rule promotion; OQ verifies bitwise reproducibility on canonical drift-event corpus.

### 15.5 Conformity-assessment evidence package (DS contribution)

This DS contributes the following evidence to the Annex I conformity-assessment package per Annex IV:

1. **Technical documentation** — this DS + `LYR-DS-AIMS-001` + `HSP2-MS-LYR-01`
2. **Risk-management documentation** — § 14 Design-level Risk Register + downstream FMEA `HSP2-RA-RTRT-001`
3. **Logging architecture** — § 9.5 Audit-trail event taxonomy + § 6.1 schema
4. **Human-oversight measures** — DS-LYR-EP-09, DS-LYR-EP-10, MOD-QP-01, § 5 SoD
5. **Accuracy + robustness measures** — MOD-DEC-01 determinism + MOD-INPUT-01 freshness/EC checks
6. **Cybersecurity measures** — § 9 Security Design (TLS 1.3 + mTLS + Vault + restricted PSP)
7. **Post-market monitoring** — MOD-PQS-01 + lyrae_drift_events table + linked `HSP-PMM-RTRT-001`
8. **Quality management system reference** — Talos eQMS / MasterControl tenancy (parent `TLB-FS-EQMS-001`)

### 15.6 Annex I (2027) readiness checklist

| Item | Status in v1.0 DS | Evidence pointer |
|---|---|---|
| Article 9 risk management | Designed | DR-17, DR-18, DR-19, DR-20; MOD-PAT-01 lifecycle |
| Article 12 logging | Designed | § 6.1 schema; § 9.5 event taxonomy |
| Article 13 transparency | Designed | MOD-RECON-01; § 8.1 `/reports/filings` |
| Article 14 human oversight | Designed | DS-LYR-EP-09, DS-LYR-EP-10, MOD-QP-01 |
| Article 26 PMM | Designed | MOD-PQS-01; lyrae_drift_events |
| Article 47 conformity assessment | Pending (separate artefact) | `<DOC-PREFIX>-CONFORMITY-NN` (out of scope here) |
| Article 50 transparency to deployers | Designed | DS-LYR-EP-07 (model-card pin per decision) |
| Article 72 PMM plan | Designed (linked) | `HSP-PMM-RTRT-001` (out of scope here) |
| Article 99 penalty awareness | Documented | DR-17 risk-register entry |

---

## 16. Appendix C — Determinism, Reproducibility & Numerical-Precision Design

### 16.1 Why bitwise reproducibility matters

A batch-release decision rendered by a Cat 5 site-developed Python service must be reproducible by a future inspector down to the bit level — otherwise the post-hoc reconstruction loses regulatory weight. Floating-point non-determinism (especially across pod restarts, library updates, or hardware migrations) is the silent enemy.

### 16.2 Design choices that enforce determinism

| Layer | Choice | Rationale |
|---|---|---|
| Arithmetic | `decimal.Decimal` with `Context(prec=28, rounding=ROUND_HALF_EVEN)` | IEEE-754-compatible rounding mode; deterministic across platforms |
| Float comparisons | Always cast Decimal before compare; never compare raw float | Avoids cross-CPU `x87` vs SSE2 register-width drift |
| Random seed | OQ pins seed `0x52545254` ("RTRT") for canonical test set | Deterministic test reproducibility |
| Library pinning | `requirements.txt` + cosign-signed image; SBOM published per release | No "latest" tag in production |
| Python version pin | 3.11.x; bumps require regression OQ | Avoids 3.11→3.12 `math.fsum` change risk |
| Container base | Wolfi (Chainguard); deterministic builds | Reproducible-builds project compliance |
| Lyrae prediction | Cast to Decimal at consumption boundary; record raw + cast | Cross-language precision boundary controlled |
| Rule expression | All literals declared as Decimal in rule store | No implicit float promotion |

### 16.3 OQ test scenarios for determinism

| Test ID | Scenario | Pass criterion |
|---|---|---|
| OQ-DEV-04 | 1000× repeat of canonical decision on fixed input + fixed rule | bitwise identical output across 1000 runs |
| OQ-DEV-04A | Same as OQ-DEV-04, but across pod-restart boundary | bitwise identical |
| OQ-DEV-04B | Same as OQ-DEV-04, but on Geneva DR cluster | bitwise identical |
| OQ-DEV-04C | Cross-version regression: Python 3.11.7 → 3.11.8 | bitwise identical OR documented diff approved by CR |

### 16.4 Reconstruction tool design

`rtrt-reconstruct --decision-id <id>` loads:
1. `decision_records.input_snapshot_s3_uri` → fetches raw inputs from S3 (Object Lock COMPLIANCE retention)
2. `decision_records.rule_id + rule_version` → loads rule definition from PostgreSQL (immutable after EFFECTIVE)
3. `decision_records.lyrae_model_version + lyrae_pccp_envelope` → records Lyrae state at time of decision
4. Replays `MOD-DEC-01` arithmetic against the snapshot
5. Asserts bitwise-identical `decision + confidence_score`

Reconstruction is a verifiable forensic operation, not a re-decision: it confirms historical record integrity, not new release authority.

---

## 17. Appendix D — Multi-Jurisdiction Filing State Machine Design Detail

### 17.1 Per-jurisdiction state machine

Each `(rule_id, jurisdiction)` pair carries an independent variation state machine:

```
            SUBMITTED ──→ UNDER_REVIEW ──→ APPROVED ──→ IMPLEMENTED ──→ OBSOLETE
                                  │
                                  ↓ (CA rejection)
                                REJECTED ──→ resubmit-cycle
```

### 17.2 Market-gate business rule

At decision time, the engine consults `rule.approved_jurisdictions[]` and the batch's `markets[]`:

```
for each market in batch.markets:
    state = mjr.gate_for_market(rule.id, market)
    if state != "IMPLEMENTED":
        raise MJR_RULE_NOT_APPROVED_FOR_MARKET(rule.id, market, state)

# All markets pass → execute rule
```

### 17.3 Range-conflict resolution

When the batch is destined for multiple markets with overlapping but non-identical approved ranges, the engine selects the **most restrictive** range (highest lower bound + lowest upper bound across markets):

```
combined_min = max(rule.approved_ranges_per_jurisdiction[market].min for market in batch.markets)
combined_max = min(rule.approved_ranges_per_jurisdiction[market].max for market in batch.markets)
if combined_min > combined_max:
    raise MJR_INCOMPATIBLE_RANGES(rule.id, batch.markets)
# Otherwise evaluate against [combined_min, combined_max]
```

### 17.4 Variation tracking gate at rule promotion

Per FS-PR-02, a rule cannot be promoted to EFFECTIVE if a variation submission is pending in any jurisdiction the rule is filed in:

```
def promote_rule(rule_id, new_state):
    pending = mjr.list_variations(rule_id, status=["SUBMITTED", "UNDER_REVIEW"])
    if pending and new_state == "EFFECTIVE":
        raise VARIATION_PENDING(rule_id, pending_jurisdictions=pending)
    # Proceed with promotion
```

### 17.5 Regulator-reporting service contract

For each variation:

| Stage | Action | Endpoint pattern (per CA) |
|---|---|---|
| SUBMITTED | post variation submission | Swissmedic: HTTPS `POST /variations` via Swissmedic eGov portal API; analogous per CA |
| UNDER_REVIEW | poll status | per-CA scheduled GET |
| APPROVED | record decision evidence | per-CA download decision letter, persist URN |
| IMPLEMENTED | activate rule + push rule-change notification | per-CA notification (where required) |
| OBSOLETE | record sunset | per-CA notification |

Per-CA endpoints and credential bindings are in `reg_reporting_config.yaml` (Vault-secret-backed).

---

## 18. Appendix E — PAT Model Lifecycle Binding Design Detail

### 18.1 Lifecycle states and transition gates

`pat_model_versions` carries the model state machine. State transitions require multi-party signatures per the table below:

| Transition | Required signers | Evidence required |
|---|---|---|
| `DRAFT → CALIBRATED` | Statistician + PAT Model Owner | calibration dataset summary; cross-validated R² + RMSEP |
| `CALIBRATED → CROSS-VALIDATED` | Statistician + PAT Model Owner + QA | cross-validation report; PRESS / Q² scores |
| `CROSS-VALIDATED → APPROVED` | Statistician + PAT Model Owner + QA | review of robustness study + intended-use envelope |
| `APPROVED → EFFECTIVE` | PAT Model Owner + Reg Affairs | filing-compatibility check + Lyrae deployment confirmation |
| `EFFECTIVE → OBSOLETE` | PAT Model Owner + QA + Reg Affairs | retirement justification + replacement-model reference |

Reverse transitions are not permitted; obsoleted models can be reactivated only by drafting a new version.

### 18.2 Runtime model-version pin enforcement

At every decision render, `rtrt-decision-engine` (MOD-DEC-01) loads the rule's `pat_model_version` field and instructs `rtrt-lyrae-client` (MOD-LYR-01) to request that specific version from Lyrae. The Lyrae response includes a `model_version` field; if it does not match the requested version exactly, the decision is rejected with `PAT_MODEL_VERSION_MISMATCH` and a deviation is raised. This pin is the single most important enforcement that protects against vendor-side silent model updates.

### 18.3 Drift monitoring: ASTM E2476 alignment

The `PatPerformanceMonitor` computes three metrics per ASTM E2476:

| Metric | Computation | Significance |
|---|---|---|
| Residual | sum of squared errors per rolling N-batch window | overall fit quality |
| Hotelling T² | per § 6.3 of ASTM E2476 | multivariate distance of new sample from training-set centroid |
| Q-statistic | per § 6.4 of ASTM E2476 | residual not captured by retained components |

Sustained out-of-spec readings (3-of-5 windows) trigger `PAT_MODEL_OOS`; in-flight decisions fall back to traditional release.

### 18.4 Retraining cadence and lifecycle re-entry

Retrained models enter the lifecycle at DRAFT. The PAT model management plan (`pat_model_management_plan.md`) documents the retraining triggers: scheduled annual review, drift event, manufacturing process change, raw-material supplier change. Each retraining yields a new `model_version`; the prior version remains in audit history with reason for retirement.

### 18.5 Per-jurisdiction variation tracking for PAT models

PAT-model changes are typically Q12 EC changes and trigger per-jurisdiction variation submissions. The `pat_model_versions.variation_record_id` FK (DS-LYR-EP-08 / FS-PMOD-05) links the model version to its filing-side variation state. A model version cannot transition to EFFECTIVE in a jurisdiction where its variation is not APPROVED.

### 18.6 Lyrae model-card pinning at decision time

For every decision, the engine fetches the Lyrae model card via `GET /models/{alias}/card` and pins the response JSON to the decision record (DS-LYR-EP-07). This preserves the vendor's transparency obligation per EU AI Act Article 50 — the deployer (Hesperia) holds a snapshot of the model's declared performance + limitations at the moment of decision. Inspector queries about "what did you know about this model when you made this batch-release decision" are answered by reading the pinned card.

### 18.7 PCCP envelope check

The Lyrae Predetermined Change-Control Plan (PCCP) envelope per `GET /models/{alias}/pccp/envelope` defines the set of approved model versions for a given product. The pre-release gate (DS-LYR-EP-07) verifies that the runtime-requested `model_version ∈ approved_envelope[product]`. Out-of-envelope reuse is rejected, preventing accidental cross-product application of a model trained for a narrower indication.

---

## 19. Appendix F — Disaster-Recovery + Audit-Continuity Design Detail

### 19.1 RTO / RPO targets per artefact class

| Artefact | RPO | RTO | DR mechanism | Restore-evidence path |
|---|---|---|---|---|
| PostgreSQL decision ledger | 15 min | 4 h | pg_basebackup + WAL streaming to Geneva | restore-certificate to eQMS |
| S3 input-snapshot archive | 1 min | 1 h | cross-region replication (Object Lock COMPLIANCE) | per-bucket integrity verification |
| Kubernetes workload state | 5 min | 4 h | ArgoCD re-sync from Git | namespace re-deploy runbook |
| Helios Kafka offsets | 1 min | 30 min | replicated cluster | consumer-group reset runbook |
| Lyrae endpoint availability | – | – | vendor-managed | vendor DR plan; fallback to traditional release |
| Vault secrets | 5 min | 1 h | Vault HA replication + Raft consensus | secret-rotation runbook |
| HashiCorp Vault audit log | 1 min | 30 min | Vault audit-file replication to SIEM | SIEM query playbook |

### 19.2 Annual DR test scope

Per FS-BAK-04, an annual DR test combines tabletop + live partial failover. Test scope:

1. Tabletop: walk through the RTRT-fallback runbook for a simulated regional outage
2. Live: failover the `rtrt-cs-reconciler` CronJob to Geneva; verify a reconciliation run succeeds
3. Live: failover one `rtrt-decision-engine` replica to Geneva; verify a canary decision against a synthetic batch
4. Verify restore-certificate is written to eQMS within 24 h of restore complete
5. Document all results in `HSP-DR-TEST-YYYYMMDD`; sign-off by VP QA + Head of CM + VP Reg Affairs

### 19.3 Audit-continuity during DR event

The decision-recorder writes to PostgreSQL synchronously; if PostgreSQL is unavailable, decisions are blocked (fail-closed). This is the design choice: it is better to halt decision-making than to render a decision that cannot be audit-trailed. The Helios publish path is asynchronous; transient Helios unavailability does not block decisions but lag breach triggers alert + reconciliation deviation.

### 19.4 Geneva DR site readiness

The Geneva site holds:
- Standby PostgreSQL replica (pg_basebackup + WAL streaming with ≤ 15 min lag)
- ArgoCD-managed namespace `rtrt-prod` (scaled to zero replicas, ready to scale on demand)
- Mirror of S3 Object Lock COMPLIANCE bucket (cross-region replication)
- Network path to Lyrae endpoint (Lyrae endpoint is vendor-managed and not site-failover-specific)
- Cert-manager state (cert renewal runs at primary; Geneva inherits via Git)

### 19.5 Restore-certificate evidence flow

Every restore (DR test or actual incident) writes a restore-certificate record to the eQMS (MasterControl) quality-records area with retention ≥ 25 y. The certificate captures: restore-event-id, source-backup-id, target-environment, restored-record-count, integrity-verification-result, QA witness, restore-start-ts, restore-complete-ts. This is the operational manifestation of Annex 11 § 12 backup-restore documentation expectations and feeds into the Annual Periodic Review.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
