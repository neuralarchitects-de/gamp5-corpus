---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-26; T4 hand-expansion 2026-05-12"
seed_corpus_basis:
  - "MAR-URS-EDC-001 (parent URS) v1.2"
  - "GAMP 5 (2nd ed.) Cat 4 conventions for SaaS clinical platforms"
  - "21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300"
  - "ICH E6(R3) GCP (Step 4, 6 January 2025); ICH E8(R1); ICH E9(R1); ICH E2A"
  - "CDISC SDTM / ADaM / CDASH / ODM-XML / Define-XML"
  - "EU CTR 536/2014 + CTIS"
  - "FDA Computerized Systems Used in Clinical Investigations (May 2007)"
  - "FDA Electronic Source Data in Clinical Investigations (Sep 2013)"
  - "Medidata Rave EDC 2024 vendor documentation"
parent_urs:
  document_number: MAR-URS-EDC-001
  version: 1.2
  file: ../../URS/_generated/final/EDC_Electronic_Data_Capture_System__Marigold_Clinical_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## EDC — Medidata Rave EDC 2024 — Platform-Level Configuration

**Document Number:** MAR-FS-EDC-001
**Version:** 1.0
**Effective Date:** 2026-04-26 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Parent URS:** MAR-URS-EDC-001 v1.2
**Site:** Marigold Clinical Operations GmbH, München, Germany *(fictional)*
**System Owner:** Director, Clinical Data Management
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Regulatory Scope:** 21 CFR Part 11; ICH E6(R3) (Step 4, 6 January 2025); ICH E8(R1); ICH E9(R1); EU CTR 536/2014 + CTIS; FDA *Computerized Systems Used in Clinical Investigations* (May 2007); FDA *Electronic Source Data in Clinical Investigations* (Sep 2013); EMA *Guideline on Computerised Systems and Electronic Data*; GDPR Arts. 6, 9, 22, 32, 35; HIPAA; CDISC SDTM / ADaM / CDASH / ODM-XML / Define-XML

> **FS scope note.** This FS describes the **platform-level** configuration that applies to all studies. Per-study eCRF / edit-check / derivation specifications are documented in study-specific FS sub-documents (`MAR-FS-EDC-STUDYNNN`) referenced from the per-study CSV plan and validated under per-study UAT.

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Clinical Data Management) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Vendor Assurance Owner) | _____________ | _____________ | _____ |
| Reviewer (Pharmacovigilance Lead) | _____________ | _____________ | _____ |
| Reviewer (Data Protection Officer) | _____________ | _____________ | _____ |
| Approver (VP Clinical Operations) | _____________ | _____________ | _____ |
| Approver (VP Quality Assurance) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue, derived from MAR-URS-EDC-001 v1.0. |
| 1.1 | 2026-05-11 | (synthetic) | DACH site relocation; CTIS gateway implementation. |
| 1.2 | 2026-05-12 | (synthetic) | **Paired to URS v1.2 T4 expansion.** Every new URS-ID has its own FS-ID row in § 4 and § 8 with per-ID implementation detail (Medidata Rave config items, CDISC schema specifics, integration endpoints, ICH E6(R3) RBM feed, CTIS extracts, DSMB firewall, eConsent, ePRO ingest, Pinnacle21 + Define-XML, GDPR Arts. 22/32/35 controls, BIMO export bundle). |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## Definitions

Inherited from MAR-URS-EDC-001. Additional FS-specific terms:

| Term | Definition |
|---|---|
| FS | Functional Specification (this document) |
| Per-study FS | Study-specific FS describing eCRFs, edit checks, derivations |
| Quick-Publish | Medidata's mid-study minor-change deployment path |
| Pinnacle21 | CDISC OpenCDISC SDTM / ADaM / Define-XML validation tool |
| TMF RM | TMF Reference Model v3.3.x |
| BAA / DPA | Business Associate Agreement (HIPAA) / Data Processing Agreement (GDPR) |

---

## 1. Purpose

This FS specifies how the Medidata Rave EDC 2024 SaaS platform is configured, integrated, and governed at the Marigold tenancy level to satisfy `MAR-URS-EDC-001` v1.2. The platform-level configuration is validated once and re-used across studies; per-study build is validated separately under per-study CSV plans.

## 2. Scope

Mirrors MAR-URS-EDC-001 §2:

- **In scope (platform-level):** tenancy configuration; per-study build lifecycle controls; role / permission model; security profiles; SSO (Okta SAML 2.0 + MFA); Coder / RTSM / Lab / Imaging / eTMF / Argus / ePRO / LIMS integrations at the tenancy level; audit-trail policy; signature configuration; retention policy; vendor-assurance evidence handling; CTIS extract gateway; DSMB / IDMC firewalled extract path; BIMO inspection-readiness bundle.
- **Out of scope (this FS):** per-study eCRF / edit-check / derivation; ePRO authoring; investigator delegation logs (CTMS scope); financial / payments tracking; Medidata-managed infrastructure.

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source / Vendor | Notes |
|---|---|---|---|---|---|
| C-01 | Rave EDC SaaS tenancy | COTS SaaS | 4 | Medidata | vendor-managed infra |
| C-02 | Rave Architect (study-build authoring) | COTS SaaS | 4 | Medidata | per-study build |
| C-03 | Medidata Coder | COTS SaaS | 4 | Medidata | MedDRA + WHODrug coding |
| C-04 | Medidata RTSM / IXRS-class | COTS SaaS | 4 | Medidata / Calyx | randomization + supply |
| C-05 | Medidata eTMF (or Marinos eTMF) | COTS SaaS | 4 | Medidata / Marinos | TMF Reference Model–aligned |
| C-06 | Okta tenant | COTS SaaS | (infra) | Okta | site IdP — separately validated |
| C-07 | Argus (safety) | COTS app | 4 | Oracle | SAE reconciliation counterparty |
| C-08 | Central labs (LabCorp / Q² / Eurofins) | external | n/a | external | CDISC LAB / ODM ingest |
| C-09 | Iolanthe ePRO | custom | 5 | Marigold (Wien) | ePRO ingest via ODM-XML |
| C-10 | Watson LIMS (Cetus) | COTS | 4 | Thermo Fisher | bioanalytical PK/PD ingest |
| C-11 | Imaging core lab | external | n/a | external | DICOM gateway |
| C-12 | Central monitoring / RBM platform | COTS | 4 | Medidata Detect / equiv. | RBM feed consumer |
| C-13 | CTIS sponsor workspace | external | n/a | EMA | CTR submission portal |
| C-14 | Pinnacle21 (validation) | COTS | 4 | Certara | SDTM / Define-XML validation |

### 3.2 Logical Architecture (textual)

```
                ┌──────────────────────────────────────────────┐
                │           Okta IdP (SAML 2.0 + MFA)           │
                └────────────────────┬─────────────────────────┘
                                     │
   ┌─────────────────────────────────▼─────────────────────────────────┐
   │                Medidata Rave EDC tenancy (Marigold)               │
   │   ┌────────────────┐ ┌────────────────┐ ┌─────────────────────┐   │
   │   │ Rave Architect │ │ Rave EDC Web   │ │ Configuration /     │   │
   │   │ (per-study)    │ │ (data capture) │ │ user-role admin     │   │
   │   └────────────────┘ └────────────────┘ └─────────────────────┘   │
   └─┬─────────┬─────────┬───────┬─────────┬────────┬─────────┬───────┘
     │         │         │       │         │        │         │
     ▼         ▼         ▼       ▼         ▼        ▼         ▼
   Coder    RTSM/      Central  Imaging   ePRO    LIMS      RBM /
   (MedDRA  IXRS       labs     (DICOM)  (Iolan-  (Watson)  Detect
    WHODrug)(rand/    (CDISC              the)              dashboard
            supply)    LAB/ODM)
     │         │         │       │         │        │
     ▼         ▼         ▼       ▼         ▼        ▼
       Argus (SAE / SUSAR reconciliation, daily) ◄────┐
                                                       │
       eTMF (config + lock evidence + DSMB manifests) ─┘
                                                       │
       CTIS (Annual Safety Report, end-of-trial pack) ─┘
                                                       │
       Pinnacle21 (SDTM / Define-XML validation) ──────┘
```

### 3.3 Functional Modules

| Module | URS sections |
|---|---|
| M-VND | URS-VND-* |
| M-BUILD | URS-BUILD-* |
| M-CRF | URS-CRF-* |
| M-DATA | URS-DATA-* |
| M-ESRC | URS-ESRC-* |
| M-QRY | URS-QRY-* |
| M-SDV | URS-SDV-* |
| M-RBM | URS-RBM-* |
| M-COD | URS-COD-* |
| M-SIG | URS-SIG-*, URS-PART11-* |
| M-AUD | URS-AUD-* |
| M-LOCK | URS-LOCK-* |
| M-SDTM | URS-SDTM-* |
| M-INT | URS-INT-* |
| M-AMD | URS-AMD-* |
| M-CONSENT | URS-CONSENT-* |
| M-DEV | URS-DEV-* |
| M-DSMB | URS-DSMB-* |
| M-CTIS | URS-CTIS-* |
| M-EST | URS-EST-* |
| M-PERF | URS-PERF-*, URS-AV-*, URS-BAK-* |
| M-SEC | URS-SEC-* |
| M-TRN | URS-TRN-*, URS-PR-* |
| M-BIMO | URS-BIMO-* |
| M-INTL | URS-INTL-* |

---

## 4. Functional Specifications (platform-level)

