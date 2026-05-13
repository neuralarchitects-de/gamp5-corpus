---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; T4 hand-expansion 2026-05-12"
seed_corpus_basis:
  - "DRY-URS-CTMS-001 (parent URS) v1.2"
  - "GAMP 5 (2nd ed.) Cat 4 SaaS conventions"
  - "21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300; 21 CFR Parts 312, 314, 50, 56"
  - "ICH E6(R3) (Step 4, 6 January 2025); ICH E8(R1); ICH E2A"
  - "EU CTR 536/2014 + CTIS Sponsor Handbook"
  - "FDA Computerized Systems Used in Clinical Investigations (May 2007)"
  - "FDA BIMO Inspection Manual 7348.809 (4 April 2025)"
  - "Veeva Vault CTMS 24R3 / 25R1 vendor documentation"
  - "TMF Reference Model v3.3.x"
parent_urs:
  document_number: DRY-URS-CTMS-001
  version: 1.2
  file: ../../URS/_generated/final/CTMS_Clinical_Trial_Management_System__Dryad_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## CTMS — Veeva Vault CTMS (24R3 / 25R1)

**Document Number:** DRY-FS-CTMS-001 | **Version:** 1.0 | **Effective Date:** 2026-04-27 *(synthetic)*
**Parent URS:** DRY-URS-CTMS-001 v1.2 | **Site:** Dryad Pharma a.s., Brno, Czech Republic *(fictional)*
**System Class:** GAMP Cat 4 — Configured Product (multi-tenant SaaS)
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Parts 312/314/50/56; ICH E6(R3) (Step 4, 6 January 2025); ICH E8(R1); ICH E2A; EU CTR 536/2014 + CTIS; FDA *Computerized Systems Used in Clinical Investigations* (May 2007); FDA BIMO Inspection Manual 7348.809 (4 April 2025); GDPR; ISO 14155:2020 (device arms); TMF RM v3.3.x

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (VP Clinical Operations) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs — CTIS) | _____________ | _____________ | _____ |
| Reviewer (Pharmacovigilance Lead) | _____________ | _____________ | _____ |
| Reviewer (Data Protection Officer) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue, derived from DRY-URS-CTMS-001 v1.0. |
| 1.2 | 2026-05-12 | (synthetic) | **Paired to URS v1.2 T4 expansion.** Every URS-ID in the v1.2 canonical ID space (URS-PROT-/URS-CTRY-/URS-SITE-/URS-INV-/URS-REC-/URS-MV-/URS-SDV-/URS-RBM-/URS-ISS-/URS-DRG-/URS-PAY-/URS-BUD-/URS-VEN-/URS-ETMF-/URS-SAF-/URS-AUD-/URS-PART11-/URS-INT-*/URS-DSMB-/URS-DEV-/URS-BIMO-/URS-DOC-/URS-CLO-/URS-INTL-/URS-PERF-/URS-AV-/URS-BAK-/URS-SEC-/URS-TRN-/URS-PR-/URS-CTIS-) has its own FS-ID row in § 4 and § 8 with per-ID implementation detail (Veeva Vault CTMS config items, Vault Connect endpoints, MasterControl REST + idempotency, Financials idempotency, EDC-CTMS protocol-deviation feed per Vault 24R3, BIMO export, DSMB tracking, audit-trail watchdog). |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## Definitions

Inherited from DRY-URS-CTMS-001. Additional FS-specific terms:

| Term | Definition |
|---|---|
| Vault Connect | Veeva's native cross-vault data-sharing service |
| Vault REST | Veeva's REST API for external integrations |
| EDL | Expected Document List per TMF Reference Model |
| SCIM | System for Cross-domain Identity Management (provisioning protocol) |

## 1. Purpose

This FS specifies how Veeva Vault CTMS (24R3 / 25R1 release line) is configured at the platform level to satisfy `DRY-URS-CTMS-001` v1.2 — managing study planning, country / site activation, investigator + delegation tracking, recruitment forecasting, monitoring + RBM, action items + CAPA, drug supply tracking, payments + budget, vendor management, eTMF + EDC + Argus + Financials + Okta + HR integrations, DSMB tracking, deviation tracking, CTIS submission tracking, inspection-readiness, multi-language + time-zone support across Dryad's clinical portfolio.

## 2. Scope

Per the URS: Vault CTMS 24R3 / 25R1 tenancy, per-study configuration, SSO via Okta + MFA, integrations with Vault eTMF, Medidata Rave EDC (enrolment + status + protocol-deviation Connection per 24R3), Medidata RTSM, Argus (PV metadata), MasterControl (eQMS), Financials (per-site payments), HR (CRA assignment), CTIS sponsor workspace tracking, BIMO inspection-readiness, DSMB / IDMC tracking.

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | GAMP Cat | Notes |
|---|---|---|---|
| C-01 | Vault CTMS tenancy (24R3 / 25R1) | 4 | Veeva multi-tenant SaaS |
| C-02 | Okta IdP | (infra) | SAML 2.0 + SCIM 2.0 |
| C-03 | Vault eTMF | 4 | Vault Connect cross-link |
| C-04 | Medidata Rave EDC | 4 | Clinical Operations–EDC Connection (Vault 24R3+) |
| C-05 | Medidata RTSM / Calyx IXRS | 4 | randomisation / supply feeds |
| C-06 | Oracle Argus 8.4 | 4 | PV metadata feeds |
| C-07 | MasterControl (eQMS) | 4 | CAPA via REST |
| C-08 | Financials system | 4 | per-site payment push |
| C-09 | HR system | 4 | CRA assignment + termination |
| C-10 | CTIS sponsor workspace | external | EMA-operated, sponsor-mediated |

### 3.2 Logical Architecture (textual)

```
                       Okta IdP (SAML 2.0 + SCIM)
                                │
                                ▼
   ┌───────────────────────────────────────────────────────────┐
   │              Vault CTMS 24R3/25R1 (Dryad tenancy)         │
   │   Protocols / Amendments / Countries / Sites / Investiga- │
   │   tors / Delegation / Recruitment / Monitoring Visits /   │
   │   MVRs / Action Items / Deviations / Drug Supply / Pay-   │
   │   ments / Vendors / DSMB / Documents / CTIS-tracking      │
   └─┬─────────┬─────────┬───────┬─────────┬────────┬─────────┘
     │         │         │       │         │        │
     ▼         ▼         ▼       ▼         ▼        ▼
  Vault     EDC (Rave   RTSM/   Argus    Master-   Financials
  eTMF      Clinical    IXRS    (PV       Control  (per-site
  (Vault    Ops–EDC    (rand   metadata) (CAPA     payments)
  Connect)  Connection) supply)           REST)
                │
                ▼
            CTIS sponsor workspace (Reg Affairs–mediated)
                │
                ▼
            BfArM / PEI / AGES / Swissmedic (national CA tracking)
```

## 4. Functional Specifications

### 4.1 Vendor / Platform Assurance (M-VND)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VND-01 | URS-VND-01 | Vendor-assurance evidence (SOC 2 Type II, ISO 27001:2022, GDPR DPA + sub-processor list, customer-shared CSV summary) tracked in `vendor-quality-register`; annual review; signed acceptance. |
| FS-VND-02 | URS-VND-02 | Quarterly Veeva-release evaluation runbook: read release notes from Veeva customer portal within 14 days; classify impact; impacted studies routed to re-validation. |
| FS-VND-03 | URS-VND-03 | Sub-processor inventory from Veeva DPA Annex reviewed annually by DPO. |
| FS-VND-04 | URS-VND-04 | Vendor incident notifications tracked in `vendor-incident-log`; breach notifications propagate to Dryad DPO within 24 h for GDPR Art. 33 clock. |

