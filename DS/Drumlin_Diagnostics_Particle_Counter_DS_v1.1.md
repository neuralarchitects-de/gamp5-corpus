---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "DRD-FS-PCL-001 v1.2 (parent FS)"
  - "DRD-URS-PCL-001 v1.2 (parent URS — informational)"
  - "GAMP 5 (2nd ed.) Cat 3 — Vendor-Design-Reliance Statement conventions"
  - "21 CFR Part 11; EU GMP Annex 11; USP <788>; USP <789>; USP <1058>; ISO 21501-3:2019"
  - "Beckman Coulter HIAC 9703+ + PharmSpec 5 Operator + Administrator Manual"
parent_fs:
  document_number: DRD-FS-PCL-001
  version: 1.2
  file: ../../../FS_FDS/_generated/final/Drumlin_Diagnostics_Particle_Counter_FS_v1.3.md
parent_urs:
  document_number: DRD-URS-PCL-001
  version: 1.2
  file: ../../../URS/_generated/final/Particle_Counter_Liquid_Computer_System__Drumlin_Diagnostics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Design Specification (Vendor-Design-Reliance Statement)

## Liquid Particle Counter Computer System — Beckman Coulter HIAC 9703+ + PharmSpec 5

**Document Number:** DRD-DS-PCL-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** DRD-FS-PCL-001 v1.2 | **Parent URS:** DRD-URS-PCL-001 v1.2 *(informational)*
**Site:** Drumlin Diagnostics (fictional)
**System Class (GAMP 5, 2nd ed.):** Category 3 — Non-Configurable COTS *(PharmSpec 5 has vendor-level configurability but the design surface available to the site is minimal — vendor design documentation is incorporated by reference, not redrawn here per METHODOLOGY § 2B.6; see § 2)*
**Project Mode:** Configuration project on non-configurable instrument / appliance **Beckman Coulter HIAC 9703+ + PharmSpec 5** (GAMP 5 Category 3 — Non-Configurable COTS).
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; USP <788>; USP <789>; USP <1058>; Ph. Eur. 2.9.19; ISO 21501-3:2019; PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (Particulates SME) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Approver (System Owner — QC Manager Particulates) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-05-15 | (synthetic) | Initial DS issue (thin / vendor-design-reliance shape). Inherited Tier T1 from parent URS+FS pair (DRD-URS-PCL-001 / DRD-FS-PCL-001 v1.2). DS covers 75/75 FS-IDs via reliance on vendor design docs + site-specific bindings. No FS-IDs deferred. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

DS-specific terms only.

| Term | Definition |
|---|---|
| LO sensor | Light-Obscuration sensor — the optical primary measurement element on HIAC 9703+. |
| PharmSpec | Beckman Coulter regulated-mode application controlling HIAC 9703+. |
| Counted-bead | NIST-traceable counted bead suspension used to verify counting accuracy at SST. |
| Sizing-bead | NIST-traceable monodisperse PSL bead used to verify size accuracy at OQ. |

## 1. Purpose

This DS records the design posture for the HIAC 9703+ + PharmSpec 5 deployment at Drumlin Diagnostics. Because the system is a **non-configurable measurement instrument with a small configuration surface**, the site does not redraw vendor internals; instead this DS:

1. Inventories the **vendor design documents** Drumlin Diagnostics relies on as the authoritative design baseline.
2. Specifies the **site-specific integration design** (network, AD, file-share, LIMS, NTP, SIEM).
3. Specifies the **site-specific configuration choices** PharmSpec exposes (project policy, role-bindings, channel selections, SST cadence).

The vendor SDLC at Beckman Coulter owns optical-engine internals (LO-sensor primary signal path, syringe-pump motion control, PharmSpec rendering pipeline).

## 2. Scope

In scope: vendor-design-doc inventory + site-side integration design + site-specific PharmSpec configuration values + site-deployed components (none beyond minor admin scripts).

Out of scope (vendor-owned, NOT redrawn here): PharmSpec UI rendering, LO-sensor primary-signal acquisition path, syringe-pump motion control firmware, internal coincidence-loss algorithm, internal pulse-height-to-size mapping.

## 3. Architectural Overview

### 3.1 Logical View

