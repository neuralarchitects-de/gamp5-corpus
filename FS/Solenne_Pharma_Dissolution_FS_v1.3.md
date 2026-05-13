---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "SOL-URS-DISSO-001 (parent URS) v1.2"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11; EU GMP Annex 11"
  - "USP <711>; USP <724>; USP <1058>; USP <1092>; Ph. Eur. 2.9.3"
parent_urs:
  document_number: SOL-URS-DISSO-001
  version: 1.2
  file: ../../URS/_generated/Dissolution_Apparatus_Computer_System__Solenne_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Dissolution Apparatus Computer System — Distek Evolution 6300 + ezfill 5300 + DissoTrack 5

**Document Number:** SOL-FS-DISSO-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** SOL-URS-DISSO-001 v1.2 | **Site:** Solenne Pharma (fictional)
**System Class:** GAMP Cat 4 — Configured Product
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; USP <711>; USP <724>; USP <1058>; USP <1092>; Ph. Eur. 2.9.3; Ph. Eur. 2.9.4; ICH Q4B Annex 7; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Solid Dosage) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Approver (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | Expanded to match SOL-URS-DISSO-001 v1.2 (T2 — 65-req). Per-URS-ID rows for USP <711>/<724>/Ph.Eur.2.9.3 compendial, AIQ per USP <1058>, Mechanical Qualification (paddle/basket alignment, wobble, vertical distance, vibration), Chemical Performance Test with USP Prednisone Tablets RS, media + reagent lifecycle, per-clause Part 11 + DI. Doc-number suffix aligned with URS (DISSO). |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies the deployment, configuration, and integration of Distek Evolution 6300 dissolution bath + ezfill 5300 + DissoTrack 5 to satisfy `SOL-URS-DISSO-001` v1.2. Controlling input to `SOL-CS-DISSO-001`, `SOL-RA-DISSO-001`, IQ/OQ/PQ protocols, and `SOL-RTM-DISSO-001`.

## 2. Scope

Distek Evolution 6300 bath + ezfill 5300 + DissoTrack 5 on a dedicated workstation (Win 11 Pro 23H2); UV-Vis sampling integration (offline Cary 60); AD authentication; LIMS integration; daily backup; NTP sync; USP <711> MQ + CPT; media + reagent register. Out: sample preparation; UV-Vis SDLC; LIMS sample-lifecycle.

## 3. System Architecture

```
   AD/NTP ──► DissoTrack 5 (PC, Win 11) ──► Distek Evolution 6300 + ezfill 5300
                  │                          │
                  ├─► USP Prednisone Tablets RS (CPT)
                  ├─► Media + Reagent Register
                  ├─► Vessel / Paddle / Basket Register
                  ├─► Cary 60 UV-Vis (offline readback)
                  └─► LabWare LIMS 8 (worklist + result push, MQ/CPT-gated)
```

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source | Notes |
|---|---|---|---|---|---|
| C-01 | DissoTrack 5 + LIMS Connector 2.1 | App SW | 4 | Distek | 21 CFR Part 11 module enabled |
| C-02 | Distek Evolution 6300 | Instrument FW | 4 | Distek | 6-vessel; Apparatus 1/2 default, 5/6/7 kit |
| C-03 | ezfill 5300 | Instrument FW | 4 | Distek | Automated media dispenser |
| C-04 | Windows 11 Pro 23H2 | OS | 1 | Microsoft | Domain-joined |
| C-05 | TruAlign fixture | Tool | (tool) | Distek | MQ alignment |
| C-06 | Agilent Cary 60 UV-Vis | External | (sep validation) | Agilent | Offline readback |
| C-07 | LabWare LIMS 8 | Interface | 4 | LabWare | Worklist + push |

## 4. Functional Specifications

| FS ID | URS ID | Specification |
|---|---|---|
| FS-HW-01 | URS-HW-01 | Workstation `sol-disso-ws-01` reserved exclusively for DissoTrack 5; no other GxP app. |
| FS-HW-02 | URS-HW-02 | HP Z2 Mini G9, 16 GB RAM, 1 TB SSD, 2× USB-3 ports for bath + ezfill comms. |
| FS-HW-03 | URS-HW-03 | APC SMT1500 UPS for ≥ 30 min controlled shutdown. |
| FS-HW-04 | URS-HW-04 | TruAlign-fixture-based mechanical verification executed at install + post-maintenance; results captured in MQ section (§ FS-MQ-*). |
| FS-HW-05 | URS-HW-05 | Bath probes calibrated against NIST-traceable reference; certificates archived; calibration interval per Site SOP. |
| FS-HW-06 | URS-HW-06 | Vessel / paddle / basket register schema: id, type, dim_measurements, qual_date, qual_evidence_path; integrated with DissoTrack at run binding. |
| FS-HW-07 | URS-HW-07 | Bath-level sensor + degas mode monitored; alarms wired into DissoTrack runtime. |
| FS-SW-01 | URS-SW-01 | Windows 11 Pro 23H2 joined to `solenne.local`; AD baseline GPO `SOL-LAB-WS-23H2`. |
| FS-SW-02 | URS-SW-02 | DissoTrack 5 + LIMS Connector 2.1 installed by Distek; install record retained. |
| FS-SW-03 | URS-SW-03 | DissoTrack project storage on `\\sol-gmp-fs01\disso-projects`; local C: write blocked via NTFS ACL. |
| FS-SW-04 | URS-SW-04 | Windows Time Service → `ntp.solenne.local`; w32time skew alert > 1000 ms. |
| FS-SW-05 | URS-SW-05 | GPO `SOL-LAB-LOCK` sets screen lock at 10 min idle. |
| FS-SW-06 | URS-SW-06 | DissoTrack project policy `SOL_DISSO_PART11`: audit trail, eSign, raw data lock. |
| FS-SW-07 | URS-SW-07 | DissoTrack SCN applied under change control `CCR-DISSO-*`; build hash verified at partial-OQ. |
| FS-CMP-01 | URS-CMP-01 | DissoTrack apparatus enum supports {1,2,3,4,5,6,7}; runtime binds method-defined apparatus + qualified vessel-kit at run start. |
| FS-CMP-02 | URS-CMP-02 | Per-vessel temperature sensor sampled at 1 Hz; out-of-band (37 °C ± 0.5 °C) raises alarm; alarm flagged in report. |
| FS-CMP-03 | URS-CMP-03 | RPM tachometer reads instantaneous shaft speed at 1 Hz; out-of-band (± 4% of set) raises deviation. |
| FS-CMP-04 | URS-CMP-04 | DissoTrack stage-evaluator implements USP <711> S1 / S2 / S3 logic per IR and ER acceptance tables; outcomes per run. |
| FS-CMP-05 | URS-CMP-05 | USP <724> acceptance applied when `apparatus ∈ {5,6,7}`. |
| FS-CMP-06 | URS-CMP-06 | EP-monograph methods carry `Compendium=EP`; Ph. Eur. 2.9.3 / 2.9.4 control criteria activated. |
| FS-CMP-07 | URS-CMP-07 | Method header `compendium` enum (USP / EP / JP / NON-COMP); rounding rules locked at method approval. |
| FS-AIQ-01 | URS-AIQ-01 | DQ `SOL-DQ-DISSO-001` captures intended-use, product portfolio (IR/ER/future transdermal). |
| FS-AIQ-02 | URS-AIQ-02 | IQ `SOL-IQ-DISSO-001` verifies install, AD bind, DissoTrack build hash, vessel set / paddle / basket installation, probe-cal certificates. |
| FS-AIQ-03 | URS-AIQ-03 | OQ `SOL-OQ-DISSO-001` battery: rotation accuracy ± 4%; temp accuracy 37 °C ± 0.5 °C; timer accuracy; ezfill dispense ± 1%; vibration; dissolved-oxygen check. |
| FS-AIQ-04 | URS-AIQ-04 | PQ `SOL-PQ-DISSO-001` includes CPT with USP Prednisone Tablets RS at go-live, post-mechanical maintenance, annually. |
| FS-AIQ-05 | URS-AIQ-05 | Partial PQ (CPT only) permitted after routine PM not affecting bath alignment. |
| FS-AIQ-06 | URS-AIQ-06 | Qualification evidence in `\\sol-gmp-fs01\disso-qual` with WORM bit; retention 25 y. |
| FS-MQ-01 | URS-MQ-01 | TruAlign centering pin / laser measures paddle / basket centering; pass ≤ 2 mm deviation from vessel center; record stored. |
| FS-MQ-02 | URS-MQ-02 | Wobble measurement using TruAlign fixture; pass ≤ 1.0 mm. |
| FS-MQ-03 | URS-MQ-03 | Vertical distance measured (vessel inside bottom → paddle/basket); pass = 25 ± 2 mm. |
| FS-MQ-04 | URS-MQ-04 | Bath level verified at MQ via spirit level + DissoTrack level sensor; alarm on out-of-level. |
| FS-MQ-05 | URS-MQ-05 | Vibration measured at vessel-holder plate at all operational RPM via accelerometer; verified within USP <711> acceptable limits. |
| FS-MQ-06 | URS-MQ-06 | Vessel verticality plumb-line check per vessel; pass within ± 0.5°. |
| FS-MQ-07 | URS-MQ-07 | MQ workflow `SOL-WF-MQ` triggers automatically on cell-fluid / paddle / basket maintenance event; results signed by MQ Engineer. |
| FS-CPT-01 | URS-CPT-01 | CPT method `SOL-CPT-PRED-50` configured: USP Prednisone Tablets RS, Apparatus 2 @ 50 rpm, 900 mL water, sampling at 30 min, n=6; acceptance per current USP CPT range. |
| FS-CPT-02 | URS-CPT-02 | CPT record schema: op_id, ts, RS_lot, cert_expiry, mean_Q, RSD, verdict; immutable. |
| FS-CPT-03 | URS-CPT-03 | CPT FAIL → product-runs blocked; FAIL record-id tagged on subsequent attempted runs until cleared. |
| FS-CPT-04 | URS-CPT-04 | Quarterly CPT trend review by QC Manager + MQ Engineer; OOT triggers MQ re-execution. |
| FS-MED-01 | URS-MED-01 | Media + reagent register schema: lot, source, COA_id, receipt_date, opening_date, expiry, custodian. |
| FS-MED-02 | URS-MED-02 | Pre-flight checker rejects run when bound media lot expired; rejection logged. |
| FS-MED-03 | URS-MED-03 | Prepared-media register: prep_date, prep_analyst, pH_verification_value, short-shelf-life expiry. |
| FS-MED-04 | URS-MED-04 | Method `degas` field captured; degas method (vacuum / helium sparge / sonication) bound; recorded per acquisition. |
| FS-MED-05 | URS-MED-05 | Waste log `SOL-LOG-WASTE-DISSO` mandatory before register entry transitions to DISPOSED. |
| FS-METH-01 | URS-METH-01 | DissoTrack method lifecycle states mapped DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE. |
| FS-METH-02 | URS-METH-02 | Method library NTFS ACL: read-only for `ERA-DISSO-ANALYST`; read-write for `ERA-DISSO-METHOD-OWNER`. |
| FS-METH-03 | URS-METH-03 | Method-change trigger on `apparatus` / `rotation` / `media` / `acceptance` field changes fires re-verification workflow `SOL-WF-METH-REVAL`. |
| FS-RUN-01 | URS-RUN-01 | Pre-flight checker evaluates temp, RPM, ezfill priming, project_lock, CPT_state, MQ_state, media_state; any block condition emits blocking-reason audit record. |
| FS-RUN-02 | URS-RUN-02 | Acquisition metadata schema: sample_ids, vessel_positions, method_id+version, instrument_id, analyst_id, ts_per_timepoint, media_lot, paddle_basket_id. |
| FS-RUN-03 | URS-RUN-03 | Per-vessel temp logged at 1 Hz throughout run; deviation events highlighted in report. |
| FS-RUN-04 | URS-RUN-04 | RFC dialog mandatory on manual sampling-time override; supervisor e-sig required; report flagged. |
| FS-RUN-05 | URS-RUN-05 | Media-replacement volume captured per timepoint when method `replace_media=true`. |
| FS-RES-01 | URS-RES-01 | LIMS Connector ingests UV-Vis or HPLC result per vessel × timepoint binding key. |
| FS-RES-02 | URS-RES-02 | Calculation engine applies method-defined equations; rounding rule from compendium-rounding lookup. |
| FS-RES-03 | URS-RES-03 | Stage evaluator (FS-CMP-04) progresses S1 → S2 → S3 per acceptance table; per-stage outcome captured. |
| FS-RES-04 | URS-RES-04 | PDF report template `SOL-RPT-DISSO`: sample metadata, method, analyst, reviewer, approver, per-vessel × per-timepoint values, stage outcome, CPT + MQ status, ALCOA+ block, SHA-256 hash. |
| FS-RES-05 | URS-RES-05 | OOS at S3 triggers LIMS workflow `LIMS-WF-211192`; sample-state transitions to HOLD. |
| FS-AUD-01 | URS-AUD-01 | Audit-trail event coverage: methods, sequences, results, configuration, MQ events, CPT events, media register, sign-on/off. |
| FS-AUD-02 | URS-AUD-02 | Audit-trail DB constraint = append-only. |
| FS-AUD-03 | URS-AUD-03 | Per-batch review by Senior Analyst; monthly by QC Manager. |
| FS-AUD-04 | URS-AUD-04 | Retention 25 y product-release-linked; 7 y default; archival job `SOL-JOB-ARCH-DISSO`. |
| FS-PART11-01 | URS-PART11-01 | § 11.10(a) procedural controls: SOPs referenced from CS. |
| FS-PART11-02 | URS-PART11-02 | § 11.10(d) access: AD-mapped roles; quarterly access review. |
| FS-PART11-03 | URS-PART11-03 | § 11.50 e-sign manifestation: username, datetime, meaning. |
| FS-PART11-04 | URS-PART11-04 | § 11.70 signature/record linking: cryptographic hash binding. |
| FS-PART11-05 | URS-PART11-05 | § 11.100 uniqueness: AD UPN. |
| FS-PART11-06 | URS-PART11-06 | § 11.200 re-auth: re-entry of password at every Approve. |
| FS-PART11-07 | URS-PART11-07 | § 11.300 password policy: AD GPO (12-char, complexity, 90 d, 5-attempt lockout). |
| FS-DI-01 | URS-DI-01 | Attributable: op_id captured per event. |
| FS-DI-02 | URS-DI-02 | Legible: PDF/A export. |
| FS-DI-03 | URS-DI-03 | Contemporaneous: NTP timestamps. |
| FS-DI-04 | URS-DI-04 | Original: raw `.dtr` files preserved. |
| FS-DI-05 | URS-DI-05 | Accurate: SST + CPT + MQ gates verified per OQ. |
| FS-DI-06 | URS-DI-06 | Complete: archival manifest verifies presence of raw + audit + signature + method-version per result. |
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | LIMS Connector polls worklist endpoint every 5 min; read-only. |
| FS-INT-LIMS-02 | URS-INT-LIMS-02 | Result push triggered only on `result_state=APPROVED`. |
| FS-INT-LIMS-03 | URS-INT-LIMS-03 | Pre-push checker evaluates CPT_state + MQ_state; block on FAIL / EXPIRED / OVERDUE. |
| FS-INT-UV-01 | URS-INT-UV-01 | UV-Vis ingest preserves source-file pointer + SHA-256 hash; no manipulation of UV-Vis raw. |
| FS-BAK-01 | URS-BAK-01 | Daily Veeam backup with SHA-256 manifest. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore drill `SOL-SOP-RESTORE-TEST`; QC-witnessed. |
| FS-BAK-03 | URS-BAK-03 | RTO ≤ 8 h; RPO ≤ 24 h; verified at restore drill. |
| FS-PERF-01 | URS-PERF-01 | PQ scenario: 6-vessel multi-timepoint run completes without crash or data loss. |
| FS-SEC-01 | URS-SEC-01 | AD bind via LDAPS; break-glass `SOL-BG-DISSO` vaulted in CyberArk. |
| FS-SEC-02 | URS-SEC-02 | Removable-media GPO `SOL-LAB-USB-BLOCK`; engineering override via change-control. |
| FS-TRN-01 | URS-TRN-01 | LMS courses: `SOL-DISSO-101` (analyst), `SOL-DISSO-201` (MQ + CPT execution); annual re-completion. |
| FS-PR-01 | URS-PR-01 | Periodic review template `SOL-PR-DISSO`: configuration, audit-trail evidence, MQ + CPT trends, deviations, backup-restore, training; QC Manager + Head of QA sign-off. |


### 4.1 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem. Conditional-access binding to policy `Lab-Workstation Conditional Access (MFA on interactive logon)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the dissolution result DB; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Configuration Items

| CI ID | Item | Value |
|---|---|---|
| CI-01 | DissoTrack Part 11 module | Enabled; project policy SOL_DISSO_PART11 |
| CI-02 | Apparatus suitability | USP <711> centering ≤ 2 mm, wobble ≤ 1 mm, vert dist 25 ± 2 mm |
| CI-03 | RPM tolerance | ± 4% of set |
| CI-04 | Temperature tolerance | 37 °C ± 0.5 °C |
| CI-05 | CPT acceptance | Per current USP Prednisone Tablets RS guidance range |
| CI-06 | USP <711> stage logic | S1 (n=6); S2 (n=12 cumulative); S3 (n=24 cumulative) |
| CI-07 | LIMS push gate | QC Manager approval + CPT_state OK + MQ_state OK |
| CI-08 | Backup retention | 25 y product-release-linked; 7 y default |
| CI-09 | Re-qualification trigger matrix | Paddle / basket / vessel maintenance → full MQ + CPT; routine PM → partial CPT |

## 6. Risks (FS-level)

| ID | Risk | Mitigation |
|---|---|---|
| FR-01 | Paddle / basket misalignment | FS-MQ-01..03 |
| FR-02 | Bath temp excursion mid-run | FS-CMP-02 + FS-RUN-03 |
| FR-03 | Rotation drift outside ± 4% | FS-CMP-03 + FS-AIQ-03 |
| FR-04 | CPT failure unrecognised | FS-CPT-03 (block product runs) |
| FR-05 | Media expired / wrong-lot | FS-MED-02 pre-flight block |
| FR-06 | LIMS push of unapproved / SST-failed | FS-INT-LIMS-02 + FS-INT-LIMS-03 |
| FR-07 | UV-Vis result tampering | FS-INT-UV-01 hash preserve |
| FR-08 | Vibration drift (motor / mount aging) | FS-MQ-05 + FS-CPT-04 trend |

## 7. References

SOL-URS-DISSO-001 v1.2; 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .192, .194; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <711>; USP <724>; USP <1058>; USP <1092>; Ph. Eur. 2.9.3; Ph. Eur. 2.9.4; ICH Q4B Annex 7; PIC/S PI 041; ISPE GAMP 5 (2nd ed., 2022); Distek — *Evolution 6300 + ezfill 5300 + DissoTrack 5 Reference*.

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-HW-01 | FS-HW-01 |
| URS-HW-02 | FS-HW-02 |
| URS-HW-03 | FS-HW-03 |
| URS-HW-04 | FS-HW-04 |
| URS-HW-05 | FS-HW-05 |
| URS-HW-06 | FS-HW-06 |
| URS-HW-07 | FS-HW-07 |
| URS-SW-01 | FS-SW-01 |
| URS-SW-02 | FS-SW-02 |
| URS-SW-03 | FS-SW-03 |
| URS-SW-04 | FS-SW-04 |
| URS-SW-05 | FS-SW-05 |
| URS-SW-06 | FS-SW-06 |
| URS-SW-07 | FS-SW-07 |
| URS-CMP-01 | FS-CMP-01 |
| URS-CMP-02 | FS-CMP-02 |
| URS-CMP-03 | FS-CMP-03 |
| URS-CMP-04 | FS-CMP-04 |
| URS-CMP-05 | FS-CMP-05 |
| URS-CMP-06 | FS-CMP-06 |
| URS-CMP-07 | FS-CMP-07 |
| URS-AIQ-01 | FS-AIQ-01 |
| URS-AIQ-02 | FS-AIQ-02 |
| URS-AIQ-03 | FS-AIQ-03 |
| URS-AIQ-04 | FS-AIQ-04 |
| URS-AIQ-05 | FS-AIQ-05 |
| URS-AIQ-06 | FS-AIQ-06 |
| URS-MQ-01 | FS-MQ-01 |
| URS-MQ-02 | FS-MQ-02 |
| URS-MQ-03 | FS-MQ-03 |
| URS-MQ-04 | FS-MQ-04 |
| URS-MQ-05 | FS-MQ-05 |
| URS-MQ-06 | FS-MQ-06 |
| URS-MQ-07 | FS-MQ-07 |
| URS-CPT-01 | FS-CPT-01 |
| URS-CPT-02 | FS-CPT-02 |
| URS-CPT-03 | FS-CPT-03 |
| URS-CPT-04 | FS-CPT-04 |
| URS-MED-01 | FS-MED-01 |
| URS-MED-02 | FS-MED-02 |
| URS-MED-03 | FS-MED-03 |
| URS-MED-04 | FS-MED-04 |
| URS-MED-05 | FS-MED-05 |
| URS-METH-01 | FS-METH-01 |
| URS-METH-02 | FS-METH-02 |
| URS-METH-03 | FS-METH-03 |
| URS-RUN-01 | FS-RUN-01 |
| URS-RUN-02 | FS-RUN-02 |
| URS-RUN-03 | FS-RUN-03 |
| URS-RUN-04 | FS-RUN-04 |
| URS-RUN-05 | FS-RUN-05 |
| URS-RES-01 | FS-RES-01 |
| URS-RES-02 | FS-RES-02 |
| URS-RES-03 | FS-RES-03 |
| URS-RES-04 | FS-RES-04 |
| URS-RES-05 | FS-RES-05 |
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
| URS-INT-UV-01 | FS-INT-UV-01 |
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
| R-01 | Paddle / basket misalignment causing biased % dissolved | Medium | High | URS-HW-04 + URS-MQ-01..07 |
| R-02 | UV-Vis source-data tampering | Low | High | URS-INT-UV-01 |
| R-03 | LIMS push of unapproved result | Medium | High | URS-INT-LIMS-02 + URS-INT-LIMS-03 |
| R-04 | Audit-trail tampering | Low | High | URS-AUD-02 + URS-DI-06 |
| R-05 | Bath temperature excursion mid-run unnoticed | Medium | High | URS-RUN-03 + URS-CMP-02 |
| R-06 | Apparatus mechanical-qualification drift (vibration aging) | Medium | High | URS-MQ-05 + URS-CPT-04 trend |
| R-07 | Media expired / wrong-lot bound to method | Medium | High | URS-MED-01 + URS-MED-02 |
| R-08 | CPT (Prednisone Tablets RS) failure unrecognised | Low | High | URS-CPT-03 (block product runs) |
| R-09 | Rotation-rate drift (motor wear) outside ± 4% | Low | High | URS-CMP-03 + URS-AIQ-03 |
| R-10 | Vessel verticality drift (uneven plate or bent vessel) | Low | Medium | URS-MQ-06 + URS-HW-06 |
| R-11 | Dissolved-oxygen contamination skewing release rate of poorly soluble compound | Low | Medium | URS-AIQ-03 + URS-MED-04 |

Full evaluation in `SOL-RA-DISSO-001` *(synthetic)*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
