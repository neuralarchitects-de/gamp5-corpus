---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring 2026-04-27; T2 rebuild 2026-05-13 (Chunk A Empower)"
seed_corpus_basis:
  - "EQX-URS-EMPOWER-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd ed.) Cat 4 conventions for CDS instrument suites"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300"
  - "21 CFR Part 211 §§ .68, .180, .192, .194(a)(8)"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "USP <621>; USP <1058>; USP <1224>-<1226>"
  - "ICH Q2(R2); ICH Q9(R1); ICH Q14"
  - "Waters — Empower 3 FR5 + Empower-LIMS Connector 4.2"
parent_urs:
  document_number: EQX-URS-EMPOWER-001
  version: 1.2
  file: ../../URS/_generated/final/HPLC_CDS_Empower_Computer_System__Equinox_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## HPLC Chromatography Data System — Waters Empower 3 FR5 (Networked, Citrix-published)

**Document Number:** EQX-FS-EMPOWER-001
**Version:** 1.2
**Effective Date:** 2026-05-13 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Parent URS:** EQX-URS-EMPOWER-001 v1.2
**Site:** Equinox Pharma GmbH, QC HPLC Cluster, Stuttgart, Germany *(fictional)*
**System Owner:** QC Manager — Chromatography
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192, .194(a)(8); EU GMP Annex 11 §§ 4, 6, 9, 11; USP <621>; USP <1058>; ICH Q2(R2); PIC/S PI 041

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Chromatography) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue, derived from EQX-URS-EMPOWER-001 v1.0. |
| 1.2 | 2026-05-13 | (synthetic) | T2 rebuild aligned to URS v1.2; per-URS-ID row expansion (no range compression for PART11 / AUD / DI); new §§ for Empower project hierarchy, SST, calibration-curve, reprocessing, federation, method-lifecycle, release-workflow, expanded LIMS interface schema. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## Definitions

Inherited from EQX-URS-EMPOWER-001. Additional FS-specific terms:

| Term | Definition |
|---|---|
| FS | Functional Specification (this document) |
| Project Policy | Empower's per-project security / audit / eSign policy bundle |
| Reason-for-Change | Empower's mandatory captured rationale on data change |
| SCN | Service / Control Notification (Waters patch / hot-fix) |
| eSign | Empower's electronic-signature feature |

---

## 1. Purpose

This FS specifies the deployment, configuration, and integration of Empower 3 FR5 (networked, Citrix-published) to satisfy `EQX-URS-EMPOWER-001` v1.0. Controlling input to `EQX-CS-EMPOWER-001`, `EQX-RA-EMPOWER-001`, IQ/OQ/PQ, and `EQX-RTM-EMPOWER-001`.

## 2. Scope

Mirrors the URS: Empower 3 FR5 server cluster (active + DR cold), 24 LAC/E acquisition nodes, Citrix-published client to thin-clients, AD on `equinox.local`, Empower-LIMS Connector 4.2 to LabWare LIMS 8, daily backup, NTP sync. Out: physical instruments + detectors (instrument-level qualifications); LIMS sample-lifecycle.

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source / Vendor | Notes |
|---|---|---|---|---|---|
| C-01 | Empower 3 FR5 Database Server | COTS app | 4 | Waters | Win Server 2022 + Oracle 19c |
| C-02 | Empower 3 FR5 Application Server | COTS app | 4 | Waters | active |
| C-03 | Empower 3 FR5 DR Server (cold) | COTS app | 4 | Waters | restore-time replica |
| C-04 | LAC/E nodes (×24) | COTS HW + app | 4 | Waters | one per instrument bench |
| C-05 | Citrix Virtual Apps server | COTS infra | (infra) | Citrix | publishes Empower client |
| C-06 | Empower-LIMS Connector 4.2 | COTS adapter | 4 | Waters / LabWare | bidirectional |
| C-07 | AD / Kerberos | COTS infra | (infra) | Microsoft | AuthN |
| C-08 | NTP infra | COTS infra | (infra) | (site) | time sync |
| C-09 | LabWare LIMS 8 | COTS app | 4 | LabWare | counterparty |

### 3.2 Logical Architecture (textual)