### 4.1 Vendor / Platform Assurance (M-VND)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VND-01 | URS-VND-01 | Vendor-assurance evidence (SOC 2 Type II, ISO 27001:2022, HIPAA, GDPR DPA + sub-processor list, customer-shared CSV summary, vendor SDLC summary) tracked in the Vendor Quality Register (eQMS module); annual review with signed evidence-acceptance; gap actions tracked as eQMS CAPAs. |
| FS-VND-02 | URS-VND-02 | Quarterly Rave-release evaluation runbook: read release notes within 14 calendar days of publication on Medidata Trust portal; classify each item as {no-impact, configuration-impact, semantics-impact, regulatory-impact}; impacted studies routed to URS-BUILD-04 re-validation; assessment recorded in `vendor-release-eval-log` (eQMS). |
| FS-VND-03 | URS-VND-03 | Vendor sub-processor inventory pulled from Medidata DPA Annex; reviewed annually; new sub-processors trigger Marigold DPO impact-assessment before vendor activation per GDPR Art. 28(2). |
| FS-VND-04 | URS-VND-04 | Vendor incident notifications received via Medidata Trust portal + email; tracked in `vendor-incident-log`; confirmed-breach notifications routed to Marigold DPO within 24 h to support Marigold's GDPR Art. 33 72-h propagation clock. |

### 4.2 Per-Study Build Lifecycle (M-BUILD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BUILD-01 | URS-BUILD-01 | Per-study environments configured: DEV, QC, UAT, PRODUCTION as separate Rave URLs (e.g., `marigold-dev.mdsol.com`, `marigold-uat.mdsol.com`, `marigold.mdsol.com`); subject data accept-controls enabled only in PRODUCTION; DEV→PROD direct push disabled at the tenancy level. |
| FS-BUILD-02 | URS-BUILD-02 | Promotion gated by role-restricted electronic signatures executed via Rave Architect's promote flow. Signer's prior actions on the study evaluated against SoD policy in identity-layer (Builder ≠ Approver enforced as Rave role permission + as Okta group membership check). |
| FS-BUILD-03 | URS-BUILD-03 | Per-study UAT execution plan generated by `uat-plan-gen` from the protocol's eCRF and edit-check inventory (Rave Architect export); UAT script execution captured in the eQMS; clinical-lead and data-manager sign-off required before promotion to PRODUCTION. |
| FS-BUILD-04 | URS-BUILD-04 | Mid-study amendment process: impact-assessment template (Confluence + signed PDF in eTMF); UAT of changed forms; data-migration scripts validated in UAT against representative subject data; production migration window with documented checkpoints + rollback plan per `mid-study-migration-runbook`. |
| FS-BUILD-05 | URS-BUILD-05 | Quick-Publish whitelist: typo fixes; edit-check expression rewrites preserving truth-table semantics; entry-restriction tweaks; restricted folder visibility. Whitelist enforced by Architect-side rule + reviewer + approver signature with explicit semantic-equivalence justification text (free-text). |
| FS-BUILD-06 | URS-BUILD-06 | Each promotion produces a build-package: zip of eCRF metadata (ODM-XML), edit-check definitions, derivation logic (post-fix), code lists (CT-XML), custom-function source, SDTM mapping spec; SHA-256 fingerprint logged; archived to eTMF under TMF RM artefact 04.02 (Functional Specifications). |
| FS-BUILD-07 | URS-BUILD-07 | Study Architect templates governed by `template-registry` versioned in Git; template changes promoted as `template@vX.Y`; new studies bind to a specific template version; existing studies are NOT retroactively re-bound. |
| FS-BUILD-08 | URS-BUILD-08 | Per-study CtQ register stored as a Rave custom-form `CTQ_REGISTER`; CtQ-tags bound to eCRF fields via Architect metadata; SDV configuration + RBM feed read the CtQ tags for risk-proportionate treatment. |

### 4.3 Per-Study eCRF Library and CDASH Alignment (M-CRF)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CRF-01 | URS-CRF-01 | eCRF library bound to CDASH-IG v2.3 controlled-terminology via Architect's CT manager; deviation register `cdash-deviation-log` captures any field outside CDASH with justification. |
| FS-CRF-02 | URS-CRF-02 | Field-level constraints enforced server-side via Rave's `Required`, `MandatoryWithSkip`, `Branch`, `EditCheck`, and `CodeList` settings; client-side enforcement is convenience only. |
| FS-CRF-03 | URS-CRF-03 | Visit-schedule configured per protocol with `EarlyVisitDays`, `NominalVisitDays`, `LateVisitDays` tolerances; visit-window violations raise queries automatically via the standard edit-check `VISIT_WINDOW_CHECK`. |
| FS-CRF-04 | URS-CRF-04 | Casebook-completion KPI computed by `casebook-completeness-job` (daily); per subject / visit / form percentages fed to the central monitoring dashboard via the RBM feed (FS-RBM-01). |
| FS-CRF-05 | URS-CRF-05 | Each eCRF associated to one or more CtQ tags via `CTQ_REGISTER` link; RBM-targeted SDV inspects the link table to determine 100% vs risk-based treatment. |

### 4.4 Data Capture and Edit Checks (M-DATA)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DATA-01 | URS-DATA-01 | eCRF field constraints enforced server-side via Rave's standard validation engine; client-side enforcement convenience only; types, mandatoriness, code-list constraints, range checks, unit handling all model-driven. |
| FS-DATA-02 | URS-DATA-02 | Edit-check failures auto-create queries via Rave's `EditCheck` action with: `rule_id`, `field_path` (folder.form.field), `raised_by = system`, `raised_at` UTC timestamp; query lifecycle tracked in audit trail. |
| FS-DATA-03 | URS-DATA-03 | Derivations expressed in Rave's standard post-fix notation derivation framework; per-derivation unit tests required in UAT; code reviewed; production-derivation logic changes via URS-BUILD-04. |
| FS-DATA-04 | URS-DATA-04 | Custom functions kept in a signed-off function library; code review evidenced in eQMS; functions locked to a build version; per-study free-form modification in production blocked by Architect role policy. |
| FS-DATA-05 | URS-DATA-05 | Time-zone aware storage: all timestamps stored as UTC + `tz_original` (IANA name); display-layer converts to subject / site time-zone per UI context. |
| FS-DATA-06 | URS-DATA-06 | Impossible-date guard implemented as edit-check `IMPOSSIBLE_DATE_CHECK` (future DOB, dose-before-randomisation, visit-before-screening, etc.); applied at field level pre-save. |
| FS-DATA-07 | URS-DATA-07 | Mobile / tablet capture supported via Rave Companion (or browser PWA per study); offline queue persists to local encrypted store; reconciliation runs on reconnect with conflict-detection raising a system query. |

### 4.5 eSource and Direct Capture (M-ESRC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ESRC-01 | URS-ESRC-01 | Designated eSource forms marked in the build with `is_esource = true`; metadata propagates to SDTM `--ORIG` per FS-ESRC-04; FDA *Electronic Source Data in Clinical Investigations* (Sep 2013) considerations documented per-study. |
| FS-ESRC-02 | URS-ESRC-02 | For eSource forms, no paper-source requirement applied; contemporaneous-capture timestamp (UTC) is the ALCOA+ satisfaction evidence; reviewed in periodic-review evidence. |
| FS-ESRC-03 | URS-ESRC-03 | eSource device authentication: Okta + MFA; device enrolled in per-study `device-registry` with device-id, serial, OS-version, browser-version; unregistered devices blocked. |
| FS-ESRC-04 | URS-ESRC-04 | SDTM `--ORIG` metadata field populated per CDISC controlled-terminology (e.g., `INVESTIGATOR`, `eSource`, `eDC`) per the field's capture mechanism. |

### 4.6 Query Management Workflow (M-QRY)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-QRY-01 | URS-QRY-01 | Query-source taxonomy implemented as enum: `SYSTEM_EDITCHECK`, `MONITOR_MANUAL`, `DM_MANUAL`, `MEDICAL_MONITOR`, `CODER`; each source produces a distinct query-type record. |
| FS-QRY-02 | URS-QRY-02 | Query schema captured as Rave standard Query object: `query_id`, `subject_id`, `form_id`, `field_path`, `rule_id`, `raised_by`, `raised_at`, `state`, `response`, `response_author`, `response_at`, `closure_author`, `closure_at`. |
| FS-QRY-03 | URS-QRY-03 | Hard-lock state disables `re-open` action on closed queries via Rave's state-machine policy; unlock-workflow (FS-LOCK-02) is the only route to re-open. |
| FS-QRY-04 | URS-QRY-04 | Query-aging KPIs: median + p90 time-to-response, time-to-close, % overdue per site; computed by `query-aging-job` daily; published to the RBM feed. |
| FS-QRY-05 | URS-QRY-05 | Bulk-query operations route through `bulk-query-runner` which writes one query event per impacted record; no silent suppression; runner output reviewed by Data Manager. |

### 4.7 Source-Data Verification and Source-Data Review (M-SDV)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SDV-01 | URS-SDV-01 | SDV plan configured per study; CtQ-tagged fields default to 100% SDV via `sdv-plan@critical-100`; non-CtQ fields routed to risk-based plan per per-study RBM plan; monitor signature captured on visit completion. |
| FS-SDV-02 | URS-SDV-02 | SDR (broader source review) implemented as a distinct activity record `sdr-event`; never written via the SDV event API; reporting keeps the two activities separated. |
| FS-SDV-03 | URS-SDV-03 | Remote-SDV flag captured per visit event; per-study RBM plan defines remote-SDV eligibility; flag propagates to central monitoring dashboard for trend review. |
| FS-SDV-04 | URS-SDV-04 | `sdv-exception-job` produces a "fields-not-yet-SDV'd" report at lock checkpoint; report attached to lock evidence. |

