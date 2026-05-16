---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (v1.0 DS corpus ship)"
seed_corpus_basis:
  - "CYG-FS-VLM-001 v1.2 (parent FS, T3 Cat 4)"
  - "CYG-URS-VLM-001 v1.2 (parent URS, transitive)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 Configuration Specification conventions"
  - "21 CFR Part 11; EU GMP Annex 11; EU GMP Chapter 4; ICH Q9(R1); ICH Q10"
  - "FDA CSA (final, February 2026); BfArM Anlage 7; Swissmedic; AGES; PIC/S PI 041"
  - "ValGenesis VLM 5.x — Configuration Reference + Validation Approach"
parent_fs:
  document_number: CYG-FS-VLM-001
  version: "1.2"
  file: ../../../FS_FDS/_generated/final/Cygnus_Pharma_ValGenesis_VLM_FS_v1.3.md
parent_urs:
  document_number: CYG-URS-VLM-001
  version: "1.2"
  file: ../../../URS/_generated/final/Validation_Lifecycle_Management_ValGenesis__Cygnus_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Validation Lifecycle Management — ValGenesis VLM 5.x — Cygnus Konstanz Tenancy

**Document Number:** CYG-DS-VLM-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** CYG-FS-VLM-001 v1.2
**Parent URS:** CYG-URS-VLM-001 v1.2
**Site:** Cygnus Pharma AG, Konstanz, Germany *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS, multi-site federation across 5 sites)
**Project Mode:** Greenfield-SaaS w/ multi-site federation (Konstanz, Basel, Vienna, Boston, Singapore)
**FDA CSA classification:** Critical — risk-based testing applies (FDA *Computer Software Assurance for Production and Quality Management System Software*, final, February 2026)
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Chapter 4; ICH Q9(R1); ICH Q10; FDA CSA (Feb 2026); ISPE GAMP 5 + GPG Risk-Based Approach; PIC/S PI 041; BfArM (DE) Anlage 7; Swissmedic (CH); AGES (AT)

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Director, Validation Operations) | _____________ | _____________ | _____ |
| Reviewer (QA Reviewer) | _____________ | _____________ | _____ |
| Reviewer (System Owner — Director Validation Ops) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — VP IT Compliance) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (FDA CSA Liaison) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |
| Approver (VP IT Compliance) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue. Inherited Tier T3 from parent URS+FS pair. DS covers 86/86 FS-IDs; 0 FS-IDs flagged as vendor-internal — no site design surface. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

| Term | Definition |
|---|---|
| CI | Configuration Item in ValGenesis VLM 5.x |
| FDA CSA | FDA Computer Software Assurance — risk-based testing (Feb 2026 final) |
| RTM | Requirements Traceability Matrix |
| VSR | Validation Summary Report |
| VMP | Validation Master Plan |
| EC | Established Conditions (ICH Q12) |
| Verified by | Planned IQ / OQ / PQ test |

## 1. Purpose

This Configuration Specification records the technical design of the ValGenesis VLM 5.x multi-tenant SaaS tenancy at Cygnus Pharma, including FDA CSA risk-classification engine, per-module protocol authoring (FS/CS/DS/IQ/OQ/PQ), handheld + offline execution, deviation lifecycle, CSV training + certification, multi-site federation across 5 sites, and integration bindings to satisfy `CYG-FS-VLM-001` v1.2.

## 2. Scope

**In scope:** ValGenesis tenancy configuration; per-tenancy + per-project config; per-module protocol authoring; FDA CSA + GAMP RBA risk classification; handheld + offline execution + sync; deviation lifecycle per execution; CSV training + certification registry; multi-site federation (5 sites); audit-trail focused review; integration bindings to Okta + Vault QualityDocs + MasterControl + Application Portfolio + validated GitLab.

**Out of scope:** ValGenesis vendor source-code internals; Okta internals; Vault internals; MasterControl internals; Application Portfolio internals; GitLab internals.

## 3. Architectural Overview

The Cygnus Konstanz tenancy is the authoritative federation primary; 4 secondary sites (Basel, Vienna, Boston, Singapore) execute projects against locally-cached templates. Identity is Okta SAML 2.0 + MFA. Validated GitLab provides release-linked validation artefacts. Handheld app `ValGenesis Mobile 5.x` supports in-room execution with offline mode + biometric e-sig.

```
                           ┌──────────────────────────────────┐
                           │   Okta SAML 2.0 + MFA            │
                           └──────────────────┬───────────────┘
                                              │
              ┌───────────────────────────────▼────────────────────────────────────┐
              │  ValGenesis VLM 5.x — Cygnus tenancy (federation primary: Konstanz)  │
              │  ┌────────────────────────────────────────────────────────────┐    │
              │  │ Documents: URS / FS / CS / DS / RTM / IQ / OQ / PQ / VSR / VMP │  │
              │  │ Per-module Protocol Authoring                                │    │
              │  │ Risk-classification engine (FDA CSA + ICH Q9R1 + GAMP RBA)   │    │
              │  │ Execution capture (web + handheld + offline sync)            │    │
              │  │ Evidence-hash verifier (SHA-256)                              │    │
              │  │ Deviation lifecycle (per execution)                           │    │
              │  │ CSV Certification registry                                    │    │
              │  │ Federation Service (5 sites)                                   │    │
              │  └────────────────────────────────────────────────────────────┘    │
              └──┬───────────┬───────────┬──────────────┬───────────────────────────┘
                 │           │           │              │
                 ▼           ▼           ▼              ▼
            Vault       Master-      App Portfolio   GitLab (validated)
            QualityDocs Control      (inventory)     (release-linked)
                        (deviations)
              │
              ▼
         5 federated sites: Konstanz / Basel / Vienna / Boston / Singapore
         (Konstanz authoritative for templates)
```

### 3.1 Component-design inventory

| Layer | Component | Vendor / source | Version | Site design surface |
|---|---|---|---|---|
| Application | ValGenesis VLM 5.x tenancy | ValGenesis | 5.x | Configuration (§ 4) |
| Mobile | ValGenesis Mobile 5.x | ValGenesis | 5.x | Configuration (§ 4) |
| Identity | Okta | Okta | per site IT | Configuration (§ 4, § 7) |
| Counterparty | Vault QualityDocs | Veeva | 24R3+ | Bindings (§ 7) |
| Counterparty | MasterControl eQMS | MasterControl | QMS 2025 | Bindings (§ 7) |
| Counterparty | Application Portfolio | per site | per site | Bindings (§ 7) |
| Counterparty | Validated GitLab | GitLab | per site IT | Bindings (§ 7) |
| Federation peers | Basel / Vienna / Boston / Singapore | ValGenesis Federation | 5.x | Configuration (§ 4) |

