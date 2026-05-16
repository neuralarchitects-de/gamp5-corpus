---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "VGD-FS-PMS-001 v1.3 (parent FS)"
  - "VGD-URS-PMS-001 v1.3 (parent URS, transitive)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 Configuration Specification conventions"
  - "EU MDR Reg. 2017/745 Arts. 10, 11, 14, 15, 16, 83–92"
  - "21 CFR Part 820 §§ .100, .198; 21 CFR Part 803 (MDR); 21 CFR Part 821 (UDI tracking); 21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300"
  - "MDCG 2019-9, 2022-21, 2023-3"
  - "FDA Computer Software Assurance for Production and Quality Management System Software (final, February 2026; supersedes the September 2025 guidance)"
  - "FDA Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions (Aug 2025)"
  - "ISO 14971:2019; ISO/TR 24971:2020; ISO 13485:2016"
  - "BfArM (DE) MPDG; Swissmedic (CH) MepV; AGES PharmMed (AT)"
  - "Sparta TrackWise Digital PMS Module — Configuration and Administration Reference"
parent_fs:
  document_number: VGD-FS-PMS-001
  version: 1.3
  file: ../../../FS_FDS/_generated/final/Vega_Devices_PMS_DB_FS_v1.3.md
parent_urs:
  document_number: VGD-URS-PMS-001
  version: 1.3
  file: ../../../URS/_generated/final/EU_MDR_Post_Market_Surveillance_DB__Vega_Devices_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## EU MDR Post-Market Surveillance (PMS) Database — Sparta TrackWise Digital PMS Module — Configuration Specification

