---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "GAMP 5 (2nd Ed., 2022) Cat 4 conventions"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200"
  - "EU GMP Annex 11 §§ 4, 6, 9; EU GMP Annex 15 (Qualification & Validation)"
  - "ICH Q9(R1)"
  - "FDA Guide to Inspections — Validation of Cleaning Processes (1993)"
  - "EMA Guideline on Setting Health Based Exposure Limits (EMA/CHMP/CVMP/SWP/169430/2012)"
  - "PIC/S PI 006-3; APIC Cleaning Validation Guideline"
  - "USP <1072>, <1078>; PIC/S PI 041"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Cleaning Validation System — ValGenesis CV 5.0

**Document Number:** VSP-URS-CLNV-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Vesper BioMed Oy, Cleaning Validation Operations, Helsinki, Finland *(fictional)*
**System Owner:** Cleaning Validation Lead | **Process Owner:** Head of Manufacturing Sciences
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **ValGenesis CV 5.0** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; EU GMP Annex 15; ICH Q9(R1); FDA *Guide to Inspections — Validation of Cleaning Processes* (1993); EMA *Guideline on Setting Health Based Exposure Limits* (EMA/CHMP/CVMP/SWP/169430/2012); APIC Cleaning Validation Guideline; PIC/S PI 006-3; USP <1072>, <1078>; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Cleaning Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Process Engineer) | _____________ | _____________ | _____ |
| Reviewer (Toxicologist — PDE/HBEL) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Approver (Head of Manufacturing Sciences) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | v1.2 enrichment: tiered to T2 (50-80 reqs; this URS lands at 56 reqs); explicit § 5 modules for MAC calculation engine (10ppm / 1/1000 TDD / PDE / HBEL), equipment grouping + worst-case, sample plan (swab + rinse + visual), recovery study lifecycle, hold-time study, cleaning agent qualification, product changeover matrix, inspection-readiness dashboard. References modernised per METHODOLOGY § 2A.1; risks expanded to 8 items. |

## Definitions

| Term | Definition |
|---|---|
| CV | Cleaning Validation |
| MAC / MACO | Maximum Allowable Carryover |
| HBEL | Health-Based Exposure Limit (per EMA guideline 2014) |
| ADE / PDE | Acceptable Daily Exposure / Permitted Daily Exposure |
| TDD | Therapeutic Daily Dose |
| Worst case | Most challenging combination of product, equipment, residue for grouping / bracketing |
| Swab / Rinse / Visual | Sampling methods per FDA Cleaning Validation Guide |
| Recovery Factor | Method-validated proportion recovered from a surface (e.g., 0.65) |
| Hold Time — Dirty | Time between end of production and start of cleaning |
| Hold Time — Clean | Time between end of cleaning and next use |
| LIMS | LabWare LIMS 8 |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the cleaning-validation management system used to plan, execute, and trend cleaning-validation studies and ongoing cleaning verification across multi-product facilities at Vesper BioMed. The system is the system of record for MAC calculations, equipment grouping + worst-case selection, sampling plans, recovery factors, hold-time studies, cleaning agent qualification, product changeover matrices, and cleaning-validation summary reports.

## 2. Scope

**In:** ValGenesis CV 5.0 server (Linux + PostgreSQL); worst-case product / equipment / residue matrices; HBEL / ADE / PDE / TDD-based MAC calculations; sampling plans (swab / rinse / visual / TOC); recovery study management; hold-time study management; cleaning-agent qualification; product-changeover risk matrix; inspection-readiness dashboard; integration with LIMS for analytical results, eQMS for OOS-driven deviations, Veeva Vault for protocol / report references, and PAS-X MES for production-schedule + changeover linkage; AD authentication.

**Out:** physical cleaning equipment / CIP / SIP skids (separate URS); analytical laboratories' instrument validation (separate URSs); HBEL toxicology source data authorship (managed by toxicology / regulatory).

## 3. System Description

ValGenesis CV is the system of record for cleaning-validation strategy, MAC calculations, sampling plans, and cleaning-verification records. For each equipment train it computes MAC based on product matrices and HBEL inputs (per the four canonical methods — 10 ppm, 1/1000 TDD, ADE/PDE, visually clean), manages sampling per CV protocol, captures recovery factors from validated recovery studies, evaluates hold-time data, qualifies cleaning agents and qualifies their detection methods, manages the product-changeover risk matrix, ingests analytical results from LIMS, evaluates pass / fail per the calculated limits, and produces validation summary reports.

GAMP Cat 4: ValGenesis maintains the platform; site validation focuses on configuration of HBEL inputs, MAC formulas, sampling plans, recovery-study workflows, hold-time-study workflows, cleaning-agent qualification, and integrations.

## 4. User Roles

