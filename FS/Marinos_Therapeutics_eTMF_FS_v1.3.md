---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (FS catch-up to URS v1.2; full per-ID expansion of 151 URS-IDs into FS rows; DIA TMF Reference Model 3.3.1; § 11 sub-section authority map; CTIS; FDA BIMO; sponsor/CRO co-management; legacy migration; GDPR Arts. 6/9/32/35)"
seed_corpus_basis:
  - "MRN-URS-ETMF-001 v1.2 (parent URS)"
  - "ISPE GAMP 5 (2nd Edition, 2022) Cat 4 SaaS conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "21 CFR Part 312 + 314 + 54"
  - "FDA Computerized Systems Used in Clinical Investigations (2007)"
  - "ICH E6(R3) (Step 4, 6 January 2025)"
  - "EU CTR 536/2014 Arts. 25, 56, 57, 58, 71, 81"
  - "EMA Guideline on TMF content, management and archiving (Rev 2)"
  - "DIA TMF Reference Model v3.3.1 (CDISC, 2023)"
  - "GDPR Arts. 6, 9, 32, 35"
  - "ISO/IEC 27001:2022; PIC/S PI 041"
parent_urs:
  document_number: MRN-URS-ETMF-001
  version: 1.2
  file: ../../URS/_generated/final/eTMF_Electronic_Trial_Master_File__Marinos_Therapeutics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# Functional Specification (FS)

## eTMF — Veeva Vault eTMF 24R3 (sponsor-side; Marinos Therapeutics tenancy)

**Document Number:** MRN-FS-ETMF-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** MRN-URS-ETMF-001 v1.2 | **Site:** Marinos Therapeutics (fictional)
**System Class:** GAMP Cat 4 — Configured Product (multi-tenant SaaS)
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Parts 312 + 314 + 54; FDA CSCI (2007); ICH E6(R3) (Step 4, 6 January 2025); EU CTR 536/2014 Arts. 25/56/57/58/71/81; EMA TMF Guideline Rev 2; DIA TMF Reference Model v3.3.1; GDPR Arts. 6, 9, 32, 35; ISO/IEC 27001:2022; PIC/S PI 041.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, TMF Operations) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Privacy / DPO — GDPR / DPIA) | _____________ | _____________ | _____ |
| Reviewer (Head of GCP Compliance) | _____________ | _____________ | _____ |
| Approver (VP Clinical Operations) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue (partial — divergent URS-ID scheme; superseded). |
| 1.1 | 2026-05-08 | (synthetic) | Vendor version bump to 24R3. |
| 1.2 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.2: full per-ID expansion of 151 URS-IDs (no range compression per § 2A.7); DIA TMF Reference Model 3.3.1 explicit; § 11 sub-section authority map applied; CTIS pack export; FDA BIMO + EU CA inspection workflows; sponsor/CRO co-management; legacy-migration validation; GDPR implementation. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies how Veeva Vault eTMF 24R3 is configured at the Marinos Therapeutics tenancy to satisfy `MRN-URS-ETMF-001` v1.2 — providing the DIA TMF Reference Model v3.3.1–aligned, inspection-ready electronic Trial Master File for clinical studies under ICH E6(R3), EU CTR 536/2014, and FDA BIMO.

## 2. Scope

Per the URS: Vault eTMF 24R3 multi-tenant SaaS, per-study + per-country + per-site TMF instances, DIA TMFR v3.3.1 classification, Real-Time TMF (RTMF) operating model, Inspection-Readiness dashboard, e-signature workflows (Form 1572, FDF, ICF, IRB/IEC, milestones), CTIS submission pack export, FDA BIMO inspection-readiness, sponsor/CRO co-management, legacy migration. Integrations: Okta SSO/MFA; Vault Connect → Vault CTMS (Dryad), Vault QualityDocs (Vellis), Vault RIM (Nimbus); Medidata Rave (Marigold) study-build feed; Cornerstone (Vega) read-and-understood trigger; Sirius Argus PV cross-reference; Iolanthe Clinical ePRO study-build deposit.

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | GAMP Cat | Notes |
|---|---|---|---|
| C-01 | Vault eTMF 24R3 tenancy | 4 | Multi-tenant SaaS; sponsor-side TMF |
| C-02 | Okta IdP | infra | SAML 2.0 + MFA |
| C-03 | Vault CTMS (Dryad) | 4 | Study + site + investigator metadata |
| C-04 | Vault QualityDocs (Vellis) | 4 | Controlled procedures + SOPs |
| C-05 | Vault RIM (Nimbus) | 4 | Regulatory submission cross-reference |
| C-06 | Medidata Rave EDC (Marigold) | 4 | Study-build artefact feed |
| C-07 | Cornerstone LMS (Vega) | 4 | Read-and-understood trigger |
| C-08 | Sirius Argus PV | 4 | Safety-letter cross-reference |
| C-09 | Clario eCOA (Iolanthe) | 4 | ePRO study-build deposit |
| C-10 | Inspector Portal | 4 | Read-only external workspace |

### 3.2 Logical Architecture

```
                  Okta SSO + MFA                       Inspector Portal
                       │                                     │
                       ▼                                     ▼
   ┌─────────────────────────────────────────────────────────────────┐
   │       Vault eTMF 24R3 (Marinos Therapeutics tenancy)             │
   │   DIA TMF Reference Model v3.3.1 (Zones 01-11 + Sections +       │
   │   Artefacts + Sub-artefacts)                                     │
   │   Per-study TMF + per-country binders + per-site binders + ISF   │
   │   mirror                                                          │
   │   Document lifecycle (DRAFT → IN-REVIEW → APPROVED → FILED-FINAL │
   │   → SUPERSEDED → ARCHIVED) + e-sig workflows (1572, FDF, ICF,    │
   │   IRB/IEC, milestone sign-off)                                    │
   │   CTQ metrics + RTMF dashboard + Inspection-Readiness +          │
   │   CTIS submission pack + FDA BIMO export                          │
   └─┬──────────┬──────────┬──────────┬──────────┬──────────┬──────────┘
     │          │          │          │          │          │
     ▼          ▼          ▼          ▼          ▼          ▼
   Vault     Vault       Vault       Medidata   Cornerstone Sirius
   CTMS      QualityDocs RIM         Rave EDC    LMS         Argus
   (Dryad)   (Vellis)    (Nimbus)    (Marigold) (Vega)      PV
```

