---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (FS catch-up to v1.2 URS, T4 uplift)"
seed_corpus_basis:
  - "BLR-URS-VSUB-001 v1.2"
  - "GAMP 5 Cat 4 SaaS"
  - "21 CFR Part 11; ICH M2/M4/M8"
  - "FDA eCTD + ESG; EMA eCTD v4 + CESP"
  - "PMDA Gateway; Health Canada CESG; MHRA; ANVISA; NMPA; Swissmedic"
  - "IDMP ISO 11238/11239/11240/11615/11616 + EMA SPOR"
parent_urs:
  document_number: BLR-URS-VSUB-001
  version: 1.2
  file: ../../URS/_generated/final/Veeva_Vault_Submissions__Bellerophon_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Regulatory Submissions Platform — Veeva Vault Submissions + Submissions Publishing 24R3 + Submissions Archive

**Document Number:** BLR-FS-VSUB-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** BLR-URS-VSUB-001 v1.2 | **Site:** Bellerophon Pharma plc (fictional) — London HQ + Basel + München + Wien + Tokyo + São Paulo + Shanghai hubs
**System Class:** GAMP Cat 4 — Configured Product (multi-tenant SaaS)
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; ICH M2/M4/M8; FDA eCTD + ESG; EMA eCTD v4 + CESP; PMDA Gateway; Health Canada CESG; MHRA UK; Swissmedic; ANVISA (BR); NMPA (CN); IDMP ISO 11238/11239/11240/11615/11616.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Regulatory Operations) | _____________ | _____________ | _____ |
| Reviewer (Publishing Manager) | _____________ | _____________ | _____ |
| Reviewer (IDMP / xEVMPD Steward) | _____________ | _____________ | _____ |
| Reviewer (Translation Manager) | _____________ | _____________ | _____ |
| Approver (VP Global Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.2 (T4 uplift): per-ID expansion for all 15 URS sub-sections; LORENZ eValidator + docuBridge integration; per-agency Module 1 templates; multi-country variation; IDMP / xEVMPD / SPOR; translation lifecycle; Brexit MHRA + ANVISA + NMPA + Swissmedic + DACH; 21 CFR Part 11 sub-section-explicit; no range compression per METHODOLOGY § 2A.7. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies Vault Submissions + Submissions Publishing + Submissions Archive configuration + integration to satisfy `BLR-URS-VSUB-001` v1.2.

## 2. Scope

Vault Submissions + Submissions Publishing 24R3 + Submissions Archive tenancy; per-product configuration; SSO via Okta SAML 2.0 + MFA; integrations with Vault QualityDocs, Vault RIM, Vault eTMF, Vault PromoMats, Sirius PV (Argus), EMA SPOR, LORENZ eValidator + docuBridge, translation-vendor service, FDA ESG / EMA CESP / PMDA / Health Canada CESG / MHRA / Swissmedic / ANVISA / NMPA gateways.

## 3. System Architecture

```
                Okta SAML 2.0 + MFA
                       │
                       ▼
   ┌────────────────────────────────────────────────────┐
   │  Veeva Vault Submissions + Publishing + Archive    │
   │  24R3 (Bellerophon tenancy)                         │
   │  • Submission Planning + Doc Selection              │
   │  • eCTD Build per ICH M8 + region-specific M1       │
   │  • LORENZ eValidator + docuBridge                   │
   │  • Granularity + Style + Cross-ref                  │
   │  • IDMP/xEVMPD product master                       │
   │  • Multi-country variation + Translation            │
   │  • Sequence Diff + Archive                          │
   └─┬──────────┬──────────┬───────────┬────────────────┘
     │          │          │           │
     ▼          ▼          ▼           ▼
   Vault       Vault     Sirius PV   EMA SPOR
   QualityDocs RIM       (Argus)     (IDMP)
     │          │          │           │
     ▼          ▼          ▼           ▼
   ┌────────────────────────────────────────────────────┐
   │  Gateway Routing Layer                             │
   │  FDA ESG • EMA CESP • PMDA • HC CESG • MHRA •      │
   │  Swissmedic • ANVISA • NMPA                        │
   └────────────────────────────────────────────────────┘
```

## 4. Functional Specifications

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VND-01 | URS-VND-01 | Veeva vendor-assurance pack (SOC 2 Type II, ISO 27001, ISO 27017, customer-shared CSV, DPA, BAA) tracked in `VA-VEEVA-2026`. |
| FS-VND-02 | URS-VND-02 | Release-impact-assessment workflow (24R1..25R1 release cadence) with 14-day SLA. |
| FS-VND-03 | URS-VND-03 | Annual Veeva TR-Audit summary filed in vendor-assurance dossier. |
| FS-CFG-01 | URS-CFG-01 | Per-product config lifecycle DRAFT → QC → UAT → PROD; SoD-enforced sign-off. |
| FS-CFG-02 | URS-CFG-02 | Configuration export endpoint emits version-stamped JSON snapshot per product. |
| FS-CFG-03 | URS-CFG-03 | Pre-PROD promotion runbook mandates regression-pack execution (`REG-VSUB-2026`). |
| FS-PLAN-01 | URS-PLAN-01 | Planning module supports IND / NDA / BLA / ANDA / MAA / CTA / variation / renewal / withdrawal artefact types. |
| FS-PLAN-02 | URS-PLAN-02 | Multi-country planning master spawns per-region sequence-build jobs with shared core content + region-specific Module 1. |
| FS-PLAN-03 | URS-PLAN-03 | Milestone-tracker with at-risk alerts (target submission date, agency interaction, expected response). |
| FS-PLAN-04 | URS-PLAN-04 | Resource-estimation calculator per submission type per region. |
| FS-DOC-01 | URS-DOC-01 | Document-selection from Vault QualityDocs via URN; selection locks document version-of-record at lock-time. |
| FS-DOC-02 | URS-DOC-02 | Document-reuse cross-reference tracker; reused-document version-of-record displayed. |
| FS-DOC-03 | URS-DOC-03 | CTD-section-validity check at selection (rule pack `ctd-section-validity-2026.yaml`). |
| FS-DOC-04 | URS-DOC-04 | Reuse-impact analysis flags downstream sequences when a reused document changes. |
| FS-ECTD-01 | URS-ECTD-01 | Sequence-build engine generates ICH M8 v3.2.2 (or v4.0 for EU) per agency profile. |
| FS-ECTD-02 | URS-ECTD-02 | Module 1 region templates: `m1-us-fda.xsl`, `m1-eu.xsl`, `m1-jp.xsl`, `m1-ca.xsl`, `m1-uk-mhra.xsl`, `m1-ch.xsl`, `m1-br.xsl`, `m1-cn.xsl`. |
| FS-ECTD-03 | URS-ECTD-03 | CTD core (Modules 2-5) shared content; region-specific xlink:href cross-references in M1 leaf elements. |
| FS-ECTD-04 | URS-ECTD-04 | Structural-validity DTD / XSD check at compile time; failure blocks compile. |
| FS-ECTD-05 | URS-ECTD-05 | Lifecycle operations (new, append, replace, delete) at leaf-document level per ICH M8; audit-trailed. |
| FS-ECTD-06 | URS-ECTD-06 | Index.xml generation deterministic given identical content set; verified by `OQ-INDEX-DETERMINISM-01`. |
| FS-VAL-01 | URS-VAL-01 | LORENZ eValidator API call pre-submission with agency-specific criteria pack version pinned per submission. |
| FS-VAL-02 | URS-VAL-02 | Error / Warning / Info classification; Errors block submission; Warnings require publisher justification capture. |
| FS-VAL-03 | URS-VAL-03 | LORENZ docuBridge preview + diff service exposed via Veeva integration; UI surfaces preview. |
| FS-VAL-04 | URS-VAL-04 | Validation-criteria-pack version stamped on each validation run; updates tracked under CR. |
| FS-VAL-05 | URS-VAL-05 | Validation reports archived per sequence in Submissions Archive. |
| FS-SEQ-01 | URS-SEQ-01 | Sequence-number generator: zero-padded 4-digit per application; gap-free; agency-specific. |
| FS-SEQ-02 | URS-SEQ-02 | xlink:href cross-references validated at compile (dangling-link check). |
| FS-SEQ-03 | URS-SEQ-03 | Sequence-release signature requires Submissions Approver re-authentication (OAuth2 max-age 5 min). |
| FS-SEQ-04 | URS-SEQ-04 | Leaf-document-lifecycle audit captures previous-leaf-reference, operation type, timestamp. |
| FS-SEQ-05 | URS-SEQ-05 | Sequence-number-conflict detector (parallel submission attempts); resolution workflow. |
| FS-GRAN-01 | URS-GRAN-01 | Granularity configurable per CTD module via `granularity-policy.yaml`; FDA + EMA recommended defaults. |
| FS-GRAN-02 | URS-GRAN-02 | Granularity-enforcement at compile; exceptions tracked in `granularity-exceptions` log. |
| FS-GRAN-03 | URS-GRAN-03 | Granularity-change impact analysis surfaces affected open sequences. |
| FS-STYLE-01 | URS-STYLE-01 | PDF/A-1b (FDA) / PDF/A-2 (EMA) rendering verified at compile; bookmarks + hyperlinks preserved. |
| FS-STYLE-02 | URS-STYLE-02 | Per-region stylesheet packs loaded per submission (`fda-stylesheet.xsl`, `ema-stylesheet.xsl`, `pmda-stylesheet.xsl`). |
| FS-STYLE-03 | URS-STYLE-03 | File-naming-convention validator (`agency-naming-2026.yaml`) enforced at compile. |
| FS-STYLE-04 | URS-STYLE-04 | Format-precheck (broken hyperlinks, oversized fonts, missing bookmarks) runs pre-validation. |
| FS-DIFF-01 | URS-DIFF-01 | Sequence-diff via docuBridge: leaf-level change-tracking with change-classification. |
| FS-DIFF-02 | URS-DIFF-02 | Submissions Archive holds all submitted sequences + regulator acks; immutable storage with object-lock. |
| FS-DIFF-03 | URS-DIFF-03 | Archive retrieval endpoint P95 ≤ 4 h; documented retrieval runbook `SOP-ARCHIVE-RETRIEVE`. |
| FS-DIFF-04 | URS-DIFF-04 | Archive sequence-index export in eCTD-viewer format (XML index + per-sequence ZIP). |
| FS-GW-01 | URS-GW-01 | FDA ESG submission via AS2 with SHA-256 receipt verification; ack reconciliation per sequence. |
| FS-GW-02 | URS-GW-02 | EMA CESP submission via SFTP-based protocol; EMA Common Repository ingestion confirmed via ack. |
| FS-GW-03 | URS-GW-03 | PMDA Gateway submission via JP-specific protocol; ack reconciliation. |
| FS-GW-04 | URS-GW-04 | Health Canada CESG via AS2 / WebTrader; ack reconciliation. |
| FS-GW-05 | URS-GW-05 | MHRA Submissions via the UK regulator's submission interface; UK M1 wrapped. |
| FS-GW-06 | URS-GW-06 | Swissmedic eGov platform integration; CH M1 wrapped. |
| FS-GW-07 | URS-GW-07 | ANVISA eCTD submission interface; BR M1 wrapped. |
| FS-GW-08 | URS-GW-08 | NMPA eCTD per China-specific requirements; CN M1 wrapped. |
| FS-GW-09 | URS-GW-09 | Negative-ack workflow opens structured Exception with agency-error-code mapping; resubmission within grace period. |
| FS-GW-10 | URS-GW-10 | Quarterly gateway-connectivity-test cron `gateway-connect-quarterly.py`. |
| FS-GW-11 | URS-GW-11 | Per-agency maintenance-window calendar `gateway-windows-2026.yaml`; scheduler avoids windows. |
| FS-IDMP-01 | URS-IDMP-01 | Product-master holds ISO 11238/11239/11240/11615/11616 identifiers; reconciled vs EMA SPOR daily. |
| FS-IDMP-02 | URS-IDMP-02 | IDMP metadata auto-population in EU M1 + xEVMPD via template binding. |
| FS-IDMP-03 | URS-IDMP-03 | xEVMPD submission worker for XEVPRM transactions; EMA ack reconciliation. |
| FS-IDMP-04 | URS-IDMP-04 | Quarterly IDMP-drift-detection job; impact-assessment opened on detected drift. |
| FS-REGION-MHRA-01 | URS-REGION-MHRA-01 | UK MHRA M1 template + UK-specific cover letter + UK-specific cover sheet. |
| FS-REGION-MHRA-02 | URS-REGION-MHRA-02 | NI Protocol handling (parallel EU + UK submission with shared core, divergent M1). |
| FS-REGION-SWISS-01 | URS-REGION-SWISS-01 | CH M1 + DACH-language label artefacts (de-CH, fr-CH, it-CH). |
| FS-REGION-ANVISA-01 | URS-REGION-ANVISA-01 | BR M1 + pt-BR translation routing. |
| FS-REGION-NMPA-01 | URS-REGION-NMPA-01 | CN M1 + zh-CN translation + CN-specific stability + manufacturing requirements pre-check. |
| FS-REGION-DACH-01 | URS-REGION-DACH-01 | EU-DACH variants: de-DE for EU MAA marketed in DE; de-AT for AT national; de-CH for CH. |
| FS-REGION-LANG-01 | URS-REGION-LANG-01 | Region-language matrix `region-lang-2026.yaml` per product. |
| FS-TRANS-01 | URS-TRANS-01 | Translation-package builder per submission per region; source-link via translation-job-id. |
| FS-TRANS-02 | URS-TRANS-02 | Translation lifecycle DRAFT → TRANSLATION → REVIEW → APPROVED → SUBMITTED; vendor hand-off + return via translation-vendor REST API. |
| FS-TRANS-03 | URS-TRANS-03 | Source-to-target alignment via segment-id; source updates flag translation drift. |
| FS-TRANS-04 | URS-TRANS-04 | Translation memory + glossary maintained per product family. |
| FS-TRANS-05 | URS-TRANS-05 | Local-medical-reviewer sign-off workflow for region-specific labelling. |
| FS-VAR-01 | URS-VAR-01 | Variation-master schema: one canonical change deployed across N regions with per-region timing. |
| FS-VAR-02 | URS-VAR-02 | Variation-classification rule pack: EU Type IA/IB/II/III; FDA supplements; JP / CA categories. |
| FS-VAR-03 | URS-VAR-03 | Variation-dashboard Grafana panel per-agency status. |
| FS-VAR-04 | URS-VAR-04 | Conditional-variation tracker with downstream-submission dependencies graph. |
| FS-AUD-01 | URS-AUD-01 | Audit-trail schema covers all document / signature / sequence-build / validation / submission / ack / archive events. |
| FS-AUD-02 | URS-AUD-02 | Vendor-controlled DB-level append-only; vendor TR-Audit confirms. |
| FS-AUD-03 | URS-AUD-03 | Monthly Submissions Manager review + quarterly QA review; signed reports filed. |
| FS-AUD-04 | URS-AUD-04 | Retention per jurisdictional minimum (US ≥ 2y post-approval, EU ≥ 10y, JP ≥ 15y) enforced at archive tier. |
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): SOPs reviewed annually. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(b): copy generation verified. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(c): retention-period protection via vendor-confirmed immutable storage. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.10(d): Okta SAML 2.0 + MFA. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.10(e): audit trail per FS-AUD-01. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.10(g): authority checks at workflow / API layer. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.10(k): operation-manual change-control. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.50: printed name + date/time + meaning rendered. |
| FS-PART11-09 | URS-PART11-09 | Per § 11.70: HMAC-SHA-256 cryptographic binding. |
| FS-PART11-10 | URS-PART11-10 | Per § 11.100: uniqueness via Okta-DB constraint. |
| FS-PART11-11 | URS-PART11-11 | Per § 11.200: re-authentication at content / sequence-release / gateway-submission signatures. |
| FS-PART11-12 | URS-PART11-12 | Per § 11.300: password / credential controls per InfoSec. |
| FS-INT-VAULT-01 | URS-INT-VAULT-01 | Vault QualityDocs URN resolver via Vault Cross-Vault Bridge. |
| FS-INT-VAULT-02 | URS-INT-VAULT-02 | Vault RIM product / authorisation master integration. |
| FS-INT-VAULT-03 | URS-INT-VAULT-03 | Vault eTMF cross-reference where TMF informs submission. |
| FS-INT-VAULT-04 | URS-INT-VAULT-04 | Vault PromoMats integration where applicable. |
| FS-INT-VIG-01 | URS-INT-VIG-01 | Sirius PV (Argus) integration for PSUR / PBRER / PADER / DSUR content via internal API. |
| FS-INT-SPOR-01 | URS-INT-SPOR-01 | EMA SPOR REST API for IDMP reference data. |
| FS-INT-EVAL-01 | URS-INT-EVAL-01 | LORENZ eValidator REST API integration. |
| FS-INT-DOCB-01 | URS-INT-DOCB-01 | LORENZ docuBridge integration via REST + thin-client browser embed. |
| FS-INT-TRANS-01 | URS-INT-TRANS-01 | Translation-vendor REST API for job dispatch + return. |
| FS-INT-SSO-01 | URS-INT-SSO-01 | Okta SAML 2.0 + MFA. |
| FS-DI-01 | URS-DI-01 | **Attributable:** actor_id captured on every record. |
| FS-DI-02 | URS-DI-02 | **Legible:** PDF/A-1b / PDF/A-2 rendering verified per agency. |
| FS-DI-03 | URS-DI-03 | **Contemporaneous:** NTP-synced server timestamps; retroactive entries flagged. |
| FS-DI-04 | URS-DI-04 | **Original:** source preserved; corrections as new versions. |
| FS-DI-05 | URS-DI-05 | **Accurate:** sequence-build calculations deterministic; OQ-verified. |
| FS-DI-06 | URS-DI-06 | **Complete / Consistent / Enduring / Available:** retention + chronology. |
| FS-PERF-01 | URS-PERF-01 | Sequence-compile P95 ≤ 30 min for 5,000-document sequence; verified by PQ. |
| FS-PERF-02 | URS-PERF-02 | eValidator P95 ≤ 15 min per sequence. |
| FS-PERF-03 | URS-PERF-03 | Archive retrieval P95 ≤ 4h. |
| FS-AV-01 | URS-AV-01 | Vendor SLA ≥ 99.7%; uptime probes 24×7. |
| FS-AV-02 | URS-AV-02 | RPO / RTO per Veeva SLA verified annually. |
| FS-BAK-01 | URS-BAK-01 | Vendor-managed backup; site verifies RPO / RTO annually. |
| FS-BAK-02 | URS-BAK-02 | Quarterly tenant-data export retained ≥ 10y in site cold storage. |
| FS-SEC-01 | URS-SEC-01 | Per-product / per-agency / per-region RBAC matrix. |
| FS-SEC-02 | URS-SEC-02 | TLS 1.3 in transit; AES-256 at rest. |
| FS-SEC-03 | URS-SEC-03 | Annual pen-test; high/critical remediation within 60 days. |
| FS-TRN-01 | URS-TRN-01 | LMS-recorded role-specific training; agency-specific publisher competency. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher `RA-ANNUAL-2026`: FDA / EMA / PMDA / HC / MHRA / ANVISA / NMPA updates. |
| FS-PR-01 | URS-PR-01 | Annual periodic-review run-book auto-collects: vendor qualification, config drift, validation-pack version, gateway connectivity, archive retrieval rehearsal, IDMP / SPOR reconciliation, translation-vendor performance, deviation summary, training currency. |
| FS-INSP-01 | URS-INSP-01 | Inspection-readiness export endpoint aggregates per-submission dossier (sequence content + validation report + ack messages + signature evidence + audit-trail extract); retrieval P95 ≤ 4 h. |
| FS-INSP-02 | URS-INSP-02 | HA-correspondence register (FDA-IR, EMA D-120/D-180, PMDA queries) with per-question sub-tracking and SLA monitoring. |
| FS-INSP-03 | URS-INSP-03 | CA-query response workflow: drafter → reviewer → Submissions Approver SoD-enforced; response export PDF/A-3. |
| FS-INSP-04 | URS-INSP-04 | Mock-audit rehearsal workflow with structured findings + remediation tracker. |
| FS-MEET-01 | URS-MEET-01 | Meeting tracker: pre-IND, Type-B, Type-C, Pre-NDA, EMA scientific-advice, PMDA-consultation; request → briefing-doc → minutes → feedback. |
| FS-MEET-02 | URS-MEET-02 | Briefing-document submission uses relevant agency template; eCTD-compiled where required. |
| FS-MEET-03 | URS-MEET-03 | Meeting-feedback feed forwards to submission planning. |
| FS-LIFE-01 | URS-LIFE-01 | Application-lifecycle tracker per (application_id, agency) covering initial / amendment / supplement / variation / renewal / withdrawal with sequence-by-sequence audit. |
| FS-LIFE-02 | URS-LIFE-02 | Application status (active / under-review / approved / withdrawn / lapsed) per agency surface in dashboard. |
| FS-LIFE-03 | URS-LIFE-03 | Approval letter + EPAR + label-of-record archived per application per agency in Vault. |
| FS-LIFE-04 | URS-LIFE-04 | Lifecycle milestone-alert engine (PDUFA, CHMP opinion, MAA renewal) with email + dashboard alerts. |
| FS-SPL-01 | URS-SPL-01 | FDA SPL generator per 21 CFR 314.81; SPL XML validated against HL7 SPL schema; output suitable for FDA SPL submission via ESG. |
| FS-SPL-02 | URS-SPL-02 | SPL versioning preserves effective-time + version-number sequencing per HL7 SPL. |
| FS-SPL-03 | URS-SPL-03 | SPL drug-listing + establishment-registration submissions to FDA per 21 CFR Part 207 tracked. |
| FS-REF-01 | URS-REF-01 | Cross-application document-reuse tracker (e.g., DMF referenced by multiple NDA / ANDA) with reference-letter management. |
| FS-REF-02 | URS-REF-02 | Letter-of-Authorization (LoA) tracker with effective dates + revocation events. |
| FS-REF-03 | URS-REF-03 | DMF status (Type II / III / IV / V) + adequacy-status tracked per DMF. |
| FS-RWD-01 | URS-RWD-01 | RWE submission support via SDTM / ADaM / SEND data-package upload + eCTD inclusion per 21st Century Cures Act + EMA RWE strategy. |
| FS-RWD-02 | URS-RWD-02 | Patient-experience-data (PFDD) submission support via dedicated Module 5 sub-section. |
| FS-DASH-01 | URS-DASH-01 | Submissions dashboard (Grafana) surfaces per-product per-agency status; refresh latency ≤ 15 min. |
| FS-DASH-02 | URS-DASH-02 | Per-publisher KPI dashboard: sequences-published, validation-error-rate, on-time-submission rate. |
| FS-DASH-03 | URS-DASH-03 | Compile / validate / submit time-histograms per sequence-size class. |
| FS-COMBO-01 | URS-COMBO-01 | Combination-product routing engine: OCP-assigned FDA Center (CDER / CBER / CDRH) selected; dual-Center coordination workflow. |
| FS-COMBO-02 | URS-COMBO-02 | Combination-product M3 (CMC) + M5 (device-specific clinical) integration template + cross-reference. |
| FS-PROF-VAL-01 | URS-PROF-VAL-01 | Per-submission-type validation profile selector (IND / NDA / ANDA / BLA / MAA / CTA / variation / supplement) pins LORENZ criteria + agency rules. |
| FS-PROF-VAL-02 | URS-PROF-VAL-02 | Per-submission-type profile changes under CR; open-submission impact assessed. |
| FS-PDF-01 | URS-PDF-01 | PDF-bookmark generator + validator enforces agency-required bookmark structure. |
| FS-PDF-02 | URS-PDF-02 | Broken-internal-link check runs at compile; failures block sequence build. |
| FS-PDF-03 | URS-PDF-03 | Font-embedding check (all fonts subsetted + embedded); non-compliant PDFs rejected. |
| FS-PDF-04 | URS-PDF-04 | PDF security-setting validator: no password / no copy-restriction enforced. |
| FS-COVER-01 | URS-COVER-01 | Per-region cover-letter template store: FDA / EMA / PMDA / HC / MHRA / Swissmedic / ANVISA / NMPA templates. |
| FS-COVER-02 | URS-COVER-02 | Form generators: FDA 356h, FDA 1571, FDA 2253, EMA CESP submission form per region requirements. |
| FS-COVER-03 | URS-COVER-03 | Cover-letter version-control tracks template-version + per-submission instance. |


