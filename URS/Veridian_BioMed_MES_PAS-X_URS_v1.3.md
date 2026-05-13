---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline variant-synthesis, 2026-04-26; v1.2 enrichment 2026-05-13"
seed_corpus_basis:
  - "josephiuliucci/SDLC-PB URS_SCADA / URS_DataOps (industrial CSA style)"
  - "IfNoise/GACP-ERP URS.md"
  - "whharris917/pipe-dream SDLC-CQ-RS (claude-qms)"
  - "GAMP 5 (2nd Edition) Category 4 conventions for configured platforms"
  - "ISPE GAMP GPG MES (2018)"
  - "21 CFR Part 11; 21 CFR Part 211 (§§ .68, .180, .188, .192); EU GMP Annex 11; EU GMP Annex 1 (2022 revised); EU GMP Annex 15; EU GMP Annex 16; PIC/S PI 041; ANSI/ISA-88; ANSI/ISA-95"
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

# User Requirements Specification (URS)

## Manufacturing Execution System — Werum / Körber PAS-X v3.2

**Document Number:** VBM-URS-MES-001
**Version:** 1.2
**Effective Date:** 2026-05-13 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Site:** Veridian BioMed Inc., Sterile Fill-Finish Plant 2, Devens, Massachusetts, USA *(fictional)*
**System Owner:** Manufacturing IT Lead
**Process Owner:** VP Manufacturing
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (with optional Cat 5 sub-components for site-specific PAS-X recipes / tasklets)
**Project Mode:** Configuration project on commercial software product **Werum / Körber PAS-X v3.2** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .100, .180, .184, .186, .188 (production records), .192 (production record review); 21 CFR Part 210; EU GMP Annex 11 §§ 4 (validation), 6 (accuracy), 7 (data storage), 9 (audit trail), 10 (change management), 12 (security), 17 (printouts); EU GMP Annex 1 (2022 revised) §§ 5, 8, 9; EU GMP Annex 15; EU GMP Annex 16 (Certification by a Qualified Person + batch release); ICH Q9(R1); ICH Q10; PIC/S PI 041; ANSI/ISA-88 Part 1+2; ANSI/ISA-95 Part 1+2 (functional model of MES)

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _______________________ | _______________________ | __________ |
| Reviewer (Manufacturing IT Lead) | _______________________ | _______________________ | __________ |
| Reviewer (Process Owner — VP Manufacturing) | _______________________ | _______________________ | __________ |
| Reviewer (QA — Computer System Validation) | _______________________ | _______________________ | __________ |
| Reviewer (Master Data Owner) | _______________________ | _______________________ | __________ |
| Reviewer (SAP Integration Lead) | _______________________ | _______________________ | __________ |
| Reviewer (LIMS Integration Lead) | _______________________ | _______________________ | __________ |
| Reviewer (Functional Safety / Equipment Lead) | _______________________ | _______________________ | __________ |
| Approver (Head of Quality Assurance) | _______________________ | _______________________ | __________ |
| Approver (Qualified Person) | _______________________ | _______________________ | __________ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Risk-table reformatted per v1.1 sweep. |
| 1.2 | 2026-05-13 | (synthetic) | Tier T4 enrichment (150-250 req target). Added full module coverage: Order, Material, Equipment, Personnel, Yield/Variance, Weighing/Dispensing, Sampling, Genealogy, ERP/LIMS/DCS integration, Electronic Batch Release per § 211.192 + Annex 16, Multi-site/multi-recipe, BPMN, Reporting, Maintenance. Citations updated per METHODOLOGY § 2A.1. |

## Definitions and Acronyms

| Term | Definition |
|---|---|
| MES | Manufacturing Execution System (per ANSI/ISA-95 Level 3 function) |
| PAS-X | Werum / Körber PAS-X MES, version 3.2 (Körber Pharma) |
| eBR / EBR | Electronic Batch Record (instance) |
| MBR | Master Batch Record (recipe template) |
| Tasklet | PAS-X scripting unit (Java-based) for site-specific logic |
| LIMS | Laboratory Information Management System (LabWare LIMS 8) |
| ERP | Enterprise Resource Planning (SAP S/4HANA — site standard) |
| SCADA | Supervisory Control and Data Acquisition (Ignition 8.3 — site standard) |
| OEE | Overall Equipment Effectiveness |
| BPMN | Business Process Model and Notation (workflow engine) |
| ANSI/ISA-95 | Standard for enterprise-control system integration; defines MES function model (production scheduling, dispatch, execution, tracking, performance, data collection, quality, maintenance, personnel, inventory) |
| ANSI/ISA-88 | Batch control standard (procedure / unit procedure / operation / phase) |
| QP | Qualified Person (Directive 2001/83/EC Art. 51 + EU GMP Annex 16) |
| OOS | Out Of Specification |
| OOT | Out Of Trend |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| PI/PO | SAP Process Integration / Process Orchestration |
| PTP | Precision Time Protocol (IEEE 1588) |
| KPI | Key Performance Indicator |

---

## 1. Purpose

This URS defines the user, functional, regulatory, and non-functional requirements for the Manufacturing Execution System used to author, dispatch, and execute electronic batch records for sterile parenteral fill-finish operations at Veridian BioMed Plant 2. PAS-X is the system of record for shop-floor execution and is the single source of truth for EBRs that feed Annex 16 / QP certification.

The URS is the controlling input to the Functional Specification (`VBM-FS-MES-001`), Configuration Specification (`VBM-CS-MES-001`), Risk Assessment (`VBM-RA-MES-001`), IQ / OQ / PQ Protocols, Requirements Traceability Matrix (`VBM-RTM-MES-001`), and Vendor Assessment of Werum / Körber (`VBM-VA-WERUM-001`).

