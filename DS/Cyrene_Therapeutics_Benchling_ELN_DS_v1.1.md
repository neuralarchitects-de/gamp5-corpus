---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (v1.0 DS corpus ship)"
seed_corpus_basis:
  - "CYR-FS-ELN-001 v1.1 (parent FS, T3 Cat 4)"
  - "CYR-URS-ELN-001 v1.0 (parent URS, transitive)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 Configuration Specification conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11"
  - "ICH Q9(R1); ICH Q10; PIC/S PI 041; ISO/IEC 27001:2022"
  - "Benchling Biotech R&D 2025 — Configuration Reference + Validation Approach"
parent_fs:
  document_number: CYR-FS-ELN-001
  version: "1.1"
  file: ../../../FS_FDS/_generated/final/Cyrene_Therapeutics_Benchling_ELN_FS_v1.3.md
parent_urs:
  document_number: CYR-URS-ELN-001
  version: "1.1"
  file: ../../../URS/_generated/final/ELN_Electronic_Lab_Notebook__Cyrene_Therapeutics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## ELN — Benchling for Biotech R&D 2025 — Cyrene Cambridge Tenancy

**Document Number:** CYR-DS-ELN-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** CYR-FS-ELN-001 v1.1
**Parent URS:** CYR-URS-ELN-001 v1.0
**Site:** Cyrene Therapeutics Ltd., Cambridge, United Kingdom *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Project Mode:** Greenfield-SaaS (Benchling tenancy + GMP-mode segregation)
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; ICH Q9(R1); ICH Q10

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Head of R&D Informatics) | _____________ | _____________ | _____ |
| Reviewer (QA Reviewer) | _____________ | _____________ | _____ |
| Reviewer (System Owner — Head of R&D) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — GMP-Mode Steward) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (Data Integrity Officer) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue. Inherited Tier T3 from parent URS+FS pair. DS covers 78/78 FS-IDs; 0 FS-IDs flagged as vendor-internal — no site design surface. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

| Term | Definition |
|---|---|
| CI | Configuration Item — one configurable parameter in Benchling 2025 |
| GMP-mode | Tenant-segregation flag enforcing curated-Registry + EFFECTIVE-template + witness gates |
| Registry | Benchling biological-entity registry (DNA, Protein, Plasmid, CellLine, Antibody) |
| Inventory | Benchling lot / location / status tracking module |
| Verified by | Planned IQ / OQ / PQ test that verifies the configuration choice |

## 1. Purpose

This Configuration Specification records the technical design of the Benchling 2025 multi-tenant SaaS tenancy at Cyrene, including per-template + per-schema configuration, Study + Experiment hierarchy, Registry + Inventory schemas, GMP / R&D mode segregation, and integration bindings to satisfy `CYR-FS-ELN-001` v1.1.

## 2. Scope

**In scope:** Benchling tenancy configuration (templates, schemas, workflows, Registry schemas, Inventory schemas, security profiles, AD groups, mode gates), integration bindings to Okta + Vault QualityDocs + LabWare LIMS + MasterControl eQMS + GitHub Enterprise, audit-trail review tool configuration.

**Out of scope:** Benchling vendor source-code internals; Okta vendor internals; LabWare LIMS internals (site DS `CTX-DS-LIMS-001` covers); MasterControl internals; GitHub Enterprise internals. Benchling is a Cat 4 system with no site-developed code in scope; no § 8 Cat-5 mini-SDS section is required.

## 3. Architectural Overview

The Cyrene Benchling tenant is configured with one project hierarchy per `study.mode` (R&D vs GMP), schema-versioned entries, and GMP-mode workflow gates. Identity is federated via Okta (SAML 2.0 + MFA + SCIM). Cross-system integrations are read-mostly outbound: Vault URN resolution, LIMS sample-ID resolution, eQMS deviation push, GitHub commit-SHA resolution.

```
                           ┌──────────────────────────────┐
                           │   Okta (SAML 2.0 + MFA + SCIM) │
                           └──────────────┬───────────────┘
                                          │
              ┌───────────────────────────▼────────────────────────────┐
              │  Benchling 2025 — Cyrene tenancy                       │
              │  ┌────────────────────────────────────────────────┐    │
              │  │ Studies (study.mode = R&D | GMP)              │    │
              │  │   └─ Experiments (inherits study.mode)         │    │
              │  │       └─ Entries (bound to schema_version_id)  │    │
              │  └────────────────────────────────────────────────┘    │
              │  ┌─────────────┐ ┌──────────┐ ┌──────────────────┐    │
              │  │ Templates    │ │ Schemas  │ │ Registry          │    │
              │  │ (lifecycle)  │ │ (versions)│ │  DNA/Protein/...   │    │
              │  └─────────────┘ └──────────┘ └──────────────────┘    │
              │  ┌──────────────┐ ┌──────────────────────────────┐    │
              │  │ Inventory     │ │ Audit-trail / GMP-mode gates │    │
              │  └──────────────┘ └──────────────────────────────┘    │
              └──┬────────────┬────────────┬─────────────┬────────────┘
                 │            │            │             │
                 ▼            ▼            ▼             ▼
            Vault         LabWare       MasterControl  GitHub Enterprise
            QualityDocs   LIMS 8        eQMS           (commit-SHA)
            (URN resolve) (sample-ID)   (deviation)
```

### 3.1 Topology rationale (text)

Benchling is vendor-hosted multi-tenant SaaS; the site design surface is entirely configuration. Mode segregation lives at the `study.mode` field with immutability after creation (DB constraint per FS-MODE-02); GMP entries bind to EFFECTIVE templates only, gated by the workflow rule `gmp_template_only`. Schema versioning is native Benchling; schema-breaking PRs are CI-labelled `breaking` and require a manual migration plan.

### 3.2 Component-design inventory

| Layer | Component | Vendor / source | Version | Site design surface |
|---|---|---|---|---|
| Application | Benchling tenancy (Cyrene) | Benchling | 2025 | Configuration (§ 4) |
| Identity | Okta | Okta | per site IT | Configuration (§ 4 + § 7) |
| Integration counterparty | Vault QualityDocs | Veeva | per Vellis Vault site | Bindings (§ 7) |
| Integration counterparty | LabWare LIMS 8 | LabWare | 8.0.4 | Bindings (§ 7) |
| Integration counterparty | MasterControl eQMS | MasterControl | QMS 2025 | Bindings (§ 7) |
| Integration counterparty | GitHub Enterprise | GitHub | per site IT | Bindings (§ 7) |

---

## 4. Configuration Specification

