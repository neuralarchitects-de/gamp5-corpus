---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "IOL2-FS-EPRO-001 v1.3 (parent FS)"
  - "IOL2-URS-EPRO-001 v1.3 (parent URS, transitive)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 Configuration Specification conventions"
  - "21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300"
  - "ICH E6(R3) GCP (Step 4, adopted 6 January 2025); ICH E8(R1); ICH E9(R1); ICH E2A; ICH E2B(R3)"
  - "EU Clinical Trials Regulation 536/2014; CTIS Sponsor Handbook"
  - "GDPR Arts. 6, 9, 22, 32, 35"
  - "FDA Patient-Reported Outcome Measures (2009); PFDD Guidance series"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026; supersedes the September 2025 guidance)"
  - "HIPAA / HITECH; ISPOR Translation Principles"
  - "Clario eCOA Platform 2025 — Configuration Reference"
  - "BfArM (DE); Paul-Ehrlich-Institut (DE); Swissmedic (CH); AGES PharmMed (AT)"
parent_fs:
  document_number: IOL2-FS-EPRO-001
  version: 1.3
  file: ../../../FS_FDS/_generated/final/Iolanthe_Clinical_ePRO_Patient_Portal_FS_v1.3.md
parent_urs:
  document_number: IOL2-URS-EPRO-001
  version: 1.3
  file: ../../../URS/_generated/final/ePRO_Patient_Portal__Iolanthe_Clinical_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## ePRO / eCOA Patient Portal — Clario eCOA Platform 2025 — Configuration Specification

**Document Number:** IOL2-DS-EPRO-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Parent FS:** IOL2-FS-EPRO-001 v1.3
**Parent URS:** IOL2-URS-EPRO-001 v1.3 *(informational; transitive via FS)*
**Site:** Iolanthe Clinical Operations GmbH, Wien, Austria *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Project Mode:** Sustaining + Configurable Change *(inherited from parent URS)*
**Regulatory Scope:** 21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300; ICH E6(R3) GCP (Step 4, adopted 6 January 2025); ICH E8(R1); ICH E9(R1); ICH E2A; ICH E2B(R3); EU CTR Reg. 536/2014 + CTIS Sponsor Handbook; FDA *Patient-Reported Outcome Measures* (2009); FDA *PFDD Guidance series*; FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance); HIPAA / HITECH; GDPR Arts. 6, 9, 22, 32, 35; ISPOR Translation Principles; ISO/IEC 27001:2022; PIC/S PI 041; BfArM (DE); Paul-Ehrlich-Institut (DE); Swissmedic (CH); AGES PharmMed (AT).

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QA Reviewer) | _____________ | _____________ | _____ |
| Reviewer (System Owner — Director, eCOA Operations) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — Sponsor Clinical Lead) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (Privacy / DPO) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Reg Affairs — CTIS) | _____________ | _____________ | _____ |
| Approver (VP Clinical Operations) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Design Control

| Field | Value |
|---|---|
| Document Number | IOL2-DS-EPRO-001 |
| Version | 1.1 |
| Effective Date *(synthetic)* | 2026-05-15 |
| Parent FS | IOL2-FS-EPRO-001 v1.3 |
| Parent URS *(informational)* | IOL2-URS-EPRO-001 v1.3 |
| Site | Iolanthe Clinical Operations GmbH, Wien, Austria *(fictional)* |
| System Class (GAMP 5, 2nd ed.) | Category 4 — Configured Product (multi-tenant SaaS) |
| Project Mode | Sustaining + Configurable Change |
| Regulatory Scope | per Title block |
| Tier | T3 (inherited from parent URS+FS pair) |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue of Configuration Specification for Clario eCOA Platform 2025 corresponding to IOL2-FS-EPRO-001 v1.3. Inherited Tier T3 from parent URS+FS pair. DS covers 106/106 FS-IDs (100% coverage). Vendor-internal Clario platform internals (Clario-managed backup primitives, Clario MDM internals, vendor-side cryptographic key rotation) are flagged as **vendor-internal — no site design surface**. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from IOL2-URS-EPRO-001 v1.3 and IOL2-FS-EPRO-001 v1.3. DS-specific additions:

| Term | Definition |
|---|---|
| eCOA | Electronic Clinical Outcomes Assessment |
| ePRO | Electronic Patient-Reported Outcome |
| PRO | Patient-Reported Outcome (questionnaire instrument) |
| BYOD | Bring Your Own Device |
| MDM | Mobile Device Management |
| TZ | Time Zone |
| DST | Daylight Saving Time |
| WCAG | Web Content Accessibility Guidelines |
| SoD | Separation of Duties |
| Marigold EDC | Iolanthe's EDC counterparty (cross-reference) |

---

## 1. Purpose

This Configuration Specification defines, at the platform-tenancy level, the configuration values, workflow designs, role-permission matrix, and integration endpoint designs that implement IOL2-FS-EPRO-001 v1.3 for the Clario eCOA Platform 2025 tenancy. It is the third document in the GAMP 5 V-model for the Iolanthe ePRO platform.

## 2. Scope

### 2.1 In Scope

- Clario eCOA Platform 2025 tenancy configuration — instrument library, linguistic-validation registry, BYOD/MDM controls, time-zone-aware schedule design, reminder ladder, AE-signal detection, diary compliance dashboard.
- Per-study configuration design (DEV → QC → UAT → PROD pattern with SoD).
- Integration design — Okta SAML 2.0 + MFA (site users); Clario patient credentials + MFA where supported; Medidata Rave EDC (Marigold) push; Marinos eTMF auto-deposit; CTIS pack export; RBM data feed.
- DACH-locale variants (de-DE, de-AT, de-CH, plus fr-CH, it-CH).
- Cross-system planes — AD identity (sponsor admin tenant + patient tenant), AUR backup tier, ePRO-to-EDC publisher.

### 2.2 Out of Scope

- Per-study instrument-version pinning (per-study DS sub-documents).
- Vendor platform internals (Clario SDLC).
- Cross-system Active Directory tenancy design (QTZ-DS-AD-001).
- Cross-system Veeam backup-infrastructure design (AUR-DS-BACKUP-001).

## 3. Architectural Overview

The Iolanthe ePRO platform is a **multi-tenant SaaS** Cat 4 system with two distinct user-facing surfaces: a **patient surface** (mobile app + web + provisioned tablet) and a **sponsor / site admin surface** (clinical monitor + site coordinator + sponsor study build). Patient authentication is per-study Clario credentials + MFA-where-supported, separated from sponsor authentication via Okta SAML 2.0 + MFA. The platform pushes data to Marigold EDC via ODM-XML, auto-deposits study build to Marinos eTMF, and emits RBM feeds per ICH E6(R3) § 3.10.

### 3.1 Platform Architectural Diagram