### 4.1 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: SAML 2.0 via Entra ID with SCIM lifecycle provisioning. Conditional-access binding to policy `Regulatory-App Conditional Access (FIDO2 phishing-resistant MFA)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the metadata DB plus object-replica for the submission binder; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.2 Cross-System Integration — Hydra + Helios (M-XINT-HYD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HYD-01 | URS-XINT-HYD-01 | Egress firewall ACL `reg-vault-egress-deny-llm` blocks vendor LLM endpoints except via the Hydra gateway VIP; Vault Submissions adapter `BLR-HYD-CLIENT-1.x` enforces use-case ID. |
| FS-XINT-HYD-02 | URS-XINT-HYD-02 | Hydra use-case `REG-DRAFT-MOD2-001`, `REG-DRAFT-MOD3-001`, `REG-DRAFT-RTI-001` each registered with `risk_class=annex_i` and Art. 11 pack artefact; gate returns 403 on missing or expired pack. |
| FS-XINT-HYD-03 | URS-XINT-HYD-03 | Vault binder ingestion hook validates per-section watermark + provenance JSON; binder finalisation API requires `approver_role=RegAffairsLead` + valid e-signature timestamp ≤ 1 h before finalisation. |
| FS-XINT-HYD-04 | URS-XINT-HYD-04 | Per-section content hash recomputed at finalisation and compared with the post-HITL hash stored at approval; mismatch raises MasterControl deviation `BLR-HYD-WATERMARK-MISMATCH`. |
| FS-XINT-HYD-05 | URS-XINT-HYD-05 | Helios ingestion via Kafka topic `helios.ingest.bellerophon.hydra.v1`; retention floor 2 y on the Vault tenant side. |


