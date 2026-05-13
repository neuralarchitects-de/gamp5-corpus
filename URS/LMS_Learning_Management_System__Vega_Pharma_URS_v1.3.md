---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; expanded 2026-05-12 (T2 uplift to 65 requirements; SCORM 2004 + xAPI 1.0.3 + cmi5 explicit; 21 CFR § 11 sub-section authority map; ICH Q10 + GMP Chapter 2; 21 CFR § 211.25 personnel qualifications)"
seed_corpus_basis:
  - "ISPE GAMP 5 (2nd Edition, 2022) Cat 4 SaaS conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "21 CFR § 211.25 — Personnel qualifications + training records"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "EU GMP Chapter 2 (Personnel) + Annex 1 § 7 (training for sterile manufacturing)"
  - "ICH Q10 — Pharmaceutical Quality System (training as quality enabler)"
  - "ISO 9001:2015 + ISO 13485:2016 (training records)"
  - "ADL SCORM 2004 4th Edition; xAPI (Tin Can) 1.0.3; cmi5"
  - "AICC HACP (legacy)"
  - "GDPR Arts. 6, 32"
  - "ISO/IEC 27001:2022; PIC/S PI 041"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# User Requirements Specification (URS)

## LMS — Cornerstone OnDemand Learning 2025

**Document Number:** VGA-URS-LMS-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Vega Pharma SL, Global Learning Operations, Tarragona, Catalonia, Spain *(fictional)*
**System Owner:** Head of Learning Operations
**Process Owner:** VP People & Culture
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS; vendor handles infrastructure; site validates configuration)
**Project Mode:** Configuration project on commercial software product **Cornerstone OnDemand Learning 2025** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a/b/c/d/e/g/k), .50, .70, .100, .200, .300; 21 CFR § 211.25; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Chapter 2 (Personnel); ICH Q10; ISO 9001:2015 + ISO 13485:2016; ADL SCORM 2004 + xAPI 1.0.3 + cmi5; GDPR Arts. 6, 32; ISO/IEC 27001:2022; PIC/S PI 041.

> **Note.** This URS covers Vega Pharma's enterprise LMS for **GxP training-records management** — the system of record for personnel qualification training under 21 CFR § 211.25 + EU GMP Chapter 2. It is distinct from: (a) **HR system** (authoritative for joiner / mover / leaver events; lifecycle source), (b) **EDMS** (Vellis Pharma — controlled-document authoring + read-and-understood document source), (c) **eQMS** (Talos Bio — CAPA + deviation training-task source).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of Learning Operations) | _____________ | _____________ | _____ |
| Reviewer (Vendor Assurance — Cornerstone relationship owner) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Privacy Officer — GDPR) | _____________ | _____________ | _____ |
| Approver (VP People & Culture) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-08 | (synthetic) | Editorial fixes. |
| 1.2 | 2026-05-12 | (synthetic) | T2 uplift to 65 requirements (Tier T2 per § 2A.13 — standard enterprise application spanning curriculum + assignment + completion + competency + integration + audit-trail). SCORM 2004 + xAPI + cmi5 explicit; 21 CFR § 211.25 personnel qualifications binding; § 11 sub-section authority map applied per § 2A.2; risk table expanded. |

## Definitions

| Term | Definition |
|---|---|
| LMS | Learning Management System |
| Cornerstone | Cornerstone OnDemand Learning 2025 |
| Curriculum | A grouped set of trainings tied to a role or system |
| Training Task | A task assigned to a user requiring completion |
| Read-and-Understood | A training type where the user reads a controlled document and confirms understanding |
| SCORM | Sharable Content Object Reference Model (ADL) — content-delivery + tracking standard (2004 4th Ed.) |
| xAPI | Experience API ("Tin Can") 1.0.3 — successor activity-tracking standard |
| cmi5 | xAPI profile for LMS / LRS interoperability |
| LRS | Learning Record Store (xAPI back-end) |
| OJT | On-the-Job Training |
| EDMS | Veeva Vault QualityDocs (Vellis Pharma — separate URS) |
| eQMS | MasterControl QMS (Talos Bio — separate URS) |
| HR | HR system (authoritative HRIS) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| Competency | Per-role required-knowledge + skill set; competency assessment confirms attainment |
| Refresher | Periodic re-training to maintain competency |

