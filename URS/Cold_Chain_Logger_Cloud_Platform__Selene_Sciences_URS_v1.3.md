---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; enriched 2026-05-12 (T2 uplift per METHODOLOGY § 2A.13)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed.) Cat 4 conventions for SaaS configurable platforms"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "EU GDP (2013/C 343/01); WHO TRS 957 Annex 9; USP <1079> Risks and Mitigation Strategies for the Storage and Transportation of Finished Drug Products"
  - "ICH Q1A(R2) Stability Testing of New Drug Substances and Products"
  - "PIC/S PI 041; IEC 60068-3-5 Environmental conditioning"
  - "BfArM (DE), Swissmedic (CH), AGES PharmMed (AT) GDP inspection annexes"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Cold Chain Logger Cloud Platform — ELPRO ecolog-NET LIB v2.4 + Liberty cloud

**Document Number:** SLN-URS-COLDCHAIN-001 | **Version:** 1.0 | **Effective Date:** 2026-04-26 *(synthetic)*
**Site:** Selene Sciences AE, Distribution Hub Athens (GR HQ) + EU distribution centres in Konstanz (DE), Basel (CH), Wien (AT) *(fictional)*
**System Owner:** Cold-Chain Logistics Lead | **Process Owner:** Head of Supply Chain
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS; vendor handles infrastructure; site validates configuration)
**Project Mode:** Configuration project on commercial software product **ELPRO ecolog-NET LIB v2.4 + Liberty cloud** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GDP (2013/C 343/01); WHO TRS 957 Annex 9; USP <1079>; ICH Q1A(R2); PIC/S PI 041; IEC 60068-3-5; BfArM (DE) AMG GDP; Swissmedic (CH) GDP-Richtlinie; AGES PharmMed (AT).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Cold-Chain Logistics Lead) | _____________ | _____________ | _____ |
| Reviewer (Vendor Assurance — ELPRO owner) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Stability / Quality Investigator) | _____________ | _____________ | _____ |
| Approver (Head of Supply Chain) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | T2 enrichment per METHODOLOGY § 2A.13 (50–80 reqs): added § 5.2 Logger Registration + Commissioning lifecycle; § 5.5 Lane Qualification + Temperature-Mapping integration; § 5.7 CTNS (Cumulative Time Not Stored / stability-budget) tracking; § 5.8 Excursion → Stability/QC hand-off workflow; § 5.9 Reusable-logger reset SOP enforcement; § 5.10 Multi-tenant CMO/CDMO; 21 CFR Part 11 sub-section-explicit; DACH GDP context (BfArM/Swissmedic/AGES); USP <1079>, ICH Q1A(R2), IEC 60068 added. |

## Definitions

| Term | Definition |
|---|---|
| Cold Chain | Temperature-controlled supply chain (typically 2–8 °C, −20 °C, or −70 °C) |
| ELPRO LIB | ELPRO ecolog-NET LIB v2.4 — local infrastructure box for receiving USB / NFC logger downloads |
| Liberty | ELPRO Liberty cloud platform — multi-tenant SaaS for cold-chain logging |
| Logger | Single-use or reusable temperature data-logger accompanying shipments |
| GDP | Good Distribution Practice |
| Lane | A configured shipping lane (origin → destination, mode, carrier, season profile) |
| MKT | Mean Kinetic Temperature |
| CTNS | Cumulative Time Not Stored — stability-budget metric for temperature excursions over a product's lifecycle |
| Excursion | A temperature reading outside the configured product profile |
| TOR (Time Out of Refrigeration) | Cumulative time above the upper-limit temperature for a shipment |
| Stability Budget | Allowed cumulative excursion per product per ICH Q1A(R2) stability data |
| WMS | Warehouse Management System (SAP EWM) — separate URS |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the cold-chain logger platform that records and analyses shipment temperature profiles for GDP-regulated finished-product distribution from Selene Sciences across EU + DACH + LATAM markets.

## 2. Scope

**In:** ELPRO Liberty cloud (multi-tenant SaaS); site-deployed ELPRO LIB v2.4 box (Linux appliance) for logger downloads at receipt; configuration of stability profiles per product / lane; integrations with WMS (SAP EWM), eQMS (MasterControl), Halcyon Stability (excursion → stability impact), and the lane-qualification + temperature-mapping evidence store; SSO via Okta SAML 2.0 + MFA; vendor-assurance program covering ELPRO.

