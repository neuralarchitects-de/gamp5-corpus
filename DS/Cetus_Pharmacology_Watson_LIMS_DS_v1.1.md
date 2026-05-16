---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring 2026-05-15 (Chunk A Watson LIMS)"
seed_corpus_basis:
  - "CET-FS-WATSON-001 v1.1 (parent FS)"
  - "CET-URS-WATSON-001 v1.1 (transitive parent URS)"
  - "GAMP 5 (2nd Edition) Category 4 — Configuration Specification (enterprise LIMS)"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "21 CFR Part 58 (GLP) §§ .29, .33, .35, .81, .120, .130, .185, .190, .195"
  - "ICH M10 (2022); OECD GLP; ICH E6(R3) GCP"
  - "BfR GLP-Bundesstelle + Länder (DE); Swissmedic (CH); AGES (AT)"
  - "Thermo Fisher — Watson LIMS 7.6 Configuration Reference (vendor doc)"
  - "Thermo Fisher — Watson LIMS 7.6 System Administrator's Guide"
parent_fs:
  document_number: CET-FS-WATSON-001
  version: 1.1
  file: ../../../FS_FDS/_generated/final/Cetus_Pharmacology_Watson_LIMS_FS_v1.3.md
parent_urs:
  document_number: CET-URS-WATSON-001
  version: 1.1
  file: ../../../URS/_generated/final/Watson_LIMS_Bioanalytical__Cetus_Pharmacology_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Bioanalytical LIMS — Thermo Fisher Watson LIMS 7.6 (Regulated Bioanalysis)

**Document Number:** CET-DS-WATSON-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** CET-FS-WATSON-001 v1.1 | **Parent URS:** CET-URS-WATSON-001 v1.1 *(informational, transitive)*
**Site:** Cetus Pharmacology GmbH, Bioanalytical Services, Heidelberg, Germany *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Thermo Fisher Watson LIMS 7.6 (Regulated Bioanalysis)** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Part 58 (GLP) §§ .29, .33, .35, .81, .120, .130, .185, .190, .195; FDA Bioanalytical Method Validation (2018); EMA Bioanalytical (2011); ICH M10 (2022); ICH E6(R3) GCP (Step 4, 2025); OECD GLP; BfR GLP-Bundesstelle + Länder (DE); BfArM (DE medicines/devices, not GLP); Swissmedic (CH); AGES (AT); ISPE GAMP 5 (2nd Ed., 2022)

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Bioanalytical Operations) | _____________ | _____________ | _____ |
| Reviewer (Study Director — GLP per § 58.33) | _____________ | _____________ | _____ |
| Reviewer (Principal Investigator) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (QAU — § 58.35) | _____________ | _____________ | _____ |
| Approver (VP DMPK / Process Owner) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T3 from parent URS+FS pair (enterprise LIMS scope). DS covers 110/115 FS-IDs; 5 FS-IDs flagged as vendor-internal — no site design surface (FS-AUD-01 Watson audit-trail engine internals, FS-LBA-02 Watson 4PL/5PL curve-fit engine internals, FS-RUN-02 Watson ICH M10 run-acceptance engine internals, FS-ISR-01 deterministic-seeded-random ISR sampler engine internals, FS-LBA-05 Watson hook-effect detector internals). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from `CET-FS-WATSON-001` and `CET-URS-WATSON-001`. DS-specific terms:

| Term | Definition |
|---|---|
| Authority Role | Watson LIMS internal name for an Okta-bound role bundle |
| Plate-Map | Watson DB representation of a plate with per-well typing (sample / cal / QC / blank) |
| Run-Acceptance Engine | Watson internal module enforcing ICH M10 §§ 3.3.2 / 4.3.2 thresholds |
| Inspection Tenant | Watson read-only tenant produced on demand for regulator inspections |
| `wel-watson` | Splunk heavy-index name reserved for this system's events |
| Helios | Site-wide audit-trail-review workbench (`HBS-URS-ATR-001`) |
| Lyrae | Site-wide AI/ML Model Server (`LYR-URS-MLSRV-001`) |

## 1. Purpose

This Configuration Specification records the design that satisfies `CET-FS-WATSON-001` v1.1 — the Watson LIMS 7.6 + Oracle 19c + Data Guard configuration plus the integrations to Empower CDS, Benchling ELN, eTMF, the LC-MS/MS instrument cluster, the GLP archive interface, Helios, and Lyrae. Each CI carries vendor-named parameter, chosen value, default-vs-custom flag, justification, FS-IDs traced, and the planned IQ/OQ verification.

The CS is the controlled design baseline that IQ and OQ execute against. Vendor internals (Watson core, run-acceptance engine, 4PL/5PL curve-fit engine, ISR sampler, hook-effect detector) remain Thermo Fisher's SDLC responsibility.

## 2. Scope

### 2.1 In scope

- Watson LIMS 7.6 configuration: per-study DRAFT-EFFECTIVE workflow; ICH M10 acceptance-criteria binding; GLP role-separation (Study Director / PI / QAU / Archivist); audit-trail bindings; archive workflow per § 58.190; inspection-tenant provisioning.
- Oracle 19c Enterprise + Data Guard physical-standby configuration: audit-table GRANT model; PITR; nightly backup.
- Okta SSO + MFA configuration; AD group → Authority Role binding.
- Integration design: Empower CDS, Benchling ELN, eTMF, LC-MS/MS instrument cluster (Sciex / Waters), GLP archive system, Helios (Kafka), Lyrae (model-serving + drift webhook).
- Site-deployed components: ISR sampler runtime wrapper (FS-ISR-01), inspection-tenant provisioning service (FS-IRT-01), Helios audit publisher (FS-XINT-LYR-03), AI-assist client adapter `CTS-LYR-CLIENT-1.x` (FS-XINT-LYR-01).

### 2.2 Out of scope

- Watson core internals (run-acceptance engine, curve-fit engines, GLP archive write path internals).
- Empower CDS configuration (separate URS+FS).
- Benchling ELN, eTMF, instrument software, Lyrae model lifecycle (separate URSs).
- GLP archive physical infrastructure.

## 3. Architectural Overview

The CS layers nine configuration domains on top of FS § 3: (1) Okta SSO + MFA; (2) Watson application configuration; (3) Oracle 19c policy and Data Guard; (4) Per-study build, method registry, ICH M10 thresholds; (5) Sample lifecycle (receipt → aliquot → freeze/thaw → storage); (6) Run-acceptance + ISR + run-review + reportable-release; (7) Study-report builder + § 58.190 archive gateway; (8) Inspection-tenant provisioning; (9) Cross-system integrations including Helios audit publisher + Lyrae AI-assist client.

```
                  Okta SSO + MFA (CI-15..18)
                  │  SAML 2.0 + step-up MFA
                  ▼
   ┌─────────────────────────────────────────────────────────────────┐
   │            Watson LIMS 7.6 Active Cluster                       │
   │   ┌─────────────────────────────────────────────────────────┐   │
   │   │ Watson App Tier                                          │  │
   │   │   Authority Roles (CI-19..27)                            │  │
   │   │   Per-study config wizard (CI-30..35)                    │  │
   │   │   ICH M10 Acceptance Engine binding (CI-40..43)          │  │
   │   │   ISR sampler binding (CI-44..46)                        │  │
   │   │   GLP role-separation (CI-50..53)                        │  │
   │   │   Run-review SoD enforcement (CI-60..62)                 │  │
   │   │   Reportable-result release engine (CI-65..68)           │  │
   │   │   § 58.185 study-report builder (CI-70..74)              │  │
   │   │   § 58.190 archive gateway (CI-80..84)                   │  │
   │   │   Inspection tenant provisioner (CI-90..93)              │  │
   │   │   Lyrae AI-assist feature flag (CI-100..104)             │  │
   │   └────────┬─────────────────────────────────────────────────┘  │
   │            │                                                    │
   │   ┌────────▼────────────────────────────────────────────────┐  │
   │   │ Oracle 19c Enterprise + Data Guard (RPO ≤ 15 min)        │ │
   │   │   Audit-table GRANT model (CI-13)                        │ │
   │   │   RMAN + PITR (CI-50, CI-55)                             │ │
   │   │   Archive-tablespace deletion-block (CI-83)              │ │
   │   └──────────────────────────────────────────────────────────┘  │
   └─┬───────────┬──────────────┬───────────────┬──────────────────┬─┘
     │           │              │               │                  │
     ▼           ▼              ▼               ▼                  ▼
   LC-MS/MS   Benchling      eTMF          GLP Archive          Helios + Lyrae
   + Empower   ELN          (study report) (§ 58.190)           (Kafka + AI)
   (CI-110)   (CI-115)      (CI-118)       (CI-120..124)        (CI-130..136)
                                                                     │
                                                                     ▼
                                                                  Splunk SIEM
                                                                  `wel-watson` (CI-140)
```

## 4. Configuration Specification

One row per CI. Vendor-named CIs follow *Thermo Fisher Watson LIMS 7.6 Configuration Reference* (rev. 2024-10) and *Watson LIMS 7.6 System Administrator's Guide* (rev. 2024-10).

