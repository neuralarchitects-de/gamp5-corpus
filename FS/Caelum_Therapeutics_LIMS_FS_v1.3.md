---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; expanded 2026-05-12 (T3 catch-up, per-ID rows, ISO 17025 + OOS + parser-lifecycle implementations)"
seed_corpus_basis:
  - "CTX-URS-LIMS-001 v1.0 (parent URS, T3)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "21 CFR Part 211 §§ .22, .68, .180, .192"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11; USP <1058>; ISO/IEC 17025:2017"
parent_urs:
  document_number: CTX-URS-LIMS-001
  version: 1.0
  file: ../../URS/_generated/final/LIMS_Laboratory_Information_Management_System__Caelum_Therapeutics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## LIMS — LabWare LIMS 8 with QM/ELN

**Document Number:** CTX-FS-LIMS-001
**Version:** 1.1
**Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** CTX-URS-LIMS-001 v1.0
**Site:** Caelum Therapeutics Inc., QC Operations, North Building, Cambridge, Massachusetts, USA *(fictional)*
**System Owner:** QC Informatics Lead
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (with Cat-5 LIMS Basic sub-components under separate change control)
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; PIC/S PI 041; USP <1058>; ISO/IEC 17025:2017

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (QC Informatics Lead) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (LabWare Field Service) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — Head of QC) | _____________ | _____________ | _____ |
| Reviewer (Data Integrity Officer) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-12 | (synthetic) | T3 catch-up: per-ID FS rows for §§ 5.2 sample lifecycle, 5.3 method registry, 5.5 instrument data ingest, 5.6 parser lifecycle, 5.7 OOS, 5.8 COA, 5.9 stability, 5.10 supplier, 5.11 EM, 5.12 federation, 5.13 audit-trail review, 5.15 ISO 17025. No range compression. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## Definitions

Defined in `CTX-URS-LIMS-001`. Additional FS-specific terms:

| Term | Definition |
|---|---|
| LIMS Basic | LabWare's scripting language for site-specific extensions |
| LBSPP | LIMS Basic Stored Procedure (per site standard, all script entry points) |
| MASTER_TEMPLATE | LabWare's configuration object that drives sample-lifecycle state machine |
| Parser | An adapter that converts an instrument-data file into LIMS-structured results |
| AIQ | Analytical Instrument Qualification per USP <1058> |

---

## 1. Purpose

This FS defines the implementation of the requirements specified in the parent URS `CTX-URS-LIMS-001` v1.0. It describes the LabWare LIMS 8 cluster, configuration objects, LIMS Basic Cat-5 sub-components, the parser-lifecycle manager, and integrations.

## 2. Scope

LabWare LIMS 8 server cluster + clients + LIMS Basic scripts authored by Caelum's Quality IT — Custom Apps team, integrated to PAS-X, eQMS (MasterControl), SAP, Empower / Chromeleon / Qtegra CDS adapters, Vaisala viewLinc EM feed, the stability scheduler, the supplier-qualification register, and the Basel federation peer.

## 3. System Architecture

### 3.1 Component Inventory

| Component | Type | Vendor | Version |
|---|---|---|---|
| LIMS Application Server | Software | LabWare | LIMS 8.0 (8.0.4 patch) on RHEL 9.2 |
| Active App Servers | Hardware | Dell | PowerEdge R760 × 3 |
| Standby App Server | Hardware | Dell | PowerEdge R760 × 1 (cold) |
| Database | Software | Oracle | 19c Enterprise Edition + Data Guard |
| LabWare Web Client | Software | LabWare | LIMS Web 8 |
| LabWare ELN Module | Software | LabWare | ELN 8 |
| LIMS Basic Scripts | Software | In-house | per `ctx-lims-basic` repo |
| Parser Lifecycle Manager | Software | In-house | per `ctx-parsers` repo |
| LIMS Connectors (CDS) | Software | Vendor adapters | Empower 8.0.1, Chromeleon 7.3.2, Qtegra 2.10 |
| EM Feed Adapter | Software | In-house | `ctx-em-bridge` |
| Federation Service | Software | LabWare | LIMS Federation 8 |
| Authentication | Service | AD `caelum.local` via Keycloak | - |

### 3.2 Logical Architecture (textual)

```
Users (browser / ELN client)                  viewLinc EM (continuous)
        │                                            │
        ▼                                            ▼
[Active App Servers ×3 + Standby ×1] ◄── ctx-em-bridge
        │                        │
        │ LIMS Basic ──────────  │
        ▼                        ▼
[Oracle 19c + Data Guard standby]
        ▲     ▲     ▲     ▲     ▲     ▲     ▲
        │     │     │     │     │     │     │
        │     │     │     │     │     │     └── [Federation peer — Basel]
        │     │     │     │     │     └────── [Stability scheduler]
        │     │     │     │     └──────────── [Empower / Chromeleon / Qtegra adapters]
        │     │     │     └──────────────── [PAS-X via REST + Sample Lifecycle Bridge]
        │     │     └──────────────────── [SAP via PI/PO]
        │     └──────────────────────── [MasterControl eQMS via REST]
        └────────────────────────── [AD `caelum.local` via Keycloak]
```

### 3.3 Functional Modules

