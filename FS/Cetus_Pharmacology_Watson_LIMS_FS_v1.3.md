---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (FS catch-up to v1.1 URS)
seed_corpus_basis: [CET-URS-WATSON-001 v1.1, GAMP 5 Cat 4, 21 CFR Part 11, 21 CFR Part 58, ICH M10, OECD GLP, BfR GLP-Bundesstelle (DE), BfArM (DE medicines/devices not GLP), Swissmedic, AGES]
parent_urs:
  document_number: CET-URS-WATSON-001
  version: 1.1
  file: ../../URS/_generated/final/Watson_LIMS_Bioanalytical__Cetus_Pharmacology_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# Functional Specification (FS)

## Bioanalytical LIMS — Thermo Fisher Watson LIMS 7.6

**Document Number:** CET-FS-WATSON-001 | **Version:** 1.1 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** CET-URS-WATSON-001 v1.1 | **Site:** Cetus Pharmacology GmbH, Heidelberg, Germany *(fictional)*
**System Class:** GAMP Cat 4 — Configured Product
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; 21 CFR Part 58 (GLP) §§ .29, .33, .35, .81, .120, .130, .185, .190, .195; FDA Bioanalytical Method Validation (2018); EMA Bioanalytical (2011); ICH M10 (2022); ICH E6(R3) GCP (Step 4, 2025); OECD GLP; **BfR GLP-Bundesstelle + Länder (DE)** for GLP; BfArM (DE medicines/devices, not GLP); Swissmedic (CH); AGES (AT).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, Bioanalytical Operations) | _____________ | _____________ | _____ |
| Reviewer (Study Director — GLP per § 58.33) | _____________ | _____________ | _____ |
| Reviewer (Principal Investigator) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (QAU — § 58.35) | _____________ | _____________ | _____ |
| Approver (VP DMPK) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.1: ICH M10 acceptance-criteria engine; 21 CFR Part 58 GLP sub-section implementations; Study Director / PI / QAU role separation; archive-Archivist-only access; inspection-readiness export; Heidelberg (DE) deployment context. |
| 1.2 | 2026-05-13 | (synthetic) | T3 catch-up to URS v1.2: new FS sections for sample-receipt + aliquoting + freeze/thaw budget + storage excursion; study-build + protocol-pinning + amendment workflow; LBA-specific plate-map + 4PL/5PL curve fit + ADA tiered approach + NAb cell-based + hook-effect; ISR selection algorithm + stability-reanalysis; run-review + re-assay decision tree; reportable-result release workflow; § 58.185 study-report builder; § 58.190 GLP archive workflow; inspection-readiness tenant. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies Watson LIMS 7.6 configuration to satisfy `CET-URS-WATSON-001` v1.1, including v1.1 additions for ICH M10 acceptance-criteria engine, 21 CFR Part 58 GLP role-separation enforcement, QAU independent access, archive-Archivist-only gateway, and inspection-readiness export.

## 2. Scope

Watson LIMS 7.6 application servers + Oracle 19c with Data Guard; per-study configuration with ICH M10 acceptance rules; SSO via Okta + MFA; integrations with LC-MS/MS instruments + Empower CDS, ELN (Benchling), eTMF, GLP archive system per § 58.190.

## 3. System Architecture

```
                Okta SSO + MFA
                    │
                    ▼
   ┌─────────────────────────────────────────────────┐
   │   Watson LIMS 7.6 (Cetus, GLP/GCP)              │
   │   ┌─────────────────────────────────────────┐    │
   │   │ Sample chain-of-custody                  │    │
   │   │ Method registry (ICH M10 validation status)│   │
   │   │ Run-acceptance engine                    │    │
   │   │ GLP-archive Archivist gateway            │    │
   │   └─────────────────────────────────────────┘    │
   │   Oracle 19c + Data Guard (HA + DR)              │
   └─┬───────────┬──────────────┬─────────────────┬───┘
     │           │              │                 │
     ▼           ▼              ▼                 ▼
   LC-MS/MS    Benchling ELN   eTMF          GLP Archive
   + Empower   (sample-prep)   (study-report)  (§ 58.190)
```

