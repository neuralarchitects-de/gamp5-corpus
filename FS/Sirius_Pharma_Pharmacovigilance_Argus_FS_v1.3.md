---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-26; expanded 2026-05-12 (FS catch-up to v1.2 URS)"
seed_corpus_basis:
  - "SIR-URS-PV-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd ed.) Cat 4 conventions for safety / pharmacovigilance platforms"
  - "21 CFR Part 11; EU GMP Annex 11; ICH E2A/E2B(R3)/E2C(R2)/E2D; ICH M1/M2"
  - "EU GVP Modules I–XVI; EMA EudraVigilance specifications"
  - "IDMP ISO 11238/11239/11240/11615/11616 + EMA SPOR"
parent_urs:
  document_number: SIR-URS-PV-001
  version: 1.2
  file: ../../URS/_generated/final/Pharmacovigilance_Safety_Database__Sirius_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Pharmacovigilance Safety Database — Oracle Argus Safety 8.4.1

**Document Number:** SIR-FS-PV-001
**Version:** 1.2
**Effective Date:** 2026-05-12 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Parent URS:** SIR-URS-PV-001 v1.2
**Site:** Sirius Pharma Ltd., Global Pharmacovigilance Operations, Dublin (HQ) with regional hubs in Basel (CH), München (DE), Wien (AT) *(fictional)*
**System Owner:** Head of Pharmacovigilance Operations
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (no site-authored custom code)
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR 314.80, 600.80, 312.32; EU GMP Annex 11 §§ 4, 6, 9, 11; ICH E2A/E2B(R3)/E2C(R2)/E2D/E2E/E2F/M1/M2; EU GVP Modules I–XVI; EU CTR Reg. 536/2014; IDMP ISO 11238/11239/11240/11615/11616; BfArM (DE); Paul-Ehrlich-Institut (DE); Swissmedic (CH); AGES PharmMed (AT).

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of PV Operations) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (QPPV) | _____________ | _____________ | _____ |
| Reviewer (Signal Management Lead) | _____________ | _____________ | _____ |
| Reviewer (Aggregate Reporting Lead) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs — IDMP / xEVMPD) | _____________ | _____________ | _____ |
| Approver (VP Drug Safety) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue, derived from SIR-URS-PV-001 v1.0. |
| 1.2 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.2: per-ID expansion for §§ 5.1–5.19 of the URS (MedDRA lifecycle, signal mgmt EBGM/PRR/ROR, RMP/REMS, PIP, IDMP/xEVMPD, literature, partner-exchange, Part 11 sub-section-explicit, DACH CA gateways, DSUR / CTIS); Argus Interchange profile per agency documented; no range-compression per METHODOLOGY § 2A.7. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## Definitions

Inherited from SIR-URS-PV-001 v1.2. Additional FS-specific terms:

| Term | Definition |
|---|---|
| FS | Functional Specification (this document) |
| Argus Mart | Argus reporting / analytics datamart |
| Argus Interchange | Argus E2B(R3) gateway component |
| RPD | Argus reporting rule definition |
| Profile | Per-agency E2B(R3) implementation profile (EudraVigilance / FAERS / PMDA / CESG / national CA) |
| ESG | FDA Electronic Submissions Gateway |
| CESG | Health Canada Common Electronic Submissions Gateway |
| OCI | Oracle Cloud Infrastructure |
| OAS | Oracle Argus Safety |
| Empirica | Oracle Empirica Signal (Argus-integrated signal-detection platform) |

---

## 1. Purpose

This FS specifies how Oracle Argus Safety 8.4.1 + Oracle 19c + Argus Mart + Argus Interchange + Oracle Empirica Signal are deployed, configured, and integrated to satisfy `SIR-URS-PV-001` v1.2. It is the controlling input to `SIR-CS-PV-001`, `SIR-RA-PV-001`, IQ / OQ / PQ Protocols, and `SIR-RTM-PV-001`.

## 2. Scope

Per SIR-URS-PV-001 §2: Argus Safety 8.4.1 application servers + Oracle 19c on OCI + Argus Mart + Argus Interchange + Empirica Signal + MedDRA + WHO Drug + IDMP/xEVMPD product-master integration; SSO via Okta SAML 2.0 + MFA; integrations with EudraVigilance, FAERS, PMDA, Health Canada CESG, BfArM, Paul-Ehrlich-Institut, Swissmedic, AGES, Medidata Rave EDC, Veeva Vault CTMS, Veeva Vault eTMF, EMA SPOR, literature-surveillance service, partner-exchange platform.

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source / Vendor | Notes |
|---|---|---|---|---|---|
| C-01 | Argus App Servers (×4) | COTS app | 4 | Oracle | 3 active + 1 hot standby; load-balanced behind Oracle Traffic Director |
| C-02 | Oracle 19c EE | COTS infra | (infra) | Oracle | OCI; Data Guard physical-standby (async) |
| C-03 | Argus Mart | COTS app | 4 | Oracle | reporting / analytics datamart; GoldenGate fed |
| C-04 | Argus Interchange | COTS app | 4 | Oracle | E2B(R3) gateway |
| C-05 | Empirica Signal | COTS app | 4 | Oracle | EBGM / PRR / ROR signal-detection |
| C-06 | MedDRA | dictionary | n/a | MSSO | semi-annual versioned |
| C-07 | WHO Drug | dictionary | n/a | UMC | annual versioned |
| C-08 | Okta tenant | COTS SaaS | (infra) | Okta | site IdP, SAML 2.0 + MFA |
| C-09 | Medidata Rave EDC | COTS SaaS | 4 | Medidata | SAE / SUSAR reconciliation counterparty |
| C-10 | Veeva Vault CTMS | COTS SaaS | 4 | Veeva | trial-product master |
| C-11 | Veeva Vault eTMF | COTS SaaS | 4 | Veeva | TMF Reference Model |
| C-12 | EMA SPOR | external | n/a | EMA | IDMP authoritative reference |
| C-13 | Literature service | COTS SaaS | 4 | (Embase / PubMed vendor) | weekly surveillance feed |
| C-14 | Partner-exchange platform | COTS SaaS | 4 | (vendor) | E2B(R3) exchange with license partners |

### 3.2 Logical Architecture (textual)

```
                  ┌────────────────────────────────────────────────────┐
                  │     Okta IdP (SAML 2.0 + MFA)                      │
                  └────────────────────┬───────────────────────────────┘
                                       │
   ┌───────────────────────────────────▼───────────────────────────────┐
   │                Argus Safety 8.4.1 (Sirius Pharma)                  │
   │  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐    │
   │  │ App Servers     │  │ Oracle 19c +    │  │ Argus Mart      │    │
   │  │ (3 act + 1)     │◄─┤ Data Guard (DR) │◄─┤ (analytics)     │    │
   │  └─────────────────┘  └─────────────────┘  └─────────────────┘    │
   │  ┌─────────────────────────────────────────────────────────────┐  │
   │  │  Argus Interchange  (E2B(R3) profile per agency)            │  │
   │  └─────────────────────────────────────────────────────────────┘  │
   │  ┌─────────────────────────────────────────────────────────────┐  │
   │  │  Empirica Signal  (EBGM / PRR / ROR + EVDAS integration)    │  │
   │  └─────────────────────────────────────────────────────────────┘  │
   └─┬────────┬────────┬─────────┬─────────┬─────────┬─────────┬───────┘
     ▼        ▼        ▼         ▼         ▼         ▼         ▼
  EudraVig  FAERS   PMDA      Health    BfArM     PEI     Swissmedic / AGES
  (EMA)     (FDA)   Gateway   Canada    (DE)      (DE)    (CH / AT)
                              CESG      meds     biologicals
     ▲        ▲        ▲
     │        │        │
   Medidata  Vault     Vault          EMA      Lit         Partner
   Rave EDC  CTMS      eTMF           SPOR     service     exchange
```

