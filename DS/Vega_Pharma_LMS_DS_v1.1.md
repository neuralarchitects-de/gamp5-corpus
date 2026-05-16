---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (v1.0 DS corpus ship)"
seed_corpus_basis:
  - "VGA-FS-LMS-001 v1.2 (parent FS, T2-T3 Cat 4)"
  - "VGA-URS-LMS-001 v1.2 (parent URS, transitive)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 Configuration Specification conventions"
  - "21 CFR Part 11; 21 CFR § 211.25; EU GMP Annex 11; EU GMP Chapter 2"
  - "ADL SCORM 2004 4th Ed.; xAPI 1.0.3; cmi5"
  - "ICH Q10; ISO 9001:2015; ISO 13485:2016; ISO/IEC 27001:2022; PIC/S PI 041"
  - "Cornerstone Learning 2025 — Configuration Reference"
parent_fs:
  document_number: VGA-FS-LMS-001
  version: "1.2"
  file: ../../../FS_FDS/_generated/final/Vega_Pharma_LMS_FS_v1.3.md
parent_urs:
  document_number: VGA-URS-LMS-001
  version: "1.2"
  file: ../../../URS/_generated/final/LMS_Learning_Management_System__Vega_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## LMS — Cornerstone OnDemand Learning 2025 — Vega Pharma Tenancy

**Document Number:** VGA-DS-LMS-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** VGA-FS-LMS-001 v1.2
**Parent URS:** VGA-URS-LMS-001 v1.2
**Site:** Vega Pharma *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Project Mode:** Greenfield-SaaS (single Vega tenancy; serves all GxP role training)
**Regulatory Scope:** 21 CFR Part 11; 21 CFR § 211.25; EU GMP Annex 11; EU GMP Chapter 2; ICH Q10; SCORM 2004 + xAPI 1.0.3 + cmi5; ISO 9001:2015; ISO 13485:2016; ISO/IEC 27001:2022; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Director, Training) | _____________ | _____________ | _____ |
| Reviewer (QA Reviewer) | _____________ | _____________ | _____ |
| Reviewer (System Owner — Head of Learning Operations) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — VP QA) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Approver (VP Quality Assurance) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue. Inherited Tier T2-T3 from parent URS+FS pair. DS covers 70/70 FS-IDs; 0 FS-IDs flagged as vendor-internal — no site design surface. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

| Term | Definition |
|---|---|
| CI | Configuration Item in Cornerstone Learning 2025 |
| SCORM 2004 | ADL Sharable Content Object Reference Model, 4th Edition |
| xAPI | Experience API 1.0.3 (Tin Can) |
| cmi5 | Computer-Managed Instruction 5 — modern xAPI profile |
| R&U | Read-and-Understood (controlled-document attestation) |
| Verified by | Planned IQ / OQ / PQ test |

## 1. Purpose

This Configuration Specification records the technical design of the Cornerstone OnDemand Learning 2025 tenancy at Vega Pharma, including curriculum + role-mapping configuration, content-delivery runtime (SCORM 2004 / xAPI 1.0.3 / cmi5), quiz engine, training records, competency + expiry, compliance dashboard, and integration bindings to satisfy `VGA-FS-LMS-001` v1.2.

## 2. Scope

**In scope:** Cornerstone tenancy configuration; curriculum lifecycle + role mapping; SCORM / xAPI / cmi5 runtime configuration; quiz engine; training-record schema; competency + expiry; compliance dashboard; integration bindings to Okta + Vault QualityDocs (Vellis) + MasterControl eQMS (Talos) + HR + GxP-app gating + LRS.

**Out of scope:** Cornerstone vendor source-code internals; Okta internals; Vault internals; MasterControl internals; HR-system internals; GxP-app internals; LRS internals (LRS may be embedded or external — site selects per CI).

## 3. Architectural Overview

The Vega tenancy operates as a single multi-tenant SaaS instance. Identity is federated via Okta (SAML 2.0 + MFA + SCIM 2.0). Content runtimes are SCORM 2004 / xAPI / cmi5; legacy AICC HACP is read-only for migration. R&U tasks resolve Vault URNs at runtime. Production access to GxP apps is gated via a training-currency REST API.

