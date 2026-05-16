---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "MAR-FS-EDC-001 v1.3 (parent FS)"
  - "MAR-URS-EDC-001 v1.3 (parent URS, transitive)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 Configuration Specification conventions"
  - "21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300"
  - "ICH E6(R3) GCP (Step 4, adopted 6 January 2025); ICH E8(R1); ICH E9(R1); ICH E2A; ICH E2B(R3); ICH M11"
  - "CDISC SDTM-IG v3.4 / ADaM-IG v1.3 / CDASH-IG v2.3 / ODM-XML v1.3.2 / Define-XML v2.1 / Dataset-JSON v1.0"
  - "EU CTR 536/2014 + CTIS Sponsor Handbook"
  - "FDA Computerized Systems Used in Clinical Investigations (May 2007)"
  - "FDA Electronic Source Data in Clinical Investigations (Sep 2013)"
  - "FDA BIMO Inspection Manual 7348.809 (updated 4 April 2025)"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026; supersedes the September 2025 guidance)"
  - "Medidata Rave EDC 2024 — Configuration Reference; Rave Architect Essentials; Medidata Trust portal"
parent_fs:
  document_number: MAR-FS-EDC-001
  version: 1.3
  file: ../../../FS_FDS/_generated/final/Marigold_Clinical_EDC_Medidata_Rave_FS_v1.3.md
parent_urs:
  document_number: MAR-URS-EDC-001
  version: 1.3
  file: ../../../URS/_generated/final/EDC_Electronic_Data_Capture_System__Marigold_Clinical_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## EDC — Medidata Rave EDC 2024 — Platform-Level Configuration Specification

**Document Number:** MAR-DS-EDC-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Parent FS:** MAR-FS-EDC-001 v1.3
**Parent URS:** MAR-URS-EDC-001 v1.3 *(informational; transitive via FS)*
**Site:** Marigold Clinical Operations GmbH, München, Germany *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Project Mode:** Sustaining + Configurable Change *(inherited from parent URS)*
**Regulatory Scope:** 21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300; ICH E6(R3) GCP (Step 4, adopted 6 January 2025); ICH E8(R1); ICH E9(R1); ICH E2A; ICH E2B(R3); ICH M11; EU CTR Regulation 536/2014 + CTIS Sponsor Handbook; FDA *Computerized Systems Used in Clinical Investigations* (May 2007); FDA *Electronic Source Data in Clinical Investigations* (Sep 2013); FDA BIMO Inspection Manual 7348.809 (4 April 2025); EMA *Guideline on Computerised Systems and Electronic Data*; GDPR Arts. 6, 9, 17, 22, 32, 33, 35; HIPAA; CDISC SDTM-IG v3.4 / ADaM-IG v1.3 / CDASH-IG v2.3 / ODM-XML v1.3.2 / Define-XML v2.1 / Dataset-JSON v1.0; ISO/IEC 27001:2022; PIC/S PI 041.

> **DS scope note.** This DS describes the **platform-level Cat 4 Configuration Specification** corresponding to MAR-FS-EDC-001 v1.3. Per-study eCRF, edit-check, derivation, and CtQ tag binding designs live in study-specific DS sub-documents (`MAR-DS-EDC-STUDYNNN`). Vendor-internal source-code design (Rave EDC, Rave Architect, Coder, RTSM) is owned by the vendor SDLC and is NOT redrawn here.

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QA Reviewer) | _____________ | _____________ | _____ |
| Reviewer (System Owner — Director Clinical Data Management) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — Director CDM) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (Privacy / DPO — GDPR / DPIA) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Vendor Assurance Owner) | _____________ | _____________ | _____ |
| Reviewer (Pharmacovigilance Lead) | _____________ | _____________ | _____ |
| Approver (VP Clinical Operations) | _____________ | _____________ | _____ |
| Approver (VP Quality Assurance) | _____________ | _____________ | _____ |

## Design Control

| Field | Value |
|---|---|
| Document Number | MAR-DS-EDC-001 |
| Version | 1.1 |
| Effective Date *(synthetic)* | 2026-05-15 |
| Parent FS | MAR-FS-EDC-001 v1.3 |
| Parent URS *(informational)* | MAR-URS-EDC-001 v1.3 |
| Site | Marigold Clinical Operations GmbH, München, Germany *(fictional)* |
| System Class (GAMP 5, 2nd ed.) | Category 4 — Configured Product (multi-tenant SaaS) |
| Project Mode | Sustaining + Configurable Change |
| Regulatory Scope | per Title block |
| Tier | T4 (inherited from parent URS+FS pair) |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue of platform-level Configuration Specification corresponding to MAR-FS-EDC-001 v1.3. Inherited Tier T4 from parent URS+FS pair. DS covers 178/178 platform-level FS-IDs (100% coverage). Six FS-IDs in the parent FS (FS-DATA-01 platform validation-engine internals; FS-AUD-02 vendor-managed append-only DB; FS-PART11-08 closed-system multi-tenant assertion; FS-BAK-01 vendor-managed backup internals; FS-SEC-05 vendor key-rotation internals; FS-AV-01 vendor SLA-tracking internals) are flagged as **vendor-internal — no site design surface** and excluded from the DS coverage percentage per METHODOLOGY § 2B.10. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from MAR-URS-EDC-001 v1.3 and MAR-FS-EDC-001 v1.3. DS-specific additions:

| Term | Definition |
|---|---|
| CS | Configuration Specification (this document — Cat 4 DS shape per METHODOLOGY § 2B.1) |
| CI | Configuration Item — a single configurable parameter with a chosen value |
| DS-ID | Design Specification identifier (this DS's row identifier) |
| Rave Architect | Medidata's study-build authoring application |
| Rave EDC Web | Medidata's data-capture web application |
| Coder | Medidata Coder (MedDRA + WHODrug coding application) |
| RTSM | Medidata Randomisation and Trial Supply Management application (or Calyx IXRS counterpart) |
| Detect | Medidata Detect (central-monitoring / RBM consumer) |
| Vellis | Marigold's controlled-document EDMS (synthetic site name) |
| eDMS | Electronic Document Management System (Vellis) |
| eQMS | Marigold's quality / CAPA system |
| LMS | Learning Management System (training currency gate) |
| Iolanthe | Marigold's ePRO counterparty (synthetic) |
| Watson | Thermo Fisher Watson LIMS (Cetus tenancy, synthetic) |
| BIMO | FDA Bioresearch Monitoring Program |
| CTIS | EU CTR Clinical Trials Information System |
| TMF RM | DIA TMF Reference Model v3.3.x |

---

## 1. Purpose

This Configuration Specification defines, at the platform-tenancy level, the concrete configuration values, workflow designs, role-permission matrices, and integration design choices that implement MAR-FS-EDC-001 v1.3. It is the third document in the GAMP 5 V-model for the Marigold Rave EDC platform — sitting between MAR-FS-EDC-001 (functional behaviour) and the per-study study-builds (downstream implementation evidence). It is the authoritative reference for the Configuration Items, workflow designs, role-permission matrices, and integration endpoints used to validate the Marigold tenancy under the Computerised System Validation programme.

The DS shall be the single design reference for IQ + OQ + PQ planning at the platform level. Per-study eCRF / edit-check / derivation configuration is covered in per-study DS sub-documents that inherit from this DS and from MAR-FS-EDC-001.

## 2. Scope

### 2.1 In Scope (platform-level)

- Medidata Rave EDC 2024 tenancy configuration (DEV / QC / UAT / PRODUCTION URL plan; SoD policy; build-promotion gates; Quick-Publish whitelist).
- Role-permission matrix at the platform level (Builder, Reviewer, Approver, Investigator, Sub-Investigator, CRA, CRA Lead, Data Manager, Director CDM, Medical Monitor, PV Lead, Coder, Inspector, DSMB Statistician).
- Audit-trail policy + watchdog design.
- Investigator-signature configuration (form + casebook scopes; meaning-string templates; PDF manifestation).
- Coder version-pinning policy (MedDRA + WHODrug).
- Vendor-assurance + release-evaluation workflow design.
- Integration design — Okta SAML 2.0 + MFA + SCIM; Coder; RTSM/IXRS; Central labs; Imaging core lab; Argus 8.4 PV; Marinos eTMF; Iolanthe ePRO; Watson LIMS; Medidata Detect (RBM); CTIS sponsor workspace; Pinnacle21 (Certara); Hydra LLM gateway; Helios audit-event bus; LMS competence adapter.
- DSMB / IDMC firewalled extract path design.
- BIMO inspection-readiness bundle design.
- DACH-locale + time-zone-aware design.
- Backup tier classification + immutability binding (Veeam + S3 Object Lock + LTO-9 air-gap per cross-system AUR-URS-BACKUP-001).

### 2.2 Out of Scope (this DS — addressed elsewhere)

- Per-study eCRF / edit-check / derivation / CtQ-tag binding (covered in study-specific DS sub-documents).
- Vendor-internal source-code design for Rave EDC, Rave Architect, Coder, RTSM (vendor SDLC).
- Cross-system Active Directory tenancy design (covered in QTZ-DS-AD-001).
- Cross-system Veeam backup-infrastructure topology design (covered in AUR-DS-BACKUP-001).
- Investigator delegation log / 1572 design (covered in DRY-DS-CTMS-001).
- ePRO instrument-version pinning design (covered in IOL2-DS-EPRO-001).

## 3. Architectural Overview

The Marigold Rave EDC platform is a **multi-tenant SaaS** Cat 4 system. The tenancy is delivered by Medidata Solutions; the design surface available to Marigold is configuration, integration, role-permissions, and study-build artefacts. Per the FS, the platform integrates with eleven counterparty systems via SAML SSO, REST, vendor-internal APIs, SFTP, DICOM, and CDISC ODM-XML / LAB. The DS specifies the chosen tenancy-level configuration values and integration endpoint designs.

### 3.1 Platform Architectural Diagram

```
                       ┌────────────────────────────────────────────┐
                       │           Okta IdP (SAML 2.0 + MFA)        │
                       │       SCIM 2.0 deprovisioning ≤ 24 h       │
                       └────────────────────┬───────────────────────┘
                                            │  SAML / SCIM
                                            ▼
  ┌─────────────────────────────────────────────────────────────────────────────┐
  │              Medidata Rave EDC 2024 tenancy (Marigold tenant)               │
  │                                                                             │
  │   ┌────────────────┐  ┌────────────────┐  ┌─────────────────────────┐       │
  │   │ Rave Architect │  │ Rave EDC Web   │  │ Tenancy Admin / Roles / │       │
  │   │  (per-study    │  │ (data capture, │  │ Audit Trail / Watchdog  │       │
  │   │   build)       │  │  queries, sig) │  │                         │       │
  │   └────────────────┘  └────────────────┘  └─────────────────────────┘       │
  │   ENV plan: marigold-dev / marigold-qc / marigold-uat / marigold (prod)     │
  └──┬─────────┬──────────┬──────────┬─────────┬─────────┬──────────┬──────────┘
     │ vendor- │ REST     │ CDISC    │ DICOM+  │ SFTP+   │ REST+    │ ODM-XML
     │ internal│ + CSV    │ LAB/ODM  │ REST    │ PGP     │ TMF RM   │ +REST
     ▼         ▼          ▼          ▼         ▼         ▼          ▼
  ┌──────┐  ┌─────────┐  ┌────────┐ ┌─────┐ ┌──────┐  ┌──────┐   ┌────────┐
  │Coder │  │ Detect  │  │Central │ │Imag.│ │Argus │  │Marinos│   │Iolanthe│
  │MedDRA│  │ RBM     │  │ labs   │ │core │ │ 8.4  │  │ eTMF  │   │ ePRO   │
  │WHODrug│ │ feed    │  │ (LAB/  │ │lab  │ │ (PV) │  │(Vault │   │ ODM-XML│
  │      │  │ /v1/rbm-│  │ ODM)   │ │     │ │      │  │ Connect│  │        │
  │      │  │ feed/   │  │        │ │     │  │      │  │/ TMF) │   │        │
  └──────┘  └─────────┘  └────────┘ └─────┘ └──────┘  └───────┘   └────────┘
     ▲         │             ▲                                          │
     │         │             │                                          │
     │         │             │                                          ▼
     │         │       ┌────────┐                            ┌──────────────────┐
     │         │       │Watson  │                            │ Pinnacle21       │
     │         │       │LIMS    │                            │ (Certara) — SDTM │
     │         │       │(Cetus) │                            │ + Define-XML     │
     │         │       └────────┘                            │ validation       │
     │         │                                              └──────────────────┘
     │         │
     ▼         ▼
  ┌────────────────────────────────────────────────────────────────────────────┐
  │  Cross-system planes                                                       │
  │  • QTZ AD / Entra ID (SAML+SCIM, Splunk gxp-authn, CyberArk PAM break-     │
  │    glass)                                                                  │
  │  • AUR Backup (Veeam + Oracle RMAN + S3 Object Lock + LTO-9 air-gap)       │
  │  • Hydra LLM gateway (egress ACL; CLIN-PROTO-DRAFT use-case)               │
  │  • Helios audit-event bus (Kafka helios.ingest.marigold.{hydra,rave}.v1)   │
  │  • LMS competence adapter (mTLS GET /lms/competence/{user_id})             │
  │  • CTIS sponsor workspace (Marigold Reg Affairs–mediated)                  │
  │  • BfArM + PEI national-CA gateways (DACH carve-out routes)                │
  └────────────────────────────────────────────────────────────────────────────┘
```

### 3.2 Environment Plan

| Environment | URL pattern | Subject data | Promotion source | Promotion target |
|---|---|---|---|---|
| DEV | `marigold-dev.mdsol.com` | Synthetic only | (none — author here) | QC (Rave Architect promote) |
| QC | `marigold-qc.mdsol.com` | Synthetic only | DEV | UAT |
| UAT | `marigold-uat.mdsol.com` | Synthetic + IRB-approved test subjects | QC | PRODUCTION |
| PRODUCTION | `marigold.mdsol.com` | Real subject data | UAT (signed promote) | (none — terminal) |

DEV → PRODUCTION direct push is disabled at the tenancy level by Rave Architect role-permission policy (no role carries both `dev_edit` and `prod_promote`).

### 3.3 Counterparty Integration Map

| Counterparty | Protocol | Direction | Endpoint pattern | Auth |
|---|---|---|---|---|
| Okta IdP | SAML 2.0 + SCIM 2.0 | bidirectional | `marigold.okta.com` | TLS 1.3 + mutual cert |
| Medidata Coder | vendor-internal | bidirectional | tenant-internal | tenant-bound |
| Medidata RTSM / Calyx IXRS | vendor-internal + REST | bidirectional | `rtsm.mdsol.com` | OAuth2 client-credentials |
| Central labs (LabCorp / Q² / Eurofins) | CDISC LAB / ODM-XML | inbound | SFTP + REST per-protocol | mTLS + PGP |
| Imaging core lab | DICOM + REST | inbound | per-vendor | mTLS |
| Argus 8.4 | SFTP + PGP | bidirectional | `argus-sftp.marigold-prod.local` | PGP + SSH key |
| Marinos eTMF (Veeva Vault) | REST + Vault Connect | outbound | `marinos.veevavault.com` | OAuth2 client-credentials |
| Iolanthe ePRO | CDISC ODM-XML + REST | inbound | `epro-ingest.marigold-prod.local` | mTLS |
| Watson LIMS (Thermo) | CDISC LAB / ODM-XML | inbound | SFTP | mTLS |
| Medidata Detect (RBM) | REST + CSV | outbound | `detect.mdsol.com` | OAuth2 |
| CTIS sponsor workspace | sponsor-mediated upload | outbound | EMA CTIS | sponsor user-mediated |
| Pinnacle21 (Certara) | CLI + REST | outbound | tenant | OAuth2 |
| Hydra LLM gateway | REST (egress-gated) | outbound | `hydra-vip.marigold-prod.local` | mTLS + use-case ID |
| Helios audit-event bus | Kafka | outbound | `kafka.helios.marigold-prod.local` | mTLS + SASL/SCRAM |
| LMS competence adapter | REST | outbound | `lms.marigold-prod.local` | mTLS + Entra workload-identity |

---

## 4. Configuration Specification

Each Configuration Item below is a row in the Marigold tenancy configuration baseline. Defaults are vendor-recommended values from the Medidata Rave EDC 2024 *System Administrator Guide*; Custom values carry a written justification line.

### 4.1 Tenancy Identity + SSO Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-01 | Rave Tenancy IdP Mode | `Okta SAML 2.0 + MFA (external IdP)` | Custom | Marigold mandates Okta as the single IdP per cross-system AD URS; Rave local accounts disabled. | FS-INT-SSO-01, FS-PART11-04, FS-SEC-01, FS-XSYS-AD-01 | IQ-SSO-01, OQ-AUTHN-01 |
| DS-EDC-02 | Rave Local-Account Provisioning | `Disabled (server-side enforced)` | Custom | Closes the IdP-bypass channel; all access via Okta SCIM. | FS-INT-SSO-01, FS-PART11-11 | OQ-AUTHN-02 |
| DS-EDC-03 | Okta SCIM Provisioning Endpoint | `https://marigold.mdsol.com/scim/v2/` | Default | Per Medidata Rave 2024 SCIM specification. | FS-INT-SSO-02 | IQ-SCIM-01 |
| DS-EDC-04 | SCIM Deprovisioning Latency Target | `≤ 24 hours (HR termination event → revoke)` | Custom | Marigold InfoSec policy; tighter than vendor default. | FS-INT-SSO-02, FS-SEC-01 | OQ-SCIM-02 |
| DS-EDC-05 | Okta Group Naming Convention | `marigold-rave-{role}-{study_id}` (e.g., `marigold-rave-pi-MAR-OAK-001`) | Custom | Per-study scoping enforced via group naming; required for FS-SEC-02 access reviews. | FS-INT-SSO-02, FS-SEC-02 | OQ-AUTHN-03 |
| DS-EDC-06 | Session Timeout (Idle) | `30 minutes` | Default | Vendor default; satisfies FS-SEC-01 idle-timeout requirement. | FS-SEC-01 | OQ-SESS-01 |
| DS-EDC-07 | Force-Reauth on Signature | `Enabled (`force-reauth-on-sign` session policy)` | Custom | Required by § 11.200 fresh authentication at every signature event. | FS-PART11-12, FS-SIG-01..04 | OQ-PART11-200 |
| DS-EDC-08 | MFA Method Allowlist | `Okta Verify Push, FIDO2 WebAuthn, hardware token (YubiKey)` | Custom | Phishing-resistant MFA per Marigold InfoSec; SMS disabled. | FS-PART11-04, FS-PART11-13, FS-XSYS-AD-01 | OQ-MFA-01 |
| DS-EDC-09 | Okta Conditional-Access Policy Binding | `Clinical-Sensitive Conditional Access (FIDO2 phishing-resistant MFA + sponsor-tenant isolation)` | Custom | Per cross-system AD design per FS-XSYS-AD-01. | FS-XSYS-AD-01, FS-PART11-04 | OQ-CA-01 |
| DS-EDC-10 | SIEM Forwarding | `Splunk index `gxp-authn` via syslog RFC 5424; lag ≤ 5 min` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01, FS-AUD-01 | OQ-SIEM-01 |
| DS-EDC-11 | Break-Glass Account Gating | `CyberArk PAM per QTZ-URS-PAM-* (24 h password-rotation + dual-witness check-out)` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-PAM-01 |

### 4.2 Password + Account Policy Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-12 | Okta Password Minimum Length | `14 characters` | Custom | Exceeds Rave platform default of 8; aligns with Marigold InfoSec standard + § 11.300. | FS-PART11-13 | OQ-PART11-300 |
| DS-EDC-13 | Okta Password History | `12 prior passwords retained` | Custom | Per FS-PART11-13. | FS-PART11-13 | OQ-PART11-300 |
| DS-EDC-14 | Okta Password Maximum Age | `90 days` | Custom | Per FS-PART11-13. | FS-PART11-13 | OQ-PART11-300 |
| DS-EDC-15 | Account Lockout Threshold | `5 failed authentication attempts` | Custom | Per FS-PART11-13; vendor default permissive. | FS-PART11-13 | OQ-PART11-300 |
| DS-EDC-16 | Lockout Audit Logging | `Enabled — emits Okta + Rave audit-trail entries` | Default | Required for forensic chain per § 11.10(e). | FS-PART11-13, FS-AUD-01 | OQ-AUDIT-01 |
| DS-EDC-17 | User-ID Uniqueness Policy | `Strict — deactivated user-ids never reassigned` | Custom | Per § 11.100 + FS-PART11-11. | FS-PART11-11 | OQ-PART11-100 |

### 4.3 Environment + Promotion Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-18 | DEV Environment URL | `marigold-dev.mdsol.com` | Custom | Per FS-BUILD-01 environment plan. | FS-BUILD-01 | IQ-ENV-01 |
| DS-EDC-19 | QC Environment URL | `marigold-qc.mdsol.com` | Custom | Per FS-BUILD-01. | FS-BUILD-01 | IQ-ENV-02 |
| DS-EDC-20 | UAT Environment URL | `marigold-uat.mdsol.com` | Custom | Per FS-BUILD-01. | FS-BUILD-01 | IQ-ENV-03 |
| DS-EDC-21 | PRODUCTION Environment URL | `marigold.mdsol.com` | Custom | Per FS-BUILD-01. | FS-BUILD-01 | IQ-ENV-04 |
| DS-EDC-22 | Subject Data Accept Controls | `Production only` | Custom | Per FS-BUILD-01 — DEV/QC/UAT carry synthetic only. | FS-BUILD-01 | OQ-ENV-01 |
| DS-EDC-23 | DEV → PROD Direct Promotion | `Disabled by role policy` | Custom | Per FS-BUILD-01 + FS-BUILD-02 — no role carries both `dev_edit` and `prod_promote`. | FS-BUILD-01, FS-BUILD-02 | OQ-PROMOTE-01 |
| DS-EDC-24 | Build Promotion Signature Workflow | `Two-Level (Builder + Approver; both signatures required)` | Custom | Per FS-BUILD-02 SoD policy. | FS-BUILD-02, FS-PART11-06 | OQ-PROMOTE-02 |
| DS-EDC-25 | Promotion-Signature SoD Enforcement | `Builder ≠ Approver (server-side check + Okta-group membership check)` | Custom | Two-layer enforcement; Rave role + Okta group cross-check. | FS-BUILD-02 | OQ-PROMOTE-03 |
| DS-EDC-26 | Build-Package Generation | `Auto — zip of eCRF metadata (ODM-XML) + edit-check defs + derivation logic + code lists (CT-XML) + custom-function source + SDTM mapping spec` | Default | Per FS-BUILD-06. | FS-BUILD-06 | OQ-BUILD-01 |
| DS-EDC-27 | Build-Package Fingerprint | `SHA-256 logged at promotion + archived to eTMF TMF RM artefact 04.02` | Custom | Per FS-BUILD-06 + FS-INT-ETMF-01. | FS-BUILD-06, FS-INT-ETMF-01 | OQ-BUILD-02 |
| DS-EDC-28 | Quick-Publish Whitelist | `Typo fixes; edit-check expression rewrites preserving truth-table semantics; entry-restriction tweaks; restricted folder visibility` | Custom | Per FS-BUILD-05 whitelist exactly. | FS-BUILD-05 | OQ-QUICKPUB-01 |
| DS-EDC-29 | Quick-Publish Approval Requirement | `Reviewer + Approver signatures + free-text semantic-equivalence justification` | Custom | Per FS-BUILD-05. | FS-BUILD-05 | OQ-QUICKPUB-02 |
| DS-EDC-30 | Study Architect Template Registry | `Git-versioned `template-registry` repo at `git.marigold-prod.local/cdm/template-registry`` | Custom | Per FS-BUILD-07 — templates governed under Git change control. | FS-BUILD-07 | IQ-TEMPLATE-01 |
| DS-EDC-31 | Template Binding Mode | `New studies bind to specific template version (e.g., `template@v3.2`); existing studies NOT retroactively re-bound` | Custom | Per FS-BUILD-07. | FS-BUILD-07 | OQ-TEMPLATE-01 |
| DS-EDC-32 | CtQ Register Form | `Rave custom-form `CTQ_REGISTER` (per-study)` | Custom | Per FS-BUILD-08 + FS-CRF-05. | FS-BUILD-08, FS-CRF-05 | OQ-CTQ-01 |

### 4.4 eCRF Library + CDASH Binding

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-33 | CDASH Controlled-Terminology Binding | `CDASH-IG v2.3 — Architect CT Manager` | Custom | Per FS-CRF-01. | FS-CRF-01 | OQ-CDASH-01 |
| DS-EDC-34 | CDASH Deviation Register | `Rave custom-table `cdash-deviation-log` (per-study)` | Custom | Per FS-CRF-01 — deviation captured with justification. | FS-CRF-01 | OQ-CDASH-02 |
| DS-EDC-35 | Field-Constraint Enforcement Layer | `Server-side (Required, MandatoryWithSkip, Branch, EditCheck, CodeList)` | Default | Per FS-CRF-02 — client-side enforcement convenience only. | FS-CRF-02, FS-DATA-01 | OQ-CRF-01 |
| DS-EDC-36 | Visit-Window Edit-Check Template | `Standard `VISIT_WINDOW_CHECK` (EarlyVisitDays / NominalVisitDays / LateVisitDays)` | Default | Per FS-CRF-03. | FS-CRF-03 | OQ-VISIT-01 |
| DS-EDC-37 | Casebook-Completion KPI Job | `casebook-completeness-job — daily 02:00 UTC; per subject / visit / form` | Custom | Per FS-CRF-04 — fed to RBM via FS-RBM-01. | FS-CRF-04, FS-RBM-01 | OQ-KPI-01 |
| DS-EDC-38 | CtQ-Tag Link Table | `CTQ_REGISTER ↔ eCRF Field via Architect metadata bind` | Custom | Per FS-CRF-05 + FS-SDV-01. | FS-CRF-05, FS-SDV-01 | OQ-CTQ-02 |
| DS-EDC-39 | Standard Edit-Check Library | `IMPOSSIBLE_DATE_CHECK, FUTURE_DOB_CHECK, DOSE_BEFORE_RAND_CHECK, VISIT_BEFORE_SCREEN_CHECK, LAB_ANOMALY_CHECK, RTSM_RECONCILE_CHECK` | Custom | Per FS-DATA-06 + FS-INT-LAB-03 + FS-INT-RTSM-01. | FS-DATA-06, FS-INT-LAB-03, FS-INT-RTSM-01 | OQ-EDIT-01 |
| DS-EDC-40 | Time-Zone Storage Mode | `UTC storage + `tz_original` IANA name; display per UI context` | Custom | Per FS-DATA-05 + FS-INTL-02. | FS-DATA-05, FS-INTL-02 | OQ-TZ-01 |
| DS-EDC-41 | Mobile / Offline Capture | `Rave Companion (browser PWA per-study toggle)` | Default | Per FS-DATA-07. | FS-DATA-07 | OQ-MOBILE-01 |
| DS-EDC-42 | Offline Conflict-Detection | `On reconnect, raise `OFFLINE_CONFLICT` system query` | Custom | Per FS-DATA-07. | FS-DATA-07 | OQ-MOBILE-02 |
| DS-EDC-43 | eSource Flag (`is_esource`) | `Per-form metadata bind in Architect` | Default | Per FS-ESRC-01. | FS-ESRC-01, FS-ESRC-04 | OQ-ESRC-01 |
| DS-EDC-44 | eSource Device Registry | `device-registry table per-study (device-id, serial, OS-version, browser-version)` | Custom | Per FS-ESRC-03. | FS-ESRC-03 | OQ-ESRC-02 |
| DS-EDC-45 | SDTM `--ORIG` Vocabulary | `INVESTIGATOR, eSource, eDC, ASSIGNED` per CDISC CT | Default | Per FS-ESRC-04 + FS-INT-IMG-02. | FS-ESRC-04, FS-INT-IMG-02 | OQ-SDTM-01 |

### 4.5 Derivations + Custom Functions

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-46 | Derivation Notation | `Rave post-fix derivation framework` | Default | Per FS-DATA-03. | FS-DATA-03 | OQ-DERIV-01 |
| DS-EDC-47 | Derivation Unit-Test Requirement | `Per-derivation unit tests required in UAT` | Custom | Per FS-DATA-03 — strict enforcement. | FS-DATA-03 | OQ-DERIV-02 |
| DS-EDC-48 | Custom-Function Library Location | `Signed-off function library at `git.marigold-prod.local/cdm/rave-functions`` | Custom | Per FS-DATA-04. | FS-DATA-04 | IQ-FUNC-01 |
| DS-EDC-49 | Custom-Function Production-Modification | `Blocked by Architect role policy (no role carries `prod_function_edit`)` | Custom | Per FS-DATA-04. | FS-DATA-04 | OQ-FUNC-01 |
| DS-EDC-50 | Custom-Function Code-Review Evidence | `eQMS record per release with reviewer signature` | Custom | Per FS-DATA-04. | FS-DATA-04 | OQ-FUNC-02 |

### 4.6 Query Management + Workflow Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-51 | Query Source Taxonomy Enum | `SYSTEM_EDITCHECK, MONITOR_MANUAL, DM_MANUAL, MEDICAL_MONITOR, CODER` | Custom | Per FS-QRY-01. | FS-QRY-01 | OQ-QRY-01 |
| DS-EDC-52 | Query Object Schema | `query_id, subject_id, form_id, field_path, rule_id, raised_by, raised_at, state, response, response_author, response_at, closure_author, closure_at` | Default | Per FS-QRY-02 — standard Rave Query object. | FS-QRY-02 | OQ-QRY-02 |
| DS-EDC-53 | Hard-Lock Reopen Policy | `Re-open action disabled on closed queries (Rave state-machine policy)` | Custom | Per FS-QRY-03 + FS-LOCK-01. | FS-QRY-03, FS-LOCK-01 | OQ-LOCK-01 |
| DS-EDC-54 | Query-Aging KPI Job | `query-aging-job — daily 02:30 UTC; median + p90 time-to-response + time-to-close + % overdue per site` | Custom | Per FS-QRY-04 + FS-RBM-01. | FS-QRY-04, FS-RBM-01 | OQ-KPI-02 |
| DS-EDC-55 | Bulk-Query Runner | `bulk-query-runner — writes one query event per impacted record; reviewed by Data Manager` | Default | Per FS-QRY-05. | FS-QRY-05 | OQ-QRY-03 |

### 4.7 SDV + SDR Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-56 | Default SDV Plan | `sdv-plan@critical-100 (CtQ-tagged 100% SDV; non-CtQ risk-based per per-study RBM plan)` | Custom | Per FS-SDV-01 + FS-RBM-01. | FS-SDV-01, FS-RBM-01 | OQ-SDV-01 |
| DS-EDC-57 | SDV Event API Endpoint | `POST /v1/sdv-event` (Rave-internal) | Default | Per Rave 2024 SDV-event model. | FS-SDV-01, FS-SDV-02 | OQ-SDV-02 |
| DS-EDC-58 | SDR Event Record Type | `Distinct `sdr-event` record type (NEVER routed via SDV API)` | Custom | Per FS-SDV-02 — strict separation of SDV vs SDR. | FS-SDV-02 | OQ-SDR-01 |
| DS-EDC-59 | Remote-SDV Flag Capture | `Per-visit-event flag; eligibility per per-study RBM plan` | Custom | Per FS-SDV-03. | FS-SDV-03 | OQ-SDV-03 |
| DS-EDC-60 | SDV Exception Report Job | `sdv-exception-job — runs at lock checkpoint; report attached to lock evidence` | Custom | Per FS-SDV-04 + FS-LOCK-06. | FS-SDV-04, FS-LOCK-06 | OQ-LOCK-02 |

### 4.8 RBM Feed Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-61 | RBM Feed Endpoint | `GET /v1/rbm-feed/{study_id} + nightly batch CSV to S3 bucket `marigold-rbm-prod`` | Custom | Per FS-RBM-01. | FS-RBM-01 | OQ-RBM-01 |
| DS-EDC-62 | RBM Feed Default Cadence | `Daily 03:00 UTC (per-study overridable)` | Default | Per FS-RBM-01. | FS-RBM-01 | OQ-RBM-02 |
| DS-EDC-63 | RBM Feed Schema Version | `rbm-feed@v1` | Custom | Per FS-RBM-04. | FS-RBM-04 | OQ-RBM-03 |
| DS-EDC-64 | RBM Feed Watchdog | `rbm-feed-watchdog — gap > 48 h → P1 alert + lock-block` | Custom | Per FS-RBM-03 + FS-LOCK-01. | FS-RBM-03, FS-LOCK-01 | OQ-RBM-04 |
| DS-EDC-65 | RBM Feed Payload Fields | `enrolment_rate, query_aging_p90, deviation_rate, sdv_completeness, missing_data_rate_by_ctq_field` | Custom | Per FS-RBM-01 + ICH E6(R3) § 3.10. | FS-RBM-01, FS-RBM-02 | OQ-RBM-05 |

### 4.9 Coding (Coder) Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-66 | MedDRA Version Pin Policy | `Per-study pinned at build time (default `MedDRA v27.0`); upgrade via FS-COD-04 workflow` | Custom | Per FS-COD-01. | FS-COD-01 | OQ-CODER-01 |
| DS-EDC-67 | WHODrug Version Pin Policy | `Per-study pinned at build time (default `WHODrug Global B3 Mar-2026`)` | Custom | Per FS-COD-02. | FS-COD-02 | OQ-CODER-02 |
| DS-EDC-68 | Coder Autocode Mode | `Enabled; manual-review queue surfaced in Coder UI` | Default | Per FS-COD-03. | FS-COD-03 | OQ-CODER-03 |
| DS-EDC-69 | Coder Manual-Override Audit Schema | `coder_id, dictionary_version, decision_timestamp, rationale_text` | Custom | Per FS-COD-03 + FS-COD-05. | FS-COD-03, FS-COD-05 | OQ-CODER-04 |
| DS-EDC-70 | Synonym-List Version Control | `Per-protocol additions captured with author + reviewer signatures` | Custom | Per FS-COD-06. | FS-COD-06 | OQ-CODER-05 |

### 4.10 Investigator-Signature Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-71 | Signature Scope | `Form-level + Casebook-level (per-protocol per-study)` | Custom | Per FS-SIG-01. | FS-SIG-01 | OQ-SIG-01 |
| DS-EDC-72 | Signature Meaning-String Template | `"I, as Principal Investigator, have reviewed and confirm the accuracy of these data for subject {subject_id} as of {timestamp_utc}." (localised per site language)` | Custom | Per FS-SIG-03 + FS-INTL-01. | FS-SIG-03, FS-INTL-01 | OQ-SIG-02 |
| DS-EDC-73 | Signature Payload Binding | `Bind to record-state SHA-256 hash; post-signature change writes `SIG_INVALIDATED` audit-trail entry` | Custom | Per FS-SIG-02 + FS-PART11-10. | FS-SIG-02, FS-PART11-10 | OQ-PART11-70 |
| DS-EDC-74 | Casebook PDF Generation Job | `casebook-pdf-job (on-demand) — embeds signature manifestations (printed name, date/time, meaning); digitally signed with sponsor PKI key (RSA-4096 + SHA-256)` | Custom | Per FS-SIG-04 + FS-PART11-09. | FS-SIG-04, FS-PART11-09 | OQ-SIG-03 |
| DS-EDC-75 | Sponsor PKI Key Reference | `Marigold sponsor key `marigold-sponsor-pki@v2`, stored in HashiCorp Vault `kv/marigold-pki/sponsor`` | Custom | Per FS-SIG-04 — secret-store reference. | FS-SIG-04 | IQ-PKI-01 |

### 4.11 21 CFR Part 11 — Sub-Section Configuration Map

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-76 | § 11.10(a) SOP Suite Binding | `SOP-CDM-01 System Access, SOP-CDM-02 Change Control, SOP-CDM-03 Data Entry, SOP-CDM-04 Data Review, SOP-CDM-05 Periodic Review — versioned in Vellis eDMS` | Custom | Per FS-PART11-01 + FS-PR-01. | FS-PART11-01, FS-PR-01 | OQ-PART11-10a |
| DS-EDC-77 | § 11.10(b) Reproducible-Copy Job | `casebook-pdf-job + sdtm-export-job — both produce SHA-256 manifest matching prior runs modulo data changes` | Custom | Per FS-PART11-02. | FS-PART11-02, FS-SIG-04, FS-LOCK-03 | OQ-PART11-10b |
| DS-EDC-78 | § 11.10(c) Retention Period | `25 years post-trial completion (per-study extension for paediatric / oncology / EU CTR Art. 58)` | Custom | Per FS-PART11-03 + FS-AUD-04. | FS-PART11-03, FS-AUD-04 | OQ-PART11-10c |
| DS-EDC-79 | § 11.10(d) Access Control Stack | `Okta SAML 2.0 + MFA + role-based + per-study + per-country / site scopes` | Custom | Per FS-PART11-04 + FS-SEC-01. | FS-PART11-04, FS-SEC-01 | OQ-PART11-10d |
| DS-EDC-80 | § 11.10(e) Audit-Trail Schema | `actor_id, timestamp_utc, action, entity, old_value, new_value, reason_for_change — append-only` | Custom | Per FS-PART11-05 + FS-AUD-01. | FS-PART11-05, FS-AUD-01 | OQ-PART11-10e |
| DS-EDC-81 | § 11.10(g) Authority-Check Middleware | `Server-side `authority-check` at signature, promote, lock — verifies actor role + SoD + training-current before commit` | Custom | Per FS-PART11-06. | FS-PART11-06, FS-TRN-01 | OQ-PART11-10g |
| DS-EDC-82 | § 11.10(k) Manual-Currency Gate | `LMS rule blocks user access if current-version Rave manual training not completed` | Custom | Per FS-PART11-07 + FS-TRN-01. | FS-PART11-07, FS-TRN-01 | OQ-PART11-10k |
| DS-EDC-83 | § 11.30 CTIS Gateway Hardening | `TLS 1.3 + mutual auth + checksum reconciliation` | Custom | Per FS-PART11-08 — closed-system + controlled-bridge stance. | FS-PART11-08, FS-CTIS-01 | OQ-PART11-30 |
| DS-EDC-84 | § 11.50 Signature Manifestation | `Printed name + UTC timestamp + meaning string in audit trail + casebook PDF` | Custom | Per FS-PART11-09. | FS-PART11-09, FS-SIG-04 | OQ-PART11-50 |
| DS-EDC-85 | § 11.70 Signature-Record Binding | `SHA-256 hash of record-state at signature time; post-signature delta invalidates` | Custom | Per FS-PART11-10 + FS-SIG-02. | FS-PART11-10, FS-SIG-02 | OQ-PART11-70 |
| DS-EDC-86 | § 11.100 User-ID Uniqueness Provisioning | `Okta provisioning rule: user-id reuse forbidden + deactivated never reassigned` | Custom | Per FS-PART11-11. | FS-PART11-11 | OQ-PART11-100 |
| DS-EDC-87 | § 11.200 Re-Auth at Signing | `force-reauth-on-sign Rave session policy — password + MFA at every signature event` | Custom | Per FS-PART11-12. | FS-PART11-12 | OQ-PART11-200 |
| DS-EDC-88 | § 11.300 Password Policy | `≥ 14 chars, history 12, age 90 d, MFA required, lockout 5 attempts` | Custom | Per FS-PART11-13. | FS-PART11-13 | OQ-PART11-300 |

### 4.12 Audit-Trail Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-89 | Audit-Trail Event Coverage | `data-entry, edit-check evaluation, query lifecycle, signatures, lock/unlock, configuration changes, build promotions, user provisioning, training-status changes` | Custom | Per FS-AUD-01. | FS-AUD-01 | OQ-AUDIT-01 |
| DS-EDC-90 | Audit-Trail Export Format | `CSV + PDF + ODM-XML; export bundle digitally signed by sponsor PKI key` | Default | Per FS-AUD-02. | FS-AUD-02 | OQ-AUDIT-02 |
| DS-EDC-91 | Audit-Trail Disablement Detector | `audit-trail-watchdog — heartbeat write + read every 5 min; gap > 15 min → tenant `READ_ONLY` + P1 alert` | Custom | Per FS-AUD-05. | FS-AUD-05 | OQ-AUDIT-03 |
| DS-EDC-92 | Reason-for-Change Vocabulary | `DATA_ENTRY_ERROR, NEW_INFORMATION, QUERY_RESPONSE, SYSTEM_DRIVEN, PROTOCOL_CLARIFICATION, OTHER_JUSTIFY (requires free-text)` | Custom | Per FS-AUD-06 + FS-AUD-07. | FS-AUD-06, FS-AUD-07 | OQ-AUDIT-04 |
| DS-EDC-93 | Audit-Trail Review Cadence | `Per-visit CRA review captured; central RBM dashboard ingests trends` | Custom | Per FS-AUD-03. | FS-AUD-03 | OQ-AUDIT-05 |

### 4.13 Database-Lock Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-94 | Lock-State Vocabulary | `OPEN, SOFT_LOCK, HARD_LOCK, UNLOCKED, RELOCKED` | Custom | Per FS-LOCK-01 + FS-LOCK-02. | FS-LOCK-01, FS-LOCK-02 | OQ-LOCK-03 |
| DS-EDC-95 | Hard-Lock Checklist Items | `queries closed + SDV complete + medical review complete + listings reviewed + signatures complete + coding complete + SAE reconciled (Argus) + RBM feed gap ≤ 0 h` | Custom | Per FS-LOCK-01. | FS-LOCK-01, FS-RBM-03, FS-INT-SAFETY-03 | OQ-LOCK-04 |
| DS-EDC-96 | Hard-Lock Approval Signatures | `Director CDM + VP Clinical Operations (dual)` | Custom | Per FS-LOCK-01. | FS-LOCK-01, FS-PART11-06 | OQ-LOCK-05 |
| DS-EDC-97 | Unlock Workflow Schema | `justification (free-text), scope ∈ {forms, sites, time-window}, re-lock signature on completion` | Custom | Per FS-LOCK-02. | FS-LOCK-02 | OQ-LOCK-06 |
| DS-EDC-98 | Final-Dataset Export Job | `sdtm-export-job — SDTM v2.0 / SDTM-IG v3.4 (XPT or Dataset-JSON v1.0), Define-XML v2.1, SHA-256 manifest, Pinnacle21 validation` | Custom | Per FS-LOCK-03 + FS-SDTM-02. | FS-LOCK-03, FS-SDTM-02 | OQ-LOCK-07 |
| DS-EDC-99 | ADaM Derivation Job | `adam-derive-job — per per-study ADaM spec; lineage in ADaM `--QUAL` + Define-XML analysis-variable annotations` | Default | Per FS-LOCK-04. | FS-LOCK-04 | OQ-LOCK-08 |
| DS-EDC-100 | Lock-Delta Job | `lock-delta-job — data changed since last DSMB / IDMC extract` | Custom | Per FS-LOCK-05 + FS-DSMB-03. | FS-LOCK-05, FS-DSMB-03 | OQ-LOCK-09 |
| DS-EDC-101 | Lock-Evidence Bundle Job | `lock-evidence-bundler — assembles lock-checklist signed + SDTM/Define-XML + ADaM spec + query-closure + SDV evidence + coding-finalisation + SAE reconciliation; filed in eTMF under TMF RM artefact 08.03` | Custom | Per FS-LOCK-06 + FS-INT-ETMF-01. | FS-LOCK-06, FS-INT-ETMF-01 | OQ-LOCK-10 |

### 4.14 SDTM / Define-XML / Submission Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-102 | SDTM Mapping Spec Storage | `Per-study `sdtm-mapping-spec` versioned artefact in eTMF` | Custom | Per FS-SDTM-01. | FS-SDTM-01 | OQ-SDTM-02 |
| DS-EDC-103 | SDTM-IG Target Version | `Per-protocol-specified (default v3.4)` | Custom | Per FS-SDTM-02. | FS-SDTM-02 | OQ-SDTM-03 |
| DS-EDC-104 | Pinnacle21 Validation Gate | `ERROR-class findings block submission-package generation; WARNING-class reviewed by biostatistics` | Custom | Per FS-SDTM-02. | FS-SDTM-02 | OQ-PINN-01 |
| DS-EDC-105 | Define-XML Generator Job | `define-xml-gen — v2.1 with full CT metadata + value-level + analysis-variable annotations` | Custom | Per FS-SDTM-03. | FS-SDTM-03 | OQ-DEFINE-01 |
| DS-EDC-106 | Dataset-JSON Export Toggle | `Per-study `submit_format` ∈ {XPT, DATASET_JSON}; FDA Dataset-JSON pilot studies use DATASET_JSON` | Custom | Per FS-SDTM-04. | FS-SDTM-04 | OQ-DATASETJSON-01 |
| DS-EDC-107 | SDTM Round-Trip Verifier | `sdtm-roundtrip-verifier — re-imports exported SDTM + byte-equivalence check; mismatches block lock` | Custom | Per FS-SDTM-05. | FS-SDTM-05 | OQ-SDTM-04 |

### 4.15 Vendor-Assurance Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-108 | Vendor-Quality Register | `eQMS module `vendor-quality-register` — SOC 2 Type II + ISO 27001:2022 + HIPAA + GDPR DPA + sub-processor list + customer-shared CSV summary` | Custom | Per FS-VND-01. | FS-VND-01 | IQ-VND-01 |
| DS-EDC-109 | Release-Evaluation Cadence | `≤ 14 calendar days from Medidata Trust portal publication` | Custom | Per FS-VND-02. | FS-VND-02 | OQ-VND-01 |
| DS-EDC-110 | Release-Impact Classification | `{no-impact, configuration-impact, semantics-impact, regulatory-impact}` | Custom | Per FS-VND-02. | FS-VND-02 | OQ-VND-02 |
| DS-EDC-111 | Vendor Sub-Processor Inventory | `Pulled annually from Medidata DPA Annex — DPO impact-assessment on new sub-processors per GDPR Art. 28(2)` | Custom | Per FS-VND-03. | FS-VND-03 | OQ-VND-03 |
| DS-EDC-112 | Vendor-Incident Routing | `vendor-incident-log in eQMS — confirmed-breach notifications to Marigold DPO within 24 h` | Custom | Per FS-VND-04 — GDPR Art. 33 72-h clock support. | FS-VND-04 | OQ-VND-04 |

### 4.16 GDPR + Privacy Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-113 | GDPR Art. 22 Block | `Automated individual decision-making against subject blocked at policy layer; algorithmic outputs routed via human-review queue with audit-trail entry` | Custom | Per FS-SEC-04. | FS-SEC-04 | OQ-PRIV-01 |
| DS-EDC-114 | GDPR Art. 32 Crypto Stance | `AES-256 at rest (vendor evidence); TLS 1.3 in transit; key rotation per Medidata SOC 2` | Custom | Per FS-SEC-05. | FS-SEC-05 | OQ-PRIV-02 |
| DS-EDC-115 | Per-Study DPIA Template | `Confluence template + signed PDF in eTMF — executed before FPI for special-category studies` | Custom | Per FS-SEC-06. | FS-SEC-06 | OQ-PRIV-03 |
| DS-EDC-116 | HIPAA BAA Binding | `Medidata BAA in place; PHI-flagged fields excluded from RBM feed payload` | Custom | Per FS-SEC-07. | FS-SEC-07, FS-RBM-01 | OQ-PRIV-04 |
| DS-EDC-117 | GDPR Art. 17 Erasure Triage | `Triage workflow — where EU CTR research-record-retention overrides erasure, refusal + rationale filed in eTMF; subject notified` | Custom | Per FS-SEC-08. | FS-SEC-08 | OQ-PRIV-05 |
| DS-EDC-118 | Subject-Identifier Minimisation | `Per-study eCRF design — pseudonymous subject-id; direct identifiers excluded where prohibited; GDPR Art. 9 special-category controls` | Custom | Per FS-SEC-03. | FS-SEC-03 | OQ-PRIV-06 |

### 4.17 Training + Periodic-Review Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-119 | LMS Production-Access Gate | `Role-specific + protocol-specific training currency; expiry-warning T-30 d; auto-block T+0` | Custom | Per FS-TRN-01. | FS-TRN-01 | OQ-TRN-01 |
| DS-EDC-120 | New-Version-Training Auto-Assignment | `Triggered on user-manual version advance or Quick-Publish behaviour-change` | Custom | Per FS-TRN-02. | FS-TRN-02 | OQ-TRN-02 |
| DS-EDC-121 | Annual Platform Periodic Review | `Per `SOP-CDM-05 Periodic Review` — signed by Director CDM + VP Clinical Operations` | Custom | Per FS-PR-01. | FS-PR-01 | OQ-PR-01 |
| DS-EDC-122 | Periodic-Review Scope Items | `RBM feed health + audit-trail completeness + vendor-release impact-assessment + SAE-reconciliation drift` | Custom | Per FS-PR-02. | FS-PR-02 | OQ-PR-02 |

### 4.18 Multi-Language + Time-Zone Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-123 | Supported Locales | `de-DE, de-AT, de-CH, fr-FR, en-GB, en-US, es-ES, it-IT, pl-PL, cs-CZ` | Custom | Per FS-INTL-01. | FS-INTL-01 | OQ-INTL-01 |
| DS-EDC-124 | Visit-Window TZ Calculator | `Subject's local time-zone (IANA) for window enforcement; storage UTC` | Custom | Per FS-INTL-02 + FS-DATA-05. | FS-INTL-02, FS-DATA-05 | OQ-INTL-02 |
| DS-EDC-125 | UI Locale Formatter | `Locale-specific date / number / unit display; canonical stored values unchanged` | Custom | Per FS-INTL-03. | FS-INTL-03 | OQ-INTL-03 |

### 4.19 BIMO Inspection-Readiness Configuration

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EDC-126 | BIMO Bundle Job | `bimo-bundle-job — on-demand: full audit trail + query history + signature history + eCRF state at lock + SAE reconciliation + coding decisions + protocol-deviation register` | Custom | Per FS-BIMO-01. | FS-BIMO-01 | OQ-BIMO-01 |
| DS-EDC-127 | BIMO Bundle Format | `PDF + CSV; bundle SHA-256-signed` | Custom | Per FS-BIMO-01. | FS-BIMO-01 | OQ-BIMO-02 |
| DS-EDC-128 | Inspector Okta Group | `marigold-rave-auditor-{study}` (read-only + export-only) | Custom | Per FS-BIMO-02. | FS-BIMO-02 | OQ-BIMO-03 |
| DS-EDC-129 | BIMO Bundle Performance Target | `≤ 60 min wall-clock for 500-subject Phase II reference study` | Custom | Per FS-BIMO-03. | FS-BIMO-03 | PQ-BIMO-01 |

---

## 5. Workflow + Business-Rule Design

### 5.1 eCRF Approval Workflow (Per-Study Build Promotion)

```
   ┌─────────────────────────────────────────────────────────────────────┐
   │  Per-Study Build Promotion Workflow                                 │
   │                                                                     │
   │  [DEV] Author (Builder role)                                        │
   │       │ commit                                                      │
   │       ▼                                                             │
   │  [QC]  UAT-plan-gen runs → UAT script execution captured in eQMS    │
   │       │ Builder signature                                           │
   │       ▼                                                             │
   │  [UAT] Clinical-lead + Data-manager review                          │
   │       │ Approver signature (Builder ≠ Approver)                     │
   │       │ Quick-Publish whitelist check (FS-BUILD-05)                 │
   │       ▼                                                             │
   │  [PROD] Build-package generated (ODM-XML + edit-checks +            │
   │         derivations + code lists + custom-function + SDTM map)      │
   │         SHA-256 fingerprint → eTMF TMF RM artefact 04.02            │
   └─────────────────────────────────────────────────────────────────────┘
```

| Step | Actor role | Action | Audit-trail event | Verified by |
|---|---|---|---|---|
| 1 | Builder | Edit study in Rave Architect (DEV) | `BUILD_EDIT` | OQ-BUILD-03 |
| 2 | Builder | Sign build → promote to QC | `BUILD_SIGN`, `BUILD_PROMOTE_QC` | OQ-PROMOTE-04 |
| 3 | UAT-plan-gen | Generate UAT execution plan from eCRF inventory | `UAT_PLAN_GEN` | OQ-UAT-01 |
| 4 | Builder + Data Manager | Execute UAT scripts in eQMS | `UAT_EXEC` | OQ-UAT-02 |
| 5 | Clinical Lead | Review UAT evidence | `UAT_REVIEW` | OQ-UAT-03 |
| 6 | Approver | Sign promotion to PRODUCTION (with SoD check: Builder ≠ Approver) | `BUILD_PROMOTE_PROD` | OQ-PROMOTE-05 |
| 7 | System | Generate build-package + SHA-256 + archive to eTMF | `BUILD_PACKAGE_ARCHIVE` | OQ-BUILD-04 |

### 5.2 Investigator-Signature Workflow

```
   [eCRF data entered / queries closed]
         │
         ▼
   [Re-authenticate (FS-PART11-12: password + MFA, force-reauth-on-sign)]
         │
         ▼
   [Compute SHA-256 of record-state at signature time]
         │
         ▼
   [Sign with meaning string (FS-SIG-03 template, localised)]
         │
         ▼
   [Audit-trail entry: SIG_APPLIED with payload(printed_name, ts_utc, meaning, hash)]
         │
         ▼
   [Generate / refresh casebook PDF with signature manifestation]

   If post-signature data change:
         │
         ▼
   [Audit-trail entry: SIG_INVALIDATED → UI surfaces "REQUIRES RESIGN"]
   [Original signature retained for forensic trail]
```

### 5.3 Database-Lock Workflow

| Step | Actor role | Action | Precondition checks | Verified by |
|---|---|---|---|---|
| 1 | Data Manager | Initiate SOFT_LOCK | None (advisory) | OQ-LOCK-11 |
| 2 | System | Run lock-checklist preconditions | queries closed + SDV complete + medical review + listings + signatures + coding + SAE reconciled + RBM feed current | OQ-LOCK-12 |
| 3 | Director CDM | First signature (Hard-Lock) | All preconditions passed | OQ-LOCK-13 |
| 4 | VP Clinical Operations | Second signature (Hard-Lock) | First signature present + SoD check | OQ-LOCK-14 |
| 5 | System | Execute `lock-evidence-bundler` | Hard-lock signatures recorded | OQ-LOCK-15 |
| 6 | System | Archive evidence to eTMF (TMF RM 08.03) | Bundle SHA-256 verified | OQ-LOCK-16 |

Unlock workflow (FS-LOCK-02) requires: justification text, scope (forms / sites / time-window), and a paired re-lock signature on completion. Unlock evidence is filed in eTMF under TMF RM artefact 08.03.07.

### 5.4 SAE / SUSAR Reconciliation Workflow

| Step | Source | Target | Mechanism | Cadence | FS-ID |
|---|---|---|---|---|---|
| 1 | Investigator confirmation in EDC | Argus 8.4 | SFTP + PGP file transfer | within 24 h | FS-INT-SAFETY-01 |
| 2 | Argus | EDC (read-only narrative surfaced) | vendor-internal | per-case | FS-INT-SAFETY-04 |
| 3 | EDC ↔ Argus | `sae-drift-job` | daily reconciliation | drift > 5 BD → P1 + lock-block | FS-INT-SAFETY-03 |
| 4 | EDC | Argus (sponsor-awareness ts) | metadata propagation | per-case | FS-INT-SAFETY-02 |

### 5.5 DSMB / IDMC Firewalled-Extract Workflow

```
   [DSMB Extract Request — paper / signed PDF in eTMF (FS-DSMB-04)]
         │
         ▼
   [dsmb-extract-job runs in isolated Okta-scoped tenant role]
         │
         ▼
   [Output → separate S3 bucket `marigold-dsmb-prod` with IAM policy:
        - Read denied to study-conduct roles
        - Read granted to DSMB statistician federated identity]
         │
         ▼
   [Two extract types per DSMB charter:
        - Closed (unblinded) → Okta group `dsmb-{study}-closed`
        - Open (blinded)    → Okta group `dsmb-{study}-open`]
         │
         ▼
   [Manifest generated: data_cut_date, included_subjects[], included_forms[],
    version_hash (SHA-256) → eTMF under TMF RM artefact 06.02]
```

### 5.6 RBM-Driven SDV Plan Workflow

| Trigger | Action | Verified by |
|---|---|---|
| Per-study build promotion to PROD | Bind CtQ-tagged fields to `sdv-plan@critical-100` (100% SDV) | OQ-SDV-04 |
| Per-study build promotion to PROD | Bind non-CtQ fields to risk-based plan per per-study RBM plan | OQ-SDV-05 |
| Monitor visit completion | Capture monitor signature on visit | OQ-SDV-06 |
| Lock checkpoint | Run `sdv-exception-job` → fields-not-yet-SDV'd report → lock evidence | OQ-SDV-07 |

### 5.7 CTIS Extract Submission Workflow

| Extract type | Trigger | Format | Routing | FS-ID |
|---|---|---|---|---|
| Annual Safety Report | Annual cadence | EMA CTIS Sponsor Handbook schema | Marigold Reg Affairs → CTIS sponsor workspace | FS-CTIS-01 |
| Substantial-modification data extract | Per amendment | EMA CTIS schema | Marigold Reg Affairs → CTIS | FS-CTIS-01 |
| End-of-trial summary | LPLV + database lock | EMA CTIS schema | Marigold Reg Affairs → CTIS | FS-CTIS-01 |
| SUSAR extracts | Argus-mediated | E2B(R3) | Argus → EudraVigilance (NOT via EDC) | FS-CTIS-02 |
| DE national notification | Per substantial modification | BfArM / PEI schema | per-country gateway | FS-CTIS-03 |

---

## 6. Role-Permission Matrix Design

The following role-permission matrix is enforced at the Rave tenancy level via Rave role configuration AND cross-checked at the Okta-group membership layer (FS-XSYS-AD-01). Every role row inherits the access-review cadence from FS-SEC-02 (FPI, 90-day during enrolment, LPLV).

| Role | View Data | Enter Data | Edit Data | Raise Query | Resolve Query | SDV / SDR | Sign Form | Sign Casebook | Promote Build | Approve Promotion | Lock | Unlock | Run Extract | View Inspector Bundle | DSMB Closed | DSMB Open | Vendor Release-Eval |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Investigator (PI) | ✓ | ✗ | ✗ | ✓ | ✓ | ✗ | ✓ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Sub-Investigator | ✓ | ✗ | ✗ | ✓ | ✓ | ✗ | (form only, per protocol) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Site Coordinator (Data Entry) | ✓ | ✓ | ✓ (with audit reason) | ✓ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Pharmacist | ✓ | ✓ (drug-acct forms) | ✓ | ✓ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| CRA (Monitor) | ✓ | ✗ | ✗ | ✓ | ✓ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| CRA Lead | ✓ | ✗ | ✗ | ✓ | ✓ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Data Manager | ✓ | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | initiate soft-lock | ✗ | ✓ | ✗ | ✗ | ✗ | ✗ |
| Director CDM | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | sign hard-lock (1st) | request | ✓ | ✓ | ✗ | ✗ | ✗ |
| VP Clinical Operations | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | sign hard-lock (2nd) | sign unlock | ✗ | ✓ | ✗ | ✗ | ✗ |
| Medical Monitor | ✓ | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Coder | ✓ (AE/Conmed only) | ✗ | (coding decisions only) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (coding) | ✗ | ✗ | ✗ | ✗ |
| Builder (Architect) | ✓ (DEV/QC/UAT only) | ✗ | ✓ (DEV/QC) | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ DEV→QC, QC→UAT | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Approver (Build) | ✓ (DEV/QC/UAT) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | sign UAT→PROD | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| PV Lead | ✓ (read-only narrative) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (SAE reconciliation) | ✗ | ✗ | ✗ | ✗ |
| Inspector (BIMO / EMA / DACH) | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | export-only | ✓ | ✗ | ✗ | ✗ |
| DSMB Statistician — Closed | ✓ (unblinded extract only) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (DSMB closed) | ✗ | ✓ | ✗ | ✗ |
| DSMB Statistician — Open | ✓ (blinded extract only) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (DSMB open) | ✗ | ✗ | ✓ | ✗ |
| Vendor Assurance Owner | ✓ (release-eval data) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ |
| Tenant Admin (Rave) | ✓ (config + roles) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| DPO | ✓ (privacy events) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (privacy events) | ✗ | ✗ | ✗ | ✗ |

**Role-permission design rules:**
- **SoD enforcement** — Builder role and Approver-of-Promotion role are mutually exclusive at the user level (server-side + Okta-group cross-check). Director CDM and VP Clinical Operations are mutually exclusive for the dual-signature lock workflow.
- **No role carries both `dev_edit` and `prod_promote`** — closes the DEV→PROD direct-promotion channel per DS-EDC-23.
- **Inspector role is export-only** — `marigold-rave-auditor-{study}` Okta group, no edit / no signature affordances at UI or API per FS-BIMO-02.
- **Tenant Admin cannot edit audit trail or data** — vendor-managed append-only DB per FS-AUD-02; configuration-only permissions.
- **Periodic access review** — FS-SEC-02 cadence (FPI / every 90 d during enrolment / LPLV) signed in eQMS.

---

## 7. Integration Design

### 7.1 Okta SAML + SCIM (FS-INT-SSO-01 / -02)

| Item | Value | FS-ID |
|---|---|---|
| Protocol | SAML 2.0 (auth) + SCIM 2.0 (provisioning) | FS-INT-SSO-01 |
| IdP-initiated SAML Endpoint | `https://marigold.okta.com/app/marigold-rave/saml/sso` | FS-INT-SSO-01 |
| Rave SP-Initiated Login URL | `https://marigold.mdsol.com/sso/login` | FS-INT-SSO-01 |
| SCIM Endpoint | `https://marigold.mdsol.com/scim/v2/` | FS-INT-SSO-02 |
| SAML Signature Algorithm | RSA-SHA256 | FS-INT-SSO-01 |
| MFA Methods | Okta Verify Push, FIDO2 WebAuthn, YubiKey | FS-PART11-04, FS-PART11-13 |
| Conditional-Access Policy | `Clinical-Sensitive Conditional Access` | FS-XSYS-AD-01 |
| Termination Latency Target | ≤ 24 h | FS-INT-SSO-02 |

### 7.2 Medidata Coder (FS-INT-CODER-01..03)

| Item | Value | FS-ID |
|---|---|---|
| Protocol | Vendor-internal API (tenant-bound) | FS-INT-CODER-01 |
| AE / Conmed Routing | Verbatim terms → Coder | FS-INT-CODER-01, FS-INT-CODER-02 |
| Failure Handling | `INT_CODER_FAIL` alert + queue-and-retry (exponential backoff); no fallback to local autocode | FS-INT-CODER-03 |
| Coding Incompleteness | Blocks lock | FS-INT-CODER-03, FS-LOCK-01 |
| Audit Metadata | `coder_id`, `meddra_version` or `whodrug_version`, `decision_timestamp_utc` | FS-INT-CODER-01, FS-INT-CODER-02 |

### 7.3 Medidata RTSM / Calyx IXRS (FS-INT-RTSM-01..04)

| Item | Value | FS-ID |
|---|---|---|
| Daily Reconciliation Job | `rtsm-reconcile-job` — runs 04:00 UTC | FS-INT-RTSM-01 |
| Mismatch Handling | Raise system query with `rule_id = RTSM_RECONCILE` → blocks lock until resolved | FS-INT-RTSM-01, FS-LOCK-01 |
| Duplicate-Enrolment Guard | RTSM ↔ EDC cross-validation: screening-id + hashed demographics (DOB, sex, initials hash) | FS-INT-RTSM-02 |
| Drug-Accountability Reconciliation | Daily — dispensed / returned / unused / destroyed kits | FS-INT-RTSM-03 |
| Heartbeat Cadence | 15 minutes | FS-INT-RTSM-04 |
| Heartbeat Failure Threshold | ≥ 4 successive misses → P1 `IXRS_SILENT_FAIL` alert | FS-INT-RTSM-04 |

### 7.4 Central Labs (FS-INT-LAB-01..03)

| Item | Value | FS-ID |
|---|---|---|
| Ingest Job | `lab-ingest-job` — daily 05:00 UTC; CDISC LAB / ODM-XML | FS-INT-LAB-01 |
| Local-Lab Mapping | Site-specific normal-range or central normalisation per protocol | FS-INT-LAB-02 |
| Lab-Anomaly Threshold | ± 5σ of historical site / protocol range (configurable per analyte) | FS-INT-LAB-03 |
| Anomaly Query Rule | `LAB_ANOMALY` auto-raised | FS-INT-LAB-03 |

### 7.5 Imaging Core Lab (FS-INT-IMG-01..02)

| Item | Value | FS-ID |
|---|---|---|
| Gateway | `imaging-bridge` — receives DICOM-derived clinical reads | FS-INT-IMG-01 |
| De-identification | Per de-identification rules; PHI scrubbed pre-insertion | FS-INT-IMG-01 |
| SDTM `--ORIG` Value | `ASSIGNED` for imaging-derived fields | FS-INT-IMG-02 |

### 7.6 Argus 8.4 (FS-INT-SAFETY-01..04)

| Item | Value | FS-ID |
|---|---|---|
| Transport | SFTP + PGP (sponsor-managed key) | FS-INT-SAFETY-01 |
| Endpoint | `sftp.argus.marigold-prod.local:22` | FS-INT-SAFETY-01 |
| SAE Transmission Window | ≤ 24 h from investigator confirmation | FS-INT-SAFETY-01 |
| SUSAR Clock Owner | Argus (NOT EDC) per ICH E2A | FS-INT-SAFETY-02 |
| Daily Drift Detector Job | `sae-drift-job` — drift > 5 BD → P1 + lock-block | FS-INT-SAFETY-03 |
| Narrative Read-Only Source | Argus (regulatory record-of-truth) | FS-INT-SAFETY-04 |

### 7.7 Marinos eTMF (FS-INT-ETMF-01..02)

| Item | Value | FS-ID |
|---|---|---|
| Transport | Vault Connect (cross-vault) + REST | FS-INT-ETMF-01 |
| Push Job | `etmf-push-job` — configuration baselines + build-package + lock-checklist + Define-XML + DSMB manifests + vendor-release evaluation logs | FS-INT-ETMF-01 |
| Filing Standard | DIA TMF RM v3.3.x | FS-INT-ETMF-01 |
| CTMS Cross-Link Endpoint | `GET /v1/etmf/lookup?study_id=...&site_id=...` | FS-INT-ETMF-02 |

### 7.8 Iolanthe ePRO (FS-INT-EPRO-01..03)

| Item | Value | FS-ID |
|---|---|---|
| Ingest Protocol | CDISC ODM-XML over REST | FS-INT-EPRO-01 |
| Reconciliation Key | `{subject_id, visit_id, instrument_id, completed_at_utc}` | FS-INT-EPRO-01 |
| Compliance KPI Cadence | Daily; published to RBM feed | FS-INT-EPRO-02 |
| Instrument-Version Pin | Per-study (e.g., `EORTC-QLQ-C30@v3.0`); mid-study change via FS-BUILD-04 | FS-INT-EPRO-03 |

### 7.9 Watson LIMS (FS-INT-LIMS-01..02)

| Item | Value | FS-ID |
|---|---|---|
| Ingest Protocol | CDISC LAB / ODM-XML | FS-INT-LIMS-01 |
| Reconciliation Keys | sample-id ↔ subject-id ↔ visit-id | FS-INT-LIMS-01 |
| Preliminary-Hold Mode | LIMS records flagged `PRELIMINARY` held in EDC staging until confirmation; lock blocked while preliminary records exist | FS-INT-LIMS-02 |

### 7.10 Medidata Detect / Central Monitoring (FS-RBM-01..04)

| Item | Value | FS-ID |
|---|---|---|
| Feed Protocol | REST `GET /v1/rbm-feed/{study_id}` + nightly batch CSV | FS-RBM-01 |
| Schema Version | `rbm-feed@v1` | FS-RBM-04 |
| Watchdog | `rbm-feed-watchdog` — gap > 48 h → P1 + lock-block | FS-RBM-03 |
| Breaking-Change Policy | Requires (transitive via parent URS) mid-study amendment | FS-RBM-04 |

### 7.11 CTIS Sponsor Workspace (FS-CTIS-01..03)

| Item | Value | FS-ID |
|---|---|---|
| Extract Job | `ctis-extract-job` — ASR + SM + EoT data extracts | FS-CTIS-01 |
| Routing | Marigold Reg Affairs → CTIS sponsor workspace | FS-CTIS-01 |
| SUSAR Route | Via Argus → EudraVigilance (NOT via EDC) | FS-CTIS-02 |
| DACH Carve-Out | DE → BfArM (medicinal products) + PEI (biologicals) per-country gateways | FS-CTIS-03 |

### 7.12 Pinnacle21 (FS-SDTM-02..03)

| Item | Value | FS-ID |
|---|---|---|
| Integration Protocol | CLI + REST | FS-SDTM-02 |
| Validation Trigger | Part of `sdtm-export-job` | FS-SDTM-02 |
| Error-Class Gate | ERROR-class blocks submission-package generation | FS-SDTM-02 |
| Warning-Class Handling | Reviewed by biostatistics | FS-SDTM-02 |

### 7.13 Hydra LLM Gateway + Helios Audit-Event Bus

| Item | Value | FS-ID |
|---|---|---|
| Hydra Egress ACL | Blocks vendor LLM endpoints except via gateway VIP | FS-XINT-HYD-01 |
| Hydra Adapter | `MAR-HYD-CLIENT-1.x` enforces use-case ID | FS-XINT-HYD-01 |
| Hydra Use-Case Template | `CLIN-PROTO-DRAFT-<study_id>` | FS-XINT-HYD-02 |
| Hydra Risk Class Gate | Returns 403 on missing Art. 11 pack for Annex-I-declared studies | FS-XINT-HYD-02 |
| Protocol-Section Ingestion Hook | Validates watermark + dual e-signature `(medical_monitor, biostat)` | FS-XINT-HYD-03 |
| Helios Hydra Topic | `helios.ingest.marigold.hydra.v1` (retention floor 2 y) | FS-XINT-HYD-04 |
| Helios Rave Audit Topic | `helios.ingest.marigold.rave.v1` | FS-XINT-HEL-01 |
| Helios Envelope Schema | `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}` (schema-registry-pinned) | FS-XINT-HEL-01 |
| Helios Delivery Mode | At-least-once + idempotency key `{source_system, event_id}` | FS-XINT-HEL-01 |
| Helios Back-Pressure Alert | Prometheus `helios_publish_lag_seconds` > 600 s for 5 min | FS-XINT-HEL-01 |
| Helios Reconciliation Job | Daily — parity check (Helios row count == local published count); MasterControl deviation on > 0.01% mismatch | FS-XINT-HEL-02 |

### 7.14 LMS Competence Adapter

| Item | Value | FS-ID |
|---|---|---|
| Endpoint | `GET /lms/competence/{user_id}?curriculum=...` | FS-XINT-LMS-01 |
| Auth | mTLS + Entra workload-identity | FS-XINT-LMS-01 |
| Cache TTL | 12-24 h per system | FS-XINT-LMS-01 |
| Block-on-Lapse Behaviour | Consumer blocks gated action + records `lms_lapse_user={user_id}` in consumer audit trail | FS-XINT-LMS-01 |

### 7.15 Backup Integration (FS-XSYS-BAK-01)

| Item | Value | FS-ID |
|---|---|---|
| Backup Solution | Veeam Application-Aware processing + Oracle RMAN for Rave Oracle backend | FS-XSYS-BAK-01 |
| Tier Classification | T1 | FS-XSYS-BAK-01 |
| RPO | ≤ 4 h | FS-XSYS-BAK-01, FS-BAK-01 |
| RTO | ≤ 4 BH | FS-XSYS-BAK-01 |
| Immutable Cloud Tier | S3 Object Lock Compliance mode (geo-replicated) | FS-XSYS-BAK-01 |
| Air-Gap Media | LTO-9 monthly rotation | FS-XSYS-BAK-01 |
| Restore-Test Cadence | Monthly QA-witnessed restore test per AUR-FS-BACKUP-001 | FS-XSYS-BAK-01 |
| Restore-Certificate Retention | ≥ 25 y in eQMS | FS-XSYS-BAK-01 |

---

## 8. Site-Deployed Components Design

### 8.1 Marigold Custom Job Components

The following job components are site-deployed and operate against the Rave tenancy via the configured integration endpoints. These components are governed under Marigold change control (eQMS) and follow GAMP 5 Cat 4 site-deployed-component rules.

| Component | Type | Source location | Owner team | Verified by |
|---|---|---|---|---|
| `casebook-completeness-job` | Scheduled job (daily 02:00 UTC) | `git.marigold-prod.local/cdm/casebook-completeness-job` | CDM Engineering | OQ-KPI-01 |
| `query-aging-job` | Scheduled job (daily 02:30 UTC) | `git.marigold-prod.local/cdm/query-aging-job` | CDM Engineering | OQ-KPI-02 |
| `bulk-query-runner` | On-demand runner | `git.marigold-prod.local/cdm/bulk-query-runner` | CDM Engineering | OQ-QRY-03 |
| `sdv-exception-job` | On-demand at lock checkpoint | `git.marigold-prod.local/cdm/sdv-exception-job` | CDM Engineering | OQ-LOCK-02 |
| `rbm-feed-watchdog` | Daemon (heartbeat every 5 min) | `git.marigold-prod.local/cdm/rbm-feed-watchdog` | CDM SRE | OQ-RBM-04 |
| `audit-trail-watchdog` | Daemon (heartbeat every 5 min) | `git.marigold-prod.local/cdm/audit-trail-watchdog` | CDM SRE | OQ-AUDIT-03 |
| `rtsm-reconcile-job` | Scheduled job (daily 04:00 UTC) | `git.marigold-prod.local/cdm/rtsm-reconcile-job` | CDM Engineering | OQ-RTSM-01 |
| `lab-ingest-job` | Scheduled job (daily 05:00 UTC) | `git.marigold-prod.local/cdm/lab-ingest-job` | CDM Engineering | OQ-LAB-01 |
| `sae-drift-job` | Scheduled job (daily 06:00 UTC) | `git.marigold-prod.local/cdm/sae-drift-job` | PV Engineering | OQ-SAE-01 |
| `etmf-push-job` | Event-driven | `git.marigold-prod.local/cdm/etmf-push-job` | CDM Engineering | OQ-ETMF-01 |
| `ctis-extract-job` | Manual + scheduled | `git.marigold-prod.local/regaffairs/ctis-extract-job` | Reg Affairs Engineering | OQ-CTIS-01 |
| `bimo-bundle-job` | On-demand | `git.marigold-prod.local/cdm/bimo-bundle-job` | CDM Engineering | OQ-BIMO-01 |
| `dsmb-extract-job` | Manual (DSMB charter–driven) | `git.marigold-prod.local/cdm/dsmb-extract-job` | Biostatistics Engineering | OQ-DSMB-01 |
| `casebook-pdf-job` | On-demand | `git.marigold-prod.local/cdm/casebook-pdf-job` | CDM Engineering | OQ-SIG-03 |
| `sdtm-export-job` | On-demand at lock + manual | `git.marigold-prod.local/cdm/sdtm-export-job` | CDM Engineering | OQ-LOCK-07 |
| `define-xml-gen` | On-demand at lock | `git.marigold-prod.local/cdm/define-xml-gen` | CDM Engineering | OQ-DEFINE-01 |
| `adam-derive-job` | Per per-study spec | `git.marigold-prod.local/biostat/adam-derive-job` | Biostatistics Engineering | OQ-LOCK-08 |
| `sdtm-roundtrip-verifier` | On-demand at lock | `git.marigold-prod.local/cdm/sdtm-roundtrip-verifier` | CDM Engineering | OQ-SDTM-04 |
| `lock-evidence-bundler` | On-demand at lock | `git.marigold-prod.local/cdm/lock-evidence-bundler` | CDM Engineering | OQ-LOCK-10 |
| `lock-delta-job` | On-demand | `git.marigold-prod.local/cdm/lock-delta-job` | CDM Engineering | OQ-LOCK-09 |
| `MAR-HYD-CLIENT` (Hydra adapter) | Library v1.x | `git.marigold-prod.local/cdm/mar-hyd-client` | AI Platform | OQ-HYDRA-01 |

### 8.2 Site-Deployed Component Governance Rules

- All site-deployed components are versioned in Git under `git.marigold-prod.local/cdm/` (or counterpart team space).
- Per GAMP 5 2nd-edition § 2B.4 rule 6 — embedded custom code in a Cat 4 system escalates to hybrid Cat 4 + Cat 5; each component above carries a mini-SDS sub-artefact in its Git repository (`docs/SDS.md`) that includes module decomposition, algorithm summary, data flow, secret references, and unit-test references.
- Per-component release follows the Quick-Publish + eQMS change-control workflow per FS-BUILD-05 only where the component's semantic contract is preserved; semantic-changing releases require (transitive via parent URS) (mid-study amendment) workflow.
- Unit tests live alongside source; integration tests run nightly against the QC environment.

---

## 9. References

### 9.1 US

- 21 CFR Part 11 §§ .10(a)–(k), .30, .50, .70, .100, .200, .300.
- 21 CFR Parts 50 + 56 (informed consent + IRB).
- 21 CFR Parts 312 + 314 (IND + NDA).
- FDA *Computerized Systems Used in Clinical Investigations* (May 2007).
- FDA *Electronic Source Data in Clinical Investigations* (Sep 2013).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).
- FDA *Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions* (Aug 2025).
- FDA *Use of Electronic Informed Consent — Q&A* (final).
- FDA BIMO Inspection Manual 7348.809 (updated 4 April 2025).
- HIPAA / HITECH.

