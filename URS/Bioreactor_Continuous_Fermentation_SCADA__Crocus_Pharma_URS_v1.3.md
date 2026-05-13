---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; expanded 2026-05-12 (T3 enrichment — bioprocess + PAT + ATMP + ISA-88/95)"
seed_corpus_basis:
  - "josephiuliucci/SDLC-PB SDLC_CSA_HiveMQ + URS_SCADA (industrial CSA + GAMP Cat 5)"
  - "GAMP 5 (2nd ed.) Cat 5 conventions for custom control software"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11; EU GMP Annex 1 (2022 revision); EU GMP Annex 2 (Biological medicinal products)"
  - "ICH Q9(R1); ICH Q10; ICH Q11; ICH Q13 (Continuous Manufacturing of Drug Substances and Drug Products); ICH Q5A/Q5B"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026)"
  - "FDA Quality Considerations for Continuous Manufacturing (2023); FDA PAT Guidance (2004)"
  - "ATMP Guidelines (EU + FDA cell/gene therapy considerations)"
  - "USP <1043> Ancillary Materials for Cell and Tissue Therapies"
  - "ISPE Baseline Guide Biopharmaceutical Manufacturing Facilities; ISPE GAMP GPG Process Analytical Technology"
  - "ISA-88 (Batch Control); ISA-95 (Enterprise-Control System Integration); ISA-101 (HMI); ISA-18.2 (Alarm Management)"
  - "PIC/S PI 041"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# User Requirements Specification (URS)

## Bioreactor Continuous Fermentation SCADA — Site-Authored Cell-Culture Orchestrator (Ignition 8.3 + DCS + Custom Python)

