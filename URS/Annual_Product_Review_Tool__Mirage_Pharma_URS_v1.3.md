---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-27; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "GAMP 5 (2nd ed.) Cat 5 conventions for site-developed analytics"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "21 CFR Part 211 § 211.180(e)"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Chapter 1 § 1.10"
  - "ICH Q9(R1); ICH Q10 — Pharmaceutical Quality System"
  - "ISPE GAMP 5 (2nd Edition, 2022)"
  - "PIC/S PI 041; WHO TRS 970 Annex 6"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# User Requirements Specification (URS)

## Annual Product Review (APR / PQR) Tool — Site-Developed Python + Postgres + Quarto Reporting

**Document Number:** MIR-URS-APR-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Site:** Mirage Pharma Co., Global Quality Operations, Boston, MA, USA *(fictional)*
**System Owner:** Director, Quality Operations
**Process Owner:** VP Quality Assurance
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom Application (site-developed Python service producing FDA Annual Product Review and EU Product Quality Review)
**Project Mode:** Custom-build project — site-developed system (GAMP 5 Category 5 — Bespoke; internal SDLC). System: Site-Developed Python + Postgres + Quarto Reporting.
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 211 § 211.180(e); EU GMP Annex 11; EU GMP Chapter 1 § 1.10; ICH Q10; ICH Q9(R1); PIC/S PI 041; WHO TRS 970 Annex 6

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Quality Operations) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Statistician) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs — EU PQR variant) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | v1.2 enrichment: tiered to T2 (50-80 reqs target; this URS lands at 62 reqs); expanded § 5 with explicit modules for data aggregation, trend + capability analysis, OOS/OOT compilation, stability data review, validation status review, supplier quality review, recommendations + sign-off workflow, EU PQR vs FDA APR variant logic, multi-product + multi-site mode; § 9 risks raised to 8 domain-specific items; references modernised per METHODOLOGY § 2A.1. |

## Definitions

| Term | Definition |
|---|---|
| APR | Annual Product Review (FDA — 21 CFR § 211.180(e)) |
| PQR | Product Quality Review (EU GMP Chapter 1 § 1.10) |
| PQS | Pharmaceutical Quality System (ICH Q10) |
| Source systems | LIMS, MES, eQMS, Pharmacovigilance, Stability, Cold-Chain, Serialization, EM (environmental monitoring) |
| OOS | Out-of-Specification (per FDA OOS Guidance, 2006) |
| OOT | Out-of-Trend (statistical deviation from established trend before reaching OOS) |
| CAPA | Corrective and Preventive Action |
| Cpk / Ppk | Process Capability / Process Performance indices |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |

## 1. Purpose

This URS defines requirements for a site-developed APR / PQR tool that aggregates per-product data across upstream GxP systems and produces the annual review report required by FDA (21 CFR § 211.180(e)) and by EU (EU GMP Chapter 1 § 1.10, Product Quality Review) regulators. The tool is the system of record for the aggregation, the trend analysis, the OOS / OOT compilation, the recommendations register, and the multi-signatory sign-off workflow that closes the annual review cycle.

## 2. Scope

**In:** Python services on K8s; Postgres warehouse; Quarto-based report rendering; integrations with LabWare LIMS 8 (release + stability + EM data), Werum PAS-X (batch yields, deviations, in-process control results), MasterControl (deviations + CAPAs + change controls), Sirius PV (complaint summary), Halcyon Stability Management System (stability protocol + Q1E shelf-life status), Selene Cold-Chain (excursions, transport deviations), Atlas Serialization (recall / counterfeit / aggregation events), supplier-quality module of MasterControl (supplier scorecards), Validation Lifecycle Management (ValGenesis — system validation status by product); SSO via Okta SAML 2.0 + MFA; outputs archived in Veeva Vault QualityDocs.

**Out:** source-system data integrity (each separately validated); literature review; CMC regulatory submissions (CMC team uses APR/PQR output, not the inverse); annual stability protocol authoring (lives in Halcyon Stability URS).

