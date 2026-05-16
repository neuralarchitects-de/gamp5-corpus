---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "AUR-FS-BACKUP-001 v1.1 (parent FS)"
  - "AUR-URS-BACKUP-001 v1.1 (informational)"
  - "GAMP 5 (2nd ed., 2022) — Cat 1 Infrastructure Design Specification"
  - "Veeam Backup & Replication 12.1 + ExaGrid + AWS S3 Object Lock Compliance + LTO-9 Air-Gapped Vault"
  - "EU GMP Annex 11 §§ 4.8 + 7 + 9 + 12; ISO/IEC 27001:2022 Annex A.5.30 + A.8.13"
parent_fs:
  document_number: AUR-FS-BACKUP-001
  version: 1.1
  file: ../../../FS_FDS/_generated/final/Aurora_Pharma_Backup_System_FS_v1.3.md
parent_urs:
  document_number: AUR-URS-BACKUP-001
  version: 1.1
  file: ../../../URS/_generated/final/Backup_System_for_GxP_Servers__Aurora_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Infrastructure Design Specification (IDS)

## Backup System for GxP Servers — Veeam Backup & Replication 12.1 + ExaGrid + AWS S3 Object Lock + LTO-9 Air-Gapped Vault

**Document Number:** AUR-DS-BACKUP-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** AUR-FS-BACKUP-001 v1.1 | **Parent URS:** AUR-URS-BACKUP-001 v1.1
**Site:** Aurora Pharma OY, Espoo (primary) + Tampere (DR) + Helsinki (vault, third-party) *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 1 — Infrastructure. **Treatment note:** the parent FS classifies this system as Category 3 (Non-Configured Product — commercial Veeam). Per the assignment prompt's Cat 1 / T2 / IDS designation, this DS is shaped per § 2B.7 (Cat 1 Infrastructure Design Specification — Network Topology + IP Plan; Identity + Authentication Design; NTP; Backup + Storage Tier Design; Hardening Baseline) rather than § 2B.6 (Cat 3 Vendor-Design-Reliance Statement). Both shapes are legitimate for an enterprise backup platform depending on site classification convention; Aurora uses Cat 1 (infrastructure-qualified) per this DS.
**Project Mode:** Greenfield deployment of 3-2-1-1-0 backup topology (3 copies, 2 different media, 1 off-site, 1 air-gap, 0 errors) replacing legacy single-copy nightly tape (per parent URS Project Mode line)
**Tier (inherited from parent URS+FS):** T2
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100; **EU GMP Annex 11 §§ 4.8 (backup), 7 (data storage), 9 (audit trail), 12 (security)**; ISO/IEC 27001:2022 Annex A.5.30 + A.8.13; **NIS2 Directive (EU) 2022/2555 (important entity)**; ISPE GAMP GPG *IT Infrastructure Control and Compliance*; CIS Microsoft Windows Server 2022 Benchmark; CIS Linux Benchmark; BSI IT-Grundschutz CON.6 (Data backup); NIST SP 800-53 r5 (CP-9 Contingency Backup); ENISA Threat Landscape for Ransomware (2024).

> **DS scope note (Cat 1 IDS).** Site-developed restore-test runbooks + monitoring jobs are validated alongside the platform as Cat-1 infrastructure components. The commercial Veeam product is the Cat-3 platform underneath; custom PowerShell beyond schedule / job definitions would trigger Cat-5 assessment for the scripted component.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect — Backup + DR) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Security Architect — Storage) | _____________ | _____________ | _____ |
| Reviewer (Network Architect) | _____________ | _____________ | _____ |
| Reviewer (Database Administration — Oracle + Postgres + SQL Server) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Third-Party Vault Operator Liaison — Helsinki) | _____________ | _____________ | _____ |
| Approver (CISO) | _____________ | _____________ | _____ |
| Approver (VP IT Compliance) | _____________ | _____________ | _____ |
| Approver (System Owner — Head of Backup + Storage Operations) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue. Inherited Tier T2 from parent URS+FS pair. Derived from AUR-FS-BACKUP-001 v1.1. DS covers 88/93 FS-IDs as DS-IDs through topology + per-CI rollup; 5 FS-IDs subsumed under category-level rollup rows. Infrastructure qualification cited by reference (`AUR-IQ-BACKUP-001`, `AUR-IQ-EXAGRID-001`, `AUR-IQ-S3-001`, `AUR-IQ-LTO9-001`); no IQ/OQ/PQ test rows per § 2B.7. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from AUR-URS-BACKUP-001 v1.1 and AUR-FS-BACKUP-001 v1.1. Additional DS-specific terms:

| Term | Definition |
|---|---|
| IDS | Infrastructure Design Specification (this document) |
| 3-2-1-1-0 | Industry-standard backup topology: 3 copies, 2 different media, 1 off-site, 1 air-gap, 0 errors on restore test |
| Veeam B&R | Veeam Backup & Replication 12.1 |
| ExaGrid | ExaGrid EX-series disk-based backup appliance with deduplication |
| Object Lock Compliance mode | AWS S3 immutability — neither user nor root can delete or shorten retention |
| Glacier Vault Lock | AWS Glacier WORM with vault-policy-bound retention |
| LTO-9 | Linear Tape-Open generation 9 (18 TB native, 45 TB compressed) |
| Air-gap vault | Physically-isolated off-line tape vault at Helsinki third-party site |
| WORM | Write-Once-Read-Many media or storage mode |
| Application-Aware | Veeam Application-Aware Processing — quiescing of databases via VSS / native scripts for crash-consistent backup |
| RPO | Recovery Point Objective |
| RTO | Recovery Time Objective |
| BH | Business Hours |
| NBU | NetBackup (legacy decommission system) |
| RBAC | Role-Based Access Control |

