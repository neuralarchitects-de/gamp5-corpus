---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "HYD2-FS-GENAI-001 v1.2 (parent FS)"
  - "HYD2-URS-GENAI-001 v1.2 (informational)"
  - "GAMP 5 (2nd ed., 2022) Cat 5 — Software Design Specification"
  - "EU AI Act 2024/1689 per-use-case decision tree — Annex I 2027 / Annex III 2026 / Art. 50 transparency"
  - "OWASP LLM Top 10 (2024); NIST AI 600-1 GenAI Profile (2024); ISO/IEC 42001:2023; ISO/IEC 23894:2023"
parent_fs:
  document_number: HYD2-FS-GENAI-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Hydra_BioPharma_GenAI_LLM_Service_FS_v1.3.md
parent_urs:
  document_number: HYD2-URS-GENAI-001
  version: 1.2
  file: ../../../URS/_generated/final/Validated_GenAI_LLM_Service_GxP__Hydra_BioPharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Software Design Specification (SDS)

## Validated GenAI / LLM-as-a-Service for GxP — Site Gateway over Anthropic + OpenAI APIs

**Document Number:** HYD2-DS-GENAI-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** HYD2-FS-GENAI-001 v1.2 | **Parent URS:** HYD2-URS-GENAI-001 v1.2
**Site:** Hydra BioPharma AG, Basel, Switzerland *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom Application (site-developed LiteLLM-Proxy + vLLM control-plane + per-customer-VPC routing + Lakera Guard pre/post filtering)
**EU AI Act 2024/1689 classification:** **Per-use-case decision tree** — every registered use-case is classified at registration via decision tree before any production traffic. Three outcomes: (a) **Annex I** (deadline 2 Aug 2027) — GxP-decision-informing use cases (e.g. PV case-triage, deviation-summarisation feeding QMS, batch-release-narrative summary, regulator-response-drafting); (b) **Annex III** (deadline 2 Aug 2026) — biometric / essential-services use cases (rare for Hydra); (c) **Art. 50 transparency-only** — document-drafting / generic-language assistance without GxP decision. Art. 99 penalty tier up to €15M or 3% global turnover for high-risk non-compliance.
**Project Mode:** Greenfield site-developed control plane over commercial Anthropic + OpenAI APIs; per-customer-VPC deployment for tenant-isolation (per parent URS Project Mode line)
**Tier (inherited from parent URS+FS):** T4
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11; EU GMP Annex 22 (DRAFT); ICH Q9(R1); **EU AI Act 2024/1689 Arts. 5 (prohibited), 8–21, 26, 27, 43, 47–49, 50 (transparency), 51–55 (GPAI obligations), 72, 73, 99, 113**; GDPR Arts. 6, 9, 22, 32, 35, 44; FDA AI/ML SaMD; FDA PCCP (Aug 2025); FDA CSA (Feb 2026); EMA AI Reflection Paper (2024); ISO/IEC 42001:2023; ISO/IEC 23894:2023; NIST AI RMF 1.0 + GenAI Profile (2024); **OWASP Top 10 for LLM Applications (2024)**; NIS2 Directive (EU) 2022/2555 (essential / important entity); EU MDR / IVDR (where SaMD per use-case); Swissmedic, BfArM, AGES.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect — GenAI Platforms) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of AI Engineering Platforms) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Security Architect — LLM) | _____________ | _____________ | _____ |
| Reviewer (Reg Affairs — AI/ML) | _____________ | _____________ | _____ |
| Reviewer (Data Protection Officer) | _____________ | _____________ | _____ |
| Reviewer (Per-Use-Case Classification Officer) | _____________ | _____________ | _____ |
| Reviewer (Foundation-Model Vendor Liaison — Anthropic + OpenAI) | _____________ | _____________ | _____ |
| Reviewer (Red-Team Lead) | _____________ | _____________ | _____ |
| Approver (VP AI / Data Science) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |
| Approver (VP Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (CISO) | _____________ | _____________ | _____ |
| Approver (System Owner — Head of AI Eng Platforms) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue. Inherited Tier T4 from parent URS+FS pair. Derived from HYD2-FS-GENAI-001 v1.2. DS covers 145/151 FS-IDs as DS-IDs; 6 FS-IDs flagged as "vendor-internal — no site design surface" (Anthropic API gateway internals, OpenAI API gateway internals, vLLM scheduler internals, Lakera Guard rule-engine internals, Azure-OpenAI control-plane internals, Pinecone vector-DB internals). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from HYD2-URS-GENAI-001 v1.2 and HYD2-FS-GENAI-001 v1.2. Additional DS-specific terms:

| Term | Definition |
|---|---|
| Use-case | A registered, classified, and approved consumer-side application of the GenAI service (e.g. `PV-CASE-TRIAGE-001`); use-cases are first-class entities with their own Annex classification, Art. 11 pack, and risk register row |
| Per-use-case decision tree | Classification flow producing Annex I / Annex III / Art. 50 / non-high-risk |
| LiteLLM-Proxy | OSS LLM API proxy (model abstraction + routing + cost tracking) |
| vLLM | Self-hosted LLM inference engine (Hydra-hosted models — currently fallback-only) |
| Lakera Guard | Third-party LLM pre/post filtering (prompt-injection, output toxicity, PII) |
| Transparency label | Art. 50 disclosure injected into model output where required |
| HITL evidence row | Database row asserting human-in-the-loop review of an output, gating downstream consumption |
| Red-teaming | Pre-deployment + periodic adversarial probing (prompt injection, jailbreak, data exfiltration) |
| GPAI | General-Purpose AI (EU AI Act Arts. 51–55) — Anthropic + OpenAI as upstream GPAI providers |
| FRIA | Fundamental Rights Impact Assessment (Art. 27) |

## 1. Purpose

This SDS describes the technical design of the Hydra Validated GenAI / LLM-as-a-Service: site-developed control plane (use-case registry, per-use-case classification engine, prompt-routing gateway, pre/post content filtering, transparency-label injection, HITL evidence enforcement, output retention + redaction, Art. 73 incident reporting) over commercial Anthropic + OpenAI APIs (with vLLM fallback). The SDS is the controlling input to Module Specifications (`HYD2-MS-GENAI-{module}-001`), Annex IV technical-documentation packs (per use-case), IQ/OQ/PQ Protocol Set, Notified Body submission (per Annex-I use-case), and the per-use-case Art. 11 pack. Vendor-internal APIs (Anthropic, OpenAI, Azure-OpenAI) are not redrawn.

## 2. Scope

**In scope.** Site-developed Python + FastAPI services: use-case registry; classification decision tree; prompt-routing gateway (LiteLLM-Proxy wrapper); content-filtering (Lakera Guard + Hydra's own DLP); transparency-label injection (Art. 50); HITL evidence-row enforcement; output retention + retention-classification; Art. 73 incident reporting; per-use-case Art. 11 pack manager; PMM service; vendor advisory subscriber (Anthropic + OpenAI security disclosures); per-customer-VPC deployment topology; red-teaming scaffolding; egress firewall design (no tenant-direct routes to anthropic.com / openai.com / *.azure-openai.com except via gateway VIP).

**Out of scope.** Anthropic, OpenAI, Azure-OpenAI internal model design (vendor SDLC); vLLM scheduler internals; Lakera Guard rule-engine internals; Pinecone vector-DB internals; underlying GxP consumer applications (Sirius PV, Theia MDR, Helios, etc. — they are deployers per Art. 26).

## 3. Architectural Overview

```
                          ┌─ Hydra Provider boundary (Art. 8–21) ─────┐
                          │                                           │
       Consumer apps   ──►│ Site API Gateway (Kong + Istio mTLS)      │
       (deployers      ──►│ Use-case ID header REQUIRED on all calls  │
        per Art. 26)   ──►│                                           │
                          │  ┌─────────────────────────────────┐      │
                          │  │ Use-case Registry +             │      │
                          │  │ Classification Decision Tree    │      │
                          │  └────────────┬────────────────────┘      │
                          │               │                            │
                          │               ▼                            │
                          │  ┌──────────────────────┐                  │
                          │  │ Per-use-case gate    │                  │
                          │  │ (Annex I/III/Art.50/ │                  │
                          │  │  non-high-risk;      │                  │
                          │  │  Art. 11 pack live?)  │                  │
                          │  └────────────┬─────────┘                  │
                          │               │                            │
                          │       Pre-filter (Lakera Guard +           │
                          │       Hydra DLP) → prompt-injection /      │
                          │       PII / GxP-redaction                  │
                          │               │                            │
                          │               ▼                            │
                          │  ┌──────────────────────────────┐          │
                          │  │ LiteLLM-Proxy Router          │          │
                          │  │   ├─► Anthropic Claude       │          │
                          │  │   ├─► OpenAI GPT             │          │
                          │  │   ├─► Azure-OpenAI (per-VPC) │          │
                          │  │   └─► vLLM fallback (Hydra-  │          │
                          │  │       hosted, on-prem only)  │          │
                          │  └────────────┬─────────────────┘          │
                          │               │                            │
                          │       Post-filter (Lakera Guard +          │
                          │       Hydra DLP + transparency-label       │
                          │       injection per Art. 50)               │
                          │               │                            │
                          │               ▼                            │
                          │       HITL evidence-row gate (Annex I)     │
                          │               │                            │
                          │               ▼                            │
                          │       Response + audit-row + retention     │
                          │                                            │
                          └─┬──────────────┬──────────┬──────────┬─────┘
                            │              │          │          │
                            ▼              ▼          ▼          ▼
                 Splunk SIEM        BfArM /     EU AI DB    EUDAMED
                 (audit)           Swissmedic / (Art. 49     (where SaMD)
                                   AGES         per Annex-I
                                   Art. 73      use case)
```

**Three architectural views per § 2B.5(1):**

**Logical view.** Every consumer call must carry a registered use-case ID. The use-case registry holds the Annex classification + Art. 11 pack reference + retention rule + transparency-label policy + HITL requirement + content-filter policy. A request flows: API Gateway (Kong) → use-case lookup → classification gate → pre-filter → router → upstream LLM → post-filter → HITL gate (Annex I only) → response. Audit event emitted at every transition. Egress ACL blocks tenant-direct routes to anthropic.com / openai.com / *.azure-openai.com except via the gateway VIP (FS-XINT-HYD-01 from consumer FS files).

**Process view.** Hydra runs in per-customer-VPC topology — each tenant has its own VPC + K8s namespace + Kong instance + LiteLLM-Proxy replica set (3-replica HA across 3 AZs) + Lakera Guard sidecar. Anthropic + OpenAI APIs reached via Hydra-managed egress proxy (`anthropic-egress.hydra.local`, `openai-egress.hydra.local`) with TLS 1.3 + mutual cert validation. Azure-OpenAI per-tenant deployment uses Azure Private Link.

**Technology view.** Python 3.12 + FastAPI 0.115 + Uvicorn (control-plane services); LiteLLM-Proxy 1.50; vLLM 0.6 (fallback); Lakera Guard SDK; Kong 3.8 (API gateway); Istio 1.24 (mTLS service mesh); Pinecone 4.0 (vector DB for RAG use-cases); Postgres 16 (control-plane state); Redis 7.4 (rate-limit + cache); HashiCorp Vault 1.18 (secrets, per-tenant API keys); Sigstore + cosign 2.4 (container signing); Prometheus 3.0 + Grafana 11 + Loki 3.0 + Tempo 2.6 (observability); Splunk Universal Forwarder 9.3 (SIEM); Trivy 0.57 + kube-bench (CI); ArgoCD 2.12 + GitLab 17 (CI/CD); Okta SAML 2.0 + MFA; CycloneDX 1.6 SBOM.

**Per-use-case Annex classification declaration.** This service classifies **each registered use-case** at registration; the platform itself does not have a single Annex classification. The decision tree (§ 7) routes use-cases to one of Annex I (2027 deadline) / Annex III (2026 deadline) / Art. 50 transparency-only / non-high-risk. Examples: `PV-CASE-TRIAGE-001` → Annex I (informs PV-decision); `DEVIATION-SUMMARIZER-001` → Annex I (feeds QMS); `REG-RESPONSE-DRAFT-001` → Annex I (feeds regulator); `MEETING-MINUTES-001` → Art. 50 transparency-only. Art. 99 penalty exposure per use-case.

## 4. Software Architecture

Eight layers (logical view):

1. **Use-Case Plane** — registry; classification decision tree; per-use-case Art. 11 pack manager; per-use-case policy (HITL, retention, transparency label).
2. **Request Gateway Plane** — Kong + Istio; use-case header enforcement; rate-limit + cost-budget; Egress ACL.
3. **Content-Filtering Plane** — pre-filter (Lakera Guard + Hydra DLP for PII / GxP-redaction / prompt-injection); post-filter (Lakera Guard + Hydra DLP + transparency-label injection).
4. **Routing Plane** — LiteLLM-Proxy router (per-use-case model binding); vendor egress proxy; per-tenant API-key management; fallback orchestration.
5. **HITL Plane** — evidence-row gate (Annex I), reviewer queue, bulk-accept rejection, submission-timer gating.
6. **Audit + Retention Plane** — audit-event writer; output-retention store; per-use-case retention policy; redaction worker.
7. **Regulatory + Post-Market Plane** — Art. 73 incident service; PMM service; vendor advisory subscriber (Anthropic + OpenAI security disclosure); EU AI DB registration; EUDAMED bridge where SaMD.
8. **Per-Tenant Infrastructure Plane** — per-customer-VPC + K8s + Kong + LiteLLM + Lakera Guard sidecar; Vault per-tenant namespace; Splunk per-tenant index `hyd2-{tenant}-genai`.

## 5. Module Decomposition

| Module ID | Name | Responsibility | Interface | Dependencies | Owner | GxP-criticality |
|---|---|---|---|---|---|---|
| MOD-UC-01 | `use-case-registry` | Register use-case; lifecycle DRAFT→REVIEW→APPROVED→EFFECTIVE→RETIRED; classification + Art. 11 pack pointer | REST `/usecase/`, `/usecase/{id}` | Postgres | GenAI Platforms | R1 (classification gate) |
| MOD-UC-02 | `classification-decision-tree` | Decision tree producing Annex I / Annex III / Art. 50 / non-high-risk | REST `/usecase/{id}/classify`, library | Postgres | Reg-Affairs IT | R1 (Art. 99 exposure) |
| MOD-UC-03 | `art11-pack-manager` | Per-use-case Art. 11 pack subfolders; export | REST `/usecase/{id}/art11`, CLI | S3 `hyd2-aiact-techdoc/usecase/{id}/` | Reg-Affairs IT | R1 |
| MOD-UC-04 | `usecase-policy-service` | Per-use-case policy: HITL?, retention class, transparency-label, content filter set | REST + library | Postgres | GenAI Platforms | R1 |
| MOD-UC-05 | `usecase-onboarding-workflow` | Onboarding workflow: classify → Art. 11 → red-team → sign-off | REST | MOD-UC-02, MOD-RED-01, MOD-VND-01 | Reg-Affairs IT | R1 |
| MOD-UC-06 | `usecase-deprecation` | Retire workflow; archive Art. 11 pack | REST | Postgres, S3 | Reg-Affairs IT | R2 |
| MOD-GW-01 | `request-gateway` | Kong plugin: usecase-id required; rate-limit per usecase | Kong plugin (Lua) + Go control | Kong, Postgres | GenAI Platforms | R1 |
| MOD-GW-02 | `egress-firewall` | Deny tenant-direct routes; allow only via gateway VIP | NetworkPolicy + Istio AuthorizationPolicy | Istio, K8s | Security Architecture | R1 |
| MOD-GW-03 | `cost-budget-service` | Per-tenant + per-usecase token-budget tracking | REST `/budget/`, library | Postgres, Redis | FinOps | R3 |
| MOD-PRE-01 | `prefilter-prompt-injection` | OWASP LLM01 prompt-injection detector (Lakera + Hydra heuristics) | inline middleware | Lakera Guard SDK | Security Architecture | R1 (Annex I) |
| MOD-PRE-02 | `prefilter-pii-dlp` | PII detection + redaction; per-use-case allowlist | inline middleware | Hydra DLP rules | DPO + Security | R1 (GDPR) |
| MOD-PRE-03 | `prefilter-gxp-redaction` | Strip per-use-case GxP-sensitive fields | inline middleware | per-use-case redaction rules | Validation IT | R1 |
| MOD-RT-01 | `litellm-router` | LiteLLM-Proxy wrapper; per-use-case model binding | REST `/v1/chat/completions` (LiteLLM-shape) | LiteLLM, Anthropic, OpenAI, Azure-OpenAI, vLLM | GenAI Platforms | R1 |
| MOD-RT-02 | `vendor-egress-proxy` | mTLS + cert-pin to Anthropic / OpenAI / Azure-OpenAI | egress sidecar | Istio Egress, Vault certs | Security Architecture | R1 |
| MOD-RT-03 | `vendor-failover-orchestrator` | Vendor outage → failover to alternate vendor or vLLM | library + Kong plugin | MOD-RT-01 | GenAI Platforms | R2 |
| MOD-POST-01 | `postfilter-toxicity` | OWASP LLM02 toxicity + harmful-output filter | inline middleware | Lakera Guard SDK | Security Architecture | R2 |
| MOD-POST-02 | `postfilter-output-dlp` | PII / GxP-leak detection in output | inline middleware | Hydra DLP rules | DPO + Security | R1 |
| MOD-POST-03 | `transparency-label-injector` | Art. 50 transparency label injection | inline middleware | per-use-case policy | Reg-Affairs IT | R1 (Art. 50) |
| MOD-POST-04 | `watermark-service` | (optional) provenance watermark for generative outputs | inline middleware | per-use-case policy | Reg-Affairs IT | R2 |
| MOD-HITL-01 | `hitl-evidence-gate` | Annex I requires HITL evidence row before downstream consumption | inline middleware + REST `/hitl/{request_id}` | Postgres `hitl_evidence` | Validation IT | R1 (Art. 14) |
| MOD-HITL-02 | `bulk-accept-rejector` | Reject any payload with `bulk_accept=true` | inline middleware | per-use-case policy | Validation IT | R1 |
| MOD-HITL-03 | `reviewer-queue` | Reviewer queue UI + assignment | REST `/hitl/queue/` | Postgres, Okta | Validation IT | R1 |
| MOD-AUD-01 | `audit-event-writer` | All transitions emit audit events | library + Postgres trigger + Splunk forwarder | Postgres `audit_events` | GenAI Platforms | R1 (Part 11) |
| MOD-AUD-02 | `audit-export` | Stream as JSON / CSV / PDF/A-3 | REST `/audit/export` | Postgres view | GenAI Platforms | R2 |
| MOD-RET-01 | `output-retention-service` | Per-use-case retention class enforcement | scheduled job + REST | S3 Object Lock, per-use-case policy | GenAI Platforms | R1 (Art. 18 + Part 11) |
| MOD-RET-02 | `redaction-worker` | Periodic redaction per retention policy | scheduled job | Postgres, S3 | DPO + Validation IT | R1 |
| MOD-RG-01 | `red-team-runner` | Adversarial test suite (prompt-injection, jailbreak, exfiltration) | CLI + scheduled job + REST | per-use-case red-team prompts | Red-Team | R1 (Art. 15) |
| MOD-RG-02 | `red-team-report-generator` | Quarterly red-team report per use-case | scheduled job | red-team runner output | Red-Team | R2 |
| MOD-RG-03 | `red-team-baseline-store` | Baseline red-team metrics per use-case | Postgres | red-team runner | Red-Team | R2 |
| MOD-PMM-01 | `pmm-service` | Collect outcomes + override events + consumer-incident webhooks per use-case | REST `/webhook/consumer-incident`, scheduled | per-use-case policy, audit | Reg-Affairs IT | R1 (Art. 72) |
| MOD-PMM-02 | `pmm-quarterly-report` | Per-use-case quarterly PMM report | scheduled | PMM service | Reg-Affairs IT | R2 |
| MOD-INC-01 | `art73-incident-service` | 3 clocks (15 d / 10 d / 2 d); per-use-case routing | REST `POST /incident` | regulatory routing | Reg-Affairs IT | R1 (Art. 73) |
| MOD-INC-02 | `regulatory-router` | DE→BfArM, CH→Swissmedic, AT→AGES + MAH defect channel SMTP | library | Vault certs | Reg-Affairs IT | R1 |
| MOD-VND-01 | `vendor-advisory-subscriber` | Anthropic + OpenAI security advisory subscription | scheduled fetcher + webhook | Anthropic + OpenAI advisory feeds | Security Architecture | R1 (Art. 15) |
| MOD-VND-02 | `gpai-obligations-tracker` | Track upstream GPAI provider compliance (Arts. 51-55) | scheduled | Anthropic + OpenAI transparency reports | Reg-Affairs IT | R2 (Arts. 51-55) |
| MOD-VND-03 | `model-snapshot-registry` | Pin upstream model version per use-case | Postgres | LiteLLM | GenAI Platforms | R1 (reproducibility) |
| MOD-VND-04 | `vendor-version-change-detector` | Detect upstream model version drift | scheduled | LiteLLM, Anthropic/OpenAI metadata endpoints | GenAI Platforms | R1 |
| MOD-REG-01 | `eu-aidb-registrar` | EU AI DB registration per Annex-I use-case | REST `/eu-aidb/usecase/{id}` | EU AI DB endpoint | Reg-Affairs IT | R1 (Art. 49) |
| MOD-REG-02 | `eudamed-bridge` | UDI-DI link where Annex-I use-case is part of SaMD | REST `/eudamed/usecase/{id}` | EUDAMED | Reg-Affairs IT | R1 |
| MOD-DEP-01 | `deployer-contract` | Art. 26 deployer obligations per consumer | REST `/deployer/`, `/usecase/{id}/deployer-obligations` | Postgres | Reg-Affairs IT | R2 (Art. 26) |
| MOD-DEP-02 | `fria-registry` | FRIA per public-body / essential-services deployer + Annex-III use-case | REST `/fria/` | Postgres | Reg-Affairs IT | R2 (Art. 27) |
| MOD-DEP-03 | `consumer-attestation` | Deployer-side attestation: HITL operational, training current | REST | LMS integration | Reg-Affairs IT | R2 |
| MOD-QMS-01 | `qms-bridge` | ServiceNow + MasterControl bridge | REST + Kafka | ServiceNow, MasterControl | QMS Ops | R2 (Art. 17, ISO/IEC 42001) |
| MOD-QMS-02 | `change-control-gate` | All use-case changes require CR | REST | MOD-QMS-01 | QMS Ops | R1 |
| MOD-DEV-01 | `tenant-vpc-deployer` | Per-customer-VPC topology provisioning | Helm + Terraform | AWS / Azure VPC peering | Cloud Ops | R2 |
| MOD-DEV-02 | `kong-config-renderer` | Per-tenant Kong route + plugin config | Helm | Kong | GenAI Platforms | R2 |
| MOD-DEV-03 | `litellm-config-renderer` | Per-tenant LiteLLM model-routing config | Helm | LiteLLM | GenAI Platforms | R2 |
| MOD-DEV-04 | `lakera-sidecar-deployer` | Per-tenant Lakera Guard sidecar | Helm | Lakera | Security Architecture | R2 |
| MOD-DEV-05 | `pinecone-tenant-namespace` | Per-tenant Pinecone namespace for RAG use-cases | Pinecone API | Pinecone | GenAI Platforms | R2 |
| MOD-DEP-LOG-01 | `request-log-writer` | Full prompt + response + token-count logging per use-case retention | inline | per-use-case retention, S3 | GenAI Platforms | R1 |
| MOD-DEP-LOG-02 | `redacted-log-writer` | Redacted-log variant for non-retention use-cases | inline | DLP rules | GenAI Platforms | R2 |
| MOD-DSR-01 | `dsr-service` | GDPR DSR access / erasure / restriction | REST `/dsr/*` | Postgres, S3 | DPO + Legal | R1 |
| MOD-DSR-02 | `dsr-erasure-coordinator` | Coordinate erasure with upstream Anthropic / OpenAI (RTBF) | scheduled + REST | vendor RTBF endpoints | DPO + Legal | R1 |
| MOD-DSR-03 | `art22-safeguards` | Art. 22(3) human-intervention queue | REST | Postgres | Reg-Affairs IT | R1 |
| MOD-OSS-01 | `openrouter-policy-enforcer` | (optional) limit OpenRouter use to specifically approved use-cases | inline | per-use-case policy | GenAI Platforms | R2 |
| MOD-OSS-02 | `oss-license-tracker` | Track OSS licenses of vLLM models | scheduled | SBOM | Legal + AI Platforms | R3 |
| MOD-PEN-01 | `penetration-test-runner` | Annual third-party pen-test orchestration | scheduled | external pen-tester | Security Architecture | R2 |
| MOD-RES-01 | `dr-test-orchestrator` | Annual DR test orchestration | scheduled | per-tenant K8s | Cloud Ops | R2 |
| MOD-CACHE-01 | `response-cache` | (optional) response caching for non-sensitive use-cases | Redis | per-use-case policy | GenAI Platforms | R3 |
| MOD-CACHE-02 | `cache-redaction` | Cache eviction on policy change | scheduled | Redis | GenAI Platforms | R3 |
| MOD-CACHE-03 | `cache-key-hashing` | SHA-256 cache key including use-case + prompt | library | — | GenAI Platforms | R3 |
| MOD-CLS-01..06 | `classification-decision-tree` rules | Annex I / Annex III / Art. 50 leaves | library | per-use-case context | Reg-Affairs IT | R1 |
| MOD-TRN-01 | `okta-lms-connector` | Use-case access blocked without LMS training | webhook | Okta + LMS | IAM Ops | R2 (Art. 4) |
| MOD-TRN-02 | `red-team-training` | LMS course for red-team operators | LMS | — | Red-Team | R2 |
| MOD-TRN-03 | `consumer-onboarding-training` | Consumer SDK key issued only after training | LMS | — | Reg-Affairs IT | R2 |
| MOD-HD-01..03 | `hd-event-emitters` | Helios audit-publish per use-case (cross-system) | Kafka | per FS-XINT-HEL-* | GenAI Platforms | R2 |
| MOD-HQ-01..02 | `hydra-quality-bridges` | Quality bridges (audit + CR) | Kafka + REST | MasterControl, ServiceNow | QMS Ops | R2 |
| MOD-PR-01 | `periodic-review-orchestrator` | Annual per-use-case review | scheduled | all DS data sources | Reg-Affairs IT | R2 |
| MOD-PI-01..05 | `prompt-injection-suite` | Sub-modules of OWASP LLM01 coverage | library | Lakera + Hydra | Security Architecture | R1 |
| MOD-GPAI-01..04 | `gpai-tracking-suite` | GPAI obligation sub-tracking | library | upstream advisories | Reg-Affairs IT | R2 |
| MOD-WM-01..03 | `watermark-suite` | Watermark + provenance sub-modules | library | per-use-case policy | Reg-Affairs IT | R2 |
| MOD-PROMPT-01..02 | `prompt-template-registry` | Prompt-template version control per use-case | Postgres + GitLab | GitLab signed tags | GenAI Platforms | R1 |
| MOD-PI-OUTPUT-01..05 | (alias of MOD-PI-* but for output checks) | Output PI sub-checks | library | Lakera | Security Architecture | R2 |

(Module set is comprehensive; ~150 named mini-modules across the 8 layers above.)

## 6. Data Model Design

### 6.1 `usecase` table (per FS-UC-*)

```sql
CREATE TABLE usecase (
  usecase_id         TEXT         PRIMARY KEY,   -- e.g. 'PV-CASE-TRIAGE-001'
  name               TEXT         NOT NULL,
  description        TEXT         NOT NULL,
  state              TEXT         NOT NULL CHECK (state IN
                       ('DRAFT','REVIEW','APPROVED','EFFECTIVE','SUSPENDED','RETIRED')),
  risk_class         TEXT         NOT NULL CHECK (risk_class IN
                       ('annex_i','annex_iii','art_50_transparency_only','non_high_risk')),
  classification_evidence_url TEXT,
  art11_pack_url     TEXT,
  art11_pack_version TEXT,
  art11_pack_expires_at DATE,
  retention_class    TEXT         NOT NULL,                    -- per FS-RET-01
  hitl_required      BOOL         NOT NULL,
  bulk_accept_allowed BOOL        NOT NULL DEFAULT false,
  transparency_label_policy TEXT,                              -- enum: 'always', 'on_synthetic', 'never'
  content_filter_set TEXT[],                                   -- e.g. ARRAY['prompt_injection','pii','gxp_redact']
  approved_models    TEXT[]       NOT NULL,                    -- e.g. ARRAY['anthropic/claude-4.5','openai/gpt-5.1']
  approved_tenants   TEXT[]       NOT NULL,
  deployer_obligations_json JSONB,
  fria_required      BOOL         NOT NULL DEFAULT false,
  fria_doc_url       TEXT,
  prompt_template_git_tag TEXT    NOT NULL,
  red_team_baseline_id UUID,
  pmm_quarterly_template_url TEXT,
  created_by         TEXT         NOT NULL,
  created_at         TIMESTAMPTZ  NOT NULL DEFAULT now(),
  approved_by        TEXT,
  approved_at        TIMESTAMPTZ,
  retired_at         TIMESTAMPTZ
);
```

### 6.2 `request_log` table (per-use-case retention)

```sql
CREATE TABLE request_log (
  request_id         UUID         PRIMARY KEY,
  usecase_id         TEXT         NOT NULL REFERENCES usecase,
  tenant_id          TEXT         NOT NULL,
  consumer_id        TEXT         NOT NULL,
  actor_id           TEXT         NOT NULL,        -- end-user Okta id
  prompt_sha256      CHAR(64)     NOT NULL,
  prompt_redacted    TEXT,                          -- redacted variant per use-case policy
  prompt_full        TEXT,                          -- full prompt only when retention_class allows
  upstream_model     TEXT         NOT NULL,
  upstream_model_snapshot_sha256 CHAR(64),
  response_sha256    CHAR(64)     NOT NULL,
  response_full      TEXT,
  transparency_label_applied BOOL NOT NULL,
  hitl_evidence_id   UUID,
  token_count_in     INTEGER,
  token_count_out    INTEGER,
  latency_ms         INTEGER,
  pre_filter_result  JSONB,
  post_filter_result JSONB,
  art50_label_text   TEXT,
  timestamp_iso8601  TIMESTAMPTZ  NOT NULL DEFAULT now()
);
```

### 6.3 `hitl_evidence` table

```sql
CREATE TABLE hitl_evidence (
  hitl_evidence_id   UUID         PRIMARY KEY,
  request_id         UUID         NOT NULL REFERENCES request_log,
  usecase_id         TEXT         NOT NULL,
  reviewer_id        TEXT         NOT NULL,
  decision           TEXT         NOT NULL CHECK (decision IN ('accept','reject','escalate')),
  reviewer_comment   TEXT,
  reviewed_at        TIMESTAMPTZ  NOT NULL DEFAULT now(),
  signature_id       UUID
);
```

### 6.4 `audit_events` table (append-only, identical pattern to Lyrae)

```sql
CREATE TABLE audit_events (
  event_id           BIGSERIAL    PRIMARY KEY,
  usecase_id         TEXT,
  tenant_id          TEXT,
  actor_id           TEXT         NOT NULL,
  request_id         UUID,
  action             TEXT         NOT NULL,
  old_value          JSONB,
  new_value          JSONB,
  reason_for_change  TEXT,
  signature_id       UUID,
  timestamp_iso8601  TIMESTAMPTZ  NOT NULL DEFAULT now(),
  integrity_hash_sha256 CHAR(64)  NOT NULL
);
CREATE OR REPLACE RULE audit_events_no_update AS ON UPDATE TO audit_events DO INSTEAD NOTHING;
CREATE OR REPLACE RULE audit_events_no_delete AS ON DELETE TO audit_events DO INSTEAD NOTHING;
```

### 6.5 `art73_incident` table (per FS-INC-*)

Same schema as Lyrae DS § 6.6, with additional `usecase_id` column.

### 6.6 Per-tenant token-budget table

```sql
CREATE TABLE token_budget (
  tenant_id          TEXT,
  usecase_id         TEXT,
  budget_window      TEXT,           -- 'daily', 'monthly'
  budget_limit       BIGINT,
  consumed           BIGINT          NOT NULL DEFAULT 0,
  reset_at           TIMESTAMPTZ,
  PRIMARY KEY (tenant_id, usecase_id, budget_window)
);
```

### 6.7 `content_filter_result` table

Records pre/post filter outcomes for forensic review. Joined to `request_log` by `request_id`.

### 6.8 `transparency_label_registry` table

Per-use-case label text + locale variants (`art50_label_text_{lang}`).

### 6.9 Data classification + retention

| Class | Examples | Retention | Storage |
|---|---|---|---|
| GxP audit (R1) | `audit_events` | ≥ 25 y | Splunk + S3 |
| Annex I `request_log` (HITL-gated) | full prompt + response per use-case policy | ≥ 10 y (Art. 18) | S3 Object Lock |
| Annex III `request_log` | full + redacted | ≥ 10 y | S3 Object Lock |
| Art. 50 transparency-only `request_log` | redacted-only | ≥ 90 d default | Postgres + S3 lifecycle |
| Art. 11 pack | per-use-case | ≥ 10 y from market placement | S3 Object Lock + Glacier Vault Lock |
| HITL evidence | `hitl_evidence` | ≥ 10 y | Postgres + S3 |
| Art. 73 incident | per incident | ≥ 10 y | S3 Object Lock |
| GDPR PII (per DSR) | per data subject | per DPIA | encrypted-at-rest AES-256 |
| Cache (response-cache) | hot cache | ≤ 24 h | Redis (volatile) |

## 7. Algorithm + Calculation Design

### 7.1 Per-use-case classification decision tree (the central algorithm)

Pseudocode for `MOD-UC-02 / MOD-CLS-01..06`:

```
function classify(usecase_context) -> risk_class:

  # Step 1: prohibited-practices check (Art. 5)
  if usecase_context.involves(prohibited_practices_list):
    return REJECT  # Art. 5 prohibits these use-cases entirely

  # Step 2: Annex I check (high-risk via Union harmonisation legislation)
  if usecase_context.is_safety_component_of(
       union_harmonisation_legislation_in_annex_I
     ):
    # Examples: drug-release decision component, medical-device output,
    #           sterilisation control, In-Vitro Diagnostic decision
    return ANNEX_I

  # Step 3: Annex III check (high-risk stand-alone)
  if usecase_context.matches_any(annex_iii_list):
    # Annex III categories: biometric, critical infra, education,
    #                       employment, essential public/private services,
    #                       law enforcement, migration, justice/democracy
    return ANNEX_III

  # Step 4: Art. 50 transparency-only checks (still applies)
  if usecase_context.generates_synthetic_content():
    return ART_50_TRANSPARENCY_ONLY

  # Step 5: non-high-risk
  return NON_HIGH_RISK
```

The classification is **manually reviewed** by the Per-Use-Case Classification Officer before approval; the tree is decision-support, not autonomous. Annex-I outcome triggers Art. 11 pack + Notified Body engagement + Art. 49 EU AI DB registration. Annex-III outcome triggers Art. 11 pack (lighter) + Art. 49 registration. Art. 50 outcome triggers transparency-label policy. Non-high-risk outcome still requires record-of-decision (audit-trail) and is subject to Art. 4 AI-literacy + Art. 50 where synthetic.

### 7.2 Prompt-routing + pre/post filtering

```
on POST /v1/chat/completions with usecase_id header:
  uc = registry.fetch(usecase_id)
  assert uc.state == 'EFFECTIVE'
  assert uc.art11_pack_expires_at > now() if uc.risk_class in (ANNEX_I, ANNEX_III)
  cost_budget.check(tenant_id, usecase_id) or return 429
  prompt = pre_filter(prompt, uc.content_filter_set)
    -> prompt-injection detection (OWASP LLM01) via Lakera + Hydra heuristics
    -> PII detection + redaction (per-use-case allowlist)
    -> GxP-redaction (strip per-use-case sensitive fields)
  upstream = LiteLLM-Proxy.route(prompt, uc.approved_models[0])
  response = upstream.complete(prompt)
  response = post_filter(response, uc.content_filter_set)
    -> toxicity (OWASP LLM02)
    -> PII / GxP-leak detection
    -> transparency-label injection if uc.transparency_label_policy applies
  if uc.hitl_required and uc.bulk_accept_allowed == false:
    request.assert_no_bulk_accept_flag()
    queue_hitl_evidence(request)  # downstream consumer blocked until hitl_evidence row
  write_audit_event(action='REQUEST_PROCESSED', usecase_id, request_id, ...)
  write_request_log(request_id, prompt_redacted | prompt_full per uc.retention_class, ...)
  return response
```

### 7.3 HITL evidence-row enforcement

For Annex I use-cases the downstream consumer's submission-timer service blocks until a `hitl_evidence` row with `decision='accept'` is present (FS-XINT-HYD-03 from consumer FS files). The HITL backend rejects payloads with `bulk_accept=true` at API level (MOD-HITL-02).

### 7.4 Transparency-label injection (Art. 50)

Per use-case policy `transparency_label_policy ∈ {'always', 'on_synthetic', 'never'}`:

- `always`: prepend or append per-locale label (`art50_label_text_{lang}`) to every response.
- `on_synthetic`: detect if response is "synthetic content" per Art. 50 definition → inject label.
- `never`: no injection.

Label text per locale: de-DE, de-AT, de-CH, fr-CH, it-CH, en, fr, es as needed.

### 7.5 Lakera Guard pre/post filtering

Lakera Guard SDK called inline. Configured rule sets per use-case (prompt-injection, jailbreak, PII, toxicity, hate-speech). Result cached in `content_filter_result` table for forensic review. Lakera-block → return error response with reason; Lakera-flag-but-pass → audit-event row.

### 7.6 Art. 73 incident clock arithmetic

Identical to Lyrae DS § 7.6 — UTC internal; 15 d / 10 d / 2 d clocks.

### 7.7 Per-tenant token-budget enforcement

```
on every request:
  budget = SELECT budget_limit, consumed FROM token_budget WHERE tenant_id=? AND usecase_id=? AND budget_window='daily'
  if consumed + estimated_tokens > budget_limit: return 429 with reason 'BUDGET_EXCEEDED'
  on response complete: UPDATE token_budget SET consumed = consumed + actual_tokens
```

Daily + monthly windows. Reset cron at 00:00 UTC.

### 7.8 Red-team baseline + drift

Each Annex-I + Annex-III use-case has a red-team baseline: % of prompt-injection prompts that succeed; % of jailbreak prompts; % of PII-exfiltration. Quarterly re-run compared against baseline (RG-01..03 modules). Drift > 10 pp triggers re-validation.

### 7.9 Upstream model snapshot pinning

Anthropic + OpenAI publish model snapshot identifiers (e.g. `claude-4.5-2025-12-01`, `gpt-5.1-2026-01-15`). Pinned per use-case in `usecase.approved_models[].snapshot`. Upstream drift detector compares published snapshot SHA-256 → blocks routing if drift detected without CR.

### 7.10 Caching (optional)

For approved-cache use-cases: cache key = SHA-256(`usecase_id` || `prompt_canonical_json` || `upstream_model` || `snapshot_sha256`). TTL ≤ 24 h. Eviction on policy change.

## 8. Interface + API Design

Subset (~30 endpoints exposed):

| Endpoint | Method | Path | AuthN | Request schema | Response schema | Rate limit | Errors | Audit |
|---|---|---|---|---|---|---|---|---|
| Register use-case | POST | `/usecase` | OAuth2 + Reg-Affairs group | `UseCaseRequest` | `UseCase` | 10/d | 400, 422 | USECASE_REGISTERED |
| Classify | POST | `/usecase/{id}/classify` | OAuth2 + Classification Officer | `ClassifyRequest` | `Classification` | 20/d | 400 | USECASE_CLASSIFIED |
| Approve | POST | `/usecase/{id}/approve` | OAuth2 + 2 JWTs (Author ≠ Approver) | — | `UseCase` | 5/d | 400, 403 | USECASE_APPROVED |
| Suspend | POST | `/usecase/{id}/suspend` | OAuth2 + HO group | `{reason}` | `UseCase` | 5/d | 400, 403 | USECASE_SUSPENDED |
| Retire | POST | `/usecase/{id}/retire` | OAuth2 + Reg-Affairs | `{reason}` | `UseCase` | 5/d | 400 | USECASE_RETIRED |
| Chat completion (LLM call) | POST | `/v1/chat/completions` | OAuth2 (consumer JWT) + usecase-id header | LiteLLM-shape `ChatRequest` | `ChatResponse` (+ transparency label if applicable) | per-tenant + per-usecase | 401, 403 USECASE_NOT_APPROVED, 422, 429 BUDGET, 503 VENDOR | REQUEST_PROCESSED |
| HITL accept/reject | POST | `/hitl/{request_id}/{decision}` | OAuth2 + Reviewer group | `{comment?: string}` | `HITLEvidence` | 100/h/reviewer | 400, 403 | HITL_DECISION |
| Art. 11 pack get | GET | `/usecase/{id}/art11` | OAuth2 + Reg-Affairs | — | `Art11Pack` | 100/h | 404 | ART11_READ |
| Art. 11 pack export | POST | `/usecase/{id}/art11/export` | OAuth2 + Reg-Affairs | — | `{zip_url, manifest_sha256}` | 5/d | 400, 403 | ART11_EXPORTED |
| EU AI DB register | POST | `/eu-aidb/usecase/{id}` | OAuth2 + Reg-Affairs | — | `{entry_id, date}` | 5/d | 400 | EUAIDB_REGISTERED |
| Art. 73 incident | POST | `/incident` | OAuth2 (deployer or HO) | `IncidentRequest` | `IncidentRecord` | 100/h | 400 | INCIDENT_RECORDED |
| Consumer-incident webhook | POST | `/webhook/consumer-incident` | mTLS (per-deployer) | `ConsumerIncident` | `Ack` | per-deployer | 401, 400 | DEPLOYER_INCIDENT |
| Audit export | GET | `/audit/export?from=&to=&format=` | OAuth2 + Audit-Readers | — | streaming | 1/h | 400 | AUDIT_EXPORTED |
| DSR access | POST | `/dsr/access` | OAuth2 + DSR group | `DSRRequest` | `DSRTicket` | 10/h | 400 | DSR_ACCESS |
| DSR erasure | POST | `/dsr/erasure` | OAuth2 + DSR group | `DSRRequest` | `DSRTicket` | 10/h | 400 | DSR_ERASURE |
| Red-team run | POST | `/redteam/usecase/{id}/run` | OAuth2 + Red-Team group | `RedTeamSuite` | `RedTeamResult` | 5/d | 400, 403 | REDTEAM_RUN |
| Token-budget set | PUT | `/budget/tenant/{tid}/usecase/{ucid}` | OAuth2 + FinOps | `BudgetRequest` | `Budget` | 50/d | 400 | BUDGET_SET |
| Vendor advisory | GET | `/vendor/advisories` | OAuth2 + Reg-Affairs | — | `[Advisory]` | 100/h | — | — |
| Pre-filter test | POST | `/prefilter/test` | OAuth2 + Security | `{prompt, filter_set}` | `{result, blocked, flags}` | 100/h | 400 | — |
| Post-filter test | POST | `/postfilter/test` | OAuth2 + Security | `{response, filter_set}` | `{result, blocked, flags}` | 100/h | 400 | — |
| Deployer obligations | GET | `/usecase/{id}/deployer-obligations` | OAuth2 | — | `DeployerObligations` | 100/h | 404 | — |
| FRIA submit | POST | `/fria` | OAuth2 + Reg-Affairs | `FRIARequest` | `FRIA` | 5/d | 400 | FRIA_RECORDED |

TLS 1.3, mTLS service-to-service via Istio. JSON canonical form (RFC 8785) for hash inputs.

## 9. Security Design

### 9.1 AuthN

Okta SAML 2.0 + MFA; FIDO2 phishing-resistant for `genai-prod-approvers`. Per-tenant Okta groups (`hyd2-{tenant}-users`). Kong validates assertion → issues short-lived OAuth2 (max-age 5 min). Istio mTLS service-to-service via SPIFFE/SPIRE.

### 9.2 AuthZ

Per-tenant + per-use-case + per-role RBAC. Consumer JWT must include `tenant_id`, `usecase_id` claim, and approved consumer group membership. Kong plugin `usecase-id-required` rejects requests without valid headers.

### 9.3 Secrets

HashiCorp Vault per-tenant namespace `hyd2-{tenant}/`: Anthropic + OpenAI + Azure-OpenAI API keys (per-tenant; rotation per vendor SLA, max 90 d); Lakera Guard SDK key; DB credentials (dynamic, TTL 1 h); regulator gateway certs.

### 9.4 Transport security

TLS 1.3 on all paths. Anthropic + OpenAI egress: mTLS with vendor-published TLS pin (renewed on vendor rotation). Vendor egress proxies `anthropic-egress.hydra.local`, `openai-egress.hydra.local` are the only paths permitted by NetworkPolicy + Istio AuthorizationPolicy from tenant namespaces.

### 9.5 OWASP LLM Top 10 coverage

| OWASP LLM | Hydra module(s) |
|---|---|
| LLM01 Prompt Injection | MOD-PRE-01 + MOD-PI-* + Lakera Guard |
| LLM02 Insecure Output Handling | MOD-POST-01 + MOD-POST-02 |
| LLM03 Training Data Poisoning | upstream vendor responsibility (Anthropic / OpenAI as GPAI providers) + MOD-VND-01 advisory |
| LLM04 Model Denial of Service | MOD-GW-01 rate-limit + MOD-GW-03 cost-budget |
| LLM05 Supply Chain Vulnerabilities | MOD-VND-01..04 + Trivy + cosign + CycloneDX SBOM |
| LLM06 Sensitive Information Disclosure | MOD-PRE-02 PII + MOD-PRE-03 GxP-redact + MOD-POST-02 output DLP |
| LLM07 Insecure Plugin Design | Hydra has no plugin surface — vendor plugins disabled |
| LLM08 Excessive Agency | MOD-UC-04 per-use-case policy + MOD-HITL-* HITL enforcement |
| LLM09 Overreliance | MOD-POST-03 transparency-label + MOD-HITL-* |
| LLM10 Model Theft | mTLS + per-tenant API-key isolation + MOD-CFG-DEF (rate-limit) |

### 9.6 Red-teaming

Quarterly per Annex-I use-case (MOD-RG-01..03); pre-deployment red-team mandatory for new Annex-I + Annex-III use-cases. Adversarial test pack version-controlled in `gitlab.hydra.local/genai-redteam`.

### 9.7 Penetration testing

Annual third-party pen-test scoped to Hydra gateway + control plane; report `PEN-TEST-HYD-{year}.pdf`.

## 10. Deployment Architecture

### 10.1 Per-customer-VPC topology

Each tenant has its own VPC + K8s namespace + Kong instance + LiteLLM-Proxy 3-replica + Lakera Guard sidecar + Postgres tenant schema + Splunk per-tenant index. Cross-tenant traffic prohibited at NetworkPolicy + Istio level. Tenant onboarding via `tenant-vpc-deployer` (MOD-DEV-01) + Terraform.

### 10.2 K8s topology

Per tenant: K8s 1.30; 3 AZs (region per customer choice — EU Frankfurt for EU customers, EU Zurich for CH customers, US East for US customers); Pod Security Standards `restricted`; CIS Kubernetes Benchmark (current release at site deployment) applied; kube-bench in CI; Trivy scan on every build.

### 10.3 Observability

Prometheus + Grafana + Loki + Tempo per tenant. Metrics: `request_latency_seconds`, `request_error_rate`, `vendor_latency_seconds{vendor=...}`, `lakera_block_rate`, `transparency_label_apply_rate`, `hitl_pending`, `budget_consumed`. Splunk per-tenant index `hyd2-{tenant}-genai-audit` + `hyd2-{tenant}-genai-request`. Retention ≥ 25 y audit.

### 10.4 Egress firewall

NetworkPolicy `genai-tenant-egress-deny-llm-direct` blocks tenant pods from reaching anthropic.com, openai.com, *.azure-openai.com directly. Only Hydra gateway egress proxies (`anthropic-egress`, `openai-egress`) allowed. Audit-event row when policy denies.

### 10.5 DR + retention

RTO ≤ 4 h; RPO ≤ 15 min. Annual DR drill per tenant. S3 Object Lock (Compliance) + Glacier Vault Lock for Art. 11 pack + audit + request log ≥ 10 y.

### 10.6 CI/CD

GitLab + ArgoCD. Signed commits required. 2-reviewer code review. CI: lint + unit-test + Trivy + kube-bench + cosign sign + SBOM. Per-tenant Helm + Kustomize.

## 11. Module Specification Table

Per-module pointer table (excerpt — full set ≈150 mini-modules; each carries `gitlab.hydra.local/genai-platform/{module}` repo + unit-test + Module Spec):

| Module ID | File path | Class / function | Unit-test | Module Spec |
|---|---|---|---|---|
| MOD-UC-01 | `services/usecase/registry.py` | `UseCaseRegistry` | `tests/test_usecase.py` | HYD2-MS-GENAI-USECASE-001 |
| MOD-UC-02 | `services/usecase/classification.py` | `ClassificationDecisionTree` | `tests/test_classification.py` | HYD2-MS-GENAI-CLASS-001 |
| MOD-PRE-01 | `services/filter/prompt_injection.py` | `PromptInjectionFilter` | `tests/test_pi.py` | HYD2-MS-GENAI-PI-001 |
| MOD-RT-01 | `services/router/litellm.py` | `LiteLLMRouter` | `tests/test_router.py` | HYD2-MS-GENAI-ROUTER-001 |
| MOD-POST-03 | `services/filter/transparency_label.py` | `TransparencyLabelInjector` | `tests/test_transp.py` | HYD2-MS-GENAI-TRANSP-001 |
| MOD-HITL-01 | `services/hitl/gate.py` | `HITLEvidenceGate` | `tests/test_hitl.py` | HYD2-MS-GENAI-HITL-001 |
| MOD-AUD-01 | `services/audit/writer.py` | `AuditEventWriter` | `tests/test_audit.py` | HYD2-MS-GENAI-AUDIT-001 |
| MOD-INC-01 | `services/incident/art73.py` | `Art73IncidentService` | `tests/test_incident.py` | HYD2-MS-GENAI-INC-001 |
| MOD-RG-01 | `services/redteam/runner.py` | `RedTeamRunner` | `tests/test_redteam.py` | HYD2-MS-GENAI-REDTEAM-001 |
| MOD-VND-01 | `services/vendor/advisory.py` | `VendorAdvisorySubscriber` | `tests/test_advisory.py` | HYD2-MS-GENAI-ADVISORY-001 |
| (… plus ~140 more) | (…) | (…) | (…) | (…) |

## 12. References

**US**
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- FDA AI/ML SaMD Action Plan (2021)
- FDA PCCP (Aug 2025)
- FDA CSA (Feb 2026)
- NIST AI 100-1 (AI RMF 1.0)
- NIST AI 600-1 (GenAI Profile, 2024)
- NIST SP 800-218 SSDF
- NIST SP 800-53 r5

**EU**
- EU AI Act Reg. (EU) 2024/1689 — full Arts. 5, 8–21, 26, 27, 43, 47–49, **50 (transparency)**, **51–55 (GPAI obligations)**, 72, 73, 99, 113
- EU AI Act Annex I (2 Aug 2027) + Annex III (2 Aug 2026)
- EU GMP Annex 11; EU GMP Annex 22 (DRAFT)
- EU MDR Reg. 2017/745; EU IVDR Reg. 2017/746 (where per-use-case SaMD)
- GDPR Reg. (EU) 2016/679 Arts. 6, 9, 22, 32, 35, 44
- NIS2 Directive (EU) 2022/2555 (essential / important entity reporting)
- EMA Reflection Paper on AI in the Medicinal Product Lifecycle (2024)

**International**
- ICH Q9(R1)
- IEC 62304:2006+A1:2015 (where Annex-I use-case is SaMD)
- IEC 81001-5-1:2021
- ISO/IEC 42001:2023 (AI management system)
- ISO/IEC 23894:2023 (AI risk management)
- ISO/IEC 27001:2022
- ISPE GAMP 5 (2nd ed., 2022); GAMP GPG *AI/ML in GxP* (2024)
- OWASP Top 10 for LLM Applications (2024)
- OWASP ASVS v5.0
- OWASP API Security Top 10 (2023)

**DACH**
- BfArM, Swissmedic, AGES
- BSI IT-Grundschutz; ENISA Threat Landscape for AI (2024)

**Vendor**
- Anthropic — Claude API documentation + Trust Center
- OpenAI — GPT API documentation + Trust Center
- Azure OpenAI Service documentation
- LiteLLM-Proxy documentation
- vLLM documentation
- Lakera Guard documentation
- Pinecone documentation
- Kong Gateway documentation; Istio documentation; HashiCorp Vault documentation
- Sigstore / cosign documentation
- Okta SAML 2.0 + MFA Administrator Guide

## 13. Appendix A — DS → FS Traceability Matrix

| DS ID / Module | FS ID |
|---|---|
| MOD-UC-01 | FS-UC-01, FS-UC-02, FS-UC-04, FS-UC-05, FS-UC-06 |
| MOD-UC-02 | FS-UC-03, FS-CLS-01, FS-CLS-02, FS-CLS-03, FS-CLS-04, FS-CLS-05, FS-CLS-06 |
| MOD-UC-03 | FS-TD-01, FS-TD-02, FS-TD-03 |
| MOD-UC-04 | FS-UC-04 |
| MOD-UC-05 | FS-UC-05 |
| MOD-UC-06 | FS-UC-06 |
| MOD-GW-01 | FS-GR-01, FS-GR-02, FS-GR-03, FS-GR-04, FS-GR-05 |
| MOD-GW-02 | FS-RG-01, FS-RG-02, FS-RG-03, FS-RG-04 |
| MOD-GW-03 | FS-COST-01, FS-COST-02, FS-COST-03 |
| MOD-PRE-01 | FS-PI-01, FS-PI-02, FS-PI-03, FS-PI-04, FS-PI-05 |
| MOD-PRE-02 | FS-CONF-01, FS-CONF-02 |
| MOD-PRE-03 | FS-CONF-03, FS-CONF-04 |
| MOD-RT-01 | FS-PROMPT-01, FS-PROMPT-02 |
| MOD-RT-02 | FS-INT-VENDOR-01, FS-SEC-04 |
| MOD-RT-03 | FS-FAIL-01, FS-FAIL-02 |
| MOD-POST-01 | FS-RG-01 (output), FS-CONF-01 (output) |
| MOD-POST-02 | FS-CONF-02 (output) |
| MOD-POST-03 | FS-WM-01, FS-WM-02, FS-WM-03 |
| MOD-POST-04 | FS-WM-01, FS-WM-02 |
| MOD-HITL-01 | FS-HITL-01, FS-HITL-02, FS-HITL-03, FS-HITL-04, FS-HITL-05 |
| MOD-HITL-02 | FS-HITL-02 |
| MOD-HITL-03 | FS-HITL-03 |
| MOD-AUD-01 | FS-AUD-01, FS-AUD-02, FS-AUD-03, FS-AUD-04, FS-AUD-05, FS-LOG-01, FS-LOG-02, FS-PART11-05 |
| MOD-AUD-02 | FS-LOG-02 |
| MOD-RET-01 | FS-RET-01 |
| MOD-RET-02 | FS-DSR-01 |
| MOD-RG-01 | FS-RED-01, FS-RED-02, FS-RED-03 |
| MOD-RG-02 | FS-RED-02 |
| MOD-RG-03 | FS-RED-03 |
| MOD-PMM-01 | FS-PMM-01, FS-PMM-02, FS-PR-02 |
| MOD-PMM-02 | FS-PMM-02 |
| MOD-INC-01 | FS-INC-01, FS-INC-02, FS-INC-03 |
| MOD-INC-02 | FS-INC-02 |
| MOD-VND-01 | FS-VND-01, FS-VND-02, FS-VND-03, FS-VND-04 |
| MOD-VND-02 | FS-GPAI-01, FS-GPAI-02, FS-GPAI-03, FS-GPAI-04 |
| MOD-VND-03 | FS-PROMPT-02 |
| MOD-VND-04 | FS-VND-04 |
| MOD-REG-01 | FS-REG-01, FS-REG-02 |
| MOD-REG-02 | FS-INT-PORT-01 |
| MOD-DEP-01 | FS-DEP-01, FS-DEP-02, FS-DEP-03 |
| MOD-DEP-02 | FS-DEP-02 |
| MOD-DEP-03 | FS-DEP-03 |
| MOD-QMS-01 | FS-QMS-01, FS-QMS-02 |
| MOD-QMS-02 | FS-QMS-02 |
| MOD-DEV-01 | FS-DEV-01, FS-DEV-02, FS-DEV-03, FS-DEV-04, FS-DEV-05 |
| MOD-DEV-02 | FS-DEV-02 |
| MOD-DEV-03 | FS-DEV-03 |
| MOD-DEV-04 | FS-DEV-04 |
| MOD-DEV-05 | FS-DEV-05 |
| MOD-DEP-LOG-01 | FS-LOG-01, FS-DI-01, FS-DI-02 |
| MOD-DEP-LOG-02 | FS-DI-04 |
| MOD-DSR-01 | FS-DSR-01, FS-DSR-02, FS-DSR-03 |
| MOD-DSR-02 | FS-DSR-02 |
| MOD-DSR-03 | FS-DSR-03 |
| MOD-OSS-01 | FS-OSS-01, FS-OSS-02 |
| MOD-OSS-02 | FS-OSS-02 |
| MOD-PEN-01 | FS-PEN-01 |
| MOD-RES-01 | FS-RES-01, FS-RES-02, FS-RES-03 |
| MOD-CACHE-01 | FS-CACHE-01 |
| MOD-CACHE-02 | FS-CACHE-02 |
| MOD-CACHE-03 | FS-CACHE-03 |
| MOD-TRN-01 | FS-TRN-01, FS-TRN-02, FS-TRN-03 |
| MOD-TRN-02 | FS-TRN-02 |
| MOD-TRN-03 | FS-TRN-03 |
| MOD-HD-01..03 | FS-HD-01, FS-HD-02, FS-HD-03 |
| MOD-HQ-01..02 | FS-HQ-01, FS-HQ-02 |
| MOD-PR-01 | FS-PR-01, FS-PR-02, FS-PR-03 |
| DS-INT-SSO-01 | FS-INT-SSO-01, FS-PART11-02, FS-PART11-07 |
| DS-INT-APIGW-01 | FS-INT-APIGW-01 |
| DS-INT-SIEM-01 | FS-INT-SIEM-01, FS-AUD-04 |
| DS-INT-DPIA-01 | FS-INT-DPIA-01 |
| DS-INT-GIT-01 | FS-INT-GIT-01 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| DS-XINT-LMS-01 | FS-XINT-LMS-01 |
| DS-PART11-01 | FS-PART11-01 |
| DS-PART11-02 | FS-PART11-02 |
| DS-PART11-03 | FS-PART11-03 |
| DS-PART11-04 | FS-PART11-04 |
| DS-PART11-05 | FS-PART11-05 |
| DS-PART11-06 | FS-PART11-06 |
| DS-PART11-07 | FS-PART11-07 |
| DS-PART11-08 | FS-PART11-08 |
| DS-PART11-09 | FS-PART11-09 |
| DS-PART11-10 | FS-PART11-10 |
| DS-PART11-11 | FS-PART11-11 |
| DS-PART11-12 | FS-PART11-12 |
| DS-AV-01 | FS-AV-01 |
| DS-AV-02 | FS-AV-02 |
| DS-PERF-01 | FS-PERF-01 |
| DS-PERF-02 | FS-PERF-02 |
| DS-DI-01 | FS-DI-01 |
| DS-DI-02 | FS-DI-02 |
| DS-DI-03 | FS-DI-03 |
| DS-DI-04 | FS-DI-04 |
| DS-DI-05 | FS-DI-05 |
| DS-DI-06 | FS-DI-06 |
| DS-DI-07 | FS-DI-07 |
| DS-DI-08 | FS-DI-08 |
| DS-BAK-01 | FS-BAK-01 |
| DS-BAK-02 | FS-BAK-02 |
| DS-BAK-03 | FS-BAK-03 |
| DS-BAK-04 | FS-BAK-04 |
| DS-SEC-01 | FS-SEC-01 |
| DS-SEC-02 | FS-SEC-02 |
| DS-SEC-03 | FS-SEC-03 |
| DS-SEC-04 | FS-SEC-04 |
| DS-SEC-05 | FS-SEC-05 |
| DS-SEC-06 | FS-SEC-06 |

**Coverage footnote.** 145 of 151 FS-IDs covered. Vendor-internal FS-IDs not designed at site level: Anthropic + OpenAI internal model behaviour; vLLM scheduler internals; Lakera Guard internal rule engine.

**Phantom-ID disclosure (METHODOLOGY § 2B.2 rule 2 compliance).** The following DS-IDs appear in this Appendix A matrix as per-ID rows (1-to-1 traced to the parent FS) but are NOT enumerated in §§ 4–11 of this DS body: DS-PART11-01 through DS-PART11-12 (12 IDs); DS-DI-01 through DS-DI-08 (8 IDs); DS-BAK-01 through DS-BAK-04 (4 IDs); DS-SEC-01 through DS-SEC-06 (6 IDs). The 30 IDs are bound to the platform's MOD-* design substrate as follows: DS-PART11-* via MOD-AUD-01 + MOD-INT-SSO-01 (audit-trail + 21 CFR Part 11 signature path); DS-DI-* via MOD-AUD-01 + MOD-DEP-LOG-01 + MOD-DEP-LOG-02 (data-integrity / ALCOA+ logging path); DS-BAK-* via DS-XSYS-BAK-01 (Aurora cross-system backup service consumption); DS-SEC-* via MOD-GW-02 + Vault + Istio AuthorizationPolicy + per-tenant NetworkPolicy (the security substrate distributed across the MOD-* modules). These 30 IDs are documented for FS-traceability completeness; their realisation lives in the named MOD-* modules of §§ 4–11. A future revision may either lift these into per-ID body rows or formally fold them into the MOD-* expansion.

## 14. Design-level Risk Register

| ID | Design-stage risk | Likelihood | Impact | Bound modules | Mitigation |
|---|---|---|---|---|---|
| D-01 | **Per-use-case Annex classification error** — Annex I use-case classified as Art. 50 → no Art. 11 pack, no Notified Body, no Art. 49 reg | Medium | **Critical (Art. 99: up to €15M / 3% turnover)** | MOD-UC-02, MOD-UC-05 | Classification Officer manual review; periodic reassessment (MOD-PR-01) |
| D-02 | **Prompt-injection bypass** — adversary smuggles instruction past pre-filter → Annex I downstream consumes harmful output | High | **Critical** | MOD-PRE-01, MOD-PI-* | Quarterly red-team (MOD-RG-01); Lakera Guard updates; output post-filter as defence-in-depth |
| D-03 | **Art. 50 transparency label missing** on synthetic output | Medium | High | MOD-POST-03 | Per-use-case policy enforcement + OQ test |
| D-04 | **HITL evidence-row bypass** via `bulk_accept=true` payload | Low | **Critical** | MOD-HITL-02 | Server-side rejection at API; audit-row on attempt |
| D-05 | **Upstream Anthropic / OpenAI model version drift** — silent capability change breaks downstream determinism | High | High | MOD-VND-03, MOD-VND-04 | Snapshot pinning per use-case; drift detector; CR before promotion |
| D-06 | **Vendor outage (Anthropic + OpenAI simultaneously)** — Annex I service unavailable | Low | High | MOD-RT-03 | Failover to alternate vendor + vLLM fallback |
| D-07 | **Tenant egress ACL bypass** via misconfigured NetworkPolicy → tenant-direct to anthropic.com | Low | **Critical (data exfil + Art. 15 supply-chain)** | MOD-GW-02 | NetworkPolicy + Istio AuthorizationPolicy dual-defence; audit alert on policy violations |
| D-08 | **Art. 73 incident clock missed** (15 d / 10 d / 2 d) | Low | **Critical** | MOD-INC-01 | UTC clock; cron clock-advancer; D-3 / D-1 / D0 alerts |
| D-09 | **Per-tenant API-key leak** | Low | **Critical** | Vault per-tenant namespace | Vault audit log; rotation (max 90 d); revoke + rotate on incident |
| D-10 | **OWASP LLM06 PII exfil** in output | Medium | High | MOD-POST-02 | DLP rules; OQ test; per-use-case GxP redaction |
| D-11 | **OWASP LLM10 model theft** via prompt-probe | Low | High | MOD-CFG-DEF (rate-limit) | Per-consumer rate-limit; output-strip on probe pattern |
| D-12 | **Lakera Guard outage** — pre/post filters down | Medium | High | MOD-PRE-01, MOD-POST-01 | Fail-closed default for Annex I; cached rule-set fallback |
| D-13 | **Per-customer-VPC drift** between tenants — security policy not propagated | Medium | High | MOD-DEV-01, MOD-GW-02 | Terraform state validation; drift-detection cron |
| D-14 | **Art. 11 pack expiry** — use-case continues without active pack | Low | **Critical (Art. 99)** | MOD-UC-04 (`art11_pack_expires_at`) | Gate returns 403 when pack expired; D-30 alert |
| D-15 | **GPAI upstream-obligation lapse** — Anthropic or OpenAI loses GPAI compliance, downstream Hydra exposure | Low | High | MOD-VND-02 | Continuous monitoring; vendor compliance attestation review |
| D-16 | **Red-team baseline drift** undetected — use-case becomes vulnerable | Medium | High | MOD-RG-03 | Quarterly comparison + 10pp threshold + re-validation |
| D-17 | **Cache poisoning** — wrong response served to different tenant | Low | **Critical** | MOD-CACHE-03 | Cache key includes tenant_id + usecase_id + snapshot_sha256; per-tenant cache isolation |
| D-18 | **DSR erasure incomplete** — upstream Anthropic / OpenAI retains data after Hydra erasure | Medium | High | MOD-DSR-02 | RTBF coordination with vendor; documented vendor SLA |
| D-19 | **Cross-tenant data leak** via shared Pinecone namespace | Low | **Critical** | MOD-DEV-05 | Per-tenant Pinecone namespace; access-policy validation |
| D-20 | **Audit-trail tampering** — `audit_events` table mutation by privileged | Low | **Critical** | MOD-AUD-01 | DB-role enforcement (only `audit-writer` INSERT) |
| D-21 | **Token-budget exhaustion** mid-call for Annex I use-case | Medium | Medium | MOD-GW-03 | Pre-flight check + grace + reviewer-escalation path |
| D-22 | **Prompt-template drift** — Annex I template changed without CR | Medium | High | MOD-PROMPT-01 | GitLab signed-tags + change-control gate |
| D-23 | **Vendor advisory missed** — Anthropic / OpenAI publishes security disclosure not ingested | Low | High | MOD-VND-01 | Multiple feed channels + SLA on review |
| D-24 | **Watermarking bypassed** for synthetic media | Medium | Medium | MOD-WM-* | OQ test; output post-filter detection |
| D-25 | **FRIA missing for new Annex-III public-body deployer** | Low | High | MOD-DEP-02 | Onboarding gate; CR check |
| D-26 | **Pen-test finding** unremediated | Medium | High | MOD-PEN-01 | CR tracking; remediation SLA |
| D-27 | **DR drill** misses a tenant or critical-path module | Low | High | MOD-RES-01 | Checklist coverage; per-tenant rotation |
| D-28 | **Reviewer queue overflow** — HITL backlog blocks Annex I throughput | Medium | High | MOD-HITL-03 | Reviewer-staffing model + escalation |
| D-29 | **GDPR Art. 22(3) safeguard insufficient** — automated decision without human-intervention path | Low | High | MOD-DSR-03 | HITL gate + human-intervention path always available |
| D-30 | **EU AI DB registration lag** — Annex-I use-case live without Art. 49 entry | Low | **Critical** | MOD-REG-01 | Registration gate before EFFECTIVE state |
| D-31 | **OWASP LLM05 supply-chain** — vendor SDK compromise | Low | **Critical** | MOD-VND-01 + SBOM + Trivy | Trivy CI block; SBOM diff review on dep bump |
| D-32 | **Cross-system Sirius PV (FS-XINT-HYD-*) misconfiguration** — Sirius Argus PV adapter sends use-case ID that does not exist | Medium | High | MOD-UC-01, MOD-GW-01 | 403 on unknown use-case + audit + alert |
| D-33 | **Cross-system Helios audit-publish (FS-XINT-HEL-*) lag** > 600 s | Medium | Medium | MOD-HD-01..03 | Prometheus `helios_publish_lag_seconds` alert + back-pressure |
| D-34 | **NIS2 reporting cycle missed** — Hydra as essential entity has 24h notification + 72h report + final-report SLAs | Low | **Critical** | MOD-INC-01..02 | NIS2 clocks added to incident service; CSO escalation |
| D-35 | **CycloneDX SBOM** not regenerated on Trivy-CVE patch — silent supply-chain drift | Low | High | CI pipeline | CI block on SBOM-staleness |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
