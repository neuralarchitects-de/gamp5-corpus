---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (v1.0 DS corpus ship)"
seed_corpus_basis:
  - "VLP-FS-EDMS-001 v1.1 (parent FS, T3 Cat 4)"
  - "VLP-URS-EDMS-001 v1.0 (parent URS, transitive)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 Configuration Specification conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11"
  - "ICH Q10; ICH Q12; ISO 9001:2015 §7.5; ISO 13485:2016 §§ 4.2.4, 4.2.5"
  - "PIC/S PI 041; ISO/IEC 27001:2022"
  - "Veeva Vault QualityDocs 24R3 / 25R1 — Configuration Reference + Validation Approach"
parent_fs:
  document_number: VLP-FS-EDMS-001
  version: "1.1"
  file: ../../../FS_FDS/_generated/final/Vellis_Pharma_EDMS_FS_v1.3.md
parent_urs:
  document_number: VLP-URS-EDMS-001
  version: "1.1"
  file: ../../../URS/_generated/final/EDMS_Electronic_Document_Management_System__Vellis_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## EDMS — Veeva Vault QualityDocs 24R3 / 25R1 — Vellis Pharma Madrid HQ

**Document Number:** VLP-DS-EDMS-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** VLP-FS-EDMS-001 v1.1
**Parent URS:** VLP-URS-EDMS-001 v1.0
**Site:** Vellis Pharma Holdings, Madrid HQ, Spain *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS, hybrid w/ Cat 5 OCR + Redaction services)
**Project Mode:** Greenfield-SaaS + on-prem Cat 5 services
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; ICH Q10; ICH Q12 (RIM linkage); ISO 9001 §7.5; ISO 13485 §§ 4.2.4, 4.2.5

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Head of Document Control) | _____________ | _____________ | _____ |
| Reviewer (QA Reviewer) | _____________ | _____________ | _____ |
| Reviewer (System Owner — Head of Quality) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — Document Coordinator) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (Data Integrity Officer) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue. Inherited Tier T3 from parent URS+FS pair. DS covers 84/84 FS-IDs; 0 FS-IDs flagged as vendor-internal — no site design surface. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

| Term | Definition |
|---|---|
| CI | Configuration Item in Veeva Vault QualityDocs |
| Doc-type | Vault document-type configuration with attached lifecycle, role-bindings, retention class |
| Rendition | Vault-generated PDF/A-3 derivative with watermarks |
| OCR | Optical Character Recognition pipeline ingesting legacy paper into Vault |
| Inspection-redaction | Destructive PDF flatten + watermark for regulator-readable redacted copy |
| Verified by | Planned IQ / OQ / PQ test |

## 1. Purpose

This Configuration Specification records the technical design of Veeva Vault QualityDocs 24R3 / 25R1 at Vellis Pharma, including doc-type library, lifecycle configurations, naming-convention engine, periodic-review scheduler, audit-trail review tool configuration, plus the two site-developed Cat-5 services (`vlp-ocr-svc` and `vlp-redact-svc`) that escalate this system to hybrid Cat 4 + Cat 5.

## 2. Scope

**In scope:** Vault QualityDocs tenancy configuration; doc-type library; lifecycles + workflows; security profiles; AD groups; renditions; periodic-review scheduler; audit-trail tooling; multi-region federation (EMEA / NA / APAC); integration bindings to Okta + MasterControl eQMS + Cornerstone LMS + PAS-X + OCR + Inspection-Redaction. Mini-SDS in § 8 for the two site-developed Cat-5 services.

**Out of scope:** Veeva Vault vendor source-code internals; Okta vendor internals; MasterControl internals; Cornerstone internals; PAS-X internals.

## 3. Architectural Overview

The Vellis tenancy operates with per-doc-type lifecycles, role-bindings, retention classes, and the `vlp-naming-engine` enforcing patterns at create. Periodic-review scheduler runs daily; expiring docs surface as review tasks. Two site-developed Cat-5 services (`vlp-ocr-svc`, `vlp-redact-svc`) integrate via REST. Multi-region federation maps EMEA-primary for SOPs/QM, NA-primary for FDA-submissions, APAC-primary for region-specific items.

```
                           ┌──────────────────────────────────┐
                           │   Okta SAML 2.0 + MFA            │
                           └──────────────────┬───────────────┘
                                              │
              ┌───────────────────────────────▼────────────────────────────┐
              │  Veeva Vault QualityDocs 24R3 / 25R1 — Vellis tenancy      │
              │  ┌──────────────────────────────────────────────────┐      │
              │  │  Doc types: SOP / WI / MBR / VP / VR / QM /       │      │
              │  │   RA / Spec / Form / Policy                       │      │
              │  └──────────────────────────────────────────────────┘      │
              │  ┌──────────────┐ ┌──────────────────┐ ┌──────────────┐   │
              │  │ Lifecycles    │ │ Naming-engine    │ │ Periodic-rev │   │
              │  │ + renditions  │ │ (regex per type) │ │ scheduler     │   │
              │  └──────────────┘ └──────────────────┘ └──────────────┘   │
              │  ┌──────────────┐ ┌──────────────────────────────┐         │
              │  │ Audit-trail   │ │ Multi-region federation       │         │
              │  │ focused review│ │ (EMEA / NA / APAC)            │         │
              │  └──────────────┘ └──────────────────────────────┘         │
              └──┬──────────┬─────────────┬────────────┬────────────────────┘
                 │          │             │            │
                 ▼          ▼             ▼            ▼
            MasterControl Cornerstone   PAS-X        OCR + Redaction
            eQMS          LMS           (URN)        (site-developed Cat 5)
            (CR-id)       (training)
```

### 3.1 Component-design inventory

| Layer | Component | Vendor / source | Version | Site design surface |
|---|---|---|---|---|
| Application | Vault QualityDocs tenancy | Veeva | 24R3 → 25R1 | Configuration (§ 4) |
| Identity | Okta | Okta | per site IT | Configuration (§ 4 + § 7) |
| Counterparty | MasterControl eQMS | MasterControl | QMS 2025 | Bindings (§ 7) |
| Counterparty | Cornerstone LMS | Cornerstone | 2025 | Bindings (§ 7) |
| Counterparty | PAS-X | Werum | 3.2 | Bindings (§ 7) |
| Site-developed Cat-5 | `vlp-ocr-svc` | In-house | per release | § 8 mini-SDS |
| Site-developed Cat-5 | `vlp-redact-svc` | In-house | per release | § 8 mini-SDS |

---