| Role | Permissions |
|---|---|
| CV Engineer | Author / edit CV protocols, MAC inputs, recovery-study + hold-time protocols under change control. |
| CV Lead | Approve protocols and MAC calculations. |
| Toxicologist | Maintain HBEL / ADE / PDE library; approve HBEL inputs. |
| Sampling Operator | Execute sampling per protocol; record chain-of-custody. |
| Analyst | Process samples in LIMS (separate system); cannot edit MAC. |
| Cleaning-Agent SME | Author cleaning-agent qualification records. |
| QA Approver | Approve CV reports for release decisions. |
| System Administrator | OS / patch / AD; cannot approve. |
| Auditor | Read-only. |

Separation of duties: CV Engineer ≠ CV Lead approving same protocol; Sampling Operator ≠ Analyst; Cleaning-Agent SME ≠ QA Approver.

## 5. User Requirements

### 5.1 Worst-Case Matrix and Equipment Grouping

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MX-01 | H | R1 | Equipment-train master data shall capture surface area, materials of construction, complexity, shared / dedicated status, CIP / SIP status. |
| URS-MX-02 | H | R1 | Product master data shall capture HBEL / ADE / PDE values referenced from a controlled toxicology source. |
| URS-MX-03 | H | R1 | The worst-case selection shall be deterministic and re-computable from the master data; bracketing shall be documented. |
| URS-MX-04 | H | R1 | Equipment grouping (family / train) shall be supported with documented justification (similar geometry, contact materials, cleaning method); group-level worst-case shall represent the family. |
| URS-MX-05 | H | R1 | Re-evaluation of grouping shall be triggered automatically upon equipment modification or new-product introduction. |

### 5.2 MAC Calculation Engine

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MACO-01 | H | R1 | MAC calculations shall implement HBEL-based limits per EMA *Guideline on Setting Health Based Exposure Limits* (2014) as the primary criterion. |
| URS-MACO-02 | H | R1 | MAC calculations shall additionally support the 10 ppm criterion and the 1/1000 of minimum therapeutic daily dose (TDD) criterion as comparators per APIC; the system shall select the most stringent acceptance value across all three criteria per residue / next-product pair. |
| URS-MACO-03 | H | R1 | MAC inputs (HBEL, batch size, surface area, recovery factor, smallest dose, TDD, safety factor) shall be version-controlled; a change to any input shall create a new MAC version. |
| URS-MACO-04 | H | R1 | Calculations shall be Accurate per OQ across edge cases (smallest-dose product, largest equipment surface area, highly potent compound with HBEL < 10 µg / day). |
| URS-MACO-05 | H | R1 | For highly hazardous compounds (HPAPI, cytotoxic, sensitizer, hormone, β-lactam), the system shall force HBEL-driven MAC and shall flag if 10 ppm or 1/1000 TDD would yield a less stringent acceptance. |

### 5.3 Sample Plan (Swab / Rinse / Visual)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SMP-01 | H | R1 | Sampling plans (swab locations, rinse, visual inspection) per equipment train shall be specified per CV protocol; chain-of-custody shall be captured electronically with sampler ID, timestamp, sample-location ID. |
| URS-SMP-02 | H | R1 | Swab-sampling locations shall be defined per worst-case-location identification (hardest-to-clean, residue-accumulation points); per-location surface area shall be recorded. |
| URS-SMP-03 | H | R1 | Rinse sampling shall capture rinse volume + rinse-acceptance limit (computed from MAC + rinse volume + surface area). |
| URS-SMP-04 | H | R1 | Visual inspection per FDA Cleaning Validation Guide 1993 shall be supported as a baseline acceptance (visually clean precedes quantitative limits). |

### 5.4 Recovery Study Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REC-01 | H | R1 | Recovery studies shall capture: surface material, spike level, recovery method (swab / rinse), analytical method, replicate count (≥ 3), recovery factor, %RSD acceptance (≤ 20 % per FDA). |
| URS-REC-02 | H | R1 | Recovery factors below 50 % shall flag a study for revision (analytical method or sampling technique issue) and shall block use until revised + re-approved. |
| URS-REC-03 | H | R1 | Recovery studies shall require periodic re-verification (default 3 years) tracked by the system. |
| URS-REC-04 | H | R1 | The MAC calculation engine shall apply the validated recovery factor per residue / surface; mis-application (e.g., applying SS-316 recovery to glass surface) shall be impossible by configuration. |

