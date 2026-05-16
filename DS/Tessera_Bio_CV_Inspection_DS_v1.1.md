---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "TES-FS-CV-001 v1.2 (parent FS)"
  - "TES-URS-CV-001 v1.2 (informational)"
  - "GAMP 5 (2nd ed., 2022) Cat 5 — Software Design Specification"
  - "EU AI Act 2024/1689 Annex I high-risk (safety component of sterile injectable per EU GMP Annex 1 § 8.123 + USP <790>/<1790>); deadline 2 Aug 2027"
  - "IEC 62304; ISO/IEC 42001:2023; PDA TR 79; FDA AI/ML SaMD; FDA GMLP; FDA PCCP"
parent_fs:
  document_number: TES-FS-CV-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Tessera_Bio_CV_Inspection_FS_v1.3.md
parent_urs:
  document_number: TES-URS-CV-001
  version: 1.2
  file: ../../../URS/_generated/final/Custom_Computer_Vision_Inspection_System__Tessera_Bio_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Software Design Specification (SDS)

## Custom Computer Vision Inspection System — Site-Developed Python + PyTorch + Basler Cameras + NVIDIA Jetson

**Document Number:** TES-DS-CV-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** TES-FS-CV-001 v1.2 | **Parent URS:** TES-URS-CV-001 v1.2
**Site:** Tessera Bio Manufacturing GmbH, Sterile Fill-Finish Plant 1, Mannheim, Germany *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 5 — Custom Application (site-developed CV / DL models on NVIDIA Jetson + ONNX Runtime; Basler cameras as Cat-3 substrate; PLC integration as Cat-3)
**EU AI Act 2024/1689 classification:** **Annex I high-risk AI system** (safety component of the release decision for sterile injectables per EU GMP Annex 1 § 8.123 visible-particulate inspection + USP <790> / USP <1790> visual inspection). Conformity-assessment pathway Annex VII (notified-body involvement) where the underlying medicinal product is required by EU GMP Annex 1 to undergo 100% visible-particulate inspection. **Compliance deadline 2 August 2027**. Art. 99 penalty tier: up to €15M / 3% global turnover for non-compliance.
**Project Mode:** Greenfield site-developed CV pipeline replacing legacy semi-automated inspection line (per parent URS Project Mode line)
**Tier (inherited from parent URS+FS):** T4
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; **21 CFR Part 211 §§ .22 (responsibilities of QCU), .68 (automatic equipment), .110 (sampling + testing of in-process materials), .192 (production-record review)**; EU GMP Annex 11; **EU GMP Annex 1 (2022 revision) — sterile-product manufacture, esp. § 8.123 visible-particulate inspection**; **EU AI Act 2024/1689 Arts. 8–21, 26, 43, 47–49, 50 (transparency — synthetic-output labelling), 72, 73, 99, 113**; **USP <1>, <787> (sub-visible 5–50 μm), <788> (sub-visible 10–25 μm), <790> (visible particulates), <1790> (visual inspection of injections)**; **Ph. Eur. 2.9.20 (particulate contamination — visible particles)**; FDA AI/ML SaMD Action Plan; FDA GMLP (2021); FDA PCCP (Aug 2025); FDA CSA (Feb 2026); ISPE GAMP GPG *AI/ML in GxP* (2024); ISO 14971:2019; ISO/IEC 42001:2023; **PDA Technical Report 79 (visible particulate inspection)**; BfArM (DE), Swissmedic (CH), AGES (AT).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect — Vision Inspection) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Head of Sterile Manufacturing) | _____________ | _____________ | _____ |
| Reviewer (QCU Manager — 21 CFR 211.22) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Security Architect) | _____________ | _____________ | _____ |
| Reviewer (Reg Affairs — AI/ML + sterile) | _____________ | _____________ | _____ |
| Reviewer (Notified Body Liaison) | _____________ | _____________ | _____ |
| Reviewer (PLC + Automation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Inspection-Operations Lead) | _____________ | _____________ | _____ |
| Approver (VP Manufacturing) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |
| Approver (VP Regulatory Affairs) | _____________ | _____________ | _____ |
| Approver (System Owner — Head of Sterile Manufacturing) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue. Inherited Tier T4 from parent URS+FS pair. Derived from TES-FS-CV-001 v1.2. DS covers 124/131 FS-IDs as DS-IDs; 7 FS-IDs flagged as "vendor-internal — no site design surface" (Basler camera firmware internals, NVIDIA Jetson driver internals, ONNX Runtime internals, MES PAS-X internal scheduler, Siemens S7 PLC firmware internals, Cognex job-edit internals, lifecycle manager internals). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from TES-URS-CV-001 v1.2 and TES-FS-CV-001 v1.2. Additional DS-specific terms:

| Term | Definition |
|---|---|
| Visible particulate | Particle ≥ 50 μm visually detectable per USP <790> / EP 2.9.20 |
| Zone of rejection | Defined region of a container where any defect classifies the unit as defective |
| Knapp-Kushner Probability of Detection (POD) | Standard validation metric for visual-inspection (USP <1790>) |
| MES PAS-X | Werum / Körber MES for sterile manufacturing (lifecycle scheduling + EBR) |
| ONNX Runtime | Open-source inference engine for ONNX-format models |
| Basler GigE Vision | Industrial-camera transport over Gigabit Ethernet |
| YOLO / SAM | YOLOv8 / Segment-Anything-Model (CV model families) |
| BBE | Batch Bill of Engineering — per-product configuration set |
| EBR | Electronic Batch Record (MES PAS-X) |
| Cognex VisionPro | Optional fixed-rule classical-CV fallback library |
| PCCP | Predetermined Change Control Plan (FDA Aug 2025) |

## 1. Purpose

This SDS describes the technical design of the site-developed Computer Vision Inspection System: site-developed Python + PyTorch + ONNX Runtime CV pipeline running on NVIDIA Jetson AGX Orin edge nodes; Basler GigE Vision camera arrays; PLC handshake to the inspection line; per-product BBE configuration; classical-CV fallback (Cognex VisionPro); challenge-set validation against USP <790> + USP <1790> Knapp-Kushner POD; PCCP-managed model lifecycle; PLC reject/accept handshake; EBR record generation via MES PAS-X. The SDS is the controlling input to Module Specs (`TES-MS-CV-{module}-001`), Annex IV technical-documentation pack template `lyr-aiact-techdoc/`, IQ/OQ/PQ Protocol Set, Notified Body submission, and the validation report against Annex 1 + USP <790> / <1790>. Vendor internals (Basler firmware, Jetson driver, ONNX Runtime, Cognex jobs, MES PAS-X scheduler, Siemens S7 firmware) are not redrawn.

## 2. Scope

**In scope.** Site-developed Python services (image-ingestion, pre-processing, YOLO + SAM derivative inference, defect-classification, zone-of-rejection logic, confidence threshold gate, PLC reject/accept signalling, EBR generation, challenge-set runner, PCCP predicate engine, Annex IV pack manager, Art. 73 incident service, human-override flow, audit-event writer, model lifecycle (train → eval → register → promote)); edge deployment topology (NVIDIA Jetson AGX Orin nodes per inspection station); Basler camera array configuration; per-product BBE; classical-CV fallback (Cognex VisionPro); MES PAS-X integration (EBR + lifecycle); PLC integration (Siemens S7); MOC (Lyrae Bioworks Model Server cross-system integration for off-line evaluation pipelines).

**Out of scope.** Basler camera firmware (vendor SDLC); NVIDIA Jetson driver (vendor); ONNX Runtime kernel (vendor); Cognex job-edit internals (vendor); MES PAS-X scheduler internals (vendor); Siemens S7 PLC firmware (vendor); sterile-line manufacturing-train design (separate URS).

## 3. Architectural Overview