**Document Number:** VGD-DS-PMS-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Parent FS:** VGD-FS-PMS-001 v1.3
**Parent URS:** VGD-URS-PMS-001 v1.3 *(informational; transitive via FS)*
**Site:** Vega Devices GmbH, Tuttlingen, Germany *(fictional)*
**Notified Body:** TÜV SÜD Product Service GmbH (CE 0123) *(synthetic placeholder)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS)
**Project Mode:** Sustaining + Configurable Change *(inherited from parent URS)*
**Regulatory Scope:** EU MDR Reg. 2017/745 Arts. 10, 11, 14, 15, 16, 83–92; 21 CFR Part 820 §§ .100, .198; 21 CFR Part 803 (MDR); 21 CFR Part 821 (UDI tracking); 21 CFR Part 11 §§ .10/.30/.50/.70/.100/.200/.300; FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance); FDA *Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions* (Aug 2025); ISO 14971:2019; ISO/TR 24971:2020; ISO 13485:2016; MDCG 2019-9 + 2022-21 + 2023-3; BfArM (DE) MPDG; Swissmedic (CH) MepV; AGES PharmMed (AT); UK MHRA UKCA; ANVISA (BR); ISO/IEC 27001:2022; PIC/S PI 041.

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QA Reviewer) | _____________ | _____________ | _____ |
| Reviewer (System Owner — Director, Post-Market Surveillance) | _____________ | _____________ | _____ |
| Reviewer (Process Owner — PRRC per EU MDR Art. 15) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Vigilance Manager) | _____________ | _____________ | _____ |
| Reviewer (Clinical Affairs / PMCF Lead) | _____________ | _____________ | _____ |
| Approver (VP Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Design Control

| Field | Value |
|---|---|
| Document Number | VGD-DS-PMS-001 |
| Version | 1.1 |
| Effective Date *(synthetic)* | 2026-05-15 |
| Parent FS | VGD-FS-PMS-001 v1.3 |
| Parent URS *(informational)* | VGD-URS-PMS-001 v1.3 |
| Site | Vega Devices GmbH, Tuttlingen, Germany *(fictional)* |
| Notified Body | TÜV SÜD Product Service GmbH (CE 0123) *(synthetic placeholder)* |
| System Class (GAMP 5, 2nd ed.) | Category 4 — Configured Product (multi-tenant SaaS) |
| Project Mode | Sustaining + Configurable Change |
| Regulatory Scope | per Title block |
| Tier | T3-T4 (inherited from parent URS+FS pair) |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue of Configuration Specification for Sparta TrackWise Digital PMS Module corresponding to VGD-FS-PMS-001 v1.3. Inherited Tier T3-T4 from parent URS+FS pair. DS covers 118/118 FS-IDs (100% coverage). Vendor-internal Sparta TrackWise Digital platform internals are flagged as **vendor-internal — no site design surface**. PSUR cadence rule explicitly: Class IIb + Class III + implantables = annual; Class IIa = biennial; Class I = PMSR per EU MDR Art. 85. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from VGD-URS-PMS-001 v1.3 and VGD-FS-PMS-001 v1.3. DS-specific additions:

| Term | Definition |
|---|---|
| PMS | Post-Market Surveillance |
| PSUR | Periodic Safety Update Report (EU MDR Art. 86) |
| PSMR | Post-Market Surveillance Report (EU MDR Art. 85 — Class I) |
| PMCF | Post-Market Clinical Follow-up |
| FSCA | Field Safety Corrective Action |
| FSN | Field Safety Notice |
| PRRC | Person Responsible for Regulatory Compliance (EU MDR Art. 15) |
| EUDAMED | European Database on Medical Devices |
| UDI-DI / UDI-PI / Basic UDI-DI | Unique Device Identifier — Device / Production / Basic identifiers |
| MDR | Medical Device Reporting (FDA) / EU Medical Device Regulation (context-dependent) |
| RMF | Risk Management File |
| EUDAMED Actor / UDI / Certificate / Vigilance / Market Surveillance / Clinical Investigation modules | EUDAMED sub-modules |
| Theia eMDR | Vega's eMDR counterparty (synthetic) |
| Atlas Serialization | Vega's serialisation system providing sales volumes |

---

## 1. Purpose

This Configuration Specification defines, at the platform-tenancy level, the configuration values, workflow designs, role-permission matrix, and integration endpoint designs that implement VGD-FS-PMS-001 v1.3 for the Sparta TrackWise Digital PMS Module tenancy at Vega Devices GmbH (Tuttlingen, DE). It is the third document in the GAMP 5 V-model for the Vega EU MDR PMS Database.

## 2. Scope

### 2.1 In Scope

- Sparta TrackWise Digital PMS Module tenancy configuration — PMS plan + PSUR template + signal-management workflow + FSCA workflow + Article 88 trend reporting + Article 87 serious-incident workflow + EUDAMED Art. 92 submission.
- Per-device configuration with class-driven cadence (Class IIb + III + implantables annual; Class IIa biennial; Class I PMSR per Art. 85).
- National-CA gateway routing (DE → BfArM, CH → Swissmedic, AT → AGES) + EUDAMED for EU-wide.
- Theia eMDR + MasterControl eQMS + Atlas Serialization integrations.
- Real-Time PMS Dashboard + Benefit-Risk Matrix + Health-Authority Correspondence + Multi-region Notified Body + Patient/HCP/Distributor intake + Data Quality.
- ISO 14971:2019 § 10 Risk Management workflow + RMF bidirectional link.
- Cross-system planes — AD identity, AUR backup tier, eQMS handover, AE DB handover (Theia).

### 2.2 Out of Scope

- Per-device PMS plan body content (per-device DS sub-documents).
- Vendor platform internals (Sparta SDLC).
- Cross-system AD design (QTZ-DS-AD-001).
- Cross-system backup design (AUR-DS-BACKUP-001).
- eMDR system internals (Theia SDLC).

## 3. Architectural Overview

The Vega Devices PMS Database is a **multi-tenant SaaS** Cat 4 system functioning as the EU MDR-compliant Post-Market Surveillance hub. It orchestrates PMS plan execution + PSUR / PSMR generation + signal management + Article 87 serious-incident reporting + Article 88 trend reporting + Article 89 FSCA management + Article 92 EUDAMED submission, integrating with Theia eMDR, MasterControl, Atlas Serialization, EUDAMED (six sub-modules), and national CA gateways (BfArM / Swissmedic / AGES).

### 3.1 Platform Architectural Diagram

```
                Okta SSO + MFA (SAML 2.0 + SCIM 2.0)
                       │
                       ▼
   ┌────────────────────────────────────────────────────────────────────────┐
   │   TrackWise Digital PMS Module (Vega Devices tenancy)                  │
   │                                                                        │
   │   ┌─────────────────────────────────────────────────────────────┐      │
   │   │  PMS plan (Art. 84) — per device-class cadence              │      │
   │   │  PSUR / PSMR (Arts. 85, 86)                                 │      │
   │   │  Signal mgmt — confirm → investigate → disposition → CAPA/  │      │
   │   │  FSCA (state-machine DB-enforced)                            │      │
   │   │  Incident triage (Art. 87) — 2/10/15-day timeline rules     │      │
   │   │  FSCA (Art. 89) — rationale + scope + comms + CA notif      │      │
   │   │  Article 88 trend reporting — Poisson / CUSUM / EWMA        │      │
   │   │  PMCF commitment table                                       │      │
   │   │  Real-time PMS Dashboard (Grafana, ≤ 15 min latency)         │      │
   │   │  Benefit-Risk Matrix + RMF link (via UDI-DI)                 │      │
   │   │  HA Correspondence register                                  │      │
   │   │  Notified-Body designation + AR register                     │      │
   │   │  Patient + HCP + Distributor intake (with dedup)             │      │
   │   │  Data Quality validators                                     │      │
   │   └─────────────────────────────────────────────────────────────┘      │
   └─┬──────────┬───────────┬───────────┬───────────────┬─────────────────┘
     │          │           │           │               │
     ▼          ▼           ▼           ▼               ▼
   Theia    Master-      Atlas       EUDAMED          BfArM / Swissmedic /
   eMDR     Control      Serial.     (Actor /         AGES national CA
   (mTLS    (CAPA REST   (sales-     UDI /            gateways
   JSON)    + idemp.)    volume      Certificate /    (mTLS + manual
            (closed-     denom.)     Vigilance /      fallback)
            loop)                    Market Surv. /
                                     Clinical Inv.)
       │
       ▼
   ┌────────────────────────────────────────────────────────────────────────────┐
   │  Cross-system planes                                                       │
   │  • QTZ AD / Entra ID (SAML+SCIM, Splunk gxp-authn, CyberArk PAM, FIDO2)    │
   │  • AUR Backup (Veeam + PostgreSQL pg_basebackup + WAL + S3 Object Lock +   │
   │    LTO-9 air-gap)                                                          │
   │  • eQMS handover (POST /capa/tickets; status webhook; closed-loop gate)    │
   │  • AE DB handover (POST /ae/signals; FSCA callback webhook)                │
   └────────────────────────────────────────────────────────────────────────────┘
```

### 3.2 PSUR Cadence per Device Class (Art. 86)

| Device class | PSUR cadence | Notified Body assessment loop |
|---|---|---|
| Class IIb (non-implantable) | **Annual** | No (per Art. 86(2)) |
| Class III | **Annual** | Yes |
| Implantable (incl. Class IIb implantable) | **Annual** | Yes |
| Class IIa | **Biennial (every 2 years)** | No |
| Class I | **PMSR per Art. 85** (different artefact type, reduced content) | N/A |

### 3.3 Counterparty Integration Map

| Counterparty | Protocol | Direction | Endpoint pattern | Auth | FS-ID |
|---|---|---|---|---|---|
| Theia eMDR | REST (JSON over mTLS) | bidirectional | `theia.vega-prod.local/v1/` | mTLS | FS-INT-EMDR-01 |
| MasterControl eQMS | REST | bidirectional | `mc.vega-prod.local/v1/` | mTLS + workload-identity | FS-INT-EQMS-01, FS-XINT-EQMS-01..02 |
| Atlas Serialization | REST | inbound | `atlas.vega-prod.local/v1/sales-volume` | mTLS | FS-INT-SER-01 |
| EUDAMED (six modules) | REST | bidirectional | EUDAMED OAuth2 client-credentials | OAuth2 | FS-INT-EUDAMED-01, FS-EUDAMED-MOD-01..06 |
| BfArM gateway | REST | outbound | `bfarm.vega-prod.local/v1/` | mTLS | FS-INT-BFARM-01 |
| Swissmedic gateway | REST | outbound | `swissmedic.vega-prod.local/v1/` | mTLS | FS-INT-SWISS-01 |
| AGES gateway | REST | outbound | `ages.vega-prod.local/v1/` | mTLS | FS-INT-AGES-01 |
| Literature feed (Embase / PubMed) | REST | inbound | `literature.vega-prod.local/v1/` | OAuth2 | FS-INT-LIT-01 |
| Patient intake | Secure web form + Zendesk | inbound | `intake.vegadevices.de/patient` | TLS 1.3 + GDPR consent | FS-INT-PAT-01 |
| HCP intake | HCP portal + email | inbound | `hcp.vegadevices.de` + `vigilance-hcp@vegadevices.de` | TLS 1.3 + HCP-credentialed | FS-INT-HCP-01 |
| Distributor intake | REST | inbound | `dist.vegadevices.de/v1/` | mTLS | FS-INT-DIST-01 |
| Theia AE DB handover | REST + webhook | bidirectional | `theia.vega-prod.local/ae/` | mTLS + workload-identity | FS-XINT-AE-01..02 |

---

## 4. Configuration Specification

### 4.1 Tenancy + SSO + Vendor-Assurance Configuration

| CI-ID | Configuration item (Sparta-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PMS-01 | TrackWise IdP Mode | `Okta SAML 2.0 + MFA via Entra ID` | Custom | Per FS-PART11-02 + FS-XSYS-AD-01. | FS-PART11-02, FS-XSYS-AD-01 | OQ-AUTHN-01 |
| DS-PMS-02 | Service-Account Auth | `mTLS only` | Custom | Per FS-PART11-02. | FS-PART11-02 | OQ-SA-01 |
| DS-PMS-03 | Conditional-Access Policy | `PMS-Sensitive Conditional Access (FIDO2 phishing-resistant MFA)` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-CA-01 |
| DS-PMS-04 | SIEM Forwarding | `Splunk gxp-authn syslog RFC 5424; lag ≤ 5 min` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-SIEM-01 |
| DS-PMS-05 | PAM Break-Glass | `CyberArk PAM — 24 h rotation + dual-witness` | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | OQ-PAM-01 |
| DS-PMS-06 | Force-Reauth on Sign | `Max-age 5 min OAuth2 token; cached creds rejected` | Custom | Per FS-PART11-07. | FS-PART11-07 | OQ-PART11-200 |
| DS-PMS-07 | Vendor-Assurance Pack | `SOC 2 Type II + ISO 27001 + ISO 13485` | Custom | Per FS-VND-01. | FS-VND-01 | IQ-VND-01 |
| DS-PMS-08 | Vendor Release-Note Review | `Automated alert; 14-day impact assessment` | Custom | Per FS-VND-02. | FS-VND-02 | OQ-VND-01 |

### 4.2 Per-Device Configuration + PMS Plan

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PMS-09 | Per-Device Configuration Lifecycle | `DEV → QC → UAT → PRODUCTION; SoD-enforced (Author ≠ Approver)` | Custom | Per FS-CFG-01. | FS-CFG-01 | OQ-BUILD-01 |
| DS-PMS-10 | CTIS-Compatible Build Pack | `Exporter per EU MDR Art. 25 (for EU trials referencing this PMS DB)` | Custom | Per FS-CFG-02. | FS-CFG-02 | OQ-CTIS-01 |
| DS-PMS-11 | Configuration Export Endpoint | `GET /config/export?device_id=... — version-stamped JSON` | Custom | Per FS-CFG-03. | FS-CFG-03 | OQ-CFG-01 |
| DS-PMS-12 | PMS Plan Template | `Per Annex III; review-cadence rules: Class III + implantables ≥ annual; Class IIa/b per Annex III; Class I ≥ 5 y` | Custom | Per FS-PLAN-01. | FS-PLAN-01 | OQ-PLAN-01 |
| DS-PMS-13 | PMS Execution Evidence | `Captured; PMS-plan-deviation auto-creates MasterControl deviation via API` | Custom | Per FS-PLAN-02. | FS-PLAN-02 | OQ-PLAN-02 |
| DS-PMS-14 | PMS Plan ↔ Technical Documentation Link | `Annex II; change-control gate for updates` | Custom | Per FS-PLAN-03. | FS-PLAN-03 | OQ-PLAN-03 |
| DS-PMS-15 | PMS-Plan Authoring UI | `Annex III template; section-binding validator enforces completeness before approval` | Custom | Per FS-PLAN-AUTH-01. | FS-PLAN-AUTH-01 | OQ-PLAN-AUTH-01 |
| DS-PMS-16 | PMS-Plan-Cycle Execution Tracker | `cycle_id, cycle_start, milestones, cycle_end, deviations — visible in dashboard` | Custom | Per FS-PLAN-AUTH-02. | FS-PLAN-AUTH-02 | OQ-PLAN-AUTH-02 |
| DS-PMS-17 | PMS-Plan Dependency Graph | `Links to PMCF protocol + literature-search strategy + registry-pull frequency lifecycle artefacts` | Custom | Per FS-PLAN-AUTH-03. | FS-PLAN-AUTH-03 | OQ-PLAN-AUTH-03 |
| DS-PMS-18 | PMS Plan Approval | `Director PMS + PRRC + VP QA via SoD-enforced workflow; modifications re-enter approval` | Custom | Per FS-PLAN-AUTH-04. | FS-PLAN-AUTH-04 | OQ-PLAN-AUTH-04 |

### 4.3 PSUR / PSMR Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PMS-19 | PSUR Template | `Per EU MDR Article 86 + MDCG 2022-21; auto-population from PMS data + complaints + literature + Atlas sales volumes` | Custom | Per FS-PSUR-01. | FS-PSUR-01 | OQ-PSUR-01 |
| DS-PMS-20 | Class I PSMR Template | `Per Art. 85; reduced-content` | Custom | Per FS-PSUR-02. | FS-PSUR-02 | OQ-PSUR-02 |
| DS-PMS-21 | PRRC Signature for PSUR | `Re-authenticated e-signature; delegation API endpoint disabled at signature time` | Custom | Per FS-PSUR-03. | FS-PSUR-03 | OQ-PSUR-03 |
| DS-PMS-22 | EUDAMED PSUR Submission via Art. 92 | `Cadence engine per Art. 86(1): IIb + III + implantables annual; IIa biennial; Class I PMSR per Art. 85 (routed to PSMR generator). NB assessment loop enabled for Class III + implantables` | Custom | Per FS-PSUR-04. | FS-PSUR-04 | OQ-PSUR-04 |
| DS-PMS-23 | PSUR Draft Export Format | `PDF/A-3 with embedded XML` | Custom | Per FS-PSUR-05. | FS-PSUR-05 | OQ-PSUR-05 |

### 4.4 Trending + Signal Management Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PMS-24 | Trending Method | `Per device-class — Poisson rate-change, CUSUM, EWMA per ISO 14971:2019` | Custom | Per FS-TRD-01. | FS-TRD-01 | OQ-TRD-01 |
| DS-PMS-25 | Article 88 Trend Report Generator | `On statistically-significant rate change → generate Art. 88 report → route to relevant national CA via gateway` | Custom | Per FS-TRD-02. | FS-TRD-02 | OQ-TRD-02 |
| DS-PMS-26 | Signal-Management State Machine | `confirm → investigate → disposition → CAPA / FSCA (DB-enforced)` | Custom | Per FS-SIG-01. | FS-SIG-01 | OQ-SIG-01 |
| DS-PMS-27 | Signal Closure Policy | `Evidence-backed disposition; auto-close on timeout disabled by default` | Custom | Per FS-SIG-02. | FS-SIG-02 | OQ-SIG-02 |

### 4.5 PMCF Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PMS-28 | PMCF Commitment Table | `Due-dates; CTMS integration via API for clinical-study linkage` | Custom | Per FS-PMCF-01. | FS-PMCF-01 | OQ-PMCF-01 |
| DS-PMS-29 | PMCF Results Feed | `Into PSUR / PSMR auto-population` | Custom | Per FS-PMCF-02. | FS-PMCF-02 | OQ-PMCF-02 |

### 4.6 Incident + FSCA Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PMS-30 | Theia eMDR Cross-Reference | `Bidirectional `incident_id` foreign key` | Custom | Per FS-INC-01 + FS-INT-EMDR-01. | FS-INC-01, FS-INT-EMDR-01 | OQ-EMDR-01 |
| DS-PMS-31 | Serious-Incident Timeline Engine | `15-day standard, 10-day public-health-threat, 2-day death; pre-deadline alerts at D-3 / D-1 / D-0` | Custom | Per FS-INC-02. | FS-INC-02 | OQ-INC-01 |
| DS-PMS-32 | Class-Change Watcher | `Non-serious → serious re-triggers reporting clocks; audit-logged` | Custom | Per FS-INC-03. | FS-INC-03 | OQ-INC-02 |
| DS-PMS-33 | National CA Routing | `DE → BfArM gateway, CH → Swissmedic gateway, AT → AGES gateway; plus EUDAMED vigilance for EU-wide events` | Custom | Per FS-INC-04. | FS-INC-04 | OQ-INC-03 |
| DS-PMS-34 | FSCA Decision Record Schema | `rationale, scope, communication plan, CA notifications; PRRC sign-off required` | Custom | Per FS-FSCA-01. | FS-FSCA-01 | OQ-FSCA-01 |
| DS-PMS-35 | FSN Generator | `Per MDCG-prescribed Art. 89 template` | Custom | Per FS-FSCA-02. | FS-FSCA-02 | OQ-FSCA-02 |
| DS-PMS-36 | FSCA Effectiveness Tracker | `Post-action quantitative metric where feasible` | Custom | Per FS-FSCA-03. | FS-FSCA-03 | OQ-FSCA-03 |

### 4.7 Audit Trail + Part 11 + ALCOA+ Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PMS-37 | Audit-Trail Schema | `actor, action, old/new value, reason, timestamp_iso8601 — all PMS / PSUR / signal / FSCA events` | Custom | Per FS-AUD-01. | FS-AUD-01, FS-PART11-03 | OQ-AUDIT-01 |
| DS-PMS-38 | Append-Only DB Constraint | `Tenant-admin role cannot UPDATE / DELETE` | Custom | Per FS-AUD-02. | FS-AUD-02 | OQ-AUDIT-02 |
| DS-PMS-39 | Retention | `10 y / 15 y implantables — enforced at archive tier` | Custom | Per FS-AUD-03. | FS-AUD-03 | OQ-AUDIT-03 |
| DS-PMS-40 | Audit-Trail Review Cadence | `Weekly System Owner + annual QA (saved-search + signed report)` | Custom | Per FS-AUD-04. | FS-AUD-04 | OQ-AUDIT-04 |
| DS-PMS-41 | § 11.10(a) Procedural Controls | `/sop/ reviewed annually` | Custom | Per FS-PART11-01. | FS-PART11-01 | OQ-PART11-10a |
| DS-PMS-42 | § 11.10(d) Access Control | `Okta SAML 2.0 + MFA; service accounts mTLS only` | Custom | Per FS-PART11-02. | FS-PART11-02 | OQ-PART11-10d |
| DS-PMS-43 | § 11.10(e) Audit Trail | `Per DS-PMS-37` | Custom | Per FS-PART11-03. | FS-PART11-03 | OQ-PART11-10e |
| DS-PMS-44 | § 11.50 Manifestation | `Printed name + date/time + meaning (DB schema-enforced)` | Custom | Per FS-PART11-04. | FS-PART11-04 | OQ-PART11-50 |
| DS-PMS-45 | § 11.70 Binding | `HMAC-SHA256 over record-hash + signer-id + timestamp; tamper detected on read` | Custom | Per FS-PART11-05. | FS-PART11-05 | OQ-PART11-70 |
| DS-PMS-46 | § 11.100 Unique Signature | `Okta-DB uniqueness constraint; no reuse / reassignment` | Custom | Per FS-PART11-06. | FS-PART11-06 | OQ-PART11-100 |
| DS-PMS-47 | § 11.200 Re-Auth at Sign | `Per DS-PMS-06 (fresh OAuth2 token max-age 5 min)` | Custom | Per FS-PART11-07. | FS-PART11-07 | OQ-PART11-200 |
| DS-PMS-48 | ALCOA+ Attributable | `actor_id not-null DB constraint` | Custom | Per FS-DI-01. | FS-DI-01 | OQ-DI-01 |
| DS-PMS-49 | ALCOA+ Legible | `PDF/A-3 + JSON/XML exports; OQ-verified` | Custom | Per FS-DI-02. | FS-DI-02 | OQ-DI-02 |
| DS-PMS-50 | ALCOA+ Contemporaneous | `NTP-synced server-side timestamps; retroactive flagged with delay reason` | Custom | Per FS-DI-03. | FS-DI-03 | OQ-DI-03 |
| DS-PMS-51 | ALCOA+ Original | `Raw inputs in immutable storage; derivatives reference but don't overwrite` | Custom | Per FS-DI-04. | FS-DI-04 | OQ-DI-04 |
| DS-PMS-52 | ALCOA+ Accurate | `Deterministic calculations; floating-point reproducibility OQ-verified` | Custom | Per FS-DI-05. | FS-DI-05 | OQ-DI-05 |
| DS-PMS-53 | ALCOA+ Retrievability | `≤ 1 BD routine; metadata completeness validated` | Custom | Per FS-DI-06. | FS-DI-06 | OQ-DI-06 |

### 4.8 Integration Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PMS-54 | Theia eMDR Integration | `Bidirectional JSON over mTLS; `theia.vega-prod.local/v1/incidents/`` | Custom | Per FS-INT-EMDR-01. | FS-INT-EMDR-01 | OQ-EMDR-01 |
| DS-PMS-55 | MasterControl CAPA Endpoint | `POST mc.vega-prod.local/v1/capa/tickets` | Custom | Per FS-INT-EQMS-01 + FS-XINT-EQMS-01. | FS-INT-EQMS-01, FS-XINT-EQMS-01 | OQ-CAPA-01 |
| DS-PMS-56 | MasterControl CAPA Status Webhook | `Payload `eqms.status.v1`; consumer maps status onto disposition fields; closed-loop gate prevents disposition without `eqms_status=CLOSED`` | Custom | Per FS-XINT-EQMS-02. | FS-XINT-EQMS-02 | OQ-CAPA-02 |
| DS-PMS-57 | Atlas Sales-Volume API | ``atlas.vega-prod.local/v1/sales-volume` for denominator in Art. 88 trending` | Custom | Per FS-INT-SER-01. | FS-INT-SER-01 | OQ-ATLAS-01 |
| DS-PMS-58 | EUDAMED Integration | `PSUR + vigilance module REST APIs via OAuth2 client-credentials` | Custom | Per FS-INT-EUDAMED-01. | FS-INT-EUDAMED-01 | OQ-EUDAMED-01 |
| DS-PMS-59 | EUDAMED Actor Module | `Nightly sync of manufacturer / AR / importer / SPP-producer registration` | Custom | Per FS-EUDAMED-MOD-01. | FS-EUDAMED-MOD-01 | OQ-EUDAMED-02 |
| DS-PMS-60 | EUDAMED UDI / Device Module | `UDI-DI / UDI-PI / Basic UDI-DI tracking; Art. 29 submission` | Custom | Per FS-EUDAMED-MOD-02. | FS-EUDAMED-MOD-02 | OQ-EUDAMED-03 |
| DS-PMS-61 | EUDAMED Certificate Module | `Expiry alerts at 90 / 60 / 30 / 7 days` | Custom | Per FS-EUDAMED-MOD-03. | FS-EUDAMED-MOD-03 | OQ-EUDAMED-04 |
| DS-PMS-62 | EUDAMED Vigilance Module | `Serious-incident + Art. 88 trend + FSCA routed via REST` | Custom | Per FS-EUDAMED-MOD-04. | FS-EUDAMED-MOD-04 | OQ-EUDAMED-05 |
| DS-PMS-63 | EUDAMED Market Surveillance Module | `CA-driven investigations tracked with case-id linkage` | Custom | Per FS-EUDAMED-MOD-05. | FS-EUDAMED-MOD-05 | OQ-EUDAMED-06 |
| DS-PMS-64 | EUDAMED Clinical Investigation + PMCF Module | `PMCF studies registered + Art. 74 status updates` | Custom | Per FS-EUDAMED-MOD-06. | FS-EUDAMED-MOD-06 | OQ-EUDAMED-07 |
| DS-PMS-65 | BfArM Gateway | `mTLS; MPDG-compliant submission interface; manual fallback documented` | Custom | Per FS-INT-BFARM-01. | FS-INT-BFARM-01 | OQ-BFARM-01 |
| DS-PMS-66 | Swissmedic Gateway | `mTLS; MepV-compliant; manual fallback documented` | Custom | Per FS-INT-SWISS-01. | FS-INT-SWISS-01 | OQ-SWISS-01 |
| DS-PMS-67 | AGES Gateway | `mTLS; manual fallback documented` | Custom | Per FS-INT-AGES-01. | FS-INT-AGES-01 | OQ-AGES-01 |
| DS-PMS-68 | Literature Feed | `Embase / PubMed via vendor service; daily ingestion with deduplication` | Custom | Per FS-INT-LIT-01. | FS-INT-LIT-01 | OQ-LIT-01 |
| DS-PMS-69 | Theia AE DB Vigilance-Signal Publisher | `POST theia.vega-prod.local/ae/signals — mTLS + workload-identity; payload `theia.ae.v1`; idempotency on `{device_udi, signal_class, detection_window_id}`; at-least-once; DLQ at 10 attempts` | Custom | Per FS-XINT-AE-01. | FS-XINT-AE-01 | OQ-AE-01 |
| DS-PMS-70 | Theia AE FSCA Callback Webhook | `Payload `theia.fsca.callback.v1`; consumer maps callback onto PMS plan state + PSUR-evidence binder; per-device hyperlink to AE FSCA case persisted` | Custom | Per FS-XINT-AE-02. | FS-XINT-AE-02 | OQ-AE-02 |
| DS-PMS-71 | Backup Integration | `Veeam + PostgreSQL pg_basebackup + continuous WAL; T1; RPO ≤ 4 h; RTO ≤ 4 BH; S3 Object Lock Compliance + LTO-9 monthly` | Custom | Per FS-XSYS-BAK-01 + FS-BAK-01..02. | FS-XSYS-BAK-01, FS-BAK-01 | OQ-BAK-01 |

### 4.9 Performance + Availability + Security Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PMS-72 | UI P95 Target | `≤ 3 s for PMS Specialist workflows; Grafana SLO` | Custom | Per FS-PERF-01. | FS-PERF-01 | PQ-PERF-01 |
| DS-PMS-73 | Sparta SLA | `≥ 99.5%/month` | Default | Per FS-AV-01. | FS-AV-01 | OQ-AV-01 |
| DS-PMS-74 | Site Tenant-Data Export | `Quarterly; 10 y retention in cold storage` | Custom | Per FS-BAK-01. | FS-BAK-01 | OQ-BAK-02 |
| DS-PMS-75 | Vendor RTO / RPO | `RTO ≤ 24 h / RPO ≤ 4 h verified annually` | Custom | Per FS-BAK-02. | FS-BAK-02 | OQ-BAK-03 |
| DS-PMS-76 | TLS / AES Stance | `TLS 1.3 in transit + AES-256 at rest (vendor-confirmed)` | Custom | Per FS-SEC-01. | FS-SEC-01 | OQ-SEC-01 |
| DS-PMS-77 | RBAC Review Cadence | `Quarterly; PRRC role assignment requires Reg-Affairs approval` | Custom | Per FS-SEC-02. | FS-SEC-02 | OQ-SEC-02 |
| DS-PMS-78 | Annual Pen-Test | `H/C findings remediated within 60 days under change control` | Custom | Per FS-SEC-03. | FS-SEC-03 | OQ-SEC-03 |

### 4.10 Training + Periodic Review Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PMS-79 | LMS Training Gate | `Role-specific; PRRC training mandatory before role-grant` | Custom | Per FS-TRN-01. | FS-TRN-01 | OQ-TRN-01 |
| DS-PMS-80 | Annual Refresher | `MDR-2026-ANNUAL — EU MDR + MDCG + FSCA + national CA changes` | Custom | Per FS-TRN-02. | FS-TRN-02 | OQ-TRN-02 |
| DS-PMS-81 | Annual Periodic Review | `Vendor qualification + config drift + audit-trail review + PMS-plan adherence + PMCF status + signal metrics + integration health + training; signed by Director PMS + PRRC + VP QA + VP Reg Affairs` | Custom | Per FS-PR-01. | FS-PR-01 | OQ-PR-01 |

### 4.11 Dashboard + Benefit-Risk + HA Correspondence + Notified Body Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PMS-82 | Real-Time PMS Dashboard | `Grafana `pms-dash-api` — per-device rolling-90-day complaint rate + serious-incident count + Art. 88 CUSUM/EWMA + PMCF commitment status + PMS-plan cycle status; refresh latency P95 ≤ 15 min; SLO `dashboard_freshness_seconds`` | Custom | Per FS-DASH-01. | FS-DASH-01 | OQ-DASH-01 |
| DS-PMS-83 | Per-Device Drill-Down Panels | `Triage breakdown + reporting-clock margin distribution + NB-required-item status table` | Custom | Per FS-DASH-02. | FS-DASH-02 | OQ-DASH-02 |
| DS-PMS-84 | Dashboard Export Format | `PNG / PDF / CSV with data-cut timestamp + dataset SHA-256 checksum in footer` | Custom | Per FS-DASH-03. | FS-DASH-03 | OQ-DASH-03 |
| DS-PMS-85 | KPI-Threshold Engine | `pms-threshold.yaml configurable per device; breach → Slack `#pms-alerts` + PagerDuty `pms-oncall` (Director PMS + PRRC)` | Custom | Per FS-DASH-04. | FS-DASH-04 | OQ-DASH-04 |
| DS-PMS-86 | Benefit-Risk Profile Module | `Per ISO 14971:2019 § 10; hazard-source links to PMS data; PSUR Section 6 auto-extraction` | Custom | Per FS-BR-01. | FS-BR-01 | OQ-BR-01 |
| DS-PMS-87 | PSUR-Risk Matrix Data Model | `hazard ↔ control-measure ↔ residual-risk ↔ post-market-evidence ↔ action; PSUR generator queries at build time` | Custom | Per FS-BR-02. | FS-BR-02 | OQ-BR-02 |
| DS-PMS-88 | Risk-Control-Effectiveness Tracker | `PMS-derived incident-rate per control; threshold breach raises change-flag per ISO 14971:2019 § 10.3` | Custom | Per FS-BR-03. | FS-BR-03 | OQ-BR-03 |
| DS-PMS-89 | RMF Bidirectional Link via UDI-DI | `RMF update triggered by signal-closure + FSCA events` | Custom | Per FS-BR-04 + FS-RM-01. | FS-BR-04, FS-RM-01 | OQ-RM-01 |
| DS-PMS-90 | HA Correspondence Register | `hac_correspondence schema: sender, recipient, due-date, response-due-date, status; covers CA queries + Notified-Body queries + PSUR feedback + FSCA ack` | Custom | Per FS-HAC-01. | FS-HAC-01 | OQ-HAC-01 |
| DS-PMS-91 | CA-Query Response Workflow | `Drafter → reviewer → PRRC approver SoD-enforced; response export in PDF/A-3` | Custom | Per FS-HAC-02. | FS-HAC-02 | OQ-HAC-02 |
| DS-PMS-92 | Inspection-Readiness Export | `PMS plan + PSURs + PMS reports + FSCAs + complaint summary + training records + audit-trail extracts; one-click dossier; ≤ 4 h` | Custom | Per FS-HAC-03. | FS-HAC-03 | OQ-HAC-03 |
| DS-PMS-93 | Mock-Audit Rehearsal | `Workflow with structured findings register` | Custom | Per FS-HAC-04. | FS-HAC-04 | OQ-HAC-04 |
| DS-PMS-94 | Notified-Body Correspondence Tagging | `nb_id (e.g., CE-0123-TUVSUD); audit-visible filter` | Custom | Per FS-HAC-05. | FS-HAC-05 | OQ-HAC-05 |
| DS-PMS-95 | Notified-Body Designation Register | `Per device per market — TÜV SÜD CE 0123 (EU); UK-Approved-Body (UKCA); CH-REP (Swiss); ANVISA holder (BR); certificate-expiry alerts at 90/60/30/7 days` | Custom | Per FS-NB-01. | FS-NB-01 | OQ-NB-01 |
| DS-PMS-96 | NB PSUR-Assessment Tracker | `Per Art. 86(2) — assessment-due-date + outcome captured; missed-assessment alert` | Custom | Per FS-NB-02. | FS-NB-02 | OQ-NB-02 |
| DS-PMS-97 | Authorised-Representative Register | `Per market — EU AR (Art. 11), CH-REP (MepV), UK Responsible Person, SG Importer, BR ANVISA holder; per-device-per-market binding` | Custom | Per FS-NB-03. | FS-NB-03 | OQ-NB-03 |
| DS-PMS-98 | Certificate-Transition Workflow | `MDD → MDR with milestones + evidence checklist` | Custom | Per FS-NB-04. | FS-NB-04 | OQ-NB-04 |

### 4.12 Patient / HCP / Distributor Intake + Data Quality Configuration

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PMS-99 | Patient-Direct Intake | `Secure web form `/intake/patient` + Zendesk phone-ticket integration; GDPR consent + contact + device + complaint description` | Custom | Per FS-INT-PAT-01. | FS-INT-PAT-01 | OQ-INTAKE-01 |
| DS-PMS-100 | HCP Intake | `HCP portal `hcp.vegadevices.de` + email-gateway parser `vigilance-hcp@vegadevices.de`; HCP-role / qualification captured` | Custom | Per FS-INT-HCP-01. | FS-INT-HCP-01 | OQ-INTAKE-02 |
| DS-PMS-101 | Distributor / Importer Intake | `Per EU MDR Arts. 14, 16; chain-of-custody fields captured` | Custom | Per FS-INT-DIST-01. | FS-INT-DIST-01 | OQ-INTAKE-03 |
| DS-PMS-102 | Complaint-Deduplication Rule Engine | `UDI-DI + complainant identifiers + event-date proximity; suspected-duplicates → Vigilance Specialist queue` | Custom | Per FS-INT-DEDUP-01. | FS-INT-DEDUP-01 | OQ-DEDUP-01 |
| DS-PMS-103 | Mandatory-Field Validator | `Per EU MDR Art. 87 Annex; blocks state transition on incomplete; runs on every transition` | Custom | Per FS-DQ-01. | FS-DQ-01 | OQ-DQ-01 |
| DS-PMS-104 | Field-Content Validator | `ISO 3166-1 country codes + IMDRF UDI-DI format + ISO 8601 dates; field-specific rejection messages` | Custom | Per FS-DQ-02. | FS-DQ-02 | OQ-DQ-02 |
| DS-PMS-105 | Data-Quality KPI Report | `Monthly — % missing optional fields + % corrected fields` | Custom | Per FS-DQ-03. | FS-DQ-03 | OQ-DQ-03 |

### 4.13 Risk Management Configuration (ISO 14971:2019)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PMS-106 | RMF Bidirectional Link via UDI-DI | `PMS data ↔ RMF hazards` | Custom | Per FS-RM-01. | FS-RM-01 | OQ-RM-02 |
| DS-PMS-107 | ISO 14971:2019 § 10 Workflow | `§ 10.1 information collection + § 10.2 review + § 10.3 actions` | Custom | Per FS-RM-02. | FS-RM-02 | OQ-RM-03 |
| DS-PMS-108 | New-Hazard CR | `Raises RMF-update CR; tracked to closure` | Custom | Per FS-RM-03. | FS-RM-03 | OQ-RM-04 |
| DS-PMS-109 | RM Plan Template | `References PMS data-collection methods + residual-risk acceptance per ISO/TR 24971:2020` | Custom | Per FS-RM-04. | FS-RM-04 | OQ-RM-05 |
| DS-PMS-110 | Risk-Management Review Cadence | `Configured; PMS metrics surfaced as primary input` | Custom | Per FS-RM-05. | FS-RM-05 | OQ-RM-06 |
| DS-PMS-111 | Hazard-to-Event Traceability | `Each PMS event ↔ {0, 1+} known hazards; new-hazard event audit-trailed` | Custom | Per FS-RM-06. | FS-RM-06 | OQ-RM-07 |

---

## 5. Workflow + Business-Rule Design

### 5.1 Serious-Incident → FSCA Routing Workflow

```
   [Incident received (eMDR / Patient / HCP / Distributor intake)]
         │
         ▼ Dedup check (DS-PMS-102)
   [Triage — class determination per EU MDR Art. 87]
         │
         ▼ Serious? Yes →
   [Serious-Incident Timeline Engine (DS-PMS-31):
        - 2-day for death (Art. 87(3))
        - 10-day for public-health threat (Art. 87(2))
        - 15-day standard (Art. 87(1))
    Pre-deadline alerts: D-3 / D-1 / D-0]
         │
         ▼ National CA routing (DS-PMS-33)
   ┌────────────────────────────────────────────────────────────┐
   │  DE → BfArM gateway (DS-PMS-65)                             │
   │  CH → Swissmedic gateway (DS-PMS-66)                        │
   │  AT → AGES gateway (DS-PMS-67)                              │
   │  + EUDAMED Vigilance module for EU-wide events (DS-PMS-62)  │
   └────────────────────────────────────────────────────────────┘
         │
         ▼ Class change watcher (DS-PMS-32) re-triggers clocks if status escalates
   [Signal-management state machine: confirm → investigate → disposition → CAPA / FSCA (DS-PMS-26)]
         │
         ▼ Closure requires evidence-backed disposition (DS-PMS-27)
   [FSCA Decision (DS-PMS-34) — PRRC sign-off required]
         │
         ▼ FSN generated per MDCG Art. 89 template (DS-PMS-35)
   [FSCA Effectiveness Tracker (DS-PMS-36) — post-action quantitative metric]
```

### 5.2 PSUR Generation Workflow

```
   [PSUR cadence reached (per Art. 86 — DS-PMS-22):
        - Class IIb + III + implantables: annual
        - Class IIa: biennial
        - Class I: PMSR per Art. 85 routed to PSMR generator (DS-PMS-20)]
         │
         ▼ PSUR template (DS-PMS-19) auto-populates from:
   ┌──────────────────────────────────────────────────────────────┐
   │  PMS data (DS-PMS-12..17)                                     │
   │  Complaints (DS-PMS-99..101 intake + DS-PMS-102 dedup)        │
   │  Literature (DS-PMS-68)                                       │
   │  Atlas sales volumes (DS-PMS-57)                              │
   │  PMCF results (DS-PMS-29)                                     │
   │  PSUR-Risk Matrix (DS-PMS-87)                                 │
   └──────────────────────────────────────────────────────────────┘
         │
         ▼ Draft reviewed by Vigilance Manager + PRRC
   [PRRC re-authenticated e-signature (DS-PMS-21) — delegation disabled at sign moment]
         │
         ▼ EUDAMED Art. 92 submission (DS-PMS-22)
   [PSUR exported in PDF/A-3 with embedded XML (DS-PMS-23)]
         │
         ▼ Notified-Body assessment loop for Class III + implantables (DS-PMS-96)
```

### 5.3 Article 88 Trend Reporting Workflow

```
   [Daily trending job runs Poisson / CUSUM / EWMA per device-class (DS-PMS-24)]
         │
         ▼ Atlas denominator pulled (DS-PMS-57)
   [Statistical significance test]
         │
         ▼ Significant rate change detected?
   [Yes → Article 88 trend report generated (DS-PMS-25)]
         │
         ▼ National CA routing per DS-PMS-33
   [Routed to relevant national CA via gateway (DS-PMS-65..67)]
         │
         ▼ EUDAMED Vigilance module logged (DS-PMS-62)
```

### 5.4 Complaint Intake → Dedup → Triage Workflow

```
   [Patient (DS-PMS-99) | HCP (DS-PMS-100) | Distributor (DS-PMS-101) intake]
         │
         ▼ Data Quality validators (DS-PMS-103..104) — mandatory + content
   [Complaint record created]
         │
         ▼ Dedup engine (DS-PMS-102) — UDI-DI + complainant + event-date proximity
   ┌──────────────────────────────────────────────────────────┐
   │  Suspected-duplicates → Vigilance Specialist queue       │
   │  Unique → Triage workflow                                 │
   └──────────────────────────────────────────────────────────┘
         │
         ▼ Triage → Signal management state machine (DS-PMS-26)
   [Linked to Theia eMDR `incident_id` (DS-PMS-30)]
         │
         ▼ If becomes signal → DS-PMS-69 vigilance-signal publisher to Theia AE DB
   [If FSCA-bearing → DS-PMS-70 FSCA callback updates PMS plan state + PSUR-evidence binder]
```

### 5.5 Risk Management Review Workflow (ISO 14971:2019)

```
   [Periodic Risk-Management Review meeting cadence (DS-PMS-110)]
         │
         ▼ Input: PMS metrics, signal closures, FSCAs, NB feedback
   [§ 10.1 Information collection (DS-PMS-107)]
         │
         ▼
   [§ 10.2 Review]
         │
         ▼ New hazard identified?
   [§ 10.3 Actions: New-hazard CR (DS-PMS-108) → RMF update]
         │
         ▼ Hazard-to-event traceability updated (DS-PMS-111)
   [Risk-Control-Effectiveness Tracker (DS-PMS-88) updated; threshold breach raises change-flag]
```

---

## 6. Role-Permission Matrix Design

| Role | Complaint Intake | Triage | Signal Confirm | Disposition | CAPA Open | FSCA Decision | FSCA Sign-Off | PSUR Draft | PSUR Sign | EUDAMED Submit | RMF Update | View Dashboard | Tenant Admin |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Patient (intake only) | ✓ (own) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| HCP (intake only) | ✓ (HCP-cred) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Distributor / Importer (intake only) | ✓ (with chain-of-custody) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Vigilance Specialist | ✓ | ✓ | ✓ | ✓ | ✓ | (drafts) | ✗ | (drafts) | ✗ | ✗ | ✗ | ✓ | ✗ |
| Vigilance Manager | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✗ | ✓ | ✗ | ✗ | ✗ | ✓ | ✗ |
| PRRC (EU MDR Art. 15) | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (sign) | ✓ (FSN sign) | ✗ | ✓ (re-auth, non-delegatable) | ✓ | ✗ | ✓ | ✗ |
| Director PMS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✗ | ✓ | ✗ | ✗ | ✗ | ✓ | ✗ |
| Clinical Affairs / PMCF Lead | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | (PMCF section) | ✗ | ✗ | ✗ | ✓ | ✗ |
| Risk Manager | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✓ | ✗ |
| VP Regulatory Affairs | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ |
| VP QA | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ |
| Notified Body Auditor | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (NB-scoped) | ✗ |
| CA Inspector (BfArM / Swissmedic / AGES) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (read-only) | ✗ |
| Tenant Admin (Sparta) | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ (config only) |

**Role-permission design rules:**
- **PRRC signature is non-delegatable** for PSUR (DS-PMS-21) — the delegation API endpoint is disabled at signature time.
- **SoD enforced** — author of CA-query response ≠ reviewer ≠ approver (DS-PMS-91).
- **Tenant Admin** excludes audit-trail UPDATE / DELETE (DS-PMS-38).

---

## 7. Integration Design

(See § 4.8 for per-integration CIs.) Summary table:

| Counterparty | Direction | Endpoint | Auth | FS-ID |
|---|---|---|---|---|
| Theia eMDR | bidirectional | `theia.vega-prod.local/v1/incidents/` | mTLS | FS-INT-EMDR-01 |
| MasterControl eQMS CAPA | bidirectional | `mc.vega-prod.local/v1/capa/tickets` + webhook | mTLS + workload-identity | FS-INT-EQMS-01, FS-XINT-EQMS-01..02 |
| Atlas Serialization | inbound | `atlas.vega-prod.local/v1/sales-volume` | mTLS | FS-INT-SER-01 |
| EUDAMED (six modules) | bidirectional | EUDAMED OAuth2 | OAuth2 | FS-INT-EUDAMED-01 + FS-EUDAMED-MOD-01..06 |
| BfArM | outbound | `bfarm.vega-prod.local/v1/` | mTLS | FS-INT-BFARM-01 |
| Swissmedic | outbound | `swissmedic.vega-prod.local/v1/` | mTLS | FS-INT-SWISS-01 |
| AGES | outbound | `ages.vega-prod.local/v1/` | mTLS | FS-INT-AGES-01 |
| Literature feed | inbound | `literature.vega-prod.local/v1/` | OAuth2 | FS-INT-LIT-01 |
| Patient intake web | inbound | `intake.vegadevices.de/patient` | TLS 1.3 + GDPR consent | FS-INT-PAT-01 |
| HCP intake portal | inbound | `hcp.vegadevices.de` | TLS 1.3 + HCP-credentialed | FS-INT-HCP-01 |
| Distributor intake | inbound | `dist.vegadevices.de/v1/` | mTLS | FS-INT-DIST-01 |
| Theia AE DB handover | bidirectional | `theia.vega-prod.local/ae/signals` + callback | mTLS + workload-identity | FS-XINT-AE-01..02 |
| AUR Backup | (cross-system) | Veeam + PG pg_basebackup + WAL | per AUR | FS-XSYS-BAK-01 |
| AD Identity | (cross-system) | Entra ID SAML + SCIM | per AD | FS-XSYS-AD-01 |

---

## 8. Site-Deployed Components Design

| Component | Type | Source location | Owner team | Verified by |
|---|---|---|---|---|
| `pms-dash-api` | Service (Grafana fronted) | `git.vega-prod.local/pms/pms-dash-api` | PMS Engineering | OQ-DASH-01..04 |
| `psur-generator` | Service | `git.vega-prod.local/pms/psur-generator` | PMS Engineering | OQ-PSUR-01..05 |
| `psmr-generator` | Service (Class I per Art. 85) | `git.vega-prod.local/pms/psmr-generator` | PMS Engineering | OQ-PSUR-02 |
| `art88-trend-engine` | Daemon | `git.vega-prod.local/pms/art88-trend-engine` | PMS Engineering | OQ-TRD-01..02 |
| `art87-timeline-engine` | Daemon | `git.vega-prod.local/pms/art87-timeline-engine` | PMS Engineering | OQ-INC-01..03 |
| `fsca-fsn-generator` | Service | `git.vega-prod.local/pms/fsca-fsn-generator` | PMS Engineering | OQ-FSCA-01..03 |
| `complaint-dedup-engine` | Service | `git.vega-prod.local/pms/complaint-dedup-engine` | PMS Engineering | OQ-DEDUP-01 |
| `dq-validator` | Library | `git.vega-prod.local/pms/dq-validator` | PMS Engineering | OQ-DQ-01..03 |
| `eudamed-publisher` | Service (six modules) | `git.vega-prod.local/pms/eudamed-publisher` | PMS Engineering | OQ-EUDAMED-01..07 |
| `national-ca-router` | Service (BfArM / Swissmedic / AGES) | `git.vega-prod.local/pms/national-ca-router` | PMS Engineering | OQ-BFARM-01 + OQ-SWISS-01 + OQ-AGES-01 |
| `rmf-link-engine` | Service | `git.vega-prod.local/pms/rmf-link-engine` | Risk Engineering | OQ-RM-01..07 |
| `literature-ingest-job` | Scheduled (daily) | `git.vega-prod.local/pms/literature-ingest-job` | PMS Engineering | OQ-LIT-01 |
| `nb-certificate-expiry-watcher` | Daemon | `git.vega-prod.local/pms/nb-certificate-expiry-watcher` | PMS Engineering | OQ-NB-01 + OQ-EUDAMED-04 |
| `inspection-readiness-export` | Service | `git.vega-prod.local/pms/inspection-readiness-export` | PMS Engineering | OQ-HAC-03 |
| `theia-ae-publisher` | Library | `git.vega-prod.local/pms/theia-ae-publisher` | PMS Engineering | OQ-AE-01..02 |
| `eqms-status-consumer` | Daemon | `git.vega-prod.local/pms/eqms-status-consumer` | PMS Engineering | OQ-CAPA-02 |

Each repository carries a `docs/SDS.md` mini-Software-Design-Specification artefact per GAMP 5 2nd-edition § 2B.4 rule 6.

---

## 9. References

### 9.1 US

- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300.
- 21 CFR Part 803 (Medical Device Reporting).
- 21 CFR Part 820 §§ .100, .198 (CAPA + complaint files).
- 21 CFR Part 821 (UDI tracking).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).
- FDA *Marketing Submission Recommendations for a Predetermined Change Control Plan for Artificial Intelligence-Enabled Device Software Functions* (Aug 2025).

### 9.2 EU

- EU MDR Reg. 2017/745 Arts. 10, 11, 14, 15, 16, 83–92.
- MDCG 2019-9, 2022-21, 2023-3.
- EU GMP Annex 11 §§ 4, 6, 9, 11 (where applicable).
- GDPR Reg. (EU) 2016/679 — Arts. 6, 32 (patient intake consent).
- EU AI Act Reg. (EU) 2024/1689 — Annex III where AI/ML-driven trend-detection or signal-management is declared.

### 9.3 DACH

- BfArM (DE) — MPDG (Medizinprodukterecht-Durchführungsgesetz).
- Swissmedic (CH) — MepV (Medizinprodukteverordnung).
- AGES PharmMed (AT).
- UK MHRA — UKCA marking.
- ANVISA (BR).

### 9.4 International

- ISO 14971:2019 — Risk management for medical devices.
- ISO/TR 24971:2020 — Guidance on application of ISO 14971.
- ISO 13485:2016 — Quality management systems for medical devices.
- IMDRF UDI guidance.
- ISPE GAMP 5 (2nd Edition, 2022).
- PIC/S PI 041.
- ISO/IEC 27001:2022.

### 9.5 Vendor

- Sparta — *TrackWise Digital PMS Module Configuration and Administration Reference*.

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS ID | FS ID(s) | Notes |
|---|---|---|
| DS-PMS-01 | FS-PART11-02 / FS-XSYS-AD-01 | TrackWise IdP mode |
| DS-PMS-02 | FS-PART11-02 | Service-account auth |
| DS-PMS-03 | FS-XSYS-AD-01 | Conditional-access |
| DS-PMS-04 | FS-XSYS-AD-01 | SIEM forwarding |
| DS-PMS-05 | FS-XSYS-AD-01 | PAM break-glass |
| DS-PMS-06 | FS-PART11-07 | Force-reauth |
| DS-PMS-07 | FS-VND-01 | Vendor-assurance pack |
| DS-PMS-08 | FS-VND-02 | Vendor release-note review |
| DS-PMS-09 | FS-CFG-01 | Per-device lifecycle |
| DS-PMS-10 | FS-CFG-02 | CTIS-compatible pack |
| DS-PMS-11 | FS-CFG-03 | Config export endpoint |
| DS-PMS-12 | FS-PLAN-01 | PMS plan template |
| DS-PMS-13 | FS-PLAN-02 | Execution evidence |
| DS-PMS-14 | FS-PLAN-03 | TechDoc linkage |
| DS-PMS-15 | FS-PLAN-AUTH-01 | PMS-plan authoring UI |
| DS-PMS-16 | FS-PLAN-AUTH-02 | PMS-plan-cycle tracker |
| DS-PMS-17 | FS-PLAN-AUTH-03 | PMS-plan dependency graph |
| DS-PMS-18 | FS-PLAN-AUTH-04 | PMS plan approval |
| DS-PMS-19 | FS-PSUR-01 | PSUR template |
| DS-PMS-20 | FS-PSUR-02 | PSMR template (Class I) |
| DS-PMS-21 | FS-PSUR-03 | PRRC signature |
| DS-PMS-22 | FS-PSUR-04 | EUDAMED PSUR submission + cadence |
| DS-PMS-23 | FS-PSUR-05 | PSUR export format |
| DS-PMS-24 | FS-TRD-01 | Trending method |
| DS-PMS-25 | FS-TRD-02 | Art. 88 generator |
| DS-PMS-26 | FS-SIG-01 | Signal state machine |
| DS-PMS-27 | FS-SIG-02 | Signal closure policy |
| DS-PMS-28 | FS-PMCF-01 | PMCF commitment table |
| DS-PMS-29 | FS-PMCF-02 | PMCF results feed |
| DS-PMS-30 | FS-INC-01 / FS-INT-EMDR-01 | Theia eMDR cross-ref |
| DS-PMS-31 | FS-INC-02 | Serious-incident timeline |
| DS-PMS-32 | FS-INC-03 | Class-change watcher |
| DS-PMS-33 | FS-INC-04 | National CA routing |
| DS-PMS-34 | FS-FSCA-01 | FSCA decision schema |
| DS-PMS-35 | FS-FSCA-02 | FSN generator |
| DS-PMS-36 | FS-FSCA-03 | FSCA effectiveness tracker |
| DS-PMS-37 | FS-AUD-01 / FS-PART11-03 | Audit-trail schema |
| DS-PMS-38 | FS-AUD-02 | Append-only constraint |
| DS-PMS-39 | FS-AUD-03 | Retention |
| DS-PMS-40 | FS-AUD-04 | Review cadence |
| DS-PMS-41 | FS-PART11-01 | § 11.10(a) |
| DS-PMS-42 | FS-PART11-02 | § 11.10(d) |
| DS-PMS-43 | FS-PART11-03 | § 11.10(e) |
| DS-PMS-44 | FS-PART11-04 | § 11.50 |
| DS-PMS-45 | FS-PART11-05 | § 11.70 |
| DS-PMS-46 | FS-PART11-06 | § 11.100 |
| DS-PMS-47 | FS-PART11-07 | § 11.200 |
| DS-PMS-48 | FS-DI-01 | Attributable |
| DS-PMS-49 | FS-DI-02 | Legible |
| DS-PMS-50 | FS-DI-03 | Contemporaneous |
| DS-PMS-51 | FS-DI-04 | Original |
| DS-PMS-52 | FS-DI-05 | Accurate |
| DS-PMS-53 | FS-DI-06 | Retrievability |
| DS-PMS-54 | FS-INT-EMDR-01 | Theia eMDR integration |
| DS-PMS-55 | FS-INT-EQMS-01 / FS-XINT-EQMS-01 | MasterControl CAPA endpoint |
| DS-PMS-56 | FS-XINT-EQMS-02 | CAPA status webhook |
| DS-PMS-57 | FS-INT-SER-01 | Atlas sales-volume |
| DS-PMS-58 | FS-INT-EUDAMED-01 | EUDAMED integration |
| DS-PMS-59 | FS-EUDAMED-MOD-01 | Actor module |
| DS-PMS-60 | FS-EUDAMED-MOD-02 | UDI / Device module |
| DS-PMS-61 | FS-EUDAMED-MOD-03 | Certificate module |
| DS-PMS-62 | FS-EUDAMED-MOD-04 | Vigilance module |
| DS-PMS-63 | FS-EUDAMED-MOD-05 | Market Surveillance module |
| DS-PMS-64 | FS-EUDAMED-MOD-06 | Clinical Investigation + PMCF module |
| DS-PMS-65 | FS-INT-BFARM-01 | BfArM gateway |
| DS-PMS-66 | FS-INT-SWISS-01 | Swissmedic gateway |
| DS-PMS-67 | FS-INT-AGES-01 | AGES gateway |
| DS-PMS-68 | FS-INT-LIT-01 | Literature feed |
| DS-PMS-69 | FS-XINT-AE-01 | Theia AE vigilance-signal publisher |
| DS-PMS-70 | FS-XINT-AE-02 | Theia AE FSCA callback |
| DS-PMS-71 | FS-XSYS-BAK-01 / FS-BAK-01..02 | Backup |
| DS-PMS-72 | FS-PERF-01 | UI P95 |
| DS-PMS-73 | FS-AV-01 | Sparta SLA |
| DS-PMS-74 | FS-BAK-01 | Tenant export retention |
| DS-PMS-75 | FS-BAK-02 | RTO / RPO |
| DS-PMS-76 | FS-SEC-01 | TLS / AES |
| DS-PMS-77 | FS-SEC-02 | RBAC review |
| DS-PMS-78 | FS-SEC-03 | Pen-test |
| DS-PMS-79 | FS-TRN-01 | LMS training gate |
| DS-PMS-80 | FS-TRN-02 | Annual refresher |
| DS-PMS-81 | FS-PR-01 | Annual periodic review |
| DS-PMS-82 | FS-DASH-01 | Real-time dashboard |
| DS-PMS-83 | FS-DASH-02 | Drill-down panels |
| DS-PMS-84 | FS-DASH-03 | Dashboard export |
| DS-PMS-85 | FS-DASH-04 | KPI-threshold engine |
| DS-PMS-86 | FS-BR-01 | Benefit-Risk profile |
| DS-PMS-87 | FS-BR-02 | PSUR-Risk Matrix |
| DS-PMS-88 | FS-BR-03 | Risk-control-effectiveness tracker |
| DS-PMS-89 | FS-BR-04 / FS-RM-01 | RMF bidirectional link |
| DS-PMS-90 | FS-HAC-01 | HA correspondence register |
| DS-PMS-91 | FS-HAC-02 | CA-query response workflow |
| DS-PMS-92 | FS-HAC-03 | Inspection-readiness export |
| DS-PMS-93 | FS-HAC-04 | Mock-audit rehearsal |
| DS-PMS-94 | FS-HAC-05 | NB correspondence tagging |
| DS-PMS-95 | FS-NB-01 | NB designation register |
| DS-PMS-96 | FS-NB-02 | NB PSUR-assessment tracker |
| DS-PMS-97 | FS-NB-03 | AR register |
| DS-PMS-98 | FS-NB-04 | Certificate-transition workflow |
| DS-PMS-99 | FS-INT-PAT-01 | Patient intake |
| DS-PMS-100 | FS-INT-HCP-01 | HCP intake |
| DS-PMS-101 | FS-INT-DIST-01 | Distributor intake |
| DS-PMS-102 | FS-INT-DEDUP-01 | Dedup engine |
| DS-PMS-103 | FS-DQ-01 | Mandatory-field validator |
| DS-PMS-104 | FS-DQ-02 | Content validator |
| DS-PMS-105 | FS-DQ-03 | DQ KPI report |
| DS-PMS-106 | FS-RM-01 | RMF link |
| DS-PMS-107 | FS-RM-02 | ISO 14971 § 10 workflow |
| DS-PMS-108 | FS-RM-03 | New-hazard CR |
| DS-PMS-109 | FS-RM-04 | RM Plan template |
| DS-PMS-110 | FS-RM-05 | RM review cadence |
| DS-PMS-111 | FS-RM-06 | Hazard-to-event traceability |

---

## 11. Design-Level Risk Register

| ID | Design-level risk | Likelihood | Impact | Mitigation reference (DS) |
|---|---|---|---|---|
| DR-01 | National-CA gateway certificate rotation failure | Medium | High | Monitoring + auto-alert; manual fallback documented (DS-PMS-65..67) |
| DR-02 | Atlas sales-volume API schema change breaks Art. 88 denominator | Medium | Medium | Contract test + integration health endpoint (DS-PMS-57) |
| DR-03 | EUDAMED PSUR module version mismatch | Low | High | Pinned API version + migration runbook (DS-PMS-58) |
| DR-04 | Missed PSUR deadline | Medium | High | DS-PMS-22 cadence engine + DS-PMS-21 PRRC alert chain |
| DR-05 | Signal not detected in trending (false-negative) | Medium | High | DS-PMS-24 + DS-PMS-25 statistical tests |
| DR-06 | Missed Article 87 serious-incident reporting timeline | Medium | Critical | DS-PMS-30..32 + alert ladder D-3/D-1/D-0 |
| DR-07 | PMCF commitment slipped | Medium | Medium | DS-PMS-28 commitment table + alerts |
| DR-08 | Audit-trail tampering | Low | Critical | DS-PMS-38 append-only constraint |
| DR-09 | Class change (non-serious → serious) not re-triggering reporting timelines | Low | Critical | DS-PMS-32 class-change watcher |
| DR-10 | Trend statistical method invalid for low-event-rate device | Medium | Medium | DS-PMS-24 per-class method choice |
| DR-11 | PRRC signature delegation under time pressure | Low | High | DS-PMS-21 delegation endpoint disabled at sign moment (non-delegatable) |
| DR-12 | Data residency non-compliance (EU MDR data crossing jurisdictions inappropriately) | Low | High | DS-PMS-76 + vendor DPA |
| DR-13 | Real-time dashboard staleness undetected during inspection | Low | High | DS-PMS-82 latency SLO + DS-PMS-92 inspection-readiness export |
| DR-14 | Notified-Body PSUR assessment milestone missed | Low | High | DS-PMS-96 NB tracker + DS-PMS-21 alert chain |
| DR-15 | Risk-control effectiveness drift unnoticed (ISO 14971 § 10.3) | Medium | High | DS-PMS-88 threshold breach raises change-flag |
| DR-16 | Health-authority correspondence response deadline breach | Medium | High | DS-PMS-90 register + DS-PMS-91 workflow |
| DR-17 | Duplicate complaints across patient + HCP + distributor channels | Medium | Medium | DS-PMS-102 dedup engine |
| DR-18 | EUDAMED Certificate module expiry watcher (DS-PMS-61) misses 7-day alert during gateway maintenance | Low | High | Pre-maintenance runbook + manual cron + DS-PMS-95 secondary NB register watcher |
| DR-19 | EU MDR Art. 92 routing (DS-PMS-22) fails for a Class I PMSR misclassified as Class IIa biennial PSUR | Low | High | Class metadata immutable post-CE-mark; PSMR generator (DS-PMS-20) hard-routes Class I |
| DR-20 | Patient intake form (DS-PMS-99) captures unconsented PII via Zendesk integration | Low | Critical | GDPR Art. 6 consent capture at form load + DPO sampled review |

The DS Design-level Risk Register is the design-stage seed for `VGD-RA-PMS-001`; per-FS-ID criticality remains in the FS Implementation Risk Register.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
