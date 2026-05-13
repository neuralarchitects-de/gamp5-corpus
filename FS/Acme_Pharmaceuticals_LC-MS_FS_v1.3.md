---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring 2026-04-27; T2 rebuild 2026-05-13 (Chunk A LC-MS)"
seed_corpus_basis:
  - "ACME-URS-LCMS-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd Edition) Category 4 conventions"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300"
  - "21 CFR Part 211 §§ .68, .180, .192"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "USP <621>; USP <1058> AIQ; USP <1224>-<1226>"
  - "ICH Q2(R2)"
  - "Waters MassLynx 4.2 SCN1027 + TargetLynx XS + Acquity I-Class + Xevo TQ-S micro"
parent_urs:
  document_number: ACME-URS-LCMS-001
  version: 1.2
  file: ../../URS/_generated/final/Acme_Pharmaceuticals_LC-MS_Computer_System_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## LC-MS Computer System — Waters Acquity I-Class UPLC + Xevo TQ-S micro + MassLynx 4.2 SCN1027

**Document Number:** ACME-FS-LCMS-001 | **Version:** 1.2 | **Effective Date:** 2026-05-13 *(synthetic)*
**Parent URS:** ACME-URS-LCMS-001 v1.2 | **Site:** Acme Pharmaceuticals Ltd, QC Lab, Pune, India *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <621>; USP <1058>; ICH Q2(R2); PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Mass-Spec Lead) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Approver (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-13 | (synthetic) | T2 rebuild aligned to URS v1.2 (Waters MassLynx 4.2 SCN1027 + TargetLynx XS + Acquity I-Class + Xevo TQ-S micro). Vendor corrected (was incorrectly Sciex in v1.0). Per-URS-ID FS row expansion (no range compression). New §4 subsections: SST per USP <621>, mass-calibration + tune mgmt, calibration-curve + quantitation, method lifecycle + reprocessing, MS library mgmt, LIMS interface. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## Definitions

Inherited from `ACME-URS-LCMS-001`. Additional FS-specific terms:

| Term | Definition |
|---|---|
| MassLynx | Waters Empower-family chromatography data system for LC-MS workflows |
| TargetLynx XS | MassLynx application manager for targeted quantitation + SST evaluation |
| SCN | Waters Service / Control Notification (patch / hot-fix bundle) |
| MS-Library Hash | SHA-256 of the controlled mass-spectrum library binary |
| RTDB | Retention-time database (per-method, per-column-lot RT pinning) |

## 1. Purpose

This FS specifies the deployment, configuration, and integration of Waters MassLynx 4.2 SCN1027 + TargetLynx XS on a dedicated workstation controlling one Acquity I-Class UPLC + Xevo TQ-S micro tandem-quadrupole MS to satisfy `ACME-URS-LCMS-001` v1.2.

## 2. Scope

Mirrors URS § 2: one MassLynx workstation on a dedicated VLAN, AD-bound, NTP-synced, with project files on the GMP file-server share `\\acme-gmp-fs01\masslynx-projects`. LIMS integration to LabWare LIMS 8 (worklist in + approved-result push). Out: sample-prep hardware (separately validated); LIMS sample lifecycle.

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source / Vendor | Notes |
|---|---|---|---|---|---|
| C-01 | Acquity I-Class UPLC chassis | Hardware | 3 | Waters | binary pump, autosampler, column manager |
| C-02 | Xevo TQ-S micro tandem quadrupole MS | Hardware | 3 | Waters | tandem-quadrupole, ESI source |
| C-03 | MassLynx 4.2 SCN1027 + TargetLynx XS | COTS app | 4 | Waters | configured for site Part 11 policy |
| C-04 | Workstation (HP Z4 G5) | Hardware | 3 | HP | Win 11 Pro 22H2, 32 GB RAM, 1 TB SSD |
| C-05 | AD `acme.local` | Infrastructure | 1 | Microsoft | authN |
| C-06 | NTP server `ntp.acme.local` | Infrastructure | 1 | (site) | time sync |
| C-07 | File share `\\acme-gmp-fs01\masslynx-projects` | Infrastructure | 1 | NetApp (SnapLock) | WORM tier, 7-y retention |
| C-08 | LabWare LIMS 8 + Waters LIMS Connector | COTS adapter | 4 | LabWare / Waters | bidirectional |
| C-09 | Splunk Universal Forwarder | COTS infra | 1 | Splunk | log forwarding to SIEM |
| C-10 | CrowdStrike Falcon Sensor | COTS infra | 1 | CrowdStrike | anti-malware |
| C-11 | Local printer (Brother HL-L6415DW) | Hardware | (n/a) | Brother | QC sign-off hard copies |

### 3.2 Logical Architecture (textual)

```
            AD `acme.local`        NTP `ntp.acme.local`
                  │                       │
                  └──────────┬────────────┘
                             ▼
              ┌────────────────────────────────┐
              │ MassLynx Workstation (HP Z4 G5)│
              │ Win 11 Pro 22H2 (domain-joined)│
              │  MassLynx 4.2 SCN1027          │
              │  + TargetLynx XS               │
              └───────┬────────────┬────────────┘
                      │            │
        USB-3 to:     │            │ SMB to file share
                      │            │
   ┌──────────────────▼──┐   ┌─────▼─────────────────────────┐
   │ Acquity I-Class UPLC │   │ \\acme-gmp-fs01\masslynx-     │
   │ + Xevo TQ-S micro MS │   │ projects (WORM, 7-y retention) │
   └──────────────────────┘   └────────────────────────────────┘
                      │
                      ▼
              Waters LIMS Connector ──► LabWare LIMS 8
              (worklist in + approved-result push)
```

### 3.3 Functional Modules

| Module | URS sections |
|---|---|
| M-HW | URS-HW-* |
| M-SW | URS-SW-* |
| M-ACQ | URS-ACQ-* |
| M-PROC | URS-PROC-* |
| M-AUD | URS-AUD-* |
| M-PART11 | URS-PART11-* |
| M-DI | URS-DI-* |
| M-BAK | URS-BAK-* |
| M-PERF | URS-PERF-* |
| M-SEC | URS-SEC-* |
| M-TRN | URS-TRN-* |
| M-PR | URS-PR-* |
| M-SST | URS-SST-* |
| M-CAL | URS-CAL-* |
| M-QNT | URS-QNT-* |
| M-MTH | URS-MTH-* |
| M-LIB | URS-LIB-* |
| M-INT | URS-INT-LIMS-* |

## 4. Functional Specifications

### 4.1 Hardware (M-HW)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-HW-01 | URS-HW-01 | Asset-register entry binds the HP Z4 G5 workstation by serial to the Acquity I-Class UPLC + Xevo TQ-S micro by serial; one-to-one binding enforced; no shared workstations. |
| FS-HW-02 | URS-HW-02 | Workstation spec: HP Z4 G5, Intel Xeon W3-2425, 32 GB DDR5 ECC, 1 TB NVMe SSD (system) + 2 TB NVMe SSD (data cache), NVIDIA T1000, 4× USB-3.2 Gen 2 (two reserved for Acquity + Xevo). |
| FS-HW-03 | URS-HW-03 | UPS APC SMT2200RM2UC sized for ≥ 30 min hold at typical load (200 W workstation + 1.2 kW Acquity + 1.8 kW Xevo source-heater); SNMP-triggered Windows controlled shutdown at 20% remaining. |
| FS-HW-04 | URS-HW-04 | Workstation on VLAN 411 (GMP-Lab); office-segment routing blocked at the firewall; verified by `IQ-HW-04`. |
| FS-HW-05 | URS-HW-05 | Instrument-room HVAC controlled by site BMS; viewLinc EM probes T/RH 1-minute cadence; HVAC excursion (T outside 20 ± 3 °C or RH outside 30-60%) triggers SIEM alert and flags downstream runs as suspect. |

### 4.2 Software Configuration (M-SW)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SW-01 | URS-SW-01 | Win 11 Pro 22H2 image deployed via SCCM; domain-joined to `acme.local`; QC users in AD group `Lab-LCMS-Analysts`; no member of `Workstation-Admins` GPO except break-glass account `acme\bg-admin`. |
| FS-SW-02 | URS-SW-02 | MassLynx 4.2 SCN1027 + TargetLynx XS installed via Waters field-service procedure `WAT-FS-MLX-2024-007`; install verification per Waters IQ checklist, signed off by Waters engineer + site validation engineer; SCN-update workflow under site CR. |
| FS-SW-03 | URS-SW-03 | MassLynx "Project Root" registry setting points to `\\acme-gmp-fs01\masslynx-projects`; local C:\\MassLynx cache limited to 50 GB, auto-purged after successful network sync; verified by `IQ-SW-03`. |
| FS-SW-04 | URS-SW-04 | Windows audit policy enables `Audit Logon`, `Audit Account Management`, `Audit Object Access (\\acme-gmp-fs01\masslynx-projects)`; events forwarded to Splunk via Universal Forwarder (heavy index `wel-lcms`). |
| FS-SW-05 | URS-SW-05 | CrowdStrike Falcon Sensor with Waters-approved exclusion list (MassLynx installation paths, real-time-data writers, TargetLynx temp paths); daily definition auto-update. |
| FS-SW-06 | URS-SW-06 | Windows Time service syncs to `ntp.acme.local`; configured skew threshold 1 s; w32time event 35/29 monitored in Splunk; alert on skew > 1 s. |
| FS-SW-07 | URS-SW-07 | GPO `GMP-Lab-Workstations` enforces 10-minute screen-saver lock; only AD `Lab-LCMS-Analysts` group can interactively log on. |

### 4.3 Acquisition (M-ACQ)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ACQ-01 | URS-ACQ-01 | MassLynx "Method Library" folder ACL'd read-only for `Lab-LCMS-Analysts`; only `Lab-LCMS-MethodOwners` can create / edit; method-state machine implemented in TargetLynx (DRAFT / REVIEW / APPROVED / EFFECTIVE / SUPERSEDED / OBSOLETE). |
| FS-ACQ-02 | URS-ACQ-02 | Sequence-start preconditions enforced by a MassLynx pre-run macro: instrument Ready-state == true; method state == EFFECTIVE; project lock not held; mass-calibration not expired. Failure displays blocking dialog and writes an audit-trail entry. |
| FS-ACQ-03 | URS-ACQ-03 | Sequence template requires fields: sample-id, vial position, injection volume; auto-binds method-id + version, instrument-id + serial, analyst (from AD session), UTC timestamp at sequence start. |
| FS-ACQ-04 | URS-ACQ-04 | Pause / Resume captured as `SequenceModified` audit-trail event with mandatory reason text dialog. |
| FS-ACQ-05 | URS-ACQ-05 | TargetLynx XS evaluates SST per USP <621> at sequence start; SST failure flips sequence to status `SST-FAILED` and blocks downstream processing; see also FS-SST-* rows. |

### 4.4 Processing and Reporting (M-PROC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PROC-01 | URS-PROC-01 | Approved processing method auto-applied to sequence results via TargetLynx; manual integration requires explicit reason-for-change captured via Waters' Reason-for-Change feature with closed-list reason codes (e.g., baseline-noise, co-elution, peak-shoulder); free-text justification required. |
| FS-PROC-02 | URS-PROC-02 | Raw `.RAW` file is read-only after acquisition close (file-system ACL `nwt-svc-masslynx-acq` only at acquisition, then immutable); processing produces `.PRO` derived artefact with parent-pointer to the raw file's SHA-256 hash. |
| FS-PROC-03 | URS-PROC-03 | Mass-spectrum library matching via TargetLynx library-search engine against the controlled MS-library `ACME-MSLIB-2026Q2`; library version + library SHA-256 hash + per-peak match score persisted with result. |
| FS-PROC-04 | URS-PROC-04 | Computed via the TargetLynx-configured equation set per analyte (assay %, related-substance %, impurity µg/g); rounding rules per site SOP `SOP-QC-CHROM-ROUND-001`; intermediate precision preserved (rounding only at final report). |
| FS-PROC-05 | URS-PROC-05 | Report template `ACME-RPT-LCMS-001-v1.0.qrt` includes all URS-required fields, ALCOA+ statement, library-id + library hash, SHA-256 hash of the underlying `.PRO` artefact. PDF rendered as PDF/A-3 with embedded fonts. |
| FS-PROC-06 | URS-PROC-06 | "Re-issue Report" feature inserts watermark `RE-ISSUED — supersedes <originalReportId>` and creates a new report-id with link to original; both retained. |

### 4.5 Audit Trail and Records (M-AUD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | MassLynx audit trail records: timestamp (UTC + local), actor user, action type, target artefact, old-value, new-value, mandatory reason-for-change. Captured at project / method / sequence / result / signature level. |
| FS-AUD-02 | URS-AUD-02 | Audit-trail entries stored in MassLynx `.AT` files with NTFS-ACL deny-delete + deny-modify even to BUILTIN\Administrators; verified at IQ and at every quarterly Audit-Trail-Review. |
| FS-AUD-03 | URS-AUD-03 | Report template `ACME-RPT-LCMS-AUDIT-001` generates a printable PDF; Senior Analyst signs per-batch audit-trail review; QC Manager signs monthly audit-trail review. |
| FS-AUD-04 | URS-AUD-04 | File-server WORM tier (NetApp SnapLock Compliance) enforces 7-year retention; longer (25 y) for batch-linked projects via metadata tag `retention=25y`. |
| FS-AUD-05 | URS-AUD-05 | Read-only `Auditor` role exposes Audit Trail Review screen; PDF export uses the same template as periodic review. |

### 4.6 21 CFR Part 11 (M-PART11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Validation evidence per § 11.10(a) maintained in dossier `ACME-VAL-LCMS-001`: IQ, OQ, PQ, RTM, VSR, periodic-review records. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(b), all records exportable as PDF/A-3 (human-readable) + native `.RAW`/`.PRO`/`.AT` (electronic) using MassLynx batch-export. Verified at OQ. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(c), NetApp SnapLock Compliance enforces 7-y immutability; daily Veeam backup with SHA-256 integrity check; restore verified quarterly. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.10(d), AD-bound access via `Lab-LCMS-*` AD groups; local accounts other than break-glass disabled by GPO `Disable-Local-Accounts`. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.10(e), MassLynx audit trail per FS-AUD-01 covers user, action, timestamp. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.10(g), MassLynx user-role matrix maps AD groups to MassLynx authority sets: `Analyst`, `SeniorAnalyst`, `MethodOwner`, `QCManager`, `SystemAdmin`, `Auditor`. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.10(k), system-operation manual `ACME-RB-LCMS-OPS-001`; vendor SCN releases managed under site change-control with impact assessment + post-upgrade OQ verification (FS-PROC-04 re-tested). |
| FS-PART11-08 | URS-PART11-08 | Per § 11.50, MassLynx eSign dialog enforces capture of printed-name, dateTime, and meaning-of-signature from a closed list (`Review`, `Approve`, `Reject`, `Lock`). |
| FS-PART11-09 | URS-PART11-09 | Per § 11.70, signature payload includes the SHA-256 hash of the signed artefact (`.PRO` or report PDF); on read, the record's current hash is compared to the signature's payload hash — mismatch is displayed as `SIGNATURE INVALID — RECORD MODIFIED`. |
| FS-PART11-10 | URS-PART11-10 | Per § 11.100, each AD account is tied to a unique HR record; reuse / reassignment prohibited at AD level (HR feed creates new SID on any rehire). |
| FS-PART11-11 | URS-PART11-11 | Per § 11.200, MassLynx eSign requires re-authentication (ID + password) at the moment of signing; cached credentials not honoured (MassLynx setting `RequireSignatureReAuth = true`). |
| FS-PART11-12 | URS-PART11-12 | Per § 11.300, AD password policy enforced by GPO `Default Domain Policy`: 5 failures / 15-min window / 30-min lockout; Splunk `wel-lcms` SIEM alert on lockout. |
| FS-PART11-13 | URS-PART11-13 | MassLynx role matrix denies any single user holding both `Analyst` and `SeniorAnalyst`/`QCManager` MassLynx authorities on the same project; enforced at user-provisioning and verified at OQ. |

### 4.7 Data Integrity (M-DI)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | Every MassLynx artefact carries the AD account that created / modified it (`.AT` entries record `domain\user`). |
| FS-DI-02 | URS-DI-02 | PDF/A-3 export embeds fonts + ICC profile; legible across PDF/A-3-compliant readers. |
| FS-DI-03 | URS-DI-03 | Retrospective entries (entries with `recordedTimestamp` ≠ `eventTimestamp`) flagged in the audit trail with a reason. |
| FS-DI-04 | URS-DI-04 | `.RAW` artefact hash-bound on close-of-acquisition; ACL flips to immutable; integrity verified before every processing run. |
| FS-DI-05 | URS-DI-05 | OQ calculation regression: 10 reference samples × 3 analytes × 2 methods, re-run at every SCN upgrade; observed-vs-validated tolerance ≤ 0.01% of the spec limit. |
| FS-DI-06 | URS-DI-06 | NetApp SnapLock retention metadata + project-share availability target 99.5% verified by Splunk dashboard `wel-lcms-availability`. |

### 4.8 Backup, Restore, Disaster Recovery (M-BAK)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BAK-01 | URS-BAK-01 | Veeam B&R 12.1 backup job `masslynx-projects-daily` runs nightly at 02:00 IST; SHA-256 verification per backup; backup target replicated to off-site immutable storage. |
| FS-BAK-02 | URS-BAK-02 | Quarterly SureBackup-scripted restore test; test plan `ACME-PROC-BAK-RESTORE-001`; QC witness sign-off on restore-test report. |
| FS-BAK-03 | URS-BAK-03 | Documented hardware-replace + software-reinstall runbook `ACME-RB-LCMS-DR-001`; RTO ≤ 8 business hours verified annually. |
| FS-BAK-04 | URS-BAK-04 | RPO 24 h documented in DR plan; calculation: max backup-window = nightly 02:00 + 22-hour acquisition day. |

### 4.9 Performance (M-PERF)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | OQ stress-test sequence of 50 injections demonstrates no MassLynx crash + no `.RAW` data loss + complete audit-trail capture; Splunk log retained as evidence. |
| FS-PERF-02 | URS-PERF-02 | Processing benchmark: 50-injection sequence ≤ 15 min on the specified hardware. |
| FS-PERF-03 | URS-PERF-03 | OQ measures UI response of `Open Project`, `Load Method`, `Display Audit Trail` ≤ 3 s P95. |
| FS-PERF-04 | URS-PERF-04 | Availability tracked via Splunk `wel-lcms-availability` dashboard (workstation up + MassLynx service running). |

### 4.10 Security (M-SEC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SEC-01 | URS-SEC-01 | All accounts AD; break-glass `acme\bg-admin` documented under quarterly review. |
| FS-SEC-02 | URS-SEC-02 | Site InfoSec policy `ACME-IS-POL-PASSWORD` enforced via GPO; 14-char minimum, 90-day rotation, history 24, complexity ON. |
| FS-SEC-03 | URS-SEC-03 | GPO `Block-RemovableMedia` denies USB mass-storage class; engineering override granted only via signed change request `ACME-CR-IT-USB-LCMS`. |
| FS-SEC-04 | URS-SEC-04 | CrowdStrike Falcon Sensor daily definition update; compliance dashboard `wel-lcms-av`. |
| FS-SEC-05 | URS-SEC-05 | GPO `GMP-Firewall` deploys site GMP-segment ruleset (deny inbound except management subnet; deny outbound except whitelisted endpoints). |

### 4.11 Training (M-TRN)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Cornerstone curriculum `ACME-CURR-LCMS-Analyst-v1` mandatory before AD group `Lab-LCMS-Analysts` membership; LMS-API-driven gate. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher curriculum auto-assigned via Cornerstone; LMS reports overdue trainees and prompts AD-group revocation. |

### 4.12 Periodic Review (M-PR)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PR-01 | URS-PR-01 | Periodic-review report template `ACME-PR-LCMS-YYYYMMDD`; covers all URS § 5.12 items (configuration drift, audit-trail review evidence, deviations / CRs, backup-restore evidence, training currency, fitness for use). |
| FS-PR-02 | URS-PR-02 | QC Manager + QA Manager signatures on the periodic-review report (eSign with Part 11 meaning `Approve`). |

### 4.13 System Suitability Test per USP <621> (M-SST)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SST-01 | URS-SST-01 | TargetLynx XS SST evaluator computes per-method USP <621> parameters: resolution (R), tailing factor (Tf), theoretical plates (N), retention-time RSD, peak-area RSD on replicate injections (n=5). Parameter thresholds method-bound; verified by `OQ-SST-USP621-01`. |
| FS-SST-02 | URS-SST-02 | TargetLynx blocks downstream `.PRO` generation when SST verdict == FAIL; sequence flagged `SST-FAILED`; user must re-run SST after corrective action documented via reason-for-change. |
| FS-SST-03 | URS-SST-03 | SST record schema: method-id, criteria thresholds, observed values per replicate, pass/fail per parameter, overall verdict, evaluator-id (TargetLynx version), SHA-256 cryptographic reference to the sequence-id. |
| FS-SST-04 | URS-SST-04 | Bracketed-SST mode: TargetLynx schedules SST at sequence start AND end for sequences ≥ 30 injections; bracket-end failure flips all bracketed results to status `SUSPECT — END-SST-FAILED` pending investigation. |
| FS-SST-05 | URS-SST-05 | Carryover injection scheduled after the highest standard; TargetLynx computes carryover-peak-area / LOQ-peak-area ratio; ratio > 0.2% triggers fail per USP <621>. |

### 4.14 Mass Calibration and Tune Management (M-CAL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CAL-01 | URS-CAL-01 | MassLynx maintains the Xevo TQ-S calibration record: daily lock-mass check (leucine-enkephalin reference, m/z 556.2771); weekly mass calibration (NaI reference); monthly full source-tune. Calibration record bound to subsequent runs via the calibration-record-id field. |
| FS-CAL-02 | URS-CAL-02 | MassLynx pre-run macro checks calibration expiry against method-specified validity window; expired calibration blocks acquisition with dialog `Mass calibration expired — re-tune required`. |
| FS-CAL-03 | URS-CAL-03 | Source-tune parameters (capillary voltage, cone voltage, source T, desolvation T, desolvation gas flow) loaded from the method; deviation > 5% triggers Method-Owner-override workflow with reason capture. |
| FS-CAL-04 | URS-CAL-04 | Instrument-PM events recorded via maintenance-log feature; flag bit `PM_PENDING_TUNE_VERIFICATION` blocks GxP runs until a fresh tune + SST passes. |

### 4.15 Calibration Curve and Quantitation (M-QNT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-QNT-01 | URS-QNT-01 | TargetLynx XS calibration-curve engine constructs the curve from method-specified standards (≥ 6 non-zero levels for quantitative assay; ≥ 5 for related-substances). r² computed automatically; r² < 0.99 fails the run for quantitative assay. |
| FS-QNT-02 | URS-QNT-02 | TargetLynx outlier-flagging rule: per-standard back-calculation outside ± 15% nominal (± 20% at LOQ) raises `STANDARD_OUTLIER` flag; exclusion requires Method-Owner eSign with reason captured. |
| FS-QNT-03 | URS-QNT-03 | Method has a `MatrixType` enum (`drug-product`, `API`, `stability`, `dissolution`); sequence-start validator rejects when sample matrix tag ≠ method matrix tag. |
| FS-QNT-04 | URS-QNT-04 | TargetLynx computes result via the method-bound equation set in IEEE-754 double precision; rounding applied only at final-report generation per site SOP `SOP-QC-CHROM-ROUND-001`. |
| FS-QNT-05 | URS-QNT-05 | Three configured limit thresholds per analyte (30%, 50%, 100% of specification) trigger TargetLynx flags `TREND` / `OOT` / `OOS`; flags propagate to LIMS payload. |

### 4.16 Method Lifecycle, Reprocessing, Report Re-issue (M-MTH)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MTH-01 | URS-MTH-01 | TargetLynx method-state machine: DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE; only EFFECTIVE permitted at sequence start; verified by `OQ-MTH-LIFECYCLE-01`. |
| FS-MTH-02 | URS-MTH-02 | Method state-transition eSign requires Author ≠ Reviewer ≠ Approver (enforced at the MassLynx user-role layer); method history retained as immutable audit-trail entries. |
| FS-MTH-03 | URS-MTH-03 | Reprocessing creates a new `.PRO` artefact pointing to the original `.RAW` and the new processing-method version; UI prevents re-acquisition under a different method-id without explicit deviation record. |
| FS-MTH-04 | URS-MTH-04 | TargetLynx compares the reprocessed result to the previously approved result; difference > 0% triggers `RESULT_DIFFERS_ON_REPROCESS` flag and blocks LIMS push until deviation + Method-Owner + QC-Manager dual eSign. |
| FS-MTH-05 | URS-MTH-05 | Method-version-migration policy: in-flight sequences may complete under the prior version; sequence-start UI defaults to the current EFFECTIVE version with explicit override permitted only within a 24-hour migration grace window. |

### 4.17 Mass Spectrum Library Management (M-LIB)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-LIB-01 | URS-LIB-01 | Reference MS-library `ACME-MSLIB-2026Q2` version-controlled in `acme-gmp-fs01\masslib`; updates require Method-Owner eSign + Senior-Analyst review; acceptance test (re-process 20 reference samples, match-score change ≤ ± 2% absolute) recorded as a `LibraryReleaseRecord`. |
| FS-LIB-02 | URS-LIB-02 | Every identification result carries library-id, library SHA-256 hash, per-component match-score and configured threshold. |
| FS-LIB-03 | URS-LIB-03 | Borderline identifications (match-score within ± 5% of threshold) flagged in TargetLynx UI for Senior-Analyst attention; flag persisted in result record. |
| FS-LIB-04 | URS-LIB-04 | RTDB drift check: at every column-lot change, a calibration sequence (10 reference compounds × 3 injections) is run; observed RT vs validated RT compared per compound; > 0.05 min shift triggers RTDB re-calibration before GxP use. |

### 4.18 LIMS Interface (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | Waters LIMS Connector polls LabWare LIMS 8 over `https://lims.acme.local/api/v3/worklist` every 60 s using service principal `acme\svc-masslynx-limsread` (read-only AD group); worklist cached locally + bound to sequence. |
| FS-INT-LIMS-02 | URS-INT-LIMS-02 | Approved-result push gated by MassLynx `LimsExport` flag (set only by QC Manager eSign with meaning `Approve`); payload signed with site PKI cert `acme-lcms-2026q2`; connector rejects payloads where `LimsExport == false`. |
| FS-INT-LIMS-03 | URS-INT-LIMS-03 | Payload schema `ACME-LIMS-PUSH-LCMS-v3.json` mandates `reportId, instrumentId, methodId+version, libraryId+hash, calibrationCurveId, sstRecordId, analystId, reviewerId, approverId, rawFileHash, resultHash`; LIMS rejects payloads failing schema validation. |
| FS-INT-LIMS-04 | URS-INT-LIMS-04 | Connector failure events written to Windows Application log + forwarded to Splunk; alert rule `wel-lcms-lims-failure` pages on-call after 5-min window. |


### 4.19 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: Kerberos (interactive) and LDAPS (service-account bind) on-prem. Conditional-access binding to policy `Lab-Workstation Conditional Access (MFA on interactive logon)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the Chromeleon SQL backend; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Interface Specifications

| IF ID | URS ID | Counterparty | Protocol | Direction | Notes |
|---|---|---|---|---|---|
| IF-LIMS-01 | URS-INT-LIMS-01 | LabWare LIMS 8 | HTTPS / JSON | inbound | worklist import; OAuth2 client credentials |
| IF-LIMS-02 | URS-INT-LIMS-02 | LabWare LIMS 8 | HTTPS / JSON (mTLS) | outbound | approved-result push |
| IF-AD-01 | URS-SEC-01 | AD / Kerberos | LDAPS | bidirectional | authN |
| IF-NTP-01 | URS-SW-06 | NTP `ntp.acme.local` | NTP | inbound | time sync |
| IF-SIEM-01 | URS-SW-04 | Splunk Enterprise | TCP/9997 (Universal Forwarder) | outbound | Windows + MassLynx audit-event forwarding |
| IF-FS-01 | URS-SW-03 | NetApp SnapLock `\\acme-gmp-fs01\masslynx-projects` | SMB 3.1.1 | bidirectional | project storage + WORM retention |

## 6. Data Model (high-level)

| Entity | Attributes (illustrative) |
|---|---|
| Project | project_id, name, owner, ad_role_map, policy {raw_data_lock, esign, audit, rfc} |
| Method | method_id, project_id, version, state, author, approver, matrix_type, equation_set, library_id+hash, sst_criteria |
| Sequence | sequence_id, project_id, instrument_id+serial, method_id+version, calibration_record_id, analyst_id, started_at, sst_status |
| Injection | injection_id, sequence_id, sample_id, vial_position, volume, ts |
| RawData | raw_id (file), sequence_id, sha256, immutable_at |
| ProcessedResult | result_id, raw_id, processing_method_id+version, integrated_peaks, calc_value, library_id+hash, match_scores, spec_status, approver_id |
| Report | report_id, result_id, signatures, hash, reissued_from |
| AuditEvent | event_id, scope, user_id, action, old, new, reason, ts |
| Signature | sig_id, scope, signer_id, meaning, ts, payload_hash |
| SSTRecord | sst_id, sequence_id, criteria, observed, pass_fail_per_param, verdict, evaluator_version |
| CalibrationRecord | cal_id, instrument_id, type {lockmass, mass_cal, full_tune}, performed_at, expires_at |
| LibraryReleaseRecord | lib_id, version, hash, released_at, acceptance_test_id |

## 7. Non-Functional Specifications (consolidated)

| Aspect | Target | URS reference |
|---|---|---|
| Concurrent users | 1 (single-instrument workstation) | n/a |
| Sequence size | 50 injections / sequence (OQ stress) | URS-PERF-01/02 |
| Processing time | ≤ 15 min for 50-injection sequence | URS-PERF-02 |
| UI response | ≤ 3 s P95 | URS-PERF-03 |
| Availability | ≥ 99.0% business hours | URS-PERF-04 |
| RPO / RTO | 24 h / 8 business h | URS-BAK-03/04 |
| Audit-trail retention | 7 y (25 y for batch-linked) | URS-AUD-04 |

## 8. Configuration Items

| CI ID | Item | Value | Owner |
|---|---|---|---|
| CI-01 | MassLynx "Project Root" | `\\acme-gmp-fs01\masslynx-projects` | System Administrator |
| CI-02 | MassLynx `RequireSignatureReAuth` | `true` | System Administrator |
| CI-03 | MassLynx project-policy bundle | `RawDataLock=ON; eSign=ON; Audit=ON; RFC=ON` | System Administrator |
| CI-04 | TargetLynx SST verdict block | `true` | QC Manager |
| CI-05 | Per-method calibration validity window | per method (typ. 7 d lock-mass / 14 d mass-cal / 30 d full-tune) | Method Owner |
| CI-06 | Per-analyte limit thresholds | per `ACME-CFG-LCMS-LIMITS-v1` | Method Owner |
| CI-07 | Library version | `ACME-MSLIB-2026Q2` | Method Owner |
| CI-08 | LIMS Connector OAuth client | `masslynx-lcms-limsread` | IT |
| CI-09 | NTP server | `ntp.acme.local` | IT |
| CI-10 | SIEM heavy index | `wel-lcms` | InfoSec |
| CI-11 | UPS shutdown threshold | 20% remaining | IT |
| CI-12 | RTDB column-lot drift threshold | 0.05 min | Method Owner |
| CI-13 | Calibration-curve r² floor | 0.99 (quantitative assay) | Method Owner |
| CI-14 | Carryover threshold (USP <621>) | ≤ 0.2% of LOQ peak area | Method Owner |

## 9. Risks (FS-level)

Inherited from URS § 9. Additional FS-specific risks captured during configuration:

- MassLynx SCN silent regression of TargetLynx SST evaluator → mitigation: FS-PROC-04 + FS-SST-* re-tested at every SCN upgrade per change control.
- LIMS Connector stalls and unsynced results pile up → mitigation: FS-INT-LIMS-04 alert rule with 5-min SLA.
- WORM-file-system retention metadata misapplied → mitigation: FS-AUD-04 + quarterly retention audit.
- Library hash drift (manual library file replaced outside change control) → mitigation: FS-LIB-01 + scheduled SHA-256 verification on every TargetLynx start-up.

## 10. References

- `ACME-URS-LCMS-001 v1.2` (parent URS).
- ISPE GAMP 5 (2nd Edition, 2022); ISPE GAMP GPG *Validation of Laboratory Computerized Systems*.
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192.
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- USP <621>, USP <1058>, USP <1224>-<1226>.
- ICH Q2(R2), ICH Q3A(R2), ICH Q3B(R2), ICH Q9(R1), ICH Q14.
- PIC/S PI 041.
- Waters — *MassLynx 4.2 SCN1027 Installation and Configuration Reference*.
- Waters — *TargetLynx XS Application Manager Reference*.
- Waters — *Acquity I-Class UPLC + Xevo TQ-S micro Hardware Reference + Maintenance Guide*.
- Site documents: `SOP-QC-CHROM-ROUND-001`, `SOP-QC-CHROM-INTEGRATION-002`, `ACME-IS-POL-PASSWORD`, `ACME-PROC-BAK-RESTORE-001`, `ACME-RB-LCMS-DR-001`.

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-HW-01 | FS-HW-01 |
| URS-HW-02 | FS-HW-02 |
| URS-HW-03 | FS-HW-03 |
| URS-HW-04 | FS-HW-04 |
| URS-HW-05 | FS-HW-05 |
| URS-SW-01 | FS-SW-01 |
| URS-SW-02 | FS-SW-02 |
| URS-SW-03 | FS-SW-03 |
| URS-SW-04 | FS-SW-04 |
| URS-SW-05 | FS-SW-05 |
| URS-SW-06 | FS-SW-06 |
| URS-SW-07 | FS-SW-07 |
| URS-ACQ-01 | FS-ACQ-01 |
| URS-ACQ-02 | FS-ACQ-02 |
| URS-ACQ-03 | FS-ACQ-03 |
| URS-ACQ-04 | FS-ACQ-04 |
| URS-ACQ-05 | FS-ACQ-05 |
| URS-PROC-01 | FS-PROC-01 |
| URS-PROC-02 | FS-PROC-02 |
| URS-PROC-03 | FS-PROC-03 |
| URS-PROC-04 | FS-PROC-04 |
| URS-PROC-05 | FS-PROC-05 |
| URS-PROC-06 | FS-PROC-06 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
| URS-AUD-05 | FS-AUD-05 |
| URS-PART11-01 | FS-PART11-01 |
| URS-PART11-02 | FS-PART11-02 |
| URS-PART11-03 | FS-PART11-03 |
| URS-PART11-04 | FS-PART11-04 |
| URS-PART11-05 | FS-PART11-05 |
| URS-PART11-06 | FS-PART11-06 |
| URS-PART11-07 | FS-PART11-07 |
| URS-PART11-08 | FS-PART11-08 |
| URS-PART11-09 | FS-PART11-09 |
| URS-PART11-10 | FS-PART11-10 |
| URS-PART11-11 | FS-PART11-11 |
| URS-PART11-12 | FS-PART11-12 |
| URS-PART11-13 | FS-PART11-13 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-BAK-03 | FS-BAK-03 |
| URS-BAK-04 | FS-BAK-04 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-PERF-03 | FS-PERF-03 |
| URS-PERF-04 | FS-PERF-04 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-SEC-05 | FS-SEC-05 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-PR-02 | FS-PR-02 |
| URS-SST-01 | FS-SST-01 |
| URS-SST-02 | FS-SST-02 |
| URS-SST-03 | FS-SST-03 |
| URS-SST-04 | FS-SST-04 |
| URS-SST-05 | FS-SST-05 |
| URS-CAL-01 | FS-CAL-01 |
| URS-CAL-02 | FS-CAL-02 |
| URS-CAL-03 | FS-CAL-03 |
| URS-CAL-04 | FS-CAL-04 |
| URS-QNT-01 | FS-QNT-01 |
| URS-QNT-02 | FS-QNT-02 |
| URS-QNT-03 | FS-QNT-03 |
| URS-QNT-04 | FS-QNT-04 |
| URS-QNT-05 | FS-QNT-05 |
| URS-MTH-01 | FS-MTH-01 |
| URS-MTH-02 | FS-MTH-02 |
| URS-MTH-03 | FS-MTH-03 |
| URS-MTH-04 | FS-MTH-04 |
| URS-MTH-05 | FS-MTH-05 |
| URS-LIB-01 | FS-LIB-01 |
| URS-LIB-02 | FS-LIB-02 |
| URS-LIB-03 | FS-LIB-03 |
| URS-LIB-04 | FS-LIB-04 |
| URS-INT-LIMS-01 | FS-INT-LIMS-01 |
| URS-INT-LIMS-02 | FS-INT-LIMS-02 |
| URS-INT-LIMS-03 | FS-INT-LIMS-03 |
| URS-INT-LIMS-04 | FS-INT-LIMS-04 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

The following risks are noted for downstream evaluation in the Risk Assessment `ACME-RA-LCMS-001` (synthetic):

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Loss of audit-trail integrity through unauthorised administrator action | Low | Critical | URS-AUD-02, URS-SEC-01, URS-PR-01 |
| R-02 | Calculation drift after SCN upgrade | Low | High | URS-QNT-04, change control + post-upgrade OQ verification (FDA Warning Letter precedent — Hetero Labs 2024 cited un-validated calculation changes post-CDS upgrade) |
| R-03 | Backup corruption discovered only at restore | Low | High | URS-BAK-02 (quarterly restore test) |
| R-04 | Unauthorised USB exfiltration of GxP data | Low | High | URS-SEC-03 |
| R-05 | Local administrator privilege creep | Medium | High | URS-SW-01, URS-SEC-01 |
| R-06 | Silent peak-integration manipulation (manual integration not justified) — FDA Warning Letter pattern across HPLC / LC-MS, e.g., FDA WL to Sun Pharma (2023) citing un-justified integration | Medium | Critical | URS-PROC-01, URS-AUD-01, URS-MTH-04 |
| R-07 | Retention-time shift on column-lot change leading to mis-identification | Medium | High | URS-LIB-04, URS-SST-01 |
| R-08 | Ion-source contamination causing sensitivity drift between SST and bracketed end-SST | Medium | High | URS-SST-04, URS-CAL-04 |
| R-09 | Mass-spectrum library version drift (un-controlled library updates altering identification calls) | Low | Critical | URS-LIB-01, URS-LIB-02 |
| R-10 | Calibration-curve outlier suppression without justification (single standard dropped to "fix" r²) | Medium | High | URS-QNT-02 |
| R-11 | MS-tune drift between scheduled tunes causing under-reported impurities | Low | High | URS-CAL-01, URS-CAL-02 |
| R-12 | LIMS push of unapproved or non-released results | Low | High | URS-INT-LIMS-02 |
| R-13 | Project-folder file-system corruption with silent loss of raw data | Low | Critical | URS-SW-03, URS-BAK-01, URS-BAK-02 |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