```
                        ┌─ Tessera Provider boundary (Art. 8–21) ─────┐
                        │                                              │
   Inspection Line     ─┼─►  Basler ace U camera array (GigE Vision)  │
   (sterile fill-       │     2× back-light + 1× side-light station    │
    finish, 100% visual │                  │                          │
    per Annex 1 § 8.123)│                  ▼                          │
                        │     ┌───────────────────────────────────┐    │
                        │     │ NVIDIA Jetson AGX Orin (edge)     │    │
                        │     │  GPU 275 TOPS                     │    │
                        │     │ ┌──────────────────────────────┐  │    │
                        │     │ │ Pre-processing               │  │    │
                        │     │ │ (de-Bayer, ROI crop, norm)   │  │    │
                        │     │ └─────────┬────────────────────┘  │    │
                        │     │           ▼                       │    │
                        │     │ ┌──────────────────────────────┐  │    │
                        │     │ │ YOLOv8 detector (defect      │  │    │
                        │     │ │ bounding-boxes + class)      │  │    │
                        │     │ └─────────┬────────────────────┘  │    │
                        │     │           ▼                       │    │
                        │     │ ┌──────────────────────────────┐  │    │
                        │     │ │ SAM-derivative segmenter     │  │    │
                        │     │ │ (per-box mask refinement)    │  │    │
                        │     │ └─────────┬────────────────────┘  │    │
                        │     │           ▼                       │    │
                        │     │ ┌──────────────────────────────┐  │    │
                        │     │ │ Zone-of-rejection logic +     │  │    │
                        │     │ │ confidence gate              │  │    │
                        │     │ └─────────┬────────────────────┘  │    │
                        │     │           ▼                       │    │
                        │     │ ┌──────────────────────────────┐  │    │
                        │     │ │ Classical-CV fallback        │  │    │
                        │     │ │ (Cognex VisionPro — optional)│  │    │
                        │     │ └─────────┬────────────────────┘  │    │
                        │     │           ▼                       │    │
                        │     │ Reject decision (Accept/Reject/  │    │
                        │     │  HumanReview)                     │    │
                        │     └───────────┬───────────────────────┘    │
                        │                 │                            │
                        │                 ▼  Siemens S7 PLC handshake  │
                        │       Reject station mechanical actuator     │
                        │                                              │
                        │   ┌────────────────────────────────────┐     │
                        │   │ Inspection control plane (cluster) │     │
                        │   │  K8s 1.30 (Mannheim factory cluster)│    │
                        │   │  ┌─ Model registry (MLflow)        │     │
                        │   │  ├─ PCCP engine                    │     │
                        │   │  ├─ Challenge-set runner            │     │
                        │   │  ├─ Annex IV pack manager           │     │
                        │   │  ├─ HumanReview station UI          │     │
                        │   │  ├─ Audit + EBR feeder              │     │
                        │   │  └─ Art. 73 incident service        │     │
                        │   └────────────────────────────────────┘     │
                        │                 │                            │
                        └─────────────────┼────────────────────────────┘
                                          ▼
                            MES PAS-X EBR + Lyrae Model Server (off-line eval) +
                            BfArM/Swissmedic/AGES (Art. 73) + EU AI DB (Art. 49)
```

**Three architectural views per § 2B.5(1):**

**Logical view.** Each inspection station (Jetson edge) pulls images from Basler cameras (GigE Vision), runs the multi-stage CV pipeline (pre-process → YOLO → SAM → zone-of-rejection → confidence gate), and emits an accept/reject/human-review decision over the Siemens S7 PLC handshake. The Mannheim factory K8s cluster hosts the control plane: MLflow model registry, PCCP engine, challenge-set runner (USP <1790> Knapp-Kushner POD validation), Annex IV pack manager, HumanReview station UI, EBR feeder to MES PAS-X, and Art. 73 incident service. Cross-system handoff to Lyrae Model Server (`LYR-FS-MLSRV-001`) is for off-line evaluation pipelines only — runtime inference is on-edge.

**Process view.** Edge nodes: Jetson AGX Orin (1 per inspection station × 4 stations). Per station: pre-process → YOLO → SAM → zone-of-rejection → confidence gate runs at 60 fps with P95 ≤ 16 ms per frame (target: 50 ms total decision latency to PLC). Control-plane K8s cluster: 3 control-plane nodes + 6 worker nodes (factory floor); HPA disabled on production inspection-deployment (deterministic-load model); CIS Kubernetes Benchmark (current release at site deployment). Network: factory L2 isolation; out-of-band SCADA VLAN.

**Technology view.** Python 3.12; PyTorch 2.4 (training); ONNX Runtime 1.20 (edge inference on Jetson via TensorRT 10 EP); YOLOv8 (custom-trained derivative); Segment-Anything-Model (custom-trained derivative); Cognex VisionPro 10 (classical-CV fallback); Basler ace U cameras (3 per station; GigE Vision via Pylon SDK 8.0); Siemens S7-1500 PLC (TIA Portal); Werum MES PAS-X V5.x (EBR); K8s 1.30 (factory); MLflow 2.18; Postgres 16; Vault 1.18; Sigstore cosign 2.4; Prometheus 3.0 + Grafana 11 + Loki 3.0; Splunk Universal Forwarder 9.3.

**EU AI Act Annex I declaration.** This system is classified **Annex I high-risk** because the inspection decision is the **safety component** of the sterile-injectable release decision per EU GMP Annex 1 (2022 revision) § 8.123 (visible-particulate inspection — 100% inspection required for parenterals) and per USP <790> / USP <1790> (visual inspection of injections). A false-negative (failing to reject a contaminated unit) directly impacts patient safety. Conformity-assessment pathway: **Annex VII** (notified-body involvement) per Art. 43. Art. 99 penalty up to €15M / 3% global turnover for non-conformance.

## 4. Software Architecture

Seven layers (logical view):

1. **Image-acquisition Plane** — Basler camera array configuration; GigE Vision frame capture; Pylon SDK 8.0; per-station synchronisation (back-light + side-light coordinated via PLC trigger).
2. **Pre-processing Plane** — de-Bayer; ROI crop per BBE; spatial normalisation; intensity normalisation; bad-pixel masking.
3. **Inference Plane** — ONNX Runtime + TensorRT EP on Jetson AGX Orin; YOLO bounding-box + class detection; SAM-derivative per-box mask refinement.
4. **Decision Plane** — Zone-of-rejection logic per USP <790> + per-BBE configuration; confidence-threshold gate; classical-CV fallback (Cognex) when DL confidence < threshold and BBE allows fallback.
5. **Actuation Plane** — Siemens S7 PLC handshake; reject-station mechanical actuator drive; HumanReview kiosk for borderline decisions.
6. **Control-Plane** — MLflow model registry; PCCP engine; challenge-set runner (USP <1790> POD validation); Annex IV pack manager; Art. 73 incident service; EBR feeder; audit-event writer.
7. **Cross-System Plane** — MES PAS-X (EBR + BBE master + lifecycle); Lyrae Model Server (off-line eval); BfArM/Swissmedic/AGES (Art. 73); EU AI DB (Art. 49); EUDAMED where SaMD per use-case; Quartz AD (identity); Aurora Backup; LMS competence.

## 5. Module Decomposition

