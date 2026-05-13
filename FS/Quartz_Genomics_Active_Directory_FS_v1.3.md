---
artifact_class: synthetic_csv_corpus_seed
artifact_status: GENERATED
generator: "Claude (Anthropic) — inline FS authoring, 2026-04-27; Wave 3 Chunk J expanded 2026-05-12 (T3 catch-up: per-URS-ID rows for all 178 URS IDs; JML wiring via Workday; FIDO2 + CA policy set; CyberArk PAM topology; Entra PIM; SCIM; gMSA; Defender for Identity; SIEM forwarding; forest-recovery runbook)"
seed_corpus_basis:
  - "QTZ-URS-AD-001 v1.1 (parent URS, T3)"
  - "GAMP 5 (2nd ed., 2022) Cat 3 conventions for IT infrastructure"
  - "21 CFR Part 11 §§ .10, .30, .100, .200, .300"
  - "EU GMP Annex 11 §§ 4, 7, 9, 12"
  - "ISO/IEC 27001:2022 (Annex A.5/A.8/A.9/A.12/A.16/A.17)"
  - "NIST SP 800-63B; NIS2 Directive (EU) 2022/2555; GDPR Art. 32"
  - "ISPE GAMP GPG IT Infrastructure Control and Compliance"
parent_urs:
  document_number: QTZ-URS-AD-001
  version: 1.1
  file: ../../URS/_generated/final/Active_Directory_Identity_Service__Quartz_Genomics_URS_v1.3.md
do_not_use_as: [regulated_record, basis_for_real_validation_decisions]
intended_use: [LLM fine-tuning corpus seed]
labelling:
  evidence_level: synthetic_seeded
  signature_status: placeholders
  production_status: simulated_or_example
  source_risk: ai_authored_disclosed
---

# Functional Specification (FS)

## Active Directory Identity Service — Microsoft AD DS 2022 + Entra ID Hybrid Federation + ADCS PKI + CyberArk PAM

**Document Number:** QTZ-FS-AD-001
**Version:** 1.1
**Effective Date:** 2026-05-12 *(synthetic)*
**Parent URS:** QTZ-URS-AD-001 v1.1
**Site:** Quartz Genomics Ltd, Cambridge UK + Munich DE + Basel CH DR *(fictional)*
**System Class:** GAMP Cat 3 — Non-Configured Product (commercial AD DS deployed to Microsoft Enterprise Access Model + RED-forest reference architecture)
**Regulatory Scope:** 21 CFR Part 11 §§ .10(a/b/c/d/e/g/k), .30, .100, .200, .300; EU GMP Annex 11 §§ 4, 7, 9, 12; ISO/IEC 27001:2022; NIST SP 800-63B; NIS2 Directive (EU) 2022/2555; GDPR Art. 32

> **FS scope note (Cat 3).** This FS proportionately addresses the standard configuration applied at the Quartz tenancy level. AD itself is not a GxP record system — it is the AuthN / AuthZ infrastructure that supports every GxP application at the site. The FS therefore focuses on identity-lifecycle controls, signing-cert PKI, audit forwarding to the SIEM, the Privileged Access Management broker, and the conditional-access policy set for hybrid federation.

## Document Control

| Role | Name | Signature | Date |
|---|---|---|---|
| Author (IT Architect) | _____________ | _____________ | _____ |
| Reviewer (Validation Engineer) | _____________ | _____________ | _____ |
| Reviewer (InfoSec / CISO delegate) | _____________ | _____________ | _____ |
| Reviewer (Data Protection Officer) | _____________ | _____________ | _____ |
| Approver (Head of IT Infrastructure) | _____________ | _____________ | _____ |
| Approver (Head of QA) | _____________ | _____________ | _____ |
| Approver (CISO) | _____________ | _____________ | _____ |

## Revision History

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0 | 2026-04-27 | (synthetic) | Initial issue with collapsed-range traceability. |
| 1.1 | 2026-05-12 | (synthetic) | Wave 3 Chunk J catch-up: per-ID rows expanded for all 178 URS-IDs; corrected FS-ID naming to match URS-ID semantics; added JML / FIDO2 / Entra PIM / CyberArk PAM / SCIM / forest-recovery / Defender-for-Identity / SIEM-forwarding / IGA / B2B / GDPR specifications. |


| 1.3 | 2026-05-13 *(synthetic)* | v1.3 corpus restructuring: added § N Implementation Risk Register (content transferred from URS § 9, removed per v1.3 reframing — implementation risk lives in FS, not URS); URS-side Project Mode line added to Document Control per METHODOLOGY § 2A.15. | Migration Script |## 1. Purpose

This FS specifies how the AD identity service is deployed and configured to satisfy `QTZ-URS-AD-001` v1.1 — providing authentication, authorisation, identity-lifecycle automation, privileged-access management, signing-cert PKI, conditional access, and audit forwarding to the SIEM in support of every GxP application at the site.

## 2. Scope

AD DS 2022 forest (`quartz.local`) + isolated tier-0 administrative forest (`admin.quartz.local`, RED forest pattern, one-way trust + Selective Authentication) + Entra ID hybrid federation (tenant `quartzgenomics.onmicrosoft.com`) + ADCS-issued user / service / signing certificates + CyberArk Privileged Access Management broker (Vault + PSM + CPM + PVWA); Kerberos + LDAPS for on-prem; SAML 2.0 / OIDC via Entra ID for SaaS; SCIM provisioning to SaaS GxP applications; SIEM forwarding (Splunk Enterprise Security via Microsoft Defender for Identity + Universal Forwarder on DCs).

## 3. System Architecture

### 3.1 Component Inventory

| ID | Component | GAMP Cat | Notes |
|---|---|---|---|
| C-01 | AD DS production forest (`quartz.local`) | 3 | 8 DCs across 5 geographies; 2 RODC in DMZ |
| C-02 | Tier-0 administrative forest (`admin.quartz.local`) | 3 | RED forest; one-way trust; Selective Authentication |
| C-03 | Entra ID hybrid tenant | 3 (vendor) | hybrid SSO; conditional access; PIM |
| C-04 | Entra ID Connect (HA pair) | 3 | password-hash-sync; sync filter excludes tier-0 |
| C-05 | ADCS two-tier PKI | 3 | offline root (HSM-protected) + 2 issuing CAs |
| C-06 | CyberArk PAM (Vault + PSM + CPM + PVWA) | 3 (vendor) | brokered privileged sessions; recording; JIT |
| C-07 | Splunk Enterprise Security | (infra) | SIEM destination; 1 y online + 7 y archive |
| C-08 | Microsoft Defender for Identity | 3 (vendor) | AD-aware threat detection; SIEM feed |
| C-09 | FIDO2 hardware-key inventory (YubiKey 5 series) | 3 | tier-0 + step-up + executive |
| C-10 | Intune + Defender for Endpoint | (infra) | device-compliance signal for conditional access |
| C-11 | Privileged Access Workstation (PAW) fleet | 3 | hardened; allow-list (WDAC); no internet |
| C-12 | Workday HRIS (provisioning source) | (external) | JML event source |
| C-13 | SailPoint IdentityIQ (or Entra ID Governance) | 3 (vendor) | IGA: requests, approvals, certifications, toxic-combo |

### 3.2 Logical Architecture (textual)

```
                  ┌────────────────────────────────────────────┐
                  │ Workday HRIS (JML event source)            │
                  └────────────────────┬───────────────────────┘
                                       │ events
                                       ▼
                  ┌────────────────────────────────────────────┐
                  │ Identity Provisioning Pipeline             │
                  │ (Joiner / Mover / Leaver orchestrator)     │
                  └────────────────────┬───────────────────────┘
                                       │
   ┌───────────────────────────────────▼────────────────────────────────┐
   │  AD DS forest quartz.local           ◄──one-way trust──   admin.   │
   │    DCs: Cambridge×3, Munich×2,                            quartz.  │
   │         Singapore, Boston, São Paulo                      local    │
   │    + 2 RODC in DMZ                                                 │
   └───────────────┬─────────────────────┬───────────────┬──────────────┘
                   │                     │               │
                   ▼                     ▼               ▼
        ┌──────────────────┐  ┌─────────────────┐  ┌─────────────────┐
        │ Entra ID Connect │  │ ADCS PKI         │  │ CyberArk PAM   │
        │   (PHS, HA pair) │  │   offline root +│  │   Vault+PSM+CPM│
        └────────┬─────────┘  │   2 issuing CAs │  │   +PVWA        │
                 │            │   (HSM L3)      │  └────────┬───────┘
                 ▼            └─────────────────┘           │
        ┌────────────────┐                                   │
        │ Entra ID tenant│   ◄──Conditional Access engine    │
        │  + PIM         │                                   │
        └────────┬───────┘                                   │
                 │                                           │
        SCIM / SAML / OIDC                          PSM-brokered tier-0/1
                 │                                           │
                 ▼                                           ▼
        SaaS GxP applications                       AD admin actions

   ────────────────────────────────────────────────────────────────────
            AD + Entra + ADCS + PAM → Microsoft Defender for Identity
            → Splunk Enterprise Security (1 y online + 7 y archive)
            → SOC + InfoSec dashboards + Inspector exports
```