### 4.3 Cross-System Integration — Helios handover (M-XINT-HEL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HEL-01 | URS-XINT-HEL-01 | Audit-event publisher emits Kafka topic `helios.ingest.bellerophon.submissions.v1` with schema-registry-pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`; at-least-once delivery; idempotency key `{source_system, event_id}`; back-pressure surfaced via Prometheus `helios_publish_lag_seconds` with 5-min alert at > 600 s. |
| FS-XINT-HEL-02 | URS-XINT-HEL-02 | Local audit-store retention policy enforces for the product lifetime + 25 y; Helios ack persisted as `helios_ack_ts` per event; periodic reconciliation job verifies parity (Helios row count == local published count) and raises a deviation in MasterControl on > 0.01% mismatch over a 24 h window. |


### 4.4 Cross-System Integration — EDMS handover (M-XINT-EDMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-EDMS-01 | URS-XINT-EDMS-01 | EDMS read adapter `BLR-EDMS-READ-1.x` performs `GET /docs/{doc_id}?version=effective` and pins the binder entry to the returned `{doc_id, version, sha256}`; version drift detected at finalisation triggers a submission re-validation. |

## 5. Configuration Items (CI)

| CI | Item | Value |
|---|---|---|
| CI-01 | Per-agency validation profiles | enabled (FDA, EMA, PMDA, HC, MHRA, Swissmedic, ANVISA, NMPA) |
| CI-02 | Negative-ack exception workflow | enabled |
| CI-03 | Sequence-release SoD | enforced |
| CI-04 | Granularity policy | per CTD module |
| CI-05 | M1 region templates | per agency |
| CI-06 | LORENZ criteria pack | pinned per submission |
| CI-07 | IDMP / SPOR reconciliation | daily |
| CI-08 | Translation lifecycle | enabled |
| CI-09 | Variation master | enabled |
| CI-10 | Archive retention | per-jurisdiction minimum |
| CI-11 | Re-authentication on signing | OAuth2 max-age 5 min |
| CI-12 | Gateway endpoints | FDA ESG, EMA CESP, PMDA, HC CESG, MHRA, Swissmedic, ANVISA, NMPA |