**Out:** physical loggers (procurement + calibration); carrier execution; ERP general ledger; serialization (separate URS); refrigerator / chamber qualification (separate URS — physical equipment).

## 3. System Description

ELPRO Liberty is the system of record for shipment temperature profiles. For each shipment, a logger is registered + commissioned with the relevant stability profile, accompanies the shipment, and is downloaded at receipt via the LIB box. Liberty evaluates the profile against the stability rules, classifies the shipment (Pass / Excursion-Investigation / Reject), pushes results to the WMS (holds affected stock as needed), creates a deviation in the eQMS for any excursion, and hands off to Halcyon Stability for stability-budget consumption tracking.

GAMP Cat 4: ELPRO maintains the platform under their published SDLC; site validation focuses on configuration, integrations, and 21 CFR Part 11 + EU GDP controls.

## 4. User Roles

| Role | Permissions |
|---|---|
| Logger Operator | Register / commission / start loggers per shipment; download loggers at receipt. |
| Senior Operator | Second-person verification on excursion-classification disputes. |
| Stability Profile Author | Author / edit stability profiles under change control. |
| Stability Profile Approver (QA) | Approve profiles to EFFECTIVE. |
| Cold-Chain Investigator | Investigate excursions; recommend disposition; hand off to Halcyon Stability. |
| Stability Reviewer | Review excursion → stability-budget impact in Halcyon. |
| Disposition Approver (QA) | Approve / reject disposition; release / hold stock via WMS. |
| Lane Qualification Engineer | Maintain lane qualification + temperature-mapping evidence. |
| System Administrator | OS / patch / AD; cannot approve. |
| Auditor | Read-only across data and audit trails. |

