---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (v1.0 DS corpus ship)"
seed_corpus_basis:
  - "CTX-FS-LIMS-001 v1.1 (parent FS, T3 Cat 4)"
  - "CTX-URS-LIMS-001 v1.0 (parent URS, transitive)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 Configuration Specification conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Part 211"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11; PIC/S PI 041"
  - "FDA OOS (2022); ICH Q2(R2), Q9(R1), Q10, Q1A(R2), Q1E"
  - "USP <1058>; ISO/IEC 17025:2017; ISO/IEC 27001:2022"
  - "LabWare LIMS 8 — System Administrator Reference + Configuration Reference"
parent_fs:
  document_number: CTX-FS-LIMS-001
  version: "1.1"
  file: ../../../FS_FDS/_generated/final/Caelum_Therapeutics_LIMS_FS_v1.3.md
parent_urs:
  document_number: CTX-URS-LIMS-001
  version: "1.1"
  file: ../../../URS/_generated/final/LIMS_Laboratory_Information_Management_System__Caelum_Therapeutics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## LIMS — LabWare LIMS 8 with QM/ELN — Caelum Therapeutics Cambridge Tenancy

**Document Number:** CTX-DS-LIMS-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** CTX-FS-LIMS-001 v1.1
**Parent URS:** CTX-URS-LIMS-001 v1.0
**Site:** Caelum Therapeutics Inc., QC Operations, North Building, Cambridge, Massachusetts, USA *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (with site-developed Cat-5 LIMS Basic sub-components under separate change control)
**Project Mode:** Greenfield-with-Federation (Cambridge primary; Basel federation peer)
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; PIC/S PI 041; USP <1058>; ISO/IEC 17025:2017

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Informatics Lead) | _____________ | _____________ | _____ |
| Reviewer (QA Reviewer) | _____________ | _____________ | _____ |
| Reviewer (System Owner — Head of QC) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — Head of Quality) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (SME — Mass-Spec / Chromatography Lead) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue. Inherited Tier T3 from parent URS+FS pair. DS covers 113/113 FS-IDs; 0 FS-IDs flagged as vendor-internal — no site design surface. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

| Term | Definition |
|---|---|
| CI | Configuration Item — one configurable parameter or grouped parameter set in LabWare LIMS 8 |
| LBSPP | LIMS Basic Stored Procedure (LabWare scripting entry point) |
| MASTER_TEMPLATE | LabWare configuration object that drives a lifecycle / record schema |
| AIQ | Analytical Instrument Qualification (USP <1058>) |
| Verified by | Planned IQ / OQ / PQ test that verifies the configuration choice |

## 1. Purpose

This Configuration Specification (CS) records the technical design of the LabWare LIMS 8 cluster, configuration parameters, LIMS Basic Cat-5 sub-components, parser-lifecycle manager, and integration bindings that implement the functional behaviour specified in `CTX-FS-LIMS-001` v1.1. It is the FS-namespace-dependent design artefact: each DS-ID traces to ≥ 1 FS-ID via § N+1 Traceability Matrix.

## 2. Scope

**In scope:** LabWare LIMS 8.0.4 application server cluster, Oracle 19c Data Guard primary, LabWare Web Client + ELN module configuration, LIMS Basic site-developed scripts authored by Caelum's Quality IT — Custom Apps team, Parser Lifecycle Manager site-code, CDS / EM / SAP / PAS-X / eQMS integration bindings, Federation 8 Cambridge-Basel link, AD-via-Keycloak authentication binding, and the site-developed `ctx-em-bridge` adapter.

**Out of scope:** LabWare vendor source-code internals (vendor SDLC owns those); Oracle 19c vendor internals; vendor adapter source-code (Empower-LIMS Connector, Chromeleon Sample-List, Qtegra LIMS Connector); Cornerstone LMS internals; viewLinc vendor internals. Site-deployed Cat-5 sub-components (LIMS Basic scripts + parsers + `ctx-em-bridge`) are designed per § 8 with mini-SDS rules.

## 3. Architectural Overview

The Cambridge deployment is a three-active-plus-one-cold-standby LabWare application-server cluster behind an HAProxy load balancer, backed by an Oracle 19c primary with a Data Guard physical standby. Site-developed Cat-5 components (LIMS Basic scripts, parsers, `ctx-em-bridge`) ship via signed GitHub Actions release manifests. Federation 8 ships the master-data + result subset to Basel as the passive secondary. AD-via-Keycloak provides MFA-bound authentication; HashiCorp Vault holds service-account secrets.

```
                                ┌────────────────────────────┐
                                │   AD `caelum.local`         │
                                │       (via Keycloak OIDC)   │
                                └─────────────┬──────────────┘
                                              │
                       ┌──────────────────────┴─────────────────────┐
                       │            HAProxy (TLS 1.2+)              │
                       │  https://lims.caelum.local                 │
                       └──┬───────────┬──────────────┬───────────────┘
                          │           │              │
              ┌───────────▼──┐  ┌─────▼────────┐  ┌──▼──────────┐  cold
              │ App-Node-01  │  │ App-Node-02  │  │ App-Node-03 │  ┌───────────┐
              │ RHEL 9.2     │  │ RHEL 9.2     │  │ RHEL 9.2    │──│ Standby-04 │
              │ LabWare 8.0.4│  │ LabWare 8.0.4│  │ LabWare 8.04│  └───────────┘
              └──────┬───────┘  └──────┬───────┘  └──────┬──────┘
                     │                 │                 │
                     └────────┬────────┴────────┬────────┘
                              │                 │
                         ┌────▼─────────────────▼────┐
                         │   Oracle 19c (LIMSPRD)    │
                         │   Data Guard primary       │
                         └────────────┬─────────────┘
                                      │
                              physical-standby (async ≤ 15 min)
                                      │
                         ┌────────────▼─────────────┐
                         │   Oracle 19c (LIMSDR)    │
                         │   caelum-dr-1            │
                         └─────────────────────────┘

       LBSPP / Parser CI/CD ──► GitHub Actions ──► signed release manifest ──► PRODUCTION
       Federation 8 (log shipping + transactional replication) ──► Basel passive secondary
```

### 3.1 Topology rationale (text)

Three active app-server nodes deliver headroom for the 300-concurrent-user steady-state load with sufficient capacity for rolling-restart maintenance windows; the cold standby (Node-04) is auto-promoted via runbook `CTX-RB-LIMS-FAILOVER-001` when the active count drops below two. Data Guard is configured for asynchronous physical-standby replication to keep primary-write latency low; observed lag is monitored via Prometheus and alerts at 600 s. Federation 8 ships methods authoritatively from Cambridge and supplier records authoritatively from Basel; site-local fallback uses the last-known-good `LW_METHOD_REG` snapshot during a Federation outage.

### 3.2 Component-design inventory

| Layer | Component | Vendor / source | Version | Site design surface |
|---|---|---|---|---|
| Application | LabWare LIMS 8 | LabWare | 8.0.4 patch | Configuration (§ 4) |
| Application | LabWare Web Client | LabWare | LIMS Web 8 | Configuration (§ 4) |
| Application | LabWare ELN Module | LabWare | ELN 8 | Configuration (§ 4) |
| Site-developed Cat-5 | LIMS Basic scripts | In-house (`ctx-lims-basic`) | per release | § 8 mini-SDS |
| Site-developed Cat-5 | Parser Lifecycle | In-house (`ctx-parsers`) | per release | § 8 mini-SDS |
| Site-developed Cat-5 | `ctx-em-bridge` | In-house | per release | § 8 mini-SDS |
| Federation | LabWare Federation 8 | LabWare | 8 | Configuration (§ 4) |
| Database | Oracle EE + Data Guard | Oracle | 19c | Configuration (§ 4 — site-binding only) |
| OS / hardware | RHEL 9.2 on Dell PowerEdge R760 | RedHat / Dell | RHEL 9.2 / R760 | Infra-qualification (referenced) |
| Identity | AD `caelum.local` via Keycloak | Microsoft / Keycloak | per site IT | Configuration (§ 4) |

---

## 4. Configuration Specification

### 4.1 Platform / Hardware bindings

| CI-ID | Configuration item (named per vendor) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PLAT-01 | LabWare cluster topology (`LW_CLUSTER_TOPOLOGY`) | `3-active+1-cold-standby` | Custom | Headroom for 300-CU load + rolling-restart window | FS-PLAT-01 | IQ-LIMS-CLUSTER-01 |
| DS-PLAT-02 | Standby promotion runbook reference (`LW_FAILOVER_RB`) | `CTX-RB-LIMS-FAILOVER-001` | Custom | Site-specific runbook ID required for traceability | FS-PLAT-01 | OQ-LIMS-FAILOVER-01 |
| DS-PLAT-03 | Oracle Data Guard mode (`DG_PROTECTION_MODE`) | `MAX PERFORMANCE` (async) | Default | Lower primary-write latency for QC throughput | FS-PLAT-01, FS-PLAT-02 | IQ-DG-01 |
| DS-PLAT-04 | Data Guard async lag SLA (`DG_LAG_ALERT_SECONDS`) | `900` (15 min) | Custom | Aligns with FS RTO ≤ 4 h budget at DR site | FS-PLAT-02 | OQ-DG-LAG-01 |
| DS-PLAT-05 | DR site replica id (`DR_SITE_ID`) | `caelum-dr-1` | Custom | Site-binding identifier | FS-PLAT-02 | IQ-DR-01 |
| DS-PLAT-06 | DR failover runbook (`DR_FAILOVER_RB`) | `CTX-RB-LIMS-DR-FAILOVER` | Custom | Annual-test discipline anchor | FS-PLAT-02 | PQ-DR-RECOVERY-01 |
| DS-PLAT-07 | Patch SLA security (`PATCH_SLA_SECURITY_DAYS`) | `30` | Default | Site InfoSec policy default | FS-PLAT-03 | OQ-PATCH-CADENCE-01 |
| DS-PLAT-08 | Patch evidence store (`PATCH_EVIDENCE_DIR`) | `CTX-PATCH-EVIDENCE` | Custom | Inspection-evidence binding | FS-PLAT-03 | OQ-PATCH-EVIDENCE-01 |
| DS-PLAT-09 | Federation 8 protocol (`FED_PROTOCOL`) | `LabWare Federation 8 transactional log shipping` | Default | Vendor-recommended primary mode | FS-PLAT-04 | IQ-FED-01 |
| DS-PLAT-10 | Federation lag alert threshold (`FED_LAG_ALERT_S`) | `600` | Custom | Aligns with FS-PLAT-04 alert binding | FS-PLAT-04 | OQ-FED-LAG-01 |
| DS-PLAT-11 | Rolling-restart runbook (`ROLLING_RESTART_RB`) | `CTX-RB-LIMS-ROLLING-RESTART` | Custom | Operational continuity binding | FS-PLAT-05 | OQ-ROLLING-RESTART-01 |

