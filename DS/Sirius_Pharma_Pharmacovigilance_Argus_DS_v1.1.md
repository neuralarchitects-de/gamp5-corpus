---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "SIR-FS-PV-001 v1.2 (parent FS)"
  - "SIR-URS-PV-001 v1.2 (informational)"
  - "GAMP 5 (2nd ed., 2022) Cat 4 — Configuration Specification"
  - "Oracle Argus Safety 8.4.1 System Administrator Guide; Argus Interchange E2B(R3) Implementation Guide; Argus Mart Reporting User Guide; Empirica Signal User Guide"
parent_fs:
  document_number: SIR-FS-PV-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Sirius_Pharma_Pharmacovigilance_Argus_FS_v1.3.md
parent_urs:
  document_number: SIR-URS-PV-001
  version: 1.2
  file: ../../../URS/_generated/final/Pharmacovigilance_Safety_Database__Sirius_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Pharmacovigilance Safety Database — Oracle Argus Safety 8.4.1

**Document Number:** SIR-DS-PV-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** SIR-FS-PV-001 v1.2 | **Parent URS:** SIR-URS-PV-001 v1.2
**Site:** Sirius Pharma Ltd., Global Pharmacovigilance Operations, Dublin (HQ) with regional hubs in Basel (CH), München (DE), Wien (AT) *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (no site-authored custom code)
**Project Mode:** Brownfield retrofit of existing Argus 8.2 tenancy to 8.4.1 + DACH gateway uplift (per parent URS Project Mode line)
**Tier (inherited from parent URS+FS):** T4 — mission-critical multi-module
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR 314.80, 600.80, 312.32; EU GMP Annex 11 §§ 4, 6, 9, 11; ICH E2A/E2B(R3)/E2C(R2)/E2D/E2E/E2F/M1/M2; EU GVP Modules I–XVI (R2 incl. Module VI R2); EU CTR Reg. 536/2014 + CTIS; IDMP ISO 11238/11239/11240/11615/11616; EMA SPOR; FDA Computer Software Assurance (Feb 2026); BfArM, Paul-Ehrlich-Institut, Swissmedic, AGES PharmMed.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect — PV Platforms) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of PV Operations) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (QPPV) | _____________ | _____________ | _____ |
| Reviewer (Signal Management Lead) | _____________ | _____________ | _____ |
| Reviewer (Aggregate Reporting Lead) | _____________ | _____________ | _____ |
| Reviewer (Regulatory Affairs — IDMP / xEVMPD) | _____________ | _____________ | _____ |
| Reviewer (Argus DBA — Oracle 19c) | _____________ | _____________ | _____ |
| Reviewer (InfoSec / DPO) | _____________ | _____________ | _____ |
| Approver (VP Drug Safety) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |
| Approver (System Owner — Head of PV Operations) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue. Inherited Tier T4 from parent URS+FS pair. Derived from SIR-FS-PV-001 v1.2. DS covers 152/160 FS-IDs as DS-IDs; 8 FS-IDs flagged as "vendor-internal — no site design surface" (Oracle Argus core engine internals such as RPD compiler, MedDRA AutoEncoder neural backbone, Empirica EBGM statistical kernel, Argus Mart GoldenGate replication primitives, Oracle 19c Data Guard apply engine, Argus Interchange XSLT runtime; full list in Appendix A footnote). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from SIR-URS-PV-001 v1.2 and SIR-FS-PV-001 v1.2. Additional DS-specific terms:

| Term | Definition |
|---|---|
| CI | Configuration Item (an Argus configurable parameter / lookup / workflow / rule) |
| RPD | Argus Reporting Rule Definition |
| Workflow XML | Argus workflow definition serialised as XML under git change control |
| OTD | Oracle Traffic Director (HA front-end for Argus app servers) |
| ESM | Argus Enterprise Service Manager |
| Argus Interchange Profile | Per-agency E2B(R3) configuration set (XSLT + element-coverage matrix + transport credentials) |
| MedDRA AutoEncoder | Argus auto-coding component (vendor-internal — site configures dictionary version + CPT only) |
| Audit Trail Filter | Argus audit-trail-display filter (configured at admin layer) |
| Tenant-region binding | Argus database-tenant ↔ OCI-region pinning per GDPR Art. 44 |

## 1. Purpose

This Configuration Specification (CS) records the technical design choices — every configurable parameter, every configured workflow, every role-permission binding, and every integration endpoint binding — needed to implement the functional behaviour specified in `SIR-FS-PV-001` v1.2 on the Oracle Argus Safety 8.4.1 platform. The CS is the controlling input to `SIR-IQ-PV-001`, `SIR-OQ-PV-001`, `SIR-PQ-PV-001`, and `SIR-CONFIG-BASELINE-PV-001`. The CS does not redraw vendor-internal Argus code; vendor-internal design remains the responsibility of Oracle under Oracle SDLC.

## 2. Scope

**In scope.** Per-CI configuration values for Argus Safety 8.4.1 application servers, Oracle 19c EE database, Argus Mart, Argus Interchange, Empirica Signal; workflow XML; RPD reporting rules; MedDRA + WHO Drug dictionary version bindings; per-agency E2B(R3) profile XSLTs + transport credentials; role-permission matrix; SoD enforcement; tenant-region bindings; integration endpoints (Okta, Medidata Rave, Veeva Vault CTMS / eTMF / RIM, EMA SPOR + xEVMPD, EVDAS, FAERS / ESG, PMDA, CESG, BfArM, PEI, Swissmedic, AGES, literature service, partner-exchange platform); site-deployed components (reconciliation cron, gateway connectivity probe, audit-trail export job).

**Out of scope.** Argus engine internals (vendor SDLC); Oracle 19c database-engine internals (vendor SDLC); MedDRA dictionary content (MSSO); WHO Drug content (UMC); Okta IdP design (Okta vendor design); end-customer infrastructure of EUDAMED, FAERS, EVDAS, PMDA, CESG, BfArM, PEI, Swissmedic, AGES.

## 3. Architectural Overview

```
                       ┌─────────────────────────────────────────────┐
                       │  Okta IdP (SAML 2.0 + MFA — `pv-prod-users`)│
                       └────────────────────┬────────────────────────┘
                                            │
                                            ▼
   ┌─────────────────────────────────────────────────────────────────────┐
   │   OCI Frankfurt (PROD)                  OCI Zurich (DR replica)     │
   │   ┌─────────────────────────────┐       ┌─────────────────────────┐ │
   │   │ Oracle Traffic Director     │       │ Standby OTD (cold)      │ │
   │   │ `otd-pv-prod-01`            │       │                         │ │
   │   └────────────┬────────────────┘       └─────────────────────────┘ │
   │                │                                                    │
   │   ┌────────────▼────────────┐  3 active + 1 standby                 │
   │   │ Argus 8.4.1 App Servers │  load-balanced, mTLS                  │
   │   │ app-pv-01..04           │                                       │
   │   └────────────┬────────────┘                                       │
   │                │                                                    │
   │   ┌────────────▼────────────┐  Data Guard physical-standby (async) │
   │   │ Oracle 19c EE 19.20+    │◄─────────────────────────────────────┐│
   │   │ tenant `siriuspv`       │                                      ││
   │   └────────────┬────────────┘                                      ││
   │                │                                                   ││
   │   ┌────────────▼────────────┐    GoldenGate 21c                    ││
   │   │ Argus Mart (analytics)  │◄────────────────────────────────────┐││
   │   └─────────────────────────┘                                     │││
   │   ┌─────────────────────────┐    Empirica Signal                  │││
   │   │ EBGM / PRR / ROR engine │                                     │││
   │   └─────────────────────────┘                                     │││
   └─────────────────────┬──────────────────────────────────────────────┘│
                         │                                               │
              ┌──────────▼──────────┐  Argus Interchange (E2B(R3))       │
              │  per-agency profiles │                                   │
              └─┬───┬───┬───┬───┬───┬┘                                   │
                ▼   ▼   ▼   ▼   ▼   ▼                                   │
            EudraVig  FAERS  PMDA  CESG  BfArM  PEI  Swissmedic  AGES   │
            (EVDAS)   (ESG)                                              │
                                                                         │
   Medidata Rave EDC  ─┐                  ┌─►  Veeva Vault CTMS          │
   Veeva Vault eTMF   ─┼─►  Argus 8.4.1 ──┤    Veeva Vault RIM            │
   EMA SPOR / xEVMPD  ─┘   integration    └─►  Lit service / Partners    │
                           bus (Kafka                                    │
                           `pv.case.state.v1`)                           │
```

The Argus 8.4.1 tenancy `siriuspv` is deployed on OCI Frankfurt (primary) with async Data Guard physical-standby on OCI Zurich (DR). Three active app servers (`app-pv-01..03`) plus one hot-standby (`app-pv-04`) sit behind Oracle Traffic Director `otd-pv-prod-01`. Argus Mart is GoldenGate-fed from the PROD database with a 15-minute P95 latency SLO. Argus Interchange runs the per-agency E2B(R3) profiles. All operator access is via Okta SAML 2.0 + MFA against the `pv-prod-users` group; service accounts use mTLS only. Audit-trail forwarding is to Splunk index `pv-audit` with a 5-minute forwarder SLO and 50-year frozen-index retention.

## 4. Configuration Specification

The following per-CI rows record every configurable parameter that the site has chosen a value for, the chosen value, whether the value is a vendor default or a site-specific custom value, the justification, the bound FS-IDs, and the planned IQ/OQ/PQ test that verifies the design choice. CIs that the FS leaves open and the site chooses to defer to a downstream configuration runbook are flagged `deferred` in the Verified-by column and tracked in `SIR-CONFIG-DEFERRED-PV-001`.

### 4.1 Platform + Vendor + Configuration Lifecycle