---

## 4. Configuration Specification

### 4.1 Vendor Assurance + Configuration Lifecycle CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VND-01 | Vendor-assurance dossier (`CYG-VND-REG.ValGenesis`) | SOC 2 Type II + ISO 27001 + customer-shared CSV summary | Custom | Critical-vendor | FS-VND-01 | OQ-VND-REG-01 |
| DS-VND-02 | Release-eval runbook (`CYG-RB-VG-RELEASE`) | ≤ 14 d impact-assess | Custom | Vendor-release cadence | FS-VND-02 | OQ-VND-REL-01 |
| DS-VND-03 | Escalation runbook (`CYG-RB-VG-ESCALATE`) | named contacts | Custom | Escalation | FS-VND-03 | OQ-VND-ESCALATE-01 |
| DS-CFG-01 | Environment topology (`CFG_ENVS`) | `DEV → QC → UAT → PRODUCTION`; SoD `Config-Author ≠ Config-Approver` | Custom | Promotion discipline | FS-CFG-01 | OQ-CFG-LIFECYCLE-01 |
| DS-CFG-02 | Config-export script (`cyg-config-export.sh`) | FDA / EMA / BfArM / Swissmedic inspection format | Custom | Inspection-readiness | FS-CFG-02 | OQ-CFG-EXPORT-01 |

### 4.2 Document Lifecycle CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-DOC-01 | Document types (`DOC_TYPES`) | `URS, FS, CS, DS, RTM, IQ, OQ, PQ, VSR, VMP` | Custom | V-model coverage | FS-DOC-01 | OQ-DOC-TYPES-01 |
| DS-DOC-02 | Lifecycle states | `DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE`; e-signed; SoD | Custom | 5-state | FS-DOC-01 | OQ-DOC-STATES-01 |
| DS-DOC-03 | Template version control | Author ≠ Approver | Custom | SoD | FS-DOC-02 | OQ-DOC-VER-SOD-01 |
| DS-DOC-04 | Typed-link integrity | first-class typed links; broken-ref detection at sign-off | Custom | Traceability discipline | FS-DOC-03 | OQ-TYPED-LINK-01 |
| DS-DOC-05 | PDF/A-3 export | regulator-friendly format | Default | Inspection-ready | FS-DOC-04 | OQ-PDFA-EXPORT-01 |

### 4.3 Per-Module Protocol Authoring CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUTH-01 | FS author module + URS link (`cyg_fs_urs_link`) | typed link; orphan-URS check at sign-off | Custom | Traceability gate | FS-AUTH-01 | OQ-FS-URS-LINK-01 |
| DS-AUTH-02 | CS module per-CI fields | configurable values + verification method (OQ test ID) | Custom | CS-vs-OQ binding | FS-AUTH-02 | OQ-CS-VERIFY-LINK-01 |
| DS-AUTH-03 | DS module fields | architecture, algorithm, error handling (Cat-5 design space) | Custom | Cat-5 design capture | FS-AUTH-03 | OQ-DS-FIELDS-01 |
| DS-AUTH-04 | IQ module vendor-IQ inherit (`vendor_iq_inherit_ref`) | site-installed components listed separately | Custom | Vendor-IQ reuse | FS-AUTH-04 | OQ-IQ-INHERIT-01 |
| DS-AUTH-05 | OQ module test-case schema | per URS/FS/CS/DS line w/ expected results + acceptance criteria | Custom | Test-case completeness | FS-AUTH-05 | OQ-OQ-SCHEMA-01 |
| DS-AUTH-06 | PQ module scenario schema | end-to-end w/ prod-representative datasets | Custom | PQ realism | FS-AUTH-06 | OQ-PQ-SCHEMA-01 |
| DS-AUTH-07 | Template registry per module + promotion workflow (`wf_template_promote`) | Author ≠ Approver e-sig | Custom | Template SoD | FS-AUTH-07 | OQ-TPL-PROMOTE-01 |

### 4.4 FDA CSA + GAMP RBA Risk-Based Testing CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RBT-01 | CSA matrix (`csa_classification_matrix`) | production / QS criticality × intended-use category → tier `T1-Lean / T2-Standard / T3-Full` | Custom | FDA CSA Feb 2026 | FS-RBT-01 | OQ-CSA-MATRIX-01 |
| DS-RBT-02 | Critical-thinking justification field | free-text ≥ 200 chars w/ ICH Q9(R1) category; required at project start | Custom | Q9(R1) discipline | FS-RBT-02 | OQ-CSA-JUSTIFICATION-01 |
| DS-RBT-03 | GAMP-category declaration | per system `(1/3/4/5)`; drives default protocol structure | Custom | Cat-driven scope | FS-RBT-03 | OQ-GAMP-CAT-01 |
| DS-RBT-04 | Reclassification trigger | change to intended-use re-evaluates tier; downstream re-testing flagged | Custom | Re-eval discipline | FS-RBT-04 | OQ-RECLASS-01 |
| DS-RBT-05 | Portfolio dashboard (`cyg_dashboard_csa_depth`) | testing-depth distribution view | Custom | Portfolio KPI | FS-RBT-05 | PQ-CSA-DASH-01 |

