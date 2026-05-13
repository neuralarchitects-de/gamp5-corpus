---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (T3 catch-up: per-ID rows; CAPA-effectiveness gate, complaint-820.198 schema, ICH Q9(R1) risk register, APR / PQR compile pipeline, inspection-readiness tenant, PV integration)"
seed_corpus_basis:
  - "TLB-URS-EQMS-001 v1.0 (parent URS, T3)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 SaaS conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Part 820 §§ .30, .40, .70, .80, .90, .100, .198"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11; ICH Q9(R1); ICH Q10"
parent_urs:
  document_number: TLB-URS-EQMS-001
  version: 1.0
  file: ../../URS/_generated/final/eQMS_Electronic_Quality_Management_System__Talos_Bio_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## eQMS — MasterControl Manufacturing Excellence + QMS 2025 — Platform-Level Configuration

**Document Number:** TLB-FS-EQMS-001
**Version:** 1.1
**Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** TLB-URS-EQMS-001 v1.0
**Site:** Talos Bio AB, Gothenburg, Sweden *(fictional)*
**System Owner:** Head of Global QA Operations
**System Class:** GAMP Cat 4 — Configured Product (multi-tenant SaaS)
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 820; EU GMP Annex 11; ICH Q9(R1); ICH Q10

> **FS scope note.** This FS covers the platform-level configuration applied across processes (Deviation, CAPA, Change Control, Complaint, Audit, Supplier, Training Assignment, Risk Mgmt, APR / PQR, Inspection Readiness). Per-process detail (state machines, field schemas, role matrices) lives in process-FS sub-documents (`TLB-FS-EQMS-DEV-001`, `TLB-FS-EQMS-CAPA-001`, `TLB-FS-EQMS-CC-001`, `TLB-FS-EQMS-COMP-001`, `TLB-FS-EQMS-AUDIT-001`, `TLB-FS-EQMS-QRM-001`, `TLB-FS-EQMS-APR-001`, `TLB-FS-EQMS-INSP-001`).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of Global QA Operations) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Risk Management Lead) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-12 | (synthetic) | T3 catch-up to URS v1.0 expanded: per-ID rows; deviation root-cause / CAPA effectiveness gate / change-control impact + ICH Q9(R1) risk capture / complaint 820.198 schema + MDR-decision logic / audit-finding capture / risk register / APR compile / inspection-readiness tenant / PV integration. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies the platform-level configuration of MasterControl QMS 2025 to satisfy `TLB-URS-EQMS-001` v1.0 (T3). Per-process FS sub-documents specialise the workflow, field schema, and role matrix per process.

## 2. Scope

Tenancy configuration, process inventory (Deviation, CAPA, Change Control, Complaint, Audit, Supplier, Training, Risk Mgmt, APR / PQR, Inspection Readiness), SSO via Okta + MFA, integrations with Vault QualityDocs, Cornerstone, PAS-X, LIMS, clinical PV-DB; vendor-assurance program. Out: vendor infrastructure; per-process detail.

## 3. System Architecture

```
                ┌──────────────────────────────────────────────┐
                │            Okta IdP (SAML 2.0 + MFA)          │
                └────────────────────┬─────────────────────────┘
                                     │
   ┌─────────────────────────────────▼─────────────────────────────────┐
   │           MasterControl QMS 2025 (Talos Bio tenancy)              │
   │  ┌────────────┐ ┌──────┐ ┌─────┐ ┌──────────┐ ┌─────┐ ┌────────┐ │
   │  │ Deviation  │ │ CAPA │ │ CC  │ │ Complaint│ │ Aud │ │Supplier│ │
   │  └────────────┘ └──────┘ └─────┘ └──────────┘ └─────┘ └────────┘ │
   │  ┌─────────────┐ ┌──────────────────┐ ┌──────────────────────┐   │
   │  │ Training    │ │ Risk Mgmt (Q9R1) │ │ APR/PQR (Q10)         │   │
   │  └─────────────┘ └──────────────────┘ └──────────────────────┘   │
   │  ┌──────────────────────────────────────────────────────────────┐│
   │  │           Inspection Readiness Tenant (read-only)             ││
   │  └──────────────────────────────────────────────────────────────┘│
   └────────┬───────────┬───────────┬───────────┬──────────┬───────────┘
            │           │           │           │          │
            ▼           ▼           ▼           ▼          ▼
        Vault      Cornerstone  PAS-X      LIMS         PV-DB (PV signals)
       QualityDocs  LMS        deviations  OOS
```

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Notes |
|---|---|---|---|---|
| C-01 | MasterControl QMS 2025 tenancy | COTS SaaS | 4 | vendor-managed |
| C-02 | Process Workflows (×10) | COTS configuration | 4 | one FS sub-document per process |
| C-03 | Okta tenant | COTS infra | (infra) | SSO + MFA |
| C-04 | Vault QualityDocs | COTS SaaS | 4 | controlled-document references |
| C-05 | Cornerstone LMS | COTS SaaS | 4 | training-task counterparty |
| C-06 | PAS-X v3.2 | COTS MES | 4 | deviation-source counterparty |
| C-07 | LabWare LIMS 8 | COTS app | 4 | OOS deviation-source counterparty |
| C-08 | Clinical PV-DB | COTS app | 4 | post-market PV-signal counterparty |