## 4. Functional Specifications

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | Active + DR Watson cluster; RPO ≤ 15 min; RTO ≤ 4 h; annual DR test. |
| FS-PLAT-02 | URS-PLAT-02 | Oracle 19c Enterprise + Data Guard physical-standby; nightly pg_dump + PITR; quarterly restore test. |
| FS-CFG-01 | URS-CFG-01 | Per-study configuration: DRAFT → REVIEW → APPROVED → EFFECTIVE; pre-sample-analysis sign-off required. |
| FS-CFG-02 | URS-CFG-02 | Configuration export for FDA / EMA / BfArM / Swissmedic inspection. |
| FS-MTH-01 | URS-MTH-01 | Method record field `validation_status` ∈ {full, partial, cross, none}; only `full` runs regulated samples per ICH M10. |
| FS-MTH-02 | URS-MTH-02 | Method approval requires Author ≠ Approver + QA + Study Director (3-of-3 signed JWTs). |
| FS-MTH-03 | URS-MTH-03 | Validation parameters per ICH M10 §§ 3 (chromatographic) + 4 (LBA) captured per method type: selectivity, specificity, accuracy, precision, linearity, sensitivity / LLOQ, dilution integrity, matrix effect, recovery, carryover, stability. Parameter set selected by `method_type` (chromatographic vs LBA). |
| FS-MTH-04 | URS-MTH-04 | Method scope (matrix, species, concentration range) enforced at run-construction; out-of-scope blocked. |
| FS-MTH-05 | URS-MTH-05 | Method-version-drift triggers partial-validation / cross-validation flow per ICH M10 § 6.1. |
| FS-SMP-01 | URS-SMP-01 | Chain-of-custody captured from receipt → storage → run; storage-temperature excursion alerts. |
| FS-SMP-02 | URS-SMP-02 | Sample record schema per § 58.81: collection date, type, source, storage location, custody trail. |
| FS-RUN-01 | URS-RUN-01 | Run-construction wizard with run-acceptance-criteria template (n calibrators + n QCs per level). |
| FS-RUN-02 | URS-RUN-02 | **ICH M10 run-acceptance engine** per §§ 3.3.2 (chromatographic) / 4.3.2 (LBA); per-method-type thresholds (chromatographic: ± 15% cal / ± 20% LLOQ / ± 15% QC; LBA: ± 20% cal / ± 25% LLOQ / ± 20% QC; ≥ 75% / ≥ 67% / ≥ 50% rules per §§ 3.3.2 / 4.3.2); fail-the-run automatic. |
| FS-RUN-03 | URS-RUN-03 | ISR engine per ICH M10 § 5: 10% clinical / 7% non-clinical; pass criterion ≥ 67% repeats within ± 20% (chromatographic) / ± 30% (LBA) of mean original-vs-repeat. |
| FS-RUN-04 | URS-RUN-04 | Reanalysis policy (repeat analysis / reassay) configurable per study with documented justification rules per ICH M10 §§ 3.3.4 (chromatographic) / 4.3.4 (LBA). |
| FS-GLP-01 | URS-GLP-01 | Per 21 CFR § 58.33: Study Director sign-off is attributable + non-delegatable; UI prevents delegation at signing time. |
| FS-GLP-02 | URS-GLP-02 | Per 21 CFR § 58.35: QAU has independent all-study-data read; QAU review records retained in separate schema not editable by operations roles. |
| FS-GLP-03 | URS-GLP-03 | Per 21 CFR § 58.120: protocol version pinned to the run; protocol amendments are controlled and trigger re-pinning on next sample. |
| FS-GLP-04 | URS-GLP-04 | Per 21 CFR § 58.130: data recorded directly + promptly + legibly with `recorder_id` captured; retroactive entries flagged. |
| FS-GLP-05 | URS-GLP-05 | Per 21 CFR § 58.185: final-study-report builder produces report with study-id, dates, materials, methods, results, Study Director + responsible-scientists + QAU statement signatures. |
| FS-GLP-06 | URS-GLP-06 | Per 21 CFR § 58.190: GLP archive gateway with Archivist-only access via dedicated service-account; archive write restricted to Archivist role. |
| FS-GLP-07 | URS-GLP-07 | Per 21 CFR § 58.195: archive retention ≥ 2 y post-Application submission (FDA) or per study contract; deletion blocked before retention threshold. |
| FS-AUD-01 | URS-AUD-01 | Audit-trail covers sample / method / run / approval events; full schema. |
| FS-AUD-02 | URS-AUD-02 | Append-only DB; LIMS Administrator cannot UPDATE / DELETE. |
| FS-AUD-03 | URS-AUD-03 | Monthly Operations review + per-run Senior Bioanalyst review. |
| FS-AUD-04 | URS-AUD-04 | QAU review entries retained separately; non-editable. |
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural controls protecting electronic-record validity documented in `/sop/`; reviewed annually. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(d): access limited to authorised individuals via Okta SAML 2.0 + MFA; service accounts via mTLS only. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(e): operational audit trail capturing user, action, date, time — implemented via FS-AUD-01. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.50: electronic signatures include signer's printed name, date and time of signing, and meaning of signature; schema enforced in DB. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.70: signatures cryptographically linked to the signed record via HMAC-SHA256 over record-hash + signer-id + timestamp; tampered records flagged on read. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.100: signature unique per individual; reuse / reassignment blocked at provisioning via Okta-DB uniqueness constraint. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.200: re-authentication required at the moment of signing (fresh OAuth2 token, max-age 5 min); cached credentials rejected. |
| FS-DI-01 | URS-DI-01 | **Attributable:** every action / entry carries `actor_id` (named user or service-account); DB constraint not-null at audit-write. |
| FS-DI-02 | URS-DI-02 | **Legible:** records exportable as PDF/A-3 + machine-readable JSON/XML; rendering verified via OQ. |
| FS-DI-03 | URS-DI-03 | **Contemporaneous:** event timestamps server-side + NTP-synced; retroactive entries flagged with delay reason. |
| FS-DI-04 | URS-DI-04 | **Original:** raw inputs / records preserved in immutable storage; derivative analyses reference but do not overwrite the original. |
| FS-DI-05 | URS-DI-05 | **Accurate:** calculations / transformations deterministic and validated under OQ; floating-point reproducibility verified where applicable. |
| FS-DI-06 | URS-DI-06 | **Complete / Consistent / Enduring / Available:** metadata completeness validated; chronological order DB-enforced; retention per applicable regulation; retrievable within 1 business day. |
| FS-INT-CDS-01 | URS-INT-CDS-01 | Empower CDS bidirectional: worklist out + signed-off result back; checksums both directions. |
| FS-INT-ELN-01 | URS-INT-ELN-01 | Sample-prep records cross-referenced to bioanalytical batch via `prep_record_urn`. |
| FS-INT-ETMF-01 | URS-INT-ETMF-01 | Bioanalytical study-report archived to eTMF on study completion. |
| FS-INT-INST-01 | URS-INT-INST-01 | LC-MS/MS instrument cluster (Sciex / Waters) feeds acquisition metadata; instrument-id + serial logged per run. |
| FS-INT-ARCH-01 | URS-INT-ARCH-01 | GLP archive interface per § 58.190; archived records read-only via Archivist service-account. |
| FS-PERF-01 | URS-PERF-01 | Run-construction P95 ≤ 30 s for 96-sample plate. |
| FS-AV-01 | URS-AV-01 | Availability ≥ 99.5% during business hours; 7-day-advance maintenance window. |
| FS-BAK-01 | URS-BAK-01 | Database backup nightly with PITR; retention ≥ GLP archive period. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore drill with QA witness. |
| FS-SEC-01 | URS-SEC-01 | TLS 1.3 + AES-256. |
| FS-SEC-02 | URS-SEC-02 | RBAC review quarterly; Study Director + QAU role assignments require management approval. |
| FS-SEC-03 | URS-SEC-03 | USB / removable media blocked at workstation; vendor-engineered access via change control only. |
| FS-SEC-04 | URS-SEC-04 | Monthly vulnerability scan; critical findings remediated within 30 days. |
| FS-TRN-01 | URS-TRN-01 | LMS training enforced; Study Director + QAU roles require 21 CFR Part 58 GLP training. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher `BIOA-2026-ANNUAL`: ICH M10 + GLP guidance updates. |
| FS-PR-01 | URS-PR-01 | Annual Periodic Review template (configuration drift + audit-trail review + method-validation status + GLP archive + training + integrations); signed by Director Bioanalytical Operations + VP DMPK + VP QA + QAU lead. |
| FS-INS-01 | URS-INS-01 | Inspection-readiness export: complete-study-package per § 58.185 ≤ 1 business day; audit-trail per study ≤ 4 business hours. |
| FS-INS-02 | URS-INS-02 | Read-only inspection-tenant view supports mock-inspection drills. |

