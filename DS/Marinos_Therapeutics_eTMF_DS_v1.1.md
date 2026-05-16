---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "MRN-FS-ETMF-001 v1.3 (parent FS)"
  - "MRN-URS-ETMF-001 v1.3 (parent URS, transitive)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 Configuration Specification conventions"
  - "21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300; 21 CFR Parts 312 + 314 + 54"
  - "FDA Computerized Systems Used in Clinical Investigations (2007)"
  - "FDA BIMO Inspection Manual 7348.809 (4 April 2025)"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026; supersedes the September 2025 guidance)"
  - "ICH E6(R3) GCP (Step 4, adopted 6 January 2025)"
  - "EU CTR 536/2014 Arts. 25, 56, 57, 58, 71, 81"
  - "EMA Guideline on TMF content, management and archiving (EMA/INS/GCP/856758/2018 Rev 2)"
  - "DIA TMF Reference Model v3.3.1 (CDISC, 2023)"
  - "GDPR Arts. 6, 9, 32, 35"
  - "Veeva Vault eTMF 24R3 — Validation Approach + Configuration Reference"
parent_fs:
  document_number: MRN-FS-ETMF-001
  version: 1.3
  file: ../../../FS_FDS/_generated/final/Marinos_Therapeutics_eTMF_FS_v1.3.md
parent_urs:
  document_number: MRN-URS-ETMF-001
  version: 1.3
  file: ../../../URS/_generated/final/eTMF_Electronic_Trial_Master_File__Marinos_Therapeutics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## eTMF — Veeva Vault eTMF 24R3 — Configuration Specification (sponsor-side; Marinos Therapeutics tenancy)

**Document Number:** MRN-DS-ETMF-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Parent FS:** MRN-FS-ETMF-001 v1.3
**Parent URS:** MRN-URS-ETMF-001 v1.3 *(informational; transitive via FS)*
**Site:** Marinos Therapeutics *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Project Mode:** Sustaining + Configurable Change *(inherited from parent URS)*
**Regulatory Scope:** 21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300; 21 CFR Parts 312 + 314 + 54; FDA *Computerized Systems Used in Clinical Investigations* (May 2007); FDA BIMO Inspection Manual 7348.809 (4 April 2025); FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance); ICH E6(R3) GCP (Step 4, adopted 6 January 2025); EU CTR 536/2014 Arts. 25/56/57/58/71/81; EU CTR sponsor-archiving obligations; EMA TMF Guideline Rev 2 (EMA/INS/GCP/856758/2018 Rev 2); DIA TMF Reference Model v3.3.1; GDPR Arts. 6, 9, 32, 35; ISO/IEC 27001:2022; PIC/S PI 041.

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QA Reviewer) | _____________ | _____________ | _____ |
| Reviewer (System Owner — Director, TMF Operations) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — Head of GCP Compliance) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Privacy / DPO — GDPR / DPIA) | _____________ | _____________ | _____ |
| Approver (VP Clinical Operations) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Design Control

| Field | Value |
|---|---|
| Document Number | MRN-DS-ETMF-001 |
| Version | 1.1 |
| Effective Date *(synthetic)* | 2026-05-15 |
| Parent FS | MRN-FS-ETMF-001 v1.3 |
| Parent URS *(informational)* | MRN-URS-ETMF-001 v1.3 |
| Site | Marinos Therapeutics *(fictional)* |
| System Class (GAMP 5, 2nd ed.) | Category 4 — Configured Product (multi-tenant SaaS) |
| Project Mode | Sustaining + Configurable Change |
| Regulatory Scope | per Title block |
| Tier | T4 (inherited from parent URS+FS pair) |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue of Configuration Specification for Veeva Vault eTMF 24R3 corresponding to MRN-FS-ETMF-001 v1.3. Inherited Tier T4 from parent URS+FS pair. DS covers 142/142 FS-IDs (100% coverage). Veeva platform internals (cryptographic-integrity primitives, vendor-managed append-only audit-trail DB internals, Veeva SOC 2 vendor-side controls) are flagged as **vendor-internal — no site design surface**. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from MRN-URS-ETMF-001 v1.3 and MRN-FS-ETMF-001 v1.3. DS-specific additions:

| Term | Definition |
|---|---|
| TMFR | DIA TMF Reference Model v3.3.1 |
| EDL | Expected Document List (per TMFR taxonomy) |
| RTMF | Real-Time TMF operating model |
| ISF | Investigator Site File (site-held; mirrored at sponsor side) |
| Zone / Section / Artefact / Sub-artefact | TMFR v3.3.1 taxonomy levels |
| FILED-FINAL | Lifecycle state at which artefact counts toward Completeness |
| CTIS pack | EU CTR Art. 25 + Art. 81 submission package |
| BIMO pack | FDA Bioresearch Monitoring inspection package |
| Inspector Portal | Time-bounded external read-only workspace |
| SoD | Separation of Duties |
| CTQ | Completeness / Timeliness / Quality metric triple |

---

## 1. Purpose

This Configuration Specification defines, at the platform-tenancy level, the configuration values, lifecycle state-machine design, workflow + signature designs, role-permission matrix, and integration endpoint designs that implement MRN-FS-ETMF-001 v1.3. It is the third document in the GAMP 5 V-model for the Marinos Vault eTMF platform.

## 2. Scope

### 2.1 In Scope

- Vault eTMF 24R3 tenancy configuration — DIA TMFR v3.3.1 classification metadata, document lifecycle state machine, e-signature workflows, RTMF Dashboard + Inspection-Readiness gate.
- Per-study + per-country + per-site TMF + ISF-mirror designs.
- EDL design (master library + per-study / per-country / per-site / per-milestone overlays).
- CTQ metric computation + alerting design.
- CTIS pack export design.
- FDA BIMO + EU CA inspection-readiness pack design.
- Inspector Portal design (time-bounded, watermarked, audit-trailed).
- Sponsor / CRO co-management design.
- Legacy migration design.
- Integration design — Okta SSO + MFA + SCIM; Vault Connect to Vault CTMS (Dryad), Vault QualityDocs (Vellis), Vault RIM (Nimbus); Medidata Rave EDC (Marigold) study-build feed; Cornerstone LMS (Vega) read-and-understood trigger; Sirius Argus PV cross-reference; Iolanthe ePRO study-build deposit; EDMS supersession event consumer.
- Cross-system planes — AD identity, AUR backup tier, Helios audit-event bus, LMS competence adapter.

### 2.2 Out of Scope

- Site-side ISF management at investigator site (site SOPs).
- Vault platform internals (Veeva SDLC).
- Cross-system AD design (QTZ-DS-AD-001).
- Cross-system backup design (AUR-DS-BACKUP-001).

## 3. Architectural Overview

The Marinos Vault eTMF platform is a **multi-tenant SaaS** Cat 4 system functioning as the sponsor-side Trial Master File for clinical studies. It organises trial documents by DIA TMFR v3.3.1 taxonomy (Zones 01-11 → Sections → Artefacts → Sub-artefacts), tracks lifecycle state per document revision, computes Completeness / Timeliness / Quality (CTQ) metrics in real time, and exports inspection-ready packages on demand.

### 3.1 Platform Architectural Diagram

```
                  Okta SSO + MFA                           Inspector Portal (time-
                       │                                    bounded, watermarked,
                       ▼                                    audit-trailed)
   ┌────────────────────────────────────────────────────────────────────────────┐
   │       Vault eTMF 24R3 (Marinos Therapeutics tenancy)                       │
   │                                                                            │
   │   ┌──────────────────────────────────────────────────────────────────┐     │
   │   │  DIA TMF Reference Model v3.3.1                                  │     │
   │   │  Zone 01 Trial Management │ Zone 07 Safety Reporting             │     │
   │   │  Zone 02 Central Trial Documents │ Zone 08 Centralised Testing   │     │
   │   │  Zone 03 Regulatory │ Zone 09 Third Parties                       │     │
   │   │  Zone 04 IRB/IEC and other Approvals │ Zone 10 Data Management   │     │
   │   │  Zone 05 Site Management │ Zone 11 Statistics                    │     │
   │   │  Zone 06 IP and Trial Supplies                                   │     │
   │   └──────────────────────────────────────────────────────────────────┘     │
   │                                                                            │
   │   Lifecycle State Machine: DRAFT → IN-REVIEW → APPROVED → FILED-FINAL →    │
   │                            SUPERSEDED → ARCHIVED                           │
   │                                                                            │
   │   Per-study TMF + per-country binders + per-site binders + ISF mirror      │
   │   RTMF dashboard + Inspection-Readiness gate + CTIS pack + BIMO pack       │
   └─┬──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┬─────────────────┘
     │      │      │      │      │      │      │      │      │
     ▼      ▼      ▼      ▼      ▼      ▼      ▼      ▼      ▼
   Vault Vault Vault Medi-  Corner- Sirius Iolanthe Inspector  EDMS
   CTMS  Quality- RIM   data  stone  Argus  Clinical Portal    super-
   (Dry  Docs   (Nim  Rave   LMS    PV     ePRO              session
   ad)   (Vel   bus)   EDC   (Vega)        (Iolanthe)         consumer
         lis)         (Mari                                   (Vellis)
                      gold)
       │
       ▼
   ┌────────────────────────────────────────────────────────────────────────────┐
   │  Cross-system planes                                                       │
   │  • QTZ AD / Entra ID (SAML+SCIM, Splunk gxp-authn, CyberArk PAM)           │
   │  • AUR Backup (Veeam + MS SQL VSS for metadata + object-replica for TMF    │
   │    binaries + S3 Object Lock + LTO-9 air-gap)                              │
   │  • Helios audit-event bus (Kafka helios.ingest.marinos.etmf.v1)            │
   │  • LMS competence adapter (mTLS GET /lms/competence/{user_id})             │
   └────────────────────────────────────────────────────────────────────────────┘
```

### 3.2 Lifecycle State Machine Diagram

```
   ┌─────────┐    ┌──────────┐   ┌──────────┐   ┌─────────────┐   ┌────────────┐   ┌──────────┐
   │  DRAFT  │───►│IN-REVIEW │──►│ APPROVED │──►│ FILED-FINAL │──►│ SUPERSEDED │──►│ ARCHIVED │
   └─────────┘    └──────────┘   └──────────┘   └─────────────┘   └────────────┘   └──────────┘
        ▲              │              │                                                  
        │              ▼              ▼                                                  
        │       (reviewer SoD)  (approver SoD)                                           
        │                                                                                
        └─── revision creates new DRAFT (FS-DOC-03)                                      
```

