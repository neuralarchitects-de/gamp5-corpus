---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (FS catch-up to URS v1.2 — T2 enrichment; ID alignment fix)"
seed_corpus_basis:
  - "PXC-URS-EMS-001 v1.2 (parent URS)"
  - "GAMP 5 (2nd ed.) Cat 4"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "EU GMP Annex 11; EU GMP Annex 1 (2022 revised)"
  - "ISO 14644-1/-2/-3; ISO 14698; USP <1116>; PIC/S PI 041"
parent_urs:
  document_number: PXC-URS-EMS-001
  version: "1.2"
  file: "../../URS/_generated/final/Environmental_Monitoring_System__Pyxis_Cleanrooms_URS_v1.3.md"
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# Functional Specification (FS)

## Environmental Monitoring System — Vaisala viewLinc 5.2 + Lighthouse APM/ApexZ Continuous Particle Monitors

**Document Number:** PXC-FS-EMS-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** PXC-URS-EMS-001 v1.2 | **Site:** Pyxis Cleanrooms BV, Leiden, NL *(fictional)*
**System Class:** GAMP Cat 4 — Configured Product
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; EU GMP Annex 11 §§ 4, 6, 9, 11; EU GMP Annex 1 (2022 revised); ISO 14644-1/-2/-3; ISO 14698; USP <1116>; PIC/S PI 041.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Cleanroom Engineer) | _____________ | _____________ | _____ |
| Reviewer (Microbiology / EM Manager) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Approver (Head of Sterile Manufacturing) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-11 | (synthetic) | Minor: grade-A/B alarm reliability spec. |
| 1.2 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.2: every URS-ID expanded; Grade A/B/C/D + CPM + viable + alert/action implementations added; ID alignment fix vs v1.0/v1.1 (which used SNS/ALM/EXC short IDs not matching the URS). |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies how Vaisala viewLinc 5.2 + Lighthouse APM/ApexZ are configured and integrated to satisfy `PXC-URS-EMS-001` v1.2 — continuous monitoring of cleanroom temperature, humidity, differential pressure, non-viable particles (CPM), and viable EM result management.

## 2. Scope

Per the URS: Vaisala viewLinc 5.2 server (active + DR), wireless sensor network across Grade A/B/C/D cleanrooms, Vaisala HMP / DPT / PTU sensors, Lighthouse APM continuous particle monitors + ApexZ portable, viewLinc Mobile, AD authentication; integrations with the BMS (read-only cross-reference), eQMS (MasterControl deviations), Watson LIMS (viable + microbial-ID), PAS-X (batch-relevance), Halcyon Stability (excursion linkage).

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | GAMP Cat | Notes |
|---|---|---|---|
| C-01 | Vaisala viewLinc 5.2 server (active) | 4 | platform; Win Server 2022 |
| C-02 | viewLinc 5.2 server (DR / warm-standby) | 4 | replicated |
| C-03 | Vaisala HMP / DPT / PTU sensors | 4 | wireless + wired (~180) |
| C-04 | Lighthouse APM continuous particle monitors | 4 | ~25 units; OPC UA / Modbus |
| C-05 | Lighthouse ApexZ portable particle counters | 4 | at-rest / qualification |
| C-06 | viewLinc Mobile | 4 | iOS app |
| C-07 | AD / NTP | (infra) | AuthN + time |
| C-08 | BMS | 4 | cross-reference counterparty |
| C-09 | MasterControl eQMS | 4 | deviation counterparty |
| C-10 | Watson LIMS | 4 | viable + microbial-ID counterparty |
| C-11 | PAS-X MES | 4 | batch-record counterparty |
| C-12 | Halcyon Stability | 4 | excursion-linkage counterparty |

### 3.2 Logical Architecture (textual)

