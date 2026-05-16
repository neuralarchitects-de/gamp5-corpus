---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (Cat 4 / Tier T3)"
seed_corpus_basis:
  - "TET-FS-DCS-001 v1.2 (parent FS)"
  - "TET-URS-DCS-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd Edition) Category 4 — Configuration Specification conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "21 CFR Part 211 §§ .22, .68, .180, .192"
  - "EU GMP Annex 11; Annex 1 (2022 revision); Annex 15"
  - "ISA-88; ISA-95; ISA-101; ISA-18.2; ISA-50.02"
  - "IEC 61508; IEC 61511; NAMUR NA 102, NE 33, NA 65, NE 159, NE 153, NE 124"
  - "PIC/S PI 041; ISPE GAMP GPG Process Control Systems"
parent_fs:
  document_number: TET-FS-DCS-001
  version: "1.2"
  file: "../../../FS_FDS/_generated/final/Tethys_Pharma_DCS_DeltaV_FS_v1.3.md"
parent_urs:
  document_number: TET-URS-DCS-001
  version: "1.2"
  file: "../../../URS/_generated/final/DCS_Distributed_Control_System__Tethys_Pharma_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## DCS — Emerson DeltaV v15.3 (Bioprocess Suite)

**Document Number:** TET-DS-DCS-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** TET-FS-DCS-001 v1.2
**Parent URS:** TET-URS-DCS-001 v1.2 *(informational, transitive)*
**Site:** Tethys Pharma S.A., Biologics Drug Substance Plant 1, Lyon, France *(fictional)*
**System Owner:** Process Automation Lead
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (Emerson DeltaV v15.3), with site-authored phase logic + master recipes treated as Cat 5 sub-components (mini-SDS in § 8)
**Project Mode:** Configuration project on commercial software product **Emerson DeltaV v15.3 (Bioprocess Suite)** (GAMP 5 Category 4) with embedded Cat-5 site phase logic + master recipes under hybrid governance.
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .22, .68, .180, .192; EU GMP Annex 11; Annex 1 (2022 revision); Annex 15; ICH Q9(R1); ICH Q10; ICH Q11; ISA-88; ISA-95; ISA-101; ISA-18.2; IEC 61508; IEC 61511; NAMUR NA 102 / NE 33 / NA 65 / NE 159 / NE 153 / NE 124; PIC/S PI 041.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect — DCS) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Process Automation Lead) | _____________ | _____________ | _____ |
| Reviewer (Functional Safety Engineer — IEC 61511) | _____________ | _____________ | _____ |
| Reviewer (DCS Engineering Manager) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Security Architect — OT) | _____________ | _____________ | _____ |
| Approver (System Owner — Process Automation Lead) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Design Control

- **Document Number:** TET-DS-DCS-001
- **Version:** 1.1
- **Effective Date:** 2026-05-15 *(synthetic)*
- **Parent FS:** TET-FS-DCS-001 v1.2
- **Parent URS:** TET-URS-DCS-001 v1.2 *(informational)*
- **Site:** Tethys Pharma S.A., Plant DSP1, Lyon, France
- **System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (DeltaV v15.3) with embedded Cat-5 phase logic + master recipes
- **Project Mode:** Hybrid Cat 4 + Cat 5 — § 4–§ 7 CS rules; § 8 mini-SDS for site phase logic
- **Regulatory Scope:** as above

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T3 from parent URS+FS pair. DS covers 87/87 FS-IDs from TET-FS-DCS-001 v1.2. No FS-IDs flagged vendor-internal — DeltaV configuration surface fully site-designable; SIS partition vendor-validated (SIL 2) but configuration of bypass workflow, proof-test plan, and event mirroring is site-designed and covered here. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from TET-FS-DCS-001 and TET-URS-DCS-001. DS-specific terms:

| Term | Definition |
|---|---|
| ProfessionalPLUS | DeltaV engineering workstation |
| ApplicationStation | DeltaV application/integration node |
| OperatorStation | DeltaV HMI client |
| Configuration DB | DeltaV ConfigExport-managed master configuration database |
| Phase Class | ISA-88 phase template (Cat-5 site code) |
| FF | Foundation Fieldbus (ISA-50.02) |
| CHARM | Characterizable Module — DeltaV I/O type |
| `dvdiff` | DeltaV ConfigExport diff tool |

---

## 1. Purpose

This DS specifies the technical design that satisfies the FS `TET-FS-DCS-001` v1.2. It records the DeltaV v15.3 Configuration Items, ISA-88 batch state-machine + alarm-rationalisation workflow design, role-permission matrix, integration design (PAS-X, Aspen IP.21, BMS, Foundation Fieldbus, HART, WirelessHART, AD), and a mini-SDS for the site-authored phase logic + master recipes. Controlling input to the IQ / OQ / PQ protocols and the RTM `TET-RTM-DCS-001`.

## 2. Scope

**In scope.** Configuration of DeltaV ProfessionalPLUS + 2 ApplicationStations (redundant) + 12 OperatorStations + 24 controllers (redundant pairs) + DeltaV SIS logic-solver pair (SIL 2, 1oo2D); DeltaV Operate + DeltaV Live HMI; alarm-rationalisation table; integrations with Werum PAS-X v3.2, Aspen IP.21, Site BMS, Foundation Fieldbus H1, HART 7, WirelessHART, AD `tethys.local`; site-developed phase logic + master/site/control recipes.

**Out of scope.** Vendor-internal DeltaV source code; SIS internal safety firmware (vendor-validated under IEC 61511 — black-box treatment, only the exposed configuration interface is recorded here); physical plant equipment; downstream IQ/OQ/PQ protocols (referenced only).

## 3. Architectural Overview

### 3.1 Topology (text)

```
        ┌─────────────────────────────────────────────────────────┐
        │  AD/PKI (tethys.local) │ PTP IEEE 1588 grandmaster        │
        └────────────────────┬────────────────────────────────────┘
                             │ LDAPS / Kerberos / PTP
                             ▼
   ┌───────────────────────────────────────────────────────────────────┐
   │              DCS Process-Control VLAN (NAMUR NE 153 zone)          │
   │  ┌──────────────────┐  ┌──────────────────┐                       │
   │  │ ProfessionalPLUS │  │ ApplicationStation│  ◄── redundant pair  │
   │  │ (engineering)    │  │ (recipe / report) │                       │
   │  └────────┬─────────┘  └────────┬─────────┘                       │
   │           │ Config DB           │ runtime                          │
   │           └──────────┬──────────┘                                  │
   │                      ▼                                              │
   │  ┌────────────────────────────────────────────────────────────┐   │
   │  │ Operator Stations (×12) — DeltaV Operate + DeltaV Live      │   │
   │  └──────────────────────┬─────────────────────────────────────┘   │
   │                          │ Fault-tolerant Ethernet ring (RSTP/PRP) │
   │   ┌──────────────────────┴────────────────────────────┐           │
   │   ▼                      ▼              ▼              ▼           │
   │ Controllers (×24,    SIS logic-       Phase logic   I/O cards     │
   │ redundant pairs)     solvers (SIL 2,  (Cat 5 site)  (CHARMs)      │
   │                      1oo2D)                                        │
   │   │                                                                │
   │   ▼                                                                │
   │ FF H1 / HART 7 / WirelessHART (ISA-50.02 + NAMUR NE 124)           │
   └────────┬───────────────┬───────────────┬────────────┬─────────────┘
            │               │               │            │
            ▼               ▼               ▼            ▼
        PAS-X v3.2     Aspen IP.21      Site BMS    MasterControl
        (recipe /      (historian)      (utility    eQMS (deviation)
         batch)                          interlock)
```

### 3.2 Cluster Design Choices

- **App Servers:** redundant ProfessionalPLUS + ApplicationStation pair; auto-promotion on failure
- **Controllers:** 24 controllers configured as redundant pairs; bumpless transfer ≤ 1 s (FS-RDN-01)
- **SIS:** DeltaV SIS logic-solver pair, 1oo2D voting, SIL 2 per IEC 61511; isolated SIS network from BPCS
- **I/O network:** ring topology with RSTP / PRP / HSR; single-fault tolerance
- **PTP:** IEEE 1588 grandmaster + boundary clocks; skew exporter `dcs_ptp_skew_milliseconds`