### 5.5 Hold-Time Studies

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HT-01 | H | R1 | Dirty hold-time studies shall capture: equipment, last-product, hold duration (hours), microbial + chemical residue endpoint, acceptance criteria; dirty hold-time limit shall be derived from worst-case soiling study. |
| URS-HT-02 | H | R1 | Clean hold-time studies shall capture: equipment, post-cleaning duration, microbial + endotoxin (where applicable) endpoint, acceptance criteria. |
| URS-HT-03 | H | R1 | Hold-time limits shall be embedded into production scheduling; exceeded hold time shall trigger eQMS deviation. |
| URS-HT-04 | M | R2 | Periodic re-verification of hold-time limits shall be tracked (default 5 years). |

### 5.6 Cleaning Agent Qualification

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AGT-01 | H | R1 | Each cleaning agent (alkaline, acidic, neutral, oxidizer, surfactant) shall be qualified with: composition, supplier CoA, removability study, residue-detection method, acceptance criteria for cleaning-agent residue. |
| URS-AGT-02 | H | R1 | Cleaning-agent residue MAC shall be computed using the agent's HBEL (or default 10 ppm / 1/1000 TDD fallback) per the same logic as URS-MACO-01..02. |
| URS-AGT-03 | M | R2 | Cleaning-agent lots shall be tracked; CoA discrepancies shall raise a deviation. |

### 5.7 Product Changeover Matrix

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CHG-01 | H | R1 | The product-changeover matrix shall enumerate every product-pair (previous-product → next-product) with: applicable MAC, cleaning procedure ID, cleaning-agent qualification status, sampling plan, last verification date. |
| URS-CHG-02 | H | R1 | Production scheduling (PAS-X MES) shall query the changeover matrix; an unsupported pair (no validated cleaning, expired verification, missing recovery factor) shall block scheduling. |
| URS-CHG-03 | H | R1 | Introduction of a new product shall trigger a changeover-matrix expansion workflow with CV Engineer authoring + CV Lead approval before the product can be scheduled. |
| URS-CHG-04 | M | R2 | The changeover matrix shall be exportable as the inspection-readiness artefact per FDA / EMA cleaning-validation expectation. |

### 5.8 Sampling, Verification, Reporting

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VER-01 | H | R1 | Analytical results from LIMS shall be evaluated against MAC per sample; pass / fail shall be recorded. |
| URS-VER-02 | H | R1 | OOS shall trigger eQMS deviation and shall block CV report progression until investigation closes. |
| URS-VER-03 | H | R1 | Trending of cleaning-verification results shall be available per equipment / product-pair / agent; OOT detection shall trigger investigation per protocol-defined rules. |
| URS-RPT-01 | H | R1 | CV report shall include: study scope, equipment trains, MAC calculations, recovery factors applied, hold-time data, cleaning-agent qualification status, sampling plan, results, deviations, conclusion; signed by CV Lead and QA Approver. |

### 5.9 Inspection-Readiness Dashboard

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DASH-01 | H | R1 | The system shall provide an inspection-readiness dashboard summarising: CV protocol status per product family, MAC currency, recovery-study currency, hold-time currency, cleaning-agent qualification currency, changeover-matrix currency, recent OOS / OOT count, periodic-review status. |
| URS-DASH-02 | H | R1 | The dashboard shall be exportable as a PDF inspection-readiness binder per equipment / product. |
| URS-DASH-03 | M | R2 | The dashboard shall surface ageing alerts (e.g., MAC > 3 y old; recovery study > 3 y; hold-time > 5 y). |

### 5.10 Audit Trail / 21 CFR Part 11 / DI

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Time-stamped, secure audit trail covering MAC inputs, recovery studies, hold-time studies, cleaning-agent qualification, changeover matrix, sampling, verification, signatures per EU GMP Annex 11 § 9. |
| URS-AUD-02 | H | R1 | Audit trail append-only. |
| URS-AUD-03 | H | R1 | Audit-trail review by CV Lead monthly. |
| URS-AUD-04 | H | R1 | Retention ≥ 25 years from product expiry. |
| URS-PART11-10 | H | R1 | Procedures and controls per 21 CFR § 11.10(a)–(e). |
| URS-PART11-50 | H | R1 | E-signature manifestation per 21 CFR § 11.50. |
| URS-PART11-70 | H | R1 | Signature binding per 21 CFR § 11.70. |
| URS-PART11-100 | H | R1 | Unique signatures per 21 CFR § 11.100. |
| URS-PART11-200 | H | R1 | Re-authentication at signing per 21 CFR § 11.200. |
| URS-DI-01 | H | R1 | Records Attributable. |
| URS-DI-04 | H | R1 | Originals preserved. |
| URS-DI-05 | H | R1 | MAC / verification calculations Accurate per OQ. |