### 4.1 Vendor Assurance bindings

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VND-01 | Vendor-quality-register entry (`CYR-VND-REG.Benchling`) | SOC 2 Type II + ISO 27001 + CSV summary + BAA | Custom | Critical-vendor qualification | FS-VND-01 | OQ-VND-REG-01 |
| DS-VND-02 | Release-evaluation runbook (`CYR-RB-BENCHLING-REL`) | review ≤ 14 d; classify; CR for re-validation | Custom | Vendor-release cadence | FS-VND-02 | OQ-VND-REL-01 |
| DS-VND-03 | SLA review portal (`Benchling Trust portal`) | quarterly | Default | Vendor portal | FS-VND-03 | OQ-VND-SLA-01 |
| DS-VND-04 | Escalation runbook (`CYR-RB-BENCHLING-ESCALATE`) | named Benchling contacts | Custom | Operational escalation | FS-VND-04 | OQ-VND-ESCALATE-01 |

### 4.2 Study + Experiment Lifecycle CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-STUDY-01 | `study.mode` field (`STUDY_MODE_ENUM`) | `[R&D, GMP]`; mandatory at study creation | Custom | Tenant-segregation primary key | FS-STUDY-01 | OQ-STUDY-MODE-01 |
| DS-STUDY-02 | Controlled-doc URN field (`study.controlled_doc_refs[]`) | URN array; Vault-resolver-validated | Custom | Doc-binding traceability | FS-STUDY-01 | OQ-STUDY-DOC-REFS-01 |
| DS-STUDY-03 | Mode-change workflow (`wf_mode_change`) | requires GMP Mode Steward e-sig; forward-only | Custom | Anti-retroactive-recategorisation | FS-STUDY-02 | OQ-MODE-CHANGE-01 |
| DS-STUDY-04 | Study dashboard (`view_study_summary`) | aggregates entry counts by state, witness backlog, last-activity | Custom | Operational visibility | FS-STUDY-03 | PQ-STUDY-DASH-01 |
| DS-EXP-01 | Experiment study FK (`experiment.study_id`) | NOT NULL | Custom | Hierarchy enforcement | FS-EXP-01 | OQ-EXP-FK-01 |
| DS-EXP-02 | Experiment-state machine id (`sm_experiment`) | `DRAFT → IN-PROGRESS → READY-FOR-WITNESS → READY-FOR-APPROVAL → APPROVED → LOCKED` | Custom | 6-state lifecycle | FS-EXP-02 | OQ-EXP-STATES-01 |
| DS-EXP-03 | Reverse-transition gate | reason + signature mandatory | Custom | Audit-trail completeness | FS-EXP-02 | OQ-EXP-REVERSE-01 |
| DS-EXP-04 | Lock enforcement (`experiment.locked`) | DB-level block on UPDATE of entry fields when true | Custom | Tamper-protection | FS-EXP-03 | OQ-EXP-LOCK-01 |
| DS-EXP-05 | Computational-protocol schema (`Computational_Protocol_v1`) | mandatory `github_commit_sha` (40-char hex) | Custom | Reproducibility | FS-EXP-04 | OQ-COMP-PROTO-01 |
| DS-EXP-06 | Commit-capture workflow (`wf_sign_capture_commit`) | embeds commit metadata at signature | Custom | Provenance pinning | FS-EXP-04 | OQ-SIGN-COMMIT-01 |

### 4.3 Schema + Template Registry CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-SCHEMA-01 | Schema versioning (`schema_version_id`) | native Benchling feature enabled | Default | Native versioning | FS-SCHEMA-01 | OQ-SCHEMA-VER-01 |
| DS-SCHEMA-02 | Schema-promotion workflow (`wf_schema_promote`) | Author ≠ Approver | Custom | SoD | FS-SCHEMA-02 | OQ-SCHEMA-SOD-01 |
| DS-SCHEMA-03 | Schema AD groups (`Schema-Author`, `Schema-Approver`) | exclusive membership | Custom | SoD enforcement | FS-SCHEMA-02 | OQ-SCHEMA-AD-01 |
| DS-SCHEMA-04 | Breaking-PR label (`breaking`) | CI job opens impact-assessment ticket; manual migration plan required | Custom | Migration discipline | FS-SCHEMA-03 | OQ-SCHEMA-BREAK-01 |
| DS-TPL-01 | Template lifecycle states | `DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE` | Custom | 5-state per FS-TPL-01 | FS-TPL-01 | OQ-TPL-STATES-01 |
| DS-TPL-02 | GMP-mode template gate (`gmp_template_only`) | denies non-EFFECTIVE for GMP entries | Custom | GMP integrity | FS-TPL-01 | OQ-TPL-GMP-GATE-01 |
| DS-TPL-03 | Template-promotion workflow (`wf_template_promote`) | Author ≠ Approver e-sig | Custom | SoD | FS-TPL-02 | OQ-TPL-SOD-01 |
| DS-TPL-04 | Template UAT script folder (`CYR-UAT-TPL/`) | covers required-field, calc, attachment, witness, amendment | Custom | UAT coverage | FS-TPL-03 | PQ-TPL-UAT-01 |
| DS-TPL-05 | Template-version-pinning rule | entries bind to creation-time version | Custom | Retrospective integrity | FS-TPL-04 | OQ-TPL-VER-PIN-01 |
| DS-TPL-06 | Template inventory view | searchable by mode/schema/last-modified/effective-date | Custom | Operational search | FS-TPL-05 | OQ-TPL-INVENTORY-01 |

### 4.4 Entry, Witness, Approval CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ENT-01 | GMP entry-create gate | enforced via `gmp_template_only` workflow rule | Custom | GMP discipline | FS-ENT-01 | OQ-ENT-GMP-GATE-01 |
| DS-ENT-02 | Entry schema fields | creator + ts + Registry FK list + Inventory FK list + raw observations + calculations + attachments | Custom | Required-field schema | FS-ENT-02 | OQ-ENT-SCHEMA-01 |
| DS-ENT-03 | Witness flag (`template.requires_witness`) | boolean per template | Custom | Critical-entry gate | FS-ENT-03 | OQ-WITNESS-FLAG-01 |
| DS-ENT-04 | Witness-required gate workflow | blocks approval until witness sig present | Custom | SoD | FS-ENT-03 | OQ-WITNESS-GATE-01 |
| DS-ENT-05 | Lab Lead re-auth workflow (`wf_approve`) | Okta re-auth (5 min); denies self-witness | Custom | Part 11 § 11.200 | FS-ENT-04 | OQ-APPROVE-REAUTH-01 |
| DS-ENT-06 | Post-approval edit workflow (`wf_unlock_amend`) | justification ≥ 30 chars; re-approval | Custom | Audit-trail discipline | FS-ENT-05 | OQ-AMEND-01 |
| DS-ENT-07 | SoD enforcement (`wf_sign_submit`) | `scientist_id ≠ witness_id ≠ approver_id` | Custom | Triple-distinct rule | FS-ENT-06 | OQ-SOD-TRIPLE-01 |
| DS-ENT-08 | Witness deadline (`template.witness_deadline_hours`) | default 48 (CI-05); per-template override allowed | Default | Operational cadence | FS-ENT-07 | OQ-WITNESS-DEADLINE-01 |
| DS-ENT-09 | Witness inbox + email digest | Lab-Lead inbox + daily email digest | Default | Visibility | FS-ENT-07 | OQ-WITNESS-INBOX-01 |
| DS-ENT-10 | View-then-sign workflow (`wf_view_then_sign`) | per-entry view-event required before sig | Custom | Anti-bulk-sign | FS-ENT-08 | OQ-VIEW-THEN-SIGN-01 |