Only `FILED-FINAL` and `ARCHIVED` count toward Completeness.

### 3.3 Counterparty Integration Map

| Counterparty | Protocol | Direction | Endpoint pattern | Auth | FS-ID |
|---|---|---|---|---|---|
| Okta IdP | SAML 2.0 + SCIM 2.0 | bidirectional | `marinos.okta.com` | TLS 1.3 + mutual cert | FS-INT-SSO-01 |
| Vault CTMS (Dryad) | Vault Connect | bidirectional | `dryad.veevavault.com` | OAuth2 | FS-INT-CTMS-01 |
| Vault QualityDocs (Vellis) | Vault Connect | bidirectional | `vellis.veevavault.com` | OAuth2 | FS-INT-EDMS-01 |
| Vault RIM (Nimbus) | Vault Connect | bidirectional | `nimbus.veevavault.com` | OAuth2 | FS-INT-RIM-01 |
| Medidata Rave EDC (Marigold) | REST + ODM-XML | inbound (study-build deposit) | `marigold.mdsol.com` | OAuth2 | FS-INT-EDC-01 |
| Cornerstone LMS (Vega) | REST + event | outbound (R&U trigger) | `vega-lms.cornerstone.local` | OAuth2 | FS-INT-LMS-01 |
| Sirius Argus PV | REST cross-link | bidirectional | `sirius.veevavault.com` | OAuth2 | FS-INT-PV-01 |
| Clario eCOA (Iolanthe) | REST | inbound (study-build deposit) | `clario-iolanthe.local` | OAuth2 | FS-INT-EPRO-01 |
| Vault Connect API | OAuth 2.0 client-credentials | bidirectional | per-vault | short-lived tokens (15 min) | FS-INT-API-01 |
| Inspector Portal | REST + short-lived token | outbound | `inspector.marinos.veevavault.com` | OAuth2 token (15 min validity) | FS-PART11-08 |
| Vellis EDMS supersession consumer | event (`vellis.doc.superseded.v1`) | inbound | event-bus | mTLS | FS-XINT-EDMS-01 |
| Helios audit-event bus | Kafka | outbound | `kafka.helios.marinos-prod.local` | mTLS + SASL/SCRAM | FS-XINT-HEL-01 |
| LMS competence adapter | REST | outbound | `lms.marinos-prod.local` | mTLS + Entra workload-identity | FS-XINT-LMS-01 |

---

## 4. Configuration Specification

### 4.1 Tenancy + SSO + Vendor-Assurance Configuration

