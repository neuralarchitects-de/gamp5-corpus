---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch 2026-04-26; T2 rebuild 2026-05-13 (Chunk A ICP-MS)"
seed_corpus_basis:
  - "NWT-URS-ICPMS-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd Edition) Category 4 conventions"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300"
  - "21 CFR Part 211 §§ .68, .180, .192, .194(a)(8)"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "ICH Q3D(R2); ICH Q2(R2); ICH Q9(R1)"
  - "USP <232> / <233> / <730>; USP <1058>; USP <1224>-<1226>"
  - "PIC/S PI 041"
  - "Thermo Fisher — Qtegra ISDS 2.10 + TraceCERT + Pharma Compliance"
parent_urs:
  document_number: NWT-URS-ICPMS-001
  version: 1.2
  file: ../../URS/_generated/final/Northwind_Therapeutics_ICP-MS_Computer_System_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## ICP-MS Computer System — Thermo Fisher iCAP RQ + Qtegra ISDS 2.10

**Document Number:** NWT-FS-ICPMS-001
**Version:** 1.2
**Effective Date:** 2026-05-13 *(synthetic)*
**Parent URS:** NWT-URS-ICPMS-001 v1.2
**Site:** Northwind Therapeutics Pvt. Ltd., Quality Control Laboratory, Block C, Hinjewadi Phase II, Pune, Maharashtra, India *(fictional)*
**System Owner:** QC Manager — Trace Analytics
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192, .194(a)(8); EU GMP Annex 11 §§ 4, 6, 9, 11; ICH Q3D(R2); ICH Q2(R2); USP <232>/<233>/<730>; USP <1058>; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _______________________ | _______________________ | __________ |
| Reviewer (QC Manager — Trace Analytics) | _______________________ | _______________________ | __________ |
| Reviewer (IT / System Administrator) | _______________________ | _______________________ | __________ |
| Reviewer (Vendor — Thermo Fisher Field Service) | _______________________ | _______________________ | __________ |
| Approver (Head of Quality Assurance) | _______________________ | _______________________ | __________ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-13 | (synthetic) | T2 rebuild aligned to URS v1.2; expanded Part 11 sub-section rows; new FS sections for tune-verification per USP <730>, interference correction + internal-standard + drift monitoring, USP <233> Procedure-1/Procedure-2 calibration engine, method lifecycle, sample-prep linkage to Milestone UltraWAVE; per-URS-ID traceability matrix (no range compression). |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## Definitions and Acronyms

Defined in `NWT-URS-ICPMS-001`. Additional FS-specific terms below.

| Term | Definition |
|---|---|
| ASR | Application Server Role (Qtegra application services) |
| KED | Helium Kinetic Energy Discrimination collision-cell mode |
| Tasklet | Qtegra workflow unit (vendor-supplied, no site authoring) |
| AD-mapped Role | A Qtegra role tied to a specific Active Directory security group |
| LIMS Connector | Qtegra-side adapter that connects to LabWare LIMS 8 |

---

## 1. Purpose

This Functional Specification defines the implementation of the user, functional, regulatory, and non-functional requirements specified in the parent URS `NWT-URS-ICPMS-001`. The FS describes *how* the configured Thermo Fisher iCAP RQ + Qtegra ISDS 2.10 platform satisfies those requirements: hardware build, software install / configuration, integration patterns, data flows, and interface contracts.

Where the URS says *the system shall …*, this FS says *the configured implementation shall achieve this by …* — without re-stating the URS requirement.

## 2. Scope

This FS covers the configured Thermo Fisher iCAP RQ + Qtegra workstation and its operational interfaces (LabWare LIMS 8 LIMS Connector, AD authentication, file-server backup target, NTP, SIEM forwarder). The FS does not cover: vendor-supplied internal SDLC of Qtegra (relied on per the Thermo Fisher CSV evidence); LIMS-side configuration (separate system).

## 3. System Architecture

### 3.1 Component Inventory

