---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (v1.0 corpus genesis per METHODOLOGY § 2B)"
seed_corpus_basis:
  - "VEL-FS-AUTOCLAVE-001 v1.2 (parent FS)"
  - "VEL-URS-AUTOCLAVE-001 v1.2 (parent URS — transitive)"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Annex 15"
  - "EU GMP Annex 1 (2022 revised)"
  - "ISO 17665-1:2024; ISO 17665-2:2009; EN 285:2015+A1:2021"
  - "ICH Q9(R1); ISPE GAMP 5 (2nd ed., 2022); PIC/S PI 041; PDA TR1"
parent_fs:
  document_number: VEL-FS-AUTOCLAVE-001
  version: "1.2"
  file: "../../../FS_FDS/_generated/final/Vela_Therapeutics_Autoclave_FS_v1.3.md"
parent_urs:
  document_number: VEL-URS-AUTOCLAVE-001
  version: "1.2"
  file: "../../../URS/_generated/final/Autoclave_Computer_System__Vela_Therapeutics_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Autoclave Computer System — Fedegari FOB 3 + Themis controller

**Document Number:** VEL-DS-AUTOCLAVE-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** VEL-FS-AUTOCLAVE-001 v1.2
**Parent URS:** VEL-URS-AUTOCLAVE-001 v1.2 *(informational; URS-ID linkage is transitive through the FS)*
**Site:** Vela Therapeutics SRL, Sterile Manufacturing Plant 1, Parma, Italy *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Fedegari FOB 3 + Themis controller** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Annex 15; EU GMP Annex 1 (2022 revised); ISO 17665-1:2024; EN 285:2015+A1:2021; PIC/S PI 041; PDA TR1.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Sterilization Engineer / SME) | _____________ | _____________ | _____ |
| Reviewer (Automation / OT-Security Architect) | _____________ | _____________ | _____ |
| Approver (System Owner — Sterilization Engineer) | _____________ | _____________ | _____ |
| Approver (Process Owner — Head of Sterile Mfg) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial issue. Inherited Tier T2 from parent URS+FS pair. DS covers 80/80 FS-IDs; 0 FS-IDs flagged as vendor-internal — no site design surface. Generated as part of the DS v1.0 corpus ship per METHODOLOGY § 2B (DS as Configuration Specification for Cat 4 — Configured Product). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

DS-specific terms only — URS / FS definitions are inherited by reference.

| Term | Definition |
|---|---|
| CS | Configuration Specification (this document, per GAMP 5 2nd ed. for Cat 4) |
| CI | Configuration Item — one configurable parameter, value, default-vs-custom flag, and justification |
| LBSPP | Logic-Based Script Plug-in Point (Themis) — vendor's hook for site-controlled configuration callbacks |
| OPC UA Tag | A named data item exposed by the Themis controller over OPC UA `Sign+Encrypt` Basic256Sha256 |
| Recipe Tasklet | Themis configuration unit executed within a recipe step (no executable code; declarative) |
| Themis-Manager | Fedegari supervisory workstation application (Windows Server 2022) |
| Themis Historian | Fedegari historian (TimescaleDB backend); read-only at the application layer |

## 1. Purpose

This Configuration Specification (CS) is the technical-design layer between `VEL-FS-AUTOCLAVE-001` v1.2 and downstream configuration / IQ / OQ / PQ Protocols for the Fedegari FOB 3 + Themis production-scale steam sterilizer at Vela Therapeutics Plant 1. It declares, per configurable item, the chosen value, the default-vs-custom status, the FS-ID(s) the choice satisfies, and the planned verification test. Vendor source-code internals (Themis firmware, S7-1500F safety partition, Siemens TP1500 HMI rendering pipeline) are NOT redrawn here — those remain under Fedegari and Siemens SDLC.

## 2. Scope

### In scope

- Themis-Manager Active LDT and Standby LDT application configuration on Windows Server 2022 (host OS, IIS, .NET runtime stack treated as infrastructure baseline).
- Themis controller PROFINET-IRT 1oo2 redundant CPU configuration (declarative parameters only; safety-partition program changes governed by IEC 61511 safety SDLC and out of scope of this DS).
- TP1500 HMI screen + alarm-list configuration.
- Themis Recipe Service state machine, recipe-parameter schema, electronic-signature workflow, and audit-trail bindings.
- Themis Historian (TimescaleDB) retention, compression, and archival policy.
- Integration endpoints (PAS-X recipe + cycle-report REST mTLS, BMS OPC UA cleanroom-pressure interlock, AD LDAPS/Kerberos, PTP master IEEE 1588, MasterControl eQMS auto-deviation REST).
- Site-deployed components: cycle-report renderer customisations, recipe-diff renderer (vendor-supplied LBSPPs only; no site-developed code).

### Out of scope

- Mechanical / piping / steam-generation / vacuum-pump hardware (covered by `EQ-AUTOCLAVE-001`).
- SIL-rated safety partition program (managed under safety SDLC per IEC 61511).
- PAS-X, BMS, AD, PTP master configuration internals (each has its own URS/FS/DS).
- Steam-supply utility qualification (`UTIL-STEAM-001`).
- Load-family physical PQ (`VAL-LOAD-FAM-NNN`).

## 3. Architectural Overview

### 3.1 Logical view

The system is a single FOB 3 cabinet driven by a redundant Themis controller pair. Two Windows-Server-2022 Themis-Manager workstations (Active LDT and Standby LDT) form a manual-failover pair connected over the process-control VLAN. The Themis Historian (TimescaleDB) is the time-series sink for probe data, F0 calculations, alarm acknowledgements, and audit events. PAS-X v3.2 MES is the recipe source and executed-cycle-report sink. The site BMS provides the cleanroom-pressure interlock signal over OPC UA. AD / PKI / PTP master are external infrastructure dependencies.

### 3.2 Probe layout (text diagram)

```
                            FOB 3 cabinet (horizontal pre-vacuum)
                            ─────────────────────────────────────
                            ┌───────────────────────────────────┐
                            │ Chamber RTD Pt100 4-wire           │
                            │   T-CH-01 (front-top)              │
                            │   T-CH-02 (centre-middle)          │
                            │   T-CH-03 (rear-bottom — drain)    │
                            │                                    │
                            │ Load probes RTD Pt100 4-wire       │
                            │   T-LD-01 (load worst-case)        │
                            │   T-LD-02 (load mid)               │
                            │   T-LD-03 (load reference)         │
                            │                                    │
                            │ Pressure: P-CH (chamber),          │
                            │           P-JK (jacket), P-VAC     │
                            │                                    │
                            │ Steam-quality: NCG, Dryness,       │
                            │   Superheat (cabinet inlet)         │
                            └───────────────────────────────────┘

                            Themis controller (1oo2 redundant CPU)
                            ─────────────────────────────────────
                            ┌───────────────────────────────────┐
                            │ CPU-A (active)   ◄──── PROFINET-IRT │
                            │ CPU-B (standby)        sync          │
                            │ Siemens S7-1500F safety partition    │
                            │ TP1500 HMI panel (cabinet-mounted)   │
                            └────────────┬──────────────────────┘
                                         │ OPC UA mTLS
                  ┌──────────────────────▼───────────────────────┐
                  │ Active LDT (Themis-Manager, Win Srv 2022)    │
                  │ Standby LDT (manual failover ≤ 1 h)           │
                  │ TimescaleDB Historian                         │
                  └──────┬──────────────┬───────────────┬────────┘
                         │ REST mTLS    │ OPC UA        │ REST
                         ▼              ▼               ▼
                       PAS-X         Site BMS       MasterControl
                       (recipe +     (room press.   (auto-deviation
                        cycle rpt)    interlock)     on override)
```