```
                  ┌─────────────────────────────┐
                  │  AD (drumlin.local) · NTP   │
                  └───────────────┬─────────────┘
                                  │
                                  ▼
┌──────────────────────────────────────────────────────────────┐
│  PharmSpec 5 Workstation `drd-pcl-ws-01`                     │
│  Win 11 Pro 23H2 · PharmSpec 5.2.1                           │
│  Project Policy = DRD_PCL_PART11                              │
│  Project Storage: \\drd-gmp-fs01\hiac-projects                │
└────────────────────┬──────────────────────┬──────────────────┘
                     │                      │
                     ▼                      ▼
┌──────────────────────────────┐  ┌────────────────────────────┐
│ Beckman Coulter HIAC 9703+   │  │ LabWare LIMS 8             │
│ LO sensor + syringe pump +   │  │ PharmSpec LIMS Connector 4 │
│ auto-sampler                 │  │ HTTPS REST (mTLS)          │
└──────────────────────────────┘  └────────────────────────────┘
```

### 3.2 Deployment Topology

| Component | Host / Path | Version pin | Hardening |
|---|---|---|---|
| PharmSpec 5 application | `drd-pcl-ws-01` | 5.2.1 | Win 11 Pro 23H2 + GPO `DRD-LAB-WS-23H2` |
| HIAC 9703+ firmware | Bench instrument | FW 1.06.0 | GxP mode ON; tamper-evident USB seal |
| Project store | `\\drd-gmp-fs01\hiac-projects` | NTFS ACL | AD-group bound |
| Audit trail DB | PharmSpec embedded MSSQL Express | per build | append-only |
| Qualification archive | `\\drd-gmp-fs01\pcl-qual` | WORM | 25 y retention |

## 4. Vendor Design Documentation Inventory

The site relies on the following Beckman Coulter design documents as authoritative for vendor-internal design. These are the vendor-controlled artefacts the site does NOT redraw.

| Vendor doc title | Version | Vendor doc-num | Site controlled-doc reference (DMS) | Retention class |
|---|---|---|---|---|
| HIAC 9703+ *System Description and Hardware Design Reference* | 1.06.A | BC-HIAC-SDD-001 | DMS link `DRD-VND-HIAC-SDD-001` | 25 y |
| HIAC 9703+ *Light-Obscuration Sensor Functional Design* | 1.06.A | BC-HIAC-LO-001 | DMS link `DRD-VND-HIAC-LO-001` | 25 y |
| HIAC 9703+ *Syringe-Pump Motion Control Specification* | 1.06.A | BC-HIAC-SP-001 | DMS link `DRD-VND-HIAC-SP-001` | 25 y |
| PharmSpec 5 *Software Architecture Description* | 5.2.A | BC-PS-SAD-001 | DMS link `DRD-VND-PS-SAD-001` | 25 y |
| PharmSpec 5 *21 CFR Part 11 Compliance Statement* | 5.2.B | BC-PS-PART11-001 | DMS link `DRD-VND-PS-PART11-001` | 25 y |
| PharmSpec 5 *System Administrator Guide* | 5.2.E | BC-PS-SAG-001 | DMS link `DRD-VND-PS-SAG-001` | 25 y |
| PharmSpec 5 *LIMS Connector 4 Integration Reference* | 4.1.B | BC-PS-LIMS-001 | DMS link `DRD-VND-PS-LIMS-001` | 25 y |
| HIAC 9703+ *USP <788> Method 1 Implementation Notes* | rev 3 | BC-HIAC-USP788-001 | DMS link `DRD-VND-HIAC-USP788-001` | 25 y |
| HIAC 9703+ *ISO 21501-3 Counting-Efficiency Specification* | rev 2 | BC-HIAC-ISO21501-001 | DMS link `DRD-VND-HIAC-ISO21501-001` | 25 y |

All vendor-doc revisions tracked via change-control workflow `CCR-PCL-VENDOR-*`; site re-acknowledges latest vendor revision at every annual periodic review (DS-PR-01).

## 5. Site-Specific Integration Design

`D = vendor default`; `C = site custom`.