| DS-ID | Configuration item (Argus / Oracle / OCI) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-PLAT-01 | Active Argus 8.4.1 application-server count | 3 (`app-pv-01..03`) + 1 hot-standby (`app-pv-04`) behind `otd-pv-prod-01` | Custom | 20% headroom over 300-concurrent-processor sizing target; matches PQ-PERF-NAV-01 envelope. | FS-PLAT-01 | IQ-PV-PLAT-01 |
| DS-PLAT-02 | Argus 8.4.1 patch baseline | 8.4.1.5 (latest SCN at baseline) | Custom | SCN.5 includes EVDAS profile fix per Oracle CR 33-xxxx; required for FS-NCA-* gateway certification. | FS-PLAT-01, FS-PLAT-05 | IQ-PV-PLAT-02 |
| DS-PLAT-03 | Oracle Database edition + version | Oracle 19c EE 19.20.0.0.0 + Apr-2026 RU | Custom | 19c EE required for Data Guard physical-standby; 19.20 is the minimum Oracle-certified Argus 8.4.1 substrate. | FS-PLAT-01 | IQ-PV-DB-01 |
| DS-PLAT-04 | Data Guard mode | Physical standby (Maximum Performance, async) | Custom | RPO ≤ 15 min achievable; sync would breach NFR-07 E2B generation P95 ≤ 10s due to commit-latency tail. | FS-PLAT-02, FS-AV-02 | OQ-DR-FAILOVER-01 |
| DS-PLAT-05 | OCI region — PROD | OCI Frankfurt (eu-frankfurt-1) | Custom | GDPR Art. 44 — EU-resident; matches DPIA-PV-2026-001 tenant-region binding. | FS-SEC-03 | IQ-PV-OCI-01 |
| DS-PLAT-06 | OCI region — DR | OCI Zurich (eu-zurich-1) | Custom | DR-region GDPR-resident; Swiss adequacy decision in force; covers DACH locality preference. | FS-PLAT-02, FS-SEC-03, FS-SEC-04 | IQ-PV-OCI-02 |
| DS-PLAT-07 | Argus configuration git repository | `gitlab.sirius.local/pv-config` (protected branch `main`, signed-commits-required) | Custom | Source-of-truth for workflow XML + RPD + per-agency profiles + role matrix. | FS-PLAT-03 | OQ-PV-CFG-GIT-01 |
| DS-PLAT-08 | Argus Mart GoldenGate replicate lag SLO | P95 ≤ 15 min (Prometheus metric `argus-mart-lag-seconds`) | Custom | Argus Mart feeds Empirica + KPI dashboards; signal-detection downstream tolerance. | FS-PLAT-04, NFR-10 | PQ-PV-MART-LAG-01 |
| DS-PLAT-09 | Argus quarterly patch + critical OOB patch workflow | Vendor RSS → Jira `PV-PATCH` → IA template `PV-CR-PATCH-IA` (14 d) → regression pack `OQ-PV-REG-PACK` → CR rollback plan | Custom | Reproduces FS-PLAT-05 workflow with named templates and named regression pack. | FS-PLAT-05, FS-VND-02 | OQ-PV-PATCH-01 |
| DS-PLAT-10 | Argus environment topology | DEV (`siriuspv-dev`) / QC (`siriuspv-qc`) / UAT (`siriuspv-uat`) / PROD (`siriuspv-prod`) | Custom | Mandatory four-env separation per CSV policy; refresh-from-PROD via Oracle Data Masking Pack template `pv-pii-mask-v3`. | FS-PLAT-06 | OQ-PV-ENV-01 |
| DS-VND-01 | Vendor assurance dossier reference | `VA-ORACLE-2026` (SOC 2 Type II + ISO 27001 + customer-shared CSV evidence) | Custom | Annual re-qualification cadence; on-boarding gate for major patches. | FS-VND-01 | OQ-PV-VND-01 |
| DS-VND-02 | Oracle release-note ingestion mechanism | RSS subscriber service `oracle-rn-poller` posting to Jira `PV-PATCH` within 24 h of vendor publication | Custom | Automation removes manual scan; SLA covers 14-day IA window. | FS-VND-02 | OQ-PV-VND-02 |
| DS-VND-03 | Oracle TR-Audit cadence | Annual; filed in `VA-ORACLE-2026/tr-audit-{year}.pdf` | Default | Aligns with Oracle's standard customer-trust report cadence. | FS-VND-03 | (deferred) |
| DS-CFG-01 | Configuration lifecycle state machine | DRAFT → REVIEW → APPROVED → EFFECTIVE; SoD-enforced (Author ≠ Approver) at APPROVED → EFFECTIVE | Custom | Implements FS-CFG-01; mirrored in workflow XML + RPD. | FS-CFG-01 | OQ-PV-CFG-LIFECYCLE-01 |
| DS-CFG-02 | Configuration export endpoint | `GET /admin/config/snapshot?product={id}` returns version-stamped JSON; archive bucket `siriuspv-cfg-archive/` with object-lock 50 y | Custom | Snapshot reproducibility for inspection retrieval. | FS-CFG-02 | OQ-PV-CFG-EXPORT-01 |
| DS-CFG-03 | Rule-engine change runbook | `SOP-PV-RULES-001` + regression case-pack `REG-CASES-2026-01` (250 cases covering FDA/EU/PMDA/CESG/BfArM/PEI/Swissmedic/AGES) | Custom | OQ-replay coverage for all jurisdictional rule changes. | FS-CFG-03 | OQ-PV-RULES-REPLAY-01 |

### 4.2 Case Intake, Triage, Workflow

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CASE-01 | Intake-adapter configuration set | Manual UI; Argus Interchange inbound; Medidata Rave SAE webservice `https://rave.medidata.com/SAEWebservice/v3` (daily 02:00 UTC); literature feed `lit-pull-weekly` (Sun 03:00 UTC); per-partner profiles in `partner-profile-registry.yaml`; patient-support REST endpoint `/intake/psp`; regulator-feedback queue `regulator-feedback-in` (Kafka) | Custom | Each intake channel matches FS-CASE-01 enumeration with named timing + named endpoint. | FS-CASE-01 | OQ-PV-INTAKE-01 |
| DS-CASE-02 | Case-id generator | Per-hub monotonic id with hub prefix: `SIR-DUB-YYYY-NNNNNN`, `SIR-BAS-YYYY-NNNNNN`, `SIR-MUC-YYYY-NNNNNN`, `SIR-WIE-YYYY-NNNNNN` | Custom | Hub-prefix enables routing + audit-trail forensic clarity. | FS-CASE-02 | OQ-PV-CASE-ID-01 |
| DS-CASE-03 | Mandatory-field server-side validation set | Intake date, awareness date, source country (ISO 3166-1), reporter type (HCP/Consumer/Other), products (≥1), seriousness (ICH E2A), expedited-eligibility flag | Custom | Reproduces ICH E2B(R3) §B mandatory matrix at intake (vs. at submission). | FS-CASE-02 | OQ-PV-CASE-VAL-01 |
| DS-CASE-04 | Workflow XML state machine | `pv-workflow-v3.xml` implementing Intake → Triaged → Coded → MedicallyAssessed → Approved → Submitted → Closed; terminal-state auto-lock; reverse-transition requires reason + e-sig + audit row | Custom | Implements FS-CASE-03 with explicit XML reference. | FS-CASE-03 | OQ-PV-WORKFLOW-01 |
| DS-CASE-05 | Reporting-clock rule pack | `clock-rules-2026-01.yaml` — FDA 7d/15d/30d (per 21 CFR 314.80(c)(1)), EU 15d/90d (per GVP VI), PMDA 7d/15d/30d, Health Canada 15d, BfArM/PEI/Swissmedic/AGES per AMG/HMG/AMG; D-3 / D-1 / D0 alert thresholds | Custom | Alert thresholds tuned to QPPV operational SLA. | FS-CASE-04 | OQ-PV-CLOCK-01 |
| DS-CASE-06 | Reclassification handler | Server-side trigger `reclassify_case_handler` on `seriousness` or `expectedness` change → re-compute clock + re-route + audit (`prev_class`, `new_class`, `reason`) | Custom | FS-CASE-05 + FS-ASSESS-05 cross-binding. | FS-CASE-05 | OQ-PV-RECLASS-01 |
| DS-CASE-07 | Follow-up delta matrix | `FOLLOWUP-DELTA-MATRIX-2026.yaml` — E2B(R3) follow-up fields per ICH E2B(R3) §D.10 + §G.k | Custom | Determines when follow-up triggers an outbound follow-up E2B. | FS-CASE-06 | OQ-PV-FU-DELTA-01 |
| DS-CASE-08 | Duplicate-detection rule set | `dedup-rules-2026.yaml` — reporter ID + patient DOB/sex + event PT + onset-date ± 7d + product hash | Custom | Tuned for low false-positive at Sirius product mix. | FS-CASE-07 | OQ-PV-DEDUP-01 |
| DS-CASE-09 | Case-priority matrix | `case-priority-matrix-2026.yaml` per product (High/Medium/Normal) | Custom | High-priority queue feeds dedicated processor team. | FS-CASE-08 | OQ-PV-PRIO-01 |
| DS-CASE-10 | Workload-balancer policy | Round-robin with hub-affinity (de-DE → MUC; fr-CH/it-CH → BAS; en → DUB; de-AT → WIE) + overflow when remaining-clock < 24h | Custom | Language-affinity reduces translation rework. | FS-CASE-09 | OQ-PV-WORKLOAD-01 |
| DS-CASE-11 | Case-state Kafka topic | `pv.case.state.v1`, partitions 12, retention 30 d, schema registry pinned | Custom | Feeds Grafana `pv-cycle-time` board. | FS-CASE-10 | OQ-PV-KAFKA-01 |

### 4.3 Coding — MedDRA + WHO Drug Lifecycle

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-CODE-01 | MedDRA AutoEncoder mode | Enabled; confidence threshold 0.85; coder review required for all suggestions | Custom | Reduces silent miscoding while keeping coder-time benefit. | FS-CODE-01 | OQ-PV-CODE-AE-01 |
| DS-CODE-02 | MedDRA hierarchy capture level | LLT (Lowest Level Term) entered; PT/HLT/HLGT/SOC auto-derived | Default | Standard MedDRA practice; preserves coder primary choice. | FS-CODE-02 | OQ-PV-MEDDRA-HIER-01 |
| DS-CODE-03 | WHO Drug coding scope | Suspect + concomitant + interacting products; ATC auto-derived from drug record number | Custom | Server-side validation block on uncoded products at Approval. | FS-CODE-03 | OQ-PV-WHODRUG-01 |
| DS-CODE-04 | MedDRA upgrade utility config | Argus MedDRA upgrade utility v8.4.1; runbook `SOP-PV-MEDDRA-UPGRADE-001`; QPPV-designee + Head-of-PV approval | Custom | Semi-annual MSSO release cycle. | FS-CODE-04 | OQ-PV-MEDDRA-UPG-01 |
| DS-CODE-05 | Open-case re-coding policy | States {Intake, Triaged, Coded} auto re-coded; {MedicallyAssessed, Approved, Submitted, Closed} preserve version-of-record; equivalent stored as `meddra_eq_v_new` | Custom | Preserves regulator-submitted version while keeping internal analytics current. | FS-CODE-05 | OQ-PV-MEDDRA-OPEN-01 |
| DS-CODE-06 | WHO Drug annual migration runbook | `SOP-PV-WHODRUG-UPGRADE-001`; ATC reassignment tracked in `wd_change_log` table | Custom | UMC annual cadence; surfaced in trending dashboards. | FS-CODE-06 | OQ-PV-WHODRUG-UPG-01 |
| DS-CODE-07 | Coding-QC sample job | Monthly; ≥ 2% of approved cases; output `coding-qc-{yyyy-mm}.csv` to Coding Manager | Custom | Discrepancy categories feed coder training (Q-PV-CODE-TRAINING). | FS-CODE-07 | OQ-PV-CODE-QC-01 |
| DS-CODE-08 | Auto-coding KPI dashboard | Grafana `pv-coding-kpi`; tiles: acceptance rate per LLT, override rate per LLT, top-overridden LLTs | Custom | Quarterly review by QPPV designee. | FS-CODE-08 | OQ-PV-CODE-KPI-01 |
| DS-CODE-09 | Company-preferred-term (CPT) table | `cpt_per_product` Argus admin table; consulted by AutoEncoder before MedDRA hierarchy | Custom | Resolves product-specific disambiguation (e.g. trade-name → SOC routing). | FS-CODE-09 | OQ-PV-CPT-01 |

