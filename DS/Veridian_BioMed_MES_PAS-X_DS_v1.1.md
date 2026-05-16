---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15 (Cat 4 / Tier T4)"
seed_corpus_basis:
  - "VBM-FS-MES-001 v1.2 (parent FS)"
  - "VBM-URS-MES-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd Edition) Category 4 — Configuration Specification conventions"
  - "ISPE GAMP Good Practice Guide MES (2018)"
  - "21 CFR Part 11; 21 CFR Part 211 §§ .68, .100, .180, .184, .186, .188, .192"
  - "EU GMP Annex 11; Annex 1 (2022 revised); Annex 15; Annex 16"
  - "Directive 2001/83/EC Art. 51 (QP)"
  - "ICH Q9(R1); ICH Q10; ICH Q12"
  - "ANSI/ISA-88; ANSI/ISA-95; BPMN 2.0"
parent_fs:
  document_number: VBM-FS-MES-001
  version: "1.2"
  file: "../../../FS_FDS/_generated/final/Veridian_BioMed_MES_PAS-X_FS_v1.3.md"
parent_urs:
  document_number: VBM-URS-MES-001
  version: "1.2"
  file: "../../../URS/_generated/final/Veridian_BioMed_MES_PAS-X_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Configuration Specification (CS)

## Manufacturing Execution System — Werum / Körber PAS-X v3.2

**Document Number:** VBM-DS-MES-001
**Version:** 1.1
**Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** VBM-FS-MES-001 v1.2
**Parent URS:** VBM-URS-MES-001 v1.2 *(informational, transitive)*
**Site:** Veridian BioMed Inc., Sterile Fill-Finish Plant 2, Devens, Massachusetts, USA *(fictional)*
**System Owner:** Manufacturing IT Lead
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (Werum/Körber PAS-X v3.2), with site tasklets assessed as Category 5 sub-components (mini-SDS in § 8)
**Project Mode:** Configuration project on commercial software product **Werum / Körber PAS-X v3.2** (GAMP 5 Category 4) with embedded Cat-5 site tasklets under hybrid governance.
**Regulatory Scope:** 21 CFR Part 11; 21 CFR Part 211 §§ .68, .100, .180, .184, .186, .188, .192; 21 CFR Part 210; EU GMP Annex 11; EU GMP Annex 1 (2022 revised); EU GMP Annex 15; EU GMP Annex 16; Directive 2001/83/EC Art. 51 (QP); ICH Q9(R1); ICH Q10; ICH Q12; ANSI/ISA-88; ANSI/ISA-95; BPMN 2.0; PIC/S PI 041.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect — MES) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Manufacturing IT Lead) | _____________ | _____________ | _____ |
| Reviewer (QA — CSV) | _____________ | _____________ | _____ |
| Reviewer (SAP Integration Lead) | _____________ | _____________ | _____ |
| Reviewer (LIMS Integration Lead) | _____________ | _____________ | _____ |
| Reviewer (Vault / eQMS Lead) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Approver (System Owner — Manufacturing IT Lead) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |
| Approver (Qualified Person) | _____________ | _____________ | _____ |

## Design Control

- **Document Number:** VBM-DS-MES-001
- **Version:** 1.1
- **Effective Date:** 2026-05-15 *(synthetic)*
- **Parent FS:** VBM-FS-MES-001 v1.2
- **Parent URS:** VBM-URS-MES-001 v1.2 *(informational)*
- **Site:** Veridian BioMed Inc., Plant 2, Devens, MA, USA
- **System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product (PAS-X v3.2) with embedded Cat-5 site tasklets
- **Project Mode:** Hybrid Cat 4 + Cat 5 — § 4–§ 7 CS rules; § 8 mini-SDS for tasklets
- **Regulatory Scope:** as above

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T4 from parent URS+FS pair. DS covers 134/134 FS-IDs from VBM-FS-MES-001 v1.2 (including all M-XSYS / M-XINT cross-system rows). No FS-IDs flagged vendor-internal — PAS-X configuration surface fully site-designable; vendor-internal core code (Werum/Körber SDLC) is out of DS scope per § 2B.1. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from VBM-FS-MES-001 and VBM-URS-MES-001. DS-specific terms:

| Term | Definition |
|---|---|
| MBR | Master Batch Record (PAS-X authored artefact) |
| EBR | Electronic Batch Record (instantiated from MBR for a SAP order) |
| Tasklet | PAS-X Java scripting unit; site-authored Cat-5 sub-component |
| MFC | Material Flow Controller (PAS-X internal service for material lifecycle) |
| PI/PO | SAP Process Integration / Process Orchestration |
| Vault URN | Veeva Vault QualityDocs Uniform Resource Name |
| Helios | downstream audit-stream consumer (Kafka) |
| BPMN | Business Process Model and Notation 2.0 |

---

## 1. Purpose

This DS specifies the technical design that satisfies the FS `VBM-FS-MES-001` v1.2 for the Veridian Plant-2 PAS-X v3.2 deployment. It records the PAS-X CI inventory, MBR / EBR / Order / Material / Equipment / Personnel / Yield / Sampling / Genealogy / Workflow / Release / Reporting / Multi-site workflow + business-rule design, the role-permission matrix, the per-interface integration design (SAP S/4HANA via PI/PO, LabWare LIMS 8, Ignition 8.3 OPC UA, Veeva Vault, MasterControl eQMS, Phlox/Maximo CMMS, LMS, AD/PKI, label printers, connected balances, Kafka Helios egress, LMS-competence handover), and a mini-SDS for site tasklets. Controlling input to IQ / OQ / PQ / RTM `VBM-RTM-MES-001`.

## 2. Scope

**In scope.** Configuration of PAS-X v3.2 App Servers (3 active + 1 standby behind HAProxy), Oracle 19c Data Guard physical-standby, MBR Designer (Windows 11 Enterprise), Web Client, PAS-X Mobile (iPad), workflow engine (BPMN 2.0), reporting engine, all integrations (SAP/LIMS/SCADA/Vault/eQMS/CMMS/LMS/AD), label-template management, inspection-readiness, and site tasklets.

**Out of scope.** Werum/Körber core code (vendor SDLC); SAP / LIMS / Vault / eQMS / CMMS / LMS / SCADA internal validation (each under its own CSV record); physical fill-finish equipment.

## 3. Architectural Overview

### 3.1 Topology (text)

```
                ┌─────────────────────────────────────────────────────────┐
                │  AD / Site PKI (NWT.local) + PTP IEEE 1588 grandmaster    │
                │  + Veeva Vault QualityDocs + LMS                          │
                └────────────────────┬────────────────────────────────────┘
                                     │
       ┌─────────────────────────────▼──────────────────────────────┐
       │       PAS-X v3.2 Application Tier (Plant 2, Devens)          │
       │  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌────────┐ │
       │  │ app-srv-01 │  │ app-srv-02 │  │ app-srv-03 │  │ app-srv │ │
       │  │   (ACT)    │  │   (ACT)    │  │   (ACT)    │  │ -04 SB  │ │
       │  └─────┬──────┘  └─────┬──────┘  └─────┬──────┘  └────┬───┘ │
       │        └───────────────┴───────────────┴──────────────┘     │
       │                     HAProxy (health-check /health 5 s)       │
       │  ┌──────────────────────────────────────────────────────┐   │
       │  │  Oracle 19c (Primary) ──── Data Guard async ──► (DR) │   │
       │  └──────────────────────────────────────────────────────┘   │
       │  ┌──────────────────────────────────────────────────────┐   │
       │  │  Workflow Engine (BPMN 2.0) + Reporting (Superset)    │   │
       │  └──────────────────────────────────────────────────────┘   │
       │  ┌──────────────────────────────────────────────────────┐   │
       │  │  Tasklets (Cat 5 site-Java) — see § 8                 │   │
       │  └──────────────────────────────────────────────────────┘   │
       └───┬──────┬──────┬──────┬──────┬──────┬──────┬───────┬──────┘
           │      │      │      │      │      │      │       │
           ▼      ▼      ▼      ▼      ▼      ▼      ▼       ▼
        SAP    LIMS   Ignition Veeva   Master- Phlox /   LMS    Connected
        S/4    LabW   8.3 SCADA Vault   Control Maximo           Balances
        PI/PO  REST + (OPC UA  REST     eQMS    CMMS              + ZPL
        iDoc   SOAP   mTLS)     URN     REST    REST              Printers
                                cache                              + Helios
                                                                   Kafka
```

### 3.2 Cluster Design Choices

- **App Servers:** 3 ACT + 1 SB behind HAProxy with `/health` health-check every 5 s; failed nodes removed automatically
- **Oracle 19c:** Data Guard physical-standby (async); managed switchover via `DGMGRL`
- **DR:** secondary DC; RPO target ≤ 15 min; RTO ≤ 4 h
- **Fault domains:** ≥ 2 physical (rack + PDU diversity) recorded in CMDB
- **Mobile:** iPad MDM (Jamf Pro); remote-wipe SLO ≤ 15 min
- **PTP:** IEEE 1588 grandmaster; clock-skew gate at every signature event (>5 s rejects)

---

## 4. Configuration Specification

