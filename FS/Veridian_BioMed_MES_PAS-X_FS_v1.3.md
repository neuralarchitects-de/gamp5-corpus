---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-26; v1.2 enrichment 2026-05-13"
seed_corpus_basis:
  - "VBM-URS-MES-001 (parent URS)"
  - "GAMP 5 (2nd ed.) Cat 4 conventions for configured MES platforms"
  - "ISPE GAMP Good Practice Guide MES (2018)"
  - "21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; EU GMP Annex 1 (2022 revised); EU GMP Annex 15; EU GMP Annex 16"
  - "ANSI/ISA-88; ANSI/ISA-95; BPMN 2.0"
parent_urs:
  document_number: VBM-URS-MES-001
  version: 1.2
  file: ../../URS/_generated/final/Veridian_BioMed_MES_PAS-X_URS_v1.3.md
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

## Manufacturing Execution System — Werum / Körber PAS-X v3.2

**Document Number:** VBM-FS-MES-001
**Version:** 1.2
**Effective Date:** 2026-05-13 *(synthetic)*
**Status:** Draft — synthetic-corpus use only
**Parent URS:** VBM-URS-MES-001 v1.2
**Site:** Veridian BioMed Inc., Sterile Fill-Finish Plant 2, Devens, Massachusetts, USA *(fictional)*
**System Owner:** Manufacturing IT Lead
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product, with site tasklets assessed as Category 5 sub-components
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 211 §§ .68, .100, .180, .184, .186, .188, .192; EU GMP Annex 11; EU GMP Annex 1 (2022 revised); EU GMP Annex 15; EU GMP Annex 16; ICH Q9(R1); ICH Q10; PIC/S PI 041; ANSI/ISA-88; ANSI/ISA-95; BPMN 2.0

---

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _______________________ | _______________________ | __________ |
| Reviewer (Validation Lead) | _______________________ | _______________________ | __________ |
| Reviewer (Manufacturing IT Lead) | _______________________ | _______________________ | __________ |
| Reviewer (QA — Computer System Validation) | _______________________ | _______________________ | __________ |
| Reviewer (SAP Integration Lead) | _______________________ | _______________________ | __________ |
| Reviewer (LIMS Integration Lead) | _______________________ | _______________________ | __________ |
| Approver (Head of Quality Assurance) | _______________________ | _______________________ | __________ |
| Approver (Qualified Person) | _______________________ | _______________________ | __________ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-26 | (synthetic) | Initial issue, derived from VBM-URS-MES-001 v1.0. |
| 1.2 | 2026-05-13 | (synthetic) | Expanded to per-URS-ID specifications (no range compression) per METHODOLOGY § 2A.7. Added Order / Material / Equipment / Personnel / Yield / Weighing / Sampling / Genealogy / Electronic Release (§ 211.192 + Annex 16) / Reporting / Multi-site / BPMN modules. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## Definitions and Acronyms

Inherited from VBM-URS-MES-001. Additional FS-specific terms:

| Term | Definition |
|---|---|
| FS | Functional Specification (this document) |
| Tasklet | PAS-X Java scripting unit; site-authored Cat-5 sub-component |
| MBR Designer | PAS-X authoring environment for Master Batch Records |
| RTM | Requirements Traceability Matrix (`VBM-RTM-MES-001`) |
| OPC UA | Open Platform Communications, Unified Architecture |
| PI/PO | SAP Process Integration / Process Orchestration |
| PTP | Precision Time Protocol (IEEE 1588) |
| MFC | Material Flow Controller (internal PAS-X service for material lifecycle) |

---

## 1. Purpose

This FS specifies, at the system-design level, how PAS-X v3.2 is configured and integrated to satisfy the user requirements expressed in `VBM-URS-MES-001` v1.2. Each functional specification entry maps to one or more URS requirements via the traceability matrix in Appendix A.

The FS is the controlling input to the Configuration Specification (`VBM-CS-MES-001`), the IQ / OQ / PQ Protocols, and the RTM. Site tasklets each have additional FS sub-documents (`VBM-FS-TASKLET-NNN`) referenced from § 4.20.

## 2. Scope

Per VBM-URS-MES-001 § 2.

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | Type | GAMP Category | Source / Vendor | Notes |
|---|---|---|---|---|---|
| C-01 | PAS-X App Server (×4) | COTS app | 4 | Werum / Körber | 3 active + 1 standby; RHEL 9.2; HAProxy load-balanced |
| C-02 | Oracle 19c DB | COTS infra | (infra) | Oracle | Data Guard physical-standby; site infra-validated |
| C-03 | MBR Designer | COTS app | 4 | Werum / Körber | Authoring client (Windows 11 Enterprise) |
| C-04 | PAS-X Web Client | COTS app | 4 | Werum / Körber | Browser-based shop-floor UI |
| C-05 | PAS-X Mobile (iPad) | COTS app | 4 | Werum / Körber | MDM-managed; gloved-hand mode |
| C-06 | Site Tasklets | Custom Java | **5** | Veridian | One FS per tasklet under change control |
| C-07 | SAP-PAS-X Adapter | Configured PI/PO interface | 4 | SAP | iDoc + SOAP envelopes |
| C-08 | LIMS Adapter | REST + SOAP connector | 4 | Werum / Körber | LabWare LIMS 8 endpoints |
| C-09 | OPC UA Client | COTS interface | 4 | Werum / Körber | Mutual-TLS to Ignition 8.3 |
| C-10 | Vault Adapter | REST connector | 4 | Werum / Körber | URN resolution + 24-h cache |
| C-11 | eQMS Adapter | REST connector | 4 | Werum / Körber | MasterControl deviation push |
| C-12 | CMMS Adapter | REST connector | 4 | Werum / Körber | Phlox / Maximo equipment-status |
| C-13 | LMS Adapter | REST connector | 4 | Werum / Körber | Training-record query |
| C-14 | Connected-Balance Driver | OPC UA + vendor RS232/Ethernet | 4 | Werum / Körber + balance vendor | Mettler / Sartorius |
| C-15 | Label Printer Driver | ZPL / CUPS | 4 | (vendor) | Zebra ZT411 |
| C-16 | Workflow Engine | BPMN 2.0 engine | 4 | Werum / Körber | versioned definitions |
| C-17 | Reporting Engine | COTS BI | 4 | Werum / Körber + Apache Superset | OEE / yield / deviation |
| C-18 | AD / PKI | COTS infra | (infra) | Microsoft | AuthN + sig certs |
| C-19 | PTP master | COTS infra | (infra) | (site) | IEEE 1588 |
| C-20 | HashiCorp Vault | COTS secrets | (infra) | HashiCorp | short-lived service creds |

### 3.2 Logical Architecture

```
                     ┌──────────────────────────────────────────────┐
                     │  Active Directory (NWT.local) + Site PKI      │
                     │  + PTP + LMS                                  │
                     └────────────────────┬──────────────────────────┘
                                          │
                ┌─────────────────────────▼─────────────────────────┐
                │                 PAS-X v3.2                         │
                │   ┌──────────────┐  ┌──────────────────────────┐  │
                │   │ App Servers  │  │   Oracle 19c             │  │
                │   │ (3 act + 1)  │◄─┤   + Data Guard           │  │
                │   └──────┬───────┘  └──────────────────────────┘  │
                │          │                                         │
                │   Modules: Order/MBR/EBR/Material/Equipment/        │
                │            Personnel/Yield/Weighing/Sampling/       │
                │            Scheduling/Genealogy/Release/Reporting/  │
                │            Workflow(BPMN)/Tasklets                  │
                └────┬──────┬──────┬───────┬─────┬─────┬─────┬──────┘
                     │      │      │       │     │     │     │
                     ▼      ▼      ▼       ▼     ▼     ▼     ▼
                   SAP   LIMS  Ignition Vault eQMS  CMMS  Balances+
                   S/4   LabW   8.3     Vault Master Phlox/ Printers
                  PI/PO  REST  OPC UA   REST Control Maximo OPC UA
```