## 3. System Description and Intended Use

The tool runs annually per product family (and on-demand for inspections). For each run it pulls per-product data from upstream systems via REST / read-only DB views, applies the validated PQR / APR template (process performance, OOS / OOT trend, deviation summary, CAPA effectiveness, complaints, stability summary, serialization recall events, change-control summary, validation status review, supplier quality review, regulatory commitments status, recommendations register), runs SPC trend tests (Western Electric + Nelson rules), computes capability indices (Cp / Cpk / Pp / Ppk), and renders the report in PDF + Excel + structured CSV. The report is reviewed by the product owner, QA, a statistician, and the EU QP where the EU PQR variant applies, and is approved with electronic signatures.

The tool supports an **FDA APR variant** (21 CFR § 211.180(e) — manufacturing, control, packaging, stability, complaints, recalls, returns, investigations) and an **EU PQR variant** (EU GMP Ch.1 § 1.10 — broader: critical IPCs, starting materials, packaging materials, rejected batches, deviations + CAPAs effectiveness, post-marketing commitments, qualification status of equipment and utilities, MA variations). Both variants share the same data backbone; the template engine selects sections per variant.

GAMP Cat 5: site SDLC applies. The PQR / APR template, SPC tests, capability calculations, and aggregation rules are the validated application logic.

## 4. User Roles

| Role | Permissions |
|---|---|
| Product Owner | Run APR / PQR for assigned products; review draft; respond to QA findings. |
| Statistician | Review SPC outputs + capability indices; co-approve. |
| QA Reviewer | Review the report; raise findings; cannot approve. |
| QA Approver (Head of QA) | Approve; cannot author. |
| Qualified Person (QP, EU PQR variant) | Final signoff on EU PQR; per Directive 2001/83/EC Art. 51. |
| Tool Administrator | Deploy + configure; cannot approve APR / PQR. |
| Auditor | Read-only across runs and audit trails. |
| Inspector (on-demand) | Read-only access to approved APR / PQR with audit-trail viewer. |

Separation of duties: Product Owner ≠ Approver; Tool Admin cannot approve APR / PQR; QA Reviewer ≠ QA Approver on the same run.

## 5. User Requirements

### 5.1 Application Lifecycle (Cat 5 SDLC)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DEV-01 | H | R1 | The system SDLC shall be documented and shall enforce code review, unit tests (≥ 85% line + branch coverage), integration tests, security scan (Snyk + SonarQube), and a regression suite covering at least one representative APR + one representative PQR end-to-end. |
| URS-DEV-02 | H | R1 | The system source code shall reside in validated GitLab (HYP-URS-GIT-001) with signed commits, protected-branch policy, and mandatory peer review. |
| URS-DEV-03 | H | R1 | Container images shall be cryptographically signed (Sigstore / cosign equivalent); deployment shall route through an approved Change Request; a rollback runbook shall exist and shall be exercised at least once per release. |
| URS-DEV-04 | H | R1 | All dependencies shall be pinned by hash; SBOM (CycloneDX) shall be produced per release and retained ≥ 25 years. |

### 5.2 Aggregation and Calculation Rules

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-RULE-01 | H | R1 | The APR / PQR template shall be version-controlled; template changes shall follow DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE with role-restricted signatures (Author ≠ Approver). |
| URS-RULE-02 | H | R1 | SPC tests (Western Electric Rules 1–4 + Nelson Rules 1–8) shall be validated against reference data; results shall be deterministic; verified per OQ. |
| URS-RULE-03 | H | R1 | Aggregation queries shall be idempotent and deterministic; the same (product, year, source-snapshot) input shall yield bit-identical aggregated output. |
| URS-RULE-04 | H | R1 | Per-source extractors shall include integrity checks (row counts vs source, checksum reconciliation); failures shall block the run. |
| URS-RULE-05 | H | R1 | Capability indices (Cp, Cpk, Pp, Ppk) shall be computed per ISO 22514-2 conventions; normality shall be tested (Anderson–Darling) before Cpk is reported; non-normal distributions shall route to non-parametric or transformed (Box–Cox) capability per template-configured rule. |
| URS-RULE-06 | H | R1 | The system shall flag any capability index computed on n < 30 batches as "indicative only — small-sample"; Cpk reported on n < 10 shall be suppressed and flagged. |