### 3.3 Component inventory inherited from parent FS

Per FS § 3.1: C-01 FOB 3 cabinet; C-02 Themis redundant CPU pair; C-03 Siemens TP1500 HMI; C-04 Themis-Manager Active LDT; C-05 Themis-Manager Standby LDT; C-06 Themis Historian (TimescaleDB); C-07 Grafana; C-08 PAS-X v3.2; C-09 Site BMS; C-10 AD / PKI; C-11 PTP master. This DS configures C-02 through C-07; C-01 + C-11 + C-10 + C-08 + C-09 are referenced via the integration endpoints in § 7.

## 4. Configuration Specification

Each row declares one Configuration Item (CI), the chosen value, default-vs-custom flag, FS-ID(s) traced, justification, and planned verification.

### 4.1 Platform / Hardware

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUTOCLAVE-01 | Themis-Manager Active LDT — host OS | Windows Server 2022 (21H2 LTSC) | Custom | Fedegari-supported baseline; matches site standard OS for OT workstations. | FS-PLAT-01 | OQ-FAILOVER-01 |
| DS-AUTOCLAVE-02 | Themis-Manager Standby LDT — host OS | Windows Server 2022 (21H2 LTSC) — identical patch baseline as Active LDT | Custom | Identical baseline reduces failover-time risk and audit-trail divergence. | FS-PLAT-01 | OQ-FAILOVER-01 |
| DS-AUTOCLAVE-03 | LDT failover mode | Manual failover; documented runbook `VEL-RB-AUTOCLAVE-FAILOVER-001`; target ≤ 1 h | Custom | FS-PLAT-01 explicitly require manual failover within 1 h; automatic failover not chosen because operator must confirm cycle-data quality before continuing on standby. | FS-PLAT-01 | OQ-FAILOVER-01 |
| DS-AUTOCLAVE-04 | Themis Historian — DB replication mode | PostgreSQL streaming replication, synchronous-commit `remote_apply` on active, asynchronous to S3 archival | Custom | Synchronous to standby guarantees RPO ≤ 1 min per FS-BAK-03; asynchronous to S3 keeps archival decoupled. | FS-PLAT-01, FS-BAK-03 | OQ-BAK-PITR-01 |
| DS-AUTOCLAVE-05 | UPS sizing for Active + Standby LDT | APC Smart-UPS SRT 5kVA per LDT; 30 min hold at 80% load; controlled-shutdown integration via PowerChute Network Shutdown | Custom | (transitive via parent URS) minimum 30 min ride-through; sizing margin chosen for headroom under cycle-end load. | FS-PLAT-02 | OQ-UPS-HOLD-01 |
| DS-AUTOCLAVE-06 | UPS sizing for Themis controller + TP1500 HMI | APC Smart-UPS SRT 3kVA on separate branch | Custom | Separate UPS branch isolates control-loop power from LDT power; required by FS-PLAT-02. | FS-PLAT-02 | OQ-UPS-HOLD-01 |
| DS-AUTOCLAVE-07 | Process-control VLAN ID | VLAN 412 | Custom | Site OT VLAN range 410-419 reserved for sterile manufacturing; FS-PLAT-03 requires segregation from office network. | FS-PLAT-03 | OQ-NET-AUDIT-01 |
| DS-AUTOCLAVE-08 | Firewall policy — OT-DMZ to office network | Deny-by-default; no L3 route configured at the OT-DMZ Fortinet FortiGate | Custom | FS-PLAT-03 explicit. | FS-PLAT-03 | OQ-NET-AUDIT-01 |
| DS-AUTOCLAVE-09 | Themis controller redundancy mode | 1oo2 hot-standby; PROFINET-IRT sync; switch-over ≤ 100 ms transparent | Default (Fedegari recommended) | FS-PLAT-04 verbatim; matches Fedegari *Themis Redundancy Configuration Reference* v3.1 § 4.2. | FS-PLAT-04 | OQ-CPU-REDUNDANCY-01 |
| DS-AUTOCLAVE-10 | CPU switch-over audit-trail emission | `themis_audit.event_type = CPU_SWITCHOVER` written to historian on every CPU role change | Default | Required by FS-PLAT-04 for traceability; vendor LBSPP `OnCpuSwitchover` configured to emit event. | FS-PLAT-04 | OQ-CPU-REDUNDANCY-01 |
| DS-AUTOCLAVE-11 | Historian online retention | ≥ 7 years online in TimescaleDB hypertable `cycle_data` | Custom | FS-PLAT-05; site cold-storage tier chosen for older archive. | FS-PLAT-05 | OQ-ARCHIVAL-01 |
| DS-AUTOCLAVE-12 | Historian archive tier | AWS S3 Object Lock (Governance mode, 25 y) for archived cycle records | Custom | Cold archive must support inspection retrieval within 4 BH per parent URS; S3 Object Lock provides retention immutability per FS-PLAT-05 + FS-BAK-01. | FS-PLAT-05, FS-BAK-01 | OQ-ARCHIVAL-01 |

### 4.2 Recipe / Load Pattern Lifecycle

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUTOCLAVE-13 | Themis Recipe Service — state machine | `DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE` enforced server-side | Default (Fedegari recipe-service template) | Matches FS-REC-01 verbatim; out-of-state attempts return HTTP 409. | FS-REC-01 | OQ-REC-LIFECYCLE-01 |
| DS-AUTOCLAVE-14 | Out-of-state transition response | HTTP 409 Conflict + audit event `RECIPE_STATE_REJECTED` | Default | Fedegari recipe-service standard error response. | FS-REC-01 | OQ-REC-LIFECYCLE-01 |
| DS-AUTOCLAVE-15 | Load-family qualification gate | Themis cycle-load handler joins recipe → `load_family.qualification_state`; loads block when state ≠ `QUALIFIED` or `expiry < now()` | Custom | FS-REC-02 + FS-F0-01 enforce no-unqualified-load policy; cycle-load handler customised via LBSPP `OnRecipeLoad`. | FS-REC-02, FS-F0-01 | OQ-LOAD-FAMILY-GATE-01 |
| DS-AUTOCLAVE-16 | Recipe-state transition signature requirement | Re-authenticated electronic signature on each transition; AD-group → role mapping enforced server-side | Default | FS-REC-03; matches Fedegari *Themis Recipe Service Administrator Guide* v5.3 § 6.1. | FS-REC-03 | OQ-REC-LIFECYCLE-01 |
| DS-AUTOCLAVE-17 | EFFECTIVE-recipe immutability constraint | `UNIQUE (recipe_id, revision)` + `CHECK (state != 'EFFECTIVE' OR row_locked = true)` + Recipe Service guard | Default | FS-REC-04; standard immutability pattern. | FS-REC-04 | OQ-REC-IMMUTABLE-01 |
| DS-AUTOCLAVE-18 | Recipe-parameter schema — cycle-type enum | `{porous_vacwrap, gravity, liquid_slow_exhaust, sealed_vial}` | Custom | Matches FS-REC-05 + FS-CYCTYPE-01..04; one-to-one with ISO 17665-1 cycle-design parameters. | FS-REC-05, FS-CYCTYPE-01, FS-CYCTYPE-02, FS-CYCTYPE-03, FS-CYCTYPE-04 | OQ-RECIPE-SCHEMA-01 |
| DS-AUTOCLAVE-19 | Recipe-parameter — exposure-temperature setpoint allowed range | 100.0 °C ≤ setpoint ≤ 138.0 °C; common values 121.1 °C and 134.0 °C | Custom | Range envelops ISO 17665-1 + EN 285 standard temperatures; values outside blocked at approval. | FS-REC-05 | OQ-RECIPE-SCHEMA-01 |
| DS-AUTOCLAVE-20 | Recipe-parameter — F0 target minimum | F0_target_min ≥ 8 min (configurable per recipe; never below per ISO 17665-1) | Custom | F0 target is recipe-specific but never below 8 min for terminal sterilization per site CCS policy `VEL-CCS-PLANT1-001`. | FS-REC-05 | OQ-RECIPE-SCHEMA-01 |
| DS-AUTOCLAVE-21 | Recipe-parameter — pre-vacuum pulses (porous) | 3–5 pulses; depth -0.85 bar to -0.95 bar; hold 60–120 s per pulse | Default (Fedegari standard porous template) | FS-CYCTYPE-01 air-removal verification; pulse window from Fedegari porous-load reference. | FS-CYCTYPE-01 | OQ-CYCTYPE-POROUS-01 |
| DS-AUTOCLAVE-22 | Recipe-approval — Sterilization Engineer signature line | Required electronic signature with meaning text "Approves recipe and confirms validated load-family + worst-case PQ doc-ID linkage" | Custom | FS-REC-06; meaning text mandated by 21 CFR § 11.50 + site SOP. | FS-REC-06 | OQ-REC-ENG-SIGNOFF-01 |
| DS-AUTOCLAVE-23 | Recipe-diff renderer | Server-side JSON diff (changed fields highlighted old / new) + change-reason text from CR; rendered in Themis-Manager review UI | Custom | FS-REC-07 + § 11.10(b) accurate-and-complete-copy requirement. | FS-REC-07 | OQ-RECIPE-DIFF-01 |

