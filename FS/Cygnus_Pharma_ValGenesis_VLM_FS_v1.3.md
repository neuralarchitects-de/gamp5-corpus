---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (T3 catch-up to URS v1.2: per-module protocol authoring, handheld + offline execution, deviation lifecycle, CSV training+cert, GitLab release-linked, multi-site federation; FDA CSA citation corrected to Feb 2026 final)"
seed_corpus_basis:
  - "CYG-URS-VLM-001 v1.2 (parent URS, T3)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 SaaS conventions"
  - "21 CFR Part 11; EU GMP Annex 11; ICH Q9(R1); ICH Q10"
  - "FDA Computer Software Assurance (final, February 2026; supersedes the September 2025 guidance)"
  - "BfArM (DE) Anlage 7"
parent_urs:
  document_number: CYG-URS-VLM-001
  version: 1.2
  file: ../../URS/_generated/final/Validation_Lifecycle_Management_ValGenesis__Cygnus_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Validation Lifecycle Management (VLM) — ValGenesis VLM 5.x

**Document Number:** CYG-FS-VLM-001
**Version:** 1.2
**Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** CYG-URS-VLM-001 v1.2
**Site:** Cygnus Pharma AG, Konstanz, Germany *(fictional)*
**System Class:** GAMP Cat 4 — Configured Product (multi-tenant SaaS)
**FDA CSA classification:** Critical — risk-based testing applies (FDA *Computer Software Assurance for Production and Quality Management System Software*, final, February 2026; supersedes the September 2025 guidance).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Chapter 4; ICH Q9(R1); ICH Q10; FDA CSA (Feb 2026); ISPE GAMP 5 + GPG Risk-Based Approach; PIC/S PI 041; BfArM (DE) Anlage 7; Swissmedic (CH); AGES (AT).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Validation Operations) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (FDA CSA Liaison) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |
| Approver (VP IT Compliance) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.1: FDA CSA risk-based-testing classification engine; ICH Q9(R1) risk-justification capture; evidence-hash verification; Konstanz (DE) deployment context; BfArM Anlage 7 binding. |
| 1.2 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.2 T3-floor uplift: per-module protocol authoring (FS/CS/DS/IQ/OQ/PQ); handheld + offline execution + e-sig + conflict resolution; deviation lifecycle per execution; CSV training + certification; GitLab release-linked validation; multi-site federation; FDA CSA citation corrected from Sep 2025 to Feb 2026 final. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies ValGenesis VLM 5.x configuration to satisfy `CYG-URS-VLM-001` v1.2, including v1.2 additions for per-module protocol authoring, handheld + offline execution capture, per-execution deviation lifecycle, CSV training + certification, GitLab release-linked validation, multi-site federation, and FDA CSA (Feb 2026) risk-based-testing classification.

## 2. Scope

ValGenesis VLM 5.x tenancy; per-tenancy + per-project configuration with risk-classification matrices; per-module protocol authoring (FS/CS/DS/IQ/OQ/PQ); SSO via Okta + MFA; integrations with Vault QualityDocs, MasterControl eQMS, Application Portfolio, validated GitLab; in-room execution via handhelds with offline sync; multi-site federation across 5 sites.

## 3. System Architecture

```
                Okta SSO + MFA
                    │
                    ▼
   ┌─────────────────────────────────────────────────────┐
   │     ValGenesis VLM 5.x (Cygnus tenancy)              │
   │   ┌─────────────────────────────────────────────┐    │
   │   │ Documents: URS / FS / CS / DS / RTM /        │    │
   │   │  IQ / OQ / PQ / VSR / VMP                    │    │
   │   │ Per-module Protocol Authoring                │    │
   │   │ Risk-classification engine (CSA + ICH Q9R1)  │    │
   │   │ Execution capture (web + handheld + offline) │    │
   │   │ Evidence-hash verifier                       │    │
   │   │ Deviation lifecycle (per execution)          │    │
   │   │ CSV Certification registry                   │    │
   │   │ Federation Service (5 sites)                  │    │
   │   └─────────────────────────────────────────────┘    │
   └─┬───────────┬──────────────┬──────────────────┬──────┘
     │           │              │                  │
     ▼           ▼              ▼                  ▼
   Vault    MasterControl   App Portfolio     GitLab
   QualityDocs (deviations) (system inventory) (release-linked)
```