### 4.2 Protocol and Amendment Management (M-PROT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PROT-01 | URS-PROT-01 | Vault Protocol object: `protocol_id`, `version`, `version_effective_date`, `ib_version_ref`, `sponsor_approval_sig`, `country_submission_status[]`. |
| FS-PROT-02 | URS-PROT-02 | Vault Amendment object linked to Protocol: `amendment_id`, `version`, `effective_date`, `impact_category` ∈ {ADMINISTRATIVE, SUBSTANTIAL}, `change_summary`, `propagation_status` to EDC/RTSM/eTMF. |
| FS-PROT-03 | URS-PROT-03 | Substantial-modification amendments trigger workflow `ctis-sm-submission` (FS-CTIS-01); status tracking from DRAFT → SUBMITTED → CA_DECISION → PUBLISHED. |
| FS-PROT-04 | URS-PROT-04 | Downstream-task generator from amendment impact assessment: re-consent triggers per Marigold EDC (MAR-URS-EDC-001 URS-CONSENT-* family), EDC re-build per Marigold (MAR-URS-EDC-001 URS-BUILD family), monitoring-plan update per FS-MV-*. |

### 4.3 Country / Site Activation (M-CTRY, M-SITE)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CTRY-01 | URS-CTRY-01 | Vault Country object: `country_id`, `national_ca` ∈ {BfArM, PEI, AGES, Swissmedic, FDA, ...}, `submission_status_initial`, `substantial_modifications[]`, `end_of_trial_status`, `planned_activation_date`, `actual_activation_date`. |
| FS-CTRY-02 | URS-CTRY-02 | Country-level milestone gating: CA submission → CA decision → IRB / EC approval → first site activation; each gate captures planned + actual dates + signatures. |
| FS-SITE-01 | URS-SITE-01 | Vault Site object: `site_id`, `country_id`, `pi_id`, `address` (encrypted), `irb_ec_oversight`, `lifecycle_state` ∈ {IDENTIFIED, QUALIFIED, INITIATED, ENROLLING, ENROLLMENT_CLOSED, FOLLOW_UP, CLOSED}. |
| FS-SITE-02 | URS-SITE-02 | Activation checklist enforced via Site Activation Plan: 1572 (IND) / EU investigator file; CV; financial-disclosure; IRB/EC approval; current ICF; site-staff training; signed CTA; insurance; SIV report. Checklist completion required before INITIATED. |
| FS-SITE-03 | URS-SITE-03 | CRA Lead signature required for activation; activation gated on country CA decision (FS-CTRY-02) + checklist completion (FS-SITE-02). |
| FS-SITE-04 | URS-SITE-04 | Site lifecycle state transitions e-signed per FS-PART11-09 + FS-PART11-10; audit trail captures prior + new state, actor, timestamp, reason. |
| FS-SITE-05 | URS-SITE-05 | Site Contacts sub-object: role, contact info (PII encrypted at rest), start / end dates. |
| FS-SITE-06 | URS-SITE-06 | Site enrolment plan vs actual visible at country + study aggregates via Vault report; forecasting via `enrol-forecast-job` (FS-REC-02). |

### 4.4 Investigator and Delegation (M-INV)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INV-01 | URS-INV-01 | Vault Investigator object: `investigator_id`, name, credentials, `cv_version`, `financial_disclosure_status`, `coi_status`, `training_records[]`, `study_assignments[]`. |
| FS-INV-02 | URS-INV-02 | Vault 1572 sub-object: `form_version`, `effective_date`, `signed_by_pi_date`, `subinvestigators[]`; re-sign triggers per 21 CFR § 312.53(c) — new protocol added to IND; new sub-I added; PI change. OMB-expiration handled per FDA guidance (no re-sign required solely on OMB expiry). |
| FS-INV-03 | URS-INV-03 | Vault Delegation Log: per site per study; `delegated_tasks[]` (e.g., INFORMED_CONSENT, DOSE_PREP, DATA_ENTRY, AE_ASSESSMENT, SAMPLE_COLLECTION), `delegate_id`, `start_date`, `end_date`, `pi_signature_date`. |
| FS-INV-04 | URS-INV-04 | `inv-training-check-job` runs at site-activation and at periodic-review; expired training blocks activation + raises P2 alert at study. |
| FS-INV-05 | URS-INV-05 | PI-change workflow `pi-transition` requires: new 1572 generation; IRB notification record; sub-I re-delegation log; ICF re-approval task (if applicable); old PI status → INACTIVE. |

### 4.5 Subject Recruitment Forecasting (M-REC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REC-01 | URS-REC-01 | Per-site enrolment plan captured at study start; actuals ingested daily from EDC + RTSM via Vault Connect. |
| FS-REC-02 | URS-REC-02 | `enrol-forecast-job` projects FPI / LPI / LPLV given current velocity + dropout rate; daily refresh. |
| FS-REC-03 | URS-REC-03 | Recruitment KPIs (screen-failure rate, screen-to-randomise ratio, time-to-FPI, time-to-LPI) computed in Vault Report; fed to central monitoring. |
| FS-REC-04 | URS-REC-04 | Exception alerts: site < 50% plan for > 30 days; country stalled — raise action items via FS-ISS-02. |

### 4.6 Monitoring Visits and MVRs (M-MV)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MV-01 | URS-MV-01 | Monitoring-visit plan configured per study per RBM; visit types {SIV, IMV, MMV, COV, REMOTE_MV}; cadence per-site risk-tier; on-site vs remote split per RBM plan. |
| FS-MV-02 | URS-MV-02 | MVR object schema: `mvr_id`, `visit_type`, `site_id`, `planned_date`, `actual_date`, `attendees[]`, `findings`, `action_items[]`, `follow_up_sla`, `deviations[]`, `sae_followup[]`, `signature_blocks[]`. |
| FS-MV-03 | URS-MV-03 | MVR approval requires CRA Lead signature via Vault e-signature; signed MVRs immutable; un-sign requires Director Clinical Ops IT approval per unlock-workflow. |
| FS-MV-04 | URS-MV-04 | Action items track owner, due date, status, escalation rule (T+0 owner; T+7 CRA Lead; T+14 Clinical Ops Manager); evidence-of-closure required. |
| FS-MV-05 | URS-MV-05 | `mvr-due-date-watch` raises alerts T-7, T-0, T+7, T+14 against per-study SLA; missed-MVR streak per site raises RBM risk indicator (FS-RBM-02). |
| FS-MV-06 | URS-MV-06 | MVR templates versioned at study level; mid-study template change follows change-control with template-version pinning. |

### 4.7 SDV Sample Plan (M-SDV)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SDV-01 | URS-SDV-01 | SDV plan configuration captured per study; CtQ-tagged critical fields 100%; non-critical risk-based per CDISC controlled terminology. |
| FS-SDV-02 | URS-SDV-02 | SDV completion ingested from EDC (Marigold MAR-URS-EDC-001 RBM feed); aggregated to field / form / visit / subject / site / study granularity. |
| FS-SDV-03 | URS-SDV-03 | `sdv-exception-job` surfaces fields not yet SDV'd at lock checkpoint as RBM KPI. |