| Component | Type | Vendor | Version |
|---|---|---|---|
| ICP-MS instrument | Hardware | Thermo Fisher | iCAP RQ |
| Autosampler | Hardware | Cetac | ASX-560 |
| Workstation | Hardware | Dell | Precision 3680 |
| OS | Software | Microsoft | Windows 11 Pro 22H2 (domain `NWT.local`) |
| Acquisition / Processing software | Software | Thermo Fisher | Qtegra ISDS 2.10 (build 2.10.4710.184) |
| TraceCERT plugin | Software | Thermo Fisher | TraceCERT v2.10 |
| Pharma Compliance plugin | Software | Thermo Fisher | Pharma Compliance v2.10 |
| LIMS Connector | Software | Thermo Fisher | Qtegra LIMS Connector 1.6 |
| Anti-malware | Software | CrowdStrike | Falcon Sensor (latest) |
| Barcode reader | Hardware | Honeywell | Voyager 1452g |

### 3.2 Logical Architecture (textual)

```
[Sample digestate]
     │
     ▼
[ASX-560]──── USB-3 ────►[iCAP RQ]──── USB-3 ────►[Qtegra Workstation]
                                                        │
                                                        │ Kerberos / LDAP
                                                        ▼
                                                 [AD `NWT.local`]
                                                        │
                                                        ▼
                                          [SIEM Splunk Enterprise]
                                                        │
                                                        ▼
                                       [\\nwt-gmp-fs02\qtegra-projects]
                                                        │
                                                        ▼
                                       [Qtegra LIMS Connector 1.6] ◄──► [LabWare LIMS 8]
```

### 3.3 Functional Modules

| Module | Provided by | Function |
|---|---|---|
| Acquisition Engine | Qtegra | Drives the iCAP RQ + ASX-560; captures spectra / counts. |
| Method Library | Qtegra | Stores acquisition + processing methods with version history. |
| Processing Engine | Qtegra | Applies mass-bias / IS-correction / KED / interference correction; computes final concentration. |
| Reporting Engine | Qtegra | Renders PDF analytical reports with template-driven layout + report hash. |
| Audit Trail Engine | Qtegra (Pharma Compliance) | Captures and renders the audit trail; append-only enforcement at the application + file-system level. |
| Authentication Service | Windows AD via Qtegra Pharma Compliance | Enforces user authentication and role mapping. |
| LIMS Adapter | Qtegra LIMS Connector | Pulls worklists / pushes approved results. |

---

## 4. Functional Specifications

Each FS-XX entry references the parent URS-XX requirement(s) it implements.

### 4.1 Hardware / Installation (URS §5.1)

| FS ID | Implements URS | Description |
|---|---|---|
| FS-HW-01 | URS-HW-01 | The Qtegra workstation is dedicated to a single iCAP RQ instrument; the asset register entry binds the workstation by serial to the instrument by serial. |
| FS-HW-02 | URS-HW-02 | Workstation specification meets Thermo Fisher recommendation: Dell Precision 3680, Intel Core i7-14700, 64 GB DDR5 RAM, 2 TB NVMe SSD, NVIDIA T1000, 4× USB-3.2. |
| FS-HW-03 | URS-HW-03 | The workstation is connected to UPS APC SMT3000RM2UC sized for 30-minute hold; the UPS broadcasts low-battery via SNMP to trigger Windows controlled shutdown at 20% remaining. |
| FS-HW-04 | URS-HW-04 | Workstation is on VLAN 412 (GMP-Lab); office-segment routing blocked at the firewall. |
| FS-HW-05 | URS-HW-05 | Helium / argon line pressures connected via the iCAP RQ utility-monitoring port; Qtegra reads pressures every 5 s and alarms if outside 3.5–6.5 bar (Ar) / 0.7–1.0 bar (He). |
| FS-HW-06 | URS-HW-06 | Room HVAC controlled by site BMS; viewLinc EM logs T/RH at 1-minute intervals (separate validation `EMS-CSV-2024-002`). |

### 4.2 Software Configuration (URS §5.2)

