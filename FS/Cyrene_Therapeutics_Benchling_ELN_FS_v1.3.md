---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (T3 catch-up: per-ID rows; study/experiment lifecycle; schema versioning; mode separation; witness SoD; GitHub commit link)"
seed_corpus_basis:
  - "CYR-URS-ELN-001 v1.0 (parent URS, T3)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 SaaS conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11"
  - "ICH Q9(R1); ICH Q10"
parent_urs:
  document_number: CYR-URS-ELN-001
  version: 1.0
  file: ../../URS/_generated/final/ELN_Electronic_Lab_Notebook__Cyrene_Therapeutics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## ELN — Benchling for Biotech R&D 2025 — Platform-Level Configuration

**Document Number:** CYR-FS-ELN-001
**Version:** 1.1
**Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** CYR-URS-ELN-001 v1.0
**Site:** Cyrene Therapeutics Ltd., Cambridge, United Kingdom *(fictional)*
**System Owner:** Head of R&D Informatics
**System Class:** GAMP Cat 4 — Configured Product (multi-tenant SaaS)
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; ICH Q9(R1); ICH Q10

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of R&D Informatics) | _____________ | _____________ | _____ |
| Reviewer (Data Integrity Officer) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-12 | (synthetic) | T3 catch-up to URS v1.0 expanded: per-ID rows, study + experiment lifecycle, schema versioning, mode separation, witness SoD, GitHub commit link, focused audit-trail review. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

Specify Benchling 2025 platform-level configuration to satisfy `CYR-URS-ELN-001` v1.0 (T3).

## 2. Scope

Benchling tenancy, per-template configuration, Study + Experiment hierarchy, Schema versioning, Registry + Inventory + Workflow configuration; SSO via Okta + MFA; integrations with Vault QualityDocs, LIMS, eQMS, GitHub.

## 3. System Architecture

```
                Okta SSO + MFA
                    │
                    ▼
   ┌──────────────────────────────────────────────┐
   │     Benchling 2025 (Cyrene tenancy)            │
   │   Studies / Experiments / Templates             │
   │   Schemas / Registry / Inventory / Workflows    │
   │   GMP-mode segregation                          │
   └─┬───────────┬──────────────┬──────────────┬───┘
     │           │              │              │
     ▼           ▼              ▼              ▼
   Vault       LIMS          eQMS           GitHub
   (controlled (sample-      (deviations)   (computational
    docs)       result link)                 protocols)
```

| ID | Component | GAMP Cat |
|---|---|---|
| C-01 | Benchling tenancy (Cyrene) | 4 |
| C-02 | Okta IdP | (infra) |
| C-03 | Vault QualityDocs | 4 |
| C-04 | LabWare LIMS 8 | 4 |
| C-05 | MasterControl eQMS | 4 |
| C-06 | GitHub Enterprise | 3 |

## 4. Functional Specifications

### 4.1 Vendor Assurance (URS § 5.1)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VND-01 | URS-VND-01 | Benchling qualified as critical SaaS vendor — SOC 2 Type II + ISO 27001 + customer-shared CSV summary + BAA tracked in Vendor Quality Register. |
| FS-VND-02 | URS-VND-02 | Vendor-release evaluation runbook `CYR-RB-BENCHLING-REL`: read release notes within 14 days; classify configuration impact; re-validation tickets opened. |
| FS-VND-03 | URS-VND-03 | Quarterly SLA review via Benchling Trust portal; deviations escalated. |
| FS-VND-04 | URS-VND-04 | Vendor escalation runbook `CYR-RB-BENCHLING-ESCALATE` with named Benchling contacts. |

### 4.2 Study and Experiment Lifecycle (URS § 5.2)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-STUDY-01 | URS-STUDY-01 | Studies implemented as top-level Benchling Projects; `study.mode` enum [R&D, GMP] at creation; controlled-document URNs in `study.controlled_doc_refs`. |
| FS-STUDY-02 | URS-STUDY-02 | Mode-change workflow `wf_mode_change` requires GMP Mode Steward e-signature; legacy entries retain original mode flag; mode change forward-only. |
| FS-STUDY-03 | URS-STUDY-03 | Study dashboard `view_study_summary` aggregates entry counts by state, witness backlog, last-activity. |
| FS-EXP-01 | URS-EXP-01 | Experiments belong to exactly one study (FK constraint `experiment.study_id NOT NULL`); inherits `study.mode` and `controlled_doc_refs` at creation. |
| FS-EXP-02 | URS-EXP-02 | State machine `sm_experiment`: DRAFT → IN-PROGRESS → READY-FOR-WITNESS → READY-FOR-APPROVAL → APPROVED → LOCKED; reverse transitions require captured `reason` + signature. |
| FS-EXP-03 | URS-EXP-03 | Lock enforcement at DB layer: `experiment.locked = true` blocks UPDATE on entry fields except via amendment workflow. |
| FS-EXP-04 | URS-EXP-04 | Computational section schema `Computational_Protocol_v1` includes mandatory field `github_commit_sha` (40-char hex); embedded at signature via `wf_sign_capture_commit`. |

