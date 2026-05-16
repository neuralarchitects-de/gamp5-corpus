---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (v1.0 corpus genesis per METHODOLOGY § 2B)"
seed_corpus_basis:
  - "SLN-FS-COLDCHAIN-001 v1.2 (parent FS)"
  - "SLN-URS-COLDCHAIN-001 v1.2 (parent URS — transitive)"
  - "GAMP 5 (2nd ed.) Cat 4 SaaS"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11; EU GDP 2013/C 343/01; WHO TRS 957 Annex 9"
  - "USP <1079>; ICH Q1A(R2); IEC 60068-3-5"
  - "BfArM / Swissmedic / AGES GDP guidance"
parent_fs:
  document_number: SLN-FS-COLDCHAIN-001
  version: "1.2"
  file: "../../../FS_FDS/_generated/final/Selene_Sciences_Cold_Chain_Logger_FS_v1.3.md"
parent_urs:
  document_number: SLN-URS-COLDCHAIN-001
  version: "1.2"
  file: "../../../URS/_generated/final/Cold_Chain_Logger_Cloud_Platform__Selene_Sciences_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Cold-Chain Logger Cloud Platform — ELPRO Liberty Cloud + ecolog-NET LIB v2.4

**Document Number:** SLN-DS-COLDCHAIN-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** SLN-FS-COLDCHAIN-001 v1.2
**Parent URS:** SLN-URS-COLDCHAIN-001 v1.2 *(informational; transitive)*
**Site:** Selene Sciences AE, Distribution Hub Athens (GR HQ) + EU distribution centres in Konstanz (DE), Basel (CH), Wien (AT) *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS; vendor handles infrastructure; site validates configuration) + IoT loggers
**Project Mode:** Configuration project on commercial software product **ELPRO ecolog-NET LIB v2.4 + Liberty cloud** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GDP 2013/C 343/01; WHO TRS 957 Annex 9; USP <1079>; ICH Q1A(R2); IEC 60068-3-5; BfArM (DE), Swissmedic (CH), AGES PharmMed (AT) GDP requirements.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Cold-Chain Operations Manager — SME) | _____________ | _____________ | _____ |
| Reviewer (Vendor Assurance — ELPRO owner) | _____________ | _____________ | _____ |
| Reviewer (Stability Reviewer) | _____________ | _____________ | _____ |
| Reviewer (OT-Security Architect) | _____________ | _____________ | _____ |
| Approver (System Owner — Cold-Chain Logistics Lead) | _____________ | _____________ | _____ |
| Approver (Head of Supply Chain) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial issue. Inherited Tier T2–T3 from parent URS+FS pair (FS lands at 74 FS-IDs across § 4 + § 4.1 + § 4.2). DS covers 73/74 FS-IDs; 1 FS-ID flagged as vendor-internal — no site design surface (FS-AV-01 vendor-platform availability is governed by ELPRO SLA, not site DS). Generated as part of the DS v1.0 corpus ship per METHODOLOGY § 2B. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

DS-specific terms only — URS / FS definitions inherited by reference.

| Term | Definition |
|---|---|
| CS | Configuration Specification (this document, per GAMP 5 2nd ed. for Cat 4) |
| CI | Configuration Item — one configurable parameter, value, default-vs-custom flag, justification |
| LIB | ELPRO ecolog-NET LIB v2.4 — local infrastructure box (Linux appliance) deployed at each distribution hub |
| Liberty | ELPRO Liberty Cloud — multi-tenant SaaS |
| BLE / NFC logger | Bluetooth-Low-Energy / Near-Field-Communication temperature data-logger |
| CTNS | Cumulative Time Not Stored — stability-budget metric |
| TOR | Time Out of Refrigeration |
| Stability Budget | Per-product allowed cumulative excursion per ICH Q1A(R2) stability data |

## 1. Purpose

This Configuration Specification (CS) is the technical-design layer between `SLN-FS-COLDCHAIN-001` v1.2 and downstream configuration / IQ / OQ / PQ Protocols for the ELPRO Liberty Cloud + ecolog-NET LIB v2.4 cold-chain logger platform supporting GDP-regulated finished-product distribution from Selene Sciences across EU + DACH + LATAM markets. The DS declares, per configuration item, the chosen value, default-vs-custom flag, FS-ID(s) traced, and planned verification. Vendor internals (ELPRO Liberty cloud platform code; ELPRO LIB v2.4 firmware; logger firmware) are not redrawn here — those remain under ELPRO SDLC and are covered by the Vendor Assurance pack `VA-ELPRO-2026`.

## 2. Scope

### In scope

- ELPRO Liberty Cloud — Selene tenancy configuration (logger registration, commissioning workflow, profile lifecycle, evaluation engine, CTNS / stability-budget tracker, lane qualification, multi-tenant isolation).
- ELPRO ecolog-NET LIB v2.4 site-deployed boxes (4 units: Athens, Konstanz, Basel, Wien) — network and AD-binding configuration.
- Logger fleet master data (USB / BLE / NFC; single-use + reusable).
- Stability profiles per product / lane (URS § 5.3 lifecycle).
- Lane qualification + temperature-mapping evidence linkage (per IEC 60068-3-5 / USP <1079>).
- CTNS / stability-budget accumulators per product per batch (per ICH Q1A(R2)).
- Excursion → Halcyon Stability + MasterControl eQMS hand-off workflow.
- Reusable-logger reset SOP enforcement.
- Multi-tenant (CMO / CDMO) isolation via row-level security.
- Audit-trail bindings, 21 CFR Part 11 controls, GDP record-retention.
- Integration endpoints: SAP EWM (WMS holds), MasterControl (deviations), Halcyon Stability (excursion impact), carrier GPS feed, Okta SAML 2.0 + MFA.

### Out of scope

- ELPRO Liberty SaaS infrastructure internals (covered by vendor SOC 2 Type II + ISO 27001 + CSV summary).
- Logger calibration laboratory operations (ISO 17025 supplier scope).
- Carrier execution (carrier contracts).
- ERP general ledger (separate SAP S/4HANA URS).
- Serialization (Atlas Serialization separate URS).
- Refrigerator / chamber qualification (physical equipment URSs).

## 3. Architectural Overview

### 3.1 Logical view