### 9.2 EU

- EU CTR Regulation 536/2014 + CTIS Sponsor Handbook (current).
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EMA *Guideline on Computerised Systems and Electronic Data*.
- GDPR Reg. (EU) 2016/679 — Arts. 6, 9, 17, 22, 32, 33, 35.
- EU AI Act Reg. (EU) 2024/1689 — Arts. 9–18, 26, 43, 47–49, 50, 72, 73, 99 (Annex III high-risk obligations where studies declare AI-augmented activities under Hydra LLM gateway).

### 9.3 DACH

- BfArM (Bundesinstitut für Arzneimittel und Medizinprodukte) — DE medicinal-product national notifications.
- Paul-Ehrlich-Institut (PEI) — DE biologicals national notifications.
- Swissmedic — CH national medicines authority.
- AGES PharmMed — AT national medicines authority.

### 9.4 International

- ICH E6(R3) GCP (Step 4, adopted 6 January 2025).
- ICH E8(R1); ICH E9(R1); ICH E2A; ICH E2B(R3); ICH M11.
- ISPE GAMP 5 (2nd Edition, 2022); GAMP GPG *Computerised Systems in Regulated GCP*.
- PIC/S PI 041.
- ISO/IEC 27001:2022; ISO/IEC 27002.
- CDISC SDTM-IG v3.4 / ADaM-IG v1.3 / CDASH-IG v2.3 / ODM-XML v1.3.2 / Define-XML v2.1 / Dataset-JSON v1.0.
- DIA TMF Reference Model v3.3.x.