### 4.3 Schema and Template Registry (URS § 5.3)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SCHEMA-01 | URS-SCHEMA-01 | Benchling schema versioning native feature; entries bind to `schema_version_id`; prior versions retained. |
| FS-SCHEMA-02 | URS-SCHEMA-02 | Schema promotion workflow `wf_schema_promote` with Author ≠ Approver via AD groups `Schema-Author` vs `Schema-Approver`. |
| FS-SCHEMA-03 | URS-SCHEMA-03 | Required-field-changing schema PR labelled `breaking`; CI job opens impact-assessment ticket; manual migration plan required before merge. |
| FS-TPL-01 | URS-TPL-01 | Template lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE in Benchling Templates module; entry-create denies non-EFFECTIVE for GMP-mode studies. |
| FS-TPL-02 | URS-TPL-02 | Template promotion requires Author ≠ Approver e-signatures via `wf_template_promote`. |
| FS-TPL-03 | URS-TPL-03 | UAT scripts in `CYR-UAT-TPL/`; cover required-field, calc, attachment, witness, amendment. |
| FS-TPL-04 | URS-TPL-04 | Template versions retained; existing entries bound to creation-time version. |
| FS-TPL-05 | URS-TPL-05 | Template inventory view searchable by mode / schema-version / last-modified / effective-date. |

### 4.4 Entry Creation, Witness, Approval (URS § 5.4)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ENT-01 | URS-ENT-01 | GMP-tagged entry-create restricted to EFFECTIVE templates via Workflow rule `gmp_template_only`. |
| FS-ENT-02 | URS-ENT-02 | Entry schema captures creator + ts + Registry FK list + Inventory FK list + raw observations + calculations + attachments. |
| FS-ENT-03 | URS-ENT-03 | Critical entries (template flag `requires_witness = true`) gated by witness signature before approval. |
| FS-ENT-04 | URS-ENT-04 | Lab Lead approval requires re-auth via Okta; `wf_approve` denies self-witness. |
| FS-ENT-05 | URS-ENT-05 | Post-approval edit triggers `wf_unlock_amend` with justification ≥ 30 chars + re-approval. |
| FS-ENT-06 | URS-ENT-06 | SoD enforced at signature submission: `scientist_id ≠ witness_id ≠ approver_id` validation in `wf_sign_submit`. |
| FS-ENT-07 | URS-ENT-07 | Witness deadline per template `witness_deadline_hours`; overdue surfaces in Lab-Lead inbox + email digest. |
| FS-ENT-08 | URS-ENT-08 | One-click bulk-sign denied: signature requires per-entry view-event recorded in `wf_view_then_sign`. |

### 4.5 Registry and Inventory (URS § 5.5)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REG-01 | URS-REG-01 | Registry schemas: `DNA_v3`, `Protein_v2`, `Plasmid_v3`, `CellLine_v4`, `Antibody_v2` with mandatory metadata; uncurated entities blocked from GMP entries via `wf_use_registry`. |
| FS-REG-02 | URS-REG-02 | Registry provenance fields: `origin`, `donor`, `vendor`, `vendor_lot`, `parent_entity_fk`; readable from any consuming entry. |
| FS-REG-03 | URS-REG-03 | Deprecation workflow `wf_deprecate_registry`; deprecated entities surface warning when referenced. |
| FS-INV-01 | URS-INV-01 | Inventory items `Inventory_v2` schema: `lot_id`, `expiry_date`, `location`, `status`; decrement on entry-consume via `wf_consume_inventory`. |
| FS-INV-02 | URS-INV-02 | Block expired (`expiry_date < now`) or quarantined (`status = QUARANTINE`) consumption for GMP-mode entries. |
| FS-INV-03 | URS-INV-03 | Negative-inventory block at decrement-time via `wf_consume_inventory` precondition; manual adjustments audited. |

