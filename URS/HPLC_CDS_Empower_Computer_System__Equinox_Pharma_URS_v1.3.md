---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch 2026-04-26; T2 enrichment 2026-05-13 (Chunk A Empower)"
seed_corpus_basis:
  - "PharmaDevils HPLC/Empower URS family"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300"
  - "21 CFR Part 211 §§ .68, .180, .192, .194(a)(8)"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "USP <621>; USP <1058> AIQ; USP <1224>-<1226>"
  - "ICH Q2(R2); ICH Q3A(R2); ICH Q9(R1); ICH Q14"
  - "PIC/S PI 041"
  - "Waters — Empower 3 FR5 Installation, Configuration, and Administration Reference (vendor doc)"
  - "Waters — Empower-LIMS Connector 4.2 Reference"
  - "BfArM (DE — medicinal products + medical devices for DACH site context)"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# User Requirements Specification (URS)

## HPLC Chromatography Data System — Waters Empower 3 FR5 (Networked, Citrix-published)

**Document Number:** EQX-URS-EMPOWER-001 | **Version:** 1.0 | **Effective Date:** 2026-04-26 *(synthetic)*
**Site:** Equinox Pharma GmbH, QC HPLC Cluster, Stuttgart, Germany *(fictional)*
**System Owner:** QC Manager — Chromatography
**Process Owner:** Head of Quality Control
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Waters Empower 3 FR5 (Networked, Citrix-published)** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192, .194(a)(8); EU GMP Annex 11 §§ 4, 6, 9, 11; USP <621>; USP <1058> AIQ; USP <1224>-<1226>; ICH Q2(R2); ICH Q3A(R2); ICH Q9(R1); ICH Q14; PIC/S PI 041; BfArM (DE — medicinal products)

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Chromatography) | _____________ | _____________ | _____ |
| Reviewer (IT / System Administrator) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-13 | (synthetic) | Authored to Tier T2 (50-80 req target; Cat 4 networked CDS multi-instrument cluster). Added §§ 5.6 Empower Project/Method/Result hierarchy, 5.7 SST per USP <621>, 5.8 Calibration Curve + Quantitation, 5.9 Reprocessing + Result Lineage, 5.10 Multi-site Project-Folder Federation, 5.11 Method Lifecycle, 5.12 Stability + Release Workflow. Expanded §§ 5.4 Audit Trail + Part 11 (sub-section bindings), 5.5 LIMS Interface. New risks (R-05..R-12): manual re-integration without justification (Hetero / Sun / Ranbaxy WL precedent), project-folder corruption, raw-data-lock bypass, calibration-curve outlier suppression, RT-shift on column-lot change, schema mismatch in LIMS push, project-folder federation drift. Web-research citations added: 21 CFR § 211.194(a)(8), USP <1058> AIQ, USP <1224>-<1226>, ICH Q14, BfArM context. |

## Definitions

| Term | Definition |
|---|---|
| Empower | Waters Empower 3 FR5 chromatography data system |
| LAC/E | Lab Acquisition and Control Engine (data acquisition node) |
| Networked Empower | Server-based deployment with multiple LAC/E acquisition nodes |
| Citrix-published | Empower client delivered via Citrix Virtual Apps to thin-client workstations |
| LIMS | LabWare LIMS 8 |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the networked Empower 3 deployment that controls and processes data from 24 HPLC and UPLC instruments across the Equinox Pharma QC chromatography cluster.

## 2. Scope

**In:** Empower 3 FR5 server cluster (active + DR) on Windows Server 2022 + Oracle 19c, 24 LAC/E acquisition nodes serving 24 HPLC / UPLC instruments (Waters Alliance and Acquity), Citrix-published Empower client to thin-client workstations, AD authentication on `equinox.local`, integration to LabWare LIMS 8 (Empower-LIMS Connector 4.2), daily backup, NTP sync.
**Out:** physical instruments (separate equipment qualification); UV / PDA / refractive-index / charged-aerosol detectors (instrument-level qualifications); LIMS sample-lifecycle.

