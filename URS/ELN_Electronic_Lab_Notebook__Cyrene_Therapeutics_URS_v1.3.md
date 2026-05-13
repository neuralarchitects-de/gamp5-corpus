---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-27; expanded 2026-05-12 (T3 uplift, study/experiment lifecycle, Registry, witness workflow, GMP vs R&D mode separation, schema-version mgmt)"
seed_corpus_basis:
  - "GAMP 5 (2nd ed., 2022) Cat 4 conventions for SaaS configurable platforms"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11"
  - "FDA Computerized Systems Used in Clinical Investigations (2007 + updates)"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026; supersedes the September 2025 guidance)"
  - "PIC/S PI 041; ICH Q9(R1); ICH Q10"
  - "ISPE GAMP Good Practice Guide: A Risk-Based Approach to Compliant ELN"
  - "Benchling — Biotech R&D 2025 Validation Approach"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed, prompt-tuning evaluation, reference template]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## ELN — Benchling for Biotech R&D 2025 (Cloud SaaS)

**Document Number:** CYR-URS-ELN-001
**Version:** 1.0
**Effective Date:** 2026-04-27 *(synthetic)*
**Site:** Cyrene Therapeutics Ltd., R&D + Process Development, Cambridge, United Kingdom *(fictional)*
**System Owner:** Head of R&D Informatics
**Process Owner:** VP Research / VP Process Development
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS; vendor handles infrastructure; site validates per-template configuration)
**Project Mode:** Configuration project on commercial software product **Benchling for Biotech R&D 2025 (Cloud SaaS)** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300 (where ELN entries are GxP records); EU GMP Annex 11 §§ 4, 6, 9, 11 (early-phase manufacturing entries); ICH Q10 (PQS-relevant entries); ICH Q9(R1); FDA *Computerized Systems Used in Clinical Investigations* (where ELN supports clinical-phase laboratory work)

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of R&D Informatics) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Vendor Assurance — Benchling owner) | _____________ | _____________ | _____ |
| Reviewer (Data Integrity Officer) | _____________ | _____________ | _____ |
| Approver (VP Research) | _____________ | _____________ | _____ |
| Approver (VP Quality Assurance) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue (Tier T3 — 108 requirements covering study + experiment lifecycle, schema + template registry, witness workflow, Registry + Inventory, GMP vs R&D mode separation, method linkage, search + indexing, vendor assurance, Annex 11 §§ 4/6/9/11). |

## Definitions

| Term | Definition |
|---|---|
| ELN | Electronic Lab Notebook |
| Benchling | Benchling for Biotech R&D 2025 |
| Study | A collection of related experiments (project / programme scope) |
| Experiment / Notebook Entry | The atomic ELN record — a versioned, signable lab note |
| Template | Pre-configured entry layout with required fields, calculations, attachments |
| Schema | The data-model layer underpinning a Registry / template field |
| Registry | Benchling's structured biological-entity catalogue (DNA, protein, plasmid, cell line, antibody) |
| Inventory | Benchling's reagent / sample / freezer location tracking |
| Workflow | Benchling task / lifecycle automation |
| GMP-tagged entry | Entry classified as a GxP record under site policy |
| LIMS | LabWare LIMS 8 (downstream QC system, separate URS) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for the ELN platform used at Cyrene Therapeutics across discovery research, process development, and early-phase manufacturing for capturing experiments, protocols, results, and lab observations as 21 CFR Part 11 / Annex 11–compliant electronic records.

## 2. Scope

**In scope:** Benchling 2025 multi-tenant SaaS instance; per-template configuration of ELN entries (research, PD, early-phase mfg); Study + Experiment hierarchy; per-schema Registry + Inventory configuration; Workflow configuration; SSO via Okta SAML 2.0 + MFA; integrations with Vault QualityDocs (controlled-document linkage), LIMS (sample-result linkage), eQMS (deviation creation from lab observations), GitHub (protocol-as-code linkage for computational protocols), and the site Active Directory; vendor-assurance program covering Benchling.

**Out of scope:** Benchling's underlying cloud infrastructure (vendor); discovery-research entries explicitly tagged "non-GxP" (still tracked but not validated as regulated records); training-content authoring (LMS); product-specification documents (Vault).

## 3. System Description and Intended Use