## 2. Scope

### 2.1 In scope

PAS-X is a multi-module MES platform. Each module is in scope at the level described below, with module-specific URS requirements in § 5.

- **PAS-X v3.2 platform core:** server cluster (production + DR), App Servers (3 active + 1 standby) on RHEL 9.2, Oracle 19c database with Data Guard physical-standby replication.
- **PAS-X Web Client** and **PAS-X Mobile** (iPad-based, gloved-hand mode) for shop-floor operators.
- **MBR Designer** — Master Batch Record authoring environment.
- **Order Management module** — production-order receipt + scheduling integration with ERP.
- **Material Management module** — material genealogy, dispensing, lot tracking, expiry control.
- **Equipment Management module** — equipment status, equipment-cycle records, maintenance interlocks.
- **Personnel Management module** — operator-training-record linkage, AD-role-to-PAS-X-role mapping, qualification-expiry blocking.
- **Recipe + Procedure Management module** — per-step approval, recipe hierarchy per ISA-88.
- **Yield + Variance + Deviation Management module** — yield calculation, OOS / OOT detection, deviation routing.
- **Weighing + Dispensing module** — connected-scale integration, label generation, dispense-verification.
- **Sampling Management module** — IPC + release sample creation, LIMS linkage.
- **Real-time Scheduling module** — line-level execution scheduling.
- **Genealogy + Traceability module** — full forward + backward traceability.
- **Electronic Batch Release module** — Annex 16 + Part 211.192 batch review + disposition.
- **Reporting + KPI module** — OEE, yield trends, deviation rate, audit-trail review evidence.
- **Site-specific tasklets** (Java) — Cat 5 sub-components.
- **Integrations:** SAP S/4HANA (ERP), LabWare LIMS 8, Ignition 8.3 (SCADA), Veeva Vault QualityDocs, MasterControl eQMS, AD federation, site PKI, PTP master.

### 2.2 Out of scope

- ERP-side master data (BoM, routings) — managed under `SAP-CSV-2024-007`.
- Equipment-level PLC programming — managed under per-equipment validations.
- Lab IT infrastructure — separately validated.
- Computer System Validation of LIMS 8 — `LIMS-CSV-2024-014`.
- SCADA / DCS validation — `SCADA-CSV-2024-002`.
- Veeva Vault QualityDocs platform validation — `VAULT-CSV-2024-001`.

### 2.3 System boundary diagram (textual)

```
                  ┌────────────────────────────────────────────┐
                  │   Active Directory (NWT.local) + Site PKI   │
                  │   + PTP master + LMS                        │
                  └───────────────────┬────────────────────────┘
                                      │ federated AuthN / AuthZ
                                      │
   ┌──────────────────────────────────▼──────────────────────────────┐
   │                          PAS-X v3.2                              │
   │  ┌─────────────────────────────────────────────────────────────┐│
   │  │ App Servers (3 act + 1 standby)  │  Oracle 19c + Data Guard ││
   │  └─────────────────────────────────────────────────────────────┘│
   │  Modules: Order │ Recipe/MBR │ EBR Execution │ Material │ Equip ││
   │           Personnel │ Yield │ Weighing │ Sampling │ Sched │ Gen ││
   │           Electronic Release │ Reporting │ Tasklets │ Workflow  ││
   └──┬─────────┬─────────┬──────────────┬──────────────┬───────────┘
      │         │         │              │              │
      ▼         ▼         ▼              ▼              ▼
   SAP        LIMS      Ignition    Veeva Vault    MasterControl
   S/4HANA   LabWare    8.3 SCADA   QualityDocs    eQMS
  (orders /  (samples / (equip /    (controlled    (deviations /
   yields /  results)   parameters/ docs in MBR)   CAPA /
   genealogy)           alarms)                     change control)
```

## 3. System Description and Intended Use

PAS-X is the system of record for shop-floor execution of sterile fill-finish operations. It receives a production order from SAP, instantiates an EBR from an approved MBR per ISA-88 procedure model, guides operators through dispensing (with connected-scale verification), compounding, sterile filtration, aseptic filling, capping, and inspection; captures process parameters from Ignition (mTLS OPC UA); captures in-process samples to LIMS; manages equipment status with maintenance interlocks; enforces personnel-qualification gating; computes yield + variance + deviation detection; and on completion writes batch genealogy, yield, and the executed eBR back to SAP / Vault and produces the electronic batch record for QP certification per EU GMP Annex 16 + 21 CFR § 211.192.

The system is GAMP Category 4. The PAS-X core platform is supplied by Werum / Körber under their internal SDLC; site-specific recipes and tasklets are Veridian-authored and assessed as Category 5 sub-components under separate change control.

## 4. User Roles