**Separation of duties:** Operator ≠ Investigator ≠ Disposition Approver of the same shipment; Profile Author ≠ Approver; Lane Qualification Engineer ≠ Disposition Approver.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` direct GxP impact / `R2` indirect / `R3` none), and a verifiable `shall`-clause.

### 5.1 Vendor / Platform Assurance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-01 | H | R1 | ELPRO shall be qualified as a critical SaaS vendor with documented evidence: SOC 2 Type II, ISO 27001, customer-shared CSV summary, DPA. |
| URS-VND-02 | H | R1 | Vendor releases impact-assessed within 14 days; configuration-affecting changes trigger re-validation. |
| URS-VND-03 | M | R2 | Annual ELPRO TR-Audit summary filed in vendor-assurance dossier. |

### 5.2 Logger Registration and Commissioning

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LOG-REG-01 | H | R1 | Each logger shall be registered in Liberty with serial number, model, firmware version, calibration certificate ID, calibration due-date, and tenant binding. |
| URS-LOG-REG-02 | H | R1 | Loggers shall be classified as single-use or reusable; reusable-logger reset SOP shall be enforced per § 5.9 before re-deployment. |
| URS-LOG-COMM-01 | H | R1 | Logger commissioning shall bind the logger to a shipment-id, stability profile (version-pinned), and lane configuration; binding shall be cryptographic (digital signature). |
| URS-LOG-COMM-02 | H | R1 | Commissioning shall record: shipment-id, profile ID + version, logger serial, calibration cert + due-date, configured-by user, timestamp; loggers with overdue calibration shall be blocked. |
| URS-LOG-COMM-03 | H | R1 | Commissioning data shall be exportable as a chain-of-custody record for inspection. |

### 5.3 Stability Profile Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PROF-01 | H | R1 | Profiles shall follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED. |
| URS-PROF-02 | H | R1 | Each profile shall carry: product code, allowed temperature range, mean kinetic temperature limits, allowed excursions (e.g., < 1 h above 8 °C cumulative), associated stability-budget cap (per ICH Q1A(R2)). |
| URS-PROF-03 | H | R1 | Only EFFECTIVE profiles may be assigned to shipments. |
| URS-PROF-04 | H | R1 | Profile transitions shall require role-restricted signatures with separation of duties. |
| URS-PROF-05 | H | R1 | EFFECTIVE profiles shall be immutable; changes create new revisions via change control. |
| URS-PROF-06 | M | R2 | Profile-version-in-use shall be inspectable per shipment to support root-cause investigation. |

### 5.4 Shipment Profile Evaluation and Classification

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-EVAL-01 | H | R1 | Logger download at receipt shall integrity-check the data (logger checksum / signature); failed checks shall raise an exception. |
| URS-EVAL-02 | H | R1 | Profile evaluation shall classify the shipment automatically (Pass / Excursion-Investigation / Reject) per the EFFECTIVE profile rules. |
| URS-EVAL-03 | H | R1 | Manual classification override shall require dual signature (Investigator + Disposition Approver) + captured reason; override events audit-trailed. |
| URS-EVAL-04 | H | R1 | TOR (Time Out of Refrigeration) shall be computed and reported per shipment; per-shipment TOR vs lane TOR-allowance shall drive classification. |
| URS-EVAL-05 | M | R2 | Profile-evaluation algorithm version shall be stamped on each shipment record. |

### 5.5 Lane Qualification and Temperature-Mapping Integration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LANE-01 | H | R1 | Each lane (origin → destination, mode {air / road / sea}, carrier, season) shall be qualified with documented temperature-mapping evidence per IEC 60068-3-5 / USP <1079>. |
| URS-LANE-02 | H | R1 | Lane qualification evidence (mapping reports, ambient-temperature data, packaging-spec validation) shall be linked from the lane configuration to the inspection-readiness export. |
| URS-LANE-03 | H | R1 | A lane shall be classified Qualified / Provisional / Disqualified; only Qualified lanes shall be used for routine shipping; Provisional lanes require enhanced monitoring + dual approval. |
| URS-LANE-04 | M | R2 | Lane re-qualification cadence shall be configurable (annual default; triggered by carrier change, route change, packaging change). |
| URS-LANE-05 | M | R2 | Seasonal-profile variants shall be supported (summer / winter / shoulder); auto-switch per shipment date. |

### 5.6 21 CFR Part 11 / GDP Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a), procedural controls protecting electronic-record validity documented. |
| URS-PART11-02 | H | R1 | Per § 11.10(d), access via Okta SAML 2.0 + MFA. |
| URS-PART11-03 | H | R1 | Per § 11.10(e), operational audit trail per § 5.11. |
| URS-PART11-04 | H | R1 | Per § 11.50, e-signatures shall include printed name, date/time, meaning. |
| URS-PART11-05 | H | R1 | Per § 11.70, signatures cryptographically bound to record state. |
| URS-PART11-06 | H | R1 | Per § 11.100, signature uniqueness; user-ids never reassigned. |
| URS-PART11-07 | H | R1 | Per § 11.200, re-authentication at signing (disposition approval, profile approval, lane qualification approval). |
| URS-PART11-08 | H | R1 | Per § 11.300, password / credential controls per InfoSec policy. |
| URS-GDP-01 | H | R1 | Distribution evidence per EU GDP § 4 (chapter on Documentation) + § 9 (transportation): receiver country, time-stamped temperature record, qualified-person assessment for excursion-impacted shipments. |
| URS-GDP-02 | H | R1 | Per WHO TRS 957 Annex 9, temperature data shall be preserved for the shelf life of the product + 1 year minimum. |
| URS-GDP-03 | M | R2 | Per USP <1079>, risk-based stability + transportation strategies shall be reflected in lane + profile configuration. |

### 5.7 CTNS (Cumulative Time Not Stored / Stability Budget) Tracking

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CTNS-01 | H | R1 | Per product / batch, a Cumulative Time Not Stored (CTNS) accumulator shall be maintained representing the total cumulative excursion time consumed over the product's lifecycle. |
| URS-CTNS-02 | H | R1 | Per product, a stability budget shall be configurable (per ICH Q1A(R2) stability data) — total allowed excursion at the high or low temperature; CTNS consumption shall be tracked against this budget. |
| URS-CTNS-03 | H | R1 | CTNS-consumption alerts shall fire at configurable thresholds (e.g., 50% / 75% / 90% of stability budget consumed); alerts go to Cold-Chain Logistics Lead + Stability Reviewer. |
| URS-CTNS-04 | H | R1 | Stability budget consumed without alert (silent breach) shall be detected by a daily reconciliation job. |
| URS-CTNS-05 | M | R2 | CTNS data shall be exportable per product for the stability program. |

### 5.8 Excursion → Stability/QC Hand-off

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HANDOFF-01 | H | R1 | Excursion-classified shipments shall auto-create a stability-impact assessment in Halcyon Stability; the assessment shall include profile-version, lane, shipment temperature trace, CTNS consumption. |
| URS-HANDOFF-02 | H | R1 | Excursion shall also auto-create a deviation in MasterControl eQMS with idempotency key = shipment-id. |
| URS-HANDOFF-03 | H | R1 | Disposition decision (release / hold / reject) shall consider the Halcyon impact assessment; disposition shall be captured with linked Halcyon assessment-id. |
| URS-HANDOFF-04 | M | R2 | Hand-off completion shall be reconciled daily; orphans (excursion without Halcyon assessment) raise alert. |

### 5.9 Reusable-Logger Reset SOP

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RESET-01 | H | R1 | Reusable loggers shall pass a reset SOP before re-deployment: data wipe verification, battery check, calibration validity check, time-sync check; reset evidence captured. |
| URS-RESET-02 | H | R1 | Logger battery exhaustion mid-shipment risk shall be mitigated by pre-deployment battery level check (configurable minimum threshold). |
| URS-RESET-03 | M | R2 | Reset-failure events shall block re-deployment and route to Logger Operator for triage. |

### 5.10 Multi-Tenant (CMO / CDMO)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TENANT-01 | H | R1 | Per-tenant data isolation shall be enforced; CMO / CDMO partners shall see only their commissioned loggers and assigned shipments. |
| URS-TENANT-02 | H | R1 | Cross-tenant audit-trail access shall be restricted to authorised Auditor roles with documented justification. |
| URS-TENANT-03 | M | R2 | Tenant onboarding / off-boarding workflow shall include data-export + retention obligations. |

### 5.11 Audit Trail / Records Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Time-stamped, secure audit trail covering profile changes, logger registration / commissioning / download, classification, manual overrides, signatures, lane qualification, CTNS updates. |
| URS-AUD-02 | H | R1 | Audit trail append-only; reviewable in-app + exportable. |
| URS-AUD-03 | H | R1 | Audit-trail review monthly (Cold-Chain Logistics Lead) + quarterly (QA Compliance). |
| URS-AUD-04 | H | R1 | Retention ≥ shelf-life of product + 1 year per WHO TRS 957; ≥ 5 years post-shipment minimum; ≥ 25 years for excursion-impacting events. |

### 5.12 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-WMS-01 | H | R1 | Profile-evaluation results pushed to WMS within 5 min of logger download; Excursion-Investigation classification auto-creates Investigation Hold in WMS. |
| URS-INT-EQMS-01 | H | R1 | Reject + Excursion-Investigation classifications create deviations in MasterControl via REST with idempotency. |
| URS-INT-STAB-01 | H | R1 | Excursion-impact assessment created in Halcyon Stability per § 5.8. |
| URS-INT-AD-01 | H | R1 | Authentication via Okta SAML 2.0 + MFA. |
| URS-INT-CARRIER-01 | M | R2 | Carrier GPS / location feed integration for chain-of-custody evidence. |

### 5.13 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | **Attributable** — records attributable to a named user / commissioned logger. |
| URS-DI-04 | H | R1 | **Original** logger data preserved unaltered; corrections recorded as new annotated records. |
| URS-DI-05 | H | R1 | **Accurate** — profile-evaluation logic + CTNS calculations validated under OQ. |
| URS-DI-06 | M | R2 | **Complete / Consistent / Enduring / Available** — retention per § 5.11. |

### 5.14 Performance / Availability / Backup / Security / Training / Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | Profile evaluation time ≤ 30 s per logger at P95. |
| URS-AV-01 | H | R1 | Availability per ELPRO published SLA (≥ 99.5%). |
| URS-BAK-01 | H | R1 | Vendor-managed backup; site verifies vendor-published RPO ≤ 4 h, RTO ≤ 24 h annually. |
| URS-BAK-02 | M | R2 | Site shall retain a quarterly tenant-data export with ≥ 5-year retention. |
| URS-SEC-01 | H | R1 | All authentication via Okta + MFA; TLS 1.3 in transit; AES-256 at rest. |
| URS-SEC-02 | M | R2 | Annual penetration test; high/critical findings remediated within 60 days. |
| URS-TRN-01 | H | R1 | Production access requires LMS-recorded role-specific training; Cold-Chain Investigator competency required. |
| URS-PR-01 | H | R1 | Annual periodic review covering: profile inventory, excursion trends, CTNS consumption metrics, integration health, vendor-assurance status, lane re-qualification status, training currency; signed by Cold-Chain Logistics Lead + Head of QA. |

### 5.15 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is SAML 2.0 via Entra ID for tenant admin; logger-device certificates for ingest authentication; conditional-access policy `Standard SaaS Conditional Access (MFA + named-location)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the SaaS-tenant data-warehouse mirror; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 5 y past distribution (cold-chain record) per the consuming-record schedule. |