| Module | Provided by | Function |
|---|---|---|
| Sample Lifecycle Engine | LabWare core (configured) | Sample state machine and workflow gates |
| Aliquot + Storage Manager | LabWare QM (configured) | Aliquot creation + chain-of-custody |
| Specification + Method Library | LabWare core (configured) | Spec / method lifecycle |
| Result Engine | LabWare core + LIMS Basic | Calculations + spec evaluation |
| Parser Lifecycle Manager | In-house | Versioned instrument-data parsers |
| OOS Workflow Engine | LabWare QM + LIMS Basic | FDA-OOS-2022 Phase I/II workflow |
| COA Generator | LabWare core (configured) | PDF/A-3 COA + signature page |
| Stability Module | LabWare Stability | Pull-point schedules + ICH Q1E reports |
| Supplier Register | LabWare QM (configured) | Supplier qualification + lot-block logic |
| EM Bridge | In-house | viewLinc → LIMS continuous data ingest |
| Federation Service | LabWare Federation 8 | Cambridge ↔ Basel master-data + result transfer |
| eQMS Bridge | LIMS Basic + REST client | OOS / OOT auto-create deviations |
| PAS-X Bridge | LIMS Basic + REST client | Sample-create + result-return |
| SAP Bridge | PI/PO middleware | Result push to SAP for batch genealogy |
| Audit Trail | LabWare Pharma Compliance | Append-only audit-trail capture |
| Audit-Trail Review Tool | In-house | Focused-review filter per § 5.13 |

---

## 4. Functional Specifications

### 4.1 Platform / Hardware (URS § 5.1)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | App-server cluster N+1 (3 active + 1 standby on Dell R760 / RHEL 9.2); cold standby auto-promoted via runbook `CTX-RB-LIMS-FAILOVER-001`; Data Guard physical-standby Oracle 19c. |
| FS-PLAT-02 | URS-PLAT-02 | DR site cold replica in `caelum-dr-1`; Data Guard async lag SLA ≤ 15 min; failover runbook tested annually; RTO ≤ 4 h. |
| FS-PLAT-03 | URS-PLAT-03 | Patching SLA: 30 days for security; major versions per change control. Patch evidence retained in `CTX-PATCH-EVIDENCE`. |
| FS-PLAT-04 | URS-PLAT-04 | Basel passive secondary via LabWare Federation 8 transaction log shipping; replication lag metric `lims_federation_lag_seconds` alerts at 600s. |
| FS-PLAT-05 | URS-PLAT-05 | Rolling restart procedure `CTX-RB-LIMS-ROLLING-RESTART`: drains one app-server, restarts, re-attaches to load balancer; transactions complete on the remaining nodes. |

### 4.2 Sample Lifecycle (URS § 5.2)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SAMPLE-01 | URS-SAMPLE-01 | Sample-create endpoint `POST /api/lims/samples` is transactional: full sample record committed in a single Oracle transaction; failure rolls back; PAS-X order untouched; HTTP 5xx returned. |
| FS-SAMPLE-02 | URS-SAMPLE-02 | Sample fields enforced by MASTER_TEMPLATE `CTX-MT-SAMPLE-V1` (sample_id PK, parent_batch_fk, sample_type, sampling_point, sampling_user_id, sampling_ts, assigned_spec_fk); mandatory metadata not-null at INSERT. |
| FS-SAMPLE-03 | URS-SAMPLE-03 | LabWare workflow `CTX-SLW-001` defines states `LOGGED → RECEIVED → IN-STORAGE → SCHEDULED → IN-TEST → RESULTS-ENTERED → REVIEWED → APPROVED → RELEASED`; reverse transitions captured in `LW_AUDIT_STATE_REVERSAL` with mandatory reason. |
| FS-SAMPLE-04 | URS-SAMPLE-04 | Hold / quarantine via LBSPP `HoldOrQuarantineSample` — requires role `QC-Manager` or `QA-Manager`; reason text mandatory ≥ 30 chars; signature appended. |
| FS-SAMPLE-05 | URS-SAMPLE-05 | Aliquot generation via LabWare QM aliquot-creation form; child aliquot inherits parent's spec / batch / chain-of-custody; new aliquot ID assigned per `CTX-ALIQUOT-ID-SCHEME-v1`. |
| FS-SAMPLE-06 | URS-SAMPLE-06 | Storage location recorded in `LW_STORAGE_LOG` (location_id, custodian_id, temp_class enum [2-8C, -20C, -80C, AMBIENT], placement_ts); temperature class drives shelf-life calc. |
| FS-SAMPLE-07 | URS-SAMPLE-07 | Chain-of-custody check-out / check-in via LBSPP `ChainOfCustodyMove`; mandatory custodian + target; broken chain (check-out without check-in within 8 h) raises `CTX-ALRT-COC-BROKEN`. |
| FS-SAMPLE-08 | URS-SAMPLE-08 | Barcode + GS1 DataMatrix scanning via the LabWare Web Client camera-input field. |
| FS-SAMPLE-09 | URS-SAMPLE-09 | Shelf-life calculation in LBSPP `CalcShelfLife`; expiration alerts surface at D-7 and D-0 via the LabWare task inbox. |
| FS-SAMPLE-10 | URS-SAMPLE-10 | Sub-sampling for stability pull-points uses LabWare's protocol-aliquot feature; parent-batch FK preserved. |

### 4.3 Method Registry (URS § 5.3)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-METH-01 | URS-METH-01 | Method Registry implemented as LabWare master table `LW_METHOD_REG` with version, lifecycle state, validation-evidence URN, applicable-matrices array. |
| FS-METH-02 | URS-METH-02 | Method lifecycle `DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE` enforced via MASTER_TEMPLATE; ICH Q2(R2) validation-evidence URN required at REVIEW → APPROVED. |
| FS-METH-03 | URS-METH-03 | Sample-create denies non-EFFECTIVE method assignment; trigger `tr_method_effective` on `LW_SAMPLE`. |
| FS-METH-04 | URS-METH-04 | Method-state transitions e-signed via Pharma Compliance; AD-group SoD: `LIMS-Method-Author` ≠ `LIMS-Method-Approver`. |
| FS-METH-05 | URS-METH-05 | Database trigger `tr_method_effective_immutable` on `LW_METHOD_REG` raises exception on UPDATE/DELETE where `STATUS = EFFECTIVE`. |
| FS-METH-06 | URS-METH-06 | Quarterly report `CTX-RPT-METHOD-USAGE` surfaces samples-per-method, revalidation-due flags via LabWare Reports + Tableau. |
| FS-METH-07 | URS-METH-07 | Method record declares AIQ category (USP <1058> A/B/C) of instruments used; field `aiq_category` mandatory at APPROVED. |

