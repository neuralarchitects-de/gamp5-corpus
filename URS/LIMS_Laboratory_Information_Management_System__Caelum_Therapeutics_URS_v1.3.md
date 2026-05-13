---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; expanded 2026-05-12 (T3 uplift, sub-section breakouts, ISO 17025 binding, OOS workflow per FDA OOS 2022, full §10 references)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed., 2022) Cat 4 conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "21 CFR Part 211 §§ .22, .68, .180, .192"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "PIC/S PI 041 Good Practices for Data Management and Integrity"
  - "USP <1058> Analytical Instrument Qualification"
  - "ISO/IEC 17025:2017 General Requirements for the Competence of Testing and Calibration Laboratories"
  - "ICH Q2(R2), ICH Q9(R1), ICH Q10"
  - "FDA Guidance for Industry: Investigating Out-of-Specification (OOS) Test Results for Pharmaceutical Production (2022)"
  - "ISPE GAMP Good Practice Guide: Validation of Laboratory Computerized Systems"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## LIMS — LabWare LIMS 8 with QM/ELN

**Document Number:** CTX-URS-LIMS-001
**Version:** 1.0
**Effective Date:** 2026-04-26 *(synthetic)*
**Site:** Caelum Therapeutics Inc., QC Operations, North Building, Cambridge, Massachusetts, USA *(fictional)*
**System Owner:** QC Informatics Lead
**Process Owner:** Head of QC
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (LabWare static configuration; project-specific LIMS Basic scripts assessed as Cat 5 sub-components under separate change control)
**Project Mode:** Configuration project on commercial software product **LabWare LIMS 8 with QM/ELN** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .22, .68, .180, .192; EU GMP Annex 11 §§ 4, 6, 9, 11; PIC/S PI 041; USP <1058>; ISO/IEC 17025:2017 (where contract-testing scope applies); ICH Q2(R2), Q9(R1), Q10

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (QC Informatics Lead) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — Head of QC) | _____________ | _____________ | _____ |
| Reviewer (Data Integrity Officer) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue (Tier T3 — 124 requirements covering sample lifecycle, method registry, instrument-data ingest, OOS/OOT workflow, stability, supplier qualification, multi-site, parser lifecycle, audit-trail review, ISO 17025). |

## Definitions

| Term | Definition |
|---|---|
| LIMS | Laboratory Information Management System |
| LabWare 8 | LabWare LIMS v8 (LIMS Basic configuration platform) |
| QM | Quality Management module of LabWare |
| ELN | Electronic Laboratory Notebook (LabWare ELN module) |
| MES / PAS-X | Manufacturing Execution System (PAS-X v3.2) |
| eQMS | MasterControl QMS |
| ERP | SAP S/4HANA |
| LIMS Basic | LabWare scripting language for site-specific extensions |
| Aliquot | Sub-sample created from a parent sample |
| COA | Certificate of Analysis |
| OOS / OOT / OOE | Out-of-Specification / Out-of-Trend / Out-of-Expectation |
| AIQ | Analytical Instrument Qualification per USP <1058> (categories A/B/C) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| Parser | An adapter that converts an instrument-data file into LIMS-structured results |
| EM | Environmental Monitoring |
| Method Registry | The controlled inventory of analytical methods, including version + status |

## 1. Purpose

This URS defines requirements for the LIMS used to manage the QC and contract-testing sample lifecycle (receipt → login → aliquot → storage → assignment → test execution → instrument-data ingest → calculation → review → approval → release → COA) for finished products, APIs, raw materials, packaging, stability, and environmental-monitoring samples at Caelum Therapeutics QC Operations.

## 2. Scope

**In scope:** LabWare LIMS 8 server cluster (3 active App Servers + 1 standby on RHEL 9.2), Oracle 19c with Data Guard physical-standby DR, LabWare web client, LabWare ELN + QM modules, LIMS Basic scripts implementing site-specific calculations / workflows, instrument-data parsers, integrations with PAS-X (MES), MasterControl (eQMS), SAP (ERP), instrument CDS systems (Empower, Chromeleon, Qtegra), the stability scheduler, the supplier-qualification module, the EM data-acquisition feed, AD federation via Keycloak, and the multi-site (Cambridge, MA + Basel, CH) federation of master data + cross-site result transfer.

