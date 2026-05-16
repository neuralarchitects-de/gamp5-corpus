---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "BLR-FS-VSUB-001 v1.3 (parent FS)"
  - "BLR-URS-VSUB-001 v1.3 (parent URS, transitive)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 Configuration Specification conventions"
  - "21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300"
  - "ICH M2 ESTRI; ICH M4 CTD; ICH M8 eCTD"
  - "FDA eCTD + ESG; FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026; supersedes the September 2025 guidance)"
  - "FDA Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions (Aug 2025)"
  - "EMA eCTD v4 + CESP; EMA SPOR; PMDA Gateway; Health Canada CESG; MHRA UK; Swissmedic; ANVISA; NMPA"
  - "IDMP ISO 11238/11239/11240/11615/11616"
  - "Veeva Vault Submissions + Submissions Publishing 24R3 + Submissions Archive"
  - "LORENZ eValidator + docuBridge"
parent_fs:
  document_number: BLR-FS-VSUB-001
  version: 1.3
  file: ../../../FS_FDS/_generated/final/Bellerophon_Pharma_Vault_Submissions_FS_v1.3.md
parent_urs:
  document_number: BLR-URS-VSUB-001
  version: 1.3
  file: ../../../URS/_generated/final/Veeva_Vault_Submissions__Bellerophon_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Regulatory Submissions Platform — Veeva Vault Submissions + Submissions Publishing 24R3 + Submissions Archive — Configuration Specification

