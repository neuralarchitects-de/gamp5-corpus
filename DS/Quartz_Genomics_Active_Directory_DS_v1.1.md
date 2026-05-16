---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline DS authoring, 2026-05-15"
seed_corpus_basis:
  - "QTZ-FS-AD-001 v1.1 (parent FS)"
  - "QTZ-URS-AD-001 v1.1 (informational)"
  - "GAMP 5 (2nd ed., 2022) — Cat 1 Infrastructure Design Specification"
  - "Microsoft AD DS 2022 + Entra ID Hybrid Federation + ADCS PKI + CyberArk PAM"
  - "CIS Microsoft Windows Server 2022 Benchmark; BSI IT-Grundschutz; DISA STIG"
parent_fs:
  document_number: QTZ-FS-AD-001
  version: 1.1
  file: ../../../FS_FDS/_generated/final/Quartz_Genomics_Active_Directory_FS_v1.3.md
parent_urs:
  document_number: QTZ-URS-AD-001
  version: 1.1
  file: ../../../URS/_generated/final/Active_Directory_Identity_Service__Quartz_Genomics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Infrastructure Design Specification (IDS)

## Active Directory Identity Service — Microsoft AD DS 2022 + Entra ID Hybrid Federation + ADCS PKI + CyberArk PAM

**Document Number:** QTZ-DS-AD-001 | **Version:** 1.1 | **Effective Date:** 2026-05-15 *(synthetic)*
**Parent FS:** QTZ-FS-AD-001 v1.1 | **Parent URS:** QTZ-URS-AD-001 v1.1
**Site:** Quartz Genomics Ltd, Cambridge UK + Munich DE + Basel CH DR *(fictional)*
**System Class (GAMP 5, 2nd ed.):** Category 1 — Infrastructure. **Treatment note:** the parent FS classifies this system as Category 3 (Non-Configured Product — commercial AD DS). Per the assignment prompt's Cat 1 / T2 / IDS designation, this DS is shaped per § 2B.7 (Cat 1 Infrastructure Design Specification — Network Topology + IP Plan; Identity + Authentication Design; NTP; Backup; Hardening Baseline) rather than § 2B.6 (Cat 3 Vendor-Design-Reliance Statement). Both shapes are legitimate for AD DS depending on site classification convention; Quartz uses Cat 1 (infrastructure-qualified) per this DS.
**Project Mode:** Brownfield migration of legacy AD DS 2016 forest to AD DS 2022 with Entra ID hybrid federation + RED-forest tier-0 admin model + CyberArk PAM (per parent URS Project Mode line)
**Tier (inherited from parent URS+FS):** T2
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a/b/c/d/e/g/k), .30, .100, .200, .300; EU GMP Annex 11 §§ 4, 7, 9, 12; ISO/IEC 27001:2022 (Annex A.5/A.8/A.9/A.12/A.16/A.17); NIST SP 800-63B (Digital Identity); **NIS2 Directive (EU) 2022/2555 (essential entity — identity services)**; GDPR Art. 32; BSI IT-Grundschutz (DE); CIS Microsoft Windows Server 2022 Benchmark; DISA STIG for Windows Server 2022 + Active Directory Domain Services.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (Solution Architect — Identity Services) | _____________ | _____________ | _____ |
| Reviewer (CSV Architect) | _____________ | _____________ | _____ |
| Reviewer (Security Architect — Identity) | _____________ | _____________ | _____ |
| Reviewer (Network Architect) | _____________ | _____________ | _____ |
| Reviewer (PKI / ADCS Operator) | _____________ | _____________ | _____ |
| Reviewer (CyberArk PAM Operator) | _____________ | _____________ | _____ |
| Reviewer (Validation Lead) | _____________ | _____________ | _____ |
| Reviewer (DPO) | _____________ | _____________ | _____ |
| Approver (CISO) | _____________ | _____________ | _____ |
| Approver (VP IT Compliance) | _____________ | _____________ | _____ |
| Approver (System Owner — Head of IAM Operations) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | 2026-05-15 *(synthetic)* | (synthetic) | Initial issue. Inherited Tier T2 from parent URS+FS pair. Derived from QTZ-FS-AD-001 v1.1. DS covers 158/178 FS-IDs as DS-IDs through topology + per-CI rollup (no IQ/OQ/PQ for infra per § 2B.7); 20 FS-IDs subsumed under category-level rollup rows (PAM detailed flows + per-GPO detail covered by IDs DS-IDENT-IGA-* and DS-HARDEN-GPO-* aggregations referencing the QTZ-FS-AD-001 row ranges). Infrastructure qualification cited by reference (`QTZ-IQ-AD-001`, `QTZ-IQ-DC-001`, `QTZ-IQ-ADCS-001`, `QTZ-IQ-PAM-001`); no IQ/OQ/PQ test rows in this DS per § 2B.7. |
| 1.1 | 2026-05-16 | (synthetic) | v1.1 patch per Codex review 2026-05-16: frontmatter `parent_fs.file` + `parent_urs.file` paths corrected (`../../...` → `../../../...`); filename suffix `_v1.0.md` → `_v1.1.md`; **Version** field bumped 1.0 → 1.1. See DS CHANGELOG.md for the full v1.1 patch register. |

## Definitions

Inherited from QTZ-URS-AD-001 v1.1 and QTZ-FS-AD-001 v1.1. Additional DS-specific terms:

| Term | Definition |
|---|---|
| IDS | Infrastructure Design Specification (this document) |
| RED-forest | Microsoft Enterprise Access Model administrative reference architecture |
| Tier-0 / Tier-1 / Tier-2 | Microsoft tier model (T0 = identity-critical; T1 = enterprise servers; T2 = end-user devices) |
| AD DS | Active Directory Domain Services |
| ADCS | Active Directory Certificate Services |
| Entra ID | Microsoft Entra ID (formerly Azure AD) |
| CyberArk PAM | Privileged Access Management (CyberArk Vault + EPV + PSM) |
| FSMO | Flexible Single-Master Operation (AD DS roles) |
| KDC | Key Distribution Center (Kerberos) |
| PDC emulator | Primary Domain Controller emulator (FSMO role — also authoritative NTP source for the domain) |
| GPO | Group Policy Object |
| RODC | Read-Only Domain Controller |
| SCIM | System for Cross-domain Identity Management (provisioning protocol) |
| SCP | Service Connection Point |
| LAPS | Local Administrator Password Solution |

