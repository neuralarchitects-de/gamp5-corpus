---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "KSP-URS-NIR-001 (parent URS) v1.2"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11; EU GMP Annex 11"
  - "USP <1119>; USP <856>; USP <1058>; Ph. Eur. 2.2.40"
  - "EMA NIR Guideline 2014; ICH Q2(R2); ICH Q14"
parent_urs:
  document_number: KSP-URS-NIR-001
  version: 1.2
  file: ../../URS/_generated/NIR_Spectrometer_Computer_System__Kestrel_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## NIR Spectrometer Computer System — Bruker MPA II + OPUS 8.7

**Document Number:** KSP-FS-NIR-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** KSP-URS-NIR-001 v1.2 | **Site:** Kestrel Pharma (fictional)
**System Class:** GAMP Cat 4 — Configured Product (chemometric models are Cat 5 sub-components)
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; USP <1119>; USP <856>; USP <1058>; Ph. Eur. 2.2.40; EMA NIR Guideline (2014); ICH Q2(R2); ICH Q14; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Goods Receipt) | _____________ | _____________ | _____ |
| Reviewer (Chemometrics Lead) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Approver (Head of Supply Quality) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | Expanded to match KSP-URS-NIR-001 v1.2 (T2 — 65-req). Per-URS-ID rows for compendial (USP <1119> / Ph. Eur. 2.2.40 / EMA NIR Guideline), AIQ per USP <1058>, SST battery, chemometric model lifecycle (PCA/PLS/SIMCA with T²/Q thresholds), reference-standard register, sample-presentation controls, per-clause Part 11 + DI. Doc-number prefix aligned with URS (KSP-). |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies the deployment, configuration, and integration of Bruker MPA II + OPUS 8.7 to satisfy `KSP-URS-NIR-001` v1.2. Controlling input to `KSP-CS-NIR-001`, `KSP-RA-NIR-001`, IQ/OQ/PQ protocols, and `KSP-RTM-NIR-001`.

## 2. Scope

Mirrors the URS: Bruker MPA II spectrometer + OPUS 8.7 + IDENT + QUANT + Validation modules on a dedicated workstation (Win 11 Pro 23H2); chemometric library / model registry; barcode reader; AD authentication; LIMS connector; daily backup; NTP sync; USP <1119> SST battery; AIQ per USP <1058>. Out: sample preparation; model-development environment; LIMS sample-lifecycle.

## 3. System Architecture

```
   AD/NTP ──► OPUS 8.7 Workstation ──► Bruker MPA II
                  │                          │
                  ├─► Chemometric Model Registry (signed/hashed)
                  ├─► Reference Standard Register (NIST SRMs)
                  └─► LabWare LIMS 8 (worklist + result push, SST/model-gated)
```

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source / Vendor | Notes |
|---|---|---|---|---|---|
| C-01 | OPUS 8.7 (IDENT + QUANT + Validation) | Application SW | 4 | Bruker | 21 CFR Part 11 module enabled |
| C-02 | Bruker MPA II | Instrument FW | 4 | Bruker | FT-NIR, polarization-interferometer |
| C-03 | Windows 11 Pro 23H2 | OS | 1 | Microsoft | Domain-joined |
| C-04 | Chemometric models | Site-developed | **5** | Site Chemometrics | Per-product / per-grade Cat 5 sub-component |
| C-05 | LabWare LIMS 8 connector | Interface | 4 | Bruker + LabWare | Worklist + result push |
| C-06 | Reference Standard Register | Config | 4 | Site | NIST SRM 1920a + USP/Ph.Eur. CRS |
| C-07 | Honeywell Voyager 1452g | Peripheral | 1 | Honeywell | Barcode reader |

## 4. Functional Specifications