| CI-ID | Configuration item (named per vendor) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| CI-01 | Watson → System Settings → `Cluster topology` | Active production + Data Guard cold DR | Custom | Per FS-PLAT-01; RPO ≤ 15 min / RTO ≤ 4 h. | FS-PLAT-01 | IQ-PLAT-01 |
| CI-02 | Watson → System Settings → `Per-study config workflow` | `DRAFT → REVIEW → APPROVED → EFFECTIVE` | Custom | Per FS-CFG-01. | FS-CFG-01 | OQ-CFG-01 |
| CI-03 | Watson → System Settings → `Pre-analysis sign-off required` | `true` | Custom | Per FS-CFG-01. | FS-CFG-01 | OQ-CFG-01 |
| CI-04 | Watson → System Settings → `Configuration export format` | PDF/A-3 + machine-readable JSON | Custom | Per FS-CFG-02. | FS-CFG-02 | OQ-CFG-02 |
| CI-05 | Oracle 19c → Edition | Enterprise Edition | Default | Per FS-PLAT-02. | FS-PLAT-02 | IQ-DB-01 |
| CI-06 | Oracle 19c → Data Guard | Physical standby; sync mode | Custom | Per FS-PLAT-02. | FS-PLAT-02 | IQ-DB-02 |
| CI-07 | Watson → eSign → `Hash algorithm` | `HMAC-SHA256` over record-hash + signer-id + timestamp | Custom | Per FS-PART11-05 cryptographic link. | FS-PART11-05 | OQ-PART11-05 |
| CI-08 | Watson → eSign → `Meaning-of-Signature list (operations)` | `Review, Approve, Reject, Lock, Author, Reissue` | Custom | Per FS-PART11-04. | FS-PART11-04 | OQ-PART11-04 |
| CI-09 | Watson → eSign → `Meaning-of-Signature list (GLP)` | `Study Director Approve, QAU Statement, PI Site-Portion, Archivist Transfer, Archivist Restore` | Custom | Per FS-GLP-05, FS-RPT-04, FS-ARC-05. | FS-GLP-05, FS-RPT-04, FS-ARC-05 | OQ-PART11-04 |
| CI-10 | Watson → eSign → `RequireReAuthOnSigning` (token max-age) | `5 min` | Custom | Per FS-PART11-07. | FS-PART11-07 | OQ-PART11-07 |
| CI-11 | Watson → eSign → `Same-user-two-roles-deny` | `Enabled` (server-side SoD enforcement) | Custom | Per FS-REL-03 / FS-PART11-13 equivalent. | FS-REL-03, FS-RVW-01 | OQ-RELEASE-SOD-01 |
| CI-12 | Watson → eSign → `Study Director delegation` | `Denied at signing time` | Custom | Per FS-GLP-01 / FS-RPT-04. | FS-GLP-01, FS-RPT-04 | OQ-GLP-01 |
| CI-13 | Oracle 19c → Audit-table GRANT model | INSERT-only to Watson service role; UPDATE/DELETE denied to all roles; QAU-review schema separately ACL'd | Custom | Per FS-AUD-02 / FS-AUD-04. | FS-AUD-02, FS-AUD-04 | OQ-AUD-APPENDONLY-01 |
| CI-14 | Watson → Audit-Trail → Retrospective-entry flag | `Enabled` with mandatory delay reason | Custom | Per FS-DI-03. | FS-DI-03 | OQ-DI-03 |
| CI-15 | Okta → SAML 2.0 binding for Watson SP | `entityID=watson.cetus.local` | Custom | Per FS-PART11-02. | FS-PART11-02 | IQ-OKTA-01 |
| CI-16 | Okta → MFA factor enforcement | `Push + WebAuthn` (no SMS) | Custom | Per FS-PART11-02 (MFA required). | FS-PART11-02 | IQ-OKTA-02 |
| CI-17 | Okta → Step-up MFA on Study Director sign-off | `Required` (fresh factor < 5 min) | Custom | Per FS-PART11-07 + FS-GLP-01. | FS-PART11-07, FS-GLP-01 | OQ-PART11-07 |
| CI-18 | Okta-DB uniqueness constraint | Email + employeeId; reuse blocked | Custom | Per FS-PART11-06. | FS-PART11-06 | OQ-PART11-06 |
| CI-19 | Watson Authority Role ↔ AD/Okta-group `Lab-Watson-Bioanalysts` | `Bioanalyst` (run analyses; no release) | Custom | Per FS-PART11-02 / FS-REL-02. | FS-PART11-02, FS-REL-02 | OQ-ROLE-01 |
| CI-20 | Watson Authority Role ↔ `Lab-Watson-SeniorBioanalysts` | `SeniorBioanalyst` (review; no self-review; no release) | Custom | Per FS-REL-02 / FS-RVW-01. | FS-REL-02, FS-RVW-01 | OQ-ROLE-02 |
| CI-21 | Watson Authority Role ↔ `Lab-Watson-StudyDirectors` | `StudyDirector` (per § 58.33; final sign-off; non-delegatable per CI-12) | Custom | Per FS-GLP-01 / FS-REL-02 / FS-RPT-04. | FS-GLP-01, FS-REL-02, FS-RPT-04 | OQ-ROLE-03 |
| CI-22 | Watson Authority Role ↔ `Lab-Watson-PIs` | `PrincipalInvestigator` (multi-site per-site sign-off under SD) | Custom | Per FS-STD-05 / FS-REL-02. | FS-STD-05, FS-REL-02 | OQ-ROLE-04 |
| CI-23 | Watson Authority Role ↔ `Lab-Watson-MethodOwners` | `MethodOwner` (method create/edit; cannot Approve) | Custom | Per FS-MTH-02. | FS-MTH-02 | OQ-ROLE-05 |
| CI-24 | Watson Authority Role ↔ `Lab-Watson-MethodApprovers` | `MethodApprover` (QA + Study Director co-approval per FS-MTH-02) | Custom | Per FS-MTH-02. | FS-MTH-02 | OQ-ROLE-06 |
| CI-25 | Watson Authority Role ↔ `Lab-Watson-QAU` | `QAU` (independent read across all studies; eSign QAU Statement; cannot edit operations records) per § 58.35 | Custom | Per FS-GLP-02 / FS-RPT-05. | FS-GLP-02, FS-RPT-05 | OQ-ROLE-07 |
| CI-26 | Watson Authority Role ↔ `Lab-Watson-Archivist` | `Archivist` (per § 58.190; sole archive read/write; cannot edit archived records) | Custom | Per FS-GLP-06 / FS-ARC-02. | FS-GLP-06, FS-ARC-02 | OQ-ROLE-08 |
| CI-27 | Watson Authority Role ↔ `Lab-Watson-Auditor` | `Auditor` (read-only inspection tenant) | Custom | Per FS-IRT-01. | FS-IRT-01 | OQ-ROLE-09 |
| CI-28 | Watson Authority Role ↔ `Lab-Watson-LIMSAdmin` | `LIMSAdmin` (config; cannot release; cannot UPDATE/DELETE audit) | Custom | Per FS-AUD-02. | FS-AUD-02 | OQ-ROLE-10 |
| CI-29 | Watson Authority Role ↔ Service principals (Empower / ELN / eTMF / Archive / Instrument / Helios / Lyrae) | Per-integration service role; mTLS-bound | Custom | Per FS-INT-* + FS-XINT-LYR-*. | FS-INT-CDS-01, FS-INT-ELN-01, FS-INT-ETMF-01, FS-INT-INST-01, FS-INT-ARCH-01, FS-XINT-LYR-01..04 | IQ-INT-01 |
| CI-30 | Watson Study-Build Wizard → Required-elements check | `sponsor + protocol-id + protocol-version + IRB/IEC or TF approval + SD assignment + method-validation evidence` | Custom | Per FS-STD-01. | FS-STD-01 | OQ-STD-01 |
| CI-31 | Watson Protocol-Pin Module | `(sample_id, acquired_at) → protocol_version` immutable binding | Custom | Per FS-STD-02 / FS-GLP-03. | FS-STD-02, FS-GLP-03 | OQ-STD-02 |
| CI-32 | Watson Protocol Document Template | § 58.120(a) required-fields enforced; missing → block SD sign-off | Custom | Per FS-STD-03. | FS-STD-03 | OQ-STD-03 |
| CI-33 | Watson Protocol-Amendment Workflow | `reason + SD eSign + date + version increment`; prior versions immutable | Custom | Per FS-STD-04. | FS-STD-04 | OQ-STD-04 |
| CI-34 | Watson Multi-Site Model | Per-site PI assigned scope; PI signature workflow per site portion | Custom | Per FS-STD-05. | FS-STD-05 | OQ-STD-05 |
| CI-35 | Watson Configuration export pipeline | Per-study config export PDF/A-3 + JSON within 1 BD | Custom | Per FS-CFG-02 / FS-INS-01. | FS-CFG-02, FS-INS-01 | OQ-CFG-02 |
| CI-36 | Watson Method Registry → `validation_status` enum | `{full, partial, cross, none}` | Default | Per FS-MTH-01. | FS-MTH-01 | OQ-MTH-01 |
| CI-37 | Watson Method Registry → run-acceptance binding | Only `validation_status=full` permitted at regulated run construction | Custom | Per FS-MTH-01 / FS-MTH-04. | FS-MTH-01, FS-MTH-04 | OQ-MTH-04 |
| CI-38 | Watson Method Registry → ICH M10 §§ 3 / 4 parameter set | Parameter set selected per `method_type` (chromatographic vs LBA) | Custom | Per FS-MTH-03. | FS-MTH-03 | OQ-MTH-03 |
| CI-39 | Watson Method Registry → Method-version-drift detector | `partial-validation / cross-validation` flow triggered per ICH M10 § 6.1 | Custom | Per FS-MTH-05. | FS-MTH-05 | OQ-MTH-05 |
| CI-40 | Watson Run-Acceptance Engine → Chromatographic thresholds | `cal ±15% / LLOQ ±20% / QC ±15%; ≥ 75% / ≥ 67% / ≥ 50%` per ICH M10 § 3.3.2 | Custom | Per FS-RUN-02. | FS-RUN-02 | OQ-RUN-02 |
| CI-41 | Watson Run-Acceptance Engine → LBA thresholds | `cal ±20% / LLOQ ±25% / QC ±20%; ≥ 75% / ≥ 67% / ≥ 50%` per ICH M10 § 4.3.2 | Custom | Per FS-RUN-02. | FS-RUN-02 | OQ-RUN-02 |
| CI-42 | Watson Run-Acceptance Engine → Fail-the-run mode | `Automatic` (no manual override at engine layer) | Custom | Per FS-RUN-02. | FS-RUN-02 | OQ-RUN-02 |
| CI-43 | Watson Run-Construction Wizard | Template enforces n calibrators + n QCs per level per study | Custom | Per FS-RUN-01. | FS-RUN-01 | OQ-RUN-01 |
| CI-44 | Watson ISR Module → Clinical sampling rate | `10%` (deterministic seeded random) | Custom | Per FS-ISR-01 / FS-RUN-03. | FS-ISR-01, FS-RUN-03 | OQ-ISR-01 |
| CI-45 | Watson ISR Module → Non-clinical sampling rate | `7%` (deterministic seeded random) | Custom | Per FS-ISR-01. | FS-ISR-01 | OQ-ISR-01 |
| CI-46 | Watson ISR Module → Pass criteria | Chromatographic ±20%; LBA ±30%; ≥ 67% repeats within (per ICH M10 § 5) | Custom | Per FS-ISR-02 / FS-RUN-03. | FS-ISR-02, FS-RUN-03 | OQ-ISR-02 |
| CI-47 | Watson Reanalysis Policy | Per-study rule-engine: instrument-failure (re-assay), insufficient-sample (no re-assay), failed-QC (re-assay batch); per ICH M10 §§ 3.3.4 / 4.3.4 | Custom | Per FS-RUN-04 / FS-RVW-02. | FS-RUN-04, FS-RVW-02 | OQ-RVW-02 |
| CI-48 | Watson Stability-Reanalysis Scheduler | 30 / 90 / 180-d intervals per method | Custom | Per FS-ISR-04. | FS-ISR-04 | OQ-ISR-04 |
| CI-49 | Watson ISR Report Builder | Auto-attach ISR appendix to § 58.185 final report | Custom | Per FS-ISR-03. | FS-ISR-03 | OQ-ISR-03 |
| CI-50 | Watson GLP role-separation enforcement | Study Director cannot analyse; QAU cannot edit operations; Archivist sole archive gateway | Custom | Per FS-GLP-01 / FS-GLP-02 / FS-GLP-06. | FS-GLP-01, FS-GLP-02, FS-GLP-06 | OQ-GLP-01..06 |
| CI-51 | Watson QAU separate schema | `qau_review` tables ACL'd to QAU role only; operations roles read-only | Custom | Per FS-AUD-04 / FS-GLP-02. | FS-AUD-04, FS-GLP-02 | OQ-AUD-04 |
| CI-52 | Watson § 58.130 recorder-id capture | `recorder_id` mandatory on all data entries; retroactive flagged | Custom | Per FS-GLP-04. | FS-GLP-04 | OQ-GLP-04 |
| CI-53 | Watson § 58.81 sample-record schema | Collection date / type / source / storage location / custody trail mandatory | Custom | Per FS-SMP-02. | FS-SMP-02 | OQ-SMP-02 |
| CI-54 | Watson Sample-Receipt UI | Required fields per FS-SAMP-01 validated server-side | Custom | Per FS-SAMP-01. | FS-SAMP-01 | OQ-SAMP-01 |
| CI-55 | Watson Sample-Aliquot Model | `parent_sample_id`, `aliquot_id`, `freeze_thaw_count`, `location_history` (FIFO), audit-bound custody | Custom | Per FS-SAMP-02. | FS-SAMP-02 | OQ-SAMP-02 |
| CI-56 | Watson Freeze/Thaw Budget enforcement | `max_ft_cycles` (default 5 per ICH M10 method-validation); exceeded → block + Method-Owner override | Custom | Per FS-SAMP-03. | FS-SAMP-03 | OQ-SAMP-03 |
| CI-57 | Watson Storage-Location Service | freezer-id / shelf / rack / position + BMS temperature integration; excursion > 1 °C / > 4 h → `StorageExcursion` event linked to aliquots | Custom | Per FS-SAMP-04 / FS-SMP-01. | FS-SAMP-04, FS-SMP-01 | OQ-SAMP-04 |
| CI-58 | Watson Sample-Destruction Workflow | Study Director + QAU dual eSign per § 58.81; record retained per § 58.195 | Custom | Per FS-SAMP-05. | FS-SAMP-05 | OQ-SAMP-05 |
| CI-59 | Watson Shipping Module | Courier + ship ts + recipient + in-transit temp log (CSV upload); arrival-inspection record required; else aliquot `RECEIPT_PENDING` | Custom | Per FS-SAMP-06. | FS-SAMP-06 | OQ-SAMP-06 |
| CI-60 | Watson Run-Review UI → SoD enforcement | reviewer != acquirer; server-side check | Custom | Per FS-RVW-01. | FS-RVW-01 | OQ-RVW-01 |
| CI-61 | Watson Re-assay Tag schema | `reassay_type ∈ {reinject, reextract}`; replacement vs supplement semantics | Custom | Per FS-RVW-03. | FS-RVW-03 | OQ-RVW-03 |
| CI-62 | Watson Run-Rejection Workflow | Senior Bioanalyst eSign + reason; rejected runs retained; excluded from reportable | Custom | Per FS-RVW-04. | FS-RVW-04 | OQ-RVW-04 |
| CI-63 | Watson LBA Plate-Map model | `(plate_id, well_position, well_type, sample_id_or_level, replicate_index)` | Custom | Per FS-LBA-01. | FS-LBA-01 | OQ-LBA-01 |
| CI-64 | Watson ADA Tiered Workflow | screen → confirmatory → titer; cut-points method-bound; ladder captured | Custom | Per FS-LBA-03. | FS-LBA-03 | OQ-LBA-03 |
| CI-65 | Watson Reportable-Result computer | Method-bound rule (default: mean of accepted replicates); rounding per protocol | Custom | Per FS-REL-01. | FS-REL-01 | OQ-REL-01 |
| CI-66 | Watson Release Workflow chain | `Bioanalyst → Senior Bioanalyst → Study Director (or PI per site) → QAU` | Custom | Per FS-REL-02. | FS-REL-02 | OQ-REL-02 |
| CI-67 | Watson Release SoD table | User-role-position table denies same user holding two consecutive roles | Custom | Per FS-REL-03. | FS-REL-03 | OQ-RELEASE-SOD-01 |
| CI-68 | Watson Held-Reportable expiry | `14 d` auto-revoke; SD re-approval required | Custom | Per FS-REL-04. | FS-REL-04 | OQ-REL-04 |
| CI-69 | Watson NAb Assay Schema | Cell-line lot / passage / plate controls captured | Custom | Per FS-LBA-04. | FS-LBA-04 | OQ-LBA-04 |
| CI-70 | Watson Study-Report Builder template | § 58.185(a) required content + § 58.185(a)(13) storage-locations auto-populated | Custom | Per FS-RPT-01 / FS-RPT-02. | FS-RPT-01, FS-RPT-02 | OQ-RPT-01 |
| CI-71 | Watson Report-Amendment Workflow | Numbered amendments + reason; original immutable; amendments linked | Custom | Per FS-RPT-03. | FS-RPT-03 | OQ-RPT-03 |
| CI-72 | Watson Final-Report SD eSign | Non-delegatable per § 58.33 (CI-12 reinforces); UI prevents delegation | Custom | Per FS-RPT-04 / FS-GLP-01. | FS-RPT-04, FS-GLP-01 | OQ-RPT-04 |
| CI-73 | Watson QAU Statement auto-populate | Inspection-dates + findings-reported-to-SD-dates from `qau_review` schema (CI-51) | Custom | Per FS-RPT-05 / FS-GLP-05. | FS-RPT-05, FS-GLP-05 | OQ-RPT-05 |
| CI-74 | Watson Report Export format | PDF/A-3 + XML | Custom | Per FS-DI-02. | FS-DI-02, FS-RPT-01 | OQ-RPT-01 |
| CI-75 | Watson Method-Validation Parameters captured | Selectivity / specificity / accuracy / precision / linearity / LLOQ / dilution integrity / matrix effect / recovery / carryover / stability | Custom | Per FS-MTH-03. | FS-MTH-03 | OQ-MTH-03 |
| CI-76 | Watson Method-Scope Validator | At run-construction: matrix + species + concentration range checked; out-of-scope blocked | Custom | Per FS-MTH-04. | FS-MTH-04 | OQ-MTH-04 |
| CI-77 | Watson Hook-Effect rule | High-conc sample read < mid-range standard → flag + auto-route to higher dilution | Custom | Per FS-LBA-05. | FS-LBA-05 | OQ-LBA-05 |
| CI-78 | Watson Storage-Excursion event propagation | `StorageExcursion` → all aliquots in affected location flagged | Custom | Per FS-SAMP-04. | FS-SAMP-04 | OQ-SAMP-04 |
| CI-79 | Watson Method-Owner override (freeze/thaw exceedance) | Method Owner eSign + documented reason captured | Custom | Per FS-SAMP-03. | FS-SAMP-03 | OQ-SAMP-03 |
| CI-80 | Watson Archive Transfer Module | Bundles raw + documentation + protocols + specimens-inventory + final report; immutable transfer event | Custom | Per FS-ARC-01 / FS-GLP-06. | FS-ARC-01, FS-GLP-06 | OQ-ARC-01 |
| CI-81 | Watson Archive Access Service | Archivist role only (CI-26); non-Archivist read requires justification + audit-trail entry | Custom | Per FS-ARC-02 / FS-GLP-06. | FS-ARC-02, FS-GLP-06 | OQ-ARC-02 |
| CI-82 | Watson Archive Index | Study-id / sponsor / dates / materials; full-text search | Custom | Per FS-ARC-03. | FS-ARC-03 | OQ-ARC-03 |
| CI-83 | Watson Deletion-Block Service | Pre-retention-threshold deletion attempts denied at DB layer; logged + alerted | Custom | Per FS-ARC-04 / FS-GLP-07. | FS-ARC-04, FS-GLP-07 | OQ-ARC-04 |
| CI-84 | Watson Archive-Restore Workflow | Archivist-only; produces audit-trail entry + sponsor/authority correspondence reference | Custom | Per FS-ARC-05. | FS-ARC-05 | OQ-ARC-05 |
| CI-85 | Watson Retention Threshold (default) | `≥ 10 years post-Application` (per sponsor contract overrides) | Custom | Per FS-GLP-07 / FS-ARC-04. | FS-GLP-07, FS-ARC-04 | OQ-ARC-04 |
| CI-86 | Watson Inspection-Tenant Provisioning Service | On-demand within 4 BH; signed + time-limited URL; SELECT-only DB role | Custom | Per FS-IRT-01 / FS-INS-01. | FS-IRT-01, FS-INS-01 | OQ-IRT-01 |
| CI-87 | Watson Inspection-Tenant Watermark | `inspection_id` watermark added on every export | Custom | Per FS-IRT-02. | FS-IRT-02 | OQ-IRT-02 |
| CI-88 | Watson Inspection-Tenant Export | QA eSign required | Custom | Per FS-IRT-02. | FS-IRT-02 | OQ-IRT-02 |
| CI-89 | Watson Mock-Inspection Drill schedule | Quarterly; findings logged in `CET-MOCK-INSP-YYYYQN` | Custom | Per FS-IRT-03 / FS-INS-02. | FS-IRT-03, FS-INS-02 | OQ-IRT-03 |
| CI-90 | Watson Per-batch Senior Review schedule | Pre-batch-close required event | Custom | Per FS-AUD-03. | FS-AUD-03 | OQ-AUD-03 |
| CI-91 | Watson Monthly Operations Review schedule | First Monday each month | Custom | Per FS-AUD-03. | FS-AUD-03 | OQ-AUD-03 |
| CI-92 | Cornerstone LMS curriculum gating | `CET-CURR-WATSON-Bioanalyst-v1`; SD + QAU additional `CET-CURR-WATSON-GLPv1` | Custom | Per FS-TRN-01 / FS-TRN-02. | FS-TRN-01, FS-TRN-02 | IQ-LMS-01 |
| CI-93 | Watson UI session timeout (idle) | `10 min` lock | Custom | Per FS-SEC-01..04 baseline. | FS-SEC-02 | IQ-CFG-02 |
| CI-94 | Watson TLS configuration | `TLS 1.3 only`; cipher floor per site InfoSec | Custom | Per FS-SEC-01. | FS-SEC-01 | IQ-SEC-01 |
| CI-95 | Watson at-rest encryption | `AES-256` on Oracle tablespace + archive volumes | Custom | Per FS-SEC-01. | FS-SEC-01 | IQ-SEC-02 |
| CI-96 | Watson RBAC quarterly review | Workflow `CET-AC-REVIEW-WATSON` | Custom | Per FS-SEC-02 / FS-PR-01. | FS-SEC-02 | OQ-PR-01 |
| CI-97 | Watson workstation USB block | GPO `Block-RemovableMedia` (override under CR) | Custom | Per FS-SEC-03. | FS-SEC-03 | IQ-GPO-01 |
| CI-98 | Watson Vulnerability Scan schedule | Monthly Tenable scan; criticals remediated ≤ 30 d | Custom | Per FS-SEC-04. | FS-SEC-04 | OQ-SEC-04 |
| CI-99 | Watson Annual PR template | `CET-PR-WATSON-YYYYMMDD` (Director BA + VP DMPK + VP QA + QAU Lead) | Custom | Per FS-PR-01. | FS-PR-01 | OQ-PR-01 |
| CI-100 | Watson AI-Assist Feature Flag | `cfg.ai_assist.peak_review.enabled = false` (default) | Default | Per FS-XINT-LYR-01. | FS-XINT-LYR-01 | OQ-AI-01 |
| CI-101 | Watson AI-Assist Flag-Toggle gate | Validation Lead + Bioanalytical Lead eSign; audit-trail entry | Custom | Per FS-XINT-LYR-01. | FS-XINT-LYR-01 | OQ-AI-01 |
| CI-102 | Watson AI-Assist Client adapter | `CTS-LYR-CLIENT-1.x` (Lyrae-only routing pinned) | Custom | Per FS-XINT-LYR-01. | FS-XINT-LYR-01 | IQ-AI-CLIENT-01 |
| CI-103 | Watson AI-Assist UI | Per-peak Accept/Reject only; bulk-accept absent; bulk_accept payloads rejected server-side | Custom | Per FS-XINT-LYR-02. | FS-XINT-LYR-02 | OQ-AI-02 |
| CI-104 | Watson AI-Assist Audit row schema | `{run_id, peak_id, model_version, confidence, analyst_action, override_reason}` | Custom | Per FS-XINT-LYR-02. | FS-XINT-LYR-02 | OQ-AI-02 |
| CI-105 | Lyrae Drift Webhook subscription | PSI > 0.15 OR confusion-matrix shift > 5% → CI-100 flipped false + MasterControl deviation | Custom | Per FS-XINT-LYR-04. | FS-XINT-LYR-04 | OQ-AI-04 |
| CI-106 | Helios Audit Publisher → Kafka topic | `helios.ingest.watson.aipeak.v1` (schema-registry pinned) | Custom | Per FS-XINT-LYR-03. | FS-XINT-LYR-03 | OQ-HELIOS-01 |
| CI-107 | Helios Audit Publisher → pre-handover retention | 2 y local | Custom | Per FS-XINT-LYR-03. | FS-XINT-LYR-03 | OQ-HELIOS-02 |
| CI-110 | Watson ↔ Empower Connector | HTTPS REST bidirectional; checksum SHA-256 both directions | Custom | Per FS-INT-CDS-01. | FS-INT-CDS-01 | OQ-INT-CDS-01 |
| CI-111 | Watson ↔ Empower mTLS cert | `cetus-watson-emp-2026q2` | Custom | Per FS-INT-CDS-01. | FS-INT-CDS-01 | IQ-PKI-01 |
| CI-115 | Watson ↔ Benchling ELN cross-ref | `prep_record_urn` field; bound at batch | Custom | Per FS-INT-ELN-01. | FS-INT-ELN-01 | OQ-INT-ELN-01 |
| CI-116 | Watson ↔ Benchling auth | OAuth2 client-credentials + mTLS | Custom | Per FS-INT-ELN-01. | FS-INT-ELN-01 | IQ-INT-ELN-01 |
| CI-118 | Watson ↔ eTMF Publisher | Study-completion event publishes report to eTMF | Custom | Per FS-INT-ETMF-01. | FS-INT-ETMF-01 | OQ-INT-ETMF-01 |
| CI-120 | Watson ↔ GLP Archive Gateway → service principal | `cetus\svc-watson-archive` (mTLS + Vault-rotated 90-d) | Custom | Per FS-INT-ARCH-01 / FS-GLP-06. | FS-INT-ARCH-01, FS-GLP-06 | IQ-INT-ARCH-01 |
| CI-121 | Watson ↔ GLP Archive Gateway → write path | Archivist-role-only via dedicated service-account | Custom | Per FS-INT-ARCH-01. | FS-INT-ARCH-01 | OQ-INT-ARCH-01 |
| CI-122 | Watson ↔ Instrument Cluster (Sciex / Waters) | Acquisition-metadata feed; instrument-id + serial logged per run | Custom | Per FS-INT-INST-01. | FS-INT-INST-01 | OQ-INT-INST-01 |
| CI-123 | Watson ↔ Instrument schema validator | Schema-registry pinned; mismatch → ingest reject + alert | Custom | Per FS-INT-INST-01 (FS § 6 risk: schema drift). | FS-INT-INST-01 | OQ-INT-INST-01 |
| CI-124 | Watson ↔ BMS Temperature Feed | Per-freezer temperature stream; excursion rule per CI-57 | Custom | Per FS-SAMP-04. | FS-SAMP-04 | OQ-SAMP-04 |
| CI-125 | Veeam B&R 12.1 → Oracle RMAN backup | Nightly full + continuous archived redo; SHA-256 verify | Custom | Per FS-BAK-01 / FS-XSYS-BAK-01. | FS-BAK-01, FS-XSYS-BAK-01 | IQ-BAK-01 |
| CI-126 | Veeam SureBackup quarterly | QA witness on `CET-PROC-WATSON-RESTORE-001` | Custom | Per FS-BAK-02. | FS-BAK-02 | IQ-BAK-02 |
| CI-127 | S3 Object Lock Compliance retention | 15 y (bioanalytical record); 25 y (release-linked) | Custom | Per FS-XSYS-BAK-01 / FS-GLP-07. | FS-XSYS-BAK-01, FS-GLP-07 | IQ-S3-01 |
| CI-128 | LTO-9 air-gap monthly rotation | Per AUR-URS-BACKUP-001 | Custom | Per FS-XSYS-BAK-01. | FS-XSYS-BAK-01 | IQ-LTO-01 |
| CI-129 | DR drill annual cadence | Full failover + run acquisition on DR + failback | Custom | Per FS-PLAT-01. | FS-PLAT-01 | OQ-DR-01 |
| CI-130 | Validation Dossier binding | `CET-VAL-WATSON-001` | Custom | Per FS-PART11-01. | FS-PART11-01 | (admin) |
| CI-131 | Ops manual binding | `CET-RB-WATSON-OPS-001` | Custom | (vendor SCN CR pattern; mirrors other systems) | FS-PART11-01 (procedural) | (admin) |
| CI-140 | Splunk UF → heavy index | `wel-watson` (TCP/9997 outbound) | Custom | Per FS-AUD-01 / FS-AV-01 / FS-PART11-02..07 forwarding. | FS-AV-01, FS-PART11-02, FS-SEC-04 | IQ-SIEM-01 |
| CI-141 | Splunk Dashboard `wel-watson-availability` | 99.5% business-hours target | Custom | Per FS-AV-01. | FS-AV-01 | OQ-AV-01 |
| CI-142 | Splunk Alert `wel-watson-archive-deletion-attempt` | Trigger on CI-83 block event | Custom | Per FS-ARC-04. | FS-ARC-04 | OQ-ARC-04 |
| CI-143 | Splunk Alert `wel-watson-lockout` | Okta lockout for `Lab-Watson-*` | Custom | Per FS-PART11-07 / FS-SEC-04. | FS-PART11-07, FS-SEC-04 | OQ-SEC-04 |