### 4.13 Sample Receipt, Aliquoting, Storage Lifecycle

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SAMP-01 | URS-SAMP-01 | Sample-receipt UI captures: sponsor study-id, collection date+time, matrix, anticoagulant, source species + animal-id (non-clinical) or subject-id + study-day (clinical), receipt date+time, receiver-id, container condition. Required fields validated server-side; missing field blocks receipt commit. |
| FS-SAMP-02 | URS-SAMP-02 | Sample-aliquot lifecycle modelled as parent→child tree (`parent_sample_id`, `aliquot_id`); each aliquot carries its own `freeze_thaw_count`, `location_history` (FIFO), `chain_of_custody` (audit-trail-bound). |
| FS-SAMP-03 | URS-SAMP-03 | Pre-run validator checks aliquot.freeze_thaw_count against method-bound `max_ft_cycles` (default 5 per ICH M10 method-validation); exceeded → block + Method-Owner-override workflow with reason. |
| FS-SAMP-04 | URS-SAMP-04 | Storage-location service records freezer-id, shelf, rack, position, in/out timestamps; integration with site BMS for temperature feed; excursion (> 1 °C deviation > 4 h) creates `StorageExcursion` event linked to all aliquots in that location. |
| FS-SAMP-05 | URS-SAMP-05 | Sample-destruction workflow requires Study Director + QAU dual eSign per § 58.81; destruction record retained per § 58.195; record contains aliquot inventory + destruction method + witness. |
| FS-SAMP-06 | URS-SAMP-06 | Shipping module captures courier, ship date+time, recipient site; in-transit temperature log uploaded from digital-data-logger (CSV); arrival-inspection record required at receiver site (else aliquot flagged `RECEIPT_PENDING`). |