### 4.4 Medical Assessment + Approval

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-ASSESS-01 | Seriousness UI checkbox set | Death; Life-threatening; Hospitalisation/prolonged; Persistent/significant disability; Congenital anomaly; Medically important; (free-text rationale optional) | Default | ICH E2A criterion-set verbatim. | FS-ASSESS-01 | OQ-PV-ASSESS-SER-01 |
| DS-ASSESS-02 | Causality UI category set | Certain / Probable / Possible / Unlikely / Conditional / Unassessable (WHO-UMC) | Default | Standard WHO-UMC categories. | FS-ASSESS-02 | OQ-PV-CAUSAL-01 |
| DS-ASSESS-03 | Expectedness UI surface | RSI version-of-record auto-surfaced at assessment time; stamped to assessment record | Custom | Prevents drift between assessor's view of RSI and version actually applied. | FS-ASSESS-03 | OQ-PV-EXPECT-01 |
| DS-ASSESS-04 | QPPV-designee re-auth policy | Okta MFA challenge max-age 5 min; HMAC-SHA-256 over (record-hash, signer-id, timestamp); SHA-256 of approval payload stored | Custom | Argus default 30-min cached creds is too permissive for QPPV signature. | FS-ASSESS-04, FS-PART11-09, FS-PART11-11 | OQ-PV-ESIG-QPPV-01 |
| DS-ASSESS-05 | Reclassification reporting-clock recompute | Trigger `recompute_reporting_clock` on reclass → audit row with old/new + recompute output | Custom | Closes R-06 (URS-level reclass-miss risk). | FS-ASSESS-05 | OQ-PV-RECLASS-CLOCK-01 |
| DS-ASSESS-06 | Dual-narrative fields | `company_narrative` + `reporter_narrative` — both preserved; edits create new version | Custom | ICH E2B(R3) §H requires both. | FS-ASSESS-06 | OQ-PV-NARR-01 |
| DS-ASSESS-07 | Paediatric auto-flag | Argus age-group derivation from DOB per ICH E11 (Pre-term, Term newborn, Infant, Child, Adolescent) | Default | ICH E11 verbatim age bands. | FS-ASSESS-07 | OQ-PV-PED-01 |
| DS-ASSESS-08 | Reviewer assignment matrix | Skills matrix table `reviewer_skills` (therapeutic area × language coverage de-DE/fr-CH/it-CH/de-AT/en) + workload module | Custom | Hub-affinity policy DS-CASE-10. | FS-ASSESS-08 | OQ-PV-ASSIGN-01 |
| DS-ASSESS-09 | Time-in-state auto-escalation | When remaining-clock < safety margin (24 h for 15-d cases; 6 h for 7-d cases) → escalate to back-up reviewer | Custom | Reproduces FS-ASSESS-09 with explicit thresholds. | FS-ASSESS-09 | OQ-PV-ESCAL-01 |

### 4.5 Submissions + Aggregate Reporting

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-SUB-01 | Per-agency E2B(R3) profile set | `agency-profile-evdas-2026`, `agency-profile-faers-2026`, `agency-profile-pmda-2026`, `agency-profile-cesg-2026` (Argus Interchange XSLT bundles) | Custom | One profile per gateway with element-coverage matrix per agency. | FS-SUB-01, FS-SUB-02 | OQ-PV-E2B-PROFILE-01 |
| DS-SUB-02 | ACK reconciliation policy | ACK-1 (transport) ≤ 60 min; ACK-2 (application) ≤ 24 h; ACK-3 (business) ≤ 30 d; reconciled to case via `submission_ack` table | Custom | Aligns with EVDAS / FAERS observed ack windows. | FS-SUB-03 | OQ-PV-ACK-01 |
| DS-SUB-03 | Negative-ack exception workflow | Argus Exception with agency-error-code map (`error-code-map-2026.yaml`); re-submission within grace; QPPV escalation via PagerDuty `pv-qppv-oncall` on breach | Custom | Implements FS-SUB-04 with named map. | FS-SUB-04 | OQ-PV-EXC-01 |
| DS-SUB-04 | Aggregate-report (PSUR/PBRER/PADER/DSUR) RPD bundles | `rpd-psur-2026-01`, `rpd-pbrer-2026-01`, `rpd-pader-2026-01`, `rpd-dsur-2026-01` (version-stamped + data-cut timestamp + SHA-256 dataset checksum) | Custom | Reproducibility for inspection. | FS-SUB-05 | OQ-PV-AGG-RPD-01 |
| DS-SUB-05 | E2B(R3) NullFlavor + omission policy | XSLT post-processor `nullflavor-cleanup.xsl` enforces no empty-element emission; sets `nullFlavor="ASKU"` / `"NI"` / `"UNK"` per ICH M2 | Custom | Eliminates downstream agency rejection on empty elements. | FS-SUB-06 | OQ-PV-NULLFLAVOR-01 |
| DS-SUB-06 | ICSR-id continuity policy | `safetyReportId` (C.1.1) stable across initial → follow-up → nullification; nullification reason captured in C.1.11 | Default | ICH E2B(R3) §C.1.8 verbatim. | FS-SUB-07 | OQ-PV-ICSR-CONT-01 |
| DS-SUB-07 | Submission throughput envelope | ≥ 500 ICSRs/hour per gateway; verified by k6 PQ script `pq-submission-k6.js` | Custom | NFR-09 + SLA peak for product-class-action mass-submission events. | FS-SUB-08 | PQ-SUBMISSION-THROUGHPUT-01 |
| DS-SUB-08 | Agency-window calendar | `agency-windows-2026.yaml` (per-agency maintenance windows); scheduler avoids windows | Custom | Reduces ACK-2 backlog on agency maintenance days. |  FS-SUB-09 | OQ-PV-AGENCY-WIN-01 |
| DS-SUB-09 | Retry policy | Exponential backoff: base 60 s, factor 2, max 16 retries (~24 h total); manual intervention after exhaustion | Custom | Tuned to gateway transient-error patterns. | FS-SUB-10 | OQ-PV-RETRY-01 |
| DS-AGG-01 | PSUR / PBRER auto-population set | Body + appendices auto-populated; exec summary + benefit-risk evaluation authored in report module (Argus Periodic Reports) | Default | ICH E2C(R2) verbatim split. | FS-AGG-01 | OQ-PV-PSUR-01 |
| DS-AGG-02 | PADER cadence per product | Quarterly first 3 y post-approval → annual thereafter (FDA 21 CFR 314.80(c)(2)) | Default | FDA verbatim cadence. | FS-AGG-02 | OQ-PV-PADER-01 |
| DS-AGG-03 | DSUR cadence + data sources | Annual per investigational product per DIBD; pulls from EDC (Medidata Rave) + Argus + CTMS (Veeva Vault CTMS) | Default | ICH E2F verbatim. | FS-AGG-03 | OQ-PV-DSUR-01 |
| DS-AGG-04 | Data-cut stamping on aggregate report | Data-cut date + MedDRA version + WHO Drug version + dataset SHA-256 stamped on every output | Custom | Reproducibility for regulator query. | FS-AGG-04 | OQ-PV-AGG-STAMP-01 |
| DS-AGG-05 | Aggregate-report signature policy | Dual signature (Author + Approver) + QPPV countersign for EU PSUR/PBRER | Custom | GVP Module VII (R2) + ICH E2C(R2). | FS-AGG-05 | OQ-PV-AGG-SIG-01 |
| DS-AGG-06 | EMA PSUR Repository transport | EMA PSUR Repository web service via `agency-profile-emapsur-2026`; legacy national fallback `legacy-national-psur-2026` flagged | Custom | Transition era; legacy off-ramp documented. | FS-AGG-06 | OQ-PV-PSUR-REPO-01 |
| DS-AGG-07 | Aggregate-report template versioning | Argus Periodic Reports template versions tracked in git `pv-config/agg-templates/`; impact assessment on template change against prior periods | Custom | Ensures comparability across reporting periods. | FS-AGG-07 | OQ-PV-AGG-TPL-01 |
| DS-AGG-08 | Aggregate-report output format | PDF/A-3 with embedded source XML (PSUR data XML + tabulations) | Custom | Long-term archival + e-readability. | FS-AGG-08 | OQ-PV-AGG-PDF-01 |

### 4.6 Signal Detection + Management

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-SIG-01 | Empirica algorithm thresholds | EBGM lower-CI ≥ 2.0; PRR ≥ 2.0 with χ² ≥ 4.0 and ≥ 3 cases; ROR lower-CI ≥ 2.0 — per drug-event-pair override matrix | Custom | Tuned against Sirius portfolio + historical FN/FP rates. | FS-SIG-01 | OQ-PV-EMP-THRESH-01 |
| DS-SIG-02 | EVDAS integration cadence | Daily 06:00 UTC pull via EMA EVDAS web service; signal alerts ingested into signal-management queue | Custom | EMA EVDAS publishes daily. | FS-SIG-02 | OQ-PV-EVDAS-01 |
| DS-SIG-03 | Qualitative-signal channel set | Aggregate-report scrutiny; regulator query; partner report; literature triage | Default | GVP Module IX list verbatim. | FS-SIG-03 | OQ-PV-SIG-QUAL-01 |
| DS-SIG-04 | Signal-management state machine | Validation → Confirmation → Prioritisation → Assessment → Recommendation → Closure (Argus Signal workflow XML `pv-sig-workflow.xml`) | Custom | GVP Module IX verbatim. | FS-SIG-04 | OQ-PV-SIG-WF-01 |
| DS-SIG-05 | Signal SoD rule | Argus role-permission: `signal_closer` group ≠ `signal_reviewer` of same signal; auto-close DISABLED | Custom | Removes pressure-driven false closures. | FS-SIG-05 | OQ-PV-SIG-SOD-01 |
| DS-SIG-06 | Signal-closure evidence-basis enforcement | Server-side validation: closure-payload must include case-ids[] + aggregate-ref + literature-ref[] | Custom | FS-SIG-06 enforced at API. | FS-SIG-06 | OQ-PV-SIG-CLOSE-01 |
| DS-SIG-07 | Labelling-change handoff | Kafka topic `pv.labelling.change.v1` → Veeva Vault RIM webhook `/rim/labelling-change` | Custom | Sirius RIM integration target. | FS-SIG-07 | OQ-PV-LBL-CHG-01 |
| DS-SIG-08 | Signal KPI dashboard | Grafana `pv-signal-kpi` tiles: time-to-validation, time-to-assessment, time-to-closure (median + P95) | Custom | Monthly QPPV review. | FS-SIG-08 | OQ-PV-SIG-KPI-01 |
| DS-SIG-09 | Signal-detection algorithm-pack git repo | `gitlab.sirius.local/pv-sigdetect` (signed tags only); validation runbook `OQ-SIG-ALGO-REVAL-01` re-run on tag bump | Custom | Reproduces FS-SIG-09 with named repo + named OQ. | FS-SIG-09 | OQ-SIG-ALGO-REVAL-01 |