| Role | Description | Permissions |
|---|---|---|
| Operator | Shop-floor user. Executes EBR steps. | Execute steps; capture data; raise deviations; cannot edit MBR. |
| Senior Operator / Line Lead | Reviews operator entries in real time. | All Operator + second-person verification; cannot release. |
| Weighing Operator | Performs material dispensing at the connected scale. | Dispense + label-print + second-person verification request. |
| MBR Author | Authors and edits MBRs in PAS-X MBR Designer. | MBR create / edit; submit for review; no production-environment edits. |
| MBR Reviewer | Reviews MBRs in DRAFT state. | Review-only; submit for approval. |
| MBR Approver (QA) | Approves MBRs to EFFECTIVE. | Approve, retire MBR; cannot author. |
| Recipe Author (Per-step) | Authors per-step approval workflow recipes. | Per-step recipe edit under change control. |
| Production Supervisor | Dispatches EBRs and assigns operators. | Dispatch, reassign, escalate, schedule. |
| Quality Reviewer | Reviews EBR for batch release. | Review EBR, raise deviation, request rework. |
| Quality Approver (Batch Disposition) | Releases batch to market under QA authority. | Disposition (Release / Reject / Quarantine). |
| Qualified Person (QP) | EU certifies batch release per Directive 2001/83/EC Art. 51 + EU GMP Annex 16. | QP certification signature; cannot edit EBR content. |
| Master Data Owner | Owns ERP-side material / BoM master data slices replicated to PAS-X. | Master-data import + reconciliation; cannot dispense. |
| Equipment Coordinator | Maintains equipment status registry + maintenance windows. | Equipment-status changes + maintenance windows; cannot release. |
| Maintenance Engineer | Executes equipment maintenance + qualification cycles. | Maintenance task closure + equipment-return-to-service request. |
| Sampling Operator | Pulls IPC + release samples and creates LIMS sample. | Sample creation + chain-of-custody recording. |
| LIMS Bridge Operator | Manages LIMS-PAS-X reconciliation in case of out-of-band events. | LIMS-result entry override under CR. |
| Tasklet Developer | Develops Java tasklets per the Cat 5 SDLC. | Tasklet create / test / submit for review; no PROD deployment. |
| Tasklet Approver (QA) | Approves tasklet promotion to PROD. | Tasklet PROD promotion sign-off. |
| System Administrator | Installation, patching, AD groups, tasklet deployment. | Full system administration except MBR approval and batch disposition. |
| Auditor | Internal QA / external regulator. | Read all records and audit trails; cannot modify. |

**Separation of duties (URS-PART11-04):** an Operator cannot self-verify; an MBR Author cannot approve their own MBR; a Quality Reviewer cannot disposition; a Tasklet Developer cannot self-promote to PROD; the QP cannot also be the Quality Reviewer on the same batch.

## 5. User Requirements

### 5.1 Platform / Hardware

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | The system shall run on a redundant infrastructure with N+1 active App Servers and Data Guard physical-standby DB replication. |
| URS-PLAT-02 | H | R1 | The DR site (off-state replica) shall maintain RPO ≤ 15 minutes and RTO ≤ 4 hours during a full-site failover. |
| URS-PLAT-03 | M | R2 | The shop-floor mobile clients (iPad) shall operate in a hardened MDM-managed configuration; no general-purpose apps. |
| URS-PLAT-04 | H | R1 | All servers shall be patched per the site change-control SLA (security patches within 30 days of vendor release; major versions per change control). |
| URS-PLAT-05 | H | R1 | App Servers shall be load-balanced behind HAProxy with health-check probes every 5 s; failed nodes shall be removed from the pool automatically. |
| URS-PLAT-06 | M | R2 | App Servers shall be distributed across ≥ 2 fault domains within the primary data centre. |

### 5.2 Master Batch Record (MBR) Authoring and Lifecycle

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-MBR-01 | H | R1 | MBRs shall progress through an immutable lifecycle: DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE. |
| URS-MBR-02 | H | R1 | Only EFFECTIVE MBRs may be dispatched to production. |
| URS-MBR-03 | H | R1 | Each MBR transition shall require an electronic signature from a user holding the appropriate role (Author / Reviewer / Approver). |
| URS-MBR-04 | H | R1 | The MBR Author shall not be permitted to apply a Reviewer or Approver signature on the same MBR. |
| URS-MBR-05 | H | R1 | An EFFECTIVE MBR shall not be editable; any change creates a new revision via a controlled change request. |
| URS-MBR-06 | M | R2 | Every MBR shall reference a controlled SOP and Master Formula via Veeva Vault QualityDocs URN; broken references shall block APPROVAL. |
| URS-MBR-07 | H | R1 | MBR structure shall follow ANSI/ISA-88 procedure / unit-procedure / operation / phase hierarchy; phases shall map to equipment classes. |
| URS-MBR-08 | H | R1 | Per-step approval shall be supported: each step in an MBR shall be classified Critical / Major / Minor; Critical steps shall require second-person verification at execution time. |
| URS-MBR-09 | H | R1 | An MBR-effectivity window (`effective_from`, `effective_until`) shall be enforced at dispatch; an MBR outside the window shall not be permitted. |
| URS-MBR-10 | M | R2 | MBR-diff (per-step) renderer shall present old/new field by field on revision review. |

### 5.3 Order Management

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-ORD-01 | H | R1 | Production orders shall be received from SAP S/4HANA via PI/PO (iDoc / SOAP); each order shall include order-number, material, target quantity, schedule, MBR reference, plant / line. |
| URS-ORD-02 | H | R1 | Order ingestion shall be idempotent on (order_number, order_version); duplicates shall be rejected. |
| URS-ORD-03 | H | R1 | Order-acknowledgement back to SAP shall be sent within recipe-defined SLA (P95 ≤ 5 min). |
| URS-ORD-04 | M | R2 | Production Supervisor shall be able to reschedule orders within the dispatch window; rescheduling shall trigger an audit event. |
| URS-ORD-05 | H | R1 | Order cancellation shall be supported only when no EBR has been instantiated; post-instantiation cancellation requires QA approval. |

