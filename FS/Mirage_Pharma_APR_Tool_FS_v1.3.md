---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "MIR-URS-APR-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd Ed., 2022) Cat 5 conventions"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200"
  - "21 CFR Part 211 § 211.180(e); EU GMP Annex 11; EU GMP Chapter 1 § 1.10"
  - "ICH Q9(R1); ICH Q10"
  - "PIC/S PI 041; ISO 22514-2:2017; WHO TRS 970 Annex 6"
parent_urs:
  document_number: MIR-URS-APR-001
  version: 1.2
  file: ../../URS/_generated/final/Annual_Product_Review_Tool__Mirage_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Annual Product Review (APR / PQR) Tool — Site-Developed Python + Postgres + Quarto

**Document Number:** MIR-FS-APR-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** MIR-URS-APR-001 v1.2 | **Site:** Mirage Pharma (fictional)
**System Class:** GAMP Cat 5 — Custom Application
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 211 § 211.180(e); EU GMP Annex 11; EU GMP Chapter 1 § 1.10; ICH Q9(R1); ICH Q10; PIC/S PI 041; WHO TRS 970 Annex 6

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Quality Operations) | _____________ | _____________ | _____ |
| Reviewer (Statistician) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | v1.2 alignment with URS v1.2; every URS-ID expanded into its own FS-ID row per METHODOLOGY § 2A.7. Added aggregation, trend / capability engine, OOS / OOT compiler, stability / validation-status / supplier review modules, recommendations + signoff workflow, FDA / EU variant logic, multi-product + multi-site mode. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

Specify the APR / PQR tool to satisfy `MIR-URS-APR-001` v1.2.

## 2. Scope

Site-developed Python services on K8s; Postgres warehouse; Quarto-based report rendering; integrations with LIMS, PAS-X, MasterControl, Sirius PV, Halcyon Stability, ValGenesis VLM, Selene Cold-Chain, Atlas Serialization; SSO via Okta; Vault archival.

## 3. System Architecture

```
   ┌─────────────────────────────────────────────────────────────┐
   │   Source GxP systems                                        │
   │   LIMS · PAS-X · eQMS · PV · Stability · VLM · CC · Atlas    │
   └────────────────┬────────────────────────────────────────────┘
                    │ read-only views + REST (snapshotted)
                    ▼
   ┌─────────────────────────────────────────────────────────────┐
   │   APR / PQR tool (Python on K8s, Cat 5)                     │
   │   ┌─────────────────┐  ┌─────────────────┐                   │
   │   │ Extractors      │  │ SPC + Capability │                   │
   │   │ (per source)    │  │ engine           │                   │
   │   └─────────────────┘  └─────────────────┘                   │
   │   ┌─────────────────┐  ┌─────────────────┐                   │
   │   │ OOS/OOT compiler│  │ Stability /     │                   │
   │   │                 │  │ VLM / Supplier  │                   │
   │   └─────────────────┘  └─────────────────┘                   │
   │   ┌─────────────────┐  ┌─────────────────┐                   │
   │   │ Recommendations │  │ Variant engine  │                   │
   │   │ register        │  │ (FDA / EU / WHO)│                   │
   │   └─────────────────┘  └─────────────────┘                   │
   │           Postgres warehouse + Quarto renderer               │
   └────────────────┬────────────────────────────────────────────┘
                    │ approved report (PDF + Excel + CSV)
                    ▼
              Vault QualityDocs (archival, ≥ 25 y)
```

### 3.1 Component Inventory

| ID | Component | GAMP Cat | Notes |
|---|---|---|---|
| C-01 | APR / PQR service (Python 3.12) | 5 | site-developed |
| C-02 | Postgres 16 warehouse | 4 | configured |
| C-03 | Quarto renderer | 3 | COTS |
| C-04 | LabWare LIMS 8 | 4 | source (separate URS) |
| C-05 | Werum PAS-X v3.2 | 4 | source (separate URS) |
| C-06 | MasterControl eQMS | 4 | source (separate URS) |
| C-07 | Sirius PV | 4 | source (separate URS) |
| C-08 | Halcyon Stability | 4 | source (separate URS) |
| C-09 | ValGenesis VLM | 4 | source (separate URS) |
| C-10 | Veeva Vault QualityDocs 24R1 | 4 | sink |
| C-11 | Okta SAML 2.0 + MFA | (infra) | SSO |

