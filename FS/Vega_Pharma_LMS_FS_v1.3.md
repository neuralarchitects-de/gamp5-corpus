---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (FS catch-up to URS v1.2; full per-ID expansion of 69 URS-IDs; SCORM 2004 + xAPI 1.0.3 + cmi5 explicit; § 11 sub-section authority map)"
seed_corpus_basis:
  - "VGA-URS-LMS-001 v1.2 (parent URS)"
  - "ISPE GAMP 5 (2nd Edition, 2022) Cat 4 SaaS conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "21 CFR § 211.25 (Personnel qualifications)"
  - "EU GMP Annex 11; EU GMP Chapter 2; ICH Q10"
  - "ADL SCORM 2004 4th Edition; xAPI 1.0.3; cmi5"
  - "ISO 9001:2015; ISO 13485:2016; ISO/IEC 27001:2022; PIC/S PI 041"
parent_urs:
  document_number: VGA-URS-LMS-001
  version: 1.2
  file: ../../URS/_generated/final/LMS_Learning_Management_System__Vega_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# Functional Specification (FS)

## LMS — Cornerstone OnDemand Learning 2025 (Vega Pharma tenancy)

**Document Number:** VGA-FS-LMS-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** VGA-URS-LMS-001 v1.2 | **Site:** Vega Pharma (fictional)
**System Class:** GAMP Cat 4 — Configured Product (multi-tenant SaaS)
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR § 211.25; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Chapter 2; ICH Q10; SCORM 2004 + xAPI 1.0.3 + cmi5; ISO 9001:2015 + ISO 13485:2016; ISO/IEC 27001:2022; PIC/S PI 041.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Director, Training) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Approver (VP Quality Assurance) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue (partial; superseded). |
| 1.1 | 2026-05-08 | (synthetic) | Cornerstone Learning version 2025. |
| 1.2 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.2: full per-ID expansion of 69 URS-IDs (no range compression per § 2A.7); SCORM 2004 + xAPI 1.0.3 + cmi5; § 11 sub-section authority map applied. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies how Cornerstone OnDemand Learning 2025 is configured at the Vega Pharma tenancy to satisfy `VGA-URS-LMS-001` v1.2 — controlled-training assignment, completion, and competency tracking for GxP roles, with content delivered via SCORM 2004 / xAPI / cmi5.

## 2. Scope

Cornerstone Learning 2025 multi-tenant SaaS; per-role curriculum + competency configuration; SSO via Okta + MFA; integrations with EDMS Vault QualityDocs (Vellis), eQMS MasterControl (Talos Bio), HR (SCIM 2.0 / SFTP), GxP applications (MES / LIMS / EDC / ELN / Vault eTMF / etc. — production-access gating).

## 3. System Architecture

```
                Okta SSO + MFA
                       │
                       ▼
   ┌──────────────────────────────────────────────────┐
   │     Cornerstone Learning 2025 (Vega tenancy)      │
   │   Curricula / role-mapping / completion +         │
   │   Quiz engine + SCORM 2004 / xAPI 1.0.3 / cmi5    │
   │   Competency + expiry + access-gating API         │
   │   Compliance Dashboard                             │
   └──┬────────┬─────────┬────────┬────────┬──────────┘
      │        │         │        │        │
      ▼        ▼         ▼        ▼        ▼
   Vault     eQMS      HR      GxP-app   LRS (xAPI)
   Quality-  Master-   (SCIM   access    (embedded or
   Docs      Control   2.0 /   gating    external)
   (Vellis)  (Talos)   SFTP)   (MES,
                                LIMS,
                                EDC, etc.)
```

## 4. Functional Specifications

### 4.1 Vendor Assurance

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VND-01 | URS-VND-01 | Cornerstone vendor-assurance dossier: SOC 2 Type II + ISO/IEC 27001:2022 + CSV summary; annual re-qualification. |
| FS-VND-02 | URS-VND-02 | Release-note review workflow; impact-assessment ≤ 14 days. |
| FS-VND-03 | URS-VND-03 | Sub-processor list quarterly review per DPA Annex II. |