| FS ID | Implements URS | Description |
|---|---|---|
| FS-SW-01 | URS-SW-01 | Windows 11 Pro 22H2 image deployed via SCCM; domain-joined to `NWT.local`; QC users in AD group `Lab-ICPMS-Analysts`; no member of `Workstation-Admins` GPO except break-glass account `NWT\bg-admin`. |
| FS-SW-02 | URS-SW-02 | Qtegra ISDS 2.10 (build 2.10.4710.184) installed via Thermo Fisher field-service procedure `THER-FS-PROC-2024-014`; install verification per Thermo IQ checklist, signed off by Thermo engineer + site validation engineer. |
| FS-SW-03 | URS-SW-03 | Qtegra "Project root path" configured to `\\nwt-gmp-fs02\qtegra-projects`; local C:\\Qtegra cache limited to 50 GB and auto-purged after sync. |
| FS-SW-04 | URS-SW-04 | Windows audit policy `Audit Logon`, `Audit Account Management`, `Audit Object Access (\\nwt-gmp-fs02\qtegra-projects)` enabled; events forwarded to Splunk via universal forwarder (heavy index `wel-icpms`). |
| FS-SW-05 | URS-SW-05 | CrowdStrike Falcon Sensor with vendor-approved exclusion list (Qtegra installation paths, real-time-data writers); definitions auto-update daily. |
| FS-SW-06 | URS-SW-06 | Windows Time service syncs to `ntp.nwt.local`; configured skew threshold 1 second; w32time event 35/29 monitored in SIEM. |
| FS-SW-07 | URS-SW-07 | GPO `GMP-Lab-Workstations` enforces 10-minute screen-saver lock; only the AD `Lab-ICPMS-Analysts` group can interactively log on. |

### 4.3 Acquisition (URS §5.3)

| FS ID | Implements URS | Description |
|---|---|---|
| FS-ACQ-01 | URS-ACQ-01 | Qtegra "Method library" is configured read-only for AD `Lab-ICPMS-Analysts`; only `Lab-ICPMS-MethodOwners` can create/edit; method states map to Qtegra "Released" / "Draft" / "Obsolete". |
| FS-ACQ-02 | URS-ACQ-02 | Sequence-start preconditions enforced by Qtegra Pharma Compliance: instrument `Plasma Ready` state == true; method status == Released; project lock not held; helium pressure within range. Failure displays a blocking dialog and writes an audit-trail entry. |
| FS-ACQ-03 | URS-ACQ-03 | Sequence template requires fields: sample ID, vial position, dilution factor, internal-standard ID, and binds method ID/version + instrument ID + analyst (from session) + UTC timestamp at start. |
| FS-ACQ-04 | URS-ACQ-04 | Q-pass tune injection scheduled at sequence start; failure enforces "Block Results" workflow per URS-ACQ-05. |
| FS-ACQ-05 | URS-ACQ-05 | Pharma-Compliance "Block on SST Failure" feature configured; corrective action documented via the in-app Reason-for-Change dialog before SST re-run. |
| FS-ACQ-06 | URS-ACQ-06 | Pause / Resume captured as `SequenceModified` audit-trail event with reason text. |

### 4.4 Processing and Reporting (URS §5.4)

| FS ID | Implements URS | Description |
|---|---|---|
| FS-PROC-01 | URS-PROC-01 | Processing methods configured per analyte: mass-bias function, KED on/off, interference equations, internal-standard correction (typ. ⁴⁵Sc, ⁷²Ge, ¹¹⁵In, ²⁰⁹Bi). |
| FS-PROC-02 | URS-PROC-02 | "Manual reprocess" requires explicit reason-for-change recorded against the result; original processed result preserved. |
| FS-PROC-03 | URS-PROC-03 | Qtegra `RawData` artefact is read-only after acquisition; processing produces a `ProcessedResult` artefact with parent-pointer and hash. |
| FS-PROC-04 | URS-PROC-04 | Result computed in µg/g (matrix) or µg/day (dose-based); report includes ICH Q3D / USP <232> limit per analyte. |
| FS-PROC-05 | URS-PROC-05 | Three configured limit thresholds per analyte (`30%`, `50%`, `100%`) trigger Qtegra flags `TREND` / `OOT` / `OOS`. |
| FS-PROC-06 | URS-PROC-06 | Report template `NWT-RPT-ICPMS-001-v1.0.qrt` includes all URS-required fields, ALCOA+ statement, and the SHA-256 hash of the underlying `ProcessedResult` artefact. |
| FS-PROC-07 | URS-PROC-07 | "Re-issue Report" feature inserts the watermark "RE-ISSUED — supersedes <originalReportId>". |

### 4.5 Audit Trail and Records (URS §5.5)