### 4.5 Protocol Execution CIs (Handheld / Offline / E-Sig)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EXE-01 | Execution-record schema | step-by-step actual results + evidence + executor + witness sigs + ts (web or handheld) | Custom | Comprehensive record | FS-EXE-01 | OQ-EXE-SCHEMA-01 |
| DS-EXE-02 | Test-step deviation push | MasterControl via `IF-EQMS-DEV`; disposition flag controls continuation | Custom | Deviation discipline | FS-EXE-02 | OQ-EXE-DEV-PUSH-01 |
| DS-EXE-03 | Execution immutability | DB-level after completion; corrections via `wf_amend_execution` + re-sig | Custom | Anti-tamper | FS-EXE-03 | OQ-EXE-IMMUT-01 |
| DS-EXE-04 | Evidence hash (`SHA-256`) | computed on upload + verified on archive; tamper alert via `cyg_evidence_hash_check` | Custom | Forensic integrity | FS-EXE-04 | OQ-EVIDENCE-HASH-01 |
| DS-EXE-05 | NTP-sync via `chronyd` | across all executors | Default | Contemporaneous | FS-EXE-05 | OQ-NTP-01 |
| DS-EXE-06 | Handheld app (`ValGenesis Mobile 5.x`) | camera, barcode scanner, sensor in-room capture | Default | In-room evidence | FS-EXE-06 | OQ-MOBILE-CAPTURE-01 |
| DS-EXE-07 | Offline mode + sync (`wf_sync_execution`) | local storage; conflicts surface in `cyg_sync_conflicts` for Project Lead resolution | Custom | Offline resilience | FS-EXE-07 | OQ-OFFLINE-SYNC-01 |
| DS-EXE-08 | Handheld e-sig | fresh Okta token (max-age 5 min) + biometric (FaceID/TouchID) bound to Okta identity | Custom | § 11.200 + biometric 2FA | FS-EXE-08 | OQ-HANDHELD-SIG-01 |

### 4.6 Deviation Lifecycle CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-DEV-01 | Deviation schema | `test-step ref, observed, expected, immediate-action, disposition, root-cause-linkage` | Custom | Comprehensive | FS-DEV-01 | OQ-DEV-SCHEMA-01 |
| DS-DEV-02 | Idempotent eQMS push | `IF-EQMS-DEV`; idempotency `vlm:exec:<id>:step:<n>`; failed push blocks finalisation | Custom | Idempotent + gating | FS-DEV-02 | OQ-DEV-PUSH-IDEMP-01 |
| DS-DEV-03 | Severity enum + routing | `Minor / Major / Critical` drives `cyg_dev_routing` distribution | Custom | Severity-driven | FS-DEV-03 | OQ-DEV-ROUTING-01 |
| DS-DEV-04 | VSR auto-summary | deviation summary table in VSR template | Custom | Reporting discipline | FS-DEV-04 | OQ-VSR-DEV-SUMMARY-01 |

### 4.7 RTM Maintenance CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RTM-01 | RTM auto-gen | from typed links; orphan-URS flagging via `cyg_rtm_orphan_check` | Custom | Traceability discipline | FS-RTM-01 | OQ-RTM-AUTOGEN-01 |
| DS-RTM-02 | Completeness gate at VSR sign-off | orphan items must be justified or addressed | Custom | Coverage discipline | FS-RTM-02 | OQ-RTM-COMPLETENESS-01 |
| DS-RTM-03 | CSA risk-justified exemption | `test-not-required` flag w/ documented justification | Custom | FDA CSA spirit | FS-RTM-03 | OQ-RTM-EXEMPTION-01 |
| DS-RTM-04 | RTM versioned snapshots (`cyg_rtm_snapshot`) | at VSR-draft + VSR-final | Custom | Snapshot discipline | FS-RTM-04 | OQ-RTM-SNAPSHOT-01 |

### 4.8 CSV Training + Certification CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-TRN-CERT-01 | CSV curriculum library (`cyg_csv_curriculum`) | role-specific modules | Custom | Role-based | FS-TRN-CERT-01 | OQ-CSV-CURR-01 |
| DS-TRN-CERT-02 | Certification gate (`cyg_role_assignment`) | project-role denied if certification expired | Custom | Currency enforcement | FS-TRN-CERT-02 | OQ-CERT-GATE-01 |
| DS-TRN-CERT-03 | Annual refresher cron (`cyg_csv_refresher_2026`) | scheduled | Custom | Currency maintenance | FS-TRN-CERT-03 | OQ-REFRESHER-CRON-01 |
| DS-TRN-CERT-04 | Certification export (`cyg_cert_export`) | inspector format | Custom | Inspection-readiness | FS-TRN-CERT-04 | OQ-CERT-EXPORT-01 |

### 4.9 Multi-Site Federation CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-FED-01 | Federation rules file (`cyg_fed_rules.yaml`) | Konstanz authoritative for templates; site-local for project execution | Custom | Per-entity authority | FS-FED-01 | OQ-FED-RULES-01 |
| DS-FED-02 | Project-transfer workflow (`wf_fed_project_transfer`) | Multi-Site Federation Steward e-sig | Custom | Inter-site discipline | FS-FED-02 | OQ-FED-TRANSFER-01 |
| DS-FED-03 | Federation lag metric (`vlm_fed_lag_seconds`) | alert at 600 s | Custom | Observability | FS-FED-03 | OQ-FED-LAG-01 |

### 4.10 Audit Trail CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUD-01 | Audit-trail coverage | document lifecycle, executions, deviations, configuration, signatures | Default | Native trail | FS-AUD-01 | OQ-AUDIT-COVERAGE-01 |
| DS-AUD-02 | Append-only enforcement | DB-layer; tenant-admin cannot UPDATE/DELETE | Custom | Tamper-protection | FS-AUD-02 | OQ-AUDIT-APPEND-01 |
| DS-AUD-03 | Review cadence | monthly Validation Ops + quarterly QA | Custom | Annex 11 § 9 | FS-AUD-03 | OQ-AUDIT-REVIEW-01 |
| DS-AUD-04 | Retention | life-of-system + ≥ 25 y; deletion blocked | Custom | EU GMP Ch. 4 | FS-AUD-04 | IQ-AUDIT-RET-01 |
| DS-AUD-05 | Focused review tool (`CYG-AUD-FOCUSED`) | signatures / deviations / config changes / RTM exemptions | Custom | Reviewer efficiency | FS-AUD-05 | OQ-AUDIT-FOCUSED-01 |