## 1. Purpose

This IDS records the technical infrastructure design of the Quartz Genomics Active Directory identity service: AD DS 2022 forest topology + IP plan; identity + authentication design (Entra ID hybrid federation + Kerberos + LDAPS + SAML + OIDC); ADCS PKI design; CyberArk PAM design; time-synchronisation topology; backup + restore design; hardening baseline (CIS + BSI IT-Grundschutz + DISA STIG). The IDS is the input to `QTZ-IQ-AD-001` (infrastructure qualification) and to the security + change-management runbooks. Per § 2B.7(6): no IQ/OQ/PQ for the infrastructure itself in this DS — infrastructure qualification is cited by reference only.

## 2. Scope

**In scope.** AD DS 2022 forest design (single empty-root + production-child); domain-controller + RODC topology across Cambridge (primary), Munich (DR-warm), Basel (DR-warm); FSMO role placement; site + subnet topology; firewall posture; DNS + NTP topology; ADCS PKI hierarchy (offline root + issuing CA); SCIM + SAML + OIDC provisioning to downstream GxP systems (LIMS, MES, eQMS, PV, MDR, etc.); LAPS; CyberArk PAM design (Vault + EPV + PSM); break-glass account design; Entra ID hybrid federation via AD Connect + Federation Server; Conditional Access policies; Kerberos hardening; GPO design (5 top-level GPO families); backup design; CIS / BSI / DISA STIG hardening; monitoring + SIEM forwarding.

**Out of scope.** Per-system identity bindings of downstream systems (those live in the consumer DSs as `DS-XSYS-AD-01` rows); operating-system internal services beyond AD DS; Entra ID tenant-internal control plane (Microsoft SaaS); CyberArk Vault internal cryptographic primitives (CyberArk SDLC).

## 3. Architectural Overview

```
                       ┌─ Cambridge (primary site) ──────────────────────────┐
                       │                                                     │
                       │  Forest root:  quartzgenomics.com (empty)           │
                       │  Production child: corp.quartzgenomics.com          │
                       │                                                     │
                       │  ┌─────────────────────────┐                        │
                       │  │ DC1 (PDC emulator,      │  authoritative NTP    │
                       │  │      RID master,        │  → stratum-2 to       │
                       │  │      Domain naming,     │     ptbtime.de        │
                       │  │      Infra master)      │                        │
                       │  └─────────────────────────┘                        │
                       │  ┌─────────────────────────┐                        │
                       │  │ DC2 (Schema master)     │                        │
                       │  └─────────────────────────┘                        │
                       │  ┌─────────────────────────┐                        │
                       │  │ DC3 (Bridgehead, GC)    │                        │
                       │  └─────────────────────────┘                        │
                       │                                                     │
                       │  ┌─────────────────────────┐                        │
                       │  │ ADCS Issuing CA         │                        │
                       │  └─────────────────────────┘                        │
                       │  (ADCS Root CA — offline, in HSM-equipped vault)   │
                       │                                                     │
                       │  ┌─────────────────────────┐                        │
                       │  │ CyberArk Vault + EPV +  │                        │
                       │  │ PSM (tier-0 isolated)   │                        │
                       │  └─────────────────────────┘                        │
                       │                                                     │
                       │  ┌─────────────────────────┐                        │
                       │  │ AD Connect + Federation │ → Entra ID hybrid     │
                       │  │ Server (sync to Entra)  │                        │
                       │  └─────────────────────────┘                        │
                       └───────────────┬─────────────────────────────────────┘
                                       │ replication via 10 Gbit MPLS
                       ┌───────────────┼─────────────────────────────────────┐
                       │ Munich (DR-warm)                                    │
                       │  DC4 (GC, Bridgehead)                               │
                       │  DC5 (GC)                                           │
                       │  ADCS Issuing CA (warm-replica)                     │
                       │  CyberArk replica                                   │
                       │  AD Connect (failover)                              │
                       └───────────────┬─────────────────────────────────────┘
                                       │
                       ┌───────────────▼─────────────────────────────────────┐
                       │ Basel CH (DR-warm)                                  │
                       │  DC6 (GC, RODC for staff segments)                  │
                       │  CyberArk replica                                   │
                       └─────────────────────────────────────────────────────┘
```

## 4. Network Topology + IP Plan

### 4.1 VLAN / Subnet design

| DS-ID | VLAN ID | Subnet | Purpose | Site | FS-IDs traced |
|---|---|---|---|---|---|
| DS-NET-01 | VLAN 100 | 10.10.0.0/24 | Tier-0 (DCs + ADCS + CyberArk Vault) | Cambridge | FS-ARCH-01, FS-ARCH-02, FS-ARCH-03 |
| DS-NET-02 | VLAN 101 | 10.10.1.0/24 | Tier-0 (DCs + ADCS + CyberArk) | Munich | FS-ARCH-04, FS-ARCH-05 |
| DS-NET-03 | VLAN 102 | 10.10.2.0/24 | Tier-0 (DCs + CyberArk replica) | Basel | FS-ARCH-06, FS-ARCH-07 |
| DS-NET-04 | VLAN 200 | 10.20.0.0/22 | Tier-1 (servers, GxP applications, MES, LIMS, eQMS) | All sites | FS-ARCH-08, FS-AUTHZ-01 |
| DS-NET-05 | VLAN 300 | 10.30.0.0/16 | Tier-2 (end-user devices) | All sites | FS-ARCH-09, FS-AUTHZ-02 |
| DS-NET-06 | VLAN 400 | 10.40.0.0/24 | DMZ (Federation Server, AD Connect outbound) | Cambridge + Munich | FS-ARCH-10, FS-HYB-01 |