| Module ID | Name | Responsibility | Interface | Dependencies | Owner | GxP-criticality |
|---|---|---|---|---|---|---|
| MOD-IMG-01 | `basler-camera-driver` | Pylon SDK 8.0 wrapper; per-camera config | library + REST `/cameras/{id}/config` | Pylon SDK, GigE Vision NIC | Vision Eng | R1 (image integrity) |
| MOD-IMG-02 | `frame-grabber` | Sync 3 cameras per station via PLC trigger | library | PLC trigger pulse | Vision Eng | R1 |
| MOD-IMG-03 | `bbe-loader` | Per-product Batch Bill of Engineering loader | REST `/bbe/{product_id}` | MES PAS-X master | Product Eng | R1 |
| MOD-HW-01 | `jetson-runtime` | TensorRT EP setup; pinned driver version | Helm + DaemonSet | Jetson, TensorRT | Edge Ops | R1 |
| MOD-HW-02 | `camera-config-manager` | Per-station camera config rendering | Helm | per-station inventory | Edge Ops | R2 |
| MOD-HW-03 | `light-controller` | Back-light + side-light intensity per BBE | PLC variable + REST | PLC | Vision Eng | R2 |
| MOD-HW-04 | `pylon-failover` | Detect camera disconnect → halt line | inline | PLC, MOD-IMG-01 | Vision Eng | R1 (line-safety) |
| MOD-HW-05 | `bad-pixel-detector` | Daily bad-pixel map per camera | scheduled | MOD-IMG-01 | Edge Ops | R2 |
| MOD-PRE-01 | `de-bayer` | RAW → RGB | inline | — | Vision Eng | R2 |
| MOD-PRE-02 | `roi-crop` | Per-BBE ROI crop | inline | BBE config | Vision Eng | R1 |
| MOD-PRE-03 | `normaliser` | Spatial + intensity norm | inline | calibration | Vision Eng | R1 |
| MOD-IMG-PRE | `image-pipeline-orchestrator` | Compose pre-processing stages | library | MOD-PRE-* | Vision Eng | R1 |
| MOD-ML-01 | `yolo-detector` | YOLOv8 inference | ONNX model + ORT EP | Jetson, ORT, model artefact | AI Platforms | R1 (Art. 15) |
| MOD-ML-02 | `sam-segmenter` | SAM-derivative mask | ONNX model + ORT EP | Jetson, ORT, model artefact | AI Platforms | R1 |
| MOD-ML-03 | `defect-classifier` | Class label per detection | inline | YOLO + SAM output | AI Platforms | R1 |
| MOD-ML-04 | `confidence-gate` | Per-defect-class confidence threshold | inline | per-BBE threshold | AI Platforms | R1 (Art. 15) |
| MOD-ML-05 | `zone-of-rejection-logic` | Per USP <790> + per-BBE zones | inline | BBE zones config | Validation IT | R1 (Annex I core decision) |
| MOD-ML-06 | `classical-cv-fallback` | Cognex VisionPro fallback | inline (Cognex SDK) | Cognex SDK, BBE | Vision Eng | R2 |
| MOD-ML-07 | `decision-fuser` | Combine DL + classical-CV → Accept/Reject/HumanReview | inline | per-BBE policy | Validation IT | R1 |
| MOD-ML-08 | `inference-orchestrator` | Pipeline orchestrator | library | MOD-ML-01..07 | AI Platforms | R1 |
| MOD-OPT-01 | `tensorrt-engine-builder` | ONNX → TensorRT engine optimisation | scheduled | ONNX, TensorRT | Edge Ops | R2 |
| MOD-OPT-02 | `int8-calibrator` | Post-training quantisation calibration | scheduled | training-eval set | Edge Ops | R2 |
| MOD-OPT-03 | `engine-cache` | Cached compiled engines per Jetson SKU | — | TensorRT | Edge Ops | R2 |
| MOD-OPT-04 | `latency-profiler` | Per-stage latency profiling | scheduled | Prometheus | Edge Ops | R2 |
| MOD-DEV-01 | `factory-k8s-deployer` | K8s + factory-floor deployment | Helm + Terraform | K8s, ArgoCD | Edge Ops | R2 |
| MOD-DEV-02 | `argocd-jetson-bridge` | ArgoCD → Jetson DaemonSet | Helm | ArgoCD | Edge Ops | R2 |
| MOD-DEV-03 | `model-deployment-orchestrator` | MLflow → ONNX → TensorRT → Jetson | scheduled | MLflow, MOD-OPT-01 | AI Platforms | R1 |
| MOD-DEV-04 | `bbe-config-deployer` | BBE Helm/ConfigMap | Helm | MES PAS-X | Product Eng | R1 |
| MOD-DEV-05 | `rollback-orchestrator` | One-shot rollback to previous model | scheduled + REST | MLflow | AI Platforms | R1 |
| MOD-DEV-06 | `canary-deploy` | Shadow / canary on 1 station | scheduled | per-station inventory | AI Platforms | R2 |
| MOD-DEV-07 | `factory-floor-rollout-gate` | Production rollout requires QA + line-stop window | REST | QA + Line-Ops | Validation IT | R1 |
| MOD-INF-01 | `inference-gateway` | Edge HTTP receiver (factory K8s) | REST | Jetson | Edge Ops | R1 |
| MOD-INF-02 | `inference-record-writer` | Per-frame record | inline | Postgres | Edge Ops | R1 (audit) |
| MOD-INF-03 | `plc-handshake` | Siemens S7 communication | inline (S7 protocol) | Siemens S7 PLC | Automation | R1 (line safety) |
| MOD-INF-04 | `reject-actuator` | Drive reject-station mechanism | PLC variable | PLC | Automation | R1 |
| MOD-INF-05 | `humanreview-kiosk` | Borderline-case kiosk UI | Web app | inspection record | Inspection Ops | R1 (Art. 14) |
| MOD-AUD-01 | `audit-event-writer` | All transitions + decisions emit audit | library + Postgres trigger + Splunk | Postgres | Edge Ops | R1 (Part 11) |
| MOD-AUD-02 | `audit-export` | JSON/CSV/PDF/A-3 | REST | Postgres view | Edge Ops | R2 |
| MOD-AUD-03 | `inspection-record` | Per-unit record with image + decision + reviewer | Postgres + S3 | Postgres + S3 | Edge Ops | R1 |
| MOD-AUD-04 | `ebr-feeder` | Emit EBR fields to MES PAS-X per batch | REST + Kafka | MES PAS-X | Edge Ops | R1 |
| MOD-AUD-05 | `audit-volume-monitor` | Audit-event-rate Prometheus monitor | inline | Prometheus | Edge Ops | R2 |
| MOD-LBL-01 | `image-label-store` | Reference image + labels for training | S3 + Postgres | training data | Data Eng | R1 (lineage) |
| MOD-LBL-02 | `label-versioning` | Annotation-version control | Git | label data | Data Eng | R1 |
| MOD-LBL-03 | `label-qa` | Inter-annotator agreement KPI | scheduled | labelling team | Data Eng | R2 |
| MOD-LBL-04 | `image-checksum` | SHA-256 of every captured frame | inline | — | Edge Ops | R1 (data integrity) |
| MOD-LBL-05 | `image-retention` | Per-batch + post-event image retention | scheduled | S3 lifecycle | Edge Ops | R1 |
| MOD-CHAL-01 | `challenge-set-runner` | USP <1790> Knapp-Kushner POD validation | scheduled + REST | challenge images | Validation IT | R1 (Annex I validation gate) |
| MOD-CHAL-02 | `usp-1790-baseline` | Per-product POD baseline | Postgres | challenge runner | Validation IT | R1 |
| MOD-CHAL-03 | `challenge-set-curation` | Curated challenge images per defect class + size | Git + S3 | — | Validation IT | R1 |
| MOD-CHAL-04 | `pccp-driven-rechallenge` | Re-challenge on PCCP-conformant model update | scheduled | PCCP engine | Validation IT | R1 |
| MOD-PCCP-01 | `pccp-predicate-engine` | FDA Aug 2025 envelope evaluation | REST + library | MLflow | Reg-Affairs IT | R1 |
| MOD-PCCP-02 | `pccp-record` | PCCP record schema | Postgres | MLflow | Reg-Affairs IT | R1 |
| MOD-PCCP-03 | `pccp-deviation` | Deviation record + Art. 43(4) trigger | REST | MOD-INC-01 | Reg-Affairs IT | R1 |
| MOD-PCCP-04 | `pccp-annual-review` | Annual review per model | scheduled | MOD-PR-01 | Reg-Affairs IT | R1 |
| MOD-TD-01 | `annex4-pack-manager` | Per-model Annex IV pack | REST + CLI | S3 `tes-aiact-techdoc/` | Reg-Affairs IT | R1 |
| MOD-TD-02 | `annex4-export` | Export bundle | scheduled + REST | MOD-TD-01 | Reg-Affairs IT | R1 |
| MOD-TD-03 | `annex4-template-version` | Template version pin | Git | — | Reg-Affairs IT | R2 |
| MOD-CONF-01 | `conformity-workflow` | Notified Body engagement | REST | NB interface | Reg-Affairs IT | R1 (Art. 43) |
| MOD-CONF-02 | `eu-doc-generator` | EU DoC | REST + DocuSign | NB record | Reg-Affairs IT | R1 (Art. 47) |
| MOD-CONF-03 | `ce-marking-service` | CE marking record | REST | conformity record | Reg-Affairs IT | R1 (Art. 48) |
| MOD-CONF-04 | `substantial-mod-detector` | Detect substantial modification via PCCP | scheduled | PCCP | Reg-Affairs IT | R1 |
| MOD-REG-01 | `eu-aidb-registrar` | EU AI DB registration | REST | EU AI DB | Reg-Affairs IT | R1 (Art. 49) |
| MOD-HUM-01 | `ho-operator-ui` | HO Operator monitoring dashboard | Web app | Prometheus, MLflow | HO Ops | R1 (Art. 14) |
| MOD-HUM-02 | `humanreview-station` | Per-station HumanReview kiosk | Web app + camera | inspection record | Inspection Ops | R1 |
| MOD-HUM-03 | `human-override-service` | Override; downstream impact | REST | MOD-AUD-01 | HO Ops | R1 |
| MOD-INC-01 | `art73-incident-service` | 3 clocks (15/10/2) | REST + cron | regulatory routing | Reg-Affairs IT | R1 (Art. 73) |
| MOD-INC-02 | `regulatory-router` | DE→BfArM, CH→Swissmedic, AT→AGES | library | Vault certs | Reg-Affairs IT | R1 |
| MOD-INC-03 | `eu-mdr-art87-bridge` | Where output supports MDR class IIa+ device | REST | EUDAMED | Reg-Affairs IT | R2 |
| MOD-BIA-01 | `bias-metrics-job` | Defect-class accuracy gap per product/site | scheduled | inspection records | AI Platforms | R2 (Art. 10) |
| MOD-BIA-02 | `bias-baseline-store` | Baseline per model + product | Postgres | bias runner | AI Platforms | R2 |
| MOD-BIA-03 | `bias-mitigation-tracker` | Track bias-mitigation experiments | MLflow | — | AI Platforms | R2 |
| MOD-ROB-01 | `adversarial-pertubation-suite` | OQ adversarial-perturbation test | scheduled | challenge images | Security Architecture | R1 (Art. 15) |
| MOD-ROB-02 | `image-tamper-detection` | Image checksum verify at inference | inline | MOD-LBL-04 | Security | R1 |
| MOD-ROB-03 | `model-tamper-detection` | Cosign verify at load | inline | Sigstore | Security | R1 |
| MOD-ROB-04 | `runtime-drift-monitor` | Image-distribution drift per shift | scheduled | Prometheus + offline | AI Platforms | R1 |
| MOD-DEF-01 | `data-egress-policy` | Image-data egress restrictions | NetworkPolicy | K8s | Security | R2 |
| MOD-DEF-02 | `inversion-defence` | Output-strip / no class-prob disclosure | inline | per-BBE policy | Security | R2 |
| MOD-DEF-03 | `rate-limit` | Per-consumer rate-limit | Kong | Kong | Security | R2 |
| MOD-DEF-04 | `dp-evaluation-record` | DP-SGD evaluation result in Annex IV | scheduled | training records | AI Platforms | R2 |
| MOD-SEC-01 | `vault-secrets-manager` | Per-station + per-model secrets | Vault | Vault | Security | R1 |
| MOD-SEC-02 | `image-encryption-at-rest` | AES-256 image storage | S3 + KMS | KMS | Security | R1 |
| MOD-SEC-03 | `cluster-hardening` | CIS Kubernetes Benchmark (current release at site deployment) + kube-bench | CI + cron | K8s | Security | R1 |
| MOD-SEC-04 | `network-policy` | Default-deny + explicit allow | NetworkPolicy | K8s | Security | R1 |
| MOD-SEC-05 | `vulnerability-scan` | Trivy + Snyk on every image | CI | Trivy | Security | R1 |
| MOD-211-01 | `211.68-automatic-equipment` | Automatic-equipment qualification record | REST | MOD-AUD-* | Validation IT | R1 |
| MOD-211-02 | `211.22-qcu-responsibility` | QCU sign-off workflow on release | REST | MOD-AUD-* | QCU | R1 |
| MOD-211-03 | `211.110-sampling-rules` | In-process sampling tie-in (where applicable) | REST | MES PAS-X | Validation IT | R2 |
| MOD-211-04 | `211.192-record-review` | EBR review workflow | REST | MES PAS-X | QCU | R1 |
| MOD-AN1-01 | `annex1-8123-handler` | Annex 1 § 8.123 100%-visible-particulate compliance handler | inline | per-BBE | Validation IT | R1 |
| MOD-USP-01 | `usp-790-zone-handler` | USP <790> zone-of-rejection encoder | per-BBE | — | Validation IT | R1 |
| MOD-USP-02 | `usp-787-handler` | USP <787> sub-visible 5-50 μm cross-ref (where applicable) | — | other instruments | Validation IT | R2 |
| MOD-USP-03 | `usp-788-handler` | USP <788> sub-visible 10-25 μm cross-ref | — | other instruments | Validation IT | R2 |
| MOD-PERF-01 | `latency-slo` | P95 ≤ 50 ms decision latency to PLC | Prometheus | — | Edge Ops | R1 (line throughput) |
| MOD-BAK-01..03 | `backup-suite` | Per AUR-FS-BACKUP-001 cross-system | — | Aurora | Edge Ops | R2 |
| MOD-PMM-01 | `pmm-service` | Post-market monitoring (Art. 72) | scheduled | inspection records | Reg-Affairs IT | R1 |
| MOD-PMM-02 | `pmm-quarterly-report` | Quarterly PMM | scheduled | MOD-PMM-01 | Reg-Affairs IT | R2 |
| MOD-QMS-01 | `qms-bridge` | ServiceNow + MasterControl bridge | REST + Kafka | ServiceNow, MasterControl | QMS Ops | R2 |
| MOD-QMS-02 | `change-control-gate` | All model + BBE changes require CR | REST | MOD-QMS-01 | QMS Ops | R1 |
| MOD-PR-01 | `periodic-review-orchestrator` | Annual per-product review | scheduled | all sources | Validation IT | R2 |
| MOD-PR-02 | `pccp-annual-review-orchestrator` | Annual PCCP review | scheduled | MOD-PCCP-04 | Reg-Affairs IT | R2 |
| MOD-PR-03 | `classification-reassessment` | Annex I vs III reassessment | scheduled | per-product | Reg-Affairs IT | R1 |
| MOD-TRN-01 | `okta-lms-connector` | Inspector access gated by LMS | webhook | Okta, LMS | IAM | R2 |
| MOD-TRN-02 | `inspector-competency` | Inspector competency record | scheduled | LMS | QCU | R1 |
| MOD-PART11-01..11 | `part11-control-suite` | Part 11 sub-section controls | library | Okta + MFA | Validation IT | R1 |
| MOD-DI-01..07 | `alcoa-plus-suite` | ALCOA+ implementation | inline | MOD-AUD-* | Validation IT | R1 |

