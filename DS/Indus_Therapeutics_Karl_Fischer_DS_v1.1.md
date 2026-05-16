---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring 2026-05-15 (Chunk A Karl Fischer — Cat 3 thin)"
seed_corpus_basis:
  - "IND-FS-CKF-001 v1.2 (parent FS)"
  - "IND-URS-CKF-001 v1.2 (transitive parent URS)"
  - "GAMP 5 (2nd Edition) Category 3 — Vendor-Design-Reliance Statement variant"
  - "21 CFR Part 11; EU GMP Annex 11; USP <921> Method Ic; USP <1058>; Ph. Eur. 2.5.32"
  - "Mettler Toledo — C30S Coulometric KF Configuration Reference (vendor doc)"
  - "Mettler Toledo — LabX 2024 Installation, Configuration, and Administration Reference (vendor doc)"
  - "Mettler Toledo — LabX 2024 21 CFR Part 11 Compliance Guide (vendor doc)"
parent_fs:
  document_number: IND-FS-CKF-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Indus_Therapeutics_Karl_Fischer_FS_v1.3.md
parent_urs:
  document_number: IND-URS-CKF-001
  version: 1.2
  file: ../../../URS/_generated/final/Coulometric_Karl_Fischer_Computer_System__Indus_Therapeutics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Design Specification (Vendor-Design-Reliance Statement)

## Coulometric Karl Fischer Computer System — Mettler Toledo C30S + LabX 2024

**Document Number:** IND-DS-CKF-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** IND-FS-CKF-001 v1.2 | **Parent URS:** IND-URS-CKF-001 v1.2 *(informational, transitive)*
**Site:** Indus Therapeutics Pvt Ltd, QC Chemical Lab, Hyderabad, India *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 3 — Non-Configurable COTS (the Mettler Toledo C30S + LabX 2024 baseline relies on the vendor's design with only site-binding configuration on top — full vendor design documentation is incorporated by reference, not redrawn here per METHODOLOGY § 2B.6; site Categorisation Decision `IND-CAT-CKF-001`).
**Project Mode:** Configuration project on non-configurable instrument / appliance **Mettler Toledo C30S + LabX 2024** (GAMP 5 Category 3 — Non-Configurable COTS).
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .160, .165, .194; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <921> Method Ic; USP <1058>; Ph. Eur. 2.5.32; ICH Q2(R2); PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Chemical) | _____________ | _____________ | _____ |
| Reviewer (KF SME / Method Owner) | _____________ | _____________ | _____ |
| Approver (Head of QC) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue. Inherited Tier T1 from parent URS+FS pair. DS covers 26/57 FS-IDs from the site-binding surface; 31 FS-IDs flagged as vendor-internal — no site design surface (covered transitively by Mettler Toledo LabX 2024 design documentation per § 4 inventory: FS-AUD-01, FS-AUD-02, FS-PART11-03..07, FS-CMP-01, FS-AIQ-02 (vendor portion), FS-AIQ-03 (vendor portion), FS-METH-01, FS-METH-02 vendor engine, FS-RUN-01..04 LabX engines, FS-PROC-01..04 LabX engines, FS-DI-01..05 LabX defaults, FS-SST-01..05 LabX SST engine). |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from `IND-FS-CKF-001` and `IND-URS-CKF-001`. DS-specific terms:

| Term | Definition |
|---|---|
| Vendor-Design-Reliance Statement | Cat 3 thin DS variant — relies on vendor design documentation by reference (METHODOLOGY § 2B.6) |
| Authority Set | LabX 2024 internal role bundle mapped 1:1 to AD group |
| Reagent Register | Site reagent register tracking anolyte / catholyte / water-standard lots |
| Drift | Background-water rate (µg H₂O / min); USP <921> threshold ≤ 25 µg/min routine |
| `wel-ckf` | Splunk heavy-index name reserved for this system |

## 1. Purpose

This DS records the site's reliance on Mettler Toledo's vendor design for the C30S + LabX 2024 system, plus the small site-specific bindings (network attachment, AD binding, site reagent register, NTP source, anti-malware policy) that satisfy the functional behaviour specified in `IND-FS-CKF-001` v1.2. The full design of the LabX 2024 application (audit-trail engine, eSign engine, SST engine, calibration engine, report renderer) is owned by Mettler Toledo under their internal SDLC and is incorporated here by reference to the controlled vendor design documents enumerated in § 4. The site does not redraw vendor internals — the Cat 3 thin DS posture (METHODOLOGY § 2B.6) keeps the artefact at the binding context only.

