---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (T3 catch-up; per-ID rows; doc-number aligned VLP-; OCR + redaction implementations; periodic-review automation)"
seed_corpus_basis:
  - "VLP-URS-EDMS-001 v1.0 (parent URS, T3)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 SaaS conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11; ICH Q10"
  - "ISO 9001:2015 §7.5; ISO 13485:2016 §§ 4.2.4, 4.2.5"
  - "Veeva Vault QualityDocs 24R3 / 25R1"
parent_urs:
  document_number: VLP-URS-EDMS-001
  version: 1.0
  file: ../../URS/_generated/final/EDMS_Electronic_Document_Management_System__Vellis_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## EDMS — Veeva Vault QualityDocs 24R3 / 25R1

**Document Number:** VLP-FS-EDMS-001
**Version:** 1.1
**Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** VLP-URS-EDMS-001 v1.0
**Site:** Vellis Pharma Holdings, Madrid HQ, Spain *(fictional)*
**System Class:** GAMP Cat 4 — Configured Product (multi-tenant SaaS)
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; ICH Q10; ISO 9001 §7.5; ISO 13485 §§ 4.2.4, 4.2.5

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of Document Control) | _____________ | _____________ | _____ |
| Reviewer (Data Integrity Officer) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-12 | (synthetic) | T3 catch-up: per-ID rows; doc-number aligned VLP-; OCR + redaction + periodic-review + naming-convention implementations; focused audit-trail review; multi-site federation. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies how Veeva Vault QualityDocs 24R3 → 25R1 is configured at the platform level to satisfy `VLP-URS-EDMS-001` v1.0 — controlled-document lifecycle management for SOPs, master batch records, validation deliverables, work instructions, quality manuals, policies, and OCR-ingested legacy paper.

## 2. Scope

Vault QualityDocs tenancy; per-document-type lifecycles + workflows; SSO via Okta + MFA; integrations with eQMS (CR linkage), LMS (training assignment), PAS-X (URN resolution), OCR pipeline, inspection-redaction tooling. Out: vendor infra.

## 3. System Architecture

```
                Okta SAML 2.0 + MFA
                  │
                  ▼
   ┌────────────────────────────────────────┐
   │  Vault QualityDocs 24R3/25R1 (Vellis)   │
   │  Doc types: SOP / WI / MBR / VP/VR /    │
   │  Spec / Policy / Form / QM / RA         │
   │  Naming-convention engine                │
   │  Periodic-review scheduler               │
   │  Focused audit-trail review tool         │
   └─┬────────┬───────────┬──────────┬───────┘
     │        │           │          │
     ▼        ▼           ▼          ▼
   eQMS     LMS         PAS-X       OCR + Redaction
           (training)   (URN)       pipeline
```

| ID | Component | GAMP Cat |
|---|---|---|
| C-01 | Vault QualityDocs tenancy | 4 |
| C-02 | Okta IdP | (infra) |
| C-03 | MasterControl eQMS | 4 |
| C-04 | LMS (Cornerstone) | 4 |
| C-05 | PAS-X v3.2 | 4 |
| C-06 | OCR pipeline (`vlp-ocr-svc`) | 5 |
| C-07 | Inspection-Redaction service (`vlp-redact-svc`) | 5 |

## 4. Functional Specifications

### 4.1 Vendor Assurance (URS § 5.1)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VND-01 | URS-VND-01 | Veeva qualified as critical SaaS vendor — SOC 2 Type II + ISO 27001 + customer-shared IQ/OQ in `VLP-VND-REG`; annual review. |
| FS-VND-02 | URS-VND-02 | Quarterly Vault Release evaluation runbook `VLP-RB-VAULT-RELEASE` — review notes within 14 days; classify config impact; re-validation ticket per `VLP-CR-TEMPLATE`. |
| FS-VND-03 | URS-VND-03 | Quarterly SLA review via Veeva Trust portal; deviations escalated to QA. |
| FS-VND-04 | URS-VND-04 | Vendor escalation runbook `VLP-RB-VAULT-ESCALATE` with named Veeva contacts. |

