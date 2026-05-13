---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-27; expanded 2026-05-11 (§5 breakout + DACH context + ICH Q12/Q13); uplifted 2026-05-12 to T3 floor (ANVISA + JP + ICH Q10 + PAT-model-lifecycle binding)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed.) Cat 5 conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11"
  - "ICH Q8(R2); Q9(R1); Q10; Q11; Q12; Q13; Q14"
  - "FDA Guidance for Industry on Real-Time Release Testing (2018); FDA Guidance on Q13 (2024); EMA Reflection Paper on RTRT (2012)"
  - "ISPE GAMP 5 (2nd ed., 2022); ISPE GAMP GPG Process Analytical Technology; ISPE RTRT GPG"
  - "Swissmedic (CH) guidance on continuous manufacturing; BfArM (DE) RTRT considerations; AGES (AT)"
  - "ANVISA RDC 1/2024 (Brazil — emerging regulatory framework); JP General Information G6 (RTRT)"
  - "Directive 2001/83/EC Art. 51 (Qualified Person)"
  - "PIC/S PI 041"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# User Requirements Specification (URS)

## Real-Time Release Testing (RTRT) Platform — Site-Developed Python on K8s + Decision-Rule Engine

**Document Number:** HSP2-URS-RTRT-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Hesperia BioPharma AG, Continuous Manufacturing Plant 1, Visp, Switzerland *(fictional)*
**System Owner:** RTRT Lead
**Process Owner:** Head of Continuous Manufacturing
**Development Owner:** Quality IT — RTRT Custom Apps
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom Application
**Project Mode:** Custom-build project — site-developed system (GAMP 5 Category 5 — Bespoke; internal SDLC). System: Site-Developed Python on K8s + Decision-Rule Engine.
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Chapter 4; ICH Q8(R2); Q9(R1); Q10; Q11; Q12 (Established Conditions); Q13 (Continuous Manufacturing); Q14; FDA *Real-Time Release Testing* Guidance (2018); FDA Q13 Guidance (2024); EMA *Reflection Paper on RTRT* (2012); Swissmedic (CH) continuous-manufacturing guidance; BfArM (DE); AGES (AT); ANVISA RDC 1/2024; JP General Information G6 (RTRT); Directive 2001/83/EC Art. 51 (QP); PIC/S PI 041.

> **Note:** Distinct from the continuous-manufacturing CRC (Ophir) and the NIR PAT (Faro). This URS covers the **RTRT decision-engine** that aggregates PAT predictions + in-process measurements + raw-material attributes + process-knowledge to render real-time release decisions in lieu of (or alongside) traditional finished-product testing per ICH Q8 design space and ICH Q12 Established Conditions.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (RTRT Lead) | _____________ | _____________ | _____ |
| Reviewer (Statistician / Chemometrician) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs — RTRT Filing) | _____________ | _____________ | _____ |
| Reviewer (Qualified Person — EU Batch Release) | _____________ | _____________ | _____ |
| Reviewer (PAT Model Owner) | _____________ | _____________ | _____ |
| Approver (Head of Continuous Manufacturing) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |
| Approver (VP Regulatory Affairs) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | §5 broken out into 11 subsections; DACH relocation (Visp, CH); ICH Q12 + Q13 explicit binding; Qualified Person (EU batch release) role added; Swissmedic + BfArM added to References; risk table expanded. |
| 1.2 | 2026-05-12 | (synthetic) | T3 floor uplift: added ANVISA + JP cross-reference (§5.12), ICH Q10 PQS linkage (§5.13), PAT model lifecycle binding (§5.14), control-strategy file-version reconciliation (§5.15); req count ~ 115; risk table 14 rows. Tier: **T3** (large enterprise application + multi-jurisdiction filing-aware + PAT + custom-Python decision engine). |

## Definitions