```
                        ┌──────────────────────────────────────┐
                        │   AD / Kerberos    │   NTP            │
                        └────────────┬───────────────┬──────────┘
                                     │               │
   ┌─────────────────────────────────▼───────────────▼──────────────────┐
   │                  Empower 3 FR5 (Equinox Pharma)                    │
   │   ┌────────────────┐  ┌────────────────────┐  ┌──────────────┐    │
   │   │ DB Server      │  │ App Server         │  │ DR Server    │    │
   │   │ (Oracle 19c)   │  │ (Empower core)     │  │ (cold)       │    │
   │   └────────┬───────┘  └─────────┬──────────┘  └──────────────┘    │
   │            │                    │                                  │
   │   ┌────────▼────────────────────▼────────────────────────────┐    │
   │   │           24 × LAC/E acquisition nodes                    │    │
   │   └────────────────────────────────────────────────────────────┘    │
   │   ┌──────────────────────────────────────────────────────────┐    │
   │   │  Citrix Virtual Apps server (Empower client published)    │    │
   │   └──────────────────────────────────────────────────────────┘    │
   └──────────────────────┬─────────────────────────────────────────────┘
                          │ Empower-LIMS Connector 4.2 (REST)
                          ▼
                    LabWare LIMS 8
```

### 3.3 Functional Modules

| Module | URS sections |
|---|---|
| M-PLAT | URS-PLAT-* |
| M-SW | URS-SW-* |
| M-ACQ | URS-ACQ-*, URS-PROC-* |
| M-AUD | URS-AUD-*, URS-PART11-* |
| M-DI | URS-DI-* |
| M-INT | URS-INT-* |
| M-PERF | URS-PERF-*, URS-AV-*, URS-BAK-* |
| M-SEC | URS-SEC-* |
| M-TRN | URS-TRN-* |
| M-PR | URS-PR-* |

---

## 4. Functional Specifications

### 4.1 Platform / Hardware (M-PLAT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | Active production cluster + cold DR replica restored from nightly backup; RPO ≤ 15 min via continuous archived redo logs; RTO ≤ 4 h; tested annually. |
| FS-PLAT-02 | URS-PLAT-02 | Each LAC/E on UPS sized for ≥ 30 min controlled shutdown; instruments fail-safe to safe state on power loss. |
| FS-PLAT-03 | URS-PLAT-03 | Lab-IT VLAN; no office-network route; firewall-rule audit annually. |

### 4.2 Software Configuration (M-SW)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SW-01 | URS-SW-01 | Installation by Waters or Waters-trained engineer per the IQ runbook; SCN updates managed under change control with an impact assessment before application. |
| FS-SW-02 | URS-SW-02 | Projects organised per product / programme; per-project access controlled via AD-mapped roles. Role-mapping table version-controlled. |
| FS-SW-03 | URS-SW-03 | All GxP projects have project-policy applied: Raw Data Lock = ON; eSign = ON; Audit-Trail-Required = ON; Reason-for-Change = ON; verified by `OQ-PROJECT-POLICY-01`. |
| FS-SW-04 | URS-SW-04 | Servers and LAC/Es synced to `ntp.equinox.local`; skew alert > 1 s. |
| FS-SW-05 | URS-SW-05 | Citrix-published Empower client at fixed version; user profiles non-persistent; configuration drift on the published image triggers re-validation. |