### 3.3 Functional Modules

| Module | URS sections |
|---|---|
| M-PLAT | URS-PLAT-*, URS-VND-*, URS-CFG-* |
| M-CASE | URS-CASE-* |
| M-CODE | URS-CODE-* (MedDRA + WHO Drug lifecycle) |
| M-ASSESS | URS-ASSESS-* |
| M-SUB | URS-SUB-* (E2B(R3) + gateway) |
| M-AGG | URS-AGG-* (PSUR / PBRER / PADER / DSUR) |
| M-SIG | URS-SIG-* (EBGM / PRR / ROR + EVDAS) |
| M-RMP | URS-RMP-* (RMP + REMS) |
| M-PIP | URS-PIP-* |
| M-IDMP | URS-IDMP-* (xEVMPD + SPOR) |
| M-LIT | URS-LIT-* |
| M-PEX | URS-PEX-* |
| M-AUD | URS-AUD-* |
| M-PART11 | URS-PART11-*, URS-GVP-* |
| M-NCA | URS-NCA-* (DACH gateways) |
| M-CT | URS-CT-SAFETY-* (DSUR + CTIS) |
| M-DI | URS-DI-* |
| M-SEC | URS-SEC-* |
| M-PERF | URS-PERF-*, URS-AV-*, URS-BAK-* |
| M-TRN | URS-TRN-* |
| M-PR | URS-PR-* |

---

## 4. Functional Specifications

### 4.1 Platform, Vendor, Configuration Lifecycle (M-PLAT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | 3 active Argus App Servers behind Oracle Traffic Director (`otd-pv-prod-01`); 1 hot standby promoted via health-check failure; Oracle 19c EE 19.20+ with Data Guard physical-standby on OCI Frankfurt + OCI Zurich. |
| FS-PLAT-02 | URS-PLAT-02 | DR replica in OCI Zurich (secondary region); async Data Guard with apply-lag monitored; RPO ≤ 15 min validated by GoldenGate lag probe; RTO ≤ 4 h validated by `OQ-DR-FAILOVER-01`; full-site failover annual. |
| FS-PLAT-03 | URS-PLAT-03 | All configuration baselines (workflow XML, RPD reporting rules, MedDRA / WHO Drug version bindings, gateway profiles, role / SoD matrix) version-controlled in `gitlab.sirius.local/pv-config`; production changes via approved CR with rollback. |
| FS-PLAT-04 | URS-PLAT-04 | Argus Mart fed by Oracle GoldenGate 21c; latency probe `argus-mart-lag-seconds` Prometheus metric; threshold 15-min P95 alert. |
| FS-PLAT-05 | URS-PLAT-05 | Argus 8.4.1.x quarterly patch + critical out-of-band patch workflow: vendor-release-note ingestion → impact assessment (template `PV-CR-PATCH-IA`) within 14 days → regression-test pack execution (`OQ-PV-REG-PACK`) → promotion under CR with rollback plan. |
| FS-PLAT-06 | URS-PLAT-06 | Four environments DEV / QC / UAT / PROD; refresh-from-PROD uses Oracle Data Masking Pack with masking template `pv-pii-mask-v3`; non-PROD live-PII detection alert raised by quarterly scan. |
| FS-VND-01 | URS-VND-01 | Oracle vendor-assurance pack (SOC 2 Type II, ISO 27001, customer-shared CSV evidence) tracked in Vendor Assurance dossier `VA-ORACLE-2026`; annual re-qualification workflow. |
| FS-VND-02 | URS-VND-02 | Oracle release-note ingestion (RSS feed `oracle.com/argus/releasenotes.rss`); auto-ticket in CR system; impact assessment within 14 days. |
| FS-VND-03 | URS-VND-03 | Oracle TR-Audit summary filed annually in `VA-ORACLE-2026`. |
| FS-CFG-01 | URS-CFG-01 | Per-product configuration (RSI binding, listedness ruleset, jurisdictional expedited matrix, MedDRA version pin) follows DRAFT → REVIEW → APPROVED → EFFECTIVE; promotion gated by SoD-enforced signature (Author ≠ Approver). |
| FS-CFG-02 | URS-CFG-02 | Configuration export endpoint emits version-stamped JSON snapshot per product; archive retains all snapshots ≥ 50 years. |
| FS-CFG-03 | URS-CFG-03 | Rule-engine change-management runbook `SOP-PV-RULES-001`; re-baseline + OQ-replay required after any change to jurisdictional submission rules; replay uses regression case-pack `REG-CASES-2026-01`. |

### 4.2 Case Intake, Triage, Workflow (M-CASE)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CASE-01 | URS-CASE-01 | Intake adapters: manual entry UI; E2B(R3) inbound via Interchange; daily EDC reconciliation feed (Medidata Rave SAE webservice); literature-surveillance import (cron `lit-pull-weekly`); partner-exchange (per-partner profile); patient-support intake (REST endpoint `/intake/psp`); regulator-feedback (queue `regulator-feedback-in`). Each intake event recorded with channel, source-id, intake-timestamp. |
| FS-CASE-02 | URS-CASE-02 | Case-id generator emits monotonic ids per regional hub (Dublin / Basel / München / Wien); mandatory fields (intake date, awareness date, source country, reporter type, products, seriousness, expedited-eligibility) validated server-side at intake. |
| FS-CASE-03 | URS-CASE-03 | Workflow engine implements `{Intake → Triaged → Coded → Medically Assessed → Approved → Submitted → Closed}` with terminal-state auto-lock; reverse transitions require captured reason + electronic signature + audit-trail entry. |
| FS-CASE-04 | URS-CASE-04 | Reporting-clock service computes deadlines from awareness date per jurisdiction; rule pack covers FDA 7d/15d/30d, EU 15d/90d, PMDA local rules, BfArM/PEI/Swissmedic/AGES per-country rules; system raises D-3 / D-1 / D0 alerts to PV operations queue and to assigned reviewer. |
| FS-CASE-05 | URS-CASE-05 | Reclassification handler re-computes reporting clock and re-routes case; reclassification event audit-trailed with `prev_class`, `new_class`, `reason`. |
| FS-CASE-06 | URS-CASE-06 | Follow-up handler: incoming follow-up creates new case version `v_n+1`; version delta computed against `v_n`; E2B(R3) follow-up generation triggered when delta intersects E2B-relevant fields per rule `FOLLOWUP-DELTA-MATRIX-2026`. |
| FS-CASE-07 | URS-CASE-07 | Duplicate-detection rule engine uses configurable rule set (reporter ID + patient DOB / sex + event PT + onset-date ± 7-day proximity + product); suspected duplicates routed to Senior Case Processor queue for merge decision. |
| FS-CASE-08 | URS-CASE-08 | Case-priority matrix (high / medium / normal) configurable per product; high-priority cases routed to dedicated processor queue with SLA monitoring. |
| FS-CASE-09 | URS-CASE-09 | Workload-balancer distributes new cases across regional hubs with overflow rules to maintain reporting-clock margin; hub-affinity per reporter language. |
| FS-CASE-10 | URS-CASE-10 | Case-state-transition events emitted to Kafka topic `pv.case.state.v1` for KPI dashboards (Grafana `pv-cycle-time`). |

