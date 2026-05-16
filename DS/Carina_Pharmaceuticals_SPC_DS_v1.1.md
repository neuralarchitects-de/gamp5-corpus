---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "CRN-FS-SPC-001 v1.2 (parent FS)"
  - "CRN-URS-SPC-001 v1.2 (parent URS — informational)"
  - "GAMP 5 (2nd ed.) Cat 4 — Configuration Specification conventions (JSL library as Cat 5 sub-component)"
  - "21 CFR Part 11; EU GMP Annex 11; ICH Q8/Q9/Q10/Q12; FDA Process Validation 2011 — Stage 3 CPV"
  - "ASTM E2587; ISO 7870; ISO 22514-2; USP <1010>"
  - "SAS Institute JMP 18 Pro Administrator Reference + JSL Language Reference"
parent_fs:
  document_number: CRN-FS-SPC-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Carina_Pharmaceuticals_SPC_FS_v1.3.md
parent_urs:
  document_number: CRN-URS-SPC-001
  version: 1.2
  file: ../../../URS/_generated/final/SPC_Statistical_Process_Control__Carina_Pharmaceuticals_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## SPC — JMP Statistical Discovery 18 Pro + Site JSL Library + Databricks + AVEVA PI + Vault + MasterControl

**Document Number:** CRN-DS-SPC-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** CRN-FS-SPC-001 v1.2 | **Parent URS:** CRN-URS-SPC-001 v1.2 *(informational)*
**Site:** Carina Pharmaceuticals (fictional)
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (JSL library treated as Cat 5 sub-component per § 8.1)
**Project Mode:** Configuration project on commercial product **JMP Statistical Discovery 18 Pro** with site-developed JSL library (Cat 5 sub-component), integrated with Databricks lakehouse, AVEVA PI Notifications, Veeva Vault QualityDocs, MasterControl eQMS, PAS-X MES.
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; ICH Q8(R2)/Q9(R1)/Q10/Q12; FDA Process Validation 2011 — Stage 3 CPV; ASTM E2587-22; ISO 7870-1/-2/-4/-6/-8; ISO 22514-2:2017; USP <1010>; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Statistician) | _____________ | _____________ | _____ |
| Reviewer (Process Engineer) | _____________ | _____________ | _____ |
| Reviewer (Data Engineer — Lakehouse) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Approver (System Owner — Head of Manufacturing) | _____________ | _____________ | _____ |
| Approver (Process Owner — Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T3 from parent URS+FS pair (CRN-URS-SPC-001 / CRN-FS-SPC-001 v1.2). DS covers 100/100 FS-IDs. JSL library Cat 5 sub-component design captured as mini-SDS in § 8.1. No FS-IDs deferred; no FS-IDs flagged vendor-internal at this iteration. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

DS-specific terms only.

| Term | Definition |
|---|---|
| JMP add-in | A JMP packaged extension (`.jmpaddin`) containing JSL scripts loaded into JMP via the Add-In Manager. |
| Signed JSL | JSL file accompanied by a cosign-style detached signature verified at load. |
| Phase 1 / Phase 2 | ISO 7870-2 / Western Electric distinction — Phase 1 establishes trial limits; Phase 2 monitors against locked limits. |
| ARL₀ | Average Run Length under in-control (no signal) conditions — used to gate rule activation. |
| CPV | Continued Process Verification — Stage 3 of FDA 2011 Process Validation. |
| `cv_*` table | Carina lakehouse table under the `cv` schema (Continued-Verification). |

## 1. Purpose

This DS specifies the technical configuration values, JSL library design, integration design, real-time alerting design, and workflow design that implement the functional behaviour defined in `CRN-FS-SPC-001` v1.2 — Stage 3 CPV across Carina commercial products.

## 2. Scope

In scope: JMP 18 Pro per-workstation configuration; site JSL library design (Cat 5 sub-component); Databricks lakehouse query design + version-control discipline; AVEVA PI Notifications design; Vault CPV-report workflow design; MasterControl eQMS deviation integration; PAS-X alarm integration; AD + SIEM + backup integration; role-permission matrix. Out of scope: JMP source-code internals (SAS Institute SDLC); Databricks platform internals; AVEVA PI System internals; Werum PAS-X internals; MasterControl internals; Vault internals.

## 3. Architectural Overview

### 3.1 Logical View

```
┌──────────────────────────────────────────────────────────────────┐
│  Sources: PAS-X · LIMS · EM · AVEVA PI System                     │
└─────────────────────────────┬────────────────────────────────────┘
                              │ documented, version-controlled queries
                              ▼
                ┌────────────────────────────┐
                │   Databricks Lakehouse      │
                │   `prod-lake-carina`        │
                │   tables: cv_*, genealogy.* │
                └──────────────┬──────────────┘
                               │
        ┌──────────────────────┼─────────────────────────┐
        │                      │                         │
        ▼                      ▼                         ▼
┌────────────────┐    ┌──────────────────┐    ┌─────────────────────┐
│ JMP 18 Pro     │    │ JSL Library      │    │ AVEVA PI            │
│ (Cat 3 COTS)   │    │ (Cat 5 site-dev) │    │ Notification engine │
│ analyst WSs    │    │ signed + tested  │    │ (real-time alerts)  │
└────────┬───────┘    └────────┬─────────┘    └──────────┬──────────┘
         │                     │                         │
         └────────┬────────────┴─────────────────────────┤
                  ▼                                      ▼
       ┌──────────────────────┐         ┌──────────────────────────┐
       │ Veeva Vault          │         │ PAS-X · MasterControl    │
       │ QualityDocs          │         │ (Production Alarms ·     │
       │ (signed CPV reports) │         │  deviation routing)      │
       └──────────────────────┘         └──────────────────────────┘
```

### 3.2 Deployment Topology

| Component | Host / Path | Version pin | Hardening |
|---|---|---|---|
| JMP 18 Pro | Site asset register `CRN-AR-WS-001` (controlled analyst WSs) | 18 Pro current SCN | GPO `GMP-Lab-Workstations` |
| JMP license server | `crn-jmp-lic-01` | 18 | Site-internal; concurrency enforced |
| Site JSL repo | GitLab `carina/spc-jsl` | per-tag | Sigstore gitsign signed commits; protected `main` |
| Databricks lakehouse | `prod-lake-carina.cloud.databricks` | runtime 14.3 LTS | OAuth2 client-credentials + HashiCorp Vault |
| AVEVA PI Notifications | `crn-pi-not-01` | PI 2024 | Site PKI + AD service account |
| Vault QualityDocs | Veeva SaaS | 24R1 | SaaS-native MFA + SSO |
| MasterControl eQMS | `crn-mc-01` | per SaaS | REST + idempotency |
| Werum PAS-X | `crn-pasx-01` | v3.2 | REST + AD service account |

## 4. Configuration Specification

`D = vendor default`; `C = site custom`.

### 4.1 JMP Deployment Configuration

| CI-ID | Configuration Item (vendor-named) | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-DEP-01 | JMP workstation registration | All controlled WSs registered in `CRN-AR-WS-001`; license-server concurrency enforced (max 50 concurrent) | C | FS-DEP-01 | IQ-DEP-01 |
| DS-DEP-02 | JMP version pin | JMP 18 Pro locked for the current CPV programme; upgrade gate = change control + JSL revalidation pass | C | FS-DEP-02 | OQ-DEP-01 |
| DS-DEP-03 | JMP add-in allowlist registry | GPO `GMP-Lab-Workstations` disables Office macros; JMP add-ins restricted to entries in `cv_jsl_signed_addins` registry | C | FS-DEP-03 | OQ-DEP-02 |
| DS-DEP-04 | JMP install location ACL | NTFS read-only for analyst accounts on `C:\Program Files\SAS\JMPPRO\18`; admin via SCCM only | C | FS-DEP-01 | IQ-DEP-02 |
| DS-DEP-05 | JMP startup script binding | `verify-signed.jsl` set as JMP startup script via registry `HKLM\SOFTWARE\SAS Institute Inc.\JMP\18\StartupScript` | C | FS-JSL-03 | OQ-DEP-03 |

### 4.2 JSL Library Configuration (Cat 5 Sub-Component Bindings)

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-JSL-01 | JSL repository | GitLab `carina/spc-jsl`; protected `main`; Sigstore gitsign-signed commits | C | FS-JSL-01 | OQ-JSL-01 |
| DS-JSL-02 | Model Card requirement | `MODEL_CARD.md` mandatory per script; CI gate `mr_check_model_card.yml` blocks merge without it | C | FS-JSL-02 | OQ-JSL-02 |
| DS-JSL-03 | Load-time signature verification | cosign-style detached signatures; `verify-signed.jsl` startup script invokes verify before any add-in load | C | FS-JSL-03 | OQ-JSL-03 |
| DS-JSL-04 | JSL test harness | `jmp-test-runner.jsl`; pytest-style harness; CI runs on every MR | C | FS-JSL-04 | OQ-JSL-04 |
| DS-JSL-05 | JMP add-in audit-log forwarding | `(script_id, version, executor, timestamp, inputs_hash, outputs_hash)` → Splunk via syslog-ng forwarder | C | FS-JSL-05 | OQ-JSL-05 |

### 4.3 Control-Chart Catalogue Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-CHT-01 | Shewhart catalogue | X̄-R (subgroup vars); X̄-s (subgroup vars n ≥ 10); I-MR (individuals); p, np, c, u (attributes) per ISO 7870-2:2023 | C | FS-CHT-01 | OQ-CHT-01 |
| DS-CHT-02 | EWMA + CUSUM defaults | EWMA λ=0.2, L=3; CUSUM h=4σ, k=0.5σ per ISO 7870-4/-6; per-attribute override | C | FS-CHT-02 | OQ-CHT-02 |
| DS-CHT-03 | Multivariate methods | Hotelling T² + MEWMA via JMP Multivariate Methods; control-limit override by statistician | C | FS-CHT-03 | OQ-CHT-03 |
| DS-CHT-04 | Chart-decision register | `cv_chart_decisions` per attribute: `chart_type, subgroup, autocorrelation, rationale, qa_approver`; rule activation requires QA approver | C | FS-CHT-04 | OQ-CHT-04 |

### 4.4 Capability + Performance Indices Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-CAP-01 | Normality + transform pipeline | Anderson–Darling α=0.05; on rejection → Box–Cox transform via JMP Distribution platform OR Clements non-parametric; ISO 22514-2 formulas | C | FS-CAP-01 | OQ-CAP-01 |
| DS-CAP-02 | Small-sample gating thresholds | n ≥ 30 valid; 10 ≤ n < 30 → "indicative"; n < 10 → suppressed `INSUFFICIENT_N`; rendered in CPV report | C | FS-CAP-02 | OQ-CAP-02 |
| DS-CAP-03 | Side-by-side index rendering | Cp/Cpk (within-batch) + Pp/Ppk (overall) + variance-component plot via JMP Capability platform | C | FS-CAP-03 | OQ-CAP-03 |
| DS-CAP-04 | Bissell 95% CI bindings | JMP Capability platform CI computation; Cpk + Ppk both rendered with bounds | C | FS-CAP-04 | OQ-CAP-04 |

### 4.5 OOC / OOT Detection-Rule Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-OOC-01 | Western Electric Rules 1–4 | JMP Control Chart Rules; verified against AIAG SPC reference dataset at OQ | D | FS-OOC-01 | OQ-OOC-01 |
| DS-OOC-02 | Nelson Rules 1–8 | JMP Control Chart Rules; per-attribute activation flag | D | FS-OOC-02 | OQ-OOC-02 |
| DS-OOC-03 | Custom-rule JSL function library | Stored in JSL library; statistician approval gates activation | C | FS-OOC-03 | OQ-OOC-03 |
| DS-OOC-04 | Rule-firing emission | `(batch_id, attribute, rule_no, ruleset, ts, value)` written to `cv_rule_firings`; idempotent eQMS push on rule-violation-id | C | FS-OOC-04 | OQ-OOC-04 |
| DS-OOC-05 | ARL₀ activation gate | `cv_ruleset_arl_table` maintained; ruleset with ARL₀ < 30 → warning + statistician sign-off required at activation | C | FS-OOC-05 | OQ-OOC-05 |

### 4.6 Phase 1 / Phase 2 Workflow Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-PH-01 | Phase 1 JSL `establish_chart.jsl` | requires ≥ 20 reference batches (≥ 25 per ASTM E2587 configurable); outputs trial limits + capability baseline + statistician + QA approval form | C | FS-PH-01 | OQ-PH-01 |
| DS-PH-02 | Limit-locking on Phase 1 → Phase 2 | `cv_chart_limits.locked=true`; further change routes through change control | C | FS-PH-02 | OQ-PH-02 |
| DS-PH-03 | Phase 2 JSL `monitor_chart.jsl` | Applies locked limits + activated ruleset; OOC firings route via DS-OOC-04 | C | FS-PH-03 | OQ-PH-03 |
| DS-PH-04 | Limit-revision workflow | ≥ 20 post-change batches required + statistician approval; new revision number assigned + Phase 1 sub-workflow re-runs | C | FS-PH-04 | OQ-PH-04 |

### 4.7 Batch Genealogy Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-GEN-01 | Genealogy schema | Lakehouse `genealogy.batch_lineage` joined into every CPV record via `link_genealogy.jsl` | C | FS-GEN-01 | OQ-GEN-01 |
| DS-GEN-02 | OOC genealogy linkage | OOC firings linked to `(step, equipment_train, raw_material_lot, operator, env_conditions)` via genealogy + MES attributes | C | FS-GEN-02 | OQ-GEN-02 |
| DS-GEN-03 | Forward-trace function | `trace_forward.jsl` enumerates downstream-affected batches given a root-cause input | C | FS-GEN-03 | OQ-GEN-03 |

### 4.8 Real-Time SPC Alerting Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-RT-01 | PI Notification subscriptions | Per critical attribute in `cv_rt_subscriptions`; latency ≤ 60 s measured per PQ-RT-01 | C | FS-RT-01 | PQ-RT-01 |
| DS-RT-02 | Alert-router topology | Push to (PAS-X Production Alarms + eQMS deviation create + Process-Eng on-call PagerDuty); idempotency on alert-id | C | FS-RT-02 | OQ-RT-01 |
| DS-RT-03 | Alert-suppression workflow | Captures `(alert_id, suppression_reason, suppressed_by, ts, statistician_review_at)`; monthly statistician review | C | FS-RT-03 | OQ-RT-02 |

### 4.9 CPV Workflow Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-CPV-01 | CPV cadence config | Per product / process in `cv_cpv_cadence`; cron triggers nightly | C | FS-CPV-01 | OQ-CPV-01 |
| DS-CPV-02 | Query version + SHA capture | `cv_lakehouse_queries` stores query versions; SHA-256 of query string captured at execution; data engineering co-signature on every revision | C | FS-CPV-02 | OQ-CPV-02 |
| DS-CPV-03 | Quarto template mandatory sections | charts; capability indices; trend; OOC/OOT; genealogy; CR summary | C | FS-CPV-03 | OQ-CPV-03 |
| DS-CPV-04 | Vault CPV signature workflow | `CRN-WF-CPV-001`: Analyst → Senior Analyst → Statistician → Head of Manufacturing Sci → Head of QA | C | FS-CPV-04 | OQ-CPV-04 |
| DS-CPV-05 | Vault filing-on-final-sign | Auto-file on final approver e-sign | C | FS-CPV-05 | OQ-CPV-05 |

### 4.10 Audit + Part 11 + DI Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-AUD-01 | Lakehouse query audit | `(user, query_sha, ts)` persisted ≥ 25 y in `cv_query_log` | C | FS-AUD-01 | OQ-AUD-01 |
| DS-AUD-02 | JMP audit → Splunk | JMP add-in audit log forwarded; Splunk index retention ≥ 25 y; WORM tier `splunk-gxp-worm` | C | FS-AUD-02 | OQ-AUD-02 |
| DS-AUD-03 | Vault audit append-only | Vault append-only on every CPV transition (SaaS-native) | C | FS-AUD-03 | OQ-AUD-03 |
| DS-AUD-04 | Retention cross-cluster | ≥ 25 y across Vault + Splunk + lakehouse | C | FS-AUD-04 | OQ-AUD-04 |
| DS-PART11-50 | § 11.50 manifestation | Vault e-sig manifestation: `printedName + dateTime + meaning` | C | FS-PART11-50 | OQ-P11-01 |
| DS-PART11-100 | § 11.100 uniqueness | AD UPN | C | FS-PART11-100 | OQ-P11-02 |
| DS-PART11-200 | § 11.200 re-auth | Vault forces re-auth at signing | C | FS-PART11-200 | OQ-P11-03 |
| DS-DI-01 | ALCOA+ Attributable | AD principal attached to every audit event | C | FS-DI-01 | OQ-DI-01 |
| DS-DI-04 | ALCOA+ Original | Lakehouse source data immutable via Delta time-travel; CPV record stores query SHA + execution ts | C | FS-DI-04 | OQ-DI-02 |
| DS-DI-05 | ALCOA+ Accurate | OQ runs against AIAG SPC reference + ASTM E2587 examples | C | FS-DI-05 | OQ-DI-03 |

### 4.11 Integration Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-INT-LAKE-01 | Lakehouse query auth | OAuth2 client-credentials; service account `svc-crn-spc-lake` in HashiCorp Vault; per-query audit log to `cv_query_log` | C | FS-INT-LAKE-01 | OQ-INT-01 |
| DS-INT-VAULT-01 | Vault QualityDocs push | REST push of CPV PDF + structured CSV + audit-trail export; endpoint `https://vault.veeva.com/api/v24.1/objects/cpv_report` | C | FS-INT-VAULT-01 | OQ-INT-02 |
| DS-INT-EQMS-01 | MasterControl deviation push | REST `POST /api/v3/deviations`; idempotency key = `rule-violation-id`; mTLS via site PKI; retry 3× expo back-off; DLQ at 5 | C | FS-INT-EQMS-01, FS-XINT-EQMS-01 | OQ-INT-03 |
| DS-INT-EQMS-02 | eQMS status webhook | subscribe `eqms.status.v1`; consumer maps `(OPEN, IN-PROGRESS, EFFECTIVENESS, CLOSED)` onto originating-record disposition; closed-loop gate prevents disposition without `eqms_status=CLOSED` | C | FS-XINT-EQMS-02 | OQ-INT-04 |
| DS-INT-PI-01 | PI Notification subscription | via PI Web API; AD service account `svc-crn-spc-pi` | C | FS-INT-PI-01 | OQ-INT-05 |
| DS-INT-MES-01 | PAS-X Production Alarms | REST `POST /pasx/api/v3/production-alarms`; idempotency on alert-id | C | FS-INT-MES-01 | OQ-INT-06 |
| DS-INT-APR-01 | APR / PQR read endpoint | `GET /spc/api/v2/summary?product={p}` read-only; AD-bound consumer | C | FS-INT-APR-01 | OQ-INT-07 |

### 4.12 Performance + Security + Training + PR Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-PERF-01 | CPV report latency target | ≤ 15 min on baseline WS per PQ-PERF-CPV-RUN-01 | C | FS-PERF-01 | PQ-PERF-01 |
| DS-SEC-01 | AD + MFA + access review | AD interactive + MFA enforced; quarterly access review | C | FS-SEC-01 | OQ-SEC-01 |
| DS-TRN-01 | Cornerstone curriculum | `CRN-CURR-SPC-Analyst-v1`; SPC competency assessment incl. Phase 1/2, capability, Nelson rules | C | FS-TRN-01 | OQ-TRN-01 |
| DS-PR-01 | Annual periodic-review template | `CRN-PR-SPC-YYYYMMDD` | C | FS-PR-01 | OQ-PR-01 |

### 4.13 Cross-System Integration Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-XSYS-AD-01 | AD conditional access | LDAPS on-prem; conditional-access policy `Quality-App Conditional Access (MFA on first logon per session)`; SIEM forwarding to Splunk `gxp-authn` ≤ 5 min; SCIM where SAML/OIDC; CyberArk PAM for break-glass with 24 h rotation + dual-witness check-out | C | FS-XSYS-AD-01 | OQ-XSYS-01 |
| DS-XSYS-BAK-01 | Backup integration | Veeam Application-Aware MS SQL VSS for SPC mart DB; Tier T2 (RPO ≤ 24 h; RTO ≤ 24 BH); S3 Object Lock Compliance + LTO-9 monthly; quarterly QA-witnessed restore drill; restore certs ≥ 25 y in eQMS | C | FS-XSYS-BAK-01 | OQ-XSYS-02 |

## 5. Workflow + Business-Rule Design

### 5.1 Phase-1 → Phase-2 Promotion Workflow (`CRN-WF-PH12-SPC`)

Trigger: ≥ 20 reference batches collected for an attribute. States: `PHASE_1_DRAFT → PHASE_1_REVIEW → PHASE_1_APPROVED → PHASE_2_LIVE → REVISION`. Transitions:

| From | To | Role | Side-effects |
|---|---|---|---|
| PHASE_1_DRAFT | PHASE_1_REVIEW | Analyst | `establish_chart.jsl` produces trial limits + capability baseline |
| PHASE_1_REVIEW | PHASE_1_APPROVED | Statistician + QA Approver dual sign | Limits frozen as proposed |
| PHASE_1_APPROVED | PHASE_2_LIVE | Statistician | `cv_chart_limits.locked=true` + ruleset bound |
| PHASE_2_LIVE | REVISION | Statistician (triggered by change control) | Re-enter PHASE_1_DRAFT with new revision number |

### 5.2 OOC Rule-Violation → eQMS Workflow

DS-OOC-04 emits idempotent eQMS push on `rule-violation-id`. eQMS workflow `CRN-MC-WF-SPC-DEV` opens deviation ticket → routing per attribute criticality matrix → CAPA effectiveness check → close. Closed-loop verification (DS-INT-EQMS-02) gates the originating CPV record's disposition.

### 5.3 Real-Time Alert Suppression Workflow

Statistician opens suppression form with `suppression_reason` (free text ≥ 20 chars) + supervisor co-sign. Monthly statistician review (DS-RT-03) reviews all open suppressions; suppressions older than 30 d auto-flag for forced disposition.

### 5.4 JSL Merge-to-Main Workflow

| Step | Gate |
|---|---|
| MR opened | CI runs `jmp-test-runner.jsl`; PASS required |
| MR reviewed | At least 2 approvers (statistician + senior data engineer); Sigstore gitsign verified |
| MR merged | protected `main`; signed commit |
| Tag release | cosign-style signature attached; entry added to `cv_jsl_signed_addins` registry |

### 5.5 Lakehouse Query-Revision Workflow

Trigger: data engineer modifies a query in `cv_lakehouse_queries`. Steps:

| Step | Actor | Gate |
|---|---|---|
| Query draft | Data Engineer | Local Databricks notebook test against `cv_test_fixtures` |
| MR opened to `cv_lakehouse_queries` repo mirror | Data Engineer | CI runs SHA-stability test (same query string ⇒ same SHA) |
| Review | Statistician | Verifies the column-semantics + join-cardinality |
| Approval | Data Engineer (≠ Author) + Statistician dual sign | Both signatures required |
| Promotion | Data Engineer | New query SHA + version captured in `cv_lakehouse_queries`; nightly CPV cron picks up at next run |

### 5.6 Chart-Decision Adoption Workflow (Decision-Register Governance)

A chart-decision row (chart type + subgroup + autocorrelation + rationale) lives in `cv_chart_decisions` per attribute. Workflow `CRN-WF-CHTDEC-SPC`:

| Step | Actor | Gate |
|---|---|---|
| Decision draft | Statistician | autocorrelation analysis + chart-fit justification |
| Approval | QA Approver | mandatory before activation per FS-CHT-04 |
| Activation | Statistician | only after QA approval; activation event emitted to `cv_query_log` for traceability |
| Re-evaluation | annually + on process-change | re-runs decision draft → approval → activation |

### 5.7 Real-Time Alert-Suppression Lifecycle

States: `OPEN → SUPPRESSED → STATISTICIAN_REVIEWED → CLOSED` or `OPEN → DISPOSITIONED`. Suppression cannot transition straight to CLOSED; statistician review (monthly) is mandatory. Stale suppressions (> 30 d) trigger `SUPPRESSION_STALE` event consumed by monthly review dashboard.

### 5.8 Suppression-Reason Taxonomy

Per DS-RT-03, suppression reasons are constrained to an enumerated taxonomy stored in `cv_suppression_reasons`:

| Reason code | Meaning | Auto-escalate? |
|---|---|---|
| `KNOWN_INSTRUMENT_ARTEFACT` | Calibration / probe artefact not affecting product | No (statistician review only) |
| `MAINTENANCE_WINDOW` | Within a documented planned-maintenance window | No |
| `INVESTIGATION_PENDING_EQMS` | Already raised in eQMS; suppress duplicate while CAPA pending | Yes — auto-link to eQMS deviation ID |
| `OOC_INVESTIGATION_FOUND_NO_IMPACT` | Investigated; no product impact | No |
| `OTHER` (free text required, ≥ 20 chars) | Catch-all | Yes — auto-flag for review at next monthly cycle |

## 6. Role-Permission Matrix Design

| AD Group → / Permission ↓ | ANALYST | SR-ANALYST | STAT | PROC-ENG | HMS | QA-APPROVER | DATA-ENG | SYS-ADMIN |
|---|---|---|---|---|---|---|---|---|
| Open JMP + run JSL | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Approve chart-decision (CHT-04) | — | — | — | — | — | ✓ | — | — |
| Run Phase 1 establish | ✓ | ✓ | ✓ | — | — | — | — | — |
| Approve Phase 1 → Phase 2 | — | — | ✓ | — | — | ✓ | — | — |
| Activate Western Electric / Nelson ruleset | — | — | ✓ | — | — | ✓ | — | — |
| Activate custom JSL rule | — | — | ✓ | — | — | ✓ | — | — |
| Approve suppression | — | — | ✓ | — | — | — | — | — |
| Sign CPV report (Analyst step) | ✓ | ✓ | — | — | — | — | — | — |
| Sign CPV report (Senior Analyst) | — | ✓ | — | — | — | — | — | — |
| Sign CPV report (Statistician) | — | — | ✓ | — | — | — | — | — |
| Sign CPV report (HMS) | — | — | — | — | ✓ | — | — | — |
| Sign CPV report (QA) | — | — | — | — | — | ✓ | — | — |
| Modify lakehouse query (with data-eng co-sign) | — | — | — | — | — | — | ✓ | — |
| Modify CS / configuration | — | — | — | — | — | — | — | ✓ (CCR) |
| Merge to JSL `main` | — | — | ✓ | — | — | — | ✓ | — |
| Read all audit | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

Author-Approver separation: a user shall NOT simultaneously hold `CRN-SPC-STAT` AND `CRN-SPC-QA-APPROVER` AD-group membership. Verified quarterly per DS-SEC-01.

## 7. Integration Design

### 7.1 Databricks Lakehouse Connector (DS-INT-LAKE-01)

| Aspect | Value |
|---|---|
| Workspace | `prod-lake-carina.cloud.databricks` |
| Auth | OAuth2 client-credentials via HashiCorp Vault path `secret/crn-spc/lake` |
| Service account | `svc-crn-spc-lake` (rotated 180 d) |
| Query auditing | every query write to `cv_query_log (user, query_sha, ts, runtime_ms, row_count)`; retention ≥ 25 y |
| Network | private link to Databricks; no public-internet path |
| Query allowlist | only signed query revisions from `cv_lakehouse_queries` may run in CPV cron |

### 7.2 Vault QualityDocs (DS-INT-VAULT-01)

| Aspect | Value |
|---|---|
| Endpoint | `https://carina.veevavault.com/api/v24.1/objects/cpv_report` |
| Auth | OAuth2 + SCIM-provisioned principals |
| Payload | PDF + structured CSV summary + JSON audit-trail export |
| Lifecycle | `DRAFT → IN-REVIEW → APPROVED → EFFECTIVE` per `CRN-WF-CPV-001` |

### 7.3 MasterControl eQMS (DS-INT-EQMS-01/02)

| Aspect | Value |
|---|---|
| Push endpoint | `POST /api/v3/deviations` |
| Transport | HTTPS + mTLS (site PKI cert `CRN-PKI-SPC-EQMS`) |
| Idempotency key | `rule-violation-id` from `cv_rule_firings` |
| Retry | 3× exponential back-off; DLQ at 5 |
| Status webhook | subscribe `eqms.status.v1`; closed-loop gate at originating CPV record |

### 7.4 AVEVA PI Notifications (DS-INT-PI-01)

| Aspect | Value |
|---|---|
| API | PI Web API; service account `svc-crn-spc-pi` |
| Subscription source | `cv_rt_subscriptions` table |
| Latency target | ≤ 60 s |
| Alert payload | `(attribute, rule_no, value, ts, batch_id, idempotency_key)` |

### 7.5 PAS-X MES (DS-INT-MES-01)

| Aspect | Value |
|---|---|
| Endpoint | `POST /pasx/api/v3/production-alarms` |
| Transport | HTTPS + AD-bound service account |
| Idempotency | alert-id |

### 7.6 AD / SIEM / Backup (DS-XSYS-*)

Inherits the cross-system patterns; specifics in § 4.13.

### 7.7 Splunk SIEM Integration Specifics

| Aspect | Value |
|---|---|
| Forwarder | syslog-ng on each JMP analyst WS + lakehouse query-log shipper |
| Indices | `gxp-authn` (interactive logon); `gxp-spc-jsl` (JMP add-in audit); `gxp-spc-query` (lakehouse query log) |
| Ingestion latency target | ≤ 5 min per FS-XSYS-AD-01 |
| WORM tier | `splunk-gxp-worm` index 25 y retention |
| Alerting rules | (a) missed JSL signature verification; (b) lakehouse query allowlist violation; (c) eQMS push DLQ overflow; (d) Vault signature out-of-order |

### 7.8 Network + Firewall Topology

| Source → Destination | Port / Protocol | Rule |
|---|---|---|
| Analyst WS → JMP license server | TCP 1701 | site-internal only |
| Analyst WS → Databricks workspace | TCP 443 (HTTPS) | private-link allowlist only |
| JMP WS → Vault QualityDocs SaaS | TCP 443 (HTTPS) | Veeva-Vault-IP allowlist |
| JMP WS → MasterControl eQMS | TCP 443 (HTTPS) + mTLS | site PKI cert validation |
| Site SPC backend → PI Notifications | TCP 5450 (PI Web API) | site-internal only |
| Site SPC backend → PAS-X | TCP 443 (HTTPS) | site-internal |
| All logs → Splunk HEC | TCP 8088 (HTTPS) | site-internal |

### 7.9 Disaster-Recovery Design

| Aspect | Value |
|---|---|
| Lakehouse | Databricks workspace replicated to secondary region (active-passive); RPO ≤ 1 h |
| JSL repo | GitLab geo-replicated; RPO ≤ 15 min |
| Vault QualityDocs | Veeva SaaS DR per Veeva SLA |
| MasterControl | per MasterControl SaaS SLA |
| AVEVA PI | warm-standby on-prem `crn-pi-not-02`; manual failover runbook `CRN-RB-PI-DR-001` |
| Failover drill | annual joint exercise per `CRN-RB-DR-DRILL-001` |

## 8. Site-Deployed Components

### 8.1 JSL Library Mini-SDS (Cat 5 Sub-Component)

The JSL library `carina/spc-jsl` is the Cat 5 sub-component embedded in this Cat 4 system. The mini-SDS below documents its design.

#### 8.1.1 Software Architecture (logical view)

| Component | Responsibility |
|---|---|
| `verify-signed.jsl` | Startup script; verifies cosign-style detached signature on every add-in load |
| `establish_chart.jsl` | Phase 1 chart-establishment + trial-limit calculation |
| `monitor_chart.jsl` | Phase 2 monitoring; applies locked limits + ruleset |
| `compute_capability.jsl` | Anderson–Darling + Box–Cox / Clements + Cp/Cpk/Pp/Ppk per ISO 22514-2 |
| `link_genealogy.jsl` | Joins `genealogy.batch_lineage` into CPV record |
| `trace_forward.jsl` | Forward-trace enumeration from a root-cause key |
| `rule_lib.jsl` | Western Electric + Nelson + custom rule implementations |
| `cpv_render.jsl` | Quarto template orchestration |

#### 8.1.2 Module Decomposition

| ID | Module | Interface | Dependencies | GxP-criticality |
|---|---|---|---|---|
| JSL-M-01 | `verify-signed.jsl` | exposes `verify_signature(path) → bool` | cosign binary | R1 |
| JSL-M-02 | `establish_chart.jsl` | `(attribute, batches) → trial_limits, baseline_capability` | M-04, M-07 | R1 |
| JSL-M-03 | `monitor_chart.jsl` | `(attribute, new_batch) → ooc_firings` | M-07 | R1 |
| JSL-M-04 | `compute_capability.jsl` | `(values, USL, LSL) → Cp, Cpk, Pp, Ppk + CI` | none (JMP platform calls) | R1 |
| JSL-M-05 | `link_genealogy.jsl` | `(batch_id) → genealogy_record` | lakehouse REST | R2 |
| JSL-M-06 | `trace_forward.jsl` | `(root_cause_key) → affected_batch_set` | M-05 | R2 |
| JSL-M-07 | `rule_lib.jsl` | `(series, ruleset) → firings` | none | R1 |
| JSL-M-08 | `cpv_render.jsl` | `(cpv_record) → PDF path` | Quarto binary | R2 |

#### 8.1.3 Data Model

JSL functions read lakehouse `cv_*` + `genealogy.*` tables (Delta format) and write to `cv_rule_firings`, `cv_chart_limits`, `cv_ruleset_arl_table`. Schemas defined in `cv_schema.yaml` (versioned in repo); changes require data-eng + statistician co-signature.

#### 8.1.4 Algorithm Specifications (sketch)

- **Phase 1 trial-limit computation:** per ISO 7870-2 §§ 8.2–8.4; subgroup formulas X̄ ± A₂R̄ (X̄-R) / X̄ ± A₃s̄ (X̄-s) with explicit A₂, A₃, D₃, D₄ from JMP tables.
- **Capability indices:** per ISO 22514-2; non-normal path via Box–Cox or Clements (3-parameter percentile-based) — chosen by Anderson–Darling p-value.
- **Western Electric Rules 1–4:** standard 3σ / 2-of-3 2σ / 4-of-5 1σ / 8-on-same-side.
- **Nelson Rules 1–8:** per Nelson (1984) Journal of Quality Technology.
- **Idempotency:** rule-firing IDs computed as `SHA-256(batch_id||attribute||rule_no||ts)` to guarantee deduplication at eQMS push.

#### 8.1.5 Security Design

| Layer | Mechanism |
|---|---|
| Source integrity | Sigstore gitsign on every commit |
| Distribution integrity | cosign-style detached signature on every add-in tag |
| Load-time integrity | `verify-signed.jsl` startup; mismatch → JMP refuses to load |
| Secrets | HashiCorp Vault paths; never embedded in JSL |

#### 8.1.6 Deployment

- CI runs `jmp-test-runner.jsl` against AIAG SPC + ASTM E2587 reference datasets on every MR.
- Tagged releases produce signed `.jmpaddin` bundles published to internal artefact repo.
- `cv_jsl_signed_addins` registry maintained by data-eng + statistician dual sign-off.

#### 8.1.7 Module Specification Table

| Module ID | Module Spec doc |
|---|---|
| JSL-M-01 | `CRN-MS-JSL-VERIFY-001` |
| JSL-M-02 | `CRN-MS-JSL-ESTABLISH-001` |
| JSL-M-03 | `CRN-MS-JSL-MONITOR-001` |
| JSL-M-04 | `CRN-MS-JSL-CAPABILITY-001` |
| JSL-M-05 | `CRN-MS-JSL-GENEALOGY-001` |
| JSL-M-06 | `CRN-MS-JSL-TRACE-001` |
| JSL-M-07 | `CRN-MS-JSL-RULELIB-001` |
| JSL-M-08 | `CRN-MS-JSL-CPVRENDER-001` |

#### 8.1.8 Observability Design

| Telemetry channel | Emitter | Sink | Use |
|---|---|---|---|
| JSL function-call audit | every JSL function emits `(script_id, version, executor, ts, inputs_hash, outputs_hash)` | Splunk `gxp-spc-jsl` | per-call traceability |
| Lakehouse query log | data-eng query shipper | Splunk `gxp-spc-query` | query-revision detection |
| Rule-firing emission | `rule_lib.jsl` | `cv_rule_firings` + Splunk | OOC investigation |
| Real-time alert latency | PI Notification emitter timestamp + receipt timestamp in PAS-X / eQMS / PagerDuty | Splunk metric `spc.rt_latency_seconds` | SLA monitoring |
| Capability index trend | `compute_capability.jsl` | `cv_capability_history` | Cpk/Ppk drift over time |
| CPV report sign-off latency | Vault audit-trail export | `cv_cpv_sign_latency` | bottleneck analysis |

#### 8.1.9 Failure-Mode Catalogue

| Failure | Detection | Recovery |
|---|---|---|
| JSL signature mismatch | `verify-signed.jsl` startup hook | JMP refuses to load add-in; ops paged |
| Lakehouse OAuth2 token expiry | OAuth2 401 response | HashiCorp Vault auto-refresh; on failure → JSL function returns `AUTH_ERROR`; CPV cron retries |
| Query SHA mismatch | nightly CPV cron pre-flight | abort run; eQMS deviation `CRN-SPC-QUERY-DRIFT` opened |
| Rule-firing duplicate at eQMS | idempotency key collision | DLQ at 5 attempts; reconciliation runs nightly |
| PI Notification source dropout | PI heartbeat | PagerDuty alert; site SPC backend pauses real-time consumption |
| Vault sign-off out of order | Vault workflow rejects | originating record stays in `IN-REVIEW`; analyst notified |

### 8.2 Lakehouse-Query Shipper (`crn-spc-query-ship.py`)

- **Language:** Python 3.12 inside `crn-spc-query-ship-env` (cosign-signed image).
- **Responsibility:** Tails Databricks `system.audit` table; writes structured records to `cv_query_log` and forwards to Splunk `gxp-spc-query` index.
- **Interface:** Databricks audit log read API; Splunk HEC write.
- **Verification:** OQ-LAKE-SHIP-01.
- **Module Spec reference:** `CRN-MS-LAKESHIP-001`.

### 8.3 eQMS Reconciliation Job (`crn-spc-eqms-reconcile.py`)

- **Language:** Python 3.12 inside `crn-spc-eqms-rec-env` (cosign-signed).
- **Responsibility:** Nightly pulls `eqms_status` REST for every open `rule-violation-id` not yet CLOSED; ensures DS-INT-EQMS-02 webhook outage doesn't leave orphan dispositions.
- **Interface:** MasterControl REST read; `cv_rule_firings` update.
- **Verification:** OQ-EQMS-REC-01.
- **Module Spec reference:** `CRN-MS-EQMSREC-001`.

### 8.4 Site-Deployed Component Deployment Pipeline

All three site-deployed Python components (8.2, 8.3 + any future addition) follow a uniform SDLC:

| Stage | Gate |
|---|---|
| Source | GitLab `carina/spc-tools`; protected `main`; Sigstore gitsign on every commit |
| Build | container image built from pinned `python:3.12-slim` base; SBOM emitted (CycloneDX); cosign signature attached |
| Test | pytest unit + integration tests against sandbox lakehouse / eQMS instances |
| Promote | dev → val → prod; val→prod requires data-eng + statistician dual sign |
| Deploy | OpenShift `crn-spc-tools-ns` namespace; container image pull restricted to signed images via Image Policy Webhook |
| Monitor | Prometheus metrics scraped to Splunk; alerts on (image-pull-fail, restart-loop, schema-mismatch) |
| Sunset | retired images archived to `crn-spc-tools-archive` registry with manifest |

### 8.5 Site-Side Cron Scheduling

| Job | Schedule | Owner |
|---|---|---|
| CPV nightly run | per `cv_cpv_cadence` per product (typically 02:00 local) | Data Engineering |
| Lakehouse query shipper | continuous tail | Data Engineering |
| eQMS reconciliation | 03:00 daily | Data Engineering |
| Vault audit-export | weekly Sunday 04:00 | QA Compliance |
| JSL signature scan | weekly Monday 05:00 | Security |
| GPO compliance scan | quarterly | Site IT |
| Lakehouse retention sweep | monthly 1st 03:00 | Data Engineering |
| Backup restore drill | quarterly | QA + IT (joint) |
| DR failover drill | annual | DR Team |

## 9. References

### US
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200
- FDA *Process Validation: General Principles and Practices* (2011) — Stage 3 CPV
- FDA *Data Integrity and Compliance Guidance* (2018)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EMA *Reflection paper on statistical methodology for the comparative assessment of quality attributes* (informational)

### DACH
- BSI IT-Grundschutz APP.4 / NET.3 (informational)

### International
- ICH Q8(R2), Q9(R1), Q10, Q12
- ASTM E2587-22 *Standard Practice for Use of Control Charts in Statistical Process Control*
- ISO 7870-1 / -2 / -4 / -6 / -8; ISO 22514-2:2017
- USP <1010>
- PIC/S PI 041
- ISPE GAMP 5 (2nd Ed., 2022)
- OWASP ASVS v4; OWASP LLM Top 10 (informational); NIST SP 800-218 SSDF; SLSA (for JSL repo + cosign chain)

### Vendor
- SAS Institute — *JMP 18 Pro Reference*; *JMP Scripting Index (JSL Language Reference)*; *JMP Administrator's Guide* (synthetic placeholders)
- AVEVA — *PI System 2024 Administrator Reference* (cross-ref `KYM-URS-HIST-001`)
- Werum — *PAS-X v3.2 Production Alarms API Reference*
- MasterControl — *Deviation REST API Reference*
- Veeva — *Vault QualityDocs 24R1 API Reference*

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) |
|---|---|
| DS-DEP-01 | FS-DEP-01 |
| DS-DEP-02 | FS-DEP-02 |
| DS-DEP-03 | FS-DEP-03 |
| DS-DEP-04 | FS-DEP-01 |
| DS-DEP-05 | FS-JSL-03 |
| DS-JSL-01 | FS-JSL-01 |
| DS-JSL-02 | FS-JSL-02 |
| DS-JSL-03 | FS-JSL-03 |
| DS-JSL-04 | FS-JSL-04 |
| DS-JSL-05 | FS-JSL-05 |
| DS-CHT-01 | FS-CHT-01 |
| DS-CHT-02 | FS-CHT-02 |
| DS-CHT-03 | FS-CHT-03 |
| DS-CHT-04 | FS-CHT-04 |
| DS-CAP-01 | FS-CAP-01 |
| DS-CAP-02 | FS-CAP-02 |
| DS-CAP-03 | FS-CAP-03 |
| DS-CAP-04 | FS-CAP-04 |
| DS-OOC-01 | FS-OOC-01 |
| DS-OOC-02 | FS-OOC-02 |
| DS-OOC-03 | FS-OOC-03 |
| DS-OOC-04 | FS-OOC-04 |
| DS-OOC-05 | FS-OOC-05 |
| DS-PH-01 | FS-PH-01 |
| DS-PH-02 | FS-PH-02 |
| DS-PH-03 | FS-PH-03 |
| DS-PH-04 | FS-PH-04 |
| DS-GEN-01 | FS-GEN-01 |
| DS-GEN-02 | FS-GEN-02 |
| DS-GEN-03 | FS-GEN-03 |
| DS-RT-01 | FS-RT-01 |
| DS-RT-02 | FS-RT-02 |
| DS-RT-03 | FS-RT-03 |
| DS-CPV-01 | FS-CPV-01 |
| DS-CPV-02 | FS-CPV-02 |
| DS-CPV-03 | FS-CPV-03 |
| DS-CPV-04 | FS-CPV-04 |
| DS-CPV-05 | FS-CPV-05 |
| DS-AUD-01 | FS-AUD-01 |
| DS-AUD-02 | FS-AUD-02 |
| DS-AUD-03 | FS-AUD-03 |
| DS-AUD-04 | FS-AUD-04 |
| DS-PART11-50 | FS-PART11-50 |
| DS-PART11-100 | FS-PART11-100 |
| DS-PART11-200 | FS-PART11-200 |
| DS-DI-01 | FS-DI-01 |
| DS-DI-04 | FS-DI-04 |
| DS-DI-05 | FS-DI-05 |
| DS-INT-LAKE-01 | FS-INT-LAKE-01 |
| DS-INT-VAULT-01 | FS-INT-VAULT-01 |
| DS-INT-EQMS-01 | FS-INT-EQMS-01, FS-XINT-EQMS-01 |
| DS-INT-EQMS-02 | FS-XINT-EQMS-02 |
| DS-INT-PI-01 | FS-INT-PI-01 |
| DS-INT-MES-01 | FS-INT-MES-01 |
| DS-INT-APR-01 | FS-INT-APR-01 |
| DS-PERF-01 | FS-PERF-01 |
| DS-SEC-01 | FS-SEC-01 |
| DS-TRN-01 | FS-TRN-01 |
| DS-PR-01 | FS-PR-01 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| DS-JSL-MOD-VERIFY-01 | FS-JSL-03 |
| DS-JSL-MOD-ESTABLISH-01 | FS-PH-01 |
| DS-JSL-MOD-MONITOR-01 | FS-PH-03 |
| DS-JSL-MOD-CAPABILITY-01 | FS-CAP-01, FS-CAP-03, FS-CAP-04 |
| DS-JSL-MOD-GENEALOGY-01 | FS-GEN-01, FS-GEN-02 |
| DS-JSL-MOD-TRACE-01 | FS-GEN-03 |
| DS-JSL-MOD-RULELIB-01 | FS-OOC-01, FS-OOC-02, FS-OOC-03 |
| DS-JSL-MOD-CPVRENDER-01 | FS-CPV-03 |
| DS-SCR-LAKESHIP-01 | FS-AUD-01, FS-CPV-02 |
| DS-SCR-EQMSREC-01 | FS-INT-EQMS-01, FS-XINT-EQMS-02 |
| DS-OBS-01 | FS-JSL-05, FS-AUD-02 |
| DS-NET-01 | FS-DEP-01, FS-XSYS-AD-01 |
| DS-DR-01 | FS-XSYS-BAK-01 |

