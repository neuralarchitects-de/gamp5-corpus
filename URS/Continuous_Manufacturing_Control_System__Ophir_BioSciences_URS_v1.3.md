---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; v1.2 enrichment 2026-05-13"
seed_corpus_basis:
  - "josephiuliucci/SDLC-PB SDLC_CSA_HiveMQ + URS_SCADA (industrial CSA + GAMP Cat 5 reasoning)"
  - "GAMP 5 (2nd ed.) Cat 5 conventions for custom control software"
  - "21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; EU GMP Annex 15; ICH Q13 (FDA implementing 2024); ICH Q14; ICH Q12; ICH Q9(R1); ICH Q10; ICH Q8(R2)"
  - "ANSI/ISA-88; ANSI/ISA-95; FDA CSA Feb 2026"
do_not_use_as:
  - regulated_record
  - basis_for_real_validation_decisions
intended_use:
  - LLM fine-tuning corpus seed
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Continuous Manufacturing Control System — Site-Authored CM Orchestrator (Python + Ignition + AB ControlLogix)

**Document Number:** OPH-URS-CM-001
**Version:** 1.2
**Effective Date:** 2026-05-13 *(synthetic)*
**Site:** Ophir BioSciences Ltd, Continuous Manufacturing Plant 1, Haifa, Israel *(fictional)*
**System Owner:** Continuous Manufacturing Lead
**Process Owner:** Head of Manufacturing Sciences
**Development Owner:** Quality IT — Custom Applications
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom Application (CM Orchestrator authored in-house; Ignition + ControlLogix are Cat 4 platforms layered with Cat 5 site logic)
**Project Mode:** Custom-build project — site-developed system (GAMP 5 Category 5 — Bespoke; internal SDLC). System: Site-Authored CM Orchestrator (Python + Ignition + AB ControlLogix).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Annex 15 (Qualification and Validation); ICH Q13 Continuous Manufacturing of Drug Substances and Drug Products (FDA implementing 2024); ICH Q14 Analytical Procedure Development; ICH Q12 Established Conditions; ICH Q9(R1); ICH Q10; ICH Q8(R2); FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026); ANSI/ISA-88 Part 1+2; ANSI/ISA-95 Part 1

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead — Continuous Manufacturing) | _____________ | _____________ | _____ |
| Reviewer (Continuous Manufacturing Lead) | _____________ | _____________ | _____ |
| Reviewer (Process Sciences Lead) | _____________ | _____________ | _____ |
| Reviewer (PAT Scientist) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Quality IT Lead — Custom Apps) | _____________ | _____________ | _____ |
| Reviewer (Functional Safety Engineer) | _____________ | _____________ | _____ |
| Approver (Head of Manufacturing Sciences) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |
| Approver (Qualified Person) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Risk-table reformatted per v1.1 sweep. |
| 1.2 | 2026-05-13 | (synthetic) | Tier T3 enrichment (100-150 req target). Added state-of-control + design-space, ICH Q12 Established Conditions, ICH Q13 specific reqs, ICH Q14 analytical-procedure, diverter / reject logic + genealogy, PAT (NIR / Raman / particle size) integration. Citations updated per METHODOLOGY § 2A.1. |

## Definitions

| Term | Definition |
|---|---|
| CM | Continuous Manufacturing |
| CDC | Continuous Direct Compression line (drug-product CM topology) |
| CM Orchestrator | Site-authored Python orchestration service supervising the CM line and enacting RTRT decisions |
| RTRT | Real-Time Release Testing per ICH Q13 |
| CQA / CPP | Critical Quality Attribute / Critical Process Parameter |
| Diversion / Diverter | Real-time material rejection from the line when CQAs exceed limits |
| Material Tracking | Per-time-resolved tracking of upstream API + excipients through the line, with residence-time distribution (RTD) modelling |
| PAT | Process Analytical Technology (NIR / Raman / mass-flow / particle-size) |
| State of Control | Per ICH Q10: demonstrated consistent process performance within validated control space |
| Design Space | Per ICH Q8(R2): multidimensional combination of input variables shown to assure quality |
| Established Conditions | Per ICH Q12: parameters required to assure product quality + subject to regulatory reporting category |
| MES | Werum / Körber PAS-X v3.2 |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| SIL | Safety Integrity Level (IEC 61511) |