### 4.4 Specifications (URS § 5.4)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SPEC-01 | URS-SPEC-01 | Specification lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE via MASTER_TEMPLATE `CTX-MT-SPEC-V1`. |
| FS-SPEC-02 | URS-SPEC-02 | Sample-create denies non-EFFECTIVE spec assignment; trigger logic in LBSPP `CheckSpecEffective`. |
| FS-SPEC-03 | URS-SPEC-03 | Transition signatures via Pharma Compliance (re-auth + meaning + cryptographic binding); SoD `LIMS-Spec-Author` ≠ `LIMS-Spec-Approver`. |
| FS-SPEC-04 | URS-SPEC-04 | Database trigger `tr_spec_effective_immutable` on `LW_SPEC_HEADER` raises exception on UPDATE/DELETE for `STATUS = EFFECTIVE`. |
| FS-SPEC-05 | URS-SPEC-05 | Limit-type enum `SINGLE`, `TWO_SIDED`, `RANGED`, `COUNT`, `ATTRIBUTE`, `SENSORY` per ICH Q6A; LBSPP `EvalAgainstSpec` selects per limit type. |
| FS-SPEC-06 | URS-SPEC-06 | LBSPP `CheckSpecEffectiveDateConflict` flags samples whose receipt date precedes the assigned spec's EFFECTIVE date; dispositioning required by QA Manager. |

### 4.5 Test Execution and Instrument-Data Ingest (URS § 5.5)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RES-01 | URS-RES-01 | CDS adapters write results into staging table `LW_RESULT_STAGE` with columns `raw_data_pointer`, `raw_data_sha256`; LBSPP `PromoteStageToResult` performs Promotion + Hash-Verify. |
| FS-RES-02 | URS-RES-02 | LIMS Basic calculations in repo `git.caelum.local/quality-it/ctx-lims-basic`; signed releases deployed via `ctx-lims-basic-release.yaml` GitHub Actions workflow with CR gate. |
| FS-RES-03 | URS-RES-03 | Spec evaluation runs on result commit; `OOS / OOT / OOE` flag persisted on the result record; LBSPP `EvalAgainstSpec`. |
| FS-RES-04 | URS-RES-04 | LBSPP `OnOosCreateDeviation` calls eQMS `POST /api/v2/deviations`; idempotency key `lims:result:<id>`; failure returns `403` to the LIMS UI and blocks approve. |
| FS-RES-05 | URS-RES-05 | Manual entry uses LBSPP `EnterDataDualKeyboard` enforcing two-user data entry with separate AD logins. |
| FS-RES-06 | URS-RES-06 | Review and approve gated by AD groups `LIMS-Reviewer` vs `LIMS-Approver`; signature payload bound to result-record SHA-256. |
| FS-RES-07 | URS-RES-07 | "Review by exception" Web view `CTX-VIEW-EXC-01` filters to records with `deviation_flag = 1 OR manual = 1 OR retest = 1 OR reprocessed = 1`. |
| FS-RES-08 | URS-RES-08 | Result commit checks `LW_INSTRUMENT_QUAL.status` for the executing instrument; non-qualified instrument returns commit error `INSTR_NOT_QUAL`. |
| FS-RES-09 | URS-RES-09 | Reagent / standard lot capture via the LabWare reagent-link panel; consumed-lots written to `LW_RESULT_REAGENTS`. |
| FS-RES-10 | URS-RES-10 | Analyst-witness signature triggered by the method-config `requires_witness = true`; LBSPP `RequireWitness` enforces SoD. |

### 4.6 Instrument Data Parser Lifecycle (URS § 5.6)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PARSE-01 | URS-PARSE-01 | Parsers in `git.caelum.local/quality-it/ctx-parsers`; each parser has `parser.yaml` (schema map, unit-test paths, USP-<1058>-cat). |
| FS-PARSE-02 | URS-PARSE-02 | Parser deployment to PRODUCTION via GitHub Actions `ctx-parsers-release.yaml` gated on Parser-Author ≠ Parser-Approver e-signatures and a passing regression suite against `golden-files/` corpus. |
| FS-PARSE-03 | URS-PARSE-03 | Each parsed result row stores `parser_name + parser_version`; raw files retained in S3 `s3://caelum-lims-raw/...`; parser changes never re-process historical results in-place. |
| FS-PARSE-04 | URS-PARSE-04 | Parser PR labelled `schema-change` triggers impact-assessment CI job; method-validation-review ticket auto-created. |
| FS-PARSE-05 | URS-PARSE-05 | Parser runtime errors written to `LW_PARSER_ERROR_Q`; LBSPP `OnParserErrorPauseSample` sets `sample.state = ERROR_HOLD`. |