## 11. Appendix B — Design-level Risk Register

| ID | Design risk | Likelihood | Impact | Mitigation in this DS |
|---|---|---|---|---|
| DR-01 | JSL signing-key compromise allows malicious add-in load | Low | Critical | DS-JSL-03 cosign verification + Sigstore gitsign signed commits + quarterly key-rotation |
| DR-02 | Lakehouse query revision silently changes column semantics | Medium | High | DS-CPV-02 query SHA capture + DS-INT-LAKE-01 query allowlist + data-eng co-signature requirement |
| DR-03 | JMP add-in registry tampering enables unsigned add-in | Low | Critical | DS-DEP-03 GPO-locked registry + DS-DEP-05 startup script verification + quarterly GPO compliance scan |
| DR-04 | Phase 1 → Phase 2 limit-lock skipped, allowing unlocked monitoring | Medium | High | DS-PH-02 `cv_chart_limits.locked` flag + DS-PH-03 monitor refuses unlocked limits + dual-sign Phase 1 approval |
| DR-05 | Capability index Cpk false-positive on non-normal data | Medium | High | DS-CAP-01 Anderson–Darling gate + transform pipeline + statistician sign-off on alternative |
| DR-06 | Western Electric / Nelson false-alarm flood overwhelms eQMS | Medium | High | DS-OOC-05 ARL₀ gate + statistician approval at activation + DS-RT-03 monthly suppression review |
| DR-07 | Real-time alert suppression masks a true OOC | Low | Critical | DS-RT-03 monthly statistician review + 30-d auto-flag of stale suppressions |
| DR-08 | eQMS push duplicate-emission floods deviation queue | Medium | Medium | DS-INT-EQMS-01 idempotency key (rule-violation-id) + DLQ at 5 + retry expo back-off |
| DR-09 | eQMS status webhook outage blocks closed-loop disposition | Low | High | DS-INT-EQMS-02 webhook + nightly reconciliation job pulls `eqms_status` REST as backup |
| DR-10 | Vault CPV signature workflow misordered (e.g., HMS signs before Statistician) | Low | High | DS-CPV-04 Vault `CRN-WF-CPV-001` enforces step order; out-of-order sign rejected |
| DR-11 | Lakehouse Delta time-travel retention exhausted before audit horizon | Medium | High | DS-DI-04 + lakehouse retention policy `delta.retentionDurationCheck.enabled=true` set to 25 y |
| DR-12 | AD service-account `svc-crn-spc-lake` rotation skipped, secret leaked | Low | Critical | DS-INT-LAKE-01 180-d rotation enforced by HashiCorp Vault + Splunk alert on missed rotation |
| DR-13 | PI Notifications latency exceeds 60 s under load, real-time SLA breach | Medium | Medium | DS-RT-01 latency monitored at PQ + Splunk alert at p95 > 60 s |
| DR-14 | PAS-X Production Alarms endpoint API-version mismatch on PAS-X upgrade | Low | High | DS-INT-MES-01 endpoint version pinned in CS + contract-test runs on every PAS-X upgrade RFC |
| DR-15 | Genealogy join misses a sub-batch hierarchy level, root-cause analysis wrong | Medium | High | DS-GEN-01 + DS-GEN-02 + statistician sign-off at every chart-decision adoption (DS-CHT-04) |
| DR-16 | Lakehouse-query shipper (`crn-spc-query-ship.py`) silently halts on Databricks audit-log schema change | Medium | High | DS-SCR-LAKESHIP-01 hard-validates schema-version; emits `LAKESHIP_SCHEMA_MISMATCH` event; Splunk alert + ops page |
| DR-17 | Suppression auto-link to wrong eQMS deviation ID (taxonomy code `INVESTIGATION_PENDING_EQMS`) | Low | High | DS-RT-03 taxonomy + DS-INT-EQMS-02 closed-loop gate verifies deviation-id matches before honoring suppression |
| DR-18 | DR drill skipped, secondary-region lakehouse stale | Medium | Critical | DS-DR-01 annual joint drill mandatory + Splunk metric `dr.last_drill_days` alerts at 365 d |
| DR-19 | JMP licence-server failure blocks all CPV runs site-wide | Low | High | DS-DEP-01 concurrency monitoring + monthly licence-server health-check + offline-licence fallback for 7 d emergency window |
| DR-20 | JSL `compute_capability.jsl` Box–Cox transform converges to ill-conditioned λ on extreme skewness, returns biased Cpk | Low | High | DS-CAP-01 Anderson–Darling p-value + λ-bounds check (-2 ≤ λ ≤ 2); on out-of-bounds → Clements fallback + statistician sign-off |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