### 3.3 Functional Modules

| Module | Description | URS sections |
|---|---|---|
| M-PLAT | Platform / hardware / DR | URS-PLAT-* |
| M-MBR | MBR authoring + lifecycle | URS-MBR-* |
| M-ORD | Order management | URS-ORD-* |
| M-EBR | EBR execution | URS-EBR-* |
| M-MAT | Material management | URS-MAT-* |
| M-WGH | Weighing + dispensing | URS-WGH-* |
| M-EQ | Equipment + maintenance | URS-EQ-* |
| M-PER | Personnel + training | URS-PER-* |
| M-REC | Per-step recipe / sub-procedure | URS-REC-* |
| M-YLD | Yield / variance / deviation | URS-YLD-* |
| M-SMP | Sampling | URS-SMP-* |
| M-SCH | Real-time scheduling | URS-SCH-* |
| M-WF | Workflow / deviation / disposition (BPMN) | URS-WF-* |
| M-GEN | Genealogy | URS-GEN-* |
| M-INT | Integrations | URS-INT-* |
| M-AUD | Audit trail | URS-AUD-* |
| M-PART11 | Part 11 / signatures / SoD | URS-PART11-* |
| M-REL | Electronic batch release (Annex 16 + § 211.192) | URS-REL-* |
| M-DI | Data integrity (ALCOA+) | URS-DI-* |
| M-DEV | Custom tasklet SDLC | URS-DEV-* |
| M-RPT | Reporting + KPI | URS-RPT-* |
| M-MSITE | Multi-site / multi-recipe | URS-MSITE-* |
| M-PERF | Performance / availability / backup | URS-PERF-*, URS-AV-*, URS-BAK-* |
| M-SEC | Security | URS-SEC-* |
| M-TRN | Training | URS-TRN-* |
| M-PR | Periodic review | URS-PR-* |

---

## 4. Functional Specifications

### 4.1 Platform / Hardware (M-PLAT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | Deploy 3 active App Servers behind HAProxy with health-checks every 5 s; 1 standby auto-promoted on failure. Oracle 19c with Data Guard physical-standby; managed switchover via DGMGRL. |
| FS-PLAT-02 | URS-PLAT-02 | DR replica in secondary data centre. Async Data Guard with redo-log shipping; tested annually. RPO target ≤ 15 min validated by `OQ-DR-RPO-01`; RTO ≤ 4 h validated by `PQ-DR-01`. |
| FS-PLAT-03 | URS-PLAT-03 | Mobile clients on dedicated VLAN; MDM (Jamf Pro) profile blocks all non-allow-listed apps; remote-wipe on report. |
| FS-PLAT-04 | URS-PLAT-04 | Patch management via the site change-control SLA. Vendor security-bulletin subscription configured; impact assessment within 14 days; deployment within 30 days for criticals. |
| FS-PLAT-05 | URS-PLAT-05 | HAProxy configured with HTTP health-checks on `/health` endpoint every 5 s; failed nodes removed automatically + alert raised; verified `OQ-LB-HEALTH-01`. |
| FS-PLAT-06 | URS-PLAT-06 | App Servers distributed across ≥ 2 fault domains using rack/PDU diversity; topology recorded in CMDB. |

### 4.2 MBR Authoring and Lifecycle (M-MBR)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MBR-01 | URS-MBR-01 | MBR state machine implemented in PAS-X core lifecycle service: states {DRAFT, REVIEW, APPROVED, EFFECTIVE, OBSOLETE}; transitions validated server-side; out-of-state attempts return HTTP 409 + audit event. |
| FS-MBR-02 | URS-MBR-02 | Production dispatch endpoint rejects non-EFFECTIVE MBRs; rejection includes the actual state for diagnosis. |
| FS-MBR-03 | URS-MBR-03 | Each transition requires a re-authenticated electronic signature; the signing UI captures meaning ("author submit", "review", "approve"). Role enforced server-side from AD-group → PAS-X-role mapping. |
| FS-MBR-04 | URS-MBR-04 | Cross-role check at signing time: signer's user ID compared to recorded Author user ID; collision rejected with HTTP 403 + audit event. |
| FS-MBR-05 | URS-MBR-05 | EFFECTIVE MBRs marked immutable in the data layer (DB constraint + service guard). Any change creates revision N+1 in DRAFT linked to the prior. |
| FS-MBR-06 | URS-MBR-06 | At APPROVAL, the Vault adapter resolves every referenced URN; unresolved references return validation errors that block approval until corrected. |
| FS-MBR-07 | URS-MBR-07 | MBR Designer enforces ISA-88 procedure / unit-procedure / operation / phase hierarchy; phases linked to equipment-class via equipment-master; verified `OQ-MBR-S88-HIER-01`. |
| FS-MBR-08 | URS-MBR-08 | Per-step `criticality` field (Critical / Major / Minor) drives second-person verification widget visibility at execution time; verified `OQ-MBR-PER-STEP-APPROVAL-01`. |
| FS-MBR-09 | URS-MBR-09 | MBR-effectivity fields (`effective_from`, `effective_until`) checked at dispatch time; outside-window MBRs rejected; verified `OQ-MBR-EFFECTIVITY-01`. |
| FS-MBR-10 | URS-MBR-10 | MBR-diff renderer compares JSON-serialised MBRs per-step + per-field; UI presents changed elements with old / new + change-reason. |

### 4.3 Order Management (M-ORD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ORD-01 | URS-ORD-01 | SAP order inbound via PI/PO iDoc + SOAP; fields validated server-side; missing required → reject + log. |
| FS-ORD-02 | URS-ORD-02 | Idempotency key = (order_number, order_version); duplicates rejected with `SAPORDER_DUPLICATE`. |
| FS-ORD-03 | URS-ORD-03 | Acknowledgement back to SAP within recipe-defined SLA (target P95 ≤ 5 min); measured by message-broker timestamps. |
| FS-ORD-04 | URS-ORD-04 | Reschedule action allowed within dispatch window for Production Supervisor role; transition logged. |
| FS-ORD-05 | URS-ORD-05 | Order-cancellation pre-EBR allowed; post-EBR requires QA approval signature; both states logged. |

### 4.4 EBR Execution (M-EBR)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-EBR-01 | URS-EBR-01 | EBR-from-order is a single transactional operation. Failure rolls back the EBR creation and returns a structured error to SAP via PI/PO; SAP-side alert raised. |
| FS-EBR-02 | URS-EBR-02 | Step-ordering enforced by the workflow engine; out-of-sequence attempts blocked by the UI and by the API. Override requires "supervisor override" signature with reason. |
| FS-EBR-03 | URS-EBR-03 | Critical-step flag in MBR; when present, the second-person verification widget is mandatory before step closure. Verifier user ID shall differ from Operator. |
| FS-EBR-04 | URS-EBR-04 | Process parameters captured via OPC UA subscription to Ignition tags; values written to EBR field with timestamp + source-tag + operator-user-id. UI presents auto-captured values read-only. |
| FS-EBR-05 | URS-EBR-05 | IPC step evaluator runs server-side after operator entry / LIMS result arrival. On FAIL, next step blocked; deviation auto-raised; QA notified. |
| FS-EBR-06 | URS-EBR-06 | Dispense step validates against MBR-defined tolerance (UCL / LCL / target) and lot-genealogy (lot status = RELEASED, expiry not lapsed). Out-of-tolerance attempts blocked. |
| FS-EBR-07 | URS-EBR-07 | Review-by-exception view filters EBR steps to those with deviations, manual entries, or overrides; configurable additional filters (CIP cycle, IPC, etc.). |
| FS-EBR-08 | URS-EBR-08 | Per-step expected_duration tracked; > recipe threshold flips step `flag_long_step = true`; surfaces in review-by-exception. |
| FS-EBR-09 | URS-EBR-09 | Step-retry endpoint preserves prior attempt(s) (immutable) and creates attempt N+1; retry reason captured + signature; verified `OQ-EBR-STEP-RETRY-01`. |

