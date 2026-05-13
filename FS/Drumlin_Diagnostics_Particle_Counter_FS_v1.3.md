---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "DRD-URS-PCL-001 (parent URS) v1.2"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11; EU GMP Annex 11"
  - "USP <788>; USP <789>; USP <1058>; Ph. Eur. 2.9.19; ISO 21501-3:2019"
parent_urs:
  document_number: DRD-URS-PCL-001
  version: 1.2
  file: ../../URS/_generated/Particle_Counter_Liquid_Computer_System__Drumlin_Diagnostics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Liquid Particle Counter Computer System — Beckman Coulter HIAC 9703+ + PharmSpec 5

**Document Number:** DRD-FS-PCL-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** DRD-URS-PCL-001 v1.2 | **Site:** Drumlin Diagnostics (fictional)
**System Class:** GAMP Cat 4 — Configured Product
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; USP <788>; USP <789>; USP <1058>; Ph. Eur. 2.9.19; ISO 21501-3:2019; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Particulates) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Approver (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | Expanded to match DRD-URS-PCL-001 v1.2 (T1 — 45-req). Per-URS-ID rows for USP <788>/<789>/Ph.Eur.2.9.19/ISO 21501-3 compendial, AIQ per USP <1058>, SST + counted-bead, reference standard register, sample-handling controls, per-clause Part 11 + DI. Doc-number prefix aligned with URS (DRD-PCL); instrument harmonised to HIAC 9703+. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies the deployment, configuration, and integration of Beckman Coulter HIAC 9703+ + PharmSpec 5 to satisfy `DRD-URS-PCL-001` v1.2. Controlling input to `DRD-CS-PCL-001`, `DRD-RA-PCL-001`, IQ/OQ/PQ protocols, and `DRD-RTM-PCL-001`.

## 2. Scope

HIAC 9703+ instrument + PharmSpec 5 on a dedicated workstation (Win 11 Pro 23H2); AD authentication; LIMS integration; daily backup; NTP sync; USP <788> SST + counted-bead reference verification; reference-standard register. Out: sample preparation; off-line size-standard calibration chain; LIMS sample-lifecycle.

## 3. System Architecture

```
   AD/NTP ──► PharmSpec 5 Workstation ──► HIAC 9703+ (auto-sampler)
                  │                          │
                  ├─► NIST-traceable Counted-Bead + Sizing-Bead Register
                  ├─► Diluent / Particle-Free Water Register
                  └─► LabWare LIMS 8 (worklist + result push, SST-gated)
```

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source | Notes |
|---|---|---|---|---|---|
| C-01 | PharmSpec 5 + LIMS Connector 4 | App SW | 4 | Beckman Coulter | 21 CFR Part 11 module enabled |
| C-02 | Beckman Coulter HIAC 9703+ | Instrument FW | 4 | Beckman Coulter | LO sensor + syringe pump + auto-sampler |
| C-03 | Windows 11 Pro 23H2 | OS | 1 | Microsoft | Domain-joined |
| C-04 | LabWare LIMS 8 connector | Interface | 4 | Beckman + LabWare | Worklist + result push |
| C-05 | Reference Standard Register | Config | 4 | Site | NIST-traceable counted + sizing beads |
| C-06 | Diluent / particle-free water register | Config | 4 | Site | Per-lot blank verification |

## 4. Functional Specifications

| FS ID | URS ID | Specification |
|---|---|---|
| FS-HW-01 | URS-HW-01 | Workstation `drd-pcl-ws-01` reserved exclusively for PharmSpec 5; no other GxP app. |
| FS-HW-02 | URS-HW-02 | Dell OptiPlex 7080 meeting PharmSpec 5 minimum spec; install record retained. |
| FS-HW-03 | URS-HW-03 | APC SMT1500 UPS for ≥ 30 min controlled shutdown. |
| FS-HW-04 | URS-HW-04 | Reference standard register entries (NIST-traceable counted bead + sizing bead suspensions) maintained per § FS-REF-*. |
| FS-HW-05 | URS-HW-05 | Instrument bench sited in ISO Class 8 (or better) area; background particulate monitored. |
| FS-SW-01 | URS-SW-01 | Windows 11 Pro 23H2 joined to `drumlin.local`; AD baseline GPO `DRD-LAB-WS-23H2`. |
| FS-SW-02 | URS-SW-02 | PharmSpec 5 installed by Beckman Coulter engineer; install record retained. |
| FS-SW-03 | URS-SW-03 | PharmSpec project storage on `\\drd-gmp-fs01\hiac-projects`; local C: write blocked. |
| FS-SW-04 | URS-SW-04 | Windows Time Service → `ntp.drumlin.local`; skew alert > 1000 ms. |
| FS-SW-05 | URS-SW-05 | PharmSpec project policy `DRD_PCL_PART11`: audit trail required, eSign required, raw data lock. |
| FS-SW-06 | URS-SW-06 | PharmSpec SCN applied under change-control `CCR-PCL-*`; build hash verified at partial-OQ. |
| FS-CMP-01 | URS-CMP-01 | USP <788> Method 1 acceptance evaluator: LVP per-mL limits (25 / 3); SVP cumulative per-container limits (6000 / 600); per-method selection of LVP-vs-SVP rule. |
| FS-CMP-02 | URS-CMP-02 | USP <789> acceptance evaluator: 50 / 5 / 2 per mL at ≥ 10 / ≥ 25 / ≥ 50 µm. |
| FS-CMP-03 | URS-CMP-03 | EP-monograph methods carry `Compendium=EP`; Ph. Eur. 2.9.19 Test 1A / 1B logic applied. |
| FS-CMP-04 | URS-CMP-04 | ISO 21501-3 performance criteria verified at OQ: size accuracy ± 10% at calibrated channels; counting efficiency 50% ± 20% at threshold + 100% ± 10% above 1.5× threshold; coincidence loss ≤ 10% at operational concentration. |
| FS-CMP-05 | URS-CMP-05 | Method header `compendium` enum (USP / EP / JP / NON-COMP). |
| FS-AIQ-01 | URS-AIQ-01 | DQ `DRD-DQ-PCL-001` captures intended-use, channels, working range. |
| FS-AIQ-02 | URS-AIQ-02 | IQ `DRD-IQ-PCL-001` verifies install, AD bind, PharmSpec build, sensor + syringe-pump install. |
| FS-AIQ-03 | URS-AIQ-03 | OQ `DRD-OQ-PCL-001` battery: size accuracy (10 + 25 µm NIST sizing beads); counting accuracy (counted-bead suspension); sample-volume gravimetric ± 1%; sensor blank; resolution; coincidence-loss verification. |
| FS-AIQ-04 | URS-AIQ-04 | PQ `DRD-PQ-PCL-001` scheduled at go-live, after sensor / pump replacement, annually. |
| FS-AIQ-05 | URS-AIQ-05 | Partial PQ (SST only) permitted after PM not affecting the sensor. |
| FS-AIQ-06 | URS-AIQ-06 | Qualification evidence on `\\drd-gmp-fs01\pcl-qual` with WORM bit; retention 25 y. |
| FS-SST-01 | URS-SST-01 | SST workflow `DRD-SST-USP788`: (a) counted-bead suspension recovery within ± 10% of nominal; (b) sensor blank ≤ method limit; (c) gravimetric sample-volume ± 1%; verdict block-on-fail. |
| FS-SST-02 | URS-SST-02 | SST record schema: op_id, ts, counted_bead_lot, cert_expiry, blank_volume_passed, recovery_pct, verdict; immutable. |
| FS-SST-03 | URS-SST-03 | SST FAIL → FSM NOT_READY; sequence runner blocks; override requires `DRD-PCL-QA-APPROVER` co-sign + RFC. |
| FS-SST-04 | URS-SST-04 | Rolling 12-month SST trend; early-warning band at ± 7% recovery; alert via Site dashboard. |
| FS-SST-05 | URS-SST-05 | Monthly audit-trail review template includes "SST trend review" step with sign-off. |
| FS-REF-01 | URS-REF-01 | Reference Standard Register schema: rs_id, type (counted-bead / sizing-bead), source, lot, COA_id, NIST_traceability_flag, receipt_date, opening_date, expiry, custodian. |
| FS-REF-02 | URS-REF-02 | SST pre-flight rejects when bound rs_id expired; rejection logged. |
| FS-REF-03 | URS-REF-03 | SST execution captures bound rs_id; mandatory field. |
| FS-REF-04 | URS-REF-04 | Disposal log entry mandatory before register transitions to DISPOSED. |
| FS-SAMP-01 | URS-SAMP-01 | Diluent / particle-free water register: lot, receipt_date, certificate-clean state, opening_date, expiry; per-batch verification at session start. |
| FS-SAMP-02 | URS-SAMP-02 | Sampling-mode bound (open-cup / closed); environment particulate background ISO Class 8 minimum enforced via facility EMS. |
| FS-SAMP-03 | URS-SAMP-03 | Acquisition record `degassing_applied=true/false`; bubble-detection routine flags suspect counts in ≥ 25 µm channel. |
| FS-SAMP-04 | URS-SAMP-04 | Method-defined `transfer_protocol` field: probe immersion depth (mm), swirl pattern; analyst training required (per FS-TRN-01). |
| FS-ACQ-01 | URS-ACQ-01 | PharmSpec method lifecycle states mapped DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE. |
| FS-ACQ-02 | URS-ACQ-02 | Pre-flight checker evaluates instrument_state, SST_state, method_state, project_lock, ref_std_expiry, diluent_expiry; any TRUE blocks. |
| FS-ACQ-03 | URS-ACQ-03 | Acquisition metadata schema: sample_id, dilution_factor, vessel_id, replicate_count, method_id+version, instrument_id, analyst_id, ts. |
| FS-PROC-01 | URS-PROC-01 | Processing engine applies USP <788> replicate averaging + outlier handling; method-bound first-replicate discard rule. |
| FS-PROC-02 | URS-PROC-02 | RFC dialog mandatory on manual reprocessing. |
| FS-PROC-03 | URS-PROC-03 | Raw data `.psr` files preserved; derived `.proc` references parent raw_id. |
| FS-PROC-04 | URS-PROC-04 | Limit-band evaluator: 30% / 50% / 100% of compendial limit; TREND / OOT / OOS flags. |
| FS-PROC-05 | URS-PROC-05 | PDF report `DRD-RPT-PCL` includes raw counts per replicate + per channel, dilution-corrected counts, SST status, limit status, ALCOA+ block, SHA-256 hash. |
| FS-PROC-06 | URS-PROC-06 | OOS flag triggers LIMS workflow `LIMS-WF-211192`; sample-state transitions to HOLD. |
| FS-AUD-01 | URS-AUD-01 | Audit-trail event coverage: methods, sequences, results, configuration, ref-std register, sign-on/off, SST events. |
| FS-AUD-02 | URS-AUD-02 | Audit-trail DB constraint = append-only. |
| FS-AUD-03 | URS-AUD-03 | Per-batch review by Senior Analyst; monthly by QC Manager. |
| FS-AUD-04 | URS-AUD-04 | Retention 25 y product-release-linked; 7 y default; archival job `DRD-JOB-ARCH-PCL`. |
| FS-PART11-01 | URS-PART11-01 | § 11.10(a) procedural controls: SOP `DRD-SOP-CC-PCL` + `DRD-SOP-IR-PCL`. |
| FS-PART11-02 | URS-PART11-02 | § 11.10(d) access: AD-mapped roles; quarterly access review. |
| FS-PART11-03 | URS-PART11-03 | § 11.50 e-sign manifestation: username, datetime (NTP), meaning. |
| FS-PART11-04 | URS-PART11-04 | § 11.70 signature/record linking: cryptographic hash. |
| FS-PART11-05 | URS-PART11-05 | § 11.100 uniqueness: AD UPN. |
| FS-PART11-06 | URS-PART11-06 | § 11.200 re-auth: re-entry of password at every Approve. |
| FS-PART11-07 | URS-PART11-07 | § 11.300 password policy: AD GPO `DRD-LAB-USERS-PWD` (12-char, complexity, 90 d, 5-attempt lockout). |
| FS-DI-01 | URS-DI-01 | Attributable: op_id captured per event. |
| FS-DI-02 | URS-DI-02 | Legible: PDF/A export. |
| FS-DI-03 | URS-DI-03 | Contemporaneous: NTP timestamps. |
| FS-DI-04 | URS-DI-04 | Original: raw `.psr` files preserved. |
| FS-DI-05 | URS-DI-05 | Accurate: SST gate + counted-bead verification verified at OQ. |
| FS-DI-06 | URS-DI-06 | Complete: archival manifest verifies presence of raw + audit + signature + method-version. |
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | PharmSpec LIMS Connector 4 polls worklist endpoint every 5 min; read-only. |
| FS-INT-LIMS-02 | URS-INT-LIMS-02 | Result push triggered only on `result_state=APPROVED`. |
| FS-INT-LIMS-03 | URS-INT-LIMS-03 | LIMS payload includes report_id, instrument_id, method_id+version, reviewer_id, approver_id, sst_status. |
| FS-INT-LIMS-04 | URS-INT-LIMS-04 | Pre-push checker evaluates SST_state; block on FAIL / EXPIRED. |
| FS-BAK-01 | URS-BAK-01 | Daily backup job `DRD-JOB-BAK-PCL` with SHA-256 manifest. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore drill `DRD-SOP-RESTORE-TEST`; QC-witnessed. |
| FS-BAK-03 | URS-BAK-03 | RTO ≤ 8 h; RPO ≤ 24 h; verified at restore drill. |
| FS-PERF-01 | URS-PERF-01 | PQ scenario: typical batch session completes without crash or data loss. |
| FS-SEC-01 | URS-SEC-01 | AD bind via LDAPS; break-glass `DRD-BG-PCL` vaulted in CyberArk. |
| FS-SEC-02 | URS-SEC-02 | Removable-media GPO `DRD-LAB-USB-BLOCK`; engineering override via change-control. |
| FS-TRN-01 | URS-TRN-01 | LMS courses: `DRD-PCL-101` (analyst), `DRD-PCL-201` (SST + ref-std lifecycle); annual re-completion. |
| FS-PR-01 | URS-PR-01 | Periodic review template `DRD-PR-PCL`: method inventory, audit-trail evidence, SST trend, counted-bead register health, deviations, training; QC Manager + Head of QA sign-off. |


### 4.1 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem. Conditional-access binding to policy `Lab-Workstation Conditional Access (MFA on interactive logon)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam file-level capture of the per-instrument result store and configuration; tier classification = T3; RPO ≤ 72 h; RTO ≤ 72 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; annual QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Configuration Items

| CI ID | Item | Value |
|---|---|---|
| CI-01 | PharmSpec Part 11 module | Enabled; project policy DRD_PCL_PART11 |
| CI-02 | USP <788> default channels | ≥ 10 µm, ≥ 25 µm; extended channels enabled |
| CI-03 | LVP / SVP rule selection | Per method header |
| CI-04 | SST cadence | At session start (counted-bead + blank + volume) |
| CI-05 | ISO 21501-3 counting efficiency | 50% ± 20% @ threshold; 100% ± 10% above 1.5× threshold |
| CI-06 | Limit bands | 30% / 50% / 100% (TREND / OOT / OOS) |
| CI-07 | Re-qualification trigger matrix | Sensor / pump change → full PQ; routine PM → SST partial |
| CI-08 | Backup retention | 25 y product-release-linked; 7 y default |

## 6. Risks (FS-level)

| ID | Risk | Mitigation |
|---|---|---|
| FR-01 | Contaminated diluent | FS-SAMP-01 + FS-SST-01 sensor blank |
| FR-02 | SST not blocking on fail | FS-SST-03 + FS-ACQ-02 |
| FR-03 | LIMS push of unapproved / SST-failed | FS-INT-LIMS-02 + FS-INT-LIMS-04 |
| FR-04 | Audit-trail tampering | FS-AUD-02 append-only |
| FR-05 | Counter calibration drift (sensor aging) | FS-CMP-04 + FS-SST-04 trend |
| FR-06 | Coincidence loss at high concentration | FS-CMP-04 + FS-AIQ-03 |
| FR-07 | Air-bubble false-positives ≥ 25 µm | FS-SAMP-03 |
| FR-08 | Expired counted-bead lot | FS-REF-02 |
| FR-09 | High-particle environment background | FS-HW-05 + FS-SAMP-02 |

## 7. References

DRD-URS-PCL-001 v1.2; 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .192, .194; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <788>; USP <789>; USP <1058>; Ph. Eur. 2.9.19; ISO 21501-3:2019; PIC/S PI 041; ISPE GAMP 5 (2nd ed., 2022); Beckman Coulter — *HIAC 9703+ + PharmSpec 5 Reference*.

## 8. Appendix A — URS → FS Traceability Matrix

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
| URS-CMP-01 | FS-CMP-01 |
| URS-CMP-02 | FS-CMP-02 |
| URS-CMP-03 | FS-CMP-03 |
| URS-CMP-04 | FS-CMP-04 |
| URS-CMP-05 | FS-CMP-05 |
| URS-AIQ-01 | FS-AIQ-01 |
| URS-AIQ-02 | FS-AIQ-02 |
| URS-AIQ-03 | FS-AIQ-03 |
| URS-AIQ-04 | FS-AIQ-04 |
| URS-AIQ-05 | FS-AIQ-05 |
| URS-AIQ-06 | FS-AIQ-06 |
| URS-SST-01 | FS-SST-01 |
| URS-SST-02 | FS-SST-02 |
| URS-SST-03 | FS-SST-03 |
| URS-SST-04 | FS-SST-04 |
| URS-SST-05 | FS-SST-05 |
| URS-REF-01 | FS-REF-01 |
| URS-REF-02 | FS-REF-02 |
| URS-REF-03 | FS-REF-03 |
| URS-REF-04 | FS-REF-04 |
| URS-SAMP-01 | FS-SAMP-01 |
| URS-SAMP-02 | FS-SAMP-02 |
| URS-SAMP-03 | FS-SAMP-03 |
| URS-SAMP-04 | FS-SAMP-04 |
| URS-ACQ-01 | FS-ACQ-01 |
| URS-ACQ-02 | FS-ACQ-02 |
| URS-ACQ-03 | FS-ACQ-03 |
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
| URS-PART11-01 | FS-PART11-01 |
| URS-PART11-02 | FS-PART11-02 |
| URS-PART11-03 | FS-PART11-03 |
| URS-PART11-04 | FS-PART11-04 |
| URS-PART11-05 | FS-PART11-05 |
| URS-PART11-06 | FS-PART11-06 |
| URS-PART11-07 | FS-PART11-07 |
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
| URS-PERF-01 | FS-PERF-01 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-TRN-01 | FS-TRN-01 |
| URS-PR-01 | FS-PR-01 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Contaminated diluent driving false-fail | Medium | High | URS-SAMP-01 + URS-SST-01 (sensor blank) |
| R-02 | SST failure not blocking results | Medium | High | URS-SST-03 + URS-ACQ-02 |
| R-03 | LIMS push of unapproved / SST-failed result | Medium | High | URS-INT-LIMS-02 + URS-INT-LIMS-04 |
| R-04 | Audit-trail tampering | Low | High | URS-AUD-02 + URS-DI-06 |
| R-05 | Counter calibration drift (sensor aging — counting efficiency loss) | Medium | High | URS-CMP-04 + URS-SST-04 trend + URS-AIQ-04 annual PQ |
| R-06 | Coincidence loss at high-particle samples producing artificially-low counts | Low | High | URS-CMP-04 + URS-AIQ-03 (coincidence-loss verification) |
| R-07 | Air-bubble miscounting (false-positive ≥ 25 µm) | Medium | High | URS-SAMP-03 (degassing + bubble detection) |
| R-08 | Expired counted-bead suspension causing biased SST | Medium | High | URS-REF-01 + URS-REF-02 |
| R-09 | Sampling-environment background (open-cup mode in too-dirty area) | Medium | High | URS-HW-05 + URS-SAMP-02 |

Full evaluation in `DRD-RA-PCL-001` *(synthetic)*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