## 2. Scope

### 2.1 In scope

- Vendor design documentation inventory (§ 4) — the authoritative design surface lives in Mettler Toledo's controlled documents.
- Site-specific integration design (§ 5) — network attachment, AD binding, NTP, file-share, anti-malware, LIMS Connector binding.
- Site-specific configuration (§ 6) — site name, site time-zone, user / AD-group mapping, reagent / water-standard register entries, SST thresholds bound to site method library.

### 2.2 Out of scope

- LabX 2024 internal design (audit-trail engine, eSign engine, SST engine, calibration engine, oxidation calculation, report renderer) — Mettler SDLC owns this; vendor design documents in § 4 are the authoritative artefacts.
- C30S firmware design (cell control, electrode control, current measurement, stoichiometry calc) — Mettler SDLC.
- LIMS-side sample lifecycle (separate validation).

## 3. Architectural Overview

The site binds LabX 2024 to the site-managed infrastructure stack with the smallest possible configuration surface. The figure expands FS § 3 with the four site-binding touchpoints (italic CI-XX refers to § 6 rows):

```
                AD `indus.local` (CI-12, qualified infra)
                │
                ▼ LDAPS bind
   ┌─────────────────────────────────────────────────────────┐
   │ LabX 2024 Workstation (Lenovo ThinkCentre M70t)         │
   │   Win 11 Pro 23H2 + GPO `IND-LAB-USERS-WS`              │
   │   ┌─────────────────────────────────────────────────┐   │
   │   │ Mettler Toledo LabX 2024 (vendor app)            │  │
   │   │   Authority Sets mapped to AD groups (CI-15..21) │  │
   │   │   Method `IND-METH-USP921-IC` (CI-25)            │  │
   │   │   Reagent Register (CI-30..33)                   │  │
   │   │   SST workflow `IND-SST-DRIFT` (CI-35..37)        │  │
   │   │   LIMS Connector → LIMS (CI-40..43)              │  │
   │   └────┬───────────────────────────────────────────┘    │
   │        │ USB-3 to C30S titrator                         │
   └────────┼─────────────────────────────────────────────────┘
            │
            ├──► NTP `ntp.indus.local` (CI-14)
            ├──► SMB `\\ind-gmp-fs01\labx-projects` (CI-13)
            ├──► TCP/9997 → Splunk UF index `wel-ckf` (CI-22)
            └──► HTTPS → LabWare LIMS 8 (CI-40)
```

## 4. Vendor Design Documentation Inventory

The authoritative design of LabX 2024 + C30S lives in Mettler Toledo's controlled documents enumerated below. Each entry is incorporated by reference into the site validation dossier `IND-VAL-CKF-001`; the site does not redraw vendor internals.

| Vendor doc title | Version | Vendor doc number | Site DMS reference | Retention class |
|---|---|---|---|---|
| Mettler Toledo — *LabX 2024 Installation, Configuration, and Administration Reference* | rev. 2024-09 | MT-LABX-INST-2024-09 | `IND-DMS-VEND-001` | 7 y product-release-linked |
| Mettler Toledo — *LabX 2024 21 CFR Part 11 Compliance Guide* | rev. 2024-09 | MT-LABX-P11-2024-09 | `IND-DMS-VEND-002` | 7 y product-release-linked |
| Mettler Toledo — *C30S Coulometric KF Hardware Reference + Maintenance Guide* | rev. 2024-06 | MT-C30S-HW-2024-06 | `IND-DMS-VEND-003` | 7 y |
| Mettler Toledo — *C30S Firmware SDLC Statement* | rev. 2024-06 | MT-C30S-SDLC-2024-06 | `IND-DMS-VEND-004` | 7 y |
| Mettler Toledo — *LabX 2024 LIMS Connector Reference* | rev. 2024-09 | MT-LABX-LIMS-2024-09 | `IND-DMS-VEND-005` | 7 y |
| Mettler Toledo — *LabX 2024 Audit-Trail + eSign Engine Compliance Evidence* | rev. 2024-09 | MT-LABX-AUDIT-2024-09 | `IND-DMS-VEND-006` | 7 y |
| Mettler Toledo — *LabX 2024 Method Library + State Machine Reference* | rev. 2024-09 | MT-LABX-METHOD-2024-09 | `IND-DMS-VEND-007` | 7 y |
| Mettler Toledo — *USP <921> Method Ic Application Note* | rev. 2024-08 | MT-APN-USP921-2024 | `IND-DMS-VEND-008` | 7 y |
| Mettler Toledo — *Ph. Eur. 2.5.32 Application Note* | rev. 2024-08 | MT-APN-EP2532-2024 | `IND-DMS-VEND-009` | 7 y |
| Mettler Toledo — *LabX 2024 Hotfix / SP Release Notes* (rolling) | rolling | MT-LABX-SCN-* | `IND-DMS-VEND-010` | 7 y (rolling) |