### 4.5 Registry + Inventory CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-REG-01 | Registry schemas | `DNA_v3, Protein_v2, Plasmid_v3, CellLine_v4, Antibody_v2` | Custom | Per-modality curation | FS-REG-01 | OQ-REG-SCHEMAS-01 |
| DS-REG-02 | Curation gate workflow (`wf_use_registry`) | blocks uncurated entities from GMP entries | Custom | GMP integrity | FS-REG-01 | OQ-REG-CURATION-01 |
| DS-REG-03 | Provenance fields (`origin, donor, vendor, vendor_lot, parent_entity_fk`) | mandatory at curation | Custom | Forensic traceability | FS-REG-02 | OQ-REG-PROV-01 |
| DS-REG-04 | Deprecation workflow (`wf_deprecate_registry`) | warning on referenced entities | Custom | Drift detection | FS-REG-03 | OQ-REG-DEPRECATE-01 |
| DS-INV-01 | Inventory schema (`Inventory_v2`) | `lot_id, expiry_date, location, status` | Custom | Tracking schema | FS-INV-01 | OQ-INV-SCHEMA-01 |
| DS-INV-02 | Consume workflow (`wf_consume_inventory`) | decrement on entry-consume | Custom | Live inventory | FS-INV-01 | OQ-INV-CONSUME-01 |
| DS-INV-03 | Expired/quarantined block | blocks consumption when `expiry_date < now` OR `status = QUARANTINE` (GMP-mode only) | Custom | GMP material integrity | FS-INV-02 | OQ-INV-EXPIRED-BLOCK-01 |
| DS-INV-04 | Negative-inventory block | precondition in `wf_consume_inventory`; manual adjustments audited | Custom | Stock integrity | FS-INV-03 | OQ-INV-NEG-BLOCK-01 |

### 4.6 GMP vs R&D Mode CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-MODE-01 | Mode-aware template selector | only mode-flagged templates surface for create | Custom | UI-level GMP integrity | FS-MODE-01 | OQ-MODE-SELECTOR-01 |
| DS-MODE-02 | Mode immutability (`entry.mode`) | DB constraint; immutable after creation | Custom | Anti-retroactive | FS-MODE-02 | OQ-MODE-IMMUT-01 |
| DS-MODE-03 | Cross-mode transfer workflow (`wf_create_gmp_from_rd`) | new GMP entry; source R&D retained as reference | Custom | Evidence bridge | FS-MODE-02 | OQ-CROSS-MODE-01 |
| DS-MODE-04 | GMP-create validation (`wf_gmp_create_validate`) | rejects non-curated Registry + expired Inventory | Custom | Integrity at create | FS-MODE-03 | OQ-GMP-CREATE-VAL-01 |
| DS-MODE-05 | Mode-mismatch detector | compares `study.mode` to controlled-doc refs; Lab-Lead ack | Custom | Drift detection | FS-MODE-04 | OQ-MODE-MISMATCH-01 |

### 4.7 Method Linkage CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-METH-01 | LIMS sample-ID resolver (`IF-LIMS-RESOLVE`) | REST outbound to LabWare LIMS 8 | Custom | Cross-system FK | FS-METH-01 | OQ-LIMS-RESOLVE-01 |
| DS-METH-02 | LIMS result-back-flow rendering | read-only; never editable in ELN | Custom | Source-of-truth | FS-METH-01 | OQ-LIMS-READONLY-01 |
| DS-METH-03 | Vault URN resolver (`IF-VAULT-RESOLVE`) | broken-ref check at approval | Custom | Doc-currency | FS-METH-02 | OQ-VAULT-RESOLVE-01 |
| DS-METH-04 | Doc-currency check workflow (`wf_check_referenced_doc_currency`) | runs at approval; superseded → banner + Lab-Lead ack | Custom | Currency enforcement | FS-METH-03 | OQ-DOC-CURRENCY-01 |

### 4.8 Search CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-SEARCH-01 | Benchling search service config | RBAC filter enabled; full-text + structured-field | Default | Native search | FS-SEARCH-01 | OQ-SEARCH-RBAC-01 |
| DS-SEARCH-02 | Search-result columns | `mode, study, template-version, signature-state` | Custom | Inspector-relevant | FS-SEARCH-02 | OQ-SEARCH-COLS-01 |
| DS-SEARCH-03 | Saved-query export endpoint (`POST /api/v2/search/export`) | returns within 4 h SLA | Default | Bulk export | FS-SEARCH-03 | OQ-SEARCH-EXPORT-01 |

### 4.9 Audit Trail / Part 11 CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUD-01 | Audit-trail coverage | entry / template / schema / Registry / Inventory / security events per § 11.10(e) | Default | Native trail | FS-AUD-01 | OQ-AUDIT-COVERAGE-01 |
| DS-AUD-02 | Append-only enforcement | Benchling DB-layer; CSV + PDF export | Default | Vendor-managed | FS-AUD-02 | OQ-AUDIT-APPEND-01 |
| DS-AUD-03 | Monthly review cadence | R&D Informatics + QA; per-entry review at approval; ≥ 25 y retention | Custom | Annex 11 § 9 | FS-AUD-03 | OQ-AUDIT-REVIEW-01 |
| DS-AUD-04 | Retention split (`AUDIT_RET_YEARS_GMP=25`, `AUDIT_RET_YEARS_RD=10`) | S3 Object Lock COMPLIANCE archive | Custom | Mode-aware retention | FS-AUD-04 | IQ-AUDIT-RET-01 |
| DS-AUD-05 | Focused-review tool (`CYR-AUD-FOCUSED`) | filters to signatures, mode changes, schema changes, unlock-edits | Custom | Reviewer efficiency | FS-AUD-05 | OQ-AUDIT-FOCUSED-01 |
| DS-PART11-01 | Procedural-control SOP id (`CYR-SOP-CSV-01`) | linked from system docs | Custom | § 11.10(a) | FS-PART11-01 | OQ-SOP-LINK-01 |
| DS-PART11-02 | Export formats | `PDF/A-3, CSV` | Custom | § 11.10(b) | FS-PART11-02 | OQ-INSPECTION-COPY-01 |
| DS-PART11-03 | IdP binding | Okta SAML 2.0 + MFA | Custom | § 11.10(d) | FS-PART11-03 | OQ-OKTA-MFA-01 |
| DS-PART11-04 | E-sig manifestation | `printedName + dateTime + meaning` | Default | § 11.50 | FS-PART11-04 | OQ-SIG-MANIFEST-01 |
| DS-PART11-05 | Signature binding | HMAC-SHA256 over entry-hash + signer-id + ts | Default | § 11.70 | FS-PART11-05 | OQ-SIG-BINDING-01 |
| DS-PART11-06 | Account uniqueness | AD uniqueness; reassignment blocked at provisioning | Custom | § 11.100 | FS-PART11-06 | OQ-ACCT-UNIQUE-01 |
| DS-PART11-07 | Re-auth max-age (`SIG_REAUTH_MAX_AGE_S`) | `300` (5 min) | Default | § 11.200 | FS-PART11-07 | OQ-SIG-REAUTH-01 |
| DS-PART11-08 | Password policy | length 14 + complexity + 90 d max-age | Custom | § 11.300 | FS-PART11-08 | OQ-PWD-POLICY-01 |
| DS-PART11-09 | Validation evidence index (`CYR-VAL-EVID-INDEX`) | per Annex 11 § 4 | Custom | Doc completeness | FS-ANX11-01 | OQ-VAL-EVID-IDX-01 |
| DS-PART11-10 | Accuracy-check rule (`AccuracyChecks`) | range + format + plausibility per template | Custom | Annex 11 § 6 | FS-ANX11-02 | OQ-ACCURACY-01 |