### 5.3 Data Aggregation Sources

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AGG-01 | H | R1 | The system shall extract batch yield, deviations, and in-process control results from PAS-X MES for every batch of the product family in the review period. |
| URS-AGG-02 | H | R1 | The system shall extract release-test results, OOS records, OOT flags, and stability sample results from LabWare LIMS per product / method / batch. |
| URS-AGG-03 | H | R1 | The system shall extract deviations, CAPAs, change controls, and supplier complaints from MasterControl eQMS with link-through to root cause classification. |
| URS-AGG-04 | H | R1 | The system shall extract complaint summaries from Sirius Pharmacovigilance with PV-classification + severity. |
| URS-AGG-05 | M | R2 | The system shall extract cold-chain excursions affecting the product from Selene Cold-Chain. |
| URS-AGG-06 | M | R2 | The system shall extract serialization-aggregation events, recall events, and counterfeit incidents from Atlas Serialization. |
| URS-AGG-07 | H | R1 | The system shall snapshot each source extraction with timestamp + source-row-count + SHA-256 manifest, and shall preserve the snapshot for ≥ 25 years to support APR / PQR reconstructability. |

### 5.4 Trend Analysis and Capability Indices

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TREND-01 | H | R1 | The system shall produce control charts (X̄-R for n ≥ 2, X̄-s for n ≥ 10, I-MR for n = 1, p-chart for binomial counts, c-chart for defect counts) per critical quality attribute (CQA) and per critical process parameter (CPP). |
| URS-TREND-02 | H | R1 | The system shall apply Western Electric Rules 1–4 and Nelson Rules 1–8 for out-of-control detection; rule firings shall be logged with batch ID, attribute, rule, and timestamp. |
| URS-TREND-03 | H | R1 | The system shall report Pp / Ppk over the review period and Cp / Cpk over the most recent stable phase; the boundary between phases shall be the most recent validated change-control closure date. |
| URS-TREND-04 | H | R1 | The system shall produce per-attribute trend commentary (free-text generated by the Product Owner) and shall block sign-off where rule firings exist without commentary. |
| URS-TREND-05 | M | R2 | The system shall provide an EWMA chart (λ = 0.2 default, configurable per attribute) as a supplementary view for slow drift detection. |

### 5.5 OOS / OOT Review Compilation

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-OOS-01 | H | R1 | The system shall enumerate every OOS investigation in the review period with: batch ID, method, result, investigation status, root cause classification, CAPA linkage. |
| URS-OOS-02 | H | R1 | The system shall enumerate every OOT observation with: detection mechanism, threshold breached, batch / batches affected, disposition. |
| URS-OOS-03 | H | R1 | OOS / OOT entries with open investigations at run-time shall be highlighted and shall require Statistician + QA Approver acknowledgement before sign-off proceeds. |
| URS-OOS-04 | M | R2 | The system shall compute the OOS rate (OOS investigations per batch) and trend it across the prior 3 review periods. |

### 5.6 Stability Data Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-STAB-01 | H | R1 | The system shall integrate with Halcyon Stability Management to enumerate active stability protocols for the product family, time-point completion status, and ICH Q1E shelf-life predictions. |
| URS-STAB-02 | H | R1 | The system shall flag stability OOS / OOT events occurring during the review period and shall link to the corresponding investigation in eQMS. |
| URS-STAB-03 | H | R1 | The system shall surface any proposed shelf-life change with the supporting Q1E regression, confidence interval, and statistician approval reference. |
| URS-STAB-04 | M | R2 | The system shall report photostability (ICH Q1B) and bracketing / matrixing (ICH Q1D) coverage status. |