**Out of scope:** instrument-side validation (per-instrument CSV); ERP master data; PAS-X internal CSV; non-GMP discovery analytics.

```
                    AD / SSO (Keycloak federation, multi-site)
                                │
                                ▼
   ┌─────────────────────────────────────────────────────────────┐
   │                     LabWare LIMS 8 (Cambridge primary)        │
   │ App Servers (3 active + 1 standby) │ Oracle 19c + Data Guard │
   │ QM module │ ELN module │ LIMS Basic │ Parser Lifecycle Mgr   │
   └──┬───────┬───────┬──────────┬──────────────┬──────────────┬──┘
      │       │       │          │              │              │
      ▼       ▼       ▼          ▼              ▼              ▼
   PAS-X   SAP    eQMS       Instrument CDS    EM Feed       Basel
                            (Empower, Chrom,    (Vaisala     federated
                             Qtegra)             viewLinc)   instance
```

## 3. System Description and Intended Use

LabWare LIMS 8 is the system of record for the QC sample lifecycle and contract-testing services. It receives sample creation requests from PAS-X (in-process and release), receives EM continuous data from Vaisala viewLinc, accepts manual sample login from goods-receiving, manages aliquot creation + storage location chain-of-custody, assigns analysts, tracks instrument runs, ingests results from CDS systems via versioned parsers, applies LIMS Basic-implemented calculations, gates results through reviewer / approver signatures, releases approved results to PAS-X / SAP, generates COAs, manages stability protocol schedules, qualifies suppliers + raw materials, federates master data between Cambridge and Basel sites, and creates eQMS deviations on OOS / OOT / OOE events per the FDA OOS (2022) workflow.

GAMP Cat 4: LabWare core platform supplied under LabWare's SDLC; site-authored LIMS Basic scripts treated as Cat 5 sub-components under separate change control with documented unit and integration tests. The LIMS is in scope of the site's ISO/IEC 17025:2017 accreditation for the contract-testing service line; clauses 7.5 (technical records), 7.7 (data control + ITC), and 8.4 (control of records) apply.

## 4. User Roles

| Role | Permissions |
|---|---|
| Sample Login Clerk | Create / receive samples; cannot edit results; manages chain-of-custody at receipt. |
| Aliquot / Storage Custodian | Generate aliquots; record storage location; chain-of-custody check-in / check-out. |
| Analyst | Run samples; enter manual data; submit results for review. |
| Senior Analyst / Reviewer | Review analyst-submitted results; cannot approve own work. |
| QC Manager (Approver) | Approve results; release to PAS-X / SAP; cannot review own. |
| Method / Spec Author | Author / edit specifications and methods under change control. |
| Method / Spec Approver (QA) | Approve specifications and methods to EFFECTIVE. |
| Parser Author | Author / version-control instrument-data parsers. |
| Parser Approver | Promote a parser version to PRODUCTION after qualification. |
| OOS Investigator | Conduct Phase I / II investigation per the FDA OOS (2022) workflow. |
| OOS Approver (QA) | Approve OOS disposition; cannot investigate own case. |
| Stability Coordinator | Maintain stability protocol schedules; trigger pull-points. |
| Supplier Qualification Officer | Manage supplier + raw-material qualification status. |
| Multi-Site Federation Steward | Authorise inter-site result transfer + master-data sync. |
| LIMS Administrator | LIMS configuration, AD groups, scripts deployment; cannot result-approve. |
| Auditor | Read-only across records and audit trails. |

Separation of duties: Analyst ≠ Reviewer ≠ Approver of the same result; Method Author ≠ Method Approver; Parser Author ≠ Parser Approver; OOS Investigator ≠ OOS Approver; Aliquot Custodian ≠ Analyst when chain-of-custody crosses shifts.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP 5 risk classification (`R1` direct GxP impact / `R2` indirect / `R3` none), and a verifiable `shall`-clause.

### 5.1 Platform / Hardware / Infrastructure

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | The system shall run an N+1 active App Server cluster with Data Guard physical-standby Oracle. |
| URS-PLAT-02 | H | R1 | The system shall maintain a DR site cold replica with RPO ≤ 15 min and RTO ≤ 4 hours during full-site failover. |
| URS-PLAT-03 | M | R2 | The system shall accept security patches within 30 days of vendor release per the site patch SLA. |
| URS-PLAT-04 | H | R1 | The system shall replicate transactions to a passive secondary site (Basel) with replication-lag monitoring and alerts. |
| URS-PLAT-05 | M | R2 | The system shall support rolling app-server restarts without dropping in-flight transactions. |

