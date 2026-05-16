---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "DRY-FS-CTMS-001 v1.3 (parent FS)"
  - "DRY-URS-CTMS-001 v1.3 (parent URS, transitive)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 Configuration Specification conventions"
  - "21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300; 21 CFR Parts 312, 314, 50, 56"
  - "ICH E6(R3) GCP (Step 4, adopted 6 January 2025); ICH E8(R1); ICH E2A; ICH E2B(R3); ICH M11"
  - "EU CTR 536/2014 + CTIS Sponsor Handbook (current)"
  - "FDA Computerized Systems Used in Clinical Investigations (May 2007)"
  - "FDA BIMO Inspection Manual 7348.809 (4 April 2025)"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026; supersedes the September 2025 guidance)"
  - "Veeva Vault CTMS 24R3 / 25R1 vendor documentation; Veeva 24R3 Clinical Operations–EDC Connection"
  - "TMF Reference Model v3.3.x"
parent_fs:
  document_number: DRY-FS-CTMS-001
  version: 1.3
  file: ../../../FS_FDS/_generated/final/Dryad_Pharma_CTMS_FS_v1.3.md
parent_urs:
  document_number: DRY-URS-CTMS-001
  version: 1.3
  file: ../../../URS/_generated/final/CTMS_Clinical_Trial_Management_System__Dryad_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## CTMS — Veeva Vault CTMS (24R3 / 25R1) — Configuration Specification

**Document Number:** DRY-DS-CTMS-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Parent FS:** DRY-FS-CTMS-001 v1.3
**Parent URS:** DRY-URS-CTMS-001 v1.3 *(informational; transitive via FS)*
**Site:** Dryad Pharma a.s., Brno, Czech Republic *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Project Mode:** Sustaining + Configurable Change *(inherited from parent URS)*
**Regulatory Scope:** 21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300; 21 CFR Parts 312/314/50/56; ICH E6(R3) GCP (Step 4, adopted 6 January 2025); ICH E8(R1); ICH E2A; EU CTR 536/2014 + CTIS Sponsor Handbook (current); EU CTR Arts. 16, 37, 42, 58; FDA *Computerized Systems Used in Clinical Investigations* (May 2007); FDA BIMO Inspection Manual 7348.809 (4 April 2025); FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance); FDA *Conducting Remote Regulatory Assessments — Q&A* (June 2025 final); GDPR Reg. (EU) 2016/679 — Arts. 6, 17, 22, 32, 33, 35; EU GMP Annex 11 §§ 4, 6, 9, 11; ISO 14155:2020 (device arms); ISO/IEC 27001:2022; PIC/S PI 041; TMF RM v3.3.x.

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QA Reviewer) | _____________ | _____________ | _____ |
| Reviewer (System Owner — Director Clinical Operations IT) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — VP Clinical Operations) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs — CTIS) | _____________ | _____________ | _____ |
| Reviewer (Pharmacovigilance Lead) | _____________ | _____________ | _____ |
| Reviewer (Data Protection Officer) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Design Control

| Field | Value |
|---|---|
| Document Number | DRY-DS-CTMS-001 |
| Version | 1.1 |
| Effective Date *(synthetic)* | 2026-05-15 |
| Parent FS | DRY-FS-CTMS-001 v1.3 |
| Parent URS *(informational)* | DRY-URS-CTMS-001 v1.3 |
| Site | Dryad Pharma a.s., Brno, Czech Republic *(fictional)* |
| System Class (GAMP 5, 2nd ed.) | Category 4 — Configured Product (multi-tenant SaaS) |
| Project Mode | Sustaining + Configurable Change |
| Regulatory Scope | per Title block |
| Tier | T4 (inherited from parent URS+FS pair) |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue of platform-level Configuration Specification for Veeva Vault CTMS 24R3 / 25R1 corresponding to DRY-FS-CTMS-001 v1.3. Inherited Tier T4 from parent URS+FS pair. DS covers 152/152 FS-IDs (100% coverage). Vendor-internal Veeva Vault platform internals (Vault Connect transport layer, Veeva-managed audit-trail append-only DB primitives, Vault SLA-tracking internals) are flagged as **vendor-internal — no site design surface** and excluded from the DS coverage percentage per METHODOLOGY § 2B.10. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from DRY-URS-CTMS-001 v1.3 and DRY-FS-CTMS-001 v1.3. DS-specific additions:

| Term | Definition |
|---|---|
| CS | Configuration Specification (this document — Cat 4 DS shape) |
| CI | Configuration Item |
| DS-ID | Design Specification identifier |
| Vault Connect | Veeva's native cross-vault data-sharing service |
| Vault REST | Veeva's REST API |
| Clinical Operations–EDC Connection | Veeva 24R3 native EDC-CTMS protocol-deviation connection |
| EDL | Expected Document List (TMF Reference Model artefact set) |
| SCIM | System for Cross-domain Identity Management |
| MV / MVR | Monitoring Visit / Monitoring Visit Report |
| RBM | Risk-Based Monitoring |
| IMP | Investigational Medicinal Product |
| Vellis | Dryad's controlled-document EDMS (synthetic) |
| Marigold EDC | Dryad's EDC counterparty (cross-reference per FS) |
| MasterControl | Dryad's eQMS / CAPA system |

---

## 1. Purpose

This Configuration Specification defines the platform-tenancy-level configuration values, workflow designs, role-permission matrix, and integration endpoint designs that implement DRY-FS-CTMS-001 v1.3. It is the third document in the GAMP 5 V-model for the Dryad Vault CTMS platform.

## 2. Scope

### 2.1 In Scope

- Veeva Vault CTMS 24R3 / 25R1 tenancy configuration (lifecycle states, Vault Object schemas, role-permissions, audit-trail watchdog, signature workflows).
- Per-study + per-country + per-site + per-investigator object designs.
- Integration design — Okta SAML 2.0 + MFA + SCIM; Vault eTMF cross-vault link; Medidata Rave EDC (Clinical Operations–EDC Connection per Vault 24R3); Medidata RTSM / Calyx IXRS; Oracle Argus 8.4 (read-only PV metadata); MasterControl (eQMS CAPA REST); Financials (idempotent payment push); HR (SCIM); CTIS sponsor workspace; BfArM / PEI / AGES / Swissmedic national-CA gateways.
- Vault Risk Register + RBM indicator computation design.
- Inspection-readiness bundle design (BIMO + EMA + DACH inspections).
- DACH-locale + time-zone-aware design.
- Cross-system planes — QTZ AD identity; AUR backup tier (Veeam + Oracle RMAN + S3 Object Lock); Helios audit-event bus; LMS competence adapter.

### 2.2 Out of Scope

- Per-study eCRF / monitoring-visit-template body (covered in per-study DS sub-documents).
- Vault platform internals (vendor SDLC).
- Cross-system Active Directory tenancy design (covered in QTZ-DS-AD-001).
- Cross-system Veeam backup-infrastructure topology design (covered in AUR-DS-BACKUP-001).
- eTMF artefact-classification design (covered in MRN-DS-ETMF-001).

## 3. Architectural Overview

The Dryad Vault CTMS platform is a **multi-tenant SaaS** Cat 4 system operating as the Clinical-Operations hub. It is the single source of truth for protocol / country / site / investigator / monitoring-visit / payment / vendor / deviation / DSMB tracking, integrating with seven counterparty systems plus four national-CA gateways.

### 3.1 Platform Architectural Diagram

```
                       ┌────────────────────────────────────────────┐
                       │           Okta IdP (SAML 2.0 + MFA)        │
                       │       SCIM 2.0 provisioning ≤ 24 h         │
                       └────────────────────┬───────────────────────┘
                                            │ SAML / SCIM
                                            ▼
  ┌─────────────────────────────────────────────────────────────────────────────┐
  │       Veeva Vault CTMS 24R3 / 25R1 (Dryad tenancy)                          │
  │                                                                             │
  │   Vault Objects: Protocol / Amendment / Country / Site / Investigator /     │
  │   Delegation Log / 1572 / Site Lifecycle / Monitoring Visit / MVR /         │
  │   Action Item / Issue / Deviation / DSMB / Risk Register / Vendor /         │
  │   Payment / Budget / Document Registry (IB/Protocol/ICF)                    │
  │                                                                             │
  │   Site Lifecycle State Machine: IDENTIFIED → QUALIFIED → INITIATED →        │
  │   ENROLLING → ENROLLMENT_CLOSED → FOLLOW_UP → CLOSED                        │
  └──┬──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┬─────────────────┘
     │      │      │      │      │      │      │      │      │
     ▼      ▼      ▼      ▼      ▼      ▼      ▼      ▼      ▼
  ┌────┐┌────┐┌────┐┌──────┐┌──────┐┌────┐┌────┐┌────┐┌──────────┐
  │Vault││Marigold││RTSM││Argus  ││Master││Fin.││ HR ││CTIS ││National  │
  │eTMF ││Rave   ││IXRS││ 8.4   ││Control││sys.││sys.││spons││CA gateways│
  │(Conn││(Clin. ││    ││(PV   ││(CAPA  ││(pay││(CRA││ wksp ││BfArM /   │
  │ect) ││ Ops–  ││    ││metad)││ REST) ││push)│ asgn││      ││ PEI /    │
  │     ││ EDC   ││    ││      ││       ││    ││    ││      ││ AGES /   │
  │     ││ Conn.)││    ││      ││       ││    ││    ││      ││ Swissmed │
  └────┘└────┘└────┘└──────┘└──────┘└────┘└────┘└────┘└──────────┘
       │
       ▼
  ┌────────────────────────────────────────────────────────────────────────────┐
  │  Cross-system planes                                                       │
  │  • QTZ AD / Entra ID (SAML+SCIM, Splunk gxp-authn, CyberArk PAM)           │
  │  • AUR Backup (Veeam + Oracle RMAN + S3 Object Lock Compliance + LTO-9)    │
  │  • Helios audit-event bus (Kafka helios.ingest.dryad.ctms.v1)              │
  │  • LMS competence adapter (mTLS GET /lms/competence/{user_id})             │
  └────────────────────────────────────────────────────────────────────────────┘
```

### 3.2 Environment Plan

| Environment | Vault URL pattern | Promotion source | Subject data |
|---|---|---|---|
| DEV | `dryad-dev.veevavault.com` | — (authoring) | Synthetic |
| UAT | `dryad-uat.veevavault.com` | DEV (Vault config-migration) | Synthetic |
| PRODUCTION | `dryad.veevavault.com` | UAT (signed) | Real |

### 3.3 Counterparty Integration Map

