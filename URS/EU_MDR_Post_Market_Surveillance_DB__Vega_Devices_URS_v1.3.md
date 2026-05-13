---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-27; expanded 2026-05-11 (§5 breakout + DACH context + EU MDR Article 87/88/89 coverage); enriched 2026-05-12 (T3 uplift per METHODOLOGY § 2A.13)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed.) Cat 4 SaaS conventions"
  - "21 CFR Part 820 §§ .100, .198; 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU MDR Reg. 2017/745 Arts. 83 (PMS), 84 (PMS Plan), 85 (PMS Report / PSMR), 86 (PSUR), 87 (Reporting of serious incidents), 88 (Trend reporting), 89 (Analysis of FSCAs), 92 (EUDAMED)"
  - "ISO 14971:2019 (Risk Management); ISO/TR 24971:2020; ISO 13485:2016"
  - "MDCG 2019-9 (Summary of safety and clinical performance); MDCG 2022-21 (PSUR guidance); MDCG 2023-3 (vigilance under MDR)"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026)"
  - "BfArM (DE) Medizinprodukterecht-Durchführungsgesetz (MPDG); Swissmedic (CH) MepV/MepKV; AGES PharmMed (AT)"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# User Requirements Specification (URS)

## EU MDR Post-Market Surveillance (PMS) Database — Sparta TrackWise Digital PMS Module

**Document Number:** VGD-URS-PMS-001 | **Version:** 1.0 | **Effective Date:** 2026-04-27 *(synthetic)*
**Site:** Vega Devices GmbH, Post-Market Surveillance, Tuttlingen, Germany *(fictional)*
**System Owner:** Director, Post-Market Surveillance
**Process Owner:** PRRC (Person Responsible for Regulatory Compliance, per EU MDR Article 15)
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Project Mode:** Configuration project on commercial software product **Sparta TrackWise Digital PMS Module** (GAMP 5 Category 4 — Configured Product).
**Notified Body:** TÜV SÜD Product Service GmbH (CE 0123) *(synthetic placeholder)*
**Regulatory Scope:** EU MDR Reg. 2017/745 Articles 83–92 (PMS, PMS Plan, PMS Report, PSUR, Vigilance, Trend Reporting, FSCA Analysis, EUDAMED); 21 CFR Part 820 §§ .100, .198; 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; ISO 14971:2019; ISO 13485:2016; MDCG 2022-21 (PSUR); MDCG 2019-9; BfArM (DE) MPDG; Swissmedic (CH) MepV/MepKV; AGES PharmMed (AT).

