---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "CRN-URS-SPC-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd Ed., 2022) Cat 3 conventions"
  - "21 CFR Part 11; EU GMP Annex 11; ICH Q8/Q9/Q10/Q12"
  - "FDA Process Validation 2011 — Stage 3"
  - "ASTM E2587; ISO 7870; ISO 22514-2; USP <1010>"
parent_urs:
  document_number: CRN-URS-SPC-001
  version: 1.2
  file: ../../URS/_generated/final/SPC_Statistical_Process_Control__Carina_Pharmaceuticals_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## SPC — JMP Statistical Discovery 18 Pro

**Document Number:** CRN-FS-SPC-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** CRN-URS-SPC-001 v1.2 | **Site:** Carina Pharmaceuticals (fictional)
**System Class:** GAMP Cat 3 — Non-Configured Product (JSL library treated as Cat 5 sub-component)
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; ICH Q8/Q9/Q10/Q12; FDA Process Validation 2011 — Stage 3 CPV; ASTM E2587; ISO 7870; ISO 22514-2

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Statistician) | _____________ | _____________ | _____ |
| Reviewer (Process Engineer) | _____________ | _____________ | _____ |
| Approver (Head of Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | v1.2: aligned with parent URS v1.2 (re-vendored prior NWA-based FS to match URS JMP/Cat-3 framing); per-URS-ID expansion across § 4 + § 8 per METHODOLOGY § 2A.7; explicit chart catalogue, capability, OOC rules, Phase 1/2 workflow, genealogy, real-time sections. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

Specify how JMP Statistical Discovery 18 Pro + the controlled JSL library is configured to satisfy `CRN-URS-SPC-001` v1.2 — Stage-3 CPV across commercial products.

## 2. Scope

JMP 18 Pro on controlled analyst workstations; JSL script library; Vault-managed CPV templates; data feed from Databricks lakehouse aggregating PAS-X + LIMS + EM + PI; real-time SPC via AVEVA PI Notification engine; integration with MasterControl eQMS for deviation routing; SSO via AD.

## 3. System Architecture

```
   ┌───────────────────────────────────────────────────────────┐
   │  Sources: PAS-X · LIMS · EM · AVEVA PI System              │
   └─────────────────────────────┬─────────────────────────────┘
                                 │ documented + version-controlled queries
                                 ▼
                   ┌──────────────────────────────┐
                   │   Databricks lakehouse        │
                   └──────────────┬───────────────┘
                                  │
            ┌─────────────────────┼──────────────────────┐
            │                     │                      │
            ▼                     ▼                      ▼
   JMP 18 Pro                JSL library              AVEVA PI
   (Cat 3 COTS)              (Cat 5 sub-comp)     Notification engine
   workstations              signed + tested       (real-time alerts)
            │                     │                      │
            └────────┬────────────┴──────────────────────┤
                     ▼                                   ▼
            Vault QualityDocs                  PAS-X · MasterControl
            (signed CPV reports)              (alarms · deviations)
```

### 3.1 Component Inventory

| ID | Component | GAMP Cat | Notes |
|---|---|---|---|
| C-01 | JMP Statistical Discovery 18 Pro | 3 | COTS (SAS Institute) |
| C-02 | JSL script library | 5 | site-developed sub-component |
| C-03 | Databricks lakehouse | 4 | data source (separate URS) |
| C-04 | AVEVA PI System 2024 + Notifications | 3 | real-time consumer (KYM-URS-HIST-001) |
| C-05 | Veeva Vault QualityDocs 24R1 | 4 | report archive |
| C-06 | MasterControl eQMS | 4 | deviation routing |
| C-07 | Werum PAS-X v3.2 | 4 | alarm consumer |
| C-08 | AD / Kerberos | (infra) | AuthN |

## 4. Functional Specifications

### 4.1 JMP Deployment

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DEP-01 | URS-DEP-01 | JMP installed on controlled workstations registered in site asset register `CRN-AR-WS-001`; license-server enforced concurrency. |
| FS-DEP-02 | URS-DEP-02 | JMP version locked at 18 Pro for the current CPV programme; upgrade gate requires change control + JSL revalidation pass. |
| FS-DEP-03 | URS-DEP-03 | GPO `GMP-Lab-Workstations` disables Office macros; JMP add-ins restricted to entries in `cv_jsl_signed_addins` registry. |

### 4.2 JSL Script Library

| FS ID | URS ID | Specification |
|---|---|---|
| FS-JSL-01 | URS-JSL-01 | JSL repo on validated GitLab `carina/spc-jsl`; signed commits via Sigstore gitsign; protected `main`. |
| FS-JSL-02 | URS-JSL-02 | Model Card markdown template `MODEL_CARD.md` required per script; CI gate blocks merge without it. |
| FS-JSL-03 | URS-JSL-03 | cosign-style detached signatures; load-time verification via JMP startup script `verify-signed.jsl`. |
| FS-JSL-04 | URS-JSL-04 | pytest-style harness for JSL via JMP scripting test harness `jmp-test-runner.jsl`; CI runs on every MR. |
| FS-JSL-05 | URS-JSL-05 | JMP add-in audit-log writes `(script_id, version, executor, timestamp, inputs_hash, outputs_hash)` to Splunk via syslog-ng forwarder. |

### 4.3 Control Chart Catalogue

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CHT-01 | URS-CHT-01 | Shewhart catalogue: X̄-R (subgroup variables), X̄-s (subgroup variables n ≥ 10), I-MR (individuals), p, np, c, u (attributes) per ISO 7870-2:2023. |
| FS-CHT-02 | URS-CHT-02 | EWMA (λ = 0.2, L = 3) + CUSUM (h = 4σ, k = 0.5σ) per ISO 7870-4 + 7870-6; defaults overridable per attribute config. |
| FS-CHT-03 | URS-CHT-03 | Multivariate: Hotelling T² + MEWMA via JMP Multivariate Methods; control limits per JMP defaults + statistician override. |
| FS-CHT-04 | URS-CHT-04 | Chart-decision register `cv_chart_decisions` per attribute (chart_type, subgroup, autocorrelation, rationale, qa_approver); rule activation requires QA approver. |

### 4.4 Capability + Performance Indices

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CAP-01 | URS-CAP-01 | JSL `compute_capability.jsl`: Anderson–Darling normality (α = 0.05); on rejection, Box–Cox transform via JMP Distribution platform or Clements non-parametric; ISO 22514-2 formulas. |
| FS-CAP-02 | URS-CAP-02 | Small-sample gating: n ≥ 30 valid; 10 ≤ n < 30 flagged "indicative"; n < 10 suppressed (`INSUFFICIENT_N`); rendered in CPV report. |
| FS-CAP-03 | URS-CAP-03 | Both Cp/Cpk (within-batch) + Pp/Ppk (overall) rendered side-by-side with variance-component plot. |
| FS-CAP-04 | URS-CAP-04 | Bissell 95 % CI on Cpk / Ppk via JMP Capability platform. |

### 4.5 OOC / OOT Detection Rules

| FS ID | URS ID | Specification |
|---|---|---|
| FS-OOC-01 | URS-OOC-01 | Western Electric Rules 1–4 via JMP Control Chart Rules; verified against AIAG SPC reference dataset in OQ. |
| FS-OOC-02 | URS-OOC-02 | Nelson Rules 1–8 via JMP; per-attribute activation flag. |
| FS-OOC-03 | URS-OOC-03 | Custom-rule JSL functions stored in JSL library; statistician approval gates activation. |
| FS-OOC-04 | URS-OOC-04 | Rule firing writes `(batch_id, attribute, rule_no, ruleset, ts, value)` to `cv_rule_firings`; idempotent eQMS deviation push on rule-violation-id. |
| FS-OOC-05 | URS-OOC-05 | ARL₀ table maintained in `cv_ruleset_arl_table`; ruleset with ARL₀ < 30 displays warning + requires statistician sign-off. |

### 4.6 Phase 1 vs Phase 2 Workflow

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PH-01 | URS-PH-01 | Phase 1 workflow JSL `establish_chart.jsl` requires ≥ 20 reference batches (configurable ≥ 25 per ASTM E2587); outputs trial limits + capability baseline + statistician + QA approval form. |
| FS-PH-02 | URS-PH-02 | Phase 1 → Phase 2 transition workflow locks limits via `cv_chart_limits.locked=true`; further change routes through change control. |
| FS-PH-03 | URS-PH-03 | Phase 2 workflow JSL `monitor_chart.jsl` applies locked limits + activated ruleset; OOC firings route via FS-OOC-04. |
| FS-PH-04 | URS-PH-04 | Limit-revision workflow requires ≥ 20 post-change batches + statistician approval; new revision number assigned + Phase 1 sub-workflow re-runs. |

### 4.7 Batch Genealogy Linkage

| FS ID | URS ID | Specification |
|---|---|---|
| FS-GEN-01 | URS-GEN-01 | Lakehouse genealogy schema `genealogy.batch_lineage` joined into every CPV record via JSL `link_genealogy.jsl`. |
| FS-GEN-02 | URS-GEN-02 | OOC firings linked to (step, equipment_train, raw_material_lot, operator, env_conditions) via genealogy + MES attributes. |
| FS-GEN-03 | URS-GEN-03 | `trace_forward.jsl` enumerates downstream-affected batches given a root-cause input (raw-material lot, equipment, etc.). |

### 4.8 Real-Time SPC Alerts

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RT-01 | URS-RT-01 | PI Notification subscriptions per critical attribute in `cv_rt_subscriptions`; latency ≤ 60 s measured per PQ-RT-01. |
| FS-RT-02 | URS-RT-02 | Alert router pushes to (MES Production Alarms + eQMS deviation create + Process Eng on-call PagerDuty); idempotency on alert-id. |
| FS-RT-03 | URS-RT-03 | Alert-suppression workflow captures (alert_id, suppression_reason, suppressed_by, ts, statistician_review_at); statistician review monthly. |

### 4.9 CPV Workflow

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CPV-01 | URS-CPV-01 | CPV cadence config per product / process in `cv_cpv_cadence`; cron triggers nightly. |
| FS-CPV-02 | URS-CPV-02 | Query versions stored in `cv_lakehouse_queries`; SHA-256 of query string captured at execution; data engineering co-signature on every revision. |
| FS-CPV-03 | URS-CPV-03 | CPV report Quarto template includes mandatory sections: charts, capability indices, trend, OOC/OOT, genealogy, CR summary. |
| FS-CPV-04 | URS-CPV-04 | Vault workflow `CRN-WF-CPV-001` enforces (Analyst → Senior Analyst → Statistician → Head of Manufacturing Sci → Head of QA) signatures. |
| FS-CPV-05 | URS-CPV-05 | Vault QualityDocs filing on final sign. |

### 4.10 Audit Trail / Part 11 / DI

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Lakehouse query log captures `(user, query_sha, ts)`; persisted ≥ 25 y. |
| FS-AUD-02 | URS-AUD-02 | JMP add-in audit log forwarded to Splunk; Splunk index retention ≥ 25 y. |
| FS-AUD-03 | URS-AUD-03 | Vault audit append-only on every CPV transition. |
| FS-AUD-04 | URS-AUD-04 | Retention ≥ 25 y across Vault + Splunk + lakehouse. |
| FS-PART11-50 | URS-PART11-50 | Vault e-signature manifestation. |
| FS-PART11-100 | URS-PART11-100 | AD uniqueness. |
| FS-PART11-200 | URS-PART11-200 | Re-auth at Vault signing. |
| FS-DI-01 | URS-DI-01 | AD principal attached to every audit event. |
| FS-DI-04 | URS-DI-04 | Lakehouse source data immutable (Delta time-travel); CPV record stores query SHA + execution ts. |
| FS-DI-05 | URS-DI-05 | OQ runs against AIAG SPC reference + ASTM E2587 examples. |

### 4.11 Integrations / Performance / Security / Training / PR

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-LAKE-01 | URS-INT-LAKE-01 | Authenticated query (OAuth2 client-credentials); service account in HashiCorp Vault; per-query audit log. |
| FS-INT-VAULT-01 | URS-INT-VAULT-01 | Vault QualityDocs REST push of CPV PDF + structured CSV + audit-trail export. |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | MasterControl REST deviation-create; idempotency key = rule-violation-id. |
| FS-INT-PI-01 | URS-INT-PI-01 | PI Notification subscription via PI Web API. |
| FS-INT-MES-01 | URS-INT-MES-01 | PAS-X Production Alarms via REST. |
| FS-INT-APR-01 | URS-INT-APR-01 | `GET /spc/api/v2/summary?product={p}` read-only consumed by APR / PQR tool. |
| FS-PERF-01 | URS-PERF-01 | CPV report ≤ 15 min on baseline workstation per PQ-PERF-CPV-RUN-01. |
| FS-SEC-01 | URS-SEC-01 | AD + MFA; quarterly access review. |
| FS-TRN-01 | URS-TRN-01 | Cornerstone curriculum `CRN-CURR-SPC-Analyst-v1`; SPC competency assessment includes Phase 1 / Phase 2 + capability + Nelson rules. |
| FS-PR-01 | URS-PR-01 | Annual periodic review per `CRN-PR-SPC-YYYYMMDD`. |


### 4.12 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem. Conditional-access binding to policy `Quality-App Conditional Access (MFA on first logon per session)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the SPC mart DB; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.13 Cross-System Integration — eQMS handover (M-XINT-EQMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-EQMS-01 | URS-XINT-EQMS-01 | CAPA-event publisher posts to eQMS endpoint `POST /capa/tickets` with mTLS + Entra workload-identity; payload schema `eqms.ticket.v1`; OpenAPI artefact `xint-eqms.openapi.yaml`; outbound retry with exponential back-off and DLQ at 5 attempts. |
| FS-XINT-EQMS-02 | URS-XINT-EQMS-02 | eQMS ticket-status webhook subscribed; payload `eqms.status.v1`; consumer rule maps eQMS status `(OPEN, IN-PROGRESS, EFFECTIVENESS, CLOSED)` onto originating-record disposition fields; closed-loop verification gate prevents disposition without `eqms_status=CLOSED`. |

## 5. Configuration Items (CI)

| CI ID | Item | Value |
|---|---|---|
| CI-01 | JMP version | 18 Pro (locked) |
| CI-02 | Shewhart catalogue | X̄-R, X̄-s, I-MR, p, np, c, u |
| CI-03 | Time-weighted defaults | EWMA λ=0.2, L=3; CUSUM h=4σ, k=0.5σ |
| CI-04 | Multivariate | Hotelling T², MEWMA |
| CI-05 | Normality gate | Anderson–Darling α=0.05 |
| CI-06 | Capability indices | Cp/Cpk/Pp/Ppk per ISO 22514-2 |
| CI-07 | Small-sample threshold | n<30 indicative; n<10 suppressed |
| CI-08 | Rules | Western Electric 1–4 + Nelson 1–8 + custom |
| CI-09 | ARL₀ threshold for sign-off | < 30 → statistician approval required |
| CI-10 | Phase 1 reference batches | ≥ 20 (configurable ≥ 25 per ASTM E2587) |
| CI-11 | Real-time alert latency | ≤ 60 s |
| CI-12 | Audit retention | ≥ 25 y |

## 6. Risks (FS-level)

| Risk | Mitigation |
|---|---|
| JSL defect | FS-JSL-04 + CI |
| Query version drift | FS-CPV-02 + query SHA capture |
| Chart parameter drift | FS-PH-02 + locked limits |
| Capability false-positive on non-normal data | FS-CAP-01 + Anderson–Darling |
| Western Electric false-alarm flood | FS-OOC-05 + ARL₀ gate |
| Real-time suppression masking true OOC | FS-RT-03 + statistician review |
| Audit-trail tampering | FS-AUD-02 + Splunk WORM index |

## 7. References

- CRN-URS-SPC-001 v1.2 (parent URS)
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200
- EU GMP Annex 11 §§ 4, 6, 9, 11
- ICH Q8(R2), Q9(R1), Q10, Q12
- FDA Process Validation 2011
- ASTM E2587-22; ISO 7870-1/-2/-4/-6/-8; ISO 22514-2:2017
- USP <1010>; PIC/S PI 041
- ISPE GAMP 5 (2nd Ed., 2022)
- SAS Institute — *JMP 18 Pro Reference*
- AVEVA PI System 2024 (KYM-URS-HIST-001 cross-reference)

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID | Notes |
|---|---|---|
| URS-DEP-01 | FS-DEP-01 | |
| URS-DEP-02 | FS-DEP-02 | |
| URS-DEP-03 | FS-DEP-03 | |
| URS-JSL-01 | FS-JSL-01 | |
| URS-JSL-02 | FS-JSL-02 | |
| URS-JSL-03 | FS-JSL-03 | |
| URS-JSL-04 | FS-JSL-04 | |
| URS-JSL-05 | FS-JSL-05 | |
| URS-CHT-01 | FS-CHT-01 | |
| URS-CHT-02 | FS-CHT-02 | |
| URS-CHT-03 | FS-CHT-03 | |
| URS-CHT-04 | FS-CHT-04 | |
| URS-CAP-01 | FS-CAP-01 | |
| URS-CAP-02 | FS-CAP-02 | |
| URS-CAP-03 | FS-CAP-03 | |
| URS-CAP-04 | FS-CAP-04 | |
| URS-OOC-01 | FS-OOC-01 | |
| URS-OOC-02 | FS-OOC-02 | |
| URS-OOC-03 | FS-OOC-03 | |
| URS-OOC-04 | FS-OOC-04 | |
| URS-OOC-05 | FS-OOC-05 | |
| URS-PH-01 | FS-PH-01 | |
| URS-PH-02 | FS-PH-02 | |
| URS-PH-03 | FS-PH-03 | |
| URS-PH-04 | FS-PH-04 | |
| URS-GEN-01 | FS-GEN-01 | |
| URS-GEN-02 | FS-GEN-02 | |
| URS-GEN-03 | FS-GEN-03 | |
| URS-RT-01 | FS-RT-01 | |
| URS-RT-02 | FS-RT-02 | |
| URS-RT-03 | FS-RT-03 | |
| URS-CPV-01 | FS-CPV-01 | |
| URS-CPV-02 | FS-CPV-02 | |
| URS-CPV-03 | FS-CPV-03 | |
| URS-CPV-04 | FS-CPV-04 | |
| URS-CPV-05 | FS-CPV-05 | |
| URS-AUD-01 | FS-AUD-01 | |
| URS-AUD-02 | FS-AUD-02 | |
| URS-AUD-03 | FS-AUD-03 | |
| URS-AUD-04 | FS-AUD-04 | |
| URS-PART11-50 | FS-PART11-50 | |
| URS-PART11-100 | FS-PART11-100 | |
| URS-PART11-200 | FS-PART11-200 | |
| URS-DI-01 | FS-DI-01 | |
| URS-DI-04 | FS-DI-04 | |
| URS-DI-05 | FS-DI-05 | |
| URS-INT-LAKE-01 | FS-INT-LAKE-01 | |
| URS-INT-VAULT-01 | FS-INT-VAULT-01 | |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 | |
| URS-INT-PI-01 | FS-INT-PI-01 | |
| URS-INT-MES-01 | FS-INT-MES-01 | |
| URS-INT-APR-01 | FS-INT-APR-01 | |
| URS-PERF-01 | FS-PERF-01 | |
| URS-SEC-01 | FS-SEC-01 | |
| URS-TRN-01 | FS-TRN-01 | |
| URS-PR-01 | FS-PR-01 | |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-EQMS-01 | FS-XINT-EQMS-01 |
| URS-XINT-EQMS-02 | FS-XINT-EQMS-02 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | JSL script defect causing biased CPV | Medium | High | URS-JSL-01..04 |
| R-02 | Query version drift undetected | Medium | High | URS-CPV-02 |
| R-03 | Audit-log gap | Medium | High | URS-AUD-02 |
| R-04 | User uses an unapproved add-in / ad-hoc JSL | Medium | Medium | URS-DEP-03 |
| R-05 | Chart parameter drift (limits not re-locked after Phase 2 revision) | Medium | High | URS-PH-02 + URS-PH-04 |
| R-06 | Capability index Cpk false-positive on non-normal data | Medium | High | URS-CAP-01 + Anderson–Darling gate |
| R-07 | Western Electric / Nelson false-alarm flood overwhelms eQMS | Medium | Medium | URS-OOC-05 + ARL₀ gate |
| R-08 | Real-time alert suppression masks a true OOC event | Low | High | URS-RT-03 + statistician review |

Full evaluation in `CRN-RA-SPC-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