## 4. Functional Specifications

### 4.1 Vendor / Platform Assurance

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VND-01 | URS-VND-01 | Vendor-assurance dossier holds SOC 2 Type II (current), ISO/IEC 27001:2022 cert, Veeva CSV summary for 24R3, HIPAA evidence where applicable; annual re-qualification gate. |
| FS-VND-02 | URS-VND-02 | Release-note workflow: vendor RNS feed → vendor-assurance owner → impact-assessment template → change-control record within 14 days. |
| FS-VND-03 | URS-VND-03 | Vendor SDLC evidence (validation approach + OQ/PQ deliverables + change-control logs) reviewed annually; checklist in `/vendor-assurance/veeva/`. |
| FS-VND-04 | URS-VND-04 | Vendor sub-processor list reviewed quarterly via DPA Annex II; new sub-processors trigger DPIA delta-review. |
| FS-VND-05 | URS-VND-05 | SLA report reviewed quarterly; breaches logged in vendor-assurance dossier + eQMS deviation. |

### 4.2 DIA TMF Reference Model 3.3.1

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TMFR-01 | URS-TMFR-01 | TMFR v3.3.1 Zones 01-11 configured as the top-level metadata schema; zone codes match the published taxonomy. |
| FS-TMFR-02 | URS-TMFR-02 | TMFR Sections + Artefacts configured per v3.3.1; deviations documented in `/config/tmfr-3-3-1-deviations.md`. |
| FS-TMFR-03 | URS-TMFR-03 | TMFR version-migration playbook preserves historical classifications via the Vault `legacy_classification` field. |
| FS-TMFR-04 | URS-TMFR-04 | Sub-artefacts available where v3.3.1 distinguishes them; UI shows zone → section → artefact → sub-artefact pickers. |
| FS-TMFR-05 | URS-TMFR-05 | Per-study TMF Index derived from master taxonomy with filters: Phase, indication, regions, IMP class. |
| FS-TMFR-06 | URS-TMFR-06 | Database constraint: `classification_zone_id` + `classification_section_id` + `classification_artefact_id` mandatory at FILED-FINAL transition. |

### 4.3 Document Lifecycle and Versioning

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DOC-01 | URS-DOC-01 | Lifecycle state machine: DRAFT → IN-REVIEW → APPROVED → FILED-FINAL → SUPERSEDED → ARCHIVED; only FILED-FINAL + ARCHIVED count toward Completeness. |
| FS-DOC-02 | URS-DOC-02 | Lifecycle transitions wired to e-sig workflow with SoD enforcement (FS-SOD-01). |
| FS-DOC-03 | URS-DOC-03 | FILED-FINAL records flagged immutable at DB layer; revision creates a new record in DRAFT state. |
| FS-DOC-04 | URS-DOC-04 | Version sequence monotonic per artefact-instance via DB unique constraint + sequence trigger. |
| FS-DOC-05 | URS-DOC-05 | PDF/A-3 rendition auto-generated on FILED-FINAL transition; native format retained as Original. |
| FS-DOC-06 | URS-DOC-06 | Classification metadata schema: zone, section, artefact, sub-artefact, country, site, study, milestone, document_date, effective_date. |
| FS-DOC-07 | URS-DOC-07 | Reason-for-change captured at every revision after first FILED-FINAL; controlled vocabulary (Editorial / Substantive / Regulatory). |
| FS-DOC-08 | URS-DOC-08 | Bulk re-classification via authenticated API or batch tool with per-item audit; manual UI limited to 50 items per action. |

### 4.4 Document Type Library + EDL

| FS ID | URS ID | Specification |
|---|---|---|
| FS-EDL-01 | URS-EDL-01 | Master Document Type Library aligned with TMFR v3.3.1; extensions approved by Director TMF Ops + Head of GCP Compliance via workflow. |
| FS-EDL-02 | URS-EDL-02 | Per-study EDL template = master + study-specific artefact overlays; configurable in DEV → UAT → PROD. |
| FS-EDL-03 | URS-EDL-03 | Per-country EDL overlays for US (FDA Form 1572, FDF), DE (BfArM + PEI), CH (Swissmedic), AT (AGES); driven by country-attribute. |
| FS-EDL-04 | URS-EDL-04 | Per-site EDL overlays for site initiation / activation / closure artefact sets. |
| FS-EDL-05 | URS-EDL-05 | Per-milestone EDL filters: FPI, LPI, LPO, DBL, CSR, Archive — selectable in dashboard view. |
| FS-EDL-06 | URS-EDL-06 | Mid-study EDL changes go through impact-assessment workflow; retrospective changes require Study TMF Owner + GCP Compliance approval. |

### 4.5 Per-Country and Per-Site Binders + ISF Mirror

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BIND-01 | URS-BIND-01 | Per-country binder view aggregates trial-level + country-regulatory artefacts; country-flag-driven filtering. |
| FS-BIND-02 | URS-BIND-02 | Per-site binder view aggregates site-specific subset (Form 1572, FDF, CVs, site-IRB, ICF version log, delegation log, monitoring visits). |
| FS-BIND-03 | URS-BIND-03 | ISF mirror view exposes sponsor-side records mirroring the site-held ISF; mirror-status indicator per artefact (mirrored / pending / discrepant). |
| FS-BIND-04 | URS-BIND-04 | ISF mirror discrepancy report generated per monitoring visit; CRA reconciles against on-site walk-through. |
| FS-BIND-05 | URS-BIND-05 | Country / site binder PDF/A-3 export ≤ 4 business hours per inspection-readiness request. |