### 4.6 GMP vs R&D Mode Separation (URS § 5.6)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MODE-01 | URS-MODE-01 | Mode-aware template / schema selector: only mode-flagged templates surface for entry creation; audit + retention policy bound to mode. |
| FS-MODE-02 | URS-MODE-02 | `entry.mode` immutable after creation (DB constraint); cross-mode evidence transfer via `wf_create_gmp_from_rd` keeping source entry as reference. |
| FS-MODE-03 | URS-MODE-03 | GMP-mode entry-create rejects non-curated Registry + expired Inventory at validation. |
| FS-MODE-04 | URS-MODE-04 | Mode-mismatch detector compares `study.mode` to controlled-doc refs; surfaces warning needing Lab-Lead ack. |

### 4.7 Method Linkage (URS § 5.7)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-METH-01 | URS-METH-01 | LIMS sample-ID resolver via `IF-LIMS-RESOLVE`; result back-flow rendered read-only. |
| FS-METH-02 | URS-METH-02 | Vault URN resolver via `IF-VAULT-RESOLVE`; broken-ref check at approval. |
| FS-METH-03 | URS-METH-03 | Workflow `wf_check_referenced_doc_currency` runs at approval; superseded doc surfaces banner; Lab-Lead ack captured. |

### 4.8 Search and Indexing (URS § 5.8)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SEARCH-01 | URS-SEARCH-01 | Benchling search service with RBAC filter; full-text + structured-field. |
| FS-SEARCH-02 | URS-SEARCH-02 | Search results render mode / study / template-version / signature-state columns. |
| FS-SEARCH-03 | URS-SEARCH-03 | Saved queries persisted; export via `POST /api/v2/search/export` returns within 4 h. |

### 4.9 Audit Trail / Part 11 (URS § 5.9)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Benchling audit-trail captures entry / template / schema / Registry / Inventory / security events per § 11.10(e). |
| FS-AUD-02 | URS-AUD-02 | Append-only at Benchling DB layer; CSV + PDF export available. |
| FS-AUD-03 | URS-AUD-03 | Monthly audit-trail review by R&D Informatics + QA; per-entry review at approval; evidence retained ≥ 25 y. |
| FS-AUD-04 | URS-AUD-04 | Retention 25 y for GMP; 10 y for non-GxP; archived to S3 Object-Lock COMPLIANCE. |
| FS-AUD-05 | URS-AUD-05 | Focused-audit-trail-review tool `CYR-AUD-FOCUSED` filters to signatures, mode changes, schema changes, unlock-edits. |
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural controls in `CYR-SOP-CSV-01`. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(b): PDF/A-3 + CSV exports validated by `OQ-INSPECTION-COPY-01`. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(d): Okta SAML 2.0 + MFA. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.50: printed name + ts + meaning captured at every signature. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.70: HMAC-SHA256 over entry-hash + signer-id + ts; tamper invalidates. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.100: AD uniqueness constraint; reassignment blocked at provisioning. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.200: Okta re-auth (fresh token, max-age 5 min) at signature. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.300: Okta password policy aligned with site InfoSec (14 chars, complexity, 90d max-age). |
| FS-ANX11-01 | URS-ANX11-01 | Validation evidence in `CYR-VAL-EVID-INDEX`; kept current per periodic review. |
| FS-ANX11-02 | URS-ANX11-02 | Accuracy checks on numeric calc fields: range + format + plausibility per template. |

### 4.10 Integrations (URS § 5.10)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-VAULT-01 | URS-INT-VAULT-01 | Vault QualityDocs URN resolution; broken-ref flag at approval; `IF-VAULT-RESOLVE`. |
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | LIMS sample-ID linkage; read-only result back-flow; `IF-LIMS-RESOLVE`. |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | Deviation push via REST `POST /api/v2/deviations`; idempotency `eln:entry:<id>:deviation`. |
| FS-INT-GIT-01 | URS-INT-GIT-01 | GitHub API resolve of `github_commit_sha`; commit metadata embedded into entry on signature. |
| FS-INT-SSO-01 | URS-INT-SSO-01 | Okta SAML 2.0 + MFA. |

### 4.11 Data Integrity (URS § 5.11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | **Attributable:** `actor_id` not-null at audit-write. |
| FS-DI-02 | URS-DI-02 | **Legible:** PDF/A-3 + CSV / JSON export; rendering validated under OQ. |
| FS-DI-03 | URS-DI-03 | **Contemporaneous:** server-side NTP-synced timestamps; future/back-dating blocked. |
| FS-DI-04 | URS-DI-04 | **Original:** entry version preserved; amendment links to original; never overwrites. |
| FS-DI-05 | URS-DI-05 | **Accurate:** calculation cells validated under OQ. |
| FS-DI-06 | URS-DI-06 | **Complete / Consistent / Enduring / Available:** retrieval ≤ 4 h during inspection. |