### 4.7 OOS / OOT / OOE Workflow per FDA OOS (2022) (URS § 5.7)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-OOS-01 | URS-OOS-01 | LBSPP `OnOosCreatePhase1` calls MasterControl `POST /api/v2/oos-cases` within 1 h of commit; idempotency key `lims:result:<id>:oos`. |
| FS-OOS-02 | URS-OOS-02 | Phase-I form `CTX-OOS-PHASE1-FORM` captures analyst, instrument, method, reagent lots, equipment status, FDA-OOS-2022 laboratory checklist as required fields. |
| FS-OOS-03 | URS-OOS-03 | Workflow gate: case cannot transition `PHASE1 → PHASE2` without QA e-signature on `phase1_conclusion`. |
| FS-OOS-04 | URS-OOS-04 | Retest authorisation captured in `LW_OOS_RETEST` with QA signature, justification ≥ 100 chars; retest sample login blocked until row present. |
| FS-OOS-05 | URS-OOS-05 | Invalidation requires `assignable_cause` field (enum: analyst error, instrument error, reagent error, method limitation, environmental); `disagree_with_result` not in the enum. |
| FS-OOS-06 | URS-OOS-06 | SoD via AD groups: `LIMS-OOS-Investigator` ≠ `LIMS-OOS-Approver`; analyst-of-record locked out of retest until assignable-cause review resolved. |
| FS-OOS-07 | URS-OOS-07 | OOT detections routed to `stability-trending` or `inprocess-trending` queue based on `sample.type`. |
| FS-OOS-08 | URS-OOS-08 | Annual OOS / OOT trend report `CTX-RPT-OOS-ANNUAL` produced by LabWare Reports + Tableau; root-cause taxonomy per FDA OOS (2022). |

### 4.8 Result Release and COA Generation (URS § 5.8)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-COA-01 | URS-COA-01 | COA generator `CTX-COA-GEN-v3` produces PDF/A-3 per batch listing every released test, spec limit, reported result, analyst, approver, test date, COA generation ts. |
| FS-COA-02 | URS-COA-02 | COA PDF/A-3 includes signature page per § 11.50 (printed name, date/time, meaning); LabWare doc hash embedded as PDF metadata. |
| FS-COA-03 | URS-COA-03 | COA generation gated by LBSPP `CanIssueCoa`: every released test in Approved + no open deviations on the batch. |
| FS-COA-04 | URS-COA-04 | Layout templates in `CTX-COA-TEMPLATES`; per-customer overrides; layout changes require change-control ticket. |
| FS-COA-05 | URS-COA-05 | COA re-issuance versioned `vN`; prior version stamped "SUPERSEDED"; reason captured; signature provenance preserved. |

### 4.9 Stability Integration (URS § 5.9)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-STAB-01 | URS-STAB-01 | LabWare Stability module configured with pull-point matrix per protocol; LBSPP `OnPullPointArrivedCreateSample` auto-creates the login task. |
| FS-STAB-02 | URS-STAB-02 | LBSPP `CheckMissedPullPoints` runs daily; pull-points past grace window create eQMS deviation via `POST /api/v2/deviations` with category `STABILITY_MISSED_PULL`. |
| FS-STAB-03 | URS-STAB-03 | Stability trending engine `CTX-STAB-TREND` runs per ICH Q1E; significant-change flag triggers investigation ticket. |
| FS-STAB-04 | URS-STAB-04 | ICH-Q1E export `CTX-RPT-STAB-Q1E` available as PDF/A-3. |
| FS-STAB-05 | URS-STAB-05 | Stability protocol amendments require MasterControl CR ID in `LW_STAB_PROTOCOL.cr_ref`. |

### 4.10 Supplier and Raw-Material Qualification (URS § 5.10)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SUPP-01 | URS-SUPP-01 | Supplier Quality Register in LabWare table `LW_SUPPLIER_REG` (status, audit_cycle_ts, qualification_cert_urn). |
| FS-SUPP-02 | URS-SUPP-02 | LBSPP `BlockReceiptIfNotQualified` denies receipt; emergency override via Head-of-QA e-signature + deviation auto-created. |
| FS-SUPP-03 | URS-SUPP-03 | Receipt creates `LW_LOT_REG` row FK-linked to `LW_SUPPLIER_REG`; spec auto-assigned per material+supplier rule. |
| FS-SUPP-04 | URS-SUPP-04 | Quarterly supplier-trend report `CTX-RPT-SUPP-TREND` surfaces acceptance / OOS / on-time-delivery. |
| FS-SUPP-05 | URS-SUPP-05 | Requalification alerts at D-90/D-30/D-0 via the LabWare task inbox. |

### 4.11 Environmental Monitoring Integration (URS § 5.11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-EM-01 | URS-EM-01 | `ctx-em-bridge` daemon polls Vaisala viewLinc API at 60 s; writes to `LW_EM_DATA` with sensor_id, location, ts, value, qualified_instrument_status. |
| FS-EM-02 | URS-EM-02 | LBSPP `OnEmExcursionLinkBatches` queries `LW_BATCH` for batches In-Production at excursion-ts, creates eQMS deviation, links batches via `LW_DEVIATION_BATCH`. |
| FS-EM-03 | URS-EM-03 | Per-cleanroom trend report `CTX-RPT-EM-APQR` feeds the APQR generator. |

### 4.12 Multi-Site Federation (URS § 5.12)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-FED-01 | URS-FED-01 | LabWare Federation 8 configured with `CTX-FED-AUTH-RULES` per entity (methods authoritative at Cambridge; suppliers authoritative at Basel for EU vendors). |
| FS-FED-02 | URS-FED-02 | Inter-site transfer via LBSPP `FederationTransfer` requires Federation-Steward e-signature; source-site audit-trail copied verbatim. |
| FS-FED-03 | URS-FED-03 | Metric `lims_federation_lag_seconds` alerts at 600 s; dashboard `wel-lims-fed` displays per-link lag. |
| FS-FED-04 | URS-FED-04 | Federation-outage degraded-mode: local master-data read-only fallback; sample login uses last-known-good `LW_METHOD_REG` snapshot. |