### 4.6 Completeness, Timeliness, Quality + RTMF

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CTQ-01 | URS-CTQ-01 | Completeness calculation: FILED-FINAL EDL artefacts / total required EDL artefacts; broken out per country + per site. |
| FS-CTQ-02 | URS-CTQ-02 | Timeliness calculation: event-timestamp → FILED-FINAL timestamp diff vs per-artefact SLA; configurable SLAs (safety letter 5BD, site-initiation pack 10BD, protocol amendment 15BD). |
| FS-CTQ-03 | URS-CTQ-03 | Quality calculation: rejected-on-first-review count / total reviews; rolling 90-day window. |
| FS-CTQ-04 | URS-CTQ-04 | Inspection-Ready gate: Completeness ≥ 95% AND Timeliness P95 within SLA AND Quality first-pass ≥ 90%; configurable thresholds; gate is workflow-enforced. |
| FS-CTQ-05 | URS-CTQ-05 | RTMF dashboard highlights overdue artefacts (red), at-risk (amber), on-track (green); refresh ≤ 5 min. |
| FS-CTQ-06 | URS-CTQ-06 | Feed-delay alerting: source-system event vs eTMF filing time-diff exceeds 24h (safety) or 5BD (standard) triggers alert to Director TMF Ops. |
| FS-CTQ-07 | URS-CTQ-07 | TMF Health Metrics report scheduled weekly + at milestones; Study TMF Owner sign-off workflow. |
| FS-CTQ-08 | URS-CTQ-08 | Forecast model projects Completeness at upcoming milestone based on current filing velocity; > 15% projected miss raises flag. |

### 4.7 Electronic Signatures and 21 CFR Part 11

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Procedural controls SOP linked from system documentation; annual review cadence. |
| FS-PART11-02 | URS-PART11-02 | Export engine produces PDF/A-3 + XML/JSON with classification + lifecycle history; tested under OQ. |
| FS-PART11-03 | URS-PART11-03 | Retention policy ≥ 25 y enforced via lifecycle ARCHIVED state with retention-clock; cryptographic-integrity verified on retrieval. |
| FS-PART11-04 | URS-PART11-04 | Access control via Okta SAML 2.0 + MFA; service accounts via mTLS; role-based authorisation tested under OQ. |
| FS-PART11-05 | URS-PART11-05 | Audit-trail schema captures actor + action + timestamp + prior + new + reason for the 8 event classes (filing, classification, lifecycle, signature, configuration, role assignment, EDL change, deletion attempts). |
| FS-PART11-06 | URS-PART11-06 | Authority-check middleware blocks out-of-role requests at API gateway; UI hides unauthorised actions; both verified under OQ. |
| FS-PART11-07 | URS-PART11-07 | Manual versioning under change control; effective manuals trigger Cornerstone read-and-understood tasks (FS-INT-LMS-01). |
| FS-PART11-08 | URS-PART11-08 | Inspector-portal endpoints serve short-lived tokens (15 min); IP allow-list when contracted; TLS 1.3 mandatory. |
| FS-PART11-09 | URS-PART11-09 | E-signature manifestation in PDF/A-3 shows printed name + date/time (ISO 8601 + TZ) + meaning-of-signature string. |
| FS-PART11-10 | URS-PART11-10 | HMAC-SHA256 record-hash + signer-id + timestamp binding; tamper-detect alert on read where verification fails. |
| FS-PART11-11 | URS-PART11-11 | Unique signature-id per user enforced via Okta uniqueness + Vault user-record constraint; deactivated users retain ID, never reassigned. |
| FS-PART11-12 | URS-PART11-12 | Re-authentication required at sign-events for 1572, FDF, ICF approval, milestone sign-off; max-age 5 min OAuth2 token; cached creds rejected. |
| FS-PART11-13 | URS-PART11-13 | Password / credential policy: MFA mandatory, lockout 5 fails / 15 min, complexity per ISO 27001 baseline. |
| FS-SOD-01 | URS-SOD-01 | SoD rules: filer.user_id ≠ reviewer.user_id ≠ approver.user_id of the same document_revision_id; DB constraint + workflow gate. |
| FS-SOD-02 | URS-SOD-02 | Vault Admin role permission matrix excludes file / review / approve actions; OQ verifies. |
| FS-SOD-03 | URS-SOD-03 | CRO Liaison closeout actions require sponsor co-signature; workflow-enforced. |

### 4.8 eSignature Workflows

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ESW-01 | URS-ESW-01 | Form 1572 workflow: investigator + sub-investigator e-sig + dates; § 11.50 / .70 / .200 controls; archived in Zone 05 (Site Management). |
| FS-ESW-02 | URS-ESW-02 | FDF workflow per 21 CFR Part 54: investigator + sub-investigator + annual re-confirmation reminder; archived in Zone 05. |
| FS-ESW-03 | URS-ESW-03 | ICF versioning: per-language + per-country variants linked under a common ICF parent; CURRENT flag per site / date-range single-valued. |
| FS-ESW-04 | URS-ESW-04 | IRB/IEC approval workflow with expiry date; D-30 + D-7 + D-0 alerts; lapse blocks new consent submissions in dependent sites. |
| FS-ESW-05 | URS-ESW-05 | Protocol amendment workflow: EDL refresh + per-country impact assessment + LMS read-and-understood task creation. |

### 4.9 Quality Review and Completeness Checking