## 4. Functional Specifications (platform-level)

### 4.1 Vendor Assurance (URS § 5.1)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VND-01 | URS-VND-01 | Vendor-assurance evidence (SOC 2 Type II, ISO 27001, HIPAA, customer-shared CSV summary) tracked in Vendor Quality Register; annual review; gaps tracked in eQMS. |
| FS-VND-02 | URS-VND-02 | Vendor-release evaluation runbook `TLB-RB-MC-RELEASE`: read release notes within 14 days; classify configuration impact; trigger re-validation where required. |
| FS-VND-03 | URS-VND-03 | Quarterly SLA review (≥ 99.7% availability) via vendor portal. |
| FS-VND-04 | URS-VND-04 | Vendor escalation runbook `TLB-RB-MC-ESCALATE` with named MasterControl contacts. |

### 4.2 Process Configuration Lifecycle (URS § 5.2)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PROC-01 | URS-PROC-01 | Each process workflow has a state machine documented in its sub-FS; states enforced server-side; out-of-state attempts rejected. |
| FS-PROC-02 | URS-PROC-02 | Configuration environments DEV → QC → UAT → PRODUCTION; only PRODUCTION runs live records; verified by `OQ-CONFIG-LIFECYCLE-01`. |
| FS-PROC-03 | URS-PROC-03 | Configuration deployment requires role-restricted signatures with SoD; verified by `OQ-CONFIG-DEPLOY-SIGN-01`. |
| FS-PROC-04 | URS-PROC-04 | Per-process UAT scripts cover each role's expected actions and exception paths; sign-off required before production deployment. |
| FS-PROC-05 | URS-PROC-05 | Configuration baseline export via `tlb-config-export.sh` archives workflows + security profiles. |

### 4.3 Deviation Lifecycle (URS § 5.3)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DEV-01 | URS-DEV-01 | Deviation record schema includes source, classification (Minor / Major / Critical), product / batch / equipment scope, root-cause, immediate actions, disposition; per-field validation server-side. |
| FS-DEV-02 | URS-DEV-02 | Critical deviations auto-route to QA distribution list within 24 h of creation; verified by `OQ-CRITICAL-ESCALATE-01`. |
| FS-DEV-03 | URS-DEV-03 | Root-cause analysis section captures method enum (5-Why / Ishikawa / FMEA-ref) + LIMS / PAS-X / EM evidence URNs. |
| FS-DEV-04 | URS-DEV-04 | Closure-gate `wf_dev_close` requires QA-Approver e-sig on `disposition_text` ≥ 100 chars; bare close blocked. |
| FS-DEV-05 | URS-DEV-05 | Quarterly trending report `tlb_rpt_dev_trend` by product / equipment / category. |
| FS-DEV-06 | URS-DEV-06 | Recurrence detector `tlb_dev_recurrence` flags same root-cause within 90 d; surfaces to Risk Owner inbox. |