### 9.5 Vendor

- Medidata Solutions — *Rave EDC 2024 System Administrator Guide* (current).
- Medidata Solutions — *Rave Architect Essentials* (current).
- Medidata Solutions — *Rave EDC 2024 Validation Approach*.
- Medidata Trust portal release notes.
- Okta — *SAML 2.0 + SCIM 2.0 Integration Guide for Rave EDC*.
- Certara — *Pinnacle21 Enterprise Reference*.

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS ID | FS ID(s) | Notes |
|---|---|---|
| DS-EDC-01 | FS-INT-SSO-01 / FS-PART11-04 / FS-SEC-01 / FS-XSYS-AD-01 | Okta SAML IdP mode |
| DS-EDC-02 | FS-INT-SSO-01 / FS-PART11-11 | Local-account disablement |
| DS-EDC-03 | FS-INT-SSO-02 | SCIM endpoint |
| DS-EDC-04 | FS-INT-SSO-02 / FS-SEC-01 | SCIM deprovisioning latency |
| DS-EDC-05 | FS-INT-SSO-02 / FS-SEC-02 | Okta group naming |
| DS-EDC-06 | FS-SEC-01 | Idle session timeout |
| DS-EDC-07 | FS-PART11-12 / FS-SIG-01 | Force-reauth on sign |
| DS-EDC-08 | FS-PART11-04 / FS-PART11-13 / FS-XSYS-AD-01 | MFA method allowlist |
| DS-EDC-09 | FS-XSYS-AD-01 / FS-PART11-04 | Conditional-access binding |
| DS-EDC-10 | FS-XSYS-AD-01 / FS-AUD-01 | SIEM forwarding |
| DS-EDC-11 | FS-XSYS-AD-01 | CyberArk PAM break-glass |
| DS-EDC-12 | FS-PART11-13 | Password min length |
| DS-EDC-13 | FS-PART11-13 | Password history |
| DS-EDC-14 | FS-PART11-13 | Password max age |
| DS-EDC-15 | FS-PART11-13 | Lockout threshold |
| DS-EDC-16 | FS-PART11-13 / FS-AUD-01 | Lockout audit logging |
| DS-EDC-17 | FS-PART11-11 | User-id uniqueness |
| DS-EDC-18 | FS-BUILD-01 | DEV env URL |
| DS-EDC-19 | FS-BUILD-01 | QC env URL |
| DS-EDC-20 | FS-BUILD-01 | UAT env URL |
| DS-EDC-21 | FS-BUILD-01 | PROD env URL |
| DS-EDC-22 | FS-BUILD-01 | Subject-data accept controls |
| DS-EDC-23 | FS-BUILD-01 / FS-BUILD-02 | DEV→PROD direct disabled |
| DS-EDC-24 | FS-BUILD-02 / FS-PART11-06 | Two-level promotion signature |
| DS-EDC-25 | FS-BUILD-02 | SoD enforcement |
| DS-EDC-26 | FS-BUILD-06 | Build-package auto-gen |
| DS-EDC-27 | FS-BUILD-06 / FS-INT-ETMF-01 | Build-package SHA-256 archive |
| DS-EDC-28 | FS-BUILD-05 | Quick-Publish whitelist |
| DS-EDC-29 | FS-BUILD-05 | Quick-Publish approval |
| DS-EDC-30 | FS-BUILD-07 | Template registry Git |
| DS-EDC-31 | FS-BUILD-07 | Template binding mode |
| DS-EDC-32 | FS-BUILD-08 / FS-CRF-05 | CTQ_REGISTER form |
| DS-EDC-33 | FS-CRF-01 | CDASH binding |
| DS-EDC-34 | FS-CRF-01 | CDASH deviation register |
| DS-EDC-35 | FS-CRF-02 / FS-DATA-01 | Field-constraint server-side |
| DS-EDC-36 | FS-CRF-03 | Visit-window edit-check |
| DS-EDC-37 | FS-CRF-04 / FS-RBM-01 | Casebook-completeness KPI |
| DS-EDC-38 | FS-CRF-05 / FS-SDV-01 | CtQ-tag link |
| DS-EDC-39 | FS-DATA-06 / FS-INT-LAB-03 / FS-INT-RTSM-01 | Standard edit-check library |
| DS-EDC-40 | FS-DATA-05 / FS-INTL-02 | TZ storage |
| DS-EDC-41 | FS-DATA-07 | Mobile / offline |
| DS-EDC-42 | FS-DATA-07 | Offline conflict-detection |
| DS-EDC-43 | FS-ESRC-01 / FS-ESRC-04 | eSource flag |
| DS-EDC-44 | FS-ESRC-03 | eSource device registry |
| DS-EDC-45 | FS-ESRC-04 / FS-INT-IMG-02 | SDTM --ORIG vocab |
| DS-EDC-46 | FS-DATA-03 | Derivation notation |
| DS-EDC-47 | FS-DATA-03 | Derivation unit-test req |
| DS-EDC-48 | FS-DATA-04 | Function library location |
| DS-EDC-49 | FS-DATA-04 | Function prod-mod block |
| DS-EDC-50 | FS-DATA-04 | Function code-review evidence |
| DS-EDC-51 | FS-QRY-01 | Query source enum |
| DS-EDC-52 | FS-QRY-02 | Query object schema |
| DS-EDC-53 | FS-QRY-03 / FS-LOCK-01 | Hard-lock reopen disabled |
| DS-EDC-54 | FS-QRY-04 / FS-RBM-01 | Query-aging KPI |
| DS-EDC-55 | FS-QRY-05 | Bulk-query runner |
| DS-EDC-56 | FS-SDV-01 / FS-RBM-01 | Default SDV plan |
| DS-EDC-57 | FS-SDV-01 / FS-SDV-02 | SDV event API |
| DS-EDC-58 | FS-SDV-02 | SDR-distinct event |
| DS-EDC-59 | FS-SDV-03 | Remote-SDV flag |
| DS-EDC-60 | FS-SDV-04 / FS-LOCK-06 | SDV exception job |
| DS-EDC-61 | FS-RBM-01 | RBM feed endpoint |
| DS-EDC-62 | FS-RBM-01 | RBM cadence |
| DS-EDC-63 | FS-RBM-04 | RBM schema version |
| DS-EDC-64 | FS-RBM-03 / FS-LOCK-01 | RBM watchdog |
| DS-EDC-65 | FS-RBM-01 / FS-RBM-02 | RBM payload fields |
| DS-EDC-66 | FS-COD-01 | MedDRA pin policy |
| DS-EDC-67 | FS-COD-02 | WHODrug pin policy |
| DS-EDC-68 | FS-COD-03 | Autocode mode |
| DS-EDC-69 | FS-COD-03 / FS-COD-05 | Manual-override audit schema |
| DS-EDC-70 | FS-COD-06 | Synonym version control |
| DS-EDC-71 | FS-SIG-01 | Signature scope |
| DS-EDC-72 | FS-SIG-03 / FS-INTL-01 | Meaning-string template |
| DS-EDC-73 | FS-SIG-02 / FS-PART11-10 | Signature payload binding |
| DS-EDC-74 | FS-SIG-04 / FS-PART11-09 | Casebook PDF generation |
| DS-EDC-75 | FS-SIG-04 | Sponsor PKI key reference |
| DS-EDC-76 | FS-PART11-01 / FS-PR-01 | § 11.10(a) SOP suite |
| DS-EDC-77 | FS-PART11-02 / FS-SIG-04 / FS-LOCK-03 | § 11.10(b) reproducible copies |
| DS-EDC-78 | FS-PART11-03 / FS-AUD-04 | § 11.10(c) retention |
| DS-EDC-79 | FS-PART11-04 / FS-SEC-01 | § 11.10(d) access control |
| DS-EDC-80 | FS-PART11-05 / FS-AUD-01 | § 11.10(e) audit-trail schema |
| DS-EDC-81 | FS-PART11-06 / FS-TRN-01 | § 11.10(g) authority checks |
| DS-EDC-82 | FS-PART11-07 / FS-TRN-01 | § 11.10(k) manual currency |
| DS-EDC-83 | FS-PART11-08 / FS-CTIS-01 | § 11.30 CTIS bridge hardening |
| DS-EDC-84 | FS-PART11-09 / FS-SIG-04 | § 11.50 manifestation |
| DS-EDC-85 | FS-PART11-10 / FS-SIG-02 | § 11.70 binding |
| DS-EDC-86 | FS-PART11-11 | § 11.100 uniqueness |
| DS-EDC-87 | FS-PART11-12 | § 11.200 re-auth |
| DS-EDC-88 | FS-PART11-13 | § 11.300 password |
| DS-EDC-89 | FS-AUD-01 | Audit-trail event coverage |
| DS-EDC-90 | FS-AUD-02 | Audit-trail export format |
| DS-EDC-91 | FS-AUD-05 | Audit-trail watchdog |
| DS-EDC-92 | FS-AUD-06 / FS-AUD-07 | Reason-for-change vocab |
| DS-EDC-93 | FS-AUD-03 | Audit-trail review cadence |
| DS-EDC-94 | FS-LOCK-01 / FS-LOCK-02 | Lock-state vocab |
| DS-EDC-95 | FS-LOCK-01 / FS-RBM-03 / FS-INT-SAFETY-03 | Hard-lock checklist |
| DS-EDC-96 | FS-LOCK-01 / FS-PART11-06 | Hard-lock dual signature |
| DS-EDC-97 | FS-LOCK-02 | Unlock workflow schema |
| DS-EDC-98 | FS-LOCK-03 / FS-SDTM-02 | Final-dataset export |
| DS-EDC-99 | FS-LOCK-04 | ADaM derivation |
| DS-EDC-100 | FS-LOCK-05 / FS-DSMB-03 | Lock-delta job |
| DS-EDC-101 | FS-LOCK-06 / FS-INT-ETMF-01 | Lock-evidence bundle |
| DS-EDC-102 | FS-SDTM-01 | SDTM mapping spec |
| DS-EDC-103 | FS-SDTM-02 | SDTM-IG target |
| DS-EDC-104 | FS-SDTM-02 | Pinnacle21 gate |
| DS-EDC-105 | FS-SDTM-03 | Define-XML generator |
| DS-EDC-106 | FS-SDTM-04 | Dataset-JSON toggle |
| DS-EDC-107 | FS-SDTM-05 | SDTM round-trip verifier |
| DS-EDC-108 | FS-VND-01 | Vendor-quality register |
| DS-EDC-109 | FS-VND-02 | Release-eval cadence |
| DS-EDC-110 | FS-VND-02 | Release-impact classification |
| DS-EDC-111 | FS-VND-03 | Vendor sub-processor inventory |
| DS-EDC-112 | FS-VND-04 | Vendor-incident routing |
| DS-EDC-113 | FS-SEC-04 | GDPR Art. 22 block |
| DS-EDC-114 | FS-SEC-05 | GDPR Art. 32 crypto |
| DS-EDC-115 | FS-SEC-06 | DPIA template |
| DS-EDC-116 | FS-SEC-07 / FS-RBM-01 | HIPAA BAA + PHI-exclusion |
| DS-EDC-117 | FS-SEC-08 | GDPR Art. 17 triage |
| DS-EDC-118 | FS-SEC-03 | Subject-id minimisation |
| DS-EDC-119 | FS-TRN-01 | LMS production gate |
| DS-EDC-120 | FS-TRN-02 | New-version training |
| DS-EDC-121 | FS-PR-01 | Annual periodic review |
| DS-EDC-122 | FS-PR-02 | PR scope items |
| DS-EDC-123 | FS-INTL-01 | Supported locales |
| DS-EDC-124 | FS-INTL-02 / FS-DATA-05 | Visit-window TZ calc |
| DS-EDC-125 | FS-INTL-03 | UI locale formatter |
| DS-EDC-126 | FS-BIMO-01 | BIMO bundle job |
| DS-EDC-127 | FS-BIMO-01 | BIMO bundle format |
| DS-EDC-128 | FS-BIMO-02 | Inspector Okta group |
| DS-EDC-129 | FS-BIMO-03 | BIMO bundle perf target |
| DS-EDC-130 | FS-INT-CODER-01 / FS-INT-CODER-02 / FS-INT-CODER-03 | Coder integration design |
| DS-EDC-131 | FS-INT-RTSM-01 / FS-INT-RTSM-02 / FS-INT-RTSM-03 / FS-INT-RTSM-04 | RTSM integration design |
| DS-EDC-132 | FS-INT-LAB-01 / FS-INT-LAB-02 / FS-INT-LAB-03 | Central-lab integration design |
| DS-EDC-133 | FS-INT-IMG-01 / FS-INT-IMG-02 | Imaging integration design |
| DS-EDC-134 | FS-INT-SAFETY-01 / FS-INT-SAFETY-02 / FS-INT-SAFETY-03 / FS-INT-SAFETY-04 | Argus integration design |
| DS-EDC-135 | FS-INT-ETMF-01 / FS-INT-ETMF-02 | eTMF integration design |
| DS-EDC-136 | FS-INT-EPRO-01 / FS-INT-EPRO-02 / FS-INT-EPRO-03 | ePRO integration design |
| DS-EDC-137 | FS-INT-LIMS-01 / FS-INT-LIMS-02 | LIMS integration design |
| DS-EDC-138 | FS-AMD-01 / FS-AMD-02 / FS-AMD-03 / FS-AMD-04 | Mid-study amendment workflow |
| DS-EDC-139 | FS-CONSENT-01 / FS-CONSENT-02 / FS-CONSENT-03 / FS-CONSENT-04 | eConsent + re-consent workflow |
| DS-EDC-140 | FS-DEV-01 / FS-DEV-02 / FS-DEV-03 | Protocol-deviation tracking |
| DS-EDC-141 | FS-DSMB-01 / FS-DSMB-02 / FS-DSMB-03 / FS-DSMB-04 | DSMB firewalled-extract design |
| DS-EDC-142 | FS-CTIS-01 / FS-CTIS-02 / FS-CTIS-03 | CTIS extract design |
| DS-EDC-143 | FS-EST-01 / FS-EST-02 | Estimand-supporting eCRFs |
| DS-EDC-144 | FS-PERF-01 / FS-PERF-02 | Performance targets |
| DS-EDC-145 | FS-AV-01 | SLA tracking |
| DS-EDC-146 | FS-BAK-01 / FS-BAK-02 / FS-BAK-03 / FS-XSYS-BAK-01 | Backup tier + immutability |
| DS-EDC-147 | FS-SEC-02 | Access-review cadence |
| DS-EDC-148 | FS-XINT-HYD-01 / FS-XINT-HYD-02 / FS-XINT-HYD-03 / FS-XINT-HYD-04 | Hydra gateway design |
| DS-EDC-149 | FS-XINT-HEL-01 / FS-XINT-HEL-02 | Helios audit-event bus design |
| DS-EDC-150 | FS-XINT-LMS-01 | LMS competence adapter |
| DS-EDC-151 | FS-XSYS-AD-01 | Cross-system AD identity |

