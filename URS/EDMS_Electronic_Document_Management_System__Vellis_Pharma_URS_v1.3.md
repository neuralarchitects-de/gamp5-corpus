---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-26; expanded 2026-05-12 (T3 uplift, document lifecycle, document-type library, training linkage, periodic-review automation, audit-trail review, OCR for legacy paper, inspection redaction, ISO 9001/13485 binding)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed., 2022) Cat 4 conventions for SaaS configurable platforms"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "ICH Q10 — Pharmaceutical Quality System"
  - "ISO 9001:2015 §7.5 Documented Information"
  - "ISO 13485:2016 §§ 4.2.4, 4.2.5 Control of documents and records"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026; supersedes the September 2025 guidance)"
  - "PIC/S PI 041; ISO/IEC 27001:2022"
  - "Veeva Vault QualityDocs 24R3 + 25R1 Validation Approach"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## EDMS — Veeva Vault QualityDocs (24R3 → 25R1)

**Document Number:** VLP-URS-EDMS-001
**Version:** 1.0
**Effective Date:** 2026-04-26 *(synthetic)*
**Site:** Vellis Pharma Holdings, Global QA Operations, Madrid Headquarters, Spain *(fictional)*
**System Owner:** Head of Document Control
**Process Owner:** VP Quality Assurance
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS; vendor handles infrastructure; site configuration validated)
**Project Mode:** Configuration project on commercial software product **Veeva Vault QualityDocs (24R3 → 25R1)** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11; ICH Q10; ISO 9001:2015 §7.5; ISO 13485:2016 §§ 4.2.4, 4.2.5

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of Document Control) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Vendor Assurance — Veeva relationship owner) | _____________ | _____________ | _____ |
| Reviewer (Data Integrity Officer) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue (Tier T3 — 116 requirements covering document lifecycle, doc-type library + naming, training-record linkage, periodic-review automation, audit-trail review tools, legacy paper OCR, inspection redaction, search + retrieval, multi-site federation, ISO 9001 / 13485 alignment). |

## Definitions

| Term | Definition |
|---|---|
| EDMS | Electronic Document Management System |
| Vault | Veeva Vault QualityDocs platform |
| 24R3 / 25R1 | Veeva Vault Releases (cadenced quarterly) |
| Lifecycle | Document state machine (DRAFT → IN-REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE) |
| Doc Type | Vault doc-type configuration governing fields, lifecycle, and permissions |
| Renditions | Auto-generated PDF rendition of approved Vault documents |
| Periodic Review | Cadenced review per doc type (e.g., 24-month SOP review) |
| OCR | Optical Character Recognition for legacy-paper ingestion |
| eQMS | MasterControl QMS |
| LMS | Learning Management System (Cornerstone OnDemand) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the EDMS that Vellis Pharma uses globally for controlled SOPs, work instructions, master batch records, validation deliverables, regulatory submissions support, quality manuals, and legacy-paper records ingested via OCR.

## 2. Scope

**In scope:** Veeva Vault QualityDocs 24R3 → 25R1 multi-tenant SaaS instance; site configuration (doc types, lifecycles, security profiles, group / role mapping, custom fields, atomic security, naming convention enforcement); integrations with eQMS (MasterControl) for change-control linkage, LMS (Cornerstone) for read-and-understood task creation, PAS-X (MES) for URN resolution of master batch records, the legacy-paper-OCR pipeline, and the inspection-redaction tooling; SSO via Okta SAML 2.0; vendor-assurance program covering Veeva.