### 4.8 Risk-Based Monitoring Data Feed (M-RBM)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RBM-01 | URS-RBM-01 | RBM data feed published via Rave's Clinical Views over REST (`/v1/rbm-feed/{study}`) + nightly batch CSV; payload includes site-level KPIs (enrolment rate, query-aging, deviation rate, SDV completeness, missing-data rate by CtQ field); cadence configurable per study (default daily). |
| FS-RBM-02 | URS-RBM-02 | Feed supports the sponsor's combined on-site / remote / centralised monitoring strategy (ICH E6(R3) § 3.10); site-risk indicators computed downstream in the central monitoring platform from feed data. |
| FS-RBM-03 | URS-RBM-03 | RBM feed health monitored by `rbm-feed-watchdog`; gap > 48 h raises P1 system alert and blocks database-lock action via FS-LOCK-01 precondition check. |
| FS-RBM-04 | URS-RBM-04 | Feed payload schema versioned (`rbm-feed@vX`); backwards-compatible across minor releases; breaking changes require URS-BUILD-04 mid-study amendment. |

### 4.9 Coding — MedDRA + WHODrug (M-COD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-COD-01 | URS-COD-01 | MedDRA version frozen per study at build time (e.g., MedDRA v27.0); `meddra_version_effective_from` captured in study metadata; Coder configured with the same version. |
| FS-COD-02 | URS-COD-02 | WHODrug version frozen per study at build time (e.g., WHODrug Global B3 Mar-2026); `whodrug_version_effective_from` captured similarly. |
| FS-COD-03 | URS-COD-03 | Autocode performed by Coder; manual-review queue surfaced in Coder UI; each manual override writes an audit-trail entry with coder-id, dictionary version, decision-timestamp, rationale text. |
| FS-COD-04 | URS-COD-04 | Mid-study dictionary upgrade workflow: (a) rationale doc; (b) impact-assessment over key tables; (c) re-coding plan; (d) archive of both versions + release notes in eTMF; (e) signed approval by Medical Monitor + Data Manager via FS-PART11-09 signatures. |
| FS-COD-05 | URS-COD-05 | Coding-decision audit trail export available via Coder's standard export + Rave audit-trail join; format CSV / PDF / ODM-XML; used in BIMO bundle (FS-BIMO-01). |
| FS-COD-06 | URS-COD-06 | Synonym lists version-controlled in Coder; per-study synonym additions captured with author + reviewer signatures. |

### 4.10 Investigator Signature (M-SIG)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SIG-01 | URS-SIG-01 | Investigator signature applied at form / casebook level per protocol configuration; meaning string per ICH E6(R3) Section 6; signature payload bound to record-state SHA-256 hash. |
| FS-SIG-02 | URS-SIG-02 | Post-signature data-change writes a `SIG_INVALIDATED` audit-trail entry; UI surfaces "REQUIRES RESIGN"; original signature retained; re-sign produces a new signature linked to the new record-state hash. |
| FS-SIG-03 | URS-SIG-03 | Signature-meaning string template: "I, as Principal Investigator, have reviewed and confirm the accuracy of these data for subject {subject_id} as of {timestamp_utc}." Localised per site language. |
| FS-SIG-04 | URS-SIG-04 | Casebook PDF generated on demand via `casebook-pdf-job`; PDF embeds signature manifestations (printed name, date / time, meaning) per § 11.50; digitally signed with sponsor's PKI key. |

### 4.11 21 CFR Part 11 — Sub-section-Specific (M-SIG)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | § 11.10(a) — SOP suite: `SOP-CDM-01 System Access`, `SOP-CDM-02 Change Control`, `SOP-CDM-03 Data Entry`, `SOP-CDM-04 Data Review`; effective at every site; training-record gate in LMS. |
| FS-PART11-02 | URS-PART11-02 | § 11.10(b) — Casebook PDFs reproducible from DB state via `casebook-pdf-job`; SDTM + Define-XML reproducible via `sdtm-export-job`; both produce SHA-256 manifest matching prior runs (modulo data changes). |
| FS-PART11-03 | URS-PART11-03 | § 11.10(c) — Retention ≥ 25 y per FS-AUD-04; vendor-hosted with backup per FS-BAK-01; DR per FS-BAK-03. |
| FS-PART11-04 | URS-PART11-04 | § 11.10(d) — Okta + MFA + role-based + per-study + per-country / site scopes per FS-SEC-01..02. |
| FS-PART11-05 | URS-PART11-05 | § 11.10(e) — Audit trail per FS-AUD-01..07. |
| FS-PART11-06 | URS-PART11-06 | § 11.10(g) — Authority checks at signature, promote, lock actions: server-side verifies actor's role + SoD + training-current before commit; failed check writes audit entry + denies action. |
| FS-PART11-07 | URS-PART11-07 | § 11.10(k) — Vendor manuals + Marigold per-study SOPs versioned in eDMS (Vellis); user training is gated on current manual version via LMS rule. |
| FS-PART11-08 | URS-PART11-08 | § 11.30 — Rave EDC platform is a closed system (Medidata multi-tenant); CTIS gateway treated as a controlled bridge with TLS 1.3 + mutual auth + checksum reconciliation. |
| FS-PART11-09 | URS-PART11-09 | § 11.50 — Every signature event records: printed name; UTC timestamp; meaning string; manifested in audit trail and casebook PDF. |
| FS-PART11-10 | URS-PART11-10 | § 11.70 — Signature payload binds to record-state SHA-256 hash; any post-signature record-state delta invalidates the signature (FS-SIG-02). |
| FS-PART11-11 | URS-PART11-11 | § 11.100 — User-id uniqueness enforced by Rave's identity layer + Okta IdP; deactivated user-ids never reassigned; "user-id reuse forbidden" enforced at IdP provisioning rule. |
| FS-PART11-12 | URS-PART11-12 | § 11.200 — Re-authentication (password + MFA) required at every signature event; cached creds disabled at signature moment via Rave session-policy `force-reauth-on-sign`. |
| FS-PART11-13 | URS-PART11-13 | § 11.300 — Okta password policy: ≥ 14 chars, history 12, age 90 d; MFA required; lockout after 5 failed attempts; lockout audit-logged. |

### 4.12 Audit Trail (M-AUD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit trail captures data-entry, edit-check evaluation, query lifecycle, signatures, lock / unlock events, configuration changes, build promotions, user provisioning, training-status changes with `actor_id`, `timestamp_utc`, `action`, `entity`, `old_value`, `new_value`, `reason_for_change`. |
| FS-AUD-02 | URS-AUD-02 | Append-only at the platform level (vendor-managed via Rave); export to CSV / PDF / ODM-XML; export bundle digitally signed by sponsor PKI key. |
| FS-AUD-03 | URS-AUD-03 | RBM dashboard ingests audit-trail review evidence via FS-RBM-01; quality-issue trends fed to the central monitoring tool; per-visit audit-trail-review record captured by CRA. |
| FS-AUD-04 | URS-AUD-04 | Retention policy: 25-year minimum post-trial completion; per-study extension applied where paediatric / oncology / EU CTR Art. 58 require longer. |
| FS-AUD-05 | URS-AUD-05 | Audit-trail disablement detection: `audit-trail-watchdog` performs heartbeat write + read every 5 min; gap > 15 min sets system to `READ_ONLY` and raises P1 to vendor + sponsor SRE; remediation evidence required before write-restore. |
| FS-AUD-06 | URS-AUD-06 | Reason-for-change required for every post-initial-entry data change; enforced at server-side commit; UI prompts for selection from controlled vocabulary. |
| FS-AUD-07 | URS-AUD-07 | Reason-for-change controlled vocabulary: `DATA_ENTRY_ERROR`, `NEW_INFORMATION`, `QUERY_RESPONSE`, `SYSTEM_DRIVEN`, `PROTOCOL_CLARIFICATION`, `OTHER_JUSTIFY`; `OTHER_JUSTIFY` requires free-text rationale. |

### 4.13 Database Lock and Export (M-LOCK)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-LOCK-01 | URS-LOCK-01 | Soft-lock and hard-lock implemented as distinct study states; hard-lock requires the lock-checklist (queries closed, SDV complete, medical review complete, listings reviewed, signatures complete, coding complete, SAE reconciliation with Argus reconciled, RBM feed gap ≤ 0 h) and dual approval signatures (Director CDM + VP Clinical Operations). |
| FS-LOCK-02 | URS-LOCK-02 | Unlock requires justification text (free-form), scope (forms / sites / time-window) and re-lock signature on completion; unlock evidence filed in eTMF as TMF RM artefact 08.03.07. |
| FS-LOCK-03 | URS-LOCK-03 | Final dataset export: `sdtm-export-job` → SDTM v2.0 / SDTM-IG v3.4 (XPT or Dataset-JSON), Define-XML v2.1 metadata, SHA-256 manifest; reconciliation against source via byte-equivalence check for verifiable fields. |
| FS-LOCK-04 | URS-LOCK-04 | ADaM v1.3 datasets derivable via `adam-derive-job` per per-study ADaM spec; lineage captured in ADaM `--QUAL` + Define-XML analysis-variable annotations. |
| FS-LOCK-05 | URS-LOCK-05 | Lock-checkpoint delta produced by `lock-delta-job` (data changed since last DSMB / IDMC extract); fed to FS-DSMB-03 manifest. |
| FS-LOCK-06 | URS-LOCK-06 | Lock-evidence pack assembled by `lock-evidence-bundler`: lock-checklist signed; SDTM + Define-XML export bundle; ADaM spec; query-closure summary; SDV evidence; coding-finalisation evidence; SAE reconciliation evidence; filed in eTMF under TMF RM artefact 08.03. |

