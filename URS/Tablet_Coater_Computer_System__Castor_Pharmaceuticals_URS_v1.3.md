---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline batch, 2026-04-27; v1.2 enrichment 2026-05-13"
seed_corpus_basis:
  - "GAMP 5 (2nd ed.) Cat 4 conventions for configured equipment-control systems"
  - "21 CFR Part 11; 21 CFR Part 211; EU GMP Annex 11; ICH Q9; ICH Q14; PIC/S PI 041"
  - "ANSI/ISA-88 (batch control); USP <1151> Pharmaceutical Dosage Forms; USP <711> Dissolution"
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

## Tablet Coater Computer System — Glatt GC Smart 1500 + GlattView 5

**Document Number:** CST-URS-COATER-001
**Version:** 1.2
**Effective Date:** 2026-05-13 *(synthetic)*
**Site:** Castor Pharmaceuticals Pvt. Ltd., Solid Oral Dosage Plant 2, Hyderabad, India *(fictional)*
**System Owner:** Coating Process Engineer
**Process Owner:** Head of Solid Oral Dosage Manufacturing
**System Class (GAMP 5, 2nd ed.):** Category 4 — Configured Product
**Project Mode:** Configuration project on commercial software product **Glatt GC Smart 1500 + GlattView 5** (GAMP 5 Category 4 — Configured Product).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .180, .192; EU GMP Annex 11 §§ 4, 6, 9, 11; ICH Q9(R1); ICH Q14 (Analytical Procedure Development — for NIR endpoint); PIC/S PI 041; ANSI/ISA-88 Part 1 + Part 2 (batch control); USP <1151>

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Coating Process Engineer) | _____________ | _____________ | _____ |
| Reviewer (Process Sciences / PAT) | _____________ | _____________ | _____ |
| Reviewer (IT / Automation) | _____________ | _____________ | _____ |
| Approver (Head of SOD Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Risk-table reformatted to 5-column shape per v1.1 mechanical sweep. |
| 1.2 | 2026-05-13 | (synthetic) | Tier T2 enrichment. Expanded Part-11 + ALCOA+ rows from collapsed range. Added recipe-parameter detail, NIR endpoint, batch genealogy linkage, pan-cleaning/CIP, solvent-recovery (organic-coater variant), ANSI/ISA-88 phase model. Citations updated per METHODOLOGY § 2A.1. |

## Definitions

| Term | Definition |
|---|---|
| Tablet Coater | Glatt GC Smart 1500 perforated drum coater (production-scale, ~50-200 kg batch) |
| GlattView 5 | Glatt's HMI / data-management software, version 5 |
| PLC | Allen-Bradley ControlLogix 5580 (embedded in coater) |
| HMI | Human-Machine Interface (GlattView OperatorPanel) |
| MES | Werum / Körber PAS-X v3.2 |
| Spray Rate | Coating-suspension delivery (g/min) |
| Atomising Pressure | Spray-gun atomising-air pressure (bar) |
| LOD | Loss On Drying — moisture-content endpoint surrogate |
| NIR | Near-Infrared spectroscopy (on-line PAT) |
| ISA-88 | ANSI/ISA-88 batch-control standard (procedure → unit procedure → operation → phase) |
| ALCOA+ | Attributable, Legible, Contemporaneous, Original, Accurate (+ Complete, Consistent, Enduring, Available) |
| CIP | Cleaning In Place |
| LDT | Local Data Terminal — workstation running GlattView 5 |

## 1. Purpose

This URS defines requirements for the tablet-coater computer system that controls and records the film-coating process on solid oral dosage tablets at Castor Plant 2. The system handles both aqueous coating (HPMC / PVA seal-coats, taste-mask coats, modified-release polymer coats — Kollicoat-class) and, on the organic-coater variant (`COATER-LINE-2`), solvent-based functional coatings with closed-loop solvent recovery.

## 2. Scope

**In scope:**

- Glatt GC Smart 1500 cabinet (perforated drum coater, configurable drum 1300-1700 mm diameter).
- Embedded Allen-Bradley ControlLogix 5580 PLC + Glatt-designed I/O modules.
- GlattView 5 supervisory software on a redundant LDT pair (Win 11 IoT LTSC).
- Coating-data Historian (InfluxDB) with Grafana viz.
- Integrations: PAS-X (recipe / batch report), site BMS (room-pressure interlock), AD authentication.
- Optional NIR PAT probe (Bruker MATRIX-F on `COATER-LINE-1` only) for end-point detection of seal-coat / functional-coat thickness.
- Solvent-recovery interlock (organic-coater variant only) — flammable-atmosphere monitoring on exhaust.

**Out of scope:**

- Mechanical / spray-gun / drying-air hardware (handled under `EQ-COATER-001`).
- Validated cleaning cycles (`CLEAN-COATER-001`); product-specific coating recipes (`PROC-DEV-PROD-XXX`).
- NIR chemometric model development + lifecycle (`PAT-MODEL-LCM-001`) — model is consumed by this system but governed separately.
- Solvent-recovery condenser / blower hardware (separate utility validation).

## 3. System Description and Intended Use

The system controls and records the coating cycle (warming → spraying → drying → cooling) for solid oral dosage tablets per ISA-88 batch control. Recipes are downloaded from PAS-X for each batch; cycle data (drum speed, inlet / exhaust air temperature, spray rate, atomising pressure, product temperature, exhaust humidity, NIR thickness — where applicable) is recorded at ≥ 1 Hz; deviations from setpoint envelopes raise alarms.

When NIR PAT is in scope, the system consumes thickness predictions and uses them to (a) inform endpoint decision per a validated chemometric model, and (b) trigger spray termination when the model-predicted thickness reaches the recipe target.

On completion, an executed-batch report is pushed to PAS-X and the batch is gated for downstream operations (packaging / dissolution release testing).

GAMP Cat 4: Glatt maintains the GlattView SDLC; the embedded PLC code is supplier-validated; site validation focuses on installation, configuration, recipe-handling functionality, integrations, Part 11 controls, and the NIR-feedback control path.

## 4. User Roles

| Role | Permissions |
|---|---|
| Operator | Load recipe (from approved set); start / pause / abort cycle; document in-process events. |
| Senior Operator / Line Lead | All Operator + second-person verification of critical events (loading complete, spray complete, NIR endpoint accept). |
| Recipe Author | Create / edit recipes in DRAFT under change control. |
| Recipe Reviewer | Review recipes; cannot approve own. |
| Recipe Approver (QA) | Approve recipes to EFFECTIVE; retire. |
| Coating Process Engineer | Recipe parameter sign-off; NIR-model version sign-off; scale-up parameter approval. |
| PAT Scientist | NIR model deployment + model-life decisions; cannot approve recipe. |
| Maintenance Engineer | Run diagnostic / CIP cycles; cannot run product cycles. |
| Quality Reviewer | Per-batch review; gates batch report to PAS-X downstream. |
| QA Compliance | Quarterly audit-trail / platform review. |
| System Administrator | Patching, AD groups, historian admin; no recipe approval. |
| Auditor | Read-only across all records and audit trails. |

Separation of duties: Operator ≠ Verifier on the same critical step; Recipe Author ≠ Approver of same recipe; PAT Scientist ≠ Recipe Approver on the same recipe.

## 5. User Requirements

### 5.1 Platform / Hardware

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PLAT-01 | H | R1 | Active / standby LDT pair with automatic failover ≤ 30 s. |
| URS-PLAT-02 | H | R1 | LDTs on UPS sized for ≥ 30 min controlled cycle hold; PLC + HMI on separate UPS branch. |
| URS-PLAT-03 | H | R1 | All LDTs and historian on a dedicated process-control VLAN; no office-network access. |
| URS-PLAT-04 | M | R2 | Historian retains ≥ 5 years online; archived to immutable cold storage. |

### 5.2 Recipe / Spray-Parameter Lifecycle

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-REC-01 | H | R1 | Recipes shall follow DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE. |
| URS-REC-02 | H | R1 | Only EFFECTIVE recipes may be loaded for product cycles. |
| URS-REC-03 | H | R1 | Recipe transitions shall require electronic signatures with role + SoD enforcement. |
| URS-REC-04 | H | R1 | EFFECTIVE recipes shall be immutable; changes shall create a new revision via change control. |
| URS-REC-05 | H | R1 | Recipe download from PAS-X shall validate checksum (SHA-256) + version against the local approved-recipe registry; mismatch shall block the cycle. |
| URS-REC-06 | H | R1 | Recipe schema shall capture coating-class parameters: drum speed (rpm), inlet-air temperature setpoint + tolerance (°C), exhaust-air temperature target (°C), spray rate setpoint + tolerance (g/min), atomising pressure setpoint (bar), gun-to-bed distance (mm), nozzle configuration, batch quantity (kg), target weight gain (%). |
| URS-REC-07 | H | R1 | Coating-class scale-up parameters (developed under DoE per ICH Q14) shall be referenced from the recipe with the source DoE-doc-ID; recipe approval shall require the Coating Process Engineer's signature attesting to scale-up validity. |
| URS-REC-08 | M | R2 | Recipe-diff renderer shall present field-by-field old/new on revision review. |

### 5.3 ANSI/ISA-88 Phase Model

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-S88-01 | H | R1 | The cycle execution shall follow ANSI/ISA-88 procedure model: Procedure (full coat run) → Unit Procedure (coat / dry / cool) → Operation (warm-up, spray-on, spray-finish, drying) → Phase (heat, spray, dwell, cool); state transitions logged. |
| URS-S88-02 | H | R1 | Phase transitions (warm-up → spray, spray → drying, drying → cooling) shall require setpoint convergence within recipe-defined band before proceeding; non-convergence shall hold the phase + raise warning. |
| URS-S88-03 | M | R2 | Operator pause shall flip the current phase to HELD per ISA-88 state model; resume shall require Senior Operator countersignature. |

### 5.4 Cycle Execution / Data Capture

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CYC-01 | H | R1 | The system shall execute the loaded recipe per its setpoint envelope; deviations shall trigger alarms classified by severity. |
| URS-CYC-02 | H | R1 | Critical alarms (loss of spray, drum-motor fault, exhaust-temperature OOE > 2 min, atomising-pressure loss, NIR-loss with feedback control active) shall be acknowledged with reason; unacknowledged criticals shall block cycle progression. |
| URS-CYC-03 | H | R1 | Drum speed, inlet air temperature, exhaust air temperature, spray rate, atomising pressure, gun-pump stroke counts, product temperature (where instrumented), exhaust humidity shall be recorded at ≥ 1 Hz. |
| URS-CYC-04 | H | R1 | Timestamps shall be PLC-derived (PTP master); LDT clock skew shall be checked at cycle start + end (> 1 s shall trigger a cycle-quality flag). |
| URS-CYC-05 | H | R1 | Manual setpoint override during a product cycle shall require Operator + Coating Process Engineer dual signature with reason captured; auto-deviation shall be raised. |
| URS-CYC-06 | H | R1 | Loading-complete and spray-complete events shall be critical-step verification points requiring second-person countersignature. |
| URS-CYC-07 | M | R2 | Cycle abort sequence shall safe the system (spray off, atomising-air off, drum coasted to safe speed, drying air maintained until product temp ≤ recipe limit). |
| URS-CYC-08 | M | R2 | Cumulative coating-suspension dispensed mass shall be tracked + compared to recipe target ± tolerance; out-of-tolerance dispense at spray-complete shall trigger investigation. |

### 5.5 NIR Endpoint Detection (Process Analytical Technology)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-NIR-01 | H | R1 | When recipe specifies NIR endpoint control, the system shall consume thickness predictions from the NIR PAT instrument via OPC UA at the validated cadence (typically 1-10 Hz). |
| URS-NIR-02 | H | R1 | Endpoint determination shall use the configured chemometric model (referenced by model-id + version); model load shall verify cryptographic signature + version match. |
| URS-NIR-03 | H | R1 | Loss of NIR signal during NIR-controlled spray shall trigger a critical alarm; the system shall fall back to time-based spray-end per the recipe's contingency parameters and the cycle shall require Coating Process Engineer disposition before release. |
| URS-NIR-04 | H | R1 | NIR-driven spray-end decision shall be deterministic, repeatable, and reconstructable from logged input spectra + model version + decision threshold. |
| URS-NIR-05 | M | R2 | NIR model deployment shall require PAT Scientist + Coating Process Engineer + QA signature with model-validation-doc reference. |

### 5.6 Pan Cleaning / CIP

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-CIP-01 | H | R1 | The system shall support automated CIP cycles (pre-rinse → caustic wash → rinse → acid wash → final rinse) with phase recording analogous to product cycles. |
| URS-CIP-02 | H | R1 | CIP cycle data (rinse-water conductivity, final-rinse TOC where instrumented) shall be recorded; failure of acceptance criteria shall block subsequent product cycles. |
| URS-CIP-03 | M | R2 | A "campaign-end CIP" workflow shall require Coating Process Engineer + Quality Reviewer sign-off before the next product campaign starts. |

### 5.7 Solvent-Recovery Interlock (Organic-Coater variant)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-SOLV-01 | H | R1 | On the organic-coater variant, the system shall consume LEL (Lower Explosive Limit) signals from the flammable-atmosphere monitoring system; LEL ≥ 25% shall trigger an emergency-stop interlock isolating spray + ramping drying-air. |
| URS-SOLV-02 | H | R1 | Solvent-recovery condenser exhaust temperature and condensate-mass-flow shall be recorded; out-of-envelope values shall raise alarms. |
| URS-SOLV-03 | M | R2 | Solvent-batch genealogy (fresh solvent lot + recovered solvent batch reference) shall be recorded per coating campaign. |

### 5.8 Batch Genealogy Linkage

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-GEN-01 | H | R1 | Each cycle record shall be bound to the PAS-X EBR via batch-ID + step-ID; the EBR shall not allow downstream steps (e.g., packaging) until the coating cycle report is received + Quality-Reviewer-approved. |
| URS-GEN-02 | H | R1 | Coating-suspension lot, sub-coat lots (where multi-layer), and tablet-core lot shall be captured as input genealogy. |
| URS-GEN-03 | M | R2 | Cycle report shall include weight-gain calculation: (post-coat tablet weight − pre-coat tablet weight) / pre-coat weight, with target + actual + ± tolerance. |

### 5.9 Audit Trail

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-AUD-01 | H | R1 | The system shall maintain a contemporaneous, time-stamped, secure audit trail covering recipe events, cycle events, alarm acknowledgements, signature events (Annex 11 § 9). |
| URS-AUD-02 | H | R1 | The audit trail shall be append-only; no user shall be able to edit or delete entries. |
| URS-AUD-03 | H | R1 | Audit-trail review shall be performed by Quality Reviewer per batch and QA Compliance quarterly. |
| URS-AUD-04 | H | R1 | Retention ≥ 25 years from product expiry. |

### 5.10 21 CFR Part 11 / Annex 11

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-PART11-01 | H | R1 | Electronic signatures shall meet 21 CFR § 11.50: printed name + date / time + meaning rendered in human-readable form. |
| URS-PART11-02 | H | R1 | Each signature shall be unique per 21 CFR § 11.100; user IDs shall not be reused. |
| URS-PART11-03 | H | R1 | Signatures shall be cryptographically bound to the signed record per 21 CFR § 11.70. |
| URS-PART11-04 | H | R1 | Separation of duties shall be enforced per 21 CFR § 11.10(d) and § 11.10(g). |
| URS-PART11-05 | H | R1 | Re-authentication at signing shall be required per 21 CFR § 11.200. |
| URS-PART11-06 | H | R1 | Password / credential controls shall meet 21 CFR § 11.300. |
| URS-PART11-07 | H | R1 | Operational audit trail per § 11.10(e); accurate-and-complete copies per § 11.10(b); record protection per § 11.10(c). |

### 5.11 Data Integrity (ALCOA+)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-DI-01 | H | R1 | Records shall be Attributable to a named AD user. |
| URS-DI-02 | H | R1 | Records shall be Legible — exportable as structured PDF + CSV. |
| URS-DI-03 | H | R1 | Records shall be Contemporaneous — PLC-derived PTP-synchronised timestamps. |
| URS-DI-04 | H | R1 | Original cycle data shall be preserved unaltered; derivations shall reference (not overwrite) originals. |
| URS-DI-05 | H | R1 | Spray-mass and weight-gain calculations shall be Accurate per OQ. |
| URS-DI-06 | M | R2 | Records shall be Complete, Consistent, Enduring (25-yr retention), Available (≤ 4 h during inspection). |

### 5.12 Integrations / Performance / Backup / Security

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-INT-PASX-01 | H | R1 | Recipe download from PAS-X via REST over mTLS; checksum + version validated. |
| URS-INT-PASX-02 | H | R1 | Executed-batch report shall be pushed to PAS-X within 30 minutes of cycle end. |
| URS-INT-PASX-03 | H | R1 | The PAS-X EBR downstream-step gate shall not clear until the Quality Reviewer approves the cycle report. |
| URS-INT-BMS-01 | H | R1 | BMS room-pressure interlock shall be consumed; loss shall abort loading. |
| URS-INT-PAT-01 | H | R1 | NIR PAT signal consumed via OPC UA over mTLS (where in scope); loss shall trigger the URS-NIR-03 contingency. |
| URS-INT-AD-01 | H | R1 | All authentication shall be via AD; service accounts via credential vault. |
| URS-PERF-01 | H | R1 | Sustained ≥ 1 Hz logging across all critical channels for full cycle (typical 2-6 h). |
| URS-PERF-02 | M | R2 | HMI alarm-ack latency shall be ≤ 1 s. |
| URS-BAK-01 | H | R1 | Historian nightly backup with PITR; retention 25 y. |
| URS-BAK-02 | H | R1 | Quarterly restore test, witnessed. |
| URS-BAK-03 | M | R2 | RTO ≤ 4 h; RPO ≤ 1 min. |
| URS-SEC-01 | H | R1 | AD-managed accounts; break-glass admin only. |
| URS-SEC-02 | H | R1 | Removable media blocked except vendor-approved engineering use under CR. |
| URS-SEC-03 | M | R2 | Vulnerability scans monthly; criticals remediated in 30 days. |

### 5.13 Training / Periodic Review

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-TRN-01 | H | R1 | LMS-recorded role-specific training shall gate production access. |
| URS-TRN-02 | M | R2 | Annual refresher; PAT Scientist competency assessment additionally. |
| URS-PR-01 | H | R1 | Annual periodic review covering recipe inventory, alarm trends, audit-trail review evidence, deviation summary, NIR-model-version register, CIP-cycle outcomes, training currency; signed by Coating Engineer + Head of SOD Mfg + Head of QA. |

### 5.14 Cross-System Integration (Identity + Backup)

| ID | Pri | Risk | Requirement |
|---|---|---|---|
| URS-XSYS-AD-01 | H | R1 | Authentication, unique-user-identity, and authorisation-group binding shall be sourced from the central Active Directory Identity Service per `QTZ-URS-AD-001` (or the local site-equivalent AD identity service); integration mode is LDAPS on-prem with local OT cached credentials for offline operation; conditional-access policy `OT-Equipment Conditional Access (MFA at HMI session start; local cache validates last 24 h)` shall be enforced; authentication and signature events shall be forwarded to the central SIEM (Splunk) within 5 minutes for 21 CFR § 11.10(e) review; no local production accounts shall be created outside the documented break-glass procedure per `QTZ-URS-AD-001` URS-PAM-* and the site PAM policy. |
| URS-XSYS-BAK-01 | H | R1 | The system shall be enrolled in the centralised GxP backup service per `AUR-URS-BACKUP-001` at backup tier T2 with RPO ≤ 24 h and RTO ≤ 24 BH; backup integration shall use Veeam Application-Aware processing with MS SQL Server VSS for the recipe / cycle DB plus file-level capture of electronic batch records; the application team shall participate in quarterly application-level restore tests per `AUR-URS-BACKUP-001` URS-TEST-02 with QA-witnessed restore certificates retained as quality records; an immutable cloud-tier copy in S3 Object Lock Compliance mode and an air-gap LTO-9 monthly rotation shall be provided per `AUR-URS-BACKUP-001`; record-class retention shall align with ≥ 15 y (batch-history) per the consuming-record schedule. |

## 6. Acceptance Criteria

The system shall enter validated GMP use when CS, RA, IQ, OQ, PQ approved and executed; PQ shall include: ≥ 3 representative product cycles (aqueous coat); ≥ 1 organic-coater cycle (variant only); ≥ 1 NIR-controlled cycle (where in scope); ≥ 1 CIP cycle; 1 LDT failover; 1 alarm scenario; 1 manual override; cycle-report flow to PAS-X verified. VSR approved.

## 7. Constraints

- Glatt patches under change control.
- PLC firmware changes require revalidation per `EQ-COATER-001`.
- NIR chemometric model changes require revalidation per `PAT-MODEL-LCM-001`.
- Recipe parameter changes affecting scale-up DoE require Coating Process Engineer sign-off + PQ revalidation.

## 8. Assumptions

- PAS-X, BMS, AD, PTP master are validated infrastructure.
- NIR instrument is qualified under `EQ-NIR-COATER-001`.
- Solvent-recovery utility (organic variant) is qualified under `UTIL-SOLV-001`.

## 9. References

### US — FDA
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .68, .180, .192.
- FDA *Guidance for Industry — PAT: A Framework for Innovative Pharmaceutical Development, Manufacturing, and Quality Assurance* (2004).
- FDA *Computer Software Assurance for Production and Quality Management System Software* (final, February 2026).

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- EudraLex Vol 4 Part I § 5 (Production).

### International — ICH / ISO / USP
- ICH Q9(R1) — Quality Risk Management.
- ICH Q14 — Analytical Procedure Development (governs NIR chemometric model lifecycle).
- ICH Q8(R2) — Pharmaceutical Development.
- USP <1151> — Pharmaceutical Dosage Forms.
- USP <711> — Dissolution (downstream release-test linkage).
- ANSI/ISA-88 Part 1 + Part 2 — Batch Control.
- ANSI/ISA-95 Part 1 — Enterprise-Control System Integration.

### Industry guidance
- ISPE GAMP 5 (2nd Edition, 2022).
- PIC/S PI 041 — Good Practices for Data Management and Integrity.
- ISPE Baseline Guide *Oral Solid Dosage Forms* (2nd ed.).

### Vendor
- Glatt — *GC Smart 1500 + GlattView 5 Configuration Reference*.
- Glatt — *Coating Recipe Design Theory of Operation*.
- Bruker — *MATRIX-F NIR Spectrometer Operation Manual* (where in scope).

### Site
- `EQ-COATER-001` — coater equipment qualification.
- `PAT-MODEL-LCM-001` — NIR chemometric model lifecycle.
- `UTIL-SOLV-001` — solvent-recovery utility validation (organic variant).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**