*(DS-IDs 130-151 above are integration-level / workflow-level design choices documented in §§ 5, 7, 8 and listed here for matrix completeness; the per-CI rows in § 4 (DS-EDC-01..129) carry the granular configuration-item design.)*

---

## 11. Design-Level Risk Register

The risks below originate in **design choices** made in this DS (configuration, integration, role-permission, workflow). They are inputs to the formal Risk Assessment (`MAR-RA-EDC-001`). Per-FS-ID GxP criticality (R1/R2/R3) is inherited from the parent FS and not duplicated here.

| ID | Design-level risk | Likelihood | Impact | Mitigation reference (DS) |
|---|---|---|---|---|
| DR-01 | Quick-Publish whitelist (DS-EDC-28) misclassifies a semantic-changing edit-check rewrite as semantic-equivalent | Medium | High | DS-EDC-29 (Reviewer + Approver + free-text semantic-equivalence justification); OQ-QUICKPUB-02 |
| DR-02 | RBM-driven SDV plan (DS-EDC-56) silently downgrades a CtQ field via per-study plan misconfiguration | Medium | High | DS-EDC-38 (CtQ-tag link enforced) + DS-EDC-60 (SDV exception report at lock) |
| DR-03 | Force-reauth-on-sign policy (DS-EDC-07) bypassed by cached session in a specific browser profile | Low | High | OQ-PART11-200 (regression test per signature event) |
| DR-04 | Sponsor PKI key (DS-EDC-75) rotation breaks `casebook-pdf-job` digital signature | Low | Medium | Pre-rotation test in QC env + key-rotation runbook |
| DR-05 | SCIM deprovisioning (DS-EDC-04) >24 h on an HR-termination edge case (manager-on-leave) | Medium | Medium | DS-EDC-11 (PAM break-glass closure) + monthly access review |
| DR-06 | RBM feed schema version pin (DS-EDC-63) drifts between Detect and EDC after a vendor release | Medium | Medium | DS-EDC-110 (release-impact classification) + DS-EDC-64 watchdog |
| DR-07 | Hard-lock SoD (DS-EDC-96) circumvented when Director CDM and VP Clinical Ops are the same person (small site) | Low | High | Marigold InfoSec policy — designate alternate-approver fallback path |
| DR-08 | Tenant `READ_ONLY` enforcement (DS-EDC-91) blocks legitimate emergency edit during inspection window | Low | Medium | Runbook + audit-trail watchdog gap-resolution playbook |
| DR-09 | Per-study DPIA template (DS-EDC-115) skipped on a fast-start special-category study | Medium | High | OQ-PRIV-03 + FPI gate enforced |
| DR-10 | DSMB firewalled-extract IAM policy (DS-EDC-141 / FS-DSMB-01) misconfigured grants study-conduct role read on extract bucket | Low | High | OQ-DSMB-01 + bucket-policy automated drift detector |
| DR-11 | Hydra adapter `MAR-HYD-CLIENT` (DS-EDC-148) ships a version that drops the use-case-ID enforcement | Low | High | Hydra gateway-side enforcement (FS-XINT-HYD-01); adapter-version regression test |
| DR-12 | Helios reconciliation false-positive (DS-EDC-149) generates spurious MasterControl deviation churning | Medium | Low | 0.01%-over-24h threshold (FS-XINT-HEL-02); manual review of reconciliation job output |
| DR-13 | Backup S3 Object Lock Compliance mode (DS-EDC-146) misconfigured Governance mode allows administrator deletion | Low | High | AUR-FS-BACKUP-001 verification suite + monthly QA-witnessed restore |
| DR-14 | Per-study eCRF locks subject-id pattern (DS-EDC-118) that allows back-derivation of DOB | Low | High | DPO sampled review during study-build approval |
| DR-15 | CDASH deviation register (DS-EDC-34) grows with un-justified deviations causing inspection finding | Medium | Medium | Annual periodic review (DS-EDC-121) + deviation-justification cardinality KPI |
| DR-16 | Coder MedDRA pin (DS-EDC-66) and per-study build mid-study upgrade misaligned causing dual-coding | Medium | Medium | FS-COD-04 dictionary-upgrade workflow + DS-EDC-69 audit metadata |
| DR-17 | Inspector Okta group (DS-EDC-128) overprivileged to include `view_signature_creds` due to group inheritance | Low | High | Access-review (DS-EDC-147) + role-permission OQ regression |
| DR-18 | DACH locale pack (DS-EDC-123) drift between de-DE / de-AT / de-CH on a translated signature meaning-string | Medium | Medium | DS-EDC-72 (per-site localisation) + locale-pack regression test |
| DR-19 | Custom-function library (DS-EDC-48) prod-modification block (DS-EDC-49) bypassed via Architect debug mode | Low | High | Tenant-admin role excludes debug-mode permission; OQ-FUNC-01 |
| DR-20 | Audit-trail watchdog (DS-EDC-91) heartbeat write competes with a tenant-wide migration causing false `READ_ONLY` | Low | Medium | Migration runbook explicitly pauses watchdog with documented re-enable check |
| DR-21 | Pinnacle21 ERROR/WARNING reclassification across versions changes lock-block behaviour mid-study | Low | High | DS-EDC-104 explicit gate + DS-EDC-109 release-evaluation cadence pre-empts surprise behavior |
| DR-22 | Casebook PDF (DS-EDC-74) digital signature breaks when sponsor PKI key (DS-EDC-75) rotation runbook skipped | Low | High | Pre-rotation QC environment test + key-rotation runbook integration with HashiCorp Vault audit |
| DR-23 | Investigator-signature meaning-string template (DS-EDC-72) localisation drift between de-DE / de-AT / de-CH on a translated re-sign event | Medium | Medium | Locale-pack regression test on signature event; DS-EDC-123 supported locales explicit |
| DR-24 | RBM feed PHI-exclusion rule (DS-EDC-116) misses a custom PHI-flagged field added in per-study build | Medium | High | Per-study build review checklist + DPO sampled review on PHI-flag inventory |
| DR-25 | Build-package SHA-256 fingerprint (DS-EDC-27) computed before all derived artefacts are written → archive hash mismatch on retrieval | Low | High | Build-package generation atomicity test + OQ-BUILD-02 fingerprint round-trip verification |