## 1. Purpose

This URS defines requirements for the continuous-manufacturing control system that supervises the integrated CM line (continuous direct compression) and enacts Real-Time Release Testing decisions per ICH Q13 at Ophir BioSciences Plant 1.

This is **GAMP Category 5 overall** because the CM Orchestrator is site-authored and materially controls product quality through diversion / acceptance decisions. Underlying Ignition (Cat 4) and AB ControlLogix safety-PLC code (vendor + site SIL-rated) are validated within their own scopes; the integrated system + custom orchestrator are validated as Cat 5.

## 2. Scope

**In scope:**

- CM Orchestrator (Python 3.12 + FastAPI + PostgreSQL 16, ~9,000 LOC).
- Ignition 8.3 SCADA layer.
- AB ControlLogix safety PLC (separate functional-safety SDLC per IEC 61511 SIL 2).
- PAT instruments: NIR (in-line blend uniformity + content uniformity feedback), Raman (assay), mass-flow (loss-in-weight feeders), particle-size (parallel acoustic emission + light-scattering).
- Diverter mechanism: pneumatic gate at compaction-train exit with sub-100-ms actuation.
- Integrations: PAS-X (recipe / batch report), eQMS (deviation creation), AD authentication, site PTP.

**Out of scope:**

- Physical equipment (mechanical / electrical / utilities — separate equipment qualification).
- PAT instrument qualifications (separate URSs `EQ-PAT-NIR-001`, `EQ-PAT-RAMAN-001`, `EQ-PAT-FEEDER-001`, `EQ-PAT-PSD-001`).
- Upstream API receipt and downstream blister packaging.
- Chemometric / multivariate model development + lifecycle (`PAT-MODEL-LCM-001`).

## 3. System Description and Intended Use

The CM Orchestrator continuously supervises the line: it consumes PAT and process-parameter signals at high frequency (≥ 1 Hz with PAT typically 5-20 Hz), computes the running CQA estimates per the validated control strategy, decides accept / divert at the time-resolved level (per RTRT), commands the Ignition layer + ControlLogix interlocks accordingly, records full traceability (material genealogy across the train, including residence-time-distribution modelling), and produces an executed-batch report to PAS-X on batch end. ICH Q13 RTRT is the basis for batch release; QP discretionary override is preserved per Directive 2001/83/EC Art. 51.

## 4. User Roles

| Role | Permissions |
|---|---|
| Operator | Acknowledge alarms; start / pause / abort line within the recipe envelope. |
| Senior Operator / Line Lead | All Operator + second-person verification of critical-step events. |
| Recipe Author | Author / edit recipes in DRAFT under change control. |
| Recipe Reviewer | Review; cannot approve own. |
| Recipe Approver (QA) | Approve recipes to EFFECTIVE; retire. |
| CM Orchestrator Author (Quality IT) | Author / modify Orchestrator code under SDLC. |
| QA Cat 5 Reviewer | Review releases; co-approve deployment. |
| PAT Scientist | Chemometric / multivariate model authoring + deployment. |
| Continuous Manufacturing Lead | Disposition of diverted material; campaign approval. |
| Functional Safety Engineer | SIL-rated PLC code reviews under safety SDLC. |
| Qualified Person | Release authority per Directive 2001/83/EC Art. 51; discretionary RTRT override authority. |
| Approver (Head of Manufacturing Sciences + Head of QA) | Joint approval of Orchestrator deployments. |
| System Administrator | OS / patch / AD groups; cannot approve. |
| Auditor | Read-only across recipes, code, alarms, audit trails. |

Separation of duties: Author ≠ Reviewer ≠ Approver of the same release; Operator ≠ Verifier of same critical event; PAT Scientist ≠ Recipe Approver of same recipe.

## 5. User Requirements

### 5.1 Platform / Hardware

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | The CM Orchestrator shall be deployed in HA on the site OpenShift cluster (3 replicas + DR replica); Ignition Gateway cluster N+1 with auto-failover. |
| URS-PLAT-02 | H | R1 | UPS coverage shall allow controlled shutdown ≥ 30 min; ControlLogix safety functions shall default to safe state on power loss (line stops; diversion remains in safe state). |
| URS-PLAT-03 | H | R1 | All clients shall reside on the process-control VLAN. |
| URS-PLAT-04 | H | R1 | The Orchestrator runtime shall verify signatures of all loaded modules (cosign-verified) at process start and on every module reload. |
| URS-PLAT-05 | M | R2 | Replicas shall be distributed across ≥ 2 physical fault domains within the data centre. |