### 5.2 Sample Lifecycle — Receipt, Login, Aliquot, Storage, Chain-of-Custody

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SAMPLE-01 | H | R1 | Sample creation from PAS-X shall be atomic — full sample created or PAS-X order untouched with error reported. |
| URS-SAMPLE-02 | H | R1 | Each sample shall carry a unique LIMS sample ID, parent batch, sample type, sampling point, sampling user + timestamp, and the assigned test specification. |
| URS-SAMPLE-03 | H | R1 | Sample status shall follow a documented workflow: Logged → Received → In-Storage → Scheduled → In-Test → Results-Entered → Reviewed → Approved → Released; reverse transitions shall require a captured reason. |
| URS-SAMPLE-04 | H | R1 | Hold and quarantine actions shall require role-restricted signatures and a disposition reason. |
| URS-SAMPLE-05 | H | R1 | The system shall support aliquot generation: an aliquot inherits its parent sample's specification, batch, and chain-of-custody, and gets a unique aliquot ID. |
| URS-SAMPLE-06 | H | R1 | Storage location assignment shall be recorded with location ID, custodian, temperature class (e.g., 2-8 °C, -20 °C, -80 °C, ambient), and time of placement. |
| URS-SAMPLE-07 | H | R1 | Chain-of-custody check-out / check-in shall record custodian, time, and target location; broken chain-of-custody (e.g., missing check-in) shall raise an alert. |
| URS-SAMPLE-08 | M | R2 | Sample-receipt manual login shall support barcode + GS1 DataMatrix scanning. |
| URS-SAMPLE-09 | M | R2 | The system shall calculate sample-shelf-life from receipt date + storage class and surface expiration alerts at D-7 and D-0. |
| URS-SAMPLE-10 | M | R2 | The system shall support sub-sampling for stability pull-points with traceability back to the parent batch. |

### 5.3 Method Registry and Version Control

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-METH-01 | H | R1 | The Method Registry shall list every analytical method with its current version, lifecycle state, validation evidence reference, and applicable matrices. |
| URS-METH-02 | H | R1 | Methods shall follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE per ICH Q2(R2). |
| URS-METH-03 | H | R1 | Only EFFECTIVE method versions may be assigned to samples; superseded versions remain readable for archive only. |
| URS-METH-04 | H | R1 | Method transitions shall require role-restricted signatures with Method Author ≠ Method Approver SoD. |
| URS-METH-05 | H | R1 | EFFECTIVE methods shall be immutable; changes shall create new revisions via change control linked to MasterControl. |
| URS-METH-06 | M | R2 | The Method Registry shall surface method-version usage statistics per quarter (samples-per-method, revalidation-due flags). |
| URS-METH-07 | M | R2 | Methods shall declare their AIQ category (USP <1058> A / B / C) for instruments used. |