**Document Number:** BLR-DS-VSUB-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Parent FS:** BLR-FS-VSUB-001 v1.3
**Parent URS:** BLR-URS-VSUB-001 v1.3 *(informational; transitive via FS)*
**Site:** Bellerophon Pharma plc *(fictional)* — London HQ + Basel + München + Wien + Tokyo + São Paulo + Shanghai hubs
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Project Mode:** Sustaining + Configurable Change *(inherited from parent URS)*
**Regulatory Scope:** 21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300; ICH M2 + M4 + M8; FDA eCTD + ESG; FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance); FDA *Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions* (Aug 2025); EMA eCTD v4 + CESP; PMDA Gateway; Health Canada CESG; MHRA UK; Swissmedic; ANVISA (BR); NMPA (CN); IDMP ISO 11238/11239/11240/11615/11616; EU CTR 536/2014 Arts. 25/81; EU GMP Annex 11; GDPR Arts. 6, 17, 32; ISO/IEC 27001:2022; PIC/S PI 041.

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QA Reviewer) | _____________ | _____________ | _____ |
| Reviewer (System Owner — Director Regulatory Operations) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — VP Global Regulatory Affairs) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (Publishing Manager) | _____________ | _____________ | _____ |
| Reviewer (IDMP / xEVMPD Steward) | _____________ | _____________ | _____ |
| Reviewer (Translation Manager) | _____________ | _____________ | _____ |
| Approver (VP Global Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Design Control

| Field | Value |
|---|---|
| Document Number | BLR-DS-VSUB-001 |
| Version | 1.1 |
| Effective Date *(synthetic)* | 2026-05-15 |
| Parent FS | BLR-FS-VSUB-001 v1.3 |
| Parent URS *(informational)* | BLR-URS-VSUB-001 v1.3 |
| Site | Bellerophon Pharma plc *(fictional)* — London HQ + Basel + München + Wien + Tokyo + São Paulo + Shanghai hubs |
| System Class (GAMP 5, 2nd ed.) | Category 4 — Configured Product (multi-tenant SaaS) |
| Project Mode | Sustaining + Configurable Change |
| Regulatory Scope | per Title block |
| Tier | T4 (inherited from parent URS+FS pair) |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue of Configuration Specification for Veeva Vault Submissions + Submissions Publishing 24R3 + Submissions Archive corresponding to BLR-FS-VSUB-001 v1.3. Inherited Tier T4 from parent URS+FS pair. DS covers 152/152 FS-IDs (100% coverage). Vendor-internal Veeva Vault platform internals + LORENZ docuBridge internals are flagged as **vendor-internal — no site design surface**. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from BLR-URS-VSUB-001 v1.3 and BLR-FS-VSUB-001 v1.3. DS-specific additions:

| Term | Definition |
|---|---|
| eCTD | electronic Common Technical Document |
| ESG | FDA Electronic Submissions Gateway |
| CESP | EMA Common European Submission Platform |
| CESG | Health Canada Common Electronic Submissions Gateway |
| SPL | Structured Product Labeling (HL7 SPL) |
| LoA | Letter of Authorization |
| DMF | Drug Master File |
| RWE / RWD | Real-World Evidence / Real-World Data |
| PFDD | Patient-Focused Drug Development |
| Hydra | Bellerophon's enterprise LLM gateway |
| Helios | Bellerophon's enterprise audit-event bus |

---

## 1. Purpose

This Configuration Specification defines, at the platform-tenancy level, the configuration values, lifecycle state-machine design, workflow + signature designs, role-permission matrix, and integration endpoint designs that implement BLR-FS-VSUB-001 v1.3 for the Bellerophon Vault Submissions + Submissions Publishing 24R3 + Submissions Archive tenancy. It is the third document in the GAMP 5 V-model.

## 2. Scope

### 2.1 In Scope

- Vault Submissions + Submissions Publishing 24R3 + Submissions Archive tenancy configuration.
- Per-product configuration design (DEV → QC → UAT → PROD pattern with SoD).
- eCTD build (ICH M8 v3.2.2 / v4.0) + per-region Module 1 templates (US FDA, EU, JP, CA, UK MHRA, CH Swissmedic, BR ANVISA, CN NMPA).
- LORENZ eValidator + docuBridge integration.
- Granularity + Style + Cross-ref + Diff design.
- IDMP / xEVMPD product master + SPOR sync.
- Multi-country variation + Translation lifecycle.
- Combination-product routing (FDA CDER / CBER / CDRH).
- Application Lifecycle tracking (initial / amendment / supplement / variation / renewal / withdrawal).
- HA Correspondence (FDA-IR, EMA D-120/D-180, PMDA queries).
- Inspection-readiness + meeting tracking.
- Cross-system planes — AD identity, AUR backup tier, Hydra LLM gateway (with AI Act Art. 11 pack enforcement), Helios audit-event bus, EDMS read adapter.

### 2.2 Out of Scope

- Per-product submission body content (per-product DS sub-documents).
- Vendor platform internals (Veeva SDLC + LORENZ SDLC).
- Cross-system AD design (QTZ-DS-AD-001).
- Cross-system backup design (AUR-DS-BACKUP-001).

## 3. Architectural Overview

The Bellerophon Vault Submissions platform is a **multi-tenant SaaS** Cat 4 system functioning as the Global Regulatory Submissions hub. It orchestrates per-product per-region eCTD build / validate / dispatch / archive across eight major HAs (FDA, EMA, PMDA, Health Canada, MHRA, Swissmedic, ANVISA, NMPA), each with its own Module 1 template + validation rule pack + gateway routing.

### 3.1 Platform Architectural Diagram

```
                Okta SAML 2.0 + MFA
                       │
                       ▼
   ┌────────────────────────────────────────────────────────────────────────┐
   │   Veeva Vault Submissions + Publishing + Archive 24R3 (Bellerophon)    │
   │                                                                        │
   │   ┌─────────────────────────────────────────────────────────────┐      │
   │   │  Submission Planning + Doc Selection (URN bind to Vellis)   │      │
   │   │  eCTD Build per ICH M8 v3.2.2 / v4.0 + region M1            │      │
   │   │  LORENZ eValidator + docuBridge (criteria pack pinned)      │      │
   │   │  Granularity + Style + Cross-ref check                       │      │
   │   │  IDMP / xEVMPD product master + EMA SPOR sync               │      │
   │   │  Multi-country variation + Translation lifecycle             │      │
   │   │  Sequence Diff + Archive (immutable + object-lock)          │      │
   │   │  SPL generator (21 CFR 314.81) + drug-listing tracker       │      │
   │   │  Meeting tracker (pre-IND / Type-B / Type-C / Pre-NDA /     │      │
   │   │  EMA scientific advice / PMDA consultation)                  │      │
   │   │  Application-lifecycle tracker (initial → amendment →       │      │
   │   │  supplement → variation → renewal → withdrawal)              │      │
   │   │  Combination-product routing (CDER / CBER / CDRH)            │      │
   │   └─────────────────────────────────────────────────────────────┘      │
   └─┬──────────────┬──────────────┬─────────────────┬─────────────────────┘
     │              │              │                 │
     ▼              ▼              ▼                 ▼
   Vault         Sirius PV     EMA SPOR          Translation
   Quality-     (Argus)        (IDMP master)     vendor REST API
   Docs +
   RIM + eTMF +
   PromoMats
     │
     ▼
   ┌────────────────────────────────────────────────────────────────────────┐
   │   Gateway Routing Layer                                                │
   │   FDA ESG (AS2 + SHA-256) │ EMA CESP (SFTP) │ PMDA Gateway │            │
   │   Health Canada CESG (AS2/WebTrader) │ MHRA UK Submissions │           │
   │   Swissmedic eGov │ ANVISA eCTD │ NMPA eCTD                            │
   └────────────────────────────────────────────────────────────────────────┘
       │
       ▼
   ┌────────────────────────────────────────────────────────────────────────────┐
   │  Cross-system planes                                                       │
   │  • QTZ AD / Entra ID (SAML+SCIM, Splunk gxp-authn, CyberArk PAM)           │
   │  • AUR Backup (Veeam + PostgreSQL pg_basebackup + WAL + object-replica +   │
   │    S3 Object Lock Compliance + LTO-9 air-gap)                              │
   │  • Hydra LLM gateway (CLIN-PROTO-DRAFT / REG-DRAFT-MOD2 / REG-DRAFT-MOD3 / │
   │    REG-DRAFT-RTI; AI Act Annex I pack enforcement)                         │
   │  • Helios audit-event bus (Kafka helios.ingest.bellerophon.{submissions,  │
   │    hydra}.v1)                                                              │
   │  • EDMS read adapter (BLR-EDMS-READ — pin doc_id + version + sha256)       │
   └────────────────────────────────────────────────────────────────────────────┘
```

### 3.2 Lifecycle State Machine (Per Document + Per Sequence)

```
   Document:
   ┌─────────┐    ┌──────────┐   ┌──────────┐   ┌─────────────────┐   ┌───────────┐   ┌────────────┐
   │  DRAFT  │───►│   QC     │──►│   UAT    │──►│      PROD       │──►│ PUBLISHED │──►│ SUPERSEDED │
   └─────────┘    └──────────┘   └──────────┘   └─────────────────┘   └───────────┘   └────────────┘

   Sequence:
   ┌──────────┐  ┌────────────┐  ┌──────────────┐  ┌────────────────┐  ┌──────────┐
   │ Planning │─►│   Build    │─►│ Validate     │─►│ Release         │─►│ Dispatch │
   └──────────┘  └────────────┘  │ (eValidator) │  │ (Sub. Approver  │  │ (gateway)│
                                 └──────────────┘  │  re-auth)       │  └──────────┘
                                                   └────────────────┘
```

---

## 4. Configuration Specification

### 4.1 Tenancy + SSO + Vendor-Assurance + Config Management

| CI-ID | Configuration item (Veeva-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-01 | Vault IdP Mode | `Okta SAML 2.0 + MFA via Entra ID` | Custom | Per FS-INT-SSO-01 + FS-PART11-04 + FS-XSYS-AD-01. | FS-INT-SSO-01, FS-PART11-04, FS-XSYS-AD-01 | OQ-AUTHN-01 |
| DS-VSUB-02 | Conditional-Access Policy | `Regulatory-App Conditional Access (FIDO2 phishing-resistant MFA)` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-CA-01 |
| DS-VSUB-03 | SIEM Forwarding | `Splunk gxp-authn syslog RFC 5424; lag ≤ 5 min` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-SIEM-01 |
| DS-VSUB-04 | PAM Break-Glass | `CyberArk PAM — 24 h rotation + dual-witness` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-PAM-01 |
| DS-VSUB-05 | Vendor-Assurance Pack | `VA-VEEVA-2026 — SOC 2 Type II + ISO 27001 + ISO 27017 + customer-shared CSV + DPA + BAA` | Custom | Per FS-VND-01. | FS-VND-01 | IQ-VND-01 |
| DS-VSUB-06 | Release-Impact-Assessment Workflow | `24R1..25R1 release cadence; 14-day SLA` | Custom | Per FS-VND-02. | FS-VND-02 | OQ-VND-01 |
| DS-VSUB-07 | Veeva TR-Audit Filing | `Annual; filed in vendor-assurance dossier` | Custom | Per FS-VND-03. | FS-VND-03 | OQ-VND-02 |
| DS-VSUB-08 | Per-Product Lifecycle | `DRAFT → QC → UAT → PROD; SoD-enforced sign-off` | Custom | Per FS-CFG-01. | FS-CFG-01 | OQ-LIFECYCLE-01 |
| DS-VSUB-09 | Config Export Endpoint | `Version-stamped JSON snapshot per product` | Custom | Per FS-CFG-02. | FS-CFG-02 | OQ-CFG-01 |
| DS-VSUB-10 | Pre-PROD Promotion Regression Pack | `REG-VSUB-2026` | Custom | Per FS-CFG-03. | FS-CFG-03 | OQ-PROMOTE-01 |
| DS-VSUB-11 | Force-Reauth on Signing | `OAuth2 max-age 5 min` | Custom | Per FS-PART11-11. | FS-PART11-11 | OQ-PART11-200 |

### 4.2 Planning + Document Selection Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-12 | Planning Module Artefact Types | `IND / NDA / BLA / ANDA / MAA / CTA / variation / renewal / withdrawal` | Custom | Per FS-PLAN-01. | FS-PLAN-01 | OQ-PLAN-01 |
| DS-VSUB-13 | Multi-Country Planning Master | `Spawns per-region sequence-build jobs with shared core + region M1` | Custom | Per FS-PLAN-02. | FS-PLAN-02 | OQ-PLAN-02 |
| DS-VSUB-14 | Milestone-Tracker At-Risk Alerts | `Target submission date + agency interaction + expected response` | Custom | Per FS-PLAN-03. | FS-PLAN-03 | OQ-PLAN-03 |
| DS-VSUB-15 | Resource-Estimation Calculator | `Per submission type per region` | Custom | Per FS-PLAN-04. | FS-PLAN-04 | OQ-PLAN-04 |
| DS-VSUB-16 | Document-Selection URN Bind | `Selection locks document version-of-record at lock-time` | Custom | Per FS-DOC-01. | FS-DOC-01 | OQ-DOC-01 |
| DS-VSUB-17 | Document-Reuse Cross-Reference | `Reused-document version-of-record displayed` | Custom | Per FS-DOC-02. | FS-DOC-02 | OQ-DOC-02 |
| DS-VSUB-18 | CTD-Section-Validity Rule Pack | `ctd-section-validity-2026.yaml` | Custom | Per FS-DOC-03. | FS-DOC-03 | OQ-DOC-03 |
| DS-VSUB-19 | Reuse-Impact Analysis | `Flags downstream sequences when reused document changes` | Custom | Per FS-DOC-04. | FS-DOC-04 | OQ-DOC-04 |

### 4.3 eCTD Build Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-20 | Sequence-Build Engine | `Generates ICH M8 v3.2.2 (or v4.0 for EU) per agency profile` | Custom | Per FS-ECTD-01. | FS-ECTD-01 | OQ-ECTD-01 |
| DS-VSUB-21 | Module 1 Region Templates | `m1-us-fda.xsl, m1-eu.xsl, m1-jp.xsl, m1-ca.xsl, m1-uk-mhra.xsl, m1-ch.xsl, m1-br.xsl, m1-cn.xsl` | Custom | Per FS-ECTD-02. | FS-ECTD-02 | OQ-ECTD-02 |
| DS-VSUB-22 | CTD Core Modules | `Modules 2-5 shared content; region-specific xlink:href in M1 leaves` | Custom | Per FS-ECTD-03. | FS-ECTD-03 | OQ-ECTD-03 |
| DS-VSUB-23 | Structural-Validity Check | `DTD / XSD check at compile time; failure blocks compile` | Custom | Per FS-ECTD-04. | FS-ECTD-04 | OQ-ECTD-04 |
| DS-VSUB-24 | Lifecycle Operations (Leaf-Level) | `new / append / replace / delete per ICH M8; audit-trailed` | Custom | Per FS-ECTD-05. | FS-ECTD-05 | OQ-ECTD-05 |
| DS-VSUB-25 | Index.xml Determinism | `Deterministic given identical content set` | Custom | Per FS-ECTD-06. | FS-ECTD-06 | OQ-INDEX-DETERMINISM-01 |

### 4.4 Validation (LORENZ) Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-26 | LORENZ eValidator Integration | `REST API; agency-specific criteria pack version pinned per submission` | Custom | Per FS-VAL-01 + FS-INT-EVAL-01. | FS-VAL-01, FS-INT-EVAL-01 | OQ-VAL-01 |
| DS-VSUB-27 | Validation Classification | `Error / Warning / Info; Errors block submission; Warnings require publisher justification capture` | Custom | Per FS-VAL-02. | FS-VAL-02 | OQ-VAL-02 |
| DS-VSUB-28 | LORENZ docuBridge Preview + Diff | `Via Veeva integration; UI surfaces preview` | Custom | Per FS-VAL-03 + FS-INT-DOCB-01. | FS-VAL-03, FS-INT-DOCB-01 | OQ-VAL-03 |
| DS-VSUB-29 | Validation Criteria-Pack Version | `Stamped on each validation run; updates tracked under CR` | Custom | Per FS-VAL-04. | FS-VAL-04 | OQ-VAL-04 |
| DS-VSUB-30 | Validation Reports Archive | `Per sequence in Submissions Archive` | Custom | Per FS-VAL-05. | FS-VAL-05 | OQ-VAL-05 |

### 4.5 Sequence + Granularity + Style Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-31 | Sequence-Number Generator | `Zero-padded 4-digit per application; gap-free; agency-specific` | Custom | Per FS-SEQ-01. | FS-SEQ-01 | OQ-SEQ-01 |
| DS-VSUB-32 | xlink:href Validation | `At compile (dangling-link check)` | Custom | Per FS-SEQ-02. | FS-SEQ-02 | OQ-SEQ-02 |
| DS-VSUB-33 | Sequence-Release Signature | `Submissions Approver re-authentication (OAuth2 max-age 5 min)` | Custom | Per FS-SEQ-03 + FS-PART11-11. | FS-SEQ-03, FS-PART11-11 | OQ-SEQ-03 |
| DS-VSUB-34 | Leaf-Document-Lifecycle Audit | `previous-leaf-reference + operation type + timestamp` | Custom | Per FS-SEQ-04. | FS-SEQ-04 | OQ-SEQ-04 |
| DS-VSUB-35 | Sequence-Number-Conflict Detector | `Parallel submission attempts; resolution workflow` | Custom | Per FS-SEQ-05. | FS-SEQ-05 | OQ-SEQ-05 |
| DS-VSUB-36 | Granularity Policy | `Per CTD module via granularity-policy.yaml; FDA + EMA recommended defaults` | Custom | Per FS-GRAN-01. | FS-GRAN-01 | OQ-GRAN-01 |
| DS-VSUB-37 | Granularity Enforcement | `At compile; exceptions in granularity-exceptions log` | Custom | Per FS-GRAN-02. | FS-GRAN-02 | OQ-GRAN-02 |
| DS-VSUB-38 | Granularity-Change Impact Analysis | `Surfaces affected open sequences` | Custom | Per FS-GRAN-03. | FS-GRAN-03 | OQ-GRAN-03 |
| DS-VSUB-39 | PDF Conformance | `PDF/A-1b (FDA) / PDF/A-2 (EMA); bookmarks + hyperlinks preserved` | Custom | Per FS-STYLE-01. | FS-STYLE-01 | OQ-STYLE-01 |
| DS-VSUB-40 | Per-Region Stylesheets | `fda-stylesheet.xsl, ema-stylesheet.xsl, pmda-stylesheet.xsl` | Custom | Per FS-STYLE-02. | FS-STYLE-02 | OQ-STYLE-02 |
| DS-VSUB-41 | File-Naming-Convention Validator | `agency-naming-2026.yaml enforced at compile` | Custom | Per FS-STYLE-03. | FS-STYLE-03 | OQ-STYLE-03 |
| DS-VSUB-42 | Format-Precheck | `Broken hyperlinks + oversized fonts + missing bookmarks runs pre-validation` | Custom | Per FS-STYLE-04. | FS-STYLE-04 | OQ-STYLE-04 |
| DS-VSUB-43 | PDF Bookmark Validator | `Enforces agency-required bookmark structure` | Custom | Per FS-PDF-01. | FS-PDF-01 | OQ-PDF-01 |
| DS-VSUB-44 | Broken-Internal-Link Check | `At compile; failures block sequence build` | Custom | Per FS-PDF-02. | FS-PDF-02 | OQ-PDF-02 |
| DS-VSUB-45 | Font-Embedding Check | `All fonts subsetted + embedded; non-compliant PDFs rejected` | Custom | Per FS-PDF-03. | FS-PDF-03 | OQ-PDF-03 |
| DS-VSUB-46 | PDF Security-Setting Validator | `No password / no copy-restriction enforced` | Custom | Per FS-PDF-04. | FS-PDF-04 | OQ-PDF-04 |

### 4.6 Diff + Archive Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-47 | Sequence-Diff | `Via docuBridge — leaf-level change-tracking with classification` | Custom | Per FS-DIFF-01. | FS-DIFF-01 | OQ-DIFF-01 |
| DS-VSUB-48 | Submissions Archive | `Immutable storage with object-lock; all submitted sequences + regulator acks` | Custom | Per FS-DIFF-02. | FS-DIFF-02 | OQ-ARC-01 |
| DS-VSUB-49 | Archive Retrieval | `P95 ≤ 4 h; runbook SOP-ARCHIVE-RETRIEVE` | Custom | Per FS-DIFF-03. | FS-DIFF-03 | PQ-ARC-01 |
| DS-VSUB-50 | Archive Sequence-Index Export | `eCTD-viewer format (XML index + per-sequence ZIP)` | Custom | Per FS-DIFF-04. | FS-DIFF-04 | OQ-ARC-02 |

### 4.7 Gateway Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-51 | FDA ESG Endpoint | `AS2 + SHA-256 receipt verification` | Custom | Per FS-GW-01. | FS-GW-01 | OQ-GW-01 |
| DS-VSUB-52 | EMA CESP Endpoint | `SFTP-based protocol; EMA Common Repository ingestion via ack` | Custom | Per FS-GW-02. | FS-GW-02 | OQ-GW-02 |
| DS-VSUB-53 | PMDA Gateway | `JP-specific protocol; ack reconciliation` | Custom | Per FS-GW-03. | FS-GW-03 | OQ-GW-03 |
| DS-VSUB-54 | Health Canada CESG | `AS2 / WebTrader; ack reconciliation` | Custom | Per FS-GW-04. | FS-GW-04 | OQ-GW-04 |
| DS-VSUB-55 | MHRA UK Endpoint | `UK regulator's submission interface; UK M1 wrapped` | Custom | Per FS-GW-05. | FS-GW-05 | OQ-GW-05 |
| DS-VSUB-56 | Swissmedic eGov Endpoint | `CH M1 wrapped` | Custom | Per FS-GW-06. | FS-GW-06 | OQ-GW-06 |
| DS-VSUB-57 | ANVISA Endpoint | `BR M1 wrapped` | Custom | Per FS-GW-07. | FS-GW-07 | OQ-GW-07 |
| DS-VSUB-58 | NMPA Endpoint | `CN M1 wrapped per China-specific requirements` | Custom | Per FS-GW-08. | FS-GW-08 | OQ-GW-08 |
| DS-VSUB-59 | Negative-Ack Workflow | `Structured Exception with agency-error-code mapping; resubmission within grace period` | Custom | Per FS-GW-09. | FS-GW-09 | OQ-GW-09 |
| DS-VSUB-60 | Quarterly Gateway Connectivity Test | `gateway-connect-quarterly.py` | Custom | Per FS-GW-10. | FS-GW-10 | OQ-GW-10 |
| DS-VSUB-61 | Per-Agency Maintenance Window Calendar | `gateway-windows-2026.yaml; scheduler avoids windows` | Custom | Per FS-GW-11. | FS-GW-11 | OQ-GW-11 |

### 4.8 IDMP + xEVMPD + SPOR Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-62 | Product Master Identifiers | `ISO 11238/11239/11240/11615/11616; reconciled vs EMA SPOR daily` | Custom | Per FS-IDMP-01 + FS-INT-SPOR-01. | FS-IDMP-01, FS-INT-SPOR-01 | OQ-IDMP-01 |
| DS-VSUB-63 | IDMP Metadata Auto-Population | `Into EU M1 + xEVMPD via template binding` | Custom | Per FS-IDMP-02. | FS-IDMP-02 | OQ-IDMP-02 |
| DS-VSUB-64 | xEVMPD XEVPRM Worker | `Per EMA ack reconciliation` | Custom | Per FS-IDMP-03. | FS-IDMP-03 | OQ-IDMP-03 |
| DS-VSUB-65 | IDMP-Drift-Detection Job | `Quarterly; impact-assessment opened on detected drift` | Custom | Per FS-IDMP-04. | FS-IDMP-04 | OQ-IDMP-04 |

### 4.9 Region-Specific Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-66 | UK MHRA Template | `UK M1 template + UK-specific cover letter + UK-specific cover sheet` | Custom | Per FS-REGION-MHRA-01. | FS-REGION-MHRA-01 | OQ-MHRA-01 |
| DS-VSUB-67 | NI Protocol Handling | `Parallel EU + UK submission with shared core, divergent M1` | Custom | Per FS-REGION-MHRA-02. | FS-REGION-MHRA-02 | OQ-MHRA-02 |
| DS-VSUB-68 | Swissmedic CH Template | `CH M1 + DACH-language label artefacts (de-CH, fr-CH, it-CH)` | Custom | Per FS-REGION-SWISS-01. | FS-REGION-SWISS-01 | OQ-SWISS-01 |
| DS-VSUB-69 | ANVISA BR Template | `BR M1 + pt-BR translation routing` | Custom | Per FS-REGION-ANVISA-01. | FS-REGION-ANVISA-01 | OQ-ANVISA-01 |
| DS-VSUB-70 | NMPA CN Template | `CN M1 + zh-CN translation + CN-specific stability + manufacturing pre-check` | Custom | Per FS-REGION-NMPA-01. | FS-REGION-NMPA-01 | OQ-NMPA-01 |
| DS-VSUB-71 | DACH EU-Variant Set | `de-DE for EU MAA marketed in DE; de-AT for AT national; de-CH for CH` | Custom | Per FS-REGION-DACH-01. | FS-REGION-DACH-01 | OQ-DACH-01 |
| DS-VSUB-72 | Region-Language Matrix | `region-lang-2026.yaml per product` | Custom | Per FS-REGION-LANG-01. | FS-REGION-LANG-01 | OQ-LANG-01 |

### 4.10 Translation Lifecycle Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-73 | Translation Package Builder | `Per submission per region; source-link via translation-job-id` | Custom | Per FS-TRANS-01. | FS-TRANS-01 | OQ-TRANS-01 |
| DS-VSUB-74 | Translation Lifecycle | `DRAFT → TRANSLATION → REVIEW → APPROVED → SUBMITTED; vendor hand-off + return via translation-vendor REST API` | Custom | Per FS-TRANS-02. | FS-TRANS-02 | OQ-TRANS-02 |
| DS-VSUB-75 | Source-to-Target Alignment | `Via segment-id; source updates flag translation drift` | Custom | Per FS-TRANS-03. | FS-TRANS-03 | OQ-TRANS-03 |
| DS-VSUB-76 | Translation Memory + Glossary | `Per product family` | Custom | Per FS-TRANS-04. | FS-TRANS-04 | OQ-TRANS-04 |
| DS-VSUB-77 | Local-Medical-Reviewer Sign-Off | `For region-specific labelling` | Custom | Per FS-TRANS-05. | FS-TRANS-05 | OQ-TRANS-05 |

### 4.11 Variation Master Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-78 | Variation Master Schema | `One canonical change deployed across N regions with per-region timing` | Custom | Per FS-VAR-01. | FS-VAR-01 | OQ-VAR-01 |
| DS-VSUB-79 | Variation-Classification Rule Pack | `EU Type IA/IB/II/III; FDA supplements; JP / CA categories` | Custom | Per FS-VAR-02. | FS-VAR-02 | OQ-VAR-02 |
| DS-VSUB-80 | Variation Dashboard | `Grafana panel per-agency status` | Custom | Per FS-VAR-03. | FS-VAR-03 | OQ-VAR-03 |
| DS-VSUB-81 | Conditional-Variation Dependency Graph | `Downstream-submission dependencies` | Custom | Per FS-VAR-04. | FS-VAR-04 | OQ-VAR-04 |

### 4.12 Audit Trail + Part 11 + ALCOA+ Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-82 | Audit-Trail Coverage | `All document / signature / sequence-build / validation / submission / ack / archive events` | Custom | Per FS-AUD-01. | FS-AUD-01 | OQ-AUDIT-01 |
| DS-VSUB-83 | Append-Only DB | `Vendor-controlled; TR-Audit confirms` | Custom | Per FS-AUD-02. | FS-AUD-02 | OQ-AUDIT-02 |
| DS-VSUB-84 | Audit-Trail Review Cadence | `Monthly Submissions Manager + quarterly QA review; signed reports filed` | Custom | Per FS-AUD-03. | FS-AUD-03 | OQ-AUDIT-03 |
| DS-VSUB-85 | Retention | `Per jurisdictional minimum (US ≥ 2 y post-approval, EU ≥ 10 y, JP ≥ 15 y) enforced at archive tier` | Custom | Per FS-AUD-04. | FS-AUD-04 | OQ-AUDIT-04 |
| DS-VSUB-86 | § 11.10(a) SOPs | `Reviewed annually` | Custom | Per FS-PART11-01. | FS-PART11-01 | OQ-PART11-10a |
| DS-VSUB-87 | § 11.10(b) Copy Generation | `Verified` | Custom | Per FS-PART11-02. | FS-PART11-02 | OQ-PART11-10b |
| DS-VSUB-88 | § 11.10(c) Retention Protection | `Vendor-confirmed immutable storage` | Custom | Per FS-PART11-03. | FS-PART11-03 | OQ-PART11-10c |
| DS-VSUB-89 | § 11.10(d) Access Control | `Okta SAML 2.0 + MFA` | Custom | Per FS-PART11-04. | FS-PART11-04 | OQ-PART11-10d |
| DS-VSUB-90 | § 11.10(e) Audit Trail | `Per DS-VSUB-82` | Custom | Per FS-PART11-05. | FS-PART11-05 | OQ-PART11-10e |
| DS-VSUB-91 | § 11.10(g) Authority Checks | `At workflow / API layer` | Custom | Per FS-PART11-06. | FS-PART11-06 | OQ-PART11-10g |
| DS-VSUB-92 | § 11.10(k) Operation-Manual Change Control | — | Custom | Per FS-PART11-07. | FS-PART11-07 | OQ-PART11-10k |
| DS-VSUB-93 | § 11.50 Manifestation | `Printed name + date/time + meaning rendered` | Custom | Per FS-PART11-08. | FS-PART11-08 | OQ-PART11-50 |
| DS-VSUB-94 | § 11.70 HMAC-SHA-256 Binding | — | Custom | Per FS-PART11-09. | FS-PART11-09 | OQ-PART11-70 |
| DS-VSUB-95 | § 11.100 Uniqueness | `Okta-DB constraint` | Custom | Per FS-PART11-10. | FS-PART11-10 | OQ-PART11-100 |
| DS-VSUB-96 | § 11.200 Re-Auth at Content / Sequence-Release / Gateway-Submission | — | Custom | Per FS-PART11-11. | FS-PART11-11 | OQ-PART11-200 |
| DS-VSUB-97 | § 11.300 Password / Credential Controls | `Per InfoSec` | Custom | Per FS-PART11-12. | FS-PART11-12 | OQ-PART11-300 |
| DS-VSUB-98 | ALCOA+ Attributable | `actor_id captured` | Custom | Per FS-DI-01. | FS-DI-01 | OQ-DI-01 |
| DS-VSUB-99 | ALCOA+ Legible | `PDF/A-1b / PDF/A-2 verified per agency` | Custom | Per FS-DI-02. | FS-DI-02 | OQ-DI-02 |
| DS-VSUB-100 | ALCOA+ Contemporaneous | `NTP-synced server timestamps` | Custom | Per FS-DI-03. | FS-DI-03 | OQ-DI-03 |
| DS-VSUB-101 | ALCOA+ Original | `Source preserved; corrections as new versions` | Custom | Per FS-DI-04. | FS-DI-04 | OQ-DI-04 |
| DS-VSUB-102 | ALCOA+ Accurate | `Sequence-build calculations deterministic; OQ-verified` | Custom | Per FS-DI-05. | FS-DI-05 | OQ-DI-05 |
| DS-VSUB-103 | ALCOA+ Retention + Chronology | `Per jurisdictional minimum` | Custom | Per FS-DI-06. | FS-DI-06 | OQ-DI-06 |

### 4.13 Integration Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-104 | Vault QualityDocs URN Resolver | `Vault Cross-Vault Bridge` | Custom | Per FS-INT-VAULT-01. | FS-INT-VAULT-01 | OQ-VAULT-01 |
| DS-VSUB-105 | Vault RIM Integration | `Product / authorisation master` | Custom | Per FS-INT-VAULT-02. | FS-INT-VAULT-02 | OQ-VAULT-02 |
| DS-VSUB-106 | Vault eTMF Cross-Reference | `Where TMF informs submission` | Custom | Per FS-INT-VAULT-03. | FS-INT-VAULT-03 | OQ-VAULT-03 |
| DS-VSUB-107 | Vault PromoMats Integration | `Where applicable` | Custom | Per FS-INT-VAULT-04. | FS-INT-VAULT-04 | OQ-VAULT-04 |
| DS-VSUB-108 | Sirius PV (Argus) Integration | `PSUR / PBRER / PADER / DSUR content via internal API` | Custom | Per FS-INT-VIG-01. | FS-INT-VIG-01 | OQ-VIG-01 |
| DS-VSUB-109 | EMA SPOR REST API | `For IDMP reference data` | Custom | Per FS-INT-SPOR-01. | FS-INT-SPOR-01 | OQ-SPOR-01 |
| DS-VSUB-110 | LORENZ eValidator REST API | — | Custom | Per FS-INT-EVAL-01. | FS-INT-EVAL-01 | OQ-EVAL-01 |
| DS-VSUB-111 | LORENZ docuBridge | `REST + thin-client browser embed` | Custom | Per FS-INT-DOCB-01. | FS-INT-DOCB-01 | OQ-DOCB-01 |
| DS-VSUB-112 | Translation-Vendor REST API | `Job dispatch + return` | Custom | Per FS-INT-TRANS-01. | FS-INT-TRANS-01 | OQ-TRANS-06 |
| DS-VSUB-113 | Okta SSO + MFA | `SAML 2.0` | Custom | Per FS-INT-SSO-01. | FS-INT-SSO-01 | OQ-SSO-01 |

### 4.14 Performance + Availability + Security Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-114 | Sequence-Compile P95 | `≤ 30 min for 5,000-document sequence` | Custom | Per FS-PERF-01. | FS-PERF-01 | PQ-PERF-01 |
| DS-VSUB-115 | eValidator P95 | `≤ 15 min per sequence` | Custom | Per FS-PERF-02. | FS-PERF-02 | PQ-PERF-02 |
| DS-VSUB-116 | Archive Retrieval P95 | `≤ 4 h` | Custom | Per FS-PERF-03. | FS-PERF-03 | PQ-PERF-03 |
| DS-VSUB-117 | Vendor SLA | `≥ 99.7%; uptime probes 24×7` | Custom | Per FS-AV-01. | FS-AV-01 | OQ-AV-01 |
| DS-VSUB-118 | RPO / RTO | `Per Veeva SLA; annual verification` | Custom | Per FS-AV-02. | FS-AV-02 | OQ-AV-02 |
| DS-VSUB-119 | Backup | `Veeva-managed; site verifies annually` | Custom | Per FS-BAK-01. | FS-BAK-01 | OQ-BAK-01 |
| DS-VSUB-120 | Quarterly Tenant Export | `Retained ≥ 10 y in site cold storage` | Custom | Per FS-BAK-02. | FS-BAK-02 | OQ-BAK-02 |
| DS-VSUB-121 | RBAC Matrix | `Per-product / per-agency / per-region` | Custom | Per FS-SEC-01. | FS-SEC-01 | OQ-SEC-01 |
| DS-VSUB-122 | TLS / AES Stance | `TLS 1.3 + AES-256` | Custom | Per FS-SEC-02. | FS-SEC-02 | OQ-SEC-02 |
| DS-VSUB-123 | Annual Pen-Test | `H/C remediation within 60 days` | Custom | Per FS-SEC-03. | FS-SEC-03 | OQ-SEC-03 |

### 4.15 Application Lifecycle + Meeting + SPL + DMF Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-124 | Application-Lifecycle Tracker | `Per (application_id, agency); initial / amendment / supplement / variation / renewal / withdrawal` | Custom | Per FS-LIFE-01. | FS-LIFE-01 | OQ-LIFE-01 |
| DS-VSUB-125 | Application Status | `Active / under-review / approved / withdrawn / lapsed; per agency on dashboard` | Custom | Per FS-LIFE-02. | FS-LIFE-02 | OQ-LIFE-02 |
| DS-VSUB-126 | Approval-Letter + EPAR + Label-of-Record | `Archived per application per agency` | Custom | Per FS-LIFE-03. | FS-LIFE-03 | OQ-LIFE-03 |
| DS-VSUB-127 | Lifecycle Milestone Alerts | `PDUFA + CHMP opinion + MAA renewal — email + dashboard` | Custom | Per FS-LIFE-04. | FS-LIFE-04 | OQ-LIFE-04 |
| DS-VSUB-128 | Meeting Tracker | `Pre-IND / Type-B / Type-C / Pre-NDA / EMA scientific-advice / PMDA-consultation; request → briefing-doc → minutes → feedback` | Custom | Per FS-MEET-01. | FS-MEET-01 | OQ-MEET-01 |
| DS-VSUB-129 | Briefing-Document Submission | `Per relevant agency template; eCTD-compiled where required` | Custom | Per FS-MEET-02. | FS-MEET-02 | OQ-MEET-02 |
| DS-VSUB-130 | Meeting-Feedback Forwarding | `To submission planning` | Custom | Per FS-MEET-03. | FS-MEET-03 | OQ-MEET-03 |
| DS-VSUB-131 | FDA SPL Generator | `Per 21 CFR 314.81; SPL XML validated against HL7 SPL schema` | Custom | Per FS-SPL-01. | FS-SPL-01 | OQ-SPL-01 |
| DS-VSUB-132 | SPL Versioning | `Effective-time + version-number sequencing per HL7 SPL` | Custom | Per FS-SPL-02. | FS-SPL-02 | OQ-SPL-02 |
| DS-VSUB-133 | SPL Drug-Listing + Establishment-Registration | `Per 21 CFR Part 207 tracked` | Custom | Per FS-SPL-03. | FS-SPL-03 | OQ-SPL-03 |
| DS-VSUB-134 | Cross-Application Document-Reuse Tracker | `DMF referenced by multiple NDA / ANDA with reference-letter management` | Custom | Per FS-REF-01. | FS-REF-01 | OQ-REF-01 |
| DS-VSUB-135 | Letter-of-Authorization (LoA) Tracker | `Effective dates + revocation events` | Custom | Per FS-REF-02. | FS-REF-02 | OQ-REF-02 |
| DS-VSUB-136 | DMF Status Tracking | `Type II / III / IV / V + adequacy-status per DMF` | Custom | Per FS-REF-03. | FS-REF-03 | OQ-REF-03 |
| DS-VSUB-137 | RWE Submission Support | `SDTM / ADaM / SEND data-package upload + eCTD inclusion per 21st Century Cures + EMA RWE strategy` | Custom | Per FS-RWD-01. | FS-RWD-01 | OQ-RWD-01 |
| DS-VSUB-138 | PFDD Submission Support | `Dedicated Module 5 sub-section` | Custom | Per FS-RWD-02. | FS-RWD-02 | OQ-RWD-02 |

### 4.16 Dashboard + Combination-Product + Profile-Validation + Cover-Letter Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-139 | Submissions Dashboard | `Grafana; per-product per-agency status; refresh latency ≤ 15 min` | Custom | Per FS-DASH-01. | FS-DASH-01 | OQ-DASH-01 |
| DS-VSUB-140 | Per-Publisher KPI Dashboard | `sequences-published, validation-error-rate, on-time-submission rate` | Custom | Per FS-DASH-02. | FS-DASH-02 | OQ-DASH-02 |
| DS-VSUB-141 | Compile / Validate / Submit Time Histograms | `Per sequence-size class` | Custom | Per FS-DASH-03. | FS-DASH-03 | OQ-DASH-03 |
| DS-VSUB-142 | Combination-Product Routing | `OCP-assigned FDA Center (CDER / CBER / CDRH); dual-Center coordination workflow` | Custom | Per FS-COMBO-01. | FS-COMBO-01 | OQ-COMBO-01 |
| DS-VSUB-143 | Combination-Product M3+M5 Integration | `Template + cross-reference` | Custom | Per FS-COMBO-02. | FS-COMBO-02 | OQ-COMBO-02 |
| DS-VSUB-144 | Per-Submission-Type Validation Profile | `IND / NDA / ANDA / BLA / MAA / CTA / variation / supplement; pins LORENZ criteria + agency rules` | Custom | Per FS-PROF-VAL-01. | FS-PROF-VAL-01 | OQ-PROF-01 |
| DS-VSUB-145 | Per-Submission-Type Profile Change Control | `Under CR; open-submission impact assessed` | Custom | Per FS-PROF-VAL-02. | FS-PROF-VAL-02 | OQ-PROF-02 |
| DS-VSUB-146 | Per-Region Cover-Letter Templates | `FDA / EMA / PMDA / HC / MHRA / Swissmedic / ANVISA / NMPA` | Custom | Per FS-COVER-01. | FS-COVER-01 | OQ-COVER-01 |
| DS-VSUB-147 | Form Generators | `FDA 356h, FDA 1571, FDA 2253, EMA CESP submission form per region` | Custom | Per FS-COVER-02. | FS-COVER-02 | OQ-COVER-02 |
| DS-VSUB-148 | Cover-Letter Version-Control | `Template-version + per-submission instance` | Custom | Per FS-COVER-03. | FS-COVER-03 | OQ-COVER-03 |

### 4.17 Cross-System Integration Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-149 | Hydra Egress ACL | `reg-vault-egress-deny-llm — blocks vendor LLM endpoints except via Hydra VIP` | Custom | Per FS-XINT-HYD-01. | FS-XINT-HYD-01 | OQ-HYD-01 |
| DS-VSUB-150 | Hydra Use-Cases | `REG-DRAFT-MOD2-001, REG-DRAFT-MOD3-001, REG-DRAFT-RTI-001 with risk_class=annex_i + Art. 11 pack artefact; gate 403 on missing pack` | Custom | Per FS-XINT-HYD-02. | FS-XINT-HYD-02 | OQ-HYD-02 |
| DS-VSUB-151 | Vault Binder Ingestion Hook | `Validates per-section watermark + provenance JSON; binder finalisation API requires approver_role=RegAffairsLead + valid e-signature ≤ 1 h before finalisation` | Custom | Per FS-XINT-HYD-03. | FS-XINT-HYD-03 | OQ-HYD-03 |
| DS-VSUB-152 | Per-Section Content Hash Verification | `Recomputed at finalisation + compared with post-HITL hash; mismatch → MasterControl deviation BLR-HYD-WATERMARK-MISMATCH` | Custom | Per FS-XINT-HYD-04. | FS-XINT-HYD-04 | OQ-HYD-04 |
| DS-VSUB-153 | Helios Hydra Topic | `helios.ingest.bellerophon.hydra.v1; retention floor 2 y` | Custom | Per FS-XINT-HYD-05. | FS-XINT-HYD-05 | OQ-HEL-01 |
| DS-VSUB-154 | Helios Submissions Topic | `helios.ingest.bellerophon.submissions.v1; schema-pinned envelope; at-least-once; idempotency key {source_system, event_id}; Prometheus alert at > 600 s P95 lag` | Custom | Per FS-XINT-HEL-01. | FS-XINT-HEL-01 | OQ-HEL-02 |
| DS-VSUB-155 | Helios Reconciliation | `Product lifetime + 25 y local retention; daily parity check; MasterControl deviation on > 0.01% mismatch over 24 h` | Custom | Per FS-XINT-HEL-02. | FS-XINT-HEL-02 | OQ-HEL-03 |
| DS-VSUB-156 | EDMS Read Adapter | `BLR-EDMS-READ-1.x — GET /docs/{doc_id}?version=effective; pin binder entry to {doc_id, version, sha256}; drift triggers re-validation` | Custom | Per FS-XINT-EDMS-01. | FS-XINT-EDMS-01 | OQ-EDMS-01 |
| DS-VSUB-157 | Backup Integration | `Veeam Application-Aware + PostgreSQL pg_basebackup + WAL + object-replica; T1; RPO ≤ 4 h; RTO ≤ 4 BH; S3 Object Lock Compliance; LTO-9 monthly` | Custom | Per FS-XSYS-BAK-01. | FS-XSYS-BAK-01 | OQ-BAK-01 |
| DS-VSUB-158 | AD Identity Integration | `SAML 2.0 via Entra ID + SCIM lifecycle provisioning; conditional-access policy Regulatory-App; SIEM + PAM per DS-VSUB-02..04` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-AD-01 |

### 4.18 Training + Periodic Review + Inspection-Readiness Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VSUB-159 | LMS Training Gate | `Role-specific + agency-specific publisher competency` | Custom | Per FS-TRN-01. | FS-TRN-01 | OQ-TRN-01 |
| DS-VSUB-160 | Annual Refresher | `RA-ANNUAL-2026 — FDA / EMA / PMDA / HC / MHRA / ANVISA / NMPA updates` | Custom | Per FS-TRN-02. | FS-TRN-02 | OQ-TRN-02 |
| DS-VSUB-161 | Annual Periodic Review Run-Book | `Vendor qualification + config drift + validation-pack version + gateway connectivity + archive retrieval rehearsal + IDMP / SPOR reconciliation + translation-vendor performance + deviation summary + training currency` | Custom | Per FS-PR-01. | FS-PR-01 | OQ-PR-01 |
| DS-VSUB-162 | Inspection-Readiness Export | `Per-submission dossier (sequence content + validation report + ack messages + signature evidence + audit-trail extract); P95 ≤ 4 h` | Custom | Per FS-INSP-01. | FS-INSP-01 | OQ-INSP-01 |
| DS-VSUB-163 | HA-Correspondence Register | `FDA-IR + EMA D-120/D-180 + PMDA queries with per-question sub-tracking + SLA monitoring` | Custom | Per FS-INSP-02. | FS-INSP-02 | OQ-INSP-02 |
| DS-VSUB-164 | CA-Query Response Workflow | `Drafter → reviewer → Submissions Approver SoD-enforced; PDF/A-3 export` | Custom | Per FS-INSP-03. | FS-INSP-03 | OQ-INSP-03 |
| DS-VSUB-165 | Mock-Audit Rehearsal | `Structured findings + remediation tracker` | Custom | Per FS-INSP-04. | FS-INSP-04 | OQ-INSP-04 |

---

## 5. Workflow + Business-Rule Design

### 5.1 ECTD Sequence Build → Dispatch Workflow

```
   [Submission Plan finalised (DS-VSUB-12..15)]
         │
         ▼ Document selection via QualityDocs URN (DS-VSUB-16) — version-of-record locked
   [DRAFT sequence]
         │
         ▼ Per-region Module 1 template applied (DS-VSUB-21)
   [Sequence-build engine (DS-VSUB-20) — ICH M8 v3.2.2 or v4.0 per agency]
         │
         ▼ Structural-validity check (DS-VSUB-23) — DTD/XSD; failure blocks compile
         ▼ Granularity enforcement (DS-VSUB-37)
         ▼ Style + cross-ref + bookmark checks (DS-VSUB-39..46)
         ▼ Sequence-number generation (DS-VSUB-31) — gap-free per HA per product
   [Compiled sequence]
         │
         ▼ LORENZ eValidator (DS-VSUB-26) — agency-specific criteria pack pinned (DS-VSUB-29)
   [Validation Report: Errors block; Warnings → publisher justification (DS-VSUB-27)]
         │
         ▼ Sequence-content SHA-256 hash recorded (per FS-SEQ-07 — Bellerophon equivalent in archive)
         ▼ docuBridge preview + diff (DS-VSUB-28, DS-VSUB-47)
   [READY-TO-PUBLISH]
         │
         ▼ Submissions Approver re-authentication (DS-VSUB-11, DS-VSUB-33)
   [Sequence Release]
         │
         ▼ Per-HA gateway routing (DS-VSUB-51..58)
   [Dispatched]
         │
         ▼ Ack reconciliation; non-ack → negative-ack workflow (DS-VSUB-59)
   [PUBLISHED]
         │
         ▼ Auto-archive to Submissions Archive (DS-VSUB-48) — immutable + object-lock
   [ARCHIVED — retention per jurisdictional minimum (DS-VSUB-85)]
```

### 5.2 Multi-Country Variation Workflow

```
   [Variation Master (DS-VSUB-78) — one canonical change]
         │
         ▼ Per-region classification (DS-VSUB-79)
   ┌────────────────────────────────────────────────────────────────┐
   │  EU → Type IA/IB/II/III                                         │
   │  FDA → CBE / CBE-30 / PAS / other supplement                    │
   │  JP / CA → JP / CA categories                                   │
   └────────────────────────────────────────────────────────────────┘
         │
         ▼ Per-region timing scheduled (DS-VSUB-78)
         ▼ Conditional-variation dependency graph traversed (DS-VSUB-81)
   [Per-region sequence-build jobs spawned (DS-VSUB-13)]
         │
         ▼ Variation Dashboard tracks per-agency status (DS-VSUB-80)
   [Per-region dispatch → Application-Lifecycle Tracker updates (DS-VSUB-124)]
```

### 5.3 Hydra-Drafted Module Workflow (AI Act Annex I)

```
   [Module 2 / Module 3 / RTI drafting initiated]
         │
         ▼ Egress firewall ACL allows only Hydra VIP (DS-VSUB-149)
   [Adapter BLR-HYD-CLIENT-1.x calls Hydra]
         │
         ▼ Hydra gate enforces use-case ID + risk_class=annex_i + Art. 11 pack present (DS-VSUB-150)
         ▼ 403 if pack missing or expired
   [Draft returned with watermark + provenance JSON]
         │
         ▼ Human-in-the-loop review by Subject-Matter Expert
   [Post-HITL hash computed + stored at approval]
         │
         ▼ Reg Affairs Lead e-signature (re-auth + valid timestamp ≤ 1 h before finalisation)
   [Vault binder ingestion hook (DS-VSUB-151) validates watermark + e-signature timestamp]
         │
         ▼ Binder finalisation API
   [Per-section content hash recomputed (DS-VSUB-152) — mismatch raises MasterControl deviation
    BLR-HYD-WATERMARK-MISMATCH]
         │
         ▼ Helios audit event to topic helios.ingest.bellerophon.hydra.v1 (DS-VSUB-153)
```

### 5.4 Translation Lifecycle Workflow

| Step | Action | Actor | Lifecycle state | FS-ID |
|---|---|---|---|---|
| 1 | Translation package built per region (DS-VSUB-73) | System | DRAFT | FS-TRANS-01 |
| 2 | Dispatched to translation vendor via REST API (DS-VSUB-112) | System | TRANSLATION | FS-INT-TRANS-01 |
| 3 | Returned translation reviewed | Translation Manager | REVIEW | FS-TRANS-02 |
| 4 | Local-medical-reviewer sign-off (DS-VSUB-77) | Local Medical Reviewer | APPROVED | FS-TRANS-05 |
| 5 | Submitted as part of region pack | System | SUBMITTED | FS-TRANS-02 |
| 6 | Source-update drift detection (DS-VSUB-75) | System | (flag) | FS-TRANS-03 |

---

## 6. Role-Permission Matrix Design

| Role | Doc Edit (DRAFT) | Review | Approve | Build Sequence | Validate | Release | Dispatch | Variation Mgr | IDMP Steward | Translation Mgr | View Archive | Inspector Read | Tenant Admin |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Submissions Author | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ |
| Submissions Reviewer | ✗ | ✓ (author ≠ reviewer) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ |
| Submissions Approver | ✗ | ✗ | ✓ (reviewer ≠ approver) | ✗ | ✗ | ✓ (re-auth) | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ |
| Publishing Manager | ✗ | ✓ | ✗ | ✓ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ |
| Publisher | ✗ | ✗ | ✗ | ✓ | ✓ | ✗ | ✓ (per agency) | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ |
| Reg Affairs Lead | ✗ | ✗ | ✓ (Hydra binder finalisation) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ |
| Director Reg Operations | ✗ | ✓ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ |
| Variation Manager | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | ✓ | ✗ | ✗ |
| IDMP / xEVMPD Steward | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✓ | ✗ | ✗ |
| Translation Manager | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | ✗ |
| Local Medical Reviewer | ✗ | ✗ | (translation sign-off) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| VP Global Reg Affairs | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ |
| Inspector (FDA / EMA / DACH / PMDA) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (time-bounded) | ✗ |
| Tenant Admin (Vault) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (config only) |

**Role-permission design rules:**
- **SoD enforced** — author ≠ reviewer ≠ approver per FS-CFG-01.
- **Dispatch requires re-authentication** per DS-VSUB-11 + DS-VSUB-96.
- **Hydra binder finalisation** requires Reg Affairs Lead e-signature with valid timestamp ≤ 1 h before finalisation (DS-VSUB-151).
- **Tenant Admin** excludes audit-trail UPDATE / DELETE.

---

## 7. Integration Design

(See § 4.13 and § 4.17 for per-integration CIs.) Summary table:

| Counterparty | Direction | Endpoint | Auth | FS-ID |
|---|---|---|---|---|
| Vault QualityDocs | bidirectional | Vault Cross-Vault Bridge | OAuth2 | FS-INT-VAULT-01 |
| Vault RIM | bidirectional | Vault Connect | OAuth2 | FS-INT-VAULT-02 |
| Vault eTMF | bidirectional | Vault Connect | OAuth2 | FS-INT-VAULT-03 |
| Vault PromoMats | bidirectional | Vault Connect | OAuth2 | FS-INT-VAULT-04 |
| Sirius PV (Argus) | bidirectional | Internal API | OAuth2 | FS-INT-VIG-01 |
| EMA SPOR | bidirectional | REST | OAuth2 | FS-INT-SPOR-01 |
| LORENZ eValidator | bidirectional | REST | OAuth2 | FS-INT-EVAL-01 |
| LORENZ docuBridge | bidirectional | REST + browser embed | OAuth2 | FS-INT-DOCB-01 |
| Translation Vendor | bidirectional | REST | OAuth2 | FS-INT-TRANS-01 |
| Okta | bidirectional | SAML 2.0 + SCIM | mutual cert | FS-INT-SSO-01 |
| FDA ESG | outbound | AS2 | AS2 SHA-256 | FS-GW-01 |
| EMA CESP | outbound | SFTP | per EMA | FS-GW-02 |
| PMDA Gateway | outbound | per PMDA | per PMDA | FS-GW-03 |
| Health Canada CESG | outbound | AS2 / WebTrader | per HC | FS-GW-04 |
| MHRA UK | outbound | per MHRA | per MHRA | FS-GW-05 |
| Swissmedic eGov | outbound | per CH | per CH | FS-GW-06 |
| ANVISA | outbound | per ANVISA | per ANVISA | FS-GW-07 |
| NMPA | outbound | per NMPA | per NMPA | FS-GW-08 |
| Hydra LLM gateway | outbound | REST (egress-gated) | mTLS + use-case ID | FS-XINT-HYD-01..05 |
| Helios Kafka | outbound | mTLS + SASL/SCRAM | per Helios | FS-XINT-HEL-01..02 |
| EDMS Read | bidirectional | REST | mTLS | FS-XINT-EDMS-01 |
| AUR Backup | (cross-system) | Veeam + PG pg_basebackup + WAL | per AUR | FS-XSYS-BAK-01 |

---

## 8. Site-Deployed Components Design

| Component | Type | Source location | Owner team | Verified by |
|---|---|---|---|---|
| `sequence-build-engine` | Service | `git.bellerophon-prod.local/regops/sequence-build-engine` | Reg Ops Engineering | OQ-ECTD-01..05 |
| `ectd-validator-adapter` | Library (LORENZ eValidator-compatible) | `git.bellerophon-prod.local/regops/ectd-validator-adapter` | Reg Ops Engineering | OQ-VAL-01..05 |
| `gateway-router` | Service | `git.bellerophon-prod.local/regops/gateway-router` | Reg Ops Engineering | OQ-GW-01..11 |
| `spl-generator` | Library | `git.bellerophon-prod.local/regops/spl-generator` | Reg Ops Engineering | OQ-SPL-01..03 |
| `idmp-export-engine` | Service | `git.bellerophon-prod.local/regops/idmp-export-engine` | Reg Ops Engineering | OQ-IDMP-01..04 |
| `xevmpd-worker` | Daemon | `git.bellerophon-prod.local/regops/xevmpd-worker` | Reg Ops Engineering | OQ-IDMP-03 |
| `idmp-drift-detector` | Scheduled (quarterly) | `git.bellerophon-prod.local/regops/idmp-drift-detector` | Reg Ops Engineering | OQ-IDMP-04 |
| `translation-package-builder` | Service | `git.bellerophon-prod.local/regops/translation-package-builder` | Reg Ops Engineering | OQ-TRANS-01..06 |
| `gateway-connect-quarterly` | Scheduled | `git.bellerophon-prod.local/regops/gateway-connect-quarterly` | Reg Ops Engineering | OQ-GW-10 |
| `meeting-tracker-api` | Service | `git.bellerophon-prod.local/regops/meeting-tracker-api` | Reg Ops Engineering | OQ-MEET-01..03 |
| `lifecycle-tracker-api` | Service | `git.bellerophon-prod.local/regops/lifecycle-tracker-api` | Reg Ops Engineering | OQ-LIFE-01..04 |
| `inspection-readiness-export` | Service | `git.bellerophon-prod.local/regops/inspection-readiness-export` | Reg Ops Engineering | PQ-INSP-01 |
| `BLR-HYD-CLIENT` (Hydra adapter) | Library v1.x | `git.bellerophon-prod.local/regops/blr-hyd-client` | AI Platform | OQ-HYD-01..04 |
| `BLR-EDMS-READ` (Vellis read adapter) | Library v1.x | `git.bellerophon-prod.local/regops/blr-edms-read` | Reg Ops Engineering | OQ-EDMS-01 |
| `helios-publisher` | Library | `git.bellerophon-prod.local/regops/helios-publisher` | Reg Ops Engineering | OQ-HEL-01..03 |

Each repository carries a `docs/SDS.md` mini-Software-Design-Specification artefact per GAMP 5 2nd-edition § 2B.4 rule 6.

---

## 9. References

### 9.1 US

- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- 21 CFR Part 207 (drug listing + establishment registration).
- 21 CFR 314.81 (SPL).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).
- FDA *Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions* (Aug 2025).
- FDA *eCTD Technical Conformance Guide*; FDA ESG specifications.
- HL7 SPL.

### 9.2 EU

- EU CTR 536/2014 Arts. 25/81.
- EMA eCTD EU IG; EMA CESP specifications; EMA SPOR.
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- GDPR Arts. 6, 17, 32.
- EU AI Act Reg. (EU) 2024/1689 — Arts. 9–18, 26, 43, 47–49, 50, 72, 73, 99; Annex I high-risk classification for Hydra-drafted Module 2/3/RTI content.

### 9.3 DACH

- BfArM (DE); Paul-Ehrlich-Institut (PEI); Swissmedic (CH); AGES PharmMed (AT).

### 9.4 International

- ICH M2 ESTRI; ICH M4 (CTD); ICH M8 (eCTD).
- IDMP ISO 11238/11239/11240/11615/11616.
- HL7 FHIR R5.
- ISPE GAMP 5 (2nd Edition, 2022).
- PIC/S PI 041.
- ISO/IEC 27001:2022; ISO/IEC 27017.
- PMDA Gateway specs; Health Canada CESG; MHRA UK Submissions; Swissmedic eGov; ANVISA eCTD; NMPA eCTD.

### 9.5 Vendor

- Veeva Systems — *Vault Submissions / Submissions Publishing 24R3 Reference*.
- LORENZ — *eValidator + docuBridge product references*.

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS ID | FS ID(s) | Notes |
|---|---|---|
| DS-VSUB-01 | FS-INT-SSO-01 / FS-PART11-04 / FS-XSYS-AD-01 | IdP mode |
| DS-VSUB-02 | FS-XSYS-AD-01 | Conditional-access policy |
| DS-VSUB-03 | FS-XSYS-AD-01 | SIEM forwarding |
| DS-VSUB-04 | FS-XSYS-AD-01 | PAM break-glass |
| DS-VSUB-05 | FS-VND-01 | Vendor-assurance pack |
| DS-VSUB-06 | FS-VND-02 | Release-impact workflow |
| DS-VSUB-07 | FS-VND-03 | TR-Audit filing |
| DS-VSUB-08 | FS-CFG-01 | Per-product lifecycle |
| DS-VSUB-09 | FS-CFG-02 | Config export |
| DS-VSUB-10 | FS-CFG-03 | Pre-PROD regression pack |
| DS-VSUB-11 | FS-PART11-11 | Force-reauth |
| DS-VSUB-12 | FS-PLAN-01 | Planning artefact types |
| DS-VSUB-13 | FS-PLAN-02 | Multi-country planning master |
| DS-VSUB-14 | FS-PLAN-03 | Milestone-tracker alerts |
| DS-VSUB-15 | FS-PLAN-04 | Resource estimator |
| DS-VSUB-16 | FS-DOC-01 | URN bind |
| DS-VSUB-17 | FS-DOC-02 | Document-reuse cross-ref |
| DS-VSUB-18 | FS-DOC-03 | CTD-section-validity rule pack |
| DS-VSUB-19 | FS-DOC-04 | Reuse-impact analysis |
| DS-VSUB-20 | FS-ECTD-01 | Sequence-build engine |
| DS-VSUB-21 | FS-ECTD-02 | M1 templates |
| DS-VSUB-22 | FS-ECTD-03 | CTD core modules |
| DS-VSUB-23 | FS-ECTD-04 | DTD/XSD check |
| DS-VSUB-24 | FS-ECTD-05 | Lifecycle operations |
| DS-VSUB-25 | FS-ECTD-06 | Index.xml determinism |
| DS-VSUB-26 | FS-VAL-01 / FS-INT-EVAL-01 | LORENZ eValidator |
| DS-VSUB-27 | FS-VAL-02 | Validation classification |
| DS-VSUB-28 | FS-VAL-03 / FS-INT-DOCB-01 | docuBridge preview |
| DS-VSUB-29 | FS-VAL-04 | Validation criteria-pack version |
| DS-VSUB-30 | FS-VAL-05 | Validation reports archive |
| DS-VSUB-31 | FS-SEQ-01 | Sequence-number generator |
| DS-VSUB-32 | FS-SEQ-02 | xlink:href validation |
| DS-VSUB-33 | FS-SEQ-03 / FS-PART11-11 | Sequence-release signature |
| DS-VSUB-34 | FS-SEQ-04 | Leaf-document-lifecycle audit |
| DS-VSUB-35 | FS-SEQ-05 | Sequence-number-conflict detector |
| DS-VSUB-36 | FS-GRAN-01 | Granularity policy |
| DS-VSUB-37 | FS-GRAN-02 | Granularity enforcement |
| DS-VSUB-38 | FS-GRAN-03 | Granularity-change impact |
| DS-VSUB-39 | FS-STYLE-01 | PDF conformance |
| DS-VSUB-40 | FS-STYLE-02 | Per-region stylesheets |
| DS-VSUB-41 | FS-STYLE-03 | File-naming validator |
| DS-VSUB-42 | FS-STYLE-04 | Format-precheck |
| DS-VSUB-43 | FS-PDF-01 | PDF bookmark validator |
| DS-VSUB-44 | FS-PDF-02 | Broken-internal-link check |
| DS-VSUB-45 | FS-PDF-03 | Font-embedding check |
| DS-VSUB-46 | FS-PDF-04 | PDF security validator |
| DS-VSUB-47 | FS-DIFF-01 | Sequence-diff |
| DS-VSUB-48 | FS-DIFF-02 | Submissions Archive |
| DS-VSUB-49 | FS-DIFF-03 | Archive retrieval |
| DS-VSUB-50 | FS-DIFF-04 | Archive sequence-index export |
| DS-VSUB-51 | FS-GW-01 | FDA ESG |
| DS-VSUB-52 | FS-GW-02 | EMA CESP |
| DS-VSUB-53 | FS-GW-03 | PMDA Gateway |
| DS-VSUB-54 | FS-GW-04 | Health Canada CESG |
| DS-VSUB-55 | FS-GW-05 | MHRA UK |
| DS-VSUB-56 | FS-GW-06 | Swissmedic eGov |
| DS-VSUB-57 | FS-GW-07 | ANVISA |
| DS-VSUB-58 | FS-GW-08 | NMPA |
| DS-VSUB-59 | FS-GW-09 | Negative-ack workflow |
| DS-VSUB-60 | FS-GW-10 | Quarterly connectivity test |
| DS-VSUB-61 | FS-GW-11 | Maintenance-window calendar |
| DS-VSUB-62 | FS-IDMP-01 / FS-INT-SPOR-01 | Product master + SPOR |
| DS-VSUB-63 | FS-IDMP-02 | IDMP auto-population |
| DS-VSUB-64 | FS-IDMP-03 | xEVMPD worker |
| DS-VSUB-65 | FS-IDMP-04 | IDMP-drift-detection |
| DS-VSUB-66 | FS-REGION-MHRA-01 | UK MHRA template |
| DS-VSUB-67 | FS-REGION-MHRA-02 | NI Protocol |
| DS-VSUB-68 | FS-REGION-SWISS-01 | Swissmedic CH |
| DS-VSUB-69 | FS-REGION-ANVISA-01 | ANVISA BR |
| DS-VSUB-70 | FS-REGION-NMPA-01 | NMPA CN |
| DS-VSUB-71 | FS-REGION-DACH-01 | DACH variants |
| DS-VSUB-72 | FS-REGION-LANG-01 | Region-language matrix |
| DS-VSUB-73 | FS-TRANS-01 | Translation package builder |
| DS-VSUB-74 | FS-TRANS-02 | Translation lifecycle |
| DS-VSUB-75 | FS-TRANS-03 | Source-to-target alignment |
| DS-VSUB-76 | FS-TRANS-04 | TM + glossary |
| DS-VSUB-77 | FS-TRANS-05 | Local-medical-reviewer sign-off |
| DS-VSUB-78 | FS-VAR-01 | Variation master schema |
| DS-VSUB-79 | FS-VAR-02 | Variation classification |
| DS-VSUB-80 | FS-VAR-03 | Variation dashboard |
| DS-VSUB-81 | FS-VAR-04 | Conditional dependency graph |
| DS-VSUB-82 | FS-AUD-01 | Audit-trail coverage |
| DS-VSUB-83 | FS-AUD-02 | Append-only DB |
| DS-VSUB-84 | FS-AUD-03 | Review cadence |
| DS-VSUB-85 | FS-AUD-04 | Retention per jurisdiction |
| DS-VSUB-86 | FS-PART11-01 | § 11.10(a) |
| DS-VSUB-87 | FS-PART11-02 | § 11.10(b) |
| DS-VSUB-88 | FS-PART11-03 | § 11.10(c) |
| DS-VSUB-89 | FS-PART11-04 | § 11.10(d) |
| DS-VSUB-90 | FS-PART11-05 | § 11.10(e) |
| DS-VSUB-91 | FS-PART11-06 | § 11.10(g) |
| DS-VSUB-92 | FS-PART11-07 | § 11.10(k) |
| DS-VSUB-93 | FS-PART11-08 | § 11.50 |
| DS-VSUB-94 | FS-PART11-09 | § 11.70 |
| DS-VSUB-95 | FS-PART11-10 | § 11.100 |
| DS-VSUB-96 | FS-PART11-11 | § 11.200 |
| DS-VSUB-97 | FS-PART11-12 | § 11.300 |
| DS-VSUB-98 | FS-DI-01 | Attributable |
| DS-VSUB-99 | FS-DI-02 | Legible |
| DS-VSUB-100 | FS-DI-03 | Contemporaneous |
| DS-VSUB-101 | FS-DI-04 | Original |
| DS-VSUB-102 | FS-DI-05 | Accurate |
| DS-VSUB-103 | FS-DI-06 | Retention + chronology |
| DS-VSUB-104 | FS-INT-VAULT-01 | QualityDocs URN |
| DS-VSUB-105 | FS-INT-VAULT-02 | Vault RIM |
| DS-VSUB-106 | FS-INT-VAULT-03 | Vault eTMF |
| DS-VSUB-107 | FS-INT-VAULT-04 | Vault PromoMats |
| DS-VSUB-108 | FS-INT-VIG-01 | Sirius PV |
| DS-VSUB-109 | FS-INT-SPOR-01 | EMA SPOR |
| DS-VSUB-110 | FS-INT-EVAL-01 | LORENZ eValidator |
| DS-VSUB-111 | FS-INT-DOCB-01 | LORENZ docuBridge |
| DS-VSUB-112 | FS-INT-TRANS-01 | Translation vendor |
| DS-VSUB-113 | FS-INT-SSO-01 | Okta SSO |
| DS-VSUB-114 | FS-PERF-01 | Sequence-compile P95 |
| DS-VSUB-115 | FS-PERF-02 | eValidator P95 |
| DS-VSUB-116 | FS-PERF-03 | Archive retrieval P95 |
| DS-VSUB-117 | FS-AV-01 | Vendor SLA |
| DS-VSUB-118 | FS-AV-02 | RPO / RTO |
| DS-VSUB-119 | FS-BAK-01 | Backup |
| DS-VSUB-120 | FS-BAK-02 | Quarterly tenant export |
| DS-VSUB-121 | FS-SEC-01 | RBAC matrix |
| DS-VSUB-122 | FS-SEC-02 | TLS / AES |
| DS-VSUB-123 | FS-SEC-03 | Pen-test |
| DS-VSUB-124 | FS-LIFE-01 | App-lifecycle tracker |
| DS-VSUB-125 | FS-LIFE-02 | App status |
| DS-VSUB-126 | FS-LIFE-03 | Approval-letter + EPAR + label-of-record |
| DS-VSUB-127 | FS-LIFE-04 | Lifecycle milestone alerts |
| DS-VSUB-128 | FS-MEET-01 | Meeting tracker |
| DS-VSUB-129 | FS-MEET-02 | Briefing-doc submission |
| DS-VSUB-130 | FS-MEET-03 | Meeting-feedback forwarding |
| DS-VSUB-131 | FS-SPL-01 | FDA SPL generator |
| DS-VSUB-132 | FS-SPL-02 | SPL versioning |
| DS-VSUB-133 | FS-SPL-03 | Drug-listing + establishment-registration |
| DS-VSUB-134 | FS-REF-01 | Document-reuse tracker (DMF) |
| DS-VSUB-135 | FS-REF-02 | LoA tracker |
| DS-VSUB-136 | FS-REF-03 | DMF status |
| DS-VSUB-137 | FS-RWD-01 | RWE submission support |
| DS-VSUB-138 | FS-RWD-02 | PFDD submission support |
| DS-VSUB-139 | FS-DASH-01 | Submissions dashboard |
| DS-VSUB-140 | FS-DASH-02 | Per-publisher KPI |
| DS-VSUB-141 | FS-DASH-03 | Time histograms |
| DS-VSUB-142 | FS-COMBO-01 | Combination-product routing |
| DS-VSUB-143 | FS-COMBO-02 | Combination-product M3+M5 |
| DS-VSUB-144 | FS-PROF-VAL-01 | Per-submission-type validation profile |
| DS-VSUB-145 | FS-PROF-VAL-02 | Profile change control |
| DS-VSUB-146 | FS-COVER-01 | Per-region cover-letter templates |
| DS-VSUB-147 | FS-COVER-02 | Form generators |
| DS-VSUB-148 | FS-COVER-03 | Cover-letter version control |
| DS-VSUB-149 | FS-XINT-HYD-01 | Hydra egress ACL |
| DS-VSUB-150 | FS-XINT-HYD-02 | Hydra use-cases + Annex I gate |
| DS-VSUB-151 | FS-XINT-HYD-03 | Vault binder ingestion hook |
| DS-VSUB-152 | FS-XINT-HYD-04 | Per-section hash verification |
| DS-VSUB-153 | FS-XINT-HYD-05 | Helios Hydra topic |
| DS-VSUB-154 | FS-XINT-HEL-01 | Helios submissions topic |
| DS-VSUB-155 | FS-XINT-HEL-02 | Helios reconciliation |
| DS-VSUB-156 | FS-XINT-EDMS-01 | EDMS read adapter |
| DS-VSUB-157 | FS-XSYS-BAK-01 | Backup integration |
| DS-VSUB-158 | FS-XSYS-AD-01 | AD identity integration |
| DS-VSUB-159 | FS-TRN-01 | LMS training gate |
| DS-VSUB-160 | FS-TRN-02 | Annual refresher |
| DS-VSUB-161 | FS-PR-01 | Annual periodic review |
| DS-VSUB-162 | FS-INSP-01 | Inspection-readiness export |
| DS-VSUB-163 | FS-INSP-02 | HA-correspondence register |
| DS-VSUB-164 | FS-INSP-03 | CA-query response workflow |
| DS-VSUB-165 | FS-INSP-04 | Mock-audit rehearsal |

---

## 11. Design-Level Risk Register

| ID | Design-level risk | Likelihood | Impact | Mitigation reference (DS) |
|---|---|---|---|---|
| DR-01 | Invalid eCTD compilation accepted at submission window | Medium | High | DS-VSUB-23 DTD/XSD + DS-VSUB-26..30 LORENZ validation |
| DR-02 | Gateway loss during submission window | Medium | High | DS-VSUB-60 quarterly connectivity test + DS-VSUB-61 maintenance window calendar |
| DR-03 | Submission of unapproved content | Low | Critical | DS-VSUB-33 sequence-release re-auth + DS-VSUB-08 SoD |
| DR-04 | Sequence numbering gap | Medium | High | DS-VSUB-31 gap-free generator + DS-VSUB-35 conflict detector |
| DR-05 | Wrong M1 region package for jurisdiction | Medium | High | DS-VSUB-21 region templates + DS-VSUB-72 region-language matrix |
| DR-06 | IDMP referential drift breaking EU variation submission | Low | High | DS-VSUB-65 quarterly drift-detection job |
| DR-07 | LORENZ criteria-pack drift breaks compile | Medium | Medium | DS-VSUB-29 criteria-pack version pinned per submission |
| DR-08 | Translation-vendor slip blocks regional submission | Medium | Medium | DS-VSUB-74 lifecycle tracking + vendor SLA |
| DR-09 | Sequence-diff misinterpretation by reviewer | Low | High | DS-VSUB-47 docuBridge + reviewer training |
| DR-10 | Archive retrieval > 4 h during inspection | Low | High | DS-VSUB-49 retrieval P95 + DS-VSUB-162 inspection-readiness export |
| DR-11 | xlink:href dangling between leaves | Medium | High | DS-VSUB-32 xlink validation at compile |
| DR-12 | Style / format non-compliance per agency stylesheet | Medium | Medium | DS-VSUB-39..46 per-agency PDF + style checks |
| DR-13 | Granularity mismatch with agency expectation | Low | Medium | DS-VSUB-36..38 granularity policy + impact analysis |
| DR-14 | Audit-trail tampering | Low | Critical | DS-VSUB-83 vendor-controlled append-only + TR-Audit |
| DR-15 | Multi-country variation drift | Medium | High | DS-VSUB-78..81 variation master + dependency graph |
| DR-16 | Hydra-drafted content (DS-VSUB-150) ships missing Art. 11 pack | Low | Critical | Hydra gateway-side 403 + binder finalisation hook DS-VSUB-151 |
| DR-17 | Hydra watermark mismatch (DS-VSUB-152) on a true positive — legitimate edit rejected | Low | Medium | MasterControl deviation review + audit-trail entry |
| DR-18 | EDMS read adapter (DS-VSUB-156) drift on doc version effective change after binder lock | Medium | High | sha256 pin at binder time + drift triggers re-validation |
| DR-19 | Combination-product routing (DS-VSUB-142) mis-classified between CDER and CBER | Low | High | OCP-assigned classification + dual-Center coordination workflow |
| DR-20 | Per-submission-type validation profile (DS-VSUB-144) outdated after FDA spec change | Medium | High | DS-VSUB-145 profile change control + DS-VSUB-161 annual periodic review |

The DS Design-level Risk Register is the design-stage seed for `BLR-RA-VSUB-001`; per-FS-ID criticality remains in the FS Implementation Risk Register.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
