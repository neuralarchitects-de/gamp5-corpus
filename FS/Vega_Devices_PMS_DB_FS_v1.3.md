---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (FS catch-up to v1.2 URS: dashboard, benefit-risk matrix, HA correspondence, multi-region NB mgmt, complaint intake, data quality)"
seed_corpus_basis:
  - "VGD-URS-PMS-001 v1.2"
  - "GAMP 5 Cat 4 SaaS"
  - "EU MDR 2017/745"
  - "ISO 14971:2019"
  - "ISO 13485:2016"
  - "21 CFR Part 820"
  - "FDA CSA Feb 2026"
  - "BfArM / Swissmedic / AGES"
parent_urs:
  document_number: VGD-URS-PMS-001
  version: 1.2
  file: ../../URS/_generated/final/EU_MDR_Post_Market_Surveillance_DB__Vega_Devices_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# Functional Specification (FS)

## EU MDR Post-Market Surveillance (PMS) Database — Sparta TrackWise Digital PMS Module

**Document Number:** VGD-FS-PMS-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** VGD-URS-PMS-001 v1.2 | **Site:** Vega Devices GmbH, Tuttlingen, Germany *(fictional)*
**Notified Body:** TÜV SÜD Product Service GmbH (CE 0123) *(synthetic placeholder)*
**System Class:** GAMP Cat 4 — Configured Product (multi-tenant SaaS)
**Regulatory Scope:** EU MDR Reg. 2017/745 Arts. 83–92; 21 CFR Part 820 §§ .100, .198; 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; ISO 14971:2019; ISO 13485:2016; MDCG 2019-9 + 2022-21; BfArM (DE) MPDG; Swissmedic (CH) MepV; AGES PharmMed (AT).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Post-Market Surveillance) | _____________ | _____________ | _____ |
| Reviewer (PRRC — EU MDR Art. 15) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Vigilance Manager) | _____________ | _____________ | _____ |
| Reviewer (Clinical Affairs / PMCF Lead) | _____________ | _____________ | _____ |
| Approver (VP Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.1: EU MDR Arts. 87/88/89 implementations; national CA gateway routing (BfArM/Swissmedic/AGES); ISO 14971:2019 alignment; DACH deployment context. |
| 1.2 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.2 (T3 uplift): Real-Time PMS Dashboard (FS-DASH-01..04), Benefit-Risk + PSUR-Risk Matrix (FS-BR-01..04), Health Authority Correspondence + Inspection Readiness (FS-HAC-01..05), Multi-region Notified Body + Authorised Rep mgmt (FS-NB-01..04), Patient + HCP + Distributor complaint intake (FS-INT-PAT/HCP/DIST/DEDUP-01), Data Quality (FS-DQ-01..03); FDA CSA Feb 2026 alignment. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies the implementation of Sparta TrackWise Digital PMS Module configuration to satisfy `VGD-URS-PMS-001` v1.1, including the v1.1 additions for EU MDR Articles 87 (serious-incident reporting), 88 (trend reporting), 89 (FSCA), and 92 (EUDAMED submission), plus national CA gateway routing for DACH.

## 2. Scope

TrackWise Digital PMS Module multi-tenant SaaS; per-device configuration (PMS plan + PSUR template + signal-management workflow + FSCA workflow); SSO via Okta + MFA; integrations with Theia eMDR, MasterControl eQMS, Atlas Serialization, EUDAMED PSUR + vigilance modules, BfArM gateway, Swissmedic gateway, AGES gateway, literature-surveillance feed.

## 3. System Architecture

```
                Okta SSO + MFA
                    │
                    ▼
   ┌─────────────────────────────────────────────────┐
   │  TrackWise Digital PMS Module (Vega Devices)    │
   │  ┌─────────────────────────────────────────┐    │
   │  │ PMS plan (Art. 84)                       │    │
   │  │ PSUR / PSMR (Arts. 85, 86)               │    │
   │  │ Signal mgmt (Art. 88 trend)              │    │
   │  │ Incident triage (Art. 87)                │    │
   │  │ FSCA (Art. 89)                           │    │
   │  │ PMCF                                     │    │
   │  └─────────────────────────────────────────┘    │
   └─┬──────────┬───────────┬───────────┬────────────┘
     │          │           │           │
     ▼          ▼           ▼           ▼
   Theia    MasterControl  Atlas      EUDAMED + BfArM + Swissmedic + AGES
   eMDR     (CAPA)         (sales-vol) (national CA gateways)
```

## 4. Functional Specifications

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VND-01 | URS-VND-01 | Sparta vendor-assurance pack (SOC 2 Type II, ISO 27001, ISO 13485) on file; annual re-qualification workflow. |
| FS-VND-02 | URS-VND-02 | Sparta release-note review automated alert; release-impact assessment within 14 days. |
| FS-CFG-01 | URS-CFG-01 | Per-device configuration: DEV → QC → UAT → PRODUCTION; SoD-enforced signatures (Author ≠ Approver). |
| FS-CFG-02 | URS-CFG-02 | CTIS-compatible study-build pack export per EU MDR Art. 25 (for EU trials referencing this PMS DB). |
| FS-CFG-03 | URS-CFG-03 | Configuration export endpoint `GET /config/export?device_id=...` returns version-stamped JSON. |
| FS-PLAN-01 | URS-PLAN-01 | PMS-plan template per Annex III; review-cadence rules: Class III + implantables ≥ annual; Class IIa/b per Annex III; Class I ≥ 5y. |
| FS-PLAN-02 | URS-PLAN-02 | Execution evidence capture; PMS-plan-deviation handler auto-creates MasterControl deviation record via API. |
| FS-PLAN-03 | URS-PLAN-03 | PMS plan linked to device Technical Documentation (Annex II); change-control gate for updates. |
| FS-PSUR-01 | URS-PSUR-01 | PSUR template per EU MDR Article 86 + MDCG 2022-21; auto-population from PMS data + complaints + literature + Atlas sales volumes. |
| FS-PSUR-02 | URS-PSUR-02 | Class I PSMR per Art. 85 supported via reduced-content template. |
| FS-PSUR-03 | URS-PSUR-03 | PRRC re-authenticated electronic signature for PSUR approval; delegation API endpoint disabled at signature time. |
| FS-PSUR-04 | URS-PSUR-04 | EUDAMED submission via PSUR-module REST API per Art. 92. Cadence engine per Art. 86(1): **Class IIb + Class III + implantables = annual**; **Class IIa = biennial (every 2 years)**; **Class I = PMSR per Art. 85** (different artefact type, routed to PSMR generator). Notified Body assessment loop enabled for Class III + implantables. |
| FS-PSUR-05 | URS-PSUR-05 | PSUR drafts exportable PDF/A-3 with embedded XML. |
| FS-TRD-01 | URS-TRD-01 | Trending per device / failure-mode / use-error per ISO 14971:2019; statistical methods: Poisson rate-change, CUSUM, EWMA per device-class. |
| FS-TRD-02 | URS-TRD-02 | Article 88 trend-report generator: on statistically-significant rate change, generate Art. 88 report and route to relevant national CA via the gateway service. |
| FS-SIG-01 | URS-SIG-01 | Signal-management workflow: confirm → investigate → disposition → CAPA / FSCA; state-machine DB-enforced. |
| FS-SIG-02 | URS-SIG-02 | Signal closure requires evidence-backed disposition; auto-close on timeout disabled by default. |
| FS-PMCF-01 | URS-PMCF-01 | PMCF commitment table with due-dates; CTMS integration via API for clinical-study linkage. |
| FS-PMCF-02 | URS-PMCF-02 | PMCF results feed into PSUR / PSMR auto-population. |
| FS-INC-01 | URS-INC-01 | Bidirectional cross-reference to Theia eMDR system via `incident_id` foreign key. |
| FS-INC-02 | URS-INC-02 | Serious-incident timeline rules engine: 15-day standard, 10-day public-health-threat, 2-day death; pre-deadline alerts at D-3, D-1, D0. |
| FS-INC-03 | URS-INC-03 | Class-change watcher (non-serious → serious) re-triggers reporting clocks; audit-logged. |
| FS-INC-04 | URS-INC-04 | National CA routing service: DE → BfArM gateway, CH → Swissmedic gateway, AT → AGES gateway; plus EUDAMED vigilance for EU-wide events. |
| FS-FSCA-01 | URS-FSCA-01 | FSCA decision record schema: rationale, scope, communication plan, CA notifications; PRRC sign-off required. |
| FS-FSCA-02 | URS-FSCA-02 | FSN generator using MDCG-prescribed Art. 89 template. |
| FS-FSCA-03 | URS-FSCA-03 | FSCA effectiveness tracker with post-action quantitative metric where feasible. |
| FS-AUD-01 | URS-AUD-01 | Audit-trail schema: actor, action, old/new value, reason, timestamp_iso8601; covers all PMS / PSUR / signal / FSCA events. |
| FS-AUD-02 | URS-AUD-02 | Append-only DB constraint; tenant-admin role cannot UPDATE/DELETE. |
| FS-AUD-03 | URS-AUD-03 | Retention 10y / 15y (implantables) enforced at archive tier. |
| FS-AUD-04 | URS-AUD-04 | Weekly System Owner review + annual QA review (saved-search + signed report). |
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural controls protecting electronic-record validity documented in `/sop/`; reviewed annually. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(d): access limited to authorised individuals via Okta SAML 2.0 + MFA; service accounts via mTLS only. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(e): operational audit trail capturing user, action, date, time — implemented via FS-AUD-01. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.50: electronic signatures include signer's printed name, date and time of signing, and meaning of signature; schema enforced in DB. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.70: signatures cryptographically linked to the signed record via HMAC-SHA256 over record-hash + signer-id + timestamp; tampered records flagged on read. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.100: signature unique per individual; reuse / reassignment blocked at provisioning via Okta-DB uniqueness constraint. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.200: re-authentication required at the moment of signing (fresh OAuth2 token, max-age 5 min); cached credentials rejected. |
| FS-DI-01 | URS-DI-01 | **Attributable:** every action / entry carries `actor_id` (named user or service-account); DB constraint not-null at audit-write. |
| FS-DI-02 | URS-DI-02 | **Legible:** records exportable as PDF/A-3 + machine-readable JSON/XML; rendering verified via OQ. |
| FS-DI-03 | URS-DI-03 | **Contemporaneous:** event timestamps server-side + NTP-synced; retroactive entries flagged with delay reason. |
| FS-DI-04 | URS-DI-04 | **Original:** raw inputs / records preserved in immutable storage; derivative analyses reference but do not overwrite the original. |
| FS-DI-05 | URS-DI-05 | **Accurate:** calculations / transformations deterministic and validated under OQ; floating-point reproducibility verified where applicable. |
| FS-DI-06 | URS-DI-06 | **Complete / Consistent / Enduring / Available:** metadata completeness validated; chronological order DB-enforced; retention per applicable regulation; retrievable within 1 business day. |
| FS-INT-EMDR-01 | URS-INT-EMDR-01 | Bidirectional Theia eMDR integration via JSON-over-mTLS. |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | MasterControl CAPA linkage with audit-trail propagation. |
| FS-INT-SER-01 | URS-INT-SER-01 | Atlas Serialization sales-volume API for denominator in Art. 88 trending. |
| FS-INT-EUDAMED-01 | URS-INT-EUDAMED-01 | EUDAMED PSUR + vigilance module REST APIs; submission via OAuth2 client-credentials flow. |
| FS-INT-BFARM-01 | URS-INT-BFARM-01 | BfArM gateway (MPDG-compliant submission interface) via mTLS; manual fallback documented. |
| FS-INT-SWISS-01 | URS-INT-SWISS-01 | Swissmedic gateway (MepV-compliant) via mTLS; manual fallback documented. |
| FS-INT-AGES-01 | URS-INT-AGES-01 | AGES PharmMed gateway via mTLS; manual fallback documented. |
| FS-INT-LIT-01 | URS-INT-LIT-01 | Embase / PubMed feed via vendor service; daily ingestion with deduplication. |
| FS-PERF-01 | URS-PERF-01 | UI P95 ≤ 3 s for PMS Specialist workflows; verified via Grafana SLO. |
| FS-AV-01 | URS-AV-01 | Availability ≥ 99.5%/month per Sparta SLA. |
| FS-BAK-01 | URS-BAK-01 | Site tenant-data export quarterly with 10y retention in cold storage. |
| FS-BAK-02 | URS-BAK-02 | Vendor RTO ≤ 24h / RPO ≤ 4h verified annually. |
| FS-SEC-01 | URS-SEC-01 | TLS 1.3 in transit; AES-256 at rest (vendor-confirmed). |
| FS-SEC-02 | URS-SEC-02 | RBAC review quarterly; PRRC role assignment requires Reg-Affairs approval. |
| FS-SEC-03 | URS-SEC-03 | Annual pen-test; high/critical findings remediated within 60 days under change control. |
| FS-TRN-01 | URS-TRN-01 | LMS-recorded role-specific training; PRRC training mandatory before role-grant. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher `MDR-2026-ANNUAL`: EU MDR + MDCG + FSCA + national CA changes. |
| FS-PR-01 | URS-PR-01 | Annual Periodic Review template (vendor qualification + config drift + audit-trail review + PMS-plan adherence + PMCF status + signal metrics + integration health + training); signed by Director PMS + PRRC + VP QA + VP Reg Affairs. |
| FS-DASH-01 | URS-DASH-01 | Real-time PMS dashboard service (Grafana fronted by `pms-dash-api`) surfacing per-device KPIs: rolling-90-day complaint rate, serious-incident count + rate, Art. 88 CUSUM/EWMA, PMCF commitment status, PMS-plan cycle status; refresh latency P95 ≤ 15 min from event arrival; SLO `dashboard_freshness_seconds`. |
| FS-DASH-02 | URS-DASH-02 | Per-device drill-down panels: triage breakdown, reporting-clock margin distribution histogram, Notified-Body-required-item status table. |
| FS-DASH-03 | URS-DASH-03 | Dashboard export (PNG / PDF / CSV) endpoint includes data-cut timestamp + dataset SHA-256 checksum in the export footer. |
| FS-DASH-04 | URS-DASH-04 | KPI-threshold engine (`pms-threshold.yaml`) configurable per device; breach events emit to Slack `#pms-alerts` + PagerDuty `pms-oncall` (Director PMS + PRRC). |
| FS-BR-01 | URS-BR-01 | Device-level Benefit-Risk Profile module per ISO 14971:2019 §10; hazard-source links to PMS data; PSUR Section 6 auto-extraction. |
| FS-BR-02 | URS-BR-02 | PSUR-Risk Matrix data model: hazard ↔ control-measure ↔ residual-risk ↔ post-market-evidence ↔ action; PSUR generator queries matrix at build time. |
| FS-BR-03 | URS-BR-03 | Risk-control-effectiveness tracker: PMS-derived incident-rate per control; threshold breach raises change-flag per ISO 14971:2019 §10.3. |
| FS-BR-04 | URS-BR-04 | Bidirectional Risk-Management File link via UDI-DI; RMF update triggered by signal-closure + FSCA events. |
| FS-HAC-01 | URS-HAC-01 | Health-Authority Correspondence register (`hac_correspondence` schema): sender, recipient, due-date, response-due-date, status; covers CA queries, Notified-Body queries, PSUR feedback, FSCA ack. |
| FS-HAC-02 | URS-HAC-02 | CA-query response workflow: drafter → reviewer → PRRC approver SoD-enforced; response package export in inspection-ready PDF/A-3. |
| FS-HAC-03 | URS-HAC-03 | Inspection-readiness export aggregates: PMS plan, PSURs, PMS reports, FSCAs, complaint summary, training records, audit-trail extracts; one-click dossier; retrieval ≤ 4h. |
| FS-HAC-04 | URS-HAC-04 | Mock-audit rehearsal workflow with structured findings register. |
| FS-HAC-05 | URS-HAC-05 | Notified-Body correspondence tagged in register with `nb_id` (e.g., `CE-0123-TUVSUD`); audit-visible filter. |
| FS-NB-01 | URS-NB-01 | Notified-Body designation register per device per market: TÜV SÜD CE 0123 (EU); UK-Approved-Body (UKCA); CH-REP (Swiss); ANVISA holder (BR); certificate-expiry alerts at 90/60/30/7 days. |
| FS-NB-02 | URS-NB-02 | Notified-Body PSUR-assessment tracker per EU MDR Art. 86(2): assessment-due-date + outcome captured; missed-assessment alert. |
| FS-NB-03 | URS-NB-03 | Authorised-Representative register per market: EU AR (Art. 11), CH-REP (MepV), UK Responsible Person, SG Importer, BR ANVISA holder; per-device-per-market binding. |
| FS-NB-04 | URS-NB-04 | Certificate-transition workflow (e.g., MDD → MDR) with milestones + evidence checklist. |
| FS-INT-PAT-01 | URS-INT-PAT-01 | Patient-direct complaint intake via secure web form (`/intake/patient`) + phone-ticket integration (Zendesk); GDPR-compliant data set (consent capture, contact, device, complaint description). |
| FS-INT-HCP-01 | URS-INT-HCP-01 | HCP complaint intake via HCP-portal `hcp.vegadevices.de` + email-gateway parser (`vigilance-hcp@vegadevices.de`); HCP-role / qualification captured. |
| FS-INT-DIST-01 | URS-INT-DIST-01 | Distributor / importer intake per EU MDR Arts. 14, 16; chain-of-custody fields captured. |
| FS-INT-DEDUP-01 | URS-INT-DEDUP-01 | Complaint-deduplication rule engine across patient + HCP + distributor channels (UDI-DI + complainant identifiers + event-date proximity); suspected-duplicates routed to Vigilance Specialist queue. |
| FS-DQ-01 | URS-DQ-01 | Mandatory-field validator per EU MDR Art. 87 Annex: blocks state transition on incomplete mandatory fields; runs on every state transition. |
| FS-DQ-02 | URS-DQ-02 | Field-content validator: ISO 3166-1 country codes, IMDRF UDI-DI format, ISO 8601 dates; rejection messages field-specific. |
| FS-DQ-03 | URS-DQ-03 | Data-quality KPI report monthly (% missing optional fields, % corrected fields). |
| FS-PLAN-AUTH-01 | URS-PLAN-AUTH-01 | PMS-plan authoring UI uses Annex III template; section-binding validator enforces completeness before approval. |
| FS-PLAN-AUTH-02 | URS-PLAN-AUTH-02 | PMS-plan-cycle execution tracker (`cycle_id`, `cycle_start`, `milestones`, `cycle_end`, `deviations`); cycle state visible in dashboard. |
| FS-PLAN-AUTH-03 | URS-PLAN-AUTH-03 | PMS-plan dependency graph links to PMCF protocol, literature-search strategy, registry-pull frequency lifecycle artefacts. |
| FS-PLAN-AUTH-04 | URS-PLAN-AUTH-04 | Plan-approval signature requires Director PMS + PRRC + VP QA via SoD-enforced workflow; modifications re-enter approval. |
| FS-EUDAMED-MOD-01 | URS-EUDAMED-MOD-01 | EUDAMED Actor module API integration; nightly sync of manufacturer / AR / importer / SPP-producer registration. |
| FS-EUDAMED-MOD-02 | URS-EUDAMED-MOD-02 | EUDAMED UDI / Device module integration: UDI-DI / UDI-PI / Basic UDI-DI tracking; Art. 29 submission. |
| FS-EUDAMED-MOD-03 | URS-EUDAMED-MOD-03 | EUDAMED Certificate module integration; certificate-expiry alerts at 90/60/30/7 days. |
| FS-EUDAMED-MOD-04 | URS-EUDAMED-MOD-04 | EUDAMED Vigilance module: serious-incident + Art. 88 trend + FSCA routed via EUDAMED REST. |
| FS-EUDAMED-MOD-05 | URS-EUDAMED-MOD-05 | EUDAMED Market Surveillance module: CA-driven investigations tracked with case-id linkage. |
| FS-EUDAMED-MOD-06 | URS-EUDAMED-MOD-06 | EUDAMED Clinical Investigation and PMCF Studies module: PMCF studies registered + Art. 74 status updates. |
| FS-RM-01 | URS-RM-01 | Bidirectional RMF-link via UDI-DI; PMS data ↔ RMF hazards. |
| FS-RM-02 | URS-RM-02 | ISO 14971:2019 § 10 workflow implemented: § 10.1 information collection, § 10.2 review, § 10.3 actions. |
| FS-RM-03 | URS-RM-03 | New-hazard event raises RMF-update CR; CR tracked to closure. |
| FS-RM-04 | URS-RM-04 | RM Plan template references PMS data collection methods + residual-risk acceptance per ISO/TR 24971:2020. |
| FS-RM-05 | URS-RM-05 | Risk-Management Review meeting cadence configured; PMS metrics surfaced as primary input. |
| FS-RM-06 | URS-RM-06 | Hazard-to-event traceability table: each PMS event ↔ {0, 1+} known hazards; new-hazard event audit-trailed. |


### 4.1 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: SAML 2.0 via Entra ID with SCIM lifecycle provisioning. Conditional-access binding to policy `PMS-Sensitive Conditional Access (FIDO2 phishing-resistant MFA)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with PostgreSQL pg_basebackup + continuous WAL archiving; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.2 Cross-System Integration — eQMS handover (M-XINT-EQMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-EQMS-01 | URS-XINT-EQMS-01 | CAPA-event publisher posts to eQMS endpoint `POST /capa/tickets` with mTLS + Entra workload-identity; payload schema `eqms.ticket.v1`; OpenAPI artefact `xint-eqms.openapi.yaml`; outbound retry with exponential back-off and DLQ at 5 attempts. |
| FS-XINT-EQMS-02 | URS-XINT-EQMS-02 | eQMS ticket-status webhook subscribed; payload `eqms.status.v1`; consumer rule maps eQMS status `(OPEN, IN-PROGRESS, EFFECTIVENESS, CLOSED)` onto originating-record disposition fields; closed-loop verification gate prevents disposition without `eqms_status=CLOSED`. |


### 4.3 Cross-System Integration — Adverse Event DB (M-XINT-AE)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-AE-01 | URS-XINT-AE-01 | Vigilance-signal publisher posts to AE DB endpoint `POST /ae/signals` with mTLS + Entra workload-identity; payload schema `theia.ae.v1`; idempotency on `{device_udi, signal_class, detection_window_id}`; at-least-once delivery; DLQ at 10 attempts. |
| FS-XINT-AE-02 | URS-XINT-AE-02 | AE FSCA-callback webhook subscribed; payload `theia.fsca.callback.v1`; consumer rule maps callback onto PMS plan state and PSUR-evidence binder; per-device hyperlink to the AE FSCA case persisted in the PMS UI. |

## 5. Configuration Items (CI)

| CI | Item | Value |
|---|---|---|
| CI-01 | PMS-plan cadence | per device-class (Annex III) |
| CI-02 | PRRC sign-off | required for PSUR (non-delegatable) |
| CI-03 | EUDAMED submission | active per device class |
| CI-04 | National CA routing | DE → BfArM, CH → Swissmedic, AT → AGES |
| CI-05 | Notified Body | TÜV SÜD CE 0123 (synthetic placeholder) |
| CI-06 | Trend stats method | Poisson / CUSUM / EWMA per device-class |
| CI-07 | Audit retention | 10y / 15y implantables |

## 6. Risks (FS-level)

Implementation-level risks; URS § 9 documents R-01..R-12 at requirements level. Additional FS risks:

- National-CA gateway certificate rotation failure → mitigation: monitoring + auto-alert
- Atlas sales-volume API schema change breaks Art. 88 denominator → mitigation: contract test + integration health endpoint
- EUDAMED PSUR module version mismatch → mitigation: pinned API version + migration runbook

## 7. References

- VGD-URS-PMS-001 v1.2
- EU MDR Reg. 2017/745 Arts. 10, 11, 14, 15, 16, 83–92
- MDCG 2019-9, 2022-21, 2023-3
- 21 CFR Part 820 §§ .100, .198; 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance)
- ISO 14971:2019; ISO/TR 24971:2020; ISO 13485:2016
- BfArM (DE) MPDG; Swissmedic (CH) MepV; AGES PharmMed (AT); UK MHRA UKCA; ANVISA (BR)
- ISPE GAMP 5 (2nd ed., 2022); PIC/S PI 041; ISO/IEC 27001:2022
- Sparta — *TrackWise Digital PMS Module Configuration and Administration Reference*

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-VND-01 | FS-VND-01 |
| URS-VND-02 | FS-VND-02 |
| URS-CFG-01 | FS-CFG-01 |
| URS-CFG-02 | FS-CFG-02 |
| URS-CFG-03 | FS-CFG-03 |
| URS-PLAN-01 | FS-PLAN-01 |
| URS-PLAN-02 | FS-PLAN-02 |
| URS-PLAN-03 | FS-PLAN-03 |
| URS-PSUR-01 | FS-PSUR-01 |
| URS-PSUR-02 | FS-PSUR-02 |
| URS-PSUR-03 | FS-PSUR-03 |
| URS-PSUR-04 | FS-PSUR-04 |
| URS-PSUR-05 | FS-PSUR-05 |
| URS-TRD-01 | FS-TRD-01 |
| URS-TRD-02 | FS-TRD-02 |
| URS-SIG-01 | FS-SIG-01 |
| URS-SIG-02 | FS-SIG-02 |
| URS-PMCF-01 | FS-PMCF-01 |
| URS-PMCF-02 | FS-PMCF-02 |
| URS-INC-01 | FS-INC-01 |
| URS-INC-02 | FS-INC-02 |
| URS-INC-03 | FS-INC-03 |
| URS-INC-04 | FS-INC-04 |
| URS-FSCA-01 | FS-FSCA-01 |
| URS-FSCA-02 | FS-FSCA-02 |
| URS-FSCA-03 | FS-FSCA-03 |
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
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-INT-EMDR-01 | FS-INT-EMDR-01 |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 |
| URS-INT-SER-01 | FS-INT-SER-01 |
| URS-INT-EUDAMED-01 | FS-INT-EUDAMED-01 |
| URS-INT-BFARM-01 | FS-INT-BFARM-01 |
| URS-INT-SWISS-01 | FS-INT-SWISS-01 |
| URS-INT-AGES-01 | FS-INT-AGES-01 |
| URS-INT-LIT-01 | FS-INT-LIT-01 |
| URS-PERF-01 | FS-PERF-01 |
| URS-AV-01 | FS-AV-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-DASH-01 | FS-DASH-01 |
| URS-DASH-02 | FS-DASH-02 |
| URS-DASH-03 | FS-DASH-03 |
| URS-DASH-04 | FS-DASH-04 |
| URS-BR-01 | FS-BR-01 |
| URS-BR-02 | FS-BR-02 |
| URS-BR-03 | FS-BR-03 |
| URS-BR-04 | FS-BR-04 |
| URS-HAC-01 | FS-HAC-01 |
| URS-HAC-02 | FS-HAC-02 |
| URS-HAC-03 | FS-HAC-03 |
| URS-HAC-04 | FS-HAC-04 |
| URS-HAC-05 | FS-HAC-05 |
| URS-NB-01 | FS-NB-01 |
| URS-NB-02 | FS-NB-02 |
| URS-NB-03 | FS-NB-03 |
| URS-NB-04 | FS-NB-04 |
| URS-INT-PAT-01 | FS-INT-PAT-01 |
| URS-INT-HCP-01 | FS-INT-HCP-01 |
| URS-INT-DIST-01 | FS-INT-DIST-01 |
| URS-INT-DEDUP-01 | FS-INT-DEDUP-01 |
| URS-DQ-01 | FS-DQ-01 |
| URS-DQ-02 | FS-DQ-02 |
| URS-DQ-03 | FS-DQ-03 |
| URS-PLAN-AUTH-01 | FS-PLAN-AUTH-01 |
| URS-PLAN-AUTH-02 | FS-PLAN-AUTH-02 |
| URS-PLAN-AUTH-03 | FS-PLAN-AUTH-03 |
| URS-PLAN-AUTH-04 | FS-PLAN-AUTH-04 |
| URS-EUDAMED-MOD-01 | FS-EUDAMED-MOD-01 |
| URS-EUDAMED-MOD-02 | FS-EUDAMED-MOD-02 |
| URS-EUDAMED-MOD-03 | FS-EUDAMED-MOD-03 |
| URS-EUDAMED-MOD-04 | FS-EUDAMED-MOD-04 |
| URS-EUDAMED-MOD-05 | FS-EUDAMED-MOD-05 |
| URS-EUDAMED-MOD-06 | FS-EUDAMED-MOD-06 |
| URS-RM-01 | FS-RM-01 |
| URS-RM-02 | FS-RM-02 |
| URS-RM-03 | FS-RM-03 |
| URS-RM-04 | FS-RM-04 |
| URS-RM-05 | FS-RM-05 |
| URS-RM-06 | FS-RM-06 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-EQMS-01 | FS-XINT-EQMS-01 |
| URS-XINT-EQMS-02 | FS-XINT-EQMS-02 |
| URS-XINT-AE-01 | FS-XINT-AE-01 |
| URS-XINT-AE-02 | FS-XINT-AE-02 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Missed PSUR deadline | Medium | High | URS-PSUR-04, URS-PSUR-03 + alerts |
| R-02 | Signal not detected in trending (false-negative) | Medium | High | URS-TRD-01, URS-TRD-02 (Art. 88) + statistical tests |
| R-03 | Missed Article 87 serious-incident reporting timeline | Medium | Critical | URS-INC-01, URS-INC-02, URS-INC-03 |
| R-04 | PMCF commitment slipped | Medium | Medium | URS-PMCF-01 + alerts |
| R-05 | Audit-trail tampering | Low | Critical | URS-AUD-02 |
| R-06 | National competent authority gateway outage at submission window | Medium | High | URS-INT-BFARM-01, URS-INT-SWISS-01, URS-INT-AGES-01 (manual fallback documented) |
| R-07 | Vendor SaaS outage during high-risk window | Medium | Medium | URS-BAK-02, URS-AV-01 |
| R-08 | Class change (non-serious → serious) not re-triggering reporting timelines | Low | Critical | URS-INC-03 |
| R-09 | Trend statistical method invalid for low-event-rate device | Medium | Medium | URS-TRD-01 (per-class method choice) |
| R-10 | PRRC signature delegation under time pressure | Low | High | URS-PSUR-03 (delegation block at signature time) |
| R-11 | Data residency non-compliance (EU MDR data crossing jurisdictions inappropriately) | Low | High | URS-SEC-01 + vendor DPA |
| R-12 | Sales-volume integration drift breaking trend denominator | Medium | Medium | URS-INT-SER-01 + integration health check |
| R-13 | Real-time dashboard staleness undetected during inspection | Low | High | URS-DASH-01 (latency probe) + URS-HAC-03 |
| R-14 | Notified-Body PSUR assessment milestone missed | Low | High | URS-NB-02 + URS-PSUR-03 |
| R-15 | Risk-control effectiveness drift unnoticed (ISO 14971 §10.3) | Medium | High | URS-BR-03 |
| R-16 | Health-authority correspondence response deadline breach | Medium | High | URS-HAC-01, URS-HAC-02 |
| R-17 | Duplicate complaints across patient + HCP + distributor channels | Medium | Medium | URS-INT-DEDUP-01 |

Full evaluation in `VGD-RA-PMS-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