**Reliance statement (per METHODOLOGY § 2B.6 / § 2A.10):** The site relies on Mettler Toledo's vendor-side SDLC for the design of: oxidation calculation engine (Method Ic stoichiometry), audit-trail event schema + append-only enforcement, eSign cryptographic linking, method state-machine engine, SST workflow engine (drift + water-standard recovery sub-steps), report renderer, LIMS Connector internals. The site provides only the bindings enumerated in §§ 5 and 6 below. Vendor SDLC evidence is collected during vendor audit `IND-VENAUDIT-MT-2025`.

## 5. Site-Specific Integration Design

The site provides exactly five integration bindings; each is a thin wrapper around vendor-provided endpoints.

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| CI-10 | LabX → Network attachment | Win 11 LTSC/Pro 23H2 on lab-IT VLAN `vlan-ckf-lab` | Custom | Per FS-HW-02 / FS-SW-01; segregates from office network. | FS-SW-01, FS-HW-02 | IQ-NW-01 |
| CI-11 | LabX → Anti-malware exclusion list | Mettler-approved LabX paths (CrowdStrike Falcon) | Custom | Per Mettler MT-LABX-INST-2024-09 § 5.3 recommendation; prevents acquisition interference. | (vendor-recommended) | IQ-AV-01 |
| CI-12 | LabX → AD bind | LDAPS `ldaps://indus.local:636`; AD groups `IND-CKF-*` | Custom | Per FS-SW-01 / FS-SEC-01 / FS-XSYS-AD-01. | FS-SW-01, FS-SEC-01, FS-XSYS-AD-01 | IQ-AD-01 |
| CI-13 | LabX → Project storage share | `\\ind-gmp-fs01\labx-projects` (SMB 3.1.1, encrypted, NetApp SnapLock 7y) | Custom | Per FS-SW-03 / FS-AUD-04. | FS-SW-03, FS-AUD-04 | IQ-FS-01 |
| CI-14 | LabX → NTP source | `ntp.indus.local`; skew threshold 1 s | Custom | Per FS-SW-04. | FS-SW-04 | IQ-NTP-01 |
| CI-22 | LabX → SIEM forwarder | Splunk UF → heavy index `wel-ckf` (TCP/9997) | Custom | Per FS-XSYS-AD-01 (Splunk forwarding within 5 min). | FS-XSYS-AD-01, FS-PART11-03 | IQ-SIEM-01 |
| CI-40 | LabX LIMS Connector → poll endpoint | `https://lims.indus.local/api/v3/worklist` every 5 min (read-only) | Custom | Per FS-INT-LIMS-01. | FS-INT-LIMS-01 | OQ-INT-01 |
| CI-41 | LabX LIMS Connector → service principal | `indus\svc-labx-limsread` (read-only AD group) | Custom | Per FS-INT-LIMS-01. | FS-INT-LIMS-01 | IQ-INT-01 |
| CI-42 | LabX LIMS Connector → push gate | `result_state == APPROVED && SST.valid` | Custom | Per FS-INT-LIMS-02 / FS-INT-LIMS-03. | FS-INT-LIMS-02, FS-INT-LIMS-03 | OQ-INT-02 |
| CI-43 | Site PKI → mTLS cert for LIMS push | `indus-ckf-2026q2` (auto-rotate 1y) | Custom | Per FS-INT-LIMS-02 secure-channel requirement. | FS-INT-LIMS-02 | IQ-PKI-01 |
| CI-44 | Veeam B&R 12.1 → backup job | `IND-JOB-BAK-CKF` daily file-level + S3 Object Lock + LTO-9 | Custom | Per FS-BAK-01 / FS-XSYS-BAK-01. | FS-BAK-01, FS-XSYS-BAK-01 | IQ-BAK-01 |