## 5. Workflow + Business-Rule Design

### 5.1 Per-Study Build Workflow `WAT-WF-STUDY-BUILD`

Per FS-CFG-01 / FS-STD-01..05. Wizard (CI-30) requires sponsor + protocol-id + version + IRB/IEC or testing-facility approval + Study Director assignment + method-validation evidence. Missing element blocks DRAFT → REVIEW. State machine: DRAFT → REVIEW → APPROVED → EFFECTIVE (CI-02). Pre-analysis sign-off mandatory (CI-03).

### 5.2 Protocol-Pinning Workflow `WAT-WF-PROTOCOL-PIN`

Per FS-STD-02 / FS-GLP-03. Each sample acquired binds `(sample_id, acquired_at) → protocol_version` (CI-31). Amendment (CI-33) creates new pinned version; prior-acquired samples remain pinned unless explicitly migrated via deviation. Protocol document template (CI-32) enforces § 58.120(a) required content; missing field blocks SD sign-off.

### 5.3 Method Lifecycle + Validation Workflow `WAT-WF-METHOD`

Per FS-MTH-01..05. Author creates DRAFT → Reviewer review → Author ≠ Approver constraint at promotion (CI-23, CI-24). Method record carries `validation_status` (CI-36); only `full` permitted at regulated run construction (CI-37). Parameter set per `method_type` (CI-38). Version-drift detector (CI-39) triggers partial/cross-validation flow.