---

## 4. Configuration Specification

Per-CI rows enumerate every configurable parameter. Vendor source-code internals (DeltaV runtime, SIS embedded firmware) are NOT redrawn. Site-developed phase logic + master/site/control recipes appear here as configuration anchors and are detailed in § 8 (mini-SDS).

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-DCS-01 | DeltaV > System > Redundancy Mode | redundant ProfessionalPLUS + ApplicationStation pair; 24 controllers as redundant pairs; 12 OpStations on fault-tolerant Ethernet ring | Custom | FS-PLAT-01 — redundancy posture | FS-PLAT-01 | OQ `TET-OQ-REDUND-01` |
| DS-DCS-02 | DeltaV > Network > Process-Control VLAN | dedicated VLAN; firewall + DMZ per NAMUR NE 153; allow-list documented in `dcs_zone_model.yaml` | Custom | FS-PLAT-02 — NAMUR NE 153 zone model | FS-PLAT-02 / FS-SEC-04 | IQ `TET-IQ-NET-01` |
| DS-DCS-03 | UPS Hold Time | ≥ 30 min for BPCS; SIS logic-solvers on isolated UPS branch | Custom | FS-PLAT-03 — UPS sizing | FS-PLAT-03 | IQ `TET-IQ-UPS-01` |
| DS-DCS-04 | PTP IEEE 1588 > Grandmaster + Boundary Clocks | enabled; skew Prometheus exporter `dcs_ptp_skew_milliseconds`; > 1 s → alarm | Custom | FS-PLAT-04 — PTP topology | FS-PLAT-04 | OQ `TET-OQ-PTP-01` |
| DS-DCS-05 | Firmware Update Governance | Emerson + site CR + IEC 61511 FSM procedure for SIS firmware | Custom | FS-PLAT-05 — firmware change control | FS-PLAT-05 | (governance) |
| DS-DCS-06 | Controller Pair > Bumpless Transfer | enabled; failover < 1 s per Emerson reference | Default | FS-RDN-01 — failover < 1 s | FS-RDN-01 | OQ `TET-OQ-CTRL-FAILOVER-01` |
| DS-DCS-07 | ApplicationStation Pair > Shared-State Replication | enabled; VIP for HMI session reconnect | Custom | FS-RDN-02 — shared state | FS-RDN-02 | OQ `TET-OQ-APP-FAILOVER-01` |
| DS-DCS-08 | I/O Network > Ring Topology | RSTP + PRP + HSR per Emerson reference | Custom | FS-RDN-03 — single-fault tolerance | FS-RDN-03 | OQ `TET-OQ-IO-RING-01` |
| DS-DCS-09 | DeltaV SIS > Voting | 1oo2D logic-solver pair; SIL 2 per IEC 61511 | Custom | FS-RDN-04 / FS-SIS-01 — SIS voting + SIL | FS-RDN-04, FS-SIS-01 | OQ `TET-OQ-SIS-VOTE-01` |
| DS-DCS-10 | DeltaV > Faceplate `gw-cluster-health` | configured; sources `failover_events` table | Custom | FS-RDN-05 — failover surfacing | FS-RDN-05 | OQ `TET-OQ-FACE-CLUSTER-01` |
| DS-DCS-11 | DeltaV Batch > Recipe Lifecycle | states `DRAFT / REVIEW / APPROVED / EFFECTIVE / OBSOLETE`; signature-gated transitions | Custom | FS-REC-01 — recipe lifecycle | FS-REC-01 | OQ `TET-OQ-REC-STATES-01` |
| DS-DCS-12 | Recipe `master / site / control` Hierarchy | `recipe_xref` table with FK pinned across levels; version-pinned | Custom | FS-REC-02 — ISA-88 hierarchy | FS-REC-02 | OQ `TET-OQ-REC-HIER-01` |
| DS-DCS-13 | PAS-X Recipe Receiver > Schema | SHA-256 + version validated; mismatch rejects with HTTP 409 + deviation | Custom | FS-REC-03 / FS-INT-PASX-01 — checksum + version | FS-REC-03, FS-INT-PASX-01 | OQ `TET-OQ-REC-CKSUM-01` |
| DS-DCS-14 | Recipe Transition Endpoint | signed JWT payload; SoD via role matrix | Custom | FS-REC-04 — JWT + SoD | FS-REC-04 | OQ `TET-OQ-REC-JWT-01` |
| DS-DCS-15 | Recipe APPROVAL > Phase-Logic-Version Check | verifies referenced phase versions exist + are APPROVED; broken refs → `RECIPE_BROKEN_REFS` | Custom | FS-REC-05 — broken-refs gate | FS-REC-05 | OQ `TET-OQ-REC-PHL-REF-01` |
| DS-DCS-16 | DB Trigger `recipe_versions_immutable_when_effective` | UPDATE/DELETE blocked when status='EFFECTIVE' | Custom | FS-REC-06 — immutability | FS-REC-06 | OQ `TET-OQ-REC-IMMUT-01` |
| DS-DCS-17 | Physical Model Table | `physical_model` per ISA-88 Part 2 (Unit / EquipmentModule / ControlModule) | Custom | FS-REC-07 — physical model | FS-REC-07 | OQ `TET-OQ-PMOD-01` |
| DS-DCS-18 | Phase Logic Cat-5 SDLC | `TET-SOP-IT-CAT5-PHL-001` — CI gates: review + unit + integration + simulation | Custom | FS-PHL-01 — Cat-5 SDLC | FS-PHL-01 | (governance) + CI |
| DS-DCS-19 | Phase Deployment Gate | green regression-test run on simulator + approved CR | Custom | FS-PHL-02 — deployment gate | FS-PHL-02 | (CI) |
| DS-DCS-20 | DeltaV Version Control > Commit Signing | cryptographically linked authorship | Custom | FS-PHL-03 — signed commits | FS-PHL-03 | (CI) |
| DS-DCS-21 | ISA-88 Phase State Model | `IDLE / RUNNING / HELD / RESTARTING / STOPPING / STOPPED / ABORTING / ABORTED / COMPLETE`; deterministic transitions | Custom | FS-PHL-04 — state model | FS-PHL-04 | OQ `TET-OQ-PHL-SM-01` |
| DS-DCS-22 | Phase Metadata > Safe-State Declarations | `safe_state_on_utility_loss`, `safe_state_on_sis_demand`, `safe_state_on_abort` required + validated at APPROVAL | Custom | FS-PHL-05 — safe-state metadata | FS-PHL-05 | OQ `TET-OQ-PHL-SAFE-01` |
| DS-DCS-23 | Prometheus Exporters (phase) | `phase_duration_seconds`, `phase_state_transitions_total` | Custom | FS-PHL-06 — observability | FS-PHL-06 | (CI) |
| DS-DCS-24 | PAS-X Order Ingestion | transactional; partial creation rolled back | Custom | FS-BAT-01 — transactional ingestion | FS-BAT-01 | OQ `TET-OQ-ORD-TRANS-01` |
| DS-DCS-25 | `StepOrderingGuard` | enforces master-recipe step order; override requires signed reason | Custom | FS-BAT-02 — step ordering | FS-BAT-02 | OQ `TET-OQ-STEP-ORDER-01` |
| DS-DCS-26 | Critical-Step Dual-Sign Workflow `criticalStepVerify` | mandatory second-person verification | Custom | FS-BAT-03 — dual-sign on critical | FS-BAT-03 | OQ `TET-OQ-DUAL-SIG-01` |
| DS-DCS-27 | CPP Historian Logging | 1 Hz to Aspen IP.21 | Custom | FS-BAT-04 — CPP 1 Hz | FS-BAT-04 | OQ `TET-OQ-CPP-LOG-01` |
| DS-DCS-28 | Override Workflow | Operator + Senior Operator dual-sign + reason ≥ 10 chars | Custom | FS-BAT-05 — override workflow | FS-BAT-05 | OQ `TET-OQ-OVR-01` |
| DS-DCS-29 | Abort Sequence | recipe-defined safe-state procedure; logged | Custom | FS-BAT-06 — abort | FS-BAT-06 | OQ `TET-OQ-ABORT-01` |
| DS-DCS-30 | Continuous-Control Modules | PID + cascade + ratio + feed-forward on redundant controllers; bumpless | Custom | FS-BAT-07 — continuous control | FS-BAT-07 | OQ `TET-OQ-CONT-CTRL-01` |
| DS-DCS-31 | Alarm-Rationalisation File | `alarm_rationalisation.xlsx` (controlled doc) — classifies INFO/WARNING/CRITICAL/SIS + response + ack + escalation | Custom | FS-ALM-01 — alarm rationalisation | FS-ALM-01 | OQ `TET-OQ-ALARM-RAT-01` |
| DS-DCS-32 | Critical-Alarm Ack Policy | reason ≥ 10 chars; unack > T_escalate → SMS + email on-call | Custom | FS-ALM-02 — critical ack | FS-ALM-02 | OQ `TET-OQ-ALARM-ACK-01` |
| DS-DCS-33 | Alarm Philosophy Document | `TET-AP-DCS-01`; annual review under PR-01 | Custom | FS-ALM-03 — alarm philosophy | FS-ALM-03 | (governance) |
| DS-DCS-34 | Prometheus Alarm-Rate Exporter | per-operator/h, peak rate, top-talkers, standing-alarm count, flood freq | Custom | FS-ALM-04 — observability | FS-ALM-04 | OQ `TET-OQ-ALARM-METRICS-01` |
| DS-DCS-35 | Shelving Function | reason capture + max-shelve-duration + auto-revert on expiration; logged | Custom | FS-ALM-05 — shelving | FS-ALM-05 | OQ `TET-OQ-SHELVE-01` |
| DS-DCS-36 | DeltaV SIS Event Recorder | events to SIS event recorder + mirrored to audit trail (one-way) | Custom | FS-SIS-01 — SIS event mirroring | FS-SIS-01 | OQ `TET-OQ-SIS-AUDIT-01` |
| DS-DCS-37 | Proof-Test Plan | `TET-SIS-PT-PLAN-001`; cadence per demand-rate; records in `sis_proof_test_records` | Custom | FS-SIS-02 — proof-test plan | FS-SIS-02 | OQ `TET-OQ-PT-PLAN-01` |
| DS-DCS-38 | SIS Bypass Workflow | FSE + FSE Approver dual-sign + duration timer + auto-revert | Custom | FS-SIS-03 — bypass workflow | FS-SIS-03 | OQ `TET-OQ-SIS-BYPASS-01` |
| DS-DCS-39 | Annual PFDavg Recalculation | per NA 65 / NE 159; result reviewed at PR-01 | Custom | FS-SIS-04 — PFDavg cadence | FS-SIS-04 | (governance) |
| DS-DCS-40 | DeltaV Operate + Live > Screen Hierarchy | ISA-101 Level 1-4; navigation budget ≤ 3 clicks | Custom | FS-HMI-01 — ISA-101 hierarchy | FS-HMI-01 | OQ `TET-OQ-HMI-NAV-01` |
| DS-DCS-41 | HMI Palette | greys normal; saturated abnormal; red=critical, amber=warning, blue=info, magenta=SIS | Custom | FS-HMI-02 — palette | FS-HMI-02 | OQ `TET-OQ-HMI-PALETTE-01` |
| DS-DCS-42 | HMI SLO Targets | alarm-ack ≤ 1 s + faceplate ≤ 500 ms | Custom | FS-HMI-03 / FS-PERF-01 — SLO | FS-HMI-03, FS-PERF-01 | OQ `TET-OQ-HMI-SLO-01` |
| DS-DCS-43 | HMI Graphic CR Template | DCS Engineer author + Eng Manager approve + QA co-sign | Custom | FS-HMI-04 — CR template | FS-HMI-04 | OQ `TET-OQ-HMI-CR-01` |
| DS-DCS-44 | DeltaV Live > AuthN | SAML SSO + MFA via Okta; sessions logged | Custom | FS-HMI-05 — DeltaV Live auth | FS-HMI-05 | OQ `TET-OQ-DV-LIVE-SSO-01` |
| DS-DCS-45 | ProfessionalPLUS > Access AD Groups | `DCS-Engineer`, `DCS-Eng-Manager`, `FSE`; MFA gated | Custom | FS-EWS-01 — access restriction | FS-EWS-01 | OQ `TET-OQ-EWS-ACCESS-01` |
| DS-DCS-46 | Configuration DB Diff Tool | `dvdiff`; signed CR closure artefact | Custom | FS-EWS-02 — config diff | FS-EWS-02 | OQ `TET-OQ-DVDIFF-01` |
| DS-DCS-47 | Simulator Regression Trigger | CPP-impacting CRs trigger simulator regression; pass required before prod | Custom | FS-EWS-03 — simulator gate | FS-EWS-03 | OQ `TET-OQ-SIM-REGR-01` |
| DS-DCS-48 | CR Register | `dcs_cr_register` cross-references HMI / control logic / recipes / phase logic | Custom | FS-EWS-04 — CR register | FS-EWS-04 | (CR system) |
| DS-DCS-49 | Annual Baseline Reconciliation | `baseline_reconcile.py` compares prod vs Configuration DB | Custom | FS-EWS-05 — baseline reconcile | FS-EWS-05 | PR-01 |
| DS-DCS-50 | DeltaV Event Chronicle + Audit Table | PTP timestamps; coverage per URS scope | Custom | FS-AUD-01 — event chronicle | FS-AUD-01 | OQ `TET-OQ-AUDIT-SCOPE-01` |
| DS-DCS-51 | Audit RBAC | App role INSERT/SELECT only; admin via break-glass with QA witness | Custom | FS-AUD-02 — audit RBAC | FS-AUD-02 | OQ `TET-OQ-AUDIT-RBAC-01` |
| DS-DCS-52 | Audit Review Perspective View | filterable; per-batch + quarterly review records signed | Custom | FS-AUD-03 — review view | FS-AUD-03 | OQ `TET-OQ-AUDIT-REV-01` |
| DS-DCS-53 | Audit Retention | 25 y to S3 Object-Lock + cross-region replication | Custom | FS-AUD-04 — retention | FS-AUD-04 | (governance) |
| DS-DCS-54 | Procedural Controls `/sop/` | annual review workflow | Custom | FS-PART11-01 — § 11.10(a) | FS-PART11-01 | PR-01 |
| DS-DCS-55 | AD Kerberos + MFA | enforced at all sign-ons | Custom | FS-PART11-02 — § 11.10(d) | FS-PART11-02 | OQ `TET-OQ-AUTHN-01` |
| DS-DCS-56 | E-Signature Meaning Enum | `authorship, review, approval, release, verification, bypass` | Custom | FS-PART11-04 — § 11.50 meaning | FS-PART11-04 | OQ `TET-OQ-ESIG-MEANING-01` |
| DS-DCS-57 | E-Signature Payload Hash Binding | SHA-256(record); tamper invalidates | Custom | FS-PART11-05 — § 11.70 binding | FS-PART11-05 | OQ `TET-OQ-ESIG-HASH-01` |
| DS-DCS-58 | AD HR-Derived Feed | daily sync; user-id reuse blocked | Custom | FS-PART11-06 — § 11.100 | FS-PART11-06 | OQ `TET-OQ-HRFEED-01` |
| DS-DCS-59 | Kerberos Fresh-Ticket Max-Age | 5 min at sign-off | Custom | FS-PART11-07 — § 11.200 | FS-PART11-07 | OQ `TET-OQ-KRB-FRESH-01` |
| DS-DCS-60 | AD Password Policy `SEC-AD-POLICY-001` | min 14 chars + complexity + 90-d rotation + MFA | Custom | FS-PART11-08 — § 11.300 | FS-PART11-08 | (governance) |
| DS-DCS-61 | Audit-Write Constraint | `actor_id NOT NULL` at audit-write | Custom | FS-DI-01 — attribution | FS-DI-01 | OQ `TET-OQ-AUDIT-ATTRIB-01` |
| DS-DCS-62 | Export Validation | PDF/A-3 + JSON/CSV | Custom | FS-DI-02 — export | FS-DI-02 | OQ `TET-OQ-EXPORT-01` |
| DS-DCS-63 | Timestamp Source | PTP timestamps; retroactive-entry guard | Custom | FS-DI-03 — PTP | FS-DI-03 | OQ `TET-OQ-PTP-AUDIT-01` |
| DS-DCS-64 | Aspen IP.21 Historian Write Mode | point-write only; corrections referenced | Custom | FS-DI-04 — point-write only | FS-DI-04 | OQ `TET-OQ-HIST-IMMUT-01` |
| DS-DCS-65 | OQ Math Regression Dataset | PID / cascade / phase math verified | Custom | FS-DI-05 — math regression | FS-DI-05 | OQ `TET-OQ-MATH-01` |
| DS-DCS-66 | Metadata Completeness + Retrieval SLA | ≤ 4 h via inspection runbook | Custom | FS-DI-06 — 4-h retrieval | FS-DI-06 | OQ `TET-OQ-INSP-01` |
| DS-DCS-67 | PAS-X Integration | OPC UA + REST mTLS; SHA-256 + version validated | Custom | FS-INT-PASX-01 — PAS-X integration | FS-INT-PASX-01 | OQ `TET-OQ-PASX-01` |
| DS-DCS-68 | Batch Report SLA | within 30 min of batch end; idempotent | Custom | FS-INT-PASX-02 — batch report | FS-INT-PASX-02 | OQ `TET-OQ-BATCH-RPT-01` |
| DS-DCS-69 | Aspen IP.21 Adapter | OPC HDA / UA; store-and-forward buffer | Custom | FS-INT-HIST-01 — Aspen integration | FS-INT-HIST-01 | OQ `TET-OQ-ASPEN-01` |
| DS-DCS-70 | BMS OPC UA mTLS | utility-status consumed; loss safes unit op | Custom | FS-INT-BMS-01 — BMS | FS-INT-BMS-01 | OQ `TET-OQ-BMS-01` |
| DS-DCS-71 | Foundation Fieldbus H1 Segments | per Emerson + ISA-50.02; health surfaced on `ff-health` faceplate | Custom | FS-INT-FF-01 — FF integration | FS-INT-FF-01 | OQ `TET-OQ-FF-HEALTH-01` |
| DS-DCS-72 | HART 7 via CHARMs + Multiplexer | secondary variables ingested (transmitter diagnostics) | Custom | FS-INT-HART-01 — HART integration | FS-INT-HART-01 | OQ `TET-OQ-HART-DIAG-01` |
| DS-DCS-73 | WirelessHART Join-Key Rotation | annual per NAMUR NE 124 | Custom | FS-INT-WHART-01 — WHART security | FS-INT-WHART-01 | OQ `TET-OQ-WHART-KEY-01` |
| DS-DCS-74 | AD Groups Consumed | `DCS-Operator, DCS-Senior, DCS-Engineer, DCS-Eng-Manager, DCS-RecipeAuthor, DCS-RecipeApprover, DCS-PhaseAuthor, DCS-PhaseApprover, FSE, FSE-Approver` | Custom | FS-INT-AD-01 — AD groups | FS-INT-AD-01 | OQ `TET-OQ-AD-GROUPS-01` |
| DS-DCS-75 | Synthetic Monitoring (SLOs) | alarm-ack + faceplate latency tracked | Custom | FS-PERF-01 — SLO measurement | FS-PERF-01 | OQ `TET-OQ-SLO-MON-01` |
| DS-DCS-76 | Availability Target | ≥ 99.95%; planned maintenance only in down windows | Custom | FS-AV-01 — availability | FS-AV-01 | (governance) |
| DS-DCS-77 | Configuration DB Backup | nightly + pre-change full-image to S3 Object-Lock | Custom | FS-BAK-01 — backup | FS-BAK-01 | OQ `TET-OQ-CFG-BAK-01` |
| DS-DCS-78 | Restore Test Cadence | quarterly + annual full DR including SIS proof-test | Custom | FS-BAK-02 — restore + DR | FS-BAK-02 | PR-01 |
| DS-DCS-79 | Security AD-Managed Accounts | auto-lockout per InfoSec policy | Custom | FS-SEC-01 — AD-managed | FS-SEC-01 | OQ `TET-OQ-SEC-ACC-01` |
| DS-DCS-80 | Removable-Media GPO | block-by-default; vendor-approved CR exceptions | Custom | FS-SEC-02 — removable media | FS-SEC-02 | OQ `TET-OQ-USB-01` |
| DS-DCS-81 | Tenable Nessus Scan | monthly; 30-d SLA on critical findings | Custom | FS-SEC-03 — vuln scan | FS-SEC-03 | (governance) |
| DS-DCS-82 | Network Segmentation Documentation | `dcs_zone_model.yaml` per NAMUR NE 153; allow-list audited | Custom | FS-SEC-04 — segmentation | FS-SEC-04 | OQ `TET-OQ-NETSEG-01` |
| DS-DCS-83 | Cornerstone Curriculum | per role; SIS roles require IEC 61511 competency cert | Custom | FS-TRN-01 — training | FS-TRN-01 | (governance) |
| DS-DCS-84 | Annual Refresher `DCS-2026-ANNUAL` | scenario practice + ISA-18.2 + Annex 1 updates | Custom | FS-TRN-02 — refresher | FS-TRN-02 | (governance) |
| DS-DCS-85 | Periodic Review Template `TET-PR-DCS-YYYYMMDD` | recipe/phase inventory + alarm drift + SIS proof-test + audit review + deviations + training + baseline | Custom | FS-PR-01 — periodic review | FS-PR-01 | PR-01 |
| DS-DCS-86 | AD Conditional Access `OT-DCS Conditional Access` | MFA at engineering workstation; OpStations named-location + role-bound smart cards; SIEM → Splunk `gxp-authn`; CyberArk PAM break-glass | Custom | FS-XSYS-AD-01 — conditional access | FS-XSYS-AD-01 | OQ `TET-OQ-CONDACC-01` |
| DS-DCS-87 | Veeam Backup | App-aware MS SQL VSS for DeltaV historian DB + file-level capture of controller + OpStation config; tier T1; RPO ≤ 4 h; RTO ≤ 4 BH; S3 Object-Lock Compliance Mode + LTO-9 air-gap monthly | Custom | FS-XSYS-BAK-01 — Veeam VSS | FS-XSYS-BAK-01 | OQ `TET-OQ-VEEAM-01` |

