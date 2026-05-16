---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "HCT-FS-STAB-001 v1.2 (parent FS)"
  - "HCT-URS-STAB-001 v1.2 (parent URS — informational)"
  - "GAMP 5 (2nd ed.) Cat 4 — Configuration Specification conventions"
  - "21 CFR Part 11; EU GMP Annex 11; ICH Q1A(R2)/Q1B/Q1C/Q1D/Q1E/Q5C"
  - "USP <659>, <1150>; WHO TRS 953 Annex 2; PIC/S PI 041"
  - "Genohm SLIMS Stability Module 6.7 Administrator Guide + StabilityNexus Reference Manual"
parent_fs:
  document_number: HCT-FS-STAB-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Halcyon_Therapeutics_Stability_Management_FS_v1.3.md
parent_urs:
  document_number: HCT-URS-STAB-001
  version: 1.2
  file: ../../../URS/_generated/final/Stability_Management_System__Halcyon_Therapeutics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Stability Management System — SLIMS / Genohm Stability Module 6.7 + StabilityNexus + Vaisala viewLinc + LabWare LIMS + Vault + MasterControl

**Document Number:** HCT-DS-STAB-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** HCT-FS-STAB-001 v1.2 | **Parent URS:** HCT-URS-STAB-001 v1.2 *(informational)*
**Site:** Halcyon Therapeutics (fictional)
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial product **Genohm SLIMS Stability Module 6.7 + StabilityNexus add-on** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** ICH Q1A(R2), Q1B, Q1C, Q1D, Q1E, Q5C; 21 CFR Part 11; EU GMP Annex 11; USP <659>, <1150>; WHO TRS 953 Annex 2; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Stability Coordinator) | _____________ | _____________ | _____ |
| Reviewer (Statistician) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Approver (System Owner — Head of QC) | _____________ | _____________ | _____ |
| Approver (Process Owner — Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T3 from parent URS+FS pair (HCT-URS-STAB-001 / HCT-FS-STAB-001 v1.2). DS covers 95/95 FS-IDs. ICH Q1E StabilityNexus statistical-analysis sub-component design captured in § 8.1. No FS-IDs deferred. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

DS-specific terms only.

| Term | Definition |
|---|---|
| SLIMS protocol | A stability protocol artefact inside SLIMS Stability Module (product, container-closure, conditions, time-points, attributes, specs, sampling plan, stats plan). |
| Time-point | A scheduled pull point in a stability protocol (e.g., 0, 3, 6, 12, 18, 24, 36 months). |
| Pull | The physical sample withdrawal event at a time-point. |
| MKT | Mean Kinetic Temperature per ICH Q1A(R2) § 2.1.7.2. |
| StabilityNexus | Shelf-life statistics add-on implementing ICH Q1E poolability test + linear/log-linear/sqrt model selection. |
| Q5C comparator | Biotech reference standard tagged `purpose=Q5C_comparator` in the RS register. |

## 1. Purpose

This DS specifies the technical SLIMS Stability Module 6.7 + StabilityNexus configuration values, protocol-lifecycle workflow design, time-point + chamber + reference-standard binding design, ICH Q1E statistical-analysis configuration, biotech-stability extensions, and integration design that implement the functional behaviour defined in `HCT-FS-STAB-001` v1.2.

## 2. Scope

In scope: SLIMS Stability Module configuration; StabilityNexus configuration; PostgreSQL 16 design; OpenShift deployment; Vaisala viewLinc 5.2 read integration; LabWare LIMS 8 result-source integration; Veeva Vault protocol+report archive; MasterControl eQMS deviation routing; AD + SIEM + backup integration. Out of scope: Genohm source-code internals; Vaisala viewLinc internals (separate URS); LabWare LIMS internals; Vault internals; MasterControl internals; chamber-qualification protocols.

## 3. Architectural Overview

### 3.1 Logical View

```
                  ┌────────────────────────────────────┐
                  │  AD (halcyon.local) + MFA · NTP   │
                  └──────────────┬─────────────────────┘
                                 │
                                 ▼
┌─────────────────────────────────────────────────────────────────────┐
│  SLIMS Stability Module v6.7 + StabilityNexus                       │
│  OpenShift `stab-prod-ns` · 3-replica workload                       │
│  PostgreSQL 16 (operator-managed, PITR)                              │
│  Domain logic: Protocol · Zone · Time-points · Photostability ·      │
│  Bracketing/Matrixing · Reference Standards · Q1E · Shelf-life ext.  │
└────┬────────────┬────────────┬────────────┬────────────┬────────────┘
     │            │            │            │            │
     ▼            ▼            ▼            ▼            ▼
┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌─────────────────┐
│ Vaisala  │ │ LabWare  │ │ Vault    │ │ Master-  │ │ APR/PQR consumer│
│ viewLinc │ │ LIMS 8   │ │ Quality- │ │ Control  │ │ (MIR-URS-APR)   │
│ 5.2 EMS  │ │ results  │ │ Docs 24R1│ │ eQMS     │ │ read-only GET   │
│ MKT      │ │ source   │ │ archive  │ │ deviations│ │                 │
└──────────┘ └──────────┘ └──────────┘ └──────────┘ └─────────────────┘
```

### 3.2 Deployment Topology

| Component | Host / Path | Version pin | Hardening |
|---|---|---|---|
| SLIMS Stability Module | OpenShift `stab-prod-ns` project; 3 replicas | 6.7.18 | OCP 4.14 + site security context constraints `SCC-GMP` |
| StabilityNexus add-on | Co-located in SLIMS pod | 2.4.5 | Same SCC |
| PostgreSQL primary | StatefulSet `pg-stab-primary` | 16.3 | CrunchyData Postgres Operator; PITR; encrypted at rest |
| PostgreSQL warm-standby (DR) | DR site | 16.3 | streaming replication + WAL archival |
| Route | `https://stab.halcyon.local` | TLS 1.3 | site PKI cert |
| Vaisala viewLinc 5.2 | `crn-emsbnk-01` (cross-system) | 5.2.4 | per Vaisala URS |
| LabWare LIMS 8 | `hct-lims-01` (cross-system) | 8.4 | per LIMS URS |
| Vault QualityDocs | Veeva SaaS | 24R1 | SaaS MFA + SSO |
| MasterControl | `hct-mc-01` (cross-system) | per SaaS | REST + mTLS |

## 4. Configuration Specification

`D = vendor default`; `C = site custom`.

### 4.1 Platform / Hardware Configuration

| CI-ID | Configuration Item (vendor-named) | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-PLAT-01 | SLIMS deployment topology | 3-replica OpenShift workload in project `stab-prod-ns`; resource requests sized for 200 concurrent users (CPU 2 / RAM 8 Gi per replica) | C | FS-PLAT-01 | IQ-PLAT-01 |
| DS-PLAT-02 | DR design + RPO/RTO | Warm-standby PostgreSQL + restore-from-PITR runbook `HCT-RB-DR-001`; RPO ≤ 15 min validated by `PQ-DR-FAILOVER-01`; RTO ≤ 4 h validated | C | FS-PLAT-02 | PQ-DR-01 |
| DS-PLAT-03 | Network confinement | All routes confined to GMP-laboratory VLAN; no direct office-network ingress | C | FS-PLAT-03 | IQ-NET-01 |
| DS-PLAT-04 | OpenShift SCC | `SCC-GMP` denies privileged + host-network + host-PID; restricts to UID/GID range `1000060000-1000069999` | C | hardening baseline | IQ-SCC-01 |
| DS-PLAT-05 | NTP | OpenShift nodes pointed to `ntp.halcyon.local`; chrony skew alert at > 1 s per node | C | FS-DI-03 | OQ-NTP-01 |

### 4.2 Stability-Protocol Lifecycle Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-PROT-01 | Protocol-lifecycle states | `DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED` (workflow `HCT-WF-PROT-001`) | C | FS-PROT-01 | OQ-PROT-01 |
| DS-PROT-02 | Protocol-form mandatory fields | `product, container_closure, ich_conditions, ich_zone, time_points, attributes, specifications, sampling_plan, stats_plan` | C | FS-PROT-02 | OQ-PROT-02 |
| DS-PROT-03 | Amendment workflow | requires `impact_assessment_form` + Protocol Author + Protocol Approver signatures; routes through eQMS change control | C | FS-PROT-03 | OQ-PROT-03 |
| DS-PROT-04 | EFFECTIVE immutability | EFFECTIVE protocols immutable; revision auto-creates `v(n+1)` with diff record | C | FS-PROT-04 | OQ-PROT-04 |
| DS-PROT-05 | Matrixing-design field requirement | mandatory `{scheme(full/1-2/1-3), rationale}` structured input | C | FS-PROT-05 | OQ-PROT-05 |

### 4.3 ICH Zone Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-ZONE-01 | Zone master table | `CFG-ZONE-MASTER`: Zones I, II, III, IVa, IVb pre-configured with long-term / accelerated / intermediate conditions per ICH Q1A(R2) | D | FS-ZONE-01 | OQ-ZONE-01 |
| DS-ZONE-02 | Market-to-zone mapping | `CFG-MARKET-ZONE-MAP`: protocol-creation wizard routes per market list | C | FS-ZONE-02 | OQ-ZONE-02 |
| DS-ZONE-03 | Zone field immutability post-EFFECTIVE | Zone field read-only after EFFECTIVE; change requires amendment per DS-PROT-03 | C | FS-ZONE-03 | OQ-ZONE-03 |

### 4.4 Time-Point + Chamber Assignment Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-SCH-01 | Schedule generator | Computes pull dates from `protocol_start + time_points`; daily cron checks missed-pull window; missed pull → eQMS deviation via DS-INT-EQMS-01 | C | FS-SCH-01 | OQ-SCH-01 |
| DS-SCH-02 | LIMS sample-create endpoint | `POST /lims/api/v2/samples`; idempotency key = `(protocol_id, time_point, condition, sample_no)` | C | FS-SCH-02 | OQ-SCH-02 |
| DS-SCH-03 | Chain-of-custody form | digital-signature-gated; mandatory `chamber_id, withdrawn_by_user, timestamp, sample_weight` | C | FS-SCH-03 | OQ-SCH-03 |
| DS-SCH-04 | Chamber-qualification check | pulls qualified-chamber list from CMMS REST; assignment to non-qualified → `ChamberNotQualifiedError` | C | FS-SCH-04 | OQ-SCH-04 |
| DS-SCH-05 | Tolerance windows | Q1A(R2) defaults pre-populated; per-protocol override via `protocol_tolerance_override` field | C | FS-SCH-05 | OQ-SCH-05 |

### 4.5 Photostability (ICH Q1B) Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-PHOTO-01 | Lamp configuration dropdown | `{Option 1 — cool white fluorescent + near-UV, Option 2 — Xe-arc}`; lamp-exposure capture form per study run | D | FS-PHOTO-01 | OQ-PHOTO-01 |
| DS-PHOTO-02 | Exposure-min validator | visible ≥ 1.2 × 10⁶ lux·h AND near-UV ≥ 200 Wh/m²; study cannot close until both met | C | FS-PHOTO-02 | OQ-PHOTO-02 |
| DS-PHOTO-03 | Sample-group taxonomy | `{test, control_protected, control_dark}`; cross-comparison view per Q1B Annex 2 | D | FS-PHOTO-03 | OQ-PHOTO-03 |

### 4.6 Bracketing + Matrixing (ICH Q1D) Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-MATRIX-01 | Design type field + rationale | `{full, bracketing, matrixing}`; rationale text mandatory for reduced designs | C | FS-MATRIX-01 | OQ-MATRIX-01 |
| DS-MATRIX-02 | Reduction-percent warning | warning banner at < 50% coverage; statistician review badge enforced | C | FS-MATRIX-02 | OQ-MATRIX-02 |
| DS-MATRIX-03 | Design-integrity-loss workflow | missed-matrixed-pull flag → workflow routes to statistician for review | C | FS-MATRIX-03 | OQ-MATRIX-03 |

### 4.7 Results / Trending / ICH Q1E Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-RES-01 | LIMS result pull binding | StabilityNexus pulls LIMS results via REST after QC approval at LIMS; binds to `pull_id` | C | FS-RES-01 | OQ-RES-01 |
| DS-RES-02 | OOT engine ruleset | per-protocol trending rules (e.g., 2σ band + Nelson Rule 2); fires investigation event | C | FS-RES-02 | OQ-RES-02 |
| DS-RES-03 | OOS protocol-block flag | auto-flag protocol `OOS_BLOCK`; cleared only by closed eQMS investigation | C | FS-RES-03 | OQ-RES-03 |
| DS-RES-04 | StabilityNexus Q1E engine | candidate models `{linear, log-linear, square-root}`; AIC-driven selection; one-sided 95% CI; statistician co-approval required for shelf-life output | C | FS-RES-04 | OQ-RES-04 |
| DS-RES-05 | Poolability test | ANCOVA slopes (α=0.25) + intercepts (α=0.25) per Q1E § 4.2; on fail → per-batch shelf-life | C | FS-RES-05 | OQ-RES-05 |
| DS-RES-06 | Trend visualisation | per attribute / condition / batch / pooled views; rendered via SLIMS chart engine | C | FS-RES-06 | OQ-RES-06 |

### 4.8 Shelf-Life Extension Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-SLE-01 | Extension validator | ≥ 3 commercial batches + ≥ 12 months long-term; extrapolation cap = `min(2× observed, observed + 12 months)` per Q1E § 3.2.2 | C | FS-SLE-01 | OQ-SLE-01 |
| DS-SLE-02 | Extension-approval workflow | statistician → Head of QC → Head of QA; embedded Q1E regression + CI + model-fit plot | C | FS-SLE-02 | OQ-SLE-02 |
| DS-SLE-03 | CI-boundary alert | nightly job recomputes upper/lower CI; alert if any active dataset crosses the boundary invalidating registered shelf-life | C | FS-SLE-03 | OQ-SLE-03 |

### 4.9 Reference + Comparator Standard Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-RS-01 | RS inventory schema | `lot, source(USP/EP/JP/in-house), potency, expiry, storage_condition, qualification_status, custody_history` | C | FS-RS-01 | OQ-RS-01 |
| DS-RS-02 | Pre-test gate | validates `qualified=true AND expiry > today`; otherwise `ReferenceStandardExpiredError` | C | FS-RS-02 | OQ-RS-02 |
| DS-RS-03 | Re-qualification workflow | comparison-to-primary protocol + statistician + RS Custodian + QA approval | C | FS-RS-03 | OQ-RS-03 |
| DS-RS-04 | Q5C comparator-standard tagging | parallel inventory tagged `purpose=Q5C_comparator` | C | FS-RS-04 | OQ-RS-04 |

### 4.10 Biotech-Specific Stability (ICH Q5C) Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-BIO-01 | Orthogonal-method requirement | protocol references ≥ 2 stability-indicating methods (CEX, SEC, iCIEF, bioassay etc.); shelf-life evaluator aggregates per Q5C § 2.5 | C | FS-BIO-01 | OQ-BIO-01 |
| DS-BIO-02 | Freeze/thaw module | captures `cycle_count, condition, hold_time, post_cycle_test_plan`; bound to protocol | C | FS-BIO-02 | OQ-BIO-02 |
| DS-BIO-03 | Method-revalidation alert | alert when method validation expiry within 90 d | C | FS-BIO-03 | OQ-BIO-03 |

### 4.11 Audit + Part 11 + DI Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-AUD-01 | Audit event-coverage | protocol changes, schedule changes, pull events, result retrievals, OOT/OOS, signatures, shelf-life proposals, RS transitions = ALL | C | FS-AUD-01 | OQ-AUD-01 |
| DS-AUD-02 | DB append-only at role-grant level | PostgreSQL role `audit_writer` granted INSERT only; no UPDATE / DELETE grants exist | C | FS-AUD-02 | OQ-AUD-02 |
| DS-AUD-03 | Audit-review cadence + templates | monthly Stability Ops Manager review + quarterly QA Compliance review; template `HCT-PR-AUD-001` | C | FS-AUD-03 | OQ-AUD-03 |
| DS-AUD-04 | Retention via Vault archive | ≥ 25 y from product expiry via Vault QualityDocs archive policy | C | FS-AUD-04 | OQ-AUD-04 |
| DS-PART11-50 | § 11.50 manifestation | printed name + UTC timestamp + meaning rendered on every signed record | C | FS-PART11-50 | OQ-P11-01 |
| DS-PART11-70 | § 11.70 signature↔record binding | SHA-256 binding; verifiable via SLIMS audit-export | C | FS-PART11-70 | OQ-P11-02 |
| DS-PART11-100 | § 11.100 uniqueness | AD UPN; deactivated accounts cannot be reassigned | C | FS-PART11-100 | OQ-P11-03 |
| DS-PART11-200 | § 11.200 re-auth | password + MFA re-entry at every signing event | C | FS-PART11-200 | OQ-P11-04 |
| DS-PART11-300 | § 11.300 password policy | AD GPO: 14 char min, 90 d rotation, complexity, loss-of-control workflow | C | FS-PART11-300 | OQ-P11-05 |
| DS-DI-01 | ALCOA+ Attributable | audit-event captures `user_id` from AD principal | C | FS-DI-01 | OQ-DI-01 |
| DS-DI-02 | ALCOA+ Legible | records rendered as PDF/A-3 + structured XML export | C | FS-DI-02 | OQ-DI-02 |
| DS-DI-03 | ALCOA+ Contemporaneous | NTP-synced clock; skew alert > 1 s | C | FS-DI-03 | OQ-DI-03 |
| DS-DI-04 | ALCOA+ Original | corrections never overwrite; new annotated record with reason field | C | FS-DI-04 | OQ-DI-04 |
| DS-DI-05 | ALCOA+ Accurate | Q1E numeric accuracy verified per OQ reference dataset | C | FS-DI-05 | OQ-DI-05 |
| DS-DI-06 | ALCOA+ Complete | ALCOA+ readiness checklist per PIC/S PI 041 in OQ | C | FS-DI-06 | OQ-DI-06 |

### 4.12 Integration Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-INT-LIMS-01 | LabWare LIMS sample-create + result-pull REST | endpoint `https://lims.halcyon.local/api/v2/{samples,results}`; idempotency on `(protocol, time_point)`; retry budget 3 | C | FS-INT-LIMS-01 | OQ-INT-01 |
| DS-INT-EMS-01 | Vaisala viewLinc read + MKT recompute | reads chamber data via viewLinc REST; MKT recomputed per ICH Q1A(R2) § 2.1.7.2; excursion-window check per `chamber_id` | C | FS-INT-EMS-01 | OQ-INT-02 |
| DS-INT-VAULT-01 | Vault URN protocol-reference | Vault URN reference field on protocol resolves on save | C | FS-INT-VAULT-01 | OQ-INT-03 |
| DS-INT-EQMS-01 | MasterControl deviation-create REST | endpoint `POST /api/v3/deviations`; idempotency on `(event_type, ref_id)`; mTLS via site PKI cert `HCT-PKI-STAB-EQMS` | C | FS-INT-EQMS-01, FS-XINT-EQMS-01 | OQ-INT-04 |
| DS-INT-EQMS-02 | eQMS status webhook | subscribe `eqms.status.v1`; closed-loop gate prevents disposition without `eqms_status=CLOSED` | C | FS-XINT-EQMS-02 | OQ-INT-05 |
| DS-INT-APR-01 | APR/PQR read endpoint | `GET /api/stability/summary?product={p}` read-only; consumed by `MIR-URS-APR-001` | C | FS-INT-APR-01 | OQ-INT-06 |

### 4.13 Backup + Performance + Security + Training + PR Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-BAK-01 | Backup engine | `pg_basebackup` + WAL archival nightly; retention ≥ 25 y on S3 Object Lock Compliance | C | FS-BAK-01 | OQ-BAK-01 |
| DS-BAK-02 | Restore-test runbook | quarterly `HCT-RB-RESTORE-001`; QA witness signature captured | C | FS-BAK-02 | OQ-BAK-02 |
| DS-PERF-01 | Q1E compute latency target | ≤ 30 s on representative (3 batches × 5 tp × 6 attributes) per PQ-PERF-CALC-01 | C | FS-PERF-01 | PQ-PERF-01 |
| DS-SEC-01 | AD + MFA + access review | AD + MFA enforced; no local accounts except break-glass; quarterly access review | C | FS-SEC-01 | OQ-SEC-01 |
| DS-TRN-01 | Cornerstone curriculum | `HCT-CURR-STAB-Coord-v1`; statistician Q1E competency assessment | C | FS-TRN-01 | OQ-TRN-01 |
| DS-PR-01 | Annual periodic-review template | `HCT-PR-STAB-YYYYMMDD` | C | FS-PR-01 | OQ-PR-01 |

### 4.14 Cross-System Integration Configuration

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-XSYS-AD-01 | AD conditional-access | LDAPS on-prem; policy `Quality-App Conditional Access (MFA + device-compliance for OOT / OOS e-signature)`; SIEM forwarding to Splunk `gxp-authn` ≤ 5 min; CyberArk PAM with 24 h rotation + dual-witness | C | FS-XSYS-AD-01 | OQ-XSYS-01 |
| DS-XSYS-BAK-01 | Backup integration | Veeam Application-Aware + `pg_basebackup` + WAL for stability DB; Tier T2 (RPO ≤ 24 h; RTO ≤ 24 BH); S3 Object Lock Compliance + LTO-9 monthly; quarterly QA-witnessed restore drill | C | FS-XSYS-BAK-01 | OQ-XSYS-02 |

## 5. Workflow + Business-Rule Design

### 5.1 Protocol Lifecycle Workflow (`HCT-WF-PROT-001`)

States: `DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED`. Transitions:

| From | To | Role required | Side-effects |
|---|---|---|---|
| DRAFT | REVIEW | Protocol Author | locks form; impact-assessment-form attached |
| REVIEW | APPROVED | Statistician + Stability Coordinator + Reviewer dual sign | rev number frozen |
| APPROVED | EFFECTIVE | Protocol Approver | matrixing-design + zone fields locked; schedule generator activates |
| EFFECTIVE | SUPERSEDED | Protocol Approver + QA Approver | revision auto-creates `v(n+1)`; old version retained with diff |

### 5.2 Pull-Point Schedule Workflow

Daily cron at 03:00 local enumerates expected pulls based on `protocol_start + time_points` with Q1A(R2) tolerance windows. For each missed pull (now > tolerance_upper) → DS-INT-EQMS-01 emits deviation with `event_type=MISSED_PULL`. Stability Coordinator triages within 24 h.

### 5.3 OOS Block + Clearance Workflow

`OOS_BLOCK` flag set immediately on OOS detection (DS-RES-03). Clearance requires:

1. eQMS deviation OPEN → INVESTIGATION → ROOT_CAUSE → CAPA → CLOSED.
2. Closed-loop gate (DS-INT-EQMS-02) verifies `eqms_status=CLOSED`.
3. Stability Coordinator + Head of QA dual sign the clearance.
4. Flag cleared; protocol resumes normal status.

### 5.4 Shelf-Life Extension Workflow (`HCT-WF-SLE`)

| Step | Actor | Gate |
|---|---|---|
| Extension request | Stability Coordinator | ≥ 3 commercial batches + ≥ 12 months long-term verified (DS-SLE-01) |
| Q1E run | StabilityNexus | candidate models fit; AIC selection; one-sided 95% CI |
| Statistician review | Statistician | model-fit plot + poolability test result reviewed |
| QC approval | Head of QC | extrapolation cap (DS-SLE-01) verified |
| QA approval | Head of QA | final sign |
| Submission package | Regulatory Affairs (downstream) | Vault filing |

### 5.5 RS Re-qualification Workflow (`HCT-WF-RS-REQUAL`)

Comparison-to-primary protocol → statistician → RS Custodian → QA approval. Each step e-signed in SLIMS RS module.

### 5.6 Matrixing-Integrity-Loss Workflow

DS-MATRIX-03 emits event on missed-matrixed-pull. Routes to statistician for `design_integrity_assessment`. If statistician verdict = `INTEGRITY_LOST`, protocol auto-flags + amendment workflow (DS-PROT-03) triggered.

### 5.7 Photostability Study-Close Workflow

DS-PHOTO-02 prevents study close until both lamp-exposure minimums met. Stability Coordinator e-signs study-close form referencing accumulated lux·h + Wh/m² values from lamp-exposure capture form.

### 5.8 Q5C Method-Revalidation Workflow

DS-BIO-03 90-d advance alert → Method Owner + Analytical Method Reviewer co-sign revalidation plan. If revalidation expires while protocol active → protocol auto-flags + statistician informed.

## 6. Role-Permission Matrix Design

| AD Group → / Permission ↓ | STAB-COORD | STAT | METHOD-OWNER | RS-CUSTODIAN | QC-HEAD | QA-HEAD | RA-OWNER | SYS-ADMIN |
|---|---|---|---|---|---|---|---|---|
| Create protocol DRAFT | ✓ | — | — | — | — | — | — | — |
| Approve protocol → EFFECTIVE | — | ✓ (rev) | — | — | — | — | — | — |
| Approve protocol final | — | — | — | — | — | ✓ | — | — |
| Trigger missed-pull deviation | ✓ (auto) | — | — | — | — | — | — | — |
| Approve matrixing rationale | — | ✓ | — | — | — | — | — | — |
| Trigger Q1E run | — | ✓ | — | — | — | — | — | — |
| Approve shelf-life extension | — | ✓ (rev) | — | — | ✓ | ✓ | — | — |
| Approve RS re-qualification | — | ✓ | — | ✓ | — | ✓ | — | — |
| Tag RS as Q5C comparator | — | — | — | ✓ | — | — | — | — |
| Approve Q5C method revalidation | — | — | ✓ | — | — | — | — | — |
| Sign photostability study-close | ✓ | — | — | — | — | — | — | — |
| Override OOS_BLOCK | — | — | — | — | — | ✓ | — | — |
| Read APR/PQR endpoint | — | — | — | — | ✓ | ✓ | ✓ | — |
| Modify CS / configuration | — | — | — | — | — | — | — | ✓ (CCR) |
| Read all audit | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

Author-Approver separation: a user shall NOT simultaneously hold `HCT-STAB-COORD` AND `HCT-STAB-STAT` AD-group membership. Verified quarterly.

## 7. Integration Design

### 7.1 LabWare LIMS 8 (DS-INT-LIMS-01)

| Aspect | Value |
|---|---|
| Endpoints | `POST /lims/api/v2/samples` (sample-create); `GET /lims/api/v2/results?protocol={p}&pull={pid}` (result-pull) |
| Transport | HTTPS + mTLS (cert `HCT-PKI-STAB-LIMS`) |
| Idempotency | `(protocol, time_point, condition, sample_no)` for sample-create |
| Retry | 3× exponential back-off; DLQ at 4 |
| Error-handling | LIMS-side reject codes `LIMS-SAMPLE-DUPLICATE`, `LIMS-PROTOCOL-NOT-FOUND` consumed |

### 7.2 Vaisala viewLinc 5.2 EMS (DS-INT-EMS-01)

| Aspect | Value |
|---|---|
| Endpoint | viewLinc REST `https://emsbnk.halcyon.local/api/v5/chambers/{id}/history?from=...&to=...` |
| Auth | AD service account `svc-stab-ems` (rotated 180 d) |
| Polling cadence | hourly (CI-11) |
| MKT recompute | per ICH Q1A(R2) § 2.1.7.2 — Arrhenius equation E_a = 83.144 kJ/mol; recomputed per chamber per protocol-condition window |
| Excursion linkage | excursion event tied to pull-id within protocol-condition window |

### 7.3 Veeva Vault QualityDocs (DS-INT-VAULT-01)

| Aspect | Value |
|---|---|
| Endpoint | Vault SaaS REST `https://halcyon.veevavault.com/api/v24.1/objects/stability_protocol` |
| Auth | OAuth2 + SCIM-provisioned principals |
| Vault URN resolution | protocol-field saves URN; resolves on form open + at every signing event |
| Archive policy | retention ≥ 25 y from product expiry |

### 7.4 MasterControl eQMS (DS-INT-EQMS-01 + 02)

| Aspect | Value |
|---|---|
| Push endpoint | `POST /api/v3/deviations` |
| Idempotency key | `(event_type, ref_id)` |
| mTLS | site PKI cert `HCT-PKI-STAB-EQMS` |
| Status webhook | `eqms.status.v1` consumed; closed-loop gate on originating record |
| Retry | 3× expo back-off; DLQ at 5 |

### 7.5 APR/PQR Read Endpoint (DS-INT-APR-01)

| Aspect | Value |
|---|---|
| Endpoint | `GET /api/stability/summary?product={p}` |
| Auth | AD-bound service account `svc-mir-apr` |
| Rate limit | 60 req/min per consumer |
| Response | structured JSON: per-attribute trend summary, current shelf-life, last OOT date, last OOS date |

### 7.6 AD + SIEM + Backup

Inherits the cross-system patterns; specifics in § 4.14.

### 7.7 Splunk SIEM Integration Specifics

| Aspect | Value |
|---|---|
| Forwarder | sidecar in `stab-prod-ns` pod; ships SLIMS audit + StabilityNexus run logs |
| Indices | `gxp-authn` (interactive logon); `gxp-stab-audit` (SLIMS audit); `gxp-stab-stat` (StabilityNexus runs); `gxp-stab-ems` (EMS read events) |
| Ingestion target | ≤ 5 min |
| Alert rules | (a) missed-pull deviation emit failure; (b) EMS read 5xx rate > 5%; (c) MKT recompute exception; (d) Vault URN resolution failure; (e) StabilityNexus Q1E exception |

### 7.8 Network + Firewall Topology

| Source → Destination | Port / Protocol | Rule |
|---|---|---|
| SLIMS pod → viewLinc | TCP 443 (HTTPS) + AD-bound | site-internal |
| SLIMS pod → LabWare LIMS | TCP 443 (HTTPS) + mTLS | site-internal |
| SLIMS pod → MasterControl | TCP 443 (HTTPS) + mTLS | site-internal |
| SLIMS pod → Vault QualityDocs | TCP 443 (HTTPS) | Vault-IP allowlist |
| APR consumer → SLIMS `/api/stability/*` | TCP 443 (HTTPS) | mTLS-gated, AD-bound |
| PostgreSQL primary ↔ replica | TCP 5432 | site-internal; TLS-required |
| OpenShift node → AD/LDAPS | TCP 636 | site-internal |
| OpenShift node → NTP | UDP 123 | site-internal |
| All audit → Splunk HEC | TCP 8088 (HTTPS) | site-internal |

### 7.9 Disaster-Recovery Design

| Aspect | Value |
|---|---|
| Primary site | OpenShift `stab-prod-ns` + PG primary; RPO 0 inside cluster |
| Warm-standby | DR-site PG replica via streaming replication + WAL; RPO ≤ 15 min (DS-PLAT-02) |
| Failover runbook | `HCT-RB-DR-001`; manual decision; RTO ≤ 4 h |
| Drill | annual joint exercise per `HCT-RB-DR-DRILL-001` |
| Vault QualityDocs | per Veeva SLA |
| MasterControl | per SaaS SLA |
| Vaisala viewLinc | per separate URS |

## 8. Site-Deployed Components

### 8.1 StabilityNexus Q1E Mini-SDS (Cat 4 statistical sub-component)

StabilityNexus is a vendor add-on but its Q1E engine is configured at the site for poolability + model selection. Sub-component mini-SDS:

#### 8.1.1 Logical View

| Component | Responsibility |
|---|---|
| `q1e_engine` | Candidate model fitting (linear, log-linear, sqrt); AIC selection; CI computation |
| `poolability_test` | ANCOVA slopes + intercepts (α = 0.25 / 0.25) per Q1E § 4.2 |
| `extrapolation_capper` | Enforces `min(2× observed, observed + 12 months)` cap per Q1E § 3.2.2 |
| `model_card_writer` | Emits model-fit JSON + PDF appendix for Vault filing |
| `ci_boundary_watcher` | Nightly job recomputes CI; emits CI-boundary alert (DS-SLE-03) |

#### 8.1.2 Algorithm Design

```
function q1e_select(data, candidates=["linear","log-linear","sqrt"]):
    fits = {model: fit(model, data) for model in candidates}
    aics = {model: aic(fits[model]) for model in candidates}
    selected = argmin(aics)
    return (selected, fits[selected])

function poolability_ancova(data_per_batch, alpha_slope=0.25, alpha_intercept=0.25):
    p_slope = ancova_test_slopes(data_per_batch)
    p_intercept = ancova_test_intercepts(data_per_batch)
    pooled_ok = (p_slope > alpha_slope) AND (p_intercept > alpha_intercept)
    return pooled_ok

function shelf_life(data, spec, observed_months):
    poolable = poolability_ancova(data)
    if poolable:
        fit = q1e_select(pool(data))
        sl_raw = solve(fit.upper_ci_95 == spec)
    else:
        fits = {batch: q1e_select(b) for batch, b in data.items()}
        sl_raw = min([solve(f.upper_ci_95 == spec) for f in fits.values()])
    sl_capped = min(sl_raw, 2 * observed_months, observed_months + 12)
    return sl_capped
```

#### 8.1.3 Numerical Precision

- Internal computation: IEEE 754 double-precision.
- AIC: `2k - 2 ln(L)` with `k = number of parameters` including σ²; `L = maximum likelihood`.
- CI: one-sided 95% upper or lower per attribute direction; t-distribution with `n - k` df.
- Boundary detection: Newton-Raphson root-finding on `f(t) - spec = 0` with abs-tol 1e-6 months.

#### 8.1.4 Model Specification References

| Module | Module Spec doc |
|---|---|
| `q1e_engine` | `HCT-MS-Q1E-ENGINE-001` |
| `poolability_test` | `HCT-MS-POOLABILITY-001` |
| `extrapolation_capper` | `HCT-MS-EXTRAP-CAP-001` |
| `model_card_writer` | `HCT-MS-MCWRITER-001` |
| `ci_boundary_watcher` | `HCT-MS-CIWATCH-001` |

### 8.2 MKT Recompute Job (`hct-stab-mkt-recompute.py`)

- **Language:** Python 3.12 inside `hct-stab-mkt-env` (cosign-signed).
- **Responsibility:** Hourly cron pulls chamber data from viewLinc, recomputes MKT per ICH Q1A(R2) § 2.1.7.2 across the relevant protocol-condition window, tags excursions to active pulls.
- **Interface:** viewLinc REST read; PostgreSQL write to `cv_chamber_mkt`.
- **Verification:** OQ-MKT-01 with reference dataset.
- **Module Spec reference:** `HCT-MS-MKT-001`.

### 8.3 Vault URN Resolver (`hct-stab-vaulturn.py`)

- **Language:** Python 3.12.
- **Responsibility:** Resolves Vault URN at form open + at signing events; verifies the protocol's referenced Vault document is current EFFECTIVE.
- **Interface:** Vault REST GET; SLIMS internal API write.
- **Verification:** OQ-VAULTURN-01.
- **Module Spec reference:** `HCT-MS-VAULTURN-001`.

### 8.4 Site-Deployed Component Deployment Pipeline

All Python components in 8.2/8.3 follow:

| Stage | Gate |
|---|---|
| Source | GitLab `halcyon/stab-tools`; protected `main`; Sigstore gitsign |
| Build | container image from pinned `python:3.12-slim`; SBOM (CycloneDX); cosign signature |
| Test | pytest unit + integration against sandbox viewLinc / Vault |
| Promote | dev → val → prod; dual sign (Data Engineering + Stability Coordinator) |
| Deploy | OpenShift `stab-prod-ns`; signed-image-only policy |
| Monitor | Prometheus → Splunk |

### 8.5 Observability Design

| Telemetry channel | Emitter | Sink | Use |
|---|---|---|---|
| SLIMS audit | SLIMS internal audit emitter | Splunk `gxp-stab-audit` | regulatory traceability |
| StabilityNexus Q1E run trace | Q1E engine | Splunk `gxp-stab-stat` | reproducibility |
| MKT recompute exception | `hct-stab-mkt-recompute.py` | Splunk `gxp-stab-ems` | EMS-integration health |
| Vault URN resolver outcome | `hct-stab-vaulturn.py` | Splunk `gxp-stab-vault` | broken-URN detection |
| Missed-pull deviation emit | scheduler | Splunk `gxp-stab-sched` | SLA monitoring |
| eQMS reconciliation summary | nightly job | Splunk `gxp-stab-eqmsrec` | webhook health |
| Performance — Q1E latency | StabilityNexus | Prometheus `stab_q1e_latency_seconds` | DS-PERF-01 verification |
| Performance — DR replication lag | PG operator | Prometheus `stab_replication_lag_seconds` | DR-02 detection |

### 8.6 Cron Schedule Inventory

| Job | Schedule | Owner |
|---|---|---|
| Missed-pull scheduler | daily 03:00 | Stability Coordinator |
| MKT recompute | hourly | Data Engineering |
| Vault URN resolver health-check | daily 04:00 | Data Engineering |
| eQMS reconciliation | daily 03:30 | Data Engineering |
| Backup `pg_basebackup` | daily 02:00 | IT / DBA |
| WAL archival | continuous | IT / DBA |
| Backup restore drill | quarterly | QA + IT (joint) |
| DR failover drill | annual | DR Team |
| RS expiry sweep | daily 05:00 | RS Custodian |
| Q5C method-revalidation alert | daily 06:00 | Method Owner |
| CI-boundary watcher | daily 23:00 | Statistician (auto) |
| Quarterly access review | quarterly | Security |
| Quarterly viewLinc URS reconciliation | quarterly | EMS Owner |

### 8.7 Failure-Mode Catalogue

| Failure | Detection | Recovery |
|---|---|---|
| viewLinc REST 5xx | EMS read job | retry 3× expo; on persistent → quarantine the affected chamber's pulls; ops paged |
| LIMS REST 5xx | LIMS sample-create / result-pull | retry 3× expo; DLQ at 4; missed-pull deviation if pull misses tolerance window |
| Vault URN 4xx | Vault URN resolver | form save rejected; Stability Coordinator informed |
| eQMS deviation push 5xx | DS-INT-EQMS-01 | retry 3× expo; DLQ at 5; nightly reconciliation backfills |
| PG primary outage | Patroni / Crunchy operator | automatic failover to replica; DR runbook if cluster-wide |
| Signature verification failure on container image | OpenShift Image Policy Webhook | pod refused; ops paged |
| StabilityNexus model-fit divergence | Q1E engine catches | model rejected; statistician notified to choose alternative |
| OpenShift `stab-prod-ns` pod crash-loop | OCP probe | Prometheus alert; ops paged |

## 9. References

### US
- 21 CFR Part 11 §§ .50, .70, .100, .200, .300
- FDA *Stability Testing of Drug Substances and Drug Products* (1998)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11; Annex 15
- EMA *Reflection paper on stability testing of advanced therapy medicinal products* (informational)

### DACH
- BfArM bekanntmachungen on stability data (informational)

### International
- ICH Q1A(R2), Q1B, Q1C, Q1D, Q1E, Q5C
- USP <659>, <1150>
- WHO TRS 953 Annex 2
- PIC/S PI 041; ISPE GAMP 5 (2nd Ed., 2022)
- NIST SP 800-218 SSDF (informational for site-deployed Python components)
- OWASP ASVS v4

### Vendor
- Genohm — *SLIMS Stability Module 6.7 Configuration Reference* (synthetic placeholder)
- Genohm — *SLIMS Administrator's Guide v6.7* (synthetic placeholder)
- Genohm — *StabilityNexus Reference Manual v2.4* (synthetic placeholder)
- Vaisala — *viewLinc 5.2 Continuous Monitoring System Administrator Guide* (cross-ref site EMS URS)
- LabWare — *LIMS 8 REST API Reference* (cross-ref LIMS URS)
- Veeva — *Vault QualityDocs 24R1 API Reference*
- MasterControl — *Deviation REST API Reference*

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) |
|---|---|
| DS-PLAT-01 | FS-PLAT-01 |
| DS-PLAT-02 | FS-PLAT-02 |
| DS-PLAT-03 | FS-PLAT-03 |
| DS-PLAT-04 | FS-PLAT-01 |
| DS-PLAT-05 | FS-DI-03 |
| DS-PROT-01 | FS-PROT-01 |
| DS-PROT-02 | FS-PROT-02 |
| DS-PROT-03 | FS-PROT-03 |
| DS-PROT-04 | FS-PROT-04 |
| DS-PROT-05 | FS-PROT-05 |
| DS-ZONE-01 | FS-ZONE-01 |
| DS-ZONE-02 | FS-ZONE-02 |
| DS-ZONE-03 | FS-ZONE-03 |
| DS-SCH-01 | FS-SCH-01 |
| DS-SCH-02 | FS-SCH-02 |
| DS-SCH-03 | FS-SCH-03 |
| DS-SCH-04 | FS-SCH-04 |
| DS-SCH-05 | FS-SCH-05 |
| DS-PHOTO-01 | FS-PHOTO-01 |
| DS-PHOTO-02 | FS-PHOTO-02 |
| DS-PHOTO-03 | FS-PHOTO-03 |
| DS-MATRIX-01 | FS-MATRIX-01 |
| DS-MATRIX-02 | FS-MATRIX-02 |
| DS-MATRIX-03 | FS-MATRIX-03 |
| DS-RES-01 | FS-RES-01 |
| DS-RES-02 | FS-RES-02 |
| DS-RES-03 | FS-RES-03 |
| DS-RES-04 | FS-RES-04 |
| DS-RES-05 | FS-RES-05 |
| DS-RES-06 | FS-RES-06 |
| DS-SLE-01 | FS-SLE-01 |
| DS-SLE-02 | FS-SLE-02 |
| DS-SLE-03 | FS-SLE-03 |
| DS-RS-01 | FS-RS-01 |
| DS-RS-02 | FS-RS-02 |
| DS-RS-03 | FS-RS-03 |
| DS-RS-04 | FS-RS-04 |
| DS-BIO-01 | FS-BIO-01 |
| DS-BIO-02 | FS-BIO-02 |
| DS-BIO-03 | FS-BIO-03 |
| DS-AUD-01 | FS-AUD-01 |
| DS-AUD-02 | FS-AUD-02 |
| DS-AUD-03 | FS-AUD-03 |
| DS-AUD-04 | FS-AUD-04 |
| DS-PART11-50 | FS-PART11-50 |
| DS-PART11-70 | FS-PART11-70 |
| DS-PART11-100 | FS-PART11-100 |
| DS-PART11-200 | FS-PART11-200 |
| DS-PART11-300 | FS-PART11-300 |
| DS-DI-01 | FS-DI-01 |
| DS-DI-02 | FS-DI-02 |
| DS-DI-03 | FS-DI-03 |
| DS-DI-04 | FS-DI-04 |
| DS-DI-05 | FS-DI-05 |
| DS-DI-06 | FS-DI-06 |
| DS-INT-LIMS-01 | FS-INT-LIMS-01 |
| DS-INT-EMS-01 | FS-INT-EMS-01 |
| DS-INT-VAULT-01 | FS-INT-VAULT-01 |
| DS-INT-EQMS-01 | FS-INT-EQMS-01, FS-XINT-EQMS-01 |
| DS-INT-EQMS-02 | FS-XINT-EQMS-02 |
| DS-INT-APR-01 | FS-INT-APR-01 |
| DS-BAK-01 | FS-BAK-01 |
| DS-BAK-02 | FS-BAK-02 |
| DS-PERF-01 | FS-PERF-01 |
| DS-SEC-01 | FS-SEC-01 |
| DS-TRN-01 | FS-TRN-01 |
| DS-PR-01 | FS-PR-01 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| DS-SNX-MOD-Q1E-01 | FS-RES-04 |
| DS-SNX-MOD-POOL-01 | FS-RES-05 |
| DS-SNX-MOD-EXTRAP-01 | FS-SLE-01 |
| DS-SNX-MOD-MCWRITER-01 | FS-SLE-02 |
| DS-SNX-MOD-CIWATCH-01 | FS-SLE-03 |
| DS-SCR-MKT-01 | FS-INT-EMS-01 |
| DS-SCR-VAULTURN-01 | FS-INT-VAULT-01 |
| DS-NET-01 | FS-PLAT-03, FS-XSYS-AD-01 |
| DS-DR-01 | FS-PLAT-02, FS-XSYS-BAK-01 |

