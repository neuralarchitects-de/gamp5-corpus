---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-27; expanded 2026-05-11 (§5 breakout + EU AI Act binding + DACH context); enriched 2026-05-12 Wave 3 Chunk I (per-use-case Annex I/III/Art.50 decision-tree + T4 depth uplift)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed., 2022) Cat 5 conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11"
  - "EU GMP Annex 22 (DRAFT, consultation closed October 2025) — cited as draft"
  - "EU AI Act 2024/1689 Arts. 5, 8–21, 26, 43, 47, 48, 49, 50, 51, 53, 55, 72, 73, 99, 113"
  - "EMA Reflection Paper on the use of Artificial Intelligence in the Medicinal Product Lifecycle (2024)"
  - "FDA AI/ML SaMD Action Plan (2021)"
  - "FDA Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions (August 2025)"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026)"
  - "ISPE GAMP GPG AI/ML in GxP (2024); ISPE GAMP 5 (2nd ed., 2022)"
  - "GDPR Reg. (EU) 2016/679 Arts. 6, 9, 22, 32, 35, 44 (international transfer)"
  - "EU Data Act (Reg. 2023/2854) where applicable"
  - "ISO/IEC 42001:2023 — Artificial Intelligence Management System"
  - "ISO/IEC 23894:2023 — AI Risk Management"
  - "ISO/IEC 27001:2022 — Information Security Management Systems"
  - "NIST AI Risk Management Framework 1.0 + NIST AI 600-1 Generative AI Profile (July 2024)"
  - "OWASP Top 10 for LLM Applications (2024)"
  - "BfArM (DE) AI guidance; Swissmedic (CH) AI guidance; AGES (AT)"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# User Requirements Specification (URS)

## Validated GenAI / LLM-as-a-Service for GxP — Site-Developed Gateway over Anthropic + OpenAI APIs

**Document Number:** HYD2-URS-GENAI-001 | **Version:** 1.2 | **Effective Date:** 2026-04-27 *(synthetic)*
**Site:** Hydra BioPharma AG, AI Engineering Platform, Basel, Switzerland *(fictional)*
**System Owner:** Head of AI Engineering Platforms
**Process Owner:** VP AI / Data Science
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom Application
**Project Mode:** Custom-build project — site-developed system (GAMP 5 Category 5 — Bespoke; internal SDLC). System: Site-Developed Gateway over Anthropic + OpenAI APIs.
**EU AI Act 2024/1689 classification:** **Per-use-case decision-tree** (see § 3 below):
  - GxP-decision-informing use cases (RTRT-supporting LLM analytics; clinical-trial protocol drafting feeding regulatory submission; pharmacovigilance triage) → **Annex I high-risk** (safety component of regulated product). **Deadline 2 August 2027.**
  - Biometric-like or essential-services-gating use cases (rare in this corpus; e.g., hospital-admission triage if deployed) → **Annex III high-risk**. **Deadline 2 August 2026.**
  - Document-drafting-only use cases (non-regulatory document drafts, internal search-augmentation) → **Article 50 transparency** (not high-risk). Continuous.
  - All GPAI vendor models used through this gateway (Anthropic Claude / OpenAI GPT) → GPAI obligations per **Arts. 51–55** apply to the vendor; site retains downstream-deployer responsibilities per Art. 26.
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11; EU GMP Annex 22 (DRAFT); ICH Q9(R1); EU AI Act 2024/1689 Arts. 5, 8–21, 26, 43, 47, 48, 49, 50, 51–55, 72, 73, 99, 113; GDPR Arts. 6, 9, 22, 32, 35, 44; FDA *AI/ML-Based SaMD Action Plan* (2021); FDA *PCCP for AI-Enabled Device Software Functions* (August 2025); FDA CSA (February 2026); EMA *Reflection Paper on the use of AI in the Medicinal Product Lifecycle* (2024); ISPE GAMP GPG *AI/ML in GxP* (2024); ISO/IEC 42001:2023; ISO/IEC 23894:2023; NIST AI RMF 1.0 + GenAI Profile (2024); OWASP Top 10 for LLM Applications (2024); Swissmedic AI guidance (CH); BfArM AI guidance (DE); AGES (AT).

> **Re-classification note (v1.2):** v1.1 declared a generic "limited-risk vs high-risk per-use-case" framework with an Aug-2026 deadline. v1.2 sharpens this per METHODOLOGY § 2A.14: GxP-decision-informing use cases are **Annex I (deadline 2027)**; biometric-like or essential-services-gating use cases are Annex III (deadline 2026); doc-drafting-only use cases trigger **Art. 50 transparency** but are not high-risk. The per-use-case classification gate (§ 5.2 + 5.2a) makes the decision explicit.

