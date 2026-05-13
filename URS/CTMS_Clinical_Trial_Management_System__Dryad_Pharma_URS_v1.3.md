---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; T4 hand-expansion 2026-05-12"
seed_corpus_basis:
  - "GAMP 5 (2nd ed.) Cat 4 conventions for SaaS clinical-operations platforms"
  - "21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300; 21 CFR Parts 312, 314, 50, 56"
  - "ICH E6(R3) GCP (Step 4, 6 January 2025); ICH E8(R1); ICH E9(R1); ICH E2A"
  - "EU CTR 536/2014 + CTIS Sponsor Handbook"
  - "FDA Computerized Systems Used in Clinical Investigations (May 2007)"
  - "FDA BIMO Inspection Manual 7348.809 (updated 4 April 2025)"
  - "ISO 14155:2020 (clinical investigation of medical devices)"
  - "Veeva Vault CTMS 24R3 / 25R1 vendor documentation"
  - "TMF Reference Model v3.3.x"
do_not_use_as: [regulated_record]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## CTMS — Veeva Vault CTMS (24R3 / 25R1 release line)

**Document Number:** DRY-URS-CTMS-001 | **Version:** 1.0 | **Effective Date:** 2026-04-26 *(synthetic)*
**Site:** Dryad Pharma a.s., Clinical Operations, Brno, Czech Republic *(fictional)*
**System Owner:** Director, Clinical Operations IT | **Process Owner:** VP Clinical Operations
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS; vendor handles infrastructure; site validates configuration)
**Project Mode:** Configuration project on commercial software product **Veeva Vault CTMS (24R3 / 25R1 release line)** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a)–(k), .30, .50, .70, .100, .200, .300; 21 CFR Part 312 (IND + Form FDA 1572 per § 312.53(c)); 21 CFR Part 314 (NDA); 21 CFR Part 50 (informed consent); 21 CFR Part 56 (IRB); ICH E6(R3) GCP (Step 4, adopted 6 January 2025); ICH E8(R1); ICH E2A (safety reporting); EU CTR Reg. 536/2014 + CTIS Sponsor Handbook; FDA *Computerized Systems Used in Clinical Investigations* (May 2007); FDA BIMO Inspection Manual 7348.809 (updated 4 April 2025); EMA Q&A on Annex 11; ISO 14155:2020 (where the trial is a medical-device clinical investigation); BfArM + Paul-Ehrlich-Institut (DE) and AGES PharmMed (AT) national CTIS gateways; Swissmedic (CH).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Clinical Operations IT) | _____________ | _____________ | _____ |
| Reviewer (CRA Lead) | _____________ | _____________ | _____ |
| Reviewer (Vendor Assurance — Veeva relationship owner) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs — CTIS owner) | _____________ | _____________ | _____ |
| Reviewer (Pharmacovigilance Lead) | _____________ | _____________ | _____ |
| Reviewer (Data Protection Officer) | _____________ | _____________ | _____ |
| Approver (VP Clinical Operations) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | **Authored to Tier T4 (CTMS-class mission-critical clinical-operations system; 170-req target; spans protocol + country/site activation + investigator + delegation log + monitoring + RBM + SAE tracking + payments forecasting + vendor management + eTMF cross-link + DSMB tracking + protocol-deviation tracking + CTIS submissions + inspection-readiness).** Added 27 new §5 sub-sections covering protocol + amendment management, country/site activation tracking (regulatory + IRB/EC + contracts), investigator + 1572 + delegation-log + training, subject recruitment forecasting, monitoring visit plans + reports, RBM risk indicators, issue + action items + CAPA on trial-level deviations, drug-supply forecast + reconciliation, investigator-payment tracking, budget + forecasting, vendor management (CRO + central lab + imaging), eTMF integration, safety-reporting tracking (SAE → SUSAR timelines), DSMB / IDMC tracking, protocol-deviation tracking, FDA BIMO + EMA inspection-readiness, document tracking (IB / Protocol / ICF versions), site closeout + final study report tracking, multi-language site activation, time-zone-aware visit / payment calc, GDPR Arts. 22 + 35 DPIA, EU CTR / CTIS sponsor obligations, and 14 new top-level risks. **NOTE:** v1.0 had an FS that referenced URS IDs (URS-STDY-/URS-SITE-/URS-MON-/URS-MIL-/URS-PAY-) absent from the URS — v1.2 introduces those IDs canonically and re-paired FS v1.2 reconciles fully. |

## Definitions

| Term | Definition |
|---|---|
| CTMS | Clinical Trial Management System |
| Vault CTMS | Veeva Vault CTMS Release line 24R3 / 25R1 |
| Study | A clinical-trial protocol under sponsor management |
| Country | A country in which the study is conducted; bound to a single national CA |
| Site | Investigative site participating in a study (one investigator, one address) |
| Site Activation | Lifecycle state in which a site is permitted to enrol subjects after regulatory + ICF + training readiness |
| Investigator (PI / Sub-I) | Principal Investigator / Sub-Investigator listed on Form FDA 1572 / EU CTR investigator file |
| 1572 | FDA Form 1572 — Statement of Investigator per 21 CFR § 312.53(c) (IND-regulated trials) |
| Delegation Log | Site-level record of which study tasks are delegated by the PI to sub-investigators / coordinators |
| Monitoring Visit | A protocol-required visit by a CRA / monitor (initiation / interim / close-out) |
| MVR | Monitoring Visit Report |
| KPI | Key Performance Indicator (study-level / site-level) |
| RBM | Risk-Based Monitoring (ICH E6(R3) § 3.10) |
| RBQM | Risk-Based Quality Management (ICH E6(R3) § 3) |
| Critical-to-Quality (CtQ) Factor | Per ICH E8(R1) — factor whose integrity is essential to participant rights / safety and trial-result reliability |
| Protocol Deviation | Departure from the approved protocol |
| Important Protocol Deviation (IPD) | Deviation significantly affecting subject rights / safety or trial-result reliability |
| AE / SAE / SUSAR | Adverse Event / Serious Adverse Event / Suspected Unexpected Serious Adverse Reaction |
| DSMB / IDMC | Data Safety Monitoring Board / Independent Data Monitoring Committee |
| IB | Investigator's Brochure |
| ICF | Informed Consent Form (per protocol + per site) |
| eTMF | Electronic Trial Master File (TMF Reference Model v3.3.x — Veeva Vault eTMF in this scope) |
| EDC | Electronic Data Capture (Medidata Rave per Marigold EDC URS) |
| RTSM / IRT / IXRS | Randomization and Trial Supply Management / Interactive Response Technology |
| CTIS | EU Clinical Trials Information System (EU CTR 536/2014 submission portal) |
| BIMO | FDA Bioresearch Monitoring program |
| BfArM / PEI / AGES / Swissmedic | DACH national competent authorities (medicinal + biologicals + medical-devices) |
| CRO | Contract Research Organisation |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate + Complete, Consistent, Enduring, Available |
| DPIA | Data Protection Impact Assessment (GDPR Art. 35) |