| FS ID | URS ID | Specification |
|---|---|---|
| FS-QC-01 | URS-QC-01 | Quality Review queue UI filterable by artefact-type + country + site + CRO + filer; SLA-driven priority. |
| FS-QC-02 | URS-QC-02 | Configurable rule engine: signature presence, date validity, country-flag consistency, IRB/IEC version-match; per-artefact rule sets. |
| FS-QC-03 | URS-QC-03 | Completeness-check rules versioned in `/config/edl-rules/`; per-artefact gating logic; rule evaluations audit-trailed. |
| FS-QC-04 | URS-QC-04 | Reject-code vocabulary in `/config/qc-reject-codes.yml`; reject without code blocked at workflow. |
| FS-QC-05 | URS-QC-05 | Quarterly calibration session: 30-document blind sample reviewed by all reviewers; agreement-metric tracked. |

### 4.10 TMF Health Metrics and Inspection-Readiness

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INSP-01 | URS-INSP-01 | Inspection-Readiness dashboard widget per study: Completeness % + Timeliness P95 + Quality first-pass + last-review-date + open-deviation count. |
| FS-INSP-02 | URS-INSP-02 | Inspection-Readiness export pipeline produces PDF/A-3 + machine-readable index (JSON) + classification matrix; ≤ 4 BH SLA. |
| FS-INSP-03 | URS-INSP-03 | Inspector workspace provisioning: time-bounded (30d default), watermarked downloads, audit-trailed activity, separate access-zone. |
| FS-INSP-04 | URS-INSP-04 | Dashboard flags: overdue artefacts (red), expiring IRB/IEC < 30d, expiring ICF < 30d, expiring investigator credentials (CV, GCP training, license). |
| FS-INSP-05 | URS-INSP-05 | FDA BIMO pack: site-selection rationale + CRA visit reports + deviation logs + SDV evidence cross-link to Medidata Rave. |
| FS-INSP-06 | URS-INSP-06 | EU CA pack (BfArM / PEI / Swissmedic / AGES): CTIS-routed submission references + EU CTR Art. 56-58 archive provenance + EudraVigilance cross-link. |

### 4.11 CTIS Submission Pack

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CTIS-01 | URS-CTIS-01 | CTIS pack export builder produces EU CTR Art. 25 + Art. 81 compatible packages; output validated against current CTIS schema in CI. |
| FS-CTIS-02 | URS-CTIS-02 | CTIS pack assembly from Zone 01 (protocol) + Zone 02 (IB, IMPD) + Zone 03 (application form, GMP statement) + Zone 04 (IRB/IEC approvals); missing-required block. |
| FS-CTIS-03 | URS-CTIS-03 | CTIS pack version history retained; cross-link to Vault RIM submission record. |

### 4.12 Audit Trail / ALCOA+

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit-trail captures every filing + classification + lifecycle + signature + config + role + EDL event; append-only DB. |
| FS-AUD-02 | URS-AUD-02 | Tenant Admin permissions exclude UPDATE / DELETE on audit-trail rows; verified by OQ + annual access review. |
| FS-AUD-03 | URS-AUD-03 | Monthly audit-trail review by Director TMF Ops + milestone sampling per study; review evidence in `/reviews/audit/`. |
| FS-AUD-04 | URS-AUD-04 | Retention clock ≥ 25 y post-trial completion; longer per 21 CFR § 312.62 where US-IND active. |
| FS-AUD-05 | URS-AUD-05 | Audit-trail export cryptographically signed by platform; signature verifiable via published Veeva public key. |
| FS-DI-01 | URS-DI-01 | Every event row carries actor_id (user or service-account); anonymous accounts prohibited; OQ verifies. |
| FS-DI-02 | URS-DI-02 | Export engine produces PDF/A-3 + XML/JSON; legibility verified by OQ rendering test. |
| FS-DI-03 | URS-DI-03 | Server-side NTP-synced timestamps authoritative; retroactive-filing flag + delay-reason required. |
| FS-DI-04 | URS-DI-04 | Raw upload stored in immutable bucket; renditions reference but never overwrite Original. |
| FS-DI-05 | URS-DI-05 | CTQ calculations deterministic; reference-implementation in `/src/ctq/`; OQ comparison test. |
| FS-DI-06 | URS-DI-06 | Retention enforced + retrievability: routine ≤ 1 BD, inspection ≤ 4 BH; verified annually. |

### 4.13 Privacy — GDPR + HIPAA

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PRV-01 | URS-PRV-01 | Per-study lawful-basis register (Art. 6) maintained in `/governance/lawful-basis/`. |
| FS-PRV-02 | URS-PRV-02 | Patient data pseudonymisation enforced via subject-ID mapping; re-identification only via EDC. |
| FS-PRV-03 | URS-PRV-03 | TLS 1.3 in transit + AES-256 at rest; vendor evidence on file. |
| FS-PRV-04 | URS-PRV-04 | DPIA URN field per study; verified at study-build approval workflow. |
| FS-PRV-05 | URS-PRV-05 | HIPAA BAA with Veeva executed; tracked in vendor-assurance dossier. |
| FS-PRV-06 | URS-PRV-06 | Cross-border transfer routes documented per study via SCCs + supplementary measures; annual review. |

### 4.14 Integrations

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-CTMS-01 | URS-INT-CTMS-01 | Bidirectional sync with Vault CTMS via Vault Connect; CTMS authoritative for operational metadata; conflict-resolution rule documented. |
| FS-INT-EDC-01 | URS-INT-EDC-01 | Auto-file from Medidata Rave at protocol amendment + DBL milestones; payload includes eCRF library, edit-check spec, blank CRF, CCG. |
| FS-INT-RIM-01 | URS-INT-RIM-01 | Cross-link from Vault RIM via Vault Connect; eCTD sequence-ID visible on regulatory artefacts. |
| FS-INT-EDMS-01 | URS-INT-EDMS-01 | Vault QualityDocs cross-reference URNs displayed in document metadata. |
| FS-INT-LMS-01 | URS-INT-LMS-01 | On QualityDocs effective-date for CRA-impacting SOPs, REST event to Cornerstone creates read-and-understood tasks. |
| FS-INT-PV-01 | URS-INT-PV-01 | Sirius Argus case-ID cross-link visible on Zone 07 safety-letter artefacts. |
| FS-INT-EPRO-01 | URS-INT-EPRO-01 | Iolanthe Clinical ePRO auto-deposit study-build artefacts on approval. |
| FS-INT-SSO-01 | URS-INT-SSO-01 | Okta SAML 2.0 + MFA + SCIM 2.0 provisioning; service-accounts via mTLS. |
| FS-INT-API-01 | URS-INT-API-01 | Vault Connect OAuth 2.0 client-credentials; short-lived tokens (15 min); CAB approval for service-account changes. |

