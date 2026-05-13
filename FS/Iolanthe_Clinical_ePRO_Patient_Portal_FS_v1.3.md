---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; expanded 2026-05-12 (FS catch-up to URS v1.2; full per-ID expansion of 106 URS-IDs per § 2A.7; FS-DCD + FS-RLR + FS-ONB + FS-AE + FS-LIB + FS-BYOPID + FS-TZ + FS-RR + FS-CCM sections added)"
seed_corpus_basis:
  - "IOL2-URS-EPRO-001 v1.2"
  - "ISPE GAMP 5 (2nd Edition, 2022) Cat 4 SaaS conventions"
  - "21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300"
  - "ICH E6(R3) — Good Clinical Practice (Step 4, adopted 6 January 2025); ICH E8(R1); ICH E9(R1); ICH E2A"
  - "EU Clinical Trials Regulation 536/2014; CTIS"
  - "GDPR Arts. 6, 9, 22, 32, 35"
  - "FDA Patient-Reported Outcome Measures (2009); PFDD Guidance series"
  - "HIPAA / HITECH"
  - "ISPOR Translation Principles"
  - "BfArM (DE); Paul-Ehrlich-Institut (DE); Swissmedic (CH); AGES PharmMed (AT)"
parent_urs:
  document_number: IOL2-URS-EPRO-001
  version: 1.2
  file: ../../URS/_generated/final/ePRO_Patient_Portal__Iolanthe_Clinical_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling: {evidence_level: synthetic_seeded, signature_status: placeholders, production_status: simulated_or_example, source_risk: ai_authored_disclosed}
---

# Functional Specification (FS)

## ePRO / eCOA Patient Portal — Clario eCOA Platform 2025

**Document Number:** IOL2-FS-EPRO-001 | **Version:** 1.2 | **Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** IOL2-URS-EPRO-001 v1.2 | **Site:** Iolanthe Clinical Operations GmbH, Wien, Austria *(fictional)*
**System Class:** GAMP Cat 4 — Configured Product (multi-tenant SaaS)
**Regulatory Scope:** 21 CFR Part 11 §§ .10, .30, .50, .70, .100, .200, .300; ICH E6(R3) GCP (Step 4, adopted 6 January 2025); ICH E8(R1); ICH E9(R1); EU CTR 536/2014; CTIS; FDA PRO Guidance (2009); HIPAA / HITECH; GDPR Arts. 6, 9, 22, 32, 35; ISPOR Translation Principles; BfArM (DE); Paul-Ehrlich-Institut (DE); Swissmedic (CH); AGES PharmMed (AT).

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (Director, eCOA Operations) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Privacy / DPO) | _____________ | _____________ | _____ |
| Reviewer (Sponsor Clinical Lead) | _____________ | _____________ | _____ |
| Reviewer (Reg Affairs — CTIS) | _____________ | _____________ | _____ |
| Approver (VP Clinical Operations) | _____________ | _____________ | _____ |
| Approver (VP QA) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue. |
| 1.1 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.1: ICH E6(R3) GCP + EU CTR / CTIS integration; GDPR Arts. 6/9/22/32/35 implementation; BYOD/MDM controls; DACH language variants; RBM data feed per ICH E6(R3) §3.10; Wien (AT) deployment context. |
| 1.2 | 2026-05-12 | (synthetic) | FS catch-up to URS v1.2: full per-ID expansion of 106 URS-IDs (no range compression per § 2A.7). Added FS-DCD (Diary Compliance Dashboard), FS-RLR (Reminder Ladder + Drop-off Recovery), FS-ONB (Patient Onboarding), FS-AE (AE Capture EDC Integration), FS-LIB (eCOA Library Mgmt), FS-BYOPID (Pseudonymisation Boundary), FS-TZ (Time-Zone-Aware Schedule), FS-RR (Recruitment + Retention Tools), FS-CCM (Configuration Management); FS-SEC-01..05 dedup-corrected per spec. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies Clario eCOA Platform 2025 configuration to satisfy `IOL2-URS-EPRO-001` v1.1, including v1.1 additions for ICH E6(R3) (Step 4, 2025) GCP, EU CTR / CTIS integration, GDPR Article-level implementations, RBM data feed, and DACH-specific language + competent-authority bindings.

