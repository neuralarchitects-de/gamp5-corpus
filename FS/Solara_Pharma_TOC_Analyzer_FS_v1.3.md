---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; v1.2 enrichment 2026-05-12"
seed_corpus_basis:
  - "SOL-URS-TOC-001 (parent URS) v1.2"
  - "GAMP 5 (2nd ed.) Cat 4 conventions"
  - "21 CFR Part 11; EU GMP Annex 11"
  - "USP <643>; USP <645>; USP <1058>; Ph. Eur. 2.2.44"
parent_urs:
  document_number: SOL-URS-TOC-001
  version: 1.2
  file: ../../URS/_generated/TOC_Analyzer_Computer_System__Solara_Pharma_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## TOC Analyzer Computer System — Sievers M9 + DataPro2 v2.4

**Document Number:** SOL-FS-TOC-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** SOL-URS-TOC-001 v1.2 | **Site:** Solara Pharma (fictional)
**System Class:** GAMP Cat 4 — Configured Product
**Regulatory Scope:** 21 CFR Part 11; EU GMP Annex 11; USP <643>; USP <645>; USP <1058>; Ph. Eur. 2.2.44; ICH Q2(R2); PIC/S PI 041

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (QC Manager — Utilities) | _____________ | _____________ | _____ |
| Reviewer (System Administrator) | _____________ | _____________ | _____ |
| Approver (Head of Manufacturing Sciences) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.2 | 2026-05-12 | (synthetic) | Expanded to match SOL-URS-TOC-001 v1.2 (T2 — 60-req). Per-URS-ID rows for USP <643> compendial, AIQ per USP <1058>, SST (sucrose/BQ + RE), reagent + standard register, UV lamp + reactor lifecycle, on-line / grab-sample mode, per-clause Part 11 + DI. Doc-number prefix aligned with URS (SOL-). |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies the deployment, configuration, and integration of Sievers M9 + DataPro2 v2.4 to satisfy `SOL-URS-TOC-001` v1.2. Controlling input to `SOL-CS-TOC-001`, `SOL-RA-TOC-001`, IQ/OQ/PQ protocols, and `SOL-RTM-TOC-001`.

## 2. Scope

Sievers M9 lab TOC analyzer + DataPro2 v2.4 on a dedicated workstation (Win 11 Pro 23H2); AD authentication; integration with LabWare LIMS 8 via DataShare 5; daily backup; NTP sync; USP <643> SST with sucrose / 1,4-benzoquinone; reagent + USP RS register; UV lamp + reactor lifecycle. Out: sample preparation; water-system loop sanitization; LIMS sample lifecycle.

## 3. System Architecture

```
   AD/NTP ──► DataPro2 v2.4 Workstation ──► Sievers M9 (UV-persulfate reactor + membrane CO₂ detector)
                  │                          │
                  ├─► USP RS Register (sucrose + 1,4-BQ)
                  ├─► UV Lamp + Reactor + ICR Lifecycle Tracking
                  └─► LabWare LIMS 8 (DataShare 5, SST-gated push)
```

### 3.1 Component Inventory

| ID | Component | Type | GAMP Cat | Source | Notes |
|---|---|---|---|---|---|
| C-01 | DataPro2 v2.4 | App SW | 4 | Sievers / Veolia | Part 11 module enabled |
| C-02 | Sievers M9 (lab) | Instrument FW | 4 | Sievers / Veolia | UV-persulfate or UV-only oxidation |
| C-03 | Windows 11 Pro 23H2 | OS | 1 | Microsoft | Domain-joined |
| C-04 | DataShare 5 connector | Interface | 4 | Sievers + LabWare | Worklist + result push |
| C-05 | USP RS register | Config | 4 | Site | sucrose + 1,4-benzoquinone + low-TOC water blank |
| C-06 | UV-lamp / reactor / ICR lifecycle store | Config | 4 | Site + Sievers | hour-tracked |

## 4. Functional Specifications

