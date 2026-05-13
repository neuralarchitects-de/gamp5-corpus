---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; enriched 2026-05-12 Wave 3 Chunk I (EU AI Act Annex I 2027 re-classification + T3 depth uplift)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed., 2022) Cat 5 conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "21 CFR Part 211 §§ .22, .68, .110, .192"
  - "EU GMP Annex 11"
  - "EU GMP Annex 1 (2022, in force 25 Aug 2023) — sterile manufacturing visual inspection"
  - "EU AI Act 2024/1689 Annex I high-risk classification — Arts. 8–21, 26, 43, 47, 48, 49, 72, 73, 99, 113"
  - "EU MDR 2017/745 (where CV system is SaMD component of a regulated device)"
  - "USP <790> Visible Particulates in Injections; USP <1790> Visual Inspection of Injections"
  - "USP <787> Subvisible Particulate Matter in Therapeutic Protein Injections; USP <788> Particulate Matter in Injections"
  - "USP <1> Injections and Implanted Drug Products"
  - "Ph. Eur. 2.9.20 Particulate Contamination — Visible Particles"
  - "FDA Inspection of Injectable Products for Visible Particulates (Draft Guidance, 2021)"
  - "FDA Good Machine Learning Practice for Medical Device Development — Guiding Principles (2021)"
  - "FDA AI/ML SaMD Action Plan (2021)"
  - "FDA Marketing Submission Recommendations for PCCP for Artificial Intelligence-Enabled Device Software Functions (August 2025)"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026)"
  - "ISPE GAMP 5 (2nd Edition, 2022); ISPE GAMP GPG AI/ML in GxP (2024)"
  - "ISPE GAMP RDI Good Practice Guide (Records and Data Integrity)"
  - "ISO 14971:2019 — Risk Management for Medical Devices"
  - "ISO/IEC 42001:2023 — AI Management System"
  - "ICH Q9(R1); ICH Q10"
  - "PDA Technical Report 79 — Particulate Matter Control in Difficult-to-Inspect Parenterals"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Custom Computer Vision Inspection System — Vials & Cosmetic Defects (in-house ML)

**Document Number:** TES-URS-CV-001
**Version:** 1.2
**Effective Date:** 2026-04-26 *(synthetic)*
**Site:** Tessera Bio Manufacturing GmbH, Sterile Fill-Finish Plant 1, Mannheim, Germany *(fictional)*
**System Owner:** Manufacturing Automation Lead
**Process Owner:** Head of Sterile Manufacturing
**Development Owner:** Quality IT — Custom Applications
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom Application (in-house ML model + integration software)
**Project Mode:** Custom-build project — site-developed system (GAMP 5 Category 5 — Bespoke; internal SDLC). System: Vials & Cosmetic Defects (in-house ML).
**EU AI Act 2024/1689 classification:** **Annex I high-risk AI system** — the CV inspection model is a safety component of the medicinal-product release decision for sterile parenterals; visual inspection per Annex 1 §8.123 and USP <790> / <1790> is a CGMP-binding control. High-risk-AI obligations under Arts. 8–21 apply. Conformity-assessment pathway inherited via Annex 1 + ICH Q10 + the site Pharmaceutical Quality System (no separate MDR conformity body where the CV system is purely a manufacturing control). **Compliance deadline: 2 August 2027.**
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .22, .68, .110, .192; EU GMP Annex 11; EU GMP Annex 1 (2022); EU AI Act 2024/1689 Arts. 8–21, 26, 43, 47, 48, 49, 72, 73, 99, 113; USP <1>, <787>, <788>, <790>, <1790>; Ph. Eur. 2.9.20; FDA *Inspection of Injectable Products for Visible Particulates* (Draft, 2021); FDA *Good Machine Learning Practice* (2021); FDA *AI/ML SaMD Action Plan* (2021); FDA *PCCP for AI-Enabled Device Software Functions* (August 2025); FDA *Computer Software Assurance* (February 2026); ISPE GAMP 5 (2nd ed., 2022); ISPE GAMP GPG *AI/ML in GxP* (2024); ISO 14971:2019; ISO/IEC 42001:2023; PDA TR 79.

> **Re-classification note (v1.2):** v1.1 implicitly treated the CV system as a generic Annex III high-risk AI with a 2 August 2026 deadline. v1.2 sharpens this per METHODOLOGY § 2A.14: visual inspection of sterile injectable products is a **safety component** of the medicinal-product manufacturing decision under Annex 1 + USP <790> / <1790>, so the CV system is **Annex I** with deadline **2 August 2027**. The site Pharmaceutical Quality System provides the conformity pathway (no separate MDR notified body unless the CV system is bundled into a regulated medical device).

