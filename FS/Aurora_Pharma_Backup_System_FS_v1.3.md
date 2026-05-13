---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; Wave 3 Chunk J expanded 2026-05-12 (T2 catch-up: per-URS-ID rows for all 93 URS IDs; 3-2-1-1-0 topology; S3 Object Lock Compliance; LTO-9 WORM vault; database-aware backups; restore-validation cadence per Annex 11 § 4.8 + § 7.2; ransomware playbook; NIS2 reporting)"
seed_corpus_basis:
  - "AUR-URS-BACKUP-001 v1.1 (parent URS, T2)"
  - "GAMP 5 (2nd ed., 2022) Cat 3 conventions for IT infrastructure"
  - "21 CFR Part 11 §§ .10, .50, .70, .100"
  - "EU GMP Annex 11 §§ 4.8 (backup), 7 (data storage), 9 (audit trail), 12 (security)"
  - "ISO/IEC 27001:2022 Annex A.5.30 + A.8.13"
  - "NIS2 Directive (EU) 2022/2555 Art. 21 + 23"
  - "ISPE GAMP GPG IT Infrastructure Control and Compliance"
parent_urs:
  document_number: AUR-URS-BACKUP-001
  version: 1.1
  file: ../../URS/_generated/final/Backup_System_for_GxP_Servers__Aurora_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Backup System for GxP Servers — Veeam Backup & Replication 12.1 + ExaGrid + AWS S3 Object Lock + LTO-9 Air-Gapped Vault

**Document Number:** AUR-FS-BACKUP-001
**Version:** 1.1
**Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** AUR-URS-BACKUP-001 v1.1
**Site:** Aurora Pharma OY, Espoo (primary) + Tampere (DR) + Helsinki (vault, third-party) *(fictional)*
**System Class:** GAMP Cat 3 — Non-Configured Product
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100; EU GMP Annex 11 §§ 4.8, 7, 9, 12; ISO/IEC 27001:2022 Annex A.5.30 + A.8.13; NIS2 Directive (EU) 2022/2555; ISPE GAMP GPG *IT Infrastructure Control and Compliance*

> **FS scope note (Cat 3).** Site-developed restore-test runbooks + monitoring jobs are validated alongside the platform; the commercial Veeam product is the Cat-3 platform. Custom PowerShell beyond schedule / job definitions would trigger Cat-5 assessment for the scripted component.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (IT Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Backup Operations) | _____________ | _____________ | _____ |
| Reviewer (InfoSec / CISO delegate) | _____________ | _____________ | _____ |
| Reviewer (DPO) | _____________ | _____________ | _____ |
| Approver (Head of IT Infrastructure) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |
| Approver (CISO) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue with range-compressed traceability. |
| 1.1 | 2026-05-12 | (synthetic) | Wave 3 Chunk J catch-up: per-ID rows for all 93 URS-IDs; corrected FS-ID naming to match URS-ID semantics; added 3-2-1-1-0 layered topology, S3 Object Lock Compliance, LTO-9 WORM vault, database-aware methods, restore-validation cadence, ransomware playbook, NIS2 reporting timelines. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies how the centralised backup system for GxP servers is deployed and configured to satisfy `AUR-URS-BACKUP-001` v1.1 — protecting GxP electronic records under 21 CFR Part 11, EU GMP Annex 11, ICH E6(R3), and Part 58 GLP through layered 3-2-1-1-0 backups with immutable cloud + air-gap tape tiers, periodic restore-test evidence per Annex 11 § 7.2 + § 4.8, and ransomware-resistant architecture aligned to NIS2 Art. 21 backup-management obligations.

## 2. Scope

Veeam Backup & Replication 12.1 active+DR pair (Espoo + Tampere); ExaGrid deduplicating disk repositories at both sites; AWS S3 Object Lock (Compliance mode) in eu-north-1 for immutable cloud tier; LTO-9 WORM tape rotation to third-party Helsinki vault; per-system backup policies for all GxP servers in scope of `AUR-IT-GxP-REG-001`; database-aware integrations (Oracle RMAN, MS SQL Server VSS, PostgreSQL pg_basebackup + WAL streaming); integration with Splunk Enterprise Security SIEM (job-status + alert forwarding), Prometheus / Loki / Grafana (operational metrics), and ServiceNow (ticketing); AD authentication via `QTZ-URS-AD-001`-equivalent; CyberArk-brokered admin sessions.

## 3. System Architecture

