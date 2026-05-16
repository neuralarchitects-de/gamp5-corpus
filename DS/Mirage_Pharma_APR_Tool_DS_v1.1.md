---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (v1.0 corpus genesis per METHODOLOGY § 2B)"
seed_corpus_basis:
  - "MIR-FS-APR-001 v1.2 (parent FS)"
  - "MIR-URS-APR-001 v1.2 (parent URS — transitive)"
  - "GAMP 5 (2nd Ed., 2022) — DS scope per site project mode: Cat 4 vendor APR/PQR module configuration; parent URS/FS classified Cat 5 (custom Python) to support a corpus diversity scenario, but the user-prescribed DS authoring scope is Cat 4 Configuration Specification using a vendor APR module (TrackWise APR / Sparta APR / Pilgrim APR family — selected: Sparta Systems TrackWise APR Module 9.2 — per the user task table)"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200"
  - "21 CFR Part 211 § 211.180(e); EU GMP Annex 11; EU GMP Chapter 1 § 1.10"
  - "ICH Q9(R1); ICH Q10"
  - "PIC/S PI 041; ISO 22514-2:2017; WHO TRS 970 Annex 6"
parent_fs:
  document_number: MIR-FS-APR-001
  version: "1.2"
  file: "../../../FS_FDS/_generated/final/Mirage_Pharma_APR_Tool_FS_v1.3.md"
parent_urs:
  document_number: MIR-URS-APR-001
  version: "1.2"
  file: "../../../URS/_generated/final/Annual_Product_Review_Tool__Mirage_Pharma_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Annual Product Review (APR / PQR) Tool — Sparta Systems TrackWise APR Module 9.2

**Document Number:** MIR-DS-APR-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** MIR-FS-APR-001 v1.2
**Parent URS:** MIR-URS-APR-001 v1.2 *(informational; transitive)*
**Site:** Mirage Pharma Co., Global Quality Operations, Boston, MA, USA *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (the parent URS/FS classify the system Cat 5 Custom Application; the site has subsequently selected a vendor APR module — Sparta Systems TrackWise APR Module 9.2 — as the implementation path, which moves the system class to Cat 4 Configured Product per METHODOLOGY § 2A.10. The two earlier-cycle FS-IDs that describe Cat 5 site-SDLC artefacts — FS-DEV-01..04 — are addressed in this DS as vendor-SDLC-equivalent obligations on Sparta plus the small site-authored extension footprint described in § 8.)
**Project Mode:** Configuration project on commercial software product **Sparta Systems TrackWise APR Module 9.2** (GAMP 5 Category 4 — Configured Product). Alternative vendor candidates evaluated and not chosen: Honeywell Sparta APR (predecessor product line, superseded by TrackWise 9.2), Pilgrim APR Module (functional equivalence but lacking the Halcyon Stability integration adaptor Mirage Pharma requires).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200; 21 CFR Part 211 § 211.180(e); EU GMP Annex 11; EU GMP Chapter 1 § 1.10; ICH Q9(R1); ICH Q10; PIC/S PI 041; WHO TRS 970 Annex 6.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Quality Operations — SME) | _____________ | _____________ | _____ |
| Reviewer (Statistician — SPC + capability) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs — EU PQR variant) | _____________ | _____________ | _____ |
| Approver (System Owner — Director Quality Operations) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial issue. Inherited Tier T2 from parent URS+FS pair (URS lands at 62 reqs; FS at 77 FS-IDs). DS covers 75/77 FS-IDs; 2 FS-IDs flagged as vendor-internal — no site design surface (FS-DEV-03 container-signing + FS-DEV-04 SBOM are vendor-SDLC obligations transferred to Sparta per vendor-assurance contract). Site-system-class change from Cat 5 (URS / FS) to Cat 4 (DS) recorded in this entry per METHODOLOGY § 2A.10. Generated as part of the DS v1.0 corpus ship per METHODOLOGY § 2B. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

DS-specific terms only — URS / FS definitions inherited by reference.

| Term | Definition |
|---|---|
| CS | Configuration Specification (this document) |
| CI | Configuration Item — one configurable parameter, value, default-vs-custom flag, justification |
| TrackWise APR | Sparta Systems TrackWise APR Module 9.2 — vendor APR/PQR product |
| Variant | APR (FDA 21 CFR § 211.180(e)) / PQR (EU GMP Ch.1 § 1.10) / APR+PQR / WHO TRS 970 Annex 6 |
| SPC ruleset | Western Electric Rules 1–4 + Nelson Rules 1–8 |
| Capability index | Cp / Cpk / Pp / Ppk per ISO 22514-2 |

## 1. Purpose

This Configuration Specification (CS) is the technical-design layer between `MIR-FS-APR-001` v1.2 and downstream configuration / IQ / OQ / PQ Protocols for the Sparta Systems TrackWise APR Module 9.2 deployment supporting FDA Annual Product Review (21 CFR § 211.180(e)) and EU Product Quality Review (EU GMP Chapter 1 § 1.10) at Mirage Pharma Global Quality Operations. The site has selected a vendor APR module (TrackWise APR 9.2) as the implementation path, moving the system from the URS/FS-declared Cat 5 Custom Application to a Cat 4 Configured Product per METHODOLOGY § 2A.10. The DS declares, per configuration item, the chosen value, default-vs-custom flag, FS-ID(s) traced, and planned verification. Vendor source-code internals (TrackWise APR module logic; SPC + capability engine) are not redrawn here — those remain under Sparta Systems SDLC.

## 2. Scope

### In scope

