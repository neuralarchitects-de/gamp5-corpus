---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; expanded 2026-05-12 (T4 enrichment per METHODOLOGY § 2A.13)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed.) Cat 4 conventions for safety / pharmacovigilance platforms"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "21 CFR 314.80 (post-marketing AE reporting), 600.80 (biological products), 312.32 (IND safety reporting)"
  - "ICH E2A (Clinical Safety Data Management), E2B(R3) (ICSR), E2C(R2) (PSUR/PBRER), E2D (Post-Approval Safety), M1 (MedDRA), M2 (ESTRI)"
  - "EU GVP Modules I–XVI (esp. II, VI, VII, IX, V, XV, XVI)"
  - "EU CTR Reg. 536/2014 + CTIS safety reporting"
  - "EMA EudraVigilance + EVDAS specifications; FDA FAERS gateway; PMDA Gateway; Health Canada Gateway"
  - "IDMP ISO 11238 / 11239 / 11240 / 11615 / 11616 + EMA SPOR"
  - "ICH E2E (PV Planning); EU RMP guidance; FDA REMS"
  - "BfArM (DE) UAW-Meldungen; Paul-Ehrlich-Institut (DE) for biologicals; Swissmedic (CH); AGES PharmMed (AT)"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Pharmacovigilance Safety Database — Oracle Argus Safety 8.4.1

**Document Number:** SIR-URS-PV-001
**Version:** 1.0
**Effective Date:** 2026-04-26 *(synthetic)*
**Site:** Sirius Pharma Ltd., Global Pharmacovigilance Operations, Dublin (HQ) with regional case-processing hubs in Basel (CH), München (DE), Wien (AT) *(fictional)*
**System Owner:** Head of Pharmacovigilance Operations
**Process Owner:** EU Qualified Person for Pharmacovigilance (QPPV)
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (Oracle vendor-maintained platform with site-authored workflow / coding / reporting configuration; no site-authored custom code)
**Project Mode:** Configuration project on commercial software product **Oracle Argus Safety 8.4.1** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR 314.80, 600.80, 312.32; EU GMP Annex 11 §§ 4, 6, 9, 11; ICH E2A; ICH E2B(R3); ICH E2C(R2); ICH E2D; ICH E2E; ICH M1 (MedDRA); ICH M2 (ESTRI); EU GVP Modules I–XVI; EU CTR Reg. 536/2014; IDMP ISO 11238/11239/11240/11615/11616; BfArM (DE); Paul-Ehrlich-Institut (DE biologicals); Swissmedic (CH); AGES PharmMed (AT).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of PV Operations) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (QPPV — EU) | _____________ | _____________ | _____ |
| Reviewer (Deputy QPPV) | _____________ | _____________ | _____ |
| Reviewer (Medical Director, Drug Safety) | _____________ | _____________ | _____ |
| Reviewer (Signal Management Lead) | _____________ | _____________ | _____ |
| Reviewer (Aggregate Reporting Lead) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs Lead — IDMP / xEVMPD) | _____________ | _____________ | _____ |
| Approver (VP Drug Safety) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | T4 enrichment per METHODOLOGY § 2A.13 (150–250 reqs target): MedDRA / WHO Drug lifecycle expanded (§ 5.3); Medical Assessment expanded (§ 5.4); E2B(R3) sub-element coverage expanded (§ 5.5); Aggregate Reporting broken into PSUR / PBRER / PADER / DSUR (§ 5.6); new § 5.7 Signal Detection + Management (EVDAS / EBGM / PRR / ROR per GVP Module IX); new § 5.8 Risk Management Plan (EU RMP + US REMS); new § 5.9 Pediatric Investigation Plan tracking; new § 5.10 IDMP / xEVMPD product-master integration; new § 5.11 Literature Surveillance; new § 5.12 Partner-Exchange Agreements; § 5.13 Audit Trail expanded with sub-section 11.10(e) binding; § 5.14 21 CFR Part 11 sub-section-explicit; § 5.15 DACH National-CA gateways (BfArM, PEI, Swissmedic, AGES); § 5.16 Clinical-Trial Safety (DSUR + CTR 536/2014 CTIS); citation currency aligned to METHODOLOGY § 2A.1. |

## Definitions

| Term | Definition |
|---|---|
| PV | Pharmacovigilance |
| Argus / Argus Safety | Oracle Argus Safety, version 8.4.1 (8.4.1+ patches applied under change control) |
| ICSR | Individual Case Safety Report |
| E2B(R3) | ICH guideline / HL7 messaging standard for ICSR transmission (current effective revision R3) |
| E2C(R2) | ICH guideline for PSUR / PBRER |
| E2D | Post-approval safety reporting (spontaneous + solicited) |
| E2E | Pharmacovigilance planning (PV plan, signal management framework) |
| MedDRA | Medical Dictionary for Regulatory Activities (per ICH M1) — current version (MedDRA 28.0+); SOC / HLGT / HLT / PT / LLT hierarchy |
| WHO Drug | WHO Drug Dictionary for product / substance coding (UMC, Uppsala) |
| EVDAS | EudraVigilance Data Analysis System (signal detection on EU PV data) |
| EBGM | Empirical Bayes Geometric Mean (disproportionality statistic for signal detection) |
| PRR / ROR | Proportional Reporting Ratio / Reporting Odds Ratio (signal-detection statistics) |
| QPPV | Qualified Person for Pharmacovigilance (EU GVP Module I) |
| Deputy QPPV | Back-up QPPV with documented delegation authority |
| PSUR / PBRER | Periodic Safety Update Report / Periodic Benefit-Risk Evaluation Report (per ICH E2C(R2)) |
| PADER | Periodic Adverse Drug Experience Report (FDA, 21 CFR 314.80(c)(2)) |
| DSUR | Development Safety Update Report (ICH E2F, clinical-trial annual safety) |
| RMP | Risk Management Plan (EU GVP Module V) |
| REMS | Risk Evaluation and Mitigation Strategy (FDA equivalent) |
| PIP | Pediatric Investigation Plan (EU Reg. 1901/2006) |
| IDMP | Identification of Medicinal Products (ISO 11238/11239/11240/11615/11616) |
| xEVMPD | extended EudraVigilance Medicinal Product Dictionary |
| SPOR | EMA Substances, Products, Organisations and Referentials data services |
| FAERS | FDA Adverse Event Reporting System |
| ESG | FDA Electronic Submissions Gateway |
| Argus Mart | Argus reporting / analytics datamart |
| Argus Interchange | Argus E2B gateway component |
| RSI | Reference Safety Information (the company core data sheet / product-specific reference) |
| SUSAR | Suspected Unexpected Serious Adverse Reaction (clinical trial context) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the global safety database used by Sirius Pharma to receive, code, medically assess, submit, periodically report, and signal-manage individual case safety reports (ICSRs) and aggregate safety data across spontaneous, clinical-trial, literature, solicited, and partner-exchange sources for marketed and investigational products. The system supports EU GVP, US 21 CFR 314.80 / 600.80 / 312.32 obligations, ICH E2A/E2B(R3)/E2C(R2)/E2D/E2E, and the operational gateways to EMA EudraVigilance, FDA FAERS, PMDA, Health Canada, and DACH national competent authorities (BfArM, PEI, Swissmedic, AGES).