```
                ┌──────────────────────────────────────────────┐
                │   AD / Kerberos    │   NTP                    │
                └────────────┬───────────────┬─────────────────┘
                             │               │
   ┌─────────────────────────▼───────────────▼──────────────────────┐
   │              Vaisala viewLinc 5.2 (active + DR)                 │
   │   ┌────────────────┐  ┌──────────────────────────────────┐    │
   │   │ Web client     │  │ viewLinc Mobile (iOS)             │    │
   │   └────────────────┘  └──────────────────────────────────┘    │
   │   ┌──────────────────────────────────────────────────────┐    │
   │   │  Wireless sensor network + wired probes               │    │
   │   │  (Vaisala HMP / DPT / PTU)                            │    │
   │   └──────────────────────────────────────────────────────┘    │
   │   ┌──────────────────────────────────────────────────────┐    │
   │   │  Lighthouse APM CPM + ApexZ portable                 │    │
   │   └──────────────────────────────────────────────────────┘    │
   └────────┬─────────────────────────────────────┬────────────────┘
            │                                     │
            ▼                                     ▼
        BMS (cross-ref) │ MasterControl (deviation) │ LIMS (viable) │ PAS-X (batch) │ Halcyon (excursion)
```

## 4. Functional Specifications

### 4.1 Platform / Hardware (URS §5.1)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PLAT-01 | URS-PLAT-01 | Active + warm-standby viewLinc 5.2 on Windows Server 2022; manual failover within 1 h tested via OQ procedure `PXC-OQ-FAILOVER-01`. |
| FS-PLAT-02 | URS-PLAT-02 | UPS sized ≥ 30 min; ride-through tested. |
| FS-PLAT-03 | URS-PLAT-03 | Servers on facilities-IT VLAN; firewall denies office-network routing. |
| FS-PLAT-04 | URS-PLAT-04 | Gateway-network design includes ≥ 1-hop redundancy per zone; reduced-redundancy state surfaces `GW_DEGRADED` alarm. |

### 4.2 Cleanroom Grade A/B/C/D Mapping (URS §5.2)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-GRADE-01 | URS-GRADE-01 | Location table `locations` has `annex1_grade` enum (`A`, `B`, `C`, `D`, `CNC`); required per location. |
| FS-GRADE-02 | URS-GRADE-02 | Location additionally carries `iso14644_class_at_rest` + `iso14644_class_in_operation` columns. |
| FS-GRADE-03 | URS-GRADE-03 | `limit_table_per_grade.yaml` stores T / RH / DP / particle limits per grade; Microbiology Manager signature required on limit-change CRs. |
| FS-GRADE-04 | URS-GRADE-04 | Grade-A + B locations enforce CPM presence in `cpm_required_locations`; missing CPM raises critical alarm. |
| FS-GRADE-05 | URS-GRADE-05 | Grade-A locations require ≥ 2 CPM units in HA pairing; loss of either raises `CPM_LOSS_GRADE_A` critical alarm. |

### 4.3 Probes / Loggers / Particle Counters (URS §5.3)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PROBE-01 | URS-PROBE-01 | `probe_inventory` table stores unique-id, location, cal-cert-id, cal-due-date. |
| FS-PROBE-02 | URS-PROBE-02 | Expired-calibration probes flagged `OUT-OF-SERVICE`; excluded from release-supporting reports until recalibrated. |
| FS-PROBE-03 | URS-PROBE-03 | Drift detection via configurable health-check thresholds; suspected drift raises `PROBE_DRIFT_<id>` maintenance alarm. |
| FS-PROBE-04 | URS-PROBE-04 | Logging interval configured per location: default 1 min cleanrooms, 5 min warehouses. |
| FS-PROBE-05 | URS-PROBE-05 | Coincidence-loss correction per Lighthouse vendor coefficient applied at the boundary. |