## 4. Functional Specifications

Each row maps a URS-ID to its implementation detail. **One row per URS-ID** (per METHODOLOGY § 2A.7). No range compression.

### 4.1 Forest / Domain Architecture (URS § 5.1)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-ARCH-01 | URS-ARCH-01 | Single production forest `quartz.local` deployed; isolated tier-0 administrative forest `admin.quartz.local` (Microsoft RED-forest pattern). Trust: one-way (`quartz.local` trusts `admin.quartz.local`) with Selective Authentication scoped to designated tier-0 admin accounts. Schema versioning under change control. |
| FS-ARCH-02 | URS-ARCH-02 | Eight production DCs deployed: 3× Cambridge UK (primary), 2× Munich DE (EU primary), 1× Singapore (APAC), 1× Boston US (NA), 1× São Paulo BR (LATAM). Replication topology: KCC + manual site-link cost tuning; convergence ≤ 15 min site-to-site. Any single-site loss demonstrated non-impacting in DR test. |
| FS-ARCH-03 | URS-ARCH-03 | Forest functional level + domain functional level pinned to Windows Server 2022. Downgrade explicitly blocked via change-control SOP. |
| FS-ARCH-04 | URS-ARCH-04 | DNS AD-integrated; secure dynamic updates only; scavenging enabled with 14-day no-refresh + refresh interval; DNSSEC signed on `quartz.local` zone with NSEC3 + automated key rollover. DoH / DoT evaluated annually. |
| FS-ARCH-05 | URS-ARCH-05 | Two RODC deployed in DMZ for branch sites (Cambridge-Annex + Singapore-Branch). Password Replication Policy (PRP) denies tier-0 + tier-1 caching; allows scoped branch user set only. RODC compromise scope strictly bounded. |
| FS-ARCH-06 | URS-ARCH-06 | FSMO role placement: Schema + Domain Naming on Cambridge-DC1 (with seizure target Cambridge-DC2); RID + PDC Emulator + Infrastructure on Munich-DC1 (with seizure targets Munich-DC2 + Cambridge-DC3). Runbooks for graceful + emergency seizure documented + rehearsed annually. |
| FS-ARCH-07 | URS-ARCH-07 | Dev forest `quartz-dev.local` in segmented network; no trust to production; out of GxP scope. Used for GPO + schema-change rehearsal. |
| FS-ARCH-08 | URS-ARCH-08 | Trust inventory documented in IAM register. New trust requires Identity Approver pair sign-off + InfoSec review + 30-day pre-prod observation. |
| FS-ARCH-09 | URS-ARCH-09 | DC OS baseline: Windows Server 2022 STIG-aligned (Microsoft Security Baseline preferred where stricter); site-justified exceptions catalogued + reviewed quarterly. |
| FS-ARCH-10 | URS-ARCH-10 | DCs run no other server role (no DHCP / IIS / file share); enforced through monitoring + configuration scans (Defender for Identity health alerts). |

### 4.2 Identity Lifecycle — JML (URS § 5.2)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-JML-01 | URS-JML-01 | Provisioning pipeline subscribes to Workday HRIS event stream; delegated rights configured so non-pipeline accounts (including service-desk operators) cannot create AD users at `Users` OU. Ad-hoc creation blocked by ACL. |
| FS-JML-02 | URS-JML-02 | Attributes populated on creation: `sAMAccountName`, `userPrincipalName` (UPN = email@quartzgenomics.com), `extensionAttribute1`=`employeeID` (HR primary key), `department`, `manager` (DN ref), `physicalDeliveryOfficeName`=location, `accountExpires` for fixed-term, `extensionAttribute2`=`gxpRelevant` (Y/N). |
| FS-JML-03 | URS-JML-03 | Leaver event triggers immediate AD `disable` within ≤ 8 business hours (target ≤ 1 hour for emergency); SCIM de-provisioning fan-out to SaaS within ≤ 4 hours; Kerberos session invalidation via `pwdLastSet` reset; Entra ID sign-in block. |
| FS-JML-04 | URS-JML-04 | Disabled accounts moved to `Disabled-Users` OU; retained 90 days; auto-deleted day 91. `employeeID` reserved in HR DB; never reassigned. SID + `objectGUID` never re-used. |
| FS-JML-05 | URS-JML-05 | Mover event triggers access-review workflow in SailPoint IdentityIQ; pre-move group memberships flagged for re-certification by new manager + QA; non-justified memberships auto-revoked at day 14. |
| FS-JML-06 | URS-JML-06 | Fixed-term contracts: `accountExpires` set to contract end + 1 day; renewal requires Workday HR change-record. Forced expiry log SIEM-forwarded. |
| FS-JML-07 | URS-JML-07 | Service account creation: separate workflow in IGA; owner role assignment; target system declared; renewal date set; URS-JML-* HRIS pipeline does NOT touch service accounts. |
| FS-JML-08 | URS-JML-08 | Privileged accounts: distinct UPN suffix `_adm@admin.quartz.local`; provisioned in tier-0 forest; standard account in production forest. Two account-objects per privileged individual; SoD enforced by forest boundary. |
| FS-JML-09 | URS-JML-09 | Re-hire: HR generates new `employeeID`; AD provisioning treats as joiner; never re-activates prior `objectGUID`. Audit-trail preserves prior identity history. |
| FS-JML-10 | URS-JML-10 | Stale-account scan runs daily; flags ≥ 60 d inactive for review; ≥ 90 d auto-disabled with manager email + QA copy; weekly report to Identity Services Lead. |

### 4.3 Authentication — MFA + Conditional Access (URS § 5.3)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUTHN-01 | URS-AUTHN-01 | Conditional access policy `CA-GxP-MFA` enforces MFA on all GxP application sign-ins; legacy auth blocked tenant-wide via `CA-Block-LegacyAuth`. SMTP-AUTH / POP / IMAP basic-auth refused. |
| FS-AUTHN-02 | URS-AUTHN-02 | Tier-0/1 conditional access policy `CA-Privileged-FIDO2` allows authentication only via FIDO2 (WebAuthn hardware key); TOTP, SMS, voice, email-OTP blocked for privileged roles. |
| FS-AUTHN-03 | URS-AUTHN-03 | Standard users default to FIDO2; Microsoft Authenticator with number-matching + GPS allowed as fallback; SMS authentication method removed from tenant. |
| FS-AUTHN-04 | URS-AUTHN-04 | Entra ID Identity Protection enabled; conditional access policy `CA-RiskBased` evaluates `signInRisk` + `userRisk`; High risk → block; Medium → step-up + DPO awareness; Low → allow + log. |
| FS-AUTHN-05 | URS-AUTHN-05 | Device-compliance signal sourced from Intune; conditional access policy `CA-CompliantDevice-GxP` blocks non-compliant device on GxP apps; unmanaged → routed through Entra App Proxy with session controls + Defender for Cloud Apps. |
| FS-AUTHN-06 | URS-AUTHN-06 | Sign-in frequency policy (CAS) enforces 8-h SIF for GxP apps; refresh-token lifetime 24 h; e-signature gateway in downstream app re-authenticates per Part 11 § 11.200(a). |
| FS-AUTHN-07 | URS-AUTHN-07 | AD account-lockout: 5 attempts / 15-min window → 30-min lockout. Defender for Identity correlates lockout-bursts → SIEM alert → SOC. |
| FS-AUTHN-08 | URS-AUTHN-08 | Risk-based step-up via Entra Identity Protection; anomalous sign-in (impossible-travel, new country, anonymous IP, infected device, leaked credentials, password spray) → step-up + DPO notification per GDPR Art. 32 audit. |
| FS-AUTHN-09 | URS-AUTHN-09 | NTLM disabled domain-wide via GPO; documented legacy exceptions (printer driver subset) tracked in exception register + retirement plan; Event 8004 monitored. |
| FS-AUTHN-10 | URS-AUTHN-10 | `LdapEnforceChannelBinding=2` + `LdapServerIntegrity=2` enforced on all DCs; unsigned LDAP blocked at protocol level; monitoring via Defender for Identity. |
| FS-AUTHN-11 | URS-AUTHN-11 | Certificate-based authentication enabled for high-assurance workflows (regulatory submissions e-sign); CBA cert issued by ADCS template `GxP-HighAssuranceUser`. |

