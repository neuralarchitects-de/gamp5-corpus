---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (FS catch-up to v1.2 URS — T3 uplift: MJR + PQS + PMOD + CS reconciliation)"
seed_corpus_basis:
  - "HSP2-URS-RTRT-001 v1.2 (parent URS)"
  - "GAMP 5 Cat 5"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "ICH Q8/Q9/Q10/Q11/Q12/Q13/Q14"
  - "FDA RTRT (2018); FDA Q13 (2024); EMA RTRT Reflection Paper (2012)"
  - "Directive 2001/83/EC Art. 51"
  - "Swissmedic; BfArM; AGES; ANVISA RDC 1/2024; PMDA JP G6"
parent_urs:
  document_number: HSP2-URS-RTRT-001
  version: "1.2"
  file: "../../URS/_generated/final/Real_Time_Release_Testing_Platform__Hesperia_BioPharma_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# Functional Specification (FS)

## Real-Time Release Testing (RTRT) Platform — Site-Developed Python on K8s + Decision-Rule Engine

**Document Number:** HSP2-FS-RTRT-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** HSP2-URS-RTRT-001 v1.2 | **Site:** Hesperia BioPharma AG, Visp, Switzerland *(fictional)*
**System Class:** GAMP Cat 5 — Custom Application
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11; ICH Q8(R2), Q9(R1), Q10, Q11, Q12, Q13, Q14; FDA RTRT Guidance (2018); FDA Q13 Guidance (2024); Directive 2001/83/EC Art. 51 (QP); Swissmedic (CH); BfArM (DE); AGES (AT); ANVISA RDC 1/2024 (BR); PMDA JP G6 (JP).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (RTRT Lead) | _____________ | _____________ | _____ |
| Reviewer (Statistician / Chemometrician) | _____________ | _____________ | _____ |
| Reviewer (PAT Model Owner) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Reg Affairs — RTRT Filing) | _____________ | _____________ | _____ |
| Reviewer (Qualified Person — EU Batch Release) | _____________ | _____________ | _____ |
| Approver (Head of Continuous Manufacturing) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |
| Approver (VP Regulatory Affairs) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.1: QP override; ICH Q12 EC classification; determinism verification; full Part 11 sub-section bindings; Visp deployment. |
| 1.2 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.2: ANVISA + PMDA multi-jurisdiction + ICH Q10 PQS linkage + PAT-model lifecycle binding + control-strategy file-version reconciliation added; all URS-IDs explicit row in §4 + §8. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies implementation of the RTRT decision platform to satisfy `HSP2-URS-RTRT-001` v1.2, including v1.2 additions for multi-jurisdiction filing tracking (EU / CH / DE / AT / BR / JP), ICH Q10 PQS linkage, PAT model lifecycle, and control-strategy reconciliation.

## 2. Scope

Site-developed Python services on K8s; decision-rule engine; integrations with Ophir CRC, Faro PAT, LIMS, Aspen IP.21, MasterControl, Vault QualityDocs; output to PAS-X; QP electronic-signature gateway; regulatory-reporting service for Swissmedic + BfArM + AGES + ANVISA + PMDA variation tracking.

## 3. System Architecture

```
   Ophir CRC + Faro PAT + LIMS + IP.21 + Vault
            │
            ▼
   ┌──────────────────────────────────────────┐
   │   RTRT Decision Engine (Cat 5 Python)    │
   │   ┌────────────────────────────────────┐ │
   │   │ ICH Q12 EC-classified rule store    │ │
   │   │ Multi-jurisdiction filing pin       │ │
   │   │ PAT-model lifecycle store           │ │
   │   │ Filing-pinned rule loader           │ │
   │   │ Determinism-verified arithmetic     │ │
   │   │ CS-pack reconciliation              │ │
   │   └────────────────────────────────────┘ │
   └────────────────┬──────────┬──────────────┘
                    │          │
                    ▼          ▼
              PAS-X        MasterControl
              (release)    (deviation / CAPA / PQS metrics)
                    │
                    ▼
              QP Signature Gateway
              (Art. 51 Directive 2001/83/EC)
                    │
                    ▼
              Regulatory-Reporting Service
              (Swissmedic / EMA / BfArM / AGES / ANVISA / PMDA)
```

## 4. Functional Specifications

