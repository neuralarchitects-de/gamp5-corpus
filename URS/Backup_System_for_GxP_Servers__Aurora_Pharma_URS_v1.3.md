---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; Wave 3 Chunk J expanded 2026-05-12 (T2 catch-up: 3-2-1-1-0 + immutable backups, restore validation cadence per Annex 11 § 4.8 + § 7.2, ransomware response, NIS2 incident reporting, per-Part 11 sub-section bindings)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed., 2022) Cat 3 conventions for non-configured infrastructure software"
  - "21 CFR Part 11 §§ .10, .50, .70, .100"
  - "EU GMP Annex 11 §§ 4.8 (backup), 7 (data storage), 9 (audit trail), 12 (security)"
  - "21 CFR Part 58 § 58.81 (GLP — equipment SOPs incl. backup)"
  - "21 CFR Part 211 § 211.68 (automatic, mechanical and electronic equipment)"
  - "ICH E6(R3) — record retention obligations (Step 4, adopted 6 January 2025)"
  - "PIC/S PI 041"
  - "ISO/IEC 27001:2022 (Annex A.8.13 information backup, A.5.30 ICT readiness)"
  - "NIST SP 800-34 Rev. 1 (Contingency Planning Guide)"
  - "NIST SP 800-209 (Security Guidelines for Storage Infrastructure)"
  - "NIS2 Directive (EU) 2022/2555 Art. 21 (backup management, crisis management)"
  - "GDPR Reg. (EU) 2016/679 Art. 32 (security of processing) + Art. 33 (breach notification)"
  - "ISPE GAMP GPG IT Infrastructure Control and Compliance"
  - "BSI IT-Grundschutz CON.3 (Datensicherungskonzept)"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Backup System for GxP Servers — Veeam Backup & Replication 12.1 + S3 Object-Lock Immutable Tier + LTO-9 Air-Gapped Vault

**Document Number:** AUR-URS-BACKUP-001
**Version:** 1.1
**Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Aurora Pharma OY, IT Operations, Espoo, Finland *(fictional)* — with DR data centre in Tampere, Finland and offsite air-gap vault at a third-party facility (Helsinki)
**System Owner:** GxP IT Infrastructure Lead
**Process Owner:** Head of IT
**System Class (GAMP 5, 2nd ed.):** Category 3 — Non-Configured Product (commercial backup software used out-of-the-box; site does not author code or non-trivial configuration logic)
**Project Mode:** Configuration project on non-configurable instrument / appliance **Veeam Backup & Replication 12.1 + S3 Object-Lock Immutable Tier + LTO-9 Air-Gapped Vault** (GAMP 5 Category 3 — Non-Configurable COTS).
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a/b/c/d/e), .50, .70, .100; 21 CFR Part 211 § 211.68 + § 211.180; 21 CFR Part 58 § 58.81 + § 58.195; EU GMP Annex 11 §§ 4.8, 7, 9, 12; ICH E6(R3) retention; PIC/S PI 041; ISO/IEC 27001:2022 Annex A.8.13 + A.5.30; NIS2 Directive (EU) 2022/2555 Art. 21; GDPR Art. 32

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (GxP IT Infrastructure Lead) | _____________ | _____________ | _____ |
| Reviewer (Information Security Officer) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Data Protection Officer) | _____________ | _____________ | _____ |
| Approver (Head of IT) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. 11 §5 subsections, ~30 requirements. |
| 1.1 | 2026-05-12 | (synthetic) | **Authored to Tier T2** (mid-complexity GxP infrastructure backup — 50-80 req target; spans coverage, methods, 3-2-1-1-0, immutability, restore-validation cadence, ransomware response, NIS2). Adds 4 §5 subsections; 3-2-1-1-0 rule + LTO-9 air-gap vault; per-Part-11 sub-section bindings; ransomware-recovery playbook; NIS2 incident reporting. |

## Definitions

| Term | Definition |
|---|---|
| Veeam B&R | Veeam Backup & Replication, version 12.1 |
| RPO | Recovery Point Objective — maximum acceptable data loss measured in time |
| RTO | Recovery Time Objective — maximum acceptable downtime from incident to restored production |
| GxP server | Any server hosting validated GxP applications (LIMS, MES, eQMS, EDMS, LMS, etc.) |
| Immutable copy | Backup copy with object lock or tape WORM, not modifiable for the retention window |
| 3-2-1-1-0 rule | Backup strategy: 3 copies of data, 2 different media, 1 off-site, 1 immutable / air-gapped, 0 errors verified |
| Air-gap | Physical or logical isolation preventing network reachability (LTO tape in vault; offline disk) |
| CDP | Continuous Data Protection — near-zero-RPO replication of transactional change |
| Object Lock (S3) | AWS-native WORM / retention API providing immutable object retention (Compliance or Governance mode) |
| LTO-9 | Linear Tape-Open generation 9 — 18 TB native, 45 TB compressed; supports WORM cartridges |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| SIEM | Security Information and Event Management (Splunk Enterprise Security) |
| SOC | Security Operations Centre |
| NIS2 | EU Directive 2022/2555 — Network and Information Security 2 |
| HSM | Hardware Security Module |
| KMS | Key Management Service |
| GxP IT register | Site register of all GxP-relevant servers + applications, mastered by IT Asset Mgmt |