## 1. Purpose

Define the user requirements for the Learning Management System that records role-specific GxP training across Vega Pharma's global organisation. Training records are GMP records per 21 CFR § 211.25 + EU GMP Chapter 2; the LMS is the system of record.

## 2. Scope

**In scope:**
- Cornerstone OnDemand Learning 2025 multi-tenant SaaS configured for Vega Pharma tenancy.
- GxP curriculum + per-role training plan + competency-assessment configuration.
- Content delivery: SCORM 2004 4th Edition, xAPI 1.0.3, cmi5; AICC HACP (legacy support).
- Training types: eLearning, instructor-led (ILT + virtual ILT), read-and-understood, OJT, blended.
- Quiz / assessment engine + pass-score thresholds + effectiveness checks.
- Training-record audit trail per § 11.10(e).
- Auto-enrollment triggered by HR joiner / mover / leaver events; auto-enrollment triggered by EDMS controlled-document effective-date events for read-and-understood tasks; auto-enrollment from eQMS CAPA tasks.
- Re-training on document update triggers; expiry tracking; production-access gating consumed by GxP applications.
- Compliance Dashboard for Head of Learning Operations + Head of QA + Site Quality Heads.
- Integrations: HR system (SCIM 2.0 / SFTP); Vault QualityDocs (Vault Connect); MasterControl eQMS (REST API); Okta SAML 2.0 + MFA; GxP application access-gating (REST).

**Out of scope:**
- Training-content authoring (separate authoring tools at content-author desktops).
- HR data of record (HR system).
- Non-GxP training (general / commercial / sales training — same platform, different tenancy / governance).

## 3. System Description and Intended Use

Cornerstone is the system of record for GxP training records at Vega Pharma. Each role has a curriculum of mandatory trainings; new joiners + movers are auto-enrolled per the role mapping; training tasks track completion + score + signature + competency attainment; a user's GxP-system access (consumed via the access-gating API) is gated on training currency.

GAMP 5 (2nd Edition, 2022) Category 4 — Configured Product. Cornerstone maintains the platform; Vega validates per-tenancy configuration: curriculum structure + role mapping + assessment + integrations + gating logic.

## 4. User Roles

| Role | Permissions | SoD Constraints |
|---|---|---|
| Learner | Complete assigned training; cannot edit assignments | Cannot retroactively mark own training complete |
| Manager | View team training status; nominate trainings | Cannot mark training complete on behalf of report |
| Curriculum Author | Author / edit curricula under change control | Cannot approve own curriculum changes |
| Curriculum Approver (QA) | Approve curricula to EFFECTIVE | Cannot author same curriculum |
| Training Administrator | Manage training assignments + exceptions | Cannot approve curricula |
| Instructor | Mark ILT attendance + assessment results | Cannot retroactively mark dates outside session |
| Content Steward (EDMS bridge) | Approve content-version-to-training mapping | Cannot mark trainings complete |
| Auditor | Read-only across training records + audit trails | Strict read-only |

SoD enforced: Curriculum Author ≠ Approver; Training Administrator cannot retroactively mark training complete; Instructor cannot back-date attendance.

## 5. User Requirements

Each requirement carries a unique ID, priority (`H` / `M` / `L`), GAMP-5 risk classification (`R1` / `R2` / `R3`), and a verifiable `shall`-clause.

### 5.1 Vendor / Platform Assurance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-01 | H | R1 | Cornerstone shall be qualified as a critical SaaS vendor with documented evidence: SOC 2 Type II, ISO/IEC 27001:2022, customer-shared CSV summary. |
| URS-VND-02 | H | R1 | Vendor releases shall be impact-assessed within 14 days; configuration-affecting changes shall trigger re-validation. |
| URS-VND-03 | M | R2 | Vendor sub-processor list shall be reviewed quarterly per GDPR Art. 28(2). |