### 5.4 Sample Receipt → Run Workflow `WAT-WF-SAMPLE-LIFECYCLE`

Per FS-SAMP-01..06 / FS-SMP-01..02. Receipt UI (CI-54) validates fields server-side. Aliquot model (CI-55) tracks parent → child + freeze/thaw + location-history + custody. Freeze/Thaw budget enforced (CI-56). Storage-location service (CI-57) integrates BMS temp feed; excursion → `StorageExcursion` event propagates to aliquots (CI-78). Destruction requires SD + QAU dual eSign (CI-58). Shipping module (CI-59) requires arrival-inspection record.

### 5.5 Run-Construction + Acceptance Workflow `WAT-WF-RUN`

Per FS-RUN-01..04. Wizard (CI-43) enforces n calibrators + n QCs per level. Run-Acceptance Engine (CI-40, CI-41) applies ICH M10 §§ 3.3.2 / 4.3.2 thresholds; fail-the-run automatic (CI-42).

### 5.6 ISR + Stability Reanalysis Workflow `WAT-WF-ISR`

Per FS-ISR-01..04. ISR Module (CI-44 clinical 10% / CI-45 non-clinical 7%) draws deterministic seeded random sample stratified across concentration range. Pass criteria (CI-46) per ICH M10 § 5. Per-sample record persists original/repeat/mean/% dev/pass-fail (FS-ISR-03). Stability scheduler (CI-48) triggers re-analysis at 30/90/180 d. ISR appendix auto-attached (CI-49).

