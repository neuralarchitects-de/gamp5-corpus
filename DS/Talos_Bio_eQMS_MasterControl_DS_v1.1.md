---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (v1.0 DS corpus ship)"
seed_corpus_basis:
  - "TLB-FS-EQMS-001 v1.1 (parent FS, T3 Cat 4)"
  - "TLB-URS-EQMS-001 v1.0 (parent URS, transitive)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 Configuration Specification conventions"
  - "21 CFR Part 11; 21 CFR Part 820; EU GMP Annex 11; ICH Q9(R1); ICH Q10; ICH Q12 (RIM linkage)"
  - "ISO 13485:2016; ISPE GAMP 5 (2nd ed., 2022); PIC/S PI 041; ISO/IEC 27001:2022"
  - "MasterControl QMS 2025 — Validation Approach + Configuration Reference"
parent_fs:
  document_number: TLB-FS-EQMS-001
  version: "1.1"
  file: ../../../FS_FDS/_generated/final/Talos_Bio_eQMS_MasterControl_FS_v1.3.md
parent_urs:
  document_number: TLB-URS-EQMS-001
  version: "1.1"
  file: ../../../URS/_generated/final/eQMS_Electronic_Quality_Management_System__Talos_Bio_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## eQMS — MasterControl Manufacturing Excellence + QMS 2025 — Talos Bio Gothenburg Tenancy

**Document Number:** TLB-DS-EQMS-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** TLB-FS-EQMS-001 v1.1
**Parent URS:** TLB-URS-EQMS-001 v1.0
**Site:** Talos Bio AB, Gothenburg, Sweden *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Project Mode:** Greenfield-SaaS (single Talos Bio tenancy; multi-process configuration)
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 820; EU GMP Annex 11; ICH Q9(R1); ICH Q10; ICH Q12 (RIM linkage)

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Head of Global QA Operations) | _____________ | _____________ | _____ |
| Reviewer (QA Reviewer) | _____________ | _____________ | _____ |
| Reviewer (System Owner — Head of Global QA Operations) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — VP QA) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (Risk Management Lead) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue. Inherited Tier T3 from parent URS+FS pair. DS covers 95/95 FS-IDs; 0 FS-IDs flagged as vendor-internal — no site design surface. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

| Term | Definition |
|---|---|
| CI | Configuration Item in MasterControl QMS 2025 |
| Process workflow | One of 10 process-specific workflows (Deviation, CAPA, Change Control, Complaint, Audit, Supplier, Training, Risk Mgmt, APR/PQR, Inspection-Readiness) |
| SoD | Separation of Duties enforced at signature submission |
| MDR | Medical-Device Reporting (21 CFR § 803) decision logic |
| APR | Annual Product Review per ICH Q10 / 21 CFR § 211.180(e) |
| Verified by | Planned IQ / OQ / PQ test |

## 1. Purpose

This Configuration Specification records the technical design of the MasterControl QMS 2025 tenancy at Talos Bio, including platform-level configuration across 10 process workflows, integration bindings, audit-trail tooling, and the inspection-readiness tenant. Per-process detail (deviation, CAPA, complaint state machines, field schemas, role matrices) is referenced from this DS but lives in per-process DS sub-documents.

## 2. Scope

**In scope:** MasterControl tenancy platform configuration; SSO via Okta + MFA; process inventory (Deviation, CAPA, Change Control, Complaint, Audit, Supplier, Training, Risk Mgmt, APR/PQR, Inspection-Readiness); integration bindings to Vault QualityDocs, Cornerstone LMS, PAS-X, LabWare LIMS, Clinical PV-DB; vendor-assurance program; inspection-readiness tenant replicator.

**Out of scope:** MasterControl vendor source-code internals; vendor infrastructure; Vault internals; Cornerstone internals; PAS-X internals; LIMS internals; PV-DB internals. Per-process DS sub-documents specialise the workflow / field-schema / role-matrix design.

## 3. Architectural Overview

The Talos Bio tenancy operates as a single multi-tenant SaaS instance with 10 process workflows configured atop the platform. Identity is federated via Okta (SAML 2.0 + MFA); cross-system integrations are configured as REST-based push/pull with idempotency keys at every counterparty boundary. The inspection-readiness tenant is a separate read-only replica.

```
                           ┌──────────────────────────────────┐
                           │   Okta SAML 2.0 + MFA            │
                           └──────────────────┬───────────────┘
                                              │
              ┌───────────────────────────────▼────────────────────────────────┐
              │  MasterControl QMS 2025 — Talos Bio tenancy                     │
              │  ┌────────────────────────────────────────────────────────┐    │
              │  │ Process Workflows (×10)                                  │    │
              │  │ Deviation / CAPA / Change Control / Complaint           │    │
              │  │ Audit / Supplier / Training / Risk Mgmt                  │    │
              │  │ APR/PQR / Inspection-Readiness                           │    │
              │  └────────────────────────────────────────────────────────┘    │
              │  ┌──────────────┐ ┌──────────────────┐ ┌──────────────────┐  │
              │  │ Workflow     │ │ Role-permission   │ │ Audit-trail       │  │
              │  │ Engine       │ │ matrix engine     │ │ + focused review  │  │
              │  └──────────────┘ └──────────────────┘ └──────────────────┘  │
              │  ┌────────────────────────────────────────────────────────┐  │
              │  │ Inspection-Readiness Tenant (read-only replica)         │  │
              │  │ Replicator: `tlb_insp_replicator`                       │  │
              │  └────────────────────────────────────────────────────────┘  │
              └──┬───────────┬───────────┬───────────┬──────────┬─────────────┘
                 │           │           │           │          │
                 ▼           ▼           ▼           ▼          ▼
            Vault        Cornerstone  PAS-X      LabWare    Clinical
            QualityDocs  LMS                     LIMS       PV-DB
            (URN)        (training)   (deviation) (OOS)     (PV signals)
```

### 3.1 Component-design inventory

| Layer | Component | Vendor / source | Version | Site design surface |
|---|---|---|---|---|
| Application | MasterControl tenancy | MasterControl | QMS 2025 | Configuration (§ 4) |
| Identity | Okta | Okta | per site IT | Configuration (§ 4, § 7) |
| Counterparty | Vault QualityDocs | Veeva | 24R3+ | Bindings (§ 7) |
| Counterparty | Cornerstone LMS | Cornerstone | 2025 | Bindings (§ 7) |
| Counterparty | PAS-X | Werum | 3.2 | Bindings (§ 7) |
| Counterparty | LabWare LIMS | LabWare | 8.0.4 | Bindings (§ 7) |
| Counterparty | Clinical PV-DB | per site | per site | Bindings (§ 7) |

---

## 4. Configuration Specification