**Document Number:** CRC-URS-BIOSCADA-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Crocus Pharma (Suzhou) Co., Ltd, Biologics Plant 1, Suzhou, Jiangsu, China *(fictional)*
**System Owner:** Bioprocess Automation Lead | **Process Owner:** Head of Biologics Manufacturing
**Development Owner:** Quality IT — Bioprocess Custom Apps
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom Application (Ignition 8.3 platform = Cat 4; site-authored Python Orchestrator + APC + SoftSensor + decision-rule engine = Cat 5)
**Project Mode:** Custom-build project — site-developed system (GAMP 5 Category 5 — Bespoke; internal SDLC). System: Site-Authored Cell-Culture Orchestrator (Ignition 8.3 + DCS + Custom Python).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11; EU GMP Annex 1 (2022 revision); EU GMP Annex 2 (Biological medicinal products); ICH Q9(R1); ICH Q10; ICH Q11; ICH Q13 (continuous bioprocessing); USP <1043>; FDA CSA (Feb 2026); FDA Quality Considerations for Continuous Manufacturing (2023); FDA PAT Guidance (2004); ISA-88; ISA-95; ISA-18.2; ISA-101; PIC/S PI 041.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead — Biologics Automation) | _____________ | _____________ | _____ |
| Reviewer (Bioprocess Automation Lead) | _____________ | _____________ | _____ |
| Reviewer (Cell-Culture Process Sciences Lead) | _____________ | _____________ | _____ |
| Reviewer (PAT Chemometrician) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Functional Safety Engineer) | _____________ | _____________ | _____ |
| Approver (Head of Biologics Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Minor: PAT-loss safe-state clarified. |
| 1.2 | 2026-05-12 | (synthetic) | Tier-T3 enrichment (100-150 reqs): §5 broken into 14 subsections (recipe phases, feed/perfusion control, PAT/chemometrics, single-use/stainless config mgmt, ATMP cell-therapy, ISA-88 batch state machine, ISA-95 enterprise integration, alarm management per ISA-18.2); expanded References to current-effective citations per METHODOLOGY § 2A.1; risk table expanded to 14 rows. Authored to **Tier T3** (production SCADA orchestrating continuous bioprocess; 100-req target; spans recipe-phase orchestration + PAT-driven control + ATMP-class data integrity + ISA-88/95 integration). |

## Definitions

| Term | Definition |
|---|---|
| Continuous Fermentation | Perfusion / continuous bioreactor cell culture (vs. fed-batch); ICH Q13-aligned |
| DCS | Distributed Control System (Emerson DeltaV v15.3 — Cat 4 platform) |
| SCADA | Supervisory Control and Data Acquisition — Ignition 8.3 (Cat 4 platform) |
| Cell-Culture Orchestrator | Site-authored Python service (~6,500 LOC) supervising the bioreactor train and PAT-driven feed control (Cat 5) |
| PAT | Process Analytical Technology — Raman / capacitance / off-gas / on-line VCD per FDA PAT Guidance (2004) |
| VCD | Viable Cell Density (capacitance-derived, on-line) |
| Perfusion | Continuous medium exchange across the bioreactor (cell-retention via ATF / TFF / spin-filter) |
| CCS | Cell-Culture Strategy — campaign-specific recipe + control-rule set |
| MAM | Multi-Attribute Method (off-line CQA reference) |
| MES | Werum PAS-X v3.2 |
| LIMS | Laboratory Information Management System (Watson LIMS — separate URS) |
| CQA | Critical Quality Attribute (per ICH Q8/Q11) |
| CPP | Critical Process Parameter (per ICH Q8/Q11) |
| OUR / CER | Oxygen Uptake Rate / CO2 Evolution Rate (off-gas-derived) |
| ATF | Alternating Tangential Flow (cell-retention device) |
| ATMP | Advanced Therapy Medicinal Product (cell + gene therapy class) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| ISA-88 | International Society of Automation batch-control standard (recipe + state-model) |
| ISA-95 | Enterprise / control-system integration standard |
| ISA-101 | HMI design standard |
| ISA-18.2 | Alarm-management standard |

## 1. Purpose

Define requirements for the bioreactor SCADA controlling continuous (perfusion) fermentation of a recombinant biologic (mAb / Fc-fusion class — campaign-defined) at Crocus Pharma Plant 1. The site-authored Cell-Culture Orchestrator implements PAT-driven feed control on top of the DCS / SCADA stack and is **GAMP Category 5**. ICH Q13 (continuous bioprocessing) and EU GMP Annex 2 (biological medicinal products) are the principal regulatory framings; USP <1043> applies for ancillary-material qualification across the cell-culture process.

## 2. Scope

**In scope:** Inductive Automation Ignition 8.3 SCADA layer (gateway cluster + redundant standby), Emerson DeltaV v15.3 DCS (Cat 4) and DeltaV SIS (SIL 2 safety partition), the Cell-Culture Orchestrator (Python 3.12, ~6,500 LOC), PAT instruments (Kaiser RamanRxn4 + Hamilton Incyte capacitance + Thermo Prima Pro mass-spec off-gas + Sartorius BioPAT Spectro on-line VCD — each separately qualified), Sartorius Biostat STR-200 single-use stainless hybrid reactors (or Cytiva XDR-200 single-use as alternative config), Repligen ATF 6 perfusion / cell-retention skids, Watson-Marlow Quantum feed-pump skids, integration with Werum PAS-X v3.2 (recipe / batch report), MasterControl eQMS (deviation), Aspen IP.21 historian (long-term archive), Active Directory `crocus.local` authentication. The Orchestrator runs on the site OpenShift 4.14 cluster (3 replicas + DR replica).

**Out of scope:** Physical bioreactor hardware (separate equipment qualification under `EQ-BIO-CRC-001..006`); upstream cell banking + thaw + seed train (separate URS); downstream chromatography + UF/DF + bulk fill (separate URS); raw-material qualification (USP <1043> tracking in Watson LIMS); off-line CQA / multi-attribute method (separate workflow); BMS for utility status (separate URS, consumed as inputs).

## 3. System Description and Intended Use

The Orchestrator continuously supervises the bioreactor train across the full perfusion lifecycle: monitors PAT signals (Raman for glucose / lactate / glutamine / IgG titer; capacitance for VCD; off-gas for OUR / CER; on-line VCD as redundant signal), computes the feed / perfusion control actions per the validated control strategy (multivariate decision rules + soft-sensor outputs), commands the DCS through OPC UA over TLS with mutual authentication, manages perfusion exchange-rate to maintain steady-state VCD and titer, executes the ISA-88 batch state model (inoculation → exponential growth → steady-state perfusion → harvest → CIP/SIP), produces continuous-process executed-batch reports at harvest and at campaign end, and surfaces ALCOA+ data to the historian and to PAS-X. ICH Q13 continuous bioprocessing principles, EU GMP Annex 2 biological-manufacturing controls, USP <1043> ancillary-material data flow, and ISA-88/95/101/18.2 best-practice standards together form the basis.

**GAMP categorisation:** Ignition 8.3 platform + DeltaV v15.3 DCS = Cat 4; the site-authored Orchestrator + APC modules + SoftSensor modules + decision-rule engine + PAT-loss safe-state logic = Cat 5. The combined system is validated as **Cat 5**.

**ATMP context:** Although the principal use case is recombinant-protein perfusion fermentation, the Orchestrator architecture is designed to also support cell-therapy bioreactor campaigns under the ATMP Guidelines (EU GTMP/CTMP + FDA cellular/gene-therapy guidances). When the campaign mode is ATMP, additional ALCOA+ controls per § 5.13 are enabled.

## 4. User Roles

| Role | Permissions |
|---|---|
| Operator | View HMI; acknowledge non-critical alarms; start / pause / abort within recipe envelope; record observations. |
| Senior Operator / Cell-Culture Lead | All Operator + second-person verification of critical events (medium changeover, perfusion-rate change, harvest decision, feed-strategy override). |
| Recipe Author | Author / edit recipes in DRAFT under change control; cannot approve. |
| Recipe Reviewer | Review recipes; cannot review own. |
| Recipe Approver (QA + Process Sciences Lead) | Approve recipes to EFFECTIVE; co-signed. |
| Chemometrician / PAT Specialist | Author / review PAT model versions; co-approve PAT model changes with Process Sciences. |
| Orchestrator Author (Quality IT — Bioprocess Custom Apps) | Modify Orchestrator code under Cat-5 SDLC; cannot approve. |
| Orchestrator Reviewer (CSV Architect) | Review Orchestrator releases; cannot approve own. |
| QA Cat-5 Reviewer | Review releases; co-approve deployment. |
| Functional Safety Engineer | Author / review SIS-side logic on DeltaV SIS partition; IEC 61511 governance. |
| Approver (Head of Biologics Mfg + Head of QA) | Joint approval of Orchestrator deployments. |
| System Administrator | OS / patch / OpenShift / AD; cannot approve recipes / releases / PAT models. |
| Auditor | Read-only across configuration, recipes, batch records, audit trails. |
| Inspection-Read-Only Account | Time-bound read-only access for regulator inspection (Annex 11 § 6 inspection-readiness). |

**Separation of duties:** Recipe Author ≠ Recipe Reviewer ≠ Recipe Approver of the same recipe; PAT Chemometrician ≠ PAT Model Approver of own model; Orchestrator Author ≠ Reviewer ≠ Approver of the same release; Operator ≠ Verifier of the same critical event; System Administrator cannot approve any GxP artefact.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` direct GxP impact / `R2` indirect / `R3` none), and a verifiable `shall`-clause.

### 5.1 Platform / Hardware

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | The Orchestrator shall be deployed in high-availability mode on the site OpenShift 4.14 cluster (3 replicas + DR replica); Ignition Gateway cluster shall run N+1 with automatic failover ≤ 60 s; DeltaV controllers shall be deployed redundantly per Emerson reference architecture; failover events shall be logged and surfaced on the HMI. |
| URS-PLAT-02 | H | R1 | UPS coverage shall provide ≥ 30 min controlled hold across the SCADA / DCS / Orchestrator stack; safety-rated DCS interlocks shall default to safe state (perfusion stops, feed stops, agitation continues at minimum, jacket temperature held at last-known setpoint) on power loss. |
| URS-PLAT-03 | H | R1 | The Orchestrator + SCADA + DCS shall reside on a dedicated process-control VLAN (Purdue Level 2/3); routing to the office IT network shall be denied by stateful firewall + diode where applicable; only allow-listed integration egress shall be permitted. |
| URS-PLAT-04 | H | R1 | Time synchronisation shall use PTP (IEEE 1588) Master-Boundary clocks; the maximum skew across DCS / SCADA / Orchestrator nodes shall be ≤ 1 ms with continuous monitoring; degraded sync shall raise an alarm. |
| URS-PLAT-05 | M | R2 | Hardware refresh / firmware update of any Cat-4 or Cat-5 node shall follow approved CR + revalidation per the impact assessment. |

### 5.2 Recipe / Control-Strategy Lifecycle (ISA-88 master / site / control recipe hierarchy)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REC-01 | H | R1 | Recipes shall follow the lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE; transitions shall require role-restricted electronic signatures. |
| URS-REC-02 | H | R1 | Recipes shall be authored at three ISA-88 levels: Master Recipe (campaign-template), Site Recipe (site-fitted), Control Recipe (per-batch instantiation); cross-level references shall be version-pinned. |
| URS-REC-03 | H | R1 | Recipes shall encode the validated control strategy: CQAs, CPPs, PAT-driven control rules, perfusion schedule, feed-strategy envelope, harvest-decision rules, alarm-classification thresholds. |
| URS-REC-04 | H | R1 | Only EFFECTIVE recipes shall be loadable for product runs; DRAFT / REVIEW / OBSOLETE recipes shall be rejected by the runtime API. |
| URS-REC-05 | H | R1 | EFFECTIVE recipes shall be immutable; changes shall create new revisions via change control (`CR-BIOSCADA-####`). |
| URS-REC-06 | H | R1 | Recipe transitions shall require role-restricted electronic signatures with separation of duties: DRAFT → REVIEW = Author submission; REVIEW → APPROVED = Process Sciences + QA dual-sign; APPROVED → EFFECTIVE = Head of Biologics Mfg + Head of QA dual-sign. |
| URS-REC-07 | H | R1 | Recipe download from PAS-X shall validate SHA-256 checksum + version against the local approved registry before load; mismatch shall block the cycle and create a deviation. |
| URS-REC-08 | H | R1 | A recipe shall reference EFFECTIVE PAT-model versions and EFFECTIVE phase-logic versions; broken references shall block APPROVAL. |
| URS-REC-09 | M | R2 | Recipe impact assessment for any change shall capture impacted CQAs / CPPs and required regulatory variation status per ICH Q12 Established Conditions. |

### 5.3 Recipe Phases (ISA-88 batch state machine — continuous-process specifics)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PHASE-01 | H | R1 | The Orchestrator shall execute the ISA-88 procedural-control hierarchy: Procedure → Unit Procedure → Operation → Phase; each Phase shall be a versioned artefact under Cat-5 SDLC. |
| URS-PHASE-02 | H | R1 | The continuous-process state machine shall include phases: `INOCULATION` (seed introduction), `EXPONENTIAL_GROWTH` (batch-mode pre-perfusion), `STEADY_STATE_PERFUSION` (continuous operation), `HARVEST_DECISION` (PAT-driven harvest trigger), `HARVEST_BLEED` (continuous harvest), `CAMPAIGN_END`, `CIP`, `SIP`. |
| URS-PHASE-03 | H | R1 | Phase transitions shall be deterministic and recorded with PTP-derived timestamps + entry/exit conditions + signing user. |
| URS-PHASE-04 | H | R1 | Each Phase shall declare its safe-state response on PAT loss, utility loss, or operator-initiated abort. |
| URS-PHASE-05 | H | R1 | Operator-driven phase transitions outside the validated envelope (e.g., forced `HARVEST_DECISION` without VCD threshold met) shall require Operator + Senior Operator dual signature with reason and shall be flagged in the executed-batch report. |
| URS-PHASE-06 | M | R2 | Phase-execution metrics (duration, deviations within phase, signed events) shall be exposed for periodic-review trending. |

### 5.4 Feed and Perfusion Control

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-FEED-01 | H | R1 | Feed control shall be PAT-driven: Raman-derived glucose / lactate signals shall drive the glucose-feed pump setpoint via the validated control rule; the rule version shall be pinned to the EFFECTIVE recipe. |
| URS-FEED-02 | H | R1 | Perfusion exchange rate (V/V/day) shall be controlled to maintain steady-state VCD within the recipe-defined envelope; capacitance + on-line VCD inputs shall be used with sensor-fusion logic; sensor loss shall demote control authority per URS-PAT-04. |
| URS-FEED-03 | H | R1 | Feed-strategy override during a run shall require Operator + Senior Operator dual signature with reason; the override shall be recorded in the executed-batch report with the input-snapshot pointer. |
| URS-FEED-04 | H | R1 | Feed-pump skid integrity (rotation sensor + flow-meter cross-check) shall be monitored; mismatch ≥ 5% sustained > 60 s shall raise a critical alarm and trigger fallback to validated open-loop schedule. |
| URS-FEED-05 | H | R1 | Bleed-rate control during continuous harvest shall maintain target VCD; bleed-rate deviation shall trigger alarms classified info / warning / critical per the alarm-rationalisation table. |
| URS-FEED-06 | M | R2 | Cell-retention device (ATF / TFF / spin-filter) health shall be monitored via TMP + flux trends; fouling-precursor detection shall raise maintenance alarms. |

### 5.5 PAT Integration and Chemometric-Model Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PAT-01 | H | R1 | PAT signals shall be consumed via OPC UA over TLS with mutual authentication; tag-quality metadata shall accompany every reading; signal-quality degradation shall be alarmed. |
| URS-PAT-02 | H | R1 | PAT models (Raman PLS for glucose / lactate / titer; capacitance for VCD) shall be versioned and lifecycle-managed under SDLC: DRAFT → CALIBRATED → CROSS-VALIDATED → APPROVED → EFFECTIVE → OBSOLETE; rule changes outside the regulator-approved range shall require ICH Q12 variation. |
| URS-PAT-03 | H | R1 | The EFFECTIVE PAT model version shall be pinned by the EFFECTIVE recipe; runtime shall reject any PAT prediction from a non-matching model version. |
| URS-PAT-04 | H | R1 | Loss of a PAT instrument used by the control strategy shall trigger the recipe-defined safe-state response (revert to a validated open-loop feed schedule, demote APC authority, flag for investigation); the response shall be deterministic, repeatable, and reconstructable from logged inputs + code-version + PAT-model-version. |
| URS-PAT-05 | H | R1 | PAT-model performance shall be monitored on-line (residual / Hotelling T² / Q-statistic per ASTM E2476); out-of-statistical-control conditions shall raise alarms and shall not silently degrade control quality. |
| URS-PAT-06 | M | R2 | Reference-method calibration check (off-line HPLC / cell-counter) shall be triggered at recipe-defined cadence (e.g., every 12 h during steady state); deviations from PAT predictions shall be logged. |
| URS-PAT-07 | M | R2 | Chemometric-model updates shall be co-approved by Chemometrician + Process Sciences + QA; regulator-impacting changes shall be linked to a ICH Q12 variation record. |

### 5.6 Run Execution and Continuous Control

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RUN-01 | H | R1 | The Orchestrator shall execute the loaded recipe per setpoint envelopes; deviations shall trigger alarms classified info / warning / critical / SIS per ISA-18.2. |
| URS-RUN-02 | H | R1 | Critical alarms (PAT-signal loss on a control-driving instrument, sustained CPP excursion ≥ recipe-defined threshold, perfusion-loop blockage indication, contamination signal) shall be acknowledged with reason; they shall not be self-clearing. |
| URS-RUN-03 | H | R1 | All CQA / CPP / PAT signals shall be recorded continuously at ≥ the rate required to support reconstruction (1 Hz minimum for CPPs; PAT cadence per instrument capability). |
| URS-RUN-04 | H | R1 | PAT-driven feed control shall be deterministic, repeatable, and reconstructable from logged PAT inputs, EFFECTIVE recipe version, EFFECTIVE PAT-model version, and Orchestrator code-release version; floating-point determinism shall be verified per OQ. |
| URS-RUN-05 | H | R1 | Manual setpoint override during a product run shall require dual signature (Operator + Senior Operator) and a captured reason; the override shall be flagged in the executed-batch report with an input-snapshot pointer for reconstruction. |
| URS-RUN-06 | H | R1 | Loss of a PAT instrument used by the control strategy shall trigger a safe-state response per URS-PAT-04. |
| URS-RUN-07 | H | R1 | Batch instantiation from a PAS-X production order shall be atomic; failure shall roll back without partial creation. |
| URS-RUN-08 | M | R2 | Out-of-sequence operator commands shall be blocked unless an authorised override is signed; the override shall record current phase + intended phase + reason. |

### 5.7 Alarm Management (ISA-18.2)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ALM-01 | H | R1 | Alarms shall be rationalised per ISA-18.2 with classifications: `INFO`, `WARNING`, `CRITICAL`, `SIS`; each shall have a defined response, acknowledgement requirement, and escalation path. |
| URS-ALM-02 | H | R1 | Critical alarms shall require operator acknowledgement with reason text ≥ 10 chars; unacknowledged criticals shall trigger escalation per the alarm-rationalisation table within the defined window. |
| URS-ALM-03 | H | R1 | Alarm flood mitigation: simultaneous alarm rate exceeding the rationalised threshold shall trigger alarm-shelving per ISA-18.2; shelving shall be logged + reviewed. |
| URS-ALM-04 | H | R1 | SIS alarms (handled by DeltaV SIS, SIL 2 partition) shall invoke pre-defined SIS responses without operator intervention; events shall be logged in the SIS event recorder and replicated to the audit trail. |
| URS-ALM-05 | M | R2 | Alarm metrics (rate, acknowledgement latency, top-talker tags, shelving frequency) shall be exposed for periodic review. |

### 5.8 HMI per ISA-101

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-HMI-01 | H | R1 | HMI screens shall follow ISA-101 hierarchical design: Level 1 (operator overview), Level 2 (unit detail), Level 3 (diagnostic), Level 4 (engineering); navigation depth ≤ 3 clicks to any control. |
| URS-HMI-02 | H | R1 | Visual coding shall use a defined high-performance HMI palette: muted greys for normal state, saturated colours reserved for abnormal indications; alarm priorities shall map to a fixed colour table. |
| URS-HMI-03 | H | R1 | Faceplate response time shall be ≤ 500 ms at 95th percentile under production load. |
| URS-HMI-04 | M | R2 | HMI changes shall be under change control; a non-prod gateway shall be used for HMI regression before deployment. |

### 5.9 Custom Software (Cat-5) SDLC

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEV-01 | H | R1 | The Orchestrator shall be developed under a documented Cat-5 SDLC: requirements → design → code → unit test → integration test → simulator-based scenario test → security scan → user acceptance → release; each gate signed off. |
| URS-DEV-02 | H | R1 | Code shall reside in validated GitLab with signed commits; merges to `main` shall require peer review and passing CI. |
| URS-DEV-03 | H | R1 | Unit-test coverage shall be ≥ 95% on safety-relevant modules (control-strategy evaluation, safe-state response, PAT-loss handler, batch state-machine transitions). |
| URS-DEV-04 | H | R1 | Static analysis (Ruff, mypy --strict, Bandit) + dependency scanning + SAST shall run on every CI build; critical findings shall block. |
| URS-DEV-05 | H | R1 | Releases shall be cryptographically signed (cosign / Sigstore); runtime shall verify signature before loading; mismatched signatures shall abort module load. |
| URS-DEV-06 | H | R1 | Each release shall ship with: release notes, FS / DS update, regression report, security-scan report, change-control record. |
| URS-DEV-07 | H | R1 | Determinism verification shall be performed at OQ: 1000× repeated decisions on canonical input set shall produce bitwise-identical outputs; floating-point round-mode pinned per IEEE-754. |
| URS-DEV-08 | M | R2 | Container images for the Orchestrator shall be scanned for CVEs at build and runtime; HIGH and CRITICAL CVEs shall block deployment. |

### 5.10 Audit Trail / 21 CFR Part 11 / Data Integrity

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | The system shall maintain a time-stamped, secure audit trail per 21 CFR § 11.10(e) and Annex 11 § 9, covering recipe lifecycle, PAT-model lifecycle, control-action decisions, phase transitions, alarm acknowledgements, signatures, code releases, configuration changes. |
| URS-AUD-02 | H | R1 | Audit trail shall be append-only per Annex 11 § 9; no admin shall be able to update or delete entries. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be performed by the Quality Reviewer per harvest cycle and by QA Compliance quarterly. |
| URS-AUD-04 | H | R1 | Retention shall be ≥ 25 years from product expiry per EU GMP Chapter 4. |
| URS-AUD-05 | H | R1 | Audit entries for control-action decisions shall include input-snapshot pointers (PAT, IP-data, recipe-version, code-version) so the decision is reconstructable from source data. |
| URS-PART11-01 | H | R1 | Per § 11.10(a), procedural controls shall protect electronic-record validity. |
| URS-PART11-02 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via AD + MFA. |
| URS-PART11-03 | H | R1 | Per § 11.10(e), the operational audit trail per URS-AUD-01 shall exist. |
| URS-PART11-04 | H | R1 | Per § 11.50, electronic signatures shall include printed name, date / time, and meaning of signature; SoD enforced. |
| URS-PART11-05 | H | R1 | Per § 11.70, signatures shall be cryptographically linked to the signed record. |
| URS-PART11-06 | H | R1 | Per § 11.100, signatures shall be unique per individual; reuse / reassignment blocked. |
| URS-PART11-07 | H | R1 | Per § 11.200, re-authentication shall be required at the moment of signing critical events. |
| URS-PART11-08 | H | R1 | Per § 11.300, password / credential controls shall meet site InfoSec policy. |
| URS-DI-01 | H | R1 | **Attributable:** every record / decision shall be attributable to a named user. |
| URS-DI-02 | H | R1 | **Legible:** records exportable as PDF/A-3 + machine-readable JSON / CSV. |
| URS-DI-03 | H | R1 | **Contemporaneous:** PTP-synchronised timestamps from DCS / PLC level up. |
| URS-DI-04 | H | R1 | **Original:** PAT signals + raw inputs preserved unaltered; corrections recorded as new annotated values referencing the original. |
| URS-DI-05 | H | R1 | **Accurate:** control-strategy calculations shall be deterministic and verified under OQ. |
| URS-DI-06 | M | R2 | **Complete / Consistent / Enduring / Available:** ≥ 25-yr retention; retrievable within 1 business day during inspection. |

### 5.11 Single-Use vs Stainless Configuration Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CFG-01 | H | R1 | The Orchestrator shall support both single-use bioreactor configurations (Sartorius Biostat STR / Cytiva XDR / Thermo HyPerforma DynaDrive) and stainless-steel configurations (ABEC CSTR / Pall Allegro stainless); the active configuration shall be declared in the EFFECTIVE recipe. |
| URS-CFG-02 | H | R1 | Configuration-specific control envelopes (volume / agitation / sparge / gas blend) shall be enforced per the active configuration; cross-config envelope leakage shall be rejected at recipe-load. |
| URS-CFG-03 | H | R1 | Single-use components (bag-id + manufacturer + lot + expiry) shall be captured at batch start and stored in the executed-batch report; mismatched / expired components shall block run start. |
| URS-CFG-04 | M | R2 | Configuration changeover (single-use → stainless or vice versa) shall require an approved CR and revalidation of affected control envelopes. |

### 5.12 ATMP Cell-Therapy Mode (when applicable)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ATMP-01 | H | R1 | When the campaign mode is ATMP, the Orchestrator shall enforce patient-batch isolation: only one ATMP patient batch active per train at a time; cross-patient contamination prevention via interlock. |
| URS-ATMP-02 | H | R1 | ATMP campaigns shall record donor-traceability metadata (de-identified donor-id + tissue-bank reference) per the ATMP Guidelines; metadata shall flow to PAS-X and Watson LIMS for chain-of-identity (COI). |
| URS-ATMP-03 | H | R1 | USP <1043> ancillary-material records (lot, qualification status, expiry) shall be consumed from Watson LIMS; expired or non-qualified materials shall block batch start. |
| URS-ATMP-04 | M | R2 | ATMP runs shall be flagged for additional QP-review steps per EU GMP Annex 2 + Directive 2001/83/EC. |

### 5.13 ISA-95 Enterprise Integration / Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-MES-01 | H | R1 | Recipe download from PAS-X via REST over mTLS; checksum + version validated before load (per URS-REC-07). |
| URS-INT-MES-02 | H | R1 | Executed-batch report (cycle profile + alarms + signatures + PAT trace) pushed to PAS-X at harvest events and at campaign end within 30 min. |
| URS-INT-EQMS-01 | H | R1 | Critical alarms not closed within the configured window shall auto-create deviations in MasterControl via REST with idempotency. |
| URS-INT-PAT-01 | H | R1 | PAT signals via OPC UA over TLS with mutual authentication; loss of PAT triggers safe-state per URS-PAT-04. |
| URS-INT-HIST-01 | H | R1 | All GxP-relevant tags streamed to Aspen IP.21 via OPC HDA / OPC UA; lossless during network blips via local buffering. |
| URS-INT-LIMS-01 | H | R1 | Watson LIMS shall be queried for raw-material qualification + ATMP donor metadata; only QC_RELEASED materials accepted. |
| URS-INT-BMS-01 | H | R1 | BMS-driven utility-status interlocks (clean steam pressure, WFI / PW availability, HVAC differential pressure) shall be consumed; loss shall safe the affected unit operation. |
| URS-INT-AD-01 | H | R1 | Authentication via AD `crocus.local`; service accounts via HashiCorp Vault; LDAPS / Kerberos only. |

### 5.14 Performance / Availability / Backup / Security / Training / Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | H | R1 | Control-loop latency shall be ≤ 500 ms at 95th percentile under production load. |
| URS-PERF-02 | H | R1 | Sustained ≥ 1 Hz logging across all CQA / CPP / PAT channels shall be demonstrated for ≥ 60 days continuous run without data loss. |
| URS-PERF-03 | M | R2 | HMI faceplate response ≤ 500 ms; alarm-ack latency ≤ 1 s. |
| URS-AV-01 | H | R1 | Availability during production shall be ≥ 99.5%; planned maintenance only during scheduled production-down windows. |
| URS-BAK-01 | H | R1 | Database backed up nightly with PITR; retention ≥ 25 years; cryptographic integrity verification. |
| URS-BAK-02 | H | R1 | Quarterly restore test, witnessed by QA. |
| URS-BAK-03 | M | R2 | RTO ≤ 4 hours (Gateway failover); RPO ≤ 1 minute (replication). |
| URS-SEC-01 | H | R1 | All authentication via AD; service accounts via vault; no local accounts other than break-glass admin. |
| URS-SEC-02 | H | R1 | TLS 1.2+ minimum on all HMI ↔ Gateway; mTLS Gateway ↔ DCS / PAT / pumps where supported. |
| URS-SEC-03 | M | R2 | Vulnerability scans monthly; criticals remediated within 30 days. |
| URS-SEC-04 | M | R2 | Removable media blocked by GPO except for vendor-approved engineering use under CR. |
| URS-TRN-01 | H | R1 | Production access shall require recorded role-specific training in the LMS, including alarm-acknowledgement and safe-state-handling scenarios. |
| URS-TRN-02 | M | R2 | Annual refresher training shall cover ICH Q13 + EU GMP Annex 2 + Annex 1 updates + ATMP scenarios. |
| URS-PR-01 | H | R1 | Annual periodic review covering configuration drift, code-release register, audit-trail review evidence, alarm trends, control-strategy verification, PAT-model performance trends, ATMP-mode coverage; signed by Bioprocess Automation Lead + Head of Biologics Mfg + Head of QA. |
| URS-PR-02 | M | R2 | Variation submissions affecting Established Conditions (ICH Q12) shall be tracked through approval; production rules updated only after variation is approved. |

### 5.15 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem with local OT cached credentials for offline operation; conditional-access policy `OT-SCADA Conditional Access (MFA at HMI session start; named-location restriction to plant network)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the SCADA historian DB; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 15 y (batch-history) per the consuming-record schedule. |

## 6. Acceptance Criteria

1. CS, FS, DS, RA, IQ, OQ, PQ approved and executed (full Cat-5 set).
2. PQ shall include a representative ≥ 60-day continuous run + PAT-loss safe-state scenarios + alarm-flood scenario + a code-deployment under the Cat-5 SDLC + an ATMP-mode dry-run.
3. VSR approved by Bioprocess Automation Lead + Head of Biologics Mfg + Head of QA + Functional Safety Engineer.
4. RTM shall demonstrate every URS-ID maps to ≥ 1 approved test case.
5. Determinism verification: OQ shall include 1000× repeat-decision test producing bitwise-identical outputs.
6. SIS proof-test integration shall be exercised during PQ per IEC 61511.

## 7. Constraints

- Cat-5 SDLC governs all Orchestrator changes.
- DCS firmware changes shall follow Emerson + IEC 61511 safety-SDLC for DeltaV SIS.
- PAT changes shall require control-strategy revalidation per ICH Q12.
- Ignition platform patches under change control per Inductive Automation SDLC.
- Site connectivity to corporate IT network through firewall + DMZ; no direct routing.

## 8. Assumptions

- MES (PAS-X v3.2), eQMS (MasterControl), AD, HashiCorp Vault, PAT instruments, DeltaV v15.3, Aspen IP.21, Watson LIMS are themselves validated.
- BMS (utilities) is validated and exposes its status via the agreed interlock contract.
- The site has approved control-strategy filings with NMPA (China) and the relevant export markets; Established Conditions are documented per ICH Q12.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300 — Electronic Records; Electronic Signatures.
- 21 CFR Part 211 §§ .22, .68, .180, .192 — Current GMP for Finished Pharmaceuticals.
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).
- FDA *Guidance on PAT — A Framework for Innovative Pharmaceutical Development, Manufacturing, and Quality Assurance* (2004).
- FDA *Quality Considerations for Continuous Manufacturing* (final, February 2023).
- FDA *Guidance on Q13: Continuous Manufacturing of Drug Substances and Drug Products* (2024).
- FDA Cellular & Gene Therapy Guidances (ATMP-equivalent context).