### 4.2 Sample Lifecycle CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-SAMPLE-01 | Sample-create endpoint transactionality (`LW_API_TX_MODE`) | `single-tx-with-rollback` | Default | Atomicity per FS-SAMPLE-01; rollback on failure | FS-SAMPLE-01 | OQ-SAMPLE-CREATE-TX-01 |
| DS-SAMPLE-02 | Sample MASTER_TEMPLATE id (`SAMPLE_MT_ID`) | `CTX-MT-SAMPLE-V1` | Custom | Site-specific schema | FS-SAMPLE-02 | OQ-SAMPLE-SCHEMA-01 |
| DS-SAMPLE-03 | Sample mandatory fields enforcement (`LW_FIELD_NULL_POLICY`) | `NOT NULL at INSERT` | Default | Server-side validation | FS-SAMPLE-02 | OQ-SAMPLE-NULLABILITY-01 |
| DS-SAMPLE-04 | Sample workflow id (`LW_WORKFLOW_ID`) | `CTX-SLW-001` | Custom | Site workflow naming | FS-SAMPLE-03 | OQ-SAMPLE-LIFECYCLE-01 |
| DS-SAMPLE-05 | Sample state list (`LW_STATES`) | `LOGGED, RECEIVED, IN-STORAGE, SCHEDULED, IN-TEST, RESULTS-ENTERED, REVIEWED, APPROVED, RELEASED` | Custom | 9-state lifecycle per FS-SAMPLE-03 | FS-SAMPLE-03 | OQ-SAMPLE-STATES-01 |
| DS-SAMPLE-06 | Reverse-transition audit table (`LW_AUDIT_STATE_REVERSAL`) | enabled w/ mandatory reason ≥ 30 chars | Custom | Audit-trail completeness | FS-SAMPLE-03 | OQ-SAMPLE-REVERSE-01 |
| DS-SAMPLE-07 | Hold/quarantine LBSPP (`HoldOrQuarantineSample`) | role-gated `QC-Manager` OR `QA-Manager`; reason ≥ 30 chars | Custom | SoD on critical-action | FS-SAMPLE-04 | OQ-SAMPLE-HOLD-01 |
| DS-SAMPLE-08 | Aliquot ID scheme (`CTX-ALIQUOT-ID-SCHEME-v1`) | `<parent>-A<seq:03d>` | Custom | Chain-of-custody readability | FS-SAMPLE-05 | OQ-ALIQUOT-ID-01 |
| DS-SAMPLE-09 | Storage temp class enum (`LW_TEMP_CLASS`) | `[2-8C, -20C, -80C, AMBIENT]` | Custom | Aligns with cold-chain matrix | FS-SAMPLE-06 | OQ-STORAGE-TEMP-01 |
| DS-SAMPLE-10 | Storage log table (`LW_STORAGE_LOG`) | columns: location_id, custodian_id, temp_class, placement_ts | Custom | Site-traceable schema | FS-SAMPLE-06 | OQ-STORAGE-LOG-01 |
| DS-SAMPLE-11 | Chain-of-custody LBSPP (`ChainOfCustodyMove`) | mandatory custodian + target | Custom | SoD enforcement | FS-SAMPLE-07 | OQ-COC-01 |
| DS-SAMPLE-12 | Broken-chain alert (`CTX-ALRT-COC-BROKEN`) | trigger at check-out-without-check-in > 8 h | Custom | 8-h window aligns with shift cycle | FS-SAMPLE-07 | OQ-COC-BROKEN-01 |
| DS-SAMPLE-13 | Barcode input mode (`LW_BARCODE_MODE`) | `Web-Client camera + GS1 DataMatrix` | Default | LabWare native | FS-SAMPLE-08 | OQ-BARCODE-01 |
| DS-SAMPLE-14 | Shelf-life LBSPP (`CalcShelfLife`) | per material spec + temp-class | Custom | Site-formulary binding | FS-SAMPLE-09 | OQ-SHELF-LIFE-01 |
| DS-SAMPLE-15 | Expiration alert cadence (`SHELF_LIFE_ALERTS`) | `D-7, D-0` | Default | LabWare task inbox default | FS-SAMPLE-09 | OQ-EXPIRY-ALERT-01 |
| DS-SAMPLE-16 | Stability protocol-aliquot binding | `protocol-aliquot` feature enabled w/ parent_batch FK preservation | Default | ICH Q1A traceability | FS-SAMPLE-10 | OQ-STAB-ALIQUOT-01 |

### 4.3 Method Registry CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-METH-01 | Method registry table (`LW_METHOD_REG`) | LabWare master table w/ version, lifecycle, evidence URN, matrices[] | Custom | Site schema | FS-METH-01 | OQ-METHOD-REG-01 |
| DS-METH-02 | Method MASTER_TEMPLATE id (`METHOD_MT_ID`) | `CTX-MT-METHOD-V1` | Custom | Site-naming | FS-METH-02 | OQ-METHOD-MT-01 |
| DS-METH-03 | Method state list (`LW_METHOD_STATES`) | `DRAFT, REVIEW, APPROVED, EFFECTIVE, OBSOLETE` | Custom | 5-state lifecycle | FS-METH-02 | OQ-METHOD-STATES-01 |
| DS-METH-04 | ICH Q2(R2) evidence requirement (`METHOD_VAL_GATE`) | required at REVIEW → APPROVED | Custom | Regulator binding | FS-METH-02 | OQ-METHOD-VAL-EVID-01 |
| DS-METH-05 | Effective-method enforcement trigger (`tr_method_effective`) | DB trigger on `LW_SAMPLE` | Custom | Server-side enforcement | FS-METH-03 | OQ-METHOD-EFFECTIVE-01 |
| DS-METH-06 | Method SoD groups (`AD: LIMS-Method-Author`, `LIMS-Method-Approver`) | distinct AD groups, exclusive membership | Custom | Part 11 § 11.10 / Annex 11 § 4 SoD | FS-METH-04 | OQ-METHOD-SOD-01 |
| DS-METH-07 | Method immutability trigger (`tr_method_effective_immutable`) | `UPDATE/DELETE` blocked where status=EFFECTIVE | Custom | Audit-trail integrity | FS-METH-05 | OQ-METHOD-IMMUT-01 |
| DS-METH-08 | Method usage report (`CTX-RPT-METHOD-USAGE`) | quarterly Tableau + LabWare Reports | Custom | Trending discipline | FS-METH-06 | PQ-METHOD-REPORT-01 |
| DS-METH-09 | AIQ category field (`METHOD.aiq_category`) | enum `USP <1058> A/B/C`, mandatory at APPROVED | Custom | Regulator binding | FS-METH-07 | OQ-AIQ-FIELD-01 |

### 4.4 Specification CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-SPEC-01 | Spec MASTER_TEMPLATE (`SPEC_MT_ID`) | `CTX-MT-SPEC-V1` | Custom | Site naming | FS-SPEC-01 | OQ-SPEC-MT-01 |
| DS-SPEC-02 | Effective-spec check LBSPP (`CheckSpecEffective`) | denies non-EFFECTIVE assignment | Custom | Spec-currency enforcement | FS-SPEC-02 | OQ-SPEC-EFFECTIVE-01 |
| DS-SPEC-03 | Spec SoD groups (`LIMS-Spec-Author` ≠ `LIMS-Spec-Approver`) | exclusive AD groups | Custom | Part 11 SoD | FS-SPEC-03 | OQ-SPEC-SOD-01 |
| DS-SPEC-04 | Spec immutability trigger (`tr_spec_effective_immutable`) | UPDATE/DELETE blocked at EFFECTIVE | Custom | Tamper protection | FS-SPEC-04 | OQ-SPEC-IMMUT-01 |
| DS-SPEC-05 | Limit-type enumeration (`SPEC_LIMIT_TYPES`) | `SINGLE, TWO_SIDED, RANGED, COUNT, ATTRIBUTE, SENSORY` | Custom | Per ICH Q6A | FS-SPEC-05 | OQ-SPEC-LIMITS-01 |
| DS-SPEC-06 | Eval-against-spec LBSPP (`EvalAgainstSpec`) | dispatches per `limit_type` | Custom | Calculation correctness | FS-SPEC-05 | OQ-SPEC-EVAL-01 |
| DS-SPEC-07 | Date-conflict LBSPP (`CheckSpecEffectiveDateConflict`) | flags sample-receipt-before-spec-EFFECTIVE | Custom | Regulator-grade dispositioning | FS-SPEC-06 | OQ-SPEC-DATE-CONFLICT-01 |