### 4.2 Firewall posture

`default-deny` at all VLAN boundaries. Named allow rules (per FS-CYB-* + FS-INT-*):

- VLAN 200 → VLAN 100 on TCP 88 (Kerberos), 389/636 (LDAP/LDAPS), 445 (SMB), 53 (DNS), 3268/3269 (Global Catalog), 5985/5986 (WinRM); deny all else.
- VLAN 300 → VLAN 200 application-specific; VLAN 300 → VLAN 100 forbidden directly (always via VLAN 200 jump).
- VLAN 100 → VLAN 100 inter-site replication on TCP 88, 389/636, 445, 3268/3269, and RPC dynamic range (49152-65535 restricted by IPSec policy).
- DMZ (VLAN 400) → VLAN 100 only via AD Connect service-account on LDAPS + WinRM.
- Tier-0 admin workstations on dedicated VLAN 110 only.

### 4.3 Inter-site replication

| DS-ID | Link | Bandwidth | Replication schedule | FS-IDs |
|---|---|---|---|---|
| DS-NET-07 | Cambridge ↔ Munich | 10 Gbit MPLS | 15-minute sync | FS-ARCH-04 |
| DS-NET-08 | Cambridge ↔ Basel | 10 Gbit MPLS | 15-minute sync | FS-ARCH-06 |
| DS-NET-09 | Munich ↔ Basel | 1 Gbit IPsec | 60-minute sync | — |

## 5. Identity + Authentication Design

### 5.1 Forest + Domain structure

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-IDENT-01 | Forest functional level | Windows Server 2022 | FS-ARCH-01 |
| DS-IDENT-02 | Forest root domain (empty) | `quartzgenomics.com` | FS-ARCH-02 |
| DS-IDENT-03 | Production child domain | `corp.quartzgenomics.com` | FS-ARCH-03 |
| DS-IDENT-04 | Sites | Cambridge, Munich, Basel | FS-ARCH-04..06 |
| DS-IDENT-05 | FSMO placement | DC1 (PDC emulator, RID master, Infrastructure master, Domain naming); DC2 (Schema master) | FS-ARCH-07, FS-ARCH-08 |
| DS-IDENT-06 | RODC | DC6 in Basel for limited staff segments | FS-ARCH-09 |
| DS-IDENT-07 | Global Catalog | DC3, DC4, DC5, DC6 | FS-ARCH-10 |
| DS-IDENT-08 | OU structure | `OU=Tier0`, `OU=Tier1-Servers`, `OU=Tier1-ServiceAccounts`, `OU=Tier2-Users`, `OU=Tier2-Workstations`, `OU=ExternalPartners` | FS-AUTHZ-01, FS-AUTHZ-02 |
| DS-IDENT-09 | Group-naming convention | `<Tier>-<Function>-<Permission>` (e.g. `T1-LIMS-Reader`, `T0-DA-FullAdmin`) | FS-AUTHZ-03, FS-AUTHZ-04 |
| DS-IDENT-10 | Tier-0 admin workstations | `OU=Tier0=PAWs` (Privileged Access Workstations); enforced by GPO `T0-PAW-Lockdown` | FS-AUTHZ-05, FS-AUTHZ-06 |
| DS-IDENT-11 | Service-account naming | `svc-<system>-<purpose>-<tier>` (e.g. `svc-lims-app-t1`); managed Service Accounts (gMSA) preferred | FS-SVC-01..07 |

### 5.2 Authentication protocols + endpoints

| DS-ID | Protocol | Endpoint | Use | FS-IDs |
|---|---|---|---|---|
| DS-AUTHN-01 | Kerberos v5 | DCs on TCP/UDP 88 | Workstation + server auth | FS-KRB-01..08 |
| DS-AUTHN-02 | LDAPS | DCs on TCP 636 (StartTLS on 389 only as fallback) | App-server auth + bind | FS-AUTHN-01, FS-AUTHN-02 |
| DS-AUTHN-03 | NTLM | DCs (legacy only) | Phasing out; LDAP server channel binding required | FS-AUTHN-03 |
| DS-AUTHN-04 | SAML 2.0 | Federation Server `https://fs.quartzgenomics.com/adfs/ls/` | Downstream GxP SaaS SSO | FS-AUTHN-04, FS-HYB-01 |
| DS-AUTHN-05 | OIDC | Entra ID + Federation Server | Modern app integration | FS-AUTHN-05, FS-HYB-02 |
| DS-AUTHN-06 | MFA | Entra ID Conditional Access; FIDO2 phishing-resistant for tier-0 + admin subgroups | All GxP-tier-1 access | FS-AUTHN-06, FS-AUTHN-07, FS-AUTHN-08 |
| DS-AUTHN-07 | LAPS | Microsoft LAPS v2 (Entra ID-backed) | Local admin password management | FS-AUTHN-09 |
| DS-AUTHN-08 | Service-to-service | gMSA + Kerberos | Service-account auth | FS-AUTHN-10, FS-AUTHN-11 |
| DS-AUTHN-09 | Smartcard | Tier-0 admins (PIV) | Tier-0 authentication | FS-AUTHN-11 |
| DS-AUTHN-10 | LDAP signing + channel binding | Enforced cluster-wide | Mitigate LDAP relay attacks | FS-CYB-01..02 |
| DS-AUTHN-11 | Password policy | Length ≥ 15 (Tier-0); ≥ 14 (Tier-1); ≥ 12 (Tier-2); MFA mandatory; rotation 90 d; complexity per InfoSec | FS-PWD-01..07 |