### 4.11 21 CFR Part 11 CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PART11-01 | Procedural-control SOP (`CYG-SOP-CSV-01`) | reviewed annually | Custom | § 11.10(a) | FS-PART11-01 | OQ-SOP-LINK-01 |
| DS-PART11-02 | Access controls | Okta SAML 2.0 + MFA; service accounts via mTLS only | Custom | § 11.10(d) | FS-PART11-02 | OQ-ACCESS-01 |
| DS-PART11-03 | Operational audit trail | via FS-AUD-01 | Default | § 11.10(e) | FS-PART11-03 | OQ-OPS-AT-01 |
| DS-PART11-04 | E-sig manifestation | `printedName + dateTime + meaning`; DB-schema-enforced | Custom | § 11.50 | FS-PART11-04 | OQ-SIG-MANIFEST-01 |
| DS-PART11-05 | Signature binding | HMAC-SHA256 over record-hash + signer-id + ts | Default | § 11.70 | FS-PART11-05 | OQ-SIG-BINDING-01 |
| DS-PART11-06 | Re-auth at signing | fresh OAuth2 token max-age 5 min; cached creds rejected | Custom | § 11.200 | FS-PART11-06 | OQ-SIG-REAUTH-01 |
| DS-PART11-07 | Password policy | per site InfoSec | Custom | § 11.300 | FS-PART11-07 | OQ-PWD-POLICY-01 |

### 4.12 Data Integrity CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-DI-01 | `actor_id` not-null | DB constraint | Default | Attributable | FS-DI-01 | OQ-DI-ACTOR-01 |
| DS-DI-02 | PDF/A-3 + JSON/XML export | OQ-validated | Custom | Legible | FS-DI-02 | OQ-DI-EXPORT-01 |
| DS-DI-03 | NTP-sync + retroactive-flagged | server-side | Custom | Contemporaneous | FS-DI-03 | OQ-DI-NTP-01 |
| DS-DI-04 | Immutable storage for raw inputs | derivatives reference | Default | Original | FS-DI-04 | OQ-DI-IMMUT-01 |
| DS-DI-05 | Calculation determinism OQ | floating-point reproducibility verified | Custom | Accurate | FS-DI-05 | OQ-DI-CALC-DETERMINISM-01 |
| DS-DI-06 | Retrieval ≤ 1 BD | chronological order DB-enforced | Custom | Available | FS-DI-06 | PQ-DI-RETRIEVE-01 |

### 4.13 Integration CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-INT-VAULT-01 | Vault URN resolver | bidirectional REST | Custom | Doc-binding | FS-INT-VAULT-01 | OQ-VAULT-RESOLVE-01 |
| DS-INT-EQMS-01 | MasterControl deviation push | audit propagation | Custom | Deviation discipline | FS-INT-EQMS-01 | OQ-EQMS-DEV-01 |
| DS-INT-PORT-01 | App Portfolio sync | inventory + criticality + owner | Custom | System-inventory binding | FS-INT-PORT-01 | OQ-PORTFOLIO-01 |
| DS-INT-GIT-01 | GitLab release-link (`cyg_gitlab_link_check`) | tag / commit URN; broken-link check | Custom | Release-linked validation | FS-INT-GIT-01 | OQ-GITLAB-LINK-01 |
| DS-INT-SSO-01 | Okta SAML 2.0 + MFA | per realm | Custom | Site IdP | FS-INT-SSO-01 | OQ-OKTA-SAML-01 |

### 4.14 Performance / Availability CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PERF-01 | Document open + edit P95 | ≤ 3 s | Default | UX target | FS-PERF-01 | PQ-PERF-DOC-01 |
| DS-PERF-02 | Concurrent executors target | ≥ 500 peak | Custom | Campaign-scale | FS-PERF-02 | PQ-PERF-500CU-01 |
| DS-PERF-03 | Offline-handheld sync target | ≤ 60 s for 50-step execution | Custom | Mobile UX | FS-PERF-03 | PQ-OFFLINE-SYNC-01 |
| DS-AV-01 | Availability target | ≥ 99.5%; 7-day-advance maintenance window | Default | Vendor SLA | FS-AV-01 | OQ-AV-SLA-01 |

### 4.15 Backup / Security CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-BAK-01 | Vendor-managed backup | daily integrity verification; RPO ≤ 4 h / RTO ≤ 24 h | Custom | Vendor-assurance | FS-BAK-01 | PQ-BAK-VERIFY-01 |
| DS-BAK-02 | Site tenant-data export | life-of-system + ≥ 25 y cold storage | Custom | Long-term archive | FS-BAK-02 | OQ-COLD-STORAGE-01 |
| DS-SEC-01 | TLS 1.3 + AES-256 | enforced | Custom | InfoSec | FS-SEC-01 | OQ-TLS-AES-01 |
| DS-SEC-02 | RBAC review quarterly | quarterly cadence | Custom | RBAC hygiene | FS-SEC-02 | OQ-RBAC-REVIEW-01 |
| DS-SEC-03 | Annual pen-test | findings remediated under CR | Custom | Independent assurance | FS-SEC-03 | OQ-PENTEST-01 |

### 4.16 Training / Periodic Review CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-TRN-01 | Risk-Classifier advanced curriculum | FDA CSA + ICH Q9(R1) | Custom | Critical-role training | FS-TRN-01 | OQ-RISK-CLASSIFIER-TRN-01 |
| DS-TRN-02 | Annual refresher (`VLM-2026-ANNUAL`) | GAMP 5 + FDA CSA updates | Custom | Currency | FS-TRN-02 | PQ-ANNUAL-REFRESHER-01 |
| DS-PR-01 | Annual periodic-review | Director Validation Ops + VP QA + VP IT Compliance sign-off | Custom | Annex 11 § 11 | FS-PR-01 | PQ-PR-VLM-01 |