### 4.4 Continuous Particle Monitoring (URS §5.4)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CPM-01 | URS-CPM-01 | Grade-A CPM continuous; ≥ 0.5 µm + ≥ 5 µm channels reported per Annex 1 § 9.16; OPC UA / Modbus to APM units; data sampled at vendor rate. |
| FS-CPM-02 | URS-CPM-02 | Grade-B CPM during operations per site EM plan; schedule per `cpm_schedule.yaml`. |
| FS-CPM-03 | URS-CPM-03 | CPM data linked to batch records via PAS-X `EM-batch-relevance` API; linked rows in `cpm_batch_link`. |
| FS-CPM-04 | URS-CPM-04 | At-rest classification per ISO 14644-2 scheduled via `qualification_scheduler`; results recorded in `classification_results`. |

### 4.5 Alarm Logic and Excursion Handling (URS §5.5)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ALARM-01 | URS-ALARM-01 | Alarms classified `INFORMATION / WARNING / ACTION_LIMIT / ALERT_LIMIT`; routing per `alarm_routing.yaml`. |
| FS-ALARM-02 | URS-ALARM-02 | Action / Alert alarms require ack with reason; unacknowledged > window auto-creates MasterControl deviation. |
| FS-ALARM-03 | URS-ALARM-03 | Grade-A / B alarms routed via two independent channels (SMS via Twilio + email via SES + push via FCM); failure of one channel monitored. |
| FS-ALARM-04 | URS-ALARM-04 | Alarm-ack latency measured via synthetic monitoring; P95 ≤ 30 s SLO. |
| FS-ALARM-05 | URS-ALARM-05 | Excursion events linked to affected batches via PAS-X `EM-batch-relevance` API (location + time-window match); auto-deviation includes batch-impact list. |

### 4.6 Viable Sampling Integration (URS §5.6)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VIAB-01 | URS-VIAB-01 | Viable-entry form in viewLinc + REST pull from Watson LIMS `GET /viable/{location}/{date}`; records location + sample-time + grade + analyst. |
| FS-VIAB-02 | URS-VIAB-02 | Viable results trended in unified dashboard; exceedances of per-grade alert / action limits per `limit_table_per_grade.yaml` auto-deviate. |
| FS-VIAB-03 | URS-VIAB-03 | Microbial-ID results from LIMS link via `microbial_id` table; surfaced in excursion-investigation view. |
| FS-VIAB-04 | URS-VIAB-04 | Viable-sampling schedule per location + cadence in `viable_schedule.yaml`; missed samples raise `VIABLE_MISSED` warning. |

### 4.7 Trend Analysis + Alert / Action Limits (URS §5.7)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TREND-01 | URS-TREND-01 | Rolling-window trend engine computes 24-h / 7-d / 30-d; surfaced in Grafana dashboard `pxc-em-trends`. |
| FS-TREND-02 | URS-TREND-02 | Recurring-excursion detector flags ≥ N excursions in rolling window per Annex 1 § 9 trend-investigation requirement. |
| FS-TREND-03 | URS-TREND-03 | Periodic-review report aggregates false-positive / false-negative + alert / action limit excursions + calibration overdue counts. |
| FS-TREND-04 | URS-TREND-04 | Limit-change events in `limit_change_history`; trend-baseline recomputed on change. |

### 4.8 Audit Trail (URS §5.8)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Audit events in `audit_events` covering config changes, data corrections, alarm acks, viable entries, signatures. |
| FS-AUD-02 | URS-AUD-02 | Append-only via DB triggers; admin role denied UPDATE / DELETE. |
| FS-AUD-03 | URS-AUD-03 | Monthly review by EM Reviewer; quarterly by QA Compliance; review records signed. |
| FS-AUD-04 | URS-AUD-04 | Retention 25 y in `audit_events_archive` (S3 object-lock). |

### 4.9 21 CFR Part 11 (URS §5.9)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural controls in `/sop/`; reviewed annually. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(d): AD Kerberos + MFA via Yubikey. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(e): audit per FS-AUD-01. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.50: e-sig fields enforced (printedName + dateTime + meaning); meaning enum validated. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.70: SHA-256(record) bound; tamper invalidates signature. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.100: AD HR-feed; reuse blocked at provisioning. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.200: fresh Kerberos ticket max-age 5 min for sign-off. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.300: AD password policy ≥ 14 chars + complexity + 90 d rotation + MFA. |