### 4.4 Password and Credential Policy (URS § 5.4)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PWD-01 | URS-PWD-01 | Default Domain Policy: min length 14; no composition rule forcing special chars; max age 0 (no scheduled rotation); password history 24; minimum age 1 day. NIST SP 800-63B aligned. |
| FS-PWD-02 | URS-PWD-02 | Entra Password Protection enabled with custom banned list (company name, season+year, brand patterns). On-prem Password Protection Agent installed on every DC. |
| FS-PWD-03 | URS-PWD-03 | Custom hook to HaveIBeenPwned API (rate-limited) at password-change time; known-breached password rejected with user-friendly error. |
| FS-PWD-04 | URS-PWD-04 | Windows Hello for Business deployed via Intune; passwordless preferred; passwords retained as fallback for legacy apps. |
| FS-PWD-05 | URS-PWD-05 | Privileged passwords vaulted in CyberArk; 20-char generated; rotated on every PAM session checkout (One-Time Password mode). |
| FS-PWD-06 | URS-PWD-06 | Service-desk password reset workflow: IAL2 identity-proof (manager call-back + knowledge factor); force MFA re-enrol next sign-in. |
| FS-PWD-07 | URS-PWD-07 | Service-desk reset audit: ServiceNow ticket-id + operator-id + target-id + timestamp logged + SIEM-forwarded; weekly QA review. |

### 4.5 Authorization — RBAC / ABAC / Groups (URS § 5.5)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUTHZ-01 | URS-AUTHZ-01 | GxP group naming: `GXP_<APP>_<ROLE>_<ENV>` (e.g., `GXP_LIMS_REVIEWER_PROD`). IAM register documents purpose, owner role, review cadence. |
| FS-AUTHZ-02 | URS-AUTHZ-02 | Group membership change via ServiceNow workflow; capture role, justification, approver, effective dates; auto-revocation at end date. |
| FS-AUTHZ-03 | URS-AUTHZ-03 | SoD reporting: nightly SailPoint scan produces SoD-violation report; AD exposes group membership via LDAP query view to compliance reporting. |
| FS-AUTHZ-04 | URS-AUTHZ-04 | Quarterly access-certification campaigns in SailPoint; non-certified members removed automatically within 5 business days. |
| FS-AUTHZ-05 | URS-AUTHZ-05 | Group-nesting depth check via PowerShell daily scan; ≥ 4 deep raises ticket for Identity Approver pair sign-off. |
| FS-AUTHZ-06 | URS-AUTHZ-06 | Entra ID dynamic groups: attribute set declared in IAM register; change-controlled via standard CR. |
| FS-AUTHZ-07 | URS-AUTHZ-07 | Group owner = AD role group (not individual); HR-event-driven ownership change. |
| FS-AUTHZ-08 | URS-AUTHZ-08 | Group creation form requires: business justification, owner role, review cadence, optional planned EOL date. |
| FS-AUTHZ-09 | URS-AUTHZ-09 | Per-app OU delegation: app-team-managed groups via delegated control on `OU=GxPApps,OU=Groups`; cross-team modification denied via ACL. |

### 4.6 Privileged Access Management (URS § 5.6)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PAM-01 | URS-PAM-01 | Tier-0 actions only from PAW; CyberArk PSM proxy enforces source-host restriction; logon from non-PAW workstation blocked at policy + monitored at Defender for Identity. |
| FS-PAM-02 | URS-PAM-02 | Break-glass workflow: ServiceNow ticket → Entra PIM activation request → second-approver out-of-band confirm → 4-h max session → InfoSec witness via PSM live view → automatic deactivation → 5-day retrospective review. |
| FS-PAM-03 | URS-PAM-03 | Domain Admins / Enterprise Admins / Schema Admins membership = 0 by default; JIT activation via PIM (cloud-side) + CyberArk JIT (on-prem); membership auto-removed at session end. |
| FS-PAM-04 | URS-PAM-04 | CyberArk PSM brokers tier-0 + tier-1 sessions: credential never disclosed to user; full session recording (screen + keystroke + command); recordings encrypted + retained ≥ 1 y online + ≥ 7 y archived; tamper-evident via signed segments. |
| FS-PAM-05 | URS-PAM-05 | Two break-glass tier-0 accounts (`brk-emergency-01`, `brk-emergency-02`); credentials sealed in two separate safes (Cambridge HQ + Munich DC); dual-key access; opening triggers SOC alert via physical-access-system integration + automatic ticket. |
| FS-PAM-06 | URS-PAM-06 | PIM approval requires second person not in requestor's reporting chain (configured in PIM); auto-approval disabled for tier-0 roles. |
| FS-PAM-07 | URS-PAM-07 | PSM recording captures: full screen video (10 fps), all keystrokes, all command-line input/output, network protocol metadata; AES-256 at rest; chain-of-custody hash + signing. |
| FS-PAM-08 | URS-PAM-08 | PAW image: Windows 11 Enterprise hardened; WDAC allow-list policy; Defender ASR rules in block mode; no productivity software; egress firewalled to identity endpoints only. |
| FS-PAM-09 | URS-PAM-09 | Privileged-account inventory: Defender for Identity + custom CyberArk export → monthly review by Identity Services Lead; orphaned accounts (no active owner role) disabled within 5 business days. |
| FS-PAM-10 | URS-PAM-10 | Vendor / third-party privileged access: named CyberArk vendor accounts with time-bounded eligibility; shared vendor accounts blocked at IGA-policy level. |

### 4.7 Service Accounts (URS § 5.7)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-SVC-01 | URS-SVC-01 | New service accounts default to gMSA (Group Managed Service Accounts); KDS root key initialised; password rotation interval 30 days; `PrincipalsAllowedToRetrieveManagedPassword` scoped to consuming host group. |
| FS-SVC-02 | URS-SVC-02 | Non-gMSA-compatible: CyberArk-vaulted standard service account; CPM rotates per policy (Tier 1 ≤ 90 d; Tier 2 ≤ 180 d; on-checkout for sensitive). |
| FS-SVC-03 | URS-SVC-03 | Service accounts denied membership in tier-0 groups via SDDL + nightly audit; "Deny logon locally" + "Deny logon through RDP" GPO applied to tier-2 workstations for service accounts. |
| FS-SVC-04 | URS-SVC-04 | Domain Admins / Enterprise Admins / Schema Admins / Account Operators denial enforced via restricted groups + nightly compliance scan. |
| FS-SVC-05 | URS-SVC-05 | Service account `description` attribute carries owning system + owner role; shared-account naming pattern flagged in compliance scan. |
| FS-SVC-06 | URS-SVC-06 | Quarterly service-account review via SailPoint; orphaned (no active owner role) disabled within 30 days. |
| FS-SVC-07 | URS-SVC-07 | Entra ID workload-identity federation for Azure-hosted GxP apps; replaces stored credentials with token-based access via managed identity. |