| CI-ID | Configuration Item | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-HW-01 | Workstation reservation | `drd-pcl-ws-01` reserved for PharmSpec only | C | FS-HW-01 | IQ-HW-01 |
| DS-HW-02 | Workstation hardware spec | Dell OptiPlex 7080 — meets PharmSpec 5 vendor min spec | D | FS-HW-02 | IQ-HW-02 |
| DS-HW-03 | UPS sizing | APC SMT1500 — ≥ 30 min runtime; PowerChute graceful at 20% | D | FS-HW-03 | IQ-UPS-01 |
| DS-HW-04 | Site environment classification | ISO Class 8 (or better) bench area; background particulate monitored via facility EMS | C | FS-HW-05 | IQ-ENV-01 |
| DS-INT-AD-01 | AD bind | LDAPS to `ldap.drumlin.local:636`; service account `svc-pcl-ldap` (rotation 180 d via CyberArk); break-glass `DRD-BG-PCL` CyberArk-vaulted | C | FS-SEC-01, FS-XSYS-AD-01 | IQ-AD-01 |
| DS-INT-NTP-01 | NTP peer | `ntp.drumlin.local`; w32time MaxPosPhaseCorrection 1000 ms | C | FS-SW-04 | OQ-NTP-01 |
| DS-INT-NET-01 | Network attachment | `vlan-lab-pcl`; firewall outbound allowlist: AD/LDAPS:636, NTP:123, LIMS:443, SIEM:514, share:445 to `drd-gmp-fs01` only | C | FS-SW-01 + FS-SW-03 | IQ-FW-01 |
| DS-INT-FS-01 | Project file-share | `\\drd-gmp-fs01\hiac-projects` NTFS: `DRD-PCL-ANALYST` R; `DRD-PCL-OWNER` RWX; local C: write blocked | C | FS-SW-03 | IQ-ACL-01 |
| DS-INT-SIEM-01 | SIEM forwarder | winlogbeat → Splunk index `gxp-authn` + `gxp-endpoint`; ≤ 5 min ingestion; RFC 5424 over TLS | C | FS-XSYS-AD-01 | OQ-SIEM-01 |
| DS-INT-LIMS-01 | LIMS connector endpoint + protocol | `https://lims.drumlin.local/api/v2/{worklist,results}`; HTTPS + mTLS (cert `DRD-PKI-PCL-WS01`); 5-min poll | C | FS-INT-LIMS-01..04 | OQ-LIMS-01 |
| DS-INT-LIMS-02 | LIMS payload schema | `report_id, instrument_id, method_id+version, reviewer_id, approver_id, sst_status` | C | FS-INT-LIMS-03 | OQ-LIMS-02 |
| DS-INT-LIMS-03 | LIMS pre-push validation | `result_state == APPROVED AND SST_state ∈ {PASS, VALID}`; reject → `DRD-PCL-NOT-APPROVED` | C | FS-INT-LIMS-02, FS-INT-LIMS-04 | OQ-LIMS-03 |
| DS-INT-BAK-01 | Backup integration | Veeam B&R 12.1 file-level capture of result store + config + audit DB; nightly `DRD-JOB-BAK-PCL`; Tier T3 (RPO ≤ 72 h; RTO ≤ 72 BH); S3 Object Lock Compliance + LTO-9 monthly | C | FS-BAK-01..03, FS-XSYS-BAK-01 | OQ-BAK-01 |

## 6. Site-Specific Configuration