| CI-ID | Configuration item (Veeva-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-01 | Vault IdP Mode | `Okta SAML 2.0 + MFA (external IdP)` | Custom | Per FS-INT-SSO-01 + FS-PART11-04. | FS-INT-SSO-01, FS-PART11-04, FS-XSYS-AD-01 | OQ-AUTHN-01 |
| DS-ETMF-02 | SCIM 2.0 Provisioning | `Enabled — Okta → Vault eTMF` | Custom | Per FS-INT-SSO-01. | FS-INT-SSO-01 | IQ-SCIM-01 |
| DS-ETMF-03 | Vault Connect Auth | `OAuth 2.0 client-credentials; short-lived tokens (15 min)` | Custom | Per FS-INT-API-01. | FS-INT-API-01, FS-PART11-08 | OQ-API-01 |
| DS-ETMF-04 | Service-Account Auth | `mTLS only (no shared secrets)` | Custom | Per FS-PART11-04. | FS-PART11-04 | OQ-SA-01 |
| DS-ETMF-05 | Session Timeout | `30 minutes idle` | Default | Per FS-SEC-02. | FS-SEC-02 | OQ-SESS-01 |
| DS-ETMF-06 | Force-Reauth at Sign | `Enabled (max-age 5 min OAuth2 token)` | Custom | Per FS-PART11-12. | FS-PART11-12 | OQ-PART11-200 |
| DS-ETMF-07 | MFA Methods | `Okta Verify Push, FIDO2 WebAuthn, YubiKey` | Custom | Phishing-resistant per Marinos InfoSec. | FS-PART11-13 | OQ-MFA-01 |
| DS-ETMF-08 | Account Lockout | `5 failures / 15 minutes` | Custom | Per FS-PART11-13. | FS-PART11-13 | OQ-PART11-300 |
| DS-ETMF-09 | Vendor-Assurance Dossier | `SOC 2 Type II (current) + ISO/IEC 27001:2022 + Veeva CSV summary for 24R3 + HIPAA evidence — annual re-qualification` | Custom | Per FS-VND-01. | FS-VND-01 | IQ-VND-01 |
| DS-ETMF-10 | Release-Note Workflow | `RNS feed → vendor-assurance owner → impact-assessment template → change-control record within 14 days` | Custom | Per FS-VND-02. | FS-VND-02 | OQ-VND-01 |
| DS-ETMF-11 | Vendor SDLC Evidence Review Cadence | `Annual` | Custom | Per FS-VND-03. | FS-VND-03 | OQ-VND-02 |
| DS-ETMF-12 | Sub-Processor List Review | `Quarterly per DPA Annex II; new sub-processors → DPIA delta-review` | Custom | Per FS-VND-04. | FS-VND-04 | OQ-VND-03 |
| DS-ETMF-13 | SLA-Report Review | `Quarterly; breaches logged in vendor-assurance dossier + eQMS deviation` | Custom | Per FS-VND-05. | FS-VND-05 | OQ-VND-04 |
| DS-ETMF-14 | Conditional-Access Policy | `Clinical-Sensitive Conditional Access (FIDO2 + sponsor-tenant isolation)` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-CA-01 |
| DS-ETMF-15 | SIEM Forwarding | `Splunk gxp-authn syslog RFC 5424; lag ≤ 5 min` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-SIEM-01 |
| DS-ETMF-16 | PAM Break-Glass | `CyberArk PAM — 24 h rotation + dual-witness` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-PAM-01 |

### 4.2 DIA TMFR v3.3.1 Taxonomy Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-17 | TMFR Version | `DIA TMF Reference Model v3.3.1` | Custom | Per FS-TMFR-01. | FS-TMFR-01 | OQ-TMFR-01 |
| DS-ETMF-18 | TMFR Zones (top level) | `01-11 per v3.3.1 published taxonomy` | Custom | Per FS-TMFR-01. | FS-TMFR-01 | OQ-TMFR-02 |
| DS-ETMF-19 | Sections + Artefacts Set | `Per v3.3.1; deviations in `/config/tmfr-3-3-1-deviations.md`` | Custom | Per FS-TMFR-02. | FS-TMFR-02 | OQ-TMFR-03 |
| DS-ETMF-20 | Sub-Artefacts Picker | `UI shows zone → section → artefact → sub-artefact pickers per v3.3.1` | Custom | Per FS-TMFR-04. | FS-TMFR-04 | OQ-TMFR-04 |
| DS-ETMF-21 | Per-Study TMF Index | `Derived from master taxonomy with filters: Phase, indication, regions, IMP class` | Custom | Per FS-TMFR-05. | FS-TMFR-05 | OQ-TMFR-05 |
| DS-ETMF-22 | TMFR Migration Field | `legacy_classification preserved for v3.x → v4 migration` | Custom | Per FS-TMFR-03. | FS-TMFR-03 | OQ-TMFR-06 |
| DS-ETMF-23 | Classification Mandatory at FILED-FINAL | `DB constraint: classification_zone_id + classification_section_id + classification_artefact_id NOT NULL at FILED-FINAL transition` | Custom | Per FS-TMFR-06. | FS-TMFR-06 | OQ-TMFR-07 |

### 4.3 Document Lifecycle Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-24 | Lifecycle State Machine | `DRAFT → IN-REVIEW → APPROVED → FILED-FINAL → SUPERSEDED → ARCHIVED` | Custom | Per FS-DOC-01. | FS-DOC-01 | OQ-DOC-01 |
| DS-ETMF-25 | Lifecycle Transition Workflow | `Wired to e-sig workflow with SoD enforcement (DS-ETMF-32..34)` | Custom | Per FS-DOC-02. | FS-DOC-02 | OQ-DOC-02 |
| DS-ETMF-26 | FILED-FINAL Immutability | `Immutable flag at DB layer; revision creates new DRAFT record` | Custom | Per FS-DOC-03. | FS-DOC-03 | OQ-DOC-03 |
| DS-ETMF-27 | Version Sequence Constraint | `DB unique constraint + sequence trigger per artefact-instance` | Custom | Per FS-DOC-04. | FS-DOC-04 | OQ-DOC-04 |
| DS-ETMF-28 | PDF/A-3 Rendition Generation | `Auto on FILED-FINAL transition; native format retained as Original` | Custom | Per FS-DOC-05. | FS-DOC-05 | OQ-DOC-05 |
| DS-ETMF-29 | Classification Metadata Schema | `zone, section, artefact, sub-artefact, country, site, study, milestone, document_date, effective_date` | Custom | Per FS-DOC-06. | FS-DOC-06 | OQ-DOC-06 |
| DS-ETMF-30 | Reason-for-Change Vocabulary | `Editorial, Substantive, Regulatory (controlled vocabulary)` | Custom | Per FS-DOC-07. | FS-DOC-07 | OQ-DOC-07 |
| DS-ETMF-31 | Bulk Re-Classification Cap | `Authenticated API or batch tool with per-item audit; manual UI limited to 50 items per action` | Custom | Per FS-DOC-08. | FS-DOC-08 | OQ-DOC-08 |

### 4.4 SoD + Signature Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-32 | SoD Constraint | `filer.user_id ≠ reviewer.user_id ≠ approver.user_id of same document_revision_id (DB constraint + workflow gate)` | Custom | Per FS-SOD-01. | FS-SOD-01 | OQ-SOD-01 |
| DS-ETMF-33 | Vault Admin Permission Matrix | `Excludes file / review / approve actions` | Custom | Per FS-SOD-02. | FS-SOD-02 | OQ-SOD-02 |
| DS-ETMF-34 | CRO Liaison Closeout SoD | `Requires sponsor co-signature (workflow-enforced)` | Custom | Per FS-SOD-03. | FS-SOD-03 | OQ-SOD-03 |

### 4.5 E-Signature Workflow Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-35 | Form 1572 Workflow | `Investigator + sub-investigator e-sig + dates; archived in Zone 05 Site Management` | Custom | Per FS-ESW-01. | FS-ESW-01 | OQ-ESW-01 |
| DS-ETMF-36 | FDF Workflow | `21 CFR Part 54 — investigator + sub-investigator + annual re-confirmation reminder; archived in Zone 05` | Custom | Per FS-ESW-02. | FS-ESW-02 | OQ-ESW-02 |
| DS-ETMF-37 | ICF Variant Linking | `Per-language + per-country variants linked under common ICF parent; CURRENT flag single-valued per site / date-range` | Custom | Per FS-ESW-03. | FS-ESW-03 | OQ-ESW-03 |
| DS-ETMF-38 | IRB/IEC Approval Workflow | `Expiry date tracked; D-30 + D-7 + D-0 alerts; lapse blocks new consent submissions in dependent sites` | Custom | Per FS-ESW-04. | FS-ESW-04 | OQ-ESW-04 |
| DS-ETMF-39 | Protocol Amendment Workflow | `EDL refresh + per-country impact assessment + LMS read-and-understood task creation` | Custom | Per FS-ESW-05. | FS-ESW-05 | OQ-ESW-05 |

### 4.6 EDL Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-40 | Master Document Type Library | `Aligned with TMFR v3.3.1; extensions approved by Director TMF Ops + Head of GCP Compliance` | Custom | Per FS-EDL-01. | FS-EDL-01 | OQ-EDL-01 |
| DS-ETMF-41 | Per-Study EDL | `Master + study-specific artefact overlays; configurable DEV → UAT → PROD` | Custom | Per FS-EDL-02. | FS-EDL-02 | OQ-EDL-02 |
| DS-ETMF-42 | Per-Country EDL Overlays | `US (FDA Form 1572, FDF), DE (BfArM + PEI), CH (Swissmedic), AT (AGES); country-attribute-driven` | Custom | Per FS-EDL-03. | FS-EDL-03 | OQ-EDL-03 |
| DS-ETMF-43 | Per-Site EDL Overlays | `Site initiation / activation / closure artefact sets` | Custom | Per FS-EDL-04. | FS-EDL-04 | OQ-EDL-04 |
| DS-ETMF-44 | Per-Milestone EDL Filters | `FPI, LPI, LPO, DBL, CSR, Archive — selectable in dashboard view` | Custom | Per FS-EDL-05. | FS-EDL-05 | OQ-EDL-05 |
| DS-ETMF-45 | Mid-Study EDL Change Workflow | `Impact-assessment workflow; retrospective changes require Study TMF Owner + GCP Compliance approval` | Custom | Per FS-EDL-06. | FS-EDL-06 | OQ-EDL-06 |

### 4.7 Per-Country + Per-Site Binders + ISF-Mirror Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-46 | Per-Country Binder View | `Aggregates trial-level + country-regulatory artefacts; country-flag-driven filtering` | Custom | Per FS-BIND-01. | FS-BIND-01 | OQ-BIND-01 |
| DS-ETMF-47 | Per-Site Binder View | `Form 1572, FDF, CVs, site-IRB, ICF version log, delegation log, monitoring visits` | Custom | Per FS-BIND-02. | FS-BIND-02 | OQ-BIND-02 |
| DS-ETMF-48 | ISF Mirror View | `Sponsor-side records mirroring site-held ISF; mirror-status indicator per artefact (mirrored / pending / discrepant)` | Custom | Per FS-BIND-03. | FS-BIND-03 | OQ-BIND-03 |
| DS-ETMF-49 | ISF Discrepancy Report | `Generated per monitoring visit; CRA reconciles against on-site walk-through` | Custom | Per FS-BIND-04. | FS-BIND-04 | OQ-BIND-04 |
| DS-ETMF-50 | Country / Site Binder Export | `PDF/A-3 export ≤ 4 BH per inspection-readiness request` | Custom | Per FS-BIND-05. | FS-BIND-05 | PQ-BIND-01 |

### 4.8 CTQ + RTMF Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-51 | Completeness Calculation | `FILED-FINAL EDL artefacts / total required EDL artefacts; per country + per site` | Custom | Per FS-CTQ-01. | FS-CTQ-01 | OQ-CTQ-01 |
| DS-ETMF-52 | Timeliness Calculation | `event-timestamp → FILED-FINAL diff vs per-artefact SLA` | Custom | Per FS-CTQ-02. | FS-CTQ-02 | OQ-CTQ-02 |
| DS-ETMF-53 | Timeliness SLA — Safety Letter | `5 business days` | Custom | Per FS-CTQ-02. | FS-CTQ-02 | OQ-CTQ-03 |
| DS-ETMF-54 | Timeliness SLA — Site-Initiation Pack | `10 business days` | Custom | Per FS-CTQ-02. | FS-CTQ-02 | OQ-CTQ-04 |
| DS-ETMF-55 | Timeliness SLA — Protocol Amendment | `15 business days` | Custom | Per FS-CTQ-02. | FS-CTQ-02 | OQ-CTQ-05 |
| DS-ETMF-56 | Quality Calculation | `rejected-on-first-review count / total reviews; rolling 90-day window` | Custom | Per FS-CTQ-03. | FS-CTQ-03 | OQ-CTQ-06 |
| DS-ETMF-57 | Inspection-Ready Gate | `Completeness ≥ 95% AND Timeliness P95 within SLA AND Quality first-pass ≥ 90% (workflow-enforced)` | Custom | Per FS-CTQ-04. | FS-CTQ-04 | OQ-CTQ-07 |
| DS-ETMF-58 | RTMF Dashboard Refresh | `≤ 5 min latency; red / amber / green flagging` | Custom | Per FS-CTQ-05. | FS-CTQ-05 | OQ-RTMF-01 |
| DS-ETMF-59 | Feed-Delay Alerting | `Source-system event vs eTMF filing > 24 h (safety) or > 5 BD (standard) → alert Director TMF Ops` | Custom | Per FS-CTQ-06. | FS-CTQ-06 | OQ-CTQ-08 |
| DS-ETMF-60 | TMF Health Report Cadence | `Weekly + at milestones; Study TMF Owner sign-off` | Custom | Per FS-CTQ-07. | FS-CTQ-07 | OQ-CTQ-09 |
| DS-ETMF-61 | Forecast Model | `Projects Completeness at upcoming milestone given current filing velocity; > 15% projected miss → flag` | Custom | Per FS-CTQ-08. | FS-CTQ-08 | OQ-CTQ-10 |

### 4.9 Quality Review Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-62 | Quality Review Queue UI | `Filterable by artefact-type + country + site + CRO + filer; SLA-driven priority` | Custom | Per FS-QC-01. | FS-QC-01 | OQ-QC-01 |
| DS-ETMF-63 | QC Rule Engine | `Signature presence + date validity + country-flag consistency + IRB/IEC version-match; per-artefact rule sets in `/config/edl-rules/`` | Custom | Per FS-QC-02 + FS-QC-03. | FS-QC-02, FS-QC-03 | OQ-QC-02 |
| DS-ETMF-64 | Reject-Code Vocabulary | `/config/qc-reject-codes.yml`; reject without code blocked at workflow | Custom | Per FS-QC-04. | FS-QC-04 | OQ-QC-03 |
| DS-ETMF-65 | Quarterly Calibration | `30-document blind sample reviewed by all reviewers; agreement-metric tracked` | Custom | Per FS-QC-05. | FS-QC-05 | OQ-QC-04 |

### 4.10 Inspection-Readiness Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-66 | Inspection-Readiness Dashboard | `Per-study widget: Completeness % + Timeliness P95 + Quality first-pass + last-review-date + open-deviation count` | Custom | Per FS-INSP-01. | FS-INSP-01 | OQ-INSP-01 |
| DS-ETMF-67 | Inspection-Readiness Export | `PDF/A-3 + machine-readable index (JSON) + classification matrix; ≤ 4 BH SLA` | Custom | Per FS-INSP-02. | FS-INSP-02 | OQ-INSP-02 |
| DS-ETMF-68 | Inspector Workspace Provisioning | `Time-bounded (30 d default), watermarked downloads, audit-trailed activity, separate access-zone` | Custom | Per FS-INSP-03. | FS-INSP-03 | OQ-INSP-03 |
| DS-ETMF-69 | Expiry Flag Set | `Overdue artefacts (red), IRB/IEC < 30 d, ICF < 30 d, investigator credentials (CV, GCP training, license) < 30 d` | Custom | Per FS-INSP-04. | FS-INSP-04 | OQ-INSP-04 |
| DS-ETMF-70 | FDA BIMO Pack Content | `Site-selection rationale + CRA visit reports + deviation logs + SDV evidence cross-link to Medidata Rave` | Custom | Per FS-INSP-05. | FS-INSP-05 | OQ-BIMO-01 |
| DS-ETMF-71 | EU CA Pack Content | `BfArM / PEI / Swissmedic / AGES — CTIS-routed submission references + EU CTR Art. 56-58 archive provenance + EudraVigilance cross-link` | Custom | Per FS-INSP-06. | FS-INSP-06 | OQ-INSP-05 |

### 4.11 CTIS Pack Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-72 | CTIS Pack Schema | `EU CTR Art. 25 + Art. 81 compatible; validated against current CTIS schema in CI` | Custom | Per FS-CTIS-01. | FS-CTIS-01 | OQ-CTIS-01 |
| DS-ETMF-73 | CTIS Pack Assembly | `Zone 01 (protocol) + Zone 02 (IB, IMPD) + Zone 03 (application form, GMP statement) + Zone 04 (IRB/IEC approvals); missing-required blocks` | Custom | Per FS-CTIS-02. | FS-CTIS-02 | OQ-CTIS-02 |
| DS-ETMF-74 | CTIS Pack Versioning + RIM Cross-Link | `Version history retained; cross-link to Vault RIM submission record` | Custom | Per FS-CTIS-03. | FS-CTIS-03 | OQ-CTIS-03 |

### 4.12 Audit Trail + ALCOA+ Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-75 | Audit-Trail Event Coverage | `Filing + classification + lifecycle + signature + config + role + EDL + deletion-attempts (8 event classes)` | Custom | Per FS-AUD-01. | FS-AUD-01, FS-PART11-05 | OQ-AUDIT-01 |
| DS-ETMF-76 | Tenant Admin Audit Permission Matrix | `Excludes UPDATE/DELETE on audit-trail rows; verified by OQ + annual access review` | Custom | Per FS-AUD-02. | FS-AUD-02 | OQ-AUDIT-02 |
| DS-ETMF-77 | Audit-Trail Review Cadence | `Monthly by Director TMF Ops + milestone sampling per study` | Custom | Per FS-AUD-03. | FS-AUD-03 | OQ-AUDIT-03 |
| DS-ETMF-78 | Audit-Trail Retention | `≥ 25 y post-trial completion; longer per 21 CFR § 312.62 where US-IND active` | Custom | Per FS-AUD-04. | FS-AUD-04 | OQ-AUDIT-04 |
| DS-ETMF-79 | Audit-Trail Export Signature | `Cryptographically signed by platform; verifiable via published Veeva public key` | Custom | Per FS-AUD-05. | FS-AUD-05 | OQ-AUDIT-05 |
| DS-ETMF-80 | ALCOA+ Attributable | `actor_id (user or service-account); anonymous accounts prohibited` | Custom | Per FS-DI-01. | FS-DI-01 | OQ-DI-01 |
| DS-ETMF-81 | ALCOA+ Legible | `PDF/A-3 + XML/JSON export; OQ rendering test` | Custom | Per FS-DI-02. | FS-DI-02 | OQ-DI-02 |
| DS-ETMF-82 | ALCOA+ Contemporaneous | `Server-side NTP-synced timestamps authoritative; retroactive-filing flag + delay-reason required` | Custom | Per FS-DI-03. | FS-DI-03 | OQ-DI-03 |
| DS-ETMF-83 | ALCOA+ Original | `Raw upload in immutable bucket; renditions reference but never overwrite Original` | Custom | Per FS-DI-04. | FS-DI-04 | OQ-DI-04 |
| DS-ETMF-84 | ALCOA+ Accurate | `CTQ calculations deterministic; reference implementation in `/src/ctq/`; OQ comparison test` | Custom | Per FS-DI-05. | FS-DI-05 | OQ-DI-05 |
| DS-ETMF-85 | ALCOA+ Retrievability | `Routine ≤ 1 BD; inspection ≤ 4 BH; annual verification` | Custom | Per FS-DI-06. | FS-DI-06 | PQ-RETRIEVE-01 |

### 4.13 21 CFR Part 11 Sub-Section Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-86 | § 11.10(a) Procedural Controls SOP | `Linked from system documentation; annual review` | Custom | Per FS-PART11-01. | FS-PART11-01 | OQ-PART11-10a |
| DS-ETMF-87 | § 11.10(b) Copy Generation | `Export engine produces PDF/A-3 + XML/JSON with classification + lifecycle history; OQ-tested` | Custom | Per FS-PART11-02. | FS-PART11-02 | OQ-PART11-10b |
| DS-ETMF-88 | § 11.10(c) Retention Enforcement | `ARCHIVED state with retention-clock; cryptographic-integrity verified on retrieval` | Custom | Per FS-PART11-03. | FS-PART11-03 | OQ-PART11-10c |
| DS-ETMF-89 | § 11.10(d) Access Control | `Okta SAML 2.0 + MFA + role-based authorisation OQ-tested` | Custom | Per FS-PART11-04. | FS-PART11-04 | OQ-PART11-10d |
| DS-ETMF-90 | § 11.10(e) Audit-Trail Schema | `actor + action + timestamp + prior + new + reason for 8 event classes` | Custom | Per FS-PART11-05. | FS-PART11-05 | OQ-PART11-10e |
| DS-ETMF-91 | § 11.10(g) Authority-Check Middleware | `Blocks out-of-role requests at API gateway; UI hides unauthorised actions` | Custom | Per FS-PART11-06. | FS-PART11-06 | OQ-PART11-10g |
| DS-ETMF-92 | § 11.10(k) Manual Currency Gate | `Effective manuals trigger Cornerstone R&U tasks (DS-ETMF-99)` | Custom | Per FS-PART11-07. | FS-PART11-07 | OQ-PART11-10k |
| DS-ETMF-93 | § 11.30 Inspector-Portal Hardening | `Short-lived tokens (15 min) + IP allow-list when contracted + TLS 1.3 mandatory` | Custom | Per FS-PART11-08. | FS-PART11-08 | OQ-PART11-30 |
| DS-ETMF-94 | § 11.50 Signature Manifestation | `PDF/A-3: printed name + date/time (ISO 8601 + TZ) + meaning-of-signature string` | Custom | Per FS-PART11-09. | FS-PART11-09 | OQ-PART11-50 |
| DS-ETMF-95 | § 11.70 Signature Binding | `HMAC-SHA256 record-hash + signer-id + timestamp; tamper-detect alert on read where verification fails` | Custom | Per FS-PART11-10. | FS-PART11-10 | OQ-PART11-70 |
| DS-ETMF-96 | § 11.100 Unique Signature-ID | `Okta uniqueness + Vault user-record constraint; deactivated users retain ID, never reassigned` | Custom | Per FS-PART11-11. | FS-PART11-11 | OQ-PART11-100 |
| DS-ETMF-97 | § 11.200 Re-Auth at Sign Events | `1572, FDF, ICF approval, milestone sign-off — max-age 5 min OAuth2 token; cached creds rejected` | Custom | Per FS-PART11-12. | FS-PART11-12 | OQ-PART11-200 |
| DS-ETMF-98 | § 11.300 Credential Policy | `MFA mandatory + lockout 5/15min + complexity per ISO 27001 baseline` | Custom | Per FS-PART11-13. | FS-PART11-13 | OQ-PART11-300 |

### 4.14 Integration Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-99 | LMS R&U Trigger | `On QualityDocs effective-date for CRA-impacting SOPs → REST event to Cornerstone creates read-and-understood tasks` | Custom | Per FS-INT-LMS-01. | FS-INT-LMS-01 | OQ-LMS-01 |
| DS-ETMF-100 | Vault CTMS (Dryad) Sync | `Bidirectional via Vault Connect; CTMS authoritative for operational metadata; conflict-resolution documented` | Custom | Per FS-INT-CTMS-01. | FS-INT-CTMS-01 | OQ-CTMS-01 |
| DS-ETMF-101 | EDC (Marigold) Auto-File | `On protocol amendment + DBL milestones; payload includes eCRF library + edit-check spec + blank CRF + CCG` | Custom | Per FS-INT-EDC-01. | FS-INT-EDC-01 | OQ-EDC-01 |
| DS-ETMF-102 | RIM (Nimbus) Cross-Link | `Via Vault Connect; eCTD sequence-ID visible on regulatory artefacts` | Custom | Per FS-INT-RIM-01. | FS-INT-RIM-01 | OQ-RIM-01 |
| DS-ETMF-103 | QualityDocs (Vellis) Cross-Reference URN | `Displayed in document metadata` | Custom | Per FS-INT-EDMS-01. | FS-INT-EDMS-01 | OQ-EDMS-01 |
| DS-ETMF-104 | PV (Sirius Argus) Cross-Link | `Case-ID visible on Zone 07 safety-letter artefacts` | Custom | Per FS-INT-PV-01. | FS-INT-PV-01 | OQ-PV-01 |
| DS-ETMF-105 | ePRO (Iolanthe Clinical) Auto-Deposit | `Study-build artefacts auto-deposited on approval` | Custom | Per FS-INT-EPRO-01. | FS-INT-EPRO-01 | OQ-EPRO-01 |
| DS-ETMF-106 | EDMS Supersession Event Consumer | `Listens on `vellis.doc.superseded.v1`; eTMF auto-flags affected sections for re-link review` | Custom | Per FS-XINT-EDMS-01. | FS-XINT-EDMS-01 | OQ-EDMS-02 |
| DS-ETMF-107 | Helios Audit-Event Bus | `Kafka topic `helios.ingest.marinos.etmf.v1`; envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`` | Custom | Per FS-XINT-HEL-01. | FS-XINT-HEL-01 | OQ-HEL-01 |
| DS-ETMF-108 | Helios Reconciliation Job | `Daily parity check; MasterControl deviation on > 0.01% mismatch over 24 h; helios_ack_ts persisted per event` | Custom | Per FS-XINT-HEL-02. | FS-XINT-HEL-02 | OQ-HEL-02 |
| DS-ETMF-109 | LMS Competence Adapter | `GET /lms/competence/{user_id}?curriculum=...` over mTLS + Entra workload-identity; cache TTL 12-24 h | Custom | Per FS-XINT-LMS-01. | FS-XINT-LMS-01 | OQ-LMS-02 |
| DS-ETMF-110 | Backup Integration | `Veeam Application-Aware + MS SQL VSS (metadata) + object-replica (TMF binaries); T1; RPO ≤ 4 h; RTO ≤ 4 BH; S3 Object Lock Compliance; LTO-9 monthly` | Custom | Per FS-XSYS-BAK-01. | FS-XSYS-BAK-01, FS-BAK-01, FS-BAK-02, FS-BAK-03 | OQ-BAK-01 |

### 4.15 Privacy + Security Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-111 | Per-Study Lawful-Basis Register | `/governance/lawful-basis/` per study; GDPR Art. 6` | Custom | Per FS-PRV-01. | FS-PRV-01 | OQ-PRIV-01 |
| DS-ETMF-112 | Patient Pseudonymisation | `Subject-ID mapping; re-identification only via EDC` | Custom | Per FS-PRV-02. | FS-PRV-02 | OQ-PRIV-02 |
| DS-ETMF-113 | Encryption Stance | `TLS 1.3 in transit + AES-256 at rest; vendor evidence on file` | Custom | Per FS-PRV-03 + FS-SEC-01. | FS-PRV-03, FS-SEC-01 | OQ-PRIV-03 |
| DS-ETMF-114 | DPIA URN Field | `Per study; verified at study-build approval workflow` | Custom | Per FS-PRV-04. | FS-PRV-04 | OQ-PRIV-04 |
| DS-ETMF-115 | HIPAA BAA Tracking | `In vendor-assurance dossier; executed with Veeva` | Custom | Per FS-PRV-05. | FS-PRV-05 | OQ-PRIV-05 |
| DS-ETMF-116 | Cross-Border Transfer Routes | `Documented per study via SCCs + supplementary measures; annual review` | Custom | Per FS-PRV-06. | FS-PRV-06 | OQ-PRIV-06 |
| DS-ETMF-117 | Per-Study + Per-Country Access | `Configurable role-matrix; CRO scoped per contract; `/config/security/`` | Custom | Per FS-SEC-02. | FS-SEC-02 | OQ-SEC-01 |
| DS-ETMF-118 | Annual Pen-Test | `Sponsor + inspector endpoints; H/C findings remediated ≤ 30 d` | Custom | Per FS-SEC-04. | FS-SEC-04 | OQ-SEC-02 |
| DS-ETMF-119 | Inspector Credentials Validity | `Time-bounded (30 d default); revocable on demand` | Custom | Per FS-SEC-05. | FS-SEC-05 | OQ-SEC-03 |

### 4.16 Sponsor + CRO Co-Management Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-120 | Per-CRO Scoped Access | `Via Vault security profile; per-protocol delegation matrix; sponsor-oversight dashboards` | Custom | Per FS-CRO-01. | FS-CRO-01 | OQ-CRO-01 |
| DS-ETMF-121 | CRO Transition Workflow | `Hand-over checklist + sponsor sign-off + audit-trail preservation` | Custom | Per FS-CRO-02. | FS-CRO-02 | OQ-CRO-02 |
| DS-ETMF-122 | Per-CRO Quality Dashboard | `Completeness + Timeliness + Quality + Deviation count` | Custom | Per FS-CRO-03. | FS-CRO-03 | OQ-CRO-03 |
| DS-ETMF-123 | CRO-Contracted Scope Enforcement | `Reflected in role-permission matrix; out-of-scope blocked at workflow gate` | Custom | Per FS-CRO-04. | FS-CRO-04 | OQ-CRO-04 |

### 4.17 Legacy Migration Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-124 | Migration Pipeline | `Preserves Original + applied signatures + original metadata + RFC history; audit-trailed per item` | Custom | Per FS-MIG-01. | FS-MIG-01 | OQ-MIG-01 |
| DS-ETMF-125 | Per-Study Migration Verification | `Sampled equivalence + metadata-completeness checks; Director TMF Ops + Head of QA approval` | Custom | Per FS-MIG-02. | FS-MIG-02 | OQ-MIG-02 |
| DS-ETMF-126 | Migration-Specialist Role | `Provisioned with expiry-date attribute; auto-revoked at window close` | Custom | Per FS-MIG-03. | FS-MIG-03 | OQ-MIG-03 |
| DS-ETMF-127 | Migration Discrepancy Routing | `Opened as eQMS deviations; tracked through to closure` | Custom | Per FS-MIG-04. | FS-MIG-04 | OQ-MIG-04 |

### 4.18 Expiry + Localisation + Closeout Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-128 | Expiry-Tracking Schema | `Mandatory expiry-date attribute on IRB/IEC, ICF, investigator credentials, IB, IMPD` | Custom | Per FS-EXP-01. | FS-EXP-01 | OQ-EXP-01 |
| DS-ETMF-129 | Expiry Workflow Logic | `D-30 flag + expired-blocks-workflow (site-activation blocked when site IRB expired)` | Custom | Per FS-EXP-02. | FS-EXP-02 | OQ-EXP-02 |
| DS-ETMF-130 | ICF Current Flag | `Per site + date-range single-valued; superseded ICFs read-only` | Custom | Per FS-EXP-03. | FS-EXP-03 | OQ-EXP-03 |
| DS-ETMF-131 | Obsolescence Workflow | `SUPERSEDED → historical view; preserves retrievability` | Custom | Per FS-EXP-04. | FS-EXP-04 | OQ-EXP-04 |
| DS-ETMF-132 | Language-Locale Metadata | `ISO 639-1 + ISO 3166-1 alpha-2 (e.g., de-DE, de-AT, de-CH)` | Custom | Per FS-LANG-01. | FS-LANG-01 | OQ-LANG-01 |
| DS-ETMF-133 | Sibling Variant Linking | `Parent + per-country variants preserved through revisions` | Custom | Per FS-LANG-02. | FS-LANG-02 | OQ-LANG-02 |
| DS-ETMF-134 | Translation Provenance | `Translator + back-translator + certification-evidence URN filed alongside translated artefact` | Custom | Per FS-LANG-03. | FS-LANG-03 | OQ-LANG-03 |
| DS-ETMF-135 | Inspection-Readiness Variant Selection | `Selectable in Inspection-Readiness export` | Custom | Per FS-LANG-04. | FS-LANG-04 | OQ-LANG-04 |
| DS-ETMF-136 | Closeout EDL | `Final monitoring visit report + drug accountability log + sample disposition + site-archive cert + IP destruction cert` | Custom | Per FS-CLS-01. | FS-CLS-01 | OQ-CLS-01 |
| DS-ETMF-137 | Closeout Sign-Off | `Investigator + sponsor e-sig per § 11.50 / .70` | Custom | Per FS-CLS-02. | FS-CLS-02 | OQ-CLS-02 |
| DS-ETMF-138 | Archive-Transition Workflow | `Freeze TMF index + generate SHA-256 archive manifest + long-term-retention package` | Custom | Per FS-CLS-03. | FS-CLS-03 | OQ-CLS-03 |
| DS-ETMF-139 | Archive Package Format | `PDF/A-3 + machine-readable index; annual integrity check` | Custom | Per FS-CLS-04. | FS-CLS-04 | OQ-CLS-04 |

### 4.19 Inspector Portal + Reporting + Notifications + CCM + Training Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-140 | Inspector Portal Mode | `Read-only + watermarked downloads + 30-d default validity` | Custom | Per FS-INSP-PORTAL-01. | FS-INSP-PORTAL-01 | OQ-INSPP-01 |
| DS-ETMF-141 | Inspector Activity Audit | `Under § 11.10(e)` | Custom | Per FS-INSP-PORTAL-02. | FS-INSP-PORTAL-02 | OQ-INSPP-02 |
| DS-ETMF-142 | Inspector Security Tagging | `Tagged for security-monitoring separation` | Custom | Per FS-INSP-PORTAL-03. | FS-INSP-PORTAL-03 | OQ-INSPP-03 |
| DS-ETMF-143 | Full-Text Search Scope | `Respects access-control scopes` | Custom | Per FS-RPT-01. | FS-RPT-01 | OQ-RPT-01 |
| DS-ETMF-144 | Saved-Search Registry | `Shareable per role; config audit-trailed` | Custom | Per FS-RPT-02. | FS-RPT-02 | OQ-RPT-02 |
| DS-ETMF-145 | Standard Report Library | `TMF Health, Country Completeness, Site Completeness, CRO Quality, Overdue, Expiring, Audit Review` | Custom | Per FS-RPT-03. | FS-RPT-03 | OQ-RPT-03 |
| DS-ETMF-146 | Ad-Hoc Report Builder | `Available to Study TMF Owner + Inspection Coordinator` | Custom | Per FS-RPT-04. | FS-RPT-04 | OQ-RPT-04 |
| DS-ETMF-147 | Per-Zone Sub-Reports | `TMFR 01-11 drillable from TMF Health` | Custom | Per FS-RPT-05. | FS-RPT-05 | OQ-RPT-05 |
| DS-ETMF-148 | Standard Report Render Perf | `≤ 5 min across 250 studies` | Custom | Per FS-RPT-06. | FS-RPT-06 | PQ-RPT-01 |
| DS-ETMF-149 | Notification Service | `Role-targeted email + in-app; configurable templates` | Custom | Per FS-NOT-01. | FS-NOT-01 | OQ-NOT-01 |
| DS-ETMF-150 | Notification Cadence + Thresholds | `Per role + per study; config audit-trailed` | Custom | Per FS-NOT-02. | FS-NOT-02 | OQ-NOT-02 |
| DS-ETMF-151 | Notification Bounce Handling | `Escalates after 3 consecutive failures` | Custom | Per FS-NOT-03. | FS-NOT-03 | OQ-NOT-03 |
| DS-ETMF-152 | Inspection-Imminent Mode | `Prioritises overdue artefacts on dashboard` | Custom | Per FS-NOT-04. | FS-NOT-04 | OQ-NOT-04 |
| DS-ETMF-153 | DEV → UAT → PROD Workflow | `SoD-enforced approvals; PROD requires change-record reference` | Custom | Per FS-CCM-01. | FS-CCM-01 | OQ-CCM-01 |
| DS-ETMF-154 | Configuration Baselines | `Versioned in `/config/baselines/`; baseline-diff tool detects drift` | Custom | Per FS-CCM-02. | FS-CCM-02 | OQ-CCM-02 |
| DS-ETMF-155 | Emergency-Change Review | `Post-implementation review ≤ 5 BD` | Custom | Per FS-CCM-03. | FS-CCM-03 | OQ-CCM-03 |
| DS-ETMF-156 | Vendor Release Impact-Assessment | `≤ 14 d; tracked in `/vendor-assurance/`` | Custom | Per FS-CCM-04. | FS-CCM-04 | OQ-CCM-04 |
| DS-ETMF-157 | Training Currency Gate | `Cornerstone-recorded role-specific training; pre-production access gate; ICH E6(R3) currency check` | Custom | Per FS-TRN-01. | FS-TRN-01 | OQ-TRN-01 |
| DS-ETMF-158 | Annual Refresher Curriculum | `ETMF-2026-ANNUAL — ICH E6(R3) updates + TMFR taxonomy changes + vendor release impact + BIMO + CTIS practice` | Custom | Per FS-TRN-02. | FS-TRN-02 | OQ-TRN-02 |
| DS-ETMF-159 | Annual Periodic Review | `Signed by Director TMF Operations + Head of GCP Compliance + Head of QA + VP Clinical Operations` | Custom | Per FS-PR-01. | FS-PR-01 | OQ-PR-01 |

### 4.20 Performance + Availability Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ETMF-160 | P95 Document-Open Target | `≤ 3 s at 10k concurrent / 250 active studies` | Custom | Per FS-PERF-01. | FS-PERF-01 | PQ-PERF-01 |
| DS-ETMF-161 | Inspection-Export Target | `≤ 4 h for 100k-document study; chunked + parallel pipeline` | Custom | Per FS-PERF-02. | FS-PERF-02 | PQ-PERF-02 |
| DS-ETMF-162 | EDL Batch Re-Evaluation | `≤ 30 min across 250 studies; scheduled nightly` | Custom | Per FS-PERF-03. | FS-PERF-03 | PQ-PERF-03 |
| DS-ETMF-163 | Veeva SLA | `99.5% normal; 99.9% sponsor-critical windows; ≥ 14 d advance maintenance notice` | Default | Per FS-AV-01. | FS-AV-01 | OQ-AV-01 |

---

## 5. Workflow + Business-Rule Design

### 5.1 Document Filing Workflow

| Step | Action | Actor | Lifecycle state | Audit-trail event |
|---|---|---|---|---|
| 1 | Upload document with classification (zone/section/artefact/sub-artefact) | Filer | DRAFT | `DOC_UPLOADED` |
| 2 | Submit for review | Filer | IN-REVIEW | `DOC_SUBMITTED_REVIEW` |
| 3 | QC review against rule set (DS-ETMF-63) | Reviewer (filer.user_id ≠ reviewer.user_id) | IN-REVIEW | `DOC_REVIEWED` |
| 4 | Approve | Approver (reviewer.user_id ≠ approver.user_id) | APPROVED | `DOC_APPROVED` |
| 5 | File as final → triggers PDF/A-3 rendition + Completeness recalc + RTMF refresh | System | FILED-FINAL | `DOC_FILED_FINAL` |
| 6 | Optional supersession on revision | Filer | SUPERSEDED + new DRAFT | `DOC_SUPERSEDED` |
| 7 | Optional archive at study closeout | System | ARCHIVED | `DOC_ARCHIVED` |

### 5.2 EDL Binding Workflow

```
   [TMF Master Document Type Library (DS-ETMF-40)]
            │
            ▼
   [Per-Study EDL Template = master + study-specific overlays (DS-ETMF-41)]
            │
            ▼
   [Per-Country EDL Overlay (DS-ETMF-42)] ◄── country_attribute_driven
            │
            ▼
   [Per-Site EDL Overlay (DS-ETMF-43)] ◄── site_attribute_driven
            │
            ▼
   [Per-Milestone EDL Filter (DS-ETMF-44)] ◄── milestone={FPI,LPI,LPO,DBL,CSR,Archive}
```

### 5.3 IRB / IEC Approval Lifecycle Workflow

```
   [IRB/IEC submission filed in Zone 04]
         │
         ▼
   [IRB/IEC approval received → expiry_date set]
         │
         ▼ Watcher: D-30 / D-7 / D-0 alerts (DS-ETMF-38)
   ┌────────────────────────────────────────────┐
   │  D-30 → Site Coordinator notification       │
   │  D-7  → CRA + Director TMF Ops              │
   │  D-0  → Site activation blocked             │
   └────────────────────────────────────────────┘
```

### 5.4 CTQ Computation + Inspection-Ready Gate Workflow

| Step | Computation | Output |
|---|---|---|
| 1 | For each EDL artefact: count FILED-FINAL vs required | Completeness % per country / site |
| 2 | For each FILED-FINAL: compute event-timestamp → FILED-FINAL diff vs SLA (DS-ETMF-53..55) | Timeliness distribution; P95 |
| 3 | For each Quality Review: count rejected-on-first-review / total | Quality first-pass rate (90-day rolling) |
| 4 | Gate: Completeness ≥ 95% AND Timeliness P95 within SLA AND Quality first-pass ≥ 90% | Inspection-Ready boolean |

### 5.5 Inspector Portal Provisioning Workflow

| Step | Action | Actor | Audit-trail event |
|---|---|---|---|
| 1 | Inspection notice received | Inspection Coordinator | `INSP_NOTICE` |
| 2 | Provision inspector workspace (30-d default validity per DS-ETMF-68) | Inspection Coordinator | `INSP_WORKSPACE_PROVISIONED` |
| 3 | Generate Inspection-Readiness export (DS-ETMF-67) | System | `INSP_EXPORT_GENERATED` |
| 4 | Inspector accesses (watermarked downloads, audit-trailed activity, IP allow-list per FS-PART11-08) | Inspector | `INSP_ACCESS` events |
| 5 | At T+30 d or on-demand revocation | System / Inspection Coordinator | `INSP_WORKSPACE_REVOKED` |

### 5.6 Legacy Migration Workflow

```
   [Migration plan + scope approved]
         │
         ▼ Migration-specialist role provisioned with expiry attribute (DS-ETMF-126)
   [Source system extract → migration pipeline (DS-ETMF-124)]
         │
         ▼ Per-item audit + Original preservation + RFC-history mapping
   [Sampled equivalence + metadata-completeness checks]
         │
         ▼ Director TMF Ops + Head of QA approval
   [Per-study migration verification report (DS-ETMF-125)]
         │
         ▼ Discrepancies opened as eQMS deviations (DS-ETMF-127)
   [Window closes → migration-specialist role auto-revoked]
```

---

## 6. Role-Permission Matrix Design

| Role | File | Review | Approve | Sign 1572/FDF/ICF | Reclassify | Bulk Reclassify (50 cap UI) | Inspection Export | Inspector Portal Read | Legacy Migrate | CRO Scope | Tenant Admin | Vendor Release-Eval |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| TMF Specialist (Filer) | ✓ | ✗ | ✗ | ✗ | (per-doc) | (UI 50 cap) | ✗ | ✗ | ✗ | (scoped) | ✗ | ✗ |
| TMF Reviewer | ✗ | ✓ (filer ≠ reviewer) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | (scoped) | ✗ | ✗ |
| TMF Approver | ✗ | ✗ | ✓ (reviewer ≠ approver) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | (scoped) | ✗ | ✗ |
| Study TMF Owner | ✓ | ✓ | ✓ (SoD enforced) | ✗ | ✓ | (API) | ✓ (request) | ✗ | ✗ | (scoped) | ✗ | ✗ |
| Investigator (PI) | (limited) | ✗ | ✗ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Sub-Investigator | ✗ | ✗ | ✗ | ✓ (FDF/1572) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Sponsor — Director TMF Ops | ✗ | ✓ | ✓ | ✗ | ✓ | ✓ | ✓ | ✗ | ✓ | (sponsor) | ✗ | ✗ |
| Head of GCP Compliance | ✗ | ✓ | ✓ | ✗ | ✓ | ✗ | ✓ | ✗ | ✓ | (sponsor) | ✗ | ✗ |
| Head of QA | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (approve) | ✗ | ✗ | ✗ |
| VP Clinical Operations | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Inspection Coordinator | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Inspector (BIMO / EU CA / DACH) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (time-bounded, watermarked) | ✗ | ✗ | ✗ | ✗ |
| CRO Liaison | ✓ | ✓ | ✓ (closeout requires sponsor co-sign per DS-ETMF-34) | ✗ | (scoped) | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ |
| Migration Specialist | ✓ (Migrate mode) | ✗ | ✗ | ✗ | ✓ | ✓ (API) | ✗ | ✗ | ✓ | ✗ | ✗ | ✗ |
| Privacy / DPO | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Vendor Assurance Owner | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ |
| Tenant Admin (Vault) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (config) | ✗ |

**Role-permission design rules:**
- **SoD enforced** — filer ≠ reviewer ≠ approver on the same document_revision_id (DS-ETMF-32).
- **Tenant Admin excludes filing / review / approval** (DS-ETMF-33).
- **CRO closeout requires sponsor co-signature** (DS-ETMF-34).
- **Migration Specialist role auto-expires at window close** (DS-ETMF-126).
- **Inspector role is time-bounded + watermarked** (DS-ETMF-68 + DS-ETMF-140).

---

## 7. Integration Design

(See § 4.14 for per-integration CIs. The table below summarises endpoint + auth + cadence for each counterparty.)

| Counterparty | Direction | Endpoint | Auth | Cadence / Trigger | FS-ID |
|---|---|---|---|---|---|
| Vault CTMS (Dryad) | bidirectional | `https://dryad.veevavault.com/connect/v1/` | OAuth2 client-credentials | Real-time + nightly reconciliation | FS-INT-CTMS-01 |
| Vault QualityDocs (Vellis) | bidirectional | `https://vellis.veevavault.com/connect/v1/` | OAuth2 + event consumer | Effective-date events | FS-INT-EDMS-01, FS-XINT-EDMS-01 |
| Vault RIM (Nimbus) | bidirectional | `https://nimbus.veevavault.com/connect/v1/` | OAuth2 | On submission-sequence publish | FS-INT-RIM-01 |
| Medidata Rave EDC (Marigold) | inbound | `https://marigold.mdsol.com/v1/etmf-deposit/` | OAuth2 | Amendment + DBL milestones | FS-INT-EDC-01 |
| Cornerstone LMS (Vega) | outbound | `https://vega-lms.cornerstone.local/v1/r&u/create` | OAuth2 | On QualityDocs effective-date for CRA SOPs | FS-INT-LMS-01 |
| Sirius Argus PV | bidirectional | `https://sirius.veevavault.com/connect/v1/` | OAuth2 | Per case-ID cross-link | FS-INT-PV-01 |
| Clario eCOA (Iolanthe) | inbound | `https://clario-iolanthe.local/v1/etmf-deposit/` | OAuth2 | On study-build approval | FS-INT-EPRO-01 |
| Inspector Portal | outbound | `https://inspector.marinos.veevavault.com/v1/` | OAuth2 (15-min tokens) | Inspection-window-bounded | FS-PART11-08 |
| Helios Kafka | outbound | `kafka.helios.marinos-prod.local` | mTLS + SASL/SCRAM | Per audit event | FS-XINT-HEL-01 |
| LMS competence adapter | outbound | `https://lms.marinos-prod.local/lms/competence/{user_id}` | mTLS + Entra workload-identity | Per gated-action request | FS-XINT-LMS-01 |
| AUR Backup | (cross-system) | Veeam + MS SQL VSS + object-replica + S3 Object Lock + LTO-9 | (per AUR DS) | Per backup tier T1 | FS-XSYS-BAK-01 |

---

## 8. Site-Deployed Components Design

| Component | Type | Source location | Owner team | Verified by |
|---|---|---|---|---|
| `ctq-engine` | Library (reference CTQ computation) | `git.marinos-prod.local/etmf/ctq-engine` | TMF Engineering | OQ-CTQ-* + OQ-DI-05 |
| `edl-rules-eval` | Library | `git.marinos-prod.local/etmf/edl-rules-eval` | TMF Engineering | OQ-EDL-* + OQ-QC-02 |
| `rtmf-dashboard-api` | Service | `git.marinos-prod.local/etmf/rtmf-dashboard-api` | TMF Engineering | OQ-RTMF-01 + OQ-CTQ-05 |
| `inspection-export-pipeline` | Service (chunked + parallel) | `git.marinos-prod.local/etmf/inspection-export-pipeline` | TMF Engineering | PQ-PERF-02 |
| `ctis-pack-builder` | Service | `git.marinos-prod.local/etmf/ctis-pack-builder` | TMF Engineering | OQ-CTIS-01..03 |
| `feed-delay-monitor` | Daemon | `git.marinos-prod.local/etmf/feed-delay-monitor` | TMF SRE | OQ-CTQ-08 |
| `migration-pipeline` | Service | `git.marinos-prod.local/etmf/migration-pipeline` | TMF Engineering | OQ-MIG-01..04 |
| `archive-manifest-job` | Scheduled | `git.marinos-prod.local/etmf/archive-manifest-job` | TMF Engineering | OQ-CLS-03 |
| `inspection-readiness-gate` | Service (workflow-enforced) | `git.marinos-prod.local/etmf/inspection-readiness-gate` | TMF Engineering | OQ-CTQ-07 |
| `MRN-EDMS-READ` | Adapter (Vellis EDMS read) | `git.marinos-prod.local/etmf/mrn-edms-read` | TMF Engineering | OQ-EDMS-02 |
| `helios-publisher` | Library | `git.marinos-prod.local/etmf/helios-publisher` | TMF Engineering | OQ-HEL-01..02 |

Each repository carries a `docs/SDS.md` mini-Software-Design-Specification artefact per GAMP 5 2nd-edition § 2B.4 rule 6.

---

## 9. References

### 9.1 US

- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- 21 CFR Parts 312 + 314 + 54.
- FDA *Computerized Systems Used in Clinical Investigations* (2007).
- FDA BIMO Inspection Manual 7348.809 (4 April 2025).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).
- FDA *Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions* (Aug 2025).