### 4.1 Application Lifecycle / SDLC (URS §5.1)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DEV-01 | URS-DEV-01 | Cat-5 SDLC: code review (≥ 2 reviewers), unit tests ≥ 90% on rule-execution modules, integration tests, regression suite, statistical sign-off, reg-affairs sign-off. |
| FS-DEV-02 | URS-DEV-02 | Source in validated GitLab; GPG-signed commits; pinned dependencies. |
| FS-DEV-03 | URS-DEV-03 | Container images signed via cosign; ArgoCD GitOps deployment; rollback runbook quarterly-tested. |
| FS-DEV-04 | URS-DEV-04 | Determinism verification: OQ pins random seed, repeats decision 1000× on canonical input set, requires bitwise reproducibility. Floating-point reproducibility validated via `decimal` for currency-class math + IEEE-754 round-mode pin. |
| FS-DEV-05 | URS-DEV-05 | CI runs Ruff + mypy --strict + Bandit + Snyk + Trivy; criticals block. |
| FS-DEV-06 | URS-DEV-06 | Container CVE gate: HIGH / CRITICAL block promotion via OPA-policy in ArgoCD. |
| FS-DEV-07 | URS-DEV-07 | Release manifest `manifest.yaml` lists FS / DS / CS deltas + regression summary + CR ID. |

### 4.2 Decision Rule Lifecycle (URS §5.2)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RULE-01 | URS-RULE-01 | Decision rule pinned to filed control-strategy version via `control_strategy_version` foreign key; out-of-filing rule loads rejected. |
| FS-RULE-02 | URS-RULE-02 | Rule state machine DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE; transitions signed. |
| FS-RULE-03 | URS-RULE-03 | Approval requires 3 signed JWTs (QA + Mfg Head + Reg Affairs). |
| FS-RULE-04 | URS-RULE-04 | ICH Q12 Established-Conditions classification field: `ec_class` (CMA / CPP / CQA) + `approved_range_min` / `approved_range_max`. |
| FS-RULE-05 | URS-RULE-05 | Variation classifier: within-range changes → notification only; out-of-range → variation-submission gate to Swissmedic / BfArM / AGES / ANVISA / PMDA via the regulatory-reporting service. |
| FS-RULE-06 | URS-RULE-06 | Rule schema `approved_ranges_per_jurisdiction` (map jurisdiction → range); runtime enforces most-restrictive range when batch destined to multiple markets. |

### 4.3 Run Execution and Decision (URS §5.3)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RUN-01 | URS-RUN-01 | Decision record schema: `batch_id`, `rule_id`, `rule_version`, `input_snapshots[]` (PAT, IP, raw-material, doc-refs), `timestamps_iso8601[]`, `decision` (release/hold/oos), `confidence_interval`. |
| FS-RUN-02 | URS-RUN-02 | Pre-decision validator: input completeness (all required fields present) + freshness (within configured staleness window); failure → fallback flag + audit-logged reason. |
| FS-RUN-03 | URS-RUN-03 | Out-of-design-space detection on input vs `ec_class` ranges; OOS auto-creates MasterControl deviation via API + reverts to traditional release. |
| FS-RUN-04 | URS-RUN-04 | Re-auth QA-Approver e-signature for decision approval; auto-approve only when `auto_approve_in_design=true` per filed control strategy. |
| FS-RUN-05 | URS-RUN-05 | QP override endpoint `POST /decision/{id}/override` with re-auth + reason; QP override final and audit-logged. |
| FS-RUN-06 | URS-RUN-06 | Decision-reconstruction tool `rtrt-reconstruct` reads logged inputs + versions; reproduces decision deterministically. |

### 4.4 Audit Trail and Records Management (URS §5.4)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit-trail schema: actor, action, old/new value, reason, timestamp; covers rule lifecycle, decisions, QP overrides, config changes. |
| FS-AUD-02 | URS-AUD-02 | Append-only DB trigger; Platform Admin cannot UPDATE / DELETE. |
| FS-AUD-03 | URS-AUD-03 | Decision audit entries include `input_snapshot_pointer` (S3 URI) for reconstruction from source data. |
| FS-AUD-04 | URS-AUD-04 | Retention ≥ 25 y per EU GMP Chapter 4; archive-tier enforcement. |
| FS-AUD-05 | URS-AUD-05 | Event-driven review per batch by QA + quarterly review by QA team. |