Per § 2B.4 — one row per CI. Vendor source-code internals (PAS-X core) are NOT redrawn. Site tasklets appear here as configuration anchors and are detailed in § 8 (mini-SDS).

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| DS-MES-01 | PAS-X > Cluster > Active App Servers | `3` | Custom | FS-PLAT-01 — 3 active behind HAProxy | FS-PLAT-01 | OQ `VBM-OQ-PLAT-CLUSTER-01` |
| DS-MES-02 | PAS-X > Cluster > Standby App Servers | `1` (`app-srv-04`) auto-promoted on failure | Custom | FS-PLAT-01 — 1 standby auto-promote | FS-PLAT-01 | OQ `VBM-OQ-PLAT-FAILOVER-01` |
| DS-MES-03 | Oracle 19c > Data Guard Mode | physical-standby async; managed switchover via DGMGRL | Custom | FS-PLAT-02 — Data Guard async | FS-PLAT-02 | OQ `OQ-DR-RPO-01` |
| DS-MES-04 | DR RPO Target | ≤ 15 min | Custom | FS-PLAT-02 | FS-PLAT-02 | OQ `OQ-DR-RPO-01` |
| DS-MES-05 | DR RTO Target | ≤ 4 h | Custom | FS-PLAT-02 — RTO | FS-PLAT-02 | PQ `PQ-DR-01` |
| DS-MES-06 | iPad MDM Profile | Jamf Pro; remote-wipe ≤ 15 min; non-allow-listed apps blocked | Custom | FS-PLAT-03 — MDM | FS-PLAT-03 / FS-SEC-03 | OQ `VBM-OQ-MDM-01` |
| DS-MES-07 | Patch Management SLA | impact assessment ≤ 14 d; deployment ≤ 30 d for criticals | Custom | FS-PLAT-04 — patch SLA | FS-PLAT-04 | (governance) |
| DS-MES-08 | HAProxy Health-Check | HTTP `/health` every `5 s`; failed-node auto-remove + alert | Custom | FS-PLAT-05 — health-check cadence | FS-PLAT-05 | OQ `OQ-LB-HEALTH-01` |
| DS-MES-09 | App-Server Distribution | ≥ 2 fault domains (rack + PDU diversity); CMDB-recorded | Custom | FS-PLAT-06 — fault domains | FS-PLAT-06 | IQ `VBM-IQ-CMDB-01` |
| DS-MES-10 | MBR Lifecycle States | `DRAFT / REVIEW / APPROVED / EFFECTIVE / OBSOLETE`; server-side validated; out-of-state → HTTP 409 + audit | Custom | FS-MBR-01 — MBR state machine | FS-MBR-01 | OQ `VBM-OQ-MBR-STATES-01` |
| DS-MES-11 | Production Dispatch Gate | rejects non-EFFECTIVE; rejection includes actual state | Custom | FS-MBR-02 — dispatch gate | FS-MBR-02 | OQ `VBM-OQ-MBR-DISPATCH-01` |
| DS-MES-12 | Transition Signature UI | captures meaning enum + AD-group → role mapping enforced server-side | Custom | FS-MBR-03 — transition signature | FS-MBR-03 | OQ `VBM-OQ-MBR-TRANS-SIG-01` |
| DS-MES-13 | SoD Cross-Role Check | signer-id ≠ Author-id at sign time; collision → HTTP 403 + audit | Custom | FS-MBR-04 — SoD check | FS-MBR-04, FS-PART11-04 | OQ `VBM-OQ-SOD-01` |
| DS-MES-14 | Data-Layer Immutability | EFFECTIVE MBR: DB constraint + service guard; change creates revision N+1 in DRAFT linked to prior | Custom | FS-MBR-05 — immutability | FS-MBR-05 | OQ `VBM-OQ-MBR-IMMUT-01` |
| DS-MES-15 | Vault URN Resolution at APPROVAL | resolves every referenced URN; unresolved blocks approval | Custom | FS-MBR-06 — Vault check | FS-MBR-06 | OQ `VBM-OQ-VAULT-RESOLVE-01` |
| DS-MES-16 | MBR Designer ISA-88 Enforcement | procedure / unit-procedure / operation / phase hierarchy; phases linked to equipment-class via equipment-master | Custom | FS-MBR-07 — ISA-88 hierarchy | FS-MBR-07 | OQ `OQ-MBR-S88-HIER-01` |
| DS-MES-17 | Per-Step `criticality` Enum | `Critical / Major / Minor` | Custom | FS-MBR-08 — criticality | FS-MBR-08 | OQ `OQ-MBR-PER-STEP-APPROVAL-01` |
| DS-MES-18 | MBR Effectivity Fields | `effective_from`, `effective_until` validated at dispatch | Custom | FS-MBR-09 — effectivity | FS-MBR-09 | OQ `OQ-MBR-EFFECTIVITY-01` |
| DS-MES-19 | MBR Diff Renderer | per-step + per-field JSON diff; UI presents old/new + reason | Custom | FS-MBR-10 — diff renderer | FS-MBR-10 | OQ `VBM-OQ-MBR-DIFF-01` |
| DS-MES-20 | SAP Order Inbound > Validators | server-side field validation; missing required → reject + log | Custom | FS-ORD-01 — inbound validation | FS-ORD-01 | OQ `VBM-OQ-ORD-VAL-01` |
| DS-MES-21 | Idempotency Key (SAP order) | `(order_number, order_version)`; duplicates → `SAPORDER_DUPLICATE` | Custom | FS-ORD-02 — idempotency | FS-ORD-02 | OQ `VBM-OQ-ORD-IDEM-01` |
| DS-MES-22 | SAP Acknowledgement SLA | P95 ≤ 5 min; measured by message-broker timestamps | Custom | FS-ORD-03 — ack SLA | FS-ORD-03 | OQ `VBM-OQ-ORD-ACK-01` |
| DS-MES-23 | Reschedule Authorisation | Production Supervisor role; logged transition | Custom | FS-ORD-04 — reschedule role | FS-ORD-04 | OQ `VBM-OQ-RESCHED-01` |
| DS-MES-24 | Order Cancellation | pre-EBR allowed; post-EBR requires QA approval signature | Custom | FS-ORD-05 — cancellation | FS-ORD-05 | OQ `VBM-OQ-ORD-CANCEL-01` |
| DS-MES-25 | EBR Creation Transactionality | single transactional operation; failure → SAP error envelope | Custom | FS-EBR-01 — transactional creation | FS-EBR-01 | OQ `VBM-OQ-EBR-TXN-01` |
| DS-MES-26 | Step-Ordering Enforcement | UI + API blocks out-of-sequence; override requires "supervisor override" signature with reason | Custom | FS-EBR-02 — step ordering | FS-EBR-02 | OQ `VBM-OQ-STEP-ORDER-01` |
| DS-MES-27 | Critical-Step Verifier Constraint | verifier user-id ≠ operator user-id; widget mandatory | Custom | FS-EBR-03 / FS-MBR-08 — second person | FS-EBR-03 | OQ `VBM-OQ-CRIT-VER-01` |
| DS-MES-28 | OPC UA EBR Capture | subscribed Ignition tags written read-only with `(value, ts, source-tag, op-id)` | Custom | FS-EBR-04 — OPC UA capture | FS-EBR-04 | OQ `VBM-OQ-OPCUA-CAPT-01` |
| DS-MES-29 | IPC Step Evaluator | server-side after operator entry / LIMS arrival; FAIL → block + auto-deviation | Custom | FS-EBR-05 — IPC | FS-EBR-05 | OQ `VBM-OQ-IPC-01` |
| DS-MES-30 | Dispense Tolerance Validation | UCL / LCL / target + lot-genealogy (status=RELEASED, expiry not lapsed) | Custom | FS-EBR-06 — dispense | FS-EBR-06 | OQ `VBM-OQ-DISP-TOL-01` |
| DS-MES-31 | Review-by-Exception View | filters EBR steps with deviations / manual entries / overrides + configurable filters | Custom | FS-EBR-07 — RBE | FS-EBR-07 | OQ `VBM-OQ-RBE-01` |
| DS-MES-32 | Long-Step Flag | per-step `expected_duration` tracked; > threshold → `flag_long_step=true` | Custom | FS-EBR-08 — long-step flag | FS-EBR-08 | OQ `VBM-OQ-LONG-STEP-01` |
| DS-MES-33 | Step-Retry Endpoint | preserves prior attempts immutably; creates attempt N+1 with reason + signature | Custom | FS-EBR-09 — retry | FS-EBR-09 | OQ `OQ-EBR-STEP-RETRY-01` |
| DS-MES-34 | Material-Master Schema (replicated from SAP) | `lot_id, material_code, supplier, receipt_date, expiry_date, qa_status, parent_lot` | Custom | FS-MAT-01 — material schema | FS-MAT-01 | OQ `VBM-OQ-MAT-SCHEMA-01` |
| DS-MES-35 | MFC Dispense Gate | non-RELEASED or expired → `LOT_NOT_RELEASED` / `LOT_EXPIRED` | Custom | FS-MAT-02 — lot-status gate | FS-MAT-02 | OQ `VBM-OQ-MAT-GATE-01` |
| DS-MES-36 | Genealogy Linker Table | `(ebr_step_id, lot_id, consumed_mass, ts)`; forward/backward query API | Custom | FS-MAT-03 — genealogy | FS-MAT-03 | OQ `VBM-OQ-GEN-LINK-01` |
| DS-MES-37 | Serialised-Unit Table | links serial → parent_lot; FMD / DSCSA export per `RPT-SERIAL-001` | Custom | FS-MAT-04 — serialised | FS-MAT-04 | OQ `VBM-OQ-SERIAL-01` |
| DS-MES-38 | Material Reservation Engine | soft + hard reservations; hard-reserve locked at MFC dispense | Custom | FS-MAT-05 — reservation | FS-MAT-05 | OQ `VBM-OQ-RES-01` |
| DS-MES-39 | SAP Material-Status Webhook | near real-time update of `lot.qa_status`; in-progress consumption → blocking deviation | Custom | FS-MAT-06 — webhook | FS-MAT-06 | OQ `OQ-MAT-STATUS-SYNC-01` |
| DS-MES-40 | Material-Reconciliation Runner | consumed-vs-theoretical per lot per campaign; PDF + CSV export | Custom | FS-MAT-07 — reconciliation | FS-MAT-07 | OQ `VBM-OQ-RECON-01` |
| DS-MES-41 | Connected-Balance Drivers | Mettler-Toledo + Sartorius via OPC UA + vendor drivers; `balance_id` in equipment-master | Custom | FS-WGH-01 — balance drivers | FS-WGH-01 | IQ `VBM-IQ-BAL-01` |
| DS-MES-42 | Dispense Workflow Capture | mass + ts + operator + balance_id auto-recorded read-only | Custom | FS-WGH-02 — dispense capture | FS-WGH-02 | OQ `VBM-OQ-WGH-CAPT-01` |
| DS-MES-43 | Over-Dispense Disposition | OOT → Quality Reviewer disposition workflow | Custom | FS-WGH-03 — disposition | FS-WGH-03 | OQ `VBM-OQ-OVR-DISP-01` |
| DS-MES-44 | Pre-Dispense Tare Check | tare-drift > threshold blocks | Custom | FS-WGH-04 — tare drift | FS-WGH-04 | OQ `OQ-WGH-TARE-DRIFT-01` |
| DS-MES-45 | Label Generator | ZPL barcode + human-readable; printer-status polled; printer-fault blocks step closure | Custom | FS-WGH-05 — label generator | FS-WGH-05 | OQ `OQ-WGH-LABEL-01` |
| DS-MES-46 | Per-Balance Calibration Gate | OUT_OF_CAL blocks dispense | Custom | FS-WGH-06 — cal gate | FS-WGH-06 | OQ `VBM-OQ-BAL-CAL-01` |
| DS-MES-47 | Equipment-Master Schema | `equipment_id, class, location, status, last_cleaning_cycle_ref, last_qualification_ref, qualification_expiry, current_user` | Custom | FS-EQ-01 — equipment schema | FS-EQ-01 | OQ `VBM-OQ-EQ-SCHEMA-01` |
| DS-MES-48 | EBR Step-Start Gate | queries `equipment_status=READY` + `qualification_expiry > now()` | Custom | FS-EQ-02 — READY gate | FS-EQ-02 | OQ `OQ-EQ-READY-GATE-01` |
| DS-MES-49 | Cleaning Gate | `last_cleaning_cycle_ref` + `dirty_hold_max_h` evaluated at step start | Custom | FS-EQ-03 — cleaning gate | FS-EQ-03 | OQ `OQ-EQ-CLEAN-GATE-01` |
| DS-MES-50 | CMMS Adapter Polling | every 60 s; in-window equipment → MAINTENANCE | Custom | FS-EQ-04 — CMMS poll | FS-EQ-04 | OQ `OQ-INT-CMMS-01` |
| DS-MES-51 | Equipment-Cycle Linker | autoclave / lyo / coater cycle IDs via inbound webhooks → EBR step | Custom | FS-EQ-05 — cycle-link | FS-EQ-05 | OQ `OQ-EQ-CYCLE-LINK-01` |
| DS-MES-52 | Return-to-Service Workflow | test-execution evidence + Quality Reviewer signature required | Custom | FS-EQ-06 — RTS | FS-EQ-06 | OQ `VBM-OQ-RTS-01` |
| DS-MES-53 | LMS REST Query at Login + Step | expired training → HTTP 403 + reason | Custom | FS-PER-01 — LMS gate | FS-PER-01 | OQ `OQ-PER-TRAIN-GATE-01` |
| DS-MES-54 | AD-Group → PAS-X Role Map | managed under CR; Manufacturing IT Lead + Head of QA dual-sign on changes | Custom | FS-PER-02 — role map | FS-PER-02 | OQ `OQ-PER-AD-MAP-01` |
| DS-MES-55 | Operator Qualification Registry | per-operator competency list; step.required_qualifications ⊆ operator.qualifications | Custom | FS-PER-03 — qualification gate | FS-PER-03 | OQ `OQ-PER-QUAL-GATE-01` |
| DS-MES-56 | Shift-Handover Capture UI | entries linked to subsequent EBR-step records | Custom | FS-PER-04 — handover | FS-PER-04 | OQ `VBM-OQ-HANDOVER-01` |
| DS-MES-57 | Personnel-on-Batch Report | enumerates all signers + verifiers + executors per batch | Custom | FS-PER-05 — personnel report | FS-PER-05 | OQ `VBM-OQ-PERSONNEL-RPT-01` |
| DS-MES-58 | Per-Step Recipe Lifecycle | mirrors MBR lifecycle; transition signatures required | Custom | FS-REC-01 — sub-procedure lifecycle | FS-REC-01 | OQ `VBM-OQ-REC-SUB-01` |
| DS-MES-59 | Per-Step Approver Signature | meaning = `per-step approval` | Custom | FS-REC-02 — per-step approver | FS-REC-02 | OQ `VBM-OQ-REC-APPR-01` |
| DS-MES-60 | Sub-Step Effectivity Window | outside-window rejected | Custom | FS-REC-03 — effectivity | FS-REC-03 | OQ `VBM-OQ-REC-EFFECT-01` |
| DS-MES-61 | Per-Batch Yield Engine | actual / theoretical with recipe acceptance band; out-of-band → deviation | Custom | FS-YLD-01 — yield engine | FS-YLD-01 | OQ `OQ-YLD-CALC-01` |
| DS-MES-62 | Variance Formula | `input_mass − output_mass − accounted_loss`; |variance| > threshold → deviation | Custom | FS-YLD-02 — variance | FS-YLD-02 | OQ `OQ-YLD-VARIANCE-01` |
| DS-MES-63 | Deviation Classification Engine | Critical / Major / Minor per recipe rules | Custom | FS-YLD-03 — classification | FS-YLD-03 | OQ `OQ-YLD-DEV-CLASS-01` |
| DS-MES-64 | Deviation eQMS Link | MasterControl deviation ID → source-of-truth post-disposition | Custom | FS-YLD-04 — eQMS link | FS-YLD-04 | OQ `OQ-YLD-EQMS-LINK-01` |
| DS-MES-65 | APR Feed Aggregator | yield + deviation + OOS + OOT trends per material / line | Custom | FS-YLD-05 — APR feed | FS-YLD-05 | OQ `OQ-RPT-APR-FEED-01` |
| DS-MES-66 | LIMS Sample Creation Endpoint | REST: method ID + expected timepoint + EBR linkage; failure → integration-exception deviation | Custom | FS-SMP-01 / FS-INT-LIMS-01 — sample creation | FS-SMP-01, FS-INT-LIMS-01 | OQ `VBM-OQ-LIMS-CREATE-01` |
| DS-MES-67 | Chain-of-Custody UI | captures pull-time + operator + container labels + lab-arrival-time | Custom | FS-SMP-02 — chain of custody | FS-SMP-02 | OQ `VBM-OQ-COC-01` |
| DS-MES-68 | LIMS Result Poll Service | every 60 s; release-pending steps gated on `result_status=APPROVED` | Custom | FS-SMP-03 / FS-INT-LIMS-02 — LIMS poll | FS-SMP-03, FS-INT-LIMS-02 | OQ `OQ-INT-LIMS-RESULT-01` |
| DS-MES-69 | OOS-Result Hook | auto-creates `OOS-PROC-001` deviation + blocks release | Custom | FS-SMP-04 — OOS hook | FS-SMP-04 | OQ `OQ-OOS-BLOCK-01` |
| DS-MES-70 | Gantt Schedule View | rendered from order + EBR + equipment + personnel data | Custom | FS-SCH-01 — Gantt view | FS-SCH-01 | OQ `OQ-SCH-GANTT-01` |
| DS-MES-71 | Reschedule API | validates equipment / personnel / material availability before commit | Custom | FS-SCH-02 — reschedule validation | FS-SCH-02 | OQ `VBM-OQ-RESCHED-API-01` |
| DS-MES-72 | Schedule-Change SAP Push | POSTs events to SAP for ERP-side visibility | Custom | FS-SCH-03 — SAP push | FS-SCH-03 | OQ `VBM-OQ-SCHED-SAP-01` |
| DS-MES-73 | Deviation-EBR Closure Guard | step-closure validator blocks if any open deviation | Custom | FS-WF-01 — deviation guard | FS-WF-01 | OQ `VBM-OQ-DEV-GUARD-01` |
| DS-MES-74 | Critical Notification → QA Distribution | immediate; QA disposition required before batch closure | Custom | FS-WF-02 — critical notification | FS-WF-02 | OQ `VBM-OQ-WF-NOTIF-01` |
| DS-MES-75 | MasterControl Deviation Push | REST adapter; eQMS deviation-ID stored as source-of-truth | Custom | FS-WF-03 / FS-INT-EQMS-01 — eQMS push | FS-WF-03, FS-INT-EQMS-01 | OQ `OQ-INT-EQMS-01` |
| DS-MES-76 | Disposition Signature at Closure | Quality Approver `release` meaning; state → RELEASED/REJECTED/QUARANTINED | Custom | FS-WF-04 — disposition | FS-WF-04 | OQ `VBM-OQ-DISP-01` |
| DS-MES-77 | BPMN 2.0 Workflow Engine | versioned deployments; CR required | Custom | FS-WF-05 — BPMN engine | FS-WF-05 | OQ `OQ-WF-BPMN-VER-01` |
| DS-MES-78 | Workflow-Step Transition SLO | P95 ≤ 1 s under nominal load | Custom | FS-WF-06 — workflow latency | FS-WF-06 | OQ `VBM-OQ-WF-LATENCY-01` |
| DS-MES-79 | Genealogy Forward Index | 24-mo lookback indexed; P95 ≤ 30 s | Custom | FS-GEN-01 / FS-PERF-03 — forward trace | FS-GEN-01, FS-PERF-03 | PQ `PQ-GEN-FORWARD-01` |
| DS-MES-80 | Genealogy Backward Index | likewise | Custom | FS-GEN-02 — backward trace | FS-GEN-02 | PQ `PQ-GEN-BACKWARD-01` |
| DS-MES-81 | Genealogy Export | machine-readable JSON; signed bundle | Custom | FS-GEN-03 — export | FS-GEN-03 | OQ `VBM-OQ-GEN-EXPORT-01` |
| DS-MES-82 | SAP PI/PO Adapter (iDoc + SOAP) | inbound order receipt | Custom | FS-INT-SAP-01 — SAP inbound | FS-INT-SAP-01 | OQ `VBM-OQ-SAP-IN-01` |
| DS-MES-83 | Yield-and-Genealogy iDoc Outbound | P95 ≤ 5 min | Custom | FS-INT-SAP-02 — SAP outbound | FS-INT-SAP-02 | OQ `VBM-OQ-SAP-OUT-01` |
| DS-MES-84 | SAP Master / BoM Replication | daily reconciliation runner; drift → alarm + optional lock-down | Custom | FS-INT-SAP-03 — master data | FS-INT-SAP-03 | OQ `OQ-INT-SAP-MASTER-01` |
| DS-MES-85 | SAP Webhook (material status) | near real-time; in-progress consumption block | Custom | FS-INT-SAP-04 — material webhook | FS-INT-SAP-04 | OQ `OQ-INT-SAP-STATUS-01` |
| DS-MES-86 | OPC UA mTLS to Ignition | end-to-end signing of `(timestamp, value, source-tag, cert-fingerprint)` in EBR | Custom | FS-INT-SCADA-01 — OPC UA capture | FS-INT-SCADA-01 | OQ `VBM-OQ-OPCUA-01` |
| DS-MES-87 | Ignition Alarm Subscription | route batch-relevant alarms to operator's current EBR step ≤ 2 s | Custom | FS-INT-SCADA-02 — alarm route | FS-INT-SCADA-02 | OQ `VBM-OQ-SCADA-ALARM-01` |
| DS-MES-88 | Equipment-Cycle Webhook Receiver | accepts autoclave / lyo / coater cycle-completion payloads | Custom | FS-INT-SCADA-03 — cycle webhook | FS-INT-SCADA-03 | OQ `OQ-INT-EQUIP-CYCLE-01` |
| DS-MES-89 | Vault URN Cache | 24-h TTL; miss-with-cache → warning audit; miss-without-cache → block | Custom | FS-INT-VAULT-01 — Vault cache | FS-INT-VAULT-01 | OQ `VBM-OQ-VAULT-CACHE-01` |
| DS-MES-90 | LMS REST Cache | 5-min cache | Custom | FS-INT-LMS-01 — LMS cache | FS-INT-LMS-01 | OQ `OQ-INT-LMS-01` |
| DS-MES-91 | AD Federation + Vault Service Accounts | short-lived secrets via HashiCorp Vault | Custom | FS-INT-AD-01 / FS-SEC-01 | FS-INT-AD-01, FS-SEC-01 | OQ `VBM-OQ-AD-VAULT-01` |
| DS-MES-92 | Audit Event Schema | `user, action, entity-id, old, new, reason, ts_ptp, client-ip, signature-event-id` | Custom | FS-AUD-01 — audit schema | FS-AUD-01 | OQ `VBM-OQ-AUDIT-SCHEMA-01` |
| DS-MES-93 | Audit Table Append-Only | revoked DELETE/UPDATE; DBA dual control; API read+insert only | Custom | FS-AUD-02 — append-only | FS-AUD-02 | OQ `VBM-OQ-AUDIT-APPEND-01` |
| DS-MES-94 | Audit Review UI | filters + PDF/CSV signed export | Custom | FS-AUD-03 — review UI | FS-AUD-03 | OQ `VBM-OQ-AUDIT-REV-01` |
| DS-MES-95 | EBR-Closure Audit Review Checkbox | mandatory QA review; quarterly report runner | Custom | FS-AUD-04 — review checkbox | FS-AUD-04 | OQ `VBM-OQ-AUDIT-RVW-CHECK-01` |
| DS-MES-96 | Archival Storage | `STG-ARCHIVE-LYFCYC-001` cold-store; ≥ 25 y | Custom | FS-AUD-05 — retention | FS-AUD-05 | (governance) |
| DS-MES-97 | Signature Render | printed-name + ts (PTP) + meaning into audit + PDF | Custom | FS-PART11-01 — § 11.50 manifestation | FS-PART11-01 | OQ `VBM-OQ-SIG-RENDER-01` |
| DS-MES-98 | AD Identity Binding | account deletion via documented deactivation; ID reuse blocked | Custom | FS-PART11-02 — identity binding | FS-PART11-02 | OQ `VBM-OQ-AD-IDENT-01` |
| DS-MES-99 | PKI-Signed Signature Payload | `(record-id, record-state-hash, signer-id, meaning, ts)`; verify-on-every-read; tampered → "INVALID — INVESTIGATE" | Custom | FS-PART11-03 — § 11.70 | FS-PART11-03 | OQ `VBM-OQ-SIG-PKI-01` |
| DS-MES-100 | SoD Policy Engine | evaluates signer's prior actions on same record at signing | Custom | FS-PART11-04 — SoD | FS-PART11-04 | OQ `VBM-OQ-SOD-API-01` |
| DS-MES-101 | Re-Auth at Every Signature | password + AD MFA; cached creds disabled | Custom | FS-PART11-05 — § 11.200 | FS-PART11-05 | OQ `VBM-OQ-REAUTH-01` |
| DS-MES-102 | Annex 11 Design-Control Map | §4 → validation lifecycle; §7 → Oracle storage + backup; §9 → audit; §10 → CR; §12 → SEC; §17 → printout with audit | Custom | FS-PART11-06 — Annex 11 map | FS-PART11-06 | (governance) |
| DS-MES-103 | AD Password Policy `SEC-AD-POLICY-001` | per central policy doc | Custom | FS-PART11-07 — § 11.300 | FS-PART11-07 | (governance) |
| DS-MES-104 | Audit + Export Coverage | per § 11.10(b)/(c)/(e) | Custom | FS-PART11-08 — Part 11 coverage | FS-PART11-08 | OQ `VBM-OQ-PART11-COV-01` |
| DS-MES-105 | QA-Review Gate at Batch Closure | all steps carry Quality Reviewer "review-complete" signature | Custom | FS-REL-01 — QA gate | FS-REL-01 | OQ `OQ-REL-QA-GATE-01` |
| DS-MES-106 | QP-Certification Terminal Node | meaning = "Annex 16 certification"; Annex 16 register reference | Custom | FS-REL-02 — QP certification | FS-REL-02 | OQ `OQ-REL-QP-SIG-01` |
| DS-MES-107 | QP-Sign Open-Deviation Gate | Critical / Major open block; Minor requires QP-noted disposition text | Custom | FS-REL-03 — open-dev gate | FS-REL-03 | OQ `OQ-REL-OPEN-DEV-BLOCK-01` |
| DS-MES-108 | QP Certification Record Table | `(batch_id, qp_id, ts, statement, ebr_hash)` archived with EBR | Custom | FS-REL-04 — QP record | FS-REL-04 | OQ `OQ-REL-QP-RECORD-01` |
| DS-MES-109 | Confirmation of Compliance PDF Template | per Annex 16 Annex II; auto-generated on QP-sign; signed | Custom | FS-REL-05 — CofC PDF | FS-REL-05 | OQ `VBM-OQ-COFC-01` |
| DS-MES-110 | QP-Readiness Dashboard | per-batch QA-review status + open-item count + certification-ready flag | Custom | FS-REL-06 — QP dashboard | FS-REL-06 | OQ `VBM-OQ-QP-DASH-01` |
| DS-MES-111 | Data Integrity > Attribution | AD-authenticated user-id on all writes; no shared accounts | Custom | FS-DI-01 — attribution | FS-DI-01 | OQ `VBM-OQ-DI-ATTRIB-01` |
| DS-MES-112 | EBR Export Formats | PDF (with audit) + PAS-X XML archive; OQ-validated | Custom | FS-DI-02 — export | FS-DI-02 | OQ `OQ-EXPORT-01` |
| DS-MES-113 | NTP + PTP Sync | clock-skew check at every signature event (>5 s rejects) | Custom | FS-DI-03 — time sync | FS-DI-03 | OQ `VBM-OQ-PTP-01` |
| DS-MES-114 | Immutability + Derivation Lineage | originals immutable; derivations reference source value | Custom | FS-DI-04 — immutability + lineage | FS-DI-04 | OQ `VBM-OQ-DI-LIN-01` |
| DS-MES-115 | Deterministic Calculation Engine | yield + variance + IPC math | Custom | FS-DI-05 — determinism | FS-DI-05 | OQ `OQ-CALC-01` |
| DS-MES-116 | Retention + Retrieval SLA | ≥ 25 y; ≤ 4 BH retrieval via inspection runbook | Custom | FS-DI-06 — retention | FS-DI-06 | OQ `VBM-OQ-RETR-01` |
| DS-MES-117 | Tasklet SDLC `SDLC-MES-TASKLET-001` | code review + ≥ 90% coverage on safety + Snyk SCA + SonarQube gate | Custom | FS-DEV-01 — tasklet SDLC | FS-DEV-01 | (CI) |
| DS-MES-118 | Tasklet Deployment | signed CR package; promotion blocked on regression failure | Custom | FS-DEV-02 — deployment | FS-DEV-02 | (CI) |
| DS-MES-119 | Source Repo GitLab Enterprise | branch protection + signed commits (GPG) | Custom | FS-DEV-03 — repo controls | FS-DEV-03 | (CI) |
| DS-MES-120 | Per-Tasklet FS Artefact `VBM-FS-TASKLET-NNN` | dedicated FS + Cat-5 RA + RTM row | Custom | FS-DEV-04 — per-tasklet FS | FS-DEV-04 | (governance) |
| DS-MES-121 | Coverage Gate CI | PR blocked on coverage < 90% on safety-relevant logic | Custom | FS-DEV-05 — coverage gate | FS-DEV-05 | (CI) |
| DS-MES-122 | OEE Computation Engine | Availability × Performance × Quality per line per shift per day | Custom | FS-RPT-01 — OEE | FS-RPT-01 | OQ `OQ-RPT-OEE-01` |
| DS-MES-123 | Superset Dashboards | yield trend + deviation-rate trend + CR velocity; role-gated | Custom | FS-RPT-02 — dashboards | FS-RPT-02 | OQ `VBM-OQ-SUPERSET-01` |
| DS-MES-124 | APR Feed Aggregator Export | per product on schedule | Custom | FS-RPT-03 — APR | FS-RPT-03 | OQ `OQ-RPT-APR-FEED-01` |
| DS-MES-125 | Quarterly Audit-Review Evidence Report Runner | scheduled job | Custom | FS-RPT-04 — quarterly evidence | FS-RPT-04 | OQ `VBM-OQ-AUDIT-Q-01` |
| DS-MES-126 | Report-Runner Sign | PKI sign of bundle with runner-user-id + params + ts | Custom | FS-RPT-05 — report signing | FS-RPT-05 | OQ `VBM-OQ-RPT-SIG-01` |
| DS-MES-127 | Per-Site Effectivity Fields | on MBR / recipe / tasklet; deployment-target field; cross-site share enabled but isolated | Custom | FS-MSITE-01 — per-site fields | FS-MSITE-01 | OQ `VBM-OQ-MSITE-01` |
| DS-MES-128 | Cross-Site Recipe-Transfer Workflow | preserves genealogy + tech-transfer doc links | Custom | FS-MSITE-02 — recipe transfer | FS-MSITE-02 | OQ `VBM-OQ-MSITE-XFR-01` |
| DS-MES-129 | Label-Template Registry | states `DRAFT/REVIEW/APPROVED/EFFECTIVE/OBSOLETE`; printer fetches EFFECTIVE by id + locale | Custom | FS-LBL-01 — label registry | FS-LBL-01 | OQ `VBM-OQ-LBL-REG-01` |
| DS-MES-130 | Template-Change Workflow | legibility-test evidence + barcode-scan-back + QA + Mfg IT signatures | Custom | FS-LBL-02 — template change | FS-LBL-02 | OQ `VBM-OQ-LBL-CR-01` |
| DS-MES-131 | Post-Print Scan-Back | attached scanner; mismatch → alert + step-closure block | Custom | FS-LBL-03 — scan-back | FS-LBL-03 | OQ `VBM-OQ-LBL-SCAN-01` |
| DS-MES-132 | Inspection-Mode Auditor Role | read-only window-bound access; cached snapshot | Custom | FS-INSP-01 — inspection role | FS-INSP-01 | OQ `VBM-OQ-INSP-ROLE-01` |
| DS-MES-133 | Inspection-Bundle Exporter | EBR + audit + genealogy + QP cert; signed; SLA ≤ 4 h | Custom | FS-INSP-02 — inspection bundle | FS-INSP-02 | OQ `VBM-OQ-INSP-BUNDLE-01` |
| DS-MES-134 | Performance Sizing | 250 concurrent operators (20% headroom); P95 navigation ≤ 1.5 s | Custom | FS-PERF-01 — sizing | FS-PERF-01 | PQ `PQ-PERF-NAV-01` |
| DS-MES-135 | MBR Designer Save SLO | P95 ≤ 5 s for 200-step MBR | Custom | FS-PERF-02 — designer SLO | FS-PERF-02 | OQ `OQ-MBR-PERF-01` |
| DS-MES-136 | Availability Target | ≥ 99.5%; planned maintenance excluded | Custom | FS-AV-01 — availability | FS-AV-01 | (governance) |
| DS-MES-137 | Redis Session Replication | shared Redis; transparent App-Server failover | Custom | FS-AV-02 — session repl | FS-AV-02 | OQ `VBM-OQ-REDIS-01` |
| DS-MES-138 | Oracle Backup + Redo | nightly + continuous archived redo logs to S3 (immutable / 30-d Object-Lock); PITR | Custom | FS-BAK-01 — backup | FS-BAK-01 | OQ `OQ-BAK-PITR-01` |
| DS-MES-139 | Restore-Test Cadence | quarterly; DBA + QA witness | Custom | FS-BAK-02 — restore test | FS-BAK-02 | PR-01 |
| DS-MES-140 | DR Failover Exercise | annual full DR-site failover | Custom | FS-BAK-03 — DR | FS-BAK-03 | PQ `PQ-DR-FULL-01` |
| DS-MES-141 | TLS Policy | TLS 1.2+; ciphers per NIST SP 800-52 Rev 2 | Custom | FS-SEC-02 — TLS | FS-SEC-02 | OQ `OQ-SEC-TLS-01` |
| DS-MES-142 | Tenable Nessus Weekly Scan | criticals 30-d remediation per site SOP | Custom | FS-SEC-04 — vuln scan | FS-SEC-04 | (governance) |
| DS-MES-143 | Bastion-Host Session Recording | privileged sessions recorded; retention 1 y for QA review | Custom | FS-SEC-05 — session recording | FS-SEC-05 | OQ `VBM-OQ-BASTION-01` |
| DS-MES-144 | LMS-Tied Production Access | AD-group membership tied to LMS course-completion attribute | Custom | FS-TRN-01 — LMS gate | FS-TRN-01 | OQ `VBM-OQ-TRN-01` |
| DS-MES-145 | Annual Refresher Reminder | triggered 60 d prior to expiry; access revoked on expiry | Custom | FS-TRN-02 — refresher | FS-TRN-02 | (governance) |
| DS-MES-146 | Periodic-Review Run-Book | auto-collects config baselines + audit-review evidence + dev/CR summary + backup/restore + integration health + training + deviation trends + security posture | Custom | FS-PR-01 — periodic review | FS-PR-01 | PR-01 |
| DS-MES-147 | Periodic-Review Signing | Mfg IT Lead + Head of QA per § 11.50 | Custom | FS-PR-02 — PR signing | FS-PR-02 | OQ `VBM-OQ-PR-SIG-01` |
| DS-MES-148 | AD Conditional Access `OT-MES Conditional Access` | MFA at engineering / line workstation; operator stations named-location + role-bound smart cards; SIEM → Splunk `gxp-authn`; CyberArk PAM break-glass | Custom | FS-XSYS-AD-01 | FS-XSYS-AD-01 | OQ `VBM-OQ-CONDACC-01` |
| DS-MES-149 | Veeam Backup | App-aware Oracle RMAN + file-level recipe / order config; tier T1; RPO ≤ 4 h; RTO ≤ 4 BH; S3 Compliance Mode + LTO-9 monthly | Custom | FS-XSYS-BAK-01 | FS-XSYS-BAK-01 | OQ `VBM-OQ-VEEAM-01` |
| DS-MES-150 | Helios Kafka Audit Egress | topic `helios.ingest.veridian.pasx.v1`; schema-pinned envelope; idempotency key `{source_system, event_id}`; Prometheus `helios_publish_lag_seconds` > 600 s alert | Custom | FS-XINT-HEL-01 — Helios | FS-XINT-HEL-01 | OQ `VBM-OQ-HELIOS-PUB-01` |
| DS-MES-151 | Helios Parity Reconciliation Job | ≥ 15-y local retention; periodic count parity; > 0.01% mismatch over 24 h → MasterControl deviation | Custom | FS-XINT-HEL-02 — Helios parity | FS-XINT-HEL-02 | OQ `VBM-OQ-HELIOS-PARITY-01` |
| DS-MES-152 | LMS-Competence Adapter `<sys>-LMS-CLIENT-1.x` | mTLS + Entra workload identity; cache TTL 12-24 h; `current=false` blocks gated action + records `lms_lapse_user` | Custom | FS-XINT-LMS-01 — LMS-competence | FS-XINT-LMS-01 | OQ `VBM-OQ-LMS-COMP-01` |