### 4.4 CAPA Lifecycle and Effectiveness Check (URS § 5.4)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CAPA-01 | URS-CAPA-01 | CAPA-create requires `source_record_id` not-null; orphan-create blocked at API + UI. |
| FS-CAPA-02 | URS-CAPA-02 | Effectiveness review workflow `wf_capa_effectiveness` mandatory before CLOSED; criteria captured at CAPA creation; verified by `OQ-CAPA-EFFECTIVENESS-01`. |
| FS-CAPA-03 | URS-CAPA-03 | SoD enforced: `effectiveness_reviewer_id ≠ capa_owner_id`. |
| FS-CAPA-04 | URS-CAPA-04 | Ineffective outcome triggers `wf_capa_reopen_or_new`. |
| FS-CAPA-05 | URS-CAPA-05 | CAPA-aging report `tlb_rpt_capa_age`; > 180 d auto-escalates to VP QA. |
| FS-CAPA-06 | URS-CAPA-06 | Effectiveness-dashboard `tlb_dashboard_capa_eff` (rates per quarter). |

### 4.5 Change Control and Impact Assessment (URS § 5.5)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CC-01 | URS-CC-01 | Change-Control schema with seven impact-assessment categories (process / product / equipment / validation / regulatory / training / supply); per-field validation. |
| FS-CC-02 | URS-CC-02 | Approval matrix configurable per change-type; QA + regulatory + process-owner signatures required per the matrix; verified by `OQ-CC-MATRIX-SIGN-01`. |
| FS-CC-03 | URS-CC-03 | ICH Q9(R1) risk-capture form embedded in CR-create (severity × probability × detectability → RPN). |
| FS-CC-04 | URS-CC-04 | CR training-impact creates LMS task; closure requires LMS completion-flag. |
| FS-CC-05 | URS-CC-05 | CR regulatory-impact creates Regulatory-Affairs review task; variation / notification routed by RA. |
| FS-CC-06 | URS-CC-06 | Emergency CR workflow `wf_cc_emergency` with shortened approval; post-implementation review required. |

### 4.6 Complaint Handling per 21 CFR § 820.198 (URS § 5.6)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-COMP-01 | URS-COMP-01 | Complaint schema captures 820.198(e) fields: complainant_id, complaint_date, device_name, serial / lot, complaint_nature_text, investigation_outcome, reply_to_complainant, reply_date. |
| FS-COMP-02 | URS-COMP-02 | MDR-decision logic `wf_comp_mdr_decide`: device-failure / potential-reportable triggers within 24 h; MDR field captures decision + rationale. |
| FS-COMP-03 | URS-COMP-03 | PV-signal source-link via `IF-PV-IN`; related-CAPA FK supported. |
| FS-COMP-04 | URS-COMP-04 | Quarterly complaint-trend report per device family / failure mode. |
| FS-COMP-05 | URS-COMP-05 | Reply-SLA configurable per market / device class. |

### 4.7 Internal and External Audit Workflow (URS § 5.7)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-IA-01 | URS-AUD-IA-01 | Audit record schema: scope, plan, agenda, team, evidence URNs, observations, findings, CAPA-FK. |
| FS-AUD-IA-02 | URS-AUD-IA-02 | Internal audit plan via `tlb_audit_calendar`; missed audits create deviations. |
| FS-AUD-IA-03 | URS-AUD-IA-03 | External-audit schema with regulator enum (FDA / EMA / BfArM / Swissmedic / NB / MHRA) + finding-class + response-due-date. |
| FS-AUD-IA-04 | URS-AUD-IA-04 | Finding-class-to-CAPA routing matrix `tlb_audit_routing.yaml`. |

### 4.8 Quality Risk Management per ICH Q9(R1) (URS § 5.8)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-QRM-01 | URS-QRM-01 | Risk register schema: description, source, severity, probability, detectability, RPN, mitigation, residual, owner, review_date. |
| FS-QRM-02 | URS-QRM-02 | Cross-process FK links (deviation / CAPA / CR / complaint) supported via `risk_link` table. |
| FS-QRM-03 | URS-QRM-03 | RPN auto-recalc trigger on severity/probability/detectability change. |
| FS-QRM-04 | URS-QRM-04 | Risk-register review calendared per risk class via `tlb_qrm_review_cron`. |