### 5.7 Run Review + Re-assay Decision Workflow `WAT-WF-REVIEW-REASSAY`

Per FS-RVW-01..04. Run-Review UI (CI-60) enforces reviewer ≠ acquirer SoD server-side. Reanalysis policy engine (CI-47) presents permitted re-assay options per ICH M10 §§ 3.3.4 / 4.3.4. Re-injection vs re-extraction tagged distinctly (CI-61). Run-rejection (CI-62) requires Senior Bioanalyst eSign.

### 5.8 LBA-Specific Workflow `WAT-WF-LBA`

Per FS-LBA-01..05. Plate-map model (CI-63) binds wells to types. Curve-fit (CI-64-bound; engine vendor-internal) supports 4PL/5PL with quality flags. ADA tiered (CI-64) screen → confirmatory → titer. NAb assay record schema (CI-69). Hook-effect rule (CI-77) auto-routes to higher dilution.

### 5.9 Reportable-Result Release Workflow `WAT-WF-RELEASE`

Per FS-REL-01..04. Reportable-result computer (CI-65). Release chain (CI-66): Bioanalyst → Senior Bioanalyst → SD (or PI per site) → QAU. SoD table (CI-67) denies two consecutive roles per same record. Held-reportable expiry 14 d (CI-68).

### 5.10 § 58.185 Study Report Workflow `WAT-WF-STUDY-REPORT`

Per FS-RPT-01..05. Report-builder template (CI-70) enforces § 58.185(a) content; storage-locations auto-populated from archive interface (CI-70). Amendments (CI-71) numbered + linked. SD eSign (CI-72) non-delegatable. QAU statement (CI-73) auto-populated from `qau_review` schema.

### 5.11 § 58.190 GLP Archive Workflow `WAT-WF-ARCHIVE`

Per FS-ARC-01..05 / FS-GLP-06 / FS-GLP-07. Archive Transfer Module (CI-80) bundles study artefacts at study-completion. Archive Access Service (CI-81) restricts to Archivist role; non-Archivist read requires justification + audit. Archive Index (CI-82) supports full-text search. Deletion-Block Service (CI-83) prevents pre-retention-threshold deletion at DB layer. Restore Workflow (CI-84) Archivist-only.

### 5.12 Inspection-Readiness Workflow `WAT-WF-INSPECTION`

Per FS-IRT-01..03 / FS-INS-01..02. Inspection-Tenant Provisioning (CI-86) reconstitutes read-only complete study view within 4 BH; tenant URL signed + time-limited. Tenant DB role SELECT only; export requires QA eSign + watermark (CI-87, CI-88). Quarterly mock drills (CI-89).

### 5.13 AI-Assist Peak-Review Workflow `WAT-WF-AI-PEAK`

Per FS-XINT-LYR-01..04. Feature flag (CI-100) `false` by default; toggle (CI-101) requires Validation Lead + Bioanalytical Lead eSign + audit-trail stamp. Client adapter (CI-102) routes to Lyrae only. UI (CI-103) per-peak Accept/Reject; bulk-accept disabled both UI and server. Every action audited (CI-104). Drift webhook (CI-105) auto-disables feature on PSI > 0.15 or confusion-matrix > 5%.

### 5.14 Audit-Trail Review Workflow `WAT-WF-AUDIT-REVIEW`

Per FS-AUD-03. Per-batch Senior Bioanalyst review (CI-90). Monthly Operations review (CI-91). QAU independent review (CI-25 + CI-51) reports outside operations chain. Helios publisher (CI-106, CI-107) ships AI-assist events to Helios as system-of-record for AI-peak audit review.

### 5.15 Annual Periodic Review Workflow `WAT-WF-PR`

Per FS-PR-01. Template (CI-99) covers configuration drift, audit-trail review evidence, method-validation status inventory, GLP archive compliance, training currency, integration health. Signed by Director BA + VP DMPK + VP QA + QAU Lead.

## 6. Role-Permission Matrix Design

Implements FS-PART11-06 / FS-GLP-01..06 / FS-REL-03 / FS-AUD-04. AD/Okta groups bind 1:1 to Watson Authority Roles (CI-19..28).

| Permission | Bioanalyst | SrBioan | SD | PI | MethodOwner | MethodApprover | QAU | Archivist | Auditor | LIMSAdmin |
|---|---|---|---|---|---|---|---|---|---|---|
| Run analyses | ✓ | ✓ | – | – | – | – | – | – | – | – |
| Review run (not own) | – | ✓ | – | – | – | – | – | – | – | – |
| eSign `Review` | – | ✓ | – | – | – | – | – | – | – | – |
| eSign `Approve` reportable (operations) | – | – | ✓ | ✓ (site-portion) | – | – | – | – | – | – |
| eSign QAU Statement | – | – | – | – | – | – | ✓ | – | – | – |
| eSign Study-Director final report (non-delegatable) | – | – | ✓ | – | – | – | – | – | – | – |
| eSign Reject | – | ✓ | ✓ | ✓ | – | – | – | – | – | – |
| Method create / edit | – | – | – | – | ✓ | – | – | – | – | – |
| Method `Approve` to `full` | – | – | (co-approver) | – | – | ✓ (QA + SD dual) | – | – | – | – |
| Per-study config edit | – | – | – | – | – | – | – | – | – | ✓ |
| QAU independent read all | – | – | – | – | – | – | ✓ | – | – | – |
| Archive read | – | – | (with justification + audit) | (with justification) | – | – | (with justification) | ✓ | – | – |
| Archive write / transfer | – | – | – | – | – | – | – | ✓ | – | – |
| Archive restore | – | – | – | – | – | – | – | ✓ | – | – |
| Inspection-tenant read | – | – | – | – | – | – | – | – | ✓ | – |
| Inspection-tenant export (with QA eSign) | – | – | – | – | – | – | ✓ | – | ✓ | – |
| Audit-trail read | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Audit-trail UPDATE/DELETE | – | – | – | – | – | – | – | – | – | – (denied to all) |
| AI-Assist feature flag toggle | – | – | – | – | – | – | – | – | – | – (Validation Lead + Bioanalytical Lead dual eSign per CI-101) |