```
   ┌─────────────────────────────────────┐      ┌─────────────────────────────────┐
   │  Patient Tenant (Entra External ID  │      │  Sponsor Admin Tenant (Entra ID │
   │  OIDC + MFA via authenticator app   │      │  SAML 2.0 + MFA FIDO2 + device-  │
   │  or SMS fallback per IRB approval)  │      │  compliance for site monitors / │
   │                                     │      │  sponsor administrators)        │
   └────────────┬────────────────────────┘      └────────────┬────────────────────┘
                │ Conditional Access:                       │ Conditional Access:
                │ Patient-Facing Conditional Access         │ Clinical-Sensitive Conditional Access
                ▼                                            ▼
   ┌────────────────────────────────────────────────────────────────────────────┐
   │       Clario eCOA Platform 2025 (Iolanthe tenancy)                         │
   │                                                                            │
   │   ┌──────────────────────────────────────────────────────────────────┐     │
   │   │  Patient Surface (Mobile app + Web + Provisioned-tablet)          │     │
   │   │  • Diary instruments (linguistic-validated per language)          │     │
   │   │  • TZ-aware schedule (patient-local time → UTC storage)           │     │
   │   │  • Reminder Ladder (push → SMS → email → site notification)       │     │
   │   │  • Onboarding flow (WCAG 2.1 AA)                                  │     │
   │   │  • AE-signal detection (out-of-range PRO + free-text keyword)     │     │
   │   │  • Offline-mode capture + auto-sync                               │     │
   │   └──────────────────────────────────────────────────────────────────┘     │
   │                                                                            │
   │   ┌──────────────────────────────────────────────────────────────────┐     │
   │   │  Admin Surface                                                     │    │
   │   │  • Diary Compliance Dashboard (site-facing)                       │     │
   │   │  • Sponsor RBM dashboard                                          │     │
   │   │  • eCOA Library Mgmt (instrument-version + licensing)             │     │
   │   │  • Study Build (DEV → QC → UAT → PROD with SoD)                   │     │
   │   │  • Audit-trail review + Periodic Review                            │     │
   │   └──────────────────────────────────────────────────────────────────┘     │
   └─┬──────────────┬───────────────────┬───────────────────┬─────────────────┘
     │              │                   │                   │
     ▼              ▼                   ▼                   ▼
   Marigold       Marinos              CTIS                Sponsor RBM
   Rave EDC       eTMF                 sponsor             dashboard (per
   (ePRO push     (study-build         workspace           ICH E6(R3)
    via ODM-XML)  auto-deposit)        (EU CTR Art. 25)    § 3.10)
       │
       ▼
   ┌────────────────────────────────────────────────────────────────────────────┐
   │  Cross-system planes                                                       │
   │  • QTZ AD / Entra ID (patient + admin separate tenants)                    │
   │  • AUR Backup (Veeam + Oracle RMAN + MS SQL VSS + S3 Object Lock + LTO-9)  │
   └────────────────────────────────────────────────────────────────────────────┘
```

### 3.2 Counterparty Integration Map

| Counterparty | Protocol | Direction | Endpoint pattern | Auth | FS-ID |
|---|---|---|---|---|---|
| Marigold Rave EDC | REST + ODM-XML | outbound (ePRO push) | `marigold.mdsol.com/datapoints` | OAuth2 + idempotency | FS-INT-EDC-01, FS-XINT-EDC-01..03 |
| Marinos eTMF | REST | outbound (study-build deposit) | `marinos.veevavault.com/v1/etmf-deposit/` | OAuth2 | FS-INT-ETMF-01 |
| CTIS sponsor workspace | sponsor-mediated upload | outbound | EMA CTIS | sponsor user | FS-INT-CTIS-01 |
| Sponsor RBM dashboard | REST | outbound | per-sponsor | OAuth2 | FS-INT-RBM-01 |
| Entra ID (sponsor admin) | SAML 2.0 + SCIM | bidirectional | `iolanthe.azuread.local` | TLS 1.3 + mutual cert | FS-XSYS-AD-01 |
| Entra External ID (patient) | OIDC | inbound | `iolanthe-patients.azuread.local` | OIDC + MFA per IRB-approved methods | FS-XSYS-AD-01 |
| Clario MDM | vendor-internal | outbound (provisioned-tablet wipe) | per-vendor | per-Clario | FS-DEV-02 |

---

## 4. Configuration Specification

### 4.1 Tenancy + SSO + Vendor-Assurance