| Term | Definition |
|---|---|
| RTRT | Real-Time Release Testing |
| Decision Rule | Pre-approved logic combining PAT + IP-data + raw-material attributes for release |
| Control Strategy | ICH Q8 / Q11 documented control strategy supporting RTRT |
| Design Space | ICH Q8(R2) multidimensional combination + interaction of input variables and process parameters demonstrated to provide quality assurance |
| Established Conditions | ICH Q12 — those critical aspects of a product or process whose changes need post-approval submissions |
| MLM | Multivariate Latent Model (e.g., PCA / PLS) for batch monitoring |
| Surrogate | A real-time predictor used in lieu of an offline test |
| QP | Qualified Person (EU batch release, per Directive 2001/83/EC Art. 51) |
| PQS | Pharmaceutical Quality System (ICH Q10) |
| ANVISA | Agência Nacional de Vigilância Sanitária (Brazil) |
| JP | Japanese Pharmacopoeia |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the RTRT decision platform that produces real-time release decisions for continuous-manufacturing campaigns at Hesperia, in alignment with the regulator-approved control strategy and the ICH Q12 Established Conditions filing.

## 2. Scope

**In:** site-developed Python services on K8s; decision-rule engine; integrations with the continuous-mfg CRC (Ophir), NIR PAT (Faro), LIMS (raw-material results), Aspen IP.21 (historian), MasterControl (deviation linkage), Vault QualityDocs (control-strategy documents); Okta SSO; output to PAS-X for batch closure; QP electronic-signature gateway for EU batch release; Swissmedic / BfArM / AGES / ANVISA / PMDA filed-strategy alignment evidence.

**Out:** the consumer systems (each separately validated); regulatory filing of the control strategy (separate regulatory process).

## 3. System Description

The RTRT engine consumes per-batch real-time data from the CRC + NIR PAT + LIMS + IP.21 + raw-material attributes; applies the pre-approved decision rule per the regulatory-filed control strategy (ICH Q8 design space + ICH Q12 Established Conditions); produces a real-time release decision with full traceability (which inputs at which timestamps drove the decision). Out-of-design-space conditions trigger fallback to traditional release testing + deviation. Decision-rule versions pinned per filed control-strategy version. The QP retains ultimate authority for EU batch release per Directive 2001/83/EC Art. 51. Multi-jurisdiction filings are tracked (EU / CH / DE / AT / BR via ANVISA / JP via PMDA) and reconciled.

GAMP Cat 5: full SDLC + per-rule validation + regulatory filing alignment.

## 4. User Roles

| Role | Permissions |
|---|---|
| RTRT Engineer | Author / edit DRAFT decision rules. |
| Statistician / Chemometrician | Review + co-approve decision rules; PAT-model author. |
| PAT Model Owner | Author + lifecycle PAT models; co-approve PAT changes with Statistician. |
| Reg Affairs (RTRT) | Co-approve rule changes that touch the regulatory filing; manages multi-jurisdiction variation. |
| RTRT Approver (QA + Mfg Head + Reg Affairs) | Approve rule to EFFECTIVE. |
| Qualified Person (QP) | EU batch release authority for finished product; can override RTRT decision. |
| QP Substitute | Backup QP per Directive 2001/83/EC; recorded in MA. |
| Mfg Operator | View real-time decisions; cannot edit rules. |
| RTRT Administrator | Configure platform; cannot approve rules. |
| Auditor | Read-only. |
| Inspection-Read-Only | Time-bound read-only for regulator inspection. |