### 4.5 Result Engine CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RES-01 | Result staging table (`LW_RESULT_STAGE`) | columns include `raw_data_pointer`, `raw_data_sha256` | Custom | Tamper-evident pointer | FS-RES-01 | OQ-RESULT-STAGE-01 |
| DS-RES-02 | Promotion LBSPP (`PromoteStageToResult`) | hash-verify before promote | Custom | Data-integrity discipline | FS-RES-01 | OQ-PROMOTE-HASH-01 |
| DS-RES-03 | LIMS Basic repo (`LBSPP_REPO_URL`) | `git.caelum.local/quality-it/ctx-lims-basic` | Custom | Site source-of-truth | FS-RES-02 | IQ-LBSPP-REPO-01 |
| DS-RES-04 | LBSPP release workflow (`LBSPP_RELEASE_WF`) | `ctx-lims-basic-release.yaml` (GitHub Actions) | Custom | CR gate enforcement | FS-RES-02 | OQ-LBSPP-RELEASE-01 |
| DS-RES-05 | Spec-eval-on-commit LBSPP (`EvalAgainstSpec`) | invoked at result commit; persists OOS/OOT/OOE flag | Custom | Inline disposition | FS-RES-03 | OQ-RESULT-COMMIT-01 |
| DS-RES-06 | Deviation-creation LBSPP (`OnOosCreateDeviation`) | calls eQMS `POST /api/v2/deviations`; idempotency `lims:result:<id>`; failure returns 403 | Custom | Idempotent integration | FS-RES-04 | OQ-OOS-DEV-CREATE-01 |
| DS-RES-07 | Dual-keyboard LBSPP (`EnterDataDualKeyboard`) | two-user data entry with separate AD logins | Custom | Manual-entry integrity | FS-RES-05 | OQ-DUAL-KB-01 |
| DS-RES-08 | Reviewer / Approver AD groups (`LIMS-Reviewer`, `LIMS-Approver`) | exclusive membership; sig payload bound to result SHA-256 | Custom | SoD + Part 11 § 11.70 | FS-RES-06 | OQ-REVIEW-APPROVE-01 |
| DS-RES-09 | Review-by-exception view (`CTX-VIEW-EXC-01`) | filter `deviation_flag = 1 OR manual = 1 OR retest = 1 OR reprocessed = 1` | Custom | Workflow efficiency | FS-RES-07 | OQ-REVIEW-EXC-01 |
| DS-RES-10 | Instrument-qualification check (`INSTR_QUAL_CHECK`) | result commit reads `LW_INSTRUMENT_QUAL.status`; non-qualified returns `INSTR_NOT_QUAL` | Custom | USP <1058> binding | FS-RES-08 | OQ-INSTR-QUAL-01 |
| DS-RES-11 | Reagent-link table (`LW_RESULT_REAGENTS`) | reagent/standard lots persisted | Custom | Forensic lot traceability | FS-RES-09 | OQ-REAGENT-LINK-01 |
| DS-RES-12 | Witness LBSPP (`RequireWitness`) | triggered by method-config `requires_witness=true`; enforces SoD | Custom | Critical-step control | FS-RES-10 | OQ-WITNESS-01 |

### 4.6 Parser Lifecycle CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PARSE-01 | Parser repo (`PARSER_REPO_URL`) | `git.caelum.local/quality-it/ctx-parsers` | Custom | Site source-of-truth | FS-PARSE-01 | IQ-PARSER-REPO-01 |
| DS-PARSE-02 | Parser metadata schema (`parser.yaml`) | schema_map, unit_test_paths, usp_1058_cat | Custom | USP-binding | FS-PARSE-01 | OQ-PARSER-META-01 |
| DS-PARSE-03 | Parser release workflow (`PARSER_RELEASE_WF`) | `ctx-parsers-release.yaml`; Author ≠ Approver gate + golden-file regression | Custom | Cat-5 release gate | FS-PARSE-02 | OQ-PARSER-RELEASE-01 |
| DS-PARSE-04 | Parser-version persistence | `parser_name + parser_version` stored on each result row | Custom | Reproducibility | FS-PARSE-03 | OQ-PARSER-VER-PERSIST-01 |
| DS-PARSE-05 | Raw-file retention store (`RAW_FILE_S3_URI`) | `s3://caelum-lims-raw/...` (Object Lock Compliance) | Custom | Immutable raw retention | FS-PARSE-03 | IQ-S3-OBJLOCK-01 |
| DS-PARSE-06 | Schema-change CI label (`PARSER_SCHEMA_LABEL`) | `schema-change` triggers impact-assessment job | Custom | Method-validation review | FS-PARSE-04 | OQ-PARSER-SCHEMA-CHANGE-01 |
| DS-PARSE-07 | Parser-error queue (`LW_PARSER_ERROR_Q`) | runtime errors persisted | Custom | Pause-on-error discipline | FS-PARSE-05 | OQ-PARSER-ERR-Q-01 |
| DS-PARSE-08 | Pause-on-error LBSPP (`OnParserErrorPauseSample`) | sets `sample.state = ERROR_HOLD` | Custom | Quality gate | FS-PARSE-05 | OQ-PARSER-PAUSE-01 |

### 4.7 OOS Workflow CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-OOS-01 | Phase-1 creation LBSPP (`OnOosCreatePhase1`) | calls eQMS `/api/v2/oos-cases`; idempotency `lims:result:<id>:oos`; ≤ 1 h | Custom | Regulatory cadence | FS-OOS-01 | OQ-OOS-PHASE1-CREATE-01 |
| DS-OOS-02 | Phase-1 form id (`CTX-OOS-PHASE1-FORM`) | per FDA OOS (2022) checklist | Custom | Regulator binding | FS-OOS-02 | OQ-OOS-PHASE1-FORM-01 |
| DS-OOS-03 | Phase-gate (`OOS_PHASE1_TO_PHASE2_GATE`) | requires QA e-sig on `phase1_conclusion` | Custom | Investigative discipline | FS-OOS-03 | OQ-OOS-PHASE-GATE-01 |
| DS-OOS-04 | Retest authorization table (`LW_OOS_RETEST`) | QA sig + justification ≥ 100 chars | Custom | Forensic retest | FS-OOS-04 | OQ-OOS-RETEST-01 |
| DS-OOS-05 | Assignable-cause enum (`OOS_ASSIGNABLE_CAUSE`) | `analyst_error, instrument_error, reagent_error, method_limitation, environmental` — `disagree_with_result` excluded | Custom | FDA OOS taxonomy | FS-OOS-05 | OQ-OOS-CAUSE-ENUM-01 |
| DS-OOS-06 | Investigator/Approver SoD (`LIMS-OOS-Investigator` ≠ `LIMS-OOS-Approver`) | exclusive AD groups + analyst-of-record retest-lockout | Custom | Independence | FS-OOS-06 | OQ-OOS-SOD-01 |
| DS-OOS-07 | OOT routing rule (`OOT_ROUTING`) | by `sample.type` → `stability-trending` OR `inprocess-trending` | Custom | Operational efficiency | FS-OOS-07 | OQ-OOT-ROUTING-01 |
| DS-OOS-08 | Annual OOS/OOT report (`CTX-RPT-OOS-ANNUAL`) | Tableau + LabWare Reports; FDA-OOS-2022 taxonomy | Custom | Trending evidence | FS-OOS-08 | PQ-OOS-ANNUAL-RPT-01 |

### 4.8 COA Generation CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COA-01 | COA generator (`CTX-COA-GEN-v3`) | PDF/A-3 output engine | Custom | Long-term-archive format | FS-COA-01 | OQ-COA-GEN-01 |
| DS-COA-02 | COA signature-page template (`COA_SIG_PAGE`) | per § 11.50 (name + ts + meaning); SHA-256 embedded as PDF metadata | Custom | Part 11 manifestation | FS-COA-02 | OQ-COA-SIGPAGE-01 |
| DS-COA-03 | Issuance gate LBSPP (`CanIssueCoa`) | every released test approved + no open deviations on batch | Custom | Release integrity | FS-COA-03 | OQ-COA-GATE-01 |
| DS-COA-04 | Template store (`CTX-COA-TEMPLATES`) | per-customer overrides allowed; CR-controlled | Custom | Layout discipline | FS-COA-04 | OQ-COA-TEMPLATE-01 |
| DS-COA-05 | COA versioning (`COA_VERSIONING`) | prior `SUPERSEDED`; signature provenance preserved | Custom | Audit-trail integrity | FS-COA-05 | OQ-COA-VERSIONING-01 |

### 4.9 Stability CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-STAB-01 | Pull-point auto-creation LBSPP (`OnPullPointArrivedCreateSample`) | LabWare Stability module + scheduler | Custom | Pull-point discipline | FS-STAB-01 | OQ-STAB-AUTO-01 |
| DS-STAB-02 | Missed-pull-point LBSPP (`CheckMissedPullPoints`) | daily cron; creates `STABILITY_MISSED_PULL` deviation | Custom | Audit-trail completeness | FS-STAB-02 | OQ-STAB-MISSED-01 |
| DS-STAB-03 | Stability trending engine (`CTX-STAB-TREND`) | ICH Q1E; significant-change flag | Custom | Investigation gate | FS-STAB-03 | OQ-STAB-TREND-01 |
| DS-STAB-04 | ICH-Q1E export id (`CTX-RPT-STAB-Q1E`) | PDF/A-3 output | Custom | Regulator export | FS-STAB-04 | OQ-STAB-Q1E-01 |
| DS-STAB-05 | Protocol-amendment CR field (`LW_STAB_PROTOCOL.cr_ref`) | mandatory link to MasterControl CR | Custom | Change-control binding | FS-STAB-05 | OQ-STAB-CR-LINK-01 |