### 4.3 Acquisition / Processing (M-ACQ)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ACQ-01 | URS-ACQ-01 | Method state machine {DRAFT, REVIEW, APPROVED, EFFECTIVE, OBSOLETE}; only EFFECTIVE methods may be selected at sequence start. |
| FS-ACQ-02 | URS-ACQ-02 | Sequence-start validator rejects when any of: instrument not Ready; no approved method; project locked. Rejection reason surfaced to analyst. |
| FS-ACQ-03 | URS-ACQ-03 | Per-injection metadata captured: sample-ID, vial position, injection volume, method-id + version, instrument-id, analyst, timestamp (PLC-side LAC/E clock + NTP-synced server clock). |
| FS-ACQ-04 | URS-ACQ-04 | System-suitability evaluation per USP <621> at sequence start (resolution, tailing, theoretical plates, RSD); SST failure blocks results acceptance and routes the sequence to a "SST-failed" status; verified by `OQ-SST-01`. |
| FS-PROC-01 | URS-PROC-01 | Approved processing method auto-applied to sequence results; method changes are project-policy-gated. |
| FS-PROC-02 | URS-PROC-02 | Manual reintegration / calibration re-fit triggers Empower's reason-for-change capture; entry without reason rejected; verified by `OQ-REINTEGRATE-REASON-01`. |
| FS-PROC-03 | URS-PROC-03 | Raw Data Lock = ON for all GxP projects; verified by `OQ-RAW-DATA-LOCK-01`. |
| FS-PROC-04 | URS-PROC-04 | Spec-comparison rule flags results at 30% / 50% / 100% of limit per the configured spec-set; flags surfaced on the result view. |
| FS-PROC-05 | URS-PROC-05 | PDF report template includes chromatogram, integrated peaks, calibration curve, calculated values, ALCOA+ statement, SHA-256 hash of source data; report stored alongside the result. |

### 4.4 Audit Trail (M-AUD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Empower audit trail enabled at project / sample / method / integration / calibration / sign-off / result-modification level; per-action schema: timestamp(UTC+local), actor user-id, action type, target artefact, old value, new value, reason-for-change. |
| FS-AUD-02 | URS-AUD-02 | Audit-trail tables in Oracle have UPDATE / DELETE GRANT denied to every role; the system-administrator role does not include audit-edit privilege; verified by `OQ-AUD-APPENDONLY-01`. |
| FS-AUD-03 | URS-AUD-03 | Senior Analyst signs per-batch audit-trail review (event-driven); QC Manager signs monthly audit-trail review (periodic); review evidence stored as eSigned PDF in the project dossier. |
| FS-AUD-04 | URS-AUD-04 | Retention ≥ 7 years (general) / ≥ 25 years (release-linked) enforced via the data-retention runbook + Oracle archive policy; immutable cold-storage backups. |
| FS-AUD-05 | URS-AUD-05 | Audit-trail export feature (per-project, per-date, per-user); produces PDF/A-3 + signed CSV without disrupting routine acquisition. |

### 4.5 21 CFR Part 11 (M-PART11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Validation evidence per § 11.10(a) maintained in dossier `EQX-VAL-EMPOWER-001`: IQ + OQ + PQ + RTM + VSR + periodic-review records. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(b), all records exportable as PDF/A-3 + Empower native `.eax` (project archive); copy fidelity verified at OQ. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(c), Oracle PITR + continuous archived redo logs + WORM immutable cold storage; integrity verified by quarterly restore test (FS-BAK-02). |
| FS-PART11-04 | URS-PART11-04 | Per § 11.10(d), all access AD-bound via `Lab-Empower-*` AD groups; no local Empower accounts other than break-glass admin (subject to quarterly access review). |
| FS-PART11-05 | URS-PART11-05 | Per § 11.10(e), operational audit trail per FS-AUD-01. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.10(g), Empower authority sets `Analyst`, `Senior`, `MethodOwner`, `QCManager`, `Approver`, `SysAdmin`, `Auditor` mapped to AD groups; authority enforced server-side. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.10(k), system-operation manual `EQX-RB-EMP-OPS-001`; Waters SCN releases under site CR with impact assessment + post-upgrade OQ verification of FS-PROC-04 + FS-PART11-09. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.50, Empower eSign dialog enforces capture of printed-name + dateTime + meaning-of-signature (closed list: Review / Approve / Reject / Lock). |
| FS-PART11-09 | URS-PART11-09 | Per § 11.70, signature payload includes SHA-256 of the signed result + Empower eSign ledger entry; record-modification flips signature to `INVALID — RECORD MODIFIED`. |
| FS-PART11-10 | URS-PART11-10 | Per § 11.100, each AD account tied to a unique HR record; reuse / reassignment prohibited at AD level. |
| FS-PART11-11 | URS-PART11-11 | Per § 11.200, Empower setting `ForceReAuthOnSignature = true`; no cached credentials at signing. |
| FS-PART11-12 | URS-PART11-12 | Per § 11.300, AD GPO enforces 14-char minimum, 90-day rotation, history 24, complexity ON; lockout 5 failures / 15 min window. |
| FS-PART11-13 | URS-PART11-13 | Empower role-matrix denies any single user holding Analyst + Senior Reviewer / QC Manager / Approver on the same project; verified by `OQ-PART11-SOD-01`. |