### 4.5 21 CFR Part 11 (URS §5.5)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural controls protecting electronic-record validity documented in `/sop/`; reviewed annually. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(d): access limited to authorised individuals via Okta SAML 2.0 + MFA; service accounts via mTLS only. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(e): operational audit trail capturing user, action, date, time — implemented via FS-AUD-01. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.50: electronic signatures include signer's printed name, date and time of signing, and meaning of signature; schema enforced in DB. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.70: signatures cryptographically linked to the signed record via HMAC-SHA256 over record-hash + signer-id + timestamp; tampered records flagged on read. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.100: signature unique per individual; reuse / reassignment blocked at provisioning via Okta-DB uniqueness constraint. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.200: re-authentication required at the moment of signing (fresh OAuth2 token, max-age 5 min); cached credentials rejected. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.300: password policy ≥ 14 chars + complexity + rotation + MFA per InfoSec policy. |

### 4.6 Data Integrity (URS §5.6)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | **Attributable:** every action / entry carries `actor_id` (named user or service-account); DB constraint not-null at audit-write. |
| FS-DI-02 | URS-DI-02 | **Legible:** records exportable as PDF/A-3 + machine-readable JSON/XML; rendering verified via OQ. |
| FS-DI-03 | URS-DI-03 | **Contemporaneous:** event timestamps server-side + NTP-synced; retroactive entries flagged with delay reason. |
| FS-DI-04 | URS-DI-04 | **Original:** raw inputs / records preserved in immutable storage; derivative analyses reference but do not overwrite the original. |
| FS-DI-05 | URS-DI-05 | **Accurate:** calculations / transformations deterministic and validated under OQ; floating-point reproducibility verified where applicable. |
| FS-DI-06 | URS-DI-06 | **Complete / Consistent / Enduring / Available:** metadata completeness validated; chronological order DB-enforced; retention per applicable regulation; retrievable within 1 business day. |

### 4.7 Integrations (URS §5.7)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-CRC-01 | URS-INT-CRC-01 | Ophir CRC bidirectional via REST+webhook; state pulled into decision input. |
| FS-INT-PAT-01 | URS-INT-PAT-01 | Faro NIR PAT predictions consumed via gRPC; model-version pin per filed control strategy enforced at consumption. |
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | LIMS raw-material API; only `QC_RELEASED` materials accepted. |
| FS-INT-HIST-01 | URS-INT-HIST-01 | Aspen IP.21 PI-tag read API; historical data for batch reconstruction. |
| FS-INT-VAULT-01 | URS-INT-VAULT-01 | Vault QualityDocs URN-resolved at decision time; document version pinned in decision record. |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | MasterControl deviation push for OOS conditions; bi-directional linkage. |
| FS-INT-MES-01 | URS-INT-MES-01 | PAS-X batch-closure API; decision pushed with full audit context. |
| FS-INT-QP-01 | URS-INT-QP-01 | QP signature gateway (separate service) enforcing Art. 51 obligations; QP override-of-RTRT logged. |
| FS-INT-REG-01 | URS-INT-REG-01 | Regulatory-reporting service implements per-jurisdiction state machine; integration over signed REST; per-CA endpoint mapped in `reg_reporting_config.yaml`. |

### 4.8 Performance + Availability (URS §5.8)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | Decision-render latency P95 ≤ 60 s; Prometheus histogram tracked. |
| FS-PERF-02 | URS-PERF-02 | ≥ 10 decisions/minute sustained across campaigns; load-tested via k6. |
| FS-AV-01 | URS-AV-01 | Availability ≥ 99.9% during campaigns. |
| FS-AV-02 | URS-AV-02 | HPA scales worker pods 2–16 on queue depth. |

### 4.9 Backup / DR (URS §5.9)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BAK-01 | URS-BAK-01 | Daily backup with integrity verification (HMAC-SHA256). |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore-test scripted; QA witness sign-off. |
| FS-BAK-03 | URS-BAK-03 | RTO ≤ 4 h; RPO ≤ 15 min monitored. |
| FS-BAK-04 | URS-BAK-04 | Annual DR test combining tabletop + live partial failover. |