```
                          Okta (SAML 2.0 + MFA)
                                    │
                                    ▼
   ┌─────────────────────────────────────────────────────────────────┐
   │  ELPRO Liberty Cloud — Selene tenancy (multi-tenant SaaS)        │
   │   ┌─────────────────────┐  ┌─────────────────────────────────┐    │
   │   │ Logger registry      │  │ Profile lifecycle (DRAFT→...→   │    │
   │   │ + commissioning      │  │   SUPERSEDED)                    │    │
   │   └─────────────────────┘  └─────────────────────────────────┘    │
   │   ┌─────────────────────┐  ┌─────────────────────────────────┐    │
   │   │ Evaluation engine    │  │ CTNS / stability-budget tracker │    │
   │   │ (Pass / Investigation │  └─────────────────────────────────┘    │
   │   │  / Reject)           │  ┌─────────────────────────────────┐    │
   │   └─────────────────────┘  │ Lane qualification + temp-map    │    │
   │   ┌─────────────────────┐  │ evidence store                    │    │
   │   │ Multi-tenant         │  └─────────────────────────────────┘    │
   │   │ row-level security   │                                          │
   │   └─────────────────────┘                                          │
   └─────────────┬─────────────────────────────┬────────────────────────┘
                 │                             │
                 ▼                             ▼
        Logger ingest (per hub)          Outbound integrations
   ┌──────────────────────────┐    ┌─────────────────────────────┐
   │ ELPRO LIB v2.4 — Athens  │    │ SAP EWM (WMS hold)            │
   │ ELPRO LIB v2.4 — Konstanz │   │ MasterControl (deviation)     │
   │ ELPRO LIB v2.4 — Basel    │   │ Halcyon Stability (impact)    │
   │ ELPRO LIB v2.4 — Wien     │   │ Carrier GPS feed              │
   └──────────────────────────┘    └─────────────────────────────┘
```

### 3.2 Logger fleet layout (text diagram)

```
┌── Single-use loggers (BLE) ─────────────────────────────────────────┐
│   ELPRO LIBERO ITS — ~3,500 active units across fleet                │
│   Commissioned at origin (Athens manufacturing); downloaded at       │
│   receiving hub (Konstanz / Basel / Wien / partner sites)            │
└──────────────────────────────────────────────────────────────────────┘
┌── Reusable loggers (USB + NFC) ──────────────────────────────────────┐
│   ELPRO LIBERO Cx — ~800 reusable units                              │
│   Reset SOP required before each redeployment (§ 5.3 workflow)       │
└──────────────────────────────────────────────────────────────────────┘
┌── Specialty loggers (-70 °C ultracold) ──────────────────────────────┐
│   ELPRO LIBERO TT — for vaccine cold-chain (selected products)       │
└──────────────────────────────────────────────────────────────────────┘
```

### 3.3 Multi-tenant partitioning

The Selene Liberty tenant hosts:

- Tenant `selene-prime` — Selene direct-distribution shipments (Athens-origin).
- Tenant `cmo-konstanz-1` — CMO partner Konstanz site (Selene-finished-product handling).
- Tenant `cdmo-basel-1` — CDMO partner Basel site (intermediate-product shipments).

Per-tenant data isolation via tenant-id partitioning + row-level security (DS-COLDCHAIN-46).

## 4. Configuration Specification

### 4.1 Vendor / Platform Assurance

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COLDCHAIN-01 | Vendor-assurance pack location | `VA-ELPRO-2026` dossier in Veeva Vault QualityDocs; SOC 2 Type II + ISO 27001 + customer-shared CSV + DPA tracked annually | Custom | FS-VND-01; ELPRO classified as critical SaaS vendor per site supplier-quality SOP. | FS-VND-01 | OQ-VND-PACK-01 |
| DS-COLDCHAIN-02 | Release-impact-assessment SLA | 14 days from ELPRO release-notes receipt; config-affecting changes raise re-validation CR | Custom | FS-VND-02; matches site change-control SOP. | FS-VND-02 | OQ-VND-RELEASE-01 |
| DS-COLDCHAIN-03 | TR-Audit cadence | Annual ELPRO TR-Audit summary filed in vendor-assurance dossier | Default | FS-VND-03. | FS-VND-03 | OQ-VND-AUDIT-01 |

### 4.2 Logger Registration and Commissioning

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COLDCHAIN-04 | Logger-registration table fields | serial, model, firmware, cal-cert-id, cal-due-date, tenant-binding | Default | FS-LOG-REG-01 + URS-LOG-REG-01. | FS-LOG-REG-01 | OQ-LOG-REG-01 |
| DS-COLDCHAIN-05 | Reusable-vs-single-use flag | `logger.reusable` boolean drives reset-SOP enforcement before redeployment | Default | FS-LOG-REG-02. | FS-LOG-REG-02 | OQ-LOG-REG-01 |
| DS-COLDCHAIN-06 | Commissioning binding | Logger → shipment-id + profile-version + lane-id; cryptographic binding (Ed25519 site key) | Custom | FS-LOG-COMM-01; Ed25519 chosen for performance + key-size advantages over RSA-2048. | FS-LOG-COMM-01 | OQ-LOG-COMM-01 |
| DS-COLDCHAIN-07 | Calibration-currency gate | Commissioning blocks with explicit error if `cal-due-date < now()`; UI shows expiry date | Custom | FS-LOG-COMM-02. | FS-LOG-COMM-02 | OQ-LOG-COMM-CAL-01 |
| DS-COLDCHAIN-08 | Chain-of-custody export endpoint | `GET /commission/export?shipment_id=...` returns PDF/A-3 + JSON | Custom | FS-LOG-COMM-03 + 21 CFR § 11.10(b). | FS-LOG-COMM-03 | OQ-LOG-COMM-EXPORT-01 |