## 4. Functional Specifications

### 4.1 Application Lifecycle (Cat 5 SDLC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DEV-01 | URS-DEV-01 | SDLC documented in `MIR-SDLC-APR-001`: code review (≥ 1 approver, ≥ 1 architect), unit tests via pytest with line + branch coverage ≥ 85% (enforced via CI gate), integration tests against mocked source-system fixtures, security scan via Snyk + SonarQube, regression suite includes one representative APR + one representative PQR. |
| FS-DEV-02 | URS-DEV-02 | GitLab `mirage/apr-prr` repo on validated GitLab instance (HYP-URS-GIT-001); protected-branch policy on `main` + `release/*`; signed commits required (Sigstore gitsign); MR approval rules enforced server-side. |
| FS-DEV-03 | URS-DEV-03 | Container images built with `BuildKit`; signed via `cosign sign`; deployment via ArgoCD requires Change Request approval; rollback runbook `MIR-RB-APR-ROLLBACK-001` exercised at every release. |
| FS-DEV-04 | URS-DEV-04 | `poetry lock --hash` pins dependencies; SBOM produced via Syft (CycloneDX format); SBOM uploaded to Vault QualityDocs per release. |

### 4.2 Aggregation and Calculation Rules

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RULE-01 | URS-RULE-01 | Template files (`.qmd`) under Vault QualityDocs lifecycle `MIR-LC-TMPL-001` (DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE); statistician + QA co-approval at EFFECTIVE; Author ≠ Approver enforced by Vault role mapping. |
| FS-RULE-02 | URS-RULE-02 | SPC engine implements Western Electric Rules 1–4 (1 pt > 3σ; 2 of 3 > 2σ; 4 of 5 > 1σ; 8 in a row same side) + Nelson Rules 1–8; OQ runs the engine against the AIAG SPC reference dataset and verifies bit-identical rule firings. |
| FS-RULE-03 | URS-RULE-03 | Aggregation SQL views are deterministic (no `random_sample`, no `now()` in joins); the (product, year, source-snapshot-hash) tuple is the cache key; re-running with the same key returns bit-identical CSV. |
| FS-RULE-04 | URS-RULE-04 | Each extractor emits `row_count + sha256_manifest`; reconciliation gate checks `row_count == source_count` and `sha256 == source_sha`; mismatch raises `ExtractorIntegrityError` and blocks the run. |
| FS-RULE-05 | URS-RULE-05 | Capability engine: Anderson–Darling normality test (α = 0.05); on rejection, Box–Cox transform applied or non-parametric Clements-method Cpk used per attribute config; ISO 22514-2 formulas; OQ reference dataset spans normal + lognormal + bi-modal. |
| FS-RULE-06 | URS-RULE-06 | Capability index display logic: n ≥ 30 → "valid"; 10 ≤ n < 30 → "indicative only — small-sample"; n < 10 → suppressed with reason `INSUFFICIENT_N`; rendered in red on the Quarto report. |

### 4.3 Data Aggregation Sources

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AGG-01 | URS-AGG-01 | PAS-X extractor uses the `BATCH_YIELDS` + `DEVIATIONS` + `IPC_RESULTS` read-only DB views (PAS-X DataSphere); pulls (product_family, period); idempotency key = (product, year, run_id). |
| FS-AGG-02 | URS-AGG-02 | LIMS extractor REST: `GET /api/v2/results?product={p}&from={d1}&to={d2}&status=APPROVED`; pulls release-test + OOS + OOT + stability records; service account in HashiCorp Vault. |
| FS-AGG-03 | URS-AGG-03 | MasterControl extractor: `GET /api/eqms/deviations,capa,changecontrol,supplier-complaints?product={p}&from={d1}&to={d2}`; root-cause classifications mapped per `MIR-CFG-RC-MAP-001`. |
| FS-AGG-04 | URS-AGG-04 | Sirius PV extractor REST; severity classes (S1–S4) + PV signal classes mapped per `MIR-CFG-PV-MAP-001`. |
| FS-AGG-05 | URS-AGG-05 | Selene Cold-Chain extractor: `GET /api/excursions?product={p}` with batch-id linkage. |
| FS-AGG-06 | URS-AGG-06 | Atlas Serialization extractor: pulls recall / counterfeit / aggregation-anomaly events per product GTIN. |
| FS-AGG-07 | URS-AGG-07 | Snapshot manifest: per extraction, write `{source, timestamp, row_count, sha256}` to `apr_snapshots` table + immutable S3 bucket (object-lock 25 y). |