> **Note:** Distinct from the AI/ML Model Server (Lyrae URS — bespoke trained models). This URS covers a **vendor-LLM-backed GenAI service** (Anthropic Claude + OpenAI GPT) wrapped in a site-validated gateway with prompt management, response logging, and PHI / PII guard-rails for GxP-supporting use cases (e.g., draft-document generation, search-augmentation, code-review-suggestion, regulatory-text drafting). LLM output **never substitutes** for human judgement in regulated decisions; consumers maintain human-in-the-loop per Art. 14 + Art. 26.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of AI Engineering Platforms) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Privacy / Data Protection Officer) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs — AI/ML) | _____________ | _____________ | _____ |
| Reviewer (Legal — AI / IP / Vendor Contracts) | _____________ | _____________ | _____ |
| Reviewer (InfoSec) | _____________ | _____________ | _____ |
| Reviewer (Conformity Assessment Coordinator) | _____________ | _____________ | _____ |
| Approver (VP AI / Data Science) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |
| Approver (VP Legal) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | §5 broken out into 13 subsections; EU AI Act per-use-case classification framework added (incorrectly tying GxP-decision use cases to 2026 Annex III); site relocated to Basel (DACH); Swissmedic + BfArM added to References; §9 Risks expanded; GDPR Art. 22 + Art. 35 DPIA references added. |
| 1.2 | 2026-05-12 | (synthetic) | **Wave 3 Chunk I enrichment.** Tier T4 uplift. EU AI Act re-classification per-use-case decision-tree: GxP-decision-informing → Annex I (deadline 2027); biometric/essential-services → Annex III (deadline 2026); doc-drafting → Art. 50 only. New subsections: 5.2a use-case classification gate; 5.3a prompt-injection + jailbreak defenses; 5.3b retrieval grounding evidence; 5.3c hallucination detection; 5.3d PII redaction in-flight; 5.3e output watermarking + provenance (Art. 50); 5.3f cost + token-budget controls; 5.3g cache-poisoning defenses; 5.4a human-in-the-loop for GxP outputs; 5.5a vendor GPAI obligations (Arts. 51–55); 5.5b vendor data-residency + Art. 44 international transfer; 5.7a Art. 11 + Annex IV pack per high-risk use case; 5.7b Art. 12 logging ≥ 6 mo / Art. 18 retention ≥ 10 y; 5.7c Art. 43+47+48 conformity + CE + EU DoC; 5.7d Art. 49 EU database registration; 5.7e Art. 72 PMM; 5.7f Art. 73 incident reporting (15 d / 10 d / 2 d); 5.7g Art. 26 deployer obligations + FRIA; 5.7h Art. 17 + ISO/IEC 42001 QMS; 5.7i Art. 18 retention; 5.7j Art. 99 penalty awareness; OWASP LLM Top 10 binding; §9 Risks expanded with 7 new domain-specific risks. |

## Definitions

| Term | Definition |
|---|---|
| GenAI | Generative AI |
| LLM | Large Language Model |
| Vendor LLM | External LLM API (Anthropic Claude, OpenAI GPT, etc.) |
| Gateway | Site-developed validated wrapper |
| Prompt Template | Pre-approved prompt structure for a specific use case |
| Guard-Rail | PHI / PII / regulated-content detection + redaction or block |
| Hallucination | LLM-generated content not grounded in input or factually incorrect |
| Use Case | A specific, approved consumer-application + LLM-task pairing |
| DPIA | Data Protection Impact Assessment (GDPR Art. 35) |
| FRIA | Fundamental Rights Impact Assessment (EU AI Act Art. 27) |
| BAA / DPA | Business Associate Agreement / Data Processing Agreement (with vendor LLM) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| GPAI | General-Purpose AI model (EU AI Act Arts. 51–55) |
| Prompt Injection | Adversarial input crafted to override system prompt or extract sensitive content |
| Jailbreak | A prompt-injection variant achieving bypass of safety policies |
| Retrieval Augmentation | RAG: providing the LLM with retrieved context to ground responses |
| Watermarking | Embedding signals identifying AI-generated content per Art. 50 |
| Annex I high-risk | Safety component of regulated product. EU AI Act Art. 6(1). Deadline 2 Aug 2027. |
| Annex III high-risk | One of 8 listed domains. EU AI Act Art. 6(2). Deadline 2 Aug 2026. |
| Art. 50 transparency | AI-generated content must be labelled; applies to all AI systems (not just high-risk). |
| Use-Case Classification | Per-use-case mapping to Annex I / Annex III / Art. 50 / non-high-risk |

## 1. Purpose

This URS defines requirements for the validated GenAI / LLM service used by GxP-supporting consumers (e.g., draft-document generation, search-augmentation, code-review-suggestion, regulatory-text drafting, pharmacovigilance triage support). The service exposes vendor LLMs (Anthropic Claude, OpenAI GPT) through a site-validated gateway with prompt management, guard-rails, response-logging, per-use-case EU AI Act classification, and per-use-case Art. 11 + Annex IV technical-documentation packs where the use case is high-risk.

## 2. Scope

**In:** site-developed Python gateway on K8s wrapping vendor LLM APIs (Anthropic Claude + OpenAI GPT); per-use-case prompt templates (Cat 5 sub-components); PHI / PII guard-rails (input redaction + output filtering); prompt-injection + jailbreak defences; retrieval-grounding evidence pipeline; hallucination detection; output watermarking / provenance per Art. 50; cost + token-budget controls; response-logging per Art. 12; consumer-facing API behind site API Gateway; Okta SSO + MFA; integrations with Splunk SIEM, Application Portfolio, validated GitLab. Per-use-case EU AI Act classification documentation (Annex I / III / Art. 50). Per-use-case Art. 11 + Annex IV technical-documentation packs where high-risk. Transparency labelling per Art. 50 universally where AI-generated content is shown to a natural person. Vendor GPAI obligations awareness (Arts. 51–55).

**Out:** consumer applications (each separately validated for the consumed-output use); vendor LLM training (vendor responsibility under Arts. 51–55); decisions made on LLM output (always human-in-the-loop per intended use); EU AI Act Art. 43 conformity assessment for high-risk use cases (separate per-use-case scope coordinated with Conformity Assessment Coordinator).

## 3. System Description

The gateway provides per-use-case validated LLM access. Each use case has: prompt template (pinned version), input guard-rails (PHI / PII detection + redaction or block), output guard-rails (hallucination detection where feasible, off-policy content block, Art. 50 watermark), response-logging, retrieval-grounding pipeline (where RAG applies), prompt-injection defence. Vendor LLM model + version pinned per use case. Output **never substitutes for human judgement** in regulated decisions; consumers are required to maintain human-in-the-loop with documented review evidence.

### Classification decision-tree (per METHODOLOGY § 2A.14)