### 4.8 Group Policy / Endpoint Configuration (URS § 5.8)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-GPO-01 | URS-GPO-01 | `GxP-Workstation-Lock` GPO sets inactivity → screen lock 10 min; require AD re-auth (`InactivityTimeoutSecs=600`). |
| FS-GPO-02 | URS-GPO-02 | `GxP-RemovableMedia-Restrict` GPO: write-block USB on GxP-tagged workstations; read-only on vendor-tagged; exceptions managed via Intune device categories. |
| FS-GPO-03 | URS-GPO-03 | `GxP-Office-Macro-Block` GPO: block macros from internet origin (`BlockContentExecutionFromInternet=1`) for Word/Excel/PowerPoint/Outlook. |
| FS-GPO-04 | URS-GPO-04 | Defender for Endpoint centrally managed via Intune; tamper-protection on; cloud-delivered protection on; ASR rules in block mode (16 rules); attack-surface reduction reports daily. |
| FS-GPO-05 | URS-GPO-05 | Drift detection via Defender configuration health + Intune compliance; weekly drift report to IT Ops; > 5% drift triggers investigation. |
| FS-GPO-06 | URS-GPO-06 | BitLocker XTS-AES-256 enforced on every GxP workstation; recovery keys escrowed in AD `msFVE-RecoveryInformation` + Entra ID; service-desk read access audited. |
| FS-GPO-07 | URS-GPO-07 | Windows LAPS deployed; local-admin password randomised + stored encrypted in AD; read access restricted to `LAPS-Readers` AD group (service-desk-elevated role). |
| FS-GPO-08 | URS-GPO-08 | Constrained Language Mode for PowerShell on tier-2; JEA endpoints on tier-1 + tier-0; PowerShell logging (module + script-block + transcription) enabled. |
| FS-GPO-09 | URS-GPO-09 | WDAC + Defender Application Control allow-list policy; signed allow-list maintained centrally; deviations alerted. |
| FS-GPO-10 | URS-GPO-10 | GPO change pipeline: develop in `quartz-dev.local` → AGPM equivalent (or Git-backed GPO export tool) → Identity Approver pair sign-off → staged deployment (pilot OU → prod OU) → rollback path documented per GPO. |

### 4.9 Kerberos Hygiene (URS § 5.9)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-KRB-01 | URS-KRB-01 | `krbtgt` rotation script (Microsoft-supplied) runs scheduled 180-d cycle (two passes 24 h apart); also triggered on tier-0 personnel-change events. Defender for Identity validates rotation success. |
| FS-KRB-02 | URS-KRB-02 | Kerberos policy: user ticket 10 h; renewable 7 d; service ticket 10 h. Documented exceptions in `KrbExceptions` register. |
| FS-KRB-03 | URS-KRB-03 | Domain-wide supported encryption types restricted to AES-256-HMAC-SHA1-96 + AES-128 (`msDS-SupportedEncryptionTypes=0x18`); DES + RC4-HMAC + MD5 disabled. |
| FS-KRB-04 | URS-KRB-04 | All tier-0 accounts in Protected Users group + `Account is sensitive and cannot be delegated` flag set; nightly compliance check. |
| FS-KRB-05 | URS-KRB-05 | Unconstrained delegation prohibited; daily PowerShell scan identifies `TRUSTED_FOR_DELEGATION` flag set on any account → alert. Constrained + RBCD only, with scope review. |
| FS-KRB-06 | URS-KRB-06 | SPN inventory via Defender for Identity + daily PowerShell export; orphaned SPNs (no live service host) removed within 30 days. |
| FS-KRB-07 | URS-KRB-07 | SIEM correlation rule: anomalous service-ticket request volume (z-score > 3) → HIGH alert to SOC; Defender for Identity Kerberoasting detection enabled. |
| FS-KRB-08 | URS-KRB-08 | All accounts require pre-authentication (`DONT_REQ_PREAUTH=False`); daily compliance scan + auto-remediation. |

### 4.10 Hybrid Cloud — Entra ID + CA (URS § 5.10)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-HYB-01 | URS-HYB-01 | Entra ID Connect HA pair deployed (active + staging-mode standby); sync filter excludes `OU=ServiceAccounts` + `OU=Tier0` + `OU=Disabled-Users`; cycle 30 min default. Optionally Entra Connect Cloud Sync for branch tenants. |
| FS-HYB-02 | URS-HYB-02 | Password-hash-sync (PHS) configured; passwordless / FIDO2 primary; AD FS deliberately NOT deployed to remove on-prem dependency for cloud SaaS auth. |
| FS-HYB-03 | URS-HYB-03 | Conditional access baseline policy set (named `CA-*` policies): block legacy auth, require MFA all users (with break-glass exclusion), require compliant device for GxP, block high-risk, require FIDO2 for privileged. Exported to JSON + change-controlled. |
| FS-HYB-04 | URS-HYB-04 | Entra PIM configured for Global Admin / Privileged Role Admin / Cloud Admin / SharePoint Admin / etc.; eligibility + activation + approval + MFA + justification + time-bound. No standing assignments allowed (policy enforced). |
| FS-HYB-05 | URS-HYB-05 | Entra ID logs (sign-in, audit, provisioning, risk) → Event Hubs (eu-north-1) → Splunk HEC ≤ 5 min latency; data-model normalisation in Splunk Enterprise Security. |
| FS-HYB-06 | URS-HYB-06 | Two cloud-only emergency Global Admin break-glass accounts (`brk-cloud-01`, `brk-cloud-02`): MFA optional (intentionally excluded from CA to provide recovery channel); credentials safe-sealed dual custody; sign-in events HIGH-alert. |
| FS-HYB-07 | URS-HYB-07 | SCIM provisioning to SaaS GxP apps (LMS Vega, ePRO Iolanthe, eQMS Talos); JIT-on-first-sign-on permitted where SCIM unsupported; nightly reconciliation report. |

### 4.11 PKI — ADCS (URS § 5.11)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PKI-01 | URS-PKI-01 | ADCS hierarchy: offline root CA (powered off, HSM-protected Thales Luna L3); two issuing CAs online (Cambridge + Munich); CRL publish interval 60 min; OCSP responder cluster. |
| FS-PKI-02 | URS-PKI-02 | User signing certificate template `GxP-UserSign`; validity 1 y; auto-enrolment via GPO; private key non-exportable. Revocation publishes to CRL + OCSP. |
| FS-PKI-03 | URS-PKI-03 | Device / service templates: `GxP-Computer-Auth`, `GxP-Service-Auth`; auto-enrolment + auto-renewal; under change control. |
| FS-PKI-04 | URS-PKI-04 | Root-CA key ceremony: 2-of-3 quorum PKI Operators physically present; full video record; cryptographically signed witness statement; CISO approval. |
| FS-PKI-05 | URS-PKI-05 | Certificate-template change: ServiceNow CR + pre-prod validation; rollback path documented per template change. |
| FS-PKI-06 | URS-PKI-06 | Annual PQC-readiness assessment: tracks NIST FIPS 203 (ML-KEM) / 204 (ML-DSA) / 205 (SLH-DSA); no operational migration this revision; tracked in cyber roadmap. |

### 4.12 Audit Trail + SIEM Forwarding (URS § 5.12)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AUD-01 | URS-AUD-01 | Advanced Audit Policy via GPO on DCs: account management, logon (success + failure), Kerberos auth, group changes, GPO changes, schema changes, replication, LDAP modifications, AD recycle-bin. |
| FS-AUD-02 | URS-AUD-02 | Splunk Universal Forwarder on every DC; HF (heavy forwarder) for parsing; Splunk indexer cluster receives ≤ 5 min after generation; gap-detection job runs every 5 min; > 10 min gap → SOC alert. |
| FS-AUD-03 | URS-AUD-03 | Splunk Enterprise Security retention: `gxp_identity` index — 1 y hot/warm + 7 y SmartStore cold (S3 with Object Lock). Hash-chain tamper-evidence at index level. |
| FS-AUD-04 | URS-AUD-04 | Tier-0 + break-glass actions: Splunk saved-search auto-routes to InfoSec Officer mailbox; 5-business-day SLA review; evidence retained ≥ 7 y. |
| FS-AUD-05 | URS-AUD-05 | Audit-trail schema: UTC ms-precision timestamp, event ID, subject SID + UPN, target DN, operation, outcome, originating IP, workstation. Normalised against CIM Auth + Change datamodels. |
| FS-AUD-06 | URS-AUD-06 | Privileged-group-membership-change events: Splunk correlation rule → CRITICAL → routes to InfoSec on-call in ≤ 1 min via PagerDuty. |
| FS-AUD-07 | URS-AUD-07 | Monthly attestation report: Splunk report scheduled monthly; volume, failed-forward events, gaps; signed by Identity Services Lead. |
| FS-AUD-08 | URS-AUD-08 | Nightly hash-chain validator job on `gxp_identity` index; mismatch → CRITICAL alert + InfoSec investigation. |