### 5.4 EBR Execution

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-EBR-01 | H | R1 | EBR instantiation from SAP production order shall be atomic — either the full EBR is created, or the order is left untouched with an error reported to SAP. |
| URS-EBR-02 | H | R1 | The system shall enforce step ordering per the MBR; out-of-sequence execution shall be blocked unless an authorized override is signed. |
| URS-EBR-03 | H | R1 | Critical steps (CIP cycle complete, sterilizing-grade filtration validated, fill weight verification, weighing complete) shall require a second-person verification with a separate signature. |
| URS-EBR-04 | H | R1 | Process parameters auto-captured from Ignition (temperature, pressure, fill weight, line speed) shall be timestamped and bound to the operator user ID; no manual override of auto-captured values. |
| URS-EBR-05 | H | R1 | An in-process check (IPC) failure shall block the next step until an authorized disposition is recorded. |
| URS-EBR-06 | H | R1 | Material dispensing shall validate dispensed mass against the MBR-defined tolerance and lot-genealogy; out-of-tolerance dispenses shall not advance. |
| URS-EBR-07 | M | R2 | EBR review shall be supported by a "review-by-exception" view highlighting deviations, manual entries, and overrides. |
| URS-EBR-08 | H | R1 | EBR-step "expected duration" shall be recipe-defined; significant deviation (> recipe threshold) shall flag review-by-exception. |
| URS-EBR-09 | H | R1 | EBR-step retry shall be supported under controlled circumstances; each retry shall be logged with a reason and shall preserve prior-attempt data. |

### 5.5 Material Management + Genealogy

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-MAT-01 | H | R1 | Material lots shall be tracked with: lot_id, material_code, supplier, receipt_date, expiry_date, qa_status (QUARANTINE / RELEASED / REJECTED), parent_lot (for sub-divided lots). |
| URS-MAT-02 | H | R1 | Only RELEASED lots within their expiry window shall be permitted for dispensing. |
| URS-MAT-03 | H | R1 | Material genealogy shall record all input lots consumed per EBR step; per-batch forward + backward traceability shall be computable in ≤ 30 s for any lot. |
| URS-MAT-04 | H | R1 | Serialised materials (e.g., serialised vials per DSCSA / FMD) shall be tracked at unit level with link to parent batch. |
| URS-MAT-05 | M | R2 | Material reservations shall be supported (soft + hard reservation) at order-instantiation; hard-reserved lots shall not be consumable by other orders. |
| URS-MAT-06 | H | R1 | Lot status changes (QUARANTINE → RELEASED → REJECTED) shall be received from SAP via integration; consumption shall be blocked when status changes mid-batch. |
| URS-MAT-07 | M | R2 | A campaign-end material-reconciliation report shall be runnable showing consumed vs theoretical mass per lot. |

### 5.6 Weighing + Dispensing

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-WGH-01 | H | R1 | The system shall integrate with the site's connected weighing-balance fleet (Mettler-Toledo / Sartorius) via OPC UA or vendor-specific drivers. |
| URS-WGH-02 | H | R1 | At dispense time, the operator shall be presented with target mass, ± tolerance, lot to dispense; the captured net mass shall be auto-recorded with timestamp, operator ID, balance ID. |
| URS-WGH-03 | H | R1 | Out-of-tolerance dispense shall block step closure; over-dispense shall require Quality Reviewer disposition (return material or accept). |
| URS-WGH-04 | H | R1 | Balance tare-state shall be verified before each dispense; tare-drift > recipe threshold shall block the dispense. |
| URS-WGH-05 | H | R1 | Label generation for dispensed material shall produce a barcode + human-readable label containing: lot, sub-lot, material, mass, expiry, EBR-link; label-printer failure shall block step closure. |
| URS-WGH-06 | M | R2 | Per-balance calibration-state shall be queried; out-of-cal balances shall not permit dispensing. |

### 5.7 Equipment Management + Maintenance Interlocks

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-EQ-01 | H | R1 | Equipment shall be registered with: equipment_id, class, location, status (READY / IN_USE / MAINTENANCE / OUT_OF_SERVICE / QUARANTINE), last-cleaning-cycle-ref, last-qualification-ref, qualification_expiry. |
| URS-EQ-02 | H | R1 | EBR step assignment shall verify equipment status = READY and qualification_expiry > now(); failure shall block step start. |
| URS-EQ-03 | H | R1 | Cleaning-cycle gate: equipment shall not be permitted for the next batch unless a valid cleaning-cycle reference exists within recipe-defined "dirty hold time"; missing / expired cleaning gate shall block. |
| URS-EQ-04 | H | R1 | Maintenance status shall integrate with the site CMMS (Phlox / Maximo); planned-maintenance windows shall block equipment use for the duration. |
| URS-EQ-05 | M | R2 | Equipment-cycle records (autoclave cycle ID, lyo cycle ID, coater cycle ID — from those system integrations) shall be linked into the EBR genealogy. |
| URS-EQ-06 | H | R1 | Equipment return-to-service after maintenance shall require Quality Reviewer approval + linked-test-execution evidence. |

### 5.8 Personnel Management + Training Linkage

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PER-01 | H | R1 | Operator login shall verify training-record state in LMS for the role + tasks they intend to execute; expired training shall block login or step assignment. |
| URS-PER-02 | H | R1 | Role-based access shall be derived from AD-group → PAS-X-role mapping; mapping changes shall require Manufacturing IT Lead + Head of QA signatures. |
| URS-PER-03 | H | R1 | Operator qualification (e.g., aseptic-technique competency for aseptic-area work) shall be checked at step assignment; expired qualifications shall block. |
| URS-PER-04 | M | R2 | Operator-fatigue / shift-handover information shall be captured at shift change for use in batch-review-by-exception. |
| URS-PER-05 | M | R2 | A "personnel-on-batch" report shall list all personnel who interacted with each batch for inspection. |