### 4.2 Curriculum + Role Mapping + Catalogue

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CUR-01 | URS-CUR-01 | Curriculum lifecycle state machine: DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED. |
| FS-CUR-02 | URS-CUR-02 | Assignment-engine selects from EFFECTIVE-only curricula; SUPERSEDED visible in history. |
| FS-CUR-03 | URS-CUR-03 | Lifecycle e-sig with SoD (FS-SOD-01). |
| FS-CUR-04 | URS-CUR-04 | EFFECTIVE records DB-flagged immutable; changes spawn new revision in DRAFT. |
| FS-CUR-05 | URS-CUR-05 | Role-to-curriculum mapping table; per-role training-plan view. |
| FS-CUR-06 | URS-CUR-06 | Course-catalogue search by topic / GxP domain / competency / role. |
| FS-CUR-07 | URS-CUR-07 | Curriculum version-in-force pinned to historical assignments. |

### 4.3 Auto-Enrollment + Lifecycle Events

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ASN-01 | URS-ASN-01 | HR joiner-event handler (SCIM 2.0 / daily SFTP) triggers curriculum auto-enrollment ≤ 4 BH. |
| FS-ASN-02 | URS-ASN-02 | Mover-event handler re-evaluates curricula; new required enrolled, no-longer-required → OBSOLETE-FOR-USER. |
| FS-ASN-03 | URS-ASN-03 | Leaver-event revokes active access; historical records preserved per retention policy. |
| FS-ASN-04 | URS-ASN-04 | EDMS effective-date event subscriber creates R&U tasks for affected roles. |
| FS-ASN-05 | URS-ASN-05 | eQMS CAPA REST endpoint; idempotency key = CAPA-id + revision. |
| FS-ASN-06 | URS-ASN-06 | Manual assignment requires justification field + audit-trail row. |

### 4.4 Content Delivery (SCORM / xAPI / cmi5)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DEL-01 | URS-DEL-01 | SCORM 2004 4th Ed. runtime: SCORM-API session, cmi.core data model, score + completion-status capture. |
| FS-DEL-02 | URS-DEL-02 | xAPI 1.0.3 LRS endpoint (embedded or external configurable); statements queryable. |
| FS-DEL-03 | URS-DEL-03 | cmi5 package support; AU launch + statement flow per cmi5 spec. |
| FS-DEL-04 | URS-DEL-04 | Legacy AICC HACP for migration-only; new content gated to SCORM 2004 / xAPI / cmi5. |
| FS-DEL-05 | URS-DEL-05 | R&U task references Vault URN; doc-open timestamp + configurable min-dwell-time enforced. |
| FS-DEL-06 | URS-DEL-06 | R&U attestation requires re-authentication (FS-PART11-10). |

### 4.5 Quiz / Assessment

| FS ID | URS ID | Specification |
|---|---|---|
| FS-QZ-01 | URS-QZ-01 | Quiz types: MC, multi-select, T/F, fill-in-blank, short-answer; pass-score per training. |
| FS-QZ-02 | URS-QZ-02 | Pass-score default 80%; below-threshold triggers re-take with question randomisation. |
| FS-QZ-03 | URS-QZ-03 | Question bank versioning; change creates new version + audit trail. |
| FS-QZ-04 | URS-QZ-04 | Effectiveness-check evidence linked to training record. |
| FS-QZ-05 | URS-QZ-05 | Attempt limit default 3; escalation on exceed. |