| CI-ID | Configuration Item (vendor-named) | Chosen value | D/C | Justification | FS-IDs | Verified by |
|---|---|---|---|---|---|---|
| DS-SW-01 | OS + domain bind | Win 11 Pro 23H2 joined to `drumlin.local`; GPO `DRD-LAB-WS-23H2` | C | FS-SW-01 | IQ-SW-01 |
| DS-SW-02 | PharmSpec install record | installed by Beckman Coulter engineer; record `DRD-IR-PCL-001` retained | C | FS-SW-02 | IQ-SW-02 |
| DS-SW-05 | PharmSpec Project Policy | `DRD_PCL_PART11` (audit_trail=mandatory; esign=mandatory; raw_data_lock=immediate) | C | FS-SW-05 | IQ-SW-03 |
| DS-SW-06 | PharmSpec SCN change-control hook | `CCR-PCL-*` mandatory; build hash verified at partial-OQ | C | FS-SW-06 | OQ-CC-01 |
| DS-CMP-01 | USP <788> Method 1 acceptance evaluator | LVP per-mL limits (25 / 3); SVP cumulative per-container limits (6000 / 600); per-method selector | C | FS-CMP-01 | OQ-USP788-01 |
| DS-CMP-02 | USP <789> acceptance evaluator | `50 / 5 / 2 per mL at ≥10 / ≥25 / ≥50 µm` | C | FS-CMP-02 | OQ-USP789-01 |
| DS-CMP-03 | Ph. Eur. 2.9.19 activation | `Compendium=EP` → Test 1A / 1B logic applied | C | FS-CMP-03 | OQ-EP-01 |
| DS-CMP-04 | ISO 21501-3 OQ acceptance | size acc ±10% at calibrated channels; counting efficiency 50% ±20% at threshold + 100% ±10% above 1.5× threshold; coincidence loss ≤ 10% at operational concentration | C | FS-CMP-04 | OQ-ISO-01 |
| DS-CMP-05 | Compendium enum | `{USP, EP, JP, NON-COMP}` | C | FS-CMP-05 | OQ-CMP-01 |
| DS-AIQ-01 | DQ document | `DRD-DQ-PCL-001` — intended-use, channels, working range | C | FS-AIQ-01 | DQ-REF-01 |
| DS-AIQ-02 | IQ protocol | `DRD-IQ-PCL-001` — install, AD bind, PharmSpec build, sensor + pump install | C | FS-AIQ-02 | IQ-AIQ-01 |
| DS-AIQ-03 | OQ battery | size acc (10 + 25 µm NIST sizing beads); counting acc (counted-bead); sample-volume gravimetric ±1%; sensor blank; resolution; coincidence-loss verification | C | FS-AIQ-03 | OQ-AIQ-01 |
| DS-AIQ-04 | PQ schedule | go-live + sensor/pump replacement + annual | C | FS-AIQ-04 | OQ-PQ-01 |
| DS-AIQ-05 | Partial-PQ rule | SST only after PM not affecting sensor | C | FS-AIQ-05 | OQ-PQP-01 |
| DS-AIQ-06 | Qualification archive | `\\drd-gmp-fs01\pcl-qual` WORM 25 y | C | FS-AIQ-06 | IQ-WORM-01 |
| DS-SST-01 | SST workflow | `DRD-SST-USP788`: counted-bead recovery ±10% nominal; sensor blank ≤ method limit; gravimetric sample-volume ±1%; verdict block-on-fail | C | FS-SST-01 | OQ-SST-01 |
| DS-SST-02 | SST record schema | `op_id, ts, counted_bead_lot, cert_expiry, blank_volume_passed, recovery_pct, verdict`; immutable | C | FS-SST-02 | OQ-SST-02 |
| DS-SST-03 | SST FAIL FSM | NOT_READY; runner block; override via `DRD-PCL-QA-APPROVER` co-sign + RFC | C | FS-SST-03 | OQ-SST-03 |
| DS-SST-04 | SST trending | 12-month rolling; early-warning band ±7% recovery; Site dashboard alert | C | FS-SST-04 | OQ-SST-04 |
| DS-SST-05 | Audit-trail monthly review template | includes "SST trend review" sign-off | C | FS-SST-05 | OQ-AUD-01 |
| DS-REF-01 | Reference Standard Register schema | `rs_id, type {counted/sizing}, source, lot, COA_id, NIST_flag, receipt_date, opening_date, expiry, custodian` | C | FS-REF-01 | OQ-REF-01 |
| DS-REF-02 | Pre-flight ref-expiry block | reject when `rs.expiry < today` | C | FS-REF-02 | OQ-REF-02 |
| DS-REF-03 | SST ref-binding | `rs_id` mandatory at SST | C | FS-REF-03 | OQ-REF-03 |
| DS-REF-04 | Disposal log gating | DISPOSED requires `operator + disposal_route` | C | FS-REF-04 | OQ-REF-04 |
| DS-SAMP-01 | Diluent / particle-free-water register | `lot, receipt_date, certificate-clean state, opening_date, expiry`; per-batch verify at session start | C | FS-SAMP-01 | OQ-SAMP-01 |
| DS-SAMP-02 | Sampling-mode enum + EMS gate | `{open_cup, closed}`; ISO Class 8 minimum environment enforced via facility EMS | C | FS-SAMP-02 | OQ-SAMP-02 |
| DS-SAMP-03 | Degassing + bubble-detection | `degassing_applied=true/false`; bubble-detection flags suspect counts in ≥ 25 µm channel | C | FS-SAMP-03 | OQ-SAMP-03 |
| DS-SAMP-04 | Method `transfer_protocol` field | probe immersion depth (mm) + swirl pattern; training-required tag | C | FS-SAMP-04 | OQ-SAMP-04 |
| DS-ACQ-01 | Method-lifecycle states | `DRAFT → REVIEW → APPROVED → EFFECTIVE → OBSOLETE` | C | FS-ACQ-01 | OQ-MTH-01 |
| DS-ACQ-02 | Pre-flight checker rules | instrument_state + SST_state + method_state + project_lock + ref_std_expiry + diluent_expiry | C | FS-ACQ-02 | OQ-PRE-01 |
| DS-ACQ-03 | Acquisition metadata schema | `sample_id, dilution_factor, vessel_id, replicate_count, method_id+version, instrument_id, analyst_id, ts` | C | FS-ACQ-03 | OQ-ACQ-03 |
| DS-PROC-01 | USP <788> replicate processing | replicate averaging + outlier handling; method-bound first-replicate discard rule | C | FS-PROC-01 | OQ-PROC-01 |
| DS-PROC-02 | RFC on manual reprocessing | mandatory dialog | C | FS-PROC-02 | OQ-PROC-02 |
| DS-PROC-03 | Raw data preservation | `.psr` preserved; `.proc` references parent `raw_id` | C | FS-PROC-03 | OQ-PROC-03 |
| DS-PROC-04 | Limit-band evaluator | 30% / 50% / 100% TREND / OOT / OOS flags | C | FS-PROC-04 | OQ-PROC-04 |
| DS-PROC-05 | PDF report content | raw counts per replicate + channel; dilution-corrected; SST status; limit status; ALCOA+; SHA-256 | C | FS-PROC-05 | OQ-RPT-01 |
| DS-PROC-06 | OOS → LIMS routing | `LIMS-WF-211192`; sample-state HOLD | C | FS-PROC-06 | OQ-PROC-05 |
| DS-AUD-01 | Audit event-coverage | methods, sequences, results, configuration, ref-std register, sign-on/off, SST events = ALL | C | FS-AUD-01 | OQ-AUD-02 |
| DS-AUD-02 | DB append-only | trigger `audit_no_update_delete`; delete-grants revoked | C | FS-AUD-02 | OQ-AUD-03 |
| DS-AUD-03 | Audit-review templates | per-batch (Senior Analyst); monthly (QC Manager) | C | FS-AUD-03 | OQ-AUD-04 |
| DS-AUD-04 | Archival retention | 25 y product-release-linked; 7 y default; job `DRD-JOB-ARCH-PCL` | C | FS-AUD-04 | OQ-ARCH-01 |
| DS-PART11-01 | § 11.10(a) SOPs | `DRD-SOP-CC-PCL` + `DRD-SOP-IR-PCL` | C | FS-PART11-01 | OQ-P11-01 |
| DS-PART11-02 | § 11.10(d) access review | quarterly | C | FS-PART11-02 | OQ-P11-02 |
| DS-PART11-03 | § 11.50 e-sign manifestation | `username + datetime(NTP) + meaning` | C | FS-PART11-03 | OQ-P11-03 |
| DS-PART11-04 | § 11.70 record↔signature | SHA-256 hash | C | FS-PART11-04 | OQ-P11-04 |
| DS-PART11-05 | § 11.100 uniqueness | AD UPN | C | FS-PART11-05 | OQ-P11-05 |
| DS-PART11-06 | § 11.200 re-auth on Approve | password re-entry | C | FS-PART11-06 | OQ-P11-06 |
| DS-PART11-07 | § 11.300 password policy | AD GPO `DRD-LAB-USERS-PWD` (12 char, complexity, 90 d, lockout=5) | C | FS-PART11-07 | OQ-P11-07 |
| DS-DI-01 | ALCOA+ Attributable | `op_id` per event | C | FS-DI-01 | OQ-DI-01 |
| DS-DI-02 | ALCOA+ Legible | PDF/A-2b export | C | FS-DI-02 | OQ-DI-02 |
| DS-DI-03 | ALCOA+ Contemporaneous | NTP-only ts | C | FS-DI-03 | OQ-DI-03 |
| DS-DI-04 | ALCOA+ Original | `.psr` raw preserved | C | FS-DI-04 | OQ-DI-04 |
| DS-DI-05 | ALCOA+ Accurate | SST gate + counted-bead verification at OQ | C | FS-DI-05 | OQ-DI-05 |
| DS-DI-06 | ALCOA+ Complete | manifest verifies raw + audit + signature + method-version | C | FS-DI-06 | OQ-DI-06 |
| DS-SEC-02 | Removable-media GPO | `DRD-LAB-USB-BLOCK`; engineering override via change-control | C | FS-SEC-02 | IQ-USB-01 |
| DS-TRN-01 | LMS course bindings | `DRD-PCL-101` analyst; `DRD-PCL-201` SST + ref-std lifecycle; annual re-completion | C | FS-TRN-01 | OQ-TRN-01 |
| DS-PR-01 | Periodic-review template | `DRD-PR-PCL`: method inventory, audit-trail evidence, SST trend, counted-bead register health, deviations, training; QC Manager + Head of QA sign-off | C | FS-PR-01 | OQ-PR-01 |
| DS-PERF-01 | PQ scenario performance | typical batch session completes without crash or data loss | C | FS-PERF-01 | PQ-PERF-01 |