### 4.4 Trend Analysis and Capability Indices

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TREND-01 | URS-TREND-01 | Chart catalogue: X̄-R, X̄-s, I-MR, p-chart, np-chart, c-chart, u-chart, EWMA, CUSUM. Chart selection per CQA / CPP per `MIR-CFG-CHART-MAP-001`. Implementation: `numpy + scipy.stats + matplotlib`. |
| FS-TREND-02 | URS-TREND-02 | Rule-firing engine emits `(batch_id, attribute, rule_no, ruleset, timestamp)` tuples to `rule_firings` table; rendered as annotated chart markers + footnote table. |
| FS-TREND-03 | URS-TREND-03 | Phase 1 (Cp / Cpk over recent stable phase) vs Phase 2 (Pp / Ppk over review period): phase boundary = last EFFECTIVE-status change-control with `process_impact=YES` per the eQMS classification. |
| FS-TREND-04 | URS-TREND-04 | Trend-commentary field required when any rule fires; pre-render check blocks sign-off via `BlockingValidationError` if commentary empty. |
| FS-TREND-05 | URS-TREND-05 | EWMA chart with `λ = 0.2` default; per-attribute override in `MIR-CFG-EWMA-001`; control limits `μ ± L·σ·sqrt(λ/(2-λ))` with `L = 3` default. |

### 4.5 OOS / OOT Review Compilation

| FS ID | URS ID | Specification |
|---|---|---|
| FS-OOS-01 | URS-OOS-01 | OOS compiler queries LIMS `OOS_INVESTIGATIONS` + eQMS `INVESTIGATION_LINKED_DEVIATION`; renders table sorted by detection date; root cause taxonomy per FDA OOS Guidance (2006). |
| FS-OOS-02 | URS-OOS-02 | OOT compiler: rule firings + LIMS `OOT_FLAGS` + statistician-curated OOT registry; renders table with detection mechanism column. |
| FS-OOS-03 | URS-OOS-03 | Open-investigation gate: any OOS / OOT with `status != CLOSED` at run-time triggers acknowledgement modal in the sign-off UI; Statistician + QA Approver must acknowledge or sign-off is blocked. |
| FS-OOS-04 | URS-OOS-04 | OOS rate = `count(OOS_investigations) / count(batches_released)`; trended over prior 3 review periods; chart embedded in report. |

### 4.6 Stability Data Review

| FS ID | URS ID | Specification |
|---|---|---|
| FS-STAB-01 | URS-STAB-01 | Halcyon Stability extractor: `GET /api/stability/protocols?product={p}` + `GET /api/stability/q1e?product={p}`; renders protocol status table with time-point completion %. |
| FS-STAB-02 | URS-STAB-02 | Stability OOS / OOT linkage: cross-references LIMS stability results with status = OOS or OOT; clickable link to eQMS investigation. |
| FS-STAB-03 | URS-STAB-03 | Proposed shelf-life change: pulled from Halcyon `q1e_shelf_life_changes` table with confidence intervals; statistician approval reference captured per ICH Q1E. |
| FS-STAB-04 | URS-STAB-04 | Photostability (ICH Q1B) + bracketing / matrixing (ICH Q1D) coverage status pulled from Halcyon protocol metadata. |

### 4.7 Validation Status Review

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VS-01 | URS-VS-01 | ValGenesis VLM extractor: `GET /api/vlm/systems-status?product={p}`; renders system-status table grouped by equipment / utility / computerised. |
| FS-VS-02 | URS-VS-02 | Expired-PR flag, revalidation-overdue flag, open-CSV-deviation flag pulled per system; rendered as red badges with required-acknowledgement modal at QA approval. |
| FS-VS-03 | URS-VS-03 | PQ-run-count metric: count of executed PQ-protocol records in the review period per critical system. |