### 4.3 Coding — MedDRA, WHO Drug, Dictionary Lifecycle (M-CODE)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CODE-01 | URS-CODE-01 | MedDRA auto-coding using Argus AutoEncoder against product-master-pinned MedDRA version; suggestions surfaced to coder with confidence score; final selection logged with coder-id, suggestion accepted/overridden, override reason if applicable. |
| FS-CODE-02 | URS-CODE-02 | MedDRA coding performed at LLT level; PT, HLT, HLGT, SOC auto-derived from LLT via MedDRA hierarchy; coder confirms PT. |
| FS-CODE-03 | URS-CODE-03 | WHO Drug coding required for suspect / concomitant / interacting products; uncoded products block Approval (server-side validation); ATC classification auto-derived from drug record number. |
| FS-CODE-04 | URS-CODE-04 | MedDRA version-upgrade workflow (semi-annual per MSSO): impact-assessment template; open-case impact analysis; cut-over runbook; rollback plan; approval by QPPV designee + Head of PV. Argus MedDRA upgrade utility used. |
| FS-CODE-05 | URS-CODE-05 | Open-case re-coding rule: cases in {Intake, Triaged, Coded} states re-coded to new version automatically; cases in {Medically Assessed, Approved, Submitted, Closed} preserve version-of-record with new-version equivalent stored as `meddra_eq_v_new`. |
| FS-CODE-06 | URS-CODE-06 | WHO Drug annual release migration runbook; ATC reassignments tracked in `wd_change_log`; flagged in trending dashboards. |
| FS-CODE-07 | URS-CODE-07 | Coding-QC sample job (monthly, ≥ 2% of approved cases) generates discrepancy report to Coding Manager; root-cause categories feed coder training. |
| FS-CODE-08 | URS-CODE-08 | Auto-coding KPI dashboard: acceptance rate per LLT, override rate per LLT, top-overridden LLTs; reviewed quarterly. |
| FS-CODE-09 | URS-CODE-09 | Company-preferred-term list (CPT) maintained per product / disambiguation context; auto-coder consults CPT before MedDRA hierarchy. |

### 4.4 Medical Assessment and Approval (M-ASSESS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ASSESS-01 | URS-ASSESS-01 | Seriousness UI: structured checkbox per ICH E2A criterion (death, life-threatening, hospitalisation/prolonged, persistent/significant disability, congenital anomaly, medically important); free-text rationale optional. |
| FS-ASSESS-02 | URS-ASSESS-02 | Causality UI: structured WHO-UMC categories (certain / probable / possible / unlikely / conditional / unassessable); RSI cross-reference surfaced for context. |
| FS-ASSESS-03 | URS-ASSESS-03 | Expectedness UI: structured listed / unlisted against current RSI version; RSI version-of-record auto-surfaced at assessment time and stamped to assessment record. |
| FS-ASSESS-04 | URS-ASSESS-04 | Approval to submit requires QPPV-designee re-authenticated electronic signature (Okta MFA challenge, max-age 5 min); signature cryptographically bound to case state via HMAC-SHA-256(record-hash + signer-id + timestamp). |
| FS-ASSESS-05 | URS-ASSESS-05 | Reclassification triggers reporting-clock recalculation + case re-route; reroute event recorded with reason and old/new classification values. |
| FS-ASSESS-06 | URS-ASSESS-06 | Dual-narrative field: Company Assessment + Reporter's Assessment; both preserved with no overwriting; edits create new version. |
| FS-ASSESS-07 | URS-ASSESS-07 | Paediatric flag (per ICH E11 age groups) auto-set from patient DOB; assessment UI surfaces applicable PIP and paediatric-listedness considerations. |
| FS-ASSESS-08 | URS-ASSESS-08 | Reviewer assignment uses skills-matrix (therapeutic area, language coverage de-DE / fr-CH / it-CH) + workload balancing. |
| FS-ASSESS-09 | URS-ASSESS-09 | Time-in-state metric per case in Medical-Assessment state; auto-escalation to back-up reviewer when remaining-clock < safety margin. |

### 4.5 Submissions and Reporting (M-SUB)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SUB-01 | URS-SUB-01 | E2B(R3) XML generated per ICH M2 ESTRI standard + per-agency profile (EudraVigilance, FAERS, PMDA, CESG); XSD schema validation pre-send; rejection blocks transmission. |
| FS-SUB-02 | URS-SUB-02 | E2B(R3) element-coverage matrix per agency (`agency-profile-evdas-2026`, `agency-profile-faers-2026`, `agency-profile-pmda-2026`, `agency-profile-cesg-2026`); mandatory-optional matrix enforced at generation time. |
| FS-SUB-03 | URS-SUB-03 | Argus Interchange transmits to gateway; ACK-1 (transport), ACK-2 (application), ACK-3 (business response) reconciled to case; status reflected on case page. |
| FS-SUB-04 | URS-SUB-04 | Negative-ack opens structured Exception with agency-error-code mapping; re-submission within grace period; if breached, escalation event to QPPV via PagerDuty `pv-qppv-oncall`. |
| FS-SUB-05 | URS-SUB-05 | Aggregate-report (PSUR / PBRER / PADER / DSUR) runs on configured schedules; query / template versioning controlled; data-cut timestamp + dataset checksum stamped on report. |
| FS-SUB-06 | URS-SUB-06 | NullFlavor + dataElementOmissionReason handling per ICH M2; empty-element emission prohibited via XSLT post-processor. |
| FS-SUB-07 | URS-SUB-07 | ICSR identifier continuity maintained across initial → follow-up → nullification per ICH E2B(R3) §C.1.8; nullification reason captured in `C.1.11`. |
| FS-SUB-08 | URS-SUB-08 | Submission throughput sustained ≥ 500 ICSRs / hour to a single gateway; verified by `PQ-SUBMISSION-THROUGHPUT-01`. |
| FS-SUB-09 | URS-SUB-09 | Agency-window calendar `agency-windows-2026.yaml` configurable per agency; submission scheduler avoids maintenance windows. |
| FS-SUB-10 | URS-SUB-10 | Retry policy: exponential backoff (base 60s, factor 2, max 16 retries / ~24h); manual intervention after exhaustion. |

### 4.6 Aggregate Reporting (M-AGG)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AGG-01 | URS-AGG-01 | PSUR / PBRER generator: body / appendices auto-populated from validated data sets per ICH E2C(R2); manual sections (exec summary, integrated benefit-risk evaluation) authored in report module. |
| FS-AGG-02 | URS-AGG-02 | PADER generator (FDA, 21 CFR 314.80(c)(2)): quarterly for first 3 years post-approval; annual thereafter; per product. |
| FS-AGG-03 | URS-AGG-03 | DSUR generator (ICH E2F): annual per investigational product per DIBD; data pulled from EDC + Argus + CTMS. |
| FS-AGG-04 | URS-AGG-04 | Data-cut date, MedDRA version, WHO Drug version, dataset SHA-256 checksum stamped on every aggregate-report output. |
| FS-AGG-05 | URS-AGG-05 | Aggregate-report dual signature (Author + Approver) + QPPV countersign for EU PSUR / PBRER. |
| FS-AGG-06 | URS-AGG-06 | EMA PSUR Repository submission via web-service; legacy national submissions supported via `legacy-national-psur-2026` config flag during transition. |
| FS-AGG-07 | URS-AGG-07 | Aggregate-report template version stored with each report run; impact assessment on prior periods triggered on template change. |
| FS-AGG-08 | URS-AGG-08 | Export PDF/A-3 with embedded source XML (PSUR data XML + tabulations). |