```
        ┌─────────────────────────────────────────────────────────┐
        │ GxP Server Estate (in AUR-IT-GxP-REG-001)              │
        │  LIMS, ELN, eQMS, EDMS, LMS, MES, SCADA, ePRO, PV, etc │
        └──────────────────────────┬──────────────────────────────┘
                                   │ Veeam Application-Aware
                                   │ (RMAN / VSS / pg_basebackup)
                                   ▼
                ┌─────────────────────────────────────┐
                │ Veeam B&R 12.1 Active (Espoo)       │◄────┐
                │   ↕ WAN replication                 │     │
                │ Veeam B&R 12.1 DR     (Tampere)     │     │
                └────┬─────────────────────┬──────────┘     │
                     │                     │                │
                     ▼                     ▼                │
              ┌──────────────┐      ┌──────────────┐        │
              │ ExaGrid disk │      │ ExaGrid disk │        │
              │  Espoo       │      │  Tampere     │        │
              └──────┬───────┘      └──────┬───────┘        │
                     │                     │                │
                     │  ┌──────────────────┘                │
                     ▼  ▼                                   │
              ┌──────────────────────┐    ┌─────────────────┴───┐
              │ AWS S3 Object Lock   │    │ LTO-9 WORM Vault     │
              │ Compliance mode      │    │ Helsinki (3rd party) │
              │ eu-north-1           │    │ monthly rotation     │
              └──────────────────────┘    └─────────────────────┘

         3-2-1-1-0:  3 copies (ExaGrid×2 + S3 + LTO)
                     2 media types (disk + cloud object + tape)
                     1 offsite (Tampere DR + Helsinki vault + AWS region)
                     1 immutable (S3 Object Lock + LTO WORM)
                     0 errors on last integrity scan

                     ↕ AD authentication + SIEM forwarding
```

## 4. Functional Specifications

Each row maps a URS-ID to its implementation. One row per URS-ID. No range compression.

### 4.1 Platform / Hardware (URS § 5.1)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | Veeam B&R 12.1 active server in Espoo (Windows Server 2022, 16 vCPU / 64 GB / 2 TB SSD scratch) + DR server in Tampere (identical sizing); Veeam replication group configured; failover documented in DR runbook `AUR-RUNBK-DR-001`. |
| FS-PLAT-02 | URS-PLAT-02 | Repositories: (a) ExaGrid EX84 Espoo (deduplicating disk, ~1.2 PB usable); (b) ExaGrid EX84 Tampere; (c) AWS S3 bucket `aurora-gxp-backup-immutable` in `eu-north-1` with Object Lock Compliance mode; (d) LTO-9 WORM tape library + monthly off-site rotation to Helsinki vault. |
| FS-PLAT-03 | URS-PLAT-03 | Sizing model: backup-window throughput ≥ 1.5× peak per region; repository headroom ≥ 30%; capacity-forecasting tool runs weekly. |
| FS-PLAT-04 | URS-PLAT-04 | Veeam admin VLAN `VL-BAK-MGMT`; egress to AWS via Direct Connect gateway with explicit allow-list (Veeam endpoints + S3 + KMS only); no internet egress from Veeam servers. |
| FS-PLAT-05 | URS-PLAT-05 | Hardware lifecycle: ExaGrid replaced on 7-year cycle; Veeam server hosts refreshed every 5 years; tape drives serviced per Quantum + LTO Consortium maintenance schedule. |

### 4.2 Coverage (URS § 5.2)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-COV-01 | URS-COV-01 | Integration with `AUR-IT-GxP-REG-001` register via nightly export; new register entries auto-create backup job in pending state; Application Owner notified via email; job activated within 7 calendar days. |
| FS-COV-02 | URS-COV-02 | Tier classification field on register; backup-job tier inherited; Tier 1 / 2 / 3 RPO+RTO matrix applied; tier reviewed annually as part of `AUR-URS-BACKUP-001` URS-PR-01 periodic review. |
| FS-COV-03 | URS-COV-03 | Veeam backup-job export schema (server, frequency, retention, repository, tier, owner) generated as PDF + CSV by scheduled report; available on-demand for inspectors. |
| FS-COV-04 | URS-COV-04 | Backup scope per system documented in job description: application data, configuration files, database, OS image, application binaries; deviations require change-control approval. |
| FS-COV-05 | URS-COV-05 | New-server onboarding workflow includes backup-job validation step; sign-off required before server enters GxP-active state in `AUR-IT-GxP-REG-001`. |