### 5.4 Specifications

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SPEC-01 | H | R1 | Specifications shall follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE. |
| URS-SPEC-02 | H | R1 | Only EFFECTIVE specifications may be assigned to samples. |
| URS-SPEC-03 | H | R1 | Specification transitions shall require role-restricted signatures with Spec Author ≠ Spec Approver SoD. |
| URS-SPEC-04 | H | R1 | EFFECTIVE specifications shall be immutable; changes shall create new revisions via change control. |
| URS-SPEC-05 | H | R1 | The system shall enforce attribute-level limit types (single-sided, two-sided, ranged, count-based, attribute, sensory) per ICH Q6A. |
| URS-SPEC-06 | M | R2 | The system shall surface specification effective-date conflicts (e.g., a sample whose receipt date precedes its assigned spec's EFFECTIVE date) and require dispositioning. |

### 5.5 Test Execution and Instrument-Data Acquisition

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RES-01 | H | R1 | Results shall be ingested from instrument CDS via documented adapters (Empower DB, Chromeleon DB, Qtegra LIMS Connector, file watchers); raw-result file pointers and SHA-256 hashes shall be preserved. |
| URS-RES-02 | H | R1 | LIMS Basic calculations shall be version-controlled; each calculation shall have documented unit / integration tests; deployments shall require approved change control. |
| URS-RES-03 | H | R1 | Results shall be compared against the assigned EFFECTIVE specification; OOS / OOT / OOE shall be flagged automatically and routed for investigation. |
| URS-RES-04 | H | R1 | OOS results shall require an immediate eQMS deviation (created via API) before approval is permitted. |
| URS-RES-05 | H | R1 | Manual data entry shall be allowed only where instrument integration is not feasible; manual entries shall require dual-keyboard verification by a second user. |
| URS-RES-06 | H | R1 | Result review and approval shall require role-restricted signatures with separation of duties. |
| URS-RES-07 | M | R2 | A Review-by-Exception view shall highlight deviations, manual entries, retests, and reprocessing. |
| URS-RES-08 | H | R1 | Each result shall record the executing instrument's qualification status at time-of-test; non-qualified instruments shall block result commit. |
| URS-RES-09 | M | R2 | The system shall record reagent / standard lot numbers consumed in the test execution. |
| URS-RES-10 | M | R2 | The system shall capture analyst-witness signature for critical-step in-process tests where the method requires it. |

### 5.6 Instrument Data Parser Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PARSE-01 | H | R1 | Each instrument-data parser shall be version-controlled with documented schema mappings, unit tests, and qualification evidence per USP <1058>. |
| URS-PARSE-02 | H | R1 | Parser deployment to PRODUCTION shall require Parser Author ≠ Parser Approver signatures and a passing regression suite against a golden-file corpus. |
| URS-PARSE-03 | H | R1 | The system shall preserve the raw instrument file alongside the parsed result; parser changes shall not retroactively alter prior parsed results. |
| URS-PARSE-04 | M | R2 | Parser schema changes that affect downstream calculations shall trigger an impact assessment and method-validation review. |
| URS-PARSE-05 | M | R2 | A parser's run-time errors (file unparseable, missing fields, hash mismatch) shall be queued for human triage; the source sample shall be paused. |

### 5.7 OOS / OOT / OOE Workflow per FDA OOS (2022)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-OOS-01 | H | R1 | OOS detection shall create a Phase-I investigation case in the eQMS within 1 hour of result commit. |
| URS-OOS-02 | H | R1 | Phase-I investigation shall capture: analyst, instrument, method, reagents, equipment status, and the laboratory checklist per FDA OOS (2022). |
| URS-OOS-03 | H | R1 | An OOS case shall not proceed to Phase-II (full investigation including root-cause) without QA sign-off on the Phase-I conclusion. |
| URS-OOS-04 | H | R1 | Retest authorisation shall require a documented justification, QA sign-off, and shall be recorded in the case file before the retest sample is logged. |
| URS-OOS-05 | H | R1 | Invalidating an original OOS result shall require a documented assignable cause; bare disagreement-with-result shall not justify invalidation. |
| URS-OOS-06 | H | R1 | The OOS workflow shall enforce SoD: OOS Investigator ≠ OOS Approver; analyst-of-record ≠ retest analyst when assignable-cause review is open. |
| URS-OOS-07 | M | R2 | OOT (Out-of-Trend) detections shall route to the stability or in-process trending sub-process per the configured rule set. |
| URS-OOS-08 | M | R2 | The system shall produce an annual OOS / OOT trend report by product and root-cause category for management review. |

### 5.8 Result Release and COA Generation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-COA-01 | H | R1 | The system shall generate a Certificate of Analysis (COA) per batch that lists every released test, the assigned spec limit, the reported result, the analyst, the approver, the test date, and the COA generation timestamp. |
| URS-COA-02 | H | R1 | The COA shall be PDF/A-3 compliant and shall include the LIMS document hash + signature page per § 11.50. |
| URS-COA-03 | H | R1 | COA generation shall be blocked until every released test of the batch holds Approved status and any related deviations are closed. |
| URS-COA-04 | M | R2 | The COA layout shall be configurable per product / customer; layout changes shall follow change control. |
| URS-COA-05 | M | R2 | Re-issuance of a COA (e.g., after a clerical correction) shall version the COA, supersede the prior version, and record the reason. |

### 5.9 Stability Integration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-STAB-01 | H | R1 | Stability protocols shall define pull-points (e.g., 0, 3, 6, 9, 12, 18, 24 months) per storage condition (e.g., 25 °C/60% RH, 40 °C/75% RH, 5 °C); pull-point arrivals shall auto-create sample-login tasks. |
| URS-STAB-02 | H | R1 | Missed pull-points beyond the configured grace window shall create eQMS deviations. |
| URS-STAB-03 | H | R1 | Stability results shall feed the stability trending engine; significant change per ICH Q1E shall trigger investigation. |
| URS-STAB-04 | M | R2 | The system shall export ICH-Q1E-compliant stability reports for regulatory submission. |
| URS-STAB-05 | M | R2 | Stability protocol amendments shall require change control linked to MasterControl. |

### 5.10 Supplier and Raw-Material Qualification

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SUPP-01 | H | R1 | The system shall maintain a Supplier Quality Register with qualification status (qualified / on-hold / disqualified), audit-cycle dates, and qualification certificates. |
| URS-SUPP-02 | H | R1 | Receipt of raw materials from non-qualified suppliers shall be blocked; emergency override shall require Head-of-QA signature and a deviation. |
| URS-SUPP-03 | H | R1 | Each incoming raw-material lot shall be linked to its supplier and shall receive its release test sequence per the assigned spec. |
| URS-SUPP-04 | M | R2 | The system shall surface supplier-trend metrics (acceptance rate, OOS rate, deliveries) per quarter. |
| URS-SUPP-05 | M | R2 | Supplier requalification due-dates shall be alerted at D-90 / D-30 / D-0. |

### 5.11 Environmental Monitoring Integration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-EM-01 | H | R1 | Continuous EM data (temperature, humidity, differential pressure, particle counts) from Vaisala viewLinc shall ingest into the LIMS with timestamp + sensor-id + location + qualified-instrument-status. |
| URS-EM-02 | H | R1 | EM excursions beyond Alert / Action limits shall create eQMS deviations and shall be linked to the affected batches in production at the time of the excursion. |
| URS-EM-03 | M | R2 | The system shall produce per-cleanroom trend reports for the Annual Product Quality Review (APQR). |

### 5.12 Multi-Site Federation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-FED-01 | H | R1 | Master data (methods, specifications, suppliers, role definitions) shall federate between Cambridge and Basel with documented authoritative-site rules per entity. |
| URS-FED-02 | H | R1 | Inter-site result transfer shall require a documented federation steward sign-off and shall preserve the source-site audit trail. |
| URS-FED-03 | M | R2 | Federation lag (Cambridge → Basel) shall be monitored; lag > 10 minutes shall raise an alert. |
| URS-FED-04 | M | R2 | A site shall be able to operate read-only against federated master data during federation outages without compromising local sample login. |

### 5.13 Audit Trail and Annex 11 § 9 Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | A time-stamped, secure audit trail per § 11.10(e) shall cover sample, specification, method, parser, result, calculation deployment, signature, and configuration events. |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only; no application-level update / delete shall be possible. |
| URS-AUD-03 | H | R1 | Audit-trail review per Annex 11 § 9 shall be performed by Reviewer per batch and by QA Compliance quarterly, with documented evidence. |
| URS-AUD-04 | H | R1 | Audit-trail retention shall be ≥ 25 years from product expiry per Part 211.180. |
| URS-AUD-05 | M | R2 | The system shall provide a focused-audit-trail-review tool that filters to material events (signatures, OOS, configuration, manual-data overrides) per shift / per batch. |
| URS-AUD-06 | M | R2 | Audit-trail review evidence shall be exportable for inspection with chain-of-custody preservation. |

### 5.14 21 CFR Part 11 / Annex 11

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a), the system shall implement procedural controls protecting electronic-record validity (validated SDLC, role definitions, change control). |
| URS-PART11-02 | H | R1 | Per § 11.10(b), the system shall produce accurate and complete copies suitable for inspection (PDF/A-3 + CSV exports). |
| URS-PART11-03 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via AD with MFA. |
| URS-PART11-04 | H | R1 | Per § 11.50, electronic signatures shall include the signer's printed name, date and time, and the meaning of the signature. |
| URS-PART11-05 | H | R1 | Per § 11.70, signatures shall be cryptographically linked to the signed record; tampering shall invalidate the signature. |
| URS-PART11-06 | H | R1 | Per § 11.100, signatures shall be unique to a single individual; no reuse or reassignment. |
| URS-PART11-07 | H | R1 | Per § 11.200, re-authentication shall be required at the moment of signing (no cached-credential signing). |
| URS-PART11-08 | H | R1 | Per § 11.300, password / credential controls per site InfoSec policy shall be enforced. |
| URS-ANX11-01 | H | R1 | Per Annex 11 § 4, validation evidence (IQ/OQ/PQ + SDLC) shall be maintained current. |
| URS-ANX11-02 | H | R1 | Per Annex 11 § 6, accuracy checks shall be implemented at data-entry boundaries (range, format, plausibility). |