| FS ID | Implements URS | Description |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Pharma-Compliance audit trail records: timestamp (UTC + local), actor user, action type, target artefact, old-value, new-value, reason-for-change. |
| FS-AUD-02 | URS-AUD-02 | Audit-trail tables on the Qtegra database are append-only; the Qtegra database service account has only INSERT/SELECT on those tables; OS-level file ACL on the project share denies modify/delete to all but `nwt-svc-qtegra-backup` (read-only). |
| FS-AUD-03 | URS-AUD-03 | `Audit Trail Review` report template `NWT-RPT-ICPMS-AUDIT-001` generates a printable PDF for batch and periodic reviews. |
| FS-AUD-04 | URS-AUD-04 | Project-share retention policy enforced by the file-server's WORM tier (NetApp SnapLock) for 7 years; longer retention for batch-linked projects via metadata tag `retention=25y`. |
| FS-AUD-05 | URS-AUD-05 | Read-only `Auditor` role exposes the Audit Trail Review screen; export uses the same template as periodic review. |

### 4.6 21 CFR Part 11 (URS §5.6)

| FS ID | Implements URS | Description |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a), validation dossier `NWT-VAL-ICPMS-001` (IQ + OQ + PQ + RTM + VSR + periodic review) maintained as the validation evidence. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(b), Qtegra report export produces PDF/A-3 (human-readable) + native `.qrt` artefact (electronic) for inspection. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(c), NetApp SnapLock 7-y immutable retention on `\\nwt-gmp-fs02\qtegra-projects` + Veeam daily backup with SHA-256 integrity check. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.10(d), AD-bound access via `Lab-ICPMS-*` groups; local accounts disabled except break-glass `NWT\bg-admin`. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.10(e), Qtegra Pharma-Compliance audit trail per FS-AUD-01. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.10(g), Qtegra authority sets `Analyst`, `Senior`, `MethodOwner`, `Manager`, `SysAdmin`, `Auditor` mapped to AD groups; authority checked server-side at every privileged action. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.10(k), system-operation manual `NWT-RB-ICPMS-OPS-001`; Thermo SCN releases under site change-control with impact assessment + post-upgrade OQ verification of FS-PROC-01 + FS-INTF-01. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.50, Pharma-Compliance e-signature dialog enforces collection of printed-name + dateTime + meaning-of-signature (closed list: Review / Approve / Reject / Lock); binds to artefact via SHA-256 hash. |
| FS-PART11-09 | URS-PART11-09 | Per § 11.70, signature payload includes the `ProcessedResult.hash`; subsequent edits invalidate the signature, displayed in the report as `SIGNATURE INVALID — RECORD MODIFIED`. |
| FS-PART11-10 | URS-PART11-10 | Per § 11.100, each AD account tied to unique HR record; reuse / reassignment prohibited at AD level. |
| FS-PART11-11 | URS-PART11-11 | Per § 11.200, Qtegra setting `RequireSignatureReAuth = true`; cached credentials not honoured at sign-off. |
| FS-PART11-12 | URS-PART11-12 | Per § 11.300, AD GPO `Default Domain Policy`: 5 failures / 15-min window / 30-min lockout; SIEM `wel-icpms` alerts on lockout events. |
| FS-PART11-13 | URS-PART11-13 | Pharma-Compliance role-matrix denies the same user holding both `Analyst` and `Reviewer` / `Approver` permissions on the same project; verified by `OQ-PART11-SOD-01`. |

### 4.7 Data Integrity (URS §5.7)

| FS ID | Implements URS | Description |
|---|---|---|
| FS-DI-01 | URS-DI-01 | Every Qtegra artefact carries the AD account that created/modified it. |
| FS-DI-02 | URS-DI-02 | Pharma-Compliance PDF export embeds fonts and complies with PDF/A-3. |
| FS-DI-03 | URS-DI-03 | Retrospective entries flagged in the audit trail with `originalEventTimestamp` ≠ `recordedTimestamp`. |
| FS-DI-04 | URS-DI-04 | RawData artefact is hash-bound on close-of-acquisition. |
| FS-DI-05 | URS-DI-05 | Calculation regression suite (10 reference samples × 4 elements) re-runs at OQ; results compared to the validated calculation spreadsheet. |
| FS-DI-06 | URS-DI-06 | NetApp SnapLock retention metadata; project-share availability target 99.5%. |

### 4.8 LIMS Interface (URS §5.8)