## 6. Site-Specific Configuration

The site enables LabX's vendor-provided Part 11 module with the project-policy bundle and binds AD groups to LabX Authority Sets. The choices below are the *site*'s configuration choices; the underlying enforcement engines are vendor-owned.

| CI-ID | Configuration item (vendor-named) | Chosen value | Default? | Justification | FS-IDs traced | Verified by |
|---|---|---|---|---|---|---|
| CI-01 | LabX → Part 11 Module → `IND_CKF_PART11` project policy | `Audit trail required=ON; eSign required=ON; Raw data lock=ON` | Default (vendor template values applied as-is) | Per FS-SW-05 — vendor-recommended Part 11 baseline retained. | FS-SW-05, FS-AUD-01, FS-DI-04 | OQ-PROJECT-POLICY-01 |
| CI-02 | GPO `IND-LAB-USERS-WS` → screen-saver lock | 10 min idle (vendor + site default) | Default | Standard site GPO baseline. | FS-SW-01 | IQ-GPO-01 |
| CI-03 | GPO `IND-LAB-USB-BLOCK` → USB mass storage | Denied (override via CR) | Custom | Per FS-SEC-02. | FS-SEC-02 | IQ-GPO-02 |
| CI-04 | Site name | `Indus Therapeutics, Hyderabad, QC Chemical Lab` | Custom | Per FS H2 site identifier. | FS-PART11-01 (procedural) | IQ-SITE-01 |
| CI-05 | Site time-zone | `Asia/Kolkata (IST UTC+5:30)` | Custom | Local site time-zone. | FS-SW-04 | IQ-NTP-01 |
| CI-15 | LabX Authority Set ↔ AD-group `IND-CKF-Analysts` | `Analyst` (acquire / integrate; no Approve eSign) | Default (vendor template) | Per FS-PART11-02. | FS-PART11-02 | OQ-ROLE-01 |
| CI-16 | LabX Authority Set ↔ `IND-CKF-SeniorAnalysts` | `SeniorAnalyst` (Review eSign) | Default | Per FS-PART11-02 / FS-AUD-03. | FS-PART11-02, FS-AUD-03 | OQ-ROLE-02 |
| CI-17 | LabX Authority Set ↔ `IND-CKF-MethodOwners` | `MethodOwner` (method create/edit; no Approve eSign) | Default | Per FS-METH-02. | FS-METH-02 | OQ-ROLE-03 |
| CI-18 | LabX Authority Set ↔ `IND-CKF-QCManagers` | `QCManager` (Approve eSign; LIMS-export) | Default | Per FS-INT-LIMS-02. | FS-INT-LIMS-02 | OQ-ROLE-04 |
| CI-19 | LabX Authority Set ↔ `IND-CKF-ReagentCustodians` | `ReagentCustodian` (Reagent Register write; SST RS-acceptance eSign) | Default | Per URS § 4 SoD + FS-REA-01. | FS-REA-01 | OQ-ROLE-05 |
| CI-20 | LabX Authority Set ↔ `IND-CKF-SysAdmin` | `SysAdmin` (config; no Approve eSign) | Default | Per FS-PART11-02. | FS-PART11-02 | OQ-ROLE-06 |
| CI-21 | LabX Authority Set ↔ `IND-CKF-Auditor` | `Auditor` (read-only) | Default | Per FS-AUD-03. | FS-AUD-03 | OQ-ROLE-07 |
| CI-25 | LabX → Method Library entry `IND-METH-USP921-IC` | Vendor template MT-APN-USP921-2024 applied; site overrides: spec, drift threshold | Custom | Per FS-CMP-01. | FS-CMP-01 | OQ-CMP-01 |
| CI-26 | LabX → Drift threshold (per method) | `25 µg/min routine; 10 µg/min low-water` | Custom | Per FS-SST-01 (vendor SST engine consumes site threshold). | FS-SST-01 | OQ-SST-01 |
| CI-27 | LabX → Water-Standard Recovery limit (per method) | `± 3% nominal` per USP <921> | Custom | Per FS-CMP-03 / FS-SST-02. | FS-CMP-03, FS-SST-02 | OQ-SST-02 |
| CI-30 | LabX → Reagent Register entry | Anolyte / Catholyte / Hydranal Water Standards (1.0 / 10 / 100 / 1000) bound | Custom | Per FS-REA-01. | FS-REA-01 | OQ-REA-01 |
| CI-31 | LabX → Reagent expiry pre-flight block | Active (vendor feature; site enables) | Default | Per FS-REA-02. | FS-REA-02 | OQ-REA-02 |
| CI-32 | LabX → Cell-Fluid-Change workflow binding | `IND-WF-CELL-CHANGE` (vendor template; site binds AD group) | Custom (binding) | Per FS-REA-03. | FS-REA-03 | OQ-REA-03 |
| CI-33 | LabX → Water-Standard expiry pre-flight block | Active (vendor feature; site enables) | Default | Per FS-REA-04. | FS-REA-04 | OQ-REA-04 |
| CI-35 | LabX → SST workflow `IND-SST-DRIFT` | Vendor template SST applied: 5-min drift stabilisation + 100 µg water-std recovery | Default (vendor template) | Per FS-SST-01 / FS-SST-02 / FS-SST-05 (vendor SST engine + site thresholds CI-26, CI-27). | FS-SST-01, FS-SST-02, FS-SST-05 | OQ-SST-01..05 |
| CI-36 | LabX → Blank-determination cadence (per method) | Per method definition (typ. start of each session + every 20 samples) | Custom | Per FS-SST-03. | FS-SST-03 | OQ-SST-03 |
| CI-37 | LabX → Drift + Blank 30-day trend report | Vendor dashboard enabled; site sets early-warning band at ½ SOP threshold | Custom (band) | Per FS-SST-04. | FS-SST-04 | OQ-SST-04 |
| CI-50 | Cornerstone LMS → curriculum gate | `IND-CKF-101` (Analyst) + `IND-CKF-201` (SST + reagent lifecycle); annual | Custom | Per FS-TRN-01. | FS-TRN-01 | IQ-LMS-01 |
| CI-51 | Periodic Review template | `IND-PR-CKF` (QC Mgr + Head of QA) | Custom | Per FS-PR-01. | FS-PR-01 | OQ-PR-01 |
| CI-52 | DQ / IQ / OQ / PQ binding | `IND-DQ-CKF-001` / `IND-IQ-CKF-001` / `IND-OQ-CKF-001` / `IND-PQ-CKF-001` | Custom | Per FS-AIQ-01..04. | FS-AIQ-01, FS-AIQ-02, FS-AIQ-03, FS-AIQ-04 | (admin) |
| CI-53 | Validation dossier binding | `IND-VAL-CKF-001` | Custom | Per FS-PART11-01. | FS-PART11-01 | (admin) |
| CI-54 | AD Password Policy | GPO `IND-LAB-USERS-PWD` (12-char / 3-of-4 complexity / 90 d / lockout 5/15 min) | Custom | Per FS-PART11-07. | FS-PART11-07 | IQ-AD-02 |
| CI-55 | Break-glass account vault | `IND-BG-CKF` in CyberArk PAM (24h rotation, dual-witness) | Custom | Per FS-XSYS-AD-01. | FS-XSYS-AD-01 | IQ-PAM-01 |