### 4.10 Integration CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-INT-VAULT-01 | Vault URN resolver endpoint (`IF-VAULT-RESOLVE`) | REST outbound; broken-ref flag at approval | Custom | Doc-currency | FS-INT-VAULT-01 | OQ-VAULT-RESOLVE-INT-01 |
| DS-INT-LIMS-01 | LIMS sample-ID resolver endpoint (`IF-LIMS-RESOLVE`) | REST outbound; read-only back-flow | Custom | Cross-system FK | FS-INT-LIMS-01 | OQ-LIMS-INT-01 |
| DS-INT-EQMS-01 | eQMS deviation endpoint | `POST /api/v2/deviations`; idempotency `eln:entry:<id>:deviation` | Custom | Idempotent push | FS-INT-EQMS-01 | OQ-EQMS-DEV-01 |
| DS-INT-GIT-01 | GitHub API resolver (`IF-GIT-RESOLVE`) | commit-metadata embed at signature | Custom | Reproducibility | FS-INT-GIT-01 | OQ-GIT-RESOLVE-01 |
| DS-INT-SSO-01 | Okta SAML 2.0 + MFA + SCIM | per realm `cyrene.okta.com` | Custom | Site IdP | FS-INT-SSO-01 | OQ-OKTA-SAML-01 |

### 4.11 Data Integrity CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-DI-01 | `actor_id` not-null | DB constraint at audit-write | Default | Attributable | FS-DI-01 | OQ-DI-ACTOR-01 |
| DS-DI-02 | Export rendering (PDF/A-3 + CSV/JSON) | OQ-validated | Custom | Legible | FS-DI-02 | OQ-DI-EXPORT-01 |
| DS-DI-03 | NTP-synced timestamps; future/back-dating blocked | server-side; site NTP source | Custom | Contemporaneous | FS-DI-03 | OQ-DI-NTP-01 |
| DS-DI-04 | Entry version preserved on amend | amendment links to original; never overwrites | Default | Original | FS-DI-04 | OQ-DI-VERSION-01 |
| DS-DI-05 | Calc-cell validation under OQ | per-template | Custom | Accurate | FS-DI-05 | OQ-DI-CALC-01 |
| DS-DI-06 | Retrieval SLA (≤ 4 h during inspection) | Vault QualityDocs + Benchling export tooling | Default | Available | FS-DI-06 | OQ-DI-RETRIEVE-01 |

### 4.12 Performance / Availability / Backup / Security CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PERF-01 | Open/save P95 threshold | ≤ 3 s nominal; monitored via Benchling Performance Insights | Custom | Vendor SLA | FS-PERF-01 | PQ-PERF-OPEN-01 |
| DS-PERF-02 | Search P95 threshold | ≤ 2 s indexed; ≤ 5 s full-text | Default | Vendor SLA | FS-PERF-02 | PQ-PERF-SEARCH-01 |
| DS-AV-01 | Vendor SLA target | ≥ 99.7% per Trust portal | Default | Vendor SLA | FS-AV-01 | OQ-AV-SLA-01 |
| DS-BAK-01 | Vendor-managed backup verification | annual site verification of RPO ≤ 4 h / RTO ≤ 24 h | Custom | Vendor-assurance dependency | FS-BAK-01 | PQ-BAK-VERIFY-01 |
| DS-BAK-02 | Annual config export | templates, schemas, Registry, Inventory, security profiles | Custom | Site-side config preservation | FS-BAK-02 | OQ-CONFIG-EXPORT-01 |
| DS-SEC-01 | Local Benchling accounts disabled | Okta SSO + MFA only | Custom | Single-source identity | FS-SEC-01 | OQ-LOCAL-ACCT-DISABLED-01 |
| DS-SEC-02 | Project-level RBAC | cross-project visibility blocked unless granted | Default | Need-to-know | FS-SEC-02 | OQ-PROJECT-RBAC-01 |
| DS-SEC-03 | GDPR/HIPAA controls | BAA + DPA on file; `CYR-SOP-MINIMISE-PHI` | Custom | Privacy compliance | FS-SEC-03 | OQ-PRIVACY-01 |
| DS-SEC-04 | Bulk-export role (`ELN-Admin`) | restricted; logged + monthly review | Custom | Anti-exfil | FS-SEC-04 | OQ-BULK-EXPORT-01 |

### 4.13 Training / Periodic Review CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-TRN-01 | Cornerstone curriculum (`CYR-CURR-ELN-Scientist`) | production-access gate | Custom | LMS binding | FS-TRN-01 | OQ-TRN-GATE-01 |
| DS-TRN-02 | Annual refresher (`CYR-CURR-ELN-Refresher-2026`) | Scientist + Lab Lead | Custom | Currency maintenance | FS-TRN-02 | PQ-TRN-REFRESH-01 |
| DS-TRN-03 | Advanced DI module | mandatory for GMP-Mode-Steward + Schema-Approver | Custom | Critical-role | FS-TRN-03 | OQ-DI-ADV-01 |
| DS-PR-01 | Annual periodic-review template (`CYR-PR-ELN-YYYYMMDD`) | Head R&D Informatics + VP QA sign-off | Custom | Annex 11 § 11 | FS-PR-01 | PQ-PR-ELN-01 |