### 4.10 Reporting (URS §5.10)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-RPT-01 | URS-RPT-01 | Batch-release EM report generated via PAS-X EM-link; includes locations, time window, alarm summary, viable summary, signature page, SHA-256 report hash. |
| FS-RPT-02 | URS-RPT-02 | Periodic trend reports configurable (daily / weekly / monthly / quarterly); signed by EM Reviewer + Microbiology Manager. |
| FS-RPT-03 | URS-RPT-03 | Reports reference probe-calibration-cert-IDs valid for the reported window. |
| FS-RPT-04 | URS-RPT-04 | Per-grade summaries (A / B / C / D) with Annex 1 limits applied. |

### 4.11 Integrations (URS §5.11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-EQMS-01 | URS-INT-EQMS-01 | Unacknowledged alarms > window auto-create MasterControl deviation via `POST /api/v2/deviations`; idempotency key. |
| FS-INT-BMS-01 | URS-INT-BMS-01 | BMS HVAC trend data consumed read-only via OPC UA; surfaced as cross-reference panel. |
| FS-INT-LIMS-01 | URS-INT-LIMS-01 | Watson LIMS REST `/viable/...` + `/microbial-id/...` ingested; mTLS. |
| FS-INT-MES-01 | URS-INT-MES-01 | PAS-X `GET /em-relevance?location=&from=&to=` returns batches affected; used for excursion linkage. |
| FS-INT-STAB-01 | URS-INT-STAB-01 | Excursion events affecting stored samples pushed to Halcyon `POST /stability/excursion-impact`. |
| FS-INT-AD-01 | URS-INT-AD-01 | LDAPS / Kerberos to `pyxis.local`; AD groups `EMS-Operator`, `EMS-Reviewer`, `EMS-Microbiology`, `EMS-FacilitiesEng`, `EMS-Cal`, `EMS-Approver`, `EMS-Admin`, `EMS-Auditor`. |

### 4.12 Data Integrity + Backup + Performance + Security (URS §5.12)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DI-01 | URS-DI-01 | Audit-write NOT-NULL `actor_id`. |
| FS-DI-02 | URS-DI-02 | PDF/A-3 + CSV export validated at OQ. |
| FS-DI-03 | URS-DI-03 | NTP + gateway-side buffering preserves probe-side timestamps during short network outages. |
| FS-DI-04 | URS-DI-04 | Raw probe readings immutable; corrections recorded as new annotated values. |
| FS-DI-05 | URS-DI-05 | Rolling-average + ISO 14644 classification math regression-tested at OQ. |
| FS-DI-06 | URS-DI-06 | Metadata completeness validated; retrievable ≤ 1 BD via inspection-mode query. |
| FS-BAK-01 | URS-BAK-01 | Nightly PITR-enabled DB backup to S3; 25 y retention. |
| FS-BAK-02 | URS-BAK-02 | Quarterly restore-test scripted; QA witness sign-off. |
| FS-BAK-03 | URS-BAK-03 | DR replication: RTO ≤ 4 h, RPO ≤ 5 min. |
| FS-PERF-01 | URS-PERF-01 | OQ stress run: ≥ 30 days continuous logging from all probes at configured interval without data loss. |
| FS-PERF-02 | URS-PERF-02 | Trend-report generation P95 ≤ 30 s for 96-h × 30 locations test case. |
| FS-SEC-01 | URS-SEC-01 | AD-managed accounts; break-glass admin sealed in HashiCorp Vault. |
| FS-SEC-02 | URS-SEC-02 | SMS / email / push channels authenticated + rate-limited; egress allow-listed. |
| FS-SEC-03 | URS-SEC-03 | Tenable Nessus monthly; 30-day SLA on critical findings. |