Hard constraints: (a) Study Director cannot perform analyses (CI-50); (b) QAU is in a separate ACL'd schema (CI-51); (c) Archivist is sole archive read/write gateway (CI-81); (d) same user cannot hold two consecutive roles in a release chain (CI-67); (e) Study Director signature non-delegatable at signing time (CI-12).

## 7. Integration Design

### 7.1 IF-OKTA (SAML 2.0 + MFA)

| Aspect | Design |
|---|---|
| Endpoint | Okta tenant; SP `entityID=watson.cetus.local` (CI-15) |
| MFA | Push + WebAuthn (CI-16); SMS forbidden |
| Step-up | Required at SD sign-off (CI-17) |
| Uniqueness | Okta-DB constraint on email + employeeId (CI-18) |
| FS-IDs traced | FS-PART11-02, FS-PART11-06, FS-PART11-07, FS-XSYS-AD-01 |

### 7.2 IF-AD (LDAPS bind for legacy on-prem service-accounts)

| Aspect | Design |
|---|---|
| Endpoint | `ldaps://cetus.local:636` |
| Groups | `Lab-Watson-*` per CI-19..28 |
| Conditional Access | `Lab-App Conditional Access (MFA + device-compliance)` per FS-XSYS-AD-01 |
| FS-IDs traced | FS-XSYS-AD-01 |

### 7.3 IF-DB (Oracle 19c + Data Guard)

| Aspect | Design |
|---|---|
| Edition | Enterprise (CI-05) |
| Data Guard | Physical standby sync mode (CI-06) |
| Audit-table GRANT | INSERT-only; UPDATE/DELETE denied (CI-13) |
| QAU schema | Separately ACL'd (CI-51) |
| Backup | RMAN nightly + continuous archived redo to immutable cold storage + S3 Object Lock (CI-125, CI-127) |
| Deletion-block | Pre-retention deletion denied at DB (CI-83) |
| FS-IDs traced | FS-PLAT-01, FS-PLAT-02, FS-AUD-02, FS-AUD-04, FS-ARC-04, FS-BAK-01, FS-XSYS-BAK-01 |

### 7.4 IF-Empower-CDS

| Aspect | Design |
|---|---|
| Protocol | HTTPS REST bidirectional; mTLS via `cetus-watson-emp-2026q2` (CI-110, CI-111) |
| Checksum | SHA-256 both directions; mismatch → alert |
| FS-IDs traced | FS-INT-CDS-01 |

### 7.5 IF-Benchling-ELN

| Aspect | Design |
|---|---|
| Cross-reference | `prep_record_urn` bound at batch (CI-115) |
| AuthN | OAuth2 client-credentials + mTLS (CI-116) |
| FS-IDs traced | FS-INT-ELN-01 |

### 7.6 IF-eTMF

| Aspect | Design |
|---|---|
| Trigger | Study-completion event publishes report (CI-118) |
| FS-IDs traced | FS-INT-ETMF-01 |

### 7.7 IF-Instruments (Sciex / Waters LC-MS/MS cluster)

| Aspect | Design |
|---|---|
| Feed | Acquisition metadata + instrument-id + serial per run (CI-122) |
| Validation | Schema-registry pinned (CI-123); mismatch → ingest reject |
| FS-IDs traced | FS-INT-INST-01 |

### 7.8 IF-GLP-Archive

| Aspect | Design |
|---|---|
| Service principal | `cetus\svc-watson-archive` (mTLS + Vault-rotated 90-d) (CI-120) |
| Write path | Archivist-role-only (CI-121) |
| FS-IDs traced | FS-INT-ARCH-01, FS-GLP-06 |

### 7.9 IF-BMS (Freezer Temperature Feed)

| Aspect | Design |
|---|---|
| Endpoint | Per-freezer temperature stream → CI-57 storage-location service |
| Excursion rule | > 1 °C / > 4 h → `StorageExcursion` event |
| FS-IDs traced | FS-SAMP-04, FS-SMP-01 |

### 7.10 IF-Helios (Kafka audit publisher for AI-Assist)

| Aspect | Design |
|---|---|
| Topic | `helios.ingest.watson.aipeak.v1` schema-registry pinned (CI-106) |
| Pre-handover retention | 2 y local (CI-107) |
| FS-IDs traced | FS-XINT-LYR-03 |

### 7.11 IF-Lyrae (AI-Assist model serve + drift webhook)

| Aspect | Design |
|---|---|
| Client adapter | `CTS-LYR-CLIENT-1.x` Lyrae-only (CI-102) |
| Drift webhook | PSI > 0.15 OR conf-matrix > 5% → CI-100 false + deviation (CI-105) |
| Audit row | `{run_id, peak_id, model_version, confidence, analyst_action, override_reason}` (CI-104) |
| FS-IDs traced | FS-XINT-LYR-01..04 |

### 7.12 IF-SIEM (Splunk Universal Forwarder)

| Aspect | Design |
|---|---|
| Endpoint | UF → indexer cluster TCP/9997 |
| Heavy index | `wel-watson` (CI-140) |
| Alert rules | `wel-watson-availability` (CI-141), `wel-watson-archive-deletion-attempt` (CI-142), `wel-watson-lockout` (CI-143) |
| FS-IDs traced | FS-AV-01, FS-PART11-02, FS-SEC-04, FS-ARC-04 |

## 8. Site-Deployed Components (micro-SDS)

Four small site-developed components extend the vendor platform.

### 8.1 `WAT-SVC-ISR-WRAPPER-01` — ISR Sampler Runtime Wrapper

| Field | Value |
|---|---|
| Type | Site sidecar service wrapping the Watson ISR sampler engine |
| Responsibility | FS-ISR-01 sampler invocation with site-specific seed strategy + stratification audit |
| Inputs | Study-build inputs + completed runs |
| Outputs | ISR sample list + audit entry per selection |
| Algorithm | Read study type; call Watson ISR engine with deterministic seed (study-id + batch-id); persist selection + stratification proof; emit audit event |
| Storage | Container image; deployed via Helm to site Kubernetes cluster |
| Unit-test | OQ-ISR-01 contract test against fixed-seed expected output |
| FS-IDs traced | FS-ISR-01 |

### 8.2 `WAT-SVC-INSPECTION-PROVISIONER-01` — Inspection-Tenant Provisioning Service

| Field | Value |
|---|---|
| Type | Site service that constructs read-only tenant on demand |
| Responsibility | FS-IRT-01 within 4 BH |
| Inputs | Inspection-id + study-id + requesting inspector |
| Outputs | Signed time-limited URL; SELECT-only Oracle role + materialised view set |
| Algorithm | Spawn read-replica from latest backup; create SELECT-only role; mint JWT URL with `inspection_id` + `exp`; emit audit event |
| Storage | Container image; deployed via Helm |
| Unit-test | OQ-IRT-01 timing test (< 4 BH) + role-grant test |
| FS-IDs traced | FS-IRT-01, FS-IRT-02, FS-INS-01 |

### 8.3 `WAT-SVC-HELIOS-PUBLISHER-01` — Helios Audit Publisher

| Field | Value |
|---|---|
| Type | Site sidecar consuming Oracle CDC for AI-Assist audit events and publishing to Kafka |
| Responsibility | FS-XINT-LYR-03 ingest of AI-Assist peak-review events to Helios |
| Inputs | Oracle CDC stream from `ai_assist_audit` table |
| Outputs | Kafka topic `helios.ingest.watson.aipeak.v1` JSON Lines envelope |
| Algorithm | Read CDC LSN; transform; publish with idempotency key `{source_system, event_id}`; persist `helios_ack_ts` on broker ack |
| Storage | Container image; deployed via Helm |
| Unit-test | Contract test against Helios schema registry |
| FS-IDs traced | FS-XINT-LYR-03 |

### 8.4 `CTS-LYR-CLIENT-1.x` — AI-Assist Client Adapter

| Field | Value |
|---|---|
| Type | Site library (.NET) embedded in Watson AI-Assist client path |
| Responsibility | FS-XINT-LYR-01 Lyrae-only routing pin |
| Inputs | Peak-review request (chromatogram hash) |
| Outputs | Lyrae inference response + model_version + confidence |
| Algorithm | Pin endpoint to Lyrae cluster URL list; reject any other endpoint at config-load; emit audit event per call |
| Storage | NuGet package in site registry; embedded at Watson AI-Assist build |
| Unit-test | OQ-AI-01 (only-Lyrae routing + endpoint-pin enforcement) |
| FS-IDs traced | FS-XINT-LYR-01, FS-XINT-LYR-02 |

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- 21 CFR Part 58 §§ .29, .33, .35, .81, .120, .130, .185, .190, .195.
- FDA *Bioanalytical Method Validation Guidance for Industry* (2018).

### EU
- EMA *Guideline on Bioanalytical Method Validation* (2011).
- EU GMP Annex 11.

### DACH
- BfR GLP-Bundesstelle + Länder authorities (DE).
- Swissmedic (CH); AGES PharmMed (AT).

### International
- ICH M10 (2022); ICH E6(R3) GCP (Step 4, 2025).
- OECD Principles of GLP.
- ISPE GAMP 5 (2nd Ed., 2022).