---

## 5. Workflow + Business-Rule Design

### 5.1 ISA-88 Batch Workflow (DeltaV Batch)

**Procedure → Unit Procedure → Operation → Phase** persistence in `physical_model` per ISA-88 Part 2. Phase classes (templates) are Cat-5 code (see § 8); batch instances reference phase classes by ID + version.

| Step | Decision point | Rule | Actor | Signature meaning |
|---|---|---|---|---|
| Recipe load | EFFECTIVE only? | Reject non-EFFECTIVE | (system) | n/a |
| Order receipt (PAS-X) | partial create? | Rollback if partial | (system) | n/a |
| Step ordering | next step | `StepOrderingGuard` enforces order | Operator | n/a |
| Critical step entry | criticality=Critical? | `criticalStepVerify` widget mandatory | Operator + Verifier | `verification` |
| CPP capture | per step | 1 Hz historian write | (system) | n/a |
| Override request | reason ≥ 10 chars | dual-sign Operator + Senior | Operator + Senior | `verification` (override) |
| Phase abort | safe-state per phase metadata | `safe_state_on_abort` execution | Senior Operator | `verification` (abort) |
| Batch end | report POST to PAS-X | within 30 min | (system) | n/a |

### 5.2 Alarm-Handling Rules (ISA-18.2)