---

## 5. Workflow + Business-Rule Design

### 5.1 MBR-Lifecycle Workflow (PAS-X core lifecycle service)

| Transition | Pre-condition | Required signatures | Resulting state |
|---|---|---|---|
| DRAFT → REVIEW | Author submits | Author `author submit` | REVIEW |
| REVIEW → APPROVED | All Reviewers signed | Reviewer `review` (n ≥ 2: Validation + Manufacturing IT + QA-CSV); Vault URN resolution clean | APPROVED |
| APPROVED → EFFECTIVE | within effectivity window | Manufacturing Lead + Head of QA `approve` dual-sign | EFFECTIVE |
| EFFECTIVE → OBSOLETE | superseded | Manufacturing Lead `retirement` | OBSOLETE |
| any → any (bypass) | not permitted | n/a — blocked | rejected with HTTP 409 |

SoD: signer-id ≠ Author-id (DS-MES-13). MBR Diff (DS-MES-19) renders changes at REVIEW gate.

### 5.2 EBR-Execution Workflow

```
SAP order → EBR creation (transactional, DS-MES-25) → step-ordering enforcement →
critical-step verifier widget (DS-MES-27) →
process-parameter capture (OPC UA, DS-MES-28) →
IPC evaluator (DS-MES-29) → dispense (tolerance, DS-MES-30) →
sample creation (DS-MES-66) → LIMS poll (DS-MES-68) →
yield calc (DS-MES-61) → variance (DS-MES-62) →
deviation classification (DS-MES-63) → QA review (DS-MES-105) →
QP certification (DS-MES-106) → batch close
```