### 4.1 Vendor Assurance bindings

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VND-01 | Vendor-quality register (`Vendor Quality Register.MasterControl`) | SOC 2 Type II + ISO 27001 + HIPAA + customer-shared CSV summary | Custom | Critical-vendor | FS-VND-01 | OQ-VND-REG-01 |
| DS-VND-02 | Release-eval runbook (`TLB-RB-MC-RELEASE`) | ≤ 14 d notes review; config-impact classification; re-validation trigger | Custom | Vendor-release cadence | FS-VND-02 | OQ-VND-REL-01 |
| DS-VND-03 | Quarterly SLA review | ≥ 99.7% availability via vendor portal | Default | Vendor portal | FS-VND-03 | OQ-VND-SLA-01 |
| DS-VND-04 | Escalation runbook (`TLB-RB-MC-ESCALATE`) | named MasterControl contacts | Custom | Operational escalation | FS-VND-04 | OQ-VND-ESCALATE-01 |

### 4.2 Process Configuration Lifecycle CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PROC-01 | Per-process state-machine binding | each workflow declares states server-side; out-of-state attempts rejected | Custom | Workflow integrity | FS-PROC-01 | OQ-PROC-STATE-01 |
| DS-PROC-02 | Environment topology (`PROC_ENVS`) | `DEV → QC → UAT → PRODUCTION` | Custom | Promotion discipline | FS-PROC-02 | OQ-CONFIG-LIFECYCLE-01 |
| DS-PROC-03 | Config-deploy signing | role-restricted; SoD `Config-Author` ≠ `Config-Approver` | Custom | Anti-tamper | FS-PROC-03 | OQ-CONFIG-DEPLOY-SIGN-01 |
| DS-PROC-04 | Per-process UAT script folders (`TLB-UAT-<process>/`) | per-role action + exception paths | Custom | UAT coverage | FS-PROC-04 | PQ-PROC-UAT-01 |
| DS-PROC-05 | Config-export script (`tlb-config-export.sh`) | archives workflows + security profiles | Custom | Site-side backup | FS-PROC-05 | OQ-CONFIG-EXPORT-01 |

### 4.3 Deviation Lifecycle CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-DEV-01 | Deviation schema fields | source, classification (`Minor/Major/Critical`), product/batch/equipment scope, root-cause, immediate actions, disposition | Custom | Per-field validation | FS-DEV-01 | OQ-DEV-SCHEMA-01 |
| DS-DEV-02 | Critical-deviation auto-route | QA distribution list within 24 h | Custom | Escalation cadence | FS-DEV-02 | OQ-CRITICAL-ESCALATE-01 |
| DS-DEV-03 | RCA method enum (`RCA_METHOD`) | `5-Why, Ishikawa, FMEA-ref` | Custom | Investigative discipline | FS-DEV-03 | OQ-RCA-METHOD-01 |
| DS-DEV-04 | Closure-gate workflow (`wf_dev_close`) | QA-Approver e-sig + `disposition_text ≥ 100 chars`; bare close blocked | Custom | Closure quality | FS-DEV-04 | OQ-DEV-CLOSE-01 |
| DS-DEV-05 | Quarterly trending report (`tlb_rpt_dev_trend`) | by product / equipment / category | Custom | Trending discipline | FS-DEV-05 | PQ-DEV-TREND-01 |
| DS-DEV-06 | Recurrence detector (`tlb_dev_recurrence`) | flags same root-cause within 90 d; surfaces to Risk Owner inbox | Custom | Repeat-finding visibility | FS-DEV-06 | OQ-DEV-RECURRENCE-01 |

### 4.4 CAPA Lifecycle CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CAPA-01 | CAPA-create constraint | `source_record_id NOT NULL`; orphan-create blocked at API + UI | Custom | Source-linkage discipline | FS-CAPA-01 | OQ-CAPA-ORPHAN-01 |
| DS-CAPA-02 | Effectiveness workflow (`wf_capa_effectiveness`) | mandatory before CLOSED; criteria captured at CAPA create | Custom | Effectiveness gate | FS-CAPA-02 | OQ-CAPA-EFFECTIVENESS-01 |
| DS-CAPA-03 | Effectiveness reviewer SoD | `effectiveness_reviewer_id ≠ capa_owner_id` | Custom | Independence | FS-CAPA-03 | OQ-CAPA-SOD-01 |
| DS-CAPA-04 | Ineffective-outcome workflow (`wf_capa_reopen_or_new`) | triggered automatically | Custom | Loop-back discipline | FS-CAPA-04 | OQ-CAPA-INEFFECTIVE-01 |
| DS-CAPA-05 | Aging report (`tlb_rpt_capa_age`) | > 180 d auto-escalates to VP QA | Custom | Aging escalation | FS-CAPA-05 | OQ-CAPA-AGING-01 |
| DS-CAPA-06 | Effectiveness dashboard (`tlb_dashboard_capa_eff`) | rates per quarter | Custom | KPI tracking | FS-CAPA-06 | PQ-CAPA-DASH-01 |

### 4.5 Change Control CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CC-01 | CR schema | 7 impact categories: process / product / equipment / validation / regulatory / training / supply | Custom | Multi-dimensional impact | FS-CC-01 | OQ-CR-SCHEMA-01 |
| DS-CC-02 | Approval matrix (`cr_approval_matrix`) | configurable per change-type | Custom | Routing flexibility | FS-CC-02 | OQ-CC-MATRIX-SIGN-01 |
| DS-CC-03 | ICH Q9(R1) risk form | `severity × probability × detectability → RPN`; embedded in CR-create | Custom | Quality risk management | FS-CC-03 | OQ-CC-Q9R1-01 |
| DS-CC-04 | Training-impact LMS task | created on CR with training-impact; closure requires LMS completion-flag | Custom | Training cycle binding | FS-CC-04 | OQ-CC-TRAINING-01 |
| DS-CC-05 | Regulatory-impact RA task | created on CR with reg-impact; variation/notification routed by RA | Custom | Regulatory binding | FS-CC-05 | OQ-CC-RA-01 |
| DS-CC-06 | Emergency CR workflow (`wf_cc_emergency`) | shortened approval; post-implementation review required | Custom | Operational continuity | FS-CC-06 | OQ-CC-EMERGENCY-01 |

### 4.6 Complaint CIs (21 CFR § 820.198)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COMP-01 | Complaint schema | per § 820.198(e): complainant_id, complaint_date, device_name, serial/lot, complaint_nature_text, investigation_outcome, reply_to_complainant, reply_date | Custom | Regulator-binding | FS-COMP-01 | OQ-COMPLAINT-SCHEMA-01 |
| DS-COMP-02 | MDR-decision workflow (`wf_comp_mdr_decide`) | device-failure / potential-reportable → 24 h; captures decision + rationale | Custom | MDR cadence | FS-COMP-02 | OQ-MDR-DECISION-01 |
| DS-COMP-03 | PV-signal source-link (`IF-PV-IN`) | related-CAPA FK supported | Custom | Cross-system linkage | FS-COMP-03 | OQ-PV-LINK-01 |
| DS-COMP-04 | Quarterly complaint-trend report | per device-family / failure-mode | Custom | Trending discipline | FS-COMP-04 | PQ-COMPLAINT-TREND-01 |
| DS-COMP-05 | Reply-SLA (`reply_sla_per_market`) | configurable per market / device class | Custom | Per-jurisdiction cadence | FS-COMP-05 | OQ-COMPLAINT-SLA-01 |