### 4.10 Security (URS §5.10)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SEC-01 | URS-SEC-01 | CIS K8s benchmark applied; non-conformities tracked in CR register. |
| FS-SEC-02 | URS-SEC-02 | HashiCorp Vault for secrets; audit logging enabled. |
| FS-SEC-03 | URS-SEC-03 | Trivy CVE scan in CI + runtime; HIGH / CRITICAL block. |
| FS-SEC-04 | URS-SEC-04 | Pod Security `restricted` + NetworkPolicy isolation for `rtrt-prod` namespace. |

### 4.11 Training / Periodic Review (URS §5.11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | LMS-recorded role-specific training; QA Approver + QP require RTRT-fallback training. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher `RTRT-2026-ANNUAL`: ICH Q12 / Q13 + control-strategy variations. |
| FS-PR-01 | URS-PR-01 | Annual Periodic Review (rule inventory + control-strategy alignment + fallback evidence + deviation summary + audit-trail review + training + variation log); signed by RTRT Lead + VP QA + VP Reg Affairs + QP. |
| FS-PR-02 | URS-PR-02 | Variation tracking gate: rules cannot be promoted to EFFECTIVE if pending variation not approved by relevant CA (Swissmedic / EMA / BfArM / AGES / ANVISA / PMDA). |

### 4.12 ANVISA + JP Multi-Jurisdiction (URS §5.12)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MJR-01 | URS-MJR-01 | `filing_registry` table records per-jurisdiction control-strategy filings with status, document refs, approval dates. |
| FS-MJR-02 | URS-MJR-02 | Rule schema `approved_jurisdictions[]`; runtime market-gate rejects rule application for batches destined to unapproved markets (raises `MJR_RULE_NOT_APPROVED_FOR_MARKET`). |
| FS-MJR-03 | URS-MJR-03 | Variation state machine `SUBMITTED → UNDER_REVIEW → APPROVED → IMPLEMENTED → OBSOLETE` per jurisdiction; promotion gate references state per market. |
| FS-MJR-04 | URS-MJR-04 | Periodic per-jurisdiction filing summary export endpoint `GET /reports/filings/{jurisdiction}` returns PDF/A-3 + JSON. |

### 4.13 ICH Q10 PQS Linkage (URS §5.13)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PQS-01 | URS-PQS-01 | PQS-linkage adapter posts deviation / CAPA / change-control events to MasterControl with bi-directional cross-reference. |
| FS-PQS-02 | URS-PQS-02 | OOS + QP-override + fallback events tagged for PQS Management Review report; surfaced via Grafana dashboard `HSP-GR-PQS-METRICS`. |
| FS-PQS-03 | URS-PQS-03 | PR-01 review template includes continuous-improvement-learnings section feeding PQS. |

### 4.14 PAT Model Lifecycle Binding (URS §5.14)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PMOD-01 | URS-PMOD-01 | PAT-model state enum in `pat_model_versions` table: `DRAFT / CALIBRATED / CROSS-VALIDATED / APPROVED / EFFECTIVE / OBSOLETE`; transitions require 3 signed JWTs (Statistician + PAT Model Owner + QA). |
| FS-PMOD-02 | URS-PMOD-02 | Runtime model-loader verifies `model_version == effective_rule.pat_model_version`; mismatch rejects prediction with `PAT_MODEL_VERSION_MISMATCH`. |
| FS-PMOD-03 | URS-PMOD-03 | `PatPerformanceMonitor` computes residual / Hotelling T² / Q-statistic per ASTM E2476; OOS for sustained window triggers `PAT_MODEL_OOS` → batches in flight fallback to traditional release. |
| FS-PMOD-04 | URS-PMOD-04 | Retraining outputs enter lifecycle as DRAFT; cadence documented in `pat_model_management_plan.md`. |
| FS-PMOD-05 | URS-PMOD-05 | PAT-model changes linked to per-jurisdiction variation via `variation_record_id` FK. |

### 4.15 Control-Strategy File-Version Reconciliation (URS §5.15)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CS-01 | URS-CS-01 | Decision record stores `cs_doc_urn` + `cs_doc_version` resolved from Vault QualityDocs at decision time. |
| FS-CS-02 | URS-CS-02 | Scheduled job `cs-reconcile` runs nightly; compares deployed EFFECTIVE rules vs filed pack; divergence raises critical PQS event + alerts QA + Reg Affairs. |
| FS-CS-03 | URS-CS-03 | Reconciliation evidence surfaced in PR-01 template under §"Control-strategy reconciliation"; signed by VP Reg Affairs. |