### 4.7 Signal Detection and Management (M-SIG)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SIG-01 | URS-SIG-01 | Empirica Signal-integrated quantitative signal-detection: PRR, ROR, EBGM with per-drug-event-pair thresholds; configurable lower-bound CI; output to signal-management queue. |
| FS-SIG-02 | URS-SIG-02 | EVDAS integration via EMA EVDAS web service; daily EVDAS signal alert ingestion into the same workflow. |
| FS-SIG-03 | URS-SIG-03 | Qualitative signal entry channel (aggregate-report scrutiny, regulator query, partner report, literature) creates `Signal-of-Interest` record. |
| FS-SIG-04 | URS-SIG-04 | Signal-management state machine: Validation → Confirmation → Prioritisation → Assessment → Recommendation → Closure per GVP Module IX; transition gates require role-restricted signature. |
| FS-SIG-05 | URS-SIG-05 | SoD enforced: Signal Closer ≠ Signal Reviewer of same signal; auto-close on timeout DISABLED by default. |
| FS-SIG-06 | URS-SIG-06 | Signal-closure record requires `evidence_basis` field (case-ids + aggregate-data ref + literature ref); validation blocks close without evidence. |
| FS-SIG-07 | URS-SIG-07 | Signal-closure outcome that changes labelling emits event to Regulatory Affairs labelling-change workflow (Vault RIM). |
| FS-SIG-08 | URS-SIG-08 | Signal-management KPI dashboard: time-to-validation, time-to-assessment, time-to-closure; monthly QPPV review. |
| FS-SIG-09 | URS-SIG-09 | Signal-detection algorithm pack version-controlled in `gitlab.sirius.local/pv-sigdetect`; algorithm changes re-validated via `OQ-SIG-ALGO-REVAL-01`. |

### 4.8 RMP / REMS (M-RMP)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RMP-01 | URS-RMP-01 | RMP commitment register per product with milestone tracking; data feed from PV system to RMP module via internal API. |
| FS-RMP-02 | URS-RMP-02 | RMP-update trigger events: signal-closure outcome, regulator request, PSUR conclusion; trigger event audit-trailed. |
| FS-RMP-03 | URS-RMP-03 | REMS module with REMS Document, REMS Assessment Reports schedule, REMS modification history; FDA REMS submission tracked. |
| FS-RMP-04 | URS-RMP-04 | RMP / REMS overdue-commitment alert engine; alerts to QPPV + Reg Affairs. |
| FS-RMP-05 | URS-RMP-05 | RMP educational-material distribution tracker (vendor-print integration); KPIs reported quarterly. |
| FS-RMP-06 | URS-RMP-06 | PASS plan-and-milestone tracker; study-completion data flows into PSUR / PBRER input. |

### 4.9 PIP (M-PIP)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PIP-01 | URS-PIP-01 | PIP register per product with milestone tracker per EU Reg. 1901/2006; modifications version-controlled. |
| FS-PIP-02 | URS-PIP-02 | Paediatric-flag set from patient DOB using ICH E11 age-group rules; cases surfaced in PIP-context reporting. |
| FS-PIP-03 | URS-PIP-03 | PIP-derived data feed into PSUR / PBRER paediatric sections + DSUR paediatric appendices. |

### 4.10 IDMP / xEVMPD (M-IDMP)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-IDMP-01 | URS-IDMP-01 | Product-master holds ISO 11238 (substance), 11239 (dose form / unit), 11240 (UoM), 11615 (medicinal product), 11616 (pharmaceutical product) identifiers; reconciled against EMA SPOR via daily diff job. |
| FS-IDMP-02 | URS-IDMP-02 | Product-master update workflow: Steward → Approver SoD-enforced; propagation to cases per `propagation-matrix.yaml` (open cases re-coded; historical preserved with cross-ref). |
| FS-IDMP-03 | URS-IDMP-03 | xEVMPD submission worker: XEVPRM transactions (initial / variation / nullification) tracked with EMA ack reconciliation; submission events audit-trailed. |
| FS-IDMP-04 | URS-IDMP-04 | Quarterly IDMP drift-detection job against EMA SPOR; impact-assessment opened for any in-scope product. |

### 4.11 Literature Surveillance (M-LIT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-LIT-01 | URS-LIT-01 | Weekly cron `lit-pull-weekly` queries Embase + PubMed + regional journals (Arzneimittelbrief DE, Pharmazeutische Mitteilungen AT, Schweizerische Ärztezeitung CH, Prescrire FR) with per-product strategies. |
| FS-LIT-02 | URS-LIT-02 | Triage UI for surveillance hits; eligible hits create ICSR with source = `literature` and citation captured per ICH E2B(R3) §C.4 fields. |
| FS-LIT-03 | URS-LIT-03 | Strategy version-control in `gitlab.sirius.local/pv-lit-strategies`; annual review workflow. |
| FS-LIT-04 | URS-LIT-04 | FP / TP rate metrics per strategy in monthly literature-surveillance report. |

### 4.12 Partner-Exchange (M-PEX)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PEX-01 | URS-PEX-01 | Partner profile registry: per-partner PVA / SDEA parameters loaded; Argus Interchange exchange behaviour configured per profile. |
| FS-PEX-02 | URS-PEX-02 | Inbound idempotency via `partner_source_case_id` deduplication key; outbound timer per PVA-stipulated timeline. |
| FS-PEX-03 | URS-PEX-03 | Exchange events audit-trailed with partner-id, direction, exchange timestamp, ack status, PVA-clause reference. |
| FS-PEX-04 | URS-PEX-04 | Partner KPI dashboard: timeliness + quality (% rejected, % corrected); reviewed quarterly. |

### 4.13 Audit Trail (M-AUD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit-trail schema (`audit_event`): event_id, case_id, user_id, action, old_value, new_value, reason, timestamp_iso8601 (UTC); covers all case / coding / assessment / signature / config / submission / reporting-clock events. |
| FS-AUD-02 | URS-AUD-02 | DB-level append-only: DELETE/UPDATE revoked on `audit_event` table; DBA dual-control on DDL; application API exposes read + insert only. |
| FS-AUD-03 | URS-AUD-03 | Audit-trail review jobs configured per PV QA plan: case-level event-driven at approval; platform-level quarterly; evidence filed in QA dossier `QA-PV-AUDIT-REVIEW-NNN`. |
| FS-AUD-04 | URS-AUD-04 | Retention enforced by archival policy: ≥ 50 years EU-marketed; ≥ life-of-product + 10y US; ≥ life-of-product + 35y paediatric per ICH M11; immutable cold storage with object-lock. |
| FS-AUD-05 | URS-AUD-05 | Audit-event volume monitored via Prometheus metric `audit_events_per_minute`; threshold alert for spikes. |
| FS-AUD-06 | URS-AUD-06 | Audit-trail export endpoint emits CSV + accompanying SHA-256 hash file for inspector handover. |

### 4.14 21 CFR Part 11 (M-PART11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural-control SOPs (`SOP-PV-VALIDATION-001`, `SOP-PV-CASE-MGMT-002`, `SOP-PV-SIGNATURE-003`) reviewed annually. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(b): copy generation — case PDF rendering, E2B(R3) XML export, audit-trail CSV export — verified under OQ. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(c): records protected with checksum-protected immutable archives (AWS S3 Object Lock equivalent on OCI). |
| FS-PART11-04 | URS-PART11-04 | Per § 11.10(d): access limited to authorised individuals via Okta SAML 2.0 + MFA; service accounts via mTLS-only. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.10(e): operational audit trail per FS-AUD-01. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.10(g): authority checks enforced at workflow / API layer (Argus role-permission matrix + API guard middleware). |
| FS-PART11-07 | URS-PART11-07 | Per § 11.10(k): operation manuals controlled in Vault QualityDocs; revisions under change control with version traceability. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.50: signature events render printed name + date/time + meaning into audit trail and PDF representation. |
| FS-PART11-09 | URS-PART11-09 | Per § 11.70: signatures cryptographically linked via HMAC-SHA-256 over (record-hash, signer-id, timestamp); tampered records flagged on read. |
| FS-PART11-10 | URS-PART11-10 | Per § 11.100: user-id uniqueness enforced via Argus + Okta IdP; deactivated user-ids never reassigned (Okta policy + DB constraint). |
| FS-PART11-11 | URS-PART11-11 | Per § 11.200: re-authentication (password + MFA) required at every critical signature event (case approval, RMP/REMS approval, aggregate-report approval, signal-closure); cached creds rejected by max-age 5 min OAuth2 token. |
| FS-PART11-12 | URS-PART11-12 | Per § 11.300: password / credential controls per InfoSec policy (length ≥ 12, complexity, MFA, 90-day rotation, lockout 5 failures). |
| FS-GVP-01 | URS-GVP-01 | GVP Module II §VI.B.6 mapping documented in PSMF section 3.4; system-master-file linkage. |
| FS-GVP-02 | URS-GVP-02 | GVP Module I — QPPV designation + Deputy QPPV + PSMF chapter-version control via `pv-psmf-control` register. |
| FS-GVP-03 | URS-GVP-03 | GVP Module IX signal-management framework implemented via M-SIG. |
| FS-GVP-04 | URS-GVP-04 | GVP Module XV — DHCPL distribution tracker integrated with Reg Affairs. |