### 4.3 Cycle-Type Specific

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUTOCLAVE-24 | Porous-load — air-removal verification gate | Daily-Bowie-Dick gate at cycle-load time per autoclave per day; failure routes to investigation workflow blocking porous cycles | Custom | FS-BD-01 + FS-CYCTYPE-05 mandatory. | FS-BD-01, FS-CYCTYPE-05 | OQ-BD-DAILY-GATE-01 |
| DS-AUTOCLAVE-25 | Gravity-displacement — steam-purge target | Equalisation at exposure_T - 1.0 °C across chamber probes before exposure phase begins | Default | FS-CYCTYPE-02 verbatim; matches Fedegari gravity-cycle template. | FS-CYCTYPE-02 | OQ-CYCTYPE-GRAVITY-01 |
| DS-AUTOCLAVE-26 | Liquid-load — cool-down ramp rate cap | ≤ 1.0 °C / min during cool-down phase; aborts on rate exceeded | Default (Fedegari liquid-template recommendation) | FS-CYCTYPE-03 to prevent container breakage. | FS-CYCTYPE-03 | OQ-CYCTYPE-LIQUID-01 |
| DS-AUTOCLAVE-27 | Liquid-load — back-pressure control | Air-overpressure ramp matched to exposure-temperature saturation pressure +0.3 bar | Default | FS-CYCTYPE-03; standard back-pressure for liquid loads. | FS-CYCTYPE-03 | OQ-CYCTYPE-LIQUID-01 |
| DS-AUTOCLAVE-28 | Sealed-vial — counter-pressure ramp | Counter-pressure profile matched to exposure_T saturation pressure +0.5 bar; container-burst-test reference required at recipe approval | Custom | FS-CYCTYPE-04 + FS-CYCTYPE-05 preflight check; cabinet supports super-heated water spray. | FS-CYCTYPE-04, FS-CYCTYPE-05 | OQ-SEALED-VIAL-CP-01 |

### 4.4 Cycle Execution / F0

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUTOCLAVE-29 | Setpoint envelope evaluation cadence | Every 1.0 s; deviation classified info / warning / critical per recipe-defined thresholds | Default | FS-CYC-01; matches probe-logging cadence (transitive via parent URS). | FS-CYC-01 | OQ-ALARM-CRITICAL-01 |
| DS-AUTOCLAVE-30 | Critical-alarm acknowledgement requirement | Operator acknowledgement with captured reason required; alarms not self-clearing | Default | FS-CYC-02; standard Annex 11 § 9 alarm-handling. | FS-CYC-02 | OQ-ALARM-CRITICAL-01 |
| DS-AUTOCLAVE-31 | NCG critical-alarm threshold | > 3.5% v/v cabinet inlet | Default | EN 285 § 13.3; matches FS-SQ-01. | FS-CYC-02, FS-SQ-01 | OQ-ALARM-CRITICAL-01 |
| DS-AUTOCLAVE-32 | Probe logging rate | 1.0 Hz per probe (3 chamber + 3 load Pt100 4-wire) | Default | FS-CYC-03 minimum; matches Themis Historian standard config. | FS-CYC-03, FS-PERF-01 | PQ-PERF-LOG-01 |
| DS-AUTOCLAVE-33 | F0 calculation parameters | z-value = 10.0 °C; reference-T = 121.1 °C; integration formula per ISO 17665-1 Annex A | Default (regulator-mandated) | ISO 17665-1 Annex A defines these constants; non-negotiable. | FS-CYC-03 | OQ-F0-CALC-01 |
| DS-AUTOCLAVE-34 | F0 calculation arithmetic | Fixed-point decimal (Python `decimal.Decimal`, 6 fractional digits) executed in Themis-Manager engine | Custom | FS-DI-05 + FS-CYC-03 deterministic-calculation requirement; IEEE-754 round-mode pinned. | FS-CYC-03, FS-DI-05 | OQ-F0-CALC-01 |
| DS-AUTOCLAVE-35 | F0 per-probe release gate | Cycle-release gate fails if any single load-probe F0 < recipe `F0_target_min`, even when chamber-mean ≥ target | Custom | FS-CYC-04 (worst-case-probe rule); critical sterility safeguard. | FS-CYC-04 | OQ-F0-PER-PROBE-01 |
| DS-AUTOCLAVE-36 | Manual-override during product cycle | Dual signature (Operator + Sterilization Engineer) with reason captured; auto-deviation raised in MasterControl eQMS | Custom | FS-CYC-05 + FS-PART11-04 SoD; high-risk action. | FS-CYC-05, FS-PART11-04 | OQ-OVERRIDE-DUAL-SIG-01 |
| DS-AUTOCLAVE-37 | Cycle-abort safing sequence | ISA-88 abort transition: isolate steam supply, controlled vent to atmospheric, drain — audit-trail integrity preserved | Default (Fedegari abort template) | FS-CYC-06; standard ISA-88 abort. | FS-CYC-06 | OQ-CYCLE-ABORT-01 |
| DS-AUTOCLAVE-38 | Probe-drift threshold | ± 0.5 °C vs paired chamber reference; trigger `PROBE_DRIFT` critical alarm + exclude probe from F0 | Default | FS-CYC-07; standard sterilizer probe-monitoring practice. | FS-CYC-07 | OQ-PROBE-FAIL-DETECT-01 |
| DS-AUTOCLAVE-39 | Minimum probes for cycle continuation | ≥ 2 chamber + ≥ 2 load probes operational; below minimum fails cycle | Custom | FS-CYC-07 worst-case-probe rule; matches site CCS policy. | FS-CYC-07 | OQ-PROBE-FAIL-DETECT-01 |
| DS-AUTOCLAVE-40 | Phase-transition timestamping | PTP IEEE 1588-derived timestamps on every phase transition (preconditioning / exposure / equalisation / drying / cool-down) | Default | FS-CYC-08 + FS-DI-03. | FS-CYC-08, FS-DI-03 | OQ-PHASE-TS-01 |
| DS-AUTOCLAVE-41 | Phase-time anomaly flag | > ± 10% of recipe-defined nominal phase duration flagged in cycle report | Custom | FS-CYC-08 anomaly-detection threshold per site cycle-engineering convention. | FS-CYC-08 | OQ-PHASE-TS-01 |