### 4.2 Document Lifecycle (URS § 5.2)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-LC-01 | URS-LC-01 | Vault lifecycle config `vlp_doc_lifecycle_v3`: DRAFT → IN-REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE. |
| FS-LC-02 | URS-LC-02 | Atomic security profile per state; e-signed transitions via Vault native workflow. |
| FS-LC-03 | URS-LC-03 | EFFECTIVE-state content lock at Vault DB layer; new versions require CR-id in metadata `change_request_ref`. |
| FS-LC-04 | URS-LC-04 | On SUPERSEDED, rendition trigger `vlp_render_superseded` stamps prior rendition + embeds new doc-id link. |
| FS-LC-05 | URS-LC-05 | OBSOLETE state: effective-date + obsolete-reason captured; remains searchable via `vlp_search_obsolete`. |
| FS-LC-06 | URS-LC-06 | SLA fields per doc-type: `draft_to_review_sla_hours`, `review_to_approve_sla_hours`. |

### 4.3 Document Type Library and Naming Convention (URS § 5.3)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DT-01 | URS-DT-01 | Doc types: SOP, WI, MBR, VP, VR, QM, RA, Spec, Form, Policy; each with metadata schema in Vault config. |
| FS-DT-02 | URS-DT-02 | Doc-type declares lifecycle, default reviewer/approver roles, retention class, `training_impact_flag`. |
| FS-DT-03 | URS-DT-03 | Doc-type change workflow `vlp_wf_doc_type_change`: Naming-Convention Steward + Vault Admin signatures; legacy docs preserved. |
| FS-DT-04 | URS-DT-04 | Naming-convention engine `vlp-naming-engine` enforces patterns at create (regex per doc-type, e.g. `^SOP-[A-Z]{2,3}-[A-Z]{2,4}-\d{3,4}$`); non-conforming rejects with helpful diff. |
| FS-DT-05 | URS-DT-05 | Doc-type dashboard `vlp_dashboard_doc_type` surfaces counts by lifecycle, periodic-review due, last-modified. |

### 4.4 Authoring, Review, Approval (URS § 5.4)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-WF-01 | URS-WF-01 | Metadata-completeness gate at submission `vlp_wf_submit_review`; missing required fields block. |
| FS-WF-02 | URS-WF-02 | Parallel + sequential routes configurable per doc-type via `vlp_route_config`. |
| FS-WF-03 | URS-WF-03 | E-signature with Okta re-auth at every signature event. |
| FS-WF-04 | URS-WF-04 | Rejection captures `rejection_reason` ≥ 50 chars; returns to DRAFT; prior signatures preserved in audit trail. |
| FS-WF-05 | URS-WF-05 | Author notification via Cornerstone + email within 5 min of state transition. |
| FS-WF-06 | URS-WF-06 | Bulk-approve denied: signature requires per-doc view-event recorded in `vlp_wf_view_then_sign`. |

### 4.5 Renditions, Watermarking, Distribution (URS § 5.5)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REND-01 | URS-REND-01 | Veeva rendition profile `vlp_rend_effective` applies watermark "EFFECTIVE — copy is uncontrolled when printed". |
| FS-REND-02 | URS-REND-02 | `vlp_rend_superseded` applies "SUPERSEDED" watermark + effective-date of replacement + new-doc-id link. |
| FS-REND-03 | URS-REND-03 | Signature page template `vlp_sig_page_v3` lists signer, role, meaning, ts, document SHA-256. |
| FS-REND-04 | URS-REND-04 | Reader cache TTL configured 60 s; offline-distribution exception logged via `vlp_wf_offline_exception`. |
| FS-REND-05 | URS-REND-05 | Inspection-ready cover-page template `vlp_inspection_cover_v2` includes hash, effective-date, signer chain, naming-convention compliance. |

### 4.6 Training Record Linkage (URS § 5.6)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRAIN-01 | URS-TRAIN-01 | EFFECTIVE-state transition with `training_impact_flag = true` triggers Cornerstone task creation via `IF-LMS-TASK-PUSH`. |
| FS-TRAIN-02 | URS-TRAIN-02 | Vault security profile blocks read of `training_required` docs until LMS completion-flag is satisfied; gate logic in `vlp_train_gate`. |
| FS-TRAIN-03 | URS-TRAIN-03 | SUPERSEDED docs retain training-attachment FK; deletion blocked. |
| FS-TRAIN-04 | URS-TRAIN-04 | Per-doc-type `training_impact_flag`; transitions surface training-cycle estimate. |
| FS-TRAIN-05 | URS-TRAIN-05 | KPI report `vlp_rpt_training_kpi` per audience produced quarterly. |

