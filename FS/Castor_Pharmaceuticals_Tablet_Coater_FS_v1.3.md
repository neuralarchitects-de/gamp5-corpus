---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; v1.2 enrichment 2026-05-13"
seed_corpus_basis:
  - "CST-URS-COATER-001 (parent URS)"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; ICH Q9; ICH Q14; ANSI/ISA-88"
parent_urs:
  document_number: CST-URS-COATER-001
  version: 1.2
  file: ../../URS/_generated/final/Tablet_Coater_Computer_System__Castor_Pharmaceuticals_URS_v1.3.md
do_not_use_as:
  - regulated_record
  - basis_for_real_validation_decisions
intended_use:
  - LLM fine-tuning corpus seed
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Tablet Coater Computer System — Glatt GC Smart 1500 + GlattView 5

**Document Number:** CST-FS-COATER-001
**Version:** 1.2
**Effective Date:** 2026-05-13 *(synthetic)*
**Parent URS:** CST-URS-COATER-001 v1.2
**Site:** Castor Pharmaceuticals Pvt. Ltd., Plant 2, Hyderabad *(fictional)*
**System Class:** GAMP Cat 4 — Configured Product
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; ICH Q9; ICH Q14; PIC/S PI 041; ANSI/ISA-88

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Coating Process Engineer) | _____________ | _____________ | _____ |
| Reviewer (PAT Scientist) | _____________ | _____________ | _____ |
| Approver (Head of SOD Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue, derived from CST-URS-COATER-001 v1.0. |
| 1.2 | 2026-05-13 | (synthetic) | Expanded to per-URS-ID specifications (no range compression) per METHODOLOGY § 2A.7. Added ISA-88 phase, NIR endpoint feedback, CIP, solvent-recovery (organic variant), batch genealogy. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies how Glatt GC Smart 1500 + GlattView 5 are configured and integrated to satisfy `CST-URS-COATER-001` v1.2.

## 2. Scope

Per parent URS § 2. In scope: cabinet + PLC + GlattView 5 on redundant LDT pair + Historian + PAS-X / BMS / NIR PAT / AD integrations.

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source / Vendor | Notes |
|---|---|---|---|---|---|
| C-01 | GC Smart 1500 cabinet | Equipment | (equipment) | Glatt | mechanical / drum / spray |
| C-02 | ControlLogix 5580 PLC | Embedded | 4 | Allen-Bradley | EtherNet/IP |
| C-03 | GlattView OperatorPanel HMI | Embedded HMI | 4 | Glatt | cabinet-mounted |
| C-04 | GlattView 5 active LDT | COTS app | 4 | Glatt | Win 11 IoT LTSC |
| C-05 | GlattView 5 standby LDT | COTS app | 4 | Glatt | auto-failover |
| C-06 | Coating Historian | COTS app | 4 | Glatt | InfluxDB backend |
| C-07 | Grafana | COTS viz | (read-only) | Grafana Labs | trend display |
| C-08 | PAS-X v3.2 | COTS MES | 4 | Werum / Körber | recipe + batch report |
| C-09 | Site BMS | COTS BMS | 4 | (site) | room-pressure interlock |
| C-10 | Bruker MATRIX-F NIR | PAT instrument | 4 | Bruker | line 1 only |
| C-11 | LEL monitoring system | Safety system | (separate) | (site) | organic variant only |
| C-12 | AD / PKI | COTS infra | (infra) | Microsoft | AuthN + sig certs |

### 3.2 Logical Architecture

```
                ┌────────────────────────────────────────────────┐
                │  Active Directory + Site PKI + PTP master       │
                └──────────────┬─────────────────────────────────┘
                               │
                               ▼
   ┌────────────────────────────────────────────────────────────────┐
   │      GlattView 5 Active LDT  ←──→  Standby LDT (auto ≤ 30 s)   │
   │      Recipe UI │ Cycle UI │ NIR Endpoint Viewer │ CIP UI         │
   │      Historian (InfluxDB) + Grafana                              │
   └────────┬──────────────────┬──────────────────┬──────────────────┘
            │ EtherNet/IP      │ REST mTLS        │ OPC UA mTLS
            ▼                  ▼                  ▼
   ┌────────────────────┐  ┌──────────────────┐  ┌──────────────────┐
   │ ControlLogix 5580  │  │ PAS-X v3.2       │  │ Bruker NIR PAT    │
   │ (cabinet PLC)      │  └──────────────────┘  │ (line 1)          │
   │                    │                        └──────────────────┘
   │ + HMI panel        │  ┌──────────────────┐
   │ + LEL inputs (org) │  │ Site BMS         │
   └────────────────────┘  └──────────────────┘
```

### 3.3 Functional Modules

| Module | URS sections |
|---|---|
| M-PLAT | URS-PLAT-* |
| M-REC | URS-REC-* |
| M-S88 | URS-S88-* |
| M-CYC | URS-CYC-* |
| M-NIR | URS-NIR-* |
| M-CIP | URS-CIP-* |
| M-SOLV | URS-SOLV-* |
| M-GEN | URS-GEN-* |
| M-AUD | URS-AUD-* |
| M-PART11 | URS-PART11-* |
| M-INT | URS-INT-* |
| M-DI | URS-DI-* |
| M-PERF | URS-PERF-*, URS-BAK-* |
| M-SEC | URS-SEC-* |
| M-TRN | URS-TRN-* |
| M-PR | URS-PR-* |

## 4. Functional Specifications

### 4.1 Platform / Hardware (M-PLAT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | Active / standby LDT pair; PostgreSQL streaming replication; auto-failover ≤ 30 s; verified `OQ-FAILOVER-01`. |
| FS-PLAT-02 | URS-PLAT-02 | LDTs on UPS ≥ 30 min; PLC + HMI on separate UPS branch. |
| FS-PLAT-03 | URS-PLAT-03 | Process-control VLAN (VLAN 421); no office-network route. |
| FS-PLAT-04 | URS-PLAT-04 | Historian retains ≥ 5 y online; archival to S3 Object Lock. |

### 4.2 Recipe / Parameter Lifecycle (M-REC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REC-01 | URS-REC-01 | Recipe state machine {DRAFT, REVIEW, APPROVED, EFFECTIVE, OBSOLETE} enforced server-side; transitions validated. |
| FS-REC-02 | URS-REC-02 | Cycle-load endpoint rejects non-EFFECTIVE recipes with HTTP 409 + audit event. |
| FS-REC-03 | URS-REC-03 | Re-authenticated electronic signature at each transition; AD-group → role mapping enforced. |
| FS-REC-04 | URS-REC-04 | EFFECTIVE recipes immutable (DB constraint + service guard); change creates revision N+1 in DRAFT. |
| FS-REC-05 | URS-REC-05 | Recipe download with SHA-256 + version validated against local approved-recipe registry; mismatch blocks cycle. |
| FS-REC-06 | URS-REC-06 | Recipe-parameter schema validates: drum_speed_rpm, inlet_T_set_C, exhaust_T_target_C, spray_rate_g_min, atomising_pressure_bar, gun_to_bed_mm, nozzle_config, batch_kg, weight_gain_pct, plus tolerances; missing / out-of-range fields block approval. |
| FS-REC-07 | URS-REC-07 | Recipe-approval workflow requires Coating Process Engineer e-signature citing scale-up DoE-doc-ID; verified `OQ-REC-ENG-SIGNOFF-01`. |
| FS-REC-08 | URS-REC-08 | Recipe-diff renderer (JSON-serialised) presents changed fields with old/new + change-reason. |

### 4.3 ISA-88 Phase Model (M-S88)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-S88-01 | URS-S88-01 | Procedure / Unit Procedure / Operation / Phase tree implemented per ANSI/ISA-88 Part 1; state machine per Part 2 (IDLE, RUNNING, HELD, COMPLETE, ABORTED). |
| FS-S88-02 | URS-S88-02 | Phase-transition gate evaluates setpoint convergence against recipe band; hold + warning on non-convergence. |
| FS-S88-03 | URS-S88-03 | Operator pause transitions current phase to HELD; resume requires Senior Operator countersignature with reason. |

### 4.4 Cycle Execution / Data Capture (M-CYC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CYC-01 | URS-CYC-01 | Cycle engine evaluates setpoint envelopes; deviations classified info / warning / critical. |
| FS-CYC-02 | URS-CYC-02 | Critical-alarm types (loss of spray, drum-motor fault, exhaust-T OOE > 2 min, atomising-pressure loss, NIR-loss when active) require ack + reason; persistent until acknowledged. |
| FS-CYC-03 | URS-CYC-03 | Channels logged ≥ 1 Hz: drum_speed, inlet_T, exhaust_T, spray_rate (gun pump strokes counted), atomising_P, product_T, exhaust_humidity. |
| FS-CYC-04 | URS-CYC-04 | PTP-derived timestamps; LDT clock-skew check; > 1 s flips cycle-quality flag. |
| FS-CYC-05 | URS-CYC-05 | Manual override during product cycle requires Operator + Coating Process Engineer dual signature; auto-deviation to MasterControl eQMS. |
| FS-CYC-06 | URS-CYC-06 | Loading-complete + spray-complete events configured as critical-step verification points; verifier user-id ≠ operator user-id. |
| FS-CYC-07 | URS-CYC-07 | Cycle-abort sequence: spray off, atomising-air off, drum coasted, drying air maintained until product-T ≤ recipe-limit. |
| FS-CYC-08 | URS-CYC-08 | Cumulative dispensed-mass tracker integrates pump-stroke counts × calibration factor; at spray-complete compares vs recipe target ± tolerance; out-of-tolerance raises investigation. |

### 4.5 NIR Endpoint Detection (M-NIR)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-NIR-01 | URS-NIR-01 | NIR predictions consumed via OPC UA mTLS at recipe-configured cadence; subscription lifecycle managed by NIR-adapter service. |
| FS-NIR-02 | URS-NIR-02 | Chemometric model load workflow: verify cosign signature, verify model-id + version match recipe, log model-fingerprint; failure blocks cycle. |
| FS-NIR-03 | URS-NIR-03 | NIR-signal-loss watchdog (≥ 3 missed samples) triggers critical alarm + falls back to time-based spray-end per recipe contingency; cycle disposition gate set to "Coating Process Engineer review required". |
| FS-NIR-04 | URS-NIR-04 | NIR spray-end decision logged with: model-id + version, input spectrum hash, predicted thickness, decision threshold, decision result; reconstructable from logs. |
| FS-NIR-05 | URS-NIR-05 | NIR model deployment workflow requires PAT Scientist + Coating Process Engineer + QA signatures + model-validation-doc-ID; new deployment idle-tested on a recorded test run before production use. |

### 4.6 Pan Cleaning / CIP (M-CIP)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CIP-01 | URS-CIP-01 | CIP cycle templates: pre-rinse / caustic / rinse / acid / final-rinse; phase recording analogous to product cycles. |
| FS-CIP-02 | URS-CIP-02 | CIP acceptance: rinse-water conductivity threshold, optional TOC where instrumented; fail blocks subsequent product cycles via `coater.state = CIP_FAIL`. |
| FS-CIP-03 | URS-CIP-03 | Campaign-end CIP workflow: required after recipe-family change; requires Coating Process Engineer + Quality Reviewer signatures before product campaign re-opens. |

### 4.7 Solvent-Recovery Interlock (M-SOLV — organic variant)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SOLV-01 | URS-SOLV-01 | LEL channel consumed via dedicated DI; LEL ≥ 25% drives emergency-stop relay (hard-wired) isolating spray + ramping drying-air; software event logged + alarm raised. |
| FS-SOLV-02 | URS-SOLV-02 | Condenser-exhaust-T + condensate-mass-flow channels logged ≥ 1 Hz; out-of-envelope raises alarm. |
| FS-SOLV-03 | URS-SOLV-03 | Solvent genealogy fields (fresh_lot, recovered_batch_ref) captured at campaign start; rendered in cycle report. |

### 4.8 Batch Genealogy (M-GEN)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-GEN-01 | URS-GEN-01 | Cycle record bound to PAS-X batch_id + step_id; PAS-X EBR downstream-step gate state checked via callback (FS-INT-PASX-03). |
| FS-GEN-02 | URS-GEN-02 | Input-genealogy fields (suspension_lot, sub_coat_lot[], tablet_core_lot) captured at recipe-load + verified vs MBR; mismatch blocks cycle. |
| FS-GEN-03 | URS-GEN-03 | Weight-gain calculation: (post − pre) / pre; target + actual + ± tolerance rendered in cycle report cover sheet; verified `OQ-WEIGHT-GAIN-CALC-01`. |

### 4.9 Audit Trail (M-AUD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit trail captures recipe events, cycle events, alarm acks, signatures; PTP-derived timestamps. |
| FS-AUD-02 | URS-AUD-02 | DB-level append-only; revoked DELETE / UPDATE; DBA dual control. |
| FS-AUD-03 | URS-AUD-03 | Per-batch Quality Reviewer audit-trail UI; quarterly QA-Compliance platform review. |
| FS-AUD-04 | URS-AUD-04 | Retention ≥ 25 y; immutable cold storage. |

### 4.10 Part 11 / Annex 11 (M-PART11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Signature events render printed name + date / time + meaning into audit trail + PDFs. |
| FS-PART11-02 | URS-PART11-02 | User-id uniqueness enforced via AD; reused-id blocked. |
| FS-PART11-03 | URS-PART11-03 | PKI-signed signature payload (record-id, hash, signer-id, meaning, ts); tamper detection on read. |
| FS-PART11-04 | URS-PART11-04 | SoD enforced at signing API; conflicts rejected. |
| FS-PART11-05 | URS-PART11-05 | Re-auth + MFA at every signature; cached creds disabled. |
| FS-PART11-06 | URS-PART11-06 | AD password policy per `SEC-AD-POLICY-001`. |
| FS-PART11-07 | URS-PART11-07 | Audit-trail coverage per § 11.10(e); accurate-copy export per § 11.10(b); retention per § 11.10(c). |

### 4.11 Integrations (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-PASX-01 | URS-INT-PASX-01 | Recipe download via REST mTLS; SHA-256 + version + cert-chain validation. |
| FS-INT-PASX-02 | URS-INT-PASX-02 | Cycle report (parameters + alarms + weight-gain + NIR-summary + signatures) posted to PAS-X within 30 min; retry with exponential backoff. |
| FS-INT-PASX-03 | URS-INT-PASX-03 | PAS-X downstream-step gate cleared only after Quality Reviewer approval signature received via REST callback. |
| FS-INT-BMS-01 | URS-INT-BMS-01 | BMS room-pressure interlock consumed via OPC UA; loss aborts loading. |
| FS-INT-PAT-01 | URS-INT-PAT-01 | NIR OPC UA mTLS connection; cert auto-rotation runbook. |
| FS-INT-AD-01 | URS-INT-AD-01 | AD authentication; service accounts via HashiCorp Vault short-lived secrets. |

### 4.12 Data Integrity (M-DI)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | All record writes attributed to AD user-id; no shared accounts. |
| FS-DI-02 | URS-DI-02 | Cycle-report export as structured PDF + CSV; both validated `OQ-EXPORT-01`. |
| FS-DI-03 | URS-DI-03 | PTP sync; LDT clock-skew check at signature; > 5 s rejects. |
| FS-DI-04 | URS-DI-04 | Originals immutable; derivations stored separately. |
| FS-DI-05 | URS-DI-05 | Spray-mass + weight-gain calculation engine deterministic; `OQ-CALC-01`. |
| FS-DI-06 | URS-DI-06 | 25 y retention; ≤ 4 h retrieval via inspection-readiness runbook. |

### 4.13 Backup / Performance / Security (M-PERF / M-SEC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BAK-01 | URS-BAK-01 | InfluxDB nightly snapshot + continuous WAL → S3 object-lock; PITR 30 d. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore test by DBA + QA witness; `RUN-BAK-RESTORE-NNN`. |
| FS-BAK-03 | URS-BAK-03 | RTO ≤ 4 h documented runbook; RPO ≤ 1 min via streaming replication. |
| FS-PERF-01 | URS-PERF-01 | Sustained ≥ 1 Hz logging across all critical channels for full cycle (2-6 h); `PQ-PERF-DATA-LOG-01`. |
| FS-PERF-02 | URS-PERF-02 | HMI alarm-ack latency ≤ 1 s. |
| FS-SEC-01 | URS-SEC-01 | AD-managed accounts; break-glass admin only with dual control. |
| FS-SEC-02 | URS-SEC-02 | Removable-media GPO-blocked; CR exception path. |
| FS-SEC-03 | URS-SEC-03 | Tenable Nessus monthly; criticals 30 d. |

### 4.14 Training / Periodic Review (M-TRN / M-PR)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Production access gated by AD-group ↔ LMS completion attribute. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher reminder + PAT-Scientist competency-assessment workflow. |
| FS-PR-01 | URS-PR-01 | Annual periodic-review runbook auto-collects recipe inventory + change history, alarm trends, audit-trail review evidence, deviation summary, NIR-model register, CIP outcomes, training currency. |


### 4.15 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem with local OT cached credentials for offline operation. Conditional-access binding to policy `OT-Equipment Conditional Access (MFA at HMI session start; local cache validates last 24 h)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the recipe / cycle DB plus file-level capture of electronic batch records; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Interface Specifications

| IF ID | URS ID | Counterparty | Protocol | Direction | Notes |
|---|---|---|---|---|---|
| IF-PLC-01 | URS-CYC-* | ControlLogix 5580 | EtherNet/IP | bidirectional | tag values + alarms |
| IF-PASX-01 | URS-INT-PASX-01 | PAS-X v3.2 | REST mTLS | inbound | recipe download |
| IF-PASX-02 | URS-INT-PASX-02 | PAS-X v3.2 | REST mTLS | outbound | cycle-report push |
| IF-PASX-03 | URS-INT-PASX-03 | PAS-X v3.2 | REST callback | outbound | downstream-gate clear |
| IF-BMS-01 | URS-INT-BMS-01 | Site BMS | OPC UA | inbound | room-pressure interlock |
| IF-NIR-01 | URS-INT-PAT-01 | Bruker MATRIX-F | OPC UA mTLS | inbound | thickness predictions |
| IF-AD-01 | URS-INT-AD-01 | AD / PKI | LDAPS + Kerberos | bidirectional | AuthN + sig certs |
| IF-EQMS-01 | URS-CYC-05 | MasterControl eQMS | REST | outbound | auto-deviation on override |
| IF-LEL-01 | URS-SOLV-01 | Site LEL system | Hard-wired DI + Modbus | inbound | organic-variant only |

## 6. Data Model (high-level)

| Entity | Attributes (illustrative) |
|---|---|
| Recipe | recipe_id, version, state, params{drum_rpm, inlet_T, spray_rate, …}, scale_up_doe_ref, sha256, signatures[] |
| Cycle | cycle_id, recipe_id, recipe_version, batch_id, step_id, started_at, ended_at, state, weight_gain_pct |
| ChannelLog | cycle_id, channel, ts, value, source_tag, quality_flag |
| NIRDecision | cycle_id, ts, model_id, model_version, spectrum_hash, predicted_thickness, decision_threshold, decision |
| CIPRun | cip_id, coater_id, started_at, ended_at, phase[], conductivity_final, toc_final, accept |
| GenealogyLink | cycle_id, suspension_lot, sub_coat_lot[], tablet_core_lot, solvent_fresh_lot?, solvent_recovered_ref? |
| Alarm | alarm_id, cycle_id, severity, type, raised_at, ack_by, ack_at, reason |
| Override | override_id, cycle_id, parameter, old, new, op_id, eng_id, reason, ts |
| Signature | sig_id, record_id, signer_id, meaning, ts, payload_hash |
| AuditEvent | event_id, user_id, action, entity, old, new, ts |

## 7. Non-Functional Specifications

| NFR ID | Specification |
|---|---|
| NFR-01 | LDT failover ≤ 30 s automatic |
| NFR-02 | Sustained ≥ 1 Hz logging on all critical channels for full cycle (2-6 h) |
| NFR-03 | HMI alarm-ack latency ≤ 1 s |
| NFR-04 | Audit trail append-only; tampering detectable by PKI signature verification |
| NFR-05 | Retention ≥ 25 y from product expiry |
| NFR-06 | RPO ≤ 1 min, RTO ≤ 4 h |
| NFR-07 | NIR-signal-loss watchdog ≤ 3 missed samples |

## 8. Configuration Items (CI)

| CI ID | Item | Configured Value | Source |
|---|---|---|---|
| CI-01 | LDT failover target | ≤ 30 s | URS-PLAT-01 |
| CI-02 | UPS hold (LDT) | ≥ 30 min | URS-PLAT-02 |
| CI-03 | Recipe states | DRAFT,REVIEW,APPROVED,EFFECTIVE,OBSOLETE | URS-REC-01 |
| CI-04 | Tag logging rate | ≥ 1 Hz | URS-CYC-03 |
| CI-05 | Manual-override dual-sig | required | URS-CYC-05 |
| CI-06 | NIR cadence | recipe-defined (typ 1-10 Hz) | URS-NIR-01 |
| CI-07 | NIR signal-loss watchdog | 3 missed samples | URS-NIR-03 |
| CI-08 | LEL trip threshold | ≥ 25% | URS-SOLV-01 (organic) |
| CI-09 | Audit retention | ≥ 25 y from expiry | URS-AUD-04 |
| CI-10 | Backup window | nightly + WAL | URS-BAK-01 |
| CI-11 | Restore-test cadence | quarterly | URS-BAK-02 |
| CI-12 | Vuln-scan cadence | monthly | URS-SEC-03 |
| CI-13 | ISA-88 state model | per Part 1 / Part 2 | URS-S88-01 |
| CI-14 | CIP phase template | pre-rinse/caustic/rinse/acid/final | URS-CIP-01 |

## 9. Constraints / Assumptions / Risks

- **Constraints (FS-level):** Glatt GlattView core code vendor-controlled; site customisation limited to declarative recipe content + tasklet hooks; NIR chemometric model lifecycle governed externally.
- **Assumptions:** PAS-X validated under `MES-CSV-2024-007`; BMS under `BMS-CSV-2024-002`; AD + PKI + PTP-master infrastructure validated; NIR instrument qualified `EQ-NIR-COATER-001`.
- **FS-level risks:** spray-rate calibration drift undetected (FS-CYC-08 + spray-mass cross-check); NIR model staleness (FS-NIR-05 model-deployment workflow); LEL sensor blind-spot in organic variant (FS-SOLV-01 redundant sensors); recipe-version drift (FS-INT-PASX-01); audit-trail tampering (FS-AUD-02 + PKI signatures); CIP-skip bypass (FS-CIP-02 state-gate enforced).

## 10. References

- CST-URS-COATER-001 v1.2 (parent URS).
- 21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11.
- ICH Q9(R1); ICH Q14; ICH Q8(R2); USP <1151>; USP <711>.
- ANSI/ISA-88 Part 1 + Part 2; ANSI/ISA-95 Part 1.
- ISPE GAMP 5 (2nd ed., 2022); PIC/S PI 041.
- Glatt — *GC Smart 1500 + GlattView 5 Configuration Reference*; Bruker — *MATRIX-F NIR Operation Manual*.

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID(s) | Notes |
|---|---|---|
| URS-PLAT-01 | FS-PLAT-01 | |
| URS-PLAT-02 | FS-PLAT-02 | |
| URS-PLAT-03 | FS-PLAT-03 | |
| URS-PLAT-04 | FS-PLAT-04 | |
| URS-REC-01 | FS-REC-01 | |
| URS-REC-02 | FS-REC-02 | |
| URS-REC-03 | FS-REC-03 | |
| URS-REC-04 | FS-REC-04 | |
| URS-REC-05 | FS-REC-05 | |
| URS-REC-06 | FS-REC-06 | |
| URS-REC-07 | FS-REC-07 | |
| URS-REC-08 | FS-REC-08 | |
| URS-S88-01 | FS-S88-01 | |
| URS-S88-02 | FS-S88-02 | |
| URS-S88-03 | FS-S88-03 | |
| URS-CYC-01 | FS-CYC-01 | |
| URS-CYC-02 | FS-CYC-02 | |
| URS-CYC-03 | FS-CYC-03 | |
| URS-CYC-04 | FS-CYC-04 | |
| URS-CYC-05 | FS-CYC-05 | |
| URS-CYC-06 | FS-CYC-06 | |
| URS-CYC-07 | FS-CYC-07 | |
| URS-CYC-08 | FS-CYC-08 | |
| URS-NIR-01 | FS-NIR-01 / IF-NIR-01 | |
| URS-NIR-02 | FS-NIR-02 | |
| URS-NIR-03 | FS-NIR-03 | |
| URS-NIR-04 | FS-NIR-04 | |
| URS-NIR-05 | FS-NIR-05 | |
| URS-CIP-01 | FS-CIP-01 | |
| URS-CIP-02 | FS-CIP-02 | |
| URS-CIP-03 | FS-CIP-03 | |
| URS-SOLV-01 | FS-SOLV-01 / IF-LEL-01 | organic variant |
| URS-SOLV-02 | FS-SOLV-02 | organic variant |
| URS-SOLV-03 | FS-SOLV-03 | organic variant |
| URS-GEN-01 | FS-GEN-01 | |
| URS-GEN-02 | FS-GEN-02 | |
| URS-GEN-03 | FS-GEN-03 | |
| URS-AUD-01 | FS-AUD-01 | |
| URS-AUD-02 | FS-AUD-02 | |
| URS-AUD-03 | FS-AUD-03 | |
| URS-AUD-04 | FS-AUD-04 | |
| URS-PART11-01 | FS-PART11-01 | |
| URS-PART11-02 | FS-PART11-02 | |
| URS-PART11-03 | FS-PART11-03 | |
| URS-PART11-04 | FS-PART11-04 | |
| URS-PART11-05 | FS-PART11-05 | |
| URS-PART11-06 | FS-PART11-06 | |
| URS-PART11-07 | FS-PART11-07 | |
| URS-DI-01 | FS-DI-01 | |
| URS-DI-02 | FS-DI-02 | |
| URS-DI-03 | FS-DI-03 | |
| URS-DI-04 | FS-DI-04 | |
| URS-DI-05 | FS-DI-05 | |
| URS-DI-06 | FS-DI-06 | |
| URS-INT-PASX-01 | FS-INT-PASX-01 / IF-PASX-01 | |
| URS-INT-PASX-02 | FS-INT-PASX-02 / IF-PASX-02 | |
| URS-INT-PASX-03 | FS-INT-PASX-03 / IF-PASX-03 | |
| URS-INT-BMS-01 | FS-INT-BMS-01 / IF-BMS-01 | |
| URS-INT-PAT-01 | FS-INT-PAT-01 / IF-NIR-01 | |
| URS-INT-AD-01 | FS-INT-AD-01 / IF-AD-01 | |
| URS-PERF-01 | FS-PERF-01 | |
| URS-PERF-02 | FS-PERF-02 | |
| URS-BAK-01 | FS-BAK-01 | |
| URS-BAK-02 | FS-BAK-02 | |
| URS-BAK-03 | FS-BAK-03 | |
| URS-SEC-01 | FS-SEC-01 | |
| URS-SEC-02 | FS-SEC-02 | |
| URS-SEC-03 | FS-SEC-03 | |
| URS-TRN-01 | FS-TRN-01 | |
| URS-TRN-02 | FS-TRN-02 | |
| URS-PR-01 | FS-PR-01 | |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

The following risks are noted for downstream evaluation in the Risk Assessment.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Undetected sensor failure causing miscontrolled product temperature | Medium | High | URS-CYC-02..03 + redundant probes |
| R-02 | Recipe-version drift on download | Medium | High | URS-INT-PASX-01 + URS-REC-05 |
| R-03 | Unauthorised manual override | Medium | High | URS-CYC-05 dual signature + auto-deviation |
| R-04 | Audit-trail tampering | Low | Critical | URS-AUD-02 + DBA dual control |
| R-05 | Coating-uniformity drift (CV > acceptance) due to spray-rate sensor drift | Medium | High | URS-CYC-03 + sensor-calibration program |
| R-06 | NIR-model drift causing premature spray-end | Medium | High | URS-NIR-04 deterministic decision + model-life monitoring |
| R-07 | NIR signal loss during product cycle | Medium | Medium | URS-NIR-03 time-based fallback + engineering disposition |
| R-08 | Solvent LEL excursion (organic variant) without trip | Low | Critical | URS-SOLV-01 LEL interlock + redundant sensors |
| R-09 | CIP cycle bypass leading to cross-contamination | Low | Critical | URS-CIP-01..03 + campaign-end gate |
| R-10 | Batch-genealogy break between coater + EBR | Low | High | URS-GEN-01 cycle-EBR binding |
| R-11 | Spray-gun blockage undetected mid-cycle | Medium | Medium | URS-CYC-02 atomising-pressure-loss alarm |

Full evaluation in `CST-RA-COATER-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