| FS ID | Implements URS | Description |
|---|---|---|
| FS-INT-01 | URS-INT-01 | Qtegra LIMS Connector polls LabWare LIMS 8 over `https://lims.nwt.local/api/v3/worklist` every 60 s using service account `NWT\\svc-qtegra-limsread` (read-only AD group). |
| FS-INT-02 | URS-INT-02 | Approved-result push gated by Qtegra `LimsExport` flag set only by `QC-Manager` role; payload signed with site PKI cert `nwt-icpms-2026q2`. |
| FS-INT-03 | URS-INT-03 | Result payload schema `NWT-LIMS-PUSH-v3.json` mandates reportId, instrumentId, methodId+version, reviewerId, approverId; LIMS rejects payloads failing schema validation. |
| FS-INT-04 | URS-INT-04 | Connector failure events written to the Windows Application log and forwarded to Splunk; alert rule `wel-icpms-lims-failure` pages on-call after 5-minute window. |

### 4.9 Backup and Recovery (URS §5.9)

| FS ID | Implements URS | Description |
|---|---|---|
| FS-BAK-01 | URS-BAK-01 | Veeam B&R 12.1 backup job `qtegra-projects-daily` runs nightly at 02:00 UTC; SHA-256 verification on each backup. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore test scripted via Veeam SureBackup; test plan `NWT-PROC-BAK-RESTORE-001`; QC witness sign-off on restore-test report. |
| FS-BAK-03 | URS-BAK-03 | Documented hardware-replacement-and-software-reinstall runbook `NWT-RB-ICPMS-DR-001`. |
| FS-BAK-04 | URS-BAK-04 | RPO of 24 h achieved by daily backup; RPO calculation documented in DR plan. |

### 4.10 Performance, Security, Training, Periodic Review (URS §5.10–5.13)

| FS ID | Implements URS | Description |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | OQ stress-test sequence of 60 injections demonstrates no crash / no data loss; Qtegra log retained as evidence. |
| FS-PERF-02 | URS-PERF-02 | Processing benchmark: 60-injection sequence ≤ 10 minutes on the specified hardware. |
| FS-PERF-03 | URS-PERF-03 | OQ measures UI response of `Open Project`, `Load Method`, `Display Audit Trail`. |
| FS-PERF-04 | URS-PERF-04 | Availability tracked via Splunk `wel-icpms-availability` dashboard (workstation up + Qtegra service running). |
| FS-SEC-01 | URS-SEC-01 | All accounts AD; break-glass `NWT\bg-admin` documented under quarterly review. |
| FS-SEC-02 | URS-SEC-02 | Site Information Security policy `NWT-IS-POL-PASSWORD` enforced via GPO. |
| FS-SEC-03 | URS-SEC-03 | GPO `Block-RemovableMedia` denies USB mass-storage; engineering override granted via change request `NWT-CR-IT-USB`. |
| FS-SEC-04 | URS-SEC-04 | CrowdStrike daily definition update; compliance dashboard `wel-icpms-av`. |
| FS-SEC-05 | URS-SEC-05 | GPO `GMP-Firewall` deploys site GMP-segment ruleset. |
| FS-TRN-01 | URS-TRN-01 | Cornerstone curriculum `NWT-CURR-ICPMS-Analyst-v1` mandatory before AD group `Lab-ICPMS-Analysts` membership. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher curriculum auto-assigned via Cornerstone. |
| FS-PR-01 | URS-PR-01 | Periodic review report `NWT-PR-ICPMS-YYYYMMDD` template; covers all URS §5.13 items. |
| FS-PR-02 | URS-PR-02 | QC Manager + QA Manager signature on the periodic-review report. |

### 4.11 System Suitability and Tune Verification (URS §5.14)

| FS ID | Implements URS | Description |
|---|---|---|
| FS-SST-01 | URS-SST-01 | TuneCheck injection scheduled at sequence start; Qtegra computes per-element sensitivity (cps for ¹¹⁵In or ²⁰⁹Bi), oxide ratio CeO⁺/Ce⁺, doubly-charged Ba²⁺/Ba⁺; method-bound thresholds (typ. CeO/Ce ≤ 3%; Ba²⁺/Ba⁺ ≤ 3%; ¹¹⁵In ≥ 50,000 cps). |
| FS-SST-02 | URS-SST-02 | Tune verification record persisted with observed values, criteria, pass/fail per parameter, verdict, cryptographic reference to sequence-id; verdict=FAIL blocks acquisition until corrective action + reason captured. |
| FS-SST-03 | URS-SST-03 | Bracketed tune-check mode for sequences ≥ 60 injections; bracket-end tune-check failure flags bracketed results as `SUSPECT — END-TUNE-FAILED`. |
| FS-SST-04 | URS-SST-04 | USP <233> Drift Control Standard (DCS) injection scheduled at start + end of analytical run; DCS observed concentration outside ± 20% of expected blocks release. |