### 5.16 Cross-System Integration — eQMS CAPA handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-EQMS-01 | H | R1 | On detection of Cold-chain excursion (trigger: temperature out-of-range during transit or storage), the system shall push a CAPA-ticket creation event to the Talos MasterControl eQMS (`TLB-URS-EQMS-001`) via the eQMS event-push channel with required metadata {originating_system, originating_record_id, finding_class, severity, evidence_package_uri, detection_ts_utc, detection_user, regulatory_basis}; severity per WHO cold-chain guidance; excursion > 24 h → critical. |
| URS-XINT-EQMS-02 | H | R1 | The eQMS ticket-creation call shall be idempotent on `{originating_system, originating_record_id, finding_class}`; the eQMS status-callback shall be ingested and reflected on the originating record with a hyperlink to the eQMS ticket; closed-loop verification per ICH Q9(R1) + ICH Q10 shall be evidenced before the originating record is dispositioned. |

## 6. Acceptance Criteria

CS, RA, IQ, OQ, PQ approved and executed; PQ shall include representative end-to-end scenarios: (1) logger registration → commissioning → shipment → download at receipt → profile evaluation → Pass classification; (2) excursion scenario with Halcyon hand-off + eQMS deviation + WMS hold; (3) reusable-logger reset SOP; (4) lane qualification + provisional-lane shipping; (5) CTNS budget consumption breach; (6) DR failover. VSR approved by Head of Supply Chain + Head of QA.