### 4.7 Periodic Review Automation (URS § 5.7)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PRA-01 | URS-PRA-01 | Periodic-review scheduler `vlp_pr_scheduler` reads per-doc-type cadence; creates review tasks at D-30 / D-7 / D-0. |
| FS-PRA-02 | URS-PRA-02 | Past grace window creates eQMS deviation via `POST /api/v2/deviations`; category `EDMS_PR_OVERDUE`. |
| FS-PRA-03 | URS-PRA-03 | Periodic-review outcome enum (no-change / minor / major) routes to MasterControl CR workflow. |
| FS-PRA-04 | URS-PRA-04 | Dashboard `vlp_dashboard_pr` surfaces upcoming / overdue per doc-type. |

### 4.8 Audit-Trail Review Tools (URS § 5.8)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Vault audit-trail captures state transitions, content changes, metadata edits, security changes, user-access events. |
| FS-AUD-02 | URS-AUD-02 | Append-only at Veeva DB layer; CSV + PDF export. |
| FS-AUD-03 | URS-AUD-03 | Monthly Document-Coordinator review + quarterly QA review; evidence retained ≥ 25 y. |
| FS-AUD-04 | URS-AUD-04 | Retention 25 y post-retirement via Vault retention policy `vlp_ret_25y`. |
| FS-AUD-05 | URS-AUD-05 | Focused review tool `VLP-AUD-FOCUSED-v3` filters to material events (signatures, naming-overrides, OCR finalisations, redaction ops, mass deletions, role-permission edits). |
| FS-AUD-06 | URS-AUD-06 | Export to S3 Object-Lock with SHA-256 manifest. |

### 4.9 21 CFR Part 11 / Annex 11 (URS § 5.9)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural controls in `VLP-SOP-CSV-01`. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(b): PDF/A-3 + CSV exports validated by OQ-INSPECTION-COPY-01. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(d): Okta SAML 2.0 + MFA enforced. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.50: printed name + ts + meaning captured at signature. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.70: HMAC-SHA256 over doc-hash + signer-id + ts; tamper invalidates. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.100: uniqueness via Okta-Vault provisioning constraint. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.200: Okta fresh-token re-auth max-age 5 min at signature. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.300: Okta password policy enforced. |
| FS-ANX11-01 | URS-ANX11-01 | Validation evidence inventory in `VLP-VAL-EVID-INDEX`. |
| FS-ANX11-02 | URS-ANX11-02 | Accuracy checks on metadata entries: enum / range / format / required. |

### 4.10 Legacy Paper OCR Workflow (URS § 5.10)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-OCR-01 | URS-OCR-01 | OCR pipeline `vlp-ocr-svc` records operator + batch-id + scan-device + scan-ts + OCR-engine + version into `vlp_ocr_event`. |
| FS-OCR-02 | URS-OCR-02 | OCR-Verifier QA workflow `vlp_wf_ocr_verify` requires per-page comparison vs original before promotion to EFFECTIVE. |
| FS-OCR-03 | URS-OCR-03 | SoD via Vault security groups: `OCR-Operator` ≠ `OCR-Verifier`. |
| FS-OCR-04 | URS-OCR-04 | Confidence threshold (default 95%) configured per doc-type; below threshold forces manual-verify step. |
| FS-OCR-05 | URS-OCR-05 | Original-paper retention per `VLP-RET-PAPER`; link stored in `vlp_doc.original_paper_ref`. |

### 4.11 Inspection Redaction Mode (URS § 5.11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RED-01 | URS-RED-01 | Inspection Redactor role + service `vlp-redact-svc` produces redacted copies without modifying source; output stored in `vlp_inspection_copies`. |
| FS-RED-02 | URS-RED-02 | Watermark "INSPECTION COPY — REDACTED — *date*" + audit-trail entry for every redaction operation. |
| FS-RED-03 | URS-RED-03 | Redaction is destructive (rasterised + flattened); reversibility prevented by PDF burn-in; source unaffected. |
| FS-RED-04 | URS-RED-04 | Bulk-redaction restricted to `Inspection-Redactor` + `Vault-Admin`; surfaces in focused audit-trail-review tool. |