### 5.15 ISO/IEC 17025 Alignment (Contract-Testing Service Line)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ISO-01 | H | R1 | Per ISO/IEC 17025:2017 § 7.5, technical records shall be sufficient to permit identification of factors affecting measurement uncertainty + repeatability. |
| URS-ISO-02 | H | R1 | Per ISO/IEC 17025:2017 § 7.7, results shall include the laboratory's name, customer / specimen identification, test method, measured value + uncertainty, and date of issue. |
| URS-ISO-03 | M | R2 | Per ISO/IEC 17025:2017 § 8.4, records shall be retained for a minimum of the accreditation cycle plus the regulatory retention (25 y). |
| URS-ISO-04 | M | R2 | The system shall surface ISO-17025-flagged samples separately for accreditation surveillance. |

### 5.16 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-PASX-01 | H | R1 | Sample creation from PAS-X shall use REST with an idempotency key; failures shall be retried with a logged correlation ID. |
| URS-INT-PASX-02 | H | R1 | Approved release results shall return to PAS-X within 5 minutes (P95). |
| URS-INT-SAP-01 | M | R2 | Approved release results shall push to SAP for batch genealogy. |
| URS-INT-EQMS-01 | H | R1 | OOS / OOT shall auto-create deviations in MasterControl via REST with idempotency. |
| URS-INT-CDS-01 | H | R1 | Result ingest from CDS shall preserve the raw-data file pointer + hash; manipulation of source data shall be prohibited. |
| URS-INT-CDS-02 | H | R1 | The system shall support documented adapters for Empower, Chromeleon, and Qtegra; adapter versions shall be tracked in CI. |
| URS-INT-AD-01 | H | R1 | Authentication shall use AD via Keycloak federation; service accounts shall use the credential vault. |
| URS-INT-EM-01 | H | R1 | EM data feed shall connect to Vaisala viewLinc via the documented API with a heartbeat and lag monitor. |
| URS-INT-STAB-01 | M | R2 | The stability scheduler shall create pull-point sample tasks via the documented LIMS API. |