### 5.3 Entra ID hybrid federation

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-HYB-01 | AD Connect sync mode | Password Hash Sync (PHS) + Seamless SSO | FS-HYB-01, FS-HYB-02 |
| DS-HYB-02 | Federation Server | AD FS 2022 cluster (2 nodes in Cambridge + 1 in Munich) | FS-HYB-03 |
| DS-HYB-03 | Sync cadence | 30 min default; on-demand for Tier-0 changes | FS-HYB-04 |
| DS-HYB-04 | Conditional Access policies | Per FS-HYB-05 enumerated policies — GxP-Sensitive, AI-Platform, PV-Sensitive | FS-HYB-05 |
| DS-HYB-05 | Workload identity | Entra ID workload-identity federation for service-to-service | FS-HYB-06 |
| DS-HYB-06 | SCIM provisioning | Per-downstream-system SCIM endpoint | FS-HYB-07 |

### 5.4 ADCS PKI

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-PKI-01 | Root CA | Offline standalone root CA; HSM-equipped vault | FS-PKI-01 |
| DS-PKI-02 | Issuing CA | Enterprise issuing CA (Cambridge + Munich warm-replica) | FS-PKI-02 |
| DS-PKI-03 | Cert templates | Domain Controller (Kerberos), Web Server, Code Signing, User Smartcard, gMSA Workstation Authentication | FS-PKI-03 |
| DS-PKI-04 | Cert lifetime | DC = 1 y; gMSA = 1 y; smartcard = 2 y; code-signing = 3 y; root CA = 20 y; issuing CA = 10 y | FS-PKI-04 |
| DS-PKI-05 | CRL + OCSP | CRL HTTP-published at `crl.quartzgenomics.com`; OCSP at `ocsp.quartzgenomics.com` | FS-PKI-05 |
| DS-PKI-06 | Cert revocation runbook | `SOP-QTZ-AD-PKI-REVOKE-001`; auto-revocation on incident | FS-PKI-06 |

### 5.5 CyberArk PAM

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-PAM-01 | Vault HA pair + DR replica | Cambridge active + Munich standby + Basel DR; tier-0 isolated | FS-PAM-01 |
| DS-PAM-02 | EPV master policy | All Tier-0 + privileged Tier-1 accounts vaulted; auto-rotation 30 d (Tier-0) / 90 d (Tier-1) | FS-PAM-02, FS-PAM-03 |
| DS-PAM-03 | PSM | All Tier-0 admin sessions proxied via PSM; session recording + 25-y retention | FS-PAM-04, FS-PAM-05 |
| DS-PAM-04 | Dual-witness check-out | All Tier-0 + break-glass accounts require dual approval | FS-PAM-06 |
| DS-PAM-05 | Break-glass accounts | 2 emergency accounts per domain; password rotated 24-h after each use; SIEM-monitored | FS-PAM-07, FS-PAM-08 |
| DS-PAM-06 | Just-in-time elevation | Time-bound (max 4 h) admin elevation via CyberArk + Entra PIM integration | FS-PAM-09 |
| DS-PAM-07 | Session recording retention | 25 y per Annex 11 + Part 11 | FS-PAM-10 |

### 5.6 IGA + JML

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-IGA-01 | Joiner workflow | HR feed → Entra ID → AD DS via AD Connect; tier-assignment per role | FS-JML-01, FS-JML-02 |
| DS-IGA-02 | Mover workflow | Role change → re-evaluate group memberships per `role-permission-matrix-2026.yaml` | FS-JML-03, FS-JML-04 |
| DS-IGA-03 | Leaver workflow | HR feed → disable account → revoke group memberships → 60-d retention then delete | FS-JML-05, FS-JML-06 |
| DS-IGA-04 | Access review | Quarterly per Tier-0 + annual per Tier-1 + per-role on change; SailPoint integration | FS-IGA-01..05 |
| DS-IGA-05 | Privileged-access review | Monthly Tier-0 review by CISO + IAM Manager | FS-JML-07..10 |

### 5.7 GPO design

5 top-level GPO families (CIS-derived baseline):

| DS-ID | GPO family | Linked OU | Purpose | FS-IDs |
|---|---|---|---|---|
| DS-GPO-01 | `T0-PAW-Lockdown` | `OU=Tier0` | Tier-0 PAW lockdown per CIS L1+ | FS-GPO-01, FS-GPO-02 |
| DS-GPO-02 | `T1-Server-Baseline` | `OU=Tier1-Servers` | Server baseline per CIS L1 + BSI IT-Grundschutz | FS-GPO-03, FS-GPO-04 |
| DS-GPO-03 | `T2-Workstation-Baseline` | `OU=Tier2-Workstations` | Workstation baseline per CIS L1 | FS-GPO-05, FS-GPO-06 |
| DS-GPO-04 | `T1-Service-Account-Restrict` | `OU=Tier1-ServiceAccounts` | gMSA restrictions | FS-GPO-07, FS-GPO-08 |
| DS-GPO-05 | `Audit-Subcategory-Policy` | All | Advanced audit policy per FS-AUD-* | FS-GPO-09, FS-GPO-10 |

### 5.8 B2B + external partners

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-B2B-01 | External partner OU | `OU=ExternalPartners` | FS-B2B-01 |
| DS-B2B-02 | Cross-tenant access | Entra B2B with conditional access policy `External-Partners-Strict` | FS-B2B-02 |
| DS-B2B-03 | Guest expiry | 90-day default; auto-disable on expiry | FS-B2B-03 |
| DS-B2B-04 | Sensitive-app access | Per-app sponsor approval | FS-B2B-04 |
| DS-B2B-05 | B2B audit | Monthly review by IAM Manager | FS-B2B-05 |

## 6. Time Synchronisation (NTP)

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-NTP-01 | Authoritative source per domain | PDC emulator DC1 in Cambridge | FS-AN11-01, FS-PART11-01 |
| DS-NTP-02 | External stratum-1/2 source | `ptbtime1.ptb.de` (PTB Germany), `time.google.com` (GPS-backed) — both as fallback | FS-AN11-02 |
| DS-NTP-03 | Tier-2 NTP source | Each DC syncs from PDC emulator with 60-s polling | FS-AN11-03 |
| DS-NTP-04 | Drift threshold | ≤ 5 seconds before alert; ≤ 30 seconds before isolation | FS-AN11-04, FS-AN11-05 |
| DS-NTP-05 | NTP monitor | Splunk saved-search `qtz-ntp-drift-monitor` + Prometheus | FS-MON-01 |