## 4. Configuration Specification

### 4.1 Vendor Assurance bindings

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VND-01 | Vendor-quality register (`VLP-VND-REG.Veeva`) | SOC 2 Type II + ISO 27001 + customer-shared IQ/OQ | Custom | Critical-vendor qualification | FS-VND-01 | OQ-VND-REG-01 |
| DS-VND-02 | Vault-release evaluation runbook (`VLP-RB-VAULT-RELEASE`) | review ≤ 14 d; classify impact; CR per `VLP-CR-TEMPLATE` | Custom | Vendor-release cadence | FS-VND-02 | OQ-VND-REL-01 |
| DS-VND-03 | SLA review (`Veeva Trust portal`) | quarterly | Default | Vendor portal | FS-VND-03 | OQ-VND-SLA-01 |
| DS-VND-04 | Escalation runbook (`VLP-RB-VAULT-ESCALATE`) | named Veeva contacts | Custom | Operational escalation | FS-VND-04 | OQ-VND-ESCALATE-01 |

### 4.2 Document Lifecycle CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-LC-01 | Vault lifecycle id (`vlp_doc_lifecycle_v3`) | `DRAFT → IN-REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE` | Custom | 6-state | FS-LC-01 | OQ-LIFECYCLE-STATES-01 |
| DS-LC-02 | Per-state atomic security profile | role assignments per state via Vault native | Custom | State-bound permissions | FS-LC-02 | OQ-SEC-PROFILE-01 |
| DS-LC-03 | EFFECTIVE content lock | DB-layer; new versions require `change_request_ref` | Custom | Anti-tamper | FS-LC-03 | OQ-EFFECTIVE-LOCK-01 |
| DS-LC-04 | Supersede rendition (`vlp_render_superseded`) | stamps prior + embeds new doc-id link | Custom | Provenance | FS-LC-04 | OQ-SUPERSEDE-REND-01 |
| DS-LC-05 | Obsolete-search view (`vlp_search_obsolete`) | searchable; effective-date + obsolete-reason captured | Custom | Audit-trail discovery | FS-LC-05 | OQ-OBSOLETE-SEARCH-01 |
| DS-LC-06 | Per-doc-type SLA fields (`draft_to_review_sla_hours`, `review_to_approve_sla_hours`) | per doc-type defaults | Custom | KPI tracking | FS-LC-06 | OQ-SLA-FIELDS-01 |

### 4.3 Doc Type Library + Naming Convention CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-DT-01 | Doc-type list | `SOP, WI, MBR, VP, VR, QM, RA, Spec, Form, Policy` | Custom | Site library scope | FS-DT-01 | OQ-DOC-TYPES-01 |
| DS-DT-02 | Doc-type metadata schema | per doc-type: lifecycle, default reviewer/approver, retention class, `training_impact_flag` | Custom | Type-aware config | FS-DT-02 | OQ-DT-META-01 |
| DS-DT-03 | Doc-type change workflow (`vlp_wf_doc_type_change`) | Naming Steward + Vault Admin sigs; legacy preserved | Custom | Library governance | FS-DT-03 | OQ-DT-CHANGE-01 |
| DS-DT-04 | Naming-convention engine (`vlp-naming-engine`) | regex per doc-type, e.g. `^SOP-[A-Z]{2,3}-[A-Z]{2,4}-\d{3,4}$` | Custom | Consistency at create | FS-DT-04 | OQ-NAMING-REGEX-01 |
| DS-DT-05 | Doc-type dashboard (`vlp_dashboard_doc_type`) | counts by lifecycle, periodic-review due, last-modified | Custom | Operational view | FS-DT-05 | PQ-DT-DASH-01 |

### 4.4 Authoring / Review / Approval CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-WF-01 | Submission gate (`vlp_wf_submit_review`) | metadata-completeness check; blocks on missing | Custom | Pre-review hygiene | FS-WF-01 | OQ-SUBMIT-GATE-01 |
| DS-WF-02 | Route config (`vlp_route_config`) | parallel + sequential per doc-type | Custom | Workflow flexibility | FS-WF-02 | OQ-ROUTE-CFG-01 |
| DS-WF-03 | E-sig re-auth | Okta re-auth at every signature | Default | § 11.200 | FS-WF-03 | OQ-SIG-REAUTH-01 |
| DS-WF-04 | Rejection capture | `rejection_reason ≥ 50 chars`; returns to DRAFT; prior sigs preserved in audit trail | Custom | Audit-trail completeness | FS-WF-04 | OQ-REJECT-CAPTURE-01 |
| DS-WF-05 | Notification routing | Cornerstone + email within 5 min | Custom | Workflow visibility | FS-WF-05 | OQ-NOTIFY-01 |
| DS-WF-06 | View-then-sign workflow (`vlp_wf_view_then_sign`) | per-doc view-event required | Custom | Anti-bulk-sign | FS-WF-06 | OQ-VIEW-THEN-SIGN-01 |

### 4.5 Renditions / Watermarking / Distribution CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-REND-01 | Effective rendition profile (`vlp_rend_effective`) | watermark "EFFECTIVE — copy is uncontrolled when printed" | Custom | Distribution control | FS-REND-01 | OQ-EFFECTIVE-REND-01 |
| DS-REND-02 | Supersede rendition profile (`vlp_rend_superseded`) | watermark "SUPERSEDED" + effective-date + new-doc-id link | Custom | Reader currency | FS-REND-02 | OQ-SUPERSEDE-REND-02 |
| DS-REND-03 | Signature page template (`vlp_sig_page_v3`) | signer + role + meaning + ts + document SHA-256 | Custom | § 11.50 manifestation | FS-REND-03 | OQ-SIG-PAGE-01 |
| DS-REND-04 | Reader cache TTL (`READER_CACHE_TTL_S`) | `60` | Default | Currency freshness | FS-REND-04 | OQ-READER-CACHE-01 |
| DS-REND-05 | Inspection cover-page (`vlp_inspection_cover_v2`) | hash + effective-date + signer chain + naming-conv OK | Custom | Inspection-readiness | FS-REND-05 | OQ-INSPECTION-COVER-01 |