### 4.7 Internal and External Audit CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUD-IA-01 | Audit record schema | scope, plan, agenda, team, evidence URNs, observations, findings, CAPA-FK | Custom | Comprehensive trail | FS-AUD-IA-01 | OQ-AUDIT-IA-SCHEMA-01 |
| DS-AUD-IA-02 | Internal audit calendar (`tlb_audit_calendar`) | missed audits create deviations | Custom | Discipline | FS-AUD-IA-02 | OQ-AUDIT-IA-CAL-01 |
| DS-AUD-IA-03 | External-audit regulator enum (`EXT_AUDIT_REGULATOR`) | `FDA, EMA, BfArM, Swissmedic, NB, MHRA` | Custom | Multi-jurisdiction | FS-AUD-IA-03 | OQ-AUDIT-IA-REG-01 |
| DS-AUD-IA-04 | Finding-class routing matrix (`tlb_audit_routing.yaml`) | matrix file | Custom | Auto-routing | FS-AUD-IA-04 | OQ-AUDIT-IA-ROUTING-01 |

### 4.8 ICH Q9(R1) Quality Risk Management CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-QRM-01 | Risk register schema | description, source, severity, probability, detectability, RPN, mitigation, residual, owner, review_date | Custom | Q9(R1) | FS-QRM-01 | OQ-QRM-SCHEMA-01 |
| DS-QRM-02 | Cross-process FK (`risk_link`) | deviation / CAPA / CR / complaint | Custom | Cross-process linkage | FS-QRM-02 | OQ-QRM-LINK-01 |
| DS-QRM-03 | RPN auto-recalc trigger | on severity / probability / detectability change | Custom | Re-evaluation discipline | FS-QRM-03 | OQ-QRM-RECALC-01 |
| DS-QRM-04 | Review cron (`tlb_qrm_review_cron`) | per risk class | Custom | Review cadence | FS-QRM-04 | OQ-QRM-REVIEW-01 |

### 4.9 Training CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-TRN-01 | Cornerstone task push (`IF-LMS-TASK-PUSH`) | role curricula + R&U tasks | Custom | LMS binding | FS-TRN-01 | OQ-LMS-PUSH-01 |
| DS-TRN-02 | Competency workflow (`wf_competency`) | critical-role assessment record retained per HR + QMS | Custom | Competency discipline | FS-TRN-02 | OQ-COMPETENCY-01 |
| DS-TRN-03 | Production-access gating | Okta-claim from Cornerstone completion-flag | Custom | Untrained-access prevention | FS-TRN-03 | OQ-ACCESS-GATE-01 |
| DS-TRN-04 | Annual-refresher cron | per quality-critical role | Custom | Currency maintenance | FS-TRN-04 | OQ-REFRESHER-CRON-01 |

### 4.10 Supplier CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-SUPP-01 | AVL table (`tlb_avl`) | status + audit-cycle + scorecard + risk-class | Custom | AVL completeness | FS-SUPP-01 | OQ-AVL-SCHEMA-01 |
| DS-SUPP-02 | Procurement gate (`tlb_proc_gate`) | denies non-AVL; emergency override requires Head-of-QA e-sig + deviation | Custom | AVL discipline | FS-SUPP-02 | OQ-PROC-GATE-01 |
| DS-SUPP-03 | Audit calendar per risk class | missed → deviation | Custom | Discipline | FS-SUPP-03 | OQ-SUPP-AUDIT-CAL-01 |
| DS-SUPP-04 | Scorecard fields | OOS rate, OTD, complaint rate, audit findings | Custom | Multi-dim KPI | FS-SUPP-04 | OQ-SCORECARD-01 |

### 4.11 APR / PQR CIs (ICH Q10 / 21 CFR § 211.180(e))

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-APR-01 | APR compile pipeline (`tlb_apr_compile`) | pulls batch + OOS/OOT + deviations + complaints + CRs + returns + stability + IPC via SQL views over Vault + LIMS + eQMS | Custom | Multi-source compile | FS-APR-01 | PQ-APR-COMPILE-01 |
| DS-APR-02 | APR SoD | `Author ≠ Approver ≠ QA Head` | Custom | Independence | FS-APR-02 | OQ-APR-SOD-01 |
| DS-APR-03 | APR cadence (`tlb_apr_cadence`) | per product / market | Custom | Cadence config | FS-APR-03 | OQ-APR-CADENCE-01 |
| DS-APR-04 | APR-outcome routing (`wf_cc_create_from_apr`) | enum routes to CR | Custom | Action loop | FS-APR-04 | OQ-APR-ROUTING-01 |

### 4.12 Inspection-Readiness Tenant CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-INSP-01 | Inspection tenant (`tlb-mc-inspection`) | read-only replica; curated record subset | Custom | Inspection readiness | FS-INSP-01 | OQ-INSP-TENANT-01 |
| DS-INSP-02 | Replicator (`tlb_insp_replicator`) | curated-record replication scheduler | Custom | Curation discipline | FS-INSP-01 | OQ-INSP-REPLICATOR-01 |
| DS-INSP-03 | Promotion workflow (`wf_insp_promote`) | requires Inspection Tenant Curator e-sig | Custom | Curation gate | FS-INSP-02 | OQ-INSP-PROMOTE-01 |
| DS-INSP-04 | Inspection dashboard (`tlb_dashboard_insp`) | deviation / CAPA / complaint / finding aging | Custom | Inspector view | FS-INSP-03 | PQ-INSP-DASH-01 |
| DS-INSP-05 | Inspection runbook (`TLB-RB-INSPECTION`) | accompanies tenant | Custom | Operational doc | FS-INSP-04 | OQ-INSP-RB-01 |