## 4. Functional Specifications

### 4.1 Vendor Assurance and Configuration Lifecycle (URS § 5.1)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VND-01 | URS-VND-01 | ValGenesis vendor-assurance: SOC 2 Type II + ISO 27001 + customer-shared CSV summary on file; annual re-qualification tracked in `CYG-VND-REG`. |
| FS-VND-02 | URS-VND-02 | Vendor release-notes impact-assessed within 14 days via runbook `CYG-RB-VG-RELEASE`. |
| FS-VND-03 | URS-VND-03 | Vendor escalation runbook `CYG-RB-VG-ESCALATE`. |
| FS-CFG-01 | URS-CFG-01 | Per-tenancy + per-project config: DEV → QC → UAT → PRODUCTION; SoD enforced via `Config-Author` ≠ `Config-Approver`. |
| FS-CFG-02 | URS-CFG-02 | Configuration export `cyg-config-export.sh` for inspection (FDA / EMA / BfArM / Swissmedic). |

### 4.2 Document Lifecycle (URS § 5.2)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DOC-01 | URS-DOC-01 | Documents (URS, FS, CS, DS, RTM, IQ, OQ, PQ, VSR, VMP) follow DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE; e-signed; SoD. |
| FS-DOC-02 | URS-DOC-02 | Template version control; Author ≠ Approver. |
| FS-DOC-03 | URS-DOC-03 | First-class typed links; broken-reference detection at sign-off. |
| FS-DOC-04 | URS-DOC-04 | PDF/A-3 export for regulator-friendly format. |

### 4.3 Per-Module Protocol Authoring (URS § 5.3)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUTH-01 | URS-AUTH-01 | FS author module enforces typed-link to URS lines via `cyg_fs_urs_link`; orphan URS surfaced at sign-off via `wf_doc_signoff` precondition. |
| FS-AUTH-02 | URS-AUTH-02 | CS module captures per-CI configurable values + verification method (OQ test ID). |
| FS-AUTH-03 | URS-AUTH-03 | DS module captures Cat-5 custom-development design decisions (architecture, algorithm, error handling). |
| FS-AUTH-04 | URS-AUTH-04 | IQ module inherits vendor-shared IQ via `vendor_iq_inherit_ref`; site-installed components listed separately. |
| FS-AUTH-05 | URS-AUTH-05 | OQ module lists test cases per URS/FS/CS/DS line with expected results + acceptance criteria. |
| FS-AUTH-06 | URS-AUTH-06 | PQ module captures end-to-end scenarios with prod-representative datasets. |
| FS-AUTH-07 | URS-AUTH-07 | Template registry per module; promotion via `wf_template_promote` requires Template Author ≠ Template Approver e-sig. |

### 4.4 Risk-Based Testing per FDA CSA (Feb 2026) and GAMP 5 RBA (URS § 5.4)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RBT-01 | URS-RBT-01 | Risk-classification matrix per FDA CSA (Feb 2026): production / quality-system criticality × intended-use category → testing-depth tier (T1-Lean / T2-Standard / T3-Full). |
| FS-RBT-02 | URS-RBT-02 | Critical-thinking justification: free-text field ≥ 200 chars with ICH Q9(R1) categorisation; required at project start. |
| FS-RBT-03 | URS-RBT-03 | GAMP-category declaration per system (1/3/4/5); drives default protocol structure. |
| FS-RBT-04 | URS-RBT-04 | Reclassification trigger: change to system's intended-use field re-evaluates testing-depth tier; downstream re-testing flagged. |
| FS-RBT-05 | URS-RBT-05 | Portfolio testing-depth distribution dashboard `cyg_dashboard_csa_depth`. |