## 2. Scope

**In scope:** Oracle Argus Safety 8.4.1 application servers (3 active + 1 standby, load-balanced behind Oracle Traffic Director); Oracle 19c Enterprise Edition with Data Guard physical-standby on OCI; Argus Mart for analytics / signal detection; Argus Interchange (E2B(R3) gateway) connected to EudraVigilance (EMA), FAERS (FDA), PMDA Gateway, Health Canada CESG, and DACH national CAs (BfArM, PEI, Swissmedic, AGES); MedDRA (current version, controlled-version policy) and WHO Drug (latest annual release) dictionaries; configuration of case workflow, reporting rules, expedited / aggregate reporting templates; integrations with the EDC (Medidata Rave) for SAE / SUSAR reconciliation, the clinical-trial CTMS (Veeva Vault CTMS) for trial-product master, the eTMF (Veeva Vault eTMF), the IDMP / xEVMPD product-master (EMA SPOR + site MPI), the literature-surveillance service (Embase + PubMed + national journals), and the partner-exchange platform; SSO via Okta SAML 2.0 + MFA.

**Out of scope:** Oracle infrastructure (vendor-managed on OCI per master agreement); customer / patient call-centre systems (separate URS); medical-information request management (separate URS); pre-clinical safety; commercial CRM.

## 3. System Description and Intended Use

Argus is the global system of record for ICSRs covering spontaneous (post-marketing), clinical-trial (SUSAR + non-serious AE), literature, solicited (patient-support programmes), partner-exchange (license / co-development partners), and regulator-feedback (EVDAS, FAERS query) sources. Cases enter through validated intake adapters, are MedDRA- / WHO-Drug-coded, medically assessed for seriousness / causality / expectedness against the company's product-specific Reference Safety Information (RSI), approved by a QPPV designee, and reported (expedited or aggregate) to global regulators per the applicable jurisdictional timelines (FDA 7-day for fatal/life-threatening unexpected, 15-day for serious unexpected, 30-day for non-serious in periodic; EU EudraVigilance 15-day for serious unexpected; PMDA per local rules; DACH national CAs per BfArM / PEI / Swissmedic / AGES requirements). Aggregate reports (PSUR / PBRER / PADER / DSUR) are produced on schedule per the EU RMP, FDA REMS, and clinical-development plans.

The system also supports signal detection (EVDAS-aligned EBGM + PRR + ROR; internal SAS / Empirica integration), signal management (per GVP Module IX), Risk Management Plan execution (EU RMP + US REMS commitments), Pediatric Investigation Plan tracking (Reg. 1901/2006), and IDMP / xEVMPD product-master integration with EMA SPOR.

GAMP Cat 4: Oracle maintains the platform under their published SDLC (Argus 8.4.1 quarterly patches + annual feature releases); Oracle's customer-shared CSV evidence is reviewed annually under site vendor assurance. Site validation focuses on configuration of workflow / coding / reporting rules, integration boundaries, and 21 CFR Part 11 / EU GVP controls. No site-authored custom code (any need would trigger a separate Cat-5 sub-component validation under change control).

## 4. User Roles

| Role | Permissions | SoD constraint |
|---|---|---|
| Case Intake Operator | Create / triage cases; assign to processor queue; cannot medically assess. | ≠ Reviewer, Approver, Submission Operator |
| Case Processor | Code (MedDRA / WHO Drug), narrate, complete demographic / product / event fields. | ≠ Medical Reviewer, Approver of same case |
| Medical Reviewer | Assess seriousness, causality, expectedness; assess listedness against RSI; cannot self-approve. | ≠ Case Processor, Approver of same case |
| Medical Approver / QPPV Designee | Approve case for submission; sign-off triggers expedited submission. | ≠ Processor, Reviewer of same case |
| QPPV | Overall pharmacovigilance accountability; periodic-review sign-off; signal-management decisions. | Statutory role per GVP Module I |
| Deputy QPPV | QPPV back-up with documented delegation authority. | Cannot delegate QPPV's statutory sign-offs |
| Signal Reviewer | Triage signals (EBGM / PRR / ROR alerts + qualitative); cannot close signals. | ≠ Signal Closer |
| Signal Manager | Disposition signals; sign-off signal-closure records. | ≠ Signal Reviewer of same signal |
| RMP / REMS Author | Author / update Risk Management Plan / REMS commitments. | ≠ RMP Approver |
| RMP / REMS Approver | Approve RMP / REMS submission. | ≠ Author |
| Submissions Specialist | Generate / submit E2B(R3); reconcile acks; cannot edit case content. | ≠ Case Processor / Reviewer |
| PSUR / PBRER Author | Author aggregate reports; cannot approve. | ≠ PSUR Approver |
| PSUR / PBRER Approver | Approve aggregate reports for submission. | ≠ PSUR Author |
| Pediatric / PIP Coordinator | Maintain PIP commitments; cross-reference cases. | Read-only on case content |
| IDMP / xEVMPD Steward | Maintain product master, IDMP attributes, SPOR linkages. | ≠ Case Approver |
| Literature Surveillance Reviewer | Triage literature hits; create cases as appropriate. | ≠ Case Approver |
| Argus Administrator | Manage configuration, workflows, reporting rules; cannot approve cases. | ≠ Approver, Submissions Specialist |
| Auditor / Inspector | Read-only across cases, audit trails, submissions, reports. | Read-only |

