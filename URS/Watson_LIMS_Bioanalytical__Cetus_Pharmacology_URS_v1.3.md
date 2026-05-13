---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: Claude (Anthropic) — inline batch, 2026-04-27; expanded 2026-05-12 (§5 breakout + DACH context + ICH M10 + GLP explicit binding)
seed_corpus_basis:
  - GAMP 5 (2nd ed.) Cat 4 conventions
  - 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Part 58 (GLP) §§ .29, .35, .81, .120, .130, .185, .190, .195
  - FDA Bioanalytical Method Validation Guidance for Industry (2018)
  - EMA Guideline on Bioanalytical Method Validation (2011, EMEA/CHMP/EWP/192217/2009)
  - ICH M10 — Bioanalytical Method Validation and Study Sample Analysis (2022)
  - ICH E6(R3) GCP (Step 4, adopted 6 January 2025); OECD Principles of GLP (1998 with consolidated revisions)
  - BfR (DE) GLP-Bundesstelle (Federal Bureau for GLP) + Länder authorities for German GLP monitoring; BfArM (DE) for medicines + devices (not GLP); Swissmedic (CH); AGES (AT)
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# User Requirements Specification (URS)

## Bioanalytical LIMS — Thermo Fisher Watson LIMS 7.6 (Regulated Bioanalysis)

**Document Number:** CET-URS-WATSON-001 | **Version:** 1.0 | **Effective Date:** 2026-04-27 *(synthetic)*
**Site:** Cetus Pharmacology GmbH, Bioanalytical Services, Heidelberg, Germany *(fictional)*
**System Owner:** Director, Bioanalytical Operations
**Process Owner:** VP Drug Metabolism & Pharmacokinetics
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Thermo Fisher Watson LIMS 7.6 (Regulated Bioanalysis)** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Part 58 (GLP); FDA *Bioanalytical Method Validation Guidance for Industry* (2018); EMA *Guideline on Bioanalytical Method Validation* (2011); ICH M10 (2022); ICH E6(R3) GCP (Step 4, adopted 6 January 2025); OECD Principles of GLP; **BfR GLP-Bundesstelle (DE)** + Länder authorities for German GLP monitoring (note: GLP is NOT BfArM's remit; BfArM covers medicines + devices); Swissmedic (CH) bioanalytical guidance; AGES (AT).

> **Note:** Distinct from the LabWare LIMS 8 URS (CTX-URS-LIMS-001 — GMP manufacturing QC) and the STARLIMS 12 URS (OCT-URS-LIMS-001 — CLIA clinical diagnostics). This URS covers a **bioanalytical LIMS** for regulated PK / PD / TK / immunogenicity sample analysis (LC-MS/MS + ligand binding) supporting clinical trials (ICH E6(R3) GCP) and GLP toxicology (21 CFR Part 58 / OECD GLP).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Bioanalytical Operations) | _____________ | _____________ | _____ |
| Reviewer (Study Director — GLP per 21 CFR § 58.33) | _____________ | _____________ | _____ |
| Reviewer (Principal Investigator — GLP multi-site) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Quality Assurance Unit — per 21 CFR § 58.35) | _____________ | _____________ | _____ |
| Approver (VP DMPK) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-12 | (synthetic) | §5 broken out into 12 subsections; DACH relocation (Heidelberg, DE); ICH M10 acceptance criteria explicit; 21 CFR Part 58 GLP sub-section bindings; OECD GLP added; Study Director (§ 58.33) + Principal Investigator (multi-site GLP convention per OECD; not separately CFR-defined) + QAU (§ 58.35) roles separated; risk table expanded. |
| 1.2 | 2026-05-13 | (synthetic) | T3 enrichment (LIMS-class enterprise system; 100-150 req target). Added §§ 5.13 Sample Receipt + Aliquoting + Storage Lifecycle, 5.14 Study Build + Protocol Pinning, 5.15 LBA-Specific Workflow (ligand-binding assays + immunogenicity), 5.16 ISR + Stability Sample Reanalysis, 5.17 Run Review + Re-assay Decision Tree, 5.18 Reportable-Result Release Workflow, 5.19 Study Report Builder per § 58.185, 5.20 GLP Archive Workflow per § 58.190, 5.21 Inspection-Readiness Tenant. Expanded §§ 5.2 ICH M10 with selectivity / accuracy / precision detail, 5.6 Part 11 sub-section rows. New risks (R-13..R-18): GLP-archive deletion before retention, study-protocol amendment un-pinned, ISR mis-categorisation between clinical / non-clinical, LBA matrix-effect under-evaluation, immunogenicity titer ladder mis-computation, multi-site PI sign-off cycle stall. Web-research citations: 21 CFR Part 58 §§ .29, .81, .120, .130, .185, .190, .195 explicit; OECD GLP Principles 1.3 + 2.2 + 4 + 7 + 8 + 10; FDA WL precedent (PPD Bioanalytical 2021 — ISR documentation gaps). |