| FS ID | URS ID | Specification |
|---|---|---|
| FS-HW-01 | URS-HW-01 | OPUS workstation `kst-nir-ws-01` reserved exclusively for NIR; no other Bruker / vendor app installed. |
| FS-HW-02 | URS-HW-02 | HP Z2 Mini G9, 32 GB RAM, 1 TB NVMe; meets / exceeds Bruker OPUS 8.7 minimum spec. |
| FS-HW-03 | URS-HW-03 | APC SMT1500 UPS sized for ≥ 30 min at observed load; PowerChute graceful-shutdown at 20%. |
| FS-HW-04 | URS-HW-04 | USP <1119> PQ executed at scheduled cadence in OPUS Validation module; results archived. |
| FS-HW-05 | URS-HW-05 | Bench equipped with site EMS sensor; alarm thresholds 14 / 31 °C, 18 / 82% RH. |
| FS-HW-06 | URS-HW-06 | Each sampling accessory (vial holder, fibre-optic probe, integrating sphere) qualified per Bruker SOP at install + post-service. |
| FS-SW-01 | URS-SW-01 | Windows 11 Pro 23H2, joined to `kestrel.local`; GPO baseline `KSP-LAB-USERS-WS-23H2` applied. |
| FS-SW-02 | URS-SW-02 | OPUS 8.7 + IDENT + QUANT + Validation installed by Bruker engineer; install record retained. |
| FS-SW-03 | URS-SW-03 | Project storage on `\\kst-gmp-fs01\nir-projects` with NTFS ACL bound to AD groups; local C: blocked for GxP writes. |
| FS-SW-04 | URS-SW-04 | Windows Time Service pointing to `ntp.kestrel.local`; w32time skew alert at > 1000 ms. |
| FS-SW-05 | URS-SW-05 | OPUS project policy `KSP_NIR_PART11` applied: audit trail required, eSign required, raw data lock; CS-NIR-001 documents the values. |
| FS-SW-06 | URS-SW-06 | Bruker OPUS revisions applied under change-control `CCR-NIR-*`; installed build hash verified at partial-OQ re-test. |
| FS-CMP-01 | URS-CMP-01 | OQ wavelength-accuracy test against NIST SRM 1920a polystyrene; pass = peak positions within ± 1 nm across 780–2500 nm. |
| FS-CMP-02 | URS-CMP-02 | OQ photometric-noise test: RMS noise on 99% reflectance ceramic ≤ 30 µAU @ 1.0 A across working range; per USP <1119>. |
| FS-CMP-03 | URS-CMP-03 | OQ photometric-linearity test using NIST-traceable transmittance standards across working range. |
| FS-CMP-04 | URS-CMP-04 | EP-monograph methods carry `Compendium=EP`; on those methods, additional Ph. Eur. 2.2.40 control tests are mandatory at SST. |
| FS-CMP-05 | URS-CMP-05 | Method authoring template enforces EMA NIR Guideline (2014) sections: variable selection, pre-processing, threshold rule, reference-method correlation; mandatory fields. |
| FS-CMP-06 | URS-CMP-06 | Quantitative methods carry ATP definition per ICH Q14 + Q2(R2) validation evidence; binding enforced at deployment. |
| FS-CMP-07 | URS-CMP-07 | Method header `compendium` enum (USP / EP / JP / NON-COMP). |
| FS-AIQ-01 | URS-AIQ-01 | DQ `KSP-DQ-NIR-001` captures intended-use, wavelength range, accessories, model classes, Part 11 binding. |
| FS-AIQ-02 | URS-AIQ-02 | IQ `KSP-IQ-NIR-001` verifies install, AD bind, OPUS build hash, optical alignment, source replacement record. |
| FS-AIQ-03 | URS-AIQ-03 | OQ `KSP-OQ-NIR-001` battery: wavelength acc + repeatability (5 reps), photometric noise, photometric linearity, SNR, scan reproducibility, resolution. |
| FS-AIQ-04 | URS-AIQ-04 | PQ `KSP-PQ-NIR-001` scheduled at go-live, on major change, annually; PQ delegate notifies QC Manager 30 d before due. |
| FS-AIQ-05 | URS-AIQ-05 | Re-qual matrix: source replacement → full PQ; detector service → full PQ; sampling-accessory change → full PQ; routine PM not affecting optical bench → SST partial only. |
| FS-AIQ-06 | URS-AIQ-06 | Qualification evidence stored on `\\kst-gmp-fs01\nir-qual` with WORM bit; retention 25 y. |
| FS-SST-01 | URS-SST-01 | SST battery scheduled: wavelength acc + photometric noise + SNR + warm-up daily; full battery (incl. linearity) weekly. |
| FS-SST-02 | URS-SST-02 | SST record schema: op_id, ts, ref_std_id, certificate_expiry, computed_value, acceptance_limit, verdict; record immutable post-write. |
| FS-SST-03 | URS-SST-03 | On SST fail, FSM → NOT_READY; sequence runner blocks; override requires `KSP-NIR-QA-APPROVER` co-sign + RFC. |
| FS-SST-04 | URS-SST-04 | Rolling 12-month SST trend; early-warning band at ½ USP <1119> limit; alert via Site EMS dashboard at first band breach. |
| FS-SST-05 | URS-SST-05 | Monthly audit-trail review template includes "SST trend review" step with sign-off. |
| FS-MODEL-01 | URS-MODEL-01 | Model Card schema in OPUS Validation module: training_set, calibration_stats, validation_stats, threshold, pre-processing, variables, factors, limitations. |
| FS-MODEL-02 | URS-MODEL-02 | Model deployment workflow `KSP-WF-MODEL-DEPLOY` requires Chemometrics Approver + QC Manager e-signatures with role-bound AD groups. |
| FS-MODEL-03 | URS-MODEL-03 | Each deployed model file (`.q2` / `.simca`) carries SHA-256 hash stored in registry; OPUS verifies before use; mismatch blocks run. |
| FS-MODEL-04 | URS-MODEL-04 | Retraining triggers configured: drift detected by Hotelling T² / Q residual; new supplier qualified; OOS rate > 1% rolling-monthly; documented audit entry. |
| FS-MODEL-05 | URS-MODEL-05 | Model-performance dashboard: false-pass rate, false-fail rate, distance-to-model statistics, residual variance; quarterly review by Chemometrics Lead. |
| FS-MODEL-06 | URS-MODEL-06 | Reference-method correlation (NIR vs HPLC / KF) recorded at deployment + at periodic review per EMA NIR Guideline § 2.4. |
| FS-MODEL-07 | URS-MODEL-07 | Retired models flagged READ-ONLY in registry; cannot be selected at acquisition; retained for traceability of legacy records. |
| FS-MODEL-08 | URS-MODEL-08 | SIMCA distance and PLS Hotelling T² + Q residual thresholds configured per model; out-of-bounds spectra flagged INCONCLUSIVE. |
| FS-MODEL-09 | URS-MODEL-09 | Promotion pipeline `dev → val → prod` enforced by environment binding; production OPUS rejects models without `val_approved=true`. |
| FS-REF-01 | URS-REF-01 | Reference Standard Register schema: ref_std_id, type, source, lot, COA_id, NIST_traceability_flag, receipt_date, opening_date, expiry, custodian. |
| FS-REF-02 | URS-REF-02 | Pre-flight checker rejects SST start when ref_std_id is expired; rejection logged. |
| FS-REF-03 | URS-REF-03 | SST execution captures bound ref_std_id; mandatory field. |
| FS-REF-04 | URS-REF-04 | Re-qualification workflow `KSP-WF-REFREQ-NIR`; QA approval required before bind. |
| FS-SAMP-01 | URS-SAMP-01 | Method `sampling_accessory` field bound to method version; accessory-mismatch detection at run start (probe ID query) blocks run. |
| FS-SAMP-02 | URS-SAMP-02 | Acquisition record fields: sampling_mode, vial_or_probe_id, accessory_serial. |
| FS-SAMP-03 | URS-SAMP-03 | SST cadence includes probe-condition check: reference-spectrum overlay against probe-baseline-spectrum; deviation > limit blocks. |
| FS-ACQ-01 | URS-ACQ-01 | Barcode scan binds material_code + lot to spectrum record; scan failure prompts manual entry under audit. |
| FS-ACQ-02 | URS-ACQ-02 | Pre-flight checker evaluates SST_overdue, PQ_overdue, model_state ≠ EFFECTIVE, project_locked; any TRUE blocks. |
| FS-ACQ-03 | URS-ACQ-03 | Acquisition metadata schema: material_code, lot, model_id, model_version, instrument_id, analyst_id, sampling_mode, accessory_id, ts. |
| FS-ID-01 | URS-ID-01 | Identification result calculated per model threshold; verdict in {PASS, FAIL, BORDERLINE, INCONCLUSIVE}; BORDERLINE / FAIL routes to Senior Analyst queue. |
| FS-ID-02 | URS-ID-02 | LIMS interface posts result with FAIL flag → LIMS sample-state transitions to HOLD; material lot blocked from release. |
| FS-ID-03 | URS-ID-03 | INCONCLUSIVE verdict (out-of-model-space per T² / Q) cannot be reported as PASS; routes to Chemometrics Engineer + Senior Analyst for disposition. |
| FS-AUD-01 | URS-AUD-01 | Audit-trail event coverage: spectra, methods, models, deployments, configuration, sign-on/off, ref-std register, SST events. |
| FS-AUD-02 | URS-AUD-02 | Audit-trail table append-only (DB constraint); delete grant revoked at vendor + DBA level. |
| FS-AUD-03 | URS-AUD-03 | Per-session review by Senior Analyst (`KSP-AUD-REVIEW-NIR-SESSION`); monthly review by QC Manager (`KSP-AUD-REVIEW-NIR-MONTH`). |
| FS-AUD-04 | URS-AUD-04 | Retention 25 y on product-release-linked; 7 y default; archival job `KSP-JOB-ARCH-NIR`. |
| FS-PART11-01 | URS-PART11-01 | § 11.10(a) procedural-controls: change-control SOP `KSP-SOP-CC-NIR` + incident-response SOP `KSP-SOP-IR-NIR` referenced from CS. |
| FS-PART11-02 | URS-PART11-02 | § 11.10(d) access: AD-mapped roles per § 4 of URS; quarterly access review. |
| FS-PART11-03 | URS-PART11-03 | § 11.50 e-sign manifestation: username, datetime (NTP), meaning (Author / Reviewer / Approver). |
| FS-PART11-04 | URS-PART11-04 | § 11.70 signature/record linking: cryptographic binding signature_record_id ↔ record_id; verifiable on export. |
| FS-PART11-05 | URS-PART11-05 | § 11.100 uniqueness: AD UPN as unique identifier; reuse / reassignment governed by AD lifecycle. |
| FS-PART11-06 | URS-PART11-06 | § 11.200 re-auth: re-entry of password required at every Approve action. |
| FS-PART11-07 | URS-PART11-07 | § 11.300 password policy: AD GPO `KSP-LAB-USERS-PWD` enforces min 12 chars, complexity 3-of-4, max age 90 d, lockout at 5. |
| FS-DI-01 | URS-DI-01 | Attributable: op_id captured on every event. |
| FS-DI-02 | URS-DI-02 | Legible: report renderer enforces font/min-size; export to PDF/A. |
| FS-DI-03 | URS-DI-03 | Contemporaneous: NTP-derived ts per FS-SW-04; manual ts entry prohibited. |
| FS-DI-04 | URS-DI-04 | Original: raw `.0` file is source-of-truth; processing emits derived `.proc` referencing parent raw_id. |
| FS-DI-05 | URS-DI-05 | Accurate: SST pre-flight + model-hash check (FS-MODEL-03) gate every run. |
| FS-DI-06 | URS-DI-06 | Complete: archival manifest verifies presence of raw + audit + signature + model-version for every result. |
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | OPUS LIMS Connector 3 polls LIMS worklist endpoint every 5 min; read-only. |
| FS-INT-LIMS-02 | URS-INT-LIMS-02 | Result push triggered only on `result_state=APPROVED`; rejected pushes emit LIMS error code `KSP-NIR-NOT-APPROVED`. |
| FS-INT-LIMS-03 | URS-INT-LIMS-03 | LIMS payload includes spectrum_hash, model_id, model_version, instrument_id, reviewer_id, approver_id. |
| FS-INT-LIMS-04 | URS-INT-LIMS-04 | Pre-push checker evaluates SST_status; block on SST_FAIL / SST_EXPIRED. |
| FS-BAK-01 | URS-BAK-01 | Daily backup job `KSP-JOB-BAK-NIR` to Site backup target; backed-up: spectra, methods, model registry, audit DB, ref-std register. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore drill `KSP-SOP-RESTORE-TEST`; QA-witnessed. |
| FS-PERF-01 | URS-PERF-01 | Identification time tested at PQ ≤ 60 s p95. |
| FS-SEC-01 | URS-SEC-01 | AD bind via LDAPS; break-glass local account `KSP-BG-NIR` vaulted in CyberArk. |
| FS-SEC-02 | URS-SEC-02 | Removable-media GPO `KSP-LAB-USB-BLOCK`; engineering override via change-control. |
| FS-TRN-01 | URS-TRN-01 | LMS courses: `KSP-NIR-101` (analyst), `KSP-NIR-201` (chemometric execution); annual re-completion required. |
| FS-PR-01 | URS-PR-01 | Periodic review template `KSP-PR-NIR`: model registry, drift trends, false-pass/-fail rate, deviations, SST trend, training currency; sign-off QC Manager + Head of QA. |