### 4.15 Performance, Availability, Backup

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | Document-open + list-view P95 ≤ 3 s at 10k concurrent / 250 active studies; performance test under PQ. |
| FS-PERF-02 | URS-PERF-02 | Inspection-export 100k-document study ≤ 4 h; chunked + parallel export pipeline. |
| FS-PERF-03 | URS-PERF-03 | EDL batch re-evaluation across 250 studies ≤ 30 min; scheduled nightly. |
| FS-AV-01 | URS-AV-01 | Veeva SLA: 99.5% normal, 99.9% sponsor-critical windows; ≥ 14 d advance notice for maintenance. |
| FS-BAK-01 | URS-BAK-01 | Vendor backup with daily integrity verify; site verifies RPO ≤ 4 h / RTO ≤ 24 h annually. |
| FS-BAK-02 | URS-BAK-02 | Tenant export to cold storage ≥ 25 y; annual restoration drill. |
| FS-BAK-03 | URS-BAK-03 | Annual Veeva DR test; site reviews report. |

### 4.16 Security

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SEC-01 | URS-SEC-01 | TLS 1.3 + AES-256; vendor cert verified annually. |
| FS-SEC-02 | URS-SEC-02 | Per-study + per-country access controls configurable; CRO scoped per contract; role-matrix in `/config/security/`. |
| FS-SEC-03 | URS-SEC-03 | Vendor SOC 2 + ISO 27001 evidence reviewed annually; gaps to change control. |
| FS-SEC-04 | URS-SEC-04 | Annual pen-test sponsor + inspector endpoints; H/C findings remediated ≤ 30 d. |
| FS-SEC-05 | URS-SEC-05 | Inspector credentials time-bounded (30 d default); revocable on demand. |

### 4.17 Sponsor + CRO Co-Management

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CRO-01 | URS-CRO-01 | Per-CRO scoped access via Vault security profile; per-protocol delegation matrix; sponsor-oversight dashboards. |
| FS-CRO-02 | URS-CRO-02 | CRO transition workflow: hand-over checklist, sponsor sign-off, audit-trail preservation. |
| FS-CRO-03 | URS-CRO-03 | Per-CRO quality dashboard (Completeness + Timeliness + Quality + Deviation count). |
| FS-CRO-04 | URS-CRO-04 | CRO-contracted scope reflected in role-permission matrix; out-of-scope blocked at workflow gate. |

### 4.18 Legacy Migration

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MIG-01 | URS-MIG-01 | Migration pipeline preserves Original + applied signatures + original metadata + RFC history; audit-trailed per item. |
| FS-MIG-02 | URS-MIG-02 | Per-study migration verification report: sampled equivalence + metadata-completeness checks; Director TMF Ops + Head of QA approval. |
| FS-MIG-03 | URS-MIG-03 | Migration-specialist role provisioned with expiry-date attribute; auto-revoked at window close. |
| FS-MIG-04 | URS-MIG-04 | Migration discrepancies opened as eQMS deviations; tracked through to closure. |

### 4.19 Document Expiry, Obsolescence, Effective-Date

| FS ID | URS ID | Specification |
|---|---|---|
| FS-EXP-01 | URS-EXP-01 | Expiry-tracking schema on IRB/IEC, ICF, investigator credentials, IB, IMPD; expiry-date attribute mandatory. |
| FS-EXP-02 | URS-EXP-02 | D-30 flag + expired-blocks-workflow logic; site-activation blocked when site IRB expired. |
| FS-EXP-03 | URS-EXP-03 | ICF CURRENT flag per site + date-range single-valued; superseded ICFs read-only. |
| FS-EXP-04 | URS-EXP-04 | Obsolescence workflow moves SUPERSEDED to historical view while preserving retrievability. |

### 4.20 Multi-language + Per-Country Variant

| FS ID | URS ID | Specification |
|---|---|---|
| FS-LANG-01 | URS-LANG-01 | Language-locale metadata field per document; ISO 639-1 + ISO 3166-1 alpha-2 (e.g., de-DE, de-AT, de-CH). |
| FS-LANG-02 | URS-LANG-02 | Sibling-link relationship between parent + per-country variants; preserved through revisions. |
| FS-LANG-03 | URS-LANG-03 | Translation provenance metadata (translator, back-translator, certification-evidence URN) filed alongside translated artefact. |
| FS-LANG-04 | URS-LANG-04 | Per-country submission variant selectable in Inspection-Readiness export. |

### 4.21 Investigator + Site Closeout

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CLS-01 | URS-CLS-01 | Closeout EDL: final monitoring visit report, drug accountability log, sample disposition, site-archive cert, IP destruction cert. |
| FS-CLS-02 | URS-CLS-02 | Investigator + sponsor closeout sign-off e-sig per § 11.50 / .70. |
| FS-CLS-03 | URS-CLS-03 | Archive-transition workflow: freeze TMF index, generate SHA-256 archive manifest, long-term-retention package. |
| FS-CLS-04 | URS-CLS-04 | Archive package PDF/A-3 + machine-readable index; annual integrity check. |