## 3. System Description

Empower is the system of record for HPLC / UPLC chromatographic data across release, stability, and method-validation activities. Methods are managed under change control; analyses are run via project / sequence; results are reviewed and approved through Empower's eSign workflow; approved results are pushed to LIMS. GAMP Cat 4: Waters maintains the Empower SDLC; site validation focuses on installation, configuration (projects / methods / users / projects-policy), Part 11 controls, and the LIMS interface.

## 4. User Roles

| Role | Permissions |
|---|---|
| Analyst | Acquire / process; cannot edit method or system configuration. |
| Senior Analyst | All Analyst + second-person review. |
| Method Owner | Author / edit methods under change control. |
| QC Manager | Approve, lock, release results to LIMS. |
| System Administrator | Empower system-level config, AD groups; cannot approve. |
| Auditor | Read-only across data and audit trails. |

Separation of duties: Analyst ≠ Reviewer ≠ Approver.

## 5. User Requirements

### 5.1 Platform / Hardware

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | Empower server cluster active + DR (cold replica); RPO ≤ 15 min; RTO ≤ 4 h. |
| URS-PLAT-02 | H | R1 | Each LAC/E on UPS for ≥ 30 min controlled shutdown; instruments fail-safe to safe state. |
| URS-PLAT-03 | H | R1 | Server / LAC/E / Citrix on a dedicated lab-IT VLAN; no office-network access. |

### 5.2 Software Configuration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SW-01 | H | R1 | Empower 3 FR5 installed by Waters or Waters-trained engineer; site SOP for SCN updates. |
| URS-SW-02 | H | R1 | Projects organised per product / programme; project-level access enforced via AD-mapped roles. |
| URS-SW-03 | H | R1 | Project-policy settings (raw data lock, eSign, audit-trail-required) applied to all GxP projects. |
| URS-SW-04 | H | R1 | Clock synced to `ntp.equinox.local`, skew ≤ 1 s. |
| URS-SW-05 | M | R2 | Citrix-published client fixed-version; user profile non-persistent. |