### 5.2 Curriculum + Per-Role Training Plan + Course Catalogue

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CUR-01 | H | R1 | Curricula shall follow lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → SUPERSEDED. |
| URS-CUR-02 | H | R1 | Only EFFECTIVE curricula shall be assignable; SUPERSEDED curricula shall be visible in history but not selectable for new assignments. |
| URS-CUR-03 | H | R1 | Curriculum lifecycle transitions shall require role-restricted electronic signatures with SoD enforced per § 5.6. |
| URS-CUR-04 | H | R1 | EFFECTIVE curricula shall be immutable; changes shall create new revisions in DRAFT state. |
| URS-CUR-05 | H | R1 | Each role shall map to one or more curricula; per-role training-plan view shall show all required trainings + status. |
| URS-CUR-06 | M | R2 | Course catalogue shall be searchable by topic, GxP domain (GMP, GCP, GLP, GDP), competency, role. |
| URS-CUR-07 | M | R2 | Curriculum versioning shall preserve historical assignments tied to the version-in-force at assignment time. |

### 5.3 Auto-Enrollment, Assignment, and Lifecycle Events

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ASN-01 | H | R1 | Joiner events from HR (SCIM 2.0 or daily SFTP) shall trigger curriculum auto-enrollment within 4 business hours of event receipt. |
| URS-ASN-02 | H | R1 | Mover events (role change, department change) shall trigger re-evaluation of curricula; new required trainings shall be enrolled, no-longer-required shall be marked OBSOLETE-FOR-USER. |
| URS-ASN-03 | H | R1 | Leaver events shall revoke active access but preserve historical training records per retention requirements. |
| URS-ASN-04 | H | R1 | EDMS controlled-document effective-date events shall trigger read-and-understood task creation for affected roles. |
| URS-ASN-05 | H | R1 | eQMS CAPA training-tasks shall be created via REST API; tasks shall be idempotent per CAPA-id + revision. |
| URS-ASN-06 | M | R2 | Manual training assignment by Training Administrator shall require justification + audit trail. |

### 5.4 Training Execution + Content Delivery (SCORM / xAPI / cmi5)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEL-01 | H | R1 | The platform shall support **SCORM 2004 4th Edition** content packages with per-launch SCORM-API session, score capture, completion-status reporting. |
| URS-DEL-02 | H | R1 | The platform shall support **xAPI 1.0.3** content via an embedded or external LRS; xAPI statements shall be queryable for training-record verification. |
| URS-DEL-03 | H | R1 | The platform shall support **cmi5** content packages for xAPI-LMS interoperability. |
| URS-DEL-04 | M | R2 | The platform shall support legacy AICC HACP for migration-period content; new content shall use SCORM 2004 or xAPI. |
| URS-DEL-05 | H | R1 | Read-and-understood tasks shall reference the controlled document by Vault URN; opening the document shall be timestamped; minimum dwell time shall be configurable per document. |
| URS-DEL-06 | H | R1 | Completion of read-and-understood shall require explicit attestation with re-authentication (per § 11.200). |

### 5.5 Quiz / Assessment Engine + Effectiveness Check

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-QZ-01 | H | R1 | The quiz engine shall support multiple-choice, multi-select, true/false, fill-in-blank, short-answer questions with configurable pass score per training. |
| URS-QZ-02 | H | R1 | Pass-score thresholds shall be configurable per training (default 80%); below-threshold attempts shall require re-take with new question randomisation. |
| URS-QZ-03 | H | R1 | Question banks shall be versioned; question changes shall create new question-version with audit trail. |
| URS-QZ-04 | M | R2 | Training **effectiveness checks** shall be supported (post-training competency-on-job verification); effectiveness-check evidence shall be linked to the training record. |
| URS-QZ-05 | M | R2 | Attempt limits shall be configurable (default 3); after limit, escalation to manager + Training Administrator. |