### 4.22 Inspector Portal

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INSP-PORTAL-01 | URS-INSP-PORTAL-01 | Inspector workspace: read-only, watermarked downloads, 30-d default validity. |
| FS-INSP-PORTAL-02 | URS-INSP-PORTAL-02 | Inspector activity audit-trailed under § 11.10(e). |
| FS-INSP-PORTAL-03 | URS-INSP-PORTAL-03 | Inspector traffic tagged for security-monitoring separation. |

### 4.23 Reporting and Search

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RPT-01 | URS-RPT-01 | Full-text search engine respects access-control scopes. |
| FS-RPT-02 | URS-RPT-02 | Saved-search registry shareable per role; config audit-trailed. |
| FS-RPT-03 | URS-RPT-03 | Standard report library: TMF Health, Country Completeness, Site Completeness, CRO Quality, Overdue, Expiring, Audit Review. |
| FS-RPT-04 | URS-RPT-04 | Ad-hoc report builder available to Study TMF Owner + Inspection Coordinator. |
| FS-RPT-05 | URS-RPT-05 | Per-Zone (TMFR 01-11) Completeness sub-reports drillable from TMF Health. |
| FS-RPT-06 | URS-RPT-06 | Standard report rendering ≤ 5 min across 250 studies. |

### 4.24 Notifications and Alerts

| FS ID | URS ID | Specification |
|---|---|---|
| FS-NOT-01 | URS-NOT-01 | Role-targeted email + in-app notifications via notification-service; configurable templates. |
| FS-NOT-02 | URS-NOT-02 | Cadence + thresholds per role + per study; config audit-trailed. |
| FS-NOT-03 | URS-NOT-03 | Bounce handling escalates after 3 consecutive failures. |
| FS-NOT-04 | URS-NOT-04 | Inspection-imminent dashboard mode prioritises overdue artefacts. |

### 4.25 Configuration Management and Change Control

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CCM-01 | URS-CCM-01 | DEV → UAT → PROD promotion workflow with SoD-enforced approvals; PROD requires change-record reference. |
| FS-CCM-02 | URS-CCM-02 | Configuration baselines versioned in `/config/baselines/`; baseline-diff tool detects drift. |
| FS-CCM-03 | URS-CCM-03 | Emergency-change post-implementation review ≤ 5 BD. |
| FS-CCM-04 | URS-CCM-04 | Vendor release impact-assessment ≤ 14 d; tracked in `/vendor-assurance/`. |

### 4.26 Training and Periodic Review

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Cornerstone-recorded role-specific training; pre-production access gate; ICH E6(R3) currency check. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher curriculum `ETMF-2026-ANNUAL`: ICH E6(R3) updates, TMFR taxonomy changes, vendor release impact, BIMO + CTIS practice. |
| FS-PR-01 | URS-PR-01 | Annual Periodic Review template signed by Director TMF Operations + Head of GCP Compliance + Head of QA + VP Clinical Operations. |


### 4.27 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: SAML 2.0 via Entra ID with SCIM lifecycle provisioning. Conditional-access binding to policy `Clinical-Sensitive Conditional Access (FIDO2 phishing-resistant MFA + sponsor-tenant isolation)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the metadata DB plus object-replica for TMF binaries; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.28 Cross-System Integration — Helios handover (M-XINT-HEL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HEL-01 | URS-XINT-HEL-01 | Audit-event publisher emits Kafka topic `helios.ingest.marinos.etmf.v1` with schema-registry-pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`; at-least-once delivery; idempotency key `{source_system, event_id}`; back-pressure surfaced via Prometheus `helios_publish_lag_seconds` with 5-min alert at > 600 s. |
| FS-XINT-HEL-02 | URS-XINT-HEL-02 | Local audit-store retention policy enforces ≥ 25 y; Helios ack persisted as `helios_ack_ts` per event; periodic reconciliation job verifies parity (Helios row count == local published count) and raises a deviation in MasterControl on > 0.01% mismatch over a 24 h window. |


### 4.29 Cross-System Integration — EDMS handover (M-XINT-EDMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-EDMS-01 | URS-XINT-EDMS-01 | EDMS read adapter `MRN-EDMS-READ-1.x` performs `GET /docs/{doc_id}?version=effective`; supersession detected via EDMS event `vellis.doc.superseded.v1`; eTMF auto-flags affected sections for re-link review. |


### 4.30 Cross-System Integration — LMS handover (M-XINT-LMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-LMS-01 | URS-XINT-LMS-01 | LMS-competence adapter `<sys>-LMS-CLIENT-1.x` performs `GET /lms/competence/{user_id}?curriculum=...` over mTLS + Entra workload-identity; cache TTL per system (12-24 h); on `current=false` the consumer blocks the gated action and records `lms_lapse_user={user_id}` in the consumer audit trail; periodic reconciliation job verifies that no gated action proceeded with a lapsed competence. |

## 5. Configuration Items (CI)

| CI ID | Item | Value |
|---|---|---|
| CI-01 | TMF taxonomy | DIA TMF Reference Model v3.3.1 |
| CI-02 | Lifecycle states | DRAFT, IN-REVIEW, APPROVED, FILED-FINAL, SUPERSEDED, ARCHIVED |
| CI-03 | Inspection-Ready gate | Completeness ≥ 95% AND Timeliness P95 within SLA AND Quality ≥ 90% |
| CI-04 | Timeliness SLA (safety letter) | 5 business days |
| CI-05 | Timeliness SLA (site-initiation pack) | 10 business days |
| CI-06 | Timeliness SLA (protocol amendment) | 15 business days |
| CI-07 | Inspector credential validity | 30 days (configurable per inspection) |
| CI-08 | Bulk re-classification UI cap | 50 items / action |
| CI-09 | Re-auth max-age (signing) | 5 minutes |
| CI-10 | Account lockout | 5 failures / 15 minutes |
| CI-11 | DR test cadence | Annual |
| CI-12 | Audit-trail review cadence | Monthly + milestone sampling |
| CI-13 | Periodic Review cadence | Annual |
| CI-14 | Retention | ≥ 25 years post-trial completion |
| CI-15 | TMFR Zones | 01-11 per v3.3.1 |
| CI-16 | DACH language variants | de-DE, de-AT, de-CH (separate locale codes) |
| CI-17 | DPIA requirement | Per study before EU enrolment |
| CI-18 | CTIS pack schema | Current CTIS technical specification |