### 4.13 Audit Trail / Part 11 CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AT-01 | Audit-trail coverage | all record state transitions, content edits, approvals, configuration changes, role assignments | Default | Native trail | FS-AT-01 | OQ-AT-COVERAGE-01 |
| DS-AT-02 | Append-only enforcement | MasterControl DB-layer; CSV + PDF export | Default | Vendor-managed | FS-AT-02 | OQ-AT-APPEND-01 |
| DS-AT-03 | Review cadence | monthly QA Compliance + quarterly platform-level | Custom | Annex 11 § 9 | FS-AT-03 | OQ-AT-REVIEW-01 |
| DS-AT-04 | Retention split (`AT_RET_YEARS=25`; selected `50`) | per-process retention policy | Custom | Long-term archive | FS-AT-04 | IQ-AT-RET-01 |
| DS-AT-05 | Focused review tool (`TLB-AUD-FOCUSED`) | filters to approvals / config / role grants / mass deletes | Custom | Reviewer efficiency | FS-AT-05 | OQ-AT-FOCUSED-01 |
| DS-PART11-01 | Procedural-control SOP (`TLB-SOP-CSV-01`) | linked from system docs | Custom | § 11.10(a) | FS-PART11-01 | OQ-SOP-LINK-01 |
| DS-PART11-02 | Export formats (`PDF/A-3, CSV`) | OQ-validated | Custom | § 11.10(b) | FS-PART11-02 | OQ-INSPECTION-COPY-01 |
| DS-PART11-03 | IdP (Okta SAML 2.0 + MFA) | enforced | Custom | § 11.10(d) | FS-PART11-03 | OQ-OKTA-MFA-01 |
| DS-PART11-04 | E-sig manifestation | `printedName + dateTime + meaning` | Default | § 11.50 | FS-PART11-04 | OQ-SIG-MANIFEST-01 |
| DS-PART11-05 | Signature binding | HMAC-SHA256 over record-hash + signer-id + ts | Default | § 11.70 | FS-PART11-05 | OQ-SIG-BINDING-01 |
| DS-PART11-06 | Account uniqueness | Okta uniqueness constraint | Custom | § 11.100 | FS-PART11-06 | OQ-ACCT-UNIQUE-01 |
| DS-PART11-07 | Re-auth max-age (`300 s`) | 5 min | Default | § 11.200 | FS-PART11-07 | OQ-SIG-REAUTH-01 |
| DS-PART11-08 | Password policy | per Okta + site InfoSec | Custom | § 11.300 | FS-PART11-08 | OQ-PWD-POLICY-01 |
| DS-PART11-09 | Validation evidence index (`TLB-VAL-EVID-INDEX`) | Annex 11 § 4 | Custom | Doc completeness | FS-ANX11-01 | OQ-VAL-EVID-IDX-01 |
| DS-PART11-10 | Accuracy checks | server-side at entry boundaries | Custom | Annex 11 § 6 | FS-ANX11-02 | OQ-ACCURACY-01 |

### 4.14 Integration CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-INT-VAULT-01 | Vault URN resolver (`IF-VAULT-RESOLVE`) | bidirectional REST; monthly reconciliation reports broken refs | Custom | Doc-binding | FS-INT-VAULT-01 | OQ-VAULT-RESOLVE-01 |
| DS-INT-LMS-01 | Cornerstone task push (`IF-LMS-TASK-PUSH`) | REST outbound; idempotency `CAPA-id + task-cycle` | Custom | Idempotent training cycle | FS-INT-LMS-01 | OQ-LMS-PUSH-INT-01 |
| DS-INT-PASX-01 | PAS-X deviation push (`IF-PASX-DEV`) | inbound REST POST; idempotency `PAS-X-event-id`; failure alert ≤ 5 min | Custom | Idempotent inbound | FS-INT-PASX-01 | OQ-PASX-DEV-IN-01 |
| DS-INT-LIMS-01 | LIMS OOS push (`IF-LIMS-OOS`) | inbound REST; idempotency `LIMS-OOS-id` | Custom | OOS auto-create | FS-INT-LIMS-01 | OQ-LIMS-OOS-01 |
| DS-INT-PV-01 | PV-DB safety-signal push (`IF-PV-IN`) | inbound REST; idempotency `PV-signal-id` | Custom | PV-signal binding | FS-INT-PV-01 | OQ-PV-IN-01 |
| DS-INT-SSO-01 | Okta SAML 2.0 + MFA | per realm `talos.okta.com` | Custom | Site IdP | FS-INT-SSO-01 | OQ-OKTA-SAML-01 |

### 4.15 Data Integrity / Performance / Security CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-DI-01 | `actor_id` not-null | DB constraint | Default | Attributable | FS-DI-01 | OQ-DI-ACTOR-01 |
| DS-DI-02 | PDF / CSV export | rendition default | Default | Legible | FS-DI-02 | OQ-DI-EXPORT-01 |
| DS-DI-03 | NTP-synced timestamps | server-side | Default | Contemporaneous | FS-DI-03 | OQ-DI-NTP-01 |
| DS-DI-04 | Content preservation; corrections audited | vendor default | Default | Original | FS-DI-04 | OQ-DI-ORIGINAL-01 |
| DS-DI-05 | Workflow-logic OQ | per-workflow | Custom | Accurate | FS-DI-05 | OQ-DI-WORKFLOW-01 |
| DS-DI-06 | Retrieval ≤ 4 h | inspection-tenant priority | Custom | Available | FS-DI-06 | PQ-DI-RETRIEVE-01 |
| DS-PERF-01 | Record-open / list P95 | ≤ 3 s | Custom | Vendor SLA | FS-PERF-01 | PQ-PERF-OPEN-01 |
| DS-PERF-02 | APR compile target | ≤ 30 min typical product | Custom | Performance benchmark | FS-PERF-02 | PQ-APR-COMPILE-TIME-01 |
| DS-AV-01 | Vendor SLA monitor | vendor portal | Default | Availability | FS-AV-01 | OQ-AV-SLA-01 |
| DS-BAK-01 | Vendor-managed backup verification | annual; RPO ≤ 4 h / RTO ≤ 24 h | Custom | Vendor-assurance | FS-BAK-01 | PQ-BAK-VERIFY-01 |
| DS-BAK-02 | Annual config export | workflows + security profiles → eDMS | Custom | Site-side preservation | FS-BAK-02 | OQ-CONFIG-EXPORT-02 |
| DS-SEC-01 | Okta SSO + MFA + break-glass (`TLB-MC-BREAKGLASS`) | monthly audit | Custom | Emergency continuity | FS-SEC-01 | OQ-BREAKGLASS-01 |
| DS-SEC-02 | Per-process / per-region access controls | RBAC enforced | Custom | Segregation | FS-SEC-02 | OQ-RBAC-01 |
| DS-SEC-03 | Bulk-export tag (`BULK_EXPORT`) | audit-trail tag; surfaced in focused review | Custom | Anti-exfil | FS-SEC-03 | OQ-BULK-EXPORT-TAG-01 |

### 4.16 Training and Periodic Review CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-TRN-PR-01 | Production-access gating | per-role LMS training | Custom | Untrained-access prevention | FS-TRN-PR-01 | OQ-ACCESS-GATE-02 |
| DS-TRN-PR-02 | Advanced curriculum (`TLB-CURR-QMS-ADV`) | Risk Owners + APR Authors + Inspection Curators | Custom | Critical-role training | FS-TRN-PR-02 | OQ-ADV-CURR-01 |
| DS-PR-01 | Annual periodic-review runbook (`TLB-PR-EQMS-YYYYMMDD`) | covers all domains; signed by Head of Global QA Operations + VP QA | Custom | Annex 11 § 11 | FS-PR-01 | PQ-PR-EQMS-01 |