### 11.0 Design Trade-Off Rationales (Notable Choices)

The following design choices required explicit trade-off rationales recorded here for downstream Risk Assessment review:

- **DS-EDC-07 force-reauth-on-sign vs UX friction**: chosen for § 11.200 compliance over reduced re-auth friction; signature events are infrequent enough that the friction cost is acceptable.
- **DS-EDC-23 DEV→PROD direct push disabled by role policy** (vs allowed-with-extra-signatures): chosen because the role-policy disable closes the channel entirely rather than relying on signature discipline, which auditors prefer.
- **DS-EDC-66 + DS-EDC-67 per-study MedDRA / WHODrug version pinning** (vs tenancy-wide pin): chosen because per-study pinning allows existing studies to remain coding-stable while new studies adopt newer dictionaries; trade-off is the operational burden of per-study version tracking, mitigated by FS-COD-04 dictionary-upgrade workflow.
- **DS-EDC-95 hard-lock dual-signature** (vs single Director CDM signature): chosen because the dual signature creates audit-friendly evidence of independent approval; trade-off is potential delay when one approver is unavailable, mitigated by the alternate-approver fallback path documented under DR-07.
- **DS-EDC-148 Hydra LLM gateway egress ACL** (vs no AI gateway): chosen because EU AI Act Annex III declares clinical AI-augmented activities as high-risk; gateway enforces Art. 11 pack presence at egress; trade-off is operational cost of adapter maintenance, mitigated by versioned adapter (`MAR-HYD-CLIENT-1.x`).