### 4.13 Audit Trail and Annex 11 § 9 Review (URS § 5.13)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Pharma-Compliance audit trail covers tables: `LW_SAMPLE`, `LW_SPEC_HEADER`, `LW_METHOD_REG`, `LW_PARSER_REG`, `LW_RESULT`, `LW_LBSPP_RELEASE`, `LW_AUDIT_EVENT`, `LW_SIGNATURE`, `LW_CONFIG_BASELINE`. |
| FS-AUD-02 | URS-AUD-02 | DBA dual-control: audit-trail tables have separate `oracle-dba-audit` role required to alter; production app role restricted to INSERT/SELECT; UPDATE/DELETE blocked by role privileges + trigger. |
| FS-AUD-03 | URS-AUD-03 | Audit-trail review report templates `CTX-RPT-LIMS-AUDIT-BATCH` and `CTX-RPT-LIMS-AUDIT-QUARTERLY`; quarterly review evidence retained ≥ 25 y. |
| FS-AUD-04 | URS-AUD-04 | Retention 25 y; archive table partitioning by year; cold-storage to S3 object-lock with retention-mode COMPLIANCE. |
| FS-AUD-05 | URS-AUD-05 | Focused-audit-trail-review tool `CTX-AUD-FOCUSED-v2` filters to signatures, OOS, configuration changes, manual-data overrides per shift / per batch. |
| FS-AUD-06 | URS-AUD-06 | Exportable as CSV / PDF + chain-of-custody (SHA-256 manifest, watermark "REVIEWED — *date*"). |

### 4.14 21 CFR Part 11 / Annex 11 (URS § 5.14)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural controls in `CTX-SOP-CSV-01` cover validated SDLC, role definitions, change-control gates. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(b): PDF/A-3 + CSV exports verified by OQ-INSPECTION-COPY-01. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(d): access via AD + Keycloak MFA; admin break-glass `LW-DBA-Emergency` documented. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.50: Pharma-Compliance e-sign collects `printedName + dateTime + meaning`; required at every signature event. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.70: signature payload binds to result-record SHA-256 via HMAC-SHA256; tamper invalidates the signature. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.100: AD account ↔ HR mapping ensures uniqueness; provisioning blocks reassignment. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.200: Pharma-Compliance re-auth at signing; cached AD credentials not honoured. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.300: Keycloak password policy per site InfoSec (length 14, complexity, 90d max-age). |
| FS-ANX11-01 | URS-ANX11-01 | Validation evidence inventory in `CTX-VAL-EVID-INDEX`; IQ/OQ/PQ kept current via the periodic-review cycle. |
| FS-ANX11-02 | URS-ANX11-02 | Accuracy checks at data-entry boundaries: range checks (e.g., assay 0–200%), format (numeric, sig-figs), plausibility (delta-from-prior); LBSPP `AccuracyChecks`. |

### 4.15 ISO/IEC 17025 Alignment (URS § 5.15)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ISO-01 | URS-ISO-01 | Technical-records template `CTX-ISO17025-TECH-REC` captures uncertainty + repeatability fields for accredited methods. |
| FS-ISO-02 | URS-ISO-02 | COA generator includes ISO-17025-flagged content (laboratory name, customer / specimen ID, test method, measured value + uncertainty, date of issue). |
| FS-ISO-03 | URS-ISO-03 | Retention extended to max(accreditation-cycle + 25 y). |
| FS-ISO-04 | URS-ISO-04 | Web view `CTX-VIEW-ISO17025` filters to ISO-17025-flagged samples. |

### 4.16 Integrations (URS § 5.16)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-PASX-01 | URS-INT-PASX-01 | LBSPP `CreateSampleFromPasx` consumes PAS-X webhook; idempotency key `pasx:order:<id>:sample:<seq>`; correlation ID logged. |
| FS-INT-PASX-02 | URS-INT-PASX-02 | LBSPP `ReleaseToPasx` posts approved release results to PAS-X within 5 min P95; alerts on > 95th-percentile breach via Prometheus rule. |
| FS-INT-SAP-01 | URS-INT-SAP-01 | LBSPP `ReleaseToSap` posts batch genealogy via PI/PO; idempotency by `releaseId`. |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | OOS / OOT auto-create — see FS-RES-04 / FS-OOS-01. |
| FS-INT-CDS-01 | URS-INT-CDS-01 | CDS adapters connect via vendor-supplied APIs; raw-data files referenced by hash + path; LIMS does not modify CDS-side records. |
| FS-INT-CDS-02 | URS-INT-CDS-02 | Adapter versions pinned in `ctx-lims-basic/adapters.yaml` and tracked in CI. |
| FS-INT-AD-01 | URS-INT-AD-01 | AD authentication via Keycloak federation; service accounts in HashiCorp Vault. |
| FS-INT-EM-01 | URS-INT-EM-01 | `ctx-em-bridge` connects to viewLinc API with heartbeat at 60 s; lag metric. |
| FS-INT-STAB-01 | URS-INT-STAB-01 | Stability scheduler posts pull-point tasks via `POST /api/lims/stab-pullpoint`. |

### 4.17 Custom-Script SDLC (URS § 5.17)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DEV-01 | URS-DEV-01 | LIMS Basic in `ctx-lims-basic` repo; signed commits (Sigstore); CI: lint, unit tests, integration tests against a test LabWare. |
| FS-DEV-02 | URS-DEV-02 | Each LBSPP has a Model Card markdown sidecar with intended use, GAMP-Cat-5 risk assessment, FS, OQ test cases. |
| FS-DEV-03 | URS-DEV-03 | Production deployment via `ctx-lims-basic-release` GitHub Actions workflow gated on a passing regression suite + change-request approval. |
| FS-DEV-04 | URS-DEV-04 | Static analysis (LabWare-aware lint) + dependency scan (Trivy) on every CI build; vulnerabilities triaged within 30 d. |
| FS-DEV-05 | URS-DEV-05 | Release produces signed manifest `release-vN-manifest.json` with SHA-256 of every deployed LBSPP. |