### 4.3 Backup Methods + Schedule (URS § 5.3)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-METH-01 | URS-METH-01 | Veeam Application-Aware Processing: Oracle RMAN integration for Oracle DBs (LIMS, ePRO); MS SQL Server VSS for SQL DBs (eQMS, EDMS, CMMS); PostgreSQL pg_basebackup + WAL streaming for PG DBs (PV DB, Stability). |
| FS-METH-02 | URS-METH-02 | Image-level VM backups via vSphere / Hyper-V snapshot integration; CBT (changed-block tracking) enabled; agent-based backups for non-virtual physical hosts (SCADA gateway, lab instruments with local storage). |
| FS-METH-03 | URS-METH-03 | Tier-1 transaction-log shipping: continuous archive logs replicated to ExaGrid + cloud; RPO ≤ 4 h achieved by log-shipping interval ≤ 15 min combined with hourly Veeam incrementals. |
| FS-SCH-01 | URS-SCH-01 | Schedule: Tier 1 daily incremental 22:00 + weekly synthetic full Sunday 00:00 + monthly archive 1st Sunday + continuous log shipping every 15 min; Tier 2 / 3 daily incremental + weekly synthetic full + monthly archive. |
| FS-SCH-02 | URS-SCH-02 | Retention: daily 30 d; weekly 12 m; monthly ≥ 7 y; long-term archive per app retention table (`AUR-RETENTION-TABLE-001`) — up to 25 y for clinical data (ICH E6(R3)) + up to 30 y for PV. |
| FS-SCH-03 | URS-SCH-03 | S3 Object Lock retention configured per app retention; Compliance mode prevents shortening; documented per bucket prefix; reviewed annually. |
| FS-SCH-04 | URS-SCH-04 | LTO-9 monthly: first Sunday tape set produced + shipped to Helsinki via dual-courier chain-of-custody; quarterly read-back verification at vault; minimum retention 7 y. |

### 4.4 RPO / RTO (URS § 5.4)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RPO-01 | URS-RPO-01 | RPO matrix: Tier 1 ≤ 4 h; Tier 2 ≤ 24 h; Tier 3 ≤ 72 h. Job schedules per FS-SCH-01 deliver these. |
| FS-RPO-02 | URS-RPO-02 | Cloud-tier RPO: Tier 1 ≤ 24 h (daily upload to S3); Tier 2 ≤ 7 d; Tier 3 ≤ 30 d. |
| FS-RPO-03 | URS-RPO-03 | Quarterly Grafana RPO compliance dashboard; deviations trigger job redesign or tier re-classification CR. |
| FS-RTO-01 | URS-RTO-01 | RTO targets enforced via runbook design + restore tests (FS-TEST-02). Tier 1 ≤ 4 BH; Tier 2 ≤ 24 BH; Tier 3 ≤ 72 BH. |
| FS-RTO-02 | URS-RTO-02 | RTO measurement: ServiceNow incident timestamps + application-restart confirmation; runbooks per Tier-1 app in `AUR-RUNBK-APP-*` series. |

### 4.5 Restore Testing — Annex 11 § 4.8 + § 7.2 (URS § 5.5)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TEST-01 | URS-TEST-01 | Backup-system-level monthly restore tests: integrity verification via Veeam SureBackup, backup mount, restore of representative file / VM from each tier (primary disk + DR disk + S3 + tape). Calendared task; misses raise deviation. |
| FS-TEST-02 | URS-TEST-02 | Application-level quarterly restore tests per Tier-1 app: database restore + application restart + functional verification; witnessed by app team; QA Reviewer signs off; evidence captured in eQMS as quality record. |
| FS-TEST-03 | URS-TEST-03 | Annual full DR exercise: failover Tier-1 representative from Espoo to Tampere using DR-site copies only; cloud-tier + tape-tier recovery exercised biennially. |
| FS-TEST-04 | URS-TEST-04 | Failed restore-test deviation auto-opens eQMS record; CAPA + remediation before next test cycle; deviation review by Head of QA. |
| FS-TEST-05 | URS-TEST-05 | Restore-test certificate schema: test ID, system, backup source, restore target, integrity-check result, sign-off identities + datetime; PDF + structured XML; retained 25 y in eQMS + immutable archive. |
| FS-TEST-06 | URS-TEST-06 | eQMS-side restore-test register supports filter / export / inspector view; data formatted per ALCOA+. |
| FS-TEST-07 | URS-TEST-07 | Unannounced restore-drill triennial: surprise day exercised by ops team without prior notice; outcome reported to senior management. |