### 4.10 Supplier CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-SUPP-01 | Supplier register table (`LW_SUPPLIER_REG`) | status, audit_cycle_ts, qualification_cert_urn | Custom | Site schema | FS-SUPP-01 | OQ-SUPP-REG-01 |
| DS-SUPP-02 | Receipt-block LBSPP (`BlockReceiptIfNotQualified`) | denies non-qualified receipt; Head-of-QA override + deviation | Custom | AVL discipline | FS-SUPP-02 | OQ-SUPP-BLOCK-01 |
| DS-SUPP-03 | Lot register table (`LW_LOT_REG`) | FK to `LW_SUPPLIER_REG`; spec auto-assignment rule | Custom | Spec-binding | FS-SUPP-03 | OQ-LOT-REG-01 |
| DS-SUPP-04 | Supplier-trend report (`CTX-RPT-SUPP-TREND`) | quarterly Tableau export | Custom | Quality KPI | FS-SUPP-04 | PQ-SUPP-TREND-01 |
| DS-SUPP-05 | Requalification alert cadence (`SUPP_REQUAL_ALERTS`) | `D-90, D-30, D-0` | Custom | Inbox cadence | FS-SUPP-05 | OQ-SUPP-ALERT-01 |

### 4.11 EM Integration CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EM-01 | EM bridge poll interval (`EM_POLL_SECONDS`) | `60` | Default | Vaisala viewLinc recommended | FS-EM-01 | OQ-EM-POLL-01 |
| DS-EM-02 | EM data table (`LW_EM_DATA`) | sensor_id, location, ts, value, qualified_status | Custom | Site schema | FS-EM-01 | OQ-EM-TABLE-01 |
| DS-EM-03 | Excursion linker LBSPP (`OnEmExcursionLinkBatches`) | queries `LW_BATCH` for In-Production; creates eQMS deviation; FK via `LW_DEVIATION_BATCH` | Custom | Batch impact discipline | FS-EM-02 | OQ-EM-LINK-01 |
| DS-EM-04 | EM trend report (`CTX-RPT-EM-APQR`) | feeds APQR generator | Custom | APR feed | FS-EM-03 | OQ-EM-TREND-01 |

### 4.12 Federation CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-FED-01 | Federation auth rules file (`CTX-FED-AUTH-RULES`) | methods authoritative Cambridge; suppliers authoritative Basel (EU) | Custom | Per-entity authority | FS-FED-01 | OQ-FED-RULES-01 |
| DS-FED-02 | Transfer LBSPP (`FederationTransfer`) | requires Federation-Steward e-sig; source audit copied | Custom | Inter-site integrity | FS-FED-02 | OQ-FED-XFER-01 |
| DS-FED-03 | Federation lag metric (`lims_federation_lag_seconds`) | Prometheus gauge; alert `wel-lims-fed > 600 s` | Custom | Observability | FS-FED-03 | OQ-FED-LAG-METRIC-01 |
| DS-FED-04 | Degraded-mode fallback (`FED_DEGRADED_MODE`) | local master-data read-only; last-known-good `LW_METHOD_REG` snapshot | Custom | Outage continuity | FS-FED-04 | OQ-FED-DEGRADED-01 |

### 4.13 Audit Trail CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUD-01 | Audit-trail coverage list (`AUDIT_TABLES`) | `LW_SAMPLE, LW_SPEC_HEADER, LW_METHOD_REG, LW_PARSER_REG, LW_RESULT, LW_LBSPP_RELEASE, LW_AUDIT_EVENT, LW_SIGNATURE, LW_CONFIG_BASELINE` | Custom | Comprehensive trail | FS-AUD-01 | OQ-AUDIT-COVERAGE-01 |
| DS-AUD-02 | DBA dual-control role (`oracle-dba-audit`) | separate role for audit-table ALTER; app role INSERT/SELECT only | Custom | Tamper-protection | FS-AUD-02 | OQ-AUDIT-DBA-DC-01 |
| DS-AUD-03 | Audit review templates | `CTX-RPT-LIMS-AUDIT-BATCH`, `CTX-RPT-LIMS-AUDIT-QUARTERLY` | Custom | Annex 11 § 9 | FS-AUD-03 | OQ-AUDIT-REPORT-01 |
| DS-AUD-04 | Audit retention (`AUDIT_RET_YEARS`) | `25`; partitioned by year; S3 Object Lock COMPLIANCE | Custom | EU GMP Ch. 4 | FS-AUD-04 | IQ-AUDIT-RET-01 |
| DS-AUD-05 | Focused-review tool (`CTX-AUD-FOCUSED-v2`) | filter to signatures/OOS/config/manual-override per shift/batch | Custom | Reviewer efficiency | FS-AUD-05 | OQ-AUDIT-FOCUSED-01 |
| DS-AUD-06 | Export manifest (`AUDIT_EXPORT_MANIFEST`) | CSV/PDF + SHA-256 manifest + "REVIEWED — <date>" watermark | Custom | Chain-of-custody export | FS-AUD-06 | OQ-AUDIT-EXPORT-01 |

### 4.14 21 CFR Part 11 / Annex 11 CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PART11-01 | Procedural-control SOP id (`CTX-SOP-CSV-01`) | linked from system docs | Custom | § 11.10(a) binding | FS-PART11-01 | OQ-SOP-LINK-01 |
| DS-PART11-02 | Export formats (`PART11_EXPORT_FORMATS`) | `PDF/A-3, CSV` | Custom | § 11.10(b) | FS-PART11-02 | OQ-INSPECTION-COPY-01 |
| DS-PART11-03 | Auth IdP (`AUTH_IDP`) | AD `caelum.local` + Keycloak MFA | Custom | § 11.10(d) | FS-PART11-03 | IQ-AUTH-IDP-01 |
| DS-PART11-04 | Admin break-glass account (`LW-DBA-Emergency`) | documented; audited monthly | Custom | Emergency continuity | FS-PART11-03 | OQ-BREAKGLASS-01 |
| DS-PART11-05 | E-sig manifestation fields (`SIG_FIELDS`) | `printedName + dateTime + meaning` | Default | § 11.50 | FS-PART11-04 | OQ-SIG-MANIFEST-01 |
| DS-PART11-06 | Signature binding (`SIG_BINDING`) | HMAC-SHA256 over result-record SHA-256 | Custom | § 11.70 | FS-PART11-05 | OQ-SIG-BINDING-01 |
| DS-PART11-07 | Account uniqueness (`ACCT_UNIQUE`) | AD↔HR mapping; reassignment blocked | Custom | § 11.100 | FS-PART11-06 | OQ-ACCT-UNIQUE-01 |
| DS-PART11-08 | Re-auth at signing (`SIG_REAUTH_MAX_AGE_S`) | `300` (5 min); cached creds rejected | Custom | § 11.200 | FS-PART11-07 | OQ-SIG-REAUTH-01 |
| DS-PART11-09 | Password policy (`PASSWORD_POLICY`) | length 14 + complexity + 90 d max-age | Custom | § 11.300 + site InfoSec | FS-PART11-08 | OQ-PWD-POLICY-01 |
| DS-PART11-10 | Validation evidence index (`CTX-VAL-EVID-INDEX`) | per Annex 11 § 4 | Custom | Documentation completeness | FS-ANX11-01 | OQ-VAL-EVID-IDX-01 |
| DS-PART11-11 | Accuracy-check LBSPP (`AccuracyChecks`) | range (0–200%), format, plausibility, delta-from-prior | Custom | Annex 11 § 6 | FS-ANX11-02 | OQ-ACCURACY-01 |

### 4.15 ISO 17025 CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ISO-01 | Tech-record template (`CTX-ISO17025-TECH-REC`) | uncertainty + repeatability captured | Custom | ISO 17025 § 7.5 | FS-ISO-01 | OQ-ISO-TECH-REC-01 |
| DS-ISO-02 | COA ISO-flagged content | lab name, customer/specimen ID, method, value+uncertainty, date | Custom | ISO 17025 § 7.8 | FS-ISO-02 | OQ-ISO-COA-01 |
| DS-ISO-03 | ISO retention extension (`ISO_RET_YEARS`) | `max(accreditation-cycle + 25 y, 25 y)` | Custom | Accreditation continuity | FS-ISO-03 | IQ-ISO-RET-01 |
| DS-ISO-04 | ISO-filtered view (`CTX-VIEW-ISO17025`) | filter to ISO-17025-flagged samples | Custom | Surveillance prep | FS-ISO-04 | OQ-ISO-VIEW-01 |