### 5.9 Recipe + Per-Step Approval (refinement of MBR)

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-REC-01 | H | R1 | Per-step recipes (sub-procedures invoked from MBRs) shall follow the same DRAFT → EFFECTIVE lifecycle as MBRs. |
| URS-REC-02 | H | R1 | Per-step approval shall be supported for high-criticality sub-procedures; approver signature shall be required at each invocation. |
| URS-REC-03 | M | R2 | Recipe-effectivity windows shall be respected at sub-step invocation. |

### 5.10 Yield + Variance + Deviation Management

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-YLD-01 | H | R1 | Per-batch yield shall be computed: actual_output / theoretical_output; recipe-defined acceptance band shall be enforced; out-of-band yields shall raise a deviation. |
| URS-YLD-02 | H | R1 | Variance (input mass − output mass − accounted-loss) shall be computed and trended; |variance| > recipe-defined threshold shall raise a deviation. |
| URS-YLD-03 | H | R1 | Deviations shall be classified (Critical / Major / Minor) with auto-routing rules: Critical → immediate QA notification + batch-closure block; Major → QA review before closure; Minor → log + review at batch closure. |
| URS-YLD-04 | H | R1 | Deviation lifecycle shall extend to MasterControl eQMS; the eQMS deviation ID shall be the source of truth post-disposition. |
| URS-YLD-05 | M | R2 | Annual product review aggregation feed shall expose yield + deviation trends per material / line. |

### 5.11 Sampling Management

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-SMP-01 | H | R1 | IPC + release samples shall be created in LIMS via REST at EBR-defined timepoints; sample creation failure shall raise an integration-deviation. |
| URS-SMP-02 | H | R1 | Sample chain-of-custody (operator pulling, sample-collection-time, sample-arrival-at-lab-time) shall be captured. |
| URS-SMP-03 | H | R1 | LIMS results shall be polled / received-via-webhook and bound to EBR steps; release-pending steps shall be gated on result_status = APPROVED. |
| URS-SMP-04 | H | R1 | OOS results shall raise a deviation per `OOS-PROC-001` and block batch release until investigation closure. |

### 5.12 Real-time Scheduling

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-SCH-01 | H | R1 | The system shall maintain a per-line schedule view (Gantt-style) showing planned + in-progress + completed EBRs. |
| URS-SCH-02 | M | R2 | The Supervisor shall be able to reschedule within the constraints of equipment availability, personnel qualification, and material availability. |
| URS-SCH-03 | M | R2 | Schedule changes shall propagate to SAP for ERP-side visibility. |

### 5.13 Workflow / Deviations / Disposition (BPMN)

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-WF-01 | H | R1 | Operators shall be able to raise a deviation against any step; deviations shall block step closure until disposition. |
| URS-WF-02 | H | R1 | Deviations of "Critical" classification shall escalate to QA on creation and require QA disposition before batch closure. |
| URS-WF-03 | M | R2 | Deviations shall be exportable to the site eQMS (MasterControl) on disposition; the eQMS link shall be the source of truth for the deviation lifecycle. |
| URS-WF-04 | H | R1 | Batch disposition (Release / Reject / Quarantine) shall require an electronic signature with meaning "release", applied by a user holding Quality Approver role, after QA review of all open items. |
| URS-WF-05 | H | R1 | Workflows shall be modelled in BPMN 2.0; workflow definitions shall be versioned + reviewable; deployment of new versions shall follow change control. |
| URS-WF-06 | M | R2 | Workflow-engine SLA: workflow-step transition latency P95 ≤ 1 s. |

### 5.14 Genealogy + Traceability

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-GEN-01 | H | R1 | Forward traceability: from any input lot, the system shall enumerate all batches produced consuming that lot in ≤ 30 s for a 24-month lookback. |
| URS-GEN-02 | H | R1 | Backward traceability: from any released batch, the system shall enumerate all input lots + equipment cycles + personnel + cleaning cycles in ≤ 30 s. |
| URS-GEN-03 | H | R1 | Genealogy snapshots shall be exportable as machine-readable JSON for inspection / DSCSA / FMD compliance. |

### 5.15 Integrations

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-INT-SAP-01 | H | R1 | The system shall receive production orders from SAP via PI/PO with confirmation acknowledgement. Failed or duplicate orders shall be rejected and logged. |
| URS-INT-SAP-02 | H | R1 | On batch completion, the system shall return yield, consumption, batch genealogy, and disposition to SAP within 5 minutes (P95). |
| URS-INT-SAP-03 | H | R1 | Material master + BoM slices shall be replicated from SAP via PI/PO; reconciliation report shall be produced daily; drift shall raise alarm. |
| URS-INT-SAP-04 | H | R1 | Material-status changes (QUARANTINE / RELEASED / REJECTED) shall be received from SAP in near real time; consumption blocking shall be enforced. |
| URS-INT-LIMS-01 | H | R1 | The system shall create LIMS samples for IPC and release tests, including method ID, expected timepoint, and EBR linkage. |
| URS-INT-LIMS-02 | H | R1 | The system shall retrieve LIMS results and gate downstream EBR steps (e.g. release-pending steps shall not start until release-test results are received and approved). |
| URS-INT-SCADA-01 | H | R1 | The system shall consume Ignition tags via OPC UA over TLS with mutual authentication; data signatures (timestamp, source) shall be preserved end-to-end. |
| URS-INT-SCADA-02 | H | R1 | SCADA-driven alarms relevant to batch quality (temperature excursions in compounding, pressure deviations on sterilizing-grade filtration) shall be raised to the operator on the EBR step in real time. |
| URS-INT-SCADA-03 | H | R1 | Equipment-cycle integrations (autoclave, lyo, coater) shall be received as completed-cycle reports; cycle-report receipt shall gate downstream EBR steps. |
| URS-INT-VAULT-01 | M | R2 | Controlled-document URN resolution in MBRs shall be cached locally with a 24-hour TTL; URN resolution failures shall not block EBR execution if a cached approved version is available. |
| URS-INT-EQMS-01 | H | R1 | Deviation lifecycle shall be reflected to MasterControl eQMS; the eQMS link shall be authoritative post-disposition. |
| URS-INT-CMMS-01 | H | R1 | Equipment-maintenance status shall be received from CMMS (Phlox / Maximo); planned maintenance windows shall block equipment use. |
| URS-INT-LMS-01 | H | R1 | Operator training records shall be queried from the LMS at login + step assignment; expired training shall block. |
| URS-INT-AD-01 | H | R1 | All authentication shall be via AD; service accounts via credential vault. |