### 4.6 3-2-1-1-0 + Immutable Backups (URS § 5.6)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-IMM-01 | URS-IMM-01 | Architecture enforces 3-2-1-1-0: 3 copies (ExaGrid Espoo + ExaGrid Tampere + S3 + LTO tape — for tier-1 data); 2 media types (disk + object + tape); 1 offsite (Tampere + Helsinki + AWS region); 1 immutable (S3 + LTO WORM); 0 integrity errors (validated weekly per FS-DI-05). |
| FS-IMM-02 | URS-IMM-02 | AWS S3 bucket configured with Object Lock in Compliance mode (not Governance); retention default-mode set per bucket prefix; no API path can shorten retention; AWS root account credentials sealed dual-custody. |
| FS-IMM-03 | URS-IMM-03 | LTO-9 WORM cartridges procured from approved supplier (LTO Consortium compliant); rewritable tape forbidden by procurement policy + verified at library load. |
| FS-IMM-04 | URS-IMM-04 | Object Lock retention duration set per app retention table; bucket-policy-as-code review annually; retention extension only — never shortening. |
| FS-IMM-05 | URS-IMM-05 | Quarterly immutability verification: deletion attempt simulated against each immutable repo; failure-mode confirmed; verification certificate signed + archived 25 y. |
| FS-IMM-06 | URS-IMM-06 | AWS Organisations cross-account isolation: Veeam writes to immutable bucket from a dedicated provisioning account; immutable-administration account is a separate identity boundary with break-glass dual-custody. |

### 4.7 Audit Trail + Records (URS § 5.7)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Veeam audit log captures: job runs (success/fail/skip), configuration changes, role/permission changes, restore operations, integrity-check results; forwarded to Splunk via syslog. |
| FS-AUD-02 | URS-AUD-02 | Splunk index `gxp_backup`: hot/warm 1 y + SmartStore cold 7 y on S3 Object Lock; gap-detection job; hash chain at index level. |
| FS-AUD-03 | URS-AUD-03 | Veeam → ServiceNow CR-link: every config change has CR-ID field; orphan change detected by nightly correlation job → HIGH alert to InfoSec. |
| FS-AUD-04 | URS-AUD-04 | Restore-test evidence retained ≥ 25 y in eQMS + immutable archive; pointer stored in Splunk for inspector cross-reference. |
| FS-AUD-05 | URS-AUD-05 | Audit-trail schema: UTC ms-precision, event ID, AD account, target object, operation, outcome, originating IP / host; normalised to CIM data model in Splunk Enterprise Security. |
| FS-AUD-06 | URS-AUD-06 | Nightly hash-chain validator on `gxp_backup` index; failure → CRITICAL alert + InfoSec investigation. |

### 4.8 21 CFR Part 11 / Annex 11 Sub-Section Alignment (URS § 5.8)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Procedures + controls: this FS + AUR-SOP-BACKUP-* SOPs + restore-validation SOP implement § 11.10(a). |
| FS-PART11-02 | URS-PART11-02 | Restored records exportable in human-readable PDF + electronic CSV / JSON via Veeam restore + downstream-app export tools (§ 11.10(b)). |
| FS-PART11-03 | URS-PART11-03 | Retention protection: S3 Object Lock + LTO WORM + hash chain → § 11.10(c). |
| FS-PART11-04 | URS-PART11-04 | Access limited per FS-SEC-01..08 (AD-mapped roles + MFA); audit-trail captures access events → § 11.10(d). |
| FS-PART11-05 | URS-PART11-05 | Audit trail operational, time-stamped, append-only → § 11.10(e). FS-AUD-01..06. |
| FS-PART11-06 | URS-PART11-06 | Restore-test sign-off via eQMS e-signature: printed name + datetime + meaning (passed / failed / accepted-with-dev) → § 11.50. |
| FS-PART11-07 | URS-PART11-07 | Restore-test signature cryptographically linked to test record (signed PDF + hash chain) → § 11.70. |
| FS-PART11-08 | URS-PART11-08 | Unique signer identity sourced from AD substrate (QTZ-FS-AD-001 FS-PART11-09) → § 11.100. |
| FS-AN11-01 | URS-AN11-01 | Annex 11 § 4.8 backup processes defined; verified per FS-TEST-01..07. |
| FS-AN11-02 | URS-AN11-02 | Annex 11 § 7.2 backup integrity + restore ability demonstrated per FS-TEST-01..04. |
| FS-AN11-03 | URS-AN11-03 | Annex 11 § 9 audit trail → FS-AUD-*. |
| FS-AN11-04 | URS-AN11-04 | Annex 11 § 12 physical + logical security → FS-SEC-*. |

### 4.9 Data Integrity / ALCOA+ (URS § 5.9)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | Veeam logs Operator identity per action; events normalised + indexed in Splunk against CIM Auth schema. |
| FS-DI-02 | URS-DI-02 | Veeam audit + restore-test logs exportable as CSV / PDF / JSON via scheduled reports. |
| FS-DI-03 | URS-DI-03 | Veeam server clocks synced to authoritative NTP pool (multiple stratum-2 sources); drift alerted; backup metadata contemporaneous with action. |
| FS-DI-04 | URS-DI-04 | Veeam backup operations are read-only on source via VSS / RMAN / pg_basebackup snapshot semantics; source-data integrity preserved. |
| FS-DI-05 | URS-DI-05 | Veeam SureBackup + ExaGrid block-level checksum + S3 ETag + LTO logical-block-protection together provide integrity verification on every backup; weekly automated repository rescans; nightly hash-chain validation. |
| FS-DI-06 | URS-DI-06 | Immutable cloud-tier + LTO WORM together deliver Enduring + Available + Consistent against ransomware + insider threats. |