### 4.6 Empower Project Hierarchy (M-EMP)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-EMP-01 | URS-EMP-01 | Project-naming convention `<PROGRAMME>-<PRODUCT>-<TYPE>` enforced at project-creation; project-policy bundle (RawDataLock=ON; eSign=ON; Audit=ON; RFC=ON) auto-applied for projects tagged `GxP=true`. |
| FS-EMP-02 | URS-EMP-02 | AD-mapped role table version-controlled in git (`empower-role-map.yaml`); quarterly access review produces signed evidence. |
| FS-EMP-03 | URS-EMP-03 | Project-rename requires QC Manager + Head of QA dual eSign; original name preserved as alias in the project metadata; audit-trail entry mandatory. |
| FS-EMP-04 | URS-EMP-04 | Processing-method-to-result-set binding becomes immutable upon Senior Analyst review; rebinding requires deviation record. |
| FS-EMP-05 | URS-EMP-05 | Empower `.eax` self-contained archive bundle includes methods + raw data + results + audit trail + signatures + library version pointers. |

### 4.7 System Suitability Test (M-SST)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SST-01 | URS-SST-01 | Empower SST evaluator computes per-method USP <621> parameters (R, Tf, N, RT-RSD, peak-area-RSD on replicate n=5); method-bound thresholds. |
| FS-SST-02 | URS-SST-02 | Empower blocks downstream result release when SST verdict = FAIL; sequence flagged `SST-FAILED`; re-run requires reason-for-change. |
| FS-SST-03 | URS-SST-03 | SST-Result entity persisted with criteria, observed, pass/fail per parameter, verdict, evaluator version, cryptographic reference to the sequence-id. |
| FS-SST-04 | URS-SST-04 | Bracketed-SST mode for sequences ≥ 30 injections; bracket-end failure flips bracketed results to `SUSPECT — END-SST-FAILED`. |

### 4.8 Calibration Curve and Quantitation (M-QNT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-QNT-01 | URS-QNT-01 | Empower calibration-curve engine requires ≥ 6 non-zero standards (assay) or ≥ 5 (related substances); r² ≥ 0.99 (assay) auto-checked; failure blocks result acceptance. |
| FS-QNT-02 | URS-QNT-02 | Per-standard back-calculation outside ± 15% (non-LOQ) or ± 20% (LOQ) raises `STANDARD_OUTLIER` flag; exclusion requires Method-Owner eSign + reason captured. |
| FS-QNT-03 | URS-QNT-03 | Result computation in IEEE-754 double precision; rounding applied only at final-report-generation step per SOP `EQX-SOP-CHROM-ROUND-001`. |
| FS-QNT-04 | URS-QNT-04 | Spec-comparison rule flags results at 30% / 50% / 100% of limit per the configured spec-set; flags `TREND`, `OOT`, `OOS` surfaced on result view + propagated to LIMS push. |

### 4.9 Reprocessing and Result Lineage (M-RPR)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RPR-01 | URS-RPR-01 | Empower Reason-for-Change dialog with closed-list reasons (baseline-noise / co-elution / peak-shoulder / wrong-integration-window / etc.) + mandatory free-text justification; save blocked without reason. |
| FS-RPR-02 | URS-RPR-02 | Reprocessing creates a new `Result` entity with `parent_result_id` + `original_result_id`; lineage tree visible in the result-set view. |
| FS-RPR-03 | URS-RPR-03 | When reprocessed-Result.value ≠ originalResult.value within configured tolerance, raise `RESULT_DIFFERS_ON_REPROCESS` flag + block LIMS push pending Method-Owner + QC-Manager dual eSign + deviation record. |
| FS-RPR-04 | URS-RPR-04 | Result-lineage export feature renders the tree as DOT (graphviz) + JSON; included in the project `.eax` bundle. |