## 7. References

### US — FDA / CFR
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300.
- 21 CFR Part 211 §§ .68, .160, .165, .194.

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11.
- Ph. Eur. 2.5.32 — Water: Micro Determination.

### International
- USP <921> Method Ic Coulometric Titration; USP <1058> AIQ; USP <1225>.
- ICH Q2(R2); PIC/S PI 041.
- ISPE GAMP 5 (2nd Ed., 2022).

### Vendor (authoritative design surface — see § 4 inventory for full version pins)
- Mettler Toledo — *LabX 2024 Installation, Configuration, and Administration Reference* (rev. 2024-09).
- Mettler Toledo — *LabX 2024 21 CFR Part 11 Compliance Guide* (rev. 2024-09).
- Mettler Toledo — *C30S Coulometric KF Hardware Reference + Maintenance Guide* (rev. 2024-06).
- Mettler Toledo — *LabX 2024 LIMS Connector Reference* (rev. 2024-09).
- Mettler Toledo — *USP <921> Method Ic Application Note* (rev. 2024-08).

### Site / parent
- `IND-FS-CKF-001 v1.2`; `IND-URS-CKF-001 v1.2`.
- `IND-VAL-CKF-001`; `IND-SOP-CC-CKF`; `IND-SOP-IR-CKF`; `IND-SOP-RESTORE-TEST`; `IND-VENAUDIT-MT-2025` (vendor audit).

## Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) | Design intent (brief) | Verified by |
|---|---|---|---|
| DS-HW-01 | FS-HW-01 | Workstation dedicated to LabX-KF (vendor-recommended baseline; site asset register) | IQ-HW-01 |
| DS-HW-02 | FS-HW-02 | Lenovo ThinkCentre M70t + APC SMT750 UPS (CI-10) | IQ-HW-02 |
| DS-HW-03 | FS-HW-03 | Bench-top humidity sensor → EMS alarm (site EMS, vendor-agnostic) | IQ-HW-03 |
| DS-SW-01 | FS-SW-01 | Win 11 Pro 23H2 AD-bound (CI-10, CI-12) | IQ-NW-01 |
| DS-SW-02 | FS-SW-02 | Mettler engineer install record (vendor procedure) | IQ-INSTALL-01 |
| DS-SW-03 | FS-SW-03 | Project storage SnapLock (CI-13) | IQ-FS-01 |
| DS-SW-04 | FS-SW-04 | NTP source + 1 s skew (CI-14) | IQ-NTP-01 |
| DS-SW-05 | FS-SW-05 | LabX Part 11 module + project policy (CI-01) | OQ-PROJECT-POLICY-01 |
| DS-CMP-01 | FS-CMP-01 | Method library entry IND-METH-USP921-IC (CI-25); engine vendor | OQ-CMP-01 |
| DS-CMP-02 | FS-CMP-02 | EP compendium flag (vendor method header) | OQ-CMP-02 |
| DS-CMP-03 | FS-CMP-03 | Water-Standard Recovery limit ± 3% (CI-27) | OQ-SST-02 |
| DS-CMP-04 | FS-CMP-04 | Method header `compendium` enum (vendor field) | OQ-CMP-02 |
| DS-AIQ-01 | FS-AIQ-01 | DQ binding (CI-52) | (admin) |
| DS-AIQ-02 | FS-AIQ-02 | IQ binding (CI-52) — vendor IQ template consumed | IQ-CKF-001 |
| DS-AIQ-03 | FS-AIQ-03 | OQ binding (CI-52) — vendor OQ battery consumed | OQ-CKF-001 |
| DS-AIQ-04 | FS-AIQ-04 | PQ binding (CI-52) | PQ-CKF-001 |
| DS-SST-01 | FS-SST-01 | Drift threshold (CI-26); vendor SST engine | OQ-SST-01 |
| DS-SST-02 | FS-SST-02 | Water-std recovery (CI-27); vendor SST engine | OQ-SST-02 |
| DS-SST-03 | FS-SST-03 | Blank cadence (CI-36); vendor blank-determination engine | OQ-SST-03 |
| DS-SST-04 | FS-SST-04 | 30-day trend early-warning band (CI-37) | OQ-SST-04 |
| DS-SST-05 | FS-SST-05 | SST log schema (vendor) | OQ-SST-05 |
| DS-REA-01 | FS-REA-01 | Reagent Register entries (CI-30); vendor register engine | OQ-REA-01 |
| DS-REA-02 | FS-REA-02 | Reagent expiry pre-flight (CI-31); vendor feature | OQ-REA-02 |
| DS-REA-03 | FS-REA-03 | Cell-fluid-change workflow (CI-32) | OQ-REA-03 |
| DS-REA-04 | FS-REA-04 | Water-standard expiry pre-flight (CI-33) | OQ-REA-04 |
| DS-REA-05 | FS-REA-05 | Cell-waste log (site SOP) | OQ-REA-05 |
| DS-PART11-02 | FS-PART11-02 | AD-bound access (CI-12, CI-15..21) | OQ-ROLE-01..07 |
| DS-PART11-07 | FS-PART11-07 | AD password policy (CI-54) | IQ-AD-02 |
| DS-INT-LIMS-01 | FS-INT-LIMS-01 | LIMS Connector poll + service principal (CI-40, CI-41) | OQ-INT-01 |
| DS-INT-LIMS-02 | FS-INT-LIMS-02 | Push gate + mTLS (CI-42, CI-43) | OQ-INT-02 |
| DS-INT-LIMS-03 | FS-INT-LIMS-03 | SST-valid pre-push (CI-42) | OQ-INT-02 |
| DS-BAK-01 | FS-BAK-01, FS-XSYS-BAK-01 | Veeam daily + S3 + LTO (CI-44) | IQ-BAK-01 |
| DS-BAK-02 | FS-BAK-02 | Quarterly restore drill (site SOP) | IQ-BAK-02 |
| DS-SEC-01 | FS-SEC-01 | LDAPS + CyberArk break-glass (CI-12, CI-55) | IQ-PAM-01 |
| DS-SEC-02 | FS-SEC-02 | GPO USB block (CI-03) | IQ-GPO-02 |
| DS-TRN-01 | FS-TRN-01 | LMS curriculum (CI-50) | IQ-LMS-01 |
| DS-PR-01 | FS-PR-01 | Periodic-review template (CI-51) | OQ-PR-01 |
| DS-XSYS-AD-01 | FS-XSYS-AD-01 | LDAPS + Conditional Access + CyberArk + Splunk (CI-12, CI-22, CI-55) | IQ-AD-01 |
| DS-XSYS-BAK-01 | FS-XSYS-BAK-01 | Veeam T3 + S3 Object Lock + LTO-9 (CI-44) | IQ-BAK-01 |
| DS-AUD-04 | FS-AUD-04 | SnapLock retention 7y/25y (CI-13) | IQ-FS-01 |