| FS ID | URS ID | Specification |
|---|---|---|
| FS-HW-01 | URS-HW-01 | Workstation `sol-toc-ws-01` reserved exclusively for DataPro2; no other GxP app. |
| FS-HW-02 | URS-HW-02 | HP EliteDesk 800 G9 with 32 GB RAM, 1 TB SSD, 4× USB-3 ports dedicated to M9 communication. |
| FS-HW-03 | URS-HW-03 | APC SMT1500 UPS sized ≥ 30 min at observed load; PowerChute graceful-shutdown at 20%. |
| FS-HW-04 | URS-HW-04 | Workstation on GMP-VLAN `vlan-gmp-utilities`; firewall rules block office-segment + internet egress. |
| FS-HW-05 | URS-HW-05 | DataPro2 streams lamp_intensity, lamp_hours, reactor_temp readings; thresholds configured per SOP; deviation fires alarm. |
| FS-HW-06 | URS-HW-06 | Autosampler qualified per Sievers SOP at install + post-service; vial-position reproducibility check. |
| FS-SW-01 | URS-SW-01 | Windows 11 Pro 23H2, joined to `solara.local`; AD baseline GPO `SOL-UTIL-LAB-WS`. |
| FS-SW-02 | URS-SW-02 | DataPro2 v2.4 installed by Sievers engineer; install record retained. |
| FS-SW-03 | URS-SW-03 | TOC projects on `\\sol-gmp-fs01\toc-projects`; local C: write blocked via NTFS ACL. |
| FS-SW-04 | URS-SW-04 | Windows Event Forwarder pushes audit logs to site Splunk. |
| FS-SW-05 | URS-SW-05 | Windows Time Service synced to `ntp.solara.local`; skew alert > 1000 ms. |
| FS-SW-06 | URS-SW-06 | GPO `SOL-LAB-LOCK` sets screen lock at 10 min idle; AD re-auth required to unlock. |
| FS-SW-07 | URS-SW-07 | DataPro2 project policy `SOL_TOC_PART11` applied: audit trail required, eSign required, raw data lock. |
| FS-SW-08 | URS-SW-08 | DataPro2 SCN applied under change control `CCR-TOC-*`; build hash verified at partial-OQ re-test. |
| FS-CMP-01 | URS-CMP-01 | TOC calculation engine binds 500 ppb limit by default for WFI / PW methods; per-method override permitted only on approved methods. |
| FS-CMP-02 | URS-CMP-02 | SST template enforces USP <643> response-efficiency criterion 85% ≤ RE ≤ 115% computed as (response_sucrose − blank) / (response_BQ − blank); fail blocks GxP. |
| FS-CMP-03 | URS-CMP-03 | EP-monograph methods carry `Compendium=EP`; Ph. Eur. 2.2.44 control tests mandatory for those methods. |
| FS-CMP-04 | URS-CMP-04 | OQ LOD test: replicate measurements at 50 ppb sucrose; verify 3×SD of blank ≤ 50 ppb. |
| FS-CMP-05 | URS-CMP-05 | Method header `compendium` enum (USP / EP / JP / NON-COMP). |
| FS-AIQ-01 | URS-AIQ-01 | DQ `SOL-DQ-TOC-001` captures working range (1 ppb – 50 ppm), on-line + grab modes, water-grade compatibility. |
| FS-AIQ-02 | URS-AIQ-02 | IQ `SOL-IQ-TOC-001` verifies install, AD bind, DataPro2 build hash, UV lamp installation, reactor + ICR installation. |
| FS-AIQ-03 | URS-AIQ-03 | OQ `SOL-OQ-TOC-001` battery: USP <643> RE test; LOD; linearity 5-point 50–5000 ppb; accuracy on 500 ppb sucrose challenge; precision RSD ≤ 5%; carry-over (low-TOC sample after 5000 ppb spike). |
| FS-AIQ-04 | URS-AIQ-04 | PQ `SOL-PQ-TOC-001` scheduled at go-live, on UV lamp replacement, on reactor service, on software upgrade, annually. |
| FS-AIQ-05 | URS-AIQ-05 | Partial PQ (SST only) permitted after routine PM not affecting UV reactor. |
| FS-AIQ-06 | URS-AIQ-06 | Qualification evidence on `\\sol-gmp-fs01\toc-qual` with WORM bit; retention 25 y. |
| FS-SST-01 | URS-SST-01 | SST workflow `SOL-SST-USP643`: triplicate water blank → triplicate 500 ppb sucrose → triplicate 500 ppb BQ; RE computed automatically; verdict 85% ≤ RE ≤ 115%. |
| FS-SST-02 | URS-SST-02 | SST scheduler: daily for grab mode, weekly for on-line mode; per-method override permitted on EFFECTIVE methods. |
| FS-SST-03 | URS-SST-03 | SST record schema: op_id, ts, USP_RS_lot, cert_expiry, blank_value, sucrose_value, BQ_value, RE, verdict; immutable. |
| FS-SST-04 | URS-SST-04 | SST failure → instrument FSM → NOT_READY; sequence runner blocks; override requires `SOL-TOC-QA-APPROVER` co-sign + RFC. |
| FS-SST-05 | URS-SST-05 | Rolling 12-month RE trend; early-warning band at RE ≤ 90% or ≥ 110%; alert via Site EMS dashboard. |
| FS-REA-01 | URS-REA-01 | USP RS Register schema: rs_id, type (sucrose / BQ), source, lot, COA_id, receipt_date, opening_date, expiry, custodian. |
| FS-REA-02 | URS-REA-02 | SST pre-flight rejects when bound USP_RS_lot is expired; rejection logged. |
| FS-REA-03 | URS-REA-03 | Working-standard register: prep_date, prep_analyst, source_RS_lot, expiry (same-day for sucrose). |
| FS-REA-04 | URS-REA-04 | Low-TOC water blank register: lot, COA showing < 50 ppb TOC at receipt. |
| FS-REA-05 | URS-REA-05 | Waste disposal log `SOL-LOG-WASTE-TOC`; EHS SOP referenced. |
| FS-LIFE-01 | URS-LIFE-01 | UV lamp install date logged; 30-day warning fires at 11 months; 12-month replacement target. |
| FS-LIFE-02 | URS-LIFE-02 | UV lamp replacement workflow `SOL-WF-LAMP-CHANGE` triggers full PQ. |
| FS-LIFE-02b | URS-LIFE-02b | Lamp intensity captured per acquisition; SOP threshold configurable; drop below fires deviation. |
| FS-LIFE-03 | URS-LIFE-03 | Reactor + ICR replacement log; replacement triggers SST + partial OQ. |
| FS-LIFE-04 | URS-LIFE-04 | Membrane CO₂ detector replacement schedule per Sievers spec; tracked in lifecycle store. |
| FS-ACQ-01 | URS-ACQ-01 | Method library on `\\sol-gmp-fs01\toc-projects\methods` with read-only ACL for analyst AD group; EFFECTIVE methods exposed to runner. |
| FS-ACQ-02 | URS-ACQ-02 | Pre-flight checker evaluates instrument_state, method_state, SST_state, project_lock; any block condition emits blocking-reason audit record. |
| FS-ACQ-03 | URS-ACQ-03 | Acquisition metadata schema: sample_id, source_point, method_id+version, instrument_id, analyst_id, ts, mode (on-line / grab), lamp_hours, reactor_lot. |
| FS-ACQ-04 | URS-ACQ-04 | Mode binding: on-line mode uses sample loop with continuous draw; grab mode uses autosampler; SST cadence differs (URS-SST-02). |
| FS-PROC-01 | URS-PROC-01 | Processing engine applies calibration curve + blank correction; per-method config. |
| FS-PROC-02 | URS-PROC-02 | RFC dialog mandatory on manual reprocessing; min 10-char free text + RFC category. |
| FS-PROC-03 | URS-PROC-03 | Raw `.dpr` files preserved unaltered; derived `.proc` files reference parent raw_id. |
| FS-PROC-04 | URS-PROC-04 | Limit-band evaluator: 30% / 50% / 100% of 500 ppb (or method-defined); flags TREND / OOT / OOS. |
| FS-PROC-05 | URS-PROC-05 | PDF report template `SOL-RPT-TOC` includes raw + derived results, SST status, limit status, ALCOA+ block, SHA-256 hash. |
| FS-PROC-06 | URS-PROC-06 | OOS flag triggers LIMS workflow `LIMS-WF-211192`; water-system sample-point transitions to HOLD. |
| FS-AUD-01 | URS-AUD-01 | Audit-trail event coverage: methods, sequences, results, configuration, USP RS register, lamp / reactor lifecycle, sign-on/off, SST events. |
| FS-AUD-02 | URS-AUD-02 | Audit-trail DB constraint = append-only; delete grant revoked at DBA + vendor level. |
| FS-AUD-03 | URS-AUD-03 | Per-batch review by Senior Analyst (`SOL-AUD-REVIEW-TOC-BATCH`); monthly by QC Manager (`SOL-AUD-REVIEW-TOC-MONTH`). |
| FS-AUD-04 | URS-AUD-04 | Retention 25 y product-release-linked; 7 y default; archival job `SOL-JOB-ARCH-TOC`. |
| FS-PART11-01 | URS-PART11-01 | § 11.10(a) procedural controls: SOP `SOL-SOP-CC-TOC` + `SOL-SOP-IR-TOC`. |
| FS-PART11-02 | URS-PART11-02 | § 11.10(d) access: AD-mapped roles per § 4 URS; quarterly access review. |
| FS-PART11-03 | URS-PART11-03 | § 11.50 e-sign manifestation: username, datetime (NTP), meaning. |
| FS-PART11-04 | URS-PART11-04 | § 11.70 signature/record linking: cryptographic hash binding. |
| FS-PART11-05 | URS-PART11-05 | § 11.100 uniqueness: AD UPN unique identifier. |
| FS-PART11-06 | URS-PART11-06 | § 11.200 re-auth: re-entry of password at every Approve. |
| FS-PART11-07 | URS-PART11-07 | § 11.300 password policy: AD GPO `SOL-LAB-USERS-PWD` (12-char, complexity 3-of-4, 90 d, 5-attempt lockout). |
| FS-DI-01 | URS-DI-01 | Attributable: op_id captured per event. |
| FS-DI-02 | URS-DI-02 | Legible: report renderer enforces font/min-size; PDF/A export. |
| FS-DI-03 | URS-DI-03 | Contemporaneous: NTP timestamps. |
| FS-DI-04 | URS-DI-04 | Original: raw `.dpr` files preserved. |
| FS-DI-05 | URS-DI-05 | Accurate: SST gate + calibration verification per OQ. |
| FS-DI-06 | URS-DI-06 | Complete: archival manifest verifies presence of raw + audit + signature + method-version. |
| FS-INT-01 | URS-INT-01 | DataShare 5 polls LIMS worklist endpoint every 5 min; read-only. |
| FS-INT-02 | URS-INT-02 | Result push triggered only on `result_state=APPROVED`; rejected pushes emit LIMS error code `SOL-TOC-NOT-APPROVED`. |
| FS-INT-03 | URS-INT-03 | LIMS payload includes report_id, instrument_id, method_id+version, reviewer_id, approver_id, sst_status. |
| FS-INT-04 | URS-INT-04 | Pre-push checker evaluates SST_status; block on SST_FAIL / SST_EXPIRED. |
| FS-BAK-01 | URS-BAK-01 | Daily backup job `SOL-JOB-BAK-TOC` to Veeam target; SHA-256 manifest. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore drill `SOL-SOP-RESTORE-TEST`; QC-witnessed. |
| FS-BAK-03 | URS-BAK-03 | RTO ≤ 8 h; RPO ≤ 24 h; verified in restore drill. |
| FS-PERF-01 | URS-PERF-01 | PQ scenario: 30-injection sequence; no crash or data loss. |
| FS-PERF-02 | URS-PERF-02 | UI response ≤ 3 s p95 at PQ. |
| FS-SEC-01 | URS-SEC-01 | AD bind via LDAPS; break-glass `SOL-BG-TOC` vaulted in CyberArk. |
| FS-SEC-02 | URS-SEC-02 | Removable-media GPO `SOL-LAB-USB-BLOCK`; engineering override via change-control. |
| FS-TRN-01 | URS-TRN-01 | LMS courses: `SOL-TOC-101` (analyst), `SOL-TOC-201` (SST + lifecycle); annual re-completion. |
| FS-PR-01 | URS-PR-01 | Periodic review template `SOL-PR-TOC`: configuration, audit-trail evidence, SST trend, lifecycle health, deviations, backup-restore, training, fitness; sign-off QC Manager + QA Manager. |


