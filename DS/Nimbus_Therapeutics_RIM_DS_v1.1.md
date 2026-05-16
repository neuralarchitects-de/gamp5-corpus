---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "NIM-FS-RIM-001 v1.3 (parent FS)"
  - "NIM-URS-RIM-001 v1.3 (parent URS, transitive)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 Configuration Specification conventions"
  - "21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300; 21 CFR Parts 312 + 314"
  - "ICH M2 ESTRI; ICH M4 CTD; ICH M8 eCTD"
  - "EMA EU Module 1; EMA Q&A on eCTD v4"
  - "IDMP ISO 11238 / 11239 / 11240 / 11615 / 11616"
  - "EMA SPOR (SMS / PMS / OMS / RMS)"
  - "FDA Electronic Submissions Gateway (ESG) Guidance"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026; supersedes the September 2025 guidance)"
  - "EU CTR 536/2014 Arts. 25, 81; EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "Veeva Vault RIM Suite 24R3 — Validation Approach + Configuration Reference"
parent_fs:
  document_number: NIM-FS-RIM-001
  version: 1.3
  file: ../../../FS_FDS/_generated/final/Nimbus_Therapeutics_RIM_FS_v1.3.md
parent_urs:
  document_number: NIM-URS-RIM-001
  version: 1.3
  file: ../../../URS/_generated/final/RIM_Regulatory_Information_Management__Nimbus_Therapeutics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## RIM — Veeva Vault RIM Suite 24R3 (Submissions + Registrations + Submissions Archive + IDMP) — Configuration Specification