## 1. Purpose

Define requirements for the Clinical Trial Management System (CTMS) that Dryad Pharma uses to plan, activate, monitor, and report on clinical-study operations across its sponsored Phase II / III interventional studies in oncology and rare disease, including all DACH and EU country / site management, CRA monitoring, vendor (CRO + central lab + imaging) management, regulatory submissions tracking, and inspection-readiness.

## 2. Scope

**In scope:** Veeva Vault CTMS 24R3 / 25R1 multi-tenant SaaS; configuration of study, country, site, investigator, monitoring-visit, action-item, deviation, milestone, payment, and vendor objects; integrations with Vault eTMF, Medidata Rave EDC (enrolment / status / protocol-deviation feeds), RTSM / IXRS (randomisation status), Argus (SUSAR / SAE-aware site KPIs), eQMS (MasterControl — deviation + CAPA), HR system (CRA assignment), financials (per-site payment push), CTIS sponsor workspace (sponsor obligations); SSO via Okta SAML 2.0 + MFA; vendor-assurance program covering Veeva.

**Out of scope:** subject-level clinical data capture (EDC scope — Marigold EDC URS); ePRO authoring; Veeva-managed infrastructure; eTMF authoring (Marinos eTMF URS); pharmacovigilance case processing (Sirius Argus PV URS).

## 3. System Description

Vault CTMS is the system of record for study-level and site-level operational data: study setup, country / site activation timelines (regulatory milestones, IRB / EC approval, ICF approval, contracts, training), enrolment, monitoring-visit plans and reports, action items, protocol deviations, site KPIs, drug-supply tracking at site level, investigator-payments forecast, vendor management, and operational reporting. Cat 4: Veeva maintains the platform under their published SDLC; site validation focuses on configuration, integrations, and 21 CFR Part 11 controls.

**ICH E6(R3) posture:** CTMS supports the sponsor's Quality-by-Design (QbD) approach — Critical-to-Quality (CtQ) factors identified during protocol design feed monitoring-plan generation; central monitoring + RBM consumes EDC + CTMS data to drive risk-proportionate on-site / remote / centralised monitoring decisions per ICH E6(R3) § 3.10.

## 4. User Roles

| Role | Permissions |
|---|---|
| CRA / Monitor | Plan / log monitoring visits; author MVRs; raise / track action items; raise deviations; cannot approve site activation or MVR for sites they monitor |
| CRA Lead / Sr CRA | Approve MVRs; approve site activation; approve action-item closure; cannot self-perform CRA actions on same site |
| Clinical Operations Manager | Manage study-level setup; monitor KPIs; manage country / site activation timelines |
| Regulatory Affairs (CTIS owner) | Manage CTIS submission tracking; manage IB / Protocol / ICF version registers; manage national-CA submissions (BfArM / PEI / AGES / Swissmedic) |
| Medical Monitor | Review safety / deviation data; trigger SAE follow-up tasks |
| Pharmacovigilance Lead | Read access to SUSAR / SAE tracking metadata; track expedited-reporting clock from sponsor-awareness date (regulatory submission via Argus) |
| Vendor / CRO User | Read / write per the contracted scope; restricted views per study and per delegated activity |
| Finance / Payments | Process per-site payments; reconcile against milestone completion |
| Vault Administrator | Configuration; cannot approve operational records |
| DSMB / IDMC Tracker | Track DSMB charter version, meeting schedule, recommendation receipts |
| Auditor / Inspector (BIMO / EMA / BfArM / Swissmedic) | Read-only across study, audit trails, configuration, change history; export-only |
| Data Protection Officer (GDPR) | Read access to data-subject identifier records; controls subject-erasure (Art. 17) triage |

Separation of duties (SoD), enforced at the user level by Vault permission sets + Okta IdP:

- CRA monitoring a site ≠ CRA Lead approving the MVR for the same site
- Configuration Author ≠ Configuration Approver
- Site Activation Author ≠ Site Activation Approver
- Payment Initiator ≠ Payment Approver
- Deviation Author ≠ Deviation Approver
- CTIS Submission Author ≠ CTIS Submission Approver
- DSMB Tracker ≠ any operational study role

## 5. User Requirements

### 5.1 Vendor / Platform Assurance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-01 | H | R1 | Veeva shall be qualified as a critical SaaS vendor with documented vendor-assurance evidence: SOC 2 Type II, ISO 27001:2022, GDPR DPA + sub-processor list, customer-shared CSV summary, vendor SDLC summary. |
| URS-VND-02 | H | R1 | Vendor releases (Vault CTMS 24R3 / 25R1 release train) shall be impact-assessed within 14 days of release-notes publication; configuration-affecting changes trigger re-validation per affected studies. |
| URS-VND-03 | M | R2 | Vendor sub-processors used in Dryad's data path shall be enumerated in the DPA and reviewed annually. |
| URS-VND-04 | H | R1 | Vendor incident notifications shall reach Dryad within the contracted SLA window (≤ 24 h for confirmed data breaches per GDPR Art. 33 propagation). |