## 1. Purpose

This IDS records the technical infrastructure design of the Aurora Pharma GxP-server backup system: 3-2-1-1-0 topology spanning Espoo primary + Tampere DR + Helsinki air-gap vault; Veeam B&R 12.1 control plane; ExaGrid disk-based backup target with deduplication; AWS S3 Object Lock Compliance mode for immutable cloud copy; LTO-9 air-gapped vault for paper-of-last-resort; database-aware backups for Oracle / Postgres / SQL Server; monthly QA-witnessed restore-validation; ransomware playbook; NIS2-aligned incident reporting. The IDS is the input to `AUR-IQ-BACKUP-001` (infrastructure qualification) and to the cross-system XSYS-BAK interfaces consumed by Sirius PV, Theia MDR, Lyrae, Hydra, Tessera, Helios, Quartz AD, and all other GxP systems. Per § 2B.7(6): no IQ/OQ/PQ for the infrastructure itself in this DS — infrastructure qualification is cited by reference only.

## 2. Scope

**In scope.** Veeam B&R 12.1 control plane (primary + DR + cloud); ExaGrid EX-series backup repositories; AWS S3 Object Lock Compliance + Glacier Vault Lock cloud copy; LTO-9 air-gapped vault at Helsinki third-party site; backup proxies; backup-network design; database-aware processing for Oracle / Postgres / SQL Server / MongoDB; backup-schedule design (T1 / T2 / T3 tiers per parent URS); restore-test cadence; ransomware playbook; NIS2 incident-reporting playbook; cross-system XSYS-BAK adapter design for consumer GxP systems; SIEM forwarding; hardening baseline.

**Out of scope.** Veeam internal kernel design (Veeam SDLC); ExaGrid firmware (ExaGrid SDLC); AWS S3 control-plane internals (AWS SDLC); LTO-9 tape-drive firmware (vendor); third-party Helsinki vault facility internal operations.

## 3. Architectural Overview

```
   ┌─ Espoo (primary site) ────────────────────────────────────────┐
   │                                                               │
   │   ┌────────────────────────┐                                  │
   │   │ Veeam B&R 12.1 Mgmt    │  (Windows Server 2022)           │
   │   │  + Enterprise Manager  │  CIS L1 + BSI IT-Grundschutz     │
   │   └────────┬───────────────┘                                  │
   │            │                                                   │
   │   ┌────────▼───────────────┐                                  │
   │   │ Veeam Proxies (3×)     │  Linux + Windows hybrid          │
   │   └────────┬───────────────┘                                  │
   │            │                                                   │
   │   ┌────────▼───────────────┐                                  │
   │   │ ExaGrid EX84 (primary  │  Backup repository (~1 PiB)     │
   │   │  backup target)        │  deduplication + landing-zone   │
   │   └────────┬───────────────┘                                  │
   │            │                                                   │
   │            ├──► WAN replication to Tampere ExaGrid (DR)       │
   │            │                                                   │
   │            └──► S3 Object Lock copy via Direct Connect        │
   │                                                                │
   └───────────────┬───────────────────────────────────────────────┘
                   │
   ┌───────────────▼───────────────────────────────────────┐
   │ Tampere (DR site, ~250 km from Espoo)                 │
   │                                                       │
   │   ExaGrid EX84 (DR replica) ◄── Veeam replication     │
   │   Veeam B&R DR-Mgmt (cold-standby)                    │
   │   Quarterly partial-restore drill target              │
   │                                                       │
   └───────────────┬───────────────────────────────────────┘
                   │
   ┌───────────────▼───────────────────────────────────────┐
   │ Helsinki (3rd-party air-gap vault)                    │
   │                                                       │
   │   LTO-9 tape vault (monthly rotation in + quarterly  │
   │   rotation out)                                       │
   │   Tape catalog mirrored from Espoo                    │
   │   Physical-security + dual-control access            │
   │                                                       │
   └───────────────────────────────────────────────────────┘

   ┌─ AWS (eu-north-1 — Stockholm) ─────────────────────────┐
   │   S3 Object Lock Compliance mode (geo-replicated to    │
   │   eu-central-1 — Frankfurt)                            │
   │   Glacier Vault Lock for ≥ 25-year retention           │
   │   Encryption-at-rest AES-256 + SSE-KMS                 │
   │   Customer-managed KMS keys in HashiCorp Vault         │
   └───────────────────────────────────────────────────────┘
```

## 4. Network Topology + IP Plan

| DS-ID | VLAN ID | Subnet | Purpose | Site | FS-IDs traced |
|---|---|---|---|---|---|
| DS-NET-01 | VLAN 500 | 10.50.0.0/24 | Veeam management + Enterprise Manager | Espoo | FS-PLAT-01 |
| DS-NET-02 | VLAN 501 | 10.50.1.0/24 | Veeam proxies | Espoo | FS-PLAT-02 |
| DS-NET-03 | VLAN 502 | 10.50.2.0/24 | ExaGrid management + data network | Espoo | FS-PLAT-03 |
| DS-NET-04 | VLAN 510 | 10.51.0.0/24 | Veeam DR management + ExaGrid DR | Tampere | FS-PLAT-04 |
| DS-NET-05 | VLAN 520 | 10.52.0.0/24 | LTO-9 tape library + catalog manager (third-party vault Helsinki) | Helsinki | FS-PLAT-05 |
| DS-NET-06 | (cloud) | AWS VPC `aurora-backup-vpc` 172.16.0.0/16 | S3 Object Lock + Glacier Vault Lock | AWS | FS-IMM-01..06 |
| DS-NET-07 | — | Direct Connect 10 Gbit + IPSec backup | Espoo ↔ AWS (eu-north-1 / eu-central-1) | — | FS-IMM-03, FS-IMM-04 |
| DS-NET-08 | — | MPLS 10 Gbit | Espoo ↔ Tampere | — | FS-PLAT-04 |
| DS-NET-09 | — | Physical courier with chain-of-custody | Espoo ↔ Helsinki (tape rotation) | — | FS-PLAT-05 |