## 2. Scope

Clario eCOA Platform 2025 tenancy; per-study configuration with CTIS-compatible study-build pack; SSO via Okta + MFA for site users; integrations with EDC (Marigold) + eTMF (Marinos) + CTIS portal; DACH language variants (de-DE, de-AT, de-CH).

## 3. System Architecture

```
   Okta SSO + MFA (site users)        Patient credentials + MFA where supported
            │                                  │
            ▼                                  ▼
   ┌────────────────────────────────────────────────┐
   │  Clario eCOA Platform 2025 (Iolanthe tenancy)  │
   │  Mobile app + Web + Provisioned-tablet         │
   │  Linguistic-validated per language             │
   │  RBM data feed per ICH E6(R3) §3.10            │
   └─┬───────────┬──────────────┬─────────────────┬─┘
     │           │              │                 │
     ▼           ▼              ▼                 ▼
   EDC          eTMF        CTIS portal       Sponsor RBM
   (Marigold)   (Marinos)   (EU CTR Art. 25)  dashboard
```

## 4. Functional Specifications

| FS ID | URS ID | Specification |
|---|---|---|
| FS-VND-01 | URS-VND-01 | Clario vendor-assurance: SOC 2 Type II + ISO 27001 + HIPAA evidence; annual re-qualification. |
| FS-VND-02 | URS-VND-02 | Vendor release-notes review automated alert; site change-control gate. |
| FS-CFG-01 | URS-CFG-01 | Per-study config: DEV → QC → UAT → PRODUCTION; SoD enforced (Author ≠ Approver). |
| FS-CFG-02 | URS-CFG-02 | CTIS-compatible study-build pack exporter per EU CTR Art. 25 (XML schema). |
| FS-CFG-03 | URS-CFG-03 | Configuration exportable for sponsor inspection; version-controlled. |
| FS-LING-01 | URS-LING-01 | Linguistic-validation certificate registry per language per instrument-version; ISPOR / FDA-compliant. |
| FS-LING-02 | URS-LING-02 | Out-of-validation translation block: API returns 422 when patient attempts to access unvalidated language. |
| FS-LING-03 | URS-LING-03 | DACH language variants enforced as distinct entries: `de-DE`, `de-AT`, `de-CH`, plus `fr-CH`, `it-CH`. |
| FS-LING-04 | URS-LING-04 | Instrument-version-change watcher invalidates dependent translations; re-validation flow triggered. |
| FS-PAT-01 | URS-PAT-01 | Entry schema: pseudonymised `patient_id`, `instrument_id`, `instrument_version`, NTP-synced `timestamp_iso8601`, `entry_payload`, `language_locale`. |
| FS-PAT-02 | URS-PAT-02 | Time-window enforcement: configurable per instrument (e.g., 06:00–22:00 patient-local-time); out-of-window flagged. |
| FS-PAT-03 | URS-PAT-03 | Adherence dashboard with patient-level + study-level metrics; data feed to RBM. |
| FS-PAT-04 | URS-PAT-04 | Missed-entry alert ladder: push → SMS → site-notification at thresholds. |
| FS-PAT-05 | URS-PAT-05 | NTP-sync verification: device clock-drift > 5 min flags entry; server-side timestamp authoritative. |
| FS-DEV-01 | URS-DEV-01 | BYOD device-registration: device-id + OS + app-version recorded; jailbreak / root detection blocks. |
| FS-DEV-02 | URS-DEV-02 | Provisioned-tablet MDM via Clario MDM service; remote-wipe API < 15 min from loss-report. |
| FS-DEV-03 | URS-DEV-03 | iOS / Android current + n-1 major versions supported; older versions blocked. |
| FS-DEV-04 | URS-DEV-04 | Per-study BYOD-vs-provisioned configuration field with documented rationale. |
| FS-AUD-01 | URS-AUD-01 | Audit-trail schema covers entries + edits + signatures + config changes + translation approvals; append-only DB. |
| FS-AUD-02 | URS-AUD-02 | Tenant-admin cannot UPDATE / DELETE audit records. |
| FS-AUD-03 | URS-AUD-03 | Per-study-build review by site QA + quarterly periodic review. |
| FS-AUD-04 | URS-AUD-04 | Retention ≥ 25 y per ICH E6(R3) and EU CTR. |
| FS-AUD-05 | URS-AUD-05 | Audit-trail review surfaces RBM patterns per ICH E6(R3) §3.10. |
| FS-PART11-01 | URS-PART11-01 | Per § 11.10(a): procedural controls protecting electronic-record validity documented in `/sop/`; reviewed annually. |
| FS-PART11-02 | URS-PART11-02 | Per § 11.10(d): access limited to authorised individuals via Okta SAML 2.0 + MFA; service accounts via mTLS only. |
| FS-PART11-03 | URS-PART11-03 | Per § 11.10(e): operational audit trail capturing user, action, date, time — implemented via FS-AUD-01. |
| FS-PART11-04 | URS-PART11-04 | Per § 11.50: electronic signatures include signer's printed name, date and time of signing, and meaning of signature; schema enforced in DB. |
| FS-PART11-05 | URS-PART11-05 | Per § 11.70: signatures cryptographically linked to the signed record via HMAC-SHA256 over record-hash + signer-id + timestamp; tampered records flagged on read. |
| FS-PART11-06 | URS-PART11-06 | Per § 11.100: signature unique per individual; reuse / reassignment blocked at provisioning via Okta-DB uniqueness constraint. |
| FS-PART11-07 | URS-PART11-07 | Per § 11.200: re-authentication required at the moment of signing (fresh OAuth2 token, max-age 5 min); cached credentials rejected. |
| FS-PART11-08 | URS-PART11-08 | Per § 11.300: password / credential controls per site InfoSec policy — MFA mandatory, lockout after 5 fails in 15 min, complexity per site standard. |
| FS-DI-01 | URS-DI-01 | **Attributable:** every action / entry carries `actor_id` (named user or service-account); DB constraint not-null at audit-write. |
| FS-DI-02 | URS-DI-02 | **Legible:** records exportable as PDF/A-3 + machine-readable JSON/XML; rendering verified via OQ. |
| FS-DI-03 | URS-DI-03 | **Contemporaneous:** event timestamps server-side + NTP-synced; retroactive entries flagged with delay reason. |
| FS-DI-04 | URS-DI-04 | **Original:** raw inputs / records preserved in immutable storage; derivative analyses reference but do not overwrite the original. |
| FS-DI-05 | URS-DI-05 | **Accurate:** calculations / transformations deterministic and validated under OQ; floating-point reproducibility verified where applicable. |
| FS-DI-06 | URS-DI-06 | **Complete / Consistent / Enduring / Available:** metadata completeness validated; chronological order DB-enforced; retention per applicable regulation; retrievable within 1 business day. |
| FS-PRV-01 | URS-PRV-01 | GDPR Art. 9: PHI minimisation + pseudonymisation; AES-256 at rest, TLS 1.3 in transit; re-identification only via EDC behind additional controls. |
| FS-PRV-02 | URS-PRV-02 | DPIA URN field per study; presence verified at study-build-approval; mandatory before patient enrolment. |
| FS-PRV-03 | URS-PRV-03 | GDPR Art. 22: automated decisions affecting participant blocked; only adherence-monitoring permitted, no automated protocol changes. |
| FS-PRV-04 | URS-PRV-04 | Cross-border transfer route documented per study; SCCs enforced via vendor DPA for non-adequacy jurisdictions. |
| FS-INT-EDC-01 | URS-INT-EDC-01 | PRO data push to Medidata Rave EDC after sign-off windows; idempotent on entry-id; reconciliation log retained. |
| FS-INT-ETMF-01 | URS-INT-ETMF-01 | Auto-deposit study-build documentation to Marinos eTMF on approval. |
| FS-INT-CTIS-01 | URS-INT-CTIS-01 | CTIS-compatible pack export per EU CTR Art. 25 (XML); validated against CTIS schema in CI. |
| FS-INT-AUTH-01 | URS-INT-AUTH-01 | Site users: Okta SAML 2.0 + MFA. Patients: Clario per-study credentials + MFA where supported. |
| FS-INT-RBM-01 | URS-INT-RBM-01 | RBM data-feed endpoint exposes adherence + completion + time-of-day patterns per ICH E6(R3) §3.10. |
| FS-PERF-01 | URS-PERF-01 | App / web instrument-open P95 ≤ 3 s. |
| FS-PERF-02 | URS-PERF-02 | ≥ 10,000 concurrent patient sessions sustained. |
| FS-AV-01 | URS-AV-01 | Per Clario SLA: ≥ 99.5% normal; ≥ 99.9% sponsor-critical visit windows. |
| FS-AV-02 | URS-AV-02 | Offline-mode capture supported; auto-sync on network restore with conflict-resolution log. |
| FS-BAK-01 | URS-BAK-01 | Vendor-managed backup with daily integrity verification; site verifies RPO ≤ 4 h / RTO ≤ 24 h annually. |
| FS-BAK-02 | URS-BAK-02 | Site tenant-data export with ≥ 25 y cold-storage retention. |
| FS-BAK-03 | URS-BAK-03 | Annual vendor DR test; site reviews report. |
| FS-SEC-01 | URS-SEC-01 | TLS 1.3 in transit + AES-256 at rest enforced platform-wide; vendor evidence on file. |
| FS-SEC-02 | URS-SEC-02 | Patient credentials per-study isolated; account-lockout 5 failures / 15 min. |
| FS-SEC-03 | URS-SEC-03 | Annual vendor SOC 2 Type II + ISO 27001 evidence review; gaps to change control. |
| FS-SEC-04 | URS-SEC-04 | Annual penetration testing of patient-facing endpoints; H/C findings remediated within 30 d. |
| FS-SEC-05 | URS-SEC-05 | PII minimisation enforced; field-level controls in site-user UI; verified under OQ. |
| FS-TRN-01 | URS-TRN-01 | LMS-recorded role-specific training; ICH E6(R3) GCP training mandatory for Site Investigators / Coordinators / Sponsor Monitors. |
| FS-TRN-02 | URS-TRN-02 | Annual refresher `EPRO-2026-ANNUAL`: ICH E6(R3) + GDPR + HIPAA + RBM updates. |
| FS-PR-01 | URS-PR-01 | Annual Periodic Review template; signed by Director eCOA Operations + Privacy Officer + VP QA + VP Clinical Operations. |
| FS-VND-03 | URS-VND-03 | Sub-processor list quarterly review per DPA Annex II; new sub-processors trigger DPIA delta-review. |
| FS-VND-04 | URS-VND-04 | New cross-border data flows assessed against existing SCC routes; new SCC signature where needed. |
| FS-VND-05 | URS-VND-05 | Quarterly SLA-report review; breaches logged in vendor-assurance dossier + eQMS deviation. |
| FS-VND-06 | URS-VND-06 | Annual SDLC-evidence review in `/vendor-assurance/clario/`. |
| FS-VND-07 | URS-VND-07 | Release-note feed subscription + 14-day impact assessment workflow. |
| FS-DCD-01 | URS-DCD-01 | Site-facing Diary Compliance Dashboard with patient adherence over rolling 7/14-day + study-to-date windows. |
| FS-DCD-02 | URS-DCD-02 | Sponsor RBM dashboard with site/study/cohort drill-down to patient-level. |
| FS-DCD-03 | URS-DCD-03 | Adherence outlier alert engine (configurable thresholds; role-targeted escalation). |
| FS-DCD-04 | URS-DCD-04 | Compliance trend reports (time-of-day, day-of-week, protocol-deviation rate) per ICH E6(R3) §3.10. |
| FS-DCD-05 | URS-DCD-05 | Site-coordinator daily worklist auto-prioritised by overdue + outlier patients. |
| FS-RLR-01 | URS-RLR-01 | Reminder ladder: push → SMS → email → site-notification → site outreach; configurable per instrument. |
| FS-RLR-02 | URS-RLR-02 | Patient-local quiet-hours window (22:00–07:00 default); TZ-aware per patient profile. |
| FS-RLR-03 | URS-RLR-03 | Drop-off-recovery workflow after configurable consecutive misses (default 3); site outreach script. |
| FS-RLR-04 | URS-RLR-04 | Patient-fatigue heuristic engine (entry-latency + dwell-time signals) flags retention-risk patients. |
| FS-ONB-01 | URS-ONB-01 | Patient onboarding flow: identity verification + device pairing + study-credential issuance + consent re-confirmation. |
| FS-ONB-02 | URS-ONB-02 | Onboarding-completion event recorded with timestamp + verifier + method; entry-into-study gated on completion. |
| FS-ONB-03 | URS-ONB-03 | Onboarding tutorial available in each supported language; completion tracked. |
| FS-ONB-04 | URS-ONB-04 | Onboarding flow conforms to WCAG 2.1 AA. |
| FS-AE-01 | URS-AE-01 | AE-signal detection engine (out-of-range PRO score + free-text symptom keyword); workflow notification to site investigator. |
| FS-AE-02 | URS-AE-02 | AE data push to Medidata Rave EDC AE module; idempotent on AE-id; reconciliation log. |
| FS-AE-03 | URS-AE-03 | SAE-trigger surfaces immediately on site dashboard with red-flag indicator; site investigator follow-up audit-trailed. |
| FS-AE-04 | URS-AE-04 | AE workflow preserves patient-reported wording; site interpretation captured as separate field. |
| FS-AE-05 | URS-AE-05 | NTP-synced server-side AE event timestamp; patient-claimed onset captured separately per ICH E2A. |
| FS-AE-06 | URS-AE-06 | AE workflow audit cross-link to Sirius Argus PV (separate URS) for PV review. |
| FS-LIB-01 | URS-LIB-01 | eCOA library schema: instrument-type + author + version + licensing + validated languages. |
| FS-LIB-02 | URS-LIB-02 | Instrument-version lifecycle; only licensed + linguistically-validated version assignable. |
| FS-LIB-03 | URS-LIB-03 | Licensing-evidence check per study; missing licence blocks study build. |
| FS-LIB-04 | URS-LIB-04 | Scoring-rule engine deterministic; scoring-rule change triggers re-validation of all dependent studies. |
| FS-LIB-05 | URS-LIB-05 | Custom-instrument workflow requires sponsor + IRB/IEC approval + linguistic-validation evidence. |
| FS-BYOPID-01 | URS-BYOPID-01 | Pseudonymisation enforced at ePRO platform boundary; re-id only in EDC (Marigold) behind separate access controls. |
| FS-BYOPID-02 | URS-BYOPID-02 | Subject-id format configurable per study (sponsor-defined); validation rule rejects identifiable patterns (DOB, MRN). |
| FS-BYOPID-03 | URS-BYOPID-03 | Per-study sampled subject-id Privacy-Officer review during study-build approval. |
| FS-TZ-01 | URS-TZ-01 | Diary schedules expressed in patient-local time; server converts to UTC for storage with TZ + offset metadata. |
| FS-TZ-02 | URS-TZ-02 | DST-transition handling: entry-validity windows respect DST per patient TZ; verified under OQ. |
| FS-TZ-03 | URS-TZ-03 | Patient-TZ-change detection + "time-zone-change" reason-flag on affected entries; reconcilable. |
| FS-TZ-04 | URS-TZ-04 | Multi-site study site-coordinator view shows patient-local time; no silent site-vs-patient mismatch. |
| FS-RR-01 | URS-RR-01 | Recruitment funnel metrics (invitations / interested / consented / onboarded / retained) per site + per study. |
| FS-RR-02 | URS-RR-02 | Retention metrics: drop-off rate + survival curve per study + per site. |
| FS-RR-03 | URS-RR-03 | Mid-study patient-feedback survey deployable separately from PRO instruments. |
| FS-RR-04 | URS-RR-04 | Compensation tracking module; audit-trailed; operates outside patient-data scope. |
| FS-RR-05 | URS-RR-05 | Recruitment-channel attribution field per consented patient where applicable. |
| FS-RR-06 | URS-RR-06 | Patient withdrawal reason captured per IRB/IEC-approved categories where voluntarily provided. |
| FS-CCM-01 | URS-CCM-01 | DEV → QC → UAT → PROD configuration promotion with SoD-enforced approvals. |
| FS-CCM-02 | URS-CCM-02 | Per-study configuration baselines versioned + exportable; baseline-diff drift detection. |
| FS-CCM-03 | URS-CCM-03 | Emergency-change post-implementation review ≤ 5 BD. |