### 5.7 Validation Status Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VS-01 | H | R1 | The system shall integrate with the Validation Lifecycle Management system (ValGenesis VLM) to enumerate equipment / utility / computerised-system validation status applicable to the product. |
| URS-VS-02 | H | R1 | The system shall flag any system in expired-periodic-review status, in revalidation-overdue status, or with open CSV deviations linked to the product, and shall require QA Approver acknowledgement. |
| URS-VS-03 | M | R2 | The system shall report the count of executed Performance Qualification (PQ) runs in the review period per critical system. |

### 5.8 Supplier Quality Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SUP-01 | H | R1 | The system shall extract supplier scorecards (lot-acceptance rate, on-time delivery, complaint rate, supplier-audit status) for every API / starting-material / critical-excipient supplier feeding the product family. |
| URS-SUP-02 | H | R1 | The system shall flag supplier scorecards with downgraded status, expired qualification, or open supplier-CAPA, and shall route them into the Recommendations register. |
| URS-SUP-03 | M | R2 | The system shall include supplier-audit findings (last audit date, status, open observations) per critical supplier. |

### 5.9 Recommendations + Sign-off Workflow

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REC-01 | H | R1 | The system shall maintain a Recommendations register per run with: finding category, owner, target date, status (OPEN / IN-PROGRESS / CLOSED / DEFERRED), CAPA linkage. |
| URS-REC-02 | H | R1 | The system shall carry forward prior-year recommendations whose status is not CLOSED, and shall report aging. |
| URS-REC-03 | H | R1 | Sign-off shall require: Product Owner (authorship), Statistician (SPC review), QA Reviewer (compliance review), QA Approver (final QA approval); EU PQR variant additionally requires QP signature. |
| URS-REC-04 | H | R1 | Sign-off shall be sequential (Author → Statistician → QA Reviewer → QA Approver → QP); skipping a step shall be impossible. |
| URS-REC-05 | H | R1 | Each signature shall use re-authentication (re-entry of credentials) per 21 CFR § 11.200 at the moment of signing. |

### 5.10 EU PQR vs FDA APR Variant Logic

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-VAR-01 | H | R1 | The template engine shall select FDA APR sections per 21 CFR § 211.180(e) (manufacturing batches, complaints, recalls, returns, OOS investigations, stability) or EU PQR sections per EU GMP Ch.1 § 1.10 (additionally: critical IPCs, starting / packaging materials, rejected batches, post-marketing commitments, equipment / utilities qualification status, MA variations) per the run-configuration flag. |
| URS-VAR-02 | H | R1 | When a product is registered in both FDA and EU jurisdictions, the system shall produce a combined APR + PQR report with both section sets and a cross-reference index. |
| URS-VAR-03 | M | R2 | The system shall support the WHO TRS 970 Annex 6 Product Quality Review variant for WHO-prequalified products, where applicable. |

### 5.11 Multi-Product and Multi-Site Mode

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-MULTI-01 | H | R1 | The system shall produce a single APR / PQR per product (one product = one run) and shall NOT silently combine products. |
| URS-MULTI-02 | H | R1 | Where a product is manufactured at ≥ 2 sites, the system shall produce per-site sections within the single product report and shall not pool data across sites without explicit configuration. |
| URS-MULTI-03 | M | R2 | The system shall provide a multi-product portfolio view (read-only) for QA management oversight, aggregating per-product compliance signals. |