## 11. Appendix B — Design-level Risk Register

| ID | Design risk | Likelihood | Impact | Mitigation in this DS |
|---|---|---|---|---|
| DR-01 | PostgreSQL append-only role grant inadvertently widened to UPDATE/DELETE on schema migration | Low | Critical | DS-AUD-02 + quarterly DB role-grant audit + CrunchyData operator GitOps manifest review |
| DR-02 | Streaming replication lag exceeds 15 min RPO target unnoticed | Medium | High | DS-PLAT-02 + Prometheus alert at lag > 10 min (50% of RPO) + DR drill annual |
| DR-03 | Q1E AIC selection picks a model with poor extrapolation behaviour (e.g., log-linear with steep slope) | Medium | Critical | DS-RES-04 statistician co-approval mandatory + model-fit plot review + DS-SLE-01 extrapolation cap |
| DR-04 | Poolability test α level (0.25) accepted batches that should have been per-batch | Medium | High | DS-RES-05 + statistician sign-off + DS-SLE-02 multi-step shelf-life approval |
| DR-05 | Extrapolation cap formula misapplied when `observed_months < 12` | Low | Critical | DS-SLE-01 + DS-SNX-MOD-EXTRAP-01 unit test coverage + OQ vector at `observed = 6, 11, 12, 13` |
| DR-06 | MKT recompute job (`hct-stab-mkt-recompute.py`) silently halts on viewLinc schema change | Medium | High | DS-SCR-MKT-01 hard schema-version validation; emits `MKT_SCHEMA_MISMATCH` event; Splunk alert |
| DR-07 | Vault URN resolution fails silently leaving stale protocol-link | Low | High | DS-SCR-VAULTURN-01 fail-closed: form save rejected if URN resolution returns non-EFFECTIVE |
| DR-08 | Chamber-qualification CMMS pull returns stale data; non-qualified chamber assigned | Low | Critical | DS-SCH-04 + CMMS-side service-level monitoring; on CMMS unavailable → DS-SCH-04 fails closed |
| DR-09 | Missed-pull deviation emission fails (DS-INT-EQMS-01 retry exhausted) | Medium | High | DS-INT-EQMS-01 DLQ at 5 + nightly reconciliation against `cv_missed_pulls` table |
| DR-10 | Photostability lamp-exposure capture analyst-typed value drifts from sensor truth | Low | High | DS-PHOTO-02 requires both visible AND near-UV minimums; lamp-exposure form requires sensor-source attestation |
| DR-11 | Matrixing-design integrity-loss flag missed when statistician on vacation | Low | High | DS-MATRIX-03 routes to statistician AND backup statistician + auto-escalate at 7 d |
| DR-12 | Q5C method revalidation expiry missed by 90-d alert (alert email filtered) | Low | High | DS-BIO-03 + Splunk alert + dashboard widget on Stability Coordinator portal |
| DR-13 | RS register expiry slip causes biased stability assay | Medium | Critical | DS-RS-02 pre-test gate fails closed + DS-RS-03 re-qualification workflow |
| DR-14 | ICH zone misalignment (e.g., Brazil registered as Zone II not IVa) | Low | Critical | DS-ZONE-02 market-zone mapping table + DS-ZONE-03 post-EFFECTIVE immutability + amendment workflow |
| DR-15 | Closed-loop eQMS gate (DS-INT-EQMS-02) webhook outage allows disposition without closure | Low | High | webhook + nightly reconciliation pull (similar pattern to DR-09); fail-closed |
| DR-16 | OpenShift SCC drift allows privileged container in `stab-prod-ns` | Low | High | DS-PLAT-04 + GitOps SCC manifest under change control; admission controller webhook enforces |
| DR-17 | mTLS cert expiry on LIMS / eQMS connector silently breaks integration | Medium | High | DS-INT-LIMS-01 + DS-INT-EQMS-01 cert rotation 90 d before expiry + 30 d operator alert |
| DR-18 | StabilityNexus Q1E numerical instability on near-zero-slope datasets | Low | High | DS-SNX-MOD-Q1E-01 + boundary OQ vector at slope = 1e-4 + statistician review of model-fit plot |
| DR-19 | Backup restore-drill skipped quarter, restore path stale | Low | Critical | DS-BAK-02 cron + Splunk metric `backup.last_drill_days` alerts at 95 d |
| DR-20 | NTP skew > 1 s on OpenShift node propagates incorrect contemporaneous timestamp | Low | High | DS-PLAT-05 chrony skew alert + DS-DI-03 NTP-only timestamps; out-of-sync node → quarantined |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