### 5.3 Acquisition / Processing

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ACQ-01 | H | R1 | Methods follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE; only EFFECTIVE methods may be selected. |
| URS-ACQ-02 | H | R1 | The system shall reject the start of a sequence if any of: instrument not Ready, no approved method, project locked. |
| URS-ACQ-03 | H | R1 | Capture per-injection metadata: sample ID, vial position, injection volume, method ID + version, instrument ID, analyst, timestamp. |
| URS-ACQ-04 | H | R1 | System suitability per USP <621> shall run at sequence start (resolution, tailing, theoretical plates, RSD); SST failure blocks results acceptance. |
| URS-PROC-01 | H | R1 | Apply approved processing method (peak integration, calibration). |
| URS-PROC-02 | H | R1 | Manual reintegration / re-fit calibration shall require captured reason for change (Empower's reason-for-change feature). |
| URS-PROC-03 | H | R1 | Raw data preserved; Empower's project-policy "raw data lock" shall be enforced. |
| URS-PROC-04 | H | R1 | Compare results to spec; flag at 30 / 50 / 100% of limit. |
| URS-PROC-05 | H | R1 | Generate PDF report including chromatogram, integrated peaks, calibration curve, calculated values, ALCOA+ statement, hash. |

### 5.4 Audit Trail and Records (Annex 11 § 9, 21 CFR § 11.10(e))

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Empower audit trail shall capture per-action user, timestamp (UTC + local), action type, target artefact, old value, new value, and reason-for-change for project, sample, method, integration, calibration, sign-off, and result-modification events. |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only at the database level (Oracle GRANT model restricts UPDATE/DELETE on audit tables to no role); system administrators shall not be able to modify entries. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be performed per batch by a Senior Analyst (event-driven) and monthly by the QC Manager (periodic); review evidence shall be retained as a controlled record. |
| URS-AUD-04 | H | R1 | Retention shall be ≥ 7 years (general); ≥ 25 years if the audit-trail entry is linked to a product release record per 21 CFR § 211.180. |
| URS-AUD-05 | M | R2 | The system shall expose a documented mechanism to export audit trails (per project, per date range, per user) for inspection without disrupting routine operation. |

### 5.5 21 CFR Part 11 Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a), the system shall be validated to ensure accuracy, reliability, and consistent intended performance. |
| URS-PART11-02 | H | R1 | Per § 11.10(b), the system shall generate accurate and complete copies of records in human-readable (PDF/A-3) and electronic form for inspection. |
| URS-PART11-03 | H | R1 | Per § 11.10(c), records shall be protected throughout the 25-year retention horizon (Oracle PITR + continuous archived redo logs + immutable cold storage). |
| URS-PART11-04 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via AD authentication; no local Empower accounts other than break-glass. |
| URS-PART11-05 | H | R1 | Per § 11.10(e), operational audit trail per § 5.4 shall exist. |
| URS-PART11-06 | H | R1 | Per § 11.10(g), Empower authority sets shall be mapped to AD groups; user authority enforced server-side. |
| URS-PART11-07 | M | R2 | Per § 11.10(k), Empower SCN updates managed under site CR; system-operation manual maintained. |
| URS-PART11-08 | H | R1 | Per § 11.50, electronic signatures shall include signer's printed name, date and time of signature, and meaning of signature (closed-list: Review / Approve / Reject / Lock). |
| URS-PART11-09 | H | R1 | Per § 11.70, signatures shall be cryptographically bound to the signed record via Empower's eSign ledger (signature payload includes record hash). |
| URS-PART11-10 | H | R1 | Per § 11.100, each electronic signature shall be unique to the individual; reuse / reassignment prohibited at AD level. |
| URS-PART11-11 | H | R1 | Per § 11.200, re-authentication shall be required at the moment of signing (no cached credentials). |
| URS-PART11-12 | H | R1 | Per § 11.300, password / credential controls shall enforce complexity, expiry, lockout (5 failures / 15-min window per site policy). |
| URS-PART11-13 | H | R1 | Separation of duties shall be enforced: Analyst ≠ Senior Reviewer ≠ QC Manager / Approver on the same sample/result. |

### 5.6 Empower Project / Method / Result Hierarchy

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-EMP-01 | H | R1 | Empower projects shall be organised per product / programme; project naming shall follow site convention `<PROGRAMME>-<PRODUCT>-<TYPE>` (e.g., `STAB-PROD42-REL`); project policy applied to all GxP projects (raw-data-lock=ON, eSign=ON, audit-trail-required=ON, reason-for-change=ON). |
| URS-EMP-02 | H | R1 | Per-project access shall be enforced via AD-mapped roles; the role-mapping table shall be version-controlled and re-reviewed quarterly. |
| URS-EMP-03 | H | R1 | A project shall not be reassignable across programmes after first acquisition; rename shall require QC Manager + Head of QA eSign + audit-trail entry. |
| URS-EMP-04 | H | R1 | Within a project, processing methods shall be bound to result-sets at integration time; the binding shall be immutable after Senior Analyst review. |
| URS-EMP-05 | M | R2 | Project-folder archive shall be exportable as a self-contained `.eax` (Empower project archive) bundle for inspection or migration. |

### 5.7 System Suitability Test per USP <621>

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SST-01 | H | R1 | The system shall execute a method-specific SST at the start of every analytical sequence per USP <621>; SST parameters shall include resolution (R), tailing factor (Tf), theoretical plates (N), retention-time RSD, peak-area RSD on replicate injections; thresholds method-bound. |
| URS-SST-02 | H | R1 | SST acceptance shall be evaluated automatically by Empower; the system shall block release of any quantitative result downstream of a failed SST until the SST is repeated and passes. |
| URS-SST-03 | H | R1 | The SST record shall be persisted as an `SST-Result` entity with criteria thresholds, observed values, pass/fail per parameter, overall verdict, and cryptographic reference to the sequence. |
| URS-SST-04 | M | R2 | Bracketed SST shall be supported for sequences ≥ 30 injections; bracket-end failure shall flag all bracketed results as suspect pending investigation. |

### 5.8 Calibration Curve and Quantitation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-QNT-01 | H | R1 | Calibration curves shall be constructed from method-specified standards (≥ 6 non-zero levels for quantitative assay; ≥ 5 for related substances per ICH Q2(R2)); r² evaluated automatically (r² ≥ 0.99 for assay). |
| URS-QNT-02 | H | R1 | Calibration outliers shall be flagged using validated outlier rules (% back-calculation outside ± 15% nominal for non-LOQ standards, ± 20% at LOQ); exclusion of any standard shall require Method Owner signature with reason. |
| URS-QNT-03 | H | R1 | Results shall be computed using the method-bound equation set in IEEE-754 double precision; rounding rules per site SOP `EQX-SOP-CHROM-ROUND-001` applied only at final-report generation. |
| URS-QNT-04 | H | R1 | The system shall flag any result exceeding 30%, 50%, and 100% of the specification limit (Trend / OOT / OOS per FDA OOS guidance 2022). |

### 5.9 Reprocessing and Result Lineage

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RPR-01 | H | R1 | Manual re-integration shall require Empower's reason-for-change feature with a closed list of reasons (baseline-noise / co-elution / peak-shoulder / etc.) + free-text justification; un-justified re-integration shall be impossible to save. |
| URS-RPR-02 | H | R1 | Reprocessing with a new processing-method version shall preserve the original `Result` and create a new `Result` with parent-pointer; both visible in the result lineage tree. |
| URS-RPR-03 | H | R1 | When reprocessing produces a quantitatively different result from an approved Result (> 0% delta), the system shall raise a `RESULT_DIFFERS_ON_REPROCESS` flag and require Method Owner + QC Manager dual eSign + deviation record before external reporting / LIMS push. |
| URS-RPR-04 | M | R2 | Result lineage shall be exportable as a tree (DOT / JSON) for inspection. |

### 5.10 Multi-Site Project-Folder Federation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-FED-01 | H | R1 | Where the Empower instance federates with a sister site's Empower (e.g., Bergisch Gladbach + Stuttgart), federated project-folder access shall require explicit federation grant per project (no implicit sharing); grant captured in audit trail. |
| URS-FED-02 | H | R1 | Federated read-only access shall be supported; federated write access shall be prohibited (results created on a remote site are read-only at home site). |
| URS-FED-03 | M | R2 | Federation health (replication lag, last-sync timestamp, divergence detection on result-hashes) shall be monitored; lag > 24 h shall trigger alert. |

### 5.11 Method Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MTH-01 | H | R1 | Methods shall follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE; only EFFECTIVE methods may be selected for GxP runs. |
| URS-MTH-02 | H | R1 | Method state-transitions shall require eSign with Author ≠ Reviewer ≠ Approver; history retained immutably. |
| URS-MTH-03 | H | R1 | A method's `MatrixType` and `ColumnLot` enforcement shall be configurable; sequences shall be blocked when method-bound matrix / column-lot does not match the sample/instrument context. |
| URS-MTH-04 | M | R2 | Method-change-impact assessment shall be captured: list of all in-flight projects / result-sets affected by a method change. |

### 5.12 Stability and Release Workflow

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REL-01 | H | R1 | Results destined for product release shall pass a `Release` workflow: Analyst → Senior Reviewer → QC Manager → QA Approver (4-eyes-plus-QA model); each transition records an eSign with meaning. |
| URS-REL-02 | H | R1 | Stability results shall be tagged with stability-time-point + storage-condition; mis-tagging shall be flagged at Senior-Reviewer step. |
| URS-REL-03 | M | R2 | A held release record (result approved by QC Manager but not yet by QA) shall persist for ≤ 30 days; expiry shall require re-approval from QC Manager. |

### 5.13 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | **Attributable:** Every action shall be attributable to a named AD user; service-account-only actions prohibited at the GxP boundary. |
| URS-DI-02 | H | R1 | **Legible:** Records exportable as PDF/A-3 (human-readable) + native `.eax` (electronic). |
| URS-DI-03 | H | R1 | **Contemporaneous:** Entries posted retrospectively shall be flagged with the actual entry timestamp and a reason. |
| URS-DI-04 | H | R1 | **Original:** Raw chromatographic data file shall be preserved unaltered (Empower Raw Data Lock = ON for all GxP projects). |
| URS-DI-05 | H | R1 | **Accurate:** Calculations and rounding shall be tested per the OQ protocol; calibration-curve fit determinism verified. |
| URS-DI-06 | M | R2 | **Complete / Consistent / Enduring / Available:** all metadata fields populated, chronological order preserved, retention met, retrievable within 1 business day during inspection. |

### 5.14 LIMS Interface

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-LIMS-01 | H | R1 | Worklist import from LabWare LIMS 8 via Empower-LIMS Connector 4.2 (read-only on LIMS side); imported worklist cached locally and bound to the sequence. |
| URS-INT-LIMS-02 | H | R1 | Approved results shall be pushed to LIMS only after QC Manager approval (and QA Approver if release-bound); rejected, in-review, or unapproved results blocked at the connector layer. |
| URS-INT-LIMS-03 | H | R1 | Result payload to LIMS shall include report-id, project-id, method-id + version, sequence-id, instrument-id, SST-record-id, calibration-curve-id, analyst-id, reviewer-id, approver-id, raw-data hash, result hash, and Trend/OOT/OOS flag; LIMS shall reject payloads missing any field. |
| URS-INT-LIMS-04 | M | R2 | LIMS interface failures (connection, schema mismatch, duplicate report-id) shall be logged and surface to the System Administrator within 5 minutes. |

### 5.15 Backup, Restore, Disaster Recovery

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | Oracle 19c database backed up nightly with PITR (continuous archived redo logs); retention ≥ 25 years for release-linked projects, ≥ 7 years general. |
| URS-BAK-02 | H | R1 | Quarterly restore test, witnessed by QA, with restore from immutable cold storage to a non-production target. |
| URS-BAK-03 | M | R2 | RTO ≤ 4 hours after cluster failover; RPO ≤ 15 minutes via Oracle Data Guard. |
| URS-BAK-04 | M | R2 | Annual DR test (full failover to DR cluster + sample sequence acquisition on DR + failback). |

### 5.16 Performance and Availability

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | The system shall sustain 24-instrument concurrent acquisition without data loss. |
| URS-PERF-02 | M | R2 | Citrix client open + project-load latency ≤ 10 s at the 95th percentile under nominal load. |
| URS-PERF-03 | M | R2 | Sequence-start UI response ≤ 5 s P95. |
| URS-AV-01 | H | R1 | System availability ≥ 99.5% during business hours, excluding planned maintenance windows announced ≥ 7 days in advance. |

### 5.17 Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | All authentication via AD; no local Empower accounts other than break-glass admin (quarterly access review). |
| URS-SEC-02 | H | R1 | Password complexity and rotation shall meet the site Information Security policy. |
| URS-SEC-03 | H | R1 | Removable media (USB drives, optical) shall be blocked on LAC/E nodes and on Citrix-published clients except for vendor-approved engineering use under CR. |
| URS-SEC-04 | M | R2 | Anti-malware definitions updated daily; LAC/E node anti-malware tuned per Waters' exclusion list to avoid acquisition interference. |
| URS-SEC-05 | M | R2 | Network segmentation: Empower app/db tier, LAC/E tier, and Citrix tier on separate VLANs with firewall rules between. |

### 5.18 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Role-specific training in the LMS shall be completed before AD-group membership and Empower role assignment. |
| URS-TRN-02 | M | R2 | Annual refresher training shall be required; LMS shall revoke AD-group membership on overdue + 30 days. |
| URS-PR-01 | H | R1 | Annual periodic review shall cover project inventory, audit-trail review evidence, deviation summary, SCN-update history, integration health, training currency, and continued fitness for use; signed by QC Manager + Head of QA. |
| URS-PR-02 | M | R2 | The periodic review shall produce a documented disposition for any drift / non-conformance findings. |

### 5.19 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem (Empower service-account bind) with Citrix-published interactive Kerberos; conditional-access policy `Lab-Workstation Conditional Access (MFA on interactive logon; LAC/E nodes named-location)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with Oracle RMAN for the Empower Oracle 19c backend plus continuous archived-redo-log shipping; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 7 y (≥ 25 y if release-linked) per the consuming-record schedule. |

### 5.20 Cross-System Integration — Helios audit-trail handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HEL-01 | H | R1 | Empower CDS shall publish audit-trail events (Empower project / method / result / signature / re-integration events; reason-for-change captured per Waters reason-codes) to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract (JSON Lines, schema-registry pinned, Kafka topic `helios.ingest.equinox.empower.v1`) within 5 minutes of event capture; 21 CFR § 11.10(e) audit-trail completeness shall be preserved end-to-end so that no event class is lost at the boundary. |
| URS-XINT-HEL-02 | H | R1 | Pre-handover audit-trail retention on the Empower CDS side shall be ≥ 7 y regardless of Helios availability; once Helios acknowledges ingest (per-message ack with idempotency key), Helios is the system-of-record for review and the Empower CDS local copy serves as the durability backstop until the local retention floor expires. |

## 6. Acceptance Criteria

CS, RA, IQ, OQ, PQ approved and executed; PQ includes representative concurrent multi-instrument acquisition + result push to LIMS; VSR approved.

## 7. Constraints

- Waters SCN updates under change control.

## 8. Assumptions

- AD, LIMS, Citrix, NTP are validated.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 — Electronic Records; Electronic Signatures §§ .10(a/b/c/d/e/g/k), .50, .70, .100, .200, .300.
- 21 CFR Part 211 — Current Good Manufacturing Practice §§ .68 (automated equipment), .180 (general records), .192 (production-record review), .194(a)(8) (laboratory records — complete record of all data).
- FDA *Guidance for Industry: Investigating Out-of-Specification (OOS) Test Results* (2022).
- FDA *Guidance on Data Integrity and Compliance With cGMP* (2018).

### EU
- EU GMP Annex 11 — Computerised Systems §§ 4 (validation), 6 (accuracy checks), 9 (audit trail), 11 (periodic evaluation).
- EudraLex Volume 4 — Good Manufacturing Practice.

### DACH
- BfArM (DE) — Bundesinstitut für Arzneimittel und Medizinprodukte — inspecting authority for medicinal products (this site is in Stuttgart, DE).
- Swissmedic (CH); AGES PharmMed (AT) — cited where multi-site partnerships apply.

### USP
- USP <621> — Chromatography (system-suitability parameters).
- USP <1058> — Analytical Instrument Qualification (AIQ).
- USP <1224> Transfer of Analytical Procedures; <1225> Validation of Compendial Procedures; <1226> Verification of Compendial Procedures.

### International — ICH
- ICH Q2(R2) — Validation of Analytical Procedures.
- ICH Q3A(R2) — Impurities in New Drug Substances.
- ICH Q9(R1) — Quality Risk Management.
- ICH Q14 — Analytical Procedure Development.

### Industry guidance
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE GAMP GPG: *Validation of Laboratory Computerized Systems*.
- ISPE GAMP GPG: *Records and Data Integrity*.
- PIC/S PI 041.

### Vendor
- Waters — *Empower 3 FR5 Installation, Configuration, and Administration Reference*.
- Waters — *Empower-LIMS Connector 4.2 Reference*.
- Waters — *Acquity / Alliance LAC/E Node Hardware Reference*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