### 5.12 Audit Trail / 21 CFR Part 11 / ALCOA+ / Data Integrity

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | The system shall maintain a time-stamped, append-only audit trail (21 CFR § 11.10(e); EU GMP Annex 11 § 9) for every state change: source extraction, template selection, SPC computation, recommendation entry, signature event. |
| URS-AUD-02 | H | R1 | The audit trail shall be protected from administrator update / delete (append-only at platform level). |
| URS-AUD-03 | H | R1 | Audit trail shall be reviewed monthly by QA Compliance; review evidence shall be filed in QA dossier. |
| URS-AUD-04 | H | R1 | Audit-trail retention ≥ 25 years from product expiry. |
| URS-PART11-10 | H | R1 | Procedures and controls protecting electronic-record validity per 21 CFR § 11.10(a)–(c) shall be documented; copies shall be generable for inspection per § 11.10(b). |
| URS-PART11-50 | H | R1 | Electronic-signature manifestations shall include the printed name, date / time of signing, and the meaning of the signature per 21 CFR § 11.50. |
| URS-PART11-70 | H | R1 | Signatures shall be cryptographically bound to the signed APR / PQR record per 21 CFR § 11.70. |
| URS-PART11-100 | H | R1 | Each electronic signature shall be unique to a single individual; no reuse / reassignment per 21 CFR § 11.100. |
| URS-PART11-200 | H | R1 | Re-authentication (credentials re-entered) shall be required at every signing event per 21 CFR § 11.200(a)(1). |
| URS-DI-01 | H | R1 | All records shall be Attributable to a named user (ALCOA+). |
| URS-DI-02 | H | R1 | All records shall be Legible (rendered PDF + structured CSV). |
| URS-DI-03 | H | R1 | All records shall be Contemporaneous (system clock NTP-synced; skew ≤ 1 s). |
| URS-DI-04 | H | R1 | Originals (source snapshots) shall be preserved alongside the report so the report is reconstructable per PIC/S PI 041. |
| URS-DI-05 | H | R1 | All numeric outputs shall be Accurate per OQ-validated equations. |

### 5.13 Integrations / Performance / Security / Training / Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-LIMS-01 | H | R1 | Read-only LIMS view (release, stability, EM) — authenticated REST + DB read-replica. |
| URS-INT-MES-01 | H | R1 | PAS-X read-only batch / deviation / IPC views. |
| URS-INT-EQMS-01 | H | R1 | MasterControl read-only deviation / CAPA / CR / supplier views. |
| URS-INT-PV-01 | H | R1 | Sirius PV read-only complaint summary. |
| URS-INT-STAB-01 | H | R1 | Halcyon Stability read-only summary. |
| URS-INT-VLM-01 | H | R1 | ValGenesis VLM read-only validation-status summary. |
| URS-INT-COLDCHAIN-01 | M | R2 | Selene Cold-Chain summary (excursions). |
| URS-INT-SER-01 | M | R2 | Atlas Serialization recall / event summary. |
| URS-INT-VAULT-01 | H | R1 | Approved-report push to Vault QualityDocs. |
| URS-PERF-01 | M | R2 | Single-product APR / PQR generation ≤ 60 minutes wall-time at the 95th percentile across the product portfolio. |
| URS-AV-01 | M | R2 | The tool is run annually per product; availability target 99.0% during the run window. |
| URS-BAK-01 | H | R1 | Postgres warehouse + run snapshots backed up nightly; retention ≥ 25 y; quarterly restore-test witnessed by QA. |
| URS-SEC-01 | H | R1 | SSO via Okta + MFA; service-account secrets in HashiCorp Vault; quarterly access review. |
| URS-TRN-01 | H | R1 | LMS-recorded training; statistician competency for SPC + capability review. |
| URS-PR-01 | H | R1 | Annual periodic review (of the tool, not the products) covering source-system schema drift, template inventory, SPC-rule configuration, audit-trail review evidence, OOS / OOT trend, capability-index distribution, sign-off cycle time; signed by Director Quality Operations + VP QA. |

### 5.14 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem; conditional-access policy `Quality-App Conditional Access (MFA on first logon per session)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T3 with RPO ≤ 72 h and RTO ≤ 72 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the APR data-mart; the application team shall participate in annual application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 15 y (Quality record) per the consuming-record schedule. |