### 11.0.1 Cross-Risk Mitigation Threads

Several design-level risks share a common mitigation thread that the DS surfaces as a coordinated control set rather than as independent per-row mitigations:

- **Tenancy `READ_ONLY` enforcement thread** — DS-EDC-91 (audit-trail watchdog → tenant `READ_ONLY`) interacts with DR-08 (legitimate emergency edit blocked), DR-20 (false `READ_ONLY` from migration competition), and DR-25 (build-package atomicity). The coordinated mitigation is the **migration / maintenance runbook** that pauses the watchdog with a documented re-enable check, and the **emergency-edit runbook** that captures audit-trail evidence even during the `READ_ONLY` window.
- **Force-reauth-on-sign thread** — DS-EDC-07 + DS-EDC-87 (re-auth at signature) interacts with DR-03 (cached session bypass) and DR-22 (PKI key rotation). The coordinated mitigation is the **annual signature-event regression test pack** that exercises every signing surface (form, casebook, build promotion, hard-lock, unlock, DSMB extract, CTIS extract) against rotated keys + every supported browser profile.
- **Per-study DPIA thread** — DS-EDC-115 (per-study DPIA template) interacts with DR-09 (DPIA skipped on fast-start), DR-14 (subject-id pattern), and DR-24 (PHI-exclusion). The coordinated mitigation is the **FPI gate** that requires DPIA + Privacy-Officer subject-id review + PHI-flag inventory review as a single signed pre-FPI artefact in eTMF.
- **DACH / locale thread** — DS-EDC-123 (supported locales) interacts with DS-EDC-72 (meaning-string localisation) and DR-18 + DR-23. The coordinated mitigation is the **locale-pack regression test suite** that runs at every Quick-Publish + every release-evaluation cycle.