### 5.2 Recipe and Control-Strategy Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REC-01 | H | R1 | Recipes shall follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE. |
| URS-REC-02 | H | R1 | Recipes shall encode the validated control strategy: CQAs, CPPs, control limits, diversion rules. |
| URS-REC-03 | H | R1 | Only EFFECTIVE recipes may be loaded for product runs. |
| URS-REC-04 | H | R1 | Recipe transitions shall require role-restricted electronic signatures with separation of duties. |
| URS-REC-05 | H | R1 | EFFECTIVE recipes shall be immutable; changes shall create new revisions via change control. |
| URS-REC-06 | H | R1 | Recipe-parameter schema shall enforce ICH Q13 control-strategy fields: CQA list (with acceptance ranges + reference methods); CPP list (with setpoint + envelope); diversion-rule set (per CQA: rule_id + window + threshold + action); PAT-source bindings (per CQA: instrument_id + model_id + cadence). |
| URS-REC-07 | M | R2 | Recipe-diff renderer shall present field-by-field old/new on revision review. |

### 5.3 State-of-Control + Design-Space Monitoring

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SOC-01 | H | R1 | The Orchestrator shall continuously evaluate whether the run is operating within the validated design space (ICH Q8(R2)); excursions outside the design space shall require investigation per the deviation procedure. |
| URS-SOC-02 | H | R1 | The Orchestrator shall maintain a "state of control" indicator per ICH Q10; loss of state-of-control (e.g., sustained CPP drift trending toward control limits, increasing diversion rate) shall trigger a campaign-pause review. |
| URS-SOC-03 | H | R1 | A statistical-process-control (SPC) layer (CUSUM + EWMA on key CPPs / CQAs) shall be implemented; alarms on rule violations (Western Electric / Nelson rules) per recipe configuration. |
| URS-SOC-04 | M | R2 | State-of-control + design-space metrics shall be exposed to the eQMS for annual-product-review aggregation. |

### 5.4 ICH Q12 Established Conditions

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-Q12-01 | H | R1 | The recipe shall identify each Established Condition (EC) per ICH Q12 with its regulatory reporting category (e.g., prior-approval / CBE-30 / annual / not-reportable). |
| URS-Q12-02 | H | R1 | Changes to ECs shall be blocked at the recipe lifecycle level until a change-control record is linked; the recipe-approval workflow shall require the regulatory-affairs signature for prior-approval / CBE-30 changes. |
| URS-Q12-03 | M | R2 | An EC-change audit-trail report shall be runnable on demand to support post-approval change submissions. |

### 5.5 ICH Q13 Continuous Manufacturing Requirements

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-Q13-01 | H | R1 | The system shall support batch definition per ICH Q13 (time-based, equipment-volume-based, or production-volume-based); batch boundaries shall be deterministic and reconstructable. |
| URS-Q13-02 | H | R1 | Material traceability shall be maintained at the time-resolution required by the validated control strategy (typically ≤ residence-time of slowest unit operation); diverted material genealogy shall be preserved. |
| URS-Q13-03 | H | R1 | Process disturbances (PAT excursion, mechanical fault) shall trigger documented response actions per the validated control strategy; auto-divert + auto-pause options shall be configurable per disturbance type. |
| URS-Q13-04 | H | R1 | RTRT decisions shall be supported by the surrogate analytical methods qualified under ICH Q14; methods shall reference their qualification dossier. |

### 5.6 ICH Q14 Analytical Procedure (PAT Methods)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-Q14-01 | H | R1 | Each PAT method (NIR-CU, NIR-blend, Raman-assay, etc.) shall reference its analytical-procedure lifecycle document per ICH Q14; methods shall not be permitted in EFFECTIVE recipes without an APL-doc-ID. |
| URS-Q14-02 | H | R1 | Multivariate / chemometric models shall reference their model-version + validation-dossier-ID; the Orchestrator shall verify cosign signature on model load. |
| URS-Q14-03 | H | R1 | Model-performance metrics (R²cv, RMSEP, residual trends) shall be monitored continuously; degradation > recipe-defined threshold shall raise alarm + flag for PAT Scientist review. |