### 5.17 Custom-Script (Cat 5 sub-component) SDLC

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEV-01 | H | R1 | LIMS Basic scripts shall be maintained in version control with signed commits; merges to `main` shall require peer review and passing CI. |
| URS-DEV-02 | H | R1 | Each script shall have documented intended use, GAMP-Cat-5 risk assessment, FS, and OQ test cases. |
| URS-DEV-03 | H | R1 | Deployment to production shall require an approved change request and a passing regression suite. |
| URS-DEV-04 | M | R2 | Static analysis on scripts shall run on every CI build; vulnerabilities shall be triaged within 30 days. |
| URS-DEV-05 | M | R2 | Script releases shall produce a signed manifest including SHA-256 of every deployed unit. |

### 5.18 Performance / Availability / Backup

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | H | R1 | Sample-page navigation latency shall be ≤ 2 seconds at the 95th percentile under nominal load (300 concurrent users). |
| URS-PERF-02 | M | R2 | Bulk result import (≥ 10,000 result records) shall complete within 10 minutes. |
| URS-AV-01 | H | R1 | System availability shall be ≥ 99.5% during business hours. |
| URS-BAK-01 | H | R1 | The database shall be backed up nightly with PITR; retention shall be ≥ 25 years. |
| URS-BAK-02 | H | R1 | A quarterly restore test shall be witnessed and recorded. |

### 5.19 Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | All authentication shall use AD with MFA; no local accounts shall exist other than break-glass. |
| URS-SEC-02 | H | R1 | TLS 1.2 or higher shall be enforced for all client-server traffic. |
| URS-SEC-03 | M | R2 | Vulnerability scans shall run weekly; critical findings shall be remediated within 30 days. |
| URS-SEC-04 | M | R2 | Penetration testing shall be performed annually; high / critical findings shall be remediated under change control. |
| URS-SEC-05 | H | R1 | Service-account credentials shall live in HashiCorp Vault; static credentials shall be rotated every 90 days. |