### 4.14 Study Build and Protocol Pinning

| FS ID | URS ID | Specification |
|---|---|---|
| FS-STD-01 | URS-STD-01 | Study-build wizard requires: sponsor, protocol-id + version, IRB/IEC approval (clinical) or testing-facility approval (GLP), study-director-assignment, method-validation-evidence reference; missing element blocks build. |
| FS-STD-02 | URS-STD-02 | Protocol-pin module binds `(sample_id, acquired_at) → protocol_version`; amendments create new pinned version; prior-acquired samples remain pinned unless explicitly migrated via deviation. |
| FS-STD-03 | URS-STD-03 | Protocol document template enforces § 58.120(a) content: purpose, sponsor, facility, Study Director, dose route+frequency+duration, test-system, schedule, sample-collection schedule. Missing field blocks Study-Director sign-off. |
| FS-STD-04 | URS-STD-04 | Protocol-amendment workflow captures: reason, Study Director eSign, date, version increment; prior versions immutable per § 58.120(b). |
| FS-STD-05 | URS-STD-05 | Multi-site study model: list per-site PIs with assigned scope; PI signature workflow per site portion; Study Director retains overall sign-off per § 58.33. |

### 4.15 LBA-Specific Workflow

| FS ID | URS ID | Specification |
|---|---|---|
| FS-LBA-01 | URS-LBA-01 | Plate-map data model: per-well (`plate_id`, `well_position`, `well_type ∈ {sample, calibrator, qc, blank}`, `sample_id_or_level`, `replicate_index`); plate-reader feed bound to wells by position. |
| FS-LBA-02 | URS-LBA-02 | Curve-fit engine supports 4PL and 5PL logistic models per ICH M10 § 4 sub-sections; per-curve quality flags (% back-calc, % recovery, parallelism) computed. |
| FS-LBA-03 | URS-LBA-03 | ADA workflow implements ICH M10 § 4 tiered approach: screen → confirmatory → titer; per-tier cut-points method-bound; titer ladder dilution series captured as separate result entries. |
| FS-LBA-04 | URS-LBA-04 | NAb assay record schema includes: cell-line lot, passage number, plate-control parameters (positive ctrl, negative ctrl, vehicle ctrl); ICH M10 § 4 validation parameters captured. |
| FS-LBA-05 | URS-LBA-05 | Hook-effect detection rule (high-concentration sample reads lower than mid-range standard); flagged samples auto-routed to higher-dilution re-assay. |