```
                           ┌──────────────────────────────────┐
                           │   Okta SAML 2.0 + MFA + SCIM     │
                           └──────────────────┬───────────────┘
                                              │
              ┌───────────────────────────────▼────────────────────────────────┐
              │  Cornerstone OnDemand Learning 2025 — Vega tenancy              │
              │  ┌──────────────────────────────────────────────────────┐    │
              │  │ Curricula / role-mapping / completion engine          │    │
              │  │ SCORM 2004 / xAPI 1.0.3 / cmi5 runtime                │    │
              │  │ Quiz engine + question banks                           │    │
              │  │ Competency + expiry + access-gating API                │    │
              │  │ Compliance Dashboard                                    │    │
              │  └──────────────────────────────────────────────────────┘    │
              └──┬───────────┬───────────┬───────────┬──────────┬─────────────┘
                 │           │           │           │          │
                 ▼           ▼           ▼           ▼          ▼
            Vault         eQMS        HR          GxP-app      LRS
            QualityDocs   Master-     (SCIM 2.0 / (MES, LIMS,  (xAPI;
            (Vellis)      Control     SFTP)       EDC, ELN,    embedded
                          (Talos)                  eTMF,        or
                                                   etc.)        external)
```

### 3.1 Component-design inventory

| Layer | Component | Vendor / source | Version | Site design surface |
|---|---|---|---|---|
| Application | Cornerstone tenancy (Vega) | Cornerstone | Learning 2025 | Configuration (§ 4) |
| Identity | Okta | Okta | per site IT | Configuration (§ 4, § 7) |
| Counterparty | Vault QualityDocs (Vellis) | Veeva | 24R3+ | Bindings (§ 7) |
| Counterparty | MasterControl eQMS (Talos) | MasterControl | QMS 2025 | Bindings (§ 7) |
| Counterparty | HR system | per site | per site | Bindings (§ 7) |
| Counterparty | GxP apps (MES, LIMS, EDC, ELN, eTMF, etc.) | various | per app | Bindings (§ 7) |
| Counterparty | LRS (xAPI) | embedded or external | per site | Bindings (§ 7) |

---

## 4. Configuration Specification

### 4.1 Vendor Assurance bindings

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VND-01 | Vendor-assurance dossier | SOC 2 Type II + ISO/IEC 27001:2022 + CSV summary; annual re-qualification | Custom | Critical-vendor | FS-VND-01 | OQ-VND-REG-01 |
| DS-VND-02 | Release-note review workflow | impact-assessment ≤ 14 days | Custom | Release cadence | FS-VND-02 | OQ-VND-REL-01 |
| DS-VND-03 | Sub-processor list quarterly review | per DPA Annex II | Custom | GDPR Art. 28 | FS-VND-03 | OQ-VND-SUBPROC-01 |

### 4.2 Curriculum + Role Mapping + Catalogue CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CUR-01 | Curriculum lifecycle states (`CUR_STATES`) | `DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED` | Custom | 5-state | FS-CUR-01 | OQ-CUR-STATES-01 |
| DS-CUR-02 | Assignment-engine source filter | EFFECTIVE-only curricula; SUPERSEDED in history | Custom | Currency enforcement | FS-CUR-02 | OQ-CUR-ASSIGN-01 |
| DS-CUR-03 | Lifecycle e-sig SoD | per FS-SOD-01 | Custom | Independence | FS-CUR-03 | OQ-CUR-SIG-SOD-01 |
| DS-CUR-04 | EFFECTIVE immutability flag | DB-level immutable; changes spawn new revision | Custom | Anti-tamper | FS-CUR-04 | OQ-CUR-IMMUT-01 |
| DS-CUR-05 | Role-to-curriculum mapping table | per-role training-plan view | Custom | Role-driven assignment | FS-CUR-05 | OQ-ROLE-MAP-01 |
| DS-CUR-06 | Course-catalogue search index | by topic / GxP domain / competency / role | Custom | Operational search | FS-CUR-06 | OQ-CATALOGUE-SEARCH-01 |
| DS-CUR-07 | Version-in-force pin | pinned to historical assignments | Custom | Retrospective integrity | FS-CUR-07 | OQ-VERSION-PIN-01 |

### 4.3 Auto-Enrollment + Lifecycle Events CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ASN-01 | Joiner-event handler | SCIM 2.0 primary / daily SFTP fallback; auto-enrollment ≤ 4 BH | Custom | Joiner cadence | FS-ASN-01 | OQ-JOINER-01 |
| DS-ASN-02 | Mover-event handler | re-evaluates curricula; obsoletes no-longer-required | Custom | Mover cadence | FS-ASN-02 | OQ-MOVER-01 |
| DS-ASN-03 | Leaver-event handler | revokes active access; preserves history | Custom | Leaver cadence | FS-ASN-03 | OQ-LEAVER-01 |
| DS-ASN-04 | EDMS effective-date subscriber | creates R&U tasks for affected roles | Custom | Doc-change cascade | FS-ASN-04 | OQ-EDMS-SUB-01 |
| DS-ASN-05 | eQMS CAPA endpoint | REST; idempotency `CAPA-id + revision` | Custom | Idempotent | FS-ASN-05 | OQ-CAPA-ENDPOINT-01 |
| DS-ASN-06 | Manual-assignment rule | `justification` mandatory + audit-trail row | Custom | Audit-trail | FS-ASN-06 | OQ-MANUAL-ASSIGN-01 |

