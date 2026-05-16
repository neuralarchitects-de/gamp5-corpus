---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (Cat 4 / Tier T2)"
seed_corpus_basis:
  - "CST-FS-COATER-001 v1.2 (parent FS)"
  - "CST-URS-COATER-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd Edition) Category 4 — Configuration Specification conventions"
  - "21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11"
  - "ICH Q9(R1); ICH Q14; ICH Q8(R2); USP <1151>; USP <711>"
  - "ANSI/ISA-88; ANSI/ISA-95; PIC/S PI 041"
parent_fs:
  document_number: CST-FS-COATER-001
  version: "1.2"
  file: "../../../FS_FDS/_generated/final/Castor_Pharmaceuticals_Tablet_Coater_FS_v1.3.md"
parent_urs:
  document_number: CST-URS-COATER-001
  version: "1.2"
  file: "../../../URS/_generated/final/Tablet_Coater_Computer_System__Castor_Pharmaceuticals_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Tablet Coater Computer System — Glatt GC Smart 1500 + GlattView 5

**Document Number:** CST-DS-COATER-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** CST-FS-COATER-001 v1.2
**Parent URS:** CST-URS-COATER-001 v1.2 *(informational, transitive)*
**Site:** Castor Pharmaceuticals Pvt. Ltd., Plant 2, Hyderabad *(fictional)*
**System Owner:** Coating Process Engineer
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (Glatt GC Smart 1500 + GlattView 5 SCADA + Allen-Bradley ControlLogix 5580 PLC)
**Project Mode:** Configuration project on commercial equipment-control software products **Glatt GlattView 5** + **Allen-Bradley ControlLogix 5580** (GAMP 5 Category 4). No site-developed custom code in scope (declarative recipe content + vendor tasklet hooks only).
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; ICH Q9(R1); ICH Q14; ICH Q8(R2); USP <1151>; USP <711>; ANSI/ISA-88; ANSI/ISA-95; PIC/S PI 041.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect — Equipment Control) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Coating Process Engineer) | _____________ | _____________ | _____ |
| Reviewer (PAT Scientist) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Approver (System Owner — Coating Process Engineer) | _____________ | _____________ | _____ |
| Approver (Head of SOD Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Design Control

- **Document Number:** CST-DS-COATER-001
- **Version:** 1.1
- **Effective Date:** 2026-05-15 *(synthetic)*
- **Parent FS:** CST-FS-COATER-001 v1.2
- **Parent URS:** CST-URS-COATER-001 v1.2 *(informational)*
- **Site:** Castor Pharmaceuticals Pvt. Ltd., Plant 2, Hyderabad
- **System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
- **Project Mode:** Configuration only — no site custom code (Cat-5 sub-components excluded per FS scope)
- **Regulatory Scope:** as above

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T2 from parent URS+FS pair. DS covers 65/65 FS-IDs from CST-FS-COATER-001 v1.2. No FS-IDs flagged vendor-internal — Glatt GlattView 5 + ControlLogix configuration surfaces are site-designable; vendor source code (Glatt SDLC, AB firmware) is out of DS scope. NIR chemometric model lifecycle governed externally (`PAT-MODEL-LCM-001`). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from CST-FS-COATER-001 and CST-URS-COATER-001. DS-specific terms:

| Term | Definition |
|---|---|
| LDT | Lyophilization/Coating Data Terminal (Glatt nomenclature) — workstation hosting GlattView 5 |
| GlattView 5 | Glatt's supervisory app on the LDT pair |
| OperatorPanel HMI | Cabinet-mounted HMI |
| LEL | Lower Explosive Limit (organic-variant solvent monitoring) |
| NIR | Near-Infrared (PAT instrument — Bruker MATRIX-F) |
| CIP | Clean-In-Place |

---

## 1. Purpose

This DS specifies the technical design that satisfies the FS `CST-FS-COATER-001` v1.2 for the Castor Plant-2 tablet coater. It records the GlattView 5 + ControlLogix 5580 + cabinet PLC CI inventory; ISA-88 phase + cycle / NIR-endpoint / CIP / solvent-recovery / batch-genealogy workflow + business-rule design; role-permission matrix; per-interface integration design (PAS-X, BMS, Bruker NIR, MasterControl eQMS, AD). Controlling input to IQ / OQ / PQ / RTM `CST-RTM-COATER-001`.

## 2. Scope

**In scope.** Configuration of GlattView 5 active/standby LDT pair, ControlLogix 5580 cabinet PLC, GlattView OperatorPanel HMI, Coating Historian (InfluxDB backend), Grafana read-only trend display, all integrations (PAS-X v3.2, site BMS, Bruker MATRIX-F NIR, MasterControl eQMS, AD), organic-variant LEL interlock.

**Out of scope.** Glatt vendor source code; ControlLogix firmware; physical cabinet mechanical / drum / spray; NIR instrument firmware; LEL detection hardware (separate safety system).

## 3. Architectural Overview

```
                ┌───────────────────────────────────────────────────┐
                │  AD (`castor.local`) │ Site PKI │ PTP master         │
                └────────────────────┬──────────────────────────────┘
                                     │
   ┌─────────────────────────────────▼─────────────────────────────────┐
   │   Process-Control VLAN 421 (no office-network route)               │
   │   ┌───────────────────────────────────────────────────────────┐    │
   │   │  GlattView 5 Active LDT ←─ replication ─→ Standby LDT       │
   │   │  (auto-failover ≤ 30 s)                                      │
   │   │  - Recipe UI │ Cycle UI │ NIR Endpoint Viewer │ CIP UI       │
   │   │  - Coating Historian (InfluxDB) + Grafana (read-only)        │
   │   └───────────────────────────────────────────────────────────┘    │
   │           │ EtherNet/IP        │ REST mTLS     │ OPC UA mTLS       │
   │           ▼                    ▼               ▼                    │
   │   ┌─────────────────┐  ┌─────────────────┐  ┌──────────────────┐  │
   │   │ ControlLogix    │  │ PAS-X v3.2      │  │ Bruker MATRIX-F  │  │
   │   │ 5580 cabinet PLC│  └─────────────────┘  │ NIR (line 1)     │  │
   │   │ + OperatorPanel │                       └──────────────────┘  │
   │   │ + LEL DI (org)  │  ┌─────────────────┐  ┌──────────────────┐  │
   │   └─────────────────┘  │ Site BMS        │  │ MasterControl    │  │
   │                        │ (room pressure) │  │ eQMS (deviation) │  │
   │                        └─────────────────┘  └──────────────────┘  │
   └─────────────────────────────────────────────────────────────────────┘
```

Design choices: LDT pair on UPS ≥ 30 min; PLC + HMI on separate UPS branch; Historian retains ≥ 5 y online, archival to S3 Object Lock.

---

## 4. Configuration Specification

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-COAT-01 | GlattView 5 > LDT Pair Replication | active / standby with PostgreSQL streaming replication; auto-failover ≤ 30 s | Custom | FS-PLAT-01 | FS-PLAT-01 | OQ `OQ-FAILOVER-01` |
| DS-COAT-02 | LDT UPS Hold | ≥ 30 min; PLC + HMI on separate UPS branch | Custom | FS-PLAT-02 | FS-PLAT-02 | IQ `CST-IQ-UPS-01` |
| DS-COAT-03 | Process-Control VLAN | VLAN 421; no office-network route | Custom | FS-PLAT-03 | FS-PLAT-03 | IQ `CST-IQ-NET-01` |
| DS-COAT-04 | Historian Retention | ≥ 5 y online; S3 Object Lock archival | Custom | FS-PLAT-04 | FS-PLAT-04 | OQ `CST-OQ-HIST-RET-01` |
| DS-COAT-05 | GlattView 5 > Recipe State Machine | `DRAFT / REVIEW / APPROVED / EFFECTIVE / OBSOLETE` enforced server-side | Custom | FS-REC-01 | FS-REC-01 | OQ `CST-OQ-REC-STATES-01` |
| DS-COAT-06 | Cycle-Load Endpoint | non-EFFECTIVE → HTTP 409 + audit event | Custom | FS-REC-02 | FS-REC-02 | OQ `CST-OQ-REC-EFF-01` |
| DS-COAT-07 | Transition E-Signature | re-auth; AD-group → role mapping enforced | Custom | FS-REC-03 | FS-REC-03 | OQ `CST-OQ-REC-ESIG-01` |
| DS-COAT-08 | EFFECTIVE Immutability | DB constraint + service guard; revision N+1 in DRAFT | Custom | FS-REC-04 | FS-REC-04 | OQ `CST-OQ-REC-IMMUT-01` |
| DS-COAT-09 | Recipe Download SHA-256 + Version | validated against local approved-recipe registry; mismatch blocks cycle | Custom | FS-REC-05 | FS-REC-05 | OQ `CST-OQ-REC-CKSUM-01` |
| DS-COAT-10 | Recipe Parameter Schema | required: `drum_speed_rpm, inlet_T_set_C, exhaust_T_target_C, spray_rate_g_min, atomising_pressure_bar, gun_to_bed_mm, nozzle_config, batch_kg, weight_gain_pct, tolerances`; out-of-range blocks approval | Custom | FS-REC-06 | FS-REC-06 | OQ `CST-OQ-REC-SCHEMA-01` |
| DS-COAT-11 | Recipe Approval Workflow | Coating Process Engineer e-signature citing scale-up DoE-doc-ID | Custom | FS-REC-07 | FS-REC-07 | OQ `OQ-REC-ENG-SIGNOFF-01` |
| DS-COAT-12 | Recipe-Diff Renderer | JSON-serialised; old/new + change-reason | Custom | FS-REC-08 | FS-REC-08 | OQ `CST-OQ-REC-DIFF-01` |
| DS-COAT-13 | ISA-88 Procedure / Phase Tree | per ANSI/ISA-88 Part 1; state machine per Part 2 (`IDLE, RUNNING, HELD, COMPLETE, ABORTED`) | Custom | FS-S88-01 | FS-S88-01 | OQ `CST-OQ-S88-SM-01` |
| DS-COAT-14 | Phase-Transition Gate | setpoint convergence against recipe band; hold + warning on non-convergence | Custom | FS-S88-02 | FS-S88-02 | OQ `CST-OQ-S88-GATE-01` |
| DS-COAT-15 | Operator-Pause Workflow | HELD state; Senior Operator countersignature with reason to resume | Custom | FS-S88-03 | FS-S88-03 | OQ `CST-OQ-S88-HELD-01` |
| DS-COAT-16 | Cycle Engine Setpoint-Envelope | deviations classified info / warning / critical | Custom | FS-CYC-01 | FS-CYC-01 | OQ `CST-OQ-CYC-ENV-01` |
| DS-COAT-17 | Critical-Alarm Types | loss of spray, drum-motor fault, exhaust-T OOE > 2 min, atomising-pressure loss, NIR-loss (when active) → ack + reason; persistent until acknowledged | Custom | FS-CYC-02 | FS-CYC-02 | OQ `CST-OQ-CRIT-ALARM-01` |
| DS-COAT-18 | Channel Logging | ≥ 1 Hz: drum_speed, inlet_T, exhaust_T, spray_rate (pump-stroke counted), atomising_P, product_T, exhaust_humidity | Custom | FS-CYC-03 | FS-CYC-03 | OQ `CST-OQ-LOG-RATE-01` |
| DS-COAT-19 | PTP Timestamps + LDT Skew Check | > 1 s flips cycle-quality flag | Custom | FS-CYC-04 | FS-CYC-04 | OQ `CST-OQ-PTP-01` |
| DS-COAT-20 | Manual-Override Dual-Sign | Operator + Coating Process Engineer; auto-deviation to MasterControl | Custom | FS-CYC-05 | FS-CYC-05 | OQ `CST-OQ-OVR-01` |
| DS-COAT-21 | Critical-Step Verification Points | loading-complete + spray-complete events; verifier ≠ operator | Custom | FS-CYC-06 | FS-CYC-06 | OQ `CST-OQ-CRIT-VER-01` |
| DS-COAT-22 | Cycle-Abort Sequence | spray off → atomising-air off → drum coasted → drying air maintained until product-T ≤ recipe-limit | Custom | FS-CYC-07 | FS-CYC-07 | OQ `CST-OQ-ABORT-01` |
| DS-COAT-23 | Cumulative Dispensed-Mass Tracker | integrates pump-stroke counts × calibration factor; OOT at spray-complete raises investigation | Custom | FS-CYC-08 | FS-CYC-08 | OQ `CST-OQ-MASS-TRACK-01` |
| DS-COAT-24 | NIR OPC UA Subscription | mTLS; recipe-configured cadence (typ 1-10 Hz) | Custom | FS-NIR-01 / FS-INT-PAT-01 | FS-NIR-01, FS-INT-PAT-01 | OQ `CST-OQ-NIR-SUB-01` |
| DS-COAT-25 | NIR Chemometric Model Loader | cosign verify + model-id + version match recipe + log fingerprint; failure blocks cycle | Custom | FS-NIR-02 | FS-NIR-02 | OQ `CST-OQ-NIR-LOAD-01` |
| DS-COAT-26 | NIR Signal-Loss Watchdog | ≥ 3 missed samples → critical alarm + fall-back to time-based spray-end; disposition gate "Coating Process Engineer review required" | Custom | FS-NIR-03 | FS-NIR-03 | OQ `CST-OQ-NIR-LOSS-01` |
| DS-COAT-27 | NIR Spray-End Decision Log | `(model-id, version, input-spectrum-hash, predicted-thickness, decision-threshold, decision-result)` | Custom | FS-NIR-04 | FS-NIR-04 | OQ `CST-OQ-NIR-DECISION-01` |
| DS-COAT-28 | NIR Model Deployment Workflow | PAT Scientist + Coating Process Engineer + QA signatures + model-validation-doc-ID; idle-tested on recorded run before production | Custom | FS-NIR-05 | FS-NIR-05 | OQ `CST-OQ-NIR-DEPLOY-01` |
| DS-COAT-29 | CIP Cycle Templates | pre-rinse / caustic / rinse / acid / final-rinse phase recording | Custom | FS-CIP-01 | FS-CIP-01 | OQ `CST-OQ-CIP-01` |
| DS-COAT-30 | CIP Acceptance | rinse-water conductivity threshold, optional TOC; fail flips `coater.state=CIP_FAIL` blocking subsequent cycles | Custom | FS-CIP-02 | FS-CIP-02 | OQ `CST-OQ-CIP-ACC-01` |
| DS-COAT-31 | Campaign-End CIP Workflow | required after recipe-family change; Coating Process Engineer + Quality Reviewer signatures | Custom | FS-CIP-03 | FS-CIP-03 | OQ `CST-OQ-CIP-CAMP-01` |
| DS-COAT-32 | LEL Channel (organic variant) | dedicated DI; LEL ≥ 25% → hard-wired emergency-stop relay isolates spray + ramps drying-air; software event logged + alarm | Custom | FS-SOLV-01 / IF-LEL-01 | FS-SOLV-01 | OQ `CST-OQ-LEL-01` |
| DS-COAT-33 | Condenser-Exhaust + Condensate-Mass-Flow Channels | logged ≥ 1 Hz; out-of-envelope alarm | Custom | FS-SOLV-02 | FS-SOLV-02 | OQ `CST-OQ-COND-01` |
| DS-COAT-34 | Solvent Genealogy Fields | `(fresh_lot, recovered_batch_ref)` captured at campaign start; rendered in cycle report | Custom | FS-SOLV-03 | FS-SOLV-03 | OQ `CST-OQ-SOLV-GEN-01` |
| DS-COAT-35 | Cycle Record → PAS-X EBR Binding | `batch_id + step_id`; downstream-step gate checked via callback | Custom | FS-GEN-01 / FS-INT-PASX-03 | FS-GEN-01 | OQ `CST-OQ-EBR-BIND-01` |
| DS-COAT-36 | Input-Genealogy Capture | `suspension_lot, sub_coat_lot[], tablet_core_lot` at recipe-load; verified vs MBR; mismatch blocks | Custom | FS-GEN-02 | FS-GEN-02 | OQ `CST-OQ-INPUT-GEN-01` |
| DS-COAT-37 | Weight-Gain Calculation | `(post − pre) / pre`; target + actual + ± tolerance in cycle-report cover sheet | Custom | FS-GEN-03 | FS-GEN-03 | OQ `OQ-WEIGHT-GAIN-CALC-01` |
| DS-COAT-38 | Audit Trail Coverage | recipe events + cycle events + alarm acks + signatures; PTP timestamps | Custom | FS-AUD-01 | FS-AUD-01 | OQ `CST-OQ-AUDIT-COV-01` |
| DS-COAT-39 | Audit Append-Only DB | revoked DELETE/UPDATE; DBA dual control | Custom | FS-AUD-02 | FS-AUD-02 | OQ `CST-OQ-AUDIT-APPEND-01` |
| DS-COAT-40 | Per-Batch QR Audit Review UI | quarterly QA-Compliance platform review | Custom | FS-AUD-03 | FS-AUD-03 | OQ `CST-OQ-AUDIT-REV-01` |
| DS-COAT-41 | 25-Y Immutable Cold Storage | S3 Object-Lock Compliance Mode | Custom | FS-AUD-04 | FS-AUD-04 | (governance) |
| DS-COAT-42 | Signature Render | printed name + ts + meaning into audit + PDFs | Custom | FS-PART11-01 | FS-PART11-01 | OQ `CST-OQ-SIG-RENDER-01` |
| DS-COAT-43 | User-ID Uniqueness | AD-enforced; reused-id blocked | Custom | FS-PART11-02 | FS-PART11-02 | OQ `CST-OQ-USERID-01` |
| DS-COAT-44 | PKI-Signed Signature Payload | `(record-id, hash, signer-id, meaning, ts)`; tamper detection on read | Custom | FS-PART11-03 | FS-PART11-03 | OQ `CST-OQ-SIG-PKI-01` |
| DS-COAT-45 | SoD at Signing API | conflicts rejected | Custom | FS-PART11-04 | FS-PART11-04 | OQ `CST-OQ-SOD-01` |
| DS-COAT-46 | Re-Auth + MFA at Every Signature | cached creds disabled | Custom | FS-PART11-05 | FS-PART11-05 | OQ `CST-OQ-REAUTH-01` |
| DS-COAT-47 | AD Password Policy | per `SEC-AD-POLICY-001` | Custom | FS-PART11-06 | FS-PART11-06 | (governance) |
| DS-COAT-48 | Audit Coverage + Export | per § 11.10(b)/(c)/(e) | Custom | FS-PART11-07 | FS-PART11-07 | OQ `CST-OQ-PART11-COV-01` |
| DS-COAT-49 | PAS-X Recipe Download (mTLS) | SHA-256 + version + cert-chain validation | Custom | FS-INT-PASX-01 | FS-INT-PASX-01 | OQ `CST-OQ-PASX-IN-01` |
| DS-COAT-50 | Cycle Report POST | within 30 min; exponential-backoff retry | Custom | FS-INT-PASX-02 | FS-INT-PASX-02 | OQ `CST-OQ-PASX-OUT-01` |
| DS-COAT-51 | PAS-X Downstream-Gate REST Callback | cleared only after Quality Reviewer approval | Custom | FS-INT-PASX-03 | FS-INT-PASX-03 | OQ `CST-OQ-PASX-CB-01` |
| DS-COAT-52 | BMS Room-Pressure OPC UA | loss aborts loading | Custom | FS-INT-BMS-01 | FS-INT-BMS-01 | OQ `CST-OQ-BMS-01` |
| DS-COAT-53 | NIR Cert Auto-Rotation Runbook | OPC UA cert lifecycle | Custom | FS-INT-PAT-01 | FS-INT-PAT-01 | (cert-manager) |
| DS-COAT-54 | AD Auth + Vault Service Accounts | short-lived secrets | Custom | FS-INT-AD-01 / FS-SEC-01 | FS-INT-AD-01, FS-SEC-01 | OQ `CST-OQ-AD-VAULT-01` |
| DS-COAT-55 | AD User-ID Attribution | all writes attributed | Custom | FS-DI-01 | FS-DI-01 | OQ `CST-OQ-DI-ATTRIB-01` |
| DS-COAT-56 | Cycle-Report Export (PDF + CSV) | OQ-validated | Custom | FS-DI-02 | FS-DI-02 | OQ `OQ-EXPORT-01` |
| DS-COAT-57 | PTP Skew Gate at Signature | > 5 s rejects | Custom | FS-DI-03 | FS-DI-03 | OQ `CST-OQ-PTP-AUDIT-01` |
| DS-COAT-58 | Originals Immutable + Derivations Separate | | Custom | FS-DI-04 | FS-DI-04 | OQ `CST-OQ-DI-LIN-01` |
| DS-COAT-59 | Spray-Mass + Weight-Gain Engine Deterministic | per `OQ-CALC-01` | Custom | FS-DI-05 | FS-DI-05 | OQ `OQ-CALC-01` |
| DS-COAT-60 | 25-Y Retention + 4-h Retrieval | inspection-readiness runbook | Custom | FS-DI-06 | FS-DI-06 | OQ `CST-OQ-RETR-01` |
| DS-COAT-61 | InfluxDB Backup | nightly snapshot + continuous WAL → S3 Object-Lock; PITR 30 d | Custom | FS-BAK-01 | FS-BAK-01 | OQ `CST-OQ-BAK-01` |
| DS-COAT-62 | Quarterly Restore Test | DBA + QA witness | Custom | FS-BAK-02 | FS-BAK-02 | PR-01 |
| DS-COAT-63 | RTO / RPO | RTO ≤ 4 h documented; RPO ≤ 1 min via streaming replication | Custom | FS-BAK-03 | FS-BAK-03 | OQ `CST-OQ-DR-01` |
| DS-COAT-64 | Sustained ≥ 1 Hz Logging | full cycle (2-6 h) | Custom | FS-PERF-01 | FS-PERF-01 | PQ `PQ-PERF-DATA-LOG-01` |
| DS-COAT-65 | HMI Alarm-Ack Latency | ≤ 1 s | Custom | FS-PERF-02 | FS-PERF-02 | OQ `CST-OQ-HMI-ACK-01` |
| DS-COAT-66 | AD-Managed Accounts | break-glass admin only with dual control | Custom | FS-SEC-01 | FS-SEC-01 | OQ `CST-OQ-SEC-ACC-01` |
| DS-COAT-67 | Removable-Media GPO | block-by-default; CR exception path | Custom | FS-SEC-02 | FS-SEC-02 | OQ `CST-OQ-USB-01` |
| DS-COAT-68 | Tenable Nessus Monthly | criticals 30 d | Custom | FS-SEC-03 | FS-SEC-03 | (governance) |
| DS-COAT-69 | LMS-Gated Production Access | AD-group ↔ LMS completion attribute | Custom | FS-TRN-01 | FS-TRN-01 | (governance) |
| DS-COAT-70 | Annual Refresher + PAT-Scientist Competency | workflow | Custom | FS-TRN-02 | FS-TRN-02 | (governance) |
| DS-COAT-71 | Periodic-Review Runbook | recipe inventory + change history + alarm trends + audit-trail review + deviation summary + NIR-model register + CIP outcomes + training currency | Custom | FS-PR-01 | FS-PR-01 | PR-01 |
| DS-COAT-72 | AD Conditional Access `OT-Equipment Conditional Access` | MFA at HMI session start; local cache validates last 24 h; SIEM → Splunk `gxp-authn`; CyberArk PAM break-glass | Custom | FS-XSYS-AD-01 | FS-XSYS-AD-01 | OQ `CST-OQ-CONDACC-01` |
| DS-COAT-73 | Veeam Backup | App-aware MS SQL VSS for recipe / cycle DB + file-level EBR capture; tier T2; RPO ≤ 24 h; RTO ≤ 24 BH; S3 Compliance + LTO-9 monthly | Custom | FS-XSYS-BAK-01 | FS-XSYS-BAK-01 | OQ `CST-OQ-VEEAM-01` |

---

## 5. Workflow + Business-Rule Design

### 5.1 Cycle-Execution Workflow

```
Recipe LOAD (EFFECTIVE only, checksum verified) →
ISA-88 Procedure → Unit Procedure → Operation → Phase →
Phase state: IDLE → RUNNING (setpoint convergence per FS-S88-02) →
Channel logging ≥ 1 Hz →
Critical alarms → ack + reason → persistent →
Manual override (if needed) → dual-sign Op + Coating Process Engineer →
auto-deviation MasterControl →
Critical-step verification (loading + spray complete; verifier ≠ operator) →
NIR endpoint OR time-based fallback (if NIR-loss) →
Cycle-abort sequence (if needed): spray off → air off → drum coasted → drying maintained
Phase → HELD / COMPLETE / ABORTED →
Cycle-report POST to PAS-X within 30 min →
Quality Reviewer signs downstream-gate callback
```

### 5.2 Recipe-Approval Workflow

| Transition | Required signatures |
|---|---|
| DRAFT → REVIEW | Author `authorship` |
| REVIEW → APPROVED | Coating Process Engineer + PAT Scientist + CSV Reviewer `review`; scale-up DoE-doc-ID cited |
| APPROVED → EFFECTIVE | Head of SOD Manufacturing + Head of QA `approval` (dual-sign) |
| EFFECTIVE → OBSOLETE | Coating Lead `retirement` |

### 5.3 CIP Workflow Rules

- **Phase sequence:** pre-rinse → caustic → rinse → acid → final-rinse (DS-COAT-29)
- **Acceptance:** rinse-water conductivity ≤ recipe threshold; optional TOC; failure → `coater.state=CIP_FAIL` blocking subsequent cycles (DS-COAT-30)
- **Campaign-end CIP:** required after recipe-family change; Coating Process Engineer + Quality Reviewer dual-sign (DS-COAT-31)

### 5.4 LEL Interlock Decision Tree (organic variant)

```
LEL channel reading (DI from site LEL system)
     │
     ▼
LEL ≥ 25%?
     ├─ Yes → Hard-wired emergency-stop relay activates →
     │         spray isolation + drying-air ramp + software event log + critical alarm
     └─ No  → continue cycle; LEL channel logged ≥ 1 Hz to historian
```

### 5.5 NIR Endpoint Decision Rules

- Endpoint criterion = `recipe.endpoint_method` (enum: `time_based / nir_thickness / pump_strokes`)
- If `nir_thickness`: monitor predicted thickness vs target; spray-end when ≥ target ± tolerance
- If NIR-loss watchdog fires (≥ 3 missed samples): fall back to time-based (DS-COAT-26); disposition gate set to "Coating Process Engineer review required"

### 5.6 Manual-Override Rule

Manual setpoint override during product cycle requires Operator + Coating Process Engineer dual signature with reason ≥ 10 chars (DS-COAT-20); auto-creates MasterControl deviation; cycle continues with `override_flag=true` on cycle profile.

### 5.7 Critical-Step Verification Rule

Loading-complete and spray-complete events are critical-step verification points (DS-COAT-21). Second-person verification widget mandatory; verifier user-id ≠ operator user-id (enforced at server-side API).

---

## 6. Role-Permission Matrix Design

| AD Group | View HMI | Ack WARN | Ack CRIT | Author recipe | Approve recipe | Sign override | Sign CIP campaign-end | NIR model deploy | Audit export | Admin |
|---|---|---|---|---|---|---|---|---|---|---|
| `Coater-Operator` | Y | Y | — | — | — | initiate | — | — | — | — |
| `Coater-Senior-Operator` | Y | Y | Y | — | — | countersign | — | — | — | — |
| `Coater-Process-Engineer` | Y | — | — | review | — | countersign | sign | review | — | — |
| `Coater-Recipe-Author` | Y | — | — | Y | — | — | — | — | — | — |
| `Coater-Recipe-Approver` | Y | — | — | review | approve | — | — | — | — | — |
| `Coater-PAT-Scientist` | Y | — | — | review | — | — | — | author + sign | — | — |
| `Coater-Quality-Reviewer` | Y | — | — | — | — | — | sign | review | Y | — |
| `Coater-CSV-Reviewer` | Y (RO) | — | — | — | review (CSV) | — | — | review | Y | — |
| `Coater-Auditor` | Y (RO) | — | — | — | — | — | — | — | Y | — |
| Break-glass DBA (vaulted) | — | — | — | — | — | — | — | — | — | DB |

FS-IDs traced: FS-INT-AD-01, FS-PART11-04 (SoD), FS-CYC-05 (override), FS-NIR-05 (NIR deploy), FS-CIP-03 (campaign-end CIP).

---

## 7. Integration Design

### 7.1 IF-PASX-01..03 (Werum PAS-X v3.2)

- Recipe download (REST mTLS, SHA-256 + version validated)
- Cycle-report POST within 30 min (exponential backoff)
- Downstream-step gate callback after Quality Reviewer approval
- FS-IDs: FS-INT-PASX-01..03

### 7.2 IF-PLC-01 (ControlLogix 5580)

- Protocol: EtherNet/IP bidirectional (tag values + alarms)
- FS-IDs: FS-CYC-*

### 7.3 IF-BMS-01 (Site BMS)

- Protocol: OPC UA (room-pressure interlock)
- Behaviour: loss aborts loading
- FS-IDs: FS-INT-BMS-01

### 7.4 IF-NIR-01 (Bruker MATRIX-F)

- Protocol: OPC UA mTLS; cert auto-rotation runbook
- Cadence: recipe-defined (typ 1-10 Hz)
- FS-IDs: FS-NIR-01, FS-INT-PAT-01

### 7.5 IF-AD-01 (AD / PKI)

- Protocol: LDAPS + Kerberos; service accounts via HashiCorp Vault
- FS-IDs: FS-INT-AD-01, FS-SEC-01

### 7.6 IF-EQMS-01 (MasterControl)

- REST outbound: auto-deviation on override
- FS-IDs: FS-CYC-05

### 7.7 IF-LEL-01 (Site LEL system — organic variant)

- Hard-wired DI + Modbus
- FS-IDs: FS-SOLV-01

### 7.8 Integration Risk Register

| Interface | Risk | Mitigation |
|---|---|---|
| IF-PASX | cert expiry | cert-manager 365-d rotation |
| IF-NIR | OPC UA cert expiry | cert-manager + 30-d alert |
| IF-BMS | OPC UA outage | local-cache + alarm on prolonged loss |
| IF-LEL | sensor blind spot (organic variant) | redundant sensors mandated per `EQ-COATER-001` |
| IF-AD | outage | local OT-cached creds 24 h |

---

## 8. Site-Deployed Components

**None in scope.** Per FS § 9 Constraints: *"Glatt GlattView core code vendor-controlled; site customisation limited to declarative recipe content + tasklet hooks; NIR chemometric model lifecycle governed externally."* No Cat-5 site code is delivered with this system; therefore § 8 mini-SDS is not required per § 2B.4 rule 6.

The NIR chemometric model lifecycle is governed externally under `PAT-MODEL-LCM-001` and referenced via DS-COAT-25 / DS-COAT-28 only.

---

## 9. References

### US
- 21 CFR Part 11; 21 CFR Part 211
- FDA CSA (final, February 2026)

### EU
- EU GMP Annex 11
- EU GMP Annex 15

### DACH
- AMWHV
- BSI IT-Grundschutz baseline

### International
- ISPE GAMP 5 (2nd ed., 2022)
- ICH Q9(R1); ICH Q14; ICH Q8(R2)
- USP <1151>; USP <711>
- ANSI/ISA-88 Part 1 + Part 2; ANSI/ISA-95 Part 1
- PIC/S PI 041
- ISO/IEC 27001:2022

### Vendor
- Glatt — *GC Smart 1500 + GlattView 5 Configuration Reference*
- Bruker — *MATRIX-F NIR Operation Manual*
- Allen-Bradley / Rockwell — *ControlLogix 5580 Reference*
- Werum / Körber — *PAS-X v3.2 Integration Guide*

### Site
- `CST-URS-COATER-001` v1.2 (informational)
- `CST-FS-COATER-001` v1.2 (parent)
- `PAT-MODEL-LCM-001` (NIR chemometric model lifecycle, external)
- `CST-PR-COATER-YYYYMMDD` (periodic-review template)
- `EQ-COATER-001` (equipment qualification)

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-COAT-01 | FS-PLAT-01 |
| DS-COAT-02 | FS-PLAT-02 |
| DS-COAT-03 | FS-PLAT-03 |
| DS-COAT-04 | FS-PLAT-04 |
| DS-COAT-05 | FS-REC-01 |
| DS-COAT-06 | FS-REC-02 |
| DS-COAT-07 | FS-REC-03 |
| DS-COAT-08 | FS-REC-04 |
| DS-COAT-09 | FS-REC-05 |
| DS-COAT-10 | FS-REC-06 |
| DS-COAT-11 | FS-REC-07 |
| DS-COAT-12 | FS-REC-08 |
| DS-COAT-13 | FS-S88-01 |
| DS-COAT-14 | FS-S88-02 |
| DS-COAT-15 | FS-S88-03 |
| DS-COAT-16 | FS-CYC-01 |
| DS-COAT-17 | FS-CYC-02 |
| DS-COAT-18 | FS-CYC-03 |
| DS-COAT-19 | FS-CYC-04 |
| DS-COAT-20 | FS-CYC-05 |
| DS-COAT-21 | FS-CYC-06 |
| DS-COAT-22 | FS-CYC-07 |
| DS-COAT-23 | FS-CYC-08 |
| DS-COAT-24 | FS-NIR-01 / FS-INT-PAT-01 |
| DS-COAT-25 | FS-NIR-02 |
| DS-COAT-26 | FS-NIR-03 |
| DS-COAT-27 | FS-NIR-04 |
| DS-COAT-28 | FS-NIR-05 |
| DS-COAT-29 | FS-CIP-01 |
| DS-COAT-30 | FS-CIP-02 |
| DS-COAT-31 | FS-CIP-03 |
| DS-COAT-32 | FS-SOLV-01 |
| DS-COAT-33 | FS-SOLV-02 |
| DS-COAT-34 | FS-SOLV-03 |
| DS-COAT-35 | FS-GEN-01 / FS-INT-PASX-03 |
| DS-COAT-36 | FS-GEN-02 |
| DS-COAT-37 | FS-GEN-03 |
| DS-COAT-38 | FS-AUD-01 |
| DS-COAT-39 | FS-AUD-02 |
| DS-COAT-40 | FS-AUD-03 |
| DS-COAT-41 | FS-AUD-04 |
| DS-COAT-42 | FS-PART11-01 |
| DS-COAT-43 | FS-PART11-02 |
| DS-COAT-44 | FS-PART11-03 |
| DS-COAT-45 | FS-PART11-04 |
| DS-COAT-46 | FS-PART11-05 |
| DS-COAT-47 | FS-PART11-06 |
| DS-COAT-48 | FS-PART11-07 |
| DS-COAT-49 | FS-INT-PASX-01 |
| DS-COAT-50 | FS-INT-PASX-02 |
| DS-COAT-51 | FS-INT-PASX-03 |
| DS-COAT-52 | FS-INT-BMS-01 |
| DS-COAT-53 | FS-INT-PAT-01 |
| DS-COAT-54 | FS-INT-AD-01 / FS-SEC-01 |
| DS-COAT-55 | FS-DI-01 |
| DS-COAT-56 | FS-DI-02 |
| DS-COAT-57 | FS-DI-03 |
| DS-COAT-58 | FS-DI-04 |
| DS-COAT-59 | FS-DI-05 |
| DS-COAT-60 | FS-DI-06 |
| DS-COAT-61 | FS-BAK-01 |
| DS-COAT-62 | FS-BAK-02 |
| DS-COAT-63 | FS-BAK-03 |
| DS-COAT-64 | FS-PERF-01 |
| DS-COAT-65 | FS-PERF-02 |
| DS-COAT-66 | FS-SEC-01 |
| DS-COAT-67 | FS-SEC-02 |
| DS-COAT-68 | FS-SEC-03 |
| DS-COAT-69 | FS-TRN-01 |
| DS-COAT-70 | FS-TRN-02 |
| DS-COAT-71 | FS-PR-01 |
| DS-COAT-72 | FS-XSYS-AD-01 |
| DS-COAT-73 | FS-XSYS-BAK-01 |

---

## 11. Design-level Risk Register

Per § 2B.8. Formal RA in `CST-RA-COATER-001` (synthetic).

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| DR-01 | Undetected sensor failure causing miscontrolled product temperature | Medium | High | DS-COAT-17 critical alarms + redundant probes per `EQ-COATER-001` |
| DR-02 | Recipe-version drift on download | Medium | High | DS-COAT-09 SHA-256 + version + cert chain |
| DR-03 | Unauthorised manual override | Medium | High | DS-COAT-20 dual signature + auto-deviation |
| DR-04 | Audit-trail tampering | Low | Critical | DS-COAT-39 append-only + DBA dual control |
| DR-05 | Coating-uniformity drift (CV > acceptance) due to spray-rate sensor drift | Medium | High | DS-COAT-18 channel coverage + sensor-calibration program |
| DR-06 | NIR-model drift causing premature spray-end | Medium | High | DS-COAT-27 deterministic decision + DS-COAT-28 model deployment workflow + model-life monitoring |
| DR-07 | NIR signal loss during product cycle | Medium | Medium | DS-COAT-26 watchdog + time-based fallback + engineering disposition |
| DR-08 | Solvent LEL excursion (organic variant) without trip | Low | Critical | DS-COAT-32 LEL interlock + redundant sensors mandated per `EQ-COATER-001` |
| DR-09 | CIP cycle bypass leading to cross-contamination | Low | Critical | DS-COAT-30 CIP_FAIL state-gate + DS-COAT-31 campaign-end gate |
| DR-10 | Batch-genealogy break between coater + EBR | Low | High | DS-COAT-35 cycle-EBR binding |
| DR-11 | Spray-gun blockage undetected mid-cycle | Medium | Medium | DS-COAT-17 atomising-pressure-loss alarm |
| DR-12 | LDT failover (DS-COAT-01) during active spray phase | Low | Medium | OQ verified failover; resume state machine from HELD |
| DR-13 | NIR cert (DS-COAT-53) rotation mid-cycle stalls subscription | Low | Medium | Pre-cycle cert-validity check + 30-d alert |
| DR-14 | Pump-stroke calibration factor (DS-COAT-23) drifts silently | Medium | Medium | Sensor-calibration program + at-OQ regression dataset |
| DR-15 | Veeam VSS backup contention during full-cycle write | Low | Low | Backup window outside cycle hours |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