### 4.8 Risk-Based Monitoring (M-RBM)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RBM-01 | URS-RBM-01 | Vault Risk Register object per study; risks categorised per ICH E6(R3) § 3; fields: `risk_id`, `category`, `description`, `likelihood`, `impact`, `mitigation`, `owner`, `status`. |
| FS-RBM-02 | URS-RBM-02 | Site-risk indicators computed daily by `rbm-indicator-job` from CTMS + EDC + RTSM + Argus feeds; published to Vault Dashboard. |
| FS-RBM-03 | URS-RBM-03 | Threshold breaches raise Action Items via FS-ISS-02 routed to CRA + CRA Lead with mandatory mitigation plan template. |
| FS-RBM-04 | URS-RBM-04 | RBM dashboards navigable by study / country / site / indicator via Vault Report; daily-digest email to central monitoring leads. |
| FS-RBM-05 | URS-RBM-05 | Risk-register review cadence enforced ≥ every 4 weeks during enrolment via `risk-review-reminder`; review evidence captured as signed Vault record. |

### 4.9 Issue Management and CAPA (M-ISS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ISS-01 | URS-ISS-01 | Vault Issue object: `issue_id`, `source`, `severity` ∈ {LOW, MED, HIGH, CRITICAL}, `owner`, `due_date`, `status`, `evidence`. |
| FS-ISS-02 | URS-ISS-02 | Vault Action Item object linked to Issue; escalation engine per FS-MV-04 default. |
| FS-ISS-03 | URS-ISS-03 | Trial-level deviations classified CAPA-bearing create idempotent records in MasterControl via REST `/v1/capa/create` with `Idempotency-Key: {study_id}:{deviation_id}`; success / failure status returned. |
| FS-ISS-04 | URS-ISS-04 | Issue / action-item KPIs (open, overdue, mean-time-to-close) published to RBM dashboard. |

### 4.10 Drug Supply Forecast (M-DRG)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DRG-01 | URS-DRG-01 | RTSM ingest job `drug-supply-ingest` daily; per-site inventory + dispensed / returned / unused / destroyed kit counts maintained. |
| FS-DRG-02 | URS-DRG-02 | `drug-forecast-job` projects per-site shortfall risk over 4 / 8 / 12 weeks given enrolment velocity + per-subject dosing schedule. |
| FS-DRG-03 | URS-DRG-03 | Alert raised when projected coverage < 4 weeks; routed to Supply Chain + CRA as action item. |
| FS-DRG-04 | URS-DRG-04 | Drug-accountability reconciliation across CTMS, RTSM, EDC drug-acct eCRFs; unreconciled discrepancies surface as RBM indicators. |

### 4.11 Investigator Payments (M-PAY)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PAY-01 | URS-PAY-01 | Vault Payment sub-object linked to Milestones; payment schedule auto-generated from CTA terms (site init, per-subject enrol, per-visit, close-out). |
| FS-PAY-02 | URS-PAY-02 | Push to Financials via REST `/v1/payments/initiate` with `Idempotency-Key: {study_id}:{site_id}:{milestone_id}:{payment_id}`; duplicate keys rejected; no silent retry on success. |
| FS-PAY-03 | URS-PAY-03 | Overpayment guard pre-submit check against Vault Payment History; payment against fully-paid milestone blocked. |
| FS-PAY-04 | URS-PAY-04 | Payment forecast (current quarter + next 2) computed by Vault Report per study / country / site. |
| FS-PAY-05 | URS-PAY-05 | Site payment history auditable + exportable per site per study via Vault Report. |

### 4.12 Budget (M-BUD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BUD-01 | URS-BUD-01 | Vault Budget object per study with line items (sites, monitoring visits, central labs, imaging, drug supply, vendors); actuals vs budget computed monthly via `budget-actuals-job`. |
| FS-BUD-02 | URS-BUD-02 | Cost-overrun alerts (line > 110% plan) raise action items to Clinical Operations Manager. |

### 4.13 Vendor Management (M-VEN)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VEN-01 | URS-VEN-01 | Vault Vendor object: `vendor_id`, `type` ∈ {CRO, CENTRAL_LAB, IMAGING, EPRO, LIMS, OTHER}, `scope`, `contract_version`, `contract_effective_start_end`, `kpis`. |
| FS-VEN-02 | URS-VEN-02 | Vendor data-feed reconciliation status tracked daily; failure raises action item via FS-ISS-02. |
| FS-VEN-03 | URS-VEN-03 | Vendor KPI report (data-freshness, on-time-delivery, query-response time) quarterly. |
| FS-VEN-04 | URS-VEN-04 | Change Order workflow with signed amendment captured; budget impact updated in FS-BUD-01. |

### 4.14 eTMF Cross-Link (M-ETMF)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ETMF-01 | URS-ETMF-01 | Site-level documents (CV, 1572, financial disclosure, IRB approval, ICF, training, CTA, insurance, SIV report) cross-linked to Vault eTMF via Vault Connect; TMF RM v3.3.x artefact mapping enforced. |
| FS-ETMF-02 | URS-ETMF-02 | EDL check at site activation + milestone gates; EDL gaps block gated transition via Site Lifecycle gate. |
| FS-ETMF-03 | URS-ETMF-03 | Document-version sync (IB, Protocol, ICF) between CTMS + eTMF; mismatches raise action items. |
| FS-ETMF-04 | URS-ETMF-04 | Inspection-readiness score from Vault eTMF surfaced in CTMS Vault Dashboard. |

### 4.15 Safety Reporting Tracking (M-SAF)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SAF-01 | URS-SAF-01 | SAE / SUSAR metadata ingested from Argus daily: `case_id`, `subject_id`, `site_id`, `country`, `sponsor_awareness_date`, `regulatory_clock_state`; Argus is regulatory record-of-truth. |
| FS-SAF-02 | URS-SAF-02 | Clock-display: fatal/LT 7-day + 8-day follow-up; non-fatal/non-LT 15-day per ICH E2A + EU CTR Art. 42; CTMS displays state but does NOT own the clock. |
| FS-SAF-03 | URS-SAF-03 | `saf-clock-watch` raises alerts T-2 / T-1 / T-0 / T+1 to PV Lead + Director Clinical Ops; T+1 unresolved → quality event flagged for CAPA via FS-ISS-03. |
| FS-SAF-04 | URS-SAF-04 | Per-site SAE / SUSAR rate computed daily; published to RBM indicator set. |
| FS-SAF-05 | URS-SAF-05 | DSUR + ASR preparation tasks tracked per study per year as Vault Task object. |