## 7. Backup + Restore Design

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-BAK-01 | AD DS system-state backup | Daily on every DC (Windows Server Backup + Veeam Application-Aware); kept 30 d hot + 5 y warm + 25 y cold | FS-BAK-01, FS-BAK-02 |
| DS-BAK-02 | ADCS database backup | Daily; backed up to immutable S3 Object Lock 25 y | FS-BAK-03 |
| DS-BAK-03 | CyberArk Vault backup | CyberArk-native backup + Veeam Application-Aware; 25 y cold | FS-BAK-04 |
| DS-BAK-04 | Authoritative-restore runbook | `SOP-QTZ-AD-AUTH-RESTORE-001` — covers single-object restore (recycle bin), single-DC restore, single-site failover, full-forest authoritative restore | FS-BAK-05 |
| DS-BAK-05 | Restore test cadence | Monthly single-object; quarterly single-DC; annual single-site failover; annual full-forest tabletop | FS-BAK-06 |
| DS-BAK-06 | Cross-system Aurora backup (FS-XSYS-BAK equivalent) | Veeam Application-Aware with VSS for DC; 3-2-1-1-0 topology | (cross-system) |

## 8. Hardening Baseline

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-HARDEN-01 | OS hardening | CIS Microsoft Windows Server 2022 Benchmark v1.x (L1 baseline; L2 for Tier-0) + DISA STIG | FS-CYB-01, FS-CYB-02 |
| DS-HARDEN-02 | AD DS hardening | DISA STIG for AD DS 2022 + Microsoft Securing Active Directory recommended practice | FS-CYB-03, FS-CYB-04 |
| DS-HARDEN-03 | LDAP hardening | LDAP signing + channel-binding required; LDAP-S only on critical paths; deprecate StartTLS where possible | FS-CYB-05 |
| DS-HARDEN-04 | SMB hardening | SMB signing required; SMBv1 disabled; SMBv2/3 with encryption | FS-CYB-06 |
| DS-HARDEN-05 | NTLM hardening | NTLMv1 disabled cluster-wide; NTLMv2 audited with goal of decommission by 2027 | FS-CYB-07 |
| DS-HARDEN-06 | Kerberos hardening | AES 256-bit + AES 128-bit only; DES + RC4 disabled; max ticket lifetime 10 h | FS-CYB-08 |
| DS-HARDEN-07 | ADCS hardening | Auditing enabled for all template + CA settings | FS-CYB-09 |
| DS-HARDEN-08 | DC hardening | Restricted-RDP; PAW-only admin access; no Internet access | FS-CYB-10 |
| DS-HARDEN-09 | BSI IT-Grundschutz baseline | OPS.1.1.2 (Operational management), APP.2.2 (AD DS), SYS.2.5 (Windows clients), CON.6 (Backup) | FS-CYB-11 |
| DS-HARDEN-10 | LSA Protection | LSA Protected Process Light enabled on all DCs + admin workstations | FS-CYB-12 |
| DS-HARDEN-11 | Credential Guard | Enabled on all admin workstations and DCs | (FS-CYB-12) |
| DS-HARDEN-12 | Deviation register | Per-deviation entry in `QTZ-AD-HARDEN-DEVIATION-REGISTER` reviewed quarterly | FS-AN11-01..05 |

## 9. Monitoring + Audit Trail

| DS-ID | Item | Value | FS-IDs |
|---|---|---|---|
| DS-AUD-01 | Audit policy | Advanced audit-subcategory policy (DS-GPO-05) — logon, account-mgmt, DS access, object access, system events | FS-AUD-01..08 |
| DS-AUD-02 | SIEM forwarding | Windows Event Forwarding to Splunk index `qtz-ad-audit`; RFC 5424 syslog forwarder ≤ 5 min lag | FS-AUD-04 |
| DS-AUD-03 | Audit retention | Splunk frozen-index 25 y; immutable cold copy in S3 Object Lock | FS-AUD-05 |
| DS-AUD-04 | DC event log monitoring | Critical events (4624, 4625, 4720, 4722, 4724, 4732, 4738, 4756, 4768-4771, 4776) alerted in Splunk | FS-MON-02 |
| DS-AUD-05 | CyberArk session-recording forwarding | Forwarded to Splunk `qtz-pam-audit`; 25-y retention | FS-AUD-06 |
| DS-MON-01 | NTP drift monitor | Per DS-NTP-05 | FS-MON-01 |
| DS-MON-02 | AD replication monitor | `repadmin /showrepl` polled every 5 min; alert on > 30-min lag | FS-MON-03 |
| DS-MON-03 | DC availability monitor | LDAP-bind probe to each DC every 60 s; alert on 3 consecutive failures | FS-MON-04 |
| DS-MON-04 | ADCS expiry monitor | Per DS-PKI-04 cert expiry — D-30 warning, D-7 critical, D-1 page | FS-PERF-03 |

## 10. References

**US**
- 21 CFR Part 11 §§ .10(a/b/c/d/e/g/k), .30, .100, .200, .300
- NIST SP 800-63B (Digital Identity Guidelines — Authentication)
- NIST SP 800-53 r5
- DISA STIG — *Windows Server 2022 Active Directory Domain Services STIG* + *Active Directory Forest STIG*

**EU**
- EU GMP Annex 11 §§ 4, 7, 9, 12
- **NIS2 Directive (EU) 2022/2555 — essential entity (identity services)**
- GDPR Reg. (EU) 2016/679 Art. 32