### 5.3 Disposition / Release Workflow (BPMN 2.0)

- **Critical deviation:** auto-notification to QA distribution (DS-MES-74); QP-sign blocked (DS-MES-107)
- **Major deviation:** disposition required; QP-sign blocked
- **Minor deviation:** disposition required; QP-sign requires noted disposition text
- **QP-Annex 16 certification:** terminal node (DS-MES-106); auto-generates CofC PDF (DS-MES-109)

### 5.4 Equipment Step-Start Gate Rules

- Equipment status must be READY (DS-MES-48)
- qualification_expiry > now() (DS-MES-48)
- Cleaning gate: `last_cleaning_cycle_ref` + `dirty_hold_max_h` (DS-MES-49)
- CMMS poll: in-window → MAINTENANCE (DS-MES-50)
- Failure returns HTTP 409 + reason; auto-deviation

### 5.5 Step-Retry Rule (FS-EBR-09 / DS-MES-33)

Step-retry preserves prior attempt(s) immutably; creates attempt N+1 with retry reason ≥ 10 chars + signature. Attempt-N+1 supersedes for compute purposes; prior attempts remain in audit + RBE view.

### 5.6 Material-Reservation Rules (FS-MAT-05 / DS-MES-38)

- **Soft reservation:** decreases available_qty but not on_hand
- **Hard reservation:** locks lot at MFC dispense API; cannot be released without signed override

### 5.7 SoD + Cross-Role Business Rules

| Combination | Blocked? | Rationale |
|---|---|---|
| Author == Reviewer of same MBR | Yes (HTTP 403) | FS-MBR-04 / DS-MES-13 |
| Operator == Verifier of same critical step | Yes | FS-EBR-03 / DS-MES-27 |
| QP == Author of MBR | No (allowed) | regulatory practice |
| Reviewer == Approver of same recipe | Yes | DS-MES-100 SoD policy |

### 5.8 OOS / Open-Deviation Release Gate (FS-REL-03 / DS-MES-107)

QP-sign endpoint queries open-deviation list:
- Critical or Major open → BLOCK with reason
- Minor open → require QP-noted disposition text in `qp_disposition_text` field
- None open → proceed

### 5.9 Inspection-Mode Workflow (FS-INSP-* / DS-MES-132/133)

Auditor role gets window-bound read-only access to a cached snapshot (does not contend with live production). Inspection-bundle exporter (DS-MES-133) produces EBR + audit + genealogy + QP cert signed bundle within 4 h SLA.

---

## 6. Role-Permission Matrix Design

| AD Group → PAS-X Role | View | Author MBR | Approve MBR | Operate EBR | Verify critical | Dispatch | Disposition | QP-sign | Audit Export | Admin |
|---|---|---|---|---|---|---|---|---|---|---|
| `MES-Operator` | Y | — | — | Y | — | — | — | — | — | — |
| `MES-Verifier` | Y | — | — | — | Y | — | — | — | — | — |
| `MES-Supervisor` | Y | — | — | review | — | Y | — | — | — | — |
| `MES-MBR-Author` | Y | Y | — | — | — | — | — | — | — | — |
| `MES-MBR-Reviewer` | Y | review | — | — | — | — | — | — | — | — |
| `MES-MBR-Approver` | Y | — | Y (dual w/ QA) | — | — | — | — | — | — | — |
| `MES-Quality-Reviewer` | Y | — | — | — | — | — | review | — | Y | — |
| `MES-Quality-Approver` | Y | — | approve (QA pair) | — | — | — | Y | — | Y | — |
| `MES-Qualified-Person` | Y | — | — | — | — | — | — | Y (Annex 16) | Y | — |
| `MES-Auditor` | Y (RO) | — | — | — | — | — | — | — | Y | — |
| `MES-Mfg-IT-Lead` | Y | — | — | — | — | — | — | — | — | role-map admin |
| Break-glass `MES-DBA` (vaulted) | — | — | — | — | — | — | — | — | — | DB admin only |

Server-side AD-group → PAS-X-role mapping under CR (DS-MES-54). FS-IDs traced: FS-INT-AD-01, FS-PART11-04 (SoD), FS-MBR-04, FS-EBR-03, FS-REL-02.

---

## 7. Integration Design

### 7.1 IF-SAP-01..04 (SAP S/4HANA via PI/PO)

- **Endpoint family:** SAP iDoc + SOAP via PI/PO; idempotent on `(order_number, order_version)`
- **Schemas:** ORDERS05/ORDRSP iDoc for order receipt; LOIPRO for yield/genealogy outbound; MATMAS / BOMMAT for material master; webhook for material-status change
- **Retry:** PI/PO native + DLQ
- **Error handling:** duplicate → `SAPORDER_DUPLICATE`; field-validation failure → reject + log
- **Audit:** `sap_order_receive`, `sap_yield_post`, `sap_material_master_sync`, `sap_material_status_webhook`
- **FS-IDs:** FS-INT-SAP-01..04

### 7.2 IF-LIMS-01/02 (LabWare LIMS 8)

- **Endpoint:** REST + SOAP — sample creation outbound; result poll + webhook inbound
- **Cadence:** 60-s poll on open samples; release-pending gated on `result_status=APPROVED`
- **OOS hook:** auto-creates `OOS-PROC-001` deviation + blocks release
- **FS-IDs:** FS-INT-LIMS-01/02, FS-SMP-*

### 7.3 IF-SCADA-01..03 (Ignition 8.3)