### 4.16 Integration-binding CIs (per-interface, see § 7 for design)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-INT-CFG-01 | PASX inbound endpoint (`PASX_IN_URL`) | `/api/lims/samples-from-pasx` | Custom | Site naming | FS-INT-PASX-01 | OQ-PASX-IN-01 |
| DS-INT-CFG-02 | PASX outbound endpoint (`PASX_OUT_URL`) | `https://pasx.caelum.local/api/v1/release-results` | Custom | Vendor binding | FS-INT-PASX-02 | OQ-PASX-OUT-01 |
| DS-INT-CFG-03 | PASX P95 latency budget (`PASX_OUT_P95_MS`) | `300000` (5 min) | Custom | FS-INT-PASX-02 SLA | FS-INT-PASX-02 | PQ-PASX-LAT-01 |
| DS-INT-CFG-04 | SAP middleware (`SAP_MW`) | `PI/PO LIMS_RELEASE_RESULT_v3`; idempotency `releaseId` | Custom | Vendor binding | FS-INT-SAP-01 | OQ-SAP-MW-01 |
| DS-INT-CFG-05 | eQMS deviation endpoint (`EQMS_DEV_URL`) | `https://eqms.caelum.local/api/v2` | Custom | Site DNS | FS-INT-EQMS-01 | OQ-EQMS-DEV-URL-01 |
| DS-INT-CFG-06 | CDS adapter pin file (`adapters.yaml`) | Empower 8.0.1 / Chromeleon 7.3.2 / Qtegra 2.10 | Custom | Version lock | FS-INT-CDS-01, FS-INT-CDS-02 | OQ-CDS-ADAPTER-PIN-01 |
| DS-INT-CFG-07 | AD/Keycloak realm (`KC_REALM`) | `caelum` realm; LDAPS + Kerberos + OIDC; groups `LIMS-*` | Custom | Site IdP | FS-INT-AD-01 | OQ-KC-REALM-01 |
| DS-INT-CFG-08 | viewLinc heartbeat (`EM_HEARTBEAT_S`) | `60` | Default | Vendor | FS-INT-EM-01 | OQ-EM-HEARTBEAT-01 |
| DS-INT-CFG-09 | Stability scheduler endpoint (`STAB_IN_URL`) | `/api/lims/stab-pullpoint` | Custom | Site naming | FS-INT-STAB-01 | OQ-STAB-IN-01 |

### 4.17 Custom-Script SDLC CIs (Cat-5 sub-components configuration metadata; design in § 8)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-DEV-01 | LBSPP signing key (`LBSPP_SIGNING_KEY`) | `caelum-sigstore-pubkey-2026q2` (Sigstore) | Custom | Supply-chain integrity | FS-DEV-01 | OQ-LBSPP-SIGN-01 |
| DS-DEV-02 | LBSPP Model Card requirement | per-LBSPP markdown sidecar w/ intent + risk + FS + OQ refs | Custom | Cat-5 design discipline | FS-DEV-02 | OQ-MODEL-CARD-01 |
| DS-DEV-03 | LBSPP release CI gate | passing regression + CR approval | Custom | Release control | FS-DEV-03 | OQ-LBSPP-RELEASE-GATE-01 |
| DS-DEV-04 | Static-analysis tools | LabWare-aware lint + Trivy dependency-scan; criticals ≤ 30 d | Custom | Vuln management | FS-DEV-04 | OQ-STATIC-ANALYSIS-01 |
| DS-DEV-05 | Release manifest (`release-vN-manifest.json`) | signed; SHA-256 per LBSPP | Custom | Release evidence | FS-DEV-05 | OQ-RELEASE-MANIFEST-01 |

### 4.18 Performance / Backup CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PERF-01 | Load-test plan (`CTX-LT-LIMS-300U-v1`) | 300 CU; nav P95 ≤ 2 s | Custom | URS-binding | FS-PERF-01 | PQ-LIMS-300U-01 |
| DS-PERF-02 | Bulk-import endpoint (`/api/lims/results/bulk`) | 10,000 records ≤ 10 min | Custom | URS-binding | FS-PERF-02 | PQ-LIMS-BULK-01 |
| DS-AV-01 | Availability dashboard (`wel-lims-availability`) | Grafana + SIEM | Custom | Observability | FS-AV-01 | OQ-AVAIL-DASH-01 |
| DS-BAK-01 | RMAN policy (`RMAN_POLICY`) | nightly + PITR; 25 y retention | Custom | Long-term archive | FS-BAK-01 | IQ-RMAN-01 |
| DS-BAK-02 | Restore-test cadence (`RESTORE_TEST_Q`) | quarterly + QA witness | Custom | Operational evidence | FS-BAK-02 | PQ-RMAN-RESTORE-01 |

### 4.19 Security CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-SEC-01 | Break-glass account (`LW-DBA-Emergency`) | documented; audited monthly | Custom | Emergency | FS-SEC-01 | OQ-BREAKGLASS-AUDIT-01 |
| DS-SEC-02 | HAProxy TLS floor (`HA_TLS_MIN`) | `ssl-min-ver TLSv1.2` | Custom | Site InfoSec | FS-SEC-02 | OQ-TLS-FLOOR-01 |
| DS-SEC-03 | Vuln-scan cadence (`VULN_SCAN`) | Trivy + Tenable weekly; criticals ≤ 30 d | Custom | Vuln management | FS-SEC-03 | OQ-VULN-SCAN-01 |
| DS-SEC-04 | Annual pen-test register (`CTX-SEC-FINDINGS`) | external assessor; findings tracked | Custom | Independent assurance | FS-SEC-04 | OQ-PENTEST-REG-01 |
| DS-SEC-05 | Vault path (`kv/lims/service-accounts/*`) | 90 d rotation | Custom | Secret hygiene | FS-SEC-05 | OQ-VAULT-ROTATE-01 |

### 4.20 Training / Periodic Review CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-TRN-01 | Cornerstone analyst curriculum (`CTX-CURR-LIMS-Analyst-v1`) | production-access gate | Custom | LMS binding | FS-TRN-01 | OQ-TRN-GATE-01 |
| DS-TRN-02 | Annual refresher (`CTX-CURR-LIMS-Refresher-2026`) | Reviewer + Approver | Custom | Currency maintenance | FS-TRN-02 | PQ-TRN-REFRESH-01 |
| DS-TRN-03 | Advanced DI curriculum (`CTX-CURR-DI-Advanced`) | Parser Authors + OOS Investigators | Custom | Critical-role training | FS-TRN-03 | OQ-DI-ADV-01 |
| DS-PR-01 | Annual periodic-review template (`CTX-PR-LIMS-YYYYMMDD`) | QC Informatics Lead + Head of QA sign-off | Custom | Annex 11 § 11 | FS-PR-01 | PQ-PR-LIMS-01 |

### 4.21 Cross-System Bindings (M-XSYS) — design

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-XSYS-AD-01 | Entra ID SAML / LDAPS binding | thick client = LDAPS; web client = SAML 2.0 via Entra ID; SCIM lifecycle | Custom | Per FS-XSYS-AD-01 | FS-XSYS-AD-01 | OQ-XSYS-AD-01 |
| DS-XSYS-AD-02 | Conditional-access policy id | `Lab-App Conditional Access (MFA + device-compliance)` | Custom | Policy reuse | FS-XSYS-AD-01 | OQ-CA-POLICY-01 |
| DS-XSYS-AD-03 | SIEM syslog target (`SIEM_INDEX`) | Splunk index `gxp-authn`; RFC 5424; ≤ 5 min lag | Custom | Cross-system correlation | FS-XSYS-AD-01 | OQ-SIEM-FWD-01 |
| DS-XSYS-AD-04 | CyberArk PAM binding (`PAM_RB`) | 24 h rotation + dual-witness check-out | Custom | Break-glass discipline | FS-XSYS-AD-01 | OQ-PAM-BREAKGLASS-01 |
| DS-XSYS-BAK-01 | Veeam VSS profile (`VEEAM_PROFILE`) | App-aware + Oracle RMAN; T1 tier; RPO ≤ 4 h / RTO ≤ 4 BH | Custom | Per FS-XSYS-BAK-01 | FS-XSYS-BAK-01 | OQ-VEEAM-01 |
| DS-XSYS-BAK-02 | S3 immutable copy (`S3_OBJLOCK_BUCKET`) | `s3://caelum-lims-immutable` Compliance mode; geo-replicated | Custom | Anti-ransom posture | FS-XSYS-BAK-01 | IQ-S3-OBJLOCK-02 |
| DS-XSYS-BAK-03 | LTO-9 air-gap rotation cadence | monthly | Custom | Air-gap policy | FS-XSYS-BAK-01 | OQ-LTO9-01 |
| DS-XSYS-BAK-04 | Restore-cert retention | ≥ 25 y in eQMS | Custom | Quality-record discipline | FS-XSYS-BAK-01 | OQ-RESTORE-CERT-01 |
| DS-XINT-HEL-01 | Helios Kafka topic (`HELIOS_TOPIC`) | `helios.ingest.caelum.labware.v1`; idempotency `{source_system, event_id}` | Custom | Per FS-XINT-HEL-01 | FS-XINT-HEL-01 | OQ-HELIOS-PUB-01 |
| DS-XINT-HEL-02 | Helios lag alert (`HELIOS_LAG_ALERT_S`) | `600`; Prometheus `helios_publish_lag_seconds` | Custom | Back-pressure SLO | FS-XINT-HEL-01 | OQ-HELIOS-LAG-01 |
| DS-XINT-HEL-03 | Helios reconciliation cadence | daily 24 h window; mismatch > 0.01% raises eQMS deviation | Custom | Parity verification | FS-XINT-HEL-02 | OQ-HELIOS-RECON-01 |

---

## 5. Workflow + Business-Rule Design

### 5.1 LabWare Workflow `CTX-SLW-001` — Sample Lifecycle

State sequence (FS-SAMPLE-03):