### 4.12 Document Search and Retrieval (URS § 5.12)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SEARCH-01 | URS-SEARCH-01 | Vault full-text + structured-field search with RBAC filter. |
| FS-SEARCH-02 | URS-SEARCH-02 | Inspection-retrieval SLA enforced via priority queue `vlp_inspection_queue`; metrics dashboard tracks SLA breaches. |
| FS-SEARCH-03 | URS-SEARCH-03 | Search-result columns include doc-type, lifecycle, effective-date, naming-conv-OK, periodic-review-due. |
| FS-SEARCH-04 | URS-SEARCH-04 | Saved-query persistence + CSV export via `vlp_search_export`. |

### 4.13 Multi-Site Federation (URS § 5.13)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-FED-01 | URS-FED-01 | Veeva cross-domain federation: EMEA-primary for SOPs/QM; NA-primary for FDA-submission-support; APAC-primary for region-specific items. |
| FS-FED-02 | URS-FED-02 | Cross-region links preserve source-region audit trail via `vlp_fed_link`. |

### 4.14 Integrations (URS § 5.14)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | MasterControl CR-id resolver `IF-EQMS-CR`; monthly reconciliation reports broken refs. |
| FS-INT-LMS-01 | URS-INT-LMS-01 | Cornerstone task push via `IF-LMS-TASK-PUSH`; idempotency key `vault:doc:<id>:ver:<version>`. |
| FS-INT-LMS-02 | URS-INT-LMS-02 | Gate FS-TRAIN-02 enforces. |
| FS-INT-PASX-01 | URS-INT-PASX-01 | PAS-X URN resolver `IF-PASX-URN`; failures alert within 5 min. |
| FS-INT-OCR-01 | URS-INT-OCR-01 | OCR pipeline REST `POST /api/v1/edms/ocr-ingest`; operator + verifier metadata. |
| FS-INT-SSO-01 | URS-INT-SSO-01 | Okta SAML 2.0 + MFA. |

### 4.15 Data Integrity (URS § 5.15)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | **Attributable:** `actor_id` not-null. |
| FS-DI-02 | URS-DI-02 | **Legible:** PDF/A-3 export with embedded fonts. |
| FS-DI-03 | URS-DI-03 | **Contemporaneous:** Veeva NTP-synced timestamps. |
| FS-DI-04 | URS-DI-04 | **Original:** content preserved; renditions reference only. |
| FS-DI-05 | URS-DI-05 | **Accurate:** workflow logic validated under OQ. |
| FS-DI-06 | URS-DI-06 | **Complete / Consistent / Enduring / Available:** retention 25y; ≤ 4 h retrieval. |

### 4.16 Backup / DR (URS § 5.16)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BAK-01 | URS-BAK-01 | Veeva-managed backup; vendor RPO ≤ 4 h / RTO ≤ 24 h verified annually via `VLP-VND-RUNBOOK`. |
| FS-BAK-02 | URS-BAK-02 | Annual config-export script `vlp-config-export.sh` archives doc-types, lifecycles, security profiles, naming rules. |

### 4.17 Performance / Security (URS § 5.17)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | Open/search P95 ≤ 3 s; monitored via Veeva performance dashboard. |
| FS-PERF-02 | URS-PERF-02 | Bulk import (≥ 1k docs) handled by `vlp-bulk-importer` with progress reporting in 4 h SLA. |
| FS-AV-01 | URS-AV-01 | Vendor SLA ≥ 99.7%. |
| FS-SEC-01 | URS-SEC-01 | Okta SSO + MFA; break-glass `VLP-VAULT-BREAKGLASS` documented + audited monthly. |
| FS-SEC-02 | URS-SEC-02 | Download watermark applied via rendition profile; bulk-export off by default. |
| FS-SEC-03 | URS-SEC-03 | Bulk-export events tagged `BULK_EXPORT` in audit trail; surfaced in focused review. |

### 4.18 Training and Periodic Review (URS § 5.18)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Cornerstone curriculum `VLP-CURR-EDMS-USER`. |
| FS-TRN-02 | URS-TRN-02 | Advanced inspection-readiness training `VLP-CURR-INSPECTION` for OCR Verifier + Inspection Redactor. |
| FS-PR-01 | URS-PR-01 | Annual periodic-review template `VLP-PR-EDMS-YYYYMMDD`. |