### 4.5 Material Management + Genealogy (M-MAT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MAT-01 | URS-MAT-01 | Material-master schema captures lot_id, material_code, supplier, receipt_date, expiry_date, qa_status, parent_lot; replicated from SAP. |
| FS-MAT-02 | URS-MAT-02 | MFC dispense API rejects non-RELEASED or expired lots with `LOT_NOT_RELEASED` / `LOT_EXPIRED`. |
| FS-MAT-03 | URS-MAT-03 | Genealogy linker writes (ebr_step_id, lot_id, consumed_mass, ts) per dispense; query API resolves forward / backward traceability. |
| FS-MAT-04 | URS-MAT-04 | Serialised-unit table links serial → parent_lot; FMD / DSCSA export per `RPT-SERIAL-001`. |
| FS-MAT-05 | URS-MAT-05 | Reservation engine supports soft + hard reservations; hard-reserved lots locked at the MFC dispense API. |
| FS-MAT-06 | URS-MAT-06 | SAP material-status change webhook updates lot.qa_status in near real time; in-progress consumption of an updated lot raises blocking deviation; verified `OQ-MAT-STATUS-SYNC-01`. |
| FS-MAT-07 | URS-MAT-07 | Material-reconciliation runner aggregates consumed-vs-theoretical per lot per campaign; export to PDF + CSV. |

### 4.6 Weighing + Dispensing (M-WGH)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-WGH-01 | URS-WGH-01 | Connected-balance driver supports Mettler-Toledo + Sartorius via OPC UA + vendor drivers; balance_id registered in equipment-master. |
| FS-WGH-02 | URS-WGH-02 | Dispense workflow: present target + tolerance + lot; capture mass + ts + operator + balance_id; auto-recorded read-only in EBR. |
| FS-WGH-03 | URS-WGH-03 | Out-of-tolerance dispense blocked at step-closure API; over-dispense routes to Quality Reviewer disposition workflow. |
| FS-WGH-04 | URS-WGH-04 | Pre-dispense tare check; tare-drift > recipe threshold blocks; verified `OQ-WGH-TARE-DRIFT-01`. |
| FS-WGH-05 | URS-WGH-05 | Label generator produces ZPL barcode + human-readable; printer-status polled; printer fault blocks step-closure; verified `OQ-WGH-LABEL-01`. |
| FS-WGH-06 | URS-WGH-06 | Per-balance calibration-state queried from balance master at dispense start; OUT_OF_CAL blocks. |

### 4.7 Equipment Management + Maintenance Interlocks (M-EQ)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-EQ-01 | URS-EQ-01 | Equipment-master schema: equipment_id, class, location, status, last_cleaning_cycle_ref, last_qualification_ref, qualification_expiry, current_user. |
| FS-EQ-02 | URS-EQ-02 | EBR step-start gate queries equipment_status = READY + qualification_expiry > now(); failure returns HTTP 409 + reason; verified `OQ-EQ-READY-GATE-01`. |
| FS-EQ-03 | URS-EQ-03 | Cleaning-gate: equipment-master `last_cleaning_cycle_ref` + recipe-defined `dirty_hold_max_h` evaluated at step-start; expired clean blocks; verified `OQ-EQ-CLEAN-GATE-01`. |
| FS-EQ-04 | URS-EQ-04 | CMMS adapter polls maintenance windows every 60 s; in-window equipment flips to MAINTENANCE state; verified `OQ-INT-CMMS-01`. |
| FS-EQ-05 | URS-EQ-05 | Equipment-cycle-record linker accepts autoclave cycle ID + lyo cycle ID + coater cycle ID via inbound webhooks; linked into EBR step record; verified `OQ-EQ-CYCLE-LINK-01`. |
| FS-EQ-06 | URS-EQ-06 | Return-to-service workflow requires linked test-execution evidence + Quality Reviewer signature; equipment flips READY only on workflow completion. |

### 4.8 Personnel Management + Training (M-PER)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PER-01 | URS-PER-01 | Login + step-assignment query LMS via REST; expired training returns HTTP 403 + reason; verified `OQ-PER-TRAIN-GATE-01`. |
| FS-PER-02 | URS-PER-02 | AD-group → PAS-X-role mapping table managed under change control; mapping changes require Manufacturing IT Lead + Head of QA signatures; verified `OQ-PER-AD-MAP-01`. |
| FS-PER-03 | URS-PER-03 | Operator-qualification registry: per-operator competency list with expiry; step-assignment cross-checks step.required_qualifications ⊆ operator.qualifications; verified `OQ-PER-QUAL-GATE-01`. |
| FS-PER-04 | URS-PER-04 | Shift-handover capture UI; entries linked to subsequent EBR-step records. |
| FS-PER-05 | URS-PER-05 | Personnel-on-batch report enumerates all signers + verifiers + step-executors per batch. |

### 4.9 Recipe + Per-Step Sub-Procedures (M-REC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REC-01 | URS-REC-01 | Per-step recipe (sub-procedure) lifecycle mirrors MBR-lifecycle; same {DRAFT...OBSOLETE} states; transition signatures required. |
| FS-REC-02 | URS-REC-02 | Per-step approver signature at sub-procedure invocation captured; meaning = "per-step approval". |
| FS-REC-03 | URS-REC-03 | Effectivity windows respected at sub-step invocation; outside-window rejected. |

### 4.10 Yield + Variance + Deviation (M-YLD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-YLD-01 | URS-YLD-01 | Per-batch yield engine computes actual / theoretical; recipe-defined acceptance band; out-of-band auto-raises deviation; verified `OQ-YLD-CALC-01`. |
| FS-YLD-02 | URS-YLD-02 | Variance = input_mass − output_mass − accounted_loss; |variance| > threshold raises deviation; verified `OQ-YLD-VARIANCE-01`. |
| FS-YLD-03 | URS-YLD-03 | Deviation classification engine assigns Critical / Major / Minor per recipe rules; routes per FS-WF-02; verified `OQ-YLD-DEV-CLASS-01`. |
| FS-YLD-04 | URS-YLD-04 | Deviation eQMS-link maintained; eQMS deviation ID becomes the source-of-truth post-disposition; verified `OQ-YLD-EQMS-LINK-01`. |
| FS-YLD-05 | URS-YLD-05 | APR feed aggregates yield + deviation + OOS + OOT trends per material / line. |

### 4.11 Sampling Management (M-SMP)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SMP-01 | URS-SMP-01 | Sample creation via LIMS REST endpoint with method ID, expected timepoint, EBR linkage; failure raises an integration-exception deviation. |
| FS-SMP-02 | URS-SMP-02 | Chain-of-custody UI captures sample-pull-time, operator, container labels, sample-arrival-at-lab-time. |
| FS-SMP-03 | URS-SMP-03 | LIMS-result poll service + webhook receiver bind results to EBR steps; release-pending steps gated by result_status = APPROVED; verified `OQ-INT-LIMS-RESULT-01`. |
| FS-SMP-04 | URS-SMP-04 | OOS-result hook auto-creates `OOS-PROC-001` deviation + blocks batch release; verified `OQ-OOS-BLOCK-01`. |