```
Is the use-case output a safety component informing
a regulated medicinal-product / medical-device decision?
   │
   ├─ Yes  ─►  Annex I high-risk. Arts. 8–21 apply.
   │          Deadline 2 Aug 2027.
   │          Annex IV pack required; conformity assessment per Art. 43.
   │
   └─ No   ─►  Is the use case in one of the 8 Annex III domains
              (biometric ID, critical infra, education, employment,
               essential services, law enforcement, migration,
               admin of justice)?
                  │
                  ├─ Yes  ─►  Annex III high-risk. Arts. 8–21 apply.
                  │          Deadline 2 Aug 2026.
                  │          EU database registration per Art. 49.
                  │          FRIA per Art. 27 where deployer obligations apply.
                  │
                  └─ No   ─►  Art. 50 transparency only.
                             Output must be labelled as AI-generated.
                             No high-risk obligations attach.
```

GAMP Cat 5: full SDLC. Each use case carries a documented intended use, fitness-for-purpose evidence, EU AI Act per-use-case classification (recorded at the gate), and consumer-side validation evidence.

## 4. User Roles

| Role | Permissions |
|---|---|
| Use-Case Author | Author / edit DRAFT prompt templates under SDLC. |
| Use-Case Reviewer | Review prompts; cannot review own. |
| Use-Case Classifier | Apply the per-use-case EU AI Act classification (Annex I / III / Art. 50 / non-high-risk); attach rationale. |
| Use-Case Approver (QA + Privacy + Reg-Affairs + AI Lead) | Approve to PROD via 4-of-4 signature. |
| Consumer Application | Service-account access via mTLS; per-use-case authorisation. |
| Gateway Administrator | OS / config; cannot approve use cases. |
| Human Oversight Operator (per EU AI Act Art. 14, for high-risk use cases) | Real-time monitoring, ability to halt a use case. |
| Post-Market Monitoring Operator (per Art. 72) | Monitor incident feeds; trigger Art. 73 escalation. |
| Conformity Assessment Coordinator | Maintain Art. 11 + Annex IV pack per high-risk use case; liaise with Notified Body. |
| Data Protection Officer | Sign DPIA per use case; review Art. 44 international-transfer arrangements. |
| Auditor | Read-only across audit. |