### 4.5 F0 Worst-Case Load Qualification

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUTOCLAVE-42 | Load-family registry — qualification state enum | `{DRAFT, QUALIFIED, EXPIRED, RETIRED}` + `qualified_until` + linked PQ-doc-ID | Default | FS-F0-01; matches Fedegari load-family schema. | FS-F0-01 | OQ-LOAD-FAMILY-GATE-01 |
| DS-AUTOCLAVE-43 | PQ load-mapping import path | Signed CSV ingestion endpoint `POST /loadfamily/pq-import`; per-probe min/max F0 + slowest-to-heat coordinates stored | Custom | FS-F0-02 import-and-store pattern; Ed25519-signed CSV prevents tampering. | FS-F0-02 | OQ-LOAD-FAMILY-IMPORT-01 |
| DS-AUTOCLAVE-44 | Cycle-record fields | `load_family_id`, `qualification_pq_doc`, `bi_cycle_ref` populated at run start; rendered on cycle-report cover sheet | Default | FS-F0-03; standard cycle-report header. | FS-F0-03 | OQ-CYCLE-REPORT-01 |

### 4.6 Bowie-Dick / Leak / Steam-Quality

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUTOCLAVE-45 | BD daily-gate enforcement scope | Per autoclave per calendar day; first porous cycle of the day blocked until BD pass recorded | Default | FS-BD-01 verbatim. | FS-BD-01 | OQ-BD-DAILY-GATE-01 |
| DS-AUTOCLAVE-46 | Vacuum-leak test cadence | Weekly + on-demand; acceptance ≤ 1.3 mbar/min per EN 285 § 21 | Default (regulator-mandated) | FS-LEAK-01 + EN 285; weekly cadence is site SOP. | FS-LEAK-01 | OQ-LEAK-TEST-01 |
| DS-AUTOCLAVE-47 | Leak-test failure disposition | Autoclave state → `OUT_OF_SERVICE`; cycle-load gate blocks all product cycles until cleared | Custom | FS-LEAK-01 + site CCS policy. | FS-LEAK-01 | OQ-LEAK-TEST-01 |
| DS-AUTOCLAVE-48 | Steam-quality sensor selection | Spirax-Sarco NCG sensor (model SQM-100) + Spirax-Sarco dryness probe + Type-K superheat thermocouple at cabinet inlet | Custom | FS-SQ-01 + EN 285 § 13; site standard supplier. | FS-SQ-01 | OQ-STEAM-QUALITY-01 |
| DS-AUTOCLAVE-49 | Steam-quality acceptance thresholds | NCG ≤ 3.5% v/v; dryness ≥ 0.95 (metal loads) / ≥ 0.90 (porous); superheat ≤ 25 °C | Default (regulator) | EN 285 § 13 verbatim. | FS-SQ-01 | OQ-STEAM-QUALITY-01 |
| DS-AUTOCLAVE-50 | Steam-quality excursion at cycle start | Blocks cycle from advancing past preconditioning phase | Default | FS-SQ-01; cycle cannot proceed with off-spec steam. | FS-SQ-01 | OQ-STEAM-QUALITY-01 |
| DS-AUTOCLAVE-51 | Manual condensate-test entry | Operator-signed pH + conductivity + chemistry-form-ID; reviewed monthly by Sterilization Engineer | Custom | FS-SQ-02; cabinet does not support automated condensate sampling, so manual path retained. | FS-SQ-02 | OQ-CONDENSATE-ENTRY-01 |

### 4.7 BI / CI Cycle Qualification

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUTOCLAVE-52 | BI-challenge workflow capture fields | BI lot, expiry, D-value (s @ 121 °C), spore population per strip, cycle-id link | Default | FS-BI-01; matches USP <55> requirements. | FS-BI-01 | PQ-BI-CHALLENGE-01 |
| DS-AUTOCLAVE-53 | BI-result entry signing | Microbiology e-signature required on BI-cycle disposition; failed-BI auto-deviation + load-release block | Custom | FS-BI-02 + FS-PART11-04 SoD. | FS-BI-02 | PQ-BI-CHALLENGE-01 |
| DS-AUTOCLAVE-54 | CI workflow | Type 5 / Type 6 indicator placement coordinates + post-cycle pass/fail entry; fail triggers investigation | Default | FS-CI-01 + ISO 11140-1; standard CI handling. | FS-CI-01 | OQ-CI-ENTRY-01 |
| DS-AUTOCLAVE-55 | BI calendar — alert threshold | 60 days before BI-cycle expiry per load family per autoclave | Default | FS-BI-03; site BI-program SOP. | FS-BI-03 | OQ-BI-CALENDAR-01 |

### 4.8 Audit Trail

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUTOCLAVE-56 | Audit-trail coverage | Recipe events, cycle events (phase, setpoint, override), alarm acknowledgements, signature events, BI/CI/PCD entries | Default | FS-AUD-01 + Annex 11 § 9. | FS-AUD-01 | OQ-AUD-COVERAGE-01 |
| DS-AUTOCLAVE-57 | Append-only enforcement | DB role grants: `themis_app` role has INSERT / SELECT only on `themis_audit`; UPDATE / DELETE revoked at role level; DBA dual-control for any maintenance | Custom | FS-AUD-02; DBA dual-control matches site OT-security policy. | FS-AUD-02 | OQ-AUD-APPENDONLY-01 |
| DS-AUTOCLAVE-58 | Audit-trail review surface | Per-cycle Quality-Reviewer UI + quarterly QA-Compliance platform-review report runner `themis_aud_quarterly.py` | Custom | FS-AUD-03; matches periodic-review pattern in URS § 5.13. | FS-AUD-03 | OQ-AUD-REVIEW-01 |
| DS-AUTOCLAVE-59 | Audit-trail retention | ≥ 25 y from product expiry; archived to S3 Object Lock Governance mode | Default (regulator-mandated) | FS-AUD-04; matches 21 CFR § 11.10(c). | FS-AUD-04 | OQ-ARCHIVAL-01 |