### 4.15 DACH National-CA Gateways (M-NCA)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-NCA-BFARM-01 | URS-NCA-BFARM-01 | BfArM gateway endpoint `https://pv.bfarm.bund.de/gateway/v2` via Argus Interchange profile `agency-profile-bfarm-2026`; mTLS; quarterly connectivity test. |
| FS-NCA-PEI-01 | URS-NCA-PEI-01 | Paul-Ehrlich-Institut endpoint `https://pv.pei.de/biological/gateway` for biologicals; product-master routes biological products via PEI. |
| FS-NCA-SWISS-01 | URS-NCA-SWISS-01 | Swissmedic endpoint per HMG / VAM; CH-specific timelines configured. |
| FS-NCA-AGES-01 | URS-NCA-AGES-01 | AGES PharmMed endpoint per AMG (AT) requirements. |
| FS-NCA-ROUTING-01 | URS-NCA-ROUTING-01 | Routing matrix `nca-routing-matrix-2026.yaml` directs each case to EudraVigilance + applicable national CAs based on (country-of-incidence, product type, jurisdictional rules). |
| FS-NCA-LANG-01 | URS-NCA-LANG-01 | DACH templates support de-DE, de-AT, de-CH, fr-CH, it-CH variants in FSN / DHCPL output. |

### 4.16 Clinical-Trial Safety (M-CT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CT-SAFETY-01 | URS-CT-SAFETY-01 | SUSAR identification rule fires E2B(R3) expedited submission within 7d (fatal/life-threatening) or 15d (other) to EudraVigilance + FDA + applicable jurisdictions per EU CTR 536/2014 + 21 CFR 312.32. |
| FS-CT-SAFETY-02 | URS-CT-SAFETY-02 | DSUR generator pulls cases via EDC (Medidata Rave) + CTMS (Veeva Vault CTMS) integration; data-cut reproducible via dataset checksum. |
| FS-CT-SAFETY-03 | URS-CT-SAFETY-03 | CTIS (EU CTR 536/2014) safety-reporting interface; ack reconciliation tracked. |
| FS-CT-SAFETY-04 | URS-CT-SAFETY-04 | Controlled-unblinding workflow preserves trial blind via two-person principle (unblinder + reviewer); audit-trailed; restored-blind notice issued to clinical-ops on completion. |
| FS-CT-SAFETY-05 | URS-CT-SAFETY-05 | EU CTR 536/2014 Annual Safety Report generator pulls trial-level safety data on a per-trial annual cycle; tabulation pack reproducible via dataset checksum. |

### 4.17 Data Integrity (M-DI)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | **Attributable:** every record / change carries `actor_id`; DB constraint NOT NULL on `audit_event.user_id`. |
| FS-DI-02 | URS-DI-02 | **Legible:** PDF/A-3 rendering + E2B(R3) XML export verified under OQ. |
| FS-DI-03 | URS-DI-03 | **Contemporaneous:** server-side NTP-synced timestamps; retroactive entries flagged with `delay_reason`. |
| FS-DI-04 | URS-DI-04 | **Original:** source preserved unaltered; corrections recorded as new version; reconstruction-of-event order possible from audit. |
| FS-DI-05 | URS-DI-05 | **Accurate:** reporting-clock + aggregate-extract calculations deterministic; OQ-verified via golden-test pack. |
| FS-DI-06 | URS-DI-06 | **Complete:** mandatory-field matrix per agency E2B(R3) profile enforced at submission. |
| FS-DI-07 | URS-DI-07 | **Consistent:** chronological order DB-enforced; LLT→PT mapping consistent via MedDRA hierarchy. |
| FS-DI-08 | URS-DI-08 | **Enduring:** ≥ 50y EU retention enforced at archive tier with object-lock. |
| FS-DI-09 | URS-DI-09 | **Available:** retrieval ≤ 4h documented in `SOP-PV-INSPECTION-RETRIEVAL`. |

### 4.18 Security, Performance, Availability, Backup (M-SEC + M-PERF)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SEC-01 | URS-SEC-01 | Okta SAML 2.0 + MFA for users; mTLS for service accounts. |
| FS-SEC-02 | URS-SEC-02 | RBAC region-product matrix in Argus role-permission table + Okta groups. |
| FS-SEC-03 | URS-SEC-03 | GDPR DPIA on file (`DPIA-PV-2026-001`); subject-identifier minimisation guidance enforced via narrative-template + DLP regex policy; cross-border transfers via SCCs / DPF (`pv-scc-2026`). |
| FS-SEC-04 | URS-SEC-04 | HIPAA + PIPEDA compliance via tenant-region binding (`tenant-region-matrix-2026`). |
| FS-SEC-05 | URS-SEC-05 | Monthly Tenable Nessus vulnerability scans; critical findings remediation 30d. |
| FS-SEC-06 | URS-SEC-06 | Annual third-party pen-test; high/critical remediation under CR. |
| FS-SEC-07 | URS-SEC-07 | DLP controls (Microsoft Purview equivalent on OCI) block bulk export of identifiable case data without authorised approval. |
| FS-PERF-01 | URS-PERF-01 | App-server tier sized for 300 concurrent processors (20% headroom); P95 nav ≤ 3s validated by `PQ-PERF-NAV-01`. |
| FS-PERF-02 | URS-PERF-02 | E2B(R3) generation P95 ≤ 10s validated by `PQ-PERF-E2B-GEN-01`. |
| FS-PERF-03 | URS-PERF-03 | PSUR / PBRER extract P95 ≤ 4h for 5-year reporting period validated by `PQ-PERF-PSUR-EXTRACT-01`. |
| FS-AV-01 | URS-AV-01 | Availability ≥ 99.5% business hours; 24×7 for gateway during submission windows; uptime probes 24×7. |
| FS-AV-02 | URS-AV-02 | RPO ≤ 15 min; RTO ≤ 4h; annual full-DR test including end-to-end gateway resubmission. |
| FS-BAK-01 | URS-BAK-01 | Oracle nightly backup + continuous archived redo; retention ≥ 50y; immutable cold storage with object-lock. |
| FS-BAK-02 | URS-BAK-02 | Annual full-DR test results filed in `RUN-DR-NNN`. |
| FS-BAK-03 | URS-BAK-03 | Quarterly partial-DR rehearsal (single hub + single gateway) without PROD downtime. |

### 4.19 Training and Periodic Review (M-TRN + M-PR)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Production access gated by LMS-recorded role-specific training + PV competency; Medical Reviewer competency re-attested annually. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher `PV-ANNUAL-2026`: GVP updates, FDA post-marketing updates, ICH revisions, EVDAS / FAERS technical changes. |
| FS-TRN-03 | URS-TRN-03 | DACH-specific training module `PV-DACH-2026`: BfArM / PEI / Swissmedic / AGES + DACH-language case-handling. |
| FS-PR-01 | URS-PR-01 | Annual periodic-review run-book auto-collects: config drift, audit-trail evidence, MedDRA / WHO Drug version status, gateway connectivity tests, signal-management metrics, RMP/REMS commitments, PIP commitments, IDMP/xEVMPD reconciliation, partner-PVA currency, deviation summary, training currency. Signed by Head of PV Operations + QPPV + VP QA. |
| FS-PR-02 | URS-PR-02 | Quarterly operational-review report (cycle-time KPIs, reporting-clock margin distribution, gateway ack rates). |

