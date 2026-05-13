---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "HCT-URS-STAB-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd Ed., 2022) Cat 4 conventions"
  - "21 CFR Part 11 §§ .50, .70, .100, .200, .300"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "ICH Q1A(R2), Q1B, Q1C, Q1D, Q1E, Q5C"
  - "USP <659>, <1150>; WHO TRS 953 Annex 2; PIC/S PI 041"
parent_urs:
  document_number: HCT-URS-STAB-001
  version: 1.2
  file: ../../URS/_generated/final/Stability_Management_System__Halcyon_Therapeutics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Stability Management System — SLIMS / Genohm Stability Module 6.7

**Document Number:** HCT-FS-STAB-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** HCT-URS-STAB-001 v1.2 | **Site:** Halcyon Therapeutics (fictional)
**System Class:** GAMP Cat 4 — Configured Product
**Regulatory Scope:** ICH Q1A(R2), Q1B, Q1C, Q1D, Q1E, Q5C; 21 CFR Part 11; EU GMP Annex 11; USP <659>, <1150>; WHO TRS 953 Annex 2; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Stability Coordinator) | _____________ | _____________ | _____ |
| Reviewer (Statistician) | _____________ | _____________ | _____ |
| Approver (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | v1.2: aligned to parent URS HCT-URS-STAB-001 v1.2 (prior FS used unaligned URS-IDs and a different parent doc-number); per-URS-ID expansion across § 4 and § 8 per METHODOLOGY § 2A.7; added ICH zone + photostability + matrixing + Q5C biotech + reference-standard modules + shelf-life-extension module. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies how SLIMS Stability Module v6.7 is configured and integrated to satisfy `HCT-URS-STAB-001` v1.2.

## 2. Scope

SLIMS Stability Module v6.7 + StabilityNexus statistical analysis add-on (ICH Q1E); integration with chamber-monitoring system (Vaisala viewLinc 5.2) for environmental excursion linkage + MKT; results consumed from LabWare LIMS 8 (sourced from HPLC CDS Empower, bioassay LIMS workflows, etc.); reference + comparator standard inventory; photostability sub-module; bracketing / matrixing module; SSO via AD; reports archived to Vault.

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | GAMP Cat | Notes |
|---|---|---|---|
| C-01 | SLIMS Stability Module v6.7 | 4 | core platform |
| C-02 | StabilityNexus | 4 | shelf-life statistics (ICH Q1E) |
| C-03 | Vaisala viewLinc 5.2 (EMS) | 4 | chamber T/RH (separate URS) |
| C-04 | LabWare LIMS 8 | 4 | result source (separate URS) |
| C-05 | Veeva Vault QualityDocs 24R1 | 4 | protocol + report archival |
| C-06 | MasterControl eQMS | 4 | deviation routing |
| C-07 | AD / Kerberos | (infra) | AuthN |
| C-08 | PostgreSQL 16 + PITR | 4 | data layer |

### 3.2 Logical Architecture (textual)

```
   ┌────────────────────────────────────────────────────────┐
   │           AD / Kerberos + MFA                          │
   └─────────────────────┬──────────────────────────────────┘
                         │
   ┌─────────────────────▼──────────────────────────────────┐
   │  SLIMS Stability Module v6.7 + StabilityNexus          │
   │  Protocols · Zones · Time-points · Photostability      │
   │  Bracketing/Matrixing · Reference Standards · Q1E      │
   └────┬────────────┬────────────┬───────────┬─────────────┘
        │            │            │           │
        ▼            ▼            ▼           ▼
   Vaisala       LabWare        Vault     MasterControl
   viewLinc      LIMS 8       QualityDocs    eQMS
   (T/RH +      (results)    (protocols +  (deviations)
    excursions)              reports)
```

## 4. Functional Specifications

### 4.1 Platform / Hardware

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | SLIMS deployed as 3-replica OpenShift workload (`stab-prod-ns` project); PostgreSQL 16 in operator-managed cluster with PITR; replicas exposed via Route + AD service account; resource requests sized for nominal 200 concurrent users. |
| FS-PLAT-02 | URS-PLAT-02 | DR site: warm-standby PostgreSQL + restore-from-PITR runbook `HCT-RB-DR-001`; RPO ≤ 15 min validated by `PQ-DR-FAILOVER-01`; RTO ≤ 4 h validated by `PQ-DR-FAILOVER-01`. |
| FS-PLAT-03 | URS-PLAT-03 | All routes confined to GMP-laboratory VLAN; no direct office-network ingress per network-config audit. |

### 4.2 Stability Protocol Lifecycle

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PROT-01 | URS-PROT-01 | SLIMS protocol-workflow `HCT-WF-PROT-001`: DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED. |
| FS-PROT-02 | URS-PROT-02 | Protocol-form fields enforced: product, container-closure, ICH conditions, ICH zone, time-points, attributes, specifications, sampling plan, statistical-analysis plan. |
| FS-PROT-03 | URS-PROT-03 | Amendments require impact-assessment-form + Protocol Author + Protocol Approver signatures; routes through eQMS change control. |
| FS-PROT-04 | URS-PROT-04 | EFFECTIVE protocols immutable; revision auto-creates `v(n+1)` with diff record. |
| FS-PROT-05 | URS-PROT-05 | Matrixing-design field mandatory; structured input includes scheme (full / 1/2 / 1/3) + rationale. |

### 4.3 ICH Zone Configuration

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ZONE-01 | URS-ZONE-01 | Zones I–IVb pre-configured in `CFG-ZONE-MASTER`: long-term + accelerated + intermediate conditions per zone; per-zone-bound default protocols. |
| FS-ZONE-02 | URS-ZONE-02 | Market-to-zone mapping table `CFG-MARKET-ZONE-MAP`; protocol-creation wizard routes per market list. |
| FS-ZONE-03 | URS-ZONE-03 | Zone field is `read-only` after protocol promotes to EFFECTIVE; change requires amendment per FS-PROT-03. |

### 4.4 Time-Point + Chamber Assignment

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SCH-01 | URS-SCH-01 | Schedule generator computes pull dates from start + time-points; daily cron checks missed-pull window; missed pull raises eQMS deviation via FS-INT-EQMS-01. |
| FS-SCH-02 | URS-SCH-02 | LIMS REST: `POST /lims/api/v2/samples` per pull; idempotency key = (protocol_id, time_point, condition, sample_no). |
| FS-SCH-03 | URS-SCH-03 | Chain-of-custody form gated by digital signature; mandatory fields: chamber_id, withdrawn-by user, timestamp, sample weight. |
| FS-SCH-04 | URS-SCH-04 | Chamber-qualification check pulls qualified-chamber list from CMMS; assignment to non-qualified chamber raises `ChamberNotQualifiedError`. |
| FS-SCH-05 | URS-SCH-05 | Tolerance windows pre-populated per Q1A(R2) defaults; per-protocol override via `protocol_tolerance_override` config. |

### 4.5 Photostability (ICH Q1B)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PHOTO-01 | URS-PHOTO-01 | Lamp-config dropdown {Option 1 — cool white fluorescent + near-UV; Option 2 — Xe-arc}; lamp-exposure capture form per study run. |
| FS-PHOTO-02 | URS-PHOTO-02 | Exposure-min validator: visible ≥ 1.2 × 10⁶ lux·h AND near-UV ≥ 200 Wh/m²; study cannot close until both met. |
| FS-PHOTO-03 | URS-PHOTO-03 | Sample-group field {test, control-protected, control-dark}; cross-comparison view per Q1B Annex 2. |

### 4.6 Bracketing and Matrixing (ICH Q1D)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MATRIX-01 | URS-MATRIX-01 | Design type {full, bracketing, matrixing}; rationale text-field mandatory for reduced designs. |
| FS-MATRIX-02 | URS-MATRIX-02 | Reduction-percent calc; warning banner at < 50 % coverage; statistician review badge enforced. |
| FS-MATRIX-03 | URS-MATRIX-03 | Missed-matrixed-pull flag; design-integrity-loss workflow routes to statistician for review. |

### 4.7 Results / Trending / ICH Q1E

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RES-01 | URS-RES-01 | StabilityNexus pulls LIMS results via REST after QC approval at LIMS; binds to pull-id. |
| FS-RES-02 | URS-RES-02 | OOT engine evaluates per-protocol trending rules (e.g., 2σ band + Nelson Rule 2); fires investigation. |
| FS-RES-03 | URS-RES-03 | OOS results auto-flag protocol with `OOS_BLOCK` status; status cleared only by closed eQMS investigation. |
| FS-RES-04 | URS-RES-04 | StabilityNexus Q1E engine: candidate models (linear, log-linear, square-root); AIC-driven selection; one-sided 95 % CI; statistician co-approval required for shelf-life output. |
| FS-RES-05 | URS-RES-05 | Poolability test: ANCOVA slopes (α = 0.25) + intercepts (α = 0.25) per Q1E § 4.2; on fail, per-batch shelf-life output. |
| FS-RES-06 | URS-RES-06 | Trend visualisation views: per attribute / condition / batch / pooled; rendered via PI Vision-equivalent SLIMS chart engine. |

### 4.8 Shelf-Life Extension

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SLE-01 | URS-SLE-01 | Extension-validator enforces ≥ 3 commercial batches + ≥ 12 months long-term; extrapolation cap per Q1E § 3.2.2 (min(2× observed, observed + 12 months)). |
| FS-SLE-02 | URS-SLE-02 | Extension-approval workflow: statistician → Head of QC → Head of QA; embedded Q1E regression + CI + model-fit plot. |
| FS-SLE-03 | URS-SLE-03 | CI-boundary alert: nightly job recomputes upper / lower CI; alert fires if any active dataset crosses the boundary invalidating registered shelf-life. |

### 4.9 Reference + Comparator Standard Management

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RS-01 | URS-RS-01 | RS inventory table: lot, source (USP / EP / JP / in-house), potency, expiry, storage condition, qualification status, custody history. |
| FS-RS-02 | URS-RS-02 | Pre-test gate validates RS status `qualified=true AND expiry > today`; otherwise `ReferenceStandardExpiredError`. |
| FS-RS-03 | URS-RS-03 | Re-qualification workflow: comparison-to-primary protocol + statistician + RS Custodian + QA approval. |
| FS-RS-04 | URS-RS-04 | Q5C comparator-standard module: parallel inventory tagged `purpose=Q5C_comparator`. |

### 4.10 Biotech-Specific Stability (ICH Q5C)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BIO-01 | URS-BIO-01 | Orthogonal-methods configuration: protocol references ≥ 2 stability-indicating methods (CEX, SEC, iCIEF, bioassay etc.); shelf-life evaluator aggregates per Q5C § 2.5. |
| FS-BIO-02 | URS-BIO-02 | Freeze / thaw module: capture cycle count, condition, hold time, post-cycle test plan; results bound to protocol. |
| FS-BIO-03 | URS-BIO-03 | Method-revalidation tracker: alert when method validation expiry within 90 d. |

### 4.11 Audit Trail / 21 CFR Part 11 / Data Integrity

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit captures protocol changes, schedule changes, pull events, result retrievals, OOT / OOS, signatures, shelf-life proposals, RS transitions per EU GMP Annex 11 § 9. |
| FS-AUD-02 | URS-AUD-02 | Audit append-only at DB role-grant level; no admin update / delete. |
| FS-AUD-03 | URS-AUD-03 | Monthly review by Stability Operations Manager; quarterly QA Compliance review; evidence template `HCT-PR-AUD-001`. |
| FS-AUD-04 | URS-AUD-04 | Retention ≥ 25 y from product expiry via Vault QualityDocs archive policy. |
| FS-PART11-50 | URS-PART11-50 | E-signature manifestation: printed name + UTC timestamp + meaning rendered on every signed record. |
| FS-PART11-70 | URS-PART11-70 | SHA-256 binding of signature to record; verifiable via SLIMS audit-export. |
| FS-PART11-100 | URS-PART11-100 | AD uniqueness; deactivated accounts cannot be reassigned. |
| FS-PART11-200 | URS-PART11-200 | Re-auth (password + MFA) at every signing event. |
| FS-PART11-300 | URS-PART11-300 | AD password policy: 14 char min, 90 d rotation, complexity, loss-of-control workflow. |
| FS-DI-01 | URS-DI-01 | Audit-event captures user_id from AD principal. |
| FS-DI-02 | URS-DI-02 | Records rendered as fixed-format PDF/A-3 + structured XML export. |
| FS-DI-03 | URS-DI-03 | NTP-synced clock; skew alert at > 1 s. |
| FS-DI-04 | URS-DI-04 | Corrections never overwrite; new annotated record with reason field. |
| FS-DI-05 | URS-DI-05 | Q1E numeric accuracy verified per OQ reference dataset. |
| FS-DI-06 | URS-DI-06 | ALCOA+ readiness checklist per PIC/S PI 041 incorporated in OQ. |

### 4.12 Integrations

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | Sample-create + results-pull REST; idempotency on (protocol, time_point); retry budget 3. |
| FS-INT-EMS-01 | URS-INT-EMS-01 | Vaisala viewLinc 5.2 read; MKT recompute per ICH Q1A(R2) § 2.1.7.2; excursion-window check per chamber-id. |
| FS-INT-VAULT-01 | URS-INT-VAULT-01 | Vault URN reference field on protocol; resolves on save. |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | MasterControl deviation-create REST; idempotency on (event_type, ref_id). |
| FS-INT-APR-01 | URS-INT-APR-01 | `GET /api/stability/summary?product={p}` read-only endpoint consumed by `MIR-URS-APR-001`. |

### 4.13 Backup / Performance / Security / Training / Periodic Review

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BAK-01 | URS-BAK-01 | pg_basebackup + WAL archival nightly; retention ≥ 25 y on object-locked S3. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore-test runbook `HCT-RB-RESTORE-001`; QA witness signature captured. |
| FS-PERF-01 | URS-PERF-01 | Q1E compute on representative (3 batches × 5 time-points × 6 attributes) ≤ 30 s per PQ-PERF-CALC-01. |
| FS-SEC-01 | URS-SEC-01 | AD + MFA enforced; no local accounts except break-glass; quarterly access review. |
| FS-TRN-01 | URS-TRN-01 | Cornerstone curriculum `HCT-CURR-STAB-Coord-v1`; statistician Q1E competency assessment. |
| FS-PR-01 | URS-PR-01 | Annual periodic review per `HCT-PR-STAB-YYYYMMDD`. |


### 4.14 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem. Conditional-access binding to policy `Quality-App Conditional Access (MFA + device-compliance for OOT / OOS e-signature)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the stability study DB; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.15 Cross-System Integration — eQMS handover (M-XINT-EQMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-EQMS-01 | URS-XINT-EQMS-01 | CAPA-event publisher posts to eQMS endpoint `POST /capa/tickets` with mTLS + Entra workload-identity; payload schema `eqms.ticket.v1`; OpenAPI artefact `xint-eqms.openapi.yaml`; outbound retry with exponential back-off and DLQ at 5 attempts. |
| FS-XINT-EQMS-02 | URS-XINT-EQMS-02 | eQMS ticket-status webhook subscribed; payload `eqms.status.v1`; consumer rule maps eQMS status `(OPEN, IN-PROGRESS, EFFECTIVENESS, CLOSED)` onto originating-record disposition fields; closed-loop verification gate prevents disposition without `eqms_status=CLOSED`. |

## 5. Configuration Items (CI)

| CI ID | Item | Value |
|---|---|---|
| CI-01 | ICH Zone master | I / II / III / IVa / IVb |
| CI-02 | Time-point tolerance defaults | per Q1A(R2) |
| CI-03 | MKT calc | per Q1A(R2) § 2.1.7.2 |
| CI-04 | Q1E poolability α | 0.25 (slopes), 0.25 (intercepts) |
| CI-05 | Q1E candidate models | linear, log-linear, square-root |
| CI-06 | Q1E selection criterion | AIC |
| CI-07 | Q1E CI side | one-sided 95 % |
| CI-08 | Shelf-life extrapolation cap | min(2× observed, observed + 12 months) |
| CI-09 | Photostability Option 1 exposure | ≥ 1.2 × 10⁶ lux·h + ≥ 200 Wh/m² near-UV |
| CI-10 | Matrixing warning threshold | < 50 % coverage |
| CI-11 | EMS-linkage cadence | hourly |
| CI-12 | Retention | ≥ 25 y |
| CI-13 | Audit review cadence | monthly (Stability Ops) + quarterly (QA) |
| CI-14 | Backup restore-test cadence | quarterly |

## 6. Risks (FS-level)

| Risk | Mitigation |
|---|---|
| Missed pull-point | FS-SCH-01 + alerts |
| Excursion not linked | FS-INT-EMS-01 + cadence |
| Statistical defect (Q1E) | FS-RES-04 + FS-RES-05 + statistician co-approval |
| Zone misalignment | FS-ZONE-02 + FS-ZONE-03 |
| Matrixing integrity loss | FS-MATRIX-03 + statistician review |
| Shelf-life over-extrapolation | FS-SLE-01 + Q1E cap |
| Expired RS used | FS-RS-02 + pre-test gate |
| Audit-trail tampering | FS-AUD-02 + DB role grants |

## 7. References

- HCT-URS-STAB-001 v1.2 (parent URS)
- ICH Q1A(R2), Q1B, Q1C, Q1D, Q1E, Q5C
- 21 CFR Part 11 §§ .50, .70, .100, .200, .300
- EU GMP Annex 11 §§ 4, 6, 9, 11; Annex 15
- USP <659>, <1150>; WHO TRS 953 Annex 2
- PIC/S PI 041; ISPE GAMP 5 (2nd Ed., 2022)
- Genohm — *SLIMS Stability Module 6.7 Configuration Reference*; StabilityNexus reference manual

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID | Notes |
|---|---|---|
| URS-PLAT-01 | FS-PLAT-01 | |
| URS-PLAT-02 | FS-PLAT-02 | |
| URS-PLAT-03 | FS-PLAT-03 | |
| URS-PROT-01 | FS-PROT-01 | |
| URS-PROT-02 | FS-PROT-02 | |
| URS-PROT-03 | FS-PROT-03 | |
| URS-PROT-04 | FS-PROT-04 | |
| URS-PROT-05 | FS-PROT-05 | |
| URS-ZONE-01 | FS-ZONE-01 | |
| URS-ZONE-02 | FS-ZONE-02 | |
| URS-ZONE-03 | FS-ZONE-03 | |
| URS-SCH-01 | FS-SCH-01 | |
| URS-SCH-02 | FS-SCH-02 | |
| URS-SCH-03 | FS-SCH-03 | |
| URS-SCH-04 | FS-SCH-04 | |
| URS-SCH-05 | FS-SCH-05 | |
| URS-PHOTO-01 | FS-PHOTO-01 | |
| URS-PHOTO-02 | FS-PHOTO-02 | |
| URS-PHOTO-03 | FS-PHOTO-03 | |
| URS-MATRIX-01 | FS-MATRIX-01 | |
| URS-MATRIX-02 | FS-MATRIX-02 | |
| URS-MATRIX-03 | FS-MATRIX-03 | |
| URS-RES-01 | FS-RES-01 | |
| URS-RES-02 | FS-RES-02 | |
| URS-RES-03 | FS-RES-03 | |
| URS-RES-04 | FS-RES-04 | |
| URS-RES-05 | FS-RES-05 | |
| URS-RES-06 | FS-RES-06 | |
| URS-SLE-01 | FS-SLE-01 | |
| URS-SLE-02 | FS-SLE-02 | |
| URS-SLE-03 | FS-SLE-03 | |
| URS-RS-01 | FS-RS-01 | |
| URS-RS-02 | FS-RS-02 | |
| URS-RS-03 | FS-RS-03 | |
| URS-RS-04 | FS-RS-04 | |
| URS-BIO-01 | FS-BIO-01 | |
| URS-BIO-02 | FS-BIO-02 | |
| URS-BIO-03 | FS-BIO-03 | |
| URS-AUD-01 | FS-AUD-01 | |
| URS-AUD-02 | FS-AUD-02 | |
| URS-AUD-03 | FS-AUD-03 | |
| URS-AUD-04 | FS-AUD-04 | |
| URS-PART11-50 | FS-PART11-50 | |
| URS-PART11-70 | FS-PART11-70 | |
| URS-PART11-100 | FS-PART11-100 | |
| URS-PART11-200 | FS-PART11-200 | |
| URS-PART11-300 | FS-PART11-300 | |
| URS-DI-01 | FS-DI-01 | |
| URS-DI-02 | FS-DI-02 | |
| URS-DI-03 | FS-DI-03 | |
| URS-DI-04 | FS-DI-04 | |
| URS-DI-05 | FS-DI-05 | |
| URS-DI-06 | FS-DI-06 | |
| URS-INT-LIMS-01 | FS-INT-LIMS-01 | |
| URS-INT-EMS-01 | FS-INT-EMS-01 | |
| URS-INT-VAULT-01 | FS-INT-VAULT-01 | |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 | |
| URS-INT-APR-01 | FS-INT-APR-01 | |
| URS-BAK-01 | FS-BAK-01 | |
| URS-BAK-02 | FS-BAK-02 | |
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
| R-01 | Missed pull undetected | Medium | High | URS-SCH-01 |
| R-02 | OOS bypass | Medium | High | URS-RES-03 |
| R-03 | Incorrect Q1E model selection (linear vs log-linear) | Medium | High | URS-RES-04 + URS-RES-05 |
| R-04 | Chamber-condition deviation not linked to pull | Medium | High | URS-INT-EMS-01 |
| R-05 | ICH zone misalignment (e.g., Brazil registered as Zone II) | Low | Critical | URS-ZONE-02 |
| R-06 | Matrixing design integrity loss after missed pull | Medium | High | URS-MATRIX-03 |
| R-07 | Shelf-life extension over-extrapolated beyond Q1E § 3.2.2 cap | Low | Critical | URS-SLE-01 |
| R-08 | Expired reference standard used in stability assay | Low | Critical | URS-RS-02 |
| R-09 | Audit-trail tampering | Low | High | URS-AUD-02 |

Full evaluation in `HCT-RA-STAB-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