### 4.9 21 CFR Part 11 / Annex 11 / Annex 1

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUTOCLAVE-60 | Signature manifestation fields | Printed name + UTC ISO-8601 timestamp (PTP-derived) + meaning text into audit trail + cycle-report PDF cover sheet | Default | 21 CFR § 11.50 verbatim; FS-PART11-01. | FS-PART11-01 | OQ-PART11-01 |
| DS-AUTOCLAVE-61 | User-ID uniqueness mechanism | AD enforces; deactivated accounts never reassigned; AD-group expiry policy `ad-no-reassign-90d` | Default | FS-PART11-02 + 21 CFR § 11.100. | FS-PART11-02 | OQ-PART11-02 |
| DS-AUTOCLAVE-62 | Signature binding mechanism | Site PKI-signed payload `{record_id, record_state_hash, signer_id, meaning, timestamp_utc}` over Ed25519; tamper-detection on read | Custom | FS-PART11-03 + 21 CFR § 11.70; Ed25519 chosen over RSA-2048 for performance under cycle-end signature volume. | FS-PART11-03 | OQ-PART11-03 |
| DS-AUTOCLAVE-63 | SoD policy engine | Server-side policy: signer's prior actions on same record blocked from final approval; conflicts return HTTP 403 + audit event | Default | FS-PART11-04 + § 11.10(d)/(g). | FS-PART11-04 | OQ-PART11-04 |
| DS-AUTOCLAVE-64 | Re-authentication at signing | Password + AD MFA (Yubikey) at every signature event; cached SSO disabled at the IdP config | Custom | FS-PART11-05 + § 11.200; cached creds explicitly disabled for sterilizer signatures. | FS-PART11-05 | OQ-PART11-05 |
| DS-AUTOCLAVE-65 | AD password policy | Min 14 chars, 90 d expiry, lockout after 5 failed attempts, 24 h lockout duration | Default (site InfoSec) | FS-PART11-06 + § 11.300; matches site-wide `SEC-AD-POLICY-001`. | FS-PART11-06 | OQ-PART11-06 |
| DS-AUTOCLAVE-66 | Audit-trail coverage of GMP operations (§ 11.10(e)) | All recipe + cycle + signature + BI/CI events captured; cycle-report PDF export per § 11.10(b); 25 y retention per § 11.10(c) | Default | FS-PART11-07. | FS-PART11-07 | OQ-AUD-COVERAGE-01 |
| DS-AUTOCLAVE-67 | Annex 1 cleanroom-pressure interlock | Cycle-load handler queries BMS OPC UA tag `BMS.CLN.GA.PRESS_DIFF`; loss-of-pressurisation blocks loading; CCS cross-reference `VEL-CCS-PLANT1-001` § 7.3 | Custom | FS-AN1-01 + Annex 1 (2022 revised). | FS-AN1-01 | OQ-BMS-INTERLOCK-01 |
| DS-AUTOCLAVE-68 | Annex 1 cycle-record content | Load lot, equipment / components listed, per-probe F0 evidence, BI/CI results, operator + verifier signatures | Default | FS-AN1-02 verbatim. | FS-AN1-02 | OQ-CYCLE-REPORT-01 |

### 4.10 Data Integrity (ALCOA+)

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUTOCLAVE-69 | Record attribution | All record writes carry AD-authenticated `user_id` from Kerberos ticket; no shared service accounts in audit-trail writes | Default | FS-DI-01. | FS-DI-01 | OQ-DI-ATTRIB-01 |
| DS-AUTOCLAVE-70 | Export format set | Structured PDF/A-3 (with embedded audit-trail extract) + CSV | Custom | FS-DI-02; PDF/A-3 supports embedded data for inspection. | FS-DI-02 | OQ-EXPORT-01 |
| DS-AUTOCLAVE-71 | Signature-time clock-skew check | LDT clock-skew check at every signature event; > 5 s skew rejects signature | Custom | FS-DI-03; clock-skew gate enforces ALCOA-Contemporaneous. | FS-DI-03 | OQ-DI-CLOCK-01 |
| DS-AUTOCLAVE-72 | Recalculation storage | Recalculations stored in `derivations` table referencing originals; originals immutable | Default | FS-DI-04. | FS-DI-04 | OQ-DI-IMMUTABLE-01 |
| DS-AUTOCLAVE-73 | Inspection retrieval SLA | ≤ 4 business hours via runbook `VEL-RB-INSPECTION-RETRIEVAL-001` | Custom | FS-DI-06 + PIC/S PI 041 expectation. | FS-DI-06 | OQ-INSPECTION-RETRIEVAL-01 |

### 4.11 Backup / Performance / Security

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUTOCLAVE-74 | DB backup mode | TimescaleDB nightly base-backup + continuous WAL archival to S3 (object-lock 30-day governance) | Custom | FS-BAK-01; PITR-validated by OQ-BAK-PITR-01. | FS-BAK-01 | OQ-BAK-PITR-01 |
| DS-AUTOCLAVE-75 | Restore-test cadence | Quarterly; DBA + QA witness; results filed in `RUN-BAK-RESTORE-NNN` | Default | FS-BAK-02. | FS-BAK-02 | OQ-BAK-RESTORE-01 |
| DS-AUTOCLAVE-76 | DR replication | PostgreSQL streaming replication active→standby; RPO ≤ 1 min, RTO ≤ 4 h documented in `VEL-RB-AUTOCLAVE-FAILOVER-001` | Custom | FS-BAK-03. | FS-BAK-03 | OQ-DR-REPLICATION-01 |
| DS-AUTOCLAVE-77 | Break-glass admin control | Local-admin sealed in HashiCorp Vault; dual-control check-out; post-use review by QA | Custom | FS-SEC-01 + FS-PART11-04 SoD; matches site OT PAM policy. | FS-SEC-01 | OQ-SEC-BREAKGLASS-01 |
| DS-AUTOCLAVE-78 | Removable-media policy | Blocked at Windows GPO level on both LDTs; vendor-approved engineering exception via temporary GPO exception under CR | Custom | FS-SEC-02; site OT-security baseline. | FS-SEC-02 | OQ-GPO-REMOVABLE-01 |
| DS-AUTOCLAVE-79 | Vulnerability scan cadence | Tenable Nessus monthly; criticals remediated within 30 days | Default | FS-SEC-03; site patching SOP. | FS-SEC-03 | OQ-SEC-SCAN-01 |

### 4.12 Training / Periodic Review

| CI-ID | Configuration item | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-AUTOCLAVE-80 | LMS access-gate | AD-group membership tied to Cornerstone LMS course-completion `VEL-CURR-AUTOCLAVE-<role>-v1`; users blocked at login if expired | Custom | FS-TRN-01. | FS-TRN-01 | OQ-LMS-GATE-01 |
| DS-AUTOCLAVE-81 | Annual refresher reminder | 60 d prior to expiry; access revoked on expiry; Sterilization Engineer + Microbiology competency assessment workflow | Custom | FS-TRN-02. | FS-TRN-02 | OQ-LMS-GATE-01 |
| DS-AUTOCLAVE-82 | Periodic-review runbook | `VEL-PR-AUTOCLAVE-YYYYMMDD` auto-collects configuration baselines, recipe inventory + change history, audit-trail review evidence, deviation summary, alarm trends, BI-cycle summary, steam-quality trends, backup-restore evidence, training currency | Custom | FS-PR-01. | FS-PR-01 | OQ-PR-RUNBOOK-01 |

## 5. Workflow + Business-Rule Design

### 5.1 Recipe lifecycle workflow

The Themis Recipe Service implements the workflow shown below. Every transition is signed (re-authenticated). Author ≠ Approver SoD enforced at the AD-group → role mapping. Recipe-loaded check happens at cycle-load time, not at recipe-approval time, so a recipe whose load family was retired between approval and use is still blocked at the right moment (DS-AUTOCLAVE-15).

```
DRAFT ─── Recipe Author submits ───► REVIEW
REVIEW ── Recipe Reviewer signs ────► APPROVED
                                       │
                                       │ Sterilization Engineer signs
                                       │  (DS-AUTOCLAVE-22)
                                       ▼
                                    EFFECTIVE  ──── (immutable; DS-AUTOCLAVE-17)
                                       │
                                       │ Recipe Approver retires
                                       ▼
                                    OBSOLETE
```