### 4.1 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem. Conditional-access binding to policy `Lab-Workstation Conditional Access (MFA on interactive logon)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the NIR result DB plus file-level capture of model files and chemometric calibrations; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Configuration Items (CI)

| CI ID | Item | Value |
|---|---|---|
| CI-01 | OPUS Part 11 module | Enabled; project policy KSP_NIR_PART11 |
| CI-02 | USP <1119> PQ cadence | Annual + on major change |
| CI-03 | SST cadence | Daily (wavelength + noise + SNR + warm-up); weekly (full battery + linearity) |
| CI-04 | Wavelength ref standard | NIST SRM 1920a polystyrene |
| CI-05 | Model match threshold | Per recipe (configurable per Model Card) |
| CI-06 | Hotelling T² / Q-residual threshold | Per model; bound at deployment |
| CI-07 | Drift monitoring cadence | Continuous (per-acquisition T²/Q); quarterly review |
| CI-08 | Backup retention | 25 y product-release-linked; 7 y default |
| CI-09 | Model-hash verification | SHA-256, pre-acquisition |
| CI-10 | Reference-method re-correlation | At deployment + annual periodic review |

## 6. Risks (FS-level)

| ID | Risk | Mitigation |
|---|---|---|
| FR-01 | False-pass identification | FS-MODEL-02 validation + FS-MODEL-08 T²/Q thresholds + FS-ID-01 senior-analyst escalation |
| FR-02 | Model drift undetected | FS-MODEL-04 retraining triggers + FS-MODEL-05 quarterly review |
| FR-03 | LIMS push of unapproved / SST-failed | FS-INT-LIMS-02 + FS-INT-LIMS-04 |
| FR-04 | Audit-trail tampering | FS-AUD-02 append-only + FS-DI-06 |
| FR-05 | Wavelength accuracy drift | FS-SST-04 trend + FS-AIQ-05 source-change full PQ |
| FR-06 | Out-of-model-space prediction reported as PASS | FS-MODEL-08 + FS-ID-03 INCONCLUSIVE routing |
| FR-07 | Wrong sampling accessory bound to method | FS-SAMP-01 accessory-mismatch check |
| FR-08 | Expired NIST SRM in SST | FS-REF-02 expiry block |