### 5.2 Protocol and Protocol-Amendment Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PROT-01 | H | R1 | Each protocol shall be tracked as a Vault Protocol record with protocol-id, version, version-effective-date, IB version reference, sponsor approval signatures, and regulatory submission status per country. |
| URS-PROT-02 | H | R1 | Protocol amendments shall be tracked as Vault Amendment records linked to the parent Protocol, with amendment-id, version, effective-date, impact category {ADMINISTRATIVE, SUBSTANTIAL}, change summary, and propagation status to EDC / RTSM / eTMF. |
| URS-PROT-03 | H | R1 | Substantial-modification amendments per EU CTR Art. 16 shall trigger a CTIS substantial-modification submission workflow (URS-CTIS-*); status tracked from draft → submitted → CA decision. |
| URS-PROT-04 | M | R2 | Protocol-amendment downstream tasks (re-consent triggers, EDC re-build, monitoring-plan update) shall be auto-generated from the amendment impact assessment. |

### 5.3 Country / Site Activation Tracking

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CTRY-01 | H | R1 | Each country participating in a study shall be tracked as a Vault Country record with country-id, national CA (BfArM / PEI / AGES / Swissmedic / FDA / others), submission status (initial, substantial-modification, end-of-trial), planned activation date, actual activation date. |
| URS-CTRY-02 | H | R1 | Country-level regulatory milestones shall be tracked with planned / actual dates and gating sequence (CA submission → CA decision → IRB / EC approval → first site activation). |
| URS-SITE-01 | H | R1 | Each site shall be tracked as a Vault Site record with site-id, country, principal investigator, address, IRB / EC oversight body, lifecycle state ∈ {IDENTIFIED, QUALIFIED, INITIATED, ENROLLING, ENROLLMENT_CLOSED, FOLLOW_UP, CLOSED}. |
| URS-SITE-02 | H | R1 | Site activation shall be gated by a required-document checklist: signed 1572 (IND trials) or equivalent EU investigator file; investigator CV; financial-disclosure forms; IRB / EC approval letter; current ICF version; site-staff training records; signed Clinical Trial Agreement (CTA); insurance coverage evidence; site-initiation visit (SIV) report. |
| URS-SITE-03 | H | R1 | Activation shall require CRA Lead signature; activation is gated on completion of the checklist (URS-SITE-02) and on country-level CA decision (URS-CTRY-02). |
| URS-SITE-04 | H | R1 | Site lifecycle state transitions shall be e-signed per § 11.50 + § 11.70; the audit trail captures prior + new state, actor, timestamp, reason. |
| URS-SITE-05 | M | R2 | Site contacts (Investigator, sub-investigators, coordinator, pharmacist) shall be tracked with role, contact info (encrypted at rest), and start / end dates. |
| URS-SITE-06 | H | R1 | Site enrolment plan vs actual enrolment shall be visible at country and study aggregates; forecasting projects projected enrolment completion. |

### 5.4 Investigator and Delegation Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INV-01 | H | R1 | Each investigator shall be tracked with investigator-id, name, credentials, CV-version, financial-disclosure status, conflict-of-interest status, training records, and per-study assignment. |
| URS-INV-02 | H | R1 | Form FDA 1572 (IND-regulated trials) shall be tracked per investigator per study with version, effective date, signed-by-PI date, sub-investigator list per § 312.53(c)(1)(viii), prior-1572 archival on re-signing per OMB-expiration / new-protocol-amendment / new-sub-I rules. |
| URS-INV-03 | H | R1 | Site Delegation Log shall be tracked per site per study, listing which study tasks (informed consent, dose preparation, data entry, AE assessment, sample collection, etc.) are delegated by the PI to which named staff, with delegation start / end dates and signatures. |
| URS-INV-04 | M | R2 | Investigator training currency shall be checked at site-activation and at periodic-review; expired training shall block site activation and shall raise a system alert at study level. |
| URS-INV-05 | M | R2 | Investigator turnover (PI change mid-study) shall trigger a controlled-transition workflow: new 1572, IRB notification, sub-I re-delegation, ICF re-approval (if applicable). |

### 5.5 Subject Recruitment Tracking and Forecasting

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REC-01 | H | R1 | Per-site enrolment plan (planned screen / randomise / complete numbers + cadence) shall be captured; actual enrolment ingested daily from EDC + RTSM. |
| URS-REC-02 | H | R1 | Forecasting shall project FPI / LPI / LPLV given current enrolment velocity and dropout rate; the projection shall update daily. |
| URS-REC-03 | M | R2 | Recruitment KPIs (screen-failure rate, screen-to-randomise ratio, time-to-FPI, time-to-LPI) shall feed the central monitoring dashboard. |
| URS-REC-04 | M | R2 | Recruitment exception alerts (site below plan by > 50% for > 30 days; country recruitment stalled) shall raise action items. |