### 4.1 Cross-System Integration (M-XSYS)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XSYS-AD-01 | URS-XSYS-AD-01 | Identity integration with `QTZ-URS-AD-001`: Entra External ID OIDC for patients in a separate tenant; SAML 2.0 via Entra ID for the internal administrator + clinical-monitor surface, with SCIM lifecycle provisioning on the admin tenant. Conditional-access binding to policy `Patient-Facing Conditional Access (MFA via authenticator app or SMS fallback per IRB approval) for patients; Clinical-Sensitive Conditional Access (FIDO2 + device-compliance) for administrators`. SIEM forwarding via syslog (RFC 5424) to Splunk index `gxp-authn` within 5 minutes; SCIM provisioning where the protocol is SAML/OIDC; break-glass accounts gated by CyberArk PAM per AD URS-PAM-* with 24 h password-rotation and dual-witness check-out. |
| FS-XSYS-BAK-01 | URS-XSYS-BAK-01 | Backup integration per `AUR-URS-BACKUP-001`: Veeam Application-Aware processing with Oracle RMAN for the ePRO Oracle backend and MS SQL Server VSS for the admin metadata store; tier classification = T1; RPO ≤ 4 h; RTO ≤ 4 BH; immutable cloud-tier copy in S3 Object Lock Compliance mode (geo-replicated); air-gap LTO-9 monthly rotation; monthly QA-witnessed restore test per AUR-FS-BACKUP-001 procedure; restore-certificate quality records retained ≥ 25 y in the eQMS. |