### 4.12 Real-time Scheduling (M-SCH)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SCH-01 | URS-SCH-01 | Gantt-style schedule view rendered from order + EBR + equipment + personnel data; verified `OQ-SCH-GANTT-01`. |
| FS-SCH-02 | URS-SCH-02 | Reschedule API validates equipment / personnel / material availability before commit. |
| FS-SCH-03 | URS-SCH-03 | Schedule-change events POSTed to SAP for ERP-side visibility. |

### 4.13 Workflow / Deviation / Disposition / BPMN (M-WF)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-WF-01 | URS-WF-01 | Deviation entity attached to EBR step; step-closure validator blocks if any open deviation. |
| FS-WF-02 | URS-WF-02 | "Critical" classification triggers an immediate notification to QA distribution list; QA disposition required before batch closure. |
| FS-WF-03 | URS-WF-03 | On disposition, deviation pushed to MasterControl eQMS via REST adapter; PAS-X stores the eQMS deviation-ID as the source-of-truth link. |
| FS-WF-04 | URS-WF-04 | Disposition step at batch closure requires Quality Approver electronic signature with meaning "release"; record state transitions to RELEASED / REJECTED / QUARANTINED. |
| FS-WF-05 | URS-WF-05 | Workflows defined in BPMN 2.0 deployed to the workflow engine; version-controlled; deployment requires CR; verified `OQ-WF-BPMN-VER-01`. |
| FS-WF-06 | URS-WF-06 | Workflow-step transition latency P95 ≤ 1 s under nominal load; monitored. |

### 4.14 Genealogy + Traceability (M-GEN)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-GEN-01 | URS-GEN-01 | Forward-traceability query indexed for 24-mo lookback; P95 ≤ 30 s on representative dataset; verified `PQ-GEN-FORWARD-01`. |
| FS-GEN-02 | URS-GEN-02 | Backward-traceability query likewise; verified `PQ-GEN-BACKWARD-01`. |
| FS-GEN-03 | URS-GEN-03 | Genealogy export as machine-readable JSON per inspection / serialisation format; signed export bundle. |

### 4.15 Integrations (M-INT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-SAP-01 | URS-INT-SAP-01 | Inbound iDoc / SOAP via SAP PI/PO. Idempotency key = SAP order number + version; duplicates rejected with `SAPORDER_DUPLICATE`. |
| FS-INT-SAP-02 | URS-INT-SAP-02 | On disposition, a yield-and-genealogy iDoc + SOAP envelope is queued; delivery within 5 minutes (P95) measured by message-broker timestamps. |
| FS-INT-SAP-03 | URS-INT-SAP-03 | Material-master + BoM replication via PI/PO; daily reconciliation runner; drift raises alarm + lock-down option; verified `OQ-INT-SAP-MASTER-01`. |
| FS-INT-SAP-04 | URS-INT-SAP-04 | SAP material-status webhook updates lot state in near real time; in-progress consumption-block on status change verified `OQ-INT-SAP-STATUS-01`. |
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | Sample creation via LIMS REST endpoint with method ID, expected timepoint, EBR linkage; failure raises an integration-exception deviation. |
| FS-INT-LIMS-02 | URS-INT-LIMS-02 | LIMS poll service every 60 s for results on open samples; release-pending steps gated by sample status = `APPROVED`. |
| FS-INT-SCADA-01 | URS-INT-SCADA-01 | OPC UA client with mutual TLS to Ignition; subscribed tag list version-controlled. End-to-end signing of (timestamp, value, source-tag, certificate fingerprint) preserved in EBR record. |
| FS-INT-SCADA-02 | URS-INT-SCADA-02 | Alarm subscription routes batch-relevant alarms to the operator's current EBR step within 2 s of receipt; dismissal requires reason capture. |
| FS-INT-SCADA-03 | URS-INT-SCADA-03 | Equipment-cycle webhook receiver accepts cycle-completion payloads from autoclave / lyo / coater systems; binds to EBR step; gates downstream step closure; verified `OQ-INT-EQUIP-CYCLE-01`. |
| FS-INT-VAULT-01 | URS-INT-VAULT-01 | Vault URN cache (24-h TTL); on miss with cache present, cycle continues using cached version + warning audit event; on miss with no cache, cycle blocks. |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | MasterControl REST adapter for deviation push; status webhook back; verified `OQ-INT-EQMS-01`. |
| FS-INT-CMMS-01 | URS-INT-CMMS-01 | Phlox / Maximo REST adapter for equipment-maintenance windows; polled every 60 s; verified `OQ-INT-CMMS-01`. |
| FS-INT-LMS-01 | URS-INT-LMS-01 | LMS REST query at login + step-assignment; cached for 5 min to reduce load; verified `OQ-INT-LMS-01`. |
| FS-INT-AD-01 | URS-INT-AD-01 | AD federation; service accounts via HashiCorp Vault short-lived secrets. |

### 4.16 Audit Trail (M-AUD)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | All GMP-relevant operations on MBR, EBR, master data, material, equipment, personnel, deviation, config emit audit events with: user, action, entity-id, old-value, new-value, reason, timestamp (PTP-derived), client-IP, signature-event-id (if any). |
| FS-AUD-02 | URS-AUD-02 | Audit table is append-only at the DB level: revoked DELETE / UPDATE privileges; DBA dual-control for any maintenance. Application API exposes only read + insert. |
| FS-AUD-03 | URS-AUD-03 | Audit-trail review UI provides human-readable rendering with filters (user, time range, entity, action). Export to PDF + CSV; signed export bundle. |
| FS-AUD-04 | URS-AUD-04 | EBR-closure workflow includes a mandatory audit-trail-review checkbox by Quality Reviewer; quarterly platform review report generated by report-runner job. |
| FS-AUD-05 | URS-AUD-05 | Retention enforced by archival policy: ≥ 25 years from product expiry; archived records stored in immutable cold storage (`STG-ARCHIVE-LYFCYC-001`). |

### 4.17 21 CFR Part 11 / Annex 11 (M-PART11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Signature events render printed-name + date-time (PTP) + meaning string into the audit-trail and into PDF representations. |
| FS-PART11-02 | URS-PART11-02 | Signature credentials bound to AD identity. AD account deletion requires a documented deactivation event; reuse of user IDs is blocked at the AD level. |
| FS-PART11-03 | URS-PART11-03 | Signature payload (record-id, record-state-hash, signer-id, meaning, timestamp) is signed using site PKI; verification on every read. Tampered signatures fail verification and are surfaced in the UI as "INVALID — INVESTIGATE". |
| FS-PART11-04 | URS-PART11-04 | SoD enforced at signing API: signer's recorded prior actions on the same record evaluated against the SoD policy; conflicts rejected. |
| FS-PART11-05 | URS-PART11-05 | Signing UI re-prompts for password + AD MFA at every signature; cached creds disabled. |
| FS-PART11-06 | URS-PART11-06 | Annex 11 mapping to design controls: §4 → validation lifecycle; §7 → Oracle storage & backup; §9 → audit-trail config; §10 → change control via site QMS; §12 → SEC controls; §17 → printout templates with audit trail. |
| FS-PART11-07 | URS-PART11-07 | AD password policy per `SEC-AD-POLICY-001`. |
| FS-PART11-08 | URS-PART11-08 | Audit coverage per § 11.10(e); accurate-copy export per § 11.10(b); retention archive per § 11.10(c). |