### 4.16 Audit Trail and Part 11 (M-AUD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit trail covers all object edits, signatures, configuration changes, lifecycle-state transitions, vendor/contract changes, action-item state changes; schema: `actor_id`, `timestamp_utc`, `action`, `entity`, `old_value`, `new_value`, `reason`. |
| FS-AUD-02 | URS-AUD-02 | Append-only at platform level (Veeva-managed); export to CSV / PDF; bundle digitally signed. |
| FS-AUD-03 | URS-AUD-03 | Monthly audit-trail review by Director Clinical Operations IT; review evidence captured as signed Vault record. |
| FS-AUD-04 | URS-AUD-04 | Retention ≥ 25 years post-trial completion; per-study extension where paediatric / oncology / EU CTR Art. 58 applies. |
| FS-AUD-05 | URS-AUD-05 | `audit-trail-watchdog` heartbeat every 5 min; gap > 15 min → tenant READ_ONLY + P1 alert to vendor + sponsor SRE. |
| FS-PART11-01 | URS-PART11-01 | § 11.10(a) — SOP suite `SOP-CLINOPS-01..05`; effective at sponsor + sites; LMS gate. |
| FS-PART11-02 | URS-PART11-02 | § 11.10(b) — Object record PDFs + report exports reproducible from DB state via `record-pdf-job`; SHA-256 manifest. |
| FS-PART11-03 | URS-PART11-03 | § 11.10(c) — Retention per FS-AUD-04; vendor-hosted with backup per FS-BAK-01. |
| FS-PART11-04 | URS-PART11-04 | § 11.10(d) — Okta + MFA + role-based per FS-SEC-01..02. |
| FS-PART11-05 | URS-PART11-05 | § 11.10(e) — Audit trail per FS-AUD-01..05. |
| FS-PART11-06 | URS-PART11-06 | § 11.10(g) — Authority checks at signature / activation / payment / CTIS-submission actions; failed authority writes audit entry + denies. |
| FS-PART11-07 | URS-PART11-07 | § 11.10(k) — Vendor manuals + Dryad per-process SOPs versioned in eDMS (Vellis); LMS gates current-version training. |
| FS-PART11-08 | URS-PART11-08 | § 11.30 — CTIS gateway + national-CA submissions + Financials gateway: TLS 1.3 + mutual auth + checksum reconciliation. |
| FS-PART11-09 | URS-PART11-09 | § 11.50 — Signature manifestations: printed name + UTC timestamp + meaning string in every signature. |
| FS-PART11-10 | URS-PART11-10 | § 11.70 — Signature payload bound to record-state SHA-256 hash; post-signature change invalidates per FS-SIG semantics. |
| FS-PART11-11 | URS-PART11-11 | § 11.100 — Okta user-id uniqueness; never reassigned. |
| FS-PART11-12 | URS-PART11-12 | § 11.200 — Re-auth (password + MFA) at every signature event; cached creds disabled at signature moment. |
| FS-PART11-13 | URS-PART11-13 | § 11.300 — Okta password policy: ≥ 14 chars, history 12, age 90 d; MFA required; lockout 5 attempts. |

### 4.17 Integrations — EDC + RTSM (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-EDC-01 | URS-INT-EDC-01 | Vault Connect to Medidata Rave for enrolment / status feed daily; subject-level state aggregated. |
| FS-INT-EDC-02 | URS-INT-EDC-02 | Vault 24R3 Clinical Operations–EDC Connection: protocol-deviation records flow from Rave with `edc_id` link enabling navigation to source record; deviations surfaced in CTMS register via FS-DEV-03. |
| FS-INT-EDC-03 | URS-INT-EDC-03 | Query KPI ingest from Rave (open count, aging, % overdue) populating site-level KPIs daily. |
| FS-INT-RTSM-01 | URS-INT-RTSM-01 | RTSM randomisation-status feed daily; reconciliation queries on EDC enrolment vs RTSM randomisation mismatch. |
| FS-INT-RTSM-02 | URS-INT-RTSM-02 | Drug-accountability data feeds FS-DRG-* drug-supply tracking. |

### 4.18 Integrations — Argus (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-ARGUS-01 | URS-INT-ARGUS-01 | SUSAR / SAE metadata feed from Argus daily for operational tracking layer (FS-SAF-*); read-only metadata. |
| FS-INT-ARGUS-02 | URS-INT-ARGUS-02 | CTMS does NOT own regulatory submission clock — Argus is regulatory record-of-truth; FS-SAF-02 enforces "display-only" posture. |

### 4.19 Integrations — eQMS MasterControl (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | REST `/v1/capa/create` with `Idempotency-Key: {study_id}:{deviation_id}` per FS-ISS-03; success / failure status returned. |
| FS-INT-EQMS-02 | URS-INT-EQMS-02 | CAPA closure status fed back to CTMS via REST `/v1/capa/status`; surfaced on Issue record. |

### 4.20 Integrations — eTMF (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-ETMF-01 | URS-INT-ETMF-01 | Vault Connect cross-vault link to Vault eTMF for regulatory / ICF / site-document artefacts. |
| FS-INT-ETMF-02 | URS-INT-ETMF-02 | eTMF inspection-readiness score surfaced via Vault Connect on CTMS Dashboard. |

### 4.21 Integrations — SSO Okta (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-SSO-01 | URS-INT-SSO-01 | Okta SAML 2.0 + MFA; Vault local accounts disabled in production. |
| FS-INT-SSO-02 | URS-INT-SSO-02 | SCIM 2.0 provisioning from HR / Okta to Vault; HR-termination event deprovisions within 24 h. |

### 4.22 Integrations — Financials (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-FIN-01 | URS-INT-FIN-01 | Idempotent payment push per FS-PAY-02. |
| FS-INT-FIN-02 | URS-INT-FIN-02 | Monthly reconciliation report (CTMS-initiated vs Financials-confirmed) generated by `payment-reconcile-job`. |

### 4.23 Integrations — HR (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-HR-01 | URS-INT-HR-01 | HR event consumer ingests CRA assignment + role changes; termination events trigger CTMS access deprovisioning via SCIM ≤ 24 h. |

### 4.24 DSMB / IDMC Tracking (M-DSMB)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DSMB-01 | URS-DSMB-01 | DSMB charter version + meeting schedule + recommendation receipts tracked as Vault DSMB object; charter version drift detected by `dsmb-charter-drift-job`. |
| FS-DSMB-02 | URS-DSMB-02 | DSMB meeting outputs (continue / modify / stop) captured as signed Vault record; downstream actions auto-generated as Action Items linked to Protocol Amendment workflow. |
| FS-DSMB-03 | URS-DSMB-03 | Interim-analysis schedule per DSMB charter tracked; missed milestone raises alert. |

### 4.25 Protocol-Deviation Tracking (M-DEV)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DEV-01 | URS-DEV-01 | Vault Deviation object: `deviation_id`, `subject_id`, `site_id`, `category`, `date_occurred`, `date_identified`, `description`, `root_cause`, `corrective_action`, `importance` ∈ {IMPORTANT, NON_IMPORTANT}, `ctis_reportable` flag. |
| FS-DEV-02 | URS-DEV-02 | IPDs routed to Medical Monitor + CRA Lead review queue; CTIS-reportable flag drives inclusion in next CTIS substantial-modification or ASR via FS-CTIS-02. |
| FS-DEV-03 | URS-DEV-03 | Vault 24R3 Clinical Operations–EDC Connection feeds EDC-originated deviations; CTMS-originated deviations co-exist; `edc_id` link enables navigation to EDC source. |
| FS-DEV-04 | URS-DEV-04 | Per-site / per-study deviation rate + IPD rate published to RBM indicator set. |

### 4.26 BIMO / EMA / DACH Inspection-Readiness (M-BIMO)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BIMO-01 | URS-BIMO-01 | `bimo-bundle-job` produces site-activation evidence; investigator + delegation records; MVR history; deviation register; SAE tracking; vendor records; CTIS submission history; budget vs actuals; format PDF + CSV; SHA-256 signed. |
| FS-BIMO-02 | URS-BIMO-02 | Inspector / auditor Okta group `dryad-vault-auditor-{study}` grants read-only + export-only; no edit / no signature / no payment-submission. |
| FS-BIMO-03 | URS-BIMO-03 | 100-site multi-country study bundle generable in ≤ 60 min wall-clock. |
| FS-BIMO-04 | URS-BIMO-04 | Late safety-reporting findings (FY2024 BIMO trend) pre-empted by FS-SAF-03 alert chain. |