### 4.12 Interference Correction, Internal Standards, and Drift Monitoring (URS §5.15)

| FS ID | Implements URS | Description |
|---|---|---|
| FS-INTF-01 | URS-INTF-01 | Method-bound interference-equation table (e.g., ⁵⁶Fe-corrected = ⁵⁶Fe-raw – k×⁴⁰Ar¹⁶O⁺; k value method-bound); equation-set version-controlled; mismatch blocks acquisition. |
| FS-INTF-02 | URS-INTF-02 | KED helium-mode flag is method-bound per analyte; sequence-start validator rejects when method demands KED but plasma not in KED mode. |
| FS-INTF-03 | URS-INTF-03 | Per-analyte internal-standard table (⁴⁵Sc, ⁷²Ge, ¹¹⁵In, ²⁰⁹Bi by mass-range); Qtegra computes IS ion-ratio per injection vs initial calibration; deviation > 30% raises `IS_DRIFT` flag on the sample. |
| FS-INTF-04 | URS-INTF-04 | Drift-QC injection scheduled every 10 samples; observed-vs-nominal outside ± 20% triggers `DRIFT_FAIL` flag; batch rejected or bracket-recalibrated per USP <233>. |
| FS-INTF-05 | URS-INTF-05 | Matrix-effect check: dilution series (1×, 2×, 4×) run per matrix; observed-concentration deviation > 25% on dilution flags the method for Method-Owner review. |

### 4.13 Calibration Curve and Quantitation (URS §5.16)

| FS ID | Implements URS | Description |
|---|---|---|
| FS-QNT-01 | URS-QNT-01 | Qtegra Procedure-1 (quantitative) curve engine: ≥ 3 standards per analyte; r² ≥ 0.99 evaluated automatically; failure flagged. |
| FS-QNT-02 | URS-QNT-02 | Qtegra Procedure-2 (limit-test) engine compares sample peak-area vs single standard at the Q3D PDE limit; sample > standard sets flag `EXCEEDS_LIMIT`. |
| FS-QNT-03 | URS-QNT-03 | Per-standard back-calculation outside ± 15% raises `STANDARD_OUTLIER`; exclusion requires Method-Owner eSign + reason captured. |
| FS-QNT-04 | URS-QNT-04 | Method record carries `RouteOfAdministration ∈ {oral, parenteral, inhalation}`; Q3D PDE-limit table selected accordingly; mis-selection at method-build blocked. |
| FS-QNT-05 | URS-QNT-05 | Three configured thresholds per analyte (30%, 50%, 100% of PDE) trigger `TREND` / `OOT` / `OOS` flags; flags propagated to LIMS push. |

### 4.14 Method Lifecycle and Reprocessing (URS §5.17)

| FS ID | Implements URS | Description |
|---|---|---|
| FS-MTH-01 | URS-MTH-01 | Qtegra method state machine: DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE; only EFFECTIVE permitted at sequence start. |
| FS-MTH-02 | URS-MTH-02 | State-transition eSign with Author ≠ Reviewer ≠ Approver enforced server-side; history retained as immutable audit-trail. |
| FS-MTH-03 | URS-MTH-03 | Reprocessing creates a new `ProcessedResult` artefact with `parent_result_id` referring to the original `RawData`; lineage retained. |
| FS-MTH-04 | URS-MTH-04 | Method record schema includes `interference_equation_set_id`, `internal_standard_table_id`, `calibration_standard_inventory_id`; all version-controlled. |

### 4.15 Sample Preparation Linkage (URS §5.18)

| FS ID | Implements URS | Description |
|---|---|---|
| FS-PREP-01 | URS-PREP-01 | Sequence-start validator requires `digestion_batch_id` field; missing reference blocks run; reference is FK to the Milestone UltraWAVE batch system. |
| FS-PREP-02 | URS-PREP-02 | Dilution factor captured per sample; computed concentration applies dilution factor at the equation step (not at the result-display step); IEEE-754 double precision preserved. |
| FS-PREP-03 | URS-PREP-03 | Sample-prep deviation flag `prep_deviation ∈ {none, digestion_incomplete, transfer_loss, dilution_mismatch}`; non-`none` value propagates to result + LIMS payload. |

---


### 4.16 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem. Conditional-access binding to policy `Lab-Workstation Conditional Access (MFA on interactive logon)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the ICP-MS data system DB; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Interface Specifications