| Counterparty | Protocol | Direction | Endpoint pattern | Auth |
|---|---|---|---|---|
| Okta IdP | SAML 2.0 + SCIM 2.0 | bidirectional | `dryad.okta.com` | TLS 1.3 + mutual cert |
| Vault eTMF (Marinos cross-vault) | Vault Connect | bidirectional | `marinos.veevavault.com` | OAuth2 client-credentials |
| Medidata Rave EDC | Vault Connect + Clinical Operations–EDC Connection | bidirectional | `marigold.mdsol.com` | OAuth2 |
| Medidata RTSM / Calyx IXRS | REST | inbound | `rtsm.mdsol.com` | OAuth2 |
| Oracle Argus 8.4 | REST (read-only metadata) | inbound | `argus.dryad-prod.local` | mTLS |
| MasterControl (eQMS) | REST | bidirectional | `mc.dryad-prod.local` | OAuth2 + Idempotency-Key |
| Financials | REST | outbound | `fin.dryad-prod.local` | OAuth2 + Idempotency-Key |
| HR | SCIM 2.0 (via Okta) | inbound | `okta.dryad-prod.local` | mutual cert |
| CTIS sponsor workspace | sponsor-mediated upload | outbound | EMA CTIS | sponsor user-mediated |
| BfArM gateway (DE — medicinal products) | mTLS | outbound | `bfarm-gw.dryad-prod.local` | mTLS |
| PEI gateway (DE — biologicals) | mTLS | outbound | `pei-gw.dryad-prod.local` | mTLS |
| AGES gateway (AT) | mTLS | outbound | `ages-gw.dryad-prod.local` | mTLS |
| Swissmedic gateway (CH) | mTLS | outbound | `sm-gw.dryad-prod.local` | mTLS |
| Helios audit-event bus | Kafka | outbound | `kafka.helios.dryad-prod.local` | mTLS + SASL/SCRAM |
| LMS competence adapter | REST | outbound | `lms.dryad-prod.local` | mTLS + Entra workload-identity |

---

## 4. Configuration Specification

### 4.1 Tenancy + SSO Configuration