### 4.6 Training Linkage CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-TRAIN-01 | LMS task push (`IF-LMS-TASK-PUSH`) | triggered at EFFECTIVE for `training_impact_flag = true` | Custom | Training cycle binding | FS-TRAIN-01 | OQ-LMS-PUSH-01 |
| DS-TRAIN-02 | Train-gate security (`vlp_train_gate`) | blocks read until LMS completion-flag satisfied | Custom | Read-and-understood enforcement | FS-TRAIN-02 | OQ-TRAIN-GATE-01 |
| DS-TRAIN-03 | Superseded training-FK retention | deletion blocked | Custom | Historical evidence | FS-TRAIN-03 | OQ-TRAIN-FK-RET-01 |
| DS-TRAIN-04 | Per-doc-type `training_impact_flag` | configurable | Custom | Selective training | FS-TRAIN-04 | OQ-TRAIN-FLAG-01 |
| DS-TRAIN-05 | KPI report (`vlp_rpt_training_kpi`) | quarterly per audience | Custom | KPI reporting | FS-TRAIN-05 | PQ-TRAIN-KPI-01 |

### 4.7 Periodic Review Automation CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PRA-01 | Periodic-review scheduler (`vlp_pr_scheduler`) | per-doc-type cadence; tasks at `D-30, D-7, D-0` | Custom | PR cadence | FS-PRA-01 | OQ-PR-SCHED-01 |
| DS-PRA-02 | Overdue eQMS deviation push | category `EDMS_PR_OVERDUE` | Custom | Escalation | FS-PRA-02 | OQ-PR-OVERDUE-DEV-01 |
| DS-PRA-03 | PR outcome enum | `no-change, minor, major` → MasterControl CR | Custom | CR routing | FS-PRA-03 | OQ-PR-OUTCOME-01 |
| DS-PRA-04 | PR dashboard (`vlp_dashboard_pr`) | upcoming / overdue per doc-type | Custom | Operational view | FS-PRA-04 | OQ-PR-DASH-01 |

### 4.8 Audit-Trail Review CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUD-01 | Audit-trail coverage | state transitions, content edits, metadata edits, security changes, user-access events | Default | Native trail | FS-AUD-01 | OQ-AUDIT-COVERAGE-01 |
| DS-AUD-02 | Append-only enforcement | Veeva DB-layer; CSV + PDF export | Default | Vendor-managed | FS-AUD-02 | OQ-AUDIT-APPEND-01 |
| DS-AUD-03 | Monthly + quarterly review cadence | Document-Coordinator monthly + QA quarterly; ≥ 25 y | Custom | Annex 11 § 9 | FS-AUD-03 | OQ-AUDIT-REVIEW-01 |
| DS-AUD-04 | Retention policy (`vlp_ret_25y`) | 25 y post-retirement | Custom | EU GMP Ch. 4 | FS-AUD-04 | IQ-RET-POLICY-01 |
| DS-AUD-05 | Focused-review tool (`VLP-AUD-FOCUSED-v3`) | signatures, naming-overrides, OCR finalisations, redaction ops, mass deletions, role-perm edits | Custom | Reviewer efficiency | FS-AUD-05 | OQ-FOCUSED-REVIEW-01 |
| DS-AUD-06 | Export manifest | S3 Object Lock + SHA-256 manifest | Custom | Chain-of-custody | FS-AUD-06 | OQ-AUDIT-EXPORT-01 |

### 4.9 21 CFR Part 11 / Annex 11 CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PART11-01 | Procedural-control SOP (`VLP-SOP-CSV-01`) | linked from system docs | Custom | § 11.10(a) | FS-PART11-01 | OQ-SOP-LINK-01 |
| DS-PART11-02 | Export formats (`PDF/A-3, CSV`) | OQ-validated | Custom | § 11.10(b) | FS-PART11-02 | OQ-INSPECTION-COPY-01 |
| DS-PART11-03 | IdP (Okta SAML 2.0 + MFA) | enforced | Custom | § 11.10(d) | FS-PART11-03 | OQ-OKTA-MFA-01 |
| DS-PART11-04 | E-sig manifestation | `printedName + dateTime + meaning` | Default | § 11.50 | FS-PART11-04 | OQ-SIG-MANIFEST-01 |
| DS-PART11-05 | Signature binding | HMAC-SHA256 over doc-hash + signer-id + ts | Default | § 11.70 | FS-PART11-05 | OQ-SIG-BINDING-01 |
| DS-PART11-06 | Account uniqueness | Okta-Vault provisioning constraint | Custom | § 11.100 | FS-PART11-06 | OQ-ACCT-UNIQUE-01 |
| DS-PART11-07 | Re-auth max-age (`SIG_REAUTH_MAX_AGE_S=300`) | 5 min | Default | § 11.200 | FS-PART11-07 | OQ-SIG-REAUTH-01 |
| DS-PART11-08 | Password policy | length 14 + complexity + 90 d max-age | Custom | § 11.300 | FS-PART11-08 | OQ-PWD-POLICY-01 |
| DS-PART11-09 | Validation evidence index (`VLP-VAL-EVID-INDEX`) | Annex 11 § 4 | Custom | Doc completeness | FS-ANX11-01 | OQ-VAL-EVID-IDX-01 |
| DS-PART11-10 | Accuracy checks | enum / range / format / required | Custom | Annex 11 § 6 | FS-ANX11-02 | OQ-ACCURACY-01 |

### 4.10 OCR Workflow CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-OCR-01 | OCR event table (`vlp_ocr_event`) | operator + batch-id + scan-device + scan-ts + OCR-engine + version | Custom | Forensic provenance | FS-OCR-01 | OQ-OCR-EVENT-01 |
| DS-OCR-02 | OCR verify workflow (`vlp_wf_ocr_verify`) | per-page comparison vs original before EFFECTIVE | Custom | QA gate | FS-OCR-02 | OQ-OCR-VERIFY-01 |
| DS-OCR-03 | OCR SoD groups (`OCR-Operator` ≠ `OCR-Verifier`) | exclusive Vault security groups | Custom | SoD | FS-OCR-03 | OQ-OCR-SOD-01 |
| DS-OCR-04 | Confidence threshold (`OCR_CONFIDENCE_THRESHOLD`) | `95%` default; per-doc-type override | Default | Quality threshold | FS-OCR-04 | OQ-OCR-CONFIDENCE-01 |
| DS-OCR-05 | Paper retention (`VLP-RET-PAPER`) | link in `vlp_doc.original_paper_ref` | Custom | Original-record preservation | FS-OCR-05 | OQ-OCR-PAPER-RET-01 |