### 5.2 Cycle-execution business rules

1. Cycle-load handler validates: (a) recipe state = `EFFECTIVE`; (b) load family state = `QUALIFIED`; (c) cleanroom-pressure interlock OK (BMS OPC UA query, DS-AUTOCLAVE-67); (d) BD daily-gate satisfied if cycle-type is `porous_vacwrap` (DS-AUTOCLAVE-24); (e) leak-test currency satisfied (DS-AUTOCLAVE-46); (f) BI calendar satisfied (DS-AUTOCLAVE-55); (g) steam-quality at cabinet inlet within acceptance (DS-AUTOCLAVE-49). Any failure blocks load.
2. During cycle execution, F0 is computed continuously per DS-AUTOCLAVE-33; probe-drift > ± 0.5 °C excludes the probe (DS-AUTOCLAVE-38). If operational probe count falls below DS-AUTOCLAVE-39 minimum, the cycle fails.
3. At cycle end, the per-probe F0 release gate (DS-AUTOCLAVE-35) is evaluated. Any single load-probe F0 below target fails the cycle even if chamber-mean ≥ target.
4. Manual override during a product cycle (DS-AUTOCLAVE-36) requires dual signature and auto-creates a MasterControl deviation; the cycle report is flagged.
5. BI cycles route to Microbiology disposition (DS-AUTOCLAVE-53); failed BI auto-blocks load release.

### 5.3 Steam-quality gate at cycle start

The steam-quality gate at the cabinet inlet evaluates NCG, dryness, and superheat against DS-AUTOCLAVE-49 thresholds. If any parameter is outside acceptance, the cycle is blocked from advancing past preconditioning. Operator may choose to: (a) wait and re-check (boiler stabilisation); (b) record the steam-quality excursion and abort; (c) escalate to Sterilization Engineer for cabinet-side investigation. Manual override of the steam-quality gate is NOT permitted (no exception path) — this is a contamination-control invariant for sterile manufacturing.

## 6. Role-Permission Matrix Design

The matrix below lists every AD group → Themis role and the action-level permissions. SoD constraints from URS § 4 are encoded as cell-level denies even where the role would otherwise have the permission.

| Action / Role | Operator | Senior Op / Line Lead | Recipe Author | Recipe Reviewer | Recipe Approver (QA) | Steriliz. Eng. | Microbiology | Maintenance Eng. | Quality Reviewer | QA Compliance | System Admin | Auditor |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| View recipes (any state) | R | R | R | R | R | R | R | R | R | R | R | R |
| Author DRAFT recipe | — | — | C/U | — | — | — | — | — | — | — | — | — |
| Sign recipe REVIEW | — | — | — | S | — | — | — | — | — | — | — | — |
| Sign recipe APPROVED → EFFECTIVE | — | — | — | — | S | S (param sign-off only) | — | — | — | — | — | — |
| Retire recipe (→ OBSOLETE) | — | — | — | — | S | — | — | — | — | — | — | — |
| Load recipe for cycle | C | C | — | — | — | — | — | C (diagnostic / qual cycles only) | — | — | — | — |
| Start / pause / abort product cycle | C | C | — | — | — | — | — | — | — | — | — | — |
| Document load contents + BI/CI/PCD placement | C/U | C/U | — | — | — | — | — | — | — | — | — | — |
| Second-person verify critical step | — | S | — | — | — | — | — | — | — | — | — | — |
| Manual setpoint override during cycle (dual-sig) | S (op leg) | — | — | — | — | S (eng leg) | — | — | — | — | — | — |
| BI-cycle disposition | — | — | — | — | — | — | S | — | — | — | — | — |
| Quality-Reviewer cycle review | — | — | — | — | — | — | — | — | S | — | — | — |
| Quarterly platform / audit-trail review | — | — | — | — | — | — | — | — | — | S | — | — |
| Patch / AD group / historian admin | — | — | — | — | — | — | — | — | — | — | C/U | — |
| Run diagnostic / qualification / leak-test cycles | — | — | — | — | — | — | — | C | — | — | — | — |
| Read-only across recipes / cycles / audit trails | — | — | — | — | — | — | — | — | — | — | — | R |

Legend: R = read, C = create, U = update, S = sign (re-authenticated electronic signature), — = denied.

**Cell-level SoD denies (per URS § 4 separation-of-duties):**

- The user who recorded the operator-leg of a critical step (e.g., "load locked") is denied the verifier-leg signature for the same step (Operator ≠ Verifier on the same critical step).
- The user who authored a recipe revision is denied the Recipe Approver signature on the same revision (Recipe Author ≠ Approver of own recipe).
- The user who held the Sterilization Engineer parameter sign-off on a recipe is denied the Quality Reviewer cycle-review signature for cycles executed against that recipe (Sterilization Engineer ≠ Quality Reviewer for the same cycle).

## 7. Integration Design

Each interface row matches an IF-ID in FS § 5 + integration row in FS § 4.10.

| IF-ID | Counterparty | Endpoint | Protocol | Direction | AuthN | Message schema | Retry / DLQ | Audit emission | FS-IDs traced |
|---|---|---|---|---|---|---|---|---|---|
| IF-PLC-01 | Themis Controller | `opc.tcp://themis-ctrl.vel.local:4840` | OPC UA `Sign+Encrypt` `Basic256Sha256` | bidirectional | site PKI client cert | OPC UA tag tree (vendor) | local buffer on disconnect; reconnect-on-fault | tag-change → `themis_audit.PLC_TAG_CHANGE` | FS-CYC-* / FS-CYC-08 |
| IF-PASX-01 | PAS-X v3.2 | `https://pasx.vel.local/api/v3/recipes/{id}/download` | REST mTLS | inbound | mTLS + PAS-X service account | JSON `{recipe_id, version, sha256, signing_cert_chain}` | exponential backoff 1/2/4/8/16 s; alarm + audit on 5th fail | `themis_audit.RECIPE_DOWNLOAD` | FS-INT-PASX-01 |
| IF-PASX-02 | PAS-X v3.2 | `POST https://pasx.vel.local/api/v3/cycles/report` | REST mTLS | outbound | mTLS | JSON cycle-report payload (F0 per probe + alarms + BI/CI + signatures + steam-quality) | exponential backoff; DLQ at 5 attempts → deviation raised | `themis_audit.CYCLE_REPORT_PUSH` | FS-INT-PASX-02 |
| IF-PASX-03 | PAS-X v3.2 | `POST https://pasx.vel.local/api/v3/cycles/{id}/gate-clear` | REST callback | outbound | mTLS | JSON `{cycle_id, qa_review_sig_id, ts}` | best-effort with audit emission on persistent fail | `themis_audit.GATE_CLEAR_PUSH` | FS-INT-PASX-03 |
| IF-BMS-01 | Site BMS | `opc.tcp://bms-server.vel.local:4840` tag `BMS.CLN.GA.PRESS_DIFF` | OPC UA | inbound | site PKI client cert | OPC UA `MonitoredItem` subscription (1 s) | local-cache last value 60 s on disconnect | `themis_audit.BMS_INTERLOCK_VALUE` | FS-INT-BMS-01 |
| IF-AD-01 | AD / PKI | `ldaps://ad.vel.local:636` + `kerberos://ad.vel.local:88` | LDAPS + Kerberos | bidirectional | machine cert + Kerberos ticket | LDAP + Kerberos standard | local OT cached creds 24 h offline | `themis_audit.AUTHN_EVENT` (forwarded to Splunk index `gxp-authn`) | FS-INT-AD-01, FS-XSYS-AD-01 |
| IF-PTP-01 | Site PTP master | `ptp4l --interface=eth0 --master=ptp-master.vel.local` | IEEE 1588 (PTP) | inbound | none (network-isolated VLAN) | PTP standard messages | hold-over via local clock for 5 min if master lost | clock-skew > 1 s logged | FS-INT-NTP-01 |
| IF-EQMS-01 | MasterControl eQMS | `POST https://eqms.vel.local/api/v2/deviations` | REST mTLS | outbound | mTLS + workload-identity | JSON deviation payload incl. idempotency-key `vel-autoclave-override-{cycle_id}` | exponential backoff; DLQ at 5; idempotent on key | `themis_audit.DEVIATION_RAISED` | FS-CYC-05 |
| IF-PKI-01 | Site PKI | site-PKI cert-manager service | ACME-equivalent | bidirectional | machine cert | cert auto-rotation ≤ 12 m | retry on next interval | cert-rotation audit | FS-PLAT-06 |
| IF-VAULT-01 | HashiCorp Vault | `https://vault.vel.local/v1/kv/autoclave/service-accounts/*` | HTTPS AppRole | inbound | AppRole + Yubikey | KV v2 | retry on rotation interval | vault-access audit | FS-SEC-01 |