### 4.5 Protocol Execution — Handhelds, Offline, E-Signature (URS § 5.5)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-EXE-01 | URS-EXE-01 | Protocol execution: step-by-step actual results + evidence attachments + executor + witness signatures + timestamps via web UI or handheld app. |
| FS-EXE-02 | URS-EXE-02 | Test-step deviation routes to MasterControl via `IF-EQMS-DEV`; execution may continue per disposition flag. |
| FS-EXE-03 | URS-EXE-03 | Execution-record DB-level immutability after completion; corrections via `wf_amend_execution` + re-signature. |
| FS-EXE-04 | URS-EXE-04 | Evidence-attachment hash (SHA-256) computed on upload + verified on archive; tamper alert via `cyg_evidence_hash_check`. |
| FS-EXE-05 | URS-EXE-05 | NTP-synced timestamps across executors via `chronyd`. |
| FS-EXE-06 | URS-EXE-06 | Handheld app `ValGenesis Mobile 5.x` supports in-room evidence capture (camera, barcode scanner, sensor). |
| FS-EXE-07 | URS-EXE-07 | Offline mode: execution data stored locally; sync via `wf_sync_execution` on reconnection; conflicts (same step edited online + offline) surface in `cyg_sync_conflicts` for Project Lead resolution. |
| FS-EXE-08 | URS-EXE-08 | Handheld e-signature: requires fresh Okta token (max-age 5 min); biometric (FaceID/TouchID) accepted as second factor bound to Okta identity. |

### 4.6 Deviation Lifecycle per Execution (URS § 5.6)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DEV-01 | URS-DEV-01 | Deviation record schema: test-step ref, observed, expected, immediate-action, disposition, root-cause-linkage. |
| FS-DEV-02 | URS-DEV-02 | Idempotent push to MasterControl via `IF-EQMS-DEV` with idempotency key `vlm:exec:<id>:step:<n>`; failed push blocks finalisation. |
| FS-DEV-03 | URS-DEV-03 | Severity enum (Minor / Major / Critical) drives routing distribution list `cyg_dev_routing`. |
| FS-DEV-04 | URS-DEV-04 | VSR template includes auto-generated deviation summary table. |

### 4.7 RTM Maintenance (URS § 5.7)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RTM-01 | URS-RTM-01 | RTM auto-generated from typed links; orphan-URS flagging via `cyg_rtm_orphan_check`. |
| FS-RTM-02 | URS-RTM-02 | Completeness gate at VSR sign-off; orphan items justified or addressed in VSR. |
| FS-RTM-03 | URS-RTM-03 | FDA CSA risk-justified exemption logic: requirements marked `test-not-required` with documented risk justification; gate accepts. |
| FS-RTM-04 | URS-RTM-04 | RTM versioned snapshots at VSR-draft + VSR-final via `cyg_rtm_snapshot`. |

### 4.8 CSV Training and Certification (URS § 5.8)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-CERT-01 | URS-TRN-CERT-01 | CSV curriculum library `cyg_csv_curriculum` with role-specific modules. |
| FS-TRN-CERT-02 | URS-TRN-CERT-02 | Certification gate in `cyg_role_assignment`: project-role assignment denied if certification expired. |
| FS-TRN-CERT-03 | URS-TRN-CERT-03 | Annual refresher cron `cyg_csv_refresher_2026`. |
| FS-TRN-CERT-04 | URS-TRN-CERT-04 | Certification export `cyg_cert_export` for inspector request. |

### 4.9 Multi-Site Federation (URS § 5.9)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-FED-01 | URS-FED-01 | Federation across 5 sites (Konstanz authoritative for templates; site-local for project execution); rules in `cyg_fed_rules.yaml`. |
| FS-FED-02 | URS-FED-02 | Project transfer workflow `wf_fed_project_transfer` requires Multi-Site Federation Steward e-sig. |
| FS-FED-03 | URS-FED-03 | Lag metric `vlm_fed_lag_seconds`; alerts at 600 s. |

### 4.10 Audit Trail and Records Management (URS § 5.10)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit-trail covers document lifecycle, executions, deviations, configuration, signatures. |
| FS-AUD-02 | URS-AUD-02 | Append-only DB level; tenant-admin cannot UPDATE / DELETE. |
| FS-AUD-03 | URS-AUD-03 | Monthly Validation Operations review + quarterly QA review per Annex 11 § 9. |
| FS-AUD-04 | URS-AUD-04 | Retention life-of-system + ≥ 25 y; deletion blocked before retention threshold. |
| FS-AUD-05 | URS-AUD-05 | Focused review tool `CYG-AUD-FOCUSED` filters to signatures, deviations, config changes, RTM exemptions. |