1. `LOGGED` — created via API or UI. Required fields enforced at INSERT by MASTER_TEMPLATE `CTX-MT-SAMPLE-V1`.
2. `RECEIVED` — physical receipt acknowledged. Storage-log row written.
3. `IN-STORAGE` — placed at storage location; `LW_STORAGE_LOG` updated.
4. `SCHEDULED` — assigned to test queue per method + spec.
5. `IN-TEST` — analyst checked-out via `ChainOfCustodyMove`.
6. `RESULTS-ENTERED` — LBSPP `PromoteStageToResult` invoked from CDS staging or manual dual-keyboard entry.
7. `REVIEWED` — AD-group `LIMS-Reviewer` member signs; SoD against analyst-of-record enforced.
8. `APPROVED` — AD-group `LIMS-Approver` member signs; e-sig payload SHA-256-bound.
9. `RELEASED` — COA generation gate (`CanIssueCoa`) passes; result pushed to PAS-X / SAP.

Reverse transitions write to `LW_AUDIT_STATE_REVERSAL` with `reason` ≥ 30 chars + signature.

### 5.2 LabWare Workflow — OOS Phase I → Phase II

| Step | Actor | Gate | Action |
|---|---|---|---|
| 1 | LBSPP `OnOosCreatePhase1` | within 1 h of OOS flag | calls eQMS `POST /api/v2/oos-cases`; idempotency `lims:result:<id>:oos` |
| 2 | OOS Investigator | role `LIMS-OOS-Investigator` | completes Phase-1 form `CTX-OOS-PHASE1-FORM` |
| 3 | QA reviewer | re-auth + e-sig on `phase1_conclusion` | gate to Phase II |
| 4 | OOS Approver | role `LIMS-OOS-Approver` (≠ Investigator) | authorises retest via `LW_OOS_RETEST` |
| 5 | Analyst | locked-out until cause review resolved | retest run in new sample |
| 6 | Investigator | assignable-cause enum value selected | mandatory at invalidation |

### 5.3 Method-state-change workflow

| Step | Actor | Gate |
|---|---|---|
| 1 | Method Author (`LIMS-Method-Author`) | drafts method + validation evidence URN |
| 2 | Method Reviewer | content review |
| 3 | Method Approver (`LIMS-Method-Approver` ≠ Author) | re-auth e-sig on `DRAFT→APPROVED` |
| 4 | DB trigger `tr_method_effective_immutable` | blocks UPDATE/DELETE when EFFECTIVE |

### 5.4 Parser-release workflow (Cat-5 sub-component)

| Step | Actor | CI gate |
|---|---|---|
| 1 | Parser Author | commit + PR labelled `schema-change` triggers impact-assessment job |
| 2 | Parser Reviewer | code review (≥ 1 reviewer) |
| 3 | Parser Approver (≠ Author) | e-sig in `ctx-parsers-release.yaml` |
| 4 | CI | regression suite against `golden-files/` corpus |
| 5 | Release manifest | `release-vN-manifest.json` signed (Sigstore) |
| 6 | Deploy | GitHub Actions → PRODUCTION |

### 5.5 EM-excursion linkage business rule

When `LW_EM_DATA` writes a row with `value > excursion_threshold`, `OnEmExcursionLinkBatches` queries `LW_BATCH` for batches `state IN ('IN-TEST', 'IN-PRODUCTION')` at the excursion timestamp window. For each matching batch, an eQMS deviation is created via `POST /api/v2/deviations` (category `EM_EXCURSION`) and a row is written to `LW_DEVIATION_BATCH`. Failure to push results in `EM_EXCURSION_QUEUE_FAIL` alert and queues the event for retry (max 24 h).

### 5.6 COA issuance business rule

`CanIssueCoa(batch_id)` returns `true` iff:
- every released test on the batch is in state `APPROVED` (FS-COA-03), AND
- no open deviation exists on the batch (`LW_DEVIATION` where `batch_id = ?` AND `state != 'CLOSED'`), AND
- the assigned spec was EFFECTIVE at sample-receipt date (FS-SPEC-06 passes).

Failure returns a structured error to the COA-generation UI; the gate is OQ-tested via OQ-COA-GATE-01.

---

## 6. Role-Permission Matrix Design

| Role (AD group) | Sample-Create | Sample-Hold | Method-Create | Method-Approve | Spec-Create | Spec-Approve | Result-Enter | Result-Review | Result-Approve | OOS-Investigate | OOS-Approve | Parser-Author | Parser-Approve | COA-Issue | Federation-Transfer | Audit-Trail-Review | DBA |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `LIMS-Analyst` | R/W | – | – | – | – | – | R/W | – | – | – | – | – | – | – | – | – | – |
| `QC-Manager` | R/W | R/W | – | – | – | – | R/W | – | – | – | – | – | – | – | – | – | – |
| `QA-Manager` | R | R/W | – | – | – | – | – | – | – | R | R/W | – | – | – | – | R | – |
| `LIMS-Method-Author` | – | – | R/W | – | – | – | – | – | – | – | – | – | – | – | – | – | – |
| `LIMS-Method-Approver` | – | – | R | R/W | – | – | – | – | – | – | – | – | – | – | – | – | – |
| `LIMS-Spec-Author` | – | – | – | – | R/W | – | – | – | – | – | – | – | – | – | – | – | – |
| `LIMS-Spec-Approver` | – | – | – | – | R | R/W | – | – | – | – | – | – | – | – | – | – | – |
| `LIMS-Reviewer` | – | – | – | – | – | – | – | R/W | – | – | – | – | – | – | – | – | – |
| `LIMS-Approver` | – | – | – | – | – | – | – | – | R/W | – | – | – | – | R/W | – | – | – |
| `LIMS-OOS-Investigator` | – | – | – | – | – | – | – | – | – | R/W | – | – | – | – | – | – | – |
| `LIMS-OOS-Approver` | – | – | – | – | – | – | – | – | – | R | R/W | – | – | – | – | – | – |
| `Parser-Author` | – | – | – | – | – | – | – | – | – | – | – | R/W | – | – | – | – | – |
| `Parser-Approver` | – | – | – | – | – | – | – | – | – | – | – | R | R/W | – | – | – | – |
| `Federation-Steward` | – | – | – | – | – | – | – | – | – | – | – | – | – | – | R/W | – | – |
| `Audit-Reviewer` | – | – | – | – | – | – | – | – | – | – | – | – | – | – | – | R/W | – |
| `oracle-dba-audit` | – | – | – | – | – | – | – | – | – | – | – | – | – | – | – | – | DBA on audit tables only |
| `LW-DBA-Emergency` | – | – | – | – | – | – | – | – | – | – | – | – | – | – | – | – | break-glass; monthly audit |

SoD constraints enforced at signing time:
- `analyst_id ≠ reviewer_id ≠ approver_id` for any result record
- `LIMS-Method-Author ∩ LIMS-Method-Approver = ∅` per AD-group membership
- `LIMS-OOS-Investigator ∩ LIMS-OOS-Approver = ∅`
- `Parser-Author ∩ Parser-Approver = ∅`

---

## 7. Integration Design

### 7.1 PAS-X — Sample-create inbound (FS-INT-PASX-01)

- Endpoint: `POST https://lims.caelum.local/api/lims/samples-from-pasx`
- Transport: HTTPS + mTLS; client cert from PAS-X site PKI
- Payload: JSON; `pasx_order_id`, `product_code`, `batch_id`, `sample_seq`, `sampling_point`, `sampling_user_id`, `sampling_ts`
- Idempotency: header `Idempotency-Key: pasx:order:<id>:sample:<seq>`
- Retry: PAS-X performs exponential back-off; site retains idempotency for 7 d
- Error handling: HTTP 4xx → no retry; HTTP 5xx → PAS-X retries; LIMS logs correlation ID
- Monitoring: Prometheus `pasx_in_request_count`, `pasx_in_error_count`

### 7.2 PAS-X — Release-results outbound (FS-INT-PASX-02)

- Endpoint: `POST https://pasx.caelum.local/api/v1/release-results`
- Transport: HTTPS + mTLS
- Latency SLA: P95 ≤ 5 min; Prometheus `lims_pasx_release_lat_p95_seconds` alerts on 95th-percentile breach
- Idempotency: per-batch correlation ID

### 7.3 SAP — Release outbound (FS-INT-SAP-01)

- Middleware: SAP PI/PO interface `LIMS_RELEASE_RESULT_v3`
- Idempotency: `releaseId` (LBSPP-generated)
- Error: PI/PO dead-letter queue; site monitors `sap_dlq_depth`

### 7.4 eQMS — Deviation + OOS outbound (FS-INT-EQMS-01, FS-OOS-01)

- Endpoints:
  - `POST https://eqms.caelum.local/api/v2/deviations` (idempotency `lims:result:<id>`)
  - `POST https://eqms.caelum.local/api/v2/oos-cases` (idempotency `lims:result:<id>:oos`)
- Failure handling: HTTP 4xx → block result approval (returns 403 to LIMS UI)
- Monitoring: Prometheus `eqms_dev_create_count`, `eqms_oos_create_count`

### 7.5 CDS adapters — inbound (FS-INT-CDS-01, FS-INT-CDS-02)

- Empower-LIMS Connector v8.0.1 — Waters Empower
- Chromeleon Sample-List v7.3.2 — Thermo Chromeleon
- Qtegra LIMS Connector v2.10 — Thermo Qtegra
- All adapter versions pinned in `ctx-lims-basic/adapters.yaml`; upgrades change-controlled
- Raw-file passed by hash + S3 path; LIMS does not modify CDS-side records

### 7.6 AD via Keycloak (FS-INT-AD-01)

- Realm: `caelum`
- Protocols: LDAPS (thick client) + Kerberos (legacy) + OIDC (web client)
- MFA: enforced at every signature event (TOTP / WebAuthn)
- Service accounts in HashiCorp Vault `kv/lims/service-accounts/*`; 90 d rotation