### 7.1 Integration sequence — cycle report push (IF-PASX-02)

1. Cycle reaches `COMPLETE` state (release gate pass) or `FAILED` state (release gate fail / probe-loss / abort / steam-quality block).
2. Themis-Manager renders cycle-report JSON payload including: per-probe F0 evidence, alarms list with ack metadata, BI/CI entries, all electronic signatures, steam-quality summary, override events.
3. `POST /api/v3/cycles/report` to PAS-X with mTLS handshake; idempotency-key `vel-autoclave-cycle-{cycle_id}`.
4. On 2xx: emit `CYCLE_REPORT_PUSH` audit event; mark cycle `report_pushed_at`.
5. On 4xx/5xx: exponential backoff (1, 2, 4, 8, 16 s); after 5 attempts → DLQ + raise deviation (DS-AUTOCLAVE-36 pattern); cycle remains in `report_push_failed` state until manually re-queued.
6. PAS-X-side EBR step `sterilizer cycle complete` consumes the report and gates downstream filling-line steps until Quality-Reviewer approval signature arrives via IF-PASX-03 callback.

## 8. Site-Deployed Components Design

The autoclave does NOT include any site-developed code in the GAMP Cat-4 sense — there are no Python scripts, custom integration adapters, Excel-VBA macros, or site-authored vendor-LBSPP business logic that would escalate this Cat 4 system to a hybrid Cat 4 + Cat 5. The four LBSPP hooks used (`OnCpuSwitchover`, `OnRecipeLoad`, `OnPmMissedCreateDeviation`-equivalent for override-deviation, `OnSignatureCommit`) are configured per Fedegari's *Themis LBSPP Configuration Reference v5.3* using declarative configuration only (event → audit-event-emission mapping, event → REST-call mapping) — they contain no site-authored procedural code.

Should the site later add a site-authored LBSPP (e.g., a Python script implementing a non-standard alarm-routing rule), that script would escalate the system to a hybrid Cat 4 + Cat 5 and the present DS would need to gain a § 8 mini-SDS sub-section per METHODOLOGY § 2B.4 rule 6.

## 9. References

### US — FDA
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .68, .180, .192.
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026).
- FDA *Guidance on Data Integrity and Compliance with cGMP* (2018).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EU GMP Annex 15 — Qualification and Validation.
- EU GMP Annex 1 (2022 revised).

### International — ISO / EN
- ISO 17665-1:2024.
- ISO 17665-2:2009.
- ISO 11140-1:2014.
- ISO 11138-1:2017.
- EN 285:2015+A1:2021.
- ICH Q9(R1).

### Industry guidance
- ISPE GAMP 5 (2nd Edition, 2022).
- PIC/S PI 041.
- PDA Technical Report TR1.
- USP <1211>, <55>.

### Vendor
- Fedegari — *FOB 3 / Themis Installation, Configuration, and Administration Reference* v5.3.
- Fedegari — *Themis Cycle-Design and F0 Calculation Theory of Operation* v3.0.
- Fedegari — *Themis Recipe Service Administrator Guide* v5.3.
- Fedegari — *Themis LBSPP Configuration Reference* v5.3.
- Siemens — *S7-1500F Safety Programming Manual* v2024-01 (safety-partition reference only; not configured here).