### 4.9 Training and Competency (URS § 5.9)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Cornerstone tasks created via `IF-LMS-TASK-PUSH` for role curricula + read-and-understood. |
| FS-TRN-02 | URS-TRN-02 | Competency assessment workflow `wf_competency` for critical roles; record retained per HR + QMS. |
| FS-TRN-03 | URS-TRN-03 | Production access gating via Okta-claim from Cornerstone completion-flag. |
| FS-TRN-04 | URS-TRN-04 | Annual-refresher cron per quality-critical role. |

### 4.10 Supplier Quality and AVL (URS § 5.10)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SUPP-01 | URS-SUPP-01 | AVL maintained in `tlb_avl` with status + audit-cycle + scorecard + risk-class. |
| FS-SUPP-02 | URS-SUPP-02 | Procurement-system gate `tlb_proc_gate` denies non-AVL; emergency override requires Head-of-QA e-sig + deviation. |
| FS-SUPP-03 | URS-SUPP-03 | Audit calendar per risk class; missed → deviation. |
| FS-SUPP-04 | URS-SUPP-04 | Scorecard fields: OOS rate, OTD, complaint rate, audit findings. |

### 4.11 APR per ICH Q10 / 21 CFR § 211.180(e) (URS § 5.11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-APR-01 | URS-APR-01 | APR compile pipeline `tlb_apr_compile` pulls batch data + OOS/OOT + deviations + complaints + CRs + returns + stability + IPC via SQL views over Vault + LIMS + eQMS. |
| FS-APR-02 | URS-APR-02 | SoD: APR Author ≠ APR Approver ≠ QA Head; verified by `OQ-APR-SOD-01`. |
| FS-APR-03 | URS-APR-03 | Cadence per product / market via `tlb_apr_cadence`; overdue surfaces in dashboard. |
| FS-APR-04 | URS-APR-04 | APR outcome enum routes to CC `wf_cc_create_from_apr`. |

### 4.12 Inspection-Readiness Tenant (URS § 5.12)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INSP-01 | URS-INSP-01 | Separate read-only tenant `tlb-mc-inspection`; replicates curated record subset via `tlb_insp_replicator`. |
| FS-INSP-02 | URS-INSP-02 | Promotion workflow `wf_insp_promote` requires Inspection Tenant Curator e-sig. |
| FS-INSP-03 | URS-INSP-03 | Inspection dashboard `tlb_dashboard_insp` shows deviation / CAPA / complaint / finding aging. |
| FS-INSP-04 | URS-INSP-04 | Inspection runbook `TLB-RB-INSPECTION` accompanies tenant. |

### 4.13 Audit Trail / Part 11 (URS § 5.13 + 5.14)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AT-01 | URS-AT-01 | Audit trail captures all record state transitions, content edits, approvals, configuration changes, role assignments. |
| FS-AT-02 | URS-AT-02 | Append-only at MasterControl DB layer; CSV + PDF export. |
| FS-AT-03 | URS-AT-03 | Monthly QA Compliance review + quarterly platform-level review. |
| FS-AT-04 | URS-AT-04 | Retention 25 y; 50 y for selected processes via per-process retention policy. |
| FS-AT-05 | URS-AT-05 | Focused review tool `TLB-AUD-FOCUSED` filters to approvals / config changes / role grants / mass deletes. |
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural controls in `TLB-SOP-CSV-01`. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(b): PDF/A-3 + CSV exports verified by `OQ-INSPECTION-COPY-01`. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(d): Okta SAML 2.0 + MFA. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.50: printed name + ts + meaning at every signature. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.70: HMAC-SHA256 over record-hash + signer-id + ts. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.100: Okta uniqueness constraint. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.200: Okta re-auth max-age 5 min. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.300: Okta password policy. |
| FS-ANX11-01 | URS-ANX11-01 | Validation evidence inventory `TLB-VAL-EVID-INDEX`. |
| FS-ANX11-02 | URS-ANX11-02 | Server-side accuracy checks on entry boundaries. |