### 4.11 Inspection Redaction CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RED-01 | Redaction service binding (`vlp-redact-svc`) | role `Inspection Redactor`; output `vlp_inspection_copies` | Custom | Service binding | FS-RED-01 | OQ-REDACT-BIND-01 |
| DS-RED-02 | Watermark (`INSPECTION_WM`) | "INSPECTION COPY — REDACTED — <date>" | Custom | Visibility | FS-RED-02 | OQ-REDACT-WM-01 |
| DS-RED-03 | Destructive flatten | rasterise + flatten; source unaffected | Custom | Anti-reverse | FS-RED-03 | OQ-REDACT-FLATTEN-01 |
| DS-RED-04 | Bulk-redaction role gate | `Inspection-Redactor` + `Vault-Admin` only; surfaces in focused review | Custom | Anti-exfil | FS-RED-04 | OQ-REDACT-BULK-01 |

### 4.12 Search CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-SEARCH-01 | Search service | full-text + structured-field with RBAC filter | Default | Native | FS-SEARCH-01 | OQ-SEARCH-RBAC-01 |
| DS-SEARCH-02 | Inspection-retrieval queue (`vlp_inspection_queue`) | priority queue; SLA-breach metrics | Custom | SLA discipline | FS-SEARCH-02 | OQ-INSPECTION-QUEUE-01 |
| DS-SEARCH-03 | Result columns | doc-type / lifecycle / effective-date / naming-conv-OK / periodic-review-due | Custom | Inspector relevance | FS-SEARCH-03 | OQ-SEARCH-COLS-01 |
| DS-SEARCH-04 | Saved-query export (`vlp_search_export`) | persistence + CSV | Default | Saved searches | FS-SEARCH-04 | OQ-SEARCH-EXPORT-01 |

### 4.13 Multi-Region Federation CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-FED-01 | Federation primary map | `EMEA: SOPs+QM; NA: FDA-submission; APAC: region-specific` | Custom | Per-domain authority | FS-FED-01 | OQ-FED-PRIMARY-01 |
| DS-FED-02 | Cross-region link (`vlp_fed_link`) | preserves source-region audit | Custom | Audit-trail integrity | FS-FED-02 | OQ-FED-LINK-01 |

### 4.14 Integration CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-INT-EQMS-01 | CR-id resolver (`IF-EQMS-CR`) | REST bidirectional; monthly reconciliation reports broken refs | Custom | CR-binding | FS-INT-EQMS-01 | OQ-EQMS-CR-RESOLVE-01 |
| DS-INT-LMS-01 | LMS task push (`IF-LMS-TASK-PUSH`) | REST outbound; idempotency `vault:doc:<id>:ver:<version>` | Custom | Idempotent training cycle | FS-INT-LMS-01 | OQ-LMS-PUSH-INT-01 |
| DS-INT-LMS-02 | Train-gate enforcement reference | `vlp_train_gate` via DS-TRAIN-02 | Custom | Reading-and-understood enforcement | FS-INT-LMS-02 | OQ-TRAIN-GATE-02 |
| DS-INT-PASX-01 | PAS-X URN resolver (`IF-PASX-URN`) | REST outbound; failures alert ≤ 5 min | Custom | MBR consumer | FS-INT-PASX-01 | OQ-PASX-URN-01 |
| DS-INT-OCR-01 | OCR ingest endpoint | `POST /api/v1/edms/ocr-ingest`; operator + verifier metadata | Custom | Cat-5 binding | FS-INT-OCR-01 | OQ-OCR-INGEST-01 |
| DS-INT-SSO-01 | Okta SAML 2.0 + MFA | per realm `vellis.okta.com` | Custom | Site IdP | FS-INT-SSO-01 | OQ-OKTA-SAML-01 |

### 4.15 Data Integrity CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-DI-01 | `actor_id` not-null | Vault audit-write constraint | Default | Attributable | FS-DI-01 | OQ-DI-ACTOR-01 |
| DS-DI-02 | PDF/A-3 with embedded fonts | rendition default | Custom | Legible | FS-DI-02 | OQ-DI-PDFA-01 |
| DS-DI-03 | Veeva NTP-synced timestamps | vendor-managed | Default | Contemporaneous | FS-DI-03 | OQ-DI-NTP-01 |
| DS-DI-04 | Content preservation; renditions reference only | vendor default | Default | Original | FS-DI-04 | OQ-DI-ORIGINAL-01 |
| DS-DI-05 | Workflow-logic OQ | per-lifecycle | Custom | Accurate | FS-DI-05 | OQ-DI-WORKFLOW-01 |
| DS-DI-06 | Retrieval ≤ 4 h | priority queue | Custom | Available | FS-DI-06 | PQ-DI-RETRIEVE-01 |

### 4.16 Backup CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-BAK-01 | Veeva-managed backup verification | annual; RPO ≤ 4 h / RTO ≤ 24 h | Custom | Vendor-assurance | FS-BAK-01 | PQ-BAK-VERIFY-01 |
| DS-BAK-02 | Site config export script (`vlp-config-export.sh`) | doc-types, lifecycles, security profiles, naming rules | Custom | Site-side backup | FS-BAK-02 | OQ-CONFIG-EXPORT-01 |

### 4.17 Performance / Security CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PERF-01 | Open/search P95 | ≤ 3 s | Default | Vendor SLA | FS-PERF-01 | PQ-PERF-OPEN-01 |
| DS-PERF-02 | Bulk-importer (`vlp-bulk-importer`) | ≥ 1k docs in 4 h SLA | Custom | Bulk capability | FS-PERF-02 | PQ-BULK-IMPORT-01 |
| DS-AV-01 | Vendor SLA target | ≥ 99.7% | Default | Vendor SLA | FS-AV-01 | OQ-AV-SLA-01 |
| DS-SEC-01 | Okta SSO + MFA enforced; break-glass (`VLP-VAULT-BREAKGLASS`) | monthly audit | Custom | Emergency continuity | FS-SEC-01 | OQ-BREAKGLASS-01 |
| DS-SEC-02 | Download watermark + bulk-export off-default | per rendition profile | Custom | Anti-exfil | FS-SEC-02 | OQ-DOWNLOAD-WM-01 |
| DS-SEC-03 | Bulk-export tagging (`BULK_EXPORT`) | audit-trail tag; surfaced in focused review | Custom | Visibility | FS-SEC-03 | OQ-BULK-EXPORT-TAG-01 |

### 4.18 Training / Periodic Review CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-TRN-01 | Cornerstone curriculum (`VLP-CURR-EDMS-USER`) | production-access gate | Custom | LMS binding | FS-TRN-01 | OQ-TRN-GATE-01 |
| DS-TRN-02 | Inspection-readiness curriculum (`VLP-CURR-INSPECTION`) | OCR Verifier + Inspection Redactor | Custom | Critical-role | FS-TRN-02 | OQ-INSPECTION-TRN-01 |
| DS-PR-01 | Annual periodic-review template (`VLP-PR-EDMS-YYYYMMDD`) | signed | Custom | Annex 11 § 11 | FS-PR-01 | PQ-PR-EDMS-01 |