## 1. Purpose

This URS defines requirements for the centralised backup system used to protect all GxP servers across the Aurora Pharma data centres (Espoo primary + Tampere DR) and the offsite air-gap vault in Helsinki. The system protects regulated electronic records governed by 21 CFR Part 11, EU GMP Annex 11, ICH E6(R3) GCP, and 21 CFR Part 58 GLP; protects them against accidental loss, hardware failure, deliberate tampering, ransomware, and force-majeure scenarios; and supports periodic restore-validation evidence required by EU GMP Annex 11 § 7.2 + § 4.8.

The system is **GAMP Category 3** — Veeam B&R is a commercial backup product deployed out-of-the-box. The site does not author scripts that materially affect data integrity beyond standard configuration (job definitions, retention policies, schedules); any such scripting would trigger a separate Cat-5 sub-component validation. Validation effort is therefore proportionate per ISPE GAMP 5 (2nd ed.) § 6 and ISPE GAMP GPG *IT Infrastructure Control and Compliance*.

Aurora Pharma is additionally classified as an *essential entity* under NIS2 Directive (EU) 2022/2555 (Annex I sector 5, manufacture of medicinal products). The backup system is in scope of NIS2 Art. 21 backup management and crisis management obligations, with Art. 23 incident reporting where a backup-touching event meets the NIS2 incident threshold.

## 2. Scope

**In scope:** Veeam B&R 12.1 backup server pair (active in Espoo + DR in Tampere) on Windows Server 2022; primary repositories (ExaGrid deduplicating disk in Espoo + Tampere); immutable cloud tier (AWS S3 with Object Lock in Compliance mode, region `eu-north-1`); air-gapped LTO-9 vault at a third-party facility in Helsinki with WORM cartridges and dual-courier chain-of-custody; Veeam proxy / repository / WAN-accelerator infrastructure; configured backup jobs for all GxP servers in scope of the GxP IT register (`AUR-IT-GxP-REG-001`); database-aware backup integrations (Oracle RMAN, MS SQL Server VSS, PostgreSQL pg_basebackup + WAL archiving) executed through Veeam application-aware processing; restore-test procedures and the cadence governing them; integration with the site monitoring (Prometheus / Loki / Grafana), the SIEM (Splunk Enterprise Security), and the ticketing platform (ServiceNow); chain-of-custody documentation for tape rotation.