## 6. Risks (FS-level)

URS § 9 documents R-01..R-12. Additional FS-level risks:

- TMFR v3.3.1 → v4 migration (~2027) breaks historical classifications → mitigation: legacy_classification preservation field + per-Zone migration playbook (FS-TMFR-03).
- Vault Connect outage delays CTMS metadata sync → mitigation: reconciliation queue + manual override (FS-INT-CTMS-01).
- CRO security-profile mis-scoping leaks cross-CRO data → mitigation: quarterly access review + automated profile diff (FS-CRO-01).
- CTIS schema version drift breaks pack export → mitigation: CI contract test against published schema (FS-CTIS-01).
- Real-Time TMF dashboard staleness from feed-delay → mitigation: feed-delay alert (FS-CTQ-06).
- Inspector-portal credential phishing → mitigation: short-lived tokens + IP allow-list + watermarked downloads (FS-PART11-08, FS-INSP-PORTAL-01).

## 7. References

- MRN-URS-ETMF-001 v1.2 (parent URS)
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- 21 CFR Parts 312 + 314 + 54
- FDA *Computerized Systems Used in Clinical Investigations* (2007)
- FDA BIMO Program
- ICH E6(R3) — Good Clinical Practice (Step 4, 6 January 2025)
- EU CTR 536/2014 Arts. 25/56/57/58/71/81
- EMA TMF Guideline Rev 2 (EMA/INS/GCP/856758/2018 Rev 2)
- DIA TMF Reference Model v3.3.1 (CDISC, 2023)
- EU GMP Annex 11 §§ 4, 6, 9, 11
- GDPR Arts. 6, 9, 32, 35
- ISPE GAMP 5 (2nd Edition, 2022)
- PIC/S PI 041
- ISO/IEC 27001:2022
- Veeva — *Vault eTMF 24R3 Validation Approach* + *24R3 Configuration Reference*

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-VND-01 | FS-VND-01 |
| URS-VND-02 | FS-VND-02 |
| URS-VND-03 | FS-VND-03 |
| URS-VND-04 | FS-VND-04 |
| URS-VND-05 | FS-VND-05 |
| URS-TMFR-01 | FS-TMFR-01 |
| URS-TMFR-02 | FS-TMFR-02 |
| URS-TMFR-03 | FS-TMFR-03 |
| URS-TMFR-04 | FS-TMFR-04 |
| URS-TMFR-05 | FS-TMFR-05 |
| URS-TMFR-06 | FS-TMFR-06 |
| URS-DOC-01 | FS-DOC-01 |
| URS-DOC-02 | FS-DOC-02 |
| URS-DOC-03 | FS-DOC-03 |
| URS-DOC-04 | FS-DOC-04 |
| URS-DOC-05 | FS-DOC-05 |
| URS-DOC-06 | FS-DOC-06 |
| URS-DOC-07 | FS-DOC-07 |
| URS-DOC-08 | FS-DOC-08 |
| URS-EDL-01 | FS-EDL-01 |
| URS-EDL-02 | FS-EDL-02 |
| URS-EDL-03 | FS-EDL-03 |
| URS-EDL-04 | FS-EDL-04 |
| URS-EDL-05 | FS-EDL-05 |
| URS-EDL-06 | FS-EDL-06 |
| URS-BIND-01 | FS-BIND-01 |
| URS-BIND-02 | FS-BIND-02 |
| URS-BIND-03 | FS-BIND-03 |
| URS-BIND-04 | FS-BIND-04 |
| URS-BIND-05 | FS-BIND-05 |
| URS-CTQ-01 | FS-CTQ-01 |
| URS-CTQ-02 | FS-CTQ-02 |
| URS-CTQ-03 | FS-CTQ-03 |
| URS-CTQ-04 | FS-CTQ-04 |
| URS-CTQ-05 | FS-CTQ-05 |
| URS-CTQ-06 | FS-CTQ-06 |
| URS-CTQ-07 | FS-CTQ-07 |
| URS-CTQ-08 | FS-CTQ-08 |
| URS-PART11-01 | FS-PART11-01 |
| URS-PART11-02 | FS-PART11-02 |
| URS-PART11-03 | FS-PART11-03 |
| URS-PART11-04 | FS-PART11-04 |
| URS-PART11-05 | FS-PART11-05 |
| URS-PART11-06 | FS-PART11-06 |
| URS-PART11-07 | FS-PART11-07 |
| URS-PART11-08 | FS-PART11-08 |
| URS-PART11-09 | FS-PART11-09 |
| URS-PART11-10 | FS-PART11-10 |
| URS-PART11-11 | FS-PART11-11 |
| URS-PART11-12 | FS-PART11-12 |
| URS-PART11-13 | FS-PART11-13 |
| URS-SOD-01 | FS-SOD-01 |
| URS-SOD-02 | FS-SOD-02 |
| URS-SOD-03 | FS-SOD-03 |
| URS-ESW-01 | FS-ESW-01 |
| URS-ESW-02 | FS-ESW-02 |
| URS-ESW-03 | FS-ESW-03 |
| URS-ESW-04 | FS-ESW-04 |
| URS-ESW-05 | FS-ESW-05 |
| URS-QC-01 | FS-QC-01 |
| URS-QC-02 | FS-QC-02 |
| URS-QC-03 | FS-QC-03 |
| URS-QC-04 | FS-QC-04 |
| URS-QC-05 | FS-QC-05 |
| URS-INSP-01 | FS-INSP-01 |
| URS-INSP-02 | FS-INSP-02 |
| URS-INSP-03 | FS-INSP-03 |
| URS-INSP-04 | FS-INSP-04 |
| URS-INSP-05 | FS-INSP-05 |
| URS-INSP-06 | FS-INSP-06 |
| URS-CTIS-01 | FS-CTIS-01 |
| URS-CTIS-02 | FS-CTIS-02 |
| URS-CTIS-03 | FS-CTIS-03 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
| URS-AUD-05 | FS-AUD-05 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-PRV-01 | FS-PRV-01 |
| URS-PRV-02 | FS-PRV-02 |
| URS-PRV-03 | FS-PRV-03 |
| URS-PRV-04 | FS-PRV-04 |
| URS-PRV-05 | FS-PRV-05 |
| URS-PRV-06 | FS-PRV-06 |
| URS-INT-CTMS-01 | FS-INT-CTMS-01 |
| URS-INT-EDC-01 | FS-INT-EDC-01 |
| URS-INT-RIM-01 | FS-INT-RIM-01 |
| URS-INT-EDMS-01 | FS-INT-EDMS-01 |
| URS-INT-LMS-01 | FS-INT-LMS-01 |
| URS-INT-PV-01 | FS-INT-PV-01 |
| URS-INT-EPRO-01 | FS-INT-EPRO-01 |
| URS-INT-SSO-01 | FS-INT-SSO-01 |
| URS-INT-API-01 | FS-INT-API-01 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-PERF-03 | FS-PERF-03 |
| URS-AV-01 | FS-AV-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-BAK-03 | FS-BAK-03 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-SEC-05 | FS-SEC-05 |
| URS-CRO-01 | FS-CRO-01 |
| URS-CRO-02 | FS-CRO-02 |
| URS-CRO-03 | FS-CRO-03 |
| URS-CRO-04 | FS-CRO-04 |
| URS-MIG-01 | FS-MIG-01 |
| URS-MIG-02 | FS-MIG-02 |
| URS-MIG-03 | FS-MIG-03 |
| URS-MIG-04 | FS-MIG-04 |
| URS-EXP-01 | FS-EXP-01 |
| URS-EXP-02 | FS-EXP-02 |
| URS-EXP-03 | FS-EXP-03 |
| URS-EXP-04 | FS-EXP-04 |
| URS-LANG-01 | FS-LANG-01 |
| URS-LANG-02 | FS-LANG-02 |
| URS-LANG-03 | FS-LANG-03 |
| URS-LANG-04 | FS-LANG-04 |
| URS-CLS-01 | FS-CLS-01 |
| URS-CLS-02 | FS-CLS-02 |
| URS-CLS-03 | FS-CLS-03 |
| URS-CLS-04 | FS-CLS-04 |
| URS-INSP-PORTAL-01 | FS-INSP-PORTAL-01 |
| URS-INSP-PORTAL-02 | FS-INSP-PORTAL-02 |
| URS-INSP-PORTAL-03 | FS-INSP-PORTAL-03 |
| URS-RPT-01 | FS-RPT-01 |
| URS-RPT-02 | FS-RPT-02 |
| URS-RPT-03 | FS-RPT-03 |
| URS-RPT-04 | FS-RPT-04 |
| URS-RPT-05 | FS-RPT-05 |
| URS-RPT-06 | FS-RPT-06 |
| URS-NOT-01 | FS-NOT-01 |
| URS-NOT-02 | FS-NOT-02 |
| URS-NOT-03 | FS-NOT-03 |
| URS-NOT-04 | FS-NOT-04 |
| URS-CCM-01 | FS-CCM-01 |
| URS-CCM-02 | FS-CCM-02 |
| URS-CCM-03 | FS-CCM-03 |
| URS-CCM-04 | FS-CCM-04 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-HEL-01 | FS-XINT-HEL-01 |
| URS-XINT-HEL-02 | FS-XINT-HEL-02 |
| URS-XINT-EDMS-01 | FS-XINT-EDMS-01 |
| URS-XINT-LMS-01 | FS-XINT-LMS-01 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