### 4.17 Cross-System Bindings (M-XSYS / M-XINT)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-XSYS-AD-01 | Entra ID SAML 2.0 + SCIM | conditional-access policy `Quality-App Conditional Access` | Custom | Per FS-XSYS-AD-01 | FS-XSYS-AD-01 | OQ-XSYS-AD-01 |
| DS-XSYS-AD-02 | SIEM (`Splunk gxp-authn`) | RFC 5424 ≤ 5 min lag | Custom | Cross-system correlation | FS-XSYS-AD-01 | OQ-SIEM-FWD-01 |
| DS-XSYS-AD-03 | CyberArk PAM binding | 24 h rotation + dual-witness check-out | Custom | Break-glass | FS-XSYS-AD-01 | OQ-PAM-01 |
| DS-XSYS-BAK-01 | Veeam VSS + MS SQL Server | T1 tier; RPO ≤ 4 h / RTO ≤ 4 BH | Custom | Per FS-XSYS-BAK-01 | FS-XSYS-BAK-01 | OQ-VEEAM-01 |
| DS-XSYS-BAK-02 | S3 Object Lock COMPLIANCE bucket | geo-replicated | Custom | Anti-ransom | FS-XSYS-BAK-01 | IQ-S3-OBJLOCK-01 |
| DS-XSYS-BAK-03 | LTO-9 air-gap rotation | monthly | Custom | Air-gap policy | FS-XSYS-BAK-01 | OQ-LTO9-01 |
| DS-XSYS-BAK-04 | Restore-cert retention | ≥ 25 y in eQMS | Custom | Quality-record discipline | FS-XSYS-BAK-01 | OQ-RESTORE-CERT-01 |
| DS-XINT-HEL-01 | Helios Kafka topic (`helios.ingest.talos.mastercontrol.v1`) | idempotency `{source_system, event_id}` | Custom | Per FS-XINT-HEL-01 | FS-XINT-HEL-01 | OQ-HELIOS-PUB-01 |
| DS-XINT-HEL-02 | Helios lag alert (`HELIOS_LAG_ALERT_S=600`) | Prometheus | Custom | Back-pressure SLO | FS-XINT-HEL-01 | OQ-HELIOS-LAG-01 |
| DS-XINT-HEL-03 | Helios reconciliation cadence | daily 24 h window | Custom | Parity | FS-XINT-HEL-02 | OQ-HELIOS-RECON-01 |
| DS-XINT-EQMS-INGEST-01 | CAPA ingest endpoint (`POST /capa/tickets`) | `eqms.ticket.v1` JSON Schema; token-bucket 100 req/min/source w/ burst 300; 429 + Retry-After | Custom | Per FS-XINT-EQMS-INGEST-01 | FS-XINT-EQMS-INGEST-01 | OQ-CAPA-INGEST-01 |
| DS-XINT-EQMS-INGEST-02 | Dedup + mTLS | dedup `(originating_system, originating_record_id, finding_class)` 7-day window; mTLS cert mismatch → `eqms.ingest.deny` | Custom | Per FS-XINT-EQMS-INGEST-02 | FS-XINT-EQMS-INGEST-02 | OQ-CAPA-INGEST-DEDUP-01 |
| DS-XINT-EQMS-INGEST-03 | MasterControl ticket schema extension | `originating_system, originating_record_id`; dashboard `eqms-quality-council` | Custom | Per FS-XINT-EQMS-INGEST-03 | FS-XINT-EQMS-INGEST-03 | OQ-CAPA-INGEST-SCHEMA-01 |
| DS-XINT-EQMS-INGEST-04 | Status webhook publisher | exponential back-off (1s..8s..) up to 10 attempts; DLQ `eqms.status.dlq`; per-system Vault path `kv/eqms/webhook-keys/<system>` | Custom | Per FS-XINT-EQMS-INGEST-04 | FS-XINT-EQMS-INGEST-04 | OQ-CAPA-STATUS-WEBHOOK-01 |
| DS-XINT-EDMS-01 | EDMS revision-request event (`vellis.docrev.request.v1`) | callback `vellis.doc.effective.v1` satisfies EFFECTIVENESS gate | Custom | Per FS-XINT-EDMS-01 | FS-XINT-EDMS-01 | OQ-EDMS-DOCREV-01 |

---

## 5. Workflow + Business-Rule Design

### 5.1 Deviation closure workflow `wf_dev_close`

| Step | Actor | Gate |
|---|---|---|
| 1 | Deviation Owner | RCA captured; method enum selected |
| 2 | QA Reviewer | review |
| 3 | QA Approver | `disposition_text ≥ 100 chars` + e-sig |
| 4 | DB constraint | bare close (without disposition_text) blocked |
| 5 | Recurrence detector | flags repeat root-cause within 90 d |

### 5.2 CAPA effectiveness workflow `wf_capa_effectiveness`

| Step | Actor | Gate |
|---|---|---|
| 1 | CAPA Owner | implements action |
| 2 | Effectiveness Reviewer (≠ CAPA Owner) | criteria check; signs |
| 3 | If ineffective → `wf_capa_reopen_or_new` | new CAPA created |
| 4 | If effective → CLOSED | dashboard updated |

### 5.3 Complaint MDR-decision workflow `wf_comp_mdr_decide`

| Step | Actor | Gate |
|---|---|---|
| 1 | Complaint Owner | classifies device-failure / potential-reportable |
| 2 | MDR Decision Maker | decision + rationale captured in MDR field |
| 3 | If reportable → file MDR within 24 h | regulatory cadence |

### 5.4 APR compile pipeline `tlb_apr_compile` (per product)

1. Pull batch master from Vault QualityDocs via URN resolver
2. Pull deviations + CRs + complaints + CAPAs from MasterControl (per-product scope)
3. Pull OOS/OOT + IPC + stability data from LIMS via REST
4. Compile into APR template; SoD `Author ≠ Approver ≠ QA Head` enforced at promotion

### 5.5 Inspection-tenant promotion workflow `wf_insp_promote`

| Step | Actor | Gate |
|---|---|---|
| 1 | Inspection Tenant Curator | selects records for promotion |
| 2 | Curator e-sig | signs at promotion |
| 3 | Replicator (`tlb_insp_replicator`) | copies records to read-only tenant `tlb-mc-inspection` |

### 5.6 ICH Q9(R1) RPN auto-recalc business rule

When any of `severity / probability / detectability` on a `RiskEntry` row is UPDATEd, a DB trigger computes `RPN = severity × probability × detectability` and updates the row. Audit-trail entry written with old + new values.

---

## 6. Role-Permission Matrix Design

| Role | Deviation | CAPA | CC | Complaint | Audit-IA | Supplier | Training | QRM | APR | Inspection-Tenant | Config-Author | Config-Approver |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `QA-Reviewer` | R/W | R/W | R | R/W | R/W | R | – | R | R | R | – | – |
| `QA-Approver` | R/W | R/W | R/W | R/W | R/W | R/W | – | R/W | R/W | R | – | – |
| `CAPA-Owner` | – | R/W | – | – | – | – | – | – | – | – | – | – |
| `Effectiveness-Reviewer` | – | R/W | – | – | – | – | – | – | – | – | – | – |
| `CR-Approver` | – | – | R/W | – | – | – | – | – | – | – | – | – |
| `Complaint-Owner` | – | – | – | R/W | – | – | – | – | – | – | – | – |
| `MDR-Decision-Maker` | – | – | – | R/W | – | – | – | – | – | – | – | – |
| `Risk-Owner` | – | – | – | – | – | – | – | R/W | – | – | – | – |
| `APR-Author` | – | – | – | – | – | – | – | – | R/W | – | – | – |
| `APR-Approver` | – | – | – | – | – | – | – | – | R | – | – | – |
| `Inspection-Tenant-Curator` | – | – | – | – | – | – | – | – | – | R/W | – | – |
| `Config-Author` | – | – | – | – | – | – | – | – | – | – | R/W | – |
| `Config-Approver` | – | – | – | – | – | – | – | – | – | – | R | R/W |
| `VP-QA` | R/W | R/W | R/W | R/W | R/W | R/W | R/W | R/W | R/W | R/W | – | R/W |
| `Audit-Reviewer` | R | R | R | R | R | R | R | R | R | R | – | – |