### 5.7 Run Execution / Diversion / RTRT

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RUN-01 | H | R1 | The Orchestrator shall execute the loaded recipe per its setpoint envelopes; deviations shall trigger alarms classified by severity (info / warning / critical). |
| URS-RUN-02 | H | R1 | Critical alarms (PAT signal loss on a CQA-determining instrument, sustained CPP excursion, diverter-actuator fault) shall acknowledge with reason; not self-clearing. |
| URS-RUN-03 | H | R1 | All CQA / CPP signals shall be recorded continuously at ≥ the rate required to support time-resolved RTRT (typically 1 Hz baseline; PAT instruments 5-20 Hz). |
| URS-RUN-04 | H | R1 | Diversion decisions shall be made per the validated control strategy and shall be deterministic, repeatable, and reconstructable from logged inputs and code version. |
| URS-RUN-05 | H | R1 | Manual override of diversion shall not be permitted during a product run; emergency stop is an alternative path that aborts the line. |
| URS-RUN-06 | H | R1 | The control strategy shall be revalidated upon any change to PAT instrument, instrument calibration window, or control-strategy formula. |
| URS-RUN-07 | H | R1 | Diverter actuation latency shall be ≤ 100 ms from decision to gate state; latency shall be measured and recorded per actuation. |
| URS-RUN-08 | H | R1 | Diverter-actuator health monitoring (cycle-count, pressure, position-sense) shall raise predictive-maintenance alerts on degradation. |

### 5.8 Material Tracking + Genealogy

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MAT-01 | H | R1 | The Orchestrator shall maintain a residence-time-distribution (RTD) model per unit operation; the model shall be qualified at PQ and revalidated on any equipment change. |
| URS-MAT-02 | H | R1 | Time-resolved input genealogy shall be recorded: API lot consumption rate, excipient lot consumption rate (per feeder), water-content per unit time; reconstructable to ± RTD-σ. |
| URS-MAT-03 | H | R1 | Diverted material shall be quarantined with a genealogy reference linking diverter actuations to the inferred input lots based on RTD propagation. |
| URS-MAT-04 | M | R2 | A campaign-end material-mass balance shall be computed (input mass − accepted mass − diverted mass − scrap = closure ε); ε > recipe-defined threshold shall flag investigation. |

### 5.9 Custom Software (Cat-5) SDLC

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEV-01 | H | R1 | The Orchestrator shall be developed under documented Cat-5 SDLC (requirements → design → code → unit / integration tests → security scan → user acceptance → release). |
| URS-DEV-02 | H | R1 | Code in version control with signed commits; merges to `main` shall require peer review and passing CI. |
| URS-DEV-03 | H | R1 | Unit-test coverage shall be ≥ 95% on safety-relevant modules (control-strategy evaluation, diversion decision, RTD model). |
| URS-DEV-04 | H | R1 | Static analysis + dependency scanning + SAST on every CI build; criticals shall block. |
| URS-DEV-05 | H | R1 | Releases shall be cryptographically signed (cosign); the Orchestrator runtime shall verify the signature before loading. |
| URS-DEV-06 | H | R1 | Each release shall ship with: release notes, FS / DS update, regression test report, security-scan report, change-control record. |
| URS-DEV-07 | H | R1 | FDA CSA (Feb 2026) risk-classification + risk-justified-testing rationale shall be documented per release. |

### 5.10 Audit Trail / Part 11

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Time-stamped, secure audit trail covering recipe lifecycle, diversion decisions, alarm acknowledgements, signatures, code releases, model deployments. |
| URS-AUD-02 | H | R1 | Audit trail append-only; no admin update / delete. |
| URS-AUD-03 | H | R1 | Review by Quality Reviewer per batch and QA Compliance quarterly. |
| URS-AUD-04 | H | R1 | Retention ≥ 25 years from product expiry. |
| URS-PART11-01 | H | R1 | E-signatures per § 11.50. |
| URS-PART11-02 | H | R1 | Each signature unique per § 11.100. |
| URS-PART11-03 | H | R1 | Signatures cryptographically bound per § 11.70. |
| URS-PART11-04 | H | R1 | Separation of duties enforced per § 11.10(d) + § 11.10(g). |
| URS-PART11-05 | H | R1 | Re-authentication at signing per § 11.200. |
| URS-PART11-06 | H | R1 | Password / credential controls per § 11.300. |
| URS-PART11-07 | H | R1 | Audit coverage per § 11.10(e); accurate copies per § 11.10(b); retention per § 11.10(c). |