| CI-ID | Configuration item (Clario-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EPRO-01 | Site User IdP Mode | `Okta SAML 2.0 + MFA via Entra ID (sponsor admin tenant)` | Custom | Per FS-INT-AUTH-01 + FS-XSYS-AD-01. | FS-INT-AUTH-01, FS-XSYS-AD-01, FS-PART11-02 | OQ-AUTHN-01 |
| DS-EPRO-02 | Patient IdP Mode | `Entra External ID OIDC + MFA where supported (authenticator app or SMS fallback per IRB approval)` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01, FS-INT-AUTH-01 | OQ-AUTHN-02 |
| DS-EPRO-03 | Patient Tenant Conditional-Access Policy | `Patient-Facing Conditional Access (MFA via authenticator app or SMS fallback per IRB approval)` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-CA-01 |
| DS-EPRO-04 | Admin Tenant Conditional-Access Policy | `Clinical-Sensitive Conditional Access (FIDO2 + device-compliance)` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-CA-02 |
| DS-EPRO-05 | SIEM Forwarding | `Splunk gxp-authn syslog RFC 5424; lag ≤ 5 min` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-SIEM-01 |
| DS-EPRO-06 | Break-Glass PAM | `CyberArk PAM — 24 h rotation + dual-witness` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-PAM-01 |
| DS-EPRO-07 | Service-Account Auth | `mTLS only` | Custom | Per FS-PART11-02. | FS-PART11-02 | OQ-SA-01 |
| DS-EPRO-08 | Force-Reauth at Sign | `Enabled (max-age 5 min OAuth2 token)` | Custom | Per FS-PART11-07. | FS-PART11-07 | OQ-PART11-200 |
| DS-EPRO-09 | Account Lockout — Site Users | `5 failures / 15 minutes` | Custom | Per FS-PART11-08 + FS-SEC-02. | FS-PART11-08, FS-SEC-02 | OQ-LOCK-01 |
| DS-EPRO-10 | Account Lockout — Patients | `5 failures / 15 minutes` | Custom | Per FS-SEC-02. | FS-SEC-02 | OQ-LOCK-02 |
| DS-EPRO-11 | Vendor-Assurance Dossier | `SOC 2 Type II + ISO 27001 + HIPAA evidence; annual re-qualification` | Custom | Per FS-VND-01. | FS-VND-01 | IQ-VND-01 |
| DS-EPRO-12 | Vendor Release-Notes Workflow | `Automated alert; site change-control gate; 14-day SLA` | Custom | Per FS-VND-02 + FS-VND-07. | FS-VND-02, FS-VND-07 | OQ-VND-01 |
| DS-EPRO-13 | Sub-Processor Review | `Quarterly per DPA Annex II; new sub-processors → DPIA delta-review` | Custom | Per FS-VND-03. | FS-VND-03 | OQ-VND-02 |
| DS-EPRO-14 | Cross-Border Flow Assessment | `New flows assessed against existing SCC routes; new SCC where needed` | Custom | Per FS-VND-04. | FS-VND-04 | OQ-VND-03 |
| DS-EPRO-15 | SLA-Report Review | `Quarterly; breaches → vendor-assurance dossier + eQMS deviation` | Custom | Per FS-VND-05. | FS-VND-05 | OQ-VND-04 |
| DS-EPRO-16 | Annual SDLC-Evidence Review | `/vendor-assurance/clario/` | Custom | Per FS-VND-06. | FS-VND-06 | OQ-VND-05 |

### 4.2 Study Build + Configuration Management

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EPRO-17 | Study-Build Lifecycle | `DEV → QC → UAT → PRODUCTION; SoD-enforced (Author ≠ Approver)` | Custom | Per FS-CFG-01 + FS-CCM-01. | FS-CFG-01, FS-CCM-01 | OQ-BUILD-01 |
| DS-EPRO-18 | CTIS-Compatible Study-Build Pack | `Exporter per EU CTR Art. 25 (XML schema)` | Custom | Per FS-CFG-02. | FS-CFG-02 | OQ-CTIS-01 |
| DS-EPRO-19 | Configuration Export Endpoint | `GET /config/export?study_id=...` version-stamped JSON | Custom | Per FS-CFG-03. | FS-CFG-03 | OQ-CFG-01 |
| DS-EPRO-20 | Configuration Baselines | `Versioned + exportable; baseline-diff drift detection` | Custom | Per FS-CCM-02. | FS-CCM-02 | OQ-CCM-01 |
| DS-EPRO-21 | Emergency-Change Review | `Post-implementation review ≤ 5 BD` | Custom | Per FS-CCM-03. | FS-CCM-03 | OQ-CCM-02 |

### 4.3 Linguistic Validation + DACH Variants

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EPRO-22 | Linguistic-Validation Registry Schema | `Per language per instrument-version (ISPOR + FDA-compliant)` | Custom | Per FS-LING-01. | FS-LING-01 | OQ-LING-01 |
| DS-EPRO-23 | Out-of-Validation Block | `API returns 422 when patient attempts unvalidated language` | Custom | Per FS-LING-02. | FS-LING-02 | OQ-LING-02 |
| DS-EPRO-24 | DACH Language Variants | `de-DE, de-AT, de-CH, plus fr-CH, it-CH (distinct entries)` | Custom | Per FS-LING-03. | FS-LING-03 | OQ-LING-03 |
| DS-EPRO-25 | Instrument-Version-Change Watcher | `Invalidates dependent translations; re-validation flow triggered` | Custom | Per FS-LING-04. | FS-LING-04 | OQ-LING-04 |

### 4.4 Patient Entry Schema + Time-Zone Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EPRO-26 | Patient Entry Schema | `patient_id (pseudonymised), instrument_id, instrument_version, NTP-synced timestamp_iso8601, entry_payload, language_locale` | Custom | Per FS-PAT-01. | FS-PAT-01 | OQ-ENTRY-01 |
| DS-EPRO-27 | Time-Window Enforcement | `Configurable per instrument (e.g., 06:00-22:00 patient-local-time); out-of-window flagged` | Custom | Per FS-PAT-02. | FS-PAT-02 | OQ-WINDOW-01 |
| DS-EPRO-28 | Adherence Dashboard | `Patient-level + study-level metrics; data feed to RBM` | Custom | Per FS-PAT-03. | FS-PAT-03 | OQ-ADH-01 |
| DS-EPRO-29 | Missed-Entry Alert Ladder | `Push → SMS → site-notification at configurable thresholds` | Custom | Per FS-PAT-04. | FS-PAT-04 | OQ-ALERT-01 |
| DS-EPRO-30 | NTP Sync Verification | `Device clock-drift > 5 min flags entry; server-side timestamp authoritative` | Custom | Per FS-PAT-05. | FS-PAT-05 | OQ-NTP-01 |
| DS-EPRO-31 | TZ Storage Model | `patient-local time displayed; UTC stored + TZ + offset metadata` | Custom | Per FS-TZ-01 + FS-DI-04. | FS-TZ-01 | OQ-TZ-01 |
| DS-EPRO-32 | DST-Transition Handling | `Entry-validity windows respect DST per patient TZ` | Custom | Per FS-TZ-02. | FS-TZ-02 | OQ-TZ-02 |
| DS-EPRO-33 | Patient-TZ-Change Detection | `"time-zone-change" reason-flag on affected entries; reconcilable` | Custom | Per FS-TZ-03. | FS-TZ-03 | OQ-TZ-03 |
| DS-EPRO-34 | Site-Coordinator TZ Display | `Multi-site study view shows patient-local time; no silent mismatch` | Custom | Per FS-TZ-04. | FS-TZ-04 | OQ-TZ-04 |

### 4.5 BYOD + Provisioned-Tablet Device Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EPRO-35 | BYOD Device Registration | `device-id + OS + app-version; jailbreak / root detection blocks` | Custom | Per FS-DEV-01. | FS-DEV-01 | OQ-DEV-01 |
| DS-EPRO-36 | Provisioned-Tablet MDM | `Clario MDM service; remote-wipe API < 15 min from loss-report` | Custom | Per FS-DEV-02. | FS-DEV-02 | OQ-DEV-02 |
| DS-EPRO-37 | OS Version Support | `iOS / Android current + n-1 major versions; older blocked` | Custom | Per FS-DEV-03. | FS-DEV-03 | OQ-DEV-03 |
| DS-EPRO-38 | Per-Study BYOD vs Provisioned | `Configuration field with documented rationale` | Custom | Per FS-DEV-04. | FS-DEV-04 | OQ-DEV-04 |

### 4.6 Audit Trail + Part 11 + ALCOA+ Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EPRO-39 | Audit-Trail Schema | `Entries + edits + signatures + config changes + translation approvals; append-only DB` | Custom | Per FS-AUD-01. | FS-AUD-01, FS-PART11-03 | OQ-AUDIT-01 |
| DS-EPRO-40 | Tenant-Admin Audit Permission | `Cannot UPDATE / DELETE audit records` | Custom | Per FS-AUD-02. | FS-AUD-02 | OQ-AUDIT-02 |
| DS-EPRO-41 | Audit-Trail Review Cadence | `Per-study-build review by site QA + quarterly periodic review` | Custom | Per FS-AUD-03. | FS-AUD-03 | OQ-AUDIT-03 |
| DS-EPRO-42 | Audit-Trail Retention | `≥ 25 y per ICH E6(R3) + EU CTR` | Custom | Per FS-AUD-04. | FS-AUD-04 | OQ-AUDIT-04 |
| DS-EPRO-43 | RBM Pattern Surfacing | `Audit-trail review surfaces patterns per ICH E6(R3) § 3.10` | Custom | Per FS-AUD-05. | FS-AUD-05 | OQ-AUDIT-05 |
| DS-EPRO-44 | § 11.10(a) Procedural Controls | `/sop/` reviewed annually` | Custom | Per FS-PART11-01. | FS-PART11-01 | OQ-PART11-10a |
| DS-EPRO-45 | § 11.10(d) Access Control | `Okta SAML 2.0 + MFA for site users; service accounts via mTLS only` | Custom | Per FS-PART11-02. | FS-PART11-02 | OQ-PART11-10d |
| DS-EPRO-46 | § 11.10(e) Audit Trail | `Per DS-EPRO-39` | Custom | Per FS-PART11-03. | FS-PART11-03 | OQ-PART11-10e |
| DS-EPRO-47 | § 11.50 Manifestation | `Printed name + date/time + meaning string (DB schema-enforced)` | Custom | Per FS-PART11-04. | FS-PART11-04 | OQ-PART11-50 |
| DS-EPRO-48 | § 11.70 Binding | `HMAC-SHA256 over record-hash + signer-id + timestamp` | Custom | Per FS-PART11-05. | FS-PART11-05 | OQ-PART11-70 |
| DS-EPRO-49 | § 11.100 Unique Signature | `Okta-DB uniqueness constraint; no reuse / reassignment` | Custom | Per FS-PART11-06. | FS-PART11-06 | OQ-PART11-100 |
| DS-EPRO-50 | § 11.200 Re-Auth | `Fresh OAuth2 token max-age 5 min; cached creds rejected` | Custom | Per FS-PART11-07. | FS-PART11-07 | OQ-PART11-200 |
| DS-EPRO-51 | § 11.300 Credential Policy | `MFA mandatory + lockout 5/15min + complexity per site standard` | Custom | Per FS-PART11-08. | FS-PART11-08 | OQ-PART11-300 |
| DS-EPRO-52 | ALCOA+ Attributable | `actor_id not-null DB constraint at audit-write` | Custom | Per FS-DI-01. | FS-DI-01 | OQ-DI-01 |
| DS-EPRO-53 | ALCOA+ Legible | `PDF/A-3 + JSON/XML exports; OQ-verified` | Custom | Per FS-DI-02. | FS-DI-02 | OQ-DI-02 |
| DS-EPRO-54 | ALCOA+ Contemporaneous | `Server-side NTP-synced timestamps; retroactive flagged with delay reason` | Custom | Per FS-DI-03. | FS-DI-03 | OQ-DI-03 |
| DS-EPRO-55 | ALCOA+ Original | `Raw inputs in immutable storage; derivatives reference but don't overwrite` | Custom | Per FS-DI-04. | FS-DI-04 | OQ-DI-04 |
| DS-EPRO-56 | ALCOA+ Accurate | `Deterministic calculations; floating-point reproducibility OQ-verified` | Custom | Per FS-DI-05. | FS-DI-05 | OQ-DI-05 |
| DS-EPRO-57 | ALCOA+ Retrievability | `≤ 1 BD routine; metadata completeness validated` | Custom | Per FS-DI-06. | FS-DI-06 | OQ-DI-06 |

### 4.7 Privacy + Security Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EPRO-58 | GDPR Art. 9 Pseudonymisation | `PHI minimisation + pseudonymisation; AES-256 at rest + TLS 1.3 in transit; re-id only via EDC behind additional controls` | Custom | Per FS-PRV-01. | FS-PRV-01 | OQ-PRIV-01 |
| DS-EPRO-59 | DPIA URN Field | `Per study; verified at study-build approval; mandatory before patient enrolment` | Custom | Per FS-PRV-02. | FS-PRV-02 | OQ-PRIV-02 |
| DS-EPRO-60 | GDPR Art. 22 Block | `Automated decisions affecting participant blocked; only adherence-monitoring permitted` | Custom | Per FS-PRV-03. | FS-PRV-03 | OQ-PRIV-03 |
| DS-EPRO-61 | Cross-Border Transfer Route | `Documented per study; SCCs enforced via vendor DPA for non-adequacy jurisdictions` | Custom | Per FS-PRV-04. | FS-PRV-04 | OQ-PRIV-04 |
| DS-EPRO-62 | Pseudonymisation Boundary | `Enforced at ePRO platform boundary; re-id only in EDC (Marigold) behind separate access controls` | Custom | Per FS-BYOPID-01. | FS-BYOPID-01 | OQ-PRIV-05 |
| DS-EPRO-63 | Subject-ID Format Validation | `Sponsor-defined per study; validation rule rejects identifiable patterns (DOB, MRN)` | Custom | Per FS-BYOPID-02. | FS-BYOPID-02 | OQ-PRIV-06 |
| DS-EPRO-64 | Subject-ID Privacy Review | `Per-study sampled review by Privacy Officer during study-build approval` | Custom | Per FS-BYOPID-03. | FS-BYOPID-03 | OQ-PRIV-07 |
| DS-EPRO-65 | TLS / AES Stance | `TLS 1.3 in transit + AES-256 at rest; vendor evidence on file` | Custom | Per FS-SEC-01. | FS-SEC-01 | OQ-SEC-01 |
| DS-EPRO-66 | Patient Credential Isolation | `Per-study isolated; account-lockout 5 failures / 15 min` | Custom | Per FS-SEC-02. | FS-SEC-02 | OQ-SEC-02 |
| DS-EPRO-67 | Annual Vendor Cert Review | `SOC 2 Type II + ISO 27001 evidence; gaps to change control` | Custom | Per FS-SEC-03. | FS-SEC-03 | OQ-SEC-03 |
| DS-EPRO-68 | Annual Pen-Test | `Patient-facing endpoints; H/C findings remediated within 30 d` | Custom | Per FS-SEC-04. | FS-SEC-04 | OQ-SEC-04 |
| DS-EPRO-69 | PII Minimisation in UI | `Field-level controls in site-user UI; OQ-verified` | Custom | Per FS-SEC-05. | FS-SEC-05 | OQ-SEC-05 |

### 4.8 Diary Compliance Dashboard + Reminder Ladder

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EPRO-70 | Site-Facing Diary Compliance Dashboard | `Patient adherence over rolling 7 / 14-day + study-to-date windows` | Custom | Per FS-DCD-01. | FS-DCD-01 | OQ-DCD-01 |
| DS-EPRO-71 | Sponsor RBM Dashboard | `Site / study / cohort drill-down to patient-level` | Custom | Per FS-DCD-02. | FS-DCD-02 | OQ-DCD-02 |
| DS-EPRO-72 | Adherence Outlier Alert Engine | `Configurable thresholds; role-targeted escalation` | Custom | Per FS-DCD-03. | FS-DCD-03 | OQ-DCD-03 |
| DS-EPRO-73 | Compliance Trend Reports | `Time-of-day, day-of-week, protocol-deviation rate per ICH E6(R3) § 3.10` | Custom | Per FS-DCD-04. | FS-DCD-04 | OQ-DCD-04 |
| DS-EPRO-74 | Site-Coordinator Daily Worklist | `Auto-prioritised by overdue + outlier patients` | Custom | Per FS-DCD-05. | FS-DCD-05 | OQ-DCD-05 |
| DS-EPRO-75 | Reminder Ladder Stages | `Push → SMS → email → site-notification → site outreach; configurable per instrument` | Custom | Per FS-RLR-01. | FS-RLR-01 | OQ-RLR-01 |
| DS-EPRO-76 | Patient Quiet-Hours Window | `22:00-07:00 patient-local-time default; TZ-aware per patient profile` | Custom | Per FS-RLR-02. | FS-RLR-02 | OQ-RLR-02 |
| DS-EPRO-77 | Drop-Off Recovery Threshold | `Configurable consecutive misses (default 3); site outreach script` | Custom | Per FS-RLR-03. | FS-RLR-03 | OQ-RLR-03 |
| DS-EPRO-78 | Patient-Fatigue Heuristic Engine | `Entry-latency + dwell-time signals flag retention-risk patients` | Custom | Per FS-RLR-04. | FS-RLR-04 | OQ-RLR-04 |

### 4.9 Onboarding Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EPRO-79 | Onboarding Flow | `Identity verification + device pairing + study-credential issuance + consent re-confirmation` | Custom | Per FS-ONB-01. | FS-ONB-01 | OQ-ONB-01 |
| DS-EPRO-80 | Onboarding Completion Event | `Timestamp + verifier + method; entry-into-study gated on completion` | Custom | Per FS-ONB-02. | FS-ONB-02 | OQ-ONB-02 |
| DS-EPRO-81 | Onboarding Tutorial | `Available per supported language; completion tracked` | Custom | Per FS-ONB-03. | FS-ONB-03 | OQ-ONB-03 |
| DS-EPRO-82 | WCAG Compliance Level | `WCAG 2.1 AA` | Custom | Per FS-ONB-04. | FS-ONB-04 | OQ-A11Y-01 |

### 4.10 AE-Signal Detection Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EPRO-83 | AE-Signal Detection Engine | `Out-of-range PRO score + free-text symptom keyword; workflow notification to site investigator` | Custom | Per FS-AE-01. | FS-AE-01 | OQ-AE-01 |
| DS-EPRO-84 | AE Push to Marigold EDC | `Idempotent on AE-id; reconciliation log` | Custom | Per FS-AE-02. | FS-AE-02 | OQ-AE-02 |
| DS-EPRO-85 | SAE-Trigger Surface | `Immediate site dashboard red-flag indicator; investigator follow-up audit-trailed` | Custom | Per FS-AE-03. | FS-AE-03 | OQ-AE-03 |
| DS-EPRO-86 | AE Wording Preservation | `Patient-reported wording preserved; site interpretation as separate field` | Custom | Per FS-AE-04. | FS-AE-04 | OQ-AE-04 |
| DS-EPRO-87 | AE Event Timestamp | `NTP-synced server-side; patient-claimed onset captured separately per ICH E2A` | Custom | Per FS-AE-05. | FS-AE-05 | OQ-AE-05 |
| DS-EPRO-88 | AE → PV Cross-Link | `Audit cross-link to Sirius Argus PV for PV review` | Custom | Per FS-AE-06. | FS-AE-06 | OQ-AE-06 |

### 4.11 eCOA Library + Instrument-Version Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EPRO-89 | eCOA Library Schema | `instrument-type + author + version + licensing + validated languages` | Custom | Per FS-LIB-01. | FS-LIB-01 | OQ-LIB-01 |
| DS-EPRO-90 | Instrument-Version Lifecycle | `Only licensed + linguistically-validated version assignable` | Custom | Per FS-LIB-02. | FS-LIB-02 | OQ-LIB-02 |
| DS-EPRO-91 | Licensing-Evidence Check | `Per study at build; missing licence blocks build` | Custom | Per FS-LIB-03. | FS-LIB-03 | OQ-LIB-03 |
| DS-EPRO-92 | Scoring-Rule Engine | `Deterministic; scoring-rule change triggers re-validation of all dependent studies` | Custom | Per FS-LIB-04. | FS-LIB-04 | OQ-LIB-04 |
| DS-EPRO-93 | Custom-Instrument Workflow | `Sponsor + IRB/IEC approval + linguistic-validation evidence required` | Custom | Per FS-LIB-05. | FS-LIB-05 | OQ-LIB-05 |

### 4.12 Recruitment + Retention + Withdrawal Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EPRO-94 | Recruitment Funnel Metrics | `invitations / interested / consented / onboarded / retained per site + study` | Custom | Per FS-RR-01. | FS-RR-01 | OQ-RR-01 |
| DS-EPRO-95 | Retention Metrics | `Drop-off rate + survival curve per study + site` | Custom | Per FS-RR-02. | FS-RR-02 | OQ-RR-02 |
| DS-EPRO-96 | Patient-Feedback Survey | `Deployable separately from PRO instruments` | Custom | Per FS-RR-03. | FS-RR-03 | OQ-RR-03 |
| DS-EPRO-97 | Compensation Tracking Module | `Audit-trailed; outside patient-data scope` | Custom | Per FS-RR-04. | FS-RR-04 | OQ-RR-04 |
| DS-EPRO-98 | Recruitment-Channel Attribution | `Per consented patient where applicable` | Custom | Per FS-RR-05. | FS-RR-05 | OQ-RR-05 |
| DS-EPRO-99 | Patient Withdrawal Reason | `Per IRB/IEC-approved categories where voluntarily provided` | Custom | Per FS-RR-06. | FS-RR-06 | OQ-RR-06 |

### 4.13 Integration Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EPRO-100 | EDC Push Endpoint | `POST marigold.mdsol.com/datapoints` ODM-XML | Custom | Per FS-INT-EDC-01 + FS-XINT-EDC-01. | FS-INT-EDC-01, FS-XINT-EDC-01 | OQ-EDC-01 |
| DS-EPRO-101 | EDC Idempotency-Key | `{study_id, subject_id, visit_id, instrument_id, item_id, completion_ts}`; back-off 1s → 1024s; DLQ `iolanthe.edc.dlq` | Custom | Per FS-XINT-EDC-01. | FS-XINT-EDC-01 | OQ-EDC-02 |
| DS-EPRO-102 | EDC Reconciliation Job | `Daily — compares ePRO published hash vs EDC stored hash; mismatch raises Rave query + Iolanthe deviation` | Custom | Per FS-XINT-EDC-02. | FS-XINT-EDC-02 | OQ-EDC-03 |
| DS-EPRO-103 | Instrument-Version Guard | `Rejects datapoint publish when active ePRO instrument_version ≠ Rave-registered instrument_version` | Custom | Per FS-XINT-EDC-03. | FS-XINT-EDC-03 | OQ-EDC-04 |
| DS-EPRO-104 | eTMF Auto-Deposit | `Study-build documentation auto-deposited to Marinos eTMF on approval` | Custom | Per FS-INT-ETMF-01. | FS-INT-ETMF-01 | OQ-ETMF-01 |
| DS-EPRO-105 | CTIS Pack Export | `Per EU CTR Art. 25 (XML); validated against CTIS schema in CI` | Custom | Per FS-INT-CTIS-01. | FS-INT-CTIS-01 | OQ-CTIS-01 |
| DS-EPRO-106 | RBM Data-Feed Endpoint | `Adherence + completion + time-of-day patterns per ICH E6(R3) § 3.10` | Custom | Per FS-INT-RBM-01. | FS-INT-RBM-01 | OQ-RBM-01 |
| DS-EPRO-107 | Backup Integration | `Veeam + Oracle RMAN (ePRO Oracle backend) + MS SQL VSS (admin metadata) + S3 Object Lock + LTO-9` | Custom | Per FS-XSYS-BAK-01 + FS-BAK-01..03. | FS-XSYS-BAK-01, FS-BAK-01 | OQ-BAK-01 |

### 4.14 Performance + Availability + Offline-Mode Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EPRO-108 | P95 Instrument-Open Target | `≤ 3 s` | Custom | Per FS-PERF-01. | FS-PERF-01 | PQ-PERF-01 |
| DS-EPRO-109 | Concurrent Patient Sessions | `≥ 10,000 sustained` | Custom | Per FS-PERF-02. | FS-PERF-02 | PQ-PERF-02 |
| DS-EPRO-110 | Clario SLA | `≥ 99.5% normal; ≥ 99.9% sponsor-critical visit windows` | Custom | Per FS-AV-01. | FS-AV-01 | OQ-AV-01 |
| DS-EPRO-111 | Offline-Mode Capture | `Auto-sync on network restore with conflict-resolution log` | Custom | Per FS-AV-02. | FS-AV-02 | OQ-AV-02 |

### 4.15 Training + Periodic Review Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-EPRO-112 | LMS Training Gate | `Role-specific training; ICH E6(R3) GCP mandatory for Site Investigators + Coordinators + Sponsor Monitors` | Custom | Per FS-TRN-01. | FS-TRN-01 | OQ-TRN-01 |
| DS-EPRO-113 | Annual Refresher | `EPRO-2026-ANNUAL — ICH E6(R3) + GDPR + HIPAA + RBM updates` | Custom | Per FS-TRN-02. | FS-TRN-02 | OQ-TRN-02 |
| DS-EPRO-114 | Annual Periodic Review | `Signed by Director eCOA Operations + Privacy Officer + VP QA + VP Clinical Operations` | Custom | Per FS-PR-01. | FS-PR-01 | OQ-PR-01 |

---

## 5. Workflow + Business-Rule Design

### 5.1 Patient Diary Capture Workflow

```
   [Patient logs in via Entra External ID OIDC + MFA (DS-EPRO-02)]
         │
         ▼ Conditional Access verified (DS-EPRO-03)
   [Instrument list shown (per linguistic-validation registry, DS-EPRO-22)]
         │
         ▼
   [Patient completes diary in patient-local TZ (DS-EPRO-31)]
         │
         ▼ NTP-sync check — clock-drift > 5 min flags entry (DS-EPRO-30)
   [Server-side timestamp authoritative + UTC stored with TZ metadata]
         │
         ▼ Time-window check (DS-EPRO-27) — flag if out-of-window
   [Entry saved with audit-trail entry (FS-AUD-01)]
         │
         ▼ AE-signal detection engine (DS-EPRO-83)
   ┌──────────────────────────────────────────────────────────┐
   │  If out-of-range PRO score OR free-text keyword match:    │
   │     → Site investigator workflow notification (DS-EPRO-83)│
   │     → If SAE-trigger: red-flag indicator on dashboard     │
   │       (DS-EPRO-85)                                        │
   │     → AE push to Marigold EDC (idempotent on AE-id,       │
   │       DS-EPRO-84)                                         │
   │     → Cross-link to Sirius Argus PV (DS-EPRO-88)          │
   └──────────────────────────────────────────────────────────┘
         │
         ▼ ePRO-to-EDC publisher (DS-EPRO-100)
   [POST marigold.mdsol.com/datapoints (ODM-XML); idempotency key
    {study_id, subject_id, visit_id, instrument_id, item_id, completion_ts}]
         │
         ▼ Instrument-version guard (DS-EPRO-103) — rejects if mismatch
   [Daily reconciliation (DS-EPRO-102) → Rave query on hash mismatch]
```

### 5.2 Reminder Ladder Workflow

| Step | Trigger | Notification channel | Latency from trigger | FS-ID |
|---|---|---|---|---|
| 1 | Diary due time + grace period | Push notification | T+0 | FS-RLR-01 |
| 2 | Push not opened within 1 h | SMS | T+1 h | FS-RLR-01 |
| 3 | SMS unread within 4 h | Email | T+4 h | FS-RLR-01 |
| 4 | Email unread within 12 h | Site notification | T+12 h | FS-RLR-01 |
| 5 | Site notification + 24 h without entry | Site outreach script triggered | T+36 h | FS-RLR-01 |
| 6 | After 3 consecutive misses (DS-EPRO-77) | Drop-Off Recovery workflow | per consecutive-miss threshold | FS-RLR-03 |
| 7 | Throughout: quiet-hours respect (DS-EPRO-76) | Suppression 22:00-07:00 patient-local | per TZ | FS-RLR-02 |

### 5.3 Onboarding Workflow

```
   [Patient invitation issued by site]
         │
         ▼
   [Step 1: Identity verification (sponsor-defined per study)]
         │
         ▼
   [Step 2: Device pairing — BYOD or provisioned tablet]
         │
         ▼ BYOD: jailbreak/root detection (DS-EPRO-35); OS version check (DS-EPRO-37)
         ▼ Provisioned: Clario MDM enrolment (DS-EPRO-36)
   [Step 3: Study-credential issuance (Clario per-study credentials)]
         │
         ▼
   [Step 4: Consent re-confirmation]
         │
         ▼
   [Step 5: Onboarding tutorial in patient language (WCAG 2.1 AA, DS-EPRO-82)]
         │
         ▼ Completion event captured with timestamp + verifier + method (DS-EPRO-80)
   [Entry-into-study unlocked]
```

### 5.4 Study Build Promotion Workflow

| Step | Environment | Actor | SoD Check | Audit-trail event |
|---|---|---|---|---|
| 1 | DEV | Author (Study Builder) | — | `STUDY_BUILD_EDIT` |
| 2 | DEV → QC | Author | — | `STUDY_PROMOTE_QC` |
| 3 | QC → UAT | Author | Reviewer sign-off | `STUDY_PROMOTE_UAT` |
| 4 | UAT execution | UAT Lead | — | `STUDY_UAT_EXEC` |
| 5 | UAT → PROD | Approver (Author ≠ Approver per DS-EPRO-17) | SoD enforced | `STUDY_PROMOTE_PROD` |
| 6 | Auto-deposit to Marinos eTMF (DS-EPRO-104) | System | — | `ETMF_DEPOSIT` |
| 7 | Auto-generate CTIS pack (DS-EPRO-105) | System | — | `CTIS_PACK_GEN` |

### 5.5 AE Signal → Investigator Workflow

```
   [Diary entry submitted]
         │
         ▼ AE-signal detection engine (DS-EPRO-83)
   ┌────────────────────────────────────────────────────────┐
   │  Out-of-range PRO score   │ Free-text symptom keyword   │
   └─────────┬──────────────────┴──────────┬─────────────────┘
             │                              │
             └──────────────┬───────────────┘
                            ▼
   [Site Investigator workflow notification (red-flag on dashboard)]
                            │
                            ▼ Investigator review
   ┌────────────────────────────────────────────────────────┐
   │  Confirm AE → push to Marigold EDC AE module             │
   │              (idempotent on AE-id, DS-EPRO-84)           │
   │  Confirm SAE → red-flag indicator + immediate Argus      │
   │               cross-link (DS-EPRO-88)                    │
   │  Not an AE → close as non-event with reason              │
   └────────────────────────────────────────────────────────┘
                            │
                            ▼
   [Audit-trail entry for every decision (DS-EPRO-39)]
```

---

## 6. Role-Permission Matrix Design

| Role | Diary Entry | View Patient Data | Build Study | Promote DEV→QC | Promote QC→UAT | Promote UAT→PROD | AE Confirm | View Dashboard | Audit-Trail Read | Tenant Admin |
|---|---|---|---|---|---|---|---|---|---|---|
| Patient | ✓ (own only) | (own only) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Site Investigator (PI) | ✗ | ✓ (assigned subjects) | ✗ | ✗ | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ |
| Site Coordinator | ✗ | ✓ (assigned subjects) | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ |
| Sponsor Monitor (CRA) | ✗ | ✓ (scoped) | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | (limited) | ✗ |
| Study Builder (Author) | ✗ | ✗ | ✓ (DEV only) | ✓ | ✓ | ✗ (SoD: cannot be Approver) | ✗ | ✗ | ✗ | ✗ |
| Study Approver | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (SoD: cannot be Author) | ✗ | ✗ | ✗ | ✗ |
| UAT Lead | ✗ | ✗ | (UAT exec only) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Director eCOA Operations | ✗ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✓ | ✗ |
| Privacy / DPO | ✗ | (privacy events only) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (privacy) | ✗ |
| VP QA | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✓ | ✗ |
| VP Clinical Operations | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ |
| Tenant Admin (Clario) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (config only) |
| Reg Affairs (CTIS) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✓ (export-CTIS) | ✗ |
| Vendor Assurance Owner | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (vendor events) | ✗ |

**Role-permission design rules:**
- **SoD** — Study Builder ≠ Study Approver (DS-EPRO-17).
- **Patient surface authentication tenant** is fully separate from sponsor-admin authentication tenant (DS-EPRO-01..04).
- **Privacy / DPO** sees only privacy events (subject-id pattern review, DPIA-related, GDPR Art. 22 algorithmic-decision logs).
- **Tenant Admin** excludes patient-data and audit-trail UPDATE / DELETE.

---

## 7. Integration Design

### 7.1 Marigold EDC Push (FS-INT-EDC-01 / FS-XINT-EDC-01..03)

| Item | Value |
|---|---|
| Protocol | REST + ODM-XML |
| Endpoint | `POST https://marigold.mdsol.com/datapoints` |
| Idempotency-Key | `{study_id, subject_id, visit_id, instrument_id, item_id, completion_ts}` |
| Auth | OAuth2 client-credentials |
| Retry Schedule | back-off 1 s → 1024 s |
| DLQ Topic | `iolanthe.edc.dlq` |
| Reconciliation Cadence | Daily (hash comparison) |
| SLO Alert | Prometheus `iolanthe_edc_publish_lag_seconds` > 600 s P95 |
| Instrument-Version Guard | Active ePRO `instrument_version` must equal Rave-registered version (FS-XINT-EDC-03) |

### 7.2 Marinos eTMF (FS-INT-ETMF-01)

| Item | Value |
|---|---|
| Endpoint | `POST https://marinos.veevavault.com/v1/etmf-deposit/` |
| Trigger | Study-build approval |
| Payload | Study build artefacts |
| Auth | OAuth2 |

### 7.3 CTIS Sponsor Workspace (FS-INT-CTIS-01)

| Item | Value |
|---|---|
| Schema | EU CTR Art. 25 XML |
| Validation | CI contract test against published CTIS schema |
| Routing | Sponsor Reg Affairs–mediated upload |

### 7.4 Sponsor RBM (FS-INT-RBM-01)

| Item | Value |
|---|---|
| Endpoint | per-sponsor (configurable per-study) |
| Payload | Adherence + completion + time-of-day patterns |
| Auth | OAuth2 |
| Cadence | Daily |

### 7.5 Identity (FS-XSYS-AD-01)

| Tenant | Endpoint | Conditional-Access Policy | MFA Methods |
|---|---|---|---|
| Sponsor admin (Entra ID) | `iolanthe.azuread.local` | Clinical-Sensitive Conditional Access (FIDO2 + device-compliance) | FIDO2 WebAuthn, YubiKey, Okta Verify Push |
| Patient (Entra External ID) | `iolanthe-patients.azuread.local` | Patient-Facing Conditional Access (MFA via authenticator app or SMS fallback per IRB approval) | Microsoft Authenticator, SMS (per IRB approval) |

### 7.6 Backup (FS-XSYS-BAK-01)

| Item | Value |
|---|---|
| Backup Solution | Veeam Application-Aware + Oracle RMAN (ePRO Oracle backend) + MS SQL VSS (admin metadata) |
| Tier | T1 / RPO ≤ 4 h / RTO ≤ 4 BH |
| Immutable Cloud Tier | S3 Object Lock Compliance (geo-replicated) |
| Air-Gap Media | LTO-9 monthly |
| Restore-Test Cadence | Monthly QA-witnessed per AUR-FS-BACKUP-001 |
| Restore-Certificate Retention | ≥ 25 y in eQMS |

---

## 8. Site-Deployed Components Design

| Component | Type | Source location | Owner team | Verified by |
|---|---|---|---|---|
| `epro-to-edc-publisher` | Service | `git.iolanthe-prod.local/ecoa/epro-to-edc-publisher` | eCOA Engineering | OQ-EDC-01..04 |
| `epro-edc-reconcile-job` | Scheduled (daily) | `git.iolanthe-prod.local/ecoa/epro-edc-reconcile-job` | eCOA Engineering | OQ-EDC-03 |
| `instrument-version-guard` | Library | `git.iolanthe-prod.local/ecoa/instrument-version-guard` | eCOA Engineering | OQ-EDC-04 |
| `diary-compliance-dashboard-api` | Service | `git.iolanthe-prod.local/ecoa/diary-compliance-dashboard-api` | eCOA Engineering | OQ-DCD-01..05 |
| `reminder-ladder-engine` | Daemon | `git.iolanthe-prod.local/ecoa/reminder-ladder-engine` | eCOA Engineering | OQ-RLR-01..04 |
| `ae-signal-detector` | Service | `git.iolanthe-prod.local/ecoa/ae-signal-detector` | eCOA Engineering | OQ-AE-01..06 |
| `tz-scheduler` | Library | `git.iolanthe-prod.local/ecoa/tz-scheduler` | eCOA Engineering | OQ-TZ-01..04 |
| `linguistic-validation-registry-api` | Service | `git.iolanthe-prod.local/ecoa/linguistic-validation-registry-api` | eCOA Engineering | OQ-LING-01..04 |
| `subject-id-validator` | Library | `git.iolanthe-prod.local/ecoa/subject-id-validator` | eCOA Engineering | OQ-PRIV-06 |
| `onboarding-flow-service` | Service | `git.iolanthe-prod.local/ecoa/onboarding-flow-service` | eCOA Engineering | OQ-ONB-01..03 |
| `recruitment-funnel-job` | Scheduled | `git.iolanthe-prod.local/ecoa/recruitment-funnel-job` | eCOA Engineering | OQ-RR-01..02 |

Each repository carries a `docs/SDS.md` mini-Software-Design-Specification artefact per GAMP 5 2nd-edition § 2B.4 rule 6.

---

## 9. References

### 9.1 US

- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- FDA *Patient-Reported Outcome Measures* (2009).
- FDA *PFDD Guidance series*.
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).
- FDA *Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions* (Aug 2025).
- HIPAA / HITECH.