### 4.3 Stability Profile Lifecycle

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COLDCHAIN-09 | Profile state machine | `DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED` | Default | FS-PROF-01. | FS-PROF-01 | OQ-PROF-LIFECYCLE-01 |
| DS-COLDCHAIN-10 | Profile schema fields | product_code, temp_range_low / high, MKT_limit, excursion_allowances[], stability_budget | Default | FS-PROF-02 + ICH Q1A(R2). | FS-PROF-02 | OQ-PROF-SCHEMA-01 |
| DS-COLDCHAIN-11 | EFFECTIVE-only commissioning rule | Commissioning rejects non-EFFECTIVE profile assignment with HTTP 409 | Default | FS-PROF-03. | FS-PROF-03 | OQ-PROF-LIFECYCLE-01 |
| DS-COLDCHAIN-12 | Profile transition SoD | Author ≠ Approver enforced at Okta-group → role mapping | Custom | FS-PROF-04. | FS-PROF-04 | OQ-PROF-SOD-01 |
| DS-COLDCHAIN-13 | EFFECTIVE-profile immutability | Read-only at DB role-grant level; edits create new version | Default | FS-PROF-05. | FS-PROF-05 | OQ-PROF-IMMUTABLE-01 |
| DS-COLDCHAIN-14 | Per-shipment profile-version stamp | Each shipment record stores `profile_version_used`; inspectable in shipment-detail view | Custom | FS-PROF-06. | FS-PROF-06 | OQ-PROF-VERSION-01 |

### 4.4 Shipment Profile Evaluation and Classification

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COLDCHAIN-15 | Logger-download integrity check | Vendor checksum + Ed25519 signature verified at download time; failure raises `LOGGER_INTEGRITY_EXCEPTION` | Custom | FS-EVAL-01. | FS-EVAL-01 | OQ-LOG-INTEGRITY-01 |
| DS-COLDCHAIN-16 | Classification states | `Pass / Excursion-Investigation / Reject`; ruleset versioned per release | Default | FS-EVAL-02. | FS-EVAL-02 | OQ-EVAL-CLASS-01 |
| DS-COLDCHAIN-17 | Manual override dual-signature | Investigator + Disposition-Approver signatures + reason capture; audit-trailed | Custom | FS-EVAL-03 + § 11.50 + § 11.200. | FS-EVAL-03 | OQ-EVAL-OVERRIDE-01 |
| DS-COLDCHAIN-18 | TOR calculator | Time Out of Refrigeration computed against lane TOR-allowance; reflected in classification | Custom | FS-EVAL-04. | FS-EVAL-04 | OQ-EVAL-TOR-01 |
| DS-COLDCHAIN-19 | Algorithm-version stamping | Each shipment record stamps `eval_algo_version` | Default | FS-EVAL-05. | FS-EVAL-05 | OQ-EVAL-VERSION-01 |

### 4.5 Lane Qualification and Temperature-Mapping

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COLDCHAIN-20 | Lane-configuration fields | origin, destination, mode (`air / road / sea`), carrier, season; temperature-mapping evidence linked via document-store URN | Default | FS-LANE-01 + IEC 60068-3-5 + USP <1079>. | FS-LANE-01 | OQ-LANE-CONFIG-01 |
| DS-COLDCHAIN-21 | Lane-qualification evidence linkage | Mapping reports, ambient-temperature data, packaging-spec validation linked from lane configuration to inspection-readiness export | Custom | FS-LANE-02. | FS-LANE-02 | OQ-LANE-EVIDENCE-01 |
| DS-COLDCHAIN-22 | Lane state machine | `Qualified / Provisional / Disqualified`; only Qualified lanes used in routine flow; Provisional requires enhanced monitoring + dual approval | Custom | FS-LANE-03. | FS-LANE-03 | OQ-LANE-STATE-01 |
| DS-COLDCHAIN-23 | Lane re-qualification cadence | Annual default; trigger events (carrier change, route change, packaging change) auto-create re-qualification CR | Custom | FS-LANE-04. | FS-LANE-04 | OQ-LANE-REQUAL-01 |
| DS-COLDCHAIN-24 | Season-profile auto-switch | Per shipment date using configurable date-window matrix (`summer / winter / shoulder`) | Custom | FS-LANE-05. | FS-LANE-05 | OQ-LANE-SEASON-01 |

### 4.6 21 CFR Part 11 / GDP Compliance

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COLDCHAIN-25 | § 11.10(a) procedural controls | Procedural-control SOPs in Vault QualityDocs; reviewed annually | Default | FS-PART11-01. | FS-PART11-01 | OQ-PART11-01 |
| DS-COLDCHAIN-26 | § 11.10(d) access control | Okta SAML 2.0 + MFA for tenant admin; logger device certificates for ingest | Custom | FS-PART11-02 + FS-XSYS-AD-01. | FS-PART11-02 | OQ-PART11-02 |
| DS-COLDCHAIN-27 | § 11.10(e) audit trail | Audit-trail schema per DS-COLDCHAIN-43 | Default | FS-PART11-03. | FS-PART11-03 | OQ-AUD-COVERAGE-01 |
| DS-COLDCHAIN-28 | § 11.50 signature manifestation | Signature events render printed name + UTC ISO-8601 timestamp + meaning text into audit-trail + shipment-record cover sheet | Default | FS-PART11-04. | FS-PART11-04 | OQ-PART11-04 |
| DS-COLDCHAIN-29 | § 11.70 cryptographic binding | HMAC-SHA-256 over `(record_id, record_state_hash, signer_id, meaning, ts)` | Custom | FS-PART11-05; ELPRO Liberty default HMAC mechanism. | FS-PART11-05 | OQ-PART11-05 |
| DS-COLDCHAIN-30 | § 11.100 uniqueness | Okta-DB unique constraint on user-id; deactivated accounts non-reassignable | Default | FS-PART11-06. | FS-PART11-06 | OQ-PART11-06 |
| DS-COLDCHAIN-31 | § 11.200 re-authentication | Okta step-up MFA at every disposition / profile / lane-qualification approval | Custom | FS-PART11-07. | FS-PART11-07 | OQ-PART11-07 |
| DS-COLDCHAIN-32 | § 11.300 password policy | Per site InfoSec policy (≥ 14 chars, MFA) | Default | FS-PART11-08. | FS-PART11-08 | OQ-PART11-08 |
| DS-COLDCHAIN-33 | EU GDP § 9 distribution evidence | Receiver country + time-stamped temperature record + QP assessment for excursion-impacted shipments | Default | FS-GDP-01 + EU GDP § 9. | FS-GDP-01 | OQ-GDP-EVIDENCE-01 |
| DS-COLDCHAIN-34 | WHO TRS 957 retention | Shelf-life of product + 1 year minimum; enforced at archive-tier policy | Default | FS-GDP-02 + WHO TRS 957 Annex 9. | FS-GDP-02 | OQ-RETENTION-01 |
| DS-COLDCHAIN-35 | USP <1079> risk strategy | Risk-based stability + transportation strategy captured per product; reviewed at periodic review | Default | FS-GDP-03. | FS-GDP-03 | OQ-USP-1079-01 |