### 5.6 Training Records + Audit Trail + 21 CFR Part 11

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REC-01 | H | R1 | Training-completion records shall capture: user_id, training_id + version, document_URN (where applicable), method (eLearning / ILT / R&U / OJT), score (if assessed), timestamp (NTP-synced, server-side), instructor (if ILT). |
| URS-REC-02 | H | R1 | Retroactive completion shall require Training Administrator + QA approval and captured reason. |
| URS-REC-03 | H | R1 | Per **21 CFR § 211.25**, training-records shall demonstrate personnel qualification per role / function. |
| URS-AUD-01 | H | R1 | Time-stamped, secure audit trail covering curriculum lifecycle, assignment, completion, retroactive entries, configuration. |
| URS-AUD-02 | H | R1 | Audit trail shall be append-only; tenant administrators shall not have UPDATE/DELETE on audit records. |
| URS-AUD-03 | H | R1 | Audit-trail review monthly by Head of Learning Operations; quarterly compliance review with Head of QA. |
| URS-AUD-04 | H | R1 | Retention: ≥ employment + 5 years (or longer per local labour law); GxP training records ≥ retention-of-related-product-record where bound by 21 CFR § 211.180. |
| URS-PART11-01 | H | R1 | Per § 11.10(a), procedural controls shall protect training-record validity. |
| URS-PART11-02 | H | R1 | Per § 11.10(b), accurate + complete copies of training records exportable for inspection. |
| URS-PART11-03 | H | R1 | Per § 11.10(c), records protected throughout retention. |
| URS-PART11-04 | H | R1 | Per § 11.10(d), access limited to authorised individuals via Okta SAML 2.0 + MFA. |
| URS-PART11-05 | H | R1 | Per § 11.10(e), operational audit trail per URS-AUD-01. |
| URS-PART11-06 | H | R1 | Per § 11.10(g), authority checks enforce role-based permissions. |
| URS-PART11-07 | H | R1 | Per § 11.50, e-signatures on curriculum approval + retroactive-completion shall include signer's printed name + date/time + meaning. |
| URS-PART11-08 | H | R1 | Per § 11.70, signatures cryptographically bound to record (HMAC-SHA256). |
| URS-PART11-09 | H | R1 | Per § 11.100, signature identifiers unique per individual; no reuse. |
| URS-PART11-10 | H | R1 | Per § 11.200, re-authentication required at read-and-understood attestation + curriculum-approval + retroactive-completion signing. |
| URS-PART11-11 | H | R1 | Per § 11.300, password / credential controls per InfoSec policy; MFA mandatory; lockout 5/15min. |
| URS-SOD-01 | H | R1 | Curriculum Author ≠ Curriculum Approver of the same curriculum revision; Training Administrator cannot mark own training complete. |

### 5.7 Competency Management + Re-training + Expiry

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-COMP-01 | H | R1 | Competency records shall be bound to user_id; each competency shall be sourced from one or more completed trainings. |
| URS-COMP-02 | H | R1 | Annual / configurable refresher cycles per role; expiry alerts at D-60 / D-30 / D-7 / D-0; expiry shall revoke production access in consumer systems via the access-gating API. |
| URS-COMP-03 | H | R1 | Document-update triggers (EDMS new effective version of a training-bound document) shall trigger re-training tasks for affected users. |
| URS-COMP-04 | M | R2 | Competency dashboard shall surface per-role + per-site + per-user competency status; gaps shall be highlighted. |
| URS-COMP-05 | M | R2 | Role-change auto-enroll shall avoid race conditions where leaver event arrives before joiner-in-new-role event; reconciliation queue shall handle ordering. |

### 5.8 Compliance Dashboard + Reporting

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DASH-01 | H | R1 | Compliance Dashboard shall surface per-site + per-department + per-role training currency, overdue, expiring, expired. |
| URS-DASH-02 | M | R2 | Standard reports: Training Currency, Overdue Trainings, Curriculum Effectiveness, CAPA Training Completion, R&U Completion, Audit-Trail Review Summary. |
| URS-DASH-03 | M | R2 | Inspection-readiness export of per-user + per-role training-history package shall complete in ≤ 4 hours. |
| URS-DASH-04 | L | R3 | Ad-hoc report builder available to Head of Learning Operations + Head of QA. |

### 5.9 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-EDMS-01 | H | R1 | Vault QualityDocs (Vellis) controlled-document effective-date events shall trigger R&U tasks via Vault Connect. |
| URS-INT-EQMS-01 | H | R1 | MasterControl eQMS (Talos Bio) CAPA-driven training tasks shall be created via REST; idempotent per CAPA-id + revision. |
| URS-INT-HR-01 | H | R1 | Joiner / mover / leaver feed from HR via SCIM 2.0 (preferred) or SFTP per HR-contract. |
| URS-INT-SSO-01 | H | R1 | Okta SAML 2.0 + MFA + SCIM 2.0 provisioning. |
| URS-INT-APP-01 | H | R1 | GxP applications shall consume training-currency status via documented REST API; non-current users shall not access GxP applications gated on the relevant training. |