Standard SoD; rule changes that fall outside the filed regulatory range require a regulatory variation before approval. QP retains independent authority per Directive 2001/83/EC.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` direct GxP impact / `R2` indirect / `R3` none).

### 5.1 Application Lifecycle (Cat 5 SDLC)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEV-01 | H | R1 | SDLC: code review, unit tests (≥ 90% coverage on rule-execution modules), integration tests, regression suite, statistical sign-off, regulatory-affairs sign-off for rule changes. |
| URS-DEV-02 | H | R1 | Source shall reside in validated GitLab; signed commits; pinned dependencies. |
| URS-DEV-03 | H | R1 | Container images shall be signed; deployment via approved CR; rollback runbook tested. |
| URS-DEV-04 | H | R1 | Site-developed code shall maintain ≥ 95% deterministic behaviour for the decision-rule engine; floating-point reproducibility verified per OQ. |
| URS-DEV-05 | H | R1 | Static analysis (Ruff, mypy --strict, Bandit) + dependency scanning + SAST run on every CI build; criticals block. |
| URS-DEV-06 | H | R1 | Container images shall be scanned for HIGH / CRITICAL CVEs; criticals block deployment. |
| URS-DEV-07 | M | R2 | Release manifest shall include FS / DS / CS deltas + regression report + CR ID. |

### 5.2 Decision Rule Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RULE-01 | H | R1 | Each decision rule shall be pinned to a filed control-strategy version; out-of-filing rule changes shall require regulatory variation per ICH Q12. |
| URS-RULE-02 | H | R1 | Rule lifecycle: DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE. State transitions shall require signed change records. |
| URS-RULE-03 | H | R1 | Approval shall require QA + Mfg Head + Reg Affairs signatures. |
| URS-RULE-04 | H | R1 | Each rule shall carry an ICH Q12 Established-Conditions classification (CMA / CPP / CQA) and the regulator-approved adjustment range. |
| URS-RULE-05 | M | R2 | Rule changes within the filed range shall require notification only; changes outside shall trigger variation submission per ICH Q12. |
| URS-RULE-06 | H | R1 | A rule's filed range may differ per jurisdiction; the rule shall record per-jurisdiction approved ranges and the runtime shall enforce the most-restrictive range when multiple markets are in scope. |

### 5.3 Run Execution and Decision

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RUN-01 | H | R1 | Each release decision shall capture: batch-id, rule-id + version, all input snapshots (PAT predictions, IP data, raw-material attributes, control-strategy doc references) with timestamps, decision (release / hold / out-of-design-space), confidence interval. |
| URS-RUN-02 | H | R1 | A pre-decision validator shall check input completeness and freshness; failure shall flip the batch to fallback (traditional testing) with documented reason. |
| URS-RUN-03 | H | R1 | Out-of-design-space conditions shall trigger automatic deviation in MasterControl plus revert to traditional release. |
| URS-RUN-04 | H | R1 | The decision shall be gated by re-authenticated QA-Approver electronic signature; auto-approve for in-design-space decisions shall be permitted only if regulator-approved per the filed control strategy. |
| URS-RUN-05 | H | R1 | The QP shall have authority to override the RTRT decision for any batch; QP override shall require re-authenticated signature with reason. |
| URS-RUN-06 | M | R2 | Decision reconstruction shall be possible from logged inputs + code-version + rule-version + PAT-model-version. |

### 5.4 Audit Trail and Records Management

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | A contemporaneous, time-stamped audit trail shall capture user, action, old value, new value, reason-for-change for all rule lifecycle transitions, release decisions, QP overrides, and configuration changes. |
| URS-AUD-02 | H | R1 | The audit trail shall not be editable or deletable by any user, including Platform Administrators. |
| URS-AUD-03 | H | R1 | Audit-trail entries for release decisions shall include the full decision-input snapshot pointer so the decision is reconstructable from source data. |
| URS-AUD-04 | H | R1 | Retention shall be ≥ 25 years for batch release records per EU GMP Chapter 4. |
| URS-AUD-05 | M | R2 | Audit-trail review shall be performed event-driven (per batch) by the QA reviewer and quarterly by the QA team. |

### 5.5 21 CFR Part 11 Compliance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a), procedures and controls shall protect the validity of release records and the decision-rule store. |
| URS-PART11-02 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via Okta SSO + MFA. |
| URS-PART11-03 | H | R1 | Per § 11.10(e), an operational audit trail per § 5.4 shall exist. |
| URS-PART11-04 | H | R1 | Per § 11.50, electronic signatures shall include signer's printed name, date and time, and meaning of signature. |
| URS-PART11-05 | H | R1 | Per § 11.70, signatures shall be cryptographically linked to the signed record; subsequent record changes shall invalidate the signature. |
| URS-PART11-06 | H | R1 | Per § 11.100, signatures shall be unique per individual; reuse / reassignment blocked. |
| URS-PART11-07 | H | R1 | Per § 11.200, re-authentication shall be required at the moment of QP signing. |
| URS-PART11-08 | H | R1 | Per § 11.300, password / credential controls per site InfoSec policy. |

### 5.6 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | **Attributable:** Every release decision shall be attributable to a named QA Approver and named QP (if applicable). |
| URS-DI-02 | H | R1 | **Legible:** Decision records exportable as human-readable PDF + machine-readable JSON. |
| URS-DI-03 | H | R1 | **Contemporaneous:** Decisions recorded at the time of input-data convergence. |
| URS-DI-04 | H | R1 | **Original:** PAT prediction + IP data + raw-material data preserved unaltered; derivative analyses reference but do not overwrite. |
| URS-DI-05 | H | R1 | **Accurate:** Decision-rule arithmetic shall be deterministic and validated under OQ. |
| URS-DI-06 | M | R2 | **Complete / Consistent / Enduring / Available:** ≥ 25-year retention; retrievable within 1 business day. |

### 5.7 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-CRC-01 | H | R1 | Ophir CRC bidirectional integration; CRC state pulled into decision input snapshot. |
| URS-INT-PAT-01 | H | R1 | Faro NIR PAT predictions consumed with model-version-pin per the filed control strategy. |
| URS-INT-LIMS-01 | H | R1 | LIMS raw-material attributes pulled with QC release status. |
| URS-INT-HIST-01 | H | R1 | Aspen IP.21 historical data accessible for batch reconstruction. |
| URS-INT-VAULT-01 | H | R1 | Vault QualityDocs control-strategy document references resolved at decision time. |
| URS-INT-EQMS-01 | H | R1 | Out-of-design-space deviations pushed to MasterControl with bi-directional linkage. |
| URS-INT-MES-01 | H | R1 | Release decision pushed to PAS-X for batch closure. |
| URS-INT-QP-01 | H | R1 | QP electronic-signature gateway for EU batch release per Directive 2001/83/EC. |
| URS-INT-REG-01 | H | R1 | Regulatory-reporting service shall be the canonical link to Swissmedic / EMA / BfArM / AGES / ANVISA / PMDA variation submissions. |

### 5.8 Performance and Availability

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | Decision rendering shall complete ≤ 60 seconds after the final input arrives, P95. |
| URS-PERF-02 | M | R2 | The platform shall sustain ≥ 10 decisions/minute across all campaigns. |
| URS-AV-01 | H | R1 | Availability ≥ 99.9% during campaigns; planned maintenance only during scheduled production-down windows. |
| URS-AV-02 | M | R2 | The platform shall auto-scale between 2 and 16 worker pods. |

### 5.9 Backup, Restore, and Disaster Recovery

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | Decision records, audit logs, and rule store shall be backed up daily with cryptographic integrity verification. |
| URS-BAK-02 | H | R1 | A documented restore test shall be performed quarterly with QA witness. |
| URS-BAK-03 | M | R2 | RTO ≤ 4 hours; RPO ≤ 15 minutes. |
| URS-BAK-04 | M | R2 | DR failover shall be tested annually with a tabletop exercise plus a live partial failover. |

### 5.10 Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | The platform shall be hardened per CIS Kubernetes benchmark; non-conformities tracked under change control. |
| URS-SEC-02 | H | R1 | Secrets (DB credentials, signing keys, integration tokens) shall be stored in HashiCorp Vault with audit logging. |
| URS-SEC-03 | H | R1 | Container images shall be scanned for CVEs at build time and runtime; HIGH and CRITICAL CVEs shall block deployment. |
| URS-SEC-04 | M | R2 | Pod Security Standards (restricted) shall be enforced; NetworkPolicies shall isolate the rule-execution namespace. |

### 5.11 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Role-specific training in the site LMS shall be completed before access; QA Approver and QP shall complete RTRT-specific training including fallback scenarios. |
| URS-TRN-02 | M | R2 | Annual refresher training shall cover ICH Q12 / Q13 updates and control-strategy variations. |
| URS-PR-01 | H | R1 | Annual periodic review shall cover rule inventory, control-strategy alignment, fallback evidence, deviation summary, audit-trail review, training currency, and regulatory variation log; signed by RTRT Lead + VP QA + VP Reg Affairs + QP. |
| URS-PR-02 | H | R1 | Variation submission events to Swissmedic / EMA / BfArM / AGES / ANVISA / PMDA shall be logged and tracked through approval; production rules shall be updated only after variation is approved per jurisdiction. |

### 5.12 ANVISA + JP Multi-Jurisdiction Cross-Reference

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MJR-01 | H | R1 | The platform shall record per-jurisdiction control-strategy filings for EU (centralised via EMA), CH (Swissmedic), DE (BfArM), AT (AGES), BR (ANVISA RDC 1/2024), JP (PMDA per JP General Information G6 RTRT). |
| URS-MJR-02 | H | R1 | Production rules shall be tagged with the list of jurisdictions in which they are approved EFFECTIVE; rules without active approval in a target market shall not be applied for batches destined to that market. |
| URS-MJR-03 | H | R1 | Variation submission state machine: SUBMITTED → UNDER_REVIEW → APPROVED → IMPLEMENTED → OBSOLETE per jurisdiction; production rule may not be promoted to EFFECTIVE in a jurisdiction until that jurisdiction's variation is APPROVED. |
| URS-MJR-04 | M | R2 | The platform shall export periodic per-jurisdiction filing summaries for regulatory affairs. |

### 5.13 ICH Q10 PQS Linkage

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PQS-01 | H | R1 | The platform shall integrate with the site ICH Q10 PQS: deviation linkage to MasterControl, CAPA linkage, change-control linkage, management-review reporting. |
| URS-PQS-02 | H | R1 | Out-of-design-space decisions, QP overrides, fallback events shall be reportable as PQS metrics in the site Management Review cadence. |
| URS-PQS-03 | M | R2 | Continuous-improvement learnings from RTRT performance trends shall be surfaced via PR-01 to feed the PQS. |

### 5.14 PAT Model Lifecycle Binding

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PMOD-01 | H | R1 | PAT models consumed from Faro NIR shall be lifecycle-managed: DRAFT → CALIBRATED → CROSS-VALIDATED → APPROVED → EFFECTIVE → OBSOLETE; each state transition signed by Statistician + PAT Model Owner + QA. |
| URS-PMOD-02 | H | R1 | The EFFECTIVE PAT-model version shall be pinned by the EFFECTIVE rule; runtime shall reject any PAT prediction from a non-matching model version. |
| URS-PMOD-03 | H | R1 | PAT-model performance shall be monitored on-line (residual / Hotelling T² / Q-statistic per ASTM E2476); out-of-statistical-control conditions shall trigger fallback to traditional release for the affected batches. |
| URS-PMOD-04 | M | R2 | PAT-model retraining cadence shall be documented in the model-management plan; retraining outputs shall enter the lifecycle workflow as DRAFT. |
| URS-PMOD-05 | M | R2 | Regulator-impacting PAT-model changes shall be linked to per-jurisdiction variation per URS-MJR-03. |

### 5.15 Control-Strategy File-Version Reconciliation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CS-01 | H | R1 | The control-strategy filing pack (Vault QualityDocs) shall be referenced by URN with version at decision time; document version pinned in the decision record. |
| URS-CS-02 | H | R1 | A scheduled reconciliation job shall compare deployed EFFECTIVE rules against the filed pack; divergence shall raise a critical PQS event. |
| URS-CS-03 | M | R2 | Reconciliation evidence shall be available at PR-01 review. |

### 5.16 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem for general roles and ADCS-issued QP certificates for the Qualified Person release-decision signature; conditional-access policy `Release-Decision Conditional Access (FIDO2 + ADCS QP-certificate hardware-token enforcement)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the RTRT decision-engine store plus file-level capture of model artefacts pinned per batch; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 15 y (batch-release record) per the consuming-record schedule. |