## 6. Data Model Design

### 6.1 Image schema

```sql
CREATE TABLE image (
  image_id           UUID         PRIMARY KEY,
  station_id         TEXT         NOT NULL,
  camera_id          TEXT         NOT NULL,
  batch_id           TEXT         NOT NULL,
  product_id         TEXT         NOT NULL,
  bbe_version        TEXT         NOT NULL,
  unit_serial        TEXT         NOT NULL,
  raw_image_uri      TEXT         NOT NULL,    -- S3 `tes-inspection-raw/`
  processed_image_uri TEXT,
  sha256             CHAR(64)     NOT NULL,
  acquisition_ts     TIMESTAMPTZ  NOT NULL,
  exposure_us        INTEGER,
  light_back_pct     INTEGER,
  light_side_pct     INTEGER
);
```

### 6.2 Label schema (training + reference)

```sql
CREATE TABLE label (
  label_id           UUID         PRIMARY KEY,
  image_id           UUID         REFERENCES image,
  annotator_id       TEXT         NOT NULL,
  defect_class       TEXT         NOT NULL,    -- e.g. 'fibre', 'glass-fragment', 'cosmetic'
  bbox               BOX,                       -- (x1,y1,x2,y2)
  mask_uri           TEXT,
  annotation_ts      TIMESTAMPTZ  NOT NULL,
  reviewer_id        TEXT,
  consensus          BOOL         NOT NULL DEFAULT false
);
```

