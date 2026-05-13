---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-27; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "PharmaDevils UV-Visible Spectrophotometer URS family"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11; EU GMP Annex 11"
  - "USP <857> UV-Visible Spectroscopy"
  - "USP <1058> Analytical Instrument Qualification"
  - "USP <1224>, <1225>, <1226> — Transfer / Validation / Verification of compendial procedures"
  - "Ph. Eur. 2.2.25 Absorption Spectrophotometry, Ultraviolet and Visible"
  - "ICH Q2(R2); PIC/S PI 041"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## UV-Vis Spectrophotometer Computer System — Agilent Cary 3500 + UV WorkStation v3

**Document Number:** ERA-URS-UVVIS-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Erato Labs ehf, QC Spectroscopy, Reykjavík, Iceland *(fictional)*
**System Owner:** QC Manager — Spectroscopy
**Process Owner:** Head of Quality Control
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Agilent Cary 3500 + UV WorkStation v3** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a)/(d)/(e)/(k), .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .160, .165, .194; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <857> (UV-Vis Spectroscopy); USP <1058> AIQ; USP <1225>; Ph. Eur. 2.2.25; ICH Q2(R2); PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Spectroscopy) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Reviewer (Quality Assurance) | _____________ | _____________ | _____ |
| Approver (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Range-compression removed; per-ID Part 11 + DI breakouts. |
| 1.2 | 2026-05-12 | (synthetic) | Authored to Tier T2 (Cat 4 configured lab instrument; 60-req target; spans USP <857> SST + Ph. Eur. 2.2.25 + AIQ DQ/IQ/OQ/PQ per USP <1058> + reference-standard lifecycle + LIMS interface). New § 5 subsections: USP/Ph. Eur. compendial compliance; AIQ + mechanical/hardware qualification; system-suitability test (SST) battery; reference standard + traceability mgmt; cuvette + sample-handling controls; reportable-result + OOS detection; Part 11 + ALCOA+ per-clause expansion. |

## Definitions

| Term | Definition |
|---|---|
| UV-Vis | Ultraviolet-visible absorption spectrophotometry (190–1100 nm operational range) |
| Cary 3500 | Agilent Cary 3500 UV-Vis spectrophotometer (Compact / Multicell / Multizone configurations) |
| UV WorkStation | Agilent UV WorkStation 21 CFR Part 11 software v3 |
| Method | Stored measurement procedure (wavelength, slit width, scan range, mode, calibration tie) |
| SST | System Suitability Test — pre-run instrument checks |
| AIQ | Analytical Instrument Qualification (USP <1058> DQ → IQ → OQ → PQ) |
| Holmium oxide | NIST-traceable wavelength accuracy reference standard (HoO solution or filter, peaks 241.13, 287.15, 361.31, 451.30, 536.64, 640.49 nm) |
| Potassium dichromate | Photometric linearity / accuracy reference (K₂Cr₂O₇ in 0.005 M H₂SO₄) per Ph. Eur. 2.2.25 |
| Nicotinic acid | Wavelength accuracy reference for solution-mode UV (peak 261 nm) per Ph. Eur. 2.2.25 |
| Stray light | Light reaching the detector outside the bandpass; USP <857> test uses KCl 12 g/L (200 nm), NaI 10 g/L (220 nm), NaNO₂ 50 g/L (340 nm) |
| Bandwidth (SBW) | Spectral bandwidth — slit width × dispersion; USP <857> requires ≤ method-specified value |
| Cuvette | Sample cell; quartz (UV) or glass (Vis); typical path-length 1 cm |
| LIMS | LabWare LIMS 8 |
| RFC | Reason-for-change — captured rationale on data modification |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| OOS | Out-of-Specification result triggering investigation per 21 CFR § 211.192 |

## 1. Purpose

This URS defines requirements for the UV-Vis spectrophotometer computer system used in QC release and stability testing at Erato Labs. The system supports identification, assay, content-uniformity, and dissolution-related photometric measurements per the relevant USP / Ph. Eur. monographs. The URS binds the Cary 3500 + UV WorkStation v3 deployment to 21 CFR Part 11 (electronic records / signatures), EU GMP Annex 11 (computerised systems), USP <857> (UV-Vis SST), USP <1058> (analytical instrument qualification), Ph. Eur. 2.2.25 (absorption spectrophotometry), USP <1225> (validation of compendial methods), and PIC/S PI 041 (data integrity).

## 2. Scope

**In:** Agilent Cary 3500 instrument (double-beam, dual-monochromator); UV WorkStation v3 client on a dedicated PC (Windows 11 Enterprise LTSC); Active Directory authentication; integration with LabWare LIMS 8 (worklist import + result push); daily backup; NTP sync; USP <857> SST procedures; reference-standard lifecycle (holmium oxide, potassium dichromate, nicotinic acid, KCl/NaI/NaNO₂ stray-light solutions, didymium / rare-earth filters); method registry; reportable-result rounding and OOS detection.

**Out:** Cary 3500 hardware-level equipment qualification (separate IQ/OQ protocols owned by Engineering); LIMS sample-lifecycle (sample login, COA generation — owned by LIMS URS); UV WorkStation SDLC (Agilent-owned per GAMP Cat 4); instrument-room environmental qualification (owned by Facilities EMS).

## 3. System Description and Intended Use

UV WorkStation is the system of record for UV-Vis measurement data generated by the Cary 3500. Methods are managed under change control; analyses are run from worklists; results are reviewed and approved through the e-signature workflow; approved results are pushed to LIMS. GAMP Cat 4: Agilent maintains the software SDLC; site validation focuses on installation, configuration, Part 11 controls, USP <857> SST configuration, reference-standard management, and the LIMS interface.

Intended use: identification (compendial UV identity test), assay (Beer-Lambert at λmax with reference-standard bracketing), content uniformity (USP <905> companion measurements), dissolution UV readback (companion to USP <711> apparatus output), photometric impurity limit tests, and stability time-point assays. Out-of-scope intended uses include dissolved-oxygen / turbidimetric measurements (separate instrument), preparative spectrophotometry, and any non-GxP research workflow.

## 4. User Roles

| Role | Permissions |
|---|---|
| Analyst | Acquire and process spectra; cannot edit method / configuration; cannot approve results. |
| Senior Analyst | All Analyst + second-person review (audit-trail review per batch). |
| Method Owner | Author / edit methods under change control; cannot approve own method changes. |
| QC Manager | Approve, lock, release results to LIMS; approve method effectivity. |
| System Administrator | OS / app config, AD groups, Part 11 settings; cannot approve methods or results. |
| Reference Standard Custodian | Receive / log / dispose reference standards; cannot run analyses. |
| Quality Assurance | Approve periodic review; second-approver on Part-11-impacting changes. |
| Auditor | Read-only across data, audit trails, periodic review records. |

**Separation of Duties:** Analyst ≠ Reviewer ≠ Approver. Method Owner ≠ Method Approver. System Administrator ≠ QC Approver. Reference Standard Custodian ≠ Analyst on same run.

## 5. User Requirements

### 5.1 Platform / Hardware

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | M | R2 | The system shall be installed on a standalone PC on the lab-IT VLAN, segregated from the corporate user network. |
| URS-PLAT-02 | H | R1 | The system clock shall be NTP-synchronised to the validated site time source; skew shall be monitored with alert at > 1 s drift. |
| URS-PLAT-03 | H | R1 | The PC shall be backed by a UPS sized for ≥ 30 min of controlled shutdown to prevent data corruption on mains failure. |
| URS-PLAT-04 | M | R2 | The Cary 3500 instrument shall be sited per vendor environmental envelope (15–30 °C; 20–80% RH non-condensing) with continuous environmental monitoring. |
| URS-PLAT-05 | M | R2 | The system shall log USB / removable-media insertion events to the OS audit trail. |

### 5.2 Software Configuration (per GAMP Cat 4)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SW-01 | H | R1 | UV WorkStation v3 shall be installed with the 21 CFR Part 11 module enabled; configuration settings (audit trail required, e-sign required, raw data lock, project policy) shall be applied per site policy and captured in the Configuration Specification. |
| URS-SW-02 | H | R1 | Methods shall be stored in a controlled methods folder; per-method access shall be enforced via AD-mapped roles. |
| URS-SW-03 | H | R1 | USP <857> calibration verification shall be configured for daily and weekly cadences per method category. |
| URS-SW-04 | H | R1 | The Part 11 module shall enforce minimum password length ≥ 12 characters, complexity (≥ 3 of 4 classes), and rotation ≤ 90 days per 21 CFR § 11.300. |
| URS-SW-05 | M | R2 | The system shall maintain a Configuration Specification (CS-EMPOWER-equivalent) listing all Part 11 settings, project policies, and AD group bindings; any change shall traverse change control. |
| URS-SW-06 | H | R1 | Vendor patches (Agilent SCN releases) shall be applied only after site change-control approval; the installed UV WorkStation build shall match the CS-approved version. |

### 5.3 Method Lifecycle and Acquisition

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MTH-01 | H | R1 | Methods shall follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE; only EFFECTIVE methods may be used for GxP samples. |
| URS-MTH-02 | H | R1 | Method state transitions shall require role-restricted electronic signatures with separation of duties (Author ≠ Approver). |
| URS-MTH-03 | H | R1 | Method changes that affect calibration tie, reference standard, slit width, or λ_target shall require re-verification per USP <1225> (method validation) or USP <1226> (method verification) as applicable, with evidence attached. |
| URS-MTH-04 | H | R1 | Method version history shall be retained with redline / diff visibility for ≥ retention period. |
| URS-ACQ-01 | H | R1 | Each acquisition shall capture sample identifier, cuvette path-length, baseline + blank scans, and USP <857> SST status (wavelength accuracy, photometric accuracy, stray light) at sequence start. |
| URS-ACQ-02 | H | R1 | A sequence-start validator shall reject runs when SST is overdue, the instrument is not in Ready state, or the method is not EFFECTIVE. |
| URS-ACQ-03 | H | R1 | The system shall capture the spectral bandwidth (SBW), scan rate, integration time, and detector mode for every acquisition. |
| URS-ACQ-04 | M | R2 | Baseline and 100%-T correction routines shall be logged with timestamp and operator identity per acquisition. |
| URS-ACQ-05 | M | R2 | The system shall reject any acquisition where the bracketing reference-standard absorbance falls outside ± 2.0% of nominal for assay methods. |

### 5.4 USP / Ph. Eur. Compendial Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CMP-01 | H | R1 | The instrument shall meet USP <857> performance criteria: wavelength accuracy ± 1 nm in UV (200–400 nm), ± 3 nm in Visible (400–800 nm) verified against NIST-traceable holmium oxide. |
| URS-CMP-02 | H | R1 | The instrument shall meet USP <857> photometric accuracy ± 1.0% of nominal absorbance verified against NIST-traceable potassium dichromate at 235, 257, 313, 350 nm or equivalent reference. |
| URS-CMP-03 | H | R1 | The instrument shall demonstrate stray light ≤ specification at 200 nm (KCl 12 g/L), 220 nm (NaI 10 g/L), 340 nm (NaNO₂ 50 g/L) per USP <857>; failure shall block GxP runs. |
| URS-CMP-04 | H | R1 | The instrument shall meet Ph. Eur. 2.2.25 control-of-absorbance criteria (verified against potassium dichromate in 0.005 M H₂SO₄) when used for EP-monograph methods. |
| URS-CMP-05 | H | R1 | The instrument shall demonstrate photometric linearity from 0 to ≥ 2.0 A (or method working range) with r² ≥ 0.999 across a ≥ 5-point standard curve per USP <857>. |
| URS-CMP-06 | M | R2 | The system shall capture compendial method designations (USP-NF, Ph. Eur., JP) in the method header and constrain calculation rounding per the cited compendium. |

### 5.5 AIQ — DQ / IQ / OQ / PQ per USP <1058>

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AIQ-01 | H | R1 | Design Qualification (DQ) shall document fitness for intended use against Beer-Lambert range, λ working range, SST capability, and Part 11 integration. |
| URS-AIQ-02 | H | R1 | Installation Qualification (IQ) shall verify physical installation, network / AD integration, software version, optical alignment, and lamp installation per vendor SOP. |
| URS-AIQ-03 | H | R1 | Operational Qualification (OQ) shall include: wavelength accuracy + repeatability, photometric accuracy + linearity, stray light, resolution (toluene-in-hexane test, USP <857>), noise + drift, baseline flatness. |
| URS-AIQ-04 | H | R1 | Performance Qualification (PQ) shall be executed at site go-live, on major change (lamp replacement, monochromator service, software upgrade), and at least annually. |
| URS-AIQ-05 | M | R2 | Re-qualification thresholds shall be defined: full PQ after deuterium / tungsten-halogen lamp replacement; partial PQ (SST only) after planned maintenance not affecting the optical bench. |
| URS-AIQ-06 | M | R2 | Qualification evidence (raw scans, calculations, certificates) shall be retained for ≥ 25 years per product-release tie. |

### 5.6 System Suitability Test (SST) Battery

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SST-01 | H | R1 | The SST battery shall include wavelength accuracy (holmium oxide), photometric accuracy (potassium dichromate or NIST SRM 935a), stray light (per § 5.4), and noise / drift (water blank) per the cadence in URS-SW-03. |
| URS-SST-02 | H | R1 | SST results shall be captured automatically with operator identity, timestamp, reference-standard ID, certificate expiry, and pass / fail evaluation against method-defined limits. |
| URS-SST-03 | H | R1 | An SST failure shall set the instrument to NOT READY; the system shall block GxP acquisitions until SST is re-passed or a documented Engineering override (with QA approval) is applied. |
| URS-SST-04 | M | R2 | The system shall trend SST results across rolling 12 months and alert on drift exceeding ½ of the USP <857> acceptance limit (early-warning band). |
| URS-SST-05 | M | R2 | Periodic SST review shall be a documented step in the monthly audit-trail review. |

### 5.7 Reference Standard and Traceability Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REF-01 | H | R1 | Reference standards (holmium oxide solution / filter, potassium dichromate, nicotinic acid, KCl / NaI / NaNO₂ stray-light solutions, didymium filter, USP-NF or Ph. Eur. chemical reference substances) shall be logged with lot number, source, COA, NIST traceability where applicable, receipt date, opening date, and expiry. |
| URS-REF-02 | H | R1 | The system shall block use of an expired or unidentified reference standard at sequence start. |
| URS-REF-03 | M | R2 | The Reference Standard Custodian shall maintain a register integrated with the UV WorkStation method-execution layer (reference-standard ID required per SST and per bracketed assay). |
| URS-REF-04 | M | R2 | Disposal of expired standards shall be logged with operator identity, disposal date, and disposal route per site SOP. |
| URS-REF-05 | M | R2 | Reference standard re-qualification (in-house re-certification against a higher-order NIST / NMI standard) shall be permitted only under a written re-qualification SOP, with QA approval. |

### 5.8 Cuvette / Cell + Sample-Handling Controls

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CELL-01 | H | R1 | Cuvettes shall be qualified per path-length tolerance (± 0.005 cm for 1 cm cells) per USP <857>; matched-pair cuvettes shall be used for assay measurements. |
| URS-CELL-02 | M | R2 | The system shall capture cuvette identifier per acquisition to support matching-pair traceability. |
| URS-CELL-03 | M | R2 | Cleaning between samples shall follow a documented cuvette-cleaning SOP; carry-over verification shall be a method-execution step when carry-over is method-relevant. |
| URS-CELL-04 | M | R2 | Multi-cell sample-changer position assignment shall be logged with sample identity per acquisition; misplaced-sample detection (mismatch between expected and operator-confirmed position) shall trigger a re-confirmation prompt. |

### 5.9 Reportable Result, Calculation, and OOS Detection

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CALC-01 | H | R1 | Reportable result rounding shall comply with the cited compendium (USP-NF, Ph. Eur., JP); rounding rules shall be configurable per method and locked at method approval. |
| URS-CALC-02 | H | R1 | OOS detection shall be automatic against method-defined spec limits; OOS results shall be flagged and shall trigger an OOS investigation workflow per 21 CFR § 211.192 (delegated to LIMS). |
| URS-CALC-03 | M | R2 | Significant-figures handling shall be method-configurable per the test category (assay, identification, limit test). |
| URS-CALC-04 | M | R2 | Result reports shall include all raw absorbance readings, baseline / blank scans, SST status, reference-standard IDs, and calculation audit. |
| URS-CALC-05 | M | R2 | A reportable result shall be the average of method-specified replicates with RSD evaluated against method-defined acceptance criteria. |

### 5.10 Data Integrity, Part 11, and Audit Trail

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PROC-01 | H | R1 | Manual data adjustments (re-baseline, peak-pick override, integration boundary edit) shall require captured reason-for-change (RFC) per 21 CFR § 11.10(e) + EU GMP Annex 11 § 9. |
| URS-PROC-02 | H | R1 | A raw data lock shall prevent post-acquisition modification of source spectra; deletion of raw data shall be cryptographically prevented or, where vendor architecture allows, audit-trailed and require QA co-sign. |
| URS-PROC-03 | H | R1 | Result reports shall be generated as PDF including raw spectrum, processing parameters, SST status, calculated value vs spec, ALCOA+ statement, and SHA-256 hash of the underlying raw data. |
| URS-AUD-01 | H | R1 | The audit trail shall cover methods, sequences, results, configuration, signature events, and reference-standard register actions. |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only; deletion shall be cryptographically prevented at the application layer. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be conducted by a Senior Analyst per batch and by the QC Manager monthly; review evidence shall be retained. |
| URS-AUD-04 | H | R1 | Audit-trail retention shall be ≥ 7 years; ≥ 25 years if linked to product release per EU GMP retention rules. |
| URS-PART11-01 | H | R1 | The system shall implement procedural and operational controls protecting electronic-record validity per 21 CFR § 11.10(a). |
| URS-PART11-02 | H | R1 | The system shall be capable of generating accurate and complete copies of records in human-readable and electronic form per § 11.10(b). |
| URS-PART11-03 | H | R1 | The system shall protect electronic records throughout the retention period against unauthorised alteration per § 11.10(c). |
| URS-PART11-04 | H | R1 | The system shall limit access to authorised individuals per § 11.10(d) via AD-mapped role bindings. |
| URS-PART11-05 | H | R1 | The system shall apply electronic signatures bearing user name, date / time, and meaning of signature per § 11.50. |
| URS-PART11-06 | H | R1 | The system shall link e-signatures to their records cryptographically per § 11.70. |
| URS-PART11-07 | H | R1 | Signatures shall be unique to one individual and shall not be reused / reassigned per § 11.100. |
| URS-PART11-08 | H | R1 | Identity-based signature components shall require re-authentication at critical moments per § 11.200. |
| URS-DI-01 | H | R1 | Data shall be attributable: every acquisition shall record operator identity per ALCOA+ + PIC/S PI 041. |
| URS-DI-02 | H | R1 | Data shall be legible: PDF reports + audit trails shall render in human-readable form. |
| URS-DI-03 | H | R1 | Data shall be contemporaneous: timestamps shall be NTP-derived per URS-PLAT-02. |
| URS-DI-04 | H | R1 | Data shall be original: raw spectra shall be the source record; all derived calculations shall trace to raw. |
| URS-DI-05 | H | R1 | Data shall be accurate: SST status (URS-SST-01) shall gate the run; bracketed reference shall confirm calibration tie per acquisition (URS-ACQ-05). |
| URS-DI-06 | H | R1 | Data shall be complete: deletion of raw or audit records shall be cryptographically prevented; archival shall preserve all attributes. |

### 5.11 Integrations, Performance, Backup, Security, Training, PR

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-LIMS-01 | H | R1 | The system shall import worklists from LIMS via the Agilent LIMS connector. |
| URS-INT-LIMS-02 | H | R1 | Approved results shall be pushed to LIMS only after QC Manager approval (e-sign-gated). |
| URS-INT-LIMS-03 | M | R2 | The LIMS interface shall reject result push when SST is failed or expired per URS-SST-03. |
| URS-INT-AD-01 | H | R1 | Authentication shall use AD; no local accounts shall exist other than the vendor break-glass account, which shall require QA approval and post-use review. |
| URS-PERF-01 | M | R2 | Sequence start latency shall be ≤ 5 s; data save per acquisition ≤ 2 s. |
| URS-BAK-01 | H | R1 | Daily backup shall include methods, raw acquisitions, audit trails, reference-standard register, and configuration; retention 25 years. |
| URS-BAK-02 | H | R1 | A quarterly restore test shall be witnessed and recorded. |
| URS-SEC-01 | H | R1 | Removable media shall be blocked except for vendor-approved engineering use under change control. |
| URS-TRN-01 | H | R1 | Role-specific training shall be LMS-recorded; SST-execution training shall be re-qualified annually. |
| URS-PR-01 | H | R1 | An annual periodic review shall cover method inventory, audit-trail review evidence, SST compliance, reference-standard register health, deviation summary, and training currency; signed by QC Manager + Head of QA. |

### 5.12 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem; conditional-access policy `Lab-Workstation Conditional Access (MFA on interactive logon)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T3 with RPO ≤ 72 h and RTO ≤ 72 BH; backup integration shall use Veeam file-level capture of the UV-Vis software's result database and method library; the application team shall participate in annual application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 7 y per the consuming-record schedule. |

## 6. Acceptance Criteria

CS, RA, IQ, OQ (USP <857> SST battery + USP <1058> mechanical / hardware checks), PQ approved and executed; VSR approved by QC Manager + Head of QA; RTM closed at 100% URS-ID coverage.

## 7. Constraints

- Agilent SCN updates shall be applied only under change control.
- Reference-standard certificates shall be NIST-traceable where compendial standards require it (holmium oxide, potassium dichromate).
- Cuvette path-length tolerance is a method-execution constraint, not a software constraint — the Quality Unit must verify per analyst training.

## 8. Assumptions

- AD, LIMS, NTP, and environmental monitoring are validated upstream.
- Reference-standard supply chain (USP-NF, Ph. Eur. CRS) is stable.
- Agilent UV WorkStation v3 SDLC evidence is available via the vendor for the GAMP Cat 4 vendor-reliance section of the CS.

## 9. References

**US / FDA:**
- 21 CFR Part 11 §§ .10(a)/(b)/(c)/(d)/(e)/(k), .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .68 (automatic, mechanical, and electronic equipment), .160 (laboratory control), .165 (testing and release for distribution), .192 (production-record review / OOS), .194 (laboratory records)
- FDA *Guidance on Data Integrity and Compliance with cGMP* (2018)

**EU / EMA:**
- EU GMP Annex 11 §§ 4 (validation), 6 (accuracy checks), 9 (audit trail), 11 (periodic evaluation)
- EudraLex Volume 4 — GMP Parts I + III
- Ph. Eur. 2.2.25 — Absorption Spectrophotometry, Ultraviolet and Visible
- Ph. Eur. 2.2.40 — Near-Infrared Spectroscopy (referenced for cross-compatibility)

**International:**
- ICH Q2(R2) — Validation of Analytical Procedures
- USP <857> — Ultraviolet-Visible Spectroscopy
- USP <1058> — Analytical Instrument Qualification (DQ / IQ / OQ / PQ framework)
- USP <1225> — Validation of Compendial Procedures
- USP <1226> — Verification of Compendial Procedures
- USP <1224> — Transfer of Analytical Procedures
- PIC/S PI 041 — Good Practices for Data Management and Integrity
- ISPE GAMP 5 (2nd Edition, 2022); GAMP GPG *Records and Data Integrity*; GAMP GPG *Validation of Laboratory Computerized Systems*

**Vendor:**
- Agilent — *Cary 3500 UV-Vis Spectrophotometer Configuration Reference* (current rev.)
- Agilent — *UV WorkStation v3 21 CFR Part 11 Compliance Guide*

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