### 4.14 Cross-System Bindings (M-XSYS)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-XSYS-AD-01 | Entra ID SAML 2.0 binding | SAML 2.0 via Entra ID with SCIM lifecycle | Custom | Per FS-XSYS-AD-01 | FS-XSYS-AD-01 | OQ-XSYS-AD-01 |
| DS-XSYS-AD-02 | Conditional-access policy id | `R&D-App Conditional Access (MFA + device-compliance)` | Custom | Policy reuse | FS-XSYS-AD-01 | OQ-CA-POLICY-01 |
| DS-XSYS-AD-03 | SIEM target (`Splunk gxp-authn`) | RFC 5424 syslog; ≤ 5 min lag | Custom | Cross-system correlation | FS-XSYS-AD-01 | OQ-SIEM-FWD-01 |
| DS-XSYS-AD-04 | CyberArk PAM binding | 24 h rotation + dual-witness check-out | Custom | Break-glass | FS-XSYS-AD-01 | OQ-PAM-01 |
| DS-XSYS-BAK-01 | Veeam VSS + pg_basebackup + WAL | T2 tier; RPO ≤ 24 h / RTO ≤ 24 BH | Custom | Per FS-XSYS-BAK-01 | FS-XSYS-BAK-01 | OQ-VEEAM-01 |
| DS-XSYS-BAK-02 | S3 Object Lock COMPLIANCE bucket | geo-replicated | Custom | Anti-ransom | FS-XSYS-BAK-01 | IQ-S3-OBJLOCK-01 |
| DS-XSYS-BAK-03 | LTO-9 air-gap rotation | monthly | Custom | Air-gap policy | FS-XSYS-BAK-01 | OQ-LTO9-01 |
| DS-XSYS-BAK-04 | Restore-cert retention | ≥ 25 y in eQMS | Custom | Quality-record discipline | FS-XSYS-BAK-01 | OQ-RESTORE-CERT-01 |
| DS-XINT-HEL-01 | Helios Kafka topic (`helios.ingest.cyrene.benchling.v1`) | idempotency `{source_system, event_id}` | Custom | Per FS-XINT-HEL-01 | FS-XINT-HEL-01 | OQ-HELIOS-PUB-01 |
| DS-XINT-HEL-02 | Helios lag alert (`HELIOS_LAG_ALERT_S=600`) | Prometheus | Custom | Back-pressure SLO | FS-XINT-HEL-01 | OQ-HELIOS-LAG-01 |
| DS-XINT-HEL-03 | Helios reconciliation cadence | daily 24 h window; > 0.01% mismatch raises eQMS deviation | Custom | Parity | FS-XINT-HEL-02 | OQ-HELIOS-RECON-01 |

---

## 5. Workflow + Business-Rule Design

### 5.1 Study + Experiment workflow (FS-STUDY-01, FS-EXP-01..04)

1. Study create: `study.mode` selected; `controlled_doc_refs[]` resolved via Vault.
2. Experiment create: inherits `study.mode`, `controlled_doc_refs[]`.
3. Entry create: gated by `gmp_template_only` (if GMP-mode) → EFFECTIVE template only.
4. Computational sections: `Computational_Protocol_v1` requires `github_commit_sha`; `wf_sign_capture_commit` embeds commit metadata at signature time.
5. Witness flow: per-entry view recorded in `wf_view_then_sign`; bulk-sign denied.
6. Lab-Lead approve: Okta re-auth ≤ 5 min; self-witness blocked.
7. Lock: experiment.locked = true blocks UPDATE on entry fields; amendments via `wf_unlock_amend`.

### 5.2 Mode-change workflow (FS-STUDY-02)

| Step | Actor | Gate |
|---|---|---|
| 1 | Study Owner | requests mode change via `wf_mode_change` |
| 2 | GMP Mode Steward | re-auth + e-sig; reason ≥ 50 chars |
| 3 | Workflow | applies mode-change forward-only; legacy entries retain original mode flag |
| 4 | Audit trail | row written with both old + new mode values |

### 5.3 Schema-promotion workflow (FS-SCHEMA-02..03)

| Step | Actor | Gate |
|---|---|---|
| 1 | Schema-Author | drafts schema PR |
| 2 | CI | labels `breaking` if required fields change; opens impact-assessment ticket |
| 3 | Schema-Reviewer | content review |
| 4 | Schema-Approver (≠ Author) | re-auth e-sig in `wf_schema_promote` |
| 5 | Manual migration plan | required before merge for breaking schemas |

### 5.4 Entry SoD rule (FS-ENT-06)

At `wf_sign_submit` time, the workflow rejects if `scientist_id == witness_id` OR `witness_id == approver_id` OR `scientist_id == approver_id`. Rejection returns structured error `SOD_TRIPLE_VIOLATION` to the UI.

### 5.5 GMP-create validation (FS-MODE-03)

When creating a GMP entry, the workflow `wf_gmp_create_validate` runs:
- Registry FK → checks `registry_entity.curation_state = CURATED` for every FK
- Inventory FK → checks `inventory.expiry_date >= now` AND `inventory.status != QUARANTINE`
- Failure → reject create with `GMP_CREATE_INTEGRITY_FAIL` and surfaced reasons

---

## 6. Role-Permission Matrix Design

| Role (AD group) | Study-Create | Mode-Change | Template-Author | Template-Approve | Schema-Author | Schema-Approve | Entry-Create | Entry-Witness | Entry-Approve | Entry-Amend | Bulk-Export | Audit-Review |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `ELN-Scientist` | – | – | – | – | – | – | R/W | – | – | – | – | – |
| `ELN-Lab-Lead` | R/W | – | – | – | – | – | R/W | – | R/W | – | – | – |
| `ELN-Witness` | – | – | – | – | – | – | – | R/W | – | – | – | – |
| `Template-Author` | – | – | R/W | – | – | – | – | – | – | – | – | – |
| `Template-Approver` | – | – | R | R/W | – | – | – | – | – | – | – | – |
| `Schema-Author` | – | – | – | – | R/W | – | – | – | – | – | – | – |
| `Schema-Approver` | – | – | – | – | R | R/W | – | – | – | – | – | – |
| `GMP-Mode-Steward` | R | R/W | – | – | – | – | – | – | – | – | – | – |
| `ELN-Admin` | R | – | – | – | – | – | – | – | – | – | R/W | – |
| `QA-Audit-Reviewer` | R | – | R | – | R | – | R | R | R | R | – | R/W |

SoD enforced at sig submission: `scientist_id ≠ witness_id ≠ approver_id`; `Schema-Author ∩ Schema-Approver = ∅`; `Template-Author ∩ Template-Approver = ∅`.

---

## 7. Integration Design

### 7.1 Vault URN resolver (FS-INT-VAULT-01)

- Endpoint: REST outbound `GET https://vault.vellis.local/api/v23.3/objects/documents__v/{urn}`
- AuthN: Vault session token; rotated 90 d
- Use: doc-currency check at entry-approval time; broken refs surface as `wf_check_referenced_doc_currency` warning + Lab-Lead ack
- Cache TTL: 1 h; cache invalidation on `wf_unlock_amend`

### 7.2 LIMS sample-ID resolver (FS-INT-LIMS-01)

- Endpoint: REST outbound `GET https://lims.caelum.local/api/lims/samples/{sample_id}`
- AuthN: service-account token from HashiCorp Vault `kv/eln/lims/*`
- Result back-flow: read-only rendering; never editable in ELN
- Cache TTL: 5 min

### 7.3 eQMS deviation push (FS-INT-EQMS-01)

- Endpoint: `POST https://eqms.talos.local/api/v2/deviations`
- AuthN: mTLS + bearer
- Idempotency: `eln:entry:<id>:deviation`
- Retry: exponential back-off (1 s, 2 s, 4 s, 8 s) up to 10 attempts; DLQ topic `eln.eqms.dev.dlq`