### 5.15 Cross-System Integration — eQMS CAPA handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-EQMS-01 | H | R1 | On detection of APR trend finding (21 CFR § 211.180(e)) (trigger: Annual Product Review trend exceedance, OOT pattern, recurrent deviation pattern), the system shall push a CAPA-ticket creation event to the Talos MasterControl eQMS (`TLB-URS-EQMS-001`) via the eQMS event-push channel with required metadata {originating_system, originating_record_id, finding_class, severity, evidence_package_uri, detection_ts_utc, detection_user, regulatory_basis}; severity per APR procedure; recurrent OOT → major. |
| URS-XINT-EQMS-02 | H | R1 | The eQMS ticket-creation call shall be idempotent on `{originating_system, originating_record_id, finding_class}`; the eQMS status-callback shall be ingested and reflected on the originating record with a hyperlink to the eQMS ticket; closed-loop verification per ICH Q9(R1) + ICH Q10 shall be evidenced before the originating record is dispositioned. |

## 6. Acceptance Criteria

URS, FS, RA (configuration + risk assessment), IQ, OQ, PQ approved and executed (Cat 5 full set); PQ includes representative end-to-end APR runs against ≥ 3 product families and ≥ 1 EU PQR variant run, with all integrations exercised, SPC + capability verification on reference data, multi-site mode tested, and Vault archival demonstrated; VSR approved; RTM maps every URS-ID to ≥ 1 approved test case.

## 7. Constraints

- Source-system schema changes communicated via the change-management process; aggregator extractors shall fail-closed on schema drift.
- Site SDLC enforced; no production deployment without VSR.
- Capability indices below n = 30 are reported indicative-only per ISO 22514-2 small-sample caveats.

## 8. Assumptions

- Source systems (LIMS, MES, eQMS, PV, Stability, Cold-Chain, Serialization, VLM) are validated; their data is ALCOA+ at source.
- Vault is validated.
- PKI / SSO / Vault credential management are validated infrastructure.
- The Quality Unit's APR / PQR procedure (`MIR-SOP-APR-001`) governs review timelines and triggers.

## 9. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .22, .68, .180, .192 (CGMP; § 211.180(e) Annual Product Review)
- FDA Guidance for Industry: *Investigating Out-of-Specification (OOS) Test Results for Pharmaceutical Production* (2006)
- FDA Guidance for Industry: *Process Validation: General Principles and Practices* (2011) — Stage 3 CPV alignment
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes September 2025 guidance)
- FDA *Data Integrity and Compliance with cGMP* (2018)

### EU
- EU GMP Annex 11 §§ 4 (validation), 6 (accuracy), 9 (audit trail), 11 (periodic evaluation) — Computerised Systems
- EU GMP Chapter 1 § 1.10 — Product Quality Review
- EU GMP Annex 15 — Qualification and Validation
- EU GMP Annex 16 — Certification by a Qualified Person
- Directive 2001/83/EC Art. 51 — QP batch-release obligations

### International — ICH
- ICH Q9(R1) — Quality Risk Management
- ICH Q10 — Pharmaceutical Quality System (especially § 3.2 PQR / APR Management Review)
- ICH Q12 — Technical and Regulatory Considerations for Pharmaceutical Product Lifecycle Management

### Industry guidance — ISPE / PIC/S / WHO / ISO
- ISPE GAMP 5 (2nd Edition, 2022) — Cat 5 conventions
- ISPE GAMP Good Practice Guide: *A Risk-Based Approach to Compliant GxP Computerized Systems*
- PIC/S PI 041 — Good Practices for Data Management and Integrity
- WHO Technical Report Series 970 Annex 6 — Product Quality Review
- ISO 22514-2:2017 — Statistical methods in process management — Capability and performance — Part 2

### Vendor / internal
- LabWare LIMS 8; Werum PAS-X v3.2; MasterControl eQMS; Sirius PV; Halcyon Stability; Selene Cold-Chain; Atlas Serialization; ValGenesis VLM; Veeva Vault QualityDocs 24R1.
- Internal: `MIR-SOP-APR-001` Annual Product Review procedure.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

