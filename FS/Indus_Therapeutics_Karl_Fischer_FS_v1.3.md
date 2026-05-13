---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "IND-URS-CKF-001 (parent URS) v1.2"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11; EU GMP Annex 11"
  - "USP <921> Method Ic; USP <1058>; Ph. Eur. 2.5.32"
parent_urs:
  document_number: IND-URS-CKF-001
  version: 1.2
  file: ../../URS/_generated/Coulometric_Karl_Fischer_Computer_System__Indus_Therapeutics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Coulometric Karl Fischer Computer System — Mettler Toledo C30S + LabX 2024

**Document Number:** IND-FS-CKF-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** IND-URS-CKF-001 v1.2 | **Site:** Indus Therapeutics (fictional)
**System Class:** GAMP Cat 4 — Configured Product
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; USP <921>; USP <1058>; Ph. Eur. 2.5.32; ICH Q2(R2); PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Chemical) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Approver (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | Expanded to match IND-URS-CKF-001 v1.2 (T1 — 40-req). Per-URS-ID rows for USP <921> compendial, AIQ per USP <1058>, SST drift+blank, reagent / titrant lifecycle, per-clause Part 11 + DI. Doc-number prefix aligned with URS (CKF). |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies the deployment, configuration, and integration of Mettler Toledo C30S coulometric KF titrator + LabX 2024 to satisfy `IND-URS-CKF-001` v1.2. Controlling input to `IND-CS-CKF-001`, `IND-RA-CKF-001`, IQ/OQ/PQ protocols, and `IND-RTM-CKF-001`.

## 2. Scope

Mirrors the URS: one C30S titrator + LabX 2024 on a dedicated workstation (Win 11 Pro 23H2); AD authentication; LIMS integration; daily backup; NTP sync; USP <921> SST + drift + blank management; reagent / titrant register. Out: sample preparation; LIMS sample-lifecycle.

## 3. System Architecture

```
   AD/NTP ──► LabX 2024 Workstation ──► Mettler Toledo C30S
                  │
                  ├─► Reagent / Titrant Register (anolyte / catholyte / water std)
                  └─► LabWare LIMS 8 (worklist + result push, SST-gated)
```

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source | Notes |
|---|---|---|---|---|---|
| C-01 | LabX 2024 + LIMS Connector | App SW | 4 | Mettler Toledo | 21 CFR Part 11 module enabled |
| C-02 | Mettler Toledo C30S | Instrument FW | 4 | Mettler Toledo | Coulometric KF, diaphragm cell |
| C-03 | Windows 11 Pro 23H2 | OS | 1 | Microsoft | Domain-joined |
| C-04 | LabWare LIMS 8 connector | Interface | 4 | Mettler + LabWare | Worklist + result push |
| C-05 | Reagent / Titrant Register | Config | 4 | Site | Anolyte + catholyte + water std lots |

## 4. Functional Specifications

| FS ID | URS ID | Specification |
|---|---|---|
| FS-HW-01 | URS-HW-01 | Workstation `ind-ckf-ws-01` reserved exclusively for LabX-KF; no other lab app installed. |
| FS-HW-02 | URS-HW-02 | Lenovo ThinkCentre M70t, 16 GB RAM, 512 GB NVMe; APC SMT750 UPS for ≥ 30 min controlled shutdown. |
| FS-HW-03 | URS-HW-03 | Bench-top humidity sensor reporting to EMS; alarm threshold 65% RH; high-RH events logged. |
| FS-SW-01 | URS-SW-01 | Windows 11 Pro 23H2, joined to `indus.local`; AD baseline GPO `IND-LAB-USERS-WS`. |
| FS-SW-02 | URS-SW-02 | LabX 2024 + LIMS Connector installed by Mettler engineer; install record retained. |
| FS-SW-03 | URS-SW-03 | LabX project storage on `\\ind-gmp-fs01\labx-projects`; local-C: write blocked for GxP via NTFS ACL. |
| FS-SW-04 | URS-SW-04 | Windows Time Service synced to `ntp.indus.local`; skew alert at > 1000 ms. |
| FS-SW-05 | URS-SW-05 | LabX project policy `IND_CKF_PART11` applied: audit trail required, eSign required, raw data lock; CS documents values. |
| FS-CMP-01 | URS-CMP-01 | LabX method template `IND-METH-USP921-IC` configured with Method Ic stoichiometry (96485 C/mol); iodine generation current configurable per cell type. |
| FS-CMP-02 | URS-CMP-02 | EP-monograph methods carry `Compendium=EP`; Ph. Eur. 2.5.32 control criteria mandatory at SST. |
| FS-CMP-03 | URS-CMP-03 | SST template enforces water-standard recovery within ± 3% of nominal per USP <921>; out-of-spec verdict blocks runs. |
| FS-CMP-04 | URS-CMP-04 | Method header `compendium` enum (USP / EP / JP / NON-COMP). |
| FS-AIQ-01 | URS-AIQ-01 | DQ `IND-DQ-CKF-001` captures intended-use, working range (1 µg–1000 mg H₂O), compendial monographs, Part 11 binding. |
| FS-AIQ-02 | URS-AIQ-02 | IQ `IND-IQ-CKF-001` verifies install, AD bind, LabX build hash, cell installation, electrode integrity (generator + indicator). |
| FS-AIQ-03 | URS-AIQ-03 | OQ `IND-OQ-CKF-001` battery: cell-drift verification; blank determination; water-standard recovery accuracy (± 3% at 100 µg + 1000 µg); precision (RSD ≤ 3% on 5 replicate water-standard injections); linearity 10–1000 µg. |
| FS-AIQ-04 | URS-AIQ-04 | PQ `IND-PQ-CKF-001` scheduled at go-live, after cell-fluid replacement, after electrode replacement, after software upgrade, annually. |
| FS-SST-01 | URS-SST-01 | LabX SST workflow `IND-SST-DRIFT` measures drift via 5-min stabilisation; threshold 25 µg/min routine, 10 µg/min low-water methods; over-threshold → BLOCK. |
| FS-SST-02 | URS-SST-02 | Water-standard recovery sub-step within SST: 100 µg Hydranal standard; verdict (mean − nominal) / nominal × 100; fail outside ± 3%; instrument → NOT_READY. |
| FS-SST-03 | URS-SST-03 | Blank determination per method cadence; blank value bound to acquisition record; over-threshold blank fires deviation. |
| FS-SST-04 | URS-SST-04 | Rolling 30-day drift + blank trend table; 7-day rolling-avg early-warning band at ½ SOP threshold; alert via Site EMS dashboard. |
| FS-SST-05 | URS-SST-05 | SST log schema: op_id, ts, water_std_lot, cert_expiry, drift_value, blank_value, recovery_pct, verdict; immutable. |
| FS-REA-01 | URS-REA-01 | Reagent Register schema: lot, source, COA_id, receipt_date, opening_date, expiry, custodian; integrated with LabX cell-change workflow. |
| FS-REA-02 | URS-REA-02 | Pre-flight check evaluates bound anolyte / catholyte expiry; expired lot → BLOCK with reason `REA_EXPIRED`. |
| FS-REA-03 | URS-REA-03 | Cell-fluid-change workflow `IND-WF-CELL-CHANGE` requires operator entry of new lot_id + opened_date before next run. |
| FS-REA-04 | URS-REA-04 | Water-standard register entries (Hydranal 1.0 / 10 / 100 / 1000); expired standard → BLOCK at SST. |
| FS-REA-05 | URS-REA-05 | Cell-waste disposal log entry `IND-LOG-WASTE` mandatory before register entry transitions to DISPOSED. |
| FS-METH-01 | URS-METH-01 | LabX method lifecycle states mapped DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE. |
| FS-METH-02 | URS-METH-02 | Method state-transition e-sign requires AD group `IND-CKF-METHOD-APPROVER`; Author identity excluded from Approver list. |
| FS-RUN-01 | URS-RUN-01 | Pre-flight checker evaluates drift > threshold, SST overdue/failed, expired reagent / standard, method ≠ EFFECTIVE, project locked; any TRUE → BLOCK. |
| FS-RUN-02 | URS-RUN-02 | Acquisition metadata schema: sample_id, sample_weight, blank_correction, method_id + version, instrument_id, analyst_id, ts. |
| FS-RUN-03 | URS-RUN-03 | RFC dialog mandatory on manual reweigh / re-run; minimum 10-character free text + RFC category dropdown. |
| FS-RUN-04 | URS-RUN-04 | Replicate-RSD evaluator computes mean + RSD per method-defined n; reject when RSD > method limit. |
| FS-PROC-01 | URS-PROC-01 | Processing engine applies mean + %RSD across replicates and applies blank correction at the recipe-defined formula. |
| FS-PROC-02 | URS-PROC-02 | Raw data table append-only; reprocessing emits derived `.proc` referencing parent raw_id. |
| FS-PROC-03 | URS-PROC-03 | OOS evaluator compares reportable_result vs method spec; flag bands at 30% / 50% / 100% of limit. |
| FS-PROC-04 | URS-PROC-04 | PDF report template `IND-RPT-CKF` includes raw replicates, mean, RSD, blank, drift, water-std recovery, limit status, ALCOA+ block, SHA-256 hash. |
| FS-AUD-01 | URS-AUD-01 | Audit-trail event coverage: methods, sequences, results, configuration, reagent register, sign-on/off, SST events. |
| FS-AUD-02 | URS-AUD-02 | Audit-trail DB constraint = append-only; delete grant revoked at DBA + vendor level. |
| FS-AUD-03 | URS-AUD-03 | Per-batch review by Senior Analyst (`IND-AUD-REVIEW-CKF-BATCH`); monthly by QC Manager (`IND-AUD-REVIEW-CKF-MONTH`). |
| FS-AUD-04 | URS-AUD-04 | Retention 25 y on product-release-linked records; 7 y default; archival job `IND-JOB-ARCH-CKF`. |
| FS-PART11-01 | URS-PART11-01 | § 11.10(a) procedural controls: SOP `IND-SOP-CC-CKF` + SOP `IND-SOP-IR-CKF` referenced. |
| FS-PART11-02 | URS-PART11-02 | § 11.10(d) access: AD-mapped roles per § 4 of URS; quarterly access review. |
| FS-PART11-03 | URS-PART11-03 | § 11.50 e-sign manifestation: username, datetime (NTP), meaning. |
| FS-PART11-04 | URS-PART11-04 | § 11.70 signature/record linking: cryptographic hash binding. |
| FS-PART11-05 | URS-PART11-05 | § 11.100 uniqueness: AD UPN unique identifier. |
| FS-PART11-06 | URS-PART11-06 | § 11.200 re-auth: re-entry of password at every Approve action. |
| FS-PART11-07 | URS-PART11-07 | § 11.300 password policy: AD GPO `IND-LAB-USERS-PWD` (12-char min, 3-of-4 complexity, 90 d). |
| FS-DI-01 | URS-DI-01 | Attributable: op_id captured per event. |
| FS-DI-02 | URS-DI-02 | Legible: report renderer enforces font/min-size; PDF/A export. |
| FS-DI-03 | URS-DI-03 | Contemporaneous: NTP timestamps per FS-SW-04. |
| FS-DI-04 | URS-DI-04 | Original: raw titration curve `.cur` files preserved. |
| FS-DI-05 | URS-DI-05 | Accurate: SST + drift + blank gate verified per OQ. |
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | LabX LIMS Connector polls LIMS worklist endpoint every 5 min; read-only. |
| FS-INT-LIMS-02 | URS-INT-LIMS-02 | Result push triggered only on `result_state=APPROVED`; rejected push emits LIMS error code `IND-CKF-NOT-APPROVED`. |
| FS-INT-LIMS-03 | URS-INT-LIMS-03 | Pre-push checker evaluates SST_status; block on SST_FAIL / SST_EXPIRED. |
| FS-BAK-01 | URS-BAK-01 | Daily backup job `IND-JOB-BAK-CKF` to Site backup target; backed-up: methods, raw curves, audit DB, reagent register. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore drill `IND-SOP-RESTORE-TEST`; QA-witnessed. |
| FS-PERF-01 | URS-PERF-01 | Tested at PQ: sustained batch of 24 samples with no crash or data loss. |
| FS-SEC-01 | URS-SEC-01 | AD bind via LDAPS; break-glass account `IND-BG-CKF` vaulted in CyberArk. |
| FS-SEC-02 | URS-SEC-02 | Removable-media GPO `IND-LAB-USB-BLOCK`; engineering override via change-control. |
| FS-TRN-01 | URS-TRN-01 | LMS courses: `IND-CKF-101` (analyst), `IND-CKF-201` (SST + reagent lifecycle); annual re-completion required. |
| FS-PR-01 | URS-PR-01 | Periodic review template `IND-PR-CKF`: method inventory, audit-trail review evidence, SST + reagent register health, deviations, training; sign-off QC Manager + Head of QA. |


### 4.1 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem. Conditional-access binding to policy `Lab-Workstation Conditional Access (MFA on interactive logon)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam file-level capture of the per-instrument result store and method library; tier classification = T3; RPO ≤ 72 h; RTO ≤ 72 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; annual QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Configuration Items

| CI ID | Item | Value |
|---|---|---|
| CI-01 | LabX Part 11 module | Enabled; project policy IND_CKF_PART11 |
| CI-02 | Drift threshold | 25 µg/min routine; 10 µg/min low-water methods |
| CI-03 | Water-standard recovery limit | ± 3% nominal per USP <921> |
| CI-04 | Trend early-warning band | ½ SOP threshold; 7-day rolling avg |
| CI-05 | Backup retention | 25 y product-release-linked; 7 y default |
| CI-06 | Audit-trail review cadence | Per batch (Senior Analyst); monthly (QC Manager) |
| CI-07 | Re-qualification trigger matrix | Cell-fluid / electrode / software change → full PQ; routine PM → SST partial |

## 6. Risks (FS-level)

| ID | Risk | Mitigation |
|---|---|---|
| FR-01 | Cell drift bias on long batch | FS-SST-01 + FS-SST-04 trend |
| FR-02 | LIMS push of unapproved / SST-failed | FS-INT-LIMS-02 + FS-INT-LIMS-03 |
| FR-03 | Audit-trail tampering | FS-AUD-02 append-only |
| FR-04 | Expired anolyte / catholyte | FS-REA-02 pre-flight block |
| FR-05 | Expired water standard giving false SST pass | FS-REA-04 + FS-SST-02 |
| FR-06 | Blank-correction drift across campaign | FS-SST-03 + FS-SST-04 trend |
| FR-07 | Cell back-flow contamination | FS-REA-03 cell-change workflow + cell-maintenance SOP |

## 7. References

IND-URS-CKF-001 v1.2; 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .194; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <921>; USP <1058>; Ph. Eur. 2.5.32; ICH Q2(R2); PIC/S PI 041; ISPE GAMP 5 (2nd ed., 2022); Mettler Toledo — *C30S + LabX 2024 Reference*.

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-HW-01 | FS-HW-01 |
| URS-HW-02 | FS-HW-02 |
| URS-HW-03 | FS-HW-03 |
| URS-SW-01 | FS-SW-01 |
| URS-SW-02 | FS-SW-02 |
| URS-SW-03 | FS-SW-03 |
| URS-SW-04 | FS-SW-04 |
| URS-SW-05 | FS-SW-05 |
| URS-CMP-01 | FS-CMP-01 |
| URS-CMP-02 | FS-CMP-02 |
| URS-CMP-03 | FS-CMP-03 |
| URS-CMP-04 | FS-CMP-04 |
| URS-AIQ-01 | FS-AIQ-01 |
| URS-AIQ-02 | FS-AIQ-02 |
| URS-AIQ-03 | FS-AIQ-03 |
| URS-AIQ-04 | FS-AIQ-04 |
| URS-SST-01 | FS-SST-01 |
| URS-SST-02 | FS-SST-02 |
| URS-SST-03 | FS-SST-03 |
| URS-SST-04 | FS-SST-04 |
| URS-SST-05 | FS-SST-05 |
| URS-REA-01 | FS-REA-01 |
| URS-REA-02 | FS-REA-02 |
| URS-REA-03 | FS-REA-03 |
| URS-REA-04 | FS-REA-04 |
| URS-REA-05 | FS-REA-05 |
| URS-METH-01 | FS-METH-01 |
| URS-METH-02 | FS-METH-02 |
| URS-RUN-01 | FS-RUN-01 |
| URS-RUN-02 | FS-RUN-02 |
| URS-RUN-03 | FS-RUN-03 |
| URS-RUN-04 | FS-RUN-04 |
| URS-PROC-01 | FS-PROC-01 |
| URS-PROC-02 | FS-PROC-02 |
| URS-PROC-03 | FS-PROC-03 |
| URS-PROC-04 | FS-PROC-04 |
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
| URS-INT-LIMS-01 | FS-INT-LIMS-01 |
| URS-INT-LIMS-02 | FS-INT-LIMS-02 |
| URS-INT-LIMS-03 | FS-INT-LIMS-03 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
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
| R-01 | Cell drift bias on a long batch (failure to detect mid-batch contamination) | Medium | High | URS-SST-01 + URS-SST-04 trend |
| R-02 | LIMS push of unapproved result | Medium | High | URS-INT-LIMS-02 + URS-INT-LIMS-03 |
| R-03 | Audit-trail tampering | Low | High | URS-AUD-02 |
| R-04 | Expired anolyte / catholyte producing biased result | Medium | High | URS-REA-01 + URS-REA-02 |
| R-05 | Water-standard expired or contaminated (false SST pass) | Low | High | URS-REA-04 + URS-SST-02 |
| R-06 | Titrant contamination from cell back-flow (catholyte contamination of anolyte at the diaphragm) | Low | High | URS-REA-03 (lot tracking) + cell-maintenance SOP |
| R-07 | Sample-weight transcription error on direct sample injection | Medium | Medium | URS-RUN-02 (balance integration where applicable) |
| R-08 | Blank-correction drift over a long campaign | Medium | High | URS-SST-03 + URS-SST-04 trend |

Full evaluation in `IND-RA-CKF-001` *(synthetic)*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