### 4.16 ISR and Stability Sample Reanalysis

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ISR-01 | URS-ISR-01 | ISR-selection algorithm: deterministic seeded random sample of 10% (clinical) / 7% (non-clinical) subjects, stratified across ≥ 3 × LLOQ, peak, trough concentrations per ICH M10 § 5. |
| FS-ISR-02 | URS-ISR-02 | ISR-evaluation engine computes `(original − repeat) / mean(original, repeat) × 100`; method-type-bound criteria (chromatographic ± 20% / LBA ± 30%) per ICH M10 § 5; failure logs `ISR_FAIL` event + triggers investigation workflow. |
| FS-ISR-03 | URS-ISR-03 | ISR record persists per-sample: original-result, repeat-result, computed-mean, % deviation, pass/fail; ISR appendix auto-attached to final study report per § 58.185. |
| FS-ISR-04 | URS-ISR-04 | Stability-reanalysis scheduler: per long-term stability plan, triggers re-analysis at configured intervals (e.g., 30, 90, 180 days); comparison vs original within method-validated stability tolerance. |

### 4.17 Run Review and Re-assay Decision Tree

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RVW-01 | URS-RVW-01 | Run-review UI presents: calibration-curve fit, QC pass/fail panel, ISR (where applicable), method-quality flags, deviations; the system shall reject any review attempt where reviewer == run-acquirer (SoD enforced server-side). |
| FS-RVW-02 | URS-RVW-02 | Re-assay decision tree configured per study: rule-engine evaluates failure context (instrument, sample, QC) and presents permitted re-assay options per ICH M10 §§ 3.3.4 / 4.3.4; each decision captured with justification. |
| FS-RVW-03 | URS-RVW-03 | Re-injection events tagged distinctly from re-extraction events (`reassay_type ∈ {reinject, reextract}`); replacement vs supplement semantics enforced per method. |
| FS-RVW-04 | URS-RVW-04 | Run-rejection workflow: Senior Bioanalyst eSign + reason; rejected runs retained (visible in inspection tenant) but excluded from reportable-result computation. |

### 4.18 Reportable-Result Release Workflow

| FS ID | URS ID | Specification |
|---|---|---|
| FS-REL-01 | URS-REL-01 | Reportable-result computer applies method-bound rule (mean of accepted replicates by default); rounding per protocol; result distinct from analytical-batch-level result. |
| FS-REL-02 | URS-REL-02 | Release workflow: Bioanalyst → Senior Bioanalyst → Study Director (or PI for site portion) → QAU; each transition eSigned with closed-list meaning. |
| FS-REL-03 | URS-REL-03 | Server-side SoD: user-role-position table denies same user holding two consecutive roles on the same record; verified by `OQ-RELEASE-SOD-01`. |
| FS-REL-04 | URS-REL-04 | Held-reportable-result expiry timer 14 days; auto-revoke after expiry; re-approval requires Study Director eSign. |