### 4.19 Cross-System Bindings (M-XSYS)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-XSYS-AD-01 | Entra ID SAML 2.0 + SCIM | conditional-access policy `Quality-App Conditional Access` | Custom | Per FS-XSYS-AD-01 | FS-XSYS-AD-01 | OQ-XSYS-AD-01 |
| DS-XSYS-AD-02 | SIEM (`Splunk gxp-authn`) | RFC 5424 ≤ 5 min lag | Custom | Cross-system correlation | FS-XSYS-AD-01 | OQ-SIEM-FWD-01 |
| DS-XSYS-AD-03 | CyberArk PAM binding | 24 h rotation + dual-witness check-out | Custom | Break-glass | FS-XSYS-AD-01 | OQ-PAM-01 |
| DS-XSYS-BAK-01 | Veeam VSS + MS SQL Server + object-replica | T1 tier; RPO ≤ 4 h / RTO ≤ 4 BH | Custom | Per FS-XSYS-BAK-01 | FS-XSYS-BAK-01 | OQ-VEEAM-01 |
| DS-XSYS-BAK-02 | S3 Object Lock COMPLIANCE bucket | geo-replicated | Custom | Anti-ransom | FS-XSYS-BAK-01 | IQ-S3-OBJLOCK-01 |
| DS-XSYS-BAK-03 | LTO-9 air-gap rotation | monthly | Custom | Air-gap policy | FS-XSYS-BAK-01 | OQ-LTO9-01 |
| DS-XSYS-BAK-04 | Restore-cert retention | ≥ 25 y in eQMS | Custom | Quality-record discipline | FS-XSYS-BAK-01 | OQ-RESTORE-CERT-01 |
| DS-XINT-HEL-01 | Helios Kafka topic (`helios.ingest.vellis.vault.v1`) | idempotency `{source_system, event_id}` | Custom | Per FS-XINT-HEL-01 | FS-XINT-HEL-01 | OQ-HELIOS-PUB-01 |
| DS-XINT-HEL-02 | Helios lag alert (`HELIOS_LAG_ALERT_S=600`) | Prometheus | Custom | Back-pressure SLO | FS-XINT-HEL-01 | OQ-HELIOS-LAG-01 |
| DS-XINT-HEL-03 | Helios reconciliation cadence | daily 24 h window; > 0.01% raises eQMS deviation | Custom | Parity | FS-XINT-HEL-02 | OQ-HELIOS-RECON-01 |

---

## 5. Workflow + Business-Rule Design

### 5.1 Doc-lifecycle workflow

| Step | State | Actor | Gate |
|---|---|---|---|
| 1 | `DRAFT` | Author | submit-review (metadata completeness gate `vlp_wf_submit_review`) |
| 2 | `IN-REVIEW` | Reviewers (parallel/sequential per `vlp_route_config`) | re-auth e-sig |
| 3 | `APPROVED` | Approver | re-auth e-sig + `view_then_sign` per-doc view-event recorded |
| 4 | `EFFECTIVE` | system | rendition `vlp_rend_effective` applied; LMS task pushed if `training_impact_flag = true` |
| 5 | `SUPERSEDED` | system on supersede | rendition `vlp_render_superseded` stamps prior + new-doc-id link |
| 6 | `OBSOLETE` | system | searchable via `vlp_search_obsolete`; retention applies |

Rejection from `IN-REVIEW` → returns to `DRAFT`; `rejection_reason ≥ 50 chars`; prior sigs preserved.

### 5.2 OCR ingestion workflow

| Step | Actor | Gate |
|---|---|---|
| 1 | OCR Operator (`OCR-Operator`) | invoke `POST /api/v1/edms/ocr-ingest` from `vlp-ocr-svc` |
| 2 | `vlp-ocr-svc` | OCR + confidence calc + page-image attach; below threshold → manual-verify step |
| 3 | OCR Verifier (`OCR-Verifier` ≠ Operator) | per-page comparison via `vlp_wf_ocr_verify` |
| 4 | System | promote to `EFFECTIVE` |
| 5 | Original paper | link in `vlp_doc.original_paper_ref` |

### 5.3 Inspection-redaction workflow

| Step | Actor | Gate |
|---|---|---|
| 1 | Inspection Redactor | identify source doc + redaction zones |
| 2 | `vlp-redact-svc` | rasterise + flatten + watermark "INSPECTION COPY — REDACTED — <date>" |
| 3 | Output | stored in `vlp_inspection_copies`; never edits source |
| 4 | Audit | event in focused-review tool (DS-AUD-05) |

### 5.4 Periodic-review business rule

`vlp_pr_scheduler` runs daily at 02:00 site time. For each doc-type with cadence `C`:
- For each doc with `effective_date + C - 30 d <= today < effective_date + C - 7 d`: create review task (`D-30`).
- For each doc with `effective_date + C - 7 d <= today < effective_date + C`: bump task priority (`D-7`).
- For each doc with `today >= effective_date + C`: `D-0` task + push `EDMS_PR_OVERDUE` deviation to eQMS.

---

## 6. Role-Permission Matrix Design

| Role (Vault security group) | Author | Reviewer | Approver | OCR-Operator | OCR-Verifier | Inspection-Redactor | Vault-Admin | Audit-Reviewer | Naming-Steward |
|---|---|---|---|---|---|---|---|---|---|
| `EDMS-Author` | R/W | – | – | – | – | – | – | – | – |
| `EDMS-Reviewer` | R | R/W | – | – | – | – | – | – | – |
| `EDMS-Approver` | R | R | R/W | – | – | – | – | – | – |
| `OCR-Operator` | – | – | – | R/W | – | – | – | – | – |
| `OCR-Verifier` | – | – | – | R | R/W | – | – | – | – |
| `Inspection-Redactor` | R | – | – | – | – | R/W | – | – | – |
| `Vault-Admin` | – | – | – | – | – | – | R/W | – | – |
| `Audit-Reviewer` | R | R | R | R | R | R | – | R/W | – |
| `Naming-Steward` | R | – | – | – | – | – | – | – | R/W |

SoD: `OCR-Operator ∩ OCR-Verifier = ∅`; `EDMS-Reviewer ∩ EDMS-Approver = ∅` per workflow step; `Inspection-Redactor ∩ Vault-Admin` allowed only via Vault-Admin role assumption (logged).