### 4.4 Content Delivery CIs (SCORM / xAPI / cmi5)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-DEL-01 | SCORM 2004 4th Ed. runtime | SCORM-API session; `cmi.core` data model | Default | ADL standard | FS-DEL-01 | OQ-SCORM-01 |
| DS-DEL-02 | xAPI LRS endpoint (`LRS_URL`) | configurable (embedded or external) | Custom | Site choice | FS-DEL-02 | OQ-XAPI-LRS-01 |
| DS-DEL-03 | cmi5 package support | AU launch + statement flow per cmi5 spec | Default | Standard | FS-DEL-03 | OQ-CMI5-01 |
| DS-DEL-04 | AICC HACP legacy | migration-only; new content gated to SCORM 2004 / xAPI / cmi5 | Custom | Legacy support window | FS-DEL-04 | OQ-AICC-LEGACY-01 |
| DS-DEL-05 | R&U task config | references Vault URN; min-dwell-time enforced | Custom | Comprehension floor | FS-DEL-05 | OQ-RU-DWELL-01 |
| DS-DEL-06 | R&U attestation re-auth | re-auth per FS-PART11-10 | Custom | § 11.200 | FS-DEL-06 | OQ-RU-REAUTH-01 |

### 4.5 Quiz / Assessment CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-QZ-01 | Quiz types (`QUIZ_TYPES`) | `MC, multi-select, T/F, fill-in-blank, short-answer` | Custom | Assessment variety | FS-QZ-01 | OQ-QUIZ-TYPES-01 |
| DS-QZ-02 | Pass-score default (`PASS_SCORE`) | `80%`; below triggers re-take with question randomisation | Default | Standard pass threshold | FS-QZ-02 | OQ-PASS-SCORE-01 |
| DS-QZ-03 | Question-bank versioning | change creates new version + audit trail | Custom | Versioning discipline | FS-QZ-03 | OQ-QBANK-VER-01 |
| DS-QZ-04 | Effectiveness-evidence linkage | per training record | Custom | Effectiveness | FS-QZ-04 | OQ-QUIZ-EFFECT-01 |
| DS-QZ-05 | Attempt limit default (`ATTEMPT_LIMIT`) | `3`; escalation on exceed | Default | Attempt control | FS-QZ-05 | OQ-ATTEMPT-LIMIT-01 |

### 4.6 Training Records + Audit Trail + Part 11 CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-REC-01 | Record schema | `user_id, training_id+version, document_URN, method, score, server-NTP timestamp, instructor` | Custom | Comprehensive record | FS-REC-01 | OQ-REC-SCHEMA-01 |
| DS-REC-02 | Retroactive workflow | Training Admin request + QA approval + reason | Custom | Anti-abuse | FS-REC-02 | OQ-RETRO-01 |
| DS-REC-03 | § 211.25 personnel-qualification report | per role / function | Custom | Regulator binding | FS-REC-03 | OQ-PQ-REPORT-01 |
| DS-AUD-01 | Audit trail coverage | curriculum lifecycle / assignment / completion / retroactive / config | Default | Native trail | FS-AUD-01 | OQ-AUDIT-COVERAGE-01 |
| DS-AUD-02 | Tenant-admin UPDATE/DELETE block | enforced at audit-row level | Custom | Tamper-protection | FS-AUD-02 | OQ-AUDIT-PROTECT-01 |
| DS-AUD-03 | Review cadence | monthly Head of Learning Ops + quarterly QA Compliance | Custom | Annex 11 § 9 | FS-AUD-03 | OQ-AUDIT-REVIEW-01 |
| DS-AUD-04 | Retention | employment + 5 y minimum; GxP product-record retention where applicable | Custom | § 211.180 + employment basis | FS-AUD-04 | IQ-RET-01 |
| DS-PART11-01 | Procedural-control SOP | linked from system docs | Custom | § 11.10(a) | FS-PART11-01 | OQ-SOP-LINK-01 |
| DS-PART11-02 | Export engine (`PDF/A-3 + CSV`) | OQ-validated | Custom | § 11.10(b) | FS-PART11-02 | OQ-INSPECTION-COPY-01 |
| DS-PART11-03 | Retention-protected records | cryptographic integrity verifiable on retrieval | Custom | § 11.10(c) | FS-PART11-03 | OQ-RECORD-PROTECT-01 |
| DS-PART11-04 | Okta SAML 2.0 + MFA access | enforced | Custom | § 11.10(d) | FS-PART11-04 | OQ-OKTA-MFA-01 |
| DS-PART11-05 | Audit-trail enforcement | per DS-AUD-01 | Default | § 11.10(e) | FS-PART11-05 | OQ-AT-ENFORCEMENT-01 |
| DS-PART11-06 | Authority-check middleware | role-based; per-action | Custom | § 11.10(g) | FS-PART11-06 | OQ-AUTHORITY-CHECK-01 |
| DS-PART11-07 | E-sig manifestation | `name + ISO 8601 + meaning` | Default | § 11.50 | FS-PART11-07 | OQ-SIG-MANIFEST-01 |
| DS-PART11-08 | Signature binding | HMAC-SHA256 over record | Default | § 11.70 | FS-PART11-08 | OQ-SIG-BINDING-01 |
| DS-PART11-09 | Signature-id uniqueness | Okta + LMS constraint | Custom | § 11.100 | FS-PART11-09 | OQ-SIG-UNIQUE-01 |
| DS-PART11-10 | Re-auth at R&U + curriculum approval + retroactive completion | max-age 5 min | Custom | § 11.200 | FS-PART11-10 | OQ-REAUTH-01 |
| DS-PART11-11 | Password policy + lockout | `5 fails / 15 min`; MFA | Custom | § 11.300 | FS-PART11-11 | OQ-LOCKOUT-01 |
| DS-SOD-01 | DB constraint | `curriculum_author_id ≠ curriculum_approver_id` per revision | Custom | SoD | FS-SOD-01 | OQ-SOD-DB-01 |