### 4.8 Supplier Quality Review

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SUP-01 | URS-SUP-01 | Supplier extractor: MasterControl `SUPPLIER_SCORECARDS` view per critical supplier; KPI columns: lot-acceptance rate, on-time delivery, complaint rate, audit status. |
| FS-SUP-02 | URS-SUP-02 | Downgrade detection: any `supplier_status in (PROBATION, DISQUALIFIED)` or `qualification_expiry < run_date` or open supplier-CAPA → flag + Recommendations register entry. |
| FS-SUP-03 | URS-SUP-03 | Supplier-audit details: last audit date, status, open observations per critical supplier. |

### 4.9 Recommendations + Sign-off Workflow

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REC-01 | URS-REC-01 | Recommendations register stored in `apr_recommendations` table with foreign keys to CAPA, source finding, and prior-year recommendation; UI grid in Quarto report's interactive HTML companion. |
| FS-REC-02 | URS-REC-02 | Carry-forward job at run-init: copies prior-year unclosed recommendations with aging-days computed; surfaces in section "Carried Forward". |
| FS-REC-03 | URS-REC-03 | Sign-off state machine: `DRAFT → AUTHORED → STATS-REVIEWED → QA-REVIEWED → QA-APPROVED → QP-APPROVED (EU)`. Each transition records (user, timestamp, role, meaning). |
| FS-REC-04 | URS-REC-04 | State machine enforces sequential transitions; `QA-APPROVED` cannot be entered without `QA-REVIEWED`; tested per OQ-SIGN-OFF-SEQUENTIAL-01. |
| FS-REC-05 | URS-REC-05 | Re-auth at each signing event: Okta step-up MFA via OIDC `acr_values=urn:okta:mfa:strong`; failure aborts signing. |

### 4.10 EU PQR vs FDA APR Variant Logic

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VAR-01 | URS-VAR-01 | Variant flag (`APR` / `PQR` / `APR+PQR` / `WHO`) selected at run-init; template engine includes / excludes section partials per variant-config table `MIR-CFG-VARIANT-SECTIONS-001`. |
| FS-VAR-02 | URS-VAR-02 | Combined APR + PQR: union of section sets; section-coverage cross-reference table generated at end of report. |
| FS-VAR-03 | URS-VAR-03 | WHO TRS 970 Annex 6 variant: adds prequalification-specific sections (re-qualification status, WHO commitments). |

### 4.11 Multi-Product and Multi-Site Mode

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MULTI-01 | URS-MULTI-01 | Run-init validator: `assert len(products) == 1`; raises `MultiProductDisallowedError` otherwise. |
| FS-MULTI-02 | URS-MULTI-02 | Per-site sections: extractor sub-divides by `manufacturing_site` field; sections rendered per site; no cross-site pooling unless `--allow-pooled-stats` flag explicitly set + QA approver-2 signature captured. |
| FS-MULTI-03 | URS-MULTI-03 | Portfolio view: read-only Quarto dashboard aggregating compliance signals (OOS rate, recommendation backlog, stability OOS count) across products; refreshed on every product-run completion. |

