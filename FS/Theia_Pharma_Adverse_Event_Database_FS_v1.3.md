---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (FS catch-up to v1.2 URS, T3 uplift)"
seed_corpus_basis:
  - "TEA-URS-MDR-001 v1.2"
  - "GAMP 5 Cat 4 SaaS"
  - "21 CFR Part 803 + 21 CFR Part 11"
  - "EU MDR Arts. 87, 88, 89, 92; EU IVDR Arts. 82, 83"
  - "IMDRF AET WG/N43"
  - "ISO 14971:2019; ISO 13485:2016"
parent_urs:
  document_number: TEA-URS-MDR-001
  version: 1.2
  file: ../../URS/_generated/final/Adverse_Event_Database__Theia_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Medical-Device Adverse Event Database — Sparta TrackWise Digital Quality (Vigilance Module)

**Document Number:** TEA-FS-MDR-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** TEA-URS-MDR-001 v1.2 | **Site:** Theia Pharma & Devices Ltd., Galway, Ireland *(fictional)* with hubs in München (DE) + Wien (AT)
**System Class:** GAMP Cat 4 — Configured Product (multi-tenant SaaS)
**Regulatory Scope:** 21 CFR Part 803 §§ .1–.58; 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU MDR Reg. 2017/745 Arts. 87, 88, 89, 92; EU IVDR 2017/746 Arts. 82, 83; IMDRF AET WG/N43; MDCG 2023-3; ISO 14971:2019; ISO 13485:2016.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Device Vigilance) | _____________ | _____________ | _____ |
| Reviewer (PRRC — EU MDR Art. 15) | _____________ | _____________ | _____ |
| Reviewer (Risk Management Lead — ISO 14971) | _____________ | _____________ | _____ |
| Approver (VP Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.2 (T3 uplift): per-ID expansion for all 13 URS sub-sections; MDR/eMDR decision-tree, IMDRF AET coding, FSCA tracking, Art. 88 trend, MAUDE prep, RMF link, DACH gateways, combination-product cross-ref to Argus; no range compression per METHODOLOGY § 2A.7. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## Definitions

Inherited from TEA-URS-MDR-001 v1.2. Additional FS-specific terms:

| Term | Definition |
|---|---|
| FS | Functional Specification (this document) |
| TWD-Q | TrackWise Digital Quality (Vigilance Module) |
| ESG | FDA Electronic Submissions Gateway |
| IRIS | BfArM device-vigilance reporting interface |
| ElViS | Swissmedic vigilance system |
| CIPARS | Health Canada device-incident-report system |

## 1. Purpose

This FS specifies how Sparta TrackWise Digital Quality (Vigilance Module) is configured and integrated to satisfy `TEA-URS-MDR-001` v1.2. Controlling input to `TEA-CS-MDR-001`, `TEA-RA-MDR-001`, IQ / OQ / PQ Protocols, and `TEA-RTM-MDR-001`.

## 2. Scope

TrackWise Digital Quality Vigilance Module multi-tenant SaaS; per-device configuration; SSO via Okta SAML 2.0 + MFA; integrations with FDA ESG (eMDR), EUDAMED vigilance module, BfArM IRIS, Swissmedic ElViS, AGES, Health Canada CIPARS, Sirius PV (Argus), MasterControl eQMS, Atlas Serialization (UDI-DI master), literature-surveillance feed.

## 3. System Architecture

```
                Okta SAML 2.0 + MFA
                        │
                        ▼
   ┌────────────────────────────────────────────────────┐
   │   TrackWise Digital Vigilance (Theia tenancy)       │
   │  Intake → Triage → Investigation → Reportability     │
   │  → Approval → Submission → Closed                    │
   │  + IMDRF AET coding + RMF link + FSCA + Art. 88     │
   └─┬───────────┬──────────────┬───────────┬───────────┘
     │           │              │           │
     ▼           ▼              ▼           ▼
   FDA ESG    EUDAMED         BfArM IRIS  Swissmedic / AGES /
   (eMDR)     vigilance       (DE)        Health Canada CIPARS
                              ▲
                              │
                          DACH hub
   ┌───────────┬──────────────┬───────────┐
   │           │              │           │
   ▼           ▼              ▼           ▼
   Sirius PV   MasterControl   Atlas      Literature
   (Argus)     (eQMS / CAPA)   (UDI-DI)   feed
```

## 4. Functional Specifications

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VND-01 | URS-VND-01 | Sparta vendor-assurance pack (SOC 2 Type II, ISO 27001, ISO 13485, customer-shared CSV, BAA, DPA) tracked in `VA-SPARTA-2026`; annual re-qualification. |
| FS-VND-02 | URS-VND-02 | Release-impact-assessment workflow; 14-day SLA on impact decision; configuration-affecting changes raise re-validation CR. |
| FS-VND-03 | URS-VND-03 | Annual Sparta TR-Audit summary filed in `VA-SPARTA-2026`. |
| FS-CFG-01 | URS-CFG-01 | Per-device config (UDI-DI, reportability ruleset, IMDRF AET pack version, gateway profiles) lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE; SoD-enforced sign-off (Author ≠ Approver). |
| FS-CFG-02 | URS-CFG-02 | Configuration export endpoint emits version-stamped JSON snapshot per device-config; archive retained ≥ 15 years. |
| FS-INTAKE-01 | URS-INTAKE-01 | Intake adapters: HCP portal `hcp.theia.com`, secure web form `/intake/patient`, distributor REST API, partner-exchange E2B(R3) feed; each event recorded with channel + source-id + intake-timestamp. |
| FS-INTAKE-02 | URS-INTAKE-02 | Email-gateway parser at `vigilance@theia.com` extracts structured fields; source email retained as audit-trail attachment. |
| FS-INTAKE-03 | URS-INTAKE-03 | Phone-ticket integration with site call-centre (Zendesk); operator-id + recording-reference + consented-transcription captured. |
| FS-INTAKE-04 | URS-INTAKE-04 | Bidirectional complaint-link to MasterControl eQMS via case-id ↔ complaint-id mapping; flow-back on case state transition. |
| FS-INTAKE-05 | URS-INTAKE-05 | Literature-surveillance hit ingestion creates case when reportability plausible; citation captured per ICH E2B §C.4 (cross-walk for combination products). |
| FS-INTAKE-06 | URS-INTAKE-06 | Distributor / importer chain-of-custody fields captured per EU MDR Arts. 14, 16. |
| FS-CASE-01 | URS-CASE-01 | Mandatory fields (case-id, intake-date, awareness-date, UDI-DI / device-id, reporter-type, country, description, suspected-event) validated server-side at intake. |
| FS-CASE-02 | URS-CASE-02 | Workflow state machine: {Intake → Triaged → Investigated → Reportability-Decided → Approved → Submitted → Closed}; reverse transitions require captured reason + e-signature + audit-trail. |
| FS-CASE-03 | URS-CASE-03 | Awareness-date capture UI requires explicit date entry + rationale ("first awareness via channel X on date Y"). |
| FS-CASE-04 | URS-CASE-04 | Follow-up handler: new info creates `case_version + 1`; delta calculation against follow-up-trigger matrix `FU-DELTA-2026.yaml`. |
| FS-CASE-05 | URS-CASE-05 | Reclassification handler re-computes reporting clocks + re-routes; reclassification event captured with `prev_class`, `new_class`, reason. |
| FS-CASE-06 | URS-CASE-06 | Case-priority matrix `priority-2026.yaml` (event-severity × device-class); high-priority cases routed to dedicated processor queue. |
| FS-CASE-07 | URS-CASE-07 | Duplicate-detection rule engine over (UDI-DI + complainant identifiers + event-date ± 7d + textual similarity ≥ 0.85); suspected duplicates routed to merge decision. |
| FS-MDR-01 | URS-MDR-01 | Reportability decision-tree per 21 CFR 803.20 categories (death-contribution, serious-injury-contribution, malfunction-likely-to-cause-S/D); decision-tree implemented as a rule engine with version-control. |
| FS-MDR-02 | URS-MDR-02 | EU MDR Art. 2(65) classification: serious incident vs non-serious incident vs use error; classification UI structured. |
| FS-MDR-03 | URS-MDR-03 | Reportability decision capture: rule-applied + reasoning narrative + decision-maker-id + timestamp; non-reportable decisions auditable; QA review queue. |
| FS-MDR-04 | URS-MDR-04 | Reportability ruleset version-controlled in `gitlab.theia/vig-rules`; rule changes re-validated via `OQ-REPORTABILITY-RULE-01`. |
| FS-MDR-05 | URS-MDR-05 | Decision pre-fill UI surfaces rule-engine suggestion; reviewer confirms or overrides (override audit-trailed). |
| FS-CODE-01 | URS-CODE-01 | IMDRF AET coding UI per Annexes A (event-type), B (device-problem), C (component/part), D (investigation), E (clinical-sign), F (investigation-result), G (event-conclusion); annex-codes drawn from IMDRF reference pack `imdrf-aet-2026.json`. |
| FS-CODE-02 | URS-CODE-02 | Coding capture: coder-id, IMDRF version, coding timestamp, manual-override reason if applicable. |
| FS-CODE-03 | URS-CODE-03 | Annual IMDRF release migration runbook; open-case re-coding policy `imdrf-recode-policy.md`. |
| FS-CODE-04 | URS-CODE-04 | Coding-QC sample job (≥ 2% monthly) generates discrepancy report. |
| FS-CODE-05 | URS-CODE-05 | IMDRF–MedDRA cross-walk pack `imdrf-meddra-xwalk-2026.csv` for combination products; bidirectional mapping. |
| FS-TIME-01 | URS-TIME-01 | FDA timeline rule pack: 30-day standard MDR; 5-day initial per 21 CFR 803.53 (`remedial-action-flag` triggers 5-day path). |
| FS-TIME-02 | URS-TIME-02 | EU MDR Art. 87 timeline rule pack: 2-day public-health-threat, 10-day death / unanticipated-deterioration, 15-day other-serious. |
| FS-TIME-03 | URS-TIME-03 | DACH-specific rule packs `de-bfarm-2026.yaml`, `ch-swiss-2026.yaml`, `at-ages-2026.yaml`. |
| FS-TIME-04 | URS-TIME-04 | Pre-deadline alerts fire D-3 / D-1 / D0; D0-breach escalation to PagerDuty `vig-prrc-oncall`. |
| FS-TIME-05 | URS-TIME-05 | Reporting-clock golden-test pack `clock-golden-2026.json` covers 25 timeline scenarios; validated via OQ. |
| FS-SUB-01 | URS-SUB-01 | eMDR HL7 ICSR XML generator per 21 CFR 803.21 + FDA eMDR IG; XSD schema validation pre-send. |
| FS-SUB-02 | URS-SUB-02 | EU MIR XML generator per EUDAMED MIR-form schema + per-CA profile during transition. |
| FS-SUB-03 | URS-SUB-03 | Transmission adapter: FDA ESG (eMDR), EUDAMED vigilance (when live), BfArM IRIS, Swissmedic ElViS, AGES, Health Canada CIPARS; ack reconciliation per case. |
| FS-SUB-04 | URS-SUB-04 | Negative-ack workflow: error-code mapping, structured Exception, resubmission within grace period, PRRC escalation on breach. |
| FS-FU-01 | URS-FU-01 | Supplemental-Report generator per 21 CFR 803.10; EU follow-up MIR per EU MDR template; trigger by case-version delta. |
| FS-FU-02 | URS-FU-02 | Final-Report generator on investigation-completion event; separate tracking from initial reports. |
| FS-FU-03 | URS-FU-03 | Open-follow-up commitment register with due-date alerts. |
| FS-TRD-01 | URS-TRD-01 | Trending per device / failure-mode / use-error; configurable statistical methods (Poisson rate-change, CUSUM, EWMA) per device-class in `trend-stats-2026.yaml`. |
| FS-TRD-02 | URS-TRD-02 | Art. 88 trend-report generator: on statistically-significant rate change, generate Art. 88 report and route to relevant CA. |
| FS-TRD-03 | URS-TRD-03 | Denominator from Atlas Serialization sales-volume API; numerator from IMDRF-coded incident count. |
| FS-TRD-04 | URS-TRD-04 | Trend-detection KPI dashboard reviewed monthly by Director of Vigilance. |
| FS-FSCA-01 | URS-FSCA-01 | FSCA decision record schema: rationale, UDI-DI + lot + serial scope, communication plan, CA notifications. |
| FS-FSCA-02 | URS-FSCA-02 | FSN generator using MDCG Art. 89 template; multi-language packs `fsn-templates-{de,en,fr,it,es,pt}.tex`. |
| FS-FSCA-03 | URS-FSCA-03 | FSCA-effectiveness tracker: % field-units recovered, repeat-event rate; post-action quarterly review. |
| FS-FSCA-04 | URS-FSCA-04 | FSCA-CA-routing: FDA + EUDAMED + BfArM + Swissmedic + AGES + Health Canada per scope. |
| FS-MAUDE-01 | URS-MAUDE-01 | MAUDE-prep report endpoint surfaces FDA-submitted MDRs for the device-line; reviewed pre-launch + quarterly. |
| FS-MAUDE-02 | URS-MAUDE-02 | MAUDE redaction policy enforced via DLP regex + manual reviewer gate before FDA submission. |
| FS-EUDAMED-01 | URS-EUDAMED-01 | EUDAMED routing engine: when module live for device class, route to EUDAMED; else national CAs per transition matrix `eudamed-transition.yaml`. |
| FS-EUDAMED-02 | URS-EUDAMED-02 | EUDAMED-module-readiness flag per device class with audit-trailed activation event. |
| FS-RMF-01 | URS-RMF-01 | Bidirectional RMF-link via UDI-DI; case events linked to known hazards in RMF. |
| FS-RMF-02 | URS-RMF-02 | New-hazard-detected event triggers RMF-update workflow per ISO 14971 §10.3. |
| FS-RMF-03 | URS-RMF-03 | Risk-control-effectiveness calculator using post-market incident-rate data; feeds Risk-Management Report. |
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural-control SOPs reviewed annually. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(b): copy generation (PDF / XML / CSV) verified under OQ. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(c): records protected; retention ≥ life-of-product + 10y (≥ 15y implantables) in immutable cold storage. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.10(d): Okta SAML 2.0 + MFA. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.10(e): audit trail per FS-AUD-01. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.50: printed name + date/time + meaning rendered into audit trail + PDF. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.70: HMAC-SHA-256 cryptographic binding of signature to record state. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.100: uniqueness enforced via Okta-DB constraint; user-ids never reassigned. |
| FS-PART11-09 | URS-PART11-09 | Per § 11.200: re-authentication at submission approval + FSCA approval (OAuth2 token max-age 5 min). |
| FS-PART11-10 | URS-PART11-10 | Per § 11.300: password / credential controls per site InfoSec. |
| FS-NCA-BFARM-01 | URS-NCA-BFARM-01 | BfArM IRIS endpoint `https://iris.bfarm.bund.de/vigilance/v1` via mTLS; quarterly connectivity test. |
| FS-NCA-SWISS-01 | URS-NCA-SWISS-01 | Swissmedic ElViS endpoint per HMG / MepV; CH-specific timeline rule pack loaded. |
| FS-NCA-AGES-01 | URS-NCA-AGES-01 | AGES PharmMed endpoint per AMG (AT). |
| FS-NCA-LANG-01 | URS-NCA-LANG-01 | FSN templates de-DE, de-AT, de-CH variants. |
| FS-COMBO-01 | URS-COMBO-01 | Argus cross-reference via daily reconciliation job `argus-theia-reconcile.py`; case-id mapping table maintained. |
| FS-COMBO-02 | URS-COMBO-02 | Dominant-mode-of-action determination drives primary-report regulation; both 21 CFR Part 803 and 314.80 applied where applicable. |
| FS-AUD-01 | URS-AUD-01 | Audit-trail schema: actor, action, old/new, reason, timestamp_iso8601; covers all case / coding / decision / signature / config / submission events. |
| FS-AUD-02 | URS-AUD-02 | Append-only DB constraint; tenant admin cannot UPDATE/DELETE. |
| FS-AUD-03 | URS-AUD-03 | Retention enforced at archive tier per EU MDR Art. 10(8): life-of-product + 10y; +15y implantables. |
| FS-AUD-04 | URS-AUD-04 | Audit-trail review jobs: case-level event-driven monthly; platform-level quarterly. |
| FS-INT-FDA-01 | URS-INT-FDA-01 | FDA ESG eMDR gateway over WebTrader / AS2; certificate rotation under CR; quarterly connectivity test. |
| FS-INT-EUDAMED-01 | URS-INT-EUDAMED-01 | EUDAMED vigilance-module REST API via OAuth2 client-credentials; transition routing to national gateways. |
| FS-INT-PV-01 | URS-INT-PV-01 | Sirius PV (Argus) cross-reference: daily reconciliation job; bidirectional case-id linkage. |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | MasterControl eQMS linkage for CAPA flow; audit-trail propagation. |
| FS-INT-SSO-01 | URS-INT-SSO-01 | Okta SAML 2.0 + MFA; service-account mTLS only. |
| FS-INT-UDI-01 | URS-INT-UDI-01 | Atlas Serialization integration: UDI-DI master + sales-volume API for trending denominator. |
| FS-INT-LIT-01 | URS-INT-LIT-01 | Literature-surveillance feed (Embase / PubMed) for proactive vigilance triage. |
| FS-DI-01 | URS-DI-01 | **Attributable:** `actor_id` not-null on `audit_event`. |
| FS-DI-02 | URS-DI-02 | **Legible:** PDF/A-3 + eMDR XML rendering verified via OQ. |
| FS-DI-03 | URS-DI-03 | **Contemporaneous:** server-side NTP-synced timestamps; retroactive entries flagged. |
| FS-DI-04 | URS-DI-04 | **Original:** raw input preserved; corrections recorded as new versions. |
| FS-DI-05 | URS-DI-05 | **Accurate:** reporting-clock + trend calculations deterministic; OQ-verified. |
| FS-DI-06 | URS-DI-06 | **Complete / Consistent / Enduring / Available:** retention per regulation; chronological order DB-enforced. |
| FS-PERF-01 | URS-PERF-01 | UI P95 ≤ 3s for typical case-page workflows; Grafana SLO. |
| FS-AV-01 | URS-AV-01 | Availability ≥ 99.7%/month per Sparta SLA; 24×7 gateway during submission windows. |
| FS-BAK-01 | URS-BAK-01 | Vendor RPO ≤ 4h, RTO ≤ 24h verified annually via vendor SLA review. |
| FS-SEC-01 | URS-SEC-01 | Okta SAML 2.0 + MFA; per-device / per-region access. |
| FS-SEC-02 | URS-SEC-02 | TLS 1.3 in transit; AES-256 at rest (vendor-confirmed). |
| FS-SEC-03 | URS-SEC-03 | Annual third-party pen-test; high / critical remediation within 60 days under CR. |
| FS-TRN-01 | URS-TRN-01 | LMS-recorded role-specific training; PRRC + eMDR competency required before role-grant. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher `VIG-ANNUAL-2026`: FDA updates, MDCG updates, IMDRF AET annual release. |
| FS-PR-01 | URS-PR-01 | Annual periodic-review run-book auto-collects: vendor qualification, config drift, IMDRF version status, gateway connectivity tests, FSCA effectiveness, deviation summary, training currency; signed by Director Device Vigilance + PRRC + VP Reg Affairs + VP QA. |
| FS-INSP-01 | URS-INSP-01 | Inspection-readiness export endpoint aggregates per-device dossier (complaints + eMDR/MIR log + FSCA + trends + RMF link + training + audit); retrieval P95 ≤ 4 h. |
| FS-INSP-02 | URS-INSP-02 | HA-correspondence register schema (sender, recipient, due-date, response-due-date, status) with SLA monitoring. |
| FS-INSP-03 | URS-INSP-03 | Mock-audit rehearsal workflow with structured findings register and remediation tracker. |


### 4.1 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: SAML 2.0 via Entra ID with SCIM lifecycle provisioning. Conditional-access binding to policy `PV-Sensitive Conditional Access (FIDO2 phishing-resistant MFA + named-location enforcement)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with PostgreSQL pg_basebackup + continuous WAL archiving; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.2 Cross-System Integration — eQMS handover (M-XINT-EQMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-EQMS-01 | URS-XINT-EQMS-01 | CAPA-event publisher posts to eQMS endpoint `POST /capa/tickets` with mTLS + Entra workload-identity; payload schema `eqms.ticket.v1`; OpenAPI artefact `xint-eqms.openapi.yaml`; outbound retry with exponential back-off and DLQ at 5 attempts. |
| FS-XINT-EQMS-02 | URS-XINT-EQMS-02 | eQMS ticket-status webhook subscribed; payload `eqms.status.v1`; consumer rule maps eQMS status `(OPEN, IN-PROGRESS, EFFECTIVENESS, CLOSED)` onto originating-record disposition fields; closed-loop verification gate prevents disposition without `eqms_status=CLOSED`. |


### 4.3 Cross-System Integration — PMS DB (M-XINT-PMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-PMS-01 | URS-XINT-PMS-01 | FSCA-callback publisher posts to PMS DB endpoint `POST /pms/fsca-callback` with mTLS; payload `theia.fsca.callback.v1`; per-device hyperlink and PSUR-evidence binder updated on receipt. |
| FS-XINT-PMS-02 | URS-XINT-PMS-02 | AE case schema extended with `originating_pms_record_id` (nullable); per-case UI shows back-link to the PMS record; reverse-search index `theia-pms-link` supports inspector queries. |

## 5. Configuration Items (CI)

| CI | Item | Value |
|---|---|---|
| CI-01 | Reportability rules version | per-jurisdiction packs |
| CI-02 | IMDRF AET pack version | current MSSO release |
| CI-03 | FDA ESG endpoint | production eMDR endpoint |
| CI-04 | EUDAMED module activation | per device class |
| CI-05 | DACH gateways | BfArM IRIS, Swissmedic ElViS, AGES |
| CI-06 | Trend statistical method | per device-class |
| CI-07 | Audit retention | life-of-product + 10y / +15y implantables |
| CI-08 | Re-authentication on signing | OAuth2 max-age 5 min |
| CI-09 | Argus reconciliation cadence | daily |
| CI-10 | Gateway connectivity tests | quarterly |

## 6. Risks (FS-level)

URS § 9 documents R-01..R-15 at requirements level. Additional FS risks:
- FDA ESG certificate rotation failure → mitigation: certificate-expiry monitoring + auto-alert.
- IMDRF AET annual release schema-change drift → mitigation: contract test against IMDRF pack.
- Argus reconciliation job lag → mitigation: lag monitoring + Director-PMS alert.
- EUDAMED-module activation drift across device classes → mitigation: explicit activation event with audit-trail.

## 7. References

- TEA-URS-MDR-001 v1.2
- 21 CFR Part 803 §§ .1–.58; 21 CFR Part 11
- EU MDR Reg. 2017/745 Arts. 10, 14, 15, 16, 87, 88, 89, 92; EU IVDR Reg. 2017/746 Arts. 82, 83
- MDCG 2023-3; MDCG 2019-9; MDCG 2022-21
- IMDRF AET (WG/N43) Annexes A–G
- ISO 14971:2019; ISO/TR 24971:2020; ISO 13485:2016; ISO/IEC 27001:2022
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026)
- BfArM (DE) MPDG + IRIS; Swissmedic (CH) MepV + ElViS; AGES PharmMed (AT)
- ISPE GAMP 5 (2nd ed., 2022); PIC/S PI 041
- Sparta Systems — *TrackWise Digital Quality (Vigilance Module) 2025 Reference*

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-VND-01 | FS-VND-01 |
| URS-VND-02 | FS-VND-02 |
| URS-VND-03 | FS-VND-03 |
| URS-CFG-01 | FS-CFG-01 |
| URS-CFG-02 | FS-CFG-02 |
| URS-INTAKE-01 | FS-INTAKE-01 |
| URS-INTAKE-02 | FS-INTAKE-02 |
| URS-INTAKE-03 | FS-INTAKE-03 |
| URS-INTAKE-04 | FS-INTAKE-04 |
| URS-INTAKE-05 | FS-INTAKE-05 |
| URS-INTAKE-06 | FS-INTAKE-06 |
| URS-CASE-01 | FS-CASE-01 |
| URS-CASE-02 | FS-CASE-02 |
| URS-CASE-03 | FS-CASE-03 |
| URS-CASE-04 | FS-CASE-04 |
| URS-CASE-05 | FS-CASE-05 |
| URS-CASE-06 | FS-CASE-06 |
| URS-CASE-07 | FS-CASE-07 |
| URS-MDR-01 | FS-MDR-01 |
| URS-MDR-02 | FS-MDR-02 |
| URS-MDR-03 | FS-MDR-03 |
| URS-MDR-04 | FS-MDR-04 |
| URS-MDR-05 | FS-MDR-05 |
| URS-CODE-01 | FS-CODE-01 |
| URS-CODE-02 | FS-CODE-02 |
| URS-CODE-03 | FS-CODE-03 |
| URS-CODE-04 | FS-CODE-04 |
| URS-CODE-05 | FS-CODE-05 |
| URS-TIME-01 | FS-TIME-01 |
| URS-TIME-02 | FS-TIME-02 |
| URS-TIME-03 | FS-TIME-03 |
| URS-TIME-04 | FS-TIME-04 |
| URS-TIME-05 | FS-TIME-05 |
| URS-SUB-01 | FS-SUB-01 |
| URS-SUB-02 | FS-SUB-02 |
| URS-SUB-03 | FS-SUB-03 |
| URS-SUB-04 | FS-SUB-04 |
| URS-FU-01 | FS-FU-01 |
| URS-FU-02 | FS-FU-02 |
| URS-FU-03 | FS-FU-03 |
| URS-TRD-01 | FS-TRD-01 |
| URS-TRD-02 | FS-TRD-02 |
| URS-TRD-03 | FS-TRD-03 |
| URS-TRD-04 | FS-TRD-04 |
| URS-FSCA-01 | FS-FSCA-01 |
| URS-FSCA-02 | FS-FSCA-02 |
| URS-FSCA-03 | FS-FSCA-03 |
| URS-FSCA-04 | FS-FSCA-04 |
| URS-MAUDE-01 | FS-MAUDE-01 |
| URS-MAUDE-02 | FS-MAUDE-02 |
| URS-EUDAMED-01 | FS-EUDAMED-01 |
| URS-EUDAMED-02 | FS-EUDAMED-02 |
| URS-RMF-01 | FS-RMF-01 |
| URS-RMF-02 | FS-RMF-02 |
| URS-RMF-03 | FS-RMF-03 |
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
| URS-NCA-BFARM-01 | FS-NCA-BFARM-01 |
| URS-NCA-SWISS-01 | FS-NCA-SWISS-01 |
| URS-NCA-AGES-01 | FS-NCA-AGES-01 |
| URS-NCA-LANG-01 | FS-NCA-LANG-01 |
| URS-COMBO-01 | FS-COMBO-01 |
| URS-COMBO-02 | FS-COMBO-02 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
| URS-INT-FDA-01 | FS-INT-FDA-01 |
| URS-INT-EUDAMED-01 | FS-INT-EUDAMED-01 |
| URS-INT-PV-01 | FS-INT-PV-01 |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 |
| URS-INT-SSO-01 | FS-INT-SSO-01 |
| URS-INT-UDI-01 | FS-INT-UDI-01 |
| URS-INT-LIT-01 | FS-INT-LIT-01 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-PERF-01 | FS-PERF-01 |
| URS-AV-01 | FS-AV-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-INSP-01 | FS-INSP-01 |
| URS-INSP-02 | FS-INSP-02 |
| URS-INSP-03 | FS-INSP-03 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-EQMS-01 | FS-XINT-EQMS-01 |
| URS-XINT-EQMS-02 | FS-XINT-EQMS-02 |
| URS-XINT-PMS-01 | FS-XINT-PMS-01 |
| URS-XINT-PMS-02 | FS-XINT-PMS-02 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Missed reporting deadline (jurisdictional clock breach) | Medium | High | URS-TIME-01..04 |
| R-02 | eMDR HL7 ICSR XML schema rejection | Medium | High | URS-SUB-01 + schema validation |
| R-03 | Mis-coded event (IMDRF AET annex mis-mapping) | Medium | Medium | URS-CODE-01, URS-CODE-04 |
| R-04 | Reportability decision error (false-negative on serious incident) | Low | Critical | URS-MDR-01..04 |
| R-05 | FDA ESG / EUDAMED gateway loss during submission window | Medium | High | URS-INT-FDA-01, URS-INT-EUDAMED-01, URS-SUB-04 |
| R-06 | Reclassification not re-triggering reporting clocks | Low | Critical | URS-CASE-05 |
| R-07 | 5-day initial report timeline miss for severe public-health-threat event | Medium | Critical | URS-TIME-01 |
| R-08 | Trend false-negative on low-event-rate device | Medium | High | URS-TRD-01 |
| R-09 | FSCA effectiveness not measured | Medium | High | URS-FSCA-03 |
| R-10 | Audit-trail tampering | Low | Critical | URS-AUD-02 |
| R-11 | MAUDE redaction failure exposing PII | Low | High | URS-MAUDE-02 |
| R-12 | Risk-Management-File update not triggered by new hazard | Medium | High | URS-RMF-02 |
| R-13 | Combination-product cross-ref drift (Argus ↔ Theia) | Medium | Medium | URS-COMBO-01 + daily reconciliation |
| R-14 | IMDRF AET version drift on open cases | Low | Medium | URS-CODE-03 |
| R-15 | Duplicate cases across intake channels | Medium | Medium | URS-CASE-07 |

Full evaluation in `TEA-RA-MDR-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