### 4.18 Electronic Batch Release (M-REL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REL-01 | URS-REL-01 | QA-review gate at batch-closure workflow: all EBR steps shall carry a Quality Reviewer "review-complete" signature before disposition; verified `OQ-REL-QA-GATE-01`. |
| FS-REL-02 | URS-REL-02 | QP-certification step is the terminal node of the release workflow; QP-signature meaning = "Annex 16 certification"; references the Annex 16 confirmation register; verified `OQ-REL-QP-SIG-01`. |
| FS-REL-03 | URS-REL-03 | QP-sign endpoint queries open-deviation list; Critical or Major open deviations block; Minor open deviations require QP-noted disposition text; verified `OQ-REL-OPEN-DEV-BLOCK-01`. |
| FS-REL-04 | URS-REL-04 | QP certification record table: (batch_id, qp_id, ts, statement, ebr_hash) archived with the EBR; rendered into Confirmation of Compliance PDF; verified `OQ-REL-QP-RECORD-01`. |
| FS-REL-05 | URS-REL-05 | Confirmation of Compliance PDF template per Annex 16 Annex II; auto-generated on QP-sign; signed. |
| FS-REL-06 | URS-REL-06 | QP-readiness dashboard surfaces per-batch QA-review status + open-item count + certification-ready flag for QP intake. |

### 4.19 Data Integrity (M-DI)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | All record writes attributed to AD-authenticated user-id; no shared accounts. |
| FS-DI-02 | URS-DI-02 | EBR exportable as structured PDF (with audit trail) and as PAS-X XML archive format; both validated under OQ-EXPORT-01. |
| FS-DI-03 | URS-DI-03 | NTP synchronisation; PTP for shop-floor; clock-skew check at every signature event (>5 s skew rejects signature). |
| FS-DI-04 | URS-DI-04 | Original captured data immutable; derivations (e.g., calculated yield) reference the source value via stored lineage. |
| FS-DI-05 | URS-DI-05 | Calculation engine deterministic; verified per `OQ-CALC-01`. |
| FS-DI-06 | URS-DI-06 | Retention 25 years; verified backup; retrieval ≤ 4 business hours via the inspection-readiness runbook. |

### 4.20 Custom Tasklets (M-DEV)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DEV-01 | URS-DEV-01 | Tasklet SDLC controlled by `SDLC-MES-TASKLET-001`: code review, unit tests (≥ 90% statement coverage on safety logic), integration tests against PAS-X test instance, Snyk SCA scan, SonarQube quality gate. |
| FS-DEV-02 | URS-DEV-02 | Tasklet deployment via signed change-request package; promotion to PROD blocks if any regression test fails. |
| FS-DEV-03 | URS-DEV-03 | Source in site GitLab Enterprise with branch-protection + signed commits (GPG). |
| FS-DEV-04 | URS-DEV-04 | Each tasklet has its own FS (`VBM-FS-TASKLET-NNN`), Cat-5 RA, and a dedicated row in the RTM. |
| FS-DEV-05 | URS-DEV-05 | Coverage gate enforced at CI; PR blocked on coverage < 90% on safety-relevant logic. |

### 4.21 Reporting + KPI (M-RPT)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RPT-01 | URS-RPT-01 | OEE computation engine (Availability × Performance × Quality) per line per shift per day; persisted; verified `OQ-RPT-OEE-01`. |
| FS-RPT-02 | URS-RPT-02 | Superset-based dashboards (yield trend, deviation rate trend, change-control velocity) with role-gated access. |
| FS-RPT-03 | URS-RPT-03 | APR feed aggregator export per product on schedule; verified `OQ-RPT-APR-FEED-01`. |
| FS-RPT-04 | URS-RPT-04 | Quarterly audit-trail-review-evidence summary report runner. |
| FS-RPT-05 | URS-RPT-05 | Report-runner signs the produced bundle (PKI) with runner-user-id + report-parameters + ts; archived for inspection evidence. |

### 4.22 Multi-Site + Multi-Recipe (M-MSITE)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MSITE-01 | URS-MSITE-01 | Per-site effectivity fields on MBR / recipe / tasklet; deployment-target field; cross-site share enabled but isolated. |
| FS-MSITE-02 | URS-MSITE-02 | Cross-site recipe-transfer workflow preserves recipe genealogy + tech-transfer documentation links. |

### 4.22a Label-Template Management (M-LBL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-LBL-01 | URS-LBL-01 | Label-template registry with state machine {DRAFT, REVIEW, APPROVED, EFFECTIVE, OBSOLETE}; printer-driver fetches EFFECTIVE template by id + locale. |
| FS-LBL-02 | URS-LBL-02 | Template-change workflow requires legibility-test evidence-doc + barcode-scan-back test record + QA + Manufacturing IT signatures. |
| FS-LBL-03 | URS-LBL-03 | Post-print scan-back via attached scanner (where supported); mismatch raises an alert + step-closure block. |

### 4.22b Inspection-Readiness (M-INSP)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INSP-01 | URS-INSP-01 | Auditor role + inspection-mode scope: read-only window-bound access; cached snapshot prevents production-record contention. |
| FS-INSP-02 | URS-INSP-02 | Inspection-bundle exporter (EBR + audit + genealogy + QP cert) signed export; SLA ≤ 4 h via the inspection-readiness runbook. |

### 4.23 Performance / Availability / Backup (M-PERF)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PERF-01 | URS-PERF-01 | App servers sized for 250 concurrent operators (20% headroom over URS); P95 navigation latency ≤ 1.5 s validated under PQ-PERF-NAV-01. |
| FS-PERF-02 | URS-PERF-02 | MBR Designer save P95 ≤ 5 s for 200-step MBR; verified `OQ-MBR-PERF-01`. |
| FS-PERF-03 | URS-PERF-03 | Genealogy query P95 ≤ 30 s for 24-month dataset; indexed on lot_id + ebr_step_id; verified `PQ-PERF-GENEALOGY-01`. |
| FS-AV-01 | URS-AV-01 | Operating-hours availability ≥ 99.5% measured by external uptime probes; planned-maintenance excluded. |
| FS-AV-02 | URS-AV-02 | Session-replication across App Servers via shared Redis; transparent failover. |
| FS-BAK-01 | URS-BAK-01 | Oracle nightly backup + continuous archived redo logs in S3 (immutable / object-lock 30-day); PITR validated by `OQ-BAK-PITR-01`. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore-test runbook executed by DBA + QA witness; results filed in `RUN-BAK-RESTORE-NNN`. |
| FS-BAK-03 | URS-BAK-03 | Annual full DR-site failover exercise; results filed `RUN-DR-NNN`; verified `PQ-DR-FULL-01`. |

### 4.24 Security (M-SEC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SEC-01 | URS-SEC-01 | All authentication via federated AD; only break-glass administrator account local. Break-glass usage requires dual control + post-use review. |
| FS-SEC-02 | URS-SEC-02 | TLS 1.2+ enforced on all listener ports; ciphers per NIST SP 800-52 Rev 2; verified by `OQ-SEC-TLS-01`. |
| FS-SEC-03 | URS-SEC-03 | iPad MDM (Jamf Pro) configured for remote-wipe within 15 min of report; tested quarterly. |
| FS-SEC-04 | URS-SEC-04 | Tenable Nessus weekly scans; criticals to remediation in 30 days per the site security SOP. |
| FS-SEC-05 | URS-SEC-05 | Privileged sessions recorded via the bastion-host session-recorder; recordings retained 1 year for QA review. |

### 4.25 Training (M-TRN)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Production access gate: AD group membership tied to LMS course-completion attribute; users without completion blocked at login. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher reminder triggered 60 days prior to expiry; access revoked on expiry. |

### 4.26 Periodic Review (M-PR)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PR-01 | URS-PR-01 | Annual periodic-review run-book auto-collects: configuration baselines, audit-trail review evidence, deviation/CR summary, backup-restore evidence, integration health, training currency, deviation rate trends, security posture. |
| FS-PR-02 | URS-PR-02 | Periodic-review record signed by Manufacturing IT Lead and Head of QA via re-authenticated electronic signature; signature meaning recorded per Part 11 § 11.50. |

