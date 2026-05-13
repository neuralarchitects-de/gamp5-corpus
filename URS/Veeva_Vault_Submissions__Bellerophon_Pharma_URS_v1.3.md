---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-27; enriched 2026-05-12 (T4 uplift per METHODOLOGY § 2A.13)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed.) Cat 4 SaaS conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "ICH M2 ESTRI; ICH M4 (CTD); ICH M8 (eCTD); FDA eCTD Technical Conformance Guide"
  - "EMA eCTD v4.0 (ICH M8 v4) + EU IG; EMA Common Repository / CESP"
  - "PMDA eCTD Module 1 (JP-specific) + PMDA Gateway"
  - "Health Canada eCTD + CESG"
  - "IDMP ISO 11238 / 11239 / 11240 / 11615 / 11616; EMA SPOR"
  - "FDA ESG with SHA-256 receipt; MHRA Submissions (post-Brexit); ANVISA (BR); NMPA (CN); Swissmedic"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Regulatory Submissions Platform — Veeva Vault Submissions + Submissions Publishing 24R3

**Document Number:** BLR-URS-VSUB-001 | **Version:** 1.0 | **Effective Date:** 2026-04-27 *(synthetic)*
**Site:** Bellerophon Pharma plc, Global Regulatory Affairs, London HQ + regional regulatory hubs in Basel (CH), München (DE), Wien (AT), Tokyo (JP), São Paulo (BR), Shanghai (CN) *(fictional)*
**System Owner:** Director, Regulatory Operations
**Process Owner:** VP Global Regulatory Affairs
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Project Mode:** Configuration project on commercial software product **Veeva Vault Submissions + Submissions Publishing 24R3** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; ICH M2 (ESTRI); ICH M4 (CTD); ICH M8 (eCTD); FDA eCTD + ESG; EMA eCTD v4 + CESP / Common Repository; PMDA Gateway; Health Canada CESG; MHRA UK post-Brexit submissions; ANVISA (BR); NMPA (CN); Swissmedic; IDMP ISO 11238/11239/11240/11615/11616; EMA SPOR.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Regulatory Operations) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Vendor Assurance — Veeva owner) | _____________ | _____________ | _____ |
| Reviewer (Publishing Manager) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs Lead — Asia) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs Lead — DACH) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs Lead — LATAM) | _____________ | _____________ | _____ |
| Reviewer (IDMP / xEVMPD Steward) | _____________ | _____________ | _____ |
| Reviewer (Translation Manager) | _____________ | _____________ | _____ |
| Approver (VP Global Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | T4 enrichment per METHODOLOGY § 2A.13 (150–250 reqs): broken § 5 into 15 sub-sections; Submission Planning (§ 5.2); Document Selection + Reuse (§ 5.3); eCTD Build per ICH M8 + region-specific Module 1 (§ 5.4); Validation engine LORENZ docuBridge + eValidator (§ 5.5); Cross-reference + Sequence Number Mgmt (§ 5.6); Granularity (per-file vs per-section) (§ 5.7); Style / Format Compliance (§ 5.8); Sequence Differencing + Archive Retrieval (§ 5.9); Gateway routing FDA ESG + EMA CESP + PMDA + CESG (§ 5.10); IDMP / xEVMPD product master (§ 5.11); Brexit MHRA / ANVISA / NMPA / Swissmedic + DACH variants (§ 5.12); Translation Mgmt (§ 5.13); Multi-country variation submission (§ 5.14); 21 CFR Part 11 sub-section-explicit; FDA CSA Feb 2026 alignment; ICH M2 ESTRI explicit. |

## Definitions

| Term | Definition |
|---|---|
| Submissions | Veeva Vault Submissions (content + planning) |
| Submissions Publishing | Veeva Vault Submissions Publishing (eCTD compile / validate / publish) |
| Submissions Archive | Veeva Vault Submissions Archive (long-term sequence-archive) |
| eCTD | Electronic Common Technical Document per ICH M8 |
| CTD | Common Technical Document per ICH M4 |
| Sequence | A submission sequence (initial / amendment / variation / supplement) per agency |
| Module 1 | Regional administrative information (per-agency: FDA M1, EU M1, JP M1, CA M1) |
| Modules 2–5 | Common-quality / nonclinical / clinical content (CTD core, shared across regions) |
| FDA ESG | FDA Electronic Submissions Gateway (US receipt) |
| EMA CESP | Common European Submission Portal (EU eCTD upload) |
| EMA Common Repository | EMA's electronic submission ingestion service |
| PMDA Gateway | Japanese PMDA submission gateway |
| Health Canada CESG | Common Electronic Submissions Gateway (CA) |
| MHRA | Medicines and Healthcare products Regulatory Agency (UK post-Brexit) |
| ANVISA | Agência Nacional de Vigilância Sanitária (BR) |
| NMPA | National Medical Products Administration (CN) |
| eValidator | LORENZ eValidator (industry-standard eCTD validation tool) |
| docuBridge | LORENZ docuBridge (eCTD viewer + sequence-differencing tool) |
| Granularity | The smallest unit of content versioned in the eCTD (file vs section) |
| IDMP | Identification of Medicinal Products (ISO 11238 et al.) |
| xEVMPD | extended EudraVigilance Medicinal Product Dictionary |
| SPOR | EMA Substances, Products, Organisations, Referentials |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the regulatory-submissions platform used to plan, author, compile, validate, publish, and submit eCTD sequences to global health authorities (FDA, EMA, PMDA, Health Canada, MHRA, Swissmedic, ANVISA, NMPA) for Bellerophon's products, with multi-country variation, IDMP-aligned product master, translation management, and submission-archive retrieval.

## 2. Scope

**In scope:** Veeva Vault Submissions + Submissions Publishing 24R3 + Submissions Archive multi-tenant SaaS; per-product configuration; SSO via Okta SAML 2.0 + MFA; integrations with Vault QualityDocs (controlled-document linkage), Vault PromoMats (where applicable), Vault RIM (Regulatory Information Management), Vault eTMF, the Sirius PV system (Argus) for periodic-safety-update content, EMA SPOR for IDMP reference, the FDA ESG / EMA CESP / PMDA / Health Canada CESG / MHRA / Swissmedic / ANVISA / NMPA gateways, the LORENZ eValidator + docuBridge utilities, and the translation-management vendor service.

**Out of scope:** vendor infrastructure (Veeva-managed); commercial promotional content (separate URS for PromoMats); the chemistry / quality data sources (CMC documentation in Vault QualityDocs is upstream, the submissions platform consumes finalized documents only); analytical lab systems (separate URSs).

## 3. System Description

The platform is the system of record for regulatory-submissions content + planning + sequence compilation. Per-product structure follows ICH M4 (CTD) and ICH M8 (eCTD); content is checked-out / -in / approved with electronic signatures; sequences are compiled, validated against agency-specific eCTD validation criteria using LORENZ eValidator, region-specific Module 1 wrapped per agency, and submitted via the appropriate gateway with ack reconciliation. Multi-country variation submissions are orchestrated from a single planning master. Translation management routes regional Module 1 artefacts through the translation-vendor pipeline. Submissions Archive provides long-term sequence-archive retrieval and sequence differencing.

GAMP Cat 4: Veeva maintains the SDLC and customer-shared CSV evidence; site validates per-product configuration, validation-rule profiles per agency, integration boundaries, and 21 CFR Part 11 controls.

## 4. User Roles

| Role | Permissions | SoD constraint |
|---|---|---|
| Document Author | Create / edit content; cannot approve. | ≠ Approver |
| Reviewer | Review; cannot approve. | ≠ Approver |
| Approver | Approve content; SoD-enforced. | ≠ Author / Reviewer of same document |
| Submissions Planner | Plan sequences; cannot publish. | ≠ Publisher |
| Submissions Publisher | Compile + validate + publish sequences; cannot author content. | ≠ Author |
| Submissions Approver | Approve sequence release to gateway. | ≠ Publisher of same sequence |
| Gateway Operator | Submit + reconcile acks. | ≠ Submissions Approver |
| Translation Manager | Manage translation packages; cannot approve content. | ≠ Approver |
| IDMP / xEVMPD Steward | Maintain product master + SPOR linkage; cannot approve. | ≠ Approver |
| Vault Administrator | Configure; cannot approve. | ≠ Approver, ≠ Publisher |
| Regional Affairs Lead | Region-specific approvals (e.g., DACH lead approves EU + DE + CH + AT variants). | Per-region scope |
| Auditor | Read-only. | Read-only |

Standard SoD across roles; agency-specific role separations as required.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` direct GxP impact / `R2` indirect / `R3` none), and a verifiable `shall`-clause.

### 5.1 Vendor Assurance + Configuration Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-01 | H | R1 | Veeva shall be qualified as a critical SaaS vendor with SOC 2 Type II, ISO 27001, ISO 27017, customer-shared CSV evidence, DPA, BAA; re-qualified annually. |
| URS-VND-02 | H | R1 | Vendor releases (24R1, 24R2, 24R3, 25R1, ...) shall be impact-assessed within 14 days of release notes; configuration-affecting changes shall trigger re-validation. |
| URS-VND-03 | M | R2 | Annual Veeva TR-Audit summary shall be filed in Vendor Assurance dossier. |
| URS-CFG-01 | H | R1 | Per-product configuration (CTD-section binding, region-specific Module 1 templates, validation profiles per agency, granularity policy, signature templates) shall follow DRAFT → QC → UAT → PRODUCTION; SoD-enforced sign-off. |
| URS-CFG-02 | H | R1 | Configuration export shall produce version-stamped artefacts for inspection. |
| URS-CFG-03 | M | R2 | Configuration-change runbook shall mandate regression-test pack execution before PROD promotion. |

### 5.2 Submission Planning

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAN-01 | H | R1 | Submission planning shall be supported for product lifecycle artefacts: IND, NDA, BLA, ANDA, MAA, CTA, variation (Type IA / IB / II / III for EU; supplements for US), renewal, withdrawal. |
| URS-PLAN-02 | H | R1 | Multi-country submission planning shall produce a single planning master that drives per-region sequence builds; per-region targets shall be configurable. |
| URS-PLAN-03 | H | R1 | Submission-plan milestones (target submission date, agency interaction date, expected response date) shall be tracked with alerts on at-risk milestones. |
| URS-PLAN-04 | M | R2 | Resource estimation per submission (author / reviewer / publisher hours) shall be supported for capacity planning. |

### 5.3 Document Selection and Reuse

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DOC-01 | H | R1 | Documents shall be selected from Vault QualityDocs by product / CTD section / version-of-record; selected documents shall be locked at selection for the sequence build. |
| URS-DOC-02 | H | R1 | Document reuse across sequences shall be supported with cross-reference tracking; reused-document version-of-record shall be unambiguous. |
| URS-DOC-03 | H | R1 | Document lifecycle binding shall enforce CTD-section validity (e.g., a Module 3.2.S document cannot be assigned to Module 5.3.5.1). |
| URS-DOC-04 | M | R2 | Document-reuse impact analysis shall flag downstream sequences when a reused document changes. |

### 5.4 eCTD Build per ICH M8 + Region-Specific Module 1

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ECTD-01 | H | R1 | Sequence builds shall produce eCTD-compliant content per ICH M8 v3.2.2 (current effective) or ICH M8 v4.0 (EU) per agency profile. |
| URS-ECTD-02 | H | R1 | Module 1 region-specific templates shall be supported: FDA M1 (US-specific structure), EU M1 (EU IG v3.0+), JP M1 (PMDA-specific), CA M1 (Health Canada), MHRA UK M1 (post-Brexit), Swissmedic CH M1, ANVISA BR M1, NMPA CN M1. |
| URS-ECTD-03 | H | R1 | Modules 2–5 (CTD core: Quality, Nonclinical, Clinical) shall be shared content across regions with region-specific cross-references via ICH M8 leaf elements. |
| URS-ECTD-04 | H | R1 | Sequence build shall enforce structural validity (DTD / XSD per agency) at compile time; non-conforming sequences shall not pass. |
| URS-ECTD-05 | H | R1 | Lifecycle operations on leaf documents (new, append, replace, delete) shall be supported per ICH M8; operations audit-trailed at leaf level. |
| URS-ECTD-06 | M | R2 | eCTD index file generation shall be deterministic across rebuilds of the same content set. |

### 5.5 Validation Engine (LORENZ eValidator)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VAL-01 | H | R1 | Pre-submission validation shall execute LORENZ eValidator with agency-specific validation criteria packs (FDA, EMA, PMDA, HC, MHRA, Swissmedic, ANVISA, NMPA). |
| URS-VAL-02 | H | R1 | Validation errors shall be classified per agency severity (Error / Warning / Info); errors shall block submission; warnings shall require justification at publisher approval. |
| URS-VAL-03 | H | R1 | LORENZ docuBridge shall be available for sequence preview + sequence differencing pre-submission. |
| URS-VAL-04 | H | R1 | Validation-criteria-pack version shall be stamped on each validation run; criteria-pack updates shall be tracked under change control. |
| URS-VAL-05 | M | R2 | Validation reports shall be archived per sequence for inspection. |

### 5.6 Cross-Reference and Sequence Number Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEQ-01 | H | R1 | Sequence numbers shall be auto-incremented per submission (0000 initial, 0001 amendment, 0002 variation, etc.); numbering shall be agency-specific and gap-free per application. |
| URS-SEQ-02 | H | R1 | Cross-references between leaves (e.g., Module 5 to Module 3) shall be maintained with `xlink:href` per ICH M8 and validated at compile. |
| URS-SEQ-03 | H | R1 | Sequence release shall require Submissions Approver re-authenticated electronic signature. |
| URS-SEQ-04 | H | R1 | Lifecycle operations (replace / append / delete) shall be audit-trailed at the leaf-document level with previous-leaf reference. |
| URS-SEQ-05 | M | R2 | Sequence number conflicts (e.g., parallel submissions) shall be detected and resolved by Submissions Manager. |

### 5.7 Granularity Policy

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-GRAN-01 | H | R1 | The granularity policy (per-file vs per-section) shall be configurable per CTD module; recommended FDA / EMA granularity shall be defaults. |
| URS-GRAN-02 | H | R1 | Granularity at section level shall be enforced (Module 3 typically per-section; Module 5 typically per-study); deviations shall be exception-tracked. |
| URS-GRAN-03 | M | R2 | Granularity changes shall be impact-assessed on existing sequences. |

### 5.8 Style and Format Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-STYLE-01 | H | R1 | PDF rendering shall comply with PDF/A-1b (or PDF/A-2 per agency) per ICH M2 ESTRI; bookmarks and hyperlinks shall be preserved. |
| URS-STYLE-02 | H | R1 | Document style guides per region (FDA stylesheet, EMA stylesheet, JP stylesheet) shall be available and applied. |
| URS-STYLE-03 | H | R1 | File-naming conventions per agency (FDA stf-naming, EMA IG-naming, JP-naming) shall be enforced. |
| URS-STYLE-04 | M | R2 | Format-compliance pre-check before validation shall surface common defects (broken hyperlinks, oversized fonts, missing bookmarks). |

### 5.9 Sequence Differencing, Archive, and Retrieval

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DIFF-01 | H | R1 | Sequence-to-sequence diff (e.g., 0001 vs 0002) shall be supported via LORENZ docuBridge with leaf-level change-tracking. |
| URS-DIFF-02 | H | R1 | Submissions Archive shall hold all submitted sequences with regulator acks per submission. |
| URS-DIFF-03 | H | R1 | Archive retrieval shall be ≤ 4 h during regulatory inspections; documented retrieval runbook. |
| URS-DIFF-04 | M | R2 | Archive sequence-index export shall be available in eCTD-viewer-compatible format. |

### 5.10 Gateway Submission and Routing

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-GW-01 | H | R1 | Submission to FDA ESG shall use SHA-256 receipt protocol; ack messages (transport + business) reconciled to sequence. |
| URS-GW-02 | H | R1 | Submission to EMA shall use CESP (Common European Submission Portal) or EMA Common Repository per IG; ack messages reconciled. |
| URS-GW-03 | H | R1 | Submission to PMDA Gateway shall use the JP-specific gateway protocol; ack messages reconciled. |
| URS-GW-04 | H | R1 | Submission to Health Canada CESG shall use the AS2 / WebTrader protocol; ack messages reconciled. |
| URS-GW-05 | H | R1 | Submission to MHRA (UK post-Brexit) shall use the MHRA Submissions interface; UK Module 1 wrapped. |
| URS-GW-06 | H | R1 | Submission to Swissmedic shall use the Swissmedic eGov platform; CH Module 1 wrapped. |
| URS-GW-07 | H | R1 | Submission to ANVISA (BR) shall use the ANVISA eCTD interface; BR Module 1 wrapped. |
| URS-GW-08 | H | R1 | Submission to NMPA (CN) shall use the NMPA eCTD per the China-specific requirements; CN Module 1 wrapped. |
| URS-GW-09 | H | R1 | Negative ack (validation rejection by agency) shall open an Exception requiring corrected resubmission within agency grace period. |
| URS-GW-10 | M | R2 | Gateway connectivity tests shall be performed quarterly per gateway. |
| URS-GW-11 | M | R2 | Gateway maintenance windows per agency shall be configurable; submission scheduler shall avoid windows. |

### 5.11 IDMP / xEVMPD Integration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-IDMP-01 | H | R1 | The product master shall hold IDMP identifiers per ISO 11238 (substance), ISO 11239 (dose form / unit), ISO 11240 (units of measure), ISO 11615 (medicinal product), ISO 11616 (pharmaceutical product); identifiers reconciled against EMA SPOR. |
| URS-IDMP-02 | H | R1 | IDMP-aligned submission metadata shall be auto-populated in EU Module 1 + xEVMPD submissions. |
| URS-IDMP-03 | H | R1 | xEVMPD submissions to EMA (XEVPRM transactions) shall be supported with ack reconciliation. |
| URS-IDMP-04 | H | R1 | IDMP referential drift (e.g., SPOR substance update) shall be detected by a quarterly reconciliation job; impact assessment opened for in-scope products. |

### 5.12 Multi-Region Variants (Brexit MHRA, ANVISA, NMPA, Swissmedic, DACH)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REGION-MHRA-01 | H | R1 | UK MHRA post-Brexit submissions shall be supported; UK-specific Module 1 (per UK IG) shall be wrapped over shared Modules 2-5. |
| URS-REGION-MHRA-02 | M | R2 | Northern Ireland Protocol-related dual-marketing (EU + UK) shall be supported per current MHRA guidance. |
| URS-REGION-SWISS-01 | H | R1 | Swissmedic submissions shall be supported with CH-specific Module 1 + DACH-language-appropriate labels (de-CH, fr-CH, it-CH). |
| URS-REGION-ANVISA-01 | H | R1 | ANVISA (BR) submissions shall be supported with BR-specific Module 1; pt-BR translation required for labelling artefacts. |
| URS-REGION-NMPA-01 | H | R1 | NMPA (CN) submissions shall be supported with CN-specific Module 1 + zh-CN translation requirements; CN-specific stability + manufacturing data requirements addressed. |
| URS-REGION-DACH-01 | H | R1 | EU-DACH variants (de-DE for DE marketing authorisation under EU MAA; de-AT for AT national submissions where applicable; de-CH for CH) shall be supported with consistent core data + region-specific labelling. |
| URS-REGION-LANG-01 | M | R2 | Region-language matrix shall be configurable per product per region. |

### 5.13 Translation Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRANS-01 | H | R1 | Translation packages shall be created per submission per region; source-language artefacts shall be linked to translated artefacts via translation-job-id. |
| URS-TRANS-02 | H | R1 | Translation lifecycle shall be DRAFT → TRANSLATION → REVIEW → APPROVED → SUBMITTED; translation-vendor integration shall handle hand-off + return. |
| URS-TRANS-03 | H | R1 | Translation versioning shall preserve source-to-target alignment; source updates shall flag translation drift. |
| URS-TRANS-04 | M | R2 | Translation memory + glossary shall be supported for consistency across products. |
| URS-TRANS-05 | M | R2 | Local-medical-reviewer sign-off shall be supported for region-specific labelling. |

### 5.14 Multi-Country Variation Submission

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VAR-01 | H | R1 | A single variation master (e.g., manufacturing-site change) shall be deployable across multiple agency submissions in parallel with per-region timing controls. |
| URS-VAR-02 | H | R1 | Variation classification shall align with EU Type IA / IB / II / III + FDA supplements + JP / CA variation categories per regulation. |
| URS-VAR-03 | H | R1 | Variation tracking dashboard shall surface per-agency status across the variation lifecycle. |
| URS-VAR-04 | M | R2 | Conditional variations (e.g., approval-pending) shall be tracked with downstream-submission dependencies. |

### 5.15 Audit Trail / 21 CFR Part 11 (sub-section-explicit)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Audit trail shall capture document edits, signatures, sequence-build events, validation events, submission events, ack reconciliations, archive retrieval. |
| URS-AUD-02 | H | R1 | Audit trail append-only at the database level; vendor controls documented in customer-shared CSV. |
| URS-AUD-03 | H | R1 | Audit-trail review monthly (Submissions Manager) + quarterly (QA). |
| URS-AUD-04 | H | R1 | Retention: ≥ life of product + jurisdictional minimum (US ≥ 2 y post-approval; EU ≥ 10 y post-last-marketed; JP ≥ 15 y post-discontinuation). |
| URS-PART11-01 | H | R1 | Per § 11.10(a), procedural-control SOPs reviewed annually. |
| URS-PART11-02 | H | R1 | Per § 11.10(b), accurate + complete copies generation verified. |
| URS-PART11-03 | H | R1 | Per § 11.10(c), records protected throughout retention. |
| URS-PART11-04 | H | R1 | Per § 11.10(d), access via Okta SAML 2.0 + MFA. |
| URS-PART11-05 | H | R1 | Per § 11.10(e), operational audit trail per § 5.15. |
| URS-PART11-06 | H | R1 | Per § 11.10(g), authority checks at workflow / API layer. |
| URS-PART11-07 | H | R1 | Per § 11.10(k), operation-manual change control. |
| URS-PART11-08 | H | R1 | Per § 11.50, signature events render printed name + date/time + meaning. |
| URS-PART11-09 | H | R1 | Per § 11.70, signatures cryptographically bound to document state. |
| URS-PART11-10 | H | R1 | Per § 11.100, signature uniqueness; user-ids never reassigned. |
| URS-PART11-11 | H | R1 | Per § 11.200, re-authentication at every signature event (content approval, sequence release, gateway submission). |
| URS-PART11-12 | H | R1 | Per § 11.300, password / credential controls per site InfoSec policy. |

### 5.16 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-VAULT-01 | H | R1 | Vault QualityDocs URN resolution for controlled-document references. |
| URS-INT-VAULT-02 | H | R1 | Vault RIM (Regulatory Information Management) for product / authorisation master and lifecycle. |
| URS-INT-VAULT-03 | M | R2 | Vault eTMF cross-reference where TMF documents inform regulatory submission. |
| URS-INT-VAULT-04 | M | R2 | Vault PromoMats where applicable (regulator-affirmed promotional content). |
| URS-INT-VIG-01 | H | R1 | Periodic safety-update content (PSUR / PBRER / PADER / DSUR) sourced from Sirius PV (Argus). |
| URS-INT-SPOR-01 | H | R1 | EMA SPOR integration for IDMP reference data. |
| URS-INT-EVAL-01 | H | R1 | LORENZ eValidator integration for pre-submission validation. |
| URS-INT-DOCB-01 | H | R1 | LORENZ docuBridge integration for sequence preview + diff. |
| URS-INT-TRANS-01 | H | R1 | Translation-vendor service integration for translation lifecycle. |
| URS-INT-SSO-01 | H | R1 | Okta SAML 2.0 + MFA. |

### 5.17 Data Integrity / Performance / Availability / Backup / Security / Training / Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | **Attributable:** records attributable to a named user. |
| URS-DI-02 | H | R1 | **Legible:** PDF/A-1b / PDF/A-2 rendering verified. |
| URS-DI-03 | H | R1 | **Contemporaneous:** server-side NTP-synced timestamps. |
| URS-DI-04 | H | R1 | **Original:** source preserved; corrections recorded as new versions. |
| URS-DI-05 | H | R1 | **Accurate:** sequence-build calculations deterministic; OQ-verified. |
| URS-DI-06 | H | R1 | **Complete / Consistent / Enduring / Available:** records meet retention obligations. |
| URS-PERF-01 | M | R2 | Sequence compile P95 ≤ 30 min for a 5,000-document sequence. |
| URS-PERF-02 | M | R2 | eValidator P95 ≤ 15 min per sequence. |
| URS-PERF-03 | M | R2 | Archive retrieval P95 ≤ 4 h. |
| URS-AV-01 | H | R1 | Availability per Veeva SLA (≥ 99.7%). |
| URS-AV-02 | H | R1 | RPO / RTO per Veeva SLA verified annually. |
| URS-BAK-01 | H | R1 | Vendor-managed backup; site verifies vendor RPO / RTO annually. |
| URS-BAK-02 | M | R2 | Quarterly site tenant-data export with ≥ 10-year retention. |
| URS-SEC-01 | H | R1 | Per-product / per-agency / per-region access. |
| URS-SEC-02 | H | R1 | TLS 1.3 in transit; AES-256 at rest. |
| URS-SEC-03 | M | R2 | Annual penetration test; high/critical findings remediated within 60 days. |
| URS-TRN-01 | H | R1 | LMS-recorded role-specific training; agency-specific competency for publishers. |
| URS-TRN-02 | M | R2 | Annual refresher covering FDA / EMA / PMDA / HC / MHRA / ANVISA / NMPA guidance updates. |
| URS-PR-01 | H | R1 | Annual periodic review covering: vendor qualification, configuration drift, validation-pack version status, gateway connectivity tests, archive retrieval rehearsal, IDMP / SPOR reconciliation, translation-vendor performance, deviation summary, training currency; signed by Director Regulatory Operations + VP QA + VP Global Reg Affairs. |

### 5.18 Inspection Readiness and Health-Authority Correspondence

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INSP-01 | H | R1 | Inspection-readiness export per submission shall produce a complete dossier (sequence content + validation report + ack messages + signature evidence + audit-trail extract) within ≤ 4 h of request. |
| URS-INSP-02 | H | R1 | Health-authority correspondence (FDA Information Request, EMA Day-120 / Day-180 questions, PMDA queries, Health-authority follow-ups) shall be tracked in a structured register with due-date, response-due-date, status, and per-question sub-tracking. |
| URS-INSP-03 | H | R1 | CA-query response workflow shall enforce SoD (drafter ≠ reviewer ≠ Submissions Approver); responses shall be exportable in inspection-ready PDF/A-3. |
| URS-INSP-04 | M | R2 | Pre-inspection mock-audit rehearsal workflow shall capture findings + remediation tracking. |

### 5.19 Pre-IND / Pre-Submission Meetings

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MEET-01 | H | R1 | Pre-IND / Type-B / Type-C / Pre-NDA / EMA scientific-advice / PMDA-consultation meetings shall be tracked with meeting requests, briefing-document submissions, meeting minutes, agency feedback. |
| URS-MEET-02 | H | R1 | Briefing-document submission shall use the relevant agency template and be eCTD-compiled where applicable. |
| URS-MEET-03 | M | R2 | Meeting-feedback shall feed downstream submission planning. |

### 5.20 Application Lifecycle Tracking

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LIFE-01 | H | R1 | Per application (IND / NDA / BLA / MAA / CTA), the full lifecycle (initial submission, amendments, supplements, variations, renewal, withdrawal) shall be tracked with sequence-by-sequence audit. |
| URS-LIFE-02 | H | R1 | Application status (active / under-review / approved / withdrawn / lapsed) shall be reflected per agency. |
| URS-LIFE-03 | H | R1 | Approval letters + EPAR + label-of-record shall be archived per application per agency. |
| URS-LIFE-04 | M | R2 | Lifecycle milestone alerts (PDUFA date, EMA CHMP opinion date, MAA renewal due) shall be configured. |

### 5.21 SPL (Structured Product Labeling) Generation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SPL-01 | H | R1 | FDA SPL (Structured Product Labeling) generation shall be supported for US labelling submissions per 21 CFR 314.81; SPL XML output validated against HL7 SPL schema. |
| URS-SPL-02 | H | R1 | SPL versioning shall preserve effective-time + version-number sequencing. |
| URS-SPL-03 | M | R2 | SPL drug-listing + establishment-registration submissions to FDA per 21 CFR Part 207 shall be tracked. |

### 5.22 Document Reuse Across Applications (Reference Model)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REF-01 | H | R1 | Documents referenced across multiple applications (e.g., a Drug Master File referenced by multiple NDA / ANDA) shall be tracked with reference-letter management. |
| URS-REF-02 | H | R1 | Letter-of-Authorization (LoA) for cross-reference shall be tracked with effective dates and revocation events. |
| URS-REF-03 | M | R2 | DMF status (Type II / Type III / etc.) + adequacy status shall be tracked. |

### 5.23 Real-World-Data Submissions

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RWD-01 | M | R2 | Real-World Evidence (RWE) submissions per FDA 21st Century Cures Act Sec. 3022 + EMA RWE strategy shall be supported via SDTM / ADaM / SEND data packages. |
| URS-RWD-02 | M | R2 | Patient-experience-data submissions per FDA Patient-Focused Drug Development guidance shall be supported. |

### 5.24 Submissions Dashboard and Metrics

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DASH-01 | H | R1 | Submissions dashboard shall surface per-product per-agency status (in-progress / submitted / under-review / approved / responses-due); refresh latency ≤ 15 min. |
| URS-DASH-02 | M | R2 | Per-publisher KPIs (sequences-published, validation-error-rate, on-time submission rate) shall be reported. |
| URS-DASH-03 | M | R2 | Compile-time + validation-time + submission-time histograms per sequence-size shall be available for capacity planning. |

### 5.25 Combination-Product Specific Submissions

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-COMBO-01 | H | R1 | Combination-product (drug-device, drug-biologic) submissions shall route to the appropriate FDA Center (CDER / CBER / CDRH) per the Office of Combination Products (OCP) assignment; dual-Center coordination supported. |
| URS-COMBO-02 | M | R2 | Combination-product Module 3 (CMC) + Module 5 (device-specific clinical) integration shall be supported. |

### 5.26 Submission-Type Specific Validation Profiles

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PROF-VAL-01 | H | R1 | Validation profile shall be selectable per submission type (IND / NDA / ANDA / BLA / MAA / CTA / variation / supplement); each profile pins the LORENZ criteria set + agency-rules. |
| URS-PROF-VAL-02 | M | R2 | Per-submission-type profile updates shall be tracked under change control; impact on open submissions assessed. |

### 5.27 Bookmarks, Hyperlinks, and PDF Quality Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PDF-01 | H | R1 | All submitted PDFs shall have agency-required bookmarks for headings, tables, and figures per FDA Portable Document Format (PDF) Specifications. |
| URS-PDF-02 | H | R1 | Internal hyperlinks (table-of-contents, in-section navigation) shall be valid; broken-link check at compile. |
| URS-PDF-03 | M | R2 | Font embedding shall be enforced (all fonts subsetted + embedded); compile rejects non-compliant PDFs. |
| URS-PDF-04 | M | R2 | PDF security settings shall not impose restrictions that prevent regulator processing (no password, no copy-restriction). |

### 5.28 Multi-Region Cover Letter and Form Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-COVER-01 | H | R1 | Per-region cover letter templates shall be maintained (FDA Form 356h cover letter, EMA cover letter, PMDA cover letter, etc.). |
| URS-COVER-02 | H | R1 | Form generation shall be supported per region (FDA Form 356h, FDA Form 1571 for INDs, FDA Form 2253 for promotional, EU CESP submission form). |
| URS-COVER-03 | M | R2 | Cover-letter version-control shall track template + per-submission instance separately. |

### 5.29 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is SAML 2.0 via Entra ID with SCIM lifecycle provisioning; conditional-access policy `Regulatory-App Conditional Access (FIDO2 phishing-resistant MFA)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the metadata DB plus object-replica for the submission binder; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ Product-lifetime + 25 y per the consuming-record schedule. |

### 5.30 Cross-System Integration — Hydra regulatory drafting + Helios

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HYD-01 | H | R1 | GenAI-assisted regulatory-text drafting (e.g., Module 2 summaries, Module 3 quality narratives, response-to-information drafting) shall be invoked exclusively via the Hydra GenAI Gateway (`HYD2-URS-GENAI-001`); direct vendor-LLM calls from the Vault tenant shall be prohibited at the egress firewall. |
| URS-XINT-HYD-02 | H | R1 | Each regulatory-drafting use case shall pass the Hydra per-use-case classification gate; regulatory-text drafting that influences a regulatory dossier shall be declared EU AI Act Annex I high-risk (2027 deadline) with a signed Art. 11 + Annex IV pack delivered to the competent authority on inspection request. |
| URS-XINT-HYD-03 | H | R1 | Every Hydra-mediated draft inserted into a submission binder shall carry a content provenance watermark (Hydra URS-WATERMARK-*) and the served `model_version`, retrieval context hash, and HITL approver identity; Reg Affairs Lead approval shall be required before binder finalisation. |
| URS-XINT-HYD-04 | H | R1 | Watermark stripping or content modification post-HITL shall be technically detectable and shall raise a deviation in `TLB-URS-EQMS-001`. |
| URS-XINT-HYD-05 | H | R1 | Inference events shall be forwarded to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract within 5 minutes. |

### 5.31 Cross-System Integration — Helios audit-trail handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HEL-01 | H | R1 | Vault Submissions shall publish audit-trail events (Submission binder lifecycle, content authoring, e-signature, and submission-transmission events) to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract (JSON Lines, schema-registry pinned, Kafka topic `helios.ingest.bellerophon.submissions.v1`) within 5 minutes of event capture; 21 CFR § 11.10(e) audit-trail completeness shall be preserved end-to-end so that no event class is lost at the boundary. |
| URS-XINT-HEL-02 | H | R1 | Pre-handover audit-trail retention on the Vault Submissions side shall be for the product lifetime + 25 y regardless of Helios availability; once Helios acknowledges ingest (per-message ack with idempotency key), Helios is the system-of-record for review and the Vault Submissions local copy serves as the durability backstop until the local retention floor expires. |

### 5.32 Cross-System Integration — EDMS handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-EDMS-01 | H | R1 | The Vault Submissions tenant shall retrieve controlled regulatory artefacts (Module 1 forms, Module 3 templates, prior approved labelling) from the EDMS (`VLP-URS-EDMS-001`) via the EDMS read API with read-only pinning to the artefact's EFFECTIVE version at the time of retrieval; retrieved artefact + version pin shall be persisted with the submission binder. |

## 6. Acceptance Criteria

CS, RA, IQ (vendor-shared), OQ (lifecycle / signature / compile / validation / submission / audit / archive), PQ (representative end-to-end including IND + amendment + variation + multi-country variation through ack reconciliation across ≥ 3 agencies + archive retrieval + sequence diff); VSR approved by Director Regulatory Operations + VP Global Reg Affairs + VP QA; RTM maps every URS-ID to ≥ 1 approved test case.

## 7. Constraints

- Vendor releases not under site change control but evaluated before promotion.
- Per-agency validation-criteria packs maintained by LORENZ; site applies through Veeva integration.
- IDMP / SPOR reference data is authoritative external.

## 8. Assumptions

- Vault QualityDocs, Vault RIM, Vault eTMF, Vault PromoMats, Sirius PV (Argus), Okta, agency gateways operational and validated.
- LORENZ eValidator + docuBridge subscriptions current.
- Translation vendor qualified per site Vendor Assurance.

## 9. References

### US

- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- FDA *eCTD Technical Conformance Guide* (current revision).
- FDA *Providing Regulatory Submissions in Electronic Format — Certain Human Pharmaceutical Product Applications and Related Submissions Using the eCTD Specifications* (Guidance).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).
- FDA ESG (Electronic Submissions Gateway) Specifications.