### 5.16 Audit Trail and Records

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | The system shall maintain a contemporaneous, time-stamped, secure audit trail capturing user, action, old value, new value, and reason-for-change for all GMP-relevant operations across MBR, EBR, master data, equipment, personnel, deviation, and disposition entities. |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only; no user, including system administrators, shall be able to edit or delete entries. |
| URS-AUD-03 | H | R1 | The audit trail shall be reviewable in human-readable form and exportable for regulatory inspection. |
| URS-AUD-04 | H | R1 | Audit-trail review shall be performed by Quality Reviewer at EBR closure and by QA Compliance quarterly across the system. |
| URS-AUD-05 | H | R1 | Retention for MBRs, EBRs, audit trails shall be at least 25 years from product expiry (per 21 CFR § 211.180). |

### 5.17 21 CFR Part 11 / EU GMP Annex 11

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Electronic signatures shall meet 21 CFR § 11.50: printed name, date and time, meaning. |
| URS-PART11-02 | H | R1 | Each signature shall be unique to an individual; reuse and reassignment are prohibited per § 11.100. |
| URS-PART11-03 | H | R1 | Signatures shall be cryptographically bound to record state per § 11.70; any post-signature change invalidates the signature. |
| URS-PART11-04 | H | R1 | Separation of duties shall be enforced per role definitions in §4 (per § 11.10(d) + § 11.10(g)). |
| URS-PART11-05 | H | R1 | Re-authentication shall be required at the moment of signing per § 11.200 (no cached credentials). |
| URS-PART11-06 | H | R1 | The system shall comply with EU GMP Annex 11 §§ 4 (validation), 6 (accuracy), 7 (data storage), 9 (audit trails), 10 (change management), 12 (security), 17 (printouts). |
| URS-PART11-07 | H | R1 | Password / credential controls shall meet 21 CFR § 11.300. |
| URS-PART11-08 | H | R1 | Audit coverage per § 11.10(e); accurate-copy export per § 11.10(b); retention archive per § 11.10(c). |

### 5.18 Electronic Batch Release (21 CFR § 211.192 + EU GMP Annex 16)

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-REL-01 | H | R1 | Per § 211.192, batch production + control records shall be reviewed and approved by the quality control unit before release; PAS-X shall enforce the QA review gate. |
| URS-REL-02 | H | R1 | Per EU GMP Annex 16, batch certification by a QP shall be supported: a QP-signature step shall conclude the release workflow; the QP-signature shall reference the Annex 16 confirmation register. |
| URS-REL-03 | H | R1 | QP-signature shall not be permitted while any open Critical or Major deviation remains; Minor deviations require QP-noted disposition. |
| URS-REL-04 | H | R1 | A QP certification record (batch_id, qp_id, ts, statement, hash of reviewed EBR) shall be archived with the EBR. |
| URS-REL-05 | H | R1 | Batch certification shall produce an Annex 16-compliant Confirmation of Compliance document available for inspection. |
| URS-REL-06 | M | R2 | A QP-readiness dashboard shall present per-batch QA-review status, open-item count, and certification-ready flag. |

### 5.19 Data Integrity (ALCOA+)

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | All records Attributable to a named user. |
| URS-DI-02 | H | R1 | Records Legible — exportable as structured PDF and as an XML / PAS-X archive format. |
| URS-DI-03 | H | R1 | Records Contemporaneous — system clock synchronised to PKI-signed NTP / PTP. |
| URS-DI-04 | H | R1 | Original captured data preserved unaltered; derivations reference but do not overwrite originals. |
| URS-DI-05 | H | R1 | Calculations Accurate — verified per OQ. |
| URS-DI-06 | M | R2 | Complete, Consistent, Enduring (25-yr retention with verified backup), Available (retrievable within 4 business hours during inspection per PIC/S PI 041). |

### 5.20 Custom Tasklets (GAMP Category 5 sub-component)

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-DEV-01 | H | R1 | Custom Java tasklets shall be developed under a documented SDLC including code review, unit tests, integration tests, and security scan (Snyk + SonarQube). |
| URS-DEV-02 | H | R1 | Tasklet deployment to production shall require an approved change request and a successful regression run against the qualification test suite. |
| URS-DEV-03 | M | R2 | Tasklet source code shall be version-controlled in the site Git enterprise instance with signed commits. |
| URS-DEV-04 | H | R1 | Each tasklet shall have a documented intended use, GAMP-Cat-5 risk assessment, and FS / IQ / OQ test cases referenced in the RTM. |
| URS-DEV-05 | H | R1 | Tasklet test coverage shall be ≥ 90% on safety-relevant logic. |