### 4.13 21 CFR Part 11 Sub-Section Alignment (URS § 5.13)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-PART11-01 | URS-PART11-01 | Procedures + controls: this FS + the IT Change Management SOP + the IAM SOP collectively implement § 11.10(a). Document references in FS § 7. |
| FS-PART11-02 | URS-PART11-02 | Identity-event export: Splunk dashboards + scheduled reports produce inspection-ready PDF + CSV + JSON exports for any user / system within retention (§ 11.10(b)). |
| FS-PART11-03 | URS-PART11-03 | Retention protection: SmartStore S3 Object Lock + hash chain → § 11.10(c). |
| FS-PART11-04 | URS-PART11-04 | Access limited via URS-JML / URS-AUTHZ / URS-PAM controls → § 11.10(d). Failed-access events alerted (FS-AUTHN-07). |
| FS-PART11-05 | URS-PART11-05 | Audit trail operational, time-stamped, append-only → § 11.10(e). Implementation FS-AUD-01..08. |
| FS-PART11-06 | URS-PART11-06 | Authority checks enforced at every Kerberos / SAML / OIDC ticket-grant + at downstream-app authorisation evaluation → § 11.10(g). |
| FS-PART11-07 | URS-PART11-07 | Operational + change-management procedures under document control in eQMS → § 11.10(k). |
| FS-PART11-08 | URS-PART11-08 | Open-system controls: TLS 1.2+ enforced; conditional access + risk-based step-up + FIDO2 for privileged → § 11.30. |
| FS-PART11-09 | URS-PART11-09 | Uniqueness: `sAMAccountName` + UPN + `objectGUID` + `objectSID` + `employeeID` all enforced non-reusable; SailPoint reconciliation prevents duplicates → § 11.100. |
| FS-PART11-10 | URS-PART11-10 | Identity-based signature substrate: unique-id from AD + PKI / FIDO2 + re-auth → § 11.200(a). Downstream-app implements signature manifestation. |
| FS-PART11-11 | URS-PART11-11 | Biometric / FIDO2 device-bound credentials: keys never leave authenticator (CTAP2 + Windows Hello attestation) → § 11.200(b). |
| FS-PART11-12 | URS-PART11-12 | Unique user-ID: see FS-PART11-09 → § 11.300(a). |
| FS-PART11-13 | URS-PART11-13 | Periodic authenticator checks: password policy + breached-cred block at every change → § 11.300(b). |
| FS-PART11-14 | URS-PART11-14 | Loss management: lost FIDO2 key → CRM ticket within 1 BD → cert revocation + key-binding removal + step-up re-enrol → § 11.300(c). |
| FS-PART11-15 | URS-PART11-15 | Transaction safeguards: lockout + breached-cred reject → § 11.300(d). |
| FS-PART11-16 | URS-PART11-16 | Authenticator periodic test: Intune device-attestation cycle + FIDO2 firmware update gate → § 11.300(e). |
| FS-AN11-01 | URS-AN11-01 | Annex 11 § 12.1 physical + logical access — implemented across FS-ARCH, FS-AUTHZ, FS-PAM. |
| FS-AN11-02 | URS-AN11-02 | Annex 11 § 12.3 access reviews — quarterly SailPoint campaigns FS-AUTHZ-04. |
| FS-AN11-03 | URS-AN11-03 | Annex 11 § 9 audit trail — FS-AUD-01..08. |
| FS-AN11-04 | URS-AN11-04 | Annex 11 § 4.8 backup — see FS-BAK-* + integration cross-ref to AUR-FS-BACKUP-001. |
| FS-AN11-05 | URS-AN11-05 | Annex 11 § 7.2 restore integrity demonstration — FS-BAK-04 forest-recovery validation. |

### 4.14 Cybersecurity / NIS2 / ISO 27001:2022 (URS § 5.14)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-CYB-01 | URS-CYB-01 | ISMS certified to ISO/IEC 27001:2022; SoA references AD as in scope; Annex A.5/A.8/A.9/A.12/A.16/A.17 controls mapped to FS implementations. |
| FS-CYB-02 | URS-CYB-02 | NIS2 essential-entity classification documented; AD-specific NIS2 risk register maintained alongside GxP register. |
| FS-CYB-03 | URS-CYB-03 | NIS2 incident-reporting playbook: 24-h early warning to BSI (DE) / NCSC-UK / NCSC-CH; 72-h incident notification; 1-month final report. Communications templates pre-approved by legal + DPO. |
| FS-CYB-04 | URS-CYB-04 | Quarterly BloodHound (or equivalent) attack-path enumeration; high-risk paths to tier-0 remediated within 90 days; tracked in Cyber Roadmap. |
| FS-CYB-05 | URS-CYB-05 | Tier-0 admin forest on dedicated VLAN; firewall ruleset documented + reviewed quarterly; PAW egress restricted via Defender for Cloud + firewall to identity endpoints only. |
| FS-CYB-06 | URS-CYB-06 | Conditional access + Identity Protection per FS-AUTHN-04 + FS-AUTHN-08 implement Zero-Trust signal evaluation. |
| FS-CYB-07 | URS-CYB-07 | Annual independent pentest of AD environment by qualified third party (e.g., NCC Group, Mandiant); findings tracked to closure in Cyber Roadmap. |
| FS-CYB-08 | URS-CYB-08 | Biennial red/purple-team exercise targeting tier-0; objectives include golden ticket, DCSync, NTDS theft, ransomware via privileged-cred abuse. |
| FS-CYB-09 | URS-CYB-09 | GDPR Art. 32 / ROPA entry maintained by DPO; AD identity-data processing flows documented; lawful-basis = Art. 6(1)(b) + 6(1)(c). |
| FS-CYB-10 | URS-CYB-10 | BSI IT-Grundschutz ORP.4 + APP.2.2 evidenced for Munich site; gaps tracked in BSI gap register. |
| FS-CYB-11 | URS-CYB-11 | Cyber-incident playbook covers AD-compromise scenarios (golden ticket, DCSync, NTDS theft, ransomware); annual tabletop with InfoSec + IT + QA + Communications + Legal + senior business stakeholder. |
| FS-CYB-12 | URS-CYB-12 | Vendor-risk register tracks CyberArk, Splunk, Microsoft, Tenable, Mandiant, YubiKey, SailPoint; critical CVE → 5-BD evaluation SLA. |

### 4.15 Backup / DR / Forest Recovery (URS § 5.15)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-BAK-01 | URS-BAK-01 | DC system-state backup nightly via Veeam-coordinated job (consumer of AUR-FS-BACKUP-001 service); 90-d online retention + 7-y immutable cloud archive. |
| FS-BAK-02 | URS-BAK-02 | Forest-recovery runbook per Microsoft "Active Directory Forest Recovery Guide"; annual tabletop; biennial full restore in isolated lab; evidence retained ≥ 7 y. |
| FS-BAK-03 | URS-BAK-03 | DC patching via WSUS + Intune; replication health monitored via `repadmin` + Defender for Identity; failure-to-resolution SLO ≤ 4 h. |
| FS-BAK-04 | URS-BAK-04 | AD restore-validation procedure verifies post-restore: schema integrity, SYSVOL FRS/DFSR convergence, krbtgt continuity, FSMO placement, recycle-bin status. Documented + run after every restore test (Annex 11 § 7.2). |
| FS-BAK-05 | URS-BAK-05 | ADCS backup: offline-root HSM key escrow procedure + issuing-CA database backup + certificate-template export; biennial restore test in isolated lab. |
| FS-BAK-06 | URS-BAK-06 | Air-gapped offline AD-state copy maintained on LTO-9 WORM tape; refresh monthly; vault custody per AUR-URS-BACKUP-001 § 5.6. |

### 4.16 Performance / Availability / Capacity (URS § 5.16)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-AV-01 | URS-AV-01 | Availability SLO ≥ 99.95%; SLA reported quarterly; measured per-region by synthetic-transaction probe. |
| FS-AV-02 | URS-AV-02 | RTO ≤ 4 h single-region DC loss (cross-site replication); full forest recovery RTO ≤ 72 h (per FS-BAK-02 runbook). |
| FS-AV-03 | URS-AV-03 | RPO ≤ 24 h system-state; ≤ 1 h replication-lag for in-day changes. |
| FS-PERF-01 | URS-PERF-01 | Kerberos AS+TGS P95 ≤ 200 ms local-site; measured via Defender for Identity + custom Prometheus exporter. |
| FS-PERF-02 | URS-PERF-02 | LDAP-bind P95 ≤ 100 ms from any GxP app server to primary DC. |
| FS-PERF-03 | URS-PERF-03 | DC capacity reviewed quarterly; growth-projection model maintains 2× peak headroom; capacity Capex planned 12 m ahead. |