### 4.13 Training / Periodic Review (URS §5.13)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | Cornerstone LMS curriculum `PXC-CURR-EMS-<role>-v1`. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher `EMS-2026-ANNUAL` covers Annex 1 (2022) updates + viable-sampling SOPs. |
| FS-PR-01 | URS-PR-01 | Periodic-review template `PXC-PR-EMS-YYYYMMDD` covers configuration drift, calibration status, alarm performance, viable trends, limit changes, backup/restore, training; signed by Facilities Engineering Lead + Microbiology Manager + Head of QA. |


### 4.14 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: LDAPS on-prem. Conditional-access binding to policy `OT-EMS Conditional Access (MFA at engineering workstation; operator stations named-location)`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with MS SQL Server VSS for the EMS historian DB; tier classification = T2; RPO ≤ 24 h; RTO ≤ 24 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; quarterly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.15 Cross-System Integration — eQMS handover (M-XINT-EQMS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-EQMS-01 | URS-XINT-EQMS-01 | CAPA-event publisher posts to eQMS endpoint `POST /capa/tickets` with mTLS + Entra workload-identity; payload schema `eqms.ticket.v1`; OpenAPI artefact `xint-eqms.openapi.yaml`; outbound retry with exponential back-off and DLQ at 5 attempts. |
| FS-XINT-EQMS-02 | URS-XINT-EQMS-02 | eQMS ticket-status webhook subscribed; payload `eqms.status.v1`; consumer rule maps eQMS status `(OPEN, IN-PROGRESS, EFFECTIVENESS, CLOSED)` onto originating-record disposition fields; closed-loop verification gate prevents disposition without `eqms_status=CLOSED`. |

## 5. Non-Functional Specifications

| NFR ID | Specification |
|---|---|
| NFR-01 | Critical-alarm notification ≤ 30 s P95 |
| NFR-02 | Sensor sampling per EMS plan |
| NFR-03 | Audit trail append-only; retention ≥ 25 y |
| NFR-04 | Excursion linkage to Halcyon ≤ 1 h |
| NFR-05 | Trend-report P95 ≤ 30 s |
| NFR-06 | DR replication lag ≤ 5 min |

## 6. Configuration Items (CI)

| CI ID | Item | Value |
|---|---|---|
| CI-01 | Per-grade alarm limits | per Annex 1 + ISO 14644 + product-specific |
| CI-02 | Notification cadence | SMS + email ≤ 30 s for criticals |
| CI-03 | DR replication-lag alert | > 5 min |
| CI-04 | Calibration overdue | OUT-OF-SERVICE flag |
| CI-05 | CPM grade-A redundancy | ≥ 2 units per location |
| CI-06 | Viable-sampling schedule | `viable_schedule.yaml` |
| CI-07 | Limit-change-history retention | ≥ 25 y |
| CI-08 | LIMS endpoint | `https://lims.pyxis.local/api/v1` |
| CI-09 | PAS-X EM-relevance endpoint | `https://pasx.pyxis.local/api/v1/em-relevance` |
| CI-10 | Halcyon excursion endpoint | `https://halcyon.pyxis.local/api/v1/stability/excursion-impact` |

## 7. Constraints / Assumptions / Risks

- Constraints: Vaisala + Lighthouse vendor patches under change control.
- Assumptions: BMS, Halcyon, AD, NTP, LIMS, PAS-X validated.
- Risks: missed critical alarm (FS-ALARM-02 + redundant notification paths); calibration drift undetected (FS-PROBE-03); sensor relocation not recorded (configuration audit); excursion not linked (FS-ALARM-05); CPM degradation on grade-A undetected (FS-GRADE-05); alert/action limit creep (FS-GRADE-03 + Microbiology Manager co-approval); viable-entry data-integrity gap (FS-VIAB-01 + audit).

## 8. References