### 4.10 Multi-Site Project-Folder Federation (M-FED)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-FED-01 | URS-FED-01 | Federation-grant table per-project; explicit grant required for cross-site sharing; grant captured as immutable audit-trail entry. |
| FS-FED-02 | URS-FED-02 | Federation replication is read-only at destination; write attempts at the federated copy raise `FED_READ_ONLY` error + audit entry. |
| FS-FED-03 | URS-FED-03 | Federation health-monitor reports last-sync timestamp, replication lag, and divergence-on-result-hashes per federated project; lag > 24 h triggers Splunk alert. |

### 4.11 Method Lifecycle (M-MTH)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MTH-01 | URS-MTH-01 | Method state machine implemented per URS lifecycle states; only EFFECTIVE selectable at sequence-start. |
| FS-MTH-02 | URS-MTH-02 | State-transition eSign with Author ≠ Reviewer ≠ Approver enforced server-side; history retained as immutable audit-trail. |
| FS-MTH-03 | URS-MTH-03 | Method `MatrixType` + `ColumnLot` enforcement configured at the method level; mismatch at sequence-start raises blocking dialog. |
| FS-MTH-04 | URS-MTH-04 | Method-change-impact engine lists in-flight projects + result-sets touched; report eSigned by Method Owner before promotion. |

### 4.12 Stability and Release Workflow (M-REL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REL-01 | URS-REL-01 | Release workflow: Analyst → Senior Reviewer → QC Manager → QA Approver; each transition eSigned with closed-list meaning; SoD enforced. |
| FS-REL-02 | URS-REL-02 | Stability-time-point + storage-condition tags mandatory on stability results; mismatch (e.g., 25 °C tag on 40 °C sample) flagged at Senior-Reviewer step. |
| FS-REL-03 | URS-REL-03 | Held release records expire after 30 days; QC Manager must re-approve before QA Approver can finalise. |

### 4.13 Data Integrity (M-DI)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | Every Empower record carries the AD account-id that created / modified it; null actor not permitted at the GxP boundary. |
| FS-DI-02 | URS-DI-02 | PDF/A-3 export embeds fonts + ICC profile; native `.eax` archive also produced. |
| FS-DI-03 | URS-DI-03 | Retrospective entries flagged in the audit trail with `recordedTimestamp` ≠ `eventTimestamp` + mandatory reason. |
| FS-DI-04 | URS-DI-04 | Raw Data Lock = ON for all GxP projects; raw-file mutation prevented at the Empower service level + at the file-system level. |
| FS-DI-05 | URS-DI-05 | OQ calculation regression suite: 20 reference samples × 3 analytes; observed vs validated values within ± 0.01% of spec limit. |
| FS-DI-06 | URS-DI-06 | Metadata-completeness validator at acquisition close; chronological-order DB-enforced; retention metadata applied per FS-AUD-04. |

### 4.14 LIMS Interface (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | Empower-LIMS Connector 4.2 polls LabWare LIMS 8 via REST every 60 s using service principal `equinox\svc-empower-limsread` (read-only AD group); worklist cached + bound to sequence. |
| FS-INT-LIMS-02 | URS-INT-LIMS-02 | Approved-result push gated by Empower `LimsExport` flag (set only when QC Manager approval state == true AND QA Approver eSign == true if release-bound); payload signed with site PKI cert `equinox-empower-2026q2`. |
| FS-INT-LIMS-03 | URS-INT-LIMS-03 | Result payload schema `EQX-LIMS-PUSH-EMP-v3.json` mandates reportId + projectId + methodId+version + sequenceId + instrumentId + sstRecordId + calCurveId + analystId + reviewerId + approverId + rawDataHash + resultHash + flagSet (TREND/OOT/OOS); LIMS rejects payloads missing any field. |
| FS-INT-LIMS-04 | URS-INT-LIMS-04 | Connector failure events logged to Windows Application log + forwarded to Splunk index `wel-empower`; alert rule `wel-empower-lims-failure` pages on-call after 5-min window. |