### 5.17 Cross-System Integration — Lyrae NIR PAT + Helios audit-trail

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-LYR-01 | H | R1 | NIR PAT prediction models used for real-time release decisioning shall be served exclusively via the Lyrae AI/ML Model Server (`LYR-URS-MLSRV-001`) so that platform-level EU AI Act Annex I controls (Art. 9 risk, Art. 10 data governance, Art. 11 + Annex IV pack, Art. 12 logging, Art. 14 human oversight, Art. 15 robustness, Art. 17 QMS, Art. 72 PMM, Art. 73 incident) apply uniformly; direct serving of NIR models from a non-Lyrae runtime shall be prohibited for GxP batch-release decisions. |
| URS-XINT-LYR-02 | H | R1 | The RTRT decision engine shall enforce a per-prediction inference SLO of P95 ≤ 750 ms and P99 ≤ 2000 ms for the NIR PAT model; SLO breach shall down-grade the batch from RTRT to conventional release per the ICH Q14 / Q9(R1) risk-based fallback and shall raise a deviation in `TLB-URS-EQMS-001`. |
| URS-XINT-LYR-03 | H | R1 | The QP release decision step shall retrieve the served model's model card and PCCP change envelope from Lyrae (per Lyrae URS-PCCP-* and URS-CARD-*) and shall block release if the served model_version is outside the approved PCCP envelope or if the model card's intended-use clause does not include NIR PAT release decisioning for the batch's product / strength / route. |
| URS-XINT-LYR-04 | H | R1 | Drift signal from Lyrae (population-stability index, prediction-distribution shift, ground-truth lag) shall be ingested via the Lyrae drift webhook within 1 minute and shall trigger a per-batch safety-net override (force conventional release) when the documented drift threshold per `LYR-URS-MLSRV-001` URS-DRIFT-* is exceeded; override evidence shall be retained ≥ 15 y with the batch-release record. |
| URS-XINT-LYR-05 | H | R1 | Inference events emitted to the RTRT decision engine (request, response, model_version, confidence, drift_flag, batch_id, qp_user) shall be forwarded to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract (JSON Lines, schema-versioned) within 5 minutes; Helios shall be the system-of-record for audit-trail review of NIR PAT inference events on release-bound batches. |