### 4.7 Competency + Re-training + Expiry CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COMP-01 | Competency entity | bound to `user_id`; sourced from completion records | Default | Native entity | FS-COMP-01 | OQ-COMP-ENTITY-01 |
| DS-COMP-02 | Refresher cycles | configurable; alerts at `D-60, D-30, D-7, D-0`; expiry revokes GxP access | Custom | Alert cadence | FS-COMP-02 | OQ-REFRESHER-01 |
| DS-COMP-03 | EDMS new-version subscriber | triggers re-training for affected users | Custom | Doc-change cascade | FS-COMP-03 | OQ-EDMS-RETRAIN-01 |
| DS-COMP-04 | Competency dashboard | per role + site + user | Custom | Operational view | FS-COMP-04 | PQ-COMP-DASH-01 |
| DS-COMP-05 | Mover-race reconciliation queue | ordering logic + retry | Custom | Race-condition handling | FS-COMP-05 | OQ-MOVER-RECON-01 |

### 4.8 Compliance Dashboard + Reporting CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-DASH-01 | Compliance dashboard | site + dept + role training currency / overdue / expiring / expired | Custom | KPI tracking | FS-DASH-01 | OQ-DASH-01 |
| DS-DASH-02 | Standard reports | Currency, Overdue, Effectiveness, CAPA Completion, R&U Completion, Audit Review | Custom | Standardised reporting | FS-DASH-02 | OQ-REPORTS-01 |
| DS-DASH-03 | Per-user / per-role inspection export | ≤ 4 h | Custom | Inspection-readiness | FS-DASH-03 | PQ-DASH-EXPORT-01 |
| DS-DASH-04 | Ad-hoc report builder | for Head of Learning Ops + Head of QA | Custom | Flexibility | FS-DASH-04 | OQ-ADHOC-01 |

### 4.9 Integration CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-INT-EDMS-01 | Vault Connect subscriber to QualityDocs effective-date events | drives R&U task creator | Custom | Doc-change binding | FS-INT-EDMS-01 | OQ-VAULT-SUBSCRIBE-01 |
| DS-INT-EQMS-01 | MasterControl CAPA task endpoint | REST; idempotency `CAPA-id + revision` | Custom | Idempotent | FS-INT-EQMS-01 | OQ-EQMS-CAPA-01 |
| DS-INT-HR-01 | HR sync | SCIM 2.0 primary; SFTP daily fallback | Custom | Joiner/mover/leaver | FS-INT-HR-01 | OQ-HR-SYNC-01 |
| DS-INT-SSO-01 | Okta SAML 2.0 + MFA + SCIM 2.0 | per realm `vega.okta.com` | Custom | Site IdP | FS-INT-SSO-01 | OQ-OKTA-SAML-01 |
| DS-INT-APP-01 | Training-currency REST API | consumed by MES / LIMS / EDC / ELN / eTMF; non-current → 403 | Custom | Access gating | FS-INT-APP-01 | OQ-CURRENCY-API-01 |