### 4.27 Document Tracking (M-DOC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DOC-01 | URS-DOC-01 | IB version registry: `ib_version`, `effective_date`, `irb_ec_approval[]`, `distribution_log[]`. |
| FS-DOC-02 | URS-DOC-02 | Protocol version registry (parent + amendments): `protocol_version`, `effective_date`, `ctis_submission_status`. |
| FS-DOC-03 | URS-DOC-03 | ICF version registry per site: `icf_version`, `language`, `irb_ec_approval_date`, `deployment_to_site_date`, `current_icf` flag. |
| FS-DOC-04 | URS-DOC-04 | Subjects under outdated ICF version flagged via Vault Report; cross-reference to Marigold EDC URS-CONSENT-* re-consent workflow. |

### 4.28 Site Closeout and CSR Tracking (M-CLO)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CLO-01 | URS-CLO-01 | Site Closeout gate enforced: COV MVR signed + all queries closed + SDV complete + drug-supply reconciled + site-payment final + site-document EDL gate. |
| FS-CLO-02 | URS-CLO-02 | CSR tracking object: `csr_version`, `statistical_analysis_status`, `signature_schedule`, `ctis_distribution`. |
| FS-CLO-03 | URS-CLO-03 | End-of-Trial CTIS notification per EU CTR Art. 37 tracked as workflow item. |

### 4.29 Multi-Language and Time-Zone (M-INTL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INTL-01 | URS-INTL-01 | Vault i18n labels for site-facing communications + EDL / ICF; supported: de-DE, de-AT, de-CH, fr-FR, en-GB, en-US, es-ES, it-IT, pl-PL, cs-CZ. |
| FS-INTL-02 | URS-INTL-02 | Visit-window + payment-due-date calculation TZ-aware; storage UTC. |
| FS-INTL-03 | URS-INTL-03 | Locale-specific date / number / currency display via UI formatter; canonical values unchanged. |

### 4.30 Performance / Availability / Backup (M-PERF)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | P95 object open / list ≤ 3 s under 300 concurrent users. |
| FS-PERF-02 | URS-PERF-02 | Site-list export for 100-site study ≤ 10 min wall-clock. |
| FS-AV-01 | URS-AV-01 | Veeva SLA 99.5% monthly tracked via Veeva Trust portal; deviations escalated. |
| FS-BAK-01 | URS-BAK-01 | Vendor-managed backup; RPO ≤ 4 h, RTO ≤ 24 h verified annually. |
| FS-BAK-02 | URS-BAK-02 | DR drill annual, vendor-evidenced; sponsor reviews. |

### 4.31 Security and Data Protection (M-SEC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SEC-01 | URS-SEC-01 | Okta SAML 2.0 + MFA; session timeout ≤ 30 min idle; FS-PART11-12 re-auth at signature. |
| FS-SEC-02 | URS-SEC-02 | Per-study + per-country scopes; access reviewed FPI / every 90 d / site closeout. |
| FS-SEC-03 | URS-SEC-03 | Investigator contact data encrypted at rest (AES-256) + in transit (TLS 1.3) per GDPR Art. 32. |
| FS-SEC-04 | URS-SEC-04 | GDPR Art. 22 — automated decision-making against the data subject blocked at policy level; algorithmic outputs are advisory to human reviewers; audit-trail entry per algorithmic decision. |
| FS-SEC-05 | URS-SEC-05 | Per-study DPIA template (Confluence + signed PDF in eTMF) executed before FPI for studies handling investigator / staff / vendor personal data. |
| FS-SEC-06 | URS-SEC-06 | GDPR Art. 17 erasure requests triaged against EU CTR + ICH E6(R3) retention obligations; decision filed in eTMF. |

### 4.32 Training and Periodic Review (M-TRN)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | LMS gate: production access blocked unless role + protocol training current; expiry-warning T-30 d; auto-block T+0. |
| FS-PR-01 | URS-PR-01 | Annual platform-level periodic review per `SOP-CLINOPS-05`; per-study at amendments + lock; signed by Director Clinical Ops IT + Head of QA. |
| FS-PR-02 | URS-PR-02 | Periodic review confirms: audit-trail completeness; vendor-release impact assessments current; integration health (EDC / RTSM / Argus / eQMS / eTMF / Financials feeds); SAE clock-tracking health. |

### 4.33 CTIS Submission Tracking (M-CTIS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CTIS-01 | URS-CTIS-01 | CTIS submission lifecycle tracked per study: `initial`, `substantial_modifications[]`, `asr[]`, `end_of_trial`, `summary_of_results`; status DRAFT → SUBMITTED → CA_DECISION → PUBLISHED. |
| FS-CTIS-02 | URS-CTIS-02 | Sponsor-obligation alerts: ASR (annual), SM (per Member-State assessment cadence), EoT (per EU CTR Art. 37), summary-of-results (per EU CTR Art. 37 timelines). |
| FS-CTIS-03 | URS-CTIS-03 | National-CA submission tracking for DE (BfArM / PEI), AT (AGES), CH (Swissmedic) where national obligations remain. |
| FS-CTIS-04 | URS-CTIS-04 | CTIS resubmission status flag: from 1 January 2026 no invoice for CTR safety / ethics assessment for technical-issue resubmissions where content unchanged; captured for evidence. |

### 4.34 Monitoring-Plan Version Control (M-MP)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MP-01 | URS-MP-01 | Vault Monitoring Plan object: `mp_version`, `effective_date`, `approver`, `amendment_linkage`; version-history retained; mid-study amendment may trigger update. |
| FS-MP-02 | URS-MP-02 | Active MP version drives FS-MV-01 MV cadence + FS-SDV-01 SDV strategy via plan-resolution lookup at MV creation / SDV-plan-bind time. |

### 4.35 IMP Import / Drug Compliance (M-IMP)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-IMP-01 | URS-IMP-01 | Per-country IMP licence + customs-documentation registry; expiry watcher raises alerts T-90 / T-60 / T-30 days; action item routed to Regulatory Affairs. |
| FS-IMP-02 | URS-IMP-02 | Country-specific labelling / leaflet versions tracked with version + effective dates; DE / AT / CH language-variant register. |

### 4.36 Study Startup KPIs (M-SS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SS-01 | URS-SS-01 | KPI computation: Time-to-CA-Submission, Time-to-First-Approval, Time-to-First-Site-Activation, Time-to-FPI per study + per country; benchmarked against historical + industry benchmark via `startup-kpi-job`. |
| FS-SS-02 | URS-SS-02 | FPI event per country + per study tracked; FPI date + site + subject screening / randomisation indicator captured; CTIS notification trigger via FS-CTIS-01. |

### 4.37 Sponsor Audit / Quality-Event Tracking (M-AUDIT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUDIT-01 | URS-AUDIT-01 | Vault Audit object: `audit_id`, `scope`, `auditor_id`, `date`, `findings[]`, `capas[]` (each linked to MasterControl via FS-ISS-03 idempotent path). |
| FS-AUDIT-02 | URS-AUDIT-02 | Findings categorised by severity {LOW, MED, HIGH, CRITICAL}; CRITICAL raises immediate Action Item routed to study-level QA. |

---