### 4.16 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem for general roles and ADCS-issued QP certificates for the Qualified Person release-decision signature. Conditional-access binding to policy `Release-Decision Conditional Access (FIDO2 + ADCS QP-certificate hardware-token enforcement)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the RTRT decision-engine store plus file-level capture of model artefacts pinned per batch; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.17 Cross-System Integration — Lyrae + Helios (M-XINT-LYR)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-LYR-01 | URS-XINT-LYR-01 | Inference-client adapter `HSP-LYR-CLIENT-1.x` enforces Lyrae-only model resolution: request payload carries `model_alias=NIR-PAT-<product>` and Lyrae returns the bound `model_version`; non-Lyrae endpoints rejected by the adapter; configuration item `CI-LYR-ENDPOINT` set to the Lyrae prod URL with mTLS + Entra workload-identity. |
| FS-XINT-LYR-02 | URS-XINT-LYR-02 | Inference SLO budget set to 750 ms P95 / 2000 ms P99 in `CI-LYR-SLO`; APM probe `apm-hsp-lyr-latency` alerts on 5-min P95 > 750 ms; SLO breach triggers state-machine transition `RTRT_FALLBACK` and creates MasterControl deviation via the eQMS event push channel. |
| FS-XINT-LYR-03 | URS-XINT-LYR-03 | Pre-release gate reads Lyrae `GET /models/{alias}/card` and `GET /models/{alias}/pccp/envelope`; gate evaluates: (a) `model_version ∈ approved_envelope`, (b) `intended_use ∋ {product, strength, route}`; gate result and full model-card + envelope JSON are pinned to the batch dossier. |
| FS-XINT-LYR-04 | URS-XINT-LYR-04 | Lyrae drift webhook subscribed via OIDC; payload schema `lyrae.drift.v1`; consumer rule engine evaluates PSI > 0.20 OR distribution-shift KS > threshold OR ground-truth lag > 7 d → safety-net override; override evidence packet `{batch_id, model_version, drift_metrics, override_user, override_ts}` written to the batch record. |
| FS-XINT-LYR-05 | URS-XINT-LYR-05 | Helios ingestion via Kafka topic `helios.ingest.rtrt.inference.v1` (JSON Lines, schema-registry pinned, Avro fallback); producer at-least-once with idempotency key `{batch_id, request_id}`; back-pressure monitored; pre-handover retention floor 2 y on the RTRT side before Helios becomes system-of-record. |


### 4.18 Cross-System Integration — Helios handover (M-XINT-HEL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HEL-01 | URS-XINT-HEL-01 | Audit-event publisher emits Kafka topic `helios.ingest.hesperia.rtrt.v1` with schema-registry-pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`; at-least-once delivery; idempotency key `{source_system, event_id}`; back-pressure surfaced via Prometheus `helios_publish_lag_seconds` with 5-min alert at > 600 s. |
| FS-XINT-HEL-02 | URS-XINT-HEL-02 | Local audit-store retention policy enforces ≥ 15 y; Helios ack persisted as `helios_ack_ts` per event; periodic reconciliation job verifies parity (Helios row count == local published count) and raises a deviation in MasterControl on > 0.01% mismatch over a 24 h window. |


### 4.19 Cross-System Integration — Caelum LIMS (M-XINT-LIMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-LIMS-01 | URS-XINT-LIMS-01 | LIMS read adapter `HSP-LIMS-READ-1.x` performs `GET /results?batch_id={batch_id}&state=APPROVED`; non-APPROVED rows filtered out at the adapter; release-decision API rejects on empty result-set or missing required test per the batch's release-specification. |
| FS-XINT-LIMS-02 | URS-XINT-LIMS-02 | Batch dossier persists `{lims_result_id, approval_ts, approval_user, approval_signature_hash}` for every consumed sample; LIMS amendment webhook `caelum.lims.result.amended.v1` subscribed; on receipt, deviation `HSP-LIMS-AMEND-AFTER-RELEASE` raised in MasterControl. |