### 4.17 Cross-System Bindings (M-XSYS / M-XINT)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-XSYS-AD-01 | Entra ID SAML 2.0 + SCIM | conditional-access `Quality-App Conditional Access (MFA + device-compliance for validation e-signature)` | Custom | Per FS-XSYS-AD-01 | FS-XSYS-AD-01 | OQ-XSYS-AD-01 |
| DS-XSYS-AD-02 | SIEM (`Splunk gxp-authn`) | RFC 5424 ≤ 5 min lag | Custom | Cross-system correlation | FS-XSYS-AD-01 | OQ-SIEM-FWD-01 |
| DS-XSYS-AD-03 | CyberArk PAM binding | 24 h rotation + dual-witness check-out | Custom | Break-glass | FS-XSYS-AD-01 | OQ-PAM-01 |
| DS-XSYS-BAK-01 | Veeam VSS + MS SQL Server | T1 tier; RPO ≤ 4 h / RTO ≤ 4 BH | Custom | Per FS-XSYS-BAK-01 | FS-XSYS-BAK-01 | OQ-VEEAM-01 |
| DS-XSYS-BAK-02 | S3 Object Lock COMPLIANCE bucket | geo-replicated | Custom | Anti-ransom | FS-XSYS-BAK-01 | IQ-S3-OBJLOCK-01 |
| DS-XSYS-BAK-03 | LTO-9 air-gap rotation | monthly | Custom | Air-gap policy | FS-XSYS-BAK-01 | OQ-LTO9-01 |
| DS-XSYS-BAK-04 | Restore-cert retention | ≥ 25 y in eQMS | Custom | Quality-record discipline | FS-XSYS-BAK-01 | OQ-RESTORE-CERT-01 |
| DS-XINT-HEL-01 | Helios Kafka topic (`helios.ingest.cygnus.valgenesis.v1`) | idempotency `{source_system, event_id}` | Custom | Per FS-XINT-HEL-01 | FS-XINT-HEL-01 | OQ-HELIOS-PUB-01 |
| DS-XINT-HEL-02 | Helios lag alert (`HELIOS_LAG_ALERT_S=600`) | Prometheus | Custom | Back-pressure SLO | FS-XINT-HEL-01 | OQ-HELIOS-LAG-01 |
| DS-XINT-HEL-03 | Helios reconciliation cadence | daily 24 h window | Custom | Parity | FS-XINT-HEL-02 | OQ-HELIOS-RECON-01 |
| DS-XINT-EQMS-01 | CAPA endpoint (`POST /capa/tickets`) | mTLS + Entra workload-identity; payload `eqms.ticket.v1`; OpenAPI `xint-eqms.openapi.yaml`; exp back-off + DLQ at 5 | Custom | Per FS-XINT-EQMS-01 | FS-XINT-EQMS-01 | OQ-CAPA-EP-01 |
| DS-XINT-EQMS-02 | eQMS status webhook | `eqms.status.v1`; maps `(OPEN, IN-PROGRESS, EFFECTIVENESS, CLOSED)` onto disposition; closed-loop gate prevents disposition without `eqms_status=CLOSED` | Custom | Per FS-XINT-EQMS-02 | FS-XINT-EQMS-02 | OQ-EQMS-STATUS-01 |

---

## 5. Workflow + Business-Rule Design

### 5.1 Document lifecycle workflow

| Step | State | Actor | Gate |
|---|---|---|---|
| 1 | `DRAFT` | Doc Author | content drafted |
| 2 | `REVIEW` | Doc Reviewer | content review |
| 3 | `APPROVED` | Doc Approver (≠ Author) | re-auth e-sig |
| 4 | `EFFECTIVE` | system | typed-link integrity verified |
| 5 | `OBSOLETE` | system | retention applies |

### 5.2 FDA CSA risk-classification business rule

For each system at project start:
1. User selects intended-use category + production criticality + quality-system criticality
2. Engine computes testing-depth tier = `f(production_crit, qs_crit, intended_use)` per CSA matrix
3. User provides ICH Q9(R1) critical-thinking justification (≥ 200 chars)
4. Engine declares GAMP category (1/3/4/5) → drives default protocol structure
5. If intended-use changes downstream → reclassification trigger fires + downstream re-test flags

### 5.3 Execution + sync workflow (handheld + offline)

| Step | Actor | Gate |
|---|---|---|
| 1 | Executor | check out execution to handheld; offline mode optional |
| 2 | Executor | step-by-step capture (web/handheld); evidence attached + SHA-256 hashed |
| 3 | Witness | per-step witness signature where required |
| 4 | Sync (online → cloud) | `wf_sync_execution`; conflicts → `cyg_sync_conflicts` queue |
| 5 | Project Lead | conflict resolution; chosen value e-signed |
| 6 | DB | execution.locked = true after completion; immutable; corrections via `wf_amend_execution` |

### 5.4 Deviation lifecycle (per execution)

| Step | Actor | Gate |
|---|---|---|
| 1 | Executor | flags step-deviation; severity tagged |
| 2 | System | pushes to MasterControl via `IF-EQMS-DEV` (idempotency `vlm:exec:<id>:step:<n>`); failure blocks finalisation |
| 3 | Project Lead | dispositions (`continue with risk acceptance` / `re-test` / `escalate`) |
| 4 | VSR | auto-summary table populated |

### 5.5 RTM completeness business rule

At VSR sign-off:
- Compute `rtm = traceability_graph(URS, FS, CS, DS, IQ, OQ, PQ)`
- Identify orphan URS items (not covered)
- For each orphan: must have `test-not-required` flag w/ documented risk justification, OR addressed in VSR
- Otherwise: sign-off blocked

---

## 6. Role-Permission Matrix Design

| Role | Doc-Author | Doc-Approver | Risk-Classifier | Project-Lead | Executor | Witness | Federation-Steward | Config-Author | Config-Approver | Audit-Reviewer |
|---|---|---|---|---|---|---|---|---|---|---|
| `Doc-Author` | R/W | – | – | – | – | – | – | – | – | – |
| `Doc-Approver` | R | R/W | – | – | – | – | – | – | – | – |
| `Risk-Classifier` | – | – | R/W | – | – | – | – | – | – | – |
| `Project-Lead` | R | – | R | R/W | – | – | – | – | – | – |
| `Executor` | – | – | – | – | R/W | – | – | – | – | – |
| `Witness` | – | – | – | – | R | R/W | – | – | – | – |
| `Multi-Site-Federation-Steward` | R | – | – | – | – | – | R/W | – | – | – |
| `Config-Author` | – | – | – | – | – | – | – | R/W | – | – |
| `Config-Approver` | – | – | – | – | – | – | – | R | R/W | – |
| `Audit-Reviewer` | R | R | R | R | R | R | R | R | R | R/W |
| `QP-CSA-Liaison` | R | R | R | R | – | – | – | – | – | R |

SoD: `Doc-Author ∩ Doc-Approver = ∅`; `Risk-Classifier ∩ Project-Lead = ∅`; `Executor ∩ Witness = ∅` per step; `Config-Author ∩ Config-Approver = ∅`.

---

## 7. Integration Design

### 7.1 Vault QualityDocs URN resolver (FS-INT-VAULT-01)

- Endpoint: bidirectional REST `https://vault.vellis.local/api/v23.3/objects/documents__v/{urn}`
- AuthN: mTLS + bearer
- Use: doc-binding for protocol references + RTM-link validation

### 7.2 MasterControl deviation push (FS-INT-EQMS-01)