### 4.14 Integrations (URS § 5.15)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-VAULT-01 | URS-INT-VAULT-01 | Vault URN resolver `IF-VAULT-RESOLVE`; monthly reconciliation reports broken refs. |
| FS-INT-LMS-01 | URS-INT-LMS-01 | Cornerstone task push via `IF-LMS-TASK-PUSH`; idempotency key = CAPA-id + task-cycle. |
| FS-INT-PASX-01 | URS-INT-PASX-01 | PAS-X-originated deviations via `IF-PASX-DEV` REST POST with idempotency key = PAS-X-event-id; failed pushes alert within 5 min. |
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | LIMS OOS auto-creates deviations via `IF-LIMS-OOS` with idempotency key = LIMS-OOS-id. |
| FS-INT-PV-01 | URS-INT-PV-01 | PV-DB pushes safety signals via `IF-PV-IN` with idempotency key = PV-signal-id. |
| FS-INT-SSO-01 | URS-INT-SSO-01 | Okta SAML 2.0 + MFA. |

### 4.15 Data Integrity / Performance / Security (URS § 5.16 + 5.17)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | **Attributable:** `actor_id` not-null. |
| FS-DI-02 | URS-DI-02 | **Legible:** PDF / CSV export. |
| FS-DI-03 | URS-DI-03 | **Contemporaneous:** NTP-synced timestamps. |
| FS-DI-04 | URS-DI-04 | **Original:** content preserved; corrections audited. |
| FS-DI-05 | URS-DI-05 | **Accurate:** workflow logic validated under OQ. |
| FS-DI-06 | URS-DI-06 | **Complete / Consistent / Enduring / Available:** retrieval ≤ 4 h. |
| FS-PERF-01 | URS-PERF-01 | Record-open / list P95 ≤ 3 s. |
| FS-PERF-02 | URS-PERF-02 | APR compile typical product ≤ 30 min; benchmark via `PQ-APR-COMPILE-TIME-01`. |
| FS-AV-01 | URS-AV-01 | Vendor SLA monitored via vendor portal; deviations escalated. |
| FS-BAK-01 | URS-BAK-01 | Vendor-managed backup; site verifies vendor-published RPO ≤ 4 h, RTO ≤ 24 h via vendor-assurance program. |
| FS-BAK-02 | URS-BAK-02 | Annual configuration export (workflows + security profiles) for traceability; archived in eDMS. |
| FS-SEC-01 | URS-SEC-01 | Okta SSO + MFA; break-glass `TLB-MC-BREAKGLASS`. |
| FS-SEC-02 | URS-SEC-02 | Per-process / per-region access controls. |
| FS-SEC-03 | URS-SEC-03 | Bulk-export events tagged `BULK_EXPORT` in audit trail; surfaced in focused review. |

### 4.16 Training and Periodic Review (URS § 5.18)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-PR-01 | URS-TRN-PR-01 | Production access gated by completed role-specific LMS training. |
| FS-TRN-PR-02 | URS-TRN-PR-02 | Advanced QMS curriculum `TLB-CURR-QMS-ADV` for Risk Owners + APR Authors + Inspection Curators. |
| FS-PR-01 | URS-PR-01 | Annual periodic-review run-book `TLB-PR-EQMS-YYYYMMDD` covering configuration drift, audit-trail evidence, vendor-assurance status, integration health, training currency, CAPA-effectiveness rate, APR currency, inspection-tenant freshness; signed by Head of Global QA Operations + VP QA. |


### 4.17 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: SAML 2.0 via Entra ID with SCIM lifecycle provisioning. Conditional-access binding to policy `Quality-App Conditional Access (MFA + device-compliance for CAPA / deviation e-signature)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the MasterControl SQL backend; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.18 Cross-System Integration — Helios handover (M-XINT-HEL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HEL-01 | URS-XINT-HEL-01 | Audit-event publisher emits Kafka topic `helios.ingest.talos.mastercontrol.v1` with schema-registry-pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`; at-least-once delivery; idempotency key `{source_system, event_id}`; back-pressure surfaced via Prometheus `helios_publish_lag_seconds` with 5-min alert at > 600 s. |
| FS-XINT-HEL-02 | URS-XINT-HEL-02 | Local audit-store retention policy enforces ≥ 25 y; Helios ack persisted as `helios_ack_ts` per event; periodic reconciliation job verifies parity (Helios row count == local published count) and raises a deviation in MasterControl on > 0.01% mismatch over a 24 h window. |