Firewall posture: `default-deny` at all VLAN boundaries; named allow rules per FS-SEC-* / FS-METH-*. Backup-network isolation from production network — explicit allow rules per backup-source system on VBM (Veeam Backup Manager) + Veeam Proxy paths.

## 5. Identity + Authentication Design

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-IDENT-01 | Veeam authentication | Microsoft Entra ID (Quartz AD federation per FS-XSYS-AD equivalent) — SAML 2.0 + FIDO2 MFA for `backup-admin` group | FS-SEC-01, FS-SEC-02 |
| DS-IDENT-02 | RBAC roles | `backup-admin` (full), `backup-operator` (run jobs, no policy edits), `restore-operator` (run restores, witness QA), `auditor-readonly`, `dba-restore` (per-database restore only) | FS-SEC-03, FS-SEC-04 |
| DS-IDENT-03 | SoD | Policy editor ≠ job executor; restore executor ≠ approver | FS-SEC-05 |
| DS-IDENT-04 | Service-account identity | gMSA per Veeam component; Veeam-VSS service for Application-Aware processing | FS-SEC-06 |
| DS-IDENT-05 | Vault for AWS + KMS credentials | HashiCorp Vault per FS-SEC-07; rotation 90 d | FS-SEC-07 |
| DS-IDENT-06 | Catalog database identity | gMSA + LDAPS to Veeam Catalog Service | FS-SEC-08 |
| DS-IDENT-07 | Break-glass account | 1 emergency Veeam admin account; password rotated 24-h after each use; SIEM-monitored | (cross-system Quartz AD) |

## 6. Time Synchronisation (NTP)

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-NTP-01 | NTP source | Quartz AD PDC emulator (cross-system) → Veeam B&R + ExaGrid + DR + tape catalog | FS-AN11-01 |
| DS-NTP-02 | Cloud NTP | AWS time-sync service via VPC | FS-AN11-02 |
| DS-NTP-03 | Drift threshold | ≤ 5 seconds before alert; ≤ 30 seconds before backup-job suspension | FS-AN11-03 |
| DS-NTP-04 | NTP monitor | Splunk saved-search `aur-backup-ntp-monitor` | FS-AN11-04 |

## 7. Backup + Storage Tier Design (CORE)

### 7.1 Tier classification per source system

| DS-ID | Tier | Sources | RPO | RTO | Retention | FS-IDs |
|---|---|---|---|---|---|---|
| DS-TIER-01 | **T1** (mission-critical) | Sirius PV (Argus), Lyrae AI/ML Model Server, Tessera CV, Hydra GenAI, Quartz AD, Cetus LIMS, Caelum LIMS, MES PAS-X (Ophir), Helios.ATR | RPO ≤ 1 h | RTO ≤ 4 BH | ≥ 25 y (Annex 11 § 7 + Part 11) | FS-RPO-01, FS-RTO-01, FS-COV-01 |
| DS-TIER-02 | **T2** (important) | Theia MDR (TWD-Q), MasterControl eQMS, Marigold EDC, ELN Cyrene, RIM Nimbus, eTMF Marinos | RPO ≤ 4 h | RTO ≤ 24 BH | ≥ 25 y | FS-RPO-02, FS-RTO-02, FS-COV-02 |
| DS-TIER-03 | **T3** (archival / supporting) | Departmental shares, project repositories, non-GxP shared drives | RPO ≤ 24 h | RTO ≤ 72 BH | ≥ 10 y | FS-RPO-03, FS-COV-03 |

### 7.2 3-2-1-1-0 topology design

| DS-ID | Copy | Medium | Location | Retention | Immutability mode | FS-IDs |
|---|---|---|---|---|---|---|
| DS-COPY-01 | Copy 1 — Primary backup | ExaGrid EX84 disk + deduplication | Espoo | T1: 90 d hot, 1 y warm; T2: 60 d hot, 90 d warm; T3: 30 d hot | Veeam-immutability via Linux Hardened Repository (per ExaGrid) | FS-METH-01, FS-COV-04 |
| DS-COPY-02 | Copy 2 — DR replica | ExaGrid EX84 disk | Tampere | Same as Copy 1 | Hardened repository + Veeam-immutability | FS-METH-02 |
| DS-COPY-03 | Copy 3 — Cloud immutable | AWS S3 Object Lock Compliance + Glacier Vault Lock | AWS eu-north-1 + eu-central-1 (geo-replicated) | T1: ≥ 25 y; T2: ≥ 25 y; T3: ≥ 10 y | **S3 Object Lock Compliance mode (neither user nor root delete; lifecycle pinned)** | FS-IMM-01, FS-IMM-02, FS-IMM-03, FS-IMM-04, FS-IMM-05, FS-IMM-06 |
| DS-COPY-04 | Copy 4 — Air-gap | LTO-9 (45 TB compressed) | Helsinki vault | T1 monthly + quarterly per FS-COV-05 | WORM (LTO-9 WORM cartridge) + physical air-gap | FS-METH-03, FS-COV-05 |