## 7. Constraints

- Vendor releases not under site change control; site impact assessment within 14 days.
- Configuration baselines re-tested as needed.
- Lane qualification gating for Qualified status.

## 8. Assumptions

- WMS (SAP EWM), eQMS (MasterControl), Halcyon Stability, Okta operational and validated.
- Logger calibration laboratory qualified per ISO 17025.
- Carrier-GPS feed available per active carrier contract.

## 9. References

### US
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- USP <1079> — Risks and Mitigation Strategies for the Storage and Transportation of Finished Drug Products.
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EU GDP Guidelines (2013/C 343/01) — Chapter 9 (Transportation).
- EudraLex Volume 4 (referenced for GMP context).

### DACH (per METHODOLOGY § 2A.6)
- BfArM (DE) AMG GDP requirements.
- Swissmedic (CH) GDP-Richtlinie.
- AGES PharmMed (AT) GDP inspection annex.

### International
- WHO TRS 957 Annex 9 — Model guidance for the storage and transport of time- and temperature-sensitive pharmaceutical products.
- ICH Q1A(R2) — Stability Testing of New Drug Substances and Products.
- IEC 60068-3-5 — Environmental testing — Confirmation of the performance of temperature chambers.
- ISO/IEC 17025 — General requirements for the competence of testing and calibration laboratories.

### Industry
- ISPE GAMP 5 (2nd Edition, 2022); ISPE GAMP Good Practice Guide *Good Distribution Practice and Cold Chain*.
- PIC/S PI 041.

### Vendor
- ELPRO — *Liberty / ecolog-NET LIB Validation Approach*.
- ELPRO — *Liberty Cloud Configuration Reference*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