### 4.38 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: SAML 2.0 via Entra ID with SCIM lifecycle provisioning. Conditional-access binding to policy `Clinical-Sensitive Conditional Access (FIDO2 phishing-resistant MFA + sponsor-tenant isolation)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with Oracle RMAN for the CTMS Oracle backend; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.39 Cross-System Integration — Helios handover (M-XINT-HEL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HEL-01 | URS-XINT-HEL-01 | Audit-event publisher emits Kafka topic `helios.ingest.dryad.ctms.v1` with schema-registry-pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`; at-least-once delivery; idempotency key `{source_system, event_id}`; back-pressure surfaced via Prometheus `helios_publish_lag_seconds` with 5-min alert at > 600 s. |
| FS-XINT-HEL-02 | URS-XINT-HEL-02 | Local audit-store retention policy enforces ≥ 25 y; Helios ack persisted as `helios_ack_ts` per event; periodic reconciliation job verifies parity (Helios row count == local published count) and raises a deviation in MasterControl on > 0.01% mismatch over a 24 h window. |


### 4.40 Cross-System Integration — LMS handover (M-XINT-LMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-LMS-01 | URS-XINT-LMS-01 | LMS-competence adapter `<sys>-LMS-CLIENT-1.x` performs `GET /lms/competence/{user_id}?curriculum=...` over mTLS + Entra workload-identity; cache TTL per system (12-24 h); on `current=false` the consumer blocks the gated action and records `lms_lapse_user={user_id}` in the consumer audit trail; periodic reconciliation job verifies that no gated action proceeded with a lapsed competence. |

## 5. Configuration Items (CI)

| CI ID | Item | Value | Source |
|---|---|---|---|
| CI-01 | IdP | Okta SAML 2.0 + MFA | URS-INT-SSO-01 |
| CI-02 | SCIM provisioning | Okta → Vault | URS-INT-SSO-02 |
| CI-03 | Audit-trail watchdog | heartbeat 5 min; gap > 15 min → READ_ONLY | URS-AUD-05 |
| CI-04 | Retention | 25 y minimum | URS-AUD-04 |
| CI-05 | Site activation checklist | 1572/CV/financial-disclosure/IRB-approval/ICF/training/CTA/insurance/SIV | URS-SITE-02 |
| CI-06 | Site lifecycle states | IDENTIFIED, QUALIFIED, INITIATED, ENROLLING, ENROLLMENT_CLOSED, FOLLOW_UP, CLOSED | URS-SITE-01 |
| CI-07 | MVR types | SIV, IMV, MMV, COV, REMOTE_MV | URS-MV-01 |
| CI-08 | MVR escalation | T+0 owner / T+7 CRA Lead / T+14 Clinical Ops Mgr | URS-MV-04 |
| CI-09 | MasterControl REST | `/v1/capa/create` idempotency key `{study_id}:{deviation_id}` | URS-INT-EQMS-01 |
| CI-10 | Financials REST | `/v1/payments/initiate` idempotency key `{study_id}:{site_id}:{milestone_id}:{payment_id}` | URS-INT-FIN-01 |
| CI-11 | RBM dashboard | navigable by study/country/site/indicator; daily digest | URS-RBM-04 |
| CI-12 | RBM review cadence | ≥ every 4 weeks during enrolment | URS-RBM-05 |
| CI-13 | Drug-supply forecast horizon | 4 / 8 / 12 weeks | URS-DRG-02 |
| CI-14 | EDC-CTMS connection | Vault 24R3 Clinical Operations–EDC Connection | URS-INT-EDC-02 |
| CI-15 | DSMB tracking | Charter version + meetings + recommendations | URS-DSMB-01..02 |
| CI-16 | CTIS lifecycle | initial / SM / ASR / EoT / SoR | URS-CTIS-01 |
| CI-17 | National-CA gateways | BfArM, PEI, AGES, Swissmedic | URS-CTIS-03 |
| CI-18 | Languages | de-DE, de-AT, de-CH, fr-FR, en-GB, en-US, es-ES, it-IT, pl-PL, cs-CZ | URS-INTL-01 |
| CI-19 | Inspector role | read-only + export-only | URS-BIMO-02 |
| CI-20 | Auditor BIMO bundle target | ≤ 60 min wall-clock for 100-site study | URS-BIMO-03 |
| CI-21 | SAE alert chain | T-2/T-1/T-0/T+1 | URS-SAF-03 |
| CI-22 | Vendor release evaluation | ≤ 14 days | URS-VND-02 |
| CI-23 | Periodic review cadence | annual platform + per-study at amendments + lock | URS-PR-01 |
| CI-24 | DPIA per study | required before FPI | URS-SEC-05 |
| CI-25 | Art. 22 block | algorithmic outputs advisory only | URS-SEC-04 |

## 6. Risks

- Mid-study amendment misconfig (mitigation: FS-PROT-04 downstream-task generator + FS-AMD chain into Marigold EDC).
- Stale site-credential data (mitigation: FS-INV-04 training-check at activation + periodic review).
- Duplicate payment via integration retry (mitigation: FS-PAY-02 idempotency + FS-PAY-03 overpayment guard).
- Audit-trail disablement (mitigation: FS-AUD-05 watchdog + READ_ONLY tenant enforcement).
- MVR due-date miss (mitigation: FS-MV-05 alert chain + FS-RBM-02 missed-MVR streak indicator).
- SAE → SUSAR clock miss (mitigation: FS-SAF-03 alert chain T-2/T-1/T-0/T+1 + FS-BIMO-04 pre-emption).
- 1572 expiry / new-sub-I addition not reflected (mitigation: FS-INV-02 re-sign triggers per 21 CFR § 312.53(c)).
- Drug-supply shortfall (mitigation: FS-DRG-02 forecast + FS-DRG-03 alert).
- Vendor CRO data-feed silent failure (mitigation: FS-VEN-02 daily reconciliation status + action-item raise).
- DSMB charter version drift (mitigation: FS-DSMB-01 drift-job).
- CTIS sponsor-obligation deadline miss (mitigation: FS-CTIS-02 alerts).
- GDPR Art. 22 violation (mitigation: FS-SEC-04 algorithmic-output advisory-only policy + audit-trail entry).
- Site closeout gated incorrectly (mitigation: FS-CLO-01 multi-gate + FS-ETMF-02 EDL gate).
- PI turnover propagation gap (mitigation: FS-INV-05 PI-transition workflow).

## 7. References