### Site
- `VEL-CCS-PLANT1-001` — Plant 1 Contamination Control Strategy per Annex 1 (2022 revised).
- `VEL-RB-AUTOCLAVE-FAILOVER-001` — LDT failover runbook.
- `VEL-RB-INSPECTION-RETRIEVAL-001` — Inspection-retrieval runbook.
- `SEC-AD-POLICY-001` — site AD password policy.

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-AUTOCLAVE-01 | FS-PLAT-01 |
| DS-AUTOCLAVE-02 | FS-PLAT-01 |
| DS-AUTOCLAVE-03 | FS-PLAT-01 |
| DS-AUTOCLAVE-04 | FS-PLAT-01 / FS-BAK-03 |
| DS-AUTOCLAVE-05 | FS-PLAT-02 |
| DS-AUTOCLAVE-06 | FS-PLAT-02 |
| DS-AUTOCLAVE-07 | FS-PLAT-03 |
| DS-AUTOCLAVE-08 | FS-PLAT-03 |
| DS-AUTOCLAVE-09 | FS-PLAT-04 |
| DS-AUTOCLAVE-10 | FS-PLAT-04 |
| DS-AUTOCLAVE-11 | FS-PLAT-05 |
| DS-AUTOCLAVE-12 | FS-PLAT-05 / FS-BAK-01 |
| DS-AUTOCLAVE-13 | FS-REC-01 |
| DS-AUTOCLAVE-14 | FS-REC-01 |
| DS-AUTOCLAVE-15 | FS-REC-02 / FS-F0-01 |
| DS-AUTOCLAVE-16 | FS-REC-03 |
| DS-AUTOCLAVE-17 | FS-REC-04 |
| DS-AUTOCLAVE-18 | FS-REC-05 / FS-CYCTYPE-01 / FS-CYCTYPE-02 / FS-CYCTYPE-03 / FS-CYCTYPE-04 |
| DS-AUTOCLAVE-19 | FS-REC-05 |
| DS-AUTOCLAVE-20 | FS-REC-05 |
| DS-AUTOCLAVE-21 | FS-CYCTYPE-01 |
| DS-AUTOCLAVE-22 | FS-REC-06 |
| DS-AUTOCLAVE-23 | FS-REC-07 |
| DS-AUTOCLAVE-24 | FS-BD-01 / FS-CYCTYPE-05 |
| DS-AUTOCLAVE-25 | FS-CYCTYPE-02 |
| DS-AUTOCLAVE-26 | FS-CYCTYPE-03 |
| DS-AUTOCLAVE-27 | FS-CYCTYPE-03 |
| DS-AUTOCLAVE-28 | FS-CYCTYPE-04 / FS-CYCTYPE-05 |
| DS-AUTOCLAVE-29 | FS-CYC-01 |
| DS-AUTOCLAVE-30 | FS-CYC-02 |
| DS-AUTOCLAVE-31 | FS-CYC-02 / FS-SQ-01 |
| DS-AUTOCLAVE-32 | FS-CYC-03 / FS-PERF-01 |
| DS-AUTOCLAVE-33 | FS-CYC-03 |
| DS-AUTOCLAVE-34 | FS-CYC-03 / FS-DI-05 |
| DS-AUTOCLAVE-35 | FS-CYC-04 |
| DS-AUTOCLAVE-36 | FS-CYC-05 / FS-PART11-04 |
| DS-AUTOCLAVE-37 | FS-CYC-06 |
| DS-AUTOCLAVE-38 | FS-CYC-07 |
| DS-AUTOCLAVE-39 | FS-CYC-07 |
| DS-AUTOCLAVE-40 | FS-CYC-08 / FS-DI-03 |
| DS-AUTOCLAVE-41 | FS-CYC-08 |
| DS-AUTOCLAVE-42 | FS-F0-01 |
| DS-AUTOCLAVE-43 | FS-F0-02 |
| DS-AUTOCLAVE-44 | FS-F0-03 |
| DS-AUTOCLAVE-45 | FS-BD-01 |
| DS-AUTOCLAVE-46 | FS-LEAK-01 |
| DS-AUTOCLAVE-47 | FS-LEAK-01 |
| DS-AUTOCLAVE-48 | FS-SQ-01 |
| DS-AUTOCLAVE-49 | FS-SQ-01 |
| DS-AUTOCLAVE-50 | FS-SQ-01 |
| DS-AUTOCLAVE-51 | FS-SQ-02 |
| DS-AUTOCLAVE-52 | FS-BI-01 |
| DS-AUTOCLAVE-53 | FS-BI-02 |
| DS-AUTOCLAVE-54 | FS-CI-01 |
| DS-AUTOCLAVE-55 | FS-BI-03 |
| DS-AUTOCLAVE-56 | FS-AUD-01 |
| DS-AUTOCLAVE-57 | FS-AUD-02 |
| DS-AUTOCLAVE-58 | FS-AUD-03 |
| DS-AUTOCLAVE-59 | FS-AUD-04 |
| DS-AUTOCLAVE-60 | FS-PART11-01 |
| DS-AUTOCLAVE-61 | FS-PART11-02 |
| DS-AUTOCLAVE-62 | FS-PART11-03 |
| DS-AUTOCLAVE-63 | FS-PART11-04 |
| DS-AUTOCLAVE-64 | FS-PART11-05 |
| DS-AUTOCLAVE-65 | FS-PART11-06 |
| DS-AUTOCLAVE-66 | FS-PART11-07 |
| DS-AUTOCLAVE-67 | FS-AN1-01 |
| DS-AUTOCLAVE-68 | FS-AN1-02 |
| DS-AUTOCLAVE-69 | FS-DI-01 |
| DS-AUTOCLAVE-70 | FS-DI-02 |
| DS-AUTOCLAVE-71 | FS-DI-03 |
| DS-AUTOCLAVE-72 | FS-DI-04 |
| DS-AUTOCLAVE-73 | FS-DI-06 |
| DS-AUTOCLAVE-74 | FS-BAK-01 |
| DS-AUTOCLAVE-75 | FS-BAK-02 |
| DS-AUTOCLAVE-76 | FS-BAK-03 |
| DS-AUTOCLAVE-77 | FS-SEC-01 |
| DS-AUTOCLAVE-78 | FS-SEC-02 |
| DS-AUTOCLAVE-79 | FS-SEC-03 |
| DS-AUTOCLAVE-80 | FS-TRN-01 |
| DS-AUTOCLAVE-81 | FS-TRN-02 |
| DS-AUTOCLAVE-82 | FS-PR-01 |

**FS-IDs in parent FS not covered by a DS-ID in this matrix:** FS-INT-PASX-01, FS-INT-PASX-02, FS-INT-PASX-03, FS-INT-BMS-01, FS-INT-AD-01, FS-INT-NTP-01, FS-PLAT-06, FS-XSYS-AD-01, FS-XSYS-BAK-01 — all covered in § 7 Integration Design rows and § 4.1 platform CIs (FS-PLAT-06 implicit via DS-AUTOCLAVE-12 cert-rotation reference and IF-PKI-01).

## 11. Appendix B — Design-level Risk Register

The risks below originate in design choices made in this DS, not in user wishes (URS) or functional behaviour (FS) or implementation defects (which are caught downstream by IQ/OQ/PQ). Per-design-item GxP criticality (R1/R2/R3) is inherited from the parent FS-ID. This register is a design-stage seed for the formal Risk Assessment (`VEL-RA-AUTOCLAVE-001`), not a substitute.

| DR-ID | Design-stage risk | Origin design choice | Mitigation reference |
|---|---|---|---|
| DR-01 | Cached SSO MFA on LDT could allow signature replay during a session | Re-auth at signing per DS-AUTOCLAVE-64 chose explicit MFA re-prompt; verify cached-creds-disabled at IdP | DS-AUTOCLAVE-64 + OQ-PART11-05 |
| DR-02 | F0 fixed-point implementation could disagree with vendor reference at edge-cases (very long cycles, micro-step integration) | DS-AUTOCLAVE-34 chose Python `decimal.Decimal`; vendor uses internal fixed-point | OQ-F0-CALC-01 reference-calculator comparison + IEEE-754 round-mode pin |
| DR-03 | PKI-cert auto-rotation could lapse during a long-running sealed-vial cycle | DS-AUTOCLAVE-12 chose ≤ 12-month validity with auto-rotation; cycle-time ≤ 4 h means no in-cycle rotation, but cert-rotation outage during cycle remains a risk | IF-PKI-01 + cert-rotation runbook + alert at 30 d before expiry |
| DR-04 | Synchronous `remote_apply` replication blocks the active LDT if standby goes down | DS-AUTOCLAVE-04 chose synchronous for RPO ≤ 1 min; degradation behavior must be exercised | OQ-DR-REPLICATION-01 + degraded-mode runbook |
| DR-05 | DBA dual-control could create operational delay during a real outage | DS-AUTOCLAVE-57 chose DBA dual-control over break-glass for append-only maintenance | Documented break-glass exception in `VEL-RB-AUTOCLAVE-FAILOVER-001` |
| DR-06 | OPC UA tag-tree drift between Themis vendor releases could break the cycle-load handler | DS-AUTOCLAVE-15 / IF-PLC-01 binds to vendor tag tree | Vendor-release impact-assessment per FS-VND-* analogue + FS-PLAT-04 vendor-release SOP |
| DR-07 | Ed25519 signature algorithm choice could be deprecated faster than RSA-2048 | DS-AUTOCLAVE-62 chose Ed25519 for performance | Algorithm-agility design: signature schema includes `alg` field for future rotation; periodic-review item in DS-AUTOCLAVE-82 |
| DR-08 | Steam-quality sensor (Spirax-Sarco SQM-100) calibration drift could mask wet-steam | DS-AUTOCLAVE-48 chose Spirax-Sarco | Sensor-calibration program in site calibration SOP (out of DS scope) + DS-AUTOCLAVE-79 vuln-scan does NOT cover this |
| DR-09 | BD daily-gate scope is per-day, not per-shift; shift-change without BD pass could allow stale gate | DS-AUTOCLAVE-45 chose per-calendar-day | Site SOP mandates BD at start-of-day; periodic-review item to consider per-shift gate after 1 y operating data |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