> **Note:** Distinct from the medical-device adverse-event / eMDR system (Theia URS — TEA-URS-MDR-001). This URS covers the **PMS / PSUR** authoring + commitment-tracking platform — proactive trending, periodic safety update reports, post-market clinical follow-up linkage, EU MDR Article 87 serious-incident escalation, Article 88 trend reporting, Article 89 FSCA analysis.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Post-Market Surveillance) | _____________ | _____________ | _____ |
| Reviewer (PRRC — EU MDR Art. 15) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Vigilance Manager) | _____________ | _____________ | _____ |
| Reviewer (Clinical Affairs / PMCF Lead) | _____________ | _____________ | _____ |
| Approver (VP Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | §5 broken out into 12 subsections; DACH relocation (Tuttlingen, DE); EU MDR Articles 87/88/89 explicit coverage; BfArM/Swissmedic/AGES added; Notified Body / TÜV SÜD reference; ISO 14971:2019 alignment. |
| 1.2 | 2026-05-12 | (synthetic) | T3 uplift per METHODOLOGY § 2A.13 (100–150 reqs target): added § 5.14 Real-Time PMS Dashboard + KPI engine; § 5.15 Benefit-Risk + PSUR-Risk matrix integration; § 5.16 Health Authority Correspondence + Inspection Readiness; § 5.17 Multi-region notified-body management; § 5.18 Patient + HCP complaint intake channels; § 5.19 Data quality + completeness rules; FDA CSA Feb 2026 citation aligned per METHODOLOGY § 2A.1; MDCG 2023-3 added; PMSR vs PSUR distinction explicit. |

## Definitions

| Term | Definition |
|---|---|
| PMS | Post-Market Surveillance (EU MDR Article 83) |
| PSUR | Periodic Safety Update Report (EU MDR Article 86) |
| PMSR | Post-Market Surveillance Report (EU MDR Article 85, for Class I devices) |
| PMCF | Post-Market Clinical Follow-up |
| PRRC | Person Responsible for Regulatory Compliance (EU MDR Article 15) |
| FSCA | Field Safety Corrective Action (EU MDR Article 89) |
| EUDAMED | European Database on Medical Devices |
| TrackWise Digital | Sparta Systems QMS / vigilance / PMS SaaS platform |
| Serious Incident | EU MDR Art. 2(65) — death, serious deterioration in health, public health threat |
| Trend Reporting | EU MDR Art. 88 — statistically significant increase in expected non-serious incidents |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the EU-MDR-aligned PMS database used to track post-market data (complaints, adverse events, trending), produce PSURs and PMSRs, manage PMCF commitments, and support serious-incident reporting (Art. 87) and FSCA analysis (Art. 89) for Vega Devices' marketed products.

## 2. Scope

**In:** Sparta TrackWise Digital PMS Module multi-tenant SaaS; per-device configuration; SSO via Okta + MFA; integrations with Theia eMDR System (cross-reference for serious incidents), the eQMS (CAPA linkage), Atlas Serialization (sales-volume context for trending), the literature-surveillance feed, EUDAMED (PSUR submission per Art. 92), BfArM national competent authority gateway, Swissmedic national gateway (CH), AGES gateway (AT).

**Out:** vendor infrastructure (Sparta-managed); commercial CRM; clinical-trial AE reporting (covered by Sirius Argus URS); pre-market clinical investigations (covered by Aquila eISF + EDC URSs).

## 3. System Description

The PMS DB is the system of record for proactive PMS — periodic PMS-plan execution per device (Art. 84), PSUR / PSMR authoring (Arts. 85, 86), PMCF commitment tracking, trending across complaint + literature sources, signal management, integration with vigilance reporting (Art. 87), Article 88 trend reporting, and FSCA analysis (Art. 89). Cat 4: Sparta maintains the SDLC; site validates per-device configuration, integration boundaries, and Part 11 controls.

For DACH-deployed devices, the system shall interface with the national competent authority gateways: BfArM (DE) for MPDG-compliant national reporting, Swissmedic (CH) for MepV-compliant reporting, AGES PharmMed (AT) for Austrian national reporting.

## 4. User Roles

| Role | Permissions |
|---|---|
| PMS Specialist | Capture / process PMS data; cannot approve. |
| Trender / Signal Reviewer | Review trends + signals; cannot self-approve. |
| Vigilance Manager | Triage serious incidents per Art. 87; coordinate with eMDR system. |
| PRRC | Approve PSUR + PMS report submission; PMS sign-off per EU MDR Article 86. |
| Submission Operator | Submit PSUR to EUDAMED; submit incident reports to national competent authorities. |
| PMCF Lead | Manage post-market clinical follow-up commitments. |
| PMS Administrator | Configure; cannot approve. |
| Auditor | Read-only. |

Standard SoD; PRRC role distinguished from Approver to satisfy Art. 15 PRRC independence.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` direct GxP impact / `R2` indirect / `R3` none).

### 5.1 Vendor Assurance and Configuration Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-01 | H | R1 | Sparta shall be qualified as a critical SaaS vendor with SOC 2 Type II + ISO 27001 + ISO 13485 evidence on file; annual re-qualification. |
| URS-VND-02 | H | R1 | Sparta release notes shall be reviewed under site change control before promotion to PROD. |
| URS-CFG-01 | H | R1 | Per-device configuration shall follow DRAFT → QC → UAT → PRODUCTION; SoD enforced (Author ≠ Approver). |
| URS-CFG-02 | M | R2 | Configuration changes shall be exportable for inspection and version-controlled. |
| URS-CFG-03 | M | R2 | A configuration-export endpoint shall return the per-device version-stamped configuration in machine-readable JSON for inspector retrieval and offline review. |

### 5.2 PMS Plan Execution (EU MDR Article 84)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAN-01 | H | R1 | Each device shall have a PMS plan per Annex III; review cadence per device-class: Class III + implantables ≥ annual; Class IIa/b per Annex III; Class I ≥ every 5 years or as triggered. |
| URS-PLAN-02 | H | R1 | Execution evidence shall be captured per cycle; deviations from plan shall auto-create eQMS records. |
| URS-PLAN-03 | H | R1 | The PMS plan shall feed the device's technical documentation (EU MDR Annex II) and shall be kept current via the change-control process. |

### 5.3 PSUR / PSMR Authoring and Submission (EU MDR Articles 85, 86)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PSUR-01 | H | R1 | PSUR template per EU MDR Article 86 and MDCG 2022-21 guidance; auto-population from underlying PMS data + sales volumes + complaints + literature. |
| URS-PSUR-02 | H | R1 | Class I PSMR per Article 85 shall be authored per device with retention obligation. |
| URS-PSUR-03 | H | R1 | PSUR approval shall require PRRC re-authenticated electronic signature; PRRC delegation shall be impossible at signature time. |
| URS-PSUR-04 | H | R1 | PSUR cadence per EU MDR Art. 86(1): **Class IIb + Class III + implantable devices** shall produce a PSUR at least **annually**; **Class IIa** devices shall produce a PSUR at least **every 2 years**. **Class I** devices follow the PMSR cadence under Art. 85 instead. EUDAMED submission via Art. 92 PSUR module when live; for Class III + implantables the PSUR is also assessed by the Notified Body. |
| URS-PSUR-05 | M | R2 | PSUR drafts shall be exportable in PDF/A-3 with embedded XML for downstream archival. |

### 5.4 Trending and Signal Management (Article 88 Trend Reporting)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRD-01 | H | R1 | Trending shall be performed per device / per failure-mode / per use-error per ISO 14971:2019; statistical-significance tests per the procedure (Poisson rate-change / CUSUM / EWMA per device-class). |
| URS-TRD-02 | H | R1 | Article 88 trend reporting: when a non-serious incident rate trend reaches statistical significance, an Article 88 report shall be generated and submitted to the competent authority. |
| URS-SIG-01 | H | R1 | Signal-management workflow on trend-positive: confirm signal → investigate → disposition → CAPA / FSCA decision. |
| URS-SIG-02 | H | R1 | Signal closure shall require evidence-backed disposition; auto-close on time-out is prohibited. |

### 5.5 PMCF Commitment Tracking

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PMCF-01 | H | R1 | Per-device PMCF commitments shall be tracked with due-dates; integration with the clinical-study tracking (CTMS where applicable) shall be active. |
| URS-PMCF-02 | M | R2 | PMCF results shall feed PSUR / PSMR generation. |

### 5.6 Serious Incident Reporting Interface (EU MDR Article 87)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INC-01 | H | R1 | Cross-reference linkage to Theia eMDR system shall be maintained for every serious incident. |
| URS-INC-02 | H | R1 | Serious-incident reporting timelines shall be enforced by alert: 15-day standard, 10-day serious public-health threat, 2-day death. |
| URS-INC-03 | H | R1 | The PMS DB shall flag any incident class change (non-serious → serious) and re-trigger reporting timelines. |
| URS-INC-04 | H | R1 | National competent authority routing: DE → BfArM, CH → Swissmedic, AT → AGES PharmMed, plus EUDAMED submission for EU-wide events. |

### 5.7 FSCA Analysis (EU MDR Article 89)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-FSCA-01 | H | R1 | FSCA decisions shall be captured with rationale, scope, communication plan, and competent authority notifications. |
| URS-FSCA-02 | H | R1 | FSN (Field Safety Notice) generation shall use the MDCG-prescribed template per Art. 89. |
| URS-FSCA-03 | M | R2 | FSCA effectiveness shall be tracked post-action with quantitative measure where feasible. |

### 5.8 Audit Trail and Records Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | A contemporaneous, time-stamped audit trail shall capture user, action, old value, new value, reason-for-change for all PMS data operations, PSUR/PSMR approvals, signal-management decisions, FSCA decisions. |
| URS-AUD-02 | H | R1 | The audit trail shall not be editable or deletable; tenant administrators included. |
| URS-AUD-03 | H | R1 | EU MDR retention: ≥ 10 years post-last-marketed; ≥ 15 years for implantables. |
| URS-AUD-04 | M | R2 | Audit-trail review shall be performed weekly by the System Owner and annually by QA. |

### 5.9 21 CFR Part 11 Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a), procedures and controls protecting the validity of electronic records (PSURs, signal records, FSCAs). |
| URS-PART11-02 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via Okta SSO + MFA. |
| URS-PART11-03 | H | R1 | Per § 11.10(e), operational audit trail per § 5.8. |
| URS-PART11-04 | H | R1 | Per § 11.50, electronic signatures shall include signer's printed name, date and time of signing, and meaning of signature. |
| URS-PART11-05 | H | R1 | Per § 11.70, signatures shall be cryptographically linked to the signed record. |
| URS-PART11-06 | H | R1 | Per § 11.200, re-authentication shall be required at the moment of PSUR / FSCA approval. |
| URS-PART11-07 | H | R1 | Per § 11.300, password / credential controls per site InfoSec policy. |

### 5.10 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | **Attributable:** All PMS entries attributable to a named user. |
| URS-DI-02 | H | R1 | **Legible:** PSUR / PSMR / FSCA records exportable as human-readable PDF/A-3. |
| URS-DI-03 | H | R1 | **Contemporaneous:** Events recorded at time of occurrence. |
| URS-DI-04 | H | R1 | **Original:** Source complaint records preserved unaltered; PSUR-derived analyses reference but do not overwrite. |
| URS-DI-05 | H | R1 | **Accurate:** Trending statistics shall be deterministic and validated under OQ. |
| URS-DI-06 | M | R2 | **Complete / Consistent / Enduring / Available:** Records meet ALCOA+ retention obligations. |

### 5.11 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-EMDR-01 | H | R1 | Cross-reference to Theia eMDR for serious incidents (bidirectional). |
| URS-INT-EQMS-01 | H | R1 | CAPA linkage to MasterControl with audit-trail propagation. |
| URS-INT-SER-01 | M | R2 | Sales-volume context from Atlas Serialization (commissioning events) for denominator in trend reporting. |
| URS-INT-EUDAMED-01 | H | R1 | PSUR submission via EUDAMED PSUR module (when live); incident submission via EUDAMED vigilance module. |
| URS-INT-BFARM-01 | H | R1 | National competent authority gateway for DE: BfArM (MPDG-compliant submission interface). |
| URS-INT-SWISS-01 | H | R1 | National competent authority gateway for CH: Swissmedic (MepV-compliant submission interface). |
| URS-INT-AGES-01 | M | R2 | National competent authority gateway for AT: AGES PharmMed. |
| URS-INT-LIT-01 | M | R2 | Literature-surveillance feed (Embase / PubMed) for proactive PMS. |

### 5.12 Performance, Availability, Backup, Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | UI response time P95 ≤ 3 seconds for typical PMS-Specialist workflows. |
| URS-AV-01 | H | R1 | Availability ≥ 99.5% measured monthly. |
| URS-BAK-01 | H | R1 | Vendor SLA + site quarterly tenant-data export verification; site retains tenant export with 10-year retention. |
| URS-BAK-02 | M | R2 | RTO ≤ 24 hours; RPO ≤ 4 hours per vendor SLA. |
| URS-SEC-01 | H | R1 | All data in transit shall be TLS 1.3; data at rest AES-256. |
| URS-SEC-02 | H | R1 | Role-based access reviewed quarterly; PRRC role assignment requires Reg-Affairs approval. |
| URS-SEC-03 | M | R2 | Penetration testing annually; high/critical findings remediated under change control. |

### 5.13 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Role-specific training in the site LMS shall be completed before access; PRRC training shall include EU MDR Art. 15 obligations. |
| URS-TRN-02 | M | R2 | Annual refresher training shall cover EU MDR updates, MDCG guidance changes, FSCA scenarios. |
| URS-PR-01 | H | R1 | Annual periodic review covering vendor qualification currency, configuration drift, audit-trail review evidence, PMS-plan adherence, PMCF status, signal-management metrics, training currency, and integration health. Signed by Director PMS + PRRC + VP QA + VP Reg Affairs. |

### 5.14 Real-Time PMS Dashboard and KPI Engine

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DASH-01 | H | R1 | A real-time PMS dashboard shall surface per-device KPIs: complaint rate (rolling 90-day), serious-incident count + rate, Article 88 trend statistics (CUSUM / EWMA chart), PMCF commitment status, PMS-plan-cycle status; refreshed ≤ 15 min latency from event arrival. |
| URS-DASH-02 | H | R1 | Per-device drill-down shall include incident triage breakdown (serious / non-serious / pending), reporting-clock margin distribution, and Notified-Body-required item status. |
| URS-DASH-03 | M | R2 | Dashboard exports (PNG / PDF / CSV) shall include data-cut timestamp and dataset checksum for inspection traceability. |
| URS-DASH-04 | M | R2 | KPI thresholds (e.g., complaint-rate alert) shall be configurable per device with change-control; threshold breach events shall raise alerts to Director PMS + PRRC. |

### 5.15 Benefit-Risk and PSUR-Risk Matrix Integration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BR-01 | H | R1 | A device-level Benefit-Risk Profile (per ISO 14971:2019 §10) shall be maintained with hazard-source links to PMS data; the profile shall feed PSUR Section 6 (benefit-risk evaluation). |
| URS-BR-02 | H | R1 | A PSUR-Risk Matrix shall map each device hazard to: (a) implemented control measures, (b) residual-risk acceptability, (c) post-market evidence (cases + literature + trend), (d) action / change required; PSUR auto-extraction from this matrix. |
| URS-BR-03 | H | R1 | Risk-control effectiveness shall be quantitatively tracked per ISO 14971:2019 §10.3 using PMS-derived incident-rate per control; change-flag raised when residual-risk acceptability is impacted. |
| URS-BR-04 | M | R2 | Risk-Management File (ISO 14971 §4.5) link to PMS shall be bidirectional; updates to the risk-management file shall be triggered by signal-closure and FSCA events. |

### 5.16 Health Authority Correspondence and Inspection Readiness

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HAC-01 | H | R1 | Health-authority correspondence (CA queries, Notified-Body queries, PSUR feedback, FSCA acknowledgements) shall be tracked in a structured register with sender, recipient, due-date, response-due-date, status. |
| URS-HAC-02 | H | R1 | CA-query response workflow shall enforce SoD (drafter ≠ reviewer ≠ PRRC approver); response packages exportable in inspection-ready format. |
| URS-HAC-03 | H | R1 | Inspection-readiness export shall produce an EU MDR Annex II-aligned dossier including PMS plan, PSURs, PMS reports, FSCAs, complaint summary, training records, audit trail extracts; export retrievable ≤ 4h. |
| URS-HAC-04 | M | R2 | Pre-inspection mock-audit reports shall be supported via a structured rehearsal workflow. |
| URS-HAC-05 | M | R2 | Notified-Body-related correspondence (TÜV SÜD CE 0123 queries, certification surveillance findings) shall be tagged separately for audit visibility. |

### 5.17 Multi-Region Notified-Body and Authorised-Representative Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-NB-01 | H | R1 | Per-device Notified Body designation (e.g., TÜV SÜD CE 0123 for EU; UK-Approved-Body for UKCA; SwissAuthorisedRepresentative for CH) shall be maintained with certificate expiry tracking. |
| URS-NB-02 | H | R1 | Notified-Body assessment of PSUR (per EU MDR Art. 86(2) for Class III + implantables) shall be tracked with assessment-due-date + outcome. |
| URS-NB-03 | H | R1 | EU MDR Authorised Representative (Art. 11), CH-REP (Swiss authorised representative per MepV), UK Responsible Person (UK Reg. 2002 amendments), Singapore Importer, Brazil ANVISA holder shall be tracked per device per market. |
| URS-NB-04 | M | R2 | Notified-Body certificate transitions (e.g., MDD → MDR) shall be tracked with transition milestones. |

### 5.18 Patient + HCP Complaint Intake Channels

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-PAT-01 | H | R1 | Patient-direct complaint intake shall be supported via secure web form + phone-call ticket integration; minimum GDPR-compliant data set captured (consent, contact, device, complaint description). |
| URS-INT-HCP-01 | H | R1 | HCP complaint intake shall be supported via HCP-portal + email-gateway parsing; HCP role / qualification captured. |
| URS-INT-DIST-01 | M | R2 | Distributor / importer complaints (per EU MDR Art. 14, 16) shall be supported with chain-of-custody capture. |
| URS-INT-DEDUP-01 | M | R2 | Complaint deduplication across intake channels shall use configurable rule set; suspected duplicates routed for merge decision. |

### 5.19 Data Quality and Completeness Rules

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DQ-01 | H | R1 | Mandatory field validation per EU MDR Art. 87 Annex shall block submission when required fields incomplete; the field-completeness check shall run on every state transition. |
| URS-DQ-02 | H | R1 | Field-content validation (date ranges, ISO 3166-1 country codes, UDI-DI format per IMDRF UDI guidance) shall execute server-side; rejection messages shall be specific. |
| URS-DQ-03 | M | R2 | Data-quality KPIs (% records with missing optional fields, % records with corrected fields after review) shall be reported monthly. |

### 5.20 PMS Plan Authoring and Cycle Execution

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAN-AUTH-01 | H | R1 | PMS plan authoring shall use the EU MDR Annex III template; section-binding shall enforce structural completeness before approval. |
| URS-PLAN-AUTH-02 | H | R1 | PMS-plan-cycle execution shall be tracked per device with cycle-start, milestones, cycle-completion, deviation; cycle status visible in dashboard. |
| URS-PLAN-AUTH-03 | M | R2 | PMS-plan dependencies (PMCF protocol, literature-search strategy, registry pull frequency) shall be linked to lifecycle artefacts. |
| URS-PLAN-AUTH-04 | H | R1 | PMS plan approval shall require Director PMS + PRRC + VP QA signature; subsequent modifications shall re-trigger approval. |

### 5.21 EUDAMED Module-Specific Integration Detail

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-EUDAMED-MOD-01 | H | R1 | EUDAMED Actor module integration: Manufacturer + Authorised Representative + Importer + System / Procedure Pack Producer registration kept in sync. |
| URS-EUDAMED-MOD-02 | H | R1 | EUDAMED UDI / Device module integration: UDI-DI, UDI-PI, Basic UDI-DI tracking; device-data submission per Art. 29. |
| URS-EUDAMED-MOD-03 | H | R1 | EUDAMED Certificate module integration: Notified Body certificates tracked with expiry monitoring. |
| URS-EUDAMED-MOD-04 | H | R1 | EUDAMED Vigilance module: serious-incident + Art. 88 trend + FSCA submissions routed to the vigilance module. |
| URS-EUDAMED-MOD-05 | H | R1 | EUDAMED Market Surveillance module: competent-authority-driven post-market investigations tracked. |
| URS-EUDAMED-MOD-06 | M | R2 | EUDAMED Clinical Investigation and PMCF Studies module: PMCF studies registered + status updates per Art. 74. |

### 5.22 ISO 14971:2019 Risk Management Integration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RM-01 | H | R1 | Risk-Management File per device shall be bidirectionally linked to PMS plan + PMS data per ISO 14971:2019 § 4.5 (Risk-Management File contents). |
| URS-RM-02 | H | R1 | Production and post-production information feedback per ISO 14971:2019 § 10 shall be implemented: information collection (§ 10.1), information review (§ 10.2), actions (§ 10.3). |
| URS-RM-03 | H | R1 | Newly identified hazards from PMS shall raise Risk-Management-File-update CRs per ISO 14971 § 10.3; CR shall be tracked to completion. |
| URS-RM-04 | M | R2 | Per ISO/TR 24971:2020, the Risk-Management Plan shall reference PMS data collection methods + acceptance criteria for residual risk. |
| URS-RM-05 | M | R2 | Risk-control effectiveness evidence shall be reviewed at the Risk-Management Review meeting cadence with PMS metrics as primary input. |
| URS-RM-06 | H | R1 | Hazard-to-event traceability shall be maintained: each PMS event ↔ {0,1+} known hazards in RMF; new-hazard creation event audit-trailed. |

### 5.23 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is SAML 2.0 via Entra ID with SCIM lifecycle provisioning; conditional-access policy `PMS-Sensitive Conditional Access (FIDO2 phishing-resistant MFA)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with PostgreSQL pg_basebackup + continuous WAL archiving; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 10 y post-EOL (MDR) per the consuming-record schedule. |

### 5.24 Cross-System Integration — eQMS CAPA handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-EQMS-01 | H | R1 | On detection of PMS finding (EU MDR Art. 83) (trigger: PMS-trend or PSUR-trend exceedance, FSCA, vigilance signal), the system shall push a CAPA-ticket creation event to the Talos MasterControl eQMS (`TLB-URS-EQMS-001`) via the eQMS event-push channel with required metadata {originating_system, originating_record_id, finding_class, severity, evidence_package_uri, detection_ts_utc, detection_user, regulatory_basis}; severity per MDCG 2020-1; FSCA → critical; trend → major. |
| URS-XINT-EQMS-02 | H | R1 | The eQMS ticket-creation call shall be idempotent on `{originating_system, originating_record_id, finding_class}`; the eQMS status-callback shall be ingested and reflected on the originating record with a hyperlink to the eQMS ticket; closed-loop verification per ICH Q9(R1) + ICH Q10 shall be evidenced before the originating record is dispositioned. |

### 5.25 Cross-System Integration — Adverse Event DB handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-AE-01 | H | R1 | Vigilance signals detected by the PMS DB (trend exceedance, PSUR-trend, FSCA precursor) shall be handed over to the Theia Adverse Event DB (`TEA-URS-MDR-001`) via the AE ingest contract `theia.ae.v1` with required metadata `{device_udi, signal_class, severity, evidence_uri, detection_ts_utc, regulatory_basis}`; the AE DB shall be the system-of-record for the per-incident MDR / eMDR / FSCA dossier. |
| URS-XINT-AE-02 | H | R1 | FSCA decisions confirmed in the AE DB shall flow back to the PMS DB via the AE callback channel `theia.fsca.callback.v1` so that the PMS DB's per-device PMS plan reflects the FSCA state and the next PSUR cycle inherits the FSCA evidence. |

## 6. Acceptance Criteria

1. CS, RA, IQ (vendor-shared), OQ (PMS plan / PSUR / signal-management / FSCA / submission / audit), PQ (representative end-to-end including PSUR generation + EUDAMED submission + Art. 87 incident escalation + Art. 88 trend report scenario) approved and executed.
2. VSR approved by VP QA + VP Reg Affairs + PRRC.
3. RTM shall demonstrate every URS requirement mapped to at least one approved test case.
4. National competent authority gateway interfaces (BfArM, Swissmedic, AGES, EUDAMED) verified under PQ.

## 7. Constraints

- Vendor releases not under site change control but evaluated before promotion.
- PRRC sign-off cannot be delegated outside the named role.
- EUDAMED submission requires the EUDAMED PSUR module to be active for the relevant device class.

## 8. Assumptions

- Theia eMDR, MasterControl, Atlas, EUDAMED, BfArM gateway, Swissmedic gateway, AGES gateway operational and validated.
- Notified Body (TÜV SÜD CE 0123) maintains its designation.
- Sales-volume data from Atlas reflect actual market exposure.

## 9. References

### EU
- EU MDR Reg. 2017/745 — Articles 10 (manufacturer obligations), 11 (Authorised Representative), 14 (importer), 15 (PRRC), 16 (distributor), 83 (PMS), 84 (PMS Plan), 85 (PMSR), 86 (PSUR), 87 (Serious incidents), 88 (Trend), 89 (FSCA), 92 (EUDAMED).
- MDCG 2019-9 — Summary of safety and clinical performance.
- MDCG 2022-21 — PSUR guidance.
- MDCG 2023-3 — Questions and Answers on vigilance terms and concepts under MDR.
- EUDAMED — European Database on Medical Devices (manufacturer, UDI, certificates, PMS, vigilance, market surveillance modules).

### DACH-specific competent authorities
- **BfArM (DE)** — Bundesinstitut für Arzneimittel und Medizinprodukte; Medizinprodukterecht-Durchführungsgesetz (MPDG).
- **Swissmedic (CH)** — Swiss Agency for Therapeutic Products; MepV (Medizinprodukteverordnung) and MepKV (Klinische-Versuche-Verordnung).
- **AGES PharmMed (AT)** — Österreichische Agentur für Gesundheit und Ernährungssicherheit, PharmMed Division.

### US
- 21 CFR Part 820 §§ .100 (Corrective and preventive action), .198 (Complaint files).
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300 — Electronic Records; Electronic Signatures.
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).

### ISO
- ISO 14971:2019 — Medical Devices: Application of Risk Management.
- ISO/TR 24971:2020 — Guidance on application of ISO 14971.
- ISO 13485:2016 — Medical Devices: Quality Management Systems.

### ISPE
- ISPE GAMP 5 (2nd Edition, 2022).

### Vendor
- Sparta — *TrackWise Digital PMS Module Configuration and Administration Reference*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