### 4.12 Performance / Availability / Backup / Security (URS § 5.12)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | Open / save P95 ≤ 3 s under nominal load; monitored via Benchling Performance Insights. |
| FS-PERF-02 | URS-PERF-02 | Search P95 ≤ 2 s indexed; ≤ 5 s full-text. |
| FS-AV-01 | URS-AV-01 | Vendor SLA ≥ 99.7% tracked via Trust portal. |
| FS-BAK-01 | URS-BAK-01 | Vendor-managed backup; site verifies RPO ≤ 4 h / RTO ≤ 24 h annually. |
| FS-BAK-02 | URS-BAK-02 | Annual config export (templates, schemas, Registry, Inventory, security profiles). |
| FS-SEC-01 | URS-SEC-01 | Okta SSO + MFA enforced; no local Benchling accounts. |
| FS-SEC-02 | URS-SEC-02 | Project-level RBAC; cross-project visibility blocked unless explicitly granted. |
| FS-SEC-03 | URS-SEC-03 | GDPR / HIPAA BAA + DPA on file; minimisation guidance in `CYR-SOP-MINIMISE-PHI`. |
| FS-SEC-04 | URS-SEC-04 | Bulk-export of GMP entries restricted to `ELN-Admin`; logged + reviewed monthly. |

### 4.13 Training and Periodic Review (URS § 5.13)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Cornerstone curriculum `CYR-CURR-ELN-Scientist`; production access gated on completion. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher `CYR-CURR-ELN-Refresher-2026`. |
| FS-TRN-03 | URS-TRN-03 | Advanced data-integrity module mandatory for GMP-Mode-Steward + Schema-Approver. |
| FS-PR-01 | URS-PR-01 | Annual periodic-review template `CYR-PR-ELN-YYYYMMDD`; sign-off Head of R&D Informatics + VP QA. |


### 4.14 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: SAML 2.0 via Entra ID with SCIM lifecycle provisioning. Conditional-access binding to policy `R&D-App Conditional Access (MFA + device-compliance)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the Benchling tenant mirror; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.15 Cross-System Integration — Helios handover (M-XINT-HEL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HEL-01 | URS-XINT-HEL-01 | Audit-event publisher emits Kafka topic `helios.ingest.cyrene.benchling.v1` with schema-registry-pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`; at-least-once delivery; idempotency key `{source_system, event_id}`; back-pressure surfaced via Prometheus `helios_publish_lag_seconds` with 5-min alert at > 600 s. |
| FS-XINT-HEL-02 | URS-XINT-HEL-02 | Local audit-store retention policy enforces ≥ 25 y; Helios ack persisted as `helios_ack_ts` per event; periodic reconciliation job verifies parity (Helios row count == local published count) and raises a deviation in MasterControl on > 0.01% mismatch over a 24 h window. |

## 5. Interface Specifications

| IF ID | URS ID | Counterparty | Protocol | Direction | Notes |
|---|---|---|---|---|---|
| IF-OKTA-01 | URS-INT-SSO-01 | Okta | SAML 2.0 | bidirectional | SSO + MFA |
| IF-VAULT-RESOLVE | URS-INT-VAULT-01 | Vault QualityDocs | REST | outbound | URN resolution |
| IF-LIMS-RESOLVE | URS-INT-LIMS-01 | LabWare LIMS | REST | outbound | sample-ID resolution |
| IF-EQMS-DEV | URS-INT-EQMS-01 | MasterControl | REST | outbound | deviation push (idempotent) |
| IF-GIT-RESOLVE | URS-INT-GIT-01 | GitHub Enterprise | GitHub API | outbound | commit metadata fetch |

## 6. Configuration Items (CI)

| CI | Item | Value |
|---|---|---|
| CI-01 | Witness on critical entries | required (template flag) |
| CI-02 | Inventory expiry check | enforced |
| CI-03 | Template SoD | Author ≠ Approver |
| CI-04 | Schema SoD | Author ≠ Approver |
| CI-05 | Witness deadline default | 48 h |
| CI-06 | Audit retention (GMP) | 25 y |
| CI-07 | Audit retention (R&D) | 10 y |
| CI-08 | Bulk-export role | `ELN-Admin` |

## 7. Risks (FS-level)