- TrackWise APR Module 9.2 — configuration of variant flags, SPC rulesets, capability calculation, OOS / OOT compilation, stability data review, validation status review, supplier quality review, recommendations register, sign-off workflow.
- Postgres-backed (Sparta-managed) data warehouse for snapshots + audit trail.
- Quarto-based report rendering (TrackWise APR's bundled renderer; configured templates only).
- Template engine variant selection (APR / PQR / APR+PQR / WHO).
- Audit-trail bindings, 21 CFR Part 11 controls.
- Integration endpoints (read-only consumers): LabWare LIMS 8 (release + stability + EM), Werum PAS-X (batch yields, deviations, IPCs), MasterControl eQMS (deviations + CAPAs + CRs + suppliers), Sirius PV (complaints), Halcyon Stability (protocols + Q1E), Selene Cold-Chain (excursions), Atlas Serialization (recall / aggregation events), ValGenesis VLM (validation status); approved-report push to Veeva Vault QualityDocs; SSO via Okta SAML 2.0 + MFA.

### Out of scope

- Source-system data integrity (each separately validated).
- Literature review.
- CMC regulatory submissions (CMC team consumes APR/PQR output).
- Annual stability protocol authoring (Halcyon Stability URS scope).

## 3. Architectural Overview

### 3.1 Logical view

```
                          Okta (SAML 2.0 + MFA)
                                    │
                                    ▼
   ┌─────────────────────────────────────────────────────────────┐
   │   Sparta Systems TrackWise APR Module 9.2 (site tenancy)     │
   │   ┌─────────────────────┐  ┌─────────────────────────────┐    │
   │   │ Extractor framework  │  │ SPC + Capability engine     │    │
   │   │ (per-source ETL)     │  │ (WER + Nelson + ISO 22514-2)│    │
   │   └─────────────────────┘  └─────────────────────────────┘    │
   │   ┌─────────────────────┐  ┌─────────────────────────────┐    │
   │   │ OOS/OOT compiler     │  │ Stability/VLM/Supplier modules│   │
   │   └─────────────────────┘  └─────────────────────────────┘    │
   │   ┌─────────────────────┐  ┌─────────────────────────────┐    │
   │   │ Recommendations      │  │ Variant engine               │    │
   │   │ register             │  │ (FDA / EU / WHO)             │    │
   │   └─────────────────────┘  └─────────────────────────────┘    │
   │   ┌────────────────────────────────────────────────────┐      │
   │   │  Postgres warehouse + Sparta report renderer (PDF + │      │
   │   │  Excel + structured CSV)                            │      │
   │   └────────────────────────────────────────────────────┘      │
   └────────────┬────────────────────────────┬────────────────────┘
                │                            │
                ▼                            ▼
   ┌──────────────────────┐         Vault QualityDocs (archival)
   │  Source GxP systems  │
   │  LIMS · PAS-X · eQMS  │
   │  PV · Stability · VLM │
   │  Cold-Chain · Atlas   │
   └──────────────────────┘
```

### 3.2 Per-run data flow

```
[Run-init: Director Quality Operations selects product + variant flag]
   │
   ▼
[Extractor framework — per source, idempotent on (product, year, run_id)]
   │  PAS-X: BATCH_YIELDS + DEVIATIONS + IPC_RESULTS
   │  LIMS: release-test + OOS + OOT + stability
   │  eQMS: deviations + CAPAs + CRs + supplier complaints
   │  PV: complaint summary
   │  Halcyon: stability protocols + Q1E
   │  Cold-Chain: excursions
   │  Atlas: recall / aggregation events
   │  VLM: system-status summary
   │  Each extractor writes snapshot manifest to apr_snapshots + S3
   │
   ▼
[Aggregation engine — joins per-source snapshots into apr_run schema]
   │
   ▼
[Analysis engines]
   │  SPC + Capability (DS-APR-... rows 4.4)
   │  OOS / OOT compiler (DS-APR-... rows 4.5)
   │  Stability / VLM / Supplier (DS-APR-... rows 4.6 - 4.8)
   │
   ▼
[Recommendations register — carry-forward + new]
   │
   ▼
[Variant engine selects template sections (APR / PQR / WHO)]
   │
   ▼
[Quarto renderer → PDF/A-3 + Excel + structured CSV]
   │
   ▼
[Sign-off workflow: Author → Statistician → QA-R → QA-A → QP(EU)]
   │
   ▼
[Approved report pushed to Vault QualityDocs — archival ≥ 25 y]
```

## 4. Configuration Specification

### 4.1 Application Lifecycle (Cat 4 vendor SDLC + site-validation obligations)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-APR-01 | Vendor SDLC reliance | Sparta Systems TrackWise APR Module 9.2 — SOC 2 Type II + ISO 27001 + customer-shared CSV summary + DPA tracked in `VA-SPARTA-2026` | Custom | Cat 4 site-class change vs URS/FS-declared Cat 5 means FS-DEV-01 site-SDLC reqs are addressed by vendor SDLC; site validation focuses on configuration. | FS-DEV-01 | OQ-VND-PACK-01 |
| DS-APR-02 | Source-code custody | Vendor source not held by site; site holds escrow agreement with Sparta for business-continuity | Custom | FS-DEV-02 site-Git custody reframed as escrow under Cat 4. | FS-DEV-02 | OQ-ESCROW-VERIFY-01 |
| DS-APR-03 | Vendor-release impact-assessment SLA | 14 days from Sparta release-notes receipt; config-affecting changes raise re-validation CR | Custom | Standard site vendor-management SOP. | FS-DEV-01, FS-DEV-02 | OQ-VND-RELEASE-01 |
| DS-APR-04 | Site-deployed Python extractor extensions | Listed in § 8.1 mini-SDS (hybrid Cat 4 + Cat 5 sub-component) | Custom | Per METHODOLOGY § 2B.4 rule 6 — site-authored extractor extension code makes this a hybrid Cat 4 + Cat 5 system for the scope of those scripts. | FS-DEV-01 .. FS-DEV-04 | OQ-EXTRACTORS-01 |

### 4.2 Aggregation and Calculation Rules

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-APR-05 | Template lifecycle | DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE; Author ≠ Approver via TrackWise role mapping | Default (TrackWise template-lifecycle) | FS-RULE-01. | FS-RULE-01 | OQ-TMPL-LIFECYCLE-01 |
| DS-APR-06 | SPC ruleset | Western Electric Rules 1–4 (1 pt > 3σ; 2 of 3 > 2σ; 4 of 5 > 1σ; 8 in a row same side) + Nelson Rules 1–8 | Default (TrackWise APR built-in) | FS-RULE-02. | FS-RULE-02 | OQ-SPC-RULES-01 |
| DS-APR-07 | SPC OQ reference dataset | AIAG SPC reference dataset; bit-identical rule firings verified | Custom | FS-RULE-02 verification approach. | FS-RULE-02 | OQ-SPC-RULES-01 |
| DS-APR-08 | Aggregation determinism | TrackWise APR SQL views deterministic; (product, year, source-snapshot-hash) tuple is cache key; re-run yields bit-identical CSV | Custom | FS-RULE-03. | FS-RULE-03 | OQ-DETERMINISM-01 |
| DS-APR-09 | Extractor integrity check | Per-extractor `row_count + sha256_manifest`; reconciliation gate; mismatch → `ExtractorIntegrityError` blocks run | Custom | FS-RULE-04. | FS-RULE-04 | OQ-EXTRACTOR-INTEGRITY-01 |
| DS-APR-10 | Capability normality test | Anderson–Darling, α = 0.05 | Default (ISO 22514-2 convention) | FS-RULE-05. | FS-RULE-05 | OQ-CAPABILITY-AD-01 |
| DS-APR-11 | Non-normal capability handling | Box–Cox transform OR non-parametric Clements-method Cpk per attribute config | Default | FS-RULE-05. | FS-RULE-05 | OQ-CAPABILITY-NONNORMAL-01 |
| DS-APR-12 | Capability OQ reference dataset | Spans normal + lognormal + bi-modal distributions | Custom | FS-RULE-05 verification. | FS-RULE-05 | OQ-CAPABILITY-AD-01 |
| DS-APR-13 | Small-sample display logic | n ≥ 30 → "valid"; 10 ≤ n < 30 → "indicative only — small-sample"; n < 10 → suppressed | Default (TrackWise APR built-in) | FS-RULE-06. | FS-RULE-06 | OQ-CAPABILITY-SMALL-N-01 |

### 4.3 Data Aggregation Sources

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-APR-14 | PAS-X extractor | Reads `BATCH_YIELDS` + `DEVIATIONS` + `IPC_RESULTS` via PAS-X DataSphere DB views; idempotency key `(product, year, run_id)` | Custom | FS-AGG-01. | FS-AGG-01 | OQ-EXTRACTOR-PASX-01 |
| DS-APR-15 | LIMS extractor | REST `GET /api/v2/results?product={p}&from={d1}&to={d2}&status=APPROVED`; service account in Vault | Custom | FS-AGG-02. | FS-AGG-02 | OQ-EXTRACTOR-LIMS-01 |
| DS-APR-16 | MasterControl extractor | REST `GET /api/eqms/{deviations,capa,changecontrol,supplier-complaints}?product={p}&from={d1}&to={d2}`; root-cause taxonomy mapping `MIR-CFG-RC-MAP-001` | Custom | FS-AGG-03. | FS-AGG-03 | OQ-EXTRACTOR-EQMS-01 |
| DS-APR-17 | Sirius PV extractor | REST; severity classes (S1–S4) + PV signal classes mapped per `MIR-CFG-PV-MAP-001` | Custom | FS-AGG-04. | FS-AGG-04 | OQ-EXTRACTOR-PV-01 |
| DS-APR-18 | Cold-Chain extractor | REST `GET /api/excursions?product={p}` with batch-id linkage | Custom | FS-AGG-05. | FS-AGG-05 | OQ-EXTRACTOR-CC-01 |
| DS-APR-19 | Atlas Serialization extractor | Pulls recall / counterfeit / aggregation-anomaly events per product GTIN | Custom | FS-AGG-06. | FS-AGG-06 | OQ-EXTRACTOR-ATLAS-01 |
| DS-APR-20 | Snapshot manifest | Per extraction `{source, timestamp, row_count, sha256}` to `apr_snapshots` + immutable S3 bucket (object-lock 25 y) | Custom | FS-AGG-07. | FS-AGG-07 | OQ-SNAPSHOT-01 |

### 4.4 Trend Analysis and Capability Indices

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-APR-21 | Chart catalogue | X̄-R, X̄-s, I-MR, p-chart, np-chart, c-chart, u-chart, EWMA, CUSUM | Default (TrackWise APR) | FS-TREND-01. | FS-TREND-01 | OQ-CHART-CAT-01 |
| DS-APR-22 | Chart selection map | Per CQA / CPP per `MIR-CFG-CHART-MAP-001` | Custom | FS-TREND-01. | FS-TREND-01 | OQ-CHART-MAP-01 |
| DS-APR-23 | Rule-firing emission | `(batch_id, attribute, rule_no, ruleset, timestamp)` tuples to `rule_firings` table; annotated chart markers + footnote table | Default | FS-TREND-02. | FS-TREND-02 | OQ-RULE-FIRINGS-01 |
| DS-APR-24 | Phase boundary rule | Phase 1 = recent stable phase (Cp/Cpk); Phase 2 = review period (Pp/Ppk); boundary = last EFFECTIVE process-impact CR closure date per eQMS classification | Custom | FS-TREND-03. | FS-TREND-03 | OQ-PHASE-BOUND-01 |
| DS-APR-25 | Trend-commentary blocking | Trend-commentary field required when any rule fires; pre-render check blocks sign-off via `BlockingValidationError` if empty | Custom | FS-TREND-04. | FS-TREND-04 | OQ-COMMENTARY-GATE-01 |
| DS-APR-26 | EWMA defaults | `λ = 0.2` default per `MIR-CFG-EWMA-001`; control limits `μ ± L·σ·sqrt(λ/(2-λ))` with `L = 3` | Default (ISO 22514-2) | FS-TREND-05. | FS-TREND-05 | OQ-EWMA-01 |

### 4.5 OOS / OOT Review Compilation

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-APR-27 | OOS compiler | Queries LIMS `OOS_INVESTIGATIONS` + eQMS `INVESTIGATION_LINKED_DEVIATION`; sorted by detection date; root-cause taxonomy per FDA OOS Guidance (2006) | Custom | FS-OOS-01. | FS-OOS-01 | OQ-OOS-COMPILE-01 |
| DS-APR-28 | OOT compiler | Rule firings + LIMS `OOT_FLAGS` + statistician-curated OOT registry | Custom | FS-OOS-02. | FS-OOS-02 | OQ-OOT-COMPILE-01 |
| DS-APR-29 | Open-investigation gate | Any OOS / OOT with `status != CLOSED` at run-time → acknowledgement modal; Statistician + QA Approver must acknowledge before sign-off proceeds | Custom | FS-OOS-03. | FS-OOS-03 | OQ-OPEN-INV-GATE-01 |
| DS-APR-30 | OOS-rate trend | `count(OOS_investigations) / count(batches_released)`; trended over prior 3 review periods | Custom | FS-OOS-04. | FS-OOS-04 | OQ-OOS-RATE-01 |

### 4.6 Stability Data Review

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-APR-31 | Halcyon Stability extractor | REST `GET /api/stability/protocols?product={p}` + `GET /api/stability/q1e?product={p}` | Custom | FS-STAB-01. | FS-STAB-01 | OQ-EXTRACTOR-HALCYON-01 |
| DS-APR-32 | Stability OOS / OOT linkage | Cross-references LIMS stability results with status = OOS or OOT; clickable link to eQMS investigation | Custom | FS-STAB-02. | FS-STAB-02 | OQ-STAB-LINK-01 |
| DS-APR-33 | Shelf-life change capture | Pulled from Halcyon `q1e_shelf_life_changes` table with confidence intervals; statistician approval reference captured per ICH Q1E | Custom | FS-STAB-03. | FS-STAB-03 | OQ-SHELF-LIFE-01 |
| DS-APR-34 | Photostability + bracketing coverage | ICH Q1B + Q1D coverage status pulled from Halcyon protocol metadata | Default | FS-STAB-04. | FS-STAB-04 | OQ-PHOTOSTAB-01 |

### 4.7 Validation Status Review

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-APR-35 | ValGenesis VLM extractor | REST `GET /api/vlm/systems-status?product={p}`; renders status table grouped by equipment / utility / computerised | Custom | FS-VS-01. | FS-VS-01 | OQ-EXTRACTOR-VLM-01 |
| DS-APR-36 | Expired-PR / revalidation-overdue flags | Pulled per system; rendered as red badges with required-acknowledgement modal at QA approval | Custom | FS-VS-02. | FS-VS-02 | OQ-VS-FLAGS-01 |
| DS-APR-37 | PQ-run count metric | Count of executed PQ-protocol records in review period per critical system | Default | FS-VS-03. | FS-VS-03 | OQ-PQ-COUNT-01 |

### 4.8 Supplier Quality Review

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-APR-38 | Supplier-scorecard extractor | MasterControl `SUPPLIER_SCORECARDS` view per critical supplier; KPI columns: lot-acceptance rate, on-time delivery, complaint rate, audit status | Custom | FS-SUP-01. | FS-SUP-01 | OQ-EXTRACTOR-SUP-01 |
| DS-APR-39 | Supplier downgrade detection | Any `supplier_status ∈ {PROBATION, DISQUALIFIED}` OR `qualification_expiry < run_date` OR open supplier-CAPA → flag + Recommendations register entry | Custom | FS-SUP-02. | FS-SUP-02 | OQ-SUP-DOWNGRADE-01 |
| DS-APR-40 | Supplier-audit details | Last audit date, status, open observations per critical supplier | Default | FS-SUP-03. | FS-SUP-03 | OQ-SUP-AUDIT-01 |

### 4.9 Recommendations + Sign-off Workflow

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-APR-41 | Recommendations register | `apr_recommendations` table with FKs to CAPA, source finding, prior-year recommendation; UI grid in Quarto report's interactive HTML companion | Custom | FS-REC-01. | FS-REC-01 | OQ-RECOMMEND-REG-01 |
| DS-APR-42 | Carry-forward job | Copies prior-year unclosed recommendations with aging-days computed; "Carried Forward" section | Custom | FS-REC-02. | FS-REC-02 | OQ-CARRY-FORWARD-01 |
| DS-APR-43 | Sign-off state machine | `DRAFT → AUTHORED → STATS-REVIEWED → QA-REVIEWED → QA-APPROVED → QP-APPROVED (EU)`; each transition records (user, ts, role, meaning) | Custom | FS-REC-03. | FS-REC-03 | OQ-SIGN-STATE-01 |
| DS-APR-44 | Sequential-transition enforcement | State machine prevents skipping; e.g., `QA-APPROVED` cannot be entered without prior `QA-REVIEWED` | Custom | FS-REC-04. | FS-REC-04 | OQ-SIGN-OFF-SEQUENTIAL-01 |
| DS-APR-45 | Re-auth at signing | Okta step-up MFA via OIDC `acr_values=urn:okta:mfa:strong`; failure aborts signing | Custom | FS-REC-05. | FS-REC-05 | OQ-REAUTH-SIGN-01 |

### 4.10 EU PQR vs FDA APR Variant Logic

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-APR-46 | Variant flag | `APR / PQR / APR+PQR / WHO` selected at run-init; template includes / excludes sections per `MIR-CFG-VARIANT-SECTIONS-001` | Custom | FS-VAR-01. | FS-VAR-01 | OQ-VARIANT-FLAG-01 |
| DS-APR-47 | Combined APR + PQR | Union of section sets; section-coverage cross-reference table at end of report | Custom | FS-VAR-02. | FS-VAR-02 | OQ-VARIANT-COMBINED-01 |
| DS-APR-48 | WHO TRS 970 variant | Adds prequalification-specific sections (re-qualification status, WHO commitments) | Custom | FS-VAR-03. | FS-VAR-03 | OQ-VARIANT-WHO-01 |

### 4.11 Multi-Product and Multi-Site Mode

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-APR-49 | Single-product-per-run validator | Run-init: `assert len(products) == 1` raises `MultiProductDisallowedError` otherwise | Custom | FS-MULTI-01. | FS-MULTI-01 | OQ-SINGLE-PRODUCT-01 |
| DS-APR-50 | Per-site sectioning | Extractor sub-divides by `manufacturing_site` field; sections rendered per site; no cross-site pooling unless `--allow-pooled-stats` + QA approver-2 signature | Custom | FS-MULTI-02. | FS-MULTI-02 | OQ-MULTI-SITE-01 |
| DS-APR-51 | Portfolio view | Read-only Quarto dashboard aggregating compliance signals across products; refreshed on every product-run completion | Custom | FS-MULTI-03. | FS-MULTI-03 | OQ-PORTFOLIO-VIEW-01 |

### 4.12 Audit Trail / 21 CFR Part 11 / ALCOA+

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-APR-52 | Audit-trail schema | `apr_audit`: event_id, user_id, action, entity_type, entity_id, before_hash, after_hash, timestamp; append-only at DB role-grant level | Custom | FS-AUD-01. | FS-AUD-01 | OQ-AUD-COVERAGE-01 |
| DS-APR-53 | Append-only enforcement | `apr_app` role has INSERT only on `apr_audit`; no UPDATE/DELETE grant; super-user access requires break-glass + audit-trail review | Custom | FS-AUD-02. | FS-AUD-02 | OQ-AUD-APPENDONLY-01 |
| DS-APR-54 | Monthly QA Compliance review | Evidence template `MIR-PR-AUD-001` filed in Vault | Default | FS-AUD-03. | FS-AUD-03 | OQ-AUD-REVIEW-01 |
| DS-APR-55 | Audit retention | ≥ 25 y on Postgres + nightly export to S3 with object-lock | Custom | FS-AUD-04. | FS-AUD-04 | OQ-RETENTION-01 |
| DS-APR-56 | § 11.10(a)–(c) validation procedure | `MIR-SOP-CSV-001` + copy-generation API `GET /api/runs/{id}/export?format=pdf,xlsx,csv` | Default | FS-PART11-10. | FS-PART11-10 | OQ-PART11-10 |
| DS-APR-57 | § 11.50 signature manifestation | Rendered on report cover + audit-trail with printed-name + UTC-timestamp + meaning | Default | FS-PART11-50. | FS-PART11-50 | OQ-PART11-50 |
| DS-APR-58 | § 11.70 signature binding | SHA-256 of report + signature timestamp + user-id signed via Sigstore; verifiable post-hoc | Custom | FS-PART11-70. | FS-PART11-70 | OQ-PART11-70 |
| DS-APR-59 | § 11.100 uniqueness | Okta enforces unique user-id; deactivated accounts non-reassignable | Default | FS-PART11-100. | FS-PART11-100 | OQ-PART11-100 |
| DS-APR-60 | § 11.200 re-auth | Okta step-up MFA on every signing event | Default | FS-PART11-200. | FS-PART11-200 | OQ-PART11-200 |
| DS-APR-61 | DI-Attributable | Every audit event carries `user_id` from Okta JWT `sub` claim | Default | FS-DI-01. | FS-DI-01 | OQ-DI-ATTRIB-01 |
| DS-APR-62 | DI-Legible | Report rendered as PDF/A-3 + Excel + structured CSV; all three identically signed | Custom | FS-DI-02. | FS-DI-02 | OQ-EXPORT-FORMATS-01 |
| DS-APR-63 | DI-Contemporaneous | NTP-synced system clock (chrony); skew alert at > 1 s | Default | FS-DI-03. | FS-DI-03 | OQ-NTP-SKEW-01 |
| DS-APR-64 | DI-Original snapshots | Preserved in immutable S3 (object-lock 25 y) referenced by manifest SHA | Custom | FS-DI-04. | FS-DI-04 | OQ-SNAPSHOT-01 |
| DS-APR-65 | DI-Accurate | Numeric accuracy verified per OQ reference dataset | Default | FS-DI-05. | FS-DI-05 | OQ-DI-ACCURATE-01 |

### 4.13 Integrations / Performance / Security / Training / Periodic Review

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-APR-66 | LIMS integration | REST + DB read-replica; OAuth2 client-credentials; service account in Vault | Custom | FS-INT-LIMS-01. | FS-INT-LIMS-01 | OQ-INT-LIMS-01 |
| DS-APR-67 | PAS-X integration | DataSphere read-only views; AD service account | Custom | FS-INT-MES-01. | FS-INT-MES-01 | OQ-INT-MES-01 |
| DS-APR-68 | MasterControl integration | REST per `MIR-IF-EQMS-001`; rate-limit 60 req/min | Custom | FS-INT-EQMS-01. | FS-INT-EQMS-01 | OQ-INT-EQMS-01 |
| DS-APR-69 | Sirius PV integration | REST | Default | FS-INT-PV-01. | FS-INT-PV-01 | OQ-INT-PV-01 |
| DS-APR-70 | Halcyon Stability integration | REST | Default | FS-INT-STAB-01. | FS-INT-STAB-01 | OQ-INT-STAB-01 |
| DS-APR-71 | ValGenesis VLM integration | REST | Default | FS-INT-VLM-01. | FS-INT-VLM-01 | OQ-INT-VLM-01 |
| DS-APR-72 | Cold-Chain integration | REST | Default | FS-INT-COLDCHAIN-01. | FS-INT-COLDCHAIN-01 | OQ-INT-CC-01 |
| DS-APR-73 | Atlas Serialization integration | REST | Default | FS-INT-SER-01. | FS-INT-SER-01 | OQ-INT-ATLAS-01 |
| DS-APR-74 | Vault QualityDocs push | Approved-report push (PDF + Excel + CSV + audit-trail export) | Custom | FS-INT-VAULT-01. | FS-INT-VAULT-01 | OQ-VAULT-PUSH-01 |
| DS-APR-75 | Per-run wall-clock SLO | P95 ≤ 60 min single-product run; measured by PQ | Custom | FS-PERF-01. | FS-PERF-01 | PQ-PERF-RUN-01 |
| DS-APR-76 | Availability target | 99.0% during annual run window; monitored via Prometheus + alertmanager | Default | FS-AV-01. | FS-AV-01 | OQ-AVAIL-MONITOR-01 |
| DS-APR-77 | DB backup | `pg_basebackup` + WAL archival nightly to S3; quarterly restore test witnessed by QA per `MIR-RB-RESTORE-001` | Custom | FS-BAK-01. | FS-BAK-01 | OQ-BAK-PITR-01 |
| DS-APR-78 | SSO + service-account | Okta SAML 2.0 + MFA; service-account secrets in HashiCorp Vault; quarterly access review | Default | FS-SEC-01. | FS-SEC-01 | OQ-SEC-ACCESS-01 |
| DS-APR-79 | LMS curriculum | Cornerstone `MIR-CURR-APR-Operator-v1`; statistician competency includes SPC + capability | Custom | FS-TRN-01. | FS-TRN-01 | OQ-LMS-GATE-01 |
| DS-APR-80 | Periodic-review template | `MIR-PR-APR-YYYYMMDD`; signed by Director Quality Operations + VP QA | Custom | FS-PR-01. | FS-PR-01 | OQ-PR-RUNBOOK-01 |

## 5. Workflow + Business-Rule Design

### 5.1 Sign-off state-machine enforcement

The TrackWise APR Module's signature workflow is configured with the state machine in DS-APR-43. Every transition is sequential (DS-APR-44) — the UI disables transition buttons for states unreachable from the current state. Re-auth at every signing event (DS-APR-45 + DS-APR-60) enforced via Okta step-up MFA.

The EU PQR variant adds the QP signature as the final state. For an APR-only run, the state machine terminates at `QA-APPROVED`. For APR+PQR combined runs (DS-APR-47), the QP signature is required regardless of variant flag.

### 5.2 OOS / OOT gating workflow

1. Run extractors complete; OOS / OOT compilers populate `apr_oos`, `apr_oot` tables.
2. Sign-off workflow reaches `STATS-REVIEWED` state.
3. Before transition to `QA-REVIEWED`: pre-render check queries open OOS / OOT (`status != CLOSED`).
4. If any open OOS / OOT exist: acknowledgement modal presented to Statistician + QA Approver; both must record acknowledgement before transition proceeds.
5. Acknowledgement events written to `apr_audit` for later inspection.

### 5.3 Multi-site mode workflow

A product manufactured at ≥ 2 sites:

1. Run-init validator confirms `products = [single_product]` per DS-APR-49.
2. Extractors sub-divide by `manufacturing_site` field; per-site partition of all source data.
3. Default rendering: per-site sub-sections within the single product report.
4. Pooled-stats option: requires `--allow-pooled-stats` flag set at run-init AND a second QA Approver signature (approver-2 ≠ approver-1) at `QA-APPROVED` transition.
5. Pooled-stats decision logged in `apr_audit.POOLED_STATS_ENABLED`.

### 5.4 Variant misconfig prevention

Risk: EU PQR variant misses critical IPC / starting-material section vs FDA APR.

Workflow:

1. Variant flag at run-init drives `MIR-CFG-VARIANT-SECTIONS-001` template lookup.
2. Section-coverage validator runs pre-render: ensures every required section per the chosen variant is populated by extractor output.
3. Missing section: render blocked with `VariantSectionMissingError`; CAPA-event raised via FS-XINT-EQMS-01.

## 6. Role-Permission Matrix Design

| Action / Role | Product Owner | Statistician | QA Reviewer | QA Approver (Head of QA) | QP (EU PQR) | Tool Administrator | Auditor | Inspector (on-demand) |
|---|---|---|---|---|---|---|---|---|
| Run APR / PQR for assigned products | C | — | — | — | — | — | — | — |
| Author trend-commentary | C/U | — | — | — | — | — | — | — |
| Review SPC outputs + capability; co-approve | — | S (STATS-REVIEWED) | — | — | — | — | — | — |
| Review report; raise findings | — | — | C/U | — | — | — | — | — |
| Sign QA-REVIEWED transition | — | — | S | — | — | — | — | — |
| Sign QA-APPROVED transition | — | — | — | S | — | — | — | — |
| Sign QP-APPROVED transition (EU PQR) | — | — | — | — | S | — | — | — |
| Deploy / configure tool | — | — | — | — | — | C/U | — | — |
| Read-only across runs + audit trails | R | R | R | R | R | R | R | — |
| Read-only inspection mode (on-demand, time-bound) | — | — | — | — | — | — | — | R |

Legend: R = read, C = create, U = update, S = sign (re-authenticated electronic signature), — = denied.

SoD denies per URS § 4:

- Product Owner ≠ Approver of the same run.
- Tool Admin cannot approve APR / PQR.
- QA Reviewer ≠ QA Approver on the same run.

## 7. Integration Design

| IF-ID | Counterparty | Endpoint | Protocol | Direction | AuthN | Message schema | Retry / DLQ | Audit emission | FS-IDs traced |
|---|---|---|---|---|---|---|---|---|---|
| IF-LIMS-01 | LabWare LIMS 8 | `https://lims.mirage.local/api/v2/results` + DB read-replica | REST mTLS + DB | inbound | OAuth2 client-credentials | JSON results schema | reconciliation nightly; runtime failure → `ExtractorIntegrityError` | `apr_audit.LIMS_EXTRACT` | FS-INT-LIMS-01 |
| IF-MES-01 | Werum PAS-X v3.2 | DataSphere DB views (read-only) | DB (read-replica) | inbound | AD service account | view-row schema | reconciliation nightly | `apr_audit.MES_EXTRACT` | FS-INT-MES-01 |
| IF-EQMS-01 | MasterControl | `GET https://eqms.mirage.local/api/eqms/...` per `MIR-IF-EQMS-001` | REST mTLS | inbound | OAuth2 | JSON deviation / CAPA / CR / supplier schemas; rate-limit 60 req/min | exponential backoff | `apr_audit.EQMS_EXTRACT` | FS-INT-EQMS-01 |
| IF-PV-01 | Sirius PV | REST | REST mTLS | inbound | OAuth2 | JSON complaint summary | reconciliation nightly | `apr_audit.PV_EXTRACT` | FS-INT-PV-01 |
| IF-STAB-01 | Halcyon Stability | `https://halcyon.mirage.local/api/stability/...` | REST mTLS | inbound | OAuth2 | JSON protocol + Q1E | reconciliation nightly | `apr_audit.STAB_EXTRACT` | FS-INT-STAB-01 |
| IF-VLM-01 | ValGenesis VLM | `https://vlm.mirage.local/api/vlm/...` | REST mTLS | inbound | OAuth2 | JSON system-status | reconciliation nightly | `apr_audit.VLM_EXTRACT` | FS-INT-VLM-01 |
| IF-COLDCHAIN-01 | Selene Cold-Chain | `https://coldchain.mirage.local/api/excursions` | REST mTLS | inbound | OAuth2 | JSON excursions | reconciliation nightly | `apr_audit.CC_EXTRACT` | FS-INT-COLDCHAIN-01 |
| IF-ATLAS-01 | Atlas Serialization | REST per product GTIN | REST mTLS | inbound | OAuth2 | JSON recall / aggregation events | reconciliation nightly | `apr_audit.ATLAS_EXTRACT` | FS-INT-SER-01 |
| IF-VAULT-DOC-01 | Veeva Vault QualityDocs | `POST https://vault.mirage.local/api/v24.1/objects/quality_docs` | REST | outbound | OAuth2 | Vault standard | exponential backoff; DLQ at 5 + alarm | `apr_audit.VAULT_PUSH` | FS-INT-VAULT-01 |
| IF-OKTA-01 | Okta IdP | `https://mirage.okta.com/.well-known/openid-configuration` | SAML 2.0 + OIDC step-up | bidirectional | SAML signed + MFA | SAML + OIDC standard | retry per SDK | `apr_audit.AUTHN` → Splunk | FS-SEC-01, FS-XSYS-AD-01 |
| IF-EQMS-CAPA-01 | MasterControl | `POST https://eqms.mirage.local/api/v2/deviations` | REST mTLS | outbound | mTLS + workload-identity | JSON CAPA-ticket per `eqms.ticket.v1`; idempotency `mir-apr-{run_id}-{finding_class}` | exponential backoff; DLQ at 5 | `apr_audit.CAPA_RAISED` | FS-XINT-EQMS-01 |
| IF-VAULT-SEC-01 | HashiCorp Vault | `https://vault-sec.mirage.local/v1/kv/apr/*` | HTTPS AppRole | inbound | AppRole | KV v2 | retry on rotation | vault-access audit | FS-SEC-01 |

## 8. Site-Deployed Components Design

### 8.1 Site-authored extractor extensions

TrackWise APR's vendor extractor framework handles standard cases (LIMS / PAS-X / eQMS / PV). Mirage Pharma's source landscape requires four custom extractors for which Sparta-supplied connectors do not exist:

- `apr-halcyon-extractor.py` — pulls Q1E shelf-life + protocol metadata from Halcyon Stability.
- `apr-atlas-extractor.py` — pulls recall / aggregation events from Atlas Serialization.
- `apr-cc-extractor.py` — pulls cold-chain excursions per product.
- `apr-vlm-extractor.py` — pulls ValGenesis VLM system-status.

**Mini-SDS per METHODOLOGY § 2B.4 rule 6 (hybrid Cat 4 + Cat 5):**

- **Modules:** Each extractor is a Python 3.12 module ≤ 400 LOC, deployed into TrackWise APR's extractor-extension folder via vendor-supported loading mechanism.
- **Common contract:** Each extractor implements the `BaseExtractor` interface from Sparta SDK: `extract(product_id, period) → ExtractorOutput(rows, row_count, sha256_manifest)`.
- **Dependencies:** Python 3.12; `requests`, `psycopg[binary]`, `pydantic` v2; pinned via `pyproject.toml` + hash-locked.
- **Tests:** pytest ≥ 90% line + branch coverage; fixture-mocked source-system responses; regression suite per extractor with reference output.
- **Audit emission:** Every extraction writes `apr_audit.EXTRACT_<source>` with row-count + manifest.
- **Change control:** Source in `mirage/apr-extractors` GitLab; signed commits required; ArgoCD-managed deployment via vendor-loading hook; CR-gated.
- **Verified by:** OQ-EXTRACTORS-01 (per-extractor sub-test).
- **Cat 5 sub-component SDLC discipline:** Code review ≥ 1 approver + ≥ 1 architect; Snyk + SonarQube security gates; SBOM (CycloneDX) per release retained ≥ 25 y per FS-DEV-04.

### 8.2 Variant template files

Per FS-VAR-01 / DS-APR-46, variant section selection is driven by `MIR-CFG-VARIANT-SECTIONS-001` template configuration. The template files (`apr.qmd`, `pqr.qmd`, `apr_pqr_combined.qmd`, `who.qmd`) are vendor TrackWise APR templates customised with Mirage-specific section copy. These are declarative (Quarto markdown + YAML front-matter); no procedural code. Cat 4 declarative only.

### 8.3 Per-source extractor configuration maps

- `MIR-CFG-RC-MAP-001` — root-cause taxonomy mapping (eQMS deviation root-cause codes → standardised APR taxonomy).
- `MIR-CFG-PV-MAP-001` — PV severity-class + signal-class mapping.
- `MIR-CFG-CHART-MAP-001` — chart-type-per-CQA/CPP map.
- `MIR-CFG-VARIANT-SECTIONS-001` — variant flag → section inclusion map.
- `MIR-CFG-EWMA-001` — per-attribute EWMA λ override.

All five are YAML configuration files under change control in `mirage/apr-config` GitLab repo; no procedural code. Cat 4 declarative.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200.
- 21 CFR Part 211 §§ .22, .68, .180, .192 (CGMP; § 211.180(e) Annual Product Review).
- FDA Guidance for Industry: *Investigating Out-of-Specification (OOS) Test Results for Pharmaceutical Production* (2006).
- FDA Guidance for Industry: *Process Validation: General Principles and Practices* (2011) — Stage 3 CPV alignment.
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026).
- FDA *Data Integrity and Compliance with cGMP* (2018).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EU GMP Chapter 1 § 1.10 — Product Quality Review.
- EU GMP Annex 15.
- EU GMP Annex 16.
- Directive 2001/83/EC Art. 51 — QP batch-release obligations.