### 4.12 Audit Trail / 21 CFR Part 11 / ALCOA+ / Data Integrity

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit trail in `apr_audit` table (append-only via Postgres role grants); fields: event_id, user_id, action, entity_type, entity_id, before_hash, after_hash, timestamp; per 21 CFR § 11.10(e). |
| FS-AUD-02 | URS-AUD-02 | Append-only enforced at DB role-grant level: `apr_app` role has `INSERT` only on `apr_audit`; no `UPDATE / DELETE` grant; super-user access requires break-glass + audit-trail review. |
| FS-AUD-03 | URS-AUD-03 | QA Compliance monthly review run; review evidence template `MIR-PR-AUD-001` filed in Vault. |
| FS-AUD-04 | URS-AUD-04 | Audit retention ≥ 25 y on Postgres + nightly export to S3 with object-lock; verified per PQ-RETENTION-01. |
| FS-PART11-10 | URS-PART11-10 | Validation procedure (`MIR-SOP-CSV-001`) + copy-generation API (`GET /api/runs/{id}/export?format=pdf,xlsx,csv`) per 21 CFR § 11.10(a)–(c). |
| FS-PART11-50 | URS-PART11-50 | Signature manifestation: rendered on report cover + audit-trail (printed-name + UTC-timestamp + meaning per § 11.50). |
| FS-PART11-70 | URS-PART11-70 | Signature binding: SHA-256 of report + signature timestamp + user-id signed via Sigstore; verifiable post-hoc per § 11.70. |
| FS-PART11-100 | URS-PART11-100 | Okta enforces unique user-id; deactivated accounts cannot be reassigned; configured per § 11.100. |
| FS-PART11-200 | URS-PART11-200 | Okta step-up MFA on every signing event per § 11.200(a)(1). |
| FS-DI-01 | URS-DI-01 | Every audit-trail event carries `user_id` from Okta JWT `sub` claim. |
| FS-DI-02 | URS-DI-02 | Report rendered as PDF/A-3 + Excel + structured CSV; all three identically signed. |
| FS-DI-03 | URS-DI-03 | NTP-synced system clock (chrony); skew alert at > 1 s. |
| FS-DI-04 | URS-DI-04 | Source snapshots preserved in immutable S3 (object-lock 25 y) referenced by manifest SHA. |
| FS-DI-05 | URS-DI-05 | Numeric accuracy verified per OQ reference dataset. |

### 4.13 Integrations / Performance / Security / Training / Periodic Review

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | LIMS REST + DB read-replica; auth via OAuth2 client-credentials; service account in HashiCorp Vault. |
| FS-INT-MES-01 | URS-INT-MES-01 | PAS-X DataSphere read-only views; auth via AD service account. |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | MasterControl REST per `MIR-IF-EQMS-001`; rate-limit 60 req/min. |
| FS-INT-PV-01 | URS-INT-PV-01 | Sirius PV REST. |
| FS-INT-STAB-01 | URS-INT-STAB-01 | Halcyon Stability REST. |
| FS-INT-VLM-01 | URS-INT-VLM-01 | ValGenesis VLM REST. |
| FS-INT-COLDCHAIN-01 | URS-INT-COLDCHAIN-01 | Selene Cold-Chain REST. |
| FS-INT-SER-01 | URS-INT-SER-01 | Atlas Serialization REST. |
| FS-INT-VAULT-01 | URS-INT-VAULT-01 | Vault QualityDocs REST push of approved APR / PQR (PDF + Excel + CSV + audit-trail export). |
| FS-PERF-01 | URS-PERF-01 | P95 single-product run ≤ 60 min wall-clock; measured by PQ across the product portfolio. |
| FS-AV-01 | URS-AV-01 | Availability target 99.0% during the annual run window; monitored via Prometheus + alertmanager. |
| FS-BAK-01 | URS-BAK-01 | pg_basebackup + WAL archival nightly to S3; quarterly restore test witnessed by QA per `MIR-RB-RESTORE-001`. |
| FS-SEC-01 | URS-SEC-01 | Okta SAML 2.0 + MFA; service-account secrets in HashiCorp Vault; quarterly access review. |
| FS-TRN-01 | URS-TRN-01 | Cornerstone curriculum `MIR-CURR-APR-Operator-v1`; statistician competency assessment includes SPC + capability indices. |
| FS-PR-01 | URS-PR-01 | Annual periodic review per `MIR-PR-APR-YYYYMMDD`; signed by Director Quality Operations + VP QA. |


### 4.14 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem. Conditional-access binding to policy `Quality-App Conditional Access (MFA on first logon per session)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the APR data-mart; tier classification = T3; RPO ≤ 72 h; RTO ≤ 72 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; annual QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.15 Cross-System Integration — eQMS handover (M-XINT-EQMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-EQMS-01 | URS-XINT-EQMS-01 | CAPA-event publisher posts to eQMS endpoint `POST /capa/tickets` with mTLS + Entra workload-identity; payload schema `eqms.ticket.v1`; OpenAPI artefact `xint-eqms.openapi.yaml`; outbound retry with exponential back-off and DLQ at 5 attempts. |
| FS-XINT-EQMS-02 | URS-XINT-EQMS-02 | eQMS ticket-status webhook subscribed; payload `eqms.status.v1`; consumer rule maps eQMS status `(OPEN, IN-PROGRESS, EFFECTIVENESS, CLOSED)` onto originating-record disposition fields; closed-loop verification gate prevents disposition without `eqms_status=CLOSED`. |