### 4.18 Performance / Availability / Backup (URS § 5.18)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | Load test `CTX-LT-LIMS-300U-v1` validates 300-concurrent-user sample-page nav ≤ 2 s P95. |
| FS-PERF-02 | URS-PERF-02 | Bulk import via `POST /api/lims/results/bulk` handles 10,000 records in ≤ 10 min; SLA verified by `CTX-LT-LIMS-BULK-v1`. |
| FS-AV-01 | URS-AV-01 | Availability tracked via `wel-lims-availability` Grafana dashboard fed by SIEM. |
| FS-BAK-01 | URS-BAK-01 | RMAN nightly backup with PITR; retention 25 y. |
| FS-BAK-02 | URS-BAK-02 | Quarterly RMAN restore test, witnessed by QA; results in `CTX-BAK-RESTORE-LOG`. |

### 4.19 Security (URS § 5.19)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SEC-01 | URS-SEC-01 | All AD via Keycloak with MFA; break-glass `LW-DBA-Emergency` documented + audited monthly. |
| FS-SEC-02 | URS-SEC-02 | TLS 1.2+ enforced at the load balancer (HAProxy `ssl-min-ver TLSv1.2`). |
| FS-SEC-03 | URS-SEC-03 | Weekly vulnerability scans via Trivy + Tenable; criticals remediated within 30 d. |
| FS-SEC-04 | URS-SEC-04 | Annual pen-test by external assessor; findings tracked in `CTX-SEC-FINDINGS`. |
| FS-SEC-05 | URS-SEC-05 | HashiCorp Vault paths `kv/lims/service-accounts/*`; rotation policy 90 d. |

### 4.20 Training and Periodic Review (URS § 5.20)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Cornerstone curriculum `CTX-CURR-LIMS-Analyst-v1`; production access gated on completion. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher `CTX-CURR-LIMS-Refresher-2026` for Reviewer + Approver. |
| FS-TRN-03 | URS-TRN-03 | Advanced training `CTX-CURR-DI-Advanced` mandatory for Parser Authors + OOS Investigators. |
| FS-PR-01 | URS-PR-01 | Annual periodic-review template `CTX-PR-LIMS-YYYYMMDD`; sign-off by QC Informatics Lead + Head of QA. |

---


### 4.21 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem for the thick client and SAML 2.0 via Entra ID for the LabWare web client. Conditional-access binding to policy `Lab-App Conditional Access (MFA + device-compliance)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with Oracle RMAN for the LabWare Oracle backend; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.22 Cross-System Integration — Helios handover (M-XINT-HEL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HEL-01 | URS-XINT-HEL-01 | Audit-event publisher emits Kafka topic `helios.ingest.caelum.labware.v1` with schema-registry-pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`; at-least-once delivery; idempotency key `{source_system, event_id}`; back-pressure surfaced via Prometheus `helios_publish_lag_seconds` with 5-min alert at > 600 s. |
| FS-XINT-HEL-02 | URS-XINT-HEL-02 | Local audit-store retention policy enforces ≥ 15 y; Helios ack persisted as `helios_ack_ts` per event; periodic reconciliation job verifies parity (Helios row count == local published count) and raises a deviation in MasterControl on > 0.01% mismatch over a 24 h window. |

## 5. Interface Specifications

| IF ID | URS ID | Counterparty | Protocol | Direction | Notes |
|---|---|---|---|---|---|
| IF-PASX-SAMPLE-IN | URS-INT-PASX-01 | PAS-X | HTTPS POST `/api/lims/samples-from-pasx` | inbound | JSON; mTLS; idempotency `pasx:order:<id>:sample:<seq>` |
| IF-PASX-RELEASE-OUT | URS-INT-PASX-02 | PAS-X | HTTPS POST `https://pasx.caelum.local/api/v1/release-results` | outbound | JSON; mTLS; per-batch correlation |
| IF-SAP-RELEASE-OUT | URS-INT-SAP-01 | SAP | PI/PO `LIMS_RELEASE_RESULT_v3` | outbound | Idempotency by `releaseId` |
| IF-EQMS-DEV-OUT | URS-INT-EQMS-01 | MasterControl | HTTPS POST `/api/v2/deviations` | outbound | JSON; idempotency `lims:result:<id>` |
| IF-EQMS-OOS-OUT | URS-OOS-01 | MasterControl | HTTPS POST `/api/v2/oos-cases` | outbound | JSON; idempotency `lims:result:<id>:oos` |
| IF-CDS-IN-EMPOWER | URS-INT-CDS-02 | Waters Empower | Empower-LIMS Connector | inbound | hash + path forwarded |
| IF-CDS-IN-CHROMELEON | URS-INT-CDS-02 | Thermo Chromeleon | Chromeleon Sample List | inbound | hash + path forwarded |
| IF-CDS-IN-QTEGRA | URS-INT-CDS-02 | Thermo Qtegra | Qtegra LIMS Connector | inbound | hash + path forwarded |
| IF-EM-IN | URS-INT-EM-01 | Vaisala viewLinc | REST API + heartbeat | inbound | 60 s poll; lag metric |
| IF-STAB-IN | URS-INT-STAB-01 | Stability Scheduler | REST `POST /api/lims/stab-pullpoint` | inbound | sample auto-login |
| IF-AD-AUTH | URS-INT-AD-01 | AD via Keycloak | LDAPS / Kerberos / OIDC | bidirectional | groups: `LIMS-*` |
| IF-FED-CB | URS-FED-01 | LabWare Federation peer (Basel) | LabWare Federation 8 protocol | bidirectional | log shipping + transactional replication |

---

## 6. Data Model (high-level)