> **Note (un-negotiable):** Per Annex 1 §8.123 and FDA expectations, 100% human visual inspection downstream is **retained** even with the CV system in service. The CV system **reduces** but does not eliminate human inspection workload. USP <790> compliance also requires a probabilistic-detection approach with statistical demonstration of capability; AVI capability is established via the ISO 17025-aligned validation protocol referenced below.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead — Automation) | _____________ | _____________ | _____ |
| Reviewer (Manufacturing Automation Lead) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (ML Engineering Lead) | _____________ | _____________ | _____ |
| Reviewer (Microbiology — visual-inspection SME) | _____________ | _____________ | _____ |
| Reviewer (Reg Affairs — AI/ML) | _____________ | _____________ | _____ |
| Reviewer (Conformity Assessment Coordinator) | _____________ | _____________ | _____ |
| Reviewer (QA — Annex 1 SME) | _____________ | _____________ | _____ |
| Approver (Head of Sterile Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |
| Approver (Qualified Person — batch release) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-13 | (synthetic) | URS-ML-03 verb fix (`must` → `shall`); minor citation currency fixes. |
| 1.2 | 2026-05-12 | (synthetic) | **Wave 3 Chunk I enrichment.** Tier T3 uplift (target 100–150 reqs). EU AI Act re-classified Annex I (2 Aug 2027) instead of generic high-risk. New §5 subsections: 5.1a Camera + lighting qualification; 5.2a Defect-class library + statistical class balance; 5.2b Ground-truth labelling protocol (dual-blind, adjudication); 5.2c Bias mitigation per Art. 10; 5.2d PCCP allowed-change envelope; 5.4a Annex IV technical-documentation pack; 5.4b Art. 12 logging ≥ 6 mo + Art. 18 retention ≥ 10 y; 5.4c Conformity + DoC + CE; 5.4d EU database registration where applicable; 5.4e PMM Art. 72; 5.4f Incident Art. 73 (15 d / 10 d / 2 d); 5.4g Deployer obligations Art. 26; 5.4h Robustness + cybersecurity Art. 15; 5.4i QMS Art. 17 + ISO/IEC 42001; 5.6a Annex 1 challenge-test cadence; 5.6b USP <790> / <1790> binding; 5.6c CGMP Part 211 binding; 5.10a Annex 1 §8.123 retained-human-inspection invariant; §9 risks expanded with 8 new domain-specific risks (false-accept on cracked vial, class imbalance, training-data drift on excipient changes, supply-chain attack on weights, Art. 99 penalty exposure). |

## Definitions

| Term | Definition |
|---|---|
| CV | Computer Vision |
| ML | Machine Learning |
| Model | The PyTorch / ONNX deep-learning model that classifies vials |
| AVI | Automated Visual Inspection |
| Pass / Reject | Two-class outcome of the model |
| Reject Class | Sub-classification of rejects (cracked, particulate, fill-level, stopper, label) |
| Conveyor PLC | Allen-Bradley ControlLogix that physically rejects flagged vials |
| MES | Werum PAS-X v3.2 |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| Annex 1 | EU GMP Annex 1 — Manufacture of Sterile Medicinal Products (2022) |
| Annex I (AI Act) | EU AI Act 2024/1689 Art. 6(1) high-risk classification — safety component of regulated product |
| Annex IV (AI Act) | EU AI Act 2024/1689 — technical documentation required of high-risk AI providers |
| PCCP | Predetermined Change Control Plan (FDA Aug 2025) |
| Knapp Test | USP <1790> reference performance test for inspector / system qualification |
| False Reject | True-good vial classified as Reject (cost/yield concern) |
| False Accept | True-defect vial classified as Pass (CRITICAL safety concern) |

## 1. Purpose

This URS defines requirements for the in-house Computer Vision (CV) Inspection System used to perform cosmetic-defect inspection of filled, sealed vials on the sterile fill-finish line at Tessera Bio Plant 1.

This is **GAMP Category 5** because the inspection model and the integration software are site-authored, and the system is an **EU AI Act 2024/1689 Annex I high-risk AI system** because the model acts as a safety component of the medicinal-product release decision via Annex 1 §8.123 visual-inspection requirements + USP <790> / <1790> / 21 CFR Part 211. The system makes a binary Pass / Reject classification per vial; the Reject decision is consumed by the conveyor PLC, which physically deflects the rejected vial. Additional 100% human visual inspection is retained downstream per Annex 1 §8.123.

## 2. Scope

**In scope:** the CV inspection station (Basler ace2 cameras, Effilux strobe lighting, NVIDIA Jetson AGX Orin edge inference compute on rails); the in-house ML pipeline (PyTorch training, ONNX deployment, Triton Inference Server registered on the Lyrae AI/ML Model Server — see LYR-URS-MLSRV-001); the integration software (Python, PostgreSQL, RabbitMQ); integrations with the conveyor PLC (deflector command), MES (recipe / batch), eQMS (deviation creation on excessive reject rate), the data-pipeline lakehouse (training-data + drift monitoring); SSO via Okta SAML 2.0; on-prem hosting in the plant DMZ. EU AI Act Annex I obligations (Arts. 9–21 + 26 + 43 + 47 + 48 + 49 + 72 + 73). USP <790> / <1790> compliance posture. Annex 1 visual-inspection capability evidence.

**Out of scope:** the conveyor itself and the deflector mechanism (separate equipment qualification); 100% human visual inspection retained downstream (separate SOP); training-data labelling tooling (separate URS); the underlying medicinal-product regulatory dossier (per product RA).

## 3. System Description and Intended Use

The system images each vial at four orientations on the inspection station, runs the model on the edge (sub-100 ms per vial at line speed of 400 vials/minute), and emits a Pass / Reject decision to the conveyor PLC. Rejected vials are deflected to a quarantine lane for downstream human inspection / disposition. All decisions, sub-classifications, and per-vial images are persisted for batch-record support and continual model evaluation.

**The system is a screening tool, not the sole release control.** Annex 1 §8.123 retention of additional 100% visual inspection downstream is a deliberate defence-in-depth measure; the URS-AN1-01 below makes this explicit.

The system is a CGMP-binding control under 21 CFR Part 211 (§ .22 quality unit responsibility, § .68 automatic equipment validation, § .110 in-process samples + tests, § .192 production records review). Annex 1 §8.123 (revised 2022) requires that automated visual inspection be **equal to or better than** manual inspection and the validation evidence is part of the manufacturing licence file.

## 4. User Roles

| Role | Permissions |
|---|---|
| Operator | Start / stop the inspection station; acknowledge alarms; cannot retrain or deploy. |
| Senior Operator / Line Lead | All Operator + escalate alarms; second-person verification of model-deployment events. |
| ML Engineer | Train models; submit candidates for evaluation; cannot deploy to production alone. |
| Validation / QA ML Reviewer | Evaluate candidate models against the validation set + risk acceptance criteria; co-sign deployment. |
| ML Deployment Approver (Head of Sterile Mfg + Head of QA) | Joint approval to deploy a new model version. |
| Conveyor Engineer | Maintain conveyor PLC interface; cannot retrain models. |
| System Administrator | OS / patch / AD groups; cannot retrain or approve deployment. |
| Conformity Assessment Coordinator | Maintain Art. 11 + Annex IV pack; liaise with notified body where applicable. |
| Human Oversight Operator (per EU AI Act Art. 14) | Real-time monitoring of model rejection rate, drift indicators, false-accept estimates; authority to halt the model. |
| Qualified Person | Batch release; reviews AVI capability + human-inspection evidence per Annex 1. |
| Auditor | Read-only across decisions, model registry, audit trails. |

Separation of duties: ML Engineer ≠ ML Reviewer ≠ Approver of the same model; Operator ≠ Verifier on the same critical event. Conformity Assessment Coordinator ≠ ML Engineer.

## 5. User Requirements

### 5.1 Hardware / Edge Compute

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HW-01 | H | R1 | Inspection station includes at minimum 4× Basler ace2 cameras + Effilux strobe lighting + NVIDIA Jetson AGX Orin compute, in an industrial enclosure rated for the cleanroom grade. |
| URS-HW-02 | H | R1 | Edge compute on UPS for ≥ 30 minutes; inspection station defaults to **Reject all** on power loss / network loss (fail-safe). |
| URS-HW-03 | H | R1 | Inspection station on a process-control VLAN segregated from office traffic. |
| URS-HW-04 | M | R2 | Camera calibration verified daily (whitebox / pattern target) before production start. |
| URS-HW-05 | H | R1 | NVIDIA Jetson firmware + driver versions shall be pinned under change control; driver updates require revalidation against the locked validation set. |

### 5.1a Camera + Lighting Qualification

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-OPT-01 | H | R1 | Camera + lighting setup shall pass an IQ / OQ qualifying contrast, focus, illumination uniformity (≥ 90% of field within ±10% of centre intensity), and absence of glare in the inspection cone. |
| URS-OPT-02 | H | R1 | Per USP <1790> recommendations, container clear-glass illumination shall be inspected at 2,000–3,750 lux backlight equivalent; per-product recipe shall specify the configured intensity. |
| URS-OPT-03 | H | R1 | Lighting + camera baseline shall be re-qualified after any hardware change; baseline-image hash shall match the recipe baseline at production start. |
| URS-OPT-04 | M | R2 | Daily start-up check shall include a Knapp-test reference vial pass to confirm sensitivity has not regressed. |

### 5.2 Model Lifecycle (Cat 5 SDLC + ML-specific)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ML-01 | H | R1 | Each candidate model shall have a documented Model Card: training data lineage, training script + version, hyperparameters, training metrics, validation-set performance (sensitivity, specificity, false-reject rate, false-accept rate, per defect class), known limitations. |
| URS-ML-02 | H | R1 | The validation set shall be locked, version-controlled, and not used for training; per-class size shall meet the documented statistical-power plan (Knapp-test compatible). |
| URS-ML-03 | H | R1 | A new model shall not be deployed unless it Pareto-improves on the production model: false-accept rate shall not increase; false-reject rate shall not increase by more than the configured tolerance (default 0.5 percentage points). |
| URS-ML-04 | H | R1 | Deployment requires joint signature of ML Reviewer and Head of Sterile Manufacturing and Head of QA; for any deployment outside the PCCP envelope (URS-PCCP-01..04) an additional Reg-Affairs (AI/ML) signature is required + an Art. 43(4) substantial-modification assessment. |
| URS-ML-05 | H | R1 | Each deployed model shall be cryptographically signed (cosign) and the deployment Triton Inference Server shall verify the signature before loading. |
| URS-ML-06 | H | R1 | Drift monitoring: continuous comparison of production class distribution and image-statistics to the validation-set baseline; configurable thresholds raise an alarm and may trigger a re-evaluation. Three axes: data drift (image stats), concept drift (defect-rate vs benchmark), prediction drift (output distribution). |
| URS-ML-07 | H | R1 | Each model version shall be registered in the Lyrae AI/ML Model Server (LYR-URS-MLSRV-001) with full Annex IV linkage so the corpus's enterprise inference governance applies. |
| URS-ML-08 | H | R1 | Models shall be retired (state RETIRED) when superseded or end-of-life; per Art. 18, all training + validation + deployment + post-market records shall be retained ≥ 10 years after market placement. |

### 5.2a Defect-Class Library + Statistical Class Balance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEF-01 | H | R1 | The defect-class library shall include at minimum: visible particulate (USP <790>), cracks (glass), chipped neck / lip, fill-volume out-of-spec (under-fill / over-fill), stopper-seat defect (mis-set / cocked / lifted), labelling defect (off-axis / missing / illegible / wrong product). |
| URS-DEF-02 | H | R1 | Per Art. 10 + USP <790> probabilistic detection, the training + validation set shall be **statistically balanced across defect classes**; minority classes shall meet the documented per-class statistical-power floor. |
| URS-DEF-03 | H | R1 | Class definitions shall be canonical (`defect_classes_v{n}.yaml` in git); class additions trigger model-lifecycle re-run. |
| URS-DEF-04 | M | R2 | The defect library shall be reviewed annually against published industry advisories + recent regulator findings. |

### 5.2b Ground-Truth Labelling Protocol (Dual-Blind + Adjudication)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LBL-01 | H | R1 | Per Art. 10 + USP <1790>, labelling shall be **dual-blind**: two independent qualified inspectors label each candidate vial without seeing the other's label; disagreements go to a third-inspector adjudication. |
| URS-LBL-02 | H | R1 | Inspector qualification shall follow USP <1790> recommendations: vision exam + Knapp-test pass + per-defect-class training. |
| URS-LBL-03 | H | R1 | Inter-rater reliability (Cohen's κ) shall be measured per labelling campaign; campaigns with κ < 0.7 shall trigger labeller re-training before label-set acceptance. |
| URS-LBL-04 | H | R1 | Labelled datasets shall be versioned + signed; downstream training runs shall pin to dataset version + SHA-256. |
| URS-LBL-05 | M | R2 | Adjudication outcomes shall be retained for inter-rater calibration analytics. |

### 5.2c Bias Mitigation per Art. 10

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BIA-01 | H | R1 | Training + validation + test datasets shall be **relevant, representative, statistically sound** per Art. 10; representativeness shall cover product types, container types (glass / cartridge), fill volumes, lighting variability, and stopper colour-variants in scope. |
| URS-BIA-02 | H | R1 | Bias evaluation per defect-class + per container-type shall be documented; performance gaps > documented threshold shall trigger targeted data-augmentation. |
| URS-BIA-03 | M | R2 | Bias-evidence pack shall be linked from the Annex IV pack and reviewed in periodic review. |

### 5.2d PCCP Allowed-Change Envelope

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PCCP-01 | H | R1 | The PCCP per model shall enumerate the modifications-only protocol (MoP), performance-and-clinical-evaluation method (PCEM), and impact assessment (IA) per FDA August 2025 PCCP guidance for AI-Enabled Device Software Functions. |
| URS-PCCP-02 | H | R1 | A predicate engine shall verify each model update against the PCCP envelope before allowing promotion; non-conformant updates shall block automatically. |
| URS-PCCP-03 | H | R1 | PCCP deviations require Art. 43(4) substantial-modification assessment + renewed conformity workflow. |
| URS-PCCP-04 | M | R2 | PCCP envelope shall be reviewed annually; envelope amendments require Reg-Affairs + VP-QA approval. |

### 5.3 Inference and Decision

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INF-01 | H | R1 | Per-vial inference latency ≤ 100 ms at the 95th percentile under nominal line speed (400 vials / minute). |
| URS-INF-02 | H | R1 | Each decision shall be recorded with: vial ID (assigned by the conveyor at entry), per-orientation image hashes, model version, decision (Pass / Reject), reject sub-class (if any), confidence score, edge-compute hostname, timestamp. |
| URS-INF-03 | H | R1 | The default decision on inference timeout, model load failure, or any internal error shall be **Reject** (fail-safe). |
| URS-INF-04 | H | R1 | A configurable confidence-threshold band may flag vials for forced human review; the threshold and routing are part of the configuration baseline. |
| URS-INF-05 | H | R1 | Inference outputs shall be deterministic given identical input + model + driver versions; deterministic-reproducibility OQ shall pin random seeds. |

### 5.4 Image / Data Retention

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-IMG-01 | H | R1 | All per-vial images shall be retained for at least 12 months for model evaluation; reject images for ≥ 7 years for batch-record support (≥ 10 y for Annex IV records per Art. 18). |
| URS-IMG-02 | H | R1 | Image storage shall be write-once (object storage with object lock); deletions outside the retention policy require dual signature. |
| URS-IMG-03 | M | R2 | A representative sample of pass images shall be reviewed monthly to detect labelling drift (false-pass spot check). |

### 5.4a Art. 11 + Annex IV Technical Documentation Pack

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TD-01 | H | R1 | The Annex IV pack shall include: general description; design + development description (SDLC + model architecture + training pipeline); training / validation / test data per Art. 10 (Knapp-test compatibility, class balance, bias evaluation); monitoring + functioning + control (drift + alarms + fail-safe); declared performance metrics (sensitivity / specificity / FRR / FAR per class) + evaluation method; Art. 9 risk-management (linked to ISO 14971:2019); lifecycle change-management + PCCP; compliance-with-harmonised-standards (Annex 1 + USP <790> / <1790>). |
| URS-TD-02 | H | R1 | Pack maintained over the deployed lifetime; lifecycle changes trigger pack-revision under change control. |
| URS-TD-03 | M | R2 | Pack exportable within 1 business day for notified-body / authority inspection. |

### 5.4b Art. 12 Logging + Art. 18 Retention

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LOG-01 | H | R1 | Per Art. 12, automatic logs shall be retained ≥ 6 months on hot storage; logs traceable end-to-end (actor, vial-id, model-id + version, timestamp ISO 8601, integrity hash). |
| URS-LOG-02 | H | R1 | Per Art. 18, Annex IV pack + DoC + conformity records + training records + PMM records shall be retained **≥ 10 years after the model is placed on the market or put into service**. |

### 5.4c Conformity + EU DoC + CE (Arts. 43, 47, 48)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CONF-01 | H | R1 | Conformity assessment per Art. 43 shall be performed before the CV system enters production use; pathway chosen (internal control Annex VI by default, since the CV system is a CGMP control inheriting the medicinal-product QMS; notified-body Annex VII only where the CV system is bundled into an MDR class IIa+ device). |
| URS-CONF-02 | H | R1 | An EU Declaration of Conformity per Art. 47 shall be on file; signed by Reg-Affairs (AI/ML). |
| URS-CONF-03 | H | R1 | CE-marking surface per Art. 48 shall be applied logically + retrievable via the operator UI. |
| URS-CONF-04 | M | R2 | Substantial modifications per Art. 43(4) shall trigger renewed conformity assessment. |

### 5.4d EU Database Registration

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REG-01 | M | R2 | Annex I CV system inherits the medicinal-product manufacturing-licence registration; no separate EU AI database registration is required unless the system is bundled into a regulated medical device (in which case EUDAMED registration applies). |

### 5.4e Post-Market Monitoring (Art. 72)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PMM-01 | H | R1 | PMM shall collect per-batch FRR + FAR estimates, downstream human-inspection findings (corroboration or contradiction of CV decisions), drift detections, and false-pass spot-check outcomes. |
| URS-PMM-02 | M | R2 | Quarterly PMM report signed by Manufacturing Automation Lead + Head of Sterile Mfg + Head of QA. |

### 5.4f Incident Reporting (Art. 73)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INC-01 | H | R1 | Serious incidents (Art. 3(49)) — e.g., a confirmed false-accept resulting in a particulate-contaminated parenteral reaching the market — shall be reported to the competent authority within **15 days standard / 10 days if death / 2 days for widespread fundamental-rights infringement**. |
| URS-INC-02 | H | R1 | Authority routing: BfArM (DE Mannheim site default), with cross-reference to Annex 1 regulator-notification channels via the QP and the site Pharmacovigilance / Manufacturing Authorisation Holder. |
| URS-INC-03 | M | R2 | Incident record schema: batch-id, vial-id (if traceable), event narrative, root-cause status, corrective action, regulator notification status. |

### 5.4g Deployer Obligations (Art. 26)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEP-01 | H | R1 | The site Manufacturing Operations function, as deployer per Art. 26, shall: use the CV system per the IFU, ensure training-data + production-data input remain representative, assign trained human oversight via the Human Oversight Operator role (§ 4), monitor + suspend on identified risk, keep logs ≥ 6 months on site, inform workers' representatives (works council) of the AI use in production workflow. |

### 5.4h Robustness + Cybersecurity (Art. 15)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ROB-01 | H | R1 | The model shall be evaluated for robustness against documented perturbation envelopes (lighting variation ±20%, camera-position offset ±2 mm, exposure variation ±10%); declared performance shall hold within envelope. |
| URS-ROB-02 | H | R1 | Training-data integrity verified via SHA-256 at registration; supply-chain attack defence — pre-trained weight ingest with cosign verification + SBOM. |
| URS-ROB-03 | H | R1 | Edge-device tamper detection: enclosure intrusion sensors, secure boot, signed firmware. |
| URS-ROB-04 | H | R1 | Network confidentiality + integrity — TLS 1.3 inter-component; mTLS to Triton + Lyrae model server. |

### 5.4i QMS Art. 17 + ISO/IEC 42001

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-QMS-01 | H | R1 | The CV-system QMS shall conform to EU AI Act Art. 17 and align with ISO/IEC 42001:2023; integration with site PQS per ICH Q10. |
| URS-QMS-02 | H | R1 | Annual QMS effectiveness review by VP QA + Head of Sterile Mfg + Reg-Affairs. |

### 5.5 Audit Trail

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Audit trail capturing model deployments, configuration changes, alarm acknowledgements, signatures, manual decision overrides, Art. 73 incident triggers. |
| URS-AUD-02 | H | R1 | Audit trail append-only; no application or admin update / delete. |
| URS-AUD-03 | H | R1 | Audit-trail review by Quality Reviewer per batch and by QA Compliance quarterly. |
| URS-AUD-04 | H | R1 | Retention ≥ 25 years for batch-relevant entries (≥ 10 y for Art. 18 Annex IV-related). |
| URS-AUD-05 | M | R2 | Audit-trail review evidence retained as part of the batch record (21 CFR § 211.192 / Annex 1). |

### 5.6 21 CFR Part 11 / Annex 11 / Annex 1

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | E-signatures meet § 11.50 (printed name, date/time, meaning). |
| URS-PART11-02 | H | R1 | Each signature unique; no reuse / reassignment (§ 11.100). |
| URS-PART11-03 | H | R1 | Signatures cryptographically bound to the signed record (§ 11.70). |
| URS-PART11-04 | H | R1 | Separation of duties enforced (§ 11.10(g)). |
| URS-PART11-05 | H | R1 | Re-authentication required at the moment of signing (§ 11.200). |
| URS-PART11-06 | H | R1 | Per § 11.10(a), procedures + controls protecting record validity shall be enforced. |
| URS-PART11-07 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via Okta + MFA. |
| URS-PART11-08 | H | R1 | Per § 11.10(e), operational audit trail captures user / action / date / time (see § 5.5). |
| URS-PART11-09 | H | R1 | Per § 11.10(b), the system shall be capable of producing accurate + complete copies (electronic + human-readable) for inspection. |
| URS-PART11-10 | H | R1 | Per § 11.10(c), records shall be protected for the retention period (≥ 25 y batch-relevant; ≥ 10 y Annex IV). |
| URS-PART11-11 | H | R1 | Per § 11.300, password / credential controls per site InfoSec policy. |
| URS-AN1-01 | H | R1 | The CV system **does not replace** Annex 1 §8.123 visual inspection; downstream 100% human visual inspection of all vials remains in force. The CV system reduces but does not eliminate the human inspection workload. |

### 5.6a Annex 1 Challenge-Test Cadence

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CHAL-01 | H | R1 | Per Annex 1 §8.123 + USP <1790>, **challenge tests shall be performed at start of batch, on a representative basis throughout the batch, and at batch end**; challenge sets shall mimic real product with known defects (Knapp-test methodology). |
| URS-CHAL-02 | H | R1 | Challenge-set sets shall be controlled to prevent mix-up with production product (visibly marked, separately stored, reconciled at end of use). |
| URS-CHAL-03 | H | R1 | A challenge-test failure (CV fails to reject a known defect) shall trigger immediate batch hold + investigation; resumption shall require Head of QA + QP sign-off. |
| URS-CHAL-04 | M | R2 | Challenge-test outcomes shall be trended; trend deviations shall feed PMM (URS-PMM-01). |

### 5.6b USP <790> / <1790> Binding

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-USP-01 | H | R1 | The system shall demonstrate compliance with USP <790> probabilistic-detection criteria for visible particulates: documented inspector-equivalent sensitivity, statistical demonstration of capability against the reference particle set. |
| URS-USP-02 | H | R1 | Per USP <1790>, system qualification shall include Knapp-test reference vials; CV decision shall correlate with the Knapp-test reference assignment per the documented acceptance criteria. |
| URS-USP-03 | H | R1 | Per USP <790> + Ph. Eur. 2.9.20, subvisible particulate handling — out of scope for this CV system; the system shall not be relied upon for subvisible (USP <787> / <788>) inspection. |

### 5.6c CGMP Part 211 Binding

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-211-01 | H | R1 | Per 21 CFR § 211.22, the Quality Unit shall have responsibility + authority for the CV system; the QA Compliance organisation shall sign off on validation evidence + change control. |
| URS-211-02 | H | R1 | Per 21 CFR § 211.68, automatic equipment used in manufacture shall be validated; routine calibration + checks shall be performed + documented. |
| URS-211-03 | H | R1 | Per 21 CFR § 211.110, in-process control + sampling shall include the CV system's reject-rate trending. |
| URS-211-04 | H | R1 | Per 21 CFR § 211.192, batch records shall include the CV system's reject summary; the QP / QA reviewer shall review per batch. |

### 5.7 Custom-Software / ML SDLC

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEV-01 | H | R1 | Application code (training pipeline, integration service) developed under documented Cat-5 SDLC; gates: requirements → design → code → unit / integration tests → security scan → user acceptance → release. |
| URS-DEV-02 | H | R1 | All code in version control with signed commits; `main` requires peer review and passing CI. |
| URS-DEV-03 | H | R1 | Unit-test coverage ≥ 90% on integration service; per-component coverage of training pipeline ≥ 80%. |
| URS-DEV-04 | H | R1 | Static analysis + dependency scanning on every CI build; criticals block. |
| URS-DEV-05 | H | R1 | ML-specific quality gates per URS-ML-01..08. |
| URS-DEV-06 | H | R1 | Open-source dependencies (PyTorch, ONNX Runtime, Triton, FastAPI, etc.) assessed annually for license, vulnerability, and maintainership. |
| URS-DEV-07 | H | R1 | Releases shall be cosign-signed; release manifest shall enumerate model + integration-service + config versions. |

### 5.8 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-PLC-01 | H | R1 | Decisions emitted to the conveyor PLC over EtherNet/IP with mutual authentication; loss of communication triggers the fail-safe Reject mode. |
| URS-INT-MES-01 | H | R1 | Recipe / batch context received from MES (vial type, expected fill-volume range); per-batch reject metrics returned. |
| URS-INT-EQMS-01 | H | R1 | Reject-rate excursions beyond per-product threshold auto-create deviations in MasterControl with idempotency. |
| URS-INT-AD-01 | H | R1 | Authentication via Okta SAML 2.0 + MFA. |
| URS-INT-LYR-01 | H | R1 | Models shall be deployed via Lyrae AI/ML Model Server (LYR-URS-MLSRV-001) so platform-level EU AI Act controls (logging, drift, audit, conformity, PMM, incident) apply uniformly. |
| URS-INT-LMS-01 | M | R2 | Operator + Inspector training records retrieved from site LMS; non-current users blocked from privileged actions. |

### 5.9 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | Records Attributable to a named user (where relevant) and to a named model version (always). |
| URS-DI-02 | H | R1 | Records Legible — exportable as CSV / PDF; images retrievable by hash. |
| URS-DI-03 | H | R1 | Records Contemporaneous — synchronised PTP timestamps from the inspection station. |
| URS-DI-04 | H | R1 | Original captured images preserved unaltered (write-once object lock). |
| URS-DI-05 | H | R1 | Decision logic (model + post-processing) Accurate — verified per OQ. |
| URS-DI-06 | M | R2 | Complete / Consistent / Enduring (≥ 25-yr retention) / Available (≤ 4 hours during inspection). |
| URS-DI-07 | H | R1 | Per Art. 10, training-data governance (URS-LBL-01..05 + URS-BIA-01..03 + URS-DEF-01..04) is the data-integrity backbone. |

### 5.10 Performance / Availability / Backup

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | H | R1 | Sustained ≥ 400 vials / minute throughput at the 95th-percentile latency in URS-INF-01 over an 8-hour shift. |
| URS-AV-01 | H | R1 | System availability during fill operations ≥ 99.5%; planned-maintenance windows excluded. |
| URS-BAK-01 | H | R1 | Decision database + image object store backed up nightly with PITR; image store replicated to a second site. |
| URS-BAK-02 | H | R1 | Quarterly restore test, witnessed. |
| URS-BAK-03 | H | R1 | Annual cold-archive retrieval drill for Annex IV Art. 18 records; documented retrieval time ≤ 24 h. |

### 5.10a Retained-Human-Inspection Invariant

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HUM-01 | H | R1 | Downstream 100% human visual inspection of all vials shall remain in force per Annex 1 §8.123; the CV system supplements but does not replace this control. |
| URS-HUM-02 | H | R1 | Inspector qualification per USP <1790> shall be maintained; inspector pool size + training cadence shall ensure capability is preserved. |
| URS-HUM-03 | M | R2 | The CV system's impact on inspector workload shall be monitored; reductions ≥ 30% shall require revalidation of inspector visual-acuity calibration. |

### 5.11 Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | All authentication via Okta + MFA; no local accounts other than break-glass admin. |
| URS-SEC-02 | H | R1 | All client-server traffic via TLS 1.3; mTLS for the inference service ↔ Triton. |
| URS-SEC-03 | H | R1 | Secrets retrieved at start-up from HashiCorp Vault; never on disk in clear or in environment variables. |
| URS-SEC-04 | M | R2 | Vulnerability scans monthly; criticals remediated within 30 days. |
| URS-SEC-05 | H | R1 | Edge-device tamper protection per URS-ROB-03; tamper events trigger fail-safe Reject + alarm. |

### 5.12 Training / Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Production access requires recorded role-specific training (LMS), including line-procedure familiarisation and the manual-fail-safe handling. |
| URS-TRN-02 | M | R2 | Per Art. 4, AI literacy training shall be assigned to all roles with AI-output exposure. |
| URS-PR-01 | H | R1 | Annual periodic review covering: configuration drift, model registry + drift trends, false-accept / false-reject metrics by batch, deviations, training-data refresh, fitness for use, PCCP adherence, QMS effectiveness; signed by Manufacturing Automation Lead, Head of Sterile Mfg, Head of QA, Reg-Affairs (AI/ML). |
| URS-PR-02 | H | R1 | Quarterly model-evaluation review, even if no new model is deployed: drift trends + false-pass spot check + reject-rate trends + Knapp-test reference results. |
| URS-PR-03 | M | R2 | Annual EU AI Act classification reassessment; reclassification change-controlled. |

### 5.13 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is Kerberos for interactive operator logon and a gMSA service account for the inference / pipeline services; conditional-access policy `AI-Platform Conditional Access (FIDO2 + device-compliance) for operators; gMSA-bound service identity for the inference workload` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the inspection-event store plus MinIO/S3 object-replica for image evidence and Annex IV artefacts; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 10 y after market placement (Art. 18) + ≥ 5 y past last fill-finish lot per the consuming-record schedule. |

## 6. Acceptance Criteria

System enters validated GMP use when:

1. FS, DS, CS, RA, IQ, OQ, PQ approved and executed;
2. PQ includes representative ≥ 8-hour production runs at line speed, drift-detection scenarios, fail-safe triggers (network loss, inference timeout), a model-deployment under the full Cat-5 + ML SDLC, **Annex 1 challenge-test cadence** at start / mid / end of batch, and an **Art. 73 incident-reporting drill**;
3. Art. 11 + Annex IV Technical Documentation pack on file (per URS-TD-01..03);
4. Conformity assessment per Art. 43 performed; EU DoC per Art. 47 signed; CE-marking surface (URS-CONF-03) verified;
5. USP <790> probabilistic-detection capability demonstrated; USP <1790> Knapp-test reference performance documented;
6. VSR approved by Manufacturing Automation Lead, Head of Sterile Mfg, Head of QA, Reg-Affairs (AI/ML), QP;
7. RTM maps every URS to ≥ 1 approved test case.

## 7. Constraints

- Model deployment requires joint signature.
- Annex 1 §8.123 downstream human inspection is non-negotiable (URS-HUM-01..03).
- Vendor (NVIDIA / camera vendors) firmware patches under change control.
- EU AI Act Annex I high-risk obligations apply from **2 August 2027**.
- AI literacy obligation (Art. 4) applies from 2 February 2025.

## 8. Assumptions

- MES, eQMS, Okta, conveyor PLC, Lyrae AI/ML Model Server are validated.
- Image-storage object lock is enforced.
- BfArM is the EU AI Act market-surveillance authority for the Mannheim site.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 — Electronic Records; Electronic Signatures (§§ .10, .30, .50, .70, .100, .200, .300).
- 21 CFR Part 211 — CGMP for Finished Pharmaceuticals (§§ .22, .68, .110, .192).
- FDA *Inspection of Injectable Products for Visible Particulates* (Draft Guidance, 2021).
- FDA *Good Machine Learning Practice for Medical Device Development — Guiding Principles* (2021).
- FDA *AI/ML-Based Software as a Medical Device Action Plan* (2021).
- FDA *Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions* (August 2025).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026).

### EU — EMA / Commission
- EU GMP Annex 11 — Computerised Systems.
- EU GMP Annex 1 (2022) — Manufacture of Sterile Medicinal Products (§ 8.123 automated visual inspection).
- EU AI Act 2024/1689 — **Annex I high-risk** classification (Art. 6(1)); Arts. 8–21, 26, 43, 47, 48, 49, 72, 73, 99, 113. **Deadline 2 August 2027.**
- EU MDR Reg. 2017/745 (where the CV system is bundled into a regulated device).

### DACH-specific
- BfArM (DE) — EU AI Act market-surveillance authority for DE.
- Swissmedic (CH); AGES (AT).

### Compendial — USP / Ph. Eur.
- USP <1> Injections and Implanted Drug Products.
- USP <787> Subvisible Particulate Matter in Therapeutic Protein Injections.
- USP <788> Particulate Matter in Injections.
- USP <790> Visible Particulates in Injections.
- USP <1790> Visual Inspection of Injections.
- Ph. Eur. 2.9.20 — Particulate Contamination: Visible Particles.

### International — ICH / ISPE / ISO / PDA
- ICH Q9(R1) — Quality Risk Management; ICH Q10 — Pharmaceutical Quality System.
- ISPE GAMP 5 (2nd Edition, 2022); ISPE GAMP GPG *AI/ML in GxP* (2024); ISPE GAMP RDI.
- ISO 14971:2019 — Risk Management for Medical Devices.
- ISO/IEC 42001:2023 — Artificial Intelligence Management System.
- PDA Technical Report 79 — Particulate Matter Control in Difficult-to-Inspect Parenterals.

### Internal
- Tessera SDLC Standard for Custom GxP Applications and ML Pipelines.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