- PXC-URS-EMS-001 v1.2; 21 CFR Part 11; EU GMP Annex 11; Annex 1 (2022); ISO 14644-1/-2/-3; ISO 14698; USP <1116>; PIC/S PI 041.
- ISPE GAMP 5 (2nd ed., 2022); ISPE GPG *Environmental Monitoring*.
- Vaisala — *viewLinc 5.2 Reference*; Lighthouse — *APM + ApexZ Reference*.

## 9. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-PLAT-01 | FS-PLAT-01 |
| URS-PLAT-02 | FS-PLAT-02 |
| URS-PLAT-03 | FS-PLAT-03 |
| URS-PLAT-04 | FS-PLAT-04 |
| URS-GRADE-01 | FS-GRADE-01 |
| URS-GRADE-02 | FS-GRADE-02 |
| URS-GRADE-03 | FS-GRADE-03 |
| URS-GRADE-04 | FS-GRADE-04 |
| URS-GRADE-05 | FS-GRADE-05 |
| URS-PROBE-01 | FS-PROBE-01 |
| URS-PROBE-02 | FS-PROBE-02 |
| URS-PROBE-03 | FS-PROBE-03 |
| URS-PROBE-04 | FS-PROBE-04 |
| URS-PROBE-05 | FS-PROBE-05 |
| URS-CPM-01 | FS-CPM-01 |
| URS-CPM-02 | FS-CPM-02 |
| URS-CPM-03 | FS-CPM-03 |
| URS-CPM-04 | FS-CPM-04 |
| URS-ALARM-01 | FS-ALARM-01 |
| URS-ALARM-02 | FS-ALARM-02 |
| URS-ALARM-03 | FS-ALARM-03 |
| URS-ALARM-04 | FS-ALARM-04 |
| URS-ALARM-05 | FS-ALARM-05 |
| URS-VIAB-01 | FS-VIAB-01 |
| URS-VIAB-02 | FS-VIAB-02 |
| URS-VIAB-03 | FS-VIAB-03 |
| URS-VIAB-04 | FS-VIAB-04 |
| URS-TREND-01 | FS-TREND-01 |
| URS-TREND-02 | FS-TREND-02 |
| URS-TREND-03 | FS-TREND-03 |
| URS-TREND-04 | FS-TREND-04 |
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
| URS-PART11-08 | FS-PART11-08 |
| URS-RPT-01 | FS-RPT-01 |
| URS-RPT-02 | FS-RPT-02 |
| URS-RPT-03 | FS-RPT-03 |
| URS-RPT-04 | FS-RPT-04 |
| URS-INT-EQMS-01 | FS-INT-EQMS-01 |
| URS-INT-BMS-01 | FS-INT-BMS-01 |
| URS-INT-LIMS-01 | FS-INT-LIMS-01 |
| URS-INT-MES-01 | FS-INT-MES-01 |
| URS-INT-STAB-01 | FS-INT-STAB-01 |
| URS-INT-AD-01 | FS-INT-AD-01 |
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-BAK-03 | FS-BAK-03 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-EQMS-01 | FS-XINT-EQMS-01 |
| URS-XINT-EQMS-02 | FS-XINT-EQMS-02 |

## 10. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Undetected probe drift causing false-pass on grade-A area | Medium | High | URS-PROBE-03, URS-PROBE-02 |
| R-02 | Alarm-routing failure on Annex 1 grade-A/B | Low | High | URS-ALARM-03 |
| R-03 | Audit-trail tampering | Low | High | URS-AUD-02 |
| R-04 | Data-loss during gateway outage | Medium | High | URS-DI-03 + URS-PLAT-04 |
| R-05 | CPM failure on grade-A undetected | Low | Critical | URS-GRADE-05 |
| R-06 | Alert-limit creep silently relaxes thresholds | Low | High | URS-GRADE-03 + Microbiology co-approval |
| R-07 | Viable-result entry data-integrity gap | Low | High | URS-VIAB-01 + audit |
| R-08 | Excursion not linked to affected batch | Low | High | URS-ALARM-05 + URS-INT-MES-01 |

Full evaluation in `PXC-RA-EMS-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