### 6.3 Inference record

```sql
CREATE TABLE inference_record (
  request_id         UUID         PRIMARY KEY,
  image_id           UUID         REFERENCES image,
  model_id           UUID         NOT NULL,
  model_version      TEXT         NOT NULL,
  yolo_output_json   JSONB        NOT NULL,
  sam_output_json    JSONB,
  classifier_output_json JSONB    NOT NULL,
  zone_decisions_json JSONB       NOT NULL,
  confidence         NUMERIC(5,4) NOT NULL,
  decision           TEXT         NOT NULL CHECK (decision IN ('ACCEPT','REJECT','HUMAN_REVIEW')),
  fallback_used      BOOL         NOT NULL DEFAULT false,
  human_review_id    UUID,
  plc_signal_sent_ts TIMESTAMPTZ,
  latency_ms         INTEGER      NOT NULL,
  timestamp_iso8601  TIMESTAMPTZ  NOT NULL DEFAULT now()
);
```

### 6.4 Audit events (identical pattern; append-only)

```sql
CREATE TABLE audit_events (
  event_id           BIGSERIAL    PRIMARY KEY,
  actor_id           TEXT         NOT NULL,
  batch_id           TEXT,
  station_id         TEXT,
  action             TEXT         NOT NULL,
  old_value          JSONB,
  new_value          JSONB,
  reason_for_change  TEXT,
  signature_id       UUID,
  timestamp_iso8601  TIMESTAMPTZ  NOT NULL DEFAULT now(),
  integrity_hash_sha256 CHAR(64)  NOT NULL
);
CREATE OR REPLACE RULE audit_events_no_update AS ON UPDATE TO audit_events DO INSTEAD NOTHING;
CREATE OR REPLACE RULE audit_events_no_delete AS ON DELETE TO audit_events DO INSTEAD NOTHING;
```

### 6.5 PCCP record

Same as Lyrae DS § 6.2 schema (MoP / PCEM / IA / envelope_yaml per FDA Aug 2025).

### 6.6 Art. 73 incident

Same as Lyrae DS § 6.6.

### 6.7 Per-product BBE schema

```sql
CREATE TABLE bbe (
  bbe_id             UUID         PRIMARY KEY,
  product_id         TEXT         NOT NULL,
  bbe_version        TEXT         NOT NULL,
  state              TEXT         NOT NULL CHECK (state IN ('DRAFT','APPROVED','EFFECTIVE','RETIRED')),
  rois_json          JSONB        NOT NULL,           -- ROI crops
  zones_json         JSONB        NOT NULL,           -- zone-of-rejection (USP <790>)
  light_settings_json JSONB       NOT NULL,
  defect_class_thresholds_json JSONB NOT NULL,        -- per-class confidence
  fallback_policy_json JSONB,                         -- when to use Cognex
  knapp_kushner_pod_target NUMERIC(5,4) NOT NULL,     -- USP <1790> POD target
  approved_by        TEXT,
  approved_at        TIMESTAMPTZ
);
```

### 6.8 Data classification + retention

| Class | Examples | Retention | Storage |
|---|---|---|---|
| GxP audit | `audit_events` | ≥ 25 y | Splunk + S3 |
| Inspection record (R1) | `inference_record` | ≥ 25 y | S3 Object Lock |
| Image (R1 reject) | rejected-unit images | ≥ 25 y (Annex 1 retention) | S3 Object Lock |
| Image (accept) | accepted-unit images | ≥ 2 y (per-batch RA decision) | S3 lifecycle |
| Label data | training labels | indefinite | S3 versioned |
| BBE | per-product config | indefinite during product lifetime + ≥ 10 y after | S3 + Postgres |
| Annex IV pack | per-model | ≥ 10 y from market placement | S3 Object Lock + Glacier Vault Lock |
| PCCP record | per-model | ≥ 10 y | S3 Object Lock |
| Art. 73 incident | per-incident | ≥ 10 y | S3 Object Lock |

## 7. Algorithm + Calculation Design

### 7.1 Defect-detection inference pipeline

```
on frame_acquired(image):
  image = de_bayer(image)
  image = roi_crop(image, bbe.rois_json)
  image = normalise(image)
  bboxes = yolo_detect(image, model.yolo)
  masks = sam_segment(image, bboxes, model.sam)
  classes = defect_classify(bboxes, masks, model.classifier)
  decisions_per_zone = zone_of_rejection_logic(
    masks, classes, bbe.zones_json, bbe.defect_class_thresholds_json)
  if any zone classifies REJECT and confidence > threshold:
    decision = REJECT
  elif borderline (confidence in [low, high] band):
    if bbe.fallback_policy_json.allow_fallback:
      cognex_result = classical_cv_fallback(image, bbe)
      decision = decision_fuser(yolo+sam result, cognex_result)
    else:
      decision = HUMAN_REVIEW
  else:
    decision = ACCEPT
  emit plc_signal(decision)
  write inference_record + audit_event
```

### 7.2 Zone-of-rejection logic per USP <790> + per-BBE

For each defect mask: compute centroid relative to container geometry. Look up `bbe.zones_json[zone_id]` for centroid-zone match. Each zone has `defect_classes_allowed[]` and `min_size_um` threshold. A defect inside a forbidden zone OR exceeding size threshold → REJECT classification per USP <790>. USP <790> says zero tolerance for visible particulates in injectable products; the zone definition implements per-container-geometry adaptation.

### 7.3 Knapp-Kushner Probability of Detection (POD) — challenge-set validation

Per USP <1790>, validation set comprises:

- Known-good units (clear; reference standard);
- Known-defect units (calibrated particulates 50-100 μm, 100-200 μm, 200-400 μm, 400-800 μm, > 800 μm; multiple defect classes);
- Borderline units (statistically-validated borderline POD set).

For each unit in the challenge set, calculate POD = TP/(TP+FN). Compare per-defect-size POD to baseline. Pass criterion: POD per defect-size class ≥ baseline POD; overall system POD ≥ trained human inspector POD by ≥ 2 percentage points (per PDA TR 79 + USP <1790> guidance).

Pseudocode:

