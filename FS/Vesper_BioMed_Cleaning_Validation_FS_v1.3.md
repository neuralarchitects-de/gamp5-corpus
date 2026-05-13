---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "VSP-URS-CLNV-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd Ed., 2022) Cat 4 conventions"
  - "21 CFR Part 11; EU GMP Annex 11; EU GMP Annex 15"
  - "ICH Q9(R1); EMA HBEL Guideline 2014"
  - "FDA Cleaning Validation Guide 1993; PIC/S PI 006-3; APIC"
parent_urs:
  document_number: VSP-URS-CLNV-001
  version: 1.2
  file: ../../URS/_generated/final/Cleaning_Validation_System__Vesper_BioMed_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Cleaning Validation System — ValGenesis CV 5.0

**Document Number:** VSP-FS-CLNV-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** VSP-URS-CLNV-001 v1.2 | **Site:** Vesper BioMed (fictional)
**System Class:** GAMP Cat 4 — Configured Product
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; EU GMP Annex 15; ICH Q9(R1); EMA HBEL Guideline (2014); FDA Cleaning Validation Guide (1993); PIC/S PI 006-3; APIC

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Cleaning Validation SME) | _____________ | _____________ | _____ |
| Reviewer (Toxicologist — PDE/HBEL) | _____________ | _____________ | _____ |
| Approver (Head of Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | v1.2: aligned to parent URS VSP-URS-CLNV-001 v1.2 (prior FS used unaligned DEV/CALC/RUN URS-IDs and a Cat 5 designation); per-URS-ID expansion across § 4 and § 8 per METHODOLOGY § 2A.7; added recovery-study, hold-time, cleaning-agent, changeover-matrix, inspection-readiness-dashboard modules. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

Specify the cleaning-validation system to satisfy `VSP-URS-CLNV-001` v1.2 — ValGenesis CV 5.0 configured for MAC engine, recovery + hold-time studies, cleaning-agent qualification, product changeover matrix, sampling lifecycle, and inspection-readiness dashboard.

## 2. Scope

ValGenesis CV 5.0 server (Linux, PostgreSQL 16); integration with LabWare LIMS 8 (residue results), Werum PAS-X (changeover scheduling), MasterControl eQMS (deviations + CAPAs), Veeva Vault QualityDocs (controlled SOPs + reports), AD (authN).

## 3. System Architecture

```
   ┌────────────────────────────────────────────────────────┐
   │                   AD + MFA                              │
   └─────────────────────┬──────────────────────────────────┘
                         │
   ┌─────────────────────▼──────────────────────────────────┐
   │             ValGenesis CV 5.0                           │
   │  Equipment MD · Product MD · Worst-Case · MAC Engine    │
   │  Recovery · Hold-Time · Cleaning-Agent · Changeover     │
   │  Sample Plan · Verification · Report · Inspection Dash  │
   └────┬──────────┬────────────┬──────────────┬─────────────┘
        │          │            │              │
        ▼          ▼            ▼              ▼
   LabWare       Vault       PAS-X        MasterControl
   LIMS 8     QualityDocs    MES           eQMS
   (results)  (SOPs/reports) (schedule)   (deviations)
```

### 3.1 Component Inventory

| ID | Component | GAMP Cat | Notes |
|---|---|---|---|
| C-01 | ValGenesis CV 5.0 | 4 | core platform |
| C-02 | PostgreSQL 16 | 4 | data layer |
| C-03 | LabWare LIMS 8 | 4 | residue source (separate URS) |
| C-04 | Veeva Vault QualityDocs 24R1 | 4 | doc archive |
| C-05 | Werum PAS-X v3.2 | 4 | scheduler (separate URS) |
| C-06 | MasterControl eQMS | 4 | deviation routing |
| C-07 | AD / Kerberos | (infra) | AuthN |

## 4. Functional Specifications

### 4.1 Worst-Case Matrix and Equipment Grouping

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MX-01 | URS-MX-01 | Equipment master `cv_equipment` table: surface_area_cm², materials (SS-316L, EPDM, PTFE…), complexity_score, dedicated_flag, CIP_SIP_flag; populated from site CMMS feed. |
| FS-MX-02 | URS-MX-02 | Product master `cv_product` table references HBEL / ADE / PDE via foreign key to toxicology register `tox_hbel`; direct edit of HBEL fields denied to CV roles. |
| FS-MX-03 | URS-MX-03 | Worst-case selector job: deterministic Python function `select_worst_case(group_id)` — runs nightly + on-demand; outputs documented to `cv_worstcase_history`. |
| FS-MX-04 | URS-MX-04 | Equipment-group definition form: justification text-field mandatory (similar geometry, contact materials, cleaning method); group-level worst-case selected via FS-MX-03. |
| FS-MX-05 | URS-MX-05 | Re-evaluation trigger: CMMS equipment-change webhook + product-introduction workflow both invoke the selector job. |

### 4.2 MAC Calculation Engine

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MACO-01 | URS-MACO-01 | HBEL-based MAC = `(HBEL × min_batch_size_next) / (max_daily_dose_next × shared_surface)` per EMA Guideline 2014; primary criterion. |
| FS-MACO-02 | URS-MACO-02 | Trio criteria: HBEL-based, 10 ppm, 1/1000 TDD; engine computes all three + selects most stringent; rationale captured in `cv_macp_decision` table. |
| FS-MACO-03 | URS-MACO-03 | MAC inputs version-controlled in `cv_macp_inputs`; PUT on any input creates new version with `created_by, created_at, prior_version_id`. |
| FS-MACO-04 | URS-MACO-04 | OQ edge-case test suite: smallest-dose × largest-surface; HPAPI (HBEL < 10 µg/d); shared multi-product equipment; verified per `OQ-MACO-EDGECASE-01`. |
| FS-MACO-05 | URS-MACO-05 | Hazard-class flag (HPAPI / cytotoxic / sensitizer / hormone / β-lactam) forces `mac_engine.method = "HBEL"`; alert raised if 10 ppm / TDD would yield less stringent. |

### 4.3 Sample Plan

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SMP-01 | URS-SMP-01 | Sampling-plan form per CV protocol; sampler captures sample_loc_id + timestamp + user via mobile data-capture; chain-of-custody locked at submission. |
| FS-SMP-02 | URS-SMP-02 | Swab-location master per equipment: location_id, name, surface_area_cm², worst-case_flag, rationale; selected per worst-case-identification SOP. |
| FS-SMP-03 | URS-SMP-03 | Rinse module captures rinse_volume + computes rinse-acceptance = MAC × (rinse_volume / surface_area). |
| FS-SMP-04 | URS-SMP-04 | Visual inspection acceptance per FDA Cleaning Validation Guide 1993; recorded as baseline check before swab/rinse. |

### 4.4 Recovery Study Lifecycle

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REC-01 | URS-REC-01 | Recovery-study module captures (surface_material, spike_level, recovery_method, analytical_method, n_replicates ≥ 3, recovery_factor, rsd_pct ≤ 20). |
| FS-REC-02 | URS-REC-02 | Engine flags `recovery_factor < 0.50` as INVALID; downstream MAC engine cannot apply INVALID recovery factor. |
| FS-REC-03 | URS-REC-03 | Re-verification due-date computed = approval_date + 3 y; dashboard ageing alert. |
| FS-REC-04 | URS-REC-04 | Per-surface-material recovery factor enforced at MAC-engine join; SS-316L recovery cannot be applied to PTFE surface. |

### 4.5 Hold-Time Studies

| FS ID | URS ID | Specification |
|---|---|---|
| FS-HT-01 | URS-HT-01 | Dirty hold-time form: equipment_id, last_product, hold_hours, microbial_count, chemical_residue; acceptance per worst-case soiling study. |
| FS-HT-02 | URS-HT-02 | Clean hold-time form: equipment_id, post-clean hours, microbial_count, endotoxin (where applicable). |
| FS-HT-03 | URS-HT-03 | PAS-X production schedule pulls hold-time limits per equipment via FS-INT-MES-01; exceed creates eQMS deviation. |
| FS-HT-04 | URS-HT-04 | Re-verification due-date computed = approval_date + 5 y; dashboard ageing alert. |

### 4.6 Cleaning Agent Qualification

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AGT-01 | URS-AGT-01 | Cleaning-agent master `cv_agent` with: composition, supplier_CoA_ref, removability_study_id, residue_detection_method, residue_acceptance. |
| FS-AGT-02 | URS-AGT-02 | Cleaning-agent residue MAC computed via FS-MACO-01..02 logic using the agent's HBEL or default fallback. |
| FS-AGT-03 | URS-AGT-03 | Agent-lot tracking; CoA-discrepancy job raises eQMS deviation via FS-INT-EQMS-01. |

### 4.7 Product Changeover Matrix

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CHG-01 | URS-CHG-01 | Changeover matrix view: (prev_product, next_product, equipment_train, mac, cleaning_proc_id, agent_qual_status, sample_plan_id, last_verify_date). |
| FS-CHG-02 | URS-CHG-02 | MES integration: `GET /cv/api/v2/changeover-allowed?prev={p1}&next={p2}&equipment={e}`; HTTP 403 with reason on unsupported pair; PAS-X blocks schedule. |
| FS-CHG-03 | URS-CHG-03 | New-product workflow: CV Engineer authors changeover rows → CV Lead approves → matrix activated. |
| FS-CHG-04 | URS-CHG-04 | PDF export `cv_inspection_changeover_binder.pdf` includes full matrix + per-pair details. |

### 4.8 Verification, Reporting

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VER-01 | URS-VER-01 | Results-evaluation engine joins LIMS residue results with MAC + recovery factor; computes pass/fail. |
| FS-VER-02 | URS-VER-02 | OOS triggers eQMS deviation auto-create; report progression blocked until investigation status = CLOSED. |
| FS-VER-03 | URS-VER-03 | Trending engine: per equipment / product-pair / agent; OOT rules configurable per protocol; firing triggers investigation. |
| FS-RPT-01 | URS-RPT-01 | CV report PDF includes scope, equipment, MAC, recovery factors, hold-time, agent qual, sampling, results, deviations, conclusion; signed by CV Lead + QA Approver. |

### 4.9 Inspection-Readiness Dashboard

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DASH-01 | URS-DASH-01 | Dashboard tile-grid summarising: CV-protocol status, MAC currency, recovery-study currency, hold-time currency, agent-qual currency, changeover-matrix currency, recent OOS / OOT count, PR status. |
| FS-DASH-02 | URS-DASH-02 | PDF export `cv_inspection_binder.pdf` per equipment / product. |
| FS-DASH-03 | URS-DASH-03 | Ageing alerts: MAC > 3 y, recovery > 3 y, hold-time > 5 y rendered as orange/red badges. |

### 4.10 Audit Trail / 21 CFR Part 11 / DI

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit captures every state change across MAC inputs, recovery, hold-time, agent qual, changeover, sampling, verification, signatures. |
| FS-AUD-02 | URS-AUD-02 | Append-only at DB role-grant level. |
| FS-AUD-03 | URS-AUD-03 | Monthly review by CV Lead; evidence template `VSP-PR-AUD-001`. |
| FS-AUD-04 | URS-AUD-04 | Retention ≥ 25 y per Vault archive policy. |
| FS-PART11-10 | URS-PART11-10 | Validation procedure + copy-generation per § 11.10(a)–(e). |
| FS-PART11-50 | URS-PART11-50 | Signature manifestation per § 11.50. |
| FS-PART11-70 | URS-PART11-70 | Signature binding per § 11.70. |
| FS-PART11-100 | URS-PART11-100 | AD uniqueness per § 11.100. |
| FS-PART11-200 | URS-PART11-200 | Re-auth (password + MFA) at every signing per § 11.200. |
| FS-DI-01 | URS-DI-01 | Records Attributable via AD principal. |
| FS-DI-04 | URS-DI-04 | Originals preserved; corrections recorded with reason field. |
| FS-DI-05 | URS-DI-05 | MAC / verification calc Accurate per OQ. |

### 4.11 Integrations / Performance / Backup / Security / Training / PR

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | LIMS REST: `POST /lims/api/v2/samples` + `GET /lims/api/v2/results`; idempotency key = (cv_run_id, sample_loc_id). |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | MasterControl REST deviation-create on OOS / hold-time exceedance. |
| FS-INT-VAULT-01 | URS-INT-VAULT-01 | Vault URN refs on protocol + report records. |
| FS-INT-MES-01 | URS-INT-MES-01 | PAS-X changeover query (FS-CHG-02). |
| FS-INT-AD-01 | URS-INT-AD-01 | AD authN; service accounts in vault. |
| FS-INT-APR-01 | URS-INT-APR-01 | `GET /cv/api/v2/summary?product={p}` read-only consumed by APR/PQR. |
| FS-PERF-01 | URS-PERF-01 | MAC recompute on master-data change ≤ 30 s per PQ-PERF-MACO-01. |
| FS-BAK-01 | URS-BAK-01 | pg_basebackup + WAL nightly to object-locked S3; retention ≥ 25 y. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore-test runbook `VSP-RB-RESTORE-001`; QA witness. |
| FS-SEC-01 | URS-SEC-01 | AD + MFA; quarterly access review. |
| FS-TRN-01 | URS-TRN-01 | Cornerstone curriculum `VSP-CURR-CV-Engineer-v1`. |
| FS-PR-01 | URS-PR-01 | Annual periodic review per `VSP-PR-CV-YYYYMMDD`. |


### 4.12 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem. Conditional-access binding to policy `Quality-App Conditional Access (MFA on first logon per session)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.13 Cross-System Integration — eQMS handover (M-XINT-EQMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-EQMS-01 | URS-XINT-EQMS-01 | CAPA-event publisher posts to eQMS endpoint `POST /capa/tickets` with mTLS + Entra workload-identity; payload schema `eqms.ticket.v1`; OpenAPI artefact `xint-eqms.openapi.yaml`; outbound retry with exponential back-off and DLQ at 5 attempts. |
| FS-XINT-EQMS-02 | URS-XINT-EQMS-02 | eQMS ticket-status webhook subscribed; payload `eqms.status.v1`; consumer rule maps eQMS status `(OPEN, IN-PROGRESS, EFFECTIVENESS, CLOSED)` onto originating-record disposition fields; closed-loop verification gate prevents disposition without `eqms_status=CLOSED`. |

## 5. Configuration Items (CI)

| CI ID | Item | Value |
|---|---|---|
| CI-01 | HBEL inputs | per-API table, version-controlled, sourced from toxicology |
| CI-02 | MAC trio criteria | HBEL + 10 ppm + 1/1000 TDD; most stringent selected |
| CI-03 | Worst-case selection | deterministic; recomputed at portfolio change |
| CI-04 | Recovery factor minimum | ≥ 0.50 (else INVALID) |
| CI-05 | Recovery-study re-verification | every 3 y |
| CI-06 | Hold-time re-verification | every 5 y |
| CI-07 | Sampling locations | worst-case per equipment |
| CI-08 | Visual inspection | baseline (FDA Cleaning Validation Guide 1993) |
| CI-09 | Changeover matrix | required for every product-pair × equipment |
| CI-10 | Dashboard ageing thresholds | MAC > 3 y, recovery > 3 y, hold-time > 5 y |
| CI-11 | Audit retention | ≥ 25 y |
| CI-12 | Backup restore-test | quarterly |

## 6. Risks (FS-level)

| Risk | Mitigation |
|---|---|
| HBEL input drift | FS-MX-02 + toxicology gate |
| Recovery factor mis-applied to wrong surface | FS-REC-04 |
| MAC calc defect | FS-MACO-04 + OQ edge-case suite |
| OOS bypass | FS-VER-02 |
| Hold-time exceedance not deviation-raised | FS-HT-03 + MES integration |
| Unsupported changeover scheduled | FS-CHG-02 + MES block |
| Cleaning-agent residue overlooked | FS-AGT-01..02 |
| Audit-trail tampering | FS-AUD-02 |

## 7. References

- VSP-URS-CLNV-001 v1.2 (parent URS)
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200
- EU GMP Annex 11; EU GMP Annex 15; EU GMP Chapters 3, 5
- EMA *Guideline on Setting Health Based Exposure Limits* (2014)
- FDA *Guide to Inspections — Validation of Cleaning Processes* (1993)
- PIC/S PI 006-3; APIC Cleaning Validation Guideline
- ICH Q9(R1); USP <1072>, <1078>; PIC/S PI 041
- ISPE GAMP 5 (2nd Ed., 2022); ISPE RiskMaPP
- ValGenesis — *CV 5.0 Reference*

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID | Notes |
|---|---|---|
| URS-MX-01 | FS-MX-01 | |
| URS-MX-02 | FS-MX-02 | |
| URS-MX-03 | FS-MX-03 | |
| URS-MX-04 | FS-MX-04 | |
| URS-MX-05 | FS-MX-05 | |
| URS-MACO-01 | FS-MACO-01 | |
| URS-MACO-02 | FS-MACO-02 | |
| URS-MACO-03 | FS-MACO-03 | |
| URS-MACO-04 | FS-MACO-04 | |
| URS-MACO-05 | FS-MACO-05 | |
| URS-SMP-01 | FS-SMP-01 | |
| URS-SMP-02 | FS-SMP-02 | |
| URS-SMP-03 | FS-SMP-03 | |
| URS-SMP-04 | FS-SMP-04 | |
| URS-REC-01 | FS-REC-01 | |
| URS-REC-02 | FS-REC-02 | |
| URS-REC-03 | FS-REC-03 | |
| URS-REC-04 | FS-REC-04 | |
| URS-HT-01 | FS-HT-01 | |
| URS-HT-02 | FS-HT-02 | |
| URS-HT-03 | FS-HT-03 | |
| URS-HT-04 | FS-HT-04 | |
| URS-AGT-01 | FS-AGT-01 | |
| URS-AGT-02 | FS-AGT-02 | |
| URS-AGT-03 | FS-AGT-03 | |
| URS-CHG-01 | FS-CHG-01 | |
| URS-CHG-02 | FS-CHG-02 | |
| URS-CHG-03 | FS-CHG-03 | |
| URS-CHG-04 | FS-CHG-04 | |
| URS-VER-01 | FS-VER-01 | |
| URS-VER-02 | FS-VER-02 | |
| URS-VER-03 | FS-VER-03 | |
| URS-RPT-01 | FS-RPT-01 | |
| URS-DASH-01 | FS-DASH-01 | |
| URS-DASH-02 | FS-DASH-02 | |
| URS-DASH-03 | FS-DASH-03 | |
| URS-AUD-01 | FS-AUD-01 | |
| URS-AUD-02 | FS-AUD-02 | |
| URS-AUD-03 | FS-AUD-03 | |
| URS-AUD-04 | FS-AUD-04 | |
| URS-PART11-10 | FS-PART11-10 | |
| URS-PART11-50 | FS-PART11-50 | |
| URS-PART11-70 | FS-PART11-70 | |
| URS-PART11-100 | FS-PART11-100 | |
| URS-PART11-200 | FS-PART11-200 | |
| URS-DI-01 | FS-DI-01 | |
| URS-DI-04 | FS-DI-04 | |
| URS-DI-05 | FS-DI-05 | |
| URS-INT-LIMS-01 | FS-INT-LIMS-01 | |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 | |
| URS-INT-VAULT-01 | FS-INT-VAULT-01 | |
| URS-INT-MES-01 | FS-INT-MES-01 | |
| URS-INT-AD-01 | FS-INT-AD-01 | |
| URS-INT-APR-01 | FS-INT-APR-01 | |
| URS-PERF-01 | FS-PERF-01 | |
| URS-BAK-01 | FS-BAK-01 | |
| URS-BAK-02 | FS-BAK-02 | |
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
| R-01 | Incorrect HBEL input causing under-estimated MAC | Medium | Critical | URS-MX-02 + toxicology gate |
| R-02 | MAC misconfig (recovery factor mis-applied to wrong surface) | Medium | High | URS-REC-04 + URS-MACO-04 |
| R-03 | Calculation drift after vendor upgrade | Medium | High | URS-MACO-04 + OQ re-run |
| R-04 | OOS bypass | Medium | High | URS-VER-02 |
| R-05 | Hold-time exceeded without deviation | Medium | High | URS-HT-03 |
| R-06 | Unsupported changeover pair scheduled in MES | Low | Critical | URS-CHG-02 |
| R-07 | Cleaning-agent residue overlooked (focus only on API) | Medium | High | URS-AGT-01..02 |
| R-08 | Audit-trail tampering | Low | High | URS-AUD-02 |

Full evaluation in `VSP-RA-CLNV-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