The following risks are noted for downstream evaluation in the Risk Assessment.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Document Zone/Section/Artefact mis-classification at scale leading to inspection gap | Medium | High | URS-TMFR-06, URS-QC-01..05 |
| R-02 | Completeness-check false-pass (artefact present but wrong version / wrong country) | Medium | High | URS-QC-02, URS-QC-03, URS-CTQ-04 |
| R-03 | Real-Time TMF feed delay from CTMS / EDC causing stale completeness verdicts | Medium | Medium | URS-CTQ-06, URS-INT-CTMS-01, URS-INT-EDC-01 |
| R-04 | Investigator-site document expiry (IRB/IEC approval, ICF, CV, license) not flagged | Medium | High | URS-INSP-04, URS-ESW-04 |
| R-05 | Late filing causing GCP/BIMO finding | Medium | High | URS-CTQ-02, URS-CTQ-05 |
| R-06 | Audit-trail tampering on vendor side | Low | Critical | URS-AUD-02, URS-AUD-05, URS-VND-03 |
| R-07 | Signature compromise (cached credentials accepted at signing) | Low | Critical | URS-PART11-12, URS-INT-SSO-01 |
| R-08 | CTIS submission pack incompatibility with current CTIS schema | Medium | High | URS-CTIS-01, URS-CTIS-02 |
| R-09 | GDPR Art. 35 DPIA absent at EU enrolment start | Low | High | URS-PRV-04 |
| R-10 | CRO transition mid-study loses audit history | Low | High | URS-CRO-02 |
| R-11 | Legacy migration discrepancy not detected | Medium | High | URS-MIG-01, URS-MIG-02 |
| R-12 | TMFR v4 migration disrupts historical classification | Low | High | URS-TMFR-03 |

Full evaluation in `MRN-RA-ETMF-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