### 4.7 RMP / REMS / PIP / IDMP / Literature / Partner-Exchange

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-RMP-01 | RMP commitment register | Argus RMP module per product; milestone tracker; API `/rmp/commitments` to PV system | Default | Argus standard RMP-module shape. | FS-RMP-01 | OQ-PV-RMP-01 |
| DS-RMP-02 | RMP-update trigger event list | Signal-closure outcome; regulator request; PSUR conclusion | Default | GVP Module V trigger list. | FS-RMP-02 | OQ-PV-RMP-TRIGGER-01 |
| DS-RMP-03 | REMS module config | Argus REMS module; REMS Document attached + REMS Assessment Reports schedule + REMS modification history | Default | FDA REMS standard shape. | FS-RMP-03 | OQ-PV-REMS-01 |
| DS-RMP-04 | Overdue-commitment alert engine | Alert at D-30 / D-7 / D0 to QPPV + Reg Affairs via PagerDuty `pv-rmp-oncall` | Custom | Three-tier escalation. | FS-RMP-04 | OQ-PV-RMP-ALERT-01 |
| DS-RMP-05 | Educational-material distribution tracker | Vendor-print integration `printvendor.sirius.local`; KPI tile in Grafana | Custom | Quarterly distribution KPI. | FS-RMP-05 | OQ-PV-RMP-DIST-01 |
| DS-RMP-06 | PASS plan-and-milestone tracker | Argus PASS module; feed into PSUR/PBRER input via `/pass/study-completion` | Default | GVP Module VIII. | FS-RMP-06 | OQ-PV-PASS-01 |
| DS-PIP-01 | PIP register | Per-product PIP register; modifications version-controlled in `pv-config/pip/` | Custom | EU Reg. 1901/2006. | FS-PIP-01 | OQ-PV-PIP-01 |
| DS-PIP-02 | Paediatric-flag derivation | Same as DS-ASSESS-07 (ICH E11 bands) | Default | Reuses Argus age-group derivation. | FS-PIP-02 | OQ-PV-PED-01 |
| DS-PIP-03 | PIP-PSUR / PBRER / DSUR data feed | Auto-populates paediatric sections from `pip_milestone` + `case.paediatric_flag` joined view | Custom | ICH M11 paediatric appendix. | FS-PIP-03 | OQ-PV-PIP-FEED-01 |
| DS-IDMP-01 | Product-master IDMP identifier set | ISO 11238 (substance), 11239 (dose form / unit), 11240 (UoM), 11615 (medicinal product), 11616 (pharmaceutical product) on `product` table | Custom | Reproduces FS-IDMP-01 schema. | FS-IDMP-01 | OQ-PV-IDMP-01 |
| DS-IDMP-02 | Product-master update workflow | Steward → Approver SoD-enforced (Argus role `idmp_steward` ≠ `idmp_approver`); propagation matrix `propagation-matrix.yaml` | Custom | Implements FS-IDMP-02 with named roles + matrix. | FS-IDMP-02 | OQ-PV-IDMP-FLOW-01 |
| DS-IDMP-03 | xEVMPD submission worker | XEVPRM transactions (initial/variation/nullification) via EMA xEVMPD endpoint; ack reconciliation in `xevmpd_ack` table | Default | EMA standard XEVPRM. | FS-IDMP-03 | OQ-PV-XEVMPD-01 |
| DS-IDMP-04 | IDMP drift-detection job | Quarterly cron `idmp-drift-quarterly` against EMA SPOR; impact assessment opened for any in-scope product diff | Custom | Reproduces FS-IDMP-04 cadence. | FS-IDMP-04 | OQ-PV-IDMP-DRIFT-01 |
| DS-LIT-01 | Literature surveillance feed config | Cron `lit-pull-weekly` (Sun 03:00 UTC); sources: Embase, PubMed, Arzneimittelbrief (DE), Pharmazeutische Mitteilungen (AT), Schweizerische Ärztezeitung (CH), Prescrire (FR) | Custom | DACH regional journals coverage. | FS-LIT-01 | OQ-PV-LIT-01 |
| DS-LIT-02 | Literature triage UI | Hits per strategy paginated; eligible hits → ICSR (source=`literature`) + ICH E2B(R3) §C.4 citation fields | Custom | Reproduces FS-LIT-02 with field-level mapping. | FS-LIT-02 | OQ-PV-LIT-TRIAGE-01 |
| DS-LIT-03 | Literature strategy git repo | `gitlab.sirius.local/pv-lit-strategies`; annual review workflow `SOP-PV-LIT-REVIEW-001` | Custom | Reproducibility + annual cadence. | FS-LIT-03 | OQ-PV-LIT-STRAT-01 |
| DS-LIT-04 | Literature FP/TP metric report | Monthly `lit-fp-tp-{yyyy-mm}.csv`; surfaced in Grafana `pv-lit-kpi` | Custom | Strategy tuning feedback loop. | FS-LIT-04 | OQ-PV-LIT-KPI-01 |
| DS-PEX-01 | Partner-profile registry | `partner-profile-registry.yaml` per partner — PVA / SDEA params, exchange timelines, jurisdictions, contact QPPV | Custom | Argus Interchange per-partner profile binding. | FS-PEX-01 | OQ-PV-PEX-REG-01 |
| DS-PEX-02 | Inbound idempotency key | `partner_source_case_id` deduplication key; outbound timer per PVA-stipulated timeline | Custom | Closes R-13 (duplicate-case proliferation). | FS-PEX-02 | OQ-PV-PEX-DEDUP-01 |
| DS-PEX-03 | Partner-exchange audit row | `partner_exchange_event` rows include partner-id, direction, exchange timestamp, ack status, PVA-clause reference | Custom | Inspection-grade audit chain. | FS-PEX-03 | OQ-PV-PEX-AUD-01 |
| DS-PEX-04 | Partner KPI dashboard | Grafana `pv-partner-kpi`: timeliness, % rejected, % corrected; quarterly review | Custom | Reproduces FS-PEX-04. | FS-PEX-04 | OQ-PV-PEX-KPI-01 |