## Definitions

| Term | Definition |
|---|---|
| Watson LIMS | Thermo Fisher Watson LIMS 7.6 |
| Bioanalysis | Quantitation of drug + metabolites in biological matrices (plasma, serum, urine, tissue) |
| LC-MS/MS | Liquid chromatography–tandem mass spectrometry |
| LBA | Ligand-Binding Assay |
| ISR | Incurred Sample Reanalysis (per ICH M10) |
| Calibration Curve | Standard curve over the validated dynamic range |
| QC | Quality control sample (LLOQ-QC, LQC, MQC, HQC, ULOQ-QC) |
| GLP | Good Laboratory Practice (21 CFR Part 58 / OECD GLP) |
| Study Director | Single point of overall study responsibility per 21 CFR § 58.33 |
| Principal Investigator | Per-site responsible person under the Study Director in multi-site GLP studies (OECD GLP Principle 1.3 / 2.2; not separately defined in 21 CFR Part 58 but used by analogy to Study Director responsibilities under § 58.33). |
| QAU | Quality Assurance Unit (21 CFR § 58.35) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the bioanalytical LIMS used to manage GLP-regulated (21 CFR Part 58 / OECD) and GCP-regulated (ICH E6(R3)) PK / PD / TK / immunogenicity sample analysis at Cetus, supporting drug-development programmes for sponsors filing to FDA / EMA / BfArM / Swissmedic.

## 2. Scope

**In:** Watson LIMS 7.6 application servers + Oracle 19c with Data Guard physical-standby; per-study configuration (matrix, analyte, method, calibrators, QCs, ISR strategy); SSO via Okta + MFA; integrations with the LC-MS/MS instrument cluster (Sciex / Waters), the Empower CDS (separate URS), the SDLC ELN (Benchling) for sample-prep linkage, the eTMF for archive, and the GLP archive system per 21 CFR § 58.190.

**Out:** instrument software (separate URSs per instrument); Empower CDS (separate URS); GLP archive physical infrastructure; clinical-trial CRO sample shipping (sponsor responsibility).

## 3. System Description

Watson is the system of record for bioanalytical samples — sample receipt, sample-storage chain-of-custody, study-build (matrix / analyte / method / calibrator / QC), batch / run construction, run review (calibration-curve fit, QC pass / fail, ISR evaluation), reportable-result release, study-report generation per FDA / EMA / ICH M10. For GLP studies the system implements 21 CFR § 58 structural separation: Study Director responsibility (§ 58.33), QAU independence (§ 58.35), and protocol-version-pinning to actual runs.

GAMP Cat 4: Thermo Fisher maintains the SDLC; site validates per-study build and Part 11 / GLP controls.

## 4. User Roles