### 4.10 Security + Encryption (URS § 5.10)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SEC-01 | URS-SEC-01 | Veeam authenticates against AD via Kerberos / LDAPS; AD groups `BAK_ADMIN`, `BAK_OPERATOR`, `BAK_AUDITOR` map to Veeam roles. Two break-glass local accounts vaulted in CyberArk + dual-custody safes. |
| FS-SEC-02 | URS-SEC-02 | Backup network traffic: TLS 1.3 preferred / 1.2 minimum; at-rest encryption AES-256 on ExaGrid; S3 SSE-KMS with customer-managed key (annual rotation); LTO drive encryption enabled. |
| FS-SEC-03 | URS-SEC-03 | Object Lock Compliance mode prevents in-window deletion; API attempts logged + alerted; CloudTrail forwarded to Splunk. |
| FS-SEC-04 | URS-SEC-04 | Tenable Nessus monthly scan on Veeam servers + ExaGrid + cloud-tier endpoint; critical → 30 d; high → 60 d remediation SLA. |
| FS-SEC-05 | URS-SEC-05 | Backup-administrator accounts require FIDO2 MFA at AD/Entra ID layer (per QTZ-FS-AD-001 FS-AUTHN-02). |
| FS-SEC-06 | URS-SEC-06 | Veeam vendor support: CyberArk PSM-brokered session; no standing vendor account; full session recording. |
| FS-SEC-07 | URS-SEC-07 | AWS KMS customer-managed key + HSM (CloudHSM Cluster); annual rotation; key-escrow procedure tested annually; offline copy of master-encryption-key sealed dual-custody. |
| FS-SEC-08 | URS-SEC-08 | Network segmentation: Veeam admin plane on `VL-BAK-MGMT`; data-mover plane on `VL-BAK-DATA`; firewall rules in `AUR-FW-BAK-001` reviewed quarterly. |

### 4.11 Ransomware + DR (URS § 5.11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RAN-01 | URS-RAN-01 | Ransomware playbook `AUR-RUNBK-RANSOMWARE-001`: isolation steps; clean-room restore environment; restore from S3 + tape; malware scan; forensic preservation of compromised images. |
| FS-RAN-02 | URS-RAN-02 | Clean-room restore infrastructure: dedicated AWS organisation account with pre-templated network + security baseline; 4-h provisioning SLA. |
| FS-RAN-03 | URS-RAN-03 | Restored systems scanned with Defender for Endpoint + Falcon (dual-vendor scan) before re-introduction; quarantine VLAN for inspection. |
| FS-RAN-04 | URS-RAN-04 | Annual tabletop with InfoSec + IT + QA + Communications + Legal + senior business stakeholder; lessons-learned → CAPA in eQMS. |
| FS-RAN-05 | URS-RAN-05 | NIS2 Art. 23 notification timeline: 24-h early warning to Traficom (FI competent authority); 72-h incident notification; 1-month final report; Fimea notified for GxP impact; templates pre-approved by legal + DPO. |
| FS-RAN-06 | URS-RAN-06 | Annual ransomware-rehearsal report to Executive Committee per NIS2 senior-management accountability obligation. |
| FS-DR-01 | URS-DR-01 | DR runbook `AUR-RUNBK-DR-001`: Espoo → Tampere failover for Tier-1 reps; annual exercise (FS-TEST-03). |
| FS-DR-02 | URS-DR-02 | RTO matrix encoded in DR runbook: Tier 1 ≤ 4 h; Tier 2 ≤ 24 h; Tier 3 ≤ 72 h. |
| FS-DR-03 | URS-DR-03 | Incident-Communication plan in `AUR-PLAN-IC-001`: Incident Commander, Comms lead, Reg-Affairs contact, QA rep, exec escalation; pre-approved templates per stakeholder. |