- **Protocol:** OPC UA mTLS — tag values + alarms + equipment-cycle webhook
- **End-to-end sign:** `(ts, value, source-tag, cert-fingerprint)` preserved in EBR
- **Alarm SLA:** alarm → operator EBR step ≤ 2 s
- **FS-IDs:** FS-INT-SCADA-01..03, FS-EBR-04

### 7.4 IF-VAULT-01 (Veeva Vault QualityDocs)

- **Endpoint:** REST URN resolution
- **Cache:** 24-h TTL; miss-with-cache → warning audit + continue with cached; miss-without-cache → block
- **FS-IDs:** FS-INT-VAULT-01

### 7.5 IF-EQMS-01 (MasterControl)

- **Endpoint:** REST bidirectional — deviation push + status webhook back
- **Source of truth:** post-disposition, MasterControl deviation-ID is canonical
- **FS-IDs:** FS-INT-EQMS-01, FS-WF-03

### 7.6 IF-CMMS-01 (Phlox / Maximo)

- **Endpoint:** REST; polled every 60 s for maintenance windows
- **FS-IDs:** FS-INT-CMMS-01

### 7.7 IF-LMS-01 (LMS)

- **Endpoint:** REST; queried at login + step-assignment; 5-min cache (DS-MES-90)
- **FS-IDs:** FS-INT-LMS-01

### 7.8 IF-AD-01 (AD / PKI)

- **Protocol:** LDAPS + Kerberos; service accounts via Vault short-lived secrets
- **FS-IDs:** FS-INT-AD-01, FS-SEC-01

### 7.9 IF-PTP-01 (PTP master)

- **Protocol:** IEEE 1588; clock-skew check at every signature event (>5 s rejects)
- **FS-IDs:** FS-DI-03

### 7.10 IF-BAL-01 (Connected balances)

- **Protocol:** OPC UA + vendor RS232/Ethernet (Mettler-Toledo + Sartorius)
- **FS-IDs:** FS-WGH-01

### 7.11 IF-PRT-01 (Label printers — Zebra ZT411)

- **Protocol:** ZPL / CUPS; printer-status polled; fault blocks step
- **FS-IDs:** FS-WGH-05, FS-LBL-*

### 7.12 IF-HEL-01 (Helios Kafka egress)

- **Topic:** `helios.ingest.veridian.pasx.v1`
- **Envelope:** schema-registry-pinned `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`
- **Delivery:** at-least-once; idempotency key `{source_system, event_id}`
- **Backpressure:** Prometheus `helios_publish_lag_seconds`; alert > 600 s
- **Parity:** local-store retention ≥ 15 y; periodic reconciliation; > 0.01% mismatch → MasterControl deviation
- **FS-IDs:** FS-XINT-HEL-01/02

### 7.13 Integration Risk Register

| Interface | Risk | Mitigation |
|---|---|---|
| IF-SAP | schema change unannounced | automated contract tests in CI |
| IF-LIMS | result-gate bypass | API-level enforcement + audit |
| IF-SCADA | mTLS cert expiry | cert-manager rotation 365 d |
| IF-VAULT | URN cache stale | 24-h TTL + miss-warning audit |
| IF-EQMS | desync of deviation lifecycle | webhook reconciliation runner |
| IF-CMMS | poll miss | 60-s cadence + alarm on poll-failure > 3 consecutive |
| IF-LMS | competence lapse undetected | LMS-competence adapter (DS-MES-152) with reconciliation |
| IF-HEL | Kafka broker down | DLQ + reprocess; > 600-s lag alert |

---

## 8. Site-Deployed Components — Mini-SDS for Tasklets (Cat 5)

The site Java tasklets are the embedded custom-code substrate that escalates this Cat 4 MES to a hybrid Cat 4 + Cat 5. Each tasklet has its own `VBM-FS-TASKLET-NNN` artefact; this section gives the cross-tasklet architecture, decomposition, and shared rules.

### 8.1 Software Architecture (logical view)

```
   ┌────────────────────────────────────────────────────────────┐
   │  Site Tasklets (Java 17, ~25k LOC cumulative across ~40 tasks)  │
   │  ┌──────────────────┐  ┌──────────────────┐                     │
   │  │  ipc/             │  │  yield/            │                  │
   │  │  - IpcEvaluator   │  │  - YieldCalculator │                  │
   │  │  - SamplePlanner  │  │  - VarianceEngine  │                  │
   │  └──────────────────┘  └──────────────────┘                     │
   │  ┌──────────────────┐  ┌──────────────────┐                     │
   │  │  dispense/        │  │  release/          │                  │
   │  │  - ToleranceCheck │  │  - QaReviewGate    │                  │
   │  │  - TareDriftCheck │  │  - QpCertify       │                  │
   │  └──────────────────┘  └──────────────────┘                     │
   │  ┌──────────────────┐  ┌──────────────────┐                     │
   │  │  integration/     │  │  audit/            │                  │
   │  │  - HeliosPublisher│  │  - SignaturePki    │                  │
   │  │  - LmsCompetence  │  │  - InspectionExp   │                  │
   │  └──────────────────┘  └──────────────────┘                     │
   └────────────────────────────────────────────────────────────┘
```

Stack: Java 17 LTS on PAS-X tasklet runtime; Maven build; SonarQube + Snyk SCA in CI.

### 8.2 Module Decomposition

| Module ID | Tasklet name | Responsibility | Interface | Dependencies | GxP class |
|---|---|---|---|---|---|
| MS-01 | `ipc.IpcEvaluator` | server-side IPC evaluation | `evaluate(stepId, inputs)` | LIMS adapter | R1 |
| MS-02 | `ipc.SamplePlanner` | sample-plan generation per recipe | `plan(ebrId)` | recipe DB | R2 |
| MS-03 | `dispense.ToleranceCheck` | dispense tolerance enforcement | `check(dispenseId)` | balance driver; lot table | R1 |
| MS-04 | `dispense.TareDriftCheck` | pre-dispense tare-drift block | `check(balanceId)` | balance driver | R2 |
| MS-05 | `yield.YieldCalculator` | per-batch yield engine | `calc(ebrId)` | EBR + recipe | R1 |
| MS-06 | `yield.VarianceEngine` | variance formula evaluator | `variance(ebrId)` | EBR | R1 |
| MS-07 | `release.QaReviewGate` | QA review-complete gate | `gate(ebrId)` | EBR + signatures | R1 |
| MS-08 | `release.QpCertify` | QP-cert + Annex 16 CofC | `certify(batchId)` | Open-deviation query | R1 |
| MS-09 | `integration.HeliosPublisher` | Kafka egress to Helios | `publish(event)` | Kafka + schema registry | R2 |
| MS-10 | `integration.LmsCompetence` | LMS-competence adapter | `check(userId, curriculum)` | LMS endpoint | R1 |
| MS-11 | `audit.SignaturePki` | PKI-signed signature payload | `sign(record)` | site PKI | R1 |
| MS-12 | `audit.InspectionExp` | inspection-bundle exporter | `export(window)` | EBR + audit + genealogy | R2 |

### 8.3 Data Model (DB schema highlights)

| Table | Key columns | Constraints | Retention |
|---|---|---|---|
| `mbr` | `mbr_id, version, state, sha256, vault_urns (JSONB), steps (JSONB)` | trigger blocks UPDATE/DELETE on EFFECTIVE | indefinite |
| `ebr` | `ebr_id, mbr_id, mbr_version, sap_order, state, steps (JSONB), deviations[]` | one per dispatch | 25 y |
| `ebr_step` | `step_id, ebr_id, idx, type, criticality, captured_data (JSONB), signatures[], deviation_id, attempt` | retry attempts versioned | 25 y |
| `order` | `order_id, order_version, material, qty, schedule, mbr_ref, state` | from SAP | 25 y |
| `material_lot` | `lot_id, material, supplier, receipt, expiry, qa_status, parent_lot` | replicated SAP | 25 y |
| `material_reservation` | `res_id, lot_id, order_id, type(soft/hard), qty` | hard locks at MFC | indefinite |
| `dispense` | `dispense_id, step_id, lot_id, mass, balance_id, label_id, ts, operator_id, verifier_id` | NOT NULL on operator + verifier | 25 y |
| `equipment` | `equipment_id, class, location, status, last_clean_ref, last_qual_ref, qual_expiry` | NOT NULL on status | indefinite |
| `equipment_cycle` | `ec_id, equipment_id, cycle_type, cycle_ref, started_at, ended_at` | linked from cycle webhook | 25 y |
| `personnel` | `user_id, ad_dn, qualifications[], training_state` | mirrored AD + LMS | indefinite |
| `deviation` | `dev_id, ebr_id, step_id, classification, state, eqms_link, raised_by, disposition` | classification enum | 25 y |
| `sample` | `sample_id, ebr_step_id, method_id, lims_sample_id, status` | LIMS linkage | 25 y |
| `yield` | `ebr_id, theoretical, actual, variance, in_band` | NOT NULL on ebr_id | 25 y |
| `signature` | `sig_id, record_id, record_state_hash, signer_id, meaning, timestamp, pki_signature` | cryptographically bound | 25 y |
| `qp_certification` | `cert_id, batch_id, qp_id, ts, ebr_hash, statement` | Annex 16 | 25 y |
| `audit_event` | per FS-AUD-01 | append-only via role GRANT | 25 y |
| `workflow_def` | `wf_id, version, bpmn_xml, state` | versioned BPMN | indefinite |

Data classification: GxP (most tables); PII (personnel); no PHI.

### 8.4 Algorithm + Calculation Design

| Algorithm | Inputs | Output | Procedure | Numerical-precision note | Reference |
|---|---|---|---|---|---|
| Per-batch yield | input_mass, output_mass, accounted_loss | yield_pct, in_band | `yield = actual / theoretical`; band per recipe | float64 with `Decimal` for mass; deterministic | site |
| Variance | input + output + loss | variance, exceeds_threshold | `var = input − output − loss`; threshold per recipe | as above | site |
| Genealogy forward | lot_id, lookback | EBR steps that consumed lot | indexed join on `genealogy_link` | textual; P95 ≤ 30 s | site |
| Genealogy backward | ebr_step_id | lots consumed | indexed reverse join | P95 ≤ 30 s | site |
| OEE | uptime, performance ratio, quality ratio | OEE % | A × P × Q per line per shift | float64 | ISA-95 |
| Tare-drift | pre-tare, current-tare | drift_pct, blocked | `|current − pre|/pre`; recipe threshold | Decimal | site |
| Annex 16 CofC text | batch metadata + QP record | CofC PDF | template + sign | textual + PKI signature | EU GMP Annex 16 |
| Helios envelope | event | published bytes | schema-pinned JSON serialise; key `{source_system, event_id}` | UTF-8 | Confluent Schema Registry |

### 8.5 Interface + API Design

| Endpoint | Method | AuthN | Request | Response | Idempotency | Audit |
|---|---|---|---|---|---|---|
| `/api/mbr/{id}` | GET | Kerberos | `id` | MBR JSON | safe | `mbr_fetch` |
| `/api/mbr/transition` | POST | Kerberos + signature | `{recordHash, signerId, meaning}` | new state | by recordHash | `mbr_transition` |
| `/api/ebr/{id}/step/{idx}/sign` | POST | Kerberos + MFA | signature payload | sig_id | by recordHash + meaning | `step_sign` |
| `/api/dispense/{id}` | POST | Kerberos | `{lot_id, mass, balance_id, label_id}` | dispense_id | by step_id | `dispense_create` |
| `/api/release/qp-certify/{batchId}` | POST | Kerberos QP + MFA | `{statement, ebr_hash}` | cert_id | by batch_id | `qp_certify` |
| `/api/helios/publish` | (internal) | mTLS | event | Kafka offset | by `{source_system, event_id}` | `helios_publish` |
| `/api/inspection/bundle` | POST | Kerberos Auditor | window | bundle URI | by window | `inspection_export` |

Rate limit: 500 req/s per IP (App-Server tier); error JSON with `correlation_id`.

### 8.6 Security Design

- **AuthN:** federated AD; service accounts via HashiCorp Vault (1-h TTL)
- **AuthZ:** AD-group → PAS-X-role mapping (DS-MES-54); SoD policy engine (DS-MES-100)
- **Secrets:** Vault @ `vault.veridian.local`; mTLS client certs auto-rotate 365 d
- **Transport:** TLS 1.2+; ciphers per NIST SP 800-52 Rev 2; mTLS for SAP / Vault / SCADA / eQMS / CMMS
- **Audit-event taxonomy:** comprehensive list per DS-MES-92; minimum 32 distinct action types
- **Session recording:** bastion-host privileged sessions (DS-MES-143); 1-y retention

### 8.7 Deployment Architecture

- **Packaging:** Tasklet JAR signed via GPG; CR-bound deployment package
- **Topology:** App-Servers run tasklet runtime; tasklets hot-deployed via PAS-X tasklet manager
- **Observability:** Prometheus exporters + Grafana `VBM-GR-MES-RUNTIME`; logs to Splunk `gxp-mes`; ELK for application logs
- **DR:** annual full DR-site failover (DS-MES-140); App-Server quorum + Oracle Data Guard

### 8.8 Module Specification Table (pointer)