### 7.4 GitHub commit-SHA resolver (FS-INT-GIT-01)

- Endpoint: `GET https://github.cyrene.local/api/v3/repos/{org}/{repo}/commits/{sha}`
- AuthN: GitHub App installation token; rotated 1 h
- Embed: `commit_sha + commit_message + commit_ts + commit_author` into entry at signature
- Failure handling: if GitHub unreachable, signature workflow blocks with `GITHUB_RESOLVE_FAIL`; manual retry path

### 7.5 Okta SSO + MFA (FS-INT-SSO-01)

- Protocol: SAML 2.0 + SCIM 2.0 lifecycle
- MFA: TOTP / WebAuthn enforced at signature
- Re-auth max-age: 300 s (5 min)
- SCIM provisioning: joiner/mover/leaver via HR-system → Okta → Benchling

### 7.6 Helios audit-event handover (FS-XINT-HEL-01..02)

- Kafka topic: `helios.ingest.cyrene.benchling.v1`
- Schema: schema-registry pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`
- Delivery: at-least-once with `{source_system, event_id}` idempotency
- Reconciliation: daily; mismatch > 0.01% raises eQMS deviation

---

## 8. Site-Deployed Components Design

Benchling is operated as a pure Cat 4 SaaS at Cyrene — no site-developed code in scope. The cross-system integration adapters (Vault resolver, LIMS resolver, eQMS push, GitHub resolver) are realised entirely through Benchling's native connector configuration (`IF-VAULT-RESOLVE`, `IF-LIMS-RESOLVE`, `IF-EQMS-DEV`, `IF-GIT-RESOLVE`) and do not contain site-authored business logic. Therefore § 8 has no mini-SDS sub-sections to declare.

Should future site requirements introduce site-authored Benchling plugins or custom scripts inside the tenancy, those components escalate the system to a hybrid Cat 4 + Cat 5 per METHODOLOGY § 2B.4.6, and § 8 sub-sections will be added in a DS revision.

---

## 9. References

### US
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- GDPR Arts. 6, 32

### DACH
- BfArM (DE) — informational reference for entries in scope of DE-supervised studies
- Swissmedic (CH) — informational reference

### International
- ICH Q9(R1); ICH Q10
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE GAMP GPG *A Risk-Based Approach to Compliant ELN*
- PIC/S PI 041
- ISO/IEC 27001:2022

### Vendor
- Benchling — *Biotech R&D 2025 Configuration Reference*
- Benchling — *Validation Approach + Release Notes 2025.x*
- Okta — *SAML 2.0 + SCIM 2.0 Integration Reference*

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-VND-01 | FS-VND-01 |
| DS-VND-02 | FS-VND-02 |
| DS-VND-03 | FS-VND-03 |
| DS-VND-04 | FS-VND-04 |
| DS-STUDY-01 | FS-STUDY-01 |
| DS-STUDY-02 | FS-STUDY-01 |
| DS-STUDY-03 | FS-STUDY-02 |
| DS-STUDY-04 | FS-STUDY-03 |
| DS-EXP-01 | FS-EXP-01 |
| DS-EXP-02 | FS-EXP-02 |
| DS-EXP-03 | FS-EXP-02 |
| DS-EXP-04 | FS-EXP-03 |
| DS-EXP-05 | FS-EXP-04 |
| DS-EXP-06 | FS-EXP-04 |
| DS-SCHEMA-01 | FS-SCHEMA-01 |
| DS-SCHEMA-02 | FS-SCHEMA-02 |
| DS-SCHEMA-03 | FS-SCHEMA-02 |
| DS-SCHEMA-04 | FS-SCHEMA-03 |
| DS-TPL-01 | FS-TPL-01 |
| DS-TPL-02 | FS-TPL-01 |
| DS-TPL-03 | FS-TPL-02 |
| DS-TPL-04 | FS-TPL-03 |
| DS-TPL-05 | FS-TPL-04 |
| DS-TPL-06 | FS-TPL-05 |
| DS-ENT-01 | FS-ENT-01 |
| DS-ENT-02 | FS-ENT-02 |
| DS-ENT-03 | FS-ENT-03 |
| DS-ENT-04 | FS-ENT-03 |
| DS-ENT-05 | FS-ENT-04 |
| DS-ENT-06 | FS-ENT-05 |
| DS-ENT-07 | FS-ENT-06 |
| DS-ENT-08 | FS-ENT-07 |
| DS-ENT-09 | FS-ENT-07 |
| DS-ENT-10 | FS-ENT-08 |
| DS-REG-01 | FS-REG-01 |
| DS-REG-02 | FS-REG-01 |
| DS-REG-03 | FS-REG-02 |
| DS-REG-04 | FS-REG-03 |
| DS-INV-01 | FS-INV-01 |
| DS-INV-02 | FS-INV-01 |
| DS-INV-03 | FS-INV-02 |
| DS-INV-04 | FS-INV-03 |
| DS-MODE-01 | FS-MODE-01 |
| DS-MODE-02 | FS-MODE-02 |
| DS-MODE-03 | FS-MODE-02 |
| DS-MODE-04 | FS-MODE-03 |
| DS-MODE-05 | FS-MODE-04 |
| DS-METH-01 | FS-METH-01 |
| DS-METH-02 | FS-METH-01 |
| DS-METH-03 | FS-METH-02 |
| DS-METH-04 | FS-METH-03 |
| DS-SEARCH-01 | FS-SEARCH-01 |
| DS-SEARCH-02 | FS-SEARCH-02 |
| DS-SEARCH-03 | FS-SEARCH-03 |
| DS-AUD-01 | FS-AUD-01 |
| DS-AUD-02 | FS-AUD-02 |
| DS-AUD-03 | FS-AUD-03 |
| DS-AUD-04 | FS-AUD-04 |
| DS-AUD-05 | FS-AUD-05 |
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
| DS-INT-VAULT-01 | FS-INT-VAULT-01 |
| DS-INT-LIMS-01 | FS-INT-LIMS-01 |
| DS-INT-EQMS-01 | FS-INT-EQMS-01 |
| DS-INT-GIT-01 | FS-INT-GIT-01 |
| DS-INT-SSO-01 | FS-INT-SSO-01 |
| DS-DI-01 | FS-DI-01 |
| DS-DI-02 | FS-DI-02 |
| DS-DI-03 | FS-DI-03 |
| DS-DI-04 | FS-DI-04 |
| DS-DI-05 | FS-DI-05 |
| DS-DI-06 | FS-DI-06 |
| DS-PERF-01 | FS-PERF-01 |
| DS-PERF-02 | FS-PERF-02 |
| DS-AV-01 | FS-AV-01 |
| DS-BAK-01 | FS-BAK-01 |
| DS-BAK-02 | FS-BAK-02 |
| DS-SEC-01 | FS-SEC-01 |
| DS-SEC-02 | FS-SEC-02 |
| DS-SEC-03 | FS-SEC-03 |
| DS-SEC-04 | FS-SEC-04 |
| DS-TRN-01 | FS-TRN-01 |
| DS-TRN-02 | FS-TRN-02 |
| DS-TRN-03 | FS-TRN-03 |
| DS-PR-01 | FS-PR-01 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 |
| DS-XSYS-AD-02 | FS-XSYS-AD-01 |
| DS-XSYS-AD-03 | FS-XSYS-AD-01 |
| DS-XSYS-AD-04 | FS-XSYS-AD-01 |
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
| DR-01 | GMP-mode template list inadvertently includes a non-EFFECTIVE entry due to selector cache staleness | DS-MODE-01 + DS-TPL-02 | Low | High | OQ-MODE-SELECTOR-01 cache-invalidation test |
| DR-02 | Schema-promotion bypass — `Schema-Author` and `Schema-Approver` group memberships overlap due to AD provisioning defect | DS-SCHEMA-02 + DS-SCHEMA-03 | Low | High | Quarterly RBAC review (DS-SEC-02 vector) |
| DR-03 | Witness deadline overrides bypass | DS-ENT-08 | Low | Medium | Template-version review at promotion (FS-TPL-02) |
| DR-04 | Cross-mode transfer (`wf_create_gmp_from_rd`) inherits stale R&D data into GMP entry | DS-MODE-03 | Low | High | Validation at workflow entry; OQ-CROSS-MODE-01 |
| DR-05 | GitHub commit-SHA resolver outage blocks computational-section signature | DS-INT-GIT-01 | Medium | Medium | Manual retry path; Lab-Lead ack with documented reason |
| DR-06 | Vault URN resolver cache staleness misses recent doc supersede event | DS-INT-VAULT-01 | Low | High | Cache TTL 1 h; invalidation on amend |
| DR-07 | Benchling vendor release silently changes template-engine behaviour | DS-VND-02 + DS-TPL-04 | Medium | Medium | Release-eval runbook within 14 d; UAT regression |
| DR-08 | Registry-entity deprecation propagates a banner but does not block consumption | DS-REG-04 | Medium | Medium | Lab-Lead ack at deprecation; OQ-REG-DEPRECATE-01 |
| DR-09 | Inventory expiry-block bypass via manual adjustment audit-trail gap | DS-INV-04 | Low | High | Audit-trail review focused-tool (DS-AUD-05) |
| DR-10 | Schema-version pinning fails for entries created during a breaking-PR migration window | DS-SCHEMA-01 + DS-SCHEMA-04 | Low | High | Migration-plan gate at PR merge |
| DR-11 | Okta MFA fatigue drives users to re-auth without verification (token replay) | DS-PART11-07 | Low | High | Lockout policy (DS-PART11-08); UX monitoring |
| DR-12 | Audit-trail focused-review tool filter list goes stale as new event types ship in Benchling releases | DS-AUD-05 + DS-VND-02 | Medium | Medium | Vendor-release runbook review |
| DR-13 | Helios reconciliation false-positive raises noise deviations | DS-XINT-HEL-03 | Medium | Low | Tunable threshold; deviation suppression review |
| DR-14 | LIMS resolver permits ELN to display non-current LIMS result (read-only race) | DS-INT-LIMS-01 + DS-METH-02 | Low | Medium | Cache TTL 5 min; banner on stale results |
| DR-15 | SCIM leaver-event lag leaves orphaned active session on Benchling side | DS-INT-SSO-01 | Low | High | Session-timeout policy + Okta governance review |
| DR-16 | Local-account creation slips through despite SSO-only policy due to vendor admin-portal exception | DS-SEC-01 | Low | High | Quarterly Benchling-admin audit |
| DR-17 | Bulk-export role privilege creep adds non-`ELN-Admin` user accidentally | DS-SEC-04 | Low | High | Monthly review (DS-SEC-04 + DS-AUD-05) |
| DR-18 | Benchling tenancy region (EU) data-residency assumption breaks if vendor moves storage | DS-AV-01 + DS-SEC-03 | Low | High | DPA Annex II quarterly review + Trust portal monitoring |

The full formal Risk Assessment is `CYR-RA-ELN-001` (synthetic, separate document).

---

## 12. Appendix B — Mode-Segregation Design Narrative

### 12.1 Why mode segregation is the load-bearing design surface

Cyrene's R&D and GMP workstreams share one Benchling tenancy by deliberate design choice: discovery scientists collaborating with bioprocess-development engineers benefit hugely from a single Registry / Inventory / search surface. The price is that one shared substrate must enforce GxP-grade integrity on the GMP-mode subset without contaminating R&D flexibility. Every mode-segregation control in §§ 4–7 of this DS exists to satisfy that constraint.

### 12.2 Design-level invariants

| Invariant | Enforced by | Test reference |
|---|---|---|
| `entry.mode` immutable after creation | DS-MODE-02 DB constraint | OQ-MODE-IMMUT-01 |
| GMP-mode entry cannot reference uncurated Registry entity | DS-MODE-04 `wf_gmp_create_validate` | OQ-GMP-CREATE-VAL-01 |
| GMP-mode entry cannot consume expired or quarantined Inventory lot | DS-INV-03 + DS-MODE-04 | OQ-INV-EXPIRED-BLOCK-01 |
| Mode change is forward-only and audit-trail-anchored | DS-STUDY-03 `wf_mode_change` | OQ-MODE-CHANGE-01 |
| Cross-mode evidence transfer creates a new GMP entry referencing R&D source — never re-tagging | DS-MODE-03 `wf_create_gmp_from_rd` | OQ-CROSS-MODE-01 |
| GMP-mode template list shows EFFECTIVE-only | DS-TPL-02 `gmp_template_only` workflow rule | OQ-TPL-GMP-GATE-01 |
| Schema-breaking PR creates an impact-assessment ticket before merge | DS-SCHEMA-04 `breaking` CI label | OQ-SCHEMA-BREAK-01 |
| Schema-Author and Schema-Approver belong to disjoint AD groups | DS-SCHEMA-02 + DS-SCHEMA-03 | OQ-SCHEMA-SOD-01 |

### 12.3 GMP-mode entry-creation business rule (pseudocode)

```
def create_gmp_entry(study_id, template_id, registry_fks[], inventory_fks[]):
    study = get_study(study_id)
    assert study.mode == "GMP"                         # DS-MODE-01

    template = get_template(template_id)
    assert template.state == "EFFECTIVE"               # DS-TPL-02
    assert template.mode_flag == "GMP"                 # DS-MODE-01

    for fk in registry_fks:
        entity = get_registry_entity(fk)
        assert entity.curation_state == "CURATED"      # DS-REG-02

    for fk in inventory_fks:
        item = get_inventory(fk)
        assert item.expiry_date >= today               # DS-INV-03
        assert item.status != "QUARANTINE"             # DS-INV-03

    entry = Entry(
        mode="GMP",
        study_id=study_id,
        template_version=template.version,
        ...
    )
    persist(entry)
