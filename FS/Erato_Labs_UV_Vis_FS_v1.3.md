---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "ERA-URS-UVVIS-001 (parent URS) v1.2"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11; EU GMP Annex 11"
  - "USP <857>; USP <1058>; USP <1225>; Ph. Eur. 2.2.25"
parent_urs:
  document_number: ERA-URS-UVVIS-001
  version: 1.2
  file: ../../URS/_generated/UV-Vis_Spectrophotometer_Computer_System__Erato_Labs_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## UV-Vis Spectrophotometer Computer System — Agilent Cary 3500 + UV WorkStation v3

**Document Number:** ERA-FS-UVVIS-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** ERA-URS-UVVIS-001 v1.2 | **Site:** Erato Labs (fictional)
**System Class:** GAMP Cat 4 — Configured Product
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; USP <857>; USP <1058>; USP <1225>; Ph. Eur. 2.2.25; ICH Q2(R2); PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Spectroscopy Lead) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Approver (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue, derived from ERA-URS-UVVIS-001 v1.0. |
| 1.2 | 2026-05-12 | (synthetic) | Expanded to match ERA-URS-UVVIS-001 v1.2 (T2 — 60-req). Per-URS-ID rows for compendial compliance (USP <857> / Ph. Eur. 2.2.25), AIQ DQ/IQ/OQ/PQ per USP <1058>, SST battery, reference-standard register, cuvette controls, calculation + OOS, and per-clause Part 11 + DI. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies the deployment, configuration, and integration of Agilent Cary 3500 + UV WorkStation v3 to satisfy `ERA-URS-UVVIS-001` v1.2. Controlling input to `ERA-CS-UVVIS-001`, `ERA-RA-UVVIS-001`, IQ/OQ/PQ protocols, and `ERA-RTM-UVVIS-001`.

## 2. Scope

Mirrors the URS: Cary 3500 instrument + UV WorkStation v3 on a dedicated PC (Win 11 LTSC); AD authentication; integration with LIMS; daily backup; NTP sync; USP <857> SST battery; AIQ DQ/IQ/OQ/PQ per USP <1058>; reference-standard lifecycle. Out: Cary 3500 instrument-level equipment qualification (separate); LIMS sample-lifecycle.

## 3. System Architecture

```
   AD/NTP ──► UV WorkStation v3 PC ──► Cary 3500 (Compact/Multicell)
                  │                          │
                  ├─► Reference Standard Register (integrated)
                  └─► LabWare LIMS 8 (worklist + result push, SST-gated)
```

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source / Vendor | Notes |
|---|---|---|---|---|---|
| C-01 | UV WorkStation v3 | Application SW | Cat 4 | Agilent | 21 CFR Part 11 module enabled |
| C-02 | Cary 3500 | Instrument FW | Cat 4 | Agilent | Double-beam, dual-monochromator |
| C-03 | Windows 11 Enterprise LTSC | OS | Cat 1 | Microsoft | Hardened per site baseline |
| C-04 | AD bind | Auth | Cat 1 | Site IT | erato.local |
| C-05 | LabWare LIMS 8 connector | Interface | Cat 4 | Agilent + LabWare | Worklist + result push |
| C-06 | Reference-standard register | Config | Cat 4 | Site | NIST-traceable certificates |

## 4. Functional Specifications

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | Standalone PC connected to lab-IT VLAN (vlan-lab-spec); no corporate-network bind; firewall rules restrict egress to AD / NTP / LIMS endpoints only. |
| FS-PLAT-02 | URS-PLAT-02 | Windows Time Service points to validated NTP pool (`ntp1.erato.local`, `ntp2.erato.local`); w32time skew alert configured at > 1000 ms via Site monitoring. |
| FS-PLAT-03 | URS-PLAT-03 | APC SMT1500 UPS sized at 1500 VA / 1000 W; runtime ≥ 30 min at observed load; PowerChute graceful-shutdown configured at 20% remaining. |
| FS-PLAT-04 | URS-PLAT-04 | Instrument bench equipped with site EMS sensor reporting to facility historian; alarm at 14 / 31 °C, 18 / 82% RH. |
| FS-PLAT-05 | URS-PLAT-05 | Windows Event Log subscription to Site SIEM for USB / removable-media event IDs 4663 / 6416 / 6420. |
| FS-SW-01 | URS-SW-01 | UV WorkStation v3 installed with Part 11 module flag `Part11Enabled=true`; project policy `ERATO_QC_PART11` applied (audit trail required, eSign required, raw data lock). |
| FS-SW-02 | URS-SW-02 | Methods stored under `\\era-fs01\uvvis\methods` with NTFS ACL bound to AD groups `ERA-UVVIS-METHOD-OWNER`, `ERA-UVVIS-METHOD-APPROVER`; deny inheritance from parent. |
| FS-SW-03 | URS-SW-03 | SST scheduler configured: wavelength accuracy + photometric + stray light daily; full battery (incl. linearity) weekly; per-method override permitted only on EFFECTIVE methods. |
| FS-SW-04 | URS-SW-04 | Password policy: min length 12, complexity 3-of-4, max age 90 d, lockout after 5 failed attempts; enforced via AD GPO `ERA-LAB-USERS-PWD`. |
| FS-SW-05 | URS-SW-05 | CS-EMPOWER-equivalent `ERA-CS-UVVIS-001` documents all Part 11 toggles, project policies, AD bindings; any change opened as RFC in eQMS before application. |
| FS-SW-06 | URS-SW-06 | Vendor SCN applied via change-control workflow `CCR-UVVIS-*`; installed build verified against CS baseline at every OQ partial re-test. |
| FS-MTH-01 | URS-MTH-01 | UV WorkStation method-lifecycle states mapped DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE; only EFFECTIVE methods exposed to the worklist runner. |
| FS-MTH-02 | URS-MTH-02 | Method state-transition e-signature requires AD group `ERA-UVVIS-METHOD-APPROVER`; Author identity captured at DRAFT and excluded from Approver list. |
| FS-MTH-03 | URS-MTH-03 | Trigger fires re-verification protocol when calibration_tie, ref_std_id, slit_width, or lambda_target fields change; protocol = USP <1226> verification or <1225> re-validation per method classification. |
| FS-MTH-04 | URS-MTH-04 | Method version history table retained per method; diff renderer shows redline of YAML method body across versions. |
| FS-ACQ-01 | URS-ACQ-01 | Acquisition header binds sample_id, cuvette_path_length, baseline_scan_id, blank_scan_id, SST_status (with SST-record-id). |
| FS-ACQ-02 | URS-ACQ-02 | Sequence pre-flight checker evaluates: SST_overdue, instrument_state ≠ READY, method_state ≠ EFFECTIVE; any TRUE blocks and emits blocking-reason audit record. |
| FS-ACQ-03 | URS-ACQ-03 | Per-acquisition metadata captured: spectral_bandwidth_nm, scan_rate_nm_per_min, integration_time_s, detector_mode. |
| FS-ACQ-04 | URS-ACQ-04 | Baseline / 100%T correction routines logged to audit trail with op_id + ts; cannot be silently re-applied. |
| FS-ACQ-05 | URS-ACQ-05 | Bracket-reference evaluator computes (observed − nominal) / nominal × 100; reject if |Δ| > 2.0% on assay methods; method-configurable for non-assay. |
| FS-CMP-01 | URS-CMP-01 | OQ wavelength-accuracy test executes against holmium oxide cuvette / filter; pass = all 6 peaks (241.13, 287.15, 361.31, 451.30, 536.64, 640.49 nm) within ± 1 nm (UV) / ± 3 nm (Vis). |
| FS-CMP-02 | URS-CMP-02 | OQ photometric-accuracy test against K₂Cr₂O₇ in 0.005 M H₂SO₄ at 235/257/313/350 nm; pass = ± 1.0% of nominal A. |
| FS-CMP-03 | URS-CMP-03 | OQ stray-light test: KCl 12 g/L @ 200 nm, NaI 10 g/L @ 220 nm, NaNO₂ 50 g/L @ 340 nm; max A reading vs USP <857> specification; failure blocks GxP runs at sequence pre-flight. |
| FS-CMP-04 | URS-CMP-04 | EP-monograph methods carry `Compendium=EP`; on those methods, control-of-absorbance check uses Ph. Eur. 2.2.25 K₂Cr₂O₇ ratio bands; failure blocks runs of EP-monograph methods only. |
| FS-CMP-05 | URS-CMP-05 | Photometric linearity: 5-point K₂Cr₂O₇ standard curve from 0 to 2.0 A (or method working range); r² ≥ 0.999 required; result archived per OQ batch. |
| FS-CMP-06 | URS-CMP-06 | Method header `compendium` enum (USP, EP, JP, NON-COMP); calculation engine applies rounding rule from compendium-rounding lookup table at method approval. |
| FS-AIQ-01 | URS-AIQ-01 | DQ document `ERA-DQ-UVVIS-001` captures intended-use scope, Beer-Lambert range (0.2–2.0 A typical), lambda working range (190–800 nm), SST capability, Part 11 binding. |
| FS-AIQ-02 | URS-AIQ-02 | IQ protocol `ERA-IQ-UVVIS-001` verifies: physical install per Agilent SOP, network / AD bind, software build hash, lamp installation (D2 + tungsten halogen), optical alignment certificate. |
| FS-AIQ-03 | URS-AIQ-03 | OQ protocol `ERA-OQ-UVVIS-001` executes the USP <857> battery: wavelength acc + repeatability (5 reps); photometric acc + linearity; stray light (3 wavelengths); resolution by toluene-in-hexane ratio (1430/1525 cm⁻¹ region, A269/A266); noise (water blank, 200 / 240 / 656 nm); drift (60 min); baseline flatness (200–800 nm). |
| FS-AIQ-04 | URS-AIQ-04 | PQ protocol `ERA-PQ-UVVIS-001` scheduled at go-live, on major change events, and annually; PQ delegate notifies QC Manager 30 d before due date. |
| FS-AIQ-05 | URS-AIQ-05 | Re-qual matrix: D2 lamp replacement → full PQ; tungsten-halogen lamp replacement → full PQ; monochromator service → full PQ; planned PM not affecting optical bench → SST partial only. |
| FS-AIQ-06 | URS-AIQ-06 | Qualification evidence stored in `\\era-fs01\uvvis\qual` with WORM bit set; retention 25 y. |
| FS-SST-01 | URS-SST-01 | SST battery configured in UV WorkStation suite per § 5.6 of URS; reference standards bound by `ref_std_id`. |
| FS-SST-02 | URS-SST-02 | SST record carries op_id, ts, ref_std_id, certificate_expiry, computed_value, acceptance_limits, verdict_pass_fail; record immutable post-write. |
| FS-SST-03 | URS-SST-03 | On SST failure: instrument FSM transitions to NOT_READY; sequence runner rejects launch; engineering override requires `ERA-UVVIS-QA-APPROVER` co-sign and RFC entry. |
| FS-SST-04 | URS-SST-04 | Trend engine computes rolling 12-month SST values; early-warning band = ½ × USP <857> acceptance limit; alert emitted via Site EMS dashboard at first band breach. |
| FS-SST-05 | URS-SST-05 | Monthly audit-trail review template `ERA-AUD-REVIEW-UVVIS` includes "SST trend review" step with sign-off. |
| FS-REF-01 | URS-REF-01 | Reference Standard Register schema: ref_std_id, type, source, lot, COA_id, NIST_traceability_flag, receipt_date, opening_date, expiry, custodian. |
| FS-REF-02 | URS-REF-02 | Pre-flight checker rejects sequence when bound ref_std_id is expired or unidentified; rejection logged with reason `REF_EXPIRED` / `REF_UNKNOWN`. |
| FS-REF-03 | URS-REF-03 | Method header `ref_std_id` required for SST and bracketed assay; method approval blocked when ref_std_id unbound. |
| FS-REF-04 | URS-REF-04 | Disposal log entry mandatory before register entry transitions to `DISPOSED`; record carries operator + disposal_route. |
| FS-REF-05 | URS-REF-05 | Re-qualification workflow `ERA-WF-REFREQ-UVVIS` requires QA approval before in-house re-certified standard is bound to any method. |
| FS-CELL-01 | URS-CELL-01 | Cuvette qualification protocol verifies path-length tolerance ± 0.005 cm for 1 cm cells using interferometric / reference-cuvette comparison; matched-pair check on absorbance differential ≤ 0.005 A at λ_method. |
| FS-CELL-02 | URS-CELL-02 | Acquisition header `cuvette_id` field; UV WorkStation barcode reader / manual entry; cuvette register stored on file server. |
| FS-CELL-03 | URS-CELL-03 | Cuvette-cleaning SOP `ERA-SOP-UVVIS-CLEAN` referenced; carry-over verification step inserted automatically into methods carrying `carryover_relevant=true`. |
| FS-CELL-04 | URS-CELL-04 | Multi-cell holder position bound per acquisition; mismatch prompt fires when scanner-read position ≠ method-assigned position. |
| FS-CALC-01 | URS-CALC-01 | Rounding-rule lookup table loads from compendium reference (USP-NF General Notices 7.20, Ph. Eur. 1. General Notices); rule frozen at method APPROVED state. |
| FS-CALC-02 | URS-CALC-02 | OOS evaluator compares reportable_result vs method-defined spec_low / spec_high; flag = OOS when out-of-bounds; LIMS push carries OOS flag for downstream § 211.192 investigation. |
| FS-CALC-03 | URS-CALC-03 | Significant-figures handling per method category (assay = 4 sig fig typical; identification = qualitative; limit test = 2 sig fig); enforced at report-render time. |
| FS-CALC-04 | URS-CALC-04 | Result-report PDF includes raw absorbances table, baseline / blank chromatograms, SST status, ref_std_ids used, calculation step-by-step audit, intermediate values, final reportable result. |
| FS-CALC-05 | URS-CALC-05 | Replicate-RSD evaluator computes mean + RSD per method-defined replicate count (typical n=3 or n=6); reject result when RSD > method limit. |
| FS-PROC-01 | URS-PROC-01 | RFC dialog mandatory on baseline / peak-pick / integration-boundary edit; minimum 10-character free text + RFC category dropdown. |
| FS-PROC-02 | URS-PROC-02 | Raw data lock implemented at filesystem layer (NTFS read-only + UV WorkStation app-layer lock); deletion requires DB admin + QA co-sign + audit. |
| FS-PROC-03 | URS-PROC-03 | PDF report template `ERA-RPT-UVVIS` includes ALCOA+ block, SHA-256 hash of underlying raw `.uvd` file. |
| FS-AUD-01 | URS-AUD-01 | Audit-trail event coverage: methods, sequences, results, project policy, sign-on / sign-off, ref-std register, SST events. |
| FS-AUD-02 | URS-AUD-02 | Audit-trail table append-only (DB constraint); delete grant revoked at vendor + DBA level. |
| FS-AUD-03 | URS-AUD-03 | Per-batch review by Senior Analyst (sign-off in `ERA-AUD-REVIEW-UVVIS-BATCH`); monthly review by QC Manager (sign-off in `ERA-AUD-REVIEW-UVVIS-MONTH`). |
| FS-AUD-04 | URS-AUD-04 | Retention 25 y on product-release-linked records; 7 y default; enforced by archival job `ERA-JOB-ARCH-UVVIS`. |
| FS-PART11-01 | URS-PART11-01 | § 11.10(a) procedural controls: change-control SOP `ERA-SOP-CC-UVVIS` and incident-response SOP `ERA-SOP-IR-UVVIS` referenced from CS. |
| FS-PART11-02 | URS-PART11-02 | § 11.10(b) export: PDF result reports + CSV raw data export; both reproducible from raw with hash match. |
| FS-PART11-03 | URS-PART11-03 | § 11.10(c) retention protection: archival job `ERA-JOB-ARCH-UVVIS` writes to WORM volume; integrity check via SHA-256 manifest. |
| FS-PART11-04 | URS-PART11-04 | § 11.10(d) access: AD-mapped roles per § 4 of URS; quarterly access review per `ERA-WF-ACC-REVIEW`. |
| FS-PART11-05 | URS-PART11-05 | § 11.50 e-sign manifestation: signature record carries username, datetime (NTP), meaning (Author / Reviewer / Approver). |
| FS-PART11-06 | URS-PART11-06 | § 11.70 signature/record linking: cryptographic hash binding signature record to record_id; verifiable on export. |
| FS-PART11-07 | URS-PART11-07 | § 11.100 uniqueness: AD UPN as unique identifier; reuse / reassignment governed by AD lifecycle `ERA-SOP-ID-LCM`. |
| FS-PART11-08 | URS-PART11-08 | § 11.200 re-auth: re-entry of password required at every Approve action; biometric / smartcard not in scope at v1.2. |
| FS-DI-01 | URS-DI-01 | Attributable: op_id captured on acquire / process / approve / RFC. |
| FS-DI-02 | URS-DI-02 | Legible: report renderer enforces font/min-size; export to PDF/A. |
| FS-DI-03 | URS-DI-03 | Contemporaneous: NTP-derived ts per FS-PLAT-02; manual ts entry prohibited. |
| FS-DI-04 | URS-DI-04 | Original: raw `.uvd` file is source-of-truth; processing emits derived `.proc` files referencing parent raw_id. |
| FS-DI-05 | URS-DI-05 | Accurate: SST pre-flight + bracket-reference (FS-ACQ-05) gate every run. |
| FS-DI-06 | URS-DI-06 | Complete: archival manifest verifies presence of raw + audit + signature + method-version for every result. |
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | Agilent LIMS connector polls LIMS worklist endpoint every 5 min; worklist items appear in UV WorkStation queue with LIMS_id binding. |
| FS-INT-LIMS-02 | URS-INT-LIMS-02 | Result push triggered only on `result_state=APPROVED`; reject conditions emit LIMS-side error code `ERA-UVVIS-NOT-APPROVED`. |
| FS-INT-LIMS-03 | URS-INT-LIMS-03 | Pre-push check evaluates SST_status of session; block + audit-record on SST_FAIL or SST_EXPIRED. |
| FS-INT-AD-01 | URS-INT-AD-01 | AD bind via LDAPS to `erato.local`; break-glass local account `ERA-BG-UVVIS` documented in CS, password vaulted in CyberArk, post-use review mandatory. |
| FS-PERF-01 | URS-PERF-01 | Sequence start latency tested at PQ ≤ 5 s wall-clock; save latency ≤ 2 s per acquisition. |
| FS-BAK-01 | URS-BAK-01 | Daily backup job `ERA-JOB-BAK-UVVIS` to Site backup target; backed-up artefacts: methods, raw files, audit DB, ref-std register, CS files. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore drill per `ERA-SOP-RESTORE-TEST`; witnessed by QA; recorded in eQMS. |
| FS-SEC-01 | URS-SEC-01 | Removable-media policy blocks USB mass-storage class via AD GPO `ERA-LAB-USB-BLOCK`; vendor engineering override requires change-control RFC. |
| FS-TRN-01 | URS-TRN-01 | LMS course IDs: `ERA-UVVIS-101` (analyst), `ERA-UVVIS-201` (SST execution); SST course requires annual re-completion. |
| FS-PR-01 | URS-PR-01 | Periodic review template `ERA-PR-UVVIS` with sections for method inventory, audit-trail review evidence, SST compliance, ref-std register health, deviation summary, training currency; sign-off by QC Manager + Head of QA. |


### 4.1 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem. Conditional-access binding to policy `Lab-Workstation Conditional Access (MFA on interactive logon)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam file-level capture of the UV-Vis software's result database and method library; tier classification = T3; RPO ≤ 72 h; RTO ≤ 72 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; annual QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Configuration Items

| CI | Item | Value |
|---|---|---|
| CI-01 | Part 11 project policy | ERATO_QC_PART11 |
| CI-02 | USP <857> SST cadence | Daily (wavelength + photometric + stray light); weekly (full battery incl. linearity) |
| CI-03 | Photometric linearity working range | 0–2.0 A; r² ≥ 0.999 |
| CI-04 | Wavelength accuracy ref standard | Holmium oxide (NIST-traceable); peaks 241.13 / 287.15 / 361.31 / 451.30 / 536.64 / 640.49 nm |
| CI-05 | Photometric accuracy ref standard | K₂Cr₂O₇ in 0.005 M H₂SO₄ at 235 / 257 / 313 / 350 nm |
| CI-06 | Stray-light ref solutions | KCl 12 g/L @ 200 nm; NaI 10 g/L @ 220 nm; NaNO₂ 50 g/L @ 340 nm |
| CI-07 | LIMS push gate | QC Manager approval + SST_status pre-check |
| CI-08 | Backup retention | 25 y product-release-linked; 7 y default |
| CI-09 | Audit-trail review cadence | Per batch (Senior Analyst); monthly (QC Manager) |
| CI-10 | Re-qualification matrix | Full PQ on lamp / monochromator change; partial SST on routine PM |

## 6. Risks (FS-level)

| ID | Risk | Mitigation |
|---|---|---|
| FR-01 | Calibration drift between scheduled SSTs | FS-SST-04 trend + early-warning band |
| FR-02 | Silent re-baseline | FS-PROC-01 RFC + FS-AUD-02 append-only |
| FR-03 | LIMS push of unapproved | FS-INT-LIMS-02 state-gate + FS-INT-LIMS-03 SST-gate |
| FR-04 | Stray-light degradation | FS-CMP-03 + FS-SST-01 cadence |
| FR-05 | Reference-standard expiry slip | FS-REF-02 pre-flight + FS-REF-04 disposal log |
| FR-06 | Cuvette mismatch in assay | FS-CELL-01 matched-pair qual + FS-CELL-02 cuvette-ID logging |
| FR-07 | Photometric linearity failure | FS-CMP-05 5-point r² ≥ 0.999 gate |

## 7. References

ERA-URS-UVVIS-001 v1.2; 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .160, .165, .192, .194; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <857>; USP <1058>; USP <1225>; USP <1226>; Ph. Eur. 2.2.25; ICH Q2(R2); PIC/S PI 041; ISPE GAMP 5 (2nd ed., 2022); Agilent — *Cary 3500 + UV WorkStation v3 Reference*.

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-PLAT-01 | FS-PLAT-01 |
| URS-PLAT-02 | FS-PLAT-02 |
| URS-PLAT-03 | FS-PLAT-03 |
| URS-PLAT-04 | FS-PLAT-04 |
| URS-PLAT-05 | FS-PLAT-05 |
| URS-SW-01 | FS-SW-01 |
| URS-SW-02 | FS-SW-02 |
| URS-SW-03 | FS-SW-03 |
| URS-SW-04 | FS-SW-04 |
| URS-SW-05 | FS-SW-05 |
| URS-SW-06 | FS-SW-06 |
| URS-MTH-01 | FS-MTH-01 |
| URS-MTH-02 | FS-MTH-02 |
| URS-MTH-03 | FS-MTH-03 |
| URS-MTH-04 | FS-MTH-04 |
| URS-ACQ-01 | FS-ACQ-01 |
| URS-ACQ-02 | FS-ACQ-02 |
| URS-ACQ-03 | FS-ACQ-03 |
| URS-ACQ-04 | FS-ACQ-04 |
| URS-ACQ-05 | FS-ACQ-05 |
| URS-CMP-01 | FS-CMP-01 |
| URS-CMP-02 | FS-CMP-02 |
| URS-CMP-03 | FS-CMP-03 |
| URS-CMP-04 | FS-CMP-04 |
| URS-CMP-05 | FS-CMP-05 |
| URS-CMP-06 | FS-CMP-06 |
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
| URS-REF-05 | FS-REF-05 |
| URS-CELL-01 | FS-CELL-01 |
| URS-CELL-02 | FS-CELL-02 |
| URS-CELL-03 | FS-CELL-03 |
| URS-CELL-04 | FS-CELL-04 |
| URS-CALC-01 | FS-CALC-01 |
| URS-CALC-02 | FS-CALC-02 |
| URS-CALC-03 | FS-CALC-03 |
| URS-CALC-04 | FS-CALC-04 |
| URS-CALC-05 | FS-CALC-05 |
| URS-PROC-01 | FS-PROC-01 |
| URS-PROC-02 | FS-PROC-02 |
| URS-PROC-03 | FS-PROC-03 |
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
| URS-PART11-08 | FS-PART11-08 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-INT-LIMS-01 | FS-INT-LIMS-01 |
| URS-INT-LIMS-02 | FS-INT-LIMS-02 |
| URS-INT-LIMS-03 | FS-INT-LIMS-03 |
| URS-INT-AD-01 | FS-INT-AD-01 |
| URS-PERF-01 | FS-PERF-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-SEC-01 | FS-SEC-01 |
| URS-TRN-01 | FS-TRN-01 |
| URS-PR-01 | FS-PR-01 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

The following risks are noted for downstream evaluation in the Risk Assessment.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Silent re-baseline / peak-pick override producing biased result | Medium | High | URS-PROC-01 (RFC) + URS-PROC-02 (raw data lock) |
| R-02 | LIMS push of unapproved result | Medium | High | URS-INT-LIMS-02 (e-sign gate) |
| R-03 | SST overdue, missed, or out-of-trend | Medium | High | URS-SW-03 + URS-ACQ-02 + URS-SST-03 |
| R-04 | Audit-trail tampering | Low | High | URS-AUD-02 + URS-DI-06 |
| R-05 | Wavelength accuracy drift between scheduled SSTs (lamp aging, alignment drift) | Medium | High | URS-SST-04 (early-warning trend band) + URS-AIQ-05 (re-qual on lamp change) |
| R-06 | Photometric linearity failure outside method working range | Low | High | URS-CMP-05 (5-point r² ≥ 0.999) + URS-CALC-04 (calculation audit) |
| R-07 | Stray-light degradation (filter / grating contamination) producing falsely low absorbance | Medium | High | URS-CMP-03 (stray-light test) + URS-SST-01 cadence |
| R-08 | Expired or mis-identified reference standard in use | Medium | High | URS-REF-01 + URS-REF-02 (block-on-expiry) |
| R-09 | Cuvette mismatch (un-matched pair or chipped cell) in assay | Medium | Medium | URS-CELL-01 + URS-CELL-02 |
| R-10 | Sample carry-over between high- and low-concentration runs | Low | Medium | URS-CELL-03 (carry-over verification) |

Full evaluation in `ERA-RA-UVVIS-001` *(synthetic)*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