---


### 4.20 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: SAML 2.0 via Entra ID with SCIM lifecycle provisioning. Conditional-access binding to policy `PV-Sensitive Conditional Access (FIDO2 phishing-resistant MFA + named-location enforcement)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with Oracle RMAN for the Argus Oracle backend; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.21 Cross-System Integration — Hydra + Helios (M-XINT-HYD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HYD-01 | URS-XINT-HYD-01 | Egress firewall ACL `pv-argus-egress-deny-llm` blocks tenant-direct routes to anthropic.com, openai.com, *.azure-openai.com except via the Hydra gateway VIP; Argus PV adapter `SIR-HYD-CLIENT-1.x` enforces use-case ID in every request. |
| FS-XINT-HYD-02 | URS-XINT-HYD-02 | Hydra use-case `PV-CASE-TRIAGE-001` is registered with `risk_class=annex_i` and `art_11_pack_artifact=pv-triage-art11-v1.x.pdf`; gate returns 403 when pack is missing or expired. |
| FS-XINT-HYD-03 | URS-XINT-HYD-03 | Argus PV UI surfaces per-suggestion Accept / Reject + reviewer comment; bulk-accept absent; back-end rejects any payload with `bulk_accept=true`; submission-timer service is gated on the HITL evidence row presence. |
| FS-XINT-HYD-04 | URS-XINT-HYD-04 | Incident-routing service `sir-hyd-art73` posts to Hydra Art. 73 endpoint + cross-posts to the configured MAH defect-channel SMTP and to BfArM/Swissmedic/AGES PV gateways per Argus DACH gateway map. |
| FS-XINT-HYD-05 | URS-XINT-HYD-05 | Helios ingestion via Kafka topic `helios.ingest.sirius.hydra.v1` (JSON Lines schema-registry pinned); retention floor on the Argus side 2 y. |


### 4.22 Cross-System Integration — Helios handover (M-XINT-HEL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HEL-01 | URS-XINT-HEL-01 | Audit-event publisher emits Kafka topic `helios.ingest.sirius.argus.v1` with schema-registry-pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`; at-least-once delivery; idempotency key `{source_system, event_id}`; back-pressure surfaced via Prometheus `helios_publish_lag_seconds` with 5-min alert at > 600 s. |
| FS-XINT-HEL-02 | URS-XINT-HEL-02 | Local audit-store retention policy enforces ≥ 30 y; Helios ack persisted as `helios_ack_ts` per event; periodic reconciliation job verifies parity (Helios row count == local published count) and raises a deviation in MasterControl on > 0.01% mismatch over a 24 h window. |


### 4.23 Cross-System Integration — LMS handover (M-XINT-LMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-LMS-01 | URS-XINT-LMS-01 | LMS-competence adapter `<sys>-LMS-CLIENT-1.x` performs `GET /lms/competence/{user_id}?curriculum=...` over mTLS + Entra workload-identity; cache TTL per system (12-24 h); on `current=false` the consumer blocks the gated action and records `lms_lapse_user={user_id}` in the consumer audit trail; periodic reconciliation job verifies that no gated action proceeded with a lapsed competence. |

## 5. Interface Specifications

| IF ID | URS ID | Counterparty | Protocol | Direction | Notes |
|---|---|---|---|---|---|
| IF-OKTA-01 | URS-SEC-01 | Okta | SAML 2.0 + MFA | bidirectional | SSO |
| IF-EVDAS-01 | URS-SUB-03, URS-SIG-02 | EMA EudraVigilance | E2B(R3) gateway + EVDAS web service | bidirectional | quarterly connectivity test |
| IF-FAERS-01 | URS-SUB-03 | FDA FAERS / ESG | E2B(R3) gateway via FDA ESG | bidirectional | quarterly connectivity test |
| IF-PMDA-01 | URS-SUB-03 | PMDA Gateway | E2B(R3) gateway | bidirectional | per-jurisdiction profile |
| IF-CESG-01 | URS-SUB-03 | Health Canada CESG | E2B(R3) gateway | bidirectional | per-jurisdiction profile |
| IF-BFARM-01 | URS-NCA-BFARM-01 | BfArM | E2B(R3) via mTLS gateway | bidirectional | quarterly connectivity test |
| IF-PEI-01 | URS-NCA-PEI-01 | Paul-Ehrlich-Institut | E2B(R3) via mTLS gateway | bidirectional | biologicals |
| IF-SWISS-01 | URS-NCA-SWISS-01 | Swissmedic | E2B(R3) via mTLS | bidirectional | HMG / VAM |
| IF-AGES-01 | URS-NCA-AGES-01 | AGES PharmMed | E2B(R3) via mTLS | bidirectional | AMG (AT) |
| IF-EDC-01 | URS-CT-SAFETY-01, URS-CASE-01 | Medidata Rave EDC | secure file / REST | bidirectional | daily SAE / SUSAR reconciliation |
| IF-CTMS-01 | URS-CT-SAFETY-02 | Veeva Vault CTMS | REST | bidirectional | trial-product master |
| IF-CTIS-01 | URS-CT-SAFETY-03 | EU CTIS | REST | outbound + ack | EU CTR safety reporting |
| IF-VAULT-RIM-01 | URS-SIG-07 | Veeva Vault RIM | REST | outbound | labelling-change handoff |
| IF-PARTNER-01 | URS-PEX-01 | License / co-dev partners | E2B(R3) per-PVA | bidirectional | per-partner profile |
| IF-LIT-01 | URS-LIT-01 | Embase + PubMed + regional journals | weekly feed | inbound | literature surveillance |
| IF-SPOR-01 | URS-IDMP-01, URS-IDMP-04 | EMA SPOR | REST / data files | inbound | IDMP reference data |
| IF-XEVMPD-01 | URS-IDMP-03 | EMA xEVMPD | XEVPRM web service | outbound + ack | xEVMPD submissions |

## 6. Data Model (high-level)

| Entity | Attributes (illustrative) |
|---|---|
| Case | case_id, intake_date, awareness_date, source_country, reporter_type, products[], seriousness, expedited_eligibility, state, hub, priority |
| CaseVersion | case_id, version, payload, prev_version, created_by, created_at |
| CodingDecision | case_id, term, dictionary {MedDRA, WHO Drug}, version, decision_by, decision_at, override_reason? |
| Assessment | case_id, seriousness, causality, expectedness, rsi_version_ref, company_narrative, reporter_narrative, assessor_id, assessed_at |
| Signature | sig_id, case_id, signer_id, meaning, timestamp, hmac_sha256 |
| Submission | case_id, agency, e2b_payload_ref, sent_at, ack_status, ack_at, exception_ref? |
| AggReport | report_id, type {PSUR, PBRER, PADER, DSUR}, data_cut_at, meddra_version, whodrug_version, dataset_checksum, output_uri |
| Signal | signal_id, drug, event_pt, prr, ror, ebgm, ebgm_lower_ci, state, evidence_basis, closed_by, closed_at |
| RMPCommitment | commitment_id, product_id, type, due_date, status, owner |
| PIPMilestone | milestone_id, product_id, milestone_name, due_date, status |
| Product | product_id, idmp_substance_id, idmp_dose_form_id, idmp_uom_id, idmp_med_product_id, idmp_pharm_product_id, atc, rsi_version_ref |
| PartnerProfile | partner_id, pva_ref, exchange_timelines, jurisdictions, contact_qppv |
| LitHit | hit_id, source, citation_e2b_c4, query_strategy_ref, triage_decision, case_id? |
| AuditEvent | event_id, case_id?, user_id, action, old, new, reason, timestamp |