### 4.19 Cross-System Integration — CAPA ingestion (M-XINT-EQMS-INGEST)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-EQMS-INGEST-01 | URS-XINT-EQMS-INGEST-01 | Endpoint `POST /capa/tickets` validates payload against `eqms.ticket.v1` JSON Schema; token-bucket rate-limiter at 100 req/min/source with burst 300; 429 returned on overflow with `Retry-After` header. |
| FS-XINT-EQMS-INGEST-02 | URS-XINT-EQMS-INGEST-02 | Dedup index on `(originating_system, originating_record_id, finding_class)` with 7-day window; mTLS client-cert validation against the site PKI; rejection on cert mismatch with audit-log entry `eqms.ingest.deny`. |
| FS-XINT-EQMS-INGEST-03 | URS-XINT-EQMS-INGEST-03 | MasterControl ticket schema extended with `originating_system` (free-text → enum) + `originating_record_id`; dashboard `eqms-quality-council` includes per-originating-system count + age + severity heat-map. |
| FS-XINT-EQMS-INGEST-04 | URS-XINT-EQMS-INGEST-04 | Status webhook publisher with exponential back-off (1s, 2s, 4s, 8s, … up to 10 attempts); DLQ topic `eqms.status.dlq`; signing-key per originating-system stored in Vault path `kv/eqms/webhook-keys/<system>`. |


### 4.20 Cross-System Integration — EDMS handover (M-XINT-EDMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-EDMS-01 | URS-XINT-EDMS-01 | eQMS publishes EDMS revision-request event `vellis.docrev.request.v1`; EDMS callback `vellis.doc.effective.v1` satisfies the EFFECTIVENESS gate; per-CAPA EDMS-document hyperlink rendered in MasterControl. |

## 5. Interface Specifications

| IF ID | URS ID | Counterparty | Protocol | Direction | Notes |
|---|---|---|---|---|---|
| IF-OKTA-01 | URS-INT-SSO-01 | Okta | SAML 2.0 | bidirectional | SSO + MFA |
| IF-VAULT-RESOLVE | URS-INT-VAULT-01 | Vault QualityDocs | REST | bidirectional | URN resolution |
| IF-LMS-TASK-PUSH | URS-INT-LMS-01 | Cornerstone | REST | outbound | training-task push |
| IF-PASX-DEV | URS-INT-PASX-01 | PAS-X | REST | inbound | deviation push (idempotent) |
| IF-LIMS-OOS | URS-INT-LIMS-01 | LabWare LIMS | REST | inbound | OOS deviation push (idempotent) |
| IF-PV-IN | URS-INT-PV-01 | Clinical PV-DB | REST | inbound | safety-signal push (idempotent) |

## 6. Data Model (high-level)

| Entity | Attributes |
|---|---|
| ProcessRecord | record_id, process_type, state, owner_id, attributes, created_at |
| Signature | sig_id, record_id, signer_id, meaning, ts, payload_hash |
| AuditEvent | event_id, record_id?, user_id, action, old, new, ts |
| ConfigBaseline | baseline_id, process_type, env, version, deployed_by, deployed_at |
| Linkage | linkage_id, source_record_id, target_record_id, link_type |
| RiskEntry | risk_id, description, severity, probability, detectability, rpn, owner, mitigation |
| AvlEntry | supplier_id, status, audit_cycle, risk_class, scorecard |
| AprBundle | apr_id, product_id, period_start, period_end, attached_records |

## 7. Non-Functional Specifications

| NFR ID | Specification |
|---|---|
| NFR-01 | P95 record-open / list ≤ 3 s |
| NFR-02 | APR compile ≤ 30 min typical product |
| NFR-03 | Availability per vendor SLA (≥ 99.7%) |
| NFR-04 | Audit trail append-only |
| NFR-05 | Retention ≥ 25 y (≥ 50 y selected processes) |
| NFR-06 | All integrations idempotent on source-event-id |

## 8. Configuration Items (CI)