### 4.6 Training Records + Audit Trail + 21 CFR Part 11

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REC-01 | URS-REC-01 | Record schema: user_id, training_id+version, document_URN, method, score, server-NTP timestamp, instructor. |
| FS-REC-02 | URS-REC-02 | Retroactive workflow: Training Administrator request + QA approval + reason required. |
| FS-REC-03 | URS-REC-03 | Personnel-qualification report per 21 CFR § 211.25 generatable per role / function. |
| FS-AUD-01 | URS-AUD-01 | Audit trail covers curriculum lifecycle, assignment, completion, retroactive, config; append-only DB. |
| FS-AUD-02 | URS-AUD-02 | Tenant admin lacks UPDATE/DELETE on audit rows. |
| FS-AUD-03 | URS-AUD-03 | Monthly Head of Learning Ops review + quarterly QA compliance review. |
| FS-AUD-04 | URS-AUD-04 | Retention ≥ employment + 5 y; GxP records bound to product-record retention where applicable. |
| FS-PART11-01 | URS-PART11-01 | Procedural-control SOP linked from system docs. |
| FS-PART11-02 | URS-PART11-02 | Export engine produces PDF/A-3 + CSV training records. |
| FS-PART11-03 | URS-PART11-03 | Retention-protected records via cryptographic integrity verifiable on retrieval. |
| FS-PART11-04 | URS-PART11-04 | Okta SAML 2.0 + MFA access. |
| FS-PART11-05 | URS-PART11-05 | Audit trail per FS-AUD-01. |
| FS-PART11-06 | URS-PART11-06 | Role-based authority-check middleware. |
| FS-PART11-07 | URS-PART11-07 | E-sig manifestation includes name + ISO 8601 + meaning. |
| FS-PART11-08 | URS-PART11-08 | HMAC-SHA256 binding signature → record. |
| FS-PART11-09 | URS-PART11-09 | Signature-id uniqueness via Okta + LMS constraint. |
| FS-PART11-10 | URS-PART11-10 | Re-auth at R&U attestation + curriculum approval + retroactive completion; max-age 5 min. |
| FS-PART11-11 | URS-PART11-11 | Password policy + 5/15min lockout + MFA. |
| FS-SOD-01 | URS-SOD-01 | DB constraint: curriculum_author_id ≠ curriculum_approver_id per revision. |

### 4.7 Competency + Re-training + Expiry

| FS ID | URS ID | Specification |
|---|---|---|
| FS-COMP-01 | URS-COMP-01 | Competency entity bound to user_id; sourced from training-completion records. |
| FS-COMP-02 | URS-COMP-02 | Refresher cycles configurable; D-60/D-30/D-7/D-0 alerts; expiry revokes GxP-app access via gating API. |
| FS-COMP-03 | URS-COMP-03 | EDMS new-version subscriber triggers re-training for affected users. |
| FS-COMP-04 | URS-COMP-04 | Competency dashboard per role + site + user. |
| FS-COMP-05 | URS-COMP-05 | Mover-race reconciliation queue with ordering logic + retry. |

### 4.8 Compliance Dashboard + Reporting

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DASH-01 | URS-DASH-01 | Compliance Dashboard: site + dept + role training currency, overdue, expiring, expired. |
| FS-DASH-02 | URS-DASH-02 | Standard reports: Currency, Overdue, Effectiveness, CAPA Completion, R&U Completion, Audit Review. |
| FS-DASH-03 | URS-DASH-03 | Per-user / per-role training-history inspection export ≤ 4 h. |
| FS-DASH-04 | URS-DASH-04 | Ad-hoc report builder for Head of Learning Ops + Head of QA. |

### 4.9 Integrations

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-EDMS-01 | URS-INT-EDMS-01 | Vault Connect subscriber to QualityDocs effective-date events → R&U task creator. |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | REST endpoint for MasterControl CAPA task creation; idempotent on CAPA-id + revision. |
| FS-INT-HR-01 | URS-INT-HR-01 | SCIM 2.0 primary; SFTP daily fallback per HR-contract. |
| FS-INT-SSO-01 | URS-INT-SSO-01 | Okta SAML 2.0 + MFA + SCIM 2.0. |
| FS-INT-APP-01 | URS-INT-APP-01 | Training-currency REST API; consumed by MES / LIMS / EDC / ELN / eTMF / etc.; non-current → 403. |

