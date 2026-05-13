---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: Claude (Anthropic) — inline batch, 2026-04-27; expanded 2026-05-12 (§5 breakout + DACH context + ICH E6(R3) explicit binding)
seed_corpus_basis:
  - GAMP 5 (2nd ed.) Cat 4 SaaS conventions
  - 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
  - ICH E6(R3) Good Clinical Practice (Step 4, adopted 6 January 2025); ICH E8(R1) General Considerations for Clinical Studies; ICH E9(R1) Statistical Principles + Estimands
  - EU Clinical Trials Regulation 536/2014 (CTR); CTIS (EU Clinical Trials Information System); ICH E2A
  - FDA Guidance on Patient-Reported Outcome Measures (2009); FDA Patient-Focused Drug Development (PFDD) Guidance series (2018-2024)
  - GDPR (Reg. (EU) 2016/679) Arts. 6, 9 (health data), 22 (automated decisions), 32 (security), 35 (DPIA)
  - HIPAA / HITECH (US patient data)
  - ISPOR Translation and Linguistic Validation Principles of Good Practice
  - BfArM (DE), Paul-Ehrlich-Institut (DE biologicals), Swissmedic (CH), AGES PharmMed (AT)
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# User Requirements Specification (URS)

## ePRO / eCOA Patient Portal — Clario eCOA Platform 2025

**Document Number:** IOL2-URS-EPRO-001 | **Version:** 1.0 | **Effective Date:** 2026-04-27 *(synthetic)*
**Site:** Iolanthe Clinical Operations GmbH, Patient-Reported Outcomes Operations, Wien, Austria *(fictional)*
**System Owner:** Director, eCOA Operations
**Process Owner:** VP Clinical Operations
**Sponsor Representative:** Clinical Trial Sponsor (per EU CTR Art. 71 / ICH E6(R3))
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Project Mode:** Configuration project on commercial software product **Clario eCOA Platform 2025** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; ICH E6(R3) GCP (Step 4, adopted 6 January 2025); ICH E8(R1); ICH E9(R1); EU Clinical Trials Regulation 536/2014 (CTR); CTIS submission requirements; FDA *Patient-Reported Outcome Measures* (2009) and PFDD Guidance series; HIPAA / HITECH; GDPR Arts. 6, 9, 22, 32, 35; ISPOR Translation Principles; BfArM (DE); Paul-Ehrlich-Institut (DE biologicals/vaccines); Swissmedic (CH); AGES PharmMed (AT).

> **Note:** Distinct from Medidata EDC (Marigold URS — site-side data management). This URS covers a **patient-facing ePRO / eCOA platform** for participants to enter outcome data via app, web, or provisioned device, with linguistically-validated translation across many languages. ICH E6(R3) (Step 4, 2025) governs the GCP framework; EU CTR 536/2014 governs EU clinical trial conduct via CTIS submissions.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, eCOA Operations) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Privacy Officer — HIPAA / GDPR / DPIA) | _____________ | _____________ | _____ |
| Reviewer (Sponsor Clinical Lead) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs — CTIS Submissions) | _____________ | _____________ | _____ |
| Approver (VP Clinical Operations) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-12 | (synthetic) | §5 broken out into 12 subsections; DACH relocation (Wien, AT); ICH E6(R3) Step 4 (Jan 2025) + EU CTR / CTIS explicit binding; GDPR Arts. 6/9/22/32/35 binding; BfArM / PEI / Swissmedic / AGES added to References; risk table expanded to 12 rows. |
| 1.2 | 2026-05-12 | (synthetic) | T3 uplift to 105 requirements (Tier T3 per § 2A.13). Added: § 5.13 Diary Compliance Dashboard; § 5.14 Reminder Ladder + Drop-off Recovery; § 5.15 Patient Onboarding Flow; § 5.16 Adverse Event Capture Integration (EDC); § 5.17 eCOA Library Management (validated instruments); § 5.18 Bring-Your-Own Patient-ID (BYOPID) Anonymization; § 5.19 Multi-Country Time-Zone-Aware Diary Schedule; § 5.20 Patient Recruitment + Retention Tools; § 5.21 Vendor Assurance hardening (sub-processor governance); risk table expanded to 17 rows. |

## Definitions