The ELN is the system of record for laboratory experiments and observations. Studies group related experiments. Each entry is created from an approved template, populated by the lab scientist, witnessed by a peer scientist for critical steps, and signed when complete. Entries can link to Registry entities (e.g., the cell line used) and Inventory items (e.g., the lot of media). GMP-tagged entries are subject to GxP controls (Part 11 signatures, audit trail, retention). The R&D-mode (non-GxP) and GMP-mode streams are functionally separated to avoid cross-contamination of records.

GAMP Cat 4: Benchling maintains the platform under their published SDLC; the vendor publishes customer-shared CSV evidence. Site validation focuses on template configuration, Workflow / Registry / Inventory schema configuration, integration boundaries, GMP-mode separation, and 21 CFR Part 11 controls applied to GMP-tagged entries.

## 4. User Roles

| Role | Permissions |
|---|---|
| Scientist | Create / edit own entries; import data; add attachments. |
| Peer Reviewer / Witness | Witness entries (second-person verification on critical entries). |
| Lab Lead | Approve entries; cannot witness own. |
| Template Author | Create / edit entry templates under change control. |
| Template Approver (QA + Lab Lead) | Approve templates to PRODUCTION. |
| Schema Author | Author / version Registry + entry schemas. |
| Schema Approver (QA + R&D Informatics) | Approve schema versions. |
| Registry Curator | Curate Registry entities (DNA / protein / cell line records). |
| Study Lead | Manage study scope, members, schema bindings. |
| GMP Mode Steward | Approve transitions between R&D and GMP modes for a project / study. |
| ELN Administrator | User / role provisioning, AD groups; cannot approve entries. |
| Auditor | Read-only across entries, audit trails, configuration. |

Separation of duties: Scientist ≠ Witness ≠ Approver of the same entry; Template Author ≠ Template Approver; Schema Author ≠ Schema Approver; Study Lead ≠ GMP Mode Steward.

## 5. User Requirements

Each requirement carries a unique ID, priority, GAMP-5 risk classification, and a verifiable `shall`-clause.

### 5.1 Vendor / Platform Assurance

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VND-01 | H | R1 | Benchling shall be qualified as a critical SaaS vendor with documented evidence: SOC 2 Type II, ISO 27001, customer-shared CSV summary, BAA where PHI data may be present. |
| URS-VND-02 | H | R1 | Vendor releases (cadenced) shall be impact-assessed within 14 days; configuration-affecting changes shall trigger re-validation of affected templates. |
| URS-VND-03 | M | R2 | Service-availability KPIs (≥ 99.7% per Benchling SLA) shall be monitored and reviewed quarterly. |
| URS-VND-04 | M | R2 | A formal vendor escalation runbook shall exist with named Benchling contacts and SLA recovery expectations. |

### 5.2 Study and Experiment Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-STUDY-01 | H | R1 | Studies shall be the top-level grouping for related experiments; each study shall declare its mode (R&D or GMP) and the controlled-documents (SOPs, master formulae) it references. |
| URS-STUDY-02 | H | R1 | A study's mode shall be set at creation and shall require GMP Mode Steward signature for any change; mode-changes shall not retroactively recategorise existing entries. |
| URS-STUDY-03 | M | R2 | The system shall surface study-level summaries (entry count by state, witness backlog, mode, last-activity). |
| URS-EXP-01 | H | R1 | Each experiment shall belong to exactly one study and shall inherit the study's mode and controlled-document references. |
| URS-EXP-02 | H | R1 | Experiments shall progress through lifecycle DRAFT → IN-PROGRESS → READY-FOR-WITNESS → READY-FOR-APPROVAL → APPROVED → LOCKED; reverse transitions shall require captured reason + signature. |
| URS-EXP-03 | H | R1 | Locked experiments shall be read-only; correction shall require an unlock + amendment workflow. |
| URS-EXP-04 | M | R2 | Experiments shall support computational sections that link to GitHub commits (notebook + code + data snapshot); the commit SHA shall be embedded on signing. |