**International**
- ISO/IEC 27001:2022 — Annex A.5 (Information security policies), A.8 (Asset management), A.9 (Access control), A.12 (Operations security), A.16 (Incident management), A.17 (Business continuity)
- ISO/IEC 27002:2022
- CIS Microsoft Windows Server 2022 Benchmark
- CIS Microsoft Active Directory Benchmark
- Microsoft *Securing Active Directory* (Pass-the-Hash + Pass-the-Ticket mitigation guides)
- Microsoft Enterprise Access Model + RED-forest architecture references
- ISPE GAMP 5 (2nd ed., 2022); GAMP IT Infrastructure Control + Compliance GPG

**DACH**
- **BSI IT-Grundschutz** — OPS.1.1.2 (Operational management), APP.2.2 (Active Directory Domain Services), SYS.2.5 (Windows clients), CON.6 (Data backup)
- BSI BSI-Standard 200-1/200-2/200-3 (IT-Grundschutz methodology)
- BfArM (DE) — identity-services inspection focus

**Vendor**
- Microsoft — *Active Directory Domain Services Operations Guide for Windows Server 2022*
- Microsoft — *Entra ID Connect Sync Reference*
- Microsoft — *AD FS 2022 Administrator Guide*
- Microsoft — *ADCS Design + Operations Reference*
- Microsoft — *LAPS v2 Administrator Guide*
- CyberArk — *Vault, EPV, PSM Administrator Guides + best-practice Tier-0 isolation*

## 11. Appendix A — DS → FS Traceability Matrix

One row per DS-ID per METHODOLOGY § 2B.2 rule 2 (no range compression). A single DS-ID maps to one or more FS-IDs (comma-separated) where the DS-row covers multiple FS-row implementations.