| Role | Permissions |
|---|---|
| Bioanalyst | Run sample analyses; cannot release. |
| Senior Bioanalyst / Reviewer | Review batches; cannot self-release; cannot review own analyses. |
| Study Director (GLP) | Final sign-off on the bioanalytical phase; sole responsibility per 21 CFR § 58.33. |
| Principal Investigator (multi-site GLP) | Per-site responsibility under Study Director. |
| Method Owner | Author / edit methods. |
| Method Approver (QA + Study Director) | Approve methods to EFFECTIVE. |
| QA Reviewer (GLP — QAU per 21 CFR § 58.35) | Independent QA review; reports outside the operations chain. |
| LIMS Administrator | Configure; cannot release. |
| Archivist (GLP per § 58.190) | Manage archived records; cannot edit. |
| Auditor | Read-only. |

Standard SoD; GLP-required role separations enforced: Study Director cannot perform analyses; QAU reports independently to senior management per § 58.35(b); Archivist cannot edit archived records per § 58.190.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` direct GxP impact / `R2` indirect / `R3` none).

### 5.1 Platform and Configuration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | Active + DR Watson cluster; RPO ≤ 15 min; RTO ≤ 4 h; annual DR test. |
| URS-PLAT-02 | H | R1 | Oracle 19c Enterprise Edition with Data Guard physical-standby; nightly backup with PITR; quarterly restore test. |
| URS-CFG-01 | H | R1 | Per-study configuration shall follow DRAFT → REVIEW → APPROVED → EFFECTIVE; sign-off required per study before sample analysis. |
| URS-CFG-02 | H | R1 | Configuration changes shall be exportable for inspection by FDA, EMA, **BfR / Länder authorities (GLP)**, BfArM (medicines / devices), and Swissmedic — appropriate authority depending on study type. |

### 5.2 Method Lifecycle and Validation (ICH M10 alignment)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MTH-01 | H | R1 | Each method record shall carry validation status per ICH M10 (full validation / partial validation / cross-validation / non-validated); only fully validated methods shall run regulated samples. |
| URS-MTH-02 | H | R1 | Method approval shall require Author ≠ Approver; QA + Study Director co-approval. |
| URS-MTH-03 | H | R1 | Method-validation parameters (selectivity, specificity, accuracy, precision, linearity, sensitivity / LLOQ, dilution integrity, matrix effect, recovery, carryover, stability) shall be recorded per ICH M10 §§ 3 (chromatographic methods) and 4 (ligand-binding assays) — parameter selection per method type. |
| URS-MTH-04 | H | R1 | Method scope (matrix, species, analyte concentration range) shall be enforced at run-construction; out-of-scope runs shall be blocked. |
| URS-MTH-05 | M | R2 | Method-version drift (e.g., reagent supplier change) shall trigger partial-validation flow per ICH M10 § 6.1 (partial validation / cross-validation). |

### 5.3 Sample Custody and Run Construction

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SMP-01 | H | R1 | Each sample shall carry chain-of-custody from receipt → storage → run; storage-temperature excursion events shall be flagged. |
| URS-SMP-02 | H | R1 | Per 21 CFR § 58.81, sample records shall include collection date, sample type, source, storage location, and chain-of-custody trail. |
| URS-RUN-01 | H | R1 | Runs shall be constructed per the run-acceptance-criteria template (n calibrators + n QCs per level); per-run acceptance evaluated automatically. |
| URS-RUN-02 | H | R1 | **ICH M10 run-acceptance criteria** per §§ 3.3.2 (chromatographic) and 4.3.2 (ligand-binding): for chromatographic — ≥ 75% of calibrators within ± 15% nominal (± 20% at LLOQ); ≥ 67% of QCs within ± 15%, ≥ 50% at each QC level. For LBA — ≥ 75% calibrators within ± 20% (± 25% at LLOQ); ≥ 67% of QCs within ± 20%, ≥ 50% per level. Fail-the-run logic applied per method type. |
| URS-RUN-03 | H | R1 | ISR per ICH M10 § 5 (Incurred Sample Reanalysis): 10% of samples for clinical studies; 7% for non-clinical (toxicology); ISR acceptance ≥ 67% of repeats within ± 20% (chromatographic) / ± 30% (LBA) of the mean original-vs-repeat. |
| URS-RUN-04 | H | R1 | Reanalysis policy (repeat analysis / reassay) shall be configured per study with documented justification rules per ICH M10 §§ 3.3.4 (chromatographic) and 4.3.4 (LBA). |

### 5.4 GLP-Specific Controls (21 CFR Part 58 / OECD GLP)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-GLP-01 | H | R1 | Per 21 CFR § 58.33, the Study Director shall sign off on the bioanalytical phase; signature attributable + non-delegatable. |
| URS-GLP-02 | H | R1 | Per 21 CFR § 58.35, QAU shall have independent access to all study data; QAU review records retained separately. |
| URS-GLP-03 | H | R1 | Per 21 CFR § 58.120, protocol version shall be pinned to the run; protocol amendments shall be controlled. |
| URS-GLP-04 | H | R1 | Per 21 CFR § 58.130, all data shall be recorded directly, promptly, and legibly with the recorder's identification. |
| URS-GLP-05 | H | R1 | Per 21 CFR § 58.185, the final report shall include study identification, dates, materials, methods, results, signatures of Study Director + responsible scientists, QAU statement. |
| URS-GLP-06 | H | R1 | Per 21 CFR § 58.190, all raw data, documentation, protocols, specimens, and final reports shall be archived; archive shall be accessible only via the Archivist. |
| URS-GLP-07 | H | R1 | Per 21 CFR § 58.195, archive retention shall be ≥ 2 years post-Application submission (FDA) or per study contract (typically ≥ 10 years; indefinite for some non-clinical). |

### 5.5 Audit Trail and Records Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | A contemporaneous, time-stamped audit trail shall capture user, action, old value, new value, reason-for-change for all sample / method / run / approval events. |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only at the database level; not editable by LIMS Administrators. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be performed monthly by Operations and per-run by Senior Bioanalyst. |
| URS-AUD-04 | H | R1 | Audit-trail entries from QAU review shall be retained separately and not editable. |

### 5.6 21 CFR Part 11 Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a), procedures and controls shall protect the validity of bioanalytical records. |
| URS-PART11-02 | H | R1 | Per § 11.10(d), access shall be limited via Okta SSO + MFA. |
| URS-PART11-03 | H | R1 | Per § 11.10(e), operational audit trail per § 5.5 shall exist. |
| URS-PART11-04 | H | R1 | Per § 11.50, electronic signatures shall include signer's printed name, date and time, and meaning of signature. |
| URS-PART11-05 | H | R1 | Per § 11.70, signatures shall be cryptographically linked to the signed record. |
| URS-PART11-06 | H | R1 | Per § 11.200, re-authentication required at Study Director sign-off. |
| URS-PART11-07 | H | R1 | Per § 11.300, password / credential controls per site InfoSec policy. |

### 5.7 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | **Attributable:** Every action attributable to a named user; GLP-specific recorder-id captured. |
| URS-DI-02 | H | R1 | **Legible:** Records exportable as PDF/A-3 + machine-readable XML. |
| URS-DI-03 | H | R1 | **Contemporaneous:** Per 21 CFR § 58.130, data recorded promptly. |
| URS-DI-04 | H | R1 | **Original:** Raw chromatograms + LBA plate-reads preserved unaltered. |
| URS-DI-05 | H | R1 | **Accurate:** Calibration-curve regression deterministic and validated under OQ. |
| URS-DI-06 | M | R2 | **Complete / Consistent / Enduring / Available:** Records meet GLP retention obligations (§ 58.195). |

### 5.8 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-CDS-01 | H | R1 | Empower CDS bidirectional integration (worklist out + signed-off result back-flow); checksums on both directions. |
| URS-INT-ELN-01 | H | R1 | Sample-prep records in Benchling ELN shall be cross-referenced to the bioanalytical batch. |
| URS-INT-ETMF-01 | H | R1 | Bioanalytical study-report shall be archived to eTMF per study completion. |
| URS-INT-INST-01 | H | R1 | LC-MS/MS instrument cluster (Sciex / Waters) shall feed acquisition metadata to Watson; instrument-id + serial logged per run. |
| URS-INT-ARCH-01 | H | R1 | GLP archive system interface per § 58.190; archived records shall be Archivist-only-accessible. |

### 5.9 Performance, Availability, Backup

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | Run-construction latency ≤ 30 s for typical 96-sample plate. |
| URS-AV-01 | H | R1 | Availability ≥ 99.5% during business hours; planned maintenance announced ≥ 7 days in advance. |
| URS-BAK-01 | H | R1 | Database backed up nightly with PITR; retention ≥ GLP archive period. |
| URS-BAK-02 | H | R1 | Quarterly restore test with QA witness. |

### 5.10 Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | TLS 1.3 in transit; AES-256 at rest. |
| URS-SEC-02 | H | R1 | Role-based access reviewed quarterly; Study Director and QAU role assignments require formal management approval. |
| URS-SEC-03 | H | R1 | USB / removable media blocked from LIMS workstations; vendor-engineered access via change control only. |
| URS-SEC-04 | M | R2 | Vulnerability scans monthly; critical findings remediated within 30 days. |

### 5.11 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Role-specific training in the LMS shall be completed before access; Study Director and QAU roles require 21 CFR Part 58 GLP training. |
| URS-TRN-02 | M | R2 | Annual refresher training shall cover ICH M10 updates and GLP guidance changes. |
| URS-PR-01 | H | R1 | Annual periodic review shall cover configuration drift, audit-trail review evidence, method-validation status inventory, GLP archive compliance, training currency, integration health; signed by Director Bioanalytical Operations + VP DMPK + VP QA + QAU lead. |

### 5.12 Inspection Readiness

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INS-01 | H | R1 | The system shall support inspection by FDA, EMA, **BfR / Länder GLP authorities (DE)**, Swissmedic (CH GLP + medicines), AGES (AT): complete-study-package export per § 58.185 within 1 business day; audit-trail export per study within 4 business hours. |
| URS-INS-02 | M | R2 | Mock-inspection drills shall be supported by a read-only inspection-tenant view. |

### 5.13 Sample Receipt, Aliquoting, and Storage Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SAMP-01 | H | R1 | Sample receipt shall capture: sponsor study-id, sample-collection date + time, matrix type, anticoagulant, source species + animal-id (non-clinical) or subject-id + study-day (clinical), receipt date + time, receiver-id, container condition. |
| URS-SAMP-02 | H | R1 | Sample-aliquot lifecycle shall be tracked: parent-sample → child-aliquots (per analytical campaign); each aliquot shall have its own freeze/thaw count, location-history, and chain-of-custody trail. |
| URS-SAMP-03 | H | R1 | The system shall enforce per-sample freeze/thaw budget: aliquots exceeding the method-specified max freeze/thaw count (typ. ICH M10 method-validated, often 5 cycles) shall be flagged and shall not be run without Method-Owner override. |
| URS-SAMP-04 | H | R1 | Storage-location history shall capture every freezer-id, shelf, rack, position, in-time, out-time, temperature-on-storage; temperature excursion events (> 1 °C deviation > 4 hours) shall be flagged and propagated to all aliquots in the affected location. |
| URS-SAMP-05 | H | R1 | Sample-destruction shall require Study-Director + QAU eSign per 21 CFR § 58.81; sample-destruction records shall be retained per § 58.195. |
| URS-SAMP-06 | M | R2 | Sample-shipping (cold-chain) shall capture courier, ship date + time, recipient site, in-transit temperature log (digital-data-logger upload); arrival inspection record required at receiving site. |

### 5.14 Study Build and Protocol Pinning per 21 CFR § 58.120

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-STD-01 | H | R1 | Study-build shall require: sponsor + protocol-id + protocol-version + IRB/IEC approval (clinical) or testing-facility approval (GLP) + study-director-assignment (per § 58.33) + method-validation evidence; missing element blocks build. |
| URS-STD-02 | H | R1 | Protocol version shall be pinned at sample-acquisition time; protocol amendments shall create a new pinned version; samples acquired before the amendment shall remain pinned to the prior version unless explicitly migrated under deviation. |
| URS-STD-03 | H | R1 | Per § 58.120(a), study protocol shall include: study purpose, sponsor identity, testing-facility identity, study director, dose route + frequency + duration, test-system characterisation, schedule, sample-collection schedule. |
| URS-STD-04 | H | R1 | Study-protocol amendments per § 58.120(b) shall capture: reason, signature of Study Director, date, version increment; previous-version records remain immutable. |
| URS-STD-05 | M | R2 | Multi-site studies shall list each test site with its assigned Principal Investigator (per multi-site GLP convention); PI shall sign per-site portions of the study report under the Study Director's overall responsibility. |

### 5.15 LBA-Specific Workflow (Ligand-Binding Assays)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LBA-01 | H | R1 | Plate-map handling shall capture per-well: sample-id (or calibrator-level, or QC-level, or blank), replicate-index, well-position; plate-reader output (OD / RLU / counts) bound to wells by position. |
| URS-LBA-02 | H | R1 | LBA calibration-curve fitting shall support 4PL and 5PL logistic models per ICH M10 § 4; curve-quality flags (% back-calculation, % recovery, parallelism) computed per fitted curve. |
| URS-LBA-03 | H | R1 | Anti-drug-antibody (ADA) screening / confirmatory / titer assays shall follow ICH M10 § 4 tiered approach; screening cut-point + confirmatory cut-point method-bound; titer ladder dilution series captured. |
| URS-LBA-04 | H | R1 | Neutralizing-antibody (NAb) cell-based assays shall capture cell-line lot, passage number, plate-control parameters; assay validation per ICH M10 § 4 sub-sections. |
| URS-LBA-05 | M | R2 | Hook-effect detection shall be supported for high-concentration samples in sandwich-format LBAs; flagged samples shall be re-assayed at higher dilution. |

### 5.16 ISR and Stability Sample Reanalysis per ICH M10 § 5

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ISR-01 | H | R1 | ISR sample-selection algorithm shall draw per ICH M10 § 5: 10% of subject samples for clinical PK studies; 7% for non-clinical toxicology studies; selection from samples spanning the assay range (≥ 3 × LLOQ, peak, trough). |
| URS-ISR-02 | H | R1 | ISR pass/fail per ICH M10 § 5: ≥ 67% of repeats within ± 20% (chromatographic) / ± 30% (LBA) of mean(original, repeat); failure triggers investigation + potential study impact assessment. |
| URS-ISR-03 | H | R1 | Per-sample ISR records shall persist original-result, repeat-result, computed-mean, % deviation, pass/fail; ISR study report attaches as appendix to the final study report per § 58.185. |
| URS-ISR-04 | M | R2 | Long-term-stability samples (months stored at validated conditions) shall be re-analysed at scheduled intervals per the method-validation stability plan; results compared to acceptance criteria. |

### 5.17 Run Review and Re-assay Decision Tree

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RVW-01 | H | R1 | Run review shall be performed by a Senior Bioanalyst not involved in the run acquisition; review includes: calibration-curve fit, QC pass/fail, ISR (if applicable), chromatographic / LBA quality flags, deviations. |
| URS-RVW-02 | H | R1 | Re-assay decision tree per ICH M10 §§ 3.3.4 / 4.3.4 shall be configurable per study: instrument failure (re-assay permitted), insufficient sample (no re-assay), failed QC (re-assay batch per defined rules); each decision captured with justification. |
| URS-RVW-03 | H | R1 | Re-injection vs re-extraction shall be distinguished; the system shall track whether re-assayed sample value replaces or supplements the original. |
| URS-RVW-04 | M | R2 | Run-rejection shall require Senior Bioanalyst eSign + reason; rejected runs retained for inspection but excluded from reportable-result computation. |

### 5.18 Reportable-Result Release Workflow

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REL-01 | H | R1 | Reportable-result computation shall follow the method-bound rule (typ. mean of accepted replicates) with rounding per protocol; reportable result distinct from the analytical-batch-level result. |
| URS-REL-02 | H | R1 | Reportable-result release workflow: Bioanalyst → Senior Bioanalyst → Study Director (or PI for site-portion) → QAU; each transition eSigned with closed-list meaning. |
| URS-REL-03 | H | R1 | The system shall prevent the same user from holding two role positions in a release workflow (Author ≠ Reviewer ≠ Approver). |
| URS-REL-04 | M | R2 | Held reportable results (Study-Director-approved but QAU-pending) shall persist for ≤ 14 days; expiry shall trigger Study-Director re-approval. |

### 5.19 Study Report Builder per 21 CFR § 58.185

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RPT-01 | H | R1 | Per § 58.185(a), the final study report shall include: study purpose, identification (sponsor + facility + study-id), testing dates, test article (name + batch + characterisation), test-system characterisation, methods, results, transformed-data summary, QAU statement. |
| URS-RPT-02 | H | R1 | Per § 58.185(a)(13), the report shall include locations where raw data + specimens + final report are stored; archive location auto-populated by the GLP archive interface (FS-INT-ARCH-01). |
| URS-RPT-03 | H | R1 | Per § 58.185(b), report corrections shall be made as numbered amendments with reason; original report immutable. |
| URS-RPT-04 | H | R1 | Per § 58.185(c), Study Director shall sign the final report; signature attributable + non-delegatable per § 58.33. |
| URS-RPT-05 | M | R2 | QAU statement per § 58.35(b) shall include inspection dates, dates findings reported to Study Director + management; auto-populated from QAU review records. |

### 5.20 GLP Archive Workflow per 21 CFR § 58.190

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ARC-01 | H | R1 | Per § 58.190(a), at study completion all raw data, documentation, protocols, specimens, and final reports shall be transferred to the archive; transfer event captured immutably. |
| URS-ARC-02 | H | R1 | Per § 58.190(b), archive access shall be limited to the Archivist role; non-Archivist read access shall be logged and require business justification. |
| URS-ARC-03 | H | R1 | Per § 58.190(c), archived records shall be indexed for retrieval; index shall include study-id, sponsor, dates, materials. |
| URS-ARC-04 | H | R1 | Per § 58.195, retention shall be ≥ 2 years post-Application submission to FDA (typ. ≥ 10 years per sponsor contract); deletion before retention threshold shall be blocked at the system level. |
| URS-ARC-05 | M | R2 | Archive-restore (Archivist-initiated, for inspection or sponsor request) shall produce an audit-trail entry + sponsor / authority correspondence reference. |

### 5.21 Inspection-Readiness Tenant

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-IRT-01 | H | R1 | A read-only inspection tenant shall be provisioned on-demand within 4 business hours per study; tenant shall present a complete view of: study build, raw data, audit trail, signatures, archive index. |
| URS-IRT-02 | H | R1 | The inspection tenant shall NOT permit any write operation; export of records from the tenant shall require Quality-Assurance eSign. |
| URS-IRT-03 | M | R2 | Mock-inspection drills shall exercise the inspection tenant quarterly; findings logged and remediated. |

### 5.22 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem; conditional-access policy `Lab-App Conditional Access (MFA + device-compliance)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with Oracle RMAN for the Watson Oracle backend; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 15 y (bioanalytical record) per the consuming-record schedule. |