### 4.17 Monitoring / Operations (URS § 5.17)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-MON-01 | URS-MON-01 | Splunk + Grafana dashboards: replication health, DC heartbeat, FSMO availability, KDC health, account-lockout volume, privileged-group changes, ADCS issuance + revocation rates, Entra Connect sync health, conditional-access denials. |
| FS-MON-02 | URS-MON-02 | Alert routing matrix: CRITICAL → PagerDuty SOC + on-call ≤ 1 min; HIGH → ticketing + dashboard ≤ 5 min; MEDIUM → daily digest. |
| FS-MON-03 | URS-MON-03 | Grafana Operations dashboard + PowerBI Executive dashboard; daily IT-Ops standup review. |
| FS-MON-04 | URS-MON-04 | Synthetic transactions: test user authenticates + requests Kerberos ticket every 5 min from each region; failures alert ≤ 1 min. |

### 4.18 Identity Governance (URS § 5.18)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-IGA-01 | URS-IGA-01 | SailPoint IdentityIQ orchestrates requests, approvals, reviews, certifications across AD + Entra ID + SCIM SaaS targets; pre-built connectors for LIMS, ELN, eQMS, EDMS. |
| FS-IGA-02 | URS-IGA-02 | Nightly toxic-combination scan: rules expressed in SailPoint policy language (e.g., `LIMS_BatchRecord_Author ∧ LIMS_BatchRecord_Approver → violation`); findings to QA + InfoSec workflow in 1 BD. |
| FS-IGA-03 | URS-IGA-03 | Access-request form captures role, justification, expiration, ticket-ref; approver chain enforced by workflow; auto-revocation at expiration. |
| FS-IGA-04 | URS-IGA-04 | Quarterly role-mining job in SailPoint; drift report to Identity Services Lead; deviations to access-review workflow. |
| FS-IGA-05 | URS-IGA-05 | JML-SLA Grafana dashboard; missed-SLA report to Identity Services Lead + Head of QA monthly. |

### 4.19 Third-party / B2B / Vendor Identity (URS § 5.19)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-B2B-01 | URS-B2B-01 | Entra ID B2B guest invitation requires sponsor + business justification + expiration (max 12 m); UI customised to capture metadata in extension attributes. |
| FS-B2B-02 | URS-B2B-02 | Conditional access policy `CA-B2B-MFA` requires MFA at home tenant OR Quartz; cross-tenant access settings tuned to stricter posture. |
| FS-B2B-03 | URS-B2B-03 | Vendor support: CyberArk-brokered session per FS-PAM-10; ad-hoc vendor accounts blocked at IAM policy. |
| FS-B2B-04 | URS-B2B-04 | Quarterly SailPoint guest-review campaign; 30-d inactive → disable; 60-d → remove. |
| FS-B2B-05 | URS-B2B-05 | Entra cross-tenant access settings list partner tenants explicitly; default-deny for other domains. |

### 4.20 Data Protection / Privacy (URS § 5.20)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-DP-01 | URS-DP-01 | Schema attributes used in AD restricted to identity-operations set; sensitive personal data prohibited; quarterly schema review. |
| FS-DP-02 | URS-DP-02 | ROPA entry for AD identity processing maintained by DPO; updated on material change; reviewed annually. |
| FS-DP-03 | URS-DP-03 | Audit-log read access restricted via Splunk RBAC to named Auditor + SOC + InfoSec roles; access-to-audit-log itself is logged in `gxp_meta_audit` index. |
| FS-DP-04 | URS-DP-04 | GDPR Art. 15 export procedure: DPO-issued request → Splunk + AD attribute export → packaged + reviewed → response within statutory timelines. |
| FS-DP-05 | URS-DP-05 | Art. 17 erasure: AD attribute clearance pipeline; identity-event audit retained per § 11.10(c) override documented in ROPA legitimate-interest basis. |
| FS-DP-06 | URS-DP-06 | Entra ID tenant region pinned to EU; cross-border transfers governed by EU SCCs filed with DPO. |

### 4.21 Training / Periodic Review (URS § 5.21)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-TRN-01 | URS-TRN-01 | LMS-recorded training tracks per role (Identity Engineer / Service-Desk / PKI Operator / tier-0 admin); annual retraining; procedure-change retraining. |
| FS-TRN-02 | URS-TRN-02 | Phishing simulation + credential-hygiene training via vendor platform (e.g., KnowBe4); results tracked + remedial assignment automated. |
| FS-PR-01 | URS-PR-01 | Annual Periodic Review package: configuration drift report; audit-log review evidence; access-review completion KPI; deviation summary; recovery-test outcomes; NIS2 compliance status; ISO 27001 surveillance findings. Signed by Identity Services Lead + Head of IT + Head of QA + CISO. |
| FS-PR-02 | URS-PR-02 | Quarterly SailPoint access-certification campaign; non-cert → auto-remove ≤ 5 BD. |
| FS-PR-03 | URS-PR-03 | Annual tabletop exercise: golden ticket / DCSync scenarios with InfoSec + IT + QA + senior business; lessons-learned → CAPA. |

### 4.22 Cross-System Integration (URS § 5.22)

| FS ID | URS ID | Specification |
|---|---|---|
| FS-INT-01 | URS-INT-01 | AD serves authentication for every GxP app at site: Kerberos / LDAPS on-prem; SAML 2.0 / OIDC via Entra ID for SaaS. Application URS files document their AD-integration pattern. |
| FS-INT-02 | URS-INT-02 | Group-membership feed to downstream-app authorisation evaluators via LDAP query / Entra app-role claims. |
| FS-INT-03 | URS-INT-03 | SCIM provisioning channel via Entra ID provisioning service; SCIM endpoint configuration per SaaS app; nightly reconciliation. |
| FS-INT-04 | URS-INT-04 | AD system-state backup consumes the backup service from AUR-FS-BACKUP-001; restore-test cadence aligned to AUR-FS-RST-* in the Backup FS. |
| FS-INT-05 | URS-INT-05 | AD-outage BC playbook documented in IT IM-process SOP; downstream-app URSs document AD-outage tolerance + fallback. |

## 5. Non-Functional Specifications

| NFR ID | Specification |
|---|---|
| NFR-01 | Kerberos AS+TGS P95 ≤ 200 ms local-site |
| NFR-02 | LDAP-bind P95 ≤ 100 ms from app to DC |
| NFR-03 | Availability ≥ 99.95% measured per quarter |
| NFR-04 | Audit-forward latency ≤ 5 min DC → Splunk |
| NFR-05 | SIEM `gxp_identity` retention ≥ 1 y online + ≥ 7 y archived |
| NFR-06 | RTO ≤ 4 h single-region; ≤ 72 h full forest |
| NFR-07 | RPO ≤ 24 h system-state; ≤ 1 h replication-lag |
| NFR-08 | krbtgt rotation 180-d cadence (double-pass) |
| NFR-09 | NIS2 incident notification ≤ 24 h / ≤ 72 h / ≤ 1 month |
| NFR-10 | Restore-test evidence retained ≥ 7 y (URS-AUD-04) + ≥ 25 y where consuming-app requires |

## 6. Configuration Items (CI)

| CI ID | Item | Configured Value |
|---|---|---|
| CI-01 | Production domain | `quartz.local` |
| CI-02 | Tier-0 admin forest | `admin.quartz.local` (RED forest) |
| CI-03 | Entra tenant | `quartzgenomics.onmicrosoft.com` |
| CI-04 | DC count | 8 production + 2 RODC |
| CI-05 | Conditional Access policy set | `CA-GxP-MFA`, `CA-Privileged-FIDO2`, `CA-RiskBased`, `CA-CompliantDevice-GxP`, `CA-B2B-MFA`, `CA-Block-LegacyAuth` |
| CI-06 | MFA matrix | Tier-0/1: FIDO2 only; Standard: FIDO2 default + Authenticator fallback; SMS removed |
| CI-07 | Password policy | NIST SP 800-63B aligned; min 14; no rotation; breached-block |
| CI-08 | Kerberos encryption types | AES-256, AES-128 only |
| CI-09 | krbtgt rotation cadence | 180 d (double pass) + tier-0-personnel-change trigger |
| CI-10 | LDAP signing + channel binding | Enforced (mode 2) |
| CI-11 | gMSA rotation interval | 30 d |
| CI-12 | Audit-forward latency target | ≤ 5 min |
| CI-13 | Splunk retention | 1 y online + 7 y SmartStore cold (S3 Object Lock) |
| CI-14 | Cert validity | User 1 y, Service 1 y, Device 2 y |
| CI-15 | CRL publish interval | 60 min |
| CI-16 | PAM session-recording retention | 1 y online + 7 y archive |
| CI-17 | DR-test cadence | quarterly DC-restore + biennial full forest + annual ransomware tabletop |
| CI-18 | NIS2 notification timeline | early warning 24 h / incident 72 h / final 1 month |
| CI-19 | SCIM provisioning targets | LMS Vega, ePRO Iolanthe, eQMS Talos, EDMS Vellis |
| CI-20 | Break-glass accounts | 2× on-prem tier-0 + 2× cloud-only Global Admin |