**Out of scope:** Veeva infrastructure (handled per Veeva's customer-shared CSV evidence and SOC 2 Type II); training content; controlled records produced from documents (e.g., executed batch records — managed by PAS-X).

```
                     Okta SAML 2.0 + MFA
                            │
   ┌────────────────────────▼────────────────────────────────┐
   │     Veeva Vault QualityDocs 24R3 / 25R1 (multi-tenant)    │
   │     Doc types │ Lifecycles │ Security │ Renditions │ OCR  │
   └────────────────────────┬────────────────────────────────┘
                            │
            ┌───────────────┼────────────────┬──────────────┐
            ▼               ▼                ▼              ▼
       MasterControl    Cornerstone     PAS-X / MES      OCR + Redaction
       (change control  (training       (URN consume)    pipeline
        linkage)         tasks)
```

## 3. System Description and Intended Use

Vault QualityDocs is the system of record for controlled-document creation, review, approval, distribution, periodic review, and retirement across the Vellis Pharma global QA + manufacturing landscape. Documents progress through DRAFT → IN-REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE with role-restricted signatures at each transition. Legacy paper records are ingested via OCR with documented re-validation. An inspection-redaction tool produces inspection-ready copies with redacted personal data, residual-risk markings, and watermarks.

GAMP Cat 4: Vendor maintains infrastructure and platform under their published SDLC and shared CSV deliverables (Veeva Trust Site, SOC 2 Type II, customer-shared IQ/OQ); site validation focuses on configuration (doc types, lifecycles, security), the integration boundary with MasterControl + Cornerstone + PAS-X + OCR, naming-convention enforcement, training-record linkage gating, periodic-review automation, and 21 CFR Part 11 controls.

## 4. User Roles

| Role | Permissions |
|---|---|
| Author | Create / edit DRAFT documents; submit for review. |
| Reviewer | Review documents; cannot approve. |
| Approver | Approve documents to EFFECTIVE; cannot review own. |
| Reader | Read EFFECTIVE documents in scope; acknowledge read-and-understood. |
| Document Coordinator | Manage document metadata, doc-type assignment, retirement; cannot approve. |
| Naming-Convention Steward | Author / approve naming-convention rules. |
| Periodic Review Coordinator | Schedule + monitor periodic reviews per doc-type cadence. |
| OCR Operator | Ingest legacy paper records via OCR pipeline; cannot finalise. |
| OCR Verifier (QA) | Verify OCR-ingested records vs original paper; finalise EFFECTIVE only after dual-check. |
| Inspection Redactor | Produce redacted copies for regulator inspection; cannot approve EFFECTIVE. |
| Vault Administrator | Configure doc types, lifecycles, security profiles; cannot approve documents. |
| Auditor | Read-only across documents and audit trails. |

Separation of duties: Author ≠ Reviewer ≠ Approver of the same document; OCR Operator ≠ OCR Verifier; Naming-Convention Steward ≠ Author; Periodic Review Coordinator ≠ Approver for triggered reviews.

## 5. User Requirements

Each requirement carries a unique ID, priority, GAMP-5 risk classification, and a verifiable `shall`-clause.

### 5.1 Vendor / Platform Assurance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-01 | H | R1 | Veeva shall be qualified as a critical SaaS vendor with documented vendor-assurance evidence: SOC 2 Type II, ISO 27001, customer-shared IQ/OQ for the Vault platform, and a continuing-supplier-qualification cadence. |
| URS-VND-02 | H | R1 | Each Vault Release (quarterly) shall be assessed for impact via Veeva-supplied release notes; site re-validation evidence shall focus on configuration-affecting changes. |
| URS-VND-03 | M | R2 | Service-availability KPIs (≥ 99.7% per Veeva SLA) shall be monitored and reviewed quarterly. |
| URS-VND-04 | M | R2 | Vendor escalation runbook with named Veeva contacts shall be on file. |

### 5.2 Document Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-LC-01 | H | R1 | Documents shall progress through DRAFT → IN-REVIEW → APPROVED → EFFECTIVE → SUPERSEDED → OBSOLETE; non-controlled informational doc types are out of scope. |
| URS-LC-02 | H | R1 | Lifecycle transitions shall require role-restricted signatures with Vault's atomic security (record-level permissions). |
| URS-LC-03 | H | R1 | EFFECTIVE documents shall be immutable in content; new versions shall be produced via a managed change request linked to MasterControl change control. |
| URS-LC-04 | H | R1 | A SUPERSEDED transition shall update the prior EFFECTIVE rendition to "SUPERSEDED" and link the new EFFECTIVE doc-id. |
| URS-LC-05 | H | R1 | OBSOLETE documents shall be marked obsolete with effective-date and shall remain searchable for inspection. |
| URS-LC-06 | M | R2 | Lifecycle transition timing (e.g., DRAFT-to-IN-REVIEW SLA, IN-REVIEW-to-APPROVED SLA) shall be configurable per doc type. |

### 5.3 Document Type Library and Naming Convention

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DT-01 | H | R1 | Site shall configure controlled doc types: SOP, Work Instruction, Master Batch Record, Validation Plan / Protocol / Report, Quality Manual, Risk Assessment, Specification, Form / Template, Policy; each with documented metadata schema. |
| URS-DT-02 | H | R1 | Each doc type shall declare its lifecycle, default reviewer / approver roles, retention class, and training-impact flag. |
| URS-DT-03 | H | R1 | Doc-type changes shall require Naming-Convention Steward sign-off and Vault Admin approval; legacy documents shall not be retroactively retitled. |
| URS-DT-04 | H | R1 | Naming-convention rules per doc type (e.g., `SOP-<dept>-<area>-<seq>`) shall be enforced at document creation; non-conforming filenames shall be rejected. |
| URS-DT-05 | M | R2 | The doc-type library shall surface counts by lifecycle state, periodic-review due, and last-modified per type. |

### 5.4 Authoring, Review, Approval

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-WF-01 | H | R1 | Authors shall be able to create / edit DRAFT documents; the system shall enforce metadata completeness before submission to review. |
| URS-WF-02 | H | R1 | The system shall support parallel and sequential review/approval routes configurable per doc type. |
| URS-WF-03 | H | R1 | Reviewers and Approvers shall sign electronically with re-authentication at the moment of signing. |
| URS-WF-04 | H | R1 | Rejection at any stage shall return the document to DRAFT with the rejection reason recorded; the original signature trail shall be preserved. |
| URS-WF-05 | M | R2 | Author shall be notified within 5 minutes of any state transition affecting their document. |
| URS-WF-06 | M | R2 | Bulk-approve mode shall be denied; signatures shall require per-document view. |

### 5.5 Renditions, Watermarking, Distribution

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REND-01 | H | R1 | On transition to EFFECTIVE the system shall generate a controlled PDF rendition with watermark "EFFECTIVE — copy is uncontrolled when printed". |
| URS-REND-02 | H | R1 | Superseded renditions shall be marked "SUPERSEDED" with the effective date of the replacement and a reference to the new doc ID. |
| URS-REND-03 | H | R1 | Renditions shall include a signature page listing signer, role, meaning, date / time, and document hash at the time of signing. |
| URS-REND-04 | M | R2 | Reader access to the latest EFFECTIVE rendition shall be ≤ 60 seconds after promotion; offline distribution shall require a documented exception. |
| URS-REND-05 | M | R2 | A printable cover-page for Inspection-Ready PDFs shall list document hash, current effective date, signer chain, and naming-convention compliance. |

### 5.6 Training Record Linkage

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRAIN-01 | H | R1 | New / revised EFFECTIVE controlled documents flagged as training-impacting shall trigger read-and-understood training tasks in Cornerstone for the assigned audience. |
| URS-TRAIN-02 | H | R1 | Reader access to documents requiring training shall be permitted only after the training task is completed. |
| URS-TRAIN-03 | H | R1 | When a document moves SUPERSEDED, prior training records shall remain attached for inspection; superseded-document training shall not be deleted. |
| URS-TRAIN-04 | M | R2 | Training-impact flagging shall be configurable per doc type; flagged transitions shall surface training-cycle estimates. |
| URS-TRAIN-05 | M | R2 | The system shall surface training-completion KPIs per audience for management review. |

### 5.7 Periodic Review Automation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PRA-01 | H | R1 | Periodic review cadence per doc type (e.g., SOP: 24 months; Master Batch Record: 12 months; Quality Manual: 36 months) shall trigger automated review tasks. |
| URS-PRA-02 | H | R1 | Overdue periodic reviews shall create eQMS deviations after a configured grace window. |
| URS-PRA-03 | M | R2 | Periodic-review outcomes (no-change / minor / major) shall route to the appropriate change-control workflow. |
| URS-PRA-04 | M | R2 | A periodic-review dashboard shall surface upcoming / overdue reviews per doc-type. |

### 5.8 Audit-Trail Review Tools

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Vault audit trail shall capture all document-state transitions, content changes, metadata edits, security changes, and user-access events per § 11.10(e). |
| URS-AUD-02 | H | R1 | Audit-trail entries shall be append-only and exportable as CSV / PDF for inspection. |
| URS-AUD-03 | H | R1 | Audit-trail review per Annex 11 § 9 shall be performed monthly by Document Coordinator and quarterly by QA Compliance. |
| URS-AUD-04 | H | R1 | Retention shall be ≥ 25 years post-retirement of a document. |
| URS-AUD-05 | H | R1 | A focused-audit-trail-review tool shall filter to material events (signatures, naming-convention overrides, OCR finalisations, redaction operations, mass deletions, role-permission edits). |
| URS-AUD-06 | M | R2 | Audit-trail review evidence shall be exportable for inspection with chain-of-custody preservation. |

### 5.9 21 CFR Part 11 / Annex 11

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Per § 11.10(a) procedural controls shall protect document validity. |
| URS-PART11-02 | H | R1 | Per § 11.10(b) accurate + complete copies shall be exportable for inspection (PDF/A-3 + CSV). |
| URS-PART11-03 | H | R1 | Per § 11.10(d) access shall be limited to authorised individuals via Okta SAML 2.0 + MFA. |
| URS-PART11-04 | H | R1 | Per § 11.50 e-signatures shall include the signer's printed name, date and time, and meaning of signature. |
| URS-PART11-05 | H | R1 | Per § 11.70 signatures shall be cryptographically bound to the document hash at the moment of signing. |
| URS-PART11-06 | H | R1 | Per § 11.100 signatures shall be unique to a single individual; no reuse / reassignment. |
| URS-PART11-07 | H | R1 | Per § 11.200 re-authentication shall be required at the moment of signing. |
| URS-PART11-08 | H | R1 | Per § 11.300 password / credential controls per site InfoSec policy shall be enforced. |
| URS-ANX11-01 | H | R1 | Per Annex 11 § 4 validation evidence shall be maintained current. |
| URS-ANX11-02 | H | R1 | Per Annex 11 § 6 accuracy checks shall be enforced at metadata-entry boundaries. |

### 5.10 Legacy Paper OCR Workflow

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-OCR-01 | H | R1 | Legacy paper documents shall be ingested via OCR with documented operator-batch identifier, scan device, scan timestamp, and OCR engine + version. |
| URS-OCR-02 | H | R1 | OCR-ingested records shall require an OCR-Verifier QA second-pass comparison vs the original paper before they can be promoted to EFFECTIVE. |
| URS-OCR-03 | H | R1 | The OCR Verifier signature shall be SoD-segregated from the OCR Operator signature. |
| URS-OCR-04 | M | R2 | OCR confidence scores below a configured threshold (e.g., 95% per character) shall force a manual verification step. |
| URS-OCR-05 | M | R2 | The original paper shall be retained per the retention policy; the link to the original shall be maintained in the EDMS. |

### 5.11 Inspection Redaction Mode

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RED-01 | H | R1 | The Inspection Redactor role shall be able to produce redacted copies of EFFECTIVE documents for regulator inspection without altering the controlled record. |
| URS-RED-02 | H | R1 | Redacted copies shall carry watermark "INSPECTION COPY — REDACTED — *date*" and an audit-trail entry of the redaction. |
| URS-RED-03 | H | R1 | Redactions shall not be reversible from the redacted PDF; the original shall remain in Vault under its current security profile. |
| URS-RED-04 | M | R2 | Bulk-redaction operations shall be limited to Inspection Redactor + Vault Admin and shall surface in the focused audit-trail-review tool. |

### 5.12 Document Search and Retrieval

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEARCH-01 | H | R1 | The system shall support full-text + structured-field search across documents with role-respecting permissions. |
| URS-SEARCH-02 | H | R1 | Inspection-mode retrieval shall return any requested EFFECTIVE document within 4 hours during an active inspection. |
| URS-SEARCH-03 | M | R2 | Search results shall surface the document's doc-type, lifecycle state, effective-date, naming-convention compliance, periodic-review due-date. |
| URS-SEARCH-04 | M | R2 | Saved queries shall be supported and exportable for inspection. |

### 5.13 Multi-Site Federation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-FED-01 | H | R1 | Master data (doc types, naming-convention rules, role definitions) shall federate across regional Vault domains (EMEA, NA, APAC) with documented authoritative-site rules. |
| URS-FED-02 | M | R2 | Cross-region document linkage shall preserve the source-region audit trail. |

### 5.14 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-EQMS-01 | H | R1 | EFFECTIVE document IDs shall be referenceable from MasterControl change control; broken references shall be flagged in monthly reconciliation. |
| URS-INT-LMS-01 | H | R1 | New / revised EFFECTIVE controlled documents shall trigger read-and-understood training tasks in Cornerstone (idempotent on document-version-id). |
| URS-INT-LMS-02 | H | R1 | Reader access to documents requiring training shall be permitted only after the training task is completed. |
| URS-INT-PASX-01 | H | R1 | PAS-X (MES) shall consume Master Batch Record URNs; URN-resolution failures shall be alerted within 5 minutes. |
| URS-INT-OCR-01 | M | R2 | The OCR pipeline shall integrate via REST with documented operator + verifier metadata. |
| URS-INT-SSO-01 | H | R1 | All authentication shall be via Okta SAML 2.0 + MFA. |

### 5.15 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | Records shall be Attributable to a named user. |
| URS-DI-02 | H | R1 | Records shall be Legible — exportable as PDF/A-3 with standard fonts; no proprietary-only viewers. |
| URS-DI-03 | H | R1 | Records shall be Contemporaneous — timestamps from Vault's NTP-synced infrastructure. |
| URS-DI-04 | H | R1 | Original document content shall be preserved unaltered; renditions reference but do not overwrite. |
| URS-DI-05 | H | R1 | Workflow logic shall be Accurate per OQ. |
| URS-DI-06 | M | R2 | Complete / Consistent / Enduring (25-yr retention) / Available (≤ 4 hours during inspection). |

### 5.16 Backup / DR and Site Responsibilities

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-BAK-01 | H | R1 | Veeva backups and DR shall be vendor-managed; site shall verify Veeva's published RPO ≤ 4 hours and RTO ≤ 24 hours via the vendor-assurance program. |
| URS-BAK-02 | M | R2 | Site shall maintain an annual configuration export (doc types, lifecycles, security profiles, naming-convention rules) for traceability and worst-case migration. |

### 5.17 Performance / Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | Document open / search response ≤ 3 s at the 95th percentile under nominal site load. |
| URS-PERF-02 | M | R2 | Bulk import (≥ 1,000 documents) shall complete within 4 hours with progress reporting. |
| URS-AV-01 | H | R1 | Site availability target shall align with Veeva's published SLA (≥ 99.7%). |
| URS-SEC-01 | H | R1 | All access shall be via Okta SSO + MFA; no local accounts other than break-glass. |
| URS-SEC-02 | H | R1 | Document download with watermark shall be required for external sharing; uncontrolled bulk export shall be prohibited. |
| URS-SEC-03 | M | R2 | Bulk-export events shall trigger audit-trail review. |

### 5.18 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Production access shall require recorded role-specific training (LMS). |
| URS-TRN-02 | M | R2 | OCR Verifier + Inspection Redactor shall complete an advanced inspection-readiness training. |
| URS-PR-01 | H | R1 | An annual periodic review per Annex 11 § 11 shall cover configuration drift, audit-trail review evidence, vendor-assurance status, integration health, training currency, naming-convention compliance, periodic-review-task currency, and fitness for use; signed by Head of Document Control and VP QA. |

### 5.19 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is SAML 2.0 via Entra ID with SCIM lifecycle provisioning; conditional-access policy `Quality-App Conditional Access (MFA + device-compliance for controlled-document e-signature)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the Vault metadata DB plus object-replica for controlled-document binaries; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 25 y (regulated SOP/Spec) per the consuming-record schedule. |

### 5.20 Cross-System Integration — Helios audit-trail handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HEL-01 | H | R1 | Vault EDMS shall publish audit-trail events (Controlled-document lifecycle (DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE), e-signature, and reason-for-change events) to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract (JSON Lines, schema-registry pinned, Kafka topic `helios.ingest.vellis.vault.v1`) within 5 minutes of event capture; 21 CFR § 11.10(e) audit-trail completeness shall be preserved end-to-end so that no event class is lost at the boundary. |
| URS-XINT-HEL-02 | H | R1 | Pre-handover audit-trail retention on the Vault EDMS side shall be ≥ 25 y regardless of Helios availability; once Helios acknowledges ingest (per-message ack with idempotency key), Helios is the system-of-record for review and the Vault EDMS local copy serves as the durability backstop until the local retention floor expires. |

## 6. Acceptance Criteria

The system shall enter validated GMP use when CS (configuration), RA, IQ (configuration verification — vendor-shared infra IQ accepted), OQ (workflow / signature / integration / OCR / redaction), PQ (representative end-to-end documents through full lifecycle including LMS training task, OCR-ingested legacy record finalisation, inspection-redaction export, periodic-review trigger) are approved and executed; vendor-assurance evidence shall be reviewed and accepted; the VSR shall be approved by Head of Document Control + VP QA; the RTM shall map every URS to ≥ 1 approved test case.

## 7. Constraints

- Veeva Releases are quarterly and not under site change control.
- Site impact assessment shall be completed within 14 days of release notes.
- Configuration baselines shall be re-tested as needed.
- Bulk-approve mode is denied.

## 8. Assumptions

- Okta, Cornerstone, MasterControl, PAS-X are independently validated.
- Veeva publishes accurate release notes and continues to maintain SOC 2 Type II.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EU GMP Chapter 4 — Documentation

### International — ICH
- ICH Q10 — Pharmaceutical Quality System

### Industry / Quality
- ISO 9001:2015 §7.5 — Documented Information
- ISO 13485:2016 §§ 4.2.4, 4.2.5 — Control of documents and records
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE GAMP Good Practice Guide: *Records and Data Integrity*
- PIC/S PI 041
- ISO/IEC 27001:2022

### Vendor
- Veeva — *Vault QualityDocs 24R3 / 25R1 Validation Approach* (vendor white paper)
- Veeva Trust Site (current SOC 2 / ISO 27001)

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