### 4.2 Cross-System Integration — Marigold EDC (M-XINT-EDC)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-XINT-EDC-01 | URS-XINT-EDC-01 | ePRO-to-EDC publisher posts to `Medidata Rave /datapoints` API in ODM-XML; idempotency key `{study_id, subject_id, visit_id, instrument_id, item_id, completion_ts}`; back-off 1s → 1024s; DLQ topic `iolanthe.edc.dlq`; Prometheus `iolanthe_edc_publish_lag_seconds` alert at > 600 s P95. |
| FS-XINT-EDC-02 | URS-XINT-EDC-02 | Per-datapoint payload includes `{epro_event_id, device_attestation_ts, response_hash_sha256}` in the extended ODM attributes; EDC reconciliation job (daily) compares ePRO published hash vs EDC stored hash → mismatch raises Rave query + Iolanthe deviation in the operations log. |
| FS-XINT-EDC-03 | URS-XINT-EDC-03 | ePRO instrument metadata mirror updated nightly from Rave study-design API; version-guard rejects datapoint publish when active ePRO instrument_version ≠ Rave-registered instrument_version. |

## 5. Configuration Items (CI)

| CI | Item | Value |
|---|---|---|
| CI-01 | Linguistic validation | per language per instrument-version (ISPOR + FDA) |
| CI-02 | Time-window enforcement | configurable per instrument |
| CI-03 | EDC push idempotency | entry-id-based |
| CI-04 | DPIA requirement | per study |
| CI-05 | CTIS submission pack | EU CTR Art. 25 XML schema |
| CI-06 | DACH language variants | de-DE, de-AT, de-CH (separate validated entries) |
| CI-07 | RBM feed | enabled per ICH E6(R3) §3.10 |