### 4.10 Performance / Availability / Backup / Security CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PERF-01 | Course load P95 | ≤ 3 s | Default | UX target | FS-PERF-01 | PQ-PERF-COURSE-01 |
| DS-AV-01 | Cornerstone SLA | per contract | Default | Vendor SLA | FS-AV-01 | OQ-SLA-01 |
| DS-BAK-01 | Vendor backup; site verifies RPO ≤ 4 h / RTO ≤ 24 h | annual | Custom | Vendor-assurance | FS-BAK-01 | PQ-BAK-VERIFY-01 |
| DS-SEC-01 | TLS 1.3 + AES-256 | enforced | Custom | InfoSec | FS-SEC-01 | OQ-TLS-AES-01 |
| DS-SEC-02 | Per-site / per-role access scope | Vault security profile | Custom | Segregation | FS-SEC-02 | OQ-RBAC-01 |
| DS-SEC-03 | Annual pen-test | learner + admin endpoints | Custom | Independent assurance | FS-SEC-03 | OQ-PENTEST-01 |

### 4.11 Training + Periodic Review CIs

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-TRN-01 | LMS-administrator training prerequisite | gate on admin permissions | Custom | Admin competency | FS-TRN-01 | OQ-ADMIN-TRN-01 |
| DS-TRN-02 | Annual refresher (`LMS-2026-ANNUAL`) | Cornerstone releases + SCORM/xAPI/cmi5 + § 211.25 + EU GMP Chapter 2 | Custom | Currency | FS-TRN-02 | PQ-ANNUAL-REFRESHER-01 |
| DS-PR-01 | Annual periodic-review template | signed by Head Learning Ops + Head QA | Custom | Annex 11 § 11 | FS-PR-01 | PQ-PR-LMS-01 |

### 4.12 Cross-System Bindings (M-XSYS / M-XINT)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-XSYS-AD-01 | Entra ID SAML 2.0 + SCIM | conditional-access policy `Standard SaaS Conditional Access` | Custom | Per FS-XSYS-AD-01 | FS-XSYS-AD-01 | OQ-XSYS-AD-01 |
| DS-XSYS-AD-02 | SIEM (`Splunk gxp-authn`) | RFC 5424 ≤ 5 min lag | Custom | Cross-system correlation | FS-XSYS-AD-01 | OQ-SIEM-FWD-01 |
| DS-XSYS-AD-03 | CyberArk PAM binding | 24 h rotation + dual-witness check-out | Custom | Break-glass | FS-XSYS-AD-01 | OQ-PAM-01 |
| DS-XSYS-BAK-01 | Veeam VSS + MS SQL Server | T2 tier; RPO ≤ 24 h / RTO ≤ 24 BH | Custom | Per FS-XSYS-BAK-01 | FS-XSYS-BAK-01 | OQ-VEEAM-01 |
| DS-XSYS-BAK-02 | S3 Object Lock COMPLIANCE bucket | geo-replicated | Custom | Anti-ransom | FS-XSYS-BAK-01 | IQ-S3-OBJLOCK-01 |
| DS-XSYS-BAK-03 | LTO-9 air-gap rotation | monthly | Custom | Air-gap policy | FS-XSYS-BAK-01 | OQ-LTO9-01 |
| DS-XSYS-BAK-04 | Restore-cert retention | ≥ 25 y in eQMS | Custom | Quality-record discipline | FS-XSYS-BAK-01 | OQ-RESTORE-CERT-01 |
| DS-XINT-EDMS-01 | EDMS webhook subscription (`vellis.doc.effective.v1`) | auto-assign linked curriculum; deadlines per risk-class | Custom | Per FS-XINT-EDMS-01 | FS-XINT-EDMS-01 | OQ-EDMS-WEBHOOK-01 |
| DS-XINT-EDMS-02 | Non-completion AD-group revocation | per LMS URS-REVOKE-* | Custom | Access-revocation discipline | FS-XINT-EDMS-01 | OQ-AD-REVOKE-01 |

---

## 5. Workflow + Business-Rule Design

### 5.1 Curriculum lifecycle workflow

| Step | State | Actor | Gate |
|---|---|---|---|
| 1 | `DRAFT` | Curriculum Author | content drafted |
| 2 | `REVIEW` | Curriculum Reviewer | content review |
| 3 | `APPROVED` | Curriculum Approver (≠ Author per DS-SOD-01) | re-auth e-sig |
| 4 | `EFFECTIVE` | system | assignment-engine includes; previous version `SUPERSEDED` |
| 5 | `SUPERSEDED` | system | visible in history; historical assignments retain version-in-force |