### 7.3 Schedule design

| DS-ID | Schedule | Frequency | Window | FS-IDs |
|---|---|---|---|---|
| DS-SCH-01 | T1 incremental | Hourly (T1) | 24×7 outside change-window | FS-SCH-01 |
| DS-SCH-02 | T1 full + DR replication | Weekly Saturday 02:00-08:00 local | 6-hour window | FS-SCH-02 |
| DS-SCH-03 | T2 incremental | Every 4 hours | 24×7 | FS-SCH-03 |
| DS-SCH-04 | T2 full | Weekly Sunday 02:00-08:00 | 6-hour window | FS-SCH-04 |
| DS-SCH-05 | T3 full (no incremental) | Daily | 24×7 | (FS-COV-03) |
| DS-SCH-06 | LTO-9 monthly air-gap rotation | First Tuesday of month | Tape courier same day | FS-COV-05 |
| DS-SCH-07 | Cloud-immutable sync | After every successful local backup | ≤ 60 min lag | FS-IMM-03 |

### 7.4 Database-aware processing (Application-Aware)

| DS-ID | Source | Method | FS-IDs |
|---|---|---|---|
| DS-DB-01 | Oracle 19c (Argus PV, Catalog, RIM) | RMAN integration via Veeam Application-Aware + Oracle plug-in; archived-redo continuous | FS-METH-01 |
| DS-DB-02 | PostgreSQL 16 (Lyrae, Hydra, Helios, Tessera, Theia, others) | `pg_basebackup` + WAL streaming via Veeam | FS-METH-01 |
| DS-DB-03 | Microsoft SQL Server (Veeam Catalog, ServiceNow, MES PAS-X partial) | VSS + Veeam SQL plug-in; transaction-log every 15 min | FS-METH-01 |
| DS-DB-04 | MongoDB (some application stores) | mongodump + WiredTiger snapshot via Veeam plug-in | FS-METH-01 |
| DS-DB-05 | DuckDB (Helios analytical) | File-level snapshot + checksum | (Helios specific) |
| DS-DB-06 | MinIO + S3 (model + object stores) | Object-replica + integrity verification | (Lyrae + Hydra specific) |

### 7.5 Backup integrity + verification

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-INT-01 | SHA-256 checksum on every backup chunk | Veeam-native | FS-DI-01, FS-DI-02 |
| DS-INT-02 | Surebackup / Instant-recovery test | Weekly T1; monthly T2; quarterly T3 | FS-TEST-01..03 |
| DS-INT-03 | Monthly QA-witnessed restore test | All T1 sources; rotation pattern documented | FS-TEST-04, FS-TEST-05 |
| DS-INT-04 | Quarterly full-restore drill | Tampere site activation; partial production cutover | FS-TEST-06 |
| DS-INT-05 | Annual full-DR exercise | Espoo → Tampere full failover + cutback | FS-TEST-07 |
| DS-INT-06 | Cloud-immutable restore drill | Annual; from S3 + Glacier | FS-IMM-06 |
| DS-INT-07 | Air-gap restore drill | Annual; LTO-9 tape from Helsinki vault | FS-COV-05 |

### 7.6 Encryption + secrets

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-SEC-01 | Encryption at rest — disk | Veeam-native AES-256 + ExaGrid AES-256 | FS-SEC-01 |
| DS-SEC-02 | Encryption at rest — cloud | S3 SSE-KMS with customer-managed key (Vault-stored) | FS-SEC-02 |
| DS-SEC-03 | Encryption at rest — tape | LTO-9 hardware encryption AES-256 | FS-SEC-03 |
| DS-SEC-04 | KMS key rotation | 90 d for cloud key; 365 d for tape master key | FS-SEC-04 |
| DS-SEC-05 | Encryption in transit | TLS 1.3 to S3; Veeam-native TLS 1.3 for replication | FS-SEC-05 |
| DS-SEC-06 | Vault for secrets | HashiCorp Vault per FS-SEC-06 | FS-SEC-06 |
| DS-SEC-07 | Air-gap chain-of-custody | Dual-witness handoff at Helsinki; tape catalog signed by both | FS-SEC-07 |
| DS-SEC-08 | Physical security (Helsinki vault) | Mantrap + dual-control + 24×7 CCTV | FS-SEC-08 |

## 8. Ransomware Playbook + Recovery

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-RAN-01 | Detection | Veeam-native ransomware indicators (entropy + rate-of-change) + Splunk SIEM correlation | FS-RAN-01 |
| DS-RAN-02 | Isolation | Veeam B&R Mgmt isolation on detection; production-source isolation per InfoSec runbook | FS-RAN-02 |
| DS-RAN-03 | Recovery source | Cloud-immutable (S3 Object Lock) primary; LTO-9 air-gap secondary | FS-RAN-03 |
| DS-RAN-04 | Recovery RTO | T1 RTO ≤ 4 BH from immutable source | FS-RAN-04 |
| DS-RAN-05 | Forensic snapshot | Snapshot of compromised state for forensic investigation before recovery | FS-RAN-05 |
| DS-RAN-06 | Annual ransomware tabletop | Tabletop exercise + live partial recovery from S3 immutable | FS-RAN-06 |