SoD constraints at sig submission: `effectiveness_reviewer_id ≠ capa_owner_id`; `APR Author ≠ APR Approver ≠ QA Head`; `Config-Author ∩ Config-Approver = ∅`.

---

## 7. Integration Design

### 7.1 Vault URN resolver (FS-INT-VAULT-01)

- Endpoint: bidirectional REST `https://vault.vellis.local/api/v23.3/objects/documents__v/{urn}`
- AuthN: mTLS + bearer
- Use: doc-binding for SOPs / specs / batch records
- Monthly reconciliation: `tlb_rpt_vault_reconcile` lists broken refs

### 7.2 Cornerstone task push (FS-INT-LMS-01)

- Endpoint: `POST https://lms.vega.local/api/v2/tasks`
- AuthN: mTLS + bearer
- Idempotency: `CAPA-id + task-cycle`

### 7.3 PAS-X deviation push (FS-INT-PASX-01)

- Endpoint: inbound `POST https://eqms.talos.local/api/v2/deviations`
- AuthN: mTLS + bearer from PAS-X
- Idempotency: header `Idempotency-Key: pasx:event:<id>`
- Failure: 5-min alert via Prometheus `pasx_push_error_rate`

### 7.4 LIMS OOS auto-create (FS-INT-LIMS-01)

- Endpoint: inbound `POST https://eqms.talos.local/api/v2/deviations`
- AuthN: mTLS + bearer from LIMS
- Idempotency: header `Idempotency-Key: lims:oos:<id>`

### 7.5 PV-DB safety-signal push (FS-INT-PV-01)

- Endpoint: inbound `POST https://eqms.talos.local/api/v2/complaints`
- AuthN: mTLS + bearer from PV-DB
- Idempotency: header `Idempotency-Key: pv:signal:<id>`

### 7.6 Okta SSO + MFA (FS-INT-SSO-01)

- Protocol: SAML 2.0 + SCIM 2.0
- MFA: TOTP / WebAuthn at every sig event
- Re-auth max-age: 300 s

### 7.7 CAPA ingest from upstream systems (FS-XINT-EQMS-INGEST-01..04)

- Endpoint: `POST /capa/tickets`
- Schema: `eqms.ticket.v1`
- Rate-limit: token-bucket 100 req/min/source + burst 300
- Dedup: 7-day window on `(originating_system, originating_record_id, finding_class)`
- Status webhook: exponential back-off + DLQ `eqms.status.dlq`

### 7.8 EDMS handover (FS-XINT-EDMS-01)

- Outbound revision-request: `vellis.docrev.request.v1`
- Inbound callback: `vellis.doc.effective.v1` → satisfies EFFECTIVENESS gate
- Per-CAPA EDMS-document hyperlink rendered in UI

### 7.9 Helios audit-event handover (FS-XINT-HEL-01..02)

- Kafka topic: `helios.ingest.talos.mastercontrol.v1`
- Schema-registry pinned envelope; at-least-once delivery
- Reconciliation: daily 24 h window

---

## 8. Site-Deployed Components Design

MasterControl is operated as a pure Cat 4 SaaS at Talos Bio — no site-developed code is in scope. All integration adapters (Vault resolver, LMS push, PAS-X / LIMS / PV inbound endpoints, EDMS event handler, Helios publisher) are realised through MasterControl's native REST configuration plus the platform's Workflow Engine. No § 8 mini-SDS sub-sections are required for v1.0.

---

## 9. References

### US
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- 21 CFR Part 820 §§ .30, .40, .70, .80, .90, .100, .198
- 21 CFR Part 211 §§ .180

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11

### DACH
- BfArM (DE) — informational reference

### International
- ICH Q9(R1); ICH Q10; ICH Q12 (RIM linkage)
- ISO 13485:2016 §§ 8.2, 8.3, 8.5
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE GAMP GPG *Records & Data Integrity*
- PIC/S PI 041
- ISO/IEC 27001:2022