### 5.3 Schema and Template Registry

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SCHEMA-01 | H | R1 | Registry and entry schemas shall be version-controlled; schema versioning shall preserve prior versions; entries shall bind to the schema version effective at entry creation. |
| URS-SCHEMA-02 | H | R1 | Schema promotion to EFFECTIVE shall require Schema Author ≠ Schema Approver SoD. |
| URS-SCHEMA-03 | H | R1 | Schema changes that affect required fields on prior entries shall trigger an impact assessment; existing entries shall not be retroactively invalidated without a documented migration. |
| URS-TPL-01 | H | R1 | Each template shall progress DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE; only EFFECTIVE templates may be selected for new GMP entries. |
| URS-TPL-02 | H | R1 | Template promotion to EFFECTIVE shall require role-restricted electronic signatures with separation of duties (Author ≠ Approver). |
| URS-TPL-03 | H | R1 | Template UAT shall execute documented test scripts covering required-field validation, calculation logic, attachment handling, witness flow, and amendment unlock. |
| URS-TPL-04 | H | R1 | Template versioning shall preserve prior versions; entries created against a prior version shall remain bound to that version. |
| URS-TPL-05 | M | R2 | Template inventory shall be searchable by mode, schema version, last-modified, and effective-date. |

### 5.4 Entry Creation, Witness, and Approval

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-ENT-01 | H | R1 | GMP-tagged entries shall be created from EFFECTIVE templates only; non-GxP discovery entries may use a wider template set tagged accordingly. |
| URS-ENT-02 | H | R1 | Entries shall capture: scientist (creator), date / time, linked Registry entities, Inventory items consumed, raw observations, calculations, attachments. |
| URS-ENT-03 | H | R1 | Critical entries (process-development batch records, early-phase-mfg observations, in-process tests) shall be witnessed by a peer scientist with a separate signature. |
| URS-ENT-04 | H | R1 | Entry approval by Lab Lead shall require a re-authenticated electronic signature; Lab Lead shall not witness their own approval. |
| URS-ENT-05 | H | R1 | Post-approval entry edits shall require an unlock workflow with justification and re-approval signatures. |
| URS-ENT-06 | H | R1 | Witness-signature SoD: Scientist ≠ Witness ≠ Approver; the system shall enforce at signature submission. |
| URS-ENT-07 | M | R2 | Witness deadline shall be configurable per template; overdue witness entries shall surface in the Lab-Lead inbox. |
| URS-ENT-08 | M | R2 | Bulk witness mode shall be supported only when each entry is individually opened + signed; one-click bulk-sign without per-entry view shall be denied. |

### 5.5 Registry and Inventory

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REG-01 | H | R1 | Registry entities (DNA, protein, plasmid, cell line, antibody) shall follow a documented schema with mandatory metadata; uncurated entities shall not be usable in GMP-tagged entries. |
| URS-REG-02 | H | R1 | Registry-entity provenance (origin, donor, vendor, lot, parent entity) shall be captured and shall be readable from any consuming entry. |
| URS-REG-03 | M | R2 | Registry entities shall support a deprecation lifecycle (active → deprecated) to manage cell-line drift or contamination. |
| URS-INV-01 | H | R1 | Inventory items shall have lot-id + expiry + location + status; entry-side consumption shall decrement quantity and link the lot to the entry. |
| URS-INV-02 | H | R1 | Expired or quarantined inventory shall not be consumable in GMP-tagged entries. |
| URS-INV-03 | M | R2 | Negative inventory (consumed > on-hand) shall be blocked at decrement-time; manual receipt adjustments shall be auditable. |

### 5.6 GMP vs R&D Mode Separation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MODE-01 | H | R1 | The system shall maintain functional separation between R&D and GMP streams: study mode shall determine the template / schema set available and the audit / retention policy. |
| URS-MODE-02 | H | R1 | An entry's mode shall be immutable after creation; conversion shall require creation of a fresh GMP entry referencing the source as evidence. |
| URS-MODE-03 | H | R1 | GMP-mode entries shall block consumption of non-curated Registry entities and expired Inventory. |
| URS-MODE-04 | M | R2 | The system shall surface mode-mismatch warnings when an experiment links to controlled documents inconsistent with its mode. |

### 5.7 Method Linkage (LIMS + Vault)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-METH-01 | H | R1 | LIMS sample IDs referenced in entries shall resolve to LIMS records; result back-flow shall appear in entries (read-only). |
| URS-METH-02 | H | R1 | Vault controlled-document URNs (SOPs, master formulae) shall be resolvable at entry-approval; broken references shall be flagged. |
| URS-METH-03 | M | R2 | When a referenced Vault document supersedes during an experiment's active life, the experiment shall display a notice and require Lab-Lead acknowledgement before approval. |