| CI-ID | Configuration item (Veeva-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-01 | Vault IdP Mode | `Okta SAML 2.0 + MFA (external IdP)` | Custom | Per FS-INT-SSO-01 — Vault local accounts disabled in production. | FS-INT-SSO-01, FS-PART11-04 | OQ-AUTHN-01 |
| DS-CTMS-02 | Vault Local-Account Provisioning | `Disabled in production` | Custom | Per FS-INT-SSO-01. | FS-INT-SSO-01, FS-PART11-11 | OQ-AUTHN-02 |
| DS-CTMS-03 | SCIM Endpoint | `https://dryad.veevavault.com/scim/v2/` | Default | Per Veeva 24R3 SCIM spec. | FS-INT-SSO-02 | IQ-SCIM-01 |
| DS-CTMS-04 | SCIM Deprovisioning Latency | `≤ 24 h on HR termination` | Custom | Per FS-INT-HR-01 + FS-INT-SSO-02. | FS-INT-HR-01, FS-INT-SSO-02 | OQ-SCIM-01 |
| DS-CTMS-05 | Okta Group Naming | `dryad-vault-{role}-{study_id}` | Custom | Per-study scoping for FS-SEC-02 access reviews. | FS-INT-SSO-02, FS-SEC-02 | OQ-AUTHN-03 |
| DS-CTMS-06 | Conditional-Access Policy Binding | `Clinical-Sensitive Conditional Access (FIDO2 + sponsor-tenant isolation)` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-CA-01 |
| DS-CTMS-07 | SIEM Forwarding | `Splunk `gxp-authn` syslog RFC 5424; lag ≤ 5 min` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01, FS-AUD-01 | OQ-SIEM-01 |
| DS-CTMS-08 | Break-Glass PAM | `CyberArk PAM — 24 h password-rotation + dual-witness check-out` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-PAM-01 |
| DS-CTMS-09 | Session Timeout | `30 minutes idle` | Default | Per FS-SEC-01. | FS-SEC-01 | OQ-SESS-01 |
| DS-CTMS-10 | Force-Reauth on Signature | `Enabled (max-age 5 min OAuth2 token)` | Custom | Per FS-PART11-12. | FS-PART11-12 | OQ-PART11-200 |
| DS-CTMS-11 | MFA Methods | `Okta Verify Push, FIDO2 WebAuthn, YubiKey` | Custom | Phishing-resistant MFA per Dryad InfoSec. | FS-PART11-04, FS-PART11-13 | OQ-MFA-01 |

### 4.2 Password + Lockout Policy

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-12 | Password Minimum Length | `14 characters` | Custom | Per FS-PART11-13. | FS-PART11-13 | OQ-PART11-300 |
| DS-CTMS-13 | Password History | `12` | Custom | Per FS-PART11-13. | FS-PART11-13 | OQ-PART11-300 |
| DS-CTMS-14 | Password Max Age | `90 days` | Custom | Per FS-PART11-13. | FS-PART11-13 | OQ-PART11-300 |
| DS-CTMS-15 | Lockout Threshold | `5 failures` | Custom | Per FS-PART11-13. | FS-PART11-13 | OQ-PART11-300 |
| DS-CTMS-16 | User-ID Uniqueness | `Strict — never reassigned` | Custom | Per FS-PART11-11. | FS-PART11-11 | OQ-PART11-100 |

### 4.3 Protocol + Amendment Object Configuration

| CI-ID | Configuration item (Vault Object) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-17 | Vault Protocol Object Schema | `protocol_id, version, version_effective_date, ib_version_ref, sponsor_approval_sig, country_submission_status[]` | Custom | Per FS-PROT-01. | FS-PROT-01 | OQ-PROT-01 |
| DS-CTMS-18 | Vault Amendment Object Schema | `amendment_id, version, effective_date, impact_category ∈ {ADMINISTRATIVE, SUBSTANTIAL}, change_summary, propagation_status` | Custom | Per FS-PROT-02. | FS-PROT-02 | OQ-PROT-02 |
| DS-CTMS-19 | Substantial-Modification Workflow | `ctis-sm-submission workflow: DRAFT → SUBMITTED → CA_DECISION → PUBLISHED` | Custom | Per FS-PROT-03. | FS-PROT-03, FS-CTIS-01 | OQ-PROT-03 |
| DS-CTMS-20 | Amendment Downstream-Task Generator | `Auto-generates: re-consent tasks (Marigold URS-CONSENT-*), EDC re-build (Marigold URS-BUILD), monitoring-plan update (FS-MV-*)` | Custom | Per FS-PROT-04. | FS-PROT-04 | OQ-PROT-04 |

### 4.4 Country + Site Lifecycle Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-21 | Vault Country Object | `country_id, national_ca ∈ {BfArM, PEI, AGES, Swissmedic, FDA, …}, submission_status_initial, substantial_modifications[], end_of_trial_status, planned_activation_date, actual_activation_date` | Custom | Per FS-CTRY-01. | FS-CTRY-01 | OQ-CTRY-01 |
| DS-CTMS-22 | Country-Milestone Gating | `CA submission → CA decision → IRB/EC approval → first site activation; each gate captures planned + actual + signatures` | Custom | Per FS-CTRY-02. | FS-CTRY-02 | OQ-CTRY-02 |
| DS-CTMS-23 | Vault Site Object | `site_id, country_id, pi_id, address (AES-256 encrypted at rest), irb_ec_oversight, lifecycle_state` | Custom | Per FS-SITE-01 + FS-SEC-03. | FS-SITE-01, FS-SEC-03 | OQ-SITE-01 |
| DS-CTMS-24 | Site Activation Checklist | `1572 + CV + financial-disclosure + IRB/EC approval + current ICF + site-staff training + signed CTA + insurance + SIV report` | Custom | Per FS-SITE-02. | FS-SITE-02 | OQ-SITE-02 |
| DS-CTMS-25 | Site Activation Gate | `Requires CRA Lead signature + country CA decision (DS-CTMS-22) + checklist completion (DS-CTMS-24)` | Custom | Per FS-SITE-03. | FS-SITE-03 | OQ-SITE-03 |
| DS-CTMS-26 | Site Lifecycle State Machine | `IDENTIFIED → QUALIFIED → INITIATED → ENROLLING → ENROLLMENT_CLOSED → FOLLOW_UP → CLOSED` | Custom | Per FS-SITE-01 + FS-SITE-04. | FS-SITE-01, FS-SITE-04 | OQ-SITE-04 |
| DS-CTMS-27 | Site Contacts PII Encryption | `AES-256 at rest + TLS 1.3 in transit` | Custom | Per FS-SITE-05 + FS-SEC-03. | FS-SITE-05, FS-SEC-03 | OQ-PRIV-01 |
| DS-CTMS-28 | Site Enrolment Plan vs Actual Report | `Vault Report: country + study aggregates; `enrol-forecast-job` daily refresh` | Custom | Per FS-SITE-06 + FS-REC-02. | FS-SITE-06, FS-REC-02 | OQ-REC-01 |

### 4.5 Investigator + Delegation Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-29 | Vault Investigator Object | `investigator_id, name, credentials, cv_version, financial_disclosure_status, coi_status, training_records[], study_assignments[]` | Custom | Per FS-INV-01. | FS-INV-01 | OQ-INV-01 |
| DS-CTMS-30 | Vault 1572 Sub-Object | `form_version, effective_date, signed_by_pi_date, subinvestigators[]; re-sign triggers per 21 CFR § 312.53(c)` | Custom | Per FS-INV-02. | FS-INV-02 | OQ-INV-02 |
| DS-CTMS-31 | Delegation Log Object | `delegated_tasks ∈ {INFORMED_CONSENT, DOSE_PREP, DATA_ENTRY, AE_ASSESSMENT, SAMPLE_COLLECTION}, delegate_id, start_date, end_date, pi_signature_date` | Custom | Per FS-INV-03. | FS-INV-03 | OQ-INV-03 |
| DS-CTMS-32 | Training-Check Job | `inv-training-check-job — runs at site-activation + periodic-review; expired training blocks activation + P2 alert` | Custom | Per FS-INV-04. | FS-INV-04 | OQ-INV-04 |
| DS-CTMS-33 | PI-Transition Workflow | `pi-transition — new 1572 + IRB notification + sub-I re-delegation + ICF re-approval task + old PI → INACTIVE` | Custom | Per FS-INV-05. | FS-INV-05 | OQ-INV-05 |

### 4.6 Recruitment + Monitoring Visit Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-34 | Enrolment Plan Capture | `Per-site enrolment plan at study start; actuals via Vault Connect from EDC + RTSM daily` | Custom | Per FS-REC-01. | FS-REC-01 | OQ-REC-02 |
| DS-CTMS-35 | Enrolment Forecast Job | `enrol-forecast-job — daily; FPI / LPI / LPLV projection given velocity + dropout` | Custom | Per FS-REC-02. | FS-REC-02 | OQ-REC-03 |
| DS-CTMS-36 | Recruitment KPI Set | `screen-failure rate, screen-to-randomise ratio, time-to-FPI, time-to-LPI` | Custom | Per FS-REC-03. | FS-REC-03 | OQ-REC-04 |
| DS-CTMS-37 | Recruitment Exception Rules | `Site < 50% plan for > 30 d; country stalled → action items` | Custom | Per FS-REC-04 + FS-ISS-02. | FS-REC-04 | OQ-REC-05 |
| DS-CTMS-38 | MV Type Vocabulary | `SIV, IMV, MMV, COV, REMOTE_MV` | Custom | Per FS-MV-01. | FS-MV-01 | OQ-MV-01 |
| DS-CTMS-39 | MVR Object Schema | `mvr_id, visit_type, site_id, planned_date, actual_date, attendees[], findings, action_items[], follow_up_sla, deviations[], sae_followup[], signature_blocks[]` | Custom | Per FS-MV-02. | FS-MV-02 | OQ-MV-02 |
| DS-CTMS-40 | MVR Signature Workflow | `CRA Lead signature via Vault e-signature; signed MVRs immutable; un-sign requires Director Clinical Ops IT approval` | Custom | Per FS-MV-03. | FS-MV-03 | OQ-MV-03 |
| DS-CTMS-41 | MVR Action-Item Escalation | `T+0 owner / T+7 CRA Lead / T+14 Clinical Ops Manager` | Custom | Per FS-MV-04. | FS-MV-04 | OQ-MV-04 |
| DS-CTMS-42 | MV Due-Date Watch Job | `mvr-due-date-watch — alerts T-7, T-0, T+7, T+14 against per-study SLA; missed-MVR streak → RBM indicator` | Custom | Per FS-MV-05 + FS-RBM-02. | FS-MV-05, FS-RBM-02 | OQ-MV-05 |
| DS-CTMS-43 | MVR Template Versioning | `Pinned at study level; mid-study change → template-version pinning + change-control` | Custom | Per FS-MV-06. | FS-MV-06 | OQ-MV-06 |

### 4.7 SDV Plan + RBM Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-44 | SDV Plan Configuration | `CtQ-tagged critical 100%; non-critical risk-based per CDISC CT` | Custom | Per FS-SDV-01. | FS-SDV-01 | OQ-SDV-01 |
| DS-CTMS-45 | SDV Completion Ingest | `Daily from Marigold MAR-FS-EDC-001 RBM feed (FS-RBM-01)` | Custom | Per FS-SDV-02. | FS-SDV-02 | OQ-SDV-02 |
| DS-CTMS-46 | SDV Exception Job | `sdv-exception-job — surfaces fields-not-yet-SDV'd at lock checkpoint` | Custom | Per FS-SDV-03. | FS-SDV-03 | OQ-SDV-03 |
| DS-CTMS-47 | Risk Register Object | `risk_id, category (per ICH E6(R3) § 3), description, likelihood, impact, mitigation, owner, status` | Custom | Per FS-RBM-01. | FS-RBM-01 | OQ-RBM-01 |
| DS-CTMS-48 | RBM Indicator Job | `rbm-indicator-job — daily from CTMS + EDC + RTSM + Argus feeds → Vault Dashboard` | Custom | Per FS-RBM-02. | FS-RBM-02 | OQ-RBM-02 |
| DS-CTMS-49 | RBM Threshold Action Routing | `Threshold breach → Action Items routed to CRA + CRA Lead with mandatory mitigation plan template` | Custom | Per FS-RBM-03 + FS-ISS-02. | FS-RBM-03 | OQ-RBM-03 |
| DS-CTMS-50 | RBM Dashboard Navigation | `Study / country / site / indicator drill-down; daily-digest email to central monitoring leads` | Custom | Per FS-RBM-04. | FS-RBM-04 | OQ-RBM-04 |
| DS-CTMS-51 | Risk-Register Review Cadence | `≥ every 4 weeks during enrolment via `risk-review-reminder`; signed Vault record` | Custom | Per FS-RBM-05. | FS-RBM-05 | OQ-RBM-05 |

### 4.8 Issue + CAPA Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-52 | Issue Object | `issue_id, source, severity ∈ {LOW, MED, HIGH, CRITICAL}, owner, due_date, status, evidence` | Custom | Per FS-ISS-01. | FS-ISS-01 | OQ-ISS-01 |
| DS-CTMS-53 | MasterControl CAPA REST Endpoint | `POST /v1/capa/create` with `Idempotency-Key: {study_id}:{deviation_id}` | Custom | Per FS-ISS-03 + FS-INT-EQMS-01. | FS-ISS-03, FS-INT-EQMS-01 | OQ-CAPA-01 |
| DS-CTMS-54 | MasterControl CAPA Status Feedback | `GET /v1/capa/status` polled hourly; surfaced on Issue record | Custom | Per FS-INT-EQMS-02. | FS-INT-EQMS-02 | OQ-CAPA-02 |
| DS-CTMS-55 | Issue / AI KPI Set | `open count, overdue count, mean-time-to-close` | Custom | Per FS-ISS-04. | FS-ISS-04 | OQ-ISS-02 |

### 4.9 Drug Supply + Payment Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-56 | RTSM Ingest Job | `drug-supply-ingest — daily; per-site inventory + dispensed/returned/unused/destroyed counts` | Custom | Per FS-DRG-01. | FS-DRG-01 | OQ-DRG-01 |
| DS-CTMS-57 | Drug Forecast Horizon | `4 / 8 / 12 weeks` | Custom | Per FS-DRG-02. | FS-DRG-02 | OQ-DRG-02 |
| DS-CTMS-58 | Drug Shortfall Alert | `Projected coverage < 4 weeks → Supply Chain + CRA action item` | Custom | Per FS-DRG-03. | FS-DRG-03 | OQ-DRG-03 |
| DS-CTMS-59 | Drug-Accountability Reconciliation | `Daily across CTMS / RTSM / EDC drug-acct eCRFs; unreconciled → RBM indicator` | Custom | Per FS-DRG-04. | FS-DRG-04 | OQ-DRG-04 |
| DS-CTMS-60 | Vault Payment Sub-Object | `Linked to Milestones; payment schedule auto-generated from CTA terms` | Custom | Per FS-PAY-01. | FS-PAY-01 | OQ-PAY-01 |
| DS-CTMS-61 | Financials REST Endpoint | `POST /v1/payments/initiate` with `Idempotency-Key: {study_id}:{site_id}:{milestone_id}:{payment_id}` | Custom | Per FS-PAY-02 + FS-INT-FIN-01. | FS-PAY-02, FS-INT-FIN-01 | OQ-PAY-02 |
| DS-CTMS-62 | Overpayment Guard | `Pre-submit check against Vault Payment History; payment against fully-paid milestone blocked` | Custom | Per FS-PAY-03. | FS-PAY-03 | OQ-PAY-03 |
| DS-CTMS-63 | Payment Forecast Report | `Vault Report — current quarter + next 2; per study / country / site` | Custom | Per FS-PAY-04. | FS-PAY-04 | OQ-PAY-04 |
| DS-CTMS-64 | Payment History Export | `Vault Report per site per study` | Default | Per FS-PAY-05. | FS-PAY-05 | OQ-PAY-05 |
| DS-CTMS-65 | Vault Budget Object | `Line items (sites, MVs, central labs, imaging, drug supply, vendors); `budget-actuals-job` monthly` | Custom | Per FS-BUD-01. | FS-BUD-01 | OQ-BUD-01 |
| DS-CTMS-66 | Cost-Overrun Alert | `Line > 110% plan → Clinical Operations Manager action item` | Custom | Per FS-BUD-02. | FS-BUD-02 | OQ-BUD-02 |
| DS-CTMS-67 | Financials Monthly Reconciliation | `payment-reconcile-job — monthly CTMS-initiated vs Financials-confirmed` | Custom | Per FS-INT-FIN-02. | FS-INT-FIN-02 | OQ-FIN-01 |

### 4.10 Vendor + eTMF Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-68 | Vault Vendor Object | `vendor_id, type ∈ {CRO, CENTRAL_LAB, IMAGING, EPRO, LIMS, OTHER}, scope, contract_version, contract_effective_start_end, kpis` | Custom | Per FS-VEN-01. | FS-VEN-01 | OQ-VEN-01 |
| DS-CTMS-69 | Vendor Feed Reconciliation Status | `Daily tracking; failure → action item via FS-ISS-02` | Custom | Per FS-VEN-02. | FS-VEN-02 | OQ-VEN-02 |
| DS-CTMS-70 | Vendor KPI Report | `Quarterly — data-freshness, on-time-delivery, query-response time` | Custom | Per FS-VEN-03. | FS-VEN-03 | OQ-VEN-03 |
| DS-CTMS-71 | Vendor Change-Order Workflow | `Signed amendment captured; budget impact updated in DS-CTMS-65` | Custom | Per FS-VEN-04. | FS-VEN-04 | OQ-VEN-04 |
| DS-CTMS-72 | eTMF Cross-Vault Link | `Vault Connect to Marinos eTMF (`marinos.veevavault.com`)` | Custom | Per FS-ETMF-01 + FS-INT-ETMF-01. | FS-ETMF-01, FS-INT-ETMF-01 | OQ-ETMF-01 |
| DS-CTMS-73 | EDL Gate at Site Activation | `EDL gaps block gated lifecycle transition` | Custom | Per FS-ETMF-02. | FS-ETMF-02 | OQ-ETMF-02 |
| DS-CTMS-74 | Document-Version Sync | `IB / Protocol / ICF version sync between CTMS + eTMF; mismatches → action items` | Custom | Per FS-ETMF-03. | FS-ETMF-03 | OQ-ETMF-03 |
| DS-CTMS-75 | Inspection-Readiness Score Surface | `From Vault eTMF → CTMS Vault Dashboard via Vault Connect` | Custom | Per FS-ETMF-04 + FS-INT-ETMF-02. | FS-ETMF-04, FS-INT-ETMF-02 | OQ-ETMF-04 |

### 4.11 Safety + Argus Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-76 | Argus Metadata Ingest | `Daily — case_id, subject_id, site_id, country, sponsor_awareness_date, regulatory_clock_state (read-only)` | Custom | Per FS-SAF-01 + FS-INT-ARGUS-01. | FS-SAF-01, FS-INT-ARGUS-01 | OQ-SAF-01 |
| DS-CTMS-77 | Clock-Display Policy | `Fatal/LT 7-day + 8-day follow-up; non-fatal/non-LT 15-day per ICH E2A + EU CTR Art. 42; CTMS displays state but does NOT own the clock` | Custom | Per FS-SAF-02 + FS-INT-ARGUS-02. | FS-SAF-02, FS-INT-ARGUS-02 | OQ-SAF-02 |
| DS-CTMS-78 | SAF Clock-Watch Alert Chain | `saf-clock-watch — T-2 / T-1 / T-0 / T+1 alerts to PV Lead + Director Clinical Ops; T+1 unresolved → quality event flagged for CAPA` | Custom | Per FS-SAF-03 + FS-BIMO-04. | FS-SAF-03, FS-BIMO-04 | OQ-SAF-03 |
| DS-CTMS-79 | Per-Site SAE / SUSAR Rate KPI | `Daily; published to RBM indicator set` | Custom | Per FS-SAF-04. | FS-SAF-04 | OQ-SAF-04 |
| DS-CTMS-80 | DSUR + ASR Task Tracking | `Vault Task object per study per year` | Custom | Per FS-SAF-05. | FS-SAF-05 | OQ-SAF-05 |

### 4.12 Audit-Trail + Part 11 Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-81 | Audit-Trail Schema | `actor_id, timestamp_utc, action, entity, old_value, new_value, reason` | Custom | Per FS-AUD-01. | FS-AUD-01 | OQ-AUDIT-01 |
| DS-CTMS-82 | Audit-Trail Export Format | `CSV + PDF; bundle digitally signed by sponsor PKI key` | Default | Per FS-AUD-02. | FS-AUD-02 | OQ-AUDIT-02 |
| DS-CTMS-83 | Audit-Trail Monthly Review | `Director Clinical Operations IT; evidence as signed Vault record` | Custom | Per FS-AUD-03. | FS-AUD-03 | OQ-AUDIT-03 |
| DS-CTMS-84 | Audit-Trail Retention | `≥ 25 y post-trial completion; per-study extension for paediatric / oncology / EU CTR Art. 58` | Custom | Per FS-AUD-04. | FS-AUD-04 | OQ-AUDIT-04 |
| DS-CTMS-85 | Audit-Trail Watchdog | `audit-trail-watchdog — heartbeat 5 min; gap > 15 min → tenant `READ_ONLY` + P1 alert` | Custom | Per FS-AUD-05. | FS-AUD-05 | OQ-AUDIT-05 |
| DS-CTMS-86 | § 11.10(a) SOP Suite | `SOP-CLINOPS-01..05 in Vellis eDMS; LMS gate` | Custom | Per FS-PART11-01. | FS-PART11-01 | OQ-PART11-10a |
| DS-CTMS-87 | § 11.10(b) Reproducible-Copy Job | `record-pdf-job — SHA-256 manifest` | Custom | Per FS-PART11-02. | FS-PART11-02 | OQ-PART11-10b |
| DS-CTMS-88 | § 11.10(c) Retention | `25 y minimum per DS-CTMS-84` | Custom | Per FS-PART11-03. | FS-PART11-03 | OQ-PART11-10c |
| DS-CTMS-89 | § 11.10(d) Access Control | `Okta + MFA + role-based per FS-SEC-01..02` | Custom | Per FS-PART11-04. | FS-PART11-04 | OQ-PART11-10d |
| DS-CTMS-90 | § 11.10(e) Audit Trail | `Per FS-AUD-01..05` | Custom | Per FS-PART11-05. | FS-PART11-05 | OQ-PART11-10e |
| DS-CTMS-91 | § 11.10(g) Authority Checks | `Server-side checks at signature / activation / payment / CTIS-submission; failed authority → audit + denial` | Custom | Per FS-PART11-06. | FS-PART11-06 | OQ-PART11-10g |
| DS-CTMS-92 | § 11.10(k) Manual Currency | `LMS rule gates current-version training` | Custom | Per FS-PART11-07. | FS-PART11-07 | OQ-PART11-10k |
| DS-CTMS-93 | § 11.30 Bridge Hardening | `CTIS + national-CA + Financials: TLS 1.3 + mutual auth + checksum reconciliation` | Custom | Per FS-PART11-08. | FS-PART11-08 | OQ-PART11-30 |
| DS-CTMS-94 | § 11.50 Signature Manifestation | `Printed name + UTC timestamp + meaning string` | Custom | Per FS-PART11-09. | FS-PART11-09 | OQ-PART11-50 |
| DS-CTMS-95 | § 11.70 Signature Record Binding | `Signature payload → record-state SHA-256 hash; post-signature change invalidates` | Custom | Per FS-PART11-10. | FS-PART11-10 | OQ-PART11-70 |
| DS-CTMS-96 | § 11.100 User-ID Uniqueness | `Okta uniqueness + Vault user-record constraint; never reassigned` | Custom | Per FS-PART11-11. | FS-PART11-11 | OQ-PART11-100 |
| DS-CTMS-97 | § 11.200 Re-Auth at Signature | `Max-age 5 min OAuth2 token; cached creds rejected` | Custom | Per FS-PART11-12. | FS-PART11-12 | OQ-PART11-200 |
| DS-CTMS-98 | § 11.300 Password Policy | `≥ 14 chars / history 12 / age 90 d / MFA / lockout 5/15min` | Custom | Per FS-PART11-13. | FS-PART11-13 | OQ-PART11-300 |

### 4.13 EDC + RTSM Integration Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-99 | Vault Connect to Rave | `Daily enrolment / status feed; subject-level state aggregated` | Custom | Per FS-INT-EDC-01. | FS-INT-EDC-01 | OQ-EDC-01 |
| DS-CTMS-100 | Vault 24R3 Clinical Ops–EDC Connection | `Protocol-deviation records from Rave with `edc_id` link → CTMS Deviation register` | Custom | Per FS-INT-EDC-02 + FS-DEV-03. | FS-INT-EDC-02, FS-DEV-03 | OQ-EDC-02 |
| DS-CTMS-101 | Query KPI Ingest | `From Rave daily — open count, aging, % overdue → site-level KPIs` | Custom | Per FS-INT-EDC-03. | FS-INT-EDC-03 | OQ-EDC-03 |
| DS-CTMS-102 | RTSM Reconciliation Feed | `Daily randomisation-status from RTSM; EDC enrolment vs RTSM mismatch → queries` | Custom | Per FS-INT-RTSM-01. | FS-INT-RTSM-01 | OQ-RTSM-01 |
| DS-CTMS-103 | Drug-Accountability Feed | `RTSM → FS-DRG-* drug-supply tracking` | Custom | Per FS-INT-RTSM-02. | FS-INT-RTSM-02 | OQ-RTSM-02 |

### 4.14 DSMB + Deviation Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-104 | Vault DSMB Object | `charter_version + meeting_schedule + recommendation_receipts; `dsmb-charter-drift-job` detects drift` | Custom | Per FS-DSMB-01. | FS-DSMB-01 | OQ-DSMB-01 |
| DS-CTMS-105 | DSMB Meeting Output | `{continue, modify, stop} signed Vault record; downstream Action Items linked to Protocol Amendment workflow` | Custom | Per FS-DSMB-02. | FS-DSMB-02 | OQ-DSMB-02 |
| DS-CTMS-106 | Interim-Analysis Schedule | `Per DSMB charter; missed milestone → alert` | Custom | Per FS-DSMB-03. | FS-DSMB-03 | OQ-DSMB-03 |
| DS-CTMS-107 | Vault Deviation Object | `deviation_id, subject_id, site_id, category, date_occurred, date_identified, description, root_cause, corrective_action, importance ∈ {IMPORTANT, NON_IMPORTANT}, ctis_reportable flag` | Custom | Per FS-DEV-01. | FS-DEV-01 | OQ-DEV-01 |
| DS-CTMS-108 | IPD Routing + CTIS Flag | `IPDs → Medical Monitor + CRA Lead review queue; CTIS-reportable flag → next CTIS SM or ASR` | Custom | Per FS-DEV-02. | FS-DEV-02, FS-CTIS-02 | OQ-DEV-02 |
| DS-CTMS-109 | Per-Site Deviation Rate KPI | `Per-site + per-study deviation rate + IPD rate → RBM indicator set` | Custom | Per FS-DEV-04. | FS-DEV-04 | OQ-DEV-03 |

### 4.15 BIMO + Inspection-Readiness Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-110 | BIMO Bundle Job | `bimo-bundle-job — site-activation evidence + investigator+delegation + MVR history + deviation register + SAE tracking + vendor records + CTIS submission history + budget vs actuals; PDF + CSV; SHA-256 signed` | Custom | Per FS-BIMO-01. | FS-BIMO-01 | OQ-BIMO-01 |
| DS-CTMS-111 | Inspector Okta Group | `dryad-vault-auditor-{study}` (read-only + export-only; no edit / no signature / no payment-submission) | Custom | Per FS-BIMO-02. | FS-BIMO-02 | OQ-BIMO-02 |
| DS-CTMS-112 | BIMO Bundle Performance Target | `≤ 60 min wall-clock for 100-site multi-country study` | Custom | Per FS-BIMO-03. | FS-BIMO-03 | PQ-BIMO-01 |
| DS-CTMS-113 | Late Safety-Reporting Pre-Emption | `FS-SAF-03 alert chain (DS-CTMS-78) pre-empts FY2024 BIMO finding pattern` | Custom | Per FS-BIMO-04. | FS-BIMO-04 | OQ-BIMO-03 |

### 4.16 Document Tracking + Closeout Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-114 | IB Version Registry | `ib_version + effective_date + irb_ec_approval[] + distribution_log[]` | Custom | Per FS-DOC-01. | FS-DOC-01 | OQ-DOC-01 |
| DS-CTMS-115 | Protocol Version Registry | `protocol_version + effective_date + ctis_submission_status` | Custom | Per FS-DOC-02. | FS-DOC-02 | OQ-DOC-02 |
| DS-CTMS-116 | ICF Version Registry | `icf_version + language + irb_ec_approval_date + deployment_to_site_date + current_icf flag` | Custom | Per FS-DOC-03. | FS-DOC-03 | OQ-DOC-03 |
| DS-CTMS-117 | Outdated-ICF Flag | `Subjects under outdated ICF version flagged via Vault Report; cross-reference to Marigold URS-CONSENT-*` | Custom | Per FS-DOC-04. | FS-DOC-04 | OQ-DOC-04 |
| DS-CTMS-118 | Site Closeout Gate | `COV MVR signed + queries closed + SDV complete + drug-supply reconciled + site-payment final + EDL gate` | Custom | Per FS-CLO-01. | FS-CLO-01 | OQ-CLO-01 |
| DS-CTMS-119 | CSR Tracking Object | `csr_version + statistical_analysis_status + signature_schedule + ctis_distribution` | Custom | Per FS-CLO-02. | FS-CLO-02 | OQ-CLO-02 |
| DS-CTMS-120 | End-of-Trial CTIS Notification | `Per EU CTR Art. 37 — tracked as workflow item` | Custom | Per FS-CLO-03. | FS-CLO-03 | OQ-CLO-03 |

### 4.17 CTIS + National-CA Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-121 | CTIS Submission Lifecycle | `initial → SUBMITTED → CA_DECISION → PUBLISHED; substantial_modifications[], asr[], end_of_trial, summary_of_results` | Custom | Per FS-CTIS-01. | FS-CTIS-01 | OQ-CTIS-01 |
| DS-CTMS-122 | Sponsor-Obligation Alerts | `ASR annual; SM per MS assessment cadence; EoT per EU CTR Art. 37; SoR per Art. 37 timelines` | Custom | Per FS-CTIS-02. | FS-CTIS-02 | OQ-CTIS-02 |
| DS-CTMS-123 | National-CA Gateway Tracking | `DE → BfArM + PEI, AT → AGES, CH → Swissmedic` | Custom | Per FS-CTIS-03 + FS-INT-*. | FS-CTIS-03 | OQ-CTIS-03 |
| DS-CTMS-124 | CTIS Resubmission Flag | `From 1 Jan 2026 no invoice for CTR safety/ethics technical resubmissions where content unchanged — captured for evidence` | Custom | Per FS-CTIS-04. | FS-CTIS-04 | OQ-CTIS-04 |

### 4.18 Monitoring Plan + IMP + Startup KPI Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-125 | Vault Monitoring Plan Object | `mp_version, effective_date, approver, amendment_linkage; version-history retained` | Custom | Per FS-MP-01. | FS-MP-01 | OQ-MP-01 |
| DS-CTMS-126 | MP Resolution Logic | `Active MP version drives FS-MV-01 cadence + FS-SDV-01 strategy at MV-creation / SDV-plan-bind time` | Custom | Per FS-MP-02. | FS-MP-02 | OQ-MP-02 |
| DS-CTMS-127 | IMP Licence Registry | `Per-country licence + customs-documentation; expiry alerts T-90 / T-60 / T-30 d` | Custom | Per FS-IMP-01. | FS-IMP-01 | OQ-IMP-01 |
| DS-CTMS-128 | Country Labelling / Leaflet Registry | `DE / AT / CH language-variant register` | Custom | Per FS-IMP-02. | FS-IMP-02 | OQ-IMP-02 |
| DS-CTMS-129 | Study Startup KPI Computation | `Time-to-CA-Submission, Time-to-First-Approval, Time-to-First-Site-Activation, Time-to-FPI per study + per country; `startup-kpi-job`` | Custom | Per FS-SS-01. | FS-SS-01 | OQ-SS-01 |
| DS-CTMS-130 | FPI Event Tracking | `FPI date + site + subject screening/randomisation indicator; CTIS notification trigger via FS-CTIS-01` | Custom | Per FS-SS-02. | FS-SS-02 | OQ-SS-02 |

### 4.19 Sponsor Audit Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-131 | Vault Audit Object | `audit_id, scope, auditor_id, date, findings[], capas[] linked to MasterControl via DS-CTMS-53` | Custom | Per FS-AUDIT-01. | FS-AUDIT-01 | OQ-SAUDIT-01 |
| DS-CTMS-132 | Audit-Severity Escalation | `CRITICAL → immediate Action Item routed to study-level QA` | Custom | Per FS-AUDIT-02. | FS-AUDIT-02 | OQ-SAUDIT-02 |

### 4.20 GDPR + Security Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-133 | Per-Study + Per-Country Scopes | `Vault role-permission matrix; FPI / 90-d / closeout access review` | Custom | Per FS-SEC-02. | FS-SEC-02 | OQ-SEC-01 |
| DS-CTMS-134 | Investigator Contact Encryption | `AES-256 at rest + TLS 1.3 in transit per GDPR Art. 32` | Custom | Per FS-SEC-03. | FS-SEC-03 | OQ-SEC-02 |
| DS-CTMS-135 | GDPR Art. 22 Algorithmic-Decision Block | `Algorithmic outputs advisory only; per-decision audit-trail entry` | Custom | Per FS-SEC-04. | FS-SEC-04 | OQ-PRIV-01 |
| DS-CTMS-136 | Per-Study DPIA Template | `Confluence + signed PDF in eTMF — required before FPI` | Custom | Per FS-SEC-05. | FS-SEC-05 | OQ-PRIV-02 |
| DS-CTMS-137 | GDPR Art. 17 Triage | `Against EU CTR + ICH E6(R3) retention obligations; decision in eTMF` | Custom | Per FS-SEC-06. | FS-SEC-06 | OQ-PRIV-03 |

### 4.21 Training + Periodic Review Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-138 | LMS Gate | `Production access blocked unless role + protocol training current; T-30 warning; auto-block T+0` | Custom | Per FS-TRN-01. | FS-TRN-01 | OQ-TRN-01 |
| DS-CTMS-139 | Annual Periodic Review | `SOP-CLINOPS-05 — Director Clinical Ops IT + Head of QA signatures` | Custom | Per FS-PR-01. | FS-PR-01 | OQ-PR-01 |
| DS-CTMS-140 | Periodic-Review Scope | `Audit-trail completeness + vendor-release impact-assessment + integration health + SAE clock-tracking` | Custom | Per FS-PR-02. | FS-PR-02 | OQ-PR-02 |

### 4.22 Localisation + Performance + Backup Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-141 | Supported Locales | `de-DE, de-AT, de-CH, fr-FR, en-GB, en-US, es-ES, it-IT, pl-PL, cs-CZ` | Custom | Per FS-INTL-01. | FS-INTL-01 | OQ-INTL-01 |
| DS-CTMS-142 | TZ-Aware Window Calculations | `Visit-window + payment-due TZ-aware; storage UTC` | Custom | Per FS-INTL-02. | FS-INTL-02 | OQ-INTL-02 |
| DS-CTMS-143 | UI Locale Formatter | `Locale-specific date / number / currency display; canonical values unchanged` | Custom | Per FS-INTL-03. | FS-INTL-03 | OQ-INTL-03 |
| DS-CTMS-144 | P95 Object-Open Target | `≤ 3 s at 300 concurrent users` | Custom | Per FS-PERF-01. | FS-PERF-01 | PQ-PERF-01 |
| DS-CTMS-145 | Site-List Export Target | `≤ 10 min wall-clock for 100-site study` | Custom | Per FS-PERF-02. | FS-PERF-02 | PQ-PERF-02 |
| DS-CTMS-146 | Backup Tier + Immutability | `T1 / RPO ≤ 4 h / RTO ≤ 4 BH; S3 Object Lock Compliance + LTO-9 air-gap` | Custom | Per FS-XSYS-BAK-01 + FS-BAK-01 + FS-BAK-02. | FS-XSYS-BAK-01, FS-BAK-01 | OQ-BAK-01 |
| DS-CTMS-147 | Veeva SLA Tracking | `99.5% monthly via Veeva Trust portal; deviations escalated` | Default | Per FS-AV-01. | FS-AV-01 | OQ-AV-01 |

### 4.23 Vendor + Vendor-Assurance Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-148 | Vendor-Quality Register | `vendor-quality-register in eQMS — SOC 2 Type II + ISO 27001:2022 + GDPR DPA + sub-processor list + customer-shared CSV summary` | Custom | Per FS-VND-01. | FS-VND-01 | IQ-VND-01 |
| DS-CTMS-149 | Veeva Release-Evaluation | `RNS feed → impact-assessment within 14 days; impacted studies routed to re-validation` | Custom | Per FS-VND-02. | FS-VND-02 | OQ-VND-01 |
| DS-CTMS-150 | Vendor Sub-Processor Inventory | `Annual DPO review per DPA Annex` | Custom | Per FS-VND-03. | FS-VND-03 | OQ-VND-02 |
| DS-CTMS-151 | Vendor-Incident Notification | `vendor-incident-log; confirmed-breach → DPO within 24 h per GDPR Art. 33` | Custom | Per FS-VND-04. | FS-VND-04 | OQ-VND-03 |

### 4.24 Cross-System Plane Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CTMS-152 | Helios Audit-Event Bus | `Kafka topic `helios.ingest.dryad.ctms.v1`; envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`; at-least-once; idempotency key `{source_system, event_id}`; Prometheus `helios_publish_lag_seconds` > 600 s alert` | Custom | Per FS-XINT-HEL-01. | FS-XINT-HEL-01 | OQ-HEL-01 |
| DS-CTMS-153 | Helios Reconciliation Job | `Daily parity check; MasterControl deviation on > 0.01% mismatch over 24 h` | Custom | Per FS-XINT-HEL-02. | FS-XINT-HEL-02 | OQ-HEL-02 |
| DS-CTMS-154 | LMS Competence Adapter | `GET /lms/competence/{user_id}?curriculum=...` over mTLS + Entra workload-identity; cache TTL 12-24 h; on `current=false` block gated action + record `lms_lapse_user={user_id}` | Custom | Per FS-XINT-LMS-01. | FS-XINT-LMS-01 | OQ-LMS-01 |

---

## 5. Workflow + Business-Rule Design

### 5.1 Site Activation Workflow

```
   [IDENTIFIED] Site identified from feasibility outreach
        │
        ▼ Vault Site lifecycle transition (e-sign, FS-SITE-04)
   [QUALIFIED] Site qualified — feasibility survey complete
        │
        ▼ Activation Plan checklist:
   ┌────────────────────────────────────────────────────────────┐
   │  1572 / EU investigator file        │ FS-SITE-02 (DS-CTMS-24)│
   │  CV                                 │                       │
   │  Financial-disclosure (Form 3454/55)│                       │
   │  IRB / EC approval (current)        │                       │
   │  Current ICF (per language)         │                       │
   │  Site-staff training (LMS)          │                       │
   │  Signed CTA                         │                       │
   │  Insurance certificate              │                       │
   │  SIV report                         │                       │
   └────────────────────────────────────────────────────────────┘
        │
        ▼ Country CA decision verified (DS-CTMS-22) + EDL gate verified (DS-CTMS-73)
   [INITIATED] CRA Lead signature applied (DS-CTMS-25)
        │
        ▼ FPI captured (DS-CTMS-130) → CTIS notification trigger
   [ENROLLING] Subject enrolment in progress
        │
        ▼ Per-study LPI event
   [ENROLLMENT_CLOSED]
        │
        ▼ Follow-up complete
   [FOLLOW_UP]
        │
        ▼ Site Closeout gate (DS-CTMS-118)
   [CLOSED]
```

### 5.2 Monitoring-Visit Lifecycle Workflow

| Step | Action | Actor | Audit-trail event | Verified by |
|---|---|---|---|---|
| 1 | MV planned (per RBM-driven cadence) | System (`mv-plan-job`) | `MV_PLANNED` | OQ-MV-07 |
| 2 | MV scheduled with site | CRA | `MV_SCHEDULED` | OQ-MV-08 |
| 3 | MV conducted (on-site or remote per DS-CTMS-38) | CRA | `MV_CONDUCTED` | OQ-MV-09 |
| 4 | MVR drafted in Vault | CRA | `MVR_DRAFTED` | OQ-MV-10 |
| 5 | MVR reviewed by CRA Lead | CRA Lead | `MVR_REVIEWED` | OQ-MV-11 |
| 6 | MVR signed (e-signature + re-auth per § 11.200) | CRA Lead | `MVR_SIGNED` | OQ-MV-03 |
| 7 | Action items created + assigned with escalation (DS-CTMS-41) | System | `AI_CREATED` | OQ-MV-04 |
| 8 | Action items closed with evidence | Owner | `AI_CLOSED` | OQ-MV-12 |

### 5.3 Protocol-Amendment Workflow

```
   [Amendment drafted in Vault]
         │
         ▼ Impact-Assessment template
   [impact_category ∈ {ADMINISTRATIVE, SUBSTANTIAL}]
         │
         ├─ ADMINISTRATIVE → propagation only
         │
         └─ SUBSTANTIAL
             │
             ▼ ctis-sm-submission workflow (DS-CTMS-19)
             [DRAFT → SUBMITTED → CA_DECISION → PUBLISHED]
             │
             ▼ Downstream-task generator (DS-CTMS-20)
             ┌────────────────────────────────────────────────────────────┐
             │  Re-consent tasks (Marigold URS-CONSENT-*)                  │
             │  EDC re-build (Marigold URS-BUILD)                          │
             │  Monitoring-plan update (FS-MV-* via DS-CTMS-125)           │
             └────────────────────────────────────────────────────────────┘
```

### 5.4 Payment-Push Workflow

| Step | Action | Endpoint | Idempotency-Key | Verified by |
|---|---|---|---|---|
| 1 | Milestone reached (e.g., site-init, per-subject enrol, per-visit, close-out) | Vault Milestone trigger | — | OQ-PAY-06 |
| 2 | Payment schedule auto-generated | Vault Payment object | — | OQ-PAY-01 |
| 3 | Overpayment guard pre-check | Internal | — | OQ-PAY-03 |
| 4 | POST `/v1/payments/initiate` | Financials | `{study_id}:{site_id}:{milestone_id}:{payment_id}` | OQ-PAY-02 |
| 5 | Financials ack received | Internal | — | OQ-PAY-07 |
| 6 | Monthly reconciliation | `payment-reconcile-job` | — | OQ-FIN-01 |

### 5.5 CTIS Submission Workflow

```
   [Substantial Modification | ASR due | EoT | SoR | Initial trial application]
         │
         ▼ Vault workflow ctis-extract
   [CTIS pack assembled per EMA CTIS schema]
         │
         ▼ National-CA carve-out routing (DS-CTMS-123)
   ┌────────────────────────────────────────────────────────────────┐
   │  DE national obligations → BfArM (medicinal) + PEI (biologicals)│
   │  AT national obligations → AGES                                 │
   │  CH national obligations → Swissmedic                           │
   └────────────────────────────────────────────────────────────────┘
         │
         ▼ Sponsor Reg Affairs upload to CTIS sponsor workspace
   [DRAFT → SUBMITTED → CA_DECISION → PUBLISHED]
         │
         ▼ Sponsor-obligation alerts (DS-CTMS-122)
```

### 5.6 SAE / SUSAR Clock-Display Workflow

| Step | Action | Source of truth | CTMS role | FS-ID |
|---|---|---|---|---|
| 1 | SAE confirmed in EDC (Marigold) | Marigold EDC | — | FS-INT-SAFETY-01 (Marigold) |
| 2 | SAE transmitted to Argus within 24 h | Marigold EDC | — | FS-INT-SAFETY-01 |
| 3 | Argus computes regulatory clock state | Argus | — | FS-INT-ARGUS-02 |
| 4 | CTMS ingests metadata (read-only) | Argus REST → CTMS | display | FS-SAF-01 |
| 5 | CTMS displays clock-state per DS-CTMS-77 | CTMS | display | FS-SAF-02 |
| 6 | T-2 / T-1 / T-0 / T+1 alerts to PV Lead + Director Clinical Ops | CTMS | alerting | FS-SAF-03 |
| 7 | T+1 unresolved → quality event flagged for CAPA via DS-CTMS-53 | CTMS → MasterControl | escalation | FS-ISS-03 |

### 5.7 DSMB Tracking Workflow

```
   [DSMB Charter approved → DS-CTMS-104]
         │
         ▼ Interim-analysis schedule tracked (DS-CTMS-106)
   [DSMB meeting scheduled]
         │
         ▼ DSMB meeting outputs captured (DS-CTMS-105):
   [Recommendation ∈ {continue, modify, stop}]
         │
         ├─ continue → no downstream action
         │
         ├─ modify  → Action Items linked to Protocol Amendment workflow (DS-CTMS-19)
         │
         └─ stop    → Study Stop workflow + Reg Affairs CTIS notification
```

---

## 6. Role-Permission Matrix Design

| Role | Protocol Edit | Country Edit | Site Edit | Investigator Edit | MVR Sign | Activation Sign | Payment Push | CAPA Open | DSMB Update | CTIS Submit | View All | Export BIMO | Vendor Release-Eval |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Reg Affairs Lead | ✓ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ |
| CRA | ✗ | ✗ | (limited) | (training/contact only) | (draft only) | ✗ | ✗ | (raise) | ✗ | ✗ | ✓ (scoped) | ✗ | ✗ |
| CRA Lead | ✗ | ✗ | ✓ (lifecycle) | ✓ (training) | ✓ | sign INITIATED | ✗ | ✓ | ✗ | ✗ | ✓ | ✗ | ✗ |
| Clinical Operations Manager | ✗ | ✓ | ✓ | ✓ | ✗ | (alternate path) | ✓ (approve) | ✓ | ✗ | ✗ | ✓ | ✗ | ✗ |
| Director Clinical Operations IT | ✓ | ✓ | ✓ | ✓ | (un-sign approval) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✗ | ✗ |
| VP Clinical Operations | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | (signs stop recommendation) | ✗ | ✓ | ✗ | ✗ |
| PV Lead | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | ✓ (SAE) | ✗ | ✗ |
| Medical Monitor | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | ✓ (deviations) | ✗ | ✗ |
| Supply Chain | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | ✓ (drug supply) | ✗ | ✗ |
| Financials Operator | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | ✗ | ✓ (payments) | ✗ | ✗ |
| DPO | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | ✓ (privacy events) | ✗ | ✗ |
| Inspector (BIMO / EU / DACH) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | export-only | ✗ |
| Vendor Assurance Owner | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (vendor reg) | ✗ | ✓ |
| Tenant Admin (Vault) | (config only) | (config only) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | (config) | ✗ | ✗ |

**Role-permission design rules:**
- **SoD enforcement** — Payment Push action requires Financials Operator + Clinical Operations Manager (or Director CO-IT) approval pair.
- **Inspector role** — `dryad-vault-auditor-{study}` Okta group; export-only; no edit / no signature / no payment-submission per FS-BIMO-02.
- **CTIS Submit** — restricted to Reg Affairs Lead + Director Clinical Operations IT.
- **Periodic access review** — FPI / 90-d / closeout cadence per DS-CTMS-133.

---

## 7. Integration Design

### 7.1 Okta SAML + SCIM (FS-INT-SSO-01..02)

| Item | Value |
|---|---|
| Protocol | SAML 2.0 + SCIM 2.0 |
| IdP-initiated Endpoint | `https://dryad.okta.com/app/dryad-vault/saml/sso` |
| SCIM Endpoint | `https://dryad.veevavault.com/scim/v2/` |
| Auth | TLS 1.3 + mutual cert |
| Termination Latency | ≤ 24 h |
| Conditional-Access Policy | Clinical-Sensitive (FIDO2 + sponsor-tenant isolation) |

### 7.2 Vault Connect to Marigold Rave + Marinos eTMF

| Item | Value | FS-ID |
|---|---|---|
| Rave Vault Connect endpoint | `https://marigold.mdsol.com/connect/v1/` | FS-INT-EDC-01 |
| Vault 24R3 Clinical Operations–EDC Connection | `https://marigold.mdsol.com/connect/v1/clinops-edc-deviation/` | FS-INT-EDC-02 |
| Marinos eTMF Vault Connect endpoint | `https://marinos.veevavault.com/connect/v1/` | FS-INT-ETMF-01 |
| eTMF lookup endpoint | `GET /v1/etmf/lookup?study_id=...&site_id=...` | FS-INT-ETMF-02 |
| Auth | OAuth2 client-credentials |

### 7.3 RTSM / IXRS (FS-INT-RTSM-01..02)

| Item | Value |
|---|---|
| Endpoint | `https://rtsm.mdsol.com/v1/` |
| Daily reconciliation | `rtsm-reconcile-job` at 04:00 UTC |
| Drug-Acct feed | Daily |
| Auth | OAuth2 |

### 7.4 Argus 8.4 (FS-INT-ARGUS-01..02)

| Item | Value |
|---|---|
| Endpoint | `https://argus.dryad-prod.local/v1/` |
| Mode | Read-only metadata ingest |
| Cadence | Daily |
| Auth | mTLS |

### 7.5 MasterControl eQMS (FS-INT-EQMS-01..02)

| Item | Value |
|---|---|
| Create CAPA Endpoint | `POST /v1/capa/create` |
| Idempotency-Key | `{study_id}:{deviation_id}` |
| Status Endpoint | `GET /v1/capa/status` (hourly poll) |
| Auth | OAuth2 client-credentials |

### 7.6 Financials (FS-INT-FIN-01..02)

| Item | Value |
|---|---|
| Initiate Endpoint | `POST /v1/payments/initiate` |
| Idempotency-Key | `{study_id}:{site_id}:{milestone_id}:{payment_id}` |
| Monthly Reconciliation Job | `payment-reconcile-job` |
| Auth | OAuth2 client-credentials |

### 7.7 HR (FS-INT-HR-01)

| Item | Value |
|---|---|
| Provisioning Protocol | SCIM 2.0 via Okta |
| Termination Latency | ≤ 24 h |
| Auth | mutual cert (Okta ↔ Vault) |

### 7.8 CTIS + National-CA Gateways (FS-CTIS-03)

| Counterparty | Endpoint | Protocol | Trigger |
|---|---|---|---|
| CTIS sponsor workspace | EMA CTIS portal (sponsor-mediated) | sponsor upload | Per CTIS submission lifecycle |
| BfArM (DE — medicinal) | `https://bfarm-gw.dryad-prod.local/v1/` | mTLS | DE substantial modification |
| PEI (DE — biologicals) | `https://pei-gw.dryad-prod.local/v1/` | mTLS | DE biologics submission |
| AGES (AT) | `https://ages-gw.dryad-prod.local/v1/` | mTLS | AT national notification |
| Swissmedic (CH) | `https://sm-gw.dryad-prod.local/v1/` | mTLS | CH national notification |

### 7.9 Cross-System Active Directory + Backup + Helios + LMS

| Plane | Counterparty | Endpoint | FS-ID |
|---|---|---|---|
| AD | Entra ID | SAML 2.0 + SCIM | FS-XSYS-AD-01 |
| Backup | AUR Veeam | Veeam infrastructure + Oracle RMAN + S3 Object Lock + LTO-9 | FS-XSYS-BAK-01 |
| Helios | Kafka helios.ingest.dryad.ctms.v1 | mTLS + SASL/SCRAM | FS-XINT-HEL-01..02 |
| LMS | Cornerstone (or Vega LMS counterparty) | mTLS + Entra workload-identity | FS-XINT-LMS-01 |

---

## 8. Site-Deployed Components Design

| Component | Type | Source location | Owner team | Verified by |
|---|---|---|---|---|
| `enrol-forecast-job` | Scheduled (daily) | `git.dryad-prod.local/clinops/enrol-forecast-job` | Clinical Ops Engineering | OQ-REC-03 |
| `rbm-indicator-job` | Scheduled (daily) | `git.dryad-prod.local/clinops/rbm-indicator-job` | Clinical Ops Engineering | OQ-RBM-02 |
| `mvr-due-date-watch` | Daemon | `git.dryad-prod.local/clinops/mvr-due-date-watch` | Clinical Ops SRE | OQ-MV-05 |
| `drug-supply-ingest` | Scheduled (daily) | `git.dryad-prod.local/clinops/drug-supply-ingest` | Supply Chain Engineering | OQ-DRG-01 |
| `drug-forecast-job` | Scheduled | `git.dryad-prod.local/clinops/drug-forecast-job` | Supply Chain Engineering | OQ-DRG-02 |
| `payment-reconcile-job` | Scheduled (monthly) | `git.dryad-prod.local/clinops/payment-reconcile-job` | Financials Engineering | OQ-FIN-01 |
| `dsmb-charter-drift-job` | Scheduled | `git.dryad-prod.local/clinops/dsmb-charter-drift-job` | Clinical Ops Engineering | OQ-DSMB-01 |
| `inv-training-check-job` | Event-driven | `git.dryad-prod.local/clinops/inv-training-check-job` | Clinical Ops Engineering | OQ-INV-04 |
| `audit-trail-watchdog` | Daemon | `git.dryad-prod.local/clinops/audit-trail-watchdog` | Clinical Ops SRE | OQ-AUDIT-05 |
| `startup-kpi-job` | Scheduled (weekly) | `git.dryad-prod.local/clinops/startup-kpi-job` | Clinical Ops Engineering | OQ-SS-01 |
| `risk-review-reminder` | Scheduled | `git.dryad-prod.local/clinops/risk-review-reminder` | Clinical Ops Engineering | OQ-RBM-05 |
| `bimo-bundle-job` | On-demand | `git.dryad-prod.local/clinops/bimo-bundle-job` | Clinical Ops Engineering | OQ-BIMO-01 |
| `record-pdf-job` | On-demand | `git.dryad-prod.local/clinops/record-pdf-job` | Clinical Ops Engineering | OQ-PART11-10b |
| `saf-clock-watch` | Daemon | `git.dryad-prod.local/clinops/saf-clock-watch` | PV Engineering | OQ-SAF-03 |
| `budget-actuals-job` | Scheduled (monthly) | `git.dryad-prod.local/clinops/budget-actuals-job` | Financials Engineering | OQ-BUD-01 |

Each site-deployed component is governed under eQMS change control + Git-versioned per Vellis-managed SOPs. Each component repository carries a `docs/SDS.md` mini-Software-Design-Specification artefact per GAMP 5 2nd-edition § 2B.4 rule 6 (hybrid Cat 4 + Cat 5 escalation for embedded custom code).

---

## 9. References

### 9.1 US

- 21 CFR Part 11 §§ .10(a)–(k), .30, .50, .70, .100, .200, .300.
- 21 CFR Part 312 (Form FDA 1572 per § 312.53(c)); 21 CFR Part 314; 21 CFR Parts 50 + 56.
- FDA *Computerized Systems Used in Clinical Investigations* (May 2007).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).
- FDA *Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions* (Aug 2025).
- FDA *Establishment and Operation of Clinical Trial Data Monitoring Committees* (current + 2024 draft).
- FDA BIMO Inspection Manual 7348.809 (updated 4 April 2025).
- FDA *Conducting Remote Regulatory Assessments — Q&A* (June 2025 final).