## 7. Non-Functional Specifications

| NFR ID | Specification |
|---|---|
| NFR-01 | P95 case-page navigation ≤ 3s under peak (300 concurrent processors) |
| NFR-02 | Availability ≥ 99.5% business hours; 24×7 gateway during submission windows |
| NFR-03 | RPO ≤ 15 min; RTO ≤ 4h; annual full-DR test |
| NFR-04 | Audit trail append-only |
| NFR-05 | Retention ≥ 50y for EU-marketed products |
| NFR-06 | Reporting-clock alert latency ≤ 5 min from awareness-date update |
| NFR-07 | E2B(R3) generation P95 ≤ 10s per case |
| NFR-08 | PSUR / PBRER extract P95 ≤ 4h for 5-year reporting period |
| NFR-09 | Submission throughput ≥ 500 ICSRs / hour per gateway |
| NFR-10 | Argus Mart datamart lag P95 ≤ 15 min |

## 8. Configuration Items (CI)

| CI ID | Item | Configured Value | Source |
|---|---|---|---|
| CI-01 | App-server count (active) | 3 | URS-PLAT-01 |
| CI-02 | DR mode | Data Guard physical-standby (async) | URS-PLAT-01, URS-PLAT-02 |
| CI-03 | DR RPO target | 15 min | URS-PLAT-02 |
| CI-04 | DR RTO target | 4 h | URS-PLAT-02 |
| CI-05 | Reporting-clock alerts | D−3 / D−1 / D0 | URS-CASE-04 |
| CI-06 | MedDRA version policy | per-product pinned; semi-annual upgrade | URS-CODE-01, URS-CODE-04 |
| CI-07 | E2B(R3) targets | EVDAS, FAERS, PMDA, Health Canada, BfArM, PEI, Swissmedic, AGES | URS-SUB-01, URS-SUB-02, URS-SUB-03, URS-NCA-BFARM-01, URS-NCA-PEI-01, URS-NCA-SWISS-01, URS-NCA-AGES-01 |
| CI-08 | Audit-trail | append-only, exportable | URS-AUD-02 |
| CI-09 | Retention | ≥ 50y EU-marketed | URS-AUD-04 |
| CI-10 | Re-authentication on signing | required (OAuth2 max-age 5 min) | URS-PART11-11 |
| CI-11 | Vuln-scan cadence | monthly | URS-SEC-05 |
| CI-12 | DR-test cadence | annual full + quarterly partial | URS-AV-02, URS-BAK-02, URS-BAK-03 |
| CI-13 | EDC reconciliation cadence | daily | URS-CASE-01, URS-CT-SAFETY-01 |
| CI-14 | Gateway connectivity test cadence | quarterly | URS-NCA-* |
| CI-15 | Signal-detection thresholds | per drug-event-pair | URS-SIG-01 |
| CI-16 | EVDAS feed cadence | daily | URS-SIG-02 |
| CI-17 | Literature-surveillance cadence | weekly | URS-LIT-01 |
| CI-18 | IDMP drift-detection cadence | quarterly | URS-IDMP-04 |
| CI-19 | xEVMPD submission targets | EMA | URS-IDMP-03 |
| CI-20 | Aggregate-report cadence | PSUR/PBRER per EU RD; PADER quarterly→annual; DSUR annual | URS-AGG-01, URS-AGG-02, URS-AGG-03 |

## 9. Constraints / Assumptions / Risks

- **Constraints:** No site-authored custom code (Cat-4 only); MedDRA / WHO Drug upgrades managed semi-annually / annually under change control; Oracle vendor patches under change control; QPPV signature non-delegatable.
- **Assumptions:** Oracle OCI infrastructure; Okta; Medidata Rave; Veeva Vault CTMS / eTMF; EMA SPOR; EVDAS; FAERS; PMDA; CESG; BfArM; PEI; Swissmedic; AGES gateways operational + validated; gateway certificates rotated per PV SOP.
- **FS-level risks:** missed reporting deadline (FS-CASE-04 + alerts + queue monitoring); E2B XML schema rejection (FS-SUB-01 + schema validation); MedDRA version drift open cases (FS-CODE-05); EVDAS / FAERS connectivity loss (FS-AV-02 + FS-SUB-10 retry); reclassification miss (FS-ASSESS-05); audit-trail tampering (FS-AUD-02 + DBA dual-control); signal false-negative (FS-SIG-01 thresholds tuning); IDMP referential drift (FS-IDMP-04 quarterly job); partner duplicate-case (FS-PEX-02 idempotency); literature regional FN (FS-LIT-04 metrics).

## 10. References