| Term | Definition |
|---|---|
| ePRO | Electronic Patient-Reported Outcome |
| eCOA | Electronic Clinical Outcome Assessment |
| ClinRO | Clinician-Reported Outcome |
| ObsRO | Observer-Reported Outcome |
| PerfO | Performance Outcome |
| BYOD | Bring Your Own Device (patient mobile) |
| Provisioned Device | Site-issued provisioned tablet (study-locked) |
| Translation | Linguistically validated translation per ISPOR / FDA guidance |
| EDC | Medidata Rave (separate URS — Marigold) |
| eTMF | electronic Trial Master File (separate URS — Marinos) |
| CTIS | Clinical Trials Information System (EU CTR submission portal) |
| DPIA | Data Protection Impact Assessment (GDPR Art. 35) |
| RBM | Risk-Based Monitoring (per ICH E6(R3) §3.10) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the patient-facing ePRO / eCOA platform that captures patient-reported outcomes for clinical trials managed by Iolanthe under ICH E6(R3) GCP, EU CTR 536/2014, and applicable US / EU / DACH regulations. The platform serves trials conducted across DACH (DE / AT / CH) and globally.

## 2. Scope

**In:** Clario eCOA Platform 2025 multi-tenant SaaS; per-study configuration of instruments + schedules + languages (translation-validated per ISPOR); patient mobile app + web + provisioned-tablet modes; SSO via Okta for site users; integrations with Medidata Rave EDC for PRO data flow, eTMF for archival, CTIS for sponsor-submission packs. GDPR Art. 35 DPIA per study; HIPAA Business Associate Agreement for US trials. ICH E6(R3) §3.10 risk-based monitoring data feed.

**Out:** vendor infrastructure; site-data-management platform (covered by EDC); investigator delegation logs (eTMF); sponsor CTIS portal interactions (separate scope); ICH E2A safety reporting (covered by Sirius Argus URS).

## 3. System Description

The platform is the system of record for patient-reported outcome data — instrument scheduling per protocol, daily / event-driven completion, time-window enforcement, alerts to patients, instrument adherence reporting. Site users see compliance dashboards. PRO data flow to EDC after configurable sign-off windows. For EU trials, study-build documentation supports CTIS submission packs per EU CTR Art. 25.

Risk-based monitoring per ICH E6(R3) §3.10: the platform surfaces protocol-deviation rates, adherence outliers, missing-data patterns, and instrument-completion times for sponsor RBM dashboards.

GAMP Cat 4: Clario maintains the SDLC; site validates per-study configuration, translation validation, integration boundaries, and Part 11 controls.

## 4. User Roles

| Role | Permissions |
|---|---|
| Patient (Participant) | Complete instruments; view own diary. |
| Site Investigator | Review patient compliance; resolve missed entries per protocol; cannot edit patient data. |
| Site Coordinator | View patient compliance dashboards; reach out to patients for missed entries. |
| Sponsor Clinical Monitor | Review study-level metrics; RBM dashboard access. |
| Study Builder | Configure instruments + schedules under change control. |
| Study Approver | Approve study build to PRODUCTION; cannot author. |
| Translation Validator | Approve linguistic validation evidence per language. |
| eCOA Administrator | User / role provisioning, AD groups; cannot edit data. |
| Auditor | Read-only across data + audit trails. |