### 4.20 Cross-System Integration — Veridian MES PAS-X (M-XINT-MES)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-MES-01 | URS-XINT-MES-01 | Release-signal publisher posts to MES endpoint `POST /batches/{batch_id}/release` with mTLS; payload `veridian.batch.release.v1`; idempotency on `{batch_id, release_decision_id}`; at-least-once delivery; DLQ at 10 attempts. |
| FS-XINT-MES-02 | URS-XINT-MES-02 | MES context adapter `HSP-MES-CTX-1.x` performs `GET /batches/{batch_id}/context?include=bmr,ipc,genealogy`; version-pin fields `{bmr_version, ipc_run_id, genealogy_hash}` persisted in the dossier. |

## 5. Configuration Items (CI)

| CI | Item | Value |
|---|---|---|
| CI-01 | Filing pinning | per ICH Q12 control strategy version |
| CI-02 | Out-of-design-space fallback | enforced (traditional release path) |
| CI-03 | Decision-render SLO | P95 ≤ 60 s |
| CI-04 | QP override | endpoint enabled per Directive 2001/83/EC Art. 51 |
| CI-05 | Determinism OQ | bitwise reproducibility on canonical input set |
| CI-06 | Variation-tracking gate | enabled per jurisdiction |
| CI-07 | Audit retention | ≥ 25 y |
| CI-08 | Multi-jurisdiction filings | EU, CH, DE, AT, BR (ANVISA), JP (PMDA) |
| CI-09 | PAT-model lifecycle | enabled |
| CI-10 | CS-pack reconciliation cadence | nightly |
| CI-11 | PQS linkage adapter | MasterControl bi-directional |

## 6. Risks (FS-level)

URS § 9 documents R-01..R-14. Additional FS risks:

- Floating-point non-determinism across pod restarts → mitigation: FS-DEV-04 + `decimal` for currency math + IEEE-754 round-mode pin
- Faro PAT model-version-pin bypass → mitigation: contract test in CI rejecting mismatched-version predictions (FS-PMOD-02)
- QP gateway certificate expiration → mitigation: cert-manager auto-renewal + monitoring
- Regulatory-reporting service outage → mitigation: queue-based retry + alerting + manual fallback to direct CA portal
- Multi-jurisdiction rule mis-tag (approved in EU but applied to BR) → mitigation: FS-MJR-02 market-gate + OQ scenario
- CS-pack reconciliation drift → mitigation: FS-CS-02 + critical PQS event + halt-promotion gate

## 7. References