### 5.11 Integrations / Performance / Backup / Security / Training / PR

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-LIMS-01 | H | R1 | Sample requests pushed to LIMS; results pulled with idempotency. |
| URS-INT-EQMS-01 | H | R1 | OOS / hold-time exceedance auto-creates eQMS deviation. |
| URS-INT-VAULT-01 | M | R2 | Protocol / report references resolve to Vault QualityDocs URNs. |
| URS-INT-MES-01 | H | R1 | PAS-X MES queries changeover matrix on schedule-creation; unsupported pair blocks schedule. |
| URS-INT-AD-01 | H | R1 | AD authentication. |
| URS-INT-APR-01 | M | R2 | Read-only summary endpoint consumed by APR / PQR tool (MIR-URS-APR-001). |
| URS-PERF-01 | M | R2 | MAC recompute on master-data change ≤ 30 seconds. |
| URS-BAK-01 | H | R1 | Database backed up nightly with PITR; retention ≥ 25 years. |
| URS-BAK-02 | H | R1 | Quarterly restore test, witnessed. |
| URS-SEC-01 | H | R1 | Domain accounts only. |
| URS-TRN-01 | H | R1 | LMS-recorded training. |
| URS-PR-01 | H | R1 | Annual periodic review covering matrix updates, MAC changes, recovery / hold-time currency, OOS trends, audit-trail review evidence; signed by CV Lead + Head of Manufacturing Sciences + Head of QA. |

### 5.12 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem; conditional-access policy `Quality-App Conditional Access (MFA on first logon per session)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 15 y (cleaning-validation record) per the consuming-record schedule. |

### 5.13 Cross-System Integration — eQMS CAPA handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-EQMS-01 | H | R1 | On detection of Cleaning-validation failure (trigger: swab or rinse result above MACO, recovery-study failure, train-validation failure), the system shall push a CAPA-ticket creation event to the Talos MasterControl eQMS (`TLB-URS-EQMS-001`) via the eQMS event-push channel with required metadata {originating_system, originating_record_id, finding_class, severity, evidence_package_uri, detection_ts_utc, detection_user, regulatory_basis}; severity per site cleaning-validation procedure; MACO exceedance → critical. |
| URS-XINT-EQMS-02 | H | R1 | The eQMS ticket-creation call shall be idempotent on `{originating_system, originating_record_id, finding_class}`; the eQMS status-callback shall be ingested and reflected on the originating record with a hyperlink to the eQMS ticket; closed-loop verification per ICH Q9(R1) + ICH Q10 shall be evidenced before the originating record is dispositioned. |

## 6. Acceptance Criteria

CS, RA, IQ, OQ, PQ approved and executed; PQ includes a representative CV study end-to-end (worst-case selection → MAC computation → sample plan → recovery factor → sampling → LIMS results → pass/fail → report) plus OOS scenario, hold-time scenario, cleaning-agent qualification scenario, and changeover-matrix block-on-unsupported-pair scenario; VSR approved; RTM maps every URS-ID to ≥ 1 approved test case.

## 7. Constraints

- Vendor patches under change control.
- HBEL inputs sourced only from a toxicology-approved register; no direct editing of HBEL values inside CV.
- Recovery factor below 50 % blocks use until revision.

## 8. Assumptions

- LIMS, eQMS, Vault, AD, PAS-X MES, toxicology source are validated / maintained.
- Cleaning SOPs (per-train) are governed under change control.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200
- 21 CFR Part 211 §§ .67, .113 (cleaning + cross-contamination)
- FDA *Guide to Inspections — Validation of Cleaning Processes* (1993) — still current
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026)

### EU
- EU GMP Annex 11 §§ 4, 6, 9 — Computerised Systems
- EU GMP Annex 15 — Qualification and Validation
- EU GMP Chapter 3 — Premises and Equipment (cross-contamination)
- EU GMP Chapter 5 — Production (dedicated facilities, HBEL)
- EMA *Guideline on Setting Health Based Exposure Limits* (EMA/CHMP/CVMP/SWP/169430/2012, Nov 2014)
- EMA Q&A on Health-Based Exposure Limits (2018, 2020 updates)

### International — ICH
- ICH Q9(R1) — Quality Risk Management

### Industry guidance — ISPE / PIC/S / APIC / USP
- ISPE GAMP 5 (2nd Edition, 2022) — Cat 4 conventions
- ISPE Baseline Guide *Risk-Based Manufacture of Pharmaceutical Products* (RiskMaPP)
- PIC/S PI 006-3 — Recommendations on Validation Master Plan / IQ-OQ-PQ / Cleaning Validation
- APIC *Cleaning Validation Guideline* (latest rev.)
- USP <1072> Disinfectants and Antiseptics
- USP <1078> Good Manufacturing Practices for Bulk Pharmaceutical Excipients
- PIC/S PI 041 — Good Practices for Data Management and Integrity

### Vendor / internal
- ValGenesis — *CV 5.0 Reference*
- Internal: `VSP-SOP-CV-001` Cleaning Validation procedure

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

