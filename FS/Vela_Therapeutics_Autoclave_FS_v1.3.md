---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; v1.2 enrichment 2026-05-13"
seed_corpus_basis:
  - "VEL-URS-AUTOCLAVE-001 (parent URS)"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11; EU GMP Annex 11; EU GMP Annex 1 (2022 revised); ISO 17665-1:2024; EN 285:2015+A1:2021"
parent_urs:
  document_number: VEL-URS-AUTOCLAVE-001
  version: 1.2
  file: ../../URS/_generated/final/Autoclave_Computer_System__Vela_Therapeutics_URS_v1.3.md
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

## Autoclave Computer System — Fedegari FOB 3 + Themis controller

**Document Number:** VEL-FS-AUTOCLAVE-001
**Version:** 1.2
**Effective Date:** 2026-05-13 *(synthetic)*
**Parent URS:** VEL-URS-AUTOCLAVE-001 v1.2
**Site:** Vela Therapeutics SRL, Sterile Manufacturing Plant 1, Parma, Italy *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Annex 1 (2022 revised); ISO 17665-1:2024; EN 285:2015+A1:2021; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Sterilization Engineer) | _____________ | _____________ | _____ |
| Reviewer (Microbiology) | _____________ | _____________ | _____ |
| Approver (Head of Sterile Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue, derived from VEL-URS-AUTOCLAVE-001 v1.0. |
| 1.2 | 2026-05-13 | (synthetic) | Expanded to per-URS-ID specifications (no range compression) per METHODOLOGY § 2A.7. Added cycle-type, F0 worst-case load, BD/leak/steam-quality, BI/CI cycle, Annex 1 (2022 revised) sub-sections. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies, at the system-design level, how Fedegari FOB 3 + Themis are configured and integrated to satisfy `VEL-URS-AUTOCLAVE-001` v1.2. Each functional specification entry maps to one or more URS requirements via the traceability matrix in Appendix A.

## 2. Scope

Per VEL-URS-AUTOCLAVE-001 § 2. In scope: FOB 3 cabinet + Themis controller + redundant LDT pair + Themis Historian + integrations with PAS-X, BMS, AD, PTP. Out of scope per parent URS.

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source / Vendor | Notes |
|---|---|---|---|---|---|
| C-01 | FOB 3 cabinet | Equipment | (equipment) | Fedegari | mechanical / vacuum / steam |
| C-02 | Themis controller (redundant CPU pair) | Embedded controller | 4 (safety partition supplier-validated per IEC 61511) | Fedegari | hot-standby |
| C-03 | TP1500 HMI panel | Embedded HMI | 4 | Siemens | cabinet-mounted |
| C-04 | Themis-Manager (active LDT) | COTS app | 4 | Fedegari | Windows Server 2022 |
| C-05 | Themis-Manager (standby LDT) | COTS app | 4 | Fedegari | manual failover |
| C-06 | Themis Historian | COTS app | 4 | Fedegari | TimescaleDB backend |
| C-07 | Grafana | COTS viz | (read-only) | Grafana Labs | trend display |
| C-08 | PAS-X v3.2 | COTS MES | 4 (separate URS/FS) | Werum / Körber | recipe + cycle report |
| C-09 | Site BMS | COTS BMS | 4 | (site) | room-pressure interlock |
| C-10 | AD / PKI | COTS infra | (infra) | Microsoft | AuthN + sig certs |
| C-11 | PTP master | COTS infra | (infra) | (site) | IEEE 1588 |

### 3.2 Logical Architecture

```
                ┌────────────────────────────────────────────┐
                │  Active Directory + Site PKI + PTP master   │
                └──────────────┬─────────────────────────────┘
                               │
                               ▼
   ┌────────────────────────────────────────────────────────────────┐
   │      Themis-Manager Active LDT  ←──→  Standby LDT (manual)     │
   │      (Win Server 2022; failover ≤ 1 h)                          │
   │      Recipe UI │ Cycle UI │ BI/CI capture │ Audit-trail viewer  │
   │      Historian (TimescaleDB) + Grafana                          │
   └────────┬──────────────────┬──────────────────────────────────────┘
            │ OPC UA mTLS      │ REST mTLS
            ▼                  ▼
   ┌────────────────────┐  ┌──────────────────────────────────┐
   │ Themis Controller  │  │ PAS-X v3.2 MES                   │
   │  (redundant CPU)   │  └──────────────────────────────────┘
   │  S7-1500F PLC      │
   │  TP1500 HMI        │  ┌──────────────────────────────────┐
   │  Safety partition  │  │ Site BMS (room-press interlock)  │
   └────────────────────┘  └──────────────────────────────────┘
```

### 3.3 Functional Modules

| Module | URS sections |
|---|---|
| M-PLAT | URS-PLAT-* |
| M-REC | URS-REC-* |
| M-CYCTYPE | URS-CYCTYPE-* |
| M-CYC | URS-CYC-* |
| M-F0 | URS-F0-* |
| M-BDLEAKSQ | URS-BD-*, URS-LEAK-*, URS-SQ-* |
| M-BI | URS-BI-*, URS-CI-* |
| M-AUD | URS-AUD-* |
| M-PART11 | URS-PART11-*, URS-AN1-* |
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
| FS-PLAT-01 | URS-PLAT-01 | Active / standby LDT pair on Windows Server 2022; database replicated via PostgreSQL streaming replication; failover documented runbook, target ≤ 1 h; verified by `OQ-FAILOVER-01`. |
| FS-PLAT-02 | URS-PLAT-02 | LDTs on UPS sized ≥ 30 min controlled hold; Themis controller + TP1500 on separate UPS branch; verified by `OQ-UPS-HOLD-01`. |
| FS-PLAT-03 | URS-PLAT-03 | Process-control VLAN (VLAN 412); no L3 route to office network; firewalled at the OT-DMZ; verified by `OQ-NET-AUDIT-01`. |
| FS-PLAT-04 | URS-PLAT-04 | Themis controller in 1oo2-redundant CPU configuration; sync over PROFINET-IRT; switch-over time ≤ 100 ms transparent to the running cycle's data plane; switch-over event written to audit trail; verified by `OQ-CPU-REDUNDANCY-01`. |
| FS-PLAT-05 | URS-PLAT-05 | Historian retains ≥ 7 y online in TimescaleDB; archival to S3-compatible immutable object store (S3 Object Lock, governance mode) thereafter. |

### 4.2 Recipe / Load Pattern Lifecycle (M-REC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REC-01 | URS-REC-01 | Recipe state machine {DRAFT, REVIEW, APPROVED, EFFECTIVE, OBSOLETE} enforced server-side in the Themis Recipe Service; transitions validated; out-of-state attempts rejected with HTTP 409 + audit event. |
| FS-REC-02 | URS-REC-02 | Cycle-load endpoint joins recipe → load-family registry; rejects load if `load_family.qualification_state != QUALIFIED` or `expiry < now()`. |
| FS-REC-03 | URS-REC-03 | Each recipe state transition requires re-authenticated electronic signature; AD-group → role mapping enforced server-side. |
| FS-REC-04 | URS-REC-04 | EFFECTIVE recipes immutable in the DB (UNIQUE + CHECK constraints + service guard); change creates revision N+1 in DRAFT linked to the prior. |
| FS-REC-05 | URS-REC-05 | Recipe-parameter schema validates ISO 17665-1 cycle-design fields: type (enum: porous_vacwrap, gravity, liquid_slow_exhaust, sealed_vial), exposure_temp_C, exposure_time_s, F0_target_min, ramp_rate_envelope, pre_vac_pulses (n + depth + hold), drying_time_s; missing / out-of-range fields block approval. |
| FS-REC-06 | URS-REC-06 | Recipe-approval workflow requires explicit Sterilization Engineer e-signature line citing the qualified load-family reference + worst-case PQ doc-ID; verified by `OQ-REC-ENG-SIGNOFF-01`. |
| FS-REC-07 | URS-REC-07 | Recipe-diff renderer (server-side) compares JSON-serialised recipes between revisions; UI presents changed fields with old / new values + change-reason text from the change request. |

### 4.3 Cycle-Type Specific (M-CYCTYPE)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CYCTYPE-01 | URS-CYCTYPE-01 | Porous-load cycle template includes mandatory pre-vacuum pulse sequence (3-5 pulses, configurable depth) and air-removal verification step (Bowie-Dick gate per URS-BD-01). |
| FS-CYCTYPE-02 | URS-CYCTYPE-02 | Gravity-displacement cycle template includes steam-purge phase with chamber-temperature equalisation target prior to exposure. |
| FS-CYCTYPE-03 | URS-CYCTYPE-03 | Liquid-load cycle template includes controlled cool-down (recipe-defined ramp rate ≤ 1 °C/min typical) with back-pressure compensation via air-overpressure; aborts on cool-down rate exceeded. |
| FS-CYCTYPE-04 | URS-CYCTYPE-04 | Sealed-vial cycle template (where the cabinet supports super-heated water spray) implements counter-pressure ramp matched to exposure temperature; verified by `OQ-SEALED-VIAL-CP-01`. |
| FS-CYCTYPE-05 | URS-CYCTYPE-05 | Recipe-load handler enforces cycle-type-specific preflight: porous_vacwrap requires daily BD pass; liquid requires container-tolerance file referenced; sealed_vial requires container-burst test reference. |

### 4.4 Cycle Execution / F0 (M-CYC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CYC-01 | URS-CYC-01 | Cycle engine evaluates setpoint envelope per recipe step; deviations classified info / warning / critical per recipe-defined thresholds. |
| FS-CYC-02 | URS-CYC-02 | Critical alarms (failure to reach exposure temp, jacket-pressure excursion, vacuum-leak > acceptance, NCG > 3.5% v/v) require operator acknowledgement + reason; alarms persist until acknowledged; persistence verified by `OQ-ALARM-CRITICAL-01`. |
| FS-CYC-03 | URS-CYC-03 | Channels logged at ≥ 1 Hz: per-zone chamber temperature (3 RTD Pt100 4-wire), per-position load temperature (3 RTD Pt100 4-wire), jacket pressure, chamber pressure, vacuum-line pressure; F0 computed continuously per ISO 17665-1 Annex A formula `F0 = Σ 10^((T(t)-121.1)/z) × Δt` with z = 10 °C, ref-T = 121.1 °C; verified by `OQ-F0-CALC-01` against a reference Python calculator. |
| FS-CYC-04 | URS-CYC-04 | Cycle-release gate evaluates F0 at every load-probe location; gate fails if any single probe < target_F0 even if chamber-mean ≥ target; verified by `OQ-F0-PER-PROBE-01`. |
| FS-CYC-05 | URS-CYC-05 | Manual setpoint override during product cycle requires Operator + Sterilization Engineer dual signature with reason captured; auto-deviation raised in MasterControl eQMS; flagged in cycle report. |
| FS-CYC-06 | URS-CYC-06 | Cycle-abort sequence safes the system (isolate steam, controlled vent to atmospheric, drain) per ISA-88 abort transition; audit-trail integrity preserved. |
| FS-CYC-07 | URS-CYC-07 | Per-probe health monitor evaluates RTD continuity (open / short via 4-wire) + drift vs paired chamber reference; > ± 0.5 °C drift triggers critical alarm + probe-exclusion; cycles continuing with < minimum-required probes fail; verified by `OQ-PROBE-FAIL-DETECT-01`. |
| FS-CYC-08 | URS-CYC-08 | Phase transitions (preconditioning / exposure / equalisation / drying / cool-down) recorded with PTP-derived timestamps; phase-time anomalies (> ± 10% of recipe-defined nominal) flagged. |

### 4.5 F0 Worst-Case Load Qualification (M-F0)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-F0-01 | URS-F0-01 | Load-family registry includes `qualification_state` ∈ {DRAFT, QUALIFIED, EXPIRED, RETIRED} + `qualified_until` + linked PQ-doc-ID; cycle-load handler queries before run start. |
| FS-F0-02 | URS-F0-02 | PQ load-mapping data ingested via dedicated import path (signed CSV); stores per-probe min/max F0 + slowest-to-heat coordinates; viewable from the Cycle UI for engineer review. |
| FS-F0-03 | URS-F0-03 | Cycle record schema includes `load_family_id`, `qualification_pq_doc`, `bi_cycle_ref` fields populated at run start; cycle report renders these in the cover sheet. |

### 4.6 Bowie-Dick / Leak / Steam-Quality (M-BDLEAKSQ)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BD-01 | URS-BD-01 | Daily-BD-gate enforced at cycle-load time for `cycle_type == porous_vacwrap` cycles; gate state per autoclave per day; failure routes to investigation workflow blocking porous cycles; verified by `OQ-BD-DAILY-GATE-01`. |
| FS-LEAK-01 | URS-LEAK-01 | Vacuum-leak test recipe runs scheduled weekly + on-demand; acceptance per EN 285 leak rate ≤ 1.3 mbar/min; failure flips autoclave state to OUT_OF_SERVICE; verified by `OQ-LEAK-TEST-01`. |
| FS-SQ-01 | URS-SQ-01 | Steam-quality input channels: NCG sensor (Spirax-Sarco or equivalent), dryness probe, superheat thermocouple; recipe defines acceptance thresholds (NCG ≤ 3.5%, dryness ≥ 0.95 metal / 0.90 porous, superheat ≤ 25 °C); excursion at cycle start blocks the cycle from advancing past preconditioning. |
| FS-SQ-02 | URS-SQ-02 | Manual condensate-test entry path captures pH + conductivity + chemistry-form-ID + operator-signature; reviewed by Sterilization Engineer monthly. |

### 4.7 BI / CI Cycle Qualification (M-BI)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BI-01 | URS-BI-01 | BI-challenge cycle workflow: operator captures BI lot, expiry, D-value (s @ 121 °C), spore population per strip; cycle ID linked; verified by `PQ-BI-CHALLENGE-01`. |
| FS-BI-02 | URS-BI-02 | Post-cycle BI-result entry path requires Microbiology e-signature; cycle disposition gated on BI outcome; failed-BI cycles auto-create deviation + block load release. |
| FS-CI-01 | URS-CI-01 | Per-cycle CI workflow: Type 5 / Type 6 indicator placement coordinates + post-cycle pass/fail entry; fail entry triggers investigation. |
| FS-BI-03 | URS-BI-03 | BI-calendar service tracks last BI-cycle date per load family per autoclave; alerts at 60 days before expiry; load-family modifications auto-flip the calendar to require re-BI. |

### 4.8 Audit Trail (M-AUD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit trail captures recipe events, cycle events (phase, setpoint, override), alarm acknowledgements, signature events, BI/CI/PCD entries; PTP-derived timestamps; verified by `OQ-AUD-COVERAGE-01`. |
| FS-AUD-02 | URS-AUD-02 | DB-level append-only on the audit schema; revoked DELETE / UPDATE; DBA dual-control for maintenance; application API exposes read + insert only; verified by `OQ-AUD-APPENDONLY-01`. |
| FS-AUD-03 | URS-AUD-03 | Per-cycle Quality-Reviewer audit-trail review UI; quarterly QA-Compliance platform review report runner. |
| FS-AUD-04 | URS-AUD-04 | Retention enforced by archival policy ≥ 25 y from product expiry; archived to immutable cold storage (object-lock governance). |

### 4.9 21 CFR Part 11 / Annex 11 / Annex 1 (M-PART11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Signature events render printed name + date / time (PTP) + meaning into audit trail and into cycle-report PDFs; verified by `OQ-PART11-01`. |
| FS-PART11-02 | URS-PART11-02 | User-id uniqueness enforced via AD; deactivated user-ids never reassigned; AD-group expiry policy enforces non-reuse. |
| FS-PART11-03 | URS-PART11-03 | Signatures cryptographically bound via PKI-signed payload (record-id, record-state-hash, signer-id, meaning, timestamp); tamper detection on read; verified by `OQ-PART11-03`. |
| FS-PART11-04 | URS-PART11-04 | SoD policy engine evaluates signer's prior actions on the same record; conflicts rejected with HTTP 403 + audit event; verified by `OQ-PART11-04`. |
| FS-PART11-05 | URS-PART11-05 | Signing UI re-prompts for password + AD MFA at every signature; cached creds disabled at the SSO config; verified by `OQ-PART11-05`. |
| FS-PART11-06 | URS-PART11-06 | AD password policy: min 14 chars, 90-day expiry, lockout after 5 attempts, 24-h lockout duration per § 11.300; documented in `SEC-AD-POLICY-001`. |
| FS-PART11-07 | URS-PART11-07 | Audit-trail covers all GMP operations per § 11.10(e); cycle-report export per § 11.10(b); 25-y retention archive per § 11.10(c). |
| FS-AN1-01 | URS-AN1-01 | Cycle-load handler validates the cleanroom-pressure interlock from BMS; pressurisation loss blocks loading; CCS cross-reference maintained in `VEL-CCS-PLANT1-001` § 7.3. |
| FS-AN1-02 | URS-AN1-02 | Cycle-record schema captures load lot, equipment / components listed, per-probe F0 evidence, BI/CI results, operator + verifier signatures; rendered in cycle-report cover sheet. |

### 4.10 Integrations (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-PASX-01 | URS-INT-PASX-01 | Recipe download via REST over mTLS; payload includes version + SHA-256 + signing cert chain; LDT validates checksum + version against the local approved-recipe registry; mismatch blocks the cycle and raises alarm + audit event. |
| FS-INT-PASX-02 | URS-INT-PASX-02 | Executed-cycle report (F0 evidence per probe + alarms + BI/CI + signatures + steam-quality summary) posted to PAS-X within 30 minutes of cycle end; retry with exponential backoff; persistent failure raises deviation. |
| FS-INT-PASX-03 | URS-INT-PASX-03 | PAS-X-side EBR step "sterilizer cycle complete" gated on receipt of cycle report + Quality-Reviewer approval signature; downstream filling-line steps blocked until gate clears. |
| FS-INT-BMS-01 | URS-INT-BMS-01 | BMS room-pressure interlock signal consumed via OPC UA from the site BMS; pressurisation loss → load-handler returns HTTP 503 with reason, operator notified at HMI. |
| FS-INT-AD-01 | URS-INT-AD-01 | AD-managed accounts; service accounts use HashiCorp Vault credential store with short-lived secrets; no local Operator / QC accounts. |
| FS-INT-NTP-01 | URS-INT-NTP-01 | PLC + workstations sync to site PTP master (IEEE 1588); LDT clock-skew check at cycle start + end; > 1 s skew flags cycle quality + raises engineering alarm. |

### 4.11 Data Integrity (M-DI)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | All record writes attributed to AD-authenticated user-id; no shared accounts; verified by `OQ-DI-ATTRIB-01`. |
| FS-DI-02 | URS-DI-02 | Cycle-report export as structured PDF (with embedded audit-trail extract) and as CSV; both validated under `OQ-EXPORT-01`. |
| FS-DI-03 | URS-DI-03 | PTP synchronisation for PLC clock; LDT clock-skew check at every signature event (> 5 s skew rejects signature). |
| FS-DI-04 | URS-DI-04 | Original captured data immutable; recalculations stored in separate `derivations` table referencing originals; verified by `OQ-DI-IMMUTABLE-01`. |
| FS-DI-05 | URS-DI-05 | F0 calculation engine deterministic (fixed-point arithmetic); verified per `OQ-F0-CALC-01` against reference calculator + IEEE-754 round-mode pin. |
| FS-DI-06 | URS-DI-06 | Retention 25 y; verified backup; retrieval ≤ 4 business hours via the inspection-readiness runbook. |

### 4.12 Backup / Performance / Security (M-PERF / M-SEC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BAK-01 | URS-BAK-01 | TimescaleDB nightly backup + continuous WAL archival to S3 (immutable / object-lock 30-day); PITR validated by `OQ-BAK-PITR-01`. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore-test runbook executed by DBA + QA witness; results filed in `RUN-BAK-RESTORE-NNN`. |
| FS-BAK-03 | URS-BAK-03 | LDT failover RTO ≤ 4 h documented runbook; RPO ≤ 1 min via PostgreSQL streaming replication. |
| FS-PERF-01 | URS-PERF-01 | Sustained ≥ 1 Hz logging on all probes for full cycle (typ 60-120 min, sealed-vial up to 4 h); verified by `PQ-PERF-LOG-01`. |
| FS-PERF-02 | URS-PERF-02 | HMI alarm-acknowledgement round-trip ≤ 1 s under normal load; verified by `PQ-HMI-LATENCY-01`. |
| FS-SEC-01 | URS-SEC-01 | AD-managed accounts; break-glass admin only with dual control + post-use review; verified by `OQ-SEC-BREAKGLASS-01`. |
| FS-SEC-02 | URS-SEC-02 | Removable media blocked at the Windows GPO level; vendor-approved engineering use opens a temporary GPO exception under CR. |
| FS-SEC-03 | URS-SEC-03 | Tenable Nessus monthly scans; criticals remediation 30 d; cadence verified `OQ-SEC-SCAN-01`. |

### 4.13 Training / Periodic Review (M-TRN / M-PR)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Production access gated by AD-group membership tied to LMS course-completion; users without completion blocked at login. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher reminder 60 d prior to expiry; access revoked on expiry; competency assessment workflow for Sterilization Engineer + Microbiology. |
| FS-PR-01 | URS-PR-01 | Annual periodic-review runbook auto-collects configuration baselines, recipe inventory + change history, audit-trail review evidence, deviation summary, alarm trends, BI-cycle summary, steam-quality trends, backup-restore evidence, training currency. |


### 4.14 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem with local OT cached credentials for offline operation. Conditional-access binding to policy `OT-Equipment Conditional Access (MFA at HMI session start; local cache validates last 24 h)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the cycle history DB + file-level capture of recipe and electronic batch records; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Interface Specifications

| IF ID | URS ID | Counterparty | Protocol | Direction | Notes |
|---|---|---|---|---|---|
| IF-PLC-01 | URS-CYC-* / URS-CYC-08 | Themis controller | OPC UA mTLS | bidirectional | tag values + alarms + phase transitions |
| IF-PASX-01 | URS-INT-PASX-01 | PAS-X v3.2 | REST mTLS | inbound | recipe download |
| IF-PASX-02 | URS-INT-PASX-02 | PAS-X v3.2 | REST mTLS | outbound | cycle-report push |
| IF-PASX-03 | URS-INT-PASX-03 | PAS-X v3.2 | REST callback | outbound | downstream-gate clear event |
| IF-BMS-01 | URS-INT-BMS-01 | Site BMS | OPC UA | inbound | room-pressure interlock |
| IF-AD-01 | URS-INT-AD-01 / URS-SEC-01 | AD / PKI | LDAPS + Kerberos | bidirectional | AuthN + sig certs |
| IF-PTP-01 | URS-INT-NTP-01 / URS-CYC-04 / URS-CYC-08 | PTP master | IEEE 1588 | inbound | time sync |
| IF-EQMS-01 | URS-CYC-05 | MasterControl eQMS | REST | outbound | auto-deviation on override |

## 6. Data Model (high-level)

| Entity | Attributes (illustrative) |
|---|---|
| Recipe | recipe_id, version, state, cycle_type, params{exposure_T, F0_target, …}, sha256, signatures[] |
| LoadFamily | family_id, qualification_state, qualified_until, pq_doc_id, mapping_data |
| Cycle | cycle_id, recipe_id, recipe_version, load_family_id, batch_id, started_at, ended_at, state, bi_cycle_ref |
| ProbeLog | cycle_id, probe_id, ts, T_C, P_bar, quality_flag |
| F0Result | cycle_id, probe_id, F0_min, F0_at_release, pass_fail |
| Alarm | alarm_id, cycle_id, severity, raised_at, ack_by, ack_at, reason |
| Override | override_id, cycle_id, parameter, old, new, op_id, eng_id, reason, ts |
| BIEntry | bi_id, cycle_id, lot, expiry, d_value, population, result, micro_id |
| CIEntry | ci_id, cycle_id, type, position, result |
| Signature | sig_id, record_id, signer_id, meaning, ts, payload_hash |
| AuditEvent | event_id, user_id, action, entity, old, new, ts |

## 7. Non-Functional Specifications

| NFR ID | Specification |
|---|---|
| NFR-01 | LDT failover ≤ 1 h documented; Themis CPU switchover ≤ 100 ms transparent |
| NFR-02 | Sustained ≥ 1 Hz logging on all probes for full cycle (≤ 4 h sealed-vial) |
| NFR-03 | HMI alarm-ack latency ≤ 1 s |
| NFR-04 | Audit trail append-only; tampering detectable via PKI signature verification |
| NFR-05 | Retention ≥ 25 y from product expiry |
| NFR-06 | RPO ≤ 1 min, RTO ≤ 4 h |
| NFR-07 | Process-control VLAN; no office-network route |
| NFR-08 | F0 calculation deterministic; verified vs reference within 0.1 min |

## 8. Configuration Items (CI)

| CI ID | Item | Configured Value | Source |
|---|---|---|---|
| CI-01 | LDT failover target | ≤ 1 h | URS-PLAT-01 |
| CI-02 | Themis CPU redundancy | 1oo2 hot-standby | URS-PLAT-04 |
| CI-03 | UPS hold (LDT) | ≥ 30 min | URS-PLAT-02 |
| CI-04 | Historian retention online | ≥ 7 y | URS-PLAT-05 |
| CI-05 | Recipe states | DRAFT,REVIEW,APPROVED,EFFECTIVE,OBSOLETE | URS-REC-01 |
| CI-06 | Cycle types supported | porous_vacwrap, gravity, liquid_slow_exhaust, sealed_vial | URS-CYCTYPE-01..04 |
| CI-07 | F0 z-value | 10 °C | URS-CYC-03 |
| CI-08 | F0 reference temperature | 121.1 °C | URS-CYC-03 |
| CI-09 | Probe array | ≥ 3 chamber + ≥ 3 load Pt100 4-wire | URS-CYC-03 |
| CI-10 | Logging rate | ≥ 1 Hz | URS-CYC-03, URS-PERF-01 |
| CI-11 | Probe drift threshold | ± 0.5 °C | URS-CYC-07 |
| CI-12 | BD daily gate | required for porous_vacwrap | URS-BD-01 |
| CI-13 | Leak-test cadence | weekly + on-demand | URS-LEAK-01 |
| CI-14 | NCG threshold | ≤ 3.5% v/v | URS-SQ-01 |
| CI-15 | Dryness threshold | ≥ 0.95 metal / ≥ 0.90 porous | URS-SQ-01 |
| CI-16 | BI cadence | quarterly per family | URS-BI-03 |
| CI-17 | Audit retention | ≥ 25 y from expiry | URS-AUD-04 |
| CI-18 | Backup window | nightly + WAL | URS-BAK-01 |
| CI-19 | Restore-test cadence | quarterly | URS-BAK-02 |
| CI-20 | Vuln-scan cadence | monthly | URS-SEC-03 |

## 9. Constraints / Assumptions / Risks

- **Constraints (FS-level):** Fedegari Themis core code is vendor-controlled; site customisation is limited to declarative configuration + recipe content + tasklet hooks. Safety partition changes follow IEC 61511 safety SDLC.
- **Assumptions:** Werum / Körber PAS-X validated under `MES-CSV-2024-007`; BMS validated under `BMS-CSV-2024-002`; AD + PKI + PTP-master are validated infrastructure.
- **FS-level risks:** F0 firmware calculation defect (mitigated by OQ-F0-CALC-01 vs reference + vendor SDLC reliance); probe-failure undetected (mitigated by FS-CYC-07 + redundant probe count); BD-gate bypass (mitigated by FS-BD-01 enforced at load-handler level); steam-quality sensor drift (mitigated by FS-SQ-01 + sensor-calibration program); audit-trail tampering (mitigated by FS-AUD-02 + DB controls + PKI signatures).

## 10. References

- VEL-URS-AUTOCLAVE-001 v1.2 (parent URS).
- 21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; EU GMP Annex 1 (2022 revised).
- ISO 17665-1:2024; ISO 17665-2:2009; EN 285:2015+A1:2021; ISO 11140-1:2014; ISO 11138-1:2017.
- ICH Q9(R1); ISPE GAMP 5 (2nd ed., 2022); PIC/S PI 041; PDA TR1.
- USP <1211>; USP <55>.
- Fedegari — *FOB 3 / Themis Configuration Reference*; *Themis F0 Calculation Theory of Operation*.

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID(s) | Notes |
|---|---|---|
| URS-PLAT-01 | FS-PLAT-01 | |
| URS-PLAT-02 | FS-PLAT-02 | |
| URS-PLAT-03 | FS-PLAT-03 | |
| URS-PLAT-04 | FS-PLAT-04 | |
| URS-PLAT-05 | FS-PLAT-05 | |
| URS-REC-01 | FS-REC-01 | |
| URS-REC-02 | FS-REC-02 | |
| URS-REC-03 | FS-REC-03 | |
| URS-REC-04 | FS-REC-04 | |
| URS-REC-05 | FS-REC-05 | |
| URS-REC-06 | FS-REC-06 | |
| URS-REC-07 | FS-REC-07 | |
| URS-CYCTYPE-01 | FS-CYCTYPE-01 | |
| URS-CYCTYPE-02 | FS-CYCTYPE-02 | |
| URS-CYCTYPE-03 | FS-CYCTYPE-03 | |
| URS-CYCTYPE-04 | FS-CYCTYPE-04 | |
| URS-CYCTYPE-05 | FS-CYCTYPE-05 | |
| URS-CYC-01 | FS-CYC-01 | |
| URS-CYC-02 | FS-CYC-02 | |
| URS-CYC-03 | FS-CYC-03 | |
| URS-CYC-04 | FS-CYC-04 | |
| URS-CYC-05 | FS-CYC-05 | |
| URS-CYC-06 | FS-CYC-06 | |
| URS-CYC-07 | FS-CYC-07 | |
| URS-CYC-08 | FS-CYC-08 | |
| URS-F0-01 | FS-F0-01 | |
| URS-F0-02 | FS-F0-02 | |
| URS-F0-03 | FS-F0-03 | |
| URS-BD-01 | FS-BD-01 | |
| URS-LEAK-01 | FS-LEAK-01 | |
| URS-SQ-01 | FS-SQ-01 | |
| URS-SQ-02 | FS-SQ-02 | |
| URS-BI-01 | FS-BI-01 | |
| URS-BI-02 | FS-BI-02 | |
| URS-BI-03 | FS-BI-03 | |
| URS-CI-01 | FS-CI-01 | |
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
| URS-AN1-01 | FS-AN1-01 | |
| URS-AN1-02 | FS-AN1-02 | |
| URS-INT-PASX-01 | FS-INT-PASX-01 / IF-PASX-01 | |
| URS-INT-PASX-02 | FS-INT-PASX-02 / IF-PASX-02 | |
| URS-INT-PASX-03 | FS-INT-PASX-03 / IF-PASX-03 | |
| URS-INT-BMS-01 | FS-INT-BMS-01 / IF-BMS-01 | |
| URS-INT-AD-01 | FS-INT-AD-01 / IF-AD-01 | |
| URS-INT-NTP-01 | FS-INT-NTP-01 / IF-PTP-01 | |
| URS-DI-01 | FS-DI-01 | |
| URS-DI-02 | FS-DI-02 | |
| URS-DI-03 | FS-DI-03 | |
| URS-DI-04 | FS-DI-04 | |
| URS-DI-05 | FS-DI-05 | |
| URS-DI-06 | FS-DI-06 | |
| URS-BAK-01 | FS-BAK-01 | |
| URS-BAK-02 | FS-BAK-02 | |
| URS-BAK-03 | FS-BAK-03 | |
| URS-PERF-01 | FS-PERF-01 | |
| URS-PERF-02 | FS-PERF-02 | |
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
| R-01 | Probe failure causing under-reported F0 leading to non-sterile load release | Medium | Critical | URS-CYC-03, URS-CYC-07, URS-BI-01 |
| R-02 | Recipe-version drift on load (operator using superseded recipe) | Medium | High | URS-INT-PASX-01, URS-REC-04 |
| R-03 | Manual override without justification masking a cycle defect | Medium | High | URS-CYC-05 dual signature + auto-deviation |
| R-04 | Audit-trail tampering by privileged user | Low | Critical | URS-AUD-02 + DBA dual control |
| R-05 | Bowie-Dick test missed; air pocket leads to non-sterile porous load | Low | Critical | URS-BD-01 daily gating + URS-CYCTYPE-05 |
| R-06 | NCG / wet-steam excursion masking exposure-time fault | Medium | High | URS-SQ-01 steam-quality monitoring |
| R-07 | BI false-negative causing release of non-sterile load | Low | Critical | URS-BI-01..03 with quarterly cadence + load-family-change trigger |
| R-08 | F0 miscalculation defect in Themis firmware causing systematic under-sterilization | Low | Critical | URS-CYC-03 OQ verification vs reference calculator + vendor SDLC reliance |
| R-09 | Cleanroom-pressure loss during load contaminating sterile components pre-cycle | Medium | High | URS-INT-BMS-01 + URS-AN1-01 |
| R-10 | Loss of historian / cycle-data during run | Low | High | URS-PLAT-04 redundant CPU + URS-BAK-01 |
| R-11 | Worst-case load family unqualified due to instrumentation change | Medium | Critical | URS-F0-01..03 qualification linkage |
| R-12 | Sealed-vial cycle counter-pressure mis-profile causing breakage | Low | Medium | URS-CYCTYPE-04 recipe validation |

Full evaluation in `VEL-RA-AUTOCLAVE-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