- Endpoint: `POST https://eqms.talos.local/api/v2/deviations`
- AuthN: mTLS + bearer
- Idempotency: `vlm:exec:<id>:step:<n>`
- Retry: exponential back-off; DLQ at 5

### 7.3 Application Portfolio sync (FS-INT-PORT-01)

- Endpoint: scheduled REST `GET https://portfolio.cygnus.local/api/v1/systems`
- AuthN: mTLS + bearer
- Sync cadence: daily; inventory + criticality + owner pulled

### 7.4 GitLab release-link check (FS-INT-GIT-01)

- Endpoint: `GET https://gitlab.cygnus.local/api/v4/projects/{id}/repository/tags/{tag}`
- AuthN: GitLab PAT (rotated 90 d)
- Use: broken-link check at sign-off via `cyg_gitlab_link_check`

### 7.5 Okta SSO + MFA (FS-INT-SSO-01)

- Protocol: SAML 2.0 + SCIM 2.0
- MFA: TOTP / WebAuthn at every sig event
- Re-auth max-age: 300 s

### 7.6 CAPA endpoint to MasterControl (FS-XINT-EQMS-01)

- Endpoint: `POST https://eqms.talos.local/capa/tickets`
- AuthN: mTLS + Entra workload-identity
- Payload schema: `eqms.ticket.v1`; OpenAPI artefact `xint-eqms.openapi.yaml`
- Retry: exponential back-off; DLQ at 5 attempts

### 7.7 eQMS status webhook (FS-XINT-EQMS-02)

- Inbound webhook from MasterControl: `POST /api/v1/vlm/eqms-status`
- Payload: `eqms.status.v1`
- Closed-loop gate: VLM disposition cannot CLOSE without `eqms_status=CLOSED`

### 7.8 Helios audit-event handover (FS-XINT-HEL-01..02)

- Kafka topic: `helios.ingest.cygnus.valgenesis.v1`
- Schema-registry pinned envelope; at-least-once delivery
- Reconciliation: daily 24 h window

---

## 8. Site-Deployed Components Design

ValGenesis VLM 5.x is operated as a pure Cat 4 SaaS at Cygnus — no site-developed code is in scope. The `ValGenesis Mobile 5.x` handheld app is vendor-supplied. All integration adapters (Vault, eQMS, App Portfolio, GitLab) are realised through ValGenesis native REST connectors plus vendor-managed federation service. No § 8 mini-SDS sub-sections are required for v1.0.

---

## 9. References

### US
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EU GMP Chapter 4

### DACH
- BfArM (DE) Anlage 7
- Swissmedic (CH)
- AGES (AT)

### International
- ICH Q9(R1); ICH Q10
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE GAMP GPGs *Risk-Based Approach* + *Records & Data Integrity*
- ISPE *Validation Master Plan Guide*
- PIC/S PI 041
- ISO/IEC 27001:2022

### Vendor
- ValGenesis — *VLM 5.x Validation Approach + Customer-Shared CSV Summary*
- ValGenesis — *VLM Mobile 5.x Reference*
- ValGenesis — *VLM Federation 5.x Administrator Guide*

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-VND-01 | FS-VND-01 |
| DS-VND-02 | FS-VND-02 |
| DS-VND-03 | FS-VND-03 |
| DS-CFG-01 | FS-CFG-01 |
| DS-CFG-02 | FS-CFG-02 |
| DS-DOC-01 | FS-DOC-01 |
| DS-DOC-02 | FS-DOC-01 |
| DS-DOC-03 | FS-DOC-02 |
| DS-DOC-04 | FS-DOC-03 |
| DS-DOC-05 | FS-DOC-04 |
| DS-AUTH-01 | FS-AUTH-01 |
| DS-AUTH-02 | FS-AUTH-02 |
| DS-AUTH-03 | FS-AUTH-03 |
| DS-AUTH-04 | FS-AUTH-04 |
| DS-AUTH-05 | FS-AUTH-05 |
| DS-AUTH-06 | FS-AUTH-06 |
| DS-AUTH-07 | FS-AUTH-07 |
| DS-RBT-01 | FS-RBT-01 |
| DS-RBT-02 | FS-RBT-02 |
| DS-RBT-03 | FS-RBT-03 |
| DS-RBT-04 | FS-RBT-04 |
| DS-RBT-05 | FS-RBT-05 |
| DS-EXE-01 | FS-EXE-01 |
| DS-EXE-02 | FS-EXE-02 |
| DS-EXE-03 | FS-EXE-03 |
| DS-EXE-04 | FS-EXE-04 |
| DS-EXE-05 | FS-EXE-05 |
| DS-EXE-06 | FS-EXE-06 |
| DS-EXE-07 | FS-EXE-07 |
| DS-EXE-08 | FS-EXE-08 |
| DS-DEV-01 | FS-DEV-01 |
| DS-DEV-02 | FS-DEV-02 |
| DS-DEV-03 | FS-DEV-03 |
| DS-DEV-04 | FS-DEV-04 |
| DS-RTM-01 | FS-RTM-01 |
| DS-RTM-02 | FS-RTM-02 |
| DS-RTM-03 | FS-RTM-03 |
| DS-RTM-04 | FS-RTM-04 |
| DS-TRN-CERT-01 | FS-TRN-CERT-01 |
| DS-TRN-CERT-02 | FS-TRN-CERT-02 |
| DS-TRN-CERT-03 | FS-TRN-CERT-03 |
| DS-TRN-CERT-04 | FS-TRN-CERT-04 |
| DS-FED-01 | FS-FED-01 |
| DS-FED-02 | FS-FED-02 |
| DS-FED-03 | FS-FED-03 |
| DS-AUD-01 | FS-AUD-01 |
| DS-AUD-02 | FS-AUD-02 |
| DS-AUD-03 | FS-AUD-03 |
| DS-AUD-04 | FS-AUD-04 |
| DS-AUD-05 | FS-AUD-05 |
| DS-PART11-01 | FS-PART11-01 |
| DS-PART11-02 | FS-PART11-02 |
| DS-PART11-03 | FS-PART11-03 |
| DS-PART11-04 | FS-PART11-04 |
| DS-PART11-05 | FS-PART11-05 |
| DS-PART11-06 | FS-PART11-06 |
| DS-PART11-07 | FS-PART11-07 |
| DS-DI-01 | FS-DI-01 |
| DS-DI-02 | FS-DI-02 |
| DS-DI-03 | FS-DI-03 |
| DS-DI-04 | FS-DI-04 |
| DS-DI-05 | FS-DI-05 |
| DS-DI-06 | FS-DI-06 |
| DS-INT-VAULT-01 | FS-INT-VAULT-01 |
| DS-INT-EQMS-01 | FS-INT-EQMS-01 |
| DS-INT-PORT-01 | FS-INT-PORT-01 |
| DS-INT-GIT-01 | FS-INT-GIT-01 |
| DS-INT-SSO-01 | FS-INT-SSO-01 |
| DS-PERF-01 | FS-PERF-01 |
| DS-PERF-02 | FS-PERF-02 |
| DS-PERF-03 | FS-PERF-03 |
| DS-AV-01 | FS-AV-01 |
| DS-BAK-01 | FS-BAK-01 |
| DS-BAK-02 | FS-BAK-02 |
| DS-SEC-01 | FS-SEC-01 |
| DS-SEC-02 | FS-SEC-02 |
| DS-SEC-03 | FS-SEC-03 |
| DS-TRN-01 | FS-TRN-01 |
| DS-TRN-02 | FS-TRN-02 |
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
| DS-XINT-EQMS-01 | FS-XINT-EQMS-01 |
| DS-XINT-EQMS-02 | FS-XINT-EQMS-02 |