**FS-IDs flagged as vendor-internal — no site design surface** (covered by vendor design documentation per § 4): FS-AUD-01, FS-AUD-02, FS-AUD-03 (vendor renderer), FS-PART11-01, FS-PART11-03, FS-PART11-04, FS-PART11-05, FS-PART11-06, FS-METH-01, FS-METH-02 (engine), FS-RUN-01, FS-RUN-02, FS-RUN-03, FS-RUN-04, FS-PROC-01, FS-PROC-02, FS-PROC-03, FS-PROC-04, FS-DI-01, FS-DI-02, FS-DI-03, FS-DI-04, FS-DI-05, FS-PERF-01 (vendor benchmark).

## Appendix B — Design-level Risk Register

Design-stage risks specific to the site's binding of the C30S + LabX 2024 to the site infrastructure. Vendor-internal risks live in Mettler Toledo's risk documentation and are not duplicated here.

| ID | Risk | Likelihood | Impact | Mitigation reference | Design surface |
|---|---|---|---|---|---|
| DR-01 | Vendor SCN reverts site-customised CI (drift threshold CI-26 or recovery limit CI-27) to vendor default | Low | High | Post-SCN delta-check across all 30+ CIs; OQ-SST-01..02 re-test after SCN | CI-26, CI-27, vendor SCN gate |
| DR-02 | mTLS cert `indus-ckf-2026q2` (CI-43) expiry blocks LIMS push silently | Low | High | 30-d pre-expiry pager alert + auto-rotation | CI-43 |
| DR-03 | Authority Set ↔ AD-group rename drift (CI-15..21) | Low | Critical | Quarterly access review; Authority Set export reconciled with AD | CI-15..21 |
| DR-04 | Vendor design documentation inventory (§ 4) drift — vendor releases new revision without site DMS update | Low | High | Vendor audit `IND-VENAUDIT-MT-2025` annual + Mettler change-notification subscription | § 4 inventory |
| DR-05 | Local-time bench-top humidity sensor (CI-10 / FS-HW-03) drift not propagated to LabX run records | Low | Medium | EMS alarm rule reflects in run-record context; periodic check | CI-10 |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