```
def knapp_kushner_validate(challenge_set, model):
  results = []
  for unit in challenge_set:
    pred = inference_pipeline(unit.images, model)
    actual = unit.label  # ground truth
    results.append((actual, pred, unit.defect_size_class))
  per_class_pod = compute_per_class_pod(results)
  overall_pod = compute_overall_pod(results)
  return ValidationResult(per_class_pod, overall_pod, pass=all(per_class_pod >= baseline))
```

### 7.4 Confidence-threshold gate

Per defect-class threshold from `bbe.defect_class_thresholds_json`. Examples (illustrative): `glass-fragment`: 0.92 (high — false-reject acceptable); `fibre`: 0.95; `cosmetic`: 0.85 (lower — false-reject = waste). Below threshold → HUMAN_REVIEW.

### 7.5 Decision-fuser algorithm

```
def decision_fuser(dl_result, cv_result, policy):
  if dl_result.decision == REJECT or cv_result.decision == REJECT:
    return REJECT   # any-reject wins (Annex I conservative)
  if dl_result.decision == ACCEPT and cv_result.decision == ACCEPT:
    return ACCEPT
  return HUMAN_REVIEW
```

Conservative semantics: any-reject wins per Annex I + USP <790> zero-tolerance.

### 7.6 PCCP predicate engine

Identical to Lyrae DS § 7.5 — model-update conformance against envelope_yaml.

### 7.7 Art. 73 clock arithmetic

Identical to Lyrae DS § 7.6.

### 7.8 Image-tamper detection

SHA-256 over canonical image bytes; verified at every stage (acquisition → S3 → MLflow-attached training → re-load for inference). Mismatch → ALERT + HALT line.

### 7.9 Cosign model verification

```
on model_load:
  artefact = fetch(model_uri)
  verify_cosign_signature(artefact, trusted_root) or raise MODEL_TAMPER
  load model into ONNX Runtime
  emit audit MODEL_LOADED
```

### 7.10 Bias-metrics per product / per line / per shift

Per-product accuracy gap, FP rate, FN rate; per-shift FN rate analysis. Gap > 5 pp triggers experiment.

### 7.11 Runtime drift detection

Image statistics (mean luminance, contrast, sharpness, dust-load) compared rolling-shift-vs-baseline. Drift > 10% → alert + line review.

## 8. Interface + API Design

| Endpoint | Method | Path | AuthN | Request | Response | Rate limit | Errors | Audit |
|---|---|---|---|---|---|---|---|---|
| Inference (edge ingress) | POST | `/inspect/{station_id}` | mTLS (per-station cert) | image bytes + metadata | `Decision`(`ACCEPT`/`REJECT`/`HUMAN_REVIEW`) + record_id | line throughput | 400, 422, 503 | INSPECTION_RECORDED |
| HumanReview decision | POST | `/humanreview/{record_id}/{decision}` | OAuth2 + Inspector group | `{reason: string}` | `HumanReviewRecord` | 100/h/reviewer | 400 | HUMAN_REVIEW_RECORDED |
| BBE register | POST | `/bbe` | OAuth2 + Product Eng + QA | `BBERequest` | `BBE` | 5/d | 400, 403 | BBE_REGISTERED |
| BBE approve | POST | `/bbe/{id}/approve` | OAuth2 + QCU | — | `BBE` | 5/d | 400, 403 | BBE_APPROVED |
| Model register | POST | `/model` | OAuth2 + AI Platforms | `ModelRequest` | `Model` | 5/d | 400 | MODEL_REGISTERED |
| Model promote | POST | `/model/{id}/promote` | OAuth2 + 2 JWTs (Author ≠ Approver) + cosign | `PromoteRequest` | `Model` | 5/d | 400, 403, 422 PCCP | MODEL_PROMOTED |
| Model rollback | POST | `/model/{id}/rollback` | OAuth2 + HO group | `{reason: string}` | `Model` | 10/d | 400, 403 | MODEL_ROLLBACK |
| Challenge-set run | POST | `/challenge/{model_id}` | OAuth2 + Validation IT | `ChallengeSetRunRequest` | `ChallengeSetResult` | 5/d | 400 | CHALLENGE_RUN |
| Annex IV export | POST | `/model/{id}/annex4/export` | OAuth2 + Reg-Affairs | — | `{zip_url, manifest_sha256}` | 5/d | 400 | ANNEX4_EXPORTED |
| Art. 73 incident | POST | `/incident` | OAuth2 (HO or QCU) | `IncidentRequest` | `IncidentRecord` | 100/h | 400 | INCIDENT_RECORDED |
| EU AI DB register | POST | `/eu-aidb/{model_id}` | OAuth2 + Reg-Affairs | `EUAIDBRequest` | `{entry_id, date}` | 5/d | 400 | EUAIDB_REGISTERED |
| EBR feed (MES PAS-X) | POST | `/ebr/{batch_id}` | mTLS (MES integration cert) | `EBRPayload` | `Ack` | per-batch | 400 | EBR_FED |
| Audit export | GET | `/audit/export?from=&to=&format=` | OAuth2 + Audit-Readers | — | streaming | 1/h | 400 | AUDIT_EXPORTED |
| Bias report | GET | `/bias/{model_id}/{q}` | OAuth2 + Reg-Affairs | — | `BiasReport` | 100/h | 404 | — |
| HO Operator dashboard | GET | `/ho/dashboard-data` | OAuth2 + HO group | — | dashboard JSON | 100/h | 403 | — |
| Drift status | GET | `/drift/{model_id}/{station_id}` | OAuth2 | — | drift JSON | 100/h | 404 | — |

TLS 1.3; mTLS service-to-service; per-station mTLS for edge ingress.

## 9. Security Design

### 9.1 AuthN

Okta SAML 2.0 + MFA (FIDO2 phishing-resistant for `cv-prod-approvers`). Per-station mTLS for edge ingress. Service-to-service mTLS via Istio.

### 9.2 AuthZ

RBAC: `inspector` (HumanReview only), `qcu`, `product_eng`, `ai_platforms`, `ho_operator`, `reg_affairs`, `validation_it`, `inspector_readonly`. LMS-gated provisioning.

### 9.3 Secrets

Vault: per-station mTLS cert, MES PAS-X integration cert, model-signing cosign key (HSM-backed, 90-d rotation), Sigstore keys.

### 9.4 Transport security

TLS 1.3 + mTLS. Image-storage AES-256 at rest. SBOM CycloneDX 1.6 attached to every container + model. Trivy CI scan blocks HIGH + CRITICAL.

### 9.5 Model + Image tamper protection

- Cosign signature verify on model load (MOD-ROB-03).
- SHA-256 image checksum verify on every stage transition (MOD-ROB-02, MOD-LBL-04).
- Tampering → ALERT + halt line + Art. 73 incident open (if patient-safety impact).

### 9.6 Network segmentation

Factory L2 VLAN isolation; out-of-band SCADA VLAN; NetworkPolicy `default-deny-all`; PLC interface only allowed from inference-edge namespace.

### 9.7 Adversarial-input protection

- OQ adversarial-perturbation suite per model (MOD-ROB-01) per FS-ROB-01..04.
- Runtime image-statistics anomaly (MOD-ROB-04).
- Output-strip on probe pattern (MOD-DEF-02).

## 10. Deployment Architecture

### 10.1 Edge topology

- 4 × inspection stations × 1 Jetson AGX Orin per station (DRC GPU mode locked, driver pinned via `pylon-failover` DaemonSet).
- Each station: 3 × Basler ace U cameras (back-light + side-light + reference).
- Reject station with Siemens S7-1500 PLC.
- HumanReview kiosks (4 × per line).

### 10.2 Factory K8s cluster