### 5.11 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-MES-01 | H | R1 | Recipes / batch-context downloaded from MES via REST over mTLS; checksum + version validated. |
| URS-INT-MES-02 | H | R1 | Executed-batch report (cycle profile + diversion log + RTRT decision) pushed to MES within 30 minutes of cycle end. |
| URS-INT-EQMS-01 | H | R1 | Critical alarms not closed in time shall auto-create deviations in MasterControl. |
| URS-INT-PAT-01 | H | R1 | PAT signals consumed via OPC UA + REST with mutual authentication; loss of PAT signal shall trigger safe-state diversion. |
| URS-INT-DCS-01 | H | R1 | DeltaV / Ignition control interactions via OPC UA mTLS. |
| URS-INT-HIST-01 | H | R1 | All channel data streamed to historian (Aspen IP.21 / TimescaleDB) at native rate. |
| URS-INT-QP-01 | H | R1 | QP override endpoint shall require QP-role electronic signature with reason; override events shall be reported to the eQMS. |

### 5.12 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | Records shall be Attributable to a named AD user. |
| URS-DI-02 | H | R1 | Records shall be Legible — exportable as structured PDF + CSV + machine-readable JSON. |
| URS-DI-03 | H | R1 | Records shall be Contemporaneous — PTP-synchronised timestamps. |
| URS-DI-04 | H | R1 | Original PAT signal values preserved unaltered. |
| URS-DI-05 | H | R1 | Control-strategy calculations Accurate per OQ. |
| URS-DI-06 | M | R2 | Records shall be Complete, Consistent, Enduring (25-yr retention), Available (≤ 4 h during inspection). |

### 5.13 Upstream Feeder + Compactor Coordination

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-FEED-01 | H | R1 | Loss-in-weight feeder mass-flow shall be consumed at ≥ 10 Hz; deviation from setpoint > recipe tolerance shall raise alarm + may trigger diversion per control strategy. |
| URS-FEED-02 | H | R1 | Refill events on each feeder shall be recorded with lot + mass + operator; mid-refill mass-flow excursions shall be classified separately from steady-state. |
| URS-FEED-03 | H | R1 | Compactor (roller-compactor / direct-compression press) parameters (force, gap, roll-speed) shall be recorded ≥ 1 Hz; CPP-envelope evaluation shall feed the control strategy. |
| URS-FEED-04 | M | R2 | Per-feeder calibration-state shall block recipe-load if any required feeder is OUT_OF_CAL. |

### 5.14 Simulator-Based Testing

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SIM-01 | H | R1 | A line-simulator (digital twin) shall be maintained for the CM line; the Orchestrator shall support a SIMULATOR_MODE wherein PAT inputs are replayed and outputs are recorded for verification without physical actuation. |
| URS-SIM-02 | H | R1 | Each Orchestrator release shall pass a scenario regression suite executed in SIMULATOR_MODE before deployment to production. |
| URS-SIM-03 | M | R2 | Simulator-mode runs shall be visibly tagged in audit + reports as non-production. |

### 5.15 Post-Market Change Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PMCM-01 | H | R1 | All changes to the control strategy, PAT models, EC parameters, or RTD model shall flow through site change control linked to the CR-ID; the Orchestrator shall reject deployments missing a CR-ID. |
| URS-PMCM-02 | M | R2 | A post-deployment monitoring window (typically 30 days) shall apply elevated-review status to the first batches after a change. |