| Module ID | Source location | Unit-test ref |
|---|---|---|
| MS-01..MS-12 | `gitlab.veridian.local/mes/tasklets/{ipc,dispense,yield,release,integration,audit}/src/main/java/...` | `<repo>/src/test/java/test_<module>.java` (JaCoCo ≥ 90% on safety/*) |

Full Module Specifications: `VBM-MS-TASKLET-NNN` (downstream).

---

## 9. References

### US
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .68, .100, .180, .184, .186, .188, .192
- 21 CFR Part 210
- FDA CSA (final, February 2026)

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11
- EU GMP Annex 1 (2022 revised)
- EU GMP Annex 15
- EU GMP Annex 16
- Directive 2001/83/EC Art. 51 (QP)

### DACH
- AMWHV
- BSI IT-Grundschutz baseline

### International
- ISPE GAMP 5 (2nd ed., 2022)
- ISPE GAMP GPG *MES* (2018)
- ISPE GAMP GPG *Records and Data Integrity*
- ICH Q9(R1); ICH Q10; ICH Q12
- ANSI/ISA-88 Part 1 + Part 2; ANSI/ISA-95 Part 1 + Part 2
- BPMN 2.0
- PIC/S PI 041
- ISO/IEC 27001:2022; ISO/IEC 27002
- NIST SP 800-52 Rev 2 (TLS); NIST SP 800-218 SSDF
- OWASP ASVS

### Vendor
- Werum / Körber — *PAS-X v3.2 Configuration Reference*
- Werum / Körber — *PAS-X Tasklet Development Guide*
- Werum / Körber — *PAS-X Mobile Configuration Guide*
- Oracle — *Oracle 19c Data Guard Concepts and Administration*
- SAP — *PI/PO Integration Guide*
- LabWare — *LIMS 8 Configuration Reference*
- Inductive Automation — *Ignition 8.3 OPC UA Reference*
- Veeva — *Vault QualityDocs API Reference*
- MasterControl — *eQMS REST API Reference*
- Mettler-Toledo / Sartorius — *Connected Balance Reference*
- Zebra — *ZT411 ZPL Reference*

### Site
- `VBM-URS-MES-001` v1.2 (informational)
- `VBM-FS-MES-001` v1.2 (parent)
- `SDLC-MES-TASKLET-001` (Cat-5 tasklet SDLC)
- `VBM-FS-TASKLET-NNN` (per-tasklet FS, downstream)
- `VBM-RTM-MES-001` (RTM)
- `STG-ARCHIVE-LYFCYC-001` (cold-storage retention)
- `SEC-AD-POLICY-001` (AD password policy)

---

## 10. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) traced |
|---|---|
| DS-MES-01 | FS-PLAT-01 |
| DS-MES-02 | FS-PLAT-01 |
| DS-MES-03 | FS-PLAT-02 |
| DS-MES-04 | FS-PLAT-02 |
| DS-MES-05 | FS-PLAT-02 |
| DS-MES-06 | FS-PLAT-03 / FS-SEC-03 |
| DS-MES-07 | FS-PLAT-04 |
| DS-MES-08 | FS-PLAT-05 |
| DS-MES-09 | FS-PLAT-06 |
| DS-MES-10 | FS-MBR-01 |
| DS-MES-11 | FS-MBR-02 |
| DS-MES-12 | FS-MBR-03 |
| DS-MES-13 | FS-MBR-04 / FS-PART11-04 |
| DS-MES-14 | FS-MBR-05 |
| DS-MES-15 | FS-MBR-06 |
| DS-MES-16 | FS-MBR-07 |
| DS-MES-17 | FS-MBR-08 |
| DS-MES-18 | FS-MBR-09 |
| DS-MES-19 | FS-MBR-10 |
| DS-MES-20 | FS-ORD-01 |
| DS-MES-21 | FS-ORD-02 |
| DS-MES-22 | FS-ORD-03 |
| DS-MES-23 | FS-ORD-04 |
| DS-MES-24 | FS-ORD-05 |
| DS-MES-25 | FS-EBR-01 |
| DS-MES-26 | FS-EBR-02 |
| DS-MES-27 | FS-EBR-03 |
| DS-MES-28 | FS-EBR-04 |
| DS-MES-29 | FS-EBR-05 |
| DS-MES-30 | FS-EBR-06 |
| DS-MES-31 | FS-EBR-07 |
| DS-MES-32 | FS-EBR-08 |
| DS-MES-33 | FS-EBR-09 |
| DS-MES-34 | FS-MAT-01 |
| DS-MES-35 | FS-MAT-02 |
| DS-MES-36 | FS-MAT-03 |
| DS-MES-37 | FS-MAT-04 |
| DS-MES-38 | FS-MAT-05 |
| DS-MES-39 | FS-MAT-06 |
| DS-MES-40 | FS-MAT-07 |
| DS-MES-41 | FS-WGH-01 |
| DS-MES-42 | FS-WGH-02 |
| DS-MES-43 | FS-WGH-03 |
| DS-MES-44 | FS-WGH-04 |
| DS-MES-45 | FS-WGH-05 |
| DS-MES-46 | FS-WGH-06 |
| DS-MES-47 | FS-EQ-01 |
| DS-MES-48 | FS-EQ-02 |
| DS-MES-49 | FS-EQ-03 |
| DS-MES-50 | FS-EQ-04 |
| DS-MES-51 | FS-EQ-05 |
| DS-MES-52 | FS-EQ-06 |
| DS-MES-53 | FS-PER-01 |
| DS-MES-54 | FS-PER-02 |
| DS-MES-55 | FS-PER-03 |
| DS-MES-56 | FS-PER-04 |
| DS-MES-57 | FS-PER-05 |
| DS-MES-58 | FS-REC-01 |
| DS-MES-59 | FS-REC-02 |
| DS-MES-60 | FS-REC-03 |
| DS-MES-61 | FS-YLD-01 |
| DS-MES-62 | FS-YLD-02 |
| DS-MES-63 | FS-YLD-03 |
| DS-MES-64 | FS-YLD-04 |
| DS-MES-65 | FS-YLD-05 |
| DS-MES-66 | FS-SMP-01 / FS-INT-LIMS-01 |
| DS-MES-67 | FS-SMP-02 |
| DS-MES-68 | FS-SMP-03 / FS-INT-LIMS-02 |
| DS-MES-69 | FS-SMP-04 |
| DS-MES-70 | FS-SCH-01 |
| DS-MES-71 | FS-SCH-02 |
| DS-MES-72 | FS-SCH-03 |
| DS-MES-73 | FS-WF-01 |
| DS-MES-74 | FS-WF-02 |
| DS-MES-75 | FS-WF-03 / FS-INT-EQMS-01 |
| DS-MES-76 | FS-WF-04 |
| DS-MES-77 | FS-WF-05 |
| DS-MES-78 | FS-WF-06 |
| DS-MES-79 | FS-GEN-01 / FS-PERF-03 |
| DS-MES-80 | FS-GEN-02 |
| DS-MES-81 | FS-GEN-03 |
| DS-MES-82 | FS-INT-SAP-01 |
| DS-MES-83 | FS-INT-SAP-02 |
| DS-MES-84 | FS-INT-SAP-03 |
| DS-MES-85 | FS-INT-SAP-04 |
| DS-MES-86 | FS-INT-SCADA-01 |
| DS-MES-87 | FS-INT-SCADA-02 |
| DS-MES-88 | FS-INT-SCADA-03 |
| DS-MES-89 | FS-INT-VAULT-01 |
| DS-MES-90 | FS-INT-LMS-01 |
| DS-MES-91 | FS-INT-AD-01 / FS-SEC-01 |
| DS-MES-92 | FS-AUD-01 |
| DS-MES-93 | FS-AUD-02 |
| DS-MES-94 | FS-AUD-03 |
| DS-MES-95 | FS-AUD-04 |
| DS-MES-96 | FS-AUD-05 |
| DS-MES-97 | FS-PART11-01 |
| DS-MES-98 | FS-PART11-02 |
| DS-MES-99 | FS-PART11-03 |
| DS-MES-100 | FS-PART11-04 |
| DS-MES-101 | FS-PART11-05 |
| DS-MES-102 | FS-PART11-06 |
| DS-MES-103 | FS-PART11-07 |
| DS-MES-104 | FS-PART11-08 |
| DS-MES-105 | FS-REL-01 |
| DS-MES-106 | FS-REL-02 |
| DS-MES-107 | FS-REL-03 |
| DS-MES-108 | FS-REL-04 |
| DS-MES-109 | FS-REL-05 |
| DS-MES-110 | FS-REL-06 |
| DS-MES-111 | FS-DI-01 |
| DS-MES-112 | FS-DI-02 |
| DS-MES-113 | FS-DI-03 |
| DS-MES-114 | FS-DI-04 |
| DS-MES-115 | FS-DI-05 |
| DS-MES-116 | FS-DI-06 |
| DS-MES-117 | FS-DEV-01 |
| DS-MES-118 | FS-DEV-02 |
| DS-MES-119 | FS-DEV-03 |
| DS-MES-120 | FS-DEV-04 |
| DS-MES-121 | FS-DEV-05 |
| DS-MES-122 | FS-RPT-01 |
| DS-MES-123 | FS-RPT-02 |
| DS-MES-124 | FS-RPT-03 |
| DS-MES-125 | FS-RPT-04 |
| DS-MES-126 | FS-RPT-05 |
| DS-MES-127 | FS-MSITE-01 |
| DS-MES-128 | FS-MSITE-02 |
| DS-MES-129 | FS-LBL-01 |
| DS-MES-130 | FS-LBL-02 |
| DS-MES-131 | FS-LBL-03 |
| DS-MES-132 | FS-INSP-01 |
| DS-MES-133 | FS-INSP-02 |
| DS-MES-134 | FS-PERF-01 |
| DS-MES-135 | FS-PERF-02 |
| DS-MES-136 | FS-AV-01 |
| DS-MES-137 | FS-AV-02 |
| DS-MES-138 | FS-BAK-01 |
| DS-MES-139 | FS-BAK-02 |
| DS-MES-140 | FS-BAK-03 |
| DS-MES-141 | FS-SEC-02 |
| DS-MES-142 | FS-SEC-04 |
| DS-MES-143 | FS-SEC-05 |
| DS-MES-144 | FS-TRN-01 |
| DS-MES-145 | FS-TRN-02 |
| DS-MES-146 | FS-PR-01 |
| DS-MES-147 | FS-PR-02 |
| DS-MES-148 | FS-XSYS-AD-01 |
| DS-MES-149 | FS-XSYS-BAK-01 |
| DS-MES-150 | FS-XINT-HEL-01 |
| DS-MES-151 | FS-XINT-HEL-02 |
| DS-MES-152 | FS-XINT-LMS-01 |
| MS-01..MS-12 | Cat-5 mini-SDS § 8.2 — site tasklets; transitively traces FS-DEV-01..05 + FS-EBR-* + FS-MAT-* + FS-WGH-* + FS-YLD-* + FS-REL-* + FS-XINT-* |

---

## 11. Design-level Risk Register

Per § 2B.8 — design-stage risks. Formal RA in `VBM-RA-MES-001` (synthetic).

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| DR-01 | Oracle Data Guard async lag exceeds 15-min RPO during peak load | Low | High | RPO monitored; switch to synchronous mode for critical batches; OQ `OQ-DR-RPO-01` |
| DR-02 | iPad MDM remote-wipe SLO (15 min) breached when device offline at incident time | Medium | High | MDM kill-switch on next online + GPO; quarterly testing |
| DR-03 | HAProxy `/health` endpoint returns 200 while App-Server is degraded (e.g., DB pool exhausted) | Medium | High | Deep health check (DB-ping included) + circuit-breaker; alerting on degraded-but-200 state |
| DR-04 | MBR state-machine bypass via direct DB write by privileged user | Low | Critical | DB role lacks UPDATE/DELETE on `mbr` when EFFECTIVE; DBA dual-control |
| DR-05 | Vault URN cache (24-h TTL) serves stale URN after a Vault doc supersedure | Medium | Medium | Miss-with-cache audit event + Vault webhook for invalidation |
| DR-06 | SoD policy engine (DS-MES-100) misclassifies sequential same-role actions on same record | Low | High | Server-side prior-action evaluation + extensive unit + integration tests |
| DR-07 | PKI signature payload (DS-MES-99) re-verification at every read creates DB hotspot | Medium | Medium | Verification cache (5-min TTL) with cache-bust on signature event |
| DR-08 | Kerberos fresh-ticket (5 min) on sign-off blocks legitimate ops during slow network | Medium | Medium | Pre-fetch ticket on UI focus; clear UI feedback |
| DR-09 | Tasklet hot-deploy introduces JAR-level conflict (classloader leak) | Low | Medium | Tasklet runtime isolates classloaders + memory-leak monitor |
| DR-10 | OPC UA cert (DS-MES-86) expiry stalls SCADA capture | Low | High | cert-manager 365-d rotation + 30-d alert |
| DR-11 | SAP PI/PO iDoc schema change unannounced breaks order ingestion | Medium | High | Automated contract tests in CI + schema versioning |
| DR-12 | LIMS poll cadence (60 s) misses fast-cycle samples | Low | Medium | Webhook receiver complement; OQ verifies coverage |
| DR-13 | Genealogy 24-mo P95 ≤ 30 s SLO degrades at extreme dataset growth | Medium | Medium | Partitioned indexes; quarterly query-plan review |
| DR-14 | QP-cert workflow (DS-MES-106) blocked on stale eQMS open-deviation cache | Low | Critical | eQMS webhook reconciliation runner + manual override path with QA dual-sign |
| DR-15 | Annex 16 CofC PDF template (DS-MES-109) regulatory format change unnoticed | Low | High | Annual template review under PR-01 + EMA guideline subscription |
| DR-16 | Helios Kafka egress lag > 600 s sustained → audit-stream gap | Low | High | DLQ + reprocess; Prometheus alert; deviation creation per FS-XINT-HEL-02 |
| DR-17 | LMS-competence adapter cache TTL (12-24 h) lets lapsed user execute gated action | Low | Critical | Reconciliation runner (FS-XINT-LMS-01) creates retroactive deviation; TTL tightened for safety-critical curricula |
| DR-18 | Audit `retention 25 y` (DS-MES-96) cold-store Object-Lock in Governance instead of Compliance Mode | Low | Critical | IQ verification of Compliance Mode at bucket creation + annual recheck |
| DR-19 | BPMN workflow definition (DS-MES-77) version drift between sites | Low | Medium | Versioned BPMN deployment + cross-site reconciliation report |
| DR-20 | Inspection-bundle export (DS-MES-133) misses live-write window during export | Low | Medium | Snapshot-cache pattern (`AS OF SCN` Oracle read consistency); OQ verified |
| DR-21 | Veeam Oracle RMAN backup creates DB write-pause beyond tolerance | Low | Medium | Backup window scheduled in maintenance window + monitored |
| DR-22 | AD Conditional Access (DS-MES-148) excludes a line workstation accidentally | Low | High | Named-location reconciliation + quarterly access review |
| DR-23 | Equipment-cycle webhook receiver (DS-MES-88) duplicate-delivery creates double-link | Low | Medium | Idempotency on `cycle_ref` + duplicate-detection log |
| DR-24 | Label-template registry (DS-MES-129) EFFECTIVE template fetched while OBSOLETE in transition | Low | High | Server-side state check at fetch time, not cached state |
| DR-25 | Step-retry (DS-MES-33) attempt-N+1 supersedes when prior attempt has open deviation linkage | Low | High | Attempt-N+1 inherits open-deviation FK; UI surfaces both in RBE view |
| DR-26 | Multi-site (DS-MES-127) cross-site recipe transfer (DS-MES-128) loses tasklet-version FK | Low | High | Cross-site workflow preserves tasklet IDs + versions + tech-transfer doc links; reconciliation runner |
| DR-27 | Material-reconciliation (DS-MES-40) runner closes window before late-arriving SAP webhook update | Medium | Medium | Reconciliation runner re-evaluates on subsequent webhook; QA alert on > 2% deviation |
| DR-28 | Inspection-mode auditor (DS-MES-132) cached snapshot lags real-time view during active inspection | Low | Medium | Snapshot refresh cadence configurable; auditor UI shows snapshot age |
| DR-29 | App-Server fault-domain distribution (DS-MES-09) CMDB record drifts vs physical placement | Medium | Medium | Annual physical-vs-CMDB reconciliation under PR-01 |
| DR-30 | Helios schema-registry (DS-MES-150) breaking change rolls out before consumer-side compatibility | Low | High | Schema-evolution gate at registry (FULL_TRANSITIVE compatibility mode); coordinated rollout per RACI |

### Design-level risk summary

The design-level risks split into five categories aligned with the FS pillars:

1. **Lifecycle-immutability risks** (DR-04, DR-05, DR-18, DR-24) — risks that originate in maintaining single-source-of-truth across MBR / EBR / label-template / Vault state machines while supporting CR-driven revisions.
2. **Identity / signature integrity risks** (DR-06, DR-07, DR-08, DR-17) — risks at the AD / Kerberos / PKI / LMS-competence boundary affecting SoD policy + signature verification + access gating.
3. **Integration-coherence risks** (DR-09, DR-10, DR-11, DR-12, DR-15, DR-16, DR-22, DR-23, DR-30) — risks at the vendor / cross-system boundary (SAP, LIMS, Vault, eQMS, CMMS, LMS, Helios, Conditional Access, equipment-cycle webhooks).
4. **Performance / DR risks** (DR-01, DR-13, DR-20, DR-21, DR-29) — risks affecting RPO / RTO / scalability / fault-domain distribution / inspection-bundle export.
5. **Workflow-state risks** (DR-14, DR-19, DR-25, DR-26, DR-27, DR-28) — risks where workflow state machines (QP-cert, BPMN versioning, step-retry, cross-site transfer, material reconciliation, inspection snapshot) drift between sites or across attempts.

Each row carries a mitigation reference to a DS-ID or governance instrument. Formal RA `VBM-RA-MES-001` (synthetic, downstream) re-evaluates with FMEA / HAZOP rigor.

---

## 12. Appendix B — Configuration Item count by FS module

| FS module | CI count (DS-MES-NN range) | Notes |
|---|---|---|
| Platform / Hardware | DS-MES-01..09 (9) | redundancy, DR, MDM, patching, HAProxy, fault domains |
| MBR lifecycle | DS-MES-10..19 (10) | states, dispatch gate, signatures, SoD, immutability, Vault URN, ISA-88, criticality, effectivity, diff |
| Order management | DS-MES-20..24 (5) | inbound validation, idempotency, ACK SLA, reschedule, cancellation |
| EBR execution | DS-MES-25..33 (9) | transactional, step-ordering, critical-step, OPC UA, IPC, dispense tolerance, RBE, long-step, retry |
| Material + genealogy | DS-MES-34..40 (7) | master schema, lot gate, genealogy linker, serialised, reservation, status webhook, reconciliation |
| Weighing | DS-MES-41..46 (6) | balance drivers, capture, OOT, tare drift, label, cal gate |
| Equipment | DS-MES-47..52 (6) | master schema, READY gate, clean gate, CMMS, cycle-link, RTS |
| Personnel | DS-MES-53..57 (5) | LMS gate, role-map CR, qual gate, handover, personnel report |
| Per-step recipe | DS-MES-58..60 (3) | sub-procedure lifecycle, approver, effectivity |
| Yield + deviation | DS-MES-61..65 (5) | yield, variance, classification, eQMS link, APR feed |
| Sampling | DS-MES-66..69 (4) | LIMS create, CoC, LIMS poll, OOS hook |
| Scheduling | DS-MES-70..72 (3) | Gantt, reschedule API, SAP push |
| Workflow / disposition | DS-MES-73..78 (6) | deviation guard, QA notify, eQMS push, disposition, BPMN, latency SLO |
| Genealogy | DS-MES-79..81 (3) | forward, backward, export |
| Integrations | DS-MES-82..91 (10) | SAP, SCADA, Vault, LMS, AD |
| Audit | DS-MES-92..96 (5) | schema, append-only, review UI, EBR-closure checkbox, retention |
| Part 11 | DS-MES-97..104 (8) | manifestation, identity binding, PKI signing, SoD, re-auth, Annex 11 map, password policy, coverage |
| Release (Annex 16) | DS-MES-105..110 (6) | QA gate, QP cert, open-dev gate, QP record, CofC PDF, QP dashboard |
| Data integrity | DS-MES-111..116 (6) | attribution, export, time sync, lineage, determinism, retrieval |
| Tasklets (Cat 5) | DS-MES-117..121 (5) | SDLC, deployment, repo, per-tasklet FS, coverage gate |
| Reporting | DS-MES-122..126 (5) | OEE, dashboards, APR, quarterly audit-review, report signing |
| Multi-site | DS-MES-127..128 (2) | per-site fields, recipe transfer |
| Label-template | DS-MES-129..131 (3) | registry, change workflow, scan-back |
| Inspection-readiness | DS-MES-132..133 (2) | auditor role, bundle exporter |
| Performance / availability | DS-MES-134..137 (4) | sizing, designer SLO, availability, Redis session |
| Backup | DS-MES-138..140 (3) | RMAN, restore test, DR exercise |
| Security | DS-MES-141..143 (3) | TLS, Nessus, bastion recording |
| Training | DS-MES-144..145 (2) | LMS gate, refresher |
| Periodic review | DS-MES-146..147 (2) | runbook, signing |
| Cross-system (M-XSYS) | DS-MES-148..149 (2) | Conditional Access, Veeam |
| Cross-integration (M-XINT) | DS-MES-150..152 (3) | Helios egress, parity reconciliation, LMS-competence |
| Cat-5 mini-SDS modules | MS-01..MS-12 (12) | tasklets — § 8.2 |
| **Total CIs (DS-MES-NN)** | **152** | |
| **Total tasklet modules (MS-NN)** | **12** | |

This breakdown supports auditor traceability when navigating large CS documents — each FS module's design-completeness can be verified by checking the CI-count range against the FS-ID coverage.

---

## 13. Appendix C — Cross-System Integration design summary

The cross-system integration design (FS § 4.27 / 4.28 / 4.29) introduces three downstream-coupling surfaces beyond the canonical PAS-X core integrations. The DS captures these as DS-MES-148..152 with full interface specs in § 7.12. Design notes worth surfacing for auditors:

**M-XSYS-AD (DS-MES-148).** The MES inherits the corporate AD identity contract (`QTZ-URS-AD-001`) — LDAPS on-prem with local OT cached credentials for offline operation. The `OT-MES Conditional Access` policy distinguishes engineering / line workstation MFA from operator-station named-location + smart-card binding. SIEM forwarding (Splunk `gxp-authn`) within 5 minutes ensures security operations have near-real-time visibility into MES authentication events. SCIM provisioning is used where the downstream protocol is SAML/OIDC (Werum/Körber tenancy-dependent). Break-glass account discipline (CyberArk PAM, 24-h rotation, dual-witness check-out) prevents long-lived elevated credentials in MES.

**M-XSYS-BAK (DS-MES-149).** The MES backup tier is T1 (RPO ≤ 4 h, RTO ≤ 4 BH) per `AUR-URS-BACKUP-001`. Veeam Application-Aware processing with Oracle RMAN is configured for the PAS-X Oracle backend; file-level capture covers recipe + order configuration. Immutable cloud-tier copies live in S3 Object Lock Compliance Mode (geo-replicated) — Governance Mode is explicitly **not** acceptable (mutable by root). Air-gap LTO-9 monthly rotation provides offline resilience. Monthly QA-witnessed restore tests per `AUR-FS-BACKUP-001` procedure produce restore-certificate quality records, retained ≥ 25 y in MasterControl eQMS.

**M-XINT-HEL (DS-MES-150/151).** Helios is the downstream audit-stream consumer (Kafka). Topic `helios.ingest.veridian.pasx.v1` carries the schema-registry-pinned envelope `{event_id, source_system, source_record_id, actor, ts_utc, ts_local, action, before, after, reason}`. At-least-once delivery + idempotency `{source_system, event_id}` ensures downstream consumers can dedup. Backpressure surfaces via Prometheus `helios_publish_lag_seconds` (5-min alert at > 600 s). Local audit-store retention ≥ 15 y supports Helios-side outage recovery. Periodic reconciliation job verifies parity (Helios row count == local published count) and raises a MasterControl deviation on > 0.01% mismatch over a 24 h window.

**M-XINT-LMS (DS-MES-152).** The LMS-competence handover adapter `<sys>-LMS-CLIENT-1.x` performs `GET /lms/competence/{user_id}?curriculum=...` over mTLS + Entra workload-identity. Per-curriculum cache TTL (12-24 h) balances LMS load vs gate-action freshness. On `current=false` the consumer blocks the gated action and records `lms_lapse_user={user_id}` in the consumer audit trail. A periodic reconciliation job verifies that no gated action proceeded with a lapsed competence — a hard guarantee for the LMS-gate property.

---

## 14. Appendix D — Tasklet inventory + governance

Per FS-DEV-04 / DS-MES-120, each tasklet has its own `VBM-FS-TASKLET-NNN` artefact + Cat-5 Risk Assessment + dedicated RTM row. The DS records the cross-tasklet architecture (§ 8) and inventories the planned tasklets at v1.0 ship:

| Tasklet ID | Tasklet name | FS-IDs primarily implemented | Cat-5 SDLC class | Coverage target | Owner |
|---|---|---|---|---|---|
| VBM-FS-TASKLET-001 | IpcEvaluator | FS-EBR-05 / FS-SMP-03 | R1 | ≥ 90% (safety) | Manufacturing IT |
| VBM-FS-TASKLET-002 | SamplePlanner | FS-SMP-01 / FS-SMP-02 | R2 | ≥ 80% | Manufacturing IT |
| VBM-FS-TASKLET-003 | DispenseToleranceCheck | FS-WGH-03 / FS-EBR-06 | R1 | ≥ 90% (safety) | Manufacturing IT |
| VBM-FS-TASKLET-004 | TareDriftCheck | FS-WGH-04 | R2 | ≥ 80% | Manufacturing IT |
| VBM-FS-TASKLET-005 | YieldCalculator | FS-YLD-01 | R1 | ≥ 90% (safety) | Manufacturing IT |
| VBM-FS-TASKLET-006 | VarianceEngine | FS-YLD-02 | R1 | ≥ 90% (safety) | Manufacturing IT |
| VBM-FS-TASKLET-007 | QaReviewGate | FS-REL-01 | R1 | ≥ 90% (safety) | Manufacturing IT |
| VBM-FS-TASKLET-008 | QpCertify (Annex 16 CofC) | FS-REL-02..06 | R1 | ≥ 95% (safety) | Manufacturing IT + QP |
| VBM-FS-TASKLET-009 | HeliosPublisher | FS-XINT-HEL-01 | R2 | ≥ 80% | Manufacturing IT |
| VBM-FS-TASKLET-010 | LmsCompetenceAdapter | FS-XINT-LMS-01 | R1 | ≥ 90% (safety) | Manufacturing IT |
| VBM-FS-TASKLET-011 | SignaturePki | FS-PART11-03 | R1 | ≥ 95% (safety) | Security IT |
| VBM-FS-TASKLET-012 | InspectionExporter | FS-INSP-02 | R2 | ≥ 80% | Manufacturing IT |

**Tasklet SDLC enforcement points:**

1. **Pre-commit:** GPG-signed commits required (DS-MES-119)
2. **PR review:** at least 1 reviewer + green CI + SonarQube quality gate + Snyk SCA + Bandit
3. **PR merge gate:** coverage threshold per tasklet GxP class (DS-MES-121)
4. **CR-bound deployment package:** signed JAR (DS-MES-117 / DS-MES-118)
5. **Promotion to PROD:** regression test pass mandatory; failure blocks promotion
6. **Post-deploy:** tasklet runtime classloader isolation prevents cross-tasklet JAR conflicts (mitigates DR-09)

Each tasklet's lifecycle is governed by `SDLC-MES-TASKLET-001`. Per-tasklet FS artefacts (`VBM-FS-TASKLET-NNN`) detail the algorithm, data model, error handling, and unit-test cases beyond the cross-tasklet architecture captured here in § 8.

## 15. Appendix E — Annex 16 + § 211.192 design coherence

The DS satisfies EU GMP Annex 16 (Certification by a Qualified Person) + 21 CFR § 211.192 (Production record review) requirements via the following design coherence chain:

| Regulatory clause | DS design choice (DS-MES-NN) | Compliance argument |
|---|---|---|
| Annex 16 § 1.7 (QP independence) | DS-MES-106 (QP terminal node) + DS-MES-100 (SoD) | QP role is the terminal disposition signer; SoD policy blocks if QP previously acted on the same EBR as Author / Reviewer |
| Annex 16 § 1.7.21 (open-deviation impact) | DS-MES-107 (open-dev gate) | Critical/Major open block; Minor requires QP-noted disposition text |
| Annex 16 Annex II (Confirmation of Compliance) | DS-MES-109 (CofC PDF) | Auto-generated on QP-sign; signed via PKI; template auditable |
| § 211.192 (production record review by QC) | DS-MES-105 (QA-review gate) | All EBR steps carry Quality Reviewer "review-complete" signature before disposition |
| § 211.192 (investigation of unexplained discrepancy) | DS-MES-73 (deviation guard) + DS-MES-75 (eQMS push) | Step-closure validator blocks open deviation; MasterControl source-of-truth post-disposition |
| Annex 16 § 1.4 (release decision basis) | DS-MES-108 (QP record table) | `(batch_id, qp_id, ts, statement, ebr_hash)` archived with EBR for inspection |
| Annex 16 § 5 (Sampling & sampling plans) | DS-MES-66..69 (LIMS sampling) | Chain-of-custody + result-status gate ensures only APPROVED samples release |

The QP-readiness dashboard (DS-MES-110) surfaces per-batch QA-review status + open-item count + certification-ready flag — designed as the QP's intake view for the daily release queue. Filterable by line, product, urgency.

## 16. Appendix F — Performance budget cross-references

The FS-PERF-NN performance targets are validated by specific DS configurations + OQ/PQ test references. The cross-reference enables performance auditors to trace each target to its enforcing CI:

| Performance target | DS configuration | OQ/PQ reference |
|---|---|---|
| 250 concurrent operators @ P95 navigation ≤ 1.5 s | DS-MES-134 (App-Server sizing) + DS-MES-137 (Redis sessions) | PQ `PQ-PERF-NAV-01` |
| MBR Designer save P95 ≤ 5 s @ 200-step MBR | DS-MES-135 (designer SLO) | OQ `OQ-MBR-PERF-01` |
| Genealogy P95 ≤ 30 s @ 24-mo dataset | DS-MES-79..81 (indexed query) | PQ `PQ-PERF-GENEALOGY-01` |
| Operating-hours availability ≥ 99.5% | DS-MES-136 (availability target) + DS-MES-02 (cluster failover) | External-probe measured monthly |
| Session-replication transparent failover | DS-MES-137 (shared Redis) | OQ `VBM-OQ-REDIS-01` |
| Workflow-step transition P95 ≤ 1 s | DS-MES-78 (BPMN engine + monitoring) | OQ `VBM-OQ-WF-LATENCY-01` |
| SAP-yield ack P95 ≤ 5 min | DS-MES-22 (PI/PO measured) + DS-MES-83 (outbound iDoc) | OQ `VBM-OQ-ORD-ACK-01` |
| RPO ≤ 15 min, RTO ≤ 4 h | DS-MES-03 (Data Guard async) + DS-MES-138 (RMAN PITR) | OQ `OQ-DR-RPO-01` + PQ `PQ-DR-01` |
| Helios publish lag < 600 s | DS-MES-150 (Prometheus exporter) | OQ `VBM-OQ-HELIOS-PUB-01` |

This cross-reference is the audit-ready proof that each performance NFR has a controlling DS CI plus a specific OQ/PQ test.

## 17. Appendix G — Data Integrity (ALCOA+) design mapping

The DS satisfies the nine ALCOA+ attributes through specific design choices documented in § 4 (CIs) and § 8 (data model). The mapping below ties each ALCOA+ letter to controlling CIs + OQ tests:

| ALCOA+ attribute | DS CI(s) | OQ verification |
|---|---|---|
| **A — Attributable** | DS-MES-111 (AD user-id) + DS-MES-92 (audit schema with `actor_id`) | `VBM-OQ-DI-ATTRIB-01` |
| **L — Legible** | DS-MES-94 (review UI human-readable) + DS-MES-112 (PDF export with audit) | `OQ-EXPORT-01` |
| **C — Contemporaneous** | DS-MES-113 (NTP + PTP at every signature) + DS-MES-92 (`timestamp` field PTP-derived) | `VBM-OQ-PTP-01` |
| **O — Original** | DS-MES-114 (originals immutable + derivation lineage) | `VBM-OQ-DI-LIN-01` |
| **A — Accurate** | DS-MES-115 (deterministic calc engine) + DS-MES-13 (SoD signing check) | `OQ-CALC-01` |
| **+ Complete** | DS-MES-92 (audit schema includes old/new + reason) + DS-MES-95 (EBR-closure review checkbox) | `VBM-OQ-AUDIT-RVW-CHECK-01` |
| **+ Consistent** | DS-MES-93 (append-only) + DS-MES-99 (PKI re-verify on read) | `VBM-OQ-AUDIT-APPEND-01` + `VBM-OQ-SIG-PKI-01` |
| **+ Enduring** | DS-MES-96 (`STG-ARCHIVE-LYFCYC-001` cold-store ≥ 25 y) | (governance) + IQ verification of Compliance Mode |
| **+ Available** | DS-MES-116 (4-BH retrieval SLA via inspection runbook) | `VBM-OQ-RETR-01` |

This mapping satisfies the FDA Data Integrity & Compliance Guidance (April 2018), the EU GMP Annex 11 §§ 7, 9, 12, and the PIC/S PI 041 GxP data-integrity expectations.

## 18. Appendix H — Configuration-drift detection design

PAS-X v3.2 configuration drift is the primary failure mode for long-lived MES installs. The DS records the drift-detection design as a separate concern:

| Drift surface | Detection mechanism | Action on detection |
|---|---|---|
| AD-group → PAS-X role mapping | Daily reconciliation runner queries AD + role-mapping table; diff alerts on changes | CR required (DS-MES-54); audit event `role_map_change` |
| Workflow definitions (BPMN) | BPMN-engine version-pinning + deployment requires CR; quarterly reconciliation | CR required (DS-MES-77) |
| Label templates | Registry state-machine + post-print scan-back | Mismatch → step-closure block (DS-MES-131) |
| OPC UA tag-list (SCADA) | Tag-list versioned + diff at each integration test | CR required (DS-MES-86) |
| Equipment-master | Equipment-class invariants enforced; quarterly inventory reconcile | CR + audit (DS-MES-47) |
| Material-master replication from SAP | Daily reconciliation runner; > 0.1% drift → alarm + optional lock-down | Investigation deviation (DS-MES-84) |
| Vault URN catalogue | URN cache invalidation via Vault webhook | Cache flush + warning audit (DS-MES-89) |
| Periodic Review | Annual full-platform PR runbook | PR-01 report signed by Mfg IT Lead + Head of QA |

The combination forms a defense-in-depth drift-detection posture: each configuration surface has either continuous reconciliation (AD, material-master), event-driven detection (label scan-back, OPC UA cert), or scheduled audit (BPMN, equipment-master, PR-01).

## 19. Appendix I — Coverage gap analysis

All 134 FS-IDs from `VBM-FS-MES-001` v1.2 are covered by at least one DS-MES-NN CI. The breakdown:

- **Fully covered (1 DS-ID → 1 FS-ID):** 116 FS-IDs
- **Multi-CI covered (1 DS-ID → 2+ FS-IDs, where the DS choice satisfies more than one FS row):** 18 FS-IDs (e.g., DS-MES-66 covers FS-SMP-01 + FS-INT-LIMS-01; DS-MES-86 covers FS-INT-SCADA-01 + FS-EBR-04 dependency; DS-MES-91 covers FS-INT-AD-01 + FS-SEC-01)
- **Cat-5 mini-SDS reference (FS-DEV-* + indirect FS-IDs covered via the tasklet ecosystem):** 12 FS-IDs reference site Cat-5 code (FS-DEV-01..05 + the FS-IDs the tasklets implement)

No FS-ID is uncovered; no DS-ID is orphan. The Cat-5 mini-SDS (§ 8) transitively traces every Cat-5-relevant FS-ID via the module decomposition + tasklet inventory (§ 14).

## 20. Appendix J — Inspection-readiness operational protocol

DS-MES-132 (auditor role) + DS-MES-133 (bundle exporter) jointly implement the inspection-readiness SLA. Operational protocol:

1. **Inspector arrives + identifies scope** → System Owner assigns auditor role with window-bound access (e.g., 8 h)
2. **Auditor accesses cached-snapshot UI** → no production-record contention; UI clearly displays snapshot age + scope
3. **Inspector requests bundle for batch X** → Quality Reviewer triggers bundle exporter via `/api/inspection/bundle`
4. **Bundle assembly (≤ 4 BH SLA)** → EBR + audit + genealogy + QP cert assembled; signed via PKI; PDF/A-3 + JSONL
5. **Bundle handed to inspector via secure portal** → access logged + audit-traced
6. **Window expires** → auditor access revoked; bundle remains in inspection archive

This protocol is rehearsed annually under the FS-INSP-02 OQ test and is the proof that the design satisfies inspection-readiness obligations under EU GMP Annex 11 § 4.4 and 21 CFR Part 11 § 11.10(b).

## 21. Appendix K — Multi-site rollout design notes

DS-MES-127 + DS-MES-128 implement multi-site capability. Design notes worth surfacing for sister-site rollouts:

- **Per-site effectivity:** MBRs / recipes / tasklets carry `effective_for_site[]` field; deployment-target field on each artefact ensures cross-site share without unintended cross-deployment.
- **Tech-transfer doc linkage:** cross-site recipe-transfer workflow preserves the tech-transfer document trail in `recipe_transfer_history`; auditor can trace recipe genealogy across sites.
- **Per-site SAP integration:** each site has its own SAP PI/PO endpoint; idempotency keys are namespaced by `site_id` to avoid cross-site collision.
- **Per-site Helios topic:** the M-XINT-HEL topic uses `helios.ingest.<site>.pasx.v1` naming convention; consumer-side filtering by site_id.
- **Per-site LMS curriculum:** LMS-competence adapter (DS-MES-152) takes both `user_id` and `site_id` to ensure the gated action's competence applies to the correct site context.

A sister-site rollout reuses this DS as the structural template; site-specific values (URLs, AD tenancy, Vault PKI roots, SAP endpoints) are parameterized in `<site>_config.yaml`.

## 22. Appendix L — Decommissioning + retirement design

PAS-X v3.2 at end-of-platform-life will require a coordinated decommissioning. The DS captures the design forethought:

- **Audit-trail retention:** 25 y from product expiry survives platform retirement; immutable S3 storage outlives the application
- **Configuration export:** PAS-X XML archive format export validated for all EFFECTIVE / OBSOLETE recipes + closed EBRs at decommission boundary
- **Helios audit-stream:** continues to consume from local audit-store during cut-over to successor platform (DS-MES-150 / DS-MES-151)
- **QP records:** Annex 16 certifications archived alongside EBRs in inspection-ready bundle format
- **Successor-platform mapping:** decommissioning runbook records the data-migration mapping for each entity table

This forward-looking design choice prevents the common pharma anti-pattern of "shadow MES" that persists past official decommission because data could not be migrated.

The decommissioning runbook is referenced as `VBM-RUN-MES-DECOM-001` (deferred to platform-end-of-life and out of scope for the v1.0 DS issue).

## 23. Appendix M — DS authoring discipline notes

The 152 DS-MES-NN configuration items in § 4 were authored following the methodology § 2B.4 rules: per-vendor-named CIs only, default-vs-custom flag on every row, justification linking the CI to a specific compliance need, FS-IDs traced (no range compression), and Verified-by column citing the planned IQ/OQ/PQ test.

Site-developed custom code (tasklets, Cat 5) appears in § 8 as a mini-SDS per § 2B.4 rule 6; the Cat-5 escalation rule applies because PAS-X tasklets embed custom Java logic. Per-tasklet FS artefacts (`VBM-FS-TASKLET-NNN`) carry the per-module algorithm + data-model + unit-test detail beyond the cross-tasklet architecture in § 8.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