### 5.10 Performance, Availability, Backup, Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | Course load / list response ≤ 3 s at 95th percentile. |
| URS-AV-01 | H | R1 | Availability per Cornerstone SLA. |
| URS-BAK-01 | H | R1 | Vendor-managed backup; site shall verify vendor-published RPO ≤ 4 h, RTO ≤ 24 h annually. |
| URS-SEC-01 | H | R1 | TLS 1.3 in transit + AES-256 at rest. |
| URS-SEC-02 | H | R1 | Per-site + per-role access control; cross-site visibility restricted per organisational hierarchy. |
| URS-SEC-03 | M | R2 | Annual penetration testing of learner + admin endpoints. |

### 5.11 Training (LMS administrator + R&U content steward) + Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | LMS administrator training shall be completed before any user receives administrative permissions. |
| URS-TRN-02 | M | R2 | Annual refresher for LMS administrators covering Cornerstone release-note impact, SCORM/xAPI/cmi5 spec updates, 21 CFR § 211.25 + EU GMP Chapter 2 updates. |
| URS-PR-01 | H | R1 | Annual Periodic Review shall cover curriculum inventory + currency, audit-trail review evidence, vendor-assurance status, integration health, expiring-certifications backlog, compliance-dashboard summary; signed by Head of Learning Operations + Head of QA. |

### 5.12 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is SAML 2.0 via Entra ID with SCIM lifecycle provisioning; conditional-access policy `Standard SaaS Conditional Access (MFA + device-compliance)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the Cornerstone OnDemand metadata mirror; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 10 y (training record beyond worker tenure) per the consuming-record schedule. |

### 5.13 Cross-System Integration — EDMS handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-EDMS-01 | H | R1 | On every EDMS controlled-document version transition (DRAFT → EFFECTIVE), the LMS shall automatically re-assign the linked training curriculum to all users currently assigned to the prior version and shall set the completion deadline per the document's risk-class (Critical 30 d / Major 60 d / Minor 90 d). |

## 6. Acceptance Criteria

1. CS, RA, IQ (vendor-shared), OQ, PQ approved + executed.
2. PQ shall include representative end-to-end training: joiner → curriculum auto-enrollment → R&U from EDMS → quiz → completion → access gating + role change (mover) → curriculum re-evaluation + expiry → re-training → access revocation on expiry.
3. VSR approved by VP People & Culture + Head of QA.
4. RTM demonstrating every URS-ID maps to ≥ 1 approved test case.

## 7. Constraints

- Vendor releases not under site change control; impact-assessed within 14 days.
- Content authoring tools out of scope but SCORM 2004 / xAPI 1.0.3 / cmi5 conformance required.

## 8. Assumptions

- HR, EDMS, eQMS, Okta, GxP-consuming applications are validated independently and stable per documented contracts.
- CAPA training tasks are correctly tagged in eQMS.
- Cornerstone maintains SOC 2 + ISO 27001 certifications.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- 21 CFR § 211.25 — Personnel qualifications.
- 21 CFR § 211.180 — Records retention.

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EU GMP Chapter 2 — Personnel.
- EU GMP Annex 1 § 7 — Training for sterile manufacturing.

### International — ICH
- ICH Q10 — Pharmaceutical Quality System.

### Industry standards
- ADL SCORM 2004 4th Edition.
- ADL Experience API (xAPI / Tin Can) 1.0.3.
- ADL cmi5 — xAPI profile for LMS interoperability.
- AICC HACP (legacy reference).
- ISO 9001:2015 — Quality Management Systems.
- ISO 13485:2016 — Medical Devices QMS.
- ISPE GAMP 5 (2nd Edition, 2022).
- PIC/S PI 041.
- ISO/IEC 27001:2022.

### Privacy
- GDPR Arts. 6, 32.

### Vendor
- Cornerstone OnDemand — *Learning 2025 Validation Approach* (vendor white paper).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

