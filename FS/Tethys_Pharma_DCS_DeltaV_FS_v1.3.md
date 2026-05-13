---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (FS catch-up to URS v1.2 — T3 enrichment)"
seed_corpus_basis:
  - "TET-URS-DCS-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd ed.) Cat 4 + Cat 5"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11; Annex 1"
  - "ISA-88; ISA-95; ISA-101; ISA-18.2; ISA-50.02"
  - "IEC 61508; IEC 61511; NAMUR NA 102, NE 33, NA 65, NE 159, NE 153, NE 124"
parent_urs:
  document_number: TET-URS-DCS-001
  version: "1.2"
  file: "../../URS/_generated/final/DCS_Distributed_Control_System__Tethys_Pharma_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# Functional Specification (FS)

## DCS — Emerson DeltaV v15.3 (Bioprocess Suite)

**Document Number:** TET-FS-DCS-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** TET-URS-DCS-001 v1.2 | **Site:** Tethys Pharma S.A., Lyon, France *(fictional)*
**System Class:** GAMP Cat 4 — Configured Product (with site phase logic + master recipes as Cat 5 sub-components)
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Part 211; EU GMP Annex 11; Annex 1; ICH Q9(R1); ICH Q10; ICH Q11; ISA-88; ISA-95; ISA-101; ISA-18.2; IEC 61508; IEC 61511; NAMUR NA 102 / NE 33 / NA 65 / NE 159 / NE 153 / NE 124; PIC/S PI 041.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Process Automation Lead) | _____________ | _____________ | _____ |
| Reviewer (Functional Safety Engineer) | _____________ | _____________ | _____ |
| Reviewer (DCS Engineering Manager) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Approver (Head of Drug Substance Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Minor SIS scope edit. |
| 1.2 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.2: every URS-ID expanded to its own FS row; redundancy + HMI + alarm management + engineering-workstation change-control + multi-protocol field-bus implementations added. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

Specify DeltaV v15.3 configuration to satisfy `TET-URS-DCS-001` v1.2 — bioprocess DCS for the 6-train DSP1 suite.

## 2. Scope

DeltaV ProfessionalPLUS / ApplicationStation (×2 redundant) / OperatorStations (12) / controllers (24, redundant pairs) / SIS logic-solvers (SIL 2, 1oo2D); site-authored phase logic + master recipes (Cat 5); integrations with PAS-X, Aspen IP.21, Site BMS, Foundation Fieldbus H1, HART 7, WirelessHART, AD `tethys.local`.

## 3. System Architecture

```
   AD/PKI/PTP ──► DeltaV ProfessionalPLUS / AppStation (redundant pair)
                          │
                          ▼
                  Operator Stations (×12)   ◄──► DeltaV Live web HMI
                          │
              ┌───────────┼───────────┬───────────┬───────────┐
              ▼           ▼           ▼           ▼           ▼
        Controllers   SIS logic   Phase logic   I/O cards   FF / HART /
        (×24,         solvers     (Cat 5)       (CHARMs)    WirelessHART
        redundant)    (SIL 2,
                      1oo2D)
                          │
          ┌───────────────┼───────────────┐
          ▼               ▼               ▼
        PAS-X       Aspen IP.21      Site BMS
        (recipe/    (historian)      (interlocks)
        report)
```

## 4. Functional Specifications

### 4.1 Platform / Hardware (URS §5.1)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | Redundant ProfessionalPLUS + ApplicationStation pair; 24 controllers as redundant pairs; 12 OpStations on fault-tolerant Ethernet ring; cluster status surfaced on overview faceplate. |
| FS-PLAT-02 | URS-PLAT-02 | Dedicated DCS process-control VLAN; firewall + DMZ to corporate per NAMUR NE 153 zone model; allow-list documented. |
| FS-PLAT-03 | URS-PLAT-03 | UPS sized ≥ 30 min; SIS logic-solvers on isolated UPS branch. |
| FS-PLAT-04 | URS-PLAT-04 | PTP IEEE 1588 grandmaster + boundary clocks; skew monitored via Prometheus exporter; > 1 s alarms. |
| FS-PLAT-05 | URS-PLAT-05 | Firmware updates governed by Emerson + site CR; SIS firmware additionally under IEC 61511 FSM procedure. |

### 4.2 Redundancy + Failover (URS §5.2)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RDN-01 | URS-RDN-01 | Controller pairs configured for bumpless transfer; failover < 1 s verified at OQ procedure `TET-OQ-CTRL-FAILOVER-01`. |
| FS-RDN-02 | URS-RDN-02 | Redundant ApplicationStations with shared state replicated; HMI sessions reconnect via VIP. |
| FS-RDN-03 | URS-RDN-03 | I/O network in ring topology with RSTP / PRP / HSR (per Emerson reference); single-fault tolerance verified. |
| FS-RDN-04 | URS-RDN-04 | SIS logic-solver pair in 1oo2D voting per IEC 61511; SIL 2 verification documented. |
| FS-RDN-05 | URS-RDN-05 | Failover events written to `failover_events` table + surfaced on `gw-cluster-health` faceplate. |

### 4.3 Recipe Management — ISA-88 Hierarchy (URS §5.3)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REC-01 | URS-REC-01 | Recipe lifecycle DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE; transitions signed in DeltaV Batch + DCS Configuration DB. |
| FS-REC-02 | URS-REC-02 | DeltaV Batch master recipes + site recipes + control recipes; version-pinned cross-level FKs in `recipe_xref` table. |
| FS-REC-03 | URS-REC-03 | PAS-X OPC UA recipe download; SHA-256 + version validated by `RecipeReceiver`; mismatch rejects. |
| FS-REC-04 | URS-REC-04 | Transition workflow requires signed JWT payloads; SoD enforced via role matrix. |
| FS-REC-05 | URS-REC-05 | APPROVAL workflow verifies referenced phase-logic versions; broken refs raise `RECIPE_BROKEN_REFS`. |
| FS-REC-06 | URS-REC-06 | EFFECTIVE recipes immutable via DB triggers. |
| FS-REC-07 | URS-REC-07 | Physical-model bindings (units / equipment-modules / control-modules) persisted in `physical_model` table per ISA-88 Part 2. |

### 4.4 Phase Logic — ISA-88 Batch State Machine (URS §5.4)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PHL-01 | URS-PHL-01 | Cat-5 SDLC documented in `TET-SOP-IT-CAT5-PHL-001`; CI gates enforce code review + unit + integration + simulation tests. |
| FS-PHL-02 | URS-PHL-02 | Deployment to PRODUCTION requires approved CR + green regression-test run on the simulator. |
| FS-PHL-03 | URS-PHL-03 | DeltaV Version Control with signed authorship; commits cryptographically linked. |
| FS-PHL-04 | URS-PHL-04 | ISA-88 state model (IDLE / RUNNING / HELD / RESTARTING / STOPPING / STOPPED / ABORTING / ABORTED / COMPLETE) implemented per phase template; transitions deterministic. |
| FS-PHL-05 | URS-PHL-05 | Each phase declares `safe_state_on_utility_loss`, `safe_state_on_sis_demand`, `safe_state_on_abort` in phase metadata; validated at recipe APPROVAL. |
| FS-PHL-06 | URS-PHL-06 | Phase-metrics exporter `phase_duration_seconds`, `phase_state_transitions_total`. |

### 4.5 Batch Execution (URS §5.5)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BAT-01 | URS-BAT-01 | PAS-X order ingestion is transactional; partial creation rolled back. |
| FS-BAT-02 | URS-BAT-02 | `StepOrderingGuard` enforces master-recipe step order; override requires signed reason. |
| FS-BAT-03 | URS-BAT-03 | Critical-step second-person verification via dual-sign workflow `criticalStepVerify`. |
| FS-BAT-04 | URS-BAT-04 | CPP channels recorded at 1 Hz to historian; verified at OQ. |
| FS-BAT-05 | URS-BAT-05 | Override workflow requires Operator + Senior Operator signatures + reason ≥ 10 chars. |
| FS-BAT-06 | URS-BAT-06 | Abort sequence runs recipe-defined safe-state procedure; logged. |
| FS-BAT-07 | URS-BAT-07 | Continuous-control modules (PID + cascade + ratio + feed-forward) execute on redundant controllers; bumpless transfer per FS-RDN-01. |

### 4.6 Alarms — ISA-18.2 (URS §5.6)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ALM-01 | URS-ALM-01 | Alarm rationalisation in `alarm_rationalisation.xlsx` (controlled doc) classifies INFO/WARNING/CRITICAL/SIS with response, ack-requirement, escalation. |
| FS-ALM-02 | URS-ALM-02 | Critical-alarm ack with reason ≥ 10 chars; unacknowledged > T_escalate triggers SMS + email on-call. |
| FS-ALM-03 | URS-ALM-03 | Alarm philosophy `TET-AP-DCS-01` controls lifecycle; reviewed annually under PR-01. |
| FS-ALM-04 | URS-ALM-04 | Alarm-rate metrics exporter (per-operator per-hour, peak rate, top-talkers, standing-alarm count, flood frequency); Grafana dashboard `TET-GR-ALARM`. |
| FS-ALM-05 | URS-ALM-05 | Shelving function with reason + max-shelve-duration; auto-revert on expiration; logged. |

### 4.7 SIS — IEC 61511 (URS §5.7)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SIS-01 | URS-SIS-01 | SIS responses implemented on DeltaV SIS logic-solver pair (SIL 2, 1oo2D); events to SIS event recorder + mirrored to audit trail. |
| FS-SIS-02 | URS-SIS-02 | Proof-test plan `TET-SIS-PT-PLAN-001` executed per demand-rate interval; evidence in `sis_proof_test_records`. |
| FS-SIS-03 | URS-SIS-03 | Bypass workflow requires FSE + FSE Approver dual-sign + duration; auto-revert at timer expiration; recorded. |
| FS-SIS-04 | URS-SIS-04 | Annual PFDavg recalculation under NA 65 / NE 159; result reviewed at PR-01. |

### 4.8 HMI — ISA-101 (URS §5.8)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-HMI-01 | URS-HMI-01 | DeltaV Operate + Live screens follow Level 1-4 hierarchy per ISA-101; navigation budget ≤ 3 clicks audited at design review. |
| FS-HMI-02 | URS-HMI-02 | High-performance palette: greys for normal, saturated for abnormal; alarm-priority colour-map fixed (red=critical, amber=warning, blue=info, magenta=SIS). |
| FS-HMI-03 | URS-HMI-03 | Alarm-ack ≤ 1 s + faceplate ≤ 500 ms SLOs measured via synthetic monitoring. |
| FS-HMI-04 | URS-HMI-04 | HMI graphic CR template requires DCS Engineer authorship, DCS Engineering Manager approval, QA co-sign. |
| FS-HMI-05 | URS-HMI-05 | DeltaV Live SAML SSO + MFA via Okta; sessions logged. |

### 4.9 Engineering Workstation + Control Logic CR (URS §5.9)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-EWS-01 | URS-EWS-01 | ProfessionalPLUS access restricted to AD groups `DCS-Engineer`, `DCS-Eng-Manager`, `FSE`; gated by MFA. |
| FS-EWS-02 | URS-EWS-02 | Configuration DB exports via DeltaV ConfigExport; diff via `dvdiff` tool; signed as CR closure artefact. |
| FS-EWS-03 | URS-EWS-03 | CPP-impacting control-module CRs trigger simulator regression suite execution; pass required before prod deploy. |
| FS-EWS-04 | URS-EWS-04 | CR register `dcs_cr_register` cross-references HMI graphics + control logic + recipes + phase logic; surfaced in periodic review. |
| FS-EWS-05 | URS-EWS-05 | Annual baseline audit script `baseline_reconcile.py` compares production vs Configuration DB; deltas reported. |

### 4.10 Audit Trail / 21 CFR Part 11 / DI (URS §5.10)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | DeltaV event chronicle + DCS audit table; PTP timestamps; coverage per URS scope. |
| FS-AUD-02 | URS-AUD-02 | App role INSERT/SELECT only on audit; admin gated by break-glass with QA witness. |
| FS-AUD-03 | URS-AUD-03 | Audit-trail review Perspective view filterable; per-batch + quarterly review records signed. |
| FS-AUD-04 | URS-AUD-04 | Retention 25 y to S3 object-lock + cross-region replication. |
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural controls documented in `/sop/`. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(d): AD Kerberos + MFA. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(e): audit per FS-AUD-01. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.50: e-sig fields enforced; meaning enum (`authorship`, `review`, `approval`, `release`, `verification`, `bypass`). |
| FS-PART11-05 | URS-PART11-05 | Per § 11.70: SHA-256(record) bound; tamper invalidates. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.100: AD HR-derived feed; reuse blocked. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.200: fresh Kerberos ticket max-age 5 min. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.300: AD password policy. |
| FS-DI-01 | URS-DI-01 | Audit-write NOT-NULL on `actor_id`. |
| FS-DI-02 | URS-DI-02 | PDF/A-3 + JSON / CSV export validated. |
| FS-DI-03 | URS-DI-03 | PTP timestamps + retroactive-entry guard. |
| FS-DI-04 | URS-DI-04 | DeltaV historian point-write only; corrections referenced. |
| FS-DI-05 | URS-DI-05 | PID / cascade / phase math verified via OQ regression dataset. |
| FS-DI-06 | URS-DI-06 | Metadata completeness validated; retrievable ≤ 4 h. |

### 4.11 Integrations (URS §5.11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-PASX-01 | URS-INT-PASX-01 | PAS-X OPC UA + REST mTLS recipe download; SHA-256 + version validated. |
| FS-INT-PASX-02 | URS-INT-PASX-02 | Executed-batch report posted to PAS-X within 30 min of batch end; idempotent. |
| FS-INT-HIST-01 | URS-INT-HIST-01 | Aspen IP.21 OPC HDA / UA; store-and-forward buffer for blip recovery. |
| FS-INT-BMS-01 | URS-INT-BMS-01 | BMS OPC UA mTLS consumed; loss safes unit op. |
| FS-INT-FF-01 | URS-INT-FF-01 | Foundation Fieldbus H1 segments designed per Emerson + ISA-50.02; segment health surfaced on `ff-health` faceplate. |
| FS-INT-HART-01 | URS-INT-HART-01 | HART 7 via CHARMs + multiplexer; secondary variables (e.g., transmitter diagnostics) ingested. |
| FS-INT-WHART-01 | URS-INT-WHART-01 | WirelessHART gateways with join-key rotation per NAMUR NE 124. |
| FS-INT-AD-01 | URS-INT-AD-01 | LDAPS / Kerberos to `tethys.local`; AD groups `DCS-Operator`, `DCS-Senior`, `DCS-Engineer`, `DCS-Eng-Manager`, `DCS-RecipeAuthor`, `DCS-RecipeApprover`, `DCS-PhaseAuthor`, `DCS-PhaseApprover`, `FSE`, `FSE-Approver`. |

### 4.12 Performance / Availability / Backup / Security (URS §5.12)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | Alarm-ack ≤ 1 s + faceplate ≤ 500 ms SLOs measured via synthetic monitoring. |
| FS-AV-01 | URS-AV-01 | Availability ≥ 99.95%; planned maintenance only in down windows. |
| FS-BAK-01 | URS-BAK-01 | Configuration DB nightly + pre-change full-image backup; S3 with object-lock. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore-test + annual full-DR including SIS proof-test integration; QA witness. |
| FS-SEC-01 | URS-SEC-01 | AD-managed accounts; auto-lockout per InfoSec policy. |
| FS-SEC-02 | URS-SEC-02 | Removable-media block via Windows GPO; vendor-approved CR exceptions. |
| FS-SEC-03 | URS-SEC-03 | Tenable Nessus monthly; 30-day SLA on critical findings; vendor-approved patches gated. |
| FS-SEC-04 | URS-SEC-04 | Network segmentation per NAMUR NE 153 documented in `dcs_zone_model.yaml`; allow-list audited. |

### 4.13 Training / Periodic Review (URS §5.13)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Cornerstone LMS curricula per role; SIS roles require IEC 61511 competency certificate. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher `DCS-2026-ANNUAL`. |
| FS-PR-01 | URS-PR-01 | Periodic-review template `TET-PR-DCS-YYYYMMDD`: recipe / phase-logic inventory + alarm-rationalisation drift + SIS proof-test compliance + audit-trail review + deviation summary + training + baseline reconciliation. |


### 4.14 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem with local OT cached credentials for offline operation. Conditional-access binding to policy `OT-DCS Conditional Access (MFA at engineering workstation; operator stations use named-location plus role-bound smart cards)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the DeltaV historian DB plus file-level capture of controller and operator-station configuration; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. CI

| CI | Item | Value |
|---|---|---|
| CI-01 | Redundant App Servers | required |
| CI-02 | SIL 2 partition | supplier-validated; 1oo2D |
| CI-03 | PTP master | required |
| CI-04 | OpStation alarm-ack latency | ≤ 1 s |
| CI-05 | DR test cadence | annual including SIS proof-test |
| CI-06 | Zone model | NAMUR NE 153 |
| CI-07 | FF segment health monitoring | enabled |
| CI-08 | WirelessHART join-key rotation | annual |
| CI-09 | Configuration DB diff tool | `dvdiff` |
| CI-10 | Baseline reconciliation cadence | annual |

## 6. Risks

Phase-logic defect causing miscontrolled CPP (FS-PHL-01..06 + Cat-5 SDLC + simulator regression); recipe-version drift (FS-INT-PASX-01); unauthorised override (FS-BAT-05); SIS bypass (FS-SIS-03 + proof-test); audit-trail tampering (FS-AUD-02); HMI graphic regression (FS-EWS-03 + simulator); FF segment fault (FS-INT-FF-01); WirelessHART join-key compromise (FS-INT-WHART-01 + NE 124).

## 7. References

TET-URS-DCS-001 v1.2; 21 CFR Part 11; EU GMP Annex 11; Annex 1; ICH Q9(R1) / Q10 / Q11; ISA-88; ISA-95; ISA-101; ISA-18.2; ISA-50.02; IEC 61508; IEC 61511; NAMUR NA 102 / NE 33 / NA 65 / NE 159 / NE 153 / NE 124; ISPE GAMP 5 (2nd ed., 2022); ISPE GAMP GPG *Process Control Systems*; PIC/S PI 041; Emerson — *DeltaV v15.3 Reference* + *DeltaV SIS Safety Manual* + *DeltaV Live Reference*.

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-PLAT-01 | FS-PLAT-01 |
| URS-PLAT-02 | FS-PLAT-02 |
| URS-PLAT-03 | FS-PLAT-03 |
| URS-PLAT-04 | FS-PLAT-04 |
| URS-PLAT-05 | FS-PLAT-05 |
| URS-RDN-01 | FS-RDN-01 |
| URS-RDN-02 | FS-RDN-02 |
| URS-RDN-03 | FS-RDN-03 |
| URS-RDN-04 | FS-RDN-04 |
| URS-RDN-05 | FS-RDN-05 |
| URS-REC-01 | FS-REC-01 |
| URS-REC-02 | FS-REC-02 |
| URS-REC-03 | FS-REC-03 |
| URS-REC-04 | FS-REC-04 |
| URS-REC-05 | FS-REC-05 |
| URS-REC-06 | FS-REC-06 |
| URS-REC-07 | FS-REC-07 |
| URS-PHL-01 | FS-PHL-01 |
| URS-PHL-02 | FS-PHL-02 |
| URS-PHL-03 | FS-PHL-03 |
| URS-PHL-04 | FS-PHL-04 |
| URS-PHL-05 | FS-PHL-05 |
| URS-PHL-06 | FS-PHL-06 |
| URS-BAT-01 | FS-BAT-01 |
| URS-BAT-02 | FS-BAT-02 |
| URS-BAT-03 | FS-BAT-03 |
| URS-BAT-04 | FS-BAT-04 |
| URS-BAT-05 | FS-BAT-05 |
| URS-BAT-06 | FS-BAT-06 |
| URS-BAT-07 | FS-BAT-07 |
| URS-ALM-01 | FS-ALM-01 |
| URS-ALM-02 | FS-ALM-02 |
| URS-ALM-03 | FS-ALM-03 |
| URS-ALM-04 | FS-ALM-04 |
| URS-ALM-05 | FS-ALM-05 |
| URS-SIS-01 | FS-SIS-01 |
| URS-SIS-02 | FS-SIS-02 |
| URS-SIS-03 | FS-SIS-03 |
| URS-SIS-04 | FS-SIS-04 |
| URS-HMI-01 | FS-HMI-01 |
| URS-HMI-02 | FS-HMI-02 |
| URS-HMI-03 | FS-HMI-03 |
| URS-HMI-04 | FS-HMI-04 |
| URS-HMI-05 | FS-HMI-05 |
| URS-EWS-01 | FS-EWS-01 |
| URS-EWS-02 | FS-EWS-02 |
| URS-EWS-03 | FS-EWS-03 |
| URS-EWS-04 | FS-EWS-04 |
| URS-EWS-05 | FS-EWS-05 |
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
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-INT-PASX-01 | FS-INT-PASX-01 |
| URS-INT-PASX-02 | FS-INT-PASX-02 |
| URS-INT-HIST-01 | FS-INT-HIST-01 |
| URS-INT-BMS-01 | FS-INT-BMS-01 |
| URS-INT-FF-01 | FS-INT-FF-01 |
| URS-INT-HART-01 | FS-INT-HART-01 |
| URS-INT-WHART-01 | FS-INT-WHART-01 |
| URS-INT-AD-01 | FS-INT-AD-01 |
| URS-PERF-01 | FS-PERF-01 |
| URS-AV-01 | FS-AV-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Phase-logic defect causing miscontrolled critical parameter | Medium | High | URS-PHL-01..06 + regression suite |
| R-02 | Recipe-version drift on download | Low | High | URS-INT-PASX-01 |
| R-03 | Unauthorised override | Low | Medium | URS-BAT-05 |
| R-04 | Audit-trail tampering | Low | High | URS-AUD-02 |
| R-05 | SIS bypass without authorisation | Low | Critical | URS-SIS-03 + proof-test |
| R-06 | Redundant controller failover defect | Low | High | URS-RDN-01 |
| R-07 | Alarm flood overwhelms operator | Medium | Medium | URS-ALM-04 / ISA-18.2 |
| R-08 | HMI graphic regression causing misread of state | Medium | Medium | URS-HMI-04 + EWS regression |
| R-09 | FF segment fault undetected | Medium | Medium | URS-INT-FF-01 |
| R-10 | HART secondary variables unavailable for diagnostics | Low | Medium | URS-INT-HART-01 |
| R-11 | WirelessHART security mis-config | Low | High | URS-INT-WHART-01 + NE 124 |
| R-12 | Configuration-baseline drift from production | Medium | Medium | URS-EWS-05 + PR-01 |
| R-13 | Lost batch transactionality on PAS-X load | Low | High | URS-BAT-01 |
| R-14 | PTP sync degradation impacting audit timestamps | Low | High | URS-PLAT-04 |
| R-15 | SIS proof-test gap → undetected SIF dangerous undetected failure | Low | Critical | URS-SIS-02 + SIL verification |
| R-16 | Annex 1 contamination-control implication of override not assessed | Low | High | (cross-ref site CCS doc) |

Full evaluation in `TET-RA-DCS-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