### 4.11 21 CFR Part 11 Compliance (URS § 5.11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural controls in `CYG-SOP-CSV-01`; reviewed annually. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(d): access via Okta SAML 2.0 + MFA; service accounts via mTLS only. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(e): operational audit trail capturing user, action, date, time — implemented via FS-AUD-01. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.50: electronic signatures include signer's printed name, date / time, meaning; schema enforced in DB. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.70: signatures cryptographically linked via HMAC-SHA256 over record-hash + signer-id + timestamp; tampered records flagged on read. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.200: re-authentication required at the moment of signing (fresh OAuth2 token, max-age 5 min); cached credentials rejected. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.300: password / credential controls per site InfoSec policy. |

### 4.12 Data Integrity (URS § 5.12)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | **Attributable:** every action carries `actor_id`; DB not-null at audit-write. |
| FS-DI-02 | URS-DI-02 | **Legible:** PDF/A-3 + machine-readable JSON/XML; rendering verified via OQ. |
| FS-DI-03 | URS-DI-03 | **Contemporaneous:** event timestamps server-side + NTP-synced; retroactive entries flagged with delay reason. |
| FS-DI-04 | URS-DI-04 | **Original:** raw inputs / records preserved in immutable storage; derivatives reference but do not overwrite. |
| FS-DI-05 | URS-DI-05 | **Accurate:** calculations deterministic and validated under OQ; floating-point reproducibility verified. |
| FS-DI-06 | URS-DI-06 | **Complete / Consistent / Enduring / Available:** metadata completeness validated; chronological order DB-enforced; retention per regulation; retrievable within 1 business day. |

### 4.13 Integrations (URS § 5.13)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-VAULT-01 | URS-INT-VAULT-01 | Vault QualityDocs URN resolution; bidirectional linkage. |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | Deviation push to MasterControl with audit propagation. |
| FS-INT-PORT-01 | URS-INT-PORT-01 | Application-portfolio sync (inventory + criticality + owner). |
| FS-INT-GIT-01 | URS-INT-GIT-01 | Release-linked validation: GitLab tag / commit URN; broken-link check via `cyg_gitlab_link_check`. |
| FS-INT-SSO-01 | URS-INT-SSO-01 | Okta SAML 2.0 + MFA. |

### 4.14 Performance and Availability (URS § 5.14)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | Document open + edit P95 ≤ 3 s; monitored via vendor performance dashboard. |
| FS-PERF-02 | URS-PERF-02 | ≥ 500 concurrent executors during peak campaigns; verified by PQ load test. |
| FS-PERF-03 | URS-PERF-03 | Offline-handheld sync ≤ 60 s for representative 50-step execution. |
| FS-AV-01 | URS-AV-01 | Availability ≥ 99.5% per vendor SLA; 7-day-advance maintenance window. |

### 4.15 Backup, Restore, Security (URS § 5.15)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BAK-01 | URS-BAK-01 | Vendor-managed backup with daily integrity verification; RPO ≤ 4 h / RTO ≤ 24 h vendor-verified annually. |
| FS-BAK-02 | URS-BAK-02 | Site tenant-data export life-of-system + ≥ 25 y cold-storage. |
| FS-SEC-01 | URS-SEC-01 | TLS 1.3 + AES-256. |
| FS-SEC-02 | URS-SEC-02 | RBAC review quarterly. |
| FS-SEC-03 | URS-SEC-03 | Annual pen-test; findings remediated under change control. |

### 4.16 Training and Periodic Review (URS § 5.16)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | LMS training enforced; Risk Classifier role requires advanced FDA CSA + ICH Q9(R1) training. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher `VLM-2026-ANNUAL`: GAMP 5 / FDA CSA updates. |
| FS-PR-01 | URS-PR-01 | Annual Periodic Review per Annex 11 § 11; signed by Director Validation Operations + VP QA + VP IT Compliance. |


### 4.17 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: SAML 2.0 via Entra ID with SCIM lifecycle provisioning. Conditional-access binding to policy `Quality-App Conditional Access (MFA + device-compliance for validation e-signature)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the ValGenesis SQL backend; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.18 Cross-System Integration — Helios handover (M-XINT-HEL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HEL-01 | URS-XINT-HEL-01 | Audit-event publisher emits Kafka topic `helios.ingest.cygnus.valgenesis.v1` with schema-registry-pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`; at-least-once delivery; idempotency key `{source_system, event_id}`; back-pressure surfaced via Prometheus `helios_publish_lag_seconds` with 5-min alert at > 600 s. |
| FS-XINT-HEL-02 | URS-XINT-HEL-02 | Local audit-store retention policy enforces ≥ 25 y; Helios ack persisted as `helios_ack_ts` per event; periodic reconciliation job verifies parity (Helios row count == local published count) and raises a deviation in MasterControl on > 0.01% mismatch over a 24 h window. |