Standard SoD; multi-stakeholder approval reflects regulatory + privacy + legal + reg-affairs concerns. Use-Case Author ≠ Use-Case Reviewer ≠ Use-Case Approver. Use-Case Classifier ≠ Use-Case Author.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` / `R2` / `R3`).

### 5.1 Application Lifecycle (Cat 5 SDLC)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEV-01 | H | R1 | The gateway code shall be developed under Cat-5 SDLC: code review, unit tests (≥ 90% coverage on guard-rails), integration tests, regression suite, privacy-officer review, reg-affairs review. |
| URS-DEV-02 | H | R1 | Source shall reside in validated GitLab with signed commits and pinned dependencies. |
| URS-DEV-03 | H | R1 | Deployment shall occur via approved Change Request; a rollback runbook shall be tested before each release. |
| URS-DEV-04 | H | R1 | The gateway shall log its own version + build metadata in every response header for downstream traceability. |
| URS-DEV-05 | H | R1 | The gateway shall be hardened against the OWASP Top 10 for LLM Applications (2024) — at minimum LLM01 prompt injection, LLM02 insecure output handling, LLM03 training-data poisoning, LLM04 model DoS, LLM06 sensitive information disclosure, LLM07 insecure plugin design, LLM08 excessive agency, LLM09 overreliance, LLM10 model theft. |

### 5.2 Use-Case + Prompt Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-UC-01 | H | R1 | Each use case shall carry documented intended use, fitness-for-purpose evidence, vendor-LLM model + version pin, prompt template (versioned), guard-rail configuration, EU AI Act per-use-case classification (Annex I / Annex III / Art. 50 / non-high-risk), and classification-rationale. |
| URS-UC-02 | H | R1 | Use-case lifecycle states: DRAFT → REVIEW → CLASSIFIED → APPROVED → EFFECTIVE → DEPRECATED. State transitions shall require signed change records. |
| URS-UC-03 | H | R1 | Approval to EFFECTIVE shall require 4-of-4 signatures: QA + Privacy + Reg-Affairs + AI Lead; for Annex I use cases an additional Conformity-Assessment-Coordinator signature is required. |
| URS-UC-04 | H | R1 | A vendor-LLM-version change (e.g., Claude 3.5 → Claude 4.0) shall trigger re-approval and re-validation for every use case that pins that model. |
| URS-UC-05 | H | R1 | Where a use case is EU AI Act high-risk (Annex I or III), an Art. 11 + Annex IV Technical Documentation pack shall be on file and linked from the use-case registry. |
| URS-UC-06 | H | R1 | Use-case configuration shall be cryptographically signed at approval; runtime gateway shall verify signature before serving the use case. |

### 5.2a Use-Case Classification Gate (EU AI Act decision-tree)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CLS-01 | H | R1 | Every use case in REVIEW state shall pass through the classification gate before reaching APPROVED. The Use-Case Classifier shall apply the per-use-case decision-tree (Annex I / Annex III / Art. 50 / non-high-risk) per METHODOLOGY § 2A.14. |
| URS-CLS-02 | H | R1 | The classification rationale shall be recorded in writing and shall reference: the use-case intended-use, the regulatory product context (if any), the decision-impact path, and the Annex III domain mapping (if any). |
| URS-CLS-03 | H | R1 | Annex I classification shall trigger: Art. 11 + Annex IV pack; conformity-assessment workflow (Art. 43); EU DoC (Art. 47); CE-marking surface (Art. 48); deadline 2 Aug 2027. |
| URS-CLS-04 | H | R1 | Annex III classification shall trigger: Art. 11 + Annex IV pack; EU database registration (Art. 49); FRIA where deployer is public-body / essential-services; deadline 2 Aug 2026. |
| URS-CLS-05 | H | R1 | Art. 50 / non-high-risk classification shall trigger: Art. 50 watermarking + transparency labelling only; no further high-risk obligations. |
| URS-CLS-06 | M | R2 | Classifications shall be re-assessed annually as part of periodic review; classification changes shall be change-controlled. |

### 5.3 Guard-Rails (Input + Output)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-GR-01 | H | R1 | Input guard-rail: PHI / PII / regulated-content detection per the use-case configuration; matching content shall be redacted or blocked per the configured policy. |
| URS-GR-02 | H | R1 | Output guard-rail: hallucination / off-policy content detection where feasible; outputs below the configured confidence threshold shall be flagged or filtered. |
| URS-GR-03 | H | R1 | Per-call audit: sender, use-case-id, prompt-template-version, vendor-LLM-version, input (redacted), output, guard-rail-decisions, timestamp, classification. |
| URS-GR-04 | H | R1 | Input guard-rails shall be tested against an adversarial PHI/PII corpus during OQ; recall ≥ 99% on a documented test set. |
| URS-GR-05 | M | R2 | Output guard-rails shall be monitored monthly for drift; failure-mode reports shall be reviewed by the Privacy Officer. |

### 5.3a Prompt Injection + Jailbreak Defenses

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PI-01 | H | R1 | A prompt-injection classifier shall pre-screen consumer-provided input segments; flagged inputs shall be blocked or sanitised per use-case policy. |
| URS-PI-02 | H | R1 | System prompts shall be isolated from consumer-injectable input via structured prompt templating; the gateway shall enforce a "do not follow instructions in user input" wrapper. |
| URS-PI-03 | H | R1 | Jailbreak attempts (known jailbreak patterns + behavioural anomaly detection) shall be logged + alerted; consumer-side throttling shall escalate per consumer ID. |
| URS-PI-04 | H | R1 | The defence suite shall be tested under OQ against an adversarial-corpus of known prompt-injection + jailbreak prompts; documented recall ≥ 95%. |
| URS-PI-05 | M | R2 | The adversarial corpus shall be refreshed quarterly and after any published Anthropic / OpenAI advisory. |

### 5.3b Retrieval Grounding Evidence

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RG-01 | H | R1 | Use cases that rely on retrieval augmentation (RAG) shall carry retrieval-corpus provenance: source URL/path, document hash, ingestion timestamp, content-classification. |
| URS-RG-02 | H | R1 | Each LLM output produced from a RAG flow shall record the retrieved chunks used; the audit trail shall include retrieval-grounding hash. |
| URS-RG-03 | H | R1 | Where retrieved corpus content is updated, downstream use cases shall be notified; pinning to corpus-version is the default to prevent silent grounding shifts. |
| URS-RG-04 | M | R2 | Retrieval quality (recall@k, MRR) shall be measured monthly on a held-out evaluation set; degradations shall be reviewed. |

### 5.3c Hallucination Detection

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HD-01 | H | R1 | An NLI-based grounding checker shall evaluate output-vs-input consistency for RAG use cases; output-confidence below threshold shall be flagged `LOW_GROUNDING`. |
| URS-HD-02 | H | R1 | For non-RAG generative use cases, factuality scoring shall use vendor-provided uncertainty signals + use-case-specific reference checks (e.g., regulatory-text drafting checks against published source text). |
| URS-HD-03 | M | R2 | Hallucination-detection metrics shall be reviewed monthly by the Privacy Officer + Reg-Affairs; thresholds shall be tuned per use case. |

### 5.3d PII Redaction In-Flight

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RED-01 | H | R1 | PII redaction shall occur **before** content leaves the site network boundary toward the vendor LLM API; the gateway shall log redaction events with category-of-redaction (name / DoB / ID / health-data) but NOT the redacted content. |
| URS-RED-02 | H | R1 | Where the use-case policy prohibits any personal-data transmission to vendor LLMs, the gateway shall block the call on redaction failure or low-confidence detection. |
| URS-RED-03 | H | R1 | Where vendor LLM is hosted in a country requiring GDPR Art. 44 international-transfer mechanism, the use case shall carry a documented SCC / adequacy decision reference. |

### 5.3e Output Watermarking + Provenance (Art. 50)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-WM-01 | H | R1 | All LLM outputs shall be labelled as AI-generated per EU AI Act Art. 50; the gateway shall emit response header `X-AI-Generated-Content: true` and an inline-watermark token where text is consumed by end-user UIs. |
| URS-WM-02 | H | R1 | Output provenance metadata shall include: use-case-id, model + version, prompt-template version, retrieval-grounding hash (where RAG), timestamp, gateway version. |
| URS-WM-03 | M | R2 | Where regulator-defined machine-readable watermarking standards become available, the gateway shall adopt them via change-controlled update. |

### 5.3f Cost + Token-Budget Controls

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-COST-01 | H | R1 | Each use case shall declare a token-budget ceiling (per call + per day); calls exceeding the ceiling shall return `BUDGET_EXCEEDED`. |
| URS-COST-02 | M | R2 | Aggregate cost telemetry (tokens-in, tokens-out, cost-USD per call) shall be exposed via dashboard and forwarded to FinOps daily. |
| URS-COST-03 | M | R2 | Anomalous-cost spikes shall page the System Owner; runaway-cost defence is a documented operational control. |

### 5.3g Cache-Poisoning Defenses

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CACHE-01 | H | R1 | Response caches (where used) shall key off `hash(prompt + retrieval_corpus_version + model_version + use_case_id)`; cache poisoning by replay shall be infeasible. |
| URS-CACHE-02 | H | R1 | Cache entries shall be signed at write; verification shall occur at read. |
| URS-CACHE-03 | M | R2 | Cache TTL shall be configurable per use case and bounded above by the retrieval-corpus freshness SLA. |

### 5.4 Human-in-the-Loop and Transparency

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HITL-01 | H | R1 | LLM output shall never substitute for human judgement in regulated decisions; consumers must implement human-in-the-loop with review evidence captured downstream. |
| URS-HITL-02 | H | R1 | Per EU AI Act Art. 50, AI-generated content shall be labelled as such where the end-user sees the output; the gateway shall enforce response-header labelling. |
| URS-HITL-03 | H | R1 | For high-risk use cases (per Art. 14), a Human Oversight Operator shall have monitoring + halt authority on the use case in production. |
| URS-HITL-04 | H | R1 | For Annex I use cases informing GxP-decision pathways, consumer SDK shall expose `requires_human_approval=true` and block downstream consumption until a documented human approval record is captured. |
| URS-HITL-05 | H | R1 | The Human Oversight Operator UI shall surface the use-case IFU (capabilities, limits, foreseeable misuse, accuracy metrics, known failure modes) per Art. 13. |

### 5.4a HITL Quality Metrics

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HQ-01 | M | R2 | For Annex I use cases, downstream consumer-side human review outcomes (accept / modify / reject) shall be reported back to the gateway for PMM analysis. |
| URS-HQ-02 | M | R2 | Frequent-rejection patterns shall trigger use-case-level fitness re-review. |

### 5.5 Vendor LLM Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-01 | H | R1 | A Data Processing Agreement (DPA) / Business Associate Agreement (BAA) shall be on file with each vendor LLM provider; data-residency clauses shall be documented per regulation. |
| URS-VND-02 | H | R1 | The gateway shall pin vendor-LLM model + version per use case; auto-upgrade is prohibited. |
| URS-VND-03 | H | R1 | Vendor LLM outage shall return a structured error to consumers; consumers must not silently consume null defaults. |
| URS-VND-04 | M | R2 | Vendor LLM cost telemetry shall be exposed for downstream FinOps reconciliation. |

### 5.5a Vendor GPAI Obligations (EU AI Act Arts. 51–55)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-GPAI-01 | H | R1 | The gateway shall maintain a registry of vendor-LLM GPAI classification (general-purpose, GPAI-with-systemic-risk per Art. 51) and the vendor-provided technical-documentation reference per Art. 53. |
| URS-GPAI-02 | H | R1 | Where the vendor LLM is GPAI-with-systemic-risk (Art. 55), the gateway shall require vendor-provided model-evaluation evidence, adversarial-testing evidence, and serious-incident reporting commitment. |
| URS-GPAI-03 | M | R2 | Vendor GPAI compliance status shall be reviewed quarterly; vendor commitments shall be referenced in the vendor DPA / BAA. |
| URS-GPAI-04 | H | R1 | GPAI deadlines apply from **2 August 2025**; the gateway shall not onboard a GPAI vendor that does not evidence compliance with Arts. 53 / 55 transparency + technical-documentation obligations. |

### 5.5b Vendor Data-Residency + GDPR Art. 44 International Transfer

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RES-01 | H | R1 | Each vendor LLM endpoint shall carry a declared data-residency region; the gateway shall route to EU-region endpoints by default. |
| URS-RES-02 | H | R1 | Where data must transit outside the EEA, the use case shall carry a documented GDPR Art. 44 mechanism: SCC, adequacy decision, BCR, or derogation per Art. 49 (rare). |
| URS-RES-03 | H | R1 | The DPO shall review Art. 44 mechanism per use case at approval and annually thereafter. |

### 5.6 Audit Trail and Records Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | All gateway events shall be logged to Splunk within 5 minutes; retention shall be immutable ≥ 25 years for clinical-impact use cases and ≥ 10 years (Art. 18) for all high-risk use cases. |
| URS-AUD-02 | H | R1 | Audit-trail entries shall not be editable or deletable by any user, including Gateway Administrators. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be performed weekly by the System Owner and annually by QA. |
| URS-AUD-04 | M | R2 | Audit logs shall be exportable for inspection without disrupting routine operation. |
| URS-AUD-05 | H | R1 | The audit trail shall capture: use-case state transitions, classification changes, approval signatures, runtime call records, guard-rail decisions, prompt-injection alerts, hallucination flags, override interventions, and Art. 73 incident triggers. |

### 5.7 21 CFR Part 11 Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a), procedures and controls protecting the validity of electronic records shall be enforced. |
| URS-PART11-02 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via Okta SSO + MFA. |
| URS-PART11-03 | H | R1 | Per § 11.10(e), operational audit trail shall capture user, action, date, time. |
| URS-PART11-04 | H | R1 | Per § 11.50, electronic signatures applied to use-case approvals shall include signer's printed name, date and time of signing, and meaning of signature. |
| URS-PART11-05 | H | R1 | Per § 11.70, signatures shall be cryptographically linked to the signed record; subsequent record changes shall invalidate the signature. |
| URS-PART11-06 | H | R1 | Per § 11.200, re-authentication shall be required at the moment of signing. |
| URS-PART11-07 | H | R1 | Per § 11.300, password / credential controls shall meet site InfoSec policy. |
| URS-PART11-08 | H | R1 | Per § 11.10(b), the system shall produce accurate and complete copies of records in both human-readable and electronic form for inspection. |
| URS-PART11-09 | H | R1 | Per § 11.10(c), records shall be protected for the full retention period (≥ 10 y per Art. 18 + ≥ 25 y for clinical-impact). |
| URS-PART11-10 | H | R1 | Per § 11.10(k), system operation manuals + change control shall be maintained; SOPs reviewed annually. |
| URS-PART11-11 | H | R1 | Per § 11.30, open-system controls (encryption-in-transit, digital signatures with non-repudiation) shall apply at all internet-facing boundaries. |
| URS-PART11-12 | H | R1 | Per § 11.100, electronic signatures shall be unique and not reused. |

### 5.7a Art. 11 + Annex IV Pack per High-Risk Use Case

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TD-01 | H | R1 | Each high-risk use case shall maintain an Art. 11 + Annex IV pack containing: intended-use description, design + development description (SDLC + prompt design + RAG architecture), data-governance per Art. 10 (training-data + retrieval-corpus), monitoring + functioning + control, declared accuracy / robustness / cybersecurity metrics, risk-management per Art. 9, lifecycle change-management, compliance-with-harmonised-standards statement. |
| URS-TD-02 | H | R1 | The pack shall be kept up-to-date over the deployed lifetime of the use case; lifecycle changes trigger pack revision under change control. |
| URS-TD-03 | M | R2 | The pack shall be exportable within 1 business day for notified-body inspection. |

### 5.7b Art. 12 Logging + Art. 18 Retention

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LOG-01 | H | R1 | Automatic event logs per Art. 12 shall be retained ≥ 6 months on hot storage; runtime traceability shall be preserved (actor, use-case-id, timestamp, request-id, model + version, retrieval-corpus-version, guard-rail decisions, output-hash). |
| URS-LOG-02 | H | R1 | Per Art. 18, all Art. 11 + Annex IV pack content, EU DoCs, conformity records, training records, post-market monitoring records shall be retained **≥ 10 years after the use case is placed on the market or put into service**. |

### 5.7c Art. 43 Conformity + Art. 47 EU DoC + Art. 48 CE Marking

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CONF-01 | H | R1 | Each Annex I high-risk use case shall undergo conformity assessment per Art. 43 before going EFFECTIVE; the pathway shall be documented (internal control Annex VI vs notified-body Annex VII). |
| URS-CONF-02 | H | R1 | Each high-risk use case shall carry an EU Declaration of Conformity per Art. 47 signed by Reg Affairs (AI/ML). |
| URS-CONF-03 | H | R1 | CE-marking surface per Art. 48 shall be retrievable via `GET /use_case/{id}/ce-marking` for each conformity-assessed use case. |
| URS-CONF-04 | M | R2 | Substantial modifications per Art. 43(4) shall trigger renewed conformity assessment. |

### 5.7d Art. 49 EU Database Registration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REG-01 | H | R1 | Annex III high-risk use cases shall be registered in the EU AI database per Art. 49 before placement on the market or putting into service. |
| URS-REG-02 | M | R2 | Annex I use cases that inherit an underlying product registration (e.g., EUDAMED for SaMD) shall record the underlying registration reference; no separate Art. 49 registration is required. |

### 5.7e Art. 72 Post-Market Monitoring

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PMM-01 | H | R1 | The gateway shall implement post-market monitoring for high-risk use cases: per-call outcomes, guard-rail alerts, downstream human-review outcomes (URS-HQ-01), drift in hallucination + grounding metrics, vendor-LLM-side incident reports. |
| URS-PMM-02 | M | R2 | Quarterly PMM reports per use case shall be reviewed by Reg-Affairs + VP QA; findings shall feed CAPA. |

### 5.7f Art. 73 Serious-Incident Reporting

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INC-01 | H | R1 | Serious incidents (Art. 3(49)) shall be reported to the market-surveillance authority within **15 days standard / 10 days if death / 2 days for widespread fundamental-rights infringement**. |
| URS-INC-02 | H | R1 | Authority routing shall be: Swissmedic for CH-deployed (Basel site default) + BfArM for DE + AGES for AT, with cross-reference to EU MDR Art. 87 channel where the underlying product is a regulated device. |
| URS-INC-03 | H | R1 | The Art. 73 clock shall start at the moment a serious incident is identified by the provider or reported by a deployer; clock progress shall be tracked per incident and surfaced to Reg Affairs. |

### 5.7g Art. 26 Deployer Obligations + FRIA

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEP-01 | H | R1 | Consumer GxP systems acting as deployers shall be contractually required to: use the use case per the IFU, ensure input data is relevant + representative, assign trained human oversight, monitor + suspend on risk, retain logs ≥ 6 months on their side. |
| URS-DEP-02 | H | R1 | Where a deployer is a public-body or essential-services private deployer of an Annex III use case, the deployer shall conduct an FRIA per Art. 27 before first deployment. |
| URS-DEP-03 | M | R2 | The gateway shall expose `GET /use_case/{id}/deployer-obligations` returning a structured Art. 26 / Art. 27 duty list. |

### 5.7h Art. 17 QMS + ISO/IEC 42001:2023

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-QMS-01 | H | R1 | The gateway QMS shall conform to EU AI Act Art. 17 and shall be aligned with ISO/IEC 42001:2023 AI Management System. |
| URS-QMS-02 | H | R1 | QMS effectiveness shall be reviewed annually; review evidence shall feed periodic review. |

### 5.7i Art. 18 Retention Enforcement

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RET-01 | H | R1 | Retention floors shall be policy-coded at the storage-class level; deletion attempts before the retention floor shall be blocked. |

### 5.7j Art. 99 Penalty Awareness

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PEN-01 | M | R2 | The risk register (URS § 9) shall reference Art. 99 penalty tiers (€35M / 7% turnover for prohibited practices; €15M / 3% for high-risk non-compliance; €7.5M / 1% for misleading information to authorities). |

### 5.8 Data Integrity (ALCOA+) and Privacy

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | **Attributable:** Every gateway call shall be attributed to a named user or service account. |
| URS-DI-02 | H | R1 | **Legible:** Audit trail exportable as human-readable JSON / PDF. |
| URS-DI-03 | H | R1 | **Contemporaneous:** Events recorded at time of occurrence. |
| URS-DI-04 | H | R1 | **Original:** Input + redacted-input + output + guard-rail-decisions retained unaltered. |
| URS-DI-05 | H | R1 | **Accurate:** Use-case fitness-for-purpose evidence shall demonstrate the LLM output is suitable for its declared use; misuse outside intended use shall be blocked. |
| URS-DI-06 | H | R1 | **PHI / PII Privacy:** A GDPR Art. 35 DPIA shall be on file for every use case that processes personal data; data-flow agreements with vendor LLMs shall include data-residency clauses + Art. 44 international-transfer mechanism. |
| URS-DI-07 | M | R2 | Records shall meet Complete / Consistent / Enduring / Available criteria. |
| URS-DI-08 | H | R1 | Per Art. 10, retrieval corpora used in high-risk RAG use cases shall be relevant, representative, statistically sound, and bias-evaluated; provenance recorded. |

### 5.9 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-APIGW-01 | H | R1 | The service shall be exposed via the site API Gateway with mTLS and per-use-case OAuth2 scopes. |
| URS-INT-PORT-01 | H | R1 | Use-case inventory shall be maintained in the site Application Portfolio with cross-reference to GxP classification + EU AI Act classification. |
| URS-INT-SSO-01 | H | R1 | All human authentication shall flow through site Okta SSO with MFA enforced. |
| URS-INT-SIEM-01 | H | R1 | Audit logs shall be forwarded to Splunk within 5 minutes; immutable retention ≥ 25 years. |
| URS-INT-GIT-01 | H | R1 | Gateway source + prompt templates shall reside in validated GitLab with signed commits. |
| URS-INT-DPIA-01 | H | R1 | The use-case registry shall reference the DPIA URN; presence enforced for any use case processing personal data. |
| URS-INT-VENDOR-01 | H | R1 | Vendor LLM API integrations shall pin model + version per use case; vendor advisory subscription shall feed into the gateway alert pipeline. |

### 5.10 Performance and Availability

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | Gateway latency P95 shall be ≤ 500 ms over upstream LLM (excluding vendor-LLM time). |
| URS-PERF-02 | M | R2 | The gateway shall sustain ≥ 500 calls/second across all use cases without queue degradation. |
| URS-AV-01 | H | R1 | Availability shall be ≥ 99.5% measured monthly, excluding planned maintenance announced ≥ 7 days in advance. |
| URS-AV-02 | M | R2 | The gateway shall auto-scale between 4 and 32 instances based on call queue depth. |

### 5.11 Backup, Restore, and Disaster Recovery

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | Audit logs, use-case registry, prompt-template store, retrieval corpora index shall be backed up daily with integrity verification. |
| URS-BAK-02 | H | R1 | Quarterly restore tests shall be performed with QA witness. |
| URS-BAK-03 | M | R2 | RTO ≤ 8 hours; RPO ≤ 1 hour. |
| URS-BAK-04 | M | R2 | Annual cold-archive retrieval drill for Art. 18 retention records; documented retrieval time ≤ 24 hours. |

### 5.12 Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | Per EU AI Act Art. 15(5), the gateway shall be hardened per CIS Kubernetes benchmark; non-conformities tracked under change control. |
| URS-SEC-02 | H | R1 | Prompt-injection defences shall be implemented and tested under OQ; documented attack-suite recall ≥ 95% (also covered by URS-PI-04). |
| URS-SEC-03 | H | R1 | Vendor-LLM API keys and signing keys shall be stored in HashiCorp Vault with audit logging; no plaintext secrets in container images. |
| URS-SEC-04 | H | R1 | Container images shall be scanned for CVEs at build time and runtime; HIGH and CRITICAL CVEs shall block deployment. |
| URS-SEC-05 | M | R2 | Pod Security Standards (restricted) shall be enforced; NetworkPolicies shall isolate gateway namespaces. |
| URS-SEC-06 | H | R1 | The gateway shall be evidence-tested against the OWASP Top 10 for LLM Applications (2024); evidence stored in Art. 11 pack for high-risk use cases. |

### 5.13 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | No user shall be granted production access (Use-Case Approver, Gateway Administrator, Human Oversight Operator, Use-Case Classifier, Conformity Assessment Coordinator, PMM Operator) until role-specific training is completed and recorded in the site LMS. |
| URS-TRN-02 | M | R2 | Annual refresher training shall cover EU AI Act obligations (Arts. 8–21 + 26 + 50 + 51–55 + 72 + 73 + 99), hallucination handling, PHI / PII handling, prompt-injection awareness, and incident response. |
| URS-TRN-03 | M | R2 | Per Art. 4, AI-literacy training shall be assigned to all staff with AI-output exposure. |
| URS-PR-01 | H | R1 | An annual periodic review shall cover: use-case inventory, vendor-LLM-version drift, guard-rail efficacy, audit-trail review evidence, EU AI Act conformance per classification, PMM findings, training currency; signed by Head of AI Engineering Platforms + VP QA + VP Reg Affairs + Privacy Officer + Legal + Conformity Assessment Coordinator. |
| URS-PR-02 | H | R1 | Per EU AI Act Art. 72 (where high-risk use cases are deployed), post-market monitoring shall be active; serious incidents shall be reported to the competent authority (Swissmedic for CH-deployed; BfArM for DE; AGES for AT) per Art. 73 within the regulatory timeline (15 d / 10 d / 2 d). |
| URS-PR-03 | M | R2 | Per-use-case EU AI Act classification shall be re-assessed annually; reclassifications shall be change-controlled. |

### 5.14 GDPR Data-Subject Rights (Arts. 15–22)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DSR-01 | H | R1 | Where use cases process personal data, GDPR Art. 15 (right of access), Art. 17 (right to erasure), and Art. 22 (automated decision-making restrictions) request workflows shall be supported. |
| URS-DSR-02 | H | R1 | Art. 22(3) safeguards (right to human intervention, right to express view, right to contest) shall be operationalised via the HITL framework (URS-HITL-03..04). |
| URS-DSR-03 | M | R2 | DSR requests shall be logged + tracked to closure with deadline enforcement per GDPR Art. 12(3). |

### 5.15 Multi-Model Routing + Failover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-FAIL-01 | M | R2 | Where a use case is approved to use multiple vendor LLMs (primary + fallback), the gateway shall implement explicit failover semantics; failover shall not cross EU AI Act classification boundaries. |
| URS-FAIL-02 | M | R2 | Failover events shall be audit-logged + included in PMM telemetry. |

### 5.16 Open-Source Foundation-Model Usage

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-OSS-01 | H | R1 | Where the gateway is configured to route to an open-source / on-prem foundation model (e.g., Llama family), the model artefact + weight provenance + SBOM shall be tracked in the same registry framework as vendor models. |
| URS-OSS-02 | H | R1 | Open-source foundation-model security advisories (Hugging Face Hub + maintainer feeds) shall be subscribed to. |

### 5.17 Prompt-Library Governance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PROMPT-01 | H | R1 | The prompt-template library shall be curated centrally; templates shall be reviewed for prompt-injection vulnerability before approval. |
| URS-PROMPT-02 | M | R2 | Per-template change history shall be preserved + reviewable; significant changes trigger use-case re-approval. |

### 5.18 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is OIDC via Entra ID with workload-identity federation for service-to-service; conditional-access policy `AI-Platform Conditional Access (FIDO2 + device-compliance + risk-based step-up)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the gateway audit store and use-case registry plus object-replica for prompt-evidence packs and Annex IV artefacts; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 10 y after market placement (Art. 18) per the consuming-record schedule. |