| Entity | Description |
|---|---|
| Sample | Per-test unit of work (MASTER_TEMPLATE) |
| Aliquot | Child sample with parent FK + chain-of-custody |
| StorageLog | Storage placement / movement events |
| Specification | Configured spec with limits per attribute |
| Method | Configured analytical method + AIQ category |
| Parser | Versioned instrument-data parser registration |
| Result | Per-attribute result with spec evaluation, parser_name, parser_version |
| OosCase | FDA-OOS-2022 Phase I / II case file |
| StabilityProtocol | Pull-point matrix + storage conditions |
| Supplier | Supplier qualification record |
| EmData | EM telemetry row |
| AuditEvent | Append-only audit-trail entry |
| LbspRelease | Release manifest of LIMS Basic deployment |
| ParserRelease | Release manifest of parser deployment |
| Signature | E-signature record (HMAC bound) |

---

## 7. Non-Functional Specifications

| Aspect | Target | URS reference |
|---|---|---|
| Concurrent users | 300 | URS-PERF-01 |
| Page nav P95 | ≤ 2 s | URS-PERF-01 |
| Bulk import | 10,000 records in ≤ 10 min | URS-PERF-02 |
| Availability | ≥ 99.5% business hours | URS-AV-01 |
| RPO / RTO | 15 min / 4 h | URS-PLAT-02 |
| Federation lag | < 600 s | URS-FED-03 |
| Audit retention | ≥ 25 y | URS-AUD-04 |
| Service-account rotation | 90 d | URS-SEC-05 |

---

## 8. Configuration Items

| CI ID | Item | Value |
|---|---|---|
| CI-01 | LabWare server pool URL | `https://lims.caelum.local` |
| CI-02 | Oracle SID | `LIMSPRD` (Data Guard primary) |
| CI-03 | LIMS Basic release tag | per `ctx-lims-basic` GitHub Releases |
| CI-04 | eQMS deviation endpoint | `https://eqms.caelum.local/api/v2` |
| CI-05 | eQMS OOS endpoint | `https://eqms.caelum.local/api/v2/oos-cases` |
| CI-06 | PAS-X release endpoint | `https://pasx.caelum.local/api/v1` |
| CI-07 | viewLinc API endpoint | `https://viewlinc.caelum.local/api` |
| CI-08 | Federation peer | `lims-basel.caelum.local` |
| CI-09 | NTP master | `ntp.caelum.local` |
| CI-10 | TLS minimum | 1.2 |
| CI-11 | LBSPP signing key | `caelum-sigstore-pubkey-2026q2` |
| CI-12 | Parser signing key | `caelum-sigstore-pubkey-parsers-2026q2` |
| CI-13 | Audit retention | 25 y (S3 Object Lock COMPLIANCE) |
| CI-14 | Federation lag alert threshold | 600 s |

---

## 9. Constraints / Assumptions / Risks

Inherited from `CTX-URS-LIMS-001`. FS-specific risks:

| Risk | Mitigation |
|---|---|
| LIMS Basic upgrade silently changes calc behaviour | OQ regression suite against reference dataset on every release |
| Parser silently regresses a historical result | FS-PARSE-03 retains immutable raw + parser-version on each result |
| CDS adapter version skew | Vendor adapters version-locked in CI; upgrades change-controlled |
| Oracle 19c DST patch causes timestamp drift | Quarterly DST-patch validation |
| Federation lag spike during heavy CDS bulk import | Lag alert at 600 s; degraded-mode runbook |
| OOS workflow misroute (Phase I → Phase II without QA sign-off) | DB-trigger gate on `phase1_conclusion` not null + signed |
| COA re-issuance drops the prior signature page | FS-COA-05 versioning + audit-trail preserved |

## 10. References