### 4.19 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: SAML 2.0 via Entra ID with SCIM lifecycle provisioning. Conditional-access binding to policy `Quality-App Conditional Access (MFA + device-compliance for controlled-document e-signature)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the Vault metadata DB plus object-replica for controlled-document binaries; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.20 Cross-System Integration — Helios handover (M-XINT-HEL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HEL-01 | URS-XINT-HEL-01 | Audit-event publisher emits Kafka topic `helios.ingest.vellis.vault.v1` with schema-registry-pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`; at-least-once delivery; idempotency key `{source_system, event_id}`; back-pressure surfaced via Prometheus `helios_publish_lag_seconds` with 5-min alert at > 600 s. |
| FS-XINT-HEL-02 | URS-XINT-HEL-02 | Local audit-store retention policy enforces ≥ 25 y; Helios ack persisted as `helios_ack_ts` per event; periodic reconciliation job verifies parity (Helios row count == local published count) and raises a deviation in MasterControl on > 0.01% mismatch over a 24 h window. |

## 5. Interface Specifications

| IF ID | URS ID | Counterparty | Protocol | Direction | Notes |
|---|---|---|---|---|---|
| IF-OKTA-01 | URS-INT-SSO-01 | Okta | SAML 2.0 | bidirectional | SSO + MFA |
| IF-EQMS-CR | URS-INT-EQMS-01 | MasterControl | REST | bidirectional | CR-id resolution |
| IF-LMS-TASK-PUSH | URS-INT-LMS-01 | Cornerstone | REST | outbound | training task creation; idempotent |
| IF-PASX-URN | URS-INT-PASX-01 | PAS-X | REST | outbound | URN resolution |
| IF-OCR-IN | URS-INT-OCR-01 | OCR Pipeline | REST | inbound | operator + verifier metadata |

## 6. Configuration Items (CI)

| CI ID | Item | Value |
|---|---|---|
| CI-01 | Document types | SOP, WI, MBR, VP, VR, QM, RA, Spec, Form, Policy |
| CI-02 | Periodic review cadence (default) | SOP 24m / WI 24m / MBR 12m / QM 36m / Policy 36m |
| CI-03 | Effective-date training gate | required for training-impact flag |
| CI-04 | Naming-convention regex per type | per `vlp-naming-engine.yaml` |
| CI-05 | OCR confidence threshold | 95% |
| CI-06 | Inspection-retrieval SLA | 4 h |
| CI-07 | Audit retention | 25 y |
| CI-08 | Bulk-export role | `Vault-Admin` |
| CI-09 | URN resolution cache TTL | 24 h on consumer side |
| CI-10 | Inspection-copy watermark | "INSPECTION COPY — REDACTED — *date*" |

## 7. Risks (FS-level)

- URN resolution gap causing consumer outage → FS-INT-PASX-01 cache + 5-min alert.
- Training not completed before EFFECTIVE → FS-TRAIN-02 gate.
- Naming-convention drift → FS-DT-04 regex enforcement at create.
- OCR finalisation without QA → FS-OCR-02..03 SoD.
- Redaction reversibility → FS-RED-03 rasterise+flatten.
- Inspection retrieval breach → FS-SEARCH-02 priority queue.
- Audit-trail tampering on Veeva side → vendor dependency tracked in `VLP-VND-REG`.

## 8. References

- VLP-URS-EDMS-001 v1.0
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- EU GMP Annex 11 §§ 4, 6, 9, 11
- ICH Q10; ISO 9001:2015 §7.5; ISO 13485:2016 §§ 4.2.4, 4.2.5
- ISPE GAMP 5 (2nd ed., 2022) + GPG: Records & Data Integrity
- PIC/S PI 041; ISO/IEC 27001:2022
- Veeva — *Vault QualityDocs 24R3 / 25R1 Configuration Reference*