## 7. References

### US
- 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300
- 21 CFR Part 211 §§ .68, .192, .194

### EU
- EU GMP Annex 11 §§ 4, 6, 9, 11

### International
- USP <788>; USP <789>; USP <1058>; Ph. Eur. 2.9.19; ISO 21501-3:2019; PIC/S PI 041; ISPE GAMP 5 (2nd ed., 2022)

### DACH
- BfArM bekanntmachungen (informational)

### Vendor
- Beckman Coulter — *HIAC 9703+ System Description and Hardware Design Reference*, BC-HIAC-SDD-001 v1.06.A (synthetic placeholder)
- Beckman Coulter — *PharmSpec 5 System Administrator Guide*, BC-PS-SAG-001 v5.2.E (synthetic placeholder)
- Beckman Coulter — *PharmSpec 5 21 CFR Part 11 Compliance Statement*, BC-PS-PART11-001 v5.2.B (synthetic placeholder)
- *Alternative vendor*: Particle Measuring Systems (HIAC-equivalent path noted for vendor-substitution risk register entry DR-03)

## 8. Appendix A — DS → FS Traceability Matrix

| DS-ID | FS-ID(s) |
|---|---|
| DS-HW-01 | FS-HW-01 |
| DS-HW-02 | FS-HW-02 |
| DS-HW-03 | FS-HW-03 |
| DS-HW-04 | FS-HW-05 |
| DS-INT-AD-01 | FS-SEC-01, FS-XSYS-AD-01 |
| DS-INT-NTP-01 | FS-SW-04 |
| DS-INT-NET-01 | FS-SW-01, FS-SW-03 |
| DS-INT-FS-01 | FS-SW-03 |
| DS-INT-SIEM-01 | FS-XSYS-AD-01 |
| DS-INT-LIMS-01 | FS-INT-LIMS-01, FS-INT-LIMS-04 |
| DS-INT-LIMS-02 | FS-INT-LIMS-03 |
| DS-INT-LIMS-03 | FS-INT-LIMS-02, FS-INT-LIMS-04 |
| DS-INT-BAK-01 | FS-BAK-01, FS-BAK-02, FS-BAK-03, FS-XSYS-BAK-01 |
| DS-SW-01 | FS-SW-01 |
| DS-SW-02 | FS-SW-02 |
| DS-SW-05 | FS-SW-05 |
| DS-SW-06 | FS-SW-06 |
| DS-CMP-01 | FS-CMP-01 |
| DS-CMP-02 | FS-CMP-02 |
| DS-CMP-03 | FS-CMP-03 |
| DS-CMP-04 | FS-CMP-04 |
| DS-CMP-05 | FS-CMP-05 |
| DS-AIQ-01 | FS-AIQ-01 |
| DS-AIQ-02 | FS-AIQ-02 |
| DS-AIQ-03 | FS-AIQ-03 |
| DS-AIQ-04 | FS-AIQ-04 |
| DS-AIQ-05 | FS-AIQ-05 |
| DS-AIQ-06 | FS-AIQ-06 |
| DS-SST-01 | FS-SST-01 |
| DS-SST-02 | FS-SST-02 |
| DS-SST-03 | FS-SST-03 |
| DS-SST-04 | FS-SST-04 |
| DS-SST-05 | FS-SST-05 |
| DS-REF-01 | FS-REF-01 |
| DS-REF-02 | FS-REF-02 |
| DS-REF-03 | FS-REF-03 |
| DS-REF-04 | FS-REF-04 |
| DS-SAMP-01 | FS-SAMP-01 |
| DS-SAMP-02 | FS-SAMP-02 |
| DS-SAMP-03 | FS-SAMP-03 |
| DS-SAMP-04 | FS-SAMP-04 |
| DS-ACQ-01 | FS-ACQ-01 |
| DS-ACQ-02 | FS-ACQ-02 |
| DS-ACQ-03 | FS-ACQ-03 |
| DS-PROC-01 | FS-PROC-01 |
| DS-PROC-02 | FS-PROC-02 |
| DS-PROC-03 | FS-PROC-03 |
| DS-PROC-04 | FS-PROC-04 |
| DS-PROC-05 | FS-PROC-05 |
| DS-PROC-06 | FS-PROC-06 |
| DS-AUD-01 | FS-AUD-01 |
| DS-AUD-02 | FS-AUD-02 |
| DS-AUD-03 | FS-AUD-03 |
| DS-AUD-04 | FS-AUD-04 |
| DS-PART11-01 | FS-PART11-01 |
| DS-PART11-02 | FS-PART11-02 |
| DS-PART11-03 | FS-PART11-03 |
| DS-PART11-04 | FS-PART11-04 |
| DS-PART11-05 | FS-PART11-05 |
| DS-PART11-06 | FS-PART11-06 |
| DS-PART11-07 | FS-PART11-07 |
| DS-DI-01 | FS-DI-01 |
| DS-DI-02 | FS-DI-02 |
| DS-DI-03 | FS-DI-03 |
| DS-DI-04 | FS-DI-04 |
| DS-DI-05 | FS-DI-05 |
| DS-DI-06 | FS-DI-06 |
| DS-SEC-02 | FS-SEC-02 |
| DS-TRN-01 | FS-TRN-01 |
| DS-PR-01 | FS-PR-01 |
| DS-PERF-01 | FS-PERF-01 |