### 4.15 Backup and Recovery (M-BAK)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BAK-01 | URS-BAK-01 | Oracle nightly RMAN backup + continuous archived redo log shipping to immutable cold storage (NetApp SnapLock 25 y); SHA-256 verified per backup. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore test against the DR cluster, witnessed by QA; restore plan `EQX-PROC-EMP-RESTORE-001`. |
| FS-BAK-03 | URS-BAK-03 | RTO ≤ 4 h achieved by Oracle Data Guard active-passive failover; RPO ≤ 15 min via continuous redo-log shipping. |
| FS-BAK-04 | URS-BAK-04 | Annual full DR drill: failover to DR cluster + representative sequence acquisition on DR LAC/E + failback; signed off by QC Manager + IT Operations Lead. |

### 4.16 Performance and Availability (M-PERF)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | Sustained 24-instrument concurrent acquisition verified by `PQ-PERF-CONCURRENT-01` (synthetic load + real instruments). |
| FS-PERF-02 | URS-PERF-02 | Citrix client open + project-load P95 ≤ 10 s; measured under nominal load via APM agent on Citrix workers. |
| FS-PERF-03 | URS-PERF-03 | Sequence-start UI response P95 ≤ 5 s; measured via Empower APM. |
| FS-AV-01 | URS-AV-01 | Availability ≥ 99.5% during business hours; outage tracking via Splunk `wel-empower-availability`. |

### 4.17 Security (M-SEC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SEC-01 | URS-SEC-01 | All authentication via AD; break-glass `equinox\bg-emp-admin` quarterly reviewed. |
| FS-SEC-02 | URS-SEC-02 | Site `EQX-IS-POL-PASSWORD` enforced via GPO. |
| FS-SEC-03 | URS-SEC-03 | GPO `Block-RemovableMedia` on LAC/E + Citrix workers; engineering override via signed CR. |
| FS-SEC-04 | URS-SEC-04 | CrowdStrike Falcon Sensor with Waters-approved exclusion list on LAC/E; daily definition updates; compliance dashboard `wel-empower-av`. |
| FS-SEC-05 | URS-SEC-05 | Three VLANs (app/db, LAC/E, Citrix) with firewall rules between; annual rule-audit. |

### 4.18 Training and Periodic Review (M-TRN / M-PR)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | LMS curriculum `EQX-CURR-EMP-Analyst-v1` mandatory before AD group + Empower role assignment. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher curriculum auto-assigned; LMS revokes AD-group membership on overdue + 30 days. |
| FS-PR-01 | URS-PR-01 | Periodic-review template `EQX-PR-EMP-YYYYMMDD`; signed by QC Manager + Head of QA. |
| FS-PR-02 | URS-PR-02 | Periodic review produces signed disposition for drift / non-conformance findings. |

---


### 4.19 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem (Empower service-account bind) with Citrix-published interactive Kerberos. Conditional-access binding to policy `Lab-Workstation Conditional Access (MFA on interactive logon; LAC/E nodes named-location)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with Oracle RMAN for the Empower Oracle 19c backend plus continuous archived-redo-log shipping; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.20 Cross-System Integration — Helios handover (M-XINT-HEL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HEL-01 | URS-XINT-HEL-01 | Audit-event publisher emits Kafka topic `helios.ingest.equinox.empower.v1` with schema-registry-pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`; at-least-once delivery; idempotency key `{source_system, event_id}`; back-pressure surfaced via Prometheus `helios_publish_lag_seconds` with 5-min alert at > 600 s. |
| FS-XINT-HEL-02 | URS-XINT-HEL-02 | Local audit-store retention policy enforces ≥ 7 y; Helios ack persisted as `helios_ack_ts` per event; periodic reconciliation job verifies parity (Helios row count == local published count) and raises a deviation in MasterControl on > 0.01% mismatch over a 24 h window. |

## 5. Interface Specifications

| IF ID | URS ID | Counterparty | Protocol | Direction | Notes |
|---|---|---|---|---|---|
| IF-LIMS-01 | URS-INT-LIMS-01 | LabWare LIMS 8 | Empower-LIMS Connector / REST | inbound | worklist import |
| IF-LIMS-02 | URS-INT-LIMS-02 | LabWare LIMS 8 | Empower-LIMS Connector / REST | outbound | approved-result push |
| IF-AD-01 | URS-SEC-01 | AD / Kerberos | LDAPS | bidirectional | AuthN |
| IF-NTP-01 | URS-SW-04 | NTP | NTP | inbound | time sync |
| IF-CITRIX-01 | URS-SW-05 | Citrix Virtual Apps | ICA | bidirectional | client publishing |