**Separation of duties:** Case Processor ≠ Medical Reviewer ≠ Approver of the same case; Argus Administrator cannot approve cases; Signal Reviewer ≠ Signal Manager on the same signal; RMP Author ≠ RMP Approver. QPPV may not be the Argus Administrator. The Deputy QPPV may execute QPPV responsibilities only when QPPV unavailability has been recorded in the delegation register.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` direct GxP impact / `R2` indirect / `R3` none), and a verifiable `shall`-clause.

### 5.1 Platform, Infrastructure, and Configuration Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | The system shall run on a minimum of N+1 active Argus application servers (3 active + 1 hot standby) behind a load-balancer with health-check-based promotion; Oracle 19c Enterprise Edition shall run with Data Guard physical-standby in async mode. |
| URS-PLAT-02 | H | R1 | A DR site shall be maintained as a warm replica with RPO ≤ 15 min and RTO ≤ 4 h during full-site failover, validated annually under a documented DR runbook with end-to-end gateway resubmission. |
| URS-PLAT-03 | H | R1 | All configuration baselines (workflow definitions, reporting rules, MedDRA / WHO Drug version bindings, gateway profiles, role definitions) shall be version-controlled in the site config-repository; production changes shall be made only via approved change requests with rollback plan. |
| URS-PLAT-04 | H | R1 | Argus Mart shall be configured as a read-replica datamart fed by Oracle GoldenGate with verified latency ≤ 15 min and reconciliation reports daily. |
| URS-PLAT-05 | M | R2 | Vendor patches (Argus 8.4.1.x quarterly + critical out-of-band) shall be triaged within 14 days, classified per change-impact, and promoted under change control with regression-test pack execution. |
| URS-PLAT-06 | H | R1 | Environments shall be DEV → QC → UAT → PROD with refresh-from-prod data masking enforced for non-PROD; live patient identifiers shall not exist outside PROD. |
| URS-VND-01 | H | R1 | Oracle shall be qualified as a critical SaaS / on-prem vendor with SOC 2 Type II, ISO 27001, customer-shared CSV evidence, and a documented MSA + DPA; re-qualified annually with documented review by Vendor Assurance + CSV Architect. |
| URS-VND-02 | H | R1 | Oracle Argus release notes shall be reviewed and impact-assessed within 14 days of vendor release; configuration-affecting changes shall trigger re-validation. |
| URS-VND-03 | M | R2 | Annual Oracle audit summary (TR-Audit) shall be reviewed and filed in the Vendor Assurance dossier. |
| URS-CFG-01 | H | R1 | Per-product configuration (RSI association, listedness rules, expedited-reporting jurisdictional matrix, MedDRA version pinning) shall follow DRAFT → REVIEW → APPROVED → EFFECTIVE; SoD-enforced signatures. |
| URS-CFG-02 | H | R1 | Configuration changes shall be exportable as version-stamped artefacts for inspection; the configuration history shall be auditable. |
| URS-CFG-03 | M | R2 | A site-defined configuration-change-management runbook shall govern releases of reporting rules, with re-baseline and OQ-replay required after rule-engine changes affecting jurisdictional submission. |

### 5.2 Case Intake, Triage, and Workflow

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CASE-01 | H | R1 | Cases shall be created from any of the following intake channels: manual entry UI, E2B(R3) inbound via Argus Interchange, EDC reconciliation feed (Medidata Rave), literature-surveillance import, partner-exchange (license / co-development), patient-support-programme intake, regulator-feedback (e.g., EVDAS query) — each intake event recorded with channel + source-id + intake-timestamp. |
| URS-CASE-02 | H | R1 | Each case shall be assigned a unique, monotonic case ID, intake date, awareness date, source country, reporter type (HCP / consumer / regulator / partner / literature / clinical-trial), product(s), and triage classification (serious / non-serious; expedited-eligible per jurisdiction). |
| URS-CASE-03 | H | R1 | Workflow lifecycle shall be {Intake → Triaged → Coded → Medically Assessed → Approved → Submitted → Closed} with auto-locked terminal states; reverse transitions shall require captured reason + electronic signature; reverse-transition events shall be audit-trailed. |
| URS-CASE-04 | H | R1 | Reporting clocks shall be calculated from awareness date per applicable jurisdiction (FDA 7-day fatal/life-threatening unexpected, 15-day serious unexpected, 30-day periodic; EU EudraVigilance 15-day serious unexpected, 90-day non-serious; PMDA per local rules; DACH per BfArM/PEI/Swissmedic/AGES); the system shall raise pre-deadline alerts at D-3, D-1, D0. |
| URS-CASE-05 | H | R1 | Reclassification (e.g., non-serious → serious, expected → unexpected) shall trigger automatic reporting-clock recalculation and re-routing to the Medical Reviewer; the reclassification event shall be audit-trailed with reason. |
| URS-CASE-06 | H | R1 | Follow-up information arriving after submission shall be captured as a new case version; the version delta shall be auto-computed and used to determine whether an E2B(R3) follow-up submission is required. |
| URS-CASE-07 | H | R1 | Duplicate-case detection shall run on intake against a configurable rule set (reporter + patient identifiers + event PT + onset date proximity); suspected duplicates shall be routed to a Senior Case Processor for merge decision. |
| URS-CASE-08 | M | R2 | Case priority shall be auto-assigned (high / medium / normal) per a configurable matrix; high-priority cases shall be routed to a dedicated processor queue. |
| URS-CASE-09 | M | R2 | Case workload balancing shall distribute cases across regional hubs (Dublin / Basel / München / Wien) with overflow rules to maintain reporting-clock margin. |
| URS-CASE-10 | M | R2 | Case-state transitions shall emit events to a downstream operational analytics topic for KPI dashboards (cycle-time per state, expedited-eligible margin). |

### 5.3 Coding — MedDRA, WHO Drug, and Dictionary Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CODE-01 | H | R1 | MedDRA coding shall use the protocol- / product-applicable MedDRA version (configured at the product master); auto-coding suggestions shall be logged with confidence indicator; manual override shall require captured reason and shall be audit-trailed. |
| URS-CODE-02 | H | R1 | MedDRA coding shall be performed at the LLT level with PT auto-derived; SOC / HLGT / HLT shall be auto-populated from the chosen LLT; coder shall confirm preferred term (PT). |
| URS-CODE-03 | H | R1 | WHO Drug coding shall identify suspect / concomitant / interacting products with valid drug-record-number identifiers; uncoded products shall block case approval; ATC classification shall be auto-derived. |
| URS-CODE-04 | H | R1 | MedDRA version upgrade (typically twice-yearly per MSSO release schedule) shall be managed via a controlled annual / semi-annual process: impact-assessment template; open-case impact analysis; cut-over plan; rollback plan; approval by QPPV designee + Head of PV. |
| URS-CODE-05 | H | R1 | On MedDRA version upgrade, open cases not yet medically assessed shall be re-coded using the new version; cases already medically assessed shall retain their version-of-record per the company policy, with the new-version equivalent recorded as metadata. |
| URS-CODE-06 | H | R1 | WHO Drug annual release shall be impact-assessed and migrated under change control; ATC reassignments shall be tracked and flagged in trending. |
| URS-CODE-07 | M | R2 | Coding QC shall be performed by a sample-based audit (≥ 2% of cases per month); discrepancies shall feed coder training and trigger root-cause review. |
| URS-CODE-08 | M | R2 | Auto-coding suggestion quality (acceptance rate, override rate per LLT) shall be reported quarterly to the Coding Manager. |
| URS-CODE-09 | H | R1 | A controlled list of company-preferred terms for ambiguous LLTs (e.g., "rash" mapping disambiguation) shall be maintained; auto-coding shall consult the list and surface preferred mapping. |

### 5.4 Medical Assessment and Approval

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ASSESS-01 | H | R1 | Medical Reviewer shall assess seriousness per ICH E2A criteria (death, life-threatening, hospitalisation, persistent disability, congenital anomaly, medically important); the assessment shall be a structured field, not free-text only. |
| URS-ASSESS-02 | H | R1 | Causality shall be assessed against the company's product-specific Reference Safety Information (RSI) using a structured framework (e.g., WHO-UMC causality categories: certain, probable/likely, possible, unlikely, conditional, unassessable). |
| URS-ASSESS-03 | H | R1 | Expectedness / listedness shall be assessed against the RSI; the system shall surface the applicable RSI version-of-record at assessment time. |
| URS-ASSESS-04 | H | R1 | Approval to submit shall require the QPPV designee's electronic signature with re-authentication per § 11.200; the signature shall be cryptographically bound to the case state at signing time. |
| URS-ASSESS-05 | H | R1 | Reclassification (e.g., non-serious → serious, expected → unexpected) shall trigger reporting-clock recalculation, case re-routing, and audit-trail capture of the reclassification rationale. |
| URS-ASSESS-06 | H | R1 | The Medical Reviewer's assessment shall include a Company Assessment narrative and a Reporter's Assessment narrative; both shall be preserved with no overwriting. |
| URS-ASSESS-07 | H | R1 | Assessment of paediatric cases shall surface the applicable PIP and any pediatric-specific listedness considerations. |
| URS-ASSESS-08 | M | R2 | Medical Reviewer assignment shall account for therapeutic-area expertise and language coverage (DE / FR / IT for DACH cases). |
| URS-ASSESS-09 | M | R2 | The Medical Reviewer's time-in-state shall be measured; cases approaching reporting-clock margin shall be auto-escalated to a back-up reviewer. |

### 5.5 Submissions and Reporting (E2B(R3) per ICH M2 + Gateway)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SUB-01 | H | R1 | The system shall generate E2B(R3) ICSR XML compliant with the ICH M2 ESTRI standard and the agency-specific implementation guides (EMA EudraVigilance, FDA FAERS, PMDA, Health Canada CESG); schema validation shall execute pre-send and rejection shall block transmission with structured error mapping. |
| URS-SUB-02 | H | R1 | E2B(R3) generation shall populate all mandatory elements per ICH E2B(R3) sections (C.1 Identification, C.2 Primary Source, C.3 Sender, C.4 Literature, C.5 Study Identification, D Patient, E Reaction/Event, F Test/Procedure, G Drug, H Narrative); element optionality shall be enforced per the receiving agency's profile. |
| URS-SUB-03 | H | R1 | Submissions shall be transmitted via Argus Interchange to the appropriate gateway (EudraVigilance EMA Gateway, FDA ESG, PMDA Gateway, Health Canada CESG, BfArM / PEI / Swissmedic / AGES national gateways); ack messages (ACK-1 transport ack, ACK-2 application ack, ACK-3 business response) shall be matched to the case and audit-trailed. |
| URS-SUB-04 | H | R1 | Negative ack (`ICSR rejected`) shall raise a structured Exception with error-code mapping; corrective action and resubmission shall occur within the regulator's grace period; if grace breached, escalation to QPPV shall be automatic. |
| URS-SUB-05 | H | R1 | Periodic reports (PSUR / PBRER, PADER, DSUR) shall be produced on configured schedules from validated data sets; report queries shall be version-controlled and the underlying data set shall be timestamped with a data-cut and dataset checksum. |
| URS-SUB-06 | H | R1 | E2B(R3) nullFlavor and dataElementOmissionReason handling shall be standards-compliant per ICH M2 and shall not silently emit empty elements. |
| URS-SUB-07 | H | R1 | Re-transmissions (initial → follow-up → nullification) shall maintain ICSR identifier continuity and version sequencing per ICH E2B(R3) §C.1.8; nullification reasons shall be captured. |
| URS-SUB-08 | M | R2 | Submission throughput shall sustain a peak rate of ≥ 500 ICSRs / hour to a single gateway without queue backlog growth. |
| URS-SUB-09 | M | R2 | Submission scheduling shall avoid agency-specified maintenance windows; the agency-window calendar shall be configurable. |
| URS-SUB-10 | M | R2 | Re-submission retry shall use exponential backoff with a hard cap; manual intervention shall be required after retry exhaustion. |

### 5.6 Aggregate Reporting — PSUR / PBRER / PADER / DSUR

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AGG-01 | H | R1 | PSUR / PBRER shall be generated per ICH E2C(R2) on the EU Reference Date schedule with body / appendices auto-populated from the safety database, with manual sections (executive summary, integrated benefit-risk evaluation) authored in the report module. |
| URS-AGG-02 | H | R1 | PADER (FDA, 21 CFR 314.80(c)(2)) shall be generated quarterly for the first 3 years post-approval and annually thereafter, per product. |
| URS-AGG-03 | H | R1 | DSUR (ICH E2F) shall be generated annually per investigational product per the IND / CTA Development International Birth Date (DIBD). |
| URS-AGG-04 | H | R1 | All aggregate-report data extracts shall be reproducible: data-cut date, dictionary versions (MedDRA / WHO Drug), and dataset checksum shall be stamped on the report. |
| URS-AGG-05 | H | R1 | Aggregate-report approval shall require dual signature (Author + Approver) plus QPPV countersign for EU PSUR / PBRER. |
| URS-AGG-06 | H | R1 | Submission of PSUR / PBRER shall be via the EMA PSUR Repository per the EU single-assessment process; legacy national submissions shall be supported during transition. |
| URS-AGG-07 | M | R2 | Aggregate-report templates shall be version-controlled and changes shall be assessed for impact on prior reporting periods. |
| URS-AGG-08 | M | R2 | Aggregate-report drafts shall be exportable in PDF/A-3 with embedded XML for downstream archival. |

### 5.7 Signal Detection and Management (EU GVP Module IX)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SIG-01 | H | R1 | The system shall support quantitative signal detection on internal data with statistical methods including PRR (Proportional Reporting Ratio), ROR (Reporting Odds Ratio), and EBGM (Empirical Bayes Geometric Mean); thresholds shall be configurable per drug-event combination and per product. |
| URS-SIG-02 | H | R1 | The system shall integrate with EVDAS for the EudraVigilance signal-detection outputs per EU GVP Module IX; EVDAS alerts shall be triaged in the same signal-management workflow. |
| URS-SIG-03 | H | R1 | Qualitative signal detection (aggregate-report scrutiny, literature triage, regulator queries, partner reports) shall be supported via a signal-of-interest entry channel. |
| URS-SIG-04 | H | R1 | Signal-management workflow shall enforce: Signal Validation → Signal Confirmation → Signal Prioritisation → Signal Assessment → Signal Recommendation → Signal Closure, per GVP Module IX. |
| URS-SIG-05 | H | R1 | Signal Closer (Signal Manager role) shall not have authored or reviewed the same signal; auto-close on time-out shall be prohibited. |
| URS-SIG-06 | H | R1 | Signal-management decisions shall require a documented evidence basis (assessment report referencing the cases / aggregate data / literature behind the signal). |
| URS-SIG-07 | H | R1 | Signal-management outcomes that change product labelling (RSI / SmPC update, RMP amendment, REMS update) shall feed the Regulatory Affairs labelling-change workflow. |
| URS-SIG-08 | M | R2 | Signal-management performance KPIs (time to validation, time to assessment, time to closure) shall be reported monthly to the QPPV. |
| URS-SIG-09 | M | R2 | The signal-detection algorithm pack (PRR / ROR / EBGM thresholds + filters) shall be version-controlled; algorithm changes shall be re-validated under OQ. |

### 5.8 Risk Management Plan (EU RMP) and REMS

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RMP-01 | H | R1 | Per-product Risk Management Plan (EU RMP per GVP Module V) shall be maintained with version history; RMP commitments (additional risk minimisation measures, additional PV activities, PASS studies) shall be tracked with due-dates. |
| URS-RMP-02 | H | R1 | RMP updates shall be triggered by signal-closure outcomes, regulator requests, and PSUR / PBRER conclusions; the trigger shall be auditable. |
| URS-RMP-03 | H | R1 | US REMS (where applicable) shall be maintained with REMS Document, REMS Assessment Reports schedule, and REMS modification history. |
| URS-RMP-04 | H | R1 | RMP / REMS commitment-status reporting shall be available for QPPV / Reg Affairs at any time; overdue commitments shall raise alerts. |
| URS-RMP-05 | M | R2 | RMP educational-material distribution tracking (HCP brochures, patient cards) shall be integrated with the Vendor Assurance for the print/distribution vendor. |
| URS-RMP-06 | M | R2 | Post-Authorisation Safety Study (PASS) plans and milestones shall be tracked, with study-completion data flowing into PSUR / PBRER input. |

### 5.9 Pediatric Investigation Plan (PIP)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PIP-01 | H | R1 | Per-product Pediatric Investigation Plan (EU Reg. 1901/2006) shall be maintained with milestone tracking; PIP modifications shall be version-controlled. |
| URS-PIP-02 | H | R1 | Cases involving paediatric patients (age groups: preterm newborn, term newborn, infant + toddler, child, adolescent per ICH E11) shall be tagged and surfaced in PIP-context reporting. |
| URS-PIP-03 | M | R2 | PIP-derived data shall feed PSUR / PBRER paediatric sections and DSUR paediatric appendices. |

### 5.10 IDMP / xEVMPD Product Master Integration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-IDMP-01 | H | R1 | The product master shall hold ISO 11238 (substances), ISO 11239 (dose forms / units), ISO 11240 (units of measure), ISO 11615 (medicinal products), ISO 11616 (pharmaceutical products) identifiers; identifiers shall be reconciled against EMA SPOR. |
| URS-IDMP-02 | H | R1 | Product master updates shall be performed under change control with SoD between Steward and Approver; updates shall propagate to open and historical cases per a defined policy (open cases re-coded; historical cases preserved with current-version cross-reference). |
| URS-IDMP-03 | H | R1 | xEVMPD submissions to EMA shall be supported for products / authorisations within EU; XEVPRM transactions (initial / variation / nullification) shall be tracked with EMA ack reconciliation. |
| URS-IDMP-04 | M | R2 | IDMP referential drift (e.g., SPOR substance update) shall be detected by a quarterly reconciliation job; impact assessment shall be opened for any in-scope product. |

### 5.11 Literature Surveillance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LIT-01 | H | R1 | A weekly literature-surveillance feed shall scan Embase + PubMed + the local-language regional journals defined per product (DE Arzneimittelbrief, AT Pharmazeutische Mitteilungen, CH Schweizerische Ärztezeitung, FR Prescrire) with configurable search strategies per product. |
| URS-LIT-02 | H | R1 | Surveillance hits shall be triaged in a structured workflow; eligible hits shall result in ICSR creation with literature as the source channel and the citation captured per ICH E2B(R3) §C.4. |
| URS-LIT-03 | M | R2 | Search strategies shall be version-controlled; periodic search-strategy reviews shall be performed annually. |
| URS-LIT-04 | M | R2 | False-positive / true-positive rates per search strategy shall be measured to support strategy tuning. |

### 5.12 Partner-Exchange Agreements

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PEX-01 | H | R1 | Per-partner Pharmacovigilance Agreement (PVA / SDEA) shall be loaded into the system with key parameters (exchange timelines, scope of products, partner-side QPPV contact, jurisdictions); the partner profile shall drive the Argus Interchange exchange behaviour. |
| URS-PEX-02 | H | R1 | Inbound partner-exchange E2B(R3) shall be auto-processed with idempotent case-creation (preventing duplicate cases when partners forward the same source case); outbound exchange shall match the PVA-stipulated timeline. |
| URS-PEX-03 | M | R2 | Partner-exchange-event audit-trail shall include partner-id, direction (inbound / outbound), exchange timestamp, ack status, and PVA-clause cross-reference. |
| URS-PEX-04 | M | R2 | Partner KPI dashboard shall report timeliness and quality (% rejected, % corrected) per partner. |

### 5.13 Audit Trail (per 21 CFR § 11.10(e))

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Per § 11.10(e), the audit trail shall capture every case content change, coding decision, assessment, signature event, configuration change, submission event, and reporting-clock recalculation with actor, action, old value, new value, reason-for-change, and timestamp. |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only at the database level (DELETE / UPDATE revoked on audit tables; DBA dual-control on DDL); the application API shall expose read + insert only. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be performed per the PV QA plan: case-level event-driven review at approval; platform-level review quarterly; evidence filed in the QA dossier. |
| URS-AUD-04 | H | R1 | Audit-trail retention shall meet the maximum of all applicable jurisdictional requirements: ≥ 50 years for EU-marketed products per GVP Module II; ≥ life-of-product + 10 years for US; ≥ life-of-product + 35 years for paediatric ICH M11; immutable cold storage with object-lock. |
| URS-AUD-05 | M | R2 | Audit-trail event volume shall be monitored; sudden spikes (e.g., bulk-update events) shall raise alerts. |
| URS-AUD-06 | M | R2 | Audit-trail exports shall be reproducible with cryptographic hash for inspector handover. |

### 5.14 21 CFR Part 11 (sub-section-explicit per METHODOLOGY § 2A.2)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a), procedures and controls protecting electronic-record validity (cases, signatures, audit, submissions) shall be documented and reviewed annually. |
| URS-PART11-02 | H | R1 | Per § 11.10(b), the system shall generate accurate and complete copies of records suitable for inspection (PDF representations of cases, E2B XML, audit-trail extracts). |
| URS-PART11-03 | H | R1 | Per § 11.10(c), records shall be protected throughout the retention period; storage shall use checksum-protected immutable archives. |
| URS-PART11-04 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via Okta SAML 2.0 + MFA; service-account access via mTLS only. |
| URS-PART11-05 | H | R1 | Per § 11.10(e), the operational audit trail per § 5.13. |
| URS-PART11-06 | H | R1 | Per § 11.10(g), authority checks shall enforce role-based permissions at the workflow / API layer. |
| URS-PART11-07 | H | R1 | Per § 11.10(k), system operation manuals shall be controlled documents and shall be revised under change control with version-traceable change records. |
| URS-PART11-08 | H | R1 | Per § 11.50, signature events shall render printed name, date / time of signing, and meaning of signature into the audit trail and into PDF representations of the case. |
| URS-PART11-09 | H | R1 | Per § 11.70, signatures shall be cryptographically linked (HMAC-SHA-256 over record-hash + signer-id + timestamp) to the signed record; tampering shall be detectable on read. |
| URS-PART11-10 | H | R1 | Per § 11.100, signature uniqueness shall be enforced; deactivated user-ids shall never be reassigned. |
| URS-PART11-11 | H | R1 | Per § 11.200, re-authentication (password + MFA) shall be required at every critical signature event (case approval, RMP / REMS approval, aggregate-report approval, signal-closure); cached credentials shall be rejected at signing time. |
| URS-PART11-12 | H | R1 | Per § 11.300, password / credential controls shall align with the site InfoSec policy (length ≥ 12, complexity, MFA, 90-day rotation, lockout after 5 failures). |
| URS-GVP-01 | H | R1 | The system shall support GVP Module II §VI.B.6 — record-retention, audit-readiness, business-continuity expectations; mapped in the Pharmacovigilance System Master File (PSMF). |
| URS-GVP-02 | H | R1 | The system shall support GVP Module I PV organisational requirements: QPPV documented designation; Deputy QPPV; PSMF maintenance with chapter-version control. |
| URS-GVP-03 | H | R1 | The system shall support GVP Module IX signal-management framework (URS-SIG-04 cross-reference). |
| URS-GVP-04 | M | R2 | The system shall support GVP Module XV safety communication (Dear Healthcare Professional Letters) tracking. |

### 5.15 DACH National Competent Authority Gateways

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-NCA-BFARM-01 | H | R1 | BfArM (DE) national gateway shall be supported for medicinal-product PV reporting per AMG § 63b/§ 63c; gateway connectivity tested quarterly; certificate rotation under change control. |
| URS-NCA-PEI-01 | H | R1 | Paul-Ehrlich-Institut (DE) gateway shall be supported for biological-medicinal-product PV reporting (vaccines, blood products, biosimilars); product-master shall route biologicals via PEI rather than BfArM. |
| URS-NCA-SWISS-01 | H | R1 | Swissmedic (CH) national gateway shall be supported per HMG / VAM PV reporting requirements; CH-specific timelines shall be configurable. |
| URS-NCA-AGES-01 | H | R1 | AGES PharmMed (AT) national gateway shall be supported per AMG (AT) PV reporting requirements. |
| URS-NCA-ROUTING-01 | H | R1 | Routing matrix shall direct each case to the correct combination of EudraVigilance + applicable national CAs based on country-of-incidence, product type (medicine / biological), and jurisdictional rules; routing changes shall be under change control. |
| URS-NCA-LANG-01 | M | R2 | DACH submission templates shall support de-DE, de-AT, de-CH, fr-CH, it-CH variants where required for FSN / DHCPL output. |

### 5.16 Clinical-Trial Safety (DSUR + CTR 536/2014 CTIS)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CT-SAFETY-01 | H | R1 | SUSAR identification per ICH E2A shall trigger expedited E2B(R3) submission to EudraVigilance (per EU CTR 536/2014) and FDA (per 21 CFR 312.32) and other CT-active jurisdictions within 7 days (fatal/life-threatening) or 15 days (other serious unexpected). |
| URS-CT-SAFETY-02 | H | R1 | DSUR generation per ICH E2F shall draw clinical-trial cases via the EDC (Medidata Rave) and CTMS (Veeva Vault CTMS) integration; data-cut shall be reproducible. |
| URS-CT-SAFETY-03 | H | R1 | EU CTR 536/2014 safety-reporting via CTIS (Clinical Trials Information System) shall be supported for EU clinical trials; CTIS submissions shall be tracked with ack reconciliation. |
| URS-CT-SAFETY-04 | M | R2 | Blinding-status handling shall preserve trial blind on cases requiring unblinding for regulatory reporting (controlled unblinding workflow). |
| URS-CT-SAFETY-05 | M | R2 | EU CTR 536/2014 Annual Safety Report (ASR per the CTR) shall be generated annually per ongoing clinical trial; trial-level safety summary tabulations shall be reproducible. |

### 5.17 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | **Attributable:** Every record / change shall be attributable to a named user (or service-account for system events); audit-write DB constraint prevents null actor. |
| URS-DI-02 | H | R1 | **Legible:** Records shall be exportable as human-readable PDF/A-3 and machine-readable E2B(R3) XML; rendering verified under OQ. |
| URS-DI-03 | H | R1 | **Contemporaneous:** Events shall be recorded at the time of occurrence with server-side NTP-synced timestamps; retroactive entries shall be flagged with delay reason. |
| URS-DI-04 | H | R1 | **Original:** Source case content shall be preserved unaltered; corrections shall be recorded as new versions with reason; reconstruction-of-event order possible from audit trail. |
| URS-DI-05 | H | R1 | **Accurate:** Reporting-clock calculations and aggregate-report data extracts shall be deterministic and validated under OQ. |
| URS-DI-06 | H | R1 | **Complete:** All mandatory fields per receiving-agency E2B(R3) profiles shall be enforced before submission. |
| URS-DI-07 | H | R1 | **Consistent:** Chronological order DB-enforced; coding decisions consistent across cases (same LLT → same PT via MedDRA). |
| URS-DI-08 | H | R1 | **Enduring:** ≥ 50-year EU retention enforced at archive tier; immutable cold storage with object-lock. |
| URS-DI-09 | H | R1 | **Available:** Retrieval ≤ 4 h during regulatory inspection windows; documented retrieval runbook. |

### 5.18 Security, Privacy, Performance, Availability, Backup

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | Authentication via Okta SAML 2.0 + MFA; service-account access via mTLS only. |
| URS-SEC-02 | H | R1 | Role-based access; cases shall be restricted by region / product / partner where partner agreements or local data-protection rules require. |
| URS-SEC-03 | H | R1 | GDPR (Reg. (EU) 2016/679) Arts. 6 + 9 + 32 + 35: subject identifiers shall be minimised in narratives per the company SOP; cross-border transfers shall be governed by SCCs or DPF; DPIA on file for the PV system. |
| URS-SEC-04 | H | R1 | HIPAA (US) and PIPEDA (Canada) compliance for relevant cases; data-residency rules enforced via tenant-region binding. |
| URS-SEC-05 | M | R2 | Vulnerability scans monthly; critical findings remediated within 30 days under change control. |
| URS-SEC-06 | M | R2 | Annual penetration test; high / critical findings remediated under change control. |
| URS-SEC-07 | M | R2 | Data-loss-prevention (DLP) controls shall block bulk export of identifiable case data without authorised approval. |
| URS-PERF-01 | M | R2 | Case-page navigation latency shall be ≤ 3 s at the 95th percentile under peak load (250 concurrent processors during pandemic-scale safety surges). |
| URS-PERF-02 | M | R2 | E2B(R3) generation latency shall be ≤ 10 s per case at the 95th percentile. |
| URS-PERF-03 | M | R2 | PSUR / PBRER full-extract job shall complete in ≤ 4 h for a 5-year reporting period on a flagship product. |
| URS-AV-01 | H | R1 | Availability ≥ 99.5% during business hours; 24×7 for the gateway during regulatory submission windows; uptime probes 24×7. |
| URS-AV-02 | H | R1 | RPO ≤ 15 min; RTO ≤ 4 h; annual full DR test including end-to-end gateway resubmission. |
| URS-BAK-01 | H | R1 | Oracle nightly backup + continuous archived redo logs; retention ≥ 50 years; immutable cold storage with object-lock. |
| URS-BAK-02 | H | R1 | Annual full DR test, including end-to-end gateway resubmission; results filed in `RUN-DR-NNN`. |
| URS-BAK-03 | M | R2 | Quarterly partial DR rehearsal (single regional hub + single gateway) shall be performed without taking PROD down. |

### 5.19 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Production access shall require recorded role-specific training (LMS) plus PV-specific competency assessment; PV-specific competency for Medical Reviewers shall be re-attested annually. |
| URS-TRN-02 | H | R1 | Annual refresher for medical reviewers and QPPV designees shall cover current GVP module updates, FDA post-marketing guidance updates, ICH-revision updates (e.g., E2B(R3) implementation notices), and EVDAS / FAERS technical changes. |
| URS-TRN-03 | M | R2 | DACH-specific training shall cover BfArM, PEI, Swissmedic, AGES PV-reporting nuances and DACH-language case-handling. |
| URS-PR-01 | H | R1 | Annual periodic review shall cover: configuration drift, audit-trail review evidence, MedDRA / WHO Drug version status, gateway connectivity tests, signal-management metrics, RMP / REMS commitment status, PIP commitment status, IDMP / xEVMPD reconciliation status, partner-PVA currency, deviation summary, training currency, fitness for use; signed by Head of PV Operations + QPPV + VP QA. |
| URS-PR-02 | M | R2 | Quarterly PV operational review (cycle-time KPIs, reporting-clock margin distribution, gateway ack rates) shall be reviewed by Head of PV Operations + QPPV. |

### 5.20 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is SAML 2.0 via Entra ID with SCIM lifecycle provisioning; conditional-access policy `PV-Sensitive Conditional Access (FIDO2 phishing-resistant MFA + named-location enforcement)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with Oracle RMAN for the Argus Oracle backend; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 30 y (PV) per the consuming-record schedule. |