### 4.7 CTNS / Stability Budget Tracking

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COLDCHAIN-36 | CTNS accumulator schema | Per product / batch: `ctns_seconds_above`, `ctns_seconds_below`; incremented at each excursion event | Custom | FS-CTNS-01. | FS-CTNS-01 | OQ-CTNS-ACCUM-01 |
| DS-COLDCHAIN-37 | Stability-budget cap | Per product per ICH Q1A(R2); stored on product master `product.stability_budget_seconds` | Custom | FS-CTNS-02. | FS-CTNS-02 | OQ-CTNS-BUDGET-01 |
| DS-COLDCHAIN-38 | CTNS-alert thresholds | 50% / 75% / 90% of stability budget consumed; alerts to Cold-Chain Logistics Lead + Stability Reviewer via email + dashboard | Custom | FS-CTNS-03. | FS-CTNS-03 | OQ-CTNS-ALERT-01 |
| DS-COLDCHAIN-39 | Silent-breach reconciliation job | `ctns-reconcile.py` runs daily; detects CTNS > budget without alert | Custom | FS-CTNS-04. | FS-CTNS-04 | OQ-CTNS-RECONCILE-01 |
| DS-COLDCHAIN-40 | CTNS export endpoint | `GET /ctns/export?product_id=...` returns JSON + CSV | Custom | FS-CTNS-05. | FS-CTNS-05 | OQ-CTNS-EXPORT-01 |

### 4.8 Excursion → Stability/QC Hand-off

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COLDCHAIN-41 | Halcyon impact-assessment push | REST POST including profile-version + lane + temperature-trace + CTNS-consumption fields | Custom | FS-HANDOFF-01. | FS-HANDOFF-01 | OQ-HANDOFF-HALCYON-01 |
| DS-COLDCHAIN-42 | MasterControl deviation push | Idempotency key = shipment-id; retry-safe | Custom | FS-HANDOFF-02 + FS-INT-EQMS-01. | FS-HANDOFF-02 | OQ-HANDOFF-EQMS-01 |
| DS-COLDCHAIN-43 | Disposition → Halcyon assessment-id linkage | Disposition decision links to Halcyon `assessment_id`; UI surfaces assessment outcome | Custom | FS-HANDOFF-03. | FS-HANDOFF-03 | OQ-HANDOFF-DISPO-01 |
| DS-COLDCHAIN-44 | Orphan-excursion reconciliation | Daily reconciliation detects orphan excursions (no Halcyon assessment within 24 h); alerts to ops queue | Custom | FS-HANDOFF-04. | FS-HANDOFF-04 | OQ-HANDOFF-ORPHAN-01 |

### 4.9 Reusable-Logger Reset SOP

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COLDCHAIN-45 | Reset SOP workflow | Data-wipe verification → battery check → calibration validity check → time-sync check; reset evidence captured | Custom | FS-RESET-01. | FS-RESET-01 | OQ-RESET-SOP-01 |
| DS-COLDCHAIN-46 | Battery pre-check threshold | Configurable per logger model: LIBERO Cx ≥ 80% battery; LIBERO ITS ≥ 90% (single-use) | Custom | FS-RESET-02; per-model threshold avoids mid-shipment exhaustion. | FS-RESET-02 | OQ-BATTERY-PRECHECK-01 |
| DS-COLDCHAIN-47 | Reset-failure handling | Blocks re-deployment; routes to Logger Operator triage queue | Custom | FS-RESET-03. | FS-RESET-03 | OQ-RESET-FAIL-01 |

### 4.10 Multi-Tenant (CMO / CDMO)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COLDCHAIN-48 | Tenant isolation mechanism | Tenant-id partitioning + PostgreSQL row-level security (RLS) policies per `tenant_id` | Custom | FS-TENANT-01; RLS chosen over schema-per-tenant for cost + ops efficiency. | FS-TENANT-01 | OQ-TENANT-ISOLATION-01 |
| DS-COLDCHAIN-49 | Cross-tenant audit access | Auditor role with documented `access_justification` field; per-event audit-trail entry | Custom | FS-TENANT-02. | FS-TENANT-02 | OQ-TENANT-XAUDIT-01 |
| DS-COLDCHAIN-50 | Tenant onboarding / off-boarding | Workflow with data-export + retention obligations enforced at off-boarding | Custom | FS-TENANT-03. | FS-TENANT-03 | OQ-TENANT-OFFBOARD-01 |

### 4.11 Audit Trail

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COLDCHAIN-51 | Audit-trail schema | Fields: actor, action, old/new, reason, timestamp_iso8601 | Default | FS-AUD-01. | FS-AUD-01 | OQ-AUD-COVERAGE-01 |
| DS-COLDCHAIN-52 | Append-only enforcement | DB constraint + RLS policy; tenant admin cannot UPDATE/DELETE | Custom | FS-AUD-02. | FS-AUD-02 | OQ-AUD-APPENDONLY-01 |
| DS-COLDCHAIN-53 | Audit-review cadence | Monthly (Cold-Chain Logistics Lead) + quarterly (QA Compliance); signed reports filed in QA dossier | Default | FS-AUD-03. | FS-AUD-03 | OQ-AUD-REVIEW-01 |
| DS-COLDCHAIN-54 | Audit retention | ≥ 5 y post-shipment minimum; ≥ 25 y for excursion-impacting events; archive-tier with object-lock | Custom | FS-AUD-04. | FS-AUD-04 | OQ-ARCHIVAL-01 |