## 9. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-VND-01 | FS-VND-01 |
| URS-VND-02 | FS-VND-02 |
| URS-VND-03 | FS-VND-03 |
| URS-VND-04 | FS-VND-04 |
| URS-LC-01 | FS-LC-01 |
| URS-LC-02 | FS-LC-02 |
| URS-LC-03 | FS-LC-03 |
| URS-LC-04 | FS-LC-04 |
| URS-LC-05 | FS-LC-05 |
| URS-LC-06 | FS-LC-06 |
| URS-DT-01 | FS-DT-01 |
| URS-DT-02 | FS-DT-02 |
| URS-DT-03 | FS-DT-03 |
| URS-DT-04 | FS-DT-04 |
| URS-DT-05 | FS-DT-05 |
| URS-WF-01 | FS-WF-01 |
| URS-WF-02 | FS-WF-02 |
| URS-WF-03 | FS-WF-03 |
| URS-WF-04 | FS-WF-04 |
| URS-WF-05 | FS-WF-05 |
| URS-WF-06 | FS-WF-06 |
| URS-REND-01 | FS-REND-01 |
| URS-REND-02 | FS-REND-02 |
| URS-REND-03 | FS-REND-03 |
| URS-REND-04 | FS-REND-04 |
| URS-REND-05 | FS-REND-05 |
| URS-TRAIN-01 | FS-TRAIN-01 |
| URS-TRAIN-02 | FS-TRAIN-02 |
| URS-TRAIN-03 | FS-TRAIN-03 |
| URS-TRAIN-04 | FS-TRAIN-04 |
| URS-TRAIN-05 | FS-TRAIN-05 |
| URS-PRA-01 | FS-PRA-01 |
| URS-PRA-02 | FS-PRA-02 |
| URS-PRA-03 | FS-PRA-03 |
| URS-PRA-04 | FS-PRA-04 |
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
| URS-ANX11-01 | FS-ANX11-01 |
| URS-ANX11-02 | FS-ANX11-02 |
| URS-OCR-01 | FS-OCR-01 |
| URS-OCR-02 | FS-OCR-02 |
| URS-OCR-03 | FS-OCR-03 |
| URS-OCR-04 | FS-OCR-04 |
| URS-OCR-05 | FS-OCR-05 |
| URS-RED-01 | FS-RED-01 |
| URS-RED-02 | FS-RED-02 |
| URS-RED-03 | FS-RED-03 |
| URS-RED-04 | FS-RED-04 |
| URS-SEARCH-01 | FS-SEARCH-01 |
| URS-SEARCH-02 | FS-SEARCH-02 |
| URS-SEARCH-03 | FS-SEARCH-03 |
| URS-SEARCH-04 | FS-SEARCH-04 |
| URS-FED-01 | FS-FED-01 |
| URS-FED-02 | FS-FED-02 |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 |
| URS-INT-LMS-01 | FS-INT-LMS-01 |
| URS-INT-LMS-02 | FS-INT-LMS-02 |
| URS-INT-PASX-01 | FS-INT-PASX-01 |
| URS-INT-OCR-01 | FS-INT-OCR-01 |
| URS-INT-SSO-01 | FS-INT-SSO-01 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-AV-01 | FS-AV-01 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-HEL-01 | FS-XINT-HEL-01 |
| URS-XINT-HEL-02 | FS-XINT-HEL-02 |

## 10. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Vault Release silently changes a configuration-affecting feature | Medium | Medium | URS-VND-02 |
| R-02 | SAML token compromise | Medium | High | URS-INT-SSO-01 |
| R-03 | Approver bypass via misconfigured security profile | Medium | High | URS-LC-02 + OQ |
| R-04 | LMS task bypass | Medium | High | URS-INT-LMS-02 |
| R-05 | Audit-trail tampering on Veeva side (vendor-assurance dependency) | Low | Critical | URS-VND-01 + URS-AUD-02 |
| R-06 | OCR ingestion finalised without QA second-pass | Low | High | URS-OCR-02..03 |
| R-07 | Inspection redaction reversible | Low | Critical | URS-RED-03 |
| R-08 | Periodic review missed | Medium | High | URS-PRA-01..02 |
| R-09 | Naming-convention drift | Medium | Medium | URS-DT-04 |
| R-10 | Training-record orphaned at supersede | Low | Medium | URS-TRAIN-03 |
| R-11 | Inspection retrieval > 4 h SLA breach | Low | High | URS-SEARCH-02 |
| R-12 | Master Batch Record URN-resolution failure breaks PAS-X | Low | High | URS-INT-PASX-01 |

Full evaluation in `VLP-RA-EDMS-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
