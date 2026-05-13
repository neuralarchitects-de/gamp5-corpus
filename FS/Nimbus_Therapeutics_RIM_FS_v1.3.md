---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (FS catch-up to URS v1.2; full per-ID expansion of 107 URS-IDs; ICH M4/M8 explicit; IDMP ISO standards; EMA SPOR; FDA ESG; § 11 sub-section authority map)"
seed_corpus_basis:
  - "NIM-URS-RIM-001 v1.2 (parent URS)"
  - "ISPE GAMP 5 (2nd Edition, 2022) Cat 4 SaaS conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "ICH M2 ESTRI; ICH M4 CTD; ICH M8 eCTD"
  - "EMA EU Module 1; EMA Q&A on eCTD v4"
  - "IDMP ISO 11238 / 11239 / 11240 / 11615 / 11616"
  - "EMA SPOR (SMS / PMS / OMS / RMS)"
  - "FDA Electronic Submissions Gateway (ESG) Guidance"
  - "EU CTR 536/2014 Arts. 25, 81"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "GDPR Arts. 6, 32; ISO/IEC 27001:2022; PIC/S PI 041"
parent_urs:
  document_number: NIM-URS-RIM-001
  version: 1.2
  file: ../../URS/_generated/final/RIM_Regulatory_Information_Management__Nimbus_Therapeutics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# Functional Specification (FS)

## RIM — Veeva Vault RIM Suite 24R3 (Submissions + Registrations + Submissions Archive + IDMP)