## 9. Hardening Baseline

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-HARDEN-01 | Veeam B&R Mgmt server OS hardening | CIS Microsoft Windows Server 2022 Benchmark L1 + DISA STIG | FS-AN11-01 |
| DS-HARDEN-02 | ExaGrid + Linux Hardened Repository | CIS Linux Benchmark + ExaGrid hardened-repository policy | FS-AN11-02 |
| DS-HARDEN-03 | BSI IT-Grundschutz CON.6 (data backup) baseline | DACH baseline | FS-AN11-03 |
| DS-HARDEN-04 | NIST SP 800-53 CP-9 (Contingency Backup) | Baseline + CP-10 + CP-12 | FS-AN11-04 |
| DS-HARDEN-05 | Veeam admin console MFA | FIDO2 phishing-resistant via Quartz AD | (cross-system Quartz AD) |
| DS-HARDEN-06 | Backup-network segregation | Backup VLANs isolated; no Internet egress except DC Direct Connect | (DS-NET-*) |
| DS-HARDEN-07 | Tamper-evident logging | Veeam B&R logs forwarded to Splunk frozen-index 25 y | FS-AUD-01..06 |
| DS-HARDEN-08 | Deviation register | Per-deviation entry reviewed quarterly | FS-AN11-01..04 |

## 10. Monitoring + Audit Trail

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-AUD-01 | Audit-event taxonomy | Veeam-native + custom events: `JOB_STARTED`, `JOB_COMPLETED`, `JOB_FAILED`, `RESTORE_INITIATED`, `RESTORE_COMPLETED`, `POLICY_CHANGED`, `IMMUTABILITY_CHANGED`, `TAPE_ROTATED`, `RANSOMWARE_INDICATOR`, `KMS_ROTATION` | FS-AUD-01 |
| DS-AUD-02 | SIEM forwarding | Splunk index `aur-backup-audit` via TLS 1.3 forwarder; lag SLO 5 min | FS-AUD-02 |
| DS-AUD-03 | Retention | 25 y frozen-index + 25 y S3 Object Lock cold | FS-AUD-03 |
| DS-AUD-04 | Periodic review | Monthly Backup-Ops review; quarterly QA-witnessed | FS-AUD-04 |
| DS-AUD-05 | Restore-certificate quality records | 25 y in eQMS (MasterControl) per FS-AUD-05 | FS-AUD-05 |
| DS-AUD-06 | Audit-trail integrity | HMAC-SHA-256 per event | FS-AUD-06 |
| DS-MON-01 | Job-success Prometheus metric | `backup_job_success_rate{tier=T1\|T2\|T3}` | FS-MON-01 |
| DS-MON-02 | Restore-test pass rate | `restore_test_pass_rate{tier=}` | FS-MON-02 |
| DS-MON-03 | RPO breach alert | Per source per tier; PagerDuty on breach | FS-MON-03 |
| DS-MON-04 | RTO test result | Tracked per drill in `aur-rto-tracker` | FS-MON-04 |
| DS-MON-05 | Cloud-immutable lag | `s3_immutable_lag_seconds`; alert > 1 h | FS-MON-05 |

## 11. Integration Design (cross-system XSYS-BAK consumers)

Every GxP system in the Aurora-pharma estate consumes this DS via a `FS-XSYS-BAK-01` interface. The pattern is uniform:

| DS-ID | Consumer | Backup method | Tier | RPO | RTO | FS-IDs |
|---|---|---|---|---|---|---|
| DS-XSYS-LYR-01 | Lyrae AI/ML Model Server | Veeam Application-Aware + Postgres pg_basebackup + WAL + MinIO/S3 object-replica for model artefacts + Annex IV pack | T1 | ≤ 4 h | ≤ 4 BH | per LYR-FS-XSYS-BAK-01 |
| DS-XSYS-HYD-01 | Hydra GenAI | Veeam Application-Aware + per-tenant Postgres + Pinecone snapshot + Vault per-tenant key backup | T1 | ≤ 4 h | ≤ 4 BH | per HYD2-FS-XSYS-BAK-01 |
| DS-XSYS-TES-01 | Tessera CV Inspection | Veeam Application-Aware + MLflow Postgres + inference S3 object-replica | T1 | ≤ 4 h | ≤ 4 BH | per TES-FS-XSYS-BAK-01 |
| DS-XSYS-HBS-01 | Helios.ATR | Veeam Application-Aware + Postgres + DuckDB file snapshot + S3 cold | T1 | ≤ 4 h | ≤ 4 BH | per HBS-FS-XSYS-BAK-01 |
| DS-XSYS-SIR-01 | Sirius PV (Argus) | Veeam Application-Aware + Oracle RMAN | T1 | ≤ 4 h | ≤ 4 BH | per SIR-FS-XSYS-BAK-01 |
| DS-XSYS-TEA-01 | Theia MDR (TWD-Q) | Veeam Application-Aware on TWD-Q tenant + Atlas DB | T2 | ≤ 4 h | ≤ 4 BH | per TEA-FS-XSYS-BAK-01 |
| DS-XSYS-QTZ-01 | Quartz AD | Veeam Application-Aware + AD DS system-state + ADCS DB + CyberArk Vault native backup | T1 | ≤ 1 h | ≤ 4 BH | per QTZ-FS-XSYS-BAK-01 |
| (… all other GxP systems in the estate) | (… per per-system FS-XSYS-BAK-01) | (… same pattern) | (… per tier) | (…) | (…) | (… per-system) |

Every cross-system consumer receives a monthly QA-witnessed restore-certificate signed by Backup-Ops + QA + System Owner; certificate retained ≥ 25 y in MasterControl eQMS per FS-AUD-05.

## 12. References

**US**
- 21 CFR Part 11 §§ .10, .50, .70, .100
- NIST SP 800-53 r5 — CP-9 (Backup), CP-10 (Recovery), CP-12 (Safe Mode)