### International — ICH
- ICH Q9(R1).
- ICH Q10 (especially § 3.2 PQR / APR Management Review).
- ICH Q12.

### Industry / Standards
- ISPE GAMP 5 (2nd Edition, 2022).
- PIC/S PI 041.
- WHO Technical Report Series 970 Annex 6 — Product Quality Review.
- ISO 22514-2:2017.

### Vendor
- Sparta Systems — *TrackWise APR Module 9.2 Configuration Reference* v9.2.
- Sparta Systems — *TrackWise APR Extractor SDK Reference* v9.2.
- Sparta Systems — *TrackWise APR Variant Configuration Guide* v9.2.

### Site
- `MIR-SOP-CSV-001` — CSV procedure.
- `MIR-SOP-APR-001` — Annual Product Review procedure.
- `MIR-RB-RESTORE-001` — restore-test runbook.
- `MIR-IF-EQMS-001` — eQMS interface specification.
- `MIR-PR-AUD-001` — audit-trail review template.
- `MIR-PR-APR-YYYYMMDD` — periodic-review template.

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-APR-01 | FS-DEV-01 |
| DS-APR-02 | FS-DEV-02 |
| DS-APR-03 | FS-DEV-01 / FS-DEV-02 |
| DS-APR-04 | FS-DEV-01 / FS-DEV-02 / FS-DEV-03 / FS-DEV-04 |
| DS-APR-05 | FS-RULE-01 |
| DS-APR-06 | FS-RULE-02 |
| DS-APR-07 | FS-RULE-02 |
| DS-APR-08 | FS-RULE-03 |
| DS-APR-09 | FS-RULE-04 |
| DS-APR-10 | FS-RULE-05 |
| DS-APR-11 | FS-RULE-05 |
| DS-APR-12 | FS-RULE-05 |
| DS-APR-13 | FS-RULE-06 |
| DS-APR-14 | FS-AGG-01 |
| DS-APR-15 | FS-AGG-02 |
| DS-APR-16 | FS-AGG-03 |
| DS-APR-17 | FS-AGG-04 |
| DS-APR-18 | FS-AGG-05 |
| DS-APR-19 | FS-AGG-06 |
| DS-APR-20 | FS-AGG-07 |
| DS-APR-21 | FS-TREND-01 |
| DS-APR-22 | FS-TREND-01 |
| DS-APR-23 | FS-TREND-02 |
| DS-APR-24 | FS-TREND-03 |
| DS-APR-25 | FS-TREND-04 |
| DS-APR-26 | FS-TREND-05 |
| DS-APR-27 | FS-OOS-01 |
| DS-APR-28 | FS-OOS-02 |
| DS-APR-29 | FS-OOS-03 |
| DS-APR-30 | FS-OOS-04 |
| DS-APR-31 | FS-STAB-01 |
| DS-APR-32 | FS-STAB-02 |
| DS-APR-33 | FS-STAB-03 |
| DS-APR-34 | FS-STAB-04 |
| DS-APR-35 | FS-VS-01 |
| DS-APR-36 | FS-VS-02 |
| DS-APR-37 | FS-VS-03 |
| DS-APR-38 | FS-SUP-01 |
| DS-APR-39 | FS-SUP-02 |
| DS-APR-40 | FS-SUP-03 |
| DS-APR-41 | FS-REC-01 |
| DS-APR-42 | FS-REC-02 |
| DS-APR-43 | FS-REC-03 |
| DS-APR-44 | FS-REC-04 |
| DS-APR-45 | FS-REC-05 |
| DS-APR-46 | FS-VAR-01 |
| DS-APR-47 | FS-VAR-02 |
| DS-APR-48 | FS-VAR-03 |
| DS-APR-49 | FS-MULTI-01 |
| DS-APR-50 | FS-MULTI-02 |
| DS-APR-51 | FS-MULTI-03 |
| DS-APR-52 | FS-AUD-01 |
| DS-APR-53 | FS-AUD-02 |
| DS-APR-54 | FS-AUD-03 |
| DS-APR-55 | FS-AUD-04 |
| DS-APR-56 | FS-PART11-10 |
| DS-APR-57 | FS-PART11-50 |
| DS-APR-58 | FS-PART11-70 |
| DS-APR-59 | FS-PART11-100 |
| DS-APR-60 | FS-PART11-200 |
| DS-APR-61 | FS-DI-01 |
| DS-APR-62 | FS-DI-02 |
| DS-APR-63 | FS-DI-03 |
| DS-APR-64 | FS-DI-04 |
| DS-APR-65 | FS-DI-05 |
| DS-APR-66 | FS-INT-LIMS-01 |
| DS-APR-67 | FS-INT-MES-01 |
| DS-APR-68 | FS-INT-EQMS-01 |
| DS-APR-69 | FS-INT-PV-01 |
| DS-APR-70 | FS-INT-STAB-01 |
| DS-APR-71 | FS-INT-VLM-01 |
| DS-APR-72 | FS-INT-COLDCHAIN-01 |
| DS-APR-73 | FS-INT-SER-01 |
| DS-APR-74 | FS-INT-VAULT-01 |
| DS-APR-75 | FS-PERF-01 |
| DS-APR-76 | FS-AV-01 |
| DS-APR-77 | FS-BAK-01 |
| DS-APR-78 | FS-SEC-01 / FS-XSYS-AD-01 |
| DS-APR-79 | FS-TRN-01 |
| DS-APR-80 | FS-PR-01 |