### 4.12 Integrations / Data Integrity / Performance / Security / Training / PR

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COLDCHAIN-55 | SAP EWM profile-result push | Webservice push within 5 min of download; Investigation-Hold creation on Excursion-Investigation classification | Custom | FS-INT-WMS-01 + URS-INT-WMS-01. | FS-INT-WMS-01 | OQ-INT-WMS-01 |
| DS-COLDCHAIN-56 | MasterControl deviation push | Idempotent on shipment-id | Default | FS-INT-EQMS-01. | FS-INT-EQMS-01 | OQ-INT-EQMS-01 |
| DS-COLDCHAIN-57 | Halcyon Stability push | Per FS-HANDOFF-01; REST mTLS | Default | FS-INT-STAB-01. | FS-INT-STAB-01 | OQ-INT-STAB-01 |
| DS-COLDCHAIN-58 | Okta SSO | SAML 2.0 + MFA | Default (site IdP) | FS-INT-AD-01 + FS-XSYS-AD-01. | FS-INT-AD-01 | OQ-INT-OKTA-01 |
| DS-COLDCHAIN-59 | Carrier GPS integration | Vendor-API per active carrier contract; per-shipment location-series captured | Custom | FS-INT-CARRIER-01. | FS-INT-CARRIER-01 | OQ-INT-CARRIER-01 |
| DS-COLDCHAIN-60 | DI-Attributable enforcement | `actor_id + commissioned_logger_id` captured on every audit-trail emission | Custom | FS-DI-01. | FS-DI-01 | OQ-DI-ATTRIB-01 |
| DS-COLDCHAIN-61 | DI-Original preservation | Logger raw data preserved; corrections recorded as new annotated records referencing original | Default | FS-DI-04. | FS-DI-04 | OQ-DI-IMMUTABLE-01 |
| DS-COLDCHAIN-62 | DI-Accurate validation | Evaluation + CTNS calculations OQ-validated against reference dataset | Custom | FS-DI-05. | FS-DI-05 | OQ-DI-ACCURATE-01 |
| DS-COLDCHAIN-63 | DI-Complete / Enduring retention | Retention per § 5.11 + chronological order at archive | Default | FS-DI-06. | FS-DI-06 | OQ-RETENTION-01 |
| DS-COLDCHAIN-64 | Evaluation latency SLO | P95 ≤ 30 s per logger | Default | FS-PERF-01. | FS-PERF-01 | PQ-PERF-EVAL-01 |
| DS-COLDCHAIN-65 | Backup verification cadence | Annual vendor-published RPO ≤ 4 h / RTO ≤ 24 h verification | Default | FS-BAK-01. | FS-BAK-01 | OQ-BAK-VERIFY-01 |
| DS-COLDCHAIN-66 | Tenant-data export retention | Quarterly tenant-data export retained ≥ 5 y in site cold storage | Custom | FS-BAK-02. | FS-BAK-02 | OQ-TENANT-EXPORT-01 |
| DS-COLDCHAIN-67 | Transport / at-rest encryption | TLS 1.3 in transit; AES-256 at rest | Default | FS-SEC-01. | FS-SEC-01 | OQ-SEC-ENCRYPT-01 |
| DS-COLDCHAIN-68 | Pen-test cadence | Annual; high/critical findings remediated within 60 days | Default | FS-SEC-02. | FS-SEC-02 | OQ-SEC-PENTEST-01 |
| DS-COLDCHAIN-69 | LMS training | Cornerstone curriculum `SLN-CURR-COLDCHAIN-<role>-v1`; Cold-Chain Investigator competency mandatory before role-grant | Custom | FS-TRN-01. | FS-TRN-01 | OQ-LMS-GATE-01 |
| DS-COLDCHAIN-70 | Periodic-review runbook | `SLN-PR-COLDCHAIN-YYYYMMDD` auto-collects profile inventory, excursion trends, CTNS-consumption metrics, integration health, vendor-assurance status, lane re-qualification status, training currency; signed by Cold-Chain Logistics Lead + Head of QA | Custom | FS-PR-01. | FS-PR-01 | OQ-PR-RUNBOOK-01 |

## 5. Workflow + Business-Rule Design

### 5.1 Logger commissioning → shipment → download → classification workflow

```
[Origin hub — Athens / Konstanz / Basel / Wien]
   │
   ▼  Logger Operator: scan logger serial + shipment-id in LIB terminal
[LIB v2.4 box] ── verifies: cal-cert valid (DS-COLDCHAIN-07), battery OK
   │                       (DS-COLDCHAIN-46), reset SOP done if reusable
   │                       (DS-COLDCHAIN-45)
   ▼
[Liberty cloud commissioning service]
   │  binds logger → shipment + profile-version + lane-id
   │  Ed25519 site-key signs binding (DS-COLDCHAIN-06)
   │  chain-of-custody record created
   ▼
[Shipment in transit — accompanied by logger; carrier GPS feed captures
 location series via DS-COLDCHAIN-59]
   │
   ▼  At receiving hub: Logger Operator scans logger in LIB terminal
[LIB v2.4 box] ── downloads logger
   │  integrity check via vendor checksum + Ed25519 (DS-COLDCHAIN-15)
   │  pass → uploads to Liberty cloud
   │  fail → LOGGER_INTEGRITY_EXCEPTION raised; manual investigation
   ▼
[Liberty evaluation engine]
   │  applies EFFECTIVE profile + lane TOR-allowance (DS-COLDCHAIN-18)
   │  classification: Pass / Excursion-Investigation / Reject
   │
   ├─ Pass            → SAP EWM release; CTNS still updated (DS-COLDCHAIN-36)
   ├─ Excursion-Inv.  → SAP EWM Investigation Hold; eQMS deviation;
   │                    Halcyon impact-assessment created
   └─ Reject          → SAP EWM hold-then-reject; eQMS deviation;
                        Halcyon impact-assessment; immediate review
```

### 5.2 CTNS budget consumption workflow

1. Each excursion event emits a `(product_id, batch_id, duration_s, above_or_below)` tuple to the CTNS accumulator (DS-COLDCHAIN-36).
2. Accumulator increments `ctns_seconds_above` or `ctns_seconds_below` per (product, batch).
3. After increment, ratio vs `stability_budget_seconds` evaluated.
4. Threshold crossings (50% / 75% / 90%) emit `CTNS_ALERT_<level>` notifications to Cold-Chain Logistics Lead + Stability Reviewer via email + dashboard tile (DS-COLDCHAIN-38).
5. Daily reconciliation job (DS-COLDCHAIN-39) scans for cases where CTNS > budget but no alert fired (e.g., due to webhook outage); raises `CTNS_SILENT_BREACH` deviation.

### 5.3 Reusable-logger reset SOP enforcement