### 5.21 Cross-System Integration — Hydra PV GenAI + Helios

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HYD-01 | H | R1 | GenAI triage of adverse-event case narratives shall be invoked exclusively via the Hydra GenAI Gateway (`HYD2-URS-GENAI-001`); direct calls to vendor LLM endpoints (Anthropic, OpenAI, etc.) from the Argus tenant shall be technically prohibited at the egress firewall. |
| URS-XINT-HYD-02 | H | R1 | Each PV GenAI use case shall pass the Hydra per-use-case classification gate per Hydra URS-UC-CLASS-*; PV-triage shall be declared EU AI Act Annex I high-risk (2027 deadline) and shall not run in production without a signed Art. 11 + Annex IV pack stored against the use-case ID. |
| URS-XINT-HYD-03 | H | R1 | Every Hydra-mediated PV triage suggestion shall be reviewed by a qualified PV case-processor before any regulatory submission timer is decremented; bulk-acceptance of AI suggestions on PV cases shall be technically prevented; HITL evidence shall be retained ≥ 30 y. |
| URS-XINT-HYD-04 | H | R1 | Serious-incident routing for PV GenAI use cases shall traverse the Hydra Art. 73 routing service (Hydra URS-ART73-*) with the underlying-product incident channel (EU MDR Art. 87 for medical devices, EU GMP defect channel via the Manufacturing Authorisation Holder for medicinal products) cross-referenced. |
| URS-XINT-HYD-05 | H | R1 | Inference events (prompt, retrieval context hash, model_version, response, watermark, HITL user, HITL action) shall be forwarded to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract within 5 minutes. |