### 4.8 Audit Trail + 21 CFR Part 11 + GVP + DACH NCA Gateways + Clinical-Trial Safety + DI

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUD-01 | Argus audit-trail filter | All Critical Events + Login + Logout + Approve + Reject + Reclassify + Coding-override + Signature + Workflow-transition + Config-change | Custom | Argus default filter is too narrow for Part 11 + GVP. | FS-AUD-01 | OQ-PV-AUD-FILT-01 |
| DS-AUD-02 | Argus audit-table DB role policy | `audit_event` table: only `audit-writer` Argus DB role can INSERT; UPDATE + DELETE revoked at all roles incl. DBA; DDL change requires dual-DBA approval | Custom | DB-level append-only beyond Argus app-tier. | FS-AUD-02 | OQ-PV-AUD-DB-01 |
| DS-AUD-03 | Audit-trail review job set | Case-level event-driven at approval; platform-level quarterly Splunk saved-search `pv-audit-quarterly`; evidence filed in `QA-PV-AUDIT-REVIEW-{NNN}` | Custom | QA dossier numbering scheme. | FS-AUD-03 | OQ-PV-AUD-REVIEW-01 |
| DS-AUD-04 | Audit retention tier | OCI Object Storage Archive-tier with 50-year object-lock (compliance mode); paediatric extension to life-of-product + 35 y per ICH M11 (immutable-lock) | Custom | EU 50 y minimum; paediatric extension explicit. | FS-AUD-04 | OQ-PV-AUD-RET-01 |
| DS-AUD-05 | Audit-event volume monitor | Prometheus metric `audit_events_per_minute`; alert thresholds: > 2× rolling-30d-mean (spike), < 0.5× (drop) | Custom | Both spike + drop are anomaly signals. | FS-AUD-05 | OQ-PV-AUD-VOLMON-01 |
| DS-AUD-06 | Audit-trail export endpoint | `GET /admin/audit/export?from=&to=&format={csv,json}` streaming; SHA-256 hash file `<export>.sha256` written alongside | Custom | Inspector handover with integrity check. | FS-AUD-06 | OQ-PV-AUD-EXPORT-01 |
| DS-PART11-01 | Part 11 procedural-control SOPs | `SOP-PV-VALIDATION-001`, `SOP-PV-CASE-MGMT-002`, `SOP-PV-SIGNATURE-003`; annual review in `pv-sop-review-calendar.yaml` | Custom | Implements FS-PART11-01 with named SOPs. | FS-PART11-01 | OQ-PV-SOP-01 |
| DS-PART11-02 | Copy generation set | Case PDF/A-3 rendering; E2B(R3) XML export; audit-trail CSV export; all verified under OQ | Custom | Three explicit copy channels. | FS-PART11-02 | OQ-PV-COPY-01 |
| DS-PART11-03 | Record protection tier | OCI Object Storage with Object Lock (compliance mode) — equivalent to AWS S3 Object Lock; checksum verified on read | Custom | Reproduces FS-PART11-03 substrate. | FS-PART11-03 | OQ-PV-PROT-01 |
| DS-PART11-04 | Access policy | Okta `pv-prod-users` group required; MFA enforced; service accounts mTLS-only (no password fallback) | Custom | Closes R-08 family (auth bypass). | FS-PART11-04, FS-SEC-01 | OQ-PV-ACCESS-01 |
| DS-PART11-05 | Operational audit-trail policy | Linked to DS-AUD-01..06 | Default | Cross-reference. | FS-PART11-05 | (see DS-AUD-*) |
| DS-PART11-06 | Authority-check middleware | Argus role-permission matrix + custom API guard `pv-api-guard.jar` at API layer | Custom | Defense-in-depth at app + API. | FS-PART11-06 | OQ-PV-AUTHZ-01 |
| DS-PART11-07 | Operation-manual repository | Veeva Vault QualityDocs; revisions under change control with version traceability | Custom | Vault is corporate QMS. | FS-PART11-07 | OQ-PV-MANUAL-01 |
| DS-PART11-08 | E-sig manifestation | Argus signature page renders printed name + date/time (UTC + local) + meaning enum (Review/Approve/QPPV-countersign/Submit/Close) into audit trail + PDF | Custom | § 11.50 verbatim manifestation. | FS-PART11-08 | OQ-PV-SIG-MANIF-01 |
| DS-PART11-09 | E-sig cryptographic linkage | HMAC-SHA-256 over (record-hash, signer-id, timestamp); tampered records flagged on read | Custom | § 11.70 closed-system binding. | FS-PART11-09 | OQ-PV-SIG-CRYPTO-01 |
| DS-PART11-10 | User-id uniqueness policy | Argus + Okta IdP both enforce; deactivated user-ids never reassigned (Okta policy + Argus DB unique-constraint on history) | Custom | § 11.100 verbatim. | FS-PART11-10 | OQ-PV-USERID-01 |
| DS-PART11-11 | Re-authentication on signing | OAuth2 max-age 5 min; cached creds rejected; MFA challenge required at every approval / QPPV-countersign | Custom | § 11.200 enforcement. | FS-PART11-11 | OQ-PV-REAUTH-01 |
| DS-PART11-12 | Password policy | Okta policy `pv-prod-password`: length ≥ 12; complexity (upper+lower+digit+special); MFA required; 90-day rotation; lockout 5 fails / 15 min | Custom | § 11.300 + InfoSec. | FS-PART11-12 | OQ-PV-PWD-01 |
| DS-GVP-01 | GVP Module II PSMF mapping | PSMF section 3.4 mapping document `PSMF-3.4-Sirius-2026.docx` under Vault QualityDocs | Custom | Inspection-grade PSMF linkage. | FS-GVP-01 | OQ-PV-PSMF-01 |
| DS-GVP-02 | QPPV + Deputy QPPV register | `pv-psmf-control` register; chapter-version control under Vault | Custom | GVP Module I requirement. | FS-GVP-02 | OQ-PV-QPPV-REG-01 |
| DS-GVP-03 | GVP Module IX framework binding | DS-SIG-* chain | Default | Cross-reference. | FS-GVP-03 | (see DS-SIG-*) |
| DS-GVP-04 | GVP Module XV DHCPL tracker | `dhcpl_tracker` table + Reg Affairs UI; distribution metrics quarterly | Custom | DHCPL distribution tracking. | FS-GVP-04 | OQ-PV-DHCPL-01 |
| DS-NCA-BFARM-01 | BfArM gateway profile | Endpoint `https://pv.bfarm.bund.de/gateway/v2`; profile `agency-profile-bfarm-2026`; mTLS client-cert `bfarm-client-2026.p12` (Vault `pv-gateway-certs`) | Custom | Implements FS-NCA-BFARM-01 with named cert + Vault path. | FS-NCA-BFARM-01 | OQ-PV-BFARM-01 |
| DS-NCA-PEI-01 | PEI gateway profile (biologicals) | Endpoint `https://pv.pei.de/biological/gateway`; profile `agency-profile-pei-2026`; product-master routing rule "if product_type=biological → PEI else BfArM" | Custom | Implements FS-NCA-PEI-01 with explicit routing rule. | FS-NCA-PEI-01 | OQ-PV-PEI-01 |
| DS-NCA-SWISS-01 | Swissmedic gateway profile | Per HMG / VAM; profile `agency-profile-swissmedic-2026`; CH-specific timelines `clock-rules-2026-01.yaml#swiss` | Custom | CH timelines diverge from EU. | FS-NCA-SWISS-01 | OQ-PV-SWISSMEDIC-01 |
| DS-NCA-AGES-01 | AGES PharmMed gateway profile | Per AMG (AT); profile `agency-profile-ages-2026`; AT-specific timelines | Custom | AT timelines diverge from EU. | FS-NCA-AGES-01 | OQ-PV-AGES-01 |
| DS-NCA-ROUTING-01 | NCA routing matrix | `nca-routing-matrix-2026.yaml` keyed by (country-of-incidence, product type, jurisdictional rule); routes case → EudraVigilance + applicable NCAs | Custom | Single source of routing truth. | FS-NCA-ROUTING-01 | OQ-PV-NCA-ROUTE-01 |
| DS-NCA-LANG-01 | DACH template set | de-DE, de-AT, de-CH, fr-CH, it-CH variants for FSN / DHCPL output; rendered by Argus letter-generator | Custom | Language-locale variants per DACH. | FS-NCA-LANG-01 | OQ-PV-DACH-LANG-01 |
| DS-CT-01 | SUSAR identification rule | Argus rule `susar-id-rule-2026.yaml`: trigger E2B(R3) expedited 7d (fatal/life-threat) or 15d (other) to EVDAS + FAERS + applicable jurisdictions per EU CTR 536/2014 + 21 CFR 312.32 | Custom | Reproduces FS-CT-SAFETY-01 explicitly. | FS-CT-SAFETY-01 | OQ-PV-SUSAR-01 |
| DS-CT-02 | DSUR pull source binding | Medidata Rave EDC `/rave/sae-export` + Veeva Vault CTMS `/ctms/trial-product` → Argus DSUR module; data-cut SHA-256 stamped | Custom | Cross-system data-cut reproducibility. | FS-CT-SAFETY-02 | OQ-PV-DSUR-PULL-01 |
| DS-CT-03 | CTIS safety-reporting interface | EU CTIS REST endpoint via `agency-profile-ctis-2026`; ack reconciliation in `ctis_ack` table | Custom | EU CTR 536/2014 mandatory. | FS-CT-SAFETY-03 | OQ-PV-CTIS-01 |
| DS-CT-04 | Controlled-unblinding workflow | Two-person principle (unblinder + reviewer); audit-trailed; restored-blind notice to clinical-ops via Kafka `clinical.unblind.v1` | Custom | Trial-blind integrity. | FS-CT-SAFETY-04 | OQ-PV-UNBLIND-01 |
| DS-CT-05 | EU CTR Annual Safety Report generator | Argus DSUR module per-trial annual cycle; tabulation pack reproducible via dataset checksum | Default | EU CTR mandatory. | FS-CT-SAFETY-05 | OQ-PV-EU-ASR-01 |
| DS-DI-01 | ALCOA+ Attributable | `audit_event.user_id` NOT NULL DB constraint; service-account identity in `audit_event.actor_role` | Custom | Implements FS-DI-01. | FS-DI-01 | OQ-PV-ALCOA-A-01 |
| DS-DI-02 | ALCOA+ Legible | PDF/A-3 rendering + E2B(R3) XML export verified under OQ | Default | Verbatim. | FS-DI-02 | OQ-PV-ALCOA-L-01 |
| DS-DI-03 | ALCOA+ Contemporaneous | Argus app-server NTP-synced to OCI NTP pool (stratum 2); retroactive entries flagged with `delay_reason` | Custom | Closes back-dating risk. | FS-DI-03 | OQ-PV-ALCOA-C-01 |
| DS-DI-04 | ALCOA+ Original | Source preserved unaltered; corrections recorded as new `case_version` row | Default | Argus default behaviour. | FS-DI-04 | OQ-PV-ALCOA-O-01 |
| DS-DI-05 | ALCOA+ Accurate | Reporting-clock + aggregate-extract calculations deterministic; OQ golden-test pack `golden-tests-2026-01` | Custom | Reproducibility for inspection. | FS-DI-05 | OQ-PV-ALCOA-AC-01 |
| DS-DI-06 | ALCOA+ Complete | Mandatory-field matrix enforced at submission per per-agency E2B(R3) profile | Default | Reuses DS-SUB-01 matrix. | FS-DI-06 | OQ-PV-ALCOA-COMP-01 |
| DS-DI-07 | ALCOA+ Consistent | Chronological order DB-enforced via `audit_event_ts` index + check-constraint; LLT→PT mapping consistent via MedDRA hierarchy | Custom | Closes ordering anomalies. | FS-DI-07 | OQ-PV-ALCOA-CONS-01 |
| DS-DI-08 | ALCOA+ Enduring | OCI Object Storage Archive-tier with 50-year object-lock | Default | Reuses DS-AUD-04. | FS-DI-08 | (see DS-AUD-04) |
| DS-DI-09 | ALCOA+ Available | Retrieval ≤ 4 h documented in `SOP-PV-INSPECTION-RETRIEVAL` | Custom | Inspection-grade SLA. | FS-DI-09 | OQ-PV-INSP-RETR-01 |

### 4.9 Security + Performance + Availability + Backup + Training + Periodic Review