| CI ID | Item | Configured Value | Source |
|---|---|---|---|
| CI-01 | IdP | Okta SAML 2.0 + MFA | URS-SEC-01 |
| CI-02 | Process environments | DEV, QC, UAT, PRODUCTION | URS-PROC-02 |
| CI-03 | Audit retention | ≥ 25 y; ≥ 50 y selected | URS-AT-04 |
| CI-04 | Critical-deviation escalation | 24 h to QA | URS-DEV-02 |
| CI-05 | CAPA effectiveness gate | required before CLOSED | URS-CAPA-02 |
| CI-06 | CC approval matrix | per change-type | URS-CC-02 |
| CI-07 | Vendor release evaluation | within 14 days | URS-VND-02 |
| CI-08 | Idempotency keys | source-event-id–based | URS-INT-PASX-01, URS-INT-LIMS-01, URS-INT-PV-01 |
| CI-09 | APR cadence default | annual per product | URS-APR-03 |
| CI-10 | Inspection-tenant promotion role | Inspection Tenant Curator | URS-INSP-02 |
| CI-11 | Risk-register review cadence | per risk class | URS-QRM-04 |
| CI-12 | Reply-to-complainant SLA | per market | URS-COMP-05 |

## 9. Constraints / Assumptions / Risks

- Constraints: vendor releases not under site CR; per-process FS sub-documents required.
- Assumptions: Okta, Vault, Cornerstone, PAS-X, LIMS, PV-DB validated.
- Risks: vendor-release silently changing config-affecting feature (FS-VND-02); CAPA effectiveness bypass via misconfigured workflow (FS-PROC-04 + UAT); idempotency failure causing duplicate deviations (FS-INT-PASX-01, FS-INT-LIMS-01); MDR-decision logic miss (FS-COMP-02); APR compile incomplete (FS-APR-01).

## 10. References