## 7. Risks (FS-level)

| Risk | Mitigation |
|---|---|
| Stale account post-termination | FS-JML-03 + Workday event SLA + URS-JML-10 stale-account scan |
| MFA bypass via legacy auth | FS-AUTHN-01 + legacy-auth tenant-wide block (CA-Block-LegacyAuth) |
| CRL / OCSP outage | FS-PKI-01 + monitoring + OCSP responder cluster + CRL caching |
| Replication failure | FS-ARCH-02 + FS-MON-01 + repadmin alerts |
| Audit-forwarding gap | FS-AUD-02 gap-detection job + FS-AUD-08 nightly hash validator |
| Tier-0 credential compromise | FS-PAM-01..10 + FS-KRB-01..08 + FS-CYB-04 attack-path enumeration |
| Entra Connect sync outage | FS-HYB-01 HA pair + FS-HYB-06 break-glass cloud channel |
| GPO drift | FS-GPO-05 + FS-GPO-10 change-control pipeline |
| NIS2 notification miss | FS-CYB-03 pre-approved templates + tabletop rehearsal |
| Object-Lock / SmartStore tier failure | FS-AUD-03 + cross-region replication + quarterly verification |

## 8. References

- QTZ-URS-AD-001 v1.1 (parent URS, T3)
- 21 CFR Part 11 §§ .10, .30, .100, .200, .300
- EU GMP Annex 11 §§ 4, 7, 9, 12
- ISPE GAMP 5 (2nd Edition, 2022)
- ISPE GAMP Good Practice Guide: *IT Infrastructure Control and Compliance*
- NIST SP 800-63B Digital Identity Guidelines
- ISO/IEC 27001:2022 — Annex A.5/A.8/A.9/A.12/A.16/A.17
- NIS2 Directive (EU) 2022/2555 Arts. 21, 23
- GDPR Reg. (EU) 2016/679 Arts. 30, 32
- BSI IT-Grundschutz ORP.4, APP.2.2, NET.1.1
- Microsoft — *Active Directory Domain Services Reference Architecture* (Windows Server 2022)
- Microsoft — *Securing Active Directory* (Tiered Administrative Model + RED forest)
- Microsoft — *Active Directory Forest Recovery Guide*
- Microsoft — *Microsoft Entra ID Connect Documentation*
- Microsoft — *Microsoft Defender for Identity*
- CyberArk — *Privileged Access Manager Architecture* + Session Manager
- SailPoint — *IdentityIQ Architecture*
- Splunk — *Enterprise Security — Identity Datamodel*
- AWS — *S3 Object Lock — Compliance vs Governance retention modes* (referenced for SmartStore cold tier)

## 9. Appendix A — URS → FS Traceability Matrix

One row per URS-ID per METHODOLOGY § 2A.7. No range compression.

| URS ID | FS ID(s) |
|---|---|
| URS-ARCH-01 | FS-ARCH-01 |
| URS-ARCH-02 | FS-ARCH-02 |
| URS-ARCH-03 | FS-ARCH-03 |
| URS-ARCH-04 | FS-ARCH-04 |
| URS-ARCH-05 | FS-ARCH-05 |
| URS-ARCH-06 | FS-ARCH-06 |
| URS-ARCH-07 | FS-ARCH-07 |
| URS-ARCH-08 | FS-ARCH-08 |
| URS-ARCH-09 | FS-ARCH-09 |
| URS-ARCH-10 | FS-ARCH-10 |
| URS-JML-01 | FS-JML-01 |
| URS-JML-02 | FS-JML-02 |
| URS-JML-03 | FS-JML-03 |
| URS-JML-04 | FS-JML-04 |
| URS-JML-05 | FS-JML-05 |
| URS-JML-06 | FS-JML-06 |
| URS-JML-07 | FS-JML-07 |
| URS-JML-08 | FS-JML-08 |
| URS-JML-09 | FS-JML-09 |
| URS-JML-10 | FS-JML-10 |
| URS-AUTHN-01 | FS-AUTHN-01 |
| URS-AUTHN-02 | FS-AUTHN-02 |
| URS-AUTHN-03 | FS-AUTHN-03 |
| URS-AUTHN-04 | FS-AUTHN-04 |
| URS-AUTHN-05 | FS-AUTHN-05 |
| URS-AUTHN-06 | FS-AUTHN-06 |
| URS-AUTHN-07 | FS-AUTHN-07 |
| URS-AUTHN-08 | FS-AUTHN-08 |
| URS-AUTHN-09 | FS-AUTHN-09 |
| URS-AUTHN-10 | FS-AUTHN-10 |
| URS-AUTHN-11 | FS-AUTHN-11 |
| URS-PWD-01 | FS-PWD-01 |
| URS-PWD-02 | FS-PWD-02 |
| URS-PWD-03 | FS-PWD-03 |
| URS-PWD-04 | FS-PWD-04 |
| URS-PWD-05 | FS-PWD-05 |
| URS-PWD-06 | FS-PWD-06 |
| URS-PWD-07 | FS-PWD-07 |
| URS-AUTHZ-01 | FS-AUTHZ-01 |
| URS-AUTHZ-02 | FS-AUTHZ-02 |
| URS-AUTHZ-03 | FS-AUTHZ-03 |
| URS-AUTHZ-04 | FS-AUTHZ-04 |
| URS-AUTHZ-05 | FS-AUTHZ-05 |
| URS-AUTHZ-06 | FS-AUTHZ-06 |
| URS-AUTHZ-07 | FS-AUTHZ-07 |
| URS-AUTHZ-08 | FS-AUTHZ-08 |
| URS-AUTHZ-09 | FS-AUTHZ-09 |
| URS-PAM-01 | FS-PAM-01 |
| URS-PAM-02 | FS-PAM-02 |
| URS-PAM-03 | FS-PAM-03 |
| URS-PAM-04 | FS-PAM-04 |
| URS-PAM-05 | FS-PAM-05 |
| URS-PAM-06 | FS-PAM-06 |
| URS-PAM-07 | FS-PAM-07 |
| URS-PAM-08 | FS-PAM-08 |
| URS-PAM-09 | FS-PAM-09 |
| URS-PAM-10 | FS-PAM-10 |
| URS-SVC-01 | FS-SVC-01 |
| URS-SVC-02 | FS-SVC-02 |
| URS-SVC-03 | FS-SVC-03 |
| URS-SVC-04 | FS-SVC-04 |
| URS-SVC-05 | FS-SVC-05 |
| URS-SVC-06 | FS-SVC-06 |
| URS-SVC-07 | FS-SVC-07 |
| URS-GPO-01 | FS-GPO-01 |
| URS-GPO-02 | FS-GPO-02 |
| URS-GPO-03 | FS-GPO-03 |
| URS-GPO-04 | FS-GPO-04 |
| URS-GPO-05 | FS-GPO-05 |
| URS-GPO-06 | FS-GPO-06 |
| URS-GPO-07 | FS-GPO-07 |
| URS-GPO-08 | FS-GPO-08 |
| URS-GPO-09 | FS-GPO-09 |
| URS-GPO-10 | FS-GPO-10 |
| URS-KRB-01 | FS-KRB-01 |
| URS-KRB-02 | FS-KRB-02 |
| URS-KRB-03 | FS-KRB-03 |
| URS-KRB-04 | FS-KRB-04 |
| URS-KRB-05 | FS-KRB-05 |
| URS-KRB-06 | FS-KRB-06 |
| URS-KRB-07 | FS-KRB-07 |
| URS-KRB-08 | FS-KRB-08 |
| URS-HYB-01 | FS-HYB-01 |
| URS-HYB-02 | FS-HYB-02 |
| URS-HYB-03 | FS-HYB-03 |
| URS-HYB-04 | FS-HYB-04 |
| URS-HYB-05 | FS-HYB-05 |
| URS-HYB-06 | FS-HYB-06 |
| URS-HYB-07 | FS-HYB-07 |
| URS-PKI-01 | FS-PKI-01 |
| URS-PKI-02 | FS-PKI-02 |
| URS-PKI-03 | FS-PKI-03 |
| URS-PKI-04 | FS-PKI-04 |
| URS-PKI-05 | FS-PKI-05 |
| URS-PKI-06 | FS-PKI-06 |
| URS-AUD-01 | FS-AUD-01 |
| URS-AUD-02 | FS-AUD-02 |
| URS-AUD-03 | FS-AUD-03 |
| URS-AUD-04 | FS-AUD-04 |
| URS-AUD-05 | FS-AUD-05 |
| URS-AUD-06 | FS-AUD-06 |
| URS-AUD-07 | FS-AUD-07 |
| URS-AUD-08 | FS-AUD-08 |
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
| URS-PART11-12 | FS-PART11-12 |
| URS-PART11-13 | FS-PART11-13 |
| URS-PART11-14 | FS-PART11-14 |
| URS-PART11-15 | FS-PART11-15 |
| URS-PART11-16 | FS-PART11-16 |
| URS-AN11-01 | FS-AN11-01 |
| URS-AN11-02 | FS-AN11-02 |
| URS-AN11-03 | FS-AN11-03 |
| URS-AN11-04 | FS-AN11-04 |
| URS-AN11-05 | FS-AN11-05 |
| URS-CYB-01 | FS-CYB-01 |
| URS-CYB-02 | FS-CYB-02 |
| URS-CYB-03 | FS-CYB-03 |
| URS-CYB-04 | FS-CYB-04 |
| URS-CYB-05 | FS-CYB-05 |
| URS-CYB-06 | FS-CYB-06 |
| URS-CYB-07 | FS-CYB-07 |
| URS-CYB-08 | FS-CYB-08 |
| URS-CYB-09 | FS-CYB-09 |
| URS-CYB-10 | FS-CYB-10 |
| URS-CYB-11 | FS-CYB-11 |
| URS-CYB-12 | FS-CYB-12 |
| URS-BAK-01 | FS-BAK-01 |
| URS-BAK-02 | FS-BAK-02 |
| URS-BAK-03 | FS-BAK-03 |
| URS-BAK-04 | FS-BAK-04 |
| URS-BAK-05 | FS-BAK-05 |
| URS-BAK-06 | FS-BAK-06 |
| URS-AV-01 | FS-AV-01 |
| URS-AV-02 | FS-AV-02 |
| URS-AV-03 | FS-AV-03 |
| URS-PERF-01 | FS-PERF-01 |
| URS-PERF-02 | FS-PERF-02 |
| URS-PERF-03 | FS-PERF-03 |
| URS-MON-01 | FS-MON-01 |
| URS-MON-02 | FS-MON-02 |
| URS-MON-03 | FS-MON-03 |
| URS-MON-04 | FS-MON-04 |
| URS-IGA-01 | FS-IGA-01 |
| URS-IGA-02 | FS-IGA-02 |
| URS-IGA-03 | FS-IGA-03 |
| URS-IGA-04 | FS-IGA-04 |
| URS-IGA-05 | FS-IGA-05 |
| URS-B2B-01 | FS-B2B-01 |
| URS-B2B-02 | FS-B2B-02 |
| URS-B2B-03 | FS-B2B-03 |
| URS-B2B-04 | FS-B2B-04 |
| URS-B2B-05 | FS-B2B-05 |
| URS-DP-01 | FS-DP-01 |
| URS-DP-02 | FS-DP-02 |
| URS-DP-03 | FS-DP-03 |
| URS-DP-04 | FS-DP-04 |
| URS-DP-05 | FS-DP-05 |
| URS-DP-06 | FS-DP-06 |
| URS-TRN-01 | FS-TRN-01 |
| URS-TRN-02 | FS-TRN-02 |
| URS-PR-01 | FS-PR-01 |
| URS-PR-02 | FS-PR-02 |
| URS-PR-03 | FS-PR-03 |
| URS-INT-01 | FS-INT-01 |
| URS-INT-02 | FS-INT-02 |
| URS-INT-03 | FS-INT-03 |
| URS-INT-04 | FS-INT-04 |
| URS-INT-05 | FS-INT-05 |