- DRY-URS-CTMS-001 v1.2 (parent URS).
- 21 CFR Part 11 §§ .10(a)–(k), .30, .50, .70, .100, .200, .300.
- 21 CFR Part 312 (Form FDA 1572 per § 312.53(c)); 21 CFR Part 314; 21 CFR Parts 50 + 56.
- ICH E6(R3) GCP (Step 4, adopted 6 January 2025); ICH E8(R1); ICH E9(R1); ICH E2A; ICH E2B(R3); ICH M11.
- EU CTR Reg. 536/2014 + CTIS Sponsor Handbook (current); EU CTR Arts. 16, 37, 42, 58.
- EU GMP Annex 11 §§ 4, 6, 9, 11; EMA Q&A on Annex 11.
- GDPR Reg. (EU) 2016/679 — Arts. 6, 17, 22, 32, 33, 35.
- FDA *Computerized Systems Used in Clinical Investigations* (May 2007).
- FDA *Establishment and Operation of Clinical Trial Data Monitoring Committees* (current + 2024 draft).
- FDA BIMO Inspection Manual 7348.809 (updated 4 April 2025).
- FDA *Conducting Remote Regulatory Assessments — Q&A* (June 2025 final).
- ISPE GAMP 5 (2nd ed., 2022); GAMP GPG *Computerised Systems in Regulated GCP*.
- PIC/S PI 041; ISO/IEC 27001:2022; ISO 14155:2020 (where device arms).
- TMF Reference Model v3.3.x.
- Veeva — *Vault CTMS 24R3 / 25R1 Release Notes*; Vault CTMS Product Brief; Clinical Operations–EDC Connection.
- Veeva — Vault eTMF Product Brief.
- Medidata Rave EDC (Marigold MAR-URS-EDC-001 / MAR-FS-EDC-001 cross-reference).
- Oracle Argus 8.4 (Sirius PV cross-reference).
- BfArM; Paul-Ehrlich-Institut (PEI); Swissmedic; AGES PharmMed.

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID(s) | Notes |
|---|---|---|
| URS-VND-01 | FS-VND-01 | Vendor evidence register |
| URS-VND-02 | FS-VND-02 | Release evaluation runbook |
| URS-VND-03 | FS-VND-03 | Sub-processor inventory |
| URS-VND-04 | FS-VND-04 | Incident notification |
| URS-PROT-01 | FS-PROT-01 | Vault Protocol object |
| URS-PROT-02 | FS-PROT-02 | Vault Amendment object |
| URS-PROT-03 | FS-PROT-03 | Substantial modification → CTIS |
| URS-PROT-04 | FS-PROT-04 | Amendment downstream-task generator |
| URS-CTRY-01 | FS-CTRY-01 | Vault Country object |
| URS-CTRY-02 | FS-CTRY-02 | Country-level milestone gating |
| URS-SITE-01 | FS-SITE-01 | Vault Site lifecycle |
| URS-SITE-02 | FS-SITE-02 | Activation checklist |
| URS-SITE-03 | FS-SITE-03 | CRA Lead activation signature |
| URS-SITE-04 | FS-SITE-04 | State-transition e-sign |
| URS-SITE-05 | FS-SITE-05 | Site Contacts (encrypted) |
| URS-SITE-06 | FS-SITE-06 | Site enrolment plan vs actual |
| URS-INV-01 | FS-INV-01 | Vault Investigator object |
| URS-INV-02 | FS-INV-02 | 1572 tracking |
| URS-INV-03 | FS-INV-03 | Delegation Log |
| URS-INV-04 | FS-INV-04 | Training currency at activation |
| URS-INV-05 | FS-INV-05 | PI-transition workflow |
| URS-REC-01 | FS-REC-01 | Enrolment plan + actuals |
| URS-REC-02 | FS-REC-02 | Forecast job |
| URS-REC-03 | FS-REC-03 | Recruitment KPIs |
| URS-REC-04 | FS-REC-04 | Exception alerts |
| URS-MV-01 | FS-MV-01 | MV plan + types |
| URS-MV-02 | FS-MV-02 | MVR schema |
| URS-MV-03 | FS-MV-03 | MVR approval / unlock |
| URS-MV-04 | FS-MV-04 | Action items + escalation |
| URS-MV-05 | FS-MV-05 | Due-date watchdog |
| URS-MV-06 | FS-MV-06 | MVR templates |
| URS-SDV-01 | FS-SDV-01 | SDV plan configuration |
| URS-SDV-02 | FS-SDV-02 | SDV completion ingest |
| URS-SDV-03 | FS-SDV-03 | SDV exception KPI |
| URS-RBM-01 | FS-RBM-01 | Risk Register |
| URS-RBM-02 | FS-RBM-02 | Site-risk indicators |
| URS-RBM-03 | FS-RBM-03 | Threshold breach → action items |
| URS-RBM-04 | FS-RBM-04 | RBM dashboards + digest |
| URS-RBM-05 | FS-RBM-05 | Risk-register review cadence |
| URS-ISS-01 | FS-ISS-01 | Issue object |
| URS-ISS-02 | FS-ISS-02 | Action Item + escalation |
| URS-ISS-03 | FS-ISS-03 | MasterControl CAPA idempotent |
| URS-ISS-04 | FS-ISS-04 | Issue / AI KPIs |
| URS-DRG-01 | FS-DRG-01 | RTSM ingest |
| URS-DRG-02 | FS-DRG-02 | Forecast |
| URS-DRG-03 | FS-DRG-03 | Coverage alert |
| URS-DRG-04 | FS-DRG-04 | Drug-acct reconciliation |
| URS-PAY-01 | FS-PAY-01 | Milestone-based payment schedule |
| URS-PAY-02 | FS-PAY-02 | Financials idempotency |
| URS-PAY-03 | FS-PAY-03 | Overpayment guard |
| URS-PAY-04 | FS-PAY-04 | Payment forecast |
| URS-PAY-05 | FS-PAY-05 | Payment history export |
| URS-BUD-01 | FS-BUD-01 | Vault Budget + actuals |
| URS-BUD-02 | FS-BUD-02 | Cost-overrun alerts |
| URS-VEN-01 | FS-VEN-01 | Vendor object |
| URS-VEN-02 | FS-VEN-02 | Vendor feed reconciliation |
| URS-VEN-03 | FS-VEN-03 | Vendor KPIs |
| URS-VEN-04 | FS-VEN-04 | Change Order |
| URS-ETMF-01 | FS-ETMF-01 | Site-doc cross-link |
| URS-ETMF-02 | FS-ETMF-02 | EDL gate |
| URS-ETMF-03 | FS-ETMF-03 | IB / Protocol / ICF version sync |
| URS-ETMF-04 | FS-ETMF-04 | Inspection-readiness score surface |
| URS-SAF-01 | FS-SAF-01 | SAE / SUSAR metadata ingest |
| URS-SAF-02 | FS-SAF-02 | Clock display (not owner) |
| URS-SAF-03 | FS-SAF-03 | Missed-deadline alerts |
| URS-SAF-04 | FS-SAF-04 | Per-site SAE rate KPI |
| URS-SAF-05 | FS-SAF-05 | DSUR / ASR tasks |
| URS-AUD-01 | FS-AUD-01 | Audit-trail schema |
| URS-AUD-02 | FS-AUD-02 | Append-only export |
| URS-AUD-03 | FS-AUD-03 | Monthly review |
| URS-AUD-04 | FS-AUD-04 | Retention 25y |
| URS-AUD-05 | FS-AUD-05 | Audit-trail watchdog |
| URS-PART11-01 | FS-PART11-01 | § 11.10(a) SOPs |
| URS-PART11-02 | FS-PART11-02 | § 11.10(b) reproducible copies |
| URS-PART11-03 | FS-PART11-03 | § 11.10(c) retention |
| URS-PART11-04 | FS-PART11-04 | § 11.10(d) access |
| URS-PART11-05 | FS-PART11-05 | § 11.10(e) audit trail |
| URS-PART11-06 | FS-PART11-06 | § 11.10(g) authority checks |
| URS-PART11-07 | FS-PART11-07 | § 11.10(k) manuals + change ctrl |
| URS-PART11-08 | FS-PART11-08 | § 11.30 open-system bridges |
| URS-PART11-09 | FS-PART11-09 | § 11.50 manifestations |
| URS-PART11-10 | FS-PART11-10 | § 11.70 binding |
| URS-PART11-11 | FS-PART11-11 | § 11.100 uniqueness |
| URS-PART11-12 | FS-PART11-12 | § 11.200 re-auth |
| URS-PART11-13 | FS-PART11-13 | § 11.300 password |
| URS-INT-EDC-01 | FS-INT-EDC-01 | EDC enrolment feed |
| URS-INT-EDC-02 | FS-INT-EDC-02 | EDC-CTMS deviation Connection |
| URS-INT-EDC-03 | FS-INT-EDC-03 | EDC query KPI ingest |
| URS-INT-RTSM-01 | FS-INT-RTSM-01 | RTSM randomisation feed |
| URS-INT-RTSM-02 | FS-INT-RTSM-02 | Drug acct via RTSM |
| URS-INT-ARGUS-01 | FS-INT-ARGUS-01 | Argus PV metadata |
| URS-INT-ARGUS-02 | FS-INT-ARGUS-02 | Argus is clock owner |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 | MasterControl CAPA REST |
| URS-INT-EQMS-02 | FS-INT-EQMS-02 | CAPA closure feedback |
| URS-INT-ETMF-01 | FS-INT-ETMF-01 | Vault Connect to eTMF |
| URS-INT-ETMF-02 | FS-INT-ETMF-02 | eTMF readiness surface |
| URS-INT-SSO-01 | FS-INT-SSO-01 | Okta SAML + MFA |
| URS-INT-SSO-02 | FS-INT-SSO-02 | SCIM provisioning |
| URS-INT-FIN-01 | FS-INT-FIN-01 | Financials idempotent push |
| URS-INT-FIN-02 | FS-INT-FIN-02 | Monthly reconciliation |
| URS-INT-HR-01 | FS-INT-HR-01 | HR sync + termination |
| URS-DSMB-01 | FS-DSMB-01 | DSMB charter tracking + drift |
| URS-DSMB-02 | FS-DSMB-02 | DSMB meeting outputs |
| URS-DSMB-03 | FS-DSMB-03 | Interim-analysis schedule |
| URS-DEV-01 | FS-DEV-01 | Deviation object |
| URS-DEV-02 | FS-DEV-02 | IPD flag + CTIS route |
| URS-DEV-03 | FS-DEV-03 | Vault 24R3 EDC connection feed |
| URS-DEV-04 | FS-DEV-04 | Deviation KPI |
| URS-BIMO-01 | FS-BIMO-01 | BIMO bundle job |
| URS-BIMO-02 | FS-BIMO-02 | Inspector role |
| URS-BIMO-03 | FS-BIMO-03 | Bundle perf target |
| URS-BIMO-04 | FS-BIMO-04 | Late-safety-reporting pre-emption |
| URS-DOC-01 | FS-DOC-01 | IB version registry |
| URS-DOC-02 | FS-DOC-02 | Protocol version registry |
| URS-DOC-03 | FS-DOC-03 | ICF version registry |
| URS-DOC-04 | FS-DOC-04 | Outdated-ICF flag |
| URS-CLO-01 | FS-CLO-01 | Site closeout gates |
| URS-CLO-02 | FS-CLO-02 | CSR tracking |
| URS-CLO-03 | FS-CLO-03 | EoT CTIS notification |
| URS-INTL-01 | FS-INTL-01 | i18n labels |
| URS-INTL-02 | FS-INTL-02 | TZ-aware calc |
| URS-INTL-03 | FS-INTL-03 | Locale formatting |
| URS-PERF-01 | FS-PERF-01 | P95 object access |
| URS-PERF-02 | FS-PERF-02 | Site-list export perf |
| URS-AV-01 | FS-AV-01 | Veeva SLA |
| URS-BAK-01 | FS-BAK-01 | Backup RPO/RTO |
| URS-BAK-02 | FS-BAK-02 | DR drill annual |
| URS-SEC-01 | FS-SEC-01 | Okta + MFA + timeout |
| URS-SEC-02 | FS-SEC-02 | Access review |
| URS-SEC-03 | FS-SEC-03 | GDPR Art. 32 crypto |
| URS-SEC-04 | FS-SEC-04 | GDPR Art. 22 block |
| URS-SEC-05 | FS-SEC-05 | DPIA per study |
| URS-SEC-06 | FS-SEC-06 | GDPR Art. 17 triage |
| URS-TRN-01 | FS-TRN-01 | LMS gate |
| URS-PR-01 | FS-PR-01 | Annual + per-study PR |
| URS-PR-02 | FS-PR-02 | PR extended scope |
| URS-CTIS-01 | FS-CTIS-01 | CTIS submission lifecycle |
| URS-CTIS-02 | FS-CTIS-02 | Sponsor-obligation alerts |
| URS-CTIS-03 | FS-CTIS-03 | National-CA tracking |
| URS-CTIS-04 | FS-CTIS-04 | CTIS resubmission flag |
| URS-MP-01 | FS-MP-01 | Monitoring-plan version control |
| URS-MP-02 | FS-MP-02 | MP drives MV + SDV |
| URS-IMP-01 | FS-IMP-01 | IMP licence expiry tracking |
| URS-IMP-02 | FS-IMP-02 | Country labelling variants |
| URS-SS-01 | FS-SS-01 | Study-startup KPIs |
| URS-SS-02 | FS-SS-02 | FPI event tracking |
| URS-AUDIT-01 | FS-AUDIT-01 | Sponsor audit register |
| URS-AUDIT-02 | FS-AUDIT-02 | Audit-severity escalation |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-HEL-01 | FS-XINT-HEL-01 |
| URS-XINT-HEL-02 | FS-XINT-HEL-02 |
| URS-XINT-LMS-01 | FS-XINT-LMS-01 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