Alarm-rationalisation file `alarm_rationalisation.xlsx` classifies every tag with: INFO / WARNING / CRITICAL / SIS — plus response, ack-requirement, escalation. Implementation:

- **INFO:** no ack; UI-display only.
- **WARNING:** ack required; reason optional.
- **CRITICAL:** ack required with reason ≥ 10 chars; persistent until ack; SMS + email on-call after T_escalate.
- **SIS:** handled by SIS logic-solver; mirrored to audit + `sis_events` table only; bypass requires FSE + FSE Approver dual-sign + auto-revert timer.
- **Shelving:** reason + max-duration captured; auto-revert.

### 5.3 SIS Bypass Workflow

```
FSE initiates → reason capture → FSE Approver countersign (within 60 s) → bypass_duration_set → SIS bypass active → timer expires → auto-revert → event logged → PR-01 review
```

### 5.4 Recipe Approval Workflow

```
DRAFT → REVIEW (Author authorship) → APPROVED (Reviewers review × n) → EFFECTIVE (Approver approval ×2: Head of Drug Substance + Head of QA) → OBSOLETE (Manufacturing Lead retirement)
```

Phase-logic-version cross-check at APPROVAL gate per FS-REC-05 / DS-DCS-15.

### 5.5 Critical-Step Verification (FS-BAT-03)