**EU**
- **EU GMP Annex 11 §§ 4.8 (backup), 7 (data storage), 9 (audit trail), 12 (security)**
- EU GMP Annex 11 § 17 (archive)
- **NIS2 Directive (EU) 2022/2555 — important entity (backup as essential service component)**
- GDPR Reg. (EU) 2016/679 Arts. 32, 33, 35

**International**
- ISO/IEC 27001:2022 — **Annex A.5.30 (ICT readiness for business continuity), A.8.13 (Information backup)**
- ISO/IEC 27002:2022 — control set
- ISO 22301:2019 (BCMS)
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE GAMP GPG *IT Infrastructure Control and Compliance*
- CIS Microsoft Windows Server 2022 Benchmark; CIS Linux Benchmark; CIS AWS Foundations Benchmark
- ENISA Threat Landscape for Ransomware (2024)

**DACH**
- **BSI IT-Grundschutz CON.6 (Data backup)**
- BSI BSI-Standard 200-1/200-2/200-3
- BfArM (DE) — GxP-server backup inspection focus

**Vendor**
- Veeam — *Backup & Replication 12.1 User Guide + Best Practices*
- Veeam — *Hardened Repository Reference Implementation Guide*
- Veeam — *Application-Aware Processing Guide (Oracle, SQL Server, PostgreSQL, MongoDB)*
- ExaGrid — *EX-Series Administrator Guide*
- AWS — *S3 Object Lock + Glacier Vault Lock documentation*
- LTO-9 specification (LTO Technical Provider Council)

## 13. Appendix A — DS → FS Traceability Matrix

One row per DS-ID. No range compression.

| DS ID | FS ID(s) |
|---|---|
| DS-NET-01 | FS-PLAT-01 |
| DS-NET-02 | FS-PLAT-02 |
| DS-NET-03 | FS-PLAT-03 |
| DS-NET-04 | FS-PLAT-04 |
| DS-NET-05 | FS-PLAT-05 |
| DS-NET-06 | FS-IMM-01, FS-IMM-02, FS-IMM-03, FS-IMM-04, FS-IMM-05, FS-IMM-06 |
| DS-NET-07 | FS-IMM-03, FS-IMM-04 |
| DS-NET-08 | FS-PLAT-04 |
| DS-NET-09 | FS-PLAT-05 |
| DS-IDENT-01 | FS-SEC-01, FS-SEC-05 |
| DS-IDENT-02 | FS-SEC-01 |
| DS-IDENT-03 | FS-SEC-01 |
| DS-IDENT-04 | FS-SEC-01 |
| DS-IDENT-05 | FS-SEC-07 |
| DS-IDENT-06 | FS-SEC-01 |
| DS-IDENT-07 | FS-SEC-01, FS-SEC-05 (cross-system Quartz AD) |
| DS-NTP-01 | FS-DI-03, FS-AN11-03 |
| DS-NTP-02 | FS-DI-03, FS-AN11-03 |
| DS-NTP-03 | FS-DI-03, FS-MON-01 |
| DS-NTP-04 | FS-DI-03, FS-MON-01 |
| DS-TIER-01 | FS-RPO-01, FS-RTO-01, FS-COV-02 |
| DS-TIER-02 | FS-RPO-01, FS-RTO-01, FS-COV-02 |
| DS-TIER-03 | FS-RPO-01, FS-RTO-01, FS-COV-02 |
| DS-COPY-01 | FS-METH-01, FS-METH-02, FS-PLAT-02 |
| DS-COPY-02 | FS-PLAT-01, FS-PLAT-02, FS-DR-01 |
| DS-COPY-03 | FS-IMM-01, FS-IMM-02, FS-IMM-04, FS-IMM-05, FS-IMM-06 |
| DS-COPY-04 | FS-IMM-01, FS-IMM-03, FS-SCH-04 |
| DS-SCH-01 | FS-SCH-01, FS-METH-03 |
| DS-SCH-02 | FS-SCH-01, FS-SCH-02 |
| DS-SCH-03 | FS-SCH-01 |
| DS-SCH-04 | FS-SCH-01, FS-SCH-02 |
| DS-SCH-05 | FS-SCH-01, FS-SCH-02 |
| DS-SCH-06 | FS-SCH-04 |
| DS-SCH-07 | FS-SCH-03, FS-IMM-04 |
| DS-DB-01 | FS-METH-01 |
| DS-DB-02 | FS-METH-01 |
| DS-DB-03 | FS-METH-01 |
| DS-DB-04 | FS-METH-01 |
| DS-DB-05 | FS-METH-02 |
| DS-DB-06 | FS-METH-02 |
| DS-INT-01 | FS-DI-05 |
| DS-INT-02 | FS-TEST-01, FS-DI-05 |
| DS-INT-03 | FS-TEST-02, FS-TEST-05 |
| DS-INT-04 | FS-TEST-03, FS-DR-01 |
| DS-INT-05 | FS-TEST-03, FS-DR-01, FS-DR-02 |
| DS-INT-06 | FS-IMM-05 |
| DS-INT-07 | FS-IMM-05, FS-TEST-01 |
| DS-SEC-01 | FS-SEC-02 |
| DS-SEC-02 | FS-SEC-02, FS-SEC-07 |
| DS-SEC-03 | FS-SEC-02 |
| DS-SEC-04 | FS-SEC-07 |
| DS-SEC-05 | FS-SEC-02 |
| DS-SEC-06 | FS-SEC-07 |
| DS-SEC-07 | FS-TRN-02 |
| DS-SEC-08 | FS-SEC-08 |
| DS-RAN-01 | FS-RAN-01, FS-MON-05 |
| DS-RAN-02 | FS-RAN-01 |
| DS-RAN-03 | FS-RAN-01, FS-IMM-01 |
| DS-RAN-04 | FS-RTO-01, FS-RAN-01 |
| DS-RAN-05 | FS-RAN-01, FS-RAN-03 |
| DS-RAN-06 | FS-RAN-04, FS-RAN-06 |
| DS-HARDEN-01 | FS-PLAT-01, FS-AN11-04 |
| DS-HARDEN-02 | FS-PLAT-02, FS-AN11-04 |
| DS-HARDEN-03 | FS-AN11-04 |
| DS-HARDEN-04 | FS-AN11-04 |
| DS-HARDEN-05 | FS-SEC-05 |
| DS-HARDEN-06 | FS-PLAT-04, FS-SEC-08 |
| DS-HARDEN-07 | FS-AUD-01, FS-AUD-02 |
| DS-HARDEN-08 | FS-PR-01 |
| DS-AUD-01 | FS-AUD-01, FS-AUD-05 |
| DS-AUD-02 | FS-AUD-02 |
| DS-AUD-03 | FS-AUD-02, FS-AUD-04 |
| DS-AUD-04 | FS-PR-01, FS-PR-02 |
| DS-AUD-05 | FS-AUD-04, FS-TEST-05 |
| DS-AUD-06 | FS-AUD-02, FS-AUD-06 |
| DS-MON-01 | FS-MON-01, FS-MON-02 |
| DS-MON-02 | FS-MON-02 |
| DS-MON-03 | FS-MON-01, FS-MON-05 |
| DS-MON-04 | FS-MON-02 |
| DS-MON-05 | FS-MON-05 |
| DS-XSYS-LYR-01 | FS-INT-05 (per LYR-FS-XSYS-BAK-01) |
| DS-XSYS-HYD-01 | FS-INT-05 (per HYD2-FS-XSYS-BAK-01) |
| DS-XSYS-TES-01 | FS-INT-05 (per TES-FS-XSYS-BAK-01) |
| DS-XSYS-HBS-01 | FS-INT-05 (per HBS-FS-XSYS-BAK-01) |
| DS-XSYS-SIR-01 | FS-INT-05 (per SIR-FS-XSYS-BAK-01) |
| DS-XSYS-TEA-01 | FS-INT-05 (per TEA-FS-XSYS-BAK-01) |
| DS-XSYS-QTZ-01 | FS-INT-04, FS-INT-05 (per QTZ-FS-XSYS-BAK-01) |