```

Any failure raises `GMP_CREATE_INTEGRITY_FAIL` with the specific failure list — surfaced to the user as actionable text, not a generic error.

### 12.4 Mode-change forward-only design intent

The `wf_mode_change` workflow accepts only `R&D → GMP` (never the reverse). Reverse changes would require re-categorising historical entries — an Annex 11 § 12 anti-pattern. Reverse cases (a study erroneously flagged as GMP that should never have been) are handled out-of-band by creating a new R&D study and explicitly orphaning the erroneous GMP study with a reason note; the audit trail preserves both sides.

### 12.5 Cross-mode evidence transfer pattern

Many bioprocess-development experiments produce data that becomes load-bearing for GMP manufacture (cell-line stability, reference-standard characterisation, etc.). The design choice is to surface that evidence in a new GMP entry that *references* the R&D source rather than re-tagging the R&D entry. This preserves the integrity of the R&D record and creates an explicit, audit-trailed re-use event in the GMP namespace.

### 12.6 Tenant-shared search RBAC implications

Project-level RBAC (DS-SEC-02) ensures that cross-project visibility is denied by default. GMP-mode entries are searchable only by members of the project that owns the entry plus explicitly-named QA-Audit-Reviewer roles. R&D scientists do not gain GMP visibility through search; GMP staff do not gain R&D visibility through search. This is the only way a shared Benchling tenancy preserves Annex 11 § 7.1 access-segregation despite the unified substrate.

### 12.7 GitHub commit-SHA capture — why computational reproducibility matters

Computational protocols (R-scripts, Python notebooks, bioinformatics pipelines) increasingly drive GMP-relevant decisions: cell-line characterisation, stability-trend analysis, release-spec derivation. Capturing the exact commit-SHA at signature time is the design choice that makes these computational artefacts auditable later. The capture workflow `wf_sign_capture_commit` (DS-EXP-06) fetches commit metadata via GitHub API and embeds it in the entry at signature.

Without commit-SHA capture, a signed entry referencing "the analysis from last Tuesday" is regulatorily worthless: the analysis can change without trace. With the 40-character hex commit-SHA embedded, any future inspector can check out exactly that revision, replay the analysis, and verify reproducibility.

Failure handling: if GitHub Enterprise is unreachable at signature time, the workflow blocks with `GITHUB_RESOLVE_FAIL` rather than capturing an incomplete record. The Lab Lead has a manual retry path that re-attempts with the resolved metadata once GitHub is available.

### 12.8 Audit-trail focused-review tool design

The focused-review tool `CYR-AUD-FOCUSED` (DS-AUD-05) filters the full audit trail to material events: signatures, mode changes, schema changes, unlock-edits. The design choice is to expose a small high-signal stream rather than a comprehensive but unreadable one. The Document-Coordinator + QA reviewer both rotate through this tool monthly + quarterly respectively.

The filter list itself is configuration — when Benchling ships a new release that introduces new event types (DS-VND-02 path), the focused-review filter must be reviewed for relevance. This is the explicit content of the vendor-release evaluation runbook step "review focused-review filter for completeness."

### 12.9 Witness-deadline business rule

Critical entries (`template.requires_witness = true`) gate approval on witness signature within `template.witness_deadline_hours` (default 48 h, CI-05). Past deadline, the Lab-Lead inbox + daily email digest surface the overdue entry; no automatic deviation is raised because Cyrene's design choice is to keep R&D collaborative — the witness backlog is a team-level conversation, not a regulatory escalation, unless the entry is in GMP mode in which case the witness deadline is treated as a quality-system commitment with QA escalation.

### 12.10 Helios audit-event handover — pre-handover semantics

Until Helios becomes the system-of-record for cross-system audit trails (post-handover target), the Benchling-side audit trail remains the authoritative record. Helios receives a publish stream via the `helios.ingest.cyrene.benchling.v1` Kafka topic; reconciliation is a parity check rather than a sole-source dependency. The publish-lag alert at 600 s ensures that an outage of the Helios path does not silently degrade the audit-trail position.

### 12.11 Per-doc-type retention split design

Audit-trail retention is mode-aware: GMP-mode entries retain ≥ 25 y per EU GMP Chapter 4; R&D-mode entries retain ≥ 10 y per Cyrene's R&D records-management policy. Both classes archive to S3 Object Lock COMPLIANCE; the 25 y vs 10 y discriminator drives the legal-hold tier. The design choice avoids both over-retention (privacy / cost) and under-retention (regulatory exposure). The retention class is stamped on the entry at creation and is immutable thereafter; mode-change forward-only (DS-MODE-02) prevents accidental tier downgrade.

### 12.12 Periodic-review template design

The annual periodic-review template `CYR-PR-ELN-YYYYMMDD` captures: tenancy-configuration drift vs baseline, audit-trail focused-review summary, vendor-assurance status, integration health (Vault / LIMS / eQMS / GitHub), schema-promotion log, template-promotion log, training-currency summary, signature-rate KPI. Sign-off requires Head of R&D Informatics + VP QA.

### 12.13 Critical-entry witness flag — design intent

The witness flag is declared at template level (`template.requires_witness = true`) rather than per-entry. This is a deliberate design choice: making witness requirement a template-design decision forces the deliberation into the template-promotion workflow (where Schema-Author + Schema-Approver have time to think it through), rather than making it an ad-hoc per-entry call (where it could be skipped under deadline pressure). Critical entry classes — release-supporting data, batch-record entries, GMP-mode characterisation results — should always carry the witness flag at template level. The witness deadline (default 48 h, CI-05) gives the witness time to engage thoughtfully without blocking lab throughput indefinitely.

### 12.14 Search RBAC + bulk-export anti-exfiltration design

Project-level RBAC (DS-SEC-02) plus the bulk-export role restriction to `ELN-Admin` (DS-SEC-04) form a layered defence against unauthorised mass-extraction. Search-result rendering respects RBAC at row level; users see only entries they have project-membership for, even when running broad full-text searches. Bulk-export events are logged + reviewed monthly per FS-SEC-04. The design choice is anti-exfiltration without blocking legitimate use cases (e.g., M&A due diligence, regulator response).

### 12.15 BAA / DPA documentation cadence

Vendor sub-processor changes (DS-VND-03 path) require GDPR Art. 28 DPA Annex II updates. The design choice is to capture sub-processor inventory in `CYR-VND-REG.Benchling-subprocessors.yaml` and review it quarterly via the vendor-assurance program. PHI minimisation guidance lives in `CYR-SOP-MINIMISE-PHI` and is referenced from every entry-create workflow that may carry patient-identifiable content.

### 12.16 Cross-system audit-event parity check

The daily Helios reconciliation job (DS-XINT-HEL-03) compares the Benchling-side published event count vs the Helios-side ingested event count over the prior 24 h window. Mismatch > 0.01% raises a MasterControl deviation; the design intent is to catch silent publish failures before they accumulate into a multi-day audit-trail gap.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