Critical steps (criticality=Critical) require a second-person verifier whose user-id ≠ operator user-id, captured via `criticalStepVerify` widget. Configured as Cat-4 workflow with FS-PHL-04 state transition guard.

---

## 6. Role-Permission Matrix Design

| AD Group | View HMI | Ack Warning | Ack Critical | Author Recipe | Approve Recipe | Author Phase | Approve Phase | Override | SIS bypass | SIS approve | Audit Export |
|---|---|---|---|---|---|---|---|---|---|---|---|
| `DCS-Operator` | Y | Y | — | — | — | — | — | initiate | — | — | — |
| `DCS-Senior` | Y | Y | Y | — | — | — | — | countersign | — | — | — |
| `DCS-Engineer` | Y | — | — | — | — | Y | — | — | — | — | — |
| `DCS-Eng-Manager` | Y | — | — | — | — | review | approve | — | — | — | — |
| `DCS-RecipeAuthor` | Y | — | — | Y | — | — | — | — | — | — | — |
| `DCS-RecipeApprover` | Y | — | — | review | approve | — | — | — | — | — | — |
| `DCS-PhaseAuthor` | Y | — | — | — | — | Y | — | — | — | — | — |
| `DCS-PhaseApprover` | Y | — | — | — | — | review | approve | — | — | — | — |
| `FSE` | Y | — | — | — | — | — | — | — | initiate | — | — |
| `FSE-Approver` | Y | — | — | — | — | — | — | — | — | countersign | — |
| `DCS-CSV-Reviewer` | Y (read-only) | — | — | — | — | — | — | — | — | — | Y |
| `DCS-Auditor` | Y (read-only) | — | — | — | — | — | — | — | — | — | Y |
| Break-glass `DCS-DBA` (vaulted) | — | — | — | — | — | — | — | — | — | — | — (DB admin only) |

FS-IDs traced: FS-INT-AD-01, FS-PART11-04 (SoD), FS-BAT-05 (override), FS-SIS-03 (SIS bypass), FS-EWS-01 (engineering access).

---

## 7. Integration Design

### 7.1 IF-PASX-RECIPE (Werum PAS-X v3.2 recipe / batch counterparty)

- **Endpoint:** OPC UA + REST mTLS — `opc.tcp://pasx.tethys.local:4840` (OPC UA path) + `https://pasx.tethys.local/api/v1` (REST path)
- **Schema (recipe response):** `{recipe_id, version, sha256, masterRecipeRef, siteRecipeRef, controlRecipeRef, payload JSON}`
- **Schema (batch report):** `{batch_id, recipe_id, recipe_version, started_at, ended_at, ebr_uri, signatures[], deviations[]}`
- **Retry:** 1/5/30 s exponential backoff; idempotency key = `batch_id`
- **Error handling:** SHA-256 mismatch → `409` + auto-deviation
- **Audit-trail emission:** `recipe_fetch`, `batch_report_post`
- **FS-IDs:** FS-INT-PASX-01, FS-INT-PASX-02

### 7.2 IF-HIST (Aspen IP.21)

- **Protocol:** OPC HDA + OPC UA; store-and-forward buffer at ApplicationStation for blip recovery
- **Cadence:** 1 Hz CPP; phase-state events on transition
- **FS-IDs:** FS-INT-HIST-01

### 7.3 IF-BMS (Site BMS)

- **Protocol:** OPC UA mTLS; utility-status tags (clean-steam P, WFI/PW availability, HVAC dP)
- **Behaviour:** loss safes the active unit op
- **FS-IDs:** FS-INT-BMS-01

### 7.4 IF-FF (Foundation Fieldbus H1)

- **Topology:** segments per Emerson reference + ISA-50.02; segment health monitored
- **Faceplate:** `ff-health` surfaces per-segment integrity
- **FS-IDs:** FS-INT-FF-01

### 7.5 IF-HART (HART 7 via CHARMs)

- **Path:** CHARMs + multiplexer; secondary variables (transmitter diagnostics) ingested into `hart_diagnostics` table
- **FS-IDs:** FS-INT-HART-01

### 7.6 IF-WHART (WirelessHART)

- **Security:** join-key rotation annual per NAMUR NE 124; gateway audit log
- **FS-IDs:** FS-INT-WHART-01

### 7.7 IF-AD (LDAPS / Kerberos `tethys.local`)

- **Groups consumed:** per DS-DCS-74
- **MFA:** Yubikey + Okta SAML for DeltaV Live
- **FS-IDs:** FS-INT-AD-01, FS-HMI-05, FS-XSYS-AD-01

### 7.8 Integration Risk Register

| Interface | Risk | Mitigation |
|---|---|---|
| IF-PASX-RECIPE | mTLS cert expiry | cert-manager 365-d rotation + 30-d alert |
| IF-HIST | Aspen IP.21 outage during batch | Store-and-forward + circuit-breaker |
| IF-FF | Segment fault undetected | Health monitor + `ff-health` faceplate (DS-DCS-71) |
| IF-WHART | Join-key compromise | Annual rotation + NE 124 audit |
| IF-AD | Outage | Local OT-cached credentials 24 h |

---

## 8. Site-Deployed Components — Mini-SDS for Phase Logic + Master Recipes (Cat 5)

The site-authored phase logic (Cat 5) is the embedded custom-code substrate that escalates this Cat 4 DCS to a hybrid Cat 4 + Cat 5. This section follows Cat 5 SDS rules at proportional depth.

### 8.1 Software Architecture (logical view)

```
   ┌─────────────────────────────────────────────────────────────┐
   │  Site Phase-Logic Library (DeltaV BPC, ~12k LOC equivalent)   │
   │  ┌────────────────────────┐  ┌──────────────────────────┐    │
   │  │  phase_classes/         │  │  master_recipes/          │    │
   │  │  - Inoculation          │  │  - mAb_PlatformA          │    │
   │  │  - Bioreactor_Ramp      │  │  - mAb_PlatformB          │    │
   │  │  - Harvest_Decision     │  │  - Cell-therapy_PlatformC │    │
   │  │  - CIP_Phase            │  └──────────────────────────┘    │
   │  │  - SIP_Phase            │  ┌──────────────────────────┐    │
   │  │  - Continuous_PID       │  │  safe_state/              │    │
   │  └────────────────────────┘  │  - utility_loss           │    │
   │  ┌────────────────────────┐  │  - sis_demand             │    │
   │  │  state_machine/         │  │  - abort                  │    │
   │  │  - Isa88StateMachine    │  └──────────────────────────┘    │
   │  └────────────────────────┘                                    │
   └─────────────────────────────────────────────────────────────┘
```

Stack: DeltaV BPC (Batch Phase Control) language for phase classes; ISA-88-aligned procedural-element framework. Where Java sub-modules are required for off-controller compute (PFDavg analytics, baseline-reconciliation), JVM 17 LTS on ApplicationStation.