**Out of scope:** Veeam infrastructure-software development (vendor-managed); the GxP applications themselves (each application's own URS governs its data); database-engine-internal dump procedures that are governed by per-application validation but are *consumed* by Veeam jobs; customer-facing portal data (separate URS); long-term records-management archive (separate Veeva Vault Submissions URS).

### 2.1 Information Flow Summary

1. **GxP servers → Veeam:** image-level VM backups + agent-based backups for physical hosts + application-aware database backups.
2. **Veeam Espoo → Veeam Tampere:** WAN-accelerated replication for DR copy (3-2-1 second copy + offsite).
3. **Veeam → S3 Object Lock (eu-north-1):** immutable cloud-tier copy for the regulatory retention window (3-2-1-1).
4. **Veeam → LTO-9 vault (Helsinki):** monthly tape rotation with WORM media for absolute air-gap (3-2-1-1-0 completion + ransomware insurance).
5. **Veeam → SIEM:** job-status events, configuration changes, restore operations, integrity-check results.
6. **Veeam → AD:** authentication; group-based authorisation per AD-managed roles.
7. **Restore-test events → eQMS:** scheduled cadence + sign-off evidence captured as quality records.

## 3. System Description and Intended Use

The backup system performs scheduled backups of all GxP servers, replicates to the DR site, writes immutable copies to the cloud Object-Lock tier, and rotates monthly air-gap tape sets to the offsite vault per the 3-2-1-1-0 strategy. Veeam Application-Aware Processing uses native database engines (Oracle RMAN, MS SQL VSS, PostgreSQL streaming) to produce consistent backups for transactional systems; image-level backups handle VM-level recovery for non-database workloads.

The IT infrastructure team performs scheduled restore tests; per-application teams perform application-level restore tests on their own validation cadence. Restore-test evidence is the regulatory artefact required by EU GMP Annex 11 § 7.2 + § 4.8 — the ability to reliably restore is required to be demonstrated periodically — and is treated as a quality record retained for the application's full record-retention window.

The system is designed for ransomware resistance: immutable cloud-tier + air-gapped tape mean that even a compromise of every Aurora-administered system (including a privileged-account abuse against the Veeam servers) cannot delete the immutable copies before their retention window expires. This is the regulatory + operational counterweight to the modern threat landscape; it is also what NIS2 Art. 21 backup-management expects of essential entities.

## 4. User Roles

| Role | Permissions | SoD enforcement |
|---|---|---|
| Backup Operator | Run scheduled jobs; monitor health; run restores per documented procedure. | Operator may not modify retention or repository configuration. |
| Backup Administrator | Configure jobs, retention, repositories under change control. | Changes require change-management approval; cannot delete immutable backups. |
| Application Team Member | Request restores; verify restored data. | Restore execution by Backup Operator on app-team request. |
| QA Reviewer | Review periodic restore-test evidence; sign off. | — |
| Auditor / Inspector | Read-only across job logs and audit trails. | — |
| Tape Courier | Custody of LTO-9 cartridges during transit. | Dual-courier signature on chain-of-custody form per movement. |
| DPO | Read access to backup metadata for GDPR Art. 32 audits. | — |
| SOC Analyst | Read access to backup events forwarded to SIEM; correlate with incident detection. | — |
| Veeam Administrator (vendor support, time-bounded) | Vendor support via PAM-brokered session only. | No standing vendor account. |

Separation of duties: Backup Administrator changes are reviewed and approved before deployment; restore execution by Backup Operator with Application Team verification; immutable-tier deletion is technically impossible during the retention window (governance neutral against admin abuse).

## 5. User Requirements

Requirements are organised into fifteen subsections covering platform, coverage, schedule + retention, RPO/RTO, restore testing, 3-2-1-1-0 immutability, audit trail, Part-11 sub-section alignment, data integrity (ALCOA+), security + encryption, ransomware response + DR, monitoring, performance, training + periodic review, and cross-system integration. Every requirement is a verifiable `shall`-clause carrying an ID, Priority (H/M/L), and Risk class (R1 / R2 / R3).

### 5.1 Platform and Hardware

The platform implements the 3-2-1-1-0 rule across four physical layers: ExaGrid primary disk (Espoo), ExaGrid DR disk (Tampere), AWS S3 Object Lock (eu-north-1), and offsite LTO-9 air-gap vault. Each layer has independent failure domains and independent administrative privilege models — a single compromised credential cannot affect all four.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | The system **shall** include two Veeam B&R servers — primary (Espoo) and DR (Tampere) — with WAN replication and automatic failover documented in the DR runbook. |
| URS-PLAT-02 | H | R1 | Repositories **shall** include: (a) on-site fast-tier ExaGrid in Espoo, (b) DR-site ExaGrid in Tampere, (c) immutable cloud-tier (AWS S3 + Object Lock in Compliance mode) for the regulatory retention window, (d) offsite LTO-9 air-gap tape vault for ransomware resistance. |
| URS-PLAT-03 | H | R1 | Veeam servers and repositories **shall** be sized to meet the configured RPO / RTO (URS-RPO-01..03, URS-RTO-01..02) for all GxP servers in scope with documented headroom of ≥ 30% on storage and ≥ 50% on backup-window throughput. |
| URS-PLAT-04 | H | R1 | The administrative network for Veeam **shall** be on a dedicated VLAN with no direct internet egress; cloud-tier traffic flows through an approved network gateway. |
| URS-PLAT-05 | M | R2 | Hardware lifecycle: ExaGrid + Veeam servers replaced on documented refresh cadence; tape drives serviced per Veeam + LTO vendor maintenance schedule. |

### 5.2 Coverage

Coverage is driven by the GxP IT register `AUR-IT-GxP-REG-001`. The register is the single source of truth for "is this server in GxP scope" — adding a server triggers automatic inclusion in a backup job within 7 calendar days, and the backup-coverage report is reconciled against the register monthly.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-COV-01 | H | R1 | Every server in the GxP IT register (`AUR-IT-GxP-REG-001`) **shall** be in a backup job. Adding a server to the register **shall** trigger inclusion within 7 calendar days; the responsible Application Owner is notified. |
| URS-COV-02 | H | R1 | Each backup job **shall** be classified by application criticality (Tier 1: ≤ 4 h RPO / ≤ 4 h RTO; Tier 2: ≤ 24 h RPO / ≤ 24 h RTO; Tier 3: ≤ 72 h RPO / ≤ 72 h RTO); tier assignment **shall** be documented per application and reviewed annually. |
| URS-COV-03 | H | R1 | Backup-job documentation (which server, frequency, retention, repository, tier, owner) **shall** be exportable for IT and regulatory audits as PDF + CSV. |
| URS-COV-04 | H | R1 | Backup scope per system **shall** include: application data, configuration files, database (consistent), operating-system image, application binaries. |
| URS-COV-05 | M | R2 | New-server onboarding **shall** include a backup-job validation step before the server enters GxP-active state. |

### 5.3 Backup Methods and Schedule

Database-aware backups use native engines (Oracle RMAN, MS SQL Server VSS, PostgreSQL pg_basebackup + WAL streaming) to deliver transactionally consistent backups. Image-level VM backups handle non-database workloads via vSphere or Hyper-V snapshots. The schedule combines full + incremental + synthetic full + monthly archive to balance backup-window cost against restore granularity.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-METH-01 | H | R1 | Database backups **shall** use database-engine native APIs (Oracle RMAN, MS SQL Server VSS, PostgreSQL pg_basebackup + WAL streaming) via Veeam Application-Aware Processing; raw image backups alone are insufficient for transactional database recovery. |
| URS-METH-02 | H | R1 | VM-level workloads **shall** use image-level backups with changed-block tracking; agent-based backups are used for physical hosts. |
| URS-METH-03 | H | R1 | Tier-1 systems **shall** have continuous transaction-log shipping (CDP-equivalent) achieving RPO ≤ 4 hours. |
| URS-SCH-01 | H | R1 | Schedules per tier: Tier 1 daily incremental + weekly synthetic full + monthly archive + continuous transaction-log shipping; Tier 2 / 3 daily incremental + weekly synthetic full + monthly archive. |
| URS-SCH-02 | H | R1 | Retention: daily backups for 30 days; weekly for 12 months; monthly for ≥ 7 years; long-term archive per the application's record-retention requirement (up to 25 years for ICH E6(R3) GCP records, up to 30+ years for PV records, up to 10 years post-EOL for some MDR records). |
| URS-SCH-03 | H | R1 | Immutable cloud-tier copies **shall** be retained for the regulatory retention window of the application; Object-Lock Compliance-mode retention **shall** prevent deletion within window even by AWS-account-root credentials. |
| URS-SCH-04 | H | R1 | Air-gap LTO-9 vault: monthly tape set rotated offsite; retention ≥ 7 years; quarterly read-back integrity verification. |

### 5.4 RPO and RTO

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RPO-01 | H | R1 | RPO targets: Tier 1 ≤ 4 hours (transaction-log shipping); Tier 2 ≤ 24 hours; Tier 3 ≤ 72 hours. |
| URS-RPO-02 | H | R1 | RPO for object-lock cloud copy: ≤ 24 hours for Tier 1; ≤ 7 days for Tier 2; ≤ 30 days for Tier 3. |
| URS-RPO-03 | M | R2 | RPO **shall** be measured per backup job per quarter; deviation triggers job-redesign or tier-re-classification. |
| URS-RTO-01 | H | R1 | RTO targets: Tier 1 ≤ 4 business hours; Tier 2 ≤ 24 business hours; Tier 3 ≤ 72 business hours. |
| URS-RTO-02 | H | R1 | RTO **shall** be measured from declared incident to confirmed application restart; documented runbooks per Tier-1 application are required. |

### 5.5 Restore Testing (Annex 11 § 4.8 + § 7.2)

Annex 11 § 7.2 requires that "regular back-ups of all relevant data should be done" and "integrity and accuracy of backup data and the ability to restore the data should be checked during validation and monitored periodically." § 4.8 requires backup processes to be defined and verified. The cadence below operationalises both: backup-system-level integrity tests monthly, application-level restore tests quarterly, full DR exercises annually. Every restore test produces a signed quality record retained ≥ 25 years.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TEST-01 | H | R1 | Backup-system-level restore tests (data-integrity verification; mounting a backup; restoring a representative file or VM) **shall** be performed monthly across all backup tiers (primary, DR, cloud, tape). |
| URS-TEST-02 | H | R1 | Application-level restore tests **shall** be performed quarterly per Tier-1 application, witnessed by the application team and signed off by the QA Reviewer; test scope **shall** include a complete database restore + application restart + functional verification. |
| URS-TEST-03 | H | R1 | An annual full DR exercise **shall** failover a representative Tier-1 application from Espoo to Tampere using only DR-site copies; cloud-tier and tape-tier recovery procedures **shall** be exercised at least biennially. |
| URS-TEST-04 | H | R1 | Failed restore tests **shall** be classified as a deviation, root-caused, and CAPA'd before the next scheduled test cycle. |
| URS-TEST-05 | H | R1 | A signed restore-test certificate **shall** be retained for every test (test ID, system, backup source, restore target, integrity-check result, sign-off identities + datetime); certificates retained ≥ 25 years. |
| URS-TEST-06 | M | R2 | Restore-test evidence **shall** be inspection-ready: filterable, exportable, and timestamped per ALCOA+. |
| URS-TEST-07 | H | R1 | At least once every 3 years, an unannounced restore drill **shall** be conducted to test operational readiness independent of scheduled cadence. |

### 5.6 3-2-1-1-0 Rule and Immutable Backups

The 3-2-1-1-0 rule is the modern ransomware-aware extension of the classic 3-2-1 rule: at least 3 copies, on at least 2 different media types, with at least 1 offsite, at least 1 immutable / air-gapped, and 0 errors detected on the most recent integrity verification. Each layer of the rule is operationalised in distinct repository / storage technology with distinct administrative privilege.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-IMM-01 | H | R1 | For every GxP server, the backup architecture **shall** maintain ≥ 3 copies of data (primary disk + DR disk + cloud-tier ± tape) on ≥ 2 media types (disk + cloud object + LTO tape) with ≥ 1 offsite (DR data centre + Helsinki vault) and ≥ 1 immutable (S3 Object Lock + LTO WORM) and 0 integrity errors on the last verification cycle. |
| URS-IMM-02 | H | R1 | Cloud-tier immutability **shall** use AWS S3 Object Lock in Compliance mode (not Governance mode) so that no administrator — including AWS root — can delete or shorten retention within the window. |
| URS-IMM-03 | H | R1 | Tape WORM **shall** be enforced through LTO-9 WORM cartridges (write-once media at the firmware level); rewritable tape is not permitted for the regulatory-retention layer. |
| URS-IMM-04 | H | R1 | Object-Lock retention period **shall** be set per application's regulatory retention window and reviewed annually; retention cannot be shortened by configuration. |
| URS-IMM-05 | H | R1 | A documented quarterly verification **shall** confirm immutability is in place across all immutable repositories; evidence retained ≥ 25 years. |
| URS-IMM-06 | M | R2 | The administrative privilege model for the immutable cloud-tier account **shall** be separate from the Veeam-administration privilege model (cross-account isolation in AWS Organizations). |

### 5.7 Audit Trail and Records

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Veeam **shall** log all job executions (success / fail / skipped), configuration changes, role / permission changes, restore operations, and integrity-check results. (Part 11 § 11.10(e); Annex 11 § 9.) |
| URS-AUD-02 | H | R1 | Veeam logs **shall** be forwarded to the site SIEM (Splunk Enterprise Security) within 5 minutes of generation; retained ≥ 7 years in SIEM cold archive with write-once index + cryptographic hash chain. |
| URS-AUD-03 | H | R1 | Configuration changes **shall** be audit-trailed and tied to a change-request ID; orphan (un-ticketed) changes **shall** raise a HIGH-priority alert to InfoSec. |
| URS-AUD-04 | H | R1 | Restore-test evidence (records of tests, results, sign-offs per URS-TEST-05) **shall** be retained ≥ 25 years to cover ICH E6(R3) GCP record-retention obligations consumed by clinical-system backups. |
| URS-AUD-05 | H | R1 | Audit-trail entries **shall** capture timestamp (UTC, ms-precision), event ID, subject identity (AD account), target object, operation, outcome, originating IP / host. |
| URS-AUD-06 | H | R1 | Audit-log integrity verification **shall** run nightly; discrepancies **shall** raise a CRITICAL alert + InfoSec investigation. |

### 5.8 21 CFR Part 11 Sub-Section Alignment

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Part 11 § 11.10(a) — procedures and controls (this URS + change-management SOP + restore-validation SOP) **shall** protect record validity through backup + restore. |
| URS-PART11-02 | H | R1 | Part 11 § 11.10(b) — restored records **shall** be exportable in human-readable + electronic form for inspection. |
| URS-PART11-03 | H | R1 | Part 11 § 11.10(c) — backed-up records **shall** be protected throughout the retention period via immutable cloud-tier + tape WORM + cryptographic hash verification (URS-IMM-* + URS-DI-05). |
| URS-PART11-04 | H | R1 | Part 11 § 11.10(d) — backup-system access **shall** be limited to authorised individuals (URS-SEC-01..05); audit-trail captures every access. |
| URS-PART11-05 | H | R1 | Part 11 § 11.10(e) — backup audit-trail **shall** be operational, time-stamped, and tamper-evident (URS-AUD-01..06). |
| URS-PART11-06 | H | R1 | Part 11 § 11.50 — restore-test sign-offs **shall** be electronically signed with printed name, date / time, meaning (test passed / failed / accepted with deviation). |
| URS-PART11-07 | H | R1 | Part 11 § 11.70 — signature linking: restore-test sign-off **shall** be cryptographically linked to the test record so it cannot be excised. |
| URS-PART11-08 | H | R1 | Part 11 § 11.100 — each restore-test sign-off **shall** be unique to a single individual; the AD identity substrate provides the unique-user guarantee (`QTZ-URS-AD-001` URS-PART11-09 in the AD URS). |
| URS-AN11-01 | H | R1 | Annex 11 § 4.8 — backup processes **shall** be defined; integrity + restore capability verified per URS-TEST-01..07. |
| URS-AN11-02 | H | R1 | Annex 11 § 7.2 — backup integrity + ability to reliably restore **shall** be demonstrated during validation and monitored periodically per URS-TEST-01..04. |
| URS-AN11-03 | H | R1 | Annex 11 § 9 — audit trail operational per URS-AUD-*. |
| URS-AN11-04 | H | R1 | Annex 11 § 12 — physical + logical security per URS-SEC-*. |

### 5.9 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | **Attributable** — backup metadata records the operator / administrator identity for every action (Part 11 § 11.10(e)). |
| URS-DI-02 | H | R1 | **Legible** — backup logs are human-readable + machine-exportable as CSV / PDF / JSON. |
| URS-DI-03 | H | R1 | **Contemporaneous** — backup metadata is generated at the moment of the action; Veeam clock synchronised to authoritative NTP. |
| URS-DI-04 | H | R1 | **Original** — source data is unaltered by backup operations; image / file backups are read-only on the source. |
| URS-DI-05 | H | R1 | **Accurate** — backup integrity is verified via cryptographic checksum / hash on every backup; weekly automated integrity rescans on repository data; nightly comparison of stored hash chain against re-computed values. |
| URS-DI-06 | H | R1 | **Complete + Enduring + Available + Consistent** — immutable cloud-tier + air-gap tape together provide enduring availability against ransomware / insider threats. |

### 5.10 Security and Encryption

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | Veeam authentication **shall** be via AD; role-based access; no local accounts other than two break-glass tier-0 accounts with credentials vaulted in dual physical custody. |
| URS-SEC-02 | H | R1 | All backup traffic **shall** be encrypted in transit (TLS 1.2 minimum; TLS 1.3 preferred) and at rest (AES-256 repository-side encryption); cloud-tier objects encrypted with KMS-managed keys (SSE-KMS) with key rotation annual. |
| URS-SEC-03 | H | R1 | Object-Lock immutable copies **cannot** be deleted within the retention window even by an administrator (Compliance mode); deletion attempts **shall** fail at API level and **shall** raise a SIEM alert. |
| URS-SEC-04 | M | R2 | Vulnerability scans **shall** run monthly on Veeam servers and repositories; CVSS critical vulnerabilities remediated within 30 days; high within 60 days. |
| URS-SEC-05 | H | R1 | Multi-factor authentication **shall** be enforced for backup-administrator accounts (FIDO2 phishing-resistant MFA preferred). |
| URS-SEC-06 | H | R1 | Vendor support sessions **shall** be brokered through PAM (CyberArk) with session recording; no standing vendor accounts on the Veeam platform. |
| URS-SEC-07 | H | R1 | Encryption keys **shall** be HSM-protected (FIPS 140-2 Level 2 minimum); key escrow procedures documented and tested annually. |
| URS-SEC-08 | M | R2 | Network segmentation: Veeam admin plane separated from data-mover plane; firewall rules documented and reviewed quarterly. |

### 5.11 Ransomware Response and Disaster Recovery

Ransomware that compromises the production estate is the modern primary threat to backups; the regulatory + operational architecture is designed so that even in this scenario the immutable cloud-tier + air-gap tape allow restoration to a known-good state. The playbook below operationalises clean-room restore, communication, and forensic preservation.

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RAN-01 | H | R1 | A documented ransomware-response playbook **shall** describe: isolation of the compromised estate; clean-room restore environment (segmented network + freshly built hosts); restore from immutable cloud-tier ± air-gap tape; integrity verification before re-introduction; forensic preservation of compromised images. |
| URS-RAN-02 | H | R1 | Clean-room restore infrastructure **shall** be pre-built (cold-standby capacity) or rapidly provisionable (within 4 hours) in a separately-managed cloud account. |
| URS-RAN-03 | H | R1 | Restored systems **shall** be scanned for malware / persistence indicators before re-introduction to production network. |
| URS-RAN-04 | H | R1 | The ransomware playbook **shall** be tabletop-exercised annually with InfoSec + IT + QA + Communications + Legal. |
| URS-RAN-05 | H | R1 | NIS2 Art. 23 incident reporting timelines **shall** be observed: early warning ≤ 24 h to competent authority (Traficom in FI for NIS2; BfArM / Fimea for GxP impact); incident notification ≤ 72 h; final report ≤ 1 month. |
| URS-RAN-06 | M | R2 | A ransomware-incident-rehearsal report **shall** be presented annually to senior management per NIS2 governance obligations. |
| URS-DR-01 | H | R1 | A documented DR runbook **shall** describe failover from Espoo to Tampere for representative Tier-1 applications; exercised annually (URS-TEST-03). |
| URS-DR-02 | H | R1 | RTO from declared disaster: ≤ 4 hours for Tier 1; ≤ 24 hours for Tier 2; ≤ 72 hours for Tier 3. |
| URS-DR-03 | M | R2 | Communication plan during DR **shall** identify: Incident Commander, communications lead, regulatory-affairs contact, QA representative, and senior-management escalation path. |

### 5.12 Monitoring and Alerting

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MON-01 | H | R1 | Job failure or repository-low-space alerts **shall** route to the on-call within ≤ 15 minutes of detection. |
| URS-MON-02 | H | R1 | Job-success-rate KPI ≥ 99% over a rolling 30-day window; below-target months **shall** trigger root-cause analysis and remediation. |
| URS-MON-03 | H | R1 | A backup-coverage daily reconciliation report **shall** compare backup-jobs ↔ GxP IT register; deviations alerted to GxP IT Infrastructure Lead. |
| URS-MON-04 | M | R2 | Storage-capacity forecasting **shall** project 90-day utilisation and raise warnings when forecast exceeds 80% of capacity. |
| URS-MON-05 | H | R1 | Critical incidents (silent-failure detection; immutability deletion attempt; integrity-check failure) **shall** route to SOC within ≤ 1 minute. |

### 5.13 Performance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | H | R1 | Backup windows **shall not** impact production application performance during business hours (verified per Tier-1 application during PQ). |
| URS-PERF-02 | M | R2 | Restore-throughput targets: ≥ 500 MB/s from primary disk repository; ≥ 100 MB/s from cloud Object-Lock tier; ≥ 80 MB/s from LTO-9 vault tape. |
| URS-PERF-03 | M | R2 | Deduplication ratio target ≥ 5:1 on the ExaGrid tier; reviewed quarterly. |

### 5.14 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Backup Operators and Administrators **shall** be trained in role-specific procedures recorded in LMS; retraining annually + on procedure change. |
| URS-TRN-02 | M | R2 | Tape Couriers **shall** be trained on chain-of-custody procedures; competency re-verified annually. |
| URS-PR-01 | H | R1 | Annual periodic review covering: backup-coverage audit against the GxP IT register; RPO / RTO compliance; restore-test outcomes; deviation summary; training records; NIS2 + ISO 27001 surveillance findings; signed by GxP IT Infrastructure Lead + Head of IT + Head of QA + CISO. |
| URS-PR-02 | M | R2 | Quarterly KPI review by GxP IT Infrastructure Lead with action items captured to closure. |

### 5.15 Cross-System Integration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-01 | H | R1 | Authentication and authorisation **shall** be sourced from AD per `QTZ-URS-AD-001` (or the local equivalent AD URS); shared service accounts forbidden. |
| URS-INT-02 | H | R1 | Audit events **shall** be forwarded to the SIEM (Splunk Enterprise Security) per URS-AUD-02. |
| URS-INT-03 | H | R1 | Restore tests + DR exercises **shall** be captured as eQMS quality records (per `TAL-URS-eQMS-001` or equivalent). |
| URS-INT-04 | H | R1 | Backup of AD itself (system-state) **shall** be covered by this system per cross-reference to `QTZ-URS-AD-001` URS-BAK-01..06. |
| URS-INT-05 | H | R1 | Every GxP application's URS that requires periodic backup demonstration **shall** reference this URS's restore-validation cadence as the implementing service. |

## 6. Acceptance Criteria

The system **shall** enter validated GxP use when CS, RA, IQ, OQ, PQ approved and executed (proportionate to Cat 3); PQ includes scheduled-job verification, monthly backup-system-level restore tests, quarterly per-Tier-1-application restore tests, annual DR exercise, cloud-tier Object-Lock immutability demonstration, LTO-9 tape WORM verification, ransomware-playbook tabletop, NIS2 incident-reporting dry-run, and demonstration of 3-2-1-1-0 across all GxP IT register entries. VSR approved by GxP IT Infrastructure Lead, Head of IT, Head of QA, CISO. RTM maps every URS to ≥ 1 approved test case in IQ / OQ / PQ.

### 6.1 Validation Deliverables Inventory

| Deliverable | Owner | Approver |
|---|---|---|
| FS — Functional Specification | IT Architect | GxP IT Infrastructure Lead |
| CS — Configuration Specification (jobs, retention, repos, Object Lock, tape rotation) | Backup Administrator | GxP IT Infrastructure Lead + InfoSec |
| RA — Risk Assessment (ICH Q9(R1) + ISO 27005, with NIS2 + GDPR overlays) | CSV Architect | Head of QA + CISO |
| IQ — Installation Qualification | Backup Administrator | Validation Engineer |
| OQ — Operational Qualification | Validation Engineer | Head of QA |
| PQ — Performance Qualification | Validation Engineer | Head of QA |
| VSR — Validation Summary Report | Validation Engineer | GxP IT Infrastructure Lead + Head of QA + CISO |
| RTM — Requirements Traceability Matrix | Validation Engineer | Head of QA |

## 7. Constraints

- Veeam patches under change control; major version upgrades rehearsed in pre-prod.
- Non-trivial scripting (e.g., custom Veeam PowerShell beyond schedule / job definitions) triggers Cat-5 assessment for that scripted component.
- No direct internet from Veeam servers (cloud-tier via approved gateway with explicit allow-list).
- Object-Lock retention windows cannot be shortened post-write; over-provisioning is therefore the safe failure mode.
- Tape couriers are required to be vetted and bonded; chain-of-custody forms retained ≥ 7 years.
- Cryptographic algorithms are limited to FIPS 140-2 Level 2 minimum; deprecated algorithms (RC4, DES, MD5, SHA-1 for signing) are prohibited.

## 8. Assumptions

- The GxP IT register `AUR-IT-GxP-REG-001` is accurate and maintained as the authoritative source of in-scope systems.
- AD (`QTZ-URS-AD-001` or local equivalent), SIEM (Splunk), monitoring (Prometheus / Loki / Grafana), and ticketing (ServiceNow) are validated and continuously operational.
- The cloud-tier provider's Object Lock in Compliance mode is honoured per AWS service contract.
- LTO-9 WORM cartridges from the approved supplier comply with the LTO Consortium WORM specification.
- The third-party Helsinki vault operator complies with the contracted physical-security + chain-of-custody obligations.
- Network bandwidth between Espoo, Tampere, and the AWS eu-north-1 region meets the backup window's throughput requirement.

## 9. References

**US — FDA + NIST:**
- 21 CFR Part 11 §§ .10(a/b/c/d/e), .50, .70, .100
- 21 CFR Part 211 § 211.68 (automatic equipment) + § 211.180 (records retention)
- 21 CFR Part 58 § 58.81 (equipment SOPs incl. backup) + § 58.195 (records retention)
- FDA Guidance on Data Integrity and Compliance with cGMP (2018)
- NIST SP 800-34 Rev. 1 — Contingency Planning Guide for Federal Information Systems
- NIST SP 800-209 — Security Guidelines for Storage Infrastructure
- NIST SP 800-53 Rev. 5 — CP (Contingency Planning) family

**EU + DACH + Nordics:**
- EU GMP Annex 11 §§ 4.8 (backup), 7 (data storage), 9 (audit trail), 12 (security)
- ICH E6(R3) — Good Clinical Practice (Step 4, adopted 6 January 2025) — record-retention obligations for backed-up clinical-system data
- NIS2 Directive (EU) 2022/2555 — Art. 21 (cybersecurity risk-management, incl. backup management + crisis management); Art. 23 (incident reporting)
- GDPR Reg. (EU) 2016/679 Arts. 32 (security of processing), 33 (breach notification)
- Traficom / NCSC-FI — competent authority for NIS2 in Finland
- Fimea — Finnish Medicines Agency (GxP authority for the Espoo / Tampere sites)
- BfArM (DE), Swissmedic (CH), AGES PharmMed (AT) — for DACH-product backups in scope
- BSI IT-Grundschutz Kompendium — CON.3 Datensicherungskonzept, OPS.1.2.4 Datenträgerarchivierung

**International / Industry:**
- ISPE GAMP 5 (2nd Edition, 2022) — Category 3 conventions
- ISPE GAMP Good Practice Guide: *IT Infrastructure Control and Compliance*
- ISPE GAMP Good Practice Guide: *Records and Data Integrity*
- PIC/S PI 041 — Good Practices for Data Management and Integrity
- ISO/IEC 27001:2022 — Annex A.5.30 (ICT readiness for business continuity), A.8.13 (information backup)
- ISO/IEC 27002:2022 — control 8.13 implementation
- ISO 22301:2019 — Business Continuity Management
- LTO Consortium — *LTO-9 + WORM specification*

**Vendor:**
- Veeam — *Backup & Replication 12.1 User Guide* + *Best Practices for Application-Aware Processing*
- AWS — *S3 Object Lock — Compliance vs Governance retention modes*
- ExaGrid — *Tiered Backup Storage Architecture*
- Microsoft — *VSS Best Practices for Backup Vendors*
- Oracle — *RMAN Backup and Recovery User's Guide*
- PostgreSQL — *Continuous Archiving and Point-in-Time Recovery*

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