## 7. References

KSP-URS-NIR-001 v1.2; 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .84, .194; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <1119>; USP <856>; USP <1058>; USP <1225>; Ph. Eur. 2.2.40; EMA NIR Guideline (2014); ICH Q2(R2); ICH Q14; ICH Q8(R2); PIC/S PI 041; ISPE GAMP 5 (2nd ed., 2022); Bruker — *MPA II + OPUS 8.7 Reference*.

## 8. Appendix A — URS → FS Traceability Matrix

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
| URS-SST-01 | FS-SST-01 |
| URS-SST-02 | FS-SST-02 |
| URS-SST-03 | FS-SST-03 |
| URS-SST-04 | FS-SST-04 |
| URS-SST-05 | FS-SST-05 |
| URS-MODEL-01 | FS-MODEL-01 |
| URS-MODEL-02 | FS-MODEL-02 |
| URS-MODEL-03 | FS-MODEL-03 |
| URS-MODEL-04 | FS-MODEL-04 |
| URS-MODEL-05 | FS-MODEL-05 |
| URS-MODEL-06 | FS-MODEL-06 |
| URS-MODEL-07 | FS-MODEL-07 |
| URS-MODEL-08 | FS-MODEL-08 |
| URS-MODEL-09 | FS-MODEL-09 |
| URS-REF-01 | FS-REF-01 |
| URS-REF-02 | FS-REF-02 |
| URS-REF-03 | FS-REF-03 |
| URS-REF-04 | FS-REF-04 |
| URS-SAMP-01 | FS-SAMP-01 |
| URS-SAMP-02 | FS-SAMP-02 |
| URS-SAMP-03 | FS-SAMP-03 |
| URS-ACQ-01 | FS-ACQ-01 |
| URS-ACQ-02 | FS-ACQ-02 |
| URS-ACQ-03 | FS-ACQ-03 |
| URS-ID-01 | FS-ID-01 |
| URS-ID-02 | FS-ID-02 |
| URS-ID-03 | FS-ID-03 |
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
| R-01 | False-pass identification (wrong material accepted) | Medium | High | URS-MODEL-02 + URS-ID-01 + URS-MODEL-08 (Hotelling T²/Q) |
| R-02 | Model drift on new supplier or grade not in training set | Medium | High | URS-MODEL-04 + URS-MODEL-05 + URS-MODEL-08 |
| R-03 | LIMS push of unapproved result | Medium | High | URS-INT-LIMS-02 |
| R-04 | Audit-trail tampering | Low | High | URS-AUD-02 + URS-DI-06 |
| R-05 | Wavelength accuracy drift between scheduled SSTs (source aging) | Medium | High | URS-SST-04 trend + URS-AIQ-04 PQ cadence |
| R-06 | Photometric noise degradation (detector or InGaAs aging) | Low | High | URS-CMP-02 + URS-SST-01 |
| R-07 | Chemometric model used outside its model space (extrapolation) | Medium | High | URS-MODEL-08 (T²/Q thresholds) + URS-ID-03 |
| R-08 | Wrong sample-presentation accessory (vial vs probe vs sphere) | Low | High | URS-SAMP-01 (method-bound accessory check) |
| R-09 | Expired NIST SRM in use | Medium | Medium | URS-REF-01 + URS-REF-02 |
| R-10 | Reference-method correlation (NIR vs HPLC) breaks at validity boundary | Low | High | URS-MODEL-06 + EMA NIR Guideline § 2.4 |

Full evaluation in `KSP-RA-NIR-001` *(synthetic)*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