1. Logger Operator scans returned reusable logger.
2. LIB v2.4 terminal checks `logger.reusable = true` (DS-COLDCHAIN-05).
3. If commissioning attempted before reset done: blocked with `RESET_REQUIRED` error.
4. Reset SOP screen runs through: (a) data-wipe verification; (b) battery check (DS-COLDCHAIN-46); (c) calibration validity check (DS-COLDCHAIN-07); (d) time-sync check.
5. Each step signed by Logger Operator; reset evidence captured in `reset_history`.
6. On all-pass: logger flagged `reset_complete = true` + `last_reset_ts`; commissioning unblocked.

### 5.4 Lane re-qualification workflow

1. Lane re-qualification cadence cron runs nightly; lanes within 90 days of `qualified_until` flagged for renewal.
2. Trigger events (carrier change, route change, packaging change) inserted into `lane_change_events` table.
3. Any event → auto-create re-qualification CR in MasterControl; lane state → `Provisional` until CR closes (DS-COLDCHAIN-22).
4. Provisional-lane shipments require enhanced monitoring (1-h sampling cadence override) + Disposition-Approver dual sign-off at receipt.
5. Disqualified lanes block new shipment commissioning at the LIB terminal.

## 6. Role-Permission Matrix Design

| Action / Role | Logger Operator | Senior Operator | Stab. Prof. Author | Stab. Prof. Approver (QA) | Cold-Chain Investigator | Stability Reviewer | Disposition Approver (QA) | Lane Qual. Engineer | System Admin | Auditor |
|---|---|---|---|---|---|---|---|---|---|---|
| Register / commission / start logger | C | C | — | — | — | — | — | — | — | — |
| Download logger at receipt | C | C | — | — | — | — | — | — | — | — |
| Run reset SOP | C | C | — | — | — | — | — | — | — | — |
| Author DRAFT profile | — | — | C/U | — | — | — | — | — | — | — |
| Approve profile to EFFECTIVE | — | — | — | S | — | — | — | — | — | — |
| Investigate excursion | — | — | — | — | C/U | — | — | — | — | — |
| Recommend disposition | — | — | — | — | C/U | — | — | — | — | — |
| Review excursion → stability-budget impact | — | — | — | — | — | C/U / S | — | — | — | — |
| Approve disposition (release / hold / reject) | — | — | — | — | — | — | S | — | — | — |
| Manual classification override (dual-sig) | — | S (verify leg) | — | — | S (investigator leg) | — | S (approver leg) | — | — | — |
| Author / approve lane qualification | — | — | — | — | — | — | — | C/U / S | — | — |
| OS / patch / AD groups | — | — | — | — | — | — | — | — | C/U | — |
| Cross-tenant audit-trail access (with justification) | — | — | — | — | — | — | — | — | — | R |

Legend: R = read, C = create, U = update, S = sign (re-authenticated), — = denied.

SoD denies per URS § 4:

- Operator ≠ Investigator ≠ Disposition Approver of the same shipment.
- Profile Author ≠ Approver of own profile.
- Lane Qualification Engineer ≠ Disposition Approver.

## 7. Integration Design

| IF-ID | Counterparty | Endpoint | Protocol | Direction | AuthN | Message schema | Retry / DLQ | Audit emission | FS-IDs traced |
|---|---|---|---|---|---|---|---|---|---|
| IF-OKTA-01 | Okta IdP | `https://selene.okta.com/.well-known/openid-configuration` | SAML 2.0 + OIDC | bidirectional | SAML signed assertions + MFA push | SAML + OIDC standard | retry per Okta SDK | `audit_events.AUTHN` → Splunk `gxp-authn` | FS-INT-AD-01, FS-XSYS-AD-01 |
| IF-WMS-01 | SAP EWM | `https://ewm.selene.local/api/v1/shipments/{id}/disposition` | REST mTLS | outbound | mTLS + workload-identity | JSON disposition payload incl. shipment-id, classification, TOR, batch-impact | exponential backoff 1/2/4/8/16 s; DLQ at 5 + alarm | `audit_events.WMS_DISPOSITION_PUSH` | FS-INT-WMS-01 |
| IF-EQMS-01 | MasterControl | `POST https://eqms.selene.local/api/v2/deviations` | REST mTLS | outbound | mTLS + workload-identity | JSON deviation incl. idempotency key `sln-coldchain-{shipment_id}` | exponential backoff; DLQ at 5; idempotent on key | `audit_events.DEVIATION_RAISED` | FS-INT-EQMS-01, FS-XINT-EQMS-01 |
| IF-STAB-01 | Halcyon Stability | `POST https://halcyon.selene.local/api/v1/stability/excursion-impact` | REST mTLS | outbound | mTLS | JSON impact payload (profile-version, lane, temperature-trace, CTNS-consumption) | exponential backoff; DLQ at 5 | `audit_events.HALCYON_PUSH` | FS-INT-STAB-01 |
| IF-CARRIER-01 | Carrier API (DHL Smart Sensor / FedEx SenseAware / UPS Quantum View) | per-carrier REST | REST HTTPS | inbound (poll) | per-carrier API key in Vault | JSON GPS location series | poll cadence per carrier; gap-fill via reconciliation | `audit_events.CARRIER_GPS_POLL` | FS-INT-CARRIER-01 |
| IF-LIB-01 | ELPRO LIB v2.4 (per hub) | `https://lib-<hub>.selene.local:8443` | HTTPS device cert | bidirectional | LIB-device cert + Liberty-tenant cert | Liberty ingest schema | LIB local buffer 7 d on cloud-link loss | `audit_events.LIB_HEARTBEAT` | FS-LOG-COMM-01, FS-EVAL-01 |
| IF-VAULT-01 | HashiCorp Vault | `https://vault.selene.local/v1/kv/coldchain/*` | HTTPS AppRole | inbound | AppRole + Yubikey | KV v2 | retry on rotation | vault-access audit | FS-SEC-01 |

### 7.1 Idempotency contracts

All outbound integrations use idempotency keys to prevent duplicate side-effects on retry:

- **MasterControl deviation:** `sln-coldchain-{shipment_id}` — repeated identical POSTs return original; divergent payload → 409 + audit event.
- **Halcyon impact-assessment:** `sln-coldchain-impact-{shipment_id}` — same contract.
- **SAP EWM disposition:** `sln-coldchain-disp-{shipment_id}-{classification_version}` — re-classification post-investigation produces new key.