### 4.12 Monitoring (URS § 5.12)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MON-01 | URS-MON-01 | Veeam alarms + Prometheus exporters → Alertmanager → PagerDuty on-call ≤ 15 min for job-failure / low-space. |
| FS-MON-02 | URS-MON-02 | Splunk rolling-30-d success-rate KPI dashboard; < 99% → ServiceNow ticket + RCA workflow. |
| FS-MON-03 | URS-MON-03 | Daily reconciliation job compares Veeam protected-objects vs `AUR-IT-GxP-REG-001`; deviations alerted to GxP IT Infrastructure Lead. |
| FS-MON-04 | URS-MON-04 | Capacity-forecasting job (Prometheus + custom predictor) projects 90-d ExaGrid + S3 utilisation; > 80% → warning. |
| FS-MON-05 | URS-MON-05 | Critical incident detection: silent-failure heuristic + immutability deletion attempt + integrity-check failure → SOC ≤ 1 min via PagerDuty. |

### 4.13 Performance (URS § 5.13)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | Veeam backup window scheduled outside production peak hours (22:00 – 06:00 site time); PQ verifies no production impact during business hours. |
| FS-PERF-02 | URS-PERF-02 | Restore throughput targets: ExaGrid disk ≥ 500 MB/s; S3 Object-Lock ≥ 100 MB/s; LTO-9 ≥ 80 MB/s; measured quarterly. |
| FS-PERF-03 | URS-PERF-03 | ExaGrid deduplication ratio dashboard target ≥ 5:1; reviewed quarterly; trend tracked. |

### 4.14 Training + Periodic Review (URS § 5.14)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | LMS-tracked training for Backup Operator + Backup Administrator + Veeam vendor patches; annual retraining + procedure-change retraining. |
| FS-TRN-02 | URS-TRN-02 | Tape-courier training (chain-of-custody, handling, tamper-evident packaging); competency re-verified annually with practical drill. |
| FS-PR-01 | URS-PR-01 | Annual periodic review: coverage audit vs `AUR-IT-GxP-REG-001`; RPO / RTO compliance; restore-test outcomes; deviation summary; training records; NIS2 + ISO 27001 surveillance findings; signed by GxP IT Infrastructure Lead + Head of IT + Head of QA + CISO. |
| FS-PR-02 | URS-PR-02 | Quarterly KPI review by GxP IT Infrastructure Lead; ServiceNow action-items tracked to closure. |

### 4.15 Cross-System Integration (URS § 5.15)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-01 | URS-INT-01 | AD authentication per `QTZ-URS-AD-001` (or local equivalent AD URS); no shared service accounts; service accounts via gMSA / CyberArk-vault. |
| FS-INT-02 | URS-INT-02 | Splunk Enterprise Security ingestion per FS-AUD-02. |
| FS-INT-03 | URS-INT-03 | eQMS (e.g., `TAL-URS-eQMS-001` or local equivalent) hosts restore-test + DR-exercise quality records via Veeam → eQMS REST integration. |
| FS-INT-04 | URS-INT-04 | AD system-state backup covered by this service per cross-reference to QTZ-URS-AD-001 URS-BAK-01..06; backup-job tagged `tier1-identity`. |
| FS-INT-05 | URS-INT-05 | Every GxP-application FS that requires periodic backup demonstration references this FS's restore-validation cadence; cross-reference maintained in `AUR-XREF-GxP-001`. |

## 5. Non-Functional Specifications

| NFR ID | Specification |
|---|---|
| NFR-01 | Tier 1 RPO ≤ 4 h (continuous log shipping) |
| NFR-02 | Tier 1 RTO ≤ 4 BH |
| NFR-03 | Object Lock retention ≥ regulatory-window per app |
| NFR-04 | LTO-9 retention ≥ 7 y; quarterly read-back |
| NFR-05 | Restore-test certificate retention ≥ 25 y |
| NFR-06 | Backup-success rate ≥ 99% rolling 30 d |
| NFR-07 | Audit-forward latency ≤ 5 min Veeam → Splunk |
| NFR-08 | NIS2 notification ≤ 24 h / ≤ 72 h / ≤ 1 month |
| NFR-09 | Encryption: AES-256 at rest + TLS 1.2/1.3 in transit |
| NFR-10 | Vulnerability remediation: critical ≤ 30 d; high ≤ 60 d |

## 6. Configuration Items (CI)

| CI ID | Item | Configured Value |
|---|---|---|
| CI-01 | Tier-1 RPO target | ≤ 4 h |
| CI-02 | Tier-1 RTO target | ≤ 4 BH |
| CI-03 | Object-Lock retention default | per app retention table |
| CI-04 | Object-Lock mode | Compliance |
| CI-05 | LTO media | LTO-9 WORM cartridges only |
| CI-06 | Backup-job restore-test cadence | monthly system-level + quarterly app-level + annual DR |
| CI-07 | Splunk `gxp_backup` retention | 1 y online + 7 y SmartStore cold |
| CI-08 | Backup-success KPI target | ≥ 99% rolling 30 d |
| CI-09 | AWS region | eu-north-1 |
| CI-10 | NIS2 competent authority | Traficom (FI) |
| CI-11 | GxP authority for site | Fimea (FI) |
| CI-12 | Backup window | 22:00 – 06:00 site time |
| CI-13 | gMSA + CyberArk-vault password policy | per AD FS |
| CI-14 | 3-2-1-1-0 verification cadence | quarterly + 0-errors on weekly integrity scan |
| CI-15 | Restore-test certificate retention | 25 y |