### 4.10 Performance, Availability, Backup, Security

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | Course load P95 ≤ 3 s. |
| FS-AV-01 | URS-AV-01 | Cornerstone SLA per contract. |
| FS-BAK-01 | URS-BAK-01 | Vendor backup; site verifies RPO ≤ 4 h / RTO ≤ 24 h annually. |
| FS-SEC-01 | URS-SEC-01 | TLS 1.3 + AES-256. |
| FS-SEC-02 | URS-SEC-02 | Per-site / per-role access scope via Vault security profile. |
| FS-SEC-03 | URS-SEC-03 | Annual pen-test of learner + admin endpoints. |

### 4.11 Training + Periodic Review

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | LMS-administrator training prerequisite for admin permissions. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher curriculum `LMS-2026-ANNUAL` covers Cornerstone releases + SCORM/xAPI/cmi5 + § 211.25 + EU GMP Chapter 2. |
| FS-PR-01 | URS-PR-01 | Annual Periodic Review template signed by Head of Learning Operations + Head of QA. |


### 4.12 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: SAML 2.0 via Entra ID with SCIM lifecycle provisioning. Conditional-access binding to policy `Standard SaaS Conditional Access (MFA + device-compliance)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the Cornerstone OnDemand metadata mirror; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.13 Cross-System Integration — EDMS handover (M-XINT-EDMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-EDMS-01 | URS-XINT-EDMS-01 | Per controlled-document version transition the LMS consumes EDMS webhook `vellis.doc.effective.v1` and auto-assigns the linked curriculum; deadlines derived from the document's risk-class field; non-completion → AD-group membership revocation per LMS URS-REVOKE-*. |

## 5. Configuration Items (CI)

| CI | Item | Value |
|---|---|---|
| CI-01 | Curriculum lifecycle | DRAFT, REVIEW, APPROVED, EFFECTIVE, SUPERSEDED |
| CI-02 | Refresher expiry alerts | D-60, D-30, D-7, D-0 |
| CI-03 | Production-access gating | Enabled |
| CI-04 | Curriculum approval | SoD-enforced |
| CI-05 | Quiz pass-score default | 80% |
| CI-06 | Quiz attempt limit default | 3 |
| CI-07 | R&U min-dwell-time | Configurable per document |
| CI-08 | HR sync mode | SCIM 2.0 primary, SFTP daily fallback |
| CI-09 | SCORM version | 2004 4th Edition |
| CI-10 | xAPI version | 1.0.3 |
| CI-11 | cmi5 | Enabled |
| CI-12 | Re-auth max-age | 5 minutes |
| CI-13 | Lockout | 5 fails / 15 min |
| CI-14 | Audit-trail review | Monthly + quarterly QA review |
| CI-15 | Retention | Employment + 5 y minimum (longer per § 211.180 binding) |

## 6. Risks (FS-level)

URS § 9 documents R-01..R-09. Additional FS-level risks:

- LRS (xAPI back-end) availability gap → mitigation: store-and-forward + reconciliation queue (FS-DEL-02).
- Joiner SCIM event burst overruns auto-enroll worker → mitigation: backpressure queue + throttle (FS-ASN-01).
- Gating API consumer mis-implementation (caches stale training-currency) → mitigation: short-TTL cache spec + integration contract test (FS-INT-APP-01).
- SCORM authoring tool publish bug yields broken package → mitigation: package-validity check on upload (FS-DEL-01).

## 7. References