### 5.19 Cross-System Integration — LMS competence handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-LMS-01 | H | R1 | Per-use-case approvers shall pass an LMS competence check (curriculum `HYDRA-APPROVER-<use_case>-v1.x`) before the gateway accepts a signed approval; LMS competence shall be re-checked at every approval submission; the competence currency status shall be logged in the gateway audit trail. |

## 6. Acceptance Criteria

1. CS, RA, IQ, OQ, PQ approved and executed (full Cat-5 set + per-use-case validation).
2. PQ shall include representative end-to-end coverage: PHI-redaction + hallucination-block + prompt-injection-defence + retrieval-grounding-evidence + watermark + vendor-version-pin + DR scenario + Art. 73 incident-reporting drill + EU AI Act high-risk-use-case path.
3. Art. 11 + Annex IV Technical Documentation packs on file for every high-risk use case.
4. Per-use-case EU AI Act classification gate exercise tested per URS-CLS-01..06.
5. VSR approved by VP AI / Data Science + VP QA + VP Legal + Privacy Officer + Conformity Assessment Coordinator.
6. RTM shall demonstrate every URS requirement mapped to at least one approved test case.
7. Vendor DPAs / BAAs on file and reviewed by Legal; vendor GPAI compliance evidence reviewed per URS-GPAI-01..04.