### 5.1 IF-LIMS-WORKLIST-IN

- **Purpose:** Consume LabWare LIMS 8 worklist for a specified project / date.
- **Direction:** LIMS → Qtegra
- **Protocol:** HTTPS, GET, JSON
- **Endpoint:** `https://lims.nwt.local/api/v3/worklist?projectId=<id>&fromDate=<iso8601>`
- **Auth:** OAuth2 client-credential, service principal `NWT\\svc-qtegra-limsread`
- **Schema:** LabWare LIMS 8 default worklist v3
- **Rate:** Poll every 60 s

### 5.2 IF-LIMS-RESULT-OUT

- **Purpose:** Push approved analytical results to LabWare LIMS 8.
- **Direction:** Qtegra → LIMS
- **Protocol:** HTTPS, POST, JSON, mTLS
- **Endpoint:** `https://lims.nwt.local/api/v3/result`
- **Auth:** mTLS, client cert `nwt-icpms-2026q2`
- **Schema:** `NWT-LIMS-PUSH-v3.json`
- **Idempotency:** `reportId` is idempotency key

### 5.3 IF-AD-AUTH

- **Purpose:** Authenticate / authorise Qtegra users.
- **Direction:** Qtegra → AD `NWT.local`
- **Protocol:** Kerberos / LDAPS
- **Configured groups:** `Lab-ICPMS-Analysts`, `Lab-ICPMS-Senior`, `Lab-ICPMS-MethodOwners`, `Lab-ICPMS-Manager`, `Lab-ICPMS-Auditor`

---

## 6. Data Model (high-level)

| Entity | Description | Key fields |
|---|---|---|
| Project | Container of methods + sequences + results | id, name, owner, status |
| Method | Acquisition or processing method | id, version, status, owner |
| Sequence | An ordered set of injections | id, projectId, methodId+version, instrumentId, analyst |
| RawData | Acquired raw spectra | id, sequenceId, hash, immutable |
| ProcessedResult | Calculated values from RawData | id, rawDataId, methodId+version, hash |
| Report | Rendered PDF report | id, processedResultId, signatures, hash |
| Signature | E-signature record | id, recordId, signerId, meaning, timestamp |
| AuditEvent | Append-only audit-trail entry | id, timestamp, actor, action, oldValue, newValue, reason |

---

## 7. Non-Functional Specifications (consolidated)

| Aspect | Target | URS reference |
|---|---|---|
| Concurrent users | up to 4 (single-instrument workstation) | n/a |
| Sequence size | 60 injections / sequence | URS-PERF-01/02 |
| Processing time | ≤ 10 min for 60-injection sequence | URS-PERF-02 |
| UI response | ≤ 3 s P95 | URS-PERF-03 |
| Availability | ≥ 99.0% business hours | URS-PERF-04 |
| RPO / RTO | 24 h / 8 business h | URS-BAK-03/04 |
| Audit-trail retention | ≥ 7 y; 25 y for batch-linked | URS-AUD-04 |

---

## 8. Configuration Items

| CI ID | Item | Value | Owner |
|---|---|---|---|
| CI-01 | Qtegra "Project root path" | `\\\\nwt-gmp-fs02\\qtegra-projects` | System Administrator |
| CI-02 | Pharma-Compliance "RequireSignatureReAuth" | `true` | System Administrator |
| CI-03 | Pharma-Compliance "BlockOnSstFailure" | `true` | QC Manager |
| CI-04 | Limit thresholds (per-analyte) | per `NWT-CFG-ICPMS-LIMITS-v1` | Method Owner |
| CI-05 | LIMS Connector OAuth client | `qtegra-icpms-limsread` | IT |
| CI-06 | NTP server | `ntp.nwt.local` | IT |
| CI-07 | SIEM heavy index | `wel-icpms` | InfoSec |
| CI-08 | UPS shutdown threshold | 20% remaining | IT |

---

## 9. Constraints / Assumptions / Risks

Inherited from `NWT-URS-ICPMS-001` §7–§9. FS-specific risks added during configuration:

| Risk | Mitigation reference |
|---|---|
| Qtegra silent SCN update changes calculation behaviour | FS-PROC-01 + FS-PROC-05 retested at SCN upgrade per change control |
| LIMS Connector stalls and unsynced results pile up | FS-INT-04 alert rule |
| WORM file-system retention misapplied | FS-AUD-04 + quarterly retention audit |