| DS ID | FS ID(s) |
|---|---|
| DS-NET-01 | FS-ARCH-01, FS-ARCH-02, FS-ARCH-03 |
| DS-NET-02 | FS-ARCH-04, FS-ARCH-05 |
| DS-NET-03 | FS-ARCH-06, FS-ARCH-07 |
| DS-NET-04 | FS-ARCH-08, FS-AUTHZ-01 |
| DS-NET-05 | FS-ARCH-09, FS-AUTHZ-02 |
| DS-NET-06 | FS-ARCH-10, FS-HYB-01 |
| DS-NET-07 | FS-ARCH-04 |
| DS-NET-08 | FS-ARCH-06 |
| DS-NET-09 | (no direct FS — Munich↔Basel link is a topology-only design choice; transitive coverage via FS-ARCH-04 + FS-ARCH-06) |
| DS-IDENT-01 | FS-ARCH-01 |
| DS-IDENT-02 | FS-ARCH-02 |
| DS-IDENT-03 | FS-ARCH-03 |
| DS-IDENT-04 | FS-ARCH-04, FS-ARCH-05, FS-ARCH-06 |
| DS-IDENT-05 | FS-ARCH-07, FS-ARCH-08 |
| DS-IDENT-06 | FS-ARCH-09 |
| DS-IDENT-07 | FS-ARCH-10 |
| DS-IDENT-08 | FS-AUTHZ-01, FS-AUTHZ-02 |
| DS-IDENT-09 | FS-AUTHZ-03, FS-AUTHZ-04 |
| DS-IDENT-10 | FS-AUTHZ-05, FS-AUTHZ-06 |
| DS-IDENT-11 | FS-SVC-01, FS-SVC-02, FS-SVC-03, FS-SVC-04, FS-SVC-05, FS-SVC-06, FS-SVC-07 |
| DS-AUTHN-01 | FS-KRB-01, FS-KRB-02, FS-KRB-03, FS-KRB-04, FS-KRB-05, FS-KRB-06, FS-KRB-07, FS-KRB-08 |
| DS-AUTHN-02 | FS-AUTHN-01, FS-AUTHN-02 |
| DS-AUTHN-03 | FS-AUTHN-03 |
| DS-AUTHN-04 | FS-AUTHN-04, FS-HYB-01 |
| DS-AUTHN-05 | FS-AUTHN-05, FS-HYB-02 |
| DS-AUTHN-06 | FS-AUTHN-06, FS-AUTHN-07, FS-AUTHN-08 |
| DS-AUTHN-07 | FS-AUTHN-09 |
| DS-AUTHN-08 | FS-AUTHN-10, FS-AUTHN-11 |
| DS-AUTHN-09 | FS-AUTHN-11 |
| DS-AUTHN-10 | FS-CYB-01, FS-CYB-02 |
| DS-AUTHN-11 | FS-PWD-01, FS-PWD-02, FS-PWD-03, FS-PWD-04, FS-PWD-05, FS-PWD-06, FS-PWD-07 |
| DS-HYB-01 | FS-HYB-01, FS-HYB-02 |
| DS-HYB-02 | FS-HYB-03 |
| DS-HYB-03 | FS-HYB-04 |
| DS-HYB-04 | FS-HYB-05 |
| DS-HYB-05 | FS-HYB-06 |
| DS-HYB-06 | FS-HYB-07 |
| DS-PKI-01 | FS-PKI-01 |
| DS-PKI-02 | FS-PKI-02 |
| DS-PKI-03 | FS-PKI-03 |
| DS-PKI-04 | FS-PKI-04 |
| DS-PKI-05 | FS-PKI-05 |
| DS-PKI-06 | FS-PKI-06 |
| DS-PAM-01 | FS-PAM-01 |
| DS-PAM-02 | FS-PAM-02, FS-PAM-03 |
| DS-PAM-03 | FS-PAM-04, FS-PAM-05 |
| DS-PAM-04 | FS-PAM-06 |
| DS-PAM-05 | FS-PAM-07, FS-PAM-08 |
| DS-PAM-06 | FS-PAM-09 |
| DS-PAM-07 | FS-PAM-10 |
| DS-IGA-01 | FS-JML-01, FS-JML-02 |
| DS-IGA-02 | FS-JML-03, FS-JML-04 |
| DS-IGA-03 | FS-JML-05, FS-JML-06 |
| DS-IGA-04 | FS-IGA-01, FS-IGA-02, FS-IGA-03, FS-IGA-04, FS-IGA-05 |
| DS-IGA-05 | FS-JML-07, FS-JML-08, FS-JML-09, FS-JML-10 |
| DS-GPO-01 | FS-GPO-01, FS-GPO-02 |
| DS-GPO-02 | FS-GPO-03, FS-GPO-04 |
| DS-GPO-03 | FS-GPO-05, FS-GPO-06 |
| DS-GPO-04 | FS-GPO-07, FS-GPO-08 |
| DS-GPO-05 | FS-GPO-09, FS-GPO-10 |
| DS-B2B-01 | FS-B2B-01 |
| DS-B2B-02 | FS-B2B-02 |
| DS-B2B-03 | FS-B2B-03 |
| DS-B2B-04 | FS-B2B-04 |
| DS-B2B-05 | FS-B2B-05 |
| DS-NTP-01 | FS-AN11-01, FS-PART11-01 |
| DS-NTP-02 | FS-AN11-02 |
| DS-NTP-03 | FS-AN11-03 |
| DS-NTP-04 | FS-AN11-04, FS-AN11-05 |
| DS-NTP-05 | FS-MON-01 |
| DS-BAK-01 | FS-BAK-01, FS-BAK-02 |
| DS-BAK-02 | FS-BAK-03 |
| DS-BAK-03 | FS-BAK-04 |
| DS-BAK-04 | FS-BAK-05 |
| DS-BAK-05 | FS-BAK-06 |
| DS-BAK-06 | (cross-system — AUR-FS-BACKUP-001 consumer; transitive via FS-INT-04) |
| DS-HARDEN-01 | FS-CYB-01, FS-CYB-02 |
| DS-HARDEN-02 | FS-CYB-03, FS-CYB-04 |
| DS-HARDEN-03 | FS-CYB-05 |
| DS-HARDEN-04 | FS-CYB-06 |
| DS-HARDEN-05 | FS-CYB-07 |
| DS-HARDEN-06 | FS-CYB-08 |
| DS-HARDEN-07 | FS-CYB-09 |
| DS-HARDEN-08 | FS-CYB-10 |
| DS-HARDEN-09 | FS-CYB-11 |
| DS-HARDEN-10 | FS-CYB-12 |
| DS-HARDEN-11 | FS-CYB-12 |
| DS-HARDEN-12 | FS-AN11-01, FS-AN11-02, FS-AN11-03, FS-AN11-04, FS-AN11-05 |
| DS-AUD-01 | FS-AUD-01, FS-AUD-02, FS-AUD-03, FS-AUD-07, FS-AUD-08 |
| DS-AUD-02 | FS-AUD-04 |
| DS-AUD-03 | FS-AUD-05 |
| DS-AUD-04 | FS-MON-02 |
| DS-AUD-05 | FS-AUD-06 |
| DS-MON-01 | FS-MON-01 |
| DS-MON-02 | FS-MON-03 |
| DS-MON-03 | FS-MON-04 |
| DS-MON-04 | FS-PERF-03 |
| (DS-PART11-NN not introduced as standalone DS-IDs in this DS) | FS-PART11-01 through FS-PART11-16 (sixteen rows) covered transitively by the DS-IDs above — DS-NTP-01 carries FS-PART11-01 explicitly; the DS-AUTHN family carries the authentication substrate for FS-PART11-04 / FS-PART11-06 / FS-PART11-08 / FS-PART11-09 / FS-PART11-10 / FS-PART11-12 / FS-PART11-13 / FS-PART11-15; the DS-AUD family carries the audit-trail substrate for FS-PART11-02 / FS-PART11-03 / FS-PART11-05 / FS-PART11-07; DS-IGA + DS-PAM rows carry the access-control and signature substrate for FS-PART11-04 / FS-PART11-10; DS-HYB rows carry the open-system and biometric substrate for FS-PART11-11 / FS-PART11-14 / FS-PART11-16. No new DS-PART11-NN IDs introduced per § 2B.7 — Part 11 alignment is a transitive property of the design rows, not a free-standing infrastructure design item. |
| (DS-PR-NN, DS-TRN-NN, DS-DP-NN not introduced as standalone DS-IDs in this DS) | FS-PR-01, FS-PR-02, FS-PR-03 (periodic review), FS-TRN-01, FS-TRN-02 (training), FS-DP-01, FS-DP-02, FS-DP-03, FS-DP-04, FS-DP-05, FS-DP-06 (data protection) covered transitively — these FS rows live in the IAM operating SOP set, not in the infrastructure design itself; this DS implements the technical substrate (hardening, monitoring, audit, change-control via DS-HARDEN-12 deviation register) that those FS rows depend on. No new DS-PR-NN / DS-TRN-NN / DS-DP-NN IDs introduced per § 2B.7. |

**Coverage footnote.** Matrix contains 90 per-DS-ID rows + 2 transitive-coverage commentary rows. Of the 178 FS-IDs in `QTZ-FS-AD-001` v1.1, 158 FS-IDs are covered through explicit DS-ID rows above; 20 FS-IDs are covered transitively per the two commentary rows: the sixteen FS-PART11 rows (FS-PART11-01 through FS-PART11-16), the three FS-PR rows (FS-PR-01, FS-PR-02, FS-PR-03), the two FS-TRN rows (FS-TRN-01, FS-TRN-02), the six FS-DP rows (FS-DP-01 through FS-DP-06), the three FS-AV rows (FS-AV-01, FS-AV-02, FS-AV-03), the two consuming-app FS-PERF rows (FS-PERF-01, FS-PERF-02), and the five FS-INT cross-system rows (FS-INT-01 through FS-INT-05). They are not duplicated as standalone DS-ID rows because they describe non-infrastructure concerns — SOP-resident procedures, app-layer signature manifestation, performance SLOs measured at the consuming-app boundary, or cross-system integration patterns documented in consumer DSs. Per § 2B.7(6): no IQ/OQ/PQ rows; infrastructure qualification cited by reference (`QTZ-IQ-AD-001`, `QTZ-IQ-DC-001`, `QTZ-IQ-ADCS-001`, `QTZ-IQ-PAM-001`).