### 5.2 Auto-enrollment workflow

| Trigger | Source | Action |
|---|---|---|
| Joiner event | HR SCIM 2.0 → Okta → LMS | match role → enroll in role-curricula within 4 BH |
| Mover event | HR SCIM 2.0 | re-evaluate; new curricula enrolled; obsolete tagged |
| Leaver event | HR SCIM 2.0 | revoke active access; preserve records per retention |
| EDMS effective-date | Vault webhook `vellis.doc.effective.v1` | R&U task auto-created for affected roles |
| eQMS CAPA-driven training | MasterControl REST POST | CAPA task created; idempotency `CAPA-id + revision` |
| Manual assignment | Training Admin | `justification` ≥ 50 chars + audit-trail row |

### 5.3 Production-access gating business rule

GxP applications consume training-currency via REST API `GET /api/v2/training-currency/{user_id}?role={role}`. Response: `{"current": true|false, "expiry_ts": "...", "missing": [...]}`. App denies production access with HTTP 403 when `current=false`. Cache TTL: 60 s on consumer side (FS-INT-APP-01 mitigation).

### 5.4 Quiz pass-score business rule

For each training where `pass_score` configured, the runtime evaluates quiz submission:
- `score >= pass_score` → completion recorded
- `score < pass_score` AND `attempts < ATTEMPT_LIMIT (3)` → re-take allowed with randomised question order
- `attempts >= ATTEMPT_LIMIT` → escalation to Training Admin + audit-trail row

### 5.5 Expiry revocation business rule

When `competency.expiry_date < now`, scheduler runs `revoke_expired_access()`:
1. Mark user as non-current for affected role.
2. AD-group membership in `<App>-Operator` group revoked.
3. Notification sent to user + Training Admin.
4. Audit-trail row written.

---

## 6. Role-Permission Matrix Design

| Role | Curriculum-Author | Curriculum-Approver | Quiz-Author | Quiz-Approver | Training-Admin | Retroactive-Approver | LRS-Admin | Dashboard-Viewer | LMS-Admin |
|---|---|---|---|---|---|---|---|---|---|
| `Curriculum-Author` | R/W | – | – | – | – | – | – | R | – |
| `Curriculum-Approver` | R | R/W | – | – | – | – | – | R | – |
| `Quiz-Author` | – | – | R/W | – | – | – | – | – | – |
| `Quiz-Approver` | – | – | R | R/W | – | – | – | – | – |
| `Training-Admin` | R | – | R | – | R/W | – | – | R | – |
| `Retroactive-Approver` (QA) | – | – | – | – | R | R/W | – | – | – |
| `LRS-Admin` | – | – | – | – | – | – | R/W | – | – |
| `Head-Learning-Ops` | R | R | R | R | R | R | R | R/W | – |
| `Head-QA` | R | R | – | – | R | R/W | – | R/W | – |
| `LMS-Admin` | – | – | – | – | R | – | R/W | R | R/W |

SoD: `curriculum_author_id ≠ curriculum_approver_id` (DS-SOD-01); `Quiz-Author ∩ Quiz-Approver = ∅`; `Training-Admin ∩ Retroactive-Approver = ∅` (retroactive completion requires QA approval).

---

## 7. Integration Design

### 7.1 Vault QualityDocs subscriber (FS-INT-EDMS-01)

- Vault Connect: subscribes to `vellis.doc.effective.v1` topic
- Payload: doc-id, doc-type, effective-date, training-impact-flag, doc-risk-class, affected-roles[]
- Action: R&U task creator runs; per-affected-role tasks created with `deadline = effective_date + risk_class.deadline_hours`

### 7.2 MasterControl CAPA endpoint (FS-INT-EQMS-01)

- Endpoint: inbound `POST https://lms.vega.local/api/v2/capa-tasks`
- AuthN: mTLS + bearer
- Idempotency: header `Idempotency-Key: capa:<id>:<revision>`

### 7.3 HR integration (FS-INT-HR-01)

- Primary: SCIM 2.0 via Okta (real-time)
- Fallback: SFTP daily delta file → batch processor
- Schema: `user_id, employee_id, role_codes[], joined_at, left_at?`

### 7.4 Okta SSO + MFA (FS-INT-SSO-01)

- Protocol: SAML 2.0 + SCIM 2.0 lifecycle
- MFA: TOTP / WebAuthn at every signature
- Re-auth max-age: 300 s

### 7.5 Training-currency API (FS-INT-APP-01)