### 8.2 Module Decomposition

| Module ID | Module name | Responsibility | Interface | Dependencies | GxP class |
|---|---|---|---|---|---|
| MS-01 | `phase_classes.Inoculation` | inoculation phase | enter/run/exit hooks | physical_model.Unit | R1 |
| MS-02 | `phase_classes.Bioreactor_Ramp` | ramp temperature + agitation | enter/run/exit | physical_model.EM | R1 |
| MS-03 | `phase_classes.Harvest_Decision` | harvest-criterion evaluation | enter/run/exit + decision_event | recipe.cqa_list | R1 |
| MS-04 | `phase_classes.CIP_Phase` | CIP recipe execution | enter/run/exit | utility tags | R1 |
| MS-05 | `phase_classes.SIP_Phase` | SIP recipe execution | enter/run/exit | utility tags | R1 |
| MS-06 | `phase_classes.Continuous_PID` | continuous-control wrapper around PID/cascade/ratio/feed-forward | enter/run/exit | controllers | R1 |
| MS-07 | `state_machine.Isa88StateMachine` | per-phase state model (IDLE..COMPLETE) | transition() callback | phase_classes | R1 |
| MS-08 | `safe_state.utility_loss_handler` | enters phase-defined safe-state on utility loss | event callback | BMS tags | R1 |
| MS-09 | `safe_state.sis_demand_handler` | enters phase-defined safe-state on SIS demand | event callback | SIS event | R1 |
| MS-10 | `safe_state.abort_handler` | enters phase-defined safe-state on abort | command callback | operator UI | R1 |
| MS-11 | `master_recipes.mAb_PlatformA` | platform A master recipe | ISA-88 procedure | phase_classes | R1 |
| MS-12 | `master_recipes.mAb_PlatformB` | platform B master recipe | ISA-88 procedure | phase_classes | R1 |

### 8.3 Data Model (DB schema highlights)

| Table | Key columns | Constraints | Retention |
|---|---|---|---|
| `recipe_versions` | `recipe_id, version`; `status` enum; `sha256`; `signatures` (JSONB) | trigger blocks UPDATE/DELETE on EFFECTIVE | indefinite |
| `recipe_xref` | `master_id, master_v, site_id, site_v, control_id, control_v` | FK pinned across levels | indefinite |
| `physical_model` | `unit_id, em_id, cm_id` per ISA-88 Part 2 | (none) | indefinite |
| `phase_events` | `phase_id, batch_id, transition, ts_ptp, signing_user, entry_condition_snapshot` | append-only | 25 y |
| `audit_events` | per FS-AUD-01 | append-only via role GRANT | 25 y |
| `sis_events` | mirror of SIS event recorder; `event_id`, `sif_id`, `state`, `ts_ptp` | append-only | 25 y |
| `failover_events` | `failover_id, gateway, from_state, to_state, ts_ptp` | append-only | 25 y |
| `sis_proof_test_records` | `pt_id, sif_id, executed_at, signed_by, result` | NOT NULL on signed_by | indefinite |

### 8.4 Algorithm + Calculation Design

| Algorithm | Inputs | Output | Procedure | Numerical-precision note | Reference |
|---|---|---|---|---|---|
| PID control loop (DeltaV native) | SP, PV, history | OP | DeltaV native PID block (vendor-validated) | IEEE-754; vendor 6-sig-fig | DeltaV reference |
| Cascade loop | primary OP, secondary PV | secondary SP | DeltaV native cascade block | vendor | DeltaV reference |
| Ratio control | primary flow, ratio | secondary SP | site-configured ratio block | float64 | site |
| Feed-forward compensation | disturbance signal, gain | OP correction | site-configured FF block | float64 | site |
| PFDavg recalculation | proof-test history + failure-rate | PFDavg per SIF | per NA 65 / NE 159 stepwise integration | float64; documented in `pfd_calc.xlsx` (controlled) | IEC 61511 |
| Alarm-flood detector | alarm-event series | bool + count | rolling 60 s count > N (recipe) | int; per ISA-18.2 | ISA-18.2 |
| Baseline reconcile (`baseline_reconcile.py`) | prod config + Config DB export | diff report | `dvdiff` invocation + Python diff renderer | textual | site |

### 8.5 Interface + API Design (site module API)

| Endpoint | Method | AuthN | Request | Response | Idempotency | Audit |
|---|---|---|---|---|---|---|
| `/api/recipes/effective` | GET | Kerberos | `recipe_id` | RecipeVersion JSON | safe | `recipe_fetch` |
| `/api/recipes/transition` | POST | Kerberos + signed JWT | `{recordHash, signerId, meaning}` | new status | by recordHash | `recipe_transition` |
| `/api/phases/{phase_id}/version` | GET | Kerberos | path | Phase metadata + safe-state declarations | safe | `phase_query` |
| `/api/sis/bypass` | POST | Kerberos + FSE/FSE-Approver dual JWT | `{sif_id, reason, duration}` | bypass_id + auto-revert ts | by sif_id + ts | `sis_bypass_create` |
| `/api/override` | POST | Kerberos + Op/Senior dual JWT | `{batch_id, reason}` | override_id | by batch_id + ts | `override_create` |

### 8.6 Security Design

- **AuthN:** Kerberos + SAML SSO (DeltaV Live) + Okta MFA
- **AuthZ:** AD-group → role mapping per § 6
- **Secret management:** CyberArk PAM for break-glass; HashiCorp Vault for service accounts (1-h TTL)
- **Transport:** TLS 1.2+; mTLS for PAS-X, BMS, IP.21
- **Audit event taxonomy:** `recipe_fetch`, `recipe_transition`, `phase_transition`, `signature_emit`, `override_create`, `sis_bypass_create`, `sis_bypass_revert`, `alarm_raise`, `alarm_ack`, `failover_event`, `module_deploy`

### 8.7 Deployment Architecture

- **Packaging:** DeltaV ConfigExport bundles signed via Emerson signing + site cosign wrap
- **Topology:** Configuration DB → controllers; simulator regression on `dcs-sim` host before production deploy
- **Observability:** Prometheus exporters + Grafana `TET-GR-DCS-RUNTIME`; logs to Splunk `gxp-dcs`
- **DR:** Annual full DR exercise including SIS proof-test

### 8.8 Module Specification Table (pointer)

| Module ID | Source location | Unit-test ref |
|---|---|---|
| MS-01..MS-12 | DeltaV ConfigExport repo `dvconfig.tethys.local/dcs-master/{phase_classes,master_recipes,safe_state}` | `<repo>/tests/sim/test_<module>.dvscen` (simulator) |

Full Module Specifications live downstream as `TET-MS-DCS-NN`.

---

## 9. References

### US
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .22, .68, .180, .192
- FDA CSA (final, February 2026)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EU GMP Annex 1 (2022 revision)
- EU GMP Annex 15
- Directive 2001/83/EC Art. 51

### DACH
- NAMUR NA 102 (Lifecycle)
- NAMUR NE 33 (DCS-System-Integration)
- NAMUR NA 65 (SIF)
- NAMUR NE 159 (Functional Safety)
- NAMUR NE 153 (Zone Model)
- NAMUR NE 124 (WirelessHART security)
- BSI IT-Grundschutz baseline (OT segmentation)

### International
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE GAMP GPG *Process Control Systems*
- ICH Q9(R1); ICH Q10; ICH Q11
- ISA-88 Part 1 + Part 2; ISA-95 Part 1; ISA-101; ISA-18.2; ISA-50.02
- IEC 61131-3 (PLC programming languages)
- IEC 61508 (Functional Safety)
- IEC 61511 (Process-industry safety)
- IEC 61850 (informational, substation comms)
- PIC/S PI 041
- ISO/IEC 27001:2022

### Vendor
- Emerson — *DeltaV v15.3 System Reference*
- Emerson — *DeltaV SIS Safety Manual*
- Emerson — *DeltaV Live Reference*
- Emerson — *DeltaV ConfigExport / dvdiff User Guide*