### 5.18 Cross-System Integration — Helios audit-trail handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HEL-01 | H | R1 | Hesperia RTRT shall publish audit-trail events (PAT instrument-level audit events (NIR scan, prediction, QP-decision) plus QP-certificate signature events) to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract (JSON Lines, schema-registry pinned, Kafka topic `helios.ingest.hesperia.rtrt.v1`) within 5 minutes of event capture; 21 CFR § 11.10(e) audit-trail completeness shall be preserved end-to-end so that no event class is lost at the boundary. |
| URS-XINT-HEL-02 | H | R1 | Pre-handover audit-trail retention on the Hesperia RTRT side shall be ≥ 15 y regardless of Helios availability; once Helios acknowledges ingest (per-message ack with idempotency key), Helios is the system-of-record for review and the Hesperia RTRT local copy serves as the durability backstop until the local retention floor expires. |

### 5.19 Cross-System Integration — Caelum LIMS sample data flow

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-LIMS-01 | H | R1 | Sample-level analytical results (release-relevant tests not covered by PAT) consumed by the RTRT decision engine shall be retrieved from the Caelum LIMS (`CTX-URS-LIMS-001`) via the LIMS approved-result feed; the RTRT engine shall reject sample data that are not in the LIMS APPROVED state at the time of release decision. |
| URS-XINT-LIMS-02 | H | R1 | The release-decision dossier shall pin the LIMS result IDs and approval e-signature timestamps for every consumed sample; subsequent LIMS-side amendment of a pinned result shall raise a deviation in `TLB-URS-EQMS-001` and shall require the QP to re-evaluate the affected batch. |