- Endpoint: `GET https://lms.vega.local/api/v2/training-currency/{user_id}?role={role}`
- AuthN: mTLS + bearer (per-app service account)
- Response shape: `{"current": bool, "expiry_ts": iso8601, "missing": [training_id...]}`
- Consumer-side cache TTL: 60 s (FS-INT-APP-01 mitigation R-04 in FS Risk Register)

### 7.6 LRS endpoint (xAPI)

- Endpoint: configurable; embedded (Cornerstone built-in) or external (per site selection)
- xAPI 1.0.3 statements: stored + queryable
- Store-and-forward: reconciliation queue on outage (FS-DEL-02 mitigation R-06 in FS Risk Register)

---

## 8. Site-Deployed Components Design

Cornerstone is operated as a pure Cat 4 SaaS at Vega — no site-developed code is in scope. All integration adapters (Vault subscriber, eQMS endpoint, HR SCIM connector, training-currency API, LRS endpoint) are realised through Cornerstone's native integration platform. No § 8 mini-SDS sub-sections are required for v1.0.

---

## 9. References

### US
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- 21 CFR § 211.25 (Personnel qualifications)
- 21 CFR § 211.180

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EU GMP Chapter 2
- GDPR Arts. 6, 28, 32

### DACH
- BfArM (DE) — informational reference

### International
- ICH Q10
- ADL SCORM 2004 4th Edition
- xAPI 1.0.3 (Tin Can)
- cmi5
- ISO 9001:2015; ISO 13485:2016
- ISO/IEC 27001:2022
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE GAMP GPG *Records & Data Integrity*
- PIC/S PI 041

### Vendor
- Cornerstone — *Learning 2025 Configuration Reference*
- Cornerstone — *Validation Approach*
- Okta — *SAML 2.0 + SCIM 2.0 Integration Reference*

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-VND-01 | FS-VND-01 |
| DS-VND-02 | FS-VND-02 |
| DS-VND-03 | FS-VND-03 |
| DS-CUR-01 | FS-CUR-01 |
| DS-CUR-02 | FS-CUR-02 |
| DS-CUR-03 | FS-CUR-03 |
| DS-CUR-04 | FS-CUR-04 |
| DS-CUR-05 | FS-CUR-05 |
| DS-CUR-06 | FS-CUR-06 |
| DS-CUR-07 | FS-CUR-07 |
| DS-ASN-01 | FS-ASN-01 |
| DS-ASN-02 | FS-ASN-02 |
| DS-ASN-03 | FS-ASN-03 |
| DS-ASN-04 | FS-ASN-04 |
| DS-ASN-05 | FS-ASN-05 |
| DS-ASN-06 | FS-ASN-06 |
| DS-DEL-01 | FS-DEL-01 |
| DS-DEL-02 | FS-DEL-02 |
| DS-DEL-03 | FS-DEL-03 |
| DS-DEL-04 | FS-DEL-04 |
| DS-DEL-05 | FS-DEL-05 |
| DS-DEL-06 | FS-DEL-06 |
| DS-QZ-01 | FS-QZ-01 |
| DS-QZ-02 | FS-QZ-02 |
| DS-QZ-03 | FS-QZ-03 |
| DS-QZ-04 | FS-QZ-04 |
| DS-QZ-05 | FS-QZ-05 |
| DS-REC-01 | FS-REC-01 |
| DS-REC-02 | FS-REC-02 |
| DS-REC-03 | FS-REC-03 |
| DS-AUD-01 | FS-AUD-01 |
| DS-AUD-02 | FS-AUD-02 |
| DS-AUD-03 | FS-AUD-03 |
| DS-AUD-04 | FS-AUD-04 |
| DS-PART11-01 | FS-PART11-01 |
| DS-PART11-02 | FS-PART11-02 |
| DS-PART11-03 | FS-PART11-03 |
| DS-PART11-04 | FS-PART11-04 |
| DS-PART11-05 | FS-PART11-05 |
| DS-PART11-06 | FS-PART11-06 |
| DS-PART11-07 | FS-PART11-07 |
| DS-PART11-08 | FS-PART11-08 |
| DS-PART11-09 | FS-PART11-09 |
| DS-PART11-10 | FS-PART11-10 |
| DS-PART11-11 | FS-PART11-11 |
| DS-SOD-01 | FS-SOD-01 |
| DS-COMP-01 | FS-COMP-01 |
| DS-COMP-02 | FS-COMP-02 |
| DS-COMP-03 | FS-COMP-03 |
| DS-COMP-04 | FS-COMP-04 |
| DS-COMP-05 | FS-COMP-05 |
| DS-DASH-01 | FS-DASH-01 |
| DS-DASH-02 | FS-DASH-02 |
| DS-DASH-03 | FS-DASH-03 |
| DS-DASH-04 | FS-DASH-04 |
| DS-INT-EDMS-01 | FS-INT-EDMS-01 |
| DS-INT-EQMS-01 | FS-INT-EQMS-01 |
| DS-INT-HR-01 | FS-INT-HR-01 |
| DS-INT-SSO-01 | FS-INT-SSO-01 |
| DS-INT-APP-01 | FS-INT-APP-01 |
| DS-PERF-01 | FS-PERF-01 |
| DS-AV-01 | FS-AV-01 |
| DS-BAK-01 | FS-BAK-01 |
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
| DS-XINT-EDMS-01 | FS-XINT-EDMS-01 |
| DS-XINT-EDMS-02 | FS-XINT-EDMS-01 |