### 5.6 Monitoring Visit Plan and Reports

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MV-01 | H | R1 | Monitoring-visit plan shall be configurable per study per ICH E6(R3) § 3.10 RBM: visit types {SIV, IMV, MMV, COV, REMOTE_MV}; visit cadence per site risk; on-site vs remote split per RBM plan. |
| URS-MV-02 | H | R1 | Monitoring Visit Reports (MVRs) shall record: visit-id, type, site-id, dates (planned / actual / scheduled-by), attendees, findings, action items, follow-up SLA, deviations identified, SAE follow-up, protocol-deviation count, signature blocks per ICH E6(R3) § 4. |
| URS-MV-03 | H | R1 | MVR approval shall require CRA Lead signature; signed MVRs immutable; un-signing requires Director Clinical Ops IT approval per unlock workflow. |
| URS-MV-04 | H | R1 | Action items from MVRs shall track owner, due date, status, escalation rule, evidence-of-closure; overdue action items shall escalate per configured rules (default: T+0 owner; T+7 CRA Lead; T+14 Clinical Ops Manager). |
| URS-MV-05 | H | R1 | MVR due-date enforcement shall trigger system alerts at T-7 / T-0 / T+7 / T+14 against the per-study SLA; missed-MVR streak per site shall raise an RBM risk indicator. |
| URS-MV-06 | M | R2 | MVR templates shall be versioned at study level; mid-study template changes follow change-control. |