The following risks are noted for downstream evaluation in the Risk Assessment.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Premature site activation without IRB / EC readiness | Medium | High | URS-SITE-02..03 |
| R-02 | Monitor-visit-report due-date miss undetected | Medium | Medium | URS-MV-05 |
| R-03 | SAE → SUSAR clock miss (15-day / 7-day) | Low | High | URS-SAF-02..03 |
| R-04 | Investigator 1572 expiry / protocol-amendment-IRB-tracking missed | Medium | High | URS-INV-02 + URS-PROT-03 |
| R-05 | Drug-supply forecast under-estimate → site stock-out | Medium | High | URS-DRG-02..03 |
| R-06 | Vendor data-feed (CRO) reconciliation failure unnoticed | Medium | High | URS-VEN-02 + URS-INT-EDC-* |
| R-07 | Investigator-payment overpayment (duplicate push) | Low | Medium | URS-PAY-02..03 + URS-INT-FIN-01 |
| R-08 | DSMB charter version drift between sites | Low | High | URS-DSMB-01 |
| R-09 | Incorrect KPI computation driving wrong RBM decision | Medium | High | URS-RBM-02..05 |
| R-10 | Audit-trail tampering on vendor side / disablement | Low | High | URS-AUD-02 + URS-AUD-05 |
| R-11 | Protocol-amendment → re-consent → EDC re-build chain breakage | Medium | High | URS-PROT-04 + URS-DEV-* |
| R-12 | CTIS sponsor-obligation deadline missed (ASR / end-of-trial / summary of results) | Medium | High | URS-CTIS-02 |
| R-13 | GDPR Art. 22 violation via auto-classification of investigators | Low | High | URS-SEC-04 |
| R-14 | BIMO inspection finding on late safety reporting (FY2024 trend) | Medium | High | URS-BIMO-04 + URS-SAF-03 |
| R-15 | Site closeout gated incorrectly (missing EDL gate) | Low | Medium | URS-CLO-01 + URS-ETMF-02 |
| R-16 | Investigator turnover mid-study not propagated to 1572 / delegation log | Medium | High | URS-INV-05 + URS-INV-03 |

Full evaluation in `DRY-RA-CTMS-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