## 6. Risks (FS-level)

Invalid eCTD compilation (FS-ECTD-04 + FS-VAL-01..05); gateway loss (FS-GW-01..11 + connectivity tests); submission of unapproved content (FS-SEQ-03 + SoD); sequence numbering gap (FS-SEQ-01, FS-SEQ-05); M1 region template wrong (FS-ECTD-02 + FS-REGION-*); IDMP referential drift (FS-IDMP-04); validation-criteria-pack drift (FS-VAL-04); translation-vendor slip (FS-TRANS-02 vendor SLA); cross-reference broken (FS-SEQ-02); style non-compliance (FS-STYLE-01..04); audit-trail tampering (FS-AUD-02 vendor controls); multi-country variation drift (FS-VAR-01..04).

## 7. References

- BLR-URS-VSUB-001 v1.2
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance)
- ICH M2 ESTRI; ICH M4 (CTD); ICH M8 (eCTD)
- FDA *eCTD Technical Conformance Guide*; FDA ESG specifications
- EMA eCTD EU IG; EMA CESP specifications; EMA SPOR
- PMDA Gateway specs; Health Canada CESG; MHRA UK Submissions; Swissmedic eGov; ANVISA eCTD; NMPA eCTD
- ISO 11238/11239/11240/11615/11616 — IDMP
- ISPE GAMP 5 (2nd ed., 2022); PIC/S PI 041; ISO/IEC 27001:2022
- Veeva — *Vault Submissions / Submissions Publishing 24R3 Reference*
- LORENZ — *eValidator + docuBridge product references*

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-VND-01 | FS-VND-01 |
| URS-VND-02 | FS-VND-02 |
| URS-VND-03 | FS-VND-03 |
| URS-CFG-01 | FS-CFG-01 |
| URS-CFG-02 | FS-CFG-02 |
| URS-CFG-03 | FS-CFG-03 |
| URS-PLAN-01 | FS-PLAN-01 |
| URS-PLAN-02 | FS-PLAN-02 |
| URS-PLAN-03 | FS-PLAN-03 |
| URS-PLAN-04 | FS-PLAN-04 |
| URS-DOC-01 | FS-DOC-01 |
| URS-DOC-02 | FS-DOC-02 |
| URS-DOC-03 | FS-DOC-03 |
| URS-DOC-04 | FS-DOC-04 |
| URS-ECTD-01 | FS-ECTD-01 |
| URS-ECTD-02 | FS-ECTD-02 |
| URS-ECTD-03 | FS-ECTD-03 |
| URS-ECTD-04 | FS-ECTD-04 |
| URS-ECTD-05 | FS-ECTD-05 |
| URS-ECTD-06 | FS-ECTD-06 |
| URS-VAL-01 | FS-VAL-01 |
| URS-VAL-02 | FS-VAL-02 |
| URS-VAL-03 | FS-VAL-03 |
| URS-VAL-04 | FS-VAL-04 |
| URS-VAL-05 | FS-VAL-05 |
| URS-SEQ-01 | FS-SEQ-01 |
| URS-SEQ-02 | FS-SEQ-02 |
| URS-SEQ-03 | FS-SEQ-03 |
| URS-SEQ-04 | FS-SEQ-04 |
| URS-SEQ-05 | FS-SEQ-05 |
| URS-GRAN-01 | FS-GRAN-01 |
| URS-GRAN-02 | FS-GRAN-02 |
| URS-GRAN-03 | FS-GRAN-03 |
| URS-STYLE-01 | FS-STYLE-01 |
| URS-STYLE-02 | FS-STYLE-02 |
| URS-STYLE-03 | FS-STYLE-03 |
| URS-STYLE-04 | FS-STYLE-04 |
| URS-DIFF-01 | FS-DIFF-01 |
| URS-DIFF-02 | FS-DIFF-02 |
| URS-DIFF-03 | FS-DIFF-03 |
| URS-DIFF-04 | FS-DIFF-04 |
| URS-GW-01 | FS-GW-01 |
| URS-GW-02 | FS-GW-02 |
| URS-GW-03 | FS-GW-03 |
| URS-GW-04 | FS-GW-04 |
| URS-GW-05 | FS-GW-05 |
| URS-GW-06 | FS-GW-06 |
| URS-GW-07 | FS-GW-07 |
| URS-GW-08 | FS-GW-08 |
| URS-GW-09 | FS-GW-09 |
| URS-GW-10 | FS-GW-10 |
| URS-GW-11 | FS-GW-11 |
| URS-IDMP-01 | FS-IDMP-01 |
| URS-IDMP-02 | FS-IDMP-02 |
| URS-IDMP-03 | FS-IDMP-03 |
| URS-IDMP-04 | FS-IDMP-04 |
| URS-REGION-MHRA-01 | FS-REGION-MHRA-01 |
| URS-REGION-MHRA-02 | FS-REGION-MHRA-02 |
| URS-REGION-SWISS-01 | FS-REGION-SWISS-01 |
| URS-REGION-ANVISA-01 | FS-REGION-ANVISA-01 |
| URS-REGION-NMPA-01 | FS-REGION-NMPA-01 |
| URS-REGION-DACH-01 | FS-REGION-DACH-01 |
| URS-REGION-LANG-01 | FS-REGION-LANG-01 |
| URS-TRANS-01 | FS-TRANS-01 |
| URS-TRANS-02 | FS-TRANS-02 |
| URS-TRANS-03 | FS-TRANS-03 |
| URS-TRANS-04 | FS-TRANS-04 |
| URS-TRANS-05 | FS-TRANS-05 |
| URS-VAR-01 | FS-VAR-01 |
| URS-VAR-02 | FS-VAR-02 |
| URS-VAR-03 | FS-VAR-03 |
| URS-VAR-04 | FS-VAR-04 |
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
| URS-INT-VAULT-01 | FS-INT-VAULT-01 |
| URS-INT-VAULT-02 | FS-INT-VAULT-02 |
| URS-INT-VAULT-03 | FS-INT-VAULT-03 |
| URS-INT-VAULT-04 | FS-INT-VAULT-04 |
| URS-INT-VIG-01 | FS-INT-VIG-01 |
| URS-INT-SPOR-01 | FS-INT-SPOR-01 |
| URS-INT-EVAL-01 | FS-INT-EVAL-01 |
| URS-INT-DOCB-01 | FS-INT-DOCB-01 |
| URS-INT-TRANS-01 | FS-INT-TRANS-01 |
| URS-INT-SSO-01 | FS-INT-SSO-01 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-PERF-03 | FS-PERF-03 |
| URS-AV-01 | FS-AV-01 |
| URS-AV-02 | FS-AV-02 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-INSP-01 | FS-INSP-01 |
| URS-INSP-02 | FS-INSP-02 |
| URS-INSP-03 | FS-INSP-03 |
| URS-INSP-04 | FS-INSP-04 |
| URS-MEET-01 | FS-MEET-01 |
| URS-MEET-02 | FS-MEET-02 |
| URS-MEET-03 | FS-MEET-03 |
| URS-LIFE-01 | FS-LIFE-01 |
| URS-LIFE-02 | FS-LIFE-02 |
| URS-LIFE-03 | FS-LIFE-03 |
| URS-LIFE-04 | FS-LIFE-04 |
| URS-SPL-01 | FS-SPL-01 |
| URS-SPL-02 | FS-SPL-02 |
| URS-SPL-03 | FS-SPL-03 |
| URS-REF-01 | FS-REF-01 |
| URS-REF-02 | FS-REF-02 |
| URS-REF-03 | FS-REF-03 |
| URS-RWD-01 | FS-RWD-01 |
| URS-RWD-02 | FS-RWD-02 |
| URS-DASH-01 | FS-DASH-01 |
| URS-DASH-02 | FS-DASH-02 |
| URS-DASH-03 | FS-DASH-03 |
| URS-COMBO-01 | FS-COMBO-01 |
| URS-COMBO-02 | FS-COMBO-02 |
| URS-PROF-VAL-01 | FS-PROF-VAL-01 |
| URS-PROF-VAL-02 | FS-PROF-VAL-02 |
| URS-PDF-01 | FS-PDF-01 |
| URS-PDF-02 | FS-PDF-02 |
| URS-PDF-03 | FS-PDF-03 |
| URS-PDF-04 | FS-PDF-04 |
| URS-COVER-01 | FS-COVER-01 |
| URS-COVER-02 | FS-COVER-02 |
| URS-COVER-03 | FS-COVER-03 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-HYD-01 | FS-XINT-HYD-01 |
| URS-XINT-HYD-02 | FS-XINT-HYD-02 |
| URS-XINT-HYD-03 | FS-XINT-HYD-03 |
| URS-XINT-HYD-04 | FS-XINT-HYD-04 |
| URS-XINT-HYD-05 | FS-XINT-HYD-05 |
| URS-XINT-HEL-01 | FS-XINT-HEL-01 |
| URS-XINT-HEL-02 | FS-XINT-HEL-02 |
| URS-XINT-EDMS-01 | FS-XINT-EDMS-01 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Invalid eCTD compilation accepted at submission window | Medium | High | URS-ECTD-04, URS-VAL-01..05 |
| R-02 | Gateway loss during submission window | Medium | High | URS-GW-01..11 |
| R-03 | Submission of unapproved content | Low | Critical | URS-SEQ-03 + SoD |
| R-04 | eCTD validation failure on sequence number (gap-in-numbering) | Medium | High | URS-SEQ-01, URS-SEQ-05 |
| R-05 | Module 1 region-specific package wrong for jurisdiction | Medium | High | URS-ECTD-02, URS-REGION-* |
| R-06 | IDMP referential drift breaking EU variation submission | Low | High | URS-IDMP-04 |
| R-07 | Validation-criteria-pack drift (LORENZ release) breaking compile | Medium | Medium | URS-VAL-04 |
| R-08 | Translation-vendor schedule slip blocking regional submission | Medium | Medium | URS-TRANS-02 |
| R-09 | Sequence-diff misinterpretation by reviewer | Low | High | URS-DIFF-01 + docuBridge |
| R-10 | Archive retrieval > 4h during inspection | Low | High | URS-DIFF-03 |
| R-11 | Cross-reference broken between leaves (xlink:href dangling) | Medium | High | URS-SEQ-02 |
| R-12 | Style / format non-compliance per agency stylesheet | Medium | Medium | URS-STYLE-01..04 |
| R-13 | Granularity mismatch with agency expectation | Low | Medium | URS-GRAN-01..03 |
| R-14 | Audit-trail tampering | Low | Critical | URS-AUD-02 |
| R-15 | Multi-country variation drift (per-region content divergence) | Medium | High | URS-VAR-01..04 |

Full evaluation in `BLR-RA-VSUB-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