### EU
- EU GMP Annex 11 §§ 4 (validation), 6 (accuracy), 9 (audit trail), 11 (periodic evaluation) — Computerised Systems.
- EU GMP Annex 1 (revised 2022) — Manufacture of Sterile Medicinal Products.
- EU GMP Annex 2 — Manufacture of Biological Active Substances and Medicinal Products for Human Use.
- EU GMP Chapter 4 — Documentation (retention).
- Directive 2001/83/EC Art. 51 — Qualified Person obligations (where ATMP applies).
- EMA *Guideline on Advanced Therapy Medicinal Products* (ATMP).

### International — ICH / USP / Compendial
- ICH Q5A(R2) / Q5B — Viral Safety / Genetic Stability for biotechnological products.
- ICH Q9(R1) — Quality Risk Management.
- ICH Q10 — Pharmaceutical Quality System.
- ICH Q11 — Development and Manufacture of Drug Substances.
- ICH Q12 — Technical and Regulatory Considerations for Pharmaceutical Product Lifecycle Management.
- ICH Q13 — Continuous Manufacturing of Drug Substances and Drug Products.
- USP <1043> — Ancillary Materials for Cell and Tissue Therapies.

### Industry — ISPE / ISA / IEC / PIC/S
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE Baseline Guide — *Biopharmaceutical Manufacturing Facilities*.
- ISPE GAMP Good Practice Guide — *Process Analytical Technology*.
- ISPE GAMP Good Practice Guide — *A Risk-Based Approach to Operation of GxP Computerized Systems*.
- ISA-88 (Batch Control standard, parts 1-4).
- ISA-95 (Enterprise-Control System Integration).
- ISA-101 (HMI Design).
- ISA-18.2 (Alarm Management).
- IEC 61511 (Safety Instrumented Systems for the Process Industry).
- ASTM E2476 — Multivariate Statistical Process Control.
- PIC/S PI 041 — Good Practices for Data Management and Integrity in Regulated GMP/GDP Environments.

### Vendor
- Inductive Automation — *Ignition 8.3 Reference*.
- Emerson — *DeltaV v15.3 Reference Architecture* + *DeltaV SIS Safety Manual*.
- Sartorius — *Biostat STR Single-Use Bioreactor Operating Manual*.
- Cytiva — *XDR Single-Use Bioreactor Reference*.
- Thermo Fisher — *HyPerforma DynaDrive Single-Use Bioreactor Reference*.
- Kaiser Optical Systems — *RamanRxn4 In-line Spectrometer Reference*.
- Hamilton Process Analytics — *Incyte Capacitance Sensor Reference*.
- Repligen — *XCell ATF Cell-Retention Operating Manual*.

### DACH / Asia-regulatory context
- BfArM (DE) — Bundesinstitut für Arzneimittel und Medizinprodukte (export market).
- Swissmedic (CH) — biological medicinal products (export market).
- NMPA (China) — local market authorisation.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