- TLB-URS-EQMS-001 v1.0 (parent URS).
- 21 CFR Part 11; 21 CFR Part 820 §§ .30, .40, .70, .80, .90, .100, .198; 21 CFR Part 211 §§ .180.
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- ICH Q9(R1); ICH Q10.
- ISO 13485:2016 §§ 8.2, 8.3, 8.5.
- ISPE GAMP 5 (2nd ed., 2022); PIC/S PI 041; ISO/IEC 27001:2022.
- MasterControl — *QMS 2025 Validation Approach*.

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-VND-01 | FS-VND-01 |
| URS-VND-02 | FS-VND-02 |
| URS-VND-03 | FS-VND-03 |
| URS-VND-04 | FS-VND-04 |
| URS-PROC-01 | FS-PROC-01 |
| URS-PROC-02 | FS-PROC-02 |
| URS-PROC-03 | FS-PROC-03 |
| URS-PROC-04 | FS-PROC-04 |
| URS-PROC-05 | FS-PROC-05 |
| URS-DEV-01 | FS-DEV-01 |
| URS-DEV-02 | FS-DEV-02 |
| URS-DEV-03 | FS-DEV-03 |
| URS-DEV-04 | FS-DEV-04 |
| URS-DEV-05 | FS-DEV-05 |
| URS-DEV-06 | FS-DEV-06 |
| URS-CAPA-01 | FS-CAPA-01 |
| URS-CAPA-02 | FS-CAPA-02 |
| URS-CAPA-03 | FS-CAPA-03 |
| URS-CAPA-04 | FS-CAPA-04 |
| URS-CAPA-05 | FS-CAPA-05 |
| URS-CAPA-06 | FS-CAPA-06 |
| URS-CC-01 | FS-CC-01 |
| URS-CC-02 | FS-CC-02 |
| URS-CC-03 | FS-CC-03 |
| URS-CC-04 | FS-CC-04 |
| URS-CC-05 | FS-CC-05 |
| URS-CC-06 | FS-CC-06 |
| URS-COMP-01 | FS-COMP-01 |
| URS-COMP-02 | FS-COMP-02 |
| URS-COMP-03 | FS-COMP-03 |
| URS-COMP-04 | FS-COMP-04 |
| URS-COMP-05 | FS-COMP-05 |
| URS-AUD-IA-01 | FS-AUD-IA-01 |
| URS-AUD-IA-02 | FS-AUD-IA-02 |
| URS-AUD-IA-03 | FS-AUD-IA-03 |
| URS-AUD-IA-04 | FS-AUD-IA-04 |
| URS-QRM-01 | FS-QRM-01 |
| URS-QRM-02 | FS-QRM-02 |
| URS-QRM-03 | FS-QRM-03 |
| URS-QRM-04 | FS-QRM-04 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-TRN-03 | FS-TRN-03 |
| URS-TRN-04 | FS-TRN-04 |
| URS-SUPP-01 | FS-SUPP-01 |
| URS-SUPP-02 | FS-SUPP-02 |
| URS-SUPP-03 | FS-SUPP-03 |
| URS-SUPP-04 | FS-SUPP-04 |
| URS-APR-01 | FS-APR-01 |
| URS-APR-02 | FS-APR-02 |
| URS-APR-03 | FS-APR-03 |
| URS-APR-04 | FS-APR-04 |
| URS-INSP-01 | FS-INSP-01 |
| URS-INSP-02 | FS-INSP-02 |
| URS-INSP-03 | FS-INSP-03 |
| URS-INSP-04 | FS-INSP-04 |
| URS-AT-01 | FS-AT-01 |
| URS-AT-02 | FS-AT-02 |
| URS-AT-03 | FS-AT-03 |
| URS-AT-04 | FS-AT-04 |
| URS-AT-05 | FS-AT-05 |
| URS-PART11-01 | FS-PART11-01 |
| URS-PART11-02 | FS-PART11-02 |
| URS-PART11-03 | FS-PART11-03 |
| URS-PART11-04 | FS-PART11-04 |
| URS-PART11-05 | FS-PART11-05 |
| URS-PART11-06 | FS-PART11-06 |
| URS-PART11-07 | FS-PART11-07 |
| URS-PART11-08 | FS-PART11-08 |
| URS-ANX11-01 | FS-ANX11-01 |
| URS-ANX11-02 | FS-ANX11-02 |
| URS-INT-VAULT-01 | FS-INT-VAULT-01 |
| URS-INT-LMS-01 | FS-INT-LMS-01 |
| URS-INT-PASX-01 | FS-INT-PASX-01 |
| URS-INT-LIMS-01 | FS-INT-LIMS-01 |
| URS-INT-PV-01 | FS-INT-PV-01 |
| URS-INT-SSO-01 | FS-INT-SSO-01 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-AV-01 | FS-AV-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-TRN-PR-01 | FS-TRN-PR-01 |
| URS-TRN-PR-02 | FS-TRN-PR-02 |
| URS-PR-01 | FS-PR-01 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-HEL-01 | FS-XINT-HEL-01 |
| URS-XINT-HEL-02 | FS-XINT-HEL-02 |
| URS-XINT-EQMS-INGEST-01 | FS-XINT-EQMS-INGEST-01 |
| URS-XINT-EQMS-INGEST-02 | FS-XINT-EQMS-INGEST-02 |
| URS-XINT-EQMS-INGEST-03 | FS-XINT-EQMS-INGEST-03 |
| URS-XINT-EQMS-INGEST-04 | FS-XINT-EQMS-INGEST-04 |
| URS-XINT-EDMS-01 | FS-XINT-EDMS-01 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Vendor release silently changing configuration-affecting feature | Medium | Medium | URS-VND-02 |
| R-02 | CAPA-effectiveness gate bypass | Low | Critical | URS-CAPA-02..04 |
| R-03 | Training-task bypass | Medium | High | URS-INT-LMS-01 |
| R-04 | Audit-trail tampering on vendor side | Low | Critical | URS-VND-01 |
| R-05 | Idempotency failure causing duplicate deviations | Medium | Medium | URS-INT-PASX-01, URS-INT-LIMS-01 |
| R-06 | MDR-decision logic miss on complaint | Low | Critical | URS-COMP-02 |
| R-07 | APR compilation incomplete | Medium | High | URS-APR-01 |
| R-08 | Risk-register stale (ICH Q9(R1) review missed) | Medium | Medium | URS-QRM-04 |
| R-09 | Inspection tenant exposes uncurated content | Low | Critical | URS-INSP-02 |
| R-10 | Supplier-non-AVL procurement | Low | High | URS-SUPP-02 |
| R-11 | Cross-process linkage break (Deviation → CAPA orphan) | Low | High | URS-CAPA-01 |
| R-12 | Bulk export of QMS data uncontrolled | Low | High | URS-SEC-03 |

Full evaluation in `TLB-RA-EQMS-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