### Vendor
- MasterControl — *QMS 2025 Validation Approach + Configuration Reference*
- MasterControl — *Workflow Engine Administrator Guide*

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-VND-01 | FS-VND-01 |
| DS-VND-02 | FS-VND-02 |
| DS-VND-03 | FS-VND-03 |
| DS-VND-04 | FS-VND-04 |
| DS-PROC-01 | FS-PROC-01 |
| DS-PROC-02 | FS-PROC-02 |
| DS-PROC-03 | FS-PROC-03 |
| DS-PROC-04 | FS-PROC-04 |
| DS-PROC-05 | FS-PROC-05 |
| DS-DEV-01 | FS-DEV-01 |
| DS-DEV-02 | FS-DEV-02 |
| DS-DEV-03 | FS-DEV-03 |
| DS-DEV-04 | FS-DEV-04 |
| DS-DEV-05 | FS-DEV-05 |
| DS-DEV-06 | FS-DEV-06 |
| DS-CAPA-01 | FS-CAPA-01 |
| DS-CAPA-02 | FS-CAPA-02 |
| DS-CAPA-03 | FS-CAPA-03 |
| DS-CAPA-04 | FS-CAPA-04 |
| DS-CAPA-05 | FS-CAPA-05 |
| DS-CAPA-06 | FS-CAPA-06 |
| DS-CC-01 | FS-CC-01 |
| DS-CC-02 | FS-CC-02 |
| DS-CC-03 | FS-CC-03 |
| DS-CC-04 | FS-CC-04 |
| DS-CC-05 | FS-CC-05 |
| DS-CC-06 | FS-CC-06 |
| DS-COMP-01 | FS-COMP-01 |
| DS-COMP-02 | FS-COMP-02 |
| DS-COMP-03 | FS-COMP-03 |
| DS-COMP-04 | FS-COMP-04 |
| DS-COMP-05 | FS-COMP-05 |
| DS-AUD-IA-01 | FS-AUD-IA-01 |
| DS-AUD-IA-02 | FS-AUD-IA-02 |
| DS-AUD-IA-03 | FS-AUD-IA-03 |
| DS-AUD-IA-04 | FS-AUD-IA-04 |
| DS-QRM-01 | FS-QRM-01 |
| DS-QRM-02 | FS-QRM-02 |
| DS-QRM-03 | FS-QRM-03 |
| DS-QRM-04 | FS-QRM-04 |
| DS-TRN-01 | FS-TRN-01 |
| DS-TRN-02 | FS-TRN-02 |
| DS-TRN-03 | FS-TRN-03 |
| DS-TRN-04 | FS-TRN-04 |
| DS-SUPP-01 | FS-SUPP-01 |
| DS-SUPP-02 | FS-SUPP-02 |
| DS-SUPP-03 | FS-SUPP-03 |
| DS-SUPP-04 | FS-SUPP-04 |
| DS-APR-01 | FS-APR-01 |
| DS-APR-02 | FS-APR-02 |
| DS-APR-03 | FS-APR-03 |
| DS-APR-04 | FS-APR-04 |
| DS-INSP-01 | FS-INSP-01 |
| DS-INSP-02 | FS-INSP-01 |
| DS-INSP-03 | FS-INSP-02 |
| DS-INSP-04 | FS-INSP-03 |
| DS-INSP-05 | FS-INSP-04 |
| DS-AT-01 | FS-AT-01 |
| DS-AT-02 | FS-AT-02 |
| DS-AT-03 | FS-AT-03 |
| DS-AT-04 | FS-AT-04 |
| DS-AT-05 | FS-AT-05 |
| DS-PART11-01 | FS-PART11-01 |
| DS-PART11-02 | FS-PART11-02 |
| DS-PART11-03 | FS-PART11-03 |
| DS-PART11-04 | FS-PART11-04 |
| DS-PART11-05 | FS-PART11-05 |
| DS-PART11-06 | FS-PART11-06 |
| DS-PART11-07 | FS-PART11-07 |
| DS-PART11-08 | FS-PART11-08 |
| DS-PART11-09 | FS-ANX11-01 |
| DS-PART11-10 | FS-ANX11-02 |
| DS-INT-VAULT-01 | FS-INT-VAULT-01 |
| DS-INT-LMS-01 | FS-INT-LMS-01 |
| DS-INT-PASX-01 | FS-INT-PASX-01 |
| DS-INT-LIMS-01 | FS-INT-LIMS-01 |
| DS-INT-PV-01 | FS-INT-PV-01 |
| DS-INT-SSO-01 | FS-INT-SSO-01 |
| DS-DI-01 | FS-DI-01 |
| DS-DI-02 | FS-DI-02 |
| DS-DI-03 | FS-DI-03 |
| DS-DI-04 | FS-DI-04 |
| DS-DI-05 | FS-DI-05 |
| DS-DI-06 | FS-DI-06 |
| DS-PERF-01 | FS-PERF-01 |
| DS-PERF-02 | FS-PERF-02 |
| DS-AV-01 | FS-AV-01 |
| DS-BAK-01 | FS-BAK-01 |
| DS-BAK-02 | FS-BAK-02 |
| DS-SEC-01 | FS-SEC-01 |
| DS-SEC-02 | FS-SEC-02 |
| DS-SEC-03 | FS-SEC-03 |
| DS-TRN-PR-01 | FS-TRN-PR-01 |
| DS-TRN-PR-02 | FS-TRN-PR-02 |
| DS-PR-01 | FS-PR-01 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 |
| DS-XSYS-AD-02 | FS-XSYS-AD-01 |
| DS-XSYS-AD-03 | FS-XSYS-AD-01 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| DS-XSYS-BAK-02 | FS-XSYS-BAK-01 |
| DS-XSYS-BAK-03 | FS-XSYS-BAK-01 |
| DS-XSYS-BAK-04 | FS-XSYS-BAK-01 |
| DS-XINT-HEL-01 | FS-XINT-HEL-01 |
| DS-XINT-HEL-02 | FS-XINT-HEL-01 |
| DS-XINT-HEL-03 | FS-XINT-HEL-02 |
| DS-XINT-EQMS-INGEST-01 | FS-XINT-EQMS-INGEST-01 |
| DS-XINT-EQMS-INGEST-02 | FS-XINT-EQMS-INGEST-02 |
| DS-XINT-EQMS-INGEST-03 | FS-XINT-EQMS-INGEST-03 |
| DS-XINT-EQMS-INGEST-04 | FS-XINT-EQMS-INGEST-04 |
| DS-XINT-EDMS-01 | FS-XINT-EDMS-01 |

---

## 11. Design-level Risk Register

| ID | Design-level risk | Origin (DS-ID / design choice) | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|---|
| DR-01 | MasterControl release silently changes a configured workflow behaviour | DS-VND-02 + DS-PROC-01 | Medium | Medium | Release-eval runbook; UAT regression |
| DR-02 | CAPA effectiveness gate bypass via misconfigured workflow | DS-CAPA-02 + DS-PROC-04 | Low | Critical | UAT scripts (DS-PROC-04); OQ-CAPA-EFFECTIVENESS-01 |
| DR-03 | Training-task bypass — production access granted before LMS completion | DS-TRN-03 + DS-INT-LMS-01 | Medium | High | Access-gate test (OQ-ACCESS-GATE-01); SCIM lifecycle |
| DR-04 | Audit-trail tampering on vendor side | DS-AT-02 + DS-VND-01 | Low | Critical | Vendor-assurance dependency; quarterly QA review |
| DR-05 | Idempotency failure causing duplicate deviations from PAS-X/LIMS | DS-INT-PASX-01 + DS-INT-LIMS-01 | Medium | Medium | Idempotency-key uniqueness OQ |
| DR-06 | MDR-decision logic miss on complaint (24 h window) | DS-COMP-02 | Low | Critical | OQ-MDR-DECISION-01 + 24 h timer test |
| DR-07 | APR compile incomplete (LIMS / Vault outage during compile) | DS-APR-01 + DS-INT-LIMS-01 + DS-INT-VAULT-01 | Medium | High | Re-try logic + completeness check at compile end |
| DR-08 | Risk-register stale (ICH Q9(R1) review missed) | DS-QRM-04 | Medium | Medium | Review cron + dashboard surface |
| DR-09 | Inspection tenant exposes uncurated content (replicator scope drift) | DS-INSP-02 + DS-INSP-03 | Low | Critical | Promotion workflow + Curator e-sig (DS-INSP-03) |
| DR-10 | Supplier-non-AVL procurement (emergency override missing deviation) | DS-SUPP-02 | Low | High | Override requires Head-of-QA + deviation; OQ-PROC-GATE-01 |
| DR-11 | Cross-process linkage break (Deviation → CAPA orphan) | DS-CAPA-01 | Low | High | NOT NULL constraint (DS-CAPA-01) |
| DR-12 | Bulk-export of QMS data uncontrolled | DS-SEC-03 | Low | High | Bulk-export tag; focused-review surface (DS-AT-05) |
| DR-13 | Recurrence detector false negatives — same root-cause not flagged | DS-DEV-06 | Medium | High | RCA taxonomy review; OQ-DEV-RECURRENCE-01 |
| DR-14 | APR SoD bypass — APR Author ≠ APR Approver enforced but QA Head signs both | DS-APR-02 | Low | High | Triple-distinct rule + OQ-APR-SOD-01 |
| DR-15 | CAPA ingest endpoint rate-limit bypass via burst spam | DS-XINT-EQMS-INGEST-01 | Low | Medium | Token-bucket + 429 + dedup window |
| DR-16 | CAPA ingest dedup window (7 d) misses legitimate re-submission of same finding | DS-XINT-EQMS-INGEST-02 | Low | Medium | Dedup-bypass admin operation logged + reviewed |
| DR-17 | EDMS revision-request callback fails — CAPA stuck at EFFECTIVENESS gate | DS-XINT-EDMS-01 | Low | High | Callback retry + manual unblock workflow |
| DR-18 | Helios reconciliation false-positive raises noise deviations | DS-XINT-HEL-03 | Medium | Low | Tunable threshold; deviation suppression review |
| DR-19 | Inspection-tenant replicator delay during inspection — stale data shown to regulator | DS-INSP-02 | Low | High | Replicator health-check + freshness alert |
| DR-20 | Okta MFA bypass via SAML-session replay | DS-INT-SSO-01 + DS-PART11-07 | Low | Critical | Re-auth at signing (5 min); session anomaly detection |
| DR-21 | Vendor support-portal exposes Talos-config to other tenants via shared session | DS-VND-01 | Low | High | Vendor-assurance dependency; quarterly portal-access review |
| DR-22 | PV-DB signal duplicate via different idempotency keys | DS-INT-PV-01 | Low | Medium | Server-side dedup on `(complaint_date, device_name, lot)` |