### Site
- `TET-URS-DCS-001` v1.2 (informational)
- `TET-FS-DCS-001` v1.2 (parent)
- `TET-SOP-IT-CAT5-PHL-001` (Cat-5 SDLC for phase logic)
- `TET-SIS-PT-PLAN-001` (SIS proof-test plan)
- `TET-AP-DCS-01` (Alarm Philosophy)
- `TET-PR-DCS-YYYYMMDD` (periodic review template)

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-DCS-01 | FS-PLAT-01 |
| DS-DCS-02 | FS-PLAT-02 / FS-SEC-04 |
| DS-DCS-03 | FS-PLAT-03 |
| DS-DCS-04 | FS-PLAT-04 |
| DS-DCS-05 | FS-PLAT-05 |
| DS-DCS-06 | FS-RDN-01 |
| DS-DCS-07 | FS-RDN-02 |
| DS-DCS-08 | FS-RDN-03 |
| DS-DCS-09 | FS-RDN-04 / FS-SIS-01 |
| DS-DCS-10 | FS-RDN-05 |
| DS-DCS-11 | FS-REC-01 |
| DS-DCS-12 | FS-REC-02 |
| DS-DCS-13 | FS-REC-03 / FS-INT-PASX-01 |
| DS-DCS-14 | FS-REC-04 |
| DS-DCS-15 | FS-REC-05 |
| DS-DCS-16 | FS-REC-06 |
| DS-DCS-17 | FS-REC-07 |
| DS-DCS-18 | FS-PHL-01 |
| DS-DCS-19 | FS-PHL-02 |
| DS-DCS-20 | FS-PHL-03 |
| DS-DCS-21 | FS-PHL-04 |
| DS-DCS-22 | FS-PHL-05 |
| DS-DCS-23 | FS-PHL-06 |
| DS-DCS-24 | FS-BAT-01 |
| DS-DCS-25 | FS-BAT-02 |
| DS-DCS-26 | FS-BAT-03 |
| DS-DCS-27 | FS-BAT-04 |
| DS-DCS-28 | FS-BAT-05 |
| DS-DCS-29 | FS-BAT-06 |
| DS-DCS-30 | FS-BAT-07 |
| DS-DCS-31 | FS-ALM-01 |
| DS-DCS-32 | FS-ALM-02 |
| DS-DCS-33 | FS-ALM-03 |
| DS-DCS-34 | FS-ALM-04 |
| DS-DCS-35 | FS-ALM-05 |
| DS-DCS-36 | FS-SIS-01 |
| DS-DCS-37 | FS-SIS-02 |
| DS-DCS-38 | FS-SIS-03 |
| DS-DCS-39 | FS-SIS-04 |
| DS-DCS-40 | FS-HMI-01 |
| DS-DCS-41 | FS-HMI-02 |
| DS-DCS-42 | FS-HMI-03 / FS-PERF-01 |
| DS-DCS-43 | FS-HMI-04 |
| DS-DCS-44 | FS-HMI-05 |
| DS-DCS-45 | FS-EWS-01 |
| DS-DCS-46 | FS-EWS-02 |
| DS-DCS-47 | FS-EWS-03 |
| DS-DCS-48 | FS-EWS-04 |
| DS-DCS-49 | FS-EWS-05 |
| DS-DCS-50 | FS-AUD-01 |
| DS-DCS-51 | FS-AUD-02 |
| DS-DCS-52 | FS-AUD-03 |
| DS-DCS-53 | FS-AUD-04 |
| DS-DCS-54 | FS-PART11-01 |
| DS-DCS-55 | FS-PART11-02 / FS-PART11-03 |
| DS-DCS-56 | FS-PART11-04 |
| DS-DCS-57 | FS-PART11-05 |
| DS-DCS-58 | FS-PART11-06 |
| DS-DCS-59 | FS-PART11-07 |
| DS-DCS-60 | FS-PART11-08 |
| DS-DCS-61 | FS-DI-01 |
| DS-DCS-62 | FS-DI-02 |
| DS-DCS-63 | FS-DI-03 |
| DS-DCS-64 | FS-DI-04 |
| DS-DCS-65 | FS-DI-05 |
| DS-DCS-66 | FS-DI-06 |
| DS-DCS-67 | FS-INT-PASX-01 |
| DS-DCS-68 | FS-INT-PASX-02 |
| DS-DCS-69 | FS-INT-HIST-01 |
| DS-DCS-70 | FS-INT-BMS-01 |
| DS-DCS-71 | FS-INT-FF-01 |
| DS-DCS-72 | FS-INT-HART-01 |
| DS-DCS-73 | FS-INT-WHART-01 |
| DS-DCS-74 | FS-INT-AD-01 |
| DS-DCS-75 | FS-PERF-01 |
| DS-DCS-76 | FS-AV-01 |
| DS-DCS-77 | FS-BAK-01 |
| DS-DCS-78 | FS-BAK-02 |
| DS-DCS-79 | FS-SEC-01 |
| DS-DCS-80 | FS-SEC-02 |
| DS-DCS-81 | FS-SEC-03 |
| DS-DCS-82 | FS-SEC-04 |
| DS-DCS-83 | FS-TRN-01 |
| DS-DCS-84 | FS-TRN-02 |
| DS-DCS-85 | FS-PR-01 |
| DS-DCS-86 | FS-XSYS-AD-01 |
| DS-DCS-87 | FS-XSYS-BAK-01 |
| MS-01..MS-12 | Cat-5 mini-SDS § 8.2 — phase-class + master-recipe code; transitively traces FS-PHL-01..06 + FS-REC-01..07 + FS-BAT-01..07 + FS-SIS-01..04 |

---

## 11. Design-level Risk Register

Per § 2B.8.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| DR-01 | Phase-logic version drift between Configuration DB and live controllers | Low | High | Baseline reconcile (DS-DCS-49) + `dvdiff` (DS-DCS-46) |
| DR-02 | SIS event mirror to audit (DS-DCS-36) creates write-back attack surface | Low | High | One-way (SIS → audit) only; SIS network isolated; firewall enforcement |
| DR-03 | Alarm-rationalisation drift after process change (DS-DCS-31 stale) | Medium | High | Annual review under PR-01 + CR gate on any alarm-table edit |
| DR-04 | `dvdiff` false negative on whitespace / formatting changes (DS-DCS-46) | Medium | Medium | Canonical-form diff before invocation + secondary `git diff` |
| DR-05 | PFDavg recalc (DS-DCS-39) uses stale failure-rate inputs | Low | High | Annual vendor failure-rate update mandate; SIS engineering review |
| DR-06 | DeltaV Live SAML SSO + Okta MFA outage prevents HMI access | Low | High | Local fallback to OperatorStation Windows AD + named-location |
| DR-07 | Foundation Fieldbus segment fault under-detected by health monitor (DS-DCS-71) | Medium | Medium | Periodic ISA-50.02 audit + redundant segment health probes |
| DR-08 | WirelessHART join-key rotation (DS-DCS-73) coincides with batch run | Low | Medium | Schedule rotation outside production windows; vendor-coordinated |
| DR-09 | NAMUR NE 153 zone-model `dcs_zone_model.yaml` (DS-DCS-82) drifts vs firewall ACLs | Medium | High | Automated reconciliation script + quarterly audit |
| DR-10 | Configuration DB backup (DS-DCS-77) misses partial-update window mid-CR | Low | Medium | Pre-change full-image triggered by CR-open hook |
| DR-11 | DR test cadence (DS-DCS-78) reveals SIS proof-test gap > demand-rate interval | Low | Critical | Quarterly + annual full DR including SIS proof-test (FS-BAK-02) |
| DR-12 | Bumpless-transfer (DS-DCS-06) fails on rare controller-pair desync | Low | High | OQ failover test + redundancy diagnostic continuous monitor |
| DR-13 | Recipe `master/site/control` FK desync (DS-DCS-12) silently breaks recipe genealogy | Low | High | DB FK constraints + APPROVAL gate check |
| DR-14 | Critical-step `criticalStepVerify` widget bypass via direct API call | Low | Critical | API-level enforcement (not UI-only); SoD check at server side |
| DR-15 | Phase metadata `safe_state_on_*` declarations missing on imported phase class | Low | High | APPROVAL gate validates non-null safe-state metadata (DS-DCS-22) |
| DR-16 | Audit-retention S3 bucket Object-Lock in Governance Mode instead of Compliance | Low | Critical | IQ verification of Compliance Mode at bucket creation + annual recheck |
| DR-17 | Veeam VSS backup (DS-DCS-87) creates write-pause window > Configuration DB tolerance | Low | Medium | Backup window scheduled in maintenance window + monitored |
| DR-18 | AD Conditional Access (DS-DCS-86) excludes SIS engineering workstation accidentally | Low | High | Named-location exception list + quarterly access review |
| DR-19 | DeltaV ConfigExport bundle (DS-DCS-46) loses provenance metadata across CR cycles | Low | Medium | `dvdiff` includes CR-ID + signing user in export header; CR system FK-pinned to bundle |
| DR-20 | PROFINET-IRT synchronisation jitter on controller pair under heavy I/O load | Low | Medium | Network-load monitoring + scheduled load testing during DR exercises |
| DR-21 | Alarm-philosophy doc (DS-DCS-33) annual review misses tag-class drift from incremental CRs | Medium | Medium | Each alarm-class CR back-references philosophy doc + annual reconciliation runner |
| DR-22 | DR test cadence (DS-DCS-78) reveals stale Configuration DB image vs production runtime drift | Low | High | Pre-DR snapshot of production runtime; reconciliation report at DR-exercise close |
| DR-23 | HMI graphic CR (DS-DCS-43) regression breaks faceplate state visualization mid-batch | Low | High | Regression suite on `gw-test` gateway before deploy; rollback CR path |
| DR-24 | SIS firmware refresh (DS-DCS-05) coincides with proof-test interval window | Low | High | Pre-firmware-refresh proof-test mandate per IEC 61511 FSM procedure |