- 3 control-plane nodes + 6 worker nodes (factory-floor on-prem).
- Pod Security Standards `restricted`.
- NetworkPolicy `default-deny-all` + explicit allow.
- CIS Kubernetes Benchmark (current release at site deployment); kube-bench in CI.
- HPA disabled on inspection-deployment (deterministic-load).

### 10.3 Observability

- Prometheus + Grafana + Loki on cluster.
- Per-station metrics: `inspection_latency_seconds`, `reject_rate`, `human_review_rate`, `image_acquisition_failures`, `model_confidence_below_threshold`, `tensorrt_engine_loaded`, `plc_handshake_errors`.
- Splunk Universal Forwarder `tes-cv-audit` + `tes-cv-inspection`.

### 10.4 DR + retention

- RTO ≤ 1 h (line-stop costly); RPO ≤ 15 min.
- Annual DR drill per Aurora cross-system.
- S3 Object Lock for inspection records ≥ 25 y; Annex IV ≥ 10 y; PCCP ≥ 10 y.

### 10.5 CI/CD

GitLab + ArgoCD. Signed commits + cosign + SBOM. Per-model CI: training reproducibility verify + adversarial-perturbation OQ + challenge-set baseline check.

## 11. Module Specification Table

(Excerpt — ~120 modules in total)

| Module ID | File path | Class | Unit-test | Module Spec |
|---|---|---|---|---|
| MOD-ML-01 | `services/inference/yolo.py` | `YOLODetector` | `tests/test_yolo.py` | TES-MS-CV-YOLO-001 |
| MOD-ML-02 | `services/inference/sam.py` | `SAMSegmenter` | `tests/test_sam.py` | TES-MS-CV-SAM-001 |
| MOD-ML-05 | `services/inference/zone_logic.py` | `ZoneOfRejectionLogic` | `tests/test_zone.py` | TES-MS-CV-ZONE-001 |
| MOD-CHAL-01 | `services/challenge/runner.py` | `ChallengeSetRunner` | `tests/test_challenge.py` | TES-MS-CV-CHAL-001 |
| MOD-PCCP-01 | `services/pccp/engine.py` | `PCCPPredicateEngine` | `tests/test_pccp.py` | TES-MS-CV-PCCP-001 |
| MOD-INF-03 | `services/plc/handshake.py` | `PLCHandshake` | `tests/test_plc.py` | TES-MS-CV-PLC-001 |
| MOD-INF-04 | `services/plc/reject_actuator.py` | `RejectActuator` | `tests/test_actuator.py` | TES-MS-CV-ACTUATOR-001 |
| MOD-HUM-01 | `services/ho/operator_ui.py` | `HOOperatorUI` | `tests/test_ho.py` | TES-MS-CV-HOUI-001 |
| MOD-HUM-02 | `services/ho/humanreview_station.py` | `HumanReviewKiosk` | `tests/test_kiosk.py` | TES-MS-CV-KIOSK-001 |
| MOD-INC-01 | `services/incident/art73.py` | `Art73IncidentService` | `tests/test_incident.py` | TES-MS-CV-INC-001 |
| MOD-AUD-04 | `services/ebr/feeder.py` | `EBRFeeder` | `tests/test_ebr.py` | TES-MS-CV-EBR-001 |
| MOD-USP-01 | `services/usp/usp_790.py` | `USP790Handler` | `tests/test_usp_790.py` | TES-MS-CV-USP-001 |
| MOD-AN1-01 | `services/annex1/handler.py` | `Annex1_8123Handler` | `tests/test_annex1.py` | TES-MS-CV-AN1-001 |
| MOD-211-04 | `services/cfr211/record_review.py` | `CFR211_192Handler` | `tests/test_211_192.py` | TES-MS-CV-211-001 |
| (… plus ~110 more) | (…) | (…) | (…) | (…) |

## 12. References

**US**
- 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300
- **21 CFR Part 211 §§ .22 (QCU), .68 (automatic equipment), .110 (sampling), .192 (record review)**
- FDA AI/ML SaMD Action Plan (2021)
- FDA GMLP (2021)
- FDA PCCP (Aug 2025)
- FDA CSA (Feb 2026)
- NIST AI RMF 1.0; NIST SP 800-218 SSDF
- USP **<1> Injections — General Notices**, **<787> Subvisible Particulate Matter in Therapeutic Protein Injections**, **<788> Particulate Matter in Injections**, **<790> Visible Particulates in Injections**, **<1790> Visual Inspection of Injections**

**EU**
- EU AI Act 2024/1689 Arts. 8–21, 26, 43, 47–49, 50 (transparency to natural persons — AI-generated content labelling), 72, 73, 99, 113 + Annex I (2027)
- **EU GMP Annex 1 (2022 revision) — Manufacture of Sterile Medicinal Products, esp. § 8.123 (100% visible-particulate inspection)**
- EU GMP Annex 11
- EU GMP Annex 22 (DRAFT)
- EU MDR Reg. 2017/745 (where output supports MDR class IIa+)
- **Ph. Eur. 2.9.20 — Particulate contamination — visible particles**
- GDPR Reg. (EU) 2016/679 Arts. 32, 35

**International**
- ICH Q9(R1)
- IEC 62304:2006+A1:2015
- IEC 81001-5-1:2021
- ISO/IEC 42001:2023 (AI MS)
- ISO 14971:2019
- ISO/IEC 27001:2022
- **PDA Technical Report 79 — Visible Particulate Inspection**
- ISPE GAMP 5 (2nd ed., 2022); GAMP GPG *AI/ML in GxP* (2024)
- OWASP ASVS v5.0; NIST SP 800-218 SSDF

**DACH**
- BfArM (DE), Swissmedic (CH), AGES (AT)
- BSI IT-Grundschutz

**Vendor**
- Basler — *ace U Series Hardware + Pylon SDK 8.0 Documentation*
- NVIDIA — *Jetson AGX Orin Developer Guide; TensorRT 10 Documentation*
- ONNX Runtime documentation (v1.20)
- PyTorch documentation (v2.4)
- Werum / Körber MES PAS-X V5.x documentation
- Siemens S7-1500 + TIA Portal documentation
- Cognex VisionPro 10 documentation
- MLflow, Vault, Sigstore documentation

## 13. Appendix A — DS → FS Traceability Matrix

| DS ID / Module | FS ID |
|---|---|
| MOD-IMG-01 | FS-IMG-01 |
| MOD-IMG-02 | FS-IMG-02 |
| MOD-IMG-03 | FS-IMG-03 |
| MOD-HW-01..05 | FS-HW-01..05 |
| MOD-PRE-01..03 | (image pipeline) |
| MOD-ML-01..08 | FS-ML-01..08 |
| MOD-OPT-01..04 | FS-OPT-01..04 |
| MOD-DEV-01..07 | FS-DEV-01..07 |
| MOD-INF-01..05 | FS-INF-01..05 |
| MOD-AUD-01..05 | FS-AUD-01..05 |
| MOD-LBL-01..05 | FS-LBL-01..05 |
| MOD-CHAL-01..04 | FS-CHAL-01..04 |
| MOD-PCCP-01..04 | FS-PCCP-01..04 |
| MOD-TD-01..03 | FS-TD-01..03 |
| MOD-CONF-01..04 | FS-CONF-01..04 |
| MOD-REG-01 | FS-REG-01 |
| MOD-HUM-01..03 | FS-HUM-01..03 |
| MOD-INC-01..03 | FS-INC-01..03 |
| MOD-BIA-01..03 | FS-BIA-01..03 |
| MOD-ROB-01..04 | FS-ROB-01..04 |
| MOD-DEF-01..04 | FS-DEF-01..04 |
| MOD-SEC-01..05 | FS-SEC-01..05 |
| MOD-211-01..04 | FS-211-01..04 |
| MOD-AN1-01 | FS-AN1-01 |
| MOD-USP-01..03 | FS-USP-01..03 |
| MOD-PERF-01 | FS-PERF-01 |
| MOD-BAK-01..03 | FS-BAK-01..03 |
| MOD-PMM-01..02 | FS-PMM-01..02 |
| MOD-QMS-01..02 | FS-QMS-01..02 |
| MOD-PR-01..03 | FS-PR-01..03 |
| MOD-TRN-01..02 | FS-TRN-01..02 |
| MOD-PART11-01..11 | FS-PART11-01..11 |
| MOD-DI-01..07 | FS-DI-01..07 |
| DS-AV-01 | FS-AV-01 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| MOD-INT-AD-01 | FS-INT-AD-01 |
| MOD-INT-EQMS-01 | FS-INT-EQMS-01 |
| MOD-INT-LMS-01 | FS-INT-LMS-01 |
| MOD-INT-LYR-01 | FS-INT-LYR-01 |
| MOD-INT-MES-01 | FS-INT-MES-01 |
| MOD-INT-PLC-01 | FS-INT-PLC-01 |