### 4.1 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem. Conditional-access binding to policy `Lab-Workstation Conditional Access (MFA on interactive logon)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam file-level capture of the per-instrument result store and method library; tier classification = T3; RPO ≤ 72 h; RTO ≤ 72 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; annual QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |

## 5. Configuration Items

| CI ID | Item | Value |
|---|---|---|
| CI-01 | DataPro2 Part 11 module | Enabled; project policy SOL_TOC_PART11 |
| CI-02 | USP <643> RE limits | 85% – 115% |
| CI-03 | TOC compendial limit | 500 ppb (default WFI / PW); per-method override only on approved methods |
| CI-04 | SST cadence | Daily (grab); weekly (on-line) |
| CI-05 | UV lamp life | 12 months; 30-day warning at 11 months |
| CI-06 | Limit bands | 30% / 50% / 100% (TREND / OOT / OOS) |
| CI-07 | Backup retention | 25 y product-release-linked; 7 y default |
| CI-08 | RTO / RPO | 8 h / 24 h |
| CI-09 | Audit-trail review cadence | Per batch (Senior Analyst); monthly (QC Manager) |

## 6. Risks (FS-level)

| ID | Risk | Mitigation |
|---|---|---|
| FR-01 | UV-lamp drift causing under-reported TOC | FS-HW-05 + FS-LIFE-01 + FS-LIFE-02b + FS-SST-05 trend |
| FR-02 | LIMS push of unapproved / SST-failed | FS-INT-02 + FS-INT-04 |
| FR-03 | Audit-trail tampering | FS-AUD-02 append-only |
| FR-04 | Expired USP RS in SST | FS-REA-02 pre-flight block |
| FR-05 | Reactor degradation hiding hard-to-oxidize species | FS-LIFE-03 + FS-SST-01 RE check |
| FR-06 | Carry-over high-TOC → low-TOC | FS-AIQ-03 carry-over test + FS-ACQ-04 mode-aware SST |
| FR-07 | Compendial limit misconfig | FS-CMP-01 + FS-PROC-04 |