### 5.21 Reporting + KPI

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-RPT-01 | H | R1 | OEE (Availability × Performance × Quality) shall be computed per line per shift per day; trended; exportable. |
| URS-RPT-02 | M | R2 | Yield-trend, deviation-rate-trend, change-control-velocity dashboards shall be available to Manufacturing IT Lead + Head of QA. |
| URS-RPT-03 | M | R2 | Annual Product Review (APR) feed shall aggregate per-product yield, deviation, OOS, OOT, change-control history. |
| URS-RPT-04 | M | R2 | Audit-trail-review-evidence summary shall be produced quarterly for QA Compliance. |
| URS-RPT-05 | M | R2 | Reports shall be parameterised (date range, line, product, role) + signed by their runner for inspection evidence. |

### 5.22 Multi-Site + Multi-Recipe Management

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-MSITE-01 | M | R2 | Although primary scope is Plant 2, the platform shall support multi-site recipe / MBR families with per-site effectivity; site-specific tasklets shall be partitionable. |
| URS-MSITE-02 | M | R2 | Cross-site recipe-transfer workflow (e.g., tech transfer from Plant 1 to Plant 2) shall preserve recipe genealogy. |

### 5.22a Label-Template Management

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-LBL-01 | H | R1 | Label templates (dispense, sample, work-in-progress, finished-good) shall be versioned + approved under change control; only EFFECTIVE templates shall be permitted at print time. |
| URS-LBL-02 | H | R1 | Label-template change shall require validation evidence (legibility test + barcode-scan-back); change approval requires QA + Manufacturing IT signatures. |
| URS-LBL-03 | M | R2 | Per-printer label rendering shall be verified via post-print barcode scan-back where the printer supports it. |

### 5.22b Inspection-Readiness

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-INSP-01 | H | R1 | The system shall support an "inspection mode" wherein an Auditor role obtains read-only access scoped to a specific batch / time-window without disturbing production records. |
| URS-INSP-02 | M | R2 | A signed inspection-bundle (EBR + audit trail + genealogy + QP cert) shall be exportable on demand ≤ 4 h per PIC/S PI 041. |

### 5.23 Performance, Availability, Backup

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PERF-01 | H | R1 | EBR step navigation latency shall be ≤ 1.5 seconds at the 95th percentile under nominal shop-floor load (200 concurrent operators across the plant). |
| URS-PERF-02 | M | R2 | MBR Designer shall save a typical 200-step MBR within 5 seconds. |
| URS-PERF-03 | H | R1 | Genealogy query (FS-GEN-01/02) shall return within 30 s for a 24-month lookback. |
| URS-AV-01 | H | R1 | System availability during operating hours shall be ≥ 99.5%; planned-maintenance windows are excluded. |
| URS-AV-02 | M | R2 | Single-app-server failure shall not interrupt active EBR sessions; transparent failover via session-replication. |
| URS-BAK-01 | H | R1 | Database shall be backed up nightly with PITR (continuous archived redo logs) supporting recovery to any point within 30 days. |
| URS-BAK-02 | H | R1 | A documented restore test shall be performed quarterly. |
| URS-BAK-03 | M | R2 | DR-site full-failover test shall be performed annually. |

### 5.24 Security

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-SEC-01 | H | R1 | All authentication via Active Directory (federated to PKI for signatures); no local accounts other than break-glass administrator. |
| URS-SEC-02 | H | R1 | All client-server traffic shall be TLS 1.2 or higher with current cipher suites. |
| URS-SEC-03 | H | R1 | Mobile clients shall be MDM-managed; loss / theft shall trigger remote wipe within 15 minutes of report. |
| URS-SEC-04 | M | R2 | Vulnerability scans (Tenable Nessus) shall run weekly; criticals shall be remediated within 30 days. |
| URS-SEC-05 | M | R2 | Privileged-access (System Administrator) sessions shall be recorded for QA review. |

### 5.25 Training

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | Production access shall require completed role-specific training recorded in the site LMS. |
| URS-TRN-02 | H | R1 | MBR Approvers, Quality Reviewers, Quality Approvers, and QPs shall additionally complete annual refresher training. |

### 5.26 Periodic Review

| ID | Priority | Risk | Requirement |
|---|---|---|---|
| URS-PR-01 | H | R1 | A periodic review shall be performed at least annually examining: configuration drift, audit-trail review evidence, deviation / change-control summary, backup-restore evidence, integration health, training currency, deviation rate trends, security posture. |
| URS-PR-02 | M | R2 | Periodic review shall be signed by the Manufacturing IT Lead and the Head of QA. |

### 5.27 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem with local OT cached credentials for offline operation; conditional-access policy `OT-MES Conditional Access (MFA at engineering / line workstation; operator stations named-location + role-bound smart cards)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T1 with RPO ≤ 4 h and RTO ≤ 4 BH; backup integration shall use Veeam Application-Aware processing with Oracle RMAN for the PAS-X Oracle backend plus file-level capture of recipe and order configuration; the application team shall participate in monthly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 15 y (batch-history) per the consuming-record schedule. |

### 5.28 Cross-System Integration — Helios audit-trail handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-HEL-01 | H | R1 | Werum PAS-X MES shall publish audit-trail events (Recipe lifecycle, batch order, EBR step execution, deviation, and material-genealogy events) to the Helios Audit Trail Review Workbench (`HBS-URS-ATR-001`) via the Helios ingest contract (JSON Lines, schema-registry pinned, Kafka topic `helios.ingest.veridian.pasx.v1`) within 5 minutes of event capture; 21 CFR § 11.10(e) audit-trail completeness shall be preserved end-to-end so that no event class is lost at the boundary. |
| URS-XINT-HEL-02 | H | R1 | Pre-handover audit-trail retention on the Werum PAS-X MES side shall be ≥ 15 y regardless of Helios availability; once Helios acknowledges ingest (per-message ack with idempotency key), Helios is the system-of-record for review and the Werum PAS-X MES local copy serves as the durability backstop until the local retention floor expires. |