**Coverage footnote.** 88 per-DS-ID rows expanded above cover the design surface of the Aurora backup platform. FS-IDs in the parent FS that are covered transitively (not bound to a single DS-ID) and therefore not listed in column 2 of any row: FS-PART11-01 through FS-PART11-08 (transitively satisfied via DS-AUD-*, DS-SEC-*, DS-IDENT-*, and DS-INT-* class rows), FS-COV-01 + FS-COV-03 + FS-COV-04 + FS-COV-05 (asset-register integration + new-server-onboarding workflow — process steps, not design CIs), FS-RPO-02 + FS-RPO-03 + FS-RTO-02 (KPI / reporting dashboards bound to DS-MON-* class), FS-TEST-04 + FS-TEST-06 + FS-TEST-07 (eQMS deviation workflow + filter view + triennial surprise drill — bound to the DS-INT-03 + DS-INT-04 + DS-INT-05 cadence rows above), FS-AN11-01 + FS-AN11-02 (Annex 11 § 4.8 + § 7.2 cited collectively by FS-TEST-* + DS-INT-* class per § 2B.7), FS-DI-01 + FS-DI-02 + FS-DI-04 + FS-DI-06 (operator-identity logging + read-only-source semantics + ransomware-resistant architecture — properties realised by DS-AUD-01 plus the DS-DB-01 through DS-DB-06 rows plus DS-COPY-03 plus DS-COPY-04), FS-SEC-03 + FS-SEC-04 + FS-SEC-06 (Object-Lock compliance assertion + vulnerability scan SLA + CyberArk vendor-session brokering — covered via DS-COPY-03 + DS-HARDEN-08 + DS-IDENT-04 + DS-IDENT-05), FS-COST-* + FS-PERF-01 + FS-PERF-02 + FS-PERF-03 + FS-TRN-01 + FS-PR-* (operational + training + periodic-review processes — covered through DS-AUD-04 + DS-HARDEN-08 + cross-system Quartz AD LMS), FS-MON-03 + FS-MON-04 (asset-register reconciliation + capacity-forecasting — DS-AUD-04 + DS-MON-* class). Per § 2B.7(6): no IQ/OQ/PQ rows; infrastructure qualification cited by reference (`AUR-IQ-BACKUP-001`, `AUR-IQ-EXAGRID-001`, `AUR-IQ-S3-001`, `AUR-IQ-LTO9-001`).

## 14. Design-level Risk Register