## 7. Constraints

- The gateway shall not enable auto-upgrade of vendor-LLM model versions.
- EU AI Act high-risk obligations apply per use case: **Annex I from 2 August 2027**; Annex III from 2 August 2026; Art. 50 transparency continuous.
- PHI / PII data shall not be sent to vendor LLMs without an executed DPA / BAA, documented residency clause, and (where transferred outside EEA) GDPR Art. 44 mechanism.
- The gateway shall not be used for use cases outside the approved Application Portfolio inventory.
- AI literacy obligation per Art. 4 applies from 2 February 2025; the gateway shall not provision access without literacy training evidence.

## 8. Assumptions

- Vendor LLMs (Anthropic, OpenAI) maintain their certifications and provide change-management notifications.
- API Gateway, Okta, GitLab, Splunk, HashiCorp Vault are themselves qualified.
- Legal has executed and maintains DPAs / BAAs with the vendor LLM providers and reviews them upon vendor-side material change.
- The Notified Body engaged for any underlying device-product context is consulted for Annex I conformity assessment.
- Swissmedic is the EU AI Act market-surveillance authority for CH-deployed contexts (or equivalent CH-specific regime as applicable).

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 — Electronic Records; Electronic Signatures (§§ .10, .30, .50, .70, .100, .200, .300).
- FDA *AI/ML-Based Software as a Medical Device Action Plan* (2021).
- FDA *Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions* (August 2025).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).