### 4.14 SDTM / ADaM / Define-XML / Submission Package (M-SDTM)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SDTM-01 | URS-SDTM-01 | SDTM mapping configured per study via `sdtm-mapping-spec`; stored as a versioned artefact in eTMF; mapping changes follow FS-BUILD-04. |
| FS-SDTM-02 | URS-SDTM-02 | SDTM export validated against the protocol-specified SDTM-IG version (e.g., v3.4); Pinnacle21 (Certara) run as part of `sdtm-export-job`; ERROR-class findings block submission-package generation; WARNING-class findings reviewed by biostatistics. |
| FS-SDTM-03 | URS-SDTM-03 | Define-XML v2.1 generated by `define-xml-gen` with full CT metadata, value-level metadata, analysis-variable annotations; validated alongside SDTM via Pinnacle21. |
| FS-SDTM-04 | URS-SDTM-04 | Dataset-JSON v1.0 export supported as alternative to XPT; per-study toggle `submit_format` ∈ {XPT, DATASET_JSON}; FDA Dataset-JSON pilot studies use DATASET_JSON. |
| FS-SDTM-05 | URS-SDTM-05 | SDTM round-trip verifier: re-imports the exported SDTM and compares byte-equivalent values for verifiable fields; mismatches block lock with detailed delta report. |

### 4.15 Integrations — Coder (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-CODER-01 | URS-INT-CODER-01 | AE / SAE verbatim terms routed to Medidata Coder via vendor-internal API; coding decisions captured with `coder_id`, `meddra_version`, `decision_timestamp_utc`; manual overrides audit-trailed. |
| FS-INT-CODER-02 | URS-INT-CODER-02 | Conmed verbatim terms routed to Coder via vendor-internal API; same metadata; `whodrug_version` substituted. |
| FS-INT-CODER-03 | URS-INT-CODER-03 | Coder interface failure raises `INT_CODER_FAIL` alert; queue-and-retry with exponential backoff; no fallback to local autocode; coding incompleteness blocks lock. |

### 4.16 Integrations — IRT / RTSM / IXRS (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-RTSM-01 | URS-INT-RTSM-01 | Daily reconciliation job `rtsm-reconcile-job` between RTSM/IXRS and EDC; mismatches raise system queries with `rule_id = RTSM_RECONCILE`; blocks lock until resolved. |
| FS-INT-RTSM-02 | URS-INT-RTSM-02 | Duplicate-enrolment guard: RTSM ↔ EDC cross-validation against screening-id + hashed demographics (DOB, sex, initials hash); duplicate detected raises P1 alert and blocks randomisation. |
| FS-INT-RTSM-03 | URS-INT-RTSM-03 | Drug-accountability reconciliation: dispensed / returned / unused / destroyed kits reconciled daily between IRT and EDC drug-acct eCRFs; unreconciled discrepancies block lock. |
| FS-INT-RTSM-04 | URS-INT-RTSM-04 | Heartbeat protocol: every 15 min; missed-heartbeat count tracked; ≥ 4 successive misses raises P1 `IXRS_SILENT_FAIL` alert to SRE + Data Manager. |

### 4.17 Integrations — Central Lab (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-LAB-01 | URS-INT-LAB-01 | Central-lab CDISC LAB / ODM-XML ingest via `lab-ingest-job`; reference-range derivation per visit and per lab; lab-specific normal ranges configured per protocol; ingested records audit-trail linked. |
| FS-INT-LAB-02 | URS-INT-LAB-02 | Local-lab data entered via dedicated forms with site-specific normal-range mapping or central normalisation table per protocol; mapping captured per FS-CRF-01 controlled-terminology. |
| FS-INT-LAB-03 | URS-INT-LAB-03 | Lab-anomaly detector: value outside ± 5σ of historical site / protocol range triggers `LAB_ANOMALY` query auto-raised; configurable thresholds per analyte. |

### 4.18 Integrations — Imaging / DICOM (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-IMG-01 | URS-INT-IMG-01 | Imaging core-lab gateway `imaging-bridge` receives DICOM-derived clinical reads with study + subject + visit triplet; PHI scrubbed per de-identification rules; matched records inserted into imaging-result eCRF. |
| FS-INT-IMG-02 | URS-INT-IMG-02 | SDTM `--ORIG = "ASSIGNED"` applied for imaging-derived fields to distinguish from investigator observations. |

### 4.19 Integrations — Pharmacovigilance / Argus (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-SAFETY-01 | URS-INT-SAFETY-01 | SAE flagged at investigator confirmation; transmitted to Argus 8.4 within 24 h via secure file transfer (SFTP + PGP); daily reconciliation log filed in eTMF; sponsor PV owns regulatory clock. |
| FS-INT-SAFETY-02 | URS-INT-SAFETY-02 | SUSAR awareness-date propagation: EDC exposes the sponsor-awareness timestamp to Argus; Argus owns the 7-day fatal-LT / 15-day non-LT clock toward EudraVigilance per ICH E2A; EDC does NOT compute the regulatory deadline. |
| FS-INT-SAFETY-03 | URS-INT-SAFETY-03 | Daily SAE-reconciliation drift detector: `sae-drift-job` compares EDC SAE records to Argus case set; drift > 5 business days unresolved raises P1 and blocks lock. |
| FS-INT-SAFETY-04 | URS-INT-SAFETY-04 | SAE narrative free-text sourced from Argus, surfaced read-only in EDC medical-monitor view; Argus is regulatory record-of-truth for narrative. |

### 4.20 Integrations — eTMF (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-ETMF-01 | URS-INT-ETMF-01 | Configuration baselines, build-package, lock-checklist, Define-XML, DSMB manifests, vendor-release evaluation logs filed in eTMF (Marinos or Veeva Vault eTMF) per TMF RM v3.3.x; automated push via `etmf-push-job`. |
| FS-INT-ETMF-02 | URS-INT-ETMF-02 | Cross-link from CTMS site-record to eTMF resolvable by `{study_id, site_id}` via REST `/v1/etmf/lookup`. |

### 4.21 Integrations — ePRO Iolanthe (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-EPRO-01 | URS-INT-EPRO-01 | ePRO data from Iolanthe ingested via CDISC ODM-XML over REST; `subject_id` + `visit_id` + `instrument_id` + `completed_at_utc` triplet reconciled against EDC casebook; mismatches raise queries. |
| FS-INT-EPRO-02 | URS-INT-EPRO-02 | ePRO compliance KPI (% completion per subject / visit) computed daily; published to RBM feed. |
| FS-INT-EPRO-03 | URS-INT-EPRO-03 | Instrument-version pinned per study (e.g., `EORTC-QLQ-C30@v3.0`); mid-study version change follows FS-BUILD-04. |

### 4.22 Integrations — LIMS Watson (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | Watson LIMS bioanalytical PK / PD data ingested via CDISC LAB / ODM-XML; sample-id ↔ subject-id ↔ visit-id reconciled; ICH M10 acceptance criteria applied upstream in LIMS. |
| FS-INT-LIMS-02 | URS-INT-LIMS-02 | Preliminary-flag LIMS records held in EDC staging until confirmation flag received; lock blocked while preliminary records exist. |

### 4.23 Integrations — SSO Okta (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-SSO-01 | URS-INT-SSO-01 | Okta SAML 2.0 + MFA; Rave local accounts disabled; SAML assertion validated server-side. |
| FS-INT-SSO-02 | URS-INT-SSO-02 | Okta groups (e.g., `marigold-rave-pi-{study}`, `marigold-rave-cra-{study}`) map to Rave roles + country / site scopes; HR-event termination deprovisions Okta and Rave session within 24 h via SCIM. |

### 4.24 Mid-Study Amendment Workflow (M-AMD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AMD-01 | URS-AMD-01 | Amendment impact-assessment template captures: affected eCRFs, edit checks, derivations, visit schedule, SDV plan, RBM plan, consent text changes, regulatory submission impact; signed by Clinical Lead + Data Manager + Medical Monitor; archived in eTMF. |
| FS-AMD-02 | URS-AMD-02 | Mid-study CRF deployment gated by FS-BUILD-04 evidence; Quick-Publish whitelist enforced (FS-BUILD-05) blocks silent semantic-changing edits. |
| FS-AMD-03 | URS-AMD-03 | Re-consent trigger flag set on amendments affecting subject rights / safety / risk-benefit; subject status auto-updated to `RECONSENT_PENDING` per affected forms; data entry on amendment-affected forms blocked. |
| FS-AMD-04 | URS-AMD-04 | Migration scripts validated in UAT against representative subject set; rollback plan documented; production migration window logged in `migration-window-log`. |

### 4.25 eConsent and Re-Consent (M-CONSENT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CONSENT-01 | URS-CONSENT-01 | eIC captured per protocol; integrates with iolanthe-econsent or per-site eConsent provider; ensures 21 CFR § 50.25 element completeness; e-signature per 21 CFR Part 11 §§ .50/.70/.100/.200. |
| FS-CONSENT-02 | URS-CONSENT-02 | Re-consent tracked per subject with `consent_version`, `signed_at_utc`, `signed_by_subject_hash`, `signed_by_investigator`, `irb_ec_approval_ref`; history preserved. |
| FS-CONSENT-03 | URS-CONSENT-03 | Subject without current-version consent blocked from amendment-affected forms via FS-AMD-03 form-block. |
| FS-CONSENT-04 | URS-CONSENT-04 | Withdrawal-of-consent captured with `effective_date`, `scope` ∈ {FULL, DATA_ONLY, FUTURE_DATA_ONLY} per EU CTR Art. 28(3); ICH E6(R3) retention treatment applied. |