### 5.8 Search and Indexing

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SEARCH-01 | H | R1 | The system shall support full-text + structured-field search across entries with role-respecting permissions. |
| URS-SEARCH-02 | M | R2 | Search results shall surface the entry's mode, study, template version, and signature state. |
| URS-SEARCH-03 | M | R2 | Search shall support saved queries and shall be exportable for inspection within 4 hours. |

### 5.9 Audit Trail / Part 11

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | Audit trail shall capture all entry creation / edits / signatures / lock-unlock events, template configuration changes, Registry curation, Inventory transactions, schema version changes, and security changes per § 11.10(e). |
| URS-AUD-02 | H | R1 | Audit trail shall be append-only; reviewable in-app and exportable as CSV / PDF. |
| URS-AUD-03 | H | R1 | Audit-trail review per Annex 11 § 9 shall be performed monthly by R&D Informatics + QA; per-entry review at approval. |
| URS-AUD-04 | H | R1 | Retention shall be ≥ 25 years for GMP-tagged entries; ≥ 10 years for non-GxP entries; archived to immutable storage. |
| URS-AUD-05 | M | R2 | A focused-audit-trail-review tool shall filter to material events (signatures, mode changes, schema changes, unlock-edits). |
| URS-PART11-01 | H | R1 | Per § 11.10(a), procedural controls shall protect entry validity (validated SDLC, role definitions, change control). |
| URS-PART11-02 | H | R1 | Per § 11.10(b), entry copies shall be exportable as PDF/A-3 + CSV for inspection. |
| URS-PART11-03 | H | R1 | Per § 11.10(d), access shall be limited to authorised individuals via Okta SAML 2.0 + MFA. |
| URS-PART11-04 | H | R1 | Per § 11.50, e-signatures shall include printed name, date / time, and meaning. |
| URS-PART11-05 | H | R1 | Per § 11.70, signatures shall be cryptographically bound to entry state. |
| URS-PART11-06 | H | R1 | Per § 11.100, signatures shall be unique to a single individual; no reuse or reassignment. |
| URS-PART11-07 | H | R1 | Per § 11.200, re-authentication shall be required at every signature event. |
| URS-PART11-08 | H | R1 | Per § 11.300, password / credential controls per site InfoSec policy shall be enforced. |
| URS-ANX11-01 | H | R1 | Per Annex 11 § 4, validation evidence shall be kept current for site configuration. |
| URS-ANX11-02 | H | R1 | Per Annex 11 § 6, accuracy checks (range, format, plausibility) shall be applied to numeric calculation fields. |

### 5.10 Integrations

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-VAULT-01 | H | R1 | Controlled-document references (SOPs, master formulae) in entries shall resolve to Vault QualityDocs URNs; broken references shall be flagged at entry-approval. |
| URS-INT-LIMS-01 | M | R2 | LIMS sample IDs in entries shall link to LIMS records; result back-flow shall show in entries (read-only). |
| URS-INT-EQMS-01 | H | R1 | Lab observations classified as deviations shall create eQMS records via REST with idempotency. |
| URS-INT-GIT-01 | M | R2 | Computational-protocol references shall link to GitHub commits; commit SHA embedded on signature. |
| URS-INT-SSO-01 | H | R1 | Authentication shall be via Okta SAML 2.0 + MFA. |

### 5.11 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | Records shall be Attributable to a named user via Okta-bound identity. |
| URS-DI-02 | H | R1 | Records shall be Legible — exportable as PDF/A-3 (with audit trail) and structured CSV / JSON. |
| URS-DI-03 | H | R1 | Records shall be Contemporaneous — vendor-platform NTP-synced timestamps; time-of-action enforced (no future-dating, no back-dating). |
| URS-DI-04 | H | R1 | Original entries preserved; corrections via audit-trailed edits or via amendment entries that link to the original. |
| URS-DI-05 | H | R1 | Calculations shall be Accurate — verified per OQ for templates with calculation fields. |
| URS-DI-06 | M | R2 | Complete / Consistent / Enduring (≥ 25 y for GMP) / Available (≤ 4 h during inspection). |