## 10. Implementation Risk Register

The risks below are properties of the **implementation** (configuration, integration, runtime, operation) of this system, not properties of the user requirements themselves. They are surfaced here for input to the formal Risk Assessment deliverable (FMEA / HAZOP — separate document `<DOC-PREFIX>-RA-NN`). Per-requirement GxP-criticality (R1/R2/R3) remains on each URS requirement and is not duplicated here.

**Origin:** transferred from the URS § 9 Top-level Risks section as part of v1.3 corpus restructuring (LLM Council verdict + user directive 2026-05-13). The transferred content is verbatim from URS; future review may re-frame entries to FS-implementation language or re-distribute to the formal RA artefact.

| ID | Risk | Likelihood | Impact | Mitigation reference |
|---|---|---|---|---|
| R-AD-01 | Tier-0 credential compromise (golden ticket, DCSync, NTDS.dit theft) | Low | Critical | URS-PAM-01..10; URS-KRB-01..08; URS-AUTHN-02; URS-CYB-04..05 |
| R-AD-02 | Stale leaver account remains active beyond SLA | Low | High | URS-JML-03 + URS-JML-10 + URS-PR-02 |
| R-AD-03 | GPO drift on a GxP workstation | Medium | Medium | URS-GPO-05 + URS-GPO-10 |
| R-AD-04 | Audit-forwarding gap masking a security incident | Low | High | URS-AUD-02 + URS-AUD-08 |
| R-AD-05 | Forest compromise via schema modification | Very Low | Critical | URS-PAM-03 + URS-BAK-02 + URS-AUD-06 |
| R-AD-06 | Replication failure isolating a region | Low | Medium | URS-ARCH-02 + URS-BAK-03 + URS-MON-01 |
| R-AD-07 | Ransomware encrypting AD itself via privileged-credential abuse | Low | Critical | URS-CYB-11 + URS-BAK-06 + URS-PAM-04 |
| R-AD-08 | Phishing-driven privileged-account takeover | Low | Critical | URS-AUTHN-02 + URS-TRN-02 |
| R-AD-09 | Shared account introduced by an application team | Low | High | URS-JML-08 + URS-AUTHZ-03 + URS-PART11-09 |
| R-AD-10 | NIS2 incident-reporting timeline missed (24 h / 72 h / 1 month) | Low | High | URS-CYB-03 + URS-PR-03 |
| R-AD-11 | Entra Connect synchronisation outage | Medium | Medium | URS-HYB-01 + URS-HYB-06 + URS-MON-01 |
| R-AD-12 | ADCS root-CA key compromise | Very Low | Critical | URS-PKI-01 + URS-PKI-04 + URS-BAK-05 |
| R-AD-13 | Kerberoasting on weakly-protected service account | Low | High | URS-KRB-07 + URS-SVC-01..05 |
| R-AD-14 | Conditional-access misconfiguration locking out legitimate users | Low | Medium | URS-HYB-03 + URS-HYB-06 (break-glass) + URS-GPO-10 |
| R-AD-15 | GDPR Art. 32 finding on insufficient access-log protection | Low | High | URS-CYB-09 + URS-AUD-03 + URS-AUD-08 |

Full evaluation in `QTZ-RA-AD-001` (synthetic).

### 9.1 NIS2 Compliance Risks (cross-reference)

NIS2 introduces specific obligations (Art. 21 cybersecurity risk-management + Art. 23 incident reporting + Art. 32 supervision). The following AD-specific NIS2 risks are tracked alongside the GxP risk register:

- *Late incident notification:* missing the 24-hour early warning to the competent authority (BSI in DE / NCSC-CH in CH / NCSC-UK in UK) is itself a sanctionable NIS2 failure. (Mitigation: URS-CYB-03 + URS-PR-03 tabletop rehearsal.)
- *Insufficient supply-chain security:* a compromise originating in a vendor product (PAM, SIEM, IDP, MFA) is treated by NIS2 as an in-scope incident. (Mitigation: URS-CYB-12 vendor-risk register.)
- *Inadequate board-level governance:* NIS2 holds senior management accountable for cybersecurity. (Mitigation: CISO + Head of IT co-approval of this URS.)

---

**END OF DOCUMENT — synthetic CSV training artifact, not a regulated record.**