- VGA-URS-LMS-001 v1.2
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- 21 CFR § 211.25 + § 211.180
- EU GMP Annex 11 + Chapter 2
- ICH Q10
- ADL SCORM 2004 4th Edition; xAPI 1.0.3; cmi5
- ISO 9001:2015; ISO 13485:2016; ISO/IEC 27001:2022
- ISPE GAMP 5 (2nd Edition, 2022); PIC/S PI 041
- GDPR Arts. 6, 32
- Cornerstone — *Learning 2025 Configuration Reference*

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-VND-01 | FS-VND-01 |
| URS-VND-02 | FS-VND-02 |
| URS-VND-03 | FS-VND-03 |
| URS-CUR-01 | FS-CUR-01 |
| URS-CUR-02 | FS-CUR-02 |
| URS-CUR-03 | FS-CUR-03 |
| URS-CUR-04 | FS-CUR-04 |
| URS-CUR-05 | FS-CUR-05 |
| URS-CUR-06 | FS-CUR-06 |
| URS-CUR-07 | FS-CUR-07 |
| URS-ASN-01 | FS-ASN-01 |
| URS-ASN-02 | FS-ASN-02 |
| URS-ASN-03 | FS-ASN-03 |
| URS-ASN-04 | FS-ASN-04 |
| URS-ASN-05 | FS-ASN-05 |
| URS-ASN-06 | FS-ASN-06 |
| URS-DEL-01 | FS-DEL-01 |
| URS-DEL-02 | FS-DEL-02 |
| URS-DEL-03 | FS-DEL-03 |
| URS-DEL-04 | FS-DEL-04 |
| URS-DEL-05 | FS-DEL-05 |
| URS-DEL-06 | FS-DEL-06 |
| URS-QZ-01 | FS-QZ-01 |
| URS-QZ-02 | FS-QZ-02 |
| URS-QZ-03 | FS-QZ-03 |
| URS-QZ-04 | FS-QZ-04 |
| URS-QZ-05 | FS-QZ-05 |
| URS-REC-01 | FS-REC-01 |
| URS-REC-02 | FS-REC-02 |
| URS-REC-03 | FS-REC-03 |
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
| URS-SOD-01 | FS-SOD-01 |
| URS-COMP-01 | FS-COMP-01 |
| URS-COMP-02 | FS-COMP-02 |
| URS-COMP-03 | FS-COMP-03 |
| URS-COMP-04 | FS-COMP-04 |
| URS-COMP-05 | FS-COMP-05 |
| URS-DASH-01 | FS-DASH-01 |
| URS-DASH-02 | FS-DASH-02 |
| URS-DASH-03 | FS-DASH-03 |
| URS-DASH-04 | FS-DASH-04 |
| URS-INT-EDMS-01 | FS-INT-EDMS-01 |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 |
| URS-INT-HR-01 | FS-INT-HR-01 |
| URS-INT-SSO-01 | FS-INT-SSO-01 |
| URS-INT-APP-01 | FS-INT-APP-01 |
| URS-PERF-01 | FS-PERF-01 |
| URS-AV-01 | FS-AV-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-EDMS-01 | FS-XINT-EDMS-01 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Joiner / mover assignment delay | Medium | Medium | URS-ASN-01, URS-ASN-02 |
| R-02 | R&U click-through without comprehension | Medium | Medium | URS-DEL-05, URS-DEL-06 |
| R-03 | Retroactive-completion abuse | Medium | Medium | URS-REC-02, URS-SOD-01 |
| R-04 | Access-gating bypass causing untrained user in GxP app | Medium | High | URS-INT-APP-01 |
| R-05 | Audit-trail tampering on vendor side | Low | High | URS-AUD-02 |
| R-06 | SCORM content version drift (content updated in authoring tool, not republished) | Medium | Medium | URS-CUR-04, URS-DEL-01 |
| R-07 | Certification expiry not enforced (user retains access past competency lapse) | Medium | High | URS-COMP-02 |
| R-08 | Document-training auto-link miss (new EDMS doc effective without R&U trigger) | Medium | Medium | URS-INT-EDMS-01, URS-COMP-03 |
| R-09 | Role-change auto-enroll race condition (leaver before joiner) | Low | Medium | URS-COMP-05 |

Full evaluation in `VGA-RA-LMS-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