## 6. Data Model (high-level)

| Entity | Attributes (illustrative) |
|---|---|
| Project | project_id, name, policy {raw_data_lock, esign, audit, rfc}, ad_role_map |
| Method | method_id, project_id, version, state, author, approver |
| Sequence | sequence_id, project_id, instrument_id, method_id+version, analyst_id, started_at, sst_status |
| Injection | injection_id, sequence_id, sample_id, vial_position, volume, ts |
| Result | result_id, injection_id, integrated_peaks, calc_value, spec_status, approver_id |
| AuditEvent | event_id, scope, user_id, action, old, new, reason, ts |
| Signature | sig_id, scope, signer_id, meaning, ts, payload_hash |

## 7. Non-Functional Specifications

| NFR ID | Specification |
|---|---|
| NFR-01 | 24-instrument concurrent acquisition without data loss |
| NFR-02 | Citrix client P95 open ≤ 10 s |
| NFR-03 | RPO ≤ 15 min, RTO ≤ 4 h |
| NFR-04 | Audit trail append-only |
| NFR-05 | Retention ≥ 7 y (≥ 25 y if release-linked) |
| NFR-06 | NTP skew alert > 1 s |

## 8. Configuration Items (CI)

| CI ID | Item | Configured Value | Source |
|---|---|---|---|
| CI-01 | Project Policy | Raw Data Lock=ON; eSign=ON; Audit=ON; RFC=ON | URS-SW-03 |
| CI-02 | LAC/E count | 24 | URS scope |
| CI-03 | Method states | DRAFT,REVIEW,APPROVED,EFFECTIVE,OBSOLETE | URS-ACQ-01 |
| CI-04 | SST policy | run at sequence start; failure blocks results | URS-ACQ-04 |
| CI-05 | Spec flag bands | 30% / 50% / 100% of limit | URS-PROC-04 |
| CI-06 | Citrix client | fixed version; non-persistent profile | URS-SW-05 |
| CI-07 | Audit retention | ≥ 7 y; ≥ 25 y release-linked | URS-AUD-04 |
| CI-08 | Backup | nightly + continuous redo | URS-BAK-01 |
| CI-09 | Restore-test cadence | quarterly | URS-BAK-02 |
| CI-10 | LIMS push gate | QC Manager approval required | URS-INT-LIMS-02 |
| CI-11 | NTP skew alert | > 1 s | URS-SW-04 |

## 9. Constraints / Assumptions / Risks

- **Constraints:** Waters SCN updates under change control; vendor-controlled core platform.
- **Assumptions:** AD, LIMS, Citrix, NTP are validated.
- **FS-level risks:** silent re-integration without justification (FS-PROC-02 + RFC required); LIMS push of unapproved results (FS-INT-LIMS-02 + connector gate); audit-trail tampering (FS-AUD-02 + role mapping); shared / generic accounts (FS-SEC-01 + AD enforcement).

## 10. References