---


### 4.27 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem with local OT cached credentials for offline operation. Conditional-access binding to policy `OT-MES Conditional Access (MFA at engineering / line workstation; operator stations named-location + role-bound smart cards)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with Oracle RMAN for the PAS-X Oracle backend plus file-level capture of recipe and order configuration; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.28 Cross-System Integration — Helios handover (M-XINT-HEL)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-HEL-01 | URS-XINT-HEL-01 | Audit-event publisher emits Kafka topic `helios.ingest.veridian.pasx.v1` with schema-registry-pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`; at-least-once delivery; idempotency key `{source_system, event_id}`; back-pressure surfaced via Prometheus `helios_publish_lag_seconds` with 5-min alert at > 600 s. |
| FS-XINT-HEL-02 | URS-XINT-HEL-02 | Local audit-store retention policy enforces ≥ 15 y; Helios ack persisted as `helios_ack_ts` per event; periodic reconciliation job verifies parity (Helios row count == local published count) and raises a deviation in MasterControl on > 0.01% mismatch over a 24 h window. |


### 4.29 Cross-System Integration — LMS handover (M-XINT-LMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-LMS-01 | URS-XINT-LMS-01 | LMS-competence adapter `<sys>-LMS-CLIENT-1.x` performs `GET /lms/competence/{user_id}?curriculum=...` over mTLS + Entra workload-identity; cache TTL per system (12-24 h); on `current=false` the consumer blocks the gated action and records `lms_lapse_user={user_id}` in the consumer audit trail; periodic reconciliation job verifies that no gated action proceeded with a lapsed competence. |

## 5. Interface Specifications

| IF ID | URS ID | Counterparty | Protocol | Direction | Notes |
|---|---|---|---|---|---|
| IF-SAP-01 | URS-INT-SAP-01 | SAP S/4HANA | iDoc + SOAP via PI/PO | inbound | production order receipt; idempotent on order # + version |
| IF-SAP-02 | URS-INT-SAP-02 | SAP S/4HANA | iDoc + SOAP via PI/PO | outbound | yield, consumption, genealogy; ≤ 5 min P95 |
| IF-SAP-03 | URS-INT-SAP-03 | SAP S/4HANA | iDoc via PI/PO | inbound | material master / BoM |
| IF-SAP-04 | URS-INT-SAP-04 | SAP S/4HANA | REST webhook | inbound | material status changes |
| IF-LIMS-01 | URS-INT-LIMS-01 | LabWare LIMS 8 | REST + SOAP | outbound | sample creation |
| IF-LIMS-02 | URS-INT-LIMS-02 | LabWare LIMS 8 | REST poll + webhook | inbound | result retrieval |
| IF-SCADA-01 | URS-INT-SCADA-01 | Ignition 8.3 | OPC UA mTLS | inbound | tag values + alarms |
| IF-SCADA-03 | URS-INT-SCADA-03 | autoclave / lyo / coater | REST webhook | inbound | equipment-cycle reports |
| IF-VAULT-01 | URS-INT-VAULT-01 | Veeva Vault QualityDocs | REST | inbound | URN resolution |
| IF-EQMS-01 | URS-INT-EQMS-01 | MasterControl eQMS | REST | bidirectional | deviation push + status |
| IF-CMMS-01 | URS-INT-CMMS-01 | Phlox / Maximo | REST | inbound | maintenance windows |
| IF-LMS-01 | URS-INT-LMS-01 | LMS | REST | inbound | training records |
| IF-AD-01 | URS-SEC-01 | AD / PKI | LDAPS + Kerberos | bidirectional | AuthN/Z + signature certs |
| IF-PTP-01 | URS-DI-03 | PTP master | IEEE 1588 | inbound | time sync |
| IF-BAL-01 | URS-WGH-01 | Connected balances | OPC UA + vendor RS232/Eth | inbound | dispense capture |
| IF-PRT-01 | URS-WGH-05 | Label printer | ZPL / CUPS | outbound | label printing |

## 6. Data Model (high-level)

| Entity | Key Attributes | Notes |
|---|---|---|
| MBR | mbr_id, version, state, author, approver, vault_urns, steps[], created_at, effective_from, effective_until | Immutable when EFFECTIVE; ISA-88 hierarchy |
| EBR | ebr_id, mbr_id, mbr_version, sap_order, state, steps[], deviations[], signatures[], created_at | One per dispatch |
| EBR-Step | step_id, ebr_id, idx, type, criticality, captured_data, signatures[], deviation_id?, override?, attempt | Step-retry attempts versioned |
| Order | order_id, order_version, material, qty, schedule, mbr_ref, state | From SAP |
| Material-Lot | lot_id, material, supplier, receipt, expiry, qa_status, parent_lot | Replicated from SAP |
| Material-Reservation | res_id, lot_id, order_id, type(soft/hard), qty | |
| Dispense | dispense_id, step_id, lot_id, mass, balance_id, label_id, ts, operator_id, verifier_id | |
| Equipment | equipment_id, class, location, status, last_clean_ref, last_qual_ref, qual_expiry | |
| EquipmentCycle | ec_id, equipment_id, cycle_type, cycle_ref, started_at, ended_at | linked from autoclave/lyo/coater |
| Personnel | user_id, ad_dn, qualifications[], training_state | mirrored from AD + LMS |
| Deviation | dev_id, ebr_id, step_id?, classification, state, eqms_link, raised_by, disposition | Pushed to eQMS |
| Sample | sample_id, ebr_step_id, method_id, lims_sample_id, status | LIMS linkage |
| Yield | ebr_id, theoretical, actual, variance, in_band | |
| Signature | sig_id, record_id, record_state_hash, signer_id, meaning, timestamp, pki_signature | Cryptographically bound |
| QPCertification | cert_id, batch_id, qp_id, ts, ebr_hash, statement | Annex 16 |
| AuditEvent | event_id, user, action, entity_type, entity_id, old, new, reason, timestamp | Append-only |
| WorkflowDef | wf_id, version, bpmn_xml, state | Versioned BPMN |

## 7. Non-Functional Specifications

| NFR ID | Specification |
|---|---|
| NFR-01 | P95 EBR-step navigation ≤ 1.5 s @ 200 concurrent operators |
| NFR-02 | Availability ≥ 99.5% during operating hours |
| NFR-03 | RPO ≤ 15 min, RTO ≤ 4 h |
| NFR-04 | Audit trail append-only; tampering detectable by signature verification |
| NFR-05 | Data retention ≥ 25 years from product expiry |
| NFR-06 | Mobile remote-wipe within 15 min of report |
| NFR-07 | TLS 1.2+ enforced; ciphers per NIST SP 800-52 r2 |
| NFR-08 | Genealogy query P95 ≤ 30 s for 24-mo dataset |
| NFR-09 | Workflow-step transition P95 ≤ 1 s |
| NFR-10 | SAP-yield acknowledgement P95 ≤ 5 min |

## 8. Configuration Items (CI)