### 9.2 EU

- EU CTR Reg. 536/2014 + CTIS Sponsor Handbook (current).
- EU CTR Arts. 16, 37, 42, 58.
- EU GMP Annex 11 §§ 4, 6, 9, 11; EMA Q&A on Annex 11.
- GDPR Reg. (EU) 2016/679 — Arts. 6, 17, 22, 32, 33, 35.

### 9.3 DACH

- BfArM (DE) — medicinal-product national notifications.
- Paul-Ehrlich-Institut (PEI) — DE biologicals.
- AGES PharmMed (AT).
- Swissmedic (CH).

### 9.4 International

- ICH E6(R3) GCP (Step 4, adopted 6 January 2025).
- ICH E8(R1); ICH E9(R1); ICH E2A; ICH E2B(R3); ICH M11.
- ISPE GAMP 5 (2nd Edition, 2022).
- PIC/S PI 041.
- ISO/IEC 27001:2022.
- ISO 14155:2020 (device arms).
- TMF Reference Model v3.3.x.

### 9.5 Vendor

- Veeva Systems — *Vault CTMS 24R3 / 25R1 Release Notes*.
- Veeva Systems — *Vault CTMS Configuration Reference*.
- Veeva Systems — *Vault 24R3 Clinical Operations–EDC Connection Documentation*.
- Medidata Rave EDC (Marigold MAR-URS-EDC-001 / MAR-FS-EDC-001 cross-reference).
- Oracle Argus 8.4 (Sirius PV cross-reference).

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS ID | FS ID(s) | Notes |
|---|---|---|
| DS-CTMS-01 | FS-INT-SSO-01 / FS-PART11-04 | Vault IdP mode |
| DS-CTMS-02 | FS-INT-SSO-01 / FS-PART11-11 | Local-account disablement |
| DS-CTMS-03 | FS-INT-SSO-02 | SCIM endpoint |
| DS-CTMS-04 | FS-INT-HR-01 / FS-INT-SSO-02 | SCIM deprovisioning latency |
| DS-CTMS-05 | FS-INT-SSO-02 / FS-SEC-02 | Okta group naming |
| DS-CTMS-06 | FS-XSYS-AD-01 | Conditional-access policy |
| DS-CTMS-07 | FS-XSYS-AD-01 / FS-AUD-01 | SIEM forwarding |
| DS-CTMS-08 | FS-XSYS-AD-01 | PAM break-glass |
| DS-CTMS-09 | FS-SEC-01 | Session timeout |
| DS-CTMS-10 | FS-PART11-12 | Force-reauth on signature |
| DS-CTMS-11 | FS-PART11-04 / FS-PART11-13 | MFA methods |
| DS-CTMS-12 | FS-PART11-13 | Password min length |
| DS-CTMS-13 | FS-PART11-13 | Password history |
| DS-CTMS-14 | FS-PART11-13 | Password max age |
| DS-CTMS-15 | FS-PART11-13 | Lockout threshold |
| DS-CTMS-16 | FS-PART11-11 | User-id uniqueness |
| DS-CTMS-17 | FS-PROT-01 | Vault Protocol object |
| DS-CTMS-18 | FS-PROT-02 | Vault Amendment object |
| DS-CTMS-19 | FS-PROT-03 / FS-CTIS-01 | Substantial-modification workflow |
| DS-CTMS-20 | FS-PROT-04 | Amendment downstream-task generator |
| DS-CTMS-21 | FS-CTRY-01 | Vault Country object |
| DS-CTMS-22 | FS-CTRY-02 | Country-milestone gating |
| DS-CTMS-23 | FS-SITE-01 / FS-SEC-03 | Vault Site object |
| DS-CTMS-24 | FS-SITE-02 | Activation checklist |
| DS-CTMS-25 | FS-SITE-03 | Activation gate |
| DS-CTMS-26 | FS-SITE-01 / FS-SITE-04 | Site lifecycle state machine |
| DS-CTMS-27 | FS-SITE-05 / FS-SEC-03 | Site Contacts encryption |
| DS-CTMS-28 | FS-SITE-06 / FS-REC-02 | Enrolment plan report |
| DS-CTMS-29 | FS-INV-01 | Vault Investigator object |
| DS-CTMS-30 | FS-INV-02 | 1572 sub-object |
| DS-CTMS-31 | FS-INV-03 | Delegation Log |
| DS-CTMS-32 | FS-INV-04 | Training-check job |
| DS-CTMS-33 | FS-INV-05 | PI-transition workflow |
| DS-CTMS-34 | FS-REC-01 | Enrolment plan capture |
| DS-CTMS-35 | FS-REC-02 | Enrolment forecast job |
| DS-CTMS-36 | FS-REC-03 | Recruitment KPI set |
| DS-CTMS-37 | FS-REC-04 / FS-ISS-02 | Recruitment exceptions |
| DS-CTMS-38 | FS-MV-01 | MV type vocab |
| DS-CTMS-39 | FS-MV-02 | MVR object schema |
| DS-CTMS-40 | FS-MV-03 | MVR signature workflow |
| DS-CTMS-41 | FS-MV-04 | MVR escalation |
| DS-CTMS-42 | FS-MV-05 / FS-RBM-02 | MV due-date watch |
| DS-CTMS-43 | FS-MV-06 | MVR template versioning |
| DS-CTMS-44 | FS-SDV-01 | SDV plan |
| DS-CTMS-45 | FS-SDV-02 | SDV completion ingest |
| DS-CTMS-46 | FS-SDV-03 | SDV exception job |
| DS-CTMS-47 | FS-RBM-01 | Risk Register object |
| DS-CTMS-48 | FS-RBM-02 | RBM indicator job |
| DS-CTMS-49 | FS-RBM-03 / FS-ISS-02 | RBM threshold routing |
| DS-CTMS-50 | FS-RBM-04 | RBM dashboard navigation |
| DS-CTMS-51 | FS-RBM-05 | Risk-register review cadence |
| DS-CTMS-52 | FS-ISS-01 | Issue object |
| DS-CTMS-53 | FS-ISS-03 / FS-INT-EQMS-01 | MasterControl CAPA REST |
| DS-CTMS-54 | FS-INT-EQMS-02 | CAPA status feedback |
| DS-CTMS-55 | FS-ISS-04 | Issue / AI KPIs |
| DS-CTMS-56 | FS-DRG-01 | RTSM ingest job |
| DS-CTMS-57 | FS-DRG-02 | Drug forecast horizon |
| DS-CTMS-58 | FS-DRG-03 | Drug shortfall alert |
| DS-CTMS-59 | FS-DRG-04 | Drug-acct reconciliation |
| DS-CTMS-60 | FS-PAY-01 | Vault Payment sub-object |
| DS-CTMS-61 | FS-PAY-02 / FS-INT-FIN-01 | Financials REST idempotency |
| DS-CTMS-62 | FS-PAY-03 | Overpayment guard |
| DS-CTMS-63 | FS-PAY-04 | Payment forecast |
| DS-CTMS-64 | FS-PAY-05 | Payment history export |
| DS-CTMS-65 | FS-BUD-01 | Vault Budget object |
| DS-CTMS-66 | FS-BUD-02 | Cost-overrun alert |
| DS-CTMS-67 | FS-INT-FIN-02 | Financials monthly reconciliation |
| DS-CTMS-68 | FS-VEN-01 | Vault Vendor object |
| DS-CTMS-69 | FS-VEN-02 | Vendor feed reconciliation |
| DS-CTMS-70 | FS-VEN-03 | Vendor KPI report |
| DS-CTMS-71 | FS-VEN-04 | Vendor change-order |
| DS-CTMS-72 | FS-ETMF-01 / FS-INT-ETMF-01 | eTMF cross-vault link |
| DS-CTMS-73 | FS-ETMF-02 | EDL gate at activation |
| DS-CTMS-74 | FS-ETMF-03 | Document-version sync |
| DS-CTMS-75 | FS-ETMF-04 / FS-INT-ETMF-02 | Inspection-readiness surface |
| DS-CTMS-76 | FS-SAF-01 / FS-INT-ARGUS-01 | Argus metadata ingest |
| DS-CTMS-77 | FS-SAF-02 / FS-INT-ARGUS-02 | Clock-display policy |
| DS-CTMS-78 | FS-SAF-03 / FS-BIMO-04 | SAF clock-watch alerts |
| DS-CTMS-79 | FS-SAF-04 | Per-site SAE rate KPI |
| DS-CTMS-80 | FS-SAF-05 | DSUR + ASR tasks |
| DS-CTMS-81 | FS-AUD-01 | Audit-trail schema |
| DS-CTMS-82 | FS-AUD-02 | Audit-trail export format |
| DS-CTMS-83 | FS-AUD-03 | Monthly audit-trail review |
| DS-CTMS-84 | FS-AUD-04 | Audit-trail retention |
| DS-CTMS-85 | FS-AUD-05 | Audit-trail watchdog |
| DS-CTMS-86 | FS-PART11-01 | § 11.10(a) SOP suite |
| DS-CTMS-87 | FS-PART11-02 | § 11.10(b) reproducible-copy job |
| DS-CTMS-88 | FS-PART11-03 | § 11.10(c) retention |
| DS-CTMS-89 | FS-PART11-04 | § 11.10(d) access control |
| DS-CTMS-90 | FS-PART11-05 | § 11.10(e) audit trail |
| DS-CTMS-91 | FS-PART11-06 | § 11.10(g) authority checks |
| DS-CTMS-92 | FS-PART11-07 | § 11.10(k) manual currency |
| DS-CTMS-93 | FS-PART11-08 | § 11.30 bridge hardening |
| DS-CTMS-94 | FS-PART11-09 | § 11.50 manifestation |
| DS-CTMS-95 | FS-PART11-10 | § 11.70 binding |
| DS-CTMS-96 | FS-PART11-11 | § 11.100 uniqueness |
| DS-CTMS-97 | FS-PART11-12 | § 11.200 re-auth |
| DS-CTMS-98 | FS-PART11-13 | § 11.300 password policy |
| DS-CTMS-99 | FS-INT-EDC-01 | Vault Connect to Rave |
| DS-CTMS-100 | FS-INT-EDC-02 / FS-DEV-03 | Vault 24R3 EDC-CTMS Connection |
| DS-CTMS-101 | FS-INT-EDC-03 | Query KPI ingest |
| DS-CTMS-102 | FS-INT-RTSM-01 | RTSM reconciliation feed |
| DS-CTMS-103 | FS-INT-RTSM-02 | Drug-acct feed |
| DS-CTMS-104 | FS-DSMB-01 | DSMB charter object |
| DS-CTMS-105 | FS-DSMB-02 | DSMB meeting output |
| DS-CTMS-106 | FS-DSMB-03 | Interim-analysis schedule |
| DS-CTMS-107 | FS-DEV-01 | Deviation object |
| DS-CTMS-108 | FS-DEV-02 / FS-CTIS-02 | IPD routing + CTIS flag |
| DS-CTMS-109 | FS-DEV-04 | Per-site deviation rate KPI |
| DS-CTMS-110 | FS-BIMO-01 | BIMO bundle job |
| DS-CTMS-111 | FS-BIMO-02 | Inspector Okta group |
| DS-CTMS-112 | FS-BIMO-03 | BIMO bundle perf target |
| DS-CTMS-113 | FS-BIMO-04 | Late safety-reporting pre-emption |
| DS-CTMS-114 | FS-DOC-01 | IB version registry |
| DS-CTMS-115 | FS-DOC-02 | Protocol version registry |
| DS-CTMS-116 | FS-DOC-03 | ICF version registry |
| DS-CTMS-117 | FS-DOC-04 | Outdated-ICF flag |
| DS-CTMS-118 | FS-CLO-01 | Site closeout gate |
| DS-CTMS-119 | FS-CLO-02 | CSR tracking object |
| DS-CTMS-120 | FS-CLO-03 | EoT CTIS notification |
| DS-CTMS-121 | FS-CTIS-01 | CTIS submission lifecycle |
| DS-CTMS-122 | FS-CTIS-02 | Sponsor-obligation alerts |
| DS-CTMS-123 | FS-CTIS-03 | National-CA tracking |
| DS-CTMS-124 | FS-CTIS-04 | CTIS resubmission flag |
| DS-CTMS-125 | FS-MP-01 | Vault Monitoring Plan object |
| DS-CTMS-126 | FS-MP-02 | MP resolution logic |
| DS-CTMS-127 | FS-IMP-01 | IMP licence registry |
| DS-CTMS-128 | FS-IMP-02 | Country labelling registry |
| DS-CTMS-129 | FS-SS-01 | Startup KPI computation |
| DS-CTMS-130 | FS-SS-02 | FPI event tracking |
| DS-CTMS-131 | FS-AUDIT-01 | Vault Audit object |
| DS-CTMS-132 | FS-AUDIT-02 | Audit-severity escalation |
| DS-CTMS-133 | FS-SEC-02 | Per-study + per-country scopes |
| DS-CTMS-134 | FS-SEC-03 | Investigator-contact encryption |
| DS-CTMS-135 | FS-SEC-04 | GDPR Art. 22 block |
| DS-CTMS-136 | FS-SEC-05 | DPIA template |
| DS-CTMS-137 | FS-SEC-06 | GDPR Art. 17 triage |
| DS-CTMS-138 | FS-TRN-01 | LMS gate |
| DS-CTMS-139 | FS-PR-01 | Annual periodic review |
| DS-CTMS-140 | FS-PR-02 | PR scope |
| DS-CTMS-141 | FS-INTL-01 | Supported locales |
| DS-CTMS-142 | FS-INTL-02 | TZ-aware window calc |
| DS-CTMS-143 | FS-INTL-03 | Locale formatter |
| DS-CTMS-144 | FS-PERF-01 | P95 object-open target |
| DS-CTMS-145 | FS-PERF-02 | Site-list export target |
| DS-CTMS-146 | FS-BAK-01 / FS-BAK-02 / FS-XSYS-BAK-01 | Backup tier + immutability |
| DS-CTMS-147 | FS-AV-01 | Veeva SLA tracking |
| DS-CTMS-148 | FS-VND-01 | Vendor-quality register |
| DS-CTMS-149 | FS-VND-02 | Release-evaluation |
| DS-CTMS-150 | FS-VND-03 | Sub-processor inventory |
| DS-CTMS-151 | FS-VND-04 | Vendor-incident notification |
| DS-CTMS-152 | FS-XINT-HEL-01 | Helios audit-event bus |
| DS-CTMS-153 | FS-XINT-HEL-02 | Helios reconciliation job |
| DS-CTMS-154 | FS-XINT-LMS-01 | LMS competence adapter |