The full formal Risk Assessment is `TLB-RA-EQMS-001` (synthetic, separate document).

---

## 12. Appendix B — Inspection-Readiness Tenant + Cross-Process Linkage Design Narrative

### 12.1 Why the Inspection-Readiness tenant exists

When an inspector arrives — FDA pre-approval, EMA GMP, BfArM follow-up, Swissmedic surveillance, MHRA risk-based, an internal audit — the productive eQMS tenant is the wrong artefact to put in front of them. It contains in-flight investigations, draft CAPAs that may resolve differently, unrelated processes, role-permission detail that distracts from the inspection topic, and live links that change underfoot. The Inspection-Readiness tenant `tlb-mc-inspection` is a separate read-only replica that holds only the curated record subset relevant to the inspection scope.

### 12.2 Curation discipline

The Inspection Tenant Curator role is the gatekeeper. The promotion workflow `wf_insp_promote` requires:
1. Curator selects records (deviation / CAPA / complaint / audit-finding / supplier / training-record / APR) by inspection-scope filter
2. Per-record review: are the linked CRs / CAPAs / source-records also needed? are PII / privileged-attorney-client communications excluded?
3. Curator re-auth + e-sig on the curation manifest
4. Replicator `tlb_insp_replicator` copies records to `tlb-mc-inspection` (read-only)
5. Inspector receives a per-inspection access scope on the inspection tenant — never on production

### 12.3 Cross-process linkage design

Talos Bio's 10 processes are linked by foreign keys in MasterControl native + by audit-trail cross-references. The design choice is to make linkage explicit and queryable, not implicit:

| Source process | Target process | Link table / mechanism |
|---|---|---|
| Deviation | CAPA | `deviation.related_capa_ids[]` FK |
| Deviation | Risk Mgmt | `risk_link` table cross-process FK |
| CAPA | Change Control | `capa.cr_refs[]` |
| Complaint | CAPA | `complaint.related_capa_ids[]` |
| Complaint | Risk Mgmt | via `risk_link` |
| Audit Finding | CAPA | `audit_finding.capa_fk` |
| Supplier | Deviation | `supplier_deviation_log` |
| Supplier | Risk Mgmt | via `risk_link` |
| APR | Change Control | `wf_cc_create_from_apr` |
| APR | Deviation / OOS / OOT | SQL views over `LW_RESULT` + `LW_DEVIATION` |
| Training | CAPA | `IF-LMS-TASK-PUSH` idempotency `CAPA-id + task-cycle` |
| Training | Change Control | `cc.training_impact` triggers LMS task |
| Change Control | Risk Mgmt | `cr.q9r1_risk_form` embedded |
| Inspection Tenant | Any | `tlb_insp_replicator` curated subset |

### 12.4 APR compile pipeline design — per ICH Q10

The APR compile pipeline `tlb_apr_compile` is the single most data-intensive cross-system operation. Design choices:

| Concern | Choice |
|---|---|
| Data sources | Vault (batch master, MBR, controlled docs); LIMS (results, OOS, OOT, IPC, stability); eQMS (deviations, CAPAs, CRs, complaints, returns) |
| Composition pattern | SQL views materialised per product per APR cycle |
| Performance target | ≤ 30 min typical product (FS-PERF-02); validated by PQ-APR-COMPILE-TIME-01 |
| Authority | APR Author writes draft; APR Approver (≠ Author) reviews; QA Head (≠ both) approves |
| Idempotency | Re-runs are deterministic against the same data window; results identical |
| Failure handling | Partial-compile state recorded; missing data sources surfaced explicitly |
| Output format | PDF/A-3 with embedded data dictionary + signature page |

### 12.5 ICH Q9(R1) risk-register design — cross-process FK

`risk_link` is the table that lets a single Risk Register entry cross-reference deviations, CAPAs, CRs, and complaints. Design pattern:

```
RiskEntry {
  risk_id, description, source,
  severity, probability, detectability, rpn,  -- auto-recalc on UPDATE
  mitigation, residual, owner, review_date
}

risk_link {
  link_id, risk_id FK, target_record_id, target_record_type,
  link_type ("source" | "mitigation_evidence" | "residual_evidence")
}
```

Querying the linkage table during APR compile gives a unified view of "what risks contributed to this product's quality outcomes this year" — closing the Q9(R1) feedback loop.

### 12.6 Vendor-release evaluation discipline

MasterControl is a SaaS that ships quarterly + ad-hoc emergency releases. Each release potentially changes configured-workflow semantics. The design choice is to treat every release as a CR trigger:

1. Within 14 days of release notes publication (DS-VND-02), runbook `TLB-RB-MC-RELEASE` is executed
2. Each release-note item is classified: configuration-affecting / non-affecting / unclear
3. Configuration-affecting items create a re-validation ticket per `VLP-CR-TEMPLATE`
4. UAT scripts (DS-PROC-04) cover the affected process flows
5. Promotion to PRODUCTION requires `Config-Author ≠ Config-Approver` signatures (DS-PROC-03)

This is the operational manifestation of the platform-level vendor-release-risk mitigation strategy and is the primary defence against DR-01.

### 12.7 Bulk-export anti-exfiltration design

Bulk-export events are tagged `BULK_EXPORT` in the audit trail (DS-SEC-03) and surfaced in the focused-review tool `TLB-AUD-FOCUSED` (DS-AT-05). The design choice is to make bulk-export visible but not blocked: legitimate use cases exist (regulator response, M&A due diligence, internal audit). The protection is observability — every bulk-export is reviewed in the next focused-review cycle.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