### 4.26 Protocol Deviation Tracking (M-DEV)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DEV-01 | URS-DEV-01 | Deviation captured in `deviation_register` with `deviation_id`, `subject_id`, `category`, `date_occurred`, `date_identified`, `description`, `root_cause`, `corrective_action`, `importance` ∈ {IMPORTANT, NON_IMPORTANT}; ICH E6(R3) terminology. |
| FS-DEV-02 | URS-DEV-02 | IPD flag triggers Medical Monitor review queue + cross-link to CTMS deviation register via `etmf-push-job`. |
| FS-DEV-03 | URS-DEV-03 | Deviation KPI computation: rate per site, rate per subject, IPD rate; published to RBM feed daily. |

### 4.27 DSMB / IDMC Interim-Analysis Support (M-DSMB)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DSMB-01 | URS-DSMB-01 | Firewalled extract path: `dsmb-extract-job` runs in isolated Okta-scoped tenant role; outputs to a separate S3 bucket with IAM policy preventing study-conduct role read; DSMB statistician accesses via federated identity. |
| FS-DSMB-02 | URS-DSMB-02 | Closed-report (unblinded) and open-report (blinded) extracts produced separately per DSMB charter; access lists enforced by Okta groups `dsmb-{study}-closed` and `dsmb-{study}-open`. |
| FS-DSMB-03 | URS-DSMB-03 | Each extract produces manifest with `data_cut_date`, `included_subjects[]`, `included_forms[]`, `version_hash` (SHA-256); filed in eTMF under TMF RM artefact 06.02. |
| FS-DSMB-04 | URS-DSMB-04 | Adaptive-design adaptations decided by DSMB executed via FS-AMD-* mid-study amendment workflow; system does not auto-adapt; DSMB recommendation is paper / signed PDF in eTMF. |

### 4.28 CTIS / EU CTR Submission Pack (M-CTIS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CTIS-01 | URS-CTIS-01 | `ctis-extract-job` produces Annual Safety Report data extract, substantial-modification data extract, end-of-trial summary; format aligned with EMA CTIS Sponsor Handbook (current); routed via Marigold Regulatory Affairs to CTIS sponsor workspace. |
| FS-CTIS-02 | URS-CTIS-02 | SUSAR-related data extracts route via PV / Argus to EudraVigilance — Argus is the regulatory submitter; EDC is the data source for investigator-reported SAEs. |
| FS-CTIS-03 | URS-CTIS-03 | Per-country carve-out logic: DE trials route national notifications via BfArM (medicinal products) and PEI (biologicals) gateways; per-country gateway endpoints configured. |

### 4.29 ICH E9(R1) Estimand-Supporting Data (M-EST)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-EST-01 | URS-EST-01 | Intercurrent-event capture via dedicated eCRFs: `disc_treatment`, `rescue_medication`, `death_pre_outcome`, `surgical_intervention`, `dose_modification`; events propagate to SDTM as intercurrent-event indicators per ICH E9(R1). |
| FS-EST-02 | URS-EST-02 | Baseline-cohort assignment immutable in source observation record; re-classification for analysis happens in ADaM derivation, not by modifying SDTM source. |

### 4.30 Performance / Availability / Backup (M-PERF)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | P95 eCRF page-load ≤ 3 s under nominal load; verified by `OQ-PERF-PAGE-01` against a reference per-study build at 200 concurrent users. |
| FS-PERF-02 | URS-PERF-02 | SDTM export job for 500-subject Phase II ≤ 30 min wall-clock; measured on a representative reference study. |
| FS-AV-01 | URS-AV-01 | Medidata SLA 99.5% monthly tracked via Medidata Trust portal; deviations escalated to vendor + sponsor SRE; quarterly review. |
| FS-BAK-01 | URS-BAK-01 | Vendor-managed backup; vendor-published RPO ≤ 4 h, RTO ≤ 24 h verified annually via vendor-assurance evidence pack. |
| FS-BAK-02 | URS-BAK-02 | Per-study build configuration archive exported to eTMF on FPI, LPLV, hard-lock via `build-archive-job`. |
| FS-BAK-03 | URS-BAK-03 | DR drill evidenced annually by vendor; sponsor reviews drill summary + RPO/RTO conformance via vendor-assurance program. |

### 4.31 Security and Data Protection (M-SEC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SEC-01 | URS-SEC-01 | Authentication via Okta SAML 2.0 + MFA; Rave local accounts disabled; session timeout ≤ 30 min idle; FS-PART11-12 re-auth at signature events. |
| FS-SEC-02 | URS-SEC-02 | Per-study access restricted by role + country / site via Rave Site Group + Okta groups; access reviewed at FPI, every 90 days during enrolment, at LPLV; reviewers signed in eQMS. |
| FS-SEC-03 | URS-SEC-03 | Subject-identifier minimisation enforced by per-study eCRF design — subject-id pseudonymous; direct identifiers (name, DOB, address) excluded from EDC where prohibited; GDPR Art. 9 special-category controls applied. |
| FS-SEC-04 | URS-SEC-04 | GDPR Art. 22 — automated individual decision-making against the subject blocked at policy level. Any algorithmic classification (e.g., risk scoring) routed through human-review queue with audit-trail entry per decision before downstream action. |
| FS-SEC-05 | URS-SEC-05 | GDPR Art. 32 — AES-256 at rest (vendor evidence); TLS 1.3 in transit; key rotation per Medidata SOC 2 attestation; reviewed annually. |
| FS-SEC-06 | URS-SEC-06 | Per-study DPIA template (Confluence + signed PDF in eTMF) executed before FPI for special-category studies; outcomes drive eCRF minimisation, access scopes, and retention treatment. |
| FS-SEC-07 | URS-SEC-07 | HIPAA-covered US studies operate under Medidata BAA; PHI handling per per-study HIPAA-authorisation; PHI-flagged fields excluded from RBM feed payload. |
| FS-SEC-08 | URS-SEC-08 | GDPR Art. 17 subject-erasure requests triaged: where EU CTR research-record-retention overrides erasure, the request decision (refusal + rationale) is filed in eTMF; subject notified. |

### 4.32 Training and Periodic Review (M-TRN)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | LMS gate: production access blocked unless role-specific training + protocol-specific training current; expiry-warning at T-30 d; auto-block at T+0. |
| FS-TRN-02 | URS-TRN-02 | New-version-training assigned automatically when user-manual version advances or Quick-Publish changes user-visible behaviour; LMS task auto-created. |
| FS-PR-01 | URS-PR-01 | Annual platform-level periodic review per `SOP-CDM-05 Periodic Review`; per-study reviews triggered at amendments and at database lock; signed by Director CDM + VP Clinical Operations. |
| FS-PR-02 | URS-PR-02 | Periodic review confirms: RBM feed health (no gap > 48 h cumulative); audit-trail completeness; vendor-release impact-assessment current; SAE-reconciliation drift < threshold. |

### 4.33 FDA BIMO / EMA / BfArM Inspection-Readiness (M-BIMO)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BIMO-01 | URS-BIMO-01 | `bimo-bundle-job` produces on-demand: full audit trail per subject; query history per subject; signature history per subject; eCRF state at lock; SAE reconciliation evidence; coding decisions; protocol-deviation register; format PDF + CSV; bundle SHA-256-signed. |
| FS-BIMO-02 | URS-BIMO-02 | Inspector / auditor Okta group `marigold-rave-auditor-{study}` grants read-only + export-only; no edit / no signature affordances at UI or API. |
| FS-BIMO-03 | URS-BIMO-03 | BIMO bundle for 500-subject Phase II generable in ≤ 60 min wall-clock; measured on representative reference study. |

### 4.34 Multi-Language and Time-Zone (M-INTL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INTL-01 | URS-INTL-01 | eCRF labels + instructional text localised per site language via Rave i18n; supported: de-DE, de-AT, de-CH, fr-FR, en-GB, en-US, es-ES, it-IT, pl-PL, cs-CZ; underlying field semantics unchanged. |
| FS-INTL-02 | URS-INTL-02 | Visit-window calculator uses subject's local time-zone (IANA) for window enforcement; stored timestamps UTC per FS-DATA-05. |
| FS-INTL-03 | URS-INTL-03 | Locale-specific date / number / unit display via UI formatter; canonical stored values unchanged. |

---


### 4.35 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: SAML 2.0 via Entra ID with SCIM lifecycle provisioning. Conditional-access binding to policy `Clinical-Sensitive Conditional Access (FIDO2 phishing-resistant MFA + sponsor-tenant isolation)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with Oracle RMAN for the Medidata Rave Oracle backend; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.36 Cross-System Integration — Hydra + Helios (M-XINT-HYD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HYD-01 | URS-XINT-HYD-01 | Per-study config `ai_draft.enabled=false` default; egress firewall ACL blocks vendor LLM endpoints except via the Hydra gateway VIP; Marigold protocol-drafting adapter `MAR-HYD-CLIENT-1.x` enforces use-case ID. |
| FS-XINT-HYD-02 | URS-XINT-HYD-02 | Hydra use-case template `CLIN-PROTO-DRAFT-<study_id>`; gate enforces sponsor-declared `risk_class` and art-11 pack presence on Annex-I-declared studies. |
| FS-XINT-HYD-03 | URS-XINT-HYD-03 | Protocol-section ingestion hook validates watermark + dual e-signature `(medical_monitor, biostat)` and stamps study activation flag only after both signatures + watermark valid. |
| FS-XINT-HYD-04 | URS-XINT-HYD-04 | Helios ingestion via Kafka topic `helios.ingest.marigold.hydra.v1`; retention floor 2 y. |


### 4.37 Cross-System Integration — Helios handover (M-XINT-HEL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HEL-01 | URS-XINT-HEL-01 | Audit-event publisher emits Kafka topic `helios.ingest.marigold.rave.v1` with schema-registry-pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`; at-least-once delivery; idempotency key `{source_system, event_id}`; back-pressure surfaced via Prometheus `helios_publish_lag_seconds` with 5-min alert at > 600 s. |
| FS-XINT-HEL-02 | URS-XINT-HEL-02 | Local audit-store retention policy enforces ≥ 25 y; Helios ack persisted as `helios_ack_ts` per event; periodic reconciliation job verifies parity (Helios row count == local published count) and raises a deviation in MasterControl on > 0.01% mismatch over a 24 h window. |