### 4.19 Study Report Builder per § 58.185

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RPT-01 | URS-RPT-01 | Report-builder template includes all § 58.185(a) elements: purpose, identification, dates, test article (name + batch + characterisation), test-system, methods, results, transformed-data summary, QAU statement. |
| FS-RPT-02 | URS-RPT-02 | Per § 58.185(a)(13), storage locations auto-populated from archive interface (`FS-INT-ARCH-01`). |
| FS-RPT-03 | URS-RPT-03 | Per § 58.185(b), corrections as numbered amendments with reason; original report immutable; amendment versions linked. |
| FS-RPT-04 | URS-RPT-04 | Study Director signature on final report; non-delegatable per § 58.33; UI prevents delegation at signing time. |
| FS-RPT-05 | URS-RPT-05 | QAU statement per § 58.35(b) auto-populated from QAU review records (inspection dates + findings-reported-to-Study-Director dates). |

### 4.20 GLP Archive Workflow per § 58.190

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ARC-01 | URS-ARC-01 | Per § 58.190(a), study-completion transfer module bundles raw data + documentation + protocols + specimens-inventory + final report; transfer event recorded immutably. |
| FS-ARC-02 | URS-ARC-02 | Per § 58.190(b), archive-access service restricts read/write to Archivist role only; non-Archivist read access requires justification + audit-trail entry. |
| FS-ARC-03 | URS-ARC-03 | Per § 58.190(c), archive index entity stores per study: study-id, sponsor, dates, materials; full-text search supported. |
| FS-ARC-04 | URS-ARC-04 | Per § 58.195, deletion-block service prevents deletion before configured retention threshold (default ≥ 10 years post-Application; per sponsor contract); attempt logged + alerted. |
| FS-ARC-05 | URS-ARC-05 | Archive-restore (Archivist-only) produces audit-trail entry referencing sponsor / authority request correspondence. |

### 4.21 Inspection-Readiness Tenant

| FS ID | URS ID | Specification |
|---|---|---|
| FS-IRT-01 | URS-IRT-01 | On-demand inspection-tenant provisioning service: reconstitutes read-only complete study view (build + raw + audit + signatures + archive index) within 4 business hours; provisioned tenant URL signed + time-limited. |
| FS-IRT-02 | URS-IRT-02 | Tenant write-deny enforcement: tenant DB role has SELECT only; export requires Quality-Assurance eSign + adds watermark with inspection-id. |
| FS-IRT-03 | URS-IRT-03 | Quarterly mock-inspection drills scripted; findings logged in `CET-MOCK-INSP-YYYYQN`; remediation tracked. |


### 4.22 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem. Conditional-access binding to policy `Lab-App Conditional Access (MFA + device-compliance)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with Oracle RMAN for the Watson Oracle backend; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.23 Cross-System Integration — Lyrae + Helios (M-XINT-LYR)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-LYR-01 | URS-XINT-LYR-01 | AI-assist feature flag `cfg.ai_assist.peak_review.enabled = false` by default; flag-toggle requires Validation Lead + Bioanalytical Lead e-signature; toggled state stamped in the audit trail; AI-assist client adapter `CTS-LYR-CLIENT-1.x` enforces Lyrae-only routing. |
| FS-XINT-LYR-02 | URS-XINT-LYR-02 | AI suggestion UI surfaces a per-peak Accept / Reject control; bulk-accept disabled (UI control absent); back-end rejects any payload with `bulk_accept=true`; audit row schema `{run_id, peak_id, model_version, confidence, analyst_action, override_reason}`. |
| FS-XINT-LYR-03 | URS-XINT-LYR-03 | Helios ingestion via Kafka topic `helios.ingest.watson.aipeak.v1` (JSON Lines schema-registry pinned); pre-handover retention 2 y on the Watson side. |
| FS-XINT-LYR-04 | URS-XINT-LYR-04 | Lyrae drift webhook subscribed; auto-disable rule: PSI > 0.15 OR confusion-matrix shift > 5% → set `cfg.ai_assist.peak_review.enabled = false`; deviation auto-raised in MasterControl. |

## 5. Configuration Items (CI)