- HSP2-URS-RTRT-001 v1.2.
- 21 CFR Part 11; EU GMP Annex 11; EU GMP Chapter 4.
- Directive 2001/83/EC Art. 51.
- ICH Q8(R2), Q9(R1), Q10, Q11, Q12, Q13, Q14.
- FDA RTRT Guidance (2018); FDA Q13 Guidance (2024); EMA Reflection Paper on RTRT (2012).
- Swissmedic (CH); BfArM (DE); AGES (AT); ANVISA RDC 1/2024 (BR); PMDA JP G6 (JP).
- ISPE GAMP 5 (2nd ed., 2022); ISPE *RTRT Good Practice Guide*; ISPE GAMP GPG *PAT*.
- ASTM E2476.
- PIC/S PI 041.

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-DEV-01 | FS-DEV-01 |
| URS-DEV-02 | FS-DEV-02 |
| URS-DEV-03 | FS-DEV-03 |
| URS-DEV-04 | FS-DEV-04 |
| URS-DEV-05 | FS-DEV-05 |
| URS-DEV-06 | FS-DEV-06 |
| URS-DEV-07 | FS-DEV-07 |
| URS-RULE-01 | FS-RULE-01 |
| URS-RULE-02 | FS-RULE-02 |
| URS-RULE-03 | FS-RULE-03 |
| URS-RULE-04 | FS-RULE-04 |
| URS-RULE-05 | FS-RULE-05 |
| URS-RULE-06 | FS-RULE-06 |
| URS-RUN-01 | FS-RUN-01 |
| URS-RUN-02 | FS-RUN-02 |
| URS-RUN-03 | FS-RUN-03 |
| URS-RUN-04 | FS-RUN-04 |
| URS-RUN-05 | FS-RUN-05 |
| URS-RUN-06 | FS-RUN-06 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
| URS-AUD-05 | FS-AUD-05 |
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
| URS-INT-CRC-01 | FS-INT-CRC-01 |
| URS-INT-PAT-01 | FS-INT-PAT-01 |
| URS-INT-LIMS-01 | FS-INT-LIMS-01 |
| URS-INT-HIST-01 | FS-INT-HIST-01 |
| URS-INT-VAULT-01 | FS-INT-VAULT-01 |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 |
| URS-INT-MES-01 | FS-INT-MES-01 |
| URS-INT-QP-01 | FS-INT-QP-01 |
| URS-INT-REG-01 | FS-INT-REG-01 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-AV-01 | FS-AV-01 |
| URS-AV-02 | FS-AV-02 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-BAK-03 | FS-BAK-03 |
| URS-BAK-04 | FS-BAK-04 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-PR-02 | FS-PR-02 |
| URS-MJR-01 | FS-MJR-01 |
| URS-MJR-02 | FS-MJR-02 |
| URS-MJR-03 | FS-MJR-03 |
| URS-MJR-04 | FS-MJR-04 |
| URS-PQS-01 | FS-PQS-01 |
| URS-PQS-02 | FS-PQS-02 |
| URS-PQS-03 | FS-PQS-03 |
| URS-PMOD-01 | FS-PMOD-01 |
| URS-PMOD-02 | FS-PMOD-02 |
| URS-PMOD-03 | FS-PMOD-03 |
| URS-PMOD-04 | FS-PMOD-04 |
| URS-PMOD-05 | FS-PMOD-05 |
| URS-CS-01 | FS-CS-01 |
| URS-CS-02 | FS-CS-02 |
| URS-CS-03 | FS-CS-03 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-LYR-01 | FS-XINT-LYR-01 |
| URS-XINT-LYR-02 | FS-XINT-LYR-02 |
| URS-XINT-LYR-03 | FS-XINT-LYR-03 |
| URS-XINT-LYR-04 | FS-XINT-LYR-04 |
| URS-XINT-LYR-05 | FS-XINT-LYR-05 |
| URS-XINT-HEL-01 | FS-XINT-HEL-01 |
| URS-XINT-HEL-02 | FS-XINT-HEL-02 |
| URS-XINT-LIMS-01 | FS-XINT-LIMS-01 |
| URS-XINT-LIMS-02 | FS-XINT-LIMS-02 |
| URS-XINT-MES-01 | FS-XINT-MES-01 |
| URS-XINT-MES-02 | FS-XINT-MES-02 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Rule executes outside filed range without variation | Medium | Critical | URS-RULE-01, URS-RULE-05, URS-RUN-03 |
| R-02 | Silent input gap leads to decision on incomplete data | Medium | Critical | URS-RUN-02 (completeness check) |
| R-03 | Decision-rule defect releases off-spec batch | Low | Critical | URS-DEV-01 (test coverage), URS-RULE-03 (multi-signature) |
| R-04 | Floating-point non-determinism produces inconsistent decisions | Low | High | URS-DEV-04 (determinism verification) |
| R-05 | Out-of-design-space not detected by validator | Low | Critical | URS-RUN-03 (deviation auto-trigger) |
| R-06 | QP override unavailable during production | Low | Critical | URS-RUN-05, URS-INT-QP-01 |
| R-07 | Audit-trail tampering by privileged user | Low | Critical | URS-AUD-02 |
| R-08 | Variation lag — rule effective before regulator approval | Low | High | URS-PR-02 (variation tracking gate), URS-MJR-03 |
| R-09 | PAT model drift consumed without re-validation | Medium | High | URS-PMOD-02 (model-version-pin), URS-PMOD-03 (T2/Q monitoring) |
| R-10 | Decision rendering latency exceeds campaign cycle time | Low | Medium | URS-PERF-01 |
| R-11 | Backup / restore failure during disaster | Low | High | URS-BAK-01, URS-BAK-02 |
| R-12 | Control-strategy document drift between filed + production references | Low | High | URS-INT-VAULT-01, URS-CS-02 |
| R-13 | Multi-jurisdiction rule application to wrong market | Low | Critical | URS-MJR-02 |
| R-14 | PAT model retraining bypasses lifecycle gates | Low | High | URS-PMOD-04 + statistician sign-off |

Full evaluation in `HSP2-RA-RTRT-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