## 5. Configuration Items (CI)

| CI ID | Item | Value |
|---|---|---|
| CI-01 | SPC rule sets | Western Electric Rules 1–4 + Nelson Rules 1–8 (per attribute config) |
| CI-02 | Capability normality test | Anderson–Darling, α = 0.05 |
| CI-03 | Capability small-sample threshold | n < 30 indicative; n < 10 suppressed |
| CI-04 | Phase boundary rule | last EFFECTIVE process-impact CR closure date |
| CI-05 | EWMA λ default | 0.2 |
| CI-06 | OOS-rate trend window | prior 3 review periods |
| CI-07 | Sign-off sequence | Author → Stats → QA-R → QA-A → QP(EU) |
| CI-08 | Variant flags | APR / PQR / APR+PQR / WHO |
| CI-09 | Multi-product disallow | enforced at run-init |
| CI-10 | Audit retention | ≥ 25 y |

## 6. Risks (FS-level)

| Risk | Mitigation |
|---|---|
| Source-system schema drift breaking aggregation | FS-DEV-01 + FS-RULE-04 + integration tests in CI |
| SPC rule defect | FS-RULE-02 + reference-data OQ |
| Capability index false-positive on small sample | FS-RULE-06 + render gate |
| Audit-trail tampering | FS-AUD-02 + DB role grants |
| Variant misconfig (FDA section missing on EU PQR) | FS-VAR-01 + variant test in PQ |
| Multi-product silent pooling | FS-MULTI-01 + run-init validator |

## 7. References