### Vendor
- Thermo Fisher — *Watson LIMS 7.6 Configuration Reference* (rev. 2024-10).
- Thermo Fisher — *Watson LIMS 7.6 System Administrator's Guide* (rev. 2024-10).
- Thermo Fisher — *Watson LIMS 7.6 Integration Adapter Reference* (Empower / ELN / eTMF / Archive).
- Oracle — *Oracle Database 19c Administrator's Guide* (Data Guard, RMAN, audit-trail GRANT model).
- Okta — *SAML 2.0 Application Setup Guide*.

### Site / parent
- `CET-FS-WATSON-001 v1.1`; `CET-URS-WATSON-001 v1.1`.
- `CET-VAL-WATSON-001`; `CET-RB-WATSON-OPS-001`; `CET-PROC-WATSON-RESTORE-001`.

## Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) | Design intent (brief) | Verified by |
|---|---|---|---|
| DS-PLAT-01 | FS-PLAT-01 | Active + DR + DR drill (CI-01, CI-129) | IQ-PLAT-01 |
| DS-PLAT-02 | FS-PLAT-02 | Oracle Enterprise + Data Guard (CI-05, CI-06) | IQ-DB-01..02 |
| DS-CFG-01 | FS-CFG-01 | Per-study workflow + pre-analysis sign-off (CI-02, CI-03) | OQ-CFG-01 |
| DS-CFG-02 | FS-CFG-02 | Config export PDF/A-3 + JSON (CI-04, CI-35) | OQ-CFG-02 |
| DS-MTH-01 | FS-MTH-01 | validation_status binding (CI-36, CI-37) | OQ-MTH-01 |
| DS-MTH-02 | FS-MTH-02 | Author ≠ Approver + QA + SD dual (CI-23, CI-24) | OQ-MTH-02 |
| DS-MTH-03 | FS-MTH-03 | ICH M10 §§ 3/4 parameter set (CI-38, CI-75) | OQ-MTH-03 |
| DS-MTH-04 | FS-MTH-04 | Method-scope validator (CI-76) | OQ-MTH-04 |
| DS-MTH-05 | FS-MTH-05 | Version-drift detector (CI-39) | OQ-MTH-05 |
| DS-SMP-01 | FS-SMP-01 | Custody captured + excursion alerts (CI-57, CI-78) | OQ-SAMP-04 |
| DS-SMP-02 | FS-SMP-02 | § 58.81 schema (CI-53) | OQ-SMP-02 |
| DS-RUN-01 | FS-RUN-01 | Construction wizard (CI-43) | OQ-RUN-01 |
| DS-RUN-02 | (vendor-internal — Watson run-acceptance engine internals) + threshold CI-40/41 | ICH M10 thresholds (CI-40, CI-41, CI-42) | OQ-RUN-02 |
| DS-RUN-03 | FS-RUN-03, FS-ISR-02 | ISR pass criteria (CI-46) | OQ-ISR-02 |
| DS-RUN-04 | FS-RUN-04 | Reanalysis policy engine (CI-47) | OQ-RVW-02 |
| DS-GLP-01 | FS-GLP-01 | Non-delegatable SD sign-off (CI-12, CI-72) | OQ-GLP-01 |
| DS-GLP-02 | FS-GLP-02 | QAU separate schema (CI-25, CI-51) | OQ-AUD-04 |
| DS-GLP-03 | FS-GLP-03 | Protocol-pin (CI-31) | OQ-STD-02 |
| DS-GLP-04 | FS-GLP-04 | § 58.130 recorder-id capture (CI-52) | OQ-GLP-04 |
| DS-GLP-05 | FS-GLP-05 | Study-report builder (CI-70..73) | OQ-RPT-01..05 |
| DS-GLP-06 | FS-GLP-06 | Archive Archivist gateway (CI-26, CI-81, CI-121) | OQ-ARC-02 |
| DS-GLP-07 | FS-GLP-07 | Retention threshold + deletion-block (CI-83, CI-85) | OQ-ARC-04 |
| DS-AUD-01 | (vendor-internal — Watson audit-trail engine) | n/a (flagged) | n/a |
| DS-AUD-02 | FS-AUD-02 | Audit-table GRANT (CI-13) | OQ-AUD-APPENDONLY-01 |
| DS-AUD-03 | FS-AUD-03 | Per-batch + monthly review (CI-90, CI-91) | OQ-AUD-03 |
| DS-AUD-04 | FS-AUD-04 | QAU separate non-editable (CI-51) | OQ-AUD-04 |
| DS-PART11-01 | FS-PART11-01 | SOP catalogue + annual review | (admin) |
| DS-PART11-02 | FS-PART11-02 | Okta SAML + MFA (CI-15, CI-16) | IQ-OKTA-01..02 |
| DS-PART11-03 | FS-PART11-03 | Audit trail (CI-13 + FS-AUD-01) | OQ-AUD-APPENDONLY-01 |
| DS-PART11-04 | FS-PART11-04 | Meaning-of-sig closed lists (CI-08, CI-09) | OQ-PART11-04 |
| DS-PART11-05 | FS-PART11-05 | HMAC-SHA256 sig hash (CI-07) | OQ-PART11-05 |
| DS-PART11-06 | FS-PART11-06 | Okta uniqueness (CI-18) | OQ-PART11-06 |
| DS-PART11-07 | FS-PART11-07 | Token max-age 5 min + step-up MFA (CI-10, CI-17) | OQ-PART11-07 |
| DS-DI-01 | FS-DI-01 | actor_id NOT NULL constraint | OQ-DI-01 |
| DS-DI-02 | FS-DI-02 | PDF/A-3 + XML export (CI-74) | OQ-RPT-01 |
| DS-DI-03 | FS-DI-03 | Retrospective-entry flag (CI-14) | OQ-DI-03 |
| DS-DI-04 | FS-DI-04 | Raw data immutable (Oracle policy) | OQ-DI-04 |
| DS-DI-05 | FS-DI-05 | OQ regression — deterministic calc | OQ-DI-05 |
| DS-DI-06 | FS-DI-06 | Metadata completeness + chronological DB constraint | OQ-DI-06 |
| DS-INT-CDS-01 | FS-INT-CDS-01 | Empower bidirectional + checksum (CI-110, CI-111) | OQ-INT-CDS-01 |
| DS-INT-ELN-01 | FS-INT-ELN-01 | Benchling cross-ref + OAuth (CI-115, CI-116) | OQ-INT-ELN-01 |
| DS-INT-ETMF-01 | FS-INT-ETMF-01 | eTMF publisher on study completion (CI-118) | OQ-INT-ETMF-01 |
| DS-INT-INST-01 | FS-INT-INST-01 | Instrument metadata feed + schema validator (CI-122, CI-123) | OQ-INT-INST-01 |
| DS-INT-ARCH-01 | FS-INT-ARCH-01 | Archive gateway service principal (CI-120, CI-121) | IQ-INT-ARCH-01 |
| DS-PERF-01 | FS-PERF-01 | Run-construction P95 ≤ 30 s | OQ-PERF-01 |
| DS-AV-01 | FS-AV-01 | Availability dashboard 99.5% (CI-141) | OQ-AV-01 |
| DS-BAK-01 | FS-BAK-01 | RMAN nightly + continuous redo (CI-125) | IQ-BAK-01 |
| DS-BAK-02 | FS-BAK-02 | Quarterly SureBackup (CI-126) | IQ-BAK-02 |
| DS-SEC-01 | FS-SEC-01 | TLS 1.3 + AES-256 (CI-94, CI-95) | IQ-SEC-01..02 |
| DS-SEC-02 | FS-SEC-02 | RBAC quarterly review (CI-96) | OQ-PR-01 |
| DS-SEC-03 | FS-SEC-03 | USB block GPO (CI-97) | IQ-GPO-01 |
| DS-SEC-04 | FS-SEC-04 | Tenable monthly + 30-d remediation (CI-98) | OQ-SEC-04 |
| DS-TRN-01 | FS-TRN-01 | LMS gating + GLP curriculum (CI-92) | IQ-LMS-01 |
| DS-TRN-02 | FS-TRN-02 | Annual refresher (CI-92) | IQ-LMS-01 |
| DS-PR-01 | FS-PR-01 | PR template (CI-99) | OQ-PR-01 |
| DS-INS-01 | FS-INS-01 | Inspection export ≤ 1 BD / 4 BH (CI-86, CI-35) | OQ-IRT-01 |
| DS-INS-02 | FS-INS-02 | Mock inspection drills (CI-89) | OQ-IRT-03 |
| DS-SAMP-01 | FS-SAMP-01 | Receipt UI required fields (CI-54) | OQ-SAMP-01 |
| DS-SAMP-02 | FS-SAMP-02 | Aliquot model (CI-55) | OQ-SAMP-02 |
| DS-SAMP-03 | FS-SAMP-03 | Freeze/Thaw budget + override (CI-56, CI-79) | OQ-SAMP-03 |
| DS-SAMP-04 | FS-SAMP-04 | Storage service + excursion propagation (CI-57, CI-78) | OQ-SAMP-04 |
| DS-SAMP-05 | FS-SAMP-05 | Destruction dual eSign (CI-58) | OQ-SAMP-05 |
| DS-SAMP-06 | FS-SAMP-06 | Shipping + arrival inspection (CI-59) | OQ-SAMP-06 |
| DS-STD-01 | FS-STD-01 | Study-build wizard required-elements (CI-30) | OQ-STD-01 |
| DS-STD-02 | FS-STD-02 | Protocol-pin module (CI-31) | OQ-STD-02 |
| DS-STD-03 | FS-STD-03 | Protocol document template § 58.120(a) (CI-32) | OQ-STD-03 |
| DS-STD-04 | FS-STD-04 | Amendment workflow (CI-33) | OQ-STD-04 |
| DS-STD-05 | FS-STD-05 | Multi-site PI assignment + per-site eSign (CI-34) | OQ-STD-05 |
| DS-LBA-01 | FS-LBA-01 | Plate-map model (CI-63) | OQ-LBA-01 |
| DS-LBA-02 | (vendor-internal — Watson 4PL/5PL curve-fit engine) | Engine consumed; per-curve flags persisted | OQ-LBA-02 |
| DS-LBA-03 | FS-LBA-03 | ADA tiered workflow + cut-points (CI-64) | OQ-LBA-03 |
| DS-LBA-04 | FS-LBA-04 | NAb schema (CI-69) | OQ-LBA-04 |
| DS-LBA-05 | (vendor-internal — Watson hook-effect detector) + rule CI-77 | Hook-effect rule (CI-77) | OQ-LBA-05 |
| DS-ISR-01 | (vendor-internal — Watson ISR sampler) + wrapper § 8.1 + rate CI-44/45 | ISR sampler wrapper (§ 8.1, CI-44, CI-45) | OQ-ISR-01 |
| DS-ISR-02 | FS-ISR-02 | Pass criteria (CI-46) | OQ-ISR-02 |
| DS-ISR-03 | FS-ISR-03 | ISR appendix auto-attach (CI-49) | OQ-ISR-03 |
| DS-ISR-04 | FS-ISR-04 | Stability scheduler 30/90/180 d (CI-48) | OQ-ISR-04 |
| DS-RVW-01 | FS-RVW-01 | reviewer ≠ acquirer (CI-60) | OQ-RVW-01 |
| DS-RVW-02 | FS-RVW-02 | Reanalysis policy engine (CI-47) | OQ-RVW-02 |
| DS-RVW-03 | FS-RVW-03 | Re-injection vs re-extraction tag (CI-61) | OQ-RVW-03 |
| DS-RVW-04 | FS-RVW-04 | Run-rejection workflow (CI-62) | OQ-RVW-04 |
| DS-REL-01 | FS-REL-01 | Reportable-result computer (CI-65) | OQ-REL-01 |
| DS-REL-02 | FS-REL-02 | Release workflow chain (CI-66) | OQ-REL-02 |
| DS-REL-03 | FS-REL-03 | SoD table (CI-67) | OQ-RELEASE-SOD-01 |
| DS-REL-04 | FS-REL-04 | Held expiry 14 d (CI-68) | OQ-REL-04 |
| DS-RPT-01 | FS-RPT-01 | § 58.185 template (CI-70) | OQ-RPT-01 |
| DS-RPT-02 | FS-RPT-02 | Storage locations auto-populated (CI-70) | OQ-RPT-02 |
| DS-RPT-03 | FS-RPT-03 | Amendment workflow (CI-71) | OQ-RPT-03 |
| DS-RPT-04 | FS-RPT-04 | SD eSign non-delegatable (CI-12, CI-72) | OQ-RPT-04 |
| DS-RPT-05 | FS-RPT-05 | QAU statement auto-populate (CI-73) | OQ-RPT-05 |
| DS-ARC-01 | FS-ARC-01 | Archive transfer module (CI-80) | OQ-ARC-01 |
| DS-ARC-02 | FS-ARC-02 | Access service Archivist-only (CI-81, CI-121) | OQ-ARC-02 |
| DS-ARC-03 | FS-ARC-03 | Archive index (CI-82) | OQ-ARC-03 |
| DS-ARC-04 | FS-ARC-04 | Deletion-block + alert (CI-83, CI-142) | OQ-ARC-04 |
| DS-ARC-05 | FS-ARC-05 | Restore workflow Archivist-only (CI-84) | OQ-ARC-05 |
| DS-IRT-01 | FS-IRT-01 | Provisioner service (§ 8.2, CI-86) | OQ-IRT-01 |
| DS-IRT-02 | FS-IRT-02 | Tenant SELECT-only + watermark (CI-87, CI-88) | OQ-IRT-02 |
| DS-IRT-03 | FS-IRT-03 | Mock-inspection quarterly (CI-89) | OQ-IRT-03 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 | Okta SAML + Conditional Access (§ 7.1, § 7.2) | IQ-OKTA-01..02 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 | RMAN + S3 Object Lock + LTO-9 (CI-125, CI-127, CI-128) | IQ-BAK-01 |
| DS-XINT-LYR-01 | FS-XINT-LYR-01 | Feature flag + toggle gate + Lyrae-only client (§ 8.4, CI-100, CI-101, CI-102) | OQ-AI-01 |
| DS-XINT-LYR-02 | FS-XINT-LYR-02 | Per-peak UI + bulk-accept absent + audit row (CI-103, CI-104) | OQ-AI-02 |
| DS-XINT-LYR-03 | FS-XINT-LYR-03 | Helios publisher (§ 8.3, CI-106, CI-107) | OQ-HELIOS-01..02 |
| DS-XINT-LYR-04 | FS-XINT-LYR-04 | Lyrae drift webhook + auto-disable (CI-105) | OQ-AI-04 |