### EU

- EMA eCTD EU Implementation Guide (current revision).
- EMA Common Repository / CESP specifications.
- EMA SPOR data services.
- EU Reg. 1234/2008 + Reg. 712/2012 (variation classifications: Type IA / IB / II / III).

### International

- ICH M2 — Electronic Standards for the Transfer of Regulatory Information (ESTRI).
- ICH M4 — Common Technical Document (CTD) — M4Q (Quality), M4S (Safety), M4E (Efficacy).
- ICH M8 — eCTD v3.2.2 / v4.0.
- ISO 11238, 11239, 11240, 11615, 11616 — IDMP.

### Regional

- PMDA — *Regulatory Submission Guideline for Pharmaceuticals* + PMDA Gateway specs (JP).
- Health Canada — CESG Specifications (CA).
- MHRA — UK Submissions Guidelines (post-Brexit, January 2021+).
- Swissmedic — eGov platform specifications (CH).
- ANVISA — *Regulamento para Submissão Eletrônica* (BR).
- NMPA — *eCTD Implementation Guide* (CN).

### DACH-specific competent authorities

- BfArM (DE) Bundesinstitut für Arzneimittel und Medizinprodukte — national approvals + central-procedure DE-leg.
- Paul-Ehrlich-Institut (DE) — biological-product authorisations.
- Swissmedic (CH) — HMG + AMZV.
- AGES PharmMed (AT) — national approvals.

### Industry

- ISPE GAMP 5 (2nd Edition, 2022); PIC/S PI 041.
- ISO/IEC 27001:2022 — Information Security Management Systems.
- LORENZ — *eValidator + docuBridge product references*.

### Vendor

- Veeva — *Vault Submissions + Submissions Publishing 24R3 Configuration Reference*.
- Veeva — *Vault Submissions Archive Reference*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