Standard SoD; Builder ≠ Approver; Site Coordinator + Site Investigator cannot edit PRO data on behalf of patient (preserves attributability per ALCOA+).

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` direct GxP impact / `R2` indirect / `R3` none).

### 5.1 Vendor Assurance and Per-Study Configuration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-01 | H | R1 | Clario shall be qualified as a critical SaaS vendor with SOC 2 Type II + ISO 27001 + HIPAA evidence on file; annual re-qualification. |
| URS-VND-02 | H | R1 | Clario release notes shall be reviewed under site change control; vendor SDLC evidence inspected annually. |
| URS-CFG-01 | H | R1 | Per-study configuration shall follow DEV → QC → UAT → PRODUCTION; promotion shall require SoD-enforced signatures (Author ≠ Approver). |
| URS-CFG-02 | H | R1 | Study-build documentation shall include CTIS-submission pack per EU CTR Art. 25 for EU trials. |
| URS-CFG-03 | M | R2 | Configuration changes shall be exportable for sponsor inspection and version-controlled. |

### 5.2 Linguistic Validation and Translation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LING-01 | H | R1 | Each instrument translation shall be linguistically validated per ISPOR Principles of Good Practice and FDA *Patient-Reported Outcome Measures* (2009) prior to use; certificate of linguistic validation shall be attached per language. |
| URS-LING-02 | H | R1 | Out-of-validation translations shall be blocked from use; patient access to unvalidated language shall return an error. |
| URS-LING-03 | H | R1 | German (de-DE, de-AT, de-CH variants), French, Italian shall be supported as separate validated translations for DACH trials. |
| URS-LING-04 | M | R2 | Translation version drift (instrument-version change) shall trigger re-validation of all affected languages. |

### 5.3 Patient Data Capture and Adherence

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PAT-01 | H | R1 | Each entry shall capture: patient-id (pseudonymised), instrument-id + version, timestamp (server-side, NTP-synced), entry payload, language-locale used. |
| URS-PAT-02 | H | R1 | Time-window enforcement per instrument (e.g., daily diary entry only valid 06:00 – 22:00 patient-local-time); out-of-window entries shall be flagged. |
| URS-PAT-03 | H | R1 | Adherence dashboard shall surface patient-level and study-level metrics for sponsor RBM per ICH E6(R3) §3.10. |
| URS-PAT-04 | H | R1 | Missed-entry alerts to patient via push notification + SMS per the configured ladder; site shall be notified after the patient-level escalation threshold. |
| URS-PAT-05 | H | R1 | Patient response timestamps shall be NTP-synced; clock-drift > 5 minutes shall flag the entry. |

### 5.4 BYOD and Provisioned Devices

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEV-01 | H | R1 | BYOD device-registration shall capture device-id + OS + app-version; out-of-policy devices (e.g., jailbroken / rooted) shall be blocked. |
| URS-DEV-02 | H | R1 | Provisioned tablets shall be MDM-managed; site-locked configuration; loss / theft shall trigger remote-wipe within 15 min of report. |
| URS-DEV-03 | H | R1 | BYOD app shall support iOS and Android current + n-1 major versions. |
| URS-DEV-04 | M | R2 | BYOD vs provisioned-device choice per study shall be documented in the study-build with rationale. |

### 5.5 Audit Trail and Records Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | A contemporaneous, time-stamped audit trail shall capture user, action, old value, new value, reason-for-change for all PRO entries, edits, signatures, configuration changes, translation approvals. |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only at the platform level; not editable by tenant administrators. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be performed per study build (event-driven) and quarterly (periodic) by the site QA. |
| URS-AUD-04 | H | R1 | Retention: per ICH E6(R3) and EU CTR — minimum 25 years for clinical trial data; longer per jurisdiction where required. |
| URS-AUD-05 | M | R2 | Audit-trail review shall include patterns suggesting data-quality issues per ICH E6(R3) §3.10 RBM. |

### 5.6 21 CFR Part 11 Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a), procedures and controls shall protect the validity of patient-entered records. |
| URS-PART11-02 | H | R1 | Per § 11.10(d), site-user access shall be limited via Okta SSO + MFA; patient access via per-study credentials + MFA where supported. |
| URS-PART11-03 | H | R1 | Per § 11.10(e), operational audit trail per § 5.5 shall exist. |
| URS-PART11-04 | H | R1 | Per § 11.50, electronic signatures applied to study-build approvals and translation-validation approvals shall include signer's printed name, date and time, and meaning of signature. |
| URS-PART11-05 | H | R1 | Per § 11.70, signatures shall be cryptographically linked to the signed record. |
| URS-PART11-06 | H | R1 | Per § 11.200, re-authentication shall be required at the moment of study-build approval. |
| URS-PART11-07 | H | R1 | Per § 11.300, password / credential controls per site InfoSec policy; patient credentials per HIPAA / GDPR + study-specific token policy. |
| URS-PART11-08 | H | R1 | Patient e-signature shall be captured at instrument completion where the instrument requires affirmation (e.g., consent-to-data-use). |

### 5.7 Data Integrity (ALCOA+) and Patient Privacy

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | **Attributable:** Every PRO entry shall be attributable to the participant by pseudonymised ID; re-identification only via EDC behind additional access controls. |
| URS-DI-02 | H | R1 | **Legible:** PRO records exportable as human-readable PDF and machine-readable CSV / XML. |
| URS-DI-03 | H | R1 | **Contemporaneous:** Entries recorded at the time of completion; retroactive entries shall be flagged and require justification. |
| URS-DI-04 | H | R1 | **Original:** Raw patient entries preserved unaltered; corrections recorded as a new version with reason-for-change. |
| URS-DI-05 | H | R1 | **Accurate:** Time-window enforcement, instrument scoring, and adherence metrics deterministic and validated under OQ. |
| URS-DI-06 | M | R2 | **Complete / Consistent / Enduring / Available:** Records shall meet ALCOA+ retention obligations (≥ 25 years per ICH E6(R3) and EU CTR). |
| URS-PRV-01 | H | R1 | **GDPR Art. 9 (special category — health data):** Patient demographics minimised; pseudonymised in the platform; encryption at rest (AES-256) and in transit (TLS 1.3). |
| URS-PRV-02 | H | R1 | **GDPR Art. 35 DPIA:** A DPIA shall be on file per study before patient enrolment; the DPIA shall be referenced from the study-build. |
| URS-PRV-03 | H | R1 | **GDPR Art. 22:** Automated decision-making affecting the participant (e.g., adherence-based protocol changes) shall require human review; pure-automated decisions on data shall be prohibited. |
| URS-PRV-04 | H | R1 | **Cross-border transfer:** EU patient data transfer outside EU/EEA shall be governed by Standard Contractual Clauses (SCCs) or adequacy decision; transfer routes shall be documented per study. |

### 5.8 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-EDC-01 | H | R1 | PRO data push to Medidata Rave EDC after configurable sign-off windows; idempotent on entry-id; reconciliation log retained. |
| URS-INT-ETMF-01 | H | R1 | Validation evidence + study-build documentation filed in eTMF (Marinos URS); auto-deposit on study-build approval. |
| URS-INT-CTIS-01 | H | R1 | For EU trials, study-build documentation pack shall be exportable in the CTIS-compatible format per EU CTR Art. 25. |
| URS-INT-AUTH-01 | H | R1 | Site-user authentication via Okta SAML 2.0 + MFA; patient authentication per Clario patient-portal mechanism (per-study credentials + MFA where supported). |
| URS-INT-RBM-01 | H | R1 | Risk-based monitoring data feed shall expose adherence + completion + time-of-day patterns to sponsor RBM dashboard per ICH E6(R3) §3.10. |

### 5.9 Performance and Availability

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | App / web instrument open shall complete ≤ 3 s at the 95th percentile from a typical patient device. |
| URS-PERF-02 | M | R2 | The platform shall sustain ≥ 10,000 concurrent patient sessions across studies. |
| URS-AV-01 | H | R1 | Availability ≥ 99.5% per Clario SLA; sponsor-critical visit windows ≥ 99.9%. |
| URS-AV-02 | M | R2 | Offline-mode data capture shall be supported with automatic sync on network restore. |

### 5.10 Backup, Restore, and Disaster Recovery

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | Vendor-managed backup with daily integrity verification; site shall verify vendor RPO ≤ 4 h, RTO ≤ 24 h via annual vendor-assurance review. |
| URS-BAK-02 | M | R2 | Site shall maintain a tenant-data export with ≥ 25-year retention in cold storage. |
| URS-BAK-03 | H | R1 | DR-site failover shall be tested annually by Clario; site shall review test report. |

### 5.11 Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | All patient data in transit shall use TLS 1.3; data at rest AES-256. |
| URS-SEC-02 | H | R1 | Patient credentials shall not be reused across studies; account-lockout after 5 failed attempts in 15 minutes. |
| URS-SEC-03 | H | R1 | Vendor SOC 2 Type II + ISO 27001 evidence reviewed annually; gaps escalated under change control. |
| URS-SEC-04 | M | R2 | Penetration testing of patient-facing endpoints annually; high/critical findings remediated. |
| URS-SEC-05 | H | R1 | Patient PII minimisation shall be enforced; field-level controls in the platform UI for site users. |

### 5.12 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Role-specific training in the site LMS shall be completed before access; ICH E6(R3) GCP training shall be current for all Site Investigators, Coordinators, and Sponsor Monitors. |
| URS-TRN-02 | M | R2 | Annual refresher training shall cover ICH E6(R3) updates, GDPR / HIPAA changes, RBM practices. |
| URS-PR-01 | H | R1 | Annual periodic review shall cover translation inventory + currency, configuration drift, audit-trail review evidence, integration health, training currency, security posture, DPIA currency, vendor qualification currency; signed by Director eCOA Operations + Privacy Officer + VP QA + VP Clinical Operations. |

### 5.13 Diary Compliance Dashboard

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DCD-01 | H | R1 | A site-facing Diary Compliance Dashboard shall surface per-patient adherence (% complete / on-time / late / missed) over rolling windows (7-day, 14-day, study-to-date). |
| URS-DCD-02 | H | R1 | Sponsor RBM dashboard view shall surface site-level + study-level + cohort-level compliance with drill-down to patient-level. |
| URS-DCD-03 | M | R2 | Adherence outlier alerts shall be configurable (e.g., < 70% adherence over 14 d) with role-targeted escalation (site coordinator → site investigator → sponsor monitor). |
| URS-DCD-04 | M | R2 | Compliance trend reports shall surface time-of-day patterns + day-of-week patterns + protocol-deviation rate to support RBM per ICH E6(R3) §3.10. |
| URS-DCD-05 | M | R2 | Site-coordinator daily worklist shall be auto-prioritised by overdue + outlier patients. |

### 5.14 Reminder Ladder + Drop-off Recovery

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RLR-01 | H | R1 | A reminder ladder shall escalate missed entries: push notification → SMS → email → site-notification → site outreach call; ladder configurable per instrument. |
| URS-RLR-02 | H | R1 | Reminder timing shall respect patient quiet-hours (default 22:00 – 07:00 patient-local); time-zone honored per patient profile. |
| URS-RLR-03 | M | R2 | Drop-off-recovery workflow shall trigger after configurable consecutive missed entries (default 3); workflow shall include site-coordinator outreach + protocol-specific re-engagement script. |
| URS-RLR-04 | M | R2 | Patient-fatigue heuristics shall surface patients at retention risk before drop-off (e.g., increasing entry-latency + decreasing dwell-time). |

### 5.15 Patient Onboarding Flow

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ONB-01 | H | R1 | Patient onboarding shall include identity verification per site IRB/IEC-approved process, device pairing (BYOD or provisioned), study-credential issuance, and consent re-confirmation in app. |
| URS-ONB-02 | H | R1 | Onboarding completion event shall be recorded with timestamp + verifying-site-staff + method; entry-into-study cannot proceed without onboarding completion. |
| URS-ONB-03 | M | R2 | Onboarding tutorial shall be available in each supported language; completion of tutorial shall be tracked. |
| URS-ONB-04 | M | R2 | Onboarding accessibility shall meet WCAG 2.1 AA for vision / motor / cognitive accessibility. |

### 5.16 Adverse Event Capture Integration (EDC)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AE-01 | H | R1 | Patient-flagged AE signals (e.g., out-of-range PRO score, free-text symptom report) shall trigger AE capture workflow with notification to site investigator. |
| URS-AE-02 | H | R1 | AE data captured via ePRO shall flow to Medidata Rave EDC (Marigold) AE module via idempotent push; flow audit-trailed. |
| URS-AE-03 | H | R1 | SAE-triggering inputs shall surface immediately on the site dashboard with red-flag indicator; site investigator follow-up shall be evidenced in the audit trail. |
| URS-AE-04 | M | R2 | AE workflow shall preserve patient-reported wording; site interpretation is captured as a separate field. |
| URS-AE-05 | M | R2 | AE event time-stamps shall use server-side NTP-synced clock; patient-claimed onset time captured as separate field per ICH E2A. |
| URS-AE-06 | M | R2 | AE workflow audit shall be reviewable by sponsor pharmacovigilance via cross-link to Sirius Argus (separate URS). |

### 5.17 eCOA Library Management (validated instruments)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LIB-01 | H | R1 | The system shall maintain an eCOA library of validated instruments (PRO, ClinRO, ObsRO, PerfO) with author, version, licensing, validated languages. |
| URS-LIB-02 | H | R1 | Instrument-version lifecycle shall be tracked; only the licensed + linguistically-validated version shall be assignable to a study. |
| URS-LIB-03 | H | R1 | Licensing evidence per instrument per study shall be on file; missing license shall block study build. |
| URS-LIB-04 | M | R2 | Instrument scoring rules shall be deterministic + validated; scoring-rule changes shall trigger re-validation of all studies using the instrument. |
| URS-LIB-05 | M | R2 | Custom (non-library) instruments shall require sponsor + IRB/IEC approval + linguistic-validation evidence before use. |

### 5.18 Bring-Your-Own Patient-ID (BYOPID) Anonymization

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BYOPID-01 | H | R1 | Patient identifiers (subject-id) shall be pseudonymised at the boundary of the ePRO platform; re-identification routes shall reside in EDC (Marigold) behind separate access controls. |
| URS-BYOPID-02 | H | R1 | Subject-id format shall be configurable per study (sponsor-defined format) but shall not contain identifiable patient information (no DOB, no MRN). |
| URS-BYOPID-03 | M | R2 | Anonymisation testing shall be performed per study build with sampled subject-id review by Privacy Officer. |

### 5.19 Multi-Country Time-Zone-Aware Diary Schedule

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TZ-01 | H | R1 | Diary schedules shall be expressed in patient-local time per patient time-zone attribute; server-side processing shall convert to UTC for storage with TZ + offset metadata. |
| URS-TZ-02 | H | R1 | Daylight-saving transitions shall be handled correctly; entry-validity time-windows shall not be silently mis-applied across DST changes. |
| URS-TZ-03 | H | R1 | Patient time-zone changes (e.g., travel) shall be detectable and reconcilable; "time-zone-change" reason for any flagged entry shall be capturable. |
| URS-TZ-04 | M | R2 | Multi-site studies across time-zones (e.g., DE + AT + CH + US) shall not experience site-vs-patient mismatch on diary timing; site coordinator views shall show patient-local time. |

### 5.20 Patient Recruitment + Retention Tools

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RR-01 | M | R2 | Recruitment funnel metrics (invitations sent / interested / consented / onboarded / retained) shall be available per site + per study. |
| URS-RR-02 | M | R2 | Retention metrics shall surface drop-off rate + survival curve per study + per site. |
| URS-RR-03 | L | R3 | Patient-feedback survey shall be deployable mid-study (separately from PRO instruments) to surface retention risks. |
| URS-RR-04 | M | R2 | Compensation / per-entry-incentive tracking shall be supported where IRB/IEC permits; financial flows shall be audit-trailed but operate outside the ePRO patient-data scope. |
| URS-RR-05 | L | R3 | Recruitment-channel attribution (site outreach / patient registry / social-media campaign / IRB-approved direct-to-patient) shall be tracked where applicable. |
| URS-RR-06 | L | R3 | Patient withdrawal reasons (where voluntarily provided) shall be captured per IRB/IEC + ICF approved categories. |

### 5.21 Vendor-Assurance Hardening + Sub-Processor Governance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-03 | H | R1 | Clario sub-processor list (per GDPR Art. 28(2) + DPA Annex II) shall be reviewed quarterly; new sub-processors shall trigger DPIA delta-review. |
| URS-VND-04 | H | R1 | Cross-border data flows arising from new sub-processors shall be assessed against existing SCC routes; new routes require new SCC signature. |
| URS-VND-05 | M | R2 | Vendor SLA shall be evidenced quarterly via SLA-report review; breaches logged in vendor-assurance dossier + eQMS deviation. |
| URS-VND-06 | M | R2 | Vendor SDLC evidence shall be reviewed annually; checklist stored in `/vendor-assurance/clario/`. |
| URS-VND-07 | M | R2 | Vendor release-note feed shall be subscribed-to; impact assessment ≤ 14 days from release-note publication. |

### 5.22 Configuration Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CCM-01 | H | R1 | Configuration changes shall flow DEV → QC → UAT → PROD with SoD-enforced approvals. |
| URS-CCM-02 | H | R1 | Configuration baselines shall be versioned and exportable per study; drift detectable via baseline-diff reports. |
| URS-CCM-03 | M | R2 | Emergency-change post-implementation review ≤ 5 business days. |

### 5.23 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is Entra External ID OIDC for patients in a separate tenant; SAML 2.0 via Entra ID for the internal administrator + clinical-monitor surface, with SCIM lifecycle provisioning on the admin tenant; conditional-access policy `Patient-Facing Conditional Access (MFA via authenticator app or SMS fallback per IRB approval) for patients; Clinical-Sensitive Conditional Access (FIDO2 + device-compliance) for administrators` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with Oracle RMAN for the ePRO Oracle backend and MS SQL Server VSS for the admin metadata store; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 25 y per ICH E6(R3) per the consuming-record schedule. |

### 5.24 Cross-System Integration — Marigold EDC handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-EDC-01 | H | R1 | Patient-reported outcome data captured by the ePRO portal shall be transmitted to the Marigold Medidata Rave EDC (`MAR-URS-EDC-001`) via the Rave datapoint API (CDISC ODM-XML payload) with idempotency on `{study_id, subject_id, visit_id, instrument_id, item_id, completion_ts}`; transmission failures shall be retried with exponential back-off and DLQ at 10 attempts. |
| URS-XINT-EDC-02 | H | R1 | Each transmitted datapoint shall carry the originating ePRO event identifier, the patient-device attestation timestamp, and a SHA-256 hash of the raw response; the EDC shall persist these for source-data verification per ICH E6(R3); discrepancies between ePRO-captured value and EDC-received value shall raise a query in the EDC and a deviation in the ePRO operations log. |
| URS-XINT-EDC-03 | M | R2 | ePRO instrument lifecycle (activation, deactivation, version bump) shall be synchronised with the EDC study metadata via the Rave study-design API; version-mismatch between the active ePRO instrument and the EDC-registered instrument shall block transmission of new datapoints until reconciled. |

## 6. Acceptance Criteria

1. CS, RA, IQ (vendor-shared), OQ (lifecycle / signature / translation / time-window / audit / RBM / library / TZ), PQ (representative end-to-end study including BYOD + provisioned + multi-language + EDC sync + AE flow + CTIS submission pack + DPIA scenario + DST transition + onboarding + drop-off recovery) approved and executed.
2. VSR approved by VP Clinical Operations + VP QA + Privacy Officer.
3. RTM shall demonstrate every URS requirement mapped to at least one approved test case.
4. DPIA approved per study before enrolment.
5. CTIS-compatible study-build pack verified for EU trials.

## 7. Constraints

- Vendor releases are continuous; site does not control vendor SDLC but reviews release notes under change control.
- Per-language linguistic validation shall be completed per ISPOR + FDA guidance before patient access in that language.
- Patient credentials and identifiers shall remain pseudonymised in the platform; re-identification routes shall remain under sponsor / IRB / EC oversight.
- The platform shall not auto-decide patient-affecting outcomes (per GDPR Art. 22).

## 8. Assumptions

- Okta, EDC (Medidata Rave), eTMF (Marinos), CTIS portal operational and validated.
- Clario maintains its certifications (SOC 2, ISO 27001, HIPAA) and gives advance notice of platform changes.
- Sponsor has executed Data Processing Agreement (DPA) with Clario per GDPR Art. 28.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 — Electronic Records; Electronic Signatures (§§ .10, .30, .50, .70, .100, .200, .300).
- FDA *Guidance for Industry: Patient-Reported Outcome Measures* (2009).
- FDA Patient-Focused Drug Development (PFDD) Guidance series (2018–2024).
- HIPAA / HITECH — Health Insurance Portability and Accountability Act.

### EU — EMA / Commission
- EU Clinical Trials Regulation 536/2014 — Articles 25 (application dossier), 56 (database), 71 (sponsor obligations).
- CTIS — Clinical Trials Information System.
- GDPR (Regulation (EU) 2016/679) — Articles 6, 9 (special category — health data), 22 (automated decision-making), 32 (security), 35 (DPIA).

### DACH-specific competent authorities
- **BfArM (DE)** — Bundesinstitut für Arzneimittel und Medizinprodukte.
- **Paul-Ehrlich-Institut (DE)** — federal authority for biologicals and vaccines.
- **Swissmedic (CH)** — Swiss Agency for Therapeutic Products.
- **AGES PharmMed (AT)** — Österreichische Agentur für Gesundheit und Ernährungssicherheit, PharmMed Division.

### International — ICH
- ICH E6(R3) — Good Clinical Practice (Step 4, adopted 6 January 2025).
- ICH E8(R1) — General Considerations for Clinical Studies.
- ICH E9(R1) — Statistical Principles for Clinical Trials + Estimands.

### Industry guidance
- ISPOR — Principles of Good Practice for the Translation and Cultural Adaptation Process for PRO Measures.
- ISPE GAMP 5 (2nd Edition, 2022).

### Vendor
- Clario — *eCOA Platform 2025 Validation Approach*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