### 5.20 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Production access shall require recorded role-specific training in the LMS. |
| URS-TRN-02 | M | R2 | An annual refresher shall be completed for all reviewer / approver roles. |
| URS-TRN-03 | M | R2 | Parser Authors + OOS Investigators shall complete an advanced-data-integrity training module. |
| URS-PR-01 | H | R1 | An annual periodic review per Annex 11 § 11 shall cover configuration, scripts inventory, parser inventory, audit-trail review evidence, deviation summary, integration health, training, and federation-replication health; the review shall be signed by the QC Informatics Lead and the Head of QA. |

### 5.21 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem for the thick client and SAML 2.0 via Entra ID for the LabWare web client; conditional-access policy `Lab-App Conditional Access (MFA + device-compliance)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with Oracle RMAN for the LabWare Oracle backend; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 25 y (release-record-linked sample data) per the consuming-record schedule. |

### 5.22 Cross-System Integration — Helios audit-trail handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HEL-01 | H | R1 | LabWare LIMS shall publish audit-trail events (Sample lifecycle, result entry, review, approval, and OOS investigation events) to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract (JSON Lines, schema-registry pinned, Kafka topic `helios.ingest.caelum.labware.v1`) within 5 minutes of event capture; 21 CFR § 11.10(e) audit-trail completeness shall be preserved end-to-end so that no event class is lost at the boundary. |
| URS-XINT-HEL-02 | H | R1 | Pre-handover audit-trail retention on the LabWare LIMS side shall be ≥ 15 y regardless of Helios availability; once Helios acknowledges ingest (per-message ack with idempotency key), Helios is the system-of-record for review and the LabWare LIMS local copy serves as the durability backstop until the local retention floor expires. |

## 6. Acceptance Criteria

The system shall enter validated GMP use when FS / DS / CS / RA / IQ / OQ / PQ are approved and executed; PQ shall include a representative end-to-end sample (PAS-X → LIMS receipt → aliquot → storage → instrument run → CDS ingest → review → approve → COA → PAS-X / SAP), a representative OOS workflow per FDA OOS (2022), and a representative stability pull-point cycle; DR failover shall be tested; VSR shall be approved by QC Informatics Lead and Head of QA; the RTM shall map every URS to ≥ 1 approved test case.

## 7. Constraints

- LIMS Basic scripts run under a separate Cat-5 lifecycle.
- Vendor patches are accepted under change control.
- Vaisala viewLinc validation is governed by its own URS.

## 8. Assumptions

- PAS-X, SAP, eQMS, AD, CDS systems, viewLinc, and the stability scheduler are independently validated.
- The Basel federation site uses the same LabWare 8 baseline configuration.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300 — Electronic Records; Electronic Signatures
- 21 CFR Part 211 §§ .22, .68, .180, .192 — CGMP for Finished Pharmaceuticals
- FDA *Guidance for Industry: Investigating Out-of-Specification (OOS) Test Results for Pharmaceutical Production* (2022)
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance)

### EU
- EU GMP Annex 11 — Computerised Systems (§§ 4, 6, 9, 11)
- EU GMP Chapter 4 — Documentation

### International — ICH / USP
- ICH Q2(R2) — Validation of Analytical Procedures
- ICH Q9(R1) — Quality Risk Management
- ICH Q10 — Pharmaceutical Quality System
- ICH Q1A(R2) / Q1E — Stability Testing of New Drug Substances and Products
- USP <1058> — Analytical Instrument Qualification

### Industry / Quality
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE GAMP Good Practice Guide: *Validation of Laboratory Computerized Systems*
- ISPE GAMP Good Practice Guide: *Records and Data Integrity*
- PIC/S PI 041 — Good Practices for Data Management and Integrity
- ISO/IEC 17025:2017 — General Requirements for the Competence of Testing and Calibration Laboratories
- ISO/IEC 27001:2022 — Information Security Management Systems

### Vendor
- LabWare — *LIMS 8 Installation, Configuration, and Administration Reference* (8.0 release notes)

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