---

## 7. Integration Design

### 7.1 MasterControl CR-id resolver (FS-INT-EQMS-01)

- Endpoint: REST bidirectional `GET https://eqms.talos.local/api/v2/change-requests/{cr_id}`
- AuthN: mTLS + bearer
- Use: validate `change_request_ref` at version-create
- Monthly reconciliation report `vlp_rpt_cr_reconcile` lists broken references

### 7.2 Cornerstone LMS task push (FS-INT-LMS-01)

- Endpoint: `POST https://lms.vega.local/api/v2/tasks`
- AuthN: mTLS + bearer
- Idempotency: `vault:doc:<id>:ver:<version>`
- Retry: exponential back-off

### 7.3 PAS-X URN resolver (FS-INT-PASX-01)

- Endpoint: `GET https://pasx.caelum.local/api/v1/urn/{urn}`
- Failure: 5-min alert via Prometheus rule `pasx_urn_resolve_error_rate`
- Cache TTL: 24 h consumer-side

### 7.4 OCR pipeline (FS-INT-OCR-01)

- Endpoint: `POST https://ocr.vellis.local/api/v1/edms/ocr-ingest`
- Payload includes operator + scan-device + batch metadata
- Output: per-page text + confidence + verification flag

### 7.5 Inspection Redaction service

- Service: `vlp-redact-svc` (Cat-5 — see § 8.2)
- Endpoint: `POST https://redact.vellis.local/api/v1/redact`
- Output: PDF/A-3 redacted copy stored in `vlp_inspection_copies`

### 7.6 Okta SSO + MFA (FS-INT-SSO-01)

- Protocol: SAML 2.0 + SCIM 2.0
- MFA: TOTP / WebAuthn at every sig event
- Re-auth max-age: 300 s

### 7.7 Helios audit-event handover (FS-XINT-HEL-01..02)

- Kafka topic: `helios.ingest.vellis.vault.v1`
- Schema-registry pinned envelope
- Delivery: at-least-once; reconciliation: daily

---

## 8. Site-Deployed Components Design (mini-SDS — Cat-5 sub-components)

### 8.1 `vlp-ocr-svc` — Legacy-paper OCR pipeline

| Aspect | Design |
|---|---|
| Repo | `git.vellis.local/quality-it/vlp-ocr-svc` |
| Language | Python 3.11 |
| Modules | `scanner_ingest`, `ocr_engine_wrapper` (Tesseract 5.3 + ABBYY FineReader Engine 12 fallback), `confidence_calculator`, `vlp_ocr_event_writer`, `verification_workflow_emitter` |
| Interface | REST `POST /api/v1/edms/ocr-ingest`; writes to Vault via Vault REST API + `vlp_ocr_event` audit table |
| Dependencies | Vault SDK; Tesseract 5.3; ABBYY FRE 12 (vendor lib pinned); psycopg2 (audit DB); pinned `requirements.txt` |
| GxP-criticality | R1 (legacy-doc fidelity for GxP records) |
| Owner | Vellis Quality IT |
| SDLC | signed commits (Sigstore); CI unit + integration tests against golden-OCR corpus; CR-controlled release |
| Determinism | OCR engine deterministic per fixed parameters; confidence threshold default 95% |

### 8.2 `vlp-redact-svc` — Inspection-redaction service

| Aspect | Design |
|---|---|
| Repo | `git.vellis.local/quality-it/vlp-redact-svc` |
| Language | Python 3.11 + PDFBox (Java 17) for PDF flatten |
| Modules | `redact_zone_parser`, `rasterizer`, `flattener`, `watermark_applier`, `inspection_copy_writer`, `audit_emitter` |
| Interface | REST `POST /api/v1/redact`; reads source via Vault REST; writes to `vlp_inspection_copies` |
| Dependencies | Vault SDK; PyPDF2; PDFBox 3.x (vendor lib pinned); Pillow; pinned `requirements.txt` |
| GxP-criticality | R1 (inspection-readiness; redaction must be irreversible) |
| Owner | Vellis Quality IT |
| SDLC | signed commits + CI + CR-controlled release |
| Anti-reverse design | rasterise-first-then-flatten ensures redacted regions are not recoverable as PDF objects |

---

## 9. References

### US
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11

### DACH
- BfArM (DE) — informational reference for DACH-supervised regions
- Swissmedic (CH) — informational reference

### International
- ICH Q10
- ICH Q12 (RIM linkage)
- ISO 9001:2015 § 7.5
- ISO 13485:2016 §§ 4.2.4, 4.2.5
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE GAMP GPG *Records & Data Integrity*
- PIC/S PI 041
- ISO/IEC 27001:2022