**Document Number:** NIM-FS-RIM-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** NIM-URS-RIM-001 v1.2 | **Site:** Nimbus Therapeutics (fictional)
**System Class:** GAMP Cat 4 — Configured Product (multi-tenant SaaS)
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Parts 312 + 314; ICH M2 + M4 + M8; EMA Module 1 + Q&A eCTD v4; IDMP ISO 11238/11239/11240/11615/11616; EMA SPOR; FDA ESG; EU CTR 536/2014 Arts. 25/81; EU GMP Annex 11; GDPR Arts. 6, 32; ISO/IEC 27001:2022; PIC/S PI 041.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of Regulatory Operations) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Privacy / DPO) | _____________ | _____________ | _____ |
| Approver (VP Global Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue (partial; superseded). |
| 1.1 | 2026-05-08 | (synthetic) | Vendor version bump to 24R3. |
| 1.2 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.2: full per-ID expansion of 107 URS-IDs (no range compression per § 2A.7); ICH M4 + M8 explicit; IDMP ISO 11238/11239/11240/11615/11616; EMA SPOR; FDA ESG; § 11 sub-section authority map applied. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies how Veeva Vault RIM Suite 24R3 is configured to satisfy `NIM-URS-RIM-001` v1.2 — managing submission planning + sequence build / validate / dispatch + archive + registrations + commitments + variations + renewals + IDMP master data + EMA SPOR sync across regions.

## 2. Scope

Vault RIM 24R3 tenancy (Submissions + Registrations + Submissions Archive + IDMP modules), per-region eCTD configuration, SSO via Okta + MFA, integrations with Vault QualityDocs (Vellis), Vault eTMF (Marinos), Sirius Argus PV; EMA SPOR (SMS / PMS / OMS / RMS); FDA ESG; regional HA gateways.

## 3. System Architecture

```
                Okta SSO + MFA
                       │
                       ▼
   ┌────────────────────────────────────────────────────────────┐
   │     Vault RIM Suite 24R3 (Nimbus tenancy)                   │
   │   Submissions / Registrations / Submissions Archive /       │
   │   Product Master (IDMP) / Health-Authority Correspondence / │
   │   Commitments / Variations / Renewals                        │
   └─┬─────────────┬──────────────┬──────────────┬────────────┬─┘
     │             │              │              │            │
     ▼             ▼              ▼              ▼            ▼
   Vault       Vault eTMF     EMA SPOR        FDA ESG     Regional HA
   Quality-    (Marinos)     (SMS / PMS /                   gateways
   Docs                       OMS / RMS)                    (EMA, PMDA,
   (Vellis)                                                 HC, TGA,
                                                            ANVISA,
                                                            NMPA)
```

## 4. Functional Specifications

### 4.1 Vendor / Platform Assurance

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VND-01 | URS-VND-01 | SOC 2 Type II + ISO/IEC 27001:2022 + Veeva CSV summary for 24R3; vendor-assurance dossier; annual re-qualification. |
| FS-VND-02 | URS-VND-02 | Release-note workflow: RNS feed → impact assessment → change-control record within 14 days. |
| FS-VND-03 | URS-VND-03 | Annual review of vendor SDLC evidence; stored in `/vendor-assurance/veeva/`. |
| FS-VND-04 | URS-VND-04 | Sub-processor list reviewed quarterly per DPA Annex II. |

### 4.2 Configuration / Region eCTD + Module 1

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CFG-01 | URS-CFG-01 | Country / region / product / submission-type metadata maintained under change control. |
| FS-CFG-02 | URS-CFG-02 | eCTD config (FDA / EMA / PMDA / HC / TGA / ANVISA / NMPA Module 1 + ICH M4 + M8) maintained to current; updates impact-assessed ≤ 30 d. |
| FS-CFG-03 | URS-CFG-03 | Region-specific Module 1 controlled vocabularies tracked per HA terminology service. |
| FS-CFG-04 | URS-CFG-04 | Document lifecycle: DRAFT → IN-REVIEW → APPROVED → READY-TO-PUBLISH → PUBLISHED → SUPERSEDED. |
| FS-CFG-05 | URS-CFG-05 | Lifecycle transitions e-sig with SoD via FS-SOD-01. |
| FS-CFG-06 | URS-CFG-06 | eCTD v4 readiness configuration deployable per HA-published v4 timelines; switchover guarded by per-HA feature flag. |

### 4.3 Submission Planning and Tracking

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLN-01 | URS-PLN-01 | Multi-region submission plan template; target HA dates, content-owner assignment, dependencies, milestone tracking. |
| FS-PLN-02 | URS-PLN-02 | Critical-path engine surfaces late tasks; D-60/D-30/D-14/D-7/D-0 configurable alerts. |
| FS-PLN-03 | URS-PLN-03 | Per-region status: Planned, In Build, In Review, Ready to Publish, Published, Acknowledged, Approved, Withdrawn. |
| FS-PLN-04 | URS-PLN-04 | Resource-planning view: workload per role vs submission deadlines. |
| FS-PLN-05 | URS-PLN-05 | Plan baseline + revisions retained for retrospective slip analysis. |

### 4.4 Sequence Build, Validate, Dispatch

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SEQ-01 | URS-SEQ-01 | Sequence builder per HA-specific Module 1 + M4/M8 modules; missing required documents block build. |
| FS-SEQ-02 | URS-SEQ-02 | Per-HA validator rule sets (FDA, EMA, PMDA, HC, TGA, ANVISA, NMPA); failure blocks dispatch. |
| FS-SEQ-03 | URS-SEQ-03 | Lifecycle operators (new/append/replace/delete) conform to ICH M8; integrity verified on build. |
| FS-SEQ-04 | URS-SEQ-04 | Unique sequence numbering per HA per product via DB constraint; gaps blocked. |
| FS-SEQ-05 | URS-SEQ-05 | Gateway dispatch (FDA ESG, EMA gateway, regional) returns MDN / ACK; non-ACK within window escalates. |
| FS-SEQ-06 | URS-SEQ-06 | Cross-reference table to eTMF + QualityDocs; monthly broken-reference report. |
| FS-SEQ-07 | URS-SEQ-07 | SHA-256 sequence-content hash recorded at READY-TO-PUBLISH; matched against Archive hash on dispatch. |
| FS-SEQ-08 | URS-SEQ-08 | Preview rendering of sequence in HA-style view pre-dispatch. |

### 4.5 Submissions Archive

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ARC-01 | URS-ARC-01 | Auto-archive of dispatched sequence + ACK; SHA-256 checksums recorded. |
| FS-ARC-02 | URS-ARC-02 | Archive immutable; retrieval ≤ 4 BH during inspection. |
| FS-ARC-03 | URS-ARC-03 | Retention ≥ 30 y post-licence-discontinuation; longer per jurisdictional minimums. |
| FS-ARC-04 | URS-ARC-04 | Quarterly archive-integrity verification job; failures deviated and remediated. |
| FS-ARC-05 | URS-ARC-05 | Archive export supports eCTD v3.2.2 + v4 formats. |

### 4.6 Registrations and IDMP Master Data

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REG-01 | URS-REG-01 | Registration records per product / country with states {PLANNED, IN-REVIEW, APPROVED, SUSPENDED, WITHDRAWN}; transitions audit-trailed. |
| FS-REG-02 | URS-REG-02 | Variations / renewals / line extensions linked to parent registration with submission-sequence linkage. |
| FS-REG-03 | URS-REG-03 | Approval-letter + label-version + indication-version linkage per registration. |
| FS-IDMP-01 | URS-IDMP-01 | Medicinal Product (MPID) entity conforms to ISO 11615 schema; identifiers tracked per HA region. |
| FS-IDMP-02 | URS-IDMP-02 | Substance entity conforms to ISO 11238; UNII + EMA SMS identifiers reconciled. |
| FS-IDMP-03 | URS-IDMP-03 | Pharmaceutical Product (PhPID) entity conforms to ISO 11616. |
| FS-IDMP-04 | URS-IDMP-04 | Dose forms + routes + packaging conform to ISO 11239 with EDQM controlled vocabulary. |
| FS-IDMP-05 | URS-IDMP-05 | Units of measurement conform to ISO 11240 with UCUM mapping. |
| FS-IDMP-06 | URS-IDMP-06 | IDMP export in HL7 FHIR R5 + ISO XML for HA submissions; schema validated in CI. |

### 4.7 EMA SPOR Sync

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SPOR-01 | URS-SPOR-01 | Nightly SMS (substance) sync; conflict queue. |
| FS-SPOR-02 | URS-SPOR-02 | Nightly PMS (product) sync; conflict queue. |
| FS-SPOR-03 | URS-SPOR-03 | Nightly OMS (organisation) sync; conflict queue. |
| FS-SPOR-04 | URS-SPOR-04 | Nightly RMS (referential vocabularies) sync; conflict queue. |
| FS-SPOR-05 | URS-SPOR-05 | Conflict-resolution UI for Product Master Steward; decisions audit-trailed. |
| FS-SPOR-06 | URS-SPOR-06 | Daily drift report; > 5% drift raises deviation. |

### 4.8 HA Correspondence

| FS ID | URS ID | Specification |
|---|---|---|
| FS-COR-01 | URS-COR-01 | Inbound + outbound correspondence capture with classification, source, target, response-required, due-date metadata. |
| FS-COR-02 | URS-COR-02 | D-30/D-14/D-7/D-0 alert ladder; overdue escalates to VP Regulatory Affairs. |
| FS-COR-03 | URS-COR-03 | Cross-link to commitments + variations + renewals. |
| FS-COR-04 | URS-COR-04 | Searchable archive by HA + product + submission + classification. |

### 4.9 Commitments + Variations + Renewals

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CMT-01 | URS-CMT-01 | Commitments tracked per HA with due-dates; D-30/D-7/D-0 alerts; overdue escalates. |
| FS-CMT-02 | URS-CMT-02 | Commitment states (Open / In Progress / Submitted / Closed / Withdrawn); closure references closing sequence. |
| FS-VAR-01 | URS-VAR-01 | Variation tracking per HA with category (Type IA/IB/II EMA; CBE/CBE-30/PAS FDA), state, sequence linkage. |
| FS-VAR-02 | URS-VAR-02 | Variation campaigns group multi-region simultaneous variations. |
| FS-RNW-01 | URS-RNW-01 | Renewal tracking with lead-time alerts (12m/6m/3m/1m). |

### 4.10 Audit Trail / 21 CFR Part 11 / ALCOA+

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit trail covers all events (doc edits, lifecycle, sequence build/validate/dispatch, config, signatures, registration state, IDMP/SPOR updates). |
| FS-AUD-02 | URS-AUD-02 | Append-only DB; tenant admin lacks UPDATE/DELETE on audit rows. |
| FS-AUD-03 | URS-AUD-03 | Monthly Head of Reg Ops audit-trail review; evidence in `/reviews/audit/`. |
| FS-AUD-04 | URS-AUD-04 | Retention ≥ 30 y post-licence-discontinuation. |
| FS-PART11-01 | URS-PART11-01 | Procedural-control SOP linked from system docs. |
| FS-PART11-02 | URS-PART11-02 | Accurate + complete copies exportable (PDF/A-3 + XML). |
| FS-PART11-03 | URS-PART11-03 | Records protected throughout retention; integrity verifiable. |
| FS-PART11-04 | URS-PART11-04 | Okta SAML 2.0 + MFA access; service accounts via mTLS. |
| FS-PART11-05 | URS-PART11-05 | Audit trail per FS-AUD-01. |
| FS-PART11-06 | URS-PART11-06 | Authority-check middleware at API + UI. |
| FS-PART11-07 | URS-PART11-07 | Operation manuals under change control; effective manuals trigger LMS R&U. |
| FS-PART11-08 | URS-PART11-08 | Internet-exposed endpoints: TLS 1.3 + short-lived tokens + IP allow-list where contracted. |
| FS-PART11-09 | URS-PART11-09 | Signature manifestation includes printed name + ISO 8601 timestamp + meaning. |
| FS-PART11-10 | URS-PART11-10 | HMAC-SHA256 binding signature → record-hash. |
| FS-PART11-11 | URS-PART11-11 | Unique signature-id per user; no reuse. |
| FS-PART11-12 | URS-PART11-12 | Re-auth at sequence approval + dispatch authorisation; max-age 5 min. |
| FS-PART11-13 | URS-PART11-13 | Password policy + lockout 5/15min + MFA mandatory. |
| FS-DI-01 | URS-DI-01 | Actor_id non-null on every event. |
| FS-DI-02 | URS-DI-02 | PDF/A-3 + XML/JSON exports. |
| FS-DI-03 | URS-DI-03 | NTP-synced server timestamps. |
| FS-DI-04 | URS-DI-04 | Original content preserved unaltered. |
| FS-DI-05 | URS-DI-05 | Deterministic build + validate calculations. |
| FS-DI-06 | URS-DI-06 | ≥ 30 y retention + retrievability ≤ 1 BD routine, ≤ 4 h inspection. |

### 4.11 Integrations

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-EDMS-01 | URS-INT-EDMS-01 | Vault Connect to Vault QualityDocs for controlled-document consumption. |
| FS-INT-ETMF-01 | URS-INT-ETMF-01 | Cross-reference to Marinos eTMF clinical-trial artefacts. |
| FS-INT-PV-01 | URS-INT-PV-01 | Cross-link to Sirius Argus PV for PSUR / PBRER references. |
| FS-INT-PUBLISH-01 | URS-INT-PUBLISH-01 | Publishing engine API; quarterly connectivity test. |
| FS-INT-ESG-01 | URS-INT-ESG-01 | FDA ESG integration per FDA technical specification; credentials managed in Reg Ops vault. |
| FS-INT-SPOR-01 | URS-INT-SPOR-01 | EMA SPOR API integration per EMA spec; OAuth 2.0 + nightly sync. |
| FS-INT-SSO-01 | URS-INT-SSO-01 | Okta SAML 2.0 + MFA + SCIM 2.0. |
| FS-INT-API-01 | URS-INT-API-01 | Vault Connect OAuth 2.0 client-credentials; short-lived tokens. |

### 4.12 Performance, Availability, Backup, Security

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | Doc open/list P95 ≤ 3 s. |
| FS-PERF-02 | URS-PERF-02 | 1500-doc sequence build ≤ 30 min. |
| FS-AV-01 | URS-AV-01 | Veeva SLA ≥ 99.9% during HA-deadline windows. |
| FS-BAK-01 | URS-BAK-01 | Vendor backup; site verifies RPO ≤ 4 h / RTO ≤ 24 h annually. |
| FS-BAK-02 | URS-BAK-02 | Tenant export to ≥ 30 y cold storage. |
| FS-SEC-01 | URS-SEC-01 | TLS 1.3 + AES-256. |
| FS-SEC-02 | URS-SEC-02 | Per-product / per-region role scoping. |
| FS-SEC-03 | URS-SEC-03 | Annual vendor cert review. |
| FS-SEC-04 | URS-SEC-04 | Annual pen-test of author + dispatch endpoints. |

### 4.13 Inspection-Readiness

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INSP-01 | URS-INSP-01 | Inspection-readiness dashboard: registrations + recent submissions + commitments + variations + correspondence backlog. |
| FS-INSP-02 | URS-INSP-02 | Export ≤ 4 BH; PDF/A-3 + machine-readable index. |
| FS-INSP-03 | URS-INSP-03 | Inspector workspace: 30-d default, watermarked, audit-trailed. |
| FS-INSP-04 | URS-INSP-04 | Per-HA pack content configurable (FDA BIMO, EMA, BfArM, PEI, Swissmedic, AGES, PMDA). |

### 4.14 Reporting and Search

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RPT-01 | URS-RPT-01 | Standard reports: Submission Pipeline, Registration Status, Commitment Aging, Variation Backlog, Correspondence Backlog, IDMP Currency, SPOR Drift. |
| FS-RPT-02 | URS-RPT-02 | Full-text search respects access-control scopes. |
| FS-RPT-03 | URS-RPT-03 | Ad-hoc report builder available to Head of Reg Ops + Submissions Coordinator. |
| FS-RPT-04 | URS-RPT-04 | Standard report rendering ≤ 5 min. |

### 4.15 Configuration Management

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CCM-01 | URS-CCM-01 | DEV → UAT → PROD promotion with SoD-enforced approvals. |
| FS-CCM-02 | URS-CCM-02 | Baselines versioned; baseline-diff drift detection. |
| FS-CCM-03 | URS-CCM-03 | Vendor release impact-assessment ≤ 14 d. |
| FS-CCM-04 | URS-CCM-04 | HA-spec-driven changes (Module 1, eCTD validator) tested via regression suite in UAT before PROD. |

### 4.16 Training and Periodic Review

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Cornerstone-recorded RIM role-training; pre-PROD gate. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher `RIM-2026-ANNUAL` covers ICH M4/M8, IDMP/SPOR, Module 1 changes. |
| FS-PR-01 | URS-PR-01 | Annual Periodic Review signed by Head of Reg Ops + VP Reg Affairs + Head of QA. |


### 4.17 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: SAML 2.0 via Entra ID with SCIM lifecycle provisioning. Conditional-access binding to policy `Regulatory-App Conditional Access (FIDO2 phishing-resistant MFA)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the RIM metadata DB plus object-replica for submission artefacts; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Configuration Items (CI)

| CI | Item | Value |
|---|---|---|
| CI-01 | Lifecycle states | DRAFT, IN-REVIEW, APPROVED, READY-TO-PUBLISH, PUBLISHED, SUPERSEDED |
| CI-02 | Registration states | PLANNED, IN-REVIEW, APPROVED, SUSPENDED, WITHDRAWN |
| CI-03 | IDMP standards | ISO 11615 / 11616 / 11238 / 11239 / 11240 |
| CI-04 | SPOR sync cadence | Nightly |
| CI-05 | SPOR drift threshold | 5% |
| CI-06 | Commitment alerts | D-30, D-7, D-0 |
| CI-07 | Renewal lead-time | 12m, 6m, 3m, 1m |
| CI-08 | Re-auth max-age | 5 minutes |
| CI-09 | Account lockout | 5 fails / 15 min |
| CI-10 | DR test cadence | Annual |
| CI-11 | Audit-trail review | Monthly |
| CI-12 | Archive retention | ≥ 30 years post-licence-discontinuation |
| CI-13 | Archive integrity check | Quarterly |
| CI-14 | Inspection export SLA | ≤ 4 business hours |
| CI-15 | eCTD v4 readiness | Per-HA feature flag |

## 6. Risks (FS-level)

URS § 9 documents R-01..R-10. Additional FS-level risks:

- IDMP / SPOR conflict-queue backlog causing stale product master → mitigation: queue-aging alert (FS-SPOR-05).
- HA gateway certificate rotation breaking dispatch → mitigation: pre-rotation test in UAT (FS-INT-ESG-01).
- eCTD v4 transition window — dual-format support → mitigation: per-HA feature flag (FS-CFG-06).
- Inspector-workspace credential phishing → mitigation: short-lived tokens + watermarked downloads (FS-INSP-03).

## 7. References

- NIM-URS-RIM-001 v1.2
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- 21 CFR Parts 312 + 314
- ICH M2 + M4 + M8
- EMA EU Module 1 specification + Q&A on eCTD v4
- IDMP — ISO 11238 / 11239 / 11240 / 11615 / 11616
- EMA SPOR (SMS / PMS / OMS / RMS)
- FDA ESG Guidance
- EU CTR 536/2014 Arts. 25, 81
- EU GMP Annex 11 §§ 4, 6, 9, 11
- GDPR Arts. 6, 32
- ISPE GAMP 5 (2nd Edition, 2022)
- PIC/S PI 041
- ISO/IEC 27001:2022
- Veeva — *Vault RIM Suite 24R3 Validation Approach* + *Configuration Reference*

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-VND-01 | FS-VND-01 |
| URS-VND-02 | FS-VND-02 |
| URS-VND-03 | FS-VND-03 |
| URS-VND-04 | FS-VND-04 |
| URS-CFG-01 | FS-CFG-01 |
| URS-CFG-02 | FS-CFG-02 |
| URS-CFG-03 | FS-CFG-03 |
| URS-CFG-04 | FS-CFG-04 |
| URS-CFG-05 | FS-CFG-05 |
| URS-CFG-06 | FS-CFG-06 |
| URS-PLN-01 | FS-PLN-01 |
| URS-PLN-02 | FS-PLN-02 |
| URS-PLN-03 | FS-PLN-03 |
| URS-PLN-04 | FS-PLN-04 |
| URS-PLN-05 | FS-PLN-05 |
| URS-SEQ-01 | FS-SEQ-01 |
| URS-SEQ-02 | FS-SEQ-02 |
| URS-SEQ-03 | FS-SEQ-03 |
| URS-SEQ-04 | FS-SEQ-04 |
| URS-SEQ-05 | FS-SEQ-05 |
| URS-SEQ-06 | FS-SEQ-06 |
| URS-SEQ-07 | FS-SEQ-07 |
| URS-SEQ-08 | FS-SEQ-08 |
| URS-ARC-01 | FS-ARC-01 |
| URS-ARC-02 | FS-ARC-02 |
| URS-ARC-03 | FS-ARC-03 |
| URS-ARC-04 | FS-ARC-04 |
| URS-ARC-05 | FS-ARC-05 |
| URS-REG-01 | FS-REG-01 |
| URS-REG-02 | FS-REG-02 |
| URS-REG-03 | FS-REG-03 |
| URS-IDMP-01 | FS-IDMP-01 |
| URS-IDMP-02 | FS-IDMP-02 |
| URS-IDMP-03 | FS-IDMP-03 |
| URS-IDMP-04 | FS-IDMP-04 |
| URS-IDMP-05 | FS-IDMP-05 |
| URS-IDMP-06 | FS-IDMP-06 |
| URS-SPOR-01 | FS-SPOR-01 |
| URS-SPOR-02 | FS-SPOR-02 |
| URS-SPOR-03 | FS-SPOR-03 |
| URS-SPOR-04 | FS-SPOR-04 |
| URS-SPOR-05 | FS-SPOR-05 |
| URS-SPOR-06 | FS-SPOR-06 |
| URS-COR-01 | FS-COR-01 |
| URS-COR-02 | FS-COR-02 |
| URS-COR-03 | FS-COR-03 |
| URS-COR-04 | FS-COR-04 |
| URS-CMT-01 | FS-CMT-01 |
| URS-CMT-02 | FS-CMT-02 |
| URS-VAR-01 | FS-VAR-01 |
| URS-VAR-02 | FS-VAR-02 |
| URS-RNW-01 | FS-RNW-01 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
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
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-INT-EDMS-01 | FS-INT-EDMS-01 |
| URS-INT-ETMF-01 | FS-INT-ETMF-01 |
| URS-INT-PV-01 | FS-INT-PV-01 |
| URS-INT-PUBLISH-01 | FS-INT-PUBLISH-01 |
| URS-INT-ESG-01 | FS-INT-ESG-01 |
| URS-INT-SPOR-01 | FS-INT-SPOR-01 |
| URS-INT-SSO-01 | FS-INT-SSO-01 |
| URS-INT-API-01 | FS-INT-API-01 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-AV-01 | FS-AV-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-INSP-01 | FS-INSP-01 |
| URS-INSP-02 | FS-INSP-02 |
| URS-INSP-03 | FS-INSP-03 |
| URS-INSP-04 | FS-INSP-04 |
| URS-RPT-01 | FS-RPT-01 |
| URS-RPT-02 | FS-RPT-02 |
| URS-RPT-03 | FS-RPT-03 |
| URS-RPT-04 | FS-RPT-04 |
| URS-CCM-01 | FS-CCM-01 |
| URS-CCM-02 | FS-CCM-02 |
| URS-CCM-03 | FS-CCM-03 |
| URS-CCM-04 | FS-CCM-04 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Missed HA deadline (target date slip) | Medium | High | URS-PLN-02, URS-SEQ-05 |
| R-02 | Incorrect sequence numbering causing HA rejection | Low | High | URS-SEQ-04 |
| R-03 | Outdated eCTD specification used | Medium | High | URS-CFG-02 |
| R-04 | eCTD submission validation failure at HA gateway | Medium | High | URS-SEQ-02, URS-SEQ-05 |
| R-05 | IDMP referential drift between local and EMA SPOR | Medium | Medium | URS-SPOR-06 |
| R-06 | Post-approval commitment expiry not detected | Medium | High | URS-CMT-01 |
| R-07 | Multi-region variation tracking gap | Medium | Medium | URS-VAR-01, URS-VAR-02 |
| R-08 | Audit-trail tampering on vendor side | Low | Critical | URS-AUD-02 |
| R-09 | Signature compromise (cached credentials accepted at signing) | Low | Critical | URS-PART11-12 |
| R-10 | FDA ESG account credential compromise | Low | Critical | URS-INT-ESG-01, URS-SEC-01 |

Full evaluation in `NIM-RA-RIM-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