### Design-level risk summary

#### Cross-section coherence notes

The DS-DCS-NN configuration items map to FS-IDs in a deliberate density pattern: 5 platform CIs (DS-DCS-01..05), 5 redundancy CIs (DS-DCS-06..10), 7 recipe-management CIs (DS-DCS-11..17), 6 phase-logic CIs (DS-DCS-18..23), 7 batch-execution CIs (DS-DCS-24..30), 5 alarm-management CIs (DS-DCS-31..35), 4 SIS CIs (DS-DCS-36..39), 5 HMI CIs (DS-DCS-40..44), 5 engineering-workstation CIs (DS-DCS-45..49), 4 audit CIs (DS-DCS-50..53), 7 Part-11 CIs (DS-DCS-54..60), 6 data-integrity CIs (DS-DCS-61..66), 8 integration CIs (DS-DCS-67..74), 2 performance CIs (DS-DCS-75..76), 2 backup CIs (DS-DCS-77..78), 4 security CIs (DS-DCS-79..82), 2 training CIs (DS-DCS-83..84), 1 periodic-review CI (DS-DCS-85), and 2 cross-system CIs (DS-DCS-86..87) — for a total of 87 CIs covering 87 FS-IDs. Each FS-ID has at least one DS-ID; some FS-IDs (FS-PERF-01, FS-INT-AD-01, FS-XSYS-AD-01) are referenced by multiple DS-IDs for orthogonal facets (latency tracking, group binding, conditional access).

#### Mini-SDS (§ 8) decomposition rationale

The site-developed phase logic + master recipes (Cat 5) are decomposed in § 8.2 across 12 modules grouped by responsibility: 6 phase classes (MS-01..06), 1 state machine (MS-07), 3 safe-state handlers (MS-08..10), and 2 master recipes (MS-11..12). The decomposition reflects the ISA-88 procedural hierarchy and the recipe-platform pattern (each master recipe references phase classes by ID + version, never by source). The safe-state handlers (MS-08/09/10) are the highest-criticality modules — their unit-test coverage gate is enforced at 95% (vs 90% baseline) at CI.

#### Vendor-internal boundary

Per § 2B.1, the DS does NOT redraw vendor internals. For this DCS, vendor-internal scope includes: DeltaV runtime engine (Emerson SDLC), SIS embedded safety firmware (vendor-validated per IEC 61511), HMI rendering pipeline (DeltaV Operate / Live internal), and CHARM I/O firmware. The DS configures the **exposed interfaces** of each (e.g., SIS bypass workflow, SIS event mirror, DeltaV Live SAML SSO, CHARM I/O assignment) — never the internals.

#### Mitigation cross-references

Specific design choices mitigate specific risks:

- **DR-01 (phase-logic version drift):** mitigated by DS-DCS-46 (`dvdiff`), DS-DCS-49 (annual baseline reconcile), DS-DCS-15 (APPROVAL-gate phase-version check)
- **DR-09 (zone-model drift vs ACLs):** mitigated by DS-DCS-82 (`dcs_zone_model.yaml` as source of truth) + automated reconciliation
- **DR-15 (missing safe-state metadata):** mitigated by DS-DCS-22 APPROVAL-gate validation — phase-metadata-completeness rule prevents EFFECTIVE promotion
- **DR-18 (Conditional Access exclusion):** mitigated by named-location reconciliation + DS-DCS-86 exception list discipline
- **DR-22 (DR drift):** mitigated by pre-DR production-runtime snapshot + DS-DCS-78 annual full-DR-with-SIS-proof-test cadence
- **DR-04 (`dvdiff` false negative on whitespace):** mitigated by canonical-form serializer pre-diff + secondary `git diff` on the serialized output
- **DR-23 (HMI graphic regression):** mitigated by `gw-test` gateway regression suite + rollback CR path within 1 h
- **DR-14 (critical-step API bypass):** mitigated by API-level server-side enforcement (not UI-only) + integration test that exercises direct-API bypass attempts at OQ

#### Coverage gap analysis

Of 87 FS-IDs, all are covered by at least one DS-DCS-NN CI. Three FS-IDs receive multi-CI coverage owing to their cross-cutting nature: FS-PLAT-04 (PTP) is referenced by DS-DCS-04 (grandmaster + skew exporter) and indirectly by DS-DCS-63 (PTP timestamps in audit) and DS-DCS-50 (PTP-timestamped event chronicle); FS-INT-AD-01 is referenced by DS-DCS-74 (group inventory) and DS-DCS-86 (Conditional Access wiring); FS-PERF-01 is referenced by DS-DCS-42 (HMI SLO) and DS-DCS-75 (synthetic monitoring). No FS-ID is uncovered; no DS-ID is an orphan.

The 12 Cat-5 mini-SDS modules (MS-01..MS-12) transitively trace FS-PHL-01..06 + FS-REC-01..07 + FS-BAT-01..07 + FS-SIS-01..04. The decomposition rationale ensures that each phase class corresponds to a recipe-defined ISA-88 phase template and that each safe-state handler is exercised at OQ via simulator-driven bypass-attempt scenarios.

The risk register reflects three distinct categories:

1. **Configuration-coherence risks** (DR-01, DR-03, DR-09, DR-13, DR-15) — risks that originate in keeping multiple configuration surfaces consistent across CRs (phase-logic versions, alarm-rationalisation, NAMUR NE 153 zone-model, recipe FK hierarchy, phase metadata).
2. **Vendor-integration risks** (DR-02, DR-12, DR-19, DR-20) — risks at the boundary between site-designed configuration and vendor-validated internals (SIS mirror, bumpless transfer, ConfigExport bundle, PROFINET-IRT).
3. **Infrastructure-tier risks** (DR-06, DR-16, DR-17, DR-21, DR-22, DR-23) — risks that propagate from supporting infrastructure (DeltaV Live SSO, Object-Lock retention, Veeam backup, alarm philosophy, DR cadence, HMI regression).

Each risk row carries a mitigation-reference to a specific DS-ID or governance instrument. The formal Risk Assessment artefact `TET-RA-DCS-001` (synthetic, downstream) re-evaluates these with FMEA / HAZOP rigor and assigns RPN scores.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