## 7. Risks (FS-level)

| Risk | Mitigation |
|---|---|
| Silent backup-job failure | FS-AUD-01..06 + FS-MON-01 + FS-MON-05 |
| Object-Lock misconfiguration (Governance instead of Compliance) | FS-IMM-02 + quarterly verification FS-IMM-05 |
| Restore-test gap | FS-TEST-01..07 cadence + deviation workflow |
| Audit tampering | FS-AUD-02 hash chain + FS-AUD-06 nightly validator |
| Ransomware attack on production + Veeam | FS-IMM-01..06 + FS-RAN-01..06 |
| Tape loss / theft in transit | FS-SEC-02 encryption + dual-courier chain-of-custody + FS-TRN-02 |
| Encryption-key loss | FS-SEC-07 HSM + escrow + annual restore test |
| NIS2 notification miss | FS-RAN-05 pre-approved templates + tabletop |
| Cloud-tier region outage | FS-PLAT-02 multi-tier + FS-DR-01..03 |
| GDPR Art. 33 breach-notification miss | FS-RAN-05 DPO coordination |

## 8. References

- AUR-URS-BACKUP-001 v1.1 (parent URS, T2)
- 21 CFR Part 11 §§ .10, .50, .70, .100
- 21 CFR Part 211 § 211.68 + § 211.180
- 21 CFR Part 58 § 58.81 + § 58.195
- EU GMP Annex 11 §§ 4.8, 7, 9, 12
- ICH E6(R3) — GCP (Step 4, adopted 6 January 2025) record retention
- ISPE GAMP 5 (2nd Edition, 2022)
- ISPE GAMP Good Practice Guide: *IT Infrastructure Control and Compliance*
- ISPE GAMP Good Practice Guide: *Records and Data Integrity*
- PIC/S PI 041
- ISO/IEC 27001:2022 Annex A.5.30 (ICT readiness for business continuity), A.8.13 (information backup)
- NIST SP 800-34 Rev. 1 — Contingency Planning Guide
- NIST SP 800-209 — Storage Infrastructure Security
- NIS2 Directive (EU) 2022/2555 Arts. 21, 23
- GDPR Reg. (EU) 2016/679 Arts. 32, 33
- Traficom — NIS2 competent authority (FI)
- Fimea — Finnish Medicines Agency
- BSI IT-Grundschutz CON.3 Datensicherungskonzept
- Veeam — *Backup & Replication 12.1 User Guide* + *Application-Aware Best Practices*
- AWS — *S3 Object Lock — Compliance vs Governance retention modes*
- LTO Consortium — *LTO-9 + WORM specification*
- ExaGrid — *Tiered Backup Storage Architecture*

## 9. Appendix A — URS → FS Traceability Matrix

One row per URS-ID. No range compression.

