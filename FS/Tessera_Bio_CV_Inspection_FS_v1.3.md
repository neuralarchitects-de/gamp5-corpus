---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; rewritten 2026-05-12 Wave 3 Chunk I (Annex I 2027 re-classification + URS-ID alignment + per-ID rows + T3 depth uplift)"
seed_corpus_basis:
  - "TES-URS-CV-001 v1.2"
  - "GAMP 5 (2nd ed., 2022) Cat 5"
  - "21 CFR Part 11; 21 CFR Part 211"
  - "EU GMP Annex 11; EU GMP Annex 1 (2022)"
  - "EU AI Act 2024/1689 Annex I high-risk"
  - "USP <790>/<1790>"
  - "FDA AI/ML SaMD; FDA GMLP (2021); FDA PCCP (Aug 2025); FDA CSA (Feb 2026)"
parent_urs:
  document_number: TES-URS-CV-001
  version: 1.2
  file: ../../URS/_generated/final/Custom_Computer_Vision_Inspection_System__Tessera_Bio_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# Functional Specification (FS)

## Custom Computer Vision Inspection System — Site-Developed Python + PyTorch + Basler Cameras + NVIDIA Jetson

**Document Number:** TES-FS-CV-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** TES-URS-CV-001 v1.2 | **Site:** Tessera Bio Manufacturing GmbH, Sterile Fill-Finish Plant 1, Mannheim, Germany *(fictional)*
**System Class:** GAMP Cat 5 — Custom Application (with site-developed CV / DL models as Cat-5 sub-components)
**EU AI Act 2024/1689 classification:** **Annex I high-risk AI system** (safety component of medicinal-product release decision via Annex 1 §8.123 + USP <790>/<1790>). Deadline **2 August 2027**.
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .22, .68, .110, .192; EU GMP Annex 11; EU GMP Annex 1 (2022); EU AI Act 2024/1689 Arts. 8–21, 26, 43, 47, 48, 49, 72, 73, 99, 113; USP <1>, <787>, <788>, <790>, <1790>; Ph. Eur. 2.9.20; FDA AI/ML SaMD Action Plan; FDA GMLP (2021); FDA PCCP (Aug 2025); FDA CSA (Feb 2026); ISPE GAMP GPG *AI/ML in GxP* (2024); ISO 14971:2019; ISO/IEC 42001:2023; PDA TR 79.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Vision Engineering Lead) | _____________ | _____________ | _____ |
| Reviewer (Quality Inspection SME) | _____________ | _____________ | _____ |
| Reviewer (Reg-Affairs — AI/ML) | _____________ | _____________ | _____ |
| Reviewer (Conformity Assessment Coordinator) | _____________ | _____________ | _____ |
| Approver (Head of Sterile Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |
| Approver (Qualified Person) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-12 | (synthetic) | Doc-number prefix correction (TSR → TES) + URS-ID alignment (URS-INSP → URS-INF). |
| 1.2 | 2026-05-12 | (synthetic) | Wave 3 Chunk I rewrite: parent URS upgraded to v1.2. EU AI Act re-classified Annex I (deadline 2027). Every URS-ID gets its own per-row FS specification (no range compression). New FS rows for URS-HW-05, URS-OPT-01..04, URS-ML-07/08, URS-DEF-01..04, URS-LBL-01..05, URS-BIA-01..03, URS-PCCP-01..04, URS-INF-05, URS-TD-01..03, URS-LOG-01..02, URS-CONF-01..04, URS-REG-01, URS-PMM-01..02, URS-INC-01..03, URS-DEP-01, URS-ROB-01..04, URS-QMS-01..02, URS-AUD-05, URS-PART11-06..11, URS-CHAL-01..04, URS-USP-01..03, URS-211-01..04, URS-INT-LYR-01, URS-INT-LMS-01, URS-DI-07, URS-DEV-07, URS-BAK-03, URS-HUM-01..03, URS-SEC-05, URS-TRN-02, URS-PR-02/03. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

Specify the site-developed CV inspection system to satisfy `TES-URS-CV-001` v1.2 — automated visual inspection of filled vials for particulates, fill-level, cosmetic defects — as an **Annex I high-risk AI system** under EU AI Act 2024/1689 (safety component of the medicinal-product release decision via Annex 1 + USP <790>/<1790>).

## 2. Scope

Site-developed Python services + PyTorch deep-learning models + Basler ace2 cameras + Effilux strobe lighting + NVIDIA Jetson AGX Orin edge compute; in-house ML pipeline (PyTorch training → ONNX → Triton Inference Server registered with the Lyrae AI/ML Model Server LYR-URS-MLSRV-001); integrations with the filling-line PLC (reject control), PAS-X MES (per-vial reject summary), MasterControl (deviations), site Okta SSO + MFA, HashiCorp Vault (secrets), site LMS (operator + inspector training records).

## 3. System Architecture

```
   Basler ace2 cameras (4×) ──► NVIDIA Jetson AGX Orin
   Effilux strobe lighting     │ ONNX runtime / Triton client
                               │ Output-hash + fail-safe Reject defaults
                               ▼
                   Site CV inference service (Python + FastAPI)
                   │ Pre/Post-processing (deterministic)
                   │ Confidence threshold gate
                   │ Decision audit-log writer
                   ▼
       ┌───────────────────────┴────────────────────────┐
       ▼                                                 ▼
   Filling-line PLC                            Lyrae ML Model Server (LYR-URS-MLSRV-001)
   (EtherNet/IP, mTLS, deflector control)      (Model registration, deployment, drift, audit,
       │                                        Annex IV pack, conformity, PMM, incident)
       ▼                                                 │
   Reject quarantine lane ─► Downstream 100%             ▼
   human visual inspection (Annex 1 §8.123)      MLflow + Splunk + S3 (Art. 18 cold archive)
       │
       ▼
   Werum PAS-X MES (per-batch reject summary, batch record per 21 CFR §211.192)
       │
       ▼
   MasterControl eQMS (deviations on reject-rate excursion)
```

## 4. Functional Specifications

| FS ID | URS ID | Specification |
|---|---|---|
| FS-HW-01 | URS-HW-01 | Inspection station: 4× Basler ace2 cameras (Mvix-LP optics) + Effilux STRA HP strobe lighting + NVIDIA Jetson AGX Orin 64GB; industrial enclosure IP54 cleanroom-suitable. |
| FS-HW-02 | URS-HW-02 | UPS sized for 30 min runtime; CV inference service implements `power_loss_detected → emit_reject_all` watchdog at <100 ms latency. |
| FS-HW-03 | URS-HW-03 | VLAN `vlan-fillfinish-cv` segregated from office; firewall rules deny office-to-VLAN; mTLS for any cross-VLAN traffic. |
| FS-HW-04 | URS-HW-04 | Daily start-up procedure runs camera-calibration on Mvix-LP pattern target; pass/fail recorded; failure blocks start. |
| FS-HW-05 | URS-HW-05 | Jetson firmware + JetPack version pinned via DaemonSet manifest in git; OQ revalidation suite runs against locked validation set on bump. |
| FS-OPT-01 | URS-OPT-01 | Camera+lighting IQ/OQ runs `optical_iq_oq.py`: measures uniformity (centre-vs-edge intensity within ±10%), focus (Sobel sharpness > threshold), absence of glare in inspection cone. |
| FS-OPT-02 | URS-OPT-02 | Per USP <1790> recommendation, backlight intensity 2,000–3,750 lux equivalent configured per-product in `recipes/{product_id}.yaml`. |
| FS-OPT-03 | URS-OPT-03 | Baseline-image hash recorded in `optical_baselines/{recipe_id}.json`; production start verifies hash matches; mismatch → re-qualify gate. |
| FS-OPT-04 | URS-OPT-04 | Daily Knapp-reference vial pass recorded in `start_of_day_check.log`; sensitivity-regression check blocks production start on failure. |
| FS-ML-01 | URS-ML-01 | Model card schema (markdown + JSON) per `model_card_template.md`: training data lineage, training script + git-tag, hyperparameters, training metrics, validation-set performance (sensitivity / specificity / FRR / FAR per class), known limitations. |
| FS-ML-02 | URS-ML-02 | Validation set in S3 `tes-validation-set/v{n}/` Object-Lock; not used in training (DB-enforced via training-pipeline contract); per-class size meets statistical-power plan recorded in `power_plan.md`. |
| FS-ML-03 | URS-ML-03 | Pareto-improvement gate `pareto_gate.py`: blocks promotion if FAR increase > 0 or FRR increase > 0.5 pp; default-tolerances overridable only by Reg-Affairs sign-off + Art. 43(4) assessment. |
| FS-ML-04 | URS-ML-04 | Joint-signature workflow: 3 signed JWTs (ML Reviewer + Head Sterile Mfg + Head QA) for in-envelope updates; 4 signed JWTs (+ Reg-Affairs AI/ML) for out-of-envelope. |
| FS-ML-05 | URS-ML-05 | Models cosign-signed pre-deployment; Triton model-repository pull verifies signature via Sigstore; verify-fail → reject load + alarm. |
| FS-ML-06 | URS-ML-06 | Drift monitor `drift_monitor.py`: 3 axes — data drift (image stats: brightness / contrast / focus distribution), concept drift (defect-rate vs reference batch), prediction drift (output distribution); alarms via `drift_alerts.yaml` thresholds. |
| FS-ML-07 | URS-ML-07 | Model registration via `lyrae_client.register_model(...)` against Lyrae AI/ML Model Server; Annex IV pack URL carried in MLflow record. |
| FS-ML-08 | URS-ML-08 | Retirement workflow: Lyrae registry state RETIRED → archival to S3 `tes-archive/` cold (10 y per Art. 18) + training records preserved indefinitely. |
| FS-DEF-01 | URS-DEF-01 | Defect-class library in `defect_classes_v{n}.yaml`: `visible_particulate`, `crack_glass`, `chipped_neck`, `fill_volume_low`, `fill_volume_high`, `stopper_misset`, `stopper_lifted`, `label_offaxis`, `label_missing`, `label_illegible`, `label_wrong_product`. |
| FS-DEF-02 | URS-DEF-02 | Per-class minimum-N statistical-power floor in `power_plan.md`; minority classes augmented per `data_augmentation_strategy.md`. |
| FS-DEF-03 | URS-DEF-03 | Class additions go through change-control PR; model-lifecycle re-run mandated; CI gate validates schema. |
| FS-DEF-04 | URS-DEF-04 | Annual defect-library review against published industry findings + recent regulator advisories; outcomes in `defect_library_review_{year}.md`. |
| FS-LBL-01 | URS-LBL-01 | Labelling tool `labeller-ui` enforces dual-blind: labeller A and labeller B see vial without each other's label; disagreement routes to labeller C adjudicator. |
| FS-LBL-02 | URS-LBL-02 | Inspector qualification recorded in LMS course `INSPECTOR-USP1790-QUAL`; enrolment includes vision exam + Knapp-test pass + per-defect-class training modules. |
| FS-LBL-03 | URS-LBL-03 | Cohen's κ computed per labelling campaign by `kappa_calc.py`; κ < 0.7 blocks campaign acceptance + triggers re-training workflow. |
| FS-LBL-04 | URS-LBL-04 | Dataset versioning: each campaign produces `dataset_v{n}.tar.gz` + SHA-256 + cosign signature; training-pipeline pins to dataset version + SHA. |
| FS-LBL-05 | URS-LBL-05 | Adjudication outcomes stored in `adjudications/` for calibration analytics; surfaced in inspector-calibration board. |
| FS-BIA-01 | URS-BIA-01 | Bias-evaluation report `bias_eval_{model_version}.md`: per-class + per-container-type + per-fill-volume + per-lighting-variant performance; representativeness metrics. |
| FS-BIA-02 | URS-BIA-02 | Performance-gap threshold 5 pp triggers targeted data-augmentation; tracked in `bias_remediation_log.md`. |
| FS-BIA-03 | URS-BIA-03 | Bias-evidence pack linked from Annex IV (`art10_data_governance/bias_evidence.md`); periodic-review checkpoint. |
| FS-PCCP-01 | URS-PCCP-01 | PCCP record per model in `pccp/{model_id}.yaml`: MoP + PCEM + IA fields per FDA Aug 2025 guidance. |
| FS-PCCP-02 | URS-PCCP-02 | `pccp_predicate_engine` (shared with Lyrae) verifies each update; `PCCP_OUT_OF_ENVELOPE` blocks promotion. |
| FS-PCCP-03 | URS-PCCP-03 | Deviation workflow: trigger Art. 43(4) substantial-modification assessment + Reg-Affairs sign-off + renewed conformity. |
| FS-PCCP-04 | URS-PCCP-04 | Annual review tracked in `pccp_review_calendar.yaml`. |
| FS-INF-01 | URS-INF-01 | Per-vial inference + reject-decision end-to-end latency P95 ≤ 30 ms at nominal line speed; verified by `latency_oq.py` benchmark. |
| FS-INF-02 | URS-INF-02 | Decision record schema: `vial_id`, `image_hashes[4]`, `model_id`, `model_version`, `decision` (Pass / Reject), `reject_subclass`, `confidence`, `edge_hostname`, `timestamp_iso8601`. |
| FS-INF-03 | URS-INF-03 | Fail-safe: model-server unreachable / inference timeout / inference error → emit Reject + alarm + audit-log; `default_to_reject_on_error: true` config-pinned. |
| FS-INF-04 | URS-INF-04 | Configurable confidence-threshold band per recipe; below-threshold routes vial to forced human review lane (`force_human_review` flag in PLC payload). |
| FS-INF-05 | URS-INF-05 | Deterministic-reproducibility OQ pins random seeds + ONNX Runtime execution-provider; bitwise output verification. |
| FS-IMG-01 | URS-IMG-01 | All vial images retained ≥ 12 mo (model evaluation) + reject images ≥ 7 y (batch record) + Annex IV-linked images ≥ 10 y (Art. 18); S3 `tes-images/` lifecycle policies. |
| FS-IMG-02 | URS-IMG-02 | S3 Object Lock (Compliance mode) on image bucket; out-of-retention delete requires dual signature via DocuSign workflow. |
| FS-IMG-03 | URS-IMG-03 | Monthly pass-image spot-check sample via `pass_spotcheck.py` → human review; false-pass findings feed PMM. |
| FS-TD-01 | URS-TD-01 | Annex IV pack template `annex_iv_template/` instantiated per `tes-aiact-techdoc/{model_id}/`; contains (a)–(h) sub-folders. |
| FS-TD-02 | URS-TD-02 | Pack-revision hook on model state transitions; pack-revision review by Conformity Assessment Coordinator before EFFECTIVE-CHAMPION. |
| FS-TD-03 | URS-TD-03 | Export job `annex_iv_export.py` produces zip within 1 business day for inspection. |
| FS-LOG-01 | URS-LOG-01 | Art. 12 event-log writer emits to Splunk index `tes-cv-audit` + local Postgres hot store; hot retention ≥ 6 mo. |
| FS-LOG-02 | URS-LOG-02 | Cold archive S3 + Glacier Vault Lock; ≥ 10 y per Art. 18 for Annex IV-linked records. |
| FS-CONF-01 | URS-CONF-01 | Conformity assessment per Art. 43 — internal-control pathway (Annex VI) by default since the CV system is a CGMP control; record in `conformity_records/{model_id}/`. |
| FS-CONF-02 | URS-CONF-02 | EU DoC per Art. 47 — template `eu_doc_template.docx` populated + signed by Reg-Affairs AI/ML via DocuSign. |
| FS-CONF-03 | URS-CONF-03 | CE-marking surface: operator-UI `Help → Compliance` panel renders structured `{marking: applied, doc_url, applied_standards}`. |
| FS-CONF-04 | URS-CONF-04 | Substantial-modification detection by PCCP predicate engine (FS-PCCP-02); triggers renewed conformity workflow. |
| FS-REG-01 | URS-REG-01 | No separate EU AI database registration; Annex I CV system inherits the medicinal-product manufacturing-authorisation registration. EUDAMED registration only triggered if the system is bundled into an MDR device. |
| FS-PMM-01 | URS-PMM-01 | PMM service collects per-batch FRR / FAR estimates, downstream human-inspection corroboration / contradiction, drift detections, false-pass spot-check; data into CAPA sink. |
| FS-PMM-02 | URS-PMM-02 | Quarterly PMM report template `pmm_report.md.j2` auto-generated + signed by Mfg Auto Lead + Head Sterile Mfg + Head QA. |
| FS-INC-01 | URS-INC-01 | Art. 73 incident service tracks 15 d / 10 d / 2 d clocks; particulate-contaminated parenteral reaching market triggers immediate incident. |
| FS-INC-02 | URS-INC-02 | Authority routing: BfArM (DE) primary; QP-mediated Annex 1 regulator-notification channel via Manufacturing Authorisation Holder. |
| FS-INC-03 | URS-INC-03 | Incident schema: `batch_id`, `vial_id_if_traceable`, `narrative`, `root_cause_status`, `corrective_action`, `notification_status`. |
| FS-DEP-01 | URS-DEP-01 | Site Manufacturing Operations is the deployer; deployer-obligations checklist in `deployer_obligations.md`; works-council notification recorded in HR ticket. |
| FS-ROB-01 | URS-ROB-01 | Perturbation OQ `perturbation_oq.py`: lighting ±20%, position ±2 mm, exposure ±10%; performance asserted within envelope. |
| FS-ROB-02 | URS-ROB-02 | Training-data hash + cosign verification at ingest; SBOM (CycloneDX) for all pre-trained weights in `sbom/`. |
| FS-ROB-03 | URS-ROB-03 | Enclosure intrusion sensor wired to PLC; secure-boot enforced on Jetson; firmware cosign-signed. |
| FS-ROB-04 | URS-ROB-04 | TLS 1.3 inter-component; mTLS to Triton + Lyrae model server; cert rotation 90 d via cert-manager. |
| FS-QMS-01 | URS-QMS-01 | QMS conformance documented in `qms_manual_cv.md`; controls mapped against ISO/IEC 42001 clauses; integrated with site PQS per ICH Q10. |
| FS-QMS-02 | URS-QMS-02 | Annual QMS effectiveness review by VP QA + Head Sterile Mfg + Reg-Affairs; report in `qms_review/{year}/`. |
| FS-AUD-01 | URS-AUD-01 | Audit trail `audit_events` captures: model deployments, configuration changes, alarm acknowledgements, signatures, manual decision overrides, Art. 73 incident triggers. |
| FS-AUD-02 | URS-AUD-02 | DB role `cv_app` granted only INSERT/SELECT on `audit_events`; UPDATE/DELETE denied at Postgres level. |
| FS-AUD-03 | URS-AUD-03 | Per-batch review UI for Quality Reviewer; quarterly review report template for QA Compliance. |
| FS-AUD-04 | URS-AUD-04 | Audit retention: Postgres hot (1 y), Splunk warm (5 y), S3 cold (≥ 25 y batch-relevant; ≥ 10 y Annex IV). |
| FS-AUD-05 | URS-AUD-05 | Audit-trail review evidence attached to batch record per 21 CFR § 211.192 / Annex 1. |
| FS-PART11-01 | URS-PART11-01 | E-signature record schema: `signer_printed_name`, `signing_timestamp_iso8601`, `signing_meaning` (REVIEW / APPROVE / SUSPEND / DEPLOY). |
| FS-PART11-02 | URS-PART11-02 | DB uniqueness constraint on `signer_id`; Okta provisioning denies reuse. |
| FS-PART11-03 | URS-PART11-03 | Signature → record link via HMAC-SHA256 over snapshot-hash + signer-ID + timestamp; verification on read. |
| FS-PART11-04 | URS-PART11-04 | OPA-based authz enforces role-separation per § 11.10(g); tested via `opa-test` CI job. |
| FS-PART11-05 | URS-PART11-05 | Re-auth: signing endpoint requires fresh OIDC ID token (`auth_time` < 60 s). |
| FS-PART11-06 | URS-PART11-06 | Procedural controls SOP `/sop/cv-controls.md` reviewed annually. |
| FS-PART11-07 | URS-PART11-07 | Okta + MFA group `tes-cv-prod`; service accounts via Vault-issued mTLS only. |
| FS-PART11-08 | URS-PART11-08 | Operational audit trail per FS-AUD-01. |
| FS-PART11-09 | URS-PART11-09 | Export endpoints produce both JSON + PDF/A-3; consistency verified by hash compare. |
| FS-PART11-10 | URS-PART11-10 | Retention enforced via S3 Object Lock + Splunk frozen-index (≥ 25 y batch + ≥ 10 y Annex IV). |
| FS-PART11-11 | URS-PART11-11 | Okta password policy: MFA mandatory, lockout 5 fails / 15 min, complexity per site standard. |
| FS-AN1-01 | URS-AN1-01 | Annex 1 §8.123 — operator-UI banner displays "Human visual inspection downstream is retained as primary release control. CV is supplementary."; inspector training course `INSPECTOR-USP1790-QUAL` enforces. |
| FS-CHAL-01 | URS-CHAL-01 | Challenge-test cadence enforced by `batch_workflow.py`: start-of-batch + 3× mid-batch + end-of-batch checks; Knapp-test reference set used. |
| FS-CHAL-02 | URS-CHAL-02 | Challenge-set library physically marked + segregated; reconciliation step before batch close; mix-up prevention SOP `/sop/challenge-set-control.md`. |
| FS-CHAL-03 | URS-CHAL-03 | Failure triggers `batch_hold` event + auto-paging Head of QA + QP; resumption gated by joint sign-off. |
| FS-CHAL-04 | URS-CHAL-04 | Trending board `challenge_trends.json`; deviations feed PMM (FS-PMM-01). |
| FS-USP-01 | URS-USP-01 | Per USP <790>, probabilistic detection capability demonstrated against reference particle set (10 μm, 25 μm, 50 μm, 100 μm) per validation plan; result in `usp790_capability_report.md`. |
| FS-USP-02 | URS-USP-02 | Per USP <1790>, Knapp-reference-vial correlation report in `usp1790_knapp_report.md`; acceptance criteria documented. |
| FS-USP-03 | URS-USP-03 | Operator-UI banner clarifies "Subvisible particulate inspection (USP <787>/<788>) out of scope — separate procedure applies." |
| FS-211-01 | URS-211-01 | QA Compliance sign-off in batch-release workflow; CV-related deviations route to QA per § 211.22. |
| FS-211-02 | URS-211-02 | Automatic-equipment validation per § 211.68: IQ + OQ + PQ on schedule + after any change; routine calibration in `cal_schedule.yaml`. |
| FS-211-03 | URS-211-03 | In-process control reject-rate trending in PAS-X per-batch summary; threshold-based deviation creation. |
| FS-211-04 | URS-211-04 | Batch record includes CV reject summary auto-pushed to PAS-X (FS-INT-MES-01); QP review per § 211.192. |
| FS-DEV-01 | URS-DEV-01 | SDLC documented per ICH Q9 + GAMP AI/ML GPG: dataset versioning, ground-truth labelling QC (FS-LBL-01..05), model-validation per assay (sensitivity / specificity / PPV / NPV against reference truth). |
| FS-DEV-02 | URS-DEV-02 | Source in validated GitLab; signed commits; pinned dependencies; reproducible-build runner. |
| FS-DEV-03 | URS-DEV-03 | Coverage measured by `pytest-cov`; CI fails below 90% on integration service, below 80% on training pipeline. |
| FS-DEV-04 | URS-DEV-04 | Ruff + mypy --strict + Bandit + Trivy + Snyk on every CI build; criticals break build. |
| FS-DEV-05 | URS-DEV-05 | ML-specific quality gates orchestrated by `ml_quality_gate.py` covering FS-ML-01..08. |
| FS-DEV-06 | URS-DEV-06 | OSS dependency vendor-assurance per `TES-VA-OSS-CV-001`; annual review covers license + vulnerability + maintainership. |
| FS-DEV-07 | URS-DEV-07 | Release cosign-signed; release manifest enumerates model + integration-service + config versions + Annex IV pack URL. |
| FS-INT-PLC-01 | URS-INT-PLC-01 | Reject command to filling-line PLC (Allen-Bradley ControlLogix) over EtherNet/IP with mTLS; loss-of-comms watchdog triggers fail-safe Reject. |
| FS-INT-MES-01 | URS-INT-MES-01 | Per-vial reject summary pushed to PAS-X via REST; recipe / batch context read at batch start. |
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | Excessive-reject-rate auto-creates deviation in MasterControl; idempotency key `tes-cv:batch:{batch_id}:event:{event_id}`. |
| FS-INT-AD-01 | URS-INT-AD-01 | Okta SAML 2.0 + MFA; service accounts via Vault. |
| FS-INT-LYR-01 | URS-INT-LYR-01 | Models deployed via Lyrae AI/ML Model Server (LYR-FS-MLSRV-001 FS-MOD-01..07); platform-level EU AI Act controls apply uniformly. |
| FS-INT-LMS-01 | URS-INT-LMS-01 | Cornerstone LMS API call at session start; non-current inspectors blocked from labelling + override; non-current operators blocked from privileged actions. |
| FS-DI-01 | URS-DI-01 | All records carry `actor_id` (named) + `model_version_id` (always). |
| FS-DI-02 | URS-DI-02 | Export endpoints render CSV + PDF/A-3; image retrieval by SHA-256 hash. |
| FS-DI-03 | URS-DI-03 | PTP timestamps synced from `ptp-master.tes.local`; skew < 10 ms verified by OQ. |
| FS-DI-04 | URS-DI-04 | Captured images written to S3 Object-Lock bucket `tes-images-raw/`; no overwrite. |
| FS-DI-05 | URS-DI-05 | Decision-logic accuracy verified by OQ on locked validation set; output transformations deterministic. |
| FS-DI-06 | URS-DI-06 | Retention metadata enforced via S3 lifecycle + Splunk frozen-index; record availability ≤ 4 h during inspection. |
| FS-DI-07 | URS-DI-07 | Training-data governance enforced via FS-LBL-01..05 + FS-BIA-01..03 + FS-DEF-01..04 (Art. 10 backbone). |
| FS-PERF-01 | URS-PERF-01 | Sustained ≥ 400 vials/min throughput at FS-INF-01 latency over 8-h shift; verified by `throughput_pq.py`. |
| FS-AV-01 | URS-AV-01 | Availability ≥ 99.5% during fill operations; Grafana SLO board. |
| FS-BAK-01 | URS-BAK-01 | Decision DB + image object store backed up nightly with PITR; image store replicated to DC-2. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore test scripted in `tes-cv-dr` repo; QA witness sign-off. |
| FS-BAK-03 | URS-BAK-03 | Annual Glacier-restore drill on Annex IV records; documented retrieval ≤ 24 h. |
| FS-HUM-01 | URS-HUM-01 | Operator-UI banner + SOP `/sop/human-inspection-downstream.md` enforces 100% human visual inspection downstream. |
| FS-HUM-02 | URS-HUM-02 | Inspector pool capability tracked via LMS qualification + Knapp-test re-pass cadence (semi-annual). |
| FS-HUM-03 | URS-HUM-03 | Inspector-workload monitor `inspector_workload.py`; ≥ 30% reduction triggers visual-acuity calibration. |
| FS-SEC-01 | URS-SEC-01 | Okta + MFA; no local accounts other than break-glass. |
| FS-SEC-02 | URS-SEC-02 | TLS 1.3 client-server; mTLS inference service ↔ Triton. |
| FS-SEC-03 | URS-SEC-03 | Vault Agent sidecar retrieves secrets at start-up; OQ verifies no on-disk / env secrets. |
| FS-SEC-04 | URS-SEC-04 | Tenable + Trivy monthly scans; criticals SLA 30 d. |
| FS-SEC-05 | URS-SEC-05 | Edge-device tamper events from enclosure-intrusion sensor wired into PLC + alarm; emits fail-safe Reject. |
| FS-TRN-01 | URS-TRN-01 | Okta group provisioning gated by LMS `INSPECTOR-USP1790-QUAL` + `CV-OPERATOR-CURRENT` + (where applicable) `CV-ML-REVIEWER`. |
| FS-TRN-02 | URS-TRN-02 | AI literacy course `AI-LITERACY-ART4` site-wide for staff with AI-output exposure. |
| FS-PR-01 | URS-PR-01 | Annual periodic review template covering config drift, model registry + drift trends, FRR / FAR by batch, deviations, training-data refresh, fitness, PCCP adherence, QMS effectiveness; signed by Mfg Auto Lead + Head Sterile Mfg + Head QA + Reg-Affairs (AI/ML). |
| FS-PR-02 | URS-PR-02 | Quarterly model-evaluation review template; drift + false-pass spot-check + reject trends + Knapp-test results; signed by Vision Eng Lead. |
| FS-PR-03 | URS-PR-03 | Annual classification reassessment; reclassification change-controlled. |


### 4.1 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: Kerberos for interactive operator logon and a gMSA service account for the inference / pipeline services. Conditional-access binding to policy `AI-Platform Conditional Access (FIDO2 + device-compliance) for operators; gMSA-bound service identity for the inference workload`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with PostgreSQL pg_basebackup + WAL for the inspection-event store plus MinIO/S3 object-replica for image evidence and Annex IV artefacts; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Configuration Items (CI)

| CI | Item | Value |
|---|---|---|
| CI-01 | Reject threshold | recipe-defined in `recipes/{product_id}.yaml` |
| CI-02 | Fail-safe | reject on model-server unreachable / timeout / power loss |
| CI-03 | Drift monitoring | enabled, 3 axes (data / concept / prediction) |
| CI-04 | Challenge cadence | start + 3× mid + end of batch per Annex 1 §8.123 |
| CI-05 | Knapp-reference vial | `knapp_ref_vials_v{n}` per USP <1790> |
| CI-06 | Defect-class library | `defect_classes_v{n}.yaml` |
| CI-07 | PCCP predicate engine | shared with Lyrae `pccp_predicate_engine v1.0` |
| CI-08 | Backlight intensity | 2,000–3,750 lux per USP <1790>, per-product configured |
| CI-09 | Annex IV pack base path | `s3://tes-aiact-techdoc/` |
| CI-10 | Art. 18 retention | 10 y from market placement |
| CI-11 | Cohen κ threshold | ≥ 0.7 for labelling campaign acceptance |
| CI-12 | Pareto-improvement tolerance | FRR Δ ≤ 0.5 pp; FAR Δ ≤ 0 |

## 6. Risks (FS-level)

Implementation-level risks (URS § 9 documents R-01..R-17). FS-side additional risks:

- Edge GPU thermal throttling under sustained load → mitigation: thermal monitoring + auto-scale to second Jetson
- ONNX Runtime non-determinism due to FP16 reduction order → mitigation: pinned EP + FP32 in determinism OQ
- Recipe-config drift between sites → mitigation: GitOps for recipes + per-recipe sign-off
- Knapp-reference-vial degradation over time → mitigation: vial refresh schedule + cross-cal against new
- Annex IV pack drift across product variants → mitigation: per-product Annex IV instance + cross-check CI
- Art. 73 clock mis-attribution between CV-system incident vs upstream / downstream cause → mitigation: incident classifier with QP gatekeeping

## 7. References

- TES-URS-CV-001 v1.2
- 21 CFR Part 11; 21 CFR Part 211 (§§ .22, .68, .110, .192)
- EU GMP Annex 11; EU GMP Annex 1 (2022, § 8.123)
- EU AI Act 2024/1689 Arts. 8–21, 26, 43, 47, 48, 49, 72, 73, 99, 113
- USP <1>, <787>, <788>, <790>, <1790>; Ph. Eur. 2.9.20
- FDA AI/ML SaMD Action Plan (2021); FDA GMLP Guiding Principles (2021); FDA PCCP (Aug 2025); FDA CSA (Feb 2026); FDA Inspection of Injectable Products for Visible Particulates (Draft, 2021)
- ISPE GAMP 5 (2nd ed., 2022); ISPE GAMP GPG *AI/ML in GxP* (2024); ISPE GAMP RDI
- ISO 14971:2019; ISO/IEC 42001:2023
- PDA Technical Report 79
- BfArM (DE); Swissmedic (CH); AGES (AT)
- Lyrae AI/ML Model Server FS (LYR-FS-MLSRV-001)
- Tessera site documents: `TES-VA-OSS-CV-001`, `TES-SOP-CV-CONTROLS-001`

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-HW-01 | FS-HW-01 |
| URS-HW-02 | FS-HW-02 |
| URS-HW-03 | FS-HW-03 |
| URS-HW-04 | FS-HW-04 |
| URS-HW-05 | FS-HW-05 |
| URS-OPT-01 | FS-OPT-01 |
| URS-OPT-02 | FS-OPT-02 |
| URS-OPT-03 | FS-OPT-03 |
| URS-OPT-04 | FS-OPT-04 |
| URS-ML-01 | FS-ML-01 |
| URS-ML-02 | FS-ML-02 |
| URS-ML-03 | FS-ML-03 |
| URS-ML-04 | FS-ML-04 |
| URS-ML-05 | FS-ML-05 |
| URS-ML-06 | FS-ML-06 |
| URS-ML-07 | FS-ML-07 |
| URS-ML-08 | FS-ML-08 |
| URS-DEF-01 | FS-DEF-01 |
| URS-DEF-02 | FS-DEF-02 |
| URS-DEF-03 | FS-DEF-03 |
| URS-DEF-04 | FS-DEF-04 |
| URS-LBL-01 | FS-LBL-01 |
| URS-LBL-02 | FS-LBL-02 |
| URS-LBL-03 | FS-LBL-03 |
| URS-LBL-04 | FS-LBL-04 |
| URS-LBL-05 | FS-LBL-05 |
| URS-BIA-01 | FS-BIA-01 |
| URS-BIA-02 | FS-BIA-02 |
| URS-BIA-03 | FS-BIA-03 |
| URS-PCCP-01 | FS-PCCP-01 |
| URS-PCCP-02 | FS-PCCP-02 |
| URS-PCCP-03 | FS-PCCP-03 |
| URS-PCCP-04 | FS-PCCP-04 |
| URS-INF-01 | FS-INF-01 |
| URS-INF-02 | FS-INF-02 |
| URS-INF-03 | FS-INF-03 |
| URS-INF-04 | FS-INF-04 |
| URS-INF-05 | FS-INF-05 |
| URS-IMG-01 | FS-IMG-01 |
| URS-IMG-02 | FS-IMG-02 |
| URS-IMG-03 | FS-IMG-03 |
| URS-TD-01 | FS-TD-01 |
| URS-TD-02 | FS-TD-02 |
| URS-TD-03 | FS-TD-03 |
| URS-LOG-01 | FS-LOG-01 |
| URS-LOG-02 | FS-LOG-02 |
| URS-CONF-01 | FS-CONF-01 |
| URS-CONF-02 | FS-CONF-02 |
| URS-CONF-03 | FS-CONF-03 |
| URS-CONF-04 | FS-CONF-04 |
| URS-REG-01 | FS-REG-01 |
| URS-PMM-01 | FS-PMM-01 |
| URS-PMM-02 | FS-PMM-02 |
| URS-INC-01 | FS-INC-01 |
| URS-INC-02 | FS-INC-02 |
| URS-INC-03 | FS-INC-03 |
| URS-DEP-01 | FS-DEP-01 |
| URS-ROB-01 | FS-ROB-01 |
| URS-ROB-02 | FS-ROB-02 |
| URS-ROB-03 | FS-ROB-03 |
| URS-ROB-04 | FS-ROB-04 |
| URS-QMS-01 | FS-QMS-01 |
| URS-QMS-02 | FS-QMS-02 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
| URS-AUD-05 | FS-AUD-05 |
| URS-PART11-01 | FS-PART11-01 |
| URS-PART11-02 | FS-PART11-02 |
| URS-PART11-03 | FS-PART11-03 |
| URS-PART11-04 | FS-PART11-04 |
| URS-PART11-05 | FS-PART11-05 |
| URS-PART11-06 | FS-PART11-06 |
| URS-PART11-07 | FS-PART11-07 |
| URS-PART11-08 | FS-PART11-08 |
| URS-PART11-09 | FS-PART11-09 |
| URS-PART11-10 | FS-PART11-10 |
| URS-PART11-11 | FS-PART11-11 |
| URS-AN1-01 | FS-AN1-01 |
| URS-CHAL-01 | FS-CHAL-01 |
| URS-CHAL-02 | FS-CHAL-02 |
| URS-CHAL-03 | FS-CHAL-03 |
| URS-CHAL-04 | FS-CHAL-04 |
| URS-USP-01 | FS-USP-01 |
| URS-USP-02 | FS-USP-02 |
| URS-USP-03 | FS-USP-03 |
| URS-211-01 | FS-211-01 |
| URS-211-02 | FS-211-02 |
| URS-211-03 | FS-211-03 |
| URS-211-04 | FS-211-04 |
| URS-DEV-01 | FS-DEV-01 |
| URS-DEV-02 | FS-DEV-02 |
| URS-DEV-03 | FS-DEV-03 |
| URS-DEV-04 | FS-DEV-04 |
| URS-DEV-05 | FS-DEV-05 |
| URS-DEV-06 | FS-DEV-06 |
| URS-DEV-07 | FS-DEV-07 |
| URS-INT-PLC-01 | FS-INT-PLC-01 |
| URS-INT-MES-01 | FS-INT-MES-01 |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 |
| URS-INT-AD-01 | FS-INT-AD-01 |
| URS-INT-LYR-01 | FS-INT-LYR-01 |
| URS-INT-LMS-01 | FS-INT-LMS-01 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-DI-07 | FS-DI-07 |
| URS-PERF-01 | FS-PERF-01 |
| URS-AV-01 | FS-AV-01 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-BAK-03 | FS-BAK-03 |
| URS-HUM-01 | FS-HUM-01 |
| URS-HUM-02 | FS-HUM-02 |
| URS-HUM-03 | FS-HUM-03 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-SEC-05 | FS-SEC-05 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-PR-02 | FS-PR-02 |
| URS-PR-03 | FS-PR-03 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | False-accept on cracked / particulate vial | Medium | Critical | URS-ML-03 + URS-AN1-01 + URS-HUM-01..03 downstream defence-in-depth + URS-CHAL-01..04 challenge tests |
| R-02 | Model drift undetected | Medium | High | URS-ML-06 + URS-PR-02 + URS-PMM-01 |
| R-03 | Fail-safe defect | Low | Critical | URS-INF-03 + URS-HW-02 |
| R-04 | Image tampering / loss | Low | High | URS-IMG-01..03 |
| R-05 | Training-data poisoning | Low | High | URS-DEV-01..07 + URS-ML-02 + URS-ROB-02 |
| R-06 | Audit-trail tampering | Low | Critical | URS-AUD-02 |
| R-07 | Communication loss to conveyor | Medium | High | URS-INT-PLC-01 |
| R-08 | Defect-class imbalance hides minority-class failures | Medium | High | URS-DEF-01..04 + URS-BIA-01..03 |
| R-09 | Inter-rater labelling disagreement biases training | Medium | High | URS-LBL-01..05 |
| R-10 | Training-data drift on excipient / container changes | Medium | High | URS-BIA-01 + URS-ML-06 + URS-PMM-01 |
| R-11 | Supply-chain attack on pre-trained weights | Low | High | URS-ROB-02 + URS-ML-05 |
| R-12 | Edge-device tamper | Low | High | URS-ROB-03 + URS-SEC-05 |
| R-13 | EU AI Act Annex I deadline missed (2 Aug 2027) | Low | Critical | URS-TD-01..03 + URS-CONF-01..04 + URS-PR-03 |
| R-14 | EU AI Act Art. 73 incident-clock missed | Low | Critical | URS-INC-01..03 |
| R-15 | USP <790> / Annex 1 challenge-test failure | Low | Critical | URS-CHAL-01..04 + URS-USP-01..02 |
| R-16 | Inspector pool capability erosion due to CV-induced workload reduction | Medium | High | URS-HUM-02..03 |
| R-17 | EU AI Act Art. 99 penalty exposure (up to €15M / 3% turnover) | Low | Critical | URS-QMS-01..02 + URS-PR-01 |

Full evaluation in `TES-RA-CV-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