## 7. References

SOL-URS-TOC-001 v1.2; 21 CFR Part 11 §§ .10, .50, .70, .100, .200, .300; 21 CFR Part 211 §§ .68, .192, .194; EU GMP Annex 11 §§ 4, 6, 9, 11; USP <643>; USP <645>; USP <1058>; USP <1225>; Ph. Eur. 2.2.44; ICH Q2(R2); PIC/S PI 041; ISPE GAMP 5 (2nd ed., 2022); Sievers / Veolia — *M9 + DataPro2 v2.4 Reference*.

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-HW-01 | FS-HW-01 |
| URS-HW-02 | FS-HW-02 |
| URS-HW-03 | FS-HW-03 |
| URS-HW-04 | FS-HW-04 |
| URS-HW-05 | FS-HW-05 |
| URS-HW-06 | FS-HW-06 |
| URS-SW-01 | FS-SW-01 |
| URS-SW-02 | FS-SW-02 |
| URS-SW-03 | FS-SW-03 |
| URS-SW-04 | FS-SW-04 |
| URS-SW-05 | FS-SW-05 |
| URS-SW-06 | FS-SW-06 |
| URS-SW-07 | FS-SW-07 |
| URS-SW-08 | FS-SW-08 |
| URS-CMP-01 | FS-CMP-01 |
| URS-CMP-02 | FS-CMP-02 |
| URS-CMP-03 | FS-CMP-03 |
| URS-CMP-04 | FS-CMP-04 |
| URS-CMP-05 | FS-CMP-05 |
| URS-AIQ-01 | FS-AIQ-01 |
| URS-AIQ-02 | FS-AIQ-02 |
| URS-AIQ-03 | FS-AIQ-03 |
| URS-AIQ-04 | FS-AIQ-04 |
| URS-AIQ-05 | FS-AIQ-05 |
| URS-AIQ-06 | FS-AIQ-06 |
| URS-SST-01 | FS-SST-01 |
| URS-SST-02 | FS-SST-02 |
| URS-SST-03 | FS-SST-03 |
| URS-SST-04 | FS-SST-04 |
| URS-SST-05 | FS-SST-05 |
| URS-REA-01 | FS-REA-01 |
| URS-REA-02 | FS-REA-02 |
| URS-REA-03 | FS-REA-03 |
| URS-REA-04 | FS-REA-04 |
| URS-REA-05 | FS-REA-05 |
| URS-LIFE-01 | FS-LIFE-01 |
| URS-LIFE-02 | FS-LIFE-02 |
| URS-LIFE-02b | FS-LIFE-02b |
| URS-LIFE-03 | FS-LIFE-03 |
| URS-LIFE-04 | FS-LIFE-04 |
| URS-ACQ-01 | FS-ACQ-01 |
| URS-ACQ-02 | FS-ACQ-02 |
| URS-ACQ-03 | FS-ACQ-03 |
| URS-ACQ-04 | FS-ACQ-04 |
| URS-PROC-01 | FS-PROC-01 |
| URS-PROC-02 | FS-PROC-02 |
| URS-PROC-03 | FS-PROC-03 |
| URS-PROC-04 | FS-PROC-04 |
| URS-PROC-05 | FS-PROC-05 |
| URS-PROC-06 | FS-PROC-06 |
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
| URS-INT-01 | FS-INT-01 |
| URS-INT-02 | FS-INT-02 |
| URS-INT-03 | FS-INT-03 |
| URS-INT-04 | FS-INT-04 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-BAK-03 | FS-BAK-03 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-TRN-01 | FS-TRN-01 |
| URS-PR-01 | FS-PR-01 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | UV-lamp drift causing under-reported TOC | Medium | High | URS-LIFE-01 + URS-LIFE-02b + URS-HW-05 |
| R-02 | LIMS push of unapproved / SST-failed results | Medium | High | URS-INT-02 + URS-INT-04 |
| R-03 | Audit-trail tampering | Low | High | URS-AUD-02 + URS-DI-06 |
| R-04 | USP RS sucrose / BQ expired or contaminated | Medium | High | URS-REA-01 + URS-REA-02 + URS-REA-03 |
| R-05 | Reactor + ICR degradation (incomplete oxidation of hard-to-oxidize organics) | Medium | High | URS-LIFE-03 + URS-SST-01 (RE check) |
| R-06 | Membrane CO₂ detector contamination causing false-high readings | Low | High | URS-LIFE-04 + URS-HW-05 alarm |
| R-07 | Sample-loop carry-over between high-TOC and low-TOC samples | Medium | High | URS-AIQ-03 carry-over test + URS-ACQ-04 mode-aware SST |
| R-08 | Method working range mismatch with sample TOC (over-range) | Low | Medium | URS-AIQ-01 + URS-PROC-04 trend bands |
| R-09 | Compendial limit misconfigured (e.g. 500 ppb vs 50 ppb confusion) | Low | High | URS-CMP-01 + URS-PROC-04 |

Full evaluation in `SOL-RA-TOC-001` *(synthetic)*.

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