---

## 11. Design-Level Risk Register

| ID | Design-level risk | Likelihood | Impact | Mitigation reference (DS) |
|---|---|---|---|---|
| DR-01 | Vault 24R3 Clinical Operations–EDC Connection (DS-CTMS-100) drift between Vault + Rave protocol-deviation schemas after a vendor release | Medium | High | DS-CTMS-149 (Veeva release-evaluation 14-day SLA) |
| DR-02 | MasterControl idempotency-key collision (DS-CTMS-53) when a deviation_id is reused across two studies sharing a sub-deviation | Low | High | Key composition `{study_id}:{deviation_id}` documented + OQ-CAPA-01 regression |
| DR-03 | Financials idempotency-key collision (DS-CTMS-61) on a re-issued milestone-id after milestone correction | Low | High | Key composition `{study_id}:{site_id}:{milestone_id}:{payment_id}` documented + DS-CTMS-62 overpayment guard |
| DR-04 | SAE clock-display (DS-CTMS-77) mis-implementation makes CTMS appear to own the regulatory clock — failed BIMO finding | Low | Critical | FS-SAF-02 — display-only; FS-INT-ARGUS-02 (Argus is record-of-truth); OQ-SAF-02 |
| DR-05 | DSMB charter version drift (DS-CTMS-104) undetected across study sites | Medium | High | `dsmb-charter-drift-job` daily run + alert |
| DR-06 | Site lifecycle state-machine (DS-CTMS-26) allows transition skip when CRA Lead has dual roles | Low | High | DS-CTMS-25 strict gate + SoD enforcement at role-permission layer |
| DR-07 | EDL gate at site activation (DS-CTMS-73) depends on Marinos eTMF inspection-readiness score (DS-CTMS-75) — eTMF outage blocks activation | Medium | Medium | Vault Connect retry queue + manual override workflow with audit-trail evidence |
| DR-08 | CTIS resubmission flag (DS-CTMS-124) misinterpreted as "no submission required" rather than "no invoice for technical resubmission" | Low | Medium | DS-CTMS-124 explicit evidence capture; periodic review (DS-CTMS-140) verifies |
| DR-09 | 1572 re-sign triggers (DS-CTMS-30) miss a sub-I addition due to delegation log misalignment | Medium | High | DS-CTMS-31 + DS-CTMS-32 training-check at activation cross-checks |
| DR-10 | National-CA gateway TLS certificate rotation (DS-CTMS-123) breaks DACH submission window | Medium | High | Pre-rotation test in UAT; runbook with rollback path |
| DR-11 | Helios reconciliation job (DS-CTMS-153) false-positive on schema migration | Medium | Low | 0.01%-over-24h threshold; manual review of reconciliation output |
| DR-12 | Per-study DPIA template (DS-CTMS-136) skipped on a fast-start studies with EU sites — GDPR Art. 35 breach | Low | High | FPI gate enforced; quarterly DPO audit |
| DR-13 | Backup S3 Object Lock Compliance mode (DS-CTMS-146) misconfigured to Governance mode | Low | High | AUR-FS-BACKUP-001 verification + monthly QA-witnessed restore |
| DR-14 | Vault audit-trail-watchdog (DS-CTMS-85) heartbeat conflicts with a Veeva-published maintenance window → spurious `READ_ONLY` | Low | Medium | Watchdog runbook explicitly pauses during published vendor maintenance |
| DR-15 | Inspector Okta group (DS-CTMS-111) overprivileged via group inheritance includes payment-view scope | Low | High | Access-review (DS-CTMS-133) + role-permission OQ regression |
| DR-16 | DACH locale pack (DS-CTMS-141) on de-AT vs de-DE drift breaks AGES-side notification formatting | Medium | Medium | Locale-pack regression test + DS-CTMS-143 UI formatter |
| DR-17 | Risk-Register review cadence (DS-CTMS-51) skipped on a fast-enrolling oncology study | Medium | High | `risk-review-reminder` daemon + DS-CTMS-139 annual review check |
| DR-18 | Drug forecast horizon (DS-CTMS-57) at 4-week threshold triggers false-positive for high-velocity studies | Medium | Low | DS-CTMS-58 alert routing to Supply Chain + manual review window |
| DR-19 | Site Closeout gate (DS-CTMS-118) bypassed when Marinos EDL endpoint returns stale state | Low | Medium | Vault Connect retry + DS-CTMS-74 document-version sync mismatch alerts |
| DR-20 | LMS competence adapter (DS-CTMS-154) cache TTL allows lapsed training to gate-pass during cache window | Medium | Medium | 12-h TTL maximum; reconciliation job verifies no gated action proceeded with lapsed competence |

The DS Design-level Risk Register is the design-stage seed for `DRY-RA-CTMS-001`; per-FS-ID criticality remains in the FS Implementation Risk Register.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