- MIR-URS-APR-001 v1.2 (parent URS)
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200
- 21 CFR Part 211 § 211.180(e); EU GMP Annex 11; EU GMP Chapter 1 § 1.10
- ICH Q9(R1); ICH Q10
- PIC/S PI 041; WHO TRS 970 Annex 6
- ISO 22514-2:2017
- ISPE GAMP 5 (2nd Edition, 2022)
- Vendor: LabWare LIMS 8; Werum PAS-X v3.2; MasterControl eQMS; Sirius PV; Halcyon Stability; ValGenesis VLM; Veeva Vault QualityDocs 24R1

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID | Notes |
|---|---|---|
| URS-DEV-01 | FS-DEV-01 | |
| URS-DEV-02 | FS-DEV-02 | |
| URS-DEV-03 | FS-DEV-03 | |
| URS-DEV-04 | FS-DEV-04 | |
| URS-RULE-01 | FS-RULE-01 | |
| URS-RULE-02 | FS-RULE-02 | |
| URS-RULE-03 | FS-RULE-03 | |
| URS-RULE-04 | FS-RULE-04 | |
| URS-RULE-05 | FS-RULE-05 | |
| URS-RULE-06 | FS-RULE-06 | |
| URS-AGG-01 | FS-AGG-01 | |
| URS-AGG-02 | FS-AGG-02 | |
| URS-AGG-03 | FS-AGG-03 | |
| URS-AGG-04 | FS-AGG-04 | |
| URS-AGG-05 | FS-AGG-05 | |
| URS-AGG-06 | FS-AGG-06 | |
| URS-AGG-07 | FS-AGG-07 | |
| URS-TREND-01 | FS-TREND-01 | |
| URS-TREND-02 | FS-TREND-02 | |
| URS-TREND-03 | FS-TREND-03 | |
| URS-TREND-04 | FS-TREND-04 | |
| URS-TREND-05 | FS-TREND-05 | |
| URS-OOS-01 | FS-OOS-01 | |
| URS-OOS-02 | FS-OOS-02 | |
| URS-OOS-03 | FS-OOS-03 | |
| URS-OOS-04 | FS-OOS-04 | |
| URS-STAB-01 | FS-STAB-01 | |
| URS-STAB-02 | FS-STAB-02 | |
| URS-STAB-03 | FS-STAB-03 | |
| URS-STAB-04 | FS-STAB-04 | |
| URS-VS-01 | FS-VS-01 | |
| URS-VS-02 | FS-VS-02 | |
| URS-VS-03 | FS-VS-03 | |
| URS-SUP-01 | FS-SUP-01 | |
| URS-SUP-02 | FS-SUP-02 | |
| URS-SUP-03 | FS-SUP-03 | |
| URS-REC-01 | FS-REC-01 | |
| URS-REC-02 | FS-REC-02 | |
| URS-REC-03 | FS-REC-03 | |
| URS-REC-04 | FS-REC-04 | |
| URS-REC-05 | FS-REC-05 | |
| URS-VAR-01 | FS-VAR-01 | |
| URS-VAR-02 | FS-VAR-02 | |
| URS-VAR-03 | FS-VAR-03 | |
| URS-MULTI-01 | FS-MULTI-01 | |
| URS-MULTI-02 | FS-MULTI-02 | |
| URS-MULTI-03 | FS-MULTI-03 | |
| URS-AUD-01 | FS-AUD-01 | |
| URS-AUD-02 | FS-AUD-02 | |
| URS-AUD-03 | FS-AUD-03 | |
| URS-AUD-04 | FS-AUD-04 | |
| URS-PART11-10 | FS-PART11-10 | |
| URS-PART11-50 | FS-PART11-50 | |
| URS-PART11-70 | FS-PART11-70 | |
| URS-PART11-100 | FS-PART11-100 | |
| URS-PART11-200 | FS-PART11-200 | |
| URS-DI-01 | FS-DI-01 | |
| URS-DI-02 | FS-DI-02 | |
| URS-DI-03 | FS-DI-03 | |
| URS-DI-04 | FS-DI-04 | |
| URS-DI-05 | FS-DI-05 | |
| URS-INT-LIMS-01 | FS-INT-LIMS-01 | |
| URS-INT-MES-01 | FS-INT-MES-01 | |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 | |
| URS-INT-PV-01 | FS-INT-PV-01 | |
| URS-INT-STAB-01 | FS-INT-STAB-01 | |
| URS-INT-VLM-01 | FS-INT-VLM-01 | |
| URS-INT-COLDCHAIN-01 | FS-INT-COLDCHAIN-01 | |
| URS-INT-SER-01 | FS-INT-SER-01 | |
| URS-INT-VAULT-01 | FS-INT-VAULT-01 | |
| URS-PERF-01 | FS-PERF-01 | |
| URS-AV-01 | FS-AV-01 | |
| URS-BAK-01 | FS-BAK-01 | |
| URS-SEC-01 | FS-SEC-01 | |
| URS-TRN-01 | FS-TRN-01 | |
| URS-PR-01 | FS-PR-01 | |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-EQMS-01 | FS-XINT-EQMS-01 |
| URS-XINT-EQMS-02 | FS-XINT-EQMS-02 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Source-system schema drift breaking aggregation | Medium | High | URS-DEV-01..02 + URS-RULE-04 + integration tests in CI |
| R-02 | SPC rule defect (Western Electric / Nelson misimplemented) | Medium | High | URS-RULE-02 + reference-data OQ |
| R-03 | Capability index Cpk false-positive on small-sample (n < 30) data | Medium | High | URS-RULE-06 + statistician review gate |
| R-04 | Incomplete data due to unreachable source at run-time | Medium | High | URS-RULE-04 + pre-run validator |
| R-05 | EU PQR variant misses critical IPC / starting-material section vs FDA APR | Low | High | URS-VAR-01 + variant test in PQ |
| R-06 | Stability OOS / shelf-life change missed due to integration lag | Low | High | URS-STAB-02 + URS-INT-STAB-01 freshness check |
| R-07 | Supplier-quality scorecard misalignment with eQMS supplier-CAPA register | Medium | Medium | URS-SUP-01 + cross-reconciliation at run-time |
| R-08 | Audit-trail tampering / SoD bypass at sign-off | Low | Critical | URS-AUD-02 + URS-REC-04 + URS-PART11-100 |

Full evaluation in `MIR-RA-APR-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
