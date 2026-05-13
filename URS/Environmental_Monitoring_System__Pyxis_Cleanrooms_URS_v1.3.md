---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; expanded 2026-05-12 (T2 enrichment — Annex 1 (2022) grades + CPM + viable + alert/action limits)"
seed_corpus_basis:
  - "PharmaDevils Stability-PC URS family (structural reference)"
  - "GAMP 5 (2nd ed.) Cat 4 conventions for monitoring platforms"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11; EU GMP Annex 1 (2022 revised)"
  - "ISO 14644-1/-2/-3 cleanroom particle classification; ISO 14698 biocontamination"
  - "USP <1116> Microbiological Control and Monitoring"
  - "PIC/S PI 041"
  - "FDA CSA (Feb 2026)"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Environmental Monitoring System — Vaisala viewLinc 5.2 + Lighthouse APM / ApexZ Continuous Particle Monitors

**Document Number:** PXC-URS-EMS-001
**Version:** 1.2
**Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Pyxis Cleanrooms BV, Sterile Drug Substance Plant 1, Leiden, the Netherlands *(fictional)*
**System Owner:** Facilities Engineering Lead — Cleanrooms
**Process Owner:** Head of Manufacturing — Sterile
**Development Owner:** Quality IT — Facilities Custom Apps
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Vaisala viewLinc 5.2 + Lighthouse APM / ApexZ Continuous Particle Monitors** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Annex 1 (2022 revised) — Manufacture of Sterile Medicinal Products; PIC/S PI 041; ISO 14644-1 / -2 / -3 (cleanroom classification + monitoring + test methods); ISO 14698 (biocontamination); USP <1116>; FDA CSA (Feb 2026).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Facilities Engineering Lead) | _____________ | _____________ | _____ |
| Reviewer (IT / System Administrator) | _____________ | _____________ | _____ |
| Reviewer (Microbiology / EM Manager) | _____________ | _____________ | _____ |
| Reviewer (Cleanroom Engineer) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Approver (Head of Sterile Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Minor: grade-A/B alarm redundancy clarification. |
| 1.2 | 2026-05-12 | (synthetic) | Tier-T2 enrichment: §5 broken into 13 subsections; Annex 1 (2022) grade A/B/C/D mapping (§5.2); viable / non-viable / settle / contact / air-active sampling integration (§5.3 + §5.6); continuous particle monitoring (CPM) per Annex 1 (§5.4); alert/action limits + trend analysis (§5.5); ~60-req target. Authored to **Tier T2** (50-80 reqs; configured platform with multi-vendor sensor integration). |

## Definitions

| Term | Definition |
|---|---|
| EMS | Environmental Monitoring System |
| viewLinc | Vaisala viewLinc 5.2 — server / client software for the Vaisala wireless monitoring network |
| HMP / DLP | Vaisala HMP-series probes / DL-series data loggers |
| EM | Environmental Monitoring (process — viable + non-viable particle counts; this URS covers physical parameters: T / RH / DP / particle counts) |
| BMS | Building Management System (separately validated) |
| Grade A/B/C/D | EU GMP Annex 1 cleanroom-grade classification |
| ISO 5/6/7/8 | ISO 14644-1 cleanroom particle classification (Grade A ≈ ISO 5 in operation; Grade B ≈ ISO 5 at rest / ISO 7 in operation; etc.) |
| CPM | Continuous Particle Monitoring (Annex 1) |
| APC / ApexZ | Active Air Sampler / portable particle counter (Lighthouse) |
| Settle plate | Passive viable sampling (gravimetric, agar) |
| Contact plate | Surface viable sampling (RODAC-style) |
| Active-air sampling | Volumetric viable air sampling (impactor / SAS / MAS) |
| Alert / Action limit | EM-trending thresholds per the site EM plan / Annex 1 |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the EMS used to continuously monitor temperature, humidity, differential pressure, non-viable particle counts (continuous and at rest), and to manage viable EM (settle / contact / active-air) result records in cleanrooms, controlled-temperature storage areas, and warehouses at Pyxis Plant 1. The system supports EU GMP Annex 1 (2022) requirements, ISO 14644 classification monitoring, and USP <1116> microbiological control + monitoring.

## 2. Scope

**In scope:** the viewLinc 5.2 server pair (active + warm standby on Windows Server 2022), the wireless gateway network, ~180 calibrated Vaisala probes / loggers, ~25 Lighthouse APM continuous particle monitors + portable ApexZ for at-rest / qualification sampling, viable-result data entry interface for settle plates / contact plates / active-air samples, alarm-routing to operators (email, SMS, mobile push), AD authentication, daily backup, NTP sync; integrations with the BMS (read-only sharing of cleanroom HVAC trend data), the eQMS (deviation creation on alarms exceeding limit thresholds), Watson LIMS (viable-result entry + microbial-ID linkage), batch-record system (PAS-X for EM-batch-relevance), Halcyon stability (excursion-impact linkage for stored samples).

**Out of scope:** the underlying HVAC system; viable EM physical sampling activities (manual workflow; results entered into the system); the cleanroom BMS itself (separate validation `BMS-CSV-2024-002`); microbiology lab platform.

## 3. System Description and Intended Use

The system continuously logs T / RH / DP / particle counts at configured intervals, compares values against per-location limits, raises and routes alarms, and provides reports for batch-record support, periodic trend analysis, and Annex 1 compliance. Viable EM results from settle plates / contact plates / active-air samples are entered manually (or via LIMS pull) and trended alongside non-viable parameters. The EMS produces grade-specific reports per Annex 1 grade A / B / C / D and per ISO 14644 cleanroom class. GAMP Cat 4: Vaisala + Lighthouse maintain the platforms under their published SDLCs; site validation focuses on configuration (locations, probes, alarm rules, limit tables), the integration boundary, and 21 CFR Part 11 controls.

## 4. User Roles

| Role | Permissions |
|---|---|
| Operator / Shift Lead | View live status; acknowledge alarms; cannot modify configuration. |
| EM Reviewer | Review trend data; raise deviations; enter viable EM results; cannot configure. |
| Microbiology / EM Manager | Co-approve alert / action limit changes; review trends. |
| Facilities Engineer | Configure locations, probes, alarm rules under change control. |
| Calibration Coordinator | Update probe calibration metadata; cannot configure alarm rules. |
| EM Approver / QA | Approve EM reports for batch release; approve configuration changes. |
| System Administrator | Server / OS / AD; cannot approve EM reports or configuration. |
| Auditor | Read-only across data and audit trails. |
| Inspection-Read-Only | Time-bound read-only for regulator inspection. |

Separation of duties: Operator ≠ Reviewer ≠ Approver of the same EM report; Facilities Engineer ≠ Approver of own configuration change; Microbiology Manager co-approves limit changes.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` / `R2` / `R3`), and a verifiable `shall`-clause.

### 5.1 Platform / Hardware

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | Active / warm-standby viewLinc server pair with manual failover within 1 hour. |
| URS-PLAT-02 | H | R1 | Servers and gateways on UPS for ≥ 30 minutes ride-through. |
| URS-PLAT-03 | H | R1 | Servers on dedicated facilities-IT VLAN; no office-network access. |
| URS-PLAT-04 | M | R2 | Wireless gateway network designed with overlap so any single gateway failure does not lose probe data; the system flags reduced redundancy. |

### 5.2 Cleanroom Grade A/B/C/D Mapping (Annex 1 + ISO 14644)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-GRADE-01 | H | R1 | Each monitored location shall be classified per EU GMP Annex 1 (2022) cleanroom grade: Grade A, B, C, or D; the grade shall be recorded in the location configuration. |
| URS-GRADE-02 | H | R1 | Each location shall additionally carry the ISO 14644-1 class (in operation + at rest) for cross-reference. |
| URS-GRADE-03 | H | R1 | Per-grade alert / action limits (T / RH / DP / particle counts at-rest + in-operation) shall be configured per the site EM plan + Annex 1; changes to limits shall require Microbiology Manager co-approval. |
| URS-GRADE-04 | H | R1 | Grade-A and Grade-B locations shall have enhanced monitoring per Annex 1 § 9: continuous particle monitoring for ≥ 0.5 µm and ≥ 5 µm channels. |
| URS-GRADE-05 | M | R2 | Grade-A locations shall have redundant continuous particle monitoring with auto-failover; loss of CPM on a grade-A location shall be a critical alarm. |

### 5.3 Probes / Loggers / Particle Counters

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PROBE-01 | H | R1 | Each probe / logger / particle counter shall have a unique identifier, location assignment, calibration certificate ID, calibration due date. |
| URS-PROBE-02 | H | R1 | Calibration-overdue devices shall be flagged and excluded from release-supporting reports until recalibrated. |
| URS-PROBE-03 | H | R1 | Probe drift shall be detected via configurable health-check thresholds; suspected drift shall raise a maintenance alarm. |
| URS-PROBE-04 | H | R1 | Logging interval per location is configured under change control (default 1 minute for cleanrooms, 5 minutes for warehouses). |
| URS-PROBE-05 | M | R2 | Particle counter coincidence-loss corrections shall be applied per the vendor reference. |

### 5.4 Continuous Particle Monitoring (CPM) per Annex 1

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CPM-01 | H | R1 | CPM in grade-A locations shall be continuous through the entire critical-zone operation per Annex 1 § 9.16; ≥ 0.5 µm and ≥ 5 µm channels reported. |
| URS-CPM-02 | H | R1 | CPM in grade-B locations shall be performed during operations per the site EM plan; ≥ 0.5 µm and ≥ 5 µm channels reported. |
| URS-CPM-03 | M | R2 | CPM data shall be linked to the batch records produced in the affected grade-A / B locations. |
| URS-CPM-04 | M | R2 | At-rest classification monitoring per ISO 14644-2 shall be scheduled and recorded; results compared against the qualification baseline. |

### 5.5 Alarm Logic and Excursion Handling

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ALARM-01 | H | R1 | Alarms classified by severity: Information, Warning, Action Limit, Alert Limit; routing rules per severity (operator screen, email, SMS, paging). |
| URS-ALARM-02 | H | R1 | Action / Alert Limit alarms shall require operator acknowledgement with a captured reason and shall auto-create an eQMS deviation if not closed within the configured window. |
| URS-ALARM-03 | H | R1 | Annex 1 grade-A and grade-B locations shall have alarm-routing redundancy (at least two independent channels). |
| URS-ALARM-04 | M | R2 | Alarm-acknowledgement latency to the operator screen ≤ 30 seconds at the 95th percentile. |
| URS-ALARM-05 | M | R2 | Excursion events shall be linked to affected batches by location + time-window; impact-assessment auto-triggered downstream. |

### 5.6 Settle / Contact / Active-Air (Viable) Sampling Integration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VIAB-01 | H | R1 | Viable sampling results (settle plates, contact plates, active-air samples) shall be entered into the EMS via the EM Reviewer interface or pulled from Watson LIMS; each result links to location + sample-time + grade + analyst. |
| URS-VIAB-02 | H | R1 | Viable results shall be trended alongside non-viable parameters; exceedances of alert / action limits per Annex 1 shall auto-deviate. |
| URS-VIAB-03 | M | R2 | Microbial-ID results (from LIMS) shall be linkable to the source sample for excursion investigations. |
| URS-VIAB-04 | M | R2 | Viable-sampling schedule (per location + cadence) shall be configurable and shall be flag-able on missed samples. |

### 5.7 Trend Analysis + Alert / Action Limits

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TREND-01 | H | R1 | Rolling-window trend analysis (24-h / 7-d / 30-d) shall be computed continuously per location + per parameter; surfaced via dashboard. |
| URS-TREND-02 | H | R1 | Alert / Action limit excursions shall be tracked over rolling windows; recurring excursions shall be flagged for trend-investigation per Annex 1 § 9. |
| URS-TREND-03 | M | R2 | Periodic-review reports shall include false-positive / false-negative trends, alert / action limit excursions, calibration overdue events. |
| URS-TREND-04 | M | R2 | Limit changes shall be tracked under change control; trend baselines shall be re-established after limit changes. |

### 5.8 Audit Trail

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Audit trail covering configuration changes (locations, probes, alarm rules, limits), data corrections, alarm acknowledgements, viable result entry, and signatures. |
| URS-AUD-02 | H | R1 | Audit trail append-only; no application or admin update / delete. |
| URS-AUD-03 | H | R1 | Audit-trail review by EM Reviewer monthly and QA Compliance quarterly. |
| URS-AUD-04 | H | R1 | Retention: ≥ 25 years from product expiry for data supporting batch release. |

### 5.9 21 CFR Part 11 / Annex 11

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a): procedural controls protect electronic-record validity. |
| URS-PART11-02 | H | R1 | Per § 11.10(d): access limited to authorised individuals via AD + MFA. |
| URS-PART11-03 | H | R1 | Per § 11.10(e): operational audit trail per URS-AUD-01. |
| URS-PART11-04 | H | R1 | Per § 11.50: e-signatures include printed name, date / time, meaning. |
| URS-PART11-05 | H | R1 | Per § 11.70: signatures cryptographically linked to the signed record. |
| URS-PART11-06 | H | R1 | Per § 11.100: signatures unique per individual; reuse / reassignment blocked. |
| URS-PART11-07 | H | R1 | Per § 11.200: re-authentication required at the moment of signing. |
| URS-PART11-08 | H | R1 | Per § 11.300: password / credential controls per InfoSec policy. |

### 5.10 Reporting

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RPT-01 | H | R1 | Batch-release EM report shall include all monitored locations relevant to the batch, the time window, alarm summary, viable result summary, signature page, and report hash. |
| URS-RPT-02 | H | R1 | Periodic trend reports shall be configurable (daily, weekly, monthly, quarterly) and signed by the EM Reviewer + Microbiology Manager. |
| URS-RPT-03 | M | R2 | Reports shall reference the probe-calibration certificate IDs valid for the reported window. |
| URS-RPT-04 | M | R2 | Reports shall be grade-aware: per-grade summaries (A / B / C / D) with Annex 1 limits applied. |

### 5.11 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-EQMS-01 | H | R1 | Action-Limit and Alert-Limit alarms not closed within the configured window shall auto-create an eQMS deviation via REST API with idempotency. |
| URS-INT-BMS-01 | M | R2 | viewLinc shall consume BMS HVAC trend data (read-only) for cross-reference; the BMS is the controlling system, viewLinc is the monitoring system of record. |
| URS-INT-LIMS-01 | H | R1 | Watson LIMS viable-result + microbial-ID data shall be consumed via secure REST; linkage to sample + location preserved. |
| URS-INT-MES-01 | M | R2 | Batch-record system (PAS-X) shall be queried for EM-batch-relevance (which batches in which rooms at which time); EM reports linked. |
| URS-INT-STAB-01 | M | R2 | Excursion events affecting stored stability samples shall be pushed to Halcyon Stability for sample-impact assessment. |
| URS-INT-AD-01 | H | R1 | Authentication via AD; service accounts use credential vault. |

### 5.12 Data Integrity (ALCOA+) + Backup + Performance + Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | **Attributable:** records attributable to a named user. |
| URS-DI-02 | H | R1 | **Legible:** records exportable as PDF / CSV. |
| URS-DI-03 | H | R1 | **Contemporaneous:** synchronised NTP timestamps; gateway-side buffering for short network outages preserves probe-side timestamps. |
| URS-DI-04 | H | R1 | **Original:** raw probe readings preserved unaltered; corrections recorded as new annotated values referencing the original. |
| URS-DI-05 | H | R1 | **Accurate:** calculations (rolling averages, classification per ISO 14644) Accurate per OQ. |
| URS-DI-06 | M | R2 | **Complete / Consistent / Enduring / Available:** ≥ 25-yr retention; available ≤ 1 business day. |
| URS-BAK-01 | H | R1 | Database backed up nightly with PITR; retention ≥ 25 years. |
| URS-BAK-02 | H | R1 | Quarterly restore test, witnessed. |
| URS-BAK-03 | M | R2 | RTO ≤ 4 h; RPO ≤ 5 min (replication). |
| URS-PERF-01 | H | R1 | The system shall sustain logging from all probes at the configured interval without data loss for at least 30 days of continuous operation in OQ. |
| URS-PERF-02 | M | R2 | Trend-report generation for a typical batch window (e.g., 96 hours, 30 locations) ≤ 30 seconds. |
| URS-SEC-01 | H | R1 | All accounts AD-managed; no local accounts other than break-glass. |
| URS-SEC-02 | H | R1 | Alarm-routing channels (SMS / email / push) authenticated and rate-limited; outbound connectivity allow-listed. |
| URS-SEC-03 | M | R2 | Vulnerability scans monthly; criticals remediated within 30 days. |

### 5.13 Training / Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Production access requires recorded role-specific training (LMS). |
| URS-TRN-02 | M | R2 | Annual refresher training including Annex 1 (2022) updates + viable-sampling SOPs. |
| URS-PR-01 | H | R1 | Annual periodic review covering configuration, calibration status, alarm performance metrics (false-positive / false-negative trends), viable result trends, alert / action limit changes, backup-restore, training currency, fitness for use; signed by Facilities Engineering Lead + Microbiology Manager + Head of QA. |

### 5.14 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem; conditional-access policy `OT-EMS Conditional Access (MFA at engineering workstation; operator stations named-location)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the EMS historian DB; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 15 y (batch-history) per the consuming-record schedule. |

### 5.15 Cross-System Integration — eQMS CAPA handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-EQMS-01 | H | R1 | On detection of Environmental excursion (trigger: Grade A/B/C/D excursion (viable, non-viable, T/RH/dP)), the system shall push a CAPA-ticket creation event to the Talos MasterControl eQMS (`TLB-URS-EQMS-001`) via the eQMS event-push channel with required metadata {originating_system, originating_record_id, finding_class, severity, evidence_package_uri, detection_ts_utc, detection_user, regulatory_basis}; severity per EU GMP Annex 1 (2022); Grade-A excursion → critical. |
| URS-XINT-EQMS-02 | H | R1 | The eQMS ticket-creation call shall be idempotent on `{originating_system, originating_record_id, finding_class}`; the eQMS status-callback shall be ingested and reflected on the originating record with a hyperlink to the eQMS ticket; closed-loop verification per ICH Q9(R1) + ICH Q10 shall be evidenced before the originating record is dispositioned. |

## 6. Acceptance Criteria

System enters validated GMP use when CS, RA, IQ, OQ, PQ approved and executed; PQ includes ≥ 30 days continuous logging, end-to-end alarm scenarios for each severity, eQMS deviation creation, viable-result entry roundtrip with LIMS, CPM coverage on grade-A/B, and a documented failover; VSR approved by Facilities Engineering Lead + Microbiology Manager + Head of QA; RTM maps every URS to ≥ 1 approved test case.

## 7. Constraints

- Vendor patches under change control.
- Probe-network design changes require revalidation of affected locations.
- Alert / action limit changes require Microbiology Manager + QA approval.
- Annex 1 (2022) limits are non-negotiable; configuration cannot relax below regulator-defined minima.

## 8. Assumptions

- BMS, AD, eQMS, NTP, Watson LIMS, PAS-X, Halcyon are validated.
- Calibration laboratory is approved.
- Microbiology lab routinely performs viable sampling per the site EM plan and provides results.

## 9. References

### US — FDA / CFR / USP
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .22, .42 (cleanroom + sterile facilities).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026).
- USP <1116> — Microbiological Control and Monitoring of Aseptic Processing Environments.

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- **EU GMP Annex 1 (2022 revised)** — Manufacture of Sterile Medicinal Products; Contamination Control Strategy (CCS).
- EU GMP Chapter 4 — Documentation.

### International — ISO / PIC/S
- ISO 14644-1 — Classification of air cleanliness by particle concentration.
- ISO 14644-2 — Monitoring to provide evidence of cleanroom performance.
- ISO 14644-3 — Test methods.
- ISO 14698-1 / -2 — Biocontamination control.
- PIC/S PI 041 — Good Practices for Data Management and Integrity.

### Industry — ISPE
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE Good Practice Guide — *Environmental Monitoring*.

### Vendor
- Vaisala — *viewLinc 5.2 Installation, Configuration, and Administration Reference*.
- Lighthouse Worldwide Solutions — *APM + ApexZ Reference Manuals*.
- Particle Measuring Systems / MET ONE / TSI AeroTrak (alternate / future vendors — reference).
- Charles River Endosafe (cross-reference for water + endotoxin context).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