---

## 11. Design-level Risk Register

| ID | Design-level risk | Origin (DS-ID / design choice) | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|---|
| DR-01 | Orphan URS at VSR sign-off slips through completeness gate | DS-RTM-02 | Medium | High | OQ on synthetic orphan injection |
| DR-02 | Execution-record tampering at DB layer | DS-EXE-03 + DS-AUD-02 | Low | Critical | DBA dual-control + audit-trail review |
| DR-03 | Deviation bypass — execution continues without disposition | DS-EXE-02 + DS-DEV-02 | Medium | High | Idempotent push + finalisation block on failure |
| DR-04 | Audit-trail tampering by tenant admin | DS-AUD-02 | Low | Critical | Vendor-assurance dependency + quarterly review |
| DR-05 | FDA CSA risk misclassification — system tested too lightly | DS-RBT-01 + DS-RBT-04 | Medium | Critical | Critical-thinking justification + Risk-Classifier role training |
| DR-06 | Vendor outage during validation campaign | DS-AV-01 + DS-BAK-01 | Low | High | DR runbook + vendor SLA monitoring |
| DR-07 | Risk Classifier ∩ Project Lead role overlap | Role matrix § 6 | Low | High | SoD: `Risk-Classifier ∩ Project-Lead = ∅` |
| DR-08 | Evidence-attachment hash mismatch on archive retrieval | DS-EXE-04 | Low | High | Hash-verify on upload + archive; alert via `cyg_evidence_hash_check` |
| DR-09 | Template drift across projects — inconsistent validation depth | DS-DOC-03 | Medium | Medium | Template registry + promotion workflow (DS-AUTH-07) |
| DR-10 | RTM auto-gen defect produces false-complete RTM | DS-RTM-01 | Low | High | Broken-link flagging + OQ-RTM-AUTOGEN-01 |
| DR-11 | Vendor SaaS schema change breaks integrations | DS-VND-02 | Low | Medium | Release-eval runbook + contract test |
| DR-12 | EU GMP Annex 11 § 11 periodic-review evidence gap | DS-PR-01 | Medium | Medium | Annual cron + dashboard surfacing |
| DR-13 | Offline-handheld sync conflict losing execution data | DS-EXE-07 | Low | Critical | Conflict-resolution queue + Project Lead review |
| DR-14 | Federation drift causing template version skew across 5 sites | DS-FED-01 + DS-FED-03 | Medium | High | Lag metric + alert at 600 s + degraded-mode runbook |
| DR-15 | GitLab release link breaks (renamed branch / deleted tag) | DS-INT-GIT-01 | Low | Medium | Broken-link check at sign-off |
| DR-16 | Certification expired but role still active | DS-TRN-CERT-02 | Low | High | Certification gate at project-role assignment |
| DR-17 | Biometric handheld e-sig bypass via shared device | DS-EXE-08 | Low | High | Biometric bound to Okta identity + fresh-token requirement |
| DR-18 | CAPA closed-loop gate failure — disposition before eQMS CLOSED | DS-XINT-EQMS-02 | Low | High | Webhook status reconciliation + manual unblock workflow |
| DR-19 | Helios audit-event reconciliation false-positive (network jitter) | DS-XINT-HEL-03 | Medium | Low | Tunable threshold + deviation suppression review |
| DR-20 | Multi-site project-transfer ownership ambiguity (Konstanz vs site-local) | DS-FED-02 | Medium | Medium | Federation Steward e-sig at transfer + clear authority rules |
| DR-21 | Reclassification trigger silently drops downstream re-test flags | DS-RBT-04 | Low | Critical | Change-impact dashboard + downstream OQ trigger test |
| DR-22 | Test-step deviation severity mis-tagged → wrong routing distribution | DS-DEV-03 | Medium | Medium | Severity-tagging UAT + audit-trail review |

The full formal Risk Assessment is `CYG-RA-VLM-001` (synthetic, separate document).

---

## 12. Appendix B — FDA CSA (Feb 2026) + Multi-Site Federation Design Narrative

### 12.1 Why FDA CSA changes the validation-system design

FDA Computer Software Assurance (final guidance, February 2026, supersedes the September 2025 draft) shifts the orientation of computerised-system validation from documentation-volume-driven to risk-based-testing-driven. The validation-system platform itself (ValGenesis VLM 5.x at Cygnus) must therefore be configured to *encourage* critical-thinking-justified testing depth rather than enforce a uniform high-volume regime. This appendix documents how the design choices in §§ 4–7 implement that orientation without losing GxP rigour.

### 12.2 Risk-classification matrix design

| Dimension | Values | Source |
|---|---|---|
| Production criticality | High / Medium / Low | per-system declared at project init |
| Quality-system criticality | High / Medium / Low | per-system declared |
| Intended-use category | direct-record-of-GxP / supporting-GxP / non-GxP | per-system declared |
| Testing-depth tier | T1-Lean / T2-Standard / T3-Full | engine output |