### 11.1 Design-Risk-Register Summary by Category

| Category | Risks | Notes |
|---|---|---|
| Configuration-choice creates permission gap | DR-01, DR-02, DR-07, DR-17 | All mitigated via OQ regression + access-review cadence |
| Integration-endpoint version-drift | DR-06, DR-11, DR-12, DR-21 | Release-evaluation 14-day SLA (DS-EDC-109) + contract tests |
| Cryptographic key / signature operational risk | DR-03, DR-04, DR-13, DR-22 | Key-rotation runbooks + PKI vault audit + force-reauth |
| Storage / backup configuration | DR-13 | AUR-FS-BACKUP-001 verification + monthly QA-witnessed restore |
| Localisation / DACH-variant drift | DR-18, DR-23 | Locale-pack regression suite per release |
| Privacy / DPIA / Art. 22 | DR-09, DR-14, DR-24 | DPO sampled reviews + FPI gates |
| Auditability / READ_ONLY enforcement | DR-08, DR-20, DR-25 | Watchdog runbooks + migration-window pause protocol |

The DS Design-level Risk Register is a design-stage seed for the formal Risk Assessment (`MAR-RA-EDC-001`); it is NOT a substitute. Implementation-level risks (configuration / integration / runtime / operation) remain in the FS Implementation Risk Register.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