### 4.38 Cross-System Integration — LMS handover (M-XINT-LMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-LMS-01 | URS-XINT-LMS-01 | LMS-competence adapter `<sys>-LMS-CLIENT-1.x` performs `GET /lms/competence/{user_id}?curriculum=...` over mTLS + Entra workload-identity; cache TTL per system (12-24 h); on `current=false` the consumer blocks the gated action and records `lms_lapse_user={user_id}` in the consumer audit trail; periodic reconciliation job verifies that no gated action proceeded with a lapsed competence. |

## 5. Interface Specifications

| IF ID | URS ID | Counterparty | Protocol | Direction | Notes |
|---|---|---|---|---|---|
| IF-OKTA-01 | URS-INT-SSO-01 | Okta | SAML 2.0 + SCIM 2.0 | bidirectional | SSO + MFA + provisioning |
| IF-CODER-01 | URS-INT-CODER-01..03 | Medidata Coder | vendor-internal | bidirectional | MedDRA + WHODrug |
| IF-RTSM-01 | URS-INT-RTSM-01..04 | Medidata RTSM / Calyx IXRS | vendor-internal + REST | bidirectional | rand + supply + heartbeat |
| IF-LAB-01 | URS-INT-LAB-01..03 | Central labs | CDISC LAB / ODM-XML | inbound | per-protocol mapping |
| IF-IMG-01 | URS-INT-IMG-01..02 | Imaging core lab | DICOM + REST | inbound | clinical-read derivations |
| IF-ARGUS-01 | URS-INT-SAFETY-01..04 | Argus 8.4 | SFTP + PGP | bidirectional | SAE / SUSAR reconciliation |
| IF-ETMF-01 | URS-INT-ETMF-01..02 | Marinos eTMF | REST + TMF RM | outbound | TMF Reference Model–aligned |
| IF-EPRO-01 | URS-INT-EPRO-01..03 | Iolanthe ePRO | CDISC ODM-XML + REST | inbound | ePRO ingest |
| IF-LIMS-01 | URS-INT-LIMS-01..02 | Watson LIMS | CDISC LAB / ODM-XML | inbound | bioanalytical PK/PD |
| IF-RBM-01 | URS-RBM-01..04 | Central monitoring platform | REST + CSV | outbound | RBM feed |
| IF-CTIS-01 | URS-CTIS-01..03 | CTIS / EudraVigilance | sponsor-mediated upload | outbound | regulatory submission |
| IF-PINNACLE21-01 | URS-SDTM-02..03 | Pinnacle21 (Certara) | CLI + REST | outbound | SDTM / Define-XML validation |

## 6. Data Model (high-level, platform-level)

| Entity | Attributes (illustrative) |
|---|---|
| Study | study_id, protocol_no, environment, build_version, lifecycle_state, jurisdictions[], cdash_ver, sdtm_ig_ver, meddra_ver, whodrug_ver |
| Build | build_id, study_id, version, promoted_at, promoted_by, package_sha256 |
| User | user_id (Okta sub), display_name, status, mfa_status, training_currency |
| StudyRole | study_id, user_id, role, country, site, granted_at, granted_by |
| Subject | subject_id, study_id, country, site, status, consent_version, screening_id, demog_hash |
| eCRF Form | form_id, study_id, build_version, fields[], cdash_binding, ctq_tags[] |
| Field | field_id, form_id, type, mandatory, code_list, ctq_tags[], is_esource |
| Query | query_id, subject_id, form_id, field_path, rule_id, raised_by, state, raised_at_utc, closed_at_utc, response, response_author |
| Signature | sig_id, scope, signer_id, meaning, timestamp_utc, sig_payload, record_state_hash |
| LockEvent | event_id, study_id, type {soft, hard, unlock, relock}, justification, signer_ids[], timestamp_utc, scope |
| AuditEvent | event_id, study_id, user_id, action, entity, old_value, new_value, timestamp_utc, reason_for_change |
| CodingDecision | coding_id, subject_id, term, dictionary, dictionary_version, coder_id, decision_timestamp_utc, override_rationale |
| RBMFeedRecord | record_id, study_id, site_id, kpi, value, computed_at_utc, schema_version |
| DSMBExtract | extract_id, study_id, data_cut_date, included_subjects[], version_hash |
| Consent | consent_id, subject_id, version, signed_at_utc, signed_by_subject_hash, signed_by_investigator, withdrawal_scope, withdrawal_effective_date |
| Deviation | deviation_id, subject_id, category, date_occurred, date_identified, description, importance, corrective_action |

## 7. Non-Functional Specifications

| NFR ID | Specification |
|---|---|
| NFR-01 | P95 eCRF page-load ≤ 3 s |
| NFR-02 | SDTM export ≤ 30 min for 500-subject study |
| NFR-03 | Medidata SLA 99.5% monthly availability — escalated monthly |
| NFR-04 | Vendor RPO ≤ 4 h / RTO ≤ 24 h verified annually |
| NFR-05 | Audit trail append-only; never disabled in production |
| NFR-06 | Retention ≥ 25 y post-trial completion |
| NFR-07 | Subject-identifier minimisation per protocol |
| NFR-08 | TLS 1.3 in transit; AES-256 at rest |
| NFR-09 | RBM feed gap ≤ 48 h cumulative |
| NFR-10 | SAE reconciliation drift ≤ 5 business days |
| NFR-11 | BIMO bundle ≤ 60 min wall-clock for 500-subject study |
| NFR-12 | Pinnacle21 ERROR-class findings blocking submission |

## 8. Configuration Items (CI)

| CI ID | Item | Configured Value | Source |
|---|---|---|---|
| CI-01 | IdP | Okta SAML 2.0 + MFA | URS-INT-SSO-01 |
| CI-02 | Study environments | DEV, QC, UAT, PRODUCTION | URS-BUILD-01 |
| CI-03 | Audit trail | append-only, exportable, watchdog enabled | URS-AUD-02 + URS-AUD-05 |
| CI-04 | Retention | 25 y minimum | URS-AUD-04 |
| CI-05 | Investigator-signature scope | form + casebook | URS-SIG-01 |
| CI-06 | Re-authentication on signing | required | URS-PART11-12 |
| CI-07 | Coder MedDRA version policy | per-protocol pinned (v27.0 default) | URS-COD-01 |
| CI-08 | Coder WHODrug version policy | per-protocol pinned (Global B3 Mar-2026 default) | URS-COD-02 |
| CI-09 | Lock checklist | queries closed + SDV complete + medical review + listings + signatures + coding + SAE reconciled + RBM feed current | URS-LOCK-01 |
| CI-10 | Unlock workflow | justification + scope + re-lock | URS-LOCK-02 |
| CI-11 | Final-dataset formats | CDISC ODM + SDTM + Define-XML; optional Dataset-JSON | URS-LOCK-03..04, URS-SDTM-04 |
| CI-12 | RBM feed cadence | daily (configurable) | URS-RBM-01 |
| CI-13 | RBM feed schema | rbm-feed@v1 | URS-RBM-04 |
| CI-14 | SAE transmission window | ≤ 24 h investigator-confirmation to Argus | URS-INT-SAFETY-01 |
| CI-15 | SUSAR clock owner | Argus / Sponsor PV (NOT EDC) | URS-INT-SAFETY-02 |
| CI-16 | SAE drift threshold | 5 business days | URS-INT-SAFETY-03 |
| CI-17 | DSMB extract path | firewalled S3 + Okta-federated role | URS-DSMB-01 |
| CI-18 | DSMB report types | closed (unblinded) + open (blinded) | URS-DSMB-02 |
| CI-19 | CTIS extract route | Marigold Reg Affairs → CTIS sponsor workspace | URS-CTIS-01 |
| CI-20 | Quick-Publish whitelist | typo / label / edit-check semantic-equivalent / entry-restriction | URS-BUILD-05 |
| CI-21 | Custom-function policy | locked to build version; no prod free-form | URS-DATA-04 |
| CI-22 | RBQM SDVV | critical (CtQ) 100%; non-critical risk-based | URS-SDV-01 |
| CI-23 | Vendor release-evaluation cadence | each Rave release (≤ 14 days) | URS-VND-02 |
| CI-24 | Languages | de-DE, de-AT, de-CH, fr-FR, en-GB, en-US, es-ES, it-IT, pl-PL, cs-CZ | URS-INTL-01 |
| CI-25 | Pinnacle21 gate | ERROR-class findings block submission | URS-SDTM-02 |
| CI-26 | Audit-trail-watchdog | heartbeat every 5 min; gap > 15 min → READ_ONLY | URS-AUD-05 |
| CI-27 | IXRS heartbeat | every 15 min; > 4 misses → P1 alert | URS-INT-RTSM-04 |
| CI-28 | Reason-for-change vocabulary | controlled enum + free-text JUSTIFY | URS-AUD-07 |
| CI-29 | Re-consent block | data entry blocked on amendment-affected forms | URS-CONSENT-03 |
| CI-30 | Inspector role | read-only + export-only | URS-BIMO-02 |

## 9. Constraints / Assumptions / Risks