**Document Number:** NIM-DS-RIM-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Parent FS:** NIM-FS-RIM-001 v1.3
**Parent URS:** NIM-URS-RIM-001 v1.3 *(informational; transitive via FS)*
**Site:** Nimbus Therapeutics *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Project Mode:** Sustaining + Configurable Change *(inherited from parent URS)*
**Regulatory Scope:** 21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300; 21 CFR Parts 312 + 314; ICH M2 + M4 + M8; EMA Module 1 + Q&A eCTD v4; IDMP ISO 11238/11239/11240/11615/11616; EMA SPOR; FDA ESG; FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance); FDA *Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions* (Aug 2025); EU CTR 536/2014 Arts. 25/81; EU GMP Annex 11 §§ 4, 6, 9, 11; GDPR Arts. 6, 32; ISO/IEC 27001:2022; PIC/S PI 041.

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QA Reviewer) | _____________ | _____________ | _____ |
| Reviewer (System Owner — Head of Regulatory Operations) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — VP Global Regulatory Affairs) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Privacy / DPO) | _____________ | _____________ | _____ |
| Approver (VP Global Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Design Control

| Field | Value |
|---|---|
| Document Number | NIM-DS-RIM-001 |
| Version | 1.1 |
| Effective Date *(synthetic)* | 2026-05-15 |
| Parent FS | NIM-FS-RIM-001 v1.3 |
| Parent URS *(informational)* | NIM-URS-RIM-001 v1.3 |
| Site | Nimbus Therapeutics *(fictional)* |
| System Class (GAMP 5, 2nd ed.) | Category 4 — Configured Product (multi-tenant SaaS) |
| Project Mode | Sustaining + Configurable Change |
| Regulatory Scope | per Title block |
| Tier | T3 (inherited from parent URS+FS pair) |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue of Configuration Specification for Veeva Vault RIM Suite 24R3 (Submissions + Registrations + Submissions Archive + IDMP) corresponding to NIM-FS-RIM-001 v1.3. Inherited Tier T3 from parent URS+FS pair. DS covers 107/107 FS-IDs (100% coverage). Vendor-internal Veeva Vault platform internals are flagged as **vendor-internal — no site design surface**. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from NIM-URS-RIM-001 v1.3 and NIM-FS-RIM-001 v1.3. DS-specific additions:

| Term | Definition |
|---|---|
| HA | Health Authority (regional regulator) |
| eCTD | electronic Common Technical Document |
| M1 | Module 1 (region-specific administrative information) |
| M4 | Module 4 (Non-clinical Study Reports per ICH M4) |
| M8 | electronic CTD specification (ICH M8) |
| IDMP | Identification of Medicinal Products (ISO 11238 / 11239 / 11240 / 11615 / 11616) |
| SPOR | Substances, Products, Organisations, Referentials (EMA master data) |
| ESG | FDA Electronic Submissions Gateway |
| MPID | Medicinal Product Identifier (ISO 11615) |
| PhPID | Pharmaceutical Product Identifier (ISO 11616) |
| UNII | Unique Ingredient Identifier (FDA) |
| EDQM | European Directorate for the Quality of Medicines |

---

## 1. Purpose

This Configuration Specification defines, at the platform-tenancy level, the configuration values, lifecycle state-machine design, workflow + signature designs, role-permission matrix, and integration endpoint designs that implement NIM-FS-RIM-001 v1.3 for the Nimbus Vault RIM Suite 24R3 tenancy. It is the third document in the GAMP 5 V-model for the Nimbus Regulatory Information Management platform.

## 2. Scope

### 2.1 In Scope

- Vault RIM Suite 24R3 tenancy configuration — Submissions + Registrations + Submissions Archive + Product Master (IDMP) modules; per-region eCTD configuration; document lifecycle state machine; e-signature workflows.
- Submission Planning + Sequence Build / Validate / Dispatch design.
- Registrations + IDMP master-data design.
- EMA SPOR nightly sync design.
- HA Correspondence + Commitments + Variations + Renewals design.
- Integration design — Okta SAML 2.0 + MFA + SCIM; Vault QualityDocs (Vellis); Vault eTMF (Marinos); Sirius Argus PV; FDA ESG; EMA SPOR; regional HA gateways.
- Cross-system planes — AD identity, AUR backup tier.

### 2.2 Out of Scope

- Per-product submission body content (per-product DS sub-documents).
- Vendor platform internals (Veeva SDLC).
- Cross-system AD design (QTZ-DS-AD-001).
- Cross-system backup design (AUR-DS-BACKUP-001).

## 3. Architectural Overview

The Nimbus Vault RIM platform is a **multi-tenant SaaS** Cat 4 system functioning as the Global Regulatory Operations hub. It manages submission planning, sequence build / validate / dispatch / archive, registration tracking, IDMP master data, EMA SPOR synchronisation, HA correspondence, commitments / variations / renewals across FDA, EMA, PMDA, Health Canada, TGA, ANVISA, NMPA.

### 3.1 Platform Architectural Diagram

```
                Okta SSO + MFA (SAML 2.0 + SCIM 2.0)
                       │
                       ▼
   ┌────────────────────────────────────────────────────────────────────────┐
   │     Vault RIM Suite 24R3 (Nimbus tenancy)                              │
   │                                                                        │
   │   ┌─────────────────────────────────────────────────────────────┐      │
   │   │  Submissions module                                          │      │
   │   │  • Sequence builder (per-HA M1 + M4/M8)                      │      │
   │   │  • Validator (per-HA rule sets)                              │      │
   │   │  • Lifecycle ops (new/append/replace/delete per ICH M8)      │      │
   │   │  • Unique sequence numbering (per-HA per-product)            │      │
   │   │  • SHA-256 sequence-content hash                              │      │
   │   │  • Preview (HA-style view)                                    │      │
   │   └─────────────────────────────────────────────────────────────┘      │
   │   ┌─────────────────────────────────────────────────────────────┐      │
   │   │  Registrations module                                         │     │
   │   │  • Registration records per product / country                │      │
   │   │  • Variations / renewals / line extensions                   │      │
   │   │  • Approval-letter + label-version + indication-version      │      │
   │   └─────────────────────────────────────────────────────────────┘      │
   │   ┌─────────────────────────────────────────────────────────────┐      │
   │   │  Submissions Archive (immutable, ≥ 30 y)                     │      │
   │   └─────────────────────────────────────────────────────────────┘      │
   │   ┌─────────────────────────────────────────────────────────────┐      │
   │   │  Product Master (IDMP — ISO 11238 / 11239 / 11240 /          │      │
   │   │  11615 / 11616)                                              │      │
   │   └─────────────────────────────────────────────────────────────┘      │
   │   ┌─────────────────────────────────────────────────────────────┐      │
   │   │  HA Correspondence + Commitments + Variations + Renewals     │      │
   │   └─────────────────────────────────────────────────────────────┘      │
   └─┬─────────────┬─────────────┬──────────────┬─────────────────────────┘
     │             │             │              │
     ▼             ▼             ▼              ▼
   Vault       Vault         EMA SPOR        FDA ESG +
   Quality-    eTMF          (SMS / PMS /    EMA gateway +
   Docs        (Marinos)     OMS / RMS)      PMDA + HC +
   (Vellis)                                  TGA + ANVISA +
                                             NMPA
       │
       ▼
   ┌────────────────────────────────────────────────────────────────────────────┐
   │  Cross-system planes                                                       │
   │  • QTZ AD / Entra ID (SAML+SCIM, Splunk gxp-authn, CyberArk PAM)           │
   │  • AUR Backup (Veeam + MS SQL VSS + object-replica for submission          │
   │    artefacts + S3 Object Lock + LTO-9 air-gap)                             │
   └────────────────────────────────────────────────────────────────────────────┘
```

### 3.2 Document Lifecycle State Machine

```
   ┌─────────┐    ┌──────────┐   ┌──────────┐   ┌─────────────────┐   ┌───────────┐   ┌────────────┐
   │  DRAFT  │───►│IN-REVIEW │──►│ APPROVED │──►│ READY-TO-PUBLISH│──►│ PUBLISHED │──►│ SUPERSEDED │
   └─────────┘    └──────────┘   └──────────┘   └─────────────────┘   └───────────┘   └────────────┘
                                                       │                                              
                                                       ▼                                              
                                               (SHA-256 content hash recorded; verified at dispatch)
```

### 3.3 Counterparty Integration Map

| Counterparty | Protocol | Direction | Endpoint pattern | Auth | FS-ID |
|---|---|---|---|---|---|
| Okta IdP | SAML 2.0 + SCIM 2.0 | bidirectional | `nimbus.okta.com` | TLS 1.3 + mutual cert | FS-INT-SSO-01 |
| Vault QualityDocs (Vellis) | Vault Connect | inbound | `vellis.veevavault.com` | OAuth2 | FS-INT-EDMS-01 |
| Vault eTMF (Marinos) | Vault Connect | bidirectional | `marinos.veevavault.com` | OAuth2 | FS-INT-ETMF-01 |
| Sirius Argus PV | REST cross-link | bidirectional | `sirius.veevavault.com` | OAuth2 | FS-INT-PV-01 |
| FDA ESG | AS2 | outbound | per FDA ESG spec | AS2 SHA-256 | FS-INT-ESG-01 |
| EMA SPOR | REST (OAuth 2.0) | bidirectional | `spor.ema.europa.eu` | OAuth2 + nightly sync | FS-INT-SPOR-01 |
| EMA Gateway | per-HA | outbound | `cesp.ema.europa.eu` | per-HA cert | FS-PLN-* / FS-SEQ-05 |
| PMDA Gateway | per-HA | outbound | PMDA spec | per-HA cert | FS-SEQ-05 |
| Health Canada (HC) | per-HA | outbound | HC spec | per-HA cert | FS-SEQ-05 |
| TGA | per-HA | outbound | TGA spec | per-HA cert | FS-SEQ-05 |
| ANVISA | per-HA | outbound | ANVISA spec | per-HA cert | FS-SEQ-05 |
| NMPA | per-HA | outbound | NMPA spec | per-HA cert | FS-SEQ-05 |
| Vault Connect API | OAuth 2.0 client-credentials | bidirectional | per-vault | short-lived tokens | FS-INT-API-01 |

---

## 4. Configuration Specification

### 4.1 Tenancy + SSO + Vendor-Assurance Configuration

| CI-ID | Configuration item (Veeva-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RIM-01 | Vault IdP Mode | `Okta SAML 2.0 + MFA + SCIM 2.0` | Custom | Per FS-INT-SSO-01 + FS-PART11-04. | FS-INT-SSO-01, FS-PART11-04, FS-XSYS-AD-01 | OQ-AUTHN-01 |
| DS-RIM-02 | Vault Connect Auth | `OAuth 2.0 client-credentials; short-lived tokens (15 min)` | Custom | Per FS-INT-API-01. | FS-INT-API-01, FS-PART11-08 | OQ-API-01 |
| DS-RIM-03 | Service-Account Auth | `mTLS only` | Custom | Per FS-PART11-04. | FS-PART11-04 | OQ-SA-01 |
| DS-RIM-04 | Conditional-Access Policy | `Regulatory-App Conditional Access (FIDO2 phishing-resistant MFA)` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-CA-01 |
| DS-RIM-05 | SIEM Forwarding | `Splunk gxp-authn syslog RFC 5424; lag ≤ 5 min` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-SIEM-01 |
| DS-RIM-06 | PAM Break-Glass | `CyberArk PAM — 24 h rotation + dual-witness` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-PAM-01 |
| DS-RIM-07 | Vendor-Assurance Dossier | `SOC 2 Type II + ISO/IEC 27001:2022 + Veeva CSV summary for 24R3; annual re-qualification` | Custom | Per FS-VND-01. | FS-VND-01 | IQ-VND-01 |
| DS-RIM-08 | Release-Note Workflow | `RNS feed → impact-assessment → change-control record within 14 days` | Custom | Per FS-VND-02. | FS-VND-02 | OQ-VND-01 |
| DS-RIM-09 | SDLC Evidence Review Cadence | `Annual` | Custom | Per FS-VND-03. | FS-VND-03 | OQ-VND-02 |
| DS-RIM-10 | Sub-Processor List Review | `Quarterly per DPA Annex II` | Custom | Per FS-VND-04. | FS-VND-04 | OQ-VND-03 |
| DS-RIM-11 | Force-Reauth at Approval / Dispatch | `Max-age 5 min OAuth2 token` | Custom | Per FS-PART11-12. | FS-PART11-12 | OQ-PART11-200 |
| DS-RIM-12 | Account Lockout | `5 failures / 15 minutes` | Custom | Per FS-PART11-13. | FS-PART11-13 | OQ-PART11-300 |

### 4.2 Region / eCTD / Module 1 Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RIM-13 | Country / Region / Product Metadata | `Maintained under change control via DEV → UAT → PROD` | Custom | Per FS-CFG-01 + FS-CCM-01. | FS-CFG-01, FS-CCM-01 | OQ-CFG-01 |
| DS-RIM-14 | eCTD Configuration | `FDA / EMA / PMDA / HC / TGA / ANVISA / NMPA Module 1 + ICH M4 + M8 maintained to current; updates impact-assessed ≤ 30 d` | Custom | Per FS-CFG-02 + FS-CCM-04. | FS-CFG-02, FS-CCM-04 | OQ-CFG-02 |
| DS-RIM-15 | Region-Specific Module 1 Controlled Vocabularies | `Tracked per HA terminology service` | Custom | Per FS-CFG-03. | FS-CFG-03 | OQ-CFG-03 |
| DS-RIM-16 | Lifecycle States | `DRAFT → IN-REVIEW → APPROVED → READY-TO-PUBLISH → PUBLISHED → SUPERSEDED` | Custom | Per FS-CFG-04. | FS-CFG-04 | OQ-LIFECYCLE-01 |
| DS-RIM-17 | Lifecycle Transition SoD | `E-sig with SoD enforcement (author ≠ reviewer ≠ approver)` | Custom | Per FS-CFG-05. | FS-CFG-05 | OQ-LIFECYCLE-02 |
| DS-RIM-18 | eCTD v4 Readiness | `Per-HA feature flag; switchover guarded per HA-published v4 timelines` | Custom | Per FS-CFG-06. | FS-CFG-06 | OQ-CFG-04 |

### 4.3 Submission Planning Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RIM-19 | Multi-Region Submission Plan Template | `Target HA dates, content-owner assignment, dependencies, milestone tracking` | Custom | Per FS-PLN-01. | FS-PLN-01 | OQ-PLN-01 |
| DS-RIM-20 | Critical-Path Alerts | `D-60 / D-30 / D-14 / D-7 / D-0 configurable per submission` | Custom | Per FS-PLN-02. | FS-PLN-02 | OQ-PLN-02 |
| DS-RIM-21 | Per-Region Status Vocabulary | `Planned, In Build, In Review, Ready to Publish, Published, Acknowledged, Approved, Withdrawn` | Custom | Per FS-PLN-03. | FS-PLN-03 | OQ-PLN-03 |
| DS-RIM-22 | Resource-Planning View | `Workload per role vs submission deadlines` | Custom | Per FS-PLN-04. | FS-PLN-04 | OQ-PLN-04 |
| DS-RIM-23 | Plan Baseline + Revisions | `Retained for retrospective slip analysis` | Custom | Per FS-PLN-05. | FS-PLN-05 | OQ-PLN-05 |

### 4.4 Sequence Build / Validate / Dispatch Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RIM-24 | Sequence Builder | `Per-HA M1 + M4/M8 modules; missing required documents block build` | Custom | Per FS-SEQ-01. | FS-SEQ-01 | OQ-SEQ-01 |
| DS-RIM-25 | Per-HA Validator Rule Sets | `FDA, EMA, PMDA, HC, TGA, ANVISA, NMPA; failure blocks dispatch` | Custom | Per FS-SEQ-02. | FS-SEQ-02 | OQ-SEQ-02 |
| DS-RIM-26 | Lifecycle Operators | `new / append / replace / delete per ICH M8; integrity verified on build` | Custom | Per FS-SEQ-03. | FS-SEQ-03 | OQ-SEQ-03 |
| DS-RIM-27 | Sequence Numbering | `Unique per HA per product (DB constraint); gaps blocked` | Custom | Per FS-SEQ-04. | FS-SEQ-04 | OQ-SEQ-04 |
| DS-RIM-28 | Gateway Dispatch + ACK Reconciliation | `FDA ESG, EMA gateway, regional; MDN / ACK returned; non-ACK within window escalates` | Custom | Per FS-SEQ-05 + FS-INT-ESG-01. | FS-SEQ-05, FS-INT-ESG-01 | OQ-SEQ-05 |
| DS-RIM-29 | Cross-Reference Job | `Table to eTMF + QualityDocs; monthly broken-reference report` | Custom | Per FS-SEQ-06. | FS-SEQ-06 | OQ-SEQ-06 |
| DS-RIM-30 | Sequence-Content Hash | `SHA-256 recorded at READY-TO-PUBLISH; matched against Archive hash on dispatch` | Custom | Per FS-SEQ-07. | FS-SEQ-07 | OQ-SEQ-07 |
| DS-RIM-31 | Sequence Preview | `HA-style view pre-dispatch` | Custom | Per FS-SEQ-08. | FS-SEQ-08 | OQ-SEQ-08 |

### 4.5 Submissions Archive Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RIM-32 | Auto-Archive on Dispatch | `Dispatched sequence + ACK; SHA-256 checksums recorded` | Custom | Per FS-ARC-01. | FS-ARC-01 | OQ-ARC-01 |
| DS-RIM-33 | Archive Immutability | `Immutable; retrieval ≤ 4 BH during inspection` | Custom | Per FS-ARC-02. | FS-ARC-02 | OQ-ARC-02 |
| DS-RIM-34 | Archive Retention | `≥ 30 y post-licence-discontinuation; longer per jurisdictional minimums` | Custom | Per FS-ARC-03. | FS-ARC-03 | OQ-ARC-03 |
| DS-RIM-35 | Archive Integrity Verification | `Quarterly job; failures deviated + remediated` | Custom | Per FS-ARC-04. | FS-ARC-04 | OQ-ARC-04 |
| DS-RIM-36 | Archive Export Formats | `eCTD v3.2.2 + v4` | Custom | Per FS-ARC-05. | FS-ARC-05 | OQ-ARC-05 |

### 4.6 Registrations + IDMP Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RIM-37 | Registration Object Schema | `Per product / country; states {PLANNED, IN-REVIEW, APPROVED, SUSPENDED, WITHDRAWN}; transitions audit-trailed` | Custom | Per FS-REG-01. | FS-REG-01 | OQ-REG-01 |
| DS-RIM-38 | Variation / Renewal Linkage | `Linked to parent registration with submission-sequence linkage` | Custom | Per FS-REG-02. | FS-REG-02 | OQ-REG-02 |
| DS-RIM-39 | Approval-Letter + Label-Version + Indication-Version Linkage | `Per registration` | Custom | Per FS-REG-03. | FS-REG-03 | OQ-REG-03 |
| DS-RIM-40 | MPID Entity (ISO 11615) | `Medicinal Product identifiers per HA region` | Custom | Per FS-IDMP-01. | FS-IDMP-01 | OQ-IDMP-01 |
| DS-RIM-41 | Substance Entity (ISO 11238) | `UNII + EMA SMS identifiers reconciled` | Custom | Per FS-IDMP-02. | FS-IDMP-02 | OQ-IDMP-02 |
| DS-RIM-42 | PhPID Entity (ISO 11616) | `Pharmaceutical Product identifiers` | Custom | Per FS-IDMP-03. | FS-IDMP-03 | OQ-IDMP-03 |
| DS-RIM-43 | Dose-Form / Route / Packaging (ISO 11239) | `EDQM controlled vocabulary` | Custom | Per FS-IDMP-04. | FS-IDMP-04 | OQ-IDMP-04 |
| DS-RIM-44 | Units of Measurement (ISO 11240) | `UCUM mapping` | Custom | Per FS-IDMP-05. | FS-IDMP-05 | OQ-IDMP-05 |
| DS-RIM-45 | IDMP Export Formats | `HL7 FHIR R5 + ISO XML for HA submissions; schema validated in CI` | Custom | Per FS-IDMP-06. | FS-IDMP-06 | OQ-IDMP-06 |

### 4.7 EMA SPOR Sync Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RIM-46 | SMS (Substance) Sync | `Nightly; conflict queue` | Custom | Per FS-SPOR-01. | FS-SPOR-01 | OQ-SPOR-01 |
| DS-RIM-47 | PMS (Product) Sync | `Nightly; conflict queue` | Custom | Per FS-SPOR-02. | FS-SPOR-02 | OQ-SPOR-02 |
| DS-RIM-48 | OMS (Organisation) Sync | `Nightly; conflict queue` | Custom | Per FS-SPOR-03. | FS-SPOR-03 | OQ-SPOR-03 |
| DS-RIM-49 | RMS (Referential Vocab) Sync | `Nightly; conflict queue` | Custom | Per FS-SPOR-04. | FS-SPOR-04 | OQ-SPOR-04 |
| DS-RIM-50 | Conflict-Resolution UI | `Product Master Steward; decisions audit-trailed` | Custom | Per FS-SPOR-05. | FS-SPOR-05 | OQ-SPOR-05 |
| DS-RIM-51 | SPOR Drift Threshold | `> 5% → deviation` | Custom | Per FS-SPOR-06. | FS-SPOR-06 | OQ-SPOR-06 |

### 4.8 HA Correspondence + Commitments + Variations + Renewals Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RIM-52 | Correspondence Schema | `Inbound + outbound; classification + source + target + response-required + due-date` | Custom | Per FS-COR-01. | FS-COR-01 | OQ-COR-01 |
| DS-RIM-53 | Correspondence Alert Ladder | `D-30 / D-14 / D-7 / D-0; overdue escalates to VP Reg Affairs` | Custom | Per FS-COR-02. | FS-COR-02 | OQ-COR-02 |
| DS-RIM-54 | Correspondence Cross-Link | `To commitments + variations + renewals` | Custom | Per FS-COR-03. | FS-COR-03 | OQ-COR-03 |
| DS-RIM-55 | Correspondence Search | `Archive by HA + product + submission + classification` | Custom | Per FS-COR-04. | FS-COR-04 | OQ-COR-04 |
| DS-RIM-56 | Commitments Tracking | `Per HA with due-dates; D-30 / D-7 / D-0 alerts; overdue escalates` | Custom | Per FS-CMT-01. | FS-CMT-01 | OQ-CMT-01 |
| DS-RIM-57 | Commitment States | `Open / In Progress / Submitted / Closed / Withdrawn; closure references closing sequence` | Custom | Per FS-CMT-02. | FS-CMT-02 | OQ-CMT-02 |
| DS-RIM-58 | Variation Categorisation | `EU Type IA/IB/II/III; FDA CBE/CBE-30/PAS; JP/CA categories` | Custom | Per FS-VAR-01. | FS-VAR-01 | OQ-VAR-01 |
| DS-RIM-59 | Variation Campaigns | `Multi-region simultaneous variations` | Custom | Per FS-VAR-02. | FS-VAR-02 | OQ-VAR-02 |
| DS-RIM-60 | Renewal Lead-Time Alerts | `12m / 6m / 3m / 1m` | Custom | Per FS-RNW-01. | FS-RNW-01 | OQ-RNW-01 |

### 4.9 Audit Trail + Part 11 + ALCOA+ Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RIM-61 | Audit-Trail Event Coverage | `Doc edits + lifecycle + sequence build/validate/dispatch + config + signatures + registration state + IDMP/SPOR updates` | Custom | Per FS-AUD-01. | FS-AUD-01 | OQ-AUDIT-01 |
| DS-RIM-62 | Append-Only DB Constraint | `Tenant admin lacks UPDATE / DELETE on audit rows` | Custom | Per FS-AUD-02. | FS-AUD-02 | OQ-AUDIT-02 |
| DS-RIM-63 | Audit-Trail Review Cadence | `Monthly by Head of Reg Ops; evidence in /reviews/audit/` | Custom | Per FS-AUD-03. | FS-AUD-03 | OQ-AUDIT-03 |
| DS-RIM-64 | Audit-Trail Retention | `≥ 30 y post-licence-discontinuation` | Custom | Per FS-AUD-04. | FS-AUD-04 | OQ-AUDIT-04 |
| DS-RIM-65 | § 11.10(a) Procedural Controls SOP | `Linked from system docs` | Custom | Per FS-PART11-01. | FS-PART11-01 | OQ-PART11-10a |
| DS-RIM-66 | § 11.10(b) Copy Generation | `PDF/A-3 + XML exportable` | Custom | Per FS-PART11-02. | FS-PART11-02 | OQ-PART11-10b |
| DS-RIM-67 | § 11.10(c) Retention Protection | `Throughout retention; integrity verifiable` | Custom | Per FS-PART11-03. | FS-PART11-03 | OQ-PART11-10c |
| DS-RIM-68 | § 11.10(d) Access Control | `Okta SAML 2.0 + MFA; service accounts mTLS` | Custom | Per FS-PART11-04. | FS-PART11-04 | OQ-PART11-10d |
| DS-RIM-69 | § 11.10(e) Audit Trail | `Per DS-RIM-61` | Custom | Per FS-PART11-05. | FS-PART11-05 | OQ-PART11-10e |
| DS-RIM-70 | § 11.10(g) Authority-Check Middleware | `At API + UI` | Custom | Per FS-PART11-06. | FS-PART11-06 | OQ-PART11-10g |
| DS-RIM-71 | § 11.10(k) Manual Currency | `Under change control; effective manuals → LMS R&U` | Custom | Per FS-PART11-07. | FS-PART11-07 | OQ-PART11-10k |
| DS-RIM-72 | § 11.30 Internet-Exposed Endpoints | `TLS 1.3 + short-lived tokens + IP allow-list where contracted` | Custom | Per FS-PART11-08. | FS-PART11-08 | OQ-PART11-30 |
| DS-RIM-73 | § 11.50 Signature Manifestation | `Printed name + ISO 8601 timestamp + meaning` | Custom | Per FS-PART11-09. | FS-PART11-09 | OQ-PART11-50 |
| DS-RIM-74 | § 11.70 HMAC-SHA256 Binding | `Signature → record-hash` | Custom | Per FS-PART11-10. | FS-PART11-10 | OQ-PART11-70 |
| DS-RIM-75 | § 11.100 Unique Signature-ID | `Per user; no reuse` | Custom | Per FS-PART11-11. | FS-PART11-11 | OQ-PART11-100 |
| DS-RIM-76 | § 11.200 Re-Auth | `At sequence approval + dispatch authorisation; max-age 5 min` | Custom | Per FS-PART11-12. | FS-PART11-12 | OQ-PART11-200 |
| DS-RIM-77 | § 11.300 Password / Lockout / MFA | `Per FS-PART11-13` | Custom | Per FS-PART11-13. | FS-PART11-13 | OQ-PART11-300 |
| DS-RIM-78 | ALCOA+ Attributable | `actor_id non-null on every event` | Custom | Per FS-DI-01. | FS-DI-01 | OQ-DI-01 |
| DS-RIM-79 | ALCOA+ Legible | `PDF/A-3 + XML/JSON exports` | Custom | Per FS-DI-02. | FS-DI-02 | OQ-DI-02 |
| DS-RIM-80 | ALCOA+ Contemporaneous | `NTP-synced server timestamps` | Custom | Per FS-DI-03. | FS-DI-03 | OQ-DI-03 |
| DS-RIM-81 | ALCOA+ Original | `Content preserved unaltered` | Custom | Per FS-DI-04. | FS-DI-04 | OQ-DI-04 |
| DS-RIM-82 | ALCOA+ Accurate | `Deterministic build + validate calculations` | Custom | Per FS-DI-05. | FS-DI-05 | OQ-DI-05 |
| DS-RIM-83 | ALCOA+ Retrievability | `≥ 30 y; ≤ 1 BD routine, ≤ 4 h inspection` | Custom | Per FS-DI-06. | FS-DI-06 | PQ-RETRIEVE-01 |

### 4.10 Integration Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RIM-84 | QualityDocs (Vellis) Cross-Link | `Vault Connect for controlled-document consumption` | Custom | Per FS-INT-EDMS-01. | FS-INT-EDMS-01 | OQ-EDMS-01 |
| DS-RIM-85 | eTMF (Marinos) Cross-Reference | `Vault Connect for clinical-trial artefacts` | Custom | Per FS-INT-ETMF-01. | FS-INT-ETMF-01 | OQ-ETMF-01 |
| DS-RIM-86 | PV (Sirius Argus) Cross-Link | `For PSUR / PBRER references` | Custom | Per FS-INT-PV-01. | FS-INT-PV-01 | OQ-PV-01 |
| DS-RIM-87 | Publishing Engine API | `Quarterly connectivity test` | Custom | Per FS-INT-PUBLISH-01. | FS-INT-PUBLISH-01 | OQ-PUB-01 |
| DS-RIM-88 | FDA ESG Integration | `Per FDA technical specification; credentials managed in Reg Ops vault` | Custom | Per FS-INT-ESG-01. | FS-INT-ESG-01 | OQ-ESG-01 |
| DS-RIM-89 | EMA SPOR API | `OAuth 2.0 + nightly sync` | Custom | Per FS-INT-SPOR-01. | FS-INT-SPOR-01 | OQ-SPOR-07 |
| DS-RIM-90 | Okta SSO + SCIM | `SAML 2.0 + MFA + SCIM 2.0` | Custom | Per FS-INT-SSO-01. | FS-INT-SSO-01 | OQ-AUTHN-02 |
| DS-RIM-91 | Backup Integration | `Veeam + MS SQL VSS (metadata DB) + object-replica (submission artefacts); T1; RPO ≤ 4 h; RTO ≤ 4 BH; S3 Object Lock Compliance; LTO-9 monthly` | Custom | Per FS-XSYS-BAK-01 + FS-BAK-01..02. | FS-XSYS-BAK-01, FS-BAK-01, FS-BAK-02 | OQ-BAK-01 |

### 4.11 Performance + Availability + Security Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RIM-92 | P95 Doc Open/List Target | `≤ 3 s` | Custom | Per FS-PERF-01. | FS-PERF-01 | PQ-PERF-01 |
| DS-RIM-93 | 1500-Doc Sequence Build Target | `≤ 30 min` | Custom | Per FS-PERF-02. | FS-PERF-02 | PQ-PERF-02 |
| DS-RIM-94 | Veeva SLA | `≥ 99.9% during HA-deadline windows` | Custom | Per FS-AV-01. | FS-AV-01 | OQ-AV-01 |
| DS-RIM-95 | TLS / AES Stance | `TLS 1.3 + AES-256` | Custom | Per FS-SEC-01. | FS-SEC-01 | OQ-SEC-01 |
| DS-RIM-96 | Per-Product / Per-Region Role Scoping | `Vault role-matrix` | Custom | Per FS-SEC-02. | FS-SEC-02 | OQ-SEC-02 |
| DS-RIM-97 | Annual Vendor Cert Review | `SOC 2 + ISO 27001 evidence; gaps to change control` | Custom | Per FS-SEC-03. | FS-SEC-03 | OQ-SEC-03 |
| DS-RIM-98 | Annual Pen-Test | `Author + dispatch endpoints` | Custom | Per FS-SEC-04. | FS-SEC-04 | OQ-SEC-04 |

### 4.12 Inspection-Readiness + Reporting + Training Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RIM-99 | Inspection-Readiness Dashboard | `Registrations + recent submissions + commitments + variations + correspondence backlog` | Custom | Per FS-INSP-01. | FS-INSP-01 | OQ-INSP-01 |
| DS-RIM-100 | Inspection Export | `≤ 4 BH; PDF/A-3 + machine-readable index` | Custom | Per FS-INSP-02. | FS-INSP-02 | OQ-INSP-02 |
| DS-RIM-101 | Inspector Workspace | `30-d default; watermarked; audit-trailed` | Custom | Per FS-INSP-03. | FS-INSP-03 | OQ-INSP-03 |
| DS-RIM-102 | Per-HA Pack Content | `FDA BIMO, EMA, BfArM, PEI, Swissmedic, AGES, PMDA configurable` | Custom | Per FS-INSP-04. | FS-INSP-04 | OQ-INSP-04 |
| DS-RIM-103 | Standard Reports | `Submission Pipeline, Registration Status, Commitment Aging, Variation Backlog, Correspondence Backlog, IDMP Currency, SPOR Drift` | Custom | Per FS-RPT-01. | FS-RPT-01 | OQ-RPT-01 |
| DS-RIM-104 | Full-Text Search Scope | `Respects access-control scopes` | Custom | Per FS-RPT-02. | FS-RPT-02 | OQ-RPT-02 |
| DS-RIM-105 | Ad-Hoc Report Builder | `Head of Reg Ops + Submissions Coordinator` | Custom | Per FS-RPT-03. | FS-RPT-03 | OQ-RPT-03 |
| DS-RIM-106 | Standard Report Render Perf | `≤ 5 min` | Custom | Per FS-RPT-04. | FS-RPT-04 | OQ-RPT-04 |
| DS-RIM-107 | DEV → UAT → PROD Workflow | `SoD-enforced approvals` | Custom | Per FS-CCM-01. | FS-CCM-01 | OQ-CCM-01 |
| DS-RIM-108 | Baselines + Drift Detection | `Versioned; baseline-diff` | Custom | Per FS-CCM-02. | FS-CCM-02 | OQ-CCM-02 |
| DS-RIM-109 | Vendor Release Impact-Assessment | `≤ 14 d` | Custom | Per FS-CCM-03. | FS-CCM-03 | OQ-CCM-03 |
| DS-RIM-110 | HA-Spec-Driven Regression Suite | `Tested in UAT before PROD` | Custom | Per FS-CCM-04. | FS-CCM-04 | OQ-CCM-04 |
| DS-RIM-111 | Training Gate | `Cornerstone-recorded RIM role-training; pre-PROD gate` | Custom | Per FS-TRN-01. | FS-TRN-01 | OQ-TRN-01 |
| DS-RIM-112 | Annual Refresher | `RIM-2026-ANNUAL — ICH M4/M8 + IDMP/SPOR + Module 1 changes` | Custom | Per FS-TRN-02. | FS-TRN-02 | OQ-TRN-02 |
| DS-RIM-113 | Annual Periodic Review | `Signed by Head of Reg Ops + VP Reg Affairs + Head of QA` | Custom | Per FS-PR-01. | FS-PR-01 | OQ-PR-01 |

---

## 5. Workflow + Business-Rule Design

### 5.1 Sequence Build / Validate / Dispatch Workflow

```
   [Submission Plan finalised (DS-RIM-19)]
         │
         ▼ Author selects documents from QualityDocs (DS-RIM-84)
   [DRAFT sequence — leaves bound to QualityDocs URNs (FS-DOC-01 cross-vault)]
         │
         ▼ Lifecycle: DRAFT → IN-REVIEW (DS-RIM-17 SoD: author ≠ reviewer)
   [IN-REVIEW]
         │
         ▼ Reviewer e-signature
   [APPROVED — lifecycle gate, DS-RIM-17 SoD: reviewer ≠ approver]
         │
         ▼ Approver e-signature (force-reauth, DS-RIM-11)
   [READY-TO-PUBLISH]
         │
         ▼ SHA-256 content hash computed (DS-RIM-30)
   [Per-HA validator runs (DS-RIM-25) — ERROR-class blocks dispatch]
         │
         ▼ Cross-reference broken-link check (DS-RIM-29)
   [Preview rendered (DS-RIM-31)]
         │
         ▼ Submissions Approver re-authentication (DS-RIM-76)
   [Gateway dispatch (DS-RIM-28) — FDA ESG / EMA gateway / regional]
         │
         ▼ MDN / ACK reconciliation; non-ACK within window escalates
   [PUBLISHED]
         │
         ▼ Auto-archive (DS-RIM-32) with SHA-256 manifest matched against READY-TO-PUBLISH hash
   [Submissions Archive — immutable, ≥ 30 y (DS-RIM-33..34)]
```

### 5.2 Lifecycle Operation Workflow (per ICH M8)

| Operator | Purpose | Audit-trail event | FS-ID |
|---|---|---|---|
| `new` | Add new leaf document to a sequence | `LEAF_NEW` | FS-SEQ-03 |
| `append` | Append to prior leaf (e.g., addendum) | `LEAF_APPEND` | FS-SEQ-03 |
| `replace` | Replace prior leaf | `LEAF_REPLACE` | FS-SEQ-03 |
| `delete` | Mark prior leaf as deleted (logical) | `LEAF_DELETE` | FS-SEQ-03 |

Integrity verified on build (DS-RIM-26).

### 5.3 EMA SPOR Sync Workflow

```
   [Nightly cron 02:00 UTC]
         │
         ▼
   [SMS sync (DS-RIM-46)] → [PMS sync (DS-RIM-47)] → [OMS sync (DS-RIM-48)] → [RMS sync (DS-RIM-49)]
         │
         ▼
   [Each delta: insert / update local entity OR queue conflict for resolution]
         │
         ▼ Conflict-Resolution UI (DS-RIM-50)
   [Product Master Steward resolves conflicts; decisions audit-trailed]
         │
         ▼ Daily drift report (DS-RIM-51)
   [Drift > 5% → deviation opened]
```

### 5.4 HA Correspondence Workflow

| Step | Action | Actor | FS-ID |
|---|---|---|---|
| 1 | Inbound HA correspondence received | Submissions Coordinator | FS-COR-01 |
| 2 | Classification + due-date capture | Submissions Coordinator | FS-COR-01 |
| 3 | Cross-link to commitment / variation / renewal (DS-RIM-54) | System / Coordinator | FS-COR-03 |
| 4 | Alert ladder D-30 / D-14 / D-7 / D-0 (DS-RIM-53) | System | FS-COR-02 |
| 5 | Overdue → escalate to VP Reg Affairs | System | FS-COR-02 |
| 6 | Response drafted + reviewed + approved (SoD) | Drafter → Reviewer → Approver | FS-COR-01 |
| 7 | Response dispatched via gateway | System | FS-SEQ-05 |

### 5.5 Variation Campaign Workflow

```
   [Variation Campaign defined (DS-RIM-59)]
         │
         ▼ Per-region variation classification (DS-RIM-58)
   ┌───────────────────────────────────────────────────────────────┐
   │  EU → Type IA/IB/II/III categorisation                         │
   │  FDA → CBE / CBE-30 / PAS categorisation                       │
   │  JP/CA → JP / CA categories                                    │
   └───────────────────────────────────────────────────────────────┘
         │
         ▼ Per-region sequence build (DS-RIM-24) with shared core + region M1
   [Multi-region simultaneous dispatch]
         │
         ▼ ACK reconciliation (DS-RIM-28) + tracking
   [Registration record updates (DS-RIM-38)]
```

---

## 6. Role-Permission Matrix Design

| Role | Doc Edit (DRAFT) | Review | Approve | Sequence Build | Sequence Dispatch | Registration Edit | IDMP Steward | SPOR Conflict Resolve | View Archive | Inspector Read | Vendor Release-Eval | Tenant Admin |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| RIM Author | ✓ | ✗ | ✗ | (build only) | ✗ | (limited) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| RIM Reviewer | ✗ | ✓ (author ≠ reviewer) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| RIM Approver | ✗ | ✗ | ✓ (reviewer ≠ approver) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Submissions Coordinator | ✓ | ✓ | ✗ | ✓ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | ✗ |
| Submissions Approver (Dispatch) | ✗ | ✗ | ✓ | ✗ | ✓ (re-auth required) | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | ✗ |
| Registration Manager | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | ✓ | ✗ | ✗ | ✗ |
| Product Master Steward (IDMP) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ | ✗ | ✗ |
| Head of Reg Ops | ✗ | ✓ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | ✗ |
| VP Global Reg Affairs | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | ✗ |
| Inspector (FDA / EMA / DACH / PMDA) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (time-bounded) | ✗ | ✗ |
| Vendor Assurance Owner | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ |
| Tenant Admin (Vault) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (config only) |

**Role-permission design rules:**
- **SoD enforced** — author ≠ reviewer ≠ approver per FS-CFG-05 (DS-RIM-17).
- **Sequence Dispatch** requires fresh re-authentication per FS-PART11-12 (DS-RIM-76).
- **Inspector role** time-bounded (30-d default), watermarked (DS-RIM-101).
- **Tenant Admin** excludes audit-trail UPDATE / DELETE (DS-RIM-62).

---

## 7. Integration Design

### 7.1 FDA ESG (FS-INT-ESG-01)

| Item | Value |
|---|---|
| Protocol | AS2 |
| Receipt Verification | SHA-256 |
| Credentials Management | Reg Ops vault (`hashi-vault://regops/fda-esg/credentials@v2`) |
| Connectivity Test Cadence | Quarterly |

### 7.2 EMA SPOR (FS-INT-SPOR-01)

| Item | Value |
|---|---|
| Protocol | REST + OAuth 2.0 |
| Sync Cadence | Nightly (SMS, PMS, OMS, RMS) |
| Conflict Queue Endpoint | Internal Vault UI |
| Drift Report Cadence | Daily |

### 7.3 Regional Gateways (FS-SEQ-05)

| HA | Endpoint pattern | Protocol |
|---|---|---|
| FDA | per FDA ESG | AS2 |
| EMA | CESP (Common European Submission Platform) | per EMA spec |
| PMDA | PMDA Gateway | per PMDA spec |
| Health Canada | Health Canada CESG | per HC spec |
| TGA | TGA submission portal | per TGA spec |
| ANVISA | ANVISA eCTD | per ANVISA spec |
| NMPA | NMPA eCTD | per NMPA spec |

### 7.4 Vault Cross-Vault Connections (FS-INT-EDMS-01 / FS-INT-ETMF-01 / FS-INT-PV-01)

| Counterparty | Endpoint | FS-ID |
|---|---|---|
| Vellis QualityDocs | `https://vellis.veevavault.com/connect/v1/` | FS-INT-EDMS-01 |
| Marinos eTMF | `https://marinos.veevavault.com/connect/v1/` | FS-INT-ETMF-01 |
| Sirius Argus PV | `https://sirius.veevavault.com/connect/v1/` | FS-INT-PV-01 |

### 7.5 Backup (FS-XSYS-BAK-01)

| Item | Value |
|---|---|
| Backup Solution | Veeam Application-Aware + MS SQL VSS (RIM metadata DB) + object-replica (submission artefacts) |
| Tier | T1 / RPO ≤ 4 h / RTO ≤ 4 BH |
| Immutable Cloud Tier | S3 Object Lock Compliance |
| Air-Gap Media | LTO-9 monthly |
| Restore-Test Cadence | Monthly QA-witnessed |
| Restore-Certificate Retention | ≥ 25 y |

---

## 8. Site-Deployed Components Design

| Component | Type | Source location | Owner team | Verified by |
|---|---|---|---|---|
| `sequence-content-hash-calculator` | Library | `git.nimbus-prod.local/rim/sequence-content-hash-calculator` | Reg Ops Engineering | OQ-SEQ-07 |
| `cross-reference-broken-link-job` | Scheduled (monthly) | `git.nimbus-prod.local/rim/cross-reference-broken-link-job` | Reg Ops Engineering | OQ-SEQ-06 |
| `archive-integrity-verifier` | Scheduled (quarterly) | `git.nimbus-prod.local/rim/archive-integrity-verifier` | Reg Ops Engineering | OQ-ARC-04 |
| `spor-sync-engine` | Daemon (nightly) | `git.nimbus-prod.local/rim/spor-sync-engine` | Reg Ops Engineering | OQ-SPOR-01..06 |
| `spor-drift-detector` | Scheduled (daily) | `git.nimbus-prod.local/rim/spor-drift-detector` | Reg Ops Engineering | OQ-SPOR-06 |
| `commitment-alert-engine` | Daemon | `git.nimbus-prod.local/rim/commitment-alert-engine` | Reg Ops Engineering | OQ-CMT-01 |
| `renewal-alert-engine` | Daemon | `git.nimbus-prod.local/rim/renewal-alert-engine` | Reg Ops Engineering | OQ-RNW-01 |
| `gateway-connect-quarterly` | Scheduled | `git.nimbus-prod.local/rim/gateway-connect-quarterly` | Reg Ops Engineering | OQ-ESG-01 + OQ-SEQ-05 |
| `idmp-export-engine` | Service | `git.nimbus-prod.local/rim/idmp-export-engine` | Reg Ops Engineering | OQ-IDMP-06 |
| `inspection-export-pipeline` | Service | `git.nimbus-prod.local/rim/inspection-export-pipeline` | Reg Ops Engineering | OQ-INSP-02 |
| `ectd-validator-adapter` | Library (LORENZ-eValidator-compatible) | `git.nimbus-prod.local/rim/ectd-validator-adapter` | Reg Ops Engineering | OQ-SEQ-02 |

Each repository carries a `docs/SDS.md` mini-Software-Design-Specification artefact per GAMP 5 2nd-edition § 2B.4 rule 6.

---

## 9. References

### 9.1 US

- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- 21 CFR Parts 312 + 314.
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).
- FDA *Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions* (Aug 2025).
- FDA *eCTD Technical Conformance Guide*; FDA ESG specifications.

### 9.2 EU

- EU CTR 536/2014 Arts. 25, 81.
- EMA EU Module 1 specification + Q&A on eCTD v4.
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- GDPR Arts. 6, 32.

### 9.3 DACH

- BfArM (DE); Paul-Ehrlich-Institut (DE); Swissmedic (CH); AGES PharmMed (AT).

### 9.4 International

- ICH M2 ESTRI; ICH M4 CTD; ICH M8 eCTD.
- IDMP — ISO 11238 / 11239 / 11240 / 11615 / 11616.
- EMA SPOR (SMS / PMS / OMS / RMS).
- HL7 FHIR R5.
- ISPE GAMP 5 (2nd Edition, 2022).
- PIC/S PI 041.
- ISO/IEC 27001:2022.

### 9.5 Vendor

- Veeva Systems — *Vault RIM Suite 24R3 Validation Approach*.
- Veeva Systems — *Vault RIM Suite 24R3 Configuration Reference*.
- LORENZ — *eValidator product reference* (cross-reference for eCTD validation).

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS ID | FS ID(s) | Notes |
|---|---|---|
| DS-RIM-01 | FS-INT-SSO-01 / FS-PART11-04 / FS-XSYS-AD-01 | IdP mode |
| DS-RIM-02 | FS-INT-API-01 / FS-PART11-08 | Vault Connect auth |
| DS-RIM-03 | FS-PART11-04 | Service-account auth |
| DS-RIM-04 | FS-XSYS-AD-01 | Conditional-access policy |
| DS-RIM-05 | FS-XSYS-AD-01 | SIEM forwarding |
| DS-RIM-06 | FS-XSYS-AD-01 | PAM break-glass |
| DS-RIM-07 | FS-VND-01 | Vendor-assurance dossier |
| DS-RIM-08 | FS-VND-02 | Release-note workflow |
| DS-RIM-09 | FS-VND-03 | SDLC evidence review |
| DS-RIM-10 | FS-VND-04 | Sub-processor list review |
| DS-RIM-11 | FS-PART11-12 | Force-reauth |
| DS-RIM-12 | FS-PART11-13 | Lockout |
| DS-RIM-13 | FS-CFG-01 / FS-CCM-01 | Metadata change control |
| DS-RIM-14 | FS-CFG-02 / FS-CCM-04 | eCTD configuration |
| DS-RIM-15 | FS-CFG-03 | M1 controlled vocab |
| DS-RIM-16 | FS-CFG-04 | Lifecycle states |
| DS-RIM-17 | FS-CFG-05 | Lifecycle SoD |
| DS-RIM-18 | FS-CFG-06 | eCTD v4 readiness |
| DS-RIM-19 | FS-PLN-01 | Submission plan template |
| DS-RIM-20 | FS-PLN-02 | Critical-path alerts |
| DS-RIM-21 | FS-PLN-03 | Per-region status |
| DS-RIM-22 | FS-PLN-04 | Resource-planning view |
| DS-RIM-23 | FS-PLN-05 | Plan baseline |
| DS-RIM-24 | FS-SEQ-01 | Sequence builder |
| DS-RIM-25 | FS-SEQ-02 | Per-HA validators |
| DS-RIM-26 | FS-SEQ-03 | Lifecycle operators |
| DS-RIM-27 | FS-SEQ-04 | Sequence numbering |
| DS-RIM-28 | FS-SEQ-05 / FS-INT-ESG-01 | Gateway dispatch + ACK |
| DS-RIM-29 | FS-SEQ-06 | Cross-reference job |
| DS-RIM-30 | FS-SEQ-07 | Sequence-content hash |
| DS-RIM-31 | FS-SEQ-08 | Sequence preview |
| DS-RIM-32 | FS-ARC-01 | Auto-archive |
| DS-RIM-33 | FS-ARC-02 | Archive immutability |
| DS-RIM-34 | FS-ARC-03 | Archive retention |
| DS-RIM-35 | FS-ARC-04 | Integrity verification |
| DS-RIM-36 | FS-ARC-05 | Archive export formats |
| DS-RIM-37 | FS-REG-01 | Registration object |
| DS-RIM-38 | FS-REG-02 | Variation / renewal linkage |
| DS-RIM-39 | FS-REG-03 | Approval-letter linkage |
| DS-RIM-40 | FS-IDMP-01 | MPID entity |
| DS-RIM-41 | FS-IDMP-02 | Substance entity |
| DS-RIM-42 | FS-IDMP-03 | PhPID entity |
| DS-RIM-43 | FS-IDMP-04 | Dose-form / route / packaging |
| DS-RIM-44 | FS-IDMP-05 | UoM |
| DS-RIM-45 | FS-IDMP-06 | IDMP export formats |
| DS-RIM-46 | FS-SPOR-01 | SMS sync |
| DS-RIM-47 | FS-SPOR-02 | PMS sync |
| DS-RIM-48 | FS-SPOR-03 | OMS sync |
| DS-RIM-49 | FS-SPOR-04 | RMS sync |
| DS-RIM-50 | FS-SPOR-05 | Conflict-resolution UI |
| DS-RIM-51 | FS-SPOR-06 | SPOR drift threshold |
| DS-RIM-52 | FS-COR-01 | Correspondence schema |
| DS-RIM-53 | FS-COR-02 | Alert ladder |
| DS-RIM-54 | FS-COR-03 | Cross-link |
| DS-RIM-55 | FS-COR-04 | Correspondence search |
| DS-RIM-56 | FS-CMT-01 | Commitments tracking |
| DS-RIM-57 | FS-CMT-02 | Commitment states |
| DS-RIM-58 | FS-VAR-01 | Variation categorisation |
| DS-RIM-59 | FS-VAR-02 | Variation campaigns |
| DS-RIM-60 | FS-RNW-01 | Renewal lead-time alerts |
| DS-RIM-61 | FS-AUD-01 | Audit-trail coverage |
| DS-RIM-62 | FS-AUD-02 | Append-only constraint |
| DS-RIM-63 | FS-AUD-03 | Review cadence |
| DS-RIM-64 | FS-AUD-04 | Retention |
| DS-RIM-65 | FS-PART11-01 | § 11.10(a) |
| DS-RIM-66 | FS-PART11-02 | § 11.10(b) |
| DS-RIM-67 | FS-PART11-03 | § 11.10(c) |
| DS-RIM-68 | FS-PART11-04 | § 11.10(d) |
| DS-RIM-69 | FS-PART11-05 | § 11.10(e) |
| DS-RIM-70 | FS-PART11-06 | § 11.10(g) |
| DS-RIM-71 | FS-PART11-07 | § 11.10(k) |
| DS-RIM-72 | FS-PART11-08 | § 11.30 |
| DS-RIM-73 | FS-PART11-09 | § 11.50 |
| DS-RIM-74 | FS-PART11-10 | § 11.70 |
| DS-RIM-75 | FS-PART11-11 | § 11.100 |
| DS-RIM-76 | FS-PART11-12 | § 11.200 |
| DS-RIM-77 | FS-PART11-13 | § 11.300 |
| DS-RIM-78 | FS-DI-01 | Attributable |
| DS-RIM-79 | FS-DI-02 | Legible |
| DS-RIM-80 | FS-DI-03 | Contemporaneous |
| DS-RIM-81 | FS-DI-04 | Original |
| DS-RIM-82 | FS-DI-05 | Accurate |
| DS-RIM-83 | FS-DI-06 | Retrievability |
| DS-RIM-84 | FS-INT-EDMS-01 | QualityDocs cross-link |
| DS-RIM-85 | FS-INT-ETMF-01 | eTMF cross-reference |
| DS-RIM-86 | FS-INT-PV-01 | PV cross-link |
| DS-RIM-87 | FS-INT-PUBLISH-01 | Publishing engine |
| DS-RIM-88 | FS-INT-ESG-01 | FDA ESG integration |
| DS-RIM-89 | FS-INT-SPOR-01 | EMA SPOR |
| DS-RIM-90 | FS-INT-SSO-01 | Okta SSO + SCIM |
| DS-RIM-91 | FS-XSYS-BAK-01 / FS-BAK-01..02 | Backup integration |
| DS-RIM-92 | FS-PERF-01 | P95 doc open |
| DS-RIM-93 | FS-PERF-02 | Sequence-build perf |
| DS-RIM-94 | FS-AV-01 | Veeva SLA |
| DS-RIM-95 | FS-SEC-01 | TLS/AES stance |
| DS-RIM-96 | FS-SEC-02 | Role scoping |
| DS-RIM-97 | FS-SEC-03 | Vendor cert review |
| DS-RIM-98 | FS-SEC-04 | Pen-test |
| DS-RIM-99 | FS-INSP-01 | Inspection-Readiness dashboard |
| DS-RIM-100 | FS-INSP-02 | Inspection export |
| DS-RIM-101 | FS-INSP-03 | Inspector workspace |
| DS-RIM-102 | FS-INSP-04 | Per-HA pack content |
| DS-RIM-103 | FS-RPT-01 | Standard reports |
| DS-RIM-104 | FS-RPT-02 | Full-text search |
| DS-RIM-105 | FS-RPT-03 | Ad-hoc report builder |
| DS-RIM-106 | FS-RPT-04 | Report render perf |
| DS-RIM-107 | FS-CCM-01 | DEV → UAT → PROD workflow |
| DS-RIM-108 | FS-CCM-02 | Baselines + drift |
| DS-RIM-109 | FS-CCM-03 | Vendor release impact |
| DS-RIM-110 | FS-CCM-04 | HA-spec regression suite |
| DS-RIM-111 | FS-TRN-01 | Training gate |
| DS-RIM-112 | FS-TRN-02 | Annual refresher |
| DS-RIM-113 | FS-PR-01 | Annual periodic review |

---

## 11. Design-Level Risk Register

| ID | Design-level risk | Likelihood | Impact | Mitigation reference (DS) |
|---|---|---|---|---|
| DR-01 | IDMP / SPOR conflict-queue backlog → stale product master | Medium | Medium | DS-RIM-50 (Conflict-Resolution UI) + DS-RIM-51 queue-aging alert |
| DR-02 | HA gateway certificate rotation breaks dispatch | Medium | High | Pre-rotation test in UAT (DS-RIM-110); runbook with rollback path |
| DR-03 | eCTD v4 transition window — dual-format support drift | Medium | Medium | DS-RIM-18 per-HA feature flag |
| DR-04 | Inspector-workspace credential phishing | Low | High | DS-RIM-101 short-lived tokens + watermarked downloads |
| DR-05 | Missed HA deadline (target date slip) | Medium | High | DS-RIM-20 critical-path alerts + DS-RIM-28 dispatch tracking |
| DR-06 | Incorrect sequence numbering → HA rejection | Low | High | DS-RIM-27 DB constraint (gaps blocked) |
| DR-07 | Outdated eCTD specification used | Medium | High | DS-RIM-14 update impact-assessment ≤ 30 d |
| DR-08 | eCTD submission validation failure at HA gateway | Medium | High | DS-RIM-25 + DS-RIM-28 ACK reconciliation |
| DR-09 | IDMP referential drift between local + EMA SPOR | Medium | Medium | DS-RIM-51 SPOR drift threshold |
| DR-10 | Post-approval commitment expiry not detected | Medium | High | DS-RIM-56 commitments tracking + alert ladder |
| DR-11 | Multi-region variation tracking gap | Medium | Medium | DS-RIM-58 + DS-RIM-59 variation campaigns |
| DR-12 | Audit-trail tampering on vendor side | Low | Critical | DS-RIM-62 append-only constraint + annual access review |
| DR-13 | Signature compromise (cached credentials accepted at signing) | Low | Critical | DS-RIM-11 + DS-RIM-76 force-reauth at sign |
| DR-14 | FDA ESG account credential compromise | Low | Critical | DS-RIM-88 credentials in Reg Ops vault + DS-RIM-95 TLS 1.3 |
| DR-15 | SoD enforcement (DS-RIM-17) bypassed via delegated approver role | Low | High | OQ regression + annual access review |
| DR-16 | Archive integrity quarterly check (DS-RIM-35) misses corruption on a rare-access sequence | Low | High | Annual full-scan + restore drill |
| DR-17 | Renewal lead-time alert (DS-RIM-60) silenced via configuration drift | Low | High | DS-RIM-108 baseline drift detection |
| DR-18 | Per-HA pack content (DS-RIM-102) outdated for a recently-changed HA spec | Medium | Medium | DS-RIM-109 vendor release impact-assessment + DS-RIM-110 regression |
| DR-19 | Tenant Admin role (DS-RIM-62) overprivileged via inheritance includes audit-trail UPDATE | Low | Critical | OQ regression on append-only constraint |
| DR-20 | Cross-reference broken-link job (DS-RIM-29) misses an xlink:href on a deeply-nested leaf | Low | High | Build-time validation + monthly report |

The DS Design-level Risk Register is the design-stage seed for `NIM-RA-RIM-001`; per-FS-ID criticality remains in the FS Implementation Risk Register.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