### EU — EMA / Commission
- EU GMP Annex 11 — Computerised Systems.
- EU GMP Annex 22 — Artificial Intelligence (DRAFT, consultation closed October 2025).
- EU AI Act 2024/1689 — Arts. 5 (prohibited practices), 8–21 (high-risk provider duties), 26 (deployer obligations), 27 (FRIA), 43 (conformity assessment), 47 (EU DoC), 48 (CE marking), 49 (EU database), 50 (transparency), 51–55 (GPAI), 72 (PMM), 73 (incident reporting 15 d / 10 d / 2 d), 99 (penalties €35M / €15M / €7.5M), 113 (timeline). **Annex I deadline: 2 August 2027. Annex III deadline: 2 August 2026. GPAI obligations: 2 August 2025. AI literacy: 2 February 2025.**
- EMA *Reflection Paper on the use of AI in the Medicinal Product Lifecycle* (2024).
- GDPR (Regulation (EU) 2016/679) — Articles 6, 9, 22, 32, 35, 44.

### DACH-specific
- Swissmedic (CH) — guidance on use of AI in regulated medicinal contexts; CH AI-Act-equivalent regime where applicable.
- BfArM (DE) — AI guidance for medicinal products; EU AI Act market-surveillance authority for DE.
- AGES (AT) — Österreichische Agentur für Gesundheit und Ernährungssicherheit.

### International — ICH / ISPE / ISO / NIST / OWASP
- ICH Q9(R1) — Quality Risk Management.
- ISPE GAMP 5 (2nd Edition, 2022); ISPE GAMP GPG *AI/ML in GxP* (2024).
- PIC/S PI 041 — Good Practices for Data Management and Integrity.
- ISO/IEC 42001:2023 — AI Management System.
- ISO/IEC 23894:2023 — AI Risk Management.
- ISO/IEC 27001:2022 — Information Security Management Systems.
- NIST AI Risk Management Framework 1.0 (NIST AI 100-1, 2023).
- NIST AI 600-1 — Generative AI Profile (July 2024).
- OWASP Top 10 for LLM Applications (2024).

### Vendor
- Anthropic Claude API + Trust Center (DPA + GPAI documentation).
- OpenAI GPT API + Trust Center (DPA + GPAI documentation).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