### 9.2 EU

- EU CTR 536/2014 Arts. 25/56/57/58/71/81.
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EMA TMF Guideline Rev 2 (EMA/INS/GCP/856758/2018 Rev 2).
- GDPR Arts. 6, 9, 32, 35.

### 9.3 DACH

- BfArM (DE) — DE national medicinal-product authority.
- Paul-Ehrlich-Institut (PEI) — DE biologicals.
- Swissmedic (CH).
- AGES (AT).

### 9.4 International

- ICH E6(R3) GCP (Step 4, adopted 6 January 2025).
- DIA TMF Reference Model v3.3.1 (CDISC, 2023).
- ISPE GAMP 5 (2nd Edition, 2022).
- PIC/S PI 041.
- ISO/IEC 27001:2022.

### 9.5 Vendor

- Veeva Systems — *Vault eTMF 24R3 Validation Approach*.
- Veeva Systems — *Vault eTMF 24R3 Configuration Reference*.
- Veeva Systems — *Vault Connect API Reference*.
- Cornerstone — *Cornerstone LMS Integration Reference*.

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS ID | FS ID(s) | Notes |
|---|---|---|
| DS-ETMF-01 | FS-INT-SSO-01 / FS-PART11-04 / FS-XSYS-AD-01 | IdP mode |
| DS-ETMF-02 | FS-INT-SSO-01 | SCIM provisioning |
| DS-ETMF-03 | FS-INT-API-01 / FS-PART11-08 | Vault Connect auth |
| DS-ETMF-04 | FS-PART11-04 | Service-account auth |
| DS-ETMF-05 | FS-SEC-02 | Session timeout |
| DS-ETMF-06 | FS-PART11-12 | Force-reauth at sign |
| DS-ETMF-07 | FS-PART11-13 | MFA methods |
| DS-ETMF-08 | FS-PART11-13 | Lockout |
| DS-ETMF-09 | FS-VND-01 | Vendor-assurance dossier |
| DS-ETMF-10 | FS-VND-02 | Release-note workflow |
| DS-ETMF-11 | FS-VND-03 | SDLC evidence review |
| DS-ETMF-12 | FS-VND-04 | Sub-processor list review |
| DS-ETMF-13 | FS-VND-05 | SLA-report review |
| DS-ETMF-14 | FS-XSYS-AD-01 | Conditional-access policy |
| DS-ETMF-15 | FS-XSYS-AD-01 | SIEM forwarding |
| DS-ETMF-16 | FS-XSYS-AD-01 | PAM break-glass |
| DS-ETMF-17 | FS-TMFR-01 | TMFR version |
| DS-ETMF-18 | FS-TMFR-01 | TMFR Zones |
| DS-ETMF-19 | FS-TMFR-02 | Sections + Artefacts |
| DS-ETMF-20 | FS-TMFR-04 | Sub-Artefacts |
| DS-ETMF-21 | FS-TMFR-05 | Per-study TMF Index |
| DS-ETMF-22 | FS-TMFR-03 | Migration field |
| DS-ETMF-23 | FS-TMFR-06 | DB constraint at FILED-FINAL |
| DS-ETMF-24 | FS-DOC-01 | Lifecycle state machine |
| DS-ETMF-25 | FS-DOC-02 | Lifecycle workflow |
| DS-ETMF-26 | FS-DOC-03 | FILED-FINAL immutability |
| DS-ETMF-27 | FS-DOC-04 | Version sequence |
| DS-ETMF-28 | FS-DOC-05 | PDF/A-3 rendition |
| DS-ETMF-29 | FS-DOC-06 | Classification schema |
| DS-ETMF-30 | FS-DOC-07 | Reason-for-change vocab |
| DS-ETMF-31 | FS-DOC-08 | Bulk reclassification cap |
| DS-ETMF-32 | FS-SOD-01 | SoD constraint |
| DS-ETMF-33 | FS-SOD-02 | Vault Admin matrix |
| DS-ETMF-34 | FS-SOD-03 | CRO closeout SoD |
| DS-ETMF-35 | FS-ESW-01 | 1572 workflow |
| DS-ETMF-36 | FS-ESW-02 | FDF workflow |
| DS-ETMF-37 | FS-ESW-03 | ICF variant linking |
| DS-ETMF-38 | FS-ESW-04 | IRB/IEC workflow |
| DS-ETMF-39 | FS-ESW-05 | Amendment workflow |
| DS-ETMF-40 | FS-EDL-01 | Master library |
| DS-ETMF-41 | FS-EDL-02 | Per-study EDL |
| DS-ETMF-42 | FS-EDL-03 | Per-country overlays |
| DS-ETMF-43 | FS-EDL-04 | Per-site overlays |
| DS-ETMF-44 | FS-EDL-05 | Per-milestone filters |
| DS-ETMF-45 | FS-EDL-06 | Mid-study EDL change |
| DS-ETMF-46 | FS-BIND-01 | Per-country binder |
| DS-ETMF-47 | FS-BIND-02 | Per-site binder |
| DS-ETMF-48 | FS-BIND-03 | ISF mirror |
| DS-ETMF-49 | FS-BIND-04 | ISF discrepancy report |
| DS-ETMF-50 | FS-BIND-05 | Binder export SLA |
| DS-ETMF-51 | FS-CTQ-01 | Completeness calc |
| DS-ETMF-52 | FS-CTQ-02 | Timeliness calc |
| DS-ETMF-53 | FS-CTQ-02 | Safety-letter SLA |
| DS-ETMF-54 | FS-CTQ-02 | Site-init-pack SLA |
| DS-ETMF-55 | FS-CTQ-02 | Protocol amendment SLA |
| DS-ETMF-56 | FS-CTQ-03 | Quality calc |
| DS-ETMF-57 | FS-CTQ-04 | Inspection-Ready gate |
| DS-ETMF-58 | FS-CTQ-05 | RTMF dashboard |
| DS-ETMF-59 | FS-CTQ-06 | Feed-delay alerting |
| DS-ETMF-60 | FS-CTQ-07 | TMF Health report |
| DS-ETMF-61 | FS-CTQ-08 | Forecast model |
| DS-ETMF-62 | FS-QC-01 | QC queue UI |
| DS-ETMF-63 | FS-QC-02 / FS-QC-03 | QC rule engine |
| DS-ETMF-64 | FS-QC-04 | Reject-code vocab |
| DS-ETMF-65 | FS-QC-05 | Quarterly calibration |
| DS-ETMF-66 | FS-INSP-01 | Inspection-Readiness dashboard |
| DS-ETMF-67 | FS-INSP-02 | Inspection-Readiness export |
| DS-ETMF-68 | FS-INSP-03 | Inspector workspace |
| DS-ETMF-69 | FS-INSP-04 | Expiry flags |
| DS-ETMF-70 | FS-INSP-05 | FDA BIMO pack |
| DS-ETMF-71 | FS-INSP-06 | EU CA pack |
| DS-ETMF-72 | FS-CTIS-01 | CTIS pack schema |
| DS-ETMF-73 | FS-CTIS-02 | CTIS pack assembly |
| DS-ETMF-74 | FS-CTIS-03 | CTIS pack versioning + RIM cross-link |
| DS-ETMF-75 | FS-AUD-01 / FS-PART11-05 | Audit event coverage |
| DS-ETMF-76 | FS-AUD-02 | Tenant admin matrix |
| DS-ETMF-77 | FS-AUD-03 | Audit-trail review cadence |
| DS-ETMF-78 | FS-AUD-04 | Retention |
| DS-ETMF-79 | FS-AUD-05 | Export signature |
| DS-ETMF-80 | FS-DI-01 | Attributable |
| DS-ETMF-81 | FS-DI-02 | Legible |
| DS-ETMF-82 | FS-DI-03 | Contemporaneous |
| DS-ETMF-83 | FS-DI-04 | Original |
| DS-ETMF-84 | FS-DI-05 | Accurate |
| DS-ETMF-85 | FS-DI-06 | Retrievability |
| DS-ETMF-86 | FS-PART11-01 | § 11.10(a) |
| DS-ETMF-87 | FS-PART11-02 | § 11.10(b) |
| DS-ETMF-88 | FS-PART11-03 | § 11.10(c) |
| DS-ETMF-89 | FS-PART11-04 | § 11.10(d) |
| DS-ETMF-90 | FS-PART11-05 | § 11.10(e) |
| DS-ETMF-91 | FS-PART11-06 | § 11.10(g) |
| DS-ETMF-92 | FS-PART11-07 | § 11.10(k) |
| DS-ETMF-93 | FS-PART11-08 | § 11.30 inspector portal |
| DS-ETMF-94 | FS-PART11-09 | § 11.50 manifestation |
| DS-ETMF-95 | FS-PART11-10 | § 11.70 binding |
| DS-ETMF-96 | FS-PART11-11 | § 11.100 uniqueness |
| DS-ETMF-97 | FS-PART11-12 | § 11.200 re-auth |
| DS-ETMF-98 | FS-PART11-13 | § 11.300 credentials |
| DS-ETMF-99 | FS-INT-LMS-01 | LMS R&U trigger |
| DS-ETMF-100 | FS-INT-CTMS-01 | CTMS sync |
| DS-ETMF-101 | FS-INT-EDC-01 | EDC auto-file |
| DS-ETMF-102 | FS-INT-RIM-01 | RIM cross-link |
| DS-ETMF-103 | FS-INT-EDMS-01 | EDMS cross-reference |
| DS-ETMF-104 | FS-INT-PV-01 | PV cross-link |
| DS-ETMF-105 | FS-INT-EPRO-01 | ePRO auto-deposit |
| DS-ETMF-106 | FS-XINT-EDMS-01 | EDMS supersession event |
| DS-ETMF-107 | FS-XINT-HEL-01 | Helios audit-event bus |
| DS-ETMF-108 | FS-XINT-HEL-02 | Helios reconciliation |
| DS-ETMF-109 | FS-XINT-LMS-01 | LMS competence adapter |
| DS-ETMF-110 | FS-XSYS-BAK-01 / FS-BAK-01..03 | Backup integration |
| DS-ETMF-111 | FS-PRV-01 | Lawful-basis register |
| DS-ETMF-112 | FS-PRV-02 | Pseudonymisation |
| DS-ETMF-113 | FS-PRV-03 / FS-SEC-01 | Encryption stance |
| DS-ETMF-114 | FS-PRV-04 | DPIA URN |
| DS-ETMF-115 | FS-PRV-05 | HIPAA BAA |
| DS-ETMF-116 | FS-PRV-06 | Cross-border routes |
| DS-ETMF-117 | FS-SEC-02 | Per-study + per-country access |
| DS-ETMF-118 | FS-SEC-04 | Annual pen-test |
| DS-ETMF-119 | FS-SEC-05 | Inspector credentials validity |
| DS-ETMF-120 | FS-CRO-01 | Per-CRO scoped access |
| DS-ETMF-121 | FS-CRO-02 | CRO transition workflow |
| DS-ETMF-122 | FS-CRO-03 | Per-CRO dashboard |
| DS-ETMF-123 | FS-CRO-04 | CRO scope enforcement |
| DS-ETMF-124 | FS-MIG-01 | Migration pipeline |
| DS-ETMF-125 | FS-MIG-02 | Migration verification |
| DS-ETMF-126 | FS-MIG-03 | Migration-specialist role |
| DS-ETMF-127 | FS-MIG-04 | Migration discrepancy routing |
| DS-ETMF-128 | FS-EXP-01 | Expiry schema |
| DS-ETMF-129 | FS-EXP-02 | Expiry workflow logic |
| DS-ETMF-130 | FS-EXP-03 | ICF current flag |
| DS-ETMF-131 | FS-EXP-04 | Obsolescence workflow |
| DS-ETMF-132 | FS-LANG-01 | Language-locale metadata |
| DS-ETMF-133 | FS-LANG-02 | Sibling variant linking |
| DS-ETMF-134 | FS-LANG-03 | Translation provenance |
| DS-ETMF-135 | FS-LANG-04 | Inspection variant selection |
| DS-ETMF-136 | FS-CLS-01 | Closeout EDL |
| DS-ETMF-137 | FS-CLS-02 | Closeout sign-off |
| DS-ETMF-138 | FS-CLS-03 | Archive-transition |
| DS-ETMF-139 | FS-CLS-04 | Archive package |
| DS-ETMF-140 | FS-INSP-PORTAL-01 | Inspector Portal mode |
| DS-ETMF-141 | FS-INSP-PORTAL-02 | Inspector activity audit |
| DS-ETMF-142 | FS-INSP-PORTAL-03 | Inspector security tagging |
| DS-ETMF-143 | FS-RPT-01 | Full-text search |
| DS-ETMF-144 | FS-RPT-02 | Saved-search registry |
| DS-ETMF-145 | FS-RPT-03 | Standard report library |
| DS-ETMF-146 | FS-RPT-04 | Ad-hoc report builder |
| DS-ETMF-147 | FS-RPT-05 | Per-zone sub-reports |
| DS-ETMF-148 | FS-RPT-06 | Report render perf |
| DS-ETMF-149 | FS-NOT-01 | Notification service |
| DS-ETMF-150 | FS-NOT-02 | Cadence + thresholds |
| DS-ETMF-151 | FS-NOT-03 | Bounce handling |
| DS-ETMF-152 | FS-NOT-04 | Inspection-imminent mode |
| DS-ETMF-153 | FS-CCM-01 | DEV → UAT → PROD workflow |
| DS-ETMF-154 | FS-CCM-02 | Configuration baselines |
| DS-ETMF-155 | FS-CCM-03 | Emergency-change review |
| DS-ETMF-156 | FS-CCM-04 | Vendor release impact-assessment |
| DS-ETMF-157 | FS-TRN-01 | Training currency gate |
| DS-ETMF-158 | FS-TRN-02 | Annual refresher |
| DS-ETMF-159 | FS-PR-01 | Annual periodic review |
| DS-ETMF-160 | FS-PERF-01 | P95 document-open |
| DS-ETMF-161 | FS-PERF-02 | Inspection-export perf |
| DS-ETMF-162 | FS-PERF-03 | EDL batch re-evaluation |
| DS-ETMF-163 | FS-AV-01 | Veeva SLA |

