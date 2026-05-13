---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring 2026-04-27; T2 rebuild 2026-05-13 (Chunk A Liquid Handler)"
seed_corpus_basis:
  - "IRS-URS-LH-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd ed.) Cat 4/5 conventions"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300"
  - "21 CFR Part 211 §§ .68, .180, .192"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "ICH Q2(R2); ICH Q9(R1)"
  - "ISO 8655 (parts 1-7)"
  - "USP <41>; USP <1251>; USP <1058> AIQ (Group B)"
  - "Hamilton — Microlab STAR + VENUS 6.x + SDK"
parent_urs:
  document_number: IRS-URS-LH-001
  version: 1.2
  file: ../../URS/_generated/final/Liquid_Handler_Hamilton_STAR_Computer_System__Iris_BioMed_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Robotic Liquid Handler — Hamilton Microlab STAR + VENUS 6.x

**Document Number:** IRS-FS-LH-001 | **Version:** 1.2 | **Effective Date:** 2026-05-13 *(synthetic)*
**Parent URS:** IRS-URS-LH-001 v1.2 | **Site:** Iris BioMed Inc., QC Bioassay Lab, Salt Lake City, Utah, USA *(fictional)*
**System Class:** GAMP Cat 4 — Configured Product (with site-authored VENUS methods as Cat-5 sub-components)
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192; EU GMP Annex 11 §§ 4, 6, 9, 11; ICH Q2(R2); ISO 8655 (parts 1-7); USP <41>; USP <1251>; USP <1058>; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Bioassay Lead) | _____________ | _____________ | _____ |
| Reviewer (Automation Engineer) | _____________ | _____________ | _____ |
| Approver (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-13 | (synthetic) | T2 rebuild aligned to URS v1.2; per-URS-ID row expansion (no range compression for Part 11 / AUD / DI / MTH / WL); new FS sections for deck-layout + labware management, liquid-class library, tip-pickup + aspirate/dispense error recovery, ISO 8655 verification cadence, multi-channel + MPH choreography, contamination control. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## Definitions

Inherited from `IRS-URS-LH-001`. FS-specific terms:

| Term | Definition |
|---|---|
| LLD | Liquid-Level Detection (capacitive sensing on Hamilton channels) |
| MPH | Multi-Probe Head (96 / 384 simultaneous pipetting head) |
| SDK | Hamilton VENUS Software Development Kit |
| Liquid Class | Method-bound parameter set governing aspirate/dispense kinematics per liquid type |
| Tip Counter | Per-rack tip-use counter for traceability |

## 1. Purpose

This FS specifies the deployment, configuration, and integration of Hamilton Microlab STAR + VENUS 6.x on a dedicated workstation to satisfy `IRS-URS-LH-001` v1.2.

## 2. Scope

Mirrors URS § 2: one STAR instrument (8-channel + Multi-Probe Head) + VENUS 6.x on a dedicated Win 11 LTSC PC; site-authored VENUS methods (Cat 5 sub-components); AD authentication; LIMS interface (worklist + provenance push); daily backup; NTP sync. Out: STAR mechanical hardware (separate EQ); plate readers (separate URSs); LIMS sample lifecycle.

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source / Vendor |
|---|---|---|---|---|
| C-01 | Hamilton Microlab STAR (8-channel + MPH) | Hardware | 3 | Hamilton |
| C-02 | Track-Gripper option | Hardware | 3 | Hamilton |
| C-03 | VENUS 6.x control software | COTS app | 4 | Hamilton |
| C-04 | Site-authored VENUS methods | Custom | 5 | Iris BioMed |
| C-05 | Workstation (Dell Precision 3680) | Hardware | 3 | Dell |
| C-06 | Win 11 LTSC | Infrastructure | 1 | Microsoft |
| C-07 | AD `iris.local` | Infrastructure | 1 | Microsoft |
| C-08 | LabWare LIMS 8 connector | COTS adapter | 4 | Hamilton/LabWare |

### 3.2 Logical Architecture

```
   AD `iris.local`         NTP `ntp.iris.local`
         │                        │
         └───────────┬────────────┘
                     ▼
           ┌──────────────────────────────┐
           │  VENUS 6.x Workstation        │
           │  (Win 11 LTSC, domain-joined) │
           └──────────┬───────────────────┘
                      │  USB-3 (instrument control)
                      ▼
           ┌──────────────────────────────┐
           │ Hamilton Microlab STAR        │
           │  8-channel + MPH + Track-     │
           │  Gripper                      │
           └──────────────────────────────┘
                      │
                      ▼
           ┌──────────────────────────────┐
           │ LabWare LIMS 8 (worklist +    │
           │ provenance push)              │
           └──────────────────────────────┘
```

## 4. Functional Specifications

### 4.1 Platform / Hardware

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | PC on lab-IT VLAN 421; UPS APC SMT1500 sized for ≥ 30 min hold; instrument fail-safe to safe state on power loss (Hamilton STAR built-in fail-safe). |
| FS-PLAT-02 | URS-PLAT-02 | Windows Time service syncs to `ntp.iris.local`; configured skew threshold 1 s. |
| FS-PLAT-03 | URS-PLAT-03 | Per-channel ISO 8655 volume verification scheduled per `IRS-CAL-PLAN-LH-001`; expired calibration blocks GxP runs (see FS-CAL-01..04). |

### 4.2 Software Configuration

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SW-01 | URS-SW-01 | VENUS Part 11 module enabled: audit-trail required, e-sign required, raw-data lock; validated configuration baseline `IRS-CFG-VENUS-v1`. |
| FS-SW-02 | URS-SW-02 | Methods stored in `\\iris-gmp-fs01\venus-methods` (NetApp SnapLock immutable for EFFECTIVE versions); per-method ACL enforced via AD-mapped roles. |

### 4.3 Method SDLC (Cat-5 Sub-Component)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MTH-01 | URS-MTH-01 | Method SDLC procedure `IRS-SOP-LH-METHOD-SDLC-001`: requirements per-assay → code review (peer + Method Reviewer) → dry-run on VENUS simulator → wet-run on instrument → ISO 8655 accuracy/precision verification on the method → regression suite (10 reference samples) before promotion. |
| FS-MTH-02 | URS-MTH-02 | Method state machine: DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE; only EFFECTIVE selectable at worklist start. |
| FS-MTH-03 | URS-MTH-03 | State-transition eSign with Method-Author ≠ Method-Reviewer ≠ Method-Approver enforced server-side. |
| FS-MTH-04 | URS-MTH-04 | Method source version-controlled in site GitLab repo `iris-venus-methods`; signed authorship via git-commit-signing. |

### 4.4 Worklist Execution and Provenance

| FS ID | URS ID | Specification |
|---|---|---|
| FS-WL-01 | URS-WL-01 | Per-worklist capture schema: operator-id, method-id + version, source-labware (with lot-ids), destination-labware (with lot-ids), per-channel per-well volume, per-dispense timestamp, error / exception events. |
| FS-WL-02 | URS-WL-02 | Pre-run validator: instrument-ready check + per-channel calibration-currency check + method-EFFECTIVE check + labware-presence-and-position check; any failure blocks run with reason surfaced to operator. |
| FS-WL-03 | URS-WL-03 | Mid-run aspirate/dispense errors (clot detection, LLD failure, no-tip detection) logged with cause; failure-handling routes to operator-decision workflow (abort / retry / continue-with-deviation). |
| FS-WL-04 | URS-WL-04 | Post-run provenance: PDF report + structured CSV; push to LIMS as the per-sample chain-of-custody record. |

### 4.5 Audit Trail

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | VENUS audit trail captures: method changes, worklist creation + run + completion + errors, calibration events, signatures, configuration changes (deck, liquid-class, labware-defs). |
| FS-AUD-02 | URS-AUD-02 | Audit-trail tables append-only at DB level; Automation Engineer + System Administrator roles have no UPDATE/DELETE GRANT. |
| FS-AUD-03 | URS-AUD-03 | Senior Operator signs per-batch audit-trail review; QC Bioassay Lead signs monthly review. |
| FS-AUD-04 | URS-AUD-04 | NetApp SnapLock WORM 7-y / 25-y release-linked retention. |
| FS-AUD-05 | URS-AUD-05 | Audit-trail export by method / worklist / date / user without disrupting routine operation. |

### 4.6 21 CFR Part 11

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Validation dossier `IRS-VAL-LH-001` (IQ + OQ + PQ + RTM + VSR + PR). |
| FS-PART11-02 | URS-PART11-02 | PDF/A-3 + native VENUS audit-trail export for inspection. |
| FS-PART11-03 | URS-PART11-03 | NetApp SnapLock 25-y immutable + daily Veeam backup with SHA-256 verification. |
| FS-PART11-04 | URS-PART11-04 | AD-bound access via `Lab-LH-*` groups; local accounts disabled except break-glass. |
| FS-PART11-05 | URS-PART11-05 | VENUS audit trail per FS-AUD-01. |
| FS-PART11-06 | URS-PART11-06 | VENUS user-role authority mapped to AD groups; checks enforced at every privileged action. |
| FS-PART11-07 | URS-PART11-07 | Hamilton SCN releases managed under site CR `IRS-RB-LH-OPS-001`; impact assessment + post-upgrade OQ for FS-WL-01 + FS-ERR-* + FS-CAL-*. |
| FS-PART11-08 | URS-PART11-08 | VENUS eSign dialog enforces printed-name + dateTime + meaning-of-signature (closed list Author / Review / Approve / Lock). |
| FS-PART11-09 | URS-PART11-09 | Signature payload includes record hash; modification invalidates signature. |
| FS-PART11-10 | URS-PART11-10 | Each AD account unique HR record; reuse/reassignment prohibited at AD level. |
| FS-PART11-11 | URS-PART11-11 | VENUS setting `RequireSignatureReAuth = true`. |
| FS-PART11-12 | URS-PART11-12 | AD GPO enforces site `IRS-IS-POL-PASSWORD` (14-char min, 90-d rotation, history 24, complexity ON, lockout 5 / 15 min). |
| FS-PART11-13 | URS-PART11-13 | VENUS user-role matrix denies Method-Author ≠ Method-Reviewer ≠ Method-Approver overlap on same method; Operator ≠ Verifier overlap on same run; verified by `OQ-PART11-SOD-01`. |

### 4.7 Data Integrity

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | Every record carries `actor_id` (AD-bound). |
| FS-DI-02 | URS-DI-02 | PDF/A-3 + CSV export. |
| FS-DI-03 | URS-DI-03 | Server-side timestamps; retroactive entries flagged. |
| FS-DI-04 | URS-DI-04 | Raw acquisition data (per-channel volume + per-well log) immutable after worklist close. |
| FS-DI-05 | URS-DI-05 | Volume measurements traceable to ISO 8655 verification records (per channel); calibration certificates retained. |
| FS-DI-06 | URS-DI-06 | Metadata-completeness validator at worklist close; chronological-order DB-enforced. |

### 4.8 Integrations, Performance, Backup, Security

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | LIMS connector polls LabWare LIMS 8 over REST every 60 s using service principal `iris\svc-lh-limsread`; provenance push gated by Operator + Senior Operator eSign. |
| FS-INT-AD-01 | URS-INT-AD-01 | AD authentication via Kerberos / LDAPS; `Lab-LH-*` AD groups for role mapping. |
| FS-PERF-01 | URS-PERF-01 | Worklist-start latency ≤ 10 s P95 measured at OQ; provenance-report generation ≤ 60 s for 384-well plate. |
| FS-PERF-02 | URS-PERF-02 | 96-well plate worklist cycle-time per method-validation; PQ stress-test executes representative method end-to-end. |
| FS-BAK-01 | URS-BAK-01 | Veeam B&R daily backup of methods + provenance + audit-trail; SHA-256 verified; retention 25 y. |
| FS-BAK-02 | URS-BAK-02 | Quarterly SureBackup-scripted restore test, QA witness. |
| FS-BAK-03 | URS-BAK-03 | Documented hardware-replacement runbook `IRS-RB-LH-DR-001`; RTO ≤ 8 business h. |
| FS-SEC-01 | URS-SEC-01 | GPO `Block-RemovableMedia` on workstation; engineering override via signed CR. |
| FS-SEC-02 | URS-SEC-02 | AD authentication; quarterly access review. |
| FS-SEC-03 | URS-SEC-03 | CrowdStrike Falcon Sensor with Hamilton-approved exclusion list (VENUS install paths + real-time-data writers). |

### 4.9 Training and Periodic Review

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | LMS curriculum `IRS-CURR-LH-Operator-v1` mandatory before AD group; Method Authors require additional `IRS-CURR-LH-MethodAuthor-v1` competency assessment (SDK fluency). |
| FS-TRN-02 | URS-TRN-02 | Annual refresher LMS curriculum auto-assigned. |
| FS-PR-01 | URS-PR-01 | Periodic-review template `IRS-PR-LH-YYYYMMDD`; signed by QC Bioassay Lead + Head of QA. |
| FS-PR-02 | URS-PR-02 | PR disposition record for drift findings. |

### 4.10 Deck Layout and Labware Management

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DECK-01 | URS-DECK-01 | VENUS deck-layout file (.lay) version-controlled in `iris-venus-decks` git repo; method references specific deck-layout hash; mismatch at run-start blocks. |
| FS-DECK-02 | URS-DECK-02 | VENUS labware definitions in `\\iris-gmp-fs01\venus-labware`; changes require Method-Owner eSign + re-validation flow trigger. |
| FS-DECK-03 | URS-DECK-03 | Pre-run deck-verification screen prompts operator confirmation of each labware (with RFID-confirmation where supported); confirmation eSigned + audit-trail entry. |
| FS-DECK-04 | URS-DECK-04 | PM-time deck-position drift check via reference plate; drift > 0.5 mm flagged + triggers re-teach workflow. |
| FS-DECK-05 | URS-DECK-05 | Per-run lot capture: reagent lot, plate lot, tip-rack lot recorded in worklist provenance. |

### 4.11 Liquid-Class Library

| FS ID | URS ID | Specification |
|---|---|---|
| FS-LQC-01 | URS-LQC-01 | Liquid-class library covers aqueous, viscous (e.g., 50% glycerol), organic (e.g., methanol), surfactant, DMSO, blood-derived; per-class parameters: aspirate-flow, dispense-flow, air-gap, blowout, tip-touch. |
| FS-LQC-02 | URS-LQC-02 | Method-promotion static analyser checks every aspirate-dispense step has explicit liquid-class assignment; default-aqueous-on-viscous mismatch flagged + blocks promotion. |
| FS-LQC-03 | URS-LQC-03 | Liquid-class add / change requires Method-Owner + Senior Bioanalyst eSign + ISO 8655 volume-accuracy + CV verification on the changed class. |
| FS-LQC-04 | URS-LQC-04 | Liquid-class library version hash pinned per method-version in the method file header. |

### 4.12 Tip Pickup, Aspirate/Dispense Error Recovery

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ERR-01 | URS-ERR-01 | Capacitive level-sense check at Z = expected-rack-Z verifies tip presence per channel; failure routes to operator-decision UI (auto-retry on alternate tip / abort / continue-with-deviation). |
| FS-ERR-02 | URS-ERR-02 | Pressure monitoring during aspirate compared to method-bound pressure-profile; deviation > threshold raises `CLOT_DETECTED` event; default abort + flag well `ASPIRATE_FAIL`. |
| FS-ERR-03 | URS-ERR-03 | LLD failure (no level detected at expected Z) raises `NO_LIQUID` event; default abort + flag well + capture operator decision rationale. |
| FS-ERR-04 | URS-ERR-04 | Per-channel pacing: VENUS schedules each channel independently when liquid-classes differ on the same plate. |
| FS-ERR-05 | URS-ERR-05 | Mid-run abort writes provenance for completed wells as valid; pending wells flagged `PENDING_ABORT`; explicit operator override required to include in downstream. |

### 4.13 ISO 8655 Verification

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CAL-01 | URS-CAL-01 | ISO 8655 gravimetric volume-verification per channel at cadence defined in `IRS-CAL-PLAN-LH-001`; calibration record persisted per channel + per verification event. |
| FS-CAL-02 | URS-CAL-02 | Pre-run validator checks per-channel calibration expiry against method-bound channel selection; expired channel blocks GxP run; override requires QC Bioassay Lead eSign + impact assessment. |
| FS-CAL-03 | URS-CAL-03 | Verification protocol: 3 volume points (10%, 50%, 100% of channel range) × n ≥ 10 replicates; accuracy + precision per ISO 8655 Part 2 thresholds; results stored per-channel + trended. |
| FS-CAL-04 | URS-CAL-04 | Trending dashboard plots per-channel volume drift over time; monotonic > 1% drift over 3 verifications flags channel for PM. |

### 4.14 Multi-Channel + MPH Choreography

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CHO-01 | URS-CHO-01 | Method-promotion static analyser detects channel-vs-MPH same-well same-time conflicts; flagged conflicts block promotion. |
| FS-CHO-02 | URS-CHO-02 | MPH wash-station configured between liquid-class changes; method-builder UI prompts wash-step insertion. |
| FS-CHO-03 | URS-CHO-03 | Track-Gripper movements logged in worklist provenance with source/dest position + timestamp. |

### 4.15 Contamination Control

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CONT-01 | URS-CONT-01 | Method-promotion static analyser blocks promotion when tip-re-use across samples detected for GxP runs (tip-re-use within single-sample serial-dilution permitted only if method-bound). |
| FS-CONT-02 | URS-CONT-02 | When liquid-class flag `sticky=true`, method-promotion validator requires explicit wash-step; missing wash-step blocks promotion. |
| FS-CONT-03 | URS-CONT-03 | Per tip-rack counter (`tips_used` field) maintained; counter reset on rack reload event. |


### 4.16 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem. Conditional-access binding to policy `Lab-Workstation Conditional Access (MFA on interactive logon)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the Venus method / run DB plus file-level capture of method scripts; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Configuration Items (CI)

| CI | Item | Value | Owner |
|---|---|---|---|
| CI-01 | ISO 8655 verification cadence (gravimetric) | per `IRS-CAL-PLAN-LH-001` (typ. 6-month / quarterly high-stakes) | Automation Engineer |
| CI-02 | VENUS method state machine | DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE | System Administrator |
| CI-03 | Pre-run gate checks | instrument-ready + calibration-currency + method-EFFECTIVE + labware-presence | Automation Engineer |
| CI-04 | Tip-pickup verification method | capacitive level-sense at Z = expected-rack-Z | Automation Engineer |
| CI-05 | Pressure-deviation threshold for clot detection | per liquid-class (typ. ± 30% from method-bound profile) | Method Owner |
| CI-06 | Liquid-class library version | hashed and pinned per method-version | Method Owner |
| CI-07 | Deck-position drift threshold | 0.5 mm | Automation Engineer |
| CI-08 | Tip-counter reset trigger | rack-reload-event | Automation Engineer |
| CI-09 | LIMS connector poll interval | 60 s | IT |
| CI-10 | NTP server | `ntp.iris.local` | IT |

## 6. Risks (FS-level)

Inherited from URS § 9. Additional FS-specific risks:

- VENUS SCN regression of capacitive level-sense calibration → mitigation: post-upgrade OQ of FS-ERR-01 + FS-CAL-03.
- Method-author writes Python-side SDK code that bypasses VENUS audit-trail → mitigation: FS-MTH-04 + code review checklist `IRS-SOP-LH-CODE-REVIEW-001`.
- LIMS connector silently drops result on schema mismatch → mitigation: FS-INT-LIMS-01 alert-on-mismatch.

## 7. References

- IRS-URS-LH-001 v1.2 (parent URS).
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192.
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- ISO 8655 (parts 1-7); USP <41>, USP <1251>, USP <1058>.
- ICH Q2(R2); ICH Q9(R1); PIC/S PI 041.
- ISPE GAMP 5 (2nd Edition, 2022); GAMP GPG *Validation of Laboratory Computerized Systems*.
- Hamilton — *Microlab STAR + VENUS 6.x Configuration Reference*; *VENUS SDK Reference*.

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-PLAT-01 | FS-PLAT-01 |
| URS-PLAT-02 | FS-PLAT-02 |
| URS-PLAT-03 | FS-PLAT-03 |
| URS-SW-01 | FS-SW-01 |
| URS-SW-02 | FS-SW-02 |
| URS-MTH-01 | FS-MTH-01 |
| URS-MTH-02 | FS-MTH-02 |
| URS-MTH-03 | FS-MTH-03 |
| URS-MTH-04 | FS-MTH-04 |
| URS-WL-01 | FS-WL-01 |
| URS-WL-02 | FS-WL-02 |
| URS-WL-03 | FS-WL-03 |
| URS-WL-04 | FS-WL-04 |
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
| URS-INT-LIMS-01 | FS-INT-LIMS-01 |
| URS-INT-AD-01 | FS-INT-AD-01 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-BAK-03 | FS-BAK-03 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-PR-02 | FS-PR-02 |
| URS-DECK-01 | FS-DECK-01 |
| URS-DECK-02 | FS-DECK-02 |
| URS-DECK-03 | FS-DECK-03 |
| URS-DECK-04 | FS-DECK-04 |
| URS-DECK-05 | FS-DECK-05 |
| URS-LQC-01 | FS-LQC-01 |
| URS-LQC-02 | FS-LQC-02 |
| URS-LQC-03 | FS-LQC-03 |
| URS-LQC-04 | FS-LQC-04 |
| URS-ERR-01 | FS-ERR-01 |
| URS-ERR-02 | FS-ERR-02 |
| URS-ERR-03 | FS-ERR-03 |
| URS-ERR-04 | FS-ERR-04 |
| URS-ERR-05 | FS-ERR-05 |
| URS-CAL-01 | FS-CAL-01 |
| URS-CAL-02 | FS-CAL-02 |
| URS-CAL-03 | FS-CAL-03 |
| URS-CAL-04 | FS-CAL-04 |
| URS-CHO-01 | FS-CHO-01 |
| URS-CHO-02 | FS-CHO-02 |
| URS-CHO-03 | FS-CHO-03 |
| URS-CONT-01 | FS-CONT-01 |
| URS-CONT-02 | FS-CONT-02 |
| URS-CONT-03 | FS-CONT-03 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Method defect causing wrong volume / wrong well | Medium | High | URS-MTH-01 + dry-run on simulator + accuracy verification on instrument |
| R-02 | Calibration drift undetected | Medium | High | URS-PLAT-03 + URS-WL-02 + URS-CAL-01 + URS-CAL-04 (trending) |
| R-03 | Operator running with non-EFFECTIVE method | Low | High | URS-MTH-02 + run-time gate |
| R-04 | Audit-trail tampering | Low | Critical | URS-AUD-02 |
| R-05 | Tip-pickup failure leading to dry-channel dispense (no liquid delivered to well) | Medium | High | URS-ERR-01 (capacitive verification) |
| R-06 | Deck-position drift causing labware mis-aspiration | Low | Critical | URS-DECK-04 (drift check at PM) |
| R-07 | Labware mis-identification (operator places wrong plate in deck slot) | Medium | High | URS-DECK-03 (pre-run verification with prompt or RFID) |
| R-08 | Liquid-class mismatch (viscous reagent run under aqueous settings → wrong volume delivered) | Medium | High | URS-LQC-02 (static analysis at method-promotion) |
| R-09 | Sample-to-sample cross-over via re-used tips for GxP runs | Low | Critical | URS-CONT-01 |
| R-10 | Method-import drift between VENUS simulator and instrument (script behaves differently on hardware) | Medium | High | URS-MTH-01 (wet-run accuracy verification required before promotion) |
| R-11 | ISO 8655 calibration lapse undetected, channel used beyond verification window | Low | Critical | URS-CAL-02 (block on expired) |
| R-12 | Reagent-lot tracking failure (run completed without recording lot information for traceability) | Low | High | URS-DECK-05 |
| R-13 | Mid-run abort with incomplete provenance capture | Low | High | URS-ERR-05 |

Full evaluation in `IRS-RA-LH-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