## 6. Risks (FS-level)

URS § 9 documents R-01..R-12. Additional FS risks:

- DACH-variant translation drift on shared base translation → mitigation: per-variant certificate enforcement
- CTIS schema version change breaks pack export → mitigation: schema-version pin + CI contract test
- Patient MFA-phone-lost recovery flow social-engineering risk → mitigation: documented manual ID-verification protocol

## 7. References

- IOL2-URS-EPRO-001 v1.1
- 21 CFR Part 11; ICH E6(R3) GCP; ICH E8(R1); ICH E9(R1)
- EU Clinical Trials Regulation 536/2014; CTIS
- FDA PRO Guidance (2009); FDA PFDD Guidance series
- HIPAA / HITECH; GDPR Arts. 6, 9, 22, 32, 35
- ISPOR Translation Principles
- BfArM (DE); Paul-Ehrlich-Institut (DE); Swissmedic (CH); AGES (AT)
- ISPE GAMP 5 (2nd ed., 2022)
- Clario — *eCOA Platform 2025 Configuration Reference*

## 8. Appendix A — URS → FS Traceability Matrix

| URS ID | FS ID |
|---|---|
| URS-VND-01 | FS-VND-01 |
| URS-VND-02 | FS-VND-02 |
| URS-CFG-01 | FS-CFG-01 |
| URS-CFG-02 | FS-CFG-02 |
| URS-CFG-03 | FS-CFG-03 |
| URS-LING-01 | FS-LING-01 |
| URS-LING-02 | FS-LING-02 |
| URS-LING-03 | FS-LING-03 |
| URS-LING-04 | FS-LING-04 |
| URS-PAT-01 | FS-PAT-01 |
| URS-PAT-02 | FS-PAT-02 |
| URS-PAT-03 | FS-PAT-03 |
| URS-PAT-04 | FS-PAT-04 |
| URS-PAT-05 | FS-PAT-05 |
| URS-DEV-01 | FS-DEV-01 |
| URS-DEV-02 | FS-DEV-02 |
| URS-DEV-03 | FS-DEV-03 |
| URS-DEV-04 | FS-DEV-04 |
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
| URS-DI-01 | FS-DI-01 |
| URS-DI-02 | FS-DI-02 |
| URS-DI-03 | FS-DI-03 |
| URS-DI-04 | FS-DI-04 |
| URS-DI-05 | FS-DI-05 |
| URS-DI-06 | FS-DI-06 |
| URS-PRV-01 | FS-PRV-01 |
| URS-PRV-02 | FS-PRV-02 |
| URS-PRV-03 | FS-PRV-03 |
| URS-PRV-04 | FS-PRV-04 |
| URS-INT-EDC-01 | FS-INT-EDC-01 |
| URS-INT-ETMF-01 | FS-INT-ETMF-01 |
| URS-INT-CTIS-01 | FS-INT-CTIS-01 |
| URS-INT-AUTH-01 | FS-INT-AUTH-01 |
| URS-INT-RBM-01 | FS-INT-RBM-01 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-AV-01 | FS-AV-01 |
| URS-AV-02 | FS-AV-02 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-BAK-03 | FS-BAK-03 |
| URS-SEC-01 | FS-SEC-01 |
| URS-SEC-02 | FS-SEC-02 |
| URS-SEC-03 | FS-SEC-03 |
| URS-SEC-04 | FS-SEC-04 |
| URS-SEC-05 | FS-SEC-05 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-VND-03 | FS-VND-03 |
| URS-VND-04 | FS-VND-04 |
| URS-VND-05 | FS-VND-05 |
| URS-VND-06 | FS-VND-06 |
| URS-VND-07 | FS-VND-07 |
| URS-DCD-01 | FS-DCD-01 |
| URS-DCD-02 | FS-DCD-02 |
| URS-DCD-03 | FS-DCD-03 |
| URS-DCD-04 | FS-DCD-04 |
| URS-DCD-05 | FS-DCD-05 |
| URS-RLR-01 | FS-RLR-01 |
| URS-RLR-02 | FS-RLR-02 |
| URS-RLR-03 | FS-RLR-03 |
| URS-RLR-04 | FS-RLR-04 |
| URS-ONB-01 | FS-ONB-01 |
| URS-ONB-02 | FS-ONB-02 |
| URS-ONB-03 | FS-ONB-03 |
| URS-ONB-04 | FS-ONB-04 |
| URS-AE-01 | FS-AE-01 |
| URS-AE-02 | FS-AE-02 |
| URS-AE-03 | FS-AE-03 |
| URS-AE-04 | FS-AE-04 |
| URS-AE-05 | FS-AE-05 |
| URS-AE-06 | FS-AE-06 |
| URS-LIB-01 | FS-LIB-01 |
| URS-LIB-02 | FS-LIB-02 |
| URS-LIB-03 | FS-LIB-03 |
| URS-LIB-04 | FS-LIB-04 |
| URS-LIB-05 | FS-LIB-05 |
| URS-BYOPID-01 | FS-BYOPID-01 |
| URS-BYOPID-02 | FS-BYOPID-02 |
| URS-BYOPID-03 | FS-BYOPID-03 |
| URS-TZ-01 | FS-TZ-01 |
| URS-TZ-02 | FS-TZ-02 |
| URS-TZ-03 | FS-TZ-03 |
| URS-TZ-04 | FS-TZ-04 |
| URS-RR-01 | FS-RR-01 |
| URS-RR-02 | FS-RR-02 |
| URS-RR-03 | FS-RR-03 |
| URS-RR-04 | FS-RR-04 |
| URS-RR-05 | FS-RR-05 |
| URS-RR-06 | FS-RR-06 |
| URS-CCM-01 | FS-CCM-01 |
| URS-CCM-02 | FS-CCM-02 |
| URS-CCM-03 | FS-CCM-03 |
| URS-XSYS-AD-01 | FS-XSYS-AD-01 |
| URS-XSYS-BAK-01 | FS-XSYS-BAK-01 |
| URS-XINT-EDC-01 | FS-XINT-EDC-01 |
| URS-XINT-EDC-02 | FS-XINT-EDC-02 |
| URS-XINT-EDC-03 | FS-XINT-EDC-03 |