- **Constraints:** Vendor-managed infrastructure; quarterly vendor releases not under site change control; per-study free-form scripting prohibited in production without Cat-5 sub-component RA; Argus is the regulatory submitter for SUSARs; CTIS submission operated by sponsor Reg Affairs.
- **Assumptions:** Okta, Medidata Coder, RTSM, eTMF (Marinos / Veeva), Argus, Iolanthe ePRO, Watson LIMS, central labs, imaging core lab, BfArM + PEI gateways, CTIS are validated; per-study DSMB charter / RBM plan / monitoring plan / eConsent IRB approval / DPIA in place before FPI.
- **FS-level risks:** Mid-study amendment defect (mitigation: FS-BUILD-04 + FS-AMD-* + UAT); SDV bypass via misconfigured RBM plan (mitigation: FS-SDV-* + FS-RBM-*); investigator-credential compromise (mitigation: FS-SIG-* + FS-SEC-01); SAE reconciliation drift (mitigation: FS-INT-SAFETY-03 daily job + eTMF reconciliation log); RBM feed gap (mitigation: FS-RBM-03 watchdog + lock-block); audit-trail disablement (mitigation: FS-AUD-05 heartbeat watchdog + system-READ_ONLY enforcement); IXRS silent failure (mitigation: FS-INT-RTSM-04 heartbeat); duplicate enrolment / re-randomisation (mitigation: FS-INT-RTSM-02); DSMB data leak (mitigation: FS-DSMB-01 firewalled S3 + Okta-federated role); Pinnacle21 ERROR-class findings at submission (mitigation: pre-submission validation in `sdtm-export-job` + biostatistics review).

## 10. References

- MAR-URS-EDC-001 v1.2 (parent URS).
- 21 CFR Part 11 §§ .10(a)–(k), .30, .50, .70, .100, .200, .300.
- 21 CFR Parts 50 + 56 (informed consent + IRB).
- 21 CFR Parts 312 + 314 (IND + NDA).
- FDA *Computerized Systems Used in Clinical Investigations* (May 2007).
- FDA *Electronic Source Data in Clinical Investigations* (Sep 2013).
- FDA *Use of Electronic Informed Consent — Q&A* (final).
- FDA *Establishment and Operation of Clinical Trial Data Monitoring Committees* (current).
- FDA BIMO Inspection Manual 7348.809 (updated 4 April 2025).
- ICH E6(R3) GCP (Step 4, adopted 6 January 2025); ICH E8(R1); ICH E9(R1); ICH E2A; ICH E2B(R3); ICH M11.
- EU CTR Regulation 536/2014 + CTIS Sponsor Handbook.
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EMA *Guideline on Computerised Systems and Electronic Data*.
- GDPR Reg. (EU) 2016/679 — Arts. 6, 9, 17, 22, 32, 33, 35.
- HIPAA / HITECH.
- CDISC SDTM-IG v3.4 / ADaM-IG v1.3 / CDASH-IG v2.3 / ODM-XML v1.3.2 / Define-XML v2.1 / Dataset-JSON v1.0.
- ISPE GAMP 5 (2nd ed., 2022); GAMP GPG *Computerised Systems in Regulated GCP*.
- PIC/S PI 041; ISO/IEC 27001:2022.
- Medidata — *Rave EDC 2024 Validation Approach*; Rave Architect Essentials; Medidata Trust portal.
- BfArM; Paul-Ehrlich-Institut (PEI); Swissmedic; AGES PharmMed.

## 11. Appendix A — URS → FS Traceability Matrix (platform-level)