| CI ID | Item | Configured Value | Source |
|---|---|---|---|
| CI-01 | App Server count (active) | 3 | URS-PLAT-01 |
| CI-02 | App Server count (standby) | 1 | URS-PLAT-01 |
| CI-03 | Data Guard mode | physical-standby (async) | URS-PLAT-02 |
| CI-04 | DR RPO target | 15 min | URS-PLAT-02 |
| CI-05 | DR RTO target | 4 h | URS-PLAT-02 |
| CI-06 | Mobile MDM | Jamf Pro | URS-PLAT-03 |
| CI-07 | HAProxy health-check | 5 s | URS-PLAT-05 |
| CI-08 | MBR states | DRAFT,REVIEW,APPROVED,EFFECTIVE,OBSOLETE | URS-MBR-01 |
| CI-09 | MBR hierarchy model | ISA-88 procedure/UP/operation/phase | URS-MBR-07 |
| CI-10 | Step criticality enum | Critical / Major / Minor | URS-MBR-08 |
| CI-11 | Vault URN cache TTL | 24 h | URS-INT-VAULT-01 |
| CI-12 | LIMS poll interval | 60 s | URS-INT-LIMS-02 |
| CI-13 | CMMS poll interval | 60 s | URS-INT-CMMS-01 |
| CI-14 | LMS query cache | 5 min | URS-INT-LMS-01 |
| CI-15 | Audit retention | 25 y from expiry | URS-AUD-05 |
| CI-16 | TLS minimum | 1.2 | URS-SEC-02 |
| CI-17 | Signature MFA | required | URS-PART11-05 |
| CI-18 | Backup window | nightly + continuous redo | URS-BAK-01 |
| CI-19 | Restore test cadence | quarterly | URS-BAK-02 |
| CI-20 | DR failover test cadence | annual | URS-BAK-03 |
| CI-21 | Vuln-scan cadence | weekly | URS-SEC-04 |
| CI-22 | LMS gate | enforced via AD-group expiry | URS-TRN-01 |
| CI-23 | Workflow engine | BPMN 2.0; versioned definitions | URS-WF-05 |
| CI-24 | Tasklet coverage gate | ≥ 90% on safety logic | URS-DEV-05 |
| CI-25 | QP-cert blocking deviations | Critical + Major open | URS-REL-03 |

## 9. Constraints / Assumptions / Risks

- **Constraints (FS-level):** PAS-X core platform code is vendor-controlled; site customisation is limited to declarative configuration + tasklets.
- **Assumptions:** Werum / Körber maintains its SDLC; SAP is validated under `SAP-CSV-2024-007`; Ignition under `SCADA-CSV-2024-002`; AD + PKI are validated infrastructure; LIMS / Vault / eQMS / CMMS / LMS validated per their respective CSV records.
- **FS-level risks:** mis-mapped AD groups bypassing SoD (mitigated by FS-PART11-04 + role-mapping CR control); OPC UA cert expiry stalling SCADA capture (FS-INT-SCADA-01 + cert-rotation runbook); tasklet quality gate weakening (FS-DEV-01..05 + Cat-5 sub-component validation); ERP-MES master-data drift (FS-INT-SAP-03 daily reconciliation); QP-cert on open Critical deviation (FS-REL-03); equipment-cycle webhook missed (FS-INT-SCADA-03 + idempotent receiver).

## 10. References

- VBM-URS-MES-001 v1.2 (parent URS).
- 21 CFR Part 11; 21 CFR Part 211 §§ .68, .100, .180, .184, .186, .188, .192; 21 CFR Part 210.
- EU GMP Annex 11; EU GMP Annex 1 (2022 revised); EU GMP Annex 15; EU GMP Annex 16.
- Directive 2001/83/EC Art. 51 (QP).
- ICH Q9(R1); ICH Q10; ICH Q12.
- ISPE GAMP 5 (2nd ed., 2022); ISPE GAMP GPG *MES* (2018); ISPE GAMP GPG *Records and Data Integrity*; PIC/S PI 041.
- ANSI/ISA-88 Part 1 + Part 2; ANSI/ISA-95 Part 1 + Part 2; BPMN 2.0.
- Werum / Körber — *PAS-X v3.2 Configuration Reference*; *PAS-X Tasklet Development Guide*.