## Appendix B — Design-level Risk Register

| ID | Risk | Likelihood | Impact | Mitigation reference | Design surface |
|---|---|---|---|---|---|
| DR-01 | SD signature delegation bypass via session sharing (analyst signs on SD's logged-in session) | Low | Critical | Step-up MFA at sign-off (CI-17) + non-delegatable enforcement at signing (CI-12); SOP-level training | CI-12, CI-17 |
| DR-02 | QAU schema ACL drift on Oracle patch (CI-51 GRANT lost on schema rebuild) | Low | Critical | Schema-ACL verification step in post-patch OQ; quarterly DB GRANT audit | CI-51, CI-13 |
| DR-03 | Archive deletion-block service (CI-83) bypassed by Oracle SYS-privilege user | Low | Critical | DB GRANT denies UPDATE/DELETE to all roles including SYS via Oracle Vault; quarterly Vault policy audit | CI-83, CI-13 |
| DR-04 | ISR sampler seed reuse across studies leaks selection pattern | Low | High | Seed derived from study-id + batch-id (§ 8.1 algorithm); OQ-ISR-01 verifies seed entropy | § 8.1, CI-44, CI-45 |
| DR-05 | Inspection-tenant provisioning (§ 8.2) leaves SELECT-only role active after inspection | Low | High | Tenant URL time-limited (CI-86); tenant role auto-revoked at JWT exp; weekly orphan-role audit | § 8.2, CI-86 |
| DR-06 | Watson SCN upgrade reverts vendor-default CI (e.g., signature hash CI-07 to SHA-1) | Low | Critical | Post-upgrade IQ delta-check across all 143 CIs + FS-PART11-05 re-test | CI-07 |
| DR-07 | Authority Role ↔ Okta-group drift on group rename without Watson re-binding | Low | Critical | Quarterly access review (CI-96) + Authority-Role export reconciled with Okta | CI-19..28 |
| DR-08 | mTLS cert `cetus-watson-emp-2026q2` expiry blocks Empower integration silently | Low | High | 30-d pre-expiry pager alert + auto-rotation | CI-111 |
| DR-09 | Lyrae drift webhook (CI-105) fails to fire → AI-Assist runs past threshold | Low | Critical | Heartbeat from Lyrae to Watson; absent heartbeat 30 min → CI-100 false + alert | CI-105 |
| DR-10 | AI-Assist bulk-accept reconstructed via legitimate per-peak Accept loop in browser console | Low | High | Server-side rate-limit on Accept actions per second + audit-trail anomaly detection | CI-103, CI-104 |
| DR-11 | Storage-excursion event (CI-78) propagation fails when freezer goes offline (no temperature feed) | Medium | High | BMS connectivity heartbeat; absent heartbeat 1 h → all aliquots in freezer flagged `STORAGE_UNKNOWN` | CI-57, CI-124 |
| DR-12 | Multi-site PI sign-off (CI-22, CI-34) cycle stall when PI on leave | Medium | Medium | Workflow timeout monitor (e.g., 5 BD) → escalation to SD + QAU notification | CI-22, CI-34 |
| DR-13 | Freeze/thaw budget (CI-56) reset on aliquot re-labelling (data-entry error rather than physical event) | Low | High | Re-label workflow requires Method-Owner eSign + impact assessment; OQ-SAMP-03 includes re-label scenario | CI-55, CI-56 |
| DR-14 | Held-Reportable (CI-68) 14-d expiry resets on minor edit, indefinitely extending hold | Low | High | Expiry timer anchored to first SD approval; minor edit does not reset | CI-68 |
| DR-15 | Helios publisher (§ 8.3) drops events on schema-registry mismatch | Low | Critical | Schema-evolution gate at publisher startup; reconciliation job daily; 0.01% mismatch → MasterControl deviation | § 8.3, CI-106 |
| DR-16 | Lyrae client adapter (§ 8.4) endpoint-pin bypassed via DNS spoof | Low | Critical | Endpoint pinned by IP + cert SAN + mTLS pinning; DNS resolution short-circuited | § 8.4, CI-102 |
| DR-17 | Inspection-Tenant export watermark (CI-87) stripped from exported PDF | Low | High | Watermark embedded in PDF/A-3 metadata + visible body; QA eSign + auto-checksum at export gate (CI-88) | CI-87, CI-88 |
| DR-18 | LBA hook-effect rule (CI-77) bypassed when method-bound threshold mis-set at method-build | Low | High | Method-build validator enforces threshold range; OQ-LBA-05 exercises edge cases | CI-77 |
| DR-19 | Sample-destruction workflow (CI-58) executed without QAU eSign due to UI race | Low | Critical | Server-side enforcement of dual eSign atomicity; OQ-SAMP-05 negative-path test | CI-58 |
| DR-20 | Method-version drift detector (CI-39) misses subtle reagent-lot change requiring partial validation | Medium | High | Reagent-lot field treated as method-bound; lot change triggers partial validation flow | CI-39 |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