### 9.2 EU

- EU CTR Reg. 536/2014 + CTIS Sponsor Handbook.
- GDPR Arts. 6, 9, 22, 32, 35.

### 9.3 DACH

- BfArM (DE); Paul-Ehrlich-Institut (DE); Swissmedic (CH); AGES PharmMed (AT).

### 9.4 International

- ICH E6(R3) GCP (Step 4, adopted 6 January 2025).
- ICH E8(R1); ICH E9(R1); ICH E2A; ICH E2B(R3).
- ISPOR Translation Principles.
- ISPE GAMP 5 (2nd Edition, 2022).
- PIC/S PI 041.
- ISO/IEC 27001:2022.
- WCAG 2.1 AA.

### 9.5 Vendor

- Clario — *eCOA Platform 2025 Configuration Reference*.
- Clario — *MDM service operational guide*.

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS ID | FS ID(s) | Notes |
|---|---|---|
| DS-EPRO-01 | FS-INT-AUTH-01 / FS-XSYS-AD-01 / FS-PART11-02 | Site User IdP |
| DS-EPRO-02 | FS-XSYS-AD-01 / FS-INT-AUTH-01 | Patient IdP |
| DS-EPRO-03 | FS-XSYS-AD-01 | Patient conditional-access |
| DS-EPRO-04 | FS-XSYS-AD-01 | Admin conditional-access |
| DS-EPRO-05 | FS-XSYS-AD-01 | SIEM forwarding |
| DS-EPRO-06 | FS-XSYS-AD-01 | PAM break-glass |
| DS-EPRO-07 | FS-PART11-02 | Service-account auth |
| DS-EPRO-08 | FS-PART11-07 | Force-reauth |
| DS-EPRO-09 | FS-PART11-08 / FS-SEC-02 | Lockout — site users |
| DS-EPRO-10 | FS-SEC-02 | Lockout — patients |
| DS-EPRO-11 | FS-VND-01 | Vendor-assurance |
| DS-EPRO-12 | FS-VND-02 / FS-VND-07 | Release-notes workflow |
| DS-EPRO-13 | FS-VND-03 | Sub-processor review |
| DS-EPRO-14 | FS-VND-04 | Cross-border flow |
| DS-EPRO-15 | FS-VND-05 | SLA review |
| DS-EPRO-16 | FS-VND-06 | SDLC evidence review |
| DS-EPRO-17 | FS-CFG-01 / FS-CCM-01 | Study-build lifecycle |
| DS-EPRO-18 | FS-CFG-02 | CTIS-compatible pack |
| DS-EPRO-19 | FS-CFG-03 | Configuration export |
| DS-EPRO-20 | FS-CCM-02 | Baselines |
| DS-EPRO-21 | FS-CCM-03 | Emergency-change review |
| DS-EPRO-22 | FS-LING-01 | Linguistic-validation registry |
| DS-EPRO-23 | FS-LING-02 | Out-of-validation block |
| DS-EPRO-24 | FS-LING-03 | DACH variants |
| DS-EPRO-25 | FS-LING-04 | Instrument-version watcher |
| DS-EPRO-26 | FS-PAT-01 | Patient entry schema |
| DS-EPRO-27 | FS-PAT-02 | Time-window enforcement |
| DS-EPRO-28 | FS-PAT-03 | Adherence dashboard |
| DS-EPRO-29 | FS-PAT-04 | Missed-entry ladder |
| DS-EPRO-30 | FS-PAT-05 | NTP sync verification |
| DS-EPRO-31 | FS-TZ-01 / FS-DI-04 | TZ storage |
| DS-EPRO-32 | FS-TZ-02 | DST handling |
| DS-EPRO-33 | FS-TZ-03 | Patient-TZ-change |
| DS-EPRO-34 | FS-TZ-04 | Site-coordinator TZ display |
| DS-EPRO-35 | FS-DEV-01 | BYOD registration |
| DS-EPRO-36 | FS-DEV-02 | Provisioned MDM |
| DS-EPRO-37 | FS-DEV-03 | OS version support |
| DS-EPRO-38 | FS-DEV-04 | Per-study BYOD vs Provisioned |
| DS-EPRO-39 | FS-AUD-01 / FS-PART11-03 | Audit-trail schema |
| DS-EPRO-40 | FS-AUD-02 | Tenant-admin audit |
| DS-EPRO-41 | FS-AUD-03 | Review cadence |
| DS-EPRO-42 | FS-AUD-04 | Retention |
| DS-EPRO-43 | FS-AUD-05 | RBM pattern surfacing |
| DS-EPRO-44 | FS-PART11-01 | § 11.10(a) |
| DS-EPRO-45 | FS-PART11-02 | § 11.10(d) |
| DS-EPRO-46 | FS-PART11-03 | § 11.10(e) |
| DS-EPRO-47 | FS-PART11-04 | § 11.50 |
| DS-EPRO-48 | FS-PART11-05 | § 11.70 |
| DS-EPRO-49 | FS-PART11-06 | § 11.100 |
| DS-EPRO-50 | FS-PART11-07 | § 11.200 |
| DS-EPRO-51 | FS-PART11-08 | § 11.300 |
| DS-EPRO-52 | FS-DI-01 | Attributable |
| DS-EPRO-53 | FS-DI-02 | Legible |
| DS-EPRO-54 | FS-DI-03 | Contemporaneous |
| DS-EPRO-55 | FS-DI-04 | Original |
| DS-EPRO-56 | FS-DI-05 | Accurate |
| DS-EPRO-57 | FS-DI-06 | Retrievability |
| DS-EPRO-58 | FS-PRV-01 | GDPR Art. 9 pseudonymisation |
| DS-EPRO-59 | FS-PRV-02 | DPIA URN |
| DS-EPRO-60 | FS-PRV-03 | GDPR Art. 22 block |
| DS-EPRO-61 | FS-PRV-04 | Cross-border route |
| DS-EPRO-62 | FS-BYOPID-01 | Pseudonymisation boundary |
| DS-EPRO-63 | FS-BYOPID-02 | Subject-ID validation |
| DS-EPRO-64 | FS-BYOPID-03 | Subject-ID privacy review |
| DS-EPRO-65 | FS-SEC-01 | TLS/AES stance |
| DS-EPRO-66 | FS-SEC-02 | Patient credentials |
| DS-EPRO-67 | FS-SEC-03 | Annual vendor cert review |
| DS-EPRO-68 | FS-SEC-04 | Annual pen-test |
| DS-EPRO-69 | FS-SEC-05 | PII minimisation |
| DS-EPRO-70 | FS-DCD-01 | Diary compliance dashboard |
| DS-EPRO-71 | FS-DCD-02 | Sponsor RBM dashboard |
| DS-EPRO-72 | FS-DCD-03 | Outlier alert engine |
| DS-EPRO-73 | FS-DCD-04 | Compliance trend reports |
| DS-EPRO-74 | FS-DCD-05 | Site-coordinator worklist |
| DS-EPRO-75 | FS-RLR-01 | Reminder ladder stages |
| DS-EPRO-76 | FS-RLR-02 | Patient quiet hours |
| DS-EPRO-77 | FS-RLR-03 | Drop-Off recovery |
| DS-EPRO-78 | FS-RLR-04 | Patient-fatigue heuristic |
| DS-EPRO-79 | FS-ONB-01 | Onboarding flow |
| DS-EPRO-80 | FS-ONB-02 | Completion event |
| DS-EPRO-81 | FS-ONB-03 | Tutorial |
| DS-EPRO-82 | FS-ONB-04 | WCAG 2.1 AA |
| DS-EPRO-83 | FS-AE-01 | AE-signal engine |
| DS-EPRO-84 | FS-AE-02 | AE push to EDC |
| DS-EPRO-85 | FS-AE-03 | SAE-trigger surface |
| DS-EPRO-86 | FS-AE-04 | AE wording preservation |
| DS-EPRO-87 | FS-AE-05 | AE event timestamp |
| DS-EPRO-88 | FS-AE-06 | AE → PV cross-link |
| DS-EPRO-89 | FS-LIB-01 | eCOA library schema |
| DS-EPRO-90 | FS-LIB-02 | Instrument-version lifecycle |
| DS-EPRO-91 | FS-LIB-03 | Licensing check |
| DS-EPRO-92 | FS-LIB-04 | Scoring-rule engine |
| DS-EPRO-93 | FS-LIB-05 | Custom-instrument workflow |
| DS-EPRO-94 | FS-RR-01 | Recruitment funnel |
| DS-EPRO-95 | FS-RR-02 | Retention metrics |
| DS-EPRO-96 | FS-RR-03 | Patient-feedback survey |
| DS-EPRO-97 | FS-RR-04 | Compensation tracking |
| DS-EPRO-98 | FS-RR-05 | Channel attribution |
| DS-EPRO-99 | FS-RR-06 | Withdrawal reason |
| DS-EPRO-100 | FS-INT-EDC-01 / FS-XINT-EDC-01 | EDC push endpoint |
| DS-EPRO-101 | FS-XINT-EDC-01 | EDC idempotency-key |
| DS-EPRO-102 | FS-XINT-EDC-02 | EDC reconciliation job |
| DS-EPRO-103 | FS-XINT-EDC-03 | Instrument-version guard |
| DS-EPRO-104 | FS-INT-ETMF-01 | eTMF auto-deposit |
| DS-EPRO-105 | FS-INT-CTIS-01 | CTIS pack export |
| DS-EPRO-106 | FS-INT-RBM-01 | RBM data-feed |
| DS-EPRO-107 | FS-XSYS-BAK-01 / FS-BAK-01..03 | Backup integration |
| DS-EPRO-108 | FS-PERF-01 | P95 instrument-open |
| DS-EPRO-109 | FS-PERF-02 | Concurrent patient sessions |
| DS-EPRO-110 | FS-AV-01 | Clario SLA |
| DS-EPRO-111 | FS-AV-02 | Offline-mode capture |
| DS-EPRO-112 | FS-TRN-01 | LMS training gate |
| DS-EPRO-113 | FS-TRN-02 | Annual refresher |
| DS-EPRO-114 | FS-PR-01 | Annual periodic review |