| ID | Design-stage risk | Likelihood | Impact | Bound DS-IDs | Mitigation reference |
|---|---|---|---|---|---|
| D-01 | **Ransomware encrypts ExaGrid + replica + cloud cache simultaneously** before air-gap rotation | Low | **Critical** | DS-COPY-01, DS-COPY-02, DS-COPY-03 | LTO-9 air-gap (DS-COPY-04) as last-resort + monthly rotation |
| D-02 | **S3 Object Lock Compliance mode policy** drift — retention shortened or deleted | Low | **Critical** | DS-COPY-03 | KMS key access SoD + annual policy audit |
| D-03 | **Tampere DR site** in-flight replication backlog at moment of Espoo failure → RPO breach | Medium | High | DS-COPY-02, DS-NET-08 | Replication-lag SLO + on-call alert; quarterly DR drill |
| D-04 | **LTO-9 tape degradation** at Helsinki vault undetected | Low | High | DS-COPY-04 | Annual tape integrity audit; rotation 5-year refresh policy |
| D-05 | **Backup-network bridged to production network** via misconfigured firewall — ransomware lateral movement | Low | **Critical** | DS-NET-01, DS-NET-02, DS-NET-03, DS-NET-04, DS-NET-05 | CR for all firewall changes + quarterly rule review |
| D-06 | **Application-Aware processing failure** silently produces crash-inconsistent Oracle / SQL Server / Postgres backup | Medium | **Critical** | DS-DB-01, DS-DB-02, DS-DB-03, DS-DB-04, DS-DB-05, DS-DB-06 | Per-DB Surebackup test (DS-INT-02) + monthly QA-witnessed restore |
| D-07 | **Cloud-immutable lag** > 1 h during peak production change-rate | Medium | High | DS-MON-05 | Alert + bandwidth scaling |
| D-08 | **KMS-key compromise** (S3 cloud-encrypt key) | Low | **Critical** | DS-SEC-02, DS-SEC-04 | Vault HSM-backed; 90-d rotation; access audit |
| D-09 | **Tape chain-of-custody break** during Helsinki rotation | Low | High | DS-SEC-07 | Dual-witness sign-off + tamper-evident transport |
| D-10 | **Veeam B&R management console hijack** | Low | **Critical** | DS-IDENT-01, DS-IDENT-02, DS-IDENT-03 | FIDO2 MFA + SoD + SIEM alert on policy change |
| D-11 | **Restore drill** misses a T1 source for > 12 months | Medium | High | DS-INT-03 | Rotation matrix in `aur-restore-cadence-matrix` |
| D-12 | **NIS2 incident-reporting clock missed** (24 h initial / 72 h intermediate / 1 month final) | Low | **Critical (NIS2 penalty)** | DS-AUD-01 | CSO escalation + NIS2-aligned incident-response runbook |
| D-13 | **ExaGrid deduplication** mis-tune produces silent block-corruption | Low | Critical | DS-COPY-01 | Surebackup test + verify-jobs cadence |
| D-14 | **Air-gap vault** physical-security breach (Helsinki) | Low | **Critical** | DS-SEC-08 | Third-party CCTV + mantrap + dual-control |
| D-15 | **Cross-system consumer drift** — a new GxP system onboarded without XSYS-BAK adapter | Low | High | DS-XSYS-* | System-onboarding gate requires Backup-Ops + QA sign-off |
| D-16 | **Restore certificate** missing for an FDA / EMA inspection retrieval | Low | Critical | DS-AUD-05 | Monthly QA-witnessed restore + certificate filed in MasterControl |
| D-17 | **Veeam licence expiry** during incident | Low | High | License inventory | D-30 / D-7 license-expiry alert |
| D-18 | **Direct Connect outage** Espoo ↔ AWS during cloud-immutable sync window | Medium | High | DS-NET-07 | IPSec backup link + retry policy |
| D-19 | **GDPR data-residency** for personal-data-bearing backups in non-EU region | Low | High | DS-COPY-03 | AWS eu-north-1 + eu-central-1 (EU only); GDPR Art. 44 SCC |
| D-20 | **LTO-9 cartridge** end-of-life supplier shortage | Low | Medium | DS-COPY-04 | 2-year tape stockpile + LTO-10 evaluation |
| D-21 | **Backup-job overlap** with production change-window | Medium | Medium | DS-SCH-01, DS-SCH-02, DS-SCH-03, DS-SCH-04, DS-SCH-05, DS-SCH-06 | Change-control calendar integration |
| D-22 | **Surebackup test** false-pass — restored VM boots but app-layer broken | Medium | High | DS-INT-02 | App-layer verify step in Surebackup |
| D-23 | **Veeam catalog corruption** during DR cutover | Low | High | DS-DB-03 | Catalog backed up independently + mirror at Tampere |
| D-24 | **Cross-system consumer's per-source mTLS cert** expires blocking backup-job | Low | High | DS-SEC-05 | Cert-expiry monitor D-30 alert per consumer |
| D-25 | **Annual full-DR exercise** discovers RTO > target due to scale change | Medium | High | DS-INT-05 | Annual capacity planning review |
| D-26 | **Splunk frozen-index 25-y retention** cost overrun forces silent tier-downshift | Low | **Critical** | DS-AUD-03 | Annual storage-cost review + VP QA sign-off |
| D-27 | **Forensic snapshot** of compromised state overwritten before forensic analysis | Low | High | DS-RAN-05 | Forensic-snapshot retention policy ≥ 90 d |
| D-28 | **Periodic-review orchestrator** fails to capture a new mandatory metric after Annex 11 amendment | Low | High | DS-AUD-04 + DS-MON-* | Annual orchestrator-template review against current Annex 11 + ISO 27001 |
| D-29 | **DR cutback to Espoo** post-Tampere failover takes longer than expected | Medium | High | DS-INT-05 | Cutback runbook + annual rehearsal |
| D-30 | **AWS service-quota** on S3 + Glacier exceeded during mass-restore | Low | High | DS-COPY-03 | Pre-allocated quota + AWS support pre-arranged |
| D-31 | **LTO-9 read-drive availability** in 25-year retention horizon | Low | High | DS-COPY-04 | Forward-migration policy to LTO-12+ within 5-year drive obsolescence window |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