The engine output is deterministic: given the same three input declarations, the same tier results. Critical-thinking justification (DS-RBT-02, ≥ 200 chars with ICH Q9(R1) categorisation) is captured but does not override the engine — it documents why the inputs were declared as they were.

### 12.3 Critical-thinking justification — what good looks like

A short or generic justification ("standard system, standard validation") is a smell that the FDA CSA spirit is being missed. The Risk Classifier role is trained (per DS-TRN-01) to write justifications that:
1. Name the highest-likelihood failure mode
2. Cite the data-integrity impact of that failure
3. Reference ICH Q9(R1) risk category (severity × probability × detectability)
4. Conclude with the testing-depth implication

Sample acceptable justification (≥ 200 chars, GMP-relevant): *"System ingests batch-genealogy data from PAS-X for QA review; highest-likelihood failure mode is silent message-loss leading to genealogy gap; data-integrity impact is loss of `Complete` per ALCOA+; Q9(R1) severity = High, probability = Low, detectability = Medium (caught at quarterly reconciliation, not in real time); RPN moderate, drives T2-Standard with focus on integration testing and reconciliation OQ."*

### 12.4 Reclassification trigger logic

When a system's `intended_use` field changes (e.g., from supporting-GxP to direct-record-of-GxP):
1. Engine re-evaluates testing-depth tier
2. If new tier > old tier: open re-testing tickets for downstream OQ scripts
3. Audit-trail entry written with old + new tier + reason
4. Project Lead notified

This is the design control against silent scope-creep. A system that gradually accumulates GxP responsibility without re-classification is the kind of validation gap that CSA is specifically designed to prevent.

### 12.5 Multi-site federation routing — why Konstanz is authoritative

The federation rule file `cyg_fed_rules.yaml` declares Konstanz authoritative for **templates** (per-module: FS, CS, DS, IQ, OQ, PQ, VSR, VMP) and site-local for **project execution**. Rationale:

- Templates are stable, slow-moving, and need consistent regulator-readable structure across all 5 sites → centralised authority avoids drift
- Project execution is fast-moving, site-context-rich, and must respect local time zones / personnel / instruments → site-local authority avoids cross-site latency

The federation peer hierarchy is therefore:

```
                      Konstanz (templates authoritative)
                              │
            ┌─────────┬─────────┼─────────┬─────────┐
            ▼         ▼         ▼         ▼         ▼
         Basel     Vienna    Boston    Singapore
       (project   (project  (project   (project
        local)     local)    local)     local)
```

### 12.6 Federation outage handling

When `vlm_fed_lag_seconds > 600`, the alert fires; degraded-mode runbook (`CYG-RB-FED-DEGRADED`) gives sites read-only access to last-known-good template versions and queues project-execution writes for retry-on-recovery. The design choice is: **never proceed with a project execution against unknown-template-version**; sites halt or use the last-known-good with explicit acknowledgement.

### 12.7 Handheld + offline execution design

The `ValGenesis Mobile 5.x` handheld app supports in-room execution with offline mode. Design choices:

| Concern | Choice |
|---|---|
| Offline storage | Encrypted local DB; 24 h forced-sync window (CI-07) |
| Conflict resolution | `cyg_sync_conflicts` queue surfaces conflicts to Project Lead |
| E-sig on handheld | Fresh Okta token (5-min max-age) + biometric (FaceID / TouchID) bound to Okta identity (DS-EXE-08) |
| Device-loss risk | Device encryption + remote-wipe via MDM + 24 h forced-sync prevents stale offline state |
| Network-recovery sync | Idempotent; same step-edit replayed produces same outcome |

### 12.8 Evidence-hash design (SHA-256)

Every evidence attachment is SHA-256-hashed on upload (DS-EXE-04). The hash is stored alongside the attachment metadata and verified again at archive read. Tamper alert fires via `cyg_evidence_hash_check`. SHA-256 is sufficient at corpus scale; SHA-3 fallback available if cryptographic guidance shifts.

### 12.9 CSV training + certification gate

A project-role assignment is denied if the user's CSV certification has expired (DS-TRN-CERT-02). The default expiry is 12 months (CI-10). Annual refresher (DS-TRN-CERT-03) runs on cron `cyg_csv_refresher_2026`. The design choice is to gate at *assignment* rather than at *execution* — preventing the assignment is cleaner than blocking an in-progress execution because the executor's certification lapsed mid-protocol.

### 12.10 RTM completeness vs CSA risk-justified exemption

Per FDA CSA, not every requirement requires a test — risk-justified exemptions are explicitly allowed. The design choice is to make this explicit:

- An RTM row with `test-not-required` flag + documented justification ≥ 200 chars passes the completeness gate
- An RTM row with no test reference and no `test-not-required` flag fails the gate
- An RTM row with both a test reference and a `test-not-required` flag → error (inconsistent state)

The VSR template includes the count of risk-justified exemptions and the percentage of total requirements; this surfaces to reviewers as a sanity check that exemption use is proportionate, not abusive.

### 12.11 GitLab release-linked validation — design intent

Validation against software that ships via GitLab tags + commits is the modern reality for many GMP systems. The `cyg_gitlab_link_check` rule (DS-INT-GIT-01) verifies at sign-off that the GitLab tag / commit URN referenced in the validation package still resolves and matches the expected SHA. Broken-link failure modes:

| Failure | Cause | Handling |
|---|---|---|
| Tag deleted | repository garbage-collected | block sign-off; require new tag + re-evidence |
| Branch renamed | git history rewritten | block sign-off; require resolved URN |
| Commit SHA missing | force-push or branch deletion | block sign-off; surface to Regulatory Affairs Lead |
| GitLab unreachable | network / vendor outage | retry queue; manual override w/ Reg-Affairs sign-off |

### 12.12 Annex 11 § 11 periodic-review evidence design

The annual periodic-review template captures all the dimensions Annex 11 § 11 expects: configuration drift (vs baseline export), audit-trail evidence (via `CYG-AUD-FOCUSED` summaries), vendor-assurance status (SOC 2 / ISO 27001 currency), integration health (counterparty up/down + latency), training currency (LMS pull), certification expiry summary (CSV registry).

Sign-off requires three signatures: Director Validation Operations + VP QA + VP IT Compliance (DS-PR-01). The three-signature gate reflects the cross-functional nature of an Annex 11 § 11 review — operational, quality, and IT-governance perspectives must all converge before the period closes.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