### Vendor
- Veeva — *Vault QualityDocs 24R3 / 25R1 Configuration Reference*
- Veeva — *Vault Platform Validation Approach*
- Tesseract — *5.3 OCR Engine Reference*
- ABBYY — *FineReader Engine 12 Developer Reference*
- Apache — *PDFBox 3.x Reference*

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-VND-01 | FS-VND-01 |
| DS-VND-02 | FS-VND-02 |
| DS-VND-03 | FS-VND-03 |
| DS-VND-04 | FS-VND-04 |
| DS-LC-01 | FS-LC-01 |
| DS-LC-02 | FS-LC-02 |
| DS-LC-03 | FS-LC-03 |
| DS-LC-04 | FS-LC-04 |
| DS-LC-05 | FS-LC-05 |
| DS-LC-06 | FS-LC-06 |
| DS-DT-01 | FS-DT-01 |
| DS-DT-02 | FS-DT-02 |
| DS-DT-03 | FS-DT-03 |
| DS-DT-04 | FS-DT-04 |
| DS-DT-05 | FS-DT-05 |
| DS-WF-01 | FS-WF-01 |
| DS-WF-02 | FS-WF-02 |
| DS-WF-03 | FS-WF-03 |
| DS-WF-04 | FS-WF-04 |
| DS-WF-05 | FS-WF-05 |
| DS-WF-06 | FS-WF-06 |
| DS-REND-01 | FS-REND-01 |
| DS-REND-02 | FS-REND-02 |
| DS-REND-03 | FS-REND-03 |
| DS-REND-04 | FS-REND-04 |
| DS-REND-05 | FS-REND-05 |
| DS-TRAIN-01 | FS-TRAIN-01 |
| DS-TRAIN-02 | FS-TRAIN-02 |
| DS-TRAIN-03 | FS-TRAIN-03 |
| DS-TRAIN-04 | FS-TRAIN-04 |
| DS-TRAIN-05 | FS-TRAIN-05 |
| DS-PRA-01 | FS-PRA-01 |
| DS-PRA-02 | FS-PRA-02 |
| DS-PRA-03 | FS-PRA-03 |
| DS-PRA-04 | FS-PRA-04 |
| DS-AUD-01 | FS-AUD-01 |
| DS-AUD-02 | FS-AUD-02 |
| DS-AUD-03 | FS-AUD-03 |
| DS-AUD-04 | FS-AUD-04 |
| DS-AUD-05 | FS-AUD-05 |
| DS-AUD-06 | FS-AUD-06 |
| DS-PART11-01 | FS-PART11-01 |
| DS-PART11-02 | FS-PART11-02 |
| DS-PART11-03 | FS-PART11-03 |
| DS-PART11-04 | FS-PART11-04 |
| DS-PART11-05 | FS-PART11-05 |
| DS-PART11-06 | FS-PART11-06 |
| DS-PART11-07 | FS-PART11-07 |
| DS-PART11-08 | FS-PART11-08 |
| DS-PART11-09 | FS-ANX11-01 |
| DS-PART11-10 | FS-ANX11-02 |
| DS-OCR-01 | FS-OCR-01 |
| DS-OCR-02 | FS-OCR-02 |
| DS-OCR-03 | FS-OCR-03 |
| DS-OCR-04 | FS-OCR-04 |
| DS-OCR-05 | FS-OCR-05 |
| DS-RED-01 | FS-RED-01 |
| DS-RED-02 | FS-RED-02 |
| DS-RED-03 | FS-RED-03 |
| DS-RED-04 | FS-RED-04 |
| DS-SEARCH-01 | FS-SEARCH-01 |
| DS-SEARCH-02 | FS-SEARCH-02 |
| DS-SEARCH-03 | FS-SEARCH-03 |
| DS-SEARCH-04 | FS-SEARCH-04 |
| DS-FED-01 | FS-FED-01 |
| DS-FED-02 | FS-FED-02 |
| DS-INT-EQMS-01 | FS-INT-EQMS-01 |
| DS-INT-LMS-01 | FS-INT-LMS-01 |
| DS-INT-LMS-02 | FS-INT-LMS-02 |
| DS-INT-PASX-01 | FS-INT-PASX-01 |
| DS-INT-OCR-01 | FS-INT-OCR-01 |
| DS-INT-SSO-01 | FS-INT-SSO-01 |
| DS-DI-01 | FS-DI-01 |
| DS-DI-02 | FS-DI-02 |
| DS-DI-03 | FS-DI-03 |
| DS-DI-04 | FS-DI-04 |
| DS-DI-05 | FS-DI-05 |
| DS-DI-06 | FS-DI-06 |
| DS-BAK-01 | FS-BAK-01 |
| DS-BAK-02 | FS-BAK-02 |
| DS-PERF-01 | FS-PERF-01 |
| DS-PERF-02 | FS-PERF-02 |
| DS-AV-01 | FS-AV-01 |
| DS-SEC-01 | FS-SEC-01 |
| DS-SEC-02 | FS-SEC-02 |
| DS-SEC-03 | FS-SEC-03 |
| DS-TRN-01 | FS-TRN-01 |
| DS-TRN-02 | FS-TRN-02 |
| DS-PR-01 | FS-PR-01 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 |
| DS-XSYS-AD-02 | FS-XSYS-AD-01 |
| DS-XSYS-AD-03 | FS-XSYS-AD-01 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| DS-XSYS-BAK-02 | FS-XSYS-BAK-01 |
| DS-XSYS-BAK-03 | FS-XSYS-BAK-01 |
| DS-XSYS-BAK-04 | FS-XSYS-BAK-01 |
| DS-XINT-HEL-01 | FS-XINT-HEL-01 |
| DS-XINT-HEL-02 | FS-XINT-HEL-01 |
| DS-XINT-HEL-03 | FS-XINT-HEL-02 |

---

## 11. Design-level Risk Register

| ID | Design-level risk | Origin (DS-ID / design choice) | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|---|
| DR-01 | Veeva release silently changes lifecycle-rendition behaviour | DS-VND-02 + DS-REND-01 | Medium | Medium | Release-eval runbook; UAT regression |
| DR-02 | Naming-engine regex too permissive — duplicate doc IDs slip through | DS-DT-04 | Low | High | Regex review at every doc-type add; OQ-NAMING-REGEX-01 |
| DR-03 | Periodic-review scheduler drift — overdue task creation misses 24 h window | DS-PRA-01 | Low | High | Scheduler health check; OQ-PR-SCHED-01 |
| DR-04 | `vlp-ocr-svc` ABBYY engine version skew breaks legacy-OCR fidelity | DS-OCR-04 + § 8.1 | Low | High | Engine version pinned; golden-OCR regression in CI |
| DR-05 | `vlp-redact-svc` redaction reversibility (PDF object recovery) due to incomplete flatten | DS-RED-03 + § 8.2 | Low | Critical | Rasterise-first design; OQ-REDACT-FLATTEN-01 + adversarial test |
| DR-06 | Multi-region federation primary failover leaves NA reads stale for FDA filings | DS-FED-01 | Low | High | Veeva federation failover runbook + monitoring |
| DR-07 | LMS-task-push idempotency key collision across two versions of same doc | DS-INT-LMS-01 | Low | Medium | Idempotency key includes version |
| DR-08 | PAS-X URN cache (24 h) returns stale URN after EFFECTIVE→SUPERSEDED transition | DS-INT-PASX-01 + DS-LC-04 | Medium | Medium | Cache invalidation on supersede event; 5-min alert |
| DR-09 | Bulk-export role privilege creep | DS-SEC-02 + DS-SEC-03 | Low | High | Quarterly RBAC review; focused-review surfacing |
| DR-10 | OCR confidence threshold drift (per doc-type override creates inconsistent quality) | DS-OCR-04 | Low | Medium | Doc-type promotion review + UAT regression |
| DR-11 | Naming-Steward + Vault-Admin role overlap defeats library governance | DS-DT-03 + Role matrix | Low | Medium | RBAC review quarterly |
| DR-12 | EFFECTIVE-state content lock bypass via DB-direct write | DS-LC-03 | Low | Critical | DBA dual-control on Veeva-side; vendor-assurance dependency |
| DR-13 | Audit-trail focused-review tool filter list stale after Veeva release | DS-AUD-05 + DS-VND-02 | Medium | Medium | Vendor-release runbook reviews focused-review filters |
| DR-14 | Periodic-review past-due deviation push fails — overdue but unflagged | DS-PRA-02 + DS-INT-EQMS-01 | Low | High | Retry queue + Prometheus error metric |
| DR-15 | Inspection-redaction source-doc accidentally exposed via Vault search (RBAC gap) | DS-RED-01 + DS-SEARCH-01 | Low | Critical | RBAC review + OQ-SEARCH-RBAC-01 |
| DR-16 | OCR-Operator / OCR-Verifier role overlap defeats SoD due to Vault-Admin assumption | DS-OCR-03 | Low | High | Vault-Admin role-assumption logging; monthly audit |
| DR-17 | Helios Kafka topic schema drift between Vellis publisher and Helios consumer | DS-XINT-HEL-01 + DS-XINT-HEL-03 | Low | High | Schema-registry contract test; reconciliation deviation gate |
| DR-18 | Cross-region federation link audit-trail copy fails on EMEA→NA event spike | DS-FED-02 | Low | Medium | Lag metric + degraded-mode fallback |
| DR-19 | Effective-state lifecycle SLA fields (`draft_to_review_sla_hours`) drift in vendor-managed config | DS-LC-06 | Low | Low | Annual config-export audit (DS-BAK-02) |
| DR-20 | Reader cache TTL (60 s) is too short, causing user-perceived load latency, encouraging cached prints | DS-REND-04 | Low | Medium | UX monitoring; document-control communication |