### 5.29 Cross-System Integration — LMS competence handover

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XINT-LMS-01 | H | R1 | MES operator competence shall be enforced by an LMS-competence check at line/order activation (curriculum `MES-OPERATOR-<line_id>-<product_id>`); non-current operators shall be blocked from EBR step execution on the affected line/order with the lapse logged. |

## 6. Acceptance Criteria

The system shall enter validated routine GMP use when:

1. FS, CS, RA, IQ, OQ, PQ Protocols approved.
2. IQ executed; all critical findings closed.
3. OQ executed; all critical and major findings closed; minor findings dispositioned.
4. PQ executed including a representative end-to-end batch through SAP → PAS-X → LIMS → SAP including: order receipt, MBR dispatch, EBR execution with at least one Critical step + dispense step + sampling step + IPC fail + retry + deviation, batch yield + variance computation, deviation routing to eQMS, QA review, QP certification per Annex 16, SAP yield/genealogy return.
5. DR failover tested and documented within the OQ or PQ.
6. Validation Summary Report approved by Manufacturing IT Lead and Head of QA.
7. RTM shows every URS requirement mapped to at least one approved test case.
8. Operators trained and assessed on the gloved-hand mobile workflow.
9. Tasklets covered under Cat-5 sub-component validation per URS-DEV-04.

## 7. Constraints

- Site-specific tasklets are GAMP Cat 5 and require their own assessment per URS-DEV-04.
- Vendor patches and major version upgrades shall be evaluated under change control before deployment.
- Direct internet access from PAS-X servers is not permitted; package mirrors are internal.
- Cross-site recipe deployment requires Quality Council approval.

## 8. Assumptions

- Werum / Körber maintains its internal SDLC and continues to release validated patches.
- SAP S/4HANA is itself validated under `SAP-CSV-2024-007`.
- Ignition 8.3 is itself validated under `SCADA-CSV-2024-002`.
- LIMS 8 validated under `LIMS-CSV-2024-014`.
- Veeva Vault QualityDocs validated under `VAULT-CSV-2024-001`.
- MasterControl eQMS validated under `EQMS-CSV-2024-005`.
- LMS validated under `LMS-CSV-2024-003`.
- CMMS (Phlox / Maximo) validated under `CMMS-CSV-2024-006`.
- Active Directory and the site PKI are validated infrastructure.
- Connected-balance fleet qualified under `EQ-BAL-001`.

## 9. References

### US — FDA
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300 — Electronic Records; Electronic Signatures.
- 21 CFR Part 211 §§ .68 (automatic, mechanical, electronic equipment), .100 (production and process control), .180 (general retention), .184 (component / drug-product container records), .186 (master production records), .188 (batch production and control records), .192 (production record review).
- 21 CFR Part 210 — Current Good Manufacturing Practice in Manufacturing, Processing, Packing, or Holding of Drugs; General.
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026; supersedes the September 2025 guidance).
- FDA *Guidance on Data Integrity and Compliance with cGMP* (2018).
- Drug Supply Chain Security Act (DSCSA) — serialisation requirements (where applicable).

### EU
- EU GMP Annex 11 §§ 4 (validation), 6 (accuracy), 7 (data storage), 9 (audit trail), 10 (change management), 12 (security), 17 (printouts).
- EU GMP Annex 1 (2022 revised) §§ 5, 8, 9.
- EU GMP Annex 15 — Qualification and Validation.
- EU GMP Annex 16 — Certification by a Qualified Person and Batch Release.
- EudraLex Vol 4 Parts I + II + III.
- Directive 2001/83/EC Art. 51 (QP).
- Falsified Medicines Directive 2011/62/EU + Commission Delegated Regulation (EU) 2016/161 (FMD — serialisation).

### International — ICH / ISO
- ICH Q9(R1) — Quality Risk Management.
- ICH Q10 — Pharmaceutical Quality System.
- ICH Q12 — Technical and Regulatory Considerations for Pharmaceutical Product Lifecycle Management (where Established Conditions are applicable).

### Industry guidance
- ISPE GAMP 5 (2nd Edition, 2022).
- ISPE GAMP Good Practice Guide *MES* (2018).
- ISPE GAMP GPG *Records and Data Integrity*.
- PIC/S PI 041 — Good Practices for Data Management and Integrity.

### Standards
- ANSI/ISA-88 Part 1 + Part 2 — Batch Control.
- ANSI/ISA-95 Part 1 + Part 2 — Enterprise-Control System Integration; defines MES function model.
- BPMN 2.0 — Business Process Model and Notation.

### Vendor
- Werum / Körber — *PAS-X v3.2 Installation, Configuration, and Administration Reference*.
- Werum / Körber — *PAS-X Tasklet Development Guide*.
- Werum / Körber — *PAS-X release notes v3.2.x*.
- Mettler-Toledo / Sartorius — *Connected-Balance Integration Manuals*.

### Site
- `SAP-CSV-2024-007` SAP S/4HANA validation.
- `LIMS-CSV-2024-014` LabWare LIMS 8 validation.
- `SCADA-CSV-2024-002` Ignition validation.
- `VAULT-CSV-2024-001` Veeva Vault validation.
- `EQMS-CSV-2024-005` MasterControl validation.
- `LMS-CSV-2024-003` LMS validation.
- `CMMS-CSV-2024-006` CMMS validation.
- `EQ-BAL-001` connected-balance qualification.
- `OOS-PROC-001` OOS investigation procedure.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

