---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "ICH Q1A(R2); ICH Q1B; ICH Q1C; ICH Q1D; ICH Q1E; ICH Q5C"
  - "USP <659> Packaging and Storage Requirements"
  - "WHO TRS 953 Annex 2; WHO TRS 1010 Annex 10"
  - "PIC/S PI 041"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Stability Management System — SLIMS / Genohm Stability Module 6.7

**Document Number:** HCT-URS-STAB-001
**Version:** 1.2
**Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Halcyon Therapeutics Inc., Stability Operations, Research Triangle Park, North Carolina, USA *(fictional)*
**System Owner:** Stability Operations Manager
**Process Owner:** Head of Quality Control
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **SLIMS / Genohm Stability Module 6.7** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 211 § 211.166 (Stability Testing); EU GMP Annex 11; ICH Q1A(R2) Stability Testing; ICH Q1B Photostability; ICH Q1C; ICH Q1D Bracketing/Matrixing; ICH Q1E Evaluation; ICH Q5C Stability of Biotech Products; USP <659>; WHO TRS 953 Annex 2; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Stability Operations Manager) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Statistician — Q1E) | _____________ | _____________ | _____ |
| Approver (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | v1.2 enrichment: tiered to T2 (50-80 reqs; this URS lands at 60 reqs). Added explicit § 5 modules: ICH zone configuration (I/II/III/IVa/IVb), photostability ICH Q1B, bracketing/matrixing ICH Q1D, shelf-life extension justification, reference + comparator standard management, biotech Q5C stability handling, chamber + time-point assignment, statistical model selection (Q1E poolability tests). References modernised per METHODOLOGY § 2A.1; § 9 risks expanded. |

## Definitions

| Term | Definition |
|---|---|
| SLIMS | SLIMS (Genohm) — laboratory data and stability platform |
| Stability Module | SLIMS Stability Module v6.7 |
| Pull (Time-point) | A scheduled withdrawal of stability samples for testing at a specified time-point |
| Condition | ICH stability-storage condition (e.g., 25 °C / 60 % RH; 40 °C / 75 % RH; 30 °C / 65 % RH) |
| ICH Zone | Climatic zone per ICH Q1A(R2) Table 1 (Zone I temperate, II subtropical, III hot dry, IVa hot humid, IVb hot very humid) |
| MKT | Mean Kinetic Temperature (USP <1150> / ICH Q1A(R2) § 2.1.7.2) |
| Bracketing / Matrixing | Reduced design per ICH Q1D |
| LIMS | LabWare LIMS 8 (separate URS) |
| EMS | Environmental Monitoring System (Vaisala viewLinc 5.2) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the stability-management system used to author stability protocols, schedule pulls per ICH Q1A(R2) time-point design, generate sample requests, retrieve and trend results, perform ICH Q1E statistical analysis (regression with poolability), justify shelf-life and shelf-life extensions, manage photostability per ICH Q1B, manage bracketing / matrixing per ICH Q1D, and produce stability summary reports for product registration and ongoing commitment studies at Halcyon Therapeutics.

## 2. Scope

**In scope:** SLIMS Stability Module v6.7 server (Linux, PostgreSQL 16) hosted on the site OpenShift cluster; web client; AD authentication on `halcyon.local`; integrations with LabWare LIMS 8 (sample creation / results retrieval), Vaisala viewLinc 5.2 (chamber-condition data feed for OOT investigations + MKT calc), and Veeva Vault QualityDocs (controlled-document references for stability protocols); the photostability sub-module (ICH Q1B Option 1 / Option 2 lamp-exposure tracking); the bracketing / matrixing design module (ICH Q1D); and the reference / comparator standard management module.

**Out of scope:** stability chambers themselves (separate equipment qualification); chamber EMS (separate URS — Vaisala viewLinc 5.2); LIMS sample lifecycle; product registration packages; in-use stability per ICH Q1C (handled in a separate workstream).

## 3. System Description and Intended Use

The system is the system of record for stability protocols and the schedule of pulls. For each protocol it generates the schedule of pulls per ICH Q1A condition + time-point design, dispatches sample-creation requests to LIMS at each pull, retrieves results from LIMS, applies stability data analysis per ICH Q1E (regression with covariate-pooling test, AIC-driven model selection, confidence intervals), produces stability summary reports, manages photostability per ICH Q1B (Option 1: cool white fluorescent + UV; Option 2: Xe-arc lamp), supports bracketing / matrixing study designs per ICH Q1D, and gates protocol amendments through change control.

For biotech products (proteins, peptides, ATMPs), the system supports ICH Q5C requirements: orthogonal stability-indicating methods, reference-standard comparison, and shorter-than-Q1A intermediate-condition cadences.

GAMP Cat 4: Genohm maintains the SLIMS SDLC; site validation focuses on installation, configuration of stability protocols / conditions / zones / time-points / matrixing designs, intended-use functionality, Part 11 controls, and the LIMS / Vault / EMS interfaces.

## 4. User Roles

| Role | Permissions |
|---|---|
| Stability Coordinator | Schedule pulls; create / dispatch sample requests; manage chain-of-custody. |
| Stability Analyst | Review per-pull results and trends; raise OOT / OOS investigations. |
| Protocol Author | Author stability protocols in DRAFT under change control. |
| Protocol Approver (QA) | Approve protocols to EFFECTIVE; cannot author. |
| Statistician | Approve ICH Q1E model selection and shelf-life calculations. |
| Report Approver (Head of QC + Head of QA) | Co-approve stability summary reports. |
| Reference Standard Custodian | Manage reference + comparator standards inventory + expiry. |
| System Administrator | OS / patching / AD groups; cannot approve. |
| Auditor | Read-only across data and audit trails. |

Separation of duties: Protocol Author ≠ Approver; Report Author ≠ Approvers; Stability Coordinator ≠ Statistician approving Q1E.

## 5. User Requirements

### 5.1 Platform / Hardware

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | The application shall be hosted on the site OpenShift cluster with three replicas; PostgreSQL 16 with PITR shall back the data layer. |
| URS-PLAT-02 | H | R1 | The system shall provide a DR site cold replica; RPO ≤ 15 min; RTO ≤ 4 h during full-site failover. |
| URS-PLAT-03 | H | R1 | All servers shall reside on the GMP-laboratory VLAN; office-network direct access shall be prohibited. |

### 5.2 Stability Protocol Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PROT-01 | H | R1 | Protocols shall follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED. |
| URS-PROT-02 | H | R1 | Each protocol shall reference: product, container-closure, ICH conditions in scope, ICH zone, time-points, attributes, specifications, sampling plan, statistical-analysis plan. |
| URS-PROT-03 | H | R1 | Protocol amendments shall follow controlled change with impact assessment and re-approval. |
| URS-PROT-04 | H | R1 | EFFECTIVE protocols shall be immutable; changes shall create new revisions. |
| URS-PROT-05 | H | R1 | Protocols shall declare bracketing / matrixing design (full / reduced per ICH Q1D) with explicit justification table. |

### 5.3 ICH Zone Configuration (Q1A(R2))

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ZONE-01 | H | R1 | The system shall support ICH Q1A(R2) climatic zones: Zone I (21 °C / 45 % RH), Zone II (25 °C / 60 % RH), Zone III (30 °C / 35 % RH), Zone IVa (30 °C / 65 % RH), Zone IVb (30 °C / 75 % RH); per-zone long-term + accelerated + intermediate conditions shall be configurable. |
| URS-ZONE-02 | H | R1 | Per market, the system shall route registration-stability protocols to the correct zone (e.g., EU = Zone II; Brazil = IVa; India = IVb; ASEAN per WHO TRS 953 Annex 2). |
| URS-ZONE-03 | H | R1 | Zone changes mid-study shall be impossible without protocol amendment (URS-PROT-03). |

### 5.4 Time-Point + Chamber Assignment

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SCH-01 | H | R1 | The system shall generate the pull schedule from the protocol's time-points + start date; missed pulls (beyond the configured tolerance window) shall raise alerts and create deviations in the eQMS. |
| URS-SCH-02 | H | R1 | The system shall create LIMS sample requests at each pull with the protocol-specified test methods. |
| URS-SCH-03 | H | R1 | A pull shall be marked complete only with a captured chain-of-custody (sample retrieved from chamber, withdrawn-by user, timestamp). |
| URS-SCH-04 | H | R1 | The system shall assign samples to specific qualified chambers; chamber qualification status shall block scheduling against a non-qualified chamber. |
| URS-SCH-05 | M | R2 | Time-point tolerance windows shall default to ICH Q1A(R2) recommendations (e.g., ± 7 d for early pulls, ± 14 d for ≥ 12 month pulls) and shall be configurable per protocol. |

### 5.5 Photostability (ICH Q1B)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PHOTO-01 | H | R1 | The system shall support ICH Q1B Option 1 (cool white fluorescent + near-UV) and Option 2 (Xe-arc) lamp configurations; lamp exposure (Wh/m² near-UV + lux·h visible) shall be captured per study. |
| URS-PHOTO-02 | H | R1 | The system shall verify the minimum exposure thresholds per Q1B (1.2 million lux·h visible + 200 Wh/m² near-UV) before the study can be closed. |
| URS-PHOTO-03 | H | R1 | Photostability sample groups (test, control 1 protected from light, control 2 dark exposure) shall be tracked separately and shall enforce comparison per Q1B Annex 2. |

### 5.6 Bracketing and Matrixing (ICH Q1D)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MATRIX-01 | H | R1 | The system shall support full + reduced (bracketing / matrixing) designs per ICH Q1D; the reduced-design rationale shall be required as a structured input. |
| URS-MATRIX-02 | H | R1 | Matrixing schemes (1/2, 1/3 reduction) shall be configurable per design; the system shall warn when reduced design covers < 50 % of the full design (Q1D caution case). |
| URS-MATRIX-03 | H | R1 | When a matrixed time-point is missed, the system shall flag the design integrity loss and shall require statistician review. |

### 5.7 Results, Trending, ICH Q1E Analysis

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RES-01 | H | R1 | The system shall retrieve approved results from LIMS and bind them to the pull; partial-pull results shall be visible but final-pull review shall require complete results. |
| URS-RES-02 | H | R1 | OOT (out-of-trend) detection per the protocol's trending rules; OOT shall raise an investigation. |
| URS-RES-03 | H | R1 | OOS results retrieved from LIMS shall block the protocol from progressing until the OOS investigation is closed. |
| URS-RES-04 | H | R1 | The system shall perform shelf-life prediction per ICH Q1E (regression with appropriate model selection — linear, log-linear, square-root — driven by AIC; covariate-pooling test at α = 0.25 per Q1E § 4.2; one-sided 95 % CI); calculations shall be version-controlled and verified per OQ. |
| URS-RES-05 | H | R1 | The system shall report poolability decisions across batches (poolability test α = 0.25 for slopes, α = 0.25 for intercepts per Q1E); failure shall yield per-batch shelf-life. |
| URS-RES-06 | M | R2 | Trend visualisations shall be available per attribute / condition / batch / pooled view. |

### 5.8 Shelf-Life Extension Justification

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SLE-01 | H | R1 | Shelf-life extension proposals shall be supported by ≥ 3 commercial batches with ≥ 12 months long-term data per ICH Q1E; extrapolation beyond observed data shall be limited per Q1E § 3.2.2 (twice the observed period or observed + 12 months, whichever is shorter). |
| URS-SLE-02 | H | R1 | Extension requests shall route through statistician + Head of QC + Head of QA co-approval; the supporting Q1E regression, model fit, and CI shall be embedded in the approval record. |
| URS-SLE-03 | M | R2 | The system shall trigger an alert when an active stability dataset crosses a confidence-interval boundary that would invalidate the registered shelf-life. |

### 5.9 Reference + Comparator Standard Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RS-01 | H | R1 | Reference standards (primary + secondary + working) shall be inventoried with lot, source (USP / EP / JP / in-house), assigned potency, expiry, storage condition, qualification status. |
| URS-RS-02 | H | R1 | The system shall block sample testing against an expired or unqualified reference standard. |
| URS-RS-03 | H | R1 | Re-qualification of working standards shall route through change control with comparison to primary or pharmacopoeial. |
| URS-RS-04 | M | R2 | For ICH Q5C biotech products, the system shall manage comparator standard / reference material qualification status separately. |

### 5.10 Biotech-Specific Stability (ICH Q5C)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BIO-01 | H | R1 | The system shall support orthogonal stability-indicating methods (e.g., CEX-HPLC + SEC-HPLC + iCIEF + bioassay) per ICH Q5C; results from all methods shall be evaluated together for shelf-life. |
| URS-BIO-02 | H | R1 | The system shall capture freeze / thaw stability data per Q5C § 2.2.7.4 (frozen drug substance) with cycle count and condition. |
| URS-BIO-03 | M | R2 | The system shall flag a stability-indicating method whose validation status is expired per Q5C method-revalidation interval. |

### 5.11 Audit Trail

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Time-stamped, secure audit trail covering protocol changes, schedule changes, pull events, result retrievals, OOT / OOS investigations, signatures, shelf-life proposals, reference-standard transitions per EU GMP Annex 11 § 9. |
| URS-AUD-02 | H | R1 | Audit trail append-only; no admin update / delete. |
| URS-AUD-03 | H | R1 | Audit-trail review by Stability Operations Manager monthly and QA Compliance quarterly. |
| URS-AUD-04 | H | R1 | Retention ≥ 25 years from product expiry. |

### 5.12 21 CFR Part 11

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-50 | H | R1 | E-signatures shall include printed name, date / time, meaning per 21 CFR § 11.50. |
| URS-PART11-70 | H | R1 | Signatures shall be cryptographically bound to the signed record per § 11.70. |
| URS-PART11-100 | H | R1 | Each signature shall be unique per § 11.100. |
| URS-PART11-200 | H | R1 | Re-authentication shall be required at signing per § 11.200(a)(1). |
| URS-PART11-300 | H | R1 | Password and credential controls shall meet § 11.300 (uniqueness, periodic change, loss-of-control management). |

### 5.13 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-LIMS-01 | H | R1 | Sample requests shall be pushed to LIMS; results shall be pulled from LIMS via REST with idempotency. |
| URS-INT-EMS-01 | H | R1 | Chamber-condition data (T / RH) shall be consumed read-only from Vaisala viewLinc; deviations within the protocol pull window shall be flagged for investigation; MKT shall be recomputed per ICH Q1A(R2) § 2.1.7.2. |
| URS-INT-VAULT-01 | M | R2 | Protocols shall reference Veeva Vault QualityDocs URNs for the controlling specifications. |
| URS-INT-EQMS-01 | H | R1 | Missed pulls / OOT / OOS shall raise eQMS deviations via REST with idempotency. |
| URS-INT-APR-01 | M | R2 | The system shall expose a read-only summary endpoint for the APR / PQR tool (`MIR-URS-APR-001`) to consume. |

### 5.14 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | Records shall be Attributable. |
| URS-DI-02 | H | R1 | Records shall be Legible. |
| URS-DI-03 | H | R1 | Records shall be Contemporaneous. |
| URS-DI-04 | H | R1 | Originals shall be preserved; corrections shall be recorded with reason. |
| URS-DI-05 | H | R1 | Q1E calculations shall be Accurate per OQ. |
| URS-DI-06 | H | R1 | All ALCOA+ attributes (Complete, Consistent, Enduring, Available) shall be enforced per PIC/S PI 041. |

### 5.15 Backup / Performance / Security / Training / Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | Database shall be backed up nightly with PITR; retention ≥ 25 years. |
| URS-BAK-02 | H | R1 | Quarterly restore test shall be witnessed. |
| URS-PERF-01 | M | R2 | Trend / shelf-life calculations on a typical product (3 batches × 5 time-points × 6 attributes) shall complete in ≤ 30 seconds. |
| URS-SEC-01 | H | R1 | Authentication via AD + MFA; no local accounts other than break-glass. |
| URS-TRN-01 | H | R1 | Production access shall require LMS-recorded training. |
| URS-PR-01 | H | R1 | Annual periodic review covering configuration, audit-trail review, missed-pull rate, OOT / OOS trends, Q1E model-selection review, photostability data, training; signed by Stability Operations Manager + Head of QC + Head of QA. |

### 5.16 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem; conditional-access policy `Quality-App Conditional Access (MFA + device-compliance for OOT / OOS e-signature)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the stability study DB; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 15 y past last released lot per the consuming-record schedule. |

### 5.17 Cross-System Integration — eQMS CAPA handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-EQMS-01 | H | R1 | On detection of Stability OOT / OOS (trigger: out-of-trend or out-of-specification stability data point), the system shall push a CAPA-ticket creation event to the Talos MasterControl eQMS (`TLB-URS-EQMS-001`) via the eQMS event-push channel with required metadata {originating_system, originating_record_id, finding_class, severity, evidence_package_uri, detection_ts_utc, detection_user, regulatory_basis}; severity per ICH Q1E + site OOS procedure; OOS → critical; OOT → major. |
| URS-XINT-EQMS-02 | H | R1 | The eQMS ticket-creation call shall be idempotent on `{originating_system, originating_record_id, finding_class}`; the eQMS status-callback shall be ingested and reflected on the originating record with a hyperlink to the eQMS ticket; closed-loop verification per ICH Q9(R1) + ICH Q10 shall be evidenced before the originating record is dispositioned. |

## 6. Acceptance Criteria

System enters validated GMP use when CS, RA, IQ, OQ, PQ approved and executed; PQ includes a representative protocol through pull-creation → LIMS push → LIMS result retrieval → ICH Q1E shelf-life prediction → reporting, plus a representative photostability run (ICH Q1B), a representative matrixed design (ICH Q1D), and a representative biotech Q5C protocol; VSR approved; RTM maps every URS-ID to ≥ 1 approved test case.

## 7. Constraints

- Vendor patches under change control.
- Statistical-model changes (e.g., Q1E poolability α threshold) require change control + statistician approval.

## 8. Assumptions

- LIMS, EMS (Vaisala viewLinc), Vault, eQMS, AD are validated.
- Reference toxicology / pharmacopoeial source documents are maintained by RA.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300
- 21 CFR Part 211 § 211.166 (Stability Testing) + § 211.137 (Expiration Dating)
- FDA Guidance for Industry: *Stability Testing of Drug Substances and Drug Products* (1998)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11 — Computerised Systems
- EU GMP Annex 15 — Qualification and Validation

### International — ICH
- ICH Q1A(R2) — Stability Testing of New Drug Substances and Products
- ICH Q1B — Photostability Testing
- ICH Q1C — Stability Testing for New Dosage Forms
- ICH Q1D — Bracketing and Matrixing Designs
- ICH Q1E — Evaluation of Stability Data
- ICH Q5C — Stability Testing of Biotechnological / Biological Products

### Pharmacopoeial
- USP <659> Packaging and Storage Requirements
- USP <1150> Pharmaceutical Stability

### Industry guidance — ISPE / PIC/S / WHO
- ISPE GAMP 5 (2nd Edition, 2022) — Cat 4 conventions
- PIC/S PI 041 — Good Practices for Data Management and Integrity
- WHO TRS 953 Annex 2 — Stability Testing of Active Pharmaceutical Ingredients
- WHO TRS 1010 Annex 10 — Storage and Transport of Time- and Temperature-sensitive Pharmaceutical Products

### Vendor
- Genohm — *SLIMS Stability Module 6.7 Installation, Configuration, and Administration Reference*
- Vaisala viewLinc 5.2 (chamber-monitoring; separate URS)

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