| CI | Item | Value |
|---|---|---|
| CI-01 | Method-validation status | full / partial / cross-validation (only `full` runs regulated samples) |
| CI-02 | Run-acceptance | ICH M10 §§ 3.3.2 (chromatographic) / 4.3.2 (LBA) engine |
| CI-03 | ISR engine | 10% clinical / 7% non-clinical |
| CI-04 | Study Director signature | non-delegatable |
| CI-05 | QAU access | independent role |
| CI-06 | Archive access | Archivist-only |
| CI-07 | Inspection export SLO | study-package ≤ 1 business day |

## 6. Risks (FS-level)

URS § 9 documents R-01..R-12. Additional FS risks:

- Empower CDS checksum mismatch on result back-flow → mitigation: contract test + alert
- Instrument-metadata feed drift on instrument software update → mitigation: schema validation at ingestion
- Archive service-account credential compromise → mitigation: Vault-stored + rotated 90-day

## 7. References

- CET-URS-WATSON-001 v1.1
- 21 CFR Part 11; 21 CFR Part 58 §§ .29, .33, .35, .81, .120, .130, .185, .190, .195
- FDA Bioanalytical Method Validation (2018); EMA Bioanalytical (2011)
- ICH M10 (2022); ICH E6(R3) GCP (Step 4, 2025)
- OECD Principles of GLP
- BfArM (DE); Swissmedic (CH); AGES (AT)
- ISPE GAMP 5 (2nd ed., 2022)
- Thermo Fisher — *Watson LIMS 7.6 Configuration Reference*

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-PLAT-01 | FS-PLAT-01 |
| URS-PLAT-02 | FS-PLAT-02 |
| URS-CFG-01 | FS-CFG-01 |
| URS-CFG-02 | FS-CFG-02 |
| URS-MTH-01 | FS-MTH-01 |
| URS-MTH-02 | FS-MTH-02 |
| URS-MTH-03 | FS-MTH-03 |
| URS-MTH-04 | FS-MTH-04 |
| URS-MTH-05 | FS-MTH-05 |
| URS-SMP-01 | FS-SMP-01 |
| URS-SMP-02 | FS-SMP-02 |
| URS-RUN-01 | FS-RUN-01 |
| URS-RUN-02 | FS-RUN-02 |
| URS-RUN-03 | FS-RUN-03 |
| URS-RUN-04 | FS-RUN-04 |
| URS-GLP-01 | FS-GLP-01 |
| URS-GLP-02 | FS-GLP-02 |
| URS-GLP-03 | FS-GLP-03 |
| URS-GLP-04 | FS-GLP-04 |
| URS-GLP-05 | FS-GLP-05 |
| URS-GLP-06 | FS-GLP-06 |
| URS-GLP-07 | FS-GLP-07 |
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
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-INT-CDS-01 | FS-INT-CDS-01 |
| URS-INT-ELN-01 | FS-INT-ELN-01 |
| URS-INT-ETMF-01 | FS-INT-ETMF-01 |
| URS-INT-INST-01 | FS-INT-INST-01 |
| URS-INT-ARCH-01 | FS-INT-ARCH-01 |
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
| URS-INS-01 | FS-INS-01 |
| URS-INS-02 | FS-INS-02 |
| URS-SAMP-01 | FS-SAMP-01 |
| URS-SAMP-02 | FS-SAMP-02 |
| URS-SAMP-03 | FS-SAMP-03 |
| URS-SAMP-04 | FS-SAMP-04 |
| URS-SAMP-05 | FS-SAMP-05 |
| URS-SAMP-06 | FS-SAMP-06 |
| URS-STD-01 | FS-STD-01 |
| URS-STD-02 | FS-STD-02 |
| URS-STD-03 | FS-STD-03 |
| URS-STD-04 | FS-STD-04 |
| URS-STD-05 | FS-STD-05 |
| URS-LBA-01 | FS-LBA-01 |
| URS-LBA-02 | FS-LBA-02 |
| URS-LBA-03 | FS-LBA-03 |
| URS-LBA-04 | FS-LBA-04 |
| URS-LBA-05 | FS-LBA-05 |
| URS-ISR-01 | FS-ISR-01 |
| URS-ISR-02 | FS-ISR-02 |
| URS-ISR-03 | FS-ISR-03 |
| URS-ISR-04 | FS-ISR-04 |
| URS-RVW-01 | FS-RVW-01 |
| URS-RVW-02 | FS-RVW-02 |
| URS-RVW-03 | FS-RVW-03 |
| URS-RVW-04 | FS-RVW-04 |
| URS-REL-01 | FS-REL-01 |
| URS-REL-02 | FS-REL-02 |
| URS-REL-03 | FS-REL-03 |
| URS-REL-04 | FS-REL-04 |
| URS-RPT-01 | FS-RPT-01 |
| URS-RPT-02 | FS-RPT-02 |
| URS-RPT-03 | FS-RPT-03 |
| URS-RPT-04 | FS-RPT-04 |
| URS-RPT-05 | FS-RPT-05 |
| URS-ARC-01 | FS-ARC-01 |
| URS-ARC-02 | FS-ARC-02 |
| URS-ARC-03 | FS-ARC-03 |
| URS-ARC-04 | FS-ARC-04 |
| URS-ARC-05 | FS-ARC-05 |
| URS-IRT-01 | FS-IRT-01 |
| URS-IRT-02 | FS-IRT-02 |
| URS-IRT-03 | FS-IRT-03 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-LYR-01 | FS-XINT-LYR-01 |
| URS-XINT-LYR-02 | FS-XINT-LYR-02 |
| URS-XINT-LYR-03 | FS-XINT-LYR-03 |
| URS-XINT-LYR-04 | FS-XINT-LYR-04 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Run-acceptance defect — invalid run released as passing | Low | Critical | URS-RUN-02 (ICH M10 automated check) |
| R-02 | ISR mis-evaluation | Medium | High | URS-RUN-03 |
| R-03 | GLP archive integrity loss | Low | Critical | URS-GLP-06, URS-AUD-04 |
| R-04 | Method-status drift — non-validated method used for regulated sample | Low | Critical | URS-MTH-01, URS-MTH-04 |
| R-05 | Study Director signature delegated inappropriately | Low | Critical | URS-GLP-01, URS-PART11-06 |
| R-06 | QAU dependence on operations | Low | High | URS-GLP-02 (independent access) |
| R-07 | Audit-trail tampering | Low | Critical | URS-AUD-02 |
| R-08 | Sample chain-of-custody gap | Medium | High | URS-SMP-01, URS-SMP-02 |
| R-09 | Empower CDS integration drift | Medium | Medium | URS-INT-CDS-01 (checksums) |
| R-10 | Re-analysis policy mis-applied | Low | High | URS-RUN-04 |
| R-11 | Backup restore failure | Low | High | URS-BAK-02 |
| R-12 | Inspection-export latency exceeds business expectation | Low | Medium | URS-INS-01 |
| R-13 | GLP-archive deletion before retention period (system or operator error) | Low | Critical | URS-ARC-04 (system-level deletion block) |
| R-14 | Study-protocol amendment not pinned to in-flight samples | Low | Critical | URS-STD-02 |
| R-15 | ISR sample mis-categorised between clinical (10%) and non-clinical (7%) — FDA WL precedent (PPD Bioanalytical 2021, citing ISR documentation gaps) | Medium | High | URS-ISR-01 |
| R-16 | LBA matrix-effect under-evaluation (matrix-bound parallelism not tested per ICH M10 § 4) | Medium | High | URS-MTH-03 + URS-LBA-02 |
| R-17 | Immunogenicity titer ladder computed against wrong cut-point | Low | Critical | URS-LBA-03 |
| R-18 | Multi-site PI sign-off cycle stall (PI on a remote site does not sign within window) | Medium | Medium | URS-STD-05 + workflow timeout monitor |
| R-19 | Freeze/thaw budget silently exceeded (aliquot re-used past max cycles) | Medium | High | URS-SAMP-03 |
| R-20 | Sample-shipping cold-chain excursion mid-transit not captured | Medium | High | URS-SAMP-06 |

Full evaluation in `CET-RA-WATSON-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