- `CTX-URS-LIMS-001 v1.0` (parent URS)
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .22, .68, .180, .192
- EU GMP Annex 11 §§ 4, 6, 9, 11
- FDA *Guidance for Industry: Investigating OOS Test Results* (2022)
- ICH Q2(R2), Q9(R1), Q10, Q1A(R2), Q1E
- USP <1058>; PIC/S PI 041
- ISO/IEC 17025:2017; ISO/IEC 27001:2022
- ISPE GAMP 5 (2nd ed., 2022); ISPE GAMP GPG *Validation of Laboratory Computerized Systems*
- LabWare — *LIMS 8.0 Installation, Configuration, and Administration Reference*
- Site documents: `CTX-RB-LIMS-FAILOVER-001`, `ctx-lims-basic` repo, `ctx-parsers` repo, `CTX-LT-LIMS-300U-v1`, `CTX-COA-GEN-v3`

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | Implementing FS ID |
|---|---|
| URS-PLAT-01 | FS-PLAT-01 |
| URS-PLAT-02 | FS-PLAT-02 |
| URS-PLAT-03 | FS-PLAT-03 |
| URS-PLAT-04 | FS-PLAT-04 |
| URS-PLAT-05 | FS-PLAT-05 |
| URS-SAMPLE-01 | FS-SAMPLE-01 |
| URS-SAMPLE-02 | FS-SAMPLE-02 |
| URS-SAMPLE-03 | FS-SAMPLE-03 |
| URS-SAMPLE-04 | FS-SAMPLE-04 |
| URS-SAMPLE-05 | FS-SAMPLE-05 |
| URS-SAMPLE-06 | FS-SAMPLE-06 |
| URS-SAMPLE-07 | FS-SAMPLE-07 |
| URS-SAMPLE-08 | FS-SAMPLE-08 |
| URS-SAMPLE-09 | FS-SAMPLE-09 |
| URS-SAMPLE-10 | FS-SAMPLE-10 |
| URS-METH-01 | FS-METH-01 |
| URS-METH-02 | FS-METH-02 |
| URS-METH-03 | FS-METH-03 |
| URS-METH-04 | FS-METH-04 |
| URS-METH-05 | FS-METH-05 |
| URS-METH-06 | FS-METH-06 |
| URS-METH-07 | FS-METH-07 |
| URS-SPEC-01 | FS-SPEC-01 |
| URS-SPEC-02 | FS-SPEC-02 |
| URS-SPEC-03 | FS-SPEC-03 |
| URS-SPEC-04 | FS-SPEC-04 |
| URS-SPEC-05 | FS-SPEC-05 |
| URS-SPEC-06 | FS-SPEC-06 |
| URS-RES-01 | FS-RES-01 |
| URS-RES-02 | FS-RES-02 |
| URS-RES-03 | FS-RES-03 |
| URS-RES-04 | FS-RES-04 |
| URS-RES-05 | FS-RES-05 |
| URS-RES-06 | FS-RES-06 |
| URS-RES-07 | FS-RES-07 |
| URS-RES-08 | FS-RES-08 |
| URS-RES-09 | FS-RES-09 |
| URS-RES-10 | FS-RES-10 |
| URS-PARSE-01 | FS-PARSE-01 |
| URS-PARSE-02 | FS-PARSE-02 |
| URS-PARSE-03 | FS-PARSE-03 |
| URS-PARSE-04 | FS-PARSE-04 |
| URS-PARSE-05 | FS-PARSE-05 |
| URS-OOS-01 | FS-OOS-01 |
| URS-OOS-02 | FS-OOS-02 |
| URS-OOS-03 | FS-OOS-03 |
| URS-OOS-04 | FS-OOS-04 |
| URS-OOS-05 | FS-OOS-05 |
| URS-OOS-06 | FS-OOS-06 |
| URS-OOS-07 | FS-OOS-07 |
| URS-OOS-08 | FS-OOS-08 |
| URS-COA-01 | FS-COA-01 |
| URS-COA-02 | FS-COA-02 |
| URS-COA-03 | FS-COA-03 |
| URS-COA-04 | FS-COA-04 |
| URS-COA-05 | FS-COA-05 |
| URS-STAB-01 | FS-STAB-01 |
| URS-STAB-02 | FS-STAB-02 |
| URS-STAB-03 | FS-STAB-03 |
| URS-STAB-04 | FS-STAB-04 |
| URS-STAB-05 | FS-STAB-05 |
| URS-SUPP-01 | FS-SUPP-01 |
| URS-SUPP-02 | FS-SUPP-02 |
| URS-SUPP-03 | FS-SUPP-03 |
| URS-SUPP-04 | FS-SUPP-04 |
| URS-SUPP-05 | FS-SUPP-05 |
| URS-EM-01 | FS-EM-01 |
| URS-EM-02 | FS-EM-02 |
| URS-EM-03 | FS-EM-03 |
| URS-FED-01 | FS-FED-01 |
| URS-FED-02 | FS-FED-02 |
| URS-FED-03 | FS-FED-03 |
| URS-FED-04 | FS-FED-04 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
| URS-AUD-05 | FS-AUD-05 |
| URS-AUD-06 | FS-AUD-06 |
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
| URS-ISO-01 | FS-ISO-01 |
| URS-ISO-02 | FS-ISO-02 |
| URS-ISO-03 | FS-ISO-03 |
| URS-ISO-04 | FS-ISO-04 |
| URS-INT-PASX-01 | FS-INT-PASX-01 |
| URS-INT-PASX-02 | FS-INT-PASX-02 |
| URS-INT-SAP-01 | FS-INT-SAP-01 |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 |
| URS-INT-CDS-01 | FS-INT-CDS-01 |
| URS-INT-CDS-02 | FS-INT-CDS-02 |
| URS-INT-AD-01 | FS-INT-AD-01 |
| URS-INT-EM-01 | FS-INT-EM-01 |
| URS-INT-STAB-01 | FS-INT-STAB-01 |
| URS-DEV-01 | FS-DEV-01 |
| URS-DEV-02 | FS-DEV-02 |
| URS-DEV-03 | FS-DEV-03 |
| URS-DEV-04 | FS-DEV-04 |
| URS-DEV-05 | FS-DEV-05 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-AV-01 | FS-AV-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-SEC-05 | FS-SEC-05 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-TRN-03 | FS-TRN-03 |
| URS-PR-01 | FS-PR-01 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-HEL-01 | FS-XINT-HEL-01 |
| URS-XINT-HEL-02 | FS-XINT-HEL-02 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

The following risks are documented for downstream evaluation in the Risk Assessment.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Script defect causing incorrect calculation | Medium | High | URS-DEV-01..05 + OQ |
| R-02 | CDS-ingest data tampering | Low | High | URS-INT-CDS-01..02; URS-PARSE-03 |
| R-03 | OOS workflow bypass | Medium | Critical | URS-OOS-01..06 |
| R-04 | Audit-trail tampering | Low | Critical | URS-AUD-02; URS-PART11-05 |
| R-05 | Unauthorised result approval | Low | High | URS-PART11-06; SoD |
| R-06 | Chain-of-custody break during shift change | Medium | Medium | URS-SAMPLE-07 |
| R-07 | Parser deployment regresses prior parsed values | Low | High | URS-PARSE-03 |
| R-08 | Federation drift between Cambridge and Basel master data | Medium | Medium | URS-FED-01..04 |
| R-09 | Stability pull-point missed (eQMS deviation not raised) | Low | High | URS-STAB-02 |
| R-10 | EM excursion not linked to in-progress batches | Medium | High | URS-EM-02 |
| R-11 | COA re-issuance loses signature provenance | Low | High | URS-COA-05 |
| R-12 | ISO 17025 surveillance finds incomplete technical record | Low | Medium | URS-ISO-01..04 |

Full evaluation in `CTX-RA-LIMS-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