| URS ID | FS ID(s) |
|---|---|
| URS-PLAT-01 | FS-PLAT-01 |
| URS-PLAT-02 | FS-PLAT-02 |
| URS-PLAT-03 | FS-PLAT-03 |
| URS-PLAT-04 | FS-PLAT-04 |
| URS-PLAT-05 | FS-PLAT-05 |
| URS-COV-01 | FS-COV-01 |
| URS-COV-02 | FS-COV-02 |
| URS-COV-03 | FS-COV-03 |
| URS-COV-04 | FS-COV-04 |
| URS-COV-05 | FS-COV-05 |
| URS-METH-01 | FS-METH-01 |
| URS-METH-02 | FS-METH-02 |
| URS-METH-03 | FS-METH-03 |
| URS-SCH-01 | FS-SCH-01 |
| URS-SCH-02 | FS-SCH-02 |
| URS-SCH-03 | FS-SCH-03 |
| URS-SCH-04 | FS-SCH-04 |
| URS-RPO-01 | FS-RPO-01 |
| URS-RPO-02 | FS-RPO-02 |
| URS-RPO-03 | FS-RPO-03 |
| URS-RTO-01 | FS-RTO-01 |
| URS-RTO-02 | FS-RTO-02 |
| URS-TEST-01 | FS-TEST-01 |
| URS-TEST-02 | FS-TEST-02 |
| URS-TEST-03 | FS-TEST-03 |
| URS-TEST-04 | FS-TEST-04 |
| URS-TEST-05 | FS-TEST-05 |
| URS-TEST-06 | FS-TEST-06 |
| URS-TEST-07 | FS-TEST-07 |
| URS-IMM-01 | FS-IMM-01 |
| URS-IMM-02 | FS-IMM-02 |
| URS-IMM-03 | FS-IMM-03 |
| URS-IMM-04 | FS-IMM-04 |
| URS-IMM-05 | FS-IMM-05 |
| URS-IMM-06 | FS-IMM-06 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
| URS-AUD-05 | FS-AUD-05 |
| URS-AUD-06 | FS-AUD-06 |
| URS-PART11-01 | FS-PART11-01 |
| URS-PART11-02 | FS-PART11-02 |
| URS-PART11-03 | FS-PART11-03 |
| URS-PART11-04 | FS-PART11-04 |
| URS-PART11-05 | FS-PART11-05 |
| URS-PART11-06 | FS-PART11-06 |
| URS-PART11-07 | FS-PART11-07 |
| URS-PART11-08 | FS-PART11-08 |
| URS-AN11-01 | FS-AN11-01 |
| URS-AN11-02 | FS-AN11-02 |
| URS-AN11-03 | FS-AN11-03 |
| URS-AN11-04 | FS-AN11-04 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-SEC-05 | FS-SEC-05 |
| URS-SEC-06 | FS-SEC-06 |
| URS-SEC-07 | FS-SEC-07 |
| URS-SEC-08 | FS-SEC-08 |
| URS-RAN-01 | FS-RAN-01 |
| URS-RAN-02 | FS-RAN-02 |
| URS-RAN-03 | FS-RAN-03 |
| URS-RAN-04 | FS-RAN-04 |
| URS-RAN-05 | FS-RAN-05 |
| URS-RAN-06 | FS-RAN-06 |
| URS-DR-01 | FS-DR-01 |
| URS-DR-02 | FS-DR-02 |
| URS-DR-03 | FS-DR-03 |
| URS-MON-01 | FS-MON-01 |
| URS-MON-02 | FS-MON-02 |
| URS-MON-03 | FS-MON-03 |
| URS-MON-04 | FS-MON-04 |
| URS-MON-05 | FS-MON-05 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-PERF-03 | FS-PERF-03 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-PR-02 | FS-PR-02 |
| URS-INT-01 | FS-INT-01 |
| URS-INT-02 | FS-INT-02 |
| URS-INT-03 | FS-INT-03 |
| URS-INT-04 | FS-INT-04 |
| URS-INT-05 | FS-INT-05 |

## 10. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

The following risks are noted for downstream evaluation in the Risk Assessment.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-BAK-01 | A Tier-1 GxP server omitted from a backup job | Medium | High | URS-COV-01 + URS-MON-03 |
| R-BAK-02 | Silent backup-job failure undetected | Medium | High | URS-MON-01 + URS-MON-05 + URS-AUD-01 |
| R-BAK-03 | Unverifiable / failed restore at point-of-need | Medium | High | URS-TEST-01..07 |
| R-BAK-04 | Ransomware compromising production + online backups | Medium | Critical | URS-IMM-01..06 + URS-RAN-01..06 |
| R-BAK-05 | Admin abuse of retention-deletion | Low | High | URS-SEC-03 (Object Lock Compliance) + URS-SEC-05 (MFA) + URS-IMM-06 (cross-account isolation) |
| R-BAK-06 | NIS2 incident-reporting timeline missed (24 h / 72 h / 1 month) | Low | High | URS-RAN-05 + URS-PR-01 |
| R-BAK-07 | Tape loss / theft during courier transit | Low | High | URS-SEC-02 (encryption) + courier chain-of-custody + URS-TRN-02 |
| R-BAK-08 | Object-Lock retention misconfiguration (Governance instead of Compliance mode) | Low | Critical | URS-IMM-02 + URS-IMM-05 quarterly verification |
| R-BAK-09 | Backup integrity-check failure not detected | Low | High | URS-DI-05 + URS-AUD-06 + URS-MON-05 |
| R-BAK-10 | Cloud-tier outage (regional) | Low | Medium | URS-PLAT-02 (multi-tier) + URS-DR-01..03 |
| R-BAK-11 | GDPR Art. 32 / Art. 33 — backup compromise involving personal data not reported within 72 h | Low | High | URS-RAN-05 + DPO coordination |
| R-BAK-12 | Encryption-key loss preventing restore | Very Low | Critical | URS-SEC-07 (HSM + escrow) + annual test |

Full evaluation in `AUR-RA-BACKUP-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