| DS-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-SEC-01 | SSO / MFA binding | Okta SAML 2.0 + MFA; group `pv-prod-users`; FIDO2 phishing-resistant for QPPV-designee subgroup | Custom | Per FS-XSYS-AD-01 (PV-Sensitive Conditional Access). | FS-SEC-01, FS-XSYS-AD-01 | OQ-PV-SSO-01 |
| DS-SEC-02 | RBAC region-product matrix | Argus role-permission table joined to Okta groups via `okta-argus-role-map.yaml` | Custom | Aligns with regional-hub model. | FS-SEC-02 | OQ-PV-RBAC-01 |
| DS-SEC-03 | DPIA + minimisation policy | DPIA-PV-2026-001 on file; narrative-template `narr-template-2026.docx` + DLP regex policy on `case.narrative` field; SCCs `pv-scc-2026` for cross-border | Custom | GDPR Art. 35 + Art. 44. | FS-SEC-03 | OQ-PV-DPIA-01 |
| DS-SEC-04 | Tenant-region binding matrix | `tenant-region-matrix-2026.yaml`: EU cases in OCI Frankfurt; US PHI cases in OCI Ashburn (out-of-scope here); CA PIPEDA via OCI Toronto routing | Custom | Multi-jurisdiction segregation. | FS-SEC-04 | OQ-PV-TENANT-01 |
| DS-SEC-05 | Vulnerability scan cadence | Monthly Tenable Nessus scan `pv-monthly-vuln`; critical findings remediated in 30 d | Custom | Aligns with InfoSec SLA. | FS-SEC-05 | OQ-PV-VULN-01 |
| DS-SEC-06 | Pen-test cadence | Annual third-party pen-test; high/critical remediation under CR; report filed `PEN-TEST-PV-{year}.pdf` | Custom | InfoSec annual cycle. | FS-SEC-06 | OQ-PV-PENTEST-01 |
| DS-SEC-07 | DLP control | OCI DLP equivalent of Microsoft Purview; rule set `pv-dlp-2026`; bulk-export of identifiable case data requires authorised-approval workflow | Custom | Closes bulk-export risk. | FS-SEC-07 | OQ-PV-DLP-01 |
| DS-PERF-01 | App-server sizing | 4 × OCI VM Standard E4 16 OCPU 256 GB RAM (3 active + 1 hot-standby) for 300 concurrent processors + 20% headroom | Custom | PQ-PERF-NAV-01 P95 ≤ 3 s envelope. | FS-PERF-01 | PQ-PERF-NAV-01 |
| DS-PERF-02 | E2B(R3) generation envelope | Per-case P95 ≤ 10 s validated by `PQ-PERF-E2B-GEN-01` (1,000-case load) | Custom | NFR-07 + SLA. | FS-PERF-02 | PQ-PERF-E2B-GEN-01 |
| DS-PERF-03 | PSUR / PBRER extract envelope | P95 ≤ 4 h for 5-year reporting period; verified `PQ-PERF-PSUR-EXTRACT-01` | Custom | NFR-08. | FS-PERF-03 | PQ-PERF-PSUR-EXTRACT-01 |
| DS-AV-01 | Availability target | ≥ 99.5% business hours; 24×7 gateway during submission windows; uptime probes 24×7 via Splunk Synthetic | Default | NFR-02. | FS-AV-01 | OQ-PV-AV-01 |
| DS-AV-02 | DR test cadence | Annual full + quarterly partial (single hub + single gateway) without PROD downtime; reports in `RUN-DR-{NNN}` | Custom | Reproduces FS-AV-02 + FS-BAK-02/03. | FS-AV-02, FS-BAK-02, FS-BAK-03 | OQ-PV-DR-01 |
| DS-BAK-01 | Oracle backup policy | Nightly RMAN level-0 weekly + level-1 daily + continuous archived redo; retention ≥ 50 y; immutable cold storage OCI Object Lock compliance mode | Custom | EU 50 y minimum. | FS-BAK-01, FS-XSYS-BAK-01 | OQ-PV-BAK-01 |
| DS-TRN-01 | Production access training gate | LMS-recorded role-specific training + PV competency check; Medical Reviewer competency re-attested annually | Custom | LMS adapter per FS-XINT-LMS-01. | FS-TRN-01, FS-XINT-LMS-01 | OQ-PV-TRN-01 |
| DS-TRN-02 | Annual refresher | LMS course `PV-ANNUAL-2026`: GVP updates, FDA post-marketing updates, ICH revisions, EVDAS/FAERS technical changes | Custom | Course identifier. | FS-TRN-02 | OQ-PV-TRN-02 |
| DS-TRN-03 | DACH-specific training | LMS course `PV-DACH-2026`: BfArM / PEI / Swissmedic / AGES + DACH-language case-handling | Custom | DACH-language coverage. | FS-TRN-03 | OQ-PV-TRN-03 |
| DS-PR-01 | Annual periodic-review run-book | `SOP-PV-ANNUAL-REVIEW-001`; auto-collects config drift, audit-trail evidence, MedDRA/WHO Drug version, gateway connectivity, signal metrics, RMP/REMS commitments, PIP commitments, IDMP/xEVMPD recon, partner PVA, deviation summary, training currency | Custom | Signed by Head of PV Ops + QPPV + VP QA. | FS-PR-01 | OQ-PV-PR-01 |
| DS-PR-02 | Quarterly operational review | Quarterly KPI report: cycle-time, reporting-clock margin distribution, gateway ack rates; published to Vault | Custom | Cycle-time governance. | FS-PR-02 | OQ-PV-PR-02 |

## 5. Workflow + Business-Rule Design

| Workflow / rule | Steps | Role bindings | Decision points |
|---|---|---|---|
| **Case Intake → Closure** | Intake → Triaged → Coded → MedicallyAssessed → Approved → Submitted → Closed | Intake: `case_intake_clerk`; Triaged: `senior_processor`; Coded: `coder` (+ `cpt_curator` for CPT changes); MedicallyAssessed: `medical_reviewer`; Approved: `qppv_designee`; Submitted: `submission_operator`; Closed: `case_closer` (≠ `medical_reviewer`) | Reverse transitions require captured reason + e-sig + audit row. Reclassification re-fires reporting-clock recompute. |
| **MedDRA Upgrade (semi-annual)** | Impact assessment → cut-over plan → Argus MedDRA upgrade utility → re-coding (open cases) → version-of-record preservation (closed cases) → smoke test → sign-off | QPPV designee + Head of PV (approvers); Coding Manager + CSV Architect (executors); Validation Lead (reviewer) | Open-case state determines re-code path (DS-CODE-05). |
| **WHO Drug Annual Migration** | Impact assessment → ATC reassignment tracking → cut-over → trending-dashboard re-baseline | Same as MedDRA + UMC liaison | ATC delta thresholds trigger trending recalibration. |
| **Signal Validation → Closure** | Validation → Confirmation → Prioritisation → Assessment → Recommendation → Closure | `signal_reviewer` (validator + assessor) ≠ `signal_closer` (SoD); QPPV reviews monthly | Closure-payload server-side validation enforces evidence basis (DS-SIG-06). |
| **PSUR / PBRER → EMA PSUR Repository** | Data cut → RPD execution → narrative authoring → dual signature (Author + Approver) → QPPV countersign → EMA PSUR Repository submit → ack reconciliation | Aggregate Reporting Lead (Author); QPPV (Approver + countersign) | Legacy national fallback only when EMA Repository unavailable. |
| **E2B(R3) Submission + ACK Reconciliation** | Case Approved → profile XSLT → XSD validation → Argus Interchange send → ACK-1 → ACK-2 → ACK-3 reconcile → close-out | `submission_operator`; QPPV (escalation on neg-ack) | Negative ACK → Exception → re-submit within grace; escalate on breach. |
| **Audit-Trail Quarterly Review** | Splunk saved-search → discrepancy triage → CAPA where applicable → evidence file in `QA-PV-AUDIT-REVIEW-{NNN}` | System Owner; QA Reviewer; QPPV (escalation) | Anomaly threshold = > 2× rolling-30d-mean. |
| **DR Annual Full + Quarterly Partial** | Failover test → end-to-end gateway resubmission (annual full) → single hub + single gateway (quarterly partial) | DR Coordinator (Author); VP IT Compliance (Approver); QA witness | Annual full: PROD failover; quarterly partial: no PROD downtime. |

## 6. Role-Permission Matrix Design

| Role (Argus + Okta group) | Cases (intake/triage/code/assess/approve/submit/close) | Workflow transitions | Signature meanings | Aggregate reports (create/sign/approve) | Signal mgmt (validate/assess/close) | RMP / REMS | Config (RPD/profile/workflow XML) |
|---|---|---|---|---|---|---|---|
| `case_intake_clerk` | C — — — — — — | Intake → Triaged | — | — | — | — | — |
| `senior_processor` | C R — — — — — | Intake → Triaged → Coded; merge-duplicate | — | — | — | — | — |
| `coder` | — R C — — — — | Triaged → Coded | — | — | — | — | — |
| `cpt_curator` | — R — — — — — | (CPT table only) | — | — | — | — | — |
| `medical_reviewer` | — R R C — — — | Coded → MedicallyAssessed; reverse-with-reason | REVIEW | — | Validate, Assess | — | — |
| `qppv_designee` | — R R R C — — | Approve (MedicallyAssessed → Approved); reverse-with-reason | APPROVE, QPPV-COUNTERSIGN | — | — | Approve | — |
| `submission_operator` | — — — — R C — | Approved → Submitted | SUBMIT | — | — | — | — |
| `case_closer` | — — — — — R C | Submitted → Closed | CLOSE | — | — | — | — |
| `signal_reviewer` | — R R — — — — | — | REVIEW | — | Validate, Assess | — | — |
| `signal_closer` | — R R — — — — | — | CLOSE | — | Close (SoD: ≠ same-signal reviewer) | — | — |
| `aggregate_author` | — R R R R — — | — | AUTHOR | C — — | — | — | — |
| `aggregate_approver` | — R R R R — — | — | APPROVE | — R C | — | — | — |
| `idmp_steward` | — — — — — — — | — | — | — | — | — | (product master, MedDRA pin) |
| `idmp_approver` | — — — — — — — | — | APPROVE | — | — | — | (product master) |
| `csv_admin` | — — — — — — — | — | — | — | — | — | C (workflow XML, RPD, profiles — SoD: ≠ approver) |
| `csv_approver` | — — — — — — — | APPROVE-CONFIG | APPROVE | — | — | — | R (signs off configs) |
| `dba` | — — — — — — — | — | — | — | — | — | — (audit-table UPDATE/DELETE revoked — dual-control on DDL) |
| `inspector_readonly` | R R R R R R R | — | — | R R R | R R R | R | R |

Legend: `C` create; `R` read; `—` denied.

## 7. Integration Design

