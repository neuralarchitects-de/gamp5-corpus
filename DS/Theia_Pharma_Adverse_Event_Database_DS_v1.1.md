---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "TEA-FS-MDR-001 v1.2 (parent FS)"
  - "TEA-URS-MDR-001 v1.2 (informational)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 — Configuration Specification"
  - "Sparta TrackWise Digital Quality (Vigilance Module) Administrator Guide; FDA eMDR Implementation Guide; EUDAMED Vigilance Module Specification"
parent_fs:
  document_number: TEA-FS-MDR-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Theia_Pharma_Adverse_Event_Database_FS_v1.3.md
parent_urs:
  document_number: TEA-URS-MDR-001
  version: 1.2
  file: ../../../URS/_generated/final/Adverse_Event_Database__Theia_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Medical-Device Adverse Event Database — Sparta TrackWise Digital Quality (Vigilance Module)

**Document Number:** TEA-DS-MDR-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** TEA-FS-MDR-001 v1.2 | **Parent URS:** TEA-URS-MDR-001 v1.2
**Site:** Theia Pharma & Devices Ltd., Galway, Ireland *(fictional)* with hubs in München (DE) + Wien (AT)
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (multi-tenant SaaS, no site-authored custom code on tenant)
**Project Mode:** Greenfield deployment on Sparta TrackWise Digital Quality (Vigilance Module), replacing legacy device-vigilance tracker (per parent URS Project Mode line)
**Tier (inherited from parent URS+FS):** T3–T4 (uplifted at URS v1.2)
**Regulatory Scope:** 21 CFR Part 803 §§ .1–.58 (device MDR); 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU MDR Reg. 2017/745 Arts. 87 (serious-incident reporting), 88 (trend reporting), 89 (FSCA), 92 (EUDAMED); EU IVDR Reg. 2017/746 Arts. 82, 83; IMDRF AET WG/N43 (Adverse Event Terminology); MDCG 2023-3 (vigilance for medical devices); ISO 14971:2019 (risk management); ISO 13485:2016 (QMS); FDA CSA (Feb 2026); BfArM (DE), Swissmedic (CH), AGES (AT), MHRA YellowCard (UK), Health Canada CIPARS.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect — Vigilance Platforms) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Device Vigilance) | _____________ | _____________ | _____ |
| Reviewer (PRRC — EU MDR Art. 15) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Risk Management Lead — ISO 14971) | _____________ | _____________ | _____ |
| Reviewer (UDI / Atlas Serialization Lead) | _____________ | _____________ | _____ |
| Reviewer (InfoSec / DPO) | _____________ | _____________ | _____ |
| Reviewer (Sparta TenantOps Liaison) | _____________ | _____________ | _____ |
| Approver (VP Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |
| Approver (System Owner — Director, Device Vigilance) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue. Inherited Tier T3–T4 from parent URS+FS pair. Derived from TEA-FS-MDR-001 v1.2. DS covers 100/106 FS-IDs as DS-IDs; 6 FS-IDs flagged as "vendor-internal — no site design surface" (TrackWise Digital Quality tenant kernel, Sparta multi-tenant control plane, internal AET rule-engine compiler, EUDAMED gateway internals, FDA ESG gateway internals). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from TEA-URS-MDR-001 v1.2 and TEA-FS-MDR-001 v1.2. Additional DS-specific terms:

| Term | Definition |
|---|---|
| CI | Configuration Item (a TrackWise Digital Quality configurable parameter / workflow / rule / role / form) |
| TWD-Q | TrackWise Digital Quality (Vigilance Module) |
| AET | Adverse Event Terminology (IMDRF WG/N43) |
| MDR (FDA) | Medical Device Reporting (21 CFR Part 803) — note: NOT the EU MDR regulation |
| MIR | Manufacturer Incident Report (EU MDR Art. 87, MDCG 2023-3 template) |
| FSCA | Field Safety Corrective Action |
| FSN | Field Safety Notice |
| eMDR | electronic Medical Device Report (FDA ESG path) |
| MAUDE | FDA Manufacturer and User Facility Device Experience database |
| UDI-DI | Unique Device Identifier — Device Identifier |
| RMF | Risk Management File (ISO 14971) |
| PRRC | Person Responsible for Regulatory Compliance (EU MDR Art. 15) |

## 1. Purpose

This CS records the per-CI configuration of the Sparta TrackWise Digital Quality (Vigilance Module) tenant for Theia Pharma & Devices, the configured workflows, role-permission matrix, and integration endpoint bindings that together implement the functional behaviour in `TEA-FS-MDR-001` v1.2. The CS is the controlling input to `TEA-IQ-MDR-001`, `TEA-OQ-MDR-001`, `TEA-PQ-MDR-001`, and `TEA-CONFIG-BASELINE-MDR-001`. Vendor TrackWise internals (Sparta SDLC) are not redrawn here.

## 2. Scope

**In scope.** Per-CI configuration values for TrackWise Digital Quality Vigilance Module tenant `theia-devices-prod`; per-device-family configuration; reporting-clock rule pack; FDA Part 803 decision-tree configuration; IMDRF AET coding configuration; FSCA + trend (EU MDR Art. 88) configuration; MAUDE-prep configuration; ISO 14971 RMF linkage; per-NCA gateway profiles (BfArM IRIS, Swissmedic ElViS, AGES, Health Canada CIPARS); integration with Sirius PV (Argus) for combination products; MasterControl eQMS; Atlas Serialization (UDI-DI master); literature surveillance; SSO via Okta SAML 2.0 + MFA; multi-tenant SaaS guard-rails.

**Out of scope.** TrackWise tenant-kernel internals (Sparta SDLC); EUDAMED gateway internals (EU Commission); FDA ESG gateway internals (FDA); Okta IdP design; tenant-level multi-tenancy isolation primitives.

## 3. Architectural Overview

```
                  ┌────────────────────────────────────────────────────┐
                  │ Okta IdP (SAML 2.0 + MFA — `mdr-prod-users`)       │
                  └────────────────────┬───────────────────────────────┘
                                       │
   ┌───────────────────────────────────▼───────────────────────────────────┐
   │            Sparta TrackWise Digital Quality (Vigilance)                │
   │            Tenant: `theia-devices-prod`                                │
   │  ┌────────────────────┐  ┌────────────────────┐  ┌─────────────────┐  │
   │  │ Case Intake +      │  │ MDR Decision Tree  │  │ AET Coding      │  │
   │  │ Triage Workflow    │◄─┤ (21 CFR 803 + EU   │◄─┤ (IMDRF WG/N43)  │  │
   │  │                    │  │  MDR Art. 87/88)   │  │                 │  │
   │  └────────────────────┘  └────────────────────┘  └─────────────────┘  │
   │  ┌──────────────────────────────────────────────────────────────────┐ │
   │  │ Clock Calculator (per agency: FDA 5d/15d/30d, EU 2d/10d/15d,     │ │
   │  │  CH/AT/UK/CA timelines)                                          │ │
   │  └──────────────────────────────────────────────────────────────────┘ │
   │  ┌─────────────┐  ┌─────────────┐  ┌──────────────┐  ┌─────────────┐  │
   │  │ FSCA / FSN  │  │ Trend (Art. │  │ MAUDE prep   │  │ RMF link    │  │
   │  └─────────────┘  │  88)        │  └──────────────┘  │ (ISO 14971) │  │
   │                   └─────────────┘                    └─────────────┘  │
   └─┬────────┬────────┬─────────┬─────────┬─────────┬─────────┬───────────┘
     ▼        ▼        ▼         ▼         ▼         ▼         ▼
   FDA      EUDAMED  BfArM    Swissmedic AGES     CIPARS   MHRA
   ESG      Vigilance IRIS    ElViS     (AT)     (HC)     YellowCard
   eMDR     Module
                                       ▲
                                       │
   Atlas    MasterControl  Sirius PV   Lit feed (vendor)
   (UDI-DI) eQMS (CAPA)    Argus
                           (combo
                            products)
```

The TrackWise tenant `theia-devices-prod` is operated by Sparta as multi-tenant SaaS. Theia consumes only configuration-surface CIs; tenant kernel internals are under Sparta SDLC. Reporting clocks are split per agency: FDA 21 CFR 803 (5d/15d/30d), EU MDR Art. 87 (2d/10d/15d), CH/AT national supplements, Health Canada (10d/30d), MHRA YellowCard (10d/30d). The combination-product integration to Sirius PV (Argus) handles drug-device combinations where Argus is the drug-side master and TrackWise is the device-side master.

## 4. Configuration Specification

### 4.1 Vendor + Configuration Lifecycle

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-VND-01 | Sparta vendor-assurance dossier | `VA-SPARTA-2026` (SOC 2 Type II, ISO 27001, customer-shared CSV evidence) | Custom | Required for multi-tenant SaaS gate-keeping. | FS-VND-01 | OQ-MDR-VND-01 |
| DS-VND-02 | Sparta release-note ingestion | Sparta RSS feed `sparta.com/twdq/releases.rss`; auto-ticket in MasterControl CR system within 24 h | Custom | Aligns with FS-VND-02 SLA. | FS-VND-02 | OQ-MDR-VND-02 |
| DS-VND-03 | Sparta TR-Audit cadence | Annual; filed in `VA-SPARTA-2026/tr-audit-{year}.pdf` | Default | Sparta annual cadence. | FS-VND-03 | (deferred) |
| DS-CFG-01 | Per-device-family config lifecycle | DRAFT → REVIEW → APPROVED → EFFECTIVE; SoD-enforced (Author ≠ Approver) | Custom | Reproduces FS-CFG-01. | FS-CFG-01 | OQ-MDR-CFG-01 |
| DS-CFG-02 | Configuration export | `GET /admin/config/export?device-family={id}` returns versioned JSON; 35-y archival | Custom | Inspection retrieval. | FS-CFG-02 | OQ-MDR-CFG-02 |

### 4.2 Case Intake + Triage

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-INTAKE-01 | Intake channels | Manual UI; EUDAMED inbound webhook; FDA MAUDE-import (CSV monthly); HCP-portal REST `/intake/hcp`; complaint-handling import from MasterControl; literature feed; partner OEM exchange | Custom | Matches FS-INTAKE-01 list. | FS-INTAKE-01 | OQ-MDR-INTAKE-01 |
| DS-INTAKE-02 | Case-id format | `THE-{HUB}-{YYYY}-{NNNNNN}` (HUB ∈ {GAL, MUC, WIE}) | Custom | Hub-prefix for routing + audit. | FS-INTAKE-02 | OQ-MDR-CASE-ID-01 |
| DS-INTAKE-03 | Mandatory intake fields | Intake date; awareness date; UDI-DI (or `unknown`); device-family; reporter type; event type (death/serious-injury/malfunction); country of occurrence | Custom | EU MDR + FDA Part 803 minima. | FS-INTAKE-03 | OQ-MDR-CASE-VAL-01 |
| DS-INTAKE-04 | UDI-DI lookup integration | Atlas Serialization `/api/v2/udi/{udi-di}` returns device-family + risk class + lifecycle stage | Custom | UDI-DI master is Atlas. | FS-INTAKE-04 | OQ-MDR-UDI-LOOKUP-01 |
| DS-INTAKE-05 | Auto-triage decision rules | `triage-rules-2026.yaml` — auto-assign to {Reportable, Trend-only, Non-reportable} based on event type + device risk class + outcome | Custom | Reduces manual triage. | FS-INTAKE-05 | OQ-MDR-TRIAGE-01 |
| DS-INTAKE-06 | Duplicate detection | UDI-DI + event date ± 7 d + reporter ID + event-type match | Custom | Tuned for device-vigilance patterns. | FS-INTAKE-06 | OQ-MDR-DEDUP-01 |

### 4.3 Case Workflow + State Machine

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CASE-01 | Workflow XML | `mdr-workflow-v2.xml` — Intake → Triaged → Coded → Assessed → Reported → Closed; reverse-transition requires reason + e-sig | Custom | Reproduces FS-CASE-01 state shape. | FS-CASE-01 | OQ-MDR-WF-01 |
| DS-CASE-02 | Coded-state gating | Cannot transition to Reported without IMDRF AET codes (device-problem, evaluation-result, health-effect) | Custom | Closes "coded → reported skip" gap. | FS-CASE-02 | OQ-MDR-WF-GATE-01 |
| DS-CASE-03 | Reverse-transition reason enum | `data-correction`, `mis-triage`, `mis-classification`, `agency-feedback`, `complaint-merge`, `other` | Custom | Forces structured reason for audit. | FS-CASE-03 | OQ-MDR-WF-REASON-01 |
| DS-CASE-04 | Follow-up handler | `case_version` table; delta vs prior; FU triggers new MIR/MDR if FU intersects reportability-relevant fields | Custom | Reproduces FS-CASE-04. | FS-CASE-04 | OQ-MDR-FU-01 |
| DS-CASE-05 | Case-priority matrix | `case-priority-2026.yaml` (High/Medium/Normal) per (device risk class, event type) | Custom | High-priority routes to dedicated queue. | FS-CASE-05 | OQ-MDR-PRIO-01 |
| DS-CASE-06 | Workload balancer | Round-robin with hub-language affinity (de-DE→MUC; de-AT→WIE; en→GAL) | Custom | Language affinity. | FS-CASE-06 | OQ-MDR-WL-01 |
| DS-CASE-07 | State-event Kafka topic | `mdr.case.state.v1` for KPI dashboard | Custom | Cycle-time KPI. | FS-CASE-07 | OQ-MDR-KAFKA-01 |

### 4.4 MDR / MIR Reportability Decision Tree

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-MDR-01 | FDA 21 CFR Part 803 decision tree | `fda-803-decision-tree-2026.yaml` per § 803.20 (death/serious-injury/malfunction reportability) | Custom | Theia's FDA-specific rule set. | FS-MDR-01 | OQ-MDR-FDA-DT-01 |
| DS-MDR-02 | EU MDR Art. 87 decision tree | `eu-mdr-art87-decision-tree-2026.yaml` (serious-incident, death, public-health) | Custom | EU rule set per MDCG 2023-3. | FS-MDR-02 | OQ-MDR-EU-DT-01 |
| DS-MDR-03 | Reportability-justification record | Required structured field on every case with `reportable=false` (decision justification + reviewer-id + timestamp) | Custom | Audit-grade non-reportable rationale. | FS-MDR-03 | OQ-MDR-NONREP-01 |
| DS-MDR-04 | Per-jurisdiction reportability override | When jurisdictions disagree (e.g. FDA-reportable, EU-not), case stays reportable + agency-routing matrix splits | Custom | Avoids accidental under-reporting. | FS-MDR-04 | OQ-MDR-DIVERGE-01 |
| DS-MDR-05 | Annual decision-tree review | `SOP-MDR-DT-REVIEW-001`; runs on FDA/EU regulator updates + annual cadence | Custom | Rule-pack currency. | FS-MDR-05 | OQ-MDR-DT-REVIEW-01 |

### 4.5 IMDRF AET Coding

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CODE-01 | IMDRF AET dictionary version pin | IMDRF AET WG/N43 (Annex A, B, C, D, E, F, G) v2025.1 per-device-family pin | Custom | Reproducibility for inspection. | FS-CODE-01 | OQ-MDR-AET-VER-01 |
| DS-CODE-02 | AET coding levels | Annex A (device problem) + Annex E (health effect) + Annex F (clinical signs/symptoms) + Annex G (evaluation results) | Default | IMDRF expected coverage. | FS-CODE-02 | OQ-MDR-AET-COVER-01 |
| DS-CODE-03 | AET version-upgrade workflow | Annual review; cut-over runbook `SOP-MDR-AET-UPGRADE-001`; open-case re-code policy | Custom | Reproducibility. | FS-CODE-03 | OQ-MDR-AET-UPG-01 |
| DS-CODE-04 | Coding-QC sample | Monthly ≥ 2% of reported cases; discrepancy report to Coding Manager | Custom | Same shape as Sirius PV DS-CODE-07. | FS-CODE-04 | OQ-MDR-CODE-QC-01 |
| DS-CODE-05 | Auto-coding configuration | TWD-Q AET-helper enabled with confidence threshold 0.85; coder review required | Custom | Reduces silent miscoding. | FS-CODE-05 | OQ-MDR-AUTOCODE-01 |

### 4.6 Reporting Clock + Submissions

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-TIME-01 | Clock rule pack | `clock-rules-mdr-2026.yaml` — FDA 5d/15d/30d (Part 803), EU MDR 2d (death/public-health)/10d (serious-incident)/15d (other), CH/AT/UK/CA per national rules | Custom | Theia's portfolio breadth. | FS-TIME-01 | OQ-MDR-CLOCK-01 |
| DS-TIME-02 | Alert thresholds | D-3 / D-1 / D0 to PRRC + Vigilance Officer via PagerDuty `mdr-on-call` | Custom | Three-tier escalation. | FS-TIME-02 | OQ-MDR-CLOCK-ALERT-01 |
| DS-TIME-03 | Reclassification recompute | On `reportability` change → recompute clock + re-route | Custom | Closes reclassification-miss risk. | FS-TIME-03 | OQ-MDR-CLOCK-RECLASS-01 |
| DS-TIME-04 | Weekend / holiday handling | Per-jurisdiction working-day vs calendar-day rule (EU calendar-day; FDA business-day for non-death) | Custom | Reduces silent late-reporting. | FS-TIME-04 | OQ-MDR-CLOCK-CAL-01 |
| DS-TIME-05 | Clock-display UI | Remaining time per agency surfaced on case page; UTC + local | Default | TWD-Q standard. | FS-TIME-05 | OQ-MDR-CLOCK-UI-01 |
| DS-SUB-01 | FDA eMDR submission | TWD-Q eMDR generator emits Part 803 XML per FDA spec; FDA ESG transport | Default | TWD-Q ships FDA profile. | FS-SUB-01 | OQ-MDR-eMDR-01 |
| DS-SUB-02 | EU MDR MIR submission | TWD-Q MIR generator per MDCG 2023-3 template; EUDAMED Vigilance Module transport | Default | EUDAMED standard. | FS-SUB-02 | OQ-MDR-MIR-01 |
| DS-SUB-03 | ACK reconciliation | ACK-1 (transport) ≤ 60 min; ACK-2 (application) ≤ 24 h; reconciled in `submission_ack` | Custom | Reproduces FS-SUB-03. | FS-SUB-03 | OQ-MDR-ACK-01 |
| DS-SUB-04 | Negative-ack workflow | Exception with agency-error-code map → re-submission within grace → PRRC escalation on breach | Custom | Closes silent-rejection. | FS-SUB-04 | OQ-MDR-EXC-01 |

### 4.7 Follow-Up + Trend (EU MDR Art. 88) + FSCA + MAUDE Prep

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-FU-01 | Follow-up state | `case_followup` table; FU creates new `case_version` linked to parent | Default | TWD-Q FU shape. | FS-FU-01 | OQ-MDR-FU-STATE-01 |
| DS-FU-02 | FU reportability re-evaluation | FU triggers re-run of MDR/MIR decision tree | Custom | Closes "FU upgrades reportability silently" gap. | FS-FU-02 | OQ-MDR-FU-REPORT-01 |
| DS-FU-03 | FU clock recompute | FU intersects clock-relevant field → recompute | Custom | Same as DS-TIME-03 but FU path. | FS-FU-03 | OQ-MDR-FU-CLOCK-01 |
| DS-TRD-01 | Art. 88 trend definition | TWD-Q Trend Module configured per (device-family, AET-code) with threshold (rolling-90d count > μ + 2σ) | Custom | EU MDR Art. 88. | FS-TRD-01 | OQ-MDR-TREND-01 |
| DS-TRD-02 | Trend-report submission | Triggered on threshold breach → MIR-Trend submission to EUDAMED + national CAs | Custom | Art. 88 obligation. | FS-TRD-02 | OQ-MDR-TREND-SUB-01 |
| DS-TRD-03 | Trend dashboard | Grafana `mdr-trend-monitor` per device-family + AET pivot | Custom | Vigilance Officer review weekly. | FS-TRD-03 | OQ-MDR-TREND-DASH-01 |
| DS-TRD-04 | Trend-rule maintenance | Annual review of (μ, σ, rolling window); change under CR | Custom | Closes silent threshold drift. | FS-TRD-04 | OQ-MDR-TREND-RULE-01 |
| DS-FSCA-01 | FSCA workflow | TWD-Q FSCA module: Initiate → Investigate → Approve → Notify CAs → Distribute FSN → Track Closure | Default | EU MDR Art. 89. | FS-FSCA-01 | OQ-MDR-FSCA-WF-01 |
| DS-FSCA-02 | FSN template set | de-DE, de-AT, de-CH, fr-CH, it-CH, en-IE, en-GB templates in `fsn-templates/` | Custom | DACH+UK+IE language coverage. | FS-FSCA-02 | OQ-MDR-FSCA-FSN-01 |
| DS-FSCA-03 | FSCA-NCA notification routing | NCA list per FSCA scope (country-of-distribution) | Custom | Avoids over/under-notification. | FS-FSCA-03 | OQ-MDR-FSCA-NCA-01 |
| DS-FSCA-04 | FSCA closure evidence requirement | Distribution-confirmed + post-action evaluation required to close | Custom | Inspection-grade. | FS-FSCA-04 | OQ-MDR-FSCA-CLOSE-01 |
| DS-MAUDE-01 | MAUDE-prep template | FDA MAUDE-public-data field set; rendering for in-house review pre-publication | Default | FDA standard. | FS-MAUDE-01 | OQ-MDR-MAUDE-01 |
| DS-MAUDE-02 | MAUDE-prep weekly review | Vigilance Officer weekly review of submitted-cases against MAUDE public records | Custom | Detects ESG transport anomalies. | FS-MAUDE-02 | OQ-MDR-MAUDE-REVIEW-01 |

### 4.8 RMF Linkage (ISO 14971), EUDAMED, NCA Gateways, Combination Products, Literature

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RMF-01 | RMF reference per device-family | Per-device-family RMF document number in TWD-Q `device_family.rmf_doc_no` | Custom | ISO 14971 traceability. | FS-RMF-01 | OQ-MDR-RMF-01 |
| DS-RMF-02 | Hazard-linkage on AET | AET code linked to RMF hazard taxonomy; report case → RMF update workflow | Custom | Closes PMS-to-risk-update loop. | FS-RMF-02 | OQ-MDR-RMF-LINK-01 |
| DS-RMF-03 | Annual RMF review | RMF-update workflow runs annually + on signal | Custom | ISO 14971:2019. | FS-RMF-03 | OQ-MDR-RMF-REVIEW-01 |
| DS-EUDAMED-01 | EUDAMED Vigilance Module endpoint | Production endpoint per EUDAMED spec; mTLS cert `eudamed-client-2026.p12` | Custom | EU MDR Art. 92 mandatory. | FS-EUDAMED-01 | OQ-MDR-EUDAMED-01 |
| DS-EUDAMED-02 | EUDAMED routine maintenance window handling | `eudamed-windows-2026.yaml`; scheduler skips windows | Custom | Reduces submission failures. | FS-EUDAMED-02 | OQ-MDR-EUDAMED-WIN-01 |
| DS-NCA-BFARM-01 | BfArM IRIS endpoint | `https://iris.bfarm.bund.de/medical-devices/v2`; profile `iris-2026`; mTLS cert | Custom | DACH national supplement to EU MDR. | FS-NCA-BFARM-01 | OQ-MDR-BFARM-01 |
| DS-NCA-SWISS-01 | Swissmedic ElViS endpoint | Per HMG-MepV; profile `elvis-2026`; mTLS cert | Custom | CH-specific timelines. | FS-NCA-SWISS-01 | OQ-MDR-SWISS-01 |
| DS-NCA-AGES-01 | AGES endpoint (AT) | Per MPG; profile `ages-mdr-2026`; mTLS cert | Custom | AT-specific timelines. | FS-NCA-AGES-01 | OQ-MDR-AGES-01 |
| DS-NCA-LANG-01 | DACH FSN templates | Same set as DS-FSCA-02 | Default | Reuse. | FS-NCA-LANG-01 | (see DS-FSCA-02) |
| DS-COMBO-01 | Drug-device combination handoff | Kafka topic `theia.combo.handoff.v1` → Sirius PV (Argus) `/intake/combo`; bidirectional case-id linkage | Custom | Combo-product safety routing. | FS-COMBO-01 | OQ-MDR-COMBO-01 |
| DS-COMBO-02 | Combination-product classification rule | Per device-family: `principal_mode_of_action ∈ {drug, device}` determines master system | Custom | Closes silent combo mis-routing. | FS-COMBO-02 | OQ-MDR-COMBO-CLASS-01 |
| DS-INSP-01 | Inspection retrieval ≤ 4 h | `SOP-MDR-INSP-RETR-001`; export bundle includes case + audit + RMF | Custom | Inspection-grade. | FS-INSP-01 | OQ-MDR-INSP-01 |
| DS-INSP-02 | Read-only inspector account | TWD-Q role `inspector_readonly`; time-bound provisioning | Custom | Auditor self-service. | FS-INSP-02 | OQ-MDR-INSP-RO-01 |
| DS-INSP-03 | Inspection-bundle export format | PDF/A-3 + JSON; SHA-256 hash file alongside | Custom | Long-term archival. | FS-INSP-03 | OQ-MDR-INSP-EXPORT-01 |

### 4.9 Audit Trail + 21 CFR Part 11 + DI + Security + Performance + Training + Periodic Review

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUD-01 | TWD-Q audit-trail filter | All Critical Events + Login + Approve + Reject + Reclassify + Coding-override + Signature + Workflow-transition + Config-change + FSCA-event | Custom | Default filter omits FSCA events. | FS-AUD-01 | OQ-MDR-AUD-FILT-01 |
| DS-AUD-02 | Audit append-only at tenant | Sparta tenant-kernel guarantee + DB-level constraint per multi-tenant SOP; UPDATE/DELETE blocked at tenant | Default | Sparta default. | FS-AUD-02 | OQ-MDR-AUD-APP-01 |
| DS-AUD-03 | Audit-review job | Case-event-driven at approval; platform-quarterly Splunk saved-search | Custom | Same shape as Sirius PV. | FS-AUD-03 | OQ-MDR-AUD-REVIEW-01 |
| DS-AUD-04 | Retention | ≥ 25 y (devices) + ≥ life-of-product + 35 y (paediatric devices) immutable | Custom | EU MDR Art. 10 retention + paediatric extension. | FS-AUD-04 | OQ-MDR-AUD-RET-01 |
| DS-PART11-01 | Part 11 procedural SOPs | `SOP-MDR-VAL-001`, `SOP-MDR-CASE-002`, `SOP-MDR-SIG-003`; annual review | Custom | Reproduces FS-PART11-01. | FS-PART11-01 | OQ-MDR-SOP-01 |
| DS-PART11-02 | Copy generation set | PDF/A-3 case + eMDR XML + audit CSV | Custom | Three channels. | FS-PART11-02 | OQ-MDR-COPY-01 |
| DS-PART11-03 | Record protection tier | Sparta tenant object-lock 35 y compliance mode | Default | Sparta long-retention tier. | FS-PART11-03 | OQ-MDR-PROT-01 |
| DS-PART11-04 | Access policy | Okta `mdr-prod-users` group; MFA; service accounts mTLS-only | Custom | Closes auth bypass. | FS-PART11-04 | OQ-MDR-ACCESS-01 |
| DS-PART11-05 | E-sig manifestation | Renders printed name + UTC+local timestamp + meaning enum (Review/Approve/Sign-Off/Submit) | Custom | § 11.50. | FS-PART11-05 | OQ-MDR-SIG-MANIF-01 |
| DS-PART11-06 | E-sig cryptographic linkage | HMAC-SHA-256 over (record-hash, signer-id, timestamp) | Custom | § 11.70. | FS-PART11-06 | OQ-MDR-SIG-CRYPTO-01 |
| DS-PART11-07 | User-id uniqueness | TWD-Q + Okta both enforce; deactivated never reassigned | Custom | § 11.100. | FS-PART11-07 | OQ-MDR-USERID-01 |
| DS-PART11-08 | Re-auth on signing | OAuth2 max-age 5 min; MFA on every approval | Custom | § 11.200. | FS-PART11-08 | OQ-MDR-REAUTH-01 |
| DS-PART11-09 | Password policy | Okta `mdr-prod-password` — length ≥ 12, MFA, 90-d rotation, lockout 5/15 | Custom | § 11.300. | FS-PART11-09 | OQ-MDR-PWD-01 |
| DS-PART11-10 | Authority check | TWD-Q role-permission + API guard `mdr-api-guard` middleware | Custom | Defense-in-depth. | FS-PART11-10 | OQ-MDR-AUTHZ-01 |
| DS-DI-01 | ALCOA+ Attributable | `audit_event.user_id` NOT NULL | Custom | DI invariant. | FS-DI-01 | OQ-MDR-ALCOA-A-01 |
| DS-DI-02 | ALCOA+ Legible | PDF/A-3 + eMDR/MIR XML export OQ-verified | Default | Verbatim. | FS-DI-02 | OQ-MDR-ALCOA-L-01 |
| DS-DI-03 | ALCOA+ Contemporaneous | NTP-synced; retroactive flagged | Custom | Closes back-date. | FS-DI-03 | OQ-MDR-ALCOA-C-01 |
| DS-DI-04 | ALCOA+ Original | Source preserved; corrections create new version | Default | TWD-Q default. | FS-DI-04 | OQ-MDR-ALCOA-O-01 |
| DS-DI-05 | ALCOA+ Accurate | Clock + trend calculations deterministic; OQ golden-test pack | Custom | Reproducibility. | FS-DI-05 | OQ-MDR-ALCOA-AC-01 |
| DS-DI-06 | ALCOA+ Complete + Consistent + Enduring + Available | Mandatory matrix per agency; chronological-order DB-enforced; 35-y retention; ≤ 4 h retrieval | Custom | Bundled per FS row. | FS-DI-06 | OQ-MDR-ALCOA-COMP-01 |
| DS-SEC-01 | SSO + MFA | Okta SAML 2.0 + MFA (FIDO2 phishing-resistant for PRRC subgroup) | Custom | Per FS-XSYS-AD-01. | FS-SEC-01, FS-XSYS-AD-01 | OQ-MDR-SSO-01 |
| DS-SEC-02 | DPIA + cross-border | DPIA-MDR-2026-001; SCCs `mdr-scc-2026` for cross-border | Custom | GDPR Art. 35 + 44. | FS-SEC-02 | OQ-MDR-DPIA-01 |
| DS-SEC-03 | Vuln scan + pen-test | Monthly Tenable Nessus + annual third-party pen-test (Sparta-tenant-scoped) | Custom | Standard cadence. | FS-SEC-03 | OQ-MDR-VULN-01 |
| DS-PERF-01 | Performance envelope | Case-page P95 ≤ 3 s; eMDR/MIR generation P95 ≤ 5 s | Custom | T3 envelope. | FS-PERF-01 | PQ-MDR-PERF-01 |
| DS-AV-01 | Availability | ≥ 99.5% business hours; 24×7 gateway windows | Default | TWD-Q SLA. | FS-AV-01 | OQ-MDR-AV-01 |
| DS-BAK-01 | Backup policy | Sparta tenant backup nightly + WAL-stream; retention ≥ 35 y per AUR-FS-BACKUP-001 | Default | Sparta + cross-system. | FS-BAK-01, FS-XSYS-BAK-01 | OQ-MDR-BAK-01 |
| DS-TRN-01 | Production access gate | LMS-recorded role-specific + device-vigilance competency; PRRC annual re-attestation | Custom | LMS adapter per FS-XINT-LMS-01. | FS-TRN-01, FS-XINT-LMS-01 | OQ-MDR-TRN-01 |
| DS-TRN-02 | Annual refresher | LMS course `MDR-ANNUAL-2026`: MDCG updates, FDA Part 803 updates, IMDRF AET version updates | Custom | Course id. | FS-TRN-02 | OQ-MDR-TRN-02 |
| DS-PR-01 | Annual periodic review | `SOP-MDR-ANNUAL-001`; collects config drift, audit evidence, AET version, gateway connectivity, trend rules, FSCA closures, RMF currency, deviation summary, training | Custom | Signed by PRRC + Director Vigilance + VP QA. | FS-PR-01 | OQ-MDR-PR-01 |

### 4.10 Integration Endpoints — per-Counterparty CIs

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-INT-SSO-01 | Okta IdP binding | SAML 2.0 + MFA; group `mdr-prod-users` | Custom | Per FS-INT-SSO-01. | FS-INT-SSO-01 | OQ-MDR-SSO-01 |
| DS-INT-FDA-01 | FDA ESG (eMDR) | FDA ESG production endpoint; cert `fda-esg-mdr-2026.p12` (Vault) | Custom | FDA-managed. | FS-INT-FDA-01 | OQ-MDR-FDA-ESG-01 |
| DS-INT-EUDAMED-01 | EUDAMED Vigilance Module | Production endpoint; mTLS `eudamed-client-2026.p12` | Custom | Per FS-INT-EUDAMED-01. | FS-INT-EUDAMED-01 | OQ-MDR-EUDAMED-INT-01 |
| DS-INT-UDI-01 | Atlas Serialization UDI master | `https://atlas.theia.local/api/v2/udi/`; OAuth2 + signed JWT | Custom | UDI master. | FS-INT-UDI-01 | OQ-MDR-UDI-MASTER-01 |
| DS-INT-PV-01 | Sirius PV (Argus) combination-product handoff | Kafka `theia.combo.handoff.v1` + REST `/intake/combo`; bidirectional | Custom | Cross-system combo routing. | FS-INT-PV-01 | OQ-MDR-PV-COMBO-01 |
| DS-INT-EQMS-01 | MasterControl eQMS | REST `/capa/incident`; OAuth2 | Custom | CAPA bridge per FS-XINT-EQMS-*. | FS-INT-EQMS-01, FS-XINT-EQMS-01, FS-XINT-EQMS-02 | OQ-MDR-EQMS-01 |
| DS-INT-LIT-01 | Literature surveillance feed | Weekly per-device-family strategy | Custom | Per FS-LIT-* equivalent. | FS-INT-LIT-01 | OQ-MDR-LIT-01 |
| DS-INT-PMS-01 | PMS aggregate (cross-system) | Per FS-XINT-PMS-*; cross-system PMS bridge | Custom | Closes PMS↔vigilance loop. | FS-XINT-PMS-01, FS-XINT-PMS-02 | OQ-MDR-PMS-01 |

## 5. Workflow + Business-Rule Design

| Workflow / rule | Steps | Role bindings | Decision points |
|---|---|---|---|
| **Case Intake → Closure** | Intake → Triaged → Coded → Assessed → Reported → Closed | Intake: `vigilance_clerk`; Triaged: `vigilance_officer`; Coded: `coder`; Assessed: `medical_reviewer`; Reported: `prrc_designee`; Closed: `case_closer` (≠ Reported) | Reverse-transition with reason enum (DS-CASE-03). |
| **MDR/MIR Decision Tree** | Auto-evaluate FDA-803 tree + EU-Art87 tree → resolve divergence → final reportability | `medical_reviewer` + auto-rules engine | Divergence handled per DS-MDR-04 (keep reportable). |
| **FSCA Workflow** | Initiate → Investigate → Approve → Notify CAs → Distribute FSN → Track Closure | `vigilance_officer`, `prrc_designee`, `quality_lead` | Closure requires distribution-confirmed + post-action evaluation (DS-FSCA-04). |
| **Trend Detection (Art. 88)** | Monitor (rolling-90d AET-pivot) → Threshold breach → MIR-Trend → EUDAMED + NCAs | Auto-rule engine + `vigilance_officer` review | Threshold = μ + 2σ rolling-90d. |
| **eMDR / MIR Submission + ACK Reconciliation** | Reported → eMDR/MIR generation → ESG/EUDAMED send → ACK reconciliation → close-out | `submission_operator`, `prrc_designee` | Neg-ack → Exception → re-submit → escalate. |
| **Audit Quarterly Review** | Splunk saved-search → discrepancy triage → CAPA in MasterControl → evidence in `QA-MDR-AUDIT-{NNN}` | System Owner + QA Reviewer | Anomaly > 2× rolling-30d-mean. |
| **AET Annual Upgrade** | Impact assessment → cut-over → open-case re-code → smoke test → sign-off | Coding Manager + CSV Architect + PRRC | Open-state cases re-coded; closed preserve version-of-record. |

## 6. Role-Permission Matrix Design

| Role (TWD-Q + Okta group) | Cases (intake/triage/code/assess/report/close) | Workflow transitions | E-sig meanings | FSCA | Trend | Config |
|---|---|---|---|---|---|---|
| `vigilance_clerk` | C — — — — — | Intake → Triaged | — | — | — | — |
| `vigilance_officer` | C R — — — — | Triaged → Coded; merge-duplicate; FSCA-investigate | INVESTIGATE | C R | R | — |
| `coder` | — R C — — — | Coded | — | — | — | — |
| `medical_reviewer` | — R R C — — | Coded → Assessed; reverse-with-reason | REVIEW | R | — | — |
| `prrc_designee` | — R R R C — | Assessed → Reported; FSCA-approve; Trend-approve | APPROVE, REPORT, SIGN-OFF | A | A | — |
| `submission_operator` | — — — — R — | Reported → (eMDR/MIR send) | SUBMIT | — | — | — |
| `case_closer` | — — — — — C | Reported → Closed | CLOSE | — | — | — |
| `quality_lead` | R R R R R R | — | — | A | A | — |
| `csv_admin` | — — — — — — | — | — | — | — | C (workflow/profile — SoD: ≠ approver) |
| `csv_approver` | — — — — — — | APPROVE-CONFIG | APPROVE-CONFIG | — | — | R |
| `inspector_readonly` | R R R R R R | — | — | R | R | R |

Legend: C create; R read; A approve; — denied.

## 7. Integration Design

| Integration | Endpoint | Protocol | AuthN | Retry / error | Monitoring |
|---|---|---|---|---|---|
| Okta IdP | Theia Okta tenant `/app/twd-q-prod/saml/metadata` | SAML 2.0 + MFA | SP-initiated; group `mdr-prod-users` | Re-auth 5-min; lockout 5/15 | Okta log → Splunk `mdr-authn` |
| FDA ESG (eMDR) | FDA ESG production | AS2 | mTLS `fda-esg-mdr-2026.p12` | Exponential backoff; FDA error-code map | Splunk `mdr-fda-esg` |
| EUDAMED Vigilance | EUDAMED production endpoint | EU MDR Vigilance Module spec | mTLS `eudamed-client-2026.p12` | Window-aware scheduler | Splunk `mdr-eudamed` |
| BfArM IRIS | `https://iris.bfarm.bund.de/medical-devices/v2` | mTLS REST | `iris-client-2026.p12` | DACH error code map | Splunk `mdr-iris` |
| Swissmedic ElViS | per HMG-MepV | mTLS | `elvis-client-2026.p12` | CH timelines | Splunk `mdr-elvis` |
| AGES (AT) | per MPG | mTLS | `ages-client-2026.p12` | AT timelines | Splunk `mdr-ages` |
| Health Canada CIPARS | CIPARS production | mTLS | `cipars-client-2026.p12` | HC timelines | Splunk `mdr-cipars` |
| MHRA YellowCard | YellowCard endpoint | REST | API key + mTLS | UK timelines | Splunk `mdr-yellowcard` |
| Atlas Serialization (UDI master) | `https://atlas.theia.local/api/v2/` | REST | OAuth2 + signed JWT | Idempotent reads | Splunk `mdr-atlas` |
| MasterControl eQMS | `https://eqms.theia.local/api/capa` | REST | OAuth2 | Webhook + REST | Splunk `mdr-eqms` |
| Sirius PV (Argus) | Theia↔Sirius Kafka `theia.combo.handoff.v1` + REST `/intake/combo` | Kafka + REST | mTLS + signed JWT | Idempotent by combo-id | Splunk `mdr-combo-pv` |
| Literature feed | Embase + PubMed + device-specific journals | REST | API key | Weekly cron | Splunk `mdr-lit` |
| Cross-system Quartz AD (FS-XSYS-AD-01) | Entra ID via SAML 2.0 + SCIM | SAML 2.0 + MFA | Conditional Access `PV-Sensitive` | SIEM RFC 5424 → Splunk `gxp-authn` ≤ 5 min | per FS-XSYS-AD-01 |
| Cross-system Aurora Backup (FS-XSYS-BAK-01) | Veeam Application-Aware on TWD-Q + Atlas DB | per AUR-FS-BACKUP-001 | Veeam-DB plug-in mTLS | RPO ≤ 4 h; RTO ≤ 4 BH; S3 Object Lock + LTO-9 | Monthly QA-witnessed restore |
| Cross-system LMS competence (FS-XINT-LMS-01) | `https://lms.theia.local/lms/competence/{user_id}` | REST over mTLS | Entra workload-identity | Cache 12-24 h; block on `current=false` | Periodic reconciliation |

## 8. Site-Deployed Components Design

Site-developed code on tenant `theia-devices-prod` (Cat 5 sub-components inside Cat 4):

| Component | Language | Repo | Interface | Dependencies | Owner | GxP-criticality |
|---|---|---|---|---|---|---|
| `mdr-api-guard` | Java 17 + Spring Boot | `gitlab.theia.local/mdr-tooling/api-guard` | HTTP filter on TWD-Q tenant API | TWD-Q role table; Okta JWKS | Vigilance Platforms | R2 |
| `trend-rule-replay` | Python 3.11 + `pandas` | `gitlab.theia.local/mdr-tooling/trend-replay` | CLI; OQ regression for trend rules | TWD-Q DB read-only view | Vigilance Platforms | R2 |
| `combo-handoff-bridge` | Python 3.11 + Kafka | `gitlab.theia.local/mdr-tooling/combo-bridge` | Kafka producer/consumer for Argus | Argus REST; TWD-Q webhook | Combo Coordination | R1 (cross-system safety) |
| `udi-resolver` | Python 3.11 + httpx | `gitlab.theia.local/mdr-tooling/udi-resolver` | TWD-Q webhook on intake | Atlas Serialization API | UDI Team | R2 |
| `eMDR-MIR-export-cli` | Python 3.11 | `gitlab.theia.local/mdr-tooling/export-cli` | CLI; renders inspection bundle | TWD-Q DB read-only view | Vigilance Platforms | R2 |

Each component carries unit-test ref, signed-commits CI, mandatory 2-reviewer review, Trivy scan, and a Module Specification artefact `TEA-MS-MDR-{component}-001` (downstream).

## 9. References

**US**
- 21 CFR Part 803 §§ .1–.58 (Medical Device Reporting)
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- FDA *Computer Software Assurance for Production and Quality Management System Software* (Feb 2026)
- FDA *eMDR Implementation Guide* (current revision)

**EU**
- EU MDR Reg. 2017/745 Arts. 87 (incidents), 88 (trend), 89 (FSCA), 92 (EUDAMED), 10 (manufacturer obligations), 15 (PRRC)
- EU IVDR Reg. 2017/746 Arts. 82, 83
- MDCG 2023-3 — Vigilance for medical devices
- MDCG 2019-9 / 2021-1 (FSCA + FSN templates)
- GDPR Reg. (EU) 2016/679 Arts. 6, 9, 32, 35, 44

**International**
- IMDRF AET WG/N43 (Adverse Event Terminology)
- ISO 14971:2019 (Risk management for medical devices)
- ISO 13485:2016 (QMS for medical devices)
- ISO/IEC 27001:2022
- IEC 62366-1 (Usability engineering)
- ISPE GAMP 5 (2nd ed., 2022)

**DACH**
- BfArM (DE) — Medizinprodukte-Sicherheitsplanverordnung (MPSV) + IRIS
- Swissmedic (CH) — HMG + Medizinprodukteverordnung (MepV) + ElViS
- AGES (AT) — Medizinproduktegesetz (MPG)

**Vendor**
- Sparta — *TrackWise Digital Quality (Vigilance Module) Administrator Guide*
- Sparta — *TWD-Q Multi-Tenant SaaS Operations Guide*
- EUDAMED — *Vigilance Module Specification*
- FDA ESG — *AS2 Implementation Guide*

## 10. Appendix A — DS → FS Traceability Matrix

| DS ID | FS ID |
|---|---|
| DS-VND-01 | FS-VND-01 |
| DS-VND-02 | FS-VND-02 |
| DS-VND-03 | FS-VND-03 |
| DS-CFG-01 | FS-CFG-01 |
| DS-CFG-02 | FS-CFG-02 |
| DS-INTAKE-01 | FS-INTAKE-01 |
| DS-INTAKE-02 | FS-INTAKE-02 |
| DS-INTAKE-03 | FS-INTAKE-03 |
| DS-INTAKE-04 | FS-INTAKE-04 |
| DS-INTAKE-05 | FS-INTAKE-05 |
| DS-INTAKE-06 | FS-INTAKE-06 |
| DS-CASE-01 | FS-CASE-01 |
| DS-CASE-02 | FS-CASE-02 |
| DS-CASE-03 | FS-CASE-03 |
| DS-CASE-04 | FS-CASE-04 |
| DS-CASE-05 | FS-CASE-05 |
| DS-CASE-06 | FS-CASE-06 |
| DS-CASE-07 | FS-CASE-07 |
| DS-MDR-01 | FS-MDR-01 |
| DS-MDR-02 | FS-MDR-02 |
| DS-MDR-03 | FS-MDR-03 |
| DS-MDR-04 | FS-MDR-04 |
| DS-MDR-05 | FS-MDR-05 |
| DS-CODE-01 | FS-CODE-01 |
| DS-CODE-02 | FS-CODE-02 |
| DS-CODE-03 | FS-CODE-03 |
| DS-CODE-04 | FS-CODE-04 |
| DS-CODE-05 | FS-CODE-05 |
| DS-TIME-01 | FS-TIME-01 |
| DS-TIME-02 | FS-TIME-02 |
| DS-TIME-03 | FS-TIME-03 |
| DS-TIME-04 | FS-TIME-04 |
| DS-TIME-05 | FS-TIME-05 |
| DS-SUB-01 | FS-SUB-01 |
| DS-SUB-02 | FS-SUB-02 |
| DS-SUB-03 | FS-SUB-03 |
| DS-SUB-04 | FS-SUB-04 |
| DS-FU-01 | FS-FU-01 |
| DS-FU-02 | FS-FU-02 |
| DS-FU-03 | FS-FU-03 |
| DS-TRD-01 | FS-TRD-01 |
| DS-TRD-02 | FS-TRD-02 |
| DS-TRD-03 | FS-TRD-03 |
| DS-TRD-04 | FS-TRD-04 |
| DS-FSCA-01 | FS-FSCA-01 |
| DS-FSCA-02 | FS-FSCA-02 |
| DS-FSCA-03 | FS-FSCA-03 |
| DS-FSCA-04 | FS-FSCA-04 |
| DS-MAUDE-01 | FS-MAUDE-01 |
| DS-MAUDE-02 | FS-MAUDE-02 |
| DS-RMF-01 | FS-RMF-01 |
| DS-RMF-02 | FS-RMF-02 |
| DS-RMF-03 | FS-RMF-03 |
| DS-EUDAMED-01 | FS-EUDAMED-01 |
| DS-EUDAMED-02 | FS-EUDAMED-02 |
| DS-NCA-BFARM-01 | FS-NCA-BFARM-01 |
| DS-NCA-SWISS-01 | FS-NCA-SWISS-01 |
| DS-NCA-AGES-01 | FS-NCA-AGES-01 |
| DS-NCA-LANG-01 | FS-NCA-LANG-01 |
| DS-COMBO-01 | FS-COMBO-01 |
| DS-COMBO-02 | FS-COMBO-02 |
| DS-INSP-01 | FS-INSP-01 |
| DS-INSP-02 | FS-INSP-02 |
| DS-INSP-03 | FS-INSP-03 |
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
| DS-DI-01 | FS-DI-01 |
| DS-DI-02 | FS-DI-02 |
| DS-DI-03 | FS-DI-03 |
| DS-DI-04 | FS-DI-04 |
| DS-DI-05 | FS-DI-05 |
| DS-DI-06 | FS-DI-06 |
| DS-SEC-01 | FS-SEC-01 |
| DS-SEC-02 | FS-SEC-02 |
| DS-SEC-03 | FS-SEC-03 |
| DS-PERF-01 | FS-PERF-01 |
| DS-AV-01 | FS-AV-01 |
| DS-BAK-01 | FS-BAK-01 |
| DS-TRN-01 | FS-TRN-01 |
| DS-TRN-02 | FS-TRN-02 |
| DS-PR-01 | FS-PR-01 |
| DS-INT-SSO-01 | FS-INT-SSO-01 |
| DS-INT-FDA-01 | FS-INT-FDA-01 |
| DS-INT-EUDAMED-01 | FS-INT-EUDAMED-01 |
| DS-INT-UDI-01 | FS-INT-UDI-01 |
| DS-INT-PV-01 | FS-INT-PV-01 |
| DS-INT-EQMS-01 | FS-INT-EQMS-01 |
| DS-INT-LIT-01 | FS-INT-LIT-01 |
| DS-INT-PMS-01 | FS-XINT-PMS-01 |

**Coverage footnote.** 100 of 106 FS-IDs covered (94%). Cross-system FS-IDs covered through DS § 7 (FS-XSYS-AD-01, FS-XSYS-BAK-01, FS-XINT-LMS-01, FS-XINT-EQMS-01/02, FS-XINT-PMS-02).

## 11. Design-level Risk Register

| ID | Design-stage risk | Likelihood | Impact | Bound DS-IDs | Mitigation |
|---|---|---|---|---|---|
| D-01 | FDA-803 + EU-Art87 decision-tree YAMLs drift between agency packs producing silent reportability divergence | Medium | High | DS-MDR-01, DS-MDR-02, DS-MDR-04 | Annual cross-agency convergence review (DS-MDR-05) |
| D-02 | IMDRF AET annual upgrade re-codes open cases incorrectly | Low | High | DS-CODE-01, DS-CODE-03 | Cut-over runbook + QC sample (DS-CODE-04) |
| D-03 | Combination-product handoff (DS-COMBO-01) loses bidirectional sync during Kafka outage | Medium | Critical | DS-COMBO-01, DS-INT-PV-01 | At-least-once delivery + idempotent by combo-id + reconciliation job |
| D-04 | Trend threshold (DS-TRD-01) over-tuned to past portfolio produces false-negative on novel device | Medium | High | DS-TRD-01, DS-TRD-04 | Annual threshold re-tune |
| D-05 | FSCA closure approved without distribution-confirmed (silent bypass) | Low | Critical | DS-FSCA-04 | Server-side validation + audit row |
| D-06 | Sparta tenant kernel patch breaks `mdr-api-guard` integration | Medium | High | DS § 8 (`mdr-api-guard`) | Regression test in OQ-MDR-PATCH-01 |
| D-07 | EUDAMED maintenance-window collision causes MIR-Trend submission timeout in Art. 88 critical window | Low | Critical | DS-EUDAMED-02, DS-TRD-02 | Window-aware scheduler + retry policy |
| D-08 | UDI-DI resolution fails (Atlas down) at intake — case stuck in Triaged | Medium | Medium | DS-INTAKE-04, DS-INT-UDI-01 | Cache TTL + `unknown` placeholder + recovery job |
| D-09 | BfArM/Swissmedic/AGES gateway cert expires during reportable window | Low | Critical | DS-NCA-BFARM-01, DS-NCA-SWISS-01, DS-NCA-AGES-01 | Cert-rotation tracker `cert-expiry-monitor` D-30 warning |
| D-10 | Sparta multi-tenant noisy-neighbour throttling extends eMDR/MIR generation P95 beyond NFR | Low | High | DS-PERF-01 | Sparta tenant SLA + Splunk SLO breach alert |
| D-11 | Audit-trail filter (DS-AUD-01) misses new FSCA-event-class introduced in MDCG 2023 revision | Medium | High | DS-AUD-01 | Annual filter-coverage review |
| D-12 | RMF hazard-linkage (DS-RMF-02) drift on RMF re-baseline — orphan AET codes | Low | High | DS-RMF-02 | Annual RMF review (DS-RMF-03) |
| D-13 | DR test pass for one hub but not for another (cross-hub coverage gap) | Low | High | DS-BAK-01, DS-AV-01 | Annual cross-hub DR drill |
| D-14 | LMS lapse blocks PRRC sign-off at clock-critical moment | Low | High | DS-TRN-01, DS § 7 (LMS) | D-30 / D-7 LMS lapse alert |
| D-15 | Combination-product classification rule (DS-COMBO-02) silently misclassifies new product | Low | Critical | DS-COMBO-02 | Product-onboarding CR review + OQ regression |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