### 5.22 Cross-System Integration — Helios audit-trail handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HEL-01 | H | R1 | Argus PV shall publish audit-trail events (Case lifecycle, expectedness assessment, reporting timer, and follow-up-report events) to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract (JSON Lines, schema-registry pinned, Kafka topic `helios.ingest.sirius.argus.v1`) within 5 minutes of event capture; 21 CFR § 11.10(e) audit-trail completeness shall be preserved end-to-end so that no event class is lost at the boundary. |
| URS-XINT-HEL-02 | H | R1 | Pre-handover audit-trail retention on the Argus PV side shall be ≥ 30 y regardless of Helios availability; once Helios acknowledges ingest (per-message ack with idempotency key), Helios is the system-of-record for review and the Argus PV local copy serves as the durability backstop until the local retention floor expires. |

### 5.23 Cross-System Integration — LMS competence handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-LMS-01 | H | R1 | PV case-processors and medical reviewers shall pass an LMS competence check (curriculum `PV-CASE-PROC-v1.x` / `PV-MEDREV-v1.x`) before being assigned to a case; LMS competence shall be re-checked at every assignment; non-current users shall be blocked from case assignment with the lapse logged in the Argus audit trail. |

## 6. Acceptance Criteria

The system enters validated GxP use when CS, RA, IQ (vendor-shared from Oracle + site supplementary), OQ, PQ are approved and executed; PQ shall include representative end-to-end scenarios covering:

1. ICSR intake (manual + E2B-in + EDC reconciliation + literature + partner-exchange) → MedDRA / WHO Drug coding → medical assessment → QPPV-designee approval → E2B(R3) submission → ack reconciliation across all configured gateways (EudraVigilance, FAERS, PMDA, Health Canada, BfArM, PEI, Swissmedic, AGES).
2. Reclassification re-clock recalculation scenario (non-serious → serious).
3. MedDRA version-upgrade scenario (open-case re-coding policy).
4. Aggregate-report scenario (PSUR + PBRER + PADER + DSUR data-cut reproducibility).
5. Signal-detection scenario (EBGM / PRR / ROR threshold breach → signal-management workflow → closure).
6. RMP commitment overdue alert scenario.
7. DR failover with end-to-end gateway resubmission.
8. IDMP / xEVMPD update propagation scenario.

VSR approved by Head of PV Operations, QPPV, VP Drug Safety, VP QA; RTM shall map every URS-ID to ≥ 1 approved test case.

## 7. Constraints

- Vendor patches under change control; vendor releases not under site change control but evaluated within 14 days before promotion.
- MedDRA / WHO Drug upgrades managed annually (or semi-annually per MSSO release schedule) under change control.
- No site-authored custom code (Cat-4 only; any custom code requirement triggers a separate Cat-5 sub-component validation).
- QPPV signature authority cannot be delegated outside the named QPPV / Deputy QPPV roles.
- EUDAMED / EVDAS / FAERS gateway availability windows constrain submission timing; manual fallback documented.