### 5.7 Source-Data Verification (SDV) Sample Plan

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SDV-01 | H | R1 | The per-study RBM plan shall define the SDV sampling strategy: CtQ-tagged critical fields 100%; non-critical fields risk-based per CDISC controlled-terminology. |
| URS-SDV-02 | H | R1 | CTMS shall track SDV completion at field / form / visit / subject / site / study granularity; SDV completion status flows from EDC (Marigold MAR-URS-EDC-001). |
| URS-SDV-03 | M | R2 | SDV exception (fields not yet SDV'd at lock checkpoint) shall surface as RBM KPI at site + study level. |

### 5.8 Risk-Based Monitoring and Risk Indicators

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RBM-01 | H | R1 | The system shall implement a Risk Register per study with risks identified per ICH E6(R3) § 3, categorised, with likelihood / impact / mitigation, owner, status. |
| URS-RBM-02 | H | R1 | Site-risk indicators (enrolment velocity deviation, query-response time, SDV completeness, AE rate, deviation rate, missed-MVR rate, drug-supply variance) shall be computed daily from CTMS + EDC + RTSM + Argus feeds. |
| URS-RBM-03 | H | R1 | Risk threshold breaches shall raise an Action Item routed to the CRA + CRA Lead with mandatory mitigation plan. |
| URS-RBM-04 | M | R2 | RBM dashboards shall be navigable by study, country, site, and indicator; central-monitoring leads receive daily digest. |
| URS-RBM-05 | M | R2 | RBM risk register shall be reviewed at minimum every 4 weeks during active enrolment; review evidence captured. |

### 5.9 Issue Management, Action Items, and CAPA on Trial-Level Deviations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ISS-01 | H | R1 | Issues raised from monitoring, audit, deviation, or risk-indicator sources shall track issue-id, source, severity {LOW, MED, HIGH, CRITICAL}, owner, due date, status, evidence-of-closure. |
| URS-ISS-02 | H | R1 | Action items shall track owner, due date, status, escalation; integration to the eQMS (MasterControl) for trial-level deviations requiring CAPA. |
| URS-ISS-03 | H | R1 | Trial-level deviations classified as CAPA-bearing shall create idempotent records in MasterControl via REST; idempotency keyed on `{study_id, deviation_id}`. |
| URS-ISS-04 | M | R2 | Issue / action-item KPIs (open count, overdue count, mean-time-to-close) shall feed the RBM dashboard. |

### 5.10 Drug Supply Forecast and Reconciliation (IRT Integration)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DRG-01 | H | R1 | Drug-supply tracking shall ingest dispensing data from RTSM / IRT daily; per-site inventory, planned-dispensed, returned, unused, destroyed kit counts maintained. |
| URS-DRG-02 | H | R1 | Drug-supply forecast shall project per-site shortfall risk over the next 4 / 8 / 12 weeks based on enrolment velocity and per-subject dosing schedule. |
| URS-DRG-03 | M | R2 | Forecast under-estimate alerts (projected shortfall < 4 weeks coverage) shall raise an action item to Supply Chain + CRA. |
| URS-DRG-04 | M | R2 | Drug-accountability reconciliation between CTMS, RTSM, and EDC drug-accountability eCRFs shall be tracked; unreconciled discrepancies surface as RBM indicators. |

### 5.11 Investigator Payment Tracking and Forecasting

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PAY-01 | H | R1 | Per-site payment records shall be linked to milestones (site initiation, per-subject enrolment, per-visit completion, close-out) per the per-site CTA; payment schedule auto-generated. |
| URS-PAY-02 | H | R1 | Payment requests shall be pushed to the Financials system idempotently on milestone-id; duplicate pushes shall be rejected by the Financials side; CTMS shall not silently retry a successful push. |
| URS-PAY-03 | H | R1 | Payment overpayment guard: payment requests against milestones already paid in full shall be blocked by CTMS before submission to Financials. |
| URS-PAY-04 | M | R2 | Payment forecast (current quarter + next 2 quarters) shall be derivable per study, country, site. |
| URS-PAY-05 | M | R2 | Site payment history shall be auditable and exportable per site per study. |

### 5.12 Budget and Forecasting

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BUD-01 | M | R2 | Per-study budget shall be tracked at the line-item level (sites, monitoring visits, central labs, imaging, drug supply, vendors); actuals vs budget computed monthly. |
| URS-BUD-02 | M | R2 | Cost-overrun alerts (line-item > 110% of plan) shall raise action items to the Clinical Operations Manager. |

### 5.13 Vendor Management (CRO + Central Lab + Imaging + ePRO + LIMS)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VEN-01 | H | R1 | Each contracted vendor (CRO, central lab, imaging core lab, ePRO provider, LIMS) shall be tracked with vendor-id, type, scope, contract version, contract effective dates, performance KPIs. |
| URS-VEN-02 | H | R1 | Vendor data-feed reconciliation status shall be tracked (e.g., daily CRO data ingest, central-lab data freshness, imaging-read backlog); reconciliation failure shall raise an action item. |
| URS-VEN-03 | M | R2 | Vendor KPIs (data-freshness, on-time-delivery, query-response time) shall be reportable; quarterly vendor performance review evidence captured. |
| URS-VEN-04 | M | R2 | Vendor change of scope (Change Order) shall be tracked with signed amendment to contract; budget impact reflected in URS-BUD-*. |

### 5.14 eTMF Integration (TMF Reference Model)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ETMF-01 | H | R1 | Site-level documents (CV, 1572, financial disclosure, IRB approval, ICF, training records, CTA, insurance, SIV report) shall be cross-linked to the Veeva Vault eTMF record per TMF RM v3.3.x artefact mapping. |
| URS-ETMF-02 | H | R1 | Expected Document List (EDL) per TMF RM shall be checked at site activation and at milestone gates; EDL gaps shall block the gated transition. |
| URS-ETMF-03 | M | R2 | Document version tracking (IB, Protocol, ICF) shall align CTMS records with eTMF version index; mismatches raise action items. |
| URS-ETMF-04 | M | R2 | Inspection-readiness score (per Veeva eTMF inspection-readiness scoring) shall be visible at study level. |

### 5.15 Safety Reporting Tracking (SAE → SUSAR Timelines)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SAF-01 | H | R1 | The system shall track SAE / SUSAR cases at the operational metadata level (case-id, subject-id, site-id, country, sponsor-awareness-date, regulatory-clock-state); the regulatory submission of record is in Argus. |
| URS-SAF-02 | H | R1 | SUSAR expedited-reporting clock (per ICH E2A + EU CTR Art. 42): fatal / life-threatening → 7 calendar days from sponsor awareness + 8-day follow-up; non-fatal / non-LT → 15 calendar days. The CTMS shall display the clock state and shall not be the regulatory clock owner. |
| URS-SAF-03 | H | R1 | Missed-deadline alerts: clock T-2 / T-1 / T-0 / T+1 shall raise alerts to PV Lead + Director Clinical Ops; missed deadlines (T+1 unresolved) shall be flagged as quality events for CAPA. |
| URS-SAF-04 | M | R2 | Per-site SAE / SUSAR rate shall feed RBM indicators. |
| URS-SAF-05 | M | R2 | DSUR (Development Safety Update Report) and ASR (Annual Safety Report per EU CTR) preparation tasks shall be tracked per study per year. |

### 5.16 Audit Trail and 21 CFR Part 11 — Sub-section-Specific Bindings

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Time-stamped, secure audit trail covering all object edits, signatures, configuration changes, lifecycle-state transitions, vendor / contract record changes, action-item state changes per § 11.10(e). |
| URS-AUD-02 | H | R1 | Audit trail append-only at the platform level (vendor-managed); reviewable in-system and exportable as CSV / PDF. |
| URS-AUD-03 | H | R1 | Audit-trail review by Director Clinical Operations IT monthly; review evidence retained. |
| URS-AUD-04 | H | R1 | Retention ≥ 25 years post-trial completion per EU CTR + FDA combined max; per-study extension where paediatric / oncology / EU CTR Art. 58 apply. |
| URS-AUD-05 | H | R1 | Audit-trail disablement detection: heartbeat checks every 5 min; gap > 15 min shall set system to READ_ONLY and raise P1 alert (mitigates known BIMO finding pattern). |
| URS-PART11-01 | H | R1 | § 11.10(a) — Procedures and controls protecting electronic-record validity: SOP suite in effect at sponsor + sites. |
| URS-PART11-02 | H | R1 | § 11.10(b) — Generating accurate and complete copies: object record PDFs and report exports reproducible with checksum verification. |
| URS-PART11-03 | H | R1 | § 11.10(c) — Protection of records throughout retention period per URS-AUD-04. |
| URS-PART11-04 | H | R1 | § 11.10(d) — Limiting access via Okta + MFA + role-based per URS-SEC-*. |
| URS-PART11-05 | H | R1 | § 11.10(e) — Operational audit trail per URS-AUD-01..05. |
| URS-PART11-06 | H | R1 | § 11.10(g) — Authority checks at signature / activation / payment-submission / CTIS-submission actions. |
| URS-PART11-07 | H | R1 | § 11.10(k) — System operation manuals + change control; vendor manuals version-controlled; user training gated on current manual version. |
| URS-PART11-08 | H | R1 | § 11.30 — Open systems: CTIS / national-CA / Financials gateways treated as controlled bridges with TLS 1.3 + mutual auth + checksum reconciliation. |
| URS-PART11-09 | H | R1 | § 11.50 — Signature manifestations include printed name, UTC timestamp, meaning string. |
| URS-PART11-10 | H | R1 | § 11.70 — Signature / record linking: signatures cryptographically bound to record-state. |
| URS-PART11-11 | H | R1 | § 11.100 — User-id uniqueness; never reassigned. |
| URS-PART11-12 | H | R1 | § 11.200 — Re-authentication required at every signature event. |
| URS-PART11-13 | H | R1 | § 11.300 — Password / credential controls enforced via Okta. |

### 5.17 Integrations — EDC (Medidata Rave) and RTSM

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-EDC-01 | H | R1 | Enrolment / status feeds from Medidata Rave EDC shall be ingested via Veeva Vault Connect / REST daily; subject-level state aggregated to site / country / study. |
| URS-INT-EDC-02 | H | R1 | Protocol-deviation feed from Rave (Clinical Operations–EDC Connection per Vault 24R3) shall surface in CTMS deviation register with `edc_id` link enabling navigation to the EDC source record. |
| URS-INT-EDC-03 | M | R2 | Query KPIs (open count, aging, % overdue) from Rave shall populate site-level KPIs. |
| URS-INT-RTSM-01 | H | R1 | Randomisation-status feeds from RTSM shall be ingested daily; mismatches with EDC enrolment raise reconciliation queries. |
| URS-INT-RTSM-02 | M | R2 | Drug-accountability data from RTSM feeds URS-DRG-* drug-supply tracking. |

### 5.18 Integrations — Argus (Pharmacovigilance)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-ARGUS-01 | H | R1 | SUSAR / SAE metadata (case-id, sponsor-awareness date, regulatory clock state) shall be ingested from Argus daily for the operational tracking layer (URS-SAF-*). |
| URS-INT-ARGUS-02 | H | R1 | The CTMS shall NOT own the regulatory submission clock; Argus is the regulatory record-of-truth. |

### 5.19 Integrations — eQMS (MasterControl)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-EQMS-01 | H | R1 | Trial-level deviations classified as CAPA-bearing shall create idempotent records in MasterControl via REST; idempotency key `{study_id, deviation_id}`; success / failure status returned. |
| URS-INT-EQMS-02 | M | R2 | CAPA closure status shall flow back to CTMS for issue-management visibility. |

### 5.20 Integrations — eTMF (Veeva Vault eTMF)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-ETMF-01 | H | R1 | Cross-link to Vault eTMF for regulatory / ICF / site-document artefacts via native Veeva Vault Connect. |
| URS-INT-ETMF-02 | M | R2 | eTMF inspection-readiness state shall surface in CTMS via Vault Connect. |

### 5.21 Integrations — SSO (Okta)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-SSO-01 | H | R1 | Authentication via Okta SAML 2.0 + MFA; Vault local accounts disabled in production. |
| URS-INT-SSO-02 | M | R2 | SCIM 2.0 provisioning from HR / Okta to Vault; deprovisioning on HR termination ≤ 24 h. |

### 5.22 Integrations — Financials

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-FIN-01 | H | R1 | Per-site payment push to Financials shall be idempotent on `{study_id, site_id, milestone_id, payment_id}`; success / failure / retry status tracked in CTMS. |
| URS-INT-FIN-02 | M | R2 | Payment reconciliation report (CTMS-initiated vs Financials-confirmed) shall be produced monthly. |

### 5.23 Integrations — HR (CRA Assignment)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-HR-01 | M | R2 | CRA assignment + role changes shall sync from HR; termination events trigger CTMS access deprovisioning ≤ 24 h. |

### 5.24 DSMB / IDMC Tracking

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DSMB-01 | H | R1 | DSMB charter version + meeting schedule + recommendation receipts shall be tracked per study; DSMB charter version drift between study sites shall be flagged. |
| URS-DSMB-02 | H | R1 | DSMB meeting outputs (recommendation: continue / modify / stop) shall be tracked with signed-by date, charter-version, distribution; downstream actions (e.g., protocol amendment per FS-AMD-*) auto-generated as action items. |
| URS-DSMB-03 | M | R2 | Interim-analysis schedule per DSMB charter shall be tracked; missed milestones raise alerts. |

### 5.25 Protocol-Deviation Tracking

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEV-01 | H | R1 | Protocol deviations shall be captured per ICH E6(R3) — Important Protocol Deviation (IPD) vs Non-Important; deviation-id, subject-id, site-id, category, date-occurred, date-identified, description, root-cause, corrective-action, importance, CTIS-reportable flag. |
| URS-DEV-02 | H | R1 | IPDs shall be reviewed by Medical Monitor + CRA Lead; CTIS-reportable IPDs shall be flagged for inclusion in the next CTIS substantial-modification or ASR. |
| URS-DEV-03 | H | R1 | Per-protocol-deviation feed from EDC (Vault 24R3 Clinical Operations-EDC Connection) shall surface in CTMS deviation register; CTMS-originated deviations also tracked. |
| URS-DEV-04 | M | R2 | Per-site deviation rate, IPD rate shall be RBM indicators. |

### 5.26 FDA BIMO + EMA + DACH Inspection-Readiness

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BIMO-01 | H | R1 | Per FDA BIMO Inspection Manual 7348.809 (updated 4 April 2025) and EMA / BfArM / Swissmedic / AGES inspection expectations, the system shall produce on-demand: site-activation evidence; investigator + delegation records; MVR history; deviation register; SAE tracking; vendor records; CTIS submission history; budget vs actuals. |
| URS-BIMO-02 | H | R1 | Inspector / auditor role shall be read-only + export-only; no edit / no signature / no payment-submission affordances. |
| URS-BIMO-03 | M | R2 | Inspection-readiness "bundle" export shall be generable in ≤ 60 min wall-clock for a 100-site multi-country study. |
| URS-BIMO-04 | H | R1 | Late safety-reporting findings (per FY2024 BIMO sponsor inspection trend) shall be pre-empted by URS-SAF-03 alert chain. |

### 5.27 Document Tracking (Investigator's Brochure, Protocol, ICF Versions)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DOC-01 | H | R1 | Investigator's Brochure (IB) versions per study tracked with version, effective-date, IRB / EC approval per site, distribution log. |
| URS-DOC-02 | H | R1 | Protocol versions per study tracked (parent + amendments) with version, effective-date, CTIS submission status. |
| URS-DOC-03 | H | R1 | ICF versions per site tracked with version, language, IRB / EC approval date, deployment-to-site date, current ICF flag. |
| URS-DOC-04 | M | R2 | Subjects under ICF version older than current shall be flagged for re-consent (cross-reference to Marigold EDC URS-CONSENT-*). |

### 5.28 Site Closeout and Final Study Report Tracking

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CLO-01 | H | R1 | Site closeout shall be gated by COV (close-out visit) MVR signature; all queries closed; SDV complete; drug-supply reconciled; site-payment final; site-document EDL gate. |
| URS-CLO-02 | H | R1 | Final Study Report (CSR) tracking shall capture CSR version, statistical analysis status, CSR signature schedule, distribution to CTIS. |
| URS-CLO-03 | M | R2 | End-of-trial CTIS notification per EU CTR Art. 37 shall be tracked as a workflow item. |

### 5.29 Multi-Language Site Activation and Time-Zone-Aware Visit / Payment Calc

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INTL-01 | M | R2 | Site-facing communications + EDL / ICF labels shall be localisable per site language (de-DE, de-AT, de-CH, fr-FR, en-GB, en-US, es-ES, it-IT, pl-PL, cs-CZ); underlying object semantics unchanged. |
| URS-INTL-02 | M | R2 | Visit-window enforcement + payment-due-date calculation shall be time-zone-aware: subject / site local time-zone shall be the basis; canonical storage in UTC. |
| URS-INTL-03 | M | R2 | Locale-specific date / number / currency display shall not corrupt stored canonical values. |

### 5.30 Performance / Availability / Backup

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | Object open / list response ≤ 3 s at the 95th percentile under nominal load (≤ 300 concurrent users). |
| URS-PERF-02 | M | R2 | Site-list export for a 100-site study ≤ 10 min wall-clock. |
| URS-AV-01 | H | R1 | Availability per Veeva SLA (99.5% monthly target); deviations escalated. |
| URS-BAK-01 | H | R1 | Vendor-managed backup; RPO ≤ 4 h, RTO ≤ 24 h per SLA. |
| URS-BAK-02 | M | R2 | DR drill annual, vendor-evidenced. |

### 5.31 Security and Data Protection (GDPR)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | All access via Okta + MFA; session timeout ≤ 30 min idle. |
| URS-SEC-02 | H | R1 | Per-study + per-country access restrictions; access reviewed at FPI, every 90 days during enrolment, and at site closeout. |
| URS-SEC-03 | H | R1 | Investigator contact data treated as personal data under GDPR Art. 6; encryption at rest + in transit per GDPR Art. 32. |
| URS-SEC-04 | H | R1 | GDPR Art. 22 — no automated decision-making against the data subject (e.g., investigator scoring driving exclusion) shall be implemented; algorithmic outputs surface as advisory to human reviewers. |
| URS-SEC-05 | H | R1 | GDPR Art. 35 — DPIA per study covering investigator / site-staff / vendor personal data shall be completed before FPI. |
| URS-SEC-06 | M | R2 | GDPR Art. 17 erasure requests from investigators / site staff shall be triaged against EU CTR + ICH-E6(R3) retention obligations; decisions filed. |

### 5.32 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | LMS-recorded role-specific training + protocol-specific training; expired training blocks access. |
| URS-PR-01 | H | R1 | Annual periodic review (platform); per-study at amendments and at lock; signed by Director Clinical Operations IT + Head of QA. |
| URS-PR-02 | M | R2 | Periodic review confirms: audit-trail completeness; vendor-release impact assessments; integration health (EDC / RTSM / Argus / eQMS / eTMF / Financials feeds); SAE-tracking-clock health. |

### 5.33 CTIS Submission Tracking and Sponsor Obligations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CTIS-01 | H | R1 | CTIS submission lifecycle (initial, substantial modification, ASR, end-of-trial, summary of results) shall be tracked per study; status from draft → submitted → CA decision → published. |
| URS-CTIS-02 | H | R1 | Sponsor obligation alerts: ASR due (annually), substantial-modification due (within Member-State assessment cadence), end-of-trial summary due (within EU CTR Art. 37 timelines), summary of results due (within EU CTR Art. 37 timelines). |
| URS-CTIS-03 | M | R2 | Per-country national-CA submission tracking for DE (BfArM / PEI), AT (AGES), CH (Swissmedic) where national obligations remain. |
| URS-CTIS-04 | M | R2 | CTIS resubmission tracking: from 1 January 2026 no invoice for CTR safety / ethics committee assessment for technical-issue resubmissions where content unchanged — status flag captured. |

### 5.34 Monitoring-Plan Version Control

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MP-01 | H | R1 | Each study's monitoring plan (RBM-aligned) shall be version-controlled with effective-date, approver, and amendment-linkage; mid-study amendment may trigger monitoring-plan update. |
| URS-MP-02 | M | R2 | Active monitoring-plan version shall drive MV visit-type cadence per FS-MV-01 and SDV strategy per FS-SDV-01. |

### 5.35 Country-Level Pharmacy / Drug-Import Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-IMP-01 | H | R1 | Per-country IMP (Investigational Medicinal Product) import licence / customs documentation shall be tracked; expiry triggers an alert at T-90 / T-60 / T-30 days. |
| URS-IMP-02 | M | R2 | Country-specific labelling / leaflet versions (DE / AT / CH language variants) shall be tracked with version + effective dates. |

### 5.36 Study Startup KPIs and First-Patient-In Tracking

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SS-01 | H | R1 | Study-startup KPIs (Time-to-CA-Submission, Time-to-First-Approval, Time-to-First-Site-Activation, Time-to-FPI) shall be computed per study and per country; benchmarked against historical Dryad average + industry benchmark. |
| URS-SS-02 | M | R2 | First-Patient-In (FPI) event per country and per study shall be tracked with date, site, subject screening / randomisation indicator; CTIS notification trigger per EU CTR. |

### 5.37 Sponsor Audit and Quality-Event Tracking

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUDIT-01 | H | R1 | Internal sponsor audits (site audit, vendor audit, system audit) shall be tracked as Audit objects with audit-id, scope, auditor-id, date, findings, CAPAs (via FS-ISS-03). |
| URS-AUDIT-02 | M | R2 | Audit findings categorised by severity; critical findings raise immediate Action Items routed to study-level QA. |

### 5.38 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is SAML 2.0 via Entra ID with SCIM lifecycle provisioning; conditional-access policy `Clinical-Sensitive Conditional Access (FIDO2 phishing-resistant MFA + sponsor-tenant isolation)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with Oracle RMAN for the CTMS Oracle backend; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 25 y per ICH E6(R3) per the consuming-record schedule. |

### 5.39 Cross-System Integration — Helios audit-trail handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HEL-01 | H | R1 | CTMS shall publish audit-trail events (Study setup, site activation, monitoring visit, and IP-accountability events) to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract (JSON Lines, schema-registry pinned, Kafka topic `helios.ingest.dryad.ctms.v1`) within 5 minutes of event capture; 21 CFR § 11.10(e) audit-trail completeness shall be preserved end-to-end so that no event class is lost at the boundary. |
| URS-XINT-HEL-02 | H | R1 | Pre-handover audit-trail retention on the CTMS side shall be ≥ 25 y regardless of Helios availability; once Helios acknowledges ingest (per-message ack with idempotency key), Helios is the system-of-record for review and the CTMS local copy serves as the durability backstop until the local retention floor expires. |

### 5.40 Cross-System Integration — LMS competence handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-LMS-01 | H | R1 | CTMS site-activation gating shall include an LMS-competence check (curriculum `CTMS-<role>-<study_id>`); non-current users shall be blocked from site assignment with the lapse surfaced on the study-activation dashboard. |

## 6. Acceptance Criteria

The platform-level configuration enters validated use when **CS, RA, IQ** (vendor-shared), **OQ** (signature, audit trail, configuration, lifecycle gates, RBM dashboards, integration feeds, CTIS workflow, BIMO export, DSMB tracking, payment-idempotency, audit-trail watchdog), **PQ** (representative study setup → country activation → site activation → enrolment → monitoring visits → MVR signature → deviation tracking → SAE tracking → CTIS submission → site closeout → CSR) approved and executed; vendor-assurance evidence reviewed; **VSR** approved by Director Clinical Operations IT + Head of QA; **RTM** demonstrates 100% URS-ID coverage.

## 7. Constraints

- Vendor releases (Vault CTMS quarterly release train 24R3 / 25R1) not under site change control.
- CTIS submission to EMA performed by Regulatory Affairs through the CTIS sponsor workspace — CTMS holds the tracking metadata, not the submission system itself.
- Argus is the regulatory submitter for SUSARs; CTMS holds operational tracking.
- DSMB recommendation is governed by per-study DSMB charter; CTMS holds the tracking metadata.
- Veeva 24R3 Clinical Operations–EDC Connection requires Medidata Rave on a compatible release.

## 8. Assumptions

- EDC (Medidata Rave per Marigold MAR-URS-EDC-001), RTSM, eTMF (Veeva Vault eTMF), eQMS (MasterControl), Argus, Financials, Okta, HR are themselves validated.
- Per-study DSMB charters, RBM plans, monitoring plans, DPIAs are in place before FPI.
- CTIS sponsor workspace is operated by Dryad's Regulatory Affairs function.

## 9. References

### Jurisdiction — US (FDA)

- 21 CFR Part 11 §§ .10(a)–(k), .30, .50, .70, .100, .200, .300
- 21 CFR Part 312 — IND Applications (Form FDA 1572 per § 312.53(c))
- 21 CFR Part 314 — NDA Applications
- 21 CFR Parts 50 + 56 — Informed Consent + IRB
- FDA *Computerized Systems Used in Clinical Investigations* (May 2007)
- FDA *Establishment and Operation of Clinical Trial Data Monitoring Committees* (current + 2024 draft update)
- FDA BIMO Inspection Manual 7348.809 (updated 4 April 2025)
- FDA *Conducting Remote Regulatory Assessments — Q&A* (June 2025 final)

### Jurisdiction — EU (EMA / European Commission)

- EU CTR Regulation 536/2014 + CTIS Sponsor Handbook
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EMA Q&A on Annex 11
- GDPR Regulation (EU) 2016/679 — Arts. 6, 17, 22, 32, 33, 35
- EU CTR Art. 16 (Substantial Modifications) + Art. 37 (End of Trial) + Art. 42 (SUSAR reporting) + Art. 58 (Retention)

### Jurisdiction — International (ICH)

- ICH E6(R3) GCP (Step 4, adopted 6 January 2025)
- ICH E8(R1) General Considerations for Clinical Studies (Step 4, October 2021)
- ICH E9(R1) Estimands Addendum (Step 4, November 2019)
- ICH E2A Clinical Safety Data
- ICH E2B(R3) Electronic Transmission of Individual Case Safety Reports
- ICH M11 Clinical Electronic Structured Harmonised Protocol (CeSHaRP)

### CDISC / TMF Reference Model

- CDISC Controlled Terminology (per release package, NCI-EVS pinned)
- TMF Reference Model v3.3.x

### Industry Guidance (ISPE / PIC/S / ISO)

- ISPE GAMP 5 (2nd Edition, 2022)
- ISPE GAMP GPG *Computerised Systems in Regulated GCP Environments*
- PIC/S PI 041 — Good Practices for Data Management and Integrity
- ISO/IEC 27001:2022
- ISO 14155:2020 — Clinical Investigation of Medical Devices (for device-arm trials)

### DACH

- BfArM — Federal Institute for Drugs and Medical Devices
- Paul-Ehrlich-Institut (PEI) — biologicals + vaccines
- Swissmedic (CH)
- AGES PharmMed (AT)
- Anlage 7 GMP-Inspektion (DE)
- CTIS — Clinical Trials Information System
- EudraVigilance — pharmacovigilance database

### Vendor

- Veeva — *Vault CTMS 24R3 / 25R1 Release Notes* (vendor portal); Vault CTMS Product Brief
- Veeva — *Vault eTMF Product Brief*; TMF Bot documentation
- Medidata Rave EDC (Marigold MAR-URS-EDC-001 cross-reference)
- Oracle Argus 8.4 (Sirius PV URS cross-reference)

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