### 5.23 Cross-System Integration — Lyrae AI-assist peak review + Helios

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-LYR-01 | M | R2 | When the Watson Bioanalytical AI-assist peak-review feature is enabled, the underlying chromatographic peak-review model shall be served exclusively via the Lyrae AI/ML Model Server (`LYR-URS-MLSRV-001`) so that EU AI Act Annex I controls (Art. 11 Annex IV pack, Art. 12 logging, Art. 14 human oversight, Art. 15 robustness, Art. 73 incident) apply; this feature is opt-in and disabled by default. |
| URS-XINT-LYR-02 | H | R1 | Every AI-assisted peak-review action shall require explicit analyst confirmation (human-in-the-loop) and shall capture the served `model_version`, confidence, raw chromatogram hash, and analyst override flag in the Watson audit trail; bulk-acceptance of AI suggestions shall be technically prevented. |
| URS-XINT-LYR-03 | M | R2 | Inference events from the AI-assist feature shall be forwarded to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract; Helios shall be the system-of-record for audit-trail review of AI-assist peak adjustments on regulated study runs. |
| URS-XINT-LYR-04 | M | R2 | Drift signal from Lyrae for the peak-review model shall be ingested and shall auto-disable the AI-assist feature on documented threshold breach pending Bioanalytical Lead and QA review. |