## 9. Appendix B — Design-level Risk Register

| ID | Design risk | Likelihood | Impact | Mitigation in this DS |
|---|---|---|---|---|
| DR-01 | Vendor revision of HIAC LO-sensor design (new SCN) silently changes coincidence-loss behaviour | Low | High | Vendor-doc inventory re-acknowledgement at annual PR (DS-PR-01) + DS-SW-06 CCR-PCL-* + OQ-ISO-01 re-execute |
| DR-02 | Counted-bead lot expiry slip causes biased SST results | Medium | High | DS-REF-02 pre-flight + DS-SST-04 12-month trend monitoring |
| DR-03 | Vendor substitution risk: HIAC supply discontinued; PMS equivalent has different acceptance behaviour | Low | High | Site keeps PMS-equivalent ISO 21501-3 OQ protocol on shelf as alternate; change-control workflow `CCR-PCL-VENDOR-SUB` defined |
| DR-04 | Open-cup mode used in ISO Class 9 (or worse) area inflating background counts | Medium | High | DS-SAMP-02 enforces ISO Class 8 minimum via facility EMS gate before run start |
| DR-05 | mTLS cert on LIMS connector expires silently | Medium | High | DS-INT-LIMS-01 90-d rotation + 30-d operator alert |
| DR-06 | Audit-trail MSSQL Express corruption | Low | High | DS-AUD-02 append-only + DS-INT-BAK-01 nightly + monthly logical export |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