| Integration (per FS-IF-* / FS-INT-* / FS-XSYS-*) | Endpoint | Protocol | AuthN | Retry / error handling | Monitoring |
|---|---|---|---|---|---|
| Okta IdP | `https://sirius.okta.com/app/argus-prod/saml/metadata` | SAML 2.0 + MFA | SP-initiated; signed AuthnRequest; group `pv-prod-users` | Re-auth on 5-min token expiry; lockout after 5 fails / 15 min | Okta system log → Splunk `pv-authn` |
| EMA EudraVigilance (E2B(R3) + EVDAS) | `https://eudravigilance.ema.europa.eu/gateway/v2`, `https://evdas.ema.europa.eu/webservice/v1` | E2B(R3) over AS2 (gateway), REST (EVDAS) | mTLS client-cert `evdas-client-2026.p12` | Exponential backoff (DS-SUB-09); negative-ack Exception | Splunk `pv-evdas`; quarterly connectivity test |
| FDA FAERS / ESG | FDA ESG production endpoint | E2B(R3) via AS2 | FDA ESG cert `esg-client-2026.p12` | Same retry; FDA-specific error code map | Splunk `pv-faers` |
| PMDA Gateway | PMDA E2B(R3) endpoint | E2B(R3) via mTLS | mTLS client-cert `pmda-client-2026.p12` | Same retry; PMDA-specific code map | Splunk `pv-pmda` |
| Health Canada CESG | CESG E2B(R3) endpoint | E2B(R3) via AS2 | CESG cert `cesg-client-2026.p12` | Same retry | Splunk `pv-cesg` |
| BfArM | `https://pv.bfarm.bund.de/gateway/v2` | E2B(R3) via mTLS | `bfarm-client-2026.p12` (Vault) | Same retry; DACH-language error code map | Splunk `pv-bfarm`; quarterly connectivity test |
| Paul-Ehrlich-Institut (biologicals) | `https://pv.pei.de/biological/gateway` | E2B(R3) via mTLS | `pei-client-2026.p12` | Same retry | Splunk `pv-pei` |
| Swissmedic | per HMG / VAM endpoint | E2B(R3) via mTLS | `swissmedic-client-2026.p12` | CH-specific timelines | Splunk `pv-swissmedic` |
| AGES PharmMed | per AMG endpoint | E2B(R3) via mTLS | `ages-client-2026.p12` | AT-specific timelines | Splunk `pv-ages` |
| Medidata Rave EDC | `https://rave.medidata.com/SAEWebservice/v3` | REST + secure file | mTLS + signed JWT | Daily 02:00 UTC; missed-run alert via PagerDuty | Splunk `pv-edc` |
| Veeva Vault CTMS | `https://sirius.veevavault.com/api/v23.1/objects/study` | REST | OAuth2 + Vault API key | Idempotent reads; webhook on study-change | Splunk `pv-ctms` |
| Veeva Vault eTMF | `https://sirius.veevavault.com/api/v23.1/objects/document` | REST | OAuth2 + Vault API key | TMF Reference Model handoff | Splunk `pv-etmf` |
| EU CTIS | CTIS REST endpoint | REST | mTLS + EU-CT cert | Same retry; CTIS-specific error code map | Splunk `pv-ctis` |
| Veeva Vault RIM (labelling change) | `https://sirius.veevavault.com/api/v23.1/objects/labelling-change` | REST + Kafka `pv.labelling.change.v1` | OAuth2 | Webhook + Kafka dual-track | Splunk `pv-rim` |
| Partner-exchange platform | per-partner profile in `partner-profile-registry.yaml` | E2B(R3) per-PVA (AS2 or REST) | Per-partner cert | Idempotent by `partner_source_case_id`; outbound timer per PVA | Splunk `pv-pex` |
| Literature service | Embase + PubMed REST + regional feeds | REST + file | API key | Weekly cron `lit-pull-weekly`; missed-run alert | Splunk `pv-lit` |
| EMA SPOR | EMA SPOR REST / data files | REST + file | EMA SPOR API key | Daily diff job; quarterly drift detection | Splunk `pv-spor` |
| EMA xEVMPD | EMA xEVMPD XEVPRM web service | XEVPRM (XML over HTTPS) | EMA xEVMPD cert | ack reconciliation in `xevmpd_ack` | Splunk `pv-xevmpd` |
| Cross-system Quartz AD (per FS-XSYS-AD-01) | Entra ID OIDC + SAML 2.0 + SCIM | SAML 2.0 + MFA (FIDO2 phishing-resistant) | Entra workload-identity for service-to-service | CyberArk PAM break-glass per FS-XSYS-AD-01 | SIEM forwarding RFC 5424 → Splunk `gxp-authn` ≤ 5 min |
| Cross-system Aurora Backup (per FS-XSYS-BAK-01) | Veeam Application-Aware + Oracle RMAN | per AUR-FS-BACKUP-001 | Veeam-Oracle plug-in mTLS | RPO ≤ 4 h; RTO ≤ 4 BH; immutable S3 Object Lock + LTO-9 air-gap | Monthly QA-witnessed restore test |
| Cross-system Hydra LLM (per FS-XINT-HYD-*) | Hydra gateway VIP `https://hydra-gw.sirius.local` | REST via per-use-case ID | Hydra issued JWT + mTLS | Egress ACL `pv-argus-egress-deny-llm` blocks tenant-direct routes | Hydra audit + Splunk `pv-hydra` |
| Cross-system Helios audit publish (per FS-XINT-HEL-*) | Kafka `helios.ingest.sirius.argus.v1` | Kafka + schema registry | mTLS + schema-pinned envelope | At-least-once; idempotency `{source_system, event_id}`; Prometheus `helios_publish_lag_seconds` | Alert > 600 s |
| Cross-system LMS competence adapter (per FS-XINT-LMS-01) | `https://lms.sirius.local/lms/competence/{user_id}` | REST over mTLS | Entra workload-identity | Cache TTL 12-24 h; block gated action on `current=false` | Periodic reconciliation job |

## 8. Site-Deployed Components Design

Per § 2B.4(6): a Cat 4 system that includes site-developed code (custom integration scripts, custom reports, integration adapters) carries a mini-SDS per Cat 5 rules for those components. Sirius Pharma has classified the following items as **configuration-script** (not custom code) — they are XML / YAML / JSON only, executed by the vendor's engine, and do not require a Cat 5 sub-section:

- All workflow XML, RPD reporting rules, per-agency XSLT profiles, `clock-rules-2026-01.yaml`, `FOLLOWUP-DELTA-MATRIX-2026.yaml`, `dedup-rules-2026.yaml`, `case-priority-matrix-2026.yaml`, `nca-routing-matrix-2026.yaml`, `partner-profile-registry.yaml`, `tenant-region-matrix-2026.yaml`, `agency-windows-2026.yaml`, `error-code-map-2026.yaml`, `propagation-matrix.yaml`.

The following items are **site-developed code** (Cat 5 sub-components inside a Cat 4 system) and carry mini-SDS rows in this section:

| Site-developed component | Language / framework | Source repo / file | Interface | Dependencies | Owner | GxP-criticality |
|---|---|---|---|---|---|---|
| `oracle-rn-poller` (Oracle release-note RSS subscriber) | Python 3.11 + `feedparser` | `gitlab.sirius.local/pv-tooling/oracle-rn-poller` (`main.py`) | Posts to Jira `PV-PATCH` via REST | Jira REST API, Oracle RSS feed | PV Platforms team | R3 (operational support) |
| `pv-api-guard.jar` (authority-check middleware) | Java 17 + Spring Boot | `gitlab.sirius.local/pv-tooling/api-guard` (`AuthorityCheckFilter.java`) | HTTP servlet filter on Argus API path | Argus role-permission table (read-only); Okta JWKS endpoint | PV Platforms team | R2 (auth bypass risk) |
| `gateway-conn-probe` (quarterly gateway connectivity probe) | Python 3.11 + `httpx` | `gitlab.sirius.local/pv-tooling/gateway-probe` (`probe.py`) | mTLS handshake to each gateway endpoint; result → Splunk + `gateway_conn_probe` table | gateway cert vault paths; `nca-routing-matrix-2026.yaml` | PV Platforms team | R2 (submission readiness) |
| `audit-export-cli` (audit-trail CSV/JSON export tool) | Python 3.11 + `psycopg2` | `gitlab.sirius.local/pv-tooling/audit-export` (`cli.py`) | CLI; reads `audit_event` view; writes CSV/JSON + SHA-256 hash file | Postgres view `audit_event_ro`; Vault for DB creds | PV Platforms team | R2 (inspection retrieval) |
| `idmp-drift-quarterly` (IDMP drift-detection job) | Python 3.11 + `pandas` | `gitlab.sirius.local/pv-tooling/idmp-drift` (`drift.py`) | Cron quarterly; emits diff report to Reg Affairs | EMA SPOR API key; Argus product-master read-only view | Reg Affairs IT | R2 (variation-submission readiness) |
| `lit-pull-weekly` (literature surveillance cron) | Python 3.11 + `httpx` | `gitlab.sirius.local/pv-tooling/lit-pull` (`pull.py`) | Cron weekly; pulls per-strategy hits; writes to literature triage queue | Embase / PubMed API keys; regional feed configs | PV Operations | R3 |
| `pccp_predicate_engine` — N/A (Argus has no Cat 5 ML in this system) | — | — | — | — | — | — |

Each site-developed component carries a unit-test reference (`tests/test_*.py`), CI pipeline in GitLab (signed-commits required, Trivy scan, mandatory 2-reviewer review), and a Module Specification artefact `SIR-MS-PV-{component}-001` (downstream — out of scope for v1.0 DS).

## 9. References

**US**
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- 21 CFR 314.80 (drug post-marketing AE); 21 CFR 600.80 (biologic AE); 21 CFR 312.32 (IND safety reporting)
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026)

**EU**
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EU GVP Modules I–XVI (incl. Module VI R2 — Management and reporting of adverse reactions to medicinal products)
- EU CTR Reg. 536/2014 + CTIS
- EU MDR Reg. 2017/745 Arts. 87, 88, 89 (combination-product AEs cross-reference)
- GDPR Reg. (EU) 2016/679 Arts. 6, 9, 32, 35, 44

**International**
- ICH E2A; ICH E2B(R3); ICH E2C(R2); ICH E2D; ICH E2E; ICH E2F; ICH M1 (MedDRA); ICH M2 (ESTRI); ICH M11 (paediatric)
- ICH Q9(R1)
- IDMP ISO 11238 / 11239 / 11240 / 11615 / 11616
- ISO/IEC 27001:2022
- ISPE GAMP 5 (2nd ed., 2022); PIC/S PI 041

**DACH**
- BfArM (DE) — Stufenplan + GVP-Modul-VI national addendum
- Paul-Ehrlich-Institut (DE) — biologicals vigilance
- Swissmedic (CH) — HMG + VAM
- AGES PharmMed (AT) — AMG

**Vendor**
- Oracle — *Argus Safety 8.4.1 Configuration Reference*
- Oracle — *Argus Interchange E2B(R3) Implementation Guide*
- Oracle — *Argus Mart Reporting User Guide*
- Oracle — *Empirica Signal User Guide*
- Oracle Cloud Infrastructure — *Object Storage Object Lock + Archive Tier* documentation
- Okta — *SAML 2.0 + MFA Administrator Guide*

## 10. Appendix A — DS → FS Traceability Matrix