## 6. Acceptance Criteria

1. CS, RA, IQ, OQ, PQ approved and executed.
2. PQ shall include representative end-to-end study: method validation per ICH M10 → bioanalytical phase with passing runs → ≥ 1 deliberate run-failure scenario (re-run logic exercised) → ISR per ICH M10 → study report per 21 CFR § 58.185 → archive per § 58.190.
3. VSR approved by VP QA + VP DMPK + Director Bioanalytical Operations.
4. RTM shall demonstrate every URS requirement mapped to at least one approved test case.

## 7. Constraints

- Thermo Fisher patches under change control.
- Non-validated methods shall not be used for GLP study samples.
- Study Director sign-off shall not be delegated.
- GLP archive integrity is non-negotiable; the Archivist role shall be the sole gateway.

## 8. Assumptions

- Empower CDS, Benchling ELN, eTMF, Okta, Oracle infra, instrument cluster are themselves validated.
- QAU is structurally independent of operations per § 58.35(b).
- **BfR GLP-Bundesstelle (Federal Bureau for GLP)** at the German Federal Institute for Risk Assessment, working with **Länder (state-level) authorities**, organises GLP monitoring in Germany. BfArM is NOT the GLP inspecting authority; BfArM covers medicinal products + medical devices.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 — Electronic Records; Electronic Signatures.
- **21 CFR Part 58 — Good Laboratory Practice for Nonclinical Laboratory Studies** §§ .29, .33, .35, .81, .120, .130, .185, .190, .195.
- FDA *Bioanalytical Method Validation Guidance for Industry* (2018).

### EU
- EMA *Guideline on Bioanalytical Method Validation* (2011, EMEA/CHMP/EWP/192217/2009).
- EU GMP Annex 11 — Computerised Systems.

### DACH-specific
- **BfR GLP-Bundesstelle (DE)** — Federal Bureau for Good Laboratory Practice at the Bundesinstitut für Risikobewertung, organising GLP monitoring in Germany with the Länder authorities. (BfArM is **not** the GLP authority; it regulates medicinal products + medical devices.)
- **Swissmedic (CH)** — bioanalytical inspection guidance.
- **AGES PharmMed (AT)**.

### International — ICH / OECD
- **ICH M10** — Bioanalytical Method Validation and Study Sample Analysis (2022).
- ICH E6(R3) GCP (Step 4, adopted 6 January 2025).
- OECD Principles of Good Laboratory Practice (1998, consolidated revisions).

### ISPE
- ISPE GAMP 5 (2nd Edition, 2022).

### Vendor
- Thermo Fisher — *Watson LIMS 7.6 Configuration Reference*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