## 8. Assumptions

- Oracle infrastructure (OCI) is qualified and operational.
- Okta IdP, Medidata Rave EDC, Veeva Vault CTMS / eTMF, MasterControl eQMS, EMA SPOR, EVDAS, FAERS, PMDA, HC, BfArM, PEI, Swissmedic, AGES gateways are operational and validated by their respective owners.
- Gateway certificates are rotated per the PV SOP under change control.
- MedDRA + WHO Drug subscriptions are current and licensed for the relevant population.
- IDMP / xEVMPD reference data from EMA SPOR is the authoritative external source.

## 9. References

### US

- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300 — Electronic Records; Electronic Signatures.
- 21 CFR 314.80 — Post-marketing reporting of adverse drug experiences.
- 21 CFR 600.80 — Post-marketing reporting of adverse experiences (biologicals).
- 21 CFR 312.32 — IND safety reporting.
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).
- FDA *Providing Postmarketing Periodic Safety Reports in the ICH E2C(R2) Format (PBRER)* (Guidance, 2016).
- FDA *Guidance for Industry: E2D Post-approval Safety Data Management* (2003).

### EU

- EU GMP Annex 11 §§ 4 (validation), 6 (accuracy), 9 (audit trail), 11 (periodic evaluation).
- EU GVP Modules I–XVI (esp. II PSMF, V RMP, VI Management and reporting of adverse reactions, VII PSUR, IX Signal management, XV Safety communication, XVI Risk minimisation measures).
- EU CTR Reg. 536/2014 + EU CTIS (Clinical Trials Information System).
- EU Reg. 1901/2006 — Pediatric Regulation (PIP).
- GDPR Reg. (EU) 2016/679 Arts. 6, 9, 32, 35.
- EMA EudraVigilance Specifications + EVDAS User Guide.
- EMA SPOR (Substances, Products, Organisations, Referentials) data services.