| DS ID | FS ID |
|---|---|
| DS-PLAT-01 | FS-PLAT-01 |
| DS-PLAT-02 | FS-PLAT-01, FS-PLAT-05 |
| DS-PLAT-03 | FS-PLAT-01 |
| DS-PLAT-04 | FS-PLAT-02 |
| DS-PLAT-05 | FS-SEC-03 |
| DS-PLAT-06 | FS-PLAT-02 |
| DS-PLAT-07 | FS-PLAT-03 |
| DS-PLAT-08 | FS-PLAT-04 |
| DS-PLAT-09 | FS-PLAT-05 |
| DS-PLAT-10 | FS-PLAT-06 |
| DS-VND-01 | FS-VND-01 |
| DS-VND-02 | FS-VND-02 |
| DS-VND-03 | FS-VND-03 |
| DS-CFG-01 | FS-CFG-01 |
| DS-CFG-02 | FS-CFG-02 |
| DS-CFG-03 | FS-CFG-03 |
| DS-CASE-01 | FS-CASE-01 |
| DS-CASE-02 | FS-CASE-02 |
| DS-CASE-03 | FS-CASE-02 |
| DS-CASE-04 | FS-CASE-03 |
| DS-CASE-05 | FS-CASE-04 |
| DS-CASE-06 | FS-CASE-05 |
| DS-CASE-07 | FS-CASE-06 |
| DS-CASE-08 | FS-CASE-07 |
| DS-CASE-09 | FS-CASE-08 |
| DS-CASE-10 | FS-CASE-09 |
| DS-CASE-11 | FS-CASE-10 |
| DS-CODE-01 | FS-CODE-01 |
| DS-CODE-02 | FS-CODE-02 |
| DS-CODE-03 | FS-CODE-03 |
| DS-CODE-04 | FS-CODE-04 |
| DS-CODE-05 | FS-CODE-05 |
| DS-CODE-06 | FS-CODE-06 |
| DS-CODE-07 | FS-CODE-07 |
| DS-CODE-08 | FS-CODE-08 |
| DS-CODE-09 | FS-CODE-09 |
| DS-ASSESS-01 | FS-ASSESS-01 |
| DS-ASSESS-02 | FS-ASSESS-02 |
| DS-ASSESS-03 | FS-ASSESS-03 |
| DS-ASSESS-04 | FS-ASSESS-04 |
| DS-ASSESS-05 | FS-ASSESS-05 |
| DS-ASSESS-06 | FS-ASSESS-06 |
| DS-ASSESS-07 | FS-ASSESS-07 |
| DS-ASSESS-08 | FS-ASSESS-08 |
| DS-ASSESS-09 | FS-ASSESS-09 |
| DS-SUB-01 | FS-SUB-01 |
| DS-SUB-02 | FS-SUB-03 |
| DS-SUB-03 | FS-SUB-04 |
| DS-SUB-04 | FS-SUB-05 |
| DS-SUB-05 | FS-SUB-06 |
| DS-SUB-06 | FS-SUB-07 |
| DS-SUB-07 | FS-SUB-08 |
| DS-SUB-08 | FS-SUB-09 |
| DS-SUB-09 | FS-SUB-10 |
| DS-AGG-01 | FS-AGG-01 |
| DS-AGG-02 | FS-AGG-02 |
| DS-AGG-03 | FS-AGG-03 |
| DS-AGG-04 | FS-AGG-04 |
| DS-AGG-05 | FS-AGG-05 |
| DS-AGG-06 | FS-AGG-06 |
| DS-AGG-07 | FS-AGG-07 |
| DS-AGG-08 | FS-AGG-08 |
| DS-SIG-01 | FS-SIG-01 |
| DS-SIG-02 | FS-SIG-02 |
| DS-SIG-03 | FS-SIG-03 |
| DS-SIG-04 | FS-SIG-04 |
| DS-SIG-05 | FS-SIG-05 |
| DS-SIG-06 | FS-SIG-06 |
| DS-SIG-07 | FS-SIG-07 |
| DS-SIG-08 | FS-SIG-08 |
| DS-SIG-09 | FS-SIG-09 |
| DS-RMP-01 | FS-RMP-01 |
| DS-RMP-02 | FS-RMP-02 |
| DS-RMP-03 | FS-RMP-03 |
| DS-RMP-04 | FS-RMP-04 |
| DS-RMP-05 | FS-RMP-05 |
| DS-RMP-06 | FS-RMP-06 |
| DS-PIP-01 | FS-PIP-01 |
| DS-PIP-02 | FS-PIP-02 |
| DS-PIP-03 | FS-PIP-03 |
| DS-IDMP-01 | FS-IDMP-01 |
| DS-IDMP-02 | FS-IDMP-02 |
| DS-IDMP-03 | FS-IDMP-03 |
| DS-IDMP-04 | FS-IDMP-04 |
| DS-LIT-01 | FS-LIT-01 |
| DS-LIT-02 | FS-LIT-02 |
| DS-LIT-03 | FS-LIT-03 |
| DS-LIT-04 | FS-LIT-04 |
| DS-PEX-01 | FS-PEX-01 |
| DS-PEX-02 | FS-PEX-02 |
| DS-PEX-03 | FS-PEX-03 |
| DS-PEX-04 | FS-PEX-04 |
| DS-AUD-01 | FS-AUD-01 |
| DS-AUD-02 | FS-AUD-02 |
| DS-AUD-03 | FS-AUD-03 |
| DS-AUD-04 | FS-AUD-04 |
| DS-AUD-05 | FS-AUD-05 |
| DS-AUD-06 | FS-AUD-06 |
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
| DS-PART11-11 | FS-PART11-11 |
| DS-PART11-12 | FS-PART11-12 |
| DS-GVP-01 | FS-GVP-01 |
| DS-GVP-02 | FS-GVP-02 |
| DS-GVP-03 | FS-GVP-03 |
| DS-GVP-04 | FS-GVP-04 |
| DS-NCA-BFARM-01 | FS-NCA-BFARM-01 |
| DS-NCA-PEI-01 | FS-NCA-PEI-01 |
| DS-NCA-SWISS-01 | FS-NCA-SWISS-01 |
| DS-NCA-AGES-01 | FS-NCA-AGES-01 |
| DS-NCA-ROUTING-01 | FS-NCA-ROUTING-01 |
| DS-NCA-LANG-01 | FS-NCA-LANG-01 |
| DS-CT-01 | FS-CT-SAFETY-01 |
| DS-CT-02 | FS-CT-SAFETY-02 |
| DS-CT-03 | FS-CT-SAFETY-03 |
| DS-CT-04 | FS-CT-SAFETY-04 |
| DS-CT-05 | FS-CT-SAFETY-05 |
| DS-DI-01 | FS-DI-01 |
| DS-DI-02 | FS-DI-02 |
| DS-DI-03 | FS-DI-03 |
| DS-DI-04 | FS-DI-04 |
| DS-DI-05 | FS-DI-05 |
| DS-DI-06 | FS-DI-06 |
| DS-DI-07 | FS-DI-07 |
| DS-DI-08 | FS-DI-08 |
| DS-DI-09 | FS-DI-09 |
| DS-SEC-01 | FS-SEC-01 |
| DS-SEC-02 | FS-SEC-02 |
| DS-SEC-03 | FS-SEC-03 |
| DS-SEC-04 | FS-SEC-04 |
| DS-SEC-05 | FS-SEC-05 |
| DS-SEC-06 | FS-SEC-06 |
| DS-SEC-07 | FS-SEC-07 |
| DS-PERF-01 | FS-PERF-01 |
| DS-PERF-02 | FS-PERF-02 |
| DS-PERF-03 | FS-PERF-03 |
| DS-AV-01 | FS-AV-01 |
| DS-AV-02 | FS-AV-02 |
| DS-BAK-01 | FS-BAK-01 |
| DS-TRN-01 | FS-TRN-01 |
| DS-TRN-02 | FS-TRN-02 |
| DS-TRN-03 | FS-TRN-03 |
| DS-PR-01 | FS-PR-01 |
| DS-PR-02 | FS-PR-02 |

**Coverage footnote.** 152 of 160 FS-IDs covered as DS-IDs (95%). Vendor-internal FS-IDs not designed at site level: FS-INT-MLFLOW-01-equivalent vendor-specific Argus internals are not redrawn; Argus integration interface entries (FS-XSYS-AD-01, FS-XSYS-BAK-01, FS-XINT-HYD-01..05, FS-XINT-HEL-01..02, FS-XINT-LMS-01) are covered through DS § 7 integration design rows rather than per-DS-ID rows. FS-BAK-02 + FS-BAK-03 are subsumed under DS-AV-02 (DR test cadence).

## 11. Design-level Risk Register

| ID | Design-stage risk | Likelihood | Impact | Bound DS-IDs | Mitigation reference |
|---|---|---|---|---|---|
| D-01 | Per-agency E2B(R3) XSLT profile drift between agency profile bundles silently produces semantic divergence on a small number of fields | Medium | High | DS-SUB-01, DS-CFG-03 | OQ-PV-RULES-REPLAY-01 + per-agency element-coverage matrix |
| D-02 | OCI Frankfurt + OCI Zurich are the same vendor cloud — concurrent region outage = full PV outage | Low | Critical | DS-PLAT-05, DS-PLAT-06 | DR runbook + manual sub-failover to second cloud (out of scope v1.0) |
| D-03 | Argus 8.4.1.5 patch baseline pin becomes unsupportable at 8.4.1 EOL | Medium | High | DS-PLAT-02 | Annual Oracle TR-Audit (DS-VND-03) + roadmap monitoring |
| D-04 | NCA routing-matrix mis-classification of biological product → routed to BfArM instead of PEI | Low | Critical | DS-NCA-PEI-01, DS-NCA-ROUTING-01 | Product-master `product_type` field enforced + OQ test in `OQ-PV-NCA-ROUTE-01` |
| D-05 | Audit-trail filter (DS-AUD-01) inadvertently omits a new GVP-mandated event class on Argus version bump | Medium | High | DS-AUD-01 | Annual filter-coverage review against current GVP module list |
| D-06 | `pv-api-guard.jar` (site-developed) breaks Argus REST contract on Argus patch bump | Medium | Medium | DS § 8 (`pv-api-guard.jar`) | Regression test in OQ-PV-PATCH-01 |
| D-07 | Cross-system Hydra LLM use-case approval drift produces 403 at submission-timer-critical window | Low | Critical | DS § 7 (Hydra) | Pre-prod Annex IV pack validation; Hydra gate freshness alert |
| D-08 | Tenant-region binding (DS-SEC-04) misclassifies a CH case as EU and ships to Frankfurt instead of Zurich | Low | High | DS-SEC-04 | Country-of-incidence validation + DLP residency rule |
| D-09 | Re-coding of open cases (DS-CODE-05) at MedDRA version cut-over produces an LLT-without-PT residual | Low | High | DS-CODE-05 | Argus MedDRA upgrade utility OQ + cut-over QC |
| D-10 | Signal-detection threshold (DS-SIG-01) over-tuned for known products fails for novel safety profile | Medium | High | DS-SIG-01 | Annual threshold re-tune (OQ-SIG-ALGO-REVAL-01) |
| D-11 | `audit_event.user_id` NOT NULL constraint is bypassed by emergency DBA insert (DBA dual-control failure) | Low | Critical | DS-DI-01, DS-AUD-02 | DBA dual-control + Splunk forwarder anomaly alert |
| D-12 | `partner-profile-registry.yaml` PVA timeline change is not propagated to outbound timer in Argus | Medium | High | DS-PEX-01, DS-PEX-02 | CR review + OQ partner-exchange regression |
| D-13 | EVDAS cert (`evdas-client-2026.p12`) expires inside expedited-submission window | Low | Critical | DS § 7 EudraVigilance | Cert-rotation tracker `cert-expiry-monitor`; D-30 warning |
| D-14 | `nca-routing-matrix-2026.yaml` change reviewed at CR but XSD-validation not re-run for affected profile | Low | High | DS-NCA-ROUTING-01, DS-SUB-01 | CR template requires per-profile XSD-validation run before merge |
| D-15 | Splunk frozen-index 50-year retention cost overrun forces silent tier-downshift | Low | Critical | DS-AUD-04 | Annual storage-cost review + Vault QA dossier sign-off |
| D-16 | LMS competence adapter (`current=false`) blocks a legitimate QPPV-designee approval at clock-critical moment | Low | High | DS § 7 (LMS), DS-TRN-01 | LMS lapse alert D-30 / D-7 |
| D-17 | Veeam application-aware backup misses Oracle archived-redo gap during Data Guard apply-lag spike | Low | High | DS-BAK-01 | Monthly QA-witnessed restore test + Data Guard apply-lag P95 monitor |
| D-18 | Argus Mart GoldenGate lag P95 > 15 min during signal-detection daily run produces stale Empirica input | Medium | Medium | DS-PLAT-08 | Lag-probe alert + signal-rerun policy |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