## 11. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID(s) | Notes |
|---|---|---|
| URS-PLAT-01 | FS-PLAT-01 | |
| URS-PLAT-02 | FS-PLAT-02 | |
| URS-PLAT-03 | FS-PLAT-03 | |
| URS-PLAT-04 | FS-PLAT-04 | |
| URS-PLAT-05 | FS-PLAT-05 | |
| URS-PLAT-06 | FS-PLAT-06 | |
| URS-MBR-01 | FS-MBR-01 | |
| URS-MBR-02 | FS-MBR-02 | |
| URS-MBR-03 | FS-MBR-03 | |
| URS-MBR-04 | FS-MBR-04 | |
| URS-MBR-05 | FS-MBR-05 | |
| URS-MBR-06 | FS-MBR-06 | |
| URS-MBR-07 | FS-MBR-07 | |
| URS-MBR-08 | FS-MBR-08 | |
| URS-MBR-09 | FS-MBR-09 | |
| URS-MBR-10 | FS-MBR-10 | |
| URS-ORD-01 | FS-ORD-01 | |
| URS-ORD-02 | FS-ORD-02 | |
| URS-ORD-03 | FS-ORD-03 | |
| URS-ORD-04 | FS-ORD-04 | |
| URS-ORD-05 | FS-ORD-05 | |
| URS-EBR-01 | FS-EBR-01 | |
| URS-EBR-02 | FS-EBR-02 | |
| URS-EBR-03 | FS-EBR-03 | |
| URS-EBR-04 | FS-EBR-04 | |
| URS-EBR-05 | FS-EBR-05 | |
| URS-EBR-06 | FS-EBR-06 | |
| URS-EBR-07 | FS-EBR-07 | |
| URS-EBR-08 | FS-EBR-08 | |
| URS-EBR-09 | FS-EBR-09 | |
| URS-MAT-01 | FS-MAT-01 | |
| URS-MAT-02 | FS-MAT-02 | |
| URS-MAT-03 | FS-MAT-03 | |
| URS-MAT-04 | FS-MAT-04 | |
| URS-MAT-05 | FS-MAT-05 | |
| URS-MAT-06 | FS-MAT-06 | |
| URS-MAT-07 | FS-MAT-07 | |
| URS-WGH-01 | FS-WGH-01 / IF-BAL-01 | |
| URS-WGH-02 | FS-WGH-02 | |
| URS-WGH-03 | FS-WGH-03 | |
| URS-WGH-04 | FS-WGH-04 | |
| URS-WGH-05 | FS-WGH-05 / IF-PRT-01 | |
| URS-WGH-06 | FS-WGH-06 | |
| URS-EQ-01 | FS-EQ-01 | |
| URS-EQ-02 | FS-EQ-02 | |
| URS-EQ-03 | FS-EQ-03 | |
| URS-EQ-04 | FS-EQ-04 | |
| URS-EQ-05 | FS-EQ-05 | |
| URS-EQ-06 | FS-EQ-06 | |
| URS-PER-01 | FS-PER-01 | |
| URS-PER-02 | FS-PER-02 | |
| URS-PER-03 | FS-PER-03 | |
| URS-PER-04 | FS-PER-04 | |
| URS-PER-05 | FS-PER-05 | |
| URS-REC-01 | FS-REC-01 | |
| URS-REC-02 | FS-REC-02 | |
| URS-REC-03 | FS-REC-03 | |
| URS-YLD-01 | FS-YLD-01 | |
| URS-YLD-02 | FS-YLD-02 | |
| URS-YLD-03 | FS-YLD-03 | |
| URS-YLD-04 | FS-YLD-04 | |
| URS-YLD-05 | FS-YLD-05 | |
| URS-SMP-01 | FS-SMP-01 / IF-LIMS-01 | |
| URS-SMP-02 | FS-SMP-02 | |
| URS-SMP-03 | FS-SMP-03 / IF-LIMS-02 | |
| URS-SMP-04 | FS-SMP-04 | |
| URS-SCH-01 | FS-SCH-01 | |
| URS-SCH-02 | FS-SCH-02 | |
| URS-SCH-03 | FS-SCH-03 | |
| URS-WF-01 | FS-WF-01 | |
| URS-WF-02 | FS-WF-02 | |
| URS-WF-03 | FS-WF-03 | |
| URS-WF-04 | FS-WF-04 | |
| URS-WF-05 | FS-WF-05 | |
| URS-WF-06 | FS-WF-06 | |
| URS-GEN-01 | FS-GEN-01 | |
| URS-GEN-02 | FS-GEN-02 | |
| URS-GEN-03 | FS-GEN-03 | |
| URS-INT-SAP-01 | FS-INT-SAP-01 / IF-SAP-01 | |
| URS-INT-SAP-02 | FS-INT-SAP-02 / IF-SAP-02 | |
| URS-INT-SAP-03 | FS-INT-SAP-03 / IF-SAP-03 | |
| URS-INT-SAP-04 | FS-INT-SAP-04 / IF-SAP-04 | |
| URS-INT-LIMS-01 | FS-INT-LIMS-01 / IF-LIMS-01 | |
| URS-INT-LIMS-02 | FS-INT-LIMS-02 / IF-LIMS-02 | |
| URS-INT-SCADA-01 | FS-INT-SCADA-01 / IF-SCADA-01 | |
| URS-INT-SCADA-02 | FS-INT-SCADA-02 / IF-SCADA-01 | |
| URS-INT-SCADA-03 | FS-INT-SCADA-03 / IF-SCADA-03 | |
| URS-INT-VAULT-01 | FS-INT-VAULT-01 / IF-VAULT-01 | |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 / IF-EQMS-01 | |
| URS-INT-CMMS-01 | FS-INT-CMMS-01 / IF-CMMS-01 | |
| URS-INT-LMS-01 | FS-INT-LMS-01 / IF-LMS-01 | |
| URS-INT-AD-01 | FS-INT-AD-01 / IF-AD-01 | |
| URS-AUD-01 | FS-AUD-01 | |
| URS-AUD-02 | FS-AUD-02 | |
| URS-AUD-03 | FS-AUD-03 | |
| URS-AUD-04 | FS-AUD-04 | |
| URS-AUD-05 | FS-AUD-05 | |
| URS-PART11-01 | FS-PART11-01 | |
| URS-PART11-02 | FS-PART11-02 | |
| URS-PART11-03 | FS-PART11-03 | |
| URS-PART11-04 | FS-PART11-04 | |
| URS-PART11-05 | FS-PART11-05 | |
| URS-PART11-06 | FS-PART11-06 | |
| URS-PART11-07 | FS-PART11-07 | |
| URS-PART11-08 | FS-PART11-08 | |
| URS-REL-01 | FS-REL-01 | |
| URS-REL-02 | FS-REL-02 | |
| URS-REL-03 | FS-REL-03 | |
| URS-REL-04 | FS-REL-04 | |
| URS-REL-05 | FS-REL-05 | |
| URS-REL-06 | FS-REL-06 | |
| URS-DI-01 | FS-DI-01 | |
| URS-DI-02 | FS-DI-02 | |
| URS-DI-03 | FS-DI-03 / IF-PTP-01 | |
| URS-DI-04 | FS-DI-04 | |
| URS-DI-05 | FS-DI-05 | |
| URS-DI-06 | FS-DI-06 | |
| URS-DEV-01 | FS-DEV-01 | |
| URS-DEV-02 | FS-DEV-02 | |
| URS-DEV-03 | FS-DEV-03 | |
| URS-DEV-04 | FS-DEV-04 | |
| URS-DEV-05 | FS-DEV-05 | |
| URS-RPT-01 | FS-RPT-01 | |
| URS-RPT-02 | FS-RPT-02 | |
| URS-RPT-03 | FS-RPT-03 | |
| URS-RPT-04 | FS-RPT-04 | |
| URS-RPT-05 | FS-RPT-05 | |
| URS-MSITE-01 | FS-MSITE-01 | |
| URS-MSITE-02 | FS-MSITE-02 | |
| URS-LBL-01 | FS-LBL-01 | |
| URS-LBL-02 | FS-LBL-02 | |
| URS-LBL-03 | FS-LBL-03 | |
| URS-INSP-01 | FS-INSP-01 | |
| URS-INSP-02 | FS-INSP-02 | |
| URS-PERF-01 | FS-PERF-01 | |
| URS-PERF-02 | FS-PERF-02 | |
| URS-PERF-03 | FS-PERF-03 | |
| URS-AV-01 | FS-AV-01 | |
| URS-AV-02 | FS-AV-02 | |
| URS-BAK-01 | FS-BAK-01 | |
| URS-BAK-02 | FS-BAK-02 | |
| URS-BAK-03 | FS-BAK-03 | |
| URS-SEC-01 | FS-SEC-01 | |
| URS-SEC-02 | FS-SEC-02 | |
| URS-SEC-03 | FS-SEC-03 | |
| URS-SEC-04 | FS-SEC-04 | |
| URS-SEC-05 | FS-SEC-05 | |
| URS-TRN-01 | FS-TRN-01 | |
| URS-TRN-02 | FS-TRN-02 | |
| URS-PR-01 | FS-PR-01 | Governance — also captured in periodic-review record |
| URS-PR-02 | FS-PR-02 | Governance — signed by Mfg IT Lead + Head of QA per Part 11 § 11.50 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-HEL-01 | FS-XINT-HEL-01 |
| URS-XINT-HEL-02 | FS-XINT-HEL-02 |
| URS-XINT-LMS-01 | FS-XINT-LMS-01 |

## 12. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Tasklet defect causing incorrect IPC evaluation | Medium | Critical | URS-DEV-01..05 + regression suite |
| R-02 | SAP integration drift (schema change unannounced) | Low | High | URS-INT-SAP-01 + automated contract tests |
| R-03 | LIMS results gate bypassed | Low | Critical | URS-INT-LIMS-02 + role-based override audit |
| R-04 | Mobile client compromise | Low | High | URS-PLAT-03, URS-SEC-03 |
| R-05 | Audit-trail tampering by privileged user | Very Low | Critical | URS-AUD-02 + DBA dual-control |
| R-06 | Sterilizing-grade filtration data not captured | Low | Critical | URS-INT-SCADA-01, URS-EBR-04 |
| R-07 | MBR-recipe-amendment without proper approval | Low | Critical | URS-MBR-04 + SoD + URS-PART11-04 |
| R-08 | Weighing tare drift causing dispense error | Medium | High | URS-WGH-04 |
| R-09 | Label-printer failure causing un-labelled material | Low | High | URS-WGH-05 step-closure block |
| R-10 | ERP-MES desync (master data drift) | Medium | High | URS-INT-SAP-03 daily reconciliation |
| R-11 | Operator runs step without valid training | Low | Critical | URS-PER-01 + URS-INT-LMS-01 |
| R-12 | Equipment use beyond qualification expiry | Low | Critical | URS-EQ-02 |
| R-13 | Cleaning-cycle gate bypassed | Low | Critical | URS-EQ-03 |
| R-14 | Deviation lifecycle desync between PAS-X + eQMS | Medium | Medium | URS-INT-EQMS-01 |
| R-15 | QP certification on a batch with open Critical deviation | Very Low | Critical | URS-REL-03 gate |
| R-16 | Serialised-material mis-link (FMD / DSCSA) | Low | High | URS-MAT-04 |
| R-17 | Loss of PTP causing audit-trail timestamp anomaly | Low | High | URS-DI-03 |
| R-18 | Workflow-engine version drift between sites | Low | Medium | URS-WF-05 versioned BPMN |
| R-19 | Yield-variance calculation error | Low | Medium | URS-YLD-01..02 + OQ verification |
| R-20 | Mass-data load (campaign-start material reservation) overwhelms DB | Low | Medium | URS-PERF-01..03 |

These risks are formally evaluated in `VBM-RA-MES-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