| URS ID | FS ID(s) | Notes |
|---|---|---|
| URS-VND-01 | FS-VND-01 | Vendor evidence register |
| URS-VND-02 | FS-VND-02 | Release-evaluation runbook |
| URS-VND-03 | FS-VND-03 | Sub-processor inventory |
| URS-VND-04 | FS-VND-04 | Incident notification |
| URS-BUILD-01 | FS-BUILD-01 | Environment isolation |
| URS-BUILD-02 | FS-BUILD-02 | Promotion signatures |
| URS-BUILD-03 | FS-BUILD-03 | UAT plan |
| URS-BUILD-04 | FS-BUILD-04 | Amendment migration |
| URS-BUILD-05 | FS-BUILD-05 | Quick-Publish whitelist |
| URS-BUILD-06 | FS-BUILD-06 | Build package fingerprint |
| URS-BUILD-07 | FS-BUILD-07 | Architect template registry |
| URS-BUILD-08 | FS-BUILD-08 | CtQ register |
| URS-CRF-01 | FS-CRF-01 | CDASH binding |
| URS-CRF-02 | FS-CRF-02 | Field constraints |
| URS-CRF-03 | FS-CRF-03 | Visit window |
| URS-CRF-04 | FS-CRF-04 | Casebook completion |
| URS-CRF-05 | FS-CRF-05 | CtQ tag link |
| URS-DATA-01 | FS-DATA-01 | Field constraints |
| URS-DATA-02 | FS-DATA-02 | Edit-check engine |
| URS-DATA-03 | FS-DATA-03 | Derivation framework |
| URS-DATA-04 | FS-DATA-04 | Custom-function library |
| URS-DATA-05 | FS-DATA-05 | TZ storage |
| URS-DATA-06 | FS-DATA-06 | Impossible-date guard |
| URS-DATA-07 | FS-DATA-07 | Mobile / offline |
| URS-ESRC-01 | FS-ESRC-01 | eSource flag |
| URS-ESRC-02 | FS-ESRC-02 | Contemporaneous capture |
| URS-ESRC-03 | FS-ESRC-03 | Device registry |
| URS-ESRC-04 | FS-ESRC-04 | --ORIG metadata |
| URS-QRY-01 | FS-QRY-01 | Source taxonomy |
| URS-QRY-02 | FS-QRY-02 | Query schema |
| URS-QRY-03 | FS-QRY-03 | No-reopen-post-lock |
| URS-QRY-04 | FS-QRY-04 | Aging KPI |
| URS-QRY-05 | FS-QRY-05 | Bulk-query runner |
| URS-SDV-01 | FS-SDV-01 | RBM-driven SDV plan |
| URS-SDV-02 | FS-SDV-02 | SDR-distinct event |
| URS-SDV-03 | FS-SDV-03 | Remote-SDV flag |
| URS-SDV-04 | FS-SDV-04 | SDV exception report |
| URS-RBM-01 | FS-RBM-01 | RBM feed |
| URS-RBM-02 | FS-RBM-02 | Combined-monitoring support |
| URS-RBM-03 | FS-RBM-03 | Feed-gap watchdog |
| URS-RBM-04 | FS-RBM-04 | Feed schema version |
| URS-COD-01 | FS-COD-01 | MedDRA version |
| URS-COD-02 | FS-COD-02 | WHODrug version |
| URS-COD-03 | FS-COD-03 | Auto + manual override |
| URS-COD-04 | FS-COD-04 | Dictionary upgrade |
| URS-COD-05 | FS-COD-05 | Coding-audit export |
| URS-COD-06 | FS-COD-06 | Synonym version control |
| URS-SIG-01 | FS-SIG-01 | Form / casebook signature |
| URS-SIG-02 | FS-SIG-02 | Re-sign on change |
| URS-SIG-03 | FS-SIG-03 | Meaning template |
| URS-SIG-04 | FS-SIG-04 | Casebook PDF |
| URS-PART11-01 | FS-PART11-01 | SOP suite (§ 11.10(a)) |
| URS-PART11-02 | FS-PART11-02 | Reproducible copies (§ 11.10(b)) |
| URS-PART11-03 | FS-PART11-03 | Retention (§ 11.10(c)) |
| URS-PART11-04 | FS-PART11-04 | Access control (§ 11.10(d)) |
| URS-PART11-05 | FS-PART11-05 | Audit trail (§ 11.10(e)) |
| URS-PART11-06 | FS-PART11-06 | Authority checks (§ 11.10(g)) |
| URS-PART11-07 | FS-PART11-07 | Manuals + change control (§ 11.10(k)) |
| URS-PART11-08 | FS-PART11-08 | Open-system (§ 11.30) |
| URS-PART11-09 | FS-PART11-09 | § 11.50 manifestations |
| URS-PART11-10 | FS-PART11-10 | § 11.70 binding |
| URS-PART11-11 | FS-PART11-11 | § 11.100 uniqueness |
| URS-PART11-12 | FS-PART11-12 | § 11.200 re-auth |
| URS-PART11-13 | FS-PART11-13 | § 11.300 password policy |
| URS-AUD-01 | FS-AUD-01 | Audit trail schema |
| URS-AUD-02 | FS-AUD-02 | Append-only + export |
| URS-AUD-03 | FS-AUD-03 | Audit-trail review |
| URS-AUD-04 | FS-AUD-04 | Retention 25y |
| URS-AUD-05 | FS-AUD-05 | Watchdog never-disable |
| URS-AUD-06 | FS-AUD-06 | Reason-for-change |
| URS-AUD-07 | FS-AUD-07 | Reason vocabulary |
| URS-LOCK-01 | FS-LOCK-01 | Soft vs hard + checklist |
| URS-LOCK-02 | FS-LOCK-02 | Unlock workflow |
| URS-LOCK-03 | FS-LOCK-03 | SDTM + Define-XML export |
| URS-LOCK-04 | FS-LOCK-04 | ADaM derivation lineage |
| URS-LOCK-05 | FS-LOCK-05 | Lock delta |
| URS-LOCK-06 | FS-LOCK-06 | Lock-evidence pack |
| URS-SDTM-01 | FS-SDTM-01 | SDTM mapping spec |
| URS-SDTM-02 | FS-SDTM-02 | Pinnacle21 validation |
| URS-SDTM-03 | FS-SDTM-03 | Define-XML generation |
| URS-SDTM-04 | FS-SDTM-04 | Dataset-JSON option |
| URS-SDTM-05 | FS-SDTM-05 | SDTM round-trip verifier |
| URS-INT-CODER-01 | FS-INT-CODER-01 / IF-CODER-01 | AE coding |
| URS-INT-CODER-02 | FS-INT-CODER-02 / IF-CODER-01 | Conmed coding |
| URS-INT-CODER-03 | FS-INT-CODER-03 / IF-CODER-01 | Coder failure |
| URS-INT-RTSM-01 | FS-INT-RTSM-01 / IF-RTSM-01 | RTSM reconciliation |
| URS-INT-RTSM-02 | FS-INT-RTSM-02 / IF-RTSM-01 | Duplicate-enrolment guard |
| URS-INT-RTSM-03 | FS-INT-RTSM-03 / IF-RTSM-01 | Drug accountability |
| URS-INT-RTSM-04 | FS-INT-RTSM-04 / IF-RTSM-01 | Heartbeat protocol |
| URS-INT-LAB-01 | FS-INT-LAB-01 / IF-LAB-01 | CDISC LAB ingest |
| URS-INT-LAB-02 | FS-INT-LAB-02 / IF-LAB-01 | Local-lab mapping |
| URS-INT-LAB-03 | FS-INT-LAB-03 / IF-LAB-01 | Anomaly detector |
| URS-INT-IMG-01 | FS-INT-IMG-01 / IF-IMG-01 | DICOM gateway |
| URS-INT-IMG-02 | FS-INT-IMG-02 / IF-IMG-01 | --ORIG ASSIGNED |
| URS-INT-SAFETY-01 | FS-INT-SAFETY-01 / IF-ARGUS-01 | SAE 24h transmission |
| URS-INT-SAFETY-02 | FS-INT-SAFETY-02 / IF-ARGUS-01 | SUSAR clock propagation |
| URS-INT-SAFETY-03 | FS-INT-SAFETY-03 / IF-ARGUS-01 | Drift detector |
| URS-INT-SAFETY-04 | FS-INT-SAFETY-04 / IF-ARGUS-01 | Narrative read-only |
| URS-INT-ETMF-01 | FS-INT-ETMF-01 / IF-ETMF-01 | TMF RM filing |
| URS-INT-ETMF-02 | FS-INT-ETMF-02 / IF-ETMF-01 | CTMS cross-link |
| URS-INT-EPRO-01 | FS-INT-EPRO-01 / IF-EPRO-01 | ePRO ingest |
| URS-INT-EPRO-02 | FS-INT-EPRO-02 / IF-EPRO-01 | Compliance KPI |
| URS-INT-EPRO-03 | FS-INT-EPRO-03 / IF-EPRO-01 | Instrument version pin |
| URS-INT-LIMS-01 | FS-INT-LIMS-01 / IF-LIMS-01 | Watson PK ingest |
| URS-INT-LIMS-02 | FS-INT-LIMS-02 / IF-LIMS-01 | Preliminary hold |
| URS-INT-SSO-01 | FS-INT-SSO-01 / IF-OKTA-01 | Okta SAML + MFA |
| URS-INT-SSO-02 | FS-INT-SSO-02 / IF-OKTA-01 | SCIM provisioning |
| URS-AMD-01 | FS-AMD-01 | Impact assessment |
| URS-AMD-02 | FS-AMD-02 | No silent CRF change |
| URS-AMD-03 | FS-AMD-03 | Re-consent trigger |
| URS-AMD-04 | FS-AMD-04 | Migration scripts |
| URS-CONSENT-01 | FS-CONSENT-01 | eIC capture |
| URS-CONSENT-02 | FS-CONSENT-02 | Re-consent tracking |
| URS-CONSENT-03 | FS-CONSENT-03 | Form-block on pending |
| URS-CONSENT-04 | FS-CONSENT-04 | Withdrawal scope |
| URS-DEV-01 | FS-DEV-01 | Deviation register |
| URS-DEV-02 | FS-DEV-02 | IPD flag + CTMS cross-link |
| URS-DEV-03 | FS-DEV-03 | Deviation KPI |
| URS-DSMB-01 | FS-DSMB-01 | Firewalled extract path |
| URS-DSMB-02 | FS-DSMB-02 | Closed vs open report |
| URS-DSMB-03 | FS-DSMB-03 | Extract manifest |
| URS-DSMB-04 | FS-DSMB-04 | Adaptive via amendment |
| URS-CTIS-01 | FS-CTIS-01 / IF-CTIS-01 | ASR / SM / EoT extract |
| URS-CTIS-02 | FS-CTIS-02 / IF-CTIS-01 | SUSAR route via Argus |
| URS-CTIS-03 | FS-CTIS-03 / IF-CTIS-01 | DACH carve-out |
| URS-EST-01 | FS-EST-01 | Intercurrent event eCRFs |
| URS-EST-02 | FS-EST-02 | Baseline immutable |
| URS-PERF-01 | FS-PERF-01 | P95 page load |
| URS-PERF-02 | FS-PERF-02 | Export wall-clock |
| URS-AV-01 | FS-AV-01 | Medidata SLA |
| URS-BAK-01 | FS-BAK-01 | Vendor backup RPO/RTO |
| URS-BAK-02 | FS-BAK-02 | Milestone archive |
| URS-BAK-03 | FS-BAK-03 | DR drill annual |
| URS-SEC-01 | FS-SEC-01 | Okta + MFA + timeout |
| URS-SEC-02 | FS-SEC-02 | Access review cadence |
| URS-SEC-03 | FS-SEC-03 | Subject-id minimisation |
| URS-SEC-04 | FS-SEC-04 | GDPR Art. 22 block |
| URS-SEC-05 | FS-SEC-05 | GDPR Art. 32 crypto |
| URS-SEC-06 | FS-SEC-06 | DPIA per study |
| URS-SEC-07 | FS-SEC-07 | HIPAA BAA |
| URS-SEC-08 | FS-SEC-08 | GDPR Art. 17 triage |
| URS-TRN-01 | FS-TRN-01 | LMS gate |
| URS-TRN-02 | FS-TRN-02 | New-version training |
| URS-PR-01 | FS-PR-01 | Annual + per-study PR |
| URS-PR-02 | FS-PR-02 | PR scope expansion |
| URS-BIMO-01 | FS-BIMO-01 | BIMO bundle job |
| URS-BIMO-02 | FS-BIMO-02 | Inspector role |
| URS-BIMO-03 | FS-BIMO-03 | Bundle perf target |
| URS-INTL-01 | FS-INTL-01 | i18n labels |
| URS-INTL-02 | FS-INTL-02 | TZ-aware visit calc |
| URS-INTL-03 | FS-INTL-03 | Locale formatting |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-HYD-01 | FS-XINT-HYD-01 |
| URS-XINT-HYD-02 | FS-XINT-HYD-02 |
| URS-XINT-HYD-03 | FS-XINT-HYD-03 |
| URS-XINT-HYD-04 | FS-XINT-HYD-04 |
| URS-XINT-HEL-01 | FS-XINT-HEL-01 |
| URS-XINT-HEL-02 | FS-XINT-HEL-02 |
| URS-XINT-LMS-01 | FS-XINT-LMS-01 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

The following risks are noted for downstream evaluation in the Risk Assessment.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Mid-study amendment defect causing data loss or silent CRF change without re-validation | Medium | High | URS-BUILD-04, URS-AMD-01..04 |
| R-02 | SDV / SDR bypass via misconfigured RBM plan, leading to undetected source-eCRF divergence on a CtQ field | Medium | High | URS-SDV-01..04, URS-RBM-01..04 |
| R-03 | Investigator-signature compromise (credential theft, MFA bypass) | Low | High | URS-SIG-*, URS-SEC-01..02 |
| R-04 | Database lock / unlock without justification or with insufficient evidence | Medium | High | URS-LOCK-01..06 |
| R-05 | SAE reconciliation drift between EDC and Argus, missing a SUSAR clock | Medium | High | URS-INT-SAFETY-01..04 |
| R-06 | Edit-checks bypass via direct database write (vendor escalation) | Low | High | URS-AUD-01..07 (audit-trail catch); URS-DATA-04 |
| R-07 | Query re-opened after data-lock without unlock workflow | Low | High | URS-QRY-03, URS-LOCK-02 |
| R-08 | ICH E6(R3) RBM data-feed failure for > 48 h leading to undetected site-risk emergence | Medium | High | URS-RBM-03 |
| R-09 | GDPR Art. 22 violation via auto-classification routing subjects into investigation arms without human review | Low | High | URS-SEC-04 |
| R-10 | SDTM export round-trip data corruption (numeric precision / character-encoding mismatch) | Low | High | URS-LOCK-03, URS-SDTM-02..05 |
| R-11 | eConsent re-consent missed after a protocol amendment affecting subject rights / safety | Medium | High | URS-AMD-03, URS-CONSENT-01..04 |
| R-12 | Mid-study MedDRA / WHODrug version change without re-coding plan, corrupting AE / conmed trend data | Medium | Medium | URS-COD-01..06 |
| R-13 | IXRS / IRT integration silent failure → randomisation mismatch + dispensing error | Low | High | URS-INT-RTSM-04 |
| R-14 | Subject re-randomisation on duplicate enrolment (screen-fail re-screened under new id) | Low | High | URS-INT-RTSM-02 |
| R-15 | Audit trail inadvertently disabled in production (known BIMO finding pattern) | Low | High | URS-AUD-05 |
| R-16 | DSMB unblinded data leak via insufficient extract-path firewalling | Low | High | URS-DSMB-01..03 |
| R-17 | Coding-decision audit-trail incompleteness on inspection (BIMO Form 483 pattern) | Low | High | URS-COD-05 |
| R-18 | Define-XML / SDTM-IG validation failure at submission (Pinnacle21 errors) blocking submission | Medium | Medium | URS-SDTM-02..03 |

Full evaluation in `MAR-RA-EDC-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