## 9. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-01 | Out-of-validation translation used by patient | Medium | High | URS-LING-01, URS-LING-02 (block) |
| R-02 | Patient-data mix-up via BYOD device sharing | Low | Critical | URS-DEV-01, URS-DEV-02 |
| R-03 | HIPAA / GDPR breach via cross-border transfer | Low | Critical | URS-PRV-01, URS-PRV-04, SCCs |
| R-04 | GDPR Art. 22 violation — automated decision affecting patient | Low | High | URS-PRV-03 |
| R-05 | Missed DPIA per study | Low | High | URS-PRV-02 |
| R-06 | Audit-trail tampering | Low | Critical | URS-AUD-02 |
| R-07 | Time-window enforcement bypass due to device-clock drift | Medium | Medium | URS-PAT-05 (NTP-sync flag) |
| R-08 | EDC sync failure causes data-flow gap | Medium | High | URS-INT-EDC-01 (idempotent + reconciliation log) |
| R-09 | CTIS submission pack incompatibility with current CTIS schema | Low | High | URS-INT-CTIS-01 |
| R-10 | Vendor outage during sponsor-critical visit window | Low | High | URS-AV-01 (SLA), URS-AV-02 (offline mode) |
| R-11 | Translation drift on instrument-version change | Medium | Medium | URS-LING-04 |
| R-12 | Patient credential compromise | Medium | High | URS-SEC-02 (lockout), URS-PRV-01 |
| R-13 | Site-vs-patient time-zone mismatch silently mis-flags valid entries | Medium | Medium | URS-TZ-01, URS-TZ-02 |
| R-14 | BYOD device-update (OS / app) induces data-loss / sync failure | Medium | High | URS-DEV-03, URS-AV-02 |
| R-15 | Language-pack drift on instrument-version change | Medium | Medium | URS-LING-04, URS-LIB-04 |
| R-16 | Patient drop-off after symptom-driven fatigue (retention risk) | Medium | Medium | URS-RLR-03, URS-RLR-04 |
| R-17 | AE signal missed because flagged free-text not routed to investigator | Low | High | URS-AE-01, URS-AE-03 |

Full evaluation in `IOL2-RA-EPRO-001` (synthetic).

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