### 7.2 Event sequence — excursion-investigation classification

1. Logger downloaded; profile evaluation classifies `Excursion-Investigation`.
2. SAP EWM `POST /shipments/{id}/disposition` with `disposition=INVESTIGATION_HOLD` — stock held in WMS.
3. MasterControl deviation auto-created via IF-EQMS-01 with idempotency `sln-coldchain-{shipment_id}`.
4. Halcyon impact-assessment created via IF-STAB-01 with shipment temperature-trace, CTNS-consumption fields.
5. Cold-Chain Investigator notified (email + dashboard).
6. Investigator reviews; recommends disposition.
7. Stability Reviewer co-reviews CTNS / shelf-life impact.
8. Disposition Approver signs decision (release / hold / reject) with linked Halcyon `assessment_id`.
9. SAP EWM disposition updated via IF-WMS-01 with new classification.
10. eQMS deviation gated to remain OPEN until eQMS-status webhook FS-XINT-EQMS-02 → `CLOSED`.

## 8. Site-Deployed Components Design

### 8.1 ELPRO LIB v2.4 hub appliances (4 units)

- **Type:** Vendor-supplied Linux appliance (Debian-based; ELPRO firmware v2.4).
- **Per-hub configuration:** Hub-specific network attachment (Athens VLAN 305, Konstanz VLAN 310, Basel VLAN 315, Wien VLAN 320); AD-binding for Logger Operator authentication; LIB device cert issued by site PKI.
- **GAMP escalation:** Cat 4 site-deployed component; firmware updated under change control per FS-VND-02. No site-authored code.

### 8.2 `ctns-reconcile.py` daily reconciliation script

- **Type:** Site-authored Python script (per FS-CTNS-04 / DS-COLDCHAIN-39) — hybrid Cat 4 + Cat 5 component.
- **Mini-SDS per METHODOLOGY § 2B.4 rule 6:**
  - **Module:** `ctns-reconcile.py` v1.0.
  - **Inputs:** Read `ctns_accumulator`, `stability_budget`, `ctns_alert_log` tables.
  - **Outputs:** Reconciliation report (CSV); `CTNS_SILENT_BREACH` deviation via IF-EQMS-01 when CTNS > budget without alert.
  - **Dependencies:** Python 3.12; `psycopg[binary]`, `requests`; pinned via `requirements.txt` + SHA-256.
  - **Tests:** pytest ≥ 85% line coverage; fixture-mocked DB + REST.
  - **Change control:** Source in `selene/coldchain-reconcile` GitLab repo; signed commits; CR-gated deployment.
  - **Verified by:** OQ-CTNS-RECONCILE-01.

### 8.3 Liberty Selene-tenant custom dashboards

- **Type:** Vendor Liberty dashboard configuration (declarative) — Cat 4 only.
- **Configuration:** Per-role dashboards (Logger Operator hub view; Cold-Chain Investigator excursion-queue view; Stability Reviewer CTNS-trending view).
- **GAMP escalation:** Remains within Cat 4 — purely declarative dashboard configuration.

## 9. References

### US
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- USP <1079>.
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EU GDP Guidelines (2013/C 343/01) — Chapter 9.

### DACH
- BfArM (DE) AMG GDP requirements.
- Swissmedic (CH) GDP-Richtlinie.
- AGES PharmMed (AT) GDP inspection annex.

### International
- WHO TRS 957 Annex 9.
- ICH Q1A(R2).
- IEC 60068-3-5.
- ISO/IEC 17025.

### Industry
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE GAMP Good Practice Guide *Good Distribution Practice and Cold Chain*.
- PIC/S PI 041.

### Vendor
- ELPRO — *Liberty Cloud Configuration Reference* v5.4.
- ELPRO — *ecolog-NET LIB v2.4 Installation and Validation Approach* v2.4.
- ELPRO — *LIBERO Cx Reusable Logger Reference* v3.2.
- ELPRO — *LIBERO ITS Single-Use Logger Reference* v2.7.

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-COLDCHAIN-01 | FS-VND-01 |
| DS-COLDCHAIN-02 | FS-VND-02 |
| DS-COLDCHAIN-03 | FS-VND-03 |
| DS-COLDCHAIN-04 | FS-LOG-REG-01 |
| DS-COLDCHAIN-05 | FS-LOG-REG-02 |
| DS-COLDCHAIN-06 | FS-LOG-COMM-01 |
| DS-COLDCHAIN-07 | FS-LOG-COMM-02 |
| DS-COLDCHAIN-08 | FS-LOG-COMM-03 |
| DS-COLDCHAIN-09 | FS-PROF-01 |
| DS-COLDCHAIN-10 | FS-PROF-02 |
| DS-COLDCHAIN-11 | FS-PROF-03 |
| DS-COLDCHAIN-12 | FS-PROF-04 |
| DS-COLDCHAIN-13 | FS-PROF-05 |
| DS-COLDCHAIN-14 | FS-PROF-06 |
| DS-COLDCHAIN-15 | FS-EVAL-01 |
| DS-COLDCHAIN-16 | FS-EVAL-02 |
| DS-COLDCHAIN-17 | FS-EVAL-03 |
| DS-COLDCHAIN-18 | FS-EVAL-04 |
| DS-COLDCHAIN-19 | FS-EVAL-05 |
| DS-COLDCHAIN-20 | FS-LANE-01 |
| DS-COLDCHAIN-21 | FS-LANE-02 |
| DS-COLDCHAIN-22 | FS-LANE-03 |
| DS-COLDCHAIN-23 | FS-LANE-04 |
| DS-COLDCHAIN-24 | FS-LANE-05 |
| DS-COLDCHAIN-25 | FS-PART11-01 |
| DS-COLDCHAIN-26 | FS-PART11-02 / FS-XSYS-AD-01 |
| DS-COLDCHAIN-27 | FS-PART11-03 |
| DS-COLDCHAIN-28 | FS-PART11-04 |
| DS-COLDCHAIN-29 | FS-PART11-05 |
| DS-COLDCHAIN-30 | FS-PART11-06 |
| DS-COLDCHAIN-31 | FS-PART11-07 |
| DS-COLDCHAIN-32 | FS-PART11-08 |
| DS-COLDCHAIN-33 | FS-GDP-01 |
| DS-COLDCHAIN-34 | FS-GDP-02 |
| DS-COLDCHAIN-35 | FS-GDP-03 |
| DS-COLDCHAIN-36 | FS-CTNS-01 |
| DS-COLDCHAIN-37 | FS-CTNS-02 |
| DS-COLDCHAIN-38 | FS-CTNS-03 |
| DS-COLDCHAIN-39 | FS-CTNS-04 |
| DS-COLDCHAIN-40 | FS-CTNS-05 |
| DS-COLDCHAIN-41 | FS-HANDOFF-01 |
| DS-COLDCHAIN-42 | FS-HANDOFF-02 / FS-INT-EQMS-01 |
| DS-COLDCHAIN-43 | FS-HANDOFF-03 |
| DS-COLDCHAIN-44 | FS-HANDOFF-04 |
| DS-COLDCHAIN-45 | FS-RESET-01 |
| DS-COLDCHAIN-46 | FS-RESET-02 |
| DS-COLDCHAIN-47 | FS-RESET-03 |
| DS-COLDCHAIN-48 | FS-TENANT-01 |
| DS-COLDCHAIN-49 | FS-TENANT-02 |
| DS-COLDCHAIN-50 | FS-TENANT-03 |
| DS-COLDCHAIN-51 | FS-AUD-01 |
| DS-COLDCHAIN-52 | FS-AUD-02 |
| DS-COLDCHAIN-53 | FS-AUD-03 |
| DS-COLDCHAIN-54 | FS-AUD-04 |
| DS-COLDCHAIN-55 | FS-INT-WMS-01 |
| DS-COLDCHAIN-56 | FS-INT-EQMS-01 |
| DS-COLDCHAIN-57 | FS-INT-STAB-01 |
| DS-COLDCHAIN-58 | FS-INT-AD-01 / FS-XSYS-AD-01 |
| DS-COLDCHAIN-59 | FS-INT-CARRIER-01 |
| DS-COLDCHAIN-60 | FS-DI-01 |
| DS-COLDCHAIN-61 | FS-DI-04 |
| DS-COLDCHAIN-62 | FS-DI-05 |
| DS-COLDCHAIN-63 | FS-DI-06 |
| DS-COLDCHAIN-64 | FS-PERF-01 |
| DS-COLDCHAIN-65 | FS-BAK-01 |
| DS-COLDCHAIN-66 | FS-BAK-02 |
| DS-COLDCHAIN-67 | FS-SEC-01 |
| DS-COLDCHAIN-68 | FS-SEC-02 |
| DS-COLDCHAIN-69 | FS-TRN-01 |
| DS-COLDCHAIN-70 | FS-PR-01 |