### DACH (per METHODOLOGY § 2A.6)

- **BfArM (DE)** — Bundesinstitut für Arzneimittel und Medizinprodukte; UAW-Meldewege per AMG § 63b/§ 63c.
- **Paul-Ehrlich-Institut (DE)** — federal authority for biological medicinal products + vaccines.
- **Swissmedic (CH)** — Schweizerisches Heilmittelinstitut; HMG / VAM PV reporting requirements.
- **AGES PharmMed (AT)** — Österreichische Agentur für Gesundheit und Ernährungssicherheit, PharmMed Division.

### International

- ICH E2A — Clinical Safety Data Management: Definitions and Standards for Expedited Reporting.
- ICH E2B(R3) — Electronic Transmission of Individual Case Safety Reports.
- ICH E2C(R2) — Periodic Benefit-Risk Evaluation Report (PBRER).
- ICH E2D — Post-Approval Safety Data Management: Definitions and Standards for Expedited Reporting.
- ICH E2E — Pharmacovigilance Planning.
- ICH E2F — Development Safety Update Report.
- ICH M1 — Medical Dictionary for Regulatory Activities (MedDRA).
- ICH M2 — Electronic Standards for the Transfer of Regulatory Information (ESTRI).
- ICH M11 — Clinical Electronic Structured Harmonised Protocol (paediatric retention reference).
- ISO 11238 (substances), ISO 11239 (dose forms / units), ISO 11240 (units of measure), ISO 11615 (medicinal products), ISO 11616 (pharmaceutical products) — IDMP.

### Industry guidance

- ISPE GAMP 5 (2nd Edition, 2022).
- PIC/S PI 041 — Good Practices for Data Management and Integrity in Regulated GMP/GDP Environments.
- ISO/IEC 27001:2022 — Information Security Management Systems.
- WHO-UMC causality assessment framework.

### Vendor

- Oracle — *Argus Safety 8.4.1 Installation, Configuration, and Administration Reference*.
- Oracle — *Argus Interchange E2B(R3) Implementation Guide*.
- Oracle — *Argus Mart Reporting User Guide*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