The full formal Risk Assessment is `VLP-RA-EDMS-001` (synthetic, separate document).

---

## 12. Appendix B — Cat 4 + Cat 5 Hybrid Boundary Design Narrative

### 12.1 Why this system is a hybrid

Vault QualityDocs is a configured Cat 4 SaaS at its core, but two site-developed services — `vlp-ocr-svc` (legacy-paper OCR pipeline) and `vlp-redact-svc` (inspection-redaction service) — extend the platform with site-authored Cat 5 code that participates in regulated workflows. Per METHODOLOGY § 2B.4.6, embedded custom code escalates a Cat 4 system to a hybrid Cat 4 + Cat 5. This appendix documents how the boundary is held — what is owned by Veeva (vendor SDLC), what is owned by Vellis Quality IT (site SDLC), and where the two meet.

### 12.2 Boundary inventory

| Concern | Vault native (Cat 4) | Site Cat 5 |
|---|---|---|
| Doc lifecycle states + transitions | Yes (configuration only) | – |
| Workflow routing + e-sig | Yes | – |
| Rendition + watermarking | Yes (rendition profiles) | – |
| Periodic-review scheduler | Yes (`vlp_pr_scheduler` config) | – |
| Audit-trail capture + storage | Yes | – |
| Naming-convention regex enforcement | Yes (per doc-type config) | – |
| OCR ingestion (scan → text + page-image) | – | `vlp-ocr-svc` (see § 8.1 mini-SDS) |
| OCR confidence calculation + thresholding | – | `vlp-ocr-svc` |
| Inspection-redaction (rasterise + flatten + watermark) | – | `vlp-redact-svc` (see § 8.2 mini-SDS) |
| Doc-type metadata schema | Yes (Vault config) | – |
| Doc-type change workflow `vlp_wf_doc_type_change` | Yes | – |
| Cross-region federation primary mapping | Yes | – |

### 12.3 Cat 5 boundary integrity rules

The two Cat 5 services participate in EFFECTIVE-state workflows and must satisfy the full Cat 5 SDLC discipline of GAMP 5 (2nd ed.) § 7 plus IEC 62304 alignment where applicable:

- Signed commits via Sigstore
- Per-module sidecar Model Card with intended use + risk class + FS-ID coverage + OQ pointers
- Static analysis (Bandit + mypy strict) + dependency scan (Trivy + Snyk) on every CI build
- Release deploys via cosign-signed container images; CR-controlled
- Regression suite against golden corpora (golden-OCR files for `vlp-ocr-svc`; adversarial reverse-engineering corpus for `vlp-redact-svc`)
- Release manifest `release-vN-manifest.json` with SHA-256 per service

### 12.4 OCR-pipeline business rule (per-page comparison)

When `vlp-ocr-svc` ingests a scan, the workflow produces a per-page artefact:

```
ocr_record(doc_id, page_n) = {
    "operator_id": ...,
    "scan_device_id": ...,
    "scan_ts": iso8601,
    "ocr_engine": "Tesseract 5.3" | "ABBYY FRE 12 fallback",
    "engine_version": ...,
    "confidence": 0.0..1.0,
    "text": "...",
    "page_image_sha256": ...,
    "verification_required": bool  # true if confidence < threshold
}
```

When `verification_required = true`, the workflow `vlp_wf_ocr_verify` (Vault-native) is invoked: an OCR-Verifier (≠ OCR-Operator per DS-OCR-03) reviews the page-image vs the OCR text side-by-side and either approves or rejects. Only approved pages can promote the doc to EFFECTIVE.

### 12.5 Inspection-redaction destructive-flatten design

`vlp-redact-svc` is intentionally destructive by design: it never produces a redacted PDF that retains the original objects beneath a redaction box. The sequence is:

1. Render the source PDF page to a high-resolution raster image (300 DPI minimum)
2. Apply the redaction zones as opaque rectangles on the raster
3. Re-encode the raster as a new flat PDF page
4. Apply watermark "INSPECTION COPY — REDACTED — <date>" via overlay
5. Sign the resulting PDF/A-3 with the inspection-copy provenance metadata

Adversarial reverse-engineering tests (in CI) attempt to recover redacted content via PDF-object extraction, OCR re-application, image-residue analysis. The build fails if any redacted content is recoverable. This is the OQ-REDACT-FLATTEN-01 acceptance criterion.

### 12.6 Multi-region federation routing

Vault's cross-domain federation places authority where the content lifecycle naturally lives. SOPs and Quality Manuals originate in EMEA HQ (Madrid); FDA-submission-supporting items (e.g., Vault Submissions binders) live in NA; region-specific items live in APAC. Cross-region links via `vlp_fed_link` preserve the source-region audit trail verbatim — readers in any region see the full forensic chain.

Federation outage handling: each region holds last-known-good cached metadata for read; writes block with explicit "FEDERATION_OUTAGE" reason. Per FS-FED-02, the design accepts read-degraded operation rather than risking a write that breaks audit-trail authority.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