---

## 11. Design-Level Risk Register

| ID | Design-level risk | Likelihood | Impact | Mitigation reference (DS) |
|---|---|---|---|---|
| DR-01 | DACH variant translation drift on shared base translation (de-DE vs de-AT vs de-CH) | Medium | High | DS-EPRO-24 distinct entries + DS-EPRO-25 instrument-version-change watcher |
| DR-02 | CTIS schema version change breaks pack export | Low | High | DS-EPRO-105 schema-version pin + CI contract test |
| DR-03 | Patient MFA-phone-lost recovery flow social-engineering exposure | Medium | High | Documented manual ID-verification protocol + audit-trail entry |
| DR-04 | Out-of-validation translation accessed by patient | Low | High | DS-EPRO-23 API 422 block |
| DR-05 | Patient-data mix-up via BYOD device sharing | Low | Critical | DS-EPRO-35 device registration + per-session re-auth |
| DR-06 | HIPAA / GDPR breach via cross-border transfer | Low | Critical | DS-EPRO-61 SCC route documentation + annual review |
| DR-07 | GDPR Art. 22 violation — automated decision affecting patient | Low | High | DS-EPRO-60 block at policy layer |
| DR-08 | Missed DPIA per study | Low | High | DS-EPRO-59 study-build-approval verification |
| DR-09 | Audit-trail tampering | Low | Critical | DS-EPRO-40 tenant-admin permission matrix |
| DR-10 | Time-window enforcement bypass due to device-clock drift | Medium | Medium | DS-EPRO-30 NTP-sync flag |
| DR-11 | EDC sync failure → data-flow gap | Medium | High | DS-EPRO-101 idempotency + DS-EPRO-102 daily reconciliation |
| DR-12 | Site-vs-patient time-zone mismatch silently mis-flags valid entries | Medium | Medium | DS-EPRO-31..34 TZ-aware design |
| DR-13 | BYOD OS / app update induces data-loss / sync failure | Medium | High | DS-EPRO-37 OS version support window + DS-EPRO-111 offline-mode |
| DR-14 | Language-pack drift on instrument-version change | Medium | Medium | DS-EPRO-25 invalidation + DS-EPRO-92 re-validation trigger |
| DR-15 | Patient drop-off after symptom-driven fatigue | Medium | Medium | DS-EPRO-77 drop-off recovery + DS-EPRO-78 fatigue heuristic |
| DR-16 | AE signal missed because flagged free-text not routed to investigator | Low | High | DS-EPRO-83 detection engine + DS-EPRO-85 SAE red-flag |
| DR-17 | Subject-ID validation rule (DS-EPRO-63) misclassifies legitimate sponsor-defined pattern as identifiable | Low | Medium | DS-EPRO-64 sampled Privacy Officer review |
| DR-18 | DST transition rolls over a 24 h diary window incorrectly | Low | Medium | DS-EPRO-32 DST-transition handling OQ-tested |
| DR-19 | Reminder ladder quiet-hours window (DS-EPRO-76) wrong for patient on travel | Low | Low | DS-EPRO-33 patient-TZ-change detection |
| DR-20 | Custom-instrument workflow (DS-EPRO-93) skips IRB approval check | Low | High | Approval gate enforced + DS-EPRO-91 licensing check |

The DS Design-level Risk Register is the design-stage seed for `IOL2-RA-EPRO-001`; per-FS-ID criticality remains in the FS Implementation Risk Register.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