## 10. References

- `NWT-URS-ICPMS-001 v1.0` (parent URS)
- ISPE GAMP 5 (2nd ed., 2022)
- 21 CFR Part 11; EU GMP Annex 11; ICH Q3D; USP <232>/<233>; PIC/S PI 041
- Thermo Fisher Scientific — *Qtegra ISDS 2.10 Installation and Configuration Reference*
- Site documents: `NWT-IS-POL-PASSWORD`, `NWT-PROC-BAK-RESTORE-001`, `NWT-RB-ICPMS-DR-001`

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-HW-01 | FS-HW-01 |
| URS-HW-02 | FS-HW-02 |
| URS-HW-03 | FS-HW-03 |
| URS-HW-04 | FS-HW-04 |
| URS-HW-05 | FS-HW-05 |
| URS-HW-06 | FS-HW-06 |
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
| URS-ACQ-06 | FS-ACQ-06 |
| URS-PROC-01 | FS-PROC-01 |
| URS-PROC-02 | FS-PROC-02 |
| URS-PROC-03 | FS-PROC-03 |
| URS-PROC-04 | FS-PROC-04 |
| URS-PROC-05 | FS-PROC-05 |
| URS-PROC-06 | FS-PROC-06 |
| URS-PROC-07 | FS-PROC-07 |
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
| URS-INT-01 | FS-INT-01 |
| URS-INT-02 | FS-INT-02 |
| URS-INT-03 | FS-INT-03 |
| URS-INT-04 | FS-INT-04 |
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
| URS-INTF-01 | FS-INTF-01 |
| URS-INTF-02 | FS-INTF-02 |
| URS-INTF-03 | FS-INTF-03 |
| URS-INTF-04 | FS-INTF-04 |
| URS-INTF-05 | FS-INTF-05 |
| URS-QNT-01 | FS-QNT-01 |
| URS-QNT-02 | FS-QNT-02 |
| URS-QNT-03 | FS-QNT-03 |
| URS-QNT-04 | FS-QNT-04 |
| URS-QNT-05 | FS-QNT-05 |
| URS-MTH-01 | FS-MTH-01 |
| URS-MTH-02 | FS-MTH-02 |
| URS-MTH-03 | FS-MTH-03 |
| URS-MTH-04 | FS-MTH-04 |
| URS-PREP-01 | FS-PREP-01 |
| URS-PREP-02 | FS-PREP-02 |
| URS-PREP-03 | FS-PREP-03 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Mass-calibration drift causing under-reported elemental impurities (Q3D-relevant) | Medium | Critical | URS-ACQ-04, URS-ACQ-05, URS-SST-01, daily tune-verification |
| R-02 | LIMS push of unapproved results | Low | High | URS-INT-02 |
| R-03 | Loss of audit-trail integrity through admin action | Low | Critical | URS-AUD-02, URS-SEC-01, URS-PR-01 |
| R-04 | Backup corruption discovered only at restore | Low | High | URS-BAK-02 (quarterly restore test) |
| R-05 | Argon supply interruption mid-sequence | Medium | Medium | URS-HW-05, URS-ACQ-02 |
| R-06 | Polyatomic-interference mis-correction (incorrect equation-set version, or KED disabled where mandated) | Medium | Critical | URS-INTF-01, URS-INTF-02 |
| R-07 | Internal-standard drift causing under-/over-reported concentrations | Medium | High | URS-INTF-03 |
| R-08 | Calibration-curve outlier suppression (single standard silently dropped to "fix" r²) — FDA WL pattern in chromatography also applies in ICP-MS | Medium | High | URS-QNT-03 |
| R-09 | Plasma instability mid-sequence (RF generator drift, sample-cone deposition) causing sensitivity loss | Medium | High | URS-INTF-04 (drift QC every 10 samples) |
| R-10 | Oxide / doubly-charged-ion ratio drift between scheduled tunes → polyatomic interference under-corrected | Low | High | URS-SST-01, URS-SST-03 |
| R-11 | ICH Q3D PDE limit mis-application (wrong route-of-administration selected → wrong limit) | Low | Critical | URS-QNT-04 |
| R-12 | Reprocessing replaces approved result without lineage / dual-eSign | Low | High | URS-MTH-03 |

These risks are formally evaluated in `NWT-RA-ICPMS-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