### 4.19 Cross-System Integration — eQMS handover (M-XINT-EQMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-EQMS-01 | URS-XINT-EQMS-01 | CAPA-event publisher posts to eQMS endpoint `POST /capa/tickets` with mTLS + Entra workload-identity; payload schema `eqms.ticket.v1`; OpenAPI artefact `xint-eqms.openapi.yaml`; outbound retry with exponential back-off and DLQ at 5 attempts. |
| FS-XINT-EQMS-02 | URS-XINT-EQMS-02 | eQMS ticket-status webhook subscribed; payload `eqms.status.v1`; consumer rule maps eQMS status `(OPEN, IN-PROGRESS, EFFECTIVENESS, CLOSED)` onto originating-record disposition fields; closed-loop verification gate prevents disposition without `eqms_status=CLOSED`. |

## 5. Configuration Items (CI)

| CI | Item | Value |
|---|---|---|
| CI-01 | Document types | URS, FS, CS, DS, RTM, IQ, OQ, PQ, VSR, VMP |
| CI-02 | Execution-record immutability | enforced at DB level |
| CI-03 | RTM completeness gate | at VSR sign-off; risk-justified exemptions allowed |
| CI-04 | Evidence hash | SHA-256 on upload + archive |
| CI-05 | CSA risk-classification matrix | per FDA CSA (Feb 2026) final |
| CI-06 | Audit retention | life-of-system + ≥ 25 y |
| CI-07 | Handheld offline-mode timeout | 24 h max before forced sync |
| CI-08 | Federation lag alert | 600 s |
| CI-09 | Sites in federation | 5 (Konstanz, Basel, Vienna, Boston, Singapore) |
| CI-10 | Certification expiry default | 12 months |

## 6. Risks (FS-level)

URS § 9 documents R-01..R-16. Additional FS risks:

- RTM auto-generation false-positive ("all items traced" when some aren't) → mitigation: OQ test on synthetic orphan injection.
- Evidence-hash collision (theoretical) → mitigation: SHA-256 sufficient at corpus scale; SHA-3 fallback available.
- Vendor SaaS schema migration breaks template inventory → mitigation: contract test in CI.
- Handheld lost / stolen with cached execution → mitigation: device-level encryption + 24h forced-sync window.
- Federation lag during global validation campaign → mitigation: lag alert + degraded-mode runbook.

## 7. References

- CYG-URS-VLM-001 v1.2
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Chapter 4
- ICH Q9(R1); ICH Q10
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance)
- ISPE GAMP 5 (2nd ed., 2022) + GPGs (RBA, Records & Data Integrity)
- ISPE *Validation Master Plan Guide*
- PIC/S PI 041
- BfArM (DE) Anlage 7; Swissmedic (CH); AGES (AT)
- ValGenesis — *VLM 5.x Validation Approach + Customer-Shared CSV Summary*

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-VND-01 | FS-VND-01 |
| URS-VND-02 | FS-VND-02 |
| URS-VND-03 | FS-VND-03 |
| URS-CFG-01 | FS-CFG-01 |
| URS-CFG-02 | FS-CFG-02 |
| URS-DOC-01 | FS-DOC-01 |
| URS-DOC-02 | FS-DOC-02 |
| URS-DOC-03 | FS-DOC-03 |
| URS-DOC-04 | FS-DOC-04 |
| URS-AUTH-01 | FS-AUTH-01 |
| URS-AUTH-02 | FS-AUTH-02 |
| URS-AUTH-03 | FS-AUTH-03 |
| URS-AUTH-04 | FS-AUTH-04 |
| URS-AUTH-05 | FS-AUTH-05 |
| URS-AUTH-06 | FS-AUTH-06 |
| URS-AUTH-07 | FS-AUTH-07 |
| URS-RBT-01 | FS-RBT-01 |
| URS-RBT-02 | FS-RBT-02 |
| URS-RBT-03 | FS-RBT-03 |
| URS-RBT-04 | FS-RBT-04 |
| URS-RBT-05 | FS-RBT-05 |
| URS-EXE-01 | FS-EXE-01 |
| URS-EXE-02 | FS-EXE-02 |
| URS-EXE-03 | FS-EXE-03 |
| URS-EXE-04 | FS-EXE-04 |
| URS-EXE-05 | FS-EXE-05 |
| URS-EXE-06 | FS-EXE-06 |
| URS-EXE-07 | FS-EXE-07 |
| URS-EXE-08 | FS-EXE-08 |
| URS-DEV-01 | FS-DEV-01 |
| URS-DEV-02 | FS-DEV-02 |
| URS-DEV-03 | FS-DEV-03 |
| URS-DEV-04 | FS-DEV-04 |
| URS-RTM-01 | FS-RTM-01 |
| URS-RTM-02 | FS-RTM-02 |
| URS-RTM-03 | FS-RTM-03 |
| URS-RTM-04 | FS-RTM-04 |
| URS-TRN-CERT-01 | FS-TRN-CERT-01 |
| URS-TRN-CERT-02 | FS-TRN-CERT-02 |
| URS-TRN-CERT-03 | FS-TRN-CERT-03 |
| URS-TRN-CERT-04 | FS-TRN-CERT-04 |
| URS-FED-01 | FS-FED-01 |
| URS-FED-02 | FS-FED-02 |
| URS-FED-03 | FS-FED-03 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
| URS-AUD-05 | FS-AUD-05 |
| URS-PART11-01 | FS-PART11-01 |
| URS-PART11-02 | FS-PART11-02 |
| URS-PART11-03 | FS-PART11-03 |
| URS-PART11-04 | FS-PART11-04 |
| URS-PART11-05 | FS-PART11-05 |
| URS-PART11-06 | FS-PART11-06 |
| URS-PART11-07 | FS-PART11-07 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-INT-VAULT-01 | FS-INT-VAULT-01 |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 |
| URS-INT-PORT-01 | FS-INT-PORT-01 |
| URS-INT-GIT-01 | FS-INT-GIT-01 |
| URS-INT-SSO-01 | FS-INT-SSO-01 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-PERF-03 | FS-PERF-03 |
| URS-AV-01 | FS-AV-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-HEL-01 | FS-XINT-HEL-01 |
| URS-XINT-HEL-02 | FS-XINT-HEL-02 |
| URS-XINT-EQMS-01 | FS-XINT-EQMS-01 |
| URS-XINT-EQMS-02 | FS-XINT-EQMS-02 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Orphan URS at VSR sign-off (untested requirement) | Medium | High | URS-RTM-02 (completeness gate) |
| R-02 | Execution-record tampering | Low | Critical | URS-EXE-03 (immutability), URS-AUD-02 |
| R-03 | Deviation bypass — execution continues without disposition | Medium | High | URS-EXE-02, URS-DEV-02 |
| R-04 | Audit-trail tampering | Low | Critical | URS-AUD-02 |
| R-05 | FDA CSA risk misclassification (system tested too lightly) | Medium | Critical | URS-RBT-01, URS-RBT-02, URS-RBT-04 |
| R-06 | Vendor outage during validation campaign | Low | High | URS-AV-01, URS-BAK-02 |
| R-07 | Risk Classifier conflict of interest with Project Lead | Low | High | SoD rule: Risk Classifier ≠ Project Lead |
| R-08 | Evidence-attachment hash mismatch on archive retrieval | Low | High | URS-EXE-04 |
| R-09 | Template drift across projects (inconsistent validation depth) | Medium | Medium | URS-DOC-02 |
| R-10 | RTM auto-generation defect produces false-complete RTM | Low | High | URS-RTM-01 (broken-link flagging) + OQ |
| R-11 | Vendor SaaS schema change breaks integrations | Low | Medium | URS-VND-02 |
| R-12 | EU GMP Annex 11 § 11 periodic-review evidence gap | Medium | Medium | URS-PR-01 |
| R-13 | Offline-handheld sync conflict losing execution data | Low | Critical | URS-EXE-07 conflict resolution |
| R-14 | Federation drift causing template version skew across sites | Medium | High | URS-FED-01..03 |
| R-15 | GitLab release link breaks (renamed branch / deleted tag) | Low | Medium | URS-INT-GIT-01 |
| R-16 | Certification expired but role still active | Low | High | URS-TRN-CERT-02 |

Full evaluation in `CYG-RA-VLM-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