---

## 11. Design-level Risk Register

| ID | Design-level risk | Origin (DS-ID / design choice) | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|---|
| DR-01 | Joiner / mover assignment delay > 4 BH due to SCIM rate-limit | DS-ASN-01 + DS-INT-HR-01 | Medium | Medium | Backpressure queue + SFTP fallback |
| DR-02 | R&U click-through without dwell-time enforcement | DS-DEL-05 + DS-DEL-06 | Medium | Medium | Min-dwell-time + re-auth (DS-PART11-10) |
| DR-03 | Retroactive-completion abuse — Training-Admin role overlap | DS-REC-02 + DS-PART11-10 | Medium | Medium | SoD: `Training-Admin ∩ Retroactive-Approver = ∅` |
| DR-04 | Access-gating bypass — GxP-app caches stale training-currency | DS-INT-APP-01 | Medium | High | Consumer cache TTL 60 s + contract test |
| DR-05 | Audit-trail tampering on vendor side | DS-AUD-02 + DS-VND-01 | Low | High | Vendor-assurance dependency |
| DR-06 | SCORM content version drift — authoring tool republish missed | DS-CUR-04 + DS-DEL-01 | Medium | Medium | Package-validity check on upload + version-pin |
| DR-07 | Certification expiry not enforced — user retains access | DS-COMP-02 | Medium | High | Scheduler revoke + AD-group revocation (DS-XINT-EDMS-02) |
| DR-08 | Document-training auto-link miss — new EDMS doc effective without R&U trigger | DS-INT-EDMS-01 + DS-COMP-03 | Medium | Medium | Subscriber health-check + reconciliation |
| DR-09 | Role-change auto-enroll race condition (leaver before joiner) | DS-COMP-05 + DS-ASN-02 | Low | Medium | Reconciliation queue with ordering + retry |
| DR-10 | LRS (xAPI) availability gap drops statements | DS-DEL-02 | Medium | Medium | Store-and-forward + reconciliation queue |
| DR-11 | Joiner SCIM-event burst overruns auto-enroll worker | DS-ASN-01 | Low | Medium | Backpressure queue + throttle |
| DR-12 | Currency API consumer mis-implementation (caches stale > 60 s) | DS-INT-APP-01 | Medium | High | Contract test + integration-test suite |
| DR-13 | SCORM authoring tool publish bug yields broken package | DS-DEL-01 | Low | Medium | Package-validity check on upload |
| DR-14 | EDMS webhook subscription drift after vendor release | DS-XINT-EDMS-01 + DS-VND-02 | Low | High | Vendor-release runbook reviews webhook schemas |
| DR-15 | Quiz question-bank version-pin failure (old question shown to new attempt) | DS-QZ-03 | Low | Medium | Version-pin OQ + golden quiz test |
| DR-16 | Mover-event handler obsoletes a curriculum that still applies (false positive) | DS-ASN-02 | Low | High | Role-mapping review + UAT scenario |
| DR-17 | LMS-Admin role escalation via misconfigured Okta group claim | DS-INT-SSO-01 | Low | Critical | Quarterly RBAC review |
| DR-18 | Compliance dashboard data freshness lag during inspection | DS-DASH-01 + DS-DASH-03 | Low | High | Inspection export priority queue |
| DR-19 | Annual refresher curriculum (`LMS-2026-ANNUAL`) becomes stale on regulatory change | DS-TRN-02 | Medium | Medium | Annual content review + RA tracking |
| DR-20 | Cornerstone vendor release silently changes SCIM rate-limit | DS-INT-HR-01 + DS-VND-02 | Low | Medium | Release-eval runbook + monitoring |

The full formal Risk Assessment is `VGA-RA-LMS-001` (synthetic, separate document).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