### 5.12 Performance / Availability / Backup / Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | M | R2 | Entry open / save P95 ≤ 3 s under nominal lab load (~500 concurrent scientists site-wide). |
| URS-PERF-02 | M | R2 | Search response P95 ≤ 2 s for indexed fields; ≤ 5 s for full-text. |
| URS-AV-01 | H | R1 | Availability target shall align with Benchling's published SLA (≥ 99.7%). |
| URS-BAK-01 | H | R1 | Vendor-managed backup; site shall verify vendor-published RPO ≤ 4 h, RTO ≤ 24 h via vendor-assurance program. |
| URS-BAK-02 | M | R2 | Site shall maintain an annual configuration export (templates, Registry schema, Inventory config, security profiles) for traceability. |
| URS-SEC-01 | H | R1 | All access shall use Okta SSO + MFA; no local Benchling accounts. |
| URS-SEC-02 | H | R1 | Per-project access controls; cross-project visibility shall be restricted. |
| URS-SEC-03 | H | R1 | GDPR / HIPAA controls in vendor BAA / DPA; subject-identifier minimisation guidance shall be applied to clinical-phase entries. |
| URS-SEC-04 | M | R2 | Bulk export of GMP entries shall be restricted to Admins with documented purpose; bulk-export events shall trigger audit-trail review. |

### 5.13 Training and Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Production access shall require recorded role-specific training (LMS) plus template-specific competency for GMP templates. |
| URS-TRN-02 | M | R2 | An annual refresher shall be completed for all witness / approver roles. |
| URS-TRN-03 | M | R2 | GMP Mode Steward + Schema Approver roles shall complete an advanced data-integrity module. |
| URS-PR-01 | H | R1 | An annual periodic review per Annex 11 § 11 shall cover configuration drift, template + schema inventory, audit-trail review evidence, vendor-assurance status, integration health, training currency, mode-tag accuracy spot-check, signed by Head of R&D Informatics + VP QA. |

### 5.14 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is SAML 2.0 via Entra ID with SCIM lifecycle provisioning; conditional-access policy `R&D-App Conditional Access (MFA + device-compliance)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the Benchling tenant mirror; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 25 y (GLP / IP record) per the consuming-record schedule. |

### 5.15 Cross-System Integration — Helios audit-trail handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HEL-01 | H | R1 | Benchling ELN shall publish audit-trail events (Experiment lifecycle, witness signature, and template-change events) to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract (JSON Lines, schema-registry pinned, Kafka topic `helios.ingest.cyrene.benchling.v1`) within 5 minutes of event capture; 21 CFR § 11.10(e) audit-trail completeness shall be preserved end-to-end so that no event class is lost at the boundary. |
| URS-XINT-HEL-02 | H | R1 | Pre-handover audit-trail retention on the Benchling ELN side shall be ≥ 25 y regardless of Helios availability; once Helios acknowledges ingest (per-message ack with idempotency key), Helios is the system-of-record for review and the Benchling ELN local copy serves as the durability backstop until the local retention floor expires. |

## 6. Acceptance Criteria

System shall enter validated GxP use when CS, RA, IQ (vendor-shared), OQ (template / signature / audit / integration / mode separation), PQ (representative end-to-end entries through full lifecycle including witness + approval + amendment + eQMS deviation push + study-mode change) are approved and executed; vendor-assurance evidence shall be accepted; VSR shall be approved by Head of R&D Informatics + VP QA; the RTM shall map every URS to ≥ 1 approved test case.

## 7. Constraints

- Vendor cadenced releases are not under site change control.
- Bulk witness mode is denied.
- GMP and R&D streams must not share templates.

## 8. Assumptions

- Okta, Vault, LIMS, MasterControl, GitHub are independently validated.
- Benchling SLA holds.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- FDA *Computerized Systems Used in Clinical Investigations* (2007 + updates)
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11

### International — ICH
- ICH Q9(R1), ICH Q10

### Industry
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE GAMP Good Practice Guide: *A Risk-Based Approach to Compliant ELN*
- ISPE GAMP Good Practice Guide: *Records and Data Integrity*
- PIC/S PI 041; ISO/IEC 27001:2022

### Vendor
- Benchling — *Benchling for Biotech R&D 2025 Validation Approach* (vendor white paper)
- Benchling — *Release Notes 2025.1 / 2025.2 / 2025.3*

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