**FS-IDs in parent FS NOT covered (with rationale):**
- FS-AV-01 (Availability ≥ 99.5% per ELPRO SLA) — **vendor-internal — no site design surface**: this is governed by the ELPRO Liberty SLA; the site monitors via Vendor Assurance pack (DS-COLDCHAIN-01) but does not design availability mechanisms.
- FS-XSYS-BAK-01 (Veeam backup integration) — covered at site enterprise-backup-service DS level per `AUR-URS-BACKUP-001`; integration row implicit via DS-COLDCHAIN-66 quarterly export.
- FS-XINT-EQMS-02 (eQMS status webhook) — covered in § 7.2 event sequence + IF-EQMS-01 integration row.

## 11. Appendix B — Design-level Risk Register

| DR-ID | Design-stage risk | Origin design choice | Mitigation reference |
|---|---|---|---|
| DR-01 | Ed25519 site-key compromise would invalidate all in-transit logger bindings | DS-COLDCHAIN-06 chose Ed25519 | Site PKI key-rotation SOP; algorithm-agility in binding-payload schema |
| DR-02 | Multi-tenant RLS policy bug could leak CMO data across tenants | DS-COLDCHAIN-48 chose RLS over schema-per-tenant | OQ-TENANT-ISOLATION-01 with cross-tenant attack-vector tests |
| DR-03 | CTNS reconciliation daily cadence creates up to 24 h detection lag on silent breach | DS-COLDCHAIN-39 daily | Daily acceptable per FS-CTNS-04; periodic-review item to consider hourly |
| DR-04 | Battery pre-check threshold (DS-COLDCHAIN-46) may not catch slow drain in long lanes | Per-model threshold | Pre-deployment battery-trend analysis at calibration intervals |
| DR-05 | Carrier GPS API outages would create gaps in chain-of-custody | DS-COLDCHAIN-59 vendor-API | Gap-fill via reconciliation; periodic-review tracks carrier-API uptime |
| DR-06 | HMAC-SHA-256 signature binding could be replayed if shared-key compromised at vendor side | DS-COLDCHAIN-29 vendor default | Vendor SOC 2 + ISO 27001 reliance; key-rotation per ELPRO standard |
| DR-07 | LIB v2.4 local buffer 7 d on cloud-link loss could exhaust during prolonged outage | IF-LIB-01 7 d | Operational SOP: site-IT escalation at 5 d; offline shipment-receipt fallback procedure |
| DR-08 | Lane-state-machine `Provisional` could be over-used as workaround to avoid full requalification | DS-COLDCHAIN-22 | Periodic-review item; alert if Provisional > 30 d unbroken |
| DR-09 | Profile-version-in-use stamp at shipment record only — does not capture mid-shipment EFFECTIVE-profile change | DS-COLDCHAIN-14 | Profile transitions require new version; mid-shipment changes are non-events for already-commissioned shipments by design |
| DR-10 | Idempotency-key reuse between investigation rounds could silently link new investigation to old | DS-COLDCHAIN-42 idempotency on shipment-id | Re-classification produces new key `sln-coldchain-disp-{shipment_id}-{version}` per § 7.1 |
| DR-11 | `ctns-reconcile.py` (DS-COLDCHAIN-39 site-authored Python) carries Cat 5 sub-component risk | § 8.2 mini-SDS | Cat 5 SDLC discipline: code review, ≥ 85% test coverage, signed commits, CR-gated deployment |
| DR-12 | Vendor releases (DS-COLDCHAIN-02 14-day SLA) could outpace site impact-assessment for security-only patches | DS-COLDCHAIN-02 | Site security patches expedited per FS-VND-02; security-only fast-track procedure |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