---

## 11. Design-Level Risk Register

| ID | Design-level risk | Likelihood | Impact | Mitigation reference (DS) |
|---|---|---|---|---|
| DR-01 | TMFR v3.3.1 → v4 migration (~2027) breaks historical classifications | Low | High | DS-ETMF-22 (`legacy_classification` preservation) + per-Zone migration playbook |
| DR-02 | Vault Connect outage delays CTMS metadata sync — completeness count stale | Medium | Medium | DS-ETMF-59 (feed-delay alert) + DS-ETMF-100 reconciliation queue |
| DR-03 | CRO security-profile mis-scoping leaks cross-CRO data | Low | High | DS-ETMF-120 quarterly access review + automated profile diff |
| DR-04 | CTIS schema version drift breaks pack export | Medium | High | DS-ETMF-72 CI contract test against published schema |
| DR-05 | RTMF dashboard staleness from feed-delay | Medium | Medium | DS-ETMF-58 5-min refresh + DS-ETMF-59 alert |
| DR-06 | Inspector Portal credential phishing | Low | High | DS-ETMF-68 short-lived tokens + DS-ETMF-140 watermarked downloads + DS-ETMF-93 IP allow-list |
| DR-07 | SoD constraint (DS-ETMF-32) misses a delegated-account loophole | Low | High | OQ-SOD-01 + annual access review (DS-ETMF-118) |
| DR-08 | Bulk reclassification UI 50-item cap (DS-ETMF-31) bypassed via API misuse | Low | High | API per-item audit + Tenant Admin role excludes filing (DS-ETMF-33) |
| DR-09 | EDL rule engine (DS-ETMF-63) misjudges first-pass quality due to ambiguous rule | Medium | Medium | DS-ETMF-65 quarterly calibration + reject-code vocabulary (DS-ETMF-64) |
| DR-10 | Expiry-date-driven blocking (DS-ETMF-129) blocks legitimate site activation due to time-zone drift | Low | Medium | TZ-aware computation + manual override workflow with audit-trail |
| DR-11 | Migration-Specialist role auto-revoke (DS-ETMF-126) trips during legitimate continuation window | Low | Medium | Configurable expiry attribute + window-extension workflow |
| DR-12 | ISF mirror discrepancy report (DS-ETMF-49) shows false-discrepancies due to clock skew | Low | Low | DS-ETMF-82 NTP-synced timestamps |
| DR-13 | Helios reconciliation false-positive on schema migration | Medium | Low | 0.01%-over-24h threshold (DS-ETMF-108) |
| DR-14 | S3 Object Lock Governance mode mis-set instead of Compliance mode | Low | High | AUR-FS-BACKUP-001 verification + monthly QA-witnessed restore |
| DR-15 | LMS competence adapter (DS-ETMF-109) cache TTL permits lapsed training within cache window | Medium | Medium | 12-h max TTL + reconciliation verifies no gated action with lapsed competence |
| DR-16 | Inspection-Ready gate (DS-ETMF-57) false-pass when completeness numerator inflated by misclassified artefacts | Low | High | DS-ETMF-23 (DB constraint at FILED-FINAL) + DS-ETMF-65 quarterly calibration |
| DR-17 | Per-country EDL overlay (DS-ETMF-42) misaligned for DACH variant — e.g., de-AT submission missing AGES-specific artefact | Medium | High | OQ-EDL-03 regression + DS-ETMF-135 inspection variant selection |
| DR-18 | DPIA URN (DS-ETMF-114) absent at EU enrolment start — GDPR Art. 35 breach | Low | High | Study-build approval workflow enforces DPIA URN presence |
| DR-19 | Vault Connect token rotation (15-min validity) breaks long-running CTMS sync | Low | Medium | DS-ETMF-03 retry + automatic token refresh |
| DR-20 | RTMF dashboard refresh latency (DS-ETMF-58) exceeded during inspection week — staleness undetected | Low | High | DS-ETMF-59 feed-delay alert + on-demand refresh override |

The DS Design-level Risk Register is the design-stage seed for `MRN-RA-ETMF-001`; per-FS-ID criticality remains in the FS Implementation Risk Register.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