### 5.20 Cross-System Integration — Veridian MES PAS-X handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-MES-01 | H | R1 | RTRT batch-release signal (`approve` / `reject` / `quarantine`) shall be transmitted to the Veridian MES PAS-X (`VBM-URS-MES-001`) via the MES batch-release channel `veridian.batch.release.v1` with idempotency on `{batch_id, release_decision_id}`; the MES shall be the system-of-record for the post-release batch disposition (shipment, hold, recall trigger). |
| URS-XINT-MES-02 | H | R1 | Pre-release context required by the RTRT engine (batch master record, in-process control values, batch genealogy) shall be retrieved from the MES via the MES context API; pinned MES record IDs and version hashes shall be persisted in the release-decision dossier. |

## 6. Acceptance Criteria

1. CS, RA, IQ, OQ, PQ approved and executed (full Cat-5 set + regulatory alignment per ICH Q12).
2. PQ shall include representative end-to-end campaign with: (a) in-design-space decision with auto-approve, (b) out-of-design-space scenario with fallback + deviation, (c) post-deviation re-evaluation, (d) QP override of RTRT decision, (e) regulatory variation impact on rule execution, (f) multi-jurisdiction scenario where rule is approved in EU but pending in BR.
3. VSR approved by VP QA + VP Reg Affairs + Head of Continuous Manufacturing + QP.
4. RTM shall demonstrate every URS requirement mapped to at least one approved test case.
5. ICH Q12 Established-Conditions filing pack reconciled against deployed rule set.
6. PAT-model lifecycle traceability verified end-to-end.