### 5.16 Performance / Availability / Backup / Security / Training / PR

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | H | R1 | Sustained CQA computation latency ≤ 200 ms at the 95th percentile under production load; sustained ingest from PAT without data loss for ≥ 30 days in OQ. |
| URS-PERF-02 | H | R1 | Diverter-decision-to-actuation latency ≤ 100 ms (URS-RUN-07). |
| URS-AV-01 | H | R1 | System availability during production runs shall be ≥ 99.5%. |
| URS-BAK-01 | H | R1 | Database backed up nightly with PITR; retention ≥ 25 years. |
| URS-BAK-02 | H | R1 | Quarterly restore test, witnessed. |
| URS-SEC-01 | H | R1 | All authentication via AD; service accounts via vault. |
| URS-SEC-02 | H | R1 | Removable media blocked except for vendor-approved engineering use under CR. |
| URS-TRN-01 | H | R1 | LMS-recorded role-specific training. |
| URS-TRN-02 | M | R2 | PAT Scientist + CM Lead + QP shall complete CM-specific decision-logic competency assessment annually. |
| URS-PR-01 | H | R1 | Annual periodic review covering configuration drift, code-release register, audit-trail review, deviation summary, control-strategy verification, EC-change history, model-performance trends, RTD-qualification currency; signed by Continuous Manufacturing Lead + Head of Manufacturing Sciences + Head of QA + QP. |

### 5.17 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem with local OT cached credentials for offline operation; conditional-access policy `OT-SCADA Conditional Access (MFA at HMI session start; named-location restriction to plant network)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the recipe / batch history DB plus file-level capture of PLC program backups; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 15 y (batch-history) per the consuming-record schedule. |

## 6. Acceptance Criteria

The system shall enter validated GMP use when CS, FS, DS, RA, IQ, OQ, PQ approved and executed; PQ shall include representative production runs at low / nominal / high throughput; diversion-rule scenarios (each CQA tested); alarm scenarios; a code-deployment under the Cat-5 SDLC; an EC-change scenario; a QP-override scenario; PAT-loss-fallback scenarios; RTD-model validation runs. VSR approved.

## 7. Constraints

- Cat-5 SDLC governs all Orchestrator code changes.
- PLC firmware changes follow safety SDLC (IEC 61511).
- PAT changes require control-strategy revalidation per URS-RUN-06.
- ICH Q12 EC-classification changes follow the regulatory affairs change-control process.

## 8. Assumptions

- MES, eQMS, AD, vault, PAT instruments are validated.
- Site OpenShift platform is validated for GxP workload per `INFRA-OS-CSV-001`.
- Multivariate-model lifecycle is governed by `PAT-MODEL-LCM-001`.

## 9. References

### US — FDA
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .68, .180, .192.
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).
- FDA *Quality Considerations for Continuous Manufacturing* (final, 2023).
- FDA *Guidance for Industry — PAT: A Framework for Innovative Pharmaceutical Development, Manufacturing, and Quality Assurance* (2004).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EU GMP Annex 15 — Qualification and Validation.
- EudraLex Vol 4 Part I.
- Directive 2001/83/EC Art. 51 (QP — Qualified Person batch-release obligations).

### International — ICH
- ICH Q13 — Continuous Manufacturing of Drug Substances and Drug Products (FDA implementing guidance, 2024).
- ICH Q14 — Analytical Procedure Development.
- ICH Q12 — Technical and Regulatory Considerations for Pharmaceutical Product Lifecycle Management.
- ICH Q9(R1) — Quality Risk Management.
- ICH Q10 — Pharmaceutical Quality System.
- ICH Q8(R2) — Pharmaceutical Development.

### Industry guidance
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE Baseline Guide *Continuous Manufacturing of Solid Oral Dosage Forms*.
- PIC/S PI 041 — Good Practices for Data Management and Integrity.

### Standards
- ANSI/ISA-88 Part 1 + Part 2 — Batch Control.
- ANSI/ISA-95 Part 1 — Enterprise-Control System Integration.
- IEC 61511 — Functional Safety; IEC 61508 (general).

### Vendor / Platform
- Real-vendor reference platforms: GEA ConsiGma; Glatt MODCOS; FETTE / Korsch; Bosch Hüttlin; Continuus Pharmaceuticals.
- Inductive Automation — *Ignition 8.3 Configuration Reference*.
- Rockwell Automation — *ControlLogix 5580 Reference*.

### Site
- `EQ-PAT-NIR-001`, `EQ-PAT-RAMAN-001`, `EQ-PAT-FEEDER-001`, `EQ-PAT-PSD-001` — PAT instrument qualifications.
- `PAT-MODEL-LCM-001` — multivariate model lifecycle.
- `INFRA-OS-CSV-001` — OpenShift platform validation.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