**FS-IDs in parent FS NOT covered (with rationale):**

- FS-DEV-03 (Container-image signing + cosign + ArgoCD-gated CR) — **vendor-internal — no site design surface**: handled by Sparta SDLC for the platform; site-authored extension deployment uses Sparta's loading mechanism, not direct container signing. Site escrow (DS-APR-02) provides business-continuity coverage.
- FS-DEV-04 (Dependency hash-pinning + SBOM CycloneDX) — **partly vendor-internal**: handled by Sparta for the platform; site-authored extensions follow the Cat 5 sub-component SDLC in § 8.1 which includes SBOM.
- FS-XSYS-BAK-01 (Veeam backup integration) — covered at site enterprise-backup-service DS level per `AUR-URS-BACKUP-001`.
- FS-XINT-EQMS-02 (eQMS status webhook) — covered in § 7 IF-EQMS-CAPA-01 integration; status-callback handled by TrackWise APR's CAPA-status reconciliation job.

## 11. Appendix B — Design-level Risk Register

| DR-ID | Design-stage risk | Origin design choice | Mitigation reference |
|---|---|---|---|
| DR-01 | Vendor-class change from Cat 5 (URS/FS) to Cat 4 (DS) could leave Cat 5 site-SDLC obligations partly uncovered | Class change documented in Revision History + DS-APR-01..04 | Vendor-assurance pack DS-APR-01 + site-extension mini-SDS § 8.1 cover the gap; PR review item |
| DR-02 | SPC ruleset defect in vendor module (Western Electric / Nelson mis-implemented) | DS-APR-06 vendor default | DS-APR-07 AIAG reference-dataset verification + OQ negative tests |
| DR-03 | Capability index Cpk false-positive on small-sample (n < 30) data | DS-APR-13 small-sample display logic | Statistician review gate + render-side suppression |
| DR-04 | Source-system schema drift breaking aggregation | DS-APR-09 extractor integrity check | Pre-run validator fails fast; reconciliation nightly catches gradual drift |
| DR-05 | EU PQR variant misses critical IPC / starting-material section vs FDA APR | DS-APR-46 + DS-APR-47 | Section-coverage validator (§ 5.4); variant-misconfig test in PQ |
| DR-06 | Stability OOS / shelf-life change missed due to Halcyon integration lag | DS-APR-31 + DS-APR-32 | Freshness check at run-init; alert if Halcyon snapshot > 24 h stale |
| DR-07 | Supplier-quality scorecard misalignment with eQMS supplier-CAPA register | DS-APR-38 + DS-APR-39 | Cross-reconciliation at run-time; flag mismatches in Recommendations |
| DR-08 | Audit-trail tampering / SoD bypass at sign-off | DS-APR-53 + DS-APR-44 + DS-APR-59 | DB role grants + state-machine enforcement + AD uniqueness; monthly QA review |
| DR-09 | Multi-product silent pooling | DS-APR-49 run-init validator | `MultiProductDisallowedError`; OQ-SINGLE-PRODUCT-01 |
| DR-10 | Site-authored extractor extension (§ 8.1) defect could yield wrong source data | Cat 5 sub-component SDLC | ≥ 90% test coverage + reference-output regression; CR-gated deployment |
| DR-11 | Variant misconfig at run-init (operator selects wrong variant flag) | DS-APR-46 | Section-coverage validator catches downstream missing-section condition |
| DR-12 | Vendor Sparta TrackWise release could change SPC default rule numbering | DS-APR-06 vendor-default reliance | Vendor-release impact-assessment SLA DS-APR-03; OQ-SPC-RULES-01 re-run at every release |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