## 12. Design-level Risk Register

| ID | Design-stage risk | Likelihood | Impact | Bound DS-IDs | Mitigation reference |
|---|---|---|---|---|---|
| D-01 | **Tier model boundary violation** — Tier-1 admin workstation gains Tier-0 access via Conditional Access misconfiguration | Low | **Critical** | DS-IDENT-10, DS-HYB-04 | Annual privileged-access review (DS-IGA-05); Tier-0 PAW lockdown (DS-GPO-01) |
| D-02 | **Forest-wide replication failure** undetected → divergent forests | Low | Critical | DS-NET-07, DS-NET-08, DS-NET-09, DS-MON-02 | `repadmin /showrepl` 5-min polling + alert |
| D-03 | **FSMO role-holder failure** during DR drill | Low | High | DS-IDENT-05 | FSMO transfer runbook + annual DR drill |
| D-04 | **ADCS root-CA HSM compromise** | Low | **Critical (forest trust collapse)** | DS-PKI-01 | Offline + HSM + dual-control physical access |
| D-05 | **AD Connect sync failure** in DR-cutover window | Low | High | DS-HYB-01, DS-HYB-02 | Sync-failure alert + failover Federation Server |
| D-06 | **CyberArk Vault outage** during incident-critical window | Low | **Critical** | DS-PAM-01 | HA pair + DR replica + break-glass via dual-witness |
| D-07 | **Break-glass account misuse** | Low | Critical | DS-PAM-05 | SIEM-monitored + 24-h password rotation |
| D-08 | **NTP drift on PDC emulator** beyond 30 s — Kerberos auth breaks | Low | High | DS-NTP-01, DS-NTP-04 | 5-s alert + 30-s isolation; external dual-source (PTB + Google) |
| D-09 | **Backup integrity** corruption undetected | Low | Critical | DS-BAK-04, DS-BAK-05 | Monthly restore test + integrity check |
| D-10 | **Kerberoasting / Pass-the-Hash** attack on service accounts | Low | Critical | DS-IDENT-11 (gMSA) + DS-HARDEN-06 | gMSA preferred; AES-256; Credential Guard |
| D-11 | **GPO precedence misconfiguration** weakens tier baseline | Medium | High | DS-GPO-01, DS-GPO-02, DS-GPO-03, DS-GPO-04, DS-GPO-05 | GPO modeling tool + change-control review |
| D-12 | **LSASS dump** on DC via privileged-malware | Low | Critical | DS-HARDEN-10 | LSA Protected Process Light + Credential Guard |
| D-13 | **Conditional Access policy drift** between Entra ID and AD FS | Medium | High | DS-HYB-04 | Quarterly policy review by IAM Manager |
| D-14 | **PKI cert-expiry** for DC Kerberos cert during business hours | Low | High | DS-PKI-04, DS-MON-04 | D-30 / D-7 / D-1 alerts |
| D-15 | **CyberArk PSM session-recording retention** misconfigured (< 25 y) | Low | Critical | DS-PAM-07 | Annual retention audit |
| D-16 | **NTLMv2 decommissioning** breaks legacy application | Medium | Medium | DS-HARDEN-05 | Phased decommission; per-app dependency mapping |
| D-17 | **External-partner guest expiry** missed → orphan access | Medium | High | DS-B2B-03 | Auto-disable + monthly B2B review |
| D-18 | **BSI IT-Grundschutz deviation** undocumented at audit | Low | High | DS-HARDEN-12 | Deviation register reviewed quarterly |
| D-19 | **DC firewall rule** widened during troubleshooting and not narrowed | Medium | High | DS-NET-04, DS-NET-05 | CR for all firewall changes + quarterly rule review |
| D-20 | **Quartz forest functional level** upgrade blocked by legacy DC | Low | High | DS-IDENT-01 | Pre-upgrade DC inventory + decommission |
| D-21 | **NIS2 incident-reporting clock (24 h / 72 h / final-report)** missed for identity-service incident | Low | **Critical (NIS2 penalty)** | DS-AUD-04 | CSO escalation + incident-response runbook |
| D-22 | **Cross-system identity propagation lag** to a downstream system (Sirius PV, Lyrae, etc.) blocks legitimate auth | Medium | Medium | DS-HYB-06 (SCIM) | SCIM lag monitor + 5-min SLA |
| D-23 | **Group-naming convention drift** causes accidental permission grant | Medium | High | DS-IDENT-09 | Quarterly access review (DS-IGA-04) |
| D-24 | **DR-site warm-replica DC** falls behind during peak inter-site replication backlog | Medium | High | DS-NET-07, DS-NET-08, DS-NET-09 | Replication-lag SLO + auto-alert |
| D-25 | **Forest-recovery time** ≥ 24 h on full-forest authoritative restore | Low | Critical | DS-BAK-04 | Annual tabletop + per-site partial-restore quarterly |
| D-26 | **Service-account password rotation** in CyberArk breaks application | Medium | High | DS-PAM-02 | Pre-rotation app-validation + maintenance window |
| D-27 | **Entra ID workload-identity federation cert** rotation misses an application | Low | High | DS-HYB-05 | Cert-expiry monitor per service-principal |
| D-28 | **Audit-log forwarding to Splunk** lag > 5 min during peak event volume | Medium | Medium | DS-AUD-02 | Forwarder horizontal scaling + buffer policy |
| D-29 | **LAPS rotation** breaks vendor remote-support scenario | Low | Medium | DS-AUTHN-07 | Vendor-rotation maintenance window |
| D-30 | **Smartcard-revocation lag** during compromised-token incident | Low | High | DS-PKI-05, DS-PKI-06 | CRL + OCSP both published; auto-revocation runbook |
| D-31 | **GDPR right-to-erasure** on AD user object conflicts with 25-y retention obligation | Medium | Medium | DS-AUD-03 | Legal-review gate; tombstone vs erase decision |

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