**Coverage footnote.** 124 of 131 FS-IDs covered. Vendor-internal FS-IDs not designed at site level: Basler firmware, Jetson driver, ONNX Runtime kernel, Cognex job-internal jobs, MES PAS-X scheduler primitives, Siemens S7 firmware, TensorRT compiler internals.

## 14. Design-level Risk Register

| ID | Design-stage risk | Likelihood | Impact | Bound modules | Mitigation |
|---|---|---|---|---|---|
| D-01 | **EU AI Act Annex I non-conformance at notified-body inspection** | Medium | **Critical (Art. 99: up to €15M / 3% turnover)** | MOD-TD-01..03, MOD-CONF-01..04 | Annex IV pack template + CI completeness check + annual periodic review |
| D-02 | **USP <790> visible-particulate false-negative** — contaminated unit released to patient | Low | **Critical (patient safety + Art. 99)** | MOD-ML-01..08, MOD-CHAL-01..04 | Quarterly Knapp-Kushner POD re-validation; per-defect-class conservative thresholds; classical-CV fallback (DS-ML-06); HumanReview default for borderline |
| D-03 | **EU GMP Annex 1 § 8.123 100%-inspection coverage gap** — image-acquisition failure not detected | Low | **Critical** | MOD-HW-04 (`pylon-failover`), MOD-INF-03 PLC | Pylon-failover halts line on camera disconnect; PLC handshake timeout halts line |
| D-04 | **Art. 14 human-oversight insufficiency** — HumanReview kiosk down at borderline-decision rate spike | Low | **Critical (Art. 99)** | MOD-HUM-02 | Kiosk redundancy + line-stop policy |
| D-05 | **Art. 73 incident clock missed** (15/10/2 d) | Low | **Critical** | MOD-INC-01..02 | UTC clock + cron + D-3/D-1/D0 alerts |
| D-06 | **PCCP envelope misconfiguration** | Medium | High | MOD-PCCP-01 | Annual review + unit-tested examples |
| D-07 | **Substantial-modification Art. 43(4) trigger missed** | Low | **Critical** | MOD-CONF-04 | PCCP engine + change-control gate |
| D-08 | **Cosign signing-key compromise** | Low | High | Vault | HSM-backed + 90-d rotation + audit |
| D-09 | **DB-trigger bypass for `audit_events`** | Low | **Critical** | MOD-AUD-01 | DB-role enforcement |
| D-10 | **Sigstore outage during model deploy** | Low | High | MOD-ROB-03 | Cached trusted-root |
| D-11 | **PLC handshake failure** during reject-trigger window — contaminated unit not rejected | Low | **Critical (patient safety)** | MOD-INF-03 | Watchdog + line-stop on handshake timeout |
| D-12 | **TensorRT engine drift** on driver bump — silent numerical change | Low | High | MOD-OPT-01 | Bitwise-reproducibility OQ on each driver/runtime bump |
| D-13 | **Annex IV pack template drift** between releases | Medium | High | MOD-TD-01 | Template version-pin per release + CI check |
| D-14 | **Knapp-Kushner POD baseline drift** undetected | Medium | **Critical** | MOD-CHAL-01..04 | Quarterly re-validation; tight delta thresholds |
| D-15 | **Defect-class confidence-threshold mis-tune** for new product | Medium | High | MOD-ML-04 | OQ per BBE; product-engineering sign-off |
| D-16 | **Camera bad-pixel drift** masked as defect → false-reject (waste) or hides real defect | Medium | High | MOD-HW-05 | Daily bad-pixel map + OQ baseline |
| D-17 | **Network outage** between Jetson and factory K8s control plane — line continues without control-plane oversight | Medium | Medium | MOD-INF-01..02 | Local audit-buffer + automatic resync; line-stop on extended outage |
| D-18 | **Cross-system Lyrae off-line eval drift** vs on-edge | Low | High | MOD-INT-LYR-01 | Periodic alignment check |
| D-19 | **Cross-system Aurora Backup misses S3-object-lock retention** transition | Low | High | DS-XSYS-BAK-01 | Monthly restore drill + retention monitor |
| D-20 | **MES PAS-X EBR feeder lag** > 60 s causes batch-release delay | Medium | Medium | MOD-AUD-04 | Kafka back-pressure handling |
| D-21 | **GDPR — no PII in images** (units only) but inspector identity is PII | Low | Medium | Audit + LMS | Inspector-id audit covered by audit_events; LMS data per LMS DPIA |
| D-22 | **Image-tamper detection** bypass via raw filesystem write | Low | **Critical** | MOD-ROB-02 | Filesystem audit + S3-write-only IAM + per-frame SHA-256 |
| D-23 | **Splunk frozen-index 25-y retention** cost overrun | Low | High | Observability | Annual storage-cost review |
| D-24 | **Adversarial-perturbation OQ suite drift** under model evolution | Medium | High | MOD-ROB-01 | Annual suite update + drift detection |
| D-25 | **EU AI DB registration lag** — model live without Art. 49 entry | Low | **Critical (Art. 49)** | MOD-REG-01 | Registration gate before EFFECTIVE state |
| D-26 | **Classical-CV fallback (Cognex) drift** breaks fusion semantics | Low | High | MOD-ML-06, MOD-ML-07 | OQ regression on Cognex job updates |
| D-27 | **LMS competence lapse** blocks legitimate inspector at HumanReview rate spike | Low | High | MOD-TRN-01 | D-30 / D-7 LMS lapse alert; staffing model |
| D-28 | **DR drill** misses an inspection station | Low | High | MOD-RES-01-equivalent | Per-station rotation in DR checklist |
| D-29 | **Cosign trusted-root rotation** breaks model-loading at production cutover | Low | **Critical** | Vault + Sigstore | Staged rotation + canary verify |
| D-30 | **Bias-metrics gap report** misses small-N defect class | Medium | High | MOD-BIA-01 | Minimum-sample-size guard + escalation |
| D-31 | **Periodic-review orchestrator** fails to capture a new mandatory field after EU AI Act amendment | Low | High | MOD-PR-01 | Annual orchestrator-template review |
| D-32 | **Foundation-model-ingest signature skip** during pressure | Low | **Critical** | MOD-ROB-03 | CI gate + no manual override |
| D-33 | **Per-station mTLS cert rotation** missed before expiry | Low | **Critical** | MOD-SEC-01 | Cert-expiry monitor D-30 alert |
| D-34 | **Inspector-kiosk session-hijack** | Low | High | MOD-PART11-* | Re-auth on every HumanReview decision (OAuth2 max-age 5 min) |
| D-35 | **PCCP annual review** misses a regulatory update | Low | High | MOD-PR-02 | Annual checklist mapped to current FDA Aug 2025 PCCP guidance |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