## 7. Constraints

- SDLC enforced per ICH Q9(R1) and GAMP 5 Cat 5; regulatory-filing alignment per ICH Q12.
- Rule changes outside the filed control strategy shall require regulatory variation approval before EFFECTIVE.
- The QP shall retain independent batch-release authority per Directive 2001/83/EC Art. 51; no system override of QP authority is permitted.
- ICH Q13 continuous-manufacturing principles shall be applied to the operating regime.
- Multi-jurisdiction filings tracked per § 5.12.

## 8. Assumptions

- Ophir CRC, Faro PAT, LIMS, Aspen IP.21, Vault, MasterControl, PAS-X, Okta, HashiCorp Vault are themselves qualified.
- Control-strategy is filed and approved by the relevant competent authorities (Swissmedic for CH-market, EMA centralised for EU, FDA for US, ANVISA for BR, PMDA for JP).
- The QP is qualified per Directive 2001/83/EC Art. 49 and is named in the marketing authorisation.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- FDA *Guidance for Industry: Real-Time Release Testing* (2018).
- FDA *Guidance on Q13: Continuous Manufacturing of Drug Substances and Drug Products* (2024).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11 — Computerised Systems.
- EU GMP Chapter 4 — Documentation.
- Directive 2001/83/EC Art. 51 — Qualified Person obligations.
- EMA *Reflection Paper on Real-Time Release Testing* (2012).

### DACH-specific
- **Swissmedic (CH)** — guidance on continuous manufacturing and RTRT.
- **BfArM (DE)** — Bundesinstitut für Arzneimittel und Medizinprodukte.
- **AGES (AT)** — Österreichische Agentur für Gesundheit und Ernährungssicherheit.

### Latin America + Asia
- **ANVISA (BR)** — RDC 1/2024 (post-approval changes), continuous-manufacturing framework.
- **PMDA (JP)** — *Japanese Pharmacopoeia General Information G6 — Real-Time Release Testing*.

### International — ICH
- ICH Q8(R2) — Pharmaceutical Development.
- ICH Q9(R1) — Quality Risk Management.
- ICH Q10 — Pharmaceutical Quality System.
- ICH Q11 — Development and Manufacture of Drug Substances.
- ICH Q12 — Technical and Regulatory Considerations for Pharmaceutical Product Lifecycle Management.
- ICH Q13 — Continuous Manufacturing of Drug Substances and Drug Products.
- ICH Q14 — Analytical Procedure Development.

### ISPE / Industry
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE GAMP Good Practice Guide: *Process Analytical Technology*.
- ISPE *Real-Time Release Testing* Good Practice Guide.
- ASTM E2476 — Multivariate Statistical Process Control.
- PIC/S PI 041.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