### 7.7 Vaisala viewLinc (FS-INT-EM-01)

- Site-developed `ctx-em-bridge` polls REST API every 60 s
- Lag metric `em_bridge_lag_seconds`; alert at 300 s
- Heartbeat to `LW_EM_HEARTBEAT` table

### 7.8 Stability scheduler (FS-INT-STAB-01)

- Endpoint: `POST /api/lims/stab-pullpoint`
- Triggers auto-creation of sample login task via `OnPullPointArrivedCreateSample`

### 7.9 LabWare Federation 8 — Cambridge ↔ Basel (FS-FED-01..04)

- Mode: transactional log shipping + master-data replication
- Authority: methods Cambridge → Basel; suppliers (EU) Basel → Cambridge
- Lag SLA: 600 s alert
- Outage handling: degraded-mode fallback to last-known-good `LW_METHOD_REG` snapshot

### 7.10 Helios audit-event handover (FS-XINT-HEL-01, FS-XINT-HEL-02)

- Kafka topic: `helios.ingest.caelum.labware.v1`
- Schema-registry pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`
- Delivery: at-least-once; idempotency key `{source_system, event_id}`
- Reconciliation: daily; mismatch > 0.01% in 24 h raises eQMS deviation

---

## 8. Site-Deployed Components Design (mini-SDS — Cat-5 sub-components)

Three site-developed components escalate the system to a hybrid Cat 4 + Cat 5; each carries a mini-SDS sub-section here.

### 8.1 `ctx-lims-basic` — LIMS Basic scripts

| Aspect | Design |
|---|---|
| Repo | `git.caelum.local/quality-it/ctx-lims-basic` |
| Language | LabWare LIMS Basic |
| Modules | `HoldOrQuarantineSample`, `ChainOfCustodyMove`, `CalcShelfLife`, `EvalAgainstSpec`, `OnOosCreatePhase1`, `OnOosCreateDeviation`, `PromoteStageToResult`, `EnterDataDualKeyboard`, `RequireWitness`, `OnPullPointArrivedCreateSample`, `CheckMissedPullPoints`, `BlockReceiptIfNotQualified`, `FederationTransfer`, `OnEmExcursionLinkBatches`, `AccuracyChecks`, `CheckSpecEffective`, `CheckSpecEffectiveDateConflict`, `CanIssueCoa` |
| Interface | Invoked via LabWare workflow gates + DB triggers + UI buttons |
| Dependencies | LabWare LIMS 8.0.4 SDK; Oracle 19c; eQMS REST API |
| GxP-criticality | inherited from FS-IDs (mostly R1: SoD, signature, OOS, COA gating) |
| Owner | Caelum Quality IT — Custom Apps team |
| SDLC | signed commits (Sigstore) + CI lint + unit + integration tests against test LabWare; release per FS-DEV-03 |

### 8.2 `ctx-parsers` — Parser Lifecycle Manager

| Aspect | Design |
|---|---|
| Repo | `git.caelum.local/quality-it/ctx-parsers` |
| Language | Python 3.11 (sandboxed runtime invoked by LabWare) |
| Modules | per-instrument parser modules + `parser.yaml` schema map + golden-files corpus |
| Interface | invoked from `PromoteStageToResult` LBSPP with raw-data pointer; returns structured result rows |
| Dependencies | pandas (pinned); numpy (pinned); `chromeleon-export-reader`, `empower-export-reader`, `qtegra-export-reader` per-vendor libraries (pinned in `requirements.txt`) |
| GxP-criticality | R1 (instrument-data integrity) |
| Owner | Caelum Quality IT — Custom Apps team |
| SDLC | per FS-PARSE-02; release deploys gated on Author ≠ Approver + golden-file regression |
| Determinism | each release deterministic against the golden-files corpus; parser-version persisted on every result row (FS-PARSE-03) |

### 8.3 `ctx-em-bridge` — Vaisala viewLinc adapter

| Aspect | Design |
|---|---|
| Repo | `git.caelum.local/quality-it/ctx-em-bridge` |
| Language | Python 3.11 |
| Modules | `viewlinc_poller`, `em_writer`, `heartbeat_emitter`, `excursion_classifier` |
| Interface | inbound REST poll to viewLinc API (60 s); outbound INSERT into `LW_EM_DATA`; emits heartbeat to Prometheus pushgateway |
| Dependencies | requests (pinned); viewLinc API spec v3 (pinned) |
| GxP-criticality | R1 (EM data integrity for batch-impact analysis) |
| Owner | Caelum Quality IT — Custom Apps team |
| SDLC | same gates as `ctx-lims-basic` (signed commits + CI + CR-controlled release) |

---

## 9. References

### US
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .22, .68, .180, .192
- FDA *Guidance for Industry: Investigating Out-of-Specification (OOS) Test Results* (October 2022)
- USP <1058> *Analytical Instrument Qualification*

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EMA *Reflection Paper on Computerised Systems* (current edition)
- EU GMP Chapter 4 (Documentation)

### DACH
- BfArM (DE) — supervisory authority binding (informational reference)
- Swissmedic (CH) — multi-site federation peer (Basel)

### International
- ICH Q2(R2), Q9(R1), Q10, Q12, Q1A(R2), Q1E
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE GAMP GPG *Validation of Laboratory Computerized Systems*
- PIC/S PI 041
- ISO/IEC 17025:2017
- ISO/IEC 27001:2022; ISO/IEC 27002

### Vendor
- LabWare — *LIMS 8.0 Installation, Configuration, and Administration Reference*
- LabWare — *LIMS Basic Programming Reference*
- LabWare — *Federation 8 Administrator Guide*
- Waters — *Empower-LIMS Connector Configuration Guide* (Empower 8.0.1)
- Thermo Fisher — *Chromeleon Sample-List Integration Guide* (Chromeleon 7.3.2)
- Thermo Fisher — *Qtegra LIMS Connector Reference* (Qtegra 2.10)
- Vaisala — *viewLinc 5.x API Reference*
- Oracle — *Oracle Database 19c Data Guard Concepts and Administration*

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-PLAT-01 | FS-PLAT-01 |
| DS-PLAT-02 | FS-PLAT-01 |
| DS-PLAT-03 | FS-PLAT-01 |
| DS-PLAT-04 | FS-PLAT-02 |
| DS-PLAT-05 | FS-PLAT-02 |
| DS-PLAT-06 | FS-PLAT-02 |
| DS-PLAT-07 | FS-PLAT-03 |
| DS-PLAT-08 | FS-PLAT-03 |
| DS-PLAT-09 | FS-PLAT-04 |
| DS-PLAT-10 | FS-PLAT-04 |
| DS-PLAT-11 | FS-PLAT-05 |
| DS-SAMPLE-01 | FS-SAMPLE-01 |
| DS-SAMPLE-02 | FS-SAMPLE-02 |
| DS-SAMPLE-03 | FS-SAMPLE-02 |
| DS-SAMPLE-04 | FS-SAMPLE-03 |
| DS-SAMPLE-05 | FS-SAMPLE-03 |
| DS-SAMPLE-06 | FS-SAMPLE-03 |
| DS-SAMPLE-07 | FS-SAMPLE-04 |
| DS-SAMPLE-08 | FS-SAMPLE-05 |
| DS-SAMPLE-09 | FS-SAMPLE-06 |
| DS-SAMPLE-10 | FS-SAMPLE-06 |
| DS-SAMPLE-11 | FS-SAMPLE-07 |
| DS-SAMPLE-12 | FS-SAMPLE-07 |
| DS-SAMPLE-13 | FS-SAMPLE-08 |
| DS-SAMPLE-14 | FS-SAMPLE-09 |
| DS-SAMPLE-15 | FS-SAMPLE-09 |
| DS-SAMPLE-16 | FS-SAMPLE-10 |
| DS-METH-01 | FS-METH-01 |
| DS-METH-02 | FS-METH-02 |
| DS-METH-03 | FS-METH-02 |
| DS-METH-04 | FS-METH-02 |
| DS-METH-05 | FS-METH-03 |
| DS-METH-06 | FS-METH-04 |
| DS-METH-07 | FS-METH-05 |
| DS-METH-08 | FS-METH-06 |
| DS-METH-09 | FS-METH-07 |
| DS-SPEC-01 | FS-SPEC-01 |
| DS-SPEC-02 | FS-SPEC-02 |
| DS-SPEC-03 | FS-SPEC-03 |
| DS-SPEC-04 | FS-SPEC-04 |
| DS-SPEC-05 | FS-SPEC-05 |
| DS-SPEC-06 | FS-SPEC-05 |
| DS-SPEC-07 | FS-SPEC-06 |
| DS-RES-01 | FS-RES-01 |
| DS-RES-02 | FS-RES-01 |
| DS-RES-03 | FS-RES-02 |
| DS-RES-04 | FS-RES-02 |
| DS-RES-05 | FS-RES-03 |
| DS-RES-06 | FS-RES-04 |
| DS-RES-07 | FS-RES-05 |
| DS-RES-08 | FS-RES-06 |
| DS-RES-09 | FS-RES-07 |
| DS-RES-10 | FS-RES-08 |
| DS-RES-11 | FS-RES-09 |
| DS-RES-12 | FS-RES-10 |
| DS-PARSE-01 | FS-PARSE-01 |
| DS-PARSE-02 | FS-PARSE-01 |
| DS-PARSE-03 | FS-PARSE-02 |
| DS-PARSE-04 | FS-PARSE-03 |
| DS-PARSE-05 | FS-PARSE-03 |
| DS-PARSE-06 | FS-PARSE-04 |
| DS-PARSE-07 | FS-PARSE-05 |
| DS-PARSE-08 | FS-PARSE-05 |
| DS-OOS-01 | FS-OOS-01 |
| DS-OOS-02 | FS-OOS-02 |
| DS-OOS-03 | FS-OOS-03 |
| DS-OOS-04 | FS-OOS-04 |
| DS-OOS-05 | FS-OOS-05 |
| DS-OOS-06 | FS-OOS-06 |
| DS-OOS-07 | FS-OOS-07 |
| DS-OOS-08 | FS-OOS-08 |
| DS-COA-01 | FS-COA-01 |
| DS-COA-02 | FS-COA-02 |
| DS-COA-03 | FS-COA-03 |
| DS-COA-04 | FS-COA-04 |
| DS-COA-05 | FS-COA-05 |
| DS-STAB-01 | FS-STAB-01 |
| DS-STAB-02 | FS-STAB-02 |
| DS-STAB-03 | FS-STAB-03 |
| DS-STAB-04 | FS-STAB-04 |
| DS-STAB-05 | FS-STAB-05 |
| DS-SUPP-01 | FS-SUPP-01 |
| DS-SUPP-02 | FS-SUPP-02 |
| DS-SUPP-03 | FS-SUPP-03 |
| DS-SUPP-04 | FS-SUPP-04 |
| DS-SUPP-05 | FS-SUPP-05 |
| DS-EM-01 | FS-EM-01 |
| DS-EM-02 | FS-EM-01 |
| DS-EM-03 | FS-EM-02 |
| DS-EM-04 | FS-EM-03 |
| DS-FED-01 | FS-FED-01 |
| DS-FED-02 | FS-FED-02 |
| DS-FED-03 | FS-FED-03 |
| DS-FED-04 | FS-FED-04 |
| DS-AUD-01 | FS-AUD-01 |
| DS-AUD-02 | FS-AUD-02 |
| DS-AUD-03 | FS-AUD-03 |
| DS-AUD-04 | FS-AUD-04 |
| DS-AUD-05 | FS-AUD-05 |
| DS-AUD-06 | FS-AUD-06 |
| DS-PART11-01 | FS-PART11-01 |
| DS-PART11-02 | FS-PART11-02 |
| DS-PART11-03 | FS-PART11-03 |
| DS-PART11-04 | FS-PART11-03 |
| DS-PART11-05 | FS-PART11-04 |
| DS-PART11-06 | FS-PART11-05 |
| DS-PART11-07 | FS-PART11-06 |
| DS-PART11-08 | FS-PART11-07 |
| DS-PART11-09 | FS-PART11-08 |
| DS-PART11-10 | FS-ANX11-01 |
| DS-PART11-11 | FS-ANX11-02 |
| DS-ISO-01 | FS-ISO-01 |
| DS-ISO-02 | FS-ISO-02 |
| DS-ISO-03 | FS-ISO-03 |
| DS-ISO-04 | FS-ISO-04 |
| DS-INT-CFG-01 | FS-INT-PASX-01 |
| DS-INT-CFG-02 | FS-INT-PASX-02 |
| DS-INT-CFG-03 | FS-INT-PASX-02 |
| DS-INT-CFG-04 | FS-INT-SAP-01 |
| DS-INT-CFG-05 | FS-INT-EQMS-01 |
| DS-INT-CFG-06 | FS-INT-CDS-01 |
| DS-INT-CFG-07 | FS-INT-AD-01 |
| DS-INT-CFG-08 | FS-INT-EM-01 |
| DS-INT-CFG-09 | FS-INT-STAB-01 |
| DS-DEV-01 | FS-DEV-01 |
| DS-DEV-02 | FS-DEV-02 |
| DS-DEV-03 | FS-DEV-03 |
| DS-DEV-04 | FS-DEV-04 |
| DS-DEV-05 | FS-DEV-05 |
| DS-PERF-01 | FS-PERF-01 |
| DS-PERF-02 | FS-PERF-02 |
| DS-AV-01 | FS-AV-01 |
| DS-BAK-01 | FS-BAK-01 |
| DS-BAK-02 | FS-BAK-02 |
| DS-SEC-01 | FS-SEC-01 |
| DS-SEC-02 | FS-SEC-02 |
| DS-SEC-03 | FS-SEC-03 |
| DS-SEC-04 | FS-SEC-04 |
| DS-SEC-05 | FS-SEC-05 |
| DS-TRN-01 | FS-TRN-01 |
| DS-TRN-02 | FS-TRN-02 |
| DS-TRN-03 | FS-TRN-03 |
| DS-PR-01 | FS-PR-01 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 |
| DS-XSYS-AD-02 | FS-XSYS-AD-01 |
| DS-XSYS-AD-03 | FS-XSYS-AD-01 |
| DS-XSYS-AD-04 | FS-XSYS-AD-01 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| DS-XSYS-BAK-02 | FS-XSYS-BAK-01 |
| DS-XSYS-BAK-03 | FS-XSYS-BAK-01 |
| DS-XSYS-BAK-04 | FS-XSYS-BAK-01 |
| DS-XINT-HEL-01 | FS-XINT-HEL-01 |
| DS-XINT-HEL-02 | FS-XINT-HEL-01 |
| DS-XINT-HEL-03 | FS-XINT-HEL-02 |

---

## 11. Design-level Risk Register

| ID | Design-level risk | Origin (DS-ID / design choice) | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|---|
| DR-01 | Federation lag spike during heavy CDS bulk import starves the Basel passive secondary | DS-FED-03 + DS-PERF-02 | Medium | Medium | OQ-FED-LAG-METRIC-01 + degraded-mode runbook (DS-FED-04) |
| DR-02 | LIMS Basic release silently regresses a calculation when LabWare 8.0.4 → 8.0.5 lands a vendor patch that changes API behaviour | DS-RES-04 + DS-DEV-03 | Low | High | Regression suite OQ-LBSPP-RELEASE-01 + vendor-release runbook |
| DR-03 | Parser deployment re-processes historical results in place, breaking immutability | DS-PARSE-04 + DS-PARSE-05 | Low | Critical | Raw-file retained in S3 Object Lock (DS-PARSE-05); never re-process in place |
| DR-04 | Oracle Data Guard async-mode loses ≤ 15 min of writes at DR failover | DS-PLAT-03 + DS-PLAT-04 | Low | High | RPO 15-min documented; DR runbook OQ-DG-LAG-01 |
| DR-05 | CDS adapter version skew when Empower 8.0.1 → 8.1 lands without site pinning | DS-INT-CFG-06 | Medium | Medium | `adapters.yaml` pin + CR-controlled upgrades |
| DR-06 | DST quarter-patch causes timestamp drift > NTP tolerance | DS-EM-01 + DS-FED-03 | Low | Medium | Quarterly DST validation |
| DR-07 | OOS workflow misroute — Phase I → Phase II without QA `phase1_conclusion` signature | DS-OOS-03 + DS-RES-08 | Low | Critical | DB trigger gate; OQ-OOS-PHASE-GATE-01 |
| DR-08 | COA re-issuance drops the prior signature page provenance chain | DS-COA-05 | Low | High | Versioning OQ-COA-VERSIONING-01; audit-trail preserved |
| DR-09 | `LIMS-Method-Author` / `LIMS-Method-Approver` AD-group overlap defeats SoD | DS-METH-06 + DS-RES-08 | Low | Critical | Quarterly RBAC review (DS-SEC-02 vector) |
| DR-10 | Federation degraded-mode last-known-good snapshot is stale (> 24 h) | DS-FED-04 | Low | High | Snapshot freshness alert + runbook escalation |
| DR-11 | RHEL 9.2 kernel CVE forces an out-of-band patch outside the 30-day SLA window | DS-PLAT-07 + DS-SEC-03 | Medium | High | Emergency CR pathway + scheduled rolling-restart (DS-PLAT-11) |
| DR-12 | `ctx-em-bridge` poller stalls and `LW_EM_DATA` rows go silently missing | DS-EM-01 + DS-EM-02 | Low | High | Heartbeat to Prometheus; alert at 300 s lag |
| DR-13 | S3 Object Lock COMPLIANCE-mode parser raw-file legal-hold blocks vendor-required deletion | DS-PARSE-05 + DS-AUD-04 | Low | Medium | Legal-hold-policy reviewed at retention-policy CR |
| DR-14 | Keycloak token re-auth max-age 5 min creates UX friction that drives users to bypass MFA via cached creds | DS-PART11-08 | Low | High | UX monitoring + lockout policy (DS-PART11-09) |
| DR-15 | Sigstore key rotation breaks LBSPP release-manifest verification at deploy time | DS-DEV-01 + DS-DEV-05 | Low | Medium | Rotation runbook; CI key-pin update CR |
| DR-16 | viewLinc API v3 → v4 vendor change breaks `ctx-em-bridge` adapter contract | DS-EM-01 + DS-INT-CFG-08 | Medium | Medium | Vendor-release runbook FS-VND-02 + adapter version pin |
| DR-17 | Helios Kafka schema-registry pinning drift between LIMS publisher and Helios consumer | DS-XINT-HEL-01 + DS-XINT-HEL-03 | Low | High | Schema-registry contract test in CI; reconciliation deviation gate |
| DR-18 | Basel federation peer endpoint TLS-certificate renewal lapses | DS-FED-01 + DS-XSYS-AD-01 | Low | High | cert-manager monitoring + renewal runbook |

The full formal Risk Assessment is `CTX-RA-LIMS-001` (synthetic, separate document).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