- Template defect propagating to many entries → mitigation: FS-TPL-03 UAT scripts.
- GMP-tag misclassification → mitigation: FS-ENT-01 + FS-MODE-01..04.
- Witness bypass → mitigation: FS-ENT-03 + FS-ENT-06 SoD enforcement.
- Duplicate eQMS deviation → mitigation: FS-INT-EQMS-01 idempotency key.
- Schema migration corruption → mitigation: FS-SCHEMA-03 impact-assessment ticket.
- Audit-trail tampering on Benchling side → mitigation: vendor-assurance dependency + monthly review.

## 8. References

- CYR-URS-ELN-001 v1.0
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- EU GMP Annex 11 §§ 4, 6, 9, 11
- ICH Q9(R1), ICH Q10
- ISPE GAMP 5 (2nd ed., 2022) + GPG: A Risk-Based Approach to Compliant ELN
- PIC/S PI 041; ISO/IEC 27001:2022
- Benchling — *Biotech R&D 2025 Validation Approach + Release Notes 2025.x*

## 9. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-VND-01 | FS-VND-01 |
| URS-VND-02 | FS-VND-02 |
| URS-VND-03 | FS-VND-03 |
| URS-VND-04 | FS-VND-04 |
| URS-STUDY-01 | FS-STUDY-01 |
| URS-STUDY-02 | FS-STUDY-02 |
| URS-STUDY-03 | FS-STUDY-03 |
| URS-EXP-01 | FS-EXP-01 |
| URS-EXP-02 | FS-EXP-02 |
| URS-EXP-03 | FS-EXP-03 |
| URS-EXP-04 | FS-EXP-04 |
| URS-SCHEMA-01 | FS-SCHEMA-01 |
| URS-SCHEMA-02 | FS-SCHEMA-02 |
| URS-SCHEMA-03 | FS-SCHEMA-03 |
| URS-TPL-01 | FS-TPL-01 |
| URS-TPL-02 | FS-TPL-02 |
| URS-TPL-03 | FS-TPL-03 |
| URS-TPL-04 | FS-TPL-04 |
| URS-TPL-05 | FS-TPL-05 |
| URS-ENT-01 | FS-ENT-01 |
| URS-ENT-02 | FS-ENT-02 |
| URS-ENT-03 | FS-ENT-03 |
| URS-ENT-04 | FS-ENT-04 |
| URS-ENT-05 | FS-ENT-05 |
| URS-ENT-06 | FS-ENT-06 |
| URS-ENT-07 | FS-ENT-07 |
| URS-ENT-08 | FS-ENT-08 |
| URS-REG-01 | FS-REG-01 |
| URS-REG-02 | FS-REG-02 |
| URS-REG-03 | FS-REG-03 |
| URS-INV-01 | FS-INV-01 |
| URS-INV-02 | FS-INV-02 |
| URS-INV-03 | FS-INV-03 |
| URS-MODE-01 | FS-MODE-01 |
| URS-MODE-02 | FS-MODE-02 |
| URS-MODE-03 | FS-MODE-03 |
| URS-MODE-04 | FS-MODE-04 |
| URS-METH-01 | FS-METH-01 |
| URS-METH-02 | FS-METH-02 |
| URS-METH-03 | FS-METH-03 |
| URS-SEARCH-01 | FS-SEARCH-01 |
| URS-SEARCH-02 | FS-SEARCH-02 |
| URS-SEARCH-03 | FS-SEARCH-03 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
| URS-AUD-05 | FS-AUD-05 |
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
| URS-INT-VAULT-01 | FS-INT-VAULT-01 |
| URS-INT-LIMS-01 | FS-INT-LIMS-01 |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 |
| URS-INT-GIT-01 | FS-INT-GIT-01 |
| URS-INT-SSO-01 | FS-INT-SSO-01 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-AV-01 | FS-AV-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-TRN-03 | FS-TRN-03 |
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
| R-01 | Template defect propagating to many entries | Medium | Medium | URS-TPL-03 + UAT |
| R-02 | GMP-tag misclassification | Medium | High | URS-ENT-01 + URS-MODE-01..04 |
| R-03 | Witness-bypass | Medium | High | URS-ENT-03, URS-ENT-06 + role enforcement |
| R-04 | Idempotency failure causing duplicate eQMS deviations | Medium | Medium | URS-INT-EQMS-01 |
| R-05 | Vendor outage during a critical entry | Medium | High | URS-AV-01 + offline-capture procedure |
| R-06 | Schema change retroactively invalidating prior entries | Low | High | URS-SCHEMA-03 |
| R-07 | Registry-entity drift (e.g., cell line contamination) | Medium | High | URS-REG-02..03 |
| R-08 | Mode-change retroactively re-categorising entries | Low | High | URS-STUDY-02, URS-MODE-02 |

Full evaluation in `CYR-RA-ELN-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