- SIR-URS-PV-001 v1.2 (parent URS).
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR 314.80, 600.80, 312.32.
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EU GVP Modules I–XVI (esp. II, V, VI, VII, IX, XV).
- EU CTR Reg. 536/2014 + CTIS.
- GDPR Reg. (EU) 2016/679 Arts. 6, 9, 32, 35.
- ICH E2A, E2B(R3), E2C(R2), E2D, E2E, E2F, M1, M2.
- IDMP ISO 11238 / 11239 / 11240 / 11615 / 11616.
- EMA EudraVigilance + EVDAS specifications.
- EMA SPOR data services.
- BfArM (DE), Paul-Ehrlich-Institut (DE), Swissmedic (CH), AGES PharmMed (AT) PV reporting requirements.
- ISPE GAMP 5 (2nd ed., 2022); PIC/S PI 041; ISO/IEC 27001:2022.
- Oracle — *Argus Safety 8.4.1 Configuration Reference*; *Argus Interchange E2B(R3) Implementation Guide*; *Argus Mart Reporting User Guide*; *Empirica Signal User Guide*.

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-PLAT-01 | FS-PLAT-01 |
| URS-PLAT-02 | FS-PLAT-02 |
| URS-PLAT-03 | FS-PLAT-03 |
| URS-PLAT-04 | FS-PLAT-04 |
| URS-PLAT-05 | FS-PLAT-05 |
| URS-PLAT-06 | FS-PLAT-06 |
| URS-VND-01 | FS-VND-01 |
| URS-VND-02 | FS-VND-02 |
| URS-VND-03 | FS-VND-03 |
| URS-CFG-01 | FS-CFG-01 |
| URS-CFG-02 | FS-CFG-02 |
| URS-CFG-03 | FS-CFG-03 |
| URS-CASE-01 | FS-CASE-01 |
| URS-CASE-02 | FS-CASE-02 |
| URS-CASE-03 | FS-CASE-03 |
| URS-CASE-04 | FS-CASE-04 |
| URS-CASE-05 | FS-CASE-05 |
| URS-CASE-06 | FS-CASE-06 |
| URS-CASE-07 | FS-CASE-07 |
| URS-CASE-08 | FS-CASE-08 |
| URS-CASE-09 | FS-CASE-09 |
| URS-CASE-10 | FS-CASE-10 |
| URS-CODE-01 | FS-CODE-01 |
| URS-CODE-02 | FS-CODE-02 |
| URS-CODE-03 | FS-CODE-03 |
| URS-CODE-04 | FS-CODE-04 |
| URS-CODE-05 | FS-CODE-05 |
| URS-CODE-06 | FS-CODE-06 |
| URS-CODE-07 | FS-CODE-07 |
| URS-CODE-08 | FS-CODE-08 |
| URS-CODE-09 | FS-CODE-09 |
| URS-ASSESS-01 | FS-ASSESS-01 |
| URS-ASSESS-02 | FS-ASSESS-02 |
| URS-ASSESS-03 | FS-ASSESS-03 |
| URS-ASSESS-04 | FS-ASSESS-04 |
| URS-ASSESS-05 | FS-ASSESS-05 |
| URS-ASSESS-06 | FS-ASSESS-06 |
| URS-ASSESS-07 | FS-ASSESS-07 |
| URS-ASSESS-08 | FS-ASSESS-08 |
| URS-ASSESS-09 | FS-ASSESS-09 |
| URS-SUB-01 | FS-SUB-01 |
| URS-SUB-02 | FS-SUB-02 |
| URS-SUB-03 | FS-SUB-03 |
| URS-SUB-04 | FS-SUB-04 |
| URS-SUB-05 | FS-SUB-05 |
| URS-SUB-06 | FS-SUB-06 |
| URS-SUB-07 | FS-SUB-07 |
| URS-SUB-08 | FS-SUB-08 |
| URS-SUB-09 | FS-SUB-09 |
| URS-SUB-10 | FS-SUB-10 |
| URS-AGG-01 | FS-AGG-01 |
| URS-AGG-02 | FS-AGG-02 |
| URS-AGG-03 | FS-AGG-03 |
| URS-AGG-04 | FS-AGG-04 |
| URS-AGG-05 | FS-AGG-05 |
| URS-AGG-06 | FS-AGG-06 |
| URS-AGG-07 | FS-AGG-07 |
| URS-AGG-08 | FS-AGG-08 |
| URS-SIG-01 | FS-SIG-01 |
| URS-SIG-02 | FS-SIG-02 |
| URS-SIG-03 | FS-SIG-03 |
| URS-SIG-04 | FS-SIG-04 |
| URS-SIG-05 | FS-SIG-05 |
| URS-SIG-06 | FS-SIG-06 |
| URS-SIG-07 | FS-SIG-07 |
| URS-SIG-08 | FS-SIG-08 |
| URS-SIG-09 | FS-SIG-09 |
| URS-RMP-01 | FS-RMP-01 |
| URS-RMP-02 | FS-RMP-02 |
| URS-RMP-03 | FS-RMP-03 |
| URS-RMP-04 | FS-RMP-04 |
| URS-RMP-05 | FS-RMP-05 |
| URS-RMP-06 | FS-RMP-06 |
| URS-PIP-01 | FS-PIP-01 |
| URS-PIP-02 | FS-PIP-02 |
| URS-PIP-03 | FS-PIP-03 |
| URS-IDMP-01 | FS-IDMP-01 |
| URS-IDMP-02 | FS-IDMP-02 |
| URS-IDMP-03 | FS-IDMP-03 |
| URS-IDMP-04 | FS-IDMP-04 |
| URS-LIT-01 | FS-LIT-01 |
| URS-LIT-02 | FS-LIT-02 |
| URS-LIT-03 | FS-LIT-03 |
| URS-LIT-04 | FS-LIT-04 |
| URS-PEX-01 | FS-PEX-01 |
| URS-PEX-02 | FS-PEX-02 |
| URS-PEX-03 | FS-PEX-03 |
| URS-PEX-04 | FS-PEX-04 |
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
| URS-PART11-09 | FS-PART11-09 |
| URS-PART11-10 | FS-PART11-10 |
| URS-PART11-11 | FS-PART11-11 |
| URS-PART11-12 | FS-PART11-12 |
| URS-GVP-01 | FS-GVP-01 |
| URS-GVP-02 | FS-GVP-02 |
| URS-GVP-03 | FS-GVP-03 |
| URS-GVP-04 | FS-GVP-04 |
| URS-NCA-BFARM-01 | FS-NCA-BFARM-01 |
| URS-NCA-PEI-01 | FS-NCA-PEI-01 |
| URS-NCA-SWISS-01 | FS-NCA-SWISS-01 |
| URS-NCA-AGES-01 | FS-NCA-AGES-01 |
| URS-NCA-ROUTING-01 | FS-NCA-ROUTING-01 |
| URS-NCA-LANG-01 | FS-NCA-LANG-01 |
| URS-CT-SAFETY-01 | FS-CT-SAFETY-01 |
| URS-CT-SAFETY-02 | FS-CT-SAFETY-02 |
| URS-CT-SAFETY-03 | FS-CT-SAFETY-03 |
| URS-CT-SAFETY-04 | FS-CT-SAFETY-04 |
| URS-CT-SAFETY-05 | FS-CT-SAFETY-05 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-DI-07 | FS-DI-07 |
| URS-DI-08 | FS-DI-08 |
| URS-DI-09 | FS-DI-09 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-SEC-05 | FS-SEC-05 |
| URS-SEC-06 | FS-SEC-06 |
| URS-SEC-07 | FS-SEC-07 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-PERF-03 | FS-PERF-03 |
| URS-AV-01 | FS-AV-01 |
| URS-AV-02 | FS-AV-02 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-BAK-03 | FS-BAK-03 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-TRN-03 | FS-TRN-03 |
| URS-PR-01 | FS-PR-01 |
| URS-PR-02 | FS-PR-02 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-HYD-01 | FS-XINT-HYD-01 |
| URS-XINT-HYD-02 | FS-XINT-HYD-02 |
| URS-XINT-HYD-03 | FS-XINT-HYD-03 |
| URS-XINT-HYD-04 | FS-XINT-HYD-04 |
| URS-XINT-HYD-05 | FS-XINT-HYD-05 |
| URS-XINT-HEL-01 | FS-XINT-HEL-01 |
| URS-XINT-HEL-02 | FS-XINT-HEL-02 |
| URS-XINT-LMS-01 | FS-XINT-LMS-01 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Missed reporting deadline (jurisdictional clock breach) | Medium | High | URS-CASE-04, URS-CASE-05, URS-SUB-04 |
| R-02 | E2B(R3) XML schema rejection on agency-specific profile mismatch | Medium | High | URS-SUB-01, URS-SUB-02, URS-SUB-04 |
| R-03 | Mis-coded reaction term (MedDRA LLT → PT propagation error) | Medium | Medium | URS-CODE-01, URS-CODE-02, URS-CODE-07 |
| R-04 | MedDRA version drift on open cases at version cut-over | Medium | High | URS-CODE-04, URS-CODE-05 |
| R-05 | EVDAS / FAERS connectivity loss during expedited submission window | Medium | Critical | URS-NCA-ROUTING-01, URS-AV-02, URS-SUB-10 |
| R-06 | Reporting-clock recalculation miss on reclassification | Low | Critical | URS-ASSESS-05, URS-CASE-05 |
| R-07 | Audit-trail tampering by privileged user | Low | Critical | URS-AUD-02, URS-PART11-09 |
| R-08 | EDC ↔ Argus reconciliation drift (SAE missed) | Medium | High | URS-CT-SAFETY-01, URS-CASE-01 |
| R-09 | Signal detection false-negative (EBGM threshold mis-tuned) | Medium | High | URS-SIG-01, URS-SIG-09 |
| R-10 | Signal closure without evidence basis | Low | Critical | URS-SIG-05, URS-SIG-06 |
| R-11 | RMP commitment slipped (e.g., PASS study) | Medium | High | URS-RMP-04 |
| R-12 | IDMP referential drift breaking variation submission | Low | High | URS-IDMP-04 |
| R-13 | Partner-exchange duplicate-case proliferation | Medium | Medium | URS-PEX-02 |
| R-14 | Literature-surveillance false-negative on regional journal | Low | High | URS-LIT-01, URS-LIT-04 |
| R-15 | QPPV signature delegation under time pressure | Low | High | URS-ASSESS-04, URS-PART11-11 |
| R-16 | Data-residency non-compliance (GDPR Art. 44 transfers) | Low | High | URS-SEC-03, URS-SEC-04 |

Full evaluation in `SIR-RA-PV-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