- EQX-URS-EMPOWER-001 v1.0 (parent URS).
- 21 CFR Part 11; EU GMP Annex 11; USP <621>; ICH Q2(R2).
- ISPE GAMP 5 (2nd ed., 2022); GAMP GPG *Validation of Laboratory Computerized Systems*.
- Waters — *Empower 3 FR5 Configuration Reference*.

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-PLAT-01 | FS-PLAT-01 |
| URS-PLAT-02 | FS-PLAT-02 |
| URS-PLAT-03 | FS-PLAT-03 |
| URS-SW-01 | FS-SW-01 |
| URS-SW-02 | FS-SW-02 |
| URS-SW-03 | FS-SW-03 |
| URS-SW-04 | FS-SW-04 |
| URS-SW-05 | FS-SW-05 |
| URS-ACQ-01 | FS-ACQ-01 |
| URS-ACQ-02 | FS-ACQ-02 |
| URS-ACQ-03 | FS-ACQ-03 |
| URS-ACQ-04 | FS-ACQ-04 |
| URS-PROC-01 | FS-PROC-01 |
| URS-PROC-02 | FS-PROC-02 |
| URS-PROC-03 | FS-PROC-03 |
| URS-PROC-04 | FS-PROC-04 |
| URS-PROC-05 | FS-PROC-05 |
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
| URS-EMP-01 | FS-EMP-01 |
| URS-EMP-02 | FS-EMP-02 |
| URS-EMP-03 | FS-EMP-03 |
| URS-EMP-04 | FS-EMP-04 |
| URS-EMP-05 | FS-EMP-05 |
| URS-SST-01 | FS-SST-01 |
| URS-SST-02 | FS-SST-02 |
| URS-SST-03 | FS-SST-03 |
| URS-SST-04 | FS-SST-04 |
| URS-QNT-01 | FS-QNT-01 |
| URS-QNT-02 | FS-QNT-02 |
| URS-QNT-03 | FS-QNT-03 |
| URS-QNT-04 | FS-QNT-04 |
| URS-RPR-01 | FS-RPR-01 |
| URS-RPR-02 | FS-RPR-02 |
| URS-RPR-03 | FS-RPR-03 |
| URS-RPR-04 | FS-RPR-04 |
| URS-FED-01 | FS-FED-01 |
| URS-FED-02 | FS-FED-02 |
| URS-FED-03 | FS-FED-03 |
| URS-MTH-01 | FS-MTH-01 |
| URS-MTH-02 | FS-MTH-02 |
| URS-MTH-03 | FS-MTH-03 |
| URS-MTH-04 | FS-MTH-04 |
| URS-REL-01 | FS-REL-01 |
| URS-REL-02 | FS-REL-02 |
| URS-REL-03 | FS-REL-03 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-INT-LIMS-01 | FS-INT-LIMS-01 |
| URS-INT-LIMS-02 | FS-INT-LIMS-02 |
| URS-INT-LIMS-03 | FS-INT-LIMS-03 |
| URS-INT-LIMS-04 | FS-INT-LIMS-04 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-BAK-03 | FS-BAK-03 |
| URS-BAK-04 | FS-BAK-04 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-PERF-03 | FS-PERF-03 |
| URS-AV-01 | FS-AV-01 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-SEC-05 | FS-SEC-05 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-PR-02 | FS-PR-02 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-HEL-01 | FS-XINT-HEL-01 |
| URS-XINT-HEL-02 | FS-XINT-HEL-02 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Silent re-integration without justification (FDA Warning Letter pattern — Hetero Labs 2024, Sun Pharma 2023, Ranbaxy precedents) | Medium | Critical | URS-RPR-01 (closed-list reason + free-text), URS-AUD-01 |
| R-02 | LIMS push of unapproved or out-of-spec results bypassing QC sign-off | Low | Critical | URS-INT-LIMS-02, URS-PART11-13 |
| R-03 | Audit-trail tampering via database-direct access | Low | Critical | URS-AUD-02 (DB GRANT model), URS-SEC-05 |
| R-04 | Shared / generic accounts on LAC/E nodes | Medium | High | URS-SEC-01, URS-PART11-04 |
| R-05 | Project-folder federation drift across sites (divergent results between Stuttgart and a partner site) | Medium | High | URS-FED-03 |
| R-06 | Raw-data-lock bypass (project-policy mis-applied to a GxP project) | Low | Critical | URS-EMP-01, URS-DI-04 |
| R-07 | Calibration-curve outlier suppression (single standard silently dropped) | Medium | High | URS-QNT-02 |
| R-08 | RT shift on column-lot change leading to mis-identification | Medium | High | URS-MTH-03 |
| R-09 | Schema-mismatch in LIMS push (missing field silently dropped on LIMS side) | Low | High | URS-INT-LIMS-03 |
| R-10 | Stability time-point mis-tagging surviving to release | Low | High | URS-REL-02 |
| R-11 | Oracle PITR archive log gap (Data Guard replication lag uncaught) | Low | Critical | URS-BAK-01, URS-BAK-03 |
| R-12 | Empower SCN silent regression of eSign or audit-trail behaviour | Low | Critical | URS-PART11-07 + post-upgrade OQ verification |

Full evaluation in `EQX-RA-EMPOWER-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
